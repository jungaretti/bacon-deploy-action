# Contribute to Bacon Deploy Action

## Testing

You can use [`nektos/act`](https://github.com/nektos/act) to test this action locally. Follow these steps to test your changes:

1. Install [`nektos/act`](https://github.com/nektos/act)
2. `mkdir -p .github/workflows`
3. `cp action.yml .github/workflows/built-action.yaml`
4. Open `.github/workflows/built-action.yaml`
5. Delete lines `name: "Deploy with Bacon"` up to `steps:`
6. Prepend the following lines
```yaml
name: Bacon Deploy Action (from source)
on:
  push:
jobs:
  built-action:
  runs-on: ubuntu-latest
```
7. Fix indentation
8. Confirm that your file looks like this
```yaml
name: Bacon Deploy Action (from source)
on:
  push:
jobs:
  built-action:
    runs-on: ubuntu-latest
    steps:
      - name: Download Bacon
        id: download-bacon
        shell: bash
        # etc...
```
