---
marp: true
theme: default
paginate: true
---

# JAVA 21
## Módulo 08 — Introdução aos Métodos

**Metodologia:** Relembrando → Desafio 1 → Solução 1 → Explicação do Desafio 1 → Desafio Extra → Solução do Desafio Extra → Explicação do Desafio Extra → Desafio Final → Solução do Desafio Final → Explicação do Desafio Final

---

# 🧠 RELEMBRANDO — O que já usamos até aqui

Antes de criar nossos próprios métodos, vamos relembrar algumas coisas que já apareceram nos módulos anteriores.

### Você já usa métodos desde o Módulo 01!
```java
public static void main(String[] args) {
    System.out.println("Olá");
}
```

- `main` **é um método**: é o ponto de partida do programa.
- `println(...)` **é um método**: ele recebe um texto e exibe no console.
- `equals(...)`, `compareTo(...)`, `add(...)` e `size()` também são métodos.

### Relembrando tipos
| Tipo | Exemplo de valor |
|------|------------------|
| `String` | `"Java"` |
| `int` | `10` |
| `double` | `7.5` |
| `boolean` | `true` |

Esses mesmos tipos vão aparecer agora como **tipo de retorno** dos nossos métodos.

---

# 🧠 RELEMBRANDO — O que é um método?

Um método é um **bloco de código com nome**, que pode ser executado sempre que precisarmos.

### Por que usar métodos?
- Evitar repetir o mesmo código em vários lugares.
- Dar um nome claro para uma tarefa (ex.: `exibirBoasVindas`).
- Deixar o `main` mais curto e fácil de ler.

### Anatomia de um método
```java
public static void exibirMensagem() {
    System.out.println("Mensagem");
}
```

| Parte | Significado |
|-------|-------------|
| `public` | Pode ser acessado de outros lugares (visto no Módulo 01) |
| `static` | Permite chamar o método direto do `main` *(será explicado no módulo de Orientação a Objetos)* |
| `void` | Tipo de retorno — `void` significa **não retorna nada** |
| `exibirMensagem` | Nome do método (verbo + complemento, em *camelCase*) |
| `()` | Parâmetros (valores de entrada) |
| `{ }` | Corpo do método |

---

# 🎯 DESAFIO 1 — Meu Primeiro Método `void`

### Contexto
Um sistema precisa exibir uma mensagem de boas-vindas sempre que for iniciado.

### Regras
1. Crie um método chamado `exibirBoasVindas`.
2. O método deve ser `void`, ou seja, não deve retornar nenhum valor.
3. O método deve exibir `"Bem-vindo ao sistema!"` e `"Treinamento Java 21"`.
4. O `main` deve **chamar** o método.
5. Chame o método duas vezes para ver a mensagem se repetir.

### Dados de teste
- Nenhum dado de entrada.

### O que o aluno precisa fazer
Criar um método `void` fora do `main` e executá-lo a partir do `main`.

---

# 💡 SOLUÇÃO 1

```java
public class Main {
    public static void main(String[] args) {
        exibirBoasVindas();
        exibirBoasVindas();
    }

    public static void exibirBoasVindas() {
        System.out.println("Bem-vindo ao sistema!");
        System.out.println("Treinamento Java 21");
    }
}
```

---

# 🔍 EXPLICAÇÃO DO DESAFIO 1

Um método `void` **executa uma ação**, mas **não devolve nenhum valor** para quem o chamou.

### O que acontece na solução?
1. O programa começa pelo `main`.
2. Ao encontrar `exibirBoasVindas();`, o Java "pula" para dentro do método.
3. As duas linhas são exibidas.
4. Ao terminar o método, o Java **volta** para o `main`, na linha seguinte.
5. A segunda chamada repete o processo.

### Declarar x Chamar
```java
public static void exibirBoasVindas() { ... } // declaração: ensina o que fazer
exibirBoasVindas();                           // chamada: manda executar
```

### Pontos de atenção
- O método é declarado **dentro da classe**, mas **fora do `main`**.
- Declarar um método não o executa — ele só roda quando é chamado.
- Na chamada, os parênteses `()` são obrigatórios.
- Como é `void`, **não existe** valor para guardar em uma variável.

### Erros comuns
- Criar o método **dentro** do `main`.
- Esquecer os parênteses: `exibirBoasVindas;`.
- Tentar fazer `String texto = exibirBoasVindas();` com um método `void`.

---

# 🎯 DESAFIO EXTRA — Método `void` com Parâmetro

### Contexto
Agora a mensagem de boas-vindas deve ser personalizada com o nome do usuário.

### Regras
1. Crie um método `void` chamado `saudarUsuario`.
2. O método deve receber um parâmetro `String nome`.
3. Deve exibir `"Olá, <nome>! Bons estudos."`.
4. Chame o método duas vezes, com nomes diferentes.

### Dados de teste
- `"Ana"`
- `"Bruno"`

### O que o aluno precisa fazer
Passar informações para dentro do método usando parâmetros.

---

# 💡 SOLUÇÃO DO DESAFIO EXTRA

```java
public class Main {
    public static void main(String[] args) {
        saudarUsuario("Ana");
        saudarUsuario("Bruno");
    }

    public static void saudarUsuario(String nome) {
        System.out.println("Olá, " + nome + "! Bons estudos.");
    }
}
```

---

