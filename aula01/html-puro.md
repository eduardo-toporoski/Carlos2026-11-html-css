# HTML puro: conhecendo as tags

Arquivo desta etapa: `01-html-puro.html`

## 1. O que vamos fazer

Abra `01-html-puro.html` no VS Code e visualize com o **Live Preview** (clique com o botão direito no arquivo e escolha **Show Preview**).

A página que aparece é feia, e isso é de propósito. Ela **não tem nenhum CSS**: toda a aparência que você vê (títulos grandes, negrito, listas com marcadores, links azuis sublinhados) é o **estilo padrão do navegador**.

A ideia central desta etapa é:

> **O HTML descreve o que cada pedaço do conteúdo é** (um título, uma lista, uma tabela, uma citação). **Quem decide como ele aparece é o CSS**, que veremos na próxima etapa.

Enquanto você lê este guia, mantenha o arquivo HTML aberto ao lado, com o código à esquerda e a prévia à direita, para relacionar cada tag com o que aparece na tela.

---

## 2. Anatomia de uma tag

```html
<a href="#tabela" title="Ir para a tabela">Link interno</a>
```

| Parte | Exemplo | Nome |
|---|---|---|
| `<a ...>` | `<a href="#tabela">` | **tag de abertura** |
| `href="#tabela"` | | **atributo** (nome e valor) |
| `Link interno` | | **conteúdo** |
| `</a>` | | **tag de fechamento** |
| O conjunto todo | | **elemento** |

Algumas tags não têm conteúdo e **não fecham**: `<br>`, `<hr>`, `<img>`, `<meta>`. São as chamadas tags vazias.

---

## 3. A estrutura do documento

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  ...informações sobre a página (não aparecem nela)...
</head>
<body>
  ...tudo o que aparece na página...
</body>
</html>
```

| Tag | Para que serve |
|---|---|
| `<!DOCTYPE html>` | Avisa ao navegador que o documento usa HTML moderno (HTML5). |
| `<html lang="pt-BR">` | Raiz do documento. O atributo `lang` informa o idioma (importante para leitores de tela e tradutores). |
| `<head>` | Cabeçalho **técnico**: informações sobre a página. Nada daqui aparece na tela, exceto o título na aba do navegador. |
| `<body>` | O **corpo**: todo o conteúdo visível. |

### Dentro do `<head>`

| Tag | O que faz |
|---|---|
| `<meta charset="UTF-8">` | Define a codificação de caracteres. Sem ela, acentos como "ç" e "ã" podem aparecer quebrados. |
| `<meta name="viewport" ...>` | Ajusta a página para telas de celular. |
| `<meta name="description" ...>` | Resumo da página, usado por buscadores. |
| `<meta name="author" ...>` | Autoria. |
| `<title>` | O texto da **aba do navegador**. |

> Na versão `02-html-com-classes.html` entra aqui mais uma tag, o `<link rel="stylesheet">`, que conecta o HTML a um arquivo CSS. Na versão pura, ela não existe.

---

## 4. As regiões da página (tags semânticas)

Estas tags dividem a página em **áreas com significado**. Por padrão elas não mudam a aparência (todas viram "blocos" um embaixo do outro), mas ajudam leitores de tela, buscadores e quem lê o código.

| Tag | Significado | Onde está na página |
|---|---|---|
| `<header>` | Cabeçalho da página | Título "Introdução ao HTML" e o menu |
| `<nav>` | Conjunto de links de navegação | Menu do topo e links do rodapé |
| `<main>` | O conteúdo principal (só pode haver um por página) | Tudo entre o cabeçalho e o rodapé |
| `<section>` | Seção temática, normalmente com um título | Cada um dos 7 blocos numerados |
| `<article>` | Conteúdo independente, que faria sentido sozinho | Os três "cartões" da seção Blocos |
| `<aside>` | Conteúdo complementar, fora do fluxo principal | A caixa "Você sabia?" |
| `<footer>` | Rodapé | Direitos autorais, contato e links finais |
| `<div>` | Bloco **sem significado**, só agrupa elementos | O agrupador dos três artigos |

> **Para discutir:** quando usar `<div>` e quando usar uma tag semântica? Regra prática: se existir uma tag com o significado certo, use-a. A `div` fica para quando você só precisa agrupar.

---

## 5. Tag por tag, seção por seção

### 5.1. Cabeçalho e menu

| Tag | Uso na página |
|---|---|
| `<h1>` | O título principal. **Só um por página.** |
| `<p>` | O subtítulo (um parágrafo). |
| `<nav>`, `<ul>`, `<li>`, `<a>` | O menu é uma **lista de links**. Isso é padrão em HTML: menus são listas. |

Os links do menu usam `href="#titulos"`. O `#` significa "vá para o elemento que tem este `id` na própria página". Por isso as seções têm `id="titulos"`, `id="formatacao"` e assim por diante.

