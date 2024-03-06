#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <openssl/des.h>

// Encrypt plaintext using DES in ECB mode
void encrypt_des_ecb(const unsigned char *plaintext, const unsigned char *key, unsigned char *ciphertext) {
    DES_key_schedule ks;
    DES_set_key((DES_cblock *)key, &ks);

    DES_ecb_encrypt((DES_cblock *)plaintext, (DES_cblock *)ciphertext, &ks, DES_ENCRYPT);
}

// Decrypt ciphertext using DES in ECB mode
void decrypt_des_ecb(const unsigned char *ciphertext, const unsigned char *key, unsigned char *plaintext) {
    DES_key_schedule ks;
    DES_set_key((DES_cblock *)key, &ks);

    DES_ecb_encrypt((DES_cblock *)ciphertext, (DES_cblock *)plaintext, &ks, DES_DECRYPT);
}

int main() {
    // DES key (8 bytes)
    unsigned char key[8] = "01234567";

    // Input plaintext (multiple of 8 bytes for simplicity)
    unsigned char plaintext[16] = "abcdefgh12345678";

    // Output ciphertext
    unsigned char ciphertext[16];

    // Encrypt in ECB mode
    encrypt_des_ecb(plaintext, key, ciphertext);

    // Print the result
    printf("Plaintext:  %s\n", plaintext);
    printf("Ciphertext: ");
    for (int i = 0; i < 16; i++) {
        printf("%02x", ciphertext[i]);
    }
    printf("\n");

    // Decrypt in ECB mode
    unsigned char decrypted_text[16];
    decrypt_des_ecb(ciphertext, key, decrypted_text);

    // Print the decrypted text
    printf("Decrypted:  %s\n", decrypted_text);

    return 0;
}
