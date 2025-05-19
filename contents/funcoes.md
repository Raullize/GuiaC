<img width=100% src="https://capsule-render.vercel.app/api?type=waving&color=A8B9CC&height=120&section=header"/>

# 🔣 Funções em C

Neste guia, vamos explorar os conceitos básicos de funções em C, incluindo declaração, definição e uso.

## 📝 O que são Funções?

Funções são blocos de código que realizam tarefas específicas. Elas ajudam a organizar o código em partes menores e reutilizáveis.

## 🏗️ Estrutura Básica

```c
tipo_retorno nome_funcao(tipo_parametro1 param1, tipo_parametro2 param2) {
    // corpo da função
    return valor; // se houver retorno
}
```

## 📋 Declaração vs Definição

### Declaração (Protótipo)
```c
int soma(int a, int b);  // Apenas declara a existência da função
```

### Definição
```c
int soma(int a, int b) {  // Implementa a função
    return a + b;
}
```

## 🔍 Parâmetros

### Parâmetros Formais
```c
void funcao(int parametro1, float parametro2) {
    // uso dos parâmetros
}
```

### Parâmetros Reais
```c
int main() {
    funcao(10, 3.14);  // valores passados na chamada
    return 0;
}
```

## 📌 Boas Práticas

1. Use nomes descritivos para funções
2. Mantenha funções pequenas e focadas
3. Documente o propósito da função
4. Declare protótipos no início do arquivo
5. Use parâmetros com nomes significativos

## 🎯 Exemplos Básicos

### Exemplo 1: Função Simples
```c
void saudacao() {
    printf("Olá, mundo!\n");
}
```

### Exemplo 2: Função com Parâmetros
```c
void imprimeSoma(int a, int b) {
    printf("A soma é: %d\n", a + b);
}
```

## ⚠️ Considerações Importantes

1. Funções devem ter um propósito único
2. Evite funções muito longas
3. Use comentários para explicar lógica complexa
4. Mantenha um padrão de nomenclatura
5. Considere a reutilização do código

---

[🔙 Voltar ao índice principal](../README.md)

<img width=100% src="https://capsule-render.vercel.app/api?type=waving&color=A8B9CC&height=120&section=footer"/> 