ATIVIDADE 04 - Lista de Algoritmos Parte 3 JOÃO GUILHERME GOMES SANNA

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
#include <stdio.h>
#include <stdlib.h>
#include <ctype.h>

#define MAX 100

// Função para verificar se o caractere é um dígito
int isDigit(char c) {
    return c >= '0' && c <= '9';
}

// Função para retornar o valor inteiro do caractere
int charToInt(char c) {
    return c - '0';
}

// Função para avaliar a expressão pós-fixa
int evaluatePostfix(const char* expression) {
    int stack[MAX];
    int top = -1;

    for (int i = 0; expression[i] != '\0'; ++i) {
        char token = expression[i];

        if (isDigit(token)) {
            // Empurrar o dígito para a pilha
            stack[++top] = charToInt(token);
        } else if (token == ' ') {
            // Ignorar espaços
            continue;
        } else {
            // Operador, então pop dois operandos da pilha
            int right = stack[top--];
            int left = stack[top--];

            // Aplicar o operador
            switch (token) {
                case '+': stack[++top] = left + right; break;
                case '-': stack[++top] = left - right; break;
                case '*': stack[++top] = left * right; break;
                case '/': stack[++top] = left / right; break;
                default:
                    printf("Operador desconhecido: %c\n", token);
                    exit(1);
            }
        }
    }

    // O resultado final estará no topo da pilha
    return stack[top];
}

int main() {
    const char* expression = "3 4 + 2 * 7 /";

    int result = evaluatePostfix(expression);
    printf("O resultado da expressão pós-fixa '%s' é %d\n", expression, result);

    return 0;
}

QUESTÃO 40:
#include <stdio.h>

#define SIZE 3

void printBoard(char board[SIZE][SIZE]) {
    printf("\n");
    for (int i = 0; i < SIZE; i++) {
        for (int j = 0; j < SIZE; j++) {
            printf(" %c ", board[i][j]);
            if (j < SIZE - 1) printf("|");
        }
        printf("\n");
        if (i < SIZE - 1) {
            for (int j = 0; j < SIZE; j++) {
                printf("---");
                if (j < SIZE - 1) printf("|");
            }
            printf("\n");
        }
    }
    printf("\n");
}

int checkWin(char board[SIZE][SIZE], char player) {
    // Check rows and columns
    for (int i = 0; i < SIZE; i++) {
        if ((board[i][0] == player && board[i][1] == player && board[i][2] == player) ||
            (board[0][i] == player && board[1][i] == player && board[2][i] == player)) {
            return 1;
        }
    }

    // Check diagonals
    if ((board[0][0] == player && board[1][1] == player && board[2][2] == player) ||
        (board[0][2] == player && board[1][1] == player && board[2][0] == player)) {
        return 1;
    }

    return 0;
}

int checkDraw(char board[SIZE][SIZE]) {
    for (int i = 0; i < SIZE; i++) {
        for (int j = 0; j < SIZE; j++) {
            if (board[i][j] == ' ') {
                return 0;
            }
        }
    }
    return 1;
}

void playGame() {
    char board[SIZE][SIZE] = { {' ', ' ', ' '}, {' ', ' ', ' '}, {' ', ' ', ' '} };
    char player = 'X';
    int row, col;

    while (1) {
        printBoard(board);
        printf("Jogador %c, insira linha e coluna (0-2): ", player);
        scanf("%d %d", &row, &col);

        // Validar movimento
        if (row < 0 || row >= SIZE || col < 0 || col >= SIZE || board[row][col] != ' ') {
            printf("Movimento inválido. Tente novamente.\n");
            continue;
        }

        // Fazer o movimento
        board[row][col] = player;

        // Verificar vitória
        if (checkWin(board, player)) {
            printBoard(board);
            printf("Parabéns, jogador %c! Você ganhou!\n", player);
            break;
        }

        // Verificar empate
        if (checkDraw(board)) {
            printBoard(board);
            printf("Empate!\n");
            break;
        }

        // Trocar jogador
        player = (player == 'X') ? 'O' : 'X';
    }
}

