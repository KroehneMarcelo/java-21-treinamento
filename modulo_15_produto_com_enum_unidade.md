---
marp: true
theme: default
paginate: true
---

# JAVA 21
## Módulo 15 — `Produto` com `enum UNIDADE`

**Metodologia:** Relembrando → Desafio 1 → Solução 1 → Explicação → Desafio Extra → Solução → Desafio Final → Solução Final → Revisão

---

# 🧠 RELEMBRANDO — Produto e lista

No módulo 13, trabalhamos com:

```java
List<Produto> produtos = new ArrayList<>();
```

No módulo 14, aprendemos a criar enums:

```java
public enum UNIDADE {
    UNIDADE,
    QUILOGRAMA,
    LITRO
}
```

Agora vamos combinar os dois conceitos: cada `Produto` terá uma unidade de venda.

Exemplos:

- arroz vendido em `QUILOGRAMA`;
- leite vendido em `LITRO`;
- teclado vendido em `UNIDADE`.

---

# 🧠 Enum `UNIDADE`

```java
public enum UNIDADE {
    UNIDADE,
    QUILOGRAMA,
    LITRO
}
```

O enum informa como o produto é medido ou vendido.

```java
UNIDADE unidade = UNIDADE.QUILOGRAMA;
```

O nome `UNIDADE` foi escolhido para acompanhar o modelo proposto. Em projetos reais, também é comum usar nomes de enum em `PascalCase`, como `Unidade`.

---

# 🎯 DESAFIO 1 — Unidade como atributo de `Produto`

Crie a classe `Produto` com os atributos privados:

- `String nome`;
- `double valor`;
- `UNIDADE unidade`.

Crie construtor, getters e setters. No `main`, crie produtos de unidades diferentes e exiba seus dados.

---

# 💡 SOLUÇÃO 1

```java
public enum UNIDADE {
    UNIDADE,
    QUILOGRAMA,
    LITRO
}
```

```java
public class Produto {
    private String nome;
    private double valor;
    private UNIDADE unidade;

    public Produto(String nome, double valor, UNIDADE unidade) {
        this.nome = nome;
        this.valor = valor;
        this.unidade = unidade;
    }

    public String getNome() {
        return nome;
    }

    public double getValor() {
        return valor;
    }

    public UNIDADE getUnidade() {
        return unidade;
    }

    public void setUnidade(UNIDADE unidade) {
        this.unidade = unidade;
    }
}
```

```java
public class Main {
    public static void main(String[] args) {
        Produto arroz = new Produto("Arroz", 2.5, UNIDADE.QUILOGRAMA);
        Produto leite = new Produto("Leite", 3.2, UNIDADE.LITRO);
        Produto teclado = new Produto("Teclado", 150.0, UNIDADE.UNIDADE);

        System.out.println(arroz.getNome() + " - " + arroz.getUnidade());
        System.out.println(leite.getNome() + " - " + leite.getUnidade());
        System.out.println(teclado.getNome() + " - " + teclado.getUnidade());
    }
}
```

---

# 🔍 EXPLICAÇÃO

O atributo é declarado com o tipo do enum:

```java
private UNIDADE unidade;
```

No construtor, recebemos uma constante válida:

```java
new Produto("Arroz", 2.5, UNIDADE.QUILOGRAMA);
```

O getter retorna o tipo `UNIDADE`:

```java
public UNIDADE getUnidade() {
    return unidade;
}
```

A unidade não é uma `String`. Ela é uma informação com opções previamente definidas.

---

# 🧠 Exibindo o enum

Ao concatenar um enum com uma `String`, o Java usa seu texto padrão:

```java
System.out.println(produto.getUnidade());
```

Saída:

```text
QUILOGRAMA
```

Para exibir um texto mais amigável, podemos usar `switch`:

```java
public static String nomeUnidade(UNIDADE unidade) {
    return switch (unidade) {
        case UNIDADE -> "unidade";
        case QUILOGRAMA -> "quilograma";
        case LITRO -> "litro";
    };
}
```

---

# 🎯 DESAFIO EXTRA — Descrição com `switch`

Crie o método:

```java
public static String descreverProduto(Produto produto)
```

