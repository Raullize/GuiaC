<img width=100% src="https://capsule-render.vercel.app/api?type=waving&color=A8B9CC&height=120&section=header"/>

# 🏗️ Entrada e Saída de Dados

## 📋 Funções de Entrada e Saída em C

A linguagem C não possui operadores integrados para entrada e saída de dados. Em vez disso, ela fornece uma biblioteca padrão chamada `stdio.h` (Standard Input/Output) que contém funções para operações de entrada e saída.

### 📤 Funções de Saída de Dados

#### 1️⃣ `printf()` - Saída Formatada

A função `printf()` é usada para exibir texto formatado na saída padrão (geralmente o console):

```c
#include <stdio.h>

int main() {
    int idade = 25;
    float altura = 1.75;
    char nome[] = "Carlos";
    
    printf("Nome: %s\n", nome);
    printf("Idade: %d anos\n", idade);
    printf("Altura: %.2f metros\n", altura);
    
    // Múltiplos valores em uma única chamada
    printf("Informações: %s, %d anos, %.2f metros\n", nome, idade, altura);
    
    return 0;
}
```

##### 📝 Especificadores de Formato para `printf()`

| Especificador | Tipo de Dado                        | Exemplo                      |
|---------------|-------------------------------------|------------------------------|
| `%d` ou `%i`  | Inteiro decimal com sinal           | `printf("%d", 42);`         |
| `%u`          | Inteiro decimal sem sinal           | `printf("%u", 42u);`        |
| `%o`          | Inteiro octal sem sinal             | `printf("%o", 42);`         |
| `%x`, `%X`    | Inteiro hexadecimal sem sinal       | `printf("%x", 42);`         |
| `%f`          | Ponto flutuante                     | `printf("%f", 3.14);`       |
| `%e`, `%E`    | Notação científica                  | `printf("%e", 3.14);`       |
| `%g`, `%G`    | Usa `%f` ou `%e` (o mais curto)     | `printf("%g", 3.14);`       |
| `%c`          | Caractere                           | `printf("%c", 'A');`        |
| `%s`          | String (cadeia de caracteres)       | `printf("%s", "texto");`    |
| `%p`          | Endereço de ponteiro                | `printf("%p", &variavel);`  |
| `%%`          | Símbolo de porcentagem literal      | `printf("%%");`             |

##### 🎚️ Modificadores de Formato

Você pode adicionar modificadores entre o `%` e o especificador para controlar a exibição:

```c
#include <stdio.h>

int main() {
    // Largura e preenchimento
    printf("[%5d]\n", 42);        // [   42] (alinhado à direita, largura 5)
    printf("[%-5d]\n", 42);       // [42   ] (alinhado à esquerda, largura 5)
    printf("[%05d]\n", 42);       // [00042] (preenchido com zeros)
    
    // Precisão para floats
    printf("[%.2f]\n", 3.14159);  // [3.14] (2 casas decimais)
    printf("[%8.2f]\n", 3.14159); // [    3.14] (largura 8, 2 casas decimais)
    
    // Modificadores para tipos de tamanho diferente
    printf("%ld\n", 1234567890L);       // long
    printf("%lld\n", 1234567890123LL);  // long long
    printf("%hd\n", (short)42);         // short
    
    return 0;
}
```

#### 2️⃣ `puts()` - Saída de Strings

A função `puts()` é usada para exibir uma string seguida de uma nova linha:

```c
#include <stdio.h>

int main() {
    puts("Olá, mundo!");  // Imprime "Olá, mundo!" e adiciona uma nova linha
    
    char mensagem[] = "Linguagem C";
    puts(mensagem);       // Imprime "Linguagem C" e adiciona uma nova linha
    
    return 0;
}
```

#### 3️⃣ `putchar()` - Saída de Caracteres

A função `putchar()` exibe um único caractere:

```c
#include <stdio.h>

int main() {
    putchar('A');      // Imprime 'A'
    putchar('\n');     // Nova linha
    
    char c = 'B';
    putchar(c);        // Imprime 'B'
    
    // Imprimindo uma string caractere por caractere
    char str[] = "Olá";
    for (int i = 0; str[i] != '\0'; i++) {
        putchar(str[i]);
    }
    
    return 0;
}
```

