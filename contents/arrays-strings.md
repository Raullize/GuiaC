<img width=100% src="https://capsule-render.vercel.app/api?type=waving&color=A8B9CC&height=120&section=header"/>

# 🔠 Arrays e Strings

## 📋 Introdução aos Arrays em C

Um array é uma coleção de elementos do mesmo tipo, armazenados em posições de memória contíguas. Os arrays proporcionam uma forma eficiente de armazenar e acessar múltiplos valores usando um único nome de variável.

### 📊 Declaração e Inicialização de Arrays

#### 1️⃣ Declaração Básica

```c
tipo nome_array[tamanho];
```

Exemplos:
```c
int numeros[5];       // Array de 5 inteiros
float precos[10];     // Array de 10 floats
char caracteres[20];  // Array de 20 caracteres
```

#### 2️⃣ Inicialização no Momento da Declaração

```c
// Inicialização explícita
int numeros[5] = {10, 20, 30, 40, 50};

// Inicialização parcial (restante preenchido com 0)
int parcial[5] = {10, 20};  // Equivale a {10, 20, 0, 0, 0}

// Inicialização sem especificar tamanho (determinado pelo compilador)
int dinamico[] = {1, 2, 3, 4, 5};  // Tamanho 5
```

#### 3️⃣ Acesso aos Elementos

Os elementos de um array são acessados usando índices, que começam em 0:

```c
#include <stdio.h>

int main() {
    int numeros[5] = {10, 20, 30, 40, 50};
    
    // Acesso usando índice
    printf("Primeiro elemento: %d\n", numeros[0]);  // 10
    printf("Terceiro elemento: %d\n", numeros[2]);  // 30
    
    // Modificando um elemento
    numeros[1] = 25;
    printf("Novo valor do segundo elemento: %d\n", numeros[1]);  // 25
    
    return 0;
}
```

### 🔄 Operações com Arrays

#### 1️⃣ Percorrendo um Array

```c
#include <stdio.h>

int main() {
    int numeros[5] = {10, 20, 30, 40, 50};
    int soma = 0;
    
    // Usando loop for para percorrer o array
    for (int i = 0; i < 5; i++) {
        printf("numeros[%d] = %d\n", i, numeros[i]);
        soma += numeros[i];
    }
    
    printf("Soma de todos os elementos: %d\n", soma);
    
    return 0;
}
```

#### 2️⃣ Tamanho de um Array

Você pode determinar o tamanho de um array usando o operador `sizeof`:

```c
#include <stdio.h>

int main() {
    int numeros[] = {10, 20, 30, 40, 50, 60, 70};
    
    // Calculando o número de elementos
    int tamanho = sizeof(numeros) / sizeof(numeros[0]);
    
    printf("O array tem %d elementos\n", tamanho);
    
    return 0;
}
```

### 📏 Arrays Multidimensionais

C suporta arrays com múltiplas dimensões, como matrizes (arrays bidimensionais):

#### 1️⃣ Declaração e Inicialização

```c
// Matriz 3x3
int matriz[3][3] = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};

// Outra forma de inicialização
int matriz2[3][3] = {1, 2, 3, 4, 5, 6, 7, 8, 9};
```

#### 2️⃣ Acesso aos Elementos

```c
#include <stdio.h>

int main() {
    int matriz[3][3] = {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    };
    
    // Acessando elemento [1][2] (segunda linha, terceira coluna)
    printf("matriz[1][2] = %d\n", matriz[1][2]);  // 6
    
    // Percorrendo a matriz
    printf("Elementos da matriz:\n");
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            printf("%d ", matriz[i][j]);
        }
        printf("\n");
    }
    
    return 0;
}
```

#### 3️⃣ Exemplo: Soma de Matrizes

```c
#include <stdio.h>

int main() {
    int A[2][3] = {{1, 2, 3}, {4, 5, 6}};
    int B[2][3] = {{7, 8, 9}, {10, 11, 12}};
    int C[2][3];  // Para armazenar a soma
    
    // Somando as matrizes
    for (int i = 0; i < 2; i++) {
        for (int j = 0; j < 3; j++) {
            C[i][j] = A[i][j] + B[i][j];
        }
    }
    
    // Exibindo o resultado
    printf("Matriz Resultante (A + B):\n");
    for (int i = 0; i < 2; i++) {
        for (int j = 0; j < 3; j++) {
            printf("%3d ", C[i][j]);
        }
        printf("\n");
    }
    
    return 0;
}
```

### 🔤 Strings em C

