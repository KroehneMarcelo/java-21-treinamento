---
marp: true
theme: default
paginate: true
---

# JAVA 21
## Módulo 13 — Lista de Produtos com `List<Produto>`

**Metodologia:** Relembrando → Desafio 1 → Solução 1 → Explicação do Desafio 1 → Desafio Extra → Solução do Desafio Extra → Explicação do Desafio Extra → Desafio Final → Solução do Desafio Final → Explicação do Desafio Final

---

# 🧠 RELEMBRANDO — Objeto `Produto`

Nos módulos anteriores, criamos objetos a partir da classe `Produto`:

```java
Produto arroz = new Produto("Arroz", 2.5);
Produto feijao = new Produto("Feijão", 4.0);
```

Agora vamos trabalhar com vários produtos ao mesmo tempo usando uma lista.

A estrutura principal deste módulo será:

```java
List<Produto> produtos = new ArrayList<>();
```

> Neste módulo, a lista ficará no fluxo principal (`main`).
>
> Vamos deixar o tema "lista dentro de uma classe" para o módulo 15.

---

# 🧠 O que é `List<Produto>`?

`List<Produto>` significa:

- uma lista que aceita apenas objetos do tipo `Produto`.
- podemos adicionar, remover, percorrer e consultar itens dessa lista.

Exemplo:

```java
List<Produto> produtos = new ArrayList<>();

produtos.add(new Produto("Arroz", 2.5));
produtos.add(new Produto("Feijão", 4.0));
```

Cada posição da lista guarda um objeto `Produto`.

---

# 🧠 Classe base para este módulo

```java
public class Produto {
    private String nome;
    private double valor;

    public Produto(String nome, double valor) {
        this.nome = nome;
        this.valor = valor;
    }

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
        if (valor >= 0) {
            this.valor = valor;
        }
    }
}
```

Com isso, conseguimos criar objetos e trabalhar com uma lista de produtos.

---

# 🎯 DESAFIO 1 — Criando a lista de produtos

### Contexto

Uma mercearia precisa montar uma lista de produtos no programa.

### Regras

1. Crie a classe `Produto` com `nome` e `valor`.
2. No `main`, crie `List<Produto> produtos = new ArrayList<>();`.
3. Adicione pelo menos 3 produtos à lista.
4. Percorra a lista com `for-each`.
5. Exiba nome e valor de cada produto.
6. Exiba a quantidade total de itens com `size()`.

### Dados de teste

- Arroz: `2.5`
- Feijão: `4.0`
- Leite: `3.2`

---

# 💡 SOLUÇÃO 1

```java
import java.util.ArrayList;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        List<Produto> produtos = new ArrayList<>();

        produtos.add(new Produto("Arroz", 2.5));
        produtos.add(new Produto("Feijão", 4.0));
        produtos.add(new Produto("Leite", 3.2));

        for (Produto produto : produtos) {
            System.out.println(produto.getNome() + " - R$ " + produto.getValor());
        }

        System.out.println("Quantidade de produtos: " + produtos.size());
    }
}
```

---

# 🔍 EXPLICAÇÃO DO DESAFIO 1

A linha principal deste módulo é:

```java
List<Produto> produtos = new ArrayList<>();
```

- `List<Produto>` define o tipo da coleção.
- `new ArrayList<>()` cria a lista.

Ao adicionar itens:

```java
produtos.add(new Produto("Arroz", 2.5));
```

cada elemento é um objeto `Produto` completo.

O `for-each` percorre todos os itens:

```java
for (Produto produto : produtos) {
    ...
}
```

`size()` retorna quantos elementos existem na lista.

---

# 🧠 Operações básicas com `List<Produto>`

### Adicionar

```java
produtos.add(new Produto("Café", 8.0));
```

### Acessar por índice

```java
Produto primeiro = produtos.get(0);
```

### Remover por índice

```java
produtos.remove(1);
```

### Tamanho

```java
int quantidade = produtos.size();
```

### Verificar se está vazia

```java
if (produtos.isEmpty()) {
    System.out.println("Lista vazia");
}
```

---

# 🎯 DESAFIO EXTRA — Buscar e remover por nome

### Contexto

Agora a mercearia precisa buscar e remover produtos da lista pelo nome.

### Regras

1. Crie um método `buscarPorNome(List<Produto> produtos, String nome)`.
2. Esse método deve retornar o objeto `Produto` encontrado ou `null`.
3. Crie um método `removerPorNome(List<Produto> produtos, String nome)`.
4. Esse método deve remover o primeiro produto com o nome informado.
5. Exiba a lista antes e depois da remoção.

### Dados de teste

- Buscar: "Feijão"
- Remover: "Arroz"

---

# 💡 SOLUÇÃO DO DESAFIO EXTRA

```java
import java.util.ArrayList;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        List<Produto> produtos = new ArrayList<>();
        produtos.add(new Produto("Arroz", 2.5));
        produtos.add(new Produto("Feijão", 4.0));
        produtos.add(new Produto("Leite", 3.2));

        Produto encontrado = buscarPorNome(produtos, "Feijão");
        if (encontrado != null) {
            System.out.println("Encontrado: " + encontrado.getNome() + " - R$ " + encontrado.getValor());
        }

        System.out.println("Antes de remover:");
        listar(produtos);

        removerPorNome(produtos, "Arroz");

        System.out.println("Depois de remover:");
        listar(produtos);
    }

    public static Produto buscarPorNome(List<Produto> produtos, String nome) {
        for (Produto produto : produtos) {
            if (produto.getNome().equalsIgnoreCase(nome)) {
                return produto;
            }
        }
        return null;
    }

    public static void removerPorNome(List<Produto> produtos, String nome) {
        for (int i = 0; i < produtos.size(); i++) {
            if (produtos.get(i).getNome().equalsIgnoreCase(nome)) {
                produtos.remove(i);
                return;
            }
        }
    }

    public static void listar(List<Produto> produtos) {
        for (Produto produto : produtos) {
            System.out.println(produto.getNome() + " - R$ " + produto.getValor());
        }
    }
}
```

