---
marp: true
theme: default
paginate: true
---

# JAVA 21
## Módulo 17 — Desafio Integrador: Sistema de Compra de Supermercado

**Metodologia:** Relembrando → Desafio 1 → Solução 1 → Explicação → Desafio Extra → Solução → Desafio Final → Solução Final → Revisão

---

# 🧠 RELEMBRANDO — O que já foi aprendido

Até aqui trabalhamos com:

- classes, objetos e construtores;
- getters e setters;
- `this`, `static` e `final`;
- enums e `switch`;
- `List<Produto>`;
- composição com `Carrinho` e `List<Produto>` dentro da classe.

Neste módulo vamos juntar tudo em um sistema simples de compra de supermercado.

---

# 🎯 OBJETIVO DO MÓDULO 17

Construir um sistema que permita:

1. cadastrar produtos;
2. adicionar produtos ao carrinho;
3. remover produtos do carrinho;
4. calcular subtotal e total da compra;
5. escolher forma de pagamento;
6. aplicar regras com `enum`, `switch`, `static`, `final` e composição.

---

# 🧱 MODELO DO SISTEMA

Classes e enums sugeridos:

- `enum UNIDADE { UNIDADE, QUILOGRAMA, LITRO }`
- `enum CATEGORIA { ALIMENTO, LIMPEZA, BEBIDA, HIGIENE }`
- `enum FORMA_PAGAMENTO { DINHEIRO, CARTAO, PIX }`
- `class Produto`
- `class ItemCarrinho`
- `class Carrinho`
- `class Caixa` (regras de checkout)
- `class Main` (simulação)

---

# 🧠 Enum e switch aplicados

Usaremos enums para representar opções fixas do domínio.

Exemplo com `switch`:

```java
public static double taxaPagamento(FORMA_PAGAMENTO formaPagamento) {
    return switch (formaPagamento) {
        case DINHEIRO -> 0.0;
        case PIX -> -0.05;      // desconto de 5%
        case CARTAO -> 0.02;    // taxa de 2%
    };
}
```

---

# 🎯 DESAFIO 1 — Cadastro de produtos

Crie a classe `Produto` com:

- `private static int totalProdutosCadastrados`;
- `private final int id`;
- `private String nome`;
- `private double valor`;
- `private UNIDADE unidade`;
- `private CATEGORIA categoria`;
- `private boolean ativo`.

Regras:

1. `id` deve ser gerado automaticamente no construtor.
2. `nome` não pode ser nulo/vazio.
3. `valor` deve ser maior que zero.
4. `unidade` e `categoria` não podem ser nulos.
5. Crie getters e setters com validação.
6. Crie método `String resumo()`.

---

# 💡 SOLUÇÃO 1

```java
public class Produto {
    private static int totalProdutosCadastrados = 0;

    private final int id;
    private String nome;
    private double valor;
    private UNIDADE unidade;
    private CATEGORIA categoria;
    private boolean ativo;

    public Produto(String nome, double valor, UNIDADE unidade, CATEGORIA categoria, boolean ativo) {
        totalProdutosCadastrados++;
        this.id = totalProdutosCadastrados;
        setNome(nome);
        setValor(valor);
        setUnidade(unidade);
        setCategoria(categoria);
        this.ativo = ativo;
    }

    public static int getTotalProdutosCadastrados() {
        return totalProdutosCadastrados;
    }

    public int getId() {
        return id;
    }

    public String getNome() {
        return nome;
    }

    public void setNome(String nome) {
        if (nome != null && !nome.isBlank()) {
            this.nome = nome;
        }
    }

    public double getValor() {
        return valor;
    }

    public void setValor(double valor) {
        if (valor > 0) {
            this.valor = valor;
        }
    }

    public UNIDADE getUnidade() {
        return unidade;
    }

    public void setUnidade(UNIDADE unidade) {
        if (unidade != null) {
            this.unidade = unidade;
        }
    }

    public CATEGORIA getCategoria() {
        return categoria;
    }

    public void setCategoria(CATEGORIA categoria) {
        if (categoria != null) {
            this.categoria = categoria;
        }
    }

    public boolean isAtivo() {
        return ativo;
    }

    public void setAtivo(boolean ativo) {
        this.ativo = ativo;
    }

    public String resumo() {
        return "#" + id + " " + nome + " - R$ " + valor + " (" + unidade + ", " + categoria + ")";
    }
}
```

