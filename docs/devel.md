# Development environment for `dex-operator`

## Project structure

This project follows the conventions presented in the [standard Golang
project](https://github.com/golang-standards/project-layout).

## Dependencies

* `go >= 1.11`

### Bumping the Kubernetes version used by `dex-operator`

Update the constraints in [`go.mod`](../go.mod).

## Building

A simple `make` should be enough. This should compile [the main
function](../cmd/dex-operator/main.go) and generate a `dex-operator` binary as
well as a _Docker_ image.

## Running tests

### Unit tests

Unit tests can be run using `make test`

### Integration tests

Integration tests can be run using `make integration`


### Code Coverage:

Run first the tests.

Then you can visualize the profile in html format:

`go tool cover -html=cover.out`

or use the `make coverage` target

Feel free to read more about this on : https://blog.golang.org/cover.

### Regenerating CRDs, RBAC and the deployment all-in-one manifest

Some files are autogenerated when you run the integration tests, like the `CRD` generation
under (`config/crds`) or the `RBAC` generation under (`config/rbac`). Also, our all-in-one
manifest can be generated by running `make manifests`.

* `make integration`
  * Will automatically regenerate files under `config{crds,rbac}`

* `make manifests`
  * Will take some files from `config{crds,rbac}` and will generate the all-in-one manifest
    under `deployments/dex-operator-full.yaml`

## Running `dex-operator` in your Development Environment

There are multiple ways you can run the `dex-operator` for bootstrapping
and managinig your Kubernetes cluster:

### ... in your local machine

You can run the `dex-operator` container locally with a
`make local-run`. This will:

  * build the `dex-operator` image
  * run it locally
    * using the `kubeconfig` in `/etc/kubernetes/admin.conf`
    * using the config files in [`../config`](`../config`)
