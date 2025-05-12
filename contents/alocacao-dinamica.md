<img width=100% src="https://capsule-render.vercel.app/api?type=waving&color=A8B9CC&height=120&section=header"/>

# 📚 Alocação Dinâmica de Memória

## 📋 Gerenciando Memória em C

A alocação dinâmica de memória é um recurso essencial na linguagem C que permite aos programadores gerenciar a memória de forma flexível durante a execução do programa, criando e liberando espaço conforme necessário.

### 🧠 Memória em Programas C

Quando um programa C é executado, ele divide sua memória em várias regiões:

1. **Segmento de Código**: Armazena o código executável do programa
2. **Segmento de Dados**: Contém variáveis globais e estáticas
3. **Stack (Pilha)**: Gerencia funções e variáveis locais
4. **Heap**: Área para alocação dinâmica de memória

```
┌────────────────┐
│ Segmento de    │
│ Código         │
├────────────────┤
│ Segmento de    │
│ Dados          │
├────────────────┤
│                │
│ Heap           │ ← Cresce para baixo
│                │
│ (memória livre)│
│                │
│ Stack          │ ← Cresce para cima
│                │
└────────────────┘
```

### 🔄 Memória Estática vs. Dinâmica

**Memória Estática**:
- Alocada durante a compilação
- Tamanho fixo e conhecido em tempo de compilação
- Variáveis globais, estáticas e arrays de tamanho fixo

**Memória Dinâmica**:
- Alocada durante a execução
- Tamanho pode ser determinado em tempo de execução
- Usada quando não se conhece antecipadamente quanto espaço será necessário

### 🛠️ Funções para Alocação Dinâmica

#### 1️⃣ `malloc()` - Memory Allocation

A função `malloc()` aloca um bloco de memória do tamanho especificado e retorna um ponteiro para o início do bloco.

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int *p;
    
    // Aloca espaço para um inteiro
    p = (int*) malloc(sizeof(int));
    
    if (p == NULL) {
        printf("Erro: Memória insuficiente!\n");
        return 1;
    }
    
    *p = 10;
    printf("Valor: %d\n", *p);
    
    free(p);  // Libera a memória
    
    return 0;
}
```

**Pontos importantes**:
- Retorna `NULL` se não conseguir alocar a memória solicitada
- A memória alocada não é inicializada (contém "lixo")
- É necessário fazer casting do tipo retornado (void*) para o tipo desejado

#### 2️⃣ `calloc()` - Cleared Allocation

A função `calloc()` aloca memória para um array de elementos, inicializando todos os bits com zero.

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int *p;
    int i, n = 5;
    
    // Aloca espaço para 5 inteiros, inicializados com zero
    p = (int*) calloc(n, sizeof(int));
    
    if (p == NULL) {
        printf("Erro: Memória insuficiente!\n");
        return 1;
    }
    
    printf("Valores iniciais: ");
    for (i = 0; i < n; i++) {
        printf("%d ", p[i]);  // Imprime 0 0 0 0 0
    }
    printf("\n");
    
    // Preenche o array
    for (i = 0; i < n; i++) {
        p[i] = i * 10;
    }
    
    printf("Valores após atribuição: ");
    for (i = 0; i < n; i++) {
        printf("%d ", p[i]);  // Imprime 0 10 20 30 40
    }
    printf("\n");
    
    free(p);  // Libera a memória
    
    return 0;
}
```

**Diferenças em relação ao `malloc()`**:
- Recebe dois parâmetros: número de elementos e tamanho de cada elemento
- Inicializa a memória com zeros
- Equivalente a `malloc(n * sizeof(tipo))` seguido de uma inicialização

#### 3️⃣ `realloc()` - Reallocation

