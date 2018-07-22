# Cross-platform Targeting

grib

**✓ CONSIDER** including a `netstandard20` target.

**X AVOID** including a `netstandard1x` target.

**X DO NOT** include a Portable Class Library (PCL) target, e.g. `portable-net45+win8+wpa81+wp8`.

**X DO NOT** include obsolete targets, e.g. `SL4`, `WP`.

## Common cross-platform issues

1. Reflection & AOT
2. UI (XAML & WinForms)