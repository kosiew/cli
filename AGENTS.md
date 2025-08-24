# AGENTS Instructions

These instructions apply to the entire repository. They are a short, machine-friendly
summary of repository conventions and developer workflows (see `README.md`,
`Makefile`, and `TESTING.md` for full details).

## Development workflow

- Format Go code before committing using:

	make fmt

- Run linters:

	make lint

	For shell scripts also run `make shellcheck` or use `docker buildx bake lint shellcheck`.

- Run unit tests (local):

	make test-unit

	`make test` is an alias to the unit test target.

- Cross-platform and containerized builds:

	docker buildx bake

	Use `make -f docker.Makefile shell` for an interactive in-container development environment.

- Vendor management: do not edit `vendor/` manually; update vendor with:

	make vendor

- Use `make help` to discover other build and testing targets.

## Commit & PR rules

- Every commit must be signed off using `git commit -s` (Developer Certificate of Origin).
- Preserve existing license headers in modified files.
- Commit message style: imperative, short summary (<=72 chars) and an optional explanatory paragraph.

## Testing & conventions (high level)

- Unit tests live beside code in `_test.go` files and use `gotest.tools/assert` for assertions.
- End-to-end tests live under `e2e/` and exercise the built `docker` binary via `gotestyourself/icmd`.
- Table-driven tests are preferred where appropriate; new flags/options that change CLI behavior
	should have their flag exercised in the relevant `e2e/` success-case test.

## Project-specific patterns

- CLI wiring uses cobra; entry points and command wiring live under `cli/` and `cli/command/`.
- Context/config helpers live in `cli/context/` and `cli/command/context.go` — prefer these over ad-hoc globals.
- Error wrapping follows patterns in `cli/error.go`.
- Telemetry/otel code appears under `contrib/otel` and in vendored `go.opentelemetry.io` modules — avoid changing
	telemetry wiring without maintainer approval.

## Small, safe automation rules for agents

- Only modify files under version control; never modify `vendor/` directly.
- Run `make fmt` and `make test-unit` locally before opening a PR and include a short test summary in the PR.
- Keep automated changes narrowly scoped: one logical change per commit and include a DCO sign-off.

## Where to look next

- `Makefile` — canonical dev commands (test, lint, fmt, vendor).
- `README.md` — containerized build instructions and `docker buildx bake` usage.
- `cli/` and `cli/command/` — main implementation and command wiring.
- `e2e/` and `internal/test` — end-to-end tests and test helpers.

If anything above is unclear or you'd like more examples from specific files, tell me which areas to expand.

