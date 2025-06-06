## **I. Security Fundamentals**

- **Security Model**: In distributed systems, _principals_ (users/processes) access _objects_ (resources like files or mailboxes). Security depends on knowing the principal’s identity and rights.
    
- **Threats**:
    
    - Attacks target both processes and communications.
        
    - Examples: Data theft, denial of service (e.g., flooding a server).
        
- **Secure Channels**:
    
    - Achieved using **cryptography**.
        
    - Based on shared secrets or public/private key pairs.
        
    - **Authentication** proves identity by demonstrating knowledge of the secret.
        

---

## **II. Types of Threats and Attacks**

- **Eavesdropping**: Unauthorized listening (e.g., reading unencrypted emails).
    
- **Masquerading**: Pretending to be someone else.
    
- **Message Tampering**: Altering messages in transit (e.g., man-in-the-middle).
    
- **Replaying**: Resending old valid messages to trick the receiver.
    
- **Denial of Service (DoS)**: Overloading a system (e.g., IP spoofing attack).
    

**Note**: Secure channels can’t stop DoS attacks or malicious code like **viruses** or **Trojan horses**.

- **Defenses**:
    
    - **Signed code** (authentication).
        
    - **Code validation** (checking logic/safety).
        
    - **Sandboxing** (restricting code access).
        

---

## **III. Cryptographic Techniques and Scenarios**

### 1. **Shared Secret Key Communication**

- Example: Alice and Bob use a shared key `K_AB` to encrypt/decrypt messages.
    
- Issues: Secure key distribution and avoiding replay attacks.
    

### 2. **Authentication with a Server (Kerberos-like)**

- An auth server (e.g., Sara) issues a **ticket** with a shared key.
    
- Example: Alice asks Sara to communicate with Bob → Sara gives `K_AB`.
    
- Problems: Replay attacks and scalability.
    

### 3. **Public Key Authentication**

- Bob has a public/private key pair.
    
- Alice uses Bob’s **public key** to send a **new shared key**, which Bob decrypts.
    
- Risk: Mallory may intercept and substitute Bob’s key.
    

### 4. **Digital Signatures**

- Alice signs a document by encrypting its hash with her **private key**.
    
- Bob verifies by decrypting with Alice’s **public key** and comparing hashes.
    
- **Birthday attack**: Alice could manipulate documents to produce the same hash → secure digests must be at least **128 bits**.
    

---

## **IV. Certificates and Credentials**

- **Certificates**: Authority-signed statements (e.g., public-key certificates).
    
- **X.509 Format**: Includes subject info, public key, issuer, validity, etc.
    
- **Credentials**: Certificates used to prove access rights.
    
    - Example: A university membership certificate + email certificate used together.
        
- The **"speaks for"** concept allows certificates to represent users.
    

---

## **V. Access Control and Delegation**

- **Access Control**:
    
    - **Access Control Lists (ACLs)**: Rights stored with objects.
        
        - Example: Unix file permissions.
            
    - **Capabilities**: Tokens held by users to access resources.
        
        - Drawback: Hard to revoke and easy to steal if not protected.
            
- **Delegation**:
    
    - Temporarily granting access to another principal.
        
    - **Delegation Certificates** or **Capabilities** used.
        
    - Example: A file server lets a user temporarily share a file link with someone else.
        

---

## **VI. Cryptographic Algorithms**

- **Symmetric (Secret Key)**:
    
    - Same key for encryption/decryption (e.g., **AES, DES**).
        
    - Efficient but needs secure key sharing.
        
- **Asymmetric (Public Key)**:
    
    - Public/private key pair (e.g., **RSA, ECC**).
        
    - Secure but slower, used mainly for key exchange/authentication.
        
- **Hybrid Protocols** (e.g., **SSL/TLS**):
    
    - Use asymmetric encryption to share a **symmetric session key**.
        
- **Cipher Techniques**:
    
    - **Cipher Block Chaining (CBC)**: Prevents repetition-based attacks.
        
    - **Stream Ciphers**: Encrypt bit by bit using a keystream.
        

---

## **VII. Digital Signatures & Secure Digests**

- **Digital Signatures**:
    
    - Prove origin and integrity of documents/messages.
        
    - Prevents **repudiation** (denial of signing).
        
- **Secure Digest Functions**:
    
    - Compute fixed-length, hard-to-reverse hashes (e.g., **SHA, MD5**).
        
    - Must resist **birthday attacks**.
        
- **MACs (Message Authentication Codes)**:
    
    - Signatures using a **shared key**.
        
    - Faster but only work between trusted parties.
        

---

## **VIII. Performance & Secure Protocols**

- **Algorithm Speeds**:
    
    - Symmetric → Fast.
        
    - Asymmetric → Slow (used only at session start).
        
    - Digest → Very fast.
        
- **SSL (Secure Socket Layer)**:
    
    - Ensures secure internet communication.
        
    - Used in **HTTPS**, **online banking**, etc.
        
    - Key features:
        
        - Negotiates session keys.
            
        - Uses **hybrid cryptography**.
            
        - Protects web traffic without prior key exchange.
            
- **SSL Protocol Stack**:
    
    - Includes handshake, record, alert, and change cipher protocols.
        
    - Built on **TCP/IP**.
        
- **SSL Handshake**:
    
    - Establishes keys, supported ciphers, and certificates.
        
    - Generates **session keys** and **MAC keys**.
        

---

## **IX. Summary**

- Security in distributed systems involves:
    
    - Protecting resources, channels, and interfaces.
        
    - Using cryptographic methods like symmetric/asymmetric encryption.
        
    - Authenticating principals via certificates and signatures.
        
    - Secure protocols like **Kerberos** and **SSL/TLS** are key components.
