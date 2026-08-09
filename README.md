# Ami for Windows

Ami is an animated Windows desktop companion that can chat by text or voice,
use local Ollama models or supported APIs, remember useful context, work with
files and applications, and express herself through a 3D avatar.

## Download and run

1. Open the repository's **Releases** page.
2. Download `Ami-Windows-x64.zip` from the latest release.
3. Extract the entire ZIP to a folder you control.
4. Run `Ami.exe`.

Ami is currently distributed as a portable Windows 10/11 x64 application.
Do not run it from inside the ZIP. The first-run screen explains how to add an
API provider or connect a local Ollama model and how to download optional
local speech models.

## Privacy

API keys, settings, memories, logs, and generated user data are stored in the
portable application's local `local` folder. They are never included in the
public download. Removing the extracted Ami folder removes that installation.

## Updates

Open **Settings > Home > App updates**. Ami checks this repository's official
GitHub Releases feed and opens the matching Windows package when an update is
available. Close Ami before replacing its program files and preserve your
existing `local` folder.

## Licensed assets

The packaged application may contain licensed third-party character and
animation assets incorporated into the functioning program. Those assets are
not licensed for extraction, resale, repackaging, or redistribution on their
own. See [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md).

This repository is the official Windows release and download hub. It does not
publish the private development tree or third-party source assets.

## Problems and security reports

Open a GitHub issue for reproducible application problems. Do not put API
keys, private files, memories, logs containing personal information, or other
secrets in an issue. Use the private reporting instructions in
[SECURITY.md](SECURITY.md) for security-sensitive reports.
