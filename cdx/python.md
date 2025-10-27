# `cdx:python` Namespace Taxonomy

_Boolean value_ are `true` or `false`. Case sensitive.

| Namespace | Description |
|-----------|-------------|
| `cdx:python:package` | Namespace for package specific properties. |

## `cdx:python:package` Namespace Taxonomy

| Property | Description |
|----------|-------------|
| `cdx:python:package:marker` | Environment markers, following the specification [here](https://packaging.python.org/en/latest/specifications/dependency-specifiers/#environment-markers), that specify conditions for when a package should be used. This represents the resolved marker expression that determines when this package is included in the environment, derived from all dependency specifications that reference this package. _Non-empty string value_. May appear once. |
| `cdx:python:package:required-extra` | The package's extra that was required. Value MAY be [normalized](https://packaging.python.org/en/latest/specifications/name-normalization/). _Non-empty string value_. May appear multiple times with different values. |

| Namespace | Description |
|-----------|-------------|
| `cdx:python:package:source` | Namespace for package-source specific properties. |

## `cdx:python:package:source` Namespace Taxonomy

In accordance with [PEP610](https://peps.python.org/pep-0610/)
and [packaging's `direct-url`](https://packaging.python.org/en/latest/specifications/direct-url/)
and [packaging's `direct-url` data structure](https://packaging.python.org/en/latest/specifications/direct-url-data-structure/)
.

| Property | Description |
|----------|-------------|
| `cdx:python:package:source:subdirectory` | Directory path, relative to the root of the VCS repository, source archive or local directory, to specify where `pyproject.toml` or `setup.py` is located. _Non-empty string value_. May appear once. |

| Namespace | Description |
|-----------|-------------|
| `cdx:python:package:source:archive` | Namespace for package-source archive-specific properties. |
| `cdx:python:package:source:vcs` | Namespace for package-source vcs-specific properties. |
| `cdx:python:package:source:local` | Namespace for package-source local-specific properties. |

## `cdx:python:package:source:archive` Namespace Taxonomy

In accordance with [packaging's `direct-url` data structure for Archive](https://packaging.python.org/en/latest/specifications/direct-url-data-structure/#vcs-urls).

| Property | Description |
|----------|-------------|
| | |

There are no properties regiestered so far.  
The `hashes` of an archive should be added to the [`ExternalReference`][CDX-useCases-externalReferences] that represents the package source.

## `cdx:python:package:source:vcs` Namespace Taxonomy

In accordance with [packaging's `direct-url` data structure for VCS](https://packaging.python.org/en/latest/specifications/direct-url-data-structure/#vcs-urls)

| Property | Description |
|----------|-------------|
| `cdx:python:package:source:vcs:requested_revision` | The repository reference of this package, e.g. "master", "1.0.0" or a commit hash for git. Values may be applied to [`externalReferences`][CDX-useCases-externalReferences] of type `vcs`. _Non-empty string value_. May appear once. |
| `cdx:python:package:source:vcs:commit_id` | The resolved repository reference of this package, e.g. a commit hash for git. Values may be applied to [`externalReferences`][CDX-useCases-externalReferences] of type `vcs`. _Non-empty string value_. May appear once. |

## `cdx:python:package:source:local` Namespace Taxonomy

In accordance with [packaging's `direct-url` data structure for Local](https://packaging.python.org/en/latest/specifications/direct-url-data-structure/#local-directories)

| Property | Description |
|----------|-------------|
| `cdx:python:package:source:local:editable` | Wether this local package was installed in editable/developer mode. _Boolean value_. If the property is missing, then assume the value to be `false`. May appear once. |

[CDX-useCases-externalReferences]: https://cyclonedx.org/use-cases/#external-references
