---
marp: true
theme: default
paginate: true
---

# JAVA 21
## Módulo 02 — Condições e Fluxo de Controle

**Metodologia:** Desafio → Solução → Explicação → Novo Desafio → Solução com Explicação

---

# 🎯 DESAFIO 1 — Verificação de Igualdade

### Contexto
Um sistema de controle de acesso precisa validar códigos.

### O que fazer:
Você recebeu um código digitado pelo usuário e um código correto armazenado no sistema. Precisa criar um programa que **compare esses dois códigos** e mostre se o acesso é permitido ou negado.

**Dados:**
- `codigoDigitado = 1234`
- `codigoCorreto = 1234`

**Saída esperada:**
- Se forem iguais: `"Acesso permitido"`
- Se forem diferentes: `"Acesso negado"`

---

# 💡 SOLUÇÃO 1 — Verificação de Igualdade

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

# 🔍 EXPLICAÇÃO 1: `if`, `else` e Operador `==`

### O que aconteceu?

- **`if`**: Avalia uma expressão booleana. Se for `true`, executa o bloco de código.
- **`else`**: Executado quando a condição do `if` resulta em `false`.
- **Operador `==`**: Compara se dois **valores primitivos** são iguais, retornando `true` ou `false`.

### Exemplo de armazenamento em variável booleana:

```java
int codigoDigitado = 1234;
int codigoCorreto = 1234;
boolean acessoValido = codigoDigitado == codigoCorreto; // Resulta em: true
```

### Fluxo de Execução:
1. Avalia: `1234 == 1234`
2. Resultado: `true`
3. Executa o bloco dentro do `if`
4. Imprime: `"Acesso permitido"`

---

# ⚠️ ERRO COMUM: Confundir Atribuição (`=`) com Comparação (`==`)

Em muitas linguagens isso causa bugs silenciosos. Em Java, o código abaixo **nem compila**:

```java
int codigo = 10;

// ERRO DE COMPILAÇÃO!
if (codigo = 10) {
    System.out.println("Código correto");
}
```

**Por quê?** O comando `(codigo = 10)` **atribui** o valor 10, mas o `if` exige uma expressão que resulte em `boolean` (`true`/`false`).

### Comparação Correta:

```java
// ✅ Correto: == compara, não atribui
if (codigo == 10) {
    System.out.println("Código correto");
}
```

---

# 🎯 NOVO DESAFIO 1 — Aplicar o Conceito

### Contexto
Você está desenvolvendo um login de segurança onde a senha deve ser validada.

### O que fazer:
Crie um programa que:
1. Armazene uma senha correta em uma variável.
2. Armazene uma senha digitada pelo usuário em outra variável.
3. Compare as duas senhas.
4. Exiba:
   - `"Senha correta!"` se forem iguais
   - `"Senha incorreta!"` se forem diferentes

**Teste com:**
- `senhaCorreta = "abc123"`
- `senhaDigitada = "abc123"`

---

# 💡 SOLUÇÃO DO NOVO DESAFIO 1

```java
String senhaCorreta = "abc123";
String senhaDigitada = "abc123";

if (senhaDigitada.equals(senhaCorreta)) {
    System.out.println("Senha correta!");
} else {
    System.out.println("Senha incorreta!");
}
```

### ⚠️ OBSERVAÇÃO IMPORTANTE:

Para comparar `String`s em Java, devemos usar o método `.equals()`, não `==`:

```java
String senhaCorreta = "abc123";
String senhaDigitada = "abc123";

// ❌ ERRADO (compara referência, não conteúdo)
if (senhaDigitada == senhaCorreta) { ... }

// ✅ CORRETO (compara conteúdo)
if (senhaDigitada.equals(senhaCorreta)) { ... }
```

**Por quê?** Porque `String` é um objeto, não um valor primitivo. O `==` compara referências na memória, não o conteúdo das strings.

---

# 🎯 PARTE 2 — DESAFIO: Operadores Relacionais

### Contexto
Um sistema de vendas precisa validar a idade de clientes para saber se podem comprar certos produtos.

### O que fazer:
Você tem uma idade armazenada em uma variável e precisa:
1. Verificar se é **maior ou igual a 18**
2. Exibir mensagens diferentes para maior e menor de idade

**Dados:**
- `idade = 20`

**Saída esperada:**
- Se age ≥ 18: `"Pessoa maior de idade"`
- Se age < 18: `"Pessoa menor de idade"`

---

