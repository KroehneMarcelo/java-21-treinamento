---
marp: true
theme: default
paginate: true
---

# JAVA 21
## Módulo 11 — Instâncias, Encapsulamento, Getters e Setters

**Metodologia:** Relembrando → Desafio 1 → Solução 1 → Explicação do Desafio 1 → Desafio Extra → Solução do Desafio Extra → Explicação do Desafio Extra → Desafio Final → Solução do Desafio Final → Explicação do Desafio Final

---

# 🧠 RELEMBRANDO — Classe e objeto

No módulo anterior, conhecemos a classe `Produto`.

```java
public class Produto {
    String nome;
    double valor;
}
```

A classe funciona como um **modelo**. Ela descreve quais atributos e comportamentos um produto pode possuir.

Para utilizar esse modelo, precisamos criar um objeto:

```java
Produto arroz = new Produto();
```

Esse processo é chamado de **instanciação**.

- `Produto` é a classe e o tipo da variável.
- `arroz` é a variável que guarda a referência para o objeto.
- `new Produto()` cria uma nova instância de `Produto`.

---

# 🧠 O que acontece com `new Produto()`?

Quando usamos `new`, o Java cria um novo objeto na memória.

```java
Produto arroz = new Produto();
Produto feijao = new Produto();
```

Foram criadas **duas instâncias diferentes**.

Cada objeto possui seu próprio conjunto de atributos:

```text
arroz  ──► Produto { nome: ?, valor: ? }
feijao ──► Produto { nome: ?, valor: ? }
```

Alterar o valor do arroz não altera o valor do feijão, porque eles representam objetos diferentes.

> Neste módulo, memória será entendida de forma introdutória: cada uso de `new Produto()` cria um novo objeto, com espaço próprio para guardar seus atributos.

---

# 🧠 Valores iniciais dos atributos

Quando um objeto é criado, seus atributos recebem valores iniciais padrão caso nenhum valor seja informado.

| Tipo do atributo | Valor inicial padrão |
|---|---|
| `String` e outras referências | `null` |
| `int` | `0` |
| `double` | `0.0` |
| `boolean` | `false` |

```java
public class Produto {
    public String nome;
    public double valor;
    public int quantidade;
    public boolean ativo;
}
```

```java
Produto produto = new Produto();

System.out.println(produto.nome);       // null
System.out.println(produto.valor);      // 0.0
System.out.println(produto.quantidade); // 0
System.out.println(produto.ativo);      // false
```

Esses valores pertencem aos **atributos do objeto**. Variáveis locais continuam precisando ser inicializadas antes do uso.

---

# 🎯 DESAFIO 1 — Duas instâncias, dois estados

### Contexto

Um mercado precisa cadastrar arroz e feijão. Os dois são produtos, mas possuem nomes e valores diferentes.

### Regras

1. Crie uma classe chamada `Produto`.
2. Declare os atributos públicos `nome` e `valor`.
3. No `main`, crie o objeto `arroz` usando `new Produto()`.
4. Preencha o nome e o valor do arroz.
5. Crie outro objeto chamado `feijao` usando um novo `new Produto()`.
6. Preencha o nome e o valor do feijão.
7. Exiba os atributos dos dois produtos.
8. Altere somente o valor do arroz e exiba novamente os dois valores.

### Dados de teste

- Arroz: valor inicial `2.5`.
- Feijão: valor inicial `4.0`.
- Novo valor do arroz: `3.0`.

### O que o aluno precisa observar

Mesmo que os objetos tenham sido criados a partir da mesma classe, cada instância mantém seus próprios valores.

---

# 💡 SOLUÇÃO 1

```java
public class Produto {
    public String nome;
    public double valor;
}
```

```java
public class Main {
    public static void main(String[] args) {
        Produto arroz = new Produto();
        arroz.nome = "Arroz";
        arroz.valor = 2.5;

        Produto feijao = new Produto();
        feijao.nome = "Feijão";
        feijao.valor = 4.0;

        System.out.println(arroz.nome + ": R$ " + arroz.valor);
        System.out.println(feijao.nome + ": R$ " + feijao.valor);

        arroz.valor = 3.0;

        System.out.println("Novo valor do arroz: R$ " + arroz.valor);
        System.out.println("Valor do feijão: R$ " + feijao.valor);
    }
}
```

