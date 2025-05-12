<img width=100% src="https://capsule-render.vercel.app/api?type=waving&color=A8B9CC&height=120&section=header"/>

# 📝 Comentários

## 📋 Documentando seu código em C

Comentários são texto inserido no código-fonte que o compilador ignora. Eles são usados para explicar o funcionamento do código e torná-lo mais legível para outros programadores (e para você mesmo no futuro). Em C, existem dois tipos de comentários que você pode utilizar.

### 💬 Tipos de Comentários em C

#### 1. Comentários de Múltiplas Linhas (Estilo C Tradicional)

Os comentários de múltiplas linhas começam com `/*` e terminam com `*/`. Todo o texto entre esses delimitadores é ignorado pelo compilador:

```c
/* Este é um comentário de múltiplas linhas.
   Ele pode se estender por várias linhas
   e é útil para explicações mais longas. */

/* Este é um 
   comentário 
   de várias linhas */
```

Você também pode usar este estilo para comentários de uma única linha:

```c
/* Esta é uma função de soma */
```

#### 2. Comentários de Linha Única (Estilo C++)

Em C99 e versões posteriores, você também pode usar comentários de linha única, que começam com `//` e continuam até o final da linha:

```c
// Este é um comentário de linha única

int soma = a + b;  // Isso calcula a soma de a e b
```

### 🎯 Quando e Como Usar Comentários

#### 1. Cabeçalhos de Arquivos e Funções

Use comentários para documentar o propósito de arquivos e funções:

```c
/*
 * arquivo: matematica.c
 * descrição: Implementa funções matemáticas básicas para o projeto XYZ
 * autor: Seu Nome
 * data: 12/05/2023
 */

/**
 * Calcula o fatorial de um número
 * 
 * @param n O número para calcular o fatorial
 * @return O fatorial de n, ou -1 se n < 0
 */
int fatorial(int n) {
    if (n < 0) return -1;
    if (n <= 1) return 1;
    return n * fatorial(n - 1);
}
```

#### 2. Explicar Algoritmos Complexos

Use comentários para explicar partes mais complexas do código:

```c
/* 
 * Algoritmo de ordenação QuickSort
 * Complexidade de tempo médio: O(n log n)
 * Complexidade de tempo pior caso: O(n²)
 */
void quicksort(int arr[], int baixo, int alto) {
    if (baixo < alto) {
        // Encontrar o pivô, que divide o array
        int pivo = particionar(arr, baixo, alto);
        
        // Ordenar os elementos antes e depois do pivô
        quicksort(arr, baixo, pivo - 1);
        quicksort(arr, pivo + 1, alto);
    }
}
```

#### 3. Explicar o "Por Quê" (Não o "O Quê")

Bons comentários explicam o motivo por trás de uma implementação, não apenas o que o código faz:

```c
// Ruim: Incrementa contador em 1
contador++;

// Bom: Incrementa contador para rastrear o número de tentativas falhas
contador++;
```

#### 4. Documentar Comportamentos Não Óbvios ou Bugs Conhecidos

```c
// NOTA: Esta função pode retornar um ponteiro nulo em condições de pouca memória
char* clonar_string(const char* str) {
    // ...
}

// FIXME: Ocasionalmente causa um vazamento de memória quando tamanho > 1024
// TODO: Implementar verificação de limites para evitar buffer overflow
// BUG: Falha quando a entrada contém caracteres Unicode
```

### 📌 Estilos de Documentação Comuns

#### Estilo Javadoc/Doxygen

Este estilo usa `/**` para iniciar um bloco de documentação e pode incluir tags especiais que ferramentas como Doxygen podem processar para gerar documentação automática:

```c
/**
 * @brief Calcula a raiz quadrada de um número.
 *
 * @param x O número para calcular a raiz quadrada
 * @pre x >= 0
 * @return A raiz quadrada de x
 * @throws Erro se x < 0
 *
 * @details Esta função utiliza o método de Newton para
 * aproximar a raiz quadrada do valor fornecido.
 *
 * @example
 * double resultado = raiz_quadrada(16.0);  // resultado = 4.0
 */
double raiz_quadrada(double x) {
    // Implementação...
}
```

