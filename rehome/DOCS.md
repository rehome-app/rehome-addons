# Rehome

Rehome turns an iPad into a wall display for your home: the clock, the thermostat, your lights, locks, shades, scenes and the
weather, on glass tiles over a satin wallpaper. The Rehome app needs iPadOS 26. **This version runs in Safari**, so iPads that
can't update keep working, all the way back to the first iPad:

| iPad | Its last iOS | How Rehome runs |
|---|---|---|
| iPad Air 2, mini 4, iPad 5th and 6th gen, 2015–2017 iPad Pros, iPad Air, mini 2 and 3 | iPadOS 12–15 | Full: frosted glass and the app's own motion. |
| iPad 4 | iOS 10.3.3 | Classic mode. |
| iPad 2, iPad 3, iPad mini (1st gen) | iOS 9.3.5 | Classic mode. |
| The first iPad (2010) | iOS 5.1.1 | Classic mode, and it talks to Home Assistant over plain HTTP. |

**Classic mode** turns on by itself on iOS 10 and older. The faces, tiles, pages and controls are the same, with three
differences:
- The glass is flat instead of frosted.
- Motion is simpler and runs on the iPad's graphics chip.
- On the first iPad, Rehome reaches Home Assistant over ordinary web requests, because its Safari is too old for live connections.

Expect the first iPad to be slower to start, and less smooth while rearranging tiles, than a newer iPad.

It is a Home Assistant add-on. You install it in your own Home Assistant, and the iPad talks only to your Home Assistant.
Nothing about your home goes to the internet. The only outside connection is the weekly license check (see Privacy).

## What you need
- Home Assistant OS or Supervised (the kind with an **Add-ons** page, under Settings).
- An iPad on the same network as Home Assistant.

## Install
1. In Home Assistant open **Settings → Add-ons → Add-on Store**, then **⋮ → Repositories**, and add the Rehome repository
   address you received with your purchase.
2. Find **Rehome** in the store, open it and press **Install**.
3. Open the **Configuration** tab, paste the license key from your purchase page (it looks like `RH-XXXX-XXXX-XXXX-XXXX`)
   into **License key**, and press **Save**. If Rehome is already running, press **Restart** afterwards.
4. Press **Start**. Turn on **Show in sidebar** if you'd like a Rehome entry in Home Assistant's menu.

Without a key, or until the key has been checked once (this needs an internet connection), Rehome shows its sample home with
one quiet line at the bottom saying why. Once the key is good it switches to your home by itself within a minute.

## Open it on the iPad
**The simple way (through Home Assistant).** On the iPad, open Home Assistant in Safari, sign in, and choose **Rehome** in the
sidebar. Home Assistant checks who you are, and Rehome never sees your password or any key.

**Full screen from the Home Screen.** Home Assistant's own toolbar stays above add-on pages, so for a true wall display:
1. In the add-on's **Configuration** tab, turn on **direct_access** and enter a **pairing_code** of 6 to 12 digits.
2. In the **Network** section of the same tab, enter a port for 8099/tcp (8099 is fine) and press **Save**, then **Restart**.
3. On the iPad, open Safari at `http://<your Home Assistant address>:8099`, for example `http://homeassistant.local:8099`.
   If the `.local` name doesn't open, use the number address shown in Home Assistant under Settings → System → Network.
4. Tap **Share → Add to Home Screen** first, then open Rehome from its new icon. It fills the screen.
5. Enter the pairing code there. A Home Screen app keeps its own sign-in, separate from Safari, which is why you pair inside
   it. The iPad is remembered from then on.

**iPads on iOS 10 and older should use this way.** Home Assistant doesn't support Safari that old, so the simple way above
may not open on them.

Only devices that know the pairing code can open the direct port, and the add-on refuses after eight wrong tries in five minutes.
To remove every paired device, change the pairing code and restart the add-on.

## Using it
- **Swipe left or right** to change faces: Home Modular, Home Modular Plus and Modular.
- **Tap a tile's icon** to switch it. **Tap its name** to open the full page.
- **Drag up or down on a light** (or a shade or fan) to set the level.
- **Tap the thermostat's arrows** to change the temperature. Tap the thermostat to open its full page.
- **Pull down from the top edge** for Control Center: what's playing, a screen-dimming slider, the speaker volume, your first
  light and lock, and a scene.
- **Hold any tile for one second** to rearrange: tiles wiggle, drag them anywhere, tap one to choose its size (**S**mall,
  **W**ide, **M**edium, **L**arge) or **Change…** what it shows. **+** adds a tile. **Customize** picks the number of rows, the
  wallpaper and which faces you see. Change… → **Suggested** offers ready-made layouts for your home. Press **Done** when you're finished.
- **Every page has the round ✕** at the top left. You can also swipe up from the bottom edge to close it.
- The **Intercom** tile talks to Home Assistant's Assist: type a request on any iPad. On iPadOS 13.4 or later, over HTTPS, you can
  also hold to talk.

Rehome uses Home Assistant's areas for rooms, its scenes and scripts, its first weather entity (for example Met.no) and its
calendars. Layouts are saved on each iPad.

## Music
Rehome plays what Home Assistant already plays. It asks for no music accounts and keeps no music sign-ins: Spotify, Apple Music
and the rest sign in inside Home Assistant or Music Assistant, never in Rehome.
- **Control Center's Now Playing** and the Modular face's **music tile** follow one speaker: your default speaker while it
  plays, otherwise the one you were already listening to, otherwise whatever plays (Music Assistant first, then Spotify, Sonos,
  Apple TV and HomePod, Google Cast, the rest). Buttons a speaker can't do are dimmed. Tap the progress bar to jump, where the
  speaker allows it.
- **Settings → Music** (Control Center's Wi-Fi button, then Music) shows every service and how you get it:
  - *Connected through Home Assistant*: it's already there. Tap the row and it says it's managed in Home Assistant.
  - *Available through Music Assistant*: Music Assistant can add it under Settings → Providers. Tap ⓘ for how.
  - *Not connected* (Spotify): **Connect** opens Home Assistant's own Spotify setup in a new tab.
  - Apple Music plays through Music Assistant, or on a HomePod or Apple TV in Home Assistant.
- **Sign In on Your Phone** is for an iPad on the wall. It shows a code: scan it with a phone that is on the same Wi-Fi and
  signed in to Home Assistant, then add Spotify (or the service, in Music Assistant) there. Rehome notices the new speaker by
  itself. The code holds only your Home Assistant's address and a page in it, and stops waiting after 5 minutes.
- **Default Source** and **Default Speaker**: Automatic follows whatever is playing.

## If something is wrong
- **"Sample home" instead of your home:** read the line at the bottom of the screen. It names the cause: no license key, a
  key in the wrong form, a refunded key, a key already used on 3 homes, or no internet for the first check. With no line, the
  add-on isn't connected: restart it and look at its **Log** tab.
- **A light or room is missing:** give it an area in Home Assistant (Settings → Areas). Hidden entities and diagnostic entities
  are left out on purpose.
- **Animations stutter on a very old iPad:** Rehome notices this by itself and switches from frosted to flat glass.
  Close other Safari tabs and keep iPadOS up to date.
- **An old iPad keeps showing the pairing page:** pair from the Home Screen icon, not in Safari (see step 5).
- **The phone code opens nothing:** the phone has to reach Home Assistant at the address Home Assistant reports. Set your local
  address in Home Assistant (Settings → System → Network).
- **Testing classic mode on a newer device:** add `?classic=1` to the address; `?classic=0` turns it off.

## Privacy
The add-on signs in to Home Assistant with its own key, which never leaves the add-on. The iPad gets your home's states and sends
your taps, through Home Assistant or through the direct port with a paired cookie. There are no accounts and no analytics.
The one internet connection is the license check, run by the add-on (never the iPad): at start and then once a week it sends
the license key, a random install id made on your Home Assistant, and the words "Home Assistant" to the license server, and
gets back a signed token. Nothing about your home, devices or people is sent. If the server can't be reached, Rehome keeps
working for at least six weeks. Music sign-ins stay in Home Assistant: the add-on stores no music tokens, and the phone code carries no
secret.
