# Dynamic Loader

This tool enables loading the angular application dynamically
after loading the index html file on command.

Instead of loading the js file, the function `appendElement(type, attrs)`
is called. Additionally the `import .. from ..` call is replaced with `import(..${importquery})`
enabling appending query arguments to the dynamically loaded angular chunks.

## Usage

Install the tool via `cargo install --git https://github.com/BitFis/angular-dynamic-loader.git`.

Following some examples on how to use it:

### Index HTML

Running ```cargo run -- index index.html``` for the following *index.html*:

```html
<body>
  <app-root></app-root>
  <script type="module" src="polyfills-B5TEDK75.js"></script>
  <script src="main-CDZAXZJF.js" type="module"></script>
</body>
```

converts it to following output:

```html
<body>
<app-root></app-root>
   <script>appendElement("script", {"type":"module","src":`polyfills-B5TEDK75.js${importquery}`,});</script>
   <script>appendElement("script", {"src":`main-CDZAXZJF.js${importquery}`,"type":"module",});</script>
</body>
```

by providing the `-S load.js` argument, an external script can be injected.
This can be useful to provide the `appendElement` function and control the
process on how those scripts are loaded.

### JS

Running ```cargo run -- js myscript.js``` for the following *myscript.js*:

```js
import {
    __async
} from \"./chunk-H3KQGMCP.js\";
var well = true;
```

Will convert the `from "..."` portion to ```await import(`...`)``` and append the `${importquery}` argument. This enables customizing the url query parameters
dynamically. This is otherwise not possible with angular.

```js
const {
    __async: __async,
} = await import(`./chunk-H3KQGMCP.js${importquery}`);
var well = true;
```

## Development

### Run cli

```
cargo run -- --help
```

### Rust Build

```
cargo build
```

### Run tests

```
cargo test
```

## Deploy

### npm package

tbd.
