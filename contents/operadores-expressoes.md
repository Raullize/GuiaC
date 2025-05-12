<img width=100% src="https://capsule-render.vercel.app/api?type=waving&color=A8B9CC&height=120&section=header"/>

# ➗ Operadores e Expressões

## 📋 Trabalhando com Operadores em C

Os operadores são símbolos especiais que realizam operações específicas em um ou mais operandos. Uma expressão é uma combinação de operadores e operandos que são avaliados para produzir um resultado.

### 📊 Operadores Aritméticos

Operadores aritméticos são usados para realizar operações matemáticas básicas:

| Operador | Descrição            | Exemplo     | Resultado |
|----------|----------------------|-------------|-----------|
| `+`      | Adição               | `5 + 3`     | `8`       |
| `-`      | Subtração            | `5 - 3`     | `2`       |
| `*`      | Multiplicação        | `5 * 3`     | `15`      |
| `/`      | Divisão              | `5 / 3`     | `1`       |
| `%`      | Módulo (resto)       | `5 % 3`     | `2`       |

**Observação**: A divisão entre inteiros em C resulta em um inteiro (truncado), como mostrado no exemplo de `5 / 3` que resulta em `1`.

```c
#include <stdio.h>

int main() {
    int a = 10, b = 3;
    
    printf("Adição: %d + %d = %d\n", a, b, a + b);        // 13
    printf("Subtração: %d - %d = %d\n", a, b, a - b);     // 7
    printf("Multiplicação: %d * %d = %d\n", a, b, a * b); // 30
    printf("Divisão: %d / %d = %d\n", a, b, a / b);       // 3
    printf("Módulo: %d %% %d = %d\n", a, b, a % b);       // 1
    
    // Exemplo com ponto flutuante
    float x = 10.0f, y = 3.0f;
    printf("Divisão real: %.1f / %.1f = %.2f\n", x, y, x / y);  // 3.33
    
    return 0;
}
```

### 👆 Operadores de Incremento e Decremento

C fornece operadores especiais para incrementar ou decrementar o valor de uma variável em 1:

| Operador | Descrição             | Exemplo       | Equivalente a |
|----------|----------------------|---------------|---------------|
| `++`     | Incremento           | `i++` ou `++i`| `i = i + 1`   |
| `--`     | Decremento           | `i--` ou `--i`| `i = i - 1`   |

Existem duas formas para cada um:
- **Pré-incremento/decremento**: `++i`, `--i` (incrementa/decrementa antes de usar o valor)
- **Pós-incremento/decremento**: `i++`, `i--` (incrementa/decrementa após usar o valor)

```c
#include <stdio.h>

int main() {
    int a = 5, b = 5;
    int result;
    
    // Pós-incremento: o valor original é usado na expressão, depois incrementado
    result = a++;
    printf("result = a++ resulta em result=%d, a=%d\n", result, a);  // result=5, a=6
    
    // Pré-incremento: o valor é incrementado primeiro, depois usado na expressão
    result = ++b;
    printf("result = ++b resulta em result=%d, b=%d\n", result, b);  // result=6, b=6
    
    return 0;
}
```

### 🔄 Operadores de Atribuição

Os operadores de atribuição são usados para atribuir valores a variáveis:

| Operador | Descrição                      | Exemplo     | Equivalente a  |
|----------|--------------------------------|-------------|----------------|
| `=`      | Atribuição simples             | `a = b`     | `a = b`        |
| `+=`     | Atribuição com adição          | `a += b`    | `a = a + b`    |
| `-=`     | Atribuição com subtração       | `a -= b`    | `a = a - b`    |
| `*=`     | Atribuição com multiplicação   | `a *= b`    | `a = a * b`    |
| `/=`     | Atribuição com divisão         | `a /= b`    | `a = a / b`    |
| `%=`     | Atribuição com módulo          | `a %= b`    | `a = a % b`    |
| `<<=`    | Atribuição com shift left      | `a <<= b`   | `a = a << b`   |
| `>>=`    | Atribuição com shift right     | `a >>= b`   | `a = a >> b`   |
| `&=`     | Atribuição com AND bit a bit   | `a &= b`    | `a = a & b`    |
| `^=`     | Atribuição com XOR bit a bit   | `a ^= b`    | `a = a ^ b`    |
| `|=`     | Atribuição com OR bit a bit    | `a |= b`    | `a = a | b`    |

