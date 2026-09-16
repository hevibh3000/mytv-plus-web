QA Verification Guide (Mobile-Only WebOS LG)

Goal:
- Prove that this build uses only Mobile API logic and is runnable.

Project:
- `mytv-webos_lg_mobile_only_20260226_v1`

1) Static Integrity Check
- Confirm no TV Box/local routes in `js/app.js`:
  - No `stb/v2`
  - No `127.0.0.1`
  - No `:8789`
  - No `/api/catalog`
  - No `/api/request`

Command:
```powershell
rg -n "stb/v2|127\\.0\\.0\\.1|8789|/api/catalog|/api/request" js/app.js
```

Expected:
- No matches.

2) Syntax Check
Command:
```powershell
node --check js/app.js
```

Expected:
- Exit code `0`.

3) API Smoke Test (Automated)
- Script: `qa/mobile_only_smoke_test.js`
- It validates:
  - `checkCountry`
  - `checkVersion`
  - `liveCatalog`
  - `moviesCatalog`
  - `seriesCatalog`
  - `seriesSeasons`
  - `seriesEpisodes`

Command:
```powershell
node qa/mobile_only_smoke_test.js
```

Expected:
- Critical tests pass:
  - `checkCountry`
  - `checkVersion`
  - `liveCatalog`
  - `seriesCatalog`

4) Runtime TV Validation (Manual)
- Build/install IPK on LG webOS.
- Validate these flows:
  - Open app and initial load succeeds.
  - Live tab renders and plays channels.
  - Series tab loads seasons and episodes.
  - Movie details open (and tags if endpoint responds).
  - Back key behavior and focus navigation with remote.

5) Evidence to Keep
- Console output from smoke test.
- Screenshot/video from TV for:
  - Live list
  - Series seasons
  - Episode playback
  - Movie details

Pass/Fail Rule:
- If any critical smoke test fails, build is not accepted.
