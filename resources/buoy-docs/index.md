---
title: "StringQueryKit"
summary: "Compose owned string predicates and transforms for eager array queries."
category: "Overview"
order: 0
keywords: ["strings", "query", "filter", "map", "predicates", "transforms", "closures"]
related: ["getting-started.md", "api.md", "typed-api.md"]
---

# StringQueryKit

StringQueryKit provides composable string filters and transforms using Buoy's owned closure types. Build a predicate from prefixes, suffixes, fragments, and boolean composition; build a transform from trimming and case conversion; then apply it to an array of strings.

This is a pure Buoy package with no native library or package dependency. Queries are eager and preserve input order. There is no filesystem access, regular-expression engine, query parser, or background execution.

## Owned composition

The package defines nominal `StringPredicate` and `StringTransform` closure types. A composed operation retains its child closures. `PredicateAll`, `PredicateAny`, and `TransformChain` copy the supplied callback array before capturing it, so later changes to that array do not replace the composed operations. Child closures can still share their own captured state; this is not a deep copy of callback state.

`MapStrings` and `FilterStrings` snapshot the input array before invoking callbacks and return fresh ordered arrays. Their default item limit is 100,000. This guards array count, not string byte lengths or the cost of user callbacks; hosts should choose additional budgets when processing untrusted data.

## Read next

- [Getting started](getting-started.md)
- [API reference](api.md)
