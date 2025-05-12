<img width=100% src="https://capsule-render.vercel.app/api?type=waving&color=A8B9CC&height=120&section=header"/>

# 📄 Estrutura de um programa em C

## 📋 Anatomia de um programa em C

Todo programa em C segue uma estrutura básica que forma a base para qualquer aplicação, desde simples scripts até sistemas operacionais complexos. Vamos explorar os elementos fundamentais que compõem um programa em C.

### 🧩 Estrutura Básica

Um programa em C simples tem a seguinte aparência:

```c
#include <stdio.h>  // Inclusão de biblioteca

int main() {        // Função principal
    // Corpo da função main
    printf("Olá, Mundo!\n");  // Instrução
    
    return 0;       // Valor de retorno
}
```

Vamos analisar cada um desses componentes detalhadamente.

### 📚 Diretivas de Pré-processador

As diretivas de pré-processador são instruções que começam com `#` e são processadas antes da compilação propriamente dita. Elas não são instruções C, mas direcionamentos para o pré-processador.

#### 1. `#include`

A diretiva `#include` insere o conteúdo de outro arquivo no ponto onde ela aparece:

```c
// Inclusão de biblioteca padrão (usa-se < >)
#include <stdio.h>

// Inclusão de arquivo local (usa-se " ")
#include "meu_cabecalho.h"
```

Os arquivos incluídos com `< >` são procurados nos diretórios padrão do sistema, enquanto os incluídos com `" "` são procurados primeiro no diretório atual e depois nos diretórios padrão.

#### 2. `#define`

A diretiva `#define` cria macros, que são substituições de texto realizadas pelo pré-processador:

```c
// Macro simples
#define PI 3.14159

// Macro com parâmetros
#define QUADRADO(x) ((x) * (x))

int main() {
    double raio = 5.0;
    double area = PI * QUADRADO(raio);
    
    return 0;
}
```

#### 3. Outras Diretivas Comuns

```c
// Compilação condicional
#ifdef DEBUG
    printf("Valor da variável: %d\n", x);
#endif

// Impedir inclusão múltipla em arquivos de cabeçalho
#ifndef MINHA_BIBLIOTECA_H
#define MINHA_BIBLIOTECA_H
// conteúdo do arquivo de cabeçalho
#endif

// Definir constantes com base em condições
#if defined(_WIN32)
    #define SEPARADOR '\\'
#else
    #define SEPARADOR '/'
#endif
```

### 🚪 Função `main()`

Todo programa em C deve ter exatamente uma função `main()`. Esta é a função onde a execução do programa se inicia:

```c
int main() {
    // Código aqui
    return 0;
}
```

Existem duas formas principais da função `main()`:

#### 1. Sem Argumentos

```c
int main(void) {
    // "void" explicitamente indica que não recebe argumentos
    return 0;
}
```

#### 2. Com Argumentos da Linha de Comando

```c
int main(int argc, char *argv[]) {
    // argc: número de argumentos
    // argv: array de strings contendo os argumentos
    
    printf("Nome do programa: %s\n", argv[0]);
    
    for (int i = 1; i < argc; i++) {
        printf("Argumento %d: %s\n", i, argv[i]);
    }
    
    return 0;
}
```

Exemplo de linha de comando:
```bash
./programa arg1 arg2 arg3
```

Neste caso:
- `argc` seria 4
- `argv[0]` seria `"./programa"`
- `argv[1]` seria `"arg1"`
- `argv[2]` seria `"arg2"`
- `argv[3]` seria `"arg3"`

### 🔄 Valor de Retorno

A função `main()` deve retornar um valor inteiro, que é usado como código de saída do programa:

```c
int main() {
    // Código aqui
    
    if (operacao_bem_sucedida) {
        return 0;  // Convenção: 0 indica sucesso
    } else {
        return 1;  // Valores não-zero indicam erro
    }
}
```

No shell/terminal, você pode verificar o código de saída de um programa:

**Linux/macOS**:
```bash
./programa
echo $?  # Exibe o código de saída
```

**Windows (PowerShell)**:
```powershell
.\programa.exe
echo $LASTEXITCODE
```

### 📑 Arquivos de Cabeçalho (Headers)

Arquivos de cabeçalho (`.h`) contêm declarações de funções, definições de tipos e macros que podem ser compartilhadas entre múltiplos arquivos `.c`.

#### Biblioteca Padrão

A linguagem C possui diversos arquivos de cabeçalho padrão:

```c
#include <stdio.h>    // Entrada/saída padrão
#include <stdlib.h>   // Utilitários gerais
#include <string.h>   // Manipulação de strings
#include <math.h>     // Funções matemáticas
#include <time.h>     // Funções de data e hora
#include <stdbool.h>  // Tipo booleano (C99 e posterior)
```

#### Criando Seu Próprio Arquivo de Cabeçalho

Um arquivo de cabeçalho personalizado (`matematica.h`):

```c
#ifndef MATEMATICA_H
#define MATEMATICA_H

// Declarações de funções
double somar(double a, double b);
double subtrair(double a, double b);
double multiplicar(double a, double b);
double dividir(double a, double b);

#endif  // MATEMATICA_H
```

