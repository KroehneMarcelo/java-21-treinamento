---
marp: true
theme: default
paginate: true
---

# JAVA 21
## Módulo 01 — Variáveis e Tipos

**Metodologia:** Desafio → Solução → Explicação → Novo Desafio → Solução com Explicação

---

# 🎯 DESAFIO 1 — Cadastro de Produto

### Contexto
Precisamos representar as informações de um produto em um estoque de supermercado.

### O que fazer:
Crie um programa que represente um produto com:
- código
- nome
- preço
- quantidade em estoque

Além disso, o código do produto deve ser **imutável** e não pode mudar depois de definido.

### Regras:
1. O produto possui um **código**.
2. O produto possui um **nome**.
3. O produto possui um **preço**.
4. O produto possui uma **quantidade em estoque**.
5. O código deve ser declarado com `final`.

---

# 💡 SOLUÇÃO 1

```java
public class Main {

    final int codigo = 101;
    String nome = "Teclado Mecânico";
    double preco = 250.50;
    int quantidade = 15;

}
```

---

# 🔍 EXPLICAÇÃO 1 — Tipagem Estática e Variáveis

Em Java, toda variável precisa ter um **tipo definido** antes de ser utilizada. Isso é chamado de **tipagem estática**.

### Tipos comuns:

- `int`: Números inteiros (ex.: `1`, `10`, `-50`)
- `double`: Números decimais / ponto flutuante (ex.: `29.90`, `3.14`)
- `String`: Textos e sequências de caracteres (ex.: `"Teclado"`, `"Java 21"`)
- `boolean`: Valores lógicos: verdadeiro (`true`) ou falso (`false`)

### Exemplo:

```java
int quantidade = 15;
double preco = 250.50;
String nome = "Teclado Mecânico";
boolean disponivel = true;
```

Cada variável recebe um tipo específico, e esse tipo define o tipo de dados que ela pode armazenar.

---

# 🔍 EXPLICAÇÃO 2 — Imutabilidade com `final`

A palavra-chave `final` impede que o valor de uma variável seja alterado após sua atribuição inicial.

```java
final int codigo = 10;

// O código abaixo gera ERRO de compilação:
// codigo = 20;
```

### Comparação:

```java
int quantidade = 10;
quantidade = 20; // OK: variável comum pode mudar

final int codigo = 10;
// codigo = 20; // ERRO: variável final é constante
```

### Quando usar `final`?
Use `final` para valores que devem permanecer fixos, como:
- código de produto
- CPF
- código de acesso
- constantes de regras de negócio

---

# ⚠️ ERRO COMUM — Incompatibilidade de Tipos

Tentativa de atribuir um tipo incorreto a uma variável:

```java
// ERRO DE COMPILAÇÃO!
int preco = 29.90;

// ERRO DE COMPILAÇÃO!
boolean nome = "Teclado";
```

### Por quê?
Java não converte automaticamente tipos com perda de informação (como `double` para `int`) e também não aceita texto em variáveis booleanas.

### Forma correta:

```java
double preco = 29.90;
String nome = "Teclado";
```

---

# 🎯 NOVO DESAFIO 1 — Criando uma Empresa

### Contexto
Você precisa modelar uma empresa em um sistema.

### O que fazer:
Crie uma classe Java com:
- `nomeEmpresa` (String)
- `cnpj` (String)
- `quantidadeFuncionarios` (int)
- `ativa` (boolean)

**Regra importante:**
- O `cnpj` deve ser declarado com `final`.

### Requisitos:
1. Escolha os tipos corretos para cada dado.
2. Aplique corretamente o `final`.
3. Use nomes claros e significativos.

---

# 💡 SOLUÇÃO DO NOVO DESAFIO 1

```java
public class Empresa {

    String nomeEmpresa = "Lykon Tech";
    final String cnpj = "12.345.678/0001-99";
    int quantidadeFuncionarios = 42;
    boolean ativa = true;

}
```

### Análise:
- `String` é usado para textos, como nome e CNPJ.
- `int` é usado para números inteiros, como quantidade de funcionários.
- `boolean` representa verdadeiro ou falso, como empresa ativa ou inativa.
- `final` no CNPJ garante que o documento não será alterado depois da criação.

---

# 🎯 DESAFIO 2 — Entendendo a Declaração de Variáveis

### Contexto
Você precisa guardar o nome de um aluno e sua idade em um sistema escolar.

### O que fazer:
Crie um programa que:
1. Armazene o nome do aluno em uma variável de texto.
2. Armazene a idade em uma variável numérica inteira.
3. Exiba os valores no console.

**Teste com:**
- `nome = "Maria"`
- `idade = 18`

---

# 💡 SOLUÇÃO 2

```java
String nome = "Maria";
int idade = 18;

System.out.println(nome);
System.out.println(idade);
```

