<div align="center">
  <img width="150" height="150" alt="PostHTML" src="https://posthtml.github.io/posthtml/logo.svg">
  <h1>PostHTML Render</h1>
  <p>Renders a PostHTML Tree to HTML/XML</p>

  [![Version][npm-version-shield]][npm]
  [![Build][github-ci-shield]][github-ci]
  [![License][license-shield]][license]
</div>

## Install

```bash
npm i -D posthtml-render
```

## Usage

### Node.js

```js
import { render } from 'posthtml-render'

const tree = []

const node = {}

node.tag = 'ul'
node.attrs = { class: 'list' }
node.content = [
 'one',
 'two',
 'three'
].map((content) => ({ tag: 'li', content }))

tree.push(node)

const html = render(tree, options)
```

```html
<ul class="list">
  <li>one</li>
  <li>two</li>
  <li>three</li>
</ul>
```

## Options

|Name|Type|Default|Description|
|:--:|:--:|:-----:|:----------|
|**[`singleTags`](#singletags)**|`Array<String\|RegExp>`|`[]`|Specify custom single tags (self closing)|
|**[`closingSingleTag`](#closingSingleTag)**|`String`|[`>`](#default)|Specify the single tag closing format|
|**[`quoteAllAttributes`](#quoteAllAttributes)**|`Boolean`|[`true`](#default)|Put double quotes around all tags, even when not necessary.|
|**[`replaceQuote`](#replaceQuote)**|`Boolean`|[`true`](#default)|Replaces quotes in attribute values with `&quote;`.|
|**[`quoteStyle`](#quoteStyle)**|`Number`|[`2`](#default)|Specify the style of quote around the attribute values|

### `singleTags`

Type: `{Array<String|RegExp>}`\
Default: `[]`

Specify custom single tags (self closing).

#### String

```js
import { render } from 'posthtml-render'

const tree = [ { tag: 'name' } ]
const options = { singleTags: [ 'name' ] }

const html = render(tree, options)
```

Result:

```html
<name>
```

#### RegExp

```js
import { render } from 'posthtml-render'

const tree = [ { tag: '%=title%' } ]
const options = { singleTags: [ /^%.*%$/ ] }

const html = render(tree, options)
```

Result:

```html
<%=title%>
```

### `closingSingleTag`

Type: `String`\
Default: `>`

Specify the single tag closing format.

```js
import { render } from 'posthtml-render'

const tree = [ { tag: 'img' } ]
```

##### `tag` format

```js
const html = render(tree, { closingSingleTag: 'tag' })
```

```html
<custom></custom>
```

##### `slash` format

```js
const html = render(tree, { closingSingleTag: 'slash' })
```

```html
<custom />
```

##### `default`  (Default)

```js
const html = render(tree)
```

```html
<img>
```

##### `closeAs`

Type: `String`\
Default: `default`

```js
const tree = [ {
  tag: 'custom',
  closeAs: 'default' // Available types: `tag` | `slash` | `default`
} ]
const html = render(tree, { closingSingleTag: 'closeAs' })
```

```html
<custom>
```

### `quoteAllAttributes`

Type: `Boolean`\
Default: `true`

Specify if all attributes should be quoted.

##### `true`

```html
<i src="index.js"></i>
```

##### `false`

```html
<i src=index.js></i>
```

### `replaceQuote`

Type: `Boolean`\
Default: `true`

Replaces quotes in attribute values with `&quote;`.

##### `true`

```html
<img src="<?php echo $foo[&quote;bar&quote;] ?>">
```

##### `false`

```html
<img src="<?php echo $foo["bar"] ?>">
```

### `quoteStyle`

Type: `Number`\
Default: `2`

##### `quoteStyle: 2`

Attribute values are wrapped in double quotes:

```html
<img src="https://example.com/example.png" onload="testFunc("test")">
```

##### `quoteStyle: 1`

Attribute values are wrapped in single quote:

```html
<img src='https://example.com/example.png' onload='testFunc("test")'>
```

##### `quoteStyle: 0`

Quote style is based on attribute values (an alternative for `replaceQuote` option):

```html
<img src="https://example.com/example.png" onload='testFunc("test")'>
```

[npm]: https://www.npmjs.com/package/posthtml-render
[npm-version-shield]: https://img.shields.io/npm/v/posthtml-render.svg
[github-ci]: https://github.com/posthtml/posthtml-render/actions
[github-ci-shield]: https://github.com/posthtml/posthtml-render/actions/workflows/nodejs.yml/badge.svg
[license]: ./LICENSE
[license-shield]: https://img.shields.io/npm/l/posthtml-render.svg
[coverage]: https://coveralls.io/github/posthtml/posthtml-render
[coverage-shield]: https://coveralls.io/repos/github/posthtml/posthtml-render/badge.svg
