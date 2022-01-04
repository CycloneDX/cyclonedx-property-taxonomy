## `cdx:deviceInfo` Namespace Taxonomy

| Namespace             | Description                                                       |
| --------------------- | ----------------------------------------------------------------- |
| `cdx:deviceInfo:quantity`  | The total number of the specified component. |
| `cdx:deviceInfo:function`  | The purpose of the component (Bluetooth, network, storage, microprocessor, connector, etc)                         |
| `cdx:deviceInfo:location`  | The location on the board or related daughter-boards where the device exists. |
| `cdx:deviceInfo:deviceType`  | The type of component such as SMD, thru-hole, etc |
| `cdx:deviceInfo:serialNumber`  | Unique identifier using serial number if available |
| `cdx:deviceInfo:sku`  | Internal inventory reference if available |
| `cdx:deviceInfo:lotNumber`  | Lot or batch identification for the component |
| `cdx:deviceInfo:prodTimestamp`  | Production timestamp for the component |
| `cdx:deviceInfo:macAddress`  | Hardware address for network interfaces |

## `cdx:deviceInfo:bom` Namespace Taxonomy

| Property                            | Description                  |
| ----------------------------------- | ---------------------------- |
| `cdx:deviceInfo:bom:ebom`  | Location to the Engineering Bill of Materials. This BOM contains assembly-component structure with documents coming from the CAD systems along with information about how the product is engineered. |
| `cdx:deviceInfo:bom:mbom`  | Location to the Manufacturing Bill of Materials. MBOM represents the data that is needed to perform product assembly. |

## `cdx:deviceInfo:certifications` Namespace Taxonomy

| Property                            | Description                  |
| ----------------------------------- | ---------------------------- |
| `cdx:deviceInfo:certifications:<AUTHORITY>`  | A certifying authority (e.g. FCC). |
| `cdx:deviceInfo:certifications:<AUTHORITY>:id` | Identifier for radio components. |
| `cdx:deviceInfo:certifications:<AUTHORITY>:url` | URL to certification details. |

## `cdx:deviceInfo:gs1` Namespace Taxonomy

| Property                            | Description                  |
| ----------------------------------- | ---------------------------- |
| `cdx:deviceInfo:gs1:epcRfid` | Electronic Product Code - RFID (EPC Tag Data Standard) |
| `cdx:deviceInfo:gs1:giai` | Global Individual Asset Identifier (GIAI) |
| `cdx:deviceInfo:gs1:gln` | Global Location Number (GLN) |
| `cdx:deviceInfo:gs1:gmn` | Global Model Number (GMN) |
| `cdx:deviceInfo:gs1:gtin-8`  | Global Trade Identification Number (GTIN-8 / EAN/UCC-8) |
| `cdx:deviceInfo:gs1:gtin-12`  | Global Trade Identification Number (GTIN-12 / UPC-A) |
| `cdx:deviceInfo:gs1:gtin-13`  | Global Trade Identification Number (GTIN-13 / EAN/UCC-13) |
| `cdx:deviceInfo:gs1:gtin-14`  | Global Trade Identification Number (GTIN / EAN/UCC-14 or ITF-14) |
