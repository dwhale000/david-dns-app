# David DNS

A DNS-based porn blocker built on [Blocky](https://github.com/0xERR0R/blocky),
deployed on Fly.io. Same setup as the gambling blocker, pointed at porn lists.

## How it works

1. A device uses this server for DNS (via DNS-over-HTTPS).
2. Blocky checks each domain against the blocklists in `config.yml`.
3. Blocked domains return `0.0.0.0` (the site fails to load).
4. Everything else is forwarded to Cloudflare / Google and works normally.

## The blocklists

`config.yml` loads two sources and blocks anything on either:

- **A public porn list** (large, maintained by others) — for broad coverage.
- **`porn-blocklist.txt`** (this repo) — your own custom additions.

The server re-downloads both once an hour (`refreshPeriod: 1h`), so editing
`porn-blocklist.txt` and pushing is enough — no redeploy needed for list changes.

## Updating your custom list

1. Edit `porn-blocklist.txt`
2. `git add . && git commit -m "update list" && git push`
3. The live server picks it up within an hour

## Deploying (changes to config/Dockerfile)

```
fly deploy
```

> If this repo is hosted under a GitHub account/name other than
> `dwhale000/david-dns-app`, update the custom-list URL in `config.yml`.
