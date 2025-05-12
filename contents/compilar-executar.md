<img width=100% src="https://capsule-render.vercel.app/api?type=waving&color=A8B9CC&height=120&section=header"/>

# 📝 Como compilar e executar um programa em C

## 📋 Do código fonte ao programa executável

Diferentemente de linguagens interpretadas, programas em C precisam ser compilados antes de serem executados. Vamos entender o processo completo de transformação do código fonte em um programa executável.

### 🔄 O Processo de Compilação

A compilação de um programa em C envolve várias etapas, que transformam o código fonte legível por humanos em código de máquina executável:

#### 📊 Diagrama do Processo de Compilação

```
┌───────────────┐     ┌───────────────┐     ┌───────────────┐     ┌───────────────┐
│  Código Fonte │     │   Pré-proces- │     │  Compilação   │     │   Ligação     │
│   (.c)        │ --> │   samento     │ --> │  (Assembly)   │ --> │  (Linking)    │ --> Executável
│               │     │               │     │               │     │               │
└───────────────┘     └───────────────┘     └───────────────┘     └───────────────┘
```

#### 1️⃣ Pré-processamento

O pré-processador processa as diretivas que começam com `#`, como `#include`, `#define` e `#ifdef`:

```c
// Antes do pré-processamento
#include <stdio.h>
#define PI 3.14159

int main() {
    printf("O valor de PI é: %f\n", PI);
    return 0;
}
```

```c
// Após o pré-processamento (simplificado)
// Conteúdo do arquivo stdio.h é inserido aqui

int main() {
    printf("O valor de PI é: %f\n", 3.14159);
    return 0;
}
```

Para ver a saída do pré-processador usando GCC:

```bash
gcc -E programa.c -o programa.i
```

#### 2️⃣ Compilação

O compilador traduz o código pré-processado para código assembly, que é uma representação legível por humanos das instruções de máquina:

```bash
gcc -S programa.c -o programa.s
```

Exemplo de saída em assembly (x86):

```assembly
    .file   "programa.c"
    .section    .rodata
.LC1:
    .string "O valor de PI \351: %f\n"
    .text
    .globl  main
    .type   main, @function
main:
    pushq   %rbp
    movq    %rsp, %rbp
    movsd   .LC0(%rip), %xmm0
    leaq    .LC1(%rip), %rdi
    movl    $1, %eax
    call    printf@PLT
    movl    $0, %eax
    popq    %rbp
    ret
    .size   main, .-main
    .section    .rodata.cst8,"aM",@progbits,8
    .align 8
.LC0:
    .long   1374389535
    .long   1074339512
    .ident  "GCC: (GNU) 11.1.0"
    .section    .note.GNU-stack,"",@progbits
```

#### 3️⃣ Montagem (Assembly)

O código assembly é convertido em código objeto (código de máquina):

```bash
gcc -c programa.c -o programa.o
```

O arquivo `.o` resultante contém código de máquina, mas ainda não pode ser executado diretamente.

#### 4️⃣ Ligação (Linking)

O linker combina um ou mais arquivos de código objeto com as bibliotecas necessárias para criar o executável final:

```bash
gcc programa.o -o programa
```

Se o programa usar funções de bibliotecas como a biblioteca matemática (`math.h`), você precisa ligar explicitamente:

```bash
gcc programa.o -o programa -lm
```

### 🚀 Compilando com um Único Comando

Na prática, geralmente realizamos todas as etapas acima com um único comando:

```bash
gcc programa.c -o programa
```

ou com Clang:

```bash
clang programa.c -o programa
```

ou com MSVC (Windows):

```bash
cl programa.c
```

### 🔧 Opções de Compilação Importantes

#### Flags de Aviso (Warning)

```bash
# Ativar avisos básicos
gcc -Wall programa.c -o programa

# Avisos extras
gcc -Wall -Wextra programa.c -o programa

# Tratar avisos como erros
gcc -Wall -Werror programa.c -o programa
```

#### Otimização

```bash
# Sem otimização (melhor para debugging)
gcc -O0 programa.c -o programa

# Otimização balanceada (recomendada)
gcc -O2 programa.c -o programa

# Otimização máxima
gcc -O3 programa.c -o programa

# Otimizar para tamanho
gcc -Os programa.c -o programa
```

#### Padrões da Linguagem

```bash
# C90/C89 (ANSI C)
gcc -std=c90 programa.c -o programa

# C99
gcc -std=c99 programa.c -o programa

# C11
gcc -std=c11 programa.c -o programa

# C17/C18
gcc -std=c17 programa.c -o programa
```

#### Debugging

```bash
# Incluir informações de debugging
gcc -g programa.c -o programa
```

### 🔍 Compilando Múltiplos Arquivos

Para programas maiores, você normalmente terá múltiplos arquivos `.c`:

#### Estrutura de Arquivos:

```
projeto/
├── main.c
├── matematica.c
├── matematica.h
└── util.c
```

#### Compilando Separadamente:

```bash
# Compilar cada arquivo para código objeto
gcc -c main.c -o main.o
gcc -c matematica.c -o matematica.o
gcc -c util.c -o util.o

# Linkar todos os objetos em um executável
gcc main.o matematica.o util.o -o programa
```

