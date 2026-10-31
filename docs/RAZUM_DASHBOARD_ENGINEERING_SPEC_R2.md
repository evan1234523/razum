# RAZUM — Universal Dashboard Engineering Specification R2

| Field | Value |
|---|---|
| Status | **R2 FINAL — APPROVED by the owner as the engineering specification for the next phase.** Closes the engineering stage. **Modeling NOT yet authorized** (separate authorization required). |
| Revision history | R2 draft → R2 corrected (tolerance and structural audit, §15) → **R2 final**: D-2 … D-7 approved; approval conditions recorded (§0.3); pending requirements listed (§16) |
| Relationship to V1 | V1 is preserved unchanged as the historical baseline. **R2 governs** where they differ |
| Base document | `docs/RAZUM_DASHBOARD_ENGINEERING_SPEC_V1.md` (preserved unchanged) |
| Sources (unchanged) | `code.html`, `DESIGN.md`, `screen.png` @ commit `5daf4ff` |
| Scope of R2 | Applies the owner decisions after pre-modeling reviews R1 and R2: fastener option B, L1 shift-light pod, shift-light logic, four animated toggles, dial roughness, and **gauge-visibility option C** |
| Units | Millimetres unless stated; angles in degrees; studs where marked |

Status keys: **APPROVED** (owner decision), **V1** (unchanged from V1), **DERIVED** (calculated here and accepted with R2 approval), **SUPERSEDED** (kept for the record only). No item in R2 final remains in PROPOSED status; open items are listed in §16.

Where R2 is silent, V1 applies.

---

## 0. Decision log and change summary

### 0.1 Owner decisions applied in R2

| ID | Decision | Section |
|---|---|---|
| R2-01 | Fasteners **option B**: real Ø15 3D heads; ring in texture | §5, §6 |
| R2-02 | Shift lights **L1**: nine-lamp pod on top of the visor | §2.4 |
| R2-03 | Thresholds: green 5,500 / 6,000 / 6,500; amber 7,000 / 7,333 / 7,667; red 8,000 / 8,667 / 9,333 RPM; hysteresis 150 RPM | §9.2 |
| R2-04 | Flashing at **2.5 Hz** at ≥ 9,500 RPM, with a player setting to disable it | §9.2 |
| R2-05 | **Four individually animated toggle levers**, ±30° travel | §6, §9.3 |
| R2-06 | Dial roughness **0.70** (face) / **0.55** (printed markings) | §1.5 |
| R2-07 | Gauge visibility **option C**: lens and bezel front plane **raked 12°**; three gauge centres and the universal architecture kept | §3 |
| R2-08 | Z 118 / 120 / 122 now refer **only to the bottom edge of the opening** | §3.2 |
| R2-09 | Threaded bezels replaced by **3 × M3 screws** per bezel, heads drawn in the texture | §4.2, §10 |
| R2-10 | Bezel OD reduced by **0.25 mm** (175.75 / 205.75) to keep the **8.25 mm** gap | §1.2, §2.3 |
| R2-11 | 22° visor kept; the **1.3 mm sliver** hidden at the top of the tach is accepted | §3.5 |
| R2-12 | **D-2:** tach bezel top rim thinned from 12.875 to **9.875** for a straight-pull removal (validated in §15.3) | §1.2, §10, §15 |
| R2-13 | **D-3:** 18° is the design eye elevation for every RAZUM vehicle | §3.5 |
| R2-14 | **D-4:** each bezel bears on the machined lug stop faces (metal to metal). **No structural load passes into the lens**; the lens sees only the gasket clamp | §4.2, §15.1 |
| R2-15 | **D-5:** lens gasket of closed-cell silicone foam, 1.0 free, compressed to 0.6; bezel lip 1.4. Material grade still to be specified (§16, P-01) | §4.2, §15.2 |
| R2-16 | **D-6:** visor tip tolerance unilateral, **+0 / −0.30** | §15.1, §15.5 |
| R2-17 | **D-7:** the §15.5 tolerance table is the **dimensional reference of R2** | §15.5 |

### 0.3 Conditions attached to the R2 approval (owner)

| ID | Condition |
|---|---|
| C-1 | The **0.161 mm worst-case depth margin** (bezel lower outer edge vs the 125 mm envelope) is **critical**. It requires dimensional inspection of the chain in §15.1 on every physical part (§16, P-02). |
| C-2 | The bezel strength and stiffness figures (§15.3) are **analytical estimates without physical validation** (§16, P-03). |
| C-3 | The silicone gasket needs a **material specification before manufacture**: hardness, temperature resistance and ageing (§16, P-01). |
| C-4 | **None of the R2 approvals validate performance in Roblox.** Every Roblox behaviour in this document is untested until the §16 tests are run. |

### 0.2 V1 values superseded by R2 (record only)

| V1 value | R2 replacement |
|---|---|
| Lens and bezel planes perpendicular to Z at Z 118 / 120 / 122 across the whole opening | Raked 12° planes; 118 / 120 / 122 apply at the opening's bottom edge (§3.2) |
| Circular bores, lens Ø159.5 / 189.5, bezel OD Ø176 / 206 | Stadium outlines with upper sight-line relief; bezel OD 175.75 / 205.75 (§1.2) |
| Bezel thread M160 / M190 × 1.5, Z 103 … 118 | 3 × M3 screws into cast lugs (§4.2) |
| E8 note: strap wrench for bezel removal | Screwdriver; removal procedure in §10 |
| Shift-light frame under the visor (Y 277 … 291) | L1 pod on the visor top (§2.4) |
| Proposed 8 Hz flash (V1 §8.6) | 2.5 Hz (R2-04) |
| `Toggles` as one MeshPart (24 parts) | Four lever MeshParts; bushings merged into Housing (**27 parts**) |
| Dial roughness 0.22 (source) | 0.70 / 0.55 |
| Fastener render with see-through gap (4,520 estimate) | Option B (V1 §5.1 fix (b)) |
| Bezel lip 2.0, lens clamped metal-to-glass | Lip 1.4 with 1.0 → 0.6 foam gasket (approved D-5, §15.2) |
| Symmetric ±0.25 die-cast tolerance on all features | Unilateral tolerance on envelope features; machined datum features (§15.5) |

