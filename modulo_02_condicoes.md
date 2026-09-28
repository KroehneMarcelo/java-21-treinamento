---
marp: true
theme: default
paginate: true
---

# JAVA 21
## Módulo 02 — Condições e Fluxo de Controle

**Metodologia:** Desafio 1 → Solução 1 → Explicação do Desafio 1 → Desafio Extra → Solução do Desafio Extra → Explicação do Desafio Extra → Desafio Final → Solução do Desafio Final → Explicação do Desafio Final

---

# 🎯 DESAFIO 1 — Validação de Maioridade

### Contexto
Um sistema de cadastro precisa informar se uma pessoa já pode finalizar o registro de adulto.

### Regras
1. O programa deve receber a idade em uma variável `int`.
2. O programa deve verificar se a idade é maior ou igual a `18`.
3. Se a condição for verdadeira, deve exibir `"Cadastro liberado"`.
4. Caso contrário, deve exibir `"Cadastro bloqueado"`.

### Dados de teste
- `idade = 20`

### O que o aluno precisa fazer
Escrever uma condição com `if` e `else` para decidir qual mensagem deve ser exibida.

---

# 💡 SOLUÇÃO 1

```java
public class Main {
    public static void main(String[] args) {
        int idade = 20;

        if (idade >= 18) {
            System.out.println("Cadastro liberado");
        } else {
            System.out.println("Cadastro bloqueado");
        }
    }
}
```

---

# 🔍 EXPLICAÇÃO DO DESAFIO 1

O `if` executa um bloco quando a condição resulta em `true`. O `else` cuida do caminho contrário.

### Conceitos usados
- `idade >= 18` é uma comparação relacional.
- Comparações relacionais retornam `boolean`.
- `true` entra no bloco do `if`.
- `false` entra no bloco do `else`.

### Operadores relacionais mais comuns
- `==` igual
- `!=` diferente
- `>` maior que
- `<` menor que
- `>=` maior ou igual
- `<=` menor ou igual

### `==` não é a mesma coisa que `=`
- `=` atribui valor.
- `==` compara valores.

```java
int codigo = 10;
// if (codigo = 10) { } // erro de compilação: o if precisa de boolean
if (codigo == 10) {
    System.out.println("Código correto");
}
```

### Pontos de atenção
- Toda condição de `if` precisa resultar em `true` ou `false`.
- Use operadores relacionais para montar essa condição.

### Erros comuns
- Tentar usar `=` dentro do `if` pensando que está comparando.
- Esquecer o bloco `else` quando o exercício pede dois comportamentos.

---

# 🎯 DESAFIO EXTRA — Liberação de Desconto

### Contexto
Uma loja quer liberar desconto quando o cliente atende regras simples de campanha.

### Regras
1. O cliente ganha desconto se for `VIP` **ou** se tiver cupom.
2. O cliente também precisa estar ativo.
3. Se todas as validações necessárias forem atendidas, o programa deve exibir `"Desconto liberado"`.
4. Caso contrário, deve exibir `"Desconto não liberado"`.

### Dados de teste
- `clienteAtivo = true`
- `clienteVip = false`
- `temCupom = true`

### O que o aluno precisa fazer
Usar variáveis booleanas com `||` e `&&` para decidir se o desconto pode ser concedido.

---

# 💡 SOLUÇÃO DO DESAFIO EXTRA

```java
public class Main {
    public static void main(String[] args) {
        boolean clienteAtivo = true;
        boolean clienteVip = false;
        boolean temCupom = true;

        if (clienteAtivo && (clienteVip || temCupom)) {
            System.out.println("Desconto liberado");
        } else {
            System.out.println("Desconto não liberado");
        }
    }
}
```

---

# 🔍 EXPLICAÇÃO DO DESAFIO EXTRA

Neste desafio, as comparações já chegaram prontas em variáveis booleanas. Por isso, podemos usá-las diretamente no `if`.

### Como a lógica funciona
- `clienteVip || temCupom` aceita quando pelo menos uma das duas condições é verdadeira.
- `clienteAtivo && (...)` exige que o cliente esteja ativo **e** também atenda à regra do desconto.

### Verdadeiro ou falso
- `||` retorna `true` quando pelo menos uma condição é verdadeira.
- `&&` retorna `true` somente quando todas as condições necessárias são verdadeiras.

### Clean Code na condição
Uma boa leitura para esse exemplo é pensar em frases:
- o cliente está ativo
- o cliente é VIP ou tem cupom

Essa leitura ajuda a manter a regra clara.

### Pontos de atenção
- Quando a expressão mistura `&&` e `||`, os parênteses deixam a intenção explícita.
- Variáveis booleanas bem nomeadas facilitam a leitura do código.

### Erros comuns
- Escrever `if (clienteAtivo == true)` em vez de `if (clienteAtivo)`.
- Esquecer que `&&` é mais restritivo que `||`.

---

# 🎯 DESAFIO FINAL — Acesso ao Painel Administrativo

### Contexto
Um sistema interno precisa decidir se um usuário pode acessar o painel administrativo.

### Regras
1. O usuário pode entrar se estiver ativo **e** tiver permissão.
2. Um administrador também pode entrar, mesmo sem a permissão comum.
3. O programa deve exibir `"Acesso permitido"` ou `"Acesso negado"`.
4. A solução deve priorizar legibilidade.

### Dados de teste
- `usuarioAtivo = true`
- `possuiPermissao = false`
- `administrador = true`

### O que o aluno precisa fazer
Montar a condição final combinando operadores relacionais e lógicos com uma escrita clara.

---

# 💡 SOLUÇÃO DO DESAFIO FINAL

```java
public class Main {
    public static void main(String[] args) {
        boolean usuarioAtivo = true;
        boolean possuiPermissao = false;
        boolean administrador = true;

        boolean acessoPadrao = usuarioAtivo && possuiPermissao;
        boolean acessoPermitido = acessoPadrao || administrador;

        if (acessoPermitido) {
            System.out.println("Acesso permitido");
        } else {
            System.out.println("Acesso negado");
        }
    }
}
```

---

# 🔍 EXPLICAÇÃO DO DESAFIO FINAL

Este desafio integra `if/else`, booleanos, `&&`, `||`, precedência e Clean Code.

### Leitura da solução
- `acessoPadrao` representa a regra comum: usuário ativo **e** com permissão.
- `acessoPermitido` abre uma exceção: acesso padrão **ou** perfil administrador.

### Sobre precedência
Sem parênteses, `&&` já é avaliado antes de `||`. Mesmo assim, quebrar a lógica em variáveis booleanas deixa a intenção mais clara.

```java
boolean acessoPadrao = usuarioAtivo && possuiPermissao;
boolean acessoPermitido = acessoPadrao || administrador;
```

### Por que isso é Clean Code?
- Os nomes explicam a regra de negócio.
- O `if` final fica curto.
- A manutenção fica mais simples se a regra mudar depois.

### Pontos de atenção
- Use `!variavel` quando precisar negar uma condição booleana.
- Prefira variáveis intermediárias quando a expressão começar a ficar longa.
- Parênteses continuam sendo úteis quando ajudam a leitura.

### Erros comuns
- Colocar toda a regra em uma linha confusa.
- Repetir comparações como `administrador == true`.
- Ignorar a prioridade de leitura humana só porque o compilador entende a expressão.
