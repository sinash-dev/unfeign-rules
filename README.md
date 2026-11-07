# Unfeign site label rules

Data file used by the [Unfeign](https://github.com/sinash-dev/unfeign) browser extension to recognise the "AI-generated" labels that websites show (YouTube, TikTok, pixiv, DeviantArt and others).

- `rules.json` is **data only**: CSS selectors and plain label texts. The extension never executes anything from it.
- The extension downloads this file at most once a day (no cookies, no referrer), validates it against a strict schema, and uses it only when its `version` is newer than the copy built into the extension. Users can turn updates off in the extension's settings.
- Rules with `"verified": false` were written from platform documentation and have not yet been checked against the live site.

## Format

```text
{ format: 1, version: <integer, increases with every change>, updated: <date>,
  rules: [ { id, site, hosts[], item, label: [{ selector, text?[], contains?[], attribute? }],
             media?, action: "blur-media" | "blur-item", verified, note? } ],
  searchRules?: [ { id, site, hosts[], item, link: { selector, attribute, json?, param? }, verified, note? } ] }
```

`rules` find a site's own "AI" label. `searchRules` find the source page of each image search result (Google, Bing, DuckDuckGo), which the extension checks against its bundled list of AI-image sites (CC0, from the uBlockOrigin AI Blocklist).

Limits enforced by the extension: at most 200 rules and 50 search rules, selectors up to 400 characters, plain hostnames only (no wildcards), unique ids.

## Changing a rule

Edit `rules.json`, **increase `version`**, and keep the extension's bundled copy (`src/adapters/rules.json` in the main repo) in step with its snapshot tests.

The X icon selector comes from [Stevo's AI Blocklist](https://github.com/Stevoisiak/Stevos-AI-Blocklist) (MIT).

## License

Apache-2.0. See [LICENSE](LICENSE).
