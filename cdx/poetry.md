# `cdx:poetry` Namespace Taxonomy

| Property | Description |
|----------|-------------|
| `cdx:poetry:group` | Name of a [dependency group](https://python-poetry.org/docs/managing-dependencies/#dependency-groups) the component belongs to. Well-known groups are: "main", "dev". _Non-empty string value_. May appear multiple times with different values. |

| Namespace | Description |
|-----------|-------------|
| `cdx:poetry:package` | Namespace for package specific properties. |

## `cdx:poetry:package` Namespace Taxonomy

| Namespace | Description |
|-----------|-------------|
| `cdx:poetry:package:source` | Namespace for package-source specific properties. |

## `cdx:poetry:package:source` Namespace Taxonomy

| Property | Description |
|----------|-------------|
| `cdx:poetry:package:source:reference` | **Deprecated** in favor of the more general [`cdx:python:package:source:vcs:requested_revision`](./python.md). <br/> The repository reference of this package, e.g. "master", "1.0.0" or a commit hash for git. Values may be applied to [`externalReferences`][CDX-useCases-externalReferences] of type `vcs`. _Non-empty string value_. May appear once. |
| `cdx:poetry:package:source:resolved_reference` | **Deprecated** in favor of the more general [`cdx:python:package:source:vcs:commit_id`](./python.md). <br/> The resolved repository reference of this package, e.g. a commit hash for git. Values may be applied to [`externalReferences`][CDX-useCases-externalReferences] of type `vcs`. _Non-empty string value_. May appear once. |

| Namespace | Description |
|-----------|-------------|
| `cdx:poetry:package:source:vcs` | **DEPRECATED** namespace for package-source's VCS specific properties. |

## `cdx:poetry:package:source:vcs` Namespace Taxonomy

This namespace is **deprecated** in favor of the more general [`cdx:python:package:source:vcs`](./python.md), or consider the properties mentioned above.

| Property | Description |
|----------|-------------|
| `cdx:poetry:package:source:vcs:requested_revision` | **Deprecated** in favor of the more general [`cdx:python:package:source:vcs:requested_revision`](./python.md). <br/> The repository reference of this package, e.g. "master", "1.0.0" or a commit hash for git. Values may be applied to [`externalReferences`][CDX-useCases-externalReferences] of type `vcs`. _Non-empty string value_. May appear once. |
| `cdx:poetry:package:source:vcs:commit_id` | **Deprecated** in favor of the more general [`cdx:python:package:source:vcs:commit_id`](./python.md). <br/> The resolved repository reference of this package, e.g. a commit hash for git. Values may be applied to [`externalReferences`][CDX-useCases-externalReferences] of type `vcs`. _Non-empty string value_. May appear once. |

[CDX-useCases-externalReferences]: https://cyclonedx.org/use-cases/#external-references
