# StringQueryKit 0.1.0

Pure Buoy string-array queries built from owned closures. Inspired by the
[archived functional-programming article](https://web.archive.org/web/20160220114803/https://www.declaresub.com/articles/2008/01/29/a-bit-of-functional-programming-by-example)
and its questions about combining and negating predicates. This package composes
existing String operations; StringUtils remains the destination for additional
individual text algorithms.

`Import stringquerykit` exposes nominal closure types `StringPredicate(text) As
Boolean` and `StringTransform(text) As String`.

| API | Behavior |
| --- | --- |
| `TextBegins`, `TextEnds`, `TextContains` | Capture a pattern and optional `caseSensitive = True` |
| `TextIsEmpty()` | Match exactly zero codepoints |
| `PredicateNot(predicate)` | Negate a non-Nil predicate |
| `PredicateAll(predicates)`, `PredicateAny(predicates)` | Ordered short-circuit composition; empty lists return True/False respectively |
| `TrimText()`, `UpperText()`, `LowerText()` | Wrap the matching built-in text operation |
| `TransformChain(transforms)` | Apply left to right; empty list is identity |
| `MapStrings(items, transform, maxItems = 100000)` | New ordered transformed array |
| `FilterStrings(items, predicate, maxItems = 100000)` | New ordered array retaining matches |

Nil callbacks are rejected before use. Composition factories clone their callback
lists. Map/Filter clone their input list before invoking callbacks, so a callback
that mutates the original array cannot alter the current traversal. Closures own
captured patterns and other closures. Exceptions from callbacks propagate.

The item limit must be nonnegative and is checked before cloning or callbacks.
There is no bound on callback runtime, recursion or individual output-string
length: callers control those operations. Callbacks may have side effects; the
package supplies no concurrency or rollback contract.

Case-sensitive matching is the default. Explicit case-insensitive matching follows
Buoy's current ASCII-only folding, not locale collation or Unicode normalization.
Trim follows built-in ASCII whitespace semantics; case transforms follow the
runtime's Unicode mappings. No grapheme segmentation, regex factory, sorting or
generic Array Map/Filter API is supplied.

Maintainers run the private validation suite before release. See the repository README for public build instructions.
