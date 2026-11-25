# lash-hirsel

A durable LLM agent harness written in [Hirsel](https://hirsel.ai), and an example app built on it.

- [harness](harness/README.md): durable agent sessions, tools, approvals and model calls,
  with a development gateway (`harness/serve`) and a TypeScript client (`harness/ts-client`).
- [notes](notes/README.md): an offline notes agent with tools and an approval step.

The repository is one Hirsel workspace (`hirsel.toml`) whose members are `harness`,
`harness/serve`, `harness/ts-client/gateway` and `notes`. Run the commands below from the
repository root.

## The Hirsel toolchain

These packages need an installed Hirsel toolchain. `std`, `store`, `runner`, `platform`,
`search` and `mcp` come from that installation, which ships them as toolchain packages; each
manifest binds them by major alone, for example `store = { major = 1 }`. No other checkout is
needed.

Install a release:

```sh
curl -fsSL https://hirsel.ai/install.sh | sh
```

To use another installation, such as a toolchain you built from the Hirsel repository with
`buck2 build //:hirsel-toolchain`, put its directory first on `PATH`; `hirsel` finds its
packages next to itself. `harness/serve.sh` also accepts the executable in `HIRSEL`:

```sh
export PATH=/path/to/hirsel-toolchain:$PATH
hirsel env          # shows the installed root and package cache in use
```

## Check and test

```sh
hirsel lock .                      # refresh hirsel.lock after changing a manifest
hirsel check harness
hirsel test harness
hirsel laws check harness
```

The same commands take `notes`, `harness/serve` and `harness/ts-client/gateway`.
