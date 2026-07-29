---
layout: cover
---

# Pares e Listas

---
layout: statement
---

# Pares

---

# Pares

<br>

Um **par** agrupa dois termos em uma única função — que os entrega ao seletor que receber:

$$\text{PAIR} \equiv \lambda x.\ \lambda y.\ \lambda s.\ ((s\ x)\ y)$$

<div class="text-gray-600 text-sm text-center mt-2">

$x$ — primeiro elemento $\quad$ $y$ — segundo elemento $\quad$ $s$ — seletor

</div>

<div class="flex gap-12 mt-8">

<div class="flex-1">

$$\text{FST} \equiv \lambda p.\ (p\ \text{TRUE})$$

<div class="text-gray-600 text-sm mt-2 text-center">
seleciona o primeiro elemento
</div>

</div>

<div class="flex-1">

$$\text{SND} \equiv \lambda p.\ (p\ \text{FALSE})$$

<div class="text-gray-600 text-sm mt-2 text-center">
seleciona o segundo elemento
</div>

</div>

</div>

<div class="mt-8">

> PAIR usa TRUE e FALSE como seletores — conectando diretamente
> com o Bloco 3.

</div>

---

# Pares — Verificação

<br>

<div class="flex gap-12 mt-4">

<div class="flex-1">

$$
\begin{aligned}
&\text{FST}\ ((\text{PAIR}\ M)\ N) \\
&\equiv \text{FST}\ (((\lambda x.\ \lambda y.\ \lambda s.\ ((s\ x)\ y))\ M)\ N) \\
&\xrightarrow{\beta} \text{FST}\ ((\lambda y.\ \lambda s.\ ((s\ M)\ y))\ N) \\
&\xrightarrow{\beta} \text{FST}\ (\lambda s.\ ((s\ M)\ N)) \\
&\equiv (\lambda p.\ (p\ \text{TRUE}))\ (\lambda s.\ ((s\ M)\ N)) \\
&\xrightarrow{\beta} (\lambda s.\ ((s\ M)\ N))\ \text{TRUE} \\
&\xrightarrow{\beta} ((\text{TRUE}\ M)\ N) \\
&\xrightarrow{\beta} M
\end{aligned}
$$

</div>

<div class="flex-1">

$$
\begin{aligned}
&\text{SND}\ ((\text{PAIR}\ M)\ N) \\
&\equiv \text{SND}\ (((\lambda x.\ \lambda y.\ \lambda s.\ ((s\ x)\ y))\ M)\ N) \\
&\xrightarrow{\beta} \text{SND}\ ((\lambda y.\ \lambda s.\ ((s\ M)\ y))\ N) \\
&\xrightarrow{\beta} \text{SND}\ (\lambda s.\ ((s\ M)\ N)) \\
&\equiv (\lambda p.\ (p\ \text{FALSE}))\ (\lambda s.\ ((s\ M)\ N)) \\
&\xrightarrow{\beta} (\lambda s.\ ((s\ M)\ N))\ \text{FALSE} \\
&\xrightarrow{\beta} ((\text{FALSE}\ M)\ N) \\
&\xrightarrow{\beta} N
\end{aligned}
$$

</div>

</div>

<div class="mt-6 text-gray-600 text-sm">

TRUE seleciona o primeiro — FALSE seleciona o segundo. O mesmo mecanismo de seletor que usamos nos booleanos.

</div>

---

# Exercícios de Fixação

<br>

**1.** Avalie passo a passo a partir da definição:

<div class="flex gap-8 mt-4">

<div class="flex-1">

$$\text{(a)}\ \text{FST}\ ((\text{PAIR}\ \overline{1})\ \overline{2})$$

</div>

<div class="flex-1">

$$\text{(b)}\ \text{SND}\ ((\text{PAIR}\ \overline{1})\ \overline{2})$$

</div>

</div>

<br>

**2.** Verdadeiro ou falso? Justifique:

*"$\text{FST}\ ((\text{PAIR}\ M)\ N) \equiv \text{SND}\ ((\text{PAIR}\ N)\ M)$"*


---
layout: statement
---

# Listas Simplesmente Encadeadas

