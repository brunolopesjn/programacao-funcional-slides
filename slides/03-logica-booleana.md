---
layout: cover
---

# Lógica Booleana em Cálculo Lambda

---
layout: statement
---

# Valores Booleanos

---

# Valores Booleanos

<br>

Em cálculo lambda não existem valores booleanos primitivos.
TRUE e FALSE são **convenções metalinguísticas** — funções que se comportam como seletores:

<div class="flex gap-12 mt-8">

<div class="flex-1">

$$\text{TRUE} \equiv \lambda first.\ \lambda second.\ first$$

<div class="text-center text-sm text-gray-600 mt-2">
seleciona o primeiro argumento
</div>

</div>

<div class="flex-1">

$$\text{FALSE} \equiv \lambda first.\ \lambda second.\ second$$

<div class="text-center text-sm text-gray-600 mt-2">
seleciona o segundo argumento
</div>

</div>

</div>

<div class="mt-10">

> TRUE e FALSE não são termos internos ao cálculo lambda —
> são nomes que damos a funções para facilitar o raciocínio.

</div>

---

# Exercícios e Fixação
Valores Booleanos

**1.** Avalie as expressões abaixo passo a passo, expandindo TRUE e FALSE para suas definições como seletores:

<div class="flex gap-8 mt-4">

<div class="flex-1">

$$\text{(a)}\ ((\text{TRUE}\ M)\ N)$$

$$\text{(b)}\ ((\text{FALSE}\ M)\ N)$$

</div>

<div class="flex-1">

$$\text{(c)}\ ((\text{TRUE}\ \text{FALSE})\ \text{TRUE})$$

$$\text{(d)}\ ((\text{FALSE}\ \text{TRUE})\ \text{FALSE})$$

</div>

</div>

<br>

**2.** Verdadeiro ou falso? Justifique:

*"TRUE e FALSE são termos primitivos do cálculo lambda — assim como variáveis e abstrações."*

---
layout: statement
---

# Expressão Condicional

---

# Expressão Condicional

<br>

A expressão condicional seleciona entre duas expressões com base em uma condição:

$$\text{COND} \equiv \lambda e_1.\ \lambda e_2.\ \lambda c.\ ((c\ e_1)\ e_2)$$

<div class="mt-6 text-gray-600 text-sm text-center">

$e_1$ — expressão caso verdadeiro $\quad$ $e_2$ — expressão caso falso $\quad$ $c$ — condição

</div>

<div class="mt-8">

Aplicando COND a duas expressões e depois a TRUE:

$$
\begin{aligned}
&((\text{COND}\ M)\ N)\ \text{TRUE} \\
&\xrightarrow{\beta} (\lambda c.\ ((c\ M)\ N))\ \text{TRUE} \\
&\xrightarrow{\beta} ((\text{TRUE}\ M)\ N) \\
&\xrightarrow{\beta} M
\end{aligned}
$$

</div>

<div class="mt-6 text-gray-600 text-sm">

Se a condição for FALSE, o resultado será $N$ — pois FALSE seleciona o segundo argumento.

</div>

---

# Notação IF/THEN/ELSE

<br>

A notação **if/then/else** é uma forma simplificada de escrever COND,
introduzida para tornar as expressões mais legíveis:

$$
\text{if}\ c\ \text{then}\ e_1\ \text{else}\ e_2 \equiv \text{COND}\ e_1\ e_2\ c
$$

<div class="mt-8 text-gray-600 text-sm">

Note a inversão da ordem: em COND a condição é o último argumento; em if/then/else ela aparece primeiro — como na linguagem natural.

</div>

<div class="mt-8">

A partir daqui, usaremos a notação if/then/else como abreviação:

$$\text{NOT} \equiv \lambda x.\ \text{if}\ x\ \text{then}\ \text{FALSE}\ \text{else}\ \text{TRUE}$$

<div class="text-center">que seria o equivalente a:</div>

$$\text{NOT} \equiv \lambda x.\ \text{COND}\ \text{FALSE}\ \text{TRUE}\ x$$

</div>

---

# Exercícios de Fixação
Expressão Condicional

<br>

**1.** Avalie passo a passo:

<div class="flex gap-8 mt-4">

<div class="flex-1">

$$\text{(a)}\ ((\text{COND}\ M)\ N)\ \text{TRUE}$$

$$\text{(b)}\ ((\text{COND}\ M)\ N)\ \text{FALSE}$$

</div>

<div class="flex-1">

$$\text{(c)}\ ((\text{COND}\ \text{TRUE})\ \text{FALSE})\ \text{TRUE}$$

$$\text{(d)}\ ((\text{COND}\ \text{TRUE})\ \text{FALSE})\ \text{FALSE}$$

</div>

</div>

<br>

**2.** Reescreva as expressões abaixo usando a notação IF/THEN/ELSE:

<div class="flex gap-8 mt-4">

<div class="flex-1">

$$\text{(a)}\ ((\text{COND}\ M)\ N)\ c$$

</div>

<div class="flex-1">

