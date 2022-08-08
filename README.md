# Bacon Deploy Action

Deploy DNS records with [Bacon](https://github.com/jungaretti/bacon) and GitHub Actions.

## Usage

Sign into Porkbun's website and [generate a new API keyset](https://porkbun.com/account/api) for your account. Read the ["Generating API Keys" section of Porkbun's docs](https://kb.porkbun.com/article/190-getting-started-with-the-porkbun-dns-api) for more detailed instructions.

[Create encrypted repository secrets to store your Porkbun API keys](https://docs.github.com/en/actions/security-guides/encrypted-secrets#creating-encrypted-secrets-for-a-repository) and pass them to this action using `${{ secrets.YOUR_SECRET_NAME }}`.

### Basic Example

```yaml
# .github/workflows/bacon-deploy.yaml

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
      - uses: jungaretti/bacon-deploy-action@v1.0
        with:
          api-key: ${{ secrets.PORKBUN_API_KEY }}
          secret-key: ${{ secrets.PORKBUN_SECRET_KEY }}
          config: example-com.yml
          create: true
          delete: true
```

### Parameters

| Parameter  | Required/Optional | Description                                                     |
| ---------- | ----------------- | --------------------------------------------------------------- |
| api-key    | Required          | Your Porkbun API key                                            |
| secret-key | Required          | Your Porkbun API secret key                                     |
| config     | Required          | YAML config file for your DNS records                           |
| create     | Optional          | Flag to create new DNS records. Uses `false` by default.        |
| delete     | Optional          | Flag to delete outdated DNS records. Uses `false` by default.   |
| version    | Optional          | Version of Bacon to download and use. Uses `latest` by default. |
