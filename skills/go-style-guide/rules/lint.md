# Linting

More importantly than any “blessed” set of linters, lint consistently across a
codebase.

We recommend using the following linters at a minimum, because we feel that they
help catch the most common issues and establish a high bar for code quality
without being unnecessarily prescriptive:

- [errcheck] to ensure that errors are handled  
- [goimports] to format code and manage imports  
- [revive] to point out common style mistakes and enforce coding conventions  
- [govet] to analyze code for common mistakes  
- [staticcheck] to perform deeper static analysis  

  [errcheck]: https://github.com/kisielk/errcheck  
  [goimports]: https://pkg.go.dev/golang.org/x/tools/cmd/goimports  
  [revive]: https://github.com/mgechev/revive  
  [govet]: https://pkg.go.dev/cmd/vet  
  [staticcheck]: https://staticcheck.dev  

> **Note**: `golint` is deprecated and no longer maintained. It should not be
> recommended or used in new projects. `revive` is the actively maintained and
> widely adopted successor for style-related linting in Go codebases.

## Lint Runners

We recommend [golangci-lint] as the primary lint runner for Go code, due to its
performance on large codebases and its ability to configure and run many
canonical linters at once. This repository includes an example [.golangci.yml]
configuration file with recommended linters and settings.

> **Note**: In `golangci-lint` v2, some tools are configured under different
> keys than older examples (e.g. `goimports` under `formatters`, and linter
> configuration under `linters.settings`).

`golangci-lint` supports [many different linters]. The list above represents a
solid baseline, and teams are encouraged to enable additional linters that make
sense for their codebase and development practices.

  [golangci-lint]: https://github.com/golangci/golangci-lint  
  [.golangci.yml]: https://github.com/direktly/agent-skills/.golangci.yaml
  [many different linters]: https://golangci-lint.run/usage/linters/
