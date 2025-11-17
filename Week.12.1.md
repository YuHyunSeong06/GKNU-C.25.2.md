## Linked list(연결 리스트)
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
