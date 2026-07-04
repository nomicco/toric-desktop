# toric-desktop

Desktop application for [Toric](https://github.com/nomicco/toric), a
decentralized AI model evaluation and trust network on Holochain.

Built on [Kangaroo-Electron](https://github.com/holochain/kangaroo-electron)
(`main-0.6`, Holochain 0.6.x): bundles the conductor and lair keystore,
installs the Toric webhapp, and serves the UI with a direct zome-call
connection. This repo is a fork of the template so upstream fixes can be
merged; see the upstream README for release workflow, auto-updates,
versioning semantics, and code signing.

## Configuration

All app-level settings live in [`kangaroo.config.ts`](kangaroo.config.ts):
app id, version (semver controls data compatibility — see upstream
versioning notes), and the network endpoints (bootstrap, signal, iroh
relay). Bootstrap and signal are served from a self-hosted
kitsune2-bootstrap-srv instance; plain-`ws://` signal is enabled through the
conductor's kitsune2 `advanced` config in
[`templates/conductor-config.yaml`](templates/conductor-config.yaml).

> Changing network URLs after deployment partitions the network. The
> current endpoints are development infrastructure.

## Development

```bash
yarn setup                                 # fetch verified binaries, write configs
# build the webhapp in the toric repo: npm run package
# then copy workdir/toric.webhapp into pouch/
yarn dev
```

To attach an external client (e.g. the Toric validator) to the bundled
conductor, launch with a fixed admin port: `ADMIN_PORT=44121 yarn dev`.

## Build

```bash
yarn build:linux      # or build:mac-arm64 / build:mac-x64 / build:windows
```

## Syncing with upstream

```bash
git fetch upstream
git merge upstream/main-0.6
```

## License

[CAL-1.0](https://github.com/nomicco/toric/blob/main/LICENSE), matching the
main Toric repository. Template code from Kangaroo-Electron retains its
upstream license.