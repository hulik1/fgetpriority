## fgetpriority

A small LKM for getpriority hiding.

## How to use?

Just install and forget its existence.

## Build with GitHub Actions

Open **Actions → Build fgetpriority (all KMI) → Run workflow** and select `lkm`.
The workflow builds all eight supported ARM64 KMI variants and packages them in
one installable ZIP.

After the run succeeds, download **fgetpriority-all-kmi** from **Artifacts**,
extract it, and install the inner `fgetpriority_<version>_all-kmi.zip` through
KernelSU Manager.

See [the build guide](docs/build.md) for the supported KMI list, local builds,
and compatibility notes.

## Credits

- [backslashxx](https://github.com/backslashxx) - Initial project owner
- [KodateMitsuru](https://github.com/KodateMitsuru) - LKM installation script and other indirect contributions