### 📥 Funções de Entrada de Dados

#### 1️⃣ `scanf()` - Entrada Formatada

A função `scanf()` é usada para ler dados formatados da entrada padrão (geralmente o teclado):

```c
#include <stdio.h>

int main() {
    int idade;
    float altura;
    char nome[50];
    
    printf("Digite seu nome: ");
    scanf("%s", nome);  // Lê uma palavra (para até no espaço em branco)
    
    printf("Digite sua idade: ");
    scanf("%d", &idade);
    
    printf("Digite sua altura (em metros): ");
    scanf("%f", &altura);
    
    printf("\nInformações:\n");
    printf("Nome: %s\n", nome);
    printf("Idade: %d anos\n", idade);
    printf("Altura: %.2f metros\n", altura);
    
    return 0;
}
```

**Observação importante**: Ao ler strings com `scanf()`, não é necessário usar o operador de endereço `&`, pois o nome de um array já é um ponteiro para o primeiro elemento. Para outros tipos de dados, como int ou float, o `&` é necessário.

#### 🚨 Problemas Comuns com `scanf()`

1. **Leitura de strings com espaços**:
   O `scanf("%s", str)` lê apenas até encontrar um espaço em branco.

   **Solução**: Use `fgets()` para ler linhas inteiras:

   ```c
   #include <stdio.h>
   #include <string.h>
   
   int main() {
       char nome_completo[50];
       
       printf("Digite seu nome completo: ");
       fgets(nome_completo, sizeof(nome_completo), stdin);
       
       // Remove o \n do final da string
       nome_completo[strcspn(nome_completo, "\n")] = '\0';
       
       printf("Nome completo: %s\n", nome_completo);
       
       return 0;
   }
   ```

2. **Buffer não limpo**:
   Ao misturar entradas numéricas com strings, o caractere de nova linha `\n` pode permanecer no buffer.

   **Solução**: Limpe o buffer com `getchar()` ou `fflush(stdin)` (não portável):

   ```c
   #include <stdio.h>
   
   int main() {
       int idade;
       char nome[50];
       
       printf("Digite sua idade: ");
       scanf("%d", &idade);
       
       // Limpa o buffer
       while (getchar() != '\n');
       
       printf("Digite seu nome: ");
       fgets(nome, sizeof(nome), stdin);
       
       printf("Idade: %d\n", idade);
       printf("Nome: %s", nome);
       
       return 0;
   }
   ```

#### 2️⃣ `gets()` - Entrada de Strings (OBSOLETO)

⚠️ **AVISO**: A função `gets()` é considerada insegura e foi removida do padrão C11 por não verificar limites de buffer.

**Alternativa segura**: Use `fgets()`:

```c
#include <stdio.h>
#include <string.h>

int main() {
    char texto[100];
    
    printf("Digite um texto: ");
    
    // Uso seguro de fgets no lugar de gets
    fgets(texto, sizeof(texto), stdin);
    
    // Remove o \n final se existir
    texto[strcspn(texto, "\n")] = '\0';
    
    printf("Você digitou: %s\n", texto);
    
    return 0;
}
```

#### 3️⃣ `getchar()` - Entrada de Caracteres

A função `getchar()` lê um único caractere da entrada padrão:

```c
#include <stdio.h>

int main() {
    char c;
    
    printf("Digite um caractere: ");
    c = getchar();
    
    printf("Caractere digitado: %c\n", c);
    
    // Leitura de múltiplos caracteres
    printf("Digite alguns caracteres (pressione Enter para finalizar):\n");
    
    while ((c = getchar()) != '\n') {
        printf("Caractere lido: %c\n", c);
    }
    
    return 0;
}
```

### 📂 Manipulação de Arquivos

C permite a leitura e escrita de dados em arquivos utilizando funções da biblioteca `stdio.h`:

#### 1️⃣ Abertura e Fechamento de Arquivos

