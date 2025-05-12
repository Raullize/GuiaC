<img width=100% src="https://capsule-render.vercel.app/api?type=waving&color=A8B9CC&height=120&section=header"/>

# 🏗️ Passagem de Argumentos por Valor e Referência

## 📋 Compreendendo os Mecanismos de Passagem de Argumentos em C

Quando chamamos funções em C, precisamos passar dados para que sejam processados. A linguagem C oferece duas principais maneiras de passar argumentos para funções: por valor e por referência.

### 💡 Passagem por Valor

Na passagem por valor, uma cópia do valor do argumento é criada e passada para a função. Qualquer modificação feita no parâmetro dentro da função não afeta a variável original.

#### 1️⃣ Funcionamento da Passagem por Valor

```c
#include <stdio.h>

void duplicar(int num) {
    num = num * 2;
    printf("Dentro da função: num = %d\n", num);
}

int main() {
    int x = 5;
    printf("Antes da função: x = %d\n", x);
    
    duplicar(x);
    
    printf("Após a função: x = %d\n", x);  // x continua sendo 5
    
    return 0;
}
```

#### 2️⃣ Características da Passagem por Valor

- Uma cópia do valor é criada
- A variável original permanece inalterada
- Mudanças no parâmetro não afetam a variável original
- Ideal para valores simples que não precisam ser modificados
- Pode ser ineficiente para estruturas grandes (devido à cópia)

### 🔄 Passagem por Referência

Em C, a "passagem por referência" é simulada passando o endereço da variável (ponteiro) para a função. Isso permite que a função modifique diretamente o valor da variável original.

#### 1️⃣ Funcionamento da Passagem por Referência

```c
#include <stdio.h>

void duplicar(int* num) {
    *num = *num * 2;  // Modifica o valor no endereço
    printf("Dentro da função: *num = %d\n", *num);
}

int main() {
    int x = 5;
    printf("Antes da função: x = %d\n", x);
    
    duplicar(&x);  // Passa o endereço de x
    
    printf("Após a função: x = %d\n", x);  // x agora é 10
    
    return 0;
}
```

#### 2️⃣ Características da Passagem por Referência

- O endereço da variável é passado (não o valor)
- A função pode acessar e modificar a variável original
- Permite retornar múltiplos valores através de parâmetros
- Mais eficiente para estruturas grandes (evita cópia)
- Requer uso de ponteiros e operador de desreferenciação

### 📊 Comparação: Valor vs. Referência

| Característica | Passagem por Valor | Passagem por Referência |
|----------------|--------------------|-----------------------|
| Modificação    | Local              | Original              |
| Sintaxe        | `func(var)`        | `func(&var)`          |
| Na função      | `tipo param`       | `tipo* param`         |
| Acesso         | Direto             | Via desreferenciação (*) |
| Efeito colateral | Isolado          | Propaga mudanças      |
| Uso ideal      | Tipos simples, quando não é necessário modificar | Tipos complexos, quando é necessário modificar |

### 🔄 Passagem de Arrays

Arrays em C são sempre passados por referência. Quando passamos um array para uma função, estamos passando um ponteiro para o primeiro elemento.

```c
#include <stdio.h>

void modificar_array(int arr[], int tamanho) {
    for (int i = 0; i < tamanho; i++) {
        arr[i] *= 2;  // Modifica o array original
    }
}

int main() {
    int numeros[5] = {1, 2, 3, 4, 5};
    
    printf("Array original: ");
    for (int i = 0; i < 5; i++) {
        printf("%d ", numeros[i]);
    }
    printf("\n");
    
    modificar_array(numeros, 5);
    
    printf("Array modificado: ");
    for (int i = 0; i < 5; i++) {
        printf("%d ", numeros[i]);  // Imprime: 2 4 6 8 10
    }
    printf("\n");
    
    return 0;
}
```

**Nota**: Embora pareça que estamos passando o array inteiro, apenas o endereço do primeiro elemento é passado. A função recebe um ponteiro para o início do array.

### 🧩 Passagem de Estruturas

Estruturas (structs) podem ser passadas tanto por valor quanto por referência:

#### 1️⃣ Passagem de Estruturas por Valor

```c
#include <stdio.h>

typedef struct {
    int x;
    int y;
} Ponto;

void mover_ponto(Ponto p, int dx, int dy) {
    p.x += dx;
    p.y += dy;
    printf("Dentro da função: (%d, %d)\n", p.x, p.y);
}

int main() {
    Ponto ponto = {10, 20};
    
    printf("Antes: (%d, %d)\n", ponto.x, ponto.y);
    
    mover_ponto(ponto, 5, 5);
    
    printf("Depois: (%d, %d)\n", ponto.x, ponto.y);  // Não muda
    
    return 0;
}
```

#### 2️⃣ Passagem de Estruturas por Referência

```c
#include <stdio.h>

typedef struct {
    int x;
    int y;
} Ponto;

void mover_ponto(Ponto* p, int dx, int dy) {
    p->x += dx;  // Use -> para acesso via ponteiro
    p->y += dy;
    printf("Dentro da função: (%d, %d)\n", p->x, p->y);
}

int main() {
    Ponto ponto = {10, 20};
    
    printf("Antes: (%d, %d)\n", ponto.x, ponto.y);
    
    mover_ponto(&ponto, 5, 5);
    
    printf("Depois: (%d, %d)\n", ponto.x, ponto.y);  // Agora é (15, 25)
    
    return 0;
}
```

### 📤 Retornando Múltiplos Valores

A passagem por referência permite que uma função "retorne" múltiplos valores:

```c
#include <stdio.h>

void calcular_stats(const int arr[], int tamanho, int* soma, float* media, int* max, int* min) {
    *soma = 0;
    *max = arr[0];
    *min = arr[0];
    
    for (int i = 0; i < tamanho; i++) {
        *soma += arr[i];
        
        if (arr[i] > *max) *max = arr[i];
        if (arr[i] < *min) *min = arr[i];
    }
    
    *media = (float)*soma / tamanho;
}

int main() {
    int numeros[] = {5, 10, 3, 8, 7};
    int tamanho = sizeof(numeros) / sizeof(numeros[0]);
    
    int soma, max, min;
    float media;
    
    calcular_stats(numeros, tamanho, &soma, &media, &max, &min);
    
    printf("Soma: %d\n", soma);
    printf("Média: %.2f\n", media);
    printf("Máximo: %d\n", max);
    printf("Mínimo: %d\n", min);
    
    return 0;
}
```

### 🛡️ Parâmetros Constantes

Para proteger dados de modificações acidentais, você pode usar o modificador `const`:

```c
// Passagem por valor com const (redundante, mas documenta intenção)
void exibir_valor(const int num) {
    printf("Valor: %d\n", num);
    // num = 10;  // Erro de compilação
}

// Passagem por referência com const (protege o dado original)
void exibir_array(const int arr[], int tamanho) {
    for (int i = 0; i < tamanho; i++) {
        printf("%d ", arr[i]);
    }
    // arr[0] = 10;  // Erro de compilação
}
```

### 🧠 Boas Práticas

1. **Use passagem por valor** para tipos simples que não precisam ser modificados
2. **Use passagem por referência** quando:
   - Precisa modificar o valor original
   - Está trabalhando com estruturas grandes (eficiência)
   - Precisa retornar múltiplos valores
3. **Use `const`** para indicar e garantir que os dados não serão modificados
4. **Sempre verifique ponteiros** recebidos antes de desreferenciar
5. **Documente** claramente o propósito de cada parâmetro (entrada, saída, ou ambos)

### 📝 Exemplo de Aplicação: Manipulação de Frações

```c
#include <stdio.h>

typedef struct {
    int numerador;
    int denominador;
} Fracao;

// Função para simplificar uma fração (passagem por referência)
void simplificar(Fracao* f) {
    if (f->numerador == 0) {
        f->denominador = 1;
        return;
    }
    
    // Encontra o MDC usando o algoritmo de Euclides
    int a = (f->numerador > 0) ? f->numerador : -f->numerador;
    int b = f->denominador;
    
    while (b != 0) {
        int temp = b;
        b = a % b;
        a = temp;
    }
    
    // Divide ambos pelo MDC
    f->numerador /= a;
    f->denominador /= a;
    
    // Garante que o denominador seja positivo
    if (f->denominador < 0) {
        f->numerador = -f->numerador;
        f->denominador = -f->denominador;
    }
}

// Função para somar frações (usa valor e referência)
void somar_fracoes(Fracao f1, Fracao f2, Fracao* resultado) {
    resultado->numerador = f1.numerador * f2.denominador + f2.numerador * f1.denominador;
    resultado->denominador = f1.denominador * f2.denominador;
    simplificar(resultado);
}

// Função para exibir uma fração (passagem por valor)
void exibir_fracao(Fracao f) {
    printf("%d/%d", f.numerador, f.denominador);
}

int main() {
    Fracao a = {2, 6};
    Fracao b = {3, 4};
    Fracao resultado;
    
    printf("Frações originais: ");
    exibir_fracao(a);
    printf(" e ");
    exibir_fracao(b);
    printf("\n");
    
    // Simplifica a primeira fração
    simplificar(&a);
    printf("Primeira fração simplificada: ");
    exibir_fracao(a);
    printf("\n");
    
    // Soma as frações
    somar_fracoes(a, b, &resultado);
    printf("Soma: ");
    exibir_fracao(resultado);
    printf("\n");
    
    return 0;
}
```

---

[🔙 Voltar ao índice principal](../README.md)

<img width=100% src="https://capsule-render.vercel.app/api?type=waving&color=A8B9CC&height=120&section=footer"/> 