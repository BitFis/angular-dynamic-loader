# Dynamic Loader

This tool enables loading the angular application dynamically
after loading the index html file on command.

Instead of loading the js file, the function `appendElement(type, attrs)`
is called. Additionally the `import .. from ..` call is replaced with `import(..${importquery})`
enabling appending query arguments to the dynamically loaded angular chunks.

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
