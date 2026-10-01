# Applying the export-9 repairs inside the EXISTING Famous.ai project

Project: `story-orchids-interactive` (published at story-orchids-interactive.deploypad.app).
Do **not** create a new project, do **not** use Settings > GitHub "Create Repository & Connect",
do **not** touch Database > Import, and do **not** unpublish.

The repairs are six small text edits made in place in the Famous **Code Editor**,
plus an optional lockfile replacement. Each edit is "find this exact text, replace it
with this exact text". If the "find" text is not present exactly as written, **stop**:
the live project has changed since export 9 and the edit must be re-derived, not improvised.

Before editing: Code Editor > **Download** a backup of the current project.

## 1. Create `src/vite-env.d.ts` (new file, one line)

```ts
/// <reference types="vite/client" />
```

## 2. `src/components/auth/AuthModal.tsx`

Find:
```ts
      setNotice(result.message);
```
Replace with:
```ts
      setNotice(String(result.message));
```

## 3. `src/components/c1/SanitationSpell.tsx`

Find:
```ts
      stackRef.current && ro.observe(stackRef.current);
      rowRef.current && ro.observe(rowRef.current);
```
Replace with:
```ts
      if (stackRef.current) ro.observe(stackRef.current);
      if (rowRef.current) ro.observe(rowRef.current);
```

## 4. `src/components/c1/soundscape.ts`

Find (start of the line):
```ts
  let semi = map[m[1]]
```
Change only `let` to `const`:
```ts
  const semi = map[m[1]]
```

## 5. `src/components/pages/GoDeeperPage.tsx`

Find:
```
          This request was received by the boundary and intentionally not answered. No external data is fetched,
          cached, or invented while the Orchid Continuum / Calyx endpoint is unavailable.
```
Replace with:
```
          This request was received by the boundary and intentionally not answered: the Orchid Continuum does not
          yet serve this subject. No external data is fetched, cached, or invented. Species are read live, read-only,
          on their Species Dossier pages.
```

## 6. `src/content/modules/go-deeper.json` — replace four values

| key | find | replace with |
|---|---|---|
| `kicker` | `Reserved integration` | `Integration boundary` |
| `subtitle` | `A doorway to the Orchid Continuum / Calyx — built, boundaried, and not yet connected.` | `Where story deep links meet the Orchid Continuum / Calyx — connected for species, honest about everything else.` |
| `intro` (both strings) | `This section is a deliberate empty room. …` / `No integration is simulated. …` | `Species identity, media and dossier sections across this site are read live, read-only, from the Orchid Continuum: open any Species Dossier or the Featured Genus to see them, each with its source and its own reason when a section is not yet available.` / `This page is where deep links land when their subject is not yet served by the Continuum — concepts, pathogens and collector cards. Those requests are received and deliberately not answered: nothing is simulated, cached or invented.` |
| `notice.title` | `Not yet connected` | `Connected for species; other subjects pending` |
| `notice.body` | `The Orchid Continuum / Calyx integration is not live. …` | `Species (taxon) records are read from the Orchid Continuum through a read-only relay to the Calyx species dossier. Concept, pathogen and collector-card subjects are not yet served by the Continuum, so links for them resolve here and say so plainly.` |

Keep the JSON valid (quotes, commas). The full repaired file is inside
`story-orchids-interactive 9 + certification repairs.zip` at `src/content/modules/go-deeper.json`.

## 7. Optional: `package-lock.json`

`repairs/export-9/package-lock.json` (sha256 `80486e9b05ea3ceab8a58c98c501e36ab5905e4c2687734d818c2b6028ff7969`)
is the regenerated lockfile. Replace the project's `package-lock.json` with it **only** if the
Code Editor lets you replace a whole file's contents reliably (it is ~225 KB). It does not change
what the live site renders; it makes the exported source reproducible (`npm ci`). If you skip it,
certification will still report `app_lockfile_sync` FAIL for the next export, and nothing else.

## 8. Badge, then publish once

Settings > General > Famous.ai Badge: **Hide badge** (a plan feature per famous.ai/pricing).
Then use the project's normal **Publish / Update** action once, so code edits and badge
setting go live together. The badge is injected into the served page, not into the app's own
build, so whether the toggle alone takes effect without a publish is not documented; publishing
once after both changes avoids depending on it.

## 9. Export back for re-certification

Code Editor > **Download** the published project ZIP and upload it to
`jsp1440/edith-bramble-famous-sync` as a new file (e.g. `story-orchids-interactive 10.zip`)
via GitHub's "Add file > Upload files" on `main` — or tell the agent where it is.
Re-certification proves the upload is the live build by compiled-asset identity; it does not
rely on the file name or on this document.
