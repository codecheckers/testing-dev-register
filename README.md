# testing-dev-register

A testing and development version of the CODECHECK Register to explore machine-to-machine workflows and test apps or new features before they are applied to the main register at <https://codecheck.org.uk/register/>.

## Data for announcing certificates

`persons.csv`, `venues.csv`, `codecheckers.csv` and `institutional-codecheckers.csv` are small copies of the files of the same name in [codecheckers/register](https://github.com/codecheckers/register) and [codecheckers/codecheckers](https://github.com/codecheckers/codecheckers), including the `fediverse` and `hashtags` columns ([register#217](https://github.com/codecheckers/register/issues/217)).
Together with `docs/1970-001/index.json` and `docs/1970-001/cert_1.png` … `cert_5.png` they give the development deployment of `@chekhovbot announce` ([chekhov#23](https://github.com/codecheckers/chekhov/issues/23)) one certificate to compose a toot about, without reading production data.
All people, accounts and identifiers are fake: the accounts are on `example.invalid`, and one author has no ORCID and one no account, so that a preview lists who could not be mentioned.
