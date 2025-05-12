<img width=100% src="https://capsule-render.vercel.app/api?type=waving&color=A8B9CC&height=120&section=header"/>

# 🔄 Funções com Retorno e sem Retorno

## 📋 Compreendendo os Tipos de Funções em C

Em C, as funções podem ser categorizadas em dois tipos principais com base no valor de retorno: funções com retorno e funções sem retorno (void). Entender essas categorias é fundamental para criar programas eficientes e bem estruturados.

### 🔄 Funções com Retorno

As funções com retorno devolvem um valor após a execução. Este valor pode ser utilizado em expressões, atribuições ou outras operações no programa.

#### 1️⃣ Sintaxe Básica

```c
tipo_de_retorno nome_da_funcao(parametros) {
    // Corpo da função
    return valor;  // Valor deve ser compatível com tipo_de_retorno
}
```

#### 2️⃣ Tipos de Retorno Comuns

| Tipo de Retorno | Descrição                                         | Exemplo                    |
|-----------------|---------------------------------------------------|----------------------------|
| `int`           | Retorna um valor inteiro                          | Contagem, status, códigos  |
| `float/double`  | Retorna um número de ponto flutuante              | Cálculos matemáticos       |
| `char`          | Retorna um caractere                              | Processamento de texto     |
| `char*`         | Retorna um ponteiro para uma string               | Manipulação de strings     |
| `void*`         | Retorna um ponteiro genérico                      | Alocação de memória        |
| Struct/tipos personalizados | Retorna estruturas de dados complexas  | Objetos, registros         |

#### 3️⃣ Exemplos Práticos

```c
#include <stdio.h>
#include <stdlib.h>
#include <math.h>

// Retorno inteiro
int soma(int a, int b) {
    return a + b;
}

// Retorno de ponto flutuante
double calcular_media(double valores[], int tamanho) {
    if (tamanho <= 0) return 0.0;
    
    double soma = 0.0;
    for (int i = 0; i < tamanho; i++) {
        soma += valores[i];
    }
    
    return soma / tamanho;
}

// Retorno de caractere
char obter_primeira_letra(const char* nome) {
    if (nome == NULL || nome[0] == '\0')
        return '\0';  // Retorna caractere nulo para string vazia
    
    return nome[0];
}

// Retorno de ponteiro
char* criar_saudacao(const char* nome) {
    if (nome == NULL) return NULL;
    
    // Aloca memória para "Olá, " + nome + "!" + '\0'
    char* saudacao = (char*)malloc(strlen("Olá, ") + strlen(nome) + 2);
    
    if (saudacao != NULL) {
        strcpy(saudacao, "Olá, ");
        strcat(saudacao, nome);
        strcat(saudacao, "!");
    }
    
    return saudacao;  // Lembre-se: o chamador deve liberar esta memória!
}

int main() {
    // Uso de função com retorno inteiro
    int resultado = soma(5, 7);
    printf("Soma: %d\n", resultado);
    
    // Uso de função com retorno de ponto flutuante
    double notas[] = {7.5, 8.0, 6.5, 9.0};
    printf("Média: %.2f\n", calcular_media(notas, 4));
    
    // Uso de função com retorno de caractere
    char inicial = obter_primeira_letra("Carlos");
    printf("Inicial: %c\n", inicial);
    
    // Uso de função com retorno de ponteiro
    char* mensagem = criar_saudacao("Maria");
    if (mensagem != NULL) {
        printf("%s\n", mensagem);
        free(mensagem);  // Libera a memória alocada
    }
    
    return 0;
}
```

#### 4️⃣ Regras Importantes

1. **Compatibilidade de tipos**: O valor retornado deve ser compatível com o tipo de retorno declarado
2. **Conversão implícita**: C permite algumas conversões automáticas, mas é uma boa prática usar tipos consistentes
3. **Múltiplos `return`**: Uma função pode ter vários comandos `return`, mas a execução termina no primeiro encontrado
4. **Valores de retorno devem ser verificados**: Sempre verifique valores de retorno, especialmente para funções que podem falhar

