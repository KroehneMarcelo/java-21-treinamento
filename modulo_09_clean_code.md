---
marp: true
theme: default
paginate: true
---

# JAVA 21
## Módulo 09 — Clean Code desde a Base

**Metodologia:** Relembrando → Desafio 1 → Solução 1 → Explicação do Desafio 1 → Desafio Extra → Solução do Desafio Extra → Explicação do Desafio Extra → Desafio Final → Solução do Desafio Final → Explicação do Desafio Final

---

# 🧠 RELEMBRANDO — Código correto também precisa ser legível

Nos módulos anteriores, usamos `if`, operadores lógicos, `switch`, ternário e métodos.

Agora vamos olhar para código que **funciona**, mas pode ser difícil de entender ou manter.

### Perguntas úteis ao ler um programa
- Consigo entender a regra sem decifrar várias condições?
- Estou repetindo a mesma comparação desnecessariamente?
- O nome do método diz claramente o que ele faz?
- Se a regra mudar, sei onde alterá-la?

> Clean Code não é escrever o menor número de linhas. É tornar a intenção clara, sem mudar o comportamento esperado.

---

# 🎯 DESAFIO 1 — Simplificando condições

### Contexto
Um sistema de acesso recebe o perfil de um usuário, seu estado de ativação e sua permissão. O código abaixo funciona para os dados de teste, mas é repetitivo.

### Código a melhorar
```java
String perfil = "OPERADOR";
boolean ativo = true;
boolean temPermissao = true;

if (perfil.equals("ADMIN")) {
    System.out.println("Acesso total");
}
if (perfil.equals("OPERADOR")) {
    System.out.println("Acesso operacional");
}
if (perfil.equals("VISITANTE")) {
    System.out.println("Somente leitura");
}

if (ativo == true) {
    if (temPermissao == true) {
        System.out.println("Pode editar");
    }
}
```

### Regras
1. Mantenha as mensagens dos três perfis conhecidos; para os demais, exiba `"Perfil desconhecido"`.
2. Substitua os vários `if` que comparam `perfil` por um único `switch`.
3. Simplifique as comparações booleanas e una as duas condições de edição.

### Dados de teste
- `perfil = "OPERADOR"`, `ativo = true`, `temPermissao = true`

### O que o aluno precisa fazer
Reescrever as decisões sem mudar o resultado dos dados de teste.

---

# 💡 SOLUÇÃO 1

```java
public class Main {
    public static void main(String[] args) {
        String perfil = "OPERADOR";
        boolean ativo = true;
        boolean temPermissao = true;

        switch (perfil) {
            case "ADMIN" -> System.out.println("Acesso total");
            case "OPERADOR" -> System.out.println("Acesso operacional");
            case "VISITANTE" -> System.out.println("Somente leitura");
            default -> System.out.println("Perfil desconhecido");
        }

        if (ativo && temPermissao) {
            System.out.println("Pode editar");
        }
    }
}
```

---

# 🔍 EXPLICAÇÃO DO DESAFIO 1

### Por que usar `switch` aqui?
- A decisão escolhe **um entre vários valores possíveis** da mesma variável: `perfil`.
- Evitamos repetir `perfil.equals(...)` a cada comparação.
- O `default` trata perfis que não foram previstos.

Se as condições fossem faixas ou regras diferentes, `if/else` poderia ser mais adequado. Não precisamos trocar **todo** `if` por `switch`.

### Booleanos no `if`
- `if (ativo == true)` repete o que `ativo` já informa. Prefira `if (ativo)`.
- Para verificar o contrário, use `if (!ativo)`, em vez de `ativo == false`.

### Um `if` em vez de dois
`if (ativo && temPermissao)` expressa que **as duas condições precisam ser verdadeiras**. Como não há ação intermediária nem um `else` separado, podemos evitar o aninhamento.

### Pontos de atenção
- Agrupe condições somente quando a regra continuar clara e o comportamento for o mesmo.
- Se cada `if` tiver uma ação diferente para o caso falso, juntar as condições pode mudar o resultado.
- `switch` com `String` não aceita valor `null` neste exemplo; trate a entrada antes, se ela puder ser nula.

---

# 🎯 DESAFIO EXTRA — Quando usar o ternário?

### Contexto
Uma loja precisa exibir se uma compra recebe frete grátis. Veja uma decisão simples escrita de forma longa:

```java
String mensagem;
if (valorCompra >= 200) {
    mensagem = "Frete grátis";
} else {
    mensagem = "Frete pago";
}
```

### Regras
1. Para escolher **apenas um texto**, use o operador ternário.
2. Se a condição passar a envolver várias ações (registrar pedido, avisar cliente, calcular valores), prefira `if/else` e métodos bem nomeados.
3. Exiba a mensagem escolhida.

