---
marp: true
theme: default
paginate: true
---

# JAVA 21
## Módulo 10 — Introdução à Orientação a Objetos

**Metodologia:** Relembrando → Desafio 1 → Solução 1 → Explicação do Desafio 1 → Desafio Extra → Solução do Desafio Extra → Explicação do Desafio Extra → Desafio Final → Solução do Desafio Final → Explicação do Desafio Final

---

# 🧠 RELEMBRANDO — Métodos vivem dentro de classes

Nos módulos anteriores, criamos métodos dentro de uma classe `Main` e usamos variáveis locais:

```java
public class Main {
    public static void main(String[] args) {
        String nome = "Teclado";
        double preco = 150.0;

        exibirProduto(nome, preco);
    }

    public static void exibirProduto(String nome, double preco) {
        System.out.println(nome + " - R$ " + preco);
    }
}
```

Agora vamos dar um passo importante:

- Os dados passarão a pertencer a uma classe.
- Os métodos poderão usar diretamente esses dados.
- Cada objeto criado a partir da classe terá seu próprio estado.

> A classe será o modelo. O objeto será uma instância criada a partir desse modelo.

---

# 🧠 O que é uma classe?

Uma **classe** descreve as características e os comportamentos de um tipo de objeto.

### Classe `Produto`

| Elemento | Representa |
|---|---|
| `nome` | Uma característica do produto |
| `preco` | Uma característica do produto |
| `quantidadeEstoque` | Uma característica do produto |
| `ativo` | Uma característica do produto |
| `exibirResumo()` | Um comportamento do produto |
| `temEstoque()` | Um comportamento do produto |

```java
public class Produto {
    String nome;
    double preco;
    int quantidadeEstoque;
    boolean ativo;
}
```

Essas variáveis declaradas dentro da classe são chamadas de **atributos** ou **campos**.

---

# 🧠 O que é um objeto?

Um **objeto** é uma instância de uma classe.

```java
Produto produto = new Produto();
```

- `Produto` é o tipo da variável.
- `produto` é a referência para o objeto.
- `new Produto()` cria uma nova instância da classe.

Podemos preencher os atributos e chamar os métodos do objeto:

```java
produto.nome = "Teclado";
produto.preco = 150.0;
produto.quantidadeEstoque = 10;
produto.ativo = true;

produto.exibirResumo();
```

Cada objeto pode possuir valores diferentes para os mesmos atributos.

---

# 🎯 DESAFIO 1 — Criando a classe `Produto`

### Contexto

Uma loja precisa representar um produto usando uma classe própria.

### Regras

1. Crie uma classe chamada `Produto`.
2. Declare os atributos `nome`, `preco`, `quantidadeEstoque` e `ativo`.
3. Use os tipos `String`, `double`, `int` e `boolean`.
4. Crie um método `exibirResumo()` que mostre todos os atributos do produto.
5. Crie um método `temEstoque()` que retorne `true` quando a quantidade em estoque for maior que zero.
6. Crie um método `alterarPreco(double novoPreco)` que atualize o preço somente quando o novo valor for maior ou igual a zero.
7. No `main`, crie um produto, preencha seus atributos e chame os métodos.

### Dados de teste

- `nome = "Teclado"`
- `preco = 150.0`
- `quantidadeEstoque = 10`
- `ativo = true`

### O que o aluno precisa fazer

Criar uma classe com atributos e métodos que utilizem o estado do próprio objeto.

---

# 💡 SOLUÇÃO 1

```java
public class Produto {
    String nome;
    double preco;
    int quantidadeEstoque;
    boolean ativo;

    public void exibirResumo() {
        System.out.println("Nome: " + nome);
        System.out.println("Preço: R$ " + preco);
        System.out.println("Estoque: " + quantidadeEstoque);
        System.out.println("Ativo: " + ativo);
    }

    public boolean temEstoque() {
        return quantidadeEstoque > 0;
    }

    public void alterarPreco(double novoPreco) {
        if (novoPreco >= 0) {
            preco = novoPreco;
        }
    }
}
```

