# `cdx:pipenv` Namespace Taxonomy

This is the namespace for official CycloneDX properties related to the [Python Pipenv ecosystem](https://pipenv.pypa.io/).

The official rules and processes apply - see [parent document](../cdx.md).

----

| Property | Description |
|----------|-------------|
| `cdx:pipenv:category` | Name of a [category](https://pipenv.pypa.io/en/latest/pipfile.html#package-category-groups) the component belongs to. Well-known categories are: "default", "develop". _Non-empty string value_. May appear multiple times with different values. |

| Namespace | Description |
|-----------|-------------|
| `cdx:pipenv:package` | Namespace for package specific properties. |