### Dados de teste
- `valorCompra = 250.0`

### O que o aluno precisa fazer
Simplificar a atribuição sem tornar o código difícil de ler.

---

# 💡 SOLUÇÃO DO DESAFIO EXTRA

```java
public class Main {
    public static void main(String[] args) {
        double valorCompra = 250.0;

        String mensagem = valorCompra >= 200 ? "Frete grátis" : "Frete pago";
        System.out.println(mensagem);
    }
}
```

---

# 🔍 EXPLICAÇÃO DO DESAFIO EXTRA

O ternário é uma boa opção quando existe **uma condição curta** e queremos **escolher um valor**.

```java
String mensagem = valorCompra >= 200 ? "Frete grátis" : "Frete pago";
```

### Quando preferir `if/else`?
- Quando cada caminho precisa executar várias ações.
- Quando a regra fica difícil de ler em uma única expressão.
- Quando você estaria tentado a encadear vários ternários.

### Exemplos de intenção
```java
// Uma escolha simples: ternário ajuda.
String situacao = nota >= 7 ? "Aprovado" : "Reprovado";

// Duas ações distintas: if/else comunica melhor.
if (valorCompra >= 200) {
    System.out.println("Frete grátis");
    System.out.println("Benefício aplicado ao pedido");
} else {
    System.out.println("Frete pago");
    System.out.println("Confira o valor antes de finalizar");
}
```

### Pontos de atenção
- **Não** use ternário só para economizar linhas.
- Escolher entre valores é diferente de executar ações em cada ramo.

---

# 🎯 DESAFIO FINAL — Um método que faz tudo

### Contexto
Um sistema escolar precisa mostrar o boletim de um aluno. O método abaixo mistura cálculo, classificação e exibição:

```java
public static void processarAluno(String nome, double nota1, double nota2) {
    double media = (nota1 + nota2) / 2;
    String situacao;
    if (media >= 7) {
        situacao = "Aprovado";
    } else {
        situacao = "Reprovado";
    }
    System.out.println("Aluno: " + nome);
    System.out.println("Média: " + media);
    System.out.println("Situação: " + situacao);
}
```

### Regras
1. Divida as responsabilidades em métodos menores com nomes claros.
2. Crie um método que **retorna `double`** para calcular a média.
3. Crie um método que **retorna `String`** para classificar a situação.
4. Crie um método `void` para exibir o boletim.
5. Mantenha a mesma saída do método original.

### Dados de teste
- `nome = "Carla"`, `nota1 = 8.0`, `nota2 = 7.0`

### O que o aluno precisa fazer
Refatorar o código para que cada método tenha uma responsabilidade clara, sem alterar o resultado.

---

# 💡 SOLUÇÃO DO DESAFIO FINAL

```java
public class Main {
    public static void main(String[] args) {
        String nome = "Carla";
        double media = calcularMedia(8.0, 7.0);
        String situacao = classificarSituacao(media);

        exibirBoletim(nome, media, situacao);
    }

    public static double calcularMedia(double nota1, double nota2) {
        return (nota1 + nota2) / 2;
    }

    public static String classificarSituacao(double media) {
        return media >= 7 ? "Aprovado" : "Reprovado";
    }

    public static void exibirBoletim(String nome, double media, String situacao) {
        System.out.println("Aluno: " + nome);
        System.out.println("Média: " + media);
        System.out.println("Situação: " + situacao);
    }
}
```

---

# 🔍 EXPLICAÇÃO DO DESAFIO FINAL

### Um método, uma responsabilidade
- `calcularMedia` **calcula** e devolve um `double`.
- `classificarSituacao` **decide** e devolve uma `String`.
- `exibirBoletim` **mostra** os dados, sem fazer cálculos.
- `main` **coordena** as chamadas, sem concentrar toda a lógica.

### O que melhorou?
Se a nota mínima mudar, alteramos a regra em `classificarSituacao`. Se a apresentação mudar, editamos `exibirBoletim`. Os cálculos podem ser usados em outro lugar sem imprimir nada.

**Saída com os dados de teste:** `Aluno: Carla`, `Média: 7.5`, `Situação: Aprovado` (uma informação por linha).

### Pontos de atenção
- Não divida um método só para deixá-lo curto: separe **responsabilidades**, não linhas.
- Um método pode ter várias linhas e continuar fazendo **uma coisa só**.
- Deixe o ternário para uma escolha simples, como a classificação acima.

### Erros comuns
- Misturar cálculo e `System.out.println` no mesmo método, impedindo reutilizar o resultado.
- Criar métodos com nomes vagos, como `fazerTudo()` ou `processar()`.
- Refatorar e, sem perceber, mudar a regra de aprovação.
