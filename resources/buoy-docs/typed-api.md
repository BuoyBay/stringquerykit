---
title: "stringquerykit typed API"
summary: "Source-derived public signatures, properties, parameters, defaults, and return values."
category: "Reference"
order: 21
types: ["StringPredicate", "StringTransform"]
dependencies: []
symbols: ["StringPredicate", "StringTransform"]
related: ["api.md", "getting-started.md", "index.md"]
---

# stringquerykit typed API

Generated from the package source declarations. Platform guards are shown where present; inherited members are documented on the base type. See the [API contracts](api.md) for behavior and limitations.

## StringQueryKit functions

### StringPredicate

`Public Closure Function StringPredicate(text As String) As Boolean`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `text` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Boolean` |

### StringTransform

`Public Closure Function StringTransform(text As String) As String`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `text` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `String` |

### TextBegins

`Public Function TextBegins(prefix As String, caseSensitive As Boolean = True) As StringPredicate`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `prefix` | `String` | `ByVal` | Required |
| `caseSensitive` | `Boolean` | `ByVal` | `True` |

#### Returns

| Type |
| --- |
| `StringPredicate` |

### TextEnds

`Public Function TextEnds(suffix As String, caseSensitive As Boolean = True) As StringPredicate`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `suffix` | `String` | `ByVal` | Required |
| `caseSensitive` | `Boolean` | `ByVal` | `True` |

#### Returns

| Type |
| --- |
| `StringPredicate` |

### TextContains

`Public Function TextContains(fragment As String, caseSensitive As Boolean = True) As StringPredicate`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `fragment` | `String` | `ByVal` | Required |
| `caseSensitive` | `Boolean` | `ByVal` | `True` |

#### Returns

| Type |
| --- |
| `StringPredicate` |

### TextIsEmpty

`Public Function TextIsEmpty() As StringPredicate`

No parameters.

#### Returns

| Type |
| --- |
| `StringPredicate` |

### PredicateNot

`Public Function PredicateNot(predicate As StringPredicate) As StringPredicate`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `predicate` | `StringPredicate` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `StringPredicate` |

### PredicateAll

`Public Function PredicateAll(predicates As Array Of StringPredicate) As StringPredicate`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `predicates` | `Array Of StringPredicate` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `StringPredicate` |

### PredicateAny

`Public Function PredicateAny(predicates As Array Of StringPredicate) As StringPredicate`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `predicates` | `Array Of StringPredicate` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `StringPredicate` |

### TrimText

`Public Function TrimText() As StringTransform`

No parameters.

#### Returns

| Type |
| --- |
| `StringTransform` |

### UpperText

`Public Function UpperText() As StringTransform`

No parameters.

#### Returns

| Type |
| --- |
| `StringTransform` |

### LowerText

`Public Function LowerText() As StringTransform`

No parameters.

#### Returns

| Type |
| --- |
| `StringTransform` |

### TransformChain

`Public Function TransformChain(transforms As Array Of StringTransform) As StringTransform`

Apply transforms left to right. The captured list is an owned snapshot.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `transforms` | `Array Of StringTransform` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `StringTransform` |

### MapStrings

`Public Function MapStrings(items As Array Of String, transform As StringTransform, maxItems As Integer = 100000) As Array Of String`

Snapshot the input before invoking callbacks; produce a fresh ordered array.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `items` | `Array Of String` | `ByVal` | Required |
| `transform` | `StringTransform` | `ByVal` | Required |
| `maxItems` | `Integer` | `ByVal` | `100000` |

#### Returns

| Type |
| --- |
| `Array Of String` |

### FilterStrings

`Public Function FilterStrings(items As Array Of String, predicate As StringPredicate, maxItems As Integer = 100000) As Array Of String`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `items` | `Array Of String` | `ByVal` | Required |
| `predicate` | `StringPredicate` | `ByVal` | Required |
| `maxItems` | `Integer` | `ByVal` | `100000` |

#### Returns

| Type |
| --- |
| `Array Of String` |
