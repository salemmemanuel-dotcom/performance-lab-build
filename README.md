# Private app build automation

This public repository contains only the build procedure. Application sources remain in their existing private repository.

## Privacy boundaries

- Manual dispatch only, restricted to the repository owner and main branch.
- Reads one explicitly selected, immutable private source commit with a dedicated read-only deploy key.
- Verifies the selected source archive against its approved SHA256 before extraction.
- Does not publish source code, app packages, private build logs, caches or signing material as GitHub artifacts.
- Build and submission output stays on the temporary hosted Mac and is discarded with that runner.
- Existing app signing is accessed through a dedicated Expo secret; no credential is committed here.
- Sends the signed app directly to Apple through EAS Submit. Apple processing remains a separate phase.
- Uses a standard GitHub-hosted Mac. Standard hosted runner execution in public repositories is free under GitHub's current billing rules; availability and service limits still apply.

## Setup required before use

Repository secrets:

- `APP_SOURCE_READ_KEY`: dedicated SSH deploy key, read-only and limited to the private source repository.
- `EXPO_TOKEN`: dedicated Expo access token for signing and submitting the app.

These credentials must be authorized before registration. Until both secrets exist, the workflow exits before accessing sources or building.

For each future release, explicitly supply the source commit, archive name, archive SHA256, expected app version and an unused Apple build number of at least 32. Do not dispatch an unapproved release.

No change to the application itself is made by configuring this repository. No builds are scheduled automatically.
