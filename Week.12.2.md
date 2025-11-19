## 중앙 제곱법 - 난수 생성
```c
#include <stdio.h>
void main(void)
{
    int seed = 1234;  // 초기값 (0~9999)
    long x;
    for (int i = 0; i < 10; i++) {
        x = seed;
        x = x * x;          // 제곱
        x = (x / 100) % 10000; // 가운데 4자리
        seed = (int)x;
        printf("%04d\n", seed);
    }
}
```
