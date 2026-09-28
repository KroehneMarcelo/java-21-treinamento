---
marp: true
theme: default
paginate: true
---

# JAVA 21
## Módulo 02 — Condições e Fluxo de Controle

**Metodologia:** Desafio → Solução → Explicação → Evolução

---

# 🎯 Parte 1 — Desafio: Verificação de Igualdade

### Contexto
Precisamos validar se um código de acesso digitado pelo usuário é igual ao código correto armazenado no sistema.

### Regra
- Usar `codigoDigitado` como variável de entrada do usuário.
- Se o código digitado for **igual** a 1234, exibir `"Acesso permitido"`.
- Caso contrário, exibir `"Acesso negado"`.

---

# 💡 Solução: Parte 1

```java
int codigoDigitado = 1234;
int codigoCorreto = 1234;

if (codigoDigitado == codigoCorreto) {
    System.out.println("Acesso permitido");
} else {
    System.out.println("Acesso negado");
}
```

---

# 🔍 Explicação: `if` e `else`

- **`if`**: Avalia uma expressão booleana. Se for `true`, executa o bloco de código.
- **`else`**: Executado quando a condição do `if` resulta em `false`.
- **Operador `==`**: Compara se dois **valores primitivos** são iguais, retornando `true` ou `false`.

```java
boolean acessoValido = codigoDigitado == codigoCorreto; // Avalia para true ou false
```

---

# 🎯 Parte 2 — Explicação: Operadores Relacionais

Os operadores relacionais comparam dois valores e retornam um `boolean` (`true` ou `false`).

### Operadores Disponíveis:

| Operador | Nome | Exemplo | Resultado |
| :---: | :--- | :--- | :---: |
| `==` | Igual | `10 == 10` | `true` |
| `!=` | Diferente | `10 != 5` | `true` |
| `>` | Maior que | `10 > 5` | `true` |
| `<` | Menor que | `10 < 5` | `false` |
| `>=` | Maior ou igual | `10 >= 10` | `true` |
| `<=` | Menor ou igual | `10 <= 5` | `false` |

---

# 💡 Exemplos Práticos: Operadores Relacionais

```java
int idade = 25;
int limite = 18;

idade > limite    // true (25 é maior que 18)
idade < limite    // false (25 não é menor que 18)
idade == limite   // false (25 não é igual a 18)
idade != limite   // true (25 é diferente de 18)
idade >= limite   // true (25 é maior ou igual a 18)
idade <= limite   // false (25 não é menor ou igual a 18)
```

---

# ⚠️ Erro Comum: Confundir Atribuição (`=`) com Comparação (`==`)

Em muitas linguagens isso causa bugs silenciosos. Em Java, o código abaixo **nem compila**:

```java
int codigo = 10;

// ERRO DE COMPILAÇÃO!
if (codigo = 10) {
    System.out.println("Código correto");
}
```

**Por quê?** O comando `(codigo = 10)` atribui o valor 10, mas o `if` exige uma expressão que resulte em `boolean` (`true`/`false`).

### Comparação Correta:

```java
// ✅ Correto: == compara, não atribui
if (codigo == 10) {
    System.out.println("Código correto");
}
```

---

# 🎯 Parte 3 — Desafio: Verificação de Idade

### Contexto
Precisamos validar se um cliente pode comprar um ingresso para um evento restrito.

### Regra
- Se a idade for maior ou igual a 18 anos, exibir `"Pessoa maior de idade"`.
- Caso contrário, exibir `"Pessoa menor de idade"`.

---

# 💡 Solução: Parte 3

```java
int idade = 20;

if (idade >= 18) {
    System.out.println("Pessoa maior de idade");
} else {
    System.out.println("Pessoa menor de idade");
}
```

---

# 🎯 Parte 4 — Trabalhando com Variáveis Booleanas

Podemos armazenar o resultado de uma comparação diretamente em uma variável `boolean`:

```java
int idade = 20;
boolean ehMaiorDeIdade = idade >= 18;

if (ehMaiorDeIdade) {
    System.out.println("Pessoa maior de idade");
}
```

---

# 🔍 Explicação e Clean Code: Expressões Booleanas

### Evite redundâncias:

```java
// ❌ Ruim (Redundante)
if (ehMaiorDeIdade == true) { ... }

// ✅ Limpo (Idiomático)
if (ehMaiorDeIdade) { ... }
```

### Para negação (`!`):

```java
// ❌ Ruim
if (ehMaiorDeIdade == false) { ... }

// ✅ Limpo (Operador de negação NOT)
if (!ehMaiorDeIdade) {
    System.out.println("Pessoa menor de idade");
}
```

---

# 🎯 Parte 5 — Operador Lógico OR (`||`)

### Contexto
Um produto ganha desconto especial se seu código for 10 **OU** 11.

```java
int codigo = 10;

if (codigo == 10 || codigo == 11) {
    System.out.println("Produto com desconto!");
}
```

### Tabela Verdade — OR (`||`)

| Condição A | Condição B | Resultado (`A \|\| B`) |
| :---: | :---: | :---: |
| `true` | `false` | **`true`** |
| `false` | `true` | **`true`** |
| `false` | `false` | **`false`** |

---

# 🎯 Parte 6 — Operador Lógico AND (`&&`)

### Contexto
Um usuário só pode acessar o sistema se estiver **ativo** **E** tiver **permissão**.

```java
boolean usuarioAtivo = true;
boolean possuiPermissao = true;

if (usuarioAtivo && possuiPermissao) {
    System.out.println("Acesso permitido");
}
```

### Tabela Verdade — AND (`&&`)

| Condição A | Condição B | Resultado (`A && B`) |
| :---: | :---: | :---: |
| `true` | `true` | **`true`** |
| `true` | `false` | **`false`** |
| `false` | `true` | **`false`** |

---

# 🎯 Parte 7 — Combinação de Condições e Precedência

### Contexto
Acesso permitido se:
1. Estiver ativo **E** possuir permissão; **OU**
2. For Administrador.

```java
boolean usuarioAtivo = true;
boolean possuiPermissao = false;
boolean administrador = false;

if ((usuarioAtivo && possuiPermissao) || administrador) {
    System.out.println("Acesso permitido");
}
```

---

# 🔍 Explicação: Uso de Parênteses

Assim como na matemática, os parênteses `()` definem a ordem de avaliação:

1. Primeiro avalia: `(usuarioAtivo && possuiPermissao)`
2. Depois avalia o resultado com: `|| administrador`

**Boas práticas:** Mesmo quando a precedência padrão da linguagem funcionar, use parênteses para deixar a **intenção clara** para quem lê o código.

---

# 🚀 Evolução: Resumo de Clean Code em Condicionais

| Evitar (Confuso/Verboso) | Preferir (Limpo e Claro) |
| :--- | :--- |
| `if (ativo == true)` | `if (ativo)` |
| `if (ativo == false)` | `if (!ativo)` |
| `if (a == true && b == true)` | `if (a && b)` |

> *Clean code não é sobre economizar letras, é sobre comunicar intenção.*

---

# 🚀 Exercício Prático Final

Crie um programa que valide se um produto pode ser vendido.

### Regras de Negócio:
1. O produto deve estar **disponível** (`boolean`).
2. A quantidade em estoque deve ser **maior que zero** (`int`).
3. O preço deve ser **maior ou igual a 10.00** (`double`).

### Condições de Venda:
- Venda permitida se **todas as três condições** forem verdadeiras.
- Use operadores relacionais e lógicos apropriados.
- Aplique as regras de **Clean Code** aprendidas.
