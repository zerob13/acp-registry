# Contributing to the ACP Agent Registry

## Adding a New Agent

1. **Fork this repository**

2. **Create a directory for your agent**

   ```
   mkdir <agent-id>/
   ```

   The directory name should match your agent's `id` field.

3. **Create `agent.json`**

   ```json
   {
     "id": "your-agent-id",
     "name": "Your Agent Name",
     "version": "1.0.0",
     "description": "Brief description of your agent",
     "repository": "https://github.com/your-org/your-repo",
     "authors": ["Your Name <email@example.com>"],
     "license": "MIT",
     "distribution": {
       // At least one distribution method required
     }
   }
   ```

4. **Add an icon** (optional but recommended)

   Place an SVG icon at `<agent-id>/icon.svg`.

   > **Warning**: Icons must be **16x16 SVG**. Larger icons may be scaled down and lose quality. Non-square icons may display incorrectly.

5. **Submit a Pull Request**

   The CI will validate your `agent.json` against the schema.

## Distribution Options

### Binary Distribution

For standalone executables:

```json
{
  "distribution": {
    "binary": {
      "darwin-aarch64": {
        "archive": "https://github.com/.../release.zip",
        "cmd": "./your-binary",
        "args": ["acp"],
        "env": {
          "OPTIONAL_VAR": "value"
        }
      }
    }
  }
}
```

Supported platforms: `darwin-aarch64`, `darwin-x86_64`, `linux-aarch64`, `linux-x86_64`, `windows-aarch64`, `windows-x86_64`

### npm Package (npx/bunx)

```json
{
  "distribution": {
    "npx": {
      "package": "@your-scope/your-package@1.0.0",
      "args": ["--acp"]
    },
    "bunx": {
      "package": "@your-scope/your-package@1.0.0",
      "args": ["--acp"]
    }
  }
}
```

### PyPI Package (uvx)

```json
{
  "distribution": {
    "uvx": {
      "package": "your-package",
      "args": ["serve", "--acp"]
    }
  }
}
```

## Required Fields

| Field | Type | Description |
|-------|------|-------------|
| `id` | string | Unique identifier (lowercase, hyphens allowed) |
| `name` | string | Display name |
| `version` | string | Semantic version |
| `description` | string | Brief description |
| `distribution` | object | At least one distribution method |

## Optional Fields

| Field | Type | Description |
|-------|------|-------------|
| `repository` | string | Source code URL |
| `authors` | array | List of author names/emails |
| `license` | string | SPDX license identifier |

## Updating an Existing Agent

To update your agent's version or distribution URLs:

1. Fork and update `<agent-id>/agent.json`
2. Submit a Pull Request
3. CI will validate and merge will trigger a new registry release

## Validation

All submissions are validated against the [JSON Schema](agent.schema.json). Run locally:

```bash
python .github/workflows/build_registry.py
```
