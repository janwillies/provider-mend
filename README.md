# provider-mend

`provider-mend` is a minimal [Crossplane](https://crossplane.io/) Provider
that is meant to be used as a mend for implementing new Providers. It comes
with the following features that are meant to be refactored:

- A `ProviderConfig` type that only points to a credentials `Secret`.
- A `MyType` resource type that serves as an example managed resource.
- A managed resource controller that reconciles `MyType` objects and simply
  prints their configuration in its `Observe` method.


# Setup

```bash
kubectl --namespace crossplane-system create secret generic provider-mend --from-literal=orgToken=123 --from-literal=userToken=456
kubectl apply -f examples/provider/config.yaml
```

## Developing

1. Use this repository as a mend to create a new one.
1. Find-and-replace `provider-mend` with your provider's name.
1. Run `make` to initialize the "build" Make submodule we use for CI/CD.
1. Run `make reviewable` to run code generation, linters, and tests.
1. Replace `MyType` with your own managed resource implementation(s).

Refer to Crossplane's [CONTRIBUTING.md] file for more information on how the
Crossplane community prefers to work. The [Provider Development][provider-dev]
guide may also be of use.

[CONTRIBUTING.md]: https://github.com/crossplane/crossplane/blob/master/CONTRIBUTING.md
[provider-dev]: https://github.com/crossplane/crossplane/blob/master/docs/contributing/provider_development_guide.md