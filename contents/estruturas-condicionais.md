<img width=100% src="https://capsule-render.vercel.app/api?type=waving&color=A8B9CC&height=120&section=header"/>

# ⚡ Estruturas Condicionais

## 📋 Tomada de Decisões em C

As estruturas condicionais permitem que seu programa tome decisões com base em condições. Elas permitem executar diferentes blocos de código dependendo se uma condição específica é verdadeira ou falsa.

### 🔍 Conceitos Básicos

Em C, os valores são considerados da seguinte forma:
- **Falso**: Valor zero (`0`)
- **Verdadeiro**: Qualquer valor diferente de zero (geralmente `1`)

### 📏 Instrução `if`

A instrução `if` é a forma mais básica de controle condicional:

```c
if (condição) {
    // Código executado se a condição for verdadeira
}
```

Exemplo:

```c
#include <stdio.h>

int main() {
    int idade = 18;
    
    if (idade >= 18) {
        printf("Você é maior de idade.\n");
    }
    
    return 0;
}
```

### 🔄 Instrução `if-else`

A instrução `if-else` permite executar um bloco de código quando a condição é verdadeira e outro bloco quando é falsa:

```c
if (condição) {
    // Código executado se a condição for verdadeira
} else {
    // Código executado se a condição for falsa
}
```

Exemplo:

```c
#include <stdio.h>

int main() {
    int idade = 16;
    
    if (idade >= 18) {
        printf("Você é maior de idade.\n");
    } else {
        printf("Você é menor de idade.\n");
    }
    
    return 0;
}
```

### 🌟 Instrução `if-else if-else`

Para testar múltiplas condições em sequência:

```c
if (condição1) {
    // Código executado se condição1 for verdadeira
} else if (condição2) {
    // Código executado se condição1 for falsa e condição2 for verdadeira
} else if (condição3) {
    // Código executado se condição1 e condição2 forem falsas e condição3 for verdadeira
} else {
    // Código executado se todas as condições anteriores forem falsas
}
```

Exemplo:

```c
#include <stdio.h>

int main() {
    int nota = 75;
    
    if (nota >= 90) {
        printf("Conceito A\n");
    } else if (nota >= 80) {
        printf("Conceito B\n");
    } else if (nota >= 70) {
        printf("Conceito C\n");
    } else if (nota >= 60) {
        printf("Conceito D\n");
    } else {
        printf("Conceito F\n");
    }
    
    return 0;
}
```

### 🎭 Instrução `if` Aninhada

É possível aninhar (colocar uma dentro da outra) instruções `if`:

```c
if (condição1) {
    if (condição2) {
        // Código executado se ambas condição1 e condição2 forem verdadeiras
    } else {
        // Código executado se condição1 for verdadeira e condição2 for falsa
    }
} else {
    // Código executado se condição1 for falsa
}
```

Exemplo:

```c
#include <stdio.h>

int main() {
    int idade = 20;
    int temCarteira = 1;  // 1 representa verdadeiro
    
    if (idade >= 18) {
        if (temCarteira) {
            printf("Você pode dirigir.\n");
        } else {
            printf("Você tem idade suficiente, mas precisa de uma carteira de motorista.\n");
        }
    } else {
        printf("Você é muito jovem para dirigir.\n");
    }
    
    return 0;
}
```

### 🔀 Instrução `switch`

A instrução `switch` é útil quando você precisa comparar uma variável com múltiplos valores possíveis:

```c
switch (expressão) {
    case valor1:
        // Código executado se expressão == valor1
        break;
    case valor2:
        // Código executado se expressão == valor2
        break;
    // Outros casos...
    default:
        // Código executado se nenhum dos casos corresponder
}
```

Exemplo:

```c
#include <stdio.h>

int main() {
    int diaSemana = 3;
    
    switch (diaSemana) {
        case 1:
            printf("Domingo\n");
            break;
        case 2:
            printf("Segunda-feira\n");
            break;
        case 3:
            printf("Terça-feira\n");
            break;
        case 4:
            printf("Quarta-feira\n");
            break;
        case 5:
            printf("Quinta-feira\n");
            break;
        case 6:
            printf("Sexta-feira\n");
            break;
        case 7:
            printf("Sábado\n");
            break;
        default:
            printf("Dia inválido\n");
    }
    
    return 0;
}
```

#### 🔑 Pontos Importantes sobre `switch`

