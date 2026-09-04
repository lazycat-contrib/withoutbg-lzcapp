# WithoutBG for LazyCat

LazyCat LPK v2 packaging for [WithoutBG](https://withoutbg.com), a background-removal API and self-hosted model.

## Runtime

- Runs the CPU open-weights v3 service on port 8000.
- Uses the `docker.1ms.run` mirror and pins the selected linux/amd64 source digest in the Manifest.
- The API remains behind LazyCat authentication rather than exposing an unauthenticated compute endpoint.
- No persistent volume is required by the upstream image.

The supplied logo is preserved as a 512×512 PNG.

The LazyCat store already contains `cloud.lazycat.app.withoutbg`. This repository intentionally uses the distinct package ID `community.lazycat.app.withoutbg` as explicitly requested.

## Digest-based updates

The upstream image publishes only a mutable `latest` tag. GitHub Actions compares its linux/amd64 digest with the trusted digest baseline stored in the Manifest. An unchanged digest is a no-op; a changed digest increments only the package patch version, verifies the mirror content, creates a versioned Release asset, and publishes it to the MiaoMiao private store.

## Build

```sh
lzc-cli project release -o dist/application.lpk
```

## GitHub Actions

Required repository or organization Secrets:

- `APPSTORE_URL`
- `APPSTORE_TOKEN`

Optional Secrets:

- `APP_ID`
- `PRIVATE_STORE_GROUP_CODES`
