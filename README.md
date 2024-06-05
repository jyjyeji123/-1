### 스택 구현
```
#include<stdio.h>
#include<stdlib.h>

#define MAX 100

typedef struct {
    int top;
    int items[MAX];
} Stack;

void initStack(Stack *s) {
    s->top = -1;
}

int isEmpty(Stack *s) {
    return s->top == -1;
}

int isFull(Stack *s) {
    return s->top == MAX - 1;
}

void push(Stack *s, int item) {
    if(isFull(s)) {
        printf("Stack is full\n");
    } else {
        s->items[++s->top] = item;
    }
}

int pop(Stack *s) {
    if(isEmpty(s)) {
        printf("Stack is empty\n");
        return -1; // 에러 값을 반환
    } else {
        return s->items[s->top--];
    }
}

int peek(Stack *s) {
    if(isEmpty(s)) {
        printf("Stack is empty\n");
        return -1; // 에러 값을 반환
    } else {
        return s->items[s->top];
    }
}

```

```
#include<stdio.h>
#include<stdlib.h>

#define MAX 100
```
#include<stdlib.h>: 동적 메모리 할당 및 유틸리티 함수를 사용하기 위해 포함.
#define MAX 100: 스택의 최대 크기를 100으로 정의.

##스택 구조체의 정의
```
typedef struct {
    int top;
    int items[MAX];
} Stack;
```
typedef struct: 새로운 구조체 타입을 정의.
int top: 스택의 가장 상단 요소의 인덱스를 저장.
int items[MAX]: 스택 요소들을 저장할 배열.

##스택 초기화
```
void initStack(Stack *s) {
    s->top = -1;
}
```
void initStack(Stack *s): 스택을 초기화하는 함수.
s->top = -1: 스택이 비어있음을 나타내기 위해 top을 -1로 설정.

##스택이 비어있는지 확인
```
int isFull(Stack *s) {
    return s->top == MAX - 1;
}
```
int isEmpty(Stack *s): 스택이 비었는지 확인하는 함수.
return s->top == -1: top이 -1이면 스택이 비어있음을 의미.

##스택이 가득 찾는지 확인
```
int isFull(Stack *s) {
    return s->top == MAX - 1;
}
```
int isFull(Stack *s): 스택이 가득 찼는지 확인하는 함수.
return s->top == MAX - 1: top이 MAX - 1이면 스택이 가득 찼음을 의미

##스택에 요소를 추가
```
void push(Stack *s, int item) {
    if(isFull(s)) {
        printf("Stack is full\n");
    } else {
        s->items[++s->top] = item;
    }
}
```
void push(Stack *s, int item): 스택에 요소를 추가하는 함수.
if(isFull(s)): 스택이 가득 찼는지 확인.
s->items[++s->top] = item: top을 증가시키고 새로운 요소를 추가.

##스택에서 요소를 제거
```
int pop(Stack *s) {
    if(isEmpty(s)) {
        printf("Stack is empty\n");
        return -1; // 오류 값을 반환
    } else {
        return s->items[s->top--];
    }
}
```
int pop(Stack *s): 스택에서 요소를 제거하는 함수.
if(isEmpty(s)): 스택이 비었는지 확인.
return s->items[s->top--]: 현재 top 요소를 반환하고 top을 감소

##스택의 최상단 요소를 확인
```
int peek(Stack *s) {
    if(isEmpty(s)) {
        printf("Stack is empty\n");
        return -1; // 오류 값을 반환
    } else {
        return s->items[s->top];
    }
}
```
int peek(Stack *s): 스택의 최상단 요소를 확인하는 함수.
if(isEmpty(s)): 스택이 비었는지 확인.
return s->items[s->top]: 현재 top 요소를 반환.
