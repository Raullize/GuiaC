<img width=100% src="https://capsule-render.vercel.app/api?type=waving&color=A8B9CC&height=120&section=header"/>

# 🔣 Funções: Declaração e Definição

## 📋 Introdução às Funções em C

Funções são blocos de código que realizam tarefas específicas e podem ser reutilizados ao longo do programa. Elas ajudam a organizar o código, evitar repetição e melhorar a legibilidade e manutenção.

### 🧩 Componentes de uma Função

Uma função em C tem quatro componentes principais:

1. **Tipo de retorno**: Especifica o tipo de dado que a função retorna (ou `void` se não retornar nada)
2. **Nome**: Identificador único para a função
3. **Parâmetros**: Valores que a função recebe para processar (opcional)
4. **Corpo**: O bloco de código que define o que a função faz

```c
tipo_retorno nome_funcao(parametro1, parametro2, ...) {
    // Corpo da função
    // Código a ser executado
    return valor;  // Opcional, dependendo do tipo de retorno
}
```

### 🔄 Declaração vs. Definição

Em C, é importante entender a diferença entre declarar e definir uma função:

#### 1️⃣ Declaração de Função (Protótipo)

A declaração informa ao compilador sobre a existência de uma função, seu tipo de retorno e parâmetros.

```c
// Declaração/Protótipo
int soma(int a, int b);
```

#### 2️⃣ Definição de Função

A definição contém o corpo da função, ou seja, o código que será executado quando a função for chamada.

```c
// Definição
int soma(int a, int b) {
    return a + b;
}
```

#### 3️⃣ Exemplo Completo

```c
#include <stdio.h>

// Declaração (Protótipo)
int soma(int a, int b);
void saudacao(void);

int main() {
    saudacao();
    
    int resultado = soma(5, 3);
    printf("Soma: %d\n", resultado);
    
    return 0;
}

// Definição
void saudacao(void) {
    printf("Olá! Bem-vindo ao programa.\n");
}

// Definição
int soma(int a, int b) {
    return a + b;
}
```

### 🚀 Chamada de Funções

Para usar (chamar) uma função, você escreve seu nome seguido de parênteses contendo os argumentos (se houver):

```c
#include <stdio.h>

// Definição
float calcular_media(float a, float b, float c) {
    return (a + b + c) / 3.0;
}

int main() {
    float nota1 = 7.5;
    float nota2 = 8.0;
    float nota3 = 6.5;
    
    // Chamada da função
    float media = calcular_media(nota1, nota2, nota3);
    
    printf("A média das notas é: %.2f\n", media);
    
    // Também podemos chamar diretamente no printf
    printf("Media recalculada: %.2f\n", calcular_media(7.5, 8.0, 6.5));
    
    return 0;
}
```

### 📝 Parâmetros de Função

#### 1️⃣ Passagem por Valor

Em C, os parâmetros são passados "por valor" por padrão, o que significa que a função recebe uma cópia do valor original. Alterações nos parâmetros dentro da função não afetam as variáveis originais.

```c
#include <stdio.h>

void tentar_modificar(int x) {
    x = x * 2;  // Modifica apenas a cópia local
    printf("Dentro da função: x = %d\n", x);
}

int main() {
    int a = 5;
    
    printf("Antes da função: a = %d\n", a);
    tentar_modificar(a);
    printf("Depois da função: a = %d\n", a);  // O valor não muda
    
    return 0;
}
```

#### 2️⃣ Parâmetro `void`

Uma função pode ser definida para não receber nenhum parâmetro usando `void`:

```c
void mensagem_inicio(void) {
    printf("Programa iniciado.\n");
}
```

### 🔄 Tipo de Retorno de Função

O tipo de retorno especifica o tipo de dado que a função devolve após sua execução.

#### 1️⃣ Funções com Retorno

```c
#include <stdio.h>

int quadrado(int num) {
    return num * num;
}

float area_circulo(float raio) {
    const float PI = 3.14159;
    return PI * raio * raio;
}

int main() {
    int n = 5;
    printf("O quadrado de %d é %d\n", n, quadrado(n));
    
    float r = 2.5;
    printf("A área do círculo com raio %.2f é %.2f\n", r, area_circulo(r));
    
    return 0;
}
```

#### 2️⃣ Funções `void` (sem retorno)

Funções do tipo `void` não retornam nenhum valor:

```c
#include <stdio.h>

void imprimir_linha(char caractere, int quantidade) {
    for (int i = 0; i < quantidade; i++) {
        printf("%c", caractere);
    }
    printf("\n");
}

int main() {
    imprimir_linha('-', 20);
    printf("Menu Principal\n");
    imprimir_linha('-', 20);
    
    return 0;
}
```

