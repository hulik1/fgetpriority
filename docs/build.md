# Building fgetpriority

## GitHub Actions

No local Ubuntu or DDK installation is needed.

1. Open the repository's **Actions** tab. If GitHub asks to enable workflows for
   this fork, enable them first.
2. Select **Build fgetpriority (all KMI)**.
3. Click **Run workflow**, select the `lkm` branch, and confirm **Run workflow**.
4. Wait for all eight **Build** jobs and **Package all 8 KMI** to succeed.
5. Download **fgetpriority-all-kmi** from the run's **Artifacts** section.
6. Extract the downloaded artifact. Install the inner
   `fgetpriority_<version>_all-kmi.zip` through KernelSU Manager. The artifact also
   contains `SHA256SUMS` and `BUILD-INFO.txt`.

The workflow also runs automatically when the workflow, `kernel/`, or `module/`
changes on `lkm`. It builds the source commit selected for that run.

Each ARM64 module is compiled in the matching public
[`Ylarod/ddk-min`](https://github.com/Ylarod/ddk) container:

- `android12-5.10`
- `android13-5.10`
- `android13-5.15`
- `android14-5.15`
- `android14-6.1`
- `android15-6.6`
- `android16-6.12`
- `android17-6.18`

The final ZIP is published only when all eight builds succeed and packaging
verifies that all eight nonempty `.ko` files are present. Individual
`fgetpriority-ko-<KMI>` artifacts are retained for seven days for troubleshooting;
the complete installer artifact is retained for 90 days.

The installer uses `uname -r` to select a module from `ko/`. KMI is the Android
kernel branch and major/minor kernel version, not the Android userspace version.
Check it with `adb shell uname -r`. Matching KMI alone does not guarantee
compatibility with every modified or vendor kernel. These are ARM64 builds only.

## Local DDK build

The existing `kernel/build_ddk.sh` remains available. It requires all eight
matching kernel build directories and Clang toolchains under `/opt/ddk`, as
described in the [DDK host setup](https://github.com/Ylarod/ddk#readme).

From the repository root, run:

```sh
cd kernel
bash build_ddk.sh
```

The local script writes `module/fgetpriority_<version>.zip`.
