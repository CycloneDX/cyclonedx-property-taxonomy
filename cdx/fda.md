# `cdx:fda` Namespace Taxonomy

This is the namespace for official CycloneDX properties carrying SBOM information for premarket submissions under the U.S. FDA guidance [*Cybersecurity in Medical Devices: Quality Management System Considerations and Content of Premarket Submissions*](https://www.fda.gov/media/119933/download), issued February 3, 2026 (referred to below as "the guidance").

The official rules and processes apply - see [parent document](../cdx.md).

Guidance-defined properties cite the relevant section for traceability. Section V.A.4(b) permits the additional component-support elements to be provided as part of the SBOM or separately in an addendum; this namespace provides an in-SBOM representation. Properties identified below as namespace conventions support submission workflows but are not fields defined by the guidance.

Dates MUST use the RFC 3339 `full-date` form, `YYYY-MM-DD`. Component-level properties attach to `components[].properties`, or to `metadata.component.properties` when they describe the device as a whole. Properties are repeatable unless stated otherwise. The key words MUST, SHOULD, and MAY are to be interpreted as described in [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119).

Known vulnerabilities, vulnerability-discovery methods, vulnerability risk assessments, and vulnerability risk controls are outside the scope of this SBOM-property namespace and are deferred to a separate vulnerability-management document.

----

## Guidance Mapping

This mapping is informative. The property definitions below are normative for properties in this namespace.

| FDA information or convention | CycloneDX 1.x core mapping | `cdx:fda` property where core does not completely cover it |
|---|---|---|
| Level of support (§V.A.4(b)) | - | `cdx:fda:level-of-support`, free text; use the guidance examples `actively maintained`, `no longer maintained`, and `abandoned` verbatim when applicable |
| End-of-support date (§V.A.4(b)) | `cdx:lifecycle:milestone:endOfSupport` | `cdx:fda:end-of-support-date`; when both properties occur, they should identify the same milestone, while the lifecycle property may use an ISO 8601 date or timestamp as its taxonomy permits |
| End of life (§VI.A) | `cdx:lifecycle:milestone:endOfLife` | `cdx:fda:end-of-life-date`; representing the information as a date is a namespace convention; when both properties occur, they should identify the same milestone, while the lifecycle property may use an ISO 8601 date or timestamp as its taxonomy permits |
| Justification when information cannot be provided (§V.A.4(b)) | - | `cdx:fda:justification`, repeatable; value is `<AFFECTED_CDX_FDA_PROPERTY_NAME>: <free-text justification>`, one instance per property that cannot be answered |
| Plan to update or replace a third-party component if support ends (§V.A.4) | - | `cdx:fda:update-or-replace-plan` |
| Custodial control of device source code, such as escrow or backups (§V.A.4 and footnote 36) | - | `cdx:fda:source-code-custody` |
| Risk-transfer process when a device remains in service after end of support (§VI.A) | - | `cdx:fda:risk-transfer-process` |
| Traceability between the threat model, cybersecurity risk assessment, SBOM, and testing documentation (§V.A) | - | `cdx:fda:traceability`; value is the corresponding traceability record identifier |
| Date on which support determinations were made | - | `cdx:fda:support-assessed-date`, a namespace-defined submission-support field rather than an FDA-defined field |

## Properties

| Property | Description |
|----------|-------------|
| `cdx:fda:level-of-support` | The software level of support provided through monitoring and maintenance by the software component manufacturer (guidance §V.A.4(b)).<br/> The value is free text.<br/> The guidance's examples `actively maintained`, `no longer maintained`, and `abandoned` SHOULD be used verbatim when applicable.<br/> MAY appear only once per component. |
| `cdx:fda:end-of-support-date` | The software component's end-of-support date (guidance §V.A.4(b)).<br/> If no date can be provided, this property MUST be omitted and a `cdx:fda:justification` property provided.<br/> When `cdx:lifecycle:milestone:endOfSupport` is also present for the component, the two properties SHOULD identify the same milestone; the lifecycle property remains governed by the `cdx:lifecycle` taxonomy and may contain an ISO 8601 date or timestamp.<br/> MAY appear only once per component. |
| `cdx:fda:end-of-life-date` | A date representing the known or anticipated component end of life described in guidance §VI.A.<br/> Representing this information as a date, and using `cdx:fda:justification` when no date can be provided, are namespace conventions.<br/> If no date can be provided, this property MUST be omitted and a `cdx:fda:justification` property provided.<br/> When `cdx:lifecycle:milestone:endOfLife` is also present for the component, the two properties SHOULD identify the same milestone; the lifecycle property remains governed by the `cdx:lifecycle` taxonomy and may contain an ISO 8601 date or timestamp.<br/> MAY appear only once per component. |
| `cdx:fda:justification` | A justification for why information cannot be included in the premarket submission (guidance §V.A.4(b)).<br/> The value MUST contain the affected `cdx:fda` property name, a colon, and a free-text justification, for example `cdx:fda:end-of-support-date: upstream project publishes no support date`.<br/> One property instance MUST be provided for each property that cannot be answered. |
| `cdx:fda:update-or-replace-plan` | Describes the plan for how a third-party software component could be updated or replaced if support ends or other software issues arise (guidance §V.A.4).<br/> The value is free text and MAY contain a controlled-document identifier or URL. |
| `cdx:fda:source-code-custody` | Describes how custodial control of device source code is established and maintained, such as through source code escrow or backups (guidance §V.A.4 and footnote 36).<br/> The value is free text and MAY contain a controlled-document identifier or URL. |
| `cdx:fda:risk-transfer-process` | Describes the pre-established and pre-communicated process for transferring risks when a device remains in service after end of support (guidance §VI.A).<br/> The value is free text and MAY contain a controlled-document identifier or URL. |
| `cdx:fda:traceability` | Identifies the record providing traceability between the threat model, cybersecurity risk assessment, SBOM, and testing documentation, as recommended by guidance §V.A.<br/> The value is the corresponding traceability record identifier. |
| `cdx:fda:support-assessed-date` | The date on which the component's level-of-support and end-of-support determinations were made.<br/> It anchors time-varying support information to the assessment used for the submission.<br/> MAY appear only once per component. |

## Example

```json
{
  "components": [
    {
      "type": "library",
      "bom-ref": "pkg:generic/dcmtk@3.6.9",
      "name": "dcmtk",
      "version": "3.6.9",
      "properties": [
        { "name": "cdx:fda:level-of-support", "value": "actively maintained" },
        { "name": "cdx:fda:end-of-support-date", "value": "2028-12-31" },
        { "name": "cdx:lifecycle:milestone:endOfSupport", "value": "2028-12-31" },
        { "name": "cdx:fda:support-assessed-date", "value": "2026-08-06" },
        { "name": "cdx:fda:update-or-replace-plan", "value": "QMS-PLN-0142" }
      ]
    }
  ]
}
```