```c
#include <stdio.h>

int main() {
    int a = 10;
    
    printf("Valor inicial: a = %d\n", a);         // 10
    
    a += 5;  // Equivalente a: a = a + 5
    printf("Após a += 5: a = %d\n", a);           // 15
    
    a -= 3;  // Equivalente a: a = a - 3
    printf("Após a -= 3: a = %d\n", a);           // 12
    
    a *= 2;  // Equivalente a: a = a * 2
    printf("Após a *= 2: a = %d\n", a);           // 24
    
    a /= 3;  // Equivalente a: a = a / 3
    printf("Após a /= 3: a = %d\n", a);           // 8
    
    a %= 5;  // Equivalente a: a = a % 5
    printf("Após a %%= 5: a = %d\n", a);          // 3
    
    return 0;
}
```

### 📏 Operadores de Comparação (Relacionais)

Operadores de comparação são usados para comparar dois valores:

| Operador | Descrição               | Exemplo  | Resultado se `a=5, b=3` |
|----------|-------------------------|----------|-----------------------|
| `==`     | Igual a                 | `a == b` | `0` (falso)           |
| `!=`     | Diferente de            | `a != b` | `1` (verdadeiro)      |
| `>`      | Maior que               | `a > b`  | `1` (verdadeiro)      |
| `<`      | Menor que               | `a < b`  | `0` (falso)           |
| `>=`     | Maior ou igual a        | `a >= b` | `1` (verdadeiro)      |
| `<=`     | Menor ou igual a        | `a <= b` | `0` (falso)           |

Em C, o resultado de uma expressão de comparação é `1` se for verdadeira e `0` se for falsa.

```c
#include <stdio.h>

int main() {
    int a = 5, b = 3;
    
    printf("%d == %d: %d\n", a, b, a == b);  // 0 (falso)
    printf("%d != %d: %d\n", a, b, a != b);  // 1 (verdadeiro)
    printf("%d > %d: %d\n", a, b, a > b);    // 1 (verdadeiro)
    printf("%d < %d: %d\n", a, b, a < b);    // 0 (falso)
    printf("%d >= %d: %d\n", a, b, a >= b);  // 1 (verdadeiro)
    printf("%d <= %d: %d\n", a, b, a <= b);  // 0 (falso)
    
    return 0;
}
```

### 🔣 Operadores Lógicos

Operadores lógicos são usados para combinar expressões condicionais:

| Operador | Descrição                  | Exemplo      | Resultado se `a=1, b=0` |
|----------|----------------------------|--------------|------------------------|
| `&&`     | AND lógico (E)             | `a && b`     | `0` (falso)            |
| `||`     | OR lógico (OU)             | `a || b`     | `1` (verdadeiro)       |
| `!`      | NOT lógico (NÃO)           | `!a`         | `0` (falso)            |

Em C, qualquer valor diferente de zero é considerado verdadeiro, e zero é considerado falso.

```c
#include <stdio.h>

int main() {
    int a = 1;  // verdadeiro
    int b = 0;  // falso
    
    // AND lógico (&&) - verdadeiro somente se ambos operandos forem verdadeiros
    printf("%d && %d = %d\n", a, b, a && b);  // 0 (falso)
    
    // OR lógico (||) - verdadeiro se pelo menos um operando for verdadeiro
    printf("%d || %d = %d\n", a, b, a || b);  // 1 (verdadeiro)
    
    // NOT lógico (!) - inverte o valor lógico
    printf("!%d = %d\n", a, !a);  // 0 (falso)
    printf("!%d = %d\n", b, !b);  // 1 (verdadeiro)
    
    // Expressões compostas
    int x = 5, y = 10, z = 15;
    int resultado = (x < y) && (y < z);
    printf("(x < y) && (y < z) = %d\n", resultado);  // 1 (verdadeiro)
    
    return 0;
}
```

### 🧮 Operadores Bit a Bit (Bitwise)

Operadores bit a bit operam nos bits individuais dos operandos:

| Operador | Descrição                | Exemplo   | Resultado (em binário) se `a=5 (101), b=3 (011)` |
|----------|--------------------------|-----------|------------------------------------------------|
| `&`      | AND bit a bit            | `a & b`   | `1 (001)`                                      |
| `|`      | OR bit a bit             | `a | b`   | `7 (111)`                                      |
| `^`      | XOR bit a bit            | `a ^ b`   | `6 (110)`                                      |
| `~`      | NOT bit a bit (complemento) | `~a`   | `-6 (complemento de 2)`                        |
| `<<`     | Shift left               | `a << 1`  | `10 (1010)`                                    |
| `>>`     | Shift right              | `a >> 1`  | `2 (010)`                                      |

