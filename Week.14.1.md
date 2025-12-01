## C언어 총정리
##### apple을 메모리에 저장하고 출력해보기
```c
#include <stdio.h>
#include <stdlib.h>

int main(void) {
	char a[10]="apple";
	char* a;
	a = (char *)malloc(6);
	strcpy(a, "apple");
	puts(a);
	free(a);
}
```
##### apple, banana, kiwi를 메모리에 저장하고 출력해보기
```c
#include <stdio.h>
#include <stdlib.h>

int main(void) {
	// 문자열 포인터를 활용
	char* a = "apple";
	char* b = "banana";
	char* k = "kiwi";
	printf("%s %s %s\n", a, b, k);

	// 2차원 배열을 이용
	char f[10][10] = { { "apple" }, { "banana" },{"kiwi"} };
	for (int i = 0;i < 3;i++) {
		printf("%s ", f[i]);
	  //printf("%s\n",f[i]);
	}
	//2개념을 응용
	char* f[] = { { "apple" }, { "banana" },{"kiwi"} };
	for (int i = 0;i < 3;i++) {
		printf("%s ", f[i]);
	}
}
```
