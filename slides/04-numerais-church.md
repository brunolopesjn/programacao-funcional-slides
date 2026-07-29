---
layout: cover
---

# Numerais de Church

---
layout: statement
---

# Representando Números com Funções

---

# Representando Números como Funções

<br>

Em cálculo lambda não existem números primitivos. Os números naturais são representados através de funções — os **Numerais de Church**.

A ideia central: um número natural $n$ é representado como **a aplicação de uma função $n$ vezes a um argumento**:

<div class="mt-8">

| Número | Representação intuitiva |
|--------|------------------------|
| $0$ | aplicar $f$ **zero** vezes a $x$ |
| $1$ | aplicar $f$ **uma** vez a $x$ |
| $2$ | aplicar $f$ **duas** vezes a $x$ |
| $n$ | aplicar $f$ **$n$** vezes a $x$ |

</div>

---

# A Abordagem Usada no Curso

<br>

Os números naturais são representados como **funções que iteram outra função** — seguindo a representação clássica dos Numerais de Church.

<br>

Dois elementos fundamentais:

- **$\overline{0}$** — o ponto de partida: não aplica $f$ nenhuma vez
- **SUCC** — a função que constrói o próximo numeral aplicando $f$ uma vez a mais

<div class="mt-8 text-gray-600 text-sm">

Todo número natural é definido pelo número de vezes
que $f$ é aplicada a $x$.

</div>

---
layout: statement
---

# A Notação $\overline{n}$

---

# A Notação $\overline{n}$

<br>

No cálculo lambda não existem números — apenas termos.

Para distinguir o número matemático do termo lambda que o representa,
usamos a notação com barra:

<div class="mt-8">

| Notação | Significado |
|---------|-------------|
| $n$ | o número natural da aritmética |
| $\overline{n}$ | o **termo lambda** que representa esse número |

</div>

---

# A Notação $\overline{n}$ — Exemplo

<br>

$$2 \quad \text{é o número dois da matemática}$$

<div class="mt-6">

$$\overline{2} \equiv \lambda f.\ \lambda x.\ (f\ (f\ x))$$

</div>

<div class="text-gray-600 text-sm mt-2 text-center">
o termo lambda que <em>representa</em> o dois
</div>

<div class="mt-10">

> Sempre que escrevermos $\overline{n}$, estamos nos referindo
> ao encoding funcional do número — não ao número em si.

</div>

---
layout: statement
---

# Numerais de Church

---

# Numerais de Church 

<br>

<div class="flex gap-12 mt-6">

<div class="flex-1">

$$\overline{0} \equiv \lambda f.\ \lambda x.\ x$$

<div class="text-gray-600 text-center text-sm mt-2">

Zero — $f$ é aplicada zero vezes a $x$.

</div>

$$\overline{1} \equiv \lambda f.\ \lambda x.\ (f\ x)$$

<div class="text-gray-600 text-center text-sm mt-2">

Um — $f$ é aplicada uma vez a $x$.

</div>

</div>

<div class="flex-1">

$$\overline{2} \equiv \lambda f.\ \lambda x.\ (f\ (f\ x))$$

<div class="text-gray-600 text-center text-sm mt-2">

Dois — $f$ é aplicada duas vezes a $x$.

</div>

$$\overline{n} \equiv \lambda f.\ \lambda x.\ f^n\ x$$

<div class="text-gray-600 text-center text-sm mt-2">

$n$ — $f$ é aplicada $n$ vezes a $x$.

</div>

</div>

</div>

<div class="mt-8">

> O número $n$ representa **quantas vezes** a função $f$ é aplicada ao argumento $x$.

</div>

---

# Exercícios de Fixação
Numerais de Church

**1.** Escreva os seguintes numerais de Church em notação lambda:

<div class="flex gap-8 mt-4">

<div class="flex-1">

$$\text{(a)}\ \overline{3} \qquad \text{(b)}\ \overline{4}$$

</div>

<div class="flex-1">

$$\text{(c)}\ \overline{0}\ f\ x \qquad \text{(d)}\ \overline{3}\ f\ x$$

</div>

</div>

<br>

**2.** Verdadeiro ou falso? Justifique:

*"$\overline{0}$ é equivalente à função identidade $\lambda x.\ x$."*

---
layout: statement
---

# Sucessor

---

# Sucessor

<br>

A função **SUCC** recebe um numeral de Church e retorna o próximo:

$$\text{SUCC} \equiv \lambda n.\ \lambda f.\ \lambda x.\ (f\ ((n\ f)\ x))$$

