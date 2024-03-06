#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <openssl/des.h>

// Padding function to add consistent padding
void add_padding(unsigned char *plaintext, int block_size, int data_size) {
    int padding_length = block_size - (data_size % block_size);
    memset(plaintext + data_size, padding_length, padding_length);
}

// Remove padding from decrypted data
void remove_padding(unsigned char *data, int data_size) {
    int padding_length = data[data_size - 1];
    memset(data + data_size - padding_length, 0, padding_length);
}

// Encrypt data using DES in ECB mode
void encrypt_des_ecb(const unsigned char *plaintext, const unsigned char *key, int block_size, int data_size) {
    DES_key_schedule ks;
    DES_set_key((DES_cblock *)key, &ks);

    unsigned char *ciphertext = malloc(data_size);

    for (int i = 0; i < data_size; i += block_size) {
        DES_ecb_encrypt((DES_cblock *)(plaintext + i), (DES_cblock *)(ciphertext + i), &ks, DES_ENCRYPT);
    }

    // Print the result
    printf("ECB Ciphertext: ");
    for (int i = 0; i < data_size; i++) {
        printf("%02x", ciphertext[i]);
    }
    printf("\n");

    free(ciphertext);
}

// Encrypt data using DES in CBC mode
void encrypt_des_cbc(const unsigned char *plaintext, const unsigned char *key, const unsigned char *iv, int block_size, int data_size) {
    DES_key_schedule ks;
    DES_set_key((DES_cblock *)key, &ks);

    unsigned char *ciphertext = malloc(data_size);
    DES_cblock ivec;
    memcpy(&ivec, iv, sizeof(DES_cblock));

    for (int i = 0; i < data_size; i += block_size) {
        DES_ncbc_encrypt((DES_cblock *)(plaintext + i), (DES_cblock *)(ciphertext + i), block_size, &ks, &ivec, DES_ENCRYPT);
    }

    // Print the result
    printf("CBC Ciphertext: ");
    for (int i = 0; i < data_size; i++) {
        printf("%02x", ciphertext[i]);
    }
    printf("\n");

    free(ciphertext);
}

// Encrypt data using DES in CFB mode
void encrypt_des_cfb(const unsigned char *plaintext, const unsigned char *key, const unsigned char *iv, int block_size, int data_size) {
    DES_key_schedule ks;
    DES_set_key((DES_cblock *)key, &ks);

    unsigned char *ciphertext = malloc(data_size);
    DES_cblock ivec;
    memcpy(&ivec, iv, sizeof(DES_cblock));

    for (int i = 0; i < data_size; i += block_size) {
        DES_cfb_encrypt(plaintext + i, ciphertext + i, block_size, &ks, &ivec, &block_size, DES_ENCRYPT);
    }

    // Print the result
    printf("CFB Ciphertext: ");
    for (int i = 0; i < data_size; i++) {
        printf("%02x", ciphertext[i]);
    }
    printf("\n");

    free(ciphertext);
}

// Decrypt data using DES in ECB mode
void decrypt_des_ecb(const unsigned char *ciphertext, const unsigned char *key, int block_size, int data_size) {
    DES_key_schedule ks;
    DES_set_key((DES_cblock *)key, &ks);

    unsigned char *decrypted_text = malloc(data_size);

    for (int i = 0; i < data_size; i += block_size) {
        DES_ecb_encrypt((DES_cblock *)(ciphertext + i), (DES_cblock *)(decrypted_text + i), &ks, DES_DECRYPT);
    }

    // Remove padding
    remove_padding(decrypted_text, data_size);

    // Print the result
    printf("ECB Decrypted: %s\n", decrypted_text);

    free(decrypted_text);
}

// Decrypt data using DES in CBC mode
void decrypt_des_cbc(const unsigned char *ciphertext, const unsigned char *key, const unsigned char *iv, int block_size, int data_size) {
    DES_key_schedule ks;
    DES_set_key((DES_cblock *)key, &ks);

    unsigned char *decrypted_text = malloc(data_size);
    DES_cblock ivec;
    memcpy(&ivec, iv, sizeof(DES_cblock));

    for (int i = 0; i < data_size; i += block_size) {
        DES_ncbc_encrypt((DES_cblock *)(ciphertext + i), (DES_cblock *)(decrypted_text + i), block_size, &ks, &ivec, DES_DECRYPT);
    }

    // Remove padding
    remove_padding(decrypted_text, data_size);

    // Print the result
    printf("CBC Decrypted: %s\n", decrypted_text);

    free(decrypted_text);
}

// Decrypt data using DES in CFB mode
void decrypt_des_cfb(const unsigned char *ciphertext, const unsigned char *key, const unsigned char *iv, int block_size, int data_size) {
    DES_key_schedule ks;
    DES_set_key((DES_cblock *)key, &ks);

    unsigned char *decrypted_text = malloc(data_size);
    DES_cblock ivec;
    memcpy(&ivec, iv, sizeof(DES_cblock));

    for (int i = 0; i < data_size; i += block_size) {
        DES_cfb_encrypt(ciphertext + i, decrypted_text + i, block_size, &ks, &ivec, &block_size, DES_DECRYPT);
    }

    // Remove padding
    remove_padding(decrypted_text, data_size);

    // Print the result
    printf("CFB Decrypted: %s\n", decrypted_text);

    free(decrypted_text);
}

int main() {
    // DES key (8 bytes)
    unsigned char key[8] = "01234567";

    // Initialization Vector (IV) (8 bytes)
    unsigned char iv[8] = "abcdefgh";

    // Input plaintext (multiple of 8 bytes for simplicity)
    unsigned char plaintext[16] = "hello world12345";

    // Block size (DES block size is 8 bytes)
    int block_size = 8;

    // Data size
    int data_size = strlen((char *)plaintext);

    // Add consistent padding
    add_padding(plaintext, block_size, data_size);

    // Print the original plaintext
    printf("Original plaintext: %s\n", plaintext);

    // Encrypt in ECB mode
    encrypt_des_ecb(plaintext, key, block_size, data_size);

    // Encrypt in CBC mode
    encrypt_des_cbc(plaintext, key, iv, block_size, data_size);

    // Encrypt in CFB mode
    encrypt_des_cfb(plaintext, key, iv, block_size, data_size);

    // Decrypt in ECB mode
    decrypt_des_ecb(plaintext, key, block_size, data_size);

    // Decrypt in CBC mode
    decrypt_des_cbc(plaintext, key, iv, block_size, data_size);

    // Decrypt in CFB mode
    decrypt_des_cfb(plaintext, key, iv, block_size, data_size);

    return 0;
}