```c
#include <stdio.h>

int dividir(int a, int b, int* resultado) {
    if (b == 0) {
        return 0;  // Código de erro: divisão por zero
    }
    
    *resultado = a / b;
    return 1;  // Código de sucesso
}

int main() {
    int a = 10, b = 0, resultado;
    
    // Verifica o valor de retorno
    if (dividir(a, b, &resultado)) {
        printf("Resultado da divisão: %d\n", resultado);
    } else {
        printf("Erro: Divisão por zero!\n");
    }
    
    return 0;
}
```

### 🚫 Funções sem Retorno (void)

Funções `void` não retornam nenhum valor. Elas são usadas para executar ações sem necessidade de fornecer um resultado.

#### 1️⃣ Sintaxe Básica

```c
void nome_da_funcao(parametros) {
    // Corpo da função
    // Não há comando 'return' com valor
    return;  // Opcional - encerra a função
}
```

#### 2️⃣ Casos de Uso Comuns

- Exibir informações na tela
- Modificar variáveis por referência (usando ponteiros)
- Executar ações sem necessidade de resultado (ex: salvar dados)
- Inicializar estruturas de dados
- Liberar recursos

#### 3️⃣ Exemplos Práticos

```c
#include <stdio.h>

// Função void para exibir uma mensagem
void exibir_mensagem(const char* mensagem) {
    printf("%s\n", mensagem);
}

// Função void para inicializar um array
void inicializar_array(int arr[], int tamanho, int valor) {
    for (int i = 0; i < tamanho; i++) {
        arr[i] = valor;
    }
}

// Função void que modifica uma variável por referência
void duplicar_valor(int* numero) {
    if (numero != NULL) {
        *numero *= 2;
    }
}

// Função void para desenhar uma linha
void desenhar_linha(int comprimento, char caractere) {
    for (int i = 0; i < comprimento; i++) {
        putchar(caractere);
    }
    putchar('\n');
}

int main() {
    exibir_mensagem("Programa iniciado");
    
    desenhar_linha(30, '=');
    
    int numeros[5];
    inicializar_array(numeros, 5, 10);
    
    printf("Array inicializado: ");
    for (int i = 0; i < 5; i++) {
        printf("%d ", numeros[i]);
    }
    printf("\n");
    
    int valor = 5;
    printf("Valor original: %d\n", valor);
    duplicar_valor(&valor);
    printf("Valor duplicado: %d\n", valor);
    
    desenhar_linha(30, '=');
    exibir_mensagem("Programa finalizado");
    
    return 0;
}
```

#### 4️⃣ Comando `return` em Funções void

Embora funções `void` não retornem valores, o comando `return` (sem valor) pode ser usado para encerrar a função prematuramente:

```c
#include <stdio.h>

void processar_idade(int idade) {
    if (idade < 0) {
        printf("Erro: idade não pode ser negativa!\n");
        return;  // Encerra a função
    }
    
    printf("Idade válida: %d anos\n", idade);
    
    if (idade < 18) {
        printf("Menor de idade\n");
    } else {
        printf("Maior de idade\n");
    }
}

int main() {
    processar_idade(25);  // Idade válida
    processar_idade(-5);  // Idade inválida
    
    return 0;
}
```

### 🔄 Quando Usar Cada Tipo de Função

#### 1️⃣ Use Funções com Retorno Quando:

- A função precisa fornecer um resultado que será usado em outro lugar
- Você precisa verificar se uma operação foi bem-sucedida
- A função calcula um valor baseado nos parâmetros
- A função busca ou gera informações que serão utilizadas

#### 2️⃣ Use Funções void Quando:

- A função realiza uma ação sem necessidade de fornecer um resultado
- A função modifica dados por referência (via ponteiros)
- A função apenas exibe informações
- A função realiza operações de entrada/saída sem processamento
- A função gerencia recursos (inicialização, liberação)

### 🔄 Combinando os Dois Tipos

É comum combinar funções de ambos os tipos para criar um programa bem estruturado:

```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

// Função com retorno para gerar número aleatório
int gerar_numero_aleatorio(int min, int max) {
    return min + rand() % (max - min + 1);
}

// Função void para exibir menu
void exibir_menu() {
    printf("\n=== Menu do Jogo ===\n");
    printf("1. Jogar\n");
    printf("2. Ver Pontuação\n");
    printf("3. Sair\n");
    printf("Escolha uma opção: ");
}

// Função com retorno para obter escolha do usuário
int obter_escolha() {
    int escolha;
    scanf("%d", &escolha);
    return escolha;
}

// Função void para processar a jogada
void jogar(int* pontuacao) {
    int numero_secreto = gerar_numero_aleatorio(1, 100);
    int tentativa, tentativas = 0;
    
    printf("\n*** Novo Jogo ***\n");
    printf("Adivinhe o número entre 1 e 100\n");
    
    do {
        printf("Tentativa: ");
        scanf("%d", &tentativa);
        tentativas++;
        
        if (tentativa < numero_secreto) {
            printf("Muito baixo! Tente um número maior.\n");
        } else if (tentativa > numero_secreto) {
            printf("Muito alto! Tente um número menor.\n");
        }
    } while (tentativa != numero_secreto);
    
    printf("Parabéns! Você acertou em %d tentativas!\n", tentativas);
    *pontuacao += 100 / tentativas;
}

// Função void para exibir pontuação
void mostrar_pontuacao(int pontuacao) {
    printf("\n*** Pontuação Atual ***\n");
    printf("Sua pontuação: %d pontos\n", pontuacao);
}

int main() {
    int pontuacao = 0;
    int opcao;
    
    srand(time(NULL));  // Inicializa o gerador de números aleatórios
    
    do {
        // Usa funções void para interface
        exibir_menu();
        
        // Usa função com retorno para capturar entrada
        opcao = obter_escolha();
        
        switch (opcao) {
            case 1:
                // Usa função void que modifica por referência
                jogar(&pontuacao);
                break;
            case 2:
                // Usa função void para exibição
                mostrar_pontuacao(pontuacao);
                break;
            case 3:
                printf("Obrigado por jogar! Pontuação final: %d\n", pontuacao);
                break;
            default:
                printf("Opção inválida! Tente novamente.\n");
        }
    } while (opcao != 3);
    
    return 0;
}
```

### 🧠 Boas Práticas

1. **Nomes claros**: Use verbos para funções `void` (ex: `exibir_mensagem`, `inicializar_dados`) e substantivos ou adjetivos para funções com retorno (ex: `calcular_media`, `eh_valido`)

2. **Uma responsabilidade**: Cada função deve fazer uma única coisa bem feita

3. **Tamanho adequado**: Funções não devem ser muito longas; se uma função está muito grande, divida-a em funções menores

4. **Documentação**: Comente o propósito da função, parâmetros esperados e valores de retorno

5. **Tratamento de erros**: Para funções com retorno, defina claramente como os erros são indicados (códigos de erro, valores especiais)

6. **Verificação de entradas**: Valide os parâmetros no início da função

7. **Consistência**: Mantenha um padrão consistente para funções similares

### 🔄 Resumo

```
┌───────────────────────┬─────────────────────────────────────────┐
│ Funções com Retorno   │ Funções void (sem Retorno)              │
├───────────────────────┼─────────────────────────────────────────┤
│ - Retornam um valor   │ - Não retornam valor                    │
│ - Usadas em expressões│ - Executam ações                        │
│ - Para cálculos       │ - Para exibição e interface             │
│ - Para validações     │ - Para modificações via ponteiros       │
│ - Para recuperar dados│ - Para inicialização/liberação          │
└───────────────────────┴─────────────────────────────────────────┘
```

Em resumo, funções com retorno e funções void são ferramentas complementares na programação em C. A escolha entre elas depende do propósito específico da função e de como ela será utilizada no contexto do programa. Um bom design de software geralmente envolve o uso adequado de ambos os tipos.

---

[🔙 Voltar ao índice principal](../README.md)

<img width=100% src="https://capsule-render.vercel.app/api?type=waving&color=A8B9CC&height=120&section=footer"/> 