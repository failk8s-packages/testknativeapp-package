# testknative-package

This package provides a test application to validate Knative functionality.

## Components

* testknativeapp

## Configuration

The following configuration values can be set to customize the testknativeapp installation.

### Global

| Value | Required/Optional | Description |
|-------|-------------------|-------------|
| `namespace` | Optional | The namespace in which to deploy testknativeapp. |
| `privileged_clusterrole_name` | Optional | If PSPs are enabled on the cluster, this is the name of the privileged clusterrole that allows our test app to start |


## Usage Example

Just delpoy the package and test it. There should be an `ksvc` ready to use in the `namespace` you used. 

## Develop checklist

1. Update your [config.json](./config.json) with the package info
2. Update your [vendir.yml](./src/bundle/vendir.yml) with your upstreams
3. `vendir sync` in `src/bundle` to fetch your new upstream files
4. Add [overlays](./src/bundle/config/overlays/) and [values](./src/bundle/config/values.yaml)
5. Update your [bundle.yml](./src/bundle/.imgpkg/bundle.yml) file
6. Test your bundle: `ytt -f bundle`
7. Lock images used: `kbld -f . --imgpkg-lock-output .imgpkg/images.yml`
8. Publish your bundle: `imgpkg push --bundle quay.io/failk8s/testknativeapp-package:develop --file .`. These steps can be done via [hack/build-package.sh](./hack/build-package.sh)
9. Package up your k8s manifests and test in k8s [hack/package-manifests.sh](./hack/package-manifests.sh). The files will be in `target` folder.
