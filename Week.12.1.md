## Linked list(연결 리스트)
##### **배열처럼 한 번에 크게 잡기 애매하고 중간 삽입/삭제가 자주 일어나는 데이터들을 다룰 때 사용하는 자료구조**
```c
#include <stdio.h>

typedef struct Node {
	int data;
	struct Node* next;
}Node;

int main(void) {
	Node n1, n2, n3;

	n1.data = 3; n2.data = 2; n3.data = 1;
	n1.next = &n2; n2.next = &n3; n3.next = NULL;

	Node* head = &n1; // head는 3을 가리키도록
	Node* p = head;

	while (p != NULL) {
		printf("%d -> ", p->data);
		p = p->next;
	}
	printf("NULL\n");
	return 0;
}
```
##### 타입 캐스팅 : 형 변환
##### **malloc을 활용한 연결 리스트**
```c
#include <stdio.h>
#include <stdlib.h>   // malloc, free

typedef struct Node {
    int data;
    struct Node *next;
} Node;

int main(void) {
    // 동적 생성: 3개 노드 할당
    Node *n1 = (Node *)malloc(sizeof(Node));
    Node *n2 = (Node *)malloc(sizeof(Node));
    Node *n3 = (Node *)malloc(sizeof(Node));

    // 값 넣기
    n1->data = 3;   n2->data = 2;   n3->data = 1;

    // 링크 연결: 3 -> 2 -> 1 -> NULL
    n1->next = n2;
    n2->next = n3;
    n3->next = NULL;

    // head는 3을 가리키도록
    Node *head = n1;

    // 리스트 출력
    Node *p = head;
    while (p != NULL) {
        printf("%d -> ", p->data);
        p = p->next;
    }
    printf("NULL\n");

    // 동적 메모리 해제
    free(n1);
    free(n2);
    free(n3);

    return 0;
}
```