---

# 🔍 EXPLICAÇÃO 3 — Declaração e Uso de Variáveis

Uma variável em Java precisa ser declarada antes de ser utilizada.

```java
String nome;
nome = "Maria";
```

Também é possível declarar e atribuir na mesma linha:

```java
String nome = "Maria";
```

### Boas práticas:
- Use nomes descritivos
- Comece com letra minúscula
- Evite nomes genéricos como `x`, `a`, `valor`

Exemplos bons:

```java
String nomeAluno = "Maria";
int idadeAluno = 18;
boolean alunoAtivo = true;
```

---

# 🎯 NOVO DESAFIO 2 — Nome e Status do Cliente

### Contexto
Você precisa guardar dados de um cliente em um sistema de vendas.

### O que fazer:
Crie um programa que:
1. Guarda o nome do cliente em uma variável `String`.
2. Guarda se ele está ativo (`true` ou `false`) em uma variável `boolean`.
3. Exiba as informações em console.

**Teste com:**
- `nomeCliente = "Carlos"`
- `clienteAtivo = true`

---

# 💡 SOLUÇÃO DO NOVO DESAFIO 2

```java
String nomeCliente = "Carlos";
boolean clienteAtivo = true;

System.out.println("Nome do cliente: " + nomeCliente);
System.out.println("Cliente ativo: " + clienteAtivo);
```

### Análise:
- `String` armazena texto.
- `boolean` representa um valor lógico.
- O operador `+` concatena textos e valores em uma mensagem.

---

# 🎯 DESAFIO 3 — Modelando uma Pessoa

### Contexto
Você precisa representar uma pessoa em um sistema.

### O que fazer:
Crie um programa que armazene:
- nome
- idade
- altura
- está empregado

Escolha os tipos corretos para cada dado.

---

# 💡 SOLUÇÃO 3

```java
String nome = "Ana";
int idade = 27;
double altura = 1.68;
boolean estaEmpregado = true;
```

---

# 🔍 EXPLICAÇÃO 4 — Escolha do Tipo Correto

Cada informação tem um tipo que melhor representa sua natureza:

```java
String nome = "Ana";          // texto
int idade = 27;               // número inteiro
double altura = 1.68;        // número decimal
boolean estaEmpregado = true; // verdadeiro ou falso
```

### Regra prática:
- Use `int` para contagens e números inteiros.
- Use `double` para valores monetários e medidas decimais.
- Use `String` para textos.
- Use `boolean` para respostas lógicas.

---

# 🎯 DESAFIO FINAL — Modelando uma Loja

### Contexto
Criar uma estrutura básica para uma loja online.

### Regras de negócio:
1. O nome da loja deve ser um texto.
2. O número de produtos deve ser inteiro.
3. O faturamento mensal deve ser decimal.
4. A loja deve indicar se está aberta ou fechada.
5. O CNPJ da loja deve ser imutável.

### O que fazer:
Declare as variáveis corretamente e aplique `final` no CNPJ.

---

# 💡 SOLUÇÃO FINAL

```java
public class Loja {

    String nome = "Loja Central";
    int quantidadeProdutos = 120;
    double faturamentoMensal = 18500.75;
    boolean aberta = true;
    final String cnpj = "11.222.333/0001-44";

}
```

---

# 🔍 EXPLICAÇÃO FINAL — Fluxo Prático do Módulo

### O que aprendemos?

- Variáveis guardam dados.
- Cada variável precisa ter um tipo.
- `final` torna o valor imutável.
- O tipo deve ser compatível com o dado representado.
- O código fica mais claro quando usamos nomes significativos.

### Fluxo básico:

```java
String nome = "Maria";
int idade = 18;
boolean ativo = true;
final String cpf = "123.456.789-00";
```

### Exemplo de uso em regra de negócio:

```java
String produto = "Teclado";
int quantidade = 15;
double preco = 250.50;
final int codigo = 101;
```

> Esse é o começo de qualquer programa Java: definir dados, escolher tipos e organizar regras de negócio.

---

# 📋 RESUMO DO MÓDULO

| Conceito | Uso | Exemplo |
| :--- | :--- | :--- |
| `int` | Números inteiros | `int idade = 18;` |
| `double` | Números decimais | `double preco = 29.90;` |
| `String` | Textos | `String nome = "Maria";` |
| `boolean` | Verdadeiro/Falso | `boolean ativo = true;` |
| `final` | Torna variável imutável | `final int codigo = 101;` |

---

# 🎓 Próximos Passos

- Pratique a criação de classes simples.
- Use `final` em valores que não devem mudar.
- Escolha tipos com cuidado para cada informação.
- Continue para o próximo módulo e veja como as variáveis se conectam com condicionais.
