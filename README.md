# Compose string predicates and transformations

Pure Buoy string-array queries built from owned closures. Inspired by the
[archived functional-programming article](https://web.archive.org/web/20160220114803/https://www.declaresub.com/articles/2008/01/29/a-bit-of-functional-programming-by-example)
and its questions about combining and negating predicates. This package composes
existing String operations; StringUtils remains the destination for additional
individual text algorithms.

`Import stringquerykit` exposes nominal closure types `StringPredicate(text) As
Boolean` and `StringTransform(text) As String`.

## Install

From a Buoy consumer project with BPM installed:

```sh
bpm add stringquerykit --git https://github.com/BuoyBay/stringquerykit.git --rev refs/heads/main
```

BPM records the resolved commit in its lockfile. Keep that lockfile with the
consumer project for reproducible installs.

## Example

```buoy
Import stringquerykit

Sub Main()
    Dim transforms As Array Of StringTransform = [TrimText(), LowerText()]
    Dim normalize As StringTransform = TransformChain(transforms)
    Dim original As Array Of String = [" docs/Guide.MD ", "src/main.bui", "docs/api.md", "   "]
    Dim normalized As Array Of String = MapStrings(original, normalize)

    Dim predicates As Array Of StringPredicate = [TextBegins("docs/"), TextEnds(".md")]
    Dim selectDocument As StringPredicate = PredicateAll(predicates)
    For Each label As String In FilterStrings(normalized, selectDocument)
        Print label
    Next
End Sub
```

## Build from source

With the native `build-packages` driver from [devtools](https://github.com/BuoyBay/devtools)
on your `PATH`, run from this checkout:

```sh
build-packages --root "$PWD" --compile-consumer stringquerykit
```

The driver checks source targets and compiles an import consumer. See the
[API guide](docs/API.md) for behavior, limits and any host prerequisites.

## Local Buoy setup

On your own machine, install Buoy and run:

```sh
buoy ai init --both
```

The generated agent files and editor settings stay local and are ignored by Git.

## Contributing

[Contributing](CONTRIBUTING.md) · [License](LICENSE)
