# Kılıbık — website

Static site for the Kılıbık mobile app, served by GitHub Pages at
<https://nodabasi.github.io/kilibik-app/>.

Plain HTML and one stylesheet — no build step, no dependencies. Edit a file, commit,
push; Pages redeploys in a minute or two.

## Pages

Turkish is the default language and sits at the root, because the app's interface is
Turkish only. English lives under `/en/` for store review and for anyone who lands here
without Turkish.

| URL | File | Used in the stores as |
|---|---|---|
| `/kilibik-app/` | `index.html` | Marketing URL (Turkish) |
| `/kilibik-app/support/` | `support/index.html` | Support URL (Turkish) |
| `/kilibik-app/privacy/` | `privacy/index.html` | Privacy Policy URL (Turkish) |
| `/kilibik-app/en/` | `en/index.html` | Marketing URL (English) |
| `/kilibik-app/en/support/` | `en/support/index.html` | Support URL (English) |
| `/kilibik-app/en/privacy/` | `en/privacy/index.html` | Privacy Policy URL (English) |

**Do not rename these directories.** Once the paths are registered in App Store Connect
and Google Play Console, changing one breaks a live store link.

## Editing

- Colours and layout live in `assets/style.css`; every page shares it.
- Links are relative, so the site also opens correctly straight from the filesystem.
- When the privacy policy changes in substance, update the effective date at the top of
  both `privacy/index.html` and `en/privacy/index.html`.
- Each page declares an `hreflang` pair pointing at both language versions of itself.
  Adding a page means adding both halves, or the pair goes stale.

## Keeping the policy true

Unlike a purely offline app, Kılıbık stores data on a server, so the privacy policy makes
concrete claims that the app has to keep honouring. If any of these change, the policy
changes with them:

- The data the app itself collects is limited to e-mail, display name, role, pairing,
  tasks and an FCM device token — no analytics or crash reporting are present.
- Ads are served by Google AdMob, which reads the advertising identifier, IP address,
  device information and ad interactions. That data goes straight to Google and is never
  joined to the account. Consent is gathered through Google's UMP form, plus ATT on iOS,
  and ads are capped at a 4+ content rating. If any of this changes — a new ad format, a
  new placement, an analytics SDK — the Advertising section of both policies changes
  with it.
- A task is readable only by its creator and its assignee, and this is enforced by the
  Firestore rules, not just by the interface.
- Account deletion removes the tasks, clears the partner's pairing, deletes the profile
  document and destroys the auth user.

## Local preview

```sh
python3 -m http.server 8000
# then open http://localhost:8000/
```
