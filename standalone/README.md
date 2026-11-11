# Rehome without the Apps page (Home Assistant Container or Core)

If your Home Assistant has no **Apps** page in Settings (called Add-ons before Home Assistant 2026.2), Rehome runs next to it in Docker, on the same
computer: for example a Raspberry Pi.

```
mkdir -p ~/rehome && cd ~/rehome
curl -fsSLO https://raw.githubusercontent.com/rehome-app/rehome-addons/main/standalone/docker-compose.yml
touch rehome.env
docker compose up -d && docker compose logs --tail 30
```

The log shows `pairing code for an iPad: 123456`. On the iPad, open `http://<this computer's address>:8099` in Safari, tap
**Share → Add to Home Screen**, open Rehome from the new icon and type the code. You'll see the sample home.

To show your own home, put your Home Assistant address and a long-lived access token in `rehome.env` (see
`rehome.env.example`), run `chmod 600 rehome.env && docker compose up -d`, then paste your key in Rehome under
**Settings → Rehome License**. Step-by-step help: https://userehome.com/pages/setup

## Updating

In the folder containing your Rehome Compose file, run:

```sh
docker compose pull
docker compose up -d
```

Keep your existing volumes and `rehome.env`; do not remove volumes or clear the iPad's browser data.
Once the new container is running, reload Rehome on each iPad, or fully close and reopen its Home Screen app.
Publishing a release does not automatically update a running Docker container.

For 24-hour time, open Rehome's **Settings > Display & Night > 24-Hour Time**. This choice is saved on each iPad.
