# Envoy Java API

This builds a grpc library for the envoy xDS API.

## Versioning
Major and minor version follow the envoy version against which they are built. The patch version is this library's patch version. Use the latest patch version for the envoy major.minor you run, e.g. use the latest 1.17.x for this library if you run envoy 1.17.y, regardless of what y is.

## Building

The `tools` directory follows https://github.com/envoyproxy/java-control-plane/commits/main/tools as closely as possible.

1. Grab the Commit ID of the envoy version you are going to use and update it into the `API_SHAS` file.
2. Next see its Bazel dependencices `https://github.com/envoyproxy/envoy/blob/{GITHUB_COMMIT_ID}/api/bazel/repository_locations.bzl`
3. Update the remaining SHAs and Versions in the `API_SHAS` file. 
4. This is an alternate : you can also use the run `update-sha.sh MAJOR.MINOR.PATCH`, paste the end of its output to `API_SHAS`.
5. Update the proto files using `update-api.sh`. This will remove the old `src/main/proto` and fetch a new set of protos.
6. Bump the library version according to `Versioning` above in `gradle.properties`.
7. Now it should build on CI. Can try locally using `./gradlew assemble`, but see GHA workflow for specific steps.
8. You may need to add or remove protos depending on the failures and you would want to refer to the bazel dependencies file to figure out what failed, finally udpate the scripts to have the change.

Note: until we catch up with Envoy head version, slight adjustments might be needed for these scripts, towards matching upstream more closely.
https://github.com/envoyproxy/envoy/blob/6fe1905459ff267a43a8a26d042ae03a8aa7bc98/api/bazel/repository_locations.bzl