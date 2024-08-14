## `cdx:rustc` Namespace Taxonomy

This namespace is used for recording information that is used by the Rust compiler, `rustc`, irrespective of the build system. For properties specific to the Rust build system, Cargo, please refer to the `cargo` namespace.

_Boolean value_ are `true` or `false`. Case sensitive.

_Target triple string_ is a case-sensitive string matching one of the Rust compilation target triples, e.g. `x86_64-unknown-linux-gnu`. All known targets are documented [here](https://doc.rust-lang.org/nightly/rustc/platform-support.html) and the list evolves over time, with targets being both added and removed. The list of target triples supported by the installed version of the Rust compiler can be obtained by running `rustc --print=target-list`.

| Namespace | Description |
| --------- | ----------- |
| `cdx:rustc:sbom` | Namespace for information about the SBOM. MAY only appear in the `$.metadata` field, and not in any other fields. |

## `cdx:rustc:sbom` Namespace Taxonomy

| Namespace | Description |
| --------- | ----------- |
| `cdx:rustc:sbom:target` | Records the information about the build target described by the SBOM. |

## `cdx:rustc:sbom:target` Namespace Taxonomy

| Property | Description |
| -------- | ----------- |
| `cdx:rustc:sbom:target:triple` | Target triple string. Its presence indicates that the list of dependency packages in the `$.components` field will only include dependencies used for this target, matching the dependencies of the compiled binary for this target.<br/> This property may appear multiple times, e.g. when describing MacOS fat binaries that merge builds for several different architectures into a single file, or to record the list of specific platforms considered when producing the SBOM without actually performing a build.<br/> Mutually exclusive with `cdx:rustc:sbom:target:all_targets`. |
| `cdx:rustc:sbom:target:all_targets` | _Boolean value_ indicating that the SBOM includes dependency packages from all possible targets in the `$.components` field, rather than for a single specific target.<br/> Mutually exclusive with `cdx:rustc:sbom:target:triple`. MAY appear at most once. |

If neither `:triple` nor `:all_targets` properties are present, the platform coverage of the SBOM SHOULD be assumed to be unknown.
