 ET44/ET45 LCR Meter Tier Unlock Tool

Software-only unlock tool for the **East Tester / Hangzhou Zhongchuang
ET4401 / ET4402 / ET4410 / ET4501 / ET4502 / ET4510** LCR meter series.

The entire ET44/ET45 series shares identical hardware — the differences
between models are software-only, encoded in three small fields in flash.
This tool writes those fields through the firmware's own service protocol
on the meter's RS232 port. **Three serial commands convert an ET4401 into
a fully-functional ET4510**, with continuous-frequency mode accessed via
the CAL key.

- ✅ No soldering
- ✅ No SWD or JTAG
- ✅ No firmware patching
- ✅ No chip erase
- ✅ Fully reversible at any time
- ✅ Cannot brick the device (firmware enforces value ranges)

## Download

See the [Releases](../../releases) page for the prebuilt Windows EXE.

For Linux/Mac users, run `tier_unlock.py` directly with Python 3 and
`pyserial` installed:

```bash
pip install pyserial
python tier_unlock.py
```

## Quick usage

1. Connect a USB-to-RS232 cable between your PC and the meter's RS232 port
2. Power on the meter, wait for the main measurement screen
3. Run the tool — it auto-detects port and baud rate
4. Click "Read current config", then "Save backup to file"
5. Pick a configuration from the dropdown, click "Apply"
6. Power-cycle the meter

## Tested on

Firmware version **V6.00.2611.089**. Other firmware versions may behave
differently.

## How it works

See [`et44_unlock_notes.md`](et44_unlock_notes.md) for full technical
documentation: hardware details, flash layout, complete service protocol
specification, command reference, and reverse engineering notes from
Ghidra analysis.

## Capability tier values

| `0x50` value | Capability |
|---|---|
| `0x00` | ET4401 — 10 kHz / 10 fixed pts |
| `0x01` | ET4402 — 20 kHz / 12 fixed pts |
| `0x02` | ET4410 — 100 kHz / 16 fixed pts |
| `0x03` | ET4501 — 10 kHz, continuous via CAL |
| `0x04` | ET4502 — 20 kHz, continuous via CAL |
| `0x05` | ET4510 — 100 kHz, continuous via CAL |

## Calibration caveat

Factory calibration only exists at the original tier's frequencies. At
unlocked frequencies, expect some accuracy degradation versus the
higher tier's published spec. Always perform user open/short cal at
your working frequencies, and verify with known-value reference parts
(1% film capacitors, NPO ceramics, precision resistors) before
trusting absolute measurements.

## Disclaimer

Use at your own risk. Voids warranty. Restore to factory before any
vendor service. Not affiliated with Hangzhou Zhongchuang Electronics,
East Tester, Mustool, Victor, or any distributor.
