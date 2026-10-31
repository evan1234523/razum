# RAZUM — Universal Dashboard Engineering Specification V1

| Field | Value |
|---|---|
| Status | **PROPOSED REVISION — for owner review. Modeling NOT authorized.** |
| Sources (unchanged) | `code.html`, `DESIGN.md`, `screen.png` @ commit `5daf4ff` |
| Owner decisions applied | E1, E2 (R1), E3, E4, E5 (provisional), E7, E8, E9, E10 |
| Units | Millimetres unless stated; angles in degrees; studs where marked |
| Supersedes | Nothing yet. This document becomes authoritative only after owner approval. |

Status keys used below: **APPROVED** (owner decision), **SOURCE** (kept from source files), **DERIVED** (calculated in this spec), **PROPOSED** (needs owner confirmation), **SUPERSEDED** (conflicting source value retained for the record only; never used in geometry).

---

## 0. Decision log and superseded values

### 0.1 Approved owner decisions

| ID | Decision |
|---|---|
| E1 | Housing width **640 mm**; three in-line gauges, apertures 150 / 180 / 150; 8.25 mm bezel-to-bezel clearance kept |
| E2 | Depth architecture **R1**: Z 0 / 40 / 42 / 65 / 118 / 120 / 122 / 125; dial-to-bezel-front depth **80 mm** |
| E3 | Sun visor **22° down, 85 mm projection**; top fasteners may be hidden in front projection; angled tool access documented (§3.4) |
| E4 | **12 × M8** in a **5 upper / 5 lower / 2 lateral** pattern at the corrected coordinates (§2.2) |
| E5 | **1 stud = 0.28 m** (provisional); Blender metric, 1 BU = 1 m, mm display; single uniform scale factor |
| E7 | **Damped second-order spring** needles, independent per gauge, hard 270° limit, frame-rate stable, configurable, collision-free (§8) |
| E8 | Keep 8.25 mm bezel clearance; **no** widening to 656 mm; strap wrench / spanner may be needed for bezel removal |
| E9 | Boost gauge **linear −0.8 … +2.4 bar**, red zone +2.0 … +2.4 bar |
| E10 | Shift light: **7,000 RPM first amber**, **8,000 RPM redline start**, red zone 8,000–10,000; 9 segments (3 green / 3 amber / 3 red) |

### 0.2 Superseded source values (kept on record, not used in geometry)

