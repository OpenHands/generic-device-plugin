# OpenHands fork

Fork of [squat/generic-device-plugin](https://github.com/squat/generic-device-plugin) (Apache-2.0). OpenHands deploys it through the `device-plugin` subchart of the OpenHands Helm chart to expose `/dev/fuse` and `/dev/kvm` to sandbox pods.

Upstream's last image (`2cc50b0`, 2026-05-15) carries fixable critical/high CVEs in Go, `grpc`, `golang.org/x/net` and `golang.org/x/text`. This fork changes only:

- `go.mod`, `go.sum`, `vendor/`: dependency versions with those fixes.
- `Dockerfile.openhands`: builds with a pinned Go toolchain (upstream's Nix build takes Go from nixpkgs, which can trail Go security releases) and ships `LICENSE` plus dependency NOTICE files under `/licenses`.
- `.github/workflows/openhands-image.yml`: scans and publishes `ghcr.io/openhands/generic-device-plugin`.
- `.github/workflows/ci.yml`: upstream's image push job runs only in the upstream repository.

To pick up a new Go security release, bump the `golang:` tag in `Dockerfile.openhands`. To sync with upstream, use **Sync fork** on GitHub or merge `squat/main`. Dependency bumps are also proposed upstream; once upstream publishes a clean image, OpenHands can return to it.
