# HTML com classes: o CSS cuida da aparência

Arquivo desta etapa: `02-html-com-classes.html`

## 1. A ideia

Na etapa anterior você viu a página **sem CSS**. Agora você vai abrir `02-html-com-classes.html`, que tem **o mesmo conteúdo e as mesmas tags**, com duas diferenças:

1. Algumas tags ganharam o atributo **`class`**, que funciona como uma etiqueta: `<header class="topo">`.
2. O `<head>` tem uma linha nova, a que liga a página a um arquivo de estilos:

```html
<link rel="stylesheet" href="css/tema-corporativo.css">
```

O trabalho desta etapa é **trocar o nome do arquivo nessa linha**, salvar e ver o que acontece. O HTML do `<body>` não muda em nenhum momento. Se a página fica completamente diferente, quem fez isso foi o CSS.

> **A lição:** o HTML é a estrutura; o CSS é a aparência. Podemos trocar a roupa inteira sem mexer no corpo.

---

## 2. Como fazer a troca

1. Abra `02-html-com-classes.html` no VS Code e a prévia ao lado (Live Preview: botão direito no arquivo, **Show Preview**).
2. No `<head>`, procure a linha com `<link rel="stylesheet" ...>`. Há um comentário logo acima dela listando as quatro opções.
3. Troque o nome do arquivo para o próximo tema:
   - `css/tema-corporativo.css`
   - `css/tema-jornal.css`
   - `css/tema-terminal.css`
   - `css/tema-pop.css`
4. Salve com `Ctrl + S` e observe a prévia.

> Se o caminho estiver errado, a página volta a ficar "crua". Confira se está escrito `css/` antes do nome e se o nome tem `.css` no final.

---

## 3. O que são as classes

Uma classe é um **nome que damos a um elemento** para que o CSS possa encontrá-lo. No HTML:

```html
<article class="cartao">...</article>
```

No CSS, a classe aparece com um ponto na frente:

```css
.cartao { ... }
```

Cada tema CSS escreve as suas próprias regras para os **mesmos nomes de classe**. Por isso o conteúdo continua igual e a aparência muda.

### As classes usadas nesta página

| Classe | Em qual elemento | O que representa |
|---|---|---|
| `pagina` | `<body>` | A página inteira |
| `topo` | `<header>` | O cabeçalho |
| `menu` | `<nav>` do topo | O menu de navegação |
| `principal` | `<main>` | O conteúdo principal |
| `secao` | cada `<section>` (7 vezes) | Cada bloco numerado |
| `destaque` | primeiro parágrafo | Parágrafo de abertura, em evidência |
| `divisor` | `<hr>` | A linha separadora |
| `etiqueta` | um `<span>` | Um trecho de texto rotulado |
| `botao` | um `<a>` | Um link com cara de botão |
| `figura` | `<figure>` | A imagem com legenda |
| `moldura` | `<iframe>` | A página incorporada |
| `tabela` | `<table>` | A tabela |
| `citacao` | `<blockquote>` | A citação em bloco |
| `codigo` | `<pre>` | O bloco de código |
| `cartoes` | `<div>` | O agrupador dos três cartões |
| `cartao` | cada `<article>` (3 vezes) | Um cartão |
| `icone` | `<svg>` | O desenho SVG |
| `sanfona` | `<details>` | O bloco que abre e fecha |
| `lateral` | `<aside>` | A caixa "Você sabia?" |
| `rodape` | `<footer>` | O rodapé |

Perceba que **nem tudo tem classe**. Os temas também formatam as próprias tags (`h2`, `code`, `mark`, `kbd`, `li` etc.), muitas vezes **usando a classe como ponto de partida** (por exemplo, "todo `h2` que estiver dentro de uma `secao`").

---

## 4. Os quatro temas, em termos gerais

Cada tema tem um guia próprio explicando seu CSS. Aqui está o que você precisa para a aula.

### Tema 1: Corporativo (`tema-corporativo.css`)

- **Impressão geral:** institucional, limpo, parecido com o site de uma empresa ou escola.
- **Cores:** azul e vermelho sobre fundo cinza-azulado claro.
- **Fonte:** sem serifa (letras sem "pezinhos").
- **Layout:** cabeçalho azul com menu em linha; cada seção vira um **cartão branco** com sombra suave; os três artigos ficam lado a lado.
- **Guia:** `css-tema-corporativo.md`

### Tema 2: Jornal (`tema-jornal.css`)

