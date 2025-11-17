# Bill of Materials (BOM)
## xNAV650 to Ouster OS1 Adapter

**Project:** Time Synchronization Adapter for Ouster OS1 LiDAR with xNAV650 INS  
**Revision:** 1.1  
**Date:** 2025-11-18  
**Designer:** Vladyslav Hirchuk

---

## Purpose
This adapter enables time synchronization between the xNAV650 INS and Ouster OS1-128 LiDAR by:
- Converting RS232 NMEA messages (from xNAV650) to TTL 5V (for OS1)
- Level-shifting the PPS signal from 3.3V to 5V TTL
- Providing buffered ethernet pass-through
- Stepping down 12V input to 3.3V for logic circuits

---

## Component List

### Power Components

| Ref | Qty | Value/Part Number | Description | Package/Footprint | Notes |
|-----|-----|-------------------|-------------|-------------------|-------|
| J1 | 1 | Jack-DC | DC Power Input, 12V | BarrelJack_Horizontal | 5.5mm x 2.1mm recommended |
| U3 | 1 | OKI-78SR-3.3/1.5-W36-C | DC-DC Buck Converter, 12V→3.3V, 1.5A | Converter_DCDC_Murata_OKI-78SR_Vertical | Non-isolated switching regulator |
| C5 | 1 | 22µF | Electrolytic Capacitor, 16V | Radial D6.3mm, P2.50mm | Input bulk capacitor |
| C8 | 1 | 22µF | Electrolytic Capacitor, 16V | Radial D6.3mm, P2.50mm | Output filter capacitor |
| D1 | 1 | LED (Green) | Power Indicator LED, 3mm | LED_D3.0mm | Forward voltage ~2V |
| R1 | 1 | 220Ω | Current Limiting Resistor | Axial DIN0207, L6.3mm, P7.62mm | For LED current limiting |

### Signal Conversion Components

| Ref | Qty | Value/Part Number | Description | Package/Footprint | Notes |
|-----|-----|-------------------|-------------|-------------------|-------|
| U2 | 1 | MAX3232E | Dual RS232 Transceiver (3.3V Version) | DIP-16, 7.62mm pitch | Converts RS232 ↔ TTL logic levels |
| C1 | 1 | 100nF | Ceramic Capacitor, 50V | SMD 0805 (2012 Metric) | Charge pump capacitor for MAX3232 |
| C2 | 1 | 100nF | Ceramic Capacitor, 50V | SMD 0805 (2012 Metric) | Charge pump capacitor for MAX3232 |
| C3 | 1 | 100nF | Ceramic Capacitor, 50V | SMD 0805 (2012 Metric) | Charge pump capacitor for MAX3232 |
| C4 | 1 | 100nF | Ceramic Capacitor, 50V | SMD 0805 (2012 Metric) | Charge pump capacitor for MAX3232 |
| C7 | 1 | 100nF | Ceramic Disc Capacitor | THT Disc D3.0mm, P2.50mm | Decoupling capacitor |
| U4 | 1 | 74HC125N | Quad 3-State Buffer | DIP-14, 7.62mm pitch (DIP254P762X420-14) | Buffers PPS signal to 5V TTL |

### Connectors

| Ref | Qty | Value/Part Number | Description | Package/Footprint | Notes |
|-----|-----|-------------------|-------------|-------------------|-------|
| J2 | 1 | 15-pin Micro-D Female | Main xNAV650 Interface | DSUB-15 Horizontal, P2.77x2.84mm, EdgePinOffset7.70mm | Mates with xNAV650 user cable |
| J4 | 1 | RJ45_LED_Shielded | Ethernet + Ouster Interface | Amphenol 54602-x08 Horizontal | Combined Ethernet + power + signals |
| U1 | 1 | Ouster OS1 | LiDAR Unit (not on PCB) | — | External device, for reference only |

---

## Key Changes from Revision 1.0

### Capacitor Updates
- **C1, C2, C3, C4:** Changed from 100µF electrolytic to **100nF ceramic SMD 0805**
  - Smaller footprint, better high-frequency performance
  - Suitable for MAX3232E charge pump operation
  - Lower profile for compact PCB design

- **C5, C8:** Changed from 100µF to **22µF electrolytic**
  - Still provides adequate filtering for DC-DC converter
  - Smaller physical size (D6.3mm)
  - More cost-effective

