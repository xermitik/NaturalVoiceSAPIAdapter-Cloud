# NaturalVoiceSAPIAdapter

NaturalVoiceSAPIAdapter is a Windows SAPI 5 text-to-speech engine. This fork keeps the functionality of the original project and concentrates on reliable configuration and use of cloud text-to-speech providers:

- Azure AI Speech Service
- Amazon Polly
- ElevenLabs

The fork does not remove the original project's support for Narrator voices, Edge Read Aloud voices, or local voice packs. Those capabilities are intentionally outside this fork's user guide; use the [upstream documentation and wiki][upstream-docs] for their configuration and troubleshooting.

## Before you begin

- Use a Windows application that supports SAPI 5 voices.
- Install the adapter in a local folder that you intend to keep. Installation requires administrator approval.
- Create an account with each cloud provider you plan to use. Provider availability, quotas, and prices are controlled by that provider.
- Text submitted for synthesis is sent to the selected cloud provider. Do not use a provider for content you are not allowed to send to it.

## Install a release from this fork

Fork releases are **overlay packages**, not standalone distributions. An overlay contains files built or changed by this fork; the remaining files must come from the matching upstream release.

1. Open this fork release's notes and identify the required [upstream release][upstream-releases]. For example, fork release `v0.3.0` requires upstream `v0.2.9`.
2. Download the required upstream archive and extract it to its final local folder.
3. Extract this fork's archive into the **same** folder and allow it to replace files. Keep every file left by the upstream archive.
4. Run `Installer.exe` from the merged folder as administrator. Install the x86 component for 32-bit applications and the x64 component for 64-bit applications; install both when you use both kinds of application.
5. Configure the cloud providers you need, close the Installer to save the settings, then reopen the voice list in your SAPI application.

To update, apply a new overlay that names the same upstream base release to the existing installation folder, then run `Installer.exe` again. Do not move, rename, or delete an installed folder without uninstalling first.

## Configure cloud providers

The following instructions cover the cloud providers maintained by this fork. Other inherited voice options remain available, but their setup belongs to the upstream documentation.

### Azure AI Speech Service

1. In `Installer.exe`, enable **Azure online voices** and choose **Set Azure key**.
2. Enter the Speech resource subscription key and region from the [Azure portal][azure-portal].
3. Close the Installer, then reopen the voice list in the application that will use the voice.

### Amazon Polly

1. In `Installer.exe`, enable **Amazon Polly online voices** and choose **Set Polly keys...**.
2. Enter an AWS access key ID, secret access key, region, and the engine name you intend to use. All four fields are required; the adapter does not select an engine for you.
3. Use an engine that is available to your AWS account and region. Refer to the [Amazon Polly SynthesizeSpeech documentation][polly-docs] for current engine availability.

Polly returns audio only. SAPI word, sentence, and bookmark events are not available for Polly voices.

### ElevenLabs

1. In `Installer.exe`, enable **ElevenLabs online voices** and choose **Set ElevenLabs key...**.
2. Enter an API key and the Model ID you intend to use. Both fields are required; the adapter does not select a model for you.
3. Refer to the [ElevenLabs model documentation][elevenlabs-docs] when choosing a model.

ElevenLabs synthesis in this adapter uses plain text. SAPI SSML markup, bookmarks, and word or sentence events are not preserved for ElevenLabs voices.

## Privacy, credentials, and logging

Credentials are stored in the current user's adapter settings. Keep API keys and AWS secrets private; do not share exported settings or screenshots that include them.

Trace-level logging can contain the text submitted for synthesis and provider error responses. Leave trace logging disabled for normal use and do not share such logs without reviewing them first.

## Test the adapter

Use `TtsApplication.exe` from the architecture-matching `x86` or `x64` folder to test that the selected SAPI voice is available.

## Build this fork

Use Visual Studio 2022 with the **Desktop development with C++** workload, the v143 toolset, and a Windows SDK.

1. Initialize the submodules: `git submodule update --init --recursive`.
2. Restore the NuGet packages.
3. Build `NaturalVoiceSAPIAdapter.sln` in `Release|x64` and `Release|x86`. The x86 build also produces the installer.

The GitHub Actions workflow is the reference for the release build and archive layout.

## Upstream project and license

This repository is a fork of [gexgd0419/NaturalVoiceSAPIAdapter][upstream]. The upstream project remains the reference for features that this fork does not document. See [LICENSE.txt](LICENSE.txt) for the project license.

[azure-portal]: https://portal.azure.com/
[elevenlabs-docs]: https://elevenlabs.io/docs/overview/models
[polly-docs]: https://docs.aws.amazon.com/polly/latest/APIReference/API_SynthesizeSpeech.html
[upstream]: https://github.com/gexgd0419/NaturalVoiceSAPIAdapter
[upstream-docs]: https://github.com/gexgd0419/NaturalVoiceSAPIAdapter/wiki
[upstream-releases]: https://github.com/gexgd0419/NaturalVoiceSAPIAdapter/releases
