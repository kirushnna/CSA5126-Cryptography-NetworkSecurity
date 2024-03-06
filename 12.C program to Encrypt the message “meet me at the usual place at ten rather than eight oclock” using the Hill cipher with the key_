#include <stdio.h>

// Function to calculate the determinant of a 2x2 matrix
int determinant(int a, int b, int c, int d) {
    return a * d - b * c;
}

// Function to calculate the modular inverse of a number
// (required for finding the inverse of the key matrix)
int modInverse(int a, int m) {
    int m0 = m, t, q;
    int x0 = 0, x1 = 1;

    if (m == 1)
        return 0;

    // Apply extended Euclidean Algorithm
    while (a > 1) {
        q = a / m;
        t = m;

        m = a % m, a = t;
        t = x0;
        x0 = x1 - q * x0;
        x1 = t;
    }

    // Make x1 positive
    if (x1 < 0)
        x1 += m0;

    return x1;
}

// Function to calculate the inverse of a 2x2 key matrix
void inverseMatrix(int key[2][2], int inverse[2][2], int mod) {
    int det = determinant(key[0][0], key[0][1], key[1][0], key[1][1]);

    if (det == 0) {
        printf("Error: The key matrix is not invertible.\n");
        return;
    }

    int detInv = modInverse(det, mod);

    inverse[0][0] = (key[1][1] * detInv) % mod;
    inverse[0][1] = (-key[0][1] * detInv + mod) % mod;
    inverse[1][0] = (-key[1][0] * detInv + mod) % mod;
    inverse[1][1] = (key[0][0] * detInv) % mod;
}

// Function to perform Hill cipher encryption
void hillEncrypt(char plaintext[], int key[2][2], int mod) {
    int len = strlen(plaintext);
    int ciphertext[len];

    for (int i = 0; i < len; i += 2) {
        int x = plaintext[i] - 'a';
        int y = (i + 1 < len) ? plaintext[i + 1] - 'a' : 'x' - 'a';

        ciphertext[i] = (key[0][0] * x + key[0][1] * y) % mod;
        ciphertext[i + 1] = (key[1][0] * x + key[1][1] * y) % mod;
    }

    // Print the encrypted message
    printf("Encrypted message: ");
    for (int i = 0; i < len; i++)
        printf("%c", ciphertext[i] + 'a');
    printf("\n");
}

// Function to perform Hill cipher decryption
void hillDecrypt(int ciphertext[], int key[2][2], int mod) {
    int len = strlen(ciphertext);
    int inverse[2][2];
    int plaintext[len];

    // Calculate the inverse of the key matrix
    inverseMatrix(key, inverse, mod);

    for (int i = 0; i < len; i += 2) {
        int x = ciphertext[i];
        int y = (i + 1 < len) ? ciphertext[i + 1] : 0;

        plaintext[i] = (inverse[0][0] * x + inverse[0][1] * y) % mod;
        plaintext[i + 1] = (inverse[1][0] * x + inverse[1][1] * y) % mod;
    }

    // Print the decrypted message
    printf("Decrypted message: ");
    for (int i = 0; i < len; i++)
        printf("%c", plaintext[i] + 'a');
    printf("\n");
}

int main() {
    char plaintext[] = "meetmeattheusualplaceattenratherthaneightoclock";
    int key[2][2] = {{9, 4}, {5, 7}};
    int mod = 26;

    printf("Original message: %s\n", plaintext);

    // Encryption
    hillEncrypt(plaintext, key, mod);

    // Decryption
    hillDecrypt(ciphertext, key, mod);

    return 0;
}
