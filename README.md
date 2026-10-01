# Edith Bramble — Famous.ai Sync

This repository is the handoff repository for the **Edith Bramble Chronicles / Orchid Continuum interactive experience**.

## Purpose
Reconcile the existing Famous.ai project with the latest revised source package without rebuilding the experience from scratch.

## Source-of-truth rules
- Preserve working Famous.ai functionality that is more complete than the exported package.
- Use the latest revised Chronicle II and fictional supporting cast.
- Do not restore rejected older Chronicle II / microscope / pencil-map versions.
- Treat Featured Genus and Species Dossier as reusable Orchid Continuum modules.
- Preserve scientific provenance, uncertainty, attribution, and honest missing-data states.
- iPad accessibility is a first-class acceptance target.
- Do not use Vercel.

## Famous.ai implementation

### Which export is authoritative — decided by evidence, not by this file

Authority is the export whose build **is** the live application, as measured by the
Calyx application certification (`jsp1440/orchid-calyx-backend`, CALYX-APP-CERT-001):

| export | sha256 | status | evidence |
|---|---|---|---|
| `story-orchids-interactive 9.zip` | `a390b803bb6c1c91ce1209df03fdbfcbdcc4b38cf4d1b6bd41579087bfd37a90` | **source of the live build** at `story-orchids-interactive.deploypad.app` | building it yields `index-Di4GJQ4W.js`, sha256 `964a9729741ba611d45f1bc384e08322cc08bbcb9808ac5e5a7a77964ee0894a`, byte-identical to the live JavaScript (certification run `edith-cert-20261001T091846Z-1757d973`) |
| `story-orchids-interactive%205_COMPLETED.zip` | `5ae8fb6cf859c88cce834f3a63048a63a253c673b6a02babf9d75a374ae7fd99` | **historical provenance only** | does not match the live build: no OC/Calyx endpoint wiring, client-side role writes instead of the `set_user_role` RPC, 1205/1443 prose literals in the live bundle |

When a new export is added, it becomes authoritative only after the certification
proves its build matches the deployed site. Newer is not evidence.

### Repairs reproduced against export 9

`repairs/export-9/export-9-repairs.patch` fixes the defects the certification
reproduced against export 9 (typecheck errors, and the Go Deeper copy that tells
readers "The Orchid Continuum / Calyx integration is not live"). The package-lock
is out of sync with `package.json` and must be regenerated with `npm install`.
See `repairs/export-9/README.md`. Famous.ai should apply the repairs to the live
project, redeploy, and export the result here; the certification then re-tests the
live runtime.
