---
marp: true
theme: default
paginate: true
---

# JAVA 21
## Módulo 03 — Comparações em Java

**Metodologia:** Desafio → Solução → Explicação → Novo Desafio → Solução com Explicação

---

# 🎯 DESAFIO 1 — Comparando Tipos Primitivos

### Contexto
Um sistema precisa verificar se dois códigos numéricos são iguais.

### O que fazer:
Crie um programa que:
1. Declare duas variáveis `int`.
2. Compare os valores das duas variáveis.
3. Exiba `"Códigos iguais"` quando os valores forem iguais.
4. Exiba `"Códigos diferentes"` caso contrário.

**Teste com:**
- `codigo1 = 10`
- `codigo2 = 10`

---

# 💡 SOLUÇÃO 1 — Comparando Tipos Primitivos

```java
int codigo1 = 10;
int codigo2 = 10;

if (codigo1 == codigo2) {
    System.out.println("Códigos iguais");
} else {
    System.out.println("Códigos diferentes");
}
```

---

# 🔍 EXPLICAÇÃO 1 — O Operador `==` em Tipos Primitivos

Para tipos primitivos, como `int`, `double`, `boolean` e `char`, o operador `==` compara os **valores diretamente**.

```java
int codigo1 = 10;
int codigo2 = 10;
boolean codigosIguais = codigo1 == codigo2;
```

Nesse exemplo:

1. `codigo1` contém `10`.
2. `codigo2` contém `10`.
3. A expressão `codigo1 == codigo2` resulta em `true`.
4. O bloco do `if` é executado.

O operador `==` também pode ser usado com outros tipos primitivos:

```java
double preco1 = 25.50;
double preco2 = 25.50;
boolean precosIguais = preco1 == preco2;

char letra1 = 'A';
char letra2 = 'A';
boolean letrasIguais = letra1 == letra2;

boolean ativo1 = true;
boolean ativo2 = true;
boolean statusIguais = ativo1 == ativo2;
```

---

# 🎯 NOVO DESAFIO 1 — Aplicando Comparações Primitivas

### Contexto
Uma loja precisa verificar se dois preços são iguais e se um produto está ativo.

### O que fazer:
Crie um programa que:
1. Declare dois preços do tipo `double`.
2. Declare duas variáveis `boolean` representando o status de dois produtos.
3. Verifique se os preços são iguais.
4. Verifique se os dois produtos estão ativos.
5. Exiba mensagens informando os resultados.

**Teste com:**
- `precoProduto1 = 49.90`
- `precoProduto2 = 49.90`
- `produto1Ativo = true`
- `produto2Ativo = false`

---

# 💡 SOLUÇÃO DO NOVO DESAFIO 1

```java
double precoProduto1 = 49.90;
double precoProduto2 = 49.90;

boolean produto1Ativo = true;
boolean produto2Ativo = false;

if (precoProduto1 == precoProduto2) {
    System.out.println("Os preços são iguais");
} else {
    System.out.println("Os preços são diferentes");
}

if (produto1Ativo == produto2Ativo) {
    System.out.println("Os produtos possuem o mesmo status");
} else {
    System.out.println("Os produtos possuem status diferentes");
}
```

### Forma mais idiomática para comparar booleanos

Quando já temos variáveis booleanas, normalmente não precisamos usar `== true` ou `== false`:

```java
if (produto1Ativo && produto2Ativo) {
    System.out.println("Os dois produtos estão ativos");
}
```

Para verificar se um produto não está ativo, use `!`:

```java
if (!produto2Ativo) {
    System.out.println("O produto 2 está inativo");
}
```

---

# 🎯 DESAFIO 2 — Comparando Strings

### Contexto
Um sistema precisa verificar se o nome digitado por um cliente é `"João"`.