---

# Listas Simplesmente Encadeadas

<br>

Uma lista é definida recursivamente como:

<div class="mt-6">

- **NIL** — a lista vazia (caso base)
- **CONS H T** — um par com cabeça $H$ e cauda $T$, onde $T$ é uma lista

</div>

<div class="mt-8">

$$\text{NIL} \equiv \lambda x.\ x$$

$$\text{CONS} \equiv \lambda h.\ \lambda t.\ \lambda s.\ ((s\ h)\ t)$$

<div class="text-gray-600 text-sm text-center mt-2">

$h$ — cabeça (head) $\quad$ $t$ — cauda (tail) $\quad$ $s$ — seletor

</div>

</div>

<div class="mt-8">

$$\text{HEAD} \equiv \lambda l.\ (l\ \text{TRUE})$$

$$\text{TAIL} \equiv \lambda l.\ (l\ \text{FALSE})$$

</div>

---

# PAIR e CONS — Mesma Estrutura, Semânticas Distintas

<br>

CONS e PAIR compartilham a mesma estrutura lambda interna:

$$\text{PAIR} \equiv \lambda x.\ \lambda y.\ \lambda s.\ ((s\ x)\ y)$$
$$\text{CONS} \equiv \lambda h.\ \lambda t.\ \lambda s.\ ((s\ h)\ t)$$

<div class="mt-8">

A diferença está na **semântica**:

- **PAIR** — agrupa dois termos quaisquer, sem restrições
- **CONS** — a cauda $t$ deve sempre ser uma lista, terminando em NIL

</div>

<div class="mt-8 text-gray-600 text-sm">

Essa distinção aparece diretamente em Elixir — o operador
`[head | tail]` em pattern matching corresponde exatamente a CONS:
a cauda deve ser sempre uma lista.

</div>

---

# Construindo uma Lista

<br>

A lista $[1, 2, 3]$ é construída aninhando CONS a partir do NIL:

$$(\text{CONS}\ \overline{1}\ (\text{CONS}\ \overline{2}\ (\text{CONS}\ \overline{3}\ \text{NIL})))$$

<div class="mt-8 text-gray-600 text-sm text-center">

Leitura: $\overline{1}$ na cabeça, $(\text{CONS}\ \overline{2}\ (\text{CONS}\ \overline{3}\ \text{NIL}))$ na cauda.

</div>

<div class="mt-8">

**Selecionando elementos:**

<div class="flex gap-12 mt-4">

<div class="flex-1">

$$\text{HEAD}\ (\text{CONS}\ \overline{1}\ (\text{CONS}\ \overline{2}\ \text{NIL})) \xrightarrow{\beta} \overline{1}$$

<div class="text-gray-600 text-sm mt-2 text-center">
seleciona a cabeça
</div>

</div>

<div class="flex-1">

$$\text{TAIL}\ (\text{CONS}\ \overline{1}\ (\text{CONS}\ \overline{2}\ \text{NIL})) \xrightarrow{\beta} \text{CONS}\ \overline{2}\ \text{NIL}$$

<div class="text-gray-600 text-sm mt-2 text-center">
seleciona a cauda
</div>

</div>

</div>

</div>

---

# Exercícios de Fixação

<br>

**1.** Construa as seguintes listas usando CONS e NIL:

<div class="flex gap-8 mt-4">

<div class="flex-1">

$$\text{(a)}\ [\overline{1}]$$

$$\text{(b)}\ [\overline{1},\ \overline{2},\ \overline{3}]$$

</div>

<div class="flex-1">

$$\text{(c)}\ \text{HEAD}\ (\text{CONS}\ \overline{1}\ (\text{CONS}\ \overline{2}\ \text{NIL}))$$

$$\text{(d)}\ \text{TAIL}\ (\text{CONS}\ \overline{1}\ (\text{CONS}\ \overline{2}\ \text{NIL}))$$

</div>

</div>

<br>

**2.** Verdadeiro ou falso? Justifique:

*"$\text{HEAD}\ \text{NIL}$ produz um resultado válido."*

---
layout: image
image: images/emily-morter.jpg
---