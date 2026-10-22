# Bundles for live-testing the bot

These are not checks. They are small, self-consistent CODECHECK bundles that
the bot is pointed at from a live test issue, in the one case where a fixture
on somebody's disk will not do: the deployment never reads its own disk, so a
`codecheck.yml` it should answer in a particular way has to live in a
repository.

| Bundle | What it is for |
|---|---|
| `future-spec/` | declares specification version 9.9, which no build knows, so `check` refuses it instead of reporting against a guess (codecheckers/chekhov#7) |
| `no-version/` | declares no version at all, so `check` assumes one and says which - the refusal above must not fire here |
| `mistyped-orcid/` | gives the paper's author an ORCID with a wrong check digit, so `check metadata` reports it once, as a likely typo under `CC-MET-001`, and does not look it up under `CC-MET-002` (codecheckers/chekhov#9) |
| `register-row/` | carries certificate `1970-021`, the next after the last row, an identifier not in `register.csv`, so `check register` builds and judges a row for it before the row exists (codecheckers/chekhov#21) |
| `yaml-directive/` | starts with `%YAML 1.2` and a comment before `---`, and a comment after it, all of which `CC-CFG-002` allows, so the file is read and passes (codecheckers/chekhov#62) |
| `no-output-files/` | has a manifest of a single item with only a comment, which declares a check without output files, so `CC-CFG-005` passes and `CC-BUN-001` has nothing to look for (codecheckers/chekhov#62) |
| `placeholder-report/` | gives the report as `zenodo.example`, which `CC-CFG-013` and `CC-CFG-023` report as a placeholder (codecheckers/chekhov#62) |
| `future-certificate/` | carries certificate `2099-001`, in a year that has not started, which `CC-REG-002` fails (codecheckers/chekhov#62) |
| `dotcodecheck-no-pdf/` | keeps its certificate directory as `.codecheck/` with no PDF in it, so `CC-BUN-003` names that directory (codecheckers/chekhov#62) |
| `no-licence/` | has no `LICENSE`, so `CC-BUN-005` names the files it looked for (codecheckers/chekhov#62) |
| `unfilled-template/` | leaves the template's `FIXME` in the paper reference, a further reference, the repository and the report, which `CC-CFG-023` reports and the rules that resolve links do not ask for; and a title naming Todorov and mastodon, which is not a placeholder (codecheckers/chekhov#62) |

Each is a copy of `testdata/valid-2.0/` from the bot's own repository with one
line changed, and carries the files its manifest names, so the only findings
are the ones the bundle is named for.

Point at one with the sub-directory form of a repository target:

```
@chekhovbot check github::codecheckers/testing-dev-register|testdata/future-spec
```
