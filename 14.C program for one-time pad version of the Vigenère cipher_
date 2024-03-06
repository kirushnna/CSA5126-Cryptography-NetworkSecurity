#include <stdio.h>
#include <string.h>

// Function to encrypt a plaintext using a key stream
void encrypt(char plaintext[], int keyStream[]) {
    int len = strlen(plaintext);
    char ciphertext[len];

    for (int i = 0; i < len; ++i) {
        if (plaintext[i] >= 'a' && plaintext[i] <= 'z') {
            ciphertext[i] = 'a' + (plaintext[i] - 'a' + keyStream[i % len]) % 26;
        } else if (plaintext[i] >= 'A' && plaintext[i] <= 'Z') {
            ciphertext[i] = 'A' + (plaintext[i] - 'A' + keyStream[i % len]) % 26;
        } else {
            ciphertext[i] = plaintext[i];
        }
    }

    // Print the encrypted message
    printf("Encrypted message: %s\n", ciphertext);
}

// Function to decrypt a ciphertext using a key stream
void decrypt(char ciphertext[], int keyStream[]) {
    int len = strlen(ciphertext);
    char decrypted[len];

    for (int i = 0; i < len; ++i) {
        if (ciphertext[i] >= 'a' && ciphertext[i] <= 'z') {
            decrypted[i] = 'a' + (ciphertext[i] - 'a' - keyStream[i % len] + 26) % 26;
        } else if (ciphertext[i] >= 'A' && ciphertext[i] <= 'Z') {
            decrypted[i] = 'A' + (ciphertext[i] - 'A' - keyStream[i % len] + 26) % 26;
        } else {
            decrypted[i] = ciphertext[i];
        }
    }

    // Print the decrypted message
    printf("Decrypted message: %s\n", decrypted);
}

int main() {
    char plaintext[] = "SENDMOREMONEY";
    int keyStream[] = {9, 0, 1, 7, 23, 15, 21, 14, 11, 11, 2, 8, 9};

    // Part (a): Encrypt the plaintext
    encrypt(plaintext, keyStream);

    // Part (b): Decrypt to find the key
    char ciphertext[] = "MJYPVFAIIDWU";
    int potentialKeyStream[sizeof(keyStream) / sizeof(keyStream[0])];

    for (int i = 0; i < sizeof(keyStream) / sizeof(keyStream[0]); ++i) {
        // Find the key by subtracting the ciphertext from the plaintext
        potentialKeyStream[i] = (ciphertext[i] - plaintext[i] + 26) % 26;
    }

    // Print the potential key stream
    printf("Potential Key Stream: ");
    for (int i = 0; i < sizeof(keyStream) / sizeof(keyStream[0]); ++i) {
        printf("%d ", potentialKeyStream[i]);
    }
    printf("\n");

    // Decrypt using the potential key stream
    decrypt(ciphertext, potentialKeyStream);

    return 0;
}
