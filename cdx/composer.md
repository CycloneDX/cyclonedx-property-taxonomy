# `cdx:composer` Namespace Taxonomy

This is the namespace for official CycloneDX properties related to the [PHP Composer ecosystem](https://getcomposer.org/).

The official rules and processes apply - see [parent document](../cdx.md).

----

| Namespace | Description |
|-----------|-------------|
| `cdx:composer:package` | Namespace for package specific properties. |

_Boolean value_ are `true` or `false`; case sensitive.

## `cdx:composer:package` Namespace Taxonomy

| Property | Description |
|----------|-------------|
| `cdx:composer:package:type` | The [package type][composer-schema-packageType] of the component. If the property is missing, then assume the value to be `library`. May appear once. |
| `cdx:composer:package:isDevRequirement` | Whether the package was flagged as "dev requirement". _Boolean value_. If the property is missing, then assume the value to be `false`. May appear once. |
| `cdx:composer:package:sourceReference` | The repository reference of this package, e.g. master, 1.0.0 or a commit hash for git. Values may be applied to [`externalReferences`][CDX-useCases-externalReferences] of type `vcs`. _Non-empty string value_. May appear once. |
| `cdx:composer:package:distReference` | The reference of the distribution archive of this version, e.g. master, 1.0.0 or a commit hash for git. Values may be applied to [`externalReferences`][CDX-useCases-externalReferences] of type `distribution`. _Non-empty string value_. May appear once. |

[composer-schema-packageType]: https://getcomposer.org/doc/04-schema.md#type
[CDX-useCases-externalReferences]: https://cyclonedx.org/use-cases/#external-references
