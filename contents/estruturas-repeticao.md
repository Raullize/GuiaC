<img width=100% src="https://capsule-render.vercel.app/api?type=waving&color=A8B9CC&height=120&section=header"/>

# ♻️ Estruturas de Repetição

## 📋 Introdução aos Loops em C

As estruturas de repetição, também chamadas de loops, permitem executar um bloco de código várias vezes. Elas são fundamentais para resolver problemas que exigem repetição de tarefas, processamento de coleções de dados e implementação de algoritmos iterativos.

Em C, existem três principais estruturas de repetição:
1. Loop `while`
2. Loop `do-while`
3. Loop `for`

### 🔄 Loop `while`

O loop `while` executa um bloco de código enquanto uma condição específica for verdadeira. A condição é verificada antes de cada iteração.

**Sintaxe:**
```c
while (condição) {
    // Bloco de código a ser repetido
}
```

**Fluxo de Execução:**
1. Verifica a condição
2. Se a condição for verdadeira, executa o bloco de código
3. Retorna ao passo 1
4. Se a condição for falsa, sai do loop

**Exemplo:**

```c
#include <stdio.h>

int main() {
    int contador = 1;
    
    while (contador <= 5) {
        printf("Contagem: %d\n", contador);
        contador++;  // Incrementa o contador
    }
    
    printf("Loop concluído!\n");
    
    return 0;
}
```

**Saída:**
```
Contagem: 1
Contagem: 2
Contagem: 3
Contagem: 4
Contagem: 5
Loop concluído!
```

#### 🔑 Pontos importantes:

- Se a condição inicial for falsa, o bloco de código não será executado nenhuma vez
- É necessário modificar algo dentro do loop que eventualmente torne a condição falsa, caso contrário, você terá um loop infinito
- A condição é reavaliada no início de cada iteração

### 🔁 Loop `do-while`

O loop `do-while` é semelhante ao `while`, mas a condição é verificada após a execução do bloco de código. Isso garante que o bloco seja executado pelo menos uma vez.

**Sintaxe:**
```c
do {
    // Bloco de código a ser repetido
} while (condição);
```

**Fluxo de Execução:**
1. Executa o bloco de código
2. Verifica a condição
3. Se a condição for verdadeira, volta ao passo 1
4. Se a condição for falsa, sai do loop

**Exemplo:**

```c
#include <stdio.h>

int main() {
    int numero;
    
    do {
        printf("Digite um número positivo: ");
        scanf("%d", &numero);
        
        if (numero <= 0) {
            printf("Número inválido! Tente novamente.\n");
        }
    } while (numero <= 0);
    
    printf("Você digitou o número positivo: %d\n", numero);
    
    return 0;
}
```

Neste exemplo, o programa solicita ao usuário que digite um número positivo. Mesmo se o usuário digitar um número não positivo na primeira tentativa, a mensagem será exibida e o usuário terá a chance de digitar novamente.

#### 🔑 Pontos importantes:

- O bloco de código é sempre executado pelo menos uma vez, independentemente da condição
- A condição é verificada no final de cada iteração
- Útil para validação de entrada de dados
- O `;` após a condição é obrigatório

### 🔢 Loop `for`

O loop `for` é ideal para iterações contáveis, onde você sabe quantas vezes deseja executar um bloco de código. É composto por três partes: inicialização, condição e expressão de incremento/decremento.

**Sintaxe:**
```c
for (inicialização; condição; incremento/decremento) {
    // Bloco de código a ser repetido
}
```

**Fluxo de Execução:**
1. Executa a expressão de inicialização (apenas uma vez)
2. Verifica a condição
3. Se a condição for verdadeira, executa o bloco de código
4. Executa a expressão de incremento/decremento
5. Volta ao passo 2
6. Se a condição for falsa, sai do loop

**Exemplo:**

