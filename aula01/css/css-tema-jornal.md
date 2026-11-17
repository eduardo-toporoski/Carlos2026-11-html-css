# Tema Jornal: explicando o CSS

Arquivo: `css/tema-jornal.css`

## Ideia do tema

Uma página que parece um **jornal impresso**: papel amarelado, tinta preta, fonte com serifa e **filetes** (linhas finas e duplas) separando as áreas. Quase não usa cor. A hierarquia vem do **tamanho, peso e posição do texto**, e não de cores.

O destaque técnico deste arquivo é a **tipografia**: justificado, hifenização, primeira letra grande e uma coluna de leitura estreita.

---

## 1. Variáveis

```css
:root {
  --papel: #f7f3e8;
  --tinta: #1a1a1a;
  --suave: #555;
  --filete: #1a1a1a;
}
```

Apenas quatro valores, quase todos "preto sobre papel". Para um tema com poucas cores, a paleta cabe em quatro linhas. Note que `--filete` e `--tinta` têm o mesmo valor: se você quisesse linhas cinzas, bastaria mudar só `--filete`.

---

## 2. Texto base

```css
body.pagina {
  background: var(--papel);
  color: var(--tinta);
  font-family: Georgia, "Times New Roman", serif;
  font-size: 1.1rem;
  line-height: 1.7;
}
```

- `serif` = fontes com **serifa** (os "pezinhos" nas letras), típicas de jornais e livros.
- `line-height: 1.7` é maior do que no tema corporativo: **textos com serifa ficam mais legíveis com mais respiro entre linhas**.

---

## 3. A "capa": cabeçalho e menu

```css
.topo {
  max-width: 820px;
  margin: 2rem auto 0;
  text-align: center;
  border-bottom: 4px double var(--filete);
}
```

- `max-width` + `margin: auto` centralizam uma coluna estreita (como a de um jornal).
- `border-bottom: 4px double` desenha o **filete duplo** (duas linhas finas). É o efeito de "linha dupla" típico de impressos.

```css
.topo h1 {
  font-size: clamp(2.6rem, 8vw, 4.6rem);
  font-weight: 900;
  letter-spacing: -.02em;
  line-height: 1.05;
}
```

- `clamp(mínimo, ideal, máximo)` define um tamanho que **acompanha a largura da tela** (`8vw` = 8% da largura), mas nunca fica menor que 2,6rem nem maior que 4,6rem.
- `letter-spacing` negativo aproxima as letras: um recurso de títulos de capa.
- `line-height: 1.05` aperta as linhas do título, para que as linhas de um título grande não fiquem soltas.

```css
.menu { border-top: 1px solid var(--filete); padding: .5rem 0; }
.menu a { color: var(--tinta); text-decoration: none; }
.menu a:hover { text-decoration: underline; }
```

O menu é uma faixa fina entre dois filetes. Nenhum botão e nenhum fundo: o link só ganha **sublinhado** ao passar o mouse.

---

## 4. Seções, títulos e parágrafos

```css
.secao { padding: 1.2rem 0; border-bottom: 1px solid var(--filete); }
.secao h2 { font-size: 2rem; border-bottom: 3px solid var(--filete); }
.secao h3 { font-size: 1.3rem; font-style: italic; }
```

Em vez de cartões, cada seção é separada por **uma linha**. Os níveis de título se distinguem por tamanho, grossura de linha e itálico.

```css
p { text-align: justify; hyphens: auto; }
```

- `text-align: justify` alinha o texto nos dois lados, como em jornal.
- `hyphens: auto` deixa o navegador dividir palavras no fim da linha (usando o idioma declarado no `<html lang="pt-BR">`). Sem isso, o justificado cria "buracos" feios entre as palavras.

### A letra capitular

```css
.destaque::first-letter {
  float: left;
  font-size: 4.2rem;
  line-height: .85;
  padding: .25rem .5rem 0 0;
  font-weight: 900;
}
```

- `::first-letter` é um **pseudo-elemento**: ele seleciona a **primeira letra** do parágrafo, sem precisar mudar o HTML.
- `float: left` faz a letra "flutuar" à esquerda e o texto contornar.

---

## 5. Detalhes de texto

```css
ins { text-decoration: underline double; }
.etiqueta { font-variant: small-caps; border: 1px solid var(--filete); }
```

- `underline double` gera sublinhado duplo.
- `small-caps` troca as minúsculas por **versaletes** (maiúsculas pequenas).

Nos demais itens (`mark`, `code`, `kbd`), o tema continua **discreto**: quase tudo é só fonte monoespaçada ou um contorno fino.

---

## 6. Imagem, tabela e citação

```css
.figura img { filter: grayscale(1) contrast(1.1); border: 1px solid var(--filete); padding: 6px; background: #fff; }
```

- `filter: grayscale(1)` deixa a imagem **em preto e branco**, em coerência com a paleta.
- `padding` + `background` + `border` criam uma "moldura de foto".

```css
.tabela thead th { border-top: 3px solid var(--filete); border-bottom: 1px solid var(--filete); }
.tabela td { border-bottom: 1px solid #bbb; }
.tabela tfoot td { border-top: 3px double var(--filete); }
```

Em vez de uma grade completa, a tabela usa **só linhas horizontais**. É um estilo editorial clássico, mais limpo. O rodapé fecha com um filete duplo.

```css
.citacao {
  font-size: 1.3rem;
  font-style: italic;
  border-top: 1px solid var(--filete);
  border-bottom: 1px solid var(--filete);
}
```

Citação em tamanho grande e itálico, entre dois filetes: o "pull quote" das revistas.

---

## 7. Colunas separadas por filetes

```css
.cartoes { display: grid; grid-template-columns: repeat(3, 1fr); }
.cartao { padding: 0 1rem; border-left: 1px solid var(--filete); }
.cartao:first-child { border-left: 0; padding-left: 0; }
```

- `repeat(3, 1fr)` cria **3 colunas de larguras iguais** (`fr` = fração do espaço disponível).
- Cada cartão tem uma linha à esquerda, **exceto o primeiro** (`:first-child` seleciona o primeiro filho de um grupo). Assim as colunas ficam separadas, como num jornal.

---

## 8. Lateral e rodapé

```css
.lateral { margin: 1.5rem 0; padding: 0 1.2rem 1rem; border: 4px double var(--filete); }
```

A caixa "Você sabia?" ganha **moldura dupla**, como um box de destaque em jornal.

O rodapé repete a linha dupla do topo, fechando a página de forma simétrica.

---

## 9. Adaptação ao celular

```css
@media (max-width: 640px) {
  .cartoes { grid-template-columns: 1fr; }
  .cartao { border-left: 0; padding: 0; }
  p { text-align: left; }
}
```

`@media` é uma **condição**: as regras dentro dela só valem quando a tela tem **até 640px de largura**. Aqui as três colunas viram uma, e o texto deixa de ser justificado (em coluna estreita, o justificado fica ruim).

Redimensione a janela do navegador para ver o efeito.

---

## Para experimentar

1. Em `:root`, mude `--papel` para `#ffffff` e depois para `#e9e4d0`.
2. Apague `hyphens: auto` e compare o justificado numa janela estreita.
3. Em `.cartoes`, troque `repeat(3, 1fr)` por `repeat(2, 1fr)` (como fica o terceiro cartão?).
4. Remova o bloco `.destaque::first-letter` e veja a capitular sumir.
5. Em `.figura img`, tire o `filter`. A imagem ganha cores. Ela combina com o resto?
6. Troque `Georgia` por `"Courier New"` em `body.pagina`. O tema ainda parece jornal?