# 🔍 EXPLICAÇÃO DO DESAFIO EXTRA

Parâmetros são **variáveis de entrada** do método.

### O que acontece na solução?
- Na primeira chamada, `"Ana"` é copiado para o parâmetro `nome`.
- O método exibe `"Olá, Ana! Bons estudos."`.
- Na segunda chamada, `nome` passa a valer `"Bruno"`.

### Parâmetro x Argumento
```java
public static void saudarUsuario(String nome) // nome = parâmetro
saudarUsuario("Ana");                         // "Ana" = argumento
```

### Pontos de atenção
- O tipo do argumento deve ser compatível com o tipo do parâmetro.
- A variável `nome` só existe **dentro** do método.
- O método continua sendo `void`: ele recebe dados, mas não devolve nada.

### Erros comuns
- Chamar `saudarUsuario()` sem passar o argumento.
- Passar um número em vez de texto: `saudarUsuario(10)`.
- Tentar usar `nome` dentro do `main`.

---

# 🧠 RELEMBRANDO — Métodos que devolvem valores

Até agora os métodos apenas **faziam algo**. Agora eles vão **calcular e devolver** um resultado.

### Comparação
```java
public static void exibirSoma(int a, int b) {  // só exibe
    System.out.println(a + b);
}

public static int somar(int a, int b) {        // devolve um int
    return a + b;
}
```

- No lugar de `void`, escrevemos o **tipo do valor devolvido**: `String`, `int`, `double`, `boolean`...
- A palavra `return` **devolve** o valor e **encerra** o método.
- Quem chama pode **guardar o resultado** em uma variável:

```java
int resultado = somar(2, 3); // resultado = 5
```

---

# 🎯 DESAFIO FINAL — Métodos Tipados: `String`, `int` e `double`

### Contexto
Um sistema escolar precisa montar o boletim de um aluno usando métodos que devolvem valores.

### Regras
1. Crie o método `montarNomeCompleto` que recebe `nome` e `sobrenome` e **retorna** uma `String`.
2. Crie o método `somarFaltas` que recebe as faltas de dois bimestres e **retorna** um `int`.
3. Crie o método `calcularMedia` que recebe duas notas e **retorna** um `double`.
4. Crie o método `void` `exibirBoletim` que recebe os três resultados e exibe o boletim.
5. O `main` deve guardar o retorno de cada método em uma variável antes de exibir.

### Dados de teste
- `nome = "Carla"`, `sobrenome = "Souza"`
- `faltasPrimeiroBimestre = 3`, `faltasSegundoBimestre = 2`
- `nota1 = 8.0`, `nota2 = 7.0`

### O que o aluno precisa fazer
Criar três métodos tipados e usar seus retornos no `main`.

---

# 💡 SOLUÇÃO DO DESAFIO FINAL

```java
public class Main {
    public static void main(String[] args) {
        String nomeCompleto = montarNomeCompleto("Carla", "Souza");
        int totalFaltas = somarFaltas(3, 2);
        double media = calcularMedia(8.0, 7.0);

        exibirBoletim(nomeCompleto, totalFaltas, media);
    }

    public static String montarNomeCompleto(String nome, String sobrenome) {
        return nome + " " + sobrenome;
    }

    public static int somarFaltas(int faltasPrimeiroBimestre, int faltasSegundoBimestre) {
        return faltasPrimeiroBimestre + faltasSegundoBimestre;
    }

    public static double calcularMedia(double nota1, double nota2) {
        return (nota1 + nota2) / 2;
    }

    public static void exibirBoletim(String nomeCompleto, int totalFaltas, double media) {
        System.out.println("Aluno: " + nomeCompleto);
        System.out.println("Faltas: " + totalFaltas);
        System.out.println("Média: " + media);
    }
}
```

---

# 🔍 EXPLICAÇÃO DO DESAFIO FINAL

Cada método tem **uma responsabilidade** e devolve **um tipo específico**.

### O que acontece na solução?
| Chamada | Tipo de retorno | Valor devolvido |
|---------|-----------------|-----------------|
| `montarNomeCompleto("Carla", "Souza")` | `String` | `"Carla Souza"` |
| `somarFaltas(3, 2)` | `int` | `5` |
| `calcularMedia(8.0, 7.0)` | `double` | `7.5` |
| `exibirBoletim(...)` | `void` | nada — apenas exibe |

### O fluxo do `return`
1. O `main` chama `calcularMedia(8.0, 7.0)`.
2. O método calcula `(8.0 + 7.0) / 2`.
3. `return` devolve `7.5` para o `main`.
4. O valor é guardado em `media`.

### Pontos de atenção
- O tipo do `return` deve ser o mesmo tipo declarado no método.
- Todo método não-`void` **precisa** ter um `return`.
- Qualquer código depois do `return` não é executado.
- Métodos que calculam (`return`) e métodos que exibem (`void`) devem ficar separados — isso facilita reaproveitar o cálculo.
- Use nomes com verbos: `calcular`, `montar`, `somar`, `exibir`.

### Erros comuns
- Esquecer o `return` em um método `int`, `double` ou `String` → erro de compilação.
- Retornar tipo errado: `return "7.5";` em um método `double`.
- Chamar um método com retorno e **não usar** o valor devolvido.
- Colocar `System.out.println` dentro do método de cálculo em vez de retornar o valor.
