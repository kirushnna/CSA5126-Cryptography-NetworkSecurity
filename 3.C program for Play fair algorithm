#include <stdio.h>
#include <string.h>
#include <ctype.h>

// Function to generate the key matrix from the key string
void generateKeyMatrix(char key[], char keyMatrix[5][5]) {
    int i, j, k;
    int keyLength = strlen(key);
    char keySet[26] = {0};
    
    // Initialize key set with alphabets excluding 'J'
    for (i = 0, k = 0; i < keyLength; ++i) {
        if (key[i] != 'J') {
            keySet[k++] = toupper(key[i]);
        }
    }
    
    // Fill the key matrix
    for (i = 0, k = 0; i < 5; ++i) {
        for (j = 0; j < 5; ++j) {
            if (k < keyLength - 1) {
                keyMatrix[i][j] = keySet[k++];
            } else {
                char ch;
                do {
                    ch = 'A' + (rand() % 26);
                } while (strchr(keySet, ch) != NULL);
                
                keyMatrix[i][j] = ch;
            }
        }
    }
}

// Function to get the position of a character in the key matrix
void getMatrixPosition(char keyMatrix[5][5], char ch, int *row, int *col) {
    if (ch == 'J') {
        ch = 'I'; // Treat 'J' as 'I'
    }

    for (*row = 0; *row < 5; ++(*row)) {
        for (*col = 0; *col < 5; ++(*col)) {
            if (keyMatrix[*row][*col] == ch) {
                return;
            }
        }
    }
}

// Function to apply Playfair cipher encryption
void playfairEncrypt(char message[], char keyMatrix[5][5]) {
    int i, row1, col1, row2, col2;
    char encryptedMessage[100];
    
    // Remove spaces and convert to uppercase
    for (i = 0; message[i] != '\0'; ++i) {
        if (message[i] != ' ') {
            message[i] = toupper(message[i]);
        }
    }

    // Pair consecutive letters
    for (i = 0; message[i + 1] != '\0'; i += 2) {
        char ch1 = message[i];
        char ch2 = message[i + 1];

        getMatrixPosition(keyMatrix, ch1, &row1, &col1);
        getMatrixPosition(keyMatrix, ch2, &row2, &col2);

        // Encrypt the pair
        if (row1 == row2) {
            encryptedMessage[i] = keyMatrix[row1][(col1 + 1) % 5];
            encryptedMessage[i + 1] = keyMatrix[row2][(col2 + 1) % 5];
        } else if (col1 == col2) {
            encryptedMessage[i] = keyMatrix[(row1 + 1) % 5][col1];
            encryptedMessage[i + 1] = keyMatrix[(row2 + 1) % 5][col2];
        } else {
            encryptedMessage[i] = keyMatrix[row1][col2];
            encryptedMessage[i + 1] = keyMatrix[row2][col1];
        }
    }

    encryptedMessage[i] = '\0';
    
    // Print the encrypted message
    printf("Encrypted message: %s\n", encryptedMessage);
}

int main() {
    char key[26];
    char keyMatrix[5][5];
    char message[100];

    // Input the key
    printf("Enter the key (no 'J' and unique letters): ");
    fgets(key, sizeof(key), stdin);

    // Input the message
    printf("Enter the message to encrypt: ");
    fgets(message, sizeof(message), stdin);

    // Generate the key matrix
    generateKeyMatrix(key, keyMatrix);

    // Perform Playfair cipher encryption
    playfairEncrypt(message, keyMatrix);

    return 0;
}