A função `realloc()` redimensiona um bloco de memória previamente alocado.

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int *p;
    int i, n = 5;
    
    // Aloca espaço inicial para 5 inteiros
    p = (int*) malloc(n * sizeof(int));
    
    if (p == NULL) {
        printf("Erro: Memória insuficiente!\n");
        return 1;
    }
    
    // Preenche o array inicial
    for (i = 0; i < n; i++) {
        p[i] = i * 10;
    }
    
    printf("Array inicial: ");
    for (i = 0; i < n; i++) {
        printf("%d ", p[i]);  // Imprime 0 10 20 30 40
    }
    printf("\n");
    
    // Redimensiona para 10 inteiros
    n = 10;
    p = (int*) realloc(p, n * sizeof(int));
    
    if (p == NULL) {
        printf("Erro: Memória insuficiente para realocar!\n");
        return 1;
    }
    
    // Preenche os novos elementos
    for (i = 5; i < n; i++) {
        p[i] = i * 10;
    }
    
    printf("Array redimensionado: ");
    for (i = 0; i < n; i++) {
        printf("%d ", p[i]);  // Imprime 0 10 20 30 40 50 60 70 80 90
    }
    printf("\n");
    
    free(p);  // Libera a memória
    
    return 0;
}
```

**Comportamento do `realloc()`**:
- Preserva o conteúdo original até o menor dos tamanhos novo/antigo
- Pode mover o bloco para um novo local na memória
- Pode falhar, retornando NULL (o bloco original permanece válido)
- Se o ponteiro original for NULL, atua como `malloc()`
- Se o novo tamanho for zero, atua como `free()`

#### 4️⃣ `free()` - Liberando Memória

A função `free()` libera um bloco de memória previamente alocado.

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int *p = (int*) malloc(sizeof(int));
    
    if (p == NULL) {
        printf("Erro: Memória insuficiente!\n");
        return 1;
    }
    
    *p = 10;
    printf("Valor: %d\n", *p);
    
    free(p);  // Libera a memória
    p = NULL; // Boa prática: evita ponteiro pendurado
    
    return 0;
}
```

**Pontos importantes**:
- Só deve ser chamada com ponteiros retornados por `malloc()`, `calloc()` ou `realloc()`
- Não deve ser chamada mais de uma vez para o mesmo ponteiro
- Não altera o valor do ponteiro, que continuará apontando para o mesmo endereço
- É boa prática atribuir NULL ao ponteiro após liberá-lo

### 📊 Alocando Arrays Dinamicamente

#### 1️⃣ Arrays Unidimensionais

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int *array;
    int tamanho, i;
    
    printf("Informe o tamanho do array: ");
    scanf("%d", &tamanho);
    
    // Aloca memória para o array
    array = (int*) malloc(tamanho * sizeof(int));
    
    if (array == NULL) {
        printf("Erro: Memória insuficiente!\n");
        return 1;
    }
    
    // Preenche o array
    for (i = 0; i < tamanho; i++) {
        array[i] = i * 10;
    }
    
    // Exibe o array
    printf("Array: ");
    for (i = 0; i < tamanho; i++) {
        printf("%d ", array[i]);
    }
    printf("\n");
    
    free(array);
    
    return 0;
}
```

#### 2️⃣ Arrays Bidimensionais (Matrizes)

##### Método 1: Array de Ponteiros

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int **matriz;
    int linhas, colunas, i, j;
    
    printf("Informe o número de linhas: ");
    scanf("%d", &linhas);
    printf("Informe o número de colunas: ");
    scanf("%d", &colunas);
    
    // Aloca o array de ponteiros (linhas)
    matriz = (int**) malloc(linhas * sizeof(int*));
    
    if (matriz == NULL) {
        printf("Erro: Memória insuficiente!\n");
        return 1;
    }
    
    // Aloca cada linha (array de colunas)
    for (i = 0; i < linhas; i++) {
        matriz[i] = (int*) malloc(colunas * sizeof(int));
        
        if (matriz[i] == NULL) {
            printf("Erro: Memória insuficiente!\n");
            
            // Libera memória já alocada
            for (j = 0; j < i; j++) {
                free(matriz[j]);
            }
            free(matriz);
            
            return 1;
        }
    }
    
    // Preenche a matriz
    for (i = 0; i < linhas; i++) {
        for (j = 0; j < colunas; j++) {
            matriz[i][j] = i * 10 + j;
        }
    }
    
    // Exibe a matriz
    printf("Matriz %dx%d:\n", linhas, colunas);
    for (i = 0; i < linhas; i++) {
        for (j = 0; j < colunas; j++) {
            printf("%3d ", matriz[i][j]);
        }
        printf("\n");
    }
    
    // Libera a memória
    for (i = 0; i < linhas; i++) {
        free(matriz[i]);
    }
    free(matriz);
    
    return 0;
}
```

