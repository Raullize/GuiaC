<img width=100% src="https://capsule-render.vercel.app/api?type=waving&color=A8B9CC&height=120&section=header"/>

# 📌 Tipos de Dados

## 📋 Entendendo os Tipos de Dados em C

Os tipos de dados em C definem a natureza dos valores que uma variável pode armazenar e as operações que podem ser realizadas sobre eles. A linguagem C é fortemente tipada, o que significa que cada variável deve ter um tipo definido, e esse tipo determina como o valor será armazenado na memória.

### 🔢 Tipos Primitivos em C

C possui um conjunto de tipos de dados fundamentais, conhecidos como tipos primitivos:

#### 1️⃣ Tipos Inteiros

Os tipos inteiros armazenam números sem partes fracionárias:

| Tipo | Tamanho Típico | Faixa de Valores | Formato |
|------|----------------|------------------|---------|
| `char` | 1 byte | -128 a 127 ou 0 a 255 | `%c` (caractere) ou `%d` (valor) |
| `unsigned char` | 1 byte | 0 a 255 | `%c` ou `%u` |
| `signed char` | 1 byte | -128 a 127 | `%c` ou `%d` |
| `int` | 4 bytes | -2,147,483,648 a 2,147,483,647 | `%d` |
| `unsigned int` | 4 bytes | 0 a 4,294,967,295 | `%u` |
| `short` ou `short int` | 2 bytes | -32,768 a 32,767 | `%hd` |
| `unsigned short` | 2 bytes | 0 a 65,535 | `%hu` |
| `long` ou `long int` | 4-8 bytes | -2,147,483,648 a 2,147,483,647 (ou maior) | `%ld` |
| `unsigned long` | 4-8 bytes | 0 a 4,294,967,295 (ou maior) | `%lu` |
| `long long` | 8 bytes | -9,223,372,036,854,775,808 a 9,223,372,036,854,775,807 | `%lld` |
| `unsigned long long` | 8 bytes | 0 a 18,446,744,073,709,551,615 | `%llu` |

**Observação**: O tamanho exato pode variar dependendo da arquitetura e do compilador.

```c
#include <stdio.h>

int main() {
    char c = 'A';
    unsigned char uc = 255;
    int i = 42;
    unsigned int ui = 3000000000;
    short s = 32767;
    long l = 2147483647;
    long long ll = 9223372036854775807LL;
    
    printf("char: %c (%d)\n", c, c);
    printf("unsigned char: %u\n", uc);
    printf("int: %d\n", i);
    printf("unsigned int: %u\n", ui);
    printf("short: %hd\n", s);
    printf("long: %ld\n", l);
    printf("long long: %lld\n", ll);
    
    return 0;
}
```

#### 2️⃣ Tipos de Ponto Flutuante

Os tipos de ponto flutuante armazenam números com partes fracionárias:

| Tipo | Tamanho | Precisão | Formato |
|------|---------|----------|---------|
| `float` | 4 bytes | 6-7 dígitos decimais | `%f` |
| `double` | 8 bytes | 15-16 dígitos decimais | `%lf` |
| `long double` | 8-16 bytes | 18-19 dígitos decimais | `%Lf` |

```c
#include <stdio.h>

int main() {
    float f = 3.14159f;
    double d = 3.14159265358979;
    long double ld = 3.14159265358979323846L;
    
    printf("float: %f\n", f);
    printf("double: %.15lf\n", d);
    printf("long double: %.18Lf\n", ld);
    
    return 0;
}
```

#### 3️⃣ O Tipo `void`

O tipo `void` é um tipo especial que indica a ausência de valor:

- **Funções sem retorno**: `void funcao()`
- **Ponteiros genéricos**: `void* ptr`
- **Funções sem parâmetros**: `int funcao(void)`

```c
#include <stdio.h>

// Função sem retorno
void saudacao(void) {
    printf("Olá, mundo!\n");
}

// Função com retorno
int soma(int a, int b) {
    return a + b;
}

int main() {
    saudacao();
    
    int resultado = soma(5, 3);
    printf("5 + 3 = %d\n", resultado);
    
    // Ponteiro void (genérico)
    void* ptr;
    int num = 42;
    ptr = &num;
    printf("Valor: %d\n", *(int*)ptr);  // Necessário fazer cast
    
    return 0;
}
```

#### 4️⃣ Tipo Booleano (C99 e posterior)

Em C99, foi introduzido um tipo booleano através do cabeçalho `<stdbool.h>`:

```c
#include <stdio.h>
#include <stdbool.h>

int main() {
    bool verdadeiro = true;
    bool falso = false;
    
    printf("Verdadeiro: %d\n", verdadeiro);  // 1
    printf("Falso: %d\n", falso);            // 0
    
    if (verdadeiro) {
        printf("Condição é verdadeira!\n");
    }
    
    return 0;
}
```

Antes do C99, valores booleanos eram normalmente representados por inteiros, onde 0 é falso e qualquer valor diferente de 0 é verdadeiro.

