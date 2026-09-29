# Contributing to Bursar

Thank you for helping. This guide applies to every bursar-world repository that has no
`CONTRIBUTING.md` of its own. The [bursar repository](https://github.com/bursar-world/bursar/blob/main/CONTRIBUTING.md)
has a detailed guide covering its build, tests and coding standards; read that one before working
there.

## Before you start

- For a bug, open an issue with the bug form and include what you ran, what you expected and what
  happened.
- For anything larger than a small fix, open an issue or a discussion first so we can agree the
  approach before you write the code.
- Security problems never go in issues or pull requests. Follow [SECURITY.md](SECURITY.md).

## Making a change

1. Fork the repository and branch from `main`.
2. Keep the change focused on one thing. Unrelated fixes belong in their own pull request.
3. Add or update tests with the behaviour they cover, and make sure the repository's checks pass
   locally.
4. Update the documentation that describes what you changed.
5. Open a pull request against `main` and fill in the template.

Commit subjects are short, lowercase and in the imperative mood, without a trailing period, for
example `show the approval threshold on the mandate page`. Add a body when the reason is not
obvious from the subject.

## Sign-off

Every commit must carry a Developer Certificate of Origin sign-off (`git commit -s`), confirming
that you wrote the change or otherwise have the right to submit it under the repository's license.
See [developercertificate.org](https://developercertificate.org).

## Never commit secrets

No private keys, seed phrases, keystore passwords, API keys or database URLs with credentials in
code, tests, fixtures or history. Every public repository has secret scanning with push
protection, which will stop most of these, but it cannot catch everything.

## Review

A maintainer reviews every pull request. Checks must pass before a change merges. We may ask for
changes, and we may close a pull request that does not fit the project's direction, with a reason.

## Conduct

Everyone taking part is expected to follow the [Code of Conduct](CODE_OF_CONDUCT.md).
