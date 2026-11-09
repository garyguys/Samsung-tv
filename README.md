# Making a slow Samsung UN55NU6900 usable again

**TV:** Samsung UN55NU6900FXZC (2018 NU6900 series, Canada)
**OS:** Tizen 4.0, software `T-KTSUAKUC-1350.7`

## Can we replace the TV's software?

No, not safely. Here's why, so you don't lose an afternoon (or the TV) trying:

- **The firmware is signed.** The TV only installs updates carrying Samsung's
  cryptographic signature. A custom build would be rejected, and forcing one on
  through the service port is the usual way these TVs get bricked.
- **The bootloader is locked**, and there's no public root or jailbreak for
  2018 Tizen TVs. That rules out Android TV, LibreELEC and "debloated Tizen".
- **The hardware is the real limit.** The NU6900 is Samsung's entry-level 2018
  model, with a low-power chip and little RAM. Even a perfectly clean OS
  would still feel sluggish running modern Netflix and YouTube apps.

The good news: the panel is fine. A 4K HDR picture from 2018 is still a good
picture. The slow part is the computer built into the TV, and you can swap that
out for $40–$200 without opening anything.

---

## Option 1 (recommended): Make the TV a "dumb" screen

Plug a streaming box into HDMI, take the TV off the internet, and never open
Smart Hub again. Everything gets faster at once, and the Samsung ads and
tracking go away because the TV can't reach the internet.

### Choosing a box

| Box | Approx. CAD | Bloat / ads | Notes |
|---|---|---|---|
| **Nvidia Shield TV** | $200+ | Low (with a custom launcher, see below) | Fastest, best for Plex/Kodi, gets updates for years |
| **Google TV Streamer** | ~$130 | Ads on home screen, removable with a launcher | Fast, every major app |
| **Amazon Fire TV Stick 4K / 4K Max** | $60–$90 | Heavy ads, launcher locked down | Cheap and quick, but Amazon pushes its own content |
| **Roku Streaming Stick 4K** | ~$60 | Some ads, very simple | Simplest remote and menus |
| **Apple TV 4K** | $170+ | Essentially no ads | Very fast and clean, best if you already use an iPhone |

**Fewest ads with every app:** Apple TV 4K, or a Google TV/Android TV box with
[Projectivy Launcher](https://play.google.com/store/apps/details?id=com.spocky.projengmenu)
set as the home screen. Projectivy replaces the ad-filled Google home screen
with a plain grid of your apps.

**Fully custom with no bloat at all:** a Raspberry Pi 5 or small mini-PC running
[LibreELEC](https://libreelec.tv/) (Kodi). It's great for your own media and
Plex/Jellyfin. The catch: Netflix, Disney+, Crave and similar services are
limited or unreliable there because of DRM, so most people pair it with one of
the boxes above.

### Setting up the TV once the box is plugged in

1. Plug the box into **HDMI 1** or **HDMI 2** and power it from its own adapter
   if it came with one. The TV's USB port is often too weak to power it.
2. **Take the TV off the internet:**
   `Settings → General → Network → Network Settings` and forget the Wi-Fi
   network or unplug the Ethernet cable. With no connection, the TV can't load
   ads, the Smart Hub banner or background updates.
3. **Stop Smart Hub from opening at power-on:**
   `Settings → General → Smart Features → Autorun Smart Hub → Off`
   and `Autorun Last App → Off`.
4. **Turn on HDMI-CEC** so the box's remote can turn the TV on and switch inputs:
   `Settings → General → External Device Manager → Anynet+ (HDMI-CEC) → On`.
   The TV then wakes up on the box's input and you can put the Samsung remote
   in a drawer.
5. **Turn on HDR/4K for that HDMI port:**
   `Settings → General → External Device Manager → HDMI UHD Color → On` for the
   port the box is in. Without it you won't get 4K HDR from the box.
6. Optional, for gaming consoles: `Settings → General → External Device Manager
   → Game Mode → On` on that input to cut input lag.

> **Tip:** Connect the TV to the internet briefly once or twice a year to
> install Samsung firmware updates (`Settings → Support → Software Update`),
> then disconnect it again.

---

## Option 2: Speed up the built-in software (no money spent)

If you'd rather keep using the TV's own apps, these steps make a noticeable
difference. Menu names are for 2018 models and may be worded a little
differently on your TV.

### 1. Cold boot it (the biggest quick win)
Samsung TVs don't really turn off; they sleep. Memory fills up over days and
everything gets slower.
- **Hold the power button on the remote** until the TV switches off and the
  Samsung logo appears again (about 5 seconds), **or**
- Unplug the TV from the wall for 60 seconds.

Do this whenever it starts to drag.

### 2. Turn off ads, tracking and voice listening
`Settings → Support → Terms & Policy`, then turn off or decline:
- **Viewing Information Services** (watches what's on screen to profile you)
- **Interest-Based Advertisement**
- **Voice Recognition Services** (if you don't use voice)
- Any other optional agreements listed

These services run in the background and use the same small processor your
apps need.

### 3. Stop things launching automatically
`Settings → General → Smart Features`
- **Autorun Smart Hub → Off**
- **Autorun Last App → Off**

### 4. Delete apps you don't use
On the home screen go to **Apps → Settings (gear icon)**, select each unused app
and choose **Delete**. Some preinstalled apps can't be removed. For those,
choose **Remove from Home** so they don't load tiles and previews.

### 5. Reset Smart Hub (clears the app cache)
`Settings → Support → Self Diagnosis → Reset Smart Hub`
The default PIN is **0000**. You'll need to sign back into your apps afterward,
but this clears out years of cached data.

### 6. Block Samsung's ad servers (optional, more technical)
If you run [Pi-hole](https://pi-hole.net/), [AdGuard Home](https://adguard.com/adguard-home/overview.html)
or [NextDNS](https://nextdns.io/) on your network, point the TV's DNS at it:
`Settings → General → Network → Network Status → IP Settings → DNS Setting → Enter manually`.
Their default blocklists cover most Samsung ad and telemetry domains. Block
carefully, because blocking too much can break app sign-ins or updates.

### 7. Picture processing that adds lag
These don't slow the menus, but they make the TV feel slow to respond:
- **Game Mode** on for consoles
  (`Settings → General → External Device Manager → Game Mode`).
- **Auto Motion Plus → Off** (removes the "soap-opera effect").

### 8. Factory reset (last resort)
`Settings → General → Reset` (PIN **0000**). This wipes everything back to how
it left the factory. After the reset, go through steps 2–4 **before** signing
into a Samsung account.

---

## Ad-free YouTube on the TV itself (advanced, optional)

The community project **[TizenBrew](https://github.com/reisxd/TizenBrew)** can
sideload modified apps such as **TizenTube** (YouTube with no ads or
SponsorBlock segments) through Samsung's Developer Mode. It's unofficial, so
check the project's README to see whether your Tizen version is supported, and
expect to redo it now and then after Samsung updates. It removes YouTube ads but
won't make the TV faster. A streaming box is still the better fix for speed.

---

## TL;DR

1. **Best fix:** buy a streaming box (Apple TV 4K, Nvidia Shield or Google TV
   Streamer with Projectivy Launcher for the least bloat), take the TV off
   Wi-Fi and turn off *Autorun Smart Hub*.
2. **Free fix:** hold the power button to cold boot, turn off everything in
   *Terms & Policy*, delete unused apps, and run *Reset Smart Hub*.
3. **Don't** try to flash custom firmware on this TV. It isn't possible and
   it's the fastest way to brick it.
