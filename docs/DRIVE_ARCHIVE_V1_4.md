# BitKultur Publications — archive workflow v1.4 (design / not enabled)

Status: STAGING DESIGN ONLY. No Drive credentials, external writes or scheduled jobs in this branch.

## Owner-configured target
- Preferred archive destination: Drive B, email@yanoshkatona.com (owner decision 2026-11-21).
- Owner-approved fallback if Drive B archive upload/readback fails: Primary Drive, mail@yanoshkatona.com. Verify Primary folder creation and upload/readback before switching the active configured destination.
- Never silently split one publication between accounts; select one verified destination per publishing operation and log which account was used. If both fail, block publication. Do not automatically repeat failed writes without reconciling their result.
- Logical root: `BitKultur Publications/{year}/{language}/{publication_id}/`.
- Valid languages: hu, en, de, ru. Publication ID is immutable and globally unique.

## Files per published revision
- `source.md`: original Markdown (approved content).
- `published.html`: exact HTML artifact that will be deployed (or web-linked Telegram/Telegra.ph source).
- `sources.json`: source register and verification dates.
- `media/`: images, license/attribution and checksums.
- `manifest.json`: publication_id, revision, language, category, editorial approval actor/time and approved SHA-256, source/content hashes, lifecycle status, public URL, GitHub commit, Telegram chat ID and message_id if applicable.
- `delivery.json`: each destination attempt and outcome, timestamps and provider returned IDs, append-only event record.

## Required workflow
1. Editorial draft and source review; owner approves exact content hashes **and target destinations**.
2. Generate the deployable web/Telegram artifacts and freeze immutable revision.
3. Pre-publication archive upload to the **designated Drive account**; read back every file; validate content checksums, manifest, filename, publication ID and approval status.
4. Only when archive verification PASS and owner approval matches: allow publishing adapter to perform an individually authorized operation. No unchecked retry.
5. After each successful publication, write provider URL, GitHub commit SHA and Telegram message_id as a new archive manifest revision. Read back to verify. If postpublication sync fails, record a recoverable reconciliation task; do not republish.
6. If prepublish archive fails, stop all publishing (FAIL CLOSED). Never display a success state.
7. If web deployment or Telegram transmission is ambiguous, reconcile externally before any action; never resend automatically.

## Idempotency and backfill
- Idempotency key = `publication_id + language + approved_revision_sha256 + artifact_kind`.
- On retries list existing manifest and compare hashes; identical bytes -> NOOP, mismatched bytes -> immutable new revision or BLOCKED on conflicting key.
- Previously published articles: import source when available, preserve actual provenance, use `historical_backfill` flag, never invent original Markdown or approval proof.

## Security and deployment
- Drive OAuth credentials confined to protected server-side config, least privilege and token rotation.
- Never put credentials in GitHub Pages, browser JavaScript or this public repository.
- Static GitHub Pages code cannot safely upload to private Drive; use an isolated backend/service or authenticated operator controlled publisher stage after approval.
- No action on `main` or GitHub Pages deployment until explicit owner release approval.
- The current GitHub Pages workflow deploys each `main` push: do not merge until release gate is configured and accepted.

## Pending checks
- Owner account selection COMPLETE: Drive B, email@yanoshkatona.com.
- Authorized test folder and a reversible non-public specimen with actual read-back.
- Browser viewport and accessibility regression test (desktop/tablet/mobile).
- Actual destination/link verification for EN/DE/Lexikon Telegram channels.
- Resource and permission gates on any eventual publisher service.