| Source value | Where | Why superseded | Replaced by |
|---|---|---|---|
| Housing width 480 mm (18.90") | `code.html` View 01 | Apertures alone sum to 480; no room for bezels, walls, fasteners | 640 (E1) |
| Backplate 11.8" × 5.2" (≈300 × 132 mm) | `code.html` strata table 01 | Smaller than one row of gauges | 640 × 320 (E1, §1) |
| Provisional width 560 mm | Owner request (validation) | Fails by 67 mm; minimum in-line width is 627 mm | 640 (E1) |
| Recessed depth 90 mm | `code.html` summary card, View 02, strata table 02 | Not consistent with the approved Z positions | 80 mm dial-to-bezel (E2) |
| Bay inset 88 mm (sides) / 92 mm (center) | `code.html` View 01 callouts | Same as above; 92 would require 134 mm depth | 80 mm (E2) |
| "GLASS LENS (Z+138)" label | `code.html` View 02 SVG | 138 is SVG drawing units from the dial line, not mm; as mm it exceeds the 125 mm envelope | Z +118 (lens inner) |
| "3D NEEDLE (Z+23)" label | `code.html` View 02 SVG | Relative to dial, ambiguous | Z +65 (dial + 23) |
| Redline 7,000 RPM | `DESIGN.md` Gauges | Owner set redline at 8,000 | 7,000 = first amber shift stage (E10) |
| Non-linear boost labels (−0.8, 0.0, +0.8, +1.6, +2.0, +2.4 at 45° steps, ending at +90°) | `code.html` View 01 | Not compatible with a single linear 270° needle mapping | Linear scale (E9) |
| 11 fasteners drawn (bottom-center missing) | `code.html` View 01 | Spec states 12; source positions also collided with tray and shift light | 12 at §2.2 (E4) |
| 7 shift-light lamps | `code.html` View 03 | View 01 shows 9 | 9 (E10) |
| Missing tach numeral "3" | `code.html` View 01 | Drafting error | Restored |
| "10-point" backplate polygon | `code.html` comment | Polygon has 8 points | 8-point outline, 20 × 45° chamfers |
| Blender unit 1 BU = 100 mm | `code.html` header | Non-standard; risks export scale errors | 1 BU = 1 m, mm display (E5) |
| `Lerp(dt*18)` needle motion | `code.html` cheat sheet | First-order smoothing, not the approved model | Second-order spring (E7, §8) |
| Source triangle split (housing 1,820; bezels 1,080; needles 450; lenses 360; "12x fasteners & toggles" 1,140) | `code.html` cheat sheet | Incomplete and ambiguous (dials, LEDs, tray, visor, tunnels not itemized) | §5 audit; **4,850 ceiling kept** |
| Demo needle angles (≈195 km/h drawn at 200; 7,440 RPM drawn at 7,667; +1.80 bar drawn at ≈+1.06 bar on the linear scale) | `code.html` View 01 | Illustration only | Not geometry; ignored |

---

## 1. Authoritative dimension table

Coordinates use the spec frame **S** (§7): +X driver's right, +Y up, +Z toward the driver; origin at the bottom-center of the rear face.

### 1.1 Envelope

| Parameter | Value | Status |
|---|---|---|
| Housing width (X) | **640.0** (X −320 … +320) | APPROVED |
| Housing height (Y), bulkhead | **320.0** (Y 0 … 320) | DERIVED |
| Overall height incl. visor root | **328.0** | DERIVED |
| Overall depth (Z), maximum envelope | **125.0** (visor tip) | APPROVED |
| Bulkhead thickness | 40.0 (Z 0 … 40) | APPROVED |
| Outline | 8-point, **20 × 45°** chamfer on each corner | DERIVED |
| Die-cast tolerance | ±0.25 | SOURCE |
| Tessellation rule | Facet (chord) error ≤ 0.25 → 48 segments for all gauge-scale circles (worst 0.221 at R 103) | DERIVED |

### 1.2 Gauges

| Parameter | Left (speed) | Center (tach) | Right (boost) | Status |
|---|---|---|---|---|
| Axis center (X, Y) | (−199, 160) | (0, 170) | (+199, 160) | DERIVED |
| Aperture = bore = bezel lip ID | **Ø150.0** | **Ø180.0** | **Ø150.0** | APPROVED |
| Tunnel wall / tunnel OD | 5.0 / Ø160.0 | 5.0 / Ø190.0 | 5.0 / Ø160.0 | DERIVED |
| Tunnel Z span | 40 … 118 (78 long) | same | same | DERIVED |
| Bezel OD (knurled) | **Ø176.0** | **Ø206.0** | **Ø176.0** | DERIVED |
| Bezel front face radial width | 13.0 | 13.0 | 13.0 | DERIVED |
| Bezel Z span (skirt rear → lip front) | 103 … 122 | same | same | DERIVED |
| Bezel thread (on tunnel OD) | M160 × 1.5, Z 103 … 118 | M190 × 1.5, Z 103 … 118 | M160 × 1.5 | DERIVED |
| Lens Ø / rim thickness / dome sag | Ø159.5 / 2.0 / 3.0 | Ø189.5 / 2.0 / 3.0 | Ø159.5 / 2.0 / 3.0 | DERIVED |
| Dial plate nominal Ø × thickness | Ø149.5 × 2.0 | Ø179.5 × 2.0 | Ø149.5 × 2.0 | DERIVED |
| Dial plate render-mesh Ø | Ø150.0 | Ø180.0 | Ø150.0 | DERIVED (see R-07) |
| Dial anti-rotation key | 3 × 3 at 6 o'clock | same | same | DERIVED |
| Needle tip radius / tail / hub Ø | 63 / 18 / Ø23 | 78 / 25 / Ø30 | 63 / 18 / Ø23 | DERIVED |
| Needle blade thickness / spindle Ø | 3.0 / Ø4.0 | 3.0 / Ø4.0 | 3.0 / Ø4.0 | DERIVED |
| Adjacent bezel clearance | 8.25 (L–C) | — | 8.25 (C–R) | APPROVED |

### 1.3 Dial scales (all 270° sweeps, measured clockwise from 12 o'clock, −135° … +135°)

| Gauge | Range | Rate | Majors | Red zone | Status |
|---|---|---|---|---|---|
| Speed | 0 … 300 km/h | 0.9° per km/h | every 50 km/h (45°) | 300 marker | SOURCE |
| Tach | 0 … 10,000 RPM | 27° per 1,000 RPM | every 1,000 RPM, numerals 0–10 | **8,000 … 10,000** (+81° … +135°) | APPROVED |
| Boost | −0.8 … +2.4 bar | 84.375° per bar | every 0.8 bar (−0.8 @ −135°, 0.0 @ −67.5°, +0.8 @ 0°, +1.6 @ +67.5°, +2.4 @ +135°); minors every 0.4 bar | **+2.0 … +2.4** (+101.25° … +135°) | APPROVED |

### 1.4 Fasteners and fittings

| Item | Specification | Status |
|---|---|---|
| Fasteners | 12 × M8 socket head cap screw (ISO 4762), Ø9.0 clearance hole, counterbore Ø15.0 × 9.0 deep (Z 31 … 40), head top at Z 39 (1.0 recessed), 6 mm hex socket | APPROVED (pattern) / DERIVED (detail) |
| Minimum bolt edge distance | ≥ 16 required; actual 18 (top/bottom), 22 (sides) | DERIVED |
| Sun visor | Full width 640; Z 40 … 125 (85 projection); 22° down; 8.0 thick (vertical); root top Y 328, root underside Y 320; tip underside **Y 285.66** | APPROVED |
| Shift light frame | 122 × 14 (X ±61, Y 277 … 291), Z 40 … 55 | DERIVED |
| Shift-light lamps | 9 × (10 W × 8 H), 3 mm gaps, Y 280 … 288; order L→R: 3 green, 3 amber, 3 red | APPROVED (count/colors) |
| Switch tray | 330 × 34 (X ±165, Y 29 … 63), Z 40 … 75 | DERIVED |
| Toggle switches | 4 × Ø18 bushing at Y 46; X −125 IGNITION, −85 FUEL PUMP, +85 TURBO DUMP, +125 OVERRIDE; levers end ≤ Z 95 | SOURCE (names) / DERIVED (position) |
| Serial plate | 100 × 24 × 1.5 centered (0, 46), text "RAZUM // COMBAT SYS.V4 · SN #882-RZ" | SOURCE |

---

## 2. Front orthographic layout (view along −Z)

### 2.1 Layout sketch (not to scale; coordinates in §2.2 are authoritative)

```
X:  -320  -298   -199          0          +199   +298  +320
Y 328 ┌──────────── VISOR (root Y320–328; tip underside Y285.66) ─────────────┐
  302 │ ⊙B1     ⊙B2              ⊙B3              ⊙B4     ⊙B5  │ ← upper row (hidden behind visor in true projection)
  291 │                       ┌[▪▪▪▪▪▪▪▪▪]┐  shift light Y277–291, X ±61        │
  273 │                     ╭──────────────────╮                    │
  248 │      ╭──────────╮   │                  │   ╭──────────╮     │
  170 │      │  SPEED   │   │  TACH C(0,170)   │   │  BOOST   │     │
  160 │ ⊙B11 │C(-199,160)│  │  bore Ø180       │   │C(199,160)│ B12⊙│
      │      │Ø150 / Ø176│  │  bezel Ø206      │   │Ø150 / Ø176│    │
   72 │      ╰──────────╯   │                  │   ╰──────────╯     │
   67 │                     ╰──────────────────╯                    │
   63 │        ┌─⊙IGN──⊙FUEL──[SERIAL 100×24]──⊙TURBO──⊙OVRD─┐      │ ← tray Y29–63, X ±165
   18 │ ⊙B6     ⊙B7              ⊙B8              ⊙B9     ⊙B10 │ ← lower row
    0 └──────────────────────────── 640 ──────────────────────────┘
     20 × 45° chamfers on all four corners
```

### 2.2 Fastener coordinates (12 × M8; 5 upper / 5 lower / 2 lateral)

| ID | X | Y | Row | Edge wall (to counterbore) | Chamfer wall |
|---|---|---|---|---|---|
| B1 | −298 | 302 | Upper | 10.5 | 6.64 |
| B2 | −199 | 302 | Upper | 10.5 | — |
| B3 | 0 | 302 | Upper | 10.5 | — |
| B4 | +199 | 302 | Upper | 10.5 | — |
| B5 | +298 | 302 | Upper | 10.5 | 6.64 |
| B6 | −298 | 18 | Lower | 10.5 | 6.64 |
| B7 | −199 | 18 | Lower | 10.5 | — |
| B8 | 0 | 18 | Lower | 10.5 | — |
| B9 | +199 | 18 | Lower | 10.5 | — |
| B10 | +298 | 18 | Lower | 10.5 | 6.64 |
| B11 | −298 | 160 | Lateral | 14.5 | — |
| B12 | +298 | 160 | Lateral | 14.5 | — |

### 2.3 Width validation at 640 mm (gauge row)

| Segment | mm |
|---|---|
| Housing edge → lateral bolt center | 22.0 |
| Counterbore radius | 7.5 |
| Counterbore → left bezel | 3.5 |
| Left bezel OD | 176.0 |
| Bezel gap (center-to-center 199.25 with 10 mm vertical offset) | 8.25 |
| Center bezel OD | 206.0 |
| Bezel gap | 8.25 |
| Right bezel OD | 176.0 |
| Clearance + counterbore radius + edge distance | 3.5 + 7.5 + 22.0 |
| **Total** | **640.0** (minimum possible with the same rules: 627) |

### 2.4 Front-plane clearance register (all values computed; minimum required 3.0)

| Pair | Clearance | Result |
|---|---|---|
| Lateral bolts B11/B12 ↔ side bezels | 3.50 | PASS (tightest bolt) |
| Bottom-center bolt B8 ↔ switch tray | 3.50 | PASS |
| Top-center bolt B3 ↔ shift-light frame | 3.50 | PASS |
| Tach bezel ↔ switch tray | 4.00 | PASS |
| Tach bezel ↔ shift-light frame | 4.00 | PASS |
| Tach bezel ↔ side bezels | 8.25 | PASS (E8 tool note) |
| Switch tray ↔ side bezels | 14.79 | PASS |
| Lower side bolts B7/B9 ↔ switch tray | 28.24 | PASS |
| Upper/lower side bolts ↔ side bezels | 46.50 | PASS |
| Corner bolts ↔ 45° chamfers (wall) | 6.64 | PASS |
| Bolt counterbores ↔ outer edges (wall) | 10.5 / 14.5 | PASS |
| Toggles ↔ serial plate / tray ends / each other | 26 / 31 / 22 | PASS |

**Result: every approved front-plane component fits inside 640 × 320 with ≥ 3.5 mm clearance.**

### 2.5 Front-projection occlusion (E3)

In a true front orthographic view, the visor projects over **Y 285.66 … 328** across the full width:
- all five upper bolts (counterbores Y 294.5 … 309.5) are **hidden** → draw as hidden lines;
- the top 5.34 mm of the shift-light frame and the top 2.34 mm of the lamps are hidden.

---

## 3. Side cross-section B-B (X = 0, tach axis)

### 3.1 Section sketch (Z horizontal, not to scale)

```
Z:  0        31  39 40 42      55  62 65 70  75      95  103    118 120 121 122 123 125
    ├─────────┼───┼──┼──┼───────┼───┼──┼──┼───┼───────┼───┼──────┼───┼───┼───┼───┼───┤
    [════ BULKHEAD S01 (Y 0–320) ════]
              [CB] M8 counterbores (Y18, Y302), head top Z39
                    [D] dial plate Z40–42 (face Z42)
                    [═══ TUNNEL S02: bore Ø180, wall Y75–80 & Y260–265 ═══]→ front face Z118
                               [SHIFT LIGHT Z40–55, Y277–291]
                                    [NEEDLE S04: hub Z62–70, blade plane Z65]
                    [TRAY Z40–75, Y29–63]──toggle levers ≤ Z95
                                                        [BEZEL S05 skirt Z103–122, Y67–273]
                                                                 [LENS rim Z118–120]
                                                                     [BEZEL LIP Z120–122]
                                                                    (lens dome: inner apex 121, outer apex 123)
                    [VISOR: underside Y320 @ Z40 → Y285.66 @ Z125, 22°, 8 thick ═══════════]
```

### 3.2 Approved Z coordinates

| Z | Feature | Status |
|---|---|---|
| 0.0 | Rear datum (bulkhead rear face) | APPROVED |
| 31.0 | Counterbore floor | DERIVED |
| 39.0 | Bolt head top (1.0 recessed) | DERIVED |
| **40.0** | Bulkhead front = bore floor = tunnel root (Stratum 02 start) | APPROVED |
| **42.0** | Dial face (plate Z 40 … 42) | APPROVED |
| 55.0 | Shift-light front | DERIVED |
| 62.0 … 70.0 | Needle hub | DERIVED |
| **65.0** | Needle blade mid-plane (dial + 23; blade 63.5 … 66.5) | APPROVED |
| 75.0 | Switch-tray front | DERIVED |
| ≤ 95.0 | Toggle lever tips | DERIVED |
| 103.0 | Bezel skirt rear / thread start | DERIVED |
| **118.0** | Lens inner rim face = tunnel front face | APPROVED |
| **120.0** | Lens outer rim face = bezel lip rear (Stratum 05 reference plane) | APPROVED |
| 121.0 | Lens inner dome apex | DERIVED |
| **122.0** | Bezel front | APPROVED |
| 123.0 | Lens outer dome apex | DERIVED |
| **125.0** | Visor tip = maximum envelope | APPROVED |

### 3.3 Depth measures and Z clearances

| Measure | Value |
|---|---|
| Dial face → bezel front (approved recess) | **80.0** |
| Dial face → lens inner rim | 76.0 |
| Tunnel physical length | 78.0 |
| Blade underside → dial face | 21.5 |
| Hub front → lens inner rim | 48.0 |
| Lens outer apex → envelope | 2.0 |
| Bezel front → envelope | 3.0 |
| Needle tip → bore wall (radial) | 12.0 (all gauges) |
| Tach tunnel ↔ tray / shift light (Y) | 12.0 / 12.0 |
| Visor underside ↔ tach bezel top at Z 122 | 13.87 |
| Visor underside ↔ shift-light top at Z 55 | 22.94 |
| Bezel thread engagement | 15.0 (Z 103 … 118) |

### 3.4 Upper-fastener maintenance access (E3)

- The visor underside reaches the upper-bolt axis height (Y 302) at **Z 84.55**. A 6 mm hex-key shank (radius ≈ 3.5) touches the visor at **Z ≈ 75.9**, so a straight key has about 36 mm of free length in front of the face.
- **Required tooling (any one):**
  1. Standard 6 mm L-key with the short arm in the socket and the long arm swung through the **lower half-circle only**, re-indexed every 60° (hex socket).
  2. 6 mm **ball-end** hex key (up to ≈ 25° tilt).
  3. 6 mm hex bit on a low-profile ratchet.
- The long arm clears the shift light, because the shift light ends at Z 55 and the key arm works at Z > 55.
- Bezel removal (E8): the 8.25 mm gap between knurled rings is too small for a full hand grip. **A strap wrench or a pin/spanner tool may be required.** Bezel removal clears the visor tip by 12.66 mm.

---

## 4. Five-stratum exploded assembly

Exploded presentation offsets along +Z (display only, not geometry): S01/S02 0, S03 +150, S04 +300, S05 +450.

| Stratum | Contents | Z span | Class | Roblox parts |
|---|---|---|---|---|
| **S01 Housing** | Bulkhead, 12 counterbores, visor, switch tray, serial plate, shift-light frame; 12 M8 heads; 4 toggles; 9 lamps | 0 … 125 | **FIXED** | `Housing` (shared with S02), `Fasteners`, `Toggles`, `LED_1…9` |
| **S02 Tunnels** | Three cylindrical tunnels, bores Ø150/180/150, cast with S01 | 40 … 118 | **FIXED** | Merged into `Housing` |
| **S03 Dial plates** | Three dial plates, keyed | 40 … 42 | **SWAPPABLE (texture only)** | `Dial_L`, `Dial_C`, `Dial_R` |
| **S04 Needles** | Three needles: blade, tail, hub, spindle | 42 … 70 | **SWAPPABLE** | `Needle_L`, `Needle_C`, `Needle_R` |
| **S05 Optics & bezels** | Three domed lenses, three threaded knurled bezels | 103 … 123 | **SWAPPABLE** | `Lens_L/C/R`, `Bezel_L/C/R` |

**Assembly order:** S01+S02 (one casting) → dial into bore, key at 6 o'clock → needle onto spindle in zero pose → lens onto tunnel front face → bezel threaded on, clamping the lens rim.

**Service order:** reverse. Removing a bezel releases the lens; the dial and needle then lift out. The housing is never disturbed.

---

## 5. Triangle budget and audit

### 5.1 Audit finding that changed the baseline

The previous estimate (4,520) modeled each M8 head at Ø13 inside a Ø15 counterbore with no counterbore floor. That leaves a 1 mm annular see-through gap at every bolt.

| Fix | Effect | Total |
|---|---|---|
| (a) Add a floor annulus at each counterbore | +28 × 12 = +336 | **4,856 — exceeds the 4,850 ceiling by 6** ✗ |
| (b) **Render head line-to-line at Ø15 (16 segments)**, gap drawn in the normal/AO texture; counterbore wall becomes a 1 mm band | −20 × 12 = −240 | **4,280** ✓ |

**Proposed: fix (b).** All tables below use it. The 4,850 ceiling is unchanged.

### 5.2 Component table

| Blender object | Roblox part | Qty | Tris each | Subtotal | Class | Merged at export | In 24-part count |
|---|---|---|---|---|---|---|---|
| `S01_Bulkhead_FrontFace` (8-pt outline, 3 tunnel roots @48, 12 counterbores @16) | Housing | 1 | 372 | 372 | Fixed | Yes → Housing | via Housing |
| `S01_Bulkhead_BackAndEdges` | Housing | 1 | 22 | 22 | Fixed | Yes → Housing | via Housing |
| `S01_CounterboreBands` (16-seg, 1 mm) | Housing | 12 | 32 | 384 | Fixed | Yes → Housing | via Housing |
| `S01_Visor` | Housing | 1 | 12 | 12 | Fixed | Yes → Housing | via Housing |
| `S01_SwitchTray` | Housing | 1 | 10 | 10 | Fixed | Yes → Housing | via Housing |
| `S01_SerialPlate` | Housing | 1 | 10 | 10 | Fixed | Yes → Housing | via Housing |
| `S01_ShiftLightFrame` | Housing | 1 | 10 | 10 | Fixed | Yes → Housing | via Housing |
| `S02_Tunnel_L/C/R` (bore + outer wall, 48-seg; hidden faces removed) | Housing | 3 | 192 | 576 | Fixed | Yes → Housing | via Housing |
| **Housing MeshPart subtotal** | | | | **1,396** | | | **1 part** |
| `S01_Fastener_01…12` (Ø15 cap 16-seg 22 + hex walls 12 + floor 4) | Fasteners | 12 | 38 | 456 | Fixed | Yes → Fasteners | **1 part** |
| `S01_Toggle_1…4` (bushing 46 + lever 12 + tip 24) | Toggles | 4 | 82 | 328 | Fixed | Yes → Toggles | **1 part** |
| `S01_LED_1…9` | LED_1…9 | 9 | 10 | 90 | Fixed | No (per-lamp state) | **9 parts** |
| **Fixed subtotal** | | | | **2,270** | | | **12 parts** |
| `S03_Dial_L/C/R` (48-seg disc, front face only) | Dial_* | 3 | 48 | 144 | Swappable | No | **3 parts** |
| `S04_Needle_L`, `S04_Needle_R` (blade 12, tail 12, 16-seg hub 46, spindle 16) | Needle_L/R | 2 | 86 | 172 | Swappable | No | **2 parts** |
| `S04_Needle_C` (20-seg hub 58 + hex imprint 12) | Needle_C | 1 | 110 | 110 | Swappable | No | **1 part** |
| `S05_Lens_L/C/R` (48-seg dome, centre fan + 1 ring, single-sided) | Lens_* | 3 | 144 | 432 | Swappable | No | **3 parts** |
| `S05_Bezel_L/C/R` (lip face, lip wall, outer wall, rear annulus; knurl in texture) | Bezel_* | 3 | 384 | 1,152 | Swappable | No | **3 parts** |
| **Swappable subtotal** | | | | **2,010** | | | **12 parts** |
| Odometer (texture window) | — | 1 | 0 | 0 | Swappable (texture) | — | — |
| Motor6D joints (Part0 = Housing; no anchor parts) | — | 3 | 0 | 0 | — | — | — |
| **TOTAL** | | | | **4,280** | | | **24 parts** |

### 5.3 Audit resolutions

1. **4,280 vs 4,850.** Total is 4,280, leaving **570** of reserve. That supersedes the 4,520 / 330 figures because of the §5.1 correction. The ceiling is not raised.
2. **Per-component caps.**

   | Slot | Current | Cap | Headroom |
   |---|---|---|---|
   | Dial (geometry frozen; texture variants only) | 48 | 48 | 0 |
   | Needle (each) | 86 / 110 / 86 | 150 | 64 / 40 / 64 |
   | Lens (each) | 144 | 144 | 0 |
   | Bezel (each) | 384 | 438 | 54 |
   | **Swappable total** | **2,010** | **2,340** | **330** |

   Fixed 2,270 + swappable caps 2,340 = **4,610 ≤ 4,850**, so caps are compatible with the estimate. **240 triangles remain unallocated** as a global reserve for fixed-geometry changes.
3. **Is the reserve sufficient?**
   - Enough for variants that differ in texture, normal map and modest silhouette: needles +40 … +64, bezels +54 each.
   - **Not** enough for geometric knurling (≥ 48 teeth ≈ +1,000 per bezel), multi-ring bezels, or faceted lenses.
   - The 240 global reserve covers an optional 3D odometer drum set (≈ 106 estimated).
   - Raising per-slot caps means reallocating the 240 global reserve (owner decision, §9 V-17).
4. **Can all three gauges be swapped within budget?**
   - Dial-face variants (derby, street tuner, military altimeter) are texture-only: **0 triangle change**.
   - Needle, lens and bezel variants on all three gauges at their caps at once: **worst case 4,610 ≤ 4,850. Yes.**
5. **Are the tunnels counted as fixed housing?** Yes. S02 (576) is in the fixed subtotal and merged into the `Housing` MeshPart.
6. **Is the 24-part count consistent?** Yes: Housing 1 + Fasteners 1 + Toggles 1 + LEDs 9 + Dials 3 + Needles 3 + Lenses 3 + Bezels 3 = **24**.
   - The earlier note "Motor6D anchors (plain parts)" is withdrawn. Motor6D `Part0` is the Housing, so no extra parts are needed.
   - If toggles must animate individually, Toggles splits into 4 parts (27 total, same triangles). Not currently specified.

---

## 6. Fixed-versus-swappable interface specification

The universal-housing rule: **S01 and S02 never change across vehicles; all customization happens in S03, S04 and S05, and every variant must satisfy these interfaces.**

| Interface | Applies to | Requirement |
|---|---|---|
| I-01 Mounting | S01 | 12 × M8 at §2.2; rear face Z 0 is the chassis datum; Roblox pivot at S origin |
| I-02 Bore | S02 → S03/S04/S05 | Bores Ø150.0 / 180.0 / 150.0 at §1.2 axes; floor Z 40; front face Z 118; thread M160 / M190 × 1.5 at Z 103 … 118 |
| I-03 Dial | S03 | Geometry frozen (render Ø150.0 / 180.0, Z 40 … 42, key at 6 o'clock, Ø4.2 center hole). Variants change the **texture only**. Scale zero at −135°, full scale at +135°, clockwise. Texture: 1024 × 1024, dial circle inscribed, centre = pixel (512, 512), 6 o'clock = bottom of image. Keep-out: hub Ø23 / Ø30 centre; outer 2 mm |
| I-04 Needle | S04 | Origin on gauge axis at Z 65; blade plane Z 65 ± 0.25; Z envelope 62 … 70; tip radius ≤ 68 (sides) / ≤ 83 (centre); **modeled in zero pose pointing −135° (7:30)**; ≤ 150 tris; `CanCollide/CanTouch/CanQuery = false`, `Massless = true` |
| I-05 Lens | S05 | Ø159.5 / 189.5, rim Z 118 … 120, apex ≤ Z 123, ≤ 144 tris, single-sided |
| I-06 Bezel | S05 | Lip ID = aperture exactly; **OD ≤ 176 / 206** (protects §2.4 clearances); front ≤ Z 122; skirt rear ≥ Z 103; ≤ 438 tris |
| I-07 Telemetry | Script | Values read from vehicle attributes `RPM`, `SpeedKmh`, `BoostBar`; customization never touches the Housing |

**Runtime swap without rebuilding the housing:** replace or reparent the `Dial_*` appearance, `Needle_*` MeshPart (re-target the Motor6D `Part1`), and `Lens_*` / `Bezel_*` MeshParts. Mechanism details are in §9 (V-08).

---

## 7. Blender coordinate and Roblox scale specification

### 7.1 Frames

| Frame | Axes | Mapping |
|---|---|---|
| **S** (this spec) | +X right, +Y up, +Z toward driver | Reference frame |
| **Blender** | Z-up; Front view (Numpad 1) looks along +Y | B = (Sx, −Sz, Sy). Gauge faces point −Y. Proper rotation, no mirroring |
| **Roblox model local** | +Y up, vehicle forward = −Z (LookVector) | R = S (identity), then mm → studs. Gauge faces point +Z toward the driver |

- **Needle rotation:** clockwise as seen by the driver = negative rotation about +Z = `CFrame.Angles(0, 0, -θ)`.
- **Blender needle origins (mm):**

  | Needle | Origin (mm) |
  |---|---|
  | Left | (−199, −65, 160) |
  | Centre | (0, −65, 170) |
  | Right | (199, −65, 160) |

- **Housing origin:** the S origin, which is Blender (0, 0, 0).

### 7.2 Units and scale

- **Blender:** Unit System Metric, Unit Scale **1.0** (1 BU = 1 m), Length unit **Millimeters**. Enter values as e.g. `640mm`.
- **Roblox:** **1 stud = 0.28 m (provisional, E5)**. studs = mm ÷ 280; 1 mm = 0.003571 studs.
- **One uniform scale factor at model level only.** No per-part scaling.

| Dimension | mm | studs |
|---|---|---|
| Housing width | 640 | 2.2857 |
| Housing height / with visor | 320 / 328 | 1.1429 / 1.1714 |
| Envelope depth | 125 | 0.4464 |
| Side / centre aperture | 150 / 180 | 0.5357 / 0.6429 |
| Side / centre bezel OD | 176 / 206 | 0.6286 / 0.7357 |
| Gauge X offset | 199 | 0.7107 |
| Gauge axis Y (side / centre) | 160 / 170 | 0.5714 / 0.6071 |
| Dial face / needle plane / bezel front Z | 42 / 65 / 122 | 0.1500 / 0.2321 / 0.4357 |

### 7.3 Export procedure (proposed; untested)

- **Format:** FBX, Forward **−Z**, Up **Y**, Apply Transform on; all object rotation and scale applied before export.
- **Triangulate** on export so the counts in §5 are measurable in the exported file.
- **Axis-marker test** (must pass before production export; see V-01):
  - Export a calibration file with three arrows: +X red, +Y green, +Z blue (in S).
  - Add a 1,000 mm cube and a "FRONT" text plate on the +Z face.
  - **Pass if:** arrows import as Roblox +X / +Y / +Z, the text is not mirrored, and the cube measures 3.5714 studs.

---

## 8. Needle spring dynamics specification (E7)

### 8.1 Model

Each gauge needle angle θ (radians, 0 = scale zero) follows an independent damped harmonic oscillator:

```
θ_target = clamp((v − v_min) / (v_max − v_min), 0, 1) · Θ_max,   Θ_max = 270° = 3π/2
θ̈ = ω² (θ_target − θ) − 2 ζ ω θ̇,                                ω = 2π f_n
```

- `f_n`: natural frequency (stiffness), configurable.
- `ζ`: damping ratio, configurable (ζ < 1 gives a visible needle bounce).

### 8.2 Integration (frame-rate stable)

- **Fixed sub-step:** semi-implicit (symplectic) Euler at h = 1/240 s, driven by an accumulator.
- **Hitch protection:** at most 16 sub-steps per frame. Excess time after a long hitch is discarded, so there is no catch-up spiral.
- **Stability:** semi-implicit Euler is stable for ω·h < 2. The stiffest proposed setting gives ω·h = 0.105, a factor of about 19 below the bound.
- **Frame-rate independence:** motion is identical at 30, 60, 120 and 240 FPS, apart from ≤ 1 sub-step of display latency (4.2 ms).

### 8.3 Hard 270° limit

- `θ_target` is clamped to [0, Θ_max].
- After **every** sub-step, θ is clamped to [0, Θ_max].
- On hitting a stop, the outward velocity is reflected with restitution `e` (stop-pin bounce, default 0.25).
- θ therefore **cannot** leave [0°, 270°] regardless of input, parameters or frame time.

### 8.4 Proposed default parameters (tuning required; V-09)

| Gauge | v_min | v_max | f_n (Hz) | ζ | e | Overshoot | 2 % settling |
|---|---|---|---|---|---|---|---|
| Speed | 0 km/h | 300 km/h | 2.0 | 0.70 | 0.20 | 4.6 % | 0.46 s |
| Tach | 0 RPM | 10,000 RPM | 4.0 | 0.45 | 0.25 | 20.5 % | 0.35 s |
| Boost | −0.8 bar | +2.4 bar | 3.0 | 0.35 | 0.25 | 30.9 % | 0.61 s |

Optional `vibration` input adds small noise to `θ_target`, never to the state. Default amplitude 0. This replaces the source `shudderJitter`.

### 8.5 Proposed Roblox implementation (reference code, not yet run)

```lua
-- GaugeSpring (client-side, cosmetic). Proposed; not tested in Roblox.
local STEP = 1 / 240
local MAX_STEPS = 16
local THETA_MAX = math.rad(270)

local GaugeSpring = {}
GaugeSpring.__index = GaugeSpring

function GaugeSpring.new(motor: Motor6D, cfg)
	return setmetatable({
		motor = motor, baseC0 = motor.C0,
		vMin = cfg.vMin, vMax = cfg.vMax,
		omega = 2 * math.pi * cfg.freqHz, zeta = cfg.damping,
		restitution = cfg.restitution or 0.25,
		theta = 0, vel = 0, target = 0, acc = 0,
	}, GaugeSpring)
end

function GaugeSpring:setValue(v: number)
	local f = math.clamp((v - self.vMin) / (self.vMax - self.vMin), 0, 1)
	self.target = f * THETA_MAX
end

function GaugeSpring:step(dt: number)
	self.acc = math.min(self.acc + dt, STEP * MAX_STEPS)
	local w, z = self.omega, self.zeta
	while self.acc >= STEP do
		local a = w * w * (self.target - self.theta) - 2 * z * w * self.vel
		self.vel += a * STEP
		self.theta += self.vel * STEP
		if self.theta < 0 then
			self.theta = 0
			if self.vel < 0 then self.vel = -self.vel * self.restitution end
		elseif self.theta > THETA_MAX then
			self.theta = THETA_MAX
			if self.vel > 0 then self.vel = -self.vel * self.restitution end
		end
		self.acc -= STEP
	end
	self.motor.C0 = self.baseC0 * CFrame.Angles(0, 0, -self.theta)
end

return GaugeSpring
```

**Integration:**
- **Joints:** one `GaugeSpring` per Motor6D (`Part0` = Housing, `Part1` = Needle, C0 at the gauge axis on Z 65, C1 = identity).
- **Script:** a single LocalScript steps all three gauges in one per-frame render callback.
- **Values:** read from vehicle attributes (I-07), so every client animates locally and nothing physics-related is replicated.
- **Needle parts:** `Massless`, no collision, touch or query. Needles take no part in physics or collision.

### 8.6 Shift-light logic (E10)

| Lamp | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---|---|
| Colour | Green | Green | Green | Amber | Amber | Amber | Red | Red | Red |
| On at RPM | 5,500* | 6,000* | 6,500* | **7,000** | 7,333* | 7,667* | **8,000** | 8,667* | 9,333* |

- **Bold** values are approved. Values marked * are PROPOSED (evenly spaced steps); owner decision V-18.
- `DESIGN.md` "redlining into flashing" is proposed as: all nine lamps flash at 8 Hz at ≥ 9,333 RPM (V-18).
- Lamps read the **raw** RPM value, not the spring-filtered needle angle.

---

## 9. Validation register

Class: **A** = resolved by documentation in this spec; **B** = needs a later technical test (nothing in this class has been verified); **C** = needs an owner decision.

| ID | Item | Class | Current status | Required action / pass criterion |
|---|---|---|---|---|
| V-01 | Blender → Roblox FBX axis mapping | A + **B** | Convention defined (§7.1). **Not tested.** | Axis-marker export (§7.3); pass = correct axes, no mirroring |
| V-02 | Import scale (0.28 m/stud) | **B** | Not tested | Housing `Size.X` = 2.2857 ± 0.001 studs after import |
| V-03 | Glass lens appearance (Glass material, Transparency 0.75) | **B** + C | Source "specular gloss 0.95" has no direct Roblox property; proposed mapping to `Reflectance`. **Not tested.** | Visual test at several graphics-quality levels; owner accepts look |
| V-04 | Emissive needles (source: emissive 0.4) and lit lamps | **B** + C | SurfaceAppearance emissive support **unconfirmed**; fallback = Neon material on lamps/needles | Test both; owner accepts fallback if needed |
| V-05 | SurfaceAppearance maps (Color, Normal, Metalness, Roughness) on Housing, Dials, Bezels | **B** | Not tested | Maps load and render correctly in Studio and on device |
| V-06 | Texture resolution (source 2048² housing map) | **B** | **Assumption:** effective limit 1024²; not confirmed | Upload test; record effective resolution |
| V-07 | Texture memory | A + **B** | Uncompressed RGBA upper bound with mips: Housing 4 × 1024² = 21.3 MiB; dial colour 3 × 1024² = 16.0 MiB; shared dial normal/roughness 2 × 512² = 2.7 MiB; bezel set 4 × 512² = 5.3 MiB; **≈ 45 MiB worst case.** GPU compression may reduce this; **not measured** | Measure with the Developer Console memory view on the target mobile device |
| V-08 | Runtime gauge customization without rebuilding the housing | A + **B** | Architecture defined (§6). **Unconfirmed:** whether SurfaceAppearance maps can be changed at runtime. Proposed paths: swap a pre-authored SurfaceAppearance instance or Decal on the dial; swap needle/lens/bezel MeshParts | Runtime test on a live vehicle; Housing instance unchanged |
| V-09 | Needle spring stability and performance | A + **B** | Model, stability bound and defaults documented (§8). **Not run.** | Test at 30/60/120/240 FPS and a 0.5 s hitch; θ stays in [0, 270°]; tune f_n, ζ, e; script cost < 0.1 ms/frame (proposed) |
| V-10 | Driver eye visibility of shift lights under the visor | A + **C** + B | **Computed** (sight line from lamp face at Z 55 passing under the visor tip): the eye's elevation above the lamps must be ≤ **−1.9°** to see full lamp height, ≤ **+1.4°** to see lamp centres, ≤ **+4.6°** to see any lamp. Above +4.6° all lamps are hidden. At the source's 18° viewing elevation they are **fully hidden**. | Owner: accept, relocate shift light, or reduce visor angle; then in-vehicle camera test |
| V-11 | Collision configuration | A + **B** | Proposed: all 24 parts `CanCollide = false`, `CanTouch = false`, `Massless = true`; `CanQuery = false` except Housing (`CollisionFidelity = Box`) if camera/raycast blocking is wanted. **Not tested.** | Test avatar seating, camera behavior, vehicle handling unchanged |
| V-12 | Mobile performance | **B** + C | 4,280 tris, 24 MeshParts. Not profiled. Target device not specified | Owner names target device; profile for 60 FPS |
| V-13 | 0.28 m/stud fit for the RAZUM cockpit and avatar | **C** + B | Provisional. Many Roblox vehicles are built larger than true scale relative to avatars | Owner confirms vehicle/avatar scale; test seat fit; if changed, apply one uniform factor |
| V-14 | Exported triangle count | **B** | Estimated only | Triangulated FBX count ≤ 4,280 (≤ 4,610 with max variants) |
| V-15 | Client-side `Motor6D.C0` updates on a moving vehicle (ownership, replication) | **B** | Expected cosmetic and local; **not tested** | Test as driver, passenger and observer |
| V-16 | MeshPart `RenderFidelity` / automatic level-of-detail on small parts (needles, fasteners) | **B** | Not tested | Confirm needles are not simplified at cockpit distance; set `Precise` if needed |
| V-17 | Allocation of the 240 global triangle reserve | **C** | Unallocated | Owner: keep, raise bezel/needle caps, or fund 3D odometer drums |
| V-18 | Proposed green/intermediate shift thresholds and flash rule | **C** | Proposed in §8.6 | Owner approves or edits |
| V-19 | Toggle animation (1 part vs 4 parts) | **C** | Not specified in source | Owner decides; triangles unchanged |
| V-20 | Dial "matte" vs roughness 0.22 (`code.html` materiality) | **C** | Contradictory | Owner picks roughness |

---

## 10. Risks and assumptions

| ID | Risk / assumption | Impact | Mitigation |
|---|---|---|---|
| R-01 | Shift lights are occluded by the approved visor at normal driver eye heights (V-10) | Main RPM cue may be invisible in play | Owner decision before modeling |
| R-02 | Roblox behaviors (V-01 … V-08, V-11, V-14 … V-16) are **assumed, not verified** | Rework after first import | Run the B-class tests on a calibration asset before production |
| R-03 | Texture limit and memory (V-06, V-07) | Downscaled detail; mobile memory pressure | Author at 2048, validate at 1024; share maps across variants |
| R-04 | Swappable caps leave small per-slot headroom (needles +40 … +64, bezels +54) | Detailed variants must use textures, not geometry | Reallocate the 240 global reserve if needed (V-17) |
| R-05 | 8.25 mm bezel gap (E8) | Hand removal impractical | Strap wrench / spanner tool, documented in §3.4 |
| R-06 | Upper fasteners under the visor (E3) | Slower maintenance | Angled tool access, documented in §3.4 |
| R-07 | Dial render mesh is line-to-line (Ø150.0 / 180.0) with the bore, while the nominal part is Ø149.5 / 179.5 | None in game; nominal value kept for the record | Render value governs geometry |
| R-08 | Housing height 328 is derived (source gave none); the source front view suggests ≈ 240 | Proportions differ from the source illustration | Accepted consequence of the approved 5-5-2 pattern and stacked layout |
| R-09 | 0.28 m/stud may not match the game's vehicle scale (V-13) | Cockpit too small or large for avatars | Single uniform scale factor; owner decision |
| R-10 | Needle spring defaults are untuned starting values | Feel may be wrong | Tuning pass in V-09 |
| R-11 | **Assumption:** the dashboard is cosmetic and client-animated; telemetry comes from vehicle attributes | If server-authoritative needles are required, the design changes | Confirm with the owner |
| R-12 | **Assumption:** 48-segment tessellation is acceptable for the art style (facet error ≤ 0.221 mm) | — | Visible faceting at extreme close-up only |

---

## 11. Self-review and verification record

**Arithmetic and geometry** were checked with a calculation script (not part of the project):
- 12 fasteners present.
- All front-plane clearances ≥ 3.5 mm (§2.4); bezel gaps 8.251 mm.
- Width stack sums to 640.0.
- Visor tip underside Y 285.658; tach-bezel clearance under the visor 13.870.
- Z stack: 80 / 76 / 78 / 48 / 2.
- Triangle sums: fixed 2,270, swappable 2,010, total 4,280, caps 4,610.
- Stud conversions, spring stability ratios, overshoot and settling values.

**Internal contradictions resolved in this revision:**
- 4,520 → 4,280 (fastener render fix, §5.1).
- Withdrawn "Motor6D anchor parts" note, so the part count is 24.
- Superseded values are isolated in §0.2 and do not appear in §1–§8.

**640 mm fit:** every approved component fits (§2.3, §2.4, §3.3).

**Triangle budget:** 4,280 ≤ 4,850; worst-case variants 4,610 ≤ 4,850.

**Open items requiring the owner:** V-10 / R-01 (shift-light visibility), V-13 (scale), V-12 (target device), V-17 (reserve), V-18 (thresholds), V-19 (toggles), V-20 (dial roughness), and approval of the §5.1 fastener render change.

**Not done (by instruction):** no Blender installation, no geometry, no assets, no modeling scripts, no changes to `code.html`, `DESIGN.md` or `screen.png`, no commit or push.
