---
layout: cover
---

# Sintaxe e Semântica do Cálculo Lambda

---
layout: statement
---

# Convenções de Notação

---

# Convenções de Notação

<br>

| Símbolo | Leitura | Significado |
|---------|---------|-------------|
| $\equiv$ | "é definido como" | identidade sintática — o termo à esquerda é exatamente o termo à direita |
| $\xrightarrow{\beta}$ | "reduz a" | uma etapa de β-redução |
| $\xrightarrow{\alpha}$ | "converte a" | uma etapa de α-conversão |
| $[N/x]M$ | "N substituído por x em M" | substituição de todas as ocorrências livres de $x$ em $M$ por $N$ |


<br>

> Nomes como TRUE, FALSE, NOT, AND são **convenções metalinguísticas** —  não fazem parte do cálculo lambda, mas nos ajudam a raciocinar sobre ele.

---
layout: statement
---

# As regras sintáticas

---

# As Três Regras (definição formal)

## Termos Lambda

Um **termo lambda** é definido recursivamente:


| Regra | Notação formal | Leitura |
|-------|---------------|---------|
| Variável | $x$ | qualquer nome |
| Abstração | $\lambda x.\ M$ | função com parâmetro $x$ e corpo $M$ |
| Aplicação | $(M\ N)$ | aplique o termo $M$ ao termo $N$ |


onde $M$, $N$ e $x$ são, eles próprios, termos lambda.

<div class="text-xl text-red-500 mt-6">
Nada mais é um termo lambda.
</div>

---

# Exemplos de Termos Lambda

<br>

**Termos válidos:**

<div class="flex gap-8 mt-4">

<div class="flex-1">

$$\lambda x.\ x$$
<div class="text-gray-600 text-sm mt-1" text-center>função identidade</div>

$$\lambda s.\ (s\ s)$$
<div class="text-gray-600 text-sm mt-1" text-center>auto-aplicação</div>

</div>

<div class="flex-1">

$$(\ (\lambda x.\ x)\ \ (\lambda s.\ (s\ s))\ )$$
<div class="text-gray-600 text-sm mt-1 text-center">aplicação da identidade à auto-aplicação</div>

$$\lambda f.\ \lambda a.\ (f\ a)$$
<div class="text-gray-600 text-sm mt-1" text-center>função que aplica seu primeiro argumento ao segundo</div>

</div>

</div>

---

# O que não é um Termo Lambda

<br>

| Expressão | Por quê |
|-----------|---------|
| $\lambda$ | símbolo isolado — não é termo |
| $\lambda x$ | falta o corpo — incompleto |
| $(x)$ | parênteses requerem dois termos — é uma aplicação, não um termo isolado |

<br>

<div class="text-xl text-red-500 mt-6">
Toda expressão lambda é construída pelas três regras — e apenas por elas.
</div>

---

# Aplicação: quem age sobre quem?

<br>

Na aplicação $(M\ N)$, a **função age sobre o argumento** — não o contrário.

<div class="flex gap-8 mt-8">

<div class="flex-1 text-center">

**Notação matemática**
$$f(x)$$
$f$ age sobre $x$

</div>

<div class="flex-1 text-center">

**Notação lambda**
$$(f\ x)$$
$f$ age sobre $x$

</div>

</div>

<div class="mt-8">

A ordem **esquerda → direita** codifica isso diretamente:

- termo da **esquerda** — a função (o agente)
- termo da **direita** — o argumento (o objeto)

</div>

---

# Associação à Esquerda

<br>

Quando uma função recebe múltiplos argumentos, a aplicação associa à esquerda:

$$f\ x\ y\ z \equiv (((f\ x)\ y)\ z)$$

<div class="mt-8 text-gray-600">

Leitura passo a passo:

</div>

<div class="mt-4">

| Passo | Expressão | Leitura |
|-------|-----------|---------|
| 1 | $(f\ x)$ | aplique $f$ a $x$ |
| 2 | $((f\ x)\ y)$ | aplique o resultado a $y$ |
| 3 | $(((f\ x)\ y)\ z)$ | aplique o resultado a $z$ |

</div>

---

# Exercícios de Fixação
Termos Lambda

**1.** Quais das expressões abaixo são termos lambda válidos? Justifique:

$$\text{(a)}\ \lambda x.\ x \qquad \text{(b)}\ \lambda \qquad \text{(c)}\ (\lambda x.\ x\ \ y) \qquad \text{(d)}\ \lambda x$$

<br>

**2.** Para cada termo abaixo, diga se é uma variável, uma abstração ou uma aplicação:

$$\text{(a)}\ x \qquad \text{(b)}\ \lambda x.\ x \qquad \text{(c)}\ (\lambda x.\ x\ \ \lambda y.\ y) \qquad \text{(d)}\ \lambda f.\ \lambda a.\ (f\ a)$$

<br>

**3.** Reescreva a expressão abaixo inserindo todos os parênteses explícitos segundo a associação à esquerda:

$$f\ x\ y\ z$$