```c
#include <stdio.h>

int main() {
    int i;
    
    for (i = 0; i < 5; i++) {
        printf("Iteração %d\n", i);
    }
    
    printf("Loop concluído! Valor final de i: %d\n", i);
    
    return 0;
}
```

**Saída:**
```
Iteração 0
Iteração 1
Iteração 2
Iteração 3
Iteração 4
Loop concluído! Valor final de i: 5
```

#### 🔢 Variações do Loop `for`

**Contagem decrescente:**
```c
for (int i = 10; i > 0; i--) {
    printf("%d ", i);
}
// Saída: 10 9 8 7 6 5 4 3 2 1
```

**Incremento diferente de 1:**
```c
for (int i = 0; i <= 10; i += 2) {
    printf("%d ", i);
}
// Saída: 0 2 4 6 8 10
```

**Múltiplas variáveis:**
```c
for (int i = 0, j = 10; i < j; i++, j--) {
    printf("i=%d, j=%d\n", i, j);
}
/* Saída:
i=0, j=10
i=1, j=9
i=2, j=8
i=3, j=7
i=4, j=6
*/
```

**Loop `for` sem inicialização ou incremento:**
```c
int i = 0;
for (; i < 5;) {
    printf("%d ", i);
    i++;
}
// Saída: 0 1 2 3 4
```

**Loop infinito com `for`:**
```c
for (;;) {
    // Código executado indefinidamente
    // Precisará de uma instrução break para sair
}
```

#### 🔑 Pontos importantes:

- A variável de controle (contador) é geralmente inicializada na primeira parte
- A condição de continuação é verificada antes de cada iteração
- A expressão de incremento/decremento é executada após cada iteração
- Todas as três partes do `for` são opcionais, mas os ponto-e-vírgula (`;`) são obrigatórios
- O loop `for` é especialmente útil quando você sabe antecipadamente o número de iterações

### 🔀 Comandos de Controle de Loop

C fornece dois comandos especiais para alterar o fluxo normal dos loops:

#### 1️⃣ `break`

O comando `break` é usado para sair imediatamente de um loop, independentemente da condição.

**Exemplo:**

```c
#include <stdio.h>

int main() {
    int i;
    
    for (i = 1; i <= 10; i++) {
        if (i == 6) {
            printf("Encontrei o 6! Saindo do loop...\n");
            break;  // Sai do loop quando i é igual a 6
        }
        printf("Número: %d\n", i);
    }
    
    printf("Loop encerrado. Valor final de i: %d\n", i);
    
    return 0;
}
```

**Saída:**
```
Número: 1
Número: 2
Número: 3
Número: 4
Número: 5
Encontrei o 6! Saindo do loop...
Loop encerrado. Valor final de i: 6
```

#### 2️⃣ `continue`

O comando `continue` é usado para pular o restante da iteração atual e continuar com a próxima iteração do loop.

**Exemplo:**

```c
#include <stdio.h>

int main() {
    for (int i = 1; i <= 10; i++) {
        if (i % 2 == 0) {
            // Pula números pares
            continue;
        }
        printf("Número ímpar: %d\n", i);
    }
    
    return 0;
}
```

**Saída:**
```
Número ímpar: 1
Número ímpar: 3
Número ímpar: 5
Número ímpar: 7
Número ímpar: 9
```

### 🔄 Loops Aninhados

Loops podem ser aninhados, ou seja, um loop dentro de outro. Isso é útil para trabalhar com estruturas de dados multidimensionais ou para resolver problemas mais complexos.

**Exemplo - Padrão de asteriscos:**

```c
#include <stdio.h>

int main() {
    int linhas = 5;
    
    for (int i = 1; i <= linhas; i++) {
        // Loop interno - imprime asteriscos
        for (int j = 1; j <= i; j++) {
            printf("* ");
        }
        printf("\n");
    }
    
    return 0;
}
```

**Saída:**
```
* 
* * 
* * * 
* * * * 
* * * * * 
```

**Exemplo - Tabela de multiplicação:**

