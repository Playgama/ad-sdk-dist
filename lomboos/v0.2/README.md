# lomboos Ads SDK v0.2

Stable CDN URL: https://cdn.jsdelivr.net/gh/Playgama/ad-sdk-dist@main/lomboos/v0.2/ads-sdk.js

Initialize with `pgAds.init({ clid, gameId })`.
SSP config: `default`. Advertising settings come from SSP without local overrides.
Country and publisher domain settings are fetched at runtime.
For shared GPT, the host must load GPT and enable its services.

Serve the script and static/ from the same directory. This SDK still uses Playgama services.
Keep third-party license notices in static/. See the repository README for terms of use.
