<img width=100% src="https://capsule-render.vercel.app/api?type=waving&color=A8B9CC&height=120&section=header"/>

# 📊 Estruturas de Dados e Algoritmos em C

Neste guia, vamos explorar as principais estruturas de dados e algoritmos de ordenação e busca em C.

## 🧠 O que são Estruturas de Dados?

Estruturas de dados são formas de organizar, gerenciar e armazenar dados de maneira eficiente para que possam ser utilizados de forma apropriada durante a execução de um programa. Elas são fundamentais para a construção de algoritmos eficientes e para a resolução de problemas complexos em programação.

### Por que estudar Estruturas de Dados?
- Permitem manipular grandes volumes de dados de forma eficiente
- Facilitam a implementação de algoritmos de busca, ordenação e processamento
- São a base para o desenvolvimento de sistemas, bancos de dados, compiladores, jogos, inteligência artificial, etc.

### Tipos de Estruturas de Dados
As principais estruturas de dados estudadas em C são:

- **Vetores (Arrays):** Estrutura sequencial de tamanho fixo, ideal para armazenar elementos do mesmo tipo.
- **Listas:** Estruturas dinâmicas que permitem inserção e remoção de elementos em qualquer posição. Podem ser listas simplesmente encadeadas, duplamente encadeadas, circulares, etc.
- **Pilhas (Stack):** Estrutura do tipo LIFO (Last In, First Out), onde o último elemento inserido é o primeiro a ser removido. Muito usada em algoritmos de recursão, controle de chamadas de funções, desfazer/refazer operações, etc.
- **Filas (Queue):** Estrutura do tipo FIFO (First In, First Out), onde o primeiro elemento inserido é o primeiro a ser removido. Utilizada em sistemas de impressão, filas de atendimento, buffers, etc.
- **Árvores:** Estruturas hierárquicas, como árvores binárias, AVL, B-trees, muito usadas em bancos de dados, sistemas de arquivos e algoritmos de busca.
- **Tabelas Hash:** Estruturas que permitem acesso rápido a dados por meio de funções de dispersão (hash), ideais para buscas rápidas e armazenamento de grandes volumes de dados.
- **Grafos:** Estruturas que representam relações entre objetos, muito usadas em redes, mapas, rotas, redes sociais, etc.

### Como escolher a estrutura de dados?
A escolha depende do problema a ser resolvido, do tipo de operação mais frequente (busca, inserção, remoção, ordenação) e das restrições de tempo e memória.

### Aplicações práticas
- **Pilhas:** Controle de chamadas de funções, algoritmos de backtracking, editores de texto (desfazer/refazer)
- **Filas:** Impressoras, sistemas de atendimento, buffers de comunicação
- **Listas:** Manipulação dinâmica de dados, implementação de outras estruturas
- **Árvores:** Índices de banco de dados, compressão de dados, inteligência artificial
- **Tabelas Hash:** Dicionários, caches, sistemas de autenticação
- **Grafos:** Mapas, redes de computadores, algoritmos de navegação

---

## 🏗️ Estruturas de Dados

### Pilhas (Stack)

**O que é?**

Uma pilha é uma estrutura de dados linear do tipo LIFO (Last In, First Out), ou seja, o último elemento inserido é o primeiro a ser removido. Imagine uma pilha de pratos: você só pode retirar o prato que está no topo.

**Principais operações:**
- `empilhar` (push): adiciona um elemento ao topo
- `desempilhar` (pop): remove o elemento do topo
- `topo` (peek): consulta o elemento do topo sem removê-lo

**Aplicações práticas:**
- Controle de chamadas de funções (pilha de execução)
- Algoritmos de recursão
- Desfazer/refazer em editores de texto
- Conversão de expressões (infixa, pós-fixa)
- Algoritmos de backtracking (ex: resolver labirintos)

**Vantagens:**
- Simples de implementar
- Ótima para problemas que exigem reversão de operações

**Desvantagens:**
- Acesso restrito (apenas topo)
- Não é eficiente para busca de elementos arbitrários

**Curiosidade:**
- A pilha é usada internamente pelo processador para armazenar o contexto de funções e variáveis locais.

```c
#define MAX 100

typedef struct {
    int dados[MAX];
    int topo;
} Pilha;

void inicializarPilha(Pilha *p) {
    p->topo = -1;
}

void empilhar(Pilha *p, int valor) {
    if (p->topo < MAX - 1) {
        p->topo++;
        p->dados[p->topo] = valor;
    }
}

int desempilhar(Pilha *p) {
    if (p->topo >= 0) {
        int valor = p->dados[p->topo];
        p->topo--;
        return valor;
    }
    return -1;
}
```

