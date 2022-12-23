# `cdx:composer` Namespace Taxonomy

| Namespace | Description |
| --------- | ----------- |
| `cdx:composer:package` | Namespace for package specific properties. |

_Boolean value_ are `true` or `false`. Case sensitive.

## `cdx:composer:package` Namespace Taxonomy

| Property | Description |
| -------- | ----------- |
| `cdx:composer:package:type` | The [package type](https://getcomposer.org/doc/04-schema.md#type) of the component. If the property is missing, then assume the value to be `library`. May appear once. |
| `cdx:composer:package:isDevRequirement` | Whether the package was flagged as "dev requirement". _Boolean value_. If the property is missing, then assume the value to be `false`. May appear once. |
