Mobile-Only Profile (WebOS LG)

- Project path: `mytv-webos_lg_mobile_only_20260226_v1`
- Data source: Mobile API only (`https://androidapi.appmytv.com/android/v2/...`)
- No TV Box endpoints (`stb/v2`) are used.
- No local backend (`127.0.0.1`, `:8789`, `/api/catalog`, `/api/request`) is used.

Implemented request mode:
- Primary: signed mobile request (`X-Smile-Sign`, `X-Smile-Timestamp`, `data=<AES-CBC payload>`).
- Fallback: plain JSON mobile request.
- Response parser:
  - Tries direct JSON parse.
  - Falls back to mobile AES decrypt in `js/utils.js`.

Main mobile endpoints wired:
- `/users/checkCountry.php`
- `/version/checkVersionV2.php`
- `/campaigns/getCampaigns.php`
- `/channels/getChannelsDetail_local.php`
- `/movies/getMoviesDetail_local.php`
- `/series/getSeriesDetail_local.php`
- `/movies/getMovieInfo_local.php`
- `/series/getSeriesSeasonDetail.php`
- `/series/getSeriesEpisodeDetail.php`
