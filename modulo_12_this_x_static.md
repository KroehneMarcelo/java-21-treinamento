---
marp: true
theme: default
paginate: true
---

# JAVA 21
## Módulo 12 — `this` x `static`

**Metodologia:** Relembrando → Desafio 1 → Solução 1 → Explicação do Desafio 1 → Desafio Extra → Solução do Desafio Extra → Explicação do Desafio Extra → Desafio Final → Solução do Desafio Final → Explicação do Desafio Final

---

# 🧠 RELEMBRANDO — Classes e objetos

Nos módulos anteriores, criamos objetos a partir de uma classe:

```java
Produto arroz = new Produto();
Produto feijao = new Produto();
```

Cada chamada de `new Produto()` cria uma instância diferente.

```text
arroz  ──► Produto A { valor: 2.5 }
feijao ──► Produto B { valor: 4.0 }
```

Cada objeto possui seus próprios atributos e pode apresentar um estado diferente dos demais objetos da mesma classe.

Agora vamos diferenciar dois tipos de membros:

- **Membros de instância:** pertencem a cada objeto.
- **Membros `static`:** pertencem à classe.

---

# 🧠 Membros de instância

Um atributo sem `static` pertence a cada objeto criado.

```java
public class Produto {
    private double valor;

    public double getValor() {
        return valor;
    }

    public void setValor(double valor) {
        this.valor = valor;
    }
}
```

```java
Produto arroz = new Produto();
Produto feijao = new Produto();

arroz.setValor(2.5);
feijao.setValor(4.0);
```

Cada instância armazena seu próprio valor:

```text
arroz  ──► Produto A { valor: 2.5 }
feijao ──► Produto B { valor: 4.0 }
```

O método `setValor` altera o atributo do objeto que recebeu a chamada.

---

# 🧠 O significado de `this`

A palavra-chave `this` representa o **objeto atual**.

```java
public void setValor(double valor) {
    this.valor = valor;
}
```

Nesta linha:

- `this.valor` é o atributo pertencente ao objeto atual.
- `valor` é o parâmetro recebido pelo método.

Quando chamamos:

```java
arroz.setValor(2.5);
```

O `this` representa o objeto `arroz`.

Quando chamamos:

```java
feijao.setValor(4.0);
```

O `this` representa o objeto `feijao`.

> O significado de `this` muda conforme o objeto que chamou o método.

---

# 🎯 DESAFIO 1 — `this` em objetos diferentes

### Contexto

Um mercado possui dois produtos. A classe `Produto` deve guardar o nome e o valor de cada produto.

### Regras

1. Crie uma classe `Produto`.
2. Declare os atributos privados `nome` e `valor`.
3. Crie os métodos `getNome`, `setNome`, `getValor` e `setValor`.
4. Use `this` nos setters.
5. No `main`, crie os objetos `arroz` e `feijao`.
6. Defina valores diferentes para cada objeto.
7. Exiba os valores utilizando os getters.

### Dados de teste

- Arroz: `R$ 2.50`.
- Feijão: `R$ 4.00`.

### O que o aluno precisa observar

O mesmo método `setValor` é executado para objetos diferentes, mas o `this` representa uma instância diferente em cada chamada.

---

# 💡 SOLUÇÃO 1

```java
public class Produto {
    private String nome;
    private double valor;

    public String getNome() {
        return nome;
    }

    public void setNome(String nome) {
        this.nome = nome;
    }

    public double getValor() {
        return valor;
    }

    public void setValor(double valor) {
        this.valor = valor;
    }
}
```

```java
public class Main {
    public static void main(String[] args) {
        Produto arroz = new Produto();
        arroz.setNome("Arroz");
        arroz.setValor(2.5);

        Produto feijao = new Produto();
        feijao.setNome("Feijão");
        feijao.setValor(4.0);

        System.out.println(arroz.getNome() + ": R$ " + arroz.getValor());
        System.out.println(feijao.getNome() + ": R$ " + feijao.getValor());
    }
}
```

---

# 🔍 EXPLICAÇÃO DO DESAFIO 1

O método `setValor` é declarado uma única vez na classe:

```java
public void setValor(double valor) {
    this.valor = valor;
}
```

Mas ele pode ser executado por diferentes objetos:

```java
arroz.setValor(2.5);
feijao.setValor(4.0);
```

Podemos interpretar as chamadas assim:

```java
// Nesta chamada, this representa arroz.
arroz.setValor(2.5);

// Nesta chamada, this representa feijao.
feijao.setValor(4.0);
```

O método é o mesmo, mas o atributo alterado pertence ao objeto que chamou o método.

