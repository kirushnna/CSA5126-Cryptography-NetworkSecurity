#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <openssl/rsa.h>
#include <openssl/pem.h>
#include <openssl/err.h>

int main() {
    // Public key (n, e)
    char *n_hex = "009d5eaf5f882bee42db9f4c08451e32f2c70f1d08e04b3f94f270ab18c38d7b";
    char *e_hex = "010001";

    BIGNUM *n = BN_new();
    BIGNUM *e = BN_new();
    BN_hex2bn(&n, n_hex);
    BN_hex2bn(&e, e_hex);

    // Create RSA public key
    RSA *rsa = RSA_new();
    rsa->n = n;
    rsa->e = e;

    // Message to encrypt
    char *message = "Hello, RSA!";

    // Encrypt the message
    int rsa_len = RSA_size(rsa);
    unsigned char *cipher_text = (unsigned char *)malloc(rsa_len);
    int encrypt_size = RSA_public_encrypt(strlen(message) + 1, (unsigned char *)message, cipher_text, rsa, RSA_PKCS1_PADDING);

    if (encrypt_size == -1) {
        ERR_print_errors_fp(stderr);
        return 1;
    }

    // Display the encrypted message
    printf("Encrypted Message: ");
    for (int i = 0; i < encrypt_size; i++) {
        printf("%02x", cipher_text[i]);
    }
    printf("\n");

    // Clean up
    free(cipher_text);
    RSA_free(rsa);

    return 0;
}