Em C, strings são implementadas como arrays de caracteres terminados por um caractere nulo (`\0`).

#### 1️⃣ Declaração e Inicialização de Strings

```c
// Inicialização com string literal
char nome[10] = "Carlos";

// Inicialização caractere por caractere
char nome2[10] = {'C', 'a', 'r', 'l', 'o', 's', '\0'};

// Inicialização sem tamanho específico
char nome3[] = "Carlos";  // Tamanho será 7 (6 caracteres + '\0')
```

#### 2️⃣ Entrada e Saída de Strings

```c
#include <stdio.h>

int main() {
    char nome[50];
    
    printf("Digite seu nome: ");
    
    // Leitura de string com scanf (limitação: para no primeiro espaço)
    scanf("%s", nome);
    
    printf("Olá, %s!\n", nome);
    
    return 0;
}
```

Para ler strings com espaços, use `fgets()`:

```c
#include <stdio.h>
#include <string.h>

int main() {
    char nome_completo[50];
    
    printf("Digite seu nome completo: ");
    
    // Leitura de string com fgets (permite espaços)
    fgets(nome_completo, sizeof(nome_completo), stdin);
    
    // Remove o caractere de nova linha capturado pelo fgets
    nome_completo[strcspn(nome_completo, "\n")] = '\0';
    
    printf("Olá, %s!\n", nome_completo);
    
    return 0;
}
```

#### 3️⃣ Funções para Manipulação de Strings

A biblioteca padrão `string.h` fornece várias funções para manipular strings:

```c
#include <stdio.h>
#include <string.h>

int main() {
    char str1[20] = "Olá";
    char str2[20] = "Mundo";
    char resultado[40];
    
    // Tamanho da string (sem contar o caractere nulo)
    printf("Tamanho de str1: %lu\n", strlen(str1));
    
    // Cópia de strings
    strcpy(resultado, str1);
    printf("Após strcpy: %s\n", resultado);
    
    // Concatenação de strings
    strcat(resultado, " ");
    strcat(resultado, str2);
    printf("Após strcat: %s\n", resultado);
    
    // Comparação de strings
    if (strcmp(str1, str2) == 0) {
        printf("str1 e str2 são iguais\n");
    } else {
        printf("str1 e str2 são diferentes\n");
    }
    
    return 0;
}
```

#### 🔑 Principais Funções de String

| Função         | Descrição                                            |
|----------------|------------------------------------------------------|
| `strlen(s)`    | Retorna o comprimento da string                      |
| `strcpy(d, s)` | Copia a string s para d                              |
| `strncpy(d, s, n)` | Copia até n caracteres de s para d               |
| `strcat(d, s)` | Concatena a string s ao final de d                   |
| `strncat(d, s, n)` | Concatena até n caracteres de s ao final de d    |
| `strcmp(s1, s2)` | Compara s1 com s2 (0 se iguais)                    |
| `strncmp(s1, s2, n)` | Compara até n caracteres de s1 com s2          |
| `strchr(s, c)` | Localiza a primeira ocorrência do caractere c em s   |
| `strstr(s1, s2)` | Localiza a primeira ocorrência da string s2 em s1  |
| `strtok(s, d)` | Divide uma string em tokens usando d como delimitador|

### 🛠️ Arrays como Parâmetros de Funções

Arrays podem ser passados como argumentos para funções. Na verdade, o que é passado é o endereço do primeiro elemento do array.

```c
#include <stdio.h>

// Função que recebe um array e seu tamanho
void imprimirArray(int arr[], int tamanho) {
    for (int i = 0; i < tamanho; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
}

// Função que modifica um array
void dobrarValores(int arr[], int tamanho) {
    for (int i = 0; i < tamanho; i++) {
        arr[i] *= 2;
    }
}

int main() {
    int numeros[] = {1, 2, 3, 4, 5};
    int tamanho = sizeof(numeros) / sizeof(numeros[0]);
    
    printf("Array original: ");
    imprimirArray(numeros, tamanho);
    
    dobrarValores(numeros, tamanho);
    
    printf("Array após dobrar valores: ");
    imprimirArray(numeros, tamanho);
    
    return 0;
}
```

Observe que a modificação do array dentro da função afeta o array original, porque o endereço do array é passado, não uma cópia.

### 🧩 Exemplo: Ordenação de um Array

Vamos implementar um algoritmo de ordenação simples (Bubble Sort) para ordenar um array:

```c
#include <stdio.h>

void bubbleSort(int arr[], int tamanho) {
    for (int i = 0; i < tamanho - 1; i++) {
        for (int j = 0; j < tamanho - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                // Troca os elementos
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
}

void imprimirArray(int arr[], int tamanho) {
    for (int i = 0; i < tamanho; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
}

int main() {
    int numeros[] = {64, 34, 25, 12, 22, 11, 90};
    int tamanho = sizeof(numeros) / sizeof(numeros[0]);
    
    printf("Array original: ");
    imprimirArray(numeros, tamanho);
    
    bubbleSort(numeros, tamanho);
    
    printf("Array ordenado: ");
    imprimirArray(numeros, tamanho);
    
    return 0;
}
```

### 🔤 Exemplo: Manipulação de Strings

Vamos criar um programa que inverte uma string:

```c
#include <stdio.h>
#include <string.h>

void inverterString(char str[]) {
    int tamanho = strlen(str);
    char temp;
    
    for (int i = 0; i < tamanho / 2; i++) {
        // Troca os caracteres simetricamente
        temp = str[i];
        str[i] = str[tamanho - 1 - i];
        str[tamanho - 1 - i] = temp;
    }
}

int main() {
    char texto[100];
    
    printf("Digite uma palavra ou frase: ");
    fgets(texto, sizeof(texto), stdin);
    
    // Remove o caractere de nova linha
    texto[strcspn(texto, "\n")] = '\0';
    
    printf("Texto original: %s\n", texto);
    
    inverterString(texto);
    
    printf("Texto invertido: %s\n", texto);
    
    return 0;
}
```

### 🧬 Arrays Dinâmicos

Em C, também é possível criar arrays cujo tamanho é determinado durante a execução do programa, usando alocação dinâmica de memória:

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int tamanho;
    int *array;
    
    printf("Digite o tamanho do array: ");
    scanf("%d", &tamanho);
    
    // Aloca memória dinamicamente
    array = (int*)malloc(tamanho * sizeof(int));
    
    if (array == NULL) {
        printf("Erro: Falha na alocação de memória\n");
        return 1;
    }
    
    // Preenche o array
    for (int i = 0; i < tamanho; i++) {
        array[i] = i * 10;
    }
    
    // Exibe o array
    printf("Array alocado dinamicamente:\n");
    for (int i = 0; i < tamanho; i++) {
        printf("%d ", array[i]);
    }
    printf("\n");
    
    // Libera a memória
    free(array);
    
    return 0;
}
```

### 🚫 Problemas Comuns com Arrays e Strings

#### 1️⃣ Acesso Fora dos Limites

C não verifica automaticamente os limites dos arrays. Acessar elementos fora do intervalo válido causa comportamento indefinido.

```c
int numeros[5] = {1, 2, 3, 4, 5};

// PERIGO: Acesso fora dos limites
numeros[5] = 6;  // O índice válido vai de 0 a 4
```

#### 2️⃣ Esquecer o Caractere Nulo em Strings

```c
char nome[5];
nome[0] = 'J';
nome[1] = 'o';
nome[2] = 'a';
nome[3] = 'o';
// ERRO: Esqueceu de adicionar '\0'
printf("%s", nome);  // Pode exibir caracteres além de "Joao"
```

#### 3️⃣ Estouro de Buffer em Strings

```c
char pequeno[5];
// PERIGO: "Programação" tem mais caracteres que o buffer pode armazenar
strcpy(pequeno, "Programação");  // Estouro de buffer
```

### 🎭 Programa Completo: Sistema de Gestão de Alunos

Vamos criar um sistema simples para gerenciar informações de alunos, demonstrando o uso de arrays, strings e matrizes:

```c
#include <stdio.h>
#include <string.h>

#define MAX_ALUNOS 100
#define MAX_NOME 50
#define NUM_NOTAS 3

typedef struct {
    char nome[MAX_NOME];
    int matricula;
    float notas[NUM_NOTAS];
    float media;
} Aluno;

// Calcula a média das notas de um aluno
float calcularMedia(float notas[], int numNotas) {
    float soma = 0;
    for (int i = 0; i < numNotas; i++) {
        soma += notas[i];
    }
    return soma / numNotas;
}

