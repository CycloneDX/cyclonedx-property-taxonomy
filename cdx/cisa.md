# `cdx:cisa` Namespace Taxonomy

This is the namespace for official CycloneDX properties carrying SBOM information defined in the [*2026 Minimum Elements for a Software Bill of Materials (SBOM)*](https://www.cisa.gov/sites/default/files/2026-07/2026_cisa_sbom_minimum_elements_508c.pdf), published July 29, 2026 by CISA and co-authoring organizations (referred to below as "the 2026 Minimum Elements"), which replaces the 2021 NTIA minimum elements. Only information without a complete native CycloneDX representation is defined here.

The official rules and processes apply - see [parent document](../cdx.md).

Where a property value names a data field, the value MUST be the data field name exactly as listed in Appendix A of the 2026 Minimum Elements (for example, `Component Version`, `Component Producer`, or `Component Hash Value`). Properties are repeatable unless stated otherwise. The key words MUST, SHOULD, and MAY are to be interpreted as described in [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119).

When a required data field is unknown, its native CycloneDX representation SHOULD also be populated when the native field supports an unknown value. For example, use the literal `unknown` for `components[].version` and `components[].manufacturer.name`, and use `compositions` to describe unknown or incomplete dependency relationships. The `cdx:cisa:unknown-information` property is still required in these cases because it explicitly identifies which required information is unknown to the SBOM author.

The CISA `SBOM Author` data field maps to `metadata.authors` when one or more people manually create the SBOM and to `metadata.manufacturer` when an organization creates it through an automated process.

----

## Guidance Mapping

This mapping is informative. The property definitions below are normative for properties in this namespace.

| Appendix A data field or CISA practice | CycloneDX 1.x mapping | `cdx:cisa` property where CycloneDX does not completely cover it |
|---|---|---|
| Component Dependency Relationship | `dependencies[]` (`ref` to `dependsOn`); completeness through `compositions` | - |
| Component Hash Algorithm | `components[].hashes[].alg` | - |
| Component Hash Value | `components[].hashes[].content` | When unknown, omit `hashes` and declare `Component Hash Value` through `cdx:cisa:unknown-information` |
| Component Identifiers | `purl`, `cpe`, `swid`, `omniborId`, and `swhid` | `cdx:cisa:component-identifier` for UUIDs and organization-specific identifiers when no more specific native field is appropriate |
| Component License | `licenses[].license.id` for SPDX identifiers; `licenses[].license.name` or other native license details when no SPDX identifier applies | - |
| Component Name | `components[].name` | `cdx:cisa:alternate-name`, repeated once per alternate name |
| Component Producer | `components[].manufacturer` | When unknown, set `manufacturer.name` to `unknown` and declare `Component Producer` through `cdx:cisa:unknown-information` |
| Component Version | `components[].version` | When unknown, set `version` to `unknown` and declare `Component Version` through `cdx:cisa:unknown-information` |
| Unknown Information | - | `cdx:cisa:unknown-information`: one instance for every required field whose value is unknown to the SBOM author; the value is the exact Appendix A data field name, even when a native field also contains `unknown` or another native mechanism describes the missing information |
| Withheld Information | - | `cdx:cisa:withheld-information`: one instance for every required field intentionally withheld from the SBOM; the value is the exact Appendix A data field name |
| Withheld Information Inquiry | - | `cdx:cisa:withheld-information-inquiry`: one document-level instance in `metadata.properties` with a textual description of how a recipient may ask about withheld or redacted security-related information |
| SBOM Author | `metadata.authors[]` when people manually create the SBOM; `metadata.manufacturer` when an organization creates it through an automated process | - |
| SBOM Author Signature | `signature`; detached signatures through `externalReferences` type `digital-signature` | - |
| SBOM Data Format Name | `bomFormat` | - |
| SBOM Data Format Version | `specVersion` | - |
| SBOM Generation Context | `metadata.lifecycles[]`, using a predefined phase or custom name | - |
| SBOM Timestamp | `metadata.timestamp` | - |
| SBOM Tool Name | `metadata.tools.components[].name` | - |
| SBOM Tool Version | `metadata.tools.components[].version` | - |
| SBOM Version | `version` and `serialNumber` | - |

## Properties

| Property | Description |
|----------|-------------|
| `cdx:cisa:unknown-information` | Explicitly identifies a required data field whose information is unknown to the SBOM author.<br/> The 2026 Minimum Elements practice *Explicitly Identifying Unknown Information* requires SBOM authors to distinguish information that is unknown from information they are withholding.<br/> The value MUST be the applicable Appendix A data field name.<br/> One property instance MUST be provided for each unknown data field, including when a native field contains `unknown` or another native mechanism also describes the missing information.<br/> Use `metadata.properties` for SBOM Metadata fields and the applicable `components[].properties` for Component Data fields. |
| `cdx:cisa:withheld-information` | Explicitly identifies a required data field whose information the SBOM author is intentionally withholding.<br/> The 2026 Minimum Elements practice *Explicitly Identifying Unknown Information* requires this information to be distinguished from information that is unknown to the author.<br/> The value MUST be the applicable Appendix A data field name.<br/> One property instance MUST be provided for each withheld data field.<br/> Use `metadata.properties` for SBOM Metadata fields and the applicable `components[].properties` for Component Data fields. |
| `cdx:cisa:withheld-information-inquiry` | Describes the process for recipients to ask about withheld or redacted security-related information, as specified by the 2026 Minimum Elements practice *Explicitly Identifying Unknown Information*.<br/> The value is free text and MAY contain a URL, email address, or document reference for the inquiry process.<br/> This document-level property MUST be placed in `metadata.properties` and MAY appear only once. |
| `cdx:cisa:alternate-name` | An alternate name for a component in addition to its native `name`.<br/> Data formats implementing Component Name are expected to allow multiple entries for alternate names.<br/> The value is one alternate name.<br/> One property instance MUST be provided for each alternate name.<br/> Component-level. |
| `cdx:cisa:component-identifier` | A UUID or organization-specific component identifier for which no more specific native CycloneDX identifier field is appropriate.<br/> Native fields such as `purl`, `cpe`, `swid`, `omniborId`, and `swhid` SHOULD be used when applicable.<br/> The value is free text and SHOULD identify its scheme, for example `urn:uuid:3e671687-395b-41f5-a30f-a58921a69b79` or `acme-part:12345`.<br/> One property instance MUST be provided for each additional identifier.<br/> Component-level. |

## Example

```json
{
  "metadata": {
    "properties": [
      {
        "name": "cdx:cisa:withheld-information-inquiry",
        "value": "Email product-security@example.com"
      }
    ]
  },
  "components": [
    {
      "type": "library",
      "name": "vendored-parser",
      "version": "unknown",
      "manufacturer": { "name": "unknown" },
      "properties": [
        { "name": "cdx:cisa:unknown-information", "value": "Component Version" },
        { "name": "cdx:cisa:unknown-information", "value": "Component Producer" },
        { "name": "cdx:cisa:unknown-information", "value": "Component Hash Value" },
        { "name": "cdx:cisa:alternate-name", "value": "legacy-parse-lib" },
        { "name": "cdx:cisa:alternate-name", "value": "parselib-ng" },
        {
          "name": "cdx:cisa:component-identifier",
          "value": "urn:uuid:3e671687-395b-41f5-a30f-a58921a69b79"
        }
      ]
    }
  ]
}
```
