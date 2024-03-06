#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Function to perform frequency analysis on the ciphertext
void frequencyAnalysis(const char *ciphertext, int length) {
    int frequency[26] = {0};

    for (int i = 0; i < length; i++) {
        if (ciphertext[i] >= 'A' && ciphertext[i] <= 'Z') {
            frequency[ciphertext[i] - 'A']++;
        }
    }

    printf("Frequency Analysis:\n");
    for (int i = 0; i < 26; i++) {
        printf("%c: %d\n", 'A' + i, frequency[i]);
    }
}

// Function to decrypt the ciphertext using a simple decryption key
void decrypt(const char *ciphertext, int length) {
    printf("Decrypted Message:\n");
    for (int i = 0; i < length; i++) {
        char decryptedChar = (ciphertext[i] - 'A' + 1) % 26 + 'A';
        printf("%c", decryptedChar);
    }
    printf("\n");
}

int main() {
    // Example ciphertext (just for demonstration)
    const char *ciphertext = "QDKADWLC";
    int length = strlen(ciphertext);

    // Perform frequency analysis
    frequencyAnalysis(ciphertext, length);

    // Decrypt the ciphertext (using a simple decryption key for demonstration)
    decrypt(ciphertext, length);

    return 0;
}
