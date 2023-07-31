# `cdx:maven` Namespace Taxonomy

| Namespace | Description |
| --------- | ----------- |
| `cdx:maven:package` | Namespace for package specific properties. |

## `cdx:maven:package` Namespace Taxonomy

| Property | Description |
| -------- | ----------- |
| `cdx:maven:package:goal` | The goal used to generate the SBOM: `makeBom`, `makeAggregateBom` or `makePackageBom`. |
| `cdx:maven:package:scopes` | The activated Maven dependency scopes: `compile`, `provided`, `runtime`, `system` or `test`, comma-separated if many. |
| `cdx:maven:package:reproducible` | Whether the SBOM has been generated in Reproducible Builds mode: in this mode, metadata timestamp and BOM serial number are dropped. _Boolean value_. If the property is missing, then assume the value to be `false`. |
| `cdx:maven:package:optional-unused` | Use bytecode analysis instead of Maven dependency declaration of optional to define SBOM OPTIONAL or REQUIRED scope. _Boolean value_. If the property is missing, then assume the value to be `false`. May appear once. |
