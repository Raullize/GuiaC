<img width=100% src="https://capsule-render.vercel.app/api?type=waving&color=A8B9CC&height=120&section=header"/>

# 🔁 Funções Recursivas

## 📋 Compreendendo a Recursão em C

Recursão é uma técnica poderosa onde uma função chama a si mesma para resolver um problema. Essa abordagem permite solucionar problemas complexos dividindo-os em casos mais simples, seguindo o paradigma "dividir para conquistar".

### 🧩 Conceitos Fundamentais da Recursão

A recursão é baseada em dois componentes essenciais:

1. **Caso Base**: A condição de parada que encerra as chamadas recursivas
2. **Caso Recursivo**: A parte que divide o problema e faz a chamada recursiva

Uma função recursiva bem estruturada sempre deve ter pelo menos um caso base que possa ser resolvido diretamente, sem recursão adicional.

#### 1️⃣ Anatomia de uma Função Recursiva

```c
tipo_retorno funcao_recursiva(parametros) {
    // Caso base - condição de parada
    if (condicao_de_parada) {
        return valor_caso_base;
    }
    
    // Caso recursivo 
    // Processa e reduz o problema
    // Chama a si mesma com entrada reduzida
    return funcao_recursiva(entrada_reduzida);
}
```

### ⭐ Exemplos Clássicos de Recursão

#### 1️⃣ Fatorial

O fatorial de um número n (representado como n!) é o produto de todos os inteiros positivos menores ou iguais a n.

```c
#include <stdio.h>

// Função recursiva para calcular o fatorial
unsigned long fatorial(unsigned int n) {
    // Caso base
    if (n == 0 || n == 1) {
        return 1;
    }
    
    // Caso recursivo
    return n * fatorial(n - 1);
}

int main() {
    unsigned int numero = 5;
    printf("Fatorial de %u = %lu\n", numero, fatorial(numero));
    return 0;
}
```

**Explicação da Recursão**:
- Caso base: Se n = 0 ou n = 1, retorna 1
- Caso recursivo: Para n > 1, calcula n * fatorial(n-1)

**Execução para fatorial(5)**:
```
fatorial(5) = 5 * fatorial(4)
             = 5 * (4 * fatorial(3))
             = 5 * (4 * (3 * fatorial(2)))
             = 5 * (4 * (3 * (2 * fatorial(1))))
             = 5 * (4 * (3 * (2 * 1)))
             = 5 * (4 * (3 * 2))
             = 5 * (4 * 6)
             = 5 * 24
             = 120
```

#### 2️⃣ Fibonacci

A sequência de Fibonacci é uma série onde cada número é a soma dos dois anteriores. Começa com 0 e 1, e continua: 0, 1, 1, 2, 3, 5, 8, 13, ...

```c
#include <stdio.h>

// Função recursiva para calcular o n-ésimo número de Fibonacci
int fibonacci(int n) {
    // Casos base
    if (n <= 0) {
        return 0;
    }
    if (n == 1) {
        return 1;
    }
    
    // Caso recursivo
    return fibonacci(n - 1) + fibonacci(n - 2);
}

int main() {
    int n = 7;
    printf("O %d-ésimo número de Fibonacci é: %d\n", n, fibonacci(n));
    
    printf("Primeiros 10 números da sequência de Fibonacci:\n");
    for (int i = 0; i < 10; i++) {
        printf("%d ", fibonacci(i));
    }
    printf("\n");
    
    return 0;
}
```

**Explicação da Recursão**:
- Casos base: Se n ≤ 0, retorna 0; Se n = 1, retorna 1
- Caso recursivo: Para n > 1, calcula fibonacci(n-1) + fibonacci(n-2)

**Árvore recursiva para fibonacci(5)**:
```
                      fib(5)
                    /        \
               fib(4)         fib(3)
              /      \        /     \
         fib(3)      fib(2)  fib(2)  fib(1)
        /     \      /    \   /    \
   fib(2)   fib(1) fib(1) fib(0) fib(1) fib(0)
  /     \
fib(1) fib(0)
```

