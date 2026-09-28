---
marp: true
theme: default
paginate: true
---

# JAVA 21
## Módulo 04 — Operador Ternário e Switch

**Metodologia:** Desafio 1 → Solução 1 → Explicação do Desafio 1 → Desafio 2 → Solução 2 → Explicação do Desafio 2 → Desafio Extra → Solução do Desafio Extra → Explicação do Desafio Extra → Desafio Final → Solução do Desafio Final → Explicação do Desafio Final

---

# 🎯 DESAFIO 1 — Situação do Aluno com Ternário

### Contexto
Um sistema escolar precisa exibir se o aluno foi aprovado ou reprovado de acordo com a nota final.

### Regras
1. A nota deve ser armazenada em uma variável `double`.
2. O aluno é aprovado quando a nota for maior ou igual a `7`.
3. A situação deve ser guardada em uma variável `String` usando o operador ternário.
4. O programa deve exibir `"Aprovado"` ou `"Reprovado"`.

### Dados de teste
- `notaFinal = 8.5`

### O que o aluno precisa fazer
Substituir um `if/else` simples por uma única linha usando `condicao ? valorSeVerdadeiro : valorSeFalso`.

---

# 💡 SOLUÇÃO 1

```java
public class Main {
    public static void main(String[] args) {
        double notaFinal = 8.5;

        String situacao = notaFinal >= 7 ? "Aprovado" : "Reprovado";

        System.out.println(situacao);
    }
}
```

---

# 🔍 EXPLICAÇÃO DO DESAFIO 1

O operador ternário é uma forma curta de escrever um `if/else` que **retorna um valor**.

### Estrutura
```java
tipo variavel = condicao ? valorSeVerdadeiro : valorSeFalso;
```

### O que acontece na solução?
- `notaFinal >= 7` resulta em `true`.
- Como a condição é verdadeira, o valor escolhido é `"Aprovado"`.
- O valor é atribuído à variável `situacao`.

### Equivalente com `if/else`
```java
String situacao;
if (notaFinal >= 7) {
    situacao = "Aprovado";
} else {
    situacao = "Reprovado";
}
```

### Pontos de atenção
- Os dois valores (verdadeiro e falso) devem ser do mesmo tipo (ou compatíveis).
- Use o ternário para decisões **simples**. Se a lógica crescer, prefira `if/else`.

### Erros comuns
- Encadear vários ternários em uma linha, deixando o código ilegível.
- Usar o ternário para executar ações (ex.: `System.out.println`) em vez de escolher valores.

---

# 🎯 DESAFIO 2 — Dia da Semana com Switch Comum

### Contexto
Um sistema recebe o número do dia da semana e precisa exibir o nome correspondente.

### Regras
1. O número do dia deve ser armazenado em uma variável `int`.
2. Use `switch` com `case` e `break`.
3. `1` = `"Domingo"`, `2` = `"Segunda"`, ..., `7` = `"Sábado"`.
4. Qualquer outro número deve exibir `"Dia inválido"`.

### Dados de teste
- `numeroDia = 3`

### O que o aluno precisa fazer
Escrever um `switch` tradicional, lembrando de usar `break` ao final de cada `case`.

---

# 💡 SOLUÇÃO 2

```java
public class Main {
    public static void main(String[] args) {
        int numeroDia = 3;

        switch (numeroDia) {
            case 1:
                System.out.println("Domingo");
                break;
            case 2:
                System.out.println("Segunda");
                break;
            case 3:
                System.out.println("Terça");
                break;
            case 4:
                System.out.println("Quarta");
                break;
            case 5:
                System.out.println("Quinta");
                break;
            case 6:
                System.out.println("Sexta");
                break;
            case 7:
                System.out.println("Sábado");
                break;
            default:
                System.out.println("Dia inválido");
        }
    }
}
```

---

# 🔍 EXPLICAÇÃO DO DESAFIO 2

O `switch` compara **um valor** com vários `case` possíveis.

### O que acontece na solução?
- `numeroDia` vale `3`.
- O `switch` pula direto para `case 3`.
- Exibe `"Terça"`.
- O `break` encerra o `switch`.

### E se esquecer o `break`?
Sem `break`, o Java continua executando os próximos `case` (*fall-through*):

```java
int numeroDia = 3;
switch (numeroDia) {
    case 3:
        System.out.println("Terça");
    case 4:
        System.out.println("Quarta");
        break;
}
// Saída: Terça
//        Quarta
```

### `default`
É executado quando nenhum `case` corresponde ao valor. Funciona como o `else` do `switch`.

### Pontos de atenção
- Cada `case` precisa ser um valor constante (ex.: `1`, `"ADMIN"`, `'A'`).
- Não podem existir dois `case` com o mesmo valor.

### Erros comuns
- Esquecer o `break` e executar `case` indesejados.
- Esquecer o `default` e não tratar valores inesperados.

---

# ⚠️ PONTO DE ATENÇÃO — O que colocar dentro do `switch( )`

O parâmetro de entrada do `switch` deve ser **um valor simples a ser comparado**, como `int`, `char`, `String` ou `enum`.

### ❌ Não use `boolean`
```java
boolean ativo = true;
switch (ativo) { // ERRO de compilação no Java 21
    ...
}
```
Para decisões de verdadeiro/falso, use `if/else` ou o operador ternário.

### ❌ Não faça operações/condições dentro do `switch`
```java
switch (idade >= 18) { ... }   // ERRO: resulta em boolean
switch (a + b * 2) { ... }     // Compila, mas dificulta a leitura
switch (texto.trim().toUpperCase()) { ... } // Esconde regra de negócio
```