```c
#include <stdio.h>

int main() {
    FILE *arquivo;
    
    // Abrir arquivo para escrita
    arquivo = fopen("dados.txt", "w");
    
    if (arquivo == NULL) {
        printf("Erro ao abrir o arquivo!\n");
        return 1;
    }
    
    // Escrever no arquivo
    fprintf(arquivo, "Exemplo de escrita em arquivo.\n");
    fprintf(arquivo, "Segunda linha do arquivo.\n");
    
    // Fechar arquivo
    fclose(arquivo);
    
    // Abrir arquivo para leitura
    arquivo = fopen("dados.txt", "r");
    
    if (arquivo == NULL) {
        printf("Erro ao abrir o arquivo para leitura!\n");
        return 1;
    }
    
    // Ler do arquivo
    char linha[100];
    while (fgets(linha, sizeof(linha), arquivo) != NULL) {
        printf("Lido do arquivo: %s", linha);
    }
    
    // Fechar arquivo
    fclose(arquivo);
    
    return 0;
}
```

#### 2️⃣ Modos de Abertura de Arquivo

| Modo | Descrição                                             |
|------|-------------------------------------------------------|
| `r`  | Abre para leitura (arquivo deve existir)              |
| `w`  | Abre para escrita (cria novo ou trunca existente)     |
| `a`  | Abre para acrescentar (cria novo ou adiciona ao fim)  |
| `r+` | Abre para leitura e escrita (arquivo deve existir)    |
| `w+` | Abre para leitura e escrita (cria novo ou trunca)     |
| `a+` | Abre para leitura e acréscimo (cria ou adiciona)      |
| `rb`, `wb`, etc. | Versões binárias dos modos acima          |

#### 3️⃣ Funções para Manipulação de Arquivos

| Função          | Descrição                                      |
|-----------------|------------------------------------------------|
| `fopen()`       | Abre um arquivo                                |
| `fclose()`      | Fecha um arquivo                               |
| `fprintf()`     | Escreve dados formatados em um arquivo         |
| `fscanf()`      | Lê dados formatados de um arquivo              |
| `fgets()`       | Lê uma linha de um arquivo                     |
| `fputs()`       | Escreve uma string em um arquivo               |
| `fgetc()`       | Lê um caractere de um arquivo                  |
| `fputc()`       | Escreve um caractere em um arquivo             |
| `fread()`       | Lê blocos de dados de um arquivo               |
| `fwrite()`      | Escreve blocos de dados em um arquivo          |
| `fseek()`       | Move o ponteiro de posição no arquivo          |
| `ftell()`       | Retorna a posição atual no arquivo             |
| `rewind()`      | Reposiciona o ponteiro para o início do arquivo|
| `remove()`      | Remove um arquivo                              |
| `rename()`      | Renomeia um arquivo                            |

#### 4️⃣ Exemplo de Manipulação de Arquivos Binários

```c
#include <stdio.h>

typedef struct {
    int id;
    char nome[50];
    float salario;
} Funcionario;

int main() {
    FILE *arquivo;
    Funcionario func1 = {1, "João Silva", 5000.0};
    Funcionario func2 = {2, "Maria Santos", 6000.0};
    Funcionario func_lido;
    
    // Escrever em arquivo binário
    arquivo = fopen("funcionarios.bin", "wb");
    
    if (arquivo == NULL) {
        printf("Erro ao abrir o arquivo para escrita!\n");
        return 1;
    }
    
    fwrite(&func1, sizeof(Funcionario), 1, arquivo);
    fwrite(&func2, sizeof(Funcionario), 1, arquivo);
    
    fclose(arquivo);
    
    // Ler do arquivo binário
    arquivo = fopen("funcionarios.bin", "rb");
    
    if (arquivo == NULL) {
        printf("Erro ao abrir o arquivo para leitura!\n");
        return 1;
    }
    
    printf("Dados lidos do arquivo binário:\n");
    
    while (fread(&func_lido, sizeof(Funcionario), 1, arquivo) == 1) {
        printf("ID: %d\n", func_lido.id);
        printf("Nome: %s\n", func_lido.nome);
        printf("Salário: %.2f\n\n", func_lido.salario);
    }
    
    fclose(arquivo);
    
    return 0;
}
```