int main() {
    printf("Bem-vindo ao Jogo da Velha!\n");
    playGame();
    return 0;
}

QUESTÃO 41:
#include <stdio.h>
#include <ctype.h>

#define ALPHABET_SIZE 26

// Função para criptografar uma mensagem usando a Cifra de César
void cifraCesar(char *mensagem, int chave) {
    while (*mensagem) {
        if (isalpha(*mensagem)) {
            char offset = islower(*mensagem) ? 'a' : 'A';
            *mensagem = (*mensagem - offset + chave) % ALPHABET_SIZE + offset;
        }
        mensagem++;
    }
}

// Função para descriptografar uma mensagem usando a Cifra de César
void decifraCesar(char *mensagem, int chave) {
    cifraCesar(mensagem, ALPHABET_SIZE - chave); // Descriptografar é criptografar com a chave invertida
}

int main() {
    char mensagem[100];
    int chave;
    int opcao;

    printf("Digite a mensagem (max 99 caracteres): ");
    fgets(mensagem, sizeof(mensagem), stdin);

    // Remover o newline no final da mensagem, se presente
    size_t len = strlen(mensagem);
    if (len > 0 && mensagem[len - 1] == '\n') {
        mensagem[len - 1] = '\0';
    }

    printf("Digite a chave (um número inteiro): ");
    scanf("%d", &chave);

    // Ajustar a chave para estar dentro do intervalo do alfabeto
    chave = chave % ALPHABET_SIZE;

    printf("Escolha uma opção:\n");
    printf("1. Criptografar\n");
    printf("2. Descriptografar\n");
    printf("Digite a opção (1 ou 2): ");
    scanf("%d", &opcao);

    if (opcao == 1) {
        cifraCesar(mensagem, chave);
        printf("Mensagem criptografada: %s\n", mensagem);
    } else if (opcao == 2) {
        decifraCesar(mensagem, chave);
        printf("Mensagem descriptografada: %s\n", mensagem);
    } else {
        printf("Opção inválida!\n");
    }

    return 0;
}

QUESTÃO 42:
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

#define MIN 1
#define MAX 100

