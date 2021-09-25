## `cdx:gomod` Namespace Taxonomy

| Namespace               | Description                                                       |
| ----------------------- | ----------------------------------------------------------------- |
| `cdx:gomod:application` | Namespace for application metadata.                               |
| `cdx:gomod:binary`      | Namespace for metadata of analyzed binaries.                      |
| `cdx:gomod:build`       | Namespace for build related information.                          |
| `cdx:gomod:build:env`   | Namespace for build constraints passed via environment variables. |

## `cdx:gomod:application` Namespace Taxonomy

| Property                     | Description                                              |
| ---------------------------- | -------------------------------------------------------- |
| `cdx:gomod:application:name` | Name of the application that the SBOM was generated for. |

## `cdx:gomod:binary` Namespace Taxonomy

| Property                            | Description                  |
| ----------------------------------- | ---------------------------- |
| `cdx:gomod:binary:name`             | Name of the analyzed binary. |
| `cdx:gomod:binary:hash:<ALGORITHM>` | Hash of the analyzed binary. |

## `cdx:gomod:build` Namespace Taxonomy

| Property              | Description           |
| --------------------- | --------------------- |
| `cdx:gomod:build:tag` | Additional build tags |

## `cdx:gomod:build:env` Namespace Taxonomy

| Property                          | Description                                        |
| --------------------------------- | -------------------------------------------------- |
| `cdx:gomod:build:env:GOARCH`      | The target architecture (386, amd64, etc.)         |
| `cdx:gomod:build:env:GOOS`        | The target operating system (linux, windows, etc.) |
| `cdx:gomod:build:env:CGO_ENABLED` | Whether or not CGO is enabled                      |
| `cdx:gomod:build:env:GOVERSION`   | Version of the Go compiler                         |
