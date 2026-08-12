# TemplateWhisper — historical Whisper server template

Small Python/Docker template for serving OpenAI Whisper through a Sanic HTTP server.

| Field | Value |
|---|---|
| **Status** | Historical experiment/template; not verified for current production use |
| **Last reviewed** | 2026-08-12 |
| **Canonical repository** | `justaride/TemplateWhisper` for this historical copy |
| **Default branch** | `master` |
| **Visibility** | Public |
| **Upstream context** | Existing documentation identifies this as a Banana serverless Whisper template derived from `sahil280114/serverless-template-whisper` |
| **License** | See [`LICENSE`](LICENSE) |
| **Live deployment** | None verified |

> [!WARNING]
> This repository pins Sanic `22.6.2`, installs Whisper directly from a Git repository, and contains deployment instructions for an older Banana workflow. Treat it as historical reference, not a current secure or supported transcription service.

## What is here

```text
app.py             model-loading and inference entry point
download.py        model download/preload helper
server.py          Sanic HTTP server wrapper
test.py            example request script
requirements.txt   historical Python dependencies
Dockerfile         container image
```

The repository is intentionally small and resembles an upstream deployment template. No repository-specific production deployment, service owner, SLA, authentication model, rate limit, storage policy, or monitoring setup was verified.

## Historical local inspection

Use an isolated environment. GPU/CPU compatibility depends on your PyTorch/Whisper environment and is not guaranteed by the current requirements file.

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
python server.py
```

Before running, inspect `app.py`, `server.py`, and `test.py` for expected request schema, model size, ports, and external calls. Do not expose the server to a network until authentication, payload limits, timeouts, logging, and resource isolation are implemented.

Container inspection:

```bash
docker build -t template-whisper .
docker run --rm -p 8000:8000 template-whisper
```

The exact container port and runtime behavior must be verified against `server.py` and `Dockerfile`; this README does not claim a tested current image.

## Upstream and local-change policy

The previous README largely reproduced Banana's upstream template instructions. For a template/fork repository, maintainers should document:

- exact upstream repository and source commit
- date copied or last synchronized
- local changes from upstream
- license/attribution obligations
- whether local changes are still used
- replacement or archive decision

Those details are not currently recorded beyond the historical upstream links in the former README. Until they are reconstructed, do not present this repository as an independently maintained product.

## Security and privacy

Audio can contain personal, confidential, biometric, health, legal, or customer information. Any real service must define:

- authentication and authorization
- accepted media types and maximum sizes/durations
- temporary-file handling and deletion
- encryption in transit and at rest
- model/provider and data-region policy
- logging/redaction and incident handling
- retention and user notice/consent
- denial-of-service and GPU resource controls

The template does not document these controls. Do not send sensitive audio to an unreviewed deployment.

## Verification required before reuse

1. update and lock all dependencies
2. pin Whisper/PyTorch/model revisions and verify licenses
3. run vulnerability and secrets scans
4. add unit/integration tests for request validation and inference
5. add authentication, rate limits, payload limits, timeouts, health/readiness, and structured logging
6. test CPU/GPU memory and concurrency behavior
7. build and scan the container
8. document model downloads, checksums, caching, and offline behavior
9. establish data handling, retention, deletion, and monitoring
10. choose and document a current deployment platform

## Recommended lifecycle decision

If no current system depends on this template, archive it and retain this README as a historical pointer. If it is still needed, create a new maintained service or modernization branch rather than deploying the old template unchanged.

## Maintenance rule

Update this README if the repo is archived, synchronized with upstream, modernized, deployed, or assigned an owner. Never replace the local project identity with unqualified upstream marketing/deployment copy.
