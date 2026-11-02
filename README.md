# Steno

A meeting recorder that transcribes on your own computer, for macOS and Windows. This repository holds release builds only.

The latest release is [v1.1.0](../../releases/latest).

## Install on a Mac

Download `Steno-<version>-macOS-arm64.zip` from the [latest release](../../releases/latest), unzip it and move `Steno.app` to Applications. Apple Silicon, macOS 13 or later.

Steno is ad-hoc signed and not Apple-notarised. If macOS blocks it, open it once with right-click → Open.

On first use Steno asks for two permissions:

- **Microphone**, to record you.
- **Screen Recording**, which macOS requires for recording the other people on a call. Steno records their audio only, never your screen.

To upgrade, replace `Steno.app` with the new one.

## Install on Windows

1. Download `Steno-<version>-Windows-x86_64-setup.exe` from the [latest release](../../releases/latest). Windows 10 or 11, 64-bit Intel or AMD.
2. Run it. Steno installs for the signed-in user, without administrator rights.
3. Steno is not code-signed, so Windows SmartScreen asks once: choose **More info → Run anyway**.

To upgrade, run the new installer over the old one. For IT installs, `Steno-<version>-Windows-x86_64-setup.exe /S` installs silently. Uninstalling keeps your meetings.

## What it is

- **Recording:** Steno records the meeting (your microphone and the other people on the call) to your disk as it happens. A crash or quit keeps the audio recorded so far.
- **Transcription:** the meeting is transcribed on your computer, live while it runs, and Steno labels who said what. The speech models (about 1 GB) download once, after you agree.
- **Summaries and action items:** written by a language model you choose. It can be Ollama or LM Studio on your own computer, or any OpenAI-compatible service with your own key, which stays in your system's keychain. Steno summarises on its own only with a model on your computer; anything else waits for you to click Summarize.
- **Your files:** each meeting becomes a markdown file in `Documents/Steno`, which you can open in any editor. There is no account and no telemetry.

## Verify a download

Each release lists the SHA-256 of its downloads in `SHA256SUMS`.

On a Mac:

```sh
shasum -a 256 Steno-<version>-macOS-arm64.zip
```

On Windows (PowerShell):

```powershell
Get-FileHash Steno-<version>-Windows-x86_64-setup.exe -Algorithm SHA256
```

## License

Steno is MIT-licensed. The speech models it downloads keep their own licences:

- [Parakeet Ultra](https://huggingface.co/moondream/parakeet-ultra): CC-BY-4.0, by Moondream, derived from NVIDIA Parakeet TDT 0.6B v3.
- [Nemotron-3 Diarization](https://huggingface.co/nvidia/Nemotron-3-Diarization): OpenMDW-1.1, by NVIDIA.

Steno fetches both as int8 builds from [naklitechie/steno-speech-models](https://huggingface.co/naklitechie/steno-speech-models). It bundles ONNX Runtime (MIT) and libopus (BSD-3-Clause).
