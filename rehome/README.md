# Rehome for Home Assistant

Turn an old iPad into a wall display for your home: the clock, weather, lights, thermostat, scenes and more, on big glass
tiles that read from across the room. It runs in Safari, so iPads that can't update anymore keep working, all the way
back to the first iPad.

## Install

Rehome runs inside your Home Assistant. You install it once from your phone or computer, then open it on the iPad.

**1. Add it to Home Assistant** (phone or computer)

[![Add Rehome to your Home Assistant.](https://my.home-assistant.io/badges/supervisor_add_addon_repository.svg)](https://my.home-assistant.io/redirect/supervisor_add_addon_repository/?repository_url=https%3A%2F%2Fgithub.com%2Frehome-app%2Frehome-addons)

Press the button, then **Add**. Or in Home Assistant open **Settings → Apps (called Add-ons before Home Assistant 2026.2) → App Store → ⋮ → Repositories** and
paste `https://github.com/rehome-app/rehome-addons`.

Then find **Rehome** in the App Store, press **Install**, then **Start**, and turn on **Show in sidebar**.
It opens with a sample home.

**2. Add your key**

In the app's **Configuration** tab, paste your license key into `license_key`, press **Save**, then **Restart**.
Your own home replaces the sample home.

**3. Open it on the iPad**

On the iPad, open Home Assistant in Safari, sign in, and tap **Rehome** in the sidebar.

You need Home Assistant OS or a Supervised install (the kind with an Apps page in Settings, called Add-ons before 2026.2), on a 64-bit machine.

## License

Rehome is paid software. One key covers one household, with up to 3 Home Assistant installs and any number of screens.
Without a key it runs as a demo with a sample home. See [LICENSE](LICENSE).

Rehome is an independent product. It is not made by, affiliated with or endorsed by Apple, Home Assistant or Nabu Casa.
