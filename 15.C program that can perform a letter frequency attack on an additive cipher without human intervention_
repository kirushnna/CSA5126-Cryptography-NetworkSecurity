#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Function to calculate the frequency distribution of letters in a string
void calculateFrequency(const char *text, int frequency[26]) {
    for (int i = 0; text[i] != '\0'; ++i) {
        if (isalpha(text[i])) {
            char c = tolower(text[i]);
            frequency[c - 'a']++;
        }
    }
}

// Function to decrypt text using a given shift value
void decryptWithShift(const char *ciphertext, int shift, char *plaintext) {
    for (int i = 0; ciphertext[i] != '\0'; ++i) {
        if (isalpha(ciphertext[i])) {
            char c = tolower(ciphertext[i]);
            char decrypted = 'a' + ((c - 'a' - shift + 26) % 26);
            plaintext[i] = isupper(ciphertext[i]) ? toupper(decrypted) : decrypted;
        } else {
            plaintext[i] = ciphertext[i];
        }
    }
}

// Function to perform a letter frequency attack
void letterFrequencyAttack(const char *ciphertext, int topN) {
    int frequency[26] = {0};
    calculateFrequency(ciphertext, frequency);

    // Determine the most frequent letter
    int maxFrequency = 0;
    int maxIndex = 0;
    for (int i = 0; i < 26; ++i) {
        if (frequency[i] > maxFrequency) {
            maxFrequency = frequency[i];
            maxIndex = i;
        }
    }

    // Calculate the shift value for the most frequent letter
    int shift = (maxIndex - ('e' - 'a') + 26) % 26;

    // Decrypt and print the top N possible plaintexts
    printf("Top %d possible plaintexts:\n", topN);
    for (int i = 0; i < topN; ++i) {
        char plaintext[1000];
        decryptWithShift(ciphertext, shift + i, plaintext);
        printf("%d. %s\n", i + 1, plaintext);
    }
}

int main() {
    // Example ciphertext
    const char *ciphertext = "Uifsf jt b tfdsfu nfttbhf.";

    // User interface
    int topN;
    printf("Enter the number of top possible plaintexts to display: ");
    scanf("%d", &topN);

    // Perform letter frequency attack
    letterFrequencyAttack(ciphertext, topN);

    return 0;
}