```c
#include <stdio.h>

int main() {
    printf("Tabela de multiplicação 10x10:\n\n");
    
    // Imprime cabeçalho
    printf("    ");
    for (int i = 1; i <= 10; i++) {
        printf("%4d", i);
    }
    printf("\n    ");
    
    for (int i = 1; i <= 10; i++) {
        printf("----");
    }
    printf("\n");
    
    // Imprime a tabela
    for (int i = 1; i <= 10; i++) {
        printf("%2d |", i);
        
        for (int j = 1; j <= 10; j++) {
            printf("%4d", i * j);
        }
        
        printf("\n");
    }
    
    return 0;
}
```

Essa tabela de multiplicação mostra produtos de 1x1 até 10x10, formatados em uma tabela.

### 🧩 Escolhendo a Estrutura Adequada

Cada estrutura de repetição tem seus usos ideais:

1. **Use `while` quando:**
   - O número de iterações não é conhecido antecipadamente
   - A condição depende de algo além de um simples contador
   - Pode ser necessário não executar o loop nenhuma vez

2. **Use `do-while` quando:**
   - O bloco de código deve ser executado pelo menos uma vez
   - Validação de entrada do usuário
   - Menus que devem ser exibidos pelo menos uma vez

3. **Use `for` quando:**
   - O número de iterações é conhecido antecipadamente
   - Iteração através de sequências numéricas
   - Controle de loop com padrão de inicialização, teste e incremento

### 🚫 Problemas Comuns e Como Evitá-los

#### 1️⃣ Loop Infinito

Um loop infinito ocorre quando a condição de saída nunca se torna falsa.

**Causas comuns:**
- Esquecer de incrementar/decrementar a variável de controle
- Usar o operador de atribuição (`=`) em vez do operador de comparação (`==`)
- Definir uma condição logicamente impossível

**Exemplo incorreto:**
```c
// Loop infinito - i nunca muda
for (int i = 0; i < 10; ) {
    printf("%d ", i);
}
```

**Correção:**
```c
for (int i = 0; i < 10; i++) {
    printf("%d ", i);
}
```

#### 2️⃣ Erro Off-by-One

Erros "off-by-one" ocorrem quando o loop executa uma iteração a mais ou a menos do que o esperado.

**Exemplo:**
```c
// Imprime 0 a 9 (10 números)
for (int i = 0; i < 10; i++) {
    printf("%d ", i);
}

// Imprime 1 a 10 (10 números)
for (int i = 1; i <= 10; i++) {
    printf("%d ", i);
}

// ERRO: Imprime 0 a 10 (11 números) - uma iteração a mais!
for (int i = 0; i <= 10; i++) {
    printf("%d ", i);
}
```

#### 3️⃣ Alteração da Variável de Controle Dentro do Loop

Modificar a variável de controle dentro do corpo do loop (além da expressão de incremento) pode levar a comportamentos inesperados.

**Exemplo:**
```c
for (int i = 0; i < 10; i++) {
    printf("%d ", i);
    
    // PROBLEMA: altera a variável de controle dentro do loop
    if (i == 5) {
        i = 8;  // Pula diretamente para 9 na próxima iteração
    }
}
```

### 🔍 Exemplos Práticos de Aplicação

#### 1️⃣ Cálculo de Fatorial

```c
#include <stdio.h>

int main() {
    int n, fatorial = 1;
    
    printf("Digite um número para calcular o fatorial: ");
    scanf("%d", &n);
    
    if (n < 0) {
        printf("Não é possível calcular o fatorial de um número negativo.\n");
    } else {
        for (int i = 1; i <= n; i++) {
            fatorial *= i;
        }
        
        printf("%d! = %d\n", n, fatorial);
    }
    
    return 0;
}
```

#### 2️⃣ Verificador de Números Primos