---

# 🔍 EXPLICAÇÃO

Nesta classe usamos conceitos importantes:

- `final` no `id` para impedir alteração após criação;
- `static` para contador global de produtos;
- validações em setters;
- enum como tipo de atributo;
- método de instância (`resumo`) usando estado do objeto.

---

# 🎯 DESAFIO EXTRA — Carrinho com itens e subtotal

Agora implemente:

## `ItemCarrinho`

Atributos:

- `Produto produto`;
- `double quantidade`.

Métodos:

- `double calcularSubtotal()`.

Regras:

- quantidade deve ser maior que zero.

## `Carrinho`

Atributo:

- `private List<ItemCarrinho> itens = new ArrayList<>();`

Métodos:

- `adicionarProduto(Produto produto, double quantidade)`;
- `removerProdutoPorId(int idProduto)`;
- `listarItens()`;
- `calcularSubtotal()`;
- `quantidadeItens()`;
- `estaVazio()`.

---

# 💡 SOLUÇÃO DO DESAFIO EXTRA

```java
public class ItemCarrinho {
    private Produto produto;
    private double quantidade;

    public ItemCarrinho(Produto produto, double quantidade) {
        this.produto = produto;
        setQuantidade(quantidade);
    }

    public Produto getProduto() {
        return produto;
    }

    public double getQuantidade() {
        return quantidade;
    }

    public void setQuantidade(double quantidade) {
        if (quantidade > 0) {
            this.quantidade = quantidade;
        }
    }

    public double calcularSubtotal() {
        return produto.getValor() * quantidade;
    }
}
```

```java
import java.util.ArrayList;
import java.util.List;

public class Carrinho {
    private List<ItemCarrinho> itens = new ArrayList<>();

    public void adicionarProduto(Produto produto, double quantidade) {
        if (produto == null || !produto.isAtivo() || quantidade <= 0) {
            return;
        }

        itens.add(new ItemCarrinho(produto, quantidade));
    }

    public void removerProdutoPorId(int idProduto) {
        for (int i = 0; i < itens.size(); i++) {
            if (itens.get(i).getProduto().getId() == idProduto) {
                itens.remove(i);
                return;
            }
        }
    }

    public void listarItens() {
        for (ItemCarrinho item : itens) {
            System.out.println(item.getProduto().getNome()
                    + " | qtd: " + item.getQuantidade()
                    + " | subtotal: R$ " + item.calcularSubtotal());
        }
    }

    public double calcularSubtotal() {
        double total = 0.0;
        for (ItemCarrinho item : itens) {
            total += item.calcularSubtotal();
        }
        return total;
    }

    public int quantidadeItens() {
        return itens.size();
    }

    public boolean estaVazio() {
        return itens.isEmpty();
    }
}
```

---

# 🔍 EXPLICAÇÃO DO DESAFIO EXTRA

Aqui aplicamos composição em dois níveis:

```text
Carrinho
└── List<ItemCarrinho>
    └── Produto
```

- `Carrinho` contém vários `ItemCarrinho`.
- `ItemCarrinho` contém um `Produto`.
- O subtotal vem de `produto.valor * quantidade`.

---

# 🎯 DESAFIO FINAL — Checkout completo

Crie a classe `Caixa` com:

- constante `private static final double DESCONTO_MAXIMO = 0.10`;
- método `calcularTotalFinal(Carrinho carrinho, FORMA_PAGAMENTO formaPagamento, double descontoAplicado)`.

