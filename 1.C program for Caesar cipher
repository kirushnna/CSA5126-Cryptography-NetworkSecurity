#include <stdio.h>
#include <ctype.h>

// Function to perform Caesar cipher encryption
void caesarCipher(char message[], int key) {
    char ch;

    for (int i = 0; message[i] != '\0'; ++i) {
        ch = message[i];

        if (isalpha(ch)) {
            // Determine whether the character is uppercase or lowercase
            char base = isupper(ch) ? 'A' : 'a';

            // Apply the Caesar cipher encryption formula
            message[i] = (char)(((ch - base + key) % 26) + base);
        }
    }
}

int main() {
    char message[100];
    int key;

    // Input the message to be encrypted
    printf("Enter a message: ");
    fgets(message, sizeof(message), stdin);

    // Iterate through possible values of k (1 to 25) and print the encrypted messages
    for (key = 1; key <= 25; ++key) {
        // Make a copy of the original message
        char encryptedMessage[100];
        strcpy(encryptedMessage, message);

        // Perform Caesar cipher encryption
        caesarCipher(encryptedMessage, key);

        // Print the encrypted message for the current key
        printf("With key %d: %s", key, encryptedMessage);
    }

    return 0;
}