##### Método 2: Bloco Contíguo de Memória

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int *matriz;
    int linhas, colunas, i, j;
    
    printf("Informe o número de linhas: ");
    scanf("%d", &linhas);
    printf("Informe o número de colunas: ");
    scanf("%d", &colunas);
    
    // Aloca toda a matriz em um bloco contíguo
    matriz = (int*) malloc(linhas * colunas * sizeof(int));
    
    if (matriz == NULL) {
        printf("Erro: Memória insuficiente!\n");
        return 1;
    }
    
    // Preenche a matriz
    for (i = 0; i < linhas; i++) {
        for (j = 0; j < colunas; j++) {
            // Acessando elementos: matriz[i * colunas + j]
            matriz[i * colunas + j] = i * 10 + j;
        }
    }
    
    // Exibe a matriz
    printf("Matriz %dx%d:\n", linhas, colunas);
    for (i = 0; i < linhas; i++) {
        for (j = 0; j < colunas; j++) {
            printf("%3d ", matriz[i * colunas + j]);
        }
        printf("\n");
    }
    
    // Libera a memória
    free(matriz);
    
    return 0;
}
```

### 🏗️ Alocando Estruturas Dinamicamente

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef struct {
    int id;
    char nome[50];
    float salario;
} Funcionario;

int main() {
    Funcionario *func;
    
    // Aloca memória para um funcionário
    func = (Funcionario*) malloc(sizeof(Funcionario));
    
    if (func == NULL) {
        printf("Erro: Memória insuficiente!\n");
        return 1;
    }
    
    // Preenche os dados
    func->id = 1;
    strcpy(func->nome, "João Silva");
    func->salario = 5000.0;
    
    // Exibe os dados
    printf("ID: %d\n", func->id);
    printf("Nome: %s\n", func->nome);
    printf("Salário: R$ %.2f\n", func->salario);
    
    free(func);
    
    return 0;
}
```

### 🧮 Array de Estruturas Dinâmico

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef struct {
    int id;
    char nome[50];
    float salario;
} Funcionario;

int main() {
    Funcionario *funcionarios;
    int num_func, i;
    
    printf("Informe o número de funcionários: ");
    scanf("%d", &num_func);
    
    // Aloca memória para o array de funcionários
    funcionarios = (Funcionario*) malloc(num_func * sizeof(Funcionario));
    
    if (funcionarios == NULL) {
        printf("Erro: Memória insuficiente!\n");
        return 1;
    }
    
    // Preenche os dados
    for (i = 0; i < num_func; i++) {
        funcionarios[i].id = i + 1;
        sprintf(funcionarios[i].nome, "Funcionário %d", i + 1);
        funcionarios[i].salario = 2000.0 + i * 500.0;
    }
    
    // Exibe os dados
    printf("\nLista de Funcionários:\n");
    printf("------------------------------------\n");
    for (i = 0; i < num_func; i++) {
        printf("ID: %d\n", funcionarios[i].id);
        printf("Nome: %s\n", funcionarios[i].nome);
        printf("Salário: R$ %.2f\n", funcionarios[i].salario);
        printf("------------------------------------\n");
    }
    
    free(funcionarios);
    
    return 0;
}
```

### ⚠️ Problemas Comuns na Alocação Dinâmica

#### 1️⃣ Vazamento de Memória (Memory Leak)

Ocorre quando a memória alocada não é liberada adequadamente:

```c
#include <stdio.h>
#include <stdlib.h>

void funcao_com_vazamento() {
    int *p = (int*) malloc(sizeof(int));
    
    if (p != NULL) {
        *p = 10;
        // Aqui falta o free(p)
    }
}

int main() {
    int i;
    
    // Chamadas repetidas causarão vazamento de memória
    for (i = 0; i < 1000; i++) {
        funcao_com_vazamento();
    }
    
    return 0;
}
```

#### 2️⃣ Acesso a Memória Liberada

Usar memória após liberá-la pode causar comportamento imprevisível:

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int *p = (int*) malloc(sizeof(int));
    
    if (p != NULL) {
        *p = 10;
        printf("Valor antes de liberar: %d\n", *p);
        
        free(p);
        
        // ERRO: Acesso a memória liberada
        *p = 20;              // Comportamento indefinido
        printf("Valor após liberar: %d\n", *p);  // Comportamento indefinido
    }
    
    return 0;
}
```

