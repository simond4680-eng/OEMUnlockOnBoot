# OEMUnlockOnBoot

[![latest release badge](https://img.shields.io/github/v/release/chenxiaolong/OEMUnlockOnBoot?sort=semver)](https://github.com/chenxiaolong/OEMUnlockOnBoot/releases/latest)
[![license badge](https://img.shields.io/github/license/chenxiaolong/OEMUnlockOnBoot)](./LICENSE)

OEMUnlockOnBoot is a simple Magisk/KernelSU module that ensures Android's `OEM unlocking` toggle is enabled on every boot. It is meant for use in setups where the bootloader is locked with the user's key (eg. with [avbroot](https://github.com/chenxiaolong/avbroot)) to ensure that the device is always recoverable in the event of a boot failure.

## Usage

1. Download the latest version from the [releases page](https://github.com/chenxiaolong/OEMUnlockOnBoot/releases). To verify the digital signature, see the [verifying digital signatures](#verifying-digital-signatures) section.

2. Install the module from the Magisk/KernelSU app.

3. Reboot. The log file is written to `/data/local/tmp/OEMUnlockOnBoot.log`.

## Verifying digital signatures

Each release includes a module zip and a detached SSH signature:

- `OEMUnlockOnBoot-<version>-release.zip`
- `OEMUnlockOnBoot-<version>-release.zip.sig`

To verify a download, create a trusted signers file and run `ssh-keygen -Y verify`.

For Unix-like systems and Windows Command Prompt:

```bash
echo chenxiaolong ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIDOe6/tBnO7xZhAWXRj3ApUYgn+XZ0wnQiXM8B7tPgv4 > chenxiaolong_trusted_keys
ssh-keygen -Y verify -f chenxiaolong_trusted_keys -I chenxiaolong -n file -s <filename>.sig < <filename>
```

For Windows PowerShell:

```powershell
echo 'chenxiaolong ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIDOe6/tBnO7xZhAWXRj3ApUYgn+XZ0wnQiXM8B7tPgv4' | Out-File -Encoding ascii chenxiaolong_trusted_keys
Start-Process -Wait -NoNewWindow -RedirectStandardInput <filename> ssh-keygen -ArgumentList "-Y verify -f chenxiaolong_trusted_keys -I chenxiaolong -n file -s <filename>.sig"
```

If verification succeeds, `ssh-keygen` reports a `Good "file" signature`.

For additional details, see [VERIFY_SSH_SIGNATURES.md](https://github.com/chenxiaolong/chenxiaolong/blob/master/VERIFY_SSH_SIGNATURES.md).

## Building from source

OEMUnlockOnBoot can be built like most other Android projects using Android Studio or the gradle command line.

To build the module zip:

```bash
./gradlew zipRelease
```

The output file is written to `app/build/distributions/release/`.

## License

OEMUnlockOnBoot is licensed under GPLv3. Please see [`LICENSE`](./LICENSE) for the full license text.