```c
#include <stdio.h>

int main() {
    unsigned char a = 5;  // 00000101 em binário
    unsigned char b = 3;  // 00000011 em binário
    
    printf("a = %d (binário: %08b)\n", a, a);  // a = 5
    printf("b = %d (binário: %08b)\n", b, b);  // b = 3
    
    // AND bit a bit: bits são 1 somente se ambos bits correspondentes forem 1
    printf("a & b = %d (binário: %08b)\n", a & b, a & b);  // 1 (00000001)
    
    // OR bit a bit: bits são 1 se pelo menos um dos bits correspondentes for 1
    printf("a | b = %d (binário: %08b)\n", a | b, a | b);  // 7 (00000111)
    
    // XOR bit a bit: bits são 1 se os bits correspondentes forem diferentes
    printf("a ^ b = %d (binário: %08b)\n", a ^ b, a ^ b);  // 6 (00000110)
    
    // NOT bit a bit (complemento): inverte todos os bits
    printf("~a = %d (binário: %08b)\n", (unsigned char)~a, (unsigned char)~a);  // 250 (11111010)
    
    // Shift left: desloca bits para a esquerda (multiplica por 2^n)
    printf("a << 1 = %d (binário: %08b)\n", a << 1, a << 1);  // 10 (00001010)
    
    // Shift right: desloca bits para a direita (divide por 2^n)
    printf("a >> 1 = %d (binário: %08b)\n", a >> 1, a >> 1);  // 2 (00000010)
    
    return 0;
}
```

**Observação**: O exemplo acima usa o formato de impressão `%08b`, que não é padrão em C. Na prática, você precisaria de uma função auxiliar para imprimir o valor em formato binário.

### 🔍 Operadores de Tamanho e Endereço

| Operador | Descrição                     | Exemplo     | Resultado                         |
|----------|-------------------------------|-------------|-----------------------------------|
| `sizeof` | Tamanho em bytes              | `sizeof(int)` | `4` (depende da plataforma)    |
| `&`      | Operador de endereço          | `&a`       | Endereço de memória da variável a |
| `*`      | Operador de desreferenciação  | `*ptr`     | Valor no endereço apontado por ptr|

```c
#include <stdio.h>

int main() {
    int a = 10;
    int *ptr = &a;  // ptr armazena o endereço de a
    
    printf("Valor de a: %d\n", a);                     // 10
    printf("Endereço de a: %p\n", (void*)&a);          // 0x...
    printf("Valor de ptr (endereço de a): %p\n", (void*)ptr);  // 0x...
    printf("Valor apontado por ptr (*ptr): %d\n", *ptr);       // 10
    
    printf("Tamanho de int: %zu bytes\n", sizeof(int));        // 4 (tipicamente)
    printf("Tamanho de float: %zu bytes\n", sizeof(float));    // 4 (tipicamente)
    printf("Tamanho de char: %zu bytes\n", sizeof(char));      // 1
    printf("Tamanho de double: %zu bytes\n", sizeof(double));  // 8 (tipicamente)
    printf("Tamanho da variável a: %zu bytes\n", sizeof(a));   // 4 (tipicamente)
    
    return 0;
}
```

### 🔄 Operador Condicional Ternário

O operador ternário `? :` é o único operador em C que aceita três operandos:

```
condição ? expressão1 : expressão2
```

Se a condição for verdadeira, a expressão1 é avaliada e se torna o resultado; caso contrário, a expressão2 é avaliada e se torna o resultado.

```c
#include <stdio.h>

int main() {
    int a = 10;
    int b = 20;
    
    // Usando operador ternário para encontrar o maior valor
    int max = (a > b) ? a : b;
    printf("O maior valor entre %d e %d é: %d\n", a, b, max);  // 20
    
    // Equivalente usando if-else
    int max2;
    if (a > b) {
        max2 = a;
    } else {
        max2 = b;
    }
    printf("O maior valor entre %d e %d é: %d\n", a, b, max2);  // 20
    
    // Exemplo com expressões mais complexas
    int idade = 18;
    printf("Você %s beber legalmente nos EUA.\n", 
           (idade >= 21) ? "pode" : "não pode");  // não pode
    
    return 0;
}
```

### 🔄 Operador Vírgula

O operador vírgula (`,`) permite avaliar múltiplas expressões onde apenas uma é esperada. As expressões são avaliadas da esquerda para a direita, e o valor da expressão mais à direita se torna o valor da expressão composta.

