# Bacon Deploy Action

Deploy DNS records easily with Bacon.

## Getting Started

```yaml
jobs:
  deploy:
    name: Deploy DNS Records
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v3
      - uses: jungaretti/bacon-deploy-action@main
        with:
          api-key: ${{ secrets.PORKBUN_API_KEY }}
          secret-key: ${{ secrets.PORKBUN_SECRET_KEY }}
          config: config.example.yml
          create: true
          delete: true
```