<div class="text-gray-600 text-sm mt-6">

**Dica**: o espaço entre dois termos dentro de parênteses indica uma aplicação $(M\ N)$.
Identifique onde cada termo começa e termina antes de classificar.

</div>

---
layout: statement
---

# Variáveis Ligadas e Livres


---

# Variáveis Ligadas

<br>

Uma variável é **ligada** quando está no escopo de um $\lambda$ que a introduz.

<div class="flex gap-12 mt-6">

<div class="flex-1">

$$\lambda x.\ x$$

<div class="text-center text-gray-600 text-sm mt-2">

$x$ é ligada —<br>
foi introduzida pelo $\lambda x$

</div>

</div>

<div class="flex-1">

$$\lambda f.\ \lambda x.\ (f\ x)$$

<div class="text-center text-gray-600 text-sm mt-2">

$f$ é ligada ao $\lambda f$;<br>
$x$ é ligada ao $\lambda x$

</div>

</div>

</div>

<div class="mt-10">

> O **escopo** de uma variável ligada é o corpo da função que a introduziu.

</div>

<div class="mt-4 text-sm">

**Exemplo**: em $\lambda f.\ \lambda s.\ (f\ (s\ s))$, o escopo de $f$ é o corpo
$\lambda s.\ (f\ (s\ s))$ — e apenas ali. Fora desse corpo, $f$ não existe como variável ligada.

</div>

---

# Variáveis Livres

<br>

Uma variável é **livre** quando não está no escopo de nenhum $\lambda$ que a introduza.

<div class="flex gap-12 mt-6">

<div class="flex-1">

$$\lambda x.\ (f\ x)$$

<div class="text-center text-sm mt-2">

$x$ é ligada, mas $f$ é livre --<br>
nenhum $\lambda$ a introduziu neste termo

</div>

</div>

<div class="flex-1">

$$(\lambda x.\ x)\ y$$

<div class="text-center text-sm mt-2">

$x$ é ligada ao $\lambda x$,<br>
mas $y$ é livre

</div>

</div>

</div>

<div class="mt-8">

> Uma variável pode ser **livre e ligada em lugares diferentes** do mesmo termo.

</div>

<div class="mt-4 text-sm">

**Exemplo**: $(\lambda x.\ x)\ x$ — o $x$ dentro da abstração é ligado;
o $x$ passado como argumento é livre. Na prática, isso é evitado
renomeando variáveis — o que veremos a seguir com a α-conversão.

</div>

---

# Exercícios de Fixação
Variáveis Ligadas e Livres

<br>

**1.** Para cada termo abaixo, identifique todas as variáveis **ligadas** e **livres**:

<div class="flex gap-8 mt-6">

<div class="flex-1">

$$\text{(a)}\ \lambda x.\ x$$

$$\text{(b)}\ \lambda x.\ (f\ x)$$

</div>

<div class="flex-1">

$$\text{(c)}\ (\lambda x.\ x\ \ y)$$

$$\text{(d)}\ \lambda f.\ \lambda x.\ (f\ x)$$

</div>

</div>

<br>

**2.** No termo abaixo, indique o **escopo** de cada variável ligada:

$$\lambda x.\ \lambda y.\ (\lambda x.\ y\ \ \lambda y.\ x)$$

---

# Exercícios de Fixação
Variáveis Ligadas e Livres

**3.** Verdadeiro ou falso? Justifique:


*"Uma mesma variável não pode ser livre e ligada no mesmo termo lambda."*

<div class="text-gray-600 text-sm mt-10">

**Dica**: uma variável é ligada quando está no escopo do $\lambda$ que a introduziu.
Fora desse escopo, ela pode aparecer livre.

</div>

---
layout: statement
---

# O Problema da Colisão de Nomes

---

# O Problema da Colisão de Nomes

<br>

Uma β-redução pode colocar uma variável livre dentro do escopo
de uma variável ligada com o **mesmo nome** — gerando um resultado errado.

<div class="mt-6">

$$(\lambda func.\ \lambda arg.\ (func\ arg)\ \ arg)\ boing$$

</div>

<div class="text-gray-600 text-center text-sm mt-2">

Aqui, $arg$ é usado como variável ligada do $\lambda arg$ <strong>e</strong> como variável livre no argumento externo.

</div>

<div class="mt-6">

Se reduzirmos literalmente:

$$
\begin{aligned}
&\xrightarrow{\beta} (\lambda arg.\ (arg\ arg))\ boing \\
&\xrightarrow{\beta} (boing\ boing)
\end{aligned}
$$

</div>

<div class="mt-4 text-gray-600 text-center text-sm">

Resultado errado — o $arg$ livre foi capturado pelo $\lambda arg$ interno.
O resultado esperado seria $(arg\ boing)$.

</div>

---

# α-Conversão

<br>

A **α-conversão** renomeia uma variável ligada para evitar colisões de nomes.

<div class="mt-6">

