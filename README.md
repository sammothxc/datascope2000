# Northern Telecom Spectron Datascope 2000 Restoration Project

## 📜 Project Overview
This repository documents my ongoing restoration and reverse engineering of a **Northern Telecom Spectron Datascope 2000** ([sometimes branded by Telenex](https://www.ebay.com/itm/187154880690)), an early 1980s serial/network protocol analyzer.
While its original role of analyzing serial and network buses via DB-25 and RJ11 connectors is mostly obsolete, the hardware is so fascinating to me. Powered by a [Hitachi HD64180](https://en.wikipedia.org/wiki/Hitachi_HD64180) (a Z80-compatible CPU with extras), the system might be able to run [CP/M natively as shown by](https://en.wikipedia.org/wiki/List_of_computers_running_CP/M#:~:text=Micromint%20SB180%20(Hitachi%20HD64180%20CPU)) the HD64180-based [Micromint SB180](http://dunfield.classiccmp.org/mmint/index.htm). 

My goals are to:
- Restore the hardware to full working order
- Preserve and disassemble the original ROMs
- Explore writing my own software for the system and/or getting CP/M to run
- Share schematics, ROM dumps, disassembly, and findings publicly

and not release too much magic smoke from the original components in the process. This whole project may prove difficult as the internet can't dig up anything more than a singular ebay listing.

## 💾 Repository Contents
- `/rom_dumps` → binary ROM images from the various ROM chips
- `/disassembly` → disassembly listings and (one day) annotated source code
- `/schematics` → reverse engineered circuit diagrams and PCB layouts
- `/docs` → manuals, datasheets, and research notes
- `/photos` → pics of the hardware

## 🛠 Hardware Specifications

- **CPU:** 12MHz Hitachi HD64B180ROP (Z80-compatible, extended instruction set, MMU, built-in peripherals)
- **RAM:** 256k worth of Hitachi HM50256P-12 chips
- **ROM:** 64k Hitachi (notice a pattern) HN27512G-25 system ROM
- **VIDEO:** Amber monochrome | 640×250 pixels | 80×25 text | 256 bytes of video RAM | 64k character ROM
- **I/O:**
  - 5 inch [Computron 115DMX modular CRT](https://www.ebay.com/itm/264263815743?gQT=2) unit (found in industrial and military gear)
  - 36-key Front Panel with 3 function layers, including an alphabetical layer
  - 12 channel Bi-directional serial LED indicators
  - 3.5 inch floppy drive
  - 2x RJ11 (phone, modem)
  - 5x DB25 (comm, terminal, test, modem, and bus machine)
  - 1x GPIB (printer)
  - 1x BNC (video out)
- **Motherboard(s):**
  - Two 98 pin ISA-style logic boards on a backplane, one system card and one (mostly) video card
  - System card notable chips: HD64B180ROP CPU, FDC9266 floppy controller
  - Peripheral card notable chips: Zilog Z8440BPS SIO/O, Standard Microsystems CRT 5037 video controller, Intel P8253-5 programmable interval timer
  - Peripheral PCB traces appear to be fine copper wires hand-laid on the board (era appropriate PCB manufacturing process?)
  - 40 pin DIP socket for mystery add-on packages (for 3270 BSC, 3270 SNA, and X25?)

## 🔬 Technical Findings

- Currently only displays a thin horizontal line, indicating vertical deflection issue or VSYNC signal failure
- 60Hz VSYNC signal is clean at the video board output, but connecting the CRT loads the line heavily and corrupts the signal
- Multiple 7404 and 7406 logic inverters in the VSYNC path have failed; I've now socketed them for easy replacement
- Original ROMs are being read with an XGecu T48 programmer; compatible Winbond W27C512-45Z EEPROMs on hand for testing my own code in system ROM
- Video ROMs are 2532 chips, and aren't supported by my programmer but I am making an adapter board to hopefully read them soon

## 📅 To-Do

### Hardware
- [ ] Diagnose and repair the vertical deflection circuitry in the CRT unit
- [ ] Verify if the issue is isolated to the CRT logic board or the deflection yoke/drive circuits
- [ ] Test system functionality with a floppy emulator (time to dig out my trusty Gotek) to attempt CP/M boot

### Software
- [ ] Fully disassemble and the system ROM and locate starting memory address
- [ ] Identify I/O port map for HD64180 peripherals and external chips
- [ ] Dump and analyze other ROMs (2532 video ROMs, I'm looking at you)
- [ ] Write custom ROMs to have fun while learning assembly language

### Documentation
- [ ] Reverse engineer several programmable logic array ICs
- [ ] Draw up schematics for both system and CRT board, along with accurate PDB layouts
- [ ] Pull ROM images and upload annotated disassembly code to the repo

## 🤝 Contributions
If you’ve worked with:
- HD64180 assembly programming
- CP/M on Z80 and compatible hardware
- Vintage CRT repair (especially old Computron units)
- Or have manuals or schematics for this exact model…

…I’d love to hear from you! Issues, PRs, and shared knowledge are welcome.

---

_P.S. I love electronics but hate writing, so I had ChatGPT do the heavy lifting for most of the READMEs_
