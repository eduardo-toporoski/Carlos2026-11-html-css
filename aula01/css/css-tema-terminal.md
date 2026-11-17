# Tema Terminal: explicando o CSS

Arquivo: `css/tema-terminal.css`

## Ideia do tema

O visual de um **terminal de computador antigo**: fundo escuro, texto cor de âmbar, fonte monoespaçada, bordas tracejadas. Dois recursos tornam este tema especial:

1. O cabeçalho e o menu **viram uma barra lateral fixa**. O CSS está mudando o **layout**, não só as cores.
2. Símbolos como `$`, `>`, `##` e `` ` `` aparecem na tela **sem existir no HTML**. Eles são criados só pelo CSS.

---

## 1. Variáveis e base

```css
:root {
  --fundo: #14100a;
  --painel: #1e1810;
  --ambar: #ffb000;
  --ambar-suave: #c98a00;
  --texto: #f0dfb8;
  --verde: #7fd18b;
  --vermelho: #ff6b57;
}
```

Paleta de um monitor antigo: marrom muito escuro, âmbar e um verde para códigos. Cada cor tem **um papel** (fundo, painel, destaque, texto), e não só um valor.

```css
body.pagina {
  background: var(--fundo);
  color: var(--texto);
  font-family: "Cascadia Mono", Consolas, "Courier New", monospace;
  font-size: 15px;
  line-height: 1.75;
}
```

- `monospace` = fonte em que **todas as letras têm a mesma largura**, como em um editor de código.
- A lista traz várias fontes de programação; o navegador usa a primeira que existir no computador.

---

## 2. O truque principal: a barra lateral fixa

```css
.topo {
  position: fixed;
  inset: 0 auto 0 0;
  width: 250px;
  padding: 1.5rem 1.2rem;
  background: var(--painel);
  border-right: 1px solid var(--ambar-suave);
  overflow-y: auto;
}
```

| Propriedade | O que faz |
|---|---|
| `position: fixed` | Tira o elemento do fluxo normal e **o prende na janela**: não rola junto com a página |
| `inset: 0 auto 0 0` | Posição: topo `0`, direita `auto`, base `0`, esquerda `0`. Ou seja, **cola na lateral esquerda e ocupa toda a altura** |
| `width: 250px` | Largura da barra |
| `overflow-y: auto` | Se o conteúdo for maior que a altura da janela, aparece rolagem |

Como a barra saiu do fluxo, o conteúdo principal passaria por baixo dela. Por isso:

```css
.principal { margin-left: 250px; padding: 2rem; max-width: 960px; }
.rodape    { margin-left: 250px; ... }
```

A margem esquerda de **250px** (a mesma largura da barra) abre espaço para ela.

```css
.menu ul { list-style: none; margin: 0; padding: 0; }
.menu a { display: block; padding: .2rem 0; ... }
```

Aqui o menu **não** usa `display: flex`: sem ele os itens ficam **um embaixo do outro**, que é o que queremos numa barra lateral.

> **Compare** com o tema Corporativo: o HTML é idêntico, mas ali o menu é horizontal no topo. Só o CSS mudou.

---

## 3. Conteúdo gerado pelo CSS (`::before` e `::after`)

```css
.topo h1::before { content: "$ "; color: var(--verde); }
.menu a::before  { content: "> "; color: var(--ambar-suave); }
.secao h2::before { content: "## "; color: var(--ambar-suave); }
.secao h3::before { content: "### "; opacity: .6; }
```

- `::before` cria um **elemento virtual antes do conteúdo** do elemento. `::after` faz o mesmo depois.
- A propriedade `content` define o texto inserido.
- Os símbolos imitam um **prompt de terminal** (`$`), setas de menu (`>`) e títulos em Markdown (`##`, `###`).

> **Importante:** esse texto **não existe no HTML**. Abra o arquivo `02-html-com-classes.html` e procure por `##`: você não vai achar. Isso é uma prova bem clara de que o CSS pode adicionar conteúdo visual, mas por isso **só deve ser usado para enfeites**, nunca para informação importante.