#### 3️⃣ Máximo Divisor Comum (MDC)

O algoritmo de Euclides para encontrar o MDC pode ser implementado de forma recursiva.

```c
#include <stdio.h>

// Função recursiva para calcular o MDC usando o algoritmo de Euclides
int mdc(int a, int b) {
    // Caso base
    if (b == 0) {
        return a;
    }
    
    // Caso recursivo
    return mdc(b, a % b);
}

int main() {
    int num1 = 48, num2 = 18;
    printf("MDC de %d e %d é: %d\n", num1, num2, mdc(num1, num2));
    return 0;
}
```

**Explicação da Recursão**:
- Caso base: Se b = 0, retorna a
- Caso recursivo: Calcula mdc(b, a % b)

**Execução para mdc(48, 18)**:
```
mdc(48, 18) = mdc(18, 48 % 18) = mdc(18, 12)
            = mdc(12, 18 % 12) = mdc(12, 6)
            = mdc(6, 12 % 6)   = mdc(6, 0)
            = 6 (caso base: b = 0, retorna a)
```

### 🔄 Tipos de Recursão

#### 1️⃣ Recursão Direta

A função chama a si mesma diretamente, como nos exemplos anteriores.

#### 2️⃣ Recursão Indireta

Uma função A chama uma função B, que por sua vez chama a função A, formando um ciclo.

```c
#include <stdio.h>

// Declarações antecipadas
int eh_par(int n);
int eh_impar(int n);

// Função que verifica se um número é par usando recursão indireta
int eh_par(int n) {
    if (n == 0) {
        return 1;  // Zero é par
    }
    return eh_impar(n - 1);
}

// Função que verifica se um número é ímpar usando recursão indireta
int eh_impar(int n) {
    if (n == 0) {
        return 0;  // Zero não é ímpar
    }
    return eh_par(n - 1);
}

int main() {
    int num = 7;
    if (eh_par(num)) {
        printf("%d é par\n", num);
    } else {
        printf("%d é ímpar\n", num);
    }
    return 0;
}
```

#### 3️⃣ Recursão em Cauda

Ocorre quando a chamada recursiva é a última operação na função. Esta forma pode ser otimizada pelo compilador.

```c
#include <stdio.h>

// Versão não otimizada para calcular fatorial
unsigned long fatorial_normal(unsigned int n) {
    if (n == 0 || n == 1) {
        return 1;
    }
    return n * fatorial_normal(n - 1);  // Não é recursão de cauda
}

// Versão com recursão em cauda
unsigned long fatorial_cauda(unsigned int n, unsigned long acumulador) {
    if (n == 0 || n == 1) {
        return acumulador;
    }
    return fatorial_cauda(n - 1, n * acumulador);  // Recursão em cauda
}

// Função wrapper para simplificar o uso
unsigned long fatorial(unsigned int n) {
    return fatorial_cauda(n, 1);
}

int main() {
    unsigned int numero = 5;
    printf("Fatorial de %u = %lu\n", numero, fatorial(numero));
    return 0;
}
```

### 🧮 Aplicações Práticas da Recursão

#### 1️⃣ Torres de Hanói

O problema das Torres de Hanói é um quebra-cabeça clássico que pode ser resolvido elegantemente com recursão.

```c
#include <stdio.h>

void hanoi(int n, char origem, char auxiliar, char destino) {
    if (n == 1) {
        printf("Mova o disco 1 de %c para %c\n", origem, destino);
        return;
    }
    
    hanoi(n - 1, origem, destino, auxiliar);
    printf("Mova o disco %d de %c para %c\n", n, origem, destino);
    hanoi(n - 1, auxiliar, origem, destino);
}

int main() {
    int n = 3;  // Número de discos
    printf("Solução para Torres de Hanói com %d discos:\n", n);
    hanoi(n, 'A', 'B', 'C');
    return 0;
}
```

