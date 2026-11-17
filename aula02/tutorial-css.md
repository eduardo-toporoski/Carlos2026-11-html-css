# Tutorial: CSS na prática

Neste tutorial você vai **dar aparência a uma página HTML usando CSS**. O HTML já está pronto e não será alterado: tudo o que você fizer será no arquivo `tutorial1.css`, que começa vazio.

Ao final você vai saber:

- formatar **tags**, **classes** e **ids**;
- como os estilos **descem em cascata** das tags de fora para as de dentro;
- qual regra vence quando duas regras brigam pelo mesmo elemento.

---

## 0. Preparação

1. No VS Code, vá em **File → Open Folder** e abra a pasta do tutorial (a pasta, não só um arquivo).
2. Instale a extensão **Live Server** (autor: *Ritwick Dey*) na aba de extensões, se ainda não tiver.
3. Clique com o botão direito em `tutorial01.html` e escolha **Open with Live Server** (ou clique em **Go Live**, no canto inferior direito).
4. O navegador abre a página. Ela está "crua": só o estilo padrão do navegador, sem nenhum CSS seu.
5. Deixe o navegador e o VS Code **lado a lado** na tela.
6. Abra o arquivo `tutorial1.css` (vazio). A cada trecho de código deste tutorial, cole no **final** do arquivo, **salve com `Ctrl + S`** e observe a página atualizar sozinha.

> **Antes de começar:** olhe a página e o arquivo `tutorial01.html`. Identifique o `header`, o `nav`, o `main`, a `div` de introdução, os cards e o `footer`. Repare nos atributos `id` e `class` que algumas tags têm.

---

## 1. Anatomia de uma regra CSS

Toda regra CSS tem esta forma:

```
seletor {
  propriedade: valor;
  outra-propriedade: valor;
}
```

- O **seletor** diz *quem* vai ser formatado.
- Cada **declaração** (`propriedade: valor;`) diz *como*.
- Não esqueça o `;` no fim de cada declaração e as chaves `{ }`.
- Comentários em CSS ficam entre `/*` e `*/` e o navegador os ignora.

---

## 2. Seletores de tag

O jeito mais simples de formatar é usar o **nome da tag** como seletor. A regra vale para **todas** as tags daquele tipo na página.

### Passo 1 — O corpo da página

```css
/* ===== 2. SELETORES DE TAG ===== */

body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.6;
  color: #333333;
  margin: 0;
}
```

Observe: a fonte e a cor mudaram **na página inteira**, embora você só tenha mexido no `body`. Já veremos por quê. O `margin: 0` removeu a margem padrão que o navegador coloca ao redor da página.

> **Experimente:** troque `Arial, Helvetica, sans-serif` por `Georgia, serif` e por `"Courier New", monospace`. Mude o `line-height` para `1` e depois para `2.2`. Volte para os valores originais quando terminar.

### Passo 2 — Títulos

```css
h1 {
  color: #1d3557;
  font-size: 2.5rem;
}

h2 {
  color: #457b9d;
}
```

Todos os `h2` da página mudaram de cor, tanto os da introdução quanto o título "Atividades da semana".

> **Experimente:** a cor pode ser escrita de várias formas. Teste `color: red;`, `color: rgb(200, 50, 50);` e `color: #2a9d8f;`. Descubra o que acontece se você aumentar o `font-size` do `h1` para `4rem`.

### Passo 3 — Agrupando seletores

Quando várias tags recebem o mesmo estilo, separe os seletores com **vírgula**:

```css
h1, h2, h3 {
  font-family: Georgia, "Times New Roman", serif;
}
```

Os títulos ganharam uma fonte com serifa, enquanto os parágrafos continuam com a fonte do `body`.

### Passo 4 — Parágrafos

```css
p {
  max-width: 60ch;
}
```

Os parágrafos agora têm no máximo cerca de 60 caracteres por linha, o que facilita a leitura. Redimensione a janela do navegador e veja o efeito.

