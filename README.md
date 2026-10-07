# kitchen-kiosk
Skylight / Cozyla clone with Home Assistant functionality. 

![The finished panel](images/frame-finished.jpg)

My wife wanted a Skylight / cozyla calendar for the kitchen. So I built one instead.

This is a wall-mounted 21.5" touchscreen in a custom MDF frame, running a Home Assistant dashboard. It does what a Skylight does - family calendars, meal planning and chores - and doubles up as a control panel for the rest of the house.

The guides here cover everything: the hardware, the woodwork, the kiosk setup and the dashboard YAML.

## What it does

**The Skylight bits**
- **Family calendar** - a Google Calendar for each of us plus a shared family one, showing the next few days at a glance
- **What's for Dinner** - a weekly meal planner that can be updated from a phone
- **Chores** - the kids' jobs are gamified with [TaskMate](#), so they earn points and can see their scores and daily progress live on the screen

**The smart home bonus**
- Banner image of the house that swaps between day and night scenes, with the clock and weather overlaid
- Solar, battery and grid usage
- Heating and hot water control
- EV charger mode and status
- Car battery and climate controls (PIN-protected)
- Battery levels for the doorbell and robot hoover
- Bottom navigation between Home, Calendar and Jobs pages

## Costs

| Item | Cost |
|---|---|
| Prechen 21.5" portable touchscreen ([Amazon UK](https://www.amazon.co.uk/dp/B0GKCVGN1V)) | ~£100 |
| Used mini PC | £40 (Facebook Marketplace) / ~£70 (eBay) |
| 6mm MDF sheet | ~£14 |
| **Core build total** | **~£155-185** |

Optional extras for automatic screen on/off:

| Item | Cost |
|---|---|
| SONOFF ZBDongle-P MG24 Zigbee coordinator | ~£20 |
| SONOFF SNZB-03PR2 motion sensor | ~£14 |
| SONOFF S60ZBTPG Zigbee smart plug | ~£10 |

Glue, filler, paint and screws not included. All the software is free.

## Hardware

**Kiosk PC** - hidden in the boxing behind the screen
- Fanless mini PC: Intel Celeron J3455, 8GB DDR3, 128GB SSD
- Windows 11, with Edge in kiosk mode loading the dashboard on boot
- USB WiFi dongle, as there's no ethernet at the wall

**Home Assistant server** - in the garage
- HP EliteDesk 800 G3 Mini: i5-6500T, 8GB RAM, 256GB SSD
- Proxmox, with Home Assistant OS running as a VM

**Screen**
- Prechen 21.5" touchscreen (HD-215), white, mounted in portrait
- Screwed straight onto the MDF back plate of the frame, which hangs on the wall on keyhole slots - no VESA bracket needed
- Powered through a Zigbee smart plug, so Home Assistant cuts power overnight and a motion sensor wakes it when someone walks in. This saves the backlight as well as electricity.

### You only need one machine

I've split this across two machines because I already had them, but you don't need to. You could run everything off the PC behind the screen - for example, Proxmox with a Home Assistant VM alongside a lightweight kiosk browser. The J3455 ran my Home Assistant happily for years, so even modest hardware will cope.

## Software

**HACS cards**
- [bubble-card](https://github.com/Clooos/Bubble-Card) - navigation and pop-ups
- [clock-weather-card](https://github.com/pkissling/clock-weather-card)
- [card-mod](https://github.com/thomasloven/lovelace-card-mod) - styling, and the day/night banner swap
- [kiosk-mode](https://github.com/NemesisRE/kiosk-mode) - hides the header and sidebar for the kiosk user
- [browser_mod](https://github.com/thomasloven/hass-browser_mod)
- [lovelace-pin-lock-card](https://github.com/qlerup/lovelace-pin-lock-card) - PIN protection for the car controls
- TaskMate - chores and points

**Integrations used on the dashboard**
- Google Calendar
- GivTCP (GivEnergy inverters and batteries)
- Octopus Energy
- myenergi (Zappi)
- Nest
- Tesla Fleet API
- Ring
- Roborock
- Met.no
- ZHA (Zigbee)

You don't need all of these. Each card file in `dashboard/cards/` lists what it depends on, so you can pick the parts that match your house.

## Guides

1. [Hardware and wiring](docs/01-hardware.md)
2. [Building the frame](docs/02-frame-build.md)
3. [Setting up the kiosk](docs/03-kiosk-setup.md)
4. [The dashboard](docs/04-dashboard.md)

## Repo layout

```
ha-kitchen-skylight/
├── README.md
├── docs/
│   ├── 01-hardware.md
│   ├── 02-frame-build.md
│   ├── 03-kiosk-setup.md
│   └── 04-dashboard.md
├── dashboard/
│   ├── full-dashboard.yaml
│   └── cards/
├── automations/
│   └── screen-power-pir.yaml
└── images/
```

## Lessons learned

A few things that cost me time, so they don't cost you any:

- **Avoid `config-template-card` for background images.** It rebuilds the whole card on every entity update, so the image reloads and flickers. Swapping the background with card-mod CSS over a transparent placeholder PNG is smooth.
- **Load card-mod as a frontend module** in `configuration.yaml`. Otherwise styling can fail to apply on first load in a kiosk browser.
- **`tile` and `vertical-stack` cards can't go directly inside `picture-elements`.** Wrap them in `custom:hui-element` with `card_type:`.
- **Give the kiosk its own non-admin user** and apply kiosk-mode to that user only. Add `?disable_km` to the URL if you need to get back into edit mode.
- **Use a DHCP reservation on your router** rather than a static IP inside Home Assistant. It survives VM rebuilds. On Proxmox, reserve the virtual NIC's MAC address, not the physical one.
- **Package files and `configuration.yaml` changes need a full restart**, not just a YAML reload.

## Licence

MIT - use whatever is useful. If you build one, I'd love to see it!
