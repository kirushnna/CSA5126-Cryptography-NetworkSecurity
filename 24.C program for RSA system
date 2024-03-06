#include <stdio.h>

// Function to calculate the greatest common divisor (GCD) using Euclidean algorithm
int gcd(int a, int b) {
    if (b == 0)
        return a;
    else
        return gcd(b, a % b);
}

// Function to calculate the multiplicative inverse using the extended Euclidean algorithm
int modInverse(int a, int m) {
    int m0 = m;
    int y = 0, x = 1;

    if (m == 1)
        return 0;

    while (a > 1) {
        // q is quotient
        int q = a / m;

        int t = m;

        // m is remainder now, process same as Euclid's algo
        m = a % m, a = t;
        t = y;

        // Update x and y
        y = x - q * y;
        x = t;
    }

    // Make x positive
    if (x < 0)
        x += m0;

    return x;
}

int main() {
    // Given public key
    int e = 31;
    int n = 3599;

    // Trial-and-error to determine p and q
    int p, q;
    for (p = 2; p < n; p++) {
        if (n % p == 0) {
            q = n / p;
            break;
        }
    }

    // Calculate totient (f(n))
    int phi = (p - 1) * (q - 1);

    // Calculate the private key using the extended Euclidean algorithm
    int d = modInverse(e, phi);

    // Display the private key
    printf("Private Key (d): %d\n", d);

    return 0;
}