### Filas (Queue)

**O que é?**

Uma fila é uma estrutura de dados linear do tipo FIFO (First In, First Out), ou seja, o primeiro elemento inserido é o primeiro a ser removido. Imagine uma fila de pessoas no banco: quem chega primeiro é atendido primeiro.

**Principais operações:**
- `enfileirar` (enqueue): adiciona um elemento ao final
- `desenfileirar` (dequeue): remove o elemento do início
- `frente` (front): consulta o elemento do início sem removê-lo

**Aplicações práticas:**
- Filas de impressão
- Sistemas de atendimento
- Buffers de comunicação (ex: streaming)
- Simulação de processos (ex: filas de supermercado)

**Vantagens:**
- Simples de implementar
- Garante ordem de processamento

**Desvantagens:**
- Acesso restrito (apenas início e fim)
- Não é eficiente para busca de elementos arbitrários

**Curiosidade:**
- Existem variações como fila circular, fila de prioridade e deque (fila dupla).

```c
#define MAX 100

typedef struct {
    int dados[MAX];
    int inicio;
    int fim;
    int tamanho;
} Fila;

void inicializarFila(Fila *f) {
    f->inicio = 0;
    f->fim = -1;
    f->tamanho = 0;
}

void enfileirar(Fila *f, int valor) {
    if (f->tamanho < MAX) {
        f->fim = (f->fim + 1) % MAX;
        f->dados[f->fim] = valor;
        f->tamanho++;
    }
}

int desenfileirar(Fila *f) {
    if (f->tamanho > 0) {
        int valor = f->dados[f->inicio];
        f->inicio = (f->inicio + 1) % MAX;
        f->tamanho--;
        return valor;
    }
    return -1;
}
```

## 🔍 Algoritmos de Busca

### Busca Linear

**O que é?**

A busca linear (ou sequencial) percorre todos os elementos de um vetor até encontrar o valor desejado ou chegar ao final. É simples, mas pode ser lenta para grandes volumes de dados.

**Quando usar?**
- Vetores pequenos
- Dados não ordenados

**Vantagens:**
- Simplicidade
- Não exige ordenação

**Desvantagens:**
- Ineficiente para grandes volumes (complexidade O(n))

### Busca Binária

**O que é?**

A busca binária só pode ser usada em vetores ordenados. Ela divide o vetor ao meio a cada passo, reduzindo drasticamente o número de comparações.

**Quando usar?**
- Vetores grandes
- Dados ordenados

**Vantagens:**
- Muito eficiente (complexidade O(log n))

**Desvantagens:**
- Só funciona em dados ordenados
- Mais complexa de implementar

**Curiosidade:**
- A busca binária é a base de algoritmos de busca em bancos de dados e sistemas de arquivos.

```c
int buscaLinear(int vetor[], int tamanho, int valor) {
    for (int i = 0; i < tamanho; i++) {
        if (vetor[i] == valor) {
            return i;
        }
    }
    return -1;
}

int buscaBinaria(int vetor[], int inicio, int fim, int valor) {
    if (fim >= inicio) {
        int meio = inicio + (fim - inicio) / 2;
        
        if (vetor[meio] == valor)
            return meio;
            
        if (vetor[meio] > valor)
            return buscaBinaria(vetor, inicio, meio - 1, valor);
            
        return buscaBinaria(vetor, meio + 1, fim, valor);
    }
    return -1;
}
```

## 📊 Algoritmos de Ordenação

Ordenar dados é uma tarefa fundamental em programação. Existem vários algoritmos, cada um com características próprias.

### Bubble Sort

**Como funciona?**
Compara pares de elementos adjacentes e os troca de lugar se estiverem fora de ordem. Repete o processo até que o vetor esteja ordenado.

**Vantagens:**
- Fácil de entender e implementar

**Desvantagens:**
- Muito ineficiente para grandes volumes (O(n²))

**Quando usar?**
- Pequenos conjuntos de dados
- Situações didáticas

```c
void bubbleSort(int vetor[], int tamanho) {
    for (int i = 0; i < tamanho - 1; i++) {
        for (int j = 0; j < tamanho - i - 1; j++) {
            if (vetor[j] > vetor[j + 1]) {
                int temp = vetor[j];
                vetor[j] = vetor[j + 1];
                vetor[j + 1] = temp;
            }
        }
    }
}
```