#### 3️⃣ Liberar Memória Mais de Uma Vez

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int *p = (int*) malloc(sizeof(int));
    
    if (p != NULL) {
        *p = 10;
        
        free(p);  // Primeira liberação (correta)
        free(p);  // ERRO: Double free (comportamento indefinido)
    }
    
    return 0;
}
```

#### 4️⃣ Estouro de Memória (Buffer Overflow)

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int *p = (int*) malloc(5 * sizeof(int));  // Aloca espaço para 5 inteiros
    
    if (p != NULL) {
        int i;
        
        // ERRO: Escrevendo além do espaço alocado
        for (i = 0; i < 10; i++) {  // Tenta acessar 10 elementos
            p[i] = i;  // Estouro quando i >= 5
        }
        
        free(p);
    }
    
    return 0;
}
```

### 🧪 Verificação de Erros

Sempre verifique se a alocação de memória foi bem-sucedida:

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main() {
    char *texto;
    int tamanho;
    
    printf("Informe o tamanho do texto: ");
    scanf("%d", &tamanho);
    
    // Aloca memória para o texto
    texto = (char*) malloc((tamanho + 1) * sizeof(char));  // +1 para o '\0'
    
    if (texto == NULL) {
        printf("Erro: Falha na alocação de memória!\n");
        return 1;
    }
    
    printf("Digite o texto: ");
    scanf(" %[^\n]", texto);
    
    printf("Texto digitado: %s\n", texto);
    
    free(texto);
    
    return 0;
}
```

### 🧠 Quando Usar Alocação Dinâmica?

**Use alocação dinâmica quando**:

1. O tamanho da estrutura de dados não é conhecido em tempo de compilação
2. O tamanho da estrutura de dados pode mudar durante a execução
3. A estrutura precisa persistir além do escopo da função onde foi criada
4. É necessário evitar o estouro de pilha com grandes estruturas
5. Você precisa compartilhar dados entre diferentes partes do programa

**Não use alocação dinâmica quando**:

1. O tamanho é conhecido e fixo
2. A estrutura é pequena e usada apenas localmente
3. A sobrecarga de gerenciamento de memória supera os benefícios
4. O desempenho é crítico (alocação estática é geralmente mais rápida)

### 📝 Exemplo Prático: Sistema de Gerenciamento de Contatos

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef struct {
    char nome[50];
    char telefone[15];
    char email[50];
} Contato;

// Função para criar um novo contato
Contato* criar_contato() {
    Contato* novo = (Contato*) malloc(sizeof(Contato));
    
    if (novo == NULL) {
        printf("Erro: Falha na alocação de memória!\n");
        exit(1);
    }
    
    // Inicializa com strings vazias
    novo->nome[0] = '\0';
    novo->telefone[0] = '\0';
    novo->email[0] = '\0';
    
    return novo;
}

// Função para preencher os dados de um contato
void preencher_contato(Contato* c) {
    printf("Nome: ");
    scanf(" %[^\n]", c->nome);
    
    printf("Telefone: ");
    scanf(" %[^\n]", c->telefone);
    
    printf("Email: ");
    scanf(" %[^\n]", c->email);
}

// Função para exibir os dados de um contato
void exibir_contato(Contato* c) {
    printf("Nome: %s\n", c->nome);
    printf("Telefone: %s\n", c->telefone);
    printf("Email: %s\n", c->email);
}

// Função para liberar a memória de um contato
void liberar_contato(Contato* c) {
    free(c);
}

// Função para criar uma agenda de contatos
Contato** criar_agenda(int capacidade) {
    Contato** agenda = (Contato**) malloc(capacidade * sizeof(Contato*));
    
    if (agenda == NULL) {
        printf("Erro: Falha na alocação de memória!\n");
        exit(1);
    }
    
    // Inicializa todos os ponteiros com NULL
    for (int i = 0; i < capacidade; i++) {
        agenda[i] = NULL;
    }
    
    return agenda;
}

// Função para adicionar um contato à agenda
void adicionar_contato(Contato** agenda, int posicao, Contato* c) {
    if (agenda[posicao] != NULL) {
        liberar_contato(agenda[posicao]);  // Libera contato existente
    }
    
    agenda[posicao] = c;
}

// Função para liberar a agenda
void liberar_agenda(Contato** agenda, int capacidade) {
    for (int i = 0; i < capacidade; i++) {
        if (agenda[i] != NULL) {
            liberar_contato(agenda[i]);
        }
    }
    
    free(agenda);
}

int main() {
    int capacidade = 3;
    int opcao, posicao;
    
    // Cria a agenda
    Contato** agenda = criar_agenda(capacidade);
    
    do {
        printf("\n===== MENU =====\n");
        printf("1. Adicionar contato\n");
        printf("2. Exibir contato\n");
        printf("3. Aumentar capacidade\n");
        printf("4. Sair\n");
        printf("Opção: ");
        scanf("%d", &opcao);
        
        switch (opcao) {
            case 1:  // Adicionar contato
                printf("Posição (0-%d): ", capacidade - 1);
                scanf("%d", &posicao);
                
                if (posicao >= 0 && posicao < capacidade) {
                    Contato* c = criar_contato();
                    preencher_contato(c);
                    adicionar_contato(agenda, posicao, c);
                    printf("Contato adicionado com sucesso!\n");
                } else {
                    printf("Posição inválida!\n");
                }
                break;
                
            case 2:  // Exibir contato
                printf("Posição (0-%d): ", capacidade - 1);
                scanf("%d", &posicao);
                
                if (posicao >= 0 && posicao < capacidade) {
                    if (agenda[posicao] != NULL) {
                        printf("\n");
                        exibir_contato(agenda[posicao]);
                    } else {
                        printf("Nenhum contato nesta posição!\n");
                    }
                } else {
                    printf("Posição inválida!\n");
                }
                break;
                
            case 3:  // Aumentar capacidade
                {
                    int nova_capacidade;
                    printf("Nova capacidade: ");
                    scanf("%d", &nova_capacidade);
                    
                    if (nova_capacidade > capacidade) {
                        // Cria nova agenda com capacidade ampliada
                        Contato** nova_agenda = criar_agenda(nova_capacidade);
                        
                        // Copia contatos da agenda original
                        for (int i = 0; i < capacidade; i++) {
                            nova_agenda[i] = agenda[i];
                        }
                        
                        // Libera apenas o array da agenda original (não os contatos)
                        free(agenda);
                        
                        // Atualiza referências
                        agenda = nova_agenda;
                        capacidade = nova_capacidade;
                        
                        printf("Capacidade ampliada com sucesso!\n");
                    } else {
                        printf("Nova capacidade deve ser maior que a atual!\n");
                    }
                }
                break;
                
            case 4:  // Sair
                printf("Saindo...\n");
                break;
                
            default:
                printf("Opção inválida!\n");
        }
    } while (opcao != 4);
    
    // Libera a agenda
    liberar_agenda(agenda, capacidade);
    
    return 0;
}
```