### 🧬 Modificadores de Tipo

Os modificadores de tipo alteram o tamanho ou o comportamento dos tipos básicos:

- **signed**: Para números com sinal (positivos e negativos) - padrão para a maioria dos tipos
- **unsigned**: Para números não negativos (apenas positivos)
- **short**: Reduz o tamanho (e a faixa) de um tipo
- **long**: Aumenta o tamanho (e a faixa) de um tipo

```c
#include <stdio.h>
#include <limits.h>

int main() {
    printf("Tamanho e limites de tipos inteiros:\n");
    
    printf("short int: %lu bytes (%hd a %hd)\n", 
           sizeof(short int), SHRT_MIN, SHRT_MAX);
    
    printf("int: %lu bytes (%d a %d)\n", 
           sizeof(int), INT_MIN, INT_MAX);
    
    printf("long int: %lu bytes (%ld a %ld)\n", 
           sizeof(long int), LONG_MIN, LONG_MAX);
    
    printf("unsigned int: %lu bytes (0 a %u)\n", 
           sizeof(unsigned int), UINT_MAX);

    return 0;
}
```

### 📐 Tamanho dos Tipos de Dados

O operador `sizeof` é usado para determinar o tamanho (em bytes) de um tipo de dado ou variável:

```c
#include <stdio.h>

int main() {
    printf("Tamanho dos tipos básicos em bytes:\n");
    printf("char: %zu\n", sizeof(char));
    printf("short: %zu\n", sizeof(short));
    printf("int: %zu\n", sizeof(int));
    printf("long: %zu\n", sizeof(long));
    printf("long long: %zu\n", sizeof(long long));
    printf("float: %zu\n", sizeof(float));
    printf("double: %zu\n", sizeof(double));
    printf("long double: %zu\n", sizeof(long double));
    
    return 0;
}
```

**Observação**: Os tamanhos podem variar dependendo da arquitetura e do compilador.

### 🔄 Conversão de Tipos (Type Casting)

Em C, você pode converter um tipo de dado em outro usando conversão (cast):

#### 1. Conversão Implícita

C realiza algumas conversões automaticamente:

```c
int i = 10;
double d = i;  // Conversão implícita de int para double
```

#### 2. Conversão Explícita (Cast)

Você pode forçar uma conversão usando o operador de cast:

```c
double pi = 3.14159;
int arredondado = (int)pi;  // Conversão explícita de double para int, trunca para 3
```

```c
#include <stdio.h>

int main() {
    // Conversão implícita
    int i = 100;
    double d = i;  // int -> double
    
    printf("Inteiro: %d, Convertido para double: %f\n", i, d);
    
    // Conversão explícita (cast)
    double pi = 3.14159;
    int pi_inteiro = (int)pi;
    
    printf("Double: %f, Convertido para int: %d\n", pi, pi_inteiro);
    
    // Cuidado com perda de dados
    int grande = 1000000;
    char c = (char)grande;  // Perda de dados (overflow)
    
    printf("Inteiro grande: %d, Convertido para char: %d\n", grande, c);
    
    return 0;
}
```

### 📌 Constantes e Literais

Valores literais em C têm tipos implícitos:

- Inteiros: `123` (int), `123L` (long), `123LL` (long long), `123U` (unsigned)
- Ponto flutuante: `3.14` (double), `3.14F` (float), `3.14L` (long double)
- Caracteres: `'A'` (char)
- Strings: `"Olá"` (array de char)

```c
#include <stdio.h>

int main() {
    // Inteiros
    int normal = 42;
    unsigned int positivo = 42U;
    long grande = 42L;
    unsigned long grande_positivo = 42UL;
    long long muito_grande = 42LL;
    
    // Ponto flutuante
    float f = 3.14F;
    double d = 3.14;
    long double ld = 3.14L;
    
    // Bases diferentes
    int decimal = 42;       // Base 10
    int octal = 052;        // Base 8 (começa com 0)
    int hexadecimal = 0x2A; // Base 16 (começa com 0x)
    int binario = 0b101010; // Base 2 (começa com 0b, C99 e posterior)
    
    printf("Decimal: %d\n", decimal);
    printf("Octal: %o (%d)\n", octal, octal);
    printf("Hexadecimal: %x (%d)\n", hexadecimal, hexadecimal);
    printf("Binário como decimal: %d\n", binario);
    
    return 0;
}
```

### 🧠 Tipos Definidos pelo Usuário

C permite criar seus próprios tipos usando `typedef`:

```c
#include <stdio.h>

// Cria um alias para unsigned int
typedef unsigned int uint;

// Cria um alias para um tipo complexo
typedef struct {
    double x;
    double y;
} Ponto;

int main() {
    uint contador = 42;
    printf("Contador: %u\n", contador);
    
    Ponto p;
    p.x = 10.5;
    p.y = 20.7;
    printf("Ponto: (%.1f, %.1f)\n", p.x, p.y);
    
    return 0;
}
```