#### 2️⃣ Busca Binária Recursiva

Implementação recursiva do algoritmo de busca binária.

```c
#include <stdio.h>

// Função recursiva para busca binária
int busca_binaria(int arr[], int esquerda, int direita, int alvo) {
    // Caso base: elemento não encontrado
    if (esquerda > direita) {
        return -1;
    }
    
    int meio = esquerda + (direita - esquerda) / 2;
    
    // Caso base: elemento encontrado
    if (arr[meio] == alvo) {
        return meio;
    }
    
    // Caso recursivo
    if (arr[meio] > alvo) {
        return busca_binaria(arr, esquerda, meio - 1, alvo);
    } else {
        return busca_binaria(arr, meio + 1, direita, alvo);
    }
}

int main() {
    int arr[] = {2, 5, 8, 12, 16, 23, 38, 45, 56, 72, 91};
    int n = sizeof(arr) / sizeof(arr[0]);
    int alvo = 23;
    
    int resultado = busca_binaria(arr, 0, n - 1, alvo);
    
    if (resultado == -1) {
        printf("Elemento %d não encontrado no array\n", alvo);
    } else {
        printf("Elemento %d encontrado na posição %d\n", alvo, resultado);
    }
    
    return 0;
}
```

#### 3️⃣ Percurso em Estruturas de Dados

Recursão é frequentemente usada para percorrer estruturas de dados complexas, como árvores.

```c
#include <stdio.h>
#include <stdlib.h>

// Definição de uma estrutura de nó de árvore binária
typedef struct No {
    int valor;
    struct No* esquerda;
    struct No* direita;
} No;

// Função para criar um novo nó
No* criar_no(int valor) {
    No* novo = (No*)malloc(sizeof(No));
    if (novo) {
        novo->valor = valor;
        novo->esquerda = NULL;
        novo->direita = NULL;
    }
    return novo;
}

// Percurso em ordem (in-order traversal)
void percurso_em_ordem(No* raiz) {
    if (raiz != NULL) {
        percurso_em_ordem(raiz->esquerda);  // Visita subárvore esquerda
        printf("%d ", raiz->valor);         // Visita raiz
        percurso_em_ordem(raiz->direita);   // Visita subárvore direita
    }
}

// Percurso pré-ordem (pre-order traversal)
void percurso_pre_ordem(No* raiz) {
    if (raiz != NULL) {
        printf("%d ", raiz->valor);         // Visita raiz
        percurso_pre_ordem(raiz->esquerda); // Visita subárvore esquerda
        percurso_pre_ordem(raiz->direita);  // Visita subárvore direita
    }
}

// Percurso pós-ordem (post-order traversal)
void percurso_pos_ordem(No* raiz) {
    if (raiz != NULL) {
        percurso_pos_ordem(raiz->esquerda); // Visita subárvore esquerda
        percurso_pos_ordem(raiz->direita);  // Visita subárvore direita
        printf("%d ", raiz->valor);         // Visita raiz
    }
}

// Função para liberar a memória da árvore
void liberar_arvore(No* raiz) {
    if (raiz != NULL) {
        liberar_arvore(raiz->esquerda);
        liberar_arvore(raiz->direita);
        free(raiz);
    }
}

int main() {
    // Criando uma árvore de exemplo
    No* raiz = criar_no(10);
    raiz->esquerda = criar_no(5);
    raiz->direita = criar_no(15);
    raiz->esquerda->esquerda = criar_no(3);
    raiz->esquerda->direita = criar_no(7);
    raiz->direita->esquerda = criar_no(12);
    raiz->direita->direita = criar_no(18);
    
    printf("Percurso em ordem: ");
    percurso_em_ordem(raiz);
    printf("\n");
    
    printf("Percurso pré-ordem: ");
    percurso_pre_ordem(raiz);
    printf("\n");
    
    printf("Percurso pós-ordem: ");
    percurso_pos_ordem(raiz);
    printf("\n");
    
    // Libera memória
    liberar_arvore(raiz);
    
    return 0;
}
```