> **Experimente:** troque `60ch` por `30ch` e depois por `100ch`. Adicione também `text-align: justify;` e veja a diferença.

---

## 3. A cascata: dos elementos de fora para os de dentro

O "C" de CSS significa **Cascading** (em cascata). Há duas ideias importantes aqui:

1. Algumas propriedades são **herdadas**: o que você define em uma tag *pai* vale também para as tags *filhas* que estão dentro dela.
2. Quando duas regras atingem o mesmo elemento, o navegador precisa **escolher uma**.

### Passo 5 — Herança em ação: o cabeçalho

```css
/* ===== 3. CASCATA E HERANÇA ===== */

header {
  background-color: #1d3557;
  color: white;
  padding: 1rem 2rem;
}
```

Observe com atenção:

- O fundo azul e o espaçamento aparecem no cabeçalho inteiro.
- O texto "Clube de Programação" ficou **branco**, mesmo sem você ter mexido na cor dele: ele **herdou** a cor do `header`.
- Mas os **links do menu continuam azuis**. Isso acontece porque o navegador já tem um estilo próprio para a tag `a`, e ele ganha da herança.

A cor do `body` era `#333333` e a do `header` é `white`. Dentro do cabeçalho vale a **mais próxima**, ou seja, a da tag de dentro.

### Passo 6 — Seletores descendentes

Para mirar apenas nos elementos que estão **dentro** de outro, separe os seletores com **espaço**:

```css
nav ul {
  list-style: none;
  margin: 0;
  padding: 0;
  display: flex;
  gap: 1.5rem;
}

nav a {
  color: inherit;
  text-decoration: none;
}
```

- `nav ul` significa: "todo `ul` que esteja dentro de um `nav`".
- `nav a` significa: "todo `a` que esteja dentro de um `nav`".
- `color: inherit` manda o link **herdar** a cor do pai. Agora ele fica branco, igual ao resto do cabeçalho.

> **Experimente:** troque `color: inherit;` por `color: #a8dadc;`. Depois mude o `gap` para `0.5rem` e para `4rem`.

### Passo 7 — O que é herdado e o que não é

Cole este trecho **de teste**:

```css
/* TESTE — borda no main (depois comente ou apague) */
main {
  border: 3px dashed tomato;
}
```

Só o `main` ganhou a borda. Nenhum elemento dentro dele recebeu uma borda própria. Isso porque **nem toda propriedade é herdada**:

| Costuma ser **herdada** pelos filhos | **Não** é herdada pelos filhos |
|---|---|
| `color` | `background` |
| `font-family`, `font-size`, `font-weight` | `border` |
| `line-height` | `margin` e `padding` |
| `text-align` | `width` e `height` |

Faz sentido: se todos os filhos herdassem a borda do pai, a página viraria uma pilha de caixas dentro de caixas.

Agora **apague o teste** (ou transforme em comentário colocando `/*` antes e `*/` depois) e salve.

### Passo 8 — Quando duas regras brigam, a última vence

Cole este segundo teste no final do arquivo:

```css
/* TESTE — duas regras iguais (depois comente ou apague) */
h2 {
  color: crimson;
}
```

Todos os `h2` ficaram vermelhos. Você já tinha uma regra `h2 { color: #457b9d; }` mais acima. Quando duas regras têm a **mesma força**, vence a que aparece **mais abaixo** no arquivo.

> **Experimente:** recorte o bloco `h2 { color: crimson; }` e cole-o **acima** do `h2` azul. Qual cor vence agora?

Ao terminar, **apague ou comente** o teste.

---

## 4. Classes

Seletores de tag atingem *todas* as tags do tipo. E se você quiser formatar só **alguns** elementos? Para isso existem as **classes**.

- No HTML: `<article class="card">`
- No CSS: `.card { ... }`  (um **ponto** antes do nome)
- A mesma classe pode ser usada em **vários** elementos.
- Um elemento pode ter **mais de uma** classe: `class="card destaque"`.