### O que fazer:
Crie um programa que:
1. Armazene o nome do cliente em uma variável `String`.
2. Compare o conteúdo dessa variável com `"João"`.
3. Exiba `"Nome encontrado"` quando o conteúdo for igual.
4. Exiba `"Nome não encontrado"` caso contrário.

**Teste com:**
- `nome = "João"`

**Atenção:** Resolva o desafio antes de consultar a solução.

---

# 💡 SOLUÇÃO 2 — Utilizando `equals()`

```java
String nome = "João";

if (nome.equals("João")) {
    System.out.println("Nome encontrado");
} else {
    System.out.println("Nome não encontrado");
}
```

---

# 🔍 EXPLICAÇÃO 2 — `equals()` e Comparação de Objetos

`String` é uma classe, portanto uma variável `String` armazena uma referência para um objeto.

Para comparar o **conteúdo textual** de duas Strings, utilize `.equals()`:

```java
String nome1 = new String("João");
String nome2 = new String("João");

System.out.println(nome1.equals(nome2)); // true
```

O operador `==`, por outro lado, verifica se as duas referências apontam para o mesmo objeto:

```java
String nome1 = new String("João");
String nome2 = new String("João");

System.out.println(nome1 == nome2); // false
```

Mesmo que os objetos contenham o mesmo texto, eles podem ser objetos diferentes na memória.

### Erro comum

```java
String nome = "João";

// ❌ Não use == para comparar o conteúdo de Strings
if (nome == "João") {
    System.out.println("Nome encontrado");
}
```

Esse código pode aparentar funcionar em alguns casos por causa do reaproveitamento de literais pelo Java, mas não é uma forma confiável de comparar o conteúdo.

---

# 🛡️ EXPLICAÇÃO EXTRA — Comparação Segura contra `null`

Se a variável puder ser `null`, chamar `.equals()` diretamente nela pode causar `NullPointerException`:

```java
String nome = null;

// ❌ Erro em tempo de execução
// nome.equals("João");
```

Uma alternativa segura é chamar `.equals()` sobre um literal que sabemos não ser nulo:

```java
String nome = null;

if ("João".equals(nome)) {
    System.out.println("Nome encontrado");
} else {
    System.out.println("Nome não encontrado");
}
```

Também é possível validar explicitamente:

```java
if (nome != null && nome.equals("João")) {
    System.out.println("Nome encontrado");
}
```

---

# 🎯 NOVO DESAFIO 2 — Validando uma Senha

### Contexto
Um sistema precisa comparar uma senha digitada com a senha cadastrada.

### O que fazer:
Crie um programa que:
1. Declare uma senha cadastrada.
2. Declare uma senha digitada.
3. Compare o conteúdo das duas Strings usando `.equals()`.
4. Exiba:
   - `"Senha correta"` quando forem iguais.
   - `"Senha incorreta"` quando forem diferentes.

**Teste com:**
- `senhaCadastrada = "java21"`
- `senhaDigitada = "java21"`

**Desafio extra:** Teste com `senhaDigitada = "Java21"` e observe que Java diferencia letras maiúsculas de minúsculas.

---

# 💡 SOLUÇÃO DO NOVO DESAFIO 2

```java
String senhaCadastrada = "java21";
String senhaDigitada = "java21";

if (senhaCadastrada.equals(senhaDigitada)) {
    System.out.println("Senha correta");
} else {
    System.out.println("Senha incorreta");
}
```

### Análise

- `"java21".equals("java21")` resulta em `true`.
- O bloco do `if` é executado.
- Se a senha digitada fosse `"Java21"`, o resultado seria `false`, pois `equals()` diferencia maiúsculas de minúsculas.

Para ignorar maiúsculas e minúsculas, existe o método `equalsIgnoreCase()`:

```java
if (senhaCadastrada.equalsIgnoreCase(senhaDigitada)) {
    System.out.println("Textos equivalentes ignorando maiúsculas e minúsculas");
}
```

