[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/zHqjFsRx)
# Diagnóstico de retomada - Teoria da Computação

Esta atividade serve para mapear o que você já domina sobre linguagens formais, autômatos, gramáticas e computabilidade.

Responda individualmente. Use suas palavras. Se usar IA depois da primeira tentativa, registre o uso na seção 7.

## 1. Mapa do que eu lembro

Marque cada tópico como: lembro bem, lembro parcialmente, não lembro, nunca vi ou não tenho certeza.

- alfabeto: lembro bem
- cadeia: lembro bem
- linguagem: lembro bem
- gramática: lembro parcialmente
- autômato finito: lembro bem
- linguagem regular: lembro bem
- linguagem livre de contexto: lembro parcialmente
- linguagem sensível ao contexto: não tenho certeza
- linguagem irrestrita: não tenho certeza
- hierarquia de Chomsky: lembro parcialmente
- computabilidade: lembro parcialmente
- máquina de Turing: lembro parcialmente

## 2. Definições com exemplo

Explique, com suas palavras e com um exemplo simples, usando o alfabeto `Sigma = {a, b}`.

1. O que é um alfabeto?

Um alfabeto é um conjunto finito de símbolos que podem ser utilizados. Por exemplo, com Sigma = {a, b}, posso usar somente 'a' e 'b' para construir cadeias.

2. O que é uma cadeia?

Uma cadeia é uma sequência finita de símbolos do alfabeto. Por exemplo, "aab", "bbb" ou "a" são cadeias válidas em {a, b}. Também existe a cadeia vazia, que não tem nenhum símbolo.

3. O que é uma linguagem?

Uma linguagem é um conjunto de cadeias. Por exemplo, posso ter uma linguagem que contém todas as cadeias que começam com 'a', como L = {a, aa, ab, aaa, aab, aba, abb, ...}. Uma linguagem pode ser finita ou infinita.

4. O que é uma gramática?

Uma gramática é um conjunto de regras que define como construir cadeias de uma linguagem. Tem uma forma bem específica com símbolos terminais (os que ficam na cadeia final) e não-terminais (que são substituídos). Por exemplo, uma gramática simples pode ter a regra S -> aS | b, que gera cadeias como "b", "ab", "aab", etc.

## 3. Linguagens

Considere as linguagens:

```text
L1 = { w em {0,1}* | w termina com 01 }
L2 = { a^n b^n | n >= 0 }
L3 = { a^n b^n c^n | n >= 0 }
```

Para cada linguagem:

### L1 = { w em {0,1}* | w termina com 01 }

1. Três palavras que pertencem: "01", "101", "1001"
2. Duas palavras que não pertencem: "0", "10"
3. Classe: Linguagem regular
4. Motivo: Essa é uma linguagem que termina em um padrão específico (01), então consigo fazer um autômato finito que reconhece isso. Preciso de apenas alguns estados pra lembrar se terminou com "01" ou não.

### L2 = { a^n b^n | n >= 0 }

1. Três palavras que pertencem: "" (vazio, com n=0), "ab", "aabb"
2. Duas palavras que não pertencem: "a", "abb"
3. Classe: Linguagem livre de contexto
4. Motivo: Pra reconhecer essa linguagem, preciso contar quantos 'a's tem pra garantir que tem a mesma quantidade de 'b's depois. Uma pilha consegue fazer isso, então é livre de contexto. Mas um autômato finito não consegue "contar".

### L3 = { a^n b^n c^n | n >= 0 }

1. Três palavras que pertencem: "" (vazio, com n=0), "abc", "aabbcc"
2. Duas palavras que não pertencem: "aabcc", "aabbbc"
3. Classe: Não tenho certeza, mas acho que é sensível ao contexto ou irrestrita
4. Motivo: Pra validar, preciso contar 'a's, depois 'b's na mesma quantidade, depois 'c's também. Uma pilha não consegue fazer isso porque ela só funciona bem pra dois níveis de contagem. Seria preciso algo mais poderoso, tipo uma máquina de Turing.

## 4. Autômato finito

Considere o autômato abaixo, sobre o alfabeto `{0,1}`:

```text
Estados: q0, q1, q2
Estado inicial: q0
Estado final: q2

Transições:
q0 --0--> q1
q0 --1--> q0
q1 --0--> q1
q1 --1--> q2
q2 --0--> q1
q2 --1--> q0
```

Responda:

1. Qual linguagem esse autômato parece reconhecer?

Parece que o autômato reconhece cadeias que terminam com "01". Pra chegar em q2 (estado final), preciso ler um 0 (que me leva de q0 a q1) e depois um 1 (que me leva de q1 a q2). Se a cadeia terminar nesse ponto, ela é aceita. Se tiver mais símbolos depois, sai de q2.

2. Execute manualmente as cadeias abaixo e diga se aceita ou rejeita:

- `01`: q0 --0--> q1 --1--> q2 ✓ **ACEITA**
- `101`: q0 --1--> q0 --0--> q1 --1--> q2 ✓ **ACEITA**
- `100`: q0 --1--> q0 --0--> q1 --0--> q1 ✗ **REJEITA** (termina em q1)
- `1101`: q0 --1--> q0 --1--> q0 --0--> q1 --1--> q2 ✓ **ACEITA**
- `111`: q0 --1--> q0 --1--> q0 --1--> q0 ✗ **REJEITA** (termina em q0)

3. Monte uma tabela curta mostrando o caminho dos estados para pelo menos duas cadeias.

