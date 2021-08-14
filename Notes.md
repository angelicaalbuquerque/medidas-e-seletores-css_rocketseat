## Nem Tudo São Pixels

Cada propriedade possui valores `property: value` e esse estudo de propriedades e valores é constante.

Para conhecer e estudar os valores, podemos verificar a [documentação oficial MDN](https://developer.mozilla.org/pt-BR/), que sempre mostrará os valores (ou data types) como os exemplos `<color>` e `<length>`.

### Tipos numéricos e unidades comuns

_Tipos numéricos:_<br>
`<integer>`: Número inteiro, como -45 ou 560;<br>
`<number>`: Número decimal, como -3.6, 64 ou 0.042;<br>
`<dimension>`: É um `<number>` com uma unidade junto, como 90deg, 2s, 8px;<br>
`<percentagem>`: Representa a fração de outro número.
<br><br>
_Unidades comuns:_<br>
`<length>`: Representa um valor de distância, como px, em, vw;<br>
`<angle>`: Representa um ângulo, como deg, rad, turn;<br>
`<time>`: Representa um temp, como s, ms;<br>
`<resolution>`: Representa resoluções para dispositivos, como dpi.<br>

### Distâncias absolutas e relativas

**Distâncias absulutas (`<length>`)**<br>
São fixas e não alteram seu valor.

| Unidade | Nome               | Equivalência        |
| ------- | ------------------ | ------------------- |
| cm      | Centímetros        | 1cm = 96px/2.54     |
| in      | Inches (polegadas) | 1in = 2.54cm = 96px |
| px      | Pixels             | 1px = 1/96th of 1in |

O mais comum e utilizado é o pixel, uma vez que todas as telas têm tamanhos de pixels. Por outro lado, não é recomendado utilizar cm.

**Distâncias relativas**<br>
São relativas a algum outro valor. Pode ser o elemento pai, um root ou o tamanho da tela.

Como benefício, tem-se a maior adaptação aos diferentes tipos de tela.

| Unidade | Relativo a                                    |
| ------- | --------------------------------------------- |
| em      | Tamanho da fonte do pai                       |
| rem     | Tamanho da fonte do elemento raiz (root/html) |
| vw      | 1% da viewport de largura (width)             |
| vh      | 1% da viewport de altura (height)             |

Tamanho da fonte do pai: <br>
Significa que se eu tiver uma `div` com um tamanho fixo de, por exemplo, **font-size: 18px;**, e colocar um `p` com **font-size: 1em;**, vai significar que o paráfrafo terá a fonte do tamanho que foi definido da fonte do pai (18px). Agora, se eu colocar esse parágrafo com **font-size: 2em;**, ele valerá **36px** (18px \* 2).

Tamanho da fonte do elemento raiz: <br>
Caso não tenha definido o valor da `div`, será buscado o valor do elemento raiz (root) HTML, definido pelo navegador.<br>
É possível também ir direto para o valor raiz mesmo tendo definido um valor para fonte da `div`, basta utilizar `rem`.

Exemplo:

```CSS
div {
  font-size: 32px;
}

p {
  font-size: 1.6rem;
}
```

Eu posso alterar o elemento root, aliás, utilizando `:root {}` ou `html {}`:

```CSS
html {
  font-size: 14px;
}
```

**viewport**:
É relativo ao dispositivo, ao que está aparecendo na tela. Aplicar a unidade relativa ao viewport significa que temos 100% de largura/altura e podemos escolher quantos "%" dessa área utilizar.

### Porcentagens

Em muitos casos é tratado da mesma maneira que as distâncias `<length>` e sempre será relativo a algum valor.

Exemplo 1:

```CSS
html {
  font-size: 50%;
}
```

Nesse caso específico, temos algo que já está sendo computado pelo navegador e, então, estou fazendo 50% do valor padrão (no caso, 16px).

Exemplo 2:

```CSS
li {
  font-size: 80%;
}
```

Em casos de listas, o estilo é aplicado em cascata, basicamente, sendo em relação ao pai. Se eu tenho uma lista com 3 elementos, o 3º elemento terá 80% em cima do 2º elemento que, por sua vez, terá 80% em cima do 1º elemento (pai).

Exemplo 3:

```CSS
div {
  background-color: blue;
  width: 100%;
  height: 100%;
}
```

Nesse caso, o elemento é aplicado na largura e altura de 100% do body. Se eu altero a largura do body, significa que estarei alterando a largura do pai dele (HTML). Sendo assim, o tamanho da largura da div será 50% do 50% do body, ou seja, a metade da metade da largura do elemento raiz.

```CSS
body {
  width: 50%;
}

div {
  background-color: blue;
  width: 50%;
  height: 100%;
}
```

### Position

`<position>` é um tipo de valor que representa um conjunto de coordenadas 2D: top, right, bottom, left e center.

É utilizado para alguns tipos de propriedades e, inclusive, o valor `<position>` não deve ser confundido com a propriedade `position`.

No exemplo abaixo, consigo mexer nos valores de background-position e ajustar a imagem como eu quero. Desse jeito, a ponta direita da imagem ficará no canto direito da tela e abaixado 50px do topo.

```HTML
<div class=box></div>
```

```CSS
.box {
  height: 300px;
  width: 400px;
  background-image: url(http://source.unsplash.com/random);
  background-repeat: no-repeat;
  background-position: right 50px;
}
```

_Teste brincar ao mudar `<background-position>` para `bottom left`, `center`, `left top`, `bottom right` e `top left`, por exemplo._

### Funções

Em programação, funções são reconhecidas por causar um reaproveitamento de código.

Algumas funções em CSS que podemos utilizar:

- rgb();
- hsl();
- url();
- calc().

Lembrando que, por exemplo, `rgb` é o nome da função e que, dentro dos parênteses, ela recebe valores (argumentos) que serão calculados e retornados.

No exemplo abaixo, eu não sei qual é a altura que quero da imagem, mas o que eu sei é que quero que essa imagem fique sempre na metade da tela e tenha ainda mais 20px.

Primeiramente, como o `body` não tem uma altura definida por padrão e vai sempre se expandir dependendo do elemento que tem dentro, precisamos definir a porcentagem:

```CSS
body {
  height: 100vh;
  margin: 0;
}

.box {
  height: calc(50% + 20%);
  width: 100%;
  background-image: url(http://source.unsplash.com/random);
  background-repeat: no-repeat;
  background-position: right 50px;
}
```

### Strings e identificadores

As `strings` são textos envoltos de aspas, enquanto os identificadores são, por exemplo, `red`, `black` e `blue` para rotular cores.

No caso abaixo, a frase "Aqui vem alguma mensagem" aparece na cor branca sobre a imagem.

```CSS
.box {
  height: 300px;
  width: 400px;
  background-image: url(http://source.unsplash.com/random);
  background-repeat: no-repeat;
  background-position: bottom right;
}

.box::after {
  content: "Aqui vem alguma mensagem";
  color: white;
}
```

## Nem só de classes ou IDs

### Selectors and Combinators

#### Seletores

Os seletores conectam um elemento HTML com o CSS a fim de alterar esse elemento.

**Tipos de seletores**:

- Element selector

  - Envolve todos os elementos HTML

  ```html
  <h1>Título da página</h1>
  <p>Subtítulo</p>
  ```

  ```CSS
  h1 {
    color: yellow;
  }

  p {
    color: pink;
  }
  ```

- ID Selector

  - Um elemento que tenha um atributo `id`;
  - Cada `id` deverá ser único

  ```html
  <h1 id="titulo">Título da página</h1>
  <p id="subtitulo">Subtítulo</p>
  ```

  ```CSS
  #titulo {
    color: red;
  }

  #subtitulo {
    color: green;
  }
  ```

- Class Selector

  - Os elementos que contenham um atributo `class`;
  - Podemos ter uma ou mais classes

  ```html
  <h1 class="red">Título da página</h1>
  <p class="red">Conteúdo</p>
  ```

  ```CSS
  .red {
    color: red;
  }
  ```

- Attribute Selector

  - Um elemento que tenha um atributo específico.

  ```html
  <h1 title="algum título">Título da página</h1>
  ```

  ```CSS
  [title] {
    color: red;
  }
  ```

- Pseudo-class Selector

  - Elementos que possuem um estado específico.

  ```html
  <h1>Título da página</h1>
  ```

  ```CSS
  h1:hover {
    color: orange;
  }
  ```

  **Múltiplos elementos**

É possível selecionar múltipos elementos e aplicar alguma regra CSS para todos eles, separando-os por vírgulas.

```CSS
h1, a:hover, .red {
  color: red;
}
```

#### Combinators

Combinadores trabalham para buscar e combinar seletores com o propósito de aplicar uma estilização.

**Descedant combinator**

É identificado por um espaço entre os seletores. Busca um elemento dentro do outro.

```CSS
body article h2 {
  color: red;
}
/* procura dentro do body alguma tag article que tenha h2 e aplica a cor vermelha */
```

No caso acima, a cor vermelha será aplicada para todos os elementos `h2` que tiverem dentro de um `article` que, por sua vez, estiver dentro de `body`, mesmo que haja outro elemento ao meio, como no caso:

```HTML
<body>
  <div>
    <article>
      <p>
        <h2>Título</h2>
      </p>
    </article>
  </div>
</body>
```

Nesses casos, daria no mesmo pro CSS procurar `body h2` ou somente `h2` na página inteira.

#### Child combinator

Deixa a busca por combinação um pouco mais específica.

Identificado pelo sinal `>` entre dois seletores, ele seleciona **somente** o elemento que é **filho direto do pai**; os elementos depois do filho direto serão desconsiderados.

```CSS
body > ul > li
```

No caso abaixo, todos os `ul > li` que estiverem dentro de body terão a cor azul aplicada.

```HTML
<body>
<ul>
  <li>Item 1</li>

  <ul>
    <li>Item 1.1</li>
  </ul>
</ul>
</body>
```

```CSS
body ul li {
  color: blue;
}
```

Mas, ao alterar o CSS para uma busca mais específica, eu altero somente o `Item 1` e não `Item 1.1` com a cor azul, ou seja, o filho direto, somente o primeiro.

```CSS
body > ul > li {
  color: blue;
}
```

Agora, se eu envolvo tudo isso em uma `div`, mesmo que ela esteja dentro de `body`, o estilo não é aplicado porque a especifidade foi tanta que ele precisaria da informação da existência dessa `div` antes de `ul > li`.

Caso eu retire o `body` do estilo, aí sim funciona a aplicação para todos os `ul > li`.

Para eu aplicar o estilo em `Item 1.1` e não no `Item 1`, devo especificar dessa forma:

```HTML
<body>
<ul>
  <li>Item 1</li>

  <ul>
    <li>Item 1.1</li>
  </ul>
</ul>
</body>
```

```CSS
ul > ul > li {
  color: blue;
}
```

#### Adjacent Sibling Combinator

É identificado pelo sinal `+` entre dois seletores; seleciona **somente** o elemento do **lado direito** que é **irmão direto** na hierarquia. Ou seja, combinador irmão adjacente.

```HTML
<h1>Título</h1>
<p>Parágrafo</p>
<p>Outro paragráfo</p>
```

```CSS
h1 + p {
  color: orange;
}
```

No exemplo acima, juntamento ao `h1` temos um irmão e depois outro irmão. Porém, esse `+` vai pegar apenas o "primeiro irmão", o irmão direto, ou seja, apenas o primeiro parágrafo.

#### General Sibling Combinator

Identificado pelo sinal `~` entre dois seletores; seleciona todos os elementos irmãos.

```HTML
<h1>Título</h1>
<p>Parágrafo</p>
<p>Outro paragráfo</p>
```

```CSS
h1 ~ p {
  color: orange;
}
```

Já nesse caso, ambos os irmãos terão a cor laranja aplicada, já que todos os elementos irmãos que estiverem ao lado do `h1` serão selecionados.

#### Utilizando combinators

Agora, podemos utilizar os combinadores de diversas maneiras. Por exemplo, pegar todos os `li` diretos de `ul` que tenham a classe `.red`:

```HTML
<ul>
  <li>Item 1</li>
  <li class="red">Item 2</li>
</ul>
```

```CSS
ul > li[class="red"] {
  color: red;
}
```

**Dica**:<br>
Seletores muito específicos tendem a causar dificuldades no reuso das regras de estilização dos elementos. Muitas vezes, um simples uso de classes torna o trabalho muito mais eficiente.

Então, no caso acima, poderia simplesmente fazer assim, facilitando a reutilização do estilo:

```CSS
.red {
  color: red;
}
```

### Pseudo-classes

#### Pseudo-classes

É um **tipo de seletor** que irá selecionar um elemento que estiver em um estado específico.

Exemplificando, é o primeiro elemento dentro de uma caixa ou o elemento está com o ponteiro do mouse em cima dele.

As pseudo-classes começam com 2 pontos seguidos do nome da pseudo class e sempre serão utilizadas no seletor (algum seletor prévio): `:pseudo-class-name`

#### first-child

Para selecionar o primeiro filho de um grupo de elementos, utilizamos: `:first-child`

No exemplo abaixo, tenho 3 elementos dentro de uma lista.

```HTML
<ul>
  <li>Feijão</li>
  <li>Arroz</li>
  <li>Batata</li>
</ul>
```

Para que eu selecione o primeiro elemento para que apenas ele tenha o estilo aplicado, posso fazer deste modo:

```CSS
ul li:first-child {
  font-weight: bold;
  color: blue;
}
```

Importante: caso eu tenha, por exemplo, um `h3` dentro do `ul`, essa regra do `:first-child` para `li` não vai funcionar. O que acontece é que o CSS segue a regra de que, dentro da caixa `ul`, o primeiro filho é o `h3`, o segundo o primeiro `li` e assim por diante.

```HTML
<ul>
  <h3>Comidas</h3>
  <li>Feijão</li>
  <li>Arroz</li>
  <li>Batata</li>
</ul>
```

Então, não existe `li` como primeiro, no caso abaixo. Entretanto, como `h3` é o primeiro filho, essa regra pode ser aplicada a ele:

```CSS
ul h3:first-child {
  font-weight: bold;
  color: blue;
}
```

#### nth-of-type

#### nth-child

#### nth-child odd e even

#### hover e focus

#### disabled e required

#### Como conseguir ajuda

### Pseudo-elements
