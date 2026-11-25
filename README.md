# Modular Stage Pedalboard

Engineering documentation, schematics, PCB layout specifications, and Bills of Materials (BOM) for a modular, SELV-powered (`18V DC`) guitar pedalboard. Includes KiCad 10 specifications, 50 monochrome SVG circuit diagrams, mechanical standards for 19" rack rails and casemaker enclosures, a 44-cable Molex harness map, 16 core effect modules, 23 swappable reference modules, and consolidated/unit BOMs.

> **Language Note:** The underlying project documentation, circuit notes, and appendices are written primarily in **Swedish** (using standard international electronic component designations and part numbers).

---

## ⚠️ Disclaimer & Limitation of Liability

This project is provided **"as is"**, without warranty of any kind, express or implied. All schematics, PCB layouts, mechanical drawings, calculations, and Bills of Materials (BOM) are shared for educational and DIY reference purposes only.

* **No Guarantee of Accuracy:** Designs, component ratings, power budgets, thermal calculations, and pinouts may contain errors, omissions, or unverified sections (specifically noted as unreviewed).
* **User Responsibility:** It is strictly the **user's own responsibility** to independently verify all circuits, manufacturer datasheets, voltage/current ratings, pinouts, mechanical clearances, and electrical safety requirements before ordering components, manufacturing PCBs, or assembling hardware.
* **Limitation of Liability:** The author assumes **no responsibility or liability** for any damage to equipment, components, amplifiers, power supplies, personal injury, or any other loss resulting from the use, modification, or construction of these designs. Build and use at your own risk.

---

## Project Status & Critical Safety Notes

* **Work in Progress:** Schematics and PCB layouts are actively being finalized and verified in KiCad 10.
* **Unreviewed Reference Library (Chapter 12B):** The 23 swappable reference modules (including the transformerless active balanced DI) have **not yet been verified against component datasheets**. Do not build or order parts from Chapter 12B without performing a complete datasheet and node audit first.
* **SELV Power Architecture:** Powered exclusively by an external regulated `18V DC` center-negative power supply (`RockPower RP NT 19 EU`, `2000 mA`). There is **no `230V AC` mains voltage or protective earth (`PE`)** inside the enclosure.
* **Center-Negative Jack Requirement:** Because the external `18V DC` barrel plug carries `+18V` on the outer sleeve, an **isolated plastic DC jack** (`Switchcraft 722A` with insulating washer or `Würth 694106301002`) is mandatory to prevent shorting against the conductive shielding tape.
* **Shielding Ground:** Internal copper/aluminum EMI shielding tape is star-grounded via separate `≥ 0.75 mm²` wires to an `M4` `0V` chassis ground bolt (`< 0.1 Ω`), maintaining `≥ 4 mm` clearance (plus `1–2 mm` acrylic/plexi insulation) from PCB undersides and heatsinks.

---

## System Architecture

### 1. Mechanical Standard (19" Rack Rail & Casemaker)
* **Grid System:** Based on standard 19" rack unit increments (`1U = 44.45 mm`).
  * **Standard Effect Module:** `2U × 3U` (`88.9 × 133.35 mm`) on flat `2 mm` aluminum faceplates, strictly one effect per module with upright controls and `30 mm` toe clearance to the footswitch.
  * **Graphic EQs:** 7-Band EQ (`2U × 3U`), 10-Band EQ (`4U × 3U` / `177.8 × 133.35 mm`).
  * **Utility Switches (ABY, Mute, Bypass, Tap):** `1U × 1U` (`44.45 × 44.45 mm`).
* **Rails & Spacers:** Horizontal `Adam Hall 6161` rack rails mounted on crossbars using `DIN 7985 M6` screws and nylon cup washers (`~6.0 mm` stack). Mandatory `6.5–7 mm` spacers are used under all module mounting points (`22.2 mm` from side edges / `44.45 mm` center-to-center) to keep faceplates completely flat.
* **Enclosure:** `7–9 mm` birch plywood in extruded casemaker aluminum profiles with a `10°` wedge angle (`50 mm` front height rising to `133.8 mm` rear height over a `19"` / `482.6 mm` hypotenuse).
* **Four Standard Board Sizes:**
  1. **Loop Board:** 1 row, `10U` width (5 time/modulation modules, no volume rocker).
  2. **Front Board:** 1 row, `10U` width + Volume rocker.
  3. **Medium Board:** 2 rows, `12U` width (12 modules) + Wah & Volume rockers.
  4. **Large Board:** 2 rows, `16U` width (16 modules) + Wah & Volume rockers.

### 2. Power Distribution & Filtering
* **Input & Protection (Sheet 1):** External `18V DC` (`2000 mA`) → isolated `2.1 × 5.5 mm` plastic jack → strain-relief hook → `1.1A` resettable PTC fuse (`Bourns MF-R110`) → main DC toggle switch → `1N5819` (`40V`) reverse-polarity Schottky diode (`~+17.65V` under load).
* **Two-Stage LC Filter (Sheet 2):** Passive π-filter (`470µF/35V` + `100nF` + `100µH 5A` toroid inductor + `470µF/35V` + `100nF`) producing `+18.0V_CLEAN` with zero regulator heat. Feeds a `500 mA` PTC main trunk (`MF-R050`) to the `9.7V` regulator and three `100 mA` PTC branches (`MF-R010`) for `10-EQ`, `7-EQ`, and `Acoustic Preamp / 18V Aux`.
* **9.70V Regulation & Active VREF (Sheet 5):** `LM317T` (with isolated TO-220 heatsink and `1N5817` protection diodes) steps down to `+9.70V DC`. A buffered `TL072` divider provides an active `~+4.75V` virtual ground (`VREF`).
* **16-Channel Distribution (Sheet 6):** 16 individually fused 4-pin Molex outputs (`15 × 100 mA` PTC + `1 × 200 mA` PTC on `J11` for the Belton Reverb).
* **Analog LED Dimmer:** Linear, PWM-free voltage follower (`+2.5V` to `+9.0V`) feeding all diffused status LEDs without switching noise.