```java
public class Main {
    public static void main(String[] args) {
        Produto produto = new Produto();

        produto.nome = "Teclado";
        produto.preco = 150.0;
        produto.quantidadeEstoque = 10;
        produto.ativo = true;

        produto.exibirResumo();
        System.out.println("Tem estoque? " + produto.temEstoque());

        produto.alterarPreco(175.0);
        produto.exibirResumo();
    }
}
```

---

# 🔍 EXPLICAÇÃO DO DESAFIO 1

Os métodos `exibirResumo`, `temEstoque` e `alterarPreco` estão dentro da classe `Produto`.

Por isso, eles podem acessar diretamente os atributos do objeto:

```java
public boolean temEstoque() {
    return quantidadeEstoque > 0;
}
```

Não foi necessário passar `quantidadeEstoque` como parâmetro. O método já consegue consultar o estado do próprio produto.

### Estado do objeto

O conjunto dos valores dos atributos representa o **estado** do objeto.

```java
produto.preco = 150.0;
produto.alterarPreco(175.0);
```

Depois da chamada, o estado do objeto mudou: `preco` passou a valer `175.0`.

### Pontos de atenção

- A classe contém atributos e métodos.
- O objeto é criado com `new`.
- Cada objeto possui seu próprio estado.
- Um método de instância pode usar os atributos da própria classe.
- Métodos não precisam receber como parâmetro um atributo que já pertence ao objeto.

---

# 🧠 `this`: o objeto atual

A palavra-chave `this` representa o objeto atual.

Ela é muito útil quando o parâmetro tem o mesmo nome do atributo:

```java
public void alterarPreco(double preco) {
    if (preco >= 0) {
        this.preco = preco;
    }
}
```

- `this.preco` representa o atributo do objeto.
- `preco` representa o parâmetro recebido pelo método.

Sem `this`, a atribuição abaixo não deixaria clara a diferença:

```java
preco = preco;
```

> Neste módulo, `this` será usado para reforçar a diferença entre o estado do objeto e os valores recebidos pelos métodos.

---

# 🎯 DESAFIO EXTRA — Métodos que alteram o estado

### Contexto

Agora o produto deverá controlar sua quantidade em estoque e seu status de ativação.

### Regras

Adicione os seguintes métodos à classe `Produto`:

1. `adicionarEstoque(int quantidade)` — soma a quantidade recebida ao estoque quando ela for maior que zero.
2. `removerEstoque(int quantidade)` — remove a quantidade somente quando ela for maior que zero e não ultrapassar o estoque atual.
3. `ativar()` — altera o atributo `ativo` para `true`.
4. `desativar()` — altera o atributo `ativo` para `false`.
5. `podeSerVendido()` — retorna `true` somente quando o produto estiver ativo e tiver estoque.

### Dados de teste

- Produto ativo.
- Estoque inicial de `10` unidades.
- Adicionar `5` unidades.
- Remover `3` unidades.
- Tentar remover `20` unidades.

### O que o aluno precisa fazer

Criar métodos que leiam e alterem os atributos do próprio objeto, mantendo regras simples de validação.

---

# 💡 SOLUÇÃO DO DESAFIO EXTRA

```java
public class Produto {
    String nome;
    double preco;
    int quantidadeEstoque;
    boolean ativo;

    public void adicionarEstoque(int quantidade) {
        if (quantidade > 0) {
            quantidadeEstoque += quantidade;
        }
    }

    public void removerEstoque(int quantidade) {
        if (quantidade > 0 && quantidade <= quantidadeEstoque) {
            quantidadeEstoque -= quantidade;
        }
    }

    public void ativar() {
        ativo = true;
    }

    public void desativar() {
        ativo = false;
    }

    public boolean podeSerVendido() {
        return ativo && quantidadeEstoque > 0;
    }
}
```

```java
public class Main {
    public static void main(String[] args) {
        Produto produto = new Produto();
        produto.nome = "Teclado";
        produto.preco = 150.0;
        produto.quantidadeEstoque = 10;
        produto.ativo = true;

        produto.adicionarEstoque(5);
        produto.removerEstoque(3);
        produto.removerEstoque(20);

        System.out.println("Estoque: " + produto.quantidadeEstoque);
        System.out.println("Pode ser vendido? " + produto.podeSerVendido());
    }
}
```

