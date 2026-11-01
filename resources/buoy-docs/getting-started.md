---
title: "StringQueryKit getting started"
summary: "Normalize strings and select matches with reusable composed callbacks."
category: "Guides"
order: 10
keywords: ["strings", "query", "filter", "map", "predicates", "transforms", "closures"]
related: ["index.md", "api.md", "typed-api.md"]
---

# Getting started

Place `stringquerykit-0.1.0.buipkg` in the consumer project's `packages/` directory, then import `stringquerykit`. The package requires a Buoy compiler supporting owned closures; the package manifest specifies Buoy 0.72.0.

## Normalize before filtering

The example trims and lowercases a list of path labels, then selects Markdown labels beneath `docs/`. These are string operations only: no files are opened or path components resolved.

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

The result contains `docs/guide.md` followed by `docs/api.md`. The original array remains unchanged. Transform order matters: `TransformChain` runs from left to right, so the filter receives the normalized text.

## Choose matching behavior

Prefix, suffix, and fragment predicates default to case-sensitive comparisons. Pass False as the second argument to use the corresponding standard-library case-insensitive operation. `TextIsEmpty` tests zero string length; it does not trim whitespace. Normalize first if whitespace-only strings should count as empty.

## Failures and callbacks

Nil callbacks and negative or exceeded item limits throw `InvalidArgumentException`. A limit of zero permits an empty input only. Callback exceptions propagate to the caller; no partial array is returned. Callback side effects that already happened are not rolled back. Keep stateful callbacks on one thread or synchronize their state externally.

[Package overview](index.md) · [API reference](api.md)
