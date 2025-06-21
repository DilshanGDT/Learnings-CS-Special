## Quiz 01 - C Programming on Forks
Write a programme based on processes to compute the sum of the an array of data using two processes, child and parent. one should only compute the sum of half of the elements and the parent process should finally compute the grand total.

Assume the following array : Arr[] = {15, 43, 56, 43, 78, 49, 50, 10, 30, 40}

The solution should be a general solution which should work with any int array of any size.
  
For example:

|Test|Input|Result|
|---|---|---|
|int Arr[] = {15, 43, 56, 43, 78, 49, 50, 10, 30, 40};|15, 43, 56, 43, 78, 49, 50, 10, 30, 40|partial sum : 235 partial sum : 179 get value : 235<br>Grand Sum : 414|
```
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h>

// compute sum
int computeSum(int arr[], int start, int end) {
    
    int sum = 0;
    for (int i = start ; i < end ; i++) {
        sum += arr[i];
    }
    return sum;
}

int main() {
    // We can change the array size and the elements
    int arr[] = {15, 43, 56, 43, 78, 49, 50, 10, 30, 40};
    
    int n = sizeof(arr) / sizeof(arr[0]);
    int fd[2];

    if (pipe(fd) == -1) {
        perror("Pipe failed");
        return 1;
    }

    pid_t pid = fork();
    if (pid < 0) {
        perror("Fork failed");
        return 1;
    }

    // Child Process
    if (pid == 0) {         
        close(fd[0]); 
        int childSum = computeSum(arr, 0, n / 2);
        printf("partial sum : %d ", childSum);
        
        write(fd[1], &childSum, sizeof(childSum));
        close(fd[1]);
        exit(0);
        
    // Parent Process
    } else { 
        close(fd[1]);
        int parentSum = computeSum(arr, n / 2, n);
        printf("partial sum : %d ", parentSum);
        
        int childSum;
        read(fd[0], &childSum, sizeof(childSum));
        close(fd[0]);
        printf("get value : %d\n", childSum);
        
        int grandTotal = childSum + parentSum;
        printf("Grand Sum : %d\n", grandTotal);
        
        wait(NULL);
    }
    return 0;
}
```

## Quiz 02 - C Programming on Locks
Write the programme with best locking strategies to handle the following scenario.

Thread 1 should increment the value of x at each iteration by 1, where Thread 2 should increment the value of y by 2 at each iteration. Thread 3 should be computing the sum of variables x and y, where the initial values of x and y are 0.   

Apply mutex knowledge to achieve proper locking strategy for the given scenario.

Use the following in the main function to display the sum after the threads run. and set the iterations to 10, 100, 1000, and 10000 to check the validity. 

printf("SUM : %d\n",sum);  

For example:

|Test|Input|Result|
|---|---|---|
|n=100;|100|SUM : 300|
|n=10000;|10000|SUM : 30000|
```
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>

int valueX, valueY, totalSum, iterationCount;
pthread_mutex_t mutexLock;

void *incrementX(void *arg) {
    for (int i = 0; i < iterationCount; i++) {
        pthread_mutex_lock(&mutexLock);
        valueX++;
        pthread_mutex_unlock(&mutexLock);
    }
    return NULL;
}

void *incrementY(void *arg) {
    for (int i = 0; i < iterationCount; i++) {
        pthread_mutex_lock(&mutexLock);
        valueY += 2;
        pthread_mutex_unlock(&mutexLock);
    }
    return NULL;
}

void runTest() {
    while (scanf("%d", &iterationCount) == 1) {  

        valueX = 0;
        valueY = 0;
        totalSum = 0;
        
        pthread_mutex_init(&mutexLock, NULL);

        pthread_t threadOne, threadTwo;

        pthread_create(&threadOne, NULL, incrementX, NULL);
        pthread_create(&threadTwo, NULL, incrementY, NULL);

        pthread_join(threadOne, NULL);
        pthread_join(threadTwo, NULL);

        pthread_mutex_lock(&mutexLock);
        totalSum = valueX + valueY;
        pthread_mutex_unlock(&mutexLock);

        printf("SUM : %d\n", totalSum);
        fflush(stdout);  

        pthread_mutex_destroy(&mutexLock);
    }
}

int main(void) {
    runTest();
    return 0;
}

```

## Quiz 03 - Go Lang
Write a go programme to perform the following.  
Implement a Map-Reducer to count the occurrences of unique study programmes of the students, and possibly to arrange them in ascending order. Consider multiple Go routines performing Mapping and one Go routine performing the reducing function to validate your programme.   
  
