# `cdx:maven` Namespace Taxonomy

This is the namespace for official CycloneDX properties related to the [Maven ecosystem](https://maven.apache.org/).

The official rules and processes apply - see [parent document](../cdx.md).

----

| Namespace | Description |
|-----------|-------------|
| `cdx:maven:package` | Namespace for package specific properties. |

_Boolean value_ are `true` or `false`; case sensitive.

## `cdx:maven:package` Namespace Taxonomy

| Property | Description |
|----------|-------------|
| `cdx:maven:package:test` | Whether the package is used only within `test` scope for Maven and `test.*` configurations for Gradle. _Boolean value_. If the property is missing, then assume the value to be `false`. May appear once. |