### 🚫 O que Evitar em Comentários

#### 1. Comentários Óbvios

Evite comentários que apenas repetem o que o código já diz claramente:

```c
// Ruim
i++; // Incrementa i

// Bom (se necessário)
retries_count++; // Incrementa o contador de tentativas após uma falha na conexão
```

#### 2. Comentários Desatualizados

Comentários que não são mantidos quando o código muda são piores que nenhum comentário:

```c
// Isso calcula a média dos valores (COMENTÁRIO DESATUALIZADO!)
soma = a + b;  // Na verdade, está apenas somando valores
```

#### 3. Comentários Excessivos

Excesso de comentários pode tornar o código mais difícil de ler:

```c
// Ruim
// Define uma variável inteira chamada contador
// e inicializa com valor zero
int contador = 0;

// Bom (geralmente não precisa de comentário)
int contador_tentativas = 0;
```

### 🔄 Comentários para Depuração

É comum usar comentários para "desativar" temporariamente partes do código durante a depuração:

```c
int main() {
    /*
    // Código antigo que está sendo substituído
    int x = calculo_antigo();
    processar(x);
    */
    
    // Nova implementação
    int y = calculo_novo();
    processar(y);
    
    return 0;
}
```

Porém, em projetos profissionais, é melhor usar diretivas de pré-processador para este fim:

```c
int main() {
    #if 0
    // Código desativado
    int x = calculo_antigo();
    processar(x);
    #else
    // Código ativo
    int y = calculo_novo();
    processar(y);
    #endif
    
    return 0;
}
```

### 📊 Padronização de Comentários

Em projetos maiores, é útil adotar um padrão consistente de comentários:

#### Exemplo de Padrão para Cabeçalho de Arquivo

```c
/*******************************************************************************
 * Arquivo: nome_arquivo.c
 * Autor: Nome do Autor
 * Data: DD/MM/AAAA
 * 
 * Descrição: Breve descrição do propósito deste arquivo.
 * 
 * Copyright (c) AAAA Empresa/Organização
 *******************************************************************************/
```

#### Exemplo de Padrão para Funções

```c
/*
 * nomeDaFuncao - Breve descrição em uma linha
 * @param1: descrição do primeiro parâmetro
 * @param2: descrição do segundo parâmetro
 *
 * Descrição mais detalhada da função se necessário.
 * Pode incluir exemplos, casos de uso, etc.
 *
 * Retorno: descrição do valor retornado
 */
```

### 🧠 Comentários em Arquivos de Cabeçalho (.h)

Os comentários em arquivos de cabeçalho são especialmente importantes, pois documentam a interface que outros programadores usarão:

```c
/*
 * matematica.h - Biblioteca de funções matemáticas
 */

#ifndef MATEMATICA_H
#define MATEMATICA_H

/**
 * Calcula o maior divisor comum entre dois números.
 *
 * @param a Primeiro número inteiro
 * @param b Segundo número inteiro
 * @return O MDC de a e b
 */
int mdc(int a, int b);

/**
 * Calcula o menor múltiplo comum entre dois números.
 *
 * @param a Primeiro número inteiro
 * @param b Segundo número inteiro
 * @return O MMC de a e b
 */
int mmc(int a, int b);

#endif /* MATEMATICA_H */
```

### 🌟 Dicas Finais

1. **Seja conciso mas completo**: Explique o necessário sem redundância
2. **Mantenha os comentários atualizados**: Comentários desatualizados são prejudiciais
3. **Use comentários para documentar decisões**: Explique por que escolheu uma abordagem em vez de outra
4. **Adote um estilo consistente**: Use o mesmo formato de comentários em todo o projeto
5. **Comente o "por quê", não o "como"**: O código já mostra como algo está sendo feito
6. **Use nomes claros de variáveis e funções**: Bom código se auto-documenta e reduz a necessidade de comentários

---

[🔙 Voltar ao índice principal](../README.md)

<img width=100% src="https://capsule-render.vercel.app/api?type=waving&color=A8B9CC&height=120&section=footer"/> 