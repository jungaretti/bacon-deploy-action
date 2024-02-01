# Bacon Deploy Action

Deploy DNS records with [Bacon](https://github.com/jungaretti/bacon) and GitHub Actions.

## Usage

Sign into Porkbun's website and [generate a new API keyset](https://porkbun.com/account/api) for your account. Read the ["Generating API Keys" section of Porkbun's docs](https://kb.porkbun.com/article/190-getting-started-with-the-porkbun-dns-api) for more detailed instructions.

[Create encrypted repository secrets to store your Porkbun API keys](https://docs.github.com/en/actions/security-guides/encrypted-secrets#creating-encrypted-secrets-for-a-repository) and pass them to this action using `${{ secrets.YOUR_SECRET_NAME }}`.

### Example

```yaml
on:
  push:
    branches:
      - main

jobs:
  deploy:
    name: Deploy DNS Records
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: jungaretti/bacon-deploy-action@v1
        with:
          api-key: ${{ secrets.PORKBUN_API_KEY }}
          secret-key: ${{ secrets.PORKBUN_SECRET_KEY }}
          config: example-com.yml
          create: true
          delete: true
```

See [`jungaretti/dns`](https://github.com/jungaretti/dns/tree/main/.github/workflows) for a more detailed example.

## Inputs

#### `api-key`

Your Porkbun API key. This input is required.

#### `secret-key`

Your Porkbun API secret key. This input is required.

#### `config`

Bacon config file to deploy. This input is required.

#### `create`

Flag to disable dry-run creations and create new records. The default value is `false`.

#### `delete`

Flag to disable dry-run deletions and delete outdated records. The default value is `false`.

#### `version`

The version of Bacon to download and use. The default value is `latest`. To use a specific release of Bacon, choose from the releases on [`jungaretti/bacon`](https://github.com/jungaretti/bacon/releases) and use the full tag name (e.g. `v1.2`) as the value for this input.
