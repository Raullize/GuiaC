<img width=100% src="https://capsule-render.vercel.app/api?type=waving&color=A8B9CC&height=120&section=header"/>

# 🔧 Structs

## 📋 Definição e Uso de Estruturas em C

As estruturas (structs) são um dos recursos mais poderosos da linguagem C, permitindo agrupar variáveis de diferentes tipos em um único tipo de dado personalizado. Elas são fundamentais para a criação de tipos de dados complexos e para organizar informações relacionadas.

### 🧩 Conceito Básico

Uma estrutura em C é uma coleção de variáveis (possivelmente de tipos diferentes) agrupadas sob um único nome. Cada variável dentro da estrutura é chamada de "membro" ou "campo".

#### 1️⃣ Sintaxe para Definir uma Estrutura

```c
struct nome_da_estrutura {
    tipo_1 membro_1;
    tipo_2 membro_2;
    // ...
    tipo_n membro_n;
};
```

#### 2️⃣ Exemplo Simples

```c
#include <stdio.h>
#include <string.h>

// Definição da estrutura
struct Pessoa {
    char nome[50];
    int idade;
    float altura;
};

int main() {
    // Declaração e inicialização de uma variável do tipo struct Pessoa
    struct Pessoa pessoa1;
    
    // Atribuindo valores aos membros
    strcpy(pessoa1.nome, "João Silva");
    pessoa1.idade = 25;
    pessoa1.altura = 1.75;
    
    // Acessando e exibindo os dados
    printf("Nome: %s\n", pessoa1.nome);
    printf("Idade: %d anos\n", pessoa1.idade);
    printf("Altura: %.2f metros\n", pessoa1.altura);
    
    return 0;
}
```

### 🔧 Declarando e Usando Estruturas

#### 1️⃣ Diferentes Formas de Declaração

**Declaração e uso separados**:
```c
// Definição da estrutura
struct Ponto {
    int x;
    int y;
};

// Uso da estrutura
struct Ponto p1, p2;
```

**Declaração com definição de variáveis**:
```c
struct Ponto {
    int x;
    int y;
} p1, p2;
```

**Estrutura sem nome (anônima)**:
```c
struct {
    int x;
    int y;
} p1, p2;
```

#### 2️⃣ Inicialização de Estruturas

**Inicialização na declaração**:
```c
struct Ponto p1 = {10, 20};  // x = 10, y = 20
```

**Inicialização com designadores (C99 e posteriores)**:
```c
struct Ponto p1 = {.y = 20, .x = 10};  // Ordem não importa
```

**Inicialização após a declaração**:
```c
struct Ponto p1;
p1.x = 10;
p1.y = 20;
```

#### 3️⃣ Acessando Membros de Estruturas

Para acessar um membro de uma estrutura, usamos o operador ponto (`.`):

```c
struct Ponto p1 = {10, 20};
printf("Coordenadas: (%d, %d)\n", p1.x, p1.y);

// Modificando um membro
p1.x = 15;
```

### 🔄 Estruturas em Funções

#### 1️⃣ Passando Estruturas para Funções

Estruturas podem ser passadas para funções por valor ou por referência:

**Passagem por valor**:
```c
#include <stdio.h>

struct Ponto {
    int x;
    int y;
};

// Função que recebe uma estrutura por valor
void exibir_ponto(struct Ponto p) {
    printf("Ponto: (%d, %d)\n", p.x, p.y);
}

// Função que retorna uma estrutura
struct Ponto criar_ponto(int x, int y) {
    struct Ponto p;
    p.x = x;
    p.y = y;
    return p;
}

int main() {
    struct Ponto p1 = {10, 20};
    exibir_ponto(p1);
    
    struct Ponto p2 = criar_ponto(30, 40);
    exibir_ponto(p2);
    
    return 0;
}
```

**Passagem por referência** (usando ponteiros):
```c
#include <stdio.h>

struct Ponto {
    int x;
    int y;
};

// Função que recebe um ponteiro para uma estrutura
void deslocar_ponto(struct Ponto* p, int dx, int dy) {
    p->x += dx;  // Note o uso do operador seta (->)
    p->y += dy;
}

int main() {
    struct Ponto p1 = {10, 20};
    printf("Antes: (%d, %d)\n", p1.x, p1.y);
    
    deslocar_ponto(&p1, 5, 7);
    
    printf("Depois: (%d, %d)\n", p1.x, p1.y);
    
    return 0;
}
```

