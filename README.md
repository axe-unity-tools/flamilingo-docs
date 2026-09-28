# Flamilingo documentation

Source for the Flamilingo user documentation, published with GitHub Pages at
<https://axe-unity-tools.github.io/flamilingo-docs/>.

## Preview locally

```sh
python -m venv .venv
python -m pip install -r requirements.txt
mkdocs serve
```

Run `mkdocs build --strict` before publishing. The `main` branch deploys through
`.github/workflows/deploy.yml` after GitHub Pages is configured to use **GitHub Actions**.

The product source lives in the separate `Asset-Store-Plugins` repository. Update
examples here when its public API or editor workflows change.