### 📂 Funções em Arquivos Separados

Em projetos maiores, é comum dividir o código em múltiplos arquivos:

#### 1️⃣ Arquivo de Cabeçalho (matematica.h)

```c
#ifndef MATEMATICA_H
#define MATEMATICA_H

// Declarações das funções
int soma(int a, int b);
int subtracao(int a, int b);
int multiplicacao(int a, int b);
float divisao(int a, int b);

#endif
```

#### 2️⃣ Arquivo de Implementação (matematica.c)

```c
#include "matematica.h"

// Definições das funções
int soma(int a, int b) {
    return a + b;
}

int subtracao(int a, int b) {
    return a - b;
}

int multiplicacao(int a, int b) {
    return a * b;
}

float divisao(int a, int b) {
    if (b != 0) {
        return (float)a / b;
    } else {
        return 0; // Tratamento simples para divisão por zero
    }
}
```

#### 3️⃣ Arquivo Principal (main.c)

```c
#include <stdio.h>
#include "matematica.h"

int main() {
    int x = 10, y = 3;
    
    printf("Soma: %d\n", soma(x, y));
    printf("Subtração: %d\n", subtracao(x, y));
    printf("Multiplicação: %d\n", multiplicacao(x, y));
    printf("Divisão: %.2f\n", divisao(x, y));
    
    return 0;
}
```

### 📚 Biblioteca Padrão de Funções

C possui uma rica biblioteca padrão com funções predefinidas. Para usá-las, você precisa incluir o arquivo de cabeçalho correspondente:

| Biblioteca   | Descrição                              | Funções Comuns |
|--------------|----------------------------------------|----------------|
| `<stdio.h>`  | Entrada/Saída                          | `printf`, `scanf`, `fopen` |
| `<stdlib.h>` | Funções utilitárias                    | `malloc`, `free`, `rand`   |
| `<string.h>` | Manipulação de strings                 | `strcpy`, `strlen`, `strcmp` |
| `<math.h>`   | Funções matemáticas                    | `sqrt`, `pow`, `sin`       |
| `<time.h>`   | Funções relacionadas a tempo           | `time`, `difftime`         |
| `<ctype.h>`  | Classificação e conversão de caracteres| `isdigit`, `toupper`       |

```c
#include <stdio.h>
#include <math.h>
#include <string.h>
#include <ctype.h>

int main() {
    // Funções matemáticas
    printf("Raiz quadrada de 16: %.2f\n", sqrt(16.0));
    printf("2 elevado a 3: %.2f\n", pow(2.0, 3.0));
    
    // Funções de string
    char texto[20] = "Exemplo";
    printf("Tamanho: %lu\n", strlen(texto));
    
    // Funções de caractere
    char c = 'a';
    printf("'%c' em maiúsculo: '%c'\n", c, toupper(c));
    
    return 0;
}
```

### 🧮 Funções com Número Variável de Argumentos

C permite criar funções que aceitam um número variável de argumentos usando o cabeçalho `<stdarg.h>`:

```c
#include <stdio.h>
#include <stdarg.h>

// Função que calcula a média de n números
double media(int n, ...) {
    va_list args;
    double soma = 0.0;
    
    va_start(args, n);
    
    for (int i = 0; i < n; i++) {
        soma += va_arg(args, double);
    }
    
    va_end(args);
    
    return soma / n;
}

int main() {
    printf("Média de 2, 4, 6: %.2f\n", media(3, 2.0, 4.0, 6.0));
    printf("Média de 1, 3, 5, 7, 9: %.2f\n", media(5, 1.0, 3.0, 5.0, 7.0, 9.0));
    
    return 0;
}
```

### 🎯 Funções Inline

Em C99 e posteriores, você pode usar a palavra-chave `inline` para sugerir ao compilador que incorpore o código da função diretamente no local da chamada, o que pode melhorar o desempenho para funções pequenas e frequentemente chamadas:

```c
#include <stdio.h>

// Função inline
inline int maximo(int a, int b) {
    return (a > b) ? a : b;
}

int main() {
    int x = 10, y = 20;
    printf("O maior valor é: %d\n", maximo(x, y));
    
    return 0;
}
```

### 🧠 Funções Recursivas

Uma função recursiva é aquela que chama a si mesma. É útil para problemas que podem ser divididos em subproblemas idênticos:

```c
#include <stdio.h>

// Função recursiva para calcular o fatorial
unsigned long fatorial(unsigned int n) {
    if (n <= 1) {
        return 1;  // Caso base
    } else {
        return n * fatorial(n - 1);  // Chamada recursiva
    }
}

int main() {
    unsigned int num = 5;
    printf("%u! = %lu\n", num, fatorial(num));
    
    return 0;
}
```