### ✅ Prefira calcular antes e passar a variável
```java
String perfilNormalizado = texto.trim().toUpperCase();
switch (perfilNormalizado) { ... }
```

- O `switch` serve para **escolher entre valores**, não para avaliar condições.
- Condições como `>`, `<`, `&&`, `||` pertencem ao `if`.
- Variáveis com nomes claros deixam o `switch` mais legível e fácil de depurar.

---

# 🎯 DESAFIO EXTRA — Permissões com Switch Moderno (`->`)

### Contexto
Um sistema precisa exibir a permissão de acordo com o perfil do usuário.

### Regras
1. O perfil deve ser armazenado em uma variável `String`.
2. Use o `switch` com a sintaxe de seta `->`.
3. `"ADMIN"` exibe `"Acesso total"`.
4. `"OPERADOR"` e `"SUPORTE"` exibem `"Acesso parcial"`.
5. `"VISITANTE"` exibe `"Somente leitura"`.
6. Qualquer outro perfil exibe `"Perfil desconhecido"`.

### Dados de teste
- `perfil = "SUPORTE"`

### O que o aluno precisa fazer
Reescrever a lógica de `switch` sem usar `break`, agrupando casos com vírgula.

---

# 💡 SOLUÇÃO DO DESAFIO EXTRA

```java
public class Main {
    public static void main(String[] args) {
        String perfil = "SUPORTE";

        switch (perfil) {
            case "ADMIN" -> System.out.println("Acesso total");
            case "OPERADOR", "SUPORTE" -> System.out.println("Acesso parcial");
            case "VISITANTE" -> System.out.println("Somente leitura");
            default -> System.out.println("Perfil desconhecido");
        }
    }
}
```

---

# 🔍 EXPLICAÇÃO DO DESAFIO EXTRA

A seta `->` é uma forma moderna e mais limpa de escrever o `switch`.

> Obs.: a seta lembra a sintaxe de *lambda*, mas aqui ela apenas indica **"se for este caso, execute isto"**. Lambdas serão estudadas mais adiante.

### Diferenças para o `switch` comum
- **Não precisa de `break`**: apenas o `case` correspondente é executado.
- **Não existe *fall-through*** acidental.
- **Vários valores no mesmo `case`**, separados por vírgula.

### Mais de uma instrução no `case`
Use chaves `{ }`:
```java
case "ADMIN" -> {
    System.out.println("Acesso total");
    System.out.println("Bem-vindo, administrador");
}
```

### Pontos de atenção
- Não misture `case X:` e `case X ->` no mesmo `switch`.
- Continue tratando o `default`.

### Erros comuns
- Colocar `break` depois da seta achando que é obrigatório.
- Esquecer as chaves quando o `case` tem mais de uma linha.

---

# 🎯 DESAFIO FINAL — Cálculo de Frete com Switch como Atribuição

### Contexto
Uma loja precisa calcular o valor do frete de acordo com a região de entrega e informar se o frete é grátis.

### Regras
1. A região deve ser armazenada em uma variável `String`.
2. O valor do frete deve ser atribuído diretamente pelo `switch` (*switch expression*).
3. `"SUL"` e `"SUDESTE"` = `15.0`.
4. `"CENTRO-OESTE"` = `25.0`.
5. `"NORTE"` e `"NORDESTE"` = `35.0`.
6. Qualquer outra região = `50.0`.
7. Se o valor da compra for maior ou igual a `200`, o frete é grátis — use o operador ternário.

### Dados de teste
- `regiao = "SUL"`
- `valorCompra = 250.0`

### O que o aluno precisa fazer
Usar o `switch` para **gerar um valor** e combinar com o operador ternário.

---

# 💡 SOLUÇÃO DO DESAFIO FINAL

```java
public class Main {
    public static void main(String[] args) {
        String regiao = "SUL";
        double valorCompra = 250.0;

        double valorFrete = switch (regiao) {
            case "SUL", "SUDESTE" -> 15.0;
            case "CENTRO-OESTE" -> 25.0;
            case "NORTE", "NORDESTE" -> 35.0;
            default -> 50.0;
        };

        double freteFinal = valorCompra >= 200 ? 0.0 : valorFrete;
        String mensagem = freteFinal == 0.0 ? "Frete grátis!" : "Frete: R$ " + freteFinal;

        System.out.println(mensagem);
    }
}
```

---

# 🔍 EXPLICAÇÃO DO DESAFIO FINAL

Aqui o `switch` deixa de apenas executar ações e passa a **retornar um valor**.

### Estrutura
```java
tipo variavel = switch (valor) {
    case A -> resultado1;
    case B -> resultado2;
    default -> resultadoPadrao;
};
```

### O que acontece na solução?
- `regiao` vale `"SUL"`, então `valorFrete` recebe `15.0`.
- `valorCompra >= 200` é `true`, então `freteFinal` recebe `0.0`.
- A mensagem exibida é `"Frete grátis!"`.

### `yield` — quando o `case` precisa de um bloco
```java
double valorFrete = switch (regiao) {
    case "SUL" -> {
        System.out.println("Calculando frete para o Sul...");
        yield 15.0;
    }
    default -> 50.0;
};
```
`yield` indica qual valor o bloco devolve.

### Pontos de atenção
- O `switch` como atribuição termina com **ponto e vírgula** `};`.
- Todos os casos possíveis devem ser cobertos — por isso o `default` é obrigatório com `String` e `int`.
- Todos os `case` devem retornar o mesmo tipo.
- Lembre-se: o valor dentro do `switch( )` não deve ser `boolean` nem uma operação.

### Erros comuns
- Esquecer o `;` após a chave final.
- Omitir o `default` e receber erro de compilação.
- Usar `return` em vez de `yield` dentro do bloco.