### 🔄 Tipos Enumerados

Os enumerados permitem criar um conjunto de constantes nomeadas:

```c
#include <stdio.h>

// Enumeração básica
enum DiaDaSemana {
    DOMINGO,    // 0
    SEGUNDA,    // 1
    TERCA,      // 2
    QUARTA,     // 3
    QUINTA,     // 4
    SEXTA,      // 5
    SABADO      // 6
};

// Enumeração com valores específicos
enum Mes {
    JANEIRO = 1,
    FEVEREIRO,   // 2
    MARCO,       // 3
    ABRIL,       // 4
    MAIO,        // 5
    JUNHO,       // 6
    JULHO,       // 7
    AGOSTO,      // 8
    SETEMBRO,    // 9
    OUTUBRO,     // 10
    NOVEMBRO,    // 11
    DEZEMBRO     // 12
};

int main() {
    enum DiaDaSemana hoje = QUARTA;
    enum Mes mes_atual = OUTUBRO;
    
    printf("Hoje é o dia %d da semana\n", hoje);
    printf("Estamos no mês %d\n", mes_atual);
    
    return 0;
}
```

### 🔍 Limitações e Melhores Práticas

1. **Overflow e Underflow**: Sempre verifique se o tipo escolhido pode armazenar a faixa de valores necessária.

```c
#include <stdio.h>
#include <limits.h>

int main() {
    short s = 32767;  // Valor máximo para short
    printf("s = %hd\n", s);
    
    s = s + 1;  // Overflow
    printf("s + 1 = %hd\n", s);  // -32768 (wraparound)
    
    unsigned char c = 255;
    printf("c = %d\n", c);
    
    c = c + 1;  // Overflow
    printf("c + 1 = %d\n", c);  // 0 (wraparound)
    
    return 0;
}
```

2. **Precisão**: Fique atento à precisão dos tipos de ponto flutuante.

```c
#include <stdio.h>

int main() {
    float f = 0.1f + 0.2f;
    double d = 0.1 + 0.2;
    
    printf("float: %.20f\n", f);   // Imprecisão
    printf("double: %.20lf\n", d); // Melhor precisão, mas ainda não exata
    
    // Teste de igualdade com problema
    if (f == 0.3f) {
        printf("f é igual a 0.3\n");
    } else {
        printf("f NÃO é igual a 0.3\n");
    }
    
    return 0;
}
```

3. **Portabilidade**: Use tipos com tamanhos definidos para maior portabilidade.

```c
#include <stdio.h>
#include <stdint.h>  // Tipos com tamanhos definidos (C99 e posterior)

int main() {
    int32_t i32 = 42;      // Inteiro de 32 bits
    uint64_t ui64 = 12345; // Inteiro sem sinal de 64 bits
    int_least16_t i16 = 1000; // Pelo menos 16 bits
    
    printf("int32_t: %d (%zu bytes)\n", i32, sizeof(i32));
    printf("uint64_t: %llu (%zu bytes)\n", ui64, sizeof(ui64));
    printf("int_least16_t: %d (%zu bytes)\n", i16, sizeof(i16));
    
    return 0;
}
```

### 📊 Tabela Comparativa de Usos Comuns

| Tipo de Dado | Uso Recomendado |
|--------------|-----------------|
| `int` | Operações gerais com números inteiros |
| `char` | Caracteres individuais e valores pequenos |
| `float` | Números de ponto flutuante quando a precisão não é crítica |
| `double` | Cálculos de ponto flutuante com precisão |
| `unsigned int` | Contadores e valores não negativos |
| `size_t` | Tamanhos e índices (resultado de `sizeof`) |
| `int32_t`, `uint64_t`, etc. | Quando o tamanho exato do tipo é importante |
| `bool` | Valores lógicos (verdadeiro/falso) |

### 🔍 Exemplos Práticos de Uso

```c
#include <stdio.h>
#include <stdbool.h>
#include <stdint.h>

// Simulação de notas de alunos
int main() {
    // Tipos apropriados para cada dado
    char nome[50] = "João Silva";
    uint8_t idade = 20;            // 0-255 é suficiente para idade
    float nota_prova1 = 8.5;       // Notas com uma casa decimal
    float nota_prova2 = 9.25;
    double media = (nota_prova1 + nota_prova2) / 2.0;
    bool aprovado = media >= 7.0;  // Valor lógico
    
    // Exibição dos dados
    printf("Aluno: %s\n", nome);
    printf("Idade: %u anos\n", idade);
    printf("Nota Prova 1: %.2f\n", nota_prova1);
    printf("Nota Prova 2: %.2f\n", nota_prova2);
    printf("Média: %.2f\n", media);
    printf("Situação: %s\n", aprovado ? "Aprovado" : "Reprovado");
    
    return 0;
}
```

---

[🔙 Voltar ao índice principal](../README.md)

<img width=100% src="https://capsule-render.vercel.app/api?type=waving&color=A8B9CC&height=120&section=footer"/> 