### Selection Sort

**Como funciona?**
Procura o menor elemento e o coloca na primeira posição, depois o segundo menor na segunda posição, e assim por diante.

**Vantagens:**
- Simples
- Poucas trocas

**Desvantagens:**
- Ineficiente para grandes volumes (O(n²))

```c
void selectionSort(int vetor[], int tamanho) {
    for (int i = 0; i < tamanho - 1; i++) {
        int min_idx = i;
        for (int j = i + 1; j < tamanho; j++) {
            if (vetor[j] < vetor[min_idx])
                min_idx = j;
        }
        int temp = vetor[min_idx];
        vetor[min_idx] = vetor[i];
        vetor[i] = temp;
    }
}
```

### Insertion Sort

**Como funciona?**
Constrói o vetor ordenado um elemento por vez, inserindo cada novo elemento na posição correta.

**Vantagens:**
- Bom para vetores pequenos ou quase ordenados

**Desvantagens:**
- Ineficiente para grandes volumes (O(n²))

```c
void insertionSort(int vetor[], int tamanho) {
    for (int i = 1; i < tamanho; i++) {
        int chave = vetor[i];
        int j = i - 1;
        
        while (j >= 0 && vetor[j] > chave) {
            vetor[j + 1] = vetor[j];
            j--;
        }
        vetor[j + 1] = chave;
    }
}
```

### Quick Sort

**Como funciona?**
Escolhe um pivô, separa os elementos menores à esquerda e maiores à direita, e aplica o processo recursivamente.

**Vantagens:**
- Muito eficiente na prática (O(n log n) em média)

**Desvantagens:**
- Pior caso O(n²) (mas raro)
- Não é estável

```c
int particionar(int vetor[], int baixo, int alto) {
    int pivo = vetor[alto];
    int i = (baixo - 1);
    
    for (int j = baixo; j <= alto - 1; j++) {
        if (vetor[j] < pivo) {
            i++;
            int temp = vetor[i];
            vetor[i] = vetor[j];
            vetor[j] = temp;
        }
    }
    int temp = vetor[i + 1];
    vetor[i + 1] = vetor[alto];
    vetor[alto] = temp;
    return (i + 1);
}

void quickSort(int vetor[], int baixo, int alto) {
    if (baixo < alto) {
        int pi = particionar(vetor, baixo, alto);
        quickSort(vetor, baixo, pi - 1);
        quickSort(vetor, pi + 1, alto);
    }
}
```

### Shell Sort

**Como funciona?**
Generaliza o insertion sort, permitindo comparações e trocas entre elementos distantes. Reduz o intervalo gradualmente até ordenar todo o vetor.

**Vantagens:**
- Mais eficiente que insertion/bubble/selection para vetores médios

**Desvantagens:**
- Complexidade depende da sequência de gaps

```c
void shellSort(int vetor[], int tamanho) {
    for (int gap = tamanho/2; gap > 0; gap /= 2) {
        for (int i = gap; i < tamanho; i++) {
            int temp = vetor[i];
            int j;
            for (j = i; j >= gap && vetor[j - gap] > temp; j -= gap) {
                vetor[j] = vetor[j - gap];
            }
            vetor[j] = temp;
        }
    }
}
```

### Merge Sort

**Como funciona?**
Divide o vetor em duas partes, ordena cada uma recursivamente e depois intercala (merge) as duas partes ordenadas.

**Vantagens:**
- Sempre O(n log n)
- Estável

**Desvantagens:**
- Usa memória extra

**Curiosidade:**
- Merge sort é muito usado em bancos de dados e sistemas que precisam ordenar grandes volumes de dados em disco.

```c
void merge(int vetor[], int esquerda, int meio, int direita) {
    int i, j, k;
    int n1 = meio - esquerda + 1;
    int n2 = direita - meio;
    
    int L[n1], R[n2];
    
    for (i = 0; i < n1; i++)
        L[i] = vetor[esquerda + i];
    for (j = 0; j < n2; j++)
        R[j] = vetor[meio + 1 + j];
        
    i = 0;
    j = 0;
    k = esquerda;
    
    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) {
            vetor[k] = L[i];
            i++;
        } else {
            vetor[k] = R[j];
            j++;
        }
        k++;
    }
    
    while (i < n1) {
        vetor[k] = L[i];
        i++;
        k++;
    }
    
    while (j < n2) {
        vetor[k] = R[j];
        j++;
        k++;
    }
}

void mergeSort(int vetor[], int esquerda, int direita) {
    if (esquerda < direita) {
        int meio = esquerda + (direita - esquerda) / 2;
        mergeSort(vetor, esquerda, meio);
        mergeSort(vetor, meio + 1, direita);
        merge(vetor, esquerda, meio, direita);
    }
}
```