---

# 🔍 EXPLICAÇÃO DO DESAFIO 1

Cada execução de `new Produto()` criou um objeto diferente:

```java
Produto arroz = new Produto();
Produto feijao = new Produto();
```

Podemos representar a situação assim:

```text
arroz  ──► Produto { nome: "Arroz",  valor: 2.5 }
feijao ──► Produto { nome: "Feijão", valor: 4.0 }
```

Depois desta alteração:

```java
arroz.valor = 3.0;
```

A memória pode ser imaginada assim:

```text
arroz  ──► Produto { nome: "Arroz",  valor: 3.0 }
feijao ──► Produto { nome: "Feijão", valor: 4.0 }
```

Somente o objeto referenciado pela variável `arroz` foi alterado.

### Pontos de atenção

- A classe define quais atributos existem.
- Cada `new Produto()` cria uma nova instância.
- Cada instância possui seu próprio estado.
- A variável não contém todos os dados do objeto; ela permite chegar ao objeto por meio de uma referência.

---

# 🧠 Atributos públicos

Um atributo `public` pode ser acessado e alterado diretamente por outra classe:

```java
public class Produto {
    public double valor;
}
```

```java
Produto produto = new Produto();
produto.valor = 10.0;
produto.valor = -500.0;
```

O acesso é simples, mas qualquer valor pode ser atribuído, até mesmo um valor inválido.

### Vantagem inicial

- Facilita visualizar o acesso direto aos atributos.

### Problema

- A classe perde o controle sobre as alterações realizadas em seu estado.
- As regras de validação podem ficar espalhadas pelo programa.

> Atributos públicos ajudam no primeiro contato, mas normalmente evitamos expor diretamente dados que precisam de controle.

---

# 🧠 Atributos privados

Um atributo `private` só pode ser acessado diretamente dentro da própria classe.

```java
public class Produto {
    private double valor;
}
```

O código abaixo não compila:

```java
Produto produto = new Produto();
produto.valor = 10.0;
```

A classe `Main` não pode acessar diretamente o atributo privado `valor`.

Para permitir operações controladas, podemos criar métodos públicos:

```java
public void setValor(double valor) {
    this.valor = valor;
}

public double getValor() {
    return valor;
}
```

---

# 🧠 Getter e setter

Um **getter** devolve o valor de um atributo.

```java
public double getValor() {
    return valor;
}
```

Um **setter** recebe um valor e pode atualizar o atributo.

```java
public void setValor(double valor) {
    this.valor = valor;
}
```

### Convenção de nomes

| Operação | Método |
|---|---|
| Consultar `nome` | `getNome()` |
| Alterar `nome` | `setNome(String nome)` |
| Consultar `valor` | `getValor()` |
| Alterar `valor` | `setValor(double valor)` |
| Consultar booleano `ativo` | `isAtivo()` |
| Alterar booleano `ativo` | `setAtivo(boolean ativo)` |

`this.valor` representa o atributo do objeto atual. `valor` representa o parâmetro recebido pelo setter.

---

# 🧠 Setter com validação

Um setter não precisa aceitar qualquer valor.

```java
public void setValor(double valor) {
    if (valor >= 0) {
        this.valor = valor;
    }
}
```

Agora a regra pertence à classe `Produto`.

```java
Produto produto = new Produto();
produto.setValor(10.0);  // alteração aceita
produto.setValor(-5.0);  // alteração ignorada
```

O atributo continua protegido:

```java
private double valor;
```

> Encapsular é proteger o estado do objeto e oferecer operações controladas para consultá-lo ou modificá-lo.

---

# 🎯 DESAFIO EXTRA — Encapsulando o produto

### Contexto

Os atributos públicos permitiram entender o acesso direto. Agora a classe deverá proteger seus dados usando `private`, getters e setters.

### Regras

1. Altere os atributos `nome`, `valor`, `quantidade` e `ativo` para `private`.
2. Crie getters para todos os atributos.
3. Crie setters para todos os atributos.
4. `setNome` deve aceitar apenas textos diferentes de `null` e que não estejam vazios.
5. `setValor` deve aceitar somente valores maiores ou iguais a zero.
6. `setQuantidade` deve aceitar somente quantidades maiores ou iguais a zero.
7. Para o atributo booleano, use `isAtivo()` como getter.
8. Crie duas instâncias e atribua valores diferentes usando os setters.
9. Exiba os valores usando os getters.

