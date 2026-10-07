# Hardware and wiring

This build uses two machines, but it doesn't have to. If you're starting from scratch, see [Running it on one machine](#running-it-on-one-machine) at the end.

## How it fits together

```
 GARAGE                                   KITCHEN
┌──────────────────────────┐            ┌──────────────────────────────┐
│ HP EliteDesk 800 G3 Mini │            │ Kiosk mini PC (in the wall)  │
│  Proxmox                 │   WiFi /   │  Windows 11                  │
│  └─ Home Assistant OS VM │◄──network─►│  Edge in kiosk mode          │
│  Zigbee dongle (USB)     │            │        │ video + USB touch   │
└────────────┬─────────────┘            │        ▼                     │
             │ Zigbee                   │  Prechen 21.5" touchscreen   │
             ▼                          │        ▲ power               │
   ┌───────────────────┐                │  Zigbee smart plug           │
   │ Motion sensor     │                │                              │
   └───────────────────┘                └──────────────────────────────┘
```

- **Home Assistant server** - runs everything: integrations, automations and the dashboard
- **Kiosk PC** - just a browser that shows the dashboard full screen
- **Touchscreen** - shows the dashboard and sends touch input back to the kiosk PC over USB
- **Smart plug and motion sensor** - turn the screen off when nobody's around

## Kiosk PC

| | |
|---|---|
| CPU | Intel Celeron J3455 |
| RAM | 8GB DDR3 |
| Storage | 128GB SSD |
| OS | Windows 11 |
| Network | USB WiFi dongle |

This was my old Home Assistant box. It only has to run a browser, so almost any mini PC from the last eight years will do. A fanless one is ideal because it's silent and it lives inside a wall.

**Why Windows?** Cheap portable touchscreens are hit and miss on Linux. With Windows, the touch and portrait rotation worked straight away, which was worth more to me than saving a licence. If you'd rather use Linux, check that your specific screen's touch works before you commit.

**Placement.** Mine sits in a recess in the boxing behind the screen, and the back panel of the frame has an opening so the cables can get through. Leave some air around it, because a mini PC sealed in a void will run hot.

**Network.** There's no ethernet at the wall, so the kiosk uses a USB WiFi dongle. It's only loading a dashboard, so WiFi is fine. If you can run a cable, do.

## Touchscreen

| | |
|---|---|
| Model | Prechen 21.5" portable touchscreen (HD-215), white |
| Where | [Amazon UK](https://www.amazon.co.uk/dp/B0GKCVGN1V) |
| Orientation | Portrait |
| Connections | Video, USB for touch, DC power |

<!-- TODO: add the exact video and USB cables you used -->

A few things to know about this screen:

- **Use the DC power adapter.** The touch layer draws too much for USB-C power alone, so plug in the supplied adapter.
- **Touch needs its own USB connection** to the kiosk PC, separate from the video cable.
- **Portrait is set in Windows.** Rotate the display in Windows Display settings. If taps land in the wrong place after rotating, run the touch calibration under Tablet PC Settings in Control Panel, so Windows maps touch to the right screen and orientation.
- **The rear has decorative RGB lights** that can't be switched off in the menu. Once it's in the frame you won't see them, but put a bit of tape over them if any light bleeds out.
- **The VESA mount is off-centre in portrait**, which is why I didn't use a wall bracket. See the [frame guide](02-frame-build.md#step-6---build-the-back-and-mount-the-monitor).

## Home Assistant server

| | |
|---|---|
| Machine | HP EliteDesk 800 G3 Mini |
| CPU | Intel Core i5-6500T |
| RAM | 8GB |
| Storage | 256GB SSD |
| Hypervisor | Proxmox |
| Home Assistant | Home Assistant OS as a VM |
| Zigbee | SONOFF ZBDongle-P MG24 |

Refurbished business mini PCs like the EliteDesk, Lenovo Tiny and Dell Micro are great value for this. They're small, quiet and low on power, and they're easy to find second hand.

Running Home Assistant OS in a Proxmox VM gives you snapshots before upgrades, and room to run other things alongside it.

**Two tips:**

- **Pass the Zigbee dongle through to the VM.** In Proxmox, add it to the Home Assistant VM as a USB device by vendor and device ID, not by port, so it survives a reboot or a move to a different port. Then set it up in Home Assistant with ZHA.
- **Use a DHCP reservation on your router** instead of setting a static IP inside Home Assistant. Reserve the MAC address of the VM's virtual network card, not the physical machine's.

## Turning the screen off automatically

Leaving a screen on 24/7 wears out the backlight and wastes power. So Home Assistant cuts power to the screen and brings it back when someone walks into the kitchen.

| Part | Job |
|---|---|
| SONOFF S60ZBTPG Zigbee smart plug | Switches the screen's power |
| SONOFF SNZB-03PR2 motion sensor | Detects someone in the kitchen |

How it works:

- The screen turns off overnight, and when the kitchen has been empty for a while.
- It turns back on when the motion sensor picks someone up.
- **Only the screen is switched, not the PC.** The kiosk PC stays on, so there's no boot wait and no risk of corrupting Windows by pulling its power.

The automation is in [`automations/screen-power-pir.yaml`](../automations/screen-power-pir.yaml).

**Plug in a few mains Zigbee devices.** Mains-powered Zigbee plugs act as routers and extend the network. This matters if, like mine, your coordinator is in the garage and the sensors are in the house.

## Power

The kiosk PC and screen need two sockets near the wall. I added a fused connection unit off an existing spur, feeding a short radial to two double sockets which sit inside the boxing (its a little snug).

In the UK, you can't take a spur off an existing spur under BS 7671, which is why the fused connection unit is there. **If you're not confident with mains wiring, get an electrician to do this part.**

## Running it on one machine

I've split this across two machines because I already had them. If you're starting from scratch, one is enough:

- **Proxmox on the kiosk PC**, with a Home Assistant OS VM and a lightweight kiosk browser alongside it. You'll want 8GB of RAM for this.
- **Or Home Assistant on a separate box you already own**, with the kiosk PC just running the browser, as I've done.

The J3455 ran my Home Assistant happily for years before I moved it, so even modest hardware will cope.