A recursão será coberta com mais detalhes em um capítulo específico.

### 🧪 Boas Práticas para Funções

1. **Nomes significativos**: Escolha nomes que indiquem claramente o que a função faz
2. **Uma responsabilidade**: Cada função deve ter uma única responsabilidade bem definida
3. **Coesão**: O código dentro da função deve estar relacionado a uma única tarefa
4. **Tamanho razoável**: Funções grandes devem ser divididas em funções menores
5. **Documentação**: Comente o propósito da função, parâmetros e valor de retorno
6. **Validação de parâmetros**: Verifique se os parâmetros são válidos antes de processá-los
7. **Tratamento de erros**: Implemente uma estratégia para lidar com erros

### 🎭 Exemplo de Programa Completo

Este programa demonstra o uso de funções para criar um simples conversor de unidades:

```c
#include <stdio.h>

// Protótipos das funções
float celsius_para_fahrenheit(float celsius);
float fahrenheit_para_celsius(float fahrenheit);
float km_para_milhas(float km);
float milhas_para_km(float milhas);
float litros_para_galoes(float litros);
float galoes_para_litros(float galoes);
void exibir_menu(void);
void linha_separadora(void);

int main() {
    int opcao;
    float valor, resultado;
    
    do {
        exibir_menu();
        printf("Escolha uma opção (0 para sair): ");
        scanf("%d", &opcao);
        
        if (opcao >= 1 && opcao <= 6) {
            printf("Digite o valor a converter: ");
            scanf("%f", &valor);
        }
        
        switch (opcao) {
            case 1:
                resultado = celsius_para_fahrenheit(valor);
                printf("%.2f °C = %.2f °F\n", valor, resultado);
                break;
            case 2:
                resultado = fahrenheit_para_celsius(valor);
                printf("%.2f °F = %.2f °C\n", valor, resultado);
                break;
            case 3:
                resultado = km_para_milhas(valor);
                printf("%.2f km = %.2f milhas\n", valor, resultado);
                break;
            case 4:
                resultado = milhas_para_km(valor);
                printf("%.2f milhas = %.2f km\n", valor, resultado);
                break;
            case 5:
                resultado = litros_para_galoes(valor);
                printf("%.2f litros = %.2f galões\n", valor, resultado);
                break;
            case 6:
                resultado = galoes_para_litros(valor);
                printf("%.2f galões = %.2f litros\n", valor, resultado);
                break;
            case 0:
                printf("Encerrando o programa...\n");
                break;
            default:
                printf("Opção inválida!\n");
        }
        
        if (opcao != 0) {
            printf("\nPressione Enter para continuar...");
            getchar();  // Consome o newline do scanf anterior
            getchar();  // Espera pelo Enter
        }
        
    } while (opcao != 0);
    
    return 0;
}

// Definições das funções
float celsius_para_fahrenheit(float celsius) {
    return (celsius * 9.0 / 5.0) + 32.0;
}

float fahrenheit_para_celsius(float fahrenheit) {
    return (fahrenheit - 32.0) * 5.0 / 9.0;
}

float km_para_milhas(float km) {
    return km * 0.621371;
}

float milhas_para_km(float milhas) {
    return milhas / 0.621371;
}

float litros_para_galoes(float litros) {
    return litros * 0.264172;
}

float galoes_para_litros(float galoes) {
    return galoes / 0.264172;
}

void exibir_menu(void) {
    // Limpa a tela (funciona no Windows)
    system("cls");
    
    linha_separadora();
    printf("     CONVERSOR DE UNIDADES     \n");
    linha_separadora();
    printf("1. Celsius para Fahrenheit\n");
    printf("2. Fahrenheit para Celsius\n");
    printf("3. Quilômetros para Milhas\n");
    printf("4. Milhas para Quilômetros\n");
    printf("5. Litros para Galões\n");
    printf("6. Galões para Litros\n");
    printf("0. Sair\n");
    linha_separadora();
}

void linha_separadora(void) {
    printf("-------------------------------\n");
}
```

Este programa demonstra:
- Declaração e definição de funções
- Funções com retorno e sem retorno
- Organização de código usando funções
- Reutilização de funções (linha_separadora)
- Interface com o usuário usando funções

As funções tornam o código mais organizado, legível e fácil de manter, além de evitar repetição de código.

---

[🔙 Voltar ao índice principal](../README.md)

<img width=100% src="https://capsule-render.vercel.app/api?type=waving&color=A8B9CC&height=120&section=footer"/> 