#include <stdio.h>

typedef unsigned char byte;
typedef unsigned short int word;

// Initial permutation for the 8-bit data
word initialPermutation(word data) {
    return ((data & 0x80) >> 7) | ((data & 0x40) >> 5) | ((data & 0x20) >> 3) | ((data & 0x10) >> 1) |
           ((data & 0x08) << 1) | ((data & 0x04) << 3) | ((data & 0x02) << 5) | ((data & 0x01) << 7);
}

// Permutation P4 for the 4-bit data
byte permutationP4(byte data) {
    return ((data & 0x08) >> 2) | (data & 0x04) | ((data & 0x02) << 2) | ((data & 0x01) << 3);
}

// Key generation
void keyGeneration(word key, word *k1, word *k2) {
    key = initialPermutation(key);
    *k1 = permutationP4((key & 0x0F) << 1 | ((key & 0xF0) >> 4));
    *k2 = permutationP4((key & 0x0F) << 3 | ((key & 0xF0) >> 2));
}

// XOR operation on two 4-bit data
byte xor4(byte a, byte b) {
    return a ^ b;
}

// S-DES round function
byte roundFunction(byte data, byte key) {
    return permutationP4(xor4(data, key));
}

// S-DES encryption
word sdesEncrypt(word plaintext, word key) {
    word k1, k2;
    keyGeneration(key, &k1, &k2);

    // Initial permutation on the plaintext
    plaintext = initialPermutation(plaintext);

    // First round
    word left = (plaintext & 0xF0) >> 4;
    word right = plaintext & 0x0F;
    word temp = right;
    right = left ^ roundFunction(right, k1);
    left = temp;

    // Second round
    temp = right;
    right = left ^ roundFunction(right, k2);
    left = temp;

    // Final permutation
    return (right << 4) | left;
}

// S-DES encryption in Counter (CTR) mode
word sdesEncryptCTR(word plaintext, word key, word counter) {
    // Encrypt the counter
    word encryptedCounter = sdesEncrypt(counter, key);

    // XOR plaintext with encrypted counter
    return plaintext ^ encryptedCounter;
}

int main() {
    // Test data
    word plaintext = 0b000000010000001000000100;
    word key = 0b0111111101;
    word counter = 0b00000000;

    // Encrypt
    word ciphertext = sdesEncryptCTR(plaintext, key, counter);

    // Display the encrypted result
    printf("Ciphertext: %06x\n", ciphertext);

    // Decrypt (for verification)
    word decryptedText = sdesEncryptCTR(ciphertext, key, counter);

    // Display the decrypted result
    printf("Decrypted Text: %06x\n", decryptedText);

    return 0;
}
