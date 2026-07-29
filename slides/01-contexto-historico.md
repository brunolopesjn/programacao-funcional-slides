---
layout: cover
---

# Contexto histórico

---
layout: center
---

# A origem secreta das funções anônimas

---

# Você já conhece funções

<br>

<div class="flex gap-6 mt-6">

<div class="flex-1">

```python
# Python
def dobrar(x):
    return x * 2


```

</div>

<div class="flex-1">

```java
// Java
int dobrar(int x) {
    return x * 2;
}
```

</div>

<div class="flex-1">

```javascript
// JavaScript
function dobrar(x) {
    return x * 2;
}
```

</div>

<div class="flex-1">

```elixir
# Elixir
def dobrar(x) do
  x * 2
end

```

</div>

</div>

<br>
<br>

<div class="text-center text-2xl mt-3">
    <p>Quatro linguagens, quatro sintaxes.</p> 
</div>

<div class="text-center text-2xl mt-6 text-blue-500">
    <p>A mesma ideia.</p>
</div>

---

# Mas há algo diferente...

<br>

<div class="flex gap-6 mt-6">

<div class="flex-1">

```python
# Python
lambda x: x * 2
```

</div>

<div class="flex-1">

```java
// Java
x -> x * 2
```

</div>

<div class="flex-1">

```javascript
// JavaScript
x => x * 2
```

</div>

<div class="flex-1">

```elixir
# Elixir
fn x -> x * 2 end
```

</div>

</div>

<div class="text-center text-xl mt-8">
Quatro linguagens. A mesma coisa estranha: <strong>uma função sem nome</strong>.
</div>

<div class="text-center text-3xl text-red-500 mt-6">
Por quê? De onde vem isso?
</div>

---

# Não é coincidência

<br>

<div class="flex gap-6 mt-6">

<div class="flex-1">

```python
# Python
lambda x: x * 2
```

</div>

<div class="flex-1">

```java
// Java
x -> x * 2
```

</div>

<div class="flex-1">

```javascript
// JavaScript
x => x * 2
```

</div>

<div class="flex-1">

```elixir
# Elixir
fn x -> x * 2 end
```

</div>

</div>

<div class="flex gap-6 mt-10 items-center justify-center">
<div class="text-6xl text-center">
λx. x * 2
</div>
</div>

<div class="text-center text-xl mt-6">
Essa notação tem quase 100 anos — e está na origem de todas elas.
</div>

---

# Alonzo Church e o Cálculo Lambda

<br>

<div class="mt-8 text-xl">

Church não estava criando uma linguagem de programação.
Computadores ainda não existiam.

</div>

<div class="mt-8 text-xl">

Ele queria responder uma pergunta fundamental:

</div>

<div class="text-center text-3xl font-bold mt-10">
O que significa computar alguma coisa?
</div>

---

# Uma questão com quase 100 anos

<br>

| Ano | Evento |
|-----|--------|
| 1910 | Russell e Whitehead — *Principia Mathematica* |
| 1931 | Gödel — Teorema da Incompletude |
| 1936 | Church — *An Unsolvable Problem of Elementary Number Theory* |
| 1936 | Turing — Máquina de Turing |
| 1958 | McCarthy — LISP, primeira linguagem funcional |
| 1990 | Haskell — linguagem funcional pura |
| 2012 | Elixir |

---

# O Cálculo Lambda

<br>

Uma linguagem com apenas **três regras**.


Um **termo** lambda é qualquer expressão construída por:

| Regra | Forma | Leitura |
|-------|-------|---------|
| Variável | $x$ | um nome qualquer |
| Função | $\lambda x.\ M$ | "dado $x$, produza $M$" |
| Aplicação | $(M\ N)$ | "aplique $M$ ao argumento $N$" |

<br>

> *Nada mais é um termo lambda.*

---

# O papel dos parênteses

<br>

Os parênteses **delimitam uma aplicação** — indicam que o termo à esquerda é aplicado ao termo à direita.


$$
(\lambda x.\ x \times 2)\ 3
$$


O parêntese agrupa a função $\lambda x.\ x \times 2$ antes de aplicá-la ao argumento $3$


$$
\begin{aligned}
&(\lambda x.\ x \times 2)\ 3 \\
&\xrightarrow{\beta} 3 \times 2 \\
&\xrightarrow{\beta} 6
\end{aligned}
$$

Isso se chama **redução beta (β-redex)** — o único mecanismo de computação do cálculo lambda — que substitui $x$ por $3$ no corpo da função.

<div class="text-sm text-red-600 mt-4">

**OBS:** A forma completa seria $((\lambda x.\ x \times 2)\ 3)$ — os parênteses externos
podem ser omitidos por convenção quando não há ambiguidade.

</div>

---

# A herança direta

<div class="flex gap-6 mt-6">

<div class="flex-1">

```python
# Python
lambda x: x * 2
```

</div>

<div class="flex-1">

```java
// Java
x -> x * 2
```

</div>

<div class="flex-1">

```javascript
// JavaScript
x => x * 2
```

</div>

<div class="flex-1">

```elixir
# Elixir
fn x -> x * 2 end
```

</div>

</div>

<div class="flex gap-6 mt-10 items-center justify-center">
<div class="text-2xl text-center">

**Cálculo Lambda (1936)**
$$\lambda x.\ x \times 2$$

</div>
</div>

<div class="text-center text-xl mt-8">
Não é coincidência. É herança direta.
</div>

<div class="text-center text-lg text-blue-600 mt-2">
Quando você escreve uma função anônima em qualquer dessas linguagens,<br>
você está usando uma ideia de 1936.
</div>

---

# O que vem pela frente

<div class="flex gap-12 mt-8">

<div class="flex-1">

**Cálculo Lambda**

- Sintaxe e reduções
- Booleanos e numerais de Church
- Recursão e o combinador Y
- Fundamentos formais da computação

</div>

<div class="flex-1">

**Elixir**

- Funções anônimas e pattern matching
- Recursão e estruturas de dados imutáveis
- Funções de alta ordem
- Aplicações concorrentes com Phoenix

</div>

</div>

<div class="mt-10">

| Cálculo Lambda | Elixir |
|----------------|--------|
| $\lambda x.\ M$ | `fn x -> ... end` |
| Aplicação $(M\ N)$ | chamada de função |
| $\beta$-redex | avaliação |
| Recursão via Y | `def` recursivo |

</div>

---
layout: image
image: images/emily-morter.jpg
---