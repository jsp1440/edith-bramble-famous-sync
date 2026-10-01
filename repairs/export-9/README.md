# Edith Bramble export-9 repair packet

`export-9-repairs.patch` (mirrored from `jsp1440/orchid-calyx-backend:artifacts/application-certification/edith-bramble/`) applies to `story-orchids-interactive 9.zip`
(`jsp1440/edith-bramble-famous-sync@b2e88c07`, sha256 `a390b803…7a90`) — the
export proven to be the live build (its build is byte-identical to the live
`index-Di4GJQ4W.js`, certification run `edith-cert-20261001T091846Z-1757d973`).

It repairs defects the certification reproduced against export 9:

| defect (certification gate) | repair |
|---|---|
| `tsc` TS2339 `import.meta.glob` / `import.meta.env` (`app_typecheck`) | add `src/vite-env.d.ts` (`/// <reference types="vite/client" />`) |
| `tsc` TS2345 `AuthModal.tsx(61)` (`app_typecheck`) | `setNotice(String(result.message))` |
| eslint `no-unused-expressions` `SanitationSpell.tsx` 44:7, 45:7; `prefer-const` `soundscape.ts` 45:7 (`app_lint`) | `if (...) ro.observe(...)`; `const semi` |
| Go Deeper tells readers "The Orchid Continuum / Calyx integration is not live" while the page's own status reads Connected and species are read live (`runtime_oc_wiring`, `journey_go_deeper_no_stale_not_live_claim`) | accurate copy: connected read-only for species; concept / pathogen / card subjects not yet served |

The lockfile (`app_lockfile_sync`) is repaired by running `npm install` in
the application after applying the patch; the hosted workflow validates
that the regenerated lockfile installs with `npm ci`.

The hosted certification workflow applies this patch to a copy of the
export and records build / lint / typecheck / lockfile results in
`repair-validation/` — evidence about the candidate repair only. The live
runtime is certified only after the repaired source is deployed by Famous.

## Validation evidence

Certification run `edith-cert-20261001T100602Z-6e22b394` (Calyx head
`dc27e0d9d2d9cb18dc7d43d5f5209b2bf18baecc`, Actions run 36846924318) applied
this patch (sha256 `9d3c2c6ffd1a439318f54b01243cc554cd2f1f5f9a77217a408db5006a7b9ad3`)
to a copy of export 9: patch applies; regenerated package-lock.json
(sha256 `80486e9b05ea3ceab8a58c98c501e36ab5905e4c2687734d818c2b6028ff7969`)
installs with `npm ci`; `npm run build`, `npm run lint` and
`tsc --noEmit -p tsconfig.app.json` exit 0; the built bundle no longer
contains "integration is not live". This is evidence about the repaired
source only. The live site is unchanged until Famous.ai redeploys it.