```c
#include <stdio.h>

int main() {
    int a, b, c;
    
    // A vírgula aqui é apenas um separador, não o operador vírgula
    
    // Usando o operador vírgula em uma expressão for
    for (a = 1, b = 10; a <= 5; a++, b += 10) {
        printf("a = %d, b = %d\n", a, b);
    }
    
    // Usando o operador vírgula em uma atribuição
    c = (a = 3, b = a + 2, a + b);
    printf("c = %d (a = %d, b = %d)\n", c, a, b);  // c = 8, a = 3, b = 5
    
    return 0;
}
```

### 📊 Precedência de Operadores

A precedência dos operadores determina a ordem na qual as operações são realizadas em uma expressão. Operadores com maior precedência são avaliados antes dos operadores com menor precedência.

| Precedência | Operador                          | Associatividade |
|-------------|------------------------------------|----------------|
| Maior       | `()` `[]` `->` `.`                | Esquerda para direita |
|             | `!` `~` `++` `--` `+` `-` (unário) `&` (endereço) `*` (ponteiro) `sizeof` | Direita para esquerda |
|             | `*` `/` `%`                       | Esquerda para direita |
|             | `+` `-` (binário)                 | Esquerda para direita |
|             | `<<` `>>`                         | Esquerda para direita |
|             | `<` `<=` `>` `>=`                 | Esquerda para direita |
|             | `==` `!=`                         | Esquerda para direita |
|             | `&` (bit a bit AND)               | Esquerda para direita |
|             | `^` (bit a bit XOR)               | Esquerda para direita |
|             | `|` (bit a bit OR)                | Esquerda para direita |
|             | `&&` (lógico AND)                 | Esquerda para direita |
|             | `||` (lógico OR)                  | Esquerda para direita |
|             | `?:` (ternário)                   | Direita para esquerda |
|             | `=` `+=` `-=` `*=` `/=` `%=` `&=` `^=` `|=` `<<=` `>>=` | Direita para esquerda |
| Menor       | `,` (vírgula)                     | Esquerda para direita |

```c
#include <stdio.h>

int main() {
    int a = 5, b = 3, c = 8;
    int result;
    
    // Demonstração de precedência
    result = a + b * c;        // b * c é calculado primeiro, depois é adicionado a
    printf("a + b * c = %d\n", result);  // 5 + (3 * 8) = 5 + 24 = 29
    
    result = (a + b) * c;      // a + b é calculado primeiro (devido aos parênteses), depois multiplicado por c
    printf("(a + b) * c = %d\n", result);  // (5 + 3) * 8 = 8 * 8 = 64
    
    // Mais exemplos
    result = a + b - c;       // Da esquerda para a direita devido à mesma precedência
    printf("a + b - c = %d\n", result);  // (5 + 3) - 8 = 8 - 8 = 0
    
    result = a * b + c / 2;   // Primeiro a * b e c / 2, depois a soma
    printf("a * b + c / 2 = %d\n", result);  // (5 * 3) + (8 / 2) = 15 + 4 = 19
    
    // Combinação de operadores lógicos e relacionais
    int d = 1;
    result = a > b && c > d;  // Primeiro as comparações, depois o AND lógico
    printf("a > b && c > d = %d\n", result);  // (5 > 3) && (8 > 1) = 1 && 1 = 1
    
    return 0;
}
```

### 🧪 Conversão de Tipos (Casting)

Em C, existem dois tipos de conversão de tipos:

1. **Conversão Implícita**: Ocorre automaticamente quando um valor é usado em um contexto que requer outro tipo.
2. **Conversão Explícita (Casting)**: É feita manualmente pelo programador utilizando o operador de casting.

```c
#include <stdio.h>

int main() {
    int i = 10;
    float f = 3.5;
    
    // Conversão implícita
    float resultado1 = i + f;    // i é convertido para float antes da adição
    printf("%d + %.1f = %.1f\n", i, f, resultado1);  // 10 + 3.5 = 13.5
    
    // Divisão entre inteiros
    int a = 5, b = 2;
    float resultado2 = a / b;    // a divisão ocorre entre inteiros, resultando em 2
    printf("%d / %d = %.1f\n", a, b, resultado2);  // 5 / 2 = 2.0
    
    // Conversão explícita (cast)
    float resultado3 = (float)a / b;  // a é explicitamente convertido para float antes da divisão
    printf("(float)%d / %d = %.1f\n", a, b, resultado3);  // (float)5 / 2 = 2.5
    
    // Outros exemplos de cast
    int x = 7;
    int y = 2;
    double resultado4 = (double)x / y;
    printf("(double)%d / %d = %.1f\n", x, y, resultado4);  // (double)7 / 2 = 3.5
    
    // Truncamento ao converter float para int
    float valor = 9.7;
    int valorInt = (int)valor;  // O valor é truncado, não arredondado
    printf("(int)%.1f = %d\n", valor, valorInt);  // (int)9.7 = 9
    
    return 0;
}
```

