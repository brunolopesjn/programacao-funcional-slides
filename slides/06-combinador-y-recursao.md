---
layout: cover
---

# Recursão e o Combinador Y

---
layout: statement
---

# O Problema da Auto-Referência

---

# O Problema da Auto-Referência

<br>

Em cálculo lambda, **não existem nomes globais** — toda função é anônima.

Como definir uma função que precisa chamar a si mesma?

<div class="mt-8">

Em linguagens imperativas, recursão é direta:

$$\text{def } f(x) = \text{... } f(x-1) \text{ ...}$$

</div>

<div class="mt-8">

Em lambda puro, isso é impossível diretamente — $f$ não existe dentro de sua própria definição:

$$\lambda x.\ (\ldots\ f\ \ldots) \quad \text{— quem é } f \text{?}$$

</div>

<div class="mt-8 text-gray-600 text-sm">

Precisamos de um mecanismo que permita a uma função receber uma cópia de si mesma como argumento.

</div>

---
layout: statement
---

# Auto-Aplicação como Mecanismo de Cópia

---

# Auto-Aplicação como Mecanismo de Cópia

<br>

A auto-aplicação $(\lambda s.\ (s\ s))$ aplicada a si mesma replica indefinidamente:

$$(\lambda s.\ (s\ s))\ (\lambda s.\ (s\ s)) \xrightarrow{\beta} (\lambda s.\ (s\ s))\ (\lambda s.\ (s\ s)) \xrightarrow{\beta} \cdots$$

<div class="mt-6 text-gray-600 text-sm text-center">
Não termina — precisamos controlar quando a replicação ocorre.
</div>

<div class="mt-8">

A solução é **atrasar** a auto-aplicação através de uma abstração:

$$\lambda s.\ (f\ (s\ s))$$

</div>

<div class="mt-6 text-gray-600 text-sm">

Agora $(s\ s)$ só é avaliado quando $f$ decidir — por exemplo, quando uma condição for satisfeita. A replicação passa a ser controlada pela própria função recursiva.

</div>

---
layout: statement
---

# O Combinador Y

---

# O Combinador Y

<br>

Aplicando a função controlada a si mesma, obtemos o mecanismo completo:

$$(\lambda s.\ (f\ (s\ s)))\ (\lambda s.\ (f\ (s\ s))) \xrightarrow{\beta} f\ ((\lambda s.\ (f\ (s\ s)))\ (\lambda s.\ (f\ (s\ s))))$$

<div class="mt-6 text-gray-600 text-sm text-center">

O resultado é $f$ aplicado a uma cópia do mecanismo inteiro — recursão controlada.

</div>

<div class="mt-8">

Abstraindo sobre $f$, chegamos ao **Combinador Y**:

$$Y \equiv \lambda f.\ (\lambda s.\ (f\ (s\ s)))\ (\lambda s.\ (f\ (s\ s)))$$

</div>

<div class="mt-6">

> $Y$ é chamado de **combinador de ponto fixo** — para qualquer $f$,
> $Y\ f$ é um ponto fixo de $f$: $Y\ f \xrightarrow{\beta} f\ (Y\ f)$

</div>

---

# Verificação do Combinador Y

<br>

Para verificar $Y\ f \xrightarrow{\beta} f\ (Y\ f)$, primeiro aplicamos α-conversão para evitar colisão entre o parâmetro de $Y$ e o argumento $f$:

$$
\begin{aligned}
Y &\equiv \lambda f.\ (\lambda s.\ (f\ (s\ s)))\ (\lambda s.\ (f\ (s\ s))) \\
&\xrightarrow{\alpha} \lambda g.\ (\lambda s.\ (g\ (s\ s)))\ (\lambda s.\ (g\ (s\ s)))
\end{aligned}
$$

<div class="mt-6">

Agora aplicamos $Y$ ao argumento $f$ sem colisão:

$$
\begin{aligned}
Y\ f &\equiv (\lambda g.\ (\lambda s.\ (g\ (s\ s)))\ (\lambda s.\ (g\ (s\ s))))\ f \\
&\xrightarrow{\beta} (\lambda s.\ (f\ (s\ s)))\ (\lambda s.\ (f\ (s\ s))) \\
&\xrightarrow{\beta} f\ ((\lambda s.\ (f\ (s\ s)))\ (\lambda s.\ (f\ (s\ s)))) \\
&\equiv f\ (Y\ f)
\end{aligned}
$$

</div>

---

# Do Combinador Y ao `def` do Elixir

<br>

Em lambda puro, recursão exige o Combinador Y. Em Elixir, o `def` fornece esse mecanismo automaticamente:

<div class="flex gap-12 mt-8">

<div class="flex-1">

**Lambda puro**

$$Y\ (\lambda f.\ \lambda n.\ \text{if}\ n = 0\ \text{then}\ 1\ \text{else}\ n \times (f\ (n-1)))$$

</div>

<div class="flex-1">

**Elixir**

```elixir
def fatorial(0), do: 1
def fatorial(n) do
  n * fatorial(n - 1)
end
```

</div>

</div>

<div class="mt-8 text-gray-600 text-sm">

O `def` em Elixir introduz o nome da função no seu próprio escopo — exatamente o que o Combinador Y faz manualmente em lambda puro.

</div>

---
layout: statement
---

# Somatório de uma Lista com o Combinador Y

---

# Somatório de uma Lista com o Combinador Y

<br>

