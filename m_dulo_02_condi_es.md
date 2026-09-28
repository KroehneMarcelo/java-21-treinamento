---
marp: true
theme: default
paginate: true
---

# JAVA 21
## Módulo 02 — Condições e Fluxo de Controle

**Metodologia:** Desafio → Solução → Explicação → Evolução

---

# 🎯 Parte 1 — Desafio: Verificação de Idade

### Contexto
Precisamos validar se um cliente pode comprar um ingresso para um evento restrito.

### Regra
- Se a idade for maior ou igual a 18 anos, exibir `"Pessoa maior de idade"`.
- Caso contrário, exibir `"Pessoa menor de idade"`.

---

# 💡 Solução: Parte 1

```java
int idade = 20;

if (idade >= 18) {
    System.out.println("Pessoa maior de idade");
} else {
    System.out.println("Pessoa menor de idade");
}
```

---

# 🔍 Explicação: `if` e `else`

- **`if`**: Avalia uma expressão booleana. Se for `true`, executa o bloco de código.
- **`else`**: Executado quando a condição do `if` resulta em `false`.
- **Operador `>=`**: Verifica se o valor da esquerda é maior ou igual ao da direita.

```java
boolean eMaior = idade >= 18; // Avalia para true ou false
```

---

# 🎯 Parte 2 — Desafio: Atribuição (`=`) vs Comparação (`==`)

### Contexto
Verificar se o código de um produto cadastrado no sistema é igual a 10.

---

# 💡 Solução: Parte 2

```java
int codigo = 10;

if (codigo == 10) {
    System.out.println("Produto encontrado");
}
```

---

# 🔍 Explicação: `=` vs `==`

- **`=` (Atribuição):** Guarda um valor dentro de uma variável.
  ```java
  int codigo = 10; // Armazena 10 na variável codigo
  ```
- **`==` (Comparação):** Compara se dois valores primitivos são iguais e retorna um `boolean`.
  ```java
  codigo == 10 // Retorna true
  ```

---

# ⚠️ Erro Comum: Confundir Atribuição com Comparação

Em muitas linguagens isso causa bugs silenciosos. Em Java, o código abaixo **nem compila**:

```java
int codigo = 10;

// ERRO DE COMPILAÇÃO!
if (codigo = 10) { 
    System.out.println("Produto encontrado");
}
```

**Por quê?** O comando `(codigo = 10)` atribui o valor 10, mas o `if` exige uma expressão que resulte em `boolean` (`true`/`false`).

---

# 🎯 Parte 3 — Trabalhando com Variáveis Booleanas

Podemos armazenar o resultado de uma comparação diretamente em uma variável `boolean`:

```java
int codigo = 10;
boolean produtoEncontrado = codigo == 10;

if (produtoEncontrado) {
    System.out.println("Produto encontrado");
}
```

---

# 🔍 Explicação e Clean Code: Expressões Booleanas

### Evite redundâncias:
```java
// ❌ Ruim (Redundante)
if (produtoEncontrado == true) { ... }

// ✅ Limpo (Idiomático)
if (produtoEncontrado) { ... }
```

### Para negação (`!`):
```java
// ❌ Ruim
if (produtoEncontrado == false) { ... }

// ✅ Limpo (Operador de negação NOT)
if (!produtoEncontrado) {
    System.out.println("Produto não encontrado");
}
```

---

# 🎯 Parte 4 — Operador Lógico OR (`||`)

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

# 🎯 Parte 5 — Operador Lógico AND (`&&`)

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

# 🎯 Parte 6 — Combinação de Condições e Precedência

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