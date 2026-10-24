# winget-fixtures

Test fixtures for Attestree's installer testing. They're published as winget manifests so the
platform can read them the way it reads winget-pkgs. Nothing here is meant for anyone's real use.

## Attestree.Fixtures.BlockingBundle

A WiX bundle around one ordinary MSI:

- **The bundle waits at a window**, even when it is run with `/quiet`. Its installer UI ignores the
  silent switch on purpose. Clicking Close ends the run with exit code 1602, and the bundle itself
  installs nothing.
- **The MSI inside installs silently.** It puts one text file under
  `C:\Program Files\Attestree Fixtures Blocking Bundle` and shows up in Apps & features, where it
  can be removed.

It tests one path: when a bundle can't be installed unattended, Attestree can take the MSI out of
the bundle and install that instead.

| Version | Release asset | SHA-256 |
| --- | --- | --- |
| 1.0.0 | `Attestree.Fixtures.BlockingBundle-1.0.0-x64.exe` | `F4FC334317B551BC559ECBE3B365072972F644FCE39B255DDB81C41BD413F589` |

Manifests are under `manifests/`, in the same layout as winget-pkgs. The binaries are unsigned.

These fixtures are not in winget-pkgs and won't be submitted there.