### ⚠️ Limitações e Desafios da Recursão

#### 1️⃣ Consumo de Pilha

Cada chamada recursiva consome espaço na pilha (stack) de execução, o que pode levar a um estouro de pilha (stack overflow) para entradas muito grandes.

```c
#include <stdio.h>

// Função propensa a estouro de pilha para entradas grandes
int fibonacci_ineficiente(int n) {
    if (n <= 1) return n;
    return fibonacci_ineficiente(n - 1) + fibonacci_ineficiente(n - 2);
}

// Teste com valor grande
int main() {
    int n = 45;  // Valor relativamente grande
    printf("Calculando fibonacci(%d)...\n", n);
    printf("Resultado: %d\n", fibonacci_ineficiente(n));  // Muito lento!
    return 0;
}
```

#### 2️⃣ Ineficiência em Certos Casos

Em funções como `fibonacci_ineficiente` acima, há muitos cálculos redundantes. Uma solução iterativa ou com memoização seria muito mais eficiente.

#### 3️⃣ Memoização para Otimizar a Recursão

A memoização é uma técnica para armazenar resultados de chamadas anteriores, evitando recálculos.

```c
#include <stdio.h>
#include <stdlib.h>

// Fibonacci com memoização
int fibonacci_memo(int n, int* memo) {
    if (memo[n] != -1) {
        return memo[n];  // Retorna resultado já calculado
    }
    
    if (n <= 1) {
        memo[n] = n;
    } else {
        memo[n] = fibonacci_memo(n - 1, memo) + fibonacci_memo(n - 2, memo);
    }
    
    return memo[n];
}

int fibonacci(int n) {
    if (n < 0) return -1;  // Erro para entrada negativa
    
    // Inicializa array de memoização
    int* memo = (int*)malloc((n + 1) * sizeof(int));
    if (!memo) return -1;  // Erro de alocação
    
    for (int i = 0; i <= n; i++) {
        memo[i] = -1;  // -1 indica valor não calculado
    }
    
    int resultado = fibonacci_memo(n, memo);
    free(memo);
    return resultado;
}

int main() {
    int n = 45;  // Agora é rápido mesmo para valores grandes
    printf("Fibonacci(%d) = %d\n", n, fibonacci(n));
    return 0;
}
```

### 🔄 Conversão de Recursão para Iteração

Muitas funções recursivas podem ser reescritas de forma iterativa, o que geralmente é mais eficiente.

#### 1️⃣ Fatorial Iterativo

```c
#include <stdio.h>

unsigned long fatorial_iterativo(unsigned int n) {
    unsigned long resultado = 1;
    
    for (unsigned int i = 2; i <= n; i++) {
        resultado *= i;
    }
    
    return resultado;
}

int main() {
    unsigned int numero = 5;
    printf("Fatorial de %u = %lu\n", numero, fatorial_iterativo(numero));
    return 0;
}
```

#### 2️⃣ Fibonacci Iterativo

```c
#include <stdio.h>

int fibonacci_iterativo(int n) {
    if (n <= 0) return 0;
    if (n == 1) return 1;
    
    int fib_prev = 0;
    int fib_curr = 1;
    int fib_next;
    
    for (int i = 2; i <= n; i++) {
        fib_next = fib_prev + fib_curr;
        fib_prev = fib_curr;
        fib_curr = fib_next;
    }
    
    return fib_curr;
}

int main() {
    int n = 10;
    printf("Primeiros %d números da sequência de Fibonacci:\n", n);
    for (int i = 0; i < n; i++) {
        printf("%d ", fibonacci_iterativo(i));
    }
    printf("\n");
    return 0;
}
```

### 🧠 Boas Práticas para Recursão

