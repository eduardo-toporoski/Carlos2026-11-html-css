# Tema Pop: explicando o CSS

Arquivo: `css/tema-pop.css`

## Ideia do tema

O oposto do tema Corporativo: **cores fortes, contornos pretos grossos, sombras duras e elementos levemente tortos**. É um estilo chamado de *neo-brutalismo* ou *pop*, muito usado em sites jovens e divertidos.

Este tema ensina uma lição importante: com poucas propriedades repetidas (**borda grossa + sombra sem desfoque + cores chapadas**) já se cria uma identidade visual forte.

---

## 1. Variáveis, inclusive de "pedaços" de regra

```css
:root {
  --amarelo: #ffe03d;
  --rosa: #ff5fa2;
  --azul: #3d7bff;
  --verde: #3ddc97;
  --preto: #111;
  --branco: #fff;
  --borda: 3px solid var(--preto);
  --sombra: 6px 6px 0 var(--preto);
}
```

Além de cores, as variáveis guardam **valores compostos**:

- `--borda` guarda "3px solid preto": uma borda completa.
- `--sombra` guarda "6px para a direita, 6px para baixo, 0 de desfoque, preto".

Depois basta escrever:

```css
.secao { border: var(--borda); box-shadow: var(--sombra); }
```

Todas as caixas ficam com o mesmo "acabamento", e mudando as duas variáveis **o tema inteiro muda de espessura**. Experimente trocar `3px` por `1px` ou `6px`.

---

## 2. A sombra dura: o coração do visual

```css
box-shadow: 6px 6px 0 var(--preto);
```

Os valores são: deslocamento horizontal, deslocamento vertical, **desfoque** e cor. No tema Corporativo o desfoque era pequeno e a cor transparente (sombra suave). Aqui o desfoque é `0`: a sombra é um **bloco sólido** deslocado, que dá a impressão de uma peça de papel recortada sobre outra.

---

## 3. Base

```css
body.pagina {
  background: var(--amarelo);
  color: var(--preto);
  font-family: "Trebuchet MS", "Arial Rounded MT Bold", Verdana, sans-serif;
  font-size: 1.05rem;
  line-height: 1.6;
}
```

Fundo amarelo chapado e uma fonte arredondada e amigável.

---

## 4. Cabeçalho torto

```css
.topo h1 {
  display: inline-block;
  padding: .2em .6em;
  background: var(--branco);
  border: var(--borda);
  box-shadow: var(--sombra);
  font-family: Impact, "Arial Black", sans-serif;
  font-size: clamp(2.2rem, 7vw, 3.8rem);
  text-transform: uppercase;
  transform: rotate(-2deg);
}
```

| Propriedade | Efeito |
|---|---|
| `display: inline-block` | O título passa a ocupar **só a largura do texto** (e não a linha inteira), para a caixa branca abraçar o texto |
| `font-family: Impact` | Fonte grossa e compacta, típica de cartazes |
| `text-transform: uppercase` | Mostra o texto em **maiúsculas**, **sem mudar** o texto do HTML |
| `transform: rotate(-2deg)` | **Gira** o título 2 graus no sentido anti-horário |
| `clamp(...)` | Tamanho que acompanha a largura da tela, com mínimo e máximo |

`transform` não mexe nos outros elementos: o título gira "por cima" do layout, sem empurrar nada.

---

## 5. Menu em forma de botões

```css
.menu a {
  display: block;
  padding: .4rem 1rem;
  background: var(--branco);
  border: var(--borda);
  box-shadow: 4px 4px 0 var(--preto);
  font-weight: 700;
  text-decoration: none;
}
.menu a:hover {
  background: var(--verde);
  transform: translate(2px, 2px);
  box-shadow: 2px 2px 0 var(--preto);
}
```

O efeito do botão sendo "apertado" tem dois ingredientes ao passar o mouse:

1. `transform: translate(2px, 2px)` **desloca** o botão 2px para baixo e para a direita;
2. a sombra **diminui** de 4px para 2px.

Juntos, dão a sensação de que o botão afundou. É o tipo de detalhe que dá vida a um tema e custa duas linhas de código.

(O mesmo recurso é usado em `.botao:hover`.)

---

## 6. Seções com etiqueta torta

```css
.secao {
  background: var(--branco);
  border: var(--borda);
  box-shadow: var(--sombra);
  padding: 1.2rem 1.6rem 1.6rem;
  margin-bottom: 2.2rem;
}

.secao h2 {
  display: inline-block;
  margin: -2rem 0 1rem -2.2rem;
  padding: .2em .7em;
  background: var(--azul);
  color: var(--branco);
  border: var(--borda);
  font-family: Impact, "Arial Black", sans-serif;
  text-transform: uppercase;
  transform: rotate(-1.5deg);
}
```

