# Endpoints

The Hex API has two endpoints: an HTTP API, which is used for all administrative tasks and to browse packages; and a repository, which is read-only and used to deliver the registry and package tarballs.

## HTTP API

See [apiary.apib](https://github.com/hexpm/specifications/blob/master/apiary.apib) file at the root of this repository.

## Repository

  * `/[@NAMESPACE/]names` - [Registry v2](https://github.com/hexpm/specifications/blob/master/registry-v2.md)
  * `/[@NAMESPACE/]versions` - [Registry v2](https://github.com/hexpm/specifications/blob/master/registry-v2.md)
  * `/[@NAMESPACE/]packages/PACKAGE` - [Registry v2](https://github.com/hexpm/specifications/blob/master/registry-v2.md)
  * `/tarballs/[@NAMESPACE/]PACKAGE-VERSION.tar` - [Package tarball](https://github.com/hexpm/specifications/blob/master/package_tarball.md)
  * `/registry.ets.gz` - [Registry v1](https://github.com/hexpm/specifications/blob/master/registry-v1.md) (DEPRECATED!)
  * `/registry.ets.gz.signed` - (optional) (DEPRECATED!)

### Registry authentication

The repository can require authentication for some resources. Token authentication with the `Authorization` header as described in the HTTP API should be used. Care needs to be taken by clients to *only* send the token to the actual repository, when unofficial mirrors are used authentication must be disabled.

### Registry v1 signing

A repository can optionally RSA sign its registry. The RSA public key should be provided to clients out-of-band of the registry fetching, for example by shipping the client with a public key or by users manually installing it. The repository signs the SHA-512 digest of the registry and base 16 encodes it with lower case characters. The repository should store the signature on the `/registry.ets.gz.signed` and update it when the registry is updated. For performance reasons the signature can also be provided in either the `x-hex-signature` or the `x-amz-meta-signature` header on the `/registry.ets.gz` endpoint.

### Registry v2 signing

The signing is defined in the registry v2 specification as it is not part of the resource delivery.

## Hex.pm endpoints

Hex.pm uses the following root endpoints:

  * HTTP API - https://hex.pm/api
  * Repository - https://repo.hex.pm
  * Repository - https://hexpmrepo.global.ssl.fastly.net (DEPRECATED!)
  * Repository - https://s3.amazonaws.com/s3.hex.pm (DEPRECATED!)