---

## 1. Authoritative dimension table (R2)

Spec frame **S** as in V1: +X driver's right, +Y up, +Z toward the driver. Origin at the bottom-centre of the rear face.

### 1.1 Envelope and housing

| Parameter | Value | Status |
|---|---|---|
| Housing width × height | 640.0 × 320.0 (328.0 with visor root) | V1 |
| Maximum depth envelope | 125.0 | V1 |
| Frontmost points | Visor tip Z 125.00; bezel lower outer edges Z **124.74** | DERIVED |
| Bulkhead | Z 0 … 40 | V1 |
| Corner chamfers | 20 × 45° | V1 |
| Visor | 22° down, 85 projection (Z 40 … 125), 8 thick; tip underside Y 285.66 | V1 / APPROVED |
| Fasteners | 12 × M8 ISO 4762, 5-5-2 pattern at V1 §2.2 coordinates | V1 |

### 1.2 Gauges (option C)

| Parameter | Side gauges (L, R) | Tach (C) | Status |
|---|---|---|---|
| Axis centre (X, Y) | (∓199, 160) | (0, 170) | V1 |
| Bore radius R (aperture Ø) | 75.0 (Ø150) | 90.0 (Ø180) | V1 |
| Opening bottom edge Y_b = centre − R | 85.0 | 80.0 | DERIVED |
| Front-plane rake (top leaning back) | **12°** | **12°** | APPROVED |
| Upper sight-line relief slope | 18° (e(Z) = (Z − 42) · tan 18°) | 18° | DERIVED |
| Relief at the bezel front plane, e_f | **14.62** | **12.69** | DERIVED |
| Relief at the lens inner plane, e_l | 13.41 | 11.47 | DERIVED |
| Bezel lip opening (front view) | Semicircles R 75.0, upper half raised 14.62 → 150.0 W × 164.62 H | R 90.0, raised 12.69 → 180.0 W × 192.69 H | DERIVED |
| Opening top at bezel front | Y 249.62 @ Z 87.01 | Y 272.69 @ Z 81.04 | DERIVED |
| Tunnel wall / tunnel OD (front view) | 5.0 / R 80.0, upper half raised by e(Z) | 5.0 / R 95.0, raised by e(Z) | DERIVED |
| Lens outline (front view) | R 79.75 semicircles, upper raised 13.41; rim 2.0; dome sag ≤ 3.0 | R 94.75, raised 11.47 | DERIVED |
| Lens rim retained under bezel lip | ≥ 3.54 (top) / 4.75 (elsewhere) | ≥ 3.53 (top) / 4.75 | DERIVED |
| Bezel OD (front view) | **175.75** (R 87.875), upper raised 14.62 | **205.75** (R 102.875), upper raised 12.69 | APPROVED |
| Bezel rim width / depth along Z | 12.875 / 19.0 (constant) | 12.875, except **9.875 within ±35° of 12 o'clock** (10° blend each side, clear of the ±60° screws) / 19.0 | DERIVED / APPROVED (R2-12) |
| Bezel outer top / bottom (Y) | 262.50 / 72.125 | **282.56** (thinned) / 67.125 | DERIVED |
| Bezel lip thickness (axial) | 1.4 (with lens gasket; §4.2) | 1.4 | APPROVED (D-5) |
| Dial plate | Flat, Z 40 … 42, render Ø150.0, key at 6 o'clock | Flat, render Ø180.0 | V1 (unchanged) |
| Needle | Blade plane Z 65; tip radius 63 | Tip radius 78 | V1 (unchanged) |
| Bezel retention | 3 × M3 countersunk (§4.2) | same | APPROVED |

### 1.3 Angles

| Angle | Value | Status |
|---|---|---|
| Design driver eye elevation | 18° | Source / APPROVED basis |
| Visor | 22° down | APPROVED |
| Lens / bezel front-plane rake | 12° | APPROVED |
| Tunnel upper relief | 18° from Z (follows the design sight line) | DERIVED |
| L1 pod face | Tilted back 18° (faces the design eye) | APPROVED |
| Needle sweep | 270° (−135° … +135°), clockwise | V1 |
| Toggle lever travel | ±30° about X | APPROVED |
| Housing chamfers | 45° | V1 |

### 1.4 Fixings

| Fixing | Qty | Specification | Status |
|---|---|---|---|
| Chassis mount | 12 | M8 ISO 4762, Ø9 clearance, Ø15 × 9 counterbore, head top Z 39; render head Ø15 line-to-line, ring in texture | V1 + R2-01 |
| Bezel retention | 9 (3 per bezel) | M3 countersunk, length 10, axis normal to the raked face, pitch radius R + 8.5, at 6 o'clock and ±60° from 12 o'clock (upper two raised by e_f); into cast lugs ≥ 8 deep with **M3 wire thread inserts**; heads in texture (0 triangles). The bezel bottoms on **machined lug stop faces** (Z 103.00 at the bottom-edge reference) | APPROVED / DERIVED |
| Lens gasket | 3 | Closed-cell silicone foam, 1.0 free, compressed to 0.6 (40 %), between lens and bezel lip; grade per §16 P-01 | APPROVED (D-5) |
| Dial plate | 3 | Keyed at 6 o'clock, clamped by the lens; no fasteners | V1 |
| Needles | 3 | Press-fit on a Ø4 spindle (physical); Motor6D joint in Roblox | V1 |

### 1.5 Materials (changes only)

| Item | Value | Status |
|---|---|---|
| Dial face | Roughness 0.70, metalness 0, base #090A0D | APPROVED |
| Dial printed markings | Roughness 0.55 (via roughness map) | APPROVED |
| Fasteners | Dedicated 256² SurfaceAppearance (ring and socket detail) | APPROVED (B) |
| Bezel M3 heads | Drawn in the bezel texture | APPROVED |

---

## 2. Front orthographic layout (R2)

### 2.1 Sketch (not to scale)