---

# 🔍 EXPLICAÇÃO DO DESAFIO EXTRA

Os métodos controlam o estado do próprio produto.

```java
public void adicionarEstoque(int quantidade) {
    if (quantidade > 0) {
        quantidadeEstoque += quantidade;
    }
}
```

O método não precisa receber o estoque atual. Ele acessa `quantidadeEstoque` diretamente porque esse atributo pertence ao objeto.

### Resultado do exemplo

- Estoque inicial: `10`
- Após adicionar `5`: `15`
- Após remover `3`: `12`
- A tentativa de remover `20` é ignorada, pois ultrapassa o estoque disponível.

### Método de consulta x método de alteração

- `podeSerVendido()` consulta o estado e retorna um `boolean`.
- `adicionarEstoque()` altera o estado e retorna `void`.
- `desativar()` altera o estado e retorna `void`.

### Erros comuns

- Permitir estoque negativo.
- Aceitar quantidade zero ou negativa.
- Usar variáveis locais em vez dos atributos da classe.
- Criar métodos fora da classe `Produto`.

---

# 🧠 Constantes com `final`

A palavra-chave `final` impede que uma variável receba outro valor depois da sua inicialização.

Quando a constante pertence à classe e possui o mesmo valor para todos os objetos, usamos:

```java
private static final double DESCONTO_MAXIMO = 0.30;
```

- `private`: só a própria classe acessa diretamente.
- `static`: existe uma única cópia para a classe.
- `final`: o valor não pode ser alterado.
- `DESCONTO_MAXIMO`: constantes usam normalmente letras maiúsculas e `_`.

Também podemos ter um atributo `final` específico de cada produto:

```java
private final String codigo;
```

Nesse caso, cada objeto recebe seu próprio código, mas o código não pode ser trocado depois de definido.

> `final` ajuda a deixar explícito quais valores são constantes e quais valores podem mudar.

---

# 🎯 DESAFIO FINAL — Produto com constantes e construtor

### Contexto

Vamos melhorar a classe `Produto` usando encapsulamento inicial, construtor e constantes.

### Regras

1. Crie a classe `Produto`.
2. Declare a constante `DESCONTO_MAXIMO` com o valor `0.30`.
3. Declare o atributo `codigo` como `final`.
4. Declare os demais atributos como `private`: `nome`, `preco`, `quantidadeEstoque` e `ativo`.
5. Crie um construtor que receba todos os valores necessários para criar um produto.
6. No construtor, use `this` para diferenciar atributos e parâmetros.
7. Crie o método `aplicarDesconto(double percentual)`.
8. O desconto deve ser aplicado somente quando estiver entre `0` e `DESCONTO_MAXIMO`.
9. Crie o método `temEstoqueMinimo()` que retorne `true` quando o estoque for maior ou igual a uma constante `ESTOQUE_MINIMO`, com valor `5`.
10. Crie o método `exibirResumo()` para retornar uma `String` com os dados do produto.
11. Crie o método `podeSerVendido()` que retorne `true` quando o produto estiver ativo e possuir estoque.
12. No `main`, crie um produto, aplique um desconto válido, tente aplicar um desconto inválido e exiba os resultados.

### Dados de teste

- `codigo = "TEC-001"`
- `nome = "Teclado"`
- `preco = 150.0`
- `quantidadeEstoque = 10`
- `ativo = true`
- desconto válido: `0.10`
- desconto inválido: `0.50`

### O que o aluno precisa fazer

Criar uma classe que concentre dados, comportamentos e regras simples de um produto.

---

# 💡 SOLUÇÃO DO DESAFIO FINAL

