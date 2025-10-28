# CycloneDX Property Taxonomy

[![shield_license]][license_file]
[![shield_website]][link_website]
[![shield_slack]][link_slack]
[![shield_groups]][link_discussion]
[![shield_twitter-follow]][link_twitter]

This is the official [CycloneDX][link_website] property namespace and name taxonomy.

[shield_license]: https://img.shields.io/github/license/CycloneDX/cyclonedx-property-taxonomy?logo=open%20source%20initiative&logoColor=white "license"
[shield_website]: https://img.shields.io/badge/https://-cyclonedx.org-blue.svg "homepage"
[shield_slack]: https://img.shields.io/badge/slack-join-blue?logo=Slack&logoColor=white "slack join"
[shield_groups]: https://img.shields.io/badge/discussion-groups.io-blue.svg "groups discussion"
[shield_twitter-follow]: https://img.shields.io/badge/Twitter-follow-blue?logo=Twitter&logoColor=white "twitter follow"
[license_file]: https://github.com/CycloneDX/cyclonedx-property-taxonomy/blob/main/LICENSE
[link_website]: https://cyclonedx.org/
[link_slack]: https://cyclonedx.org/slack/invite
[link_discussion]: https://groups.io/g/CycloneDX
[link_twitter]: https://twitter.com/CycloneDX_Spec

## Introduction

