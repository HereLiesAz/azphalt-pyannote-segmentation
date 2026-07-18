# pyannote Segmentation

**pyannote segmentation 3.0 (speech activity / overlap)** — Frame-level speech activity, speaker-change, and overlap detection.

An **azphalt** AI-model plugin, packaged as a `.azp` (the azphalt analogue of a VS Code `.vsix`). It is
named for the *model*, not a single feature — the same model powers many tools, and it is **host-neutral**:
any azphalt host that understands its role can use it, not just one app. Install it from any host's
**Azphalt Storefront**.

## What it can do

- voice-activity detection
- diarization segmentation
- overlapped-speech detection
- silence trimming

## Roles (host-neutral routing)

This plugin contributes the role(s): `speaker-segmentation`. A host routes the model by role — it carries no
`targetApps`, so it is not tied to any single application.

**Example host — [Guillotine](https://github.com/HereLiesAz/Guillotine):** Desktop `diarizeSegModelPath` — `diarize_clip` (pair with WeSpeaker).

## Model file(s)

- **`segmentation.onnx`** (role `speaker-segmentation`) — [upstream](https://huggingface.co/onnx-community/pyannote-segmentation-3.0/resolve/main/segmentation.onnx)

Model license: **MIT (pyannote segmentation 3.0)**. This plugin's manifest/packaging is `MIT`.

## How it works — the VSCode Header Pattern

The `.azp` does **not** bundle the weights. The manifest declares each model as a *remote asset*
(`"path": ""` + `remoteUrl` + `checksum` + `byteSize`); the host downloads the weights on install and
verifies them against the pinned SHA-256 — exactly how a large VS Code extension fetches its language
server instead of shipping it inside the `.vsix`. `remoteUrl` points at this repo's own GitHub **Release**
asset (named the exact filename the host expects); the `release` workflow fetches the upstream model,
renames it, checksums it, and publishes it beside the packed `.azp`.

## Build / release

```sh
npm install && npm run build     # packs com.hereliesaz.azphalt.pyannote-segmentation-1.0.0.azp
git tag v1.0.0 && git push --tags   # runs the release workflow: hosts the model + .azp
```