#### Compilando Tudo de Uma Vez:

```bash
gcc main.c matematica.c util.c -o programa
```

### 📦 Usando Make para Automatizar

Para projetos maiores, o utilitário `make` simplifica o processo de compilação:

#### Exemplo de Makefile:

```makefile
CC = gcc
CFLAGS = -Wall -g

programa: main.o matematica.o util.o
	$(CC) main.o matematica.o util.o -o programa

main.o: main.c matematica.h
	$(CC) $(CFLAGS) -c main.c

matematica.o: matematica.c matematica.h
	$(CC) $(CFLAGS) -c matematica.c

util.o: util.c
	$(CC) $(CFLAGS) -c util.c

clean:
	rm -f *.o programa
```

Para compilar usando o Makefile:

```bash
make
```

Para limpar os arquivos compilados:

```bash
make clean
```

### 🏃‍♂️ Executando Programas em C

Após compilar com sucesso, você pode executar seu programa:

#### Linux/macOS:

```bash
./programa
```

#### Windows (CMD):

```cmd
programa.exe
```

ou simplesmente:

```cmd
programa
```

### 💾 Bibliotecas Estáticas e Dinâmicas

#### Bibliotecas Estáticas (`.a` no Linux/macOS, `.lib` no Windows):

1. Criar biblioteca:
   ```bash
   # Compilar os arquivos fonte para objetos
   gcc -c lib1.c lib2.c
   
   # Criar a biblioteca estática
   ar rcs libminhalib.a lib1.o lib2.o
   ```

2. Usar biblioteca:
   ```bash
   gcc programa.c -o programa -L. -lminhalib
   ```

#### Bibliotecas Dinâmicas (`.so` no Linux, `.dylib` no macOS, `.dll` no Windows):

1. Criar biblioteca:
   ```bash
   # Linux
   gcc -shared -fPIC lib1.c lib2.c -o libminhalib.so
   
   # macOS
   gcc -shared -fPIC lib1.c lib2.c -o libminhalib.dylib
   
   # Windows (MinGW)
   gcc -shared lib1.c lib2.c -o minhalib.dll
   ```

2. Usar biblioteca:
   ```bash
   # Linux/macOS
   gcc programa.c -o programa -L. -lminhalib
   
   # Windows (MinGW)
   gcc programa.c -o programa -L. -lminhalib
   ```

### 🔬 Depuração de Programas em C

Depois de compilar com a flag `-g`, você pode usar um depurador como o GDB:

```bash
# Compilar com informações de depuração
gcc -g programa.c -o programa

# Iniciar o depurador
gdb ./programa
```

Comandos básicos do GDB:

```
(gdb) break main            # Define um ponto de parada na função main
(gdb) run                   # Executa o programa até o próximo ponto de parada
(gdb) next                  # Executa a próxima linha (sem entrar em funções)
(gdb) step                  # Executa a próxima linha (entrando em funções)
(gdb) print variavel        # Mostra o valor de uma variável
(gdb) continue              # Continua a execução até o próximo ponto de parada
(gdb) quit                  # Sai do GDB
```

### 📊 Analisando o Executável

Para analisar o executável após a compilação:

```bash
# Mostrar símbolos (funções, variáveis globais)
nm programa

# Mostrar dependências de bibliotecas dinâmicas
ldd programa   # Linux
otool -L programa   # macOS
objdump -p programa | grep "DLL"   # Windows (MinGW)

# Mostrar informações sobre o formato do executável
file programa
```

### 🧠 Dicas para Compilação Eficiente

1. **Use flags de aviso**: `-Wall -Wextra` ajudam a encontrar problemas potenciais
2. **Compartilhe cabeçalhos corretamente**: Use guardas de inclusão para evitar inclusões múltiplas
3. **Divida programas grandes**: Organize em múltiplos arquivos `.c` com funções relacionadas
4. **Use um sistema de build**: Para projetos maiores, considere Make, CMake ou outros sistemas de build
5. **Entenda as flags de otimização**: Use `-O0` para debugging e `-O2` ou `-O3` para produção
6. **Mantenha a compatibilidade**: Especifique o padrão C que está usando com `-std=`

### 🚫 Erros Comuns de Compilação e Como Resolvê-los

#### Erro: "Undefined reference to [função]"

**Causa**: O linker não encontrou a implementação da função.

**Solução**:
- Verifique se esqueceu de incluir o arquivo `.c` que contém a função
- Verifique se está linkando todas as bibliotecas necessárias (ex: `-lm` para math.h)

#### Erro: "Implicit declaration of function [função]"

**Causa**: Usando uma função sem incluir o cabeçalho correto.

**Solução**:
- Adicione o `#include` apropriado
- Verifique a ortografia da função

#### Erro: "Expected [tipo] before [token]"

**Causa**: Erro de sintaxe no código.

**Solução**:
- Verifique os parênteses, chaves e ponto-e-vírgula
- Verifique a ordem das declarações

---

[🔙 Voltar ao índice principal](../README.md)

<img width=100% src="https://capsule-render.vercel.app/api?type=waving&color=A8B9CC&height=120&section=footer"/> 