## 📌 Complexidade dos Algoritmos

### Busca
- Busca Linear: O(n)
- Busca Binária: O(log n)

### Ordenação
- Bubble Sort: O(n²)
- Selection Sort: O(n²)
- Insertion Sort: O(n²)
- Quick Sort: O(n log n) médio, O(n²) pior caso
- Shell Sort: O(n log n)
- Merge Sort: O(n log n)

## 🎯 Exemplos Práticos

### Exemplo 1: Sistema de Gerenciamento de Tarefas
```c
typedef struct {
    char descricao[100];
    int prioridade;
    int concluida;
} Tarefa;

typedef struct {
    Tarefa tarefas[100];
    int quantidade;
} ListaTarefas;

void adicionarTarefa(ListaTarefas *lista, Tarefa tarefa) {
    if (lista->quantidade < 100) {
        lista->tarefas[lista->quantidade] = tarefa;
        lista->quantidade++;
    }
}

void ordenarPorPrioridade(ListaTarefas *lista) {
    for (int i = 0; i < lista->quantidade - 1; i++) {
        for (int j = 0; j < lista->quantidade - i - 1; j++) {
            if (lista->tarefas[j].prioridade < lista->tarefas[j + 1].prioridade) {
                Tarefa temp = lista->tarefas[j];
                lista->tarefas[j] = lista->tarefas[j + 1];
                lista->tarefas[j + 1] = temp;
            }
        }
    }
}
```

## ⚠️ Considerações Importantes

1. Escolha o algoritmo adequado para cada situação
2. Considere a complexidade do algoritmo
3. Teste com diferentes tamanhos de dados
4. Otimize quando necessário
5. Documente o código

---

# 📋 Busca e Operações com Listas Sequenciais

Listas sequenciais são estruturas de dados lineares que armazenam elementos em posições contíguas de memória, geralmente implementadas como arrays. São ideais para situações em que o número máximo de elementos é conhecido ou não muda com frequência.

## 🧭 Navegação e Conceitos

- **Lista Sequencial**: Estrutura baseada em array, com acesso direto por índice.
- **Navegação**: Feita por índices (ex: `lista[0]`, `lista[1]`, ...).
- **Tamanho**: Pode ser fixo (array estático) ou dinâmico (alocação dinâmica).

## 🗂️ Operações Básicas

1. **Inserção**
   - Início
   - Fim
   - Posição específica
2. **Remoção**
   - Início
   - Fim
   - Posição específica
3. **Busca**
   - Sequencial (linear)

## 📝 Exemplo Prático em C

Vamos implementar um menu para manipular uma lista sequencial de pessoas (nome e RG):

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX 100

// Estrutura para pessoa
typedef struct {
    char nome[50];
    int rg;
} Pessoa;

// Função para limpar a tela (Windows/Linux)
void limparTela() {
#ifdef _WIN32
    system("cls");
#else
    system("clear");
#endif
}

// Imprime a lista sequencial
void imprimeSequencial(Pessoa lista[], int tamanho) {
    printf("\nLista:\n");
    for (int i = 0; i < tamanho; i++) {
        printf("%d - %s, %d\n", i, lista[i].nome, lista[i].rg);
    }
}

// Inserção no início
void inserirInicio(Pessoa lista[], int *tamanho, char nome[], int rg) {
    if (*tamanho >= MAX) {
        printf("Lista cheia!\n");
        return;
    }
    for (int i = *tamanho; i > 0; i--) {
        lista[i] = lista[i-1];
    }
    strcpy(lista[0].nome, nome);
    lista[0].rg = rg;
    (*tamanho)++;
}

// Inserção no fim
void inserirFim(Pessoa lista[], int *tamanho, char nome[], int rg) {
    if (*tamanho >= MAX) {
        printf("Lista cheia!\n");
        return;
    }
    strcpy(lista[*tamanho].nome, nome);
    lista[*tamanho].rg = rg;
    (*tamanho)++;
}

// Inserção em posição específica
void inserirPosicao(Pessoa lista[], int *tamanho, char nome[], int rg, int pos) {
    if (*tamanho >= MAX || pos < 0 || pos > *tamanho) {
        printf("Posição inválida ou lista cheia!\n");
        return;
    }
    for (int i = *tamanho; i > pos; i--) {
        lista[i] = lista[i-1];
    }
    strcpy(lista[pos].nome, nome);
    lista[pos].rg = rg;
    (*tamanho)++;
}