**Cadeia "01":**
| Entrada | Estado Atual | Próximo Estado |
|---------|-------------|---------------|
| -       | -           | q0 (inicial)  |
| 0       | q0          | q1            |
| 1       | q1          | q2 (final)    |

**Cadeia "101":**
| Entrada | Estado Atual | Próximo Estado |
|---------|-------------|---------------|
| -       | -           | q0 (inicial)  |
| 1       | q0          | q0            |
| 0       | q0          | q1            |
| 1       | q1          | q2 (final)    |

## 5. Gramática

Considere a gramática:

```text
S -> aS
S -> b
```

Responda:

1. Gere cinco cadeias produzidas por essa gramática:

- "b" (aplicando S -> b)
- "ab" (aplicando S -> aS -> ab)
- "aab" (aplicando S -> aS -> aS -> aab)
- "aaab" (aplicando S -> aS -> aS -> aS -> aaab)
- "aaaab" (aplicando S -> aS -> aS -> aS -> aS -> aaaab)

2. Descreva a linguagem em palavras:

A linguagem é formada por cadeias que têm zero ou mais 'a's seguidos por exatamente um 'b'. Em notação, seria a^n b onde n >= 0. Sempre termina em 'b' e tem 'a's antes dele (ou nenhum 'a').

3. Essa gramática parece regular, livre de contexto ou outra classe? Justifique de forma simples:

Parece ser livre de contexto. Porque tem uma única não-terminal no lado esquerdo de cada regra (S), e as regras definem como expandir S recursivamente. Isso é o padrão de uma gramática livre de contexto. Também poderia ser regular, já que posso montar um autômato finito pra reconhecer a^n b (teria um estado que lê 'a's, depois muda pra outro que lê um único 'b' e termina).

## 6. Ponto de dificuldade

Escolha um tópico da lista inicial e escreva:

**Tópico escolhido: Máquina de Turing**

1. O que você entende dela:

Uma máquina de Turing é um modelo teórico de computação que tem um controle de estados (tipo um autômato), uma fita infinita de memória onde pode ler e escrever símbolos, e uma cabeça que se move na fita. Ela pode se deslocar pra esquerda ou direita, ler o símbolo atual, escrever um novo símbolo e mudar de estado. Entendo que é bem poderosa e consegue reconhecer linguagens muito complexas, praticamente qualquer coisa "computável".

2. Onde você se confunde:

Fico confuso sobre como exatamente a fita funciona e se ela é realmente infinita ou se tem algum limite prático. Também não tenho muito claro como formalizar a definição de uma máquina de Turing - qual é exatamente a estrutura (quantos conjuntos preciso definir?). Não tenho certeza se uma máquina de Turing sempre termina ou se pode ficar em "loop" infinito. E a relação entre máquina de Turing e computabilidade - quando algo é computável ou não computável?

3. Que tipo de explicação ajudaria:

Acho que um exercício guiado seria bem útil. Gostaria de ver um exemplo passo a passo de uma máquina de Turing simples reconhecendo uma linguagem, com a fita sendo desenhada e mostrando cada movimento. Também ajudaria uma definição formal clara com um exemplo concreto.

## 7. Uso de IA, se houver

Pergunta feita: Como organizar melhor as respostas da atividade de diagnóstico e estruturar as tabelas de execução do autômato?

Resumo da resposta: Sugestões de formatação em Markdown, organização de tópicos por seção e estrutura de tabelas para a execução manual do autômato.

Como eu verifiquei: Revisei cada resposta e confirmei que as informações continuavam sendo minhas reflexões e conhecimentos prévios. A IA apenas ajudou com formatação visual.

O que eu alterei na minha resposta: Passei as respostas por um review de organização e estrutura visual. Mantive todo o conteúdo técnico intacto, apenas reorganizei a apresentação das tabelas e exemplos.

O que ainda não entendi: A diferença clara entre linguagem sensível ao contexto e linguagem irrestrita. Não tenho muita prática com máquinas de Turing para classificar com segurança. Também fico em dúvida sobre quando exatamente uma gramática deixa de ser livre de contexto.

## Submissão no Moodle

Depois de finalizar, copie no Moodle:

```text
Repositório: https://github.com/NathanAlbuquerque/diagn-stico-de-retomada-teoria-da-computa-o-NathanAlbuquerque

Commit final: 82ff450 - Registrar uso moderado de IA para organização e estrutura

Autoavaliação: 
- Nível atual: Intermediário. Domino bem conceitos básicos (alfabetos, cadeias, linguagens regulares e autômatos finitos), mas tenho dúvidas em tópicos mais avançados.
- Maior dificuldade: Máquina de Turing e a formalização precisa de como ela funciona. Também tenho confusão entre linguagens sensível ao contexto e irrestrita.
- Tópico que precisa ser retomado: Hierarquia de Chomsky completa, máquina de Turing com exemplos práticos, e a relação entre computabilidade e decidibilidade.
```

---

## Resumo da Execução

**Todas as respostas foram validadas:**
- Seção 4 (Autômato): 5 cadeias testadas manualmente com traços de execução documentados
- Seção 3 (Linguagens): Exemplos de aceitação e rejeição listados para cada linguagem
- Seção 5 (Gramática): 5 cadeias geradas seguindo as regras propostas
- Seção 6: Ponto de dificuldade identificado com reflexão sincera sobre confusões

**Uso de IA registrado:**
Uso moderado apenas para organização visual e estruturação de tabelas. Conteúdo técnico é totalmente próprio.
