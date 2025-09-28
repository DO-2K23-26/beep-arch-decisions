# Tracing

I suggest using [linkerd.io](https://linkerd.io/) for tracing in our Kubernetes environment. Linkerd is a lightweight and easy-to-use service mesh that provides robust observability features, including distributed tracing.

## Poc

You can find a POC here that leverages Linkerd wonderful documentation to set up a mesh with mTls and distributed tracing using Jaeger as a backend: [poc-linkerd](https://github.com/hugoponthieu/poc-linker)