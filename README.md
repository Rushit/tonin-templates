# tonin-templates

Service scaffolding templates for the [tonin](https://github.com/Rushit/tonin) microservice framework.

## Directory Structure

```
├── service/              # Service scaffolds
│   ├── rust/            # Rust backend service
│   │   ├── server/
│   │   ├── client-rust/
│   │   └── ...
│   ├── python/          # Python backend service
│   │   ├── server/
│   │   ├── client-python/
│   │   └── ...
│   └── ts/              # TypeScript services
│       ├── backend/
│       ├── client-ts/
│       ├── web-spa/
│       └── web-bff/
├── k8s/                 # Kubernetes manifests templates
├── Dockerfile.tmpl      # Container image template
└── version.toml         # Version metadata
```

## Usage with tonin CLI

The tonin CLI automatically downloads these templates when scaffolding a new service:

```bash
tonin service new myapp --lang rust
```

### Custom Template Location

Use a local copy:
```bash
tonin service new myapp --lang rust --template-dir /path/to/templates
```

Or custom GitHub repo:
```bash
tonin service new myapp --lang rust --template-url https://github.com/myorg/templates
```

## Contributing

To add or update templates:

1. Edit files in the relevant subdirectory
2. Update `version.toml` with a new version
3. Create a git tag matching the version: `git tag v0.4.0`
4. Push to trigger release workflow

## License

Apache-2.0 (same as tonin)