$$\text{(b)}\ ((\text{COND}\ \text{FALSE})\ \text{TRUE})\ x$$

</div>

</div>

<br>

**3.** Verdadeiro ou falso? Justifique:

*"Em COND, a condição é o primeiro argumento."*

---
layout: statement
---

# Operador NOT

---

# NOT

<br>

NOT é um operador unário — inverte o valor booleano do operando:

<div class="flex gap-12 mt-6">

<div class="flex-1">

| $x$ | $\text{NOT}\ x$ |
|-----|-----------------|
| FALSE | TRUE |
| TRUE | FALSE |

</div>

<div class="flex-1">

$$\text{NOT} \equiv \lambda x.\ ((x\ \text{FALSE})\ \text{TRUE})$$

<div class="text-gray-600 text-sm mt-2">

Se $x$ for TRUE, seleciona o primeiro argumento (FALSE).<br>
Se $x$ for FALSE, seleciona o segundo argumento (TRUE).

</div>

</div>

</div>

---

# NOT — Verificação

<br>

<div class="flex gap-12 mt-4">

<div class="flex-1">

**NOT TRUE**

$$
\begin{aligned}
&(\lambda x.\ ((x\ \text{FALSE})\ \text{TRUE}))\ \text{TRUE} \\
&\xrightarrow{\beta} ((\text{TRUE}\ \text{FALSE})\ \text{TRUE}) \\
&\equiv ((\lambda f.\ \lambda s.\ f)\ \text{FALSE})\ \text{TRUE}) \\
&\xrightarrow{\beta} (\lambda s.\ \text{FALSE})\ \text{TRUE} \\
&\xrightarrow{\beta} \text{FALSE}
\end{aligned}
$$

</div>

<div class="flex-1">

**NOT FALSE**

$$
\begin{aligned}
&(\lambda x.\ ((x\ \text{FALSE})\ \text{TRUE}))\ \text{FALSE} \\
&\xrightarrow{\beta} ((\text{FALSE}\ \text{FALSE})\ \text{TRUE}) \\
&\equiv ((\lambda f.\ \lambda s.\ s)\ \text{FALSE})\ \text{TRUE}) \\
&\xrightarrow{\beta} (\lambda s.\ s)\ \text{TRUE} \\
&\xrightarrow{\beta} \text{TRUE}
\end{aligned}
$$

</div>

</div>

<div class="text-gray-600 text-sm mt-6">

Os resultados correspondem à tabela verdade.

</div>

---

# NOT — Formas Equivalentes

<br>

As três formas abaixo são equivalentes — apenas níveis diferentes de abstração:

<div class="mt-8">

**Usando COND:**
$$\text{NOT} \equiv \lambda x.\ (((\text{COND}\ \text{FALSE})\ \text{TRUE})\ x)$$

</div>

<div class="mt-6">

**Simplificada** *(expandindo e reduzindo COND)*:
$$\text{NOT} \equiv \lambda x.\ ((x\ \text{FALSE})\ \text{TRUE})$$

</div>

<div class="mt-6">

**Usando IF/THEN/ELSE** *(notação abreviada)*:
$$\text{NOT} \equiv \lambda x.\ \text{if}\ x\ \text{then}\ \text{FALSE}\ \text{else}\ \text{TRUE}$$

</div>

<div class="mt-8 text-gray-600 text-sm">

Nos próximos operadores, apresentaremos sempre a forma simplificada —
que é a que será usada nas reduções. As outras formas são equivalentes e
podem ser usadas conforme o contexto.

</div>

---

# Exercícios de Fixação
Operador NOT

**1.** Avalie passo a passo:

<div class="flex gap-8 mt-4">

<div class="flex-1">

$$\text{(a)}\ \text{NOT}\ \text{FALSE}$$

</div>

<div class="flex-1">

$$\text{(b)}\ \text{NOT}\ (\text{NOT}\ \text{TRUE})$$

</div>

</div>

<br>

**2.** Verdadeiro ou falso? Justifique:

*"$\text{NOT}\ (\text{NOT}\ x) \equiv x$ para qualquer valor booleano de $x$."*

---
layout: statement
---

# Operador AND

---

# AND

<br>

AND é um operador binário — retorna TRUE apenas quando ambos os operandos são TRUE:

<div class="flex gap-12 mt-6">

<div class="flex-1">

| $x$ | $y$ | $x\ \text{AND}\ y$ |
|-----|-----|---------------------|
| FALSE | FALSE | FALSE |
| FALSE | TRUE | FALSE |
| TRUE | FALSE | FALSE |
| TRUE | TRUE | TRUE |

</div>

<div class="flex-1">

$$\text{AND} \equiv \lambda x.\ \lambda y.\ ((x\ y)\ \text{FALSE})$$

<div class="text-gray-600 text-sm mt-4">

Se $x$ for TRUE, seleciona $y$ — o resultado depende do segundo operando.<br>
Se $x$ for FALSE, seleciona FALSE — independente de $y$.

</div>

</div>

</div>

---

# AND — Verificação

<br>