#### 2️⃣ Operador Seta (->)

O operador seta é usado para acessar membros de uma estrutura através de um ponteiro:

```c
struct Ponto* p_ptr = &p1;
p_ptr->x = 100;  // Equivalente a (*p_ptr).x = 100;
```

### 🧠 Typedef com Estruturas

A palavra-chave `typedef` permite criar apelidos para tipos de dados, incluindo estruturas, simplificando o código:

```c
#include <stdio.h>
#include <string.h>

// Definição da estrutura com typedef
typedef struct {
    char nome[50];
    int idade;
    float altura;
} Pessoa;

int main() {
    // Agora podemos declarar variáveis sem usar a palavra 'struct'
    Pessoa pessoa1;
    
    strcpy(pessoa1.nome, "Maria Santos");
    pessoa1.idade = 30;
    pessoa1.altura = 1.65;
    
    printf("Nome: %s\n", pessoa1.nome);
    printf("Idade: %d anos\n", pessoa1.idade);
    printf("Altura: %.2f metros\n", pessoa1.altura);
    
    return 0;
}
```

### 🏗️ Estruturas Aninhadas

Estruturas podem conter outras estruturas como membros:

```c
#include <stdio.h>

typedef struct {
    int dia;
    int mes;
    int ano;
} Data;

typedef struct {
    char nome[50];
    int idade;
    Data data_nascimento;  // Estrutura aninhada
} Pessoa;

int main() {
    Pessoa pessoa;
    
    // Atribuindo valores
    strcpy(pessoa.nome, "Carlos Oliveira");
    pessoa.idade = 28;
    pessoa.data_nascimento.dia = 15;
    pessoa.data_nascimento.mes = 3;
    pessoa.data_nascimento.ano = 1995;
    
    // Acessando e exibindo os dados
    printf("Nome: %s\n", pessoa.nome);
    printf("Idade: %d anos\n", pessoa.idade);
    printf("Data de Nascimento: %02d/%02d/%d\n", 
           pessoa.data_nascimento.dia, 
           pessoa.data_nascimento.mes, 
           pessoa.data_nascimento.ano);
    
    return 0;
}
```

### 📏 Tamanho das Estruturas e Alinhamento de Memória

#### 1️⃣ Tamanho das Estruturas

O tamanho de uma estrutura não é necessariamente a soma dos tamanhos de seus membros, devido ao alinhamento de memória:

```c
#include <stdio.h>

struct Exemplo1 {
    char c;     // 1 byte
    int i;      // 4 bytes
    double d;   // 8 bytes
};

struct Exemplo2 {
    int i;      // 4 bytes
    double d;   // 8 bytes
    char c;     // 1 byte
};

int main() {
    printf("Tamanho de char: %zu bytes\n", sizeof(char));
    printf("Tamanho de int: %zu bytes\n", sizeof(int));
    printf("Tamanho de double: %zu bytes\n", sizeof(double));
    
    printf("Soma dos membros: %zu bytes\n", sizeof(char) + sizeof(int) + sizeof(double));
    
    printf("Tamanho de struct Exemplo1: %zu bytes\n", sizeof(struct Exemplo1));
    printf("Tamanho de struct Exemplo2: %zu bytes\n", sizeof(struct Exemplo2));
    
    return 0;
}
```

A saída poderia ser:
```
Tamanho de char: 1 bytes
Tamanho de int: 4 bytes
Tamanho de double: 8 bytes
Soma dos membros: 13 bytes
Tamanho de struct Exemplo1: 16 bytes
Tamanho de struct Exemplo2: 24 bytes
```

Isso ocorre porque o compilador adiciona preenchimento (padding) entre os membros para garantir que cada membro esteja alinhado corretamente na memória.

#### 2️⃣ Empacotamento de Estruturas

Em alguns casos, é possível controlar o alinhamento usando diretivas do compilador:

```c
#include <stdio.h>

// Estrutura normal com padding
struct NormalStruct {
    char a;
    int b;
    char c;
};

// Estrutura empacotada (usando GCC)
#pragma pack(1)
struct PackedStruct {
    char a;
    int b;
    char c;
};
#pragma pack()

int main() {
    printf("Tamanho de NormalStruct: %zu bytes\n", sizeof(struct NormalStruct));
    printf("Tamanho de PackedStruct: %zu bytes\n", sizeof(struct PackedStruct));
    
    return 0;
}
```