### 🔄 Redirecionamento de Entrada e Saída

Em C, podemos redirecionar a entrada e saída padrão (stdin, stdout e stderr) para outros fluxos:

```c
#include <stdio.h>

int main() {
    // Redirecionando stdout para um arquivo
    FILE *arquivo_saida = fopen("saida.txt", "w");
    if (arquivo_saida != NULL) {
        int stdout_original = dup(fileno(stdout));  // Salva o stdout original
        
        // Redireciona stdout para o arquivo
        fflush(stdout);
        dup2(fileno(arquivo_saida), fileno(stdout));
        
        // Agora estas mensagens vão para o arquivo
        printf("Esta mensagem vai para o arquivo.\n");
        puts("Esta também vai para o arquivo.");
        
        // Restaura stdout
        fflush(stdout);
        dup2(stdout_original, fileno(stdout));
        close(stdout_original);
        
        // Esta mensagem vai para o console
        printf("Esta mensagem vai para o console.\n");
        
        fclose(arquivo_saida);
    }
    
    return 0;
}
```

**Observação**: O exemplo acima usa funções específicas do Unix/Linux como `dup` e `dup2`. Em Windows, seria necessário usar abordagens diferentes.

### 🧩 Formatação Avançada de Entrada/Saída

#### 1️⃣ Controle de Largura e Alinhamento

```c
#include <stdio.h>

int main() {
    // Tabela formatada
    printf("%-15s %-10s %-8s\n", "Nome", "Idade", "Altura");
    printf("%-15s %-10d %-8.2f\n", "Carlos", 25, 1.75);
    printf("%-15s %-10d %-8.2f\n", "Ana", 30, 1.62);
    printf("%-15s %-10d %-8.2f\n", "João da Silva", 45, 1.80);
    
    return 0;
}
```

Saída:
```
Nome            Idade      Altura  
Carlos          25         1.75    
Ana             30         1.62    
João da Silva   45         1.80    
```

#### 2️⃣ Formatação de Números

```c
#include <stdio.h>

int main() {
    int num = 42;
    double pi = 3.14159265;
    
    // Formatação de inteiros
    printf("Decimal:    %d\n", num);       // 42
    printf("Octal:      %o\n", num);       // 52
    printf("Hexadecimal: %x\n", num);      // 2a
    printf("Hexadecimal: %X\n", num);      // 2A
    
    // Formatação de números de ponto flutuante
    printf("Padrão:     %f\n", pi);        // 3.141593
    printf("Científico: %e\n", pi);        // 3.141593e+00
    printf("Científico: %E\n", pi);        // 3.141593E+00
    printf("Compacto:   %g\n", pi);        // 3.14159
    printf("Precisão:   %.10f\n", pi);     // 3.1415926500
    
    // Formatação monetária
    float valor = 1234.56;
    printf("Valor: R$%9.2f\n", valor);     // R$  1234.56
    
    return 0;
}
```

#### 3️⃣ Leitura Formatada Avançada

```c
#include <stdio.h>

int main() {
    char nome[50];
    int idade;
    float altura;
    char linha[100];
    
    // Ler até encontrar vírgula
    printf("Digite nome,idade,altura: ");
    scanf("%[^,],%d,%f", nome, &idade, &altura);
    
    printf("Nome: %s\n", nome);
    printf("Idade: %d\n", idade);
    printf("Altura: %.2f\n", altura);
    
    // Limpar buffer
    while (getchar() != '\n');
    
    // Ler uma linha e extrair informações dela
    printf("\nDigite 'nome:valor': ");
    fgets(linha, sizeof(linha), stdin);
    
    char chave[20], valor[20];
    if (sscanf(linha, "%[^:]:%s", chave, valor) == 2) {
        printf("Chave: %s\n", chave);
        printf("Valor: %s\n", valor);
    }
    
    return 0;
}
```

### 📊 Exemplo de Programa Completo

O programa abaixo demonstra várias técnicas de entrada e saída em um sistema simples de gerenciamento de contatos:

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_CONTATOS 100
#define MAX_NOME 50
#define MAX_EMAIL 50

