---
marp: true
theme: default
paginate: true
---

# JAVA 21
## Módulo 03 — Comparações em Java

**Metodologia:** Desafio 1 → Solução 1 → Explicação do Desafio 1 → Desafio Extra → Solução do Desafio Extra → Explicação do Desafio Extra → Desafio Final → Solução do Desafio Final → Explicação do Desafio Final

---

# 🎯 DESAFIO 1 — Comparando Códigos Numéricos

### Contexto
Um sistema precisa verificar se dois códigos de confirmação são iguais.

### Regras
1. Os dois códigos devem ser armazenados em variáveis `int`.
2. O programa deve comparar os valores usando `==`.
3. Quando os valores forem iguais, deve exibir `"Códigos iguais"`.
4. Caso contrário, deve exibir `"Códigos diferentes"`.

### Dados de teste
- `codigoInformado = 10`
- `codigoEsperado = 10`

### O que o aluno precisa fazer
Criar a comparação entre dois tipos primitivos e mostrar o resultado no console.

---

# 💡 SOLUÇÃO 1

```java
public class Main {
    public static void main(String[] args) {
        int codigoInformado = 10;
        int codigoEsperado = 10;

        if (codigoInformado == codigoEsperado) {
            System.out.println("Códigos iguais");
        } else {
            System.out.println("Códigos diferentes");
        }
    }
}
```

---

# 🔍 EXPLICAÇÃO DO DESAFIO 1

Para tipos primitivos, `==` compara o valor guardado na variável.

### O que acontece na solução?
- `codigoInformado` guarda `10`.
- `codigoEsperado` guarda `10`.
- `codigoInformado == codigoEsperado` resulta em `true`.
- O programa exibe `"Códigos iguais"`.

### Onde isso funciona bem?
- `int`
- `double`
- `char`
- `boolean`

### Pontos de atenção
- Este uso de `==` é seguro para comparar valores primitivos.
- O mesmo raciocínio não deve ser aplicado automaticamente a `String`.

### Erros comuns
- Usar `==` em `String` achando que ele compara o texto.
- Confundir o valor guardado com o objeto referenciado.

---

# 🎯 DESAFIO EXTRA — Conferência de Mensagem e Ordem Alfabética

### Contexto
Um sistema recebe uma mensagem em `StringBuilder` e também precisa descobrir qual nome vem primeiro em ordem alfabética.

### Regras
1. Compare o conteúdo de uma `String` esperada com uma mensagem recebida em `StringBuilder`.
2. Se o conteúdo for igual, exiba `"Mensagem válida"`; caso contrário, exiba `"Mensagem inválida"`.
3. Compare dois nomes com `compareTo()`.
4. Se o primeiro nome vier antes do segundo, exiba `"O primeiro nome vem antes"`.
5. Se os nomes forem iguais, exiba `"Os nomes são iguais"`.
6. Se o primeiro nome vier depois do segundo, exiba `"O primeiro nome vem depois"`.

### Dados de teste
- `mensagemEsperada = "CONFIRMADO"`
- `mensagemRecebida = new StringBuilder("CONFIRMADO")`
- `primeiroNome = "Ana"`
- `segundoNome = "Bruno"`

### O que o aluno precisa fazer
Usar `contentEquals()` para comparar conteúdos textuais diferentes e `compareTo()` para descobrir a ordem entre dois nomes.

---

# 💡 SOLUÇÃO DO DESAFIO EXTRA

```java
public class Main {
    public static void main(String[] args) {
        String mensagemEsperada = "CONFIRMADO";
        StringBuilder mensagemRecebida = new StringBuilder("CONFIRMADO");
        String primeiroNome = "Ana";
        String segundoNome = "Bruno";

        if (mensagemEsperada.contentEquals(mensagemRecebida)) {
            System.out.println("Mensagem válida");
        } else {
            System.out.println("Mensagem inválida");
        }

        int resultado = primeiroNome.compareTo(segundoNome);

        if (resultado < 0) {
            System.out.println("O primeiro nome vem antes");
        } else if (resultado == 0) {
            System.out.println("Os nomes são iguais");
        } else {
            System.out.println("O primeiro nome vem depois");
        }
    }
}
```

---

# 🔍 EXPLICAÇÃO DO DESAFIO EXTRA

Este desafio apresenta duas comparações muito comuns com texto.