int main() {
    int numero_aleatorio;

    // Inicializa o gerador de números aleatórios com base no tempo atual
    srand(time(NULL));

    // Gera um número aleatório entre 1 e 100
    numero_aleatorio = (rand() % (MAX - MIN + 1)) + MIN;

    printf("Número aleatório entre %d e %d: %d\n", MIN, MAX, numero_aleatorio);
#include <stdio.h>

#define MAX_SIZE 100

void printLIS(int arr[], int n, int lis[]) {
    printf("Maior subsequência crescente: ");
    for (int i = 0; i < n; i++) {
        if (lis[i] == 1) {
            printf("%d ", arr[i]);
        }
    }
    printf("\n");
}

void findLIS(int arr[], int n) {
    int lis[MAX_SIZE];
    int maxLength = 1;
    int maxIndex = 0;

    // Inicializa o array LIS
    for (int i = 0; i < n; i++) {
        lis[i] = 1;
    }

    // Preenche o array LIS
    for (int i = 1; i < n; i++) {
        for (int j = 0; j < i; j++) {
            if (arr[i] > arr[j] && lis[i] < lis[j] + 1) {
                lis[i] = lis[j] + 1;
            }
        }
        if (lis[i] > maxLength) {
            maxLength = lis[i];
            maxIndex = i;
        }
    }

    // Exibe o resultado
    printf("Comprimento da maior subsequência crescente: %d\n", maxLength);
    printLIS(arr, maxIndex + 1, lis);
}

int main() {
    int arr[MAX_SIZE];
    int n;

    printf("Digite o número de elementos: ");
    scanf("%d", &n);

    if (n > MAX_SIZE) {
        printf("Número de elementos excede o tamanho máximo permitido.\n");
        return 1;
    }

    printf("Digite os elementos do vetor:\n");
    for (int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }

    findLIS(arr, n);

    return 0;
}

QUESTÃO 44:
#include <stdio.h>

#define BOARD_SIZE 8

// Função para verificar se uma posição está dentro dos limites do tabuleiro
int isValidMove(int x, int y) {
    return x >= 0 && x < BOARD_SIZE && y >= 0 && y < BOARD_SIZE;
}

// Função para imprimir a posição em formato de coordenadas (letra + número)
void printPosition(int x, int y) {
    printf("(%c, %d)\n", 'a' + y, BOARD_SIZE - x);
}

// Função para encontrar e exibir todos os movimentos possíveis do cavalo
void findKnightMoves(int x, int y) {
    // Possíveis movimentos do cavalo
    int moves[8][2] = {
        {2, 1}, {2, -1},
        {-2, 1}, {-2, -1},
        {1, 2}, {1, -2},
        {-1, 2}, {-1, -2}
    };

    printf("Movimentos possíveis do cavalo a partir da posição (%c, %d):\n", 'a' + y, BOARD_SIZE - x);

    for (int i = 0; i < 8; i++) {
        int newX = x + moves[i][0];
        int newY = y + moves[i][1];
        if (isValidMove(newX, newY)) {
            printPosition(newX, newY);
        }
    }
}

int main() {
    char col;
    int row;
    int x, y;

    printf("Digite a posição inicial do cavalo (por exemplo, 'e4'):\n");
    scanf(" %c%d", &col, &row);

    // Converter a entrada para índices do array (0-7)
    x = BOARD_SIZE - row;   // Converter linha para índice de 0 a 7
    y = col - 'a';          // Converter coluna para índice de 0 a 7

    if (isValidMove(x, y)) {
        findKnightMoves(x, y);
    } else {
        printf("Posição inválida. As coordenadas devem estar entre 'a1' e 'h8'.\n");
    }

    return 0;
}

QUESTÃO 45:
#include <stdio.h>

#define N 9

// Função para imprimir o tabuleiro do Sudoku
void printBoard(int board[N][N]) {
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++) {
            printf("%d ", board[i][j]);
        }
        printf("\n");
    }
}

// Função para verificar se um número pode ser colocado na posição (linha, coluna)
int isSafe(int board[N][N], int row, int col, int num) {
    // Verificar a linha
    for (int x = 0; x < N; x++) {
        if (board[row][x] == num) {
            return 0;
        }
    }

    // Verificar a coluna
    for (int x = 0; x < N; x++) {
        if (board[x][col] == num) {
            return 0;
        }
    }

    // Verificar o sub-quadrante 3x3
    int startRow = row - row % 3;
    int startCol = col - col % 3;
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            if (board[i + startRow][j + startCol] == num) {
                return 0;
            }
        }
    }

    return 1;
}

// Função para resolver o Sudoku usando backtracking
int solveSudoku(int board[N][N]) {
    int row, col;

    // Verificar se há uma célula vazia
    int isEmpty = 0;
    for (row = 0; row < N; row++) {
        for (col = 0; col < N; col++) {
            if (board[row][col] == 0) {
                isEmpty = 1;
                break;
            }
        }
        if (isEmpty) {
            break;
        }
    }

    // Se não houver célula vazia, o Sudoku está resolvido
    if (!isEmpty) {
        return 1;
    }

    // Tentar todos os números de 1 a 9
    for (int num = 1; num <= N; num++) {
        if (isSafe(board, row, col, num)) {
            // Atribuir num à célula
            board[row][col] = num;

            // Recursivamente tentar resolver o Sudoku
            if (solveSudoku(board)) {
                return 1;
            }

            // Se a solução não for encontrada, desfaça a atribuição
            board[row][col] = 0;
        }
    }

    // Se nenhum número é válido, retornar false
    return 0;
}

