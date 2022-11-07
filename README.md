# Envoy Java API

This builds a grpc library for the envoy xDS API.

## Versioning
Major and minor version follow the envoy version against which they are built. The patch version is this library's patch version. Use the latest patch version for the envoy major.minor you run, e.g. use the latest 1.17.x for this library if you run envoy 1.17.y, regardless of what y is.

## Building

The `tools` directory follows https://github.com/envoyproxy/java-control-plane/commits/main/tools as closely as possible.

1. Update the `API_SHAS` (which are not really just SHAs), either manually looking at the file, or using the `update-sha.sh` script (TODO does this already work?).

1. Update the proto files using `update-api.sh`. This will remove the old `src/main/proto` and fetch a new set of protos.

1. Bump the library version accoring to `Versioning` above in `gradle.properties`.

1. Now it should build on CI. Can try locally using `./gradlew assemble`, but see GHA workflow for specific steps.
