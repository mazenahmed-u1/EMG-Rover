# EMG-Rover

**EMG-Controlled Differential Drive Robot** — An end-to-end biomedical signal processing and embedded actuation system bridging **Digital Signal Processing (DSP)**, **Industrial Electronics**, and **Electrical Machines**.

---

## Repository Structure

```text
EMG-Rover/
├── README.md                            # Project overview, architecture, team, and setup guide
├── .gitignore                           # Ignored temporary, cache, and build artifacts
├── docs/
│   ├── spec-v5.1.md                     # Locked system architecture specification
│   ├── bom.md                           # Final Bill of Materials (AD620, LM3403, AMS1117, etc.)
│   └── safety.md                        # Biomedical & electrical safety rules (battery-only, no HDMI)
├── hardware/
│   ├── afe/
│   │   ├── sim/
│   │   │   └── emg_rover_afe.pdsprj     # Proteus Analog Front-End simulation file
│   │   ├── screenshots/                 # Oscilloscope & probe verification captures
│   │   └── test-log.md                  # Expected vs. measured values (Simulation & Breadboard)
│   ├── chassis/                         # Differential drive schematics & motor load measurements
│   └── lab-demos/                       # Off-car bench demos (555 PWM, SCR, Linear PSU, Transformer)
├── firmware/
│   ├── uno_daq/
│   │   └── uno_daq.ino                  # ATmega328P Timer1 @ 2kHz ISR + 8-byte binary protocol
│   └── nano_car/
│       └── nano_car.ino                 # HC-05 Bluetooth, Watchdog, and 3V motor PWM control
├── software/
│   ├── emg_rover/                       # Core from-scratch Python DSP & control package
│   │   ├── __init__.py
│   │   ├── filters.py                   # IIR DC blocker, 50Hz notch, IIR/FIR bandpass filters
│   │   ├── envelope.py                  # Full-wave rectifier & 15Hz fast envelope extractor
│   │   ├── fsm.py                       # Calibrated temporal gesture FSM (Hold vs. Double-Tap)
│   │   └── serial_parser.py             # Threaded binary frame parser (Seq_ID & XOR checksum)
│   ├── scripts/
│   │   ├── record_csv.py                # Raw sEMG data logger to CSV
│   │   ├── live_plot.py                 # Real-time PyQtGraph waveform & FFT visualizer
│   │   └── calibrate.py                 # Per-session rest/contraction threshold calibration
│   ├── tests/                           # Unit tests validating custom filters against SciPy
│   └── requirements.txt                 # Python dependencies (numpy, scipy, pyserial, pyqtgraph)
├── matlab/                              # Offline filter design (zplane/freqz), RMSE check & Simulink
├── data/
│   ├── raw/                             # Recorded sEMG CSV datasets (e.g., subject_01.csv)
│   └── README.md                        # CSV schema and recording protocol
└── results/                             # Auto-generated plots and confusion matrices (gitignored)