Para uma abstração $\lambda x.\ M$, podemos substituir $x$ por um novo nome $y$
em $\lambda x$ e em todas as ocorrências **livres** de $x$ em $M$,
desde que $y$ não seja uma variável livre em $\lambda x.\ M$.

</div>

<div class="mt-8">

Aplicando ao exemplo anterior — renomeando $arg$ para $arg_1$:

$$
\begin{aligned}
&(\lambda func.\ \lambda arg.\ (func\ arg)\ \ arg)\ boing \\
&\xrightarrow{\alpha} (\lambda func.\ \lambda arg_1.\ (func\ arg_1)\ \ arg)\ boing \\
&\xrightarrow{\beta} (\lambda arg_1.\ (arg\ arg_1))\ boing \\
&\xrightarrow{\beta} (arg\ boing)
\end{aligned}
$$

</div>

<div class="mt-6 text-gray-600 text-sm">

Resultado correto. A α-conversão é sempre aplicada **antes** da β-redução
quando há risco de colisão.

</div>

---

# Exercícios de Fixação
α-Conversão

**1.** A α-conversão abaixo está correta? Justifique:

$$\lambda x.\ (x\ y) \xrightarrow{\alpha} \lambda z.\ (z\ y)$$

<br>

**2.** Antes de realizar a β-redução abaixo, identifique se há colisão de nomes. Se houver, aplique α-conversão primeiro:

$$(\lambda x.\ \lambda y.\ x)\ y$$

<br>

**3.** A α-conversão abaixo está correta? Justifique:

$$\lambda x.\ (x\ y) \xrightarrow{\alpha} \lambda y.\ (y\ y)$$

---
layout: statement
---

# Mecanismo de computação no Cálculo Lambda

---

# β-Redução

<br>

A **β-redução** é o único mecanismo de computação do cálculo lambda.

Para uma aplicação $(\lambda x.\ M)\ N$:

<div class="mt-6">

> Substitua todas as ocorrências **livres** de $x$ em $M$ pelo termo $N$.

</div>

<div class="mt-8">

Notação: $(\lambda x.\ M)\ N$ é chamado de **β-redex**.

O resultado $[N/x]M$ é chamado de **contractum**.

$$(\lambda x.\ M)\ N \xrightarrow{\beta} [N/x]M$$

</div>

---

# β-Redução: Exemplos

<br>

<div class="flex gap-12 mt-4">

<div class="flex-1">

**Função identidade**

$$(\lambda x.\ x)\ N \xrightarrow{\beta} N$$

<div class="text-center text-sm mt-2">

$x$ é substituído por $N$ no corpo $x$

</div>

</div>

<div class="flex-1">

**Função constante**

$$(\lambda x.\ y)\ N \xrightarrow{\beta} y$$

<div class="text-center text-sm mt-2">

$x$ não ocorre livre em $y$ — resultado independe de $N$

</div>

</div>

</div>

<div class="mt-8">

**Redução em dois passos**

$$
\begin{aligned}
&(\lambda x.\ (\lambda y.\ y\ x)\ z)\ v \\
&\xrightarrow{\beta} (\lambda y.\ y\ z)\ v \\
&\xrightarrow{\beta} v\ z
\end{aligned}
$$
</div>

<div class="mt-4 text-red-600 text-sm">

Nem toda redução termina — $(\lambda x.\ x\ x)\ (\lambda x.\ x\ x)$ reduz sempre a si mesmo.

</div>

---

# Forma Normal

<br>

Uma expressão lambda que não pode ser reduzida é dita estar em sua **forma normal**.

<br>

> Um termo $Q$ está em **forma normal** quando não contém nenhum β-redex —
> ou seja, não há mais nenhuma aplicação da forma $(\lambda x.\ M)\ N$ a ser reduzida.

<div class="mt-8">

**Exemplo:** $(\lambda x.\ (\lambda y.\ y\ x)\ z)\ v$ reduz a $z\ v$, que está em forma normal.

</div>

<div class="mt-6">

**Atenção:** nem todo termo possui forma normal.

$$(\lambda x.\ x\ x)\ (\lambda x.\ x\ x) \xrightarrow{\beta} (\lambda x.\ x\ x)\ (\lambda x.\ x\ x) \xrightarrow{\beta} \cdots$$

</div>

---

# Exercícios de Fixação

<br>

**1.** Realize a β-redução dos seguintes termos passo a passo:

<div class="flex gap-8 mt-4">

<div class="flex-1">

$$\text{(a)}\ (\lambda x.\ x)\ N$$

$$\text{(b)}\ (\lambda x.\ y)\ N$$

</div>

<div class="flex-1">

$$\text{(c)}\ (\lambda x.\ x\ (x\ y))\ N$$

$$\text{(d)}\ (\lambda x.\ (\lambda y.\ y\ x)\ z)\ v$$

</div>

</div>

<br>

**2.** O termo abaixo possui forma normal? Justifique:

$$(\lambda x.\ x\ x)\ (\lambda x.\ x\ x)$$

---
layout: image
image: images/emily-morter.jpg
---