Dataset : [https://www.kaggle.com/datasets/shariful07/student-mental-health](https://www.kaggle.com/datasets/shariful07/student-mental-health)  
  
* You can use the [Go Playground](https://go.dev/play/p/5jpkxJ2T0Lv) to code and execution if you do not have Go lang installed and configured in your computer.

```
package main

import (
	"encoding/csv"
	"fmt"
	"os"
	"sort"
	"sync"
	"runtime"
)

// Processes a slice of records and counts occurrences
func mapper(records [][]string, out chan<- map[string]int, wg *sync.WaitGroup) {
	defer wg.Done()
	programCounts := make(map[string]int)

	for _, row := range records {
		if len(row) >= 3 {
			studyProgram := row[2]
			programCounts[studyProgram]++
		}
	}

	out <- programCounts
}

// Combines results from all mappers
func reducer(in <-chan map[string]int) map[string]int {
	aggregate := make(map[string]int)

	for partial := range in {
		for program, count := range partial {
			aggregate[program] += count
		}
	}

	return aggregate
}

func main() {
	// Open the dataset
	csvFile, err := os.Open("student_mental_health.csv")
	if err != nil {
		fmt.Println("Failed to open file:", err)
		return
	}
	defer csvFile.Close()

	// Reading all rows
	csvReader := csv.NewReader(csvFile)
	rows, err := csvReader.ReadAll()
	if err != nil {
		fmt.Println("Failed to read CSV data:", err)
		return
	}

	if len(rows) > 0 {
		rows = rows[1:]
	}

	// Dynamically set the number of mappers based on available CPUs
	cpuCores := runtime.NumCPU()
	batchSize := (len(rows) + cpuCores - 1) / cpuCores
	channel := make(chan map[string]int, cpuCores)
	var wg sync.WaitGroup

	// Launch mapper goroutines for chunks of data
	for i := 0; i < cpuCores; i++ {
		startIdx := i * batchSize
		endIdx := startIdx + batchSize
		if endIdx > len(rows) {
			endIdx = len(rows)
		}

		if startIdx >= len(rows) {
			break
		}

		wg.Add(1)
		go mapper(rows[startIdx:endIdx], channel, &wg)
	}

	// Close the channel once all mappers are done
	go func() {
		wg.Wait()
		close(channel)
	}()

	// Run reducer
	finalResult := reducer(channel)

	// Sort names alphabetically
	var programList []string
	for program := range finalResult {
		programList = append(programList, program)
	}
	sort.Strings(programList)

	// Display the sorted results
	fmt.Println("Study Programs (Alphabetical Order):")
	for _, prog := range programList {
		fmt.Printf("%s: %d\n", prog, finalResult[prog])
	}
}
```

## Quiz 04 - Zookeeper

Lets assume we use [Zookeeper](https://scilms.pdn.ac.lk/mod/resource/view.php?id=7027 "ZooKeeper") to implement master fail-over for our distributed application. Each application instance acts as a [ZooKeeper](https://scilms.pdn.ac.lk/mod/resource/view.php?id=7027 "ZooKeeper") client, and each instance is willing to take over as master if there is no live master. We will first manually create a _regular_ znode /app/master. The value of this znode is either “none” (if there is no master) or the ID of the application instance that is the current master. Each application instance does the following in order to learn who the master is, and perhaps to take over as master if needed:

1. Run getData("/app/master", watch) to find out who (if anyone) is the current master, where watch is a notification handler.

2. If the read returns an instance ID IDM, and IDM is not the current instance, the instance becomes a backup with IDM as master.

3. If the result is “none”, the instance uses setData("/app/master", <instanceID, -1> to write its instance ID into the znode. If the write returns successfully, the instance becomes the master; otherwise it starts again at step 1.

4. When watch triggers, it causes the instance to go to step 1 in order to try to become master.

Q1. When testing our implementation, we notice that the system never chooses a new master after the existing master fails, no matter how long he waits. Explain why.

The issue arises because ephemeral nodes are not used. The master writes to a regular znode (/app/master), which stays even after a crash. Since it’s not ephemeral, ZooKeeper doesn’t delete it when the session ends, and no change is detected by the backups. As a result, they assume the master is still up and take no action.

Q2. Also, at certain instances, it ends up with several masters (i.e., split brain). Explain why?

This happens due to a race condition in the master election. Two backups see "/app/master" as "none" and both try setData("/app/master", <theirID>, -1). One write goes through, but the other might still retry and succeed later because getData and setData aren’t atomic together. This can result in multiple masters being elected.

Q3. Diagrammatically elaborate how these two happens
![[ZooKeeper.pdf]]

Q4. Provide your solution.

Q1 - Use an ephemeral znode for /app/master as create("/app/master", instanceID, EPHEMERAL). If the master crashes, ZooKeeper make sure to auto-deletes the znode and triggering watches. Then elect a new master by detecting "none" by the backups.

Q2 - Use atomic creation along with the ephemeral for master election. This ensure only one instance can create /app/master (atomicity). Sequential flags and version controlling prevent if any collision happens.

## Quiz 05 - Linearizability
![[WhatsApp Image 2025-05-09 at 14.20.22_8b9e80a6.jpg]]

![[lin.jpg]]

## Quiz 06 - Raft

Q. There are five RAFT servers. S1 is the leader in term 17. S1 and S2 become isolated in a network partition. S3, S4, and S5 choose S3 as the leader for term 18. S3, S4, and S5 commit and execute commands in term 18. S1 crashes and restarts, and S1 and S2 run many elections, so that their currentTerms are 50. S3 crashes but does not re-start, and an instant later the network partition heals, so that S1, S2, S4, and S5 can communicate. Could S1 become the next leader? How could that happen, or what prevents it from happening? Your answer should refer to specific rules in the RAFT paper, and explain how the rules apply in this specific scenario.

No, S1 cannot become the next leader.
S1 and S2 logs are stale by log comparison since the term 18 entries were committed by S3, S4, and S5. Then S4 and S5 will reject S1’s vote requests because its log is not up-to-date, as per the rule discussed in the Raft paper. S1 can only get votes from itself and S2, not the required 3. This will represent that there is no majority for S1. Finally, a leader must have the most up-to-date log as described in the paper, but S1’s log is outdated, so the election fails.