1. A expressão no `switch` deve ser um valor inteiro (ou um tipo que possa ser promovido para inteiro, como `char`).
2. O `break` é necessário para evitar que a execução "caia" para o próximo caso.
3. O `default` é opcional e funciona como um "caso contrário".
4. Múltiplos casos podem compartilhar o mesmo código:

```c
#include <stdio.h>

int main() {
    char vogal = 'E';
    
    switch (vogal) {
        case 'A':
        case 'E':
        case 'I':
        case 'O':
        case 'U':
        case 'a':
        case 'e':
        case 'i':
        case 'o':
        case 'u':
            printf("É uma vogal.\n");
            break;
        default:
            printf("Não é uma vogal.\n");
    }
    
    return 0;
}
```

#### 🧩 Fall-Through (Omissão do `break`)

Quando o `break` é omitido, o fluxo "cai" para o próximo caso. Isso pode ser útil em alguns cenários, mas geralmente é um erro se não for intencional:

```c
#include <stdio.h>

int main() {
    int x = 2;
    
    switch (x) {
        case 1:
            printf("Um\n");
            // Sem break - o código "cai" para o próximo caso
        case 2:
            printf("Dois\n");
            // Sem break - o código "cai" para o próximo caso
        case 3:
            printf("Três\n");
            break;
        case 4:
            printf("Quatro\n");
            break;
    }
    
    return 0;
}
```

Este código imprime:
```
Dois
Três
```

### 🔄 Operador Ternário

O operador ternário `? :` é uma forma concisa de expressar decisões simples:

```c
condição ? expressão1 : expressão2
```

Se a condição for verdadeira, a expressão1 é avaliada; caso contrário, a expressão2 é avaliada.

Exemplo:

```c
#include <stdio.h>

int main() {
    int idade = 20;
    
    // Usando o operador ternário
    printf("Você %s beber legalmente nos EUA.\n", idade >= 21 ? "pode" : "não pode");
    
    // Equivalente usando if-else
    if (idade >= 21) {
        printf("Você pode beber legalmente nos EUA.\n");
    } else {
        printf("Você não pode beber legalmente nos EUA.\n");
    }
    
    // Usando o operador ternário para atribuir valor
    int maioridade = idade >= 18 ? 1 : 0;
    printf("Maior de idade: %d\n", maioridade);
    
    return 0;
}
```

### 🧪 Operadores Lógicos em Condições

Os operadores lógicos permitem criar condições mais complexas:

| Operador | Descrição     | Exemplo          |
|----------|---------------|------------------|
| `&&`     | E lógico      | `a > 0 && b > 0` |
| `||`     | OU lógico     | `a > 0 || b > 0` |
| `!`      | NÃO lógico    | `!ehValido`      |

Exemplo:

```c
#include <stdio.h>

int main() {
    int idade = 25;
    int temCarteira = 1;  // 1 representa verdadeiro
    int temCarro = 0;     // 0 representa falso
    
    // Usando E lógico (&&)
    if (idade >= 18 && temCarteira) {
        printf("Você está legalmente autorizado a dirigir.\n");
    }
    
    // Usando OU lógico (||)
    if (temCarro || temDinheiro) {
        printf("Você pode se locomover.\n");
    }
    
    // Usando NÃO lógico (!)
    if (!temCarro) {
        printf("Você não tem um carro.\n");
    }
    
    // Combinando operadores lógicos
    if ((idade >= 18 && temCarteira) && !temCarro) {
        printf("Você pode dirigir, mas não tem um carro.\n");
    }
    
    return 0;
}
```

#### 🔑 Avaliação de Curto-Circuito

Os operadores `&&` e `||` usam avaliação de curto-circuito:

- Em `expr1 && expr2`: Se `expr1` for falsa, `expr2` nem é avaliada, pois o resultado já será falso.
- Em `expr1 || expr2`: Se `expr1` for verdadeira, `expr2` nem é avaliada, pois o resultado já será verdadeiro.

```c
#include <stdio.h>

int main() {
    int a = 5;
    int b = 0;  // Divisor zero
    
    // Avaliação de curto-circuito previne divisão por zero
    if (b != 0 && a / b > 2) {
        printf("Resultado maior que 2\n");
    } else {
        printf("Condição falsa ou divisão por zero evitada\n");
    }
    
    return 0;
}
```

### 🧮 Expressões Relacionais

Operadores relacionais são usados para comparar valores:

| Operador | Descrição               | Exemplo  |
|----------|-------------------------|----------|
| `==`     | Igual a                 | `a == b` |
| `!=`     | Diferente de            | `a != b` |
| `<`      | Menor que               | `a < b`  |
| `>`      | Maior que               | `a > b`  |
| `<=`     | Menor ou igual a        | `a <= b` |
| `>=`     | Maior ou igual a        | `a >= b` |

### ❗ Erros Comuns em Estruturas Condicionais

1. **Confundir `=` (atribuição) com `==` (comparação)**:

```c
// ERRADO - Atribui 5 a x e verifica se é diferente de zero (sempre verdadeiro)
if (x = 5) {
    printf("Esta linha sempre será executada!\n");
}

// CORRETO - Compara se x é igual a 5
if (x == 5) {
    printf("x é igual a 5\n");
}
```

2. **Esquecer chaves em blocos de uma única linha**:

Embora opcionais para blocos de uma única instrução, a ausência de chaves pode levar a erros lógicos:

```c
// Potencialmente confuso
if (x > 10)
    printf("x é maior que 10\n");
    printf("Sempre executado!\n");  // Esta linha NÃO faz parte do if!

// Melhor prática
if (x > 10) {
    printf("x é maior que 10\n");
}
printf("Sempre executado!\n");
```

3. **Condições invertidas ou redundantes**:

```c
// Redundante
if (ehValido == true) {
    // Código
}

// Melhor
if (ehValido) {
    // Código
}

// Invertido de forma desnecessariamente complexa
if (!(x <= 10)) {
    // Código
}

// Mais claro
if (x > 10) {
    // Código
}
```

4. **Parênteses ausentes em expressões complexas**:

```c
// Pode não fazer o que você espera
if (x > 0 && y > 0 || z > 0) {
    // Executado se (x > 0 && y > 0) OU se (z > 0)
}

// Mais claro com parênteses
if ((x > 0 && y > 0) || z > 0) {
    // Mesmo comportamento, mais legível
}

// Comportamento diferente
if (x > 0 && (y > 0 || z > 0)) {
    // Executado se x > 0 E (y > 0 OU z > 0)
}
```

### 📊 Diagrama de Decisão

```
     ┌──────────┐
     │  Início  │
     └────┬─────┘
          │
    ┌─────▼─────┐
    │ Condição? │
    └──┬───┬────┘
       │   │
┌──────▼─┐ │ ┌────▼────┐
│ Verdade│ │ │  Falso  │
└────┬───┘ │ └────┬────┘
     │     │      │
┌────▼───┐ │ ┌────▼────┐
│ Bloco A│ │ │ Bloco B │
└────┬───┘ │ └────┬────┘
     │     │      │
     └─────┼──────┘
           │
     ┌─────▼─────┐
     │    Fim    │
     └───────────┘
```

### 🧩 Aplicações Práticas

#### 1️⃣ Validação de Entrada

```c
#include <stdio.h>

int main() {
    int idade;
    
    printf("Digite sua idade: ");
    scanf("%d", &idade);
    
    // Validação de entrada
    if (idade < 0 || idade > 150) {
        printf("Idade inválida!\n");
    } else if (idade < 18) {
        printf("Você é menor de idade.\n");
    } else if (idade < 60) {
        printf("Você é adulto.\n");
    } else {
        printf("Você é idoso.\n");
    }
    
    return 0;
}
```

#### 2️⃣ Menu de Opções

```c
#include <stdio.h>

int main() {
    int opcao;
    
    printf("==== MENU ====\n");
    printf("1. Consultar saldo\n");
    printf("2. Fazer depósito\n");
    printf("3. Fazer saque\n");
    printf("4. Sair\n");
    printf("Escolha uma opção: ");
    scanf("%d", &opcao);
    
    switch (opcao) {
        case 1:
            printf("Seu saldo é R$ 1000,00\n");
            break;
        case 2:
            printf("Digite o valor do depósito: ");
            // Código para depósito
            break;
        case 3:
            printf("Digite o valor do saque: ");
            // Código para saque
            break;
        case 4:
            printf("Saindo do programa. Até logo!\n");
            break;
        default:
            printf("Opção inválida!\n");
    }
    
    return 0;
}
```

#### 3️⃣ Calculadora Simples

