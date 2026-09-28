---
marp: true
theme: default
paginate: true
---

# JAVA 21
## Módulo 16 — Composição: `Carrinho` com `List<Produto>`

**Metodologia:** Relembrando → Desafio 1 → Solução 1 → Explicação → Desafio Extra → Solução → Desafio Final → Solução Final → Revisão

---

# 🧠 RELEMBRANDO — Uma classe pode usar outra classe

Nos módulos anteriores, criamos objetos `Produto` e uma lista no `main`:

```java
List<Produto> produtos = new ArrayList<>();
```

Agora vamos mover essa responsabilidade para uma classe própria: `Carrinho`.

```java
public class Carrinho {
    private List<Produto> produtos;
}
```

O `Carrinho` será um objeto que contém outros objetos `Produto`.

Esse relacionamento é chamado de **composição**: uma classe utiliza objetos de outra classe para formar seu estado.

---

# 🧠 Classe `Carrinho`

```java
import java.util.ArrayList;
import java.util.List;

public class Carrinho {
    private List<Produto> produtos = new ArrayList<>();
}
```

A lista é um atributo privado do carrinho.

Isso significa que o próprio `Carrinho` será responsável por:

- adicionar produtos;
- remover produtos;
- listar produtos;
- calcular o total;
- informar a quantidade de produtos.

O `main` apenas utiliza os métodos públicos do carrinho.

---

# 🎯 DESAFIO 1 — Adicionando produtos ao carrinho

Crie a classe `Carrinho` com uma lista privada de produtos.

Regras:

1. Declare `private List<Produto> produtos = new ArrayList<>();`.
2. Crie `adicionarProduto(Produto produto)`.
3. Ignore produtos `null`.
4. Crie `listarProdutos()` usando `for-each`.
5. No `main`, crie arroz, feijão e leite.
6. Adicione os três ao carrinho.
7. Liste os itens.

---

# 💡 SOLUÇÃO 1

```java
import java.util.ArrayList;
import java.util.List;

public class Carrinho {
    private List<Produto> produtos = new ArrayList<>();

    public void adicionarProduto(Produto produto) {
        if (produto != null) {
            produtos.add(produto);
        }
    }

    public void listarProdutos() {
        for (Produto produto : produtos) {
            System.out.println(produto.getNome()
                    + " - R$ " + produto.getValor()
                    + " por " + produto.getUnidade());
        }
    }
}
```

```java
public class Main {
    public static void main(String[] args) {
        Carrinho carrinho = new Carrinho();

        carrinho.adicionarProduto(new Produto("Arroz", 2.5, UNIDADE.QUILOGRAMA));
        carrinho.adicionarProduto(new Produto("Feijão", 4.0, UNIDADE.QUILOGRAMA));
        carrinho.adicionarProduto(new Produto("Leite", 3.2, UNIDADE.LITRO));

        carrinho.listarProdutos();
    }
}
```

---

# 🔍 EXPLICAÇÃO

O `Carrinho` contém uma lista de objetos `Produto`:

```text
Carrinho
└── produtos
    ├── Produto Arroz
    ├── Produto Feijão
    └── Produto Leite
```

A classe `Main` não precisa acessar a lista diretamente. Ela usa os comportamentos públicos:

```java
carrinho.adicionarProduto(produto);
carrinho.listarProdutos();
```

Essa organização concentra as regras relacionadas ao carrinho na classe correta.

---

# 🧠 Composição e responsabilidades

### `Produto` é responsável por:

- nome;
- valor;
- unidade;
- regras próprias do produto.

### `Carrinho` é responsável por:

- conjunto de produtos;
- inclusão e remoção;
- total da compra;
- quantidade de itens.

```text
Produto → dados de um item
Carrinho → organização de vários itens
```

Uma classe não precisa fazer tudo. Cada classe deve cuidar da responsabilidade que representa.

---

# 🎯 DESAFIO EXTRA — Total e remoção

Adicione à classe `Carrinho`:

1. `double calcularTotal()`.
2. `int quantidadeProdutos()`.
3. `void removerProduto(String nome)`.
4. A remoção deve ignorar nomes nulos ou vazios.
5. Remova apenas o primeiro produto com o nome encontrado.
6. Teste o carrinho antes e depois da remoção.

---

# 💡 SOLUÇÃO DO DESAFIO EXTRA

```java
public double calcularTotal() {
    double total = 0.0;

    for (Produto produto : produtos) {
        total += produto.getValor();
    }

    return total;
}

public int quantidadeProdutos() {
    return produtos.size();
}

public void removerProduto(String nome) {
    if (nome == null || nome.isBlank()) {
        return;
    }

    for (int i = 0; i < produtos.size(); i++) {
        if (produtos.get(i).getNome().equalsIgnoreCase(nome)) {
            produtos.remove(i);
            return;
        }
    }
}
```

```java
Carrinho carrinho = new Carrinho();
carrinho.adicionarProduto(new Produto("Arroz", 2.5, UNIDADE.QUILOGRAMA));
carrinho.adicionarProduto(new Produto("Feijão", 4.0, UNIDADE.QUILOGRAMA));

System.out.println("Total: R$ " + carrinho.calcularTotal());
carrinho.removerProduto("Arroz");
System.out.println("Quantidade: " + carrinho.quantidadeProdutos());
```

---

# 🔍 EXPLICAÇÃO DO DESAFIO EXTRA

O cálculo do total pertence ao carrinho porque ele conhece todos os itens:

```java
for (Produto produto : produtos) {
    total += produto.getValor();
}
```

O produto fornece seu valor por meio de `getValor()`, mas não precisa conhecer os outros produtos.

A remoção também pertence ao carrinho, pois a lista é seu atributo.