<div class="text-gray-600 text-sm text-center mt-2">

$n$ — o numeral recebido $\quad$ $f$ — a função $\quad$ $x$ — o argumento

</div>

<div class="flex gap-12 mt-8">

<div class="flex-1 text-center">

$$
\begin{aligned}
&\text{SUCC}\ \overline{0} \equiv (\lambda n.\ \lambda f.\ \lambda x.\ (f\ ((n\ f)\ x)))\ \overline{0} \\
&\xrightarrow{\beta} \lambda f.\ \lambda x.\ (f\ ((\overline{0}\ f)\ x)) \\
&\xrightarrow{\beta} \lambda f.\ \lambda x.\ (f\ x) \\
&\equiv \overline{1}
\end{aligned}
$$

</div>

<div class="flex-1 text-center">

$$
\begin{aligned}
&\text{SUCC}\ \overline{1} \equiv (\lambda n.\ \lambda f.\ \lambda x.\ (f\ ((n\ f)\ x)))\ \overline{1} \\
&\xrightarrow{\beta} \lambda f.\ \lambda x.\ (f\ ((\overline{1}\ f)\ x)) \\
&\xrightarrow{\beta} \lambda f.\ \lambda x.\ (f\ (f\ x)) \\
&\equiv \overline{2}
\end{aligned}
$$

</div>

</div>

---

# Exercícios de Fixação
Sucessor

**1.** Avalie passo a passo a partir da definição:

<div class="flex gap-8 mt-4">

<div class="flex-1">

$$\text{(a)}\ \text{SUCC}\ \overline{2}$$

</div>

<div class="flex-1">

$$\text{(b)}\ \text{SUCC}\ (\text{SUCC}\ \overline{0})$$

</div>

</div>

<br>

**2.** Verdadeiro ou falso? Justifique:

*"$\text{SUCC}\ \overline{0} \equiv \overline{1}$."*

---
layout: statement
---

# Adição

---

# Adição

<br>

Somar $m + n$ é aplicar **SUCC** exatamente $m$ vezes a $\overline{n}$:

$$\text{ADD} \equiv \lambda m.\ \lambda n.\ ((m\ \text{SUCC})\ n)$$

<div class="text-gray-600 text-sm text-center mt-2">

$\overline{m}$ recebe SUCC como função e $\overline{n}$ como ponto de partida —
avançando $m$ posições a partir de $n$.

</div>

<div class="flex gap-12 mt-8">

<div class="flex-1 text-center">

$$
\begin{aligned}
&((\text{ADD}\ \overline{1})\ \overline{1}) \equiv (((\lambda m.\ \lambda n.\ ((m\ \text{SUCC})\ n))\ \overline{1})\ \overline{1}) \\
&\xrightarrow{\beta} ((\lambda n.\ ((\overline{1}\ \text{SUCC})\ n))\ \overline{1}) \\
&\xrightarrow{\beta} ((\overline{1}\ \text{SUCC})\ \overline{1}) \\
&\xrightarrow{\beta} (\text{SUCC}\ \overline{1}) \\
&\xrightarrow{\beta} \overline{2}
\end{aligned}
$$

</div>

<div class="flex-1 text-center">

$$
\begin{aligned}
&((\text{ADD}\ \overline{2})\ \overline{1}) \equiv (((\lambda m.\ \lambda n.\ ((m\ \text{SUCC})\ n))\ \overline{2})\ \overline{1}) \\
&\xrightarrow{\beta} ((\lambda n.\ ((\overline{2}\ \text{SUCC})\ n))\ \overline{1}) \\
&\xrightarrow{\beta} ((\overline{2}\ \text{SUCC})\ \overline{1}) \\
&\xrightarrow{\beta} (\text{SUCC}\ (\text{SUCC}\ \overline{1})) \\
&\xrightarrow{\beta} (\text{SUCC}\ \overline{2}) \\
&\xrightarrow{\beta} \overline{3}
\end{aligned}
$$

</div>

</div>

---

# Exercícios de Fixação
Adição


**1.** Avalie passo a passo a partir da definição:

<div class="flex gap-8 mt-4">

<div class="flex-1">

$$\text{(a)}\ ((\text{ADD}\ \overline{0})\ \overline{2})$$

</div>

<div class="flex-1">

$$\text{(b)}\ ((\text{ADD}\ \overline{2})\ \overline{3})$$

</div>

</div>

<br>

**2.** Verdadeiro ou falso? Justifique:

*"$((\text{ADD}\ \overline{m})\ \overline{0}) \equiv \overline{m}$ para qualquer numeral $\overline{m}$."*

---
layout: statement
---

# Multiplicação

---

# Multiplicação

<br>

Multiplicar $m \times n$ é aplicar **ADD $\overline{n}$** exatamente $m$ vezes a $\overline{0}$:

$$\text{MULT} \equiv \lambda m.\ \lambda n.\ ((m\ (\text{ADD}\ n))\ \overline{0})$$

<div class="text-gray-600 text-sm text-center mt-2">
Somar $n$ consigo mesmo $m$ vezes a partir de zero.
</div>

<div class="flex gap-12 mt-8">

<div class="flex-1">

$$
\begin{aligned}
&((\text{MULT}\ \overline{2})\ \overline{2}) \equiv (((\lambda m.\ \lambda n.\ ((m\ (\text{ADD}\ n))\ \overline{0}))\ \overline{2})\ \overline{2}) \\
&\xrightarrow{\beta} ((\lambda n.\ ((\overline{2}\ (\text{ADD}\ n))\ \overline{0}))\ \overline{2}) \\
&\xrightarrow{\beta} ((\overline{2}\ (\text{ADD}\ \overline{2}))\ \overline{0}) \\
&\xrightarrow{\beta} ((\text{ADD}\ \overline{2})\ ((\text{ADD}\ \overline{2})\ \overline{0})) \\
&\xrightarrow{\beta} ((\text{ADD}\ \overline{2})\ \overline{2}) \\
&\xrightarrow{\beta} \overline{4}
\end{aligned}
$$

</div>

<div class="flex-1">

$$
\begin{aligned}
&((\text{MULT}\ \overline{2})\ \overline{3}) \equiv (((\lambda m.\ \lambda n.\ ((m\ (\text{ADD}\ n))\ \overline{0}))\ \overline{2})\ \overline{3}) \\
&\xrightarrow{\beta} ((\lambda n.\ ((\overline{2}\ (\text{ADD}\ n))\ \overline{0}))\ \overline{3}) \\
&\xrightarrow{\beta} ((\overline{2}\ (\text{ADD}\ \overline{3}))\ \overline{0}) \\
&\xrightarrow{\beta} ((\text{ADD}\ \overline{3})\ ((\text{ADD}\ \overline{3})\ \overline{0})) \\
&\xrightarrow{\beta} ((\text{ADD}\ \overline{3})\ \overline{3}) \\
&\xrightarrow{\beta} \overline{6}
\end{aligned}
$$

</div>

</div>

---

# Exercícios de Fixação
Multiplicação

**1.** Avalie passo a passo a partir da definição:

<div class="flex gap-8 mt-4">

<div class="flex-1">

$$\text{(a)}\ ((\text{MULT}\ \overline{1})\ \overline{3})$$

</div>

<div class="flex-1">

$$\text{(b)}\ ((\text{MULT}\ \overline{0})\ \overline{3})$$

</div>

</div>

<br>

**2.** Verdadeiro ou falso? Justifique:

*"$((\text{MULT}\ \overline{m})\ \overline{0}) \equiv \overline{0}$ para qualquer numeral $\overline{m}$."*

---
layout: statement
---

# A Progressão Completa

---

# A Progressão Completa

<br>

Cada operação é construída sobre a anterior:

<div class="mt-6">

$$\text{SUCC} \equiv \lambda n.\ \lambda f.\ \lambda x.\ (f\ ((n\ f)\ x))$$

<div class="text-gray-600 text-sm mt-1 text-center">

aplica $f$ uma vez a mais

</div>

</div>

<div class="mt-6">

$$\text{ADD} \equiv \lambda m.\ \lambda n.\ ((m\ \text{SUCC})\ n)$$

<div class="text-gray-600 text-sm mt-1 text-center">

aplica SUCC $m$ vezes a partir de $n$

</div>

</div>

<div class="mt-6">

$$\text{MULT} \equiv \lambda m.\ \lambda n.\ ((m\ (\text{ADD}\ n))\ \overline{0})$$

<div class="text-gray-600 text-sm mt-1 text-center">

aplica ADD $n$ exatamente $m$ vezes a partir de $\overline{0}$

</div>

</div>

<div class="mt-8">

> Subtração e divisão existem no cálculo lambda, mas exigem técnicas mais avançadas — predecessor, pares e recursão — e não serão abordadas neste curso por questões de objetividade.

</div>

---
layout: image
image: images/emily-morter.jpg
---