### 5.2. Títulos e parágrafos (`#titulos`)

| Tag | Efeito padrão | Observação |
|---|---|---|
| `<h2>` a `<h6>` | Títulos de nível 2 a 6, cada vez menores | O nível indica **hierarquia**, não tamanho. Não pule níveis. |
| `<p>` | Parágrafo | O navegador ignora quebras de linha do código. |
| `<br>` | Quebra de linha | Tag vazia. |
| `<hr>` | Linha horizontal | Separa assuntos. Tag vazia. |
| `<code>` | Fonte monoespaçada | Usada aqui para citar nomes de tags. |
| `<strong>` | **Negrito** com significado de importância | |

### 5.3. Formatação de texto (`#formatacao`)

Aqui estão as tags que marcam trechos dentro de um parágrafo (as **tags de texto em linha**):

| Tag | Significado | Aparência padrão |
|---|---|---|
| `<strong>` | Importância forte | Negrito |
| `<em>` | Ênfase | Itálico |
| `<b>` | Negrito sem importância extra | Negrito |
| `<i>` | Itálico para termos, pensamentos | Itálico |
| `<u>` | Texto "anotado" | Sublinhado |
| `<mark>` | Trecho destacado | Fundo amarelo |
| `<small>` | Letras miúdas | Fonte menor |
| `<del>` | Texto removido | Riscado |
| `<ins>` | Texto inserido | Sublinhado |
| `<s>` | Texto que deixou de ser correto | Riscado |
| `<sub>`, `<sup>` | Subscrito e sobrescrito | H<sub>2</sub>O, mc<sup>2</sup> |
| `<abbr title="...">` | Abreviação com explicação | Passe o mouse |
| `<dfn>` | Termo sendo definido | Itálico |
| `<q>` | Citação curta | O navegador coloca aspas |
| `<cite>` | Título de uma obra ou fonte | Itálico |
| `<time datetime="...">` | Data ou hora que o computador consegue ler | Texto normal |
| `<code>` | Trecho de código | Monoespaçada |
| `<kbd>` | Tecla do teclado | Monoespaçada |
| `<samp>` | Saída de um programa | Monoespaçada |
| `<var>` | Variável | Itálico |
| `<span>` | **Sem significado nenhum**; serve de "gancho" para o CSS | Nenhuma |

> **Observe:** `<strong>` e `<b>` parecem iguais, assim como `<em>` e `<i>`. A diferença está no **significado**: um leitor de tela lê `strong` e `em` com entonação diferente. Por isso o HTML separa significado de aparência.

### 5.4. Listas (`#listas`)

| Tag | O que é |
|---|---|
| `<ul>` | Lista **não ordenada** (com marcadores) |
| `<ol>` | Lista **ordenada** (numerada) |
| `<li>` | Cada item, usado dentro de `ul` ou `ol` |
| `<dl>`, `<dt>`, `<dd>` | Lista de **descrição**: termo (`dt`) e definição (`dd`) |

Repare na lista aninhada: um `<ul>` dentro de um `<li>`. Listas dentro de listas são permitidas.

### 5.5. Links e mídia (`#midia`)

