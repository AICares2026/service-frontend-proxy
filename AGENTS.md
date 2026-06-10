## Stack
Envoy reverse proxy (config-driven, no application language). Docker for containerisation. No application framework or package manager detected.

## Constraints
Never modify: any credential or secret files (`*.key`, `*.pem`, `*.crt`, `*.env`, `.env*`). Never modify lock files. Never modify generated or compiled artefacts. Never delete or rewrite the base proxy config in a way that changes upstream routing semantics without explicit instruction.

## Conventions
The primary configuration file is `envoy.tmpl.yaml` at the repo root (environment variables are substituted at container startup via `envsubst`). Dockerfile is the primary build artefact. Config lint fixes must preserve all `clusters`, `listeners`, and `routes` logic exactly; only style/syntax issues may be corrected. Docker hardening must follow CIS Docker Benchmark: non-root user, minimal base image, no `latest` tag, read-only filesystem where possible, drop all capabilities.

## Dependency manifests
`Dockerfile` — base image and version are declared here; this is the only dependency manifest. When updating the base image, pin to a specific digest or version tag, never `latest`.
