# Pro Race Ready — Changelog

A sailboat-racing companion for Keyport Yacht Club (KYC) Wednesday-night racing and
custom courses. Single-file PWA (HTML/JS/CSS), offline-capable, hosted on GitHub Pages.

Live: https://superiyer.github.io/ProRaceReady-By-Raju/
Created by Raju Venkatraman.

The `vNN` markers below correspond to the service-worker cache version (`sw.js`),
which is bumped on every deploy so phones pull the new build.

---

## Foundation (initial build)

- **Course engine** — 8 KYC marks (A–H) plus CM (committee/center), the published
  magnetic heading matrix, and 6 course families (Wind/Lee, Trapezoid, Modified Olympic,
  Modified Triangle, Long Triangle, Short W/L) with 1–4 laps.
- **Heading table** — full leg-by-leg sequence with from→to, magnetic heading, GPS-computed
  leg distance, and the destination mark's coordinates.
- **To-scale course diagram** — north-up SVG built from the mark coordinates.
- **Custom Race mode** — build any course from your own marks (Start + up to 6 + Finish),
  decimal or deg-min input, editable magnetic variation; headings computed from coordinates.
- **Shared races (cloud)** — save/load named custom courses via a Google Apps Script + Sheet.
- **Live GPS** — SOG, COG (magnetic), position, next-mark guidance, breadcrumb track.
- **Wind tactics** — point of sail (beat/reach/run), close-hauled & gybe headings, layline calls,
  favored tack, steer-to guidance.
- **PWA** — installable, offline cache, Apple touch icons, manifest.
- **Access gate** — animated splash, User Agreement (every launch), hashed access code
  (remotely changeable kill-switch via `config.json`).
- **Analytics** — anonymous device/session usage to a Google Sheet, plus a reporting script
  (Dashboard / By User / By Day / Courses / Devices).
- Magnetic variation (~14°W) derived from the data itself (no hard-coded constant).
- Node test harness (`test.js`) for the pure data/geo/tactics logic.

---

## Recent changes

### v16 — Set Course gate & cleaner start
- Added a **Set Course** button to KYC mode; the table + map appear only after tapping it.
- No default course is pre-selected (fixes phantom "W1A" analytics on open).
- Custom Race coordinates start blank with sample hints only in the Start row.
- Larger Map-page title; the separate timed splash is hidden (Agreement page covers it).

### v17–v20 — Map clarity
- **Off-grid note** explaining the boat only plots inside the course area.
- **GPS-off hint**; messages reworded to be short and consistent (no contradictions).
- **Next-mark direction** spelled out and shown in parentheses, e.g. `Next mark: C (East)`.

### v21–v23 — Branding & layout polish
- Bigger logo-before-name brand band with a stylish credits band (consistent both screens).
- **Wind compass** on the live map (amber arrow to windward).
- Footer cleaned to the exact User Agreement + info; removed legacy text.
- User Agreement + info footer added to the Map page too.

### v24–v25 — Tactics on the map
- **Most-efficient wind route** to the next mark: dotted line with a single **tack (T)** when
  beating or **gybe (G)** when running, to the layline.
- **Laylines** drawn from the next mark (faint dashed; the two relevant for the point of sail).

### v26 — Wind compass readability
- White, larger arrowhead for clear reading on a phone.

### v27–v28 — iPad support & decluttering
- Detect **iPadOS** for analytics (Safari reports a desktop UA).
- **Side-by-side** Course + live map on tablet/desktop **landscape**; **full-width** map on
  iPad **portrait**.
- Removed the redundant static course diagram and the Print / Open-map buttons.

### v29 — Single page + breadcrumb fix
- Removed the Course/Map tabs — one continuous scroll; the live map reveals under the table
  on **Set Course**.
- **Breadcrumb bug fix**: the trail now records vs. the last breadcrumb (was the previous fix),
  so it accumulates at slow speed.

### v30 — Pinch-zoom map
- **Pinch to zoom** and **drag to pan** the course map, bounded to the course; one finger still
  scrolls the page when not zoomed.

### v31–v33 — Sticky brand bar
- **Locked top bar**: logo + "Pro Race Ready!" + credits stay fixed, **Start GPS** pinned right.
- Larger responsive title and logo; phone number on its own line in phone portrait.
- Larger, screen-fitting live **Position** readout; removed the "all roundings to port" note;
  hid footer info notes except the User Agreement.

### v34–v35 — Ping the Line
- **Ping the line**: pin the start-line ends and get the **favored (more-upwind) end** for the
  entered wind. KYC auto-uses **CM** as the pin end (ping only the RC/boat end); custom pings both.
- **Distance-to-line** with **OVER EARLY** detection and time-to-line at current speed.
- **Start countdown timer** with **Sync** (snap to nearest minute) and Reset.

### v36 — Collapsible phase sections
- Start-line and Next-mark sections are collapsible and **auto-swap at the start**
  (pre-start shows start tools; crossing the line opens next-mark).

