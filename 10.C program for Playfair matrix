#include <stdio.h>
#include <string.h>
#include <ctype.h>

// Function to prepare the Playfair matrix
void preparePlayfairMatrix(char keyTable[5][5], const char *key) {
    int k, i, j;
    int keyLength = strlen(key);
    int index = 0;
    char keySet[26] = {0};

    // Fill the key set with the letters from the key
    for (k = 0; k < keyLength; ++k) {
        if (key[k] != 'J') {
            if (keySet[key[k] - 'A'] == 0) {
                keySet[key[k] - 'A'] = 1;
                keyTable[index / 5][index % 5] = key[k];
                ++index;
            }
        }
    }

    // Fill the key set with the remaining letters of the alphabet
    for (k = 0; k < 26; ++k) {
        if (keySet[k] == 0 && k != ('J' - 'A')) {
            keyTable[index / 5][index % 5] = 'A' + k;
            ++index;
        }
    }
}

// Function to find the positions of two characters in the Playfair matrix
void findPositions(char keyTable[5][5], char a, char b, int *rowA, int *colA, int *rowB, int *colB) {
    int i, j;

    for (i = 0; i < 5; ++i) {
        for (j = 0; j < 5; ++j) {
            if (keyTable[i][j] == a) {
                *rowA = i;
                *colA = j;
            }
            if (keyTable[i][j] == b) {
                *rowB = i;
                *colB = j;
            }
        }
    }
}

// Function to encrypt a Playfair message
void playfairEncrypt(char keyTable[5][5], char message[]) {
    int i, rowA, colA, rowB, colB;
    int len = strlen(message);

    for (i = 0; i < len; i += 2) {
        // Find positions of the two characters in the key table
        findPositions(keyTable, message[i], message[i + 1], &rowA, &colA, &rowB, &colB);

        // Encrypt the pair
        if (rowA == rowB) {
            // Same row, shift right
            printf("%c%c", keyTable[rowA][(colA + 1) % 5], keyTable[rowB][(colB + 1) % 5]);
        } else if (colA == colB) {
            // Same column, shift down
            printf("%c%c", keyTable[(rowA + 1) % 5][colA], keyTable[(rowB + 1) % 5][colB]);
        } else {
            // Rectangle, swap columns
            printf("%c%c", keyTable[rowA][colB], keyTable[rowB][colA]);
        }
    }
}

int main() {
    char key[] = "MFHIJKUNOPQZVWXYELDRGTSBC";
    char keyTable[5][5];
    char message[] = "MUSTSEEYOUOVERCADOGANWESTCOMINGATONCE";

    // Prepare the Playfair matrix
    preparePlayfairMatrix(keyTable, key);

    // Encrypt the Playfair message
    playfairEncrypt(keyTable, message);

    return 0;
}