# 💡 SOLUÇÃO 2 — Operadores Relacionais

```java
int idade = 20;

if (idade >= 18) {
    System.out.println("Pessoa maior de idade");
} else {
    System.out.println("Pessoa menor de idade");
}
```

---

# 🔍 EXPLICAÇÃO 2: Operadores Relacionais

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

### Exemplos Práticos:

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

# 🎯 NOVO DESAFIO 2 — Aplicar Operadores Relacionais

### Contexto
Um e-commerce valida se o produto tem preço acessível.

### O que fazer:
Crie um programa que:
1. Armazene um preço de produto
2. Armazene um orçamento do cliente
3. Verifique se o cliente pode comprar (orçamento ≥ preço)
4. Exiba:
   - `"Pode comprar!"` se o orçamento for suficiente
   - `"Orçamento insuficiente"` caso contrário

**Teste com:**
- `preco = 150.00`
- `orcamento = 200.00`

**Desafio extra:** Teste também com valores diferentes!

---

# 💡 SOLUÇÃO DO NOVO DESAFIO 2

```java
double preco = 150.00;
double orcamento = 200.00;

if (orcamento >= preco) {
    System.out.println("Pode comprar!");
} else {
    System.out.println("Orçamento insuficiente");
}
```

### Análise:
- `200.00 >= 150.00` → `true`
- Executa o primeiro bloco
- Imprime: `"Pode comprar!"`

### Com Variável Booleana (Clean Code):

```java
double preco = 150.00;
double orcamento = 200.00;
boolean podeComprar = orcamento >= preco;

if (podeComprar) {
    System.out.println("Pode comprar!");
} else {
    System.out.println("Orçamento insuficiente");
}
```

---

# 🎯 PARTE 3 — DESAFIO: Operadores Lógicos OR e AND

### Contexto
Um produto recebe desconto especial se atende a certos critérios.

### O que fazer (Desafio OR):
Um produto ganha desconto se o código for **10 OU 11**.

**Crie um programa que:**
1. Receba um código de produto
2. Verifique se o código é 10 **OU** 11
3. Exiba:
   - `"Desconto aplicado!"` se atender
   - `"Sem desconto"` se não atender

**Teste com:**
- `codigo = 10`

---

# 💡 SOLUÇÃO 3 — Operador Lógico OR (`||`)

```java
int codigo = 10;

if (codigo == 10 || codigo == 11) {
    System.out.println("Desconto aplicado!");
} else {
    System.out.println("Sem desconto");
}
```

---

# 🔍 EXPLICAÇÃO 3: Operador Lógico OR (`||`)

O operador `||` (OR) retorna `true` se **pelo menos uma** das condições for verdadeira.

### Tabela Verdade — OR (`||`)

| Condição A | Condição B | Resultado (`A \|\| B`) |
| :---: | :---: | :---: |
| `true` | `true` | **`true`** |
| `true` | `false` | **`true`** |
| `false` | `true` | **`true`** |
| `false` | `false` | **`false`** |

### Fluxo do Exemplo:
- `codigo == 10` → `true`
- `true || codigo == 11` → **`true`** (nem precisa avaliar a segunda condição)
- Executa o bloco do `if`

---

# 🎯 NOVO DESAFIO 3A — Aplicar OR

### Contexto
Um sistema de acesso permite que clientes entrem se forem **VIP OU possuírem cupom de desconto**.

### O que fazer:
Crie um programa que:
1. Armazene se o cliente é VIP (`boolean`)
2. Armazene se o cliente tem cupom (`boolean`)
3. Verifique se pelo menos um deles é verdadeiro
4. Exiba:
   - `"Bem-vindo!"` se puder entrar
   - `"Acesso negado"` caso contrário

**Teste com:**
- `ehVip = false`
- `temCupom = true`

---

# 💡 SOLUÇÃO DO NOVO DESAFIO 3A

```java
boolean ehVip = false;
boolean temCupom = true;

if (ehVip || temCupom) {
    System.out.println("Bem-vindo!");
} else {
    System.out.println("Acesso negado");
}
```

### Análise:
- `ehVip` → `false`
- `temCupom` → `true`
- `false || true` → **`true`**
- Imprime: `"Bem-vindo!"`

### Por que o OR foi perfeito aqui?
Porque o cliente precisa atender **PELO MENOS UM** critério para entrar. Se fosse AND, precisaria atender AMBOS.

---

# 🎯 DESAFIO 3B — Operador Lógico AND

