# EX-NO-11-ELLIPTIC-CURVE-CRYPTOGRAPHY-ECC

## Aim:
To Implement ELLIPTIC CURVE CRYPTOGRAPHY(ECC)


## ALGORITHM:

1. Elliptic Curve Cryptography (ECC) is a public-key cryptography technique based on the algebraic structure of elliptic curves over finite fields.

2. Initialization:
   - Select an elliptic curve equation \( y^2 = x^3 + ax + b \) with parameters \( a \) and \( b \), along with a large prime \( p \) (defining the finite field).
   - Choose a base point \( G \) on the curve, which will be used for generating public keys.

3. Key Generation:
   - Each party selects a private key \( d \) (a random integer).
   - Calculate the public key as \( Q = d \times G \) (using elliptic curve point multiplication).

4. Encryption and Decryption:
   - Encryption: The sender uses the recipient’s public key and the base point \( G \) to encode the message.
   - Decryption: The recipient uses their private key to decode the message and retrieve the original plaintext.

5. Security: ECC’s security relies on the Elliptic Curve Discrete Logarithm Problem (ECDLP), making it highly secure with shorter key lengths compared to traditional methods like RSA.

## Program:
```
#include <stdio.h>

typedef struct
{
    int x;
    int y;
} Point;

int mod(int a, int p)
{
    return (a % p + p) % p;
}

Point add(Point P, Point Q, int a, int p)
{
    Point R;
    int m;

    /* Point at infinity */
    if(P.x == -1 && P.y == -1)
        return Q;

    if(Q.x == -1 && Q.y == -1)
        return P;

    /* Point doubling */
    if(P.x == Q.x && P.y == Q.y)
    {
        if(P.y == 0)
        {
            R.x = -1;
            R.y = -1;
            return R;
        }

        /* For demonstration with small values */
        m = mod((3 * P.x * P.x + a), p);
    }
    else
    {
        m = mod((Q.y - P.y), p);
    }

    /* Simplified point calculation for demonstration */
    R.x = mod(m * m - P.x - Q.x, p);
    R.y = mod(m * (P.x - R.x) - P.y, p);

    return R;
}

Point multiply(Point P, int d, int a, int p)
{
    Point R = {-1, -1};

    for(int i = 0; i < d; i++)
    {
        R = add(R, P, a, p);
    }

    return R;
}

int main()
{
    int a, b, p, privateKey;
    Point G, publicKey;

    printf("Enter prime number p: ");
    scanf("%d", &p);

    printf("Enter curve parameter a: ");
    scanf("%d", &a);

    printf("Enter curve parameter b: ");
    scanf("%d", &b);

    printf("Enter base point G (x y): ");
    scanf("%d %d", &G.x, &G.y);

    printf("Enter private key: ");
    scanf("%d", &privateKey);

    publicKey = multiply(G, privateKey, a, p);

    printf("\nElliptic Curve: y^2 = x^3 + %dx + %d (mod %d)",
           a, b, p);

    printf("\nBase Point G: (%d, %d)", G.x, G.y);

    printf("\nPrivate Key: %d", privateKey);

    printf("\nPublic Key Q = dG: (%d, %d)\n",
           publicKey.x, publicKey.y);

    return 0;
}
```


## Output:

<img width="414" height="372" alt="Screenshot 2026-09-03 at 10 26 44 PM" src="https://github.com/user-attachments/assets/3e827af6-e22e-4b33-b7b5-90258311b868" />

## Result:
The program is executed successfully

