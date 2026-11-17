# Tema Corporativo: explicando o CSS

Arquivo: `css/tema-corporativo.css`

## Ideia do tema

Visual **institucional e organizado**, como o site de uma empresa ou escola: fundo claro, azul e vermelho como cores de marca, fonte sem serifa e conteúdo separado em **cartões brancos**. É o tema mais "comportado" dos quatro.

Use-o como **ponto de partida** para ler os outros, porque ele usa os recursos mais comuns do CSS.

---

## 1. Variáveis de cor (`:root`)

```css
:root {
  --azul: #0b3d91;
  --vermelho: #d3202f;
  --fundo: #eef2f8;
  ...
}
```

- `:root` representa a página inteira (a tag `<html>`).
- Nomes que começam com `--` são **variáveis CSS** (propriedades personalizadas). Você escolhe o nome e o valor.
- Para usar, escreve-se `var(--azul)`:

```css
.topo { background: var(--azul); }
```

**Vantagem:** a paleta fica num lugar só. Mudando `--azul` no topo do arquivo, **todo o azul da página muda de uma vez**. Experimente!

---

## 2. Regras de base

```css
* { box-sizing: border-box; }
```

O `*` significa "todos os elementos". O `box-sizing: border-box` faz com que `width` inclua o espaçamento interno e a borda, o que torna as contas de largura muito mais previsíveis. É praticamente um padrão em CSS moderno.

```css
body.pagina {
  margin: 0;
  font-family: "Segoe UI", Roboto, Arial, sans-serif;
  line-height: 1.65;
  color: var(--texto);
  background: var(--fundo);
}
```

- `body.pagina` = "a tag `body` **que tem** a classe `pagina`".
- `margin: 0` tira a margem padrão do navegador.
- `font-family` lista fontes em ordem de preferência: se a primeira não existir no computador, usa a próxima. `sans-serif` é o plano B genérico.
- `line-height: 1.65` é o espaçamento entre linhas (1,65 vezes o tamanho da letra).
- Esses valores são **herdados** por tudo que está dentro do `body`.

---

## 3. Cabeçalho e menu

```css
.topo {
  background: var(--azul);
  color: #fff;
  padding: 2.5rem 1.5rem 0;
  text-align: center;
  border-bottom: 5px solid var(--vermelho);
}
```

- `padding` é o espaço **interno** (entre o conteúdo e a borda). Com 3 valores: cima, laterais, baixo.
- `border-bottom` desenha uma faixa vermelha embaixo.
- `rem` é uma unidade relativa ao tamanho da fonte base (1rem ≈ 16px). Mais flexível do que `px`.

### O menu em linha

```css
.menu ul {
  list-style: none;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: .25rem;
}
```

Aqui está o **truque central de qualquer menu horizontal**:

| Propriedade | O que faz |
|---|---|
| `list-style: none` | Tira os marcadores da lista |
| `display: flex` | Coloca os filhos (`li`) **lado a lado** |
| `flex-wrap: wrap` | Permite quebrar para a linha de baixo se faltar espaço |
| `justify-content: center` | Centraliza |
| `gap` | Espaço entre os itens |

```css
.menu a { display: block; padding: .8rem 1.1rem; color: #fff; text-decoration: none; }
.menu a:hover { background: var(--azul-escuro); }
```

- `display: block` faz o link ocupar uma área clicável maior (por causa do `padding`).
- `text-decoration: none` remove o sublinhado.
- `:hover` é um **estado**: a regra só vale enquanto o mouse está em cima.

---

## 4. Conteúdo principal e cartões

```css
.principal { max-width: 920px; margin: 2rem auto; padding: 0 1rem; }
```

- `max-width` limita a largura (texto muito largo é difícil de ler).
- `margin: 2rem auto` = 2rem em cima e embaixo, e `auto` nas laterais, o que **centraliza** o bloco.

```css
.secao {
  background: var(--papel);
  padding: 1.5rem 2rem;
  margin-bottom: 1.5rem;
  border-radius: 8px;
  border-left: 5px solid var(--azul);
  box-shadow: 0 1px 4px rgba(20, 40, 90, .12);
}
```