1. **Sempre tenha um caso base claro** para evitar recursão infinita
2. **Verifique os limites de entrada** para prevenir comportamentos inesperados
3. **Considere a profundidade da recursão** para evitar estouro de pilha
4. **Use memoização** para funções que recalculam os mesmos valores
5. **Considere alternativas iterativas** para casos onde a recursão é ineficiente
6. **Utilize recursão em cauda** quando possível, pois pode ser otimizada
7. **Documente claramente** o funcionamento da recursão para facilitar a manutenção

### 📝 Exemplo Prático: Sistema de Arquivos

Vamos implementar uma função recursiva para listar arquivos em um diretório e seus subdiretórios.

```c
#include <stdio.h>
#include <dirent.h>
#include <string.h>
#include <sys/stat.h>

// Função recursiva para listar arquivos em um diretório e subdiretórios
void listar_arquivos(const char* caminho, int nivel) {
    DIR* dir;
    struct dirent* entrada;
    struct stat info;
    char caminho_completo[1024];
    
    // Abre o diretório
    dir = opendir(caminho);
    if (dir == NULL) {
        printf("Não foi possível abrir o diretório: %s\n", caminho);
        return;
    }
    
    // Percorre as entradas do diretório
    while ((entrada = readdir(dir)) != NULL) {
        // Ignora os diretórios "." e ".."
        if (strcmp(entrada->d_name, ".") == 0 || strcmp(entrada->d_name, "..") == 0) {
            continue;
        }
        
        // Constrói o caminho completo
        snprintf(caminho_completo, sizeof(caminho_completo), "%s/%s", caminho, entrada->d_name);
        
        // Obtém informações sobre o arquivo
        if (stat(caminho_completo, &info) != 0) {
            printf("Erro ao obter informações: %s\n", caminho_completo);
            continue;
        }
        
        // Imprime indentação para mostrar a hierarquia
        for (int i = 0; i < nivel; i++) {
            printf("  ");
        }
        
        // Imprime o nome do arquivo/diretório
        printf("|-- %s\n", entrada->d_name);
        
        // Se for um diretório, chama recursivamente
        if (S_ISDIR(info.st_mode)) {
            listar_arquivos(caminho_completo, nivel + 1);
        }
    }
    
    closedir(dir);
}

int main() {
    const char* diretorio = ".";  // Diretório atual
    printf("Listando arquivos em: %s\n", diretorio);
    listar_arquivos(diretorio, 0);
    return 0;
}
```

**Observação**: Este código funciona em sistemas Unix/Linux. Para Windows, seria necessário usar as APIs específicas do Windows.

### 🧮 Resumo

A recursão é uma técnica poderosa na programação em C, especialmente útil para:

1. Problemas que podem ser divididos em subproblemas idênticos, porém menores
2. Algoritmos que seguem naturalmente uma abordagem recursiva, como Torres de Hanói
3. Manipulação de estruturas de dados hierárquicas, como árvores e sistemas de arquivos

Apesar de suas vantagens em clareza e elegância, é importante estar ciente das limitações de desempenho e do risco de estouro de pilha.

```
┌─────────────────────┬─────────────────────────────────────────┐
│ Prós da Recursão    │ Contras da Recursão                     │
├─────────────────────┼─────────────────────────────────────────┤
│ - Código elegante   │ - Risco de estouro de pilha             │
│ - Mais legível para │ - Overhead de chamadas de função        │
│   certos problemas  │ - Pode ser ineficiente (recálculos)     │
│ - Natural para      │ - Maior consumo de memória              │
│   estruturas        │ - Mais difícil de depurar               │
│   hierárquicas      │                                         │
└─────────────────────┴─────────────────────────────────────────┘
```

---

[🔙 Voltar ao índice principal](../README.md)

<img width=100% src="https://capsule-render.vercel.app/api?type=waving&color=A8B9CC&height=120&section=footer"/> 