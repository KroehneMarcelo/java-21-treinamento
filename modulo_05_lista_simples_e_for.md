---
marp: true
theme: default
paginate: true
---

# JAVA 21
## Módulo 05 — Lista Simples e Loop For

**Metodologia:** Desafio 1 → Solução 1 → Explicação do Desafio 1 → Desafio Extra → Solução do Desafio Extra → Explicação do Desafio Extra → Desafio Final → Solução do Desafio Final → Explicação do Desafio Final

---

# 🎯 DESAFIO 1 — Criando uma Lista Simples

### Contexto
Um sistema precisa guardar uma pequena lista de nomes de alunos para exibição posterior.

### Regras
1. A lista deve ser criada usando array simples `[]`.
2. A lista deve armazenar `String`.
3. A lista deve conter exatamente 4 nomes.
4. O programa deve exibir cada nome na ordem em que foi armazenado.

### Dados de teste
- `alunos = {"Ana", "Bruno", "Carla", "Diego"}`

### O que o aluno precisa fazer
Criar um array simples e imprimir todos os elementos.

---

# 💡 SOLUÇÃO 1

```java
public class Main {
    public static void main(String[] args) {
        String[] alunos = {"Ana", "Bruno", "Carla", "Diego"};

        System.out.println(alunos[0]);
        System.out.println(alunos[1]);
        System.out.println(alunos[2]);
        System.out.println(alunos[3]);
    }
}
```

---

# 🔍 EXPLICAÇÃO DO DESAFIO 1

Um array simples é uma estrutura que guarda vários valores do mesmo tipo em uma única variável.

### O que acontece na solução?
- `alunos` armazena quatro textos.
- Cada posição do array é acessada pelo índice.
- O primeiro item fica na posição `0`.
- O último item, nesse caso, fica na posição `3`.

### Estrutura básica
```java
String[] alunos = {"Ana", "Bruno", "Carla", "Diego"};
```

### Pontos de atenção
- Em arrays, o primeiro índice sempre começa em `0`.
- O tamanho da lista deve ser respeitado para evitar `ArrayIndexOutOfBoundsException`.
- Arrays são úteis quando o número de itens é conhecido ou varia pouco.

### Erros comuns
- Tentar acessar `alunos[4]` em um array de 4 posições.
- Confundir quantidade de elementos com índice máximo.

---

# 🎯 DESAFIO EXTRA — Percorrendo a Lista com `for`

### Contexto
Agora o sistema precisa percorrer uma lista de produtos e exibir cada item automaticamente.

### Regras
1. A lista deve ser armazenada em um array simples.
2. Use o laço `for` tradicional.
3. O laço deve percorrer todos os elementos do array.
4. O programa deve exibir o índice e o valor de cada posição.

### Dados de teste
- `produtos = {"Teclado", "Mouse", "Monitor"}`

### O que o aluno precisa fazer
Usar o `for` para percorrer o array sem escrever cada `println` manualmente.

---

# 💡 SOLUÇÃO DO DESAFIO EXTRA

```java
public class Main {
    public static void main(String[] args) {
        String[] produtos = {"Teclado", "Mouse", "Monitor"};

        for (int i = 0; i < produtos.length; i++) {
            System.out.println("Índice " + i + ": " + produtos[i]);
        }
    }
}
```

---

# 🔍 EXPLICAÇÃO DO DESAFIO EXTRA

O `for` é ideal quando sabemos quantas vezes queremos repetir uma ação.

### Estrutura do `for`
```java
for (inicializacao; condicao; atualizacao) {
    // bloco de codigo
}
```

### O que acontece na solução?
- `i` começa em `0`.
- O loop continua enquanto `i < produtos.length`.
- A cada repetição, `i` é incrementado com `i++`.
- Cada posição do array é acessada e exibida.

### Pontos de atenção
- `produtos.length` representa a quantidade de elementos do array.
- O último índice é sempre `length - 1`.
- O `for` evita repetição manual e deixa o código mais limpo.

### Erros comuns
- Usar `<=` em vez de `<` e tentar acessar uma posição inválida.
- Esquecer o incremento do contador.
- Confundir `length` com o último índice.

---

# 🎯 DESAFIO FINAL — Lista e For em Conjunto

### Contexto
Um sistema precisa guardar notas de um aluno e calcular a soma de todas elas.

### Regras
1. As notas devem ser armazenadas em um array simples.
2. Use `for` para percorrer todas as notas.
3. Some todos os valores do array.
4. No final, exiba a soma e a média das notas.

### Dados de teste
- `notas = {7.5, 8.0, 6.5, 9.0}`

### O que o aluno precisa fazer
Criar a lista, percorrê-la com `for` e calcular soma e média.

---

# 💡 SOLUÇÃO DO DESAFIO FINAL

```java
public class Main {
    public static void main(String[] args) {
        double[] notas = {7.5, 8.0, 6.5, 9.0};
        double soma = 0;

        for (int i = 0; i < notas.length; i++) {
            soma += notas[i];
        }

        double media = soma / notas.length;

        System.out.println("Soma: " + soma);
        System.out.println("Média: " + media);
    }
}
```

---

# 🔍 EXPLICAÇÃO DO DESAFIO FINAL

Aqui o array e o `for` trabalham juntos para resolver um problema real.

### O que a solução faz?
- Armazena quatro notas em um array.
- Percorre cada posição com `for`.
- Soma os valores na variável `soma`.
- Calcula a média dividindo pela quantidade de elementos.

### Pontos de atenção
- Sempre inicialize a variável acumuladora com `0`.
- A média deve usar `notas.length` para funcionar com qualquer tamanho de lista.
- Arrays simples são ótimos para começar, porque deixam claro o conceito de posição e repetição.

### Erros comuns
- Esquecer de somar dentro do loop.
- Dividir por um valor fixo em vez do tamanho do array.
- Usar índice fora do limite do array.