É a receita do "cartão":

- `border-radius` arredonda os cantos;
- `border-left` faz uma tira colorida na lateral;
- `box-shadow: x y desfoque cor` cria uma sombra suave (`rgba` é cor com transparência).

```css
.secao h2 { margin-top: 0; color: var(--azul); }
```

O espaço no seletor significa "**todo `h2` que esteja dentro** de um elemento `.secao`". Assim o estilo só afeta os títulos das seções, e não todos os `h2` da página.

---

## 5. Texto

```css
mark { background: #ffe58a; padding: 0 .2em; }
del  { color: var(--vermelho); }
ins  { color: #1a7f45; text-decoration: none; border-bottom: 2px solid #1a7f45; }
```

Estas regras usam **o nome da tag** como seletor. Elas valem para toda a página.

```css
code { background: #e8edf7; padding: .1em .35em; border-radius: 4px; }
kbd  { border: 1px solid var(--linha); border-bottom-width: 3px; border-radius: 4px; }
```

- O `kbd` imita a **tecla de um teclado**: borda mais grossa embaixo dá a sensação de relevo.
- O `samp` ganha fundo escuro com texto verde, parecendo a saída de um programa.

```css
.etiqueta { background: var(--azul); color: #fff; padding: .1em .6em; border-radius: 99px; }
```

`border-radius: 99px` com um valor muito grande transforma o fundo numa **pílula**.

---

## 6. Botão, imagem, tabela

```css
.botao { display: inline-block; background: var(--vermelho); color: #fff; padding: .6rem 1.2rem; border-radius: 6px; ... }
.botao:hover { background: #a8161f; }
```

Um link (`<a>`) transformado em botão: é só **fundo, espaçamento e cantos arredondados**. Nada mudou no HTML.

```css
.figura img { max-width: 100%; height: auto; ... }
```

`max-width: 100%` impede que a imagem passe do tamanho do contêiner (importante em celulares).

```css
.tabela { width: 100%; border-collapse: collapse; }
.tabela th { background: var(--azul); color: #fff; }
.tabela tbody tr:nth-child(even) { background: #f4f7fc; }
```

- `border-collapse: collapse` junta as bordas das células (sem isso, ficam bordas duplas).
- `:nth-child(even)` seleciona **as linhas pares**: é o efeito "zebrado".

---

## 7. Blocos

```css
.cartoes {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 1rem;
}
```

Este é o **layout em grade** (`grid`) que se adapta sozinho:

- cada cartão tem no mínimo 220px;
- cabem quantos couberem na linha;
- o restante vai para a linha de baixo.

Redimensione a janela do navegador e veja o número de colunas mudar sem nenhum código extra.

```css
.codigo { background: #14213d; color: #e6edf8; padding: 1rem 1.2rem; border-radius: 8px; overflow-x: auto; }
```

`overflow-x: auto` cria uma barra de rolagem horizontal se o código for mais largo que o bloco.

---

## 8. Elementos interativos e rodapé

```css
.sanfona summary { cursor: pointer; font-weight: 700; color: var(--azul); }
progress, meter { width: 220px; vertical-align: middle; }
```

- `cursor: pointer` troca o ponteiro do mouse pela mãozinha.
- Há também regras para a `.lateral` (caixa amarelada) e para o `.rodape` (fundo azul-escuro, texto claro e centralizado).

---

## Para experimentar

1. Troque `--azul` e `--vermelho` por outras cores e veja a página inteira se adaptar.
2. Em `.secao`, mude `border-radius` para `0` e depois para `30px`.
3. Em `.cartoes`, mude `220px` para `400px`. Quantas colunas aparecem?
4. Tire o `display: flex` de `.menu ul`. O que acontece com o menu?
5. Apague `.tabela tbody tr:nth-child(even) {...}` e veja o zebrado sumir.
6. Em `.botao:hover`, troque a cor e passe o mouse.
