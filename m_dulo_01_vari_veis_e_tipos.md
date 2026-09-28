---
marp: true
theme: default
paginate: true
---

# JAVA 21
## Módulo 01 — Variáveis e Tipos

**Metodologia:** Desafio → Solução → Explicação → Evolução

---

# 🎯 Desafio: Cadastro de Produto

### Contexto
Precisamos representar as informações de um produto em um estoque de supermercado.

### Regras
1. Todo produto possui um **código**, um **nome**, um **preço** e uma **quantidade em estoque**.
2. O código do produto é atribuído uma única vez e **nunca mais pode ser alterado**.

---

# ❓ Pense antes de programar

Antes de ver a solução, identifique:

- Quais tipos de dados representam melhor cada informação?
- Qual atributo deve ser **imutável** (`final`)?

---

# 💡 Solução

```java
public class Main {

    final int codigo = 101;
    String nome = "Teclado Mecânico";
    double preco = 250.50;
    int quantidade = 15;

}
```

---

# 🔍 Explicação: Tipagem Estática

Em Java, toda variável precisa ter um **tipo definido** antes de ser utilizada. Isso é chamado de **tipagem estática**.

- `int`: Números inteiros (ex: $1, 10, -50$).
- `double`: Números decimais / ponto flutuante (ex: $29.90, 3.14$).
- `String`: Textos e sequências de caracteres (ex: `"Teclado"`, `"Java 21"`).
- `boolean`: Valores lógicos: verdadeiro (`true`) ou falso (`false`).

---

# 🔍 Explicação: Imutabilidade com `final`

A palavra-chave `final` impede que o valor de uma variável seja modificado após sua atribuição inicial.

```java
final int codigo = 10;

// O código abaixo gera ERRO de compilação:
codigo = 20; 
```

### Comparação:
```java
int quantidade = 10;
quantidade = 20; // OK: variável comum pode mudar

final int codigo = 10;
codigo = 20; // ERRO: variável final é constante
```

---

# ⚠️ Erro Comum: Incompatibilidade de Tipos

Tentativa de atribuir um tipo incorreto a uma variável:

```java
// ERRO DE COMPILAÇÃO!
int preco = 29.90; 

// ERRO DE COMPILAÇÃO!
boolean nome = "Teclado"; 
```

**Por quê?**
Java não converte automaticamente tipos com perda de informação (como `double` para `int`) nem aceita texto em variáveis booleanas.

---

**Objetivo deste módulo:** Compreender o fluxo básico:
$$\text{variáveis} \longrightarrow \text{tipos} \longrightarrow \text{imutabilidade}$$

---

# 🚀 Evolução: Exercício Prático

Crie uma classe Java para representar uma **Empresa**.

### Requisitos:
1. Atributos necessários:
   - Razão Social / Nome
   - CNPJ (o CNPJ não pode mudar após definido)
   - Quantidade de Funcionários
   - Situação (Ativa ou Inativa)
2. Aplique corretamente o `final`.
3. Escolha os tipos primitivos e de objetos corretos.