With the [v1.3 release](https://github.com/CycloneDX/specification/releases/tag/1.3) of the
[CycloneDX specification](https://github.com/CycloneDX/specification),
[custom properties](https://github.com/CycloneDX/specification/issues/42) have been added.

Although the specification doesn't impose restrictions on the property names used,
standardization can assist tool implementers and BOM consumers.

The authoritative source of official namespaces and property names is
[this repository](https://github.com/CycloneDX/cyclonedx-property-taxonomy).

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC2119](https://datatracker.ietf.org/doc/html/rfc2119).

## Property Name Structure

A CycloneDX property name has two components:

- **Namespace** (_optional_): an identifier that scopes or categorizes the property.
- **Name** (_required_): the actual key or label for the property.

When a namespace is present it is separated from the name by a single colon.  
A namespace is a hierarchical sequence of segments separated by colons. The first segment is the top-level namespace; subsequent segments are sub-namespaces.

Names and namespace segments MUST NOT contain ":".
The only characters that SHALL be used in official property namespace segments and names are alphanumerical characters, "-", "_" and " " from the US ASCII character set.

Namespaces SHOULD be lower case.  
Names MAY use upper case.

### Examples

```text
internal:information_security_classification
internal:team_responsible
internal:project:guid
```

### ABNF for Official CycloneDX Property Names

```abnf
property-name     = [ namespace delimiter ] name

namespace         = namespace-segment           ; top-level namespace
                    *( delimiter namespace-segment ) ; sub-namespaces
namespace-segment = 1*namechar

name              = 1*namechar

namechar          = ALPHA / DIGIT / "-" / "_" / " "
delimiter         = ":"
```

ABNF syntax as per [RFC5234: Augmented BNF for Syntax Specifications: ABNF](https://datatracker.ietf.org/doc/html/rfc5234).

## Registered Top-Level Namespaces

Regardless of other licensing attributes in this repository or document,  
the following table (called "registry") is marked with
<a href="http://creativecommons.org/publicdomain/zero/1.0" style="display:inline-block;">
  CC0 1.0
  <img src="https://mirrors.creativecommons.org/presskit/icons/cc.svg" height="20" style="height:1.3em!important;margin-left:3px;vertical-align:text-bottom;"/><img src="https://mirrors.creativecommons.org/presskit/icons/zero.svg" height="20" style="height:1.3em!important;margin-left:3px;vertical-align:text-bottom;"/>
  <!-- The attributation icons might look broken in githubs's rendered markdown view,
   but they appear correct in any other mardown viewer, and most importantly
   they appear perfectly fine in the generated web publication: https://cyclonedx.github.io/cyclonedx-property-taxonomy/
  -->
</a>

| TL Namespace | Description | Administered By | Taxonomy |
|--------------|-------------|-----------------|----------|
| `cdx` | Namespace for official CycloneDX namespaces and properties. Unofficial sub-namespaces and properties MUST NOT be used under the `cdx` namespace. | [CycloneDX Core Working Group](https://github.com/orgs/CycloneDX) | [cdx taxonomy](cdx.md) |
| `internal` | Namespace for **internal use only**. BOMs shared with 3rd parties SHOULD NOT include properties in this namespace. | N/A | N/A |
| `urn` | Namespace **blocked** to prevent confusions with [Uniform Resource Name](https://datatracker.ietf.org/doc/html/rfc2141) | N/A | N/A |
| `aboutcode` | Namespace for use by AboutCode projects. | [AboutCode.org](https://github.com/aboutcode-org) | [AboutCode taxonomy](https://github.com/aboutcode-org/aboutcode-cyclonedx-taxonomy#readme) |
| `accellence` | Namespace for use by Accellence Technologies. | [AccellenceTechnologies](https://github.com/AccellenceTechnologies) | [Accellence taxonomy](https://github.com/AccellenceTechnologies/cyclonedx-property-taxonomy#readme) |
| `amazon` | Namespace for use by Amazon. | [Amazon](https://github.com/amzn) | [Amazon Inspector](https://docs.aws.amazon.com/inspector/latest/user/cyclonedx-namespace.html) |
| `appknox` | Namespace for use by Appknox Platform. | [Appknox](https://github.com/appknox) | [Appknox taxonomy](https://github.com/appknox/cyclonedx-property-taxonomy#readme) |
| `aquasecurity` | Namespace for use by Aqua Security. | [Aqua Security](https://github.com/aquasecurity) | `RESERVED` |
| `atis` | Namespace for use by Alliance for Telecommunications Industry Solutions (ATIS) | [ATIS](https://atis.org/) | [ATIS taxonomy](https://github.com/atisorg/cyclonedx-property-taxonomy/) |
| `boschrexroth` | Namespace for use by Bosch Rexroth. | [Bosch Rexroth AG](https://github.com/boschrexroth) | [Bosch Rexroth taxonomy](https://github.com/boschrexroth/cyclonedx-property-taxonomy#readme) |
| `bsi` | Namespace for use by BSI. | [BSI](https://github.com/BSI-Bund) | [BSI taxonomy](https://github.com/BSI-Bund/tr-03183-cyclonedx-property-taxonomy) |
| `bytetrail` | Namespace for use by ByteTrail. | [ByteTrail](https://github.com/bytetrail) | `RESERVED` |
| `codenotary` | Namespace for use by Codenotary platform. | [Codenotary](https://github.com/codenotary) | [Codenotary taxonomy](https://github.com/codenotary/cyclonedx-property-taxonomy#readme) |
| `contact-software` | Namespace for use by Contact Software. | [Contact Software](https://github.com/cslab) | `RESERVED` |
| `dependency-track` | Namespace for use by the OWASP Dependency-Track project. | [Dependency-Track Maintainers](https://github.com/DependencyTrack) | [Dependency-Track taxonomy](https://github.com/DependencyTrack/cyclonedx-property-taxonomy) |
| `expliot` | Namespace for use by EXPLIoT. | [EXPLIoT](https://gitlab.com/expliot_framework) | [EXPLIoT taxonomy](https://gitlab.com/expliot_framework/expliot/-/blob/master/docs/compliance/cyclonedx.rst) |
| `finitestate` | Namespace for the use by Finite State. | [Finite State](https://github.com/FiniteStateInc) | [finitestate taxonomy](https://github.com/FiniteStateInc/cyclonedx-property-taxonomy#readme) |
| `fortify` | Namespace for use by Fortify. | [Micro Focus](https://github.com/MicroFocus) | `RESERVED` |
| `gitlab` | Namespace for use by GitLab. | [GitLab](https://gitlab.com) | [GitLab taxonomy](https://docs.gitlab.com/ee/development/sec/cyclonedx_property_taxonomy.html) |
| `grype` | Namespace for use by the Grype project. | [Grype Maintainers](https://github.com/anchore/grype) | `RESERVED` |
| `hoppr` | Namespace for the use by the Hoppr project. | [Lockheed Martin](https://hoppr.dev) | [Hoppr Taxonomy Documentation](https://hoppr.dev/docs/architecture/cdx-taxonomy) |
| `ibm` | Namespace for use by IBM. | [IBM](https://github.com/IBM) | `RESERVED` |
| `interlynk` | Namespace for use by Interlynk. | [Interlynk](https://github.com/interlynk-io) | [Interlynk taxonomy](https://github.com/interlynk-io/cyclonedx-property-taxonomy) |
| `jfrog` | Namespace for use by JFrog. | [JFrog](https://jfrog.com) | `RESERVED` |
| `medical-aegis` | Namespace for use by Medical Aegis. | [Medical Aegis](https://github.com/Medical-Aegis) | `RESERVED` |
| `nix` | Namespace for Nix properties. | [Nixpkgs Maintainers](https://github.com/NixOS/nixpkgs/) | [Nixpkgs Manual](https://nixos.org/manual/nixpkgs/unstable/#sec-interop.cylonedx-nix) |
| `nvidia` | Namespace for NVIDIA properties. | [NVIDIA](https://github.com/NVIDIA) | [NVIDIA Taxonomy Documentation](https://github.com/NVIDIA/Trustworthy-AI/blob/main/CycloneDX-Property-Taxonomy/cyclonedx-property-taxonomy.md) |
| `observer` | Namespace for use by SBOM Observer. | [Bitfront](https://github.com/bitfront-se) | [SBOM Observer Taxonomy](https://github.com/bitfront-se/cyclonedx-property-taxonomy) |
| `ort` | Namespace for use by the OSS Review Toolkit. | [OSS Review Toolkit](https://github.com/oss-review-toolkit) | [ORT taxonomy](https://github.com/oss-review-toolkit/ort/tree/main/plugins/reporters/cyclonedx#property-taxonomy) |
| `rad` | Namespace for use by RAD Security. | [RAD Security](https://github.com/rad-security) | [RAD KBOM Taxonomy](https://github.com/rad-security/kbom/blob/main/docs/taxonomy.md) |
| `recon` | Namespace for use by the Recon Project. | [Recon Project](https://github.com/rusty-ferris-club/recon) | `RESERVED` |
| `redhat` | Namespace for use by Red Hat. | [Red Hat](https://github.com/RedHatOfficial/) | `RESERVED` |
| `scribe` | Namespace for use by Scribe Security | [Scribe Security](https://github.com/scribe-security) | `RESERVED` |
| `servicenow` | Namespace for use by ServiceNow. | [ServiceNow](https://github.com/ServiceNow) | `RESERVED` |
| `siemens` | Namespace for use by Siemens. | [Siemens](https://github.com/siemens) | [Siemens taxonomy](https://github.com/siemens/cyclonedx-property-taxonomy#readme) |
| `snyk` | Namespace for use by Snyk. | [Snyk](https://github.com/snyk) | [Snyk Taxonomy Documentation](https://docs.snyk.io/snyk-api-info/get-a-projects-sbom-document-endpoint#custom-cyclonedx-properties) |
| `sonatype` | Namespace for use by Sonatype | [Sonatype](https://github.com/sonatype) | [Sonatype Taxonomy Documentation](https://help.sonatype.com/lift/open-source-vulnerability-analysis/dependency-view/cyclonedx-sonatype-namespace-taxonomy) |
| `soos` | Namespace for use by SOOS. | [SOOS](https://github.com/soos-io) | [SOOS taxonomy](https://github.com/soos-io/cyclonedx-property-taxonomy) |
| `spack` | Namespace for use by the Spack package manager. | [Spack Maintainers](https://github.com/spack) | [Spack SBOM Project](https://github.com/spack/spack-sbom#readme) |
| `stackable` | Namespace for use by Stackable | [Stackable](https://github.com/stackabletech) | [Stackable taxonomy](https://github.com/stackabletech/cyclonedx-property-taxonomy) |
| `syft` | Namespace for use by the Syft project. | [Syft Maintainers](https://github.com/anchore/syft) | `RESERVED` |
| `tern` | Namespace for use by the Tern project. | [Tern Maintainers](https://github.com/tern-tools/tern) | `RESERVED` |
| `veracode` | Namespace for use by Veracode. | [Veracode](https://github.com/veracode) | [Veracode taxonomy](https://github.com/veracode/cyclonedx-property-taxonomy#readme) |

## Registering new Top-Level Namespaces

It is RECOMMENDED that anyone creating custom properties outside of the `internal`
namespace SHOULD register a new top-level namespace.

The process for registering a new top-level namespace is to
[create a new issue requesting it](https://github.com/CycloneDX/cyclonedx-property-taxonomy/issues/new).

Top-level namespaces are initially registered as `RESERVED`.

Registered top-level namespaces SHOULD be more than two characters long.

Before using your `RESERVED` namespace, documentation for the taxonomy of the
namespace SHOULD be publicly available. Failure to do so MAY result in the
namespace reservation being revoked.

An example is the [`cdx` taxonomy](cdx.md).