### 3. Standardized Component Series ("Alternative 2")
* **Resistors:** `1%` Metal Film (`0.6W DIN0207`; `1.62k` = `0.25W 1%`). All effect PCBs share 9 core resistor values (`100R`, `1k`, `4.7k`, `10k`, `22k`, `47k`, `100k`, `470k`, `1M`) plus `470R` for the TS9/808 switch and `240R`/`1.62k` for the `9.70V` regulator.
* **Capacitors:** E6 series (`5.00 mm` pitch). Film `≤ 22nF`: `2.5%–5%` WIMA FKP2 / C0G-NP0. Film `47nF–1µF`: `5%` WIMA MKS2/MKP2. Electrolytics: `20%` low-impedance (`≥ 25V` on `9.7V` rails, mandatory `≥ 35V` on `18V` rails).
* **Poka-Yoke Wiring (44 Cables):** Keyed Molex connectors prevent miswiring:
  * `2-pin Mini-Fit Jr`: Unfiltered `18V` raw input.
  * `5-pin Micro-Fit 3.0`: Filtered `+18.0V_CLEAN` power.
  * `4-pin Micro-Fit 3.0`: Regulated `+9.70V` + `~4.75V VREF`.
  * `3-pin Micro-Fit 3.0`: Off-board rockers/potentiometers (`POTx:y`).
  * `2-pin Micro-Fit 3.0`: Shielded audio signal links.

---

## Included Modules

### Core Board Modules (16 Modules — Chapter 12)
1. **Input Buffer & Mute:** Guitar 1/2 selector, `TL072` unity buffer, buffered Tuner Out, `3PDT` True Bypass, and footswitch Mute.
2. **Wah-Wah:** Dual `MPSA18`, `500mH` Fasel inductor, rocker pot, and external `Q` control.
3. **Opto-Compressor:** `VTL5C3` + `TL072` optical compression (Sustain, Level).
4. **TS9 / TS808 Tube Screamer:** Symmetrical soft-clipping overdrive with DPDT `TS9` / `TS808` toggle.
5. **Boss OD-1 OverDrive:** Asymmetrical (`2+1`) diode clipping overdrive.
6. **MXR Distortion+:** `LM741`/`TL071` hard-clipping germanium (`1N60P`/`AA119`/`1N34A`) distortion.
7. **Noise Gate:** Fast JFET shunt gate (`PF5102`/`2N5457`) placed after dirt and before time/modulation effects.
8. **MXR Phase 90:** 4-stage matched JFET phaser (`PF5102`/`2N5457`).
9. **Analog Chorus:** `MN3207` BBD + `MN3102` clock (with local `1N4148` diode drop to `+9.0V_BBD`).
10. **PT2399 Delay:** Echo processor with dedicated internal `5V` regulator (`78L05`).
11. **Belton Reverb:** `BTDR-2H` reverb brick with dedicated `78M05` (`500 mA`) regulator.
12. **7-Band Graphic EQ (`7-EQ`):** `18.0V` active gyrator EQ (`100Hz–6.4kHz`) with `Bourns PTL30` illuminated sliders.
13. **10-Band Graphic EQ (`10-EQ`):** `18.0V` active gyrator EQ (`31.25Hz–16kHz`) + Gain & Volume sliders.
14. **Active Buffered Volume:** Dual `TL072` buffer stages before and after the `100kA` volume rocker.
15. **Output Peak Limiter:** `VTL5C3` optical peak limiter with a 5-LED level meter protecting the output transformer.
16. **Passive 1:1 Isolation / ABY & Back Panel:** `Bourns LM-NP-1001-B1L` transformer isolating Amp B, with `0°/180°` phase invert, ground lift, and ABY switching.

*(Also includes a standalone **Battery / Wall-Wart Stompbox Power Base** PCB in Section 12.1 so any effect module can be boxed as an individual pedal.)*

### Swappable Reference Library (23 Modules — Chapter 12B, Unreviewed)
* **Dirt & Fuzz:** ProCo RAT, Big Muff Pi, Silicon Fuzz Face, Bluesbreaker, MOSFET Overdrive (OCD-style), Analog Octave Fuzz (Green Ringer).
* **Dynamics & Pitch:** Dual Octaver (`+1` Up / `-1` Down), JFET Sustain Compressor, Keyed Sidechain Opto-Gate.
* **Modulation & Time:** Analog Opto-Tremolo, Modulated Tape Echo, Ambient Hall Pre-Delay Reverb, Optical Uni-Vibe (`4× VTL5C3`), Analog BBD Flanger (`MN3207`), Harmonic Tremolo (`2× VTL5C3`), Optical Auto-Wah / Envelope Filter.
* **EQ, Preamp & Routing:** Sweepable Parametric Mid-EQ, Clean Boost (`9.7V`/`18V`), Acoustic Piezo Preamp (`18.0V`, `2.0 MΩ`), Active Parallel Blender & Phase Inverter, Active Transformerless Balanced DI (PA/Mixer only), Passive 1:1 DI/ABY, and Center Pass-Through / Audio Probe.

---

## Repository Structure

* `docs/` — Full project specification documents (`.odt` / `.pdf`) and revision logs.
* `kicad/` — KiCad 10 schematics (`.kicad_sch`), PCB layouts (`.kicad_pcb`), custom symbol/footprint libraries.
* `svg/` — Exported monochrome vector schematics.
* `bom/` — Master BOM and individual unit BOM spreadsheets/CSVs.
