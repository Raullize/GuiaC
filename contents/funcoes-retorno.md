<img width=100% src="https://capsule-render.vercel.app/api?type=waving&color=A8B9CC&height=120&section=header"/>

# 🔄 Funções com Retorno em C

Neste guia, vamos explorar os conceitos de retorno em funções C, incluindo funções com e sem retorno.

## 📝 Tipos de Retorno

### Funções com Retorno
```c
int soma(int a, int b) {
    return a + b;  // Retorna um valor inteiro
}

float media(float a, float b) {
    return (a + b) / 2.0;  // Retorna um valor float
}

char proximoCaractere(char c) {
    return c + 1;  // Retorna um caractere
}
```

### Funções sem Retorno (void)
```c
void imprimirMensagem() {
    printf("Olá, mundo!\n");
    // Não possui return
}

void limparTela() {
    system("cls");
    // Não possui return
}
```

## 🔍 O Comando return

O comando `return` tem duas funções principais:
1. Retornar um valor para a função chamadora
2. Encerrar a execução da função

```c
int verificarIdade(int idade) {
    if (idade < 0) {
        return -1;  // Retorno antecipado em caso de erro
    }
    if (idade < 18) {
        return 0;   // Menor de idade
    }
    return 1;       // Maior de idade
}
```

## 📌 Múltiplos Retornos

Uma função pode ter múltiplos pontos de retorno:

```c
int maior(int a, int b) {
    if (a > b) {
        return a;
    } else {
        return b;
    }
}
```

## ⚠️ Considerações Importantes

1. O tipo de retorno deve corresponder ao declarado
2. Funções void não devem retornar valores
3. Evite múltiplos retornos quando possível
4. Sempre retorne valores consistentes
5. Documente o significado dos valores de retorno

## 🎯 Exemplos Práticos

### Exemplo 1: Função com Retorno Condicional
```c
int verificarParidade(int numero) {
    if (numero % 2 == 0) {
        return 1;  // Par
    }
    return 0;      // Ímpar
}
```

### Exemplo 2: Função sem Retorno
```c
void exibirMenu() {
    printf("1. Opção 1\n");
    printf("2. Opção 2\n");
    printf("3. Sair\n");
}
```

## 🔍 Boas Práticas

1. Use tipos de retorno apropriados
2. Documente o significado dos valores de retorno
3. Mantenha a consistência nos retornos
4. Evite retornos desnecessários
5. Trate todos os casos possíveis

---

[🔙 Voltar ao índice principal](../README.md)

<img width=100% src="https://capsule-render.vercel.app/api?type=waving&color=A8B9CC&height=120&section=footer"/> 