Regras:

1. Se carrinho estiver vazio, total = 0.
2. O desconto aplicado deve ficar entre `0` e `DESCONTO_MAXIMO`.
3. Aplicar taxa/desconto por forma de pagamento com `switch`:
   - `DINHEIRO`: 0%
   - `PIX`: -5%
   - `CARTAO`: +2%
4. Total final não pode ser negativo.

---

# 💡 SOLUÇÃO DO DESAFIO FINAL

```java
public class Caixa {
    private static final double DESCONTO_MAXIMO = 0.10;

    public double calcularTotalFinal(Carrinho carrinho,
                                     FORMA_PAGAMENTO formaPagamento,
                                     double descontoAplicado) {

        if (carrinho == null || carrinho.estaVazio()) {
            return 0.0;
        }

        double subtotal = carrinho.calcularSubtotal();

        if (descontoAplicado < 0 || descontoAplicado > DESCONTO_MAXIMO) {
            descontoAplicado = 0.0;
        }

        double totalComDesconto = subtotal - (subtotal * descontoAplicado);

        double taxaOuDescontoPagamento = switch (formaPagamento) {
            case DINHEIRO -> 0.0;
            case PIX -> -0.05;
            case CARTAO -> 0.02;
        };

        double totalFinal = totalComDesconto + (totalComDesconto * taxaOuDescontoPagamento);

        return Math.max(totalFinal, 0.0);
    }
}
```

---

# 💡 SIMULAÇÃO COMPLETA (Main)

```java
import java.util.ArrayList;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        Produto arroz = new Produto("Arroz", 2.5, UNIDADE.QUILOGRAMA, CATEGORIA.ALIMENTO, true);
        Produto feijao = new Produto("Feijão", 4.0, UNIDADE.QUILOGRAMA, CATEGORIA.ALIMENTO, true);
        Produto leite = new Produto("Leite", 3.2, UNIDADE.LITRO, CATEGORIA.BEBIDA, true);
        Produto sabao = new Produto("Sabão", 6.5, UNIDADE.UNIDADE, CATEGORIA.LIMPEZA, false);

        System.out.println(arroz.resumo());
        System.out.println(feijao.resumo());
        System.out.println(leite.resumo());
        System.out.println(sabao.resumo());

        Carrinho carrinho = new Carrinho();
        carrinho.adicionarProduto(arroz, 2);
        carrinho.adicionarProduto(feijao, 1);
        carrinho.adicionarProduto(leite, 3);
        carrinho.adicionarProduto(sabao, 1); // ignorado: inativo

        System.out.println("\nItens no carrinho:");
        carrinho.listarItens();

        System.out.println("Subtotal: R$ " + carrinho.calcularSubtotal());

        Caixa caixa = new Caixa();
        double totalFinal = caixa.calcularTotalFinal(carrinho, FORMA_PAGAMENTO.PIX, 0.08);

        System.out.println("Total final (PIX + desconto): R$ " + totalFinal);
        System.out.println("Total de produtos cadastrados: " + Produto.getTotalProdutosCadastrados());
    }
}
```

---

# ✅ REVISÃO DO MÓDULO 17

Ao concluir este módulo, você deve conseguir:

- modelar um domínio simples com múltiplas classes;
- usar composição entre classes;
- aplicar enums em atributos e `switch`;
- usar `static`, `final` e validações de regra;
- trabalhar com listas de objetos e agregações;
- organizar responsabilidades entre `Produto`, `Carrinho`, `ItemCarrinho` e `Caixa`;
- simular fluxo completo de compra.

---

# 🧠 CONCLUSÃO

Este módulo representa um desafio integrador de nível iniciante/intermediário. Ele demonstra como os conceitos aprendidos se conectam em um sistema realista.

Próximos passos naturais:

- persistência em arquivo/banco;
- menu interativo no console;
- tratamento de exceções mais detalhado;
- testes automatizados.
