# ECZ-ID MSP Evidence & QBR Pack

Turn observable GitHub and machine-estate facts into a deterministic client evidence pack for QBR, vCISO, insurance and regulatory review workflows.

**Start without an ECZ-ID account or API key.** GitHub Actions runner usage follows your GitHub plan.

This is a thin GitHub Marketplace discovery wrapper over the already-tested ECZ-ID MSP engine. It delegates to immutable engine commit `fedb5cb7633e7cf74c952291a7fbe302e5333af6`; it does not duplicate the engine or create a second source of truth.

## Run it now

Create `.github/workflows/eczid-msp.yml`, paste this complete first-run workflow, commit it, then run it from the **Actions** tab.

```yaml
name: ECZ-ID MSP Evidence & QBR Pack

on:
  workflow_dispatch:

permissions:
  contents: read

jobs:
  eczid:
    runs-on: ubuntu-latest
    steps:
      - name: Check out repository
        uses: actions/checkout@v7

      - uses: EcoCitizenz-Ltd/eczid-msp-evidence-qbr-pack@v1
```

### First-run path

1. Add the workflow above.
2. Run it manually with **Run workflow**.
3. Review the job output and generated local evidence report.
4. Use the bounded outputs below in your own MSP/customer policy.
5. If you want the wider estate view, [run the free MSP / MSSP Machine Trust Check](https://msp.ecocitizenz.com/trust-check?utm_source=github&utm_medium=action-readme&utm_campaign=msp-machine-trust&utm_content=eczid-msp-evidence-qbr-pack).

## Minimal Action step

Already have a workflow? Add only this step:

```yaml
- uses: EcoCitizenz-Ltd/eczid-msp-evidence-qbr-pack@v1
```

## Inputs

| Input | Required | Default | Meaning |
|---|---:|---|---|
| `path` | no | `.` | Repository-relative path to inspect. |
| `client-id` | no | empty | Optional MSP/customer identifier recorded locally in the pack. |
| `profile` | no | `qbr` | generic, qbr, vciso, cyber-insurance, nis2, iso27001, soc2, or dora. |
| `output-json` | no | `eczid-msp-evidence-pack.json` | Repository-relative JSON evidence pack path. |
| `output-markdown` | no | `eczid-msp-evidence-pack.md` | Repository-relative Markdown client summary path. |
| `fail-on` | no | `invalid` | invalid or never. |

## Outputs

| Output | Meaning |
|---|---|
| `result-state` | EVIDENCE_PACK_CREATED or INVALID_INPUT. |
| `evidence-hash` | SHA-256 hash of the normalized technical evidence payload. |
| `observed-count` | Number of evidence observations marked observed. |
| `not-observed-count` | Number of evidence observations marked not_observed. |
| `json-path` | Path to the JSON evidence pack. |
| `markdown-path` | Path to the Markdown client summary. |
| `next-action-url` | Contextual recurring-service next step when a managed-evidence need is indicated. |

## Trust boundary

- Runs in the caller's GitHub Actions workspace.
- No repository source upload to ECZ-ID.
- No hidden telemetry.
- Missing ECZ-ID identity is neutral and never means unsafe, non-compliant or untrusted.
- No universal safety, trust, certification or compliance verdict.
- No pay-to-pass.
- Local MSP/customer policy decides what observed evidence means.

## Engine provenance

Delegates to `EcoCitizenz-Ltd/eczid-msp-machine-trust-toolkit/actions/evidence-qbr-pack@fedb5cb7633e7cf74c952291a7fbe302e5333af6`. Marketplace wrapper releases must only advance this pin after the shared engine's cross-platform tests are green.

## Version pinning

Use `@v1` for ECZ-ID's stable compatibility channel. Where your organisation requires immutable third-party Action references, pin the wrapper repository to its full release commit SHA. The wrapper itself always pins the shared MSP engine by full commit SHA.

## Support and policy

See [PRIVACY.md](PRIVACY.md), [SECURITY.md](SECURITY.md), [SUPPORT.md](SUPPORT.md) and [LICENSE.txt](LICENSE.txt).

## Why this wrapper exists

GitHub Marketplace discovery works at the repository root. The underlying MSP engine intentionally keeps related Actions together; this wrapper makes one proven capability independently discoverable without copying implementation or creating maintenance drift.