```java
public class Produto {
    private static final double DESCONTO_MAXIMO = 0.30;
    private static final int ESTOQUE_MINIMO = 5;

    private final String codigo;
    private String nome;
    private double preco;
    private int quantidadeEstoque;
    private boolean ativo;

    public Produto(String codigo, String nome, double preco,
                   int quantidadeEstoque, boolean ativo) {
        this.codigo = codigo;
        this.nome = nome;
        this.preco = preco;
        this.quantidadeEstoque = quantidadeEstoque;
        this.ativo = ativo;
    }

    public void aplicarDesconto(double percentual) {
        if (percentual >= 0 && percentual <= DESCONTO_MAXIMO) {
            preco -= preco * percentual;
        }
    }

    public boolean temEstoqueMinimo() {
        return quantidadeEstoque >= ESTOQUE_MINIMO;
    }

    public boolean podeSerVendido() {
        return ativo && quantidadeEstoque > 0;
    }

    public String exibirResumo() {
        return "Código: " + codigo
                + " | Nome: " + nome
                + " | Preço: R$ " + preco
                + " | Estoque: " + quantidadeEstoque
                + " | Ativo: " + ativo;
    }
}
```

```java
public class Main {
    public static void main(String[] args) {
        Produto produto = new Produto(
                "TEC-001",
                "Teclado",
                150.0,
                10,
                true
        );

        produto.aplicarDesconto(0.10);
        produto.aplicarDesconto(0.50);

        System.out.println(produto.exibirResumo());
        System.out.println("Tem estoque mínimo? " + produto.temEstoqueMinimo());
        System.out.println("Pode ser vendido? " + produto.podeSerVendido());
    }
}
```

---

# 🔍 EXPLICAÇÃO DO DESAFIO FINAL

### O construtor

O construtor é executado no momento em que o objeto é criado:

```java
Produto produto = new Produto("TEC-001", "Teclado", 150.0, 10, true);
```

Ele garante que o produto já seja criado com seus dados principais.

### O atributo `final`

```java
private final String codigo;
```

O código precisa ser inicializado no construtor e não pode ser substituído depois.

Isso representa uma regra do modelo: o produto possui um código fixo após sua criação.

### Constantes da classe

```java
private static final double DESCONTO_MAXIMO = 0.30;
private static final int ESTOQUE_MINIMO = 5;
```

Esses valores são regras fixas utilizadas pelos métodos. Em vez de espalhar números sem significado pelo código, damos nomes claros às regras.

### O método de desconto

```java
public void aplicarDesconto(double percentual) {
    if (percentual >= 0 && percentual <= DESCONTO_MAXIMO) {
        preco -= preco * percentual;
    }
}
```

O método usa o atributo `preco` do próprio produto e a constante `DESCONTO_MAXIMO` da classe.

Com o preço inicial de `150.0` e desconto de `10%`:

```text
150.0 - (150.0 * 0.10) = 135.0
```

O desconto de `50%` não é aplicado porque ultrapassa o limite definido pela constante.

### Pontos de atenção

- `private` protege os atributos contra acesso direto de outras classes.
- `final` impede a alteração do código após a criação.
- `static final` representa uma constante compartilhada pela classe.
- O construtor inicializa o estado do objeto.
- Os métodos representam comportamentos do produto.
- O método `exibirResumo()` retorna uma `String`; ele não precisa imprimir diretamente.

### Erros comuns

- Tentar alterar `codigo` depois de criar o produto.
- Esquecer de inicializar o atributo `final` no construtor.
- Usar `DESCONTO_MAXIMO` como se fosse um percentual inteiro (`30` em vez de `0.30`).
- Aplicar desconto negativo ou acima do limite.
- Criar métodos que recebem todos os atributos como parâmetros mesmo quando eles já pertencem ao objeto.
- Confundir a classe `Produto` com o objeto criado no `main`.

---

# ✅ REVISÃO DO MÓDULO 10

Ao concluir este módulo, você deve conseguir:

- Identificar uma classe como um modelo de dados e comportamentos.
- Criar objetos usando `new`.
- Declarar atributos de tipos simples e `String`.
- Criar métodos dentro da classe.
- Usar os atributos do próprio objeto dentro dos métodos.
- Diferenciar atributos, parâmetros e variáveis locais.
- Utilizar `this` para representar o objeto atual.
- Criar construtores para inicializar objetos.
- Usar `final` em atributos que não devem mudar.
- Criar constantes com `static final`.
- Separar dados e comportamentos dentro de uma classe simples.
