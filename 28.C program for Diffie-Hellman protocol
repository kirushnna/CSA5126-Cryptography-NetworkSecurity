#include <stdio.h>
#include <stdlib.h>
#include <math.h>

// Function to perform modular exponentiation (a^b mod m)
long long modExp(long long a, long long b, long long m) {
    long long result = 1;
    a = a % m;

    while (b > 0) {
        if (b % 2 == 1)
            result = (result * a) % m;
        b = b / 2;
        a = (a * a) % m;
    }

    return result;
}

int main() {
    // Public parameters
    long long q = 23; // Prime modulus
    long long a = 5;  // Generator
    long long privateA = 6; // Alice's secret
    long long privateB = 15; // Bob's secret

    // Alice computes (a^x mod q)
    long long publicA = modExp(a, privateA, q);

    // Bob computes (a^y mod q)
    long long publicB = modExp(a, privateB, q);

    // Alice and Bob exchange public values

    // Alice computes shared secret
    long long secretA = modExp(publicB, privateA, q);

    // Bob computes shared secret
    long long secretB = modExp(publicA, privateB, q);

    // Display shared secrets
    printf("Shared Secret (Alice): %lld\n", secretA);
    printf("Shared Secret (Bob): %lld\n", secretB);

    return 0;
}