> Quando uma classe possui uma lista de objetos, os métodos de manipulação dessa lista normalmente ficam na classe que é dona da coleção.

---

# 🧠 Encapsulando a lista

A lista deve continuar privada:

```java
private List<Produto> produtos = new ArrayList<>();
```

Evite expor diretamente a lista sem necessidade:

```java
public List<Produto> getProdutos() {
    return produtos;
}
```

Se o getter retornar a lista original, outra classe poderá alterá-la sem passar pelas regras do carrinho.

Uma opção mais protegida é retornar uma cópia:

```java
public List<Produto> getProdutos() {
    return new ArrayList<>(produtos);
}
```

Neste módulo, vamos priorizar métodos específicos como `adicionarProduto` e `removerProduto`.

---

# 🎯 DESAFIO FINAL — Carrinho completo

Crie um carrinho usando a classe `Produto` do módulo 15, que possui:

- `nome`;
- `valor`;
- `UNIDADE unidade`.

A classe `Carrinho` deve ter:

1. lista privada `List<Produto>`;
2. método para adicionar;
3. método para remover por nome;
4. método para listar com unidade amigável;
5. método para calcular total;
6. método para informar quantidade;
7. método `estaVazio()` retornando `boolean`.

No `main`:

- crie um carrinho;
- adicione arroz, feijão, leite e teclado;
- liste os produtos;
- mostre quantidade e total;
- remova o feijão;
- mostre os dados novamente.

---

# 💡 SOLUÇÃO DO DESAFIO FINAL

```java
import java.util.ArrayList;
import java.util.List;

public class Carrinho {
    private List<Produto> produtos = new ArrayList<>();

    public void adicionarProduto(Produto produto) {
        if (produto != null) {
            produtos.add(produto);
        }
    }

    public void removerProduto(String nome) {
        if (nome == null || nome.isBlank()) {
            return;
        }

        for (int i = 0; i < produtos.size(); i++) {
            if (produtos.get(i).getNome().equalsIgnoreCase(nome)) {
                produtos.remove(i);
                return;
            }
        }
    }

    public void listarProdutos() {
        for (Produto produto : produtos) {
            System.out.println(produto.getNome()
                    + " - R$ " + produto.getValor()
                    + " por " + nomeUnidade(produto.getUnidade()));
        }
    }

    private String nomeUnidade(UNIDADE unidade) {
        return switch (unidade) {
            case UNIDADE -> "unidade";
            case QUILOGRAMA -> "quilograma";
            case LITRO -> "litro";
        };
    }

    public double calcularTotal() {
        double total = 0.0;

        for (Produto produto : produtos) {
            total += produto.getValor();
        }

        return total;
    }

    public int quantidadeProdutos() {
        return produtos.size();
    }

    public boolean estaVazio() {
        return produtos.isEmpty();
    }
}
```

```java
public class Main {
    public static void main(String[] args) {
        Carrinho carrinho = new Carrinho();

        carrinho.adicionarProduto(new Produto("Arroz", 2.5, UNIDADE.QUILOGRAMA));
        carrinho.adicionarProduto(new Produto("Feijão", 4.0, UNIDADE.QUILOGRAMA));
        carrinho.adicionarProduto(new Produto("Leite", 3.2, UNIDADE.LITRO));
        carrinho.adicionarProduto(new Produto("Teclado", 150.0, UNIDADE.UNIDADE));

        carrinho.listarProdutos();
        System.out.println("Quantidade: " + carrinho.quantidadeProdutos());
        System.out.println("Total: R$ " + carrinho.calcularTotal());

        carrinho.removerProduto("Feijão");

        System.out.println("Após remover Feijão:");
        carrinho.listarProdutos();
        System.out.println("Total: R$ " + carrinho.calcularTotal());
        System.out.println("Está vazio? " + carrinho.estaVazio());
    }
}
```

---

# 🔍 EXPLICAÇÃO DO DESAFIO FINAL

O objeto `Carrinho` possui seu próprio estado:

```text
Carrinho
└── produtos
    ├── Arroz
    ├── Feijão
    ├── Leite
    └── Teclado
```

O `Produto` não precisa conhecer o carrinho. O carrinho conhece seus produtos porque possui a lista.

Essa é uma relação de composição:

```java
private List<Produto> produtos = new ArrayList<>();
```

A lista pertence ao carrinho, e os métodos do carrinho controlam sua alteração.

### Responsabilidades

- `Produto.getValor()` retorna o valor de um produto.
- `Carrinho.calcularTotal()` soma os valores de todos os produtos.
- `Carrinho.removerProduto()` manipula a coleção.
- `Carrinho.estaVazio()` consulta o estado da lista.

---

# ✅ REVISÃO DO MÓDULO 16

Ao concluir este módulo, você deve conseguir:

- Criar uma classe que contém objetos de outra classe.
- Declarar `List<Produto>` como atributo.
- Inicializar a lista no objeto `Carrinho`.
- Encapsular a lista com `private`.
- Adicionar e remover objetos por métodos da classe.
- Percorrer a lista dentro da classe.
- Calcular informações a partir dos objetos contidos.
- Explicar composição de objetos.
- Separar as responsabilidades entre `Produto` e `Carrinho`.

---

# 🧠 CONCLUSÃO

No módulo 13, a lista estava diretamente no fluxo principal:

```java
List<Produto> produtos = new ArrayList<>();
```

No módulo 16, a lista passou a fazer parte de um objeto especializado:

```java
Carrinho carrinho = new Carrinho();
```

```java
private List<Produto> produtos = new ArrayList<>();
```

Essa evolução mostra como transformar um programa procedural em um modelo orientado a objetos, distribuindo dados e comportamentos entre classes.