<div class="flex gap-12 mt-4">

<div class="flex-1">

**TRUE AND FALSE**

$$
\begin{aligned}
&((\text{AND}\ \text{TRUE})\ \text{FALSE}) \\
&\xrightarrow{\beta} ((\text{TRUE}\ \text{FALSE})\ \text{FALSE}) \\
&\equiv ((\lambda f.\ \lambda s.\ f)\ \text{FALSE})\ \text{FALSE}) \\
&\xrightarrow{\beta} (\lambda s.\ \text{FALSE})\ \text{FALSE} \\
&\xrightarrow{\beta} \text{FALSE}
\end{aligned}
$$

</div>

<div class="flex-1">

**TRUE AND TRUE**

$$
\begin{aligned}
&((\text{AND}\ \text{TRUE})\ \text{TRUE}) \\
&\xrightarrow{\beta} ((\text{TRUE}\ \text{TRUE})\ \text{FALSE}) \\
&\equiv ((\lambda f.\ \lambda s.\ f)\ \text{TRUE})\ \text{FALSE}) \\
&\xrightarrow{\beta} (\lambda s.\ \text{TRUE})\ \text{FALSE} \\
&\xrightarrow{\beta} \text{TRUE}
\end{aligned}
$$

</div>

</div>

<div class="text-gray-600 text-sm mt-6">

Os resultados correspondem à tabela verdade.

</div>

---

# Exercícios de Fixação
Operador AND

**1.** Avalie passo a passo:

<div class="flex gap-8 mt-4">

<div class="flex-1">

$$\text{(a)}\ \text{AND}\ \text{FALSE}\ \text{TRUE}$$

</div>

<div class="flex-1">

$$\text{(b)}\ \text{AND}\ \text{TRUE}\ (\text{NOT}\ \text{FALSE})$$

</div>

</div>

<br>

**2.** Verdadeiro ou falso? Justifique:

*"$\text{AND}\ x\ y \equiv \text{AND}\ y\ x$ para quaisquer valores booleanos de $x$ e $y$."*

---
layout: statement
---

# Operador OR

---

# OR

<br>

OR é um operador binário — retorna TRUE quando pelo menos um dos operandos é TRUE:

<div class="flex gap-12 mt-6">

<div class="flex-1">

| $x$ | $y$ | $x\ \text{OR}\ y$ |
|-----|-----|-------------------|
| FALSE | FALSE | FALSE |
| FALSE | TRUE | TRUE |
| TRUE | FALSE | TRUE |
| TRUE | TRUE | TRUE |

</div>

<div class="flex-1">

$$\text{OR} \equiv \lambda x.\ \lambda y.\ ((x\ \text{TRUE})\ y)$$

<div class="text-gray-600 text-sm mt-4">

Se $x$ for TRUE, seleciona TRUE — independente de $y$.<br>
Se $x$ for FALSE, seleciona $y$ — o resultado depende do segundo operando.

</div>

</div>

</div>

---

# OR — Verificação

<br>

<div class="flex gap-12 mt-4">

<div class="flex-1">

**FALSE OR TRUE**

$$
\begin{aligned}
&((\text{OR}\ \text{FALSE})\ \text{TRUE}) \\
&\xrightarrow{\beta} ((\text{FALSE}\ \text{TRUE})\ \text{TRUE}) \\
&\equiv ((\lambda f.\ \lambda s.\ s)\ \text{TRUE})\ \text{TRUE}) \\
&\xrightarrow{\beta} (\lambda s.\ s)\ \text{TRUE} \\
&\xrightarrow{\beta} \text{TRUE}
\end{aligned}
$$

</div>

<div class="flex-1">

**FALSE OR FALSE**

$$
\begin{aligned}
&((\text{OR}\ \text{FALSE})\ \text{FALSE}) \\
&\xrightarrow{\beta} ((\text{FALSE}\ \text{TRUE})\ \text{FALSE}) \\
&\equiv ((\lambda f.\ \lambda s.\ s)\ \text{TRUE})\ \text{FALSE}) \\
&\xrightarrow{\beta} (\lambda s.\ s)\ \text{FALSE} \\
&\xrightarrow{\beta} \text{FALSE}
\end{aligned}
$$

</div>

</div>

<div class="text-gray-600 text-sm mt-6">

Os resultados correspondem à tabela verdade.

</div>

---

# Exercícios de Fixação
Operador OR

**1.** Avalie passo a passo:

<div class="flex gap-8 mt-4">

<div class="flex-1">

$$\text{(a)}\ \text{OR}\ \text{TRUE}\ \text{FALSE}$$

</div>

<div class="flex-1">

$$\text{(b)}\ \text{OR}\ \text{FALSE}\ (\text{AND}\ \text{TRUE}\ \text{FALSE})$$

</div>

</div>

<br>

**2.** Verdadeiro ou falso? Justifique:

*"$\text{OR}\ x\ y \equiv \text{OR}\ y\ x$ para quaisquer valores booleanos de $x$ e $y$."*

---
layout: image
image: images/emily-morter.jpg
---