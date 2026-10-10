# Small AI for Windows

A small Windows app for local AI chat, short summaries and English rewrites. Choose a model, click Install, then Use. No Python, terminal, cloud account or separate runtime setup.

The warm dark "reading desk" layout uses large cream text, amber buttons and a sidebar. Qwen3 is the starting choice. Granite is an extra choice for chat and rewrites only.

## Download and start

Download **SmallAI-Windows-x64.zip** from this repository's GitHub Releases page. You do not need a GitHub account.

1. Right-click the ZIP and choose **Extract All**. Do not run the app inside the ZIP.
2. Open the extracted folder and run **SmallAI.exe**. Keep the **engine** and **licenses** folders beside it.
3. Choose a model and click **Install**. Internet is needed to download it. The app checks the file size and SHA-256 hash before loading.
4. Click **Use** and wait for **Ready**.
5. Select **Chat**, **Summarize** or **Rewrite**, enter short English text and click **Ask**. Granite does not offer summaries.
6. **Stop** cancels work and unloads the engine. Click Use to start again. A partial model download can resume with Install.
7. **Remove** deletes the selected model after confirmation. **Clear text** empties the text on screen.

## Requirements and safety

- Intended for Windows 11 x64 with a compatible CPU. This release was tested on a Windows Server CI machine, not on the owner's PC or a physical Windows 11 PC. Other Windows versions and hardware are unverified.
- Each model downloads less than 2 GB, but it needs more RAM and disk space than that. CPU speed and available memory affect loading and answers. No minimum RAM has been validated.
- This is an **unsigned early release**. Windows may warn or block it. Do not disable antivirus or other Windows security to run it. No installer or code-signing certificate is included.
- Inputs are limited to 6,000 characters and 1,400 model tokens. Answers may hit a length limit and be incomplete.
- Models can invent or change facts. Check names, amounts, numbers, dates, conditions and negatives against your source. The numeric checks are limited checks, not a guarantee.

## Models

| Model | Download | Tasks |
| --- | --- | --- |
| Qwen3-1.7B Q8_0 | 1,834,426,016 bytes | Chat, Summarize, Rewrite |
| Granite 4.0 1B Q8_0 | 1,737,791,232 bytes | Chat, Rewrite |

Granite's persistent note says: "Cleaner English for chat and rewrites. It may change details. Check important facts. Summaries use Qwen3."

Granite sometimes reformats dates. Qwen3 summaries can copy too much, change who did something, or change other details. This is not ChatGPT-level quality and is not suitable as an unchecked source for important decisions. English is the tested language. LFM is not included.

## Local data

Models download from Hugging Face. The bundled llama.cpp engine listens only on this PC's loopback address with a per-session key. Prompts are processed locally. The app does not upload prompts, save chats, send telemetry, execute generated code or control the PC.

Models are stored in the local app-data folder named **SmallAI-Prototype**. Closing the app stops its engine. Deleting the extracted app folder does not delete downloaded models. Use Remove first, or delete only that specific model folder yourself.

## Test status

Windows test run #15, source commit `79a63baf066119335b683d91b9606de44216df80`, passed in 8 minutes 28 seconds. It completed 67 functional checks, including two-model install/hash checks, offline answers, Stop/reload, partial downloads, Remove confirmation, input limits and the Granite summary restriction. The checks include 24 English output completions. **67 functional passes do not mean 67 accuracy passes.**

Actual rendered desktop and narrow-window screenshots were inspected. The narrow layout stacks the sidebar above the text workspace. Known model-quality limits remain. No test was run on your PC.

## Build from source

Use .NET 8 SDK on Windows. Run `./prepare.ps1` to create `src`, then:

```powershell
dotnet publish src/SmallAI.csproj -c Release -r win-x64 --self-contained true -o dist
```

The manual GitHub Actions workflow bundles the pinned llama.cpp CPU runtime, includes its licenses and the model licenses, renders the WPF UI, and tests real model downloads and replies. It is manual-only, not triggered by commits.

## Licenses

Qwen3 and Granite use Apache 2.0. The llama.cpp runtime uses MIT. The release keeps their license files and the Granite model card in **licenses**. Keep them with any redistribution. Model downloads use fixed revisions and verified hashes. Runtime release: llama.cpp b9999.

No separate open-source license has been selected for the app's own code. Public visibility alone does not grant an open-source license. Third-party components keep their own licenses.
