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

Each is a copy of `testdata/valid-2.0/` from the bot's own repository with one
line changed, and carries the files its manifest names, so the only findings
are the ones the bundle is named for.

Point at one with the sub-directory form of a repository target:

```
@chekhovbot check github::codecheckers/testing-dev-register|testdata/future-spec
```