---

# 🔍 EXPLICAÇÃO DO DESAFIO EXTRA

Para buscar por nome, percorremos a lista e comparamos o nome de cada item:

```java
if (produto.getNome().equalsIgnoreCase(nome))
```

Para remover por nome, usamos `for` com índice:

```java
produtos.remove(i);
```

Assim removemos o item encontrado e encerramos com `return`.

### Pontos de atenção

- `buscarPorNome` retorna `null` quando não encontra.
- `equalsIgnoreCase` facilita comparação de texto.
- Remoção durante iteração é mais segura com laço por índice.

---

# 🧠 Somando valores da lista

Um uso comum de `List<Produto>` é calcular o total:

```java
public static double calcularTotal(List<Produto> produtos) {
    double total = 0.0;

    for (Produto produto : produtos) {
        total += produto.getValor();
    }

    return total;
}
```

Com a lista:

- Arroz `2.5`
- Feijão `4.0`
- Leite `3.2`

Total esperado: `9.7`.

---

# 🎯 DESAFIO FINAL — Lista completa de produtos

### Contexto

A mercearia quer um fluxo completo no `main` usando `List<Produto>`:

- adicionar,
- listar,
- buscar,
- remover,
- calcular total.

### Regras

1. Use `List<Produto> produtos = new ArrayList<>();`.
2. Adicione 4 produtos.
3. Liste todos com nome e valor.
4. Exiba a quantidade de itens.
5. Busque um produto por nome.
6. Remova um produto por nome.
7. Liste novamente.
8. Exiba o total final da lista.
9. Se a lista estiver vazia, exiba mensagem adequada.

### Dados de teste

- Arroz `2.5`
- Feijão `4.0`
- Leite `3.2`
- Café `8.0`

---

# 💡 SOLUÇÃO DO DESAFIO FINAL

```java
import java.util.ArrayList;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        List<Produto> produtos = new ArrayList<>();

        produtos.add(new Produto("Arroz", 2.5));
        produtos.add(new Produto("Feijão", 4.0));
        produtos.add(new Produto("Leite", 3.2));
        produtos.add(new Produto("Café", 8.0));

        System.out.println("Lista inicial:");
        listar(produtos);

        System.out.println("Quantidade: " + produtos.size());

        Produto encontrado = buscarPorNome(produtos, "Leite");
        if (encontrado != null) {
            System.out.println("Busca: " + encontrado.getNome() + " - R$ " + encontrado.getValor());
        }

        removerPorNome(produtos, "Feijão");

        System.out.println("Lista após remover Feijão:");
        listar(produtos);

        if (produtos.isEmpty()) {
            System.out.println("Lista vazia");
        } else {
            System.out.println("Total final: R$ " + calcularTotal(produtos));
        }
    }

    public static void listar(List<Produto> produtos) {
        for (Produto produto : produtos) {
            System.out.println(produto.getNome() + " - R$ " + produto.getValor());
        }
    }

    public static Produto buscarPorNome(List<Produto> produtos, String nome) {
        for (Produto produto : produtos) {
            if (produto.getNome().equalsIgnoreCase(nome)) {
                return produto;
            }
        }
        return null;
    }

    public static void removerPorNome(List<Produto> produtos, String nome) {
        for (int i = 0; i < produtos.size(); i++) {
            if (produtos.get(i).getNome().equalsIgnoreCase(nome)) {
                produtos.remove(i);
                return;
            }
        }
    }

    public static double calcularTotal(List<Produto> produtos) {
        double total = 0.0;
        for (Produto produto : produtos) {
            total += produto.getValor();
        }
        return total;
    }
}
```

---

# 🔍 EXPLICAÇÃO DO DESAFIO FINAL

Este fluxo mostra o uso completo de uma lista de objetos:

```java
List<Produto> produtos = new ArrayList<>();
```

A lista foi manipulada no `main` e passada para métodos auxiliares.

### O que isso ensina

- coleção tipada com objetos;
- operações básicas de lista;
- busca e remoção por critério;
- agregação de valores (total);
- verificação de lista vazia.

### Saída esperada (resumo)

- lista inicial com 4 itens;
- busca do leite com sucesso;
- remoção do feijão;
- total recalculado com os itens restantes.

---

# ⚠️ Erros comuns

- Esquecer imports:

```java
import java.util.List;
import java.util.ArrayList;
```

- Declarar `List<Produto>` mas não inicializar com `new ArrayList<>()`.
- Tentar acessar índice inválido com `get`.
- Comparar nomes com `==` em vez de `equals`/`equalsIgnoreCase`.
- Remover item dentro de `for-each`.

---

# ✅ REVISÃO DO MÓDULO 13

Ao concluir este módulo, você deve conseguir:

- Criar `List<Produto>`.
- Adicionar objetos com `add`.
- Percorrer itens com `for-each`.
- Buscar por nome em uma lista de objetos.
- Remover item por critério.
- Calcular total com base nos valores dos produtos.
- Verificar quantidade (`size`) e lista vazia (`isEmpty`).
- Organizar métodos auxiliares recebendo `List<Produto>` como parâmetro.

---

# 🧠 CONCLUSÃO

Neste módulo, a ideia central foi dominar:

```java
List<Produto> produtos
```

com a lista sendo usada diretamente no fluxo principal.

No **módulo 15**, avançaremos para o próximo passo: lista como atributo dentro de classe (ex.: `Carrinho` com `List<Produto>`).
