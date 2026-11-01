# Provenance

The 2016-02-20 declaresub homepage links Charles Yeomans' 2008 article
“A Bit of Functional Programming By Example”. The article demonstrates mapping
Trim over an array and filtering empty fields from `gzip -l` output. It ends by
asking how to combine or negate conditions. The current GitHub
[stringarraycombinatorlibrary](https://github.com/declaresub/stringarraycombinatorlibrary/tree/c9298583cfe5893bad9167edf5eea30ffc7f5582/files)
implements related predicate/transform factories in REALbasic XML exports.

StringQueryKit is an independent implementation using the installed Buoy closure
syntax and standard-library methods. No article code, GitHub code, images or
downloaded binaries are redistributed. No license was established for copying
the legacy implementations. Article URLs and fetched-content fingerprints are
recorded in `examples/declaresub/archive/inventory.json`.

This implements the reusable composition idea, not API compatibility. In
particular it uses Buoy `Closure` values with captured patterns rather than
REALbasic `Delegate.Invoke`, defaults to exact matching, snapshots inputs and
callback arrays, and provides explicit item-count limits. Regex, POSIX date
format conversion and original array-slice extensions are not included.
