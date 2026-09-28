# 🗺️ Roadmap de Aprendizado — Java 21

Este roadmap apresenta o caminho de evolução do desenvolvedor no treinamento, do básico até tópicos modernos do Java 21.

---

```
[Etapa 01: Fundamentos] ──► [Etapa 02: Condições] ──► [Etapa 03: Comparações]
                                                               │
[Etapa 06: OO Básica]   ◄── [Etapa 05: Métodos]   ◄── [Etapa 04: Estruturas]
       │
       ▼
[Etapa 07: Coleções]   ──► [Etapa 08: Java 21 Moderno]
```

---

### 📍 Etapa 01 — Fundamentos de Sintaxe e Tipos
- Variáveis e Tipagem Estática
- Tipos Primitivos (`int`, `double`, `boolean`) e `String`
- Modificadores de Acesso Práticos: `public` e `private`
- Imutabilidade básica com `final`

### 📍 Etapa 02 — Condições e Decisões
- Estrutura condicional: `if` e `else`
- Operadores Relacionais (`>`, `>=`, `<`, `<=`)
- Atribuição (`=`) versus Comparação (`==`)
- Operadores Lógicos: `&&` (AND), `||` (OR), `!` (NOT)
- Introdução ao *Clean Code* em condicionais

---

### 📍 Etapa 03 — Comparações de Dados
- Comparação de Primitivos com `==`
- Comparação de Conteúdo de Objetos com `equals()`
- Null Safety no uso de condicionais
- Comparação de sequências de texto com `contentEquals()`
- Ordenação e Classificação com `compareTo()`

### 📍 Etapa 04 — Próximos Fundamentos
- Operador Ternário (`condicao ? v1 : v2`)
- Estruturas de Seleção: `switch` (e *Switch Expressions*)
- Laços de Repetição: `for`, `while`, `do-while`
- Estruturas de Dados Básicas: Arrays unidimensionais

---

### 📍 Etapa 05 — Métodos e Modarização
- Declaração de Métodos
- Parâmetros e Argumentos
- Tipos de Retorno e palavra-chave `void`
- Escopo de Variáveis
- Sobrecarga de Métodos (*Overloading*)

### 📍 Etapa 06 — Orientação a Objetos (Essencial)
- Conceito de Classes, Objetos e Instâncias
- Construtores de Classe
- Encapsulamento completo (Getters e Setters)
- **Introdução ao `this`** *(somente aqui após entender instâncias!)*
- **Introdução ao `static`** *(membros da classe vs membros da instância)*

---

### 📍 Etapa 07 — Estruturas e Exceções
- Coleções: `List`, `Set`, `Map`
- Uso de `Generics` (`List<String>`)
- Tratamento de Erros: `try`, `catch`, `finally`
- Lançamento de Exceções personalizadas

### 📍 Etapa 08 — Java Moderno & Java 21
- Expressões Lambda
- Stream API para manipulação de dados
- Encoders e Utilitários: `Optional`
- Modelagem Imutável com **Records**
- Nova Date & Time API (`LocalDate`, `DateTimeFormatter`)
- Funcionalidades modernas do Java 21 (Pattern Matching, Virtual Threads - Introdução)