<img width=100% src="https://capsule-render.vercel.app/api?type=waving&color=A8B9CC&height=120&section=header"/>

# 🔢 Variáveis e Constantes

## 📋 Trabalhando com Variáveis em C

Variáveis são espaços de memória nomeados que armazenam valores. Em C, cada variável deve ter um tipo específico que determina o tamanho e o layout da memória da variável, o intervalo de valores que podem ser armazenados e o conjunto de operações que podem ser aplicadas.

### 📝 Declaração de Variáveis

A sintaxe básica para declarar uma variável em C é:

```c
tipo_da_variavel nome_da_variavel;
```

Exemplos:

```c
int idade;              // Declara uma variável de tipo inteiro chamada "idade"
float altura;           // Declara uma variável de ponto flutuante chamada "altura"
char inicial;           // Declara uma variável de caractere chamada "inicial"
double salario;         // Declara uma variável de ponto flutuante de precisão dupla
```

### ⚡ Inicialização de Variáveis

Você pode inicializar (atribuir um valor inicial) uma variável no momento da declaração:

```c
int idade = 25;         // Declara e inicializa com valor 25
float altura = 1.75;    // Declara e inicializa com valor 1.75
char inicial = 'J';     // Declara e inicializa com caractere 'J'
```

Também é possível declarar múltiplas variáveis do mesmo tipo em uma única linha:

```c
int a, b, c;            // Declara três variáveis inteiras
int x = 5, y = 10, z;   // Declara e inicializa duas, deixa a terceira sem inicialização
```

### 🔄 Atribuição de Valores

Após a declaração, você pode atribuir (ou modificar) valores às variáveis usando o operador de atribuição `=`:

```c
#include <stdio.h>

int main() {
    int numero;         // Declaração
    
    numero = 10;        // Atribuição inicial
    printf("Valor inicial: %d\n", numero);
    
    numero = 20;        // Reatribuição (mudança de valor)
    printf("Novo valor: %d\n", numero);
    
    return 0;
}
```

### 🧬 Escopo de Variáveis

O escopo de uma variável define onde ela pode ser acessada no código. Em C, existem três tipos principais de escopo:

#### 1️⃣ Variáveis Locais

Declaradas dentro de uma função ou bloco de código. Só são acessíveis dentro desse bloco ou função.

```c
#include <stdio.h>

void exemploEscopo() {
    int x = 10;         // Variável local à função exemploEscopo
    printf("Dentro da função: x = %d\n", x);
    
    {
        int y = 20;     // Variável local ao bloco
        printf("Dentro do bloco: x = %d, y = %d\n", x, y);
    }
    
    // printf("y = %d\n", y);  // ERRO: y não está acessível aqui
}

int main() {
    exemploEscopo();
    
    // printf("x = %d\n", x);  // ERRO: x não está acessível aqui
    
    return 0;
}
```

#### 2️⃣ Variáveis Globais

Declaradas fora de todas as funções. Acessíveis em qualquer parte do programa após a declaração.

```c
#include <stdio.h>

int contador = 0;      // Variável global

void incrementa() {
    contador++;        // Acessa e modifica a variável global
}

int main() {
    printf("Valor inicial: %d\n", contador);
    
    incrementa();
    incrementa();
    
    printf("Valor final: %d\n", contador);
    
    return 0;
}
```

#### 3️⃣ Variáveis Estáticas

Mantêm seus valores entre chamadas de função. Variáveis estáticas locais têm escopo local, mas vida útil por toda a execução do programa.

```c
#include <stdio.h>

void contar() {
    static int contador = 0;  // Inicializado apenas uma vez
    contador++;
    printf("Esta função foi chamada %d vez(es)\n", contador);
}

int main() {
    contar();  // Imprime: Esta função foi chamada 1 vez(es)
    contar();  // Imprime: Esta função foi chamada 2 vez(es)
    contar();  // Imprime: Esta função foi chamada 3 vez(es)
    
    return 0;
}
```

### 🔒 Constantes em C

Constantes são valores que não podem ser alterados durante a execução do programa. Existem várias maneiras de definir constantes em C:

#### 1️⃣ Usando `#define` (Diretiva de Pré-processador)

```c
#include <stdio.h>

#define PI 3.14159
#define NOME "Programa de Exemplo"
#define MAXIMO 100

int main() {
    printf("Nome: %s\n", NOME);
    printf("Pi: %.5f\n", PI);
    printf("Valor máximo: %d\n", MAXIMO);
    
    // PI = 3.15; // ERRO: Não pode modificar uma constante definida com #define
    
    return 0;
}
```

#### 2️⃣ Usando a palavra-chave `const`

```c
#include <stdio.h>

int main() {
    const float PI = 3.14159;
    const char* MENSAGEM = "Olá, mundo!";
    const int DIAS_SEMANA = 7;
    
    printf("Pi: %.5f\n", PI);
    printf("Mensagem: %s\n", MENSAGEM);
    printf("Dias na semana: %d\n", DIAS_SEMANA);
    
    // PI = 3.15; // ERRO: Não pode modificar uma variável const
    
    return 0;
}
```