- **C7:** New component - **100nF ceramic disc capacitor (THT)**
  - Additional decoupling for digital logic
  - Through-hole for easy assembly/replacement

### Component Updates
- **U2:** Specified as **MAX3232E** (3.3V version) instead of generic MAX3232
  - Explicitly designed for 3.3V operation
  - Lower power consumption
  - Better suited for the 3.3V system voltage

- **R1:** Increased from **100Ω to 220Ω**
  - Better current limiting for LED (≈10mA @ 3.3V)
  - Extends LED lifespan

- **D1:** Changed to **3mm LED** from 5mm
  - Smaller footprint
  - Adequate brightness for indicator

---

## Additional Materials Required (Not on PCB)

| Item | Qty | Description | Purpose |
|------|-----|-------------|---------|
| PCB | 1 | Custom PCB, 2-layer minimum | Houses all components |
| Enclosure | 1 | Plastic/aluminum project box | Weather protection, mounting |
| Cable - xNAV650 | 1 | User cable or custom 15-pin Micro-D | Connect to xNAV650 main port |
| Cable - Ethernet | 1 | Standard Cat5e/Cat6 patch cable | Ethernet pass-through |
| Cable - OS1 Power/IO | 1 | Custom cable per Ouster spec | Connect to OS1 I/O connector |
| Standoffs/Screws | 4 | M3 or #4-40, 10mm | PCB mounting in enclosure |
| Wire | — | 22-24 AWG stranded | Internal connections |
| Heat shrink tubing | — | Various sizes | Wire insulation and strain relief |

---

## Component Specifications & Notes

### Power Supply Requirements
- **Input:** 12V DC ±10% (10.8V - 13.2V acceptable)
- **Current Draw:** ~150-250mA typical (reduced from v1.0 due to smaller capacitors)
- **Output:** 3.3V @ 1.5A max (OKI-78SR capability)

### Critical Design Notes

1. **MAX3232E (U2)**
   - Operating voltage: 3.0V - 5.5V (optimized for 3.3V operation)
   - Converts xNAV650 RS232 NMEA output to TTL 5V for OS1
   - Requires four external 100nF capacitors (C1-C4) for charge pump operation
   - Lower power consumption than standard MAX3232
   - ESD sensitive - handle with care

2. **74HC125N (U4)**
   - Quad buffer with 3-state outputs
   - Used to level-shift PPS signal from 3.3V to 5V TTL
   - Enables/disables controlled via OE pins
   - Can buffer multiple signals if needed

3. **OKI-78SR-3.3 (U3)**
   - Efficient switching regulator (typically 85-90% efficiency)
   - Built-in overload and thermal protection
   - Minimal external components required (C5, C8 for filtering)
   - Compatible with wide input range (6.5V - 36V)

4. **Capacitors**
   - C1-C4: 100nF ceramic SMD 0805 (X7R or X5R dielectric recommended)
   - C5, C8: 22µF electrolytic, minimum 16V rating
   - C7: 100nF ceramic disc, through-hole
   - Ensure proper polarity on electrolytic capacitors during assembly

### Signal Connections

**From xNAV650 (J2) to Circuit:**
- Pin 3: Serial RX (RS232) → U2
- Pin 4: Serial TX (RS232) → U2
- Pin 12: PPS (3.3V isolated) → U4 buffer
- Pins 5-8: Ethernet (pass-through to J4)
- Pins 1-2, 14-15: Supply+ and Supply- (12V power)

**To Ouster OS1 (via J4):**
- NMEA_TX: TTL 5V from U2 R1OUT
- SYNC_PULSE_IN: Buffered 5V PPS from U4
- Ethernet: Pins 1-2, 3-6, 4-5, 7-8 (standard pinout)

---

## Assembly Notes

1. **Component Orientation:**
   - Pay attention to IC pin 1 indicators
   - Electrolytic capacitors (C5, C8) have polarity markings
   - LED (D1) has polarity (longer lead = anode/+)
   - SMD capacitors (C1-C4) are non-polarized

2. **Soldering Order:**
   - **SMD components first** (C1-C4) - requires reflow or hot air station
   - Then low-profile THT components (resistors, C7)
   - ICs next (or sockets if using)
   - Electrolytic capacitors (C5, C8)
   - Connectors and taller components last
   - LED and barrel jack final

