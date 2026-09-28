# Treinamento Java 21 — Nível Básico

Bem-vindo ao material do **Treinamento Java 21 — Nível Básico**! Este curso foi desenhado para quem está dando os primeiros passos na linguagem Java, utilizando uma abordagem prática, incremental e didática.

---

## 🎯 Metodologia

O treinamento adota a seguinte metodologia em todos os módulos:

$$\text{Desafio} \longrightarrow \text{Solução} \longrightarrow \text{Explicação} \longrightarrow \text{Evolução}$$

1. **Desafio:** Apresentação de um problema real/prático com regras claras.
2. **Solução:** Apresentação da implementação em código Java simples e legível.
3. **Explicação:** Detalhamento do funcionamento dos conceitos, com exemplos, erros comuns e dicas de *Clean Code*.
4. **Evolução:** Ampliação do desafio para solidificar a aprendizagem.

---

## 📂 Arquivos do Treinamento

| Arquivo | Descrição |
| :--- | :--- |
| `00-template.md` | Template base reutilizável para criação de novas aulas em Marp |
| `01-variaveis.md` | Tipos primitivos, String, modificadores (`public`, `private`, `final`) e imutabilidade |
| `02-if.md` | Controle de fluxo, operadores relacionais e lógicos, booleanos e *Clean Code* |
| `03-comparacoes.md` | Diferenças conceituais e práticas entre `==`, `equals()`, `contentEquals()` e `compareTo()` |
| `04-roadmap.md` | Visão geral da jornada de aprendizado do básico até o avançado |

---

## 💻 Apresentação com Marp

Todos os arquivos `.md` contêm o cabeçalho (*front matter*) necessário para renderização em slides utilizando o **Marp**:

```yaml
---
marp: true
theme: default
paginate: true
---
```

Você pode visualizar e exportar os slides instalando a extensão **Marp for VS Code** ou utilizando a **Marp CLI**.

---

## ⚠️ Nota Importante sobre a Didática

Para não sobrecarregar quem está iniciando, os primeiros módulos **NÃO** apresentam os seguintes conceitos:
- Palavra-chave `this`
- Palavra-chave `static`
- Construtores
- Getters / Setters
- Conceitos avançados de Orientação a Objetos (Herança, Polimorfismo)

Esses tópicos serão introduzidos gradualmente no momento oportuno, após o aluno consolidar os fundamentos de variáveis, tipos e estruturas condicionais.