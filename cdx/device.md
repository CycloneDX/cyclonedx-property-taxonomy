# `cdx:device` Namespace Taxonomy

| Namespace | Description |
|-----------|-------------|
| `cdx:device:quantity` | The total number of the specified component. |
| `cdx:device:function` | The purpose of the component (Bluetooth, network, storage, microprocessor, connector, etc) |
| `cdx:device:location` | The location on the board or related daughter-boards where the device exists. |
| `cdx:device:deviceType` | The type of component such as SMD, thru-hole, etc |
| `cdx:device:serialNumber` | Unique identifier using serial number if available |
| `cdx:device:sku` | Internal inventory reference if available |
| `cdx:device:lotNumber` | Lot or batch identification for the component |
| `cdx:device:prodTimestamp` | Production timestamp for the component |
| `cdx:device:macAddress` | Hardware address for network interfaces |

## `cdx:device:bom` Namespace Taxonomy

| Property | Description |
|----------|-------------|
| `cdx:device:bom:ebom` | Location to the Engineering Bill of Materials. This BOM contains assembly-component structure with documents coming from the CAD systems along with information about how the product is engineered. |
| `cdx:device:bom:mbom` | Location to the Manufacturing Bill of Materials. MBOM represents the data that is needed to perform product assembly. |

## `cdx:device:certifications` Namespace Taxonomy

| Property | Description |
|----------|-------------|
| `cdx:device:certifications:<ISO-3166-1>` | ISO-3166-1 alpha-2 country code of a certifying authority |
| `cdx:device:certifications:<ISO-3166-1>:<AUTHORITY>` | Abbreviation of the certifying authority (e.g. FCC, UL, and CE) |
| `cdx:device:certifications:<ISO-3166-1>:<AUTHORITY>:id` | Identifier for radio components. |
| `cdx:device:certifications:<ISO-3166-1>:<AUTHORITY>:url` | URL to certification details. |

## `cdx:device:gs1` Namespace Taxonomy

| Property | Description |
|----------|-------------|
| `cdx:device:gs1:epcRfid` | Electronic Product Code - RFID (EPC Tag Data Standard) |
| `cdx:device:gs1:giai` | Global Individual Asset Identifier (GIAI) |
| `cdx:device:gs1:gln` | Global Location Number (GLN) |
| `cdx:device:gs1:gmn` | Global Model Number (GMN) |
| `cdx:device:gs1:gtin-8` | Global Trade Identification Number (GTIN-8 / EAN/UCC-8) |
| `cdx:device:gs1:gtin-12` | Global Trade Identification Number (GTIN-12 / UPC-A) |
| `cdx:device:gs1:gtin-13` | Global Trade Identification Number (GTIN-13 / EAN/UCC-13) |
| `cdx:device:gs1:gtin-14` | Global Trade Identification Number (GTIN / EAN/UCC-14 or ITF-14) |