// Remoção do início
void removerInicio(Pessoa lista[], int *tamanho) {
    if (*tamanho == 0) {
        printf("Lista vazia!\n");
        return;
    }
    for (int i = 0; i < *tamanho-1; i++) {
        lista[i] = lista[i+1];
    }
    (*tamanho)--;
}

// Remoção do fim
void removerFim(Pessoa lista[], int *tamanho) {
    if (*tamanho == 0) {
        printf("Lista vazia!\n");
        return;
    }
    (*tamanho)--;
}

// Remoção em posição específica
void removerPosicao(Pessoa lista[], int *tamanho, int pos) {
    if (*tamanho == 0 || pos < 0 || pos >= *tamanho) {
        printf("Posição inválida ou lista vazia!\n");
        return;
    }
    for (int i = pos; i < *tamanho-1; i++) {
        lista[i] = lista[i+1];
    }
    (*tamanho)--;
}

// Busca sequencial por RG
int buscarPorRG(Pessoa lista[], int tamanho, int rg) {
    for (int i = 0; i < tamanho; i++) {
        if (lista[i].rg == rg) {
            return i;
        }
    }
    return -1;
}

int main() {
    Pessoa lista[MAX];
    int tamanho = 0;
    int opcao;
    do {
        printf("\n=== Menu Lista Sequencial ===\n");
        printf("1. Inserir no início\n");
        printf("2. Inserir no fim\n");
        printf("3. Inserir em posição\n");
        printf("4. Remover do início\n");
        printf("5. Remover do fim\n");
        printf("6. Remover em posição\n");
        printf("7. Buscar por RG\n");
        printf("8. Imprimir lista\n");
        printf("9. Sair\n");
        printf("Escolha uma opção: ");
        scanf("%d", &opcao);
        limparTela();
        char nome[50];
        int rg, pos, idx;
        switch(opcao) {
            case 1:
                printf("Nome: "); scanf("%s", nome);
                printf("RG: "); scanf("%d", &rg);
                inserirInicio(lista, &tamanho, nome, rg);
                break;
            case 2:
                printf("Nome: "); scanf("%s", nome);
                printf("RG: "); scanf("%d", &rg);
                inserirFim(lista, &tamanho, nome, rg);
                break;
            case 3:
                printf("Posição: "); scanf("%d", &pos);
                printf("Nome: "); scanf("%s", nome);
                printf("RG: "); scanf("%d", &rg);
                inserirPosicao(lista, &tamanho, nome, rg, pos);
                break;
            case 4:
                removerInicio(lista, &tamanho);
                break;
            case 5:
                removerFim(lista, &tamanho);
                break;
            case 6:
                printf("Posição: "); scanf("%d", &pos);
                removerPosicao(lista, &tamanho, pos);
                break;
            case 7:
                printf("RG: "); scanf("%d", &rg);
                idx = buscarPorRG(lista, tamanho, rg);
                if (idx != -1) {
                    printf("Encontrado na posição %d: %s\n", idx, lista[idx].nome);
                } else {
                    printf("RG não encontrado!\n");
                }
                break;
            case 8:
                imprimeSequencial(lista, tamanho);
                break;
            case 9:
                printf("Saindo...\n");
                break;
            default:
                printf("Opção inválida!\n");
        }
    } while(opcao != 9);
    return 0;
}
```

## 🔎 Resumo das Operações

| Operação                | Complexidade |
|------------------------|--------------|
| Inserção no início     | O(n)         |
| Inserção no fim        | O(1)         |
| Inserção em posição    | O(n)         |
| Remoção do início      | O(n)         |
| Remoção do fim         | O(1)         |
| Remoção em posição     | O(n)         |
| Busca sequencial       | O(n)         |

## 🧠 Dicas e Boas Práticas

- Sempre verifique se a lista está cheia ou vazia antes de inserir/remover.
- Prefira arrays dinâmicos (`malloc`/`realloc`) para listas que crescem muito.
- Use funções para modularizar o código e evitar repetição.
- Para buscas frequentes, considere outras estruturas (listas encadeadas, árvores, etc).

---

[🔙 Voltar ao índice principal](../README.md)

<img width=100% src="https://capsule-render.vercel.app/api?type=waving&color=A8B9CC&height=120&section=footer"/> 