### Pontos de atenção

- `this` só faz sentido no contexto de uma instância.
- `this.valor` não é uma variável compartilhada por todos os produtos.
- Cada objeto possui seu próprio atributo `valor`.
- Métodos de instância podem acessar atributos de instância diretamente.

---

# 🧠 Métodos de instância

Métodos sem `static` são chamados de **métodos de instância**.

Eles precisam de um objeto para serem executados:

```java
Produto produto = new Produto();
produto.setValor(10.0);
double valorAtual = produto.getValor();
```

Também podemos criar um método de instância que use vários atributos do próprio objeto:

```java
public String exibirResumo() {
    return nome + " - R$ " + valor;
}
```

A chamada é feita a partir do objeto:

```java
System.out.println(produto.exibirResumo());
```

Esse método utiliza o estado da instância que realizou a chamada.

---

# 🧠 O que é `static`?

A palavra-chave `static` indica que um membro pertence à **classe**, e não a um objeto específico.

```java
public class Produto {
    private static int quantidadeCriada = 0;
}
```

Existe uma única variável `quantidadeCriada` compartilhada pela classe `Produto`.

Para acessar um membro `static`, usamos o nome da classe:

```java
Produto.quantidadeCriada;
```

Quando o membro é privado, o acesso externo deve ser feito por um método `static` público:

```java
Produto.getQuantidadeCriada();
```

---

# 🧠 Atributo de instância x atributo `static`

```java
public class Produto {
    private String nome;                    // instância
    private static int quantidadeCriada;    // classe
}
```

### Atributo de instância

```text
Produto A { nome: "Arroz" }
Produto B { nome: "Feijão" }
```

Cada objeto tem seu próprio `nome`.

### Atributo `static`

```text
Produto.quantidadeCriada = 2
```

Existe apenas um valor compartilhado pela classe.

| Característica | Instância | `static` |
|---|---|---|
| Pertence a | Um objeto | À classe |
| Precisa de `new`? | Sim, para existir o objeto | Não para acessar o membro da classe |
| Pode usar `this`? | Sim | Não |
| Cada objeto tem uma cópia? | Sim | Não, o valor é compartilhado |
| Acesso recomendado | `objeto.metodo()` | `Classe.metodo()` |

---

# 🧠 Método `static`

Um método `static` pode ser chamado sem criar um objeto:

```java
public class Calculadora {
    public static double somar(double primeiroValor, double segundoValor) {
        return primeiroValor + segundoValor;
    }
}
```

```java
double resultado = Calculadora.somar(2.5, 4.0);
System.out.println(resultado);
```

O método pertence à classe `Calculadora` e não depende do estado de um objeto específico.

### Características

- É chamado usando o nome da classe.
- Não precisa de `new Calculadora()`.
- Não pode usar `this`.
- Não acessa diretamente atributos de instância.
- É adequado para operações que dependem apenas dos parâmetros recebidos ou de dados `static`.

---

# 🧠 Por que um método `static` não pode usar `this`?

Considere:

```java
public class Produto {
    private double valor;

    public static void exibirValor() {
        System.out.println(this.valor);
    }
}
```

Esse código não compila.

O método `exibirValor` é da classe, mas `this` representa um objeto específico. Como o método foi chamado sem indicar qual produto deve ser usado, não existe um `this` disponível.

A chamada de um método `static` acontece assim:

```java
Produto.exibirValor();
```

Qual objeto deveria representar o `this`?

A resposta é: nenhum. Por isso, métodos `static` não podem acessar `this` nem atributos de instância diretamente.

---

# 🎯 DESAFIO EXTRA — Contando produtos criados

### Contexto

A loja quer saber quantos objetos `Produto` foram criados durante a execução do programa.

### Regras

1. Crie um atributo privado de instância `nome`.
2. Crie um atributo privado e `static` chamado `quantidadeCriada`.
3. No construtor da classe, incremente `quantidadeCriada`.
4. Crie o método de instância `getNome()`.
5. Crie o método `static getQuantidadeCriada()`.
6. Crie três objetos `Produto` no `main`.
7. Exiba o nome de cada produto.
8. Exiba a quantidade total criada usando o nome da classe.

### O que o aluno precisa observar

Os nomes pertencem a objetos diferentes, mas a quantidade criada é compartilhada pela classe.

---

# 💡 SOLUÇÃO DO DESAFIO EXTRA

```java
public class Produto {
    private String nome;
    private static int quantidadeCriada;

    public Produto(String nome) {
        this.nome = nome;
        quantidadeCriada++;
    }

    public String getNome() {
        return nome;
    }

    public static int getQuantidadeCriada() {
        return quantidadeCriada;
    }
}
```