### Dados de teste

- Arroz: valor `2.5`, quantidade `10`, ativo.
- Feijão: valor `4.0`, quantidade `5`, ativo.
- Tente definir o valor do arroz como `-2.0`.

### O que o aluno precisa fazer

Substituir o acesso direto por métodos públicos que controlem o acesso aos atributos privados.

---

# 💡 SOLUÇÃO DO DESAFIO EXTRA

```java
public class Produto {
    private String nome;
    private double valor;
    private int quantidade;
    private boolean ativo;

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
        if (valor >= 0) {
            this.valor = valor;
        }
    }

    public int getQuantidade() {
        return quantidade;
    }

    public void setQuantidade(int quantidade) {
        if (quantidade >= 0) {
            this.quantidade = quantidade;
        }
    }

    public boolean isAtivo() {
        return ativo;
    }

    public void setAtivo(boolean ativo) {
        this.ativo = ativo;
    }
}
```

```java
public class Main {
    public static void main(String[] args) {
        Produto arroz = new Produto();
        arroz.setNome("Arroz");
        arroz.setValor(2.5);
        arroz.setQuantidade(10);
        arroz.setAtivo(true);

        Produto feijao = new Produto();
        feijao.setNome("Feijão");
        feijao.setValor(4.0);
        feijao.setQuantidade(5);
        feijao.setAtivo(true);

        arroz.setValor(-2.0);

        System.out.println(arroz.getNome() + ": R$ " + arroz.getValor());
        System.out.println(feijao.getNome() + ": R$ " + feijao.getValor());
    }
}
```

---

# 🔍 EXPLICAÇÃO DO DESAFIO EXTRA

Os atributos não podem mais ser acessados diretamente pelo `main`:

```java
private double valor;
```

O acesso acontece por meio dos métodos públicos:

```java
arroz.setValor(2.5);
System.out.println(arroz.getValor());
```

### Fluxo do setter

```java
arroz.setValor(-2.0);
```

1. O método `setValor` recebe `-2.0`.
2. A condição `valor >= 0` é falsa.
3. O atributo não é alterado.
4. O valor do arroz continua sendo `2.5`.

### Encapsulamento

```text
Classe Main
    │
    ├── setValor(...) ──► altera de forma controlada
    │
    └── getValor()    ◄── consulta o valor

Produto
    └── private double valor
```

### Pontos de atenção

- `private` impede acesso direto externo.
- `public` permite chamar os getters e setters.
- O setter pode validar antes de alterar.
- O getter devolve o valor atual do objeto.
- Nem todo atributo precisa obrigatoriamente de getter e setter; eles devem existir quando fizerem sentido para o modelo.

---

# 🧠 Referências para o mesmo objeto

Duas variáveis também podem apontar para o **mesmo objeto**.

```java
Produto arroz = new Produto();
arroz.setValor(2.5);

Produto produtoEmPromocao = arroz;
produtoEmPromocao.setValor(2.0);
```

Não houve um segundo `new Produto()`.

```text
arroz             ──┐
                    ├──► Produto { valor: 2.0 }
produtoEmPromocao ──┘
```

Por isso, as duas variáveis consultam o mesmo valor:

```java
System.out.println(arroz.getValor());             // 2.0
System.out.println(produtoEmPromocao.getValor()); // 2.0
```

> Uma nova variável não cria automaticamente um novo objeto. Um novo objeto é criado quando usamos `new`.

---

# 🧠 Comparando as duas situações

### Dois objetos diferentes

```java
Produto arroz = new Produto();
Produto feijao = new Produto();
```

```text
arroz  ──► Produto A
feijao ──► Produto B
```

Cada objeto possui seu próprio estado.

### Duas referências para o mesmo objeto

```java
Produto arroz = new Produto();
Produto produtoEmPromocao = arroz;
```

```text
arroz             ──┐
                    ├──► Produto A
produtoEmPromocao ──┘
```

Uma alteração feita por uma referência pode ser observada pela outra.

---

# 🎯 DESAFIO FINAL — Instâncias e referências

### Contexto

Um mercado quer cadastrar arroz e feijão e também criar uma referência para o produto que está em promoção.

### Regras

