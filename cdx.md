# `cdx` Namespace Taxonomy

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL"
in this document are to be interpreted as described in [RFC2119](http://www.ietf.org/rfc/rfc2119.txt).

_Boolean value_ are `true` or `false`. Case sensitive.

| Property | Description |
|----------|-------------|
| `cdx:reproducible` | Whether the CycloneDX document has been generated in a reproducible manner: if so, then time- or random-based values MUST be omitted, and elements order SHOULD be reproducible. <br/> _Boolean value_ - defaults to `false`. <br/> MAY appear only once. SHOULD be used in `$.metadata.properties`. |

| Namespace | Description | Administered By | Taxonomy |
|-----------|-------------|-----------------|----------|
| `cdx:composer` | Namespace for properties specific to the PHP Composer ecosystem. | [CycloneDX PHP Maintainers] | [cdx:composer taxonomy](cdx/composer.md) |
| `cdx:device` | Namespace for properties specific to hardware devices. | [CycloneDX Core Working Group] | [cdx:device taxonomy](cdx/device.md) |
| `cdx:gomod` | Namespace for properties specific to the Go Module ecosystem. | [CycloneDX Go Maintainers] | [cdx:gomod taxonomy](cdx/gomod.md) |
| `cdx:lifecycle` | Namespace for properties specific to component and service lifecycles. | [CycloneDX Core Working Group] | [cdx:lifecycle taxonomy](cdx/lifecycle.md) |
| `cdx:maven` | Namespace for properties specific to the Maven ecosystem. | [CycloneDX Maven Maintainers] [CycloneDX Gradle Maintainers] | [cdx:maven taxonomy](cdx/maven.md) |
| `cdx:npm` | Namespace for properties specific to the Node NPM ecosystem. | [CycloneDX JavaScript Maintainers] | [cdx:npm taxonomy](cdx/npm.md) |
| `cdx:pipenv` | Namespace for properties specific to the Python Pipenv ecosystem. | [CycloneDX Python Maintainers] | [cdx:pipenv taxonomy](cdx/pipenv.md) |
| `cdx:poetry` | Namespace for properties specific to the Python Poetry ecosystem. | [CycloneDX Python Maintainers] | [cdx:poetry taxonomy](cdx/poetry.md) |
| `cdx:python` | Namespace for properties specific to the Python general packaging. | [CycloneDX Python Maintainers] | [cdx:python taxonomy](cdx/python.md) |
| `cdx:rustc` | Namespace for properties specific to the Rust compiler, `rustc`. | [CycloneDX Rust Maintainers] | [cdx:rustc taxonomy](cdx/rustc.md) |

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
[CycloneDX Rust Maintainers]: https://github.com/orgs/CycloneDX/teams/rust-maintainers
[CycloneDX Maven Maintainers]: https://github.com/orgs/CycloneDX/teams/maven-maintainers
[CycloneDX Gradle Maintainers]: https://github.com/orgs/CycloneDX/teams/gradle-maintainers