Arquivo de implementação correspondente (`matematica.c`):

```c
#include "matematica.h"

double somar(double a, double b) {
    return a + b;
}

double subtrair(double a, double b) {
    return a - b;
}

double multiplicar(double a, double b) {
    return a * b;
}

double dividir(double a, double b) {
    if (b != 0) {
        return a / b;
    } else {
        // Na prática, você poderia lançar um erro
        return 0;
    }
}
```

Como usar no programa principal:

```c
#include <stdio.h>
#include "matematica.h"

int main() {
    double x = 10.0;
    double y = 5.0;
    
    printf("Soma: %.2f\n", somar(x, y));
    printf("Diferença: %.2f\n", subtrair(x, y));
    
    return 0;
}
```

### 🏛️ Escopo e Blocos de Código

Em C, o escopo é definido por blocos delimitados por chaves `{}`:

```c
int main() {
    // Variáveis declaradas aqui são acessíveis em todo o main
    int x = 10;
    
    {
        // Este é um bloco interno
        // Variáveis declaradas aqui só são acessíveis dentro deste bloco
        int y = 20;
        printf("x = %d, y = %d\n", x, y);  // Funciona
    }
    
    // printf("y = %d\n", y);  // Erro! 'y' não existe neste escopo
    
    return 0;
}
```

### 📊 Programa Completo Multi-arquivo

Para programas maiores, é comum dividir o código em múltiplos arquivos:

#### Estrutura de Diretórios
```
projeto/
├── include/
│   ├── matematica.h
│   └── util.h
├── src/
│   ├── main.c
│   ├── matematica.c
│   └── util.c
└── Makefile
```

#### Arquivo de Cabeçalho (`include/matematica.h`)
```c
#ifndef MATEMATICA_H
#define MATEMATICA_H

double somar(double a, double b);
double subtrair(double a, double b);

#endif
```

#### Implementação (`src/matematica.c`)
```c
#include "matematica.h"

double somar(double a, double b) {
    return a + b;
}

double subtrair(double a, double b) {
    return a - b;
}
```

#### Programa Principal (`src/main.c`)
```c
#include <stdio.h>
#include "matematica.h"
#include "util.h"

int main() {
    double x = 10.0;
    double y = 5.0;
    
    printf("Soma: %.2f\n", somar(x, y));
    printf("Diferença: %.2f\n", subtrair(x, y));
    
    imprimir_linha();  // Função definida em util.c
    
    return 0;
}
```

#### Makefile
```makefile
CC = gcc
CFLAGS = -Wall -I./include

programa: main.o matematica.o util.o
	$(CC) -o programa main.o matematica.o util.o

main.o: src/main.c
	$(CC) $(CFLAGS) -c src/main.c

matematica.o: src/matematica.c include/matematica.h
	$(CC) $(CFLAGS) -c src/matematica.c

util.o: src/util.c include/util.h
	$(CC) $(CFLAGS) -c src/util.c

clean:
	rm -f *.o programa
```

### 🔍 Exemplos Completos

#### 1. Programa Simples
```c
#include <stdio.h>

int main() {
    printf("Olá, Mundo!\n");
    return 0;
}
```

#### 2. Programa com Entrada de Usuário
```c
#include <stdio.h>

int main() {
    char nome[50];
    int idade;
    
    printf("Digite seu nome: ");
    scanf("%49s", nome);
    
    printf("Digite sua idade: ");
    scanf("%d", &idade);
    
    printf("Olá, %s! Você tem %d anos.\n", nome, idade);
    
    return 0;
}
```

#### 3. Programa com Múltiplas Funções
```c
#include <stdio.h>

// Declarações de funções
void saudacao();
int somar(int a, int b);

int main() {
    saudacao();
    
    int resultado = somar(5, 7);
    printf("5 + 7 = %d\n", resultado);
    
    return 0;
}

// Definições de funções
void saudacao() {
    printf("Bem-vindo ao programa!\n");
}

int somar(int a, int b) {
    return a + b;
}
```

### 🧠 Boas Práticas

1. **Organização clara**: Divida o código em funções com propósitos bem definidos
2. **Nomes significativos**: Use nomes de variáveis e funções que descrevam seu propósito
3. **Comentários úteis**: Explique o "porquê", não o "o quê" (o código já mostra o que está fazendo)
4. **Um arquivo, uma responsabilidade**: Cada arquivo `.c` deve ter uma responsabilidade bem definida
5. **Guarda de inclusão**: Sempre use guardas (`#ifndef`, `#define`, `#endif`) em arquivos de cabeçalho
6. **Verificação de erros**: Sempre verifique valores de retorno de funções que podem falhar
7. **Constantes em vez de literais**: Use `#define` ou `const` para valores que não mudam

---

[🔙 Voltar ao índice principal](../README.md)

<img width=100% src="https://capsule-render.vercel.app/api?type=waving&color=A8B9CC&height=120&section=footer"/> 