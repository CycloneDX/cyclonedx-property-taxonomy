# `cdx:npm` Namespace Taxonomy

This is the namespace for official CycloneDX properties related to the [Node NPM ecosystem](https://docs.npmjs.com/packages-and-modules).

The official rules and processes apply - see [parent document](../cdx.md).

----

| Namespace | Description |
|-----------|-------------|
| `cdx:npm:package` | Namespace for package specific properties. |
| `cdx:npm:package:constraint` | Namespace for package constraints. |

_Boolean value_ are `true` or `false`; case sensitive.

## `cdx:npm:package` Namespace Taxonomy

| Property | Description |
|----------|-------------|
| `cdx:npm:package:bundled` | Whether the package was bundled(shipped) with its parent component. _Boolean value_. If the property is missing, then assume the value to be `false`. May appear once. |
| `cdx:npm:package:extraneous` | Whether the package was installed extraneous. _Boolean value_. If the property is missing, then assume the value to be `false`. May appear once. |
| `cdx:npm:package:private` | Whether the package was flagged as "private". _Boolean value_. If the property is missing, then assume the value to be `false`. May appear once. |
| `cdx:npm:package:development` | Whether the package was flagged as "devDependency". _Boolean value_. If the property is missing, then assume the value to be `false`. May appear once. |
| `cdx:npm:package:path` | A path the package is installed to. Posix-like path representation relative to the root directory of the project under analysis. To represent the root dir, an empty string is used. May appear multiple times with different values. Example value: `node_modules/cliui/node_modules/strip-ansi` |

## `cdx:npm:package:constraint` Namespace Taxonomy

| Property | Description |
|----------|-------------|
| `cdx:npm:package:constraint:engine:<NAME>` | Supported/required [engine marker](https://docs.npmjs.com/cli/v8/configuring-npm/package-json#engines). May appear once. Example: `cdx:npm:package:constraint:engine:node = >=12.2`|
| `cdx:npm:package:constraint:engine-strict` | Whether the engine is a requirement, or an advice. _Boolean value_. If the property is missing, then assume the value to be `false`. May appear once. |
| `cdx:npm:package:constraint:os` | Supported/required [operating system markers](https://docs.npmjs.com/cli/v8/configuring-npm/package-json#os). May appear multiple times with different values. |
