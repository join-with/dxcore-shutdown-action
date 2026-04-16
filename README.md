# DxCore Shutdown Action

Gracefully shut down the DxCore coordinator.

## Inputs

| Input             | Description                                              | Required | Default  |
|-------------------|----------------------------------------------------------|----------|----------|
| `coordinator-url` | URL of the running DxCore coordinator                    | Yes      |          |
| `token`           | Authentication token matching the coordinator            | Yes      |          |
| `version`         | Release tag to download (e.g. `v0.1.0`). Defaults to latest. | No  | `latest` |

## Usage

```yaml
jobs:
  shutdown:
    runs-on: ubuntu-latest
    if: always()
    needs: [coordinator, agent, dispatch]
    steps:
      - uses: join-with/dxcore-shutdown-action@main
        with:
          coordinator-url: http://<coordinator-host>:4000
          token: ${{ secrets.DXCORE_TOKEN }}
```

## How It Works

1. Resolves the release version (latest or pinned)
2. Downloads the CLI binary from [`join-with/dxcore`](https://github.com/join-with/dxcore) releases
3. Sends a shutdown command to the coordinator

## Related

- [join-with/dxcore](https://github.com/join-with/dxcore) -- Main DxCore repository
- [join-with/dxcore-coordinator-action](https://github.com/join-with/dxcore-coordinator-action) -- Start coordinator
- [join-with/dxcore-agent-action](https://github.com/join-with/dxcore-agent-action) -- Connect build agents
- [join-with/dxcore-dispatch-action](https://github.com/join-with/dxcore-dispatch-action) -- Dispatch task graphs

## Disclaimer

DxCore is an independent project by Eyal Lapid ([JoinWith])(https://joinwith.com) and is not affiliated with, endorsed by, or sponsored by Vercel, Nrwl, Gradle, Docker, GitHub, or any other third-party project. All trademarks belong to their respective owners.