int main() {
    int board[N][N] = {
        {5, 3, 0, 0, 7, 0, 0, 0, 0},
        {6, 0, 0, 1, 9, 5, 0, 0, 0},
        {0, 9, 8, 0, 0, 0, 0, 6, 0},
        {8, 0, 0, 0, 6, 0, 0, 0, 3},
        {4, 0, 0, 8, 0, 3, 0, 0, 1},
        {7, 0, 0, 0, 2, 0, 0, 0, 6},
        {0, 6, 0, 0, 0, 0, 2, 8, 0},
        {0, 0, 0, 4, 1, 9, 0, 0, 5},
        {0, 0, 0, 0, 8, 0, 0, 7, 9}
    };

    printf("Tabuleiro do Sudoku inicial:\n");
    printBoard(board);

    if (solveSudoku(board)) {
        printf("\nTabuleiro do Sudoku resolvido:\n");
        printBoard(board);
    } else {
        printf("\nNão foi possível resolver o Sudoku.\n");
    }

    return 0;
}

QUESTÃO 46:
#include <stdio.h>
#include <limits.h>

#define V 9 // Número de vértices no grafo

// Função para encontrar o vértice com a distância mínima
int minDistance(int dist[], int sptSet[]) {
    int min = INT_MAX;
    int min_index;

    for (int v = 0; v < V; v++) {
        if (!sptSet[v] && dist[v] <= min) {
            min = dist[v];
            min_index = v;
        }
    }
    return min_index;
}

// Função para imprimir o array de distâncias
void printSolution(int dist[], int n) {
    printf("Vértice   Distância da origem\n");
    for (int i = 0; i < n; i++) {
        printf("%d \t\t %d\n", i, dist[i]);
    }
}

// Função para implementar o Algoritmo de Dijkstra
void dijkstra(int graph[V][V], int src) {
    int dist[V];    // Array para armazenar a menor distância de src para cada vértice
    int sptSet[V];  // Array para indicar se o vértice está incluído no conjunto de caminhos mais curtos

    // Inicializa as distâncias como infinito e sptSet como falso
    for (int i = 0; i < V; i++) {
        dist[i] = INT_MAX;
        sptSet[i] = 0;
    }

    // A distância do vértice de origem para ele mesmo é sempre 0
    dist[src] = 0;

    // Encontrar o caminho mais curto para todos os vértices
    for (int count = 0; count < V - 1; count++) {
        // Escolhe o vértice com a distância mínima do conjunto de vértices não processados
        int u = minDistance(dist, sptSet);

        // Marca o vértice como processado
        sptSet[u] = 1;

        // Atualiza o valor da distância dos vértices adjacentes ao vértice escolhido
        for (int v = 0; v < V; v++) {
            // Atualiza dist[v] se houver um caminho mais curto de u para v
            if (!sptSet[v] && graph[u][v] && dist[u] != INT_MAX && dist[u] + graph[u][v] < dist[v]) {
                dist[v] = dist[u] + graph[u][v];
            }
        }
    }

    // Imprime o array de distâncias
    printSolution(dist, V);
}

int main() {
    // Matriz de adjacência do grafo
    int graph[V][V] = {
        {0, 4, 0, 0, 0, 0, 0, 8, 0},
        {4, 0, 8, 0, 0, 0, 0, 11, 0},
        {0, 8, 0, 7, 0, 4, 0, 0, 2},
        {0, 0, 7, 0, 9, 14, 0, 0, 0},
        {0, 0, 0, 9, 0, 10, 0, 0, 0},
        {0, 0, 4, 14, 10, 0, 2, 0, 0},
        {0, 0, 0, 0, 0, 2, 0, 1, 6},
        {8, 11, 0, 0, 0, 0, 1, 0, 7},
        {0, 0, 2, 0, 0, 0, 6, 7, 0}
    };

    dijkstra(graph, 0);

    return 0;
}

QUESTÃO 47:
#include <stdio.h>
#include <stdlib.h>