> Para senhas reais, não é recomendado armazenar ou comparar senhas dessa forma. Este exemplo tem finalidade exclusivamente didática.

---

# 🎯 DESAFIO 3 — Comparando com `contentEquals()`

### Contexto
Uma aplicação recebe um texto em uma `StringBuilder`, mas precisa compará-lo com uma `String` esperada.

### O que fazer:
Crie um programa que:
1. Declare uma `String` com o texto esperado.
2. Declare um `StringBuilder` com o texto recebido.
3. Compare os conteúdos dos dois objetos.
4. Exiba `"Conteúdo exatamente igual"` quando forem iguais.
5. Exiba `"Conteúdo diferente"` caso contrário.

**Teste com:**
- texto esperado: `"João"`
- texto recebido: `new StringBuilder("João")`

---

# 💡 SOLUÇÃO 3 — Utilizando `contentEquals()`

```java
String textoEsperado = "João";
StringBuilder textoRecebido = new StringBuilder("João");

if (textoEsperado.contentEquals(textoRecebido)) {
    System.out.println("Conteúdo exatamente igual");
} else {
    System.out.println("Conteúdo diferente");
}
```

---

# 🔍 EXPLICAÇÃO 3 — `contentEquals()`

O método `contentEquals()` compara o conteúdo de uma `String` com uma sequência de caracteres, como `StringBuilder` ou `StringBuffer`.

```java
String nome = "João";
StringBuilder outro = new StringBuilder("João");

boolean textosIguais = nome.contentEquals(outro);
```

### Diferença entre os métodos

- **`equals()`**: verifica igualdade de conteúdo entre objetos `String`.
- **`contentEquals()`**: compara o conteúdo da `String` com uma `CharSequence`, como `String`, `StringBuilder` ou `StringBuffer`.

```java
String texto = "Java";
StringBuilder builder = new StringBuilder("Java");

texto.equals(builder);        // false: tipos de objeto diferentes
texto.contentEquals(builder); // true: conteúdos iguais
```

---

# 🎯 NOVO DESAFIO 3 — Validando uma Mensagem Recebida

### Contexto
Um sistema recebe uma mensagem que deve ser exatamente igual à mensagem esperada.

### O que fazer:
Crie um programa que:
1. Declare `mensagemEsperada` como `String`.
2. Declare `mensagemRecebida` como `StringBuilder`.
3. Compare os conteúdos com `contentEquals()`.
4. Exiba:
   - `"Mensagem válida"` quando forem iguais.
   - `"Mensagem inválida"` caso contrário.

**Teste com:**
- `mensagemEsperada = "CONFIRMADO"`
- `mensagemRecebida = new StringBuilder("CONFIRMADO")`

---

# 💡 SOLUÇÃO DO NOVO DESAFIO 3

```java
String mensagemEsperada = "CONFIRMADO";
StringBuilder mensagemRecebida = new StringBuilder("CONFIRMADO");

if (mensagemEsperada.contentEquals(mensagemRecebida)) {
    System.out.println("Mensagem válida");
} else {
    System.out.println("Mensagem inválida");
}
```

### Análise

- A String esperada contém `"CONFIRMADO"`.
- O `StringBuilder` também contém `"CONFIRMADO"`.
- `contentEquals()` compara a sequência de caracteres.
- O resultado é `true` e a mensagem é considerada válida.

---

# 🎯 DESAFIO 4 — Comparação para Ordenação

### Contexto
Uma agenda precisa identificar qual nome aparece primeiro na ordem alfabética.

### O que fazer:
Crie um programa que:
1. Declare dois nomes.
2. Use `compareTo()` para comparar os nomes.
3. Exiba:
   - O primeiro nome vem antes do segundo quando o resultado for menor que zero.
   - Os nomes são iguais quando o resultado for zero.
   - O primeiro nome vem depois do segundo quando o resultado for maior que zero.

**Teste com:**
- `nome1 = "Ana"`
- `nome2 = "Bruno"`

