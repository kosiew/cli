# AGENTS Instructions

These instructions apply to the entire repository.

## Development workflow

- Format Go code using `make fmt` before committing.
- Run linters with `make lint`. For shell scripts also run `make shellcheck` or use `docker buildx bake lint shellcheck`.
- Run unit tests with `make test` (or `docker buildx bake test`).
- Do not edit files under `vendor/` manually; update dependencies using `make vendor`.
- Use `make help` to discover other build and testing targets.

## Commit rules

- Every commit must be signed off using `git commit -s` (Developer Certificate of Origin).
- Ensure files retain their existing license headers.

