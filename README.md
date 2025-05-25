# EX-NO-9-RSA-Algorithm

## AIM:
To Implement RSA Encryption Algorithm in Cryptography

## Algorithm:


Step 1: Design of RSA Algorithm  
The RSA algorithm is based on the mathematical difficulty of factoring the product of two large prime numbers. It involves generating a public and private key pair, where the public key is used for encryption, and the private key is used for decryption.

Step 2: Implementation in Python or C 
This algorithm can be implemented in languages like Python or C by performing large integer calculations for key generation, encryption, and decryption, utilizing libraries for modular arithmetic if necessary.

Step 3: Algorithm Description  
1. Key Generation:
   - Select two large prime numbers \( p \) and \( q \).
   - Calculate \( n = p \times q \), which will be used as the modulus.
   - Compute the totient \( \phi(n) = (p - 1)(q - 1) \).
   - Choose a public exponent \( e \) such that \( e \) is coprime with \( \phi(n) \).
   - Compute the private key \( d \), which is the modular inverse of \( e \) mod \( \phi(n) \).

2. Encryption:
   - Convert the plaintext message \( M \) into a numerical form \( m \) (such that \( 0 \le m < n \)).
   - Compute the ciphertext \( c \) using the formula: \( c = m^e \mod n \).

3. Decryption:
   - Use the private key \( d \) to recover \( m \) from \( c \) using: \( m = c^d \mod n \).
   - Convert \( m \) back into the original message \( M \).

Step 4: Mathematical Representation  
- Encryption: \( E(m) = m^e \mod n \)
- Decryption: \( D(c) = c^d \mod n \)

Step 5: **Security Foundation  
The security of RSA relies on the difficulty of factoring large numbers; thus, choosing sufficiently large prime numbers for \( p \) and \( q \) is crucial for security.

## Program:


```
#include <stdio.h>
#include <string.h>
#include <math.h>

int gcd(int a, int b) {
    while (b != 0) {
        int temp = b;
        b = a % b;
        a = temp;
    }
    return a;
}

int modExp(int base, int exp, int mod) {
    int result = 1;
    base = base % mod;
    while (exp > 0) {
        if (exp % 2 == 1) {
            result = (result * base) % mod;
        }
        exp = exp >> 1;
        base = (base * base) % mod;
    }
    return result;
}

int modInverse(int a, int m) {
    int m0 = m, t, q;
    int x0 = 0, x1 = 1;
    
    if (m == 1)
        return 0;

    while (a > 1) {
        q = a / m;
        t = m;
        m = a % m;
        a = t;
        t = x0;
        x0 = x1 - q * x0;
        x1 = t;
    }

    if (x1 < 0)
        x1 += m0;

    return x1;
}

int main() {
    int p = 61, q = 53;  
    int n = p * q;     
    int phi = (p - 1) * (q - 1); 
    int e = 17;        
    while (gcd(e, phi) != 1) {
        e++;
    }
    
    int d = modInverse(e, phi); 
    
    char plaintext[100];
    printf("Enter the plaintext: ");
    scanf("%s", plaintext);
    
    int encryptedMessage[100];
    int decryptedMessage[100];
  
    printf("Encrypted Message: ");
    for (int i = 0; i < strlen(plaintext); i++) {
        encryptedMessage[i] = modExp(plaintext[i], e, n);
        printf("%d ", encryptedMessage[i]);
    }
    printf("\n");
  
    printf("Decrypted Message: ");
    for (int i = 0; i < strlen(plaintext); i++) {
        decryptedMessage[i] = modExp(encryptedMessage[i], d, n);
        printf("%c", (char)decryptedMessage[i]);
    }
    printf("\n");
    
    return 0;
}

```

## Output:

![image](https://github.com/user-attachments/assets/95f85fef-56a4-43f1-99d1-f730d9fd547d)





## Result:
 The program is executed successfully.