// Adiciona um novo aluno na lista
int adicionarAluno(Aluno alunos[], int numAlunos) {
    if (numAlunos >= MAX_ALUNOS) {
        printf("Erro: Número máximo de alunos atingido.\n");
        return numAlunos;
    }
    
    Aluno novoAluno;
    
    printf("\n=== Cadastro de Novo Aluno ===\n");
    
    printf("Nome: ");
    scanf(" %[^\n]", novoAluno.nome);
    
    printf("Matrícula: ");
    scanf("%d", &novoAluno.matricula);
    
    for (int i = 0; i < NUM_NOTAS; i++) {
        printf("Nota %d: ", i + 1);
        scanf("%f", &novoAluno.notas[i]);
        
        // Validação de nota
        while (novoAluno.notas[i] < 0 || novoAluno.notas[i] > 10) {
            printf("Nota inválida! Digite novamente (0-10): ");
            scanf("%f", &novoAluno.notas[i]);
        }
    }
    
    novoAluno.media = calcularMedia(novoAluno.notas, NUM_NOTAS);
    
    alunos[numAlunos] = novoAluno;
    return numAlunos + 1;
}

// Exibe todos os alunos cadastrados
void exibirAlunos(Aluno alunos[], int numAlunos) {
    if (numAlunos == 0) {
        printf("\nNenhum aluno cadastrado.\n");
        return;
    }
    
    printf("\n=== Lista de Alunos ===\n");
    printf("%-5s %-30s %-10s %-20s %-7s\n", "ID", "Nome", "Matrícula", "Notas", "Média");
    printf("-------------------------------------------------------------------------\n");
    
    for (int i = 0; i < numAlunos; i++) {
        printf("%-5d %-30s %-10d [", i + 1, alunos[i].nome, alunos[i].matricula);
        
        for (int j = 0; j < NUM_NOTAS; j++) {
            printf("%.1f", alunos[i].notas[j]);
            if (j < NUM_NOTAS - 1) printf(", ");
        }
        
        printf("] %-7.2f\n", alunos[i].media);
    }
}

// Busca um aluno pelo nome
void buscarAluno(Aluno alunos[], int numAlunos) {
    if (numAlunos == 0) {
        printf("\nNenhum aluno cadastrado.\n");
        return;
    }
    
    char nomeBusca[MAX_NOME];
    printf("\nDigite o nome para busca: ");
    scanf(" %[^\n]", nomeBusca);
    
    printf("\n=== Resultados da Busca ===\n");
    
    int encontrados = 0;
    for (int i = 0; i < numAlunos; i++) {
        // Busca caso insensitivo
        if (strcasecmp(alunos[i].nome, nomeBusca) == 0) {
            printf("ID: %d\n", i + 1);
            printf("Nome: %s\n", alunos[i].nome);
            printf("Matrícula: %d\n", alunos[i].matricula);
            printf("Notas: ");
            
            for (int j = 0; j < NUM_NOTAS; j++) {
                printf("%.1f", alunos[i].notas[j]);
                if (j < NUM_NOTAS - 1) printf(", ");
            }
            
            printf("\nMédia: %.2f\n", alunos[i].media);
            printf("Situação: %s\n\n", alunos[i].media >= 6.0 ? "Aprovado" : "Reprovado");
            
            encontrados++;
        }
    }
    
    if (encontrados == 0) {
        printf("Nenhum aluno encontrado com o nome '%s'.\n", nomeBusca);
    }
}

int main() {
    Aluno alunos[MAX_ALUNOS];
    int numAlunos = 0;
    int opcao;
    
    do {
        printf("\n=== Sistema de Gestão de Alunos ===\n");
        printf("1. Adicionar Aluno\n");
        printf("2. Exibir Todos os Alunos\n");
        printf("3. Buscar Aluno por Nome\n");
        printf("0. Sair\n");
        printf("Escolha uma opção: ");
        scanf("%d", &opcao);
        
        switch (opcao) {
            case 1:
                numAlunos = adicionarAluno(alunos, numAlunos);
                break;
            case 2:
                exibirAlunos(alunos, numAlunos);
                break;
            case 3:
                buscarAluno(alunos, numAlunos);
                break;
            case 0:
                printf("Saindo do programa...\n");
                break;
            default:
                printf("Opção inválida!\n");
        }
    } while (opcao != 0);
    
    return 0;
}
```

Este programa demonstra vários conceitos:
- Uso de arrays para armazenar notas
- Uso de strings para armazenar nomes
- Array de estruturas para armazenar informações completas
- Passagem de arrays para funções
- Manipulação de strings para busca
- Validação de dados de entrada

---

[🔙 Voltar ao índice principal](../README.md)

<img width=100% src="https://capsule-render.vercel.app/api?type=waving&color=A8B9CC&height=120&section=footer"/> 