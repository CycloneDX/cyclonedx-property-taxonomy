# `cdx:esbuild` Namespace Taxonomy

This is the namespace for official CycloneDX properties related to the [esbuild ecosystem](https://esbuild.github.io/).

The official rules and processes apply - see [parent document](../cdx.md).

----


| Namespace | Description |
|-----------|-------------|
| `cdx:esbuild:input` | Namespace for input specific properties. |

_Boolean value_ are `true` or `false`; case sensitive.

## `cdx:esbuild:input` Namespace Taxonomy

| Property | Description |
|----------|-------------|
| `cdx:esbuild:input:isVirtual` | Whether the input is virtual. _Boolean value_.<br/> If the property is missing, then assume the value to be `false`.<br/> May appear once. |