### Contexto
Um usuário só pode acessar um sistema confidencial se estiver **ATIVO E tiver PERMISSÃO**.

### O que fazer:
Crie um programa que:
1. Armazene se o usuário está ativo
2. Armazene se o usuário tem permissão
3. Verifique se **AMBAS** as condições são verdadeiras
4. Exiba:
   - `"Acesso permitido"` se ambas forem true
   - `"Acesso negado"` caso contrário

**Teste com:**
- `usuarioAtivo = true`
- `possuiPermissao = true`

---

# 💡 SOLUÇÃO 3B — Operador Lógico AND (`&&`)

```java
boolean usuarioAtivo = true;
boolean possuiPermissao = true;

if (usuarioAtivo && possuiPermissao) {
    System.out.println("Acesso permitido");
} else {
    System.out.println("Acesso negado");
}
```

---

# 🔍 EXPLICAÇÃO 3B: Operador Lógico AND (`&&`)

O operador `&&` (AND) retorna `true` se **TODAS** as condições forem verdadeiras.

### Tabela Verdade — AND (`&&`)

| Condição A | Condição B | Resultado (`A && B`) |
| :---: | :---: | :---: |
| `true` | `true` | **`true`** |
| `true` | `false` | **`false`** |
| `false` | `true` | **`false`** |
| `false` | `false` | **`false`** |

### Fluxo do Exemplo:
- `usuarioAtivo` → `true`
- `possuiPermissao` → `true`
- `true && true` → **`true`**
- Executa o bloco do `if`

### Diferença OR vs AND:
- **OR (`||`)**: Precisa de **UM** verdadeiro
- **AND (`&&`)**: Precisa de **TODOS** verdadeiros

---

# 🎯 NOVO DESAFIO 3B — Aplicar AND

### Contexto
Um produto só pode ser vendido se estiver **DISPONÍVEL E tiver ESTOQUE**.

### O que fazer:
Crie um programa que:
1. Armazene se o produto está disponível (`boolean`)
2. Armazene a quantidade em estoque (`int`)
3. Verifique se está disponível **E** tem estoque (quantidade > 0)
4. Exiba:
   - `"Pode vender!"` se ambas as condições forem verdadeiras
   - `"Não pode vender"` caso contrário

**Teste com:**
- `disponivel = true`
- `estoque = 5`

---

# 💡 SOLUÇÃO DO NOVO DESAFIO 3B

```java
boolean disponivel = true;
int estoque = 5;

if (disponivel && estoque > 0) {
    System.out.println("Pode vender!");
} else {
    System.out.println("Não pode vender");
}
```

### Análise:
- `disponivel` → `true`
- `estoque > 0` → `5 > 0` → `true`
- `true && true` → **`true`**
- Imprime: `"Pode vender!"`

### E se estoque fosse 0?
- `disponivel` → `true`
- `estoque > 0` → `0 > 0` → `false`
- `true && false` → **`false`**
- Imprime: `"Não pode vender"`

---

# 🎯 PARTE 4 — DESAFIO: Combinação de Condições e Precedência

### Contexto
Um usuário tem acesso a dados confidenciais se:
1. Estiver **ativo E tiver permissão**, **OU**
2. For um **administrador**

### O que fazer:
Crie um programa que implemente essa lógica.

**Teste com:**
- `usuarioAtivo = true`
- `possuiPermissao = false`
- `administrador = false`

**Esperado:** `"Acesso negado"`

---

# 💡 SOLUÇÃO 4 — Combinação de Condições

```java
boolean usuarioAtivo = true;
boolean possuiPermissao = false;
boolean administrador = false;

if ((usuarioAtivo && possuiPermissao) || administrador) {
    System.out.println("Acesso permitido");
} else {
    System.out.println("Acesso negado");
}
```

---

# 🔍 EXPLICAÇÃO 4: Precedência e Parênteses

### Por que os parênteses importam?

Assim como na matemática, os parênteses `()` definem a ordem de avaliação:

```java
// Com parênteses (ordem clara):
if ((usuarioAtivo && possuiPermissao) || administrador) { ... }

// Avalia:
// 1. (true && false) = false
// 2. (false) || false = false
// Resultado: false → Acesso negado
```

### Precedência padrão de operadores:
1. `&&` (AND) tem maior precedência
2. `||` (OR) tem menor precedência

```java
// Mesmo sem parênteses, a ordem seria a mesma:
if (usuarioAtivo && possuiPermissao || administrador) { ... }
```

