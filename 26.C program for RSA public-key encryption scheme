#include <stdio.h>
#include <openssl/rsa.h>
#include <openssl/pem.h>
#include <openssl/rand.h>

void generateNewKeyPair(RSA **rsa, int bits) {
    *rsa = RSA_generate_key(bits, RSA_F4, NULL, NULL);
}

int main() {
    // Original key pair
    RSA *original_rsa = RSA_new();
    generateNewKeyPair(&original_rsa, 2048);

    // Display original modulus
    printf("Original Modulus (n): %s\n", BN_bn2hex(original_rsa->n));

    // Assume Bob's private key is leaked
    // Generate a new modulus and key pair
    RSA *new_rsa = RSA_new();
    generateNewKeyPair(&new_rsa, 2048);

    // Display new modulus
    printf("New Modulus (n): %s\n", BN_bn2h