### Passo 9 — A classe `.logo`

```css
/* ===== 4. CLASSES ===== */

.logo {
  font-size: 1.4rem;
  font-weight: bold;
  margin: 0 0 0.5rem 0;
}
```

### Passo 10 — Os cards

```css
.cards {
  display: flex;
  flex-wrap: wrap;
  gap: 1.5rem;
}

.card {
  background-color: #f1faee;
  border: 1px solid #a8dadc;
  border-radius: 12px;
  padding: 1.25rem;
  flex: 1 1 240px;
}
```

Os três cards agora ficam lado a lado, com fundo claro e cantos arredondados. Reduza a largura da janela e veja os cards se reorganizarem.

> **Experimente:** mude o `border-radius` para `0` e depois para `30px`. Troque o `background-color` e a cor da borda.

### Passo 11 — Duas classes no mesmo elemento

O segundo card, no HTML, é `class="card destaque"`. Ele usa **duas classes ao mesmo tempo**. Vamos estilizar a segunda:

```css
.destaque {
  background-color: #ffe8a3;
  border-color: #f4a261;
}
```

O card do meio ficou amarelo, mas continua com os cantos arredondados e o espaçamento de `.card`. Os estilos das duas classes **se somam**.

> **Experimente:** recorte o bloco `.destaque` e cole **antes** do bloco `.card`. O card deixa de ser amarelo! Por quê? (Dica: releia o Passo 8.) Depois devolva o bloco para o final.

### Passo 12 — Links que parecem botões

```css
.botao {
  display: inline-block;
  background-color: #1d3557;
  color: white;
  padding: 0.5rem 1rem;
  border-radius: 6px;
  text-decoration: none;
}

.botao:hover {
  background-color: #e63946;
}
```

`.botao:hover` é um estilo que só vale **enquanto o mouse está sobre** o botão. Passe o mouse e veja.

> **Experimente:** adicione `class="botao"` a outro link do HTML (por exemplo, um dos links do menu) e veja o resultado. Depois desfaça.

---

## 5. Ids

Um `id` identifica **um único elemento** da página. Por isso ele **não pode se repetir** no mesmo HTML.

- No HTML: `<div id="introducao">`
- No CSS: `#introducao { ... }`  (uma **cerquilha** antes do nome)

Procure no HTML os ids que já existem: `topo`, `introducao`, `atividades` e `contato`. (Eles também servem como destino dos links do menu.)

### Passo 13 — Formatando por id

```css
/* ===== 5. IDS ===== */

#topo {
  border-bottom: 4px solid #e63946;
}

#introducao {
  background-color: #e9f1f7;
  padding: 2rem;
}

#atividades {
  padding: 2rem;
}

#contato {
  background-color: #14213d;
  color: #e5e5e5;
  text-align: center;
  padding: 1.5rem;
}
```

Cada região da página ganhou sua própria identidade. Note o `text-align: center` no rodapé: ele é herdado pelos parágrafos de dentro.

### Passo 14 — Combinando id e tag

Você pode misturar os tipos de seletor para ser mais específico:

```css
#introducao h2 {
  border-bottom: 2px solid #a8dadc;
  padding-bottom: 0.3rem;
}
```

Esta regra só atinge os `h2` **dentro** do elemento de id `introducao`. O `h2` "Atividades da semana" não é afetado.

> **Experimente:** crie a regra `#contato p { margin: 0.3rem; }` e veja o que muda. Depois escreva uma regra `#atividades h3` que mude a cor dos títulos dos cards.

---

## 6. Tag, classe ou id: quem vence?

Já vimos que a ordem importa. Mas existe uma regra **mais forte** que a ordem: a **especificidade**.

> **id  >  classe  >  tag**

Uma regra com id vence uma regra com classe, que vence uma regra com tag, **não importa qual esteja mais abaixo no arquivo**.

### Passo 15 — Teste de força

