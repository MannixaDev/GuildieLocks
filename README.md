# Forever Roster Planner

A planning board for World of Warcraft: Forever groups. Start a group, share its join code, and everyone:

- votes **Horde or Alliance**
- lists up to three **class/spec choices** in order of preference

The board then checks the composition against the group size (5-player dungeon, or a 10, 20, 25 or 40-player raid). It flags too few tanks or healers, too many of a role, class stacking and open spots, and names who could switch to a backup role.

It's a single static page (`index.html`), hosted on GitHub Pages, with Firebase Firestore storing the shared data.

## Setup

### 1. Create the Firebase project (free Spark plan)

1. Go to <https://console.firebase.google.com> and choose **Create a project**. Google Analytics isn't needed.
2. **Build → Authentication → Get started → Sign-in method**, then enable **Anonymous**.
3. **Build → Firestore Database → Create database**. Pick a location and start in **production mode**.
4. In Firestore, open the **Rules** tab, paste in the contents of [`firestore.rules`](firestore.rules), and click **Publish**.
5. **Project settings (gear icon) → General → Your apps → Web (`</>`)**. Register an app (no Hosting needed) and copy the `firebaseConfig` values it shows.
6. Paste those values into [`firebase-config.js`](firebase-config.js), then commit and push.
7. **Authentication → Settings → Authorized domains**. Add `mannixadev.github.io`.

The Firebase web config is meant to be public. The Firestore rules are what keep each player's entry editable only by them, and groups editable only by whoever created them.

### 2. Turn on GitHub Pages

In this repo: **Settings → Pages → Build and deployment**. Set Source to **Deploy from a branch**, branch `main`, folder `/ (root)`, then click Save.

After a minute the site is live at <https://mannixadev.github.io/GuildieLocks/>.

## How players are identified

Each browser signs in anonymously in the background, so nobody needs an account. A player's entry stays tied to the browser they used. If they switch device or clear site data, they rejoin with the code and enter their picks again.

## Classes and specs

The class list follows the published Forever guides: 9 classes, all available to both factions. Druid Feral is split into Cat (DPS) and Bear (tank) so tank counts come out right. To change classes, specs, or the role targets per group size, edit `CLASSES` and `SIZES` near the top of the script in `index.html`.

---

Fan-made tool. Not affiliated with or endorsed by Blizzard Entertainment.