**Nota**: Embora o empacotamento economize memória, pode reduzir a eficiência de acesso em algumas arquiteturas de CPU.

### 🔄 Arrays de Estruturas

Podemos criar arrays onde cada elemento é uma estrutura:

```c
#include <stdio.h>
#include <string.h>

typedef struct {
    char nome[50];
    int idade;
} Pessoa;

int main() {
    // Array de 3 pessoas
    Pessoa pessoas[3];
    
    // Atribuindo valores
    strcpy(pessoas[0].nome, "Ana");
    pessoas[0].idade = 25;
    
    strcpy(pessoas[1].nome, "Bruno");
    pessoas[1].idade = 32;
    
    strcpy(pessoas[2].nome, "Carla");
    pessoas[2].idade = 28;
    
    // Percorrendo e exibindo o array
    for (int i = 0; i < 3; i++) {
        printf("Pessoa %d:\n", i+1);
        printf("  Nome: %s\n", pessoas[i].nome);
        printf("  Idade: %d anos\n", pessoas[i].idade);
    }
    
    return 0;
}
```

### 🔢 Enumerações (enum) com Estruturas

Enumerações são frequentemente usadas com estruturas para criar códigos mais legíveis:

```c
#include <stdio.h>
#include <string.h>

// Definindo uma enumeração
typedef enum {
    SOLTEIRO,
    CASADO,
    DIVORCIADO,
    VIUVO
} EstadoCivil;

typedef struct {
    char nome[50];
    int idade;
    EstadoCivil estado_civil;
} Pessoa;

int main() {
    Pessoa pessoa;
    
    strcpy(pessoa.nome, "Paulo Souza");
    pessoa.idade = 35;
    pessoa.estado_civil = CASADO;
    
    printf("Nome: %s\n", pessoa.nome);
    printf("Idade: %d anos\n", pessoa.idade);
    
    // Exibindo o estado civil
    printf("Estado Civil: ");
    switch (pessoa.estado_civil) {
        case SOLTEIRO:
            printf("Solteiro\n");
            break;
        case CASADO:
            printf("Casado\n");
            break;
        case DIVORCIADO:
            printf("Divorciado\n");
            break;
        case VIUVO:
            printf("Viúvo\n");
            break;
    }
    
    return 0;
}
```

### 🧩 Uniões (union) e Estruturas

Uniões permitem que diferentes tipos de dados ocupem o mesmo espaço de memória, e frequentemente são usadas dentro de estruturas:

```c
#include <stdio.h>
#include <string.h>

// Definindo uma união
typedef union {
    int i;
    float f;
    char str[20];
} Valor;

typedef struct {
    char nome[50];
    char tipo;  // 'i' para inteiro, 'f' para float, 's' para string
    Valor valor;
} Item;

int main() {
    Item item1, item2, item3;
    
    // Item com valor inteiro
    strcpy(item1.nome, "Contador");
    item1.tipo = 'i';
    item1.valor.i = 100;
    
    // Item com valor float
    strcpy(item2.nome, "Preço");
    item2.tipo = 'f';
    item2.valor.f = 19.99;
    
    // Item com valor string
    strcpy(item3.nome, "Descrição");
    item3.tipo = 's';
    strcpy(item3.valor.str, "Produto básico");
    
    // Exibindo os itens
    printf("Item 1:\n");
    printf("  Nome: %s\n", item1.nome);
    printf("  Valor: %d\n", item1.valor.i);
    
    printf("\nItem 2:\n");
    printf("  Nome: %s\n", item2.nome);
    printf("  Valor: %.2f\n", item2.valor.f);
    
    printf("\nItem 3:\n");
    printf("  Nome: %s\n", item3.nome);
    printf("  Valor: %s\n", item3.valor.str);
    
    return 0;
}
```

### 📝 Exemplo Prático: Sistema de Gerenciamento de Biblioteca

Este exemplo demonstra um sistema simples de gerenciamento de biblioteca usando estruturas:

```c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

#define MAX_LIVROS 100
#define MAX_STRING 100

// Enumeração para o status do livro
typedef enum {
    DISPONIVEL,
    EMPRESTADO,
    EM_MANUTENCAO
} StatusLivro;

// Estrutura para data
typedef struct {
    int dia;
    int mes;
    int ano;
} Data;

// Estrutura para livro
typedef struct {
    int id;
    char titulo[MAX_STRING];
    char autor[MAX_STRING];
    char editora[MAX_STRING];
    int ano_publicacao;
    StatusLivro status;
    Data data_aquisicao;
} Livro;

// Estrutura para a biblioteca
typedef struct {
    Livro livros[MAX_LIVROS];
    int quantidade_livros;
} Biblioteca;

// Funções
void inicializar_biblioteca(Biblioteca* bib) {
    bib->quantidade_livros = 0;
}

void adicionar_livro(Biblioteca* bib, const char* titulo, const char* autor, 
                     const char* editora, int ano_pub, Data data_aquisicao) {
    if (bib->quantidade_livros >= MAX_LIVROS) {
        printf("Erro: Biblioteca cheia!\n");
        return;
    }
    
    Livro novo_livro;
    novo_livro.id = bib->quantidade_livros + 1;
    strncpy(novo_livro.titulo, titulo, MAX_STRING - 1);
    strncpy(novo_livro.autor, autor, MAX_STRING - 1);
    strncpy(novo_livro.editora, editora, MAX_STRING - 1);
    novo_livro.ano_publicacao = ano_pub;
    novo_livro.status = DISPONIVEL;
    novo_livro.data_aquisicao = data_aquisicao;
    
    bib->livros[bib->quantidade_livros] = novo_livro;
    bib->quantidade_livros++;
    
    printf("Livro \"%s\" adicionado com sucesso (ID: %d).\n", 
           titulo, novo_livro.id);
}

void buscar_livro_por_titulo(Biblioteca* bib, const char* titulo) {
    int encontrados = 0;
    
    printf("\nResultados da busca por \"%s\":\n", titulo);
    printf("------------------------------------------\n");
    
    for (int i = 0; i < bib->quantidade_livros; i++) {
        // Busca case-insensitive e parcial
        if (strstr(bib->livros[i].titulo, titulo) != NULL) {
            printf("ID: %d\n", bib->livros[i].id);
            printf("Título: %s\n", bib->livros[i].titulo);
            printf("Autor: %s\n", bib->livros[i].autor);
            printf("Editora: %s\n", bib->livros[i].editora);
            printf("Ano: %d\n", bib->livros[i].ano_publicacao);
            
            printf("Status: ");
            switch (bib->livros[i].status) {
                case DISPONIVEL:
                    printf("Disponível\n");
                    break;
                case EMPRESTADO:
                    printf("Emprestado\n");
                    break;
                case EM_MANUTENCAO:
                    printf("Em manutenção\n");
                    break;
            }
            
            printf("Data de Aquisição: %02d/%02d/%d\n", 
                   bib->livros[i].data_aquisicao.dia,
                   bib->livros[i].data_aquisicao.mes,
                   bib->livros[i].data_aquisicao.ano);
            
            printf("------------------------------------------\n");
            encontrados++;
        }
    }
    
    if (encontrados == 0) {
        printf("Nenhum livro encontrado com o título \"%s\".\n", titulo);
    } else {
        printf("Total de livros encontrados: %d\n", encontrados);
    }
}

void alterar_status_livro(Biblioteca* bib, int id, StatusLivro novo_status) {
    for (int i = 0; i < bib->quantidade_livros; i++) {
        if (bib->livros[i].id == id) {
            StatusLivro status_antigo = bib->livros[i].status;
            bib->livros[i].status = novo_status;
            
            printf("Status do livro \"%s\" alterado: ", bib->livros[i].titulo);
            
            switch (status_antigo) {
                case DISPONIVEL:
                    printf("Disponível");
                    break;
                case EMPRESTADO:
                    printf("Emprestado");
                    break;
                case EM_MANUTENCAO:
                    printf("Em manutenção");
                    break;
            }
            
            printf(" -> ");
            
            switch (novo_status) {
                case DISPONIVEL:
                    printf("Disponível\n");
                    break;
                case EMPRESTADO:
                    printf("Emprestado\n");
                    break;
                case EM_MANUTENCAO:
                    printf("Em manutenção\n");
                    break;
            }
            
            return;
        }
    }
    
    printf("Erro: Livro com ID %d não encontrado.\n", id);
}

void listar_todos_livros(Biblioteca* bib) {
    if (bib->quantidade_livros == 0) {
        printf("A biblioteca está vazia.\n");
        return;
    }
    
    printf("\nListagem de todos os livros:\n");
    printf("------------------------------------------\n");
    
    for (int i = 0; i < bib->quantidade_livros; i++) {
        printf("ID: %d\n", bib->livros[i].id);
        printf("Título: %s\n", bib->livros[i].titulo);
        printf("Autor: %s\n", bib->livros[i].autor);
        printf("Status: ");
        
        switch (bib->livros[i].status) {
            case DISPONIVEL:
                printf("Disponível\n");
                break;
            case EMPRESTADO:
                printf("Emprestado\n");
                break;
            case EM_MANUTENCAO:
                printf("Em manutenção\n");
                break;
        }
        
        printf("------------------------------------------\n");
    }
    
    printf("Total de livros: %d\n", bib->quantidade_livros);
}

int main() {
    Biblioteca minha_biblioteca;
    inicializar_biblioteca(&minha_biblioteca);
    
    // Adicionando alguns livros
    Data data1 = {15, 3, 2020};
    adicionar_livro(&minha_biblioteca, "O Senhor dos Anéis", "J.R.R. Tolkien", 
                    "HarperCollins", 1954, data1);
    
    Data data2 = {10, 7, 2021};
    adicionar_livro(&minha_biblioteca, "Harry Potter e a Pedra Filosofal", 
                    "J.K. Rowling", "Rocco", 1997, data2);
    
    Data data3 = {22, 11, 2019};
    adicionar_livro(&minha_biblioteca, "1984", "George Orwell", 
                    "Companhia das Letras", 1949, data3);
    
    // Listar todos os livros
    listar_todos_livros(&minha_biblioteca);
    
    // Buscar por título
    buscar_livro_por_titulo(&minha_biblioteca, "Potter");
    
    // Alterar status de um livro
    alterar_status_livro(&minha_biblioteca, 2, EMPRESTADO);
    
    // Listar novamente para verificar a alteração
    listar_todos_livros(&minha_biblioteca);
    
    return 0;
}
```

