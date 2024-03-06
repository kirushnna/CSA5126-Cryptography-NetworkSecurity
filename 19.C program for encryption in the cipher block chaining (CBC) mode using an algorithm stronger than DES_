#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <openssl/des.h>

// Encrypt plaintext using 3DES in CBC mode
void encrypt_3des_cbc(const unsigned char *plaintext, const unsigned char *key, const unsigned char *iv, unsigned char *ciphertext) {
    DES_key_schedule ks1, ks2, ks3;
    DES_set_key((DES_cblock *)key, &ks1);
    DES_set_key((DES_cblock *)(key + 8), &ks2);
    DES_set_key((DES_cblock *)(key + 16), &ks3);

    DES_cblock ivec;
    memcpy(&ivec, iv, sizeof(DES_cblock));

    DES_ede3_cbc_encrypt(plaintext, ciphertext, 8, &ks1, &ks2, &ks3, &ivec, DES_ENCRYPT);
}

int main() {
    // 3DES key (24 bytes)
    unsigned char key[24] = "0123456789abcdef01234567";

    // Initialization Vector (IV) (8 bytes)
    unsigned char iv[8] = "abcdefgh";

    // Input plaintext (8 bytes)
    unsigned char plaintext[8] = "message";

    // Output ciphertext (8 bytes)
    unsigned char ciphertext[8];

    // Perform 3DES encryption in CBC mode
    encrypt_3des_cbc(plaintext, key, iv, ciphertext);

    // Print the result
    printf("Plaintext:  %s\n", plaintext);
    printf("Ciphertext: ");
    for (int i = 0; i < 8; i++) {
        printf("%02x", ciphertext[i]);
    }
    printf("\n");

    return 0;
}
