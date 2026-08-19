# NaturalVoiceSAPIAdapter v0.3.0

`v0.3.0` is an overlay release for the [upstream v0.2.9 release](https://github.com/gexgd0419/NaturalVoiceSAPIAdapter/releases/tag/v0.2.9). It preserves the original project's functionality and adds cloud-provider improvements maintained by this fork.

## Install

This archive is **not** a standalone distribution.

1. Download and extract the upstream `v0.2.9` archive to its final local folder.
2. Extract this `v0.3.0` archive into the same folder and allow it to replace files. Keep the other files from the upstream archive.
3. Run `Installer.exe` from the merged folder as administrator and install the x86 and/or x64 components required by your SAPI applications.
4. Configure the cloud provider you want to use, close the Installer to save the settings, and reopen the voice list in the target application.

## Cloud providers

- **Azure AI Speech Service**: configure the Azure Speech subscription key and region in the Installer.
- **Amazon Polly**: configure an AWS access key ID, secret access key, region, and a current engine name. The engine is a required field, so new provider engines can be selected without waiting for an adapter update.
- **ElevenLabs**: configure an API key and a current Model ID. The model is a required field, so new provider models can be selected without waiting for an adapter update.

## Service limitations

Polly and ElevenLabs return audio only, so SAPI word, sentence, and bookmark events are unavailable for these voices. ElevenLabs receives plain text; SAPI SSML markup is not retained.

## Privacy and support scope

Speech text is sent to the cloud provider selected for synthesis and may be subject to that provider's charges and policies. Keep credentials private and avoid sharing trace logs, which can include submitted text.

This fork's documentation covers Azure AI Speech, Amazon Polly, and ElevenLabs. The original project's other capabilities remain in the codebase; refer to the [upstream documentation](https://github.com/gexgd0419/NaturalVoiceSAPIAdapter/wiki) for them.