### `contentEquals()`
`contentEquals()` compara o conteúdo de uma `String` com outra sequência de caracteres, como `StringBuilder`.

```java
String texto = "Java";
StringBuilder builder = new StringBuilder("Java");
boolean mesmoConteudo = texto.contentEquals(builder);
```

Se você usasse `equals()` nesse caso, o resultado seria `false`, porque os tipos dos objetos são diferentes.

### `compareTo()`
`compareTo()` informa a ordem lexicográfica entre dois textos.

- resultado menor que `0`: o primeiro texto vem antes.
- resultado igual a `0`: os textos são iguais.
- resultado maior que `0`: o primeiro texto vem depois.

### Pontos de atenção
- Não dependa de um valor específico como `-1` ou `1`; compare apenas com zero.
- `compareTo()` considera letras maiúsculas e minúsculas.
- `contentEquals()` é útil quando o outro lado não é exatamente uma `String`.

### Erros comuns
- Tentar comparar `StringBuilder` com `==`.
- Usar `equals()` entre `String` e `StringBuilder` esperando igualdade de conteúdo.

---

# 🎯 DESAFIO FINAL — Validação de Login

### Contexto
Um sistema precisa validar uma tentativa de login sem correr risco de erro quando algum texto vier nulo.

### Regras
1. O usuário só pode entrar se estiver ativo.
2. O perfil deve ser `"ADMIN"` ou `"OPERADOR"`.
3. O nome do usuário não pode ser `"GUEST"`.
4. A senha digitada deve ter o mesmo conteúdo da senha cadastrada.
5. As comparações textuais devem ser feitas de forma segura contra `null`.

### Dados de teste
- `usuarioAtivo = true`
- `perfil = "ADMIN"`
- `nomeUsuario = "marcelo"`
- `senhaCadastrada = "java21"`
- `senhaDigitada = "java21"`

### O que o aluno precisa fazer
Montar a validação do login usando `equals()` para comparar texto, sem usar `==` para `String`.

---

# 💡 SOLUÇÃO DO DESAFIO FINAL

```java
public class Main {
    public static void main(String[] args) {
        boolean usuarioAtivo = true;
        String perfil = "ADMIN";
        String nomeUsuario = "marcelo";
        String senhaCadastrada = "java21";
        String senhaDigitada = "java21";

        boolean perfilPermitido = "ADMIN".equals(perfil) || "OPERADOR".equals(perfil);
        boolean usuarioPermitido = !"GUEST".equals(nomeUsuario);
        boolean senhaCorreta = senhaCadastrada != null && senhaCadastrada.equals(senhaDigitada);
        boolean loginAutorizado = usuarioAtivo && perfilPermitido && usuarioPermitido && senhaCorreta;

        if (loginAutorizado) {
            System.out.println("Login autorizado");
        } else {
            System.out.println("Login negado");
        }
    }
}
```

---

# 🔍 EXPLICAÇÃO DO DESAFIO FINAL

Aqui entram `equals()`, segurança contra `null` e comparação de login.

### Por que usar `equals()` em `String`?
`String` é objeto. Para comparar o conteúdo textual, usamos `equals()`.

```java
String perfil = "ADMIN";
boolean perfilCorreto = "ADMIN".equals(perfil);
```

### Como evitar problema com `null`?
Se `perfil` ou `nomeUsuario` vierem nulos, chamar `perfil.equals("ADMIN")` pode causar `NullPointerException`.

Por isso, a forma mais segura é deixar o texto fixo à esquerda:

```java
boolean perfilPermitido = "ADMIN".equals(perfil) || "OPERADOR".equals(perfil);
boolean usuarioPermitido = !"GUEST".equals(nomeUsuario);
boolean senhaCorreta = senhaCadastrada != null && senhaCadastrada.equals(senhaDigitada);
```

### O que a validação final faz?
- Confirma que o usuário está ativo.
- Verifica se o perfil é aceito.
- Garante que o nome não seja `GUEST`.
- Compara a senha cadastrada com a senha digitada sem falhar caso a senha cadastrada esteja nula.

### Pontos de atenção
- Não use `==` para comparar `String` em login.
- A escrita segura contra `null` evita falhas em tempo de execução.
- Separar a regra em variáveis booleanas deixa o código mais legível.

### Erros comuns
- Escrever `perfil == "ADMIN"`.
- Chamar `.equals()` em uma variável que pode ser `null`.
- Misturar várias regras em uma linha sem nomes descritivos.
