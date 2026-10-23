# Rittal Dashboard

One repo holding both Rittal ELA2 Usage Level Report Builder apps. Each app is
its own Cloudflare Worker and deploys from its own folder.

| Folder       | Cloudflare Worker                                  | Formerly                                           |
|--------------|----------------------------------------------------|----------------------------------------------------|
| `main/`      | `rittal-ela2-usage-level-report-builder`           | `HP6673/rittal-ela2-usage-level-report-builder`    |
| `tradeshow/` | `tradeshow-rittal-ela2-usage-level-report-builder` | `HP6673/tradeshow_rittal-ela2-usage-level-report-builder` |

The Worker name in each folder's `wrangler.json` sets the live URL, so keep
those names unchanged to keep the existing links working.

## Local development

Run commands from inside the app's folder:

```bash
cd main        # or: cd tradeshow
pnpm install
pnpm run dev
```

## Cloudflare deploy settings

In Workers & Pages, open each Worker → Settings → Build, connect it to
`HP6673/rittal-dashboard`, and set:

```text
Root directory:                       /main   (or /tradeshow)
Build command:                        pnpm run build
Deploy command:                       pnpm exec wrangler deploy
Non-production branch deploy command: pnpm exec wrangler versions upload
Build watch paths (include):          main/*  (or tradeshow/*)
```

The build watch path keeps a change in one app from redeploying the other.