```
X:  -320  -298   -199          0          +199   +298  +320
Y 328 ┌────────── VISOR (root 320–328; tip underside 285.66) ─────────┐
  309 │                     ┌[▪▪▪▪▪▪▪▪▪]┐  L1 pod on the visor top  │
  302 │ ⊙B1     ⊙B2          ⊙B3          ⊙B4     ⊙B5  │ ← hidden behind visor
  283 │                 ┌────────────────┐ tach bezel top 282.56   │
  262 │    ┌──────────┐ │  ·M3      M3·  │ ┌──────────┐ side top 262.50
  250 │    │ ·M3  M3· │ │                │ │ ·M3  M3· │           │
      │    │  SPEED   │ │  TACH (0,170)  │ │  BOOST   │           │
  160 │⊙B11│(-199,160)│ │                │ │(199,160) │B12⊙       │
      │    │          │ │                │ │          │           │
   72 │    ╰───·M3────╯ │                │ ╰───·M3────╯           │
   67 │                 ╰──────·M3───────╯                         │
   63 │      ┌─IGN──FUEL──[SERIAL 100×24]──TURBO──OVRD─┐           │ ← 4 animated levers
   18 │ ⊙B6     ⊙B7          ⊙B8          ⊙B9     ⊙B10 │
    0 └──────────────────────── 640 ─────────────────────────────┘
  Stadium outlines: round lower half; upper half raised 14.62 (side) / 12.69 (tach).
```

### 2.2 Coordinates (unchanged from V1 unless noted)

| Feature | Coordinates |
|---|---|
| M8 B1 … B5 (upper) | (−298, 302), (−199, 302), (0, 302), (199, 302), (298, 302) |
| M8 B6 … B10 (lower) | (−298, 18), (−199, 18), (0, 18), (199, 18), (298, 18) |
| M8 B11, B12 (lateral) | (−298, 160), (298, 160) |
| Left-gauge M3 | (−199.00, 76.50) Z 123.81; (−271.31, 216.37) Z 94.08; (−126.69, 216.37) Z 94.08 |
| Tach M3 | (0.00, 71.50) Z 123.81; (−85.30, 231.94) Z 89.71; (85.30, 231.94) Z 89.71 |
| Right-gauge M3 | Mirror of left: (199.00, 76.50); (126.69, 216.37); (271.31, 216.37) |
| Toggle bushings / lever pivots | X −125 IGN, −85 FUEL, +85 TURBO, +125 OVRD; Y 46; Z 75 |
| L1 pod | X ±61; face Z 115.67 … 120.00, Y 295.68 … 308.99 |

### 2.3 Front-plane clearance register (R2, computed)

| Pair | V1 | R2 | Result |
|---|---|---|---|
| Side bezel ↔ tach bezel (minimum, incl. straight sides) | 8.25 | **8.25** (8.252) | PASS (R2-10) |
| Lateral bolts B11/B12 ↔ side bezels | 3.50 | 3.625 | PASS |
| Bottom-centre bolt B8 ↔ tray | 3.50 | 3.50 | PASS |
| Tach bezel ↔ tray | 4.00 | 4.125 | PASS |
| Side bezel top ↔ upper bolt counterbore B2/B4 | 46.5 | 32.0 | PASS |
| Tach bezel top ↔ upper-centre bolt B3 counterbore (projection; different Z) | — | 11.94 | PASS |
| Tach bezel top ↔ L1 pod (projection; different Z) | — | 13.12 | PASS |
| Toggle levers (full ±30° travel) ↔ any bezel | — | ≥ 56 | PASS |

---

## 3. Side section and depth references (option C)

### 3.1 Raked reference planes

For a gauge with bottom edge Y_b (85.0 side, 80.0 tach) and tan 12° = 0.21256:

```
Z_lens_inner(y)  = 118 − (y − Y_b) · 0.21256
Z_lens_outer(y)  = 120 − (y − Y_b) · 0.21256
Z_bezel_front(y) = 122 − (y − Y_b) · 0.21256
Upper relief:    opening top at depth Z = (centre + R) + (Z − 42) · 0.32492
```

Planes are uniform across X (raked about a horizontal axis). The dial (Z 40 … 42) and needle plane (Z 65) are **not** raked.

### 3.2 Depth along the opening

**Side gauges (centre Y 160, R 75, Y_b 85)**

| Position | Y | Lens inner Z | Lens outer Z | Bezel front Z | Dial → bezel front | Dial → lens inner | Tunnel length |
|---|---|---|---|---|---|---|---|
| Bottom edge (reference) | 85.00 | **118.00** | **120.00** | **122.00** | **80.00** | 76.00 | 78.00 |
| Centre | 160.00 | 102.06 | 104.06 | 106.06 | 64.06 | 60.06 | 62.06 |
| Top of round bore | 235.00 | 86.12 | 88.12 | 90.12 | 48.12 | 44.12 | 46.12 |
| Top of relieved opening | 249.62 | 83.01 | 85.01 | 87.01 | 45.01 | 41.01 | 43.01 |

**Tach (centre Y 170, R 90, Y_b 80)**

| Position | Y | Lens inner Z | Lens outer Z | Bezel front Z | Dial → bezel front | Dial → lens inner | Tunnel length |
|---|---|---|---|---|---|---|---|
| Bottom edge (reference) | 80.00 | **118.00** | **120.00** | **122.00** | **80.00** | 76.00 | 78.00 |
| Centre | 170.00 | 98.87 | 100.87 | 102.87 | 60.87 | 56.87 | 58.87 |
| Top of round bore | 260.00 | 79.74 | 81.74 | 83.74 | 41.74 | 37.74 | 39.74 |
| Top of relieved opening | 272.69 | 77.04 | 79.04 | 81.04 | 39.04 | 35.04 | 37.04 |

### 3.3 Section sketch (tach, X = 0; not to scale)

```
Z:  0          40 42      65 70   78–81         98–103          118 120 122 125
    ├───────────┼──┼───────┼──┼─────┼──────────────┼────────────────┼───┼───┼───┤
    [BULKHEAD ]
                [D] dial (flat, Z40–42)
                        [N] needle plane Z65, hub to Z70
     top of opening ──────────────────► Z81.04 (opening top Y272.69; thinned bezel top Y282.56)
                                    ╲ raked lens/bezel planes, 12°
     centre ─────────────────────────────────► Z102.87 (bezel front at Y170)
                                                     ╲
     bottom edge ───────────────────────────────────────────► Z118 / 120 / 122
                                                               bezel outer bottom Z124.74
    VISOR: underside Y320 @ Z40 → Y285.66 @ Z125 ; L1 pod on top near the tip
```

