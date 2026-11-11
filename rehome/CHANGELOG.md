# Changelog

## 0.5.2
- Settings > Display & Night now has a saved **24-Hour Time** switch for each iPad.
- Digital faces, clock tiles, night clock, alarms, world clocks, calendar times and weather times share that setting.
  Without a saved choice, the browser's locale is used; older browsers without locale support keep 12-hour time.
- Update the Rehome app/add-on (or pull and recreate the standalone Docker container), then reload Rehome on each iPad.
  Existing pairings, layouts, photos and license settings are preserved.

## 0.5.1
Security fixes from the second security review, and two fixes to the light page found on a real iPad. Nothing changes for an
iPad that is already set up, except where it says so.
- **The add-on now really connects to Home Assistant.** In 0.5.0, Home Assistant's app base image started Rehome with an empty
  environment. Rehome never received its Home Assistant sign-in or its own settings, so the add-on showed the sample home with no
  key field, and its port 8099 wasn't limited to paired iPads. Rehome now keeps its environment. If the sign-in is ever missing
  again, Rehome says so in its log and on screen, and stays closed to everything except Home Assistant itself.
- **The light page's colour panel no longer covers Turn Off or the brightness hint.** It now sits above Turn Off and the colour
  button on every iPad, the right way up or sideways. The hint steps aside while the panel is open. The colour dots are at least
  44 points, and the hue and white sliders start where the light really is.
- **A colour bulb no longer seems to change on its own.** A bulb that fades (LIFX does) reports each step of the fade, and the page
  used to follow those steps back through old colours and brightness after you let go. Now what you chose stays on screen until
  the bulb reports it, or for 5 seconds at most. While your finger is down, your drag always wins, and the colour you let go on
  is always sent. Rehome never sends anything to Home Assistant because a state changed.
- **Settings → Paired Devices** (new). Every iPad paired with Rehome's own address, with its name and when it was last used. Tap a
  name to rename it. **Remove** stops that iPad at once, even mid-use: it has to pair again with a new code.
- An iPad now stays paired for 90 days after it was last used, instead of a full year from pairing. Every use starts the 90 days
  again, so an iPad on the wall never notices.
- **Locks, Alarms & Garage Doors → Only From Home Assistant** (in standalone: Only From the Admin iPad). Off unless you turn it on.
  When it's on, paired iPads still show locks, alarms and garage doors but can't unlock, disarm or open them, unless a
  scene or script you made does it.
- Setting up another iPad, changing the license key (which restarts Rehome) and managing paired iPads now need Home Assistant
  itself: Rehome opened from Home Assistant's sidebar. In standalone it's the **admin**: the iPad that set Rehome up. The admin
  can hand the job to another iPad (Paired Devices → Make Admin), and a lost admin is replaced by restarting Rehome and pairing
  with the code in its log. Any other iPad that asks sees "Ask the person who set up Rehome."
- A fixed **pairing_code** must now be 8 to 12 digits. A shorter one is ignored (the log says so); iPads it already paired stay
  paired.
- One device typing wrong codes can no longer lock every other device out of pairing.
- Rehome now answers only to its number address, `.local` names, `.home.arpa`, `.internal`, one-word names and Tailscale's names
  (`*.ts.net`, and bare MagicDNS names). If your iPads use another name, such as `rehome.lan`, add it to the new
  **allowed_hosts** option (standalone: `REHOME_ALLOWED_HOSTS`).
- Standalone answers only devices on your home network: private addresses, and Tailscale (100.64.0.0/10 and fd7a:115c:a1e0::/48),
  so reaching it over Tailscale from away keeps working. `REHOME_ALLOW_PUBLIC=1` turns that off.
- Rehome's files with sign-in details (`sessions.json`, `license.json`) can now be read only by Rehome.
- Two ways a hostile Home Assistant setting could have put a fake link or overlay on the screen are closed: a "javascript:" address
  in Home Assistant's own URL setting, and a quote mark in a picture's address.

## 0.5.0
- **When an exact native look and accessibility disagree, accessibility wins** (the owner's rule): the light page's Turn On /
  Turn Off button, On/Off words on tiles, text never under 16 real pixels, rows and buttons at least 44, the Paste hint, error
  messages read out by VoiceOver, and names for every button.
- License page, old iPads (iOS 5–10): tapping Save Key right after pasting, while the key box still had focus, showed nothing:
  no "Saving…" and no red line for a wrong key, until the box lost focus. Save, Paste and Remove now let go of the box first.
- Standalone: the Docker health check follows `REHOME_PORT`, so a changed port no longer shows "unhealthy".
- Standalone: Settings → Use on Another iPad now has **Put Rehome on This iPad's Home Screen** (every guide points at it). It
  puts a setup code in this address and shows where Safari's Share button is.
- The sample home's "Demo…" line shows only over the faces and the Home Screen. It no longer covers the welcome's Continue
  (on a phone), a page's buttons, or Settings.
- A narrow tile (a phone) toggles from its top 55 %. Before, its wrapped name made a tap in the middle open the page.
- A real home's Home Modular Plus now has the sample home's look with the home's own things. Before, a home with twenty lights
  got a wall of bulb tiles. Now the top row is the thermostat or clock, the clock or weather, and the photo ("Add Photo Here"
  until there is one). Below are weather and Up Next or the Home tile, the camera or the two biggest rooms as one tile each,
  two scenes, and about six lights and devices: the ones that are on, locks and doors, then one per room. The rest stay in
  the Home app.
- Tile glyphs no longer rise to the top edge when a name in the row takes two lines.
- The Home app's scenes and unlit tiles were black on real iPads, because Safari can't blend through the page's scroll area.
  They are now plain see-through glass in every browser.
- An area Home Assistant named "Living Room (2)" joins "Living Room".
- The Home Screen's Photos widget shows the photos added to Rehome. With none, it says "Add Photo Here" and a tap adds one;
  the face's photo tile uses the same words.
- Home Assistant 2026.2 renamed Add-ons to Apps: every place that sends you there now says **Settings → Apps** (Add-ons on older
  Home Assistant), in the License page, Use on Another iPad, the server's messages, DOCS, README and STANDALONE.
- Security:
  - Rehome's pages now refuse any script that isn't Rehome's own (a Content-Security-Policy), and picture addresses from Home
    Assistant are escaped everywhere they're drawn.
  - The add-on passes on only the Home Assistant messages the dashboard uses. It never passes on calls that change Home
    Assistant itself (restart, add-ons, backups, users, scripts that run code).
  - Pairing: each device gets its own lockout after wrong codes, and only local addresses are accepted.
  - Pairing codes and the license key accept only requests from Rehome's own page.
  - Pictures are served only as pictures, and picture paths can't climb out of Home Assistant's picture addresses.
  - The live connection to Home Assistant accepts only Rehome's own page (another website opened on an old iPad can't use it).