---

# 💡 SOLUÇÃO 4 — Utilizando `compareTo()`

```java
String nome1 = "Ana";
String nome2 = "Bruno";

int resultado = nome1.compareTo(nome2);

if (resultado < 0) {
    System.out.println(nome1 + " vem antes de " + nome2);
} else if (resultado == 0) {
    System.out.println("Nomes idênticos");
} else {
    System.out.println(nome1 + " vem depois de " + nome2);
}
```

---

# 🔍 EXPLICAÇÃO 4 — Retornos do `compareTo()`

O método `.compareTo()` retorna um número inteiro:

- **Número negativo (`< 0`)**: o primeiro texto vem antes do segundo na ordem lexicográfica.
- **Zero (`== 0`)**: os textos são iguais para a comparação.
- **Número positivo (`> 0`)**: o primeiro texto vem depois do segundo.

```java
"Ana".compareTo("Bruno")   // valor negativo
"Ana".compareTo("Ana")     // 0
"Bruno".compareTo("Ana")   // valor positivo
```

Não dependa de um valor específico, como `-1` ou `1`. O importante é verificar se o resultado é menor, igual ou maior que zero.

### Atenção às letras maiúsculas e minúsculas

A comparação padrão considera os valores Unicode dos caracteres:

```java
System.out.println("ana".compareTo("Ana"));
```

Para ordenar ignorando maiúsculas e minúsculas, use `compareToIgnoreCase()`:

```java
int resultado = nome1.compareToIgnoreCase(nome2);
```

---

# 🎯 NOVO DESAFIO 4 — Ordenando Produtos

### Contexto
Uma loja precisa verificar a ordem alfabética entre dois nomes de produtos.

### O que fazer:
Crie um programa que:
1. Declare dois nomes de produtos.
2. Compare os nomes sem diferenciar letras maiúsculas e minúsculas.
3. Informe qual produto vem primeiro, se são iguais ou qual vem depois.

**Teste com:**
- `produto1 = "Notebook"`
- `produto2 = "celular"`

Use `compareToIgnoreCase()`.

---

# 💡 SOLUÇÃO DO NOVO DESAFIO 4

```java
String produto1 = "Notebook";
String produto2 = "celular";

int resultado = produto1.compareToIgnoreCase(produto2);

if (resultado < 0) {
    System.out.println(produto1 + " vem antes de " + produto2);
} else if (resultado == 0) {
    System.out.println("Os produtos possuem o mesmo nome");
} else {
    System.out.println(produto1 + " vem depois de " + produto2);
}
```

### Análise

A comparação ignora a diferença entre letras maiúsculas e minúsculas:

- `"Notebook"` é comparado com `"celular"` como texto.
- O resultado é maior que zero.
- Portanto, `"Notebook"` vem depois de `"celular"` na ordem alfabética.

---

# 📊 TABELA COMPARATIVA

| Mecanismo | Finalidade principal | Exemplo |
| :--- | :--- | :--- |
| `==` | Comparar valores primitivos ou referências de objetos | `codigo1 == codigo2` |
| `equals()` | Verificar igualdade de conteúdo entre objetos | `"A".equals(texto)` |
| `contentEquals()` | Comparar conteúdo textual com uma `CharSequence` | `texto.contentEquals(builder)` |
| `compareTo()` | Determinar ordem lexicográfica | `nome1.compareTo(nome2) < 0` |
| `compareToIgnoreCase()` | Determinar ordem ignorando maiúsculas/minúsculas | `a.compareToIgnoreCase(b)` |

---

# 🎯 DESAFIO FINAL — Validação de Login

### Contexto
Um sistema precisa validar se uma tentativa de login é válida.