### v37 — Gun cues
- Beep + vibrate (Android) + flash at the **3/2/1 min**, the **final 10 s**, and the **gun**.
- Live countdown shown in the collapsed Start header.

### v38 — ISAF 5·4·1 preset
- One-tap **World Sailing Rule 26** start sequence: signals at **5:00 / 4:00 / 1:00 / gun**,
  with a phase label (Warning → Preparatory → One minute → STARTED).

### v39 — Race timer
- New collapsible **Race timer** section: **arms at the gun**, **auto-clocks roundings** into
  **lap/leg splits**, with **Mark / Undo / Finish / Reset** (and manual **Start**).
- Auto-finish at the last mark with per-lap times + total. A lap = each CM passing.

### v40–v46 — Race-day refinements
- Start countdown **retires at the gun**; the whole **Start-line section hides once racing**
  (back on a race Reset for general recalls).
- **Confirm / Cancel** prompts on Race-timer **Reset** and **Finish** (finish time stamped at the tap);
  **Start** hides once the race is running.
- **Course setup** (mode toggle → Set Course) is now a **collapsible section** that folds on Set Course,
  showing the chosen course in its header.
- Wording/visibility tidy-ups: CM = Center Mark; "Ping RC boat end"; start-line legend moved into the
  Start-line section and hidden once racing; footer hint hidden.

### v47 — RC Race (committee-boat course)
- New third mode **RC Race**: **ping the committee boat** (or type its position), then place each mark by
  **magnetic bearing + distance (nm)** — Windward, Offset, Reach/Wing, Leeward, Pin, Finish.
- Enter the **wind**, tap **Set Course**, and all marks are computed and plotted, with the **start line =
  RC ↔ Pin** auto-set (favored-end works immediately).
- Builds the **course sequence** (Windward → Offset → Reach → Leeward, repeated for laps) and feeds the
  heading table, next-mark guidance, route, laylines, and race timer. W/L laps go leeward → windward
  directly (no start rounding between laps). **Custom Race is unchanged.**

### v82 — Silence + accurate mark rounding
- **Removed all sound effects.** No more start/mark/finish horns, timer beeps, or the layline beep — the
  app is now silent. The start countdown keeps its **silent on-screen flash** (and a short vibrate on
  phones that support it); the layline still shows the **red arrow** visually.
- **Mark rounding now triggers after you actually round**, not as you approach. Instead of advancing the
  moment the boat comes within ~50 m of the mark, it arms in that zone, tracks the **closest point of
  approach**, and advances only once the boat has moved back out ~20 m past it — i.e. you've turned the
  corner and are heading down the next leg. Manual **Mark / prev / next** still work instantly.

### v81 — RC pin: online storage + Clear-line keeps it
- The remembered **RC boat position is now stored online** (Google Sheet backend, per device) as the
  source of truth, with the on-device copy kept as an instant/offline cache. So it survives a reinstall
  or a new phone, not just an app restart. Requires the backend to support `save_pin` / `get_pin`.
- **Clear line no longer forgets the remembered pin** — it just clears the on-screen start line so you can
  re-ping; the saved RC position stays and is restored when you next set a course.

### v80 — Race sound effects + remembered RC pin
- **Ship's Horn sound effects** now play at the three big moments — **race start**, **each mark
  rounding**, and the **finish** — each as a **triple horn blast** (synthesized, no files). Great on a
  bluetooth speaker. (Audio unlocks when you start a timer or open the Race View.)
- **RC boat position is remembered on this device.** Your **Ping RC boat** position is saved locally and
  **restored as the default RC end** when you set a course, so a mid-race app restart no longer loses your
  start/finish line. **Clear line** forgets it; a fresh ping updates it.

### v79 — Sound-sample preview + service-worker hardening
- Added a standalone **`sounds.html`** audition page (three themes: Regatta Bells, Ship's Horn, Arcade
  Victory) to pick race sound effects before wiring them in. Not linked from the app.
- **Service worker:** only the **app shell** (root / `index.html`) is cached back as `./index.html`.
  Previously *any* navigation was, so opening another page (like the samples) could overwrite the offline
  app. Non-shell pages now fall through to normal caching.

### v78 — Auto-fill wind from the first mark (KYC)
- Picking the **first mark** (the "wind direction" step) now **pre-fills "Wind from"** with that mark's
  bearing — e.g. first mark **C (East) → 090°M**. Adjust it to your true wind reading as needed. Applies to
  KYC courses only (RC has its own wind entry; Custom has none).

### v77 — Layout cleanup
- **Course type is now a dropdown** (KYC), defaulting to **Z · Trapezoid** (first in the list). Laps and
  First mark stay as buttons.
- **Start-line timer and Race timer moved directly under Course Setup**, and **both start collapsed**.
- **Removed the SOG / heading / wind strip** at the top of the live map (redundant with the Race View and
  guidance panel).