O método deve retornar uma descrição contendo nome, valor e unidade por extenso. Use `switch` sobre `produto.getUnidade()`.

---

# 💡 SOLUÇÃO DO DESAFIO EXTRA

```java
public static String nomeUnidade(UNIDADE unidade) {
    return switch (unidade) {
        case UNIDADE -> "unidade";
        case QUILOGRAMA -> "quilograma";
        case LITRO -> "litro";
    };
}

public static String descreverProduto(Produto produto) {
    return produto.getNome()
            + " - R$ " + produto.getValor()
            + " por " + nomeUnidade(produto.getUnidade());
}
```

```java
Produto arroz = new Produto("Arroz", 2.5, UNIDADE.QUILOGRAMA);
System.out.println(descreverProduto(arroz));
```

Saída esperada:

```text
Arroz - R$ 2.5 por quilograma
```

---

# 🧠 Enum na lista de produtos

Podemos guardar produtos com unidades diferentes na mesma lista:

```java
List<Produto> produtos = new ArrayList<>();

produtos.add(new Produto("Arroz", 2.5, UNIDADE.QUILOGRAMA));
produtos.add(new Produto("Leite", 3.2, UNIDADE.LITRO));
produtos.add(new Produto("Teclado", 150.0, UNIDADE.UNIDADE));
```

A lista continua sendo `List<Produto>`. A unidade é uma informação de cada objeto.

---

# 🎯 DESAFIO FINAL — Lista de produtos por unidade

Crie uma lista com produtos de unidades diferentes.

Regras:

1. Use o enum `UNIDADE`.
2. Crie a classe `Produto` com `nome`, `valor` e `unidade`.
3. Crie uma `List<Produto>`.
4. Adicione arroz, leite, feijão e teclado.
5. Percorra a lista com `for-each`.
6. Use `switch` para exibir o texto da unidade.
7. Crie um método que conte quantos produtos pertencem a determinada unidade.

---

# 💡 SOLUÇÃO DO DESAFIO FINAL

```java
public static String nomeUnidade(UNIDADE unidade) {
    return switch (unidade) {
        case UNIDADE -> "unidade";
        case QUILOGRAMA -> "quilograma";
        case LITRO -> "litro";
    };
}

public static long contarPorUnidade(List<Produto> produtos, UNIDADE unidade) {
    long quantidade = 0;

    for (Produto produto : produtos) {
        if (produto.getUnidade() == unidade) {
            quantidade++;
        }
    }

    return quantidade;
}
```

```java
List<Produto> produtos = new ArrayList<>();
produtos.add(new Produto("Arroz", 2.5, UNIDADE.QUILOGRAMA));
produtos.add(new Produto("Feijão", 4.0, UNIDADE.QUILOGRAMA));
produtos.add(new Produto("Leite", 3.2, UNIDADE.LITRO));
produtos.add(new Produto("Teclado", 150.0, UNIDADE.UNIDADE));

for (Produto produto : produtos) {
    System.out.println(produto.getNome()
            + " - R$ " + produto.getValor()
            + " por " + nomeUnidade(produto.getUnidade()));
}

System.out.println("Produtos por quilograma: "
        + contarPorUnidade(produtos, UNIDADE.QUILOGRAMA));
```

---

# 🔍 EXPLICAÇÃO DO DESAFIO FINAL

Para comparar enums, podemos usar `==`:

```java
produto.getUnidade() == unidade
```

Enums representam constantes únicas, por isso essa comparação é adequada.

A lista pode conter vários produtos, e cada produto pode ter uma unidade diferente:

```text
Arroz    → QUILOGRAMA
Feijão   → QUILOGRAMA
Leite    → LITRO
Teclado  → UNIDADE
```

A unidade é parte do estado de cada produto, não da lista inteira.

---

# ✅ REVISÃO DO MÓDULO 15

Ao concluir este módulo, você deve conseguir:

- Criar o enum `UNIDADE`.
- Usar um enum como atributo de `Produto`.
- Receber enum no construtor.
- Criar getter e setter para enum.
- Usar enum em `switch`.
- Comparar valores de enum com `==`.
- Trabalhar com uma lista de produtos que possui unidades diferentes.