3. **SMD Soldering Tips:**
   - Use solder paste and hot air station, or hand solder with fine tip
   - 0805 components are beginner-friendly for hand soldering
   - Apply flux for easier soldering

4. **Testing Before Connection:**
   - Verify 12V input polarity at J1
   - Measure 3.3V output from U3 before installing ICs
   - Check continuity on ethernet pass-through
   - Test LED operation

5. **Strain Relief:**
   - Use cable ties or clamps for all external cables
   - Ensure no mechanical stress on PCB connectors

---

## Recommended Suppliers & Part Numbers

### Mouser/Digikey Part Numbers:

| Component | Manufacturer Part # | Supplier Part # | Notes |
|-----------|-------------------|-----------------|-------|
| MAX3232E | MAX3232ECPE+ | Mouser: 700-MAX3232ECPE+ | DIP-16 package |
| 74HC125N | 74HC125N | Mouser: 771-74HC125N | DIP-14 package |
| OKI-78SR-3.3/1.5-W36-C | OKI-78SR-3.3/1.5-W36-C | Mouser: 811-OKI-78SR-3.3/1.5W36C | Vertical mount |
| 100nF SMD 0805 | Various (X7R/X5R) | Search: "0805 100nF X7R" | Buy 10+ for spares |
| 22µF Electrolytic | Panasonic/Nichicon | Radial, 16V min | Standard grade OK |
| 220Ω Resistor | Various | 1/4W, 5% tolerance | Metal film preferred |
| LED 3mm | Various colors | Green recommended | Diffused lens |
| Micro-D 15-pin | Varies by manufacturer | Amphenol, Norcomp, etc. | Right-angle mount |
| RJ45 Shielded | Amphenol 54602-x08 | Check specific variant | LED integrated |

---

## Cost Estimate (Approximate, USD)

| Category | Estimated Cost | Notes |
|----------|---------------|-------|
| ICs (U2, U3, U4) | $15 - $25 | Similar to v1.0 |
| SMD Capacitors (4× 100nF) | $1 - $3 | Much cheaper than electrolytics |
| THT Capacitors (C5, C7, C8) | $1 - $2 | Reduced from v1.0 |
| Resistor & LED | $0.50 - $1 | Unchanged |
| Connectors (J1, J2, J4) | $10 - $20 | Unchanged |
| PCB (prototype, single unit) | $20 - $50 | Unchanged |
| Enclosure + hardware | $10 - $30 | Unchanged |
| Cables & misc | $15 - $30 | Unchanged |
| **Total per unit** | **$70 - $155** | Slightly lower due to cheaper caps |

*Bulk pricing will significantly reduce per-unit costs. SMD components offer better pricing at volume.*

---

## PCB Design Considerations

### Component Placement (From Your Schematic)
- **Area:** Approximately 228mm × 141mm board
- **Power section:** Left side (J1, U3, C5, C8, R1, D1)
- **Serial interface:** Center (U2, C1-C4)
- **Digital buffer:** Center-right (U4, C7)
- **Connectors:** J2 on left edge, J4 on right edge

### Design Tips
1. Keep SMD capacitors (C1-C4) close to MAX3232E pins
2. Short traces from U3 to C5 and C8 for stable power
3. Separate analog (RS232) and digital (buffer) ground planes if possible
4. Add mounting holes near corners for M3 standoffs
5. Consider copper pour for GND to reduce EMI

---

## Revision History

| Rev | Date | Changes | Author |
|-----|------|---------|--------|
| 1.0 | 2025-11-14 | Initial release | Vladyslav Hirchuk |
| 1.1 | 2025-11-18 | Updated capacitor values and packages; specified MAX3232E; adjusted resistor value; added C7 | Vladyslav Hirchuk |

---

## Additional Resources

- [xNAV650 Hardware Manual](https://www.datrontechnology.co.uk/wp-content/uploads/2021/03/xNAV650-manual-210311.pdf)
- [Ouster OS1 Documentation](https://ouster.com/downloads)
- [MAX3232E Datasheet](https://www.ti.com/product/MAX3232E)
- [74HC125 Datasheet](https://www.ti.com/product/SN74HC125)
- [OKI-78SR Datasheet](https://www.murata.com/products/productdata/8807031734302/oki-78sr.pdf)

---