| Tag / atributo | Uso |
|---|---|
| `<a href="#tabela">` | Link **interno**, para um `id` da própria página |
| `<a href="https://...">` | Link **externo** |
| `target="_blank"` | Abre em nova aba |
| `rel="noopener noreferrer"` | Medida de segurança para links que abrem em nova aba |
| `<a href="mailto:...">` | Abre o programa de e-mail |
| `<a href="tel:...">` | Inicia uma ligação (no celular) |
| `<figure>` e `<figcaption>` | Uma imagem (ou outro conteúdo) com **legenda** |
| `<img src="..." alt="...">` | Imagem |
| `<iframe>` | Uma página dentro da página |

Sobre a tag `<img>`:

- `src`: caminho do arquivo. Aqui é `assets/exemplo.svg` (um caminho **relativo** à pasta do HTML).
- `alt`: descrição em texto. **É obrigatório** por acessibilidade, e é o que aparece se a imagem não carregar.
- `width` e `height`: dimensões em pixels.

### 5.6. Tabela (`#tabela`)

| Tag | Função |
|---|---|
| `<table>` | A tabela inteira |
| `<caption>` | Título da tabela |
| `<thead>`, `<tbody>`, `<tfoot>` | Cabeçalho, corpo e rodapé da tabela |
| `<tr>` | Uma linha |
| `<th>` | Célula de **cabeçalho** (`scope="col"` ou `"row"` diz se cabeça coluna ou linha) |
| `<td>` | Célula de **dados** |
| `colspan` e `rowspan` | Mesclam células na horizontal e na vertical |

> **Observe:** sem CSS a tabela aparece **sem bordas**. As linhas e cores serão trabalho do CSS.

> **Importante:** tabelas servem para **dados**, não para organizar o layout da página.

### 5.7. Blocos e semântica (`#blocos`)

| Tag | Uso |
|---|---|
| `<blockquote cite="...">` | Citação longa, em bloco |
| `<footer>` dentro do `blockquote` | Indica a autoria da citação |
| `<pre>` | Texto **pré-formatado**: mantém espaços e quebras de linha |
| `<code>` dentro de `<pre>` | Bloco de código |
| `&lt;` e `&gt;` | Os símbolos `<` e `>` escritos como **texto** (senão o navegador acharia que são tags) |
| `<article>` | Os três cartões |
| `<svg>` | Desenho vetorial escrito direto no HTML |

> **Para discutir:** por que o código de exemplo usa `&lt;` e `&gt;` em vez de `<` e `>`?

### 5.8. Interativos (`#interativos`)

| Tag | Efeito |
|---|---|
| `<details>` e `<summary>` | Bloco que abre e fecha ao clicar, sem JavaScript |
| `<progress value="65" max="100">` | Barra de progresso |
| `<meter value="0.8" min="0" max="1">` | Medidor (bateria, nota, nível) |

### 5.9. Rodapé

| Tag | Uso |
|---|---|
| `<small>` | Letras miúdas, ideal para direitos autorais |
| `&copy;` | O símbolo © |
| `<address>` | Informação de contato de quem criou a página |

---

## 6. Atividades de observação

1. **Teste os links do menu.** Clique em cada um. O que faz a página rolar até a seção certa? (Procure o `id` correspondente no código.)
2. **Troque uma tag.** Pegue um `<strong>` e transforme-o em `<b>` (ou vice-versa). A aparência mudou? E o significado?
3. **Quebre o `alt`.** Apague o arquivo `assets/exemplo.svg` (ou mude o `src` para um nome errado). O que aparece no lugar da imagem?
4. **Mude os níveis de título.** Troque um `<h2>` por `<h4>`. O texto ficou menor? Por que isso **não** é um bom jeito de mudar o tamanho?
5. **Inspecione.** Clique com o botão direito em um elemento da prévia e escolha **Inspecionar**. No painel **Styles**, veja o item "user agent stylesheet": é o CSS embutido no navegador.
6. **Conte as listas.** Quantos menus de navegação existem na página? Todos são listas (`ul`)?

---

## 7. Resumo

- HTML **estrutura e dá significado** ao conteúdo; não define a aparência.
- Toda tag tem um significado: escolha a tag pelo **que o conteúdo é**, não pela aparência que ela tem por padrão.
- A aparência que você viu é o estilo padrão do navegador.
- A próxima etapa: o **mesmo conteúdo** ganha classes e é ligado a um arquivo CSS. Veja `html-com-classes.md`.