O título "Atividades da semana" é `<h2 class="titulo-secao">`. Ele é, ao mesmo tempo, uma **tag** `h2` e membro de uma **classe**. Cole os trechos um de cada vez, salvando e observando a cor desse título:

```css
/* ===== 6. QUEM VENCE? ===== */

.titulo-secao {
  color: #2a9d8f;
}
```

O título fica verde.

Agora cole **depois** dele uma regra de tag:

```css
h2 {
  color: #e76f51;
}
```

Os `h2` da introdução ficam laranja (a regra de tag mais abaixo venceu a anterior, como no Passo 8). Mas o título "Atividades da semana" **continua verde**: a **classe** vence a **tag**, mesmo a tag estando mais abaixo.

Por fim, cole:

```css
#atividades h2 {
  color: #6a4c93;
}
```

O título passa a ser roxo: o **id** vence a classe.

| Seletor | Tipo | Força |
|---|---|---|
| `h2` | tag | fraca |
| `.titulo-secao` | classe | média |
| `#atividades h2` | id + tag | forte |

> **Experimente:** apague a regra com `#atividades` e confirme que o título volta a ficar verde. Depois mude a ordem das regras e observe que o resultado não muda.

---

## 7. Descubra quem manda: as ferramentas do navegador

Quando um estilo não funciona como você espera, o navegador mostra o que está acontecendo:

1. Clique com o botão direito em qualquer elemento da página e escolha **Inspecionar** (ou aperte `F12`).
2. No painel **Styles**, veja todas as regras que atingem aquele elemento.
3. As declarações **riscadas** são as que **perderam** a disputa.
4. Você pode **editar valores ali mesmo** para testar ideias. As mudanças desaparecem ao recarregar a página; não alteram seu arquivo.

> **Experimente:** inspecione o título "Atividades da semana". Quais regras aparecem riscadas? Por quê?

---

## 8. Desafios livres

Agora a página é sua. Mude o que quiser, só no `tutorial1.css`:

1. **Troque a paleta.** Escolha 3 ou 4 cores novas e substitua em todo o arquivo. (Dica: `Ctrl + H` faz localizar e substituir.)
2. **Troque as fontes.** Experimente `Verdana`, `Trebuchet MS` e `Courier New`.
3. **Dê vida aos cards.** Adicione `.card:hover { transform: translateY(-4px); }` e `box-shadow: 0 4px 10px rgba(0,0,0,0.15);`.
4. **Estilize o rodapé** e o `main` com uma largura máxima: `main { max-width: 900px; margin: 0 auto; }`.
5. **Crie uma classe nova**, por exemplo `.aviso`, e aplique-a em um dos parágrafos editando o HTML (`<p class="aviso">`).
6. **Quebre de propósito.** Esqueça um `;`, apague uma chave `}` ou troque `.card` por `card` (sem o ponto). O que acontece? Aprender a reconhecer os erros faz parte do trabalho.

---

## 9. Resumo

| Quero formatar... | No CSS escrevo | No HTML preciso de... |
|---|---|---|
| todas as tags de um tipo | `p { ... }` | nada |
| vários tipos de tag | `h1, h2 { ... }` | nada |
| só o que está dentro de algo | `nav a { ... }` | nada |
| um grupo de elementos | `.card { ... }` | `class="card"` |
| um único elemento | `#topo { ... }` | `id="topo"` |

Lembre-se:

- **Herança:** cor, fonte e alinhamento descem do pai para os filhos; fundo, borda e espaçamentos não.
- **Ordem:** com a mesma força, vence a regra que vem mais abaixo.
- **Especificidade:** `id` vence `classe`, que vence `tag`.
- **Comentários:** `/* assim */`.

### Para pensar

1. Por que o texto do cabeçalho ficou branco sem você mexer na cor dele, mas os links não?
2. Por que o card amarelo deixou de ser amarelo quando a regra `.destaque` veio antes de `.card`?
3. Por que `#introducao h2` não afetou o título "Atividades da semana"?
4. Em que situação vale mais a pena usar uma classe do que um id?