1. Use a classe `Produto` com atributos privados, getters e setters.
2. Crie uma instância para o arroz.
3. Crie uma instância diferente para o feijão.
4. Defina valores diferentes para os dois produtos.
5. Crie a variável `produtoEmPromocao` e faça ela receber a referência de `arroz`.
6. Altere o valor usando `produtoEmPromocao.setValor(2.0)`.
7. Exiba o valor do arroz, do feijão e do produto em promoção.
8. Explique por que arroz e produto em promoção exibem o mesmo valor.
9. Tente aplicar um valor negativo e confirme que o setter protege o objeto.

### Dados de teste

- Arroz: `2.5`.
- Feijão: `4.0`.
- Arroz em promoção: `2.0`.
- Valor inválido: `-10.0`.

### O que o aluno precisa observar

`arroz` e `feijao` apontam para objetos diferentes. `arroz` e `produtoEmPromocao` apontam para o mesmo objeto.

---

# 💡 SOLUÇÃO DO DESAFIO FINAL

```java
public class Produto {
    private String nome;
    private double valor;

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
        if (valor >= 0) {
            this.valor = valor;
        }
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

        Produto produtoEmPromocao = arroz;
        produtoEmPromocao.setValor(2.0);

        System.out.println("Arroz: R$ " + arroz.getValor());
        System.out.println("Feijão: R$ " + feijao.getValor());
        System.out.println("Promoção: R$ " + produtoEmPromocao.getValor());

        produtoEmPromocao.setValor(-10.0);

        System.out.println("Após valor inválido: R$ " + arroz.getValor());
    }
}
```

---

# 🔍 EXPLICAÇÃO DO DESAFIO FINAL

No início, dois objetos foram criados:

```java
Produto arroz = new Produto();
Produto feijao = new Produto();
```

A memória pode ser entendida assim:

```text
arroz  ──► Produto A { nome: "Arroz",  valor: 2.5 }
feijao ──► Produto B { nome: "Feijão", valor: 4.0 }
```

Depois, outra variável recebeu a referência do arroz:

```java
Produto produtoEmPromocao = arroz;
```

Nenhum novo objeto foi criado nessa linha:

```text
arroz             ──┐
                    ├──► Produto A { nome: "Arroz", valor: 2.0 }
produtoEmPromocao ──┘

feijao ───────────────► Produto B { nome: "Feijão", valor: 4.0 }
```

Quando `produtoEmPromocao` altera o valor, o objeto apontado por `arroz` também apresenta a mudança, pois as duas variáveis chegam ao mesmo objeto.

### Saída esperada

```text
Arroz: R$ 2.0
Feijão: R$ 4.0
Promoção: R$ 2.0
Após valor inválido: R$ 2.0
```

### Pontos de atenção

- `new Produto()` cria um novo objeto.
- Duas chamadas de `new Produto()` criam dois objetos diferentes.
- Atribuir uma referência a outra variável não cria um novo objeto.
- Cada objeto possui seu próprio conjunto de atributos.
- Duas referências podem apontar para o mesmo objeto.
- Getters permitem consultar atributos privados.
- Setters permitem controlar mudanças nos atributos privados.

### Erros comuns

- Achar que `Produto copia = original;` cria uma cópia independente.
- Tentar acessar diretamente um atributo `private`.
- Criar setters sem considerar as regras do atributo.
- Confundir o nome da variável com o objeto armazenado na memória.
- Imaginar que alterar o arroz também altera o feijão, mesmo eles tendo sido criados com dois usos diferentes de `new`.

---

# ✅ REVISÃO DO MÓDULO 11

Ao concluir este módulo, você deve conseguir:

- Instanciar objetos com `new Produto()`.
- Identificar classe, variável de referência e objeto.
- Entender que cada `new` cria uma nova instância.
- Entender que instâncias diferentes podem possuir valores diferentes.
- Acessar e alterar atributos públicos diretamente.
- Reconhecer os riscos de expor atributos públicos.
- Proteger atributos usando `private`.
- Criar getters para consultar valores.
- Criar setters para realizar alterações controladas.
- Usar `this` para diferenciar atributo e parâmetro.
- Compreender, de forma introdutória, que objetos ocupam espaços distintos na memória.
- Reconhecer quando duas variáveis apontam para objetos diferentes ou para o mesmo objeto.
