#include <stdio.h>
#include <string.h>
#include <ctype.h>

// Function to perform monoalphabetic substitution cipher encryption
void substitutionCipher(char message[], char key[]) {
    for (int i = 0; message[i] != '\0'; ++i) {
        char ch = message[i];

        if (isalpha(ch)) {
            // Determine whether the character is uppercase or lowercase
            char base = isupper(ch) ? 'A' : 'a';

            // Apply substitution cipher using the key
            message[i] = isupper(ch) ? key[ch - base] : tolower(key[ch - base]);
        }
    }
}

int main() {
    char message[100];
    char key[26];

    // Input the message to be encrypted
    printf("Enter a message: ");
    fgets(message, sizeof(message), stdin);

    // Input the substitution key
    printf("Enter the substitution key (26 unique letters): ");
    fgets(key, sizeof(key), stdin);

    // Check if the key is valid (contains 26 unique letters)
    if (strlen(key) != 27 || key[26] != '\n') {
        printf("Invalid key. Please enter 26 unique letters for substitution.\n");
        return 1; // Exit with an error code
    }

    // Perform monoalphabetic substitution cipher encryption
    substitutionCipher(message, key);

    // Print the encrypted message
    printf("Encrypted message: %s", message);

    return 0;
}
