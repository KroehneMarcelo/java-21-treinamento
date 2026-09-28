---
marp: true
theme: default
paginate: true
---

# JAVA 21
## Módulo 01 — Variáveis e Tipos

**Metodologia:** Desafio 1 → Solução 1 → Explicação do Desafio 1 → Desafio Extra → Solução do Desafio Extra → Explicação do Desafio Extra → Desafio Final → Solução do Desafio Final → Explicação do Desafio Final

---

# 🎯 DESAFIO 1 — Cadastro Inicial de Aluno

### Contexto
Uma escola está começando um sistema simples para cadastrar alunos.

### Regras
1. O nome do aluno deve ser armazenado em uma variável de texto.
2. A idade deve ser armazenada em uma variável numérica inteira.
3. A informação sobre matrícula ativa deve ser armazenada em uma variável booleana.
4. O programa deve exibir os três valores no console.

### Dados de teste
- `nomeAluno = "Maria"`
- `idadeAluno = 18`
- `matriculaAtiva = true`

### O que o aluno precisa fazer
Declarar as variáveis com os tipos corretos, atribuir os valores de teste e exibir as informações.

---

# 💡 SOLUÇÃO 1

```java
public class Main {
    public static void main(String[] args) {
        String nomeAluno = "Maria";
        int idadeAluno = 18;
        boolean matriculaAtiva = true;

        System.out.println("Nome: " + nomeAluno);
        System.out.println("Idade: " + idadeAluno);
        System.out.println("Matrícula ativa: " + matriculaAtiva);
    }
}
```

---

# 🔍 EXPLICAÇÃO DO DESAFIO 1

Em Java, toda variável precisa ser declarada com um tipo antes de ser usada. Esse tipo informa ao compilador qual dado pode ser armazenado naquela variável.

### Tipos usados na solução
- `String` guarda textos, como nomes.
- `int` guarda números inteiros, como idade.
- `boolean` guarda apenas `true` ou `false`.

### Como ler a declaração
- `String nomeAluno = "Maria";`
- `int idadeAluno = 18;`
- `boolean matriculaAtiva = true;`

Cada linha tem a mesma ideia: **tipo + nome da variável + valor inicial**.

### Pontos de atenção
- O nome da variável deve deixar claro o que ela representa.
- `String` sempre usa aspas duplas.
- `boolean` não usa aspas: o valor é `true` ou `false`.

### Erros comuns
- Tentar usar a variável sem declarar o tipo.
- Escolher nomes genéricos, como `x` ou `valor`.
- Misturar texto com número na mesma variável.

---

# 🎯 DESAFIO EXTRA — Código Fixo do Produto

### Contexto
Agora o sistema precisa cadastrar um produto simples.

### Regras
1. O código do produto deve ser um número inteiro.
2. O código do produto não pode mudar depois de definido.
3. O nome do produto deve ser um texto.
4. O preço deve ser um número decimal.
5. O programa deve exibir os dados no console.

### Dados de teste
- `codigoProduto = 101`
- `nomeProduto = "Teclado Mecânico"`
- `precoProduto = 250.50`

### O que o aluno precisa fazer
Declarar as variáveis com os tipos corretos e usar `final` no código do produto.

---

# 💡 SOLUÇÃO DO DESAFIO EXTRA

```java
public class Main {
    public static void main(String[] args) {
        final int codigoProduto = 101;
        String nomeProduto = "Teclado Mecânico";
        double precoProduto = 250.50;

        System.out.println("Código: " + codigoProduto);
        System.out.println("Produto: " + nomeProduto);
        System.out.println("Preço: " + precoProduto);
    }
}
```

---

# 🔍 EXPLICAÇÃO DO DESAFIO EXTRA

A palavra-chave `final` impede uma nova atribuição depois que a variável recebe o primeiro valor.

### O que isso significa na prática?
```java
final int codigoProduto = 101;
// codigoProduto = 202; // erro de compilação
```

O código do produto é um bom candidato para `final` porque representa uma informação que não deveria mudar ao longo da execução.

### Tipos escolhidos
- `int` para o código, porque é um número inteiro.
- `String` para o nome, porque é texto.
- `double` para o preço, porque pode ter casas decimais.

### Pontos de atenção
- `final` bloqueia a troca da referência ou do valor da variável, não apenas a impressão no console.
- `double` é mais adequado do que `int` para valores com centavos.

### Erros comuns
- Declarar preço com `int` quando existe parte decimal.
- Tentar reatribuir uma variável marcada com `final`.
- Criar nomes vagos, como `nome` e `valor`, em exemplos que já têm mais de um dado.

---

# 🎯 DESAFIO FINAL — Corrigindo Tipos Incompatíveis

### Contexto
Um colega montou um rascunho de cadastro de empresa, mas o código não compila.

### Regras
1. O nome da empresa deve continuar sendo um texto.
2. O CNPJ deve continuar sendo um texto e não pode mudar depois de definido.
3. A quantidade de funcionários deve ser numérica e inteira.
4. A empresa deve informar se está ativa com um valor booleano.
5. O programa deve ser corrigido sem mudar o objetivo do cadastro.

### Dados de teste
Use este rascunho como ponto de partida:

```java
String nomeEmpresa = 500;
final String cnpj = "12.345.678/0001-99";
double quantidadeFuncionarios = 42;
boolean empresaAtiva = "sim";
```

### O que o aluno precisa fazer
Corrigir os tipos incompatíveis para que o cadastro represente os dados corretamente e o programa possa ser executado.

---

# 💡 SOLUÇÃO DO DESAFIO FINAL

```java
public class Main {
    public static void main(String[] args) {
        String nomeEmpresa = "Lykon Tech";
        final String cnpj = "12.345.678/0001-99";
        int quantidadeFuncionarios = 42;
        boolean empresaAtiva = true;

        System.out.println("Empresa: " + nomeEmpresa);
        System.out.println("CNPJ: " + cnpj);
        System.out.println("Funcionários: " + quantidadeFuncionarios);
        System.out.println("Ativa: " + empresaAtiva);
    }
}
```

---

# 🔍 EXPLICAÇÃO DO DESAFIO FINAL

O problema do rascunho original era a incompatibilidade entre o tipo declarado e o valor atribuído.

### Ajustes feitos
- `String nomeEmpresa = "Lykon Tech";` porque nome é texto.
- `int quantidadeFuncionarios = 42;` porque contagem de pessoas usa número inteiro.
- `boolean empresaAtiva = true;` porque o status precisa ser `true` ou `false`.
- `final String cnpj = "12.345.678/0001-99";` foi mantido porque o CNPJ continua sendo um texto fixo.

### Por que o código original falhava?
```java
String nomeEmpresa = 500;      // número em variável de texto
boolean empresaAtiva = "sim"; // texto em variável booleana
```

Java é uma linguagem de tipagem estática. Isso significa que o compilador verifica se o tipo da variável combina com o valor informado.

### Pontos de atenção
- `int` e `double` não são a mesma coisa: contagem usa `int`, valores com casas decimais usam `double`.
- `boolean` aceita apenas `true` ou `false`.
- Corrigir o tipo não é “enfeite”: é o que faz o programa compilar e representar o dado certo.

### Fechamento do módulo
Neste módulo, você praticou declaração de variáveis, escolha do tipo correto, uso de `final` e correção de incompatibilidade de tipos.
