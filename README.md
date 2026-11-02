# tandem.kautiontape.com

Static landing + privacy policy for **Tandem Alarm**, an Android alarm clock that pairs
two phones (package `com.kautiontape.tandem`). The app lives in
`github.com/shawnsquire/tandem-alarm`; this is just the public web presence.

- `index.html` — product landing page
- `privacy/index.html` — privacy policy (the URL given to the Google Play listing; the
  Data safety form links `https://tandem.kautiontape.com/privacy/#deleting-your-data`)
- `favicon.svg` — the app icon (same artwork as the launcher icon)

No build step. The host nginx serves this directory directly and terminates TLS, same
as the other static subdomains (alphaplate, glitterdelve). Pushing to `main` triggers
`.github/workflows/deploy.yml`, which `git pull`s into `/opt/services/tandem` on the ktn
runner (HTTPS origin; ktn holds no GitHub key).

## One-time wiring (on the ktn host, outside this repo)

1. `git clone` this repo to `/opt/services/tandem`.
2. Add an nginx server block for `tandem.kautiontape.com` whose root is
   `/opt/services/tandem`, with TLS (same pattern as alphaplate.kautiontape.com).
3. DNS: nothing to do. `*.kautiontape.com` already resolves through Cloudflare.

## TODO

- Add the Play opt-in link in `index.html` (search for `TODO`) once the closed test exists.

## Keeping the privacy policy in sync

The privacy policy is authored as Markdown in the app repo (`docs/privacy-policy.md`).
When it changes, update `privacy/index.html` here to match.