typedef struct {
    int id;
    char nome[MAX_NOME];
    char email[MAX_EMAIL];
    long telefone;
} Contato;

void limparBuffer() {
    int c;
    while ((c = getchar()) != '\n' && c != EOF);
}

void adicionarContato(Contato contatos[], int *numContatos) {
    if (*numContatos >= MAX_CONTATOS) {
        printf("Limite de contatos atingido!\n");
        return;
    }
    
    Contato novo;
    novo.id = *numContatos + 1;
    
    printf("\n=== Novo Contato ===\n");
    
    printf("Nome: ");
    fgets(novo.nome, MAX_NOME, stdin);
    novo.nome[strcspn(novo.nome, "\n")] = '\0';  // Remove \n
    
    printf("Email: ");
    fgets(novo.email, MAX_EMAIL, stdin);
    novo.email[strcspn(novo.email, "\n")] = '\0';  // Remove \n
    
    printf("Telefone: ");
    scanf("%ld", &novo.telefone);
    limparBuffer();
    
    contatos[*numContatos] = novo;
    (*numContatos)++;
    
    printf("\nContato adicionado com sucesso!\n");
}

void listarContatos(Contato contatos[], int numContatos) {
    if (numContatos == 0) {
        printf("\nNenhum contato cadastrado.\n");
        return;
    }
    
    printf("\n=== Lista de Contatos ===\n");
    printf("%-5s %-30s %-30s %-15s\n", "ID", "Nome", "Email", "Telefone");
    printf("-------------------------------------------------------------------------------------\n");
    
    for (int i = 0; i < numContatos; i++) {
        printf("%-5d %-30s %-30s %-15ld\n", 
               contatos[i].id,
               contatos[i].nome, 
               contatos[i].email,
               contatos[i].telefone);
    }
}

void salvarContatos(Contato contatos[], int numContatos) {
    FILE *arquivo = fopen("contatos.dat", "wb");
    
    if (arquivo == NULL) {
        printf("\nErro ao abrir arquivo para salvar contatos!\n");
        return;
    }
    
    fwrite(&numContatos, sizeof(int), 1, arquivo);
    fwrite(contatos, sizeof(Contato), numContatos, arquivo);
    
    fclose(arquivo);
    printf("\nContatos salvos com sucesso!\n");
}

void carregarContatos(Contato contatos[], int *numContatos) {
    FILE *arquivo = fopen("contatos.dat", "rb");
    
    if (arquivo == NULL) {
        *numContatos = 0;
        return;
    }
    
    fread(numContatos, sizeof(int), 1, arquivo);
    fread(contatos, sizeof(Contato), *numContatos, arquivo);
    
    fclose(arquivo);
    printf("Contatos carregados com sucesso!\n");
}

int main() {
    Contato contatos[MAX_CONTATOS];
    int numContatos = 0;
    int opcao;
    
    carregarContatos(contatos, &numContatos);
    
    do {
        printf("\n=== Sistema de Contatos ===\n");
        printf("1. Adicionar Contato\n");
        printf("2. Listar Contatos\n");
        printf("3. Salvar e Sair\n");
        printf("Escolha uma opção: ");
        
        scanf("%d", &opcao);
        limparBuffer();
        
        switch (opcao) {
            case 1:
                adicionarContato(contatos, &numContatos);
                break;
            case 2:
                listarContatos(contatos, numContatos);
                break;
            case 3:
                salvarContatos(contatos, numContatos);
                printf("Até logo!\n");
                break;
            default:
                printf("Opção inválida!\n");
        }
    } while (opcao != 3);
    
    return 0;
}
```

Este programa demonstra:
- Leitura e escrita formatada com `printf()` e `scanf()`
- Leitura de strings completas com `fgets()`
- Manipulação de arquivos binários com `fread()` e `fwrite()`
- Formatação de saída em forma de tabela
- Limpeza de buffer de entrada
- Combinação de várias técnicas de E/S em um programa prático

---

[🔙 Voltar ao índice principal](../README.md)

<img width=100% src="https://capsule-render.vercel.app/api?type=waving&color=A8B9CC&height=120&section=footer"/> 