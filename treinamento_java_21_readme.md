# Treinamento Java 21 — Nível Básico

Bem-vindo ao material do **Treinamento Java 21 — Nível Básico**! Este curso foi desenhado para quem está dando os primeiros passos na linguagem Java, utilizando uma abordagem prática, incremental e didática.

---

## 🎯 Metodologia

Todos os módulos devem seguir a mesma sequência pedagógica:

1. **Desafio 1:** apresenta apenas o contexto, as regras, os dados de teste e o que o aluno precisa fazer.
2. **Solução 1:** apresenta a implementação do Desafio 1.
3. **Explicação do Desafio 1:** detalha a solução, com avisos, erros comuns e pontos de atenção.
4. **Desafio Extra:** propõe um novo exercício para consolidar o aprendizado, apenas com o enunciado.
5. **Solução do Desafio Extra:** apresenta a implementação do desafio extra.
6. **Explicação do Desafio Extra:** detalha a solução, com avisos e pontos de atenção.
7. **Desafio Final:** aparece somente quando o módulo trabalha mais de um conceito e precisa integrar o conteúdo estudado.
8. **Solução do Desafio Final:** apresenta a implementação completa do desafio final.
9. **Explicação do Desafio Final:** analisa a solução final e reforça os cuidados importantes.

### Regras de padronização

- Não incluir seções de **Evolução**.
- Não incluir seções de **Próximos Passos**.
- Não antecipar explicações antes do respectivo **Desafio 1**.
- Preferir os títulos:
  - `🎯 DESAFIO 1`
  - `💡 SOLUÇÃO 1`
  - `🔍 EXPLICAÇÃO DO DESAFIO 1`
  - `🎯 DESAFIO EXTRA`
  - `💡 SOLUÇÃO DO DESAFIO EXTRA`
  - `🔍 EXPLICAÇÃO DO DESAFIO EXTRA`
  - `🎯 DESAFIO FINAL`
  - `💡 SOLUÇÃO DO DESAFIO FINAL`
  - `🔍 EXPLICAÇÃO DO DESAFIO FINAL`

---

## 📂 Arquivos do Treinamento

| Arquivo | Descrição |
| :--- | :--- |
| `template_de_slide_marp.md` | Template base reutilizável para criação de novas aulas em Marp |
| `modulo_01_variaveis_e_tipos.md` | Tipos, declaração de variáveis, `final` e incompatibilidade de tipos |
| `modulo_02_condicoes.md` | Condições, operadores relacionais e operadores lógicos |
| `m_dulo_03_compara_es.md` | Comparações com `==`, `equals()`, `contentEquals()` e `compareTo()` |
| `roadmap_do_treinamento.md` | Visão geral da jornada de aprendizado do básico até o avançado |

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