Queremos definir uma função que soma todos os elementos de uma lista de numerais de Church:

$$\text{SUM}\ (\text{CONS}\ \overline{1}\ (\text{CONS}\ \overline{2}\ (\text{CONS}\ \overline{3}\ \text{NIL}))) \xrightarrow{\beta} \overline{6}$$

<div class="mt-8">

A lógica recursiva é simples:

- Se a lista é **vazia** → o resultado é $\overline{0}$
- Caso contrário → some a **cabeça** com o somatório da **cauda**

</div>

<div class="mt-8 text-gray-600 text-sm">

Para isso, precisamos de um operador que verifique se uma lista é vazia — o operador **ISNIL** — que veremos a seguir.

</div>

---

# O Operador ISNIL

<br>

ISNIL verifica se uma lista é vazia — retorna TRUE se a lista for NIL,
FALSE caso contrário:

$$\text{ISNIL} \equiv \lambda l.\ ((l\ (\lambda h.\ \lambda t.\ \text{FALSE}))\ \text{TRUE})$$

<div class="mt-8">

| Expressão | Resultado |
|-----------|-----------|
| $\text{ISNIL}\ \text{NIL}$ | $\text{TRUE}$ |
| $\text{ISNIL}\ ((\text{CONS}\ M)\ N)$ | $\text{FALSE}$ |

</div>

<div class="mt-8 text-gray-600 text-sm">

ISNIL depende da representação interna de NIL e CONS —
o mecanismo de verificação é apresentado aqui por convenção,
como ferramenta para construção do somatório recursivo.

</div>

---

# Somatório com o Combinador Y

<br>

**Passo 1:** versão não-recursiva, recebendo $f$ no lugar da auto-referência:

$$\text{SUM}_1 \equiv \lambda f.\ \lambda l.\ \text{if}\ (\text{ISNIL}\ l)\ \text{then}\ \overline{0}\ \text{else}\ ((\text{ADD}\ (\text{HEAD}\ l))\ (f\ (\text{TAIL}\ l)))$$


**Passo 2:** aplicar Y para obter a versão recursiva:

$$\text{SUM} \equiv Y\ \text{SUM}_1$$


**Verificação da propriedade do ponto fixo:**

$$
\begin{aligned}
\text{SUM} &\equiv Y\ \text{SUM}_1 \\
&\xrightarrow{\beta} \text{SUM}_1\ (Y\ \text{SUM}_1) \\
&\equiv \text{SUM}_1\ \text{SUM}
\end{aligned}
$$

<div class="mt-6 text-gray-600 text-sm">

$\text{SUM}_1$ recebe uma cópia de $\text{SUM}$ como argumento $f$ — o Combinador Y fornece essa cópia automaticamente a cada chamada recursiva.

</div>

---

# Exemplo — SUM $[\ \overline{1},\ \overline{2},\ \overline{3}\ ]$

<br>

$$
\begin{aligned}
&\text{SUM}\ ((\text{CONS}\ \overline{1})\ ((\text{CONS}\ \overline{2})\ ((\text{CONS}\ \overline{3})\ \text{NIL}))) \\
&\xrightarrow{\beta} \text{SUM}_1\ \text{SUM}\ ((\text{CONS}\ \overline{1})\ ((\text{CONS}\ \overline{2})\ ((\text{CONS}\ \overline{3})\ \text{NIL})))
\quad \small{\text{(ponto fixo: SUM} \equiv \text{SUM}_1\ \text{SUM)}} \\
&\xrightarrow{\beta} (\text{ADD}\ \overline{1})\ (\text{SUM}\ ((\text{CONS}\ \overline{2})\ ((\text{CONS}\ \overline{3})\ \text{NIL})))
\quad \small{\text{(ISNIL falso — ramo else, HEAD} = \overline{1}\text{, TAIL} = [\overline{2}, \overline{3}]\text{)}} \\
&\xrightarrow{\beta} (\text{ADD}\ \overline{1})\ ((\text{ADD}\ \overline{2})\ (\text{SUM}\ ((\text{CONS}\ \overline{3})\ \text{NIL})))
\quad \small{\text{(ISNIL falso — HEAD} = \overline{2}\text{, TAIL} = [\overline{3}]\text{)}} \\
&\xrightarrow{\beta} (\text{ADD}\ \overline{1})\ ((\text{ADD}\ \overline{2})\ ((\text{ADD}\ \overline{3})\ (\text{SUM}\ \text{NIL})))
\quad \small{\text{(ISNIL falso — HEAD} = \overline{3}\text{, TAIL} = \text{NIL}\text{)}} \\
&\xrightarrow{\beta} (\text{ADD}\ \overline{1})\ ((\text{ADD}\ \overline{2})\ ((\text{ADD}\ \overline{3})\ \overline{0}))
\quad \small{\text{(ISNIL verdadeiro — caso base: } \overline{0}\text{)}} \\
&\xrightarrow{\beta} (\text{ADD}\ \overline{1})\ ((\text{ADD}\ \overline{2})\ \overline{3})
\quad \small{(\overline{3} + \overline{0} = \overline{3})} \\
&\xrightarrow{\beta} (\text{ADD}\ \overline{1})\ \overline{5}
\quad \small{(\overline{2} + \overline{3} = \overline{5})} \\
&\xrightarrow{\beta} \overline{6}
\quad \small{(\overline{1} + \overline{5} = \overline{6})}
\end{aligned}
$$