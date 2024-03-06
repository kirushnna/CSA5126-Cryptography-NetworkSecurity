#include <stdio.h>
#include <string.h>
#include <ctype.h>

// Function to generate the cipher sequence from the keyword
void generateCipherSequence(char keyword[], char cipherSequence[]) {
    int keywordLength = strlen(keyword);
    int index = 0;

    // Copy the keyword to the cipher sequence
    strcpy(cipherSequence, keyword);

    // Append the unused letters in normal order
    for (char ch = 'A'; ch <= 'Z'; ++ch) {
        if (strchr(keyword, toupper(ch)) == NULL) {
            cipherSequence[keywordLength + index] = ch;
            ++index;
        }
    }

    // Null-terminate the cipher sequence
    cipherSequence[keywordLength + index] = '\0';
}

// Function to perform monoalphabetic substitution cipher encryption
void monoalphabeticCipher(char message[], char cipherSequence[]) {
    for (int i = 0; message[i] != '\0'; ++i) {
        if (isalpha(message[i])) {
            char base = isupper(message[i]) ? 'A' : 'a';

            // Use the cipher sequence for substitution
            message[i] = cipherSequence[message[i] - base];
        }
    }
}

int main() {
    char keyword[] = "CIPHER";
    char cipherSequence[26];
    char message[100];

    // Generate the cipher sequence from the keyword
    generateCipherSequence(keyword, cipherSequence);

    // Input the message to be encrypted
    printf("Enter a message: ");
    fgets(message, sizeof(message), stdin);

    // Perform monoalphabetic substitution cipher encryption
    monoalphabeticCipher(message, cipherSequence);

    // Print the encrypted message
    printf("Encrypted message: %s", message);

    return 0;
}
