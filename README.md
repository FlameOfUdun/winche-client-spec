# Winche client spec

The contract every Winche client SDK follows: versioned protocol documents and language-neutral test cases for
Database, Storage, Auth and Functions.

An SDK, in any language, proves it follows the spec by running the cases in `cases/`. The Winche servers run the same
cases, so the clients and the server agree on how values sort, which documents a query matches, and which error a
caller gets.

Nothing is written yet. See [PLAN.md](PLAN.md).

## Layout (planned)

| Folder | What it holds |
| --- | --- |
| `spec/core/` | The parts every product shares: values, paths, errors, sessions and tokens |
| `spec/database/`, `spec/storage/`, `spec/auth/`, `spec/functions/` | One protocol document per product |
| `cases/<product>/` | JSON test cases: an input, the expected output, and the spec section it tests |
| `schema/` | The JSON Schema every case file must match |

## Versions

The repo has one version for all products, released with a `v<version>` tag. Each SDK pins one version, so a spec
change can't break an SDK until the SDK moves to it. The changelog says which products each change affects.

## License

MIT