- **Impressão geral:** página de jornal ou revista impressa.
- **Cores:** preto sobre papel amarelado, quase sem cor.
- **Fonte:** com serifa, texto justificado, primeira letra grande no parágrafo de abertura.
- **Layout:** uma coluna centralizada, separada por **filetes** (linhas finas e duplas); a imagem fica em preto e branco.
- **Guia:** `css-tema-jornal.md`

### Tema 3: Terminal (`tema-terminal.css`)

- **Impressão geral:** o visual de um terminal de programação antigo.
- **Cores:** fundo escuro com texto âmbar e detalhes em verde.
- **Fonte:** monoespaçada (todas as letras com a mesma largura).
- **Layout:** o cabeçalho e o menu **viram uma barra lateral fixa** à esquerda. Detalhe curioso: símbolos como `$`, `>` e `##` aparecem na tela **sem estarem no HTML**.
- **Guia:** `css-tema-terminal.md`

### Tema 4: Pop (`tema-pop.css`)

- **Impressão geral:** divertido, chamativo, estilo "brutalista".
- **Cores:** amarelo, rosa, azul e verde fortes, com contorno preto.
- **Fonte:** arredondada, com títulos em letras grossas e maiúsculas.
- **Layout:** bordas grossas, sombras duras (sem desfoque) e elementos **levemente tortos**. Os botões se mexem quando o mouse passa.
- **Guia:** `css-tema-pop.md`

---

## 5. Roteiro da atividade

### Parte A: veja cada tema

Para cada um dos quatro temas, faça o seguinte:

1. Troque o `<link>`, salve e olhe a página do topo ao fim.
2. Anote **três diferenças** que você percebeu em relação ao tema anterior (cor, fonte, espaçamento, posição das coisas).
3. Responda: **o texto mudou?** Se mudou, por quê? (Dica: não mudou.)

### Parte B: o que o HTML puro mostrava, o CSS resolve

Compare com a versão `01-html-puro.html` e procure como cada tema mostra:

1. A **tabela**: com bordas, listras, cores?
2. O **menu**: uma lista com marcadores ou uma barra de botões?
3. A **citação em bloco**: como cada tema destaca que aquilo é uma citação?
4. O **bloco de código**: fundo claro ou escuro?
5. As tags `<mark>`, `<del>`, `<ins>` e `<kbd>`: continuam reconhecíveis em todos os temas?

### Parte C: experimentos

Faça cada um e depois **desfaça**:

1. **Sem CSS:** apague (ou comente com `<!--` e `-->`) a linha do `<link>`. A página volta a ser a versão pura?
2. **Caminho errado:** escreva `css/tema-xxx.css`. O que acontece? É preciso mexer em algo além do nome do arquivo para corrigir?
3. **Dois temas ao mesmo tempo:** deixe duas linhas `<link>` no `<head>`, por exemplo o Corporativo e depois o Pop. Qual aparência prevalece? O que acontece se você inverter a ordem das linhas?
4. **Mexa em um tema:** abra `css/tema-corporativo.css`, ache `--azul` no começo do arquivo e troque o código da cor. Salve e veja o que mudou na página.
5. **Retire uma classe:** no HTML, apague `class="topo"` do `<header>`. O que acontece com o cabeçalho? (Isso mostra como o CSS **encontra** os elementos.)
6. **Crie uma classe:** adicione `class="destaque"` a outro parágrafo. O que muda? Em quais temas o efeito é visível?

### Parte D: discussão

1. Se uma empresa quisesse um **modo escuro**, quais arquivos teria que alterar: o HTML, o CSS ou ambos?
2. Por que é uma boa ideia ter **vários** arquivos CSS em vez de misturar o estilo dentro do HTML?
3. Alguns temas mudam o **posicionamento** (como a barra lateral do Terminal). Isso contradiz a ideia de que "o HTML cuida da estrutura"? Por quê?
4. Qual tema você usaria para um site de notícias? Para um blog de programação? Para uma loja de brinquedos?

---

## 6. Resumo

- O **mesmo HTML** pode ter aparências totalmente diferentes: quem manda nisso é o CSS.
- As **classes** são as etiquetas que permitem ao CSS encontrar e formatar elementos específicos.
- A tag `<link rel="stylesheet" href="...">` conecta o HTML a um arquivo CSS.
- Trocar de tema é trocar **uma linha** do HTML.
- Próxima etapa: ler os guias de cada CSS e entender **como** cada efeito foi feito.
