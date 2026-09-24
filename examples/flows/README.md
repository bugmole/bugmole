# Flow examples

Flows live in your repository, by default under `spec/flows/`. Run a folder of them against any environment:

```bash
bugmole --mode suite --flows examples/flows --base-url https://staging.example.com --browsers chromium,firefox,webkit
```

The full list of steps is in [Sample tests](https://bugmole.com/docs/sample-tests/).