- **Settings → Privacy:** what Rehome sends (made from the code that sends it), every outside connection with its time,
  address and size, and what an iPad can and can't do through Rehome. The welcome says it in one line. DOCS explains how to
  watch it yourself.
- A shorter first-run welcome: what Rehome does, then the setup steps. An arrow points at Safari's Share button for Add to
  Home Screen.
- A "Swipe up for apps" hint, if nobody has opened the Home Screen in the first minute.
- One Timers app with World Clock, Alarms and Timers tabs (it was three apps).
- Intercom and Messages are removed: the Intercom tile and app, Settings → Displays and the Messages app are gone. A saved
  layout or Home Screen that had them drops them. To ask Home Assistant something, hold the top of a face or tap the waveform
  in Control Center.
- Homes that lack things say so: "Weather Unavailable", "No Calendar", "No Lists", "No speakers in Home Assistant". The
  Thermostat app shows only with a thermostat.
- Setting up an old iPad no longer needs a second device at hand:
  - **Use on Another iPad → Make a Setup Sheet:** the address and a code in big letters (and a QR code), to print or keep on
    screen. The code works once, for 7 days.
  - The add-on's Log tab shows a code for the first iPad on its first start.
  - In Home Assistant's sidebar, **Put Rehome on This iPad's Home Screen** opens Rehome full screen in Safari, ready to add to the
    Home Screen; opened from its new icon it sets itself up.
- Rehome's own server for Home Assistant without add-ons (Container or Core, e.g. on a Raspberry Pi): Docker, step by step in
  docs/STANDALONE.md.
- License page: plain steps, a Paste button, the key found in whatever is pasted, a clear red message under the field, "Buy
  Rehome", and "Rehome is now using your home" after the restart. Rehome License is the first row in Settings.
- Display: **Style**, Liquid Glass or Flat (solid tiles and panels, no blur).
- Photos: a clear "Add Photo Here" when there are none; photos are made smaller on the iPad before they're sent (much faster),
  with real progress; three big buttons to add them; on Rehome's own server they're kept with its data.
- A real home starts on Home Modular Plus, with the same faces as the sample home. The sample Home Modular Plus matches the
  owner's own wall iPad at every screen size, with one photo.
- No face flashes before the welcome on a first open.
- The light page has a Turn On / Turn Off button.
- Sample music uses made-up songs and artists.
- Settings: "Add an Old iPad" is now "Use on Another iPad", with a line saying what it does. Performance is gone (developers:
  `?dev=1`). The Rehome icon in Settings is fixed. Help text is larger and darker.
- Updates reach iPads on the next load (every script and style address carries its own stamp).

## 0.4.0
- License key: paste it in Configuration → License key. Without a good key Rehome shows the sample home with one quiet line
  saying why, and switches to your home by itself once the key checks out. The add-on checks the key at start and weekly
  (the key and a random install id only), and keeps working for six weeks without a connection.
- Friendly names and descriptions for the add-on's options.

## 0.3.0
- Settings, like iPad Settings: Home Assistant, Display (glass, Reduce Motion), Music, Performance and About. Control Center's
  Wi-Fi button opens it.
- Music, following the shared spec (MUSIC-ACCOUNTS.md v1): Home Assistant's speakers, Music Assistant first; one Now Playing for
  Control Center and the Modular music tile, with only the controls each speaker supports; Settings → Music with every
  service's state; Connect opens Home Assistant's own Spotify setup; "Sign In on Your Phone" shows a QR code to your Home
  Assistant. The add-on stores no music sign-ins.
- The Modular music tile now follows changes as they happen.

## 0.2.0
- Classic mode for iPads on iOS 5–10 (the first iPad, iPad 2, 3, 4 and the first iPad mini): polyfills, the 2009 flexbox
  syntax, flat wallpaper-tinted glass, compositor-run motion, glass pictures baked in advance, immediate taps.
- Home Assistant over plain HTTP (bridge/open, send, poll) where websockets are too old, and automatically when one never opens.
- The pairing page works on old Safari; the Home Screen icon loads before pairing.
- Faster rearranging and dimming in both modes (reflow only on a new cell, one update per frame).

## 0.1.0
- First version: Home Modular, Home Modular Plus and Modular faces, the Home app, light / shade / fan pages, the thermostat,
  Control Center, rearranging (hold 1 s), sizes S/W/M/L, rows, Change… and suggested layouts, Assist intercom.
