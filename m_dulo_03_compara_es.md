---
marp: true
theme: default
paginate: true
---

# JAVA 21
## Módulo 03 — Comparações em Java

**Metodologia:** Desafio → Solução → Explicação → Evolução

---

# 🎯 Parte 1 — Comparando Tipos Primitivos

Para tipos primitivos (`int`, `double`, `boolean`, `char`), o operador `==` compara os **valores** diretamente:

```java
int codigo1 = 10;
int codigo2 = 10;

if (codigo1 == codigo2) {
    System.out.println("Códigos iguais");
}
```

---

# 🎯 Parte 2 — Desafio: Comparando Strings

### Problema
Verificar se o nome de um cliente digitado é `"João"`.

### ⚠️ O erro comum
```java
String nome = "João";

if (nome == "João") { // CUIDADO!
    System.out.println("Nome encontrado");
}
```

**Atenção:** Em Java, o operador `==` em objetos compara **referências de memória**, e não o conteúdo do texto!

---

# 💡 Solução: Utilizando `equals()`

Para comparar o **conteúdo textual** de duas Strings, utilize o método `.equals()`:

```java
String nome = "João";

if (nome.equals("João")) {
    System.out.println("Nome encontrado");
}
```

`equals()` verifica se a sequência de caracteres é idêntica.

---

# 🛡️ Dica de Segurança: Null Safety

Se a variável `nome` estiver nula (`null`), chamar `nome.equals(...)` causa um erro grave (`NullPointerException`).

### Boa Prática:
```java
String nome = null;

// ❌ Riscos de erro (NullPointerException):
// if (nome.equals("João"))

// ✅ Seguro contra Null:
if ("João".equals(nome)) {
    System.out.println("Nome encontrado");
}
```

---

# 🎯 Parte 3 — Comparando com `contentEquals()`

E se precisarmos comparar uma `String` com outro tipo de sequência de texto (como um `StringBuilder`)?

```java
String nome = "João";
StringBuilder outro = new StringBuilder("João");

if (nome.contentEquals(outro)) {
    System.out.println("Conteúdo exatamente igual");
}
```

### Diferença:
- `equals()`: Exige que o objeto comparado seja uma `String` idêntica.
- `contentEquals()`: Compara a sequência de texto com qualquer `CharSequence` (`String`, `StringBuilder`, `StringBuffer`).

---

# 🎯 Parte 4 — Comparação para Ordenação: `compareTo()`

### Problema
Como saber qual nome vem primeiro na ordem alfabética?

```java
String nome1 = "Ana";
String nome2 = "Bruno";

int resultado = nome1.compareTo(nome2);

if (resultado < 0) {
    System.out.println(nome1 + " vem antes de " + nome2);
} else if (resultado == 0) {
    System.out.println("Nomes idênticos");
} else {
    System.out.println(nome1 + " vem depois de " + nome2);
}
```

---

# 🔍 Explicação: Retornos do `compareTo()`

O método `.compareTo()` retorna um **número inteiro**:

- **Número Negativo (`< 0`):** O primeiro texto vem **antes** do segundo na ordem lexicográfica.
- **Zero (`== 0`):** Os textos são **iguais**.
- **Número Positivo (`> 0`):** O primeiro texto vem **depois** do segundo na ordem lexicográfica.

---

# 📊 Tabela Comparativa

| Mecanismo | Finalidade Principal | Exemplo |
| :--- | :--- | :--- |
| `==` | Comparar **valores primitivos** ou **endereços de memória** | `a == b` |
| `equals()` | Verificar **igualdade de conteúdo** de objetos | `"A".equals(texto)` |
| `contentEquals()` | Comparar conteúdo textual com **CharSequence** | `texto.contentEquals(sb)` |
| `compareTo()` | Determinar **ordem alfabética / classificação** | `a.compareTo(b) < 0` |

---

# 🚀 Desafio Final Integrado

Crie um programa em Java que valide se uma tentativa de login é válida.

### Regras de Negócio:
1. O usuário deve estar **ativo** (`boolean`).
2. O perfil deve ser igual a `"ADMIN"` ou `"OPERADOR"`. Use `.equals()`.
3. O nome do usuário não pode ser igual a `"GUEST"`. Use `!`.
4. Escreva o código aplicando as regras de **Clean Code** aprendidas até aqui.
