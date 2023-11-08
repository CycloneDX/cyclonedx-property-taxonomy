# CycloneDX Property Taxonomy

[![License](https://img.shields.io/badge/license-apache%20v2-brightgreen.svg)](https://github.com/CycloneDX/cyclonedx-property-taxonomy/blob/master/LICENSE)
[![Website](https://img.shields.io/badge/https://-cyclonedx.org-blue.svg)](https://cyclonedx.org/)
[![Slack Invite](https://img.shields.io/badge/Slack-Join-blue?logo=slack&labelColor=393939)](https://cyclonedx.org/slack/invite)
[![Group Discussion](https://img.shields.io/badge/discussion-groups.io-blue.svg)](https://groups.io/g/CycloneDX)
[![Twitter](https://img.shields.io/twitter/url/http/shields.io.svg?style=social&label=Follow)](https://twitter.com/CycloneDX_Spec)

This is the official CycloneDX property namespace and name taxonomy.

## Introduction

With the v1.3 release of the specification, custom properties have been added.

Although the specification doesn't impose restrictions on the property names used,
standardization can assist tool implementers and BOM consumers.

The authoritative source of official namespaces and property names is this repository.

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC2119](http://www.ietf.org/rfc/rfc2119.txt).

## Namespace Syntax

Namespaces are hierarchical and delimited with a `:`.

As such, `:` MUST NOT be used in property namespaces and names except as a delimiter.

The only characters that SHALL be used in official property namespaces and names are alphanumerical characters, "-", "_" and " " from the US ASCII character set.

Namespaces SHOULD be lower case. Base property names MAY use upper case.

### Examples

```text
internal:information_security_classification
internal:team_responsible
```

### ABNF for Official CycloneDX Property Names

```ABNF
property-name = 1*(namespace ":") name

namespace     = 1*namechar

name          = 1*namechar

namechar      = ALPHA / DIGIT / "-" / "_" / " "
```

ABNF syntax as per [RFC5234: Augmented BNF for Syntax Specifications: ABNF](https://datatracker.ietf.org/doc/html/rfc5234).

## Registered Top Level Namespaces

| Namespace | Description | Administered By | Taxonomy |
| --- | --- | --- | --- |
| `cdx` | Namespace for official CycloneDX namespaces and properties. Unofficial namespaces and properties MUST NOT be used under the `cdx` namespace. | [CycloneDX Core Working Group](https://github.com/orgs/CycloneDX) | [cdx taxonomy](cdx.md) |
| `internal` | Namespace for internal use only. BOMs shared with 3rd parties SHOULD NOT include properties in this namespace. | N/A | N/A |
| `urn` | Namespace blocked to prevent confusions with [Uniform Resource Name](https://www.rfc-editor.org/rfc/rfc2141) | N/A | N/A |
| `aboutcode` | Namespace for use by AboutCode projects. | [nexB](https://github.com/nexB) | [AboutCode taxonomy](https://github.com/nexB/aboutcode-cyclonedx-taxonomy#readme) |
| `amazon` | Namespace for use by Amazon. | [Amazon](https://github.com/amzn) | `RESERVED` |
| `appknox` | Namespace for use by Appknox Platform. | [Appknox](https://github.com/appknox) | [Appknox taxonomy](https://github.com/appknox/cyclonedx-property-taxonomy#readme) |
| `aquasecurity` | Namespace for use by Aqua Security. | [Aqua Security](https://github.com/aquasecurity) | `RESERVED` |
| `boschrexroth` | Namespace for use by Bosch Rexroth. | [Bosch Rexroth AG](https://github.com/boschrexroth) | [Bosch Rexroth taxonomy](https://github.com/boschrexroth/cyclonedx-property-taxonomy#readme) |
| `bytetrail` | Namespace for use by ByteTrail. | [ByteTrail](https://github.com/bytetrail) | `RESERVED` |
| `codenotary` | Namespace for use by Codenotary platform. | [Codenotary](https://github.com/codenotary) | [Codenotary taxonomy](https://github.com/codenotary/cyclonedx-property-taxonomy) |
| `dependency-track` | Namespace for use by the Dependency-Track project. | [Dependency-Track Maintainers](https://github.com/DependencyTrack) | `RESERVED` |
| `expliot` | Namespace for use by EXPLIoT. | [EXPLIoT](https://gitlab.com/expliot_framework) | [EXPLIoT taxonomy](https://gitlab.com/expliot_framework/expliot/-/blob/master/docs/compliance/cyclonedx.rst) |
| `finitestate` | Namespace for the use by Finite State. | [Finite State](https://github.com/FiniteStateInc) | [finitestate taxonomy](https://github.com/FiniteStateInc/cyclonedx-property-taxonomy#readme) |
| `fortify` | Namespace for use by Fortify. | [Micro Focus](https://github.com/MicroFocus) | `RESERVED` |
| `gitlab` | Namespace for use by GitLab. | [GitLab](https://gitlab.com) | [GitLab taxonomy](https://docs.gitlab.com/ee/development/sec/cyclonedx_property_taxonomy.html) |
| `grype` | Namespace for use by the Grype project. | [Grype Maintainers](https://github.com/anchore/grype) | `RESERVED` |
| `hoppr` | Namespace for the use by the Hoppr project. | [Lockheed Martin](https://hoppr.dev/) | `RESERVED` |
| `ibm` | Namespace for use by IBM. | [IBM](https://github.com/IBM) | `RESERVED` |
| `ksoc` | Namespace for use by KSOC. | [KSOC](https://github.com/ksoclabs) | [KSOC taxonomy](https://github.com/ksoclabs/kbom/blob/main/docs/taxonomy.md) |
| `medical-aegis` | Namespace for use by Medical Aegis. | [Medical Aegis](https://github.com/Medical-Aegis) | `RESERVED` |
| `recon` | Namespace for use by the Recon Project. | [Recon Project](https://github.com/rusty-ferris-club/recon) | `RESERVED` |
| `servicenow` | Namespace for use by ServiceNow. | [ServiceNow](https://github.com/ServiceNow) | `RESERVED` |
| `siemens` | Namespace for use by Siemens. | [Siemens](https://github.com/siemens) | [Siemens taxonomy](https://github.com/siemens/cyclonedx-property-taxonomy#readme) |
| `snyk` | Namespace for use by Snyk. | [Snyk](https://github.com/snyk) | [Snyk Taxonomy Documentation](https://docs.snyk.io/snyk-api-info/get-a-projects-sbom-document-endpoint#custom-cyclonedx-properties) |
| `sonatype` | Namespace for use by Sonatype | [Sonatype](https://github.com/sonatype) | [Sonatype Taxonomy Documentation](https://help.sonatype.com/lift/open-source-vulnerability-analysis/dependency-view/cyclonedx-sonatype-namespace-taxonomy) |
| `spack` | Namespace for use by the Spack package manager. | Spack Maintainers | [Spack SBOM Project](https://github.com/spack/spack-sbom#readme) |
| `stackable` | Namespace for use by Stackable | [Stackable](https://github.com/stackabletech) | `RESERVED` |
| `syft` | Namespace for use by the Syft project. | [Syft Maintainers](https://github.com/anchore/syft) | `RESERVED` |
| `tern` | Namespace for use by the Tern project. | [Tern Maintainers](https://github.com/tern-tools/tern) | `RESERVED` |
| `veracode` | Namespace for use by Veracode. | [Veracode](https://github.com/veracod) | [Veracode taxonomy](https://github.com/veracode/cyclonedx-property-taxonomy#readme) |

## Registering New Top Level Namespaces

It is RECOMMENDED that anyone creating custom properties outside of the `internal`
namespace SHOULD register a new top level namespace.

The process for registering a new top level namespace is to
[create a new issue requesting it](https://github.com/CycloneDX/cyclonedx-property-taxonomy/issues/new).

Namespaces are initially registered as `RESERVED`.

Before using your `RESERVED` namespace, documentation for the taxonomy of the
namespace SHOULD be publicly available. Failure to do so MAY result in the
namespace reservation being revoked.

An example is the [cdx taxonomy](cdx.md).