// Estrutura para representar uma aresta
typedef struct {
    int src, dest, weight;
} Edge;

// Estrutura para representar um subconjunto para union-find
typedef struct {
    int parent, rank;
} Subset;

// Função para comparar duas arestas (para ordenação)
int compareEdges(const void* a, const void* b) {
    Edge* edgeA = (Edge*)a;
    Edge* edgeB = (Edge*)b;
    return edgeA->weight - edgeB->weight;
}

// Função para encontrar o representante de um subconjunto (find)
int find(Subset subsets[], int i) {
    if (subsets[i].parent != i) {
        subsets[i].parent = find(subsets, subsets[i].parent);
    }
    return subsets[i].parent;
}

// Função para unir dois subconjuntos (union)
void unionSubsets(Subset subsets[], int x, int y) {
    int xroot = find(subsets, x);
    int yroot = find(subsets, y);

    if (subsets[xroot].rank < subsets[yroot].rank) {
        subsets[xroot].parent = yroot;
    } else if (subsets[xroot].rank > subsets[yroot].rank) {
        subsets[yroot].parent = xroot;
    } else {
        subsets[yroot].parent = xroot;
        subsets[xroot].rank++;
    }
}

// Função para implementar o Algoritmo de Kruskal
void kruskal(Edge edges[], int V, int E) {
    Edge result[V]; // Array para armazenar a MST
    int e = 0; // Contador para o número de arestas na MST
    int i = 0; // Índice para as arestas ordenadas

    // Ordenar todas as arestas em ordem crescente de peso
    qsort(edges, E, sizeof(Edge), compareEdges);

    // Criar V subconjuntos com um único elemento
    Subset subsets[V];
    for (int v = 0; v < V; ++v) {
        subsets[v].parent = v;
        subsets[v].rank = 0;
    }

    // Adicionar arestas à MST
    while (e < V - 1 && i < E) {
        Edge nextEdge = edges[i++];
        int x = find(subsets, nextEdge.src);
        int y = find(subsets, nextEdge.dest);

        // Se a inclusão da aresta não formar um ciclo
        if (x != y) {
            result[e++] = nextEdge;
            unionSubsets(subsets, x, y);
        }
    }

    // Imprimir a MST
    printf("Arestas na Árvore Geradora Mínima:\n");
    int minimumCost = 0;
    for (i = 0; i < e; ++i) {
        printf("%d - %d: %d\n", result[i].src, result[i].dest, result[i].weight);
        minimumCost += result[i].weight;
    }
    printf("Custo total da Árvore Geradora Mínima: %d\n", minimumCost);
}

int main() {
    int V = 4; // Número de vértices
    int E = 5; // Número de arestas

    // Array de arestas (src, dest, peso)
    Edge edges[] = {
        {0, 1, 10},
        {0, 2, 6},
        {0, 3, 5},
        {1, 3, 15},
        {2, 3, 4}
    };

    kruskal(edges, V, E);

    return 0;
}

QUESTÃO 48:
#include <stdio.h>
#include <stdlib.h>

#define MAX_FLOORS 10

typedef struct {
    int currentFloor;
    int requestedFloor;
    int direction; // 1 para cima, -1 para baixo, 0 para parado
} Elevator;

void printElevatorStatus(Elevator elevator) {
    printf("Elevador está no andar %d\n", elevator.currentFloor);
    if (elevator.direction == 1) {
        printf("Direção: Subindo\n");
    } else if (elevator.direction == -1) {
        printf("Direção: Descendo\n");
    } else {
        printf("Direção: Parado\n");
    }
}

void moveElevator(Elevator *elevator) {
    if (elevator->currentFloor < elevator->requestedFloor) {
        elevator->direction = 1;
        elevator->currentFloor++;
    } else if (elevator->currentFloor > elevator->requestedFloor) {
        elevator->direction = -1;
        elevator->currentFloor--;
    } else {
        elevator->direction = 0;
    }
}

