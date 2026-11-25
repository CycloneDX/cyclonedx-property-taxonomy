# `cdx:maven` Namespace Taxonomy

This is the namespace for official CycloneDX properties related to the [Maven ecosystem](https://maven.apache.org/).

The official rules and processes apply - see [parent document](../cdx.md).

----

| Namespace | Description |
|-----------|-------------|
| `cdx:maven:license` | Namespace for properties of a license read from a POM. |
| `cdx:maven:package` | Namespace for package specific properties. |

_Boolean value_ are `true` or `false`; case sensitive.

## `cdx:maven:license` Namespace Taxonomy

Properties in this namespace are set on a license object, in `components[].licenses[].license.properties` and
`metadata.component.licenses[].license.properties`, for a license read from a POM `<license>` entry.

| Property | Description |
|----------|-------------|
| `cdx:maven:license:comments` | The `<comments>` of the POM `<license>` entry this license object was read from: addendum information the POM author attached to that license, for example that it covers only part of the package. Free text for a reader, with whitespace collapsed to single spaces; set only when the element is present and not blank. The property states nothing about how the comment changes the license. May appear once. |

## `cdx:maven:package` Namespace Taxonomy

| Property | Description |
|----------|-------------|
| `cdx:maven:package:test` | Whether the package is used only within `test` scope for Maven and `test.*` configurations for Gradle. _Boolean value_. If the property is missing, then assume the value to be `false`. May appear once. |
| `cdx:maven:package:metadata-unresolved` | Why the package's Maven metadata could not be obtained in full, so that a component whose metadata was unavailable is distinguishable from one that declares nothing. Value MUST be a single keyword [listed in the section below](#reasons-for-unresolved-package-metadata). If the property is missing, then the metadata was read in full. May appear once. |

### Reasons for unresolved package metadata

These values MUST be used on the `cdx:maven:package:metadata-unresolved` property. A value MUST NOT claim a more
specific cause than the evidence supports.

| Value | Description |
| ----- | ----------- |
| `pom-unresolved` | No usable POM artifact was obtained. |
| `pom-unparseable` | A POM was obtained and could not be read. |
| `parent-unresolved` | The POM was read, and the parent POM it declares was not obtained. |
| `model-incomplete` | The effective model could not be built, and the failing input could not be identified. |
