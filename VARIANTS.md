# Template Variants

The `tonin` CLI supports multiple service scaffolding templates to match your use case.

## Available Variants

### `default` (Recommended)
The full-featured scaffold with everything you need for production Kubernetes.

**Includes:**
- gRPC service with proto definitions
- Dockerfile for containerization
- Kubernetes manifests (Deployment, Service, HPA, Ingress)
- Build system (Makefile, nextest, CI/CD)
- Auth, telemetry, and MCP wiring
- Database and cache support

**Use when:**
- Building microservices for Kubernetes
- Want all framework features out of the box
- Need production-ready scaffolding

```bash
tonin service new myapp --lang rust
# or explicitly:
tonin service new myapp --lang rust --variant default
```

---

### `flat`
Minimal scaffold focused on the service logic itself.

**Includes:**
- gRPC service with proto definitions
- Main service code and handler
- Makefile for build/test

**Excludes:**
- Kubernetes manifests
- Docker configuration
- Extensive framework wiring

**Use when:**
- Want to add tonin incrementally
- Starting simple and building complexity
- Just need a gRPC endpoint quickly
- Plan to hand-craft k8s manifests later

```bash
tonin service new myapp --lang rust --variant flat
```

---

### `workspace`
Monorepo scaffold with shared proto definitions and multiple services.

**Structure:**
```
monorepo/
├── shared/
│   └── proto/           # Shared message definitions
├── services/
│   ├── auth/
│   ├── api/
│   └── worker/
└── Cargo.workspace.toml # or equivalent
```

**Includes:**
- Workspace configuration
- Shared proto library
- Multiple service templates
- Unified k8s deployment
- CI/CD for monorepo

**Use when:**
- Building a microservice ecosystem
- Multiple services with shared types
- Need coordinated deployments
- Want DRY proto definitions

```bash
tonin workspace new mycompany --lang rust
```

---

## Migrating Between Variants

You can start with `flat` and grow into `default`:

1. Start with `flat`
2. Run `tonin k8s generate` from an existing `flat` service to add manifests
3. Add missing configuration sections to `tonin.toml`

Or go the other way:

1. Start with `default`
2. Ignore `k8s/` directory if you don't deploy to Kubernetes yet
3. Add k8s later when you're ready

---

## Language Support

All variants support:
- **Rust** - Full framework integration
- **Python** - gRPC + telemetry via tonin libraries
- **TypeScript** - Backend and frontend (web) services

Not all variants have all languages — for unsupported combos, the CLI will error helpfully.

```bash
tonin service new myapp --lang python --variant flat
tonin service new frontend --lang ts --variant flat
```