Este exemplo demonstra:
1. Alocação dinâmica de estruturas
2. Arrays de ponteiros para estruturas
3. Redimensionamento dinâmico de capacidade
4. Gerenciamento adequado de memória
5. Manipulação de dados através de ponteiros

### 🔧 Boas Práticas de Alocação Dinâmica

1. **Sempre verifique o retorno das funções de alocação** para garantir que a memória foi alocada com sucesso
2. **Libere toda memória alocada** quando não for mais necessária
3. **Atribua NULL a ponteiros após liberar a memória** para evitar ponteiros pendurados
4. **Documente claramente a responsabilidade pela liberação de memória** em APIs
5. **Evite complexidade excessiva** nos padrões de alocação/liberação
6. **Considere estruturas de dados auxiliares** para rastrear a memória alocada em aplicações complexas
7. **Use ferramentas de detecção de vazamento** como Valgrind durante o desenvolvimento
8. **Implemente funções específicas** para inicialização e liberação de estruturas personalizadas

### 📊 Resumo

```
┌─────────────────┬──────────────────────────────────────────────┐
│ Função          │ Descrição                                    │
├─────────────────┼──────────────────────────────────────────────┤
│ malloc(size)    │ Aloca 'size' bytes de memória                │
│ calloc(n, size) │ Aloca memória para 'n' itens de 'size' bytes │
│                 │ e inicializa com zeros                       │
│ realloc(p, size)│ Redimensiona o bloco de memória apontado por │
│                 │ 'p' para 'size' bytes                        │
│ free(p)         │ Libera o bloco de memória apontado por 'p'   │
└─────────────────┴──────────────────────────────────────────────┘
```

A alocação dinâmica de memória é uma ferramenta poderosa em C, permitindo criar programas flexíveis que se adaptam às necessidades em tempo de execução. Entretanto, seu uso adequado requer cuidado e disciplina para evitar problemas como vazamentos de memória e comportamentos indefinidos.

---

[🔙 Voltar ao índice principal](../README.md)

<img width=100% src="https://capsule-render.vercel.app/api?type=waving&color=A8B9CC&height=120&section=footer"/> 