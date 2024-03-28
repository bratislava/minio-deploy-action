# Minio Deploy GitHub Action


### Our fork of this repo is using prebuild image instead of building an image every time when pipeline runs.


Run [minio client][] in GitHub Actions to deploy files to Minio object storage.

It uses the `mc mirror --overwrite` command to deploy.

## Usage

Put the following step in your workflow:

```yml
- name: Minio Deploy
uses: hkdobrev/minio-deploy-action@v1
with:
  endpoint: ${{ secrets.MINIO_ENDPOINT }}
  access_key: ${{ secrets.MINIO_ACCESS_KEY }}
  secret_key: ${{ secrets.MINIO_SECRET_KEY }}
  bucket: 'mybucket'
  # Optional inputs with their defaults:
  source_dir: 'public'
  target_dir: '/'
```

Workflow example:

```yml
name: Deploy

on:
  pull_request:
    types: [opened, synchronize]
  push:
    branches:
      - master

jobs:
  build:
    name: Deploy
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v1

      - name: Minio Deploy
        uses: hkdobrev/minio-deploy-action@v1
        with:
          endpoint: ${{ secrets.MINIO_ENDPOINT }}
          access_key: ${{ secrets.MINIO_ACCESS_KEY }}
          secret_key: ${{ secrets.MINIO_SECRET_KEY }}
          bucket: 'mybucket'
          source_dir 'public'
          target_dir: '/'
```

## License

Licensed under the MIT license. See [LICENSE](LICENSE).

[minio client]: https://docs.min.io/docs/minio-client-quickstart-guide
