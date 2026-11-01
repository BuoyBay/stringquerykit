---
title: "StringQueryKit API"
summary: "Predicate factories, boolean composition, transforms, mapping, and filtering."
category: "Reference"
order: 20
keywords: ["strings", "query", "filter", "map", "predicates", "transforms", "closures"]
symbols: ["StringPredicate", "StringTransform", "TextBegins", "TextEnds", "TextContains", "TextIsEmpty", "PredicateNot", "PredicateAll", "PredicateAny", "TrimText", "UpperText", "LowerText", "TransformChain", "MapStrings", "FilterStrings"]
related: ["index.md", "getting-started.md", "typed-api.md"]
---

# API reference

## Callback types

| Symbol | Contract |
| --- | --- |
| `StringPredicate(text As String) As Boolean` | Owned Closure Function deciding whether a string matches. |
| `StringTransform(text As String) As String` | Owned Closure Function producing a replacement string. |

These are nominal closure types, not interchangeable delegate or native callback pointers. Custom callbacks must have the expected StringPredicate or StringTransform type.

## Predicate factories

| Symbol | Contract |
| --- | --- |
| `TextBegins(prefix, caseSensitive = True)` | Match using String.StartsWith; capture prefix and case mode. |
| `TextEnds(suffix, caseSensitive = True)` | Match using String.EndsWith. |
| `TextContains(fragment, caseSensitive = True)` | Match using String.Contains. |
| `TextIsEmpty()` | True exactly when String.Len(text) is zero. |
| `PredicateNot(predicate)` | Negate one non-Nil predicate. |
| `PredicateAll(predicates)` | Evaluate in order and stop at the first False; empty array returns True. |
| `PredicateAny(predicates)` | Evaluate in order and stop at the first True; empty array returns False. |

All/Any validate every callback at construction and capture a cloned callback array. A Nil callback rejects even when an earlier predicate could otherwise short-circuit. Text matching and case conversion retain the semantics of Buoy's String operations; the package adds no separate locale or normalization policy.

## Transforms

| Symbol | Contract |
| --- | --- |
| `TrimText()` | Return a transform using String.Trim. |
| `UpperText()` | Return a transform using String.UCase. |
| `LowerText()` | Return a transform using String.LCase. |
| `TransformChain(transforms)` | Apply non-Nil transforms left to right, capturing a cloned callback array. An empty chain returns its input unchanged. |

## Eager array operations

`MapStrings(items, transform, maxItems = 100000)` returns one transformed value for every snapshotted input item, in order. `FilterStrings(items, predicate, maxItems = 100000)` returns the original snapshotted values whose predicate is True, in order. Filtering does not substitute any normalized value unless normalization was performed in an earlier mapping step.

Both functions validate the callback and item limit before invoking callbacks. Negative limits, a count above maxItems, or a Nil callback throw InvalidArgumentException. Each call returns a new array and leaves the supplied array alone. They make no guarantee of rollback for a user callback's external side effects and do not catch callback exceptions.

[Getting started](getting-started.md) · [Package overview](index.md)


[Full typed API: properties, parameters, defaults, and returns](typed-api.md)
