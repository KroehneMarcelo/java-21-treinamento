---
marp: true
theme: default
paginate: true
---

# JAVA 21
## Módulo 06 — Laços `while` e `do-while`

**Metodologia:** Desafio 1 → Solução 1 → Explicação do Desafio 1 → Desafio Extra → Solução do Desafio Extra → Explicação do Desafio Extra → Desafio Final → Solução do Desafio Final → Explicação do Desafio Final

---

# 🎯 DESAFIO 1 — Contagem Regressiva com `while`

### Contexto
Um sistema precisa mostrar uma contagem regressiva antes de iniciar um processo.

### Regras
1. A contagem deve começar em `5`.
2. Use o laço `while`.
3. O programa deve exibir os números até `1`.
4. Ao final, exiba a mensagem `"Iniciando..."`.

### Dados de teste
- `contador = 5`

### O que o aluno precisa fazer
Criar uma repetição com `while` que vá diminuindo o contador a cada volta.

---

# 💡 SOLUÇÃO 1

```java
public class Main {
    public static void main(String[] args) {
        int contador = 5;

        while (contador >= 1) {
            System.out.println(contador);
            contador--;
        }

        System.out.println("Iniciando...");
    }
}
```

---

# 🔍 EXPLICAÇÃO DO DESAFIO 1

O `while` executa um bloco **enquanto** a condição for verdadeira.

### Estrutura
```java
while (condicao) {
    // bloco de codigo
}
```

### O que acontece na solução?
- `contador` começa em `5`.
- Enquanto `contador >= 1`, o número é impresso.
- A cada volta, `contador--` diminui o valor em 1.
- Quando o contador chega a `0`, o laço para.

### Pontos de atenção
- A atualização da variável precisa acontecer dentro do laço, senão ocorre loop infinito.
- A condição deve ser escrita com cuidado para não pular valores.
- O `while` é útil quando não sabemos exatamente quantas repetições ocorrerão.

### Erros comuns
- Esquecer de diminuir o contador.
- Inverter a condição e nunca entrar no laço.
- Criar uma condição que nunca fica falsa.

---

# 🎯 DESAFIO EXTRA — Tentativas de Senha com `while`

### Contexto
Um sistema precisa permitir até 3 tentativas para o usuário informar a senha correta.

### Regras
1. A quantidade máxima de tentativas deve ser `3`.
2. Use o laço `while`.
3. A cada tentativa, exiba quantas tentativas já foram feitas.
4. Ao final, exiba `"Acesso liberado"` ou `"Acesso bloqueado"`.

### Dados de teste
- `senhaCorreta = "java21"`
- `senhaDigitada = "teste"`
- `tentativas = 0`

### O que o aluno precisa fazer
Controlar a repetição com `while` até a senha ser aceita ou as tentativas acabarem.

---

# 💡 SOLUÇÃO DO DESAFIO EXTRA

```java
public class Main {
    public static void main(String[] args) {
        String senhaCorreta = "java21";
        String senhaDigitada = "teste";
        int tentativas = 0;
        boolean acessoLiberado = false;

        while (tentativas < 3 && !acessoLiberado) {
            tentativas++;
            System.out.println("Tentativa " + tentativas);

            if (senhaCorreta.equals(senhaDigitada)) {
                acessoLiberado = true;
            }
        }

        if (acessoLiberado) {
            System.out.println("Acesso liberado");
        } else {
            System.out.println("Acesso bloqueado");
        }
    }
}
```

---

# 🔍 EXPLICAÇÃO DO DESAFIO EXTRA

Aqui o `while` repete até uma condição de controle ser satisfeita.

### O que acontece na solução?
- `tentativas` começa em `0`.
- O laço continua enquanto houver menos de 3 tentativas e o acesso não tiver sido liberado.
- A cada volta, a tentativa é contabilizada.
- Se a senha estiver correta, a variável `acessoLiberado` muda para `true`.

### Pontos de atenção
- Repetições com condição dupla exigem cuidado na leitura.
- Compare textos com `equals()`.
- Separe a lógica de controle da lógica de validação para manter o código legível.

### Erros comuns
- Esquecer de atualizar o contador.
- Colocar a comparação da senha fora do loop sem necessidade.
- Não inicializar corretamente a variável booleana de controle.

---

# 🎯 DESAFIO FINAL — Execução Inicial com `do-while`

### Contexto
Um sistema precisa exibir um menu pelo menos uma vez e repetir a exibição enquanto o usuário não escolher sair.

### Regras
1. Use o laço `do-while`.
2. O menu deve aparecer pelo menos uma vez.
3. A opção `0` encerra o sistema.
4. Qualquer outra opção faz o menu aparecer novamente.

### Dados de teste
- `opcao = 1`

### O que o aluno precisa fazer
Criar um menu simples que seja executado antes da verificação da condição.

---

# 💡 SOLUÇÃO DO DESAFIO FINAL

```java
public class Main {
    public static void main(String[] args) {
        int opcao;

        do {
            System.out.println("1 - Continuar");
            System.out.println("0 - Sair");
            opcao = 1;
        } while (opcao != 0);

        System.out.println("Sistema encerrado");
    }
}
```

---

# 🔍 EXPLICAÇÃO DO DESAFIO FINAL

O `do-while` é parecido com o `while`, mas com uma diferença importante: ele executa o bloco **antes** de testar a condição.

### Estrutura
```java
do {
    // bloco de codigo
} while (condicao);
```

### O que acontece na solução?
- O menu é exibido pelo menos uma vez.
- Depois disso, o Java verifica se `opcao != 0`.
- Como o valor de teste é `1`, o laço continuaria repetindo.

### Diferença entre `while` e `do-while`
- `while`: testa primeiro, executa depois.
- `do-while`: executa primeiro, testa depois.

### Pontos de atenção
- O `do-while` termina com `while (condicao);` e precisa desse ponto e vírgula.
- Use essa estrutura quando o bloco precisar acontecer ao menos uma vez.
- Se a lógica depender de entrada do usuário, a opção deve ser atualizada dentro do laço.

### Erros comuns
- Esquecer o `;` no final do `while`.
- Usar `do-while` quando `while` já resolveria de forma mais simples.
- Não atualizar a variável usada na condição.
