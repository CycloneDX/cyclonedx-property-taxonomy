# `cdx:maven` Namespace Taxonomy

| Namespace | Description |
|-----------|-------------|
| `cdx:maven:package` | Namespace for package specific properties. |

_Boolean value_ are `true` or `false`. Case sensitive.

## `cdx:maven:package` Namespace Taxonomy

| Property | Description |
|----------|-------------|
| `cdx:maven:package:test` | Whether the package is used only within `test` scope for Maven and `test.*` configurations for Gradle. _Boolean value_. If the property is missing, then assume the value to be `false`. May appear once. |