### Regras de negócio:
1. O usuário deve estar ativo (`boolean`).
2. O perfil deve ser igual a `"ADMIN"` ou `"OPERADOR"`.
3. O nome do usuário não pode ser igual a `"GUEST"`.
4. As Strings devem ser comparadas com `.equals()`.
5. A lógica deve aplicar Clean Code, usando nomes descritivos e evitando comparações redundantes.

### O que fazer:
Crie um programa que exiba:
- `"Login autorizado"` quando todas as regras forem atendidas.
- `"Login negado"` caso contrário.

**Teste com:**
- `usuarioAtivo = true`
- `perfil = "ADMIN"`
- `nomeUsuario = "marcelo"`

**Faça também um segundo teste com:**
- `usuarioAtivo = true`
- `perfil = "VISITANTE"`
- `nomeUsuario = "GUEST"`

---

# 💡 SOLUÇÃO DO DESAFIO FINAL

```java
boolean usuarioAtivo = true;
String perfil = "ADMIN";
String nomeUsuario = "marcelo";

boolean perfilPermitido = "ADMIN".equals(perfil) || "OPERADOR".equals(perfil);
boolean usuarioPermitido = !"GUEST".equals(nomeUsuario);
boolean loginValido = usuarioAtivo && perfilPermitido && usuarioPermitido;

if (loginValido) {
    System.out.println("Login autorizado");
} else {
    System.out.println("Login negado");
}
```

---

# 🔍 EXPLICAÇÃO DO DESAFIO FINAL

### Primeira validação: usuário ativo

```java
boolean usuarioAtivo = true;
```

A variável já representa uma condição booleana. Por isso, podemos usá-la diretamente:

```java
if (usuarioAtivo) {
    // Usuário está ativo
}
```

Não é necessário escrever `usuarioAtivo == true`.

### Segunda validação: perfil permitido

```java
boolean perfilPermitido = "ADMIN".equals(perfil) || "OPERADOR".equals(perfil);
```

O perfil será aceito quando for `ADMIN` **ou** `OPERADOR`.

Os literais ficam à esquerda da comparação para evitar `NullPointerException` caso `perfil` seja `null`.

### Terceira validação: usuário diferente de GUEST

```java
boolean usuarioPermitido = !"GUEST".equals(nomeUsuario);
```

O operador `!` inverte o resultado:

- Se o nome for `GUEST`, a comparação resulta em `true` e o `!` transforma em `false`.
- Se o nome for diferente de `GUEST`, a comparação resulta em `false` e o `!` transforma em `true`.

### Validação completa

```java
boolean loginValido = usuarioAtivo && perfilPermitido && usuarioPermitido;
```

O operador `&&` exige que todas as condições sejam verdadeiras:

```text
true && true && true → true → Login autorizado
```

No segundo teste:

```text
true && false && false → false → Login negado
```

Separar as regras em variáveis booleanas torna o código mais legível, testável e fácil de manter.

---

# 📋 RESUMO DO MÓDULO

| Conceito | Quando utilizar |
| :--- | :--- |
| `==` | Comparar valores de tipos primitivos |
| `equals()` | Comparar o conteúdo de objetos, especialmente `String` |
| `contentEquals()` | Comparar uma `String` com outra `CharSequence` |
| `compareTo()` | Comparar a ordem lexicográfica de Strings |
| `compareToIgnoreCase()` | Comparar ordem ignorando maiúsculas e minúsculas |
| `!` | Negar uma condição booleana |
| `&&` | Exigir que todas as condições sejam verdadeiras |
| `||` | Aceitar quando pelo menos uma condição for verdadeira |

> **Regra de ouro:** use `==` para valores primitivos, `equals()` para conteúdo de objetos e `compareTo()` para ordenação.

---

# 🎓 Próximos Passos

- Pratique comparações com entradas diferentes.
- Teste valores `null` e observe como evitar `NullPointerException`.
- Combine `equals()`, `!`, `&&` e `||` em regras de negócio.
- No próximo módulo, avance para múltiplas condições e estruturas como `else if` e `switch`.
