# Ami

Ami is an animated Windows desktop companion that can chat by text or voice,
use local Ollama models or supported APIs, remember useful context, work with
files and applications, and express herself through a 3D avatar.

## Download and run

1. Download `Ami-Windows-x64.zip` from the
   [latest release](https://github.com/mtfffg/ami-windows/releases/latest).
2. Extract the entire ZIP to a folder you control. Do not run it from inside
   the ZIP.
3. Run `Ami.exe`.

Nothing is installed into Windows. Delete the extracted folder to remove Ami.
Her settings, memory, API credentials, and logs live in the `local\` folder
inside it.

## First run

`Ami.exe` checks the machine, then offers to download her speech models. She
starts either way. Without those models you can type to her, and the capability
panel reports speech as unavailable instead of failing.

She will not answer until she has a brain configured. Once Ami starts, open
**Settings > Brain** and either add a supported API key or connect her to a
local Ollama model.

## What gets downloaded

`scripts\fetch_models.cmd` downloads what Ami needs to hear and speak, totaling
about 350 MB:

| Component | Approximate size | Purpose |
|---|---:|---|
| Ami's voice | 210 MB | Pocket TTS and the model that gives her a cloned voice instead of a stock voice |
| Whisper base.en | 138 MB | Turns your speech into text |
| Silero VAD | 2 MB | Detects when you start and stop speaking |

Her voice comes from Hugging Face rather than a plain file download, so the
setup process loads it once in advance. This prevents her first sentence from
stalling silently for a minute during a conversation.

There is also an optional Kokoro backup voice of approximately 337 MB. It is
used only if Ami's regular voice cannot load, so it is not downloaded by
default:

```powershell
scripts\fetch_models.cmd -IncludeBackupVoice
```

Other download commands:

```powershell
scripts\fetch_models.cmd                 # Download everything missing
scripts\fetch_models.cmd -List           # Show model status without downloading
scripts\fetch_models.cmd -Only Whisper   # Retry only Whisper
```

Downloads resume when interrupted, and every file is checked by its expected
size so a truncated download is fetched again instead of failing later inside
a model loader.

None of these speech downloads are required to type to Ami. You can skip them
if you want a text-only assistant.

## Using local Ollama

Ami can run her primary language model entirely on your computer without an API
key.

1. Install [Ollama for Windows](https://ollama.com/download/windows).
2. Pull a model from a terminal:

   ```powershell
   ollama pull llama3.1:8b
   ```

3. Start Ami and open **Settings > Brain**.
4. Set **Assistant AI** to **Local Ollama**.
5. Select the downloaded model from Ami's Ollama model list.

Above the Assistant AI setting, Ami estimates what the computer can run—for
example, **Up to 14B parameters**. She bases this on available GPU memory, or
roughly half the system RAM when there is no dedicated GPU. The estimate assumes
the 4-bit quantization commonly used by Ollama.

Choosing a model larger than the estimate may cause Ollama to move work onto
the CPU. Responses can then become so slow that Ami appears frozen.

| GPU memory | Suggested maximum | Example models |
|---:|---:|---|
| 6 GB | Up to 8B | `llama3.1:8b`, `qwen2.5:7b` |
| 12 GB | Up to 14B | `phi4:14b`, `qwen2.5:14b` |
| 24 GB | Up to 32B | `qwen2.5:32b` |

If Ollama is running but Ami's model list is empty, select **Refresh Ollama
models**. Ami reads the list directly from Ollama, so anything already pulled
should appear there.

Local models are generally slower and less capable than hosted APIs, but their
conversation data stays on your machine.

## If something is wrong

Run the packaged preflight check:

```powershell
scripts\preflight.cmd
```

It reports missing requirements and suggests how to correct them. Runtime logs
are stored in `local\logs\`.

When reporting a problem, do not publish API keys, private files, memories, or
logs containing personal information. See [SECURITY.md](SECURITY.md) for
security-sensitive reports.

## Updates

Open **Settings > Home > App updates**. Ami checks this repository's official
GitHub Releases feed and selects the matching Windows package. If an update is
available, **Quick update** opens that exact release download.

Close Ami before replacing her program folder. Preserve the existing `local\`
folder because it contains your settings and memory.

## Licensed assets

The packaged application contains licensed third-party character and animation
assets incorporated into the functioning program. Those assets are not
licensed for extraction, resale, repackaging, or redistribution on their own.
See [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md).

This repository is Ami's official Windows release and download hub. It does not
publish the private development tree or third-party source assets.