```c
#include <stdio.h>
#include <stdbool.h>
#include <math.h>

bool ehPrimo(int num) {
    if (num <= 1) return false;
    if (num <= 3) return true;
    if (num % 2 == 0 || num % 3 == 0) return false;
    
    // Verifica divisibilidade por números da forma 6k±1
    for (int i = 5; i * i <= num; i += 6) {
        if (num % i == 0 || num % (i + 2) == 0) {
            return false;
        }
    }
    
    return true;
}

int main() {
    int num;
    
    printf("Digite um número para verificar se é primo: ");
    scanf("%d", &num);
    
    if (ehPrimo(num)) {
        printf("%d é um número primo.\n", num);
    } else {
        printf("%d não é um número primo.\n", num);
    }
    
    return 0;
}
```

#### 3️⃣ Sequência de Fibonacci

```c
#include <stdio.h>

int main() {
    int n, primeiro = 0, segundo = 1, proximo;
    
    printf("Digite a quantidade de termos da sequência de Fibonacci: ");
    scanf("%d", &n);
    
    printf("Sequência de Fibonacci com %d termos:\n", n);
    
    for (int i = 0; i < n; i++) {
        if (i <= 1) {
            proximo = i;
        } else {
            proximo = primeiro + segundo;
            primeiro = segundo;
            segundo = proximo;
        }
        
        printf("%d ", proximo);
    }
    
    printf("\n");
    
    return 0;
}
```

#### 4️⃣ Busca Linear em Array

```c
#include <stdio.h>
#include <stdbool.h>

int main() {
    int array[] = {10, 23, 5, 17, 42, 8, 15, 30};
    int tamanho = sizeof(array) / sizeof(array[0]);
    int busca, i;
    bool encontrado = false;
    
    printf("Array: ");
    for (i = 0; i < tamanho; i++) {
        printf("%d ", array[i]);
    }
    
    printf("\nDigite um valor para buscar: ");
    scanf("%d", &busca);
    
    // Busca linear usando while
    i = 0;
    while (i < tamanho) {
        if (array[i] == busca) {
            encontrado = true;
            break;
        }
        i++;
    }
    
    if (encontrado) {
        printf("Valor %d encontrado na posição %d.\n", busca, i);
    } else {
        printf("Valor %d não encontrado no array.\n", busca);
    }
    
    return 0;
}
```

### 🔄 Loops com `goto` (Não Recomendado)

C possui uma instrução `goto` que permite saltos incondicionais no código. Embora possa ser usada para criar loops, seu uso é **fortemente desencorajado** na programação moderna, pois pode tornar o código difícil de entender e manter.

**Exemplo (apenas para conhecimento):**

```c
#include <stdio.h>

int main() {
    int contador = 1;
    
inicio_loop:
    if (contador <= 5) {
        printf("Contagem: %d\n", contador);
        contador++;
        goto inicio_loop;
    }
    
    printf("Loop concluído!\n");
    
    return 0;
}
```

Este código produz o mesmo resultado que um loop `while`, mas é menos legível e mais propenso a erros.

### 🧪 Loop Controlado por Eventos

Em algumas situações, você pode querer que um loop continue até que um evento específico ocorra, como o usuário digitar um valor específico.

**Exemplo - Menu interativo:**

```c
#include <stdio.h>
#include <stdbool.h>

int main() {
    int opcao;
    bool executando = true;
    
    while (executando) {
        printf("\n=== MENU ===\n");
        printf("1. Opção 1\n");
        printf("2. Opção 2\n");
        printf("3. Opção 3\n");
        printf("0. Sair\n");
        printf("Escolha uma opção: ");
        scanf("%d", &opcao);
        
        switch (opcao) {
            case 1:
                printf("Você escolheu a Opção 1\n");
                break;
            case 2:
                printf("Você escolheu a Opção 2\n");
                break;
            case 3:
                printf("Você escolheu a Opção 3\n");
                break;
            case 0:
                printf("Saindo do programa...\n");
                executando = false;
                break;
            default:
                printf("Opção inválida!\n");
        }
    }
    
    return 0;
}
```

### 🎭 Exemplo de Programa Completo

