# Cross-platform Targeting

grib

**✓ CONSIDER** including a `netstandard20` target. .NET Standard 2.0 is the recommended way to support multiple platforms with one target.

**X AVOID** including a `netstandard1x` target. A .NET Standard 1.x target has a large package dependency graph. Prefer .NET Standard 2.0 and above.

**X DO NOT** include a Portable Class Library (PCL) target, e.g. `portable-net45+win8+wpa81+wp8`.

**X DO NOT** include obsolete targets, e.g. `SL4`, `WP`.

## Common cross-platform issues

1. Reflection & AOT
2. UI (XAML & WinForms)