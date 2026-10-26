# Visitor statistics (GoatCounter)

How visits and clicks on the personal homepage (henzandreas.github.io) are
counted. Written 2026-10-26.

## Account

- Service: [GoatCounter](https://www.goatcounter.com), free for non-commercial use.
- Account: **`henzandreas`** (one account holds several sites)
- Site code for this homepage: **`henzandreas-homepage`**
- Dashboard: <https://henzandreas-homepage.goatcounter.com>
- Count endpoint: `https://henzandreas-homepage.goatcounter.com/count`

The site has to be added once in the GoatCounter dashboard under
*Settings → Sites* with the code `henzandreas-homepage`; until then nothing is
recorded. The site code appears in the page source anyway, so it is not a
secret. The login is the account's e-mail and password; neither is stored here.

The Little Ice Age viewer (`/little-ice-age-glacier-viewer/`) has its own
GoatCounter site, `henzandreas-lia-viewer`, which counts everything that
happens inside the viewer. This homepage only counts its own visits and how
many visitors go on to the viewer from here.

## What is counted

Everything lives in `index.html`:

1. **Page views:** the GoatCounter script tag at the end of `<body>`:

   ```html
   <script data-goatcounter="https://henzandreas-homepage.goatcounter.com/count"
           async src="https://gc.zgo.at/count.js"></script>
   ```

2. **Language switch:** the click handler of the EN / DE buttons calls
   `countEvent("language/<code>")`. It counts only real switches, not clicks on
   the language that is already active.
3. **Viewer link:** the project card has
   `data-goatcounter-click="link/lia-viewer"`, so GoatCounter counts the click
   itself, without extra JavaScript.
4. **No privacy note (for now):** the homepage deliberately has no footer about
   the counting. GoatCounter sets no cookies and stores no personal data, so no
   consent banner is needed, but Swiss and EU data protection rules usually
   expect analytics to be mentioned somewhere. **To do:** as soon as the page
   gets regular traffic, add a short privacy / imprint note (e.g. a small
   privacy or imprint page linked from the homepage) saying that visits and
   clicks are counted anonymously with GoatCounter, without cookies or
   personal data.

When the script is blocked or has not loaded yet, `countEvent` does nothing and
the page works as before.

Events that appear in the dashboard (events are listed among the paths):

| Event | When it is counted |
|---|---|
| `language/de`, `language/en` | Switching the page language |
| `link/lia-viewer` | Clicking the Little Ice Age Glacier Viewer card |

To compare: `link/lia-viewer` here against the visits in the viewer's own
dashboard (whose referrer list also shows `henzandreas.github.io`) tells how
many viewer visitors come through the homepage.

## Notes

- Ad blockers block 10–30% of such scripts, so treat the numbers as lower
  bounds.
- GoatCounter ignores `localhost`, so local testing is never counted. Check
  from a browser without an ad blocker on the live site; the first hits show in
  the dashboard within a minute.
- No cookies are set, so no consent banner is needed (GDPR / Swiss data
  protection law).

## Adding more tracking

- **Links or buttons present in the HTML:** add
  `data-goatcounter-click="<event-name>"` (optionally
  `data-goatcounter-title="..."`).
- **Anything triggered from JavaScript:** call `countEvent("<event-name>")`
  from the inline script in `index.html`.
- Add each new event to the table above.

The GoatCounter setup was added with the help of Claude (Anthropic) in Claude
Code on 2026-10-26.
