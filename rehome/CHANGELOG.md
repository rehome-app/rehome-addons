# Changelog

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
