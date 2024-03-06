#include <stdio.h>

long long factorial(int n) {
    if (n == 0 || n == 1) {
        return 1;
    } else {
        return n * factorial(n - 1);
    }
}

int main() {
    int totalLetters = 25;  // 26 letters in the English alphabet excluding 'J'
    int occurrencesIJ = 1;  // Number of occurrences of 'I' or 'J' in the matrix

    // Calculate the total number of possible keys
    long long totalKeys = factorial(totalLetters);

    // Calculate the effective number of unique keys considering duplicates
    long long uniqueKeys = totalKeys / factorial(occurrencesIJ);

    printf("Number of possible keys: %lld\n", totalKeys);
    printf("Effective number of unique keys: %lld\n", uniqueKeys);

    return 0;
}