### 3.4 Z clearances

| Measure | Side | Tach |
|---|---|---|
| Needle / hub ↔ lens inner (minimum over sweep) | 22.17 | 15.79 |
| Bezel outer top ↔ visor underside (at the bezel's top front edge) | 39.61 | 21.70 (thinned rim) |
| Bezel lower outer edge ↔ envelope | 0.26 nominal / 0.161 worst case (§15.1) | same |
| Lens dome apex | ≈ 1 mm in front of the lip plane at centre (as in V1) | same |

### 3.5 Visibility at the 18° design eye (ray-traced)

| | Side dials | Tach dial | Needle tips |
|---|---|---|---|
| V1 | 78.1 % | 81.7 % | Hidden ±53° / ±52° from 12 o'clock, up to 6 mm |
| **R2 (option C)** | **100.0 %** | **99.9 %** (top 1.3 mm hidden by the visor; accepted, R2-11) | **Fully visible** across 270° |

**Robustness to eye elevation** (fixed R2 geometry; relief designed for 18°):

| Eye elevation | 0° | 10° | 14° | 18° | 20° | 22° | 25° | 28° |
|---|---|---|---|---|---|---|---|---|
| Side dials | 100 | 100 | 100 | 100 | 98.4 | 96.9 | 94.4 | 91.7 |
| Tach | 100 | 100 | 100 | 99.9 | 98.4 | 96.9 | 94.3 | 91.5 |
| Needle tips | visible | visible | visible | visible | visible | visible | visible | visible |

---

## 4. Five-stratum exploded assembly (R2)

### 4.1 Strata

| Stratum | Contents | Class | Roblox parts |
|---|---|---|---|
| **S01 Housing** | Bulkhead, counterbore bands, visor with **L1 pod**, tray, serial plate, **4 toggle bushings**; 12 M8 heads; **4 levers**; 9 lamps | **Fixed** (levers animate; geometry fixed) | `Housing`, `Fasteners`, `Lever_*` ×4, `LED_*` ×9 |
| **S02 Tunnels** | Three bores with upper 18° relief, **front ends on the 12° raked plane**, 3 retention lugs each; cast with S01 | **Fixed** | Merged into `Housing` |
| **S03 Dials** | Flat keyed plates, Z 40 … 42 | **Swappable (texture only)** | `Dial_L/C/R` |
| **S04 Needles** | Blade, tail, hub, spindle | **Swappable** | `Needle_L/C/R` |
| **S05 Lens and bezel** | **Raked 12° stadium** lens; raked stadium bezel with 3 × M3 | **Swappable** | `Lens_L/C/R`, `Bezel_L/C/R` |

### 4.2 Bezel retention detail (physical spec; hidden parts not modeled in the render mesh)

- **Lugs:** three cast lugs on each tunnel exterior at the screw positions. Radial extent R + 5 … R + 11.5; at least 8 deep along Z, ending at the lens-outer plane.
- **Bezel pockets:** each bezel has matching internal pockets in its skirt. They key the bezel's orientation, so it cannot be fitted rotated.
- **Screws:** M3 × 10 countersunk, head Ø6 on the rim (R + 5.5 … R + 11.5, inside the 12.875 rim). The shank (R + 7 … R + 10) clears the lens edge (R + 4.75) by 2.25. Thread engagement ≈ 7 (≥ 2 × d).
- **Lens:** sits on the tunnel's raked end face (5 mm wall). It is clamped through a 1.0 mm closed-cell silicone foam gasket compressed to 0.6, under a **1.4 mm** bezel lip. Overlap is ≥ 3.53 at the top and 4.75 elsewhere. Plane references are unchanged: lens 118 … 120, gasket 120 … 120.6, lip 120.6 … 122 at the bottom edge.
- **Axial location:** the bezel is located by its rear face on the three **machined lug stop faces** (metal to metal), not by the lens stack. This keeps the envelope chain short (§15.1).
- **Threads:** M3 wire thread inserts in the aluminium lugs for repeated service.
- **Tach top rim:** 9.875 within ±35° of 12 o'clock (R2-12).

---

## 5. Triangle budget (R2) — confirmation

| Roblox part | Contents | Tris | Class |
|---|---|---|---|
| Housing | Bulkhead front face 372; back and edges 22; counterbore bands 384; visor 12; tray 10; serial plate 10; tunnels 3 × 192 = 576; toggle bushings 4 × 46 = 184; L1 frame + wedge 18 | **1,588** | Fixed |
| Fasteners | 12 × 38 (option B) | **456** | Fixed |
| Lever_IGN / _FUEL / _TURBO / _OVRD | 4 × (lever 12 + tip 24) | **144** | Fixed (animated) |
| LED_1 … LED_9 | 9 × 10 | **90** | Fixed |
| **Fixed subtotal** | | **2,278** | |
| Dial_L/C/R | 3 × 48 | 144 | Swappable |
| Needle_L/C/R | 86 + 110 + 86 | 282 | Swappable |
| Lens_L/C/R | 3 × 144 (48-segment raked stadium dome) | 432 | Swappable |
| Bezel_L/C/R | 3 × 384 (48-segment raked stadium band; M3 heads in texture) | 1,152 | Swappable |
| **Swappable subtotal** | | **2,010** | |
| **Base total** | | **4,288** | ≤ 4,850 (562 reserve) |
| **Worst case** (needles 150, lenses 144, bezels 438, dials 48 each) | 2,278 + 2,340 | **4,618** | ≤ 4,850 (232 reserve) |

**Why option C costs 0 triangles:**
- Every stadium outline (bore, tunnel OD, lens, bezel) keeps exactly 48 segments: two 23-segment arcs plus two straight segments.
- The rake changes vertex positions, not counts.
- The tunnel bore and OD stay ruled surfaces between a 48-vertex ring at Z 40 and a 48-vertex ring on the raked plane: 96 + 96 = 192 per tunnel, as in V1.
- Facet error with 23 segments per half-circle: 0.240 at R 102.875, 0.210 at R 90, 0.175 at R 75. All are ≤ 0.25.
- Lugs, pockets and M3 shanks are hidden and not modeled; M3 heads are texture.

**V1 → R2 reconciliation:** 4,280 + 184 (bushings moved into Housing) − 328 (old merged `Toggles` part) + 144 (four levers) + 18 (L1 frame and wedge) − 10 (old shift frame) = **4,288**. Worst case 4,610 + 8 = **4,618**.

---

## 6. Roblox assembly — 27 parts

| # | Part | Joint to Housing | Moves at runtime |
|---|---|---|---|
| 1 | `Housing` (PrimaryPart; includes S02 tunnels, bushings, L1 pod frame) | — | No |
| 2 | `Fasteners` (12 M8 heads, one mesh) | Weld | No |
| 3 | `Lever_IGN` | Motor6D | Yes (±30°) |
| 4 | `Lever_FUEL` | Motor6D | Yes |
| 5 | `Lever_TURBO` | Motor6D | Yes |
| 6 | `Lever_OVRD` | Motor6D | Yes |
| 7–15 | `LED_1` … `LED_9` | Weld | Colour/material state only |
| 16–18 | `Dial_L`, `Dial_C`, `Dial_R` | Weld | No (texture swap) |
| 19–21 | `Needle_L`, `Needle_C`, `Needle_R` | Motor6D | Yes (spring) |
| 22–24 | `Lens_L`, `Lens_C`, `Lens_R` | Weld | No |
| 25–27 | `Bezel_L`, `Bezel_C`, `Bezel_R` | Weld | No |

**Why four animated levers take the count from 24 to 27:**
- A Roblox MeshPart moves only as one rigid body. In V1 the four toggles were one merged part (`Toggles`), so they could only move together.
- Animating each lever independently needs each lever to be its own part with its own joint. One part becomes four: **24 − 1 + 4 = 27**.
- The static bushings were merged into `Housing`, so they add no part.
- Joints: **7 Motor6D** (3 needles + 4 levers). Every other part is welded.

---

## 7. Fixed-versus-swappable interfaces (R2 updates)

| Interface | R2 requirement |
|---|---|
| I-01 Mounting | V1 unchanged (12 × M8) |
| I-02 Tunnel (fixed) | Bore R 75 / 90 at V1 centres; floor Z 40; upper half relieved per §3.1; front end on Z_lens_inner(y); 3 lugs per tunnel at §2.2 positions. **One casting for every vehicle.** |
| I-03 Dial | **Unchanged from V1:** flat Ø150.0 / 180.0 render, Z 40 … 42, key at 6 o'clock; texture-only variants; roughness 0.70 / 0.55 |
| I-04 Needle | Unchanged from V1 (origin on axis at Z 65; zero pose −135°; ≤ 150 tris; tip ≤ 68 / 83). Lens clearance ≥ 15.79 |
| I-05 Lens | Raked 12° stadium per §1.2; rim 2.00 ± 0.03; dome sag ≤ 3.0; seated through the 1.0 foam gasket (§4.2); ≤ 144 tris; 48-segment outline |
| I-06 Bezel | Raked 12° ± 0.05°; stadium; OD ≤ 175.75 / 205.75 (raised by e_f); tach top rim 9.875 within ±35°; lip 1.4; depth 19.00 ± 0.05 from the stop face; lip opening exactly per §1.2; lower edge ≤ Z 124.84 worst case; 3 × M3 pattern, lug stops and pockets per §4.2; ≤ 438 tris; non-rotating |
| I-07 Telemetry | V1 (vehicle attributes) plus lever states as attributes `ToggleIgnition`, `ToggleFuelPump`, `ToggleTurboDump`, `ToggleOverride` |
| I-08 Lever (new) | Pivot at the bushing centre (§2.2), rotation about +X, travel −30° (off) … +30° (on), length 20, ≤ 36 tris; `CanQuery = true` for interaction |

---

## 8. Coordinates and scale

Unchanged from V1 §7 (Blender B = (Sx, −Sz, Sy); 1 BU = 1 m with mm display; **1 stud = 0.28 m provisional** until vehicle-fit testing; one uniform scale factor).

R2 additions:
- **Lever origins (Blender, mm):** (−125, −75, 46), (−85, −75, 46), (85, −75, 46), (125, −75, 46).
- **Needle origins unchanged:** (−199, −65, 160), (0, −65, 170), (199, −65, 160).

---

## 9. Dynamics and lamp logic

### 9.1 Needles
V1 §8 unchanged: second-order spring, 1/240 s fixed sub-steps, hard 0 … 270° clamp, per-gauge defaults.

### 9.2 Shift lights (approved)

| Lamp | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---|---|
| Colour | G | G | G | A | A | A | R | R | R |
| On at RPM | 5,500 | 6,000 | 6,500 | 7,000 | 7,333 | 7,667 | 8,000 | 8,667 | 9,333 |
| Off below RPM | 5,350 | 5,850 | 6,350 | 6,850 | 7,183 | 7,517 | 7,850 | 8,517 | 9,183 |

- **Flashing:** all nine lamps flash at 2.5 Hz, 50 % duty, at ≥ 9,500 RPM; flashing stops below 9,350.
- **Player setting "Reduce flashing":** lamps stay steady.
- **Input:** raw RPM.

### 9.3 Toggle levers
- **Motion:** each lever is driven by the same fixed-step spring as the needles (f_n 12 Hz, ζ 0.5, ≈ 0.08 s snap; stability ω·h = 0.31 < 2), with a target of −30° or +30°.
- **Replication:** state is stored in vehicle attributes so all players see the same lever positions.

---

## 10. Removal, maintenance and individual replacement

| Step | Side gauges | Tach |
|---|---|---|
| 1. Remove 3 × M3 (screwdriver along the raked-face normal) | Tool paths are clear; the upper screws' tool axis reaches Z 125 at Y 222.9 (visor 285.66) | Clear; reaches Z 125 at Y 239.4 |
| 2. Withdraw bezel | **Straight pull along +Z.** Clears the visor tip by 23.16 (min 22.71) | **Straight pull along +Z** with the thinned top rim (R2-12): clears the visor tip by **3.09** (min **2.64** with tolerances). Fallback if R2-12 were reverted: pull 8, lower ≥ 3, withdraw |
| 3. Remove lens | Straight pull; clears | Straight pull; top Y 276.22, clears the visor tip by 9.44 |
| 4. Remove needle | Pull off the spindle | Same |
| 5. Remove dial | Lift out along Z through the 150-wide opening (dial 149.5) | Same through 180 (dial 179.5) |
| Refit | Reverse; the dial key and the bezel lug pockets give fixed orientation | Same |

**Conclusions:**
- Every gauge can be serviced and replaced on its own, without disturbing the other gauges, the housing, the visor, the L1 pod or the levers.
- With R2-12, all three bezels come off with a single straight pull, and every clearance stays positive at worst-case tolerances (§15.4).
- In Roblox, swapping parts at runtime is unaffected by these physical steps.

---

## 11. Interchangeability and the universal housing

- **One housing for every vehicle.** The 12° rake, the 18° relief, the lugs and the tunnel ends are identical on every unit. No per-vehicle housing variant exists or is needed.
- **Left and right side gauges are geometrically identical:**
  - same bore, relief (14.62), rake, lug pattern and bezel/lens shape;
  - their dials, needles, lenses and bezels can swap between the two positions;
  - the tach uses its own size class (Ø180).
- **Dials (S03) are unchanged from V1:** flat, keyed, texture-only. Every dial texture variant fits every housing. The rake does not touch the dial interface.
- **Needles (S04) are unchanged from V1.**
- **Lenses and bezels (S05):** one interface per size class (§7 I-05, I-06). Every variant must follow the raked stadium form and the M3 pattern. Variants differ in texture, finish or permitted silhouette within the caps.
- **Remaining per-vehicle variable:** the actual driver eye elevation. Visibility is 100 % up to 18°, then degrades gradually (§3.5). The housing stays the same.

---

## 12. Validation register (R2 changes)

V1 §9 items V-01 … V-20 still apply. Untested items stay untested. R2 updates:

| ID | Item | Class | Status |
|---|---|---|---|
| V-10 | Shift-light visibility | A (resolved by L1) + B | Pod face-on at 18°; in-vehicle camera test pending |
| V-18 | Shift thresholds / flash | Closed (approved R2-03, R2-04) | — |
| V-19 | Toggle animation | Closed (approved R2-05); B: click and animation test | Pending test |
| V-20 | Dial roughness | Closed (approved R2-06) | — |
| V-21 | Raked stadium lens and Glass material appearance | B | Not tested |
| V-22 | Driver eye elevation per vehicle | C + B | Housing designed for 18°; check each vehicle's seat |
| V-23 | Tach bezel removal (physical maintenance only) | A | Straight pull with R2-12 (§10); two-step kept as fallback |
| V-24 | Stadium texture mapping for lens/bezel variants (UV layout) | B | Not tested |
| V-25 | Lens gasket compression and lens retention (physical prototype) | B | Not tested; calculated range in §15.2 |
| V-26 | Bezel structural check with the thinned rim (physical prototype or FEA) | B | Hand calculation only (§15.3); not tested |

---

## 13. Decision record and risks

| ID | Item | Status |
|---|---|---|
| D-1 | R2 replaces V1 as the governing engineering specification | **Approved** (V1 preserved as history) |
| D-2 | Thinned tach top rim (9.875) | **Approved**; validated analytically (§15.3) |
| D-3 | 18° design eye elevation for every RAZUM vehicle | **Approved** |
| D-4 | Bezel bears on machined lug stops; no structural load into the lens | **Approved** |
| D-5 | 1.0 → 0.6 silicone foam gasket; 1.4 bezel lip | **Approved**; material grade pending (§16, P-01) |
| D-6 | Visor tip Z 125.00 +0 / −0.30 | **Approved** |
| D-7 | §15.5 tolerance table is the R2 dimensional reference | **Approved** |

| Risk | Description | Control |
|---|---|---|
| R-1 | Envelope margin 0.161 worst case at the bezel's lower outer edge | Critical: dimensional inspection (C-1, §16 P-02) |
| R-2 | Worst-case triangle reserve 232 | Variants must stay within slot caps (§5) |
| R-3 | Bezel strength and stiffness only estimated analytically | Physical or FEA validation (C-2, §16 P-03) |
| R-4 | Gasket material not yet specified | Specification before manufacture (C-3, §16 P-01) |
| R-5 | All Roblox behaviour untested | §16 Roblox tests (C-4) |

## 14. Self-check record

All values were computed by the R2 geometry, sight-line and tolerance scripts, not hand-estimated:
- **Dimensions and clearances:** every clearance in §2.3, §3.4 and §15.4 stays positive at worst-case tolerance. The envelope holds with 0.161 margin.
- **Triangle totals:** 4,288 / 4,618 (§5). The rim thinning moves vertices only, so the count is unchanged.
- **Part count:** 27 (§6).
- **Depth references:** §3.2.
- **Visibility:** §3.5. The rim thinning is outside the opening, so visibility is unchanged.

**Contradictions checked:**
- Z 118 / 120 / 122 appear only as bottom-edge references. The gasket and the 1.4 lip sit between 120 and 122, so all three planes are unchanged.
- Bezel OD 175.75 / 205.75 is used everywhere; the tach top is 282.56 everywhere.
- The two-step tach removal appears only as a fallback.

**Not done (by instruction):** no Blender installation, no geometry, no modeling, V1 preserved, no commit or push.

**Final consistency check (R2 final):** no item remains in PROPOSED status; every approved decision D-1 … D-7 appears in §0.1 and §13; conditions C-1 … C-4 map to pending requirements in §16.

---

## 15. Final tolerance and structural audit

**The §15.5 table is the approved dimensional reference of R2 (D-7).** Tolerances are physical-part values (die-cast with machined datum features). The Roblox render mesh uses nominal values.

### 15.1 Envelope stack (bezel lower outer edge, nominal Z 124.737)

| Chain element | Nominal | Tolerance |
|---|---|---|
| Lug stop faces (machined, same setup as the lens seat), at the bottom-edge reference | Z 103.00 | +0.00 / −0.10 |
| Bezel depth, stop face → front face | 19.00 | ±0.05 |
| Lower rim width × tan(rake) | 12.875 × tan 12° = 2.737 | rim ±0.05, rake ±0.05° |
| Front-face flatness | — | 0.03 |
| **Result** | **124.737** | **min 124.534 / max 124.839 → margin 0.161 to Z 125** |

- **Finding:** locating the bezel on the lens stack (seat + lens + lip, each ±0.10, rake ±0.25°) reaches Z **125.117**, which exceeds the envelope by 0.117. Hence D-4: locate the bezel on the lug stops.
- **Finding:** the visor tip defines the envelope itself, so it must carry a unilateral tolerance, **125.00 +0 / −0.30** (D-6).

### 15.2 Lens clamp under real tolerances

- **The problem:** the lens seat (S02) and the bezel lip (S05) are separate raked 12° faces. A combined angle mismatch of 0.05° across the ≈ 207 mm lens height opens a gap variation of 0.18. A rigid glass-to-metal clamp would leave the lens rocking or point-loaded.
- **The fix:** a 1.0 closed-cell silicone foam gasket (working range ≈ 20–70 %), compressed to 0.6 nominal (40 %). Contributors: seat-to-stop ±0.03, bezel stop-to-lip ±0.03, lens ±0.03, angle mismatch 0.18.
- **Compression range:** 28 – 52 % (statistical, RSS) and 13 – 67 % (worst case). The lens stays clamped at every corner.
- The bezel lip becomes 1.4 (was 2.0). The 118 / 120 / 122 references are unchanged.

### 15.3 Thinned tach top rim (D-2) — validation

Model: hand calculation treating the rim between the ±60° screws (arc ≈ 207 mm) as a fixed-fixed beam. The section is the lip (1.4 axial) plus the skirt (to 19 deep); aluminium 6061-T6 (E 68.9 GPa, yield 276 MPa). Conservative: the thinned section is assumed over the whole span.

| Check | Full rim 12.875 | Thinned 9.875 | Requirement | Result |
|---|---|---|---|---|
| Section area | 156.6 mm² | 99.6 mm² (64 %) | — | — |
| Remaining skirt wall (radial) | 7.875 | **4.875** (≈ 4.4 under 0.5 knurl) | ≥ 2.5 (die-cast) / ≥ 1.5 (machined) | PASS |
| Bending stiffness I | 5,020 mm⁴ | 3,292 mm⁴ (66 %) | — | — |
| Stress, 500 N hand load at mid-span | 25.5 MPa (SF 10.8) | **39.8 MPa (SF 6.9)** | SF ≥ 3 | PASS |
| Deflection, 500 N | 0.067 | **0.102** | ≤ 0.2 | PASS |
| Gasket load (≈ 1 N/mm) | 7.1 MPa / 0.014 | 11.0 MPa / 0.021 | — | PASS |
| First bending mode | ≈ 2.4 kHz | ≈ 2.4 kHz | ≫ 200 Hz vehicle vibration | PASS |

- **Appearance:** the tach rim narrows from 12.875 to 9.875 over the top 70° with 10° tapers. It sits under the visor's shadow line and reads as a deliberate brow relief, in keeping with the cut-steel language of `DESIGN.md`. The other two bezels and the rest of the tach rim are unchanged.
- **Manufacture:** CNC toolpath change only, or ≥ 2.5 mm wall if die-cast. Knurling stays possible. 0 triangles.
- **Conclusion: no structural compromise.** The two-step removal stays documented only as a fallback.

### 15.4 Assembly and disassembly with real tolerances

| Step | Interface | Nominal | Worst case | Result |
|---|---|---|---|---|
| Fit bezel | Pockets over lugs: 0.10 clearance per side (machined lug faces) | 0.10 | 0.00 (line fit) | PASS |
| Fit bezel | M3: Ø3.4 clearance hole vs tapped hole, position ±0.10 each (floating fastener) | 0.20 | 0.00 | PASS |
| Fit lens | Lens outline vs skirt inner | 0.25 radial | 0.15 | PASS |
| Clamp lens | Gasket compression | 40 % | 13 – 67 % | PASS (§15.2) |
| Remove tach bezel (straight) | Bezel top vs visor tip | 3.09 | 2.64 | PASS |
| Remove side bezels | Bezel top vs visor tip | 23.16 | 22.71 | PASS |
| Remove tach lens | Lens top vs visor tip | 9.44 | 9.04 | PASS |
| Remove dial | Dial Ø179.5 (0 / −0.10) through bore Ø180.0 (+0.10 / 0) | 0.50 Ø | 0.30 Ø | PASS |
| Running | Needle/hub ↔ lens (tach) | 15.79 | 15.47 | PASS |
| Running | Bezel ↔ bezel | 8.25 | 7.85 | PASS |
| Running | Lateral bolt ↔ side bezel | 3.625 | 3.33 | PASS |
| Running | Tach bezel ↔ tray | 4.125 | 3.68 | PASS |

No collisions between bezel, lens, visor and instruments in any step at worst-case tolerances.

### 15.5 Final tolerance table — R2 dimensional reference (approved, D-7)

Features marked **CRITICAL** require 100 % dimensional inspection (C-1).

| Feature | Nominal | Recommended tolerance | Min | Max | Limit / requirement | Remaining margin (worst case) |
|---|---|---|---|---|---|---|
| Visor tip Z (envelope) — **CRITICAL** | 125.00 | +0 / −0.30 (D-6) | 124.70 | 125.00 | ≤ 125 | 0 (by definition) |
| Bezel lower outer edge Z — **CRITICAL** | 124.737 | stack §15.1 | 124.534 | 124.839 | ≤ 125 | **0.161** |
| Lug stop faces Z (bottom ref.) — **CRITICAL** | 103.00 | +0 / −0.10 | 102.90 | 103.00 | stack | — |
| Bezel depth (stop → front) — **CRITICAL** | 19.00 | ±0.05 | 18.95 | 19.05 | stack | — |
| Lens seat Z (bottom ref.) | 118.00 | ±0.03 rel. to lug stops | 117.97 | 118.03 | gasket range | — |
| Lens rim thickness | 2.00 | ±0.03 | 1.97 | 2.03 | gasket range | — |
| Gasket compressed thickness | 0.60 | ±0.27 (wc) / ±0.12 (RSS) | 0.33 | 0.87 | 0 < gap < 1.0 | 0.13 / 0.33 |
| Bezel lip thickness | 1.40 | ±0.05 | 1.35 | 1.45 | — | — |
| Rake (seat, lug stops, bezel face) — **CRITICAL** | 12.00° | ±0.05° | 11.95° | 12.05° | envelope, gasket | in stacks |
| Tunnel relief profile (cast) | per §3.1 | +0.25 / −0 (outward only) | nominal | +0.25 | 100 % dial visibility | 0.25 |
| Gauge axis positions | V1 | ±0.05 (machined) | — | — | bezel gap | in gap |
| Bezel OD | 175.75 / 205.75 | ±0.10 | −0.10 | +0.10 | bezel gap | in gap |
| Bezel radial float on lugs | 0 | ±0.10 | −0.10 | +0.10 | bezel gap | in gap |
| Bezel-to-bezel gap | 8.25 | derived | 7.85 | 8.65 | > 0 | **7.85** |
| Lateral bolt ↔ side bezel | 3.625 | derived (bolt position ±0.10) | 3.33 | 3.93 | > 0 | **3.33** |
| Tach bezel ↔ tray | 4.125 | derived (tray ±0.25 cast) | 3.68 | 4.58 | > 0 | **3.68** |
| Tach top rim width | 9.875 | ±0.10 | 9.775 | 9.975 | wall ≥ 2.5 | 2.28 (wall) |
| Tach straight-pull clearance | 3.09 | derived (visor ±0.25) | 2.64 | 3.54 | > 0 | **2.64** |
| Side straight-pull clearance | 23.16 | derived | 22.71 | 23.61 | > 0 | **22.71** |
| Needle ↔ lens (tach / side) | 15.79 / 22.17 | derived (needle plane ±0.10) | 15.47 / 21.85 | — | ≥ 3 | **12.47 / 18.85** |
| Dial ↔ bore (diametral) | 0.50 | dial 0 / −0.10, bore +0.10 / 0 | 0.30 | 0.70 | > 0 | **0.30** |
| M8 counterbore Ø | 15.00 | +0.10 / 0 | 15.00 | 15.10 | head Ø15 render | — |
| M3 clearance hole | Ø3.40 | +0.10 / 0 | 3.40 | 3.50 | floating fastener | 0 |

---

## 16. Pending requirements for the next stages

None of these blocks closing the engineering stage. Each one must be closed before the stage named in its "Gate" column.

### 16.1 Physical / manufacturing

| ID | Requirement | Source | Gate |
|---|---|---|---|
| P-01 | **Gasket material specification:** silicone foam grade, hardness (target range to be set), compression set, operating temperature range, UV/ozone and ageing resistance, adhesive or loose fit | C-3, D-5 | Before manufacture |
| P-02 | **Dimensional inspection plan** for the critical envelope chain (§15.1: lug stop Z, bezel depth, rake, rim width, front-face flatness) and the visor tip (+0 / −0.30); 100 % inspection while the margin is 0.161 | C-1, D-6 | Before manufacture / first article |
| P-03 | **Structural validation of the bezel** (thinned tach top rim): FEA or a physical test of handling load (500 N), clamp load and vibration | C-2, D-2 | Before manufacture |
| P-04 | Gasket compression and lens retention test on a prototype (range 13–67 % worst case) | §15.2, V-25 | Before manufacture |
| P-05 | Bezel and lug material and finish (6061-T6 assumed; anodizing, knurl depth ≤ 0.5) | §15.3 | Before manufacture |
| P-06 | M3 wire thread insert type and installation spec | §4.2 | Before manufacture |

### 16.2 Roblox / digital asset (none validated — C-4)

| ID | Requirement | Ref. | Gate |
|---|---|---|---|
| G-01 | Owner authorization to start modeling (Blender install, geometry) | — | Before modeling |
| G-02 | FBX axis-marker test (axes, mirroring, 3.5714-stud cube) | V-01, V-02 | Before production export |
| G-03 | Vehicle and avatar fit at 0.28 m/stud (provisional) | V-13 | Before production export |
| G-04 | Target mobile devices confirmed; profile 60 FPS (mid tier) / ≥ 30 FPS (low tier) | V-12 | Before release |
| G-05 | Materials: Glass lens, reflectance mapping, emissive or Neon lamps, SurfaceAppearance maps | V-03 … V-05, V-21 | Before release |
| G-06 | Texture resolution and memory budget measured on device (≤ 35 MiB uncompressed estimate) | V-06, V-07 | Before release |
| G-07 | Runtime swap of dials, needles, lenses and bezels without rebuilding Housing | V-08 | Before release |
| G-08 | Needle and lever spring stability at 30/60/120/240 FPS and frame hitches; lever click interaction | V-09, V-19 | Before release |
| G-09 | Shift-light visibility from the real seat camera (L1 pod) | V-10 | Before release |
| G-10 | Collision, query and level-of-detail settings | V-11, V-16 | Before release |
| G-11 | Exported triangle count ≤ 4,288 base / ≤ 4,618 worst case | V-14 | Before production export |
| G-12 | Client-side Motor6D updates for driver, passenger and observer | V-15 | Before release |
| G-13 | Stadium and raked UV layouts for lens and bezel variants | V-24 | Before variant production |

### 16.3 Engineering stage closure

| Item | State |
|---|---|
| Engineering specification | **R2 final approved** (this document) |
| V1 | Preserved unchanged (historical baseline) |
| Modeling | **Not authorized**; requires G-01 |
| Repository | Documents not committed or pushed (owner instruction) |