```java
public class Main {
    public static void main(String[] args) {
        Produto arroz = new Produto("Arroz");
        Produto feijao = new Produto("Feijão");
        Produto macarrao = new Produto("Macarrão");

        System.out.println(arroz.getNome());
        System.out.println(feijao.getNome());
        System.out.println(macarrao.getNome());

        System.out.println("Produtos criados: " + Produto.getQuantidadeCriada());
    }
}
```

---

# 🔍 EXPLICAÇÃO DO DESAFIO EXTRA

O atributo `nome` é de instância:

```java
private String nome;
```

Cada produto possui seu próprio nome.

O atributo `quantidadeCriada` é `static`:

```java
private static int quantidadeCriada;
```

Existe uma única variável compartilhada por todos os objetos `Produto`.

A cada execução do construtor:

```java
quantidadeCriada++;
```

O contador compartilhado é incrementado.

### Estado representado

```text
arroz   ──► Produto { nome: "Arroz" }
feijao  ──► Produto { nome: "Feijão" }
macarrao ─► Produto { nome: "Macarrão" }

Produto.quantidadeCriada = 3
```

### Forma correta de acesso

```java
Produto.getQuantidadeCriada();
```

O método é chamado pelo nome da classe porque a informação pertence à classe, e não a um produto individual.

Embora o Java permita algumas chamadas `static` usando uma variável de objeto, a forma recomendada e mais clara é usar o nome da classe.

---

# 🧠 `this` x `static`

A comparação principal deste módulo é:

| `this` | `static` |
|---|---|
| Representa o objeto atual | Indica um membro da classe |
| Relacionado à instância | Compartilhado pela classe |
| Usado em métodos de instância | Usado em atributos e métodos da classe |
| Pode acessar atributos da instância | Não pode acessar atributos de instância diretamente |
| Não existe em método `static` | Pode ser usado sem criar um objeto |

### Exemplo combinado

```java
public class Produto {
    private String nome;
    private static int quantidadeCriada;

    public Produto(String nome) {
        this.nome = nome;
        quantidadeCriada++;
    }

    public String getNome() {
        return this.nome;
    }

    public static int getQuantidadeCriada() {
        return quantidadeCriada;
    }
}
```

- `this.nome` acessa o nome do objeto atual.
- `quantidadeCriada` acessa o contador compartilhado da classe.

---

# 🎯 DESAFIO FINAL — Produto, `this` e `static`

### Contexto

Uma loja deseja controlar seus produtos. Cada produto possui nome e valor próprios, enquanto a classe precisa controlar um contador geral de produtos criados e definir um limite de desconto compartilhado.

### Regras

1. Crie a classe `Produto`.
2. Declare os atributos privados de instância `nome` e `valor`.
3. Declare o atributo privado e `static` `quantidadeCriada`.
4. Declare a constante `private static final double DESCONTO_MAXIMO = 0.30`.
5. Crie um construtor que receba `nome` e `valor`.
6. Use `this` para inicializar os atributos de instância.
7. Incremente `quantidadeCriada` no construtor.
8. Crie getters e setters para `nome` e `valor`.
9. Crie o método de instância `aplicarDesconto(double percentual)`.
10. O desconto deve ser aplicado somente quando estiver entre `0` e `DESCONTO_MAXIMO`.
11. Crie o método `static getQuantidadeCriada()`.
12. Crie o método `exibirResumo()` como método de instância.
13. No `main`, crie arroz e feijão com valores diferentes.
14. Aplique desconto somente no arroz.
15. Exiba os dois produtos e a quantidade total criada.
16. Explique por que o desconto do arroz não altera o valor do feijão.

### Dados de teste

- Arroz: valor `2.5`.
- Feijão: valor `4.0`.
- Desconto do arroz: `0.10`.
- Desconto inválido no feijão: `0.50`.

---

# 💡 SOLUÇÃO DO DESAFIO FINAL

```java
public class Produto {
    private static final double DESCONTO_MAXIMO = 0.30;
    private static int quantidadeCriada;

    private String nome;
    private double valor;

    public Produto(String nome, double valor) {
        this.nome = nome;
        this.valor = valor;
        quantidadeCriada++;
    }

    public String getNome() {
        return this.nome;
    }

    public void setNome(String nome) {
        this.nome = nome;
    }

    public double getValor() {
        return this.valor;
    }

    public void setValor(double valor) {
        if (valor >= 0) {
            this.valor = valor;
        }
    }

    public void aplicarDesconto(double percentual) {
        if (percentual >= 0 && percentual <= DESCONTO_MAXIMO) {
            this.valor -= this.valor * percentual;
        }
    }

    public String exibirResumo() {
        return this.nome + ": R$ " + this.valor;
    }

    public static int getQuantidadeCriada() {
        return quantidadeCriada;
    }
}
```

