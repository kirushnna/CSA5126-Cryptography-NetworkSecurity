#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <ctype.h>

// Function to calculate the frequency distribution of letters in a string
void calculateFrequency(const char *text, int frequency[26]) {
    for (int i = 0; text[i] != '\0'; ++i) {
        if (isalpha(text[i])) {
            char c = tolower(text[i]);
            frequency[c - 'a']++;
        }
    }
}

// Function to decrypt text using a given substitution
void decryptWithSubstitution(const char *ciphertext, const char *substitution, char *plaintext) {
    for (int i = 0; ciphertext[i] != '\0'; ++i) {
        if (isalpha(ciphertext[i])) {
            char c = tolower(ciphertext[i]);
            plaintext[i] = isupper(ciphertext[i]) ? toupper(substitution[c - 'a']) : substitution[c - 'a'];
        } else {
            plaintext[i] = ciphertext[i];
        }
    }
}

// Function to perform a letter frequency attack
void letterFrequencyAttack(const char *ciphertext, int topN) {
    int frequency[26] = {0};
    calculateFrequency(ciphertext, frequency);

    // Create a mapping of ciphertext letters to their frequencies
    char frequencyMapping[26];
    for (int i = 0; i < 26; ++i) {
        frequencyMapping[i] = 'a' + i;
    }

    // Sort the mapping based on letter frequencies
    for (int i = 0; i < 25; ++i) {
        for (int j = 0; j < 25 - i; ++j) {
            if (frequency[j] < frequency[j + 1]) {
                // Swap frequency
                int tempFreq = frequency[j];
                frequency[j] = frequency[j + 1];
                frequency[j + 1] = tempFreq;

                // Swap mapping
                char tempMap = frequencyMapping[j];
                frequencyMapping[j] = frequencyMapping[j + 1];
                frequencyMapping[j + 1] = tempMap;
            }
        }
    }

    // Decrypt and print the top N possible plaintexts
    printf("Top %d possible plaintexts:\n", topN);
    for (int i = 0; i < topN; ++i) {
        char plaintext[1000];
        decryptWithSubstitution(ciphertext, frequencyMapping, plaintext);
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