**Mas use parênteses mesmo assim!** Deixa sua intenção clara para quem lê o código.

---

# 🔍 EXPLICAÇÃO: Clean Code em Expressões Booleanas

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

### Tabela Resumida de Clean Code:

| Evitar (Confuso/Verboso) | Preferir (Limpo e Claro) |
| :--- | :--- |
| `if (ativo == true)` | `if (ativo)` |
| `if (ativo == false)` | `if (!ativo)` |
| `if (a == true && b == true)` | `if (a && b)` |
| `if (a == false \|\| b == false)` | `if (!a \|\| !b)` |

---

# 🎯 DESAFIO FINAL — Integração Completa

### Contexto
Uma loja online precisa validar se um produto pode ser vendido. O sistema deve verificar **TRÊS critérios** simultaneamente.

### Regras de Negócio:
1. O produto deve estar **disponível** (`boolean`)
2. A quantidade em estoque deve ser **maior que zero** (`int`)
3. O preço deve ser **maior ou igual a 10.00** (`double`)

### O que fazer:
Crie um programa que:
- Declare as três variáveis com valores
- Use operadores relacionais (`>`, `>=`) e lógicos (`&&`) apropriados
- Exiba:
  - `"Produto pode ser vendido!"` se **TODAS as três** condições forem verdadeiras
  - `"Produto NÃO pode ser vendido!"` caso contrário
- Aplique **Clean Code** (use variáveis booleanas se necessário)

**Teste com:**
- `disponivel = true`
- `estoque = 15`
- `preco = 25.50`

**Teste também com:**
- `disponivel = true`
- `estoque = 0`
- `preco = 25.50`

---

# 💡 SOLUÇÃO DESAFIO FINAL

### Forma 1 — Direta:

```java
boolean disponivel = true;
int estoque = 15;
double preco = 25.50;

if (disponivel && estoque > 0 && preco >= 10.00) {
    System.out.println("Produto pode ser vendido!");
} else {
    System.out.println("Produto NÃO pode ser vendido!");
}
```

### Forma 2 — Clean Code com variáveis booleanas:

```java
boolean disponivel = true;
int estoque = 15;
double preco = 25.50;

boolean temEstoque = estoque > 0;
boolean precoValido = preco >= 10.00;
boolean podeVender = disponivel && temEstoque && precoValido;

if (podeVender) {
    System.out.println("Produto pode ser vendido!");
} else {
    System.out.println("Produto NÃO pode ser vendido!");
}
```

---

# 🔍 EXPLICAÇÃO DESAFIO FINAL

### Análise da Solução 1:

```java
disponivel → true
estoque > 0 → 15 > 0 → true
preco >= 10.00 → 25.50 >= 10.00 → true

true && true && true → true

Resultado: "Produto pode ser vendido!"
```

### Análise com estoque = 0:

```java
disponivel → true
estoque > 0 → 0 > 0 → false
preco >= 10.00 → 25.50 >= 10.00 → true

true && false && true → false

Resultado: "Produto NÃO pode ser vendido!"
```

### Por que Forma 2 é mais Clean Code?

1. **Legibilidade**: Cada condição tem um nome significativo
2. **Manutenção**: Fácil adicionar/remover critérios
3. **Reutilização**: Variáveis booleanas podem ser usadas em outro lugar
4. **Testabilidade**: Cada condição pode ser verificada isoladamente

### Regra de Ouro:
> Se a condição é complexa, quebre em variáveis booleanas descritivas!

---

# 📋 RESUMO DO MÓDULO

| Conceito | O Que Faz | Exemplo |
| :--- | :--- | :--- |
| `if` / `else` | Executa código baseado em condição | `if (idade >= 18) { ... }` |
| `==` / `!=` / `>` / `<` / `>=` / `<=` | Comparam valores | `preco >= 10.00` |
| `&&` (AND) | Verdadeiro se **TODOS** forem true | `a && b && c` |
| `\|\|` (OR) | Verdadeiro se **QUALQUER UM** for true | `a \|\| b` |
| `!` (NOT) | Inverte o boolean | `!ativo` |
| `()` Parênteses | Define ordem de avaliação | `(a && b) \|\| c` |

---

# 🎓 Próximos Passos

- Pratique combinando operadores em programas reais
- Use `else if` para múltiplas condições (próximo módulo)
- Explore `switch` para casos com muitas opções (próximo módulo)
- Sempre aplique Clean Code: parênteses e nomes descritivos!
