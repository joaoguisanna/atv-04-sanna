ATIVIDADE 04 - Lista de Algoritmos Parte 3

QUESTÃO 31:
#include <stdio.h>

// Função para realizar a ordenação Bubble Sort
void bubbleSort(int arr[], int n) {
    int i, j, temp;
    // Percorre todos os elementos do array
    for (i = 0; i < n-1; i++) {
        // Últimos i elementos já estão no lugar
        for (j = 0; j < n-i-1; j++) {
            // Troca se o elemento encontrado for maior que o próximo elemento
            if (arr[j] > arr[j+1]) {
                temp = arr[j];
                arr[j] = arr[j+1];
                arr[j+1] = temp;
            }
        }
    }
}

// Função para imprimir o array
void printArray(int arr[], int size) {
    int i;
    for (i = 0; i < size; i++)
        printf("%d ", arr[i]);
    printf("\n");
}

int main() {
    int arr[] = {64, 34, 25, 12, 22, 11, 90};
    int n = sizeof(arr)/sizeof(arr[0]);

    printf("Array original:\n");
    printArray(arr, n);

    bubbleSort(arr, n);

    printf("Array ordenado:\n");
    printArray(arr, n);

    return 0;
}

QUESTÃO 32:
#include <stdio.h>

// Função para realizar a ordenação Selection Sort
void selectionSort(int arr[], int n) {
    int i, j, min_idx, temp;
    // Passa por todos os elementos do array
    for (i = 0; i < n-1; i++) {
        // Encontra o menor elemento na parte não ordenada do array
        min_idx = i;
        for (j = i+1; j < n; j++) {
            if (arr[j] < arr[min_idx]) {
                min_idx = j;
            }
        }
        // Troca o elemento encontrado com o primeiro elemento não ordenado
        if (min_idx != i) {
            temp = arr[i];
            arr[i] = arr[min_idx];
            arr[min_idx] = temp;
        }
    }
}

// Função para imprimir o array
void printArray(int arr[], int size) {
    int i;
    for (i = 0; i < size; i++)
        printf("%d ", arr[i]);
    printf("\n");
}

int main() {
    int arr[] = {64, 34, 25, 12, 22, 11, 90};
    int n = sizeof(arr)/sizeof(arr[0]);

    printf("Array original:\n");
    printArray(arr, n);

    selectionSort(arr, n);

    printf("Array ordenado:\n");
    printArray(arr, n);

    return 0;
}

QUESTÃO 33:
#include <stdio.h>

// Função para realizar a ordenação Insertion Sort
void insertionSort(int arr[], int n) {
    int i, key, j;
    // Percorre do segundo elemento até o último
    for (i = 1; i < n; i++) {
        key = arr[i];
        j = i - 1;
        
        // Move os elementos do array que são maiores que a chave para uma posição à frente
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j = j - 1;
        }
        arr[j + 1] = key;
    }
}

// Função para imprimir o array
void printArray(int arr[], int size) {
    int i;
    for (i = 0; i < size; i++)
        printf("%d ", arr[i]);
    printf("\n");
}

int main() {
    int arr[] = {64, 34, 25, 12, 22, 11, 90};
    int n = sizeof(arr)/sizeof(arr[0]);

    printf("Array original:\n");
    printArray(arr, n);

    insertionSort(arr, n);

    printf("Array ordenado:\n");
    printArray(arr, n);

    return 0;
}

QUESTÃO 34:
#include <stdio.h>
#include <stdlib.h>

// Função para mesclar duas sublistas ordenadas em uma única lista ordenada
void merge(int arr[], int l, int m, int r) {
    int i, j, k;
    int n1 = m - l + 1;
    int n2 = r - m;

    // Criar arrays temporários
    int *L = (int*)malloc(n1 * sizeof(int));
    int *R = (int*)malloc(n2 * sizeof(int));

    // Copiar dados para arrays temporários L[] e R[]
    for (i = 0; i < n1; i++)
        L[i] = arr[l + i];
    for (j = 0; j < n2; j++)
        R[j] = arr[m + 1 + j];

    // Mesclar os arrays temporários de volta para arr[l..r]
    i = 0; // Índice inicial do primeiro subarray
    j = 0; // Índice inicial do segundo subarray
    k = l; // Índice inicial do subarray mesclado
    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) {
            arr[k] = L[i];
            i++;
        } else {
            arr[k] = R[j];
            j++;
        }
        k++;
    }

    // Copiar os elementos restantes de L[], se houver
    while (i < n1) {
        arr[k] = L[i];
        i++;
        k++;
    }

    // Copiar os elementos restantes de R[], se houver
    while (j < n2) {
        arr[k] = R[j];
        j++;
        k++;
    }

    // Liberar a memória dos arrays temporários
    free(L);
    free(R);
}

