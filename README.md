# ACP Agent Registry

A registry of agents implementing the [Agent Client Protocol (ACP)](https://github.com/anthropics/agent-client-protocol).

## Usage

Fetch the registry index:

```
https://github.com/<org>/<repo>/releases/latest/download/registry.json
```

Fetch agent icons:

```
https://github.com/<org>/<repo>/releases/latest/download/<agent-id>.svg
```

## Registry Format

```json
{
  "version": "1.0.0",
  "agents": [
    {
      "id": "agent-id",
      "name": "Agent Name",
      "version": "1.0.0",
      "description": "Agent description",
      "repository": "https://github.com/...",
      "authors": ["Author Name"],
      "license": "MIT",
      "icon": "https://.../agent-id.svg",
      "distribution": {
        "binary": {
          "darwin-aarch64": {
            "archive": "https://...",
            "cmd": "./agent",
            "args": ["serve"],
            "env": {}
          }
        },
        "npx": {
          "package": "@scope/package",
          "args": ["--acp"]
        },
        "bunx": {
          "package": "@scope/package",
          "args": ["--acp"]
        },
        "uvx": {
          "package": "package-name",
          "args": ["serve"]
        }
      }
    }
  ]
}
```

## Distribution Types

| Type | Description | Command |
|------|-------------|---------|
| `binary` | Platform-specific executables | Download, extract, run |
| `npx` | npm packages | `npx <package> [args]` |
| `bunx` | npm packages via Bun | `bunx <package> [args]` |
| `uvx` | PyPI packages via uv | `uvx <package> [args]` |

## Icons

Icons should be SVG format with a **preferred size of 16x16**.

> **Warning**: Icons larger than 16x16 may be scaled down and lose quality. Icons with non-square aspect ratios may display incorrectly in some clients.

## Platform Targets

For binary distribution, use these platform identifiers:

- `darwin-aarch64` - macOS Apple Silicon
- `darwin-x86_64` - macOS Intel
- `linux-aarch64` - Linux ARM64
- `linux-x86_64` - Linux x86_64
- `windows-aarch64` - Windows ARM64
- `windows-x86_64` - Windows x86_64

## Adding an Agent

See [CONTRIBUTING.md](CONTRIBUTING.md) for instructions on submitting a new agent.

## License

This registry is open source. Individual agents are subject to their own licenses.