#### 3️⃣ Diferenças entre `#define` e `const`

| Característica         | `#define`                      | `const`                             |
|------------------------|---------------------------------|-------------------------------------|
| Momento de substituição| Durante o pré-processamento    | Em tempo de compilação              |
| Verificação de tipo    | Não (simples substituição)     | Sim (tem tipo específico)           |
| Escopo                 | Global (do ponto da definição) | Segue as regras normais de escopo   |
| Depuração              | Mais difícil (texto substituído)| Mais fácil (variável real)         |
| Uso com ponteiros      | Limitado                        | Mais flexível                       |

### 📋 Convenções de Nomenclatura

Para manter o código legível e consistente, é recomendado seguir algumas convenções:

1. Nomes de variáveis devem ser descritivos
2. Em C, nomes de variáveis geralmente usam `snake_case` (letras minúsculas e underscores)
3. Constantes são geralmente escritas em `MAIÚSCULAS`
4. Evite usar nomes muito curtos (exceto para contadores simples como `i`, `j`, `k`)

```c
// Boas práticas
int idade_aluno = 20;
float taxa_juros = 0.05;
char primeira_letra = 'A';

// Constantes
#define VELOCIDADE_LUZ 299792458
const double PI = 3.14159265358979;

// Convenções para contadores
for (int i = 0; i < 10; i++) {
    // ...
}
```

### 🧪 Modificadores de Variáveis

Além dos tipos básicos, C oferece modificadores que alteram como as variáveis são tratadas:

#### 1️⃣ `static`

Como mencionado anteriormente, o modificador `static` faz com que uma variável local mantenha seu valor entre chamadas de função.

#### 2️⃣ `extern`

Permite declarar uma variável que está definida em outro arquivo.

```c
// arquivo1.c
int contador = 0;  // Definição

// arquivo2.c
extern int contador;  // Declaração de variável definida em outro lugar
```

#### 3️⃣ `register`

Sugere ao compilador que armazene a variável em um registrador do processador para acesso mais rápido (embora compiladores modernos geralmente ignorem essa sugestão).

```c
register int i;
for (i = 0; i < 1000000; i++) {
    // Operações frequentes com i
}
```

#### 4️⃣ `volatile`

Informa ao compilador que o valor da variável pode mudar a qualquer momento (útil quando se lida com hardware ou threads).

```c
volatile int sensor_value;  // Valor pode ser alterado externamente
```

### 🚫 Erros Comuns com Variáveis

1. **Usar variável não inicializada**:
   ```c
   int a;
   printf("%d\n", a);  // CUIDADO: Valor indeterminado
   ```

2. **Confundir atribuição com comparação**:
   ```c
   if (x = 5) {  // CUIDADO: Isto é uma atribuição, não comparação
       // ...
   }
   // Correto seria: if (x == 5)
   ```

3. **Tentar modificar constantes**:
   ```c
   const int MAX = 100;
   MAX = 200;  // ERRO: Não pode modificar constante
   ```

4. **Ignorar o escopo das variáveis**:
   ```c
   if (condicao) {
       int resultado = calcular();
   }
   printf("%d\n", resultado);  // ERRO: resultado não existe neste escopo
   ```

### ⚙️ Exemplo de Programa Completo

```c
#include <stdio.h>

// Constantes globais
#define PI 3.14159
#define MAX_ALUNOS 50

// Variável global
int contador_global = 0;

void demonstrar_escopos() {
    // Variável local
    int contador_local = 10;
    
    // Variável estática
    static int chamadas = 0;
    chamadas++;
    
    printf("Local: %d, Global: %d, Chamadas: %d\n", 
           contador_local, contador_global, chamadas);
    
    contador_local++;
    contador_global++;
}

int main() {
    // Constante local
    const double TAXA = 0.25;
    
    // Variáveis locais
    int idade = 25;
    float altura = 1.75;
    char nome[20] = "Carlos";
    
    printf("Nome: %s, Idade: %d, Altura: %.2f\n", nome, idade, altura);
    printf("PI: %.5f, Taxa: %.2f\n", PI, TAXA);
    
    demonstrar_escopos();  // Local: 10, Global: 0, Chamadas: 1
    demonstrar_escopos();  // Local: 10, Global: 1, Chamadas: 2
    demonstrar_escopos();  // Local: 10, Global: 2, Chamadas: 3
    
    printf("Contador global final: %d\n", contador_global);
    
    return 0;
}
```

Este programa demonstra vários conceitos relacionados a variáveis e constantes em C, incluindo diferentes tipos, escopos, inicialização e modificadores.

---

[🔙 Voltar ao índice principal](../README.md)

<img width=100% src="https://capsule-render.vercel.app/api?type=waving&color=A8B9CC&height=120&section=footer"/> 