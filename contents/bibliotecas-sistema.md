<img width=100% src="https://capsule-render.vercel.app/api?type=waving&color=A8B9CC&height=120&section=header"/>

# 📚 Bibliotecas do Sistema em C

Neste guia, vamos explorar o uso de bibliotecas do sistema em C, incluindo a limpeza da tela e inclusão de arquivos.

## 🧹 Limpando a Tela

Para limpar a tela do console em C, podemos usar a função `system()` da biblioteca `stdlib.h`. No Windows, usamos `"cls"`, e em sistemas Unix-like, usamos `"clear"`.

```c
#include <stdlib.h>

void limparTela() {
    #ifdef _WIN32
        system("cls");
    #else
        system("clear");
    #endif
}
```

## 📂 Incluindo Arquivos

### Arquivos de Cabeçalho (.h)

Arquivos de cabeçalho são usados para declarar funções, estruturas e constantes que serão utilizadas em múltiplos arquivos fonte.

```c
// exemplo.h
#ifndef EXEMPLO_H
#define EXEMPLO_H

// Declarações de funções
int soma(int a, int b);
void imprimeMensagem();

// Definições de constantes
#define PI 3.14159
#define MAX_TAMANHO 100

// Declarações de estruturas
struct Ponto {
    int x;
    int y;
};

#endif
```

### Incluindo Arquivos de Cabeçalho

```c
// main.c
#include <stdio.h>
#include "exemplo.h"

int main() {
    int resultado = soma(5, 3);
    printf("Resultado: %d\n", resultado);
    return 0;
}
```

## 🔧 Funções do Sistema

### system()

A função `system()` permite executar comandos do sistema operacional.

```c
#include <stdlib.h>

int main() {
    // Listar arquivos do diretório
    system("dir");  // Windows
    // system("ls");  // Unix-like
    
    return 0;
}
```

## 📌 Boas Práticas

1. **Proteção contra Inclusão Múltipla**
   - Use `#ifndef`, `#define` e `#endif` em arquivos de cabeçalho
   - Evita problemas de redefinição

2. **Organização de Arquivos**
   - Mantenha funções relacionadas no mesmo arquivo
   - Use nomes descritivos para arquivos
   - Documente o propósito de cada arquivo

3. **Inclusão de Bibliotecas**
   - Inclua apenas o necessário
   - Use `<>` para bibliotecas do sistema
   - Use `""` para seus próprios arquivos

## 🎯 Exemplos Práticos

### Exemplo 1: Sistema de Menu
```c
#include <stdio.h>
#include <stdlib.h>

void limparTela() {
    system("cls");  // Windows
}

void exibirMenu() {
    printf("1. Opção 1\n");
    printf("2. Opção 2\n");
    printf("3. Sair\n");
}

int main() {
    int opcao;
    
    do {
        limparTela();
        exibirMenu();
        scanf("%d", &opcao);
        
        switch(opcao) {
            case 1:
                printf("Opção 1 selecionada\n");
                break;
            case 2:
                printf("Opção 2 selecionada\n");
                break;
        }
    } while(opcao != 3);
    
    return 0;
}
```

### Exemplo 2: Módulo de Utilitários
```c
// utils.h
#ifndef UTILS_H
#define UTILS_H

void limparTela();
void pausarTela();
void exibirErro(const char* mensagem);

#endif

// utils.c
#include <stdio.h>
#include <stdlib.h>
#include "utils.h"

void limparTela() {
    system("cls");
}

void pausarTela() {
    printf("\nPressione ENTER para continuar...");
    getchar();
    getchar();
}

void exibirErro(const char* mensagem) {
    printf("ERRO: %s\n", mensagem);
    pausarTela();
}
```

## ⚠️ Considerações de Segurança

1. Evite usar `system()` com entrada do usuário
2. Valide todos os dados antes de usar em comandos do sistema
3. Use funções mais seguras quando disponíveis
4. Considere a portabilidade entre sistemas operacionais

---

[🔙 Voltar ao índice principal](../README.md)

<img width=100% src="https://capsule-render.vercel.app/api?type=waving&color=A8B9CC&height=120&section=footer"/> 