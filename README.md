# xNAV650 to Ouster OS1 Adapter

**Time Synchronization Interface for Precision LiDAR Mapping**

![Project Status](https://img.shields.io/badge/status-stable-green)
![License](https://img.shields.io/badge/license-MIT-blue)
![Hardware](https://img.shields.io/badge/hardware-open-orange)

---

## 📋 Overview

This project provides a complete hardware adapter solution to interface the **OxTS xNAV650 GPS/INS** system with **Ouster OS1 LiDAR** sensors. The adapter enables precise time synchronization via PPS (Pulse Per Second) signals and NMEA data transmission, critical for accurate georeferenced point cloud generation in autonomous vehicle and mobile mapping applications.

### Why This Adapter?

The xNAV650 outputs RS232 signals at 3.3V logic levels, while the Ouster OS1 requires TTL 5V signals. This adapter bridges the gap by:

- Converting RS232 NMEA messages to TTL 5V logic
- Level-shifting PPS synchronization signals from 3.3V to 5V
- Providing stable 5V power regulation from 12V vehicle supply
- Offering a compact, ruggedized enclosure for field deployment
- Enabling plug-and-play operation with standard connectors

---

## ✨ Features

- ✅ **RS232 to TTL Conversion** - MAX3232 transceiver for NMEA data
- ✅ **PPS Signal Buffering** - 74HC125 quad buffer for 5V TTL output
- ✅ **Power Regulation** - OKI-78SR switching regulator (12V → 3.3V, 1.5A)
- ✅ **Compact Design** - 90×60×30mm enclosure fits in tight spaces
- ✅ **Standard Connectors** - Micro-D 15-pin (xNAV650), RJ45 (Ouster)
- ✅ **Visual Feedback** - Power indicator LED
- ✅ **Ethernet Pass-through** - Maintains network connectivity
- ✅ **Field-Ready** - Designed for vibration and outdoor use

---

## 🛠️ Project Components

### 📁 Repository Structure

```
xNAV650-Ouster-Adapter/
├── hardware/
│   ├── schematics/
│   │   └── XNAVOUSTER.kicad_sch      # KiCad schematic
│   ├── pcb/
│   │   └── XNAVOUSTER.kicad_pcb      # PCB layout (if available)
│   └── gerbers/                       # Manufacturing files
├── enclosure/
│   ├── 3d-models/
│   │   ├── bottom.stl                 # 3D printable base
│   │   ├── lid.stl                    # 3D printable lid
│   │   └── complete.step              # Editable CAD file
│   └── drilling-template.pdf          # For off-the-shelf enclosures
├── docs/
│   ├── BOM.md                         # Bill of Materials
│   ├── assembly-guide.md              # Step-by-step assembly
│   └── user-manual.pdf                # Operation instructions
├── firmware/                          # (Future: microcontroller config)
├── examples/                          # Sample configurations
└── README.md                          # This file
```

---

## 🔧 Hardware Specifications

### Electrical

| Parameter | Value |
|-----------|-------|
| **Input Voltage** | 12V DC ±10% (10.8V - 13.2V) |
| **Current Draw** | 200-300mA typical |
| **Output Voltage** | 5V TTL (Ouster), 3.3V internal logic |
| **NMEA Baud Rate** | 115200 bps (configurable) |
| **PPS Signal** | 5V TTL, 1Hz, <1μs rise time |
| **Connectors** | Micro-D 15 (input), RJ45 (output) |

### Mechanical

| Parameter | Value |
|-----------|-------|
| **External Dimensions** | 90×60×30mm |
| **Weight** | ~120g (with PCB) |
| **Enclosure Material** | ABS/PETG (3D print) or polycarbonate |
| **Operating Temperature** | -20°C to +70°C |
| **Mounting** | 4× M3 standoffs |

### Key Components

- **U2** - MAX3232CPE: RS232 ↔ TTL transceiver
- **U3** - OKI-78SR-3.3/1.5-W36-C: Buck converter (12V→3.3V)
- **U4** - 74HC125N: Quad 3-state buffer for signal conditioning
- **C1-C5** - 100µF electrolytic capacitors for filtering
- **J1** - DC barrel jack (12V input)
- **J2** - 15-pin Micro-D connector (xNAV650 interface)
- **J4** - RJ45 shielded connector (Ouster interface)

---

## 📦 Bill of Materials (BOM)

Total estimated cost: **$75-160 USD** (prototype quantities)

### Core Components

| Ref | Qty | Part Number | Description | Est. Price |
|-----|-----|-------------|-------------|------------|
| U2 | 1 | MAX3232CPE+ | RS232 Transceiver | $3-5 |
| U3 | 1 | OKI-78SR-3.3/1.5-W36-C | DC-DC Converter | $6-10 |
| U4 | 1 | 74HC125N | Quad Buffer | $0.50-1 |
| J2 | 1 | Micro-D 15-pin Female | xNAV650 Connector | $8-15 |
| J4 | 1 | RJ45 Shielded | Ouster Connector | $2-5 |
| C1-C5 | 5 | 100µF/16V | Electrolytic Caps | $3-5 |
| R1-R2 | 2 | 100Ω | Resistors | $0.50 |

**📄 [Complete BOM with part numbers →](docs/BOM.md)**

### Where to Buy

- **Mouser Electronics** - https://www.mouser.com
- **DigiKey** - https://www.digikey.com
- **Farnell** - https://www.farnell.com
- **LCSC** (for Asia) - https://www.lcsc.com

---

## 🚀 Quick Start Guide

### Prerequisites

Before starting, ensure you have:

- [ ] xNAV650 GPS/INS system with user cable
- [ ] Ouster OS1 LiDAR sensor
- [ ] 12V DC power supply (vehicle or bench supply)
- [ ] Basic soldering equipment
- [ ] Multimeter for testing

### Assembly Overview

1. **Order Components** - Use BOM to order parts from suppliers
2. **PCB Fabrication** - Upload gerbers to PCB manufacturer (JLCPCB, PCBWay, etc.)
3. **Enclosure Preparation** - 3D print or purchase Hammond 1591XXSSBK
4. **PCB Assembly** - Solder all components following assembly guide
5. **Enclosure Integration** - Mount connectors and install PCB
6. **Testing** - Verify voltages and signal integrity
7. **Deployment** - Connect to xNAV650 and Ouster

**📖 [Detailed Assembly Instructions →](docs/assembly-guide.md)**

---

## 🔌 Connection Diagram

```
┌─────────────┐         ┌──────────────┐         ┌─────────────┐
│  xNAV650    │         │   Adapter    │         │  Ouster OS1 │
│  GPS/INS    │─15pin──▶│   PCB        │──RJ45──▶│   LiDAR     │
│             │         │              │         │             │
│ • RS232 TX  │────────▶│ MAX3232      │────────▶│ NMEA (TTL)  │
│ • PPS 3.3V  │────────▶│ 74HC125      │────────▶│ PPS (5V)    │
│ • Ethernet  │────────▶│ Pass-through │────────▶│ Ethernet    │
└─────────────┘         └──────────────┘         └─────────────┘
                              ▲
                              │ 12V DC
                        ┌─────┴─────┐
                        │  Vehicle  │
                        │   Power   │
                        └───────────┘
```

### Pin Mapping

**xNAV650 (J2 - Micro-D 15) → Adapter:**
- Pin 1-2, 14-15: Supply+ / Supply- (12V)
- Pin 3: Serial RX (RS232)
- Pin 4: Serial TX (RS232) → to MAX3232
- Pin 12: PPS (3.3V isolated) → to 74HC125
- Pin 5-8: Ethernet (ERX+/-, ETX+/-) → pass-through

**Adapter → Ouster OS1 (J4 - RJ45):**
- Pins 1-2, 3-6, 7-8: Ethernet (standard T568B)
- Pin 4-5: NMEA_TX (TTL 5V from MAX3232)
- Custom pin: SYNC_PULSE_IN (PPS 5V from 74HC125)

**💡 Tip:** Refer to Ouster OS1 hardware integration guide for exact pinout

---

## ⚙️ Configuration

### xNAV650 Configuration (NAVconfig)

1. **Enable NMEA Output:**
   - Open NAVconfig
   - Navigate to: `Hardware Setup > LiDAR Scanner`
   - Select: Velodyne VLP-16 (or custom)
   - Set NMEA Output: **Serial** or **Ethernet** (choose serial for this adapter)
   - Baud Rate: **115200 bps**

2. **Configure PPS Signal:**
   - Navigate to: `Interfaces > PPS/Triggers`
   - PPS Active Edge: **Falling** (check Ouster requirements)
   - PPS Source: **GNSS Receiver**

3. **Save and Upload:**
   - Save configuration
   - Upload to xNAV650 via ethernet
   - Reboot unit

### Ouster OS1 Configuration

Access Ouster web interface (default: `http://os1-XXXX.local/`):

1. **Set Time Sync Mode:**
   ```bash
   TIME_SYNC_MODE = "PTP" or "NMEA"
   ```
   For this adapter, use: **NMEA + PPS**

2. **Configure NMEA:**
   ```bash
   NMEA_IN_POLARITY = "ACTIVE_HIGH"  # or ACTIVE_LOW, test both
   NMEA_BAUD_RATE = 115200
   ```

3. **Verify Synchronization:**
   - Check web interface: `Status > Time Sync`
   - Should show: "Synchronized" with GPS time

**📚 [Official Ouster Integration Guide](https://www.oxts.com/wp-content/uploads/2025/03/Ouster-Hardware-Integration-Guide_compressed.pdf)**

---

## 🧪 Testing & Validation

### Pre-Deployment Checks

**1. Power Test:**
```
□ Connect 12V power supply
□ Verify LED illuminates (green)
□ Measure 3.3V at U3 output pin
□ Measure 5V at MAX3232 VCC pin
□ Check U3 temperature (<60°C)
```

**2. Signal Integrity Test:**
```
□ Connect oscilloscope to PPS output
□ Verify 1Hz square wave, 5V amplitude
□ Check rise time <1μs
□ Measure NMEA TX voltage: ~5V high, ~0V low
```

**3. Communication Test:**
```
□ Connect xNAV650 and power on
□ Use USB-TTL adapter to monitor NMEA output
□ Should see NMEA sentences at 115200 baud
□ Example: $GPRMC,123519,A,4807.038,N,01131.000,E...
```

**4. Integration Test:**
```
□ Connect complete system (xNAV + Adapter + Ouster)
□ Power on in sequence
□ Check Ouster web interface for sync status
□ Verify point cloud timestamps match GPS time
```

### Troubleshooting

| Issue | Possible Cause | Solution |
|-------|---------------|----------|
| No LED | No 12V power / blown fuse | Check power supply, replace fuse |
| LED on, no NMEA | MAX3232 not configured | Check solder joints, verify xNAV config |
| NMEA works, no PPS | 74HC125 issue | Verify PPS input from xNAV, check buffer |
| Ouster not syncing | Wrong polarity | Try inverting PPS_IN_POLARITY setting |
| Intermittent operation | Loose connections | Re-solder connectors, check crimps |

---

## 📐 Enclosure Options

### Option 1: 3D Printing (Recommended)

**Files:** `enclosure/3d-models/`

**Materials:**
- **PETG** (recommended) - Strong, temperature resistant
- **ABS** - Good for outdoor use
- **Nylon** - Maximum durability

**Print Settings:**
- Layer height: 0.2mm
- Infill: 30-40%
- Supports: Yes (for mounting holes)
- Print time: ~4-6 hours

**📥 [Download STL Files →](enclosure/3d-models/)**

### Option 2: Off-the-Shelf Enclosure

**Recommended:** Hammond 1591XXSSBK
- Dimensions: 85×56×25mm
- Material: ABS, IP54 rated
- Price: $8-12 USD
- Requires drilling holes (template provided)

**📄 [Drilling Template PDF →](enclosure/drilling-template.pdf)**

### Option 3: CNC Machining

For production runs or harsh environments:
- Material: Aluminum 6061-T6
- Anodized finish for corrosion resistance
- Cost: $40-80 per unit (qty 10+)

---

## 🎯 Use Cases

### Mobile Mapping
- Survey vehicles with synchronized LiDAR and GPS
- Accurate georeferencing of point clouds
- Highway infrastructure inspection

### Autonomous Vehicles
- Sensor fusion with precise timing
- SLAM (Simultaneous Localization and Mapping)
- Real-time navigation systems

### Robotics
- Mobile robots requiring GPS/LiDAR integration
- Agricultural automation
- Warehouse and industrial AGVs

### Research & Development
- Academic research platforms
- Algorithm development for autonomous systems
- Multi-sensor calibration studies

---

## 📚 Documentation

- **[Bill of Materials (BOM)](docs/BOM.md)** - Complete component list with part numbers
- **[Assembly Guide](docs/assembly-guide.md)** - Step-by-step construction
- **[User Manual](docs/user-manual.pdf)** - Operation and maintenance
- **[Hardware Schematic](hardware/schematics/XNAVOUSTER.kicad_sch)** - KiCad source
- **[3D Models](enclosure/3d-models/)** - STL and STEP files

### External References

- [xNAV650 Hardware Manual](https://www.datrontechnology.co.uk/wp-content/uploads/2021/03/xNAV650-manual-210311.pdf)
- [Ouster OS1 Documentation](https://ouster.com/downloads)
- [OxTS-Ouster Integration Guide](https://www.oxts.com/wp-content/uploads/2025/03/Ouster-Hardware-Integration-Guide_compressed.pdf)
- [MAX3232 Datasheet (TI)](https://www.ti.com/product/MAX3232)
- [OKI-78SR Datasheet (Murata)](https://www.murata.com/products/productdata/8807031734302/oki-78sr.pdf)

---

## 🤝 Contributing

Contributions are welcome! Here's how you can help:

### Ways to Contribute

- 🐛 **Report bugs** - Open an issue with details
- 💡 **Suggest features** - Share your ideas for improvements
- 📖 **Improve documentation** - Fix typos, add examples
- 🔧 **Hardware improvements** - PCB layout optimizations, component alternatives
- 📦 **Alternative enclosures** - Share your designs
- 🧪 **Testing** - Validate in different environments

### Development Workflow

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-improvement`)
3. Commit your changes (`git commit -am 'Add amazing improvement'`)
4. Push to the branch (`git push origin feature/amazing-improvement`)
5. Open a Pull Request

### Code of Conduct

Be respectful, constructive, and collaborative. This is an open-source hardware project intended to help the community.

---

## 📄 License

This project is licensed under the **MIT License** - see [LICENSE](LICENSE) file for details.

### What this means:
- ✅ Commercial use allowed
- ✅ Modification allowed
- ✅ Distribution allowed
- ✅ Private use allowed
- ⚠️ No warranty provided
- ⚠️ Author not liable

**Attribution appreciated but not required!**

---

## 🙋 Support & Contact

### Getting Help

- **Issues:** Open an issue on GitHub for bugs or questions
- **Discussions:** Use GitHub Discussions for general questions
- **Email:** hirchukv@gmail.com

### Community

- **GitHub:** [@SoloScriptSage](https://github.com/SoloScriptSage)
- **Project Website:** [View interactive demo →](https://soloscriptsage.github.io/xnav-adapter.html)

### Commercial Support

For custom designs, integration services, or bulk orders:
- Contact: hirchukv@gmail.com
- Available for consulting on similar GPS/LiDAR projects

---

## 🏆 Acknowledgments

- **OxTS** - xNAV650 documentation and support
- **Ouster** - LiDAR hardware integration guides
- **Open Source Community** - KiCad, FreeCAD, and related tools
- **Contributors** - Everyone who improves this project

---

## 📊 Project Status

- [x] Initial schematic design
- [x] PCB layout
- [x] BOM compilation
- [x] 3D enclosure design
- [x] Assembly documentation
- [ ] Prototype testing
- [ ] Production manufacturing
- [ ] Field deployment validation
- [ ] Firmware development (future)
- [ ] Web configuration interface (future)

**Current Version:** 1.0 (Beta)  
**Last Updated:** November 2025

---

## 🔮 Future Improvements

### Planned Features

- [ ] **Onboard microcontroller** - ESP32 for configuration via WiFi
- [ ] **OLED display** - Status information and diagnostics
- [ ] **Data logging** - SD card for timestamp verification
- [ ] **Multiple LiDAR support** - Switch between Ouster/Velodyne/Hesai
- [ ] **Galvanic isolation** - Full isolation for harsh environments
- [ ] **Reverse power protection** - TVS diodes and polarity protection
- [ ] **Automotive connectors** - Deutsch or Amphenol for vibration resistance

### Version Roadmap

- **v1.0** - Current release (basic functionality)
- **v1.1** - Improved power filtering, EMI reduction
- **v2.0** - Microcontroller integration, web interface
- **v3.0** - Multi-LiDAR support, advanced diagnostics

---

## 💬 FAQ

**Q: Can I use this with other LiDAR brands?**  
A: Yes, with modifications. Most LiDARs accept similar NMEA+PPS inputs. Check voltage levels and pinouts.

**Q: Does this work with single-antenna xNAV systems?**  
A: Yes, PPS and NMEA work identically on single and dual-antenna configurations.

**Q: What's the expected accuracy of time synchronization?**  
A: PPS provides <1μs timing accuracy. Overall system accuracy depends on xNAV650 GPS lock quality.

**Q: Can I power the Ouster from this adapter?**  
A: No, this only provides signal conversion. Ouster requires separate 12-24V power supply.

**Q: Is PCB assembly service available?**  
A: Not officially, but you can use services like JLCPCB or PCBWay with provided gerbers.

**Q: What about CE/FCC certification?**  
A: This is a development tool. For commercial products, you'll need proper certification.

---

## 📸 Gallery

*Coming soon: Photos of assembled units, field deployments, and point cloud results*

---

**⭐ If this project helps you, please consider starring the repository!**

---

**Made with ⚡ by [Vladyslav Hirchuk](https://github.com/SoloScriptSage)**  
*Open Hardware for the Robotics Community*