O título de cada seção parece uma **etiqueta colada** na quina do cartão. O truque são as **margens negativas**:

- `margin-top: -2rem` puxa o título para **cima**, para fora da caixa;
- `margin-left: -2.2rem` puxa para a **esquerda**.

Margens negativas fazem o elemento "sair" do espaço onde estaria. Junto com a rotação, dão o efeito de adesivo.

---

## 7. Cartões coloridos e inclinados

```css
.cartoes { display: grid; grid-template-columns: repeat(auto-fit, minmax(210px, 1fr)); gap: 1.4rem; }

.cartao:nth-child(1) { background: #ffd0e5; transform: rotate(-1.5deg); }
.cartao:nth-child(2) { background: #cfe0ff; transform: rotate(1deg); }
.cartao:nth-child(3) { background: #c8f7e0; transform: rotate(-.5deg); }
```

- `:nth-child(1)`, `(2)`, `(3)` escolhem o **primeiro, segundo e terceiro** cartão do grupo. Assim, cada um recebe uma cor e uma inclinação diferentes **sem precisar de classes extras no HTML**.
- A grade se adapta à largura da tela, como no tema Corporativo.

A mesma ideia de inclinar aparece em outros elementos:

```css
.figura   { transform: rotate(1deg); }
.citacao  { background: var(--rosa); transform: rotate(-.7deg); }
.lateral  { background: var(--verde); transform: rotate(.8deg); }
```

Cada elemento gira em direção e ângulo diferentes, para a página parecer **montada à mão**, como uma colagem.

---

## 8. Detalhes de texto

```css
mark { background: var(--rosa); padding: 0 .25em; }
kbd  { background: var(--branco); border: 2px solid var(--preto); box-shadow: 2px 2px 0 var(--preto); }
.etiqueta { background: var(--verde); border: 2px solid var(--preto); border-radius: 99px; }
dt { background: var(--amarelo); display: inline-block; border: 2px solid var(--preto); }
li::marker { color: var(--rosa); font-weight: 700; }
```

- A mesma linguagem se repete em tudo: **contorno preto + cor chapada** (e sombra dura, quando é um elemento maior). Essa repetição é o que deixa o tema coeso.
- `li::marker` pinta só o **marcador** da lista.

---

## 9. Tabela, código e interativos

```css
.tabela { border-collapse: collapse; border: var(--borda); }
.tabela th { background: var(--preto); color: var(--amarelo); }
.tabela tbody tr:nth-child(odd) { background: #fff6bf; }
.tabela tbody tr:hover { background: #ffd0e5; }
```

Cabeçalho preto com letras amarelas, linhas **ímpares** (`odd`) em amarelo-claro (zebrado) e linha rosada ao passar o mouse.

```css
.codigo { background: var(--preto); color: var(--verde); border: var(--borda); box-shadow: 5px 5px 0 var(--rosa); }
```

O bloco de código usa uma **sombra colorida** (rosa), e não preta, para sair do padrão.

```css
progress, meter { width: 220px; height: 1.2rem; accent-color: var(--rosa); }
.sanfona { border: var(--borda); background: var(--amarelo); }
```

---

## 10. Rodapé e celular

```css
.rodape { background: var(--preto); color: var(--amarelo); border-top: var(--borda); text-align: center; }
.rodape a { color: var(--rosa); }
```

O rodapé inverte as cores: fundo preto, texto amarelo e links rosa.

```css
@media (max-width: 640px) {
  .secao h2 { margin-left: -.5rem; }
}
```

Em telas pequenas, o título "etiqueta" não pode sair tanto para a esquerda, senão ficaria cortado pela borda da tela. O `@media` reduz a margem negativa só nesse caso.

---

## Para experimentar

1. Mude `--borda` para `1px solid var(--preto)` e veja o tema virar uma versão "delicada".
2. Mude `--sombra` para `0 0 0 var(--preto)`. O visual perde força? Por quê?
3. Zere todas as `rotate(...)` (troque por `rotate(0deg)`). A página fica "arrumadinha demais"?
4. Em `.menu a:hover`, apague a linha do `transform`. O efeito de apertar continua?
5. Troque as quatro cores principais por uma paleta que você goste (por exemplo, tons de laranja e roxo).
6. Crie um quarto cartão no HTML (copie um `<article class="cartao">`). Que cor ele recebe? (Dica: nenhuma regra `:nth-child(4)` existe.)
