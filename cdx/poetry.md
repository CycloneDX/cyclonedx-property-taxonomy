# `cdx:poetry` Namespace Taxonomy

| Property | Description |
| -------- | ----------- |
| `cdx:poetry:group` | Name of a [dependency group](https://python-poetry.org/docs/managing-dependencies/#dependency-groups) the component belongs to. Well-known groups are: "main", "dev". May appear multiple times with different values. |

| Namespace | Description |
| --------- | ----------- |
| `cdx:poetry:package` | Namespace for package specific properties. |


## `cdx:poetry:package` Namespace Taxonomy

| Property | Description |
| -------- | ----------- |
| `cdx:poetry:package:reference` | The repository reference of this package, e.g. master, 1.0.0 or a commit hash for git. Values may be applied to [`externalReferences`][CDX-useCases-externalReferences] of type `vcs`. _Non-empty string value_. May appear once. |
| `cdx:poetry:package:resolved_reference` | The resolved repository reference of this package, e.g. a commit hash for git. Values may be applied to [`externalReferences`][CDX-useCases-externalReferences] of type `vcs`. _Non-empty string value_. May appear once. |