int main() {
    Elevator elevator;
    elevator.currentFloor = 0; // Elevador começa no andar 0
    elevator.requestedFloor = -1;
    elevator.direction = 0;

    int request;
    int exit = 0;

    printf("Simulador de Elevador\n");
    printf("O prédio tem %d andares (0 a %d)\n", MAX_FLOORS, MAX_FLOORS - 1);

    while (!exit) {
        printElevatorStatus(elevator);

        if (elevator.direction == 0) {
            printf("Digite o andar para o qual deseja chamar o elevador (ou -1 para sair): ");
            scanf("%d", &request);

            if (request == -1) {
                exit = 1;
            } else if (request >= 0 && request < MAX_FLOORS) {
                elevator.requestedFloor = request;
            } else {
                printf("Andar inválido! Por favor, escolha um andar entre 0 e %d.\n", MAX_FLOORS - 1);
            }
        } else {
            moveElevator(&elevator);

            if (elevator.direction == 0) {
                printf("Elevador chegou ao andar %d\n", elevator.currentFloor);
            }
        }
    }

    printf("Simulação encerrada.\n");
    return 0;
}

QUESTÃO 49:
#include <stdio.h>
#include <string.h>

void searchPattern(const char *text, const char *pattern) {
    int textLen = strlen(text);
    int patternLen = strlen(pattern);

    // Percorre o texto para procurar o padrão
    for (int i = 0; i <= textLen - patternLen; i++) {
        int j;
        // Verifica se o padrão corresponde ao segmento do texto
        for (j = 0; j < patternLen; j++) {
            if (text[i + j] != pattern[j]) {
                break;
            }
        }

        // Se o padrão é encontrado
        if (j == patternLen) {
            printf("Padrão encontrado na posição %d\n", i);
        }
    }
}

int main() {
    char text[100];
    char pattern[100];

    // Recebe o texto e o padrão do usuário
    printf("Digite o texto: ");
    fgets(text, sizeof(text), stdin);
    text[strcspn(text, "\n")] = '\0'; // Remove o caractere de nova linha

    printf("Digite o padrão a ser buscado: ");
    fgets(pattern, sizeof(pattern), stdin);
    pattern[strcspn(pattern, "\n")] = '\0'; // Remove o caractere de nova linha

    // Chama a função de busca de padrão
    searchPattern(text, pattern);

    return 0;
}

QUESTÃO 50:
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

#define MAX_LEN 1000

// Função para comprimir dados usando RLE
void compressRLE(const char *input, char *output) {
    int len = strlen(input);
    int count = 1;
    int j = 0;

    for (int i = 0; i < len; i++) {
        if (i < len - 1 && input[i] == input[i + 1]) {
            count++;
        } else {
            output[j++] = input[i];
            output[j++] = count + '0'; // Convertendo o número para caractere
            count = 1;
        }
    }
    output[j] = '\0'; // Finaliza a string de saída
}

// Função para descomprimir dados usando RLE
void decompressRLE(const char *input, char *output) {
    int len = strlen(input);
    int j = 0;

    for (int i = 0; i < len; i += 2) {
        char ch = input[i];
        int count = input[i + 1] - '0'; // Convertendo caractere para número

        for (int k = 0; k < count; k++) {
            output[j++] = ch;
        }
    }
    output[j] = '\0'; // Finaliza a string de saída
}

int main() {
    char input[MAX_LEN];
    char compressed[MAX_LEN];
    char decompressed[MAX_LEN];

    // Recebe a string de entrada
    printf("Digite a string para compressão: ");
    fgets(input, sizeof(input), stdin);
    input[strcspn(input, "\n")] = '\0'; // Remove o caractere de nova linha

    // Compressão
    compressRLE(input, compressed);
    printf("String comprimida: %s\n", compressed);

    // Descompressão
    decompressRLE(compressed, decompressed);
    printf("String descomprimida: %s\n", decompressed);

    return 0;
}

    return 0;
}

QUESTÃO 43:
