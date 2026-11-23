# SaxSpheric channel branding

Channel: **SaxSpheric** — `@saxspheric` — channel ID: **pending**

| Asset | File | Status |
| --- | --- | --- |
| Avatar | `channel_avatar_800.png` | **manual upload in YouTube Studio** |
| Banner | `channel_banner_2048x1152.jpg` | ready for `scripts/update_channel_branding.py` |
| Description | `channel_description.txt` | ready for the branding script |
| Keywords | `channel_keywords.txt` | ready for the branding script |
| Video watermark | not used | the paper score owns the upper-right corner |

The channel itself still has to be created in YouTube Studio. The YouTube Data
API cannot create a channel, upload an avatar, or mint the first OAuth token.

## After the channel exists

1. Create a new YouTube channel named **SaxSpheric** in YouTube Studio.
2. Upload `channel_avatar_800.png` as the channel avatar (manual step).
3. Mint a channel-specific refresh token with the shared OAuth client:

```powershell
python scripts/get_refresh_token.py `
  --client-json "D:\E agy cli\E api tokens\.HarpSpheric\token_HarpSpheric.json" `
  --out "D:\E agy cli\E api tokens\.SaxSpheric\token_SaxSpheric.json" `
  --nickname SaxSpheric
```

4. Add these GitHub secrets to `velocityjapanese/sax-sphr`:
   - `YT_CLIENT_ID`
   - `YT_CLIENT_SECRET`
   - `YT_REFRESH_TOKEN`
   - `CHANNEL_NAME` = `SaxSpheric`
   - `POLLINATIONS_API_KEY`
5. Set the banner, description, keywords and country:

```powershell
python scripts/update_channel_branding.py --token "D:\E agy cli\E api tokens\.SaxSpheric\token_SaxSpheric.json"
```

6. Enable the daily workflow:

```powershell
gh workflow enable daily_sax.yml --repo velocityjapanese/sax-sphr
```

The workflow is intentionally left disabled until the channel and token exist.
Its schedule is **11:00 UTC** daily.
