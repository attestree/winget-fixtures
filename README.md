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

## Attestree.Fixtures.InstallerShapes.*

One small exe that draws the installer window its install switches name, and thirteen packages that
use it, each with its own switches. They test how Attestree tells an installer that waits for a
click from one that is still working, one that has frozen, and one that only shows a message.

| Package | What it shows |
| --- | --- |
| `Wizard` | A setup wizard page whose Next button is enabled. It waits there. |
| `Agree` | A licence page whose I Agree button is enabled. It waits there. |
| `Licence` | A licence page with Next disabled until "I accept" is ticked. It waits there. |
| `NoisyWizard` | The wizard page, writing 8 KiB every 20 seconds while it waits. |
| `BusyWizard` | The wizard page, writing 512 KiB every second. It installs after 3 minutes. |
| `Progress` | An install page whose progress bar moves for 3 minutes. Then it installs. |
| `Frozen` | An install page whose progress bar never moves. |
| `SlowWriter` | A still progress bar, writing 6 KiB every 2 minutes. It installs after 11 minutes. |
| `Hung` | An install page that stops responding. |
| `Alert` | An OK-only message box captioned "Setup". It waits there. |
| `ErrorBox` | An OK-only message box captioned "Setup Error". Answered, it exits with 1603. |
| `Relaunch` | Starts a copy of itself that shows the wizard page, and exits after 5 seconds. |
| `Orphan` | Starts its install page through a process that exits 2 seconds later. It installs after 11 minutes. |

A package that installs puts a readme and an uninstaller under
`C:\Program Files\Attestree Fixtures\Installer Shapes\<Shape>` and shows up in Apps & features, where
it can be removed. Clicking any button in a window ends the run with exit code 1602 and installs
nothing.

| Version | Release asset | SHA-256 |
| --- | --- | --- |
| 1.0.0 | `Attestree.Fixtures.InstallerShapes-1.0.0-x64.exe` | `AE3CC5EC687C6D86F5C9147783E67FB4A666A52F31B612B88D1E2DC593FE5DB4` |

Manifests are under `manifests/`, in the same layout as winget-pkgs. The binaries are unsigned.

These fixtures are not in winget-pkgs and won't be submitted there.
