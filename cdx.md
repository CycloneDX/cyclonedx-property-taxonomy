# `cdx` Namespace Taxonomy

_Boolean value_ are `true` or `false`. Case sensitive.

| Property | Description |
| -------- | ----------- |
| `cdx:reproducible` | Whether the CycloneDX document has been generated in a reproducible manner: if so, then time- or random-based values MUST be omitted, and elements order SHOULD be reproducible. _Boolean value_. May appear once. |

| Namespace | Description | Administered By | Taxonomy |
| --------- | ----------- | --------------- | -------- |
| `cdx:composer` | Namespace for properties specific to the PHP Composer ecosystem. | [CycloneDX PHP Maintainers] | [cdx:composer taxonomy](cdx/composer.md) |
| `cdx:device` | Namespace for properties specific to hardware devices. | [CycloneDX Core Working Group] | [cdx:device taxonomy](cdx/device.md) |
| `cdx:gomod` | Namespace for properties specific to the Go Module ecosystem. | [CycloneDX Go Maintainers] | [cdx:gomod taxonomy](cdx/gomod.md) |
| `cdx:npm` | Namespace for properties specific to the Node NPM ecosystem. | [CycloneDX JavaScript Maintainers] | [cdx:npm taxonomy](cdx/npm.md) |
| `cdx:pipenv` | Namespace for properties specific to the Python Pipenv ecosystem. | [CycloneDX Python Maintainers] | [cdx:pipenv taxonomy](cdx/pipenv.md) |
| `cdx:poetry` | Namespace for properties specific to the Python Poetry ecosystem. | [CycloneDX Python Maintainers] | [cdx:poetry taxonomy](cdx/poetry.md) |

## Registering `cdx` Namespaces and Properties

The process for registering new `cdx` namespaces and properties is to
[create a new issue requesting it](https://github.com/CycloneDX/cyclonedx-property-taxonomy/issues/new).

If you are requesting a new namespace directly under the `cdx` namespace,
the request will be reviewed by the Core Working Group.

If you are requesting a new namespace or property under one of the
namespaces within `cdx`, it will be reviewed by the team identified in the
table above.

[CycloneDX Core Working Group]: https://github.com/orgs/CycloneDX/teams/core-team
[CycloneDX PHP Maintainers]: https://github.com/orgs/CycloneDX/teams/php-maintainers
[CycloneDX Go Maintainers]: https://github.com/orgs/CycloneDX/teams/go-maintainers
[CycloneDX Python Maintainers]: https://github.com/orgs/CycloneDX/teams/python-maintainers
[CycloneDX JavaScript Maintainers]: https://github.com/orgs/CycloneDX/teams/javascript-maintainers