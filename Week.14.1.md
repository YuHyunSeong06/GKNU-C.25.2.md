## C언어 총정리
##### apple을 메모리에 저장하고 출력해보기
```c
#include <stdio.h>
#include <stdlib.h>

int main(void) {
	char* a;
	a = (char *)malloc(6);
	strcpy(a, "apple");
	puts(a);
	free(a);
}
```