// Função para ordenar o array usando Merge Sort
void mergeSort(int arr[], int l, int r) {
    if (l < r) {
        // Encontrar o ponto médio
        int m = l + (r - l) / 2;

        // Ordenar as duas metades
        mergeSort(arr, l, m);
        mergeSort(arr, m + 1, r);

        // Mesclar as duas metades ordenadas
        merge(arr, l, m, r);
    }
}

// Função para imprimir o array
void printArray(int arr[], int size) {
    int i;
    for (i = 0; i < size; i++)
        printf("%d ", arr[i]);
    printf("\n");
}

int main() {
    int arr[] = {64, 34, 25, 12, 22, 11, 90};
    int n = sizeof(arr)/sizeof(arr[0]);

    printf("Array original:\n");
    printArray(arr, n);

    mergeSort(arr, 0, n - 1);

    printf("Array ordenado:\n");
    printArray(arr, n);

    return 0;
}

QUESTÃO 35:
#include <stdio.h>

// Função para trocar dois elementos no array
void swap(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

// Função para particionar o array e retornar o índice do pivô
int partition(int arr[], int low, int high) {
    int pivot = arr[high]; // Pivô é o último elemento
    int i = (low - 1);     // Índice do menor elemento

    for (int j = low; j < high; j++) {
        // Se o elemento atual é menor ou igual ao pivô
        if (arr[j] <= pivot) {
            i++; // Incrementa o índice do menor elemento
            swap(&arr[i], &arr[j]);
        }
    }
    swap(&arr[i + 1], &arr[high]);
    return (i + 1);
}

// Função principal do Quick Sort
void quickSort(int arr[], int low, int high) {
    if (low < high) {
        // Encontra o índice do pivô tal que os elementos menores que o pivô estão à esquerda e os maiores à direita
        int pi = partition(arr, low, high);

        // Ordena as sublistas antes e depois do pivô
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

// Função para imprimir o array
void printArray(int arr[], int size) {
    for (int i = 0; i < size; i++)
        printf("%d ", arr[i]);
    printf("\n");
}

int main() {
    int arr[] = {64, 34, 25, 12, 22, 11, 90};
    int n = sizeof(arr) / sizeof(arr[0]);

    printf("Array original:\n");
    printArray(arr, n);

    quickSort(arr, 0, n - 1);

    printf("Array ordenado:\n");
    printArray(arr, n);

    return 0;
}

QUESTÃO 36:
#include <stdio.h>
#include <stdlib.h>

#define MAX 100 // Tamanho máximo da pilha

// Estrutura para a pilha
typedef struct {
    int top;
    int items[MAX];
} Stack;

// Função para inicializar a pilha
void initStack(Stack *s) {
    s->top = -1;
}

// Função para verificar se a pilha está cheia
int isFull(Stack *s) {
    return s->top == MAX - 1;
}

// Função para verificar se a pilha está vazia
int isEmpty(Stack *s) {
    return s->top == -1;
}

// Função para adicionar um item à pilha
void push(Stack *s, int item) {
    if (isFull(s)) {
        printf("Pilha cheia! Não é possível adicionar o item %d.\n", item);
        return;
    }
    s->items[++(s->top)] = item;
    printf("Item %d adicionado à pilha.\n", item);
}

// Função para remover um item da pilha
int pop(Stack *s) {
    if (isEmpty(s)) {
        printf("Pilha vazia! Não é possível remover um item.\n");
        return -1; // Valor de erro
    }
    return s->items[(s->top)--];
}

// Função para ver o item no topo da pilha sem removê-lo
int peek(Stack *s) {
    if (isEmpty(s)) {
        printf("Pilha vazia! Não há itens para mostrar.\n");
        return -1; // Valor de erro
    }
    return s->items[s->top];
}

// Função para exibir todos os itens da pilha
void display(Stack *s) {
    if (isEmpty(s)) {
        printf("Pilha vazia!\n");
        return;
    }
    printf("Itens na pilha:\n");
    for (int i = s->top; i >= 0; i--) {
        printf("%d\n", s->items[i]);
    }
}

int main() {
    Stack s;
    initStack(&s);

    // Testando a pilha
    push(&s, 10);
    push(&s, 20);
    push(&s, 30);
    push(&s, 40);
    push(&s, 50);

    printf("Topo da pilha: %d\n", peek(&s));

    display(&s);

    printf("Item removido: %d\n", pop(&s));
    printf("Item removido: %d\n", pop(&s));

    display(&s);

    return 0;
}

QUESTÇAO 37:
#include <stdio.h>
#include <stdlib.h>

#define MAX 100 // Tamanho máximo da fila

// Estrutura para a fila
typedef struct {
    int front, rear, size;
    int items[MAX];
} Queue;

// Função para inicializar a fila
void initQueue(Queue *q) {
    q->front = 0;
    q->rear = -1;
    q->size = 0;
}

// Função para verificar se a fila está cheia
int isFull(Queue *q) {
    return q->size == MAX;
}

// Função para verificar se a fila está vazia
int isEmpty(Queue *q) {
    return q->size == 0;
}

// Função para adicionar um item à fila
void enqueue(Queue *q, int item) {
    if (isFull(q)) {
        printf("Fila cheia! Não é possível adicionar o item %d.\n", item);
        return;
    }
    q->rear = (q->rear + 1) % MAX;
    q->items[q->rear] = item;
    q->size++;
    printf("Item %d adicionado à fila.\n", item);
}

// Função para remover um item da fila
int dequeue(Queue *q) {
    if (isEmpty(q)) {
        printf("Fila vazia! Não é possível remover um item.\n");
        return -1; // Valor de erro
    }
    int item = q->items[q->front];
    q->front = (q->front + 1) % MAX;
    q->size--;
    return item;
}

// Função para ver o item na frente da fila sem removê-lo
int peek(Queue *q) {
    if (isEmpty(q)) {
        printf("Fila vazia! Não há itens para mostrar.\n");
        return -1; // Valor de erro
    }
    return q->items[q->front];
}

// Função para exibir todos os itens da fila
void display(Queue *q) {
    if (isEmpty(q)) {
        printf("Fila vazia!\n");
        return;
    }
    printf("Itens na fila:\n");
    for (int i = 0; i < q->size; i++) {
        printf("%d\n", q->items[(q->front + i) % MAX]);
    }
}

int main() {
    Queue q;
    initQueue(&q);

    // Testando a fila
    enqueue(&q, 10);
    enqueue(&q, 20);
    enqueue(&q, 30);
    enqueue(&q, 40);
    enqueue(&q, 50);

    printf("Item na frente da fila: %d\n", peek(&q));

    display(&q);

    printf("Item removido: %d\n", dequeue(&q));
    printf("Item removido: %d\n", dequeue(&q));

    display(&q);

    return 0;
}

QUESTÃO 38:
#include <stdio.h>
#include <stdlib.h>
#include <ctype.h>
#include <string.h>

#define MAX 100

// Estrutura para a pilha
typedef struct {
    int top;
    char items[MAX];
} Stack;

// Função para inicializar a pilha
void initStack(Stack *s) {
    s->top = -1;
}

// Função para verificar se a pilha está cheia
int isFull(Stack *s) {
    return s->top == MAX - 1;
}

// Função para verificar se a pilha está vazia
int isEmpty(Stack *s) {
    return s->top == -1;
}

// Função para adicionar um item à pilha
void push(Stack *s, char item) {
    if (isFull(s)) {
        printf("Pilha cheia!\n");
        return;
    }
    s->items[++(s->top)] = item;
}

// Função para remover um item da pilha
char pop(Stack *s) {
    if (isEmpty(s)) {
        printf("Pilha vazia!\n");
        return '\0'; // Valor de erro
    }
    return s->items[(s->top)--];
}

// Função para ver o item no topo da pilha sem removê-lo
char peek(Stack *s) {
    if (isEmpty(s)) {
        return '\0'; // Valor de erro
    }
    return s->items[s->top];
}

// Função para verificar a precedência dos operadores
int precedence(char op) {
    switch (op) {
        case '+':
        case '-':
            return 1;
        case '*':
        case '/':
            return 2;
        case '^':
            return 3;
        default:
            return 0;
    }
}

// Função para converter expressão infixa para pós-fixa
void infixToPostfix(const char *infix, char *postfix) {
    Stack s;
    initStack(&s);
    int k = 0;

    for (int i = 0; infix[i] != '\0'; i++) {
        char ch = infix[i];

        if (isspace(ch)) {
            continue;
        }

        if (isalnum(ch)) {
            postfix[k++] = ch;
        } else if (ch == '(') {
            push(&s, ch);
        } else if (ch == ')') {
            while (!isEmpty(&s) && peek(&s) != '(') {
                postfix[k++] = pop(&s);
            }
            pop(&s); // Remover '('
        } else {
            while (!isEmpty(&s) && precedence(peek(&s)) >= precedence(ch)) {
                postfix[k++] = pop(&s);
            }
            push(&s, ch);
        }
    }

    // Desempilhar todos os operadores restantes
    while (!isEmpty(&s)) {
        postfix[k++] = pop(&s);
    }

    postfix[k] = '\0'; // Terminar a string
}

int main() {
    char infix[MAX], postfix[MAX];

    printf("Digite a expressão infixa: ");
    fgets(infix, sizeof(infix), stdin);

    // Remove o caractere de nova linha, se presente
    size_t len = strlen(infix);
    if (len > 0 && infix[len - 1] == '\n') {
        infix[len - 1] = '\0';
    }

    infixToPostfix(infix, postfix);

    printf("Expressão pós-fixa: %s\n", postfix);

    return 0;
}

QUESTÃO 39:
