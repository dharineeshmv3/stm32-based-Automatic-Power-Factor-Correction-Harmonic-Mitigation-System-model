# Dual-Stage Grid Power Quality System — final version

| File | What it is |
|---|---|
| `main.c` | STM32F401RE firmware (CMSIS only): APFC capacitor bank + Active Harmonic Filter (TB6612FNG) |
| `dashboard.py` | Real-time PC dashboard: shared V/I waveforms, *Power Factor Correction* and *Harmonic Mitigation* tabs |
| `requirements.txt` | Python libraries for the dashboard and how to install them |
| `CAPACITOR_RELAY_GUIDELINES.txt` | **Read before using the capacitor bank**: switching rules and safety |

## Run the dashboard

```
python -m pip install -r requirements.txt
python dashboard.py --port COM6
```

`python dashboard.py --demo` runs it without the board.

## Capacitor bank safety

* Fit a **bleeder resistor across every capacitor**: 2.5 µF → 820 kΩ, 10 µF → 220 kΩ, 20 µF → 100 kΩ (1 W, ≥ 400 V rated). Without it the capacitor stays charged for minutes and the relay closes onto up to 650 V, which welds its contacts.
* Prefer **zero-cross SSRs** for switching capacitors; mechanical relay modules (10 A resistive rating) are not rated for capacitor inrush.
* Use AC film capacitors (motor-run / PFC type) rated **≥ 400 VAC**, never electrolytics.
