## `cdx:rustc` Namespace Taxonomy

This namespace is used for recording information that is used by the Rust compiler, `rustc`, irrespective of the build system. For properties specific to the Rust build system, Cargo, please refer to the `cargo` namespace.

_Boolean value_ are `true` or `false`. Case sensitive.

| Namespace | Description |
| --------- | ----------- |
| `cdx:rustc:meta` | Namespace for information about the SBOM and properties that apply to the entire build. May only appear in the `$.metadata` field, and not in any other fields. |

## `cdx:rustc:meta` Namespace Taxonomy

| Namespace | Description |
| --------- | ----------- |
| `cdx:rustc:meta:target` | Records the information about the build target for the entire build. |

## `cdx:rustc:meta:target` Namespace Taxonomy

| Property  | Description                                                       |
| --------------------- | ----------------------------------------------------------------- |
| `cdx:rustc:meta:target:triple` | The target triple used for the build (e.g. `x86_64-unknown-linux-gnu`). Its presence indicates that the list of dependency packages in the `$.components` field will only include dependencies used for this one target, matching the dependencies of the compiled binary for this target. All known targets are documented [here](https://doc.rust-lang.org/nightly/rustc/platform-support.html) and the list evolves over time. Details about a specific target triple can be obtained by running `rustc --print=cfg --target=$TRIPLE` |
| `cdx:rustc:meta:target:all_targets` | Boolean value. Indicates that the SBOM includes dependency packages from all possible targets in the `$.components` field, rather than for a single specific target. |