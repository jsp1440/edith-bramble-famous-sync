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
The authoritative project export should be stored in this repository as:

`story-orchids-interactive-5-COMPLETED.zip`

Famous.ai should extract/reconcile that package against the existing live project, preserve stronger existing backend integrations, implement the required changes, test, repair, and only then declare publish readiness.
