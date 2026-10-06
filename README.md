# openGym on iPhone

[openGym](https://github.com/DuarteSantos8/openGym) built and hosted on **GitHub Pages**, so you
can install it on an iPhone from Safari. You don't need a server, a Mac or an App Store account.

**App address:** <https://choralet.github.io/opengym-iphone/>

## How this works

Apple only allows native app installs through the App Store, and openGym isn't there. Safari can
install any website as a full-screen **home-screen web app** instead. This repository doesn't
hold openGym's code. It holds one GitHub Actions workflow that:

1. checks out the openGym release named in [`OPENGYM_VERSION`](OPENGYM_VERSION),
2. runs upstream's normal web build, unmodified, with the exercise images and GIFs pointed at
   the same jsDelivr CDN openGym's own demo and phone app use (so ~140 MB of media doesn't have
   to be hosted here), and
3. publishes the result to GitHub Pages.

GitHub Pages only serves static files. openGym's Node server can't run here, so the app runs in
**guest mode**, with everything stored on your phone.

| Works | Doesn't work (needs the openGym server) |
|---|---|
| Plans, all 1,324 exercises with animations, guided workouts, rest timer, PRs, stats, body weight | Passkey / Face ID sign-in |
| Custom exercises with photos and videos | Sync between devices |
| Imports (FitNotes, Strong, Hevy CSV, Apple Health weight) and JSON backups | Push reminders when the app is closed |
| Offline use after the first load | Admin dashboard, AI coach |

The **Sign in** buttons in the app go nowhere on this deployment. Ignore them and use
**Continue without account**.

## First-time setup (all on the iPhone)

1. **Turn on Pages.** In Safari, open
   [Settings → Pages](https://github.com/Choralet/opengym-iphone/settings/pages) for this repo.
   Under *Build and deployment → Source*, choose **GitHub Actions**.
2. **Deploy.** Open [Actions → Deploy openGym to GitHub Pages](https://github.com/Choralet/opengym-iphone/actions/workflows/deploy.yml)
   and tap **Run workflow**. If you can't see that button, tap **aA** in Safari's address bar →
   *Request Desktop Website*. It takes about 2 minutes; a green tick means it's live.
3. **Install it.** Open <https://choralet.github.io/opengym-iphone/> in **Safari**, then tap
   Share → **Add to Home Screen** → Add.
4. **Open it from the new home-screen icon**, not from Safari, and tap **Continue without
   account**. Load a starter plan or build your own.

> [!IMPORTANT]
> Use the app only from the home-screen icon. On iOS a home-screen web app has its **own
> storage, separate from Safari**: anything you log in a Safari tab won't show up in the icon's
> app, and the other way round.

## Keep your data safe

Your workouts live only in the app's storage on this iPhone. iOS doesn't clear a home-screen
app's data on a timer, but you lose it if you **delete the icon**, reset the phone, or (rarely)
iOS frees space under heavy storage pressure. So:

- Now and then, go to **Settings → Data → Export backup (JSON)** and save the file to Files or
  iCloud Drive. Use *Export with photos & videos (.zip)* if you've made custom exercises with
  media.
- **Settings → Data → Import backup** restores it, on this phone or on a real openGym server
  later.

## Updating openGym

The version is pinned on purpose, so an upstream change can't reach your phone without you
choosing it. Every Monday a workflow checks for a new openGym release and **opens an issue**
when there is one, so you get a GitHub notification.

To update: export a backup, then edit [`OPENGYM_VERSION`](https://github.com/Choralet/opengym-iphone/edit/main/OPENGYM_VERSION)
in the browser (for example to `v1.3.10`) and commit. The site redeploys by itself. Then swipe
the app closed and reopen it.

To try a version without committing, use **Run workflow** with the *version* field filled in.

## Things worth knowing

- **The site is public.** Anyone with the link can open the app, but each person only ever sees
  the data in their own browser. Nothing you log is uploaded anywhere.
- **Shared storage origin.** All GitHub Pages project sites under `choralet.github.io` share one
  browser origin. If you later host other Pages sites there, they could read this app's local
  storage. Keep that in mind, or move openGym to its own custom domain.
- **Moving to a real server later** (to get sync and passkeys): self-host openGym
  ([guide](https://github.com/DuarteSantos8/openGym/blob/main/docs/SELF_HOSTING.md)), export a
  backup here, and import it there.

## License

The workflows and docs here are MIT ([LICENSE](LICENSE)). openGym itself is AGPL-3.0-or-later and
is fetched unmodified from upstream at build time. The exercise media is © Gym visual; see
openGym's [NOTICE.md](https://github.com/DuarteSantos8/openGym/blob/main/NOTICE.md).