```c
#include <stdio.h>

int main() {
    double num1, num2, resultado;
    char operador;
    
    printf("Digite uma expressão (ex: 5 + 3): ");
    scanf("%lf %c %lf", &num1, &operador, &num2);
    
    switch (operador) {
        case '+':
            resultado = num1 + num2;
            printf("%.2lf + %.2lf = %.2lf\n", num1, num2, resultado);
            break;
        case '-':
            resultado = num1 - num2;
            printf("%.2lf - %.2lf = %.2lf\n", num1, num2, resultado);
            break;
        case '*':
            resultado = num1 * num2;
            printf("%.2lf * %.2lf = %.2lf\n", num1, num2, resultado);
            break;
        case '/':
            if (num2 != 0) {
                resultado = num1 / num2;
                printf("%.2lf / %.2lf = %.2lf\n", num1, num2, resultado);
            } else {
                printf("Erro: Divisão por zero!\n");
            }
            break;
        default:
            printf("Operador inválido!\n");
    }
    
    return 0;
}
```

#### 4️⃣ Verificador de Ano Bissexto

```c
#include <stdio.h>

int main() {
    int ano;
    
    printf("Digite um ano: ");
    scanf("%d", &ano);
    
    // Um ano é bissexto se for divisível por 4
    // Exceto anos centenários (divisíveis por 100) que não são divisíveis por 400
    if ((ano % 4 == 0 && ano % 100 != 0) || (ano % 400 == 0)) {
        printf("%d é um ano bissexto.\n", ano);
    } else {
        printf("%d não é um ano bissexto.\n", ano);
    }
    
    return 0;
}
```

### 🧪 Boas Práticas

1. **Use chaves sempre**, mesmo para blocos de uma única instrução.
2. **Mantenha a indentação consistente** para melhorar a legibilidade.
3. **Prefira `if-else` em vez de múltiplos `if`** quando as condições são mutuamente exclusivas.
4. **Use parênteses em expressões complexas** para tornar a ordem de avaliação clara.
5. **Evite condições aninhadas muito profundas** (refatore usando funções ou variáveis auxiliares).
6. **Não se esqueça do `break` em casos de `switch`**, a menos que o "fall-through" seja intencional.
7. **Teste casos de limite e valores extremos** ao usar estruturas condicionais.

### 🎭 Exemplo de Programa Completo

Este programa demonstra diferentes estruturas condicionais em um sistema de classificação de notas:

```c
#include <stdio.h>

void avaliarNota(float nota) {
    // Usando if-else if-else
    if (nota < 0 || nota > 10) {
        printf("Nota inválida!\n");
    } else if (nota >= 9) {
        printf("Conceito A - Excelente!\n");
    } else if (nota >= 8) {
        printf("Conceito B - Muito bom!\n");
    } else if (nota >= 7) {
        printf("Conceito C - Bom\n");
    } else if (nota >= 6) {
        printf("Conceito D - Satisfatório\n");
    } else if (nota >= 5) {
        printf("Conceito E - Em recuperação\n");
    } else {
        printf("Conceito F - Reprovado\n");
    }
    
    // Usando operador ternário
    printf("Situação: %s\n", nota >= 6 ? "Aprovado" : "Reprovado");
    
    // Usando switch para comentários adicionais
    // Convertendo a nota para um valor inteiro entre 0 e 10
    int notaInteira = (int)nota;
    
    switch (notaInteira) {
        case 10:
            printf("Comentário: Perfeito!\n");
            break;
        case 9:
            printf("Comentário: Quase perfeito!\n");
            break;
        case 8:
        case 7:
            printf("Comentário: Acima da média!\n");
            break;
        case 6:
            printf("Comentário: Na média.\n");
            break;
        case 5:
            printf("Comentário: Precisa melhorar.\n");
            break;
        default:
            if (notaInteira < 5 && notaInteira >= 0) {
                printf("Comentário: Estude mais!\n");
            } else {
                printf("Comentário: Nota fora do intervalo válido.\n");
            }
    }
}

int main() {
    float nota;
    char continuar;
    
    do {
        printf("\n===== Sistema de Avaliação =====\n");
        printf("Digite a nota do aluno (0-10): ");
        scanf("%f", &nota);
        
        avaliarNota(nota);
        
        printf("\nDeseja avaliar outra nota? (S/N): ");
        scanf(" %c", &continuar);  // Espaço antes de %c para ignorar whitespace
        
    } while (continuar == 'S' || continuar == 's');
    
    printf("Programa encerrado.\n");
    
    return 0;
}
```

Este programa utiliza estruturas condicionais `if-else if-else`, operador ternário e `switch` para demonstrar diferentes formas de implementar a lógica condicional em C.

---

[🔙 Voltar ao índice principal](../README.md)

<img width=100% src="https://capsule-render.vercel.app/api?type=waving&color=A8B9CC&height=120&section=footer"/> 