### 🧠 Boas Práticas ao Trabalhar com Estruturas

1. **Use typedef para simplificar a sintaxe** - Facilita a leitura e escrita do código
2. **Mantenha as estruturas coesas** - Cada estrutura deve representar um conceito único e bem definido
3. **Considere o encapsulamento** - Crie funções para manipular estruturas, mantendo a lógica em um só lugar
4. **Seja consciente com o alinhamento de memória** - A ordem dos membros pode afetar o tamanho total da estrutura
5. **Documente o propósito** - Adicione comentários explicando o propósito da estrutura e seus membros
6. **Inicialize estruturas** - Sempre inicialize todos os membros para evitar comportamentos inesperados
7. **Use constantes para tamanhos de arrays** - Isso torna o código mais manutenível
8. **Verifique alocações dinâmicas** - Ao alocar estruturas dinamicamente, sempre verifique se a alocação foi bem-sucedida

### 📊 Resumo

```
┌─────────────────────────┬───────────────────────────────────────┐
│ Aspecto                 │ Detalhes                              │
├─────────────────────────┼───────────────────────────────────────┤
│ Declaração              │ struct Nome {membros};                │
│ Typedef                 │ typedef struct {membros} Nome;        │
│ Acessar membros         │ estrutura.membro                      │
│ Acessar via ponteiro    │ ponteiro->membro                      │
│ Inicialização           │ {valor1, valor2, ...}                 │
│ Passagem para funções   │ Por valor ou referência (ponteiro)    │
│ Tamanho                 │ Afetado pelo alinhamento de memória   │
│ Aninhamento             │ Estruturas dentro de estruturas       │
│ Uso com arrays          │ tipo_estrutura array[tamanho];        │
└─────────────────────────┴───────────────────────────────────────┘
```

As estruturas são uma ferramenta essencial em C para organizar dados relacionados e criar tipos de dados complexos. Elas são a base para a implementação de estruturas de dados mais avançadas como listas encadeadas, árvores e grafos, e são amplamente utilizadas em aplicações do mundo real.

---

[🔙 Voltar ao índice principal](../README.md)

<img width=100% src="https://capsule-render.vercel.app/api?type=waving&color=A8B9CC&height=120&section=footer"/> 