```java
public class Main {
    public static void main(String[] args) {
        Produto arroz = new Produto("Arroz", 2.5);
        Produto feijao = new Produto("Feijão", 4.0);

        arroz.aplicarDesconto(0.10);
        feijao.aplicarDesconto(0.50);

        System.out.println(arroz.exibirResumo());
        System.out.println(feijao.exibirResumo());
        System.out.println("Produtos criados: " + Produto.getQuantidadeCriada());
    }
}
```

---

# 🔍 EXPLICAÇÃO DO DESAFIO FINAL

Quando os objetos são criados:

```java
Produto arroz = new Produto("Arroz", 2.5);
Produto feijao = new Produto("Feijão", 4.0);
```

A memória pode ser representada assim:

```text
arroz  ──► Produto A { nome: "Arroz",  valor: 2.5 }
feijao ──► Produto B { nome: "Feijão", valor: 4.0 }

Produto.quantidadeCriada = 2
```

O desconto é aplicado por um método de instância:

```java
arroz.aplicarDesconto(0.10);
```

O `this` representa `arroz`, então somente o valor do objeto arroz é alterado:

```text
arroz  ──► Produto A { nome: "Arroz",  valor: 2.25 }
feijao ──► Produto B { nome: "Feijão", valor: 4.0 }
```

A constante `DESCONTO_MAXIMO` pertence à classe e é compartilhada por todos os objetos. Ela não representa o valor de um produto específico.

### Saída esperada

```text
Arroz: R$ 2.25
Feijão: R$ 4.0
Produtos criados: 2
```

### Fluxo do desconto do feijão

```java
feijao.aplicarDesconto(0.50);
```

O percentual `0.50` ultrapassa `DESCONTO_MAXIMO`, que vale `0.30`. Por isso, o valor do feijão continua `4.0`.

---

# 🧠 Quando usar instância e quando usar `static`?

### Use membros de instância quando:

- O dado pertence a um objeto específico.
- Cada objeto pode possuir um valor diferente.
- O comportamento depende do estado daquele objeto.
- Você precisa usar `this`.

Exemplos:

```java
arroz.setValor(2.5);
arroz.aplicarDesconto(0.10);
arroz.exibirResumo();
```

### Use `static` quando:

- O dado pertence à classe inteira.
- O valor é compartilhado entre todas as instâncias.
- O método não depende de um objeto específico.
- A operação utiliza apenas parâmetros e/ou dados `static`.

Exemplos:

```java
Produto.getQuantidadeCriada();
Calculadora.somar(2.0, 3.0);
```

### Evite usar `static` apenas para fugir da criação de objetos

Se um método precisa consultar o nome ou o valor de um produto específico, ele provavelmente deve ser um método de instância.

---

# ⚠️ Erros comuns

### Tentar usar `this` em método `static`

```java
public static void exibir() {
    System.out.println(this.valor); // não compila
}
```

### Acessar atributo de instância diretamente em método `static`

```java
private double valor;

public static void exibirValor() {
    System.out.println(valor); // não compila
}
```

### Chamar método de instância pelo nome da classe

```java
Produto.exibirResumo(); // não compila
```

É necessário ter um objeto:

```java
Produto arroz = new Produto("Arroz", 2.5);
arroz.exibirResumo();
```

### Usar `static` em um dado que deveria ser independente

```java
private static double valor;
```

Nesse caso, todos os produtos compartilhariam o mesmo preço, o que não representa corretamente o domínio.

### Esquecer que `static` é compartilhado

Uma alteração em um atributo `static` pode ser observada por todas as instâncias e pela própria classe.

---

# ✅ REVISÃO DO MÓDULO 12

Ao concluir este módulo, você deve conseguir:

- Diferenciar membros de instância e membros `static`.
- Explicar que atributos de instância pertencem a objetos específicos.
- Explicar que atributos `static` pertencem à classe.
- Usar `this` para representar o objeto atual.
- Entender por que `this` não pode ser usado em métodos `static`.
- Criar e chamar métodos de instância por meio de objetos.
- Criar e chamar métodos `static` por meio do nome da classe.
- Identificar quando um método depende do estado de um objeto.
- Identificar quando uma informação deve ser compartilhada pela classe.
- Usar `static final` para constantes da classe.
- Compreender que dois produtos podem ter valores diferentes, enquanto um contador `static` pode ser compartilhado.
