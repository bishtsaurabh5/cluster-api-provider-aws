# Release process

## Semi-automatic

1. make the release artifacts `make release-artifacts`
2. Run the release tool found in `cmd/release`
3. Pick up the manual steps starting with step 6

## Manual

1. Create a draft release in github
2. Tag the repository and push the tag `git tag -s $VERSION `
3. Run `make release-artifacts`
4. Attach the tarball to the drafted release
5. Attach `clusterawsadm` and `clusterctl` to the drafted release (for darwin
   and linux architectures)
6. Write the release notes (see note below on release notes)
7. Get someone with permission to copy the container image from your own
   personal gcr registry to the production one, or have them build and push the
   container image themselves.
8. Publish release
9. Email `kubernetes-dev@googlegroups.com` to announce the release

## Expected artifacts

1. A container image containing the aws-provider manager binary
2. A release tarball containing the manifest-templates and a script to generate
   the actual manifests
3. `clusterctl`
4. `clusterawsadm`
5. Release notes
6. Email to `kubernetes-dev@googlegroups.com` announcing the release

## Output locations

### Container image

The container image will live in the registry `gcr.io/cluster-api-provider-aws`
under the image name `cluster-api-aws-controller:<tag>` where `<tag>` is
replaced by the version being released.

### Manifests

Manifests must be generated by hand.

Running `make release-artifacts` will create a tarball that you can attach to
the drafted release.

### Binaries

The two binaries produced by a release are the `clusterctl` binary and the
`clusterawsadm` binary. There should be support for both darwin and linux architectures.

### Release Notes

Release notes are written by hand. Generally we'll make a [hackmd](hackmd.io)
and share the release note responsibility for a few days in advance of the
release.

The markdown is shared in the kubernetes slack in the channel #cluster-api-aws.