### ⚙️ Expressões de Avaliação

Uma expressão é uma sequência de operadores e operandos que especifica um cálculo. Expressões podem ser:

1. **Aritméticas**: Resultam em um valor numérico (`a + b * c`)
2. **Relacionais**: Resultam em verdadeiro ou falso (`a > b`)
3. **Lógicas**: Combinam expressões relacionais (`(a > b) && (c < d)`)
4. **De atribuição**: Atribuem valores a variáveis (`a = b + c`)

```c
#include <stdio.h>

int main() {
    int a = 5, b = 3, c = 10;
    int resultado;
    
    // Expressão aritmética
    resultado = a + b * c / 2 - 1;
    printf("a + b * c / 2 - 1 = %d\n", resultado);  // 5 + 3 * 10 / 2 - 1 = 5 + 15 - 1 = 19
    
    // Expressão relacional
    int ehMaior = a > b;
    printf("a > b = %d\n", ehMaior);  // 1 (verdadeiro)
    
    // Expressão lógica
    int logico = (a > b) && (c > a);
    printf("(a > b) && (c > a) = %d\n", logico);  // 1 (verdadeiro)
    
    // Expressões de atribuição
    a += 2;  // a = a + 2
    printf("Após a += 2, a = %d\n", a);  // 7
    
    // Expressão com efeitos colaterais
    int d = 1;
    resultado = a + (d += 2);  // d é incrementado, depois somado a 'a'
    printf("a + (d += 2) = %d, d = %d\n", resultado, d);  // 10, d = 3
    
    return 0;
}
```

### 🚫 Erros Comuns com Operadores

1. **Confundir `=` (atribuição) com `==` (comparação)**:
   ```c
   if (a = 5) {  // Atribui 5 a 'a' e verifica se é não-zero (sempre verdadeiro)
       // Código executado sempre
   }
   // Correto: if (a == 5)
   ```

2. **Divisão inteira inesperada**:
   ```c
   float resultado = 5 / 2;       // Resultado é 2.0, não 2.5
   // Correto: float resultado = 5.0 / 2 ou (float)5 / 2
   ```

3. **Avaliação de curto-circuito mal interpretada**:
   ```c
   if (ptr != NULL && ptr->valor > 10) {
       // Código seguro: se ptr for NULL, a segunda parte não é avaliada
   }
   
   if (ptr->valor > 10 && ptr != NULL) {
       // PERIGO: se ptr for NULL, a primeira verificação causará erro
   }
   ```

4. **Precedência de operadores não considerada**:
   ```c
   int resultado = a + b * c;      // Pode não fazer o que você espera
   // Se a ordem desejada for diferente: int resultado = (a + b) * c;
   ```

5. **Efeitos colaterais de incremento/decremento**:
   ```c
   int a = 5;
   printf("%d %d\n", a++, a++);  // Comportamento indefinido!
   ```

### ⚡ Resumo dos Operadores em C

```
┌─────────────────────────────────┬───────────────────────┐
│ Categoria                        │ Operadores            │
├─────────────────────────────────┼───────────────────────┤
│ Aritméticos                      │ + - * / %            │
│ Incremento/Decremento            │ ++ --                │
│ Relacionais                      │ == != > < >= <=      │
│ Lógicos                          │ && || !              │
│ Bit a bit                        │ & | ^ ~ << >>        │
│ Atribuição                       │ = += -= *= /= %=     │
│                                  │ &= |= ^= <<= >>=     │
│ Tamanho e Endereço               │ sizeof & *           │
│ Condicional                      │ ?:                   │
│ Vírgula                          │ ,                    │
│ Acesso a Membros de Estrutura    │ . ->                 │
└─────────────────────────────────┴───────────────────────┘
```

---

[🔙 Voltar ao índice principal](../README.md)

<img width=100% src="https://capsule-render.vercel.app/api?type=waving&color=A8B9CC&height=120&section=footer"/> 