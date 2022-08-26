# `cdx:npm` Namespace Taxonomy

| Namespace | Description |
| --------- | ----------- |
| `cdx:npm:package` | Namespace for package specific properties. |
| `cdx:npm:package:constraint` | Namespace for package constraints. |

_Boolean value_ are `true` or `false`. Case sensitive.

## `cdx:npm:package` Namespace Taxonomy

| Property | Description |
| -------- | ----------- |
| `cdx:npm:package:bundled` | Whether the package was bundled(shipped) with its parent component. _Boolean value_. If the property is missing, then assume the value to be `false`. May appear once. |
| `cdx:npm:package:extraneous` | Whether the package was installed extraneous. _Boolean value_. If the property is missing, then assume the value to be `false`. May appear once. |
| `cdx:npm:package:private` | Whether the package was flagged as "private". _Boolean value_. If the property is missing, then assume the value to be `false`. May appear once. |
| `cdx:npm:package:development` | Whether the package was flagged as "devDependency". _Boolean value_. If the property is missing, then assume the value to be `false`. May appear once. |

## `cdx:npm:package:constraint` Namespace Taxonomy

| Property | Description |
| -------- | ----------- |
| `cdx:npm:package:constraint:engine:<NAME>` | Supported/required [engine marker](https://docs.npmjs.com/cli/v8/configuring-npm/package-json#engines). May appear once. |
| `cdx:npm:package:constraint:engine-strict` | Whether the engine is a requirement, or an advice. _Boolean value_.  If the property is missing, then assume the value to be `false`. May appear once. |
| `cdx:npm:package:constraint:os` | Supported/required [operating system markers](https://docs.npmjs.com/cli/v8/configuring-npm/package-json#os). May appear multiple times with different values. |
