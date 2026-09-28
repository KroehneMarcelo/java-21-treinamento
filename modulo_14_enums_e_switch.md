---
marp: true
theme: default
paginate: true
---

# JAVA 21
## Módulo 14 — Enums e `switch`

**Metodologia:** Relembrando → Desafio 1 → Solução 1 → Explicação → Desafio Extra → Solução → Desafio Final → Solução Final → Revisão

---

# 🧠 RELEMBRANDO — Valores que representam opções

Até agora, muitas decisões foram feitas usando `String`:

```java
String categoria = "ALIMENTO";

switch (categoria) {
    case "ALIMENTO" -> System.out.println("Produto alimentício");
    case "LIMPEZA" -> System.out.println("Produto de limpeza");
    default -> System.out.println("Categoria desconhecida");
}
```

Esse código funciona, mas permite erros de digitação:

```java
String categoria = "ALIMNETO";
```

O programa não consegue impedir facilmente esse valor incorreto. Para representar um conjunto fechado de opções, podemos usar um `enum`.

---

# 🧠 O que é um `enum`?

`enum` define um conjunto fixo de constantes relacionadas.

```java
public enum Categoria {
    ALIMENTO,
    LIMPEZA,
    ELETRONICO
}
```

A variável passa a aceitar somente valores da enumeração:

```java
Categoria categoria = Categoria.ALIMENTO;
```

As constantes de um `enum` normalmente são escritas em letras maiúsculas.

### Vantagens

- Evita textos soltos espalhados pelo código.
- Reduz erros de digitação.
- Melhora a legibilidade.
- Permite usar `switch` com valores conhecidos.
- O compilador ajuda a verificar o tipo correto.

---

# 🎯 DESAFIO 1 — Primeiro `enum` com `switch`

Crie o enum `Categoria` com as opções `ALIMENTO`, `LIMPEZA` e `ELETRONICO`.

No `main`:

1. Crie uma variável `Categoria categoria`.
2. Atribua `Categoria.ALIMENTO`.
3. Use `switch` para exibir uma mensagem diferente para cada categoria.
4. Use `default` para tratar uma situação não prevista.

---

# 💡 SOLUÇÃO 1

```java
public enum Categoria {
    ALIMENTO,
    LIMPEZA,
    ELETRONICO
}
```

```java
public class Main {
    public static void main(String[] args) {
        Categoria categoria = Categoria.ALIMENTO;

        switch (categoria) {
            case ALIMENTO -> System.out.println("Produto alimentício");
            case LIMPEZA -> System.out.println("Produto de limpeza");
            case ELETRONICO -> System.out.println("Produto eletrônico");
            default -> System.out.println("Categoria desconhecida");
        }
    }
}
```

---

# 🔍 EXPLICAÇÃO

A atribuição usa o nome do enum e o nome da constante:

```java
Categoria categoria = Categoria.ALIMENTO;
```

No `switch`, não é necessário repetir `Categoria.ALIMENTO`; dentro dos `case`, usamos apenas `ALIMENTO`.

```java
switch (categoria) {
    case ALIMENTO -> ...;
}
```

O valor da variável só pode ser uma das constantes definidas em `Categoria`.

---

# 🧠 `enum` é um tipo

Assim como `String`, `int` e `boolean`, um enum é um tipo:

```java
Categoria categoria;
```

A diferença é que o conjunto de valores permitidos é definido pelo próprio programa.

```java
categoria = Categoria.LIMPEZA;
// categoria = "LIMPEZA"; // não é a mesma coisa
```

`Categoria.LIMPEZA` é uma constante do tipo `Categoria`; `"LIMPEZA"` é uma `String`.

---

# 🎯 DESAFIO EXTRA — Método que retorna uma mensagem

Crie o método:

```java
public static String descreverCategoria(Categoria categoria)
```

Regras:

- `ALIMENTO` retorna `"Pode ser armazenado na seção de alimentos"`.
- `LIMPEZA` retorna `"Pode ser armazenado na seção de limpeza"`.
- `ELETRONICO` retorna `"Pode ser armazenado na seção de eletrônicos"`.
- Use `switch` expression.

---

# 💡 SOLUÇÃO DO DESAFIO EXTRA

```java
public static String descreverCategoria(Categoria categoria) {
    return switch (categoria) {
        case ALIMENTO -> "Pode ser armazenado na seção de alimentos";
        case LIMPEZA -> "Pode ser armazenado na seção de limpeza";
        case ELETRONICO -> "Pode ser armazenado na seção de eletrônicos";
    };
}
```

Uma `switch expression` produz um valor, que pode ser retornado diretamente.

---

# 🧠 `switch` statement x `switch` expression

### Statement

```java
switch (categoria) {
    case ALIMENTO -> System.out.println("Alimento");
    case LIMPEZA -> System.out.println("Limpeza");
}
```

Executa uma ação.

### Expression

```java
String mensagem = switch (categoria) {
    case ALIMENTO -> "Alimento";
    case LIMPEZA -> "Limpeza";
    case ELETRONICO -> "Eletrônico";
};
```

Produz um valor.

---

# 🎯 DESAFIO FINAL — Status de pedido

Crie o enum:

```java
public enum StatusPedido {
    ABERTO,
    PAGO,
    ENVIADO,
    ENTREGUE,
    CANCELADO
}
```

Crie um método que use `switch` para retornar uma mensagem para cada status. No `main`, teste pelo menos três estados diferentes.

---

# 💡 SOLUÇÃO DO DESAFIO FINAL

```java
public enum StatusPedido {
    ABERTO,
    PAGO,
    ENVIADO,
    ENTREGUE,
    CANCELADO
}
```

```java
public static String descreverStatus(StatusPedido status) {
    return switch (status) {
        case ABERTO -> "Pedido aguardando pagamento";
        case PAGO -> "Pagamento confirmado";
        case ENVIADO -> "Pedido enviado";
        case ENTREGUE -> "Pedido entregue";
        case CANCELADO -> "Pedido cancelado";
    };
}
```

```java
public class Main {
    public static void main(String[] args) {
        System.out.println(descreverStatus(StatusPedido.ABERTO));
        System.out.println(descreverStatus(StatusPedido.PAGO));
        System.out.println(descreverStatus(StatusPedido.ENVIADO));
    }
}
```

---

# ✅ REVISÃO DO MÓDULO 14

Ao concluir este módulo, você deve conseguir:

- Declarar um `enum`.
- Usar constantes de enumeração.
- Declarar variáveis de um tipo enum.
- Usar enums em `switch`.
- Diferenciar `String` de valores de enum.
- Usar `switch` statement e `switch` expression.
- Representar estados e categorias com valores controlados.
