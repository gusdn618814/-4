# 과제 2) 피보나치 및 GCD 시간 복잡도 프로파일링 보고서

## 1. 과제 개요
본 보고서는 재귀 호출을 이용한 피보나치 수열 $F(n)$과 $F(n-1)$을 구하고, 그 결과값들의 최대공약수(GCD)를 구하는 과정의 시간 복잡도를 프로파일링을 통해 검증한다.

## 2. 소스 코드 (C 언어)
```c
#include <stdio.h>
#include <time.h>

// 재귀적 피보나치 함수 (O(2^n))
long long fibonacci(int n) {
    if (n <= 1) return n;
    return fibonacci(n - 1) + fibonacci(n - 2);
}

// 유클리드 알고리즘 GCD 함수 (O(log n))
long long gcd(long long a, long long b) {
    while (b != 0) {
        long long tmp = a % b;
        a = b;
        b = tmp;
    }
    return a;
}

int main() {
    printf("n\tF(n)\t\tTime(sec)\n");
    printf("------------------------------------\n");
    for (int n = 5; n <= 40; n += 5) {
        clock_t start = clock();
        long long fn = fibonacci(n);
        long long fn_1 = fibonacci(n - 1);
        long long res = gcd(fn, fn_1);
        clock_t end = clock();
        double duration = (double)(end - start) / CLOCKS_PER_SEC;
        printf("%d\t%lld\t\t%.6f\n", n, fn, duration);
    }
    return 0;
}