```css
code::before, code::after { content: "`"; opacity: .5; }
```

Cada `<code>` ganha crases ao redor, estilo Markdown. No bloco de código grande, as crases são desligadas:

```css
.codigo code::before, .codigo code::after { content: none; }
```

---

## 4. Listas com marcadores personalizados

```css
.principal ul { list-style: none; padding-left: 1.2rem; }
.principal ul li::before { content: "- "; color: var(--ambar-suave); margin-left: -1rem; }
ol li::marker { color: var(--ambar); }
```

- Os marcadores originais da `ul` são desligados e **trocados por um hífen**, criado com `::before`.
- `margin-left` negativo puxa o hífen para a esquerda, alinhando o texto.
- `::marker` formata o **número** da lista ordenada, sem precisar recriá-lo.
- Repare no `.principal` na frente: a regra vale **só para as listas do conteúdo principal**. Sem isso, o menu lateral e o rodapé (que também são listas `ul`) ganhariam hífens indesejados. Delimitar uma regra pelo contêiner é uma forma de evitar que ela "vaze" para onde você não queria.

---

## 5. Interação e cores

```css
a { color: var(--verde); }
a:hover { background: var(--verde); color: var(--fundo); }
```

Ao passar o mouse, o link **inverte as cores** (fundo verde, texto escuro): a mesma lógica de um cursor de terminal.

```css
mark { background: var(--ambar); color: var(--fundo); }
.botao:hover { background: var(--ambar); color: var(--fundo); }
```

A inversão de cores é o padrão visual do tema para tudo o que está "selecionado" ou em destaque.

---

## 6. Tabela, blocos e interativos

```css
.tabela th, .tabela td { border: 1px solid #5a4417; padding: .45rem .7rem; }
.tabela tbody tr:hover { background: var(--painel); }
```

A linha da tabela **acende** quando o mouse passa: `tr:hover`.

```css
.codigo { background: #000; border: 1px solid var(--ambar-suave); color: var(--verde); }
```

O bloco de código usa o preto puro com verde, o contraste clássico dos terminais.

```css
progress, meter { width: 220px; vertical-align: middle; accent-color: var(--ambar); }
```

`accent-color` é a forma mais curta de **pintar os controles nativos do navegador** (barra de progresso, medidor, caixas de seleção) na cor do tema.

```css
.lateral { border: 1px dashed var(--vermelho); }
.lateral h2::before { content: "! "; }
```

A caixa "Você sabia?" vira um aviso: borda tracejada vermelha e um `!` na frente do título.

---

## 7. Adaptação ao celular

```css
@media (max-width: 800px) {
  .topo { position: static; width: auto; border-right: 0; border-bottom: 1px solid var(--ambar-suave); }
  .principal, .rodape { margin-left: 0; padding-left: 1rem; padding-right: 1rem; }
}
```

Em telas com até 800px, uma barra lateral de 250px ocuparia espaço demais. O `@media` desfaz o truque:

- `position: static` devolve o cabeçalho ao **fluxo normal** (de volta ao topo);
- as margens esquerdas deixam de existir.

Estreite a janela do navegador para ver a barra lateral "voltar ao lugar".

---

## Para experimentar

1. Troque `--ambar` por `#00ff66` (verde fosforescente) e veja o terminal ficar mais "hacker".
2. Em `.topo`, mude `width: 250px` para `400px`. O que quebra? (Dica: ajuste também o `margin-left` do `.principal`.)
3. Troque `position: fixed` por `position: static`. O que acontece com a barra?
4. Mude `content: "$ "` para `content: "C:\\> "` e veja o título.
5. Apague a regra `.menu a::before` e perceba que o `>` some, sem nenhuma alteração no HTML.
6. Em `a:hover`, troque as cores por outras de sua escolha.
