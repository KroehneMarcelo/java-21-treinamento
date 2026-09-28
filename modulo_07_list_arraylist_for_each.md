---
marp: true
theme: default
paginate: true
---

# JAVA 21
## Módulo 07 — List, ArrayList e `for each`

**Metodologia:** Desafio 1 → Solução 1 → Explicação do Desafio 1 → Desafio Extra → Solução do Desafio Extra → Explicação do Desafio Extra → Desafio Final → Solução do Desafio Final → Explicação do Desafio Final

---

# 🎯 DESAFIO 1 — Criando uma `List`

### Contexto
Um sistema precisa guardar uma lista de nomes de clientes que pode crescer com facilidade.

### Regras
1. A lista deve ser declarada usando a interface `List`.
2. A implementação deve ser `ArrayList`.
3. A lista deve armazenar `String`.
4. O programa deve exibir a quantidade de elementos da lista.

### Dados de teste
- `clientes = ["Ana", "Bruno", "Carla"]`

### O que o aluno precisa fazer
Criar uma lista usando `List` e `ArrayList`, adicionar elementos e mostrar o tamanho.

---

# 💡 SOLUÇÃO 1

```java
import java.util.ArrayList;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        List<String> clientes = new ArrayList<>();

        clientes.add("Ana");
        clientes.add("Bruno");
        clientes.add("Carla");

        System.out.println("Quantidade: " + clientes.size());
    }
}
```

---

# 🔍 EXPLICAÇÃO DO DESAFIO 1

`List` representa o contrato e `ArrayList` é uma das implementações mais usadas.

### O que acontece na solução?
- `clientes` é declarada como `List<String>`.
- A criação real usa `new ArrayList<>()`.
- Os nomes são adicionados com `add()`.
- `size()` informa quantos elementos existem na lista.

### Por que usar `List` na declaração?
Isso deixa o código mais flexível. Se necessário, a implementação pode mudar depois sem alterar o restante da lógica.

### Pontos de atenção
- `List` é uma interface, então não pode ser instanciada diretamente.
- `ArrayList` permite crescer dinamicamente.
- O tipo dentro de `<>` garante que a lista aceite apenas um tipo de dado.

### Erros comuns
- Escrever `new List<>()`.
- Esquecer de importar `java.util.List` e `java.util.ArrayList`.
- Usar a lista sem declarar o tipo genérico.

---

# 🎯 DESAFIO EXTRA — Percorrendo uma `List` com `for each`

### Contexto
Agora o sistema precisa exibir todos os produtos de uma lista de forma mais simples.

### Regras
1. A lista deve ser criada com `ArrayList`.
2. Use o laço `for each`.
3. Exiba cada item da lista.
4. O código deve ser mais legível do que o `for` tradicional quando o índice não for necessário.

### Dados de teste
- `produtos = ["Teclado", "Mouse", "Monitor"]`

### O que o aluno precisa fazer
Percorrer a lista usando `for each` e imprimir cada valor.

---

# 💡 SOLUÇÃO DO DESAFIO EXTRA

```java
import java.util.ArrayList;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        List<String> produtos = new ArrayList<>();

        produtos.add("Teclado");
        produtos.add("Mouse");
        produtos.add("Monitor");

        for (String produto : produtos) {
            System.out.println(produto);
        }
    }
}
```

---

# 🔍 EXPLICAÇÃO DO DESAFIO EXTRA

O `for each` é uma forma simples de percorrer coleções e arrays.

### Estrutura
```java
for (tipo elemento : colecao) {
    // uso do elemento
}
```

### O que acontece na solução?
- Cada item da lista é entregue em uma variável temporária chamada `produto`.
- O laço percorre todos os valores automaticamente.
- Não precisamos lidar com índice quando ele não é necessário.

### Pontos de atenção
- `for each` é ótimo para leitura, mas não é a melhor opção quando você precisa do índice.
- Ele serve bem para exibir ou processar cada elemento individualmente.
- O nome da variável do laço deve ser claro e representativo.

### Erros comuns
- Tentar alterar a coleção dentro do `for each` sem necessidade.
- Usar `for each` quando o índice é obrigatório.
- Confundir o elemento atual com a coleção inteira.

---

# 🎯 DESAFIO FINAL — Lista de Tarefas com `List` e `for each`

### Contexto
Um sistema precisa armazenar tarefas e marcar quais já foram concluídas.

### Regras
1. Use `List<String>` com `ArrayList`.
2. Adicione pelo menos 4 tarefas.
3. Percorra a lista com `for each`.
4. Exiba cada tarefa com o prefixo `"- "`.

### Dados de teste
- `tarefas = ["Estudar Java", "Praticar exercícios", "Ler documentação", "Revisar código"]`

### O que o aluno precisa fazer
Criar a lista e usar `for each` para exibir todas as tarefas.

---

# 💡 SOLUÇÃO DO DESAFIO FINAL

```java
import java.util.ArrayList;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        List<String> tarefas = new ArrayList<>();

        tarefas.add("Estudar Java");
        tarefas.add("Praticar exercícios");
        tarefas.add("Ler documentação");
        tarefas.add("Revisar código");

        for (String tarefa : tarefas) {
            System.out.println("- " + tarefa);
        }
    }
}
```

---

# 🔍 EXPLICAÇÃO DO DESAFIO FINAL

Aqui os três pontos do módulo aparecem juntos: `List`, `ArrayList` e `for each`.

### O que a solução faz?
- Cria uma lista dinâmica de tarefas.
- Adiciona vários textos com `add()`.
- Percorre todos os itens com `for each`.
- Exibe cada tarefa de forma simples e legível.

### Pontos de atenção
- `List` é a forma recomendada de declarar a variável.
- `ArrayList` é uma implementação prática para listas com crescimento dinâmico.
- `for each` simplifica o código quando o índice não é necessário.

### Erros comuns
- Instanciar a interface `List` diretamente.
- Usar `for each` esperando acessar o índice.
- Misturar lógica de processamento desnecessária dentro do laço.