- **Removed the old side-by-side Race View.** There's now a **single race-view button** (the checkered
  flag) that opens the **stacked top/bottom compasses** — the double-flag button is gone.

### v76 — Bow-sight mark ID + layline alarm + build tag
- **Build tag on the splash:** the launch screen now shows the current **build number** (e.g. "Build v76")
  so you can confirm at a glance you're running the newest deploy.
- **Bow-sight (boat compass):** a circled **mark letter** now appears at the centre of the boat when
  your bow is lined up to pass within **50 yards** of a mark (scanning all KYC marks, not just your
  course). It's **green** when that's your **next mark** and **red** when it's a **different** mark — a
  wrong-mark warning (the accuracy sharpens with distance, since it's a cross-track test).
- **Layline alarm (mark compass):** when you reach the **layline** to the mark (the mark sits at your
  wind-based **tacking angle** off the bow, on either side), the mark arrow turns **red** and the app
  gives a **double beep + buzz** — once on entry, re-arming when you leave. Applies while beating upwind.
- The mark-compass wind arrow is now **thinner** and drawn as a **dashed** line (solid arrowhead) to
  set it apart from the boat-compass wind arrow.

### v74 — Wind arrow on the mark rose
- Added the green **wind-from arrow** to the bottom (mark) compass in Race View 2, drawn **thinner**
  than the one on the top (boat) compass.

### v73 — Drop the depth caveat line
- Removed the always-on "depth is approximate" note under Race View 2; the **≈ DEPTH** label already
  signals it's an estimate.

### v72 — Approximate depth (Race View 2)
- The boat compass's bottom-right corner now shows **≈ DEPTH** in feet at your location, from **NOAA
  NCEI** global bathymetry (free, no key). Throttled (refetch after ~40 m moved, min 8 s apart).
- **Important:** this is surveyed sea-floor depth vs a fixed datum — **approximate, not tide-corrected,
  online-only** — a rough indicator, **not for navigation**. Shows "—" when offline.

### v71 — Faster updates
- The page (HTML) is now fetched **network-first**: a single normal refresh shows new content when
  online, while the cached copy still loads instantly when offline. Static assets stay cache-first.

### v70 — Race View 2 heading labels
- Top compass label is now **Boat heading**; bottom compass label is now **Mark heading**.

### v69 — Race View 2 label tweaks
- Bottom-right distance unit shortened to **YD**.
- Bottom (mark) compass labels (Heading, Next mark, Distance) now **yellow** to match the mark arrow.

### v68 — Race View 2 separator
- Added a **white band** between the two stacked compasses in Race view 2.

### v67 — Checkered-flag icons + Race View 2 sizing
- Race buttons are now **checkered flags**: **one flag** for Race view, **two flags** for Race view 2.
- Race View 2: mark arrow made **thinner** again; compass **letters nudged inward** so they clear the
  tick notches; the **roses are a bit larger** (reclaiming the control-row height) and the **top numbers**
  (heading, speed / heading, next mark) are **bigger**. Bottom distance numbers unchanged.

### v66 — Race View 2 polish
- **Thinner** mark arrow on the bottom (mark) compass.
- Mark panel readouts re-arranged: **Heading** (bearing) top-left, the **next mark letter big** top-right,
  and **distance** along the bottom — **NM** bottom-left, **YDS** bottom-right.
- Compasses made **slightly smaller** for a touch more breathing room.

### v65 — Icon controls + stacked Race View
- The map control row is now **all icons**: **race car** (Race view), **F1 car** (Race view 2),
  **locate**, **sailboat** (Course), **camera drone** (Both), and a **cancel ⊗** (Clear). Icons are
  inline SVG, so they stay sharp and work offline.
- New **Race view 2** (second car icon) — the **same** heading / speed / wind / bearing / distance data
  as Race view, but the two big compasses are **stacked top (boat) and bottom (mark)** instead of side by
  side, so each rose is as **large as fits** on a phone. The readouts sit in the **corners around** each
  circle, with the **STEER / ON COURSE** cue across the bottom.

### v55 — Race View
- New **Race View** button (first on the map row) — a big two-column readout that **replaces the map**
  for at-a-glance steering. **Left:** your boat (fixed pointing up), **heading** on top, **SOG** below, plus a
  **green arrow** showing where the **wind comes from**. **Right:** a bold **black arrow** to the next mark,
  the **desired heading** on top, and **distance** (nm + yards) below.
- **Heading-up** orientation: arrows point to where the wind and mark are **relative to your bow**
  (mark to your right → arrow points right). Falls back to compass-up until there's a heading.
- Tap **Locate / Course / Both** to return to the map.
- Section order tidied: **Race timer** now sits below **Start line & timer**; **Next mark** stays just
  above the course map.

---

🤖 Generated with [Claude Code](https://claude.com/claude-code)
