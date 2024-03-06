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
word sdesEncrypt(word plaintext, word key, word iv) {
    word k1, k2;
    keyGeneration(key, &k1, &k2);

    // Initial permutation on the plaintext and XOR with the IV
    plaintext = initialPermutation(plaintext) ^ iv;

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

int main() {
    // Test data
    word plaintext = 0b0000000100100011;
    word key = 0b0111111101;
    word iv = 0b10101010;

    // Encrypt
    word ciphertext = sdesEncrypt(plaintext, key, iv);

    // Display the encrypted result
    printf("Ciphertext: %04x\n", ciphertext);

    // Decrypt (for verification)
    word decryptedText = sdesEncrypt(ciphertext, key, iv);

    // Display the decrypted result
    printf("Decrypted Text: %04x\n", decryptedText);

    return 0;
}