Este programa demonstra o uso das diferentes estruturas de repetição para criar um jogo simples de adivinhação:

```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#include <stdbool.h>

int main() {
    // Inicializa gerador de números aleatórios
    srand(time(NULL));
    
    int numeroSecreto, palpite, tentativas = 0;
    int min = 1, max = 100;
    char jogarNovamente;
    bool acertou;
    
    printf("=== JOGO DE ADIVINHAÇÃO ===\n");
    printf("Tente adivinhar o número entre 1 e 100\n\n");
    
    do {
        // Gera novo número secreto entre 1 e 100
        numeroSecreto = rand() % 100 + 1;
        tentativas = 0;
        acertou = false;
        
        printf("Um novo número foi gerado!\n");
        
        // Loop while - continua até o jogador acertar
        while (!acertou) {
            tentativas++;
            
            printf("\nTentativa #%d\n", tentativas);
            printf("Digite seu palpite (%d-%d): ", min, max);
            scanf("%d", &palpite);
            
            // Verifica palpite
            if (palpite < min || palpite > max) {
                printf("Por favor, digite um número entre %d e %d.\n", min, max);
                tentativas--; // Não conta esta tentativa
                continue;
            }
            
            if (palpite < numeroSecreto) {
                printf("Muito BAIXO! Tente um número maior.\n");
            } else if (palpite > numeroSecreto) {
                printf("Muito ALTO! Tente um número menor.\n");
            } else {
                acertou = true;
                printf("\nPARABÉNS! Você acertou em %d tentativas!\n", tentativas);
                
                // For loop para imprimir estrelas
                for (int i = 0; i < 20; i++) {
                    printf("*");
                }
                printf("\n");
            }
            
            // Dá uma dica após 5 tentativas
            if (tentativas == 5 && !acertou) {
                int dica = (numeroSecreto % 2 == 0) ? 0 : 1;
                printf("DICA: O número é %s.\n", dica == 0 ? "PAR" : "ÍMPAR");
            }
        }
        
        printf("\nDeseja jogar novamente? (S/N): ");
        scanf(" %c", &jogarNovamente);
        
    } while (jogarNovamente == 'S' || jogarNovamente == 's');
    
    printf("\nObrigado por jogar! Até a próxima!\n");
    
    return 0;
}
```

Este programa incorpora:
- Loop `do-while` para controlar a repetição do jogo
- Loop `while` para controlar as tentativas de adivinhação
- Instrução `continue` para ignorar entradas inválidas
- Loop `for` para exibir um padrão de celebração
- Lógica condicional para fornecer feedback e dicas

### 🧮 Resumo das Estruturas de Repetição

```
┌─────────────────┬────────────────────────────────────────────────┐
│ Estrutura       │ Características                                │
├─────────────────┼────────────────────────────────────────────────┤
│ while           │ - Testa a condição antes de executar o bloco   │
│                 │ - Pode executar zero vezes                     │
│                 │ - Bom para loops com número desconhecido       │
│                 │   de iterações                                 │
├─────────────────┼────────────────────────────────────────────────┤
│ do-while        │ - Testa a condição após executar o bloco       │
│                 │ - Sempre executa pelo menos uma vez            │
│                 │ - Bom para validação de entrada e menus        │
├─────────────────┼────────────────────────────────────────────────┤
│ for             │ - Inicialização, condição e incremento         │
│                 │   em uma única linha                           │
│                 │ - Bom para loops com contagem                  │
│                 │ - Variável de controle tipicamente local       │
│                 │   ao loop                                      │
└─────────────────┴────────────────────────────────────────────────┘
```

As estruturas de repetição são ferramentas poderosas e essenciais na programação em C, permitindo resolver uma ampla gama de problemas de forma eficiente e elegante.

---

[🔙 Voltar ao índice principal](../README.md)

<img width=100% src="https://capsule-render.vercel.app/api?type=waving&color=A8B9CC&height=120&section=footer"/> 