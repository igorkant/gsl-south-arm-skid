# Great Salt Lake DLE Pilot — South Arm

Interactive 3D visualisation of the XtraLit direct-lithium-extraction pilot on the Gilbert Bay (South Arm) of the Great Salt Lake, Utah. Feed Li ≈ 25 ppm.


## The skid

One skid, built like a factory ultrafiltration unit, carries the whole process side:

- **P-101** — the single brine pump, drawing from the accumulation pond.
- **Filtration train** — 50 µm mesh strainer → 10 µm cartridge → 1 µm cartridge → UF.
  UF concentrate and backwash go to the Spent Brine tank.
- **PT-101** after the UF and **NMR-in** — on-line lithium analyser on the feed.
- **Valve battery** — brine, water and acid feed headers, spent / eluate / sulfate
  collect headers, and 6 actuated valves per column (48 in all) driven by the PLC.
  All valves sit in the battery at the headers, none on the column: brine → the
  column's brine line; water or acid → its service line (both feeds join after their
  valves); its outlet line → spent, eluate or sulfate.
- **Three pipes per column** — brine line and service line on top (they tee at the
  single top nozzle), one outlet line from the bottom nozzle back to the battery.
- **8 radial columns** (~20 L, 20 kg LMO) in two banks of four, each with a magnetic
  flowmeter FT-1…FT-8 on its outlet line (every step passes it).
- **P-201** (water, both washes) and **P-301** (0.8 M H₂SO₄).
- **Sample selector + NMR-out** — a sample line taps every column's outlet line in
  the battery and runs under the collect headers to the selector;
  NMR-out reads the outlet Li of the columns on sorption in turn.
- **EC-101 / pH-101** on the spent and sulfate collect lines, and the **PLC cabinet**.

Six tanks stand off the skid: pond, fresh water, acid, eluate, sulfate, spent brine.

## Process

| Step | Medium | Direction | Valves (per column) | Control |
| --- | --- | --- | --- | --- |
| Sorption | Lake brine, 9 m³/h | top → down (radial) | brine in, spent out | 1.1 h, or stop on breakthrough |
| Water wash 1 | Fresh water, 9 m³/h | top → down | water in, spent out | EC to set-point |
| Desorption | 0.8 M H₂SO₄ | top → down, same way as sorption | acid in; eluate out (Fr-2/3) or sulfate out (Fr-1/4/5) | 5 timed fractions |
| Water wash 2 | Fresh water, 9 m³/h | top → down | water in, sulfate out | pH back above 6 |

Every step enters through the column's top nozzle — brine by the brine line, water
and acid by the service line — and leaves by the one outlet line at the bottom.

There is no NaCl reconditioning stage and no NaCl tank: the bed is washed with
water after desorption exactly as it is after sorption.

## Carousel

The eight columns run the same cycle shifted by one eighth of it: column N starts
(N−1)·P/8 after C1.

| | |
| --- | --- |
| Column cycle P | 2.20 h |
| Sorption | 1.10 h |
| Water wash 1 · desorption · water wash 2 | 0.20 · 0.65 · 0.25 h (regeneration 1.10 h) |
| Shift between neighbours | P/8 = 0.275 h |
| Columns on sorption | 4 (fewer while a column is on hold) |
| P-101 brine | 36 m³/h nominal = 4 × 9 m³/h (27 with one column on hold) |
| P-201 water | 0–2 washing columns at once, 0–18 m³/h |
| P-301 acid | every column desorbing at the time, up to 3 at once |
| Cycles per day | ~10.9 |
| Brine per day | ~860 m³ |

Brine flows without a break: some column is always on sorption, so P-101 never stops.

**Stop on breakthrough.** NMR-out watches the outlet of each sorbing column. When it
reaches 10 % of the feed Li (2.5 ppm), the PLC ends that column's sorption early: its valves
shut and it waits on **hold** until the end of its sorption slot. The schedule of
the following steps does not move.

## Sorption time

Sorption is timed to load the sorbent to 10–11 mg Li per g at 85 % recovery:

    t = m_sorbent x loading / (Q x C_feed x recovery)
      = 20 kg x 10.5 g/kg / (9 m³/h x 25 g/m³ x 0.85)
      = 1.10 h  (1.1 h)

The regeneration half of the cycle — both water washes and the fractionated
desorption — takes a further 1.10 h, so a full cycle runs 2.20 h:
**~10.9 cycles per day**, ~9 kg Li₂CO₃ per cycle across the eight columns
(~97 kg/day) on ~860 m³/day of brine.

Throughput is set by the sorbent inventory and the cycle count, not by the feed
grade: the richer arm loads the bed faster and so needs far less brine pumped
for the same lithium.

Derived from the Dead Sea pilot layout (igorkant/Dead-sea-pilot).

Live: https://igorkant.github.io/gsl-south-arm-skid/
