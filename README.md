### How to repro:

1. clone this repo
2. run `bazel build //:test`

This return an error:

```
INFO: Analyzed target //:test (0 packages loaded, 0 targets configured).
INFO: Found 1 target...
ERROR: <BAZEL/OUTPUT_BASE>/external/com_github_google_go_containerregistry/internal/estargz/BUILD.bazel:3:11: GoCompilePkg external/com_github_google_go_containerregistry/internal/estargz/estargz.a [for tool] failed: (Exit 1): builder failed: error executing command (from target @com_github_google_go_containerregistry//internal/estargz:estargz) bazel-out/darwin_arm64-opt-exec-2B5CBBC6-ST-625e526ca8a8/bin/external/go_sdk/builder compilepkg -sdk external/go_sdk -installsuffix darwin_arm64 -src ... (remaining 23 arguments skipped)

Use --sandbox_debug to see verbose messages from the sandbox and retain the sandbox build root for debugging
compilepkg: missing strict dependencies:
	<PATH/TO/EXEC/ROOT>/execroot/myworkspace/external/com_github_google_go_containerregistry/internal/estargz/estargz.go: import of "github.com/containerd/stargz-snapshotter/estargz"
No dependencies were provided.
Check that imports in Go sources match importpath attributes in deps.
Target //:test failed to build
```

Note that `go-containerregistry` is unused by this project, however it is still listed under `go list -m all`, its transitive dependencies are not.
