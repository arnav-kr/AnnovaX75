# Annova X75 RMK Firmware (Vial Enabled)

Firmware for the **Annova X75** mechanical keyboard built with [RMK](https://rmk.rs) (Rust Keyboard Firmware) and [Vial](https://get.vial.today) support.

## Hardware Specifications

- **MCU**: Raspberry Pi RP2040
- **Matrix**: 6 rows × 15 columns (COL2ROW)
  - Rows: `GP17`, `GP18`, `GP19`, `GP20`, `GP21`, `GP22` (`PIN_17` to `PIN_22`)
  - Columns: `GP0`, `GP1`, `GP15`, `GP14`, `GP13`, `GP12`, `GP11`, `GP10`, `GP9`, `GP8`, `GP7`, `GP6`, `GP5`, `GP4`, `GP3`
- **Rotary Encoder (EC11)**:
  - Pin A: `GP2` (`PIN_2`)
  - Pin B: `GP16` (`PIN_16`)
  - Push Button: Matrix `(0, 14)` (Row 0, Col 14)
  - Internal Pull-up: Enabled
  - Default Action: CCW = Volume Down, CW = Volume Up, Press = Mute
- **Bootloader / Bootmagic**:
  - Hold `Escape` (`(0, 0)`) during plug-in to enter RP2040 BOOTSEL mode.
  - Or press the physical RESET button on the back of the PCB.

## Vial Support

- Real-time on-the-fly keymap and rotary encoder remapping via the [Vial Web App](https://vial.rocks) or Vial desktop application.
- `vial.json` is embedded directly into the firmware binary (`build.rs`). No sideloading required.
- **Layers**: 4 layers enabled with persistent flash storage.
- **Unlock Combination**: Press `Escape` + `F1` (`(0, 0)` and `(0, 1)`) simultaneously to unlock secure features in Vial (matrix tester, etc.).

## Building the Firmware

Ensure you have Rust and the `thumbv6m-none-eabi` target installed:

```bash
rustup target add thumbv6m-none-eabi
```

### Build Release Binary

```bash
cargo build --release
```

### Generate `.uf2` file

Using `elf2uf2-rs`:

```bash
cargo install elf2uf2-rs
elf2uf2-rs target/thumbv6m-none-eabi/release/AnnovaX75 AnnovaX75.uf2
```

## Flashing the Keyboard

### Method 1: One-step USB Flash & Autoboot (Recommended)
`runner = "elf2uf2-rs -d"` is enabled by default in `.cargo/config.toml`.
1. Put the keyboard in BOOTSEL mode (hold `Escape` while plugging in, or press the button on the back of the PCB).
2. Run:
   ```bash
   cargo run --release
   ```
   `elf2uf2-rs` will detect the mounted Pico disk, flash the firmware, and **autoboot** the keyboard immediately.

### Method 2: Manual Drag and Drop
1. Build the `.uf2` file:
   ```bash
   cargo build --release
   elf2uf2-rs target/thumbv6m-none-eabi/release/AnnovaX75 AnnovaX75.uf2
   ```
2. Hold down `Escape` while plugging in the keyboard.
3. Drag and drop `AnnovaX75.uf2` onto the mounted `RPI-RP2` drive. The board will autoboot.

### Method 3: Debug Probe (probe-rs)
If using a Picoprobe or J-Link:

```bash
cargo run --release
```