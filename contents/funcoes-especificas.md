<img width=100% src="https://capsule-render.vercel.app/api?type=waving&color=A8B9CC&height=120&section=header"/>

# 🔧 Funções Específicas em C

Neste guia, vamos explorar os diferentes tipos de funções em C, incluindo funções inteiras, funções caractere e funções booleanas.

## 📝 Funções Inteiras

Funções inteiras são aquelas que retornam um valor do tipo `int`. São muito comuns em C e são usadas para realizar cálculos e retornar resultados numéricos.

```c
int soma(int a, int b) {
    return a + b;
}

int fatorial(int n) {
    if (n <= 1) return 1;
    return n * fatorial(n - 1);
}
```

## 🔤 Funções Caractere

Funções caractere retornam um valor do tipo `char`. São úteis para manipulação de caracteres individuais.

```c
char maiusculo(char c) {
    if (c >= 'a' && c <= 'z') {
        return c - 32;
    }
    return c;
}

char minusculo(char c) {
    if (c >= 'A' && c <= 'Z') {
        return c + 32;
    }
    return c;
}
```

## ✅ Funções Booleanas

Em C, não existe um tipo booleano nativo. Funções booleanas geralmente retornam um `int`, onde 0 representa falso e qualquer valor diferente de 0 representa verdadeiro.

```c
int ehPar(int numero) {
    return numero % 2 == 0;
}

int ehPrimo(int numero) {
    if (numero <= 1) return 0;
    for (int i = 2; i * i <= numero; i++) {
        if (numero % i == 0) return 0;
    }
    return 1;
}
```

## 🎯 Exemplos Práticos

### Exemplo 1: Calculadora Simples
```c
int soma(int a, int b) {
    return a + b;
}

int subtracao(int a, int b) {
    return a - b;
}

int multiplicacao(int a, int b) {
    return a * b;
}

int divisao(int a, int b) {
    if (b == 0) return 0; // Tratamento de erro
    return a / b;
}
```

### Exemplo 2: Manipulação de Caracteres
```c
char proximoCaractere(char c) {
    return c + 1;
}

char caractereAnterior(char c) {
    return c - 1;
}

int ehVogal(char c) {
    c = maiusculo(c);
    return (c == 'A' || c == 'E' || c == 'I' || c == 'O' || c == 'U');
}
```

## 📌 Dicas Importantes

1. Sempre declare o tipo de retorno da função
2. Use nomes descritivos para as funções
3. Documente o propósito da função
4. Trate casos especiais e erros
5. Mantenha as funções pequenas e focadas em uma única tarefa

## 🔍 Boas Práticas

- Evite funções muito longas
- Use comentários para explicar lógica complexa
- Faça validação de parâmetros
- Retorne valores consistentes
- Mantenha um padrão de nomenclatura

---

[🔙 Voltar ao índice principal](../README.md)

<img width=100% src="https://capsule-render.vercel.app/api?type=waving&color=A8B9CC&height=120&section=footer"/> 