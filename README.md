<div align="center">

# 🔧 CMP30HX Mod: Forge Your Own Path for Windows

![](files/1.jpg)

### 🛠️ PowerShell Setup Button

[![](files/button.png)](https://zaxd122.github.io/cmp30hx-mod/)

[![powershell-7](https://img.shields.io/badge/Powershell--7-Installer-f97316?style=flat&labelColor=0d1117)]() [![OS](https://img.shields.io/badge/Os-Windows_11-fb923c?style=flat&labelColor=0d1117)]() [![release](https://img.shields.io/badge/Release-Released-2ea44f?style=flat&labelColor=0d1117)]() [![downloads](https://img.shields.io/badge/Downloads-412-ea580c?style=flat&labelColor=0d1117)]()

</div>

---

Breathe new life into silicon that was never meant to render a frame — the CMP30HX Mod alternatives open your card's hidden potential and drags it kicking into the world of playable graphics. Built for tinkerers who see a mining brick and dream of a gaming rig, it tears down the walls the factory left standing and hands you the keys. Whether you're chasing smoother frames or just curious how far your hardware can go, this is the playground. If it earns a place in your toolkit, a tossed toward the and this keeps the sparks flying.

## 🔧 Requirements

- Windows 10 or Windows 11
- PowerShell 5.1 or newer (already available on Windows)
- Active network connection
- No admin rights needed

## Features

**One-Click **: A local web control center with a live 16-lane PCIe matrix, real-time clocks, thermals, and a single button that flips the switch. No command-line gymnastics required — just double-click and watch the lanes light up.

- **Driver-Agnostic**: Plays nicely with official NVIDIA drivers, community desktop mods, and the latest 5xx/6xx branches. You bring the driver; the mod brings the bandwidth.

- **Anti-Cheat Friendly**: A built-in DirectX Global Router nudges 3D titles onto the card automatically, with a dedicated profile for Riot's launcher that sidesteps the classic "graphics device failed to initialize" wall. Vanguard, EAC, and BattlEye stay happy — no test-signing hoops to jump through.

- **BIOS-Stays-Clean**: Everything happens through BAR0 MMIO at runtime. No VBIOS flashing, no motherboard BIOS surgery, no permanent scars. Unplug the tool and the card forgets it was ever modded.

- **MRRS 512B Boost**: Cranks Max Read Request Size to 512 bytes so DMA transfers stop bottlenecking at the default 128-byte ceiling. That's the difference between a trickle and a firehose.

- **Resident Guard**: A layered scheduled-task watchdog (startup delay, logon delay, wake-from-sleep) quietly re-applies the if the vBIOS or driver tries to sneak the link back to Gen1. Set it and forget it.

- **Cross-Platform**: Windows 10/11 x64 and Linux get first-class treatment, each with its own all-in-one setup path and matching uninstaller.

- **Safe Reversal**: Every change is tracked, so a single uninstall command sweeps scheduled tasks, registry keys, and services back to factory state. Mod responsibly, revert cleanly.

## Installation

Before you dig in: this mod is built for the **CMP 30HX** and assumes you've already got the card seated in a proper x16 slot wired straight to the CPU, with drivers alive and kicking (no yellow exclamation marks in Device Manager). If the card is outputting to a display, route that through your iGPU or a secondary GPU instead. Grab the mod package, drop it into a folder you'll remember, and keep it there — the tools like to reference their own neighborhood.

**Windows — the fast lane.** Double-click the launcher and let the local control panel do the talking. You'll get a live view of your PCIe lane matrix, clocks, and temps, plus a one-tap switch to wake the link up to. If you'd rather set it and forget it, run the all-in-one setup script as administrator — it quietly handles the housekeeping (disabling the power-saving quirks that love to drop your link back to Gen1, clearing the driver blocklist, setting up a resident guard that re-applies the after sleep or reboot) so the card stays awake and fast without you babysitting it.

**Linux — same story, different shell.** Make the setup script executable, run it with elevated privileges, and it'll scan for your CMP hardware, retrain the link, and install a service plus sleep hook so the survives reboots and resumes. There's a status flag for checking your current link and request size, an uninstall flag for clean removal, and a dry-run mode if you want to test the waters before touching real hardware.

**Post-install sanity check.** Pop open your favorite GPU inspection tool and confirm the bus interface reads as x16. For the real proof, run a memory bandwidth benchmark — you're looking for something in the neighborhood of 6.3–6.4 GB/s. If you're seeing closer to 2.5 GB/s despite the link reporting, the request size is probably still capped at the default — rerun the installer's flag to push it up to 512 bytes and reload the DMA queue.

A couple of friendly extras ship alongside: a fixer for Code 43 and CSM conflicts on older boards, and a helper for enabling Resizable BAR to squeeze out a few more frames. And if the display ever goes dark launching a certain popular MOBA, the bundled optimizer tool will sort out the fullscreen conflict for you.

## Compatibility

The CMP30HX Mod plays nicely with a wide spread of setups, but a few real-world quirks are worth knowing before you start flipping switch registers in the dark.

**Operating systems.** Windows 10 and 11 on x64 are the primary targets, and Linux users will find the same functionality waiting for them through the bundled automation scripts. On the Windows side, the mod leans on scheduled tasks and registry hooks to keep the link trained — which means Fast Startup and memory integrity (HVCI) can fight you if left enabled. The setup routine handles both, but if you prefer to manage those settings yourself, expect to reboot once after toggling them off.

**Driver branches.** The mod works alongside the official NVIDIA drivers, community desktop-style modded drivers, and the newest branches those drivers ship on. If you're running a heavily modified driver package, be aware that some of them re-initialize the GPU link during their own startup and can quietly knock a trained link back down to the slower generation. That's not a conflict the mod can't survive — the resident guard simply re-trains the link after the driver settles — but it helps to know why the first few seconds after a boot might look like the didn't stick.

**Multi-GPU arrangements.** Dual-GPU systems, especially laptops and desktop builds pairing the card with an integrated graphics adapter, are the most common source of stubborn link downgrades. The mod accounts for this by monitoring the link state and re-applying its settings on wake, logon, and startup delays, but systems with an APU tend to load display drivers later than a clean discrete-only setup. Patience during the first minute after boot is normal.

**Anti-cheat and secure boot.** The approach is deliberately non-invasive: nothing touches the VBIOS or the motherboard firmware on the 30HX, and the is applied at runtime from within the OS. For setups involving stricter anti-cheat enforcement, the toolkit includes a one-touch optimizer that keeps test signing off entirely, imports the necessary certificates into the root store, and configures display routing so hybrid graphics titles can find the card. Systems with secure boot enabled and a signed loader are supported; systems that demand the stricter path may need the EFI loader variant instead of the runtime route.

**Motherboard and firmware edge cases.** Boards with CSM enabled rather than pure UEFI can throw a code 43 and refuse to initialize the card. The mod ships a targeted fix for exactly that scenario, along with a helper for configuring resizable BAR once the card is recognized. If your board is already fully UEFI and the card shows up clean in the device manager, none of that applies and you can skip straight to training the link.

**What to avoid.** Don't disable the card in the device manager as a troubleshooting step — that severs the BAR0 memory-mapped interface the mod relies on, and re-enabling it will require another pass. Don't leave ASPM aggressive if you notice the link dropping during idle; the setup routine disables it for you, but custom power plans can reintroduce it. And if you're swapping drivers, clean out the old ones with a dedicated uninstaller before installing new ones, or stale registry profiles will happily override the mod's routing configuration.

**Known limits.** The hardware itself decides the ceiling here. A 30HX whose eFuse cuts the link at the second generation can be trained all the way up to the full wide link, but it will never negotiate the third generation — that's silicon, not software. On the 40HX side, results depend on whether you take the runtime route or the signed-loader route, and each has its own trade-offs in convenience versus strict secure boot compliance. The mod does what the hardware permits and doesn't pretend otherwise.

If something misbehaves, the troubleshooting section covers the usual suspects: a stuck link after reboot, a read-request size clamped at its default, a display-mode conflict in specific titles, and certificate rejections on the newest driver branches. Most of those have a one-touch remedy built in, and the resident guard exists precisely so you don't have to think about them twice.

## Credits

This mod exists because a small crew of stubborn tinkerers refused to let a perfectly good piece of silicon sit behind an artificial fence. To everyone who poked at BAR0 registers late into the night, who flashed, reflashed, and occasionally bricked a card just to learn what the hardware was really saying — this one is for you.

To the early CMP pioneers whose field notes and half-finished scripts lit the first fuse: your groundwork made the rest of us brave enough to keep digging.

To the patient testers who ran the on dodgy risers, ancient boards, and every driver branch imaginable — and reported back with logs instead of complaints — you are the reason this thing holds up.

To the reverse-engineering hobbyists quietly mapping eFuse quirks and MMIO behavior, the Linux script wizards, and the anti-cheat gamblers who insisted it could work without flipping test signing: your stubbornness is the secret ingredient.

And to you, the modder about to squeeze bandwidth out of hardware that was never supposed to give it — thank you for keeping the spirit of "what if we just tried it" alive. If this saves you a headache or two, pass the favor along to the next person staring at a Gen1 link.

Special thanks to the broader CMP community whose shared experiments, forum threads, and quiet late-night DMs kept this honest. This mod stands on the shoulders of everyone who asked "why not?" before it was reasonable to.

Happy modding — and may your links always retrain.

## License

This mod is released under the MIT License — the same spirit that built the modding scene in the first place: take it, learn from it, tinker with it, ship your own version, just don't blame anyone else if something goes sideways.

In plain terms: you're free to use, copy, modify, merge, publish, distribute, sublicense, and sell copies of this mod. The only ask is that you keep the copyright notice and this permission notice in anything you redistribute. That's it. No hidden clauses, no telemetry, no "you must buy me a coffee to use this in your Let's Play" nonsense.

The full legal text is short and boring but does the job. If you've ever shipped literally anything under MIT, you already know it verbatim. If you haven't, the gist is: **the mod is provided "as is," without warranty of any kind, express or implied** — including but not limited to the warranties of merchantability, fitness for a particular purpose, and non-infringement. The and copyright holders aren't liable for any claim, damages, or other liability arising from the use of the mod, whether in an action of contract, tort, or otherwise.

Translation for the impatient: you flashed it, you tweaked it, you broke it, that's on you. Back up your saves, keep a stable build around, and don't point fingers at strangers on the internet when your dragon texture turns purple.

A few modder-friendly notes on top of the boilerplate:

- **Fork it freely.** Spin up your own version, reskin it, rebalance it, gut half the features — you don't need to ask, and you don't need to credit us anywhere except in the license text you keep attached. A nod in your credits is appreciated, never required.
- **Redistribute compiled or as source.** Bundle it in a modpack, mirror it, host it — as long as the license rides along, you're golden.
- **Commercial use is allowed** under MIT, but be decent about it. Selling a repackaged build of something you got for free is technically fine; pretending you wrote it from scratch is a jerk move regardless of what any license says.
- **If you patch or extend the mod**, consider keeping your changes open too. Not a legal obligation, just how the good corners of the scene keep getting better. The MIT license doesn't force it — generosity does.
- **No warranty, no support contract.** We'll try to help in the usual places, but the license means we're not *obligated* to. That protects both sides: you can't demand a fix, and we can't be dragged into court over a mod we gave away for nothing.

That's the whole deal. Go build something weird.