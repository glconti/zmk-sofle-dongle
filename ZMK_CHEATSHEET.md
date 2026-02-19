# ZMK Advanced Features Cheatsheet

> A comprehensive reference for QMK users transitioning to ZMK.

---

## Table of Contents

1. [QMK → ZMK Keycode Reference](#1-qmk--zmk-keycode-reference)
2. [Behaviors (The Core Concept)](#2-behaviors-the-core-concept)
3. [Tap-Dance](#3-tap-dance)
4. [Hold-Tap / Mod-Tap / Layer-Tap](#4-hold-tap--mod-tap--layer-tap)
5. [Sticky Keys (One-Shot)](#5-sticky-keys-one-shot)
6. [Combos](#6-combos)
7. [Macros](#7-macros)
8. [Conditional Layers](#8-conditional-layers)
9. [Caps Word](#9-caps-word)
10. [Key Repeat](#10-key-repeat)
11. [Bluetooth Management](#11-bluetooth-management)
12. [RGB Underglow](#12-rgb-underglow)
13. [Backlight](#13-backlight)
14. [Pointing Devices (Mouse)](#14-pointing-devices-mouse)
15. [Encoders (Sensors)](#15-encoders-sensors)
16. [Power Management & Sleep](#16-power-management--sleep)
17. [Configuration (.conf file)](#17-configuration-conf-file)
18. [Building & Flashing](#18-building--flashing)
19. [Common Gotchas for QMK Users](#19-common-gotchas-for-qmk-users)
20. [Debugging Tips](#20-debugging-tips)

---

## 1. QMK → ZMK Keycode Reference

### Basic Keys

| QMK | ZMK | Description |
|---|---|---|
| `KC_A` ... `KC_Z` | `A` ... `Z` | Letters |
| `KC_1` ... `KC_0` | `N1` ... `N0` | Number row |
| `KC_F1` ... `KC_F12` | `F1` ... `F12` | Function keys |
| `KC_ENT` | `ENTER` or `RET` | Enter |
| `KC_ESC` | `ESC` | Escape |
| `KC_BSPC` | `BSPC` | Backspace |
| `KC_TAB` | `TAB` | Tab |
| `KC_SPC` | `SPACE` | Space |
| `KC_DEL` | `DEL` | Delete |
| `KC_INS` | `INS` | Insert |
| `KC_CAPS` | `CAPS` | Caps Lock |

### Modifiers

| QMK | ZMK | Description |
|---|---|---|
| `KC_LSFT` | `LSHFT` | Left Shift |
| `KC_RSFT` | `RSHFT` | Right Shift |
| `KC_LCTL` | `LCTRL` | Left Control |
| `KC_RCTL` | `RCTRL` | Right Control |
| `KC_LALT` | `LALT` | Left Alt |
| `KC_RALT` | `RALT` | Right Alt |
| `KC_LGUI` | `LGUI` | Left GUI/Win/Cmd |
| `KC_RGUI` | `RGUI` | Right GUI |

### Symbols (WATCH OUT — naming differs!)

| QMK | ZMK | Character |
|---|---|---|
| `KC_MINS` | `MINUS` | `-` |
| `KC_EQL` | `EQUAL` | `=` |
| `KC_LBRC` | `LBKT` | `[` ⚠️ |
| `KC_RBRC` | `RBKT` | `]` ⚠️ |
| `KC_BSLS` | `BSLH` | `\` |
| `KC_SCLN` | `SEMI` | `;` |
| `KC_QUOT` | `SQT` or `APOS` | `'` |
| `KC_GRV` | `GRAVE` | `` ` `` |
| `KC_COMM` | `COMMA` | `,` |
| `KC_DOT` | `DOT` or `PERIOD` | `.` |
| `KC_SLSH` | `FSLH` | `/` |

### Shifted Symbols

| QMK | ZMK | Character |
|---|---|---|
| `KC_TILD` / `S(KC_GRV)` | `TILDE` | `~` |
| `KC_EXLM` | `EXCL` | `!` |
| `KC_AT` | `AT` or `AT_SIGN` | `@` |
| `KC_HASH` | `HASH` | `#` |
| `KC_DLR` | `DLLR` or `DOLLAR` | `$` |
| `KC_PERC` | `PRCNT` or `PERCENT` | `%` |
| `KC_CIRC` | `CARET` | `^` |
| `KC_AMPR` | `AMPS` | `&` |
| `KC_ASTR` | `STAR` or `ASTRK` | `*` |
| `KC_LPRN` | `LPAR` | `(` |
| `KC_RPRN` | `RPAR` | `)` |
| `KC_UNDS` | `UNDER` | `_` |
| `KC_PLUS` | `PLUS` | `+` |
| `KC_LCBR` | `LBRC` | `{` ⚠️ |
| `KC_RCBR` | `RBRC` | `}` ⚠️ |
| `KC_PIPE` | `PIPE` | `\|` |

> ⚠️ **BRACKET NAMING** is the #1 porting gotcha:
> - QMK: `LBRC` = `[`, `LCBR` = `{`
> - ZMK: `LBKT` = `[`, `LBRC` = `{`

### Navigation

| QMK | ZMK |
|---|---|
| `KC_LEFT/DOWN/UP/RGHT` | `LEFT` / `DOWN` / `UP` / `RIGHT` |
| `KC_HOME` / `KC_END` | `HOME` / `END` |
| `KC_PGUP` / `KC_PGDN` | `PG_UP` / `PG_DN` |

### Media / Consumer Keys

| QMK | ZMK | Description |
|---|---|---|
| `KC_MUTE` | `C_MUTE` | Mute |
| `KC_VOLU` / `KC_VOLD` | `C_VOL_UP` / `C_VOL_DN` | Volume |
| `KC_MPLY` | `C_PP` or `C_PLAY_PAUSE` | Play/Pause |
| `KC_MNXT` / `KC_MPRV` | `C_NEXT` / `C_PREV` | Next/Previous track |
| `KC_BRIU` / `KC_BRID` | `C_BRI_UP` / `C_BRI_DN` | Screen brightness |

### Numpad Keys

| QMK | ZMK |
|---|---|
| `KC_P0` ... `KC_P9` | `KP_N0` ... `KP_N9` |
| `KC_PDOT` | `KP_DOT` |
| `KC_PENT` | `KP_ENTER` |
| `KC_PPLS` | `KP_PLUS` |
| `KC_PMNS` | `KP_MINUS` |
| `KC_PAST` | `KP_MULTIPLY` |
| `KC_PSLS` | `KP_DIVIDE` |
| `KC_NUM` | `KP_NUM` |

### Modifier Combinations

| QMK | ZMK | Example |
|---|---|---|
| `LCTL(kc)` | `LC(kc)` | `&kp LC(Z)` = Ctrl+Z |
| `LSFT(kc)` | `LS(kc)` | `&kp LS(A)` = Shift+A |
| `LALT(kc)` | `LA(kc)` | `&kp LA(F4)` = Alt+F4 |
| `LGUI(kc)` | `LG(kc)` | `&kp LG(L)` = Win+L |
| `RCTL(kc)` | `RC(kc)` | Right Ctrl + key |
| `C_S_T(kc)` | `LC(LS(kc))` | Ctrl+Shift+key |
| `MEH(kc)` | `LC(LS(LA(kc)))` | Ctrl+Shift+Alt+key |
| `HYPR(kc)` | `LC(LS(LA(LG(kc))))` | Ctrl+Shift+Alt+GUI+key |

---

## 2. Behaviors (The Core Concept)

In QMK, everything is a keycode. In ZMK, everything is a **behavior** — a reusable action that can be bound to a key position.

| Behavior | Syntax | QMK Equivalent |
|---|---|---|
| Key Press | `&kp KEYCODE` | `KC_*` |
| Momentary Layer | `&mo LAYER` | `MO(layer)` |
| Toggle Layer | `&tog LAYER` | `TG(layer)` |
| To Layer | `&to LAYER` | `TO(layer)` |
| Layer-Tap | `&lt LAYER KEYCODE` | `LT(layer, kc)` |
| Mod-Tap | `&mt MOD KEYCODE` | `MT(mod, kc)` |
| Sticky Key | `&sk KEYCODE` | `OSM(mod)` |
| Sticky Layer | `&sl LAYER` | `OSL(layer)` |
| None | `&none` | `XXXXXXX` |
| Transparent | `&trans` | `_______` |
| Bootloader | `&bootloader` | `QK_BOOT` |
| Reset | `&sys_reset` | `QK_RBT` |
| Soft Off | `&soft_off` | (no QMK equivalent) |

---

## 3. Tap-Dance

Tap once for one action, tap multiple times for different actions.

```dts
behaviors {
    td0: tap_dance_0 {
        compatible = "zmk,behavior-tap-dance";
        #binding-cells = <0>;
        tapping-term-ms = <200>;    // Window for next tap (like TAPPING_TERM)
        bindings = <&kp ESC>,       // 1 tap  = ESC
                   <&kp GRAVE>,     // 2 taps = `
                   <&kp TILDE>;     // 3 taps = ~ (optional, can chain)
    };
};
```

Use in keymap: `&td0`

**QMK equivalent:**
```c
[TD_ESC_GRV] = ACTION_TAP_DANCE_DOUBLE(KC_ESC, KC_GRV)
```

---

## 4. Hold-Tap / Mod-Tap / Layer-Tap

### Built-in Layer-Tap (`&lt`)

Hold for layer, tap for keycode:

```dts
&lt 1 SPACE    // Hold = activate layer 1, Tap = Space
```

QMK: `LT(1, KC_SPC)`

### Built-in Mod-Tap (`&mt`)

Hold for modifier, tap for keycode:

```dts
&mt LSHFT A    // Hold = Left Shift, Tap = A
```

QMK: `MT(MOD_LSFT, KC_A)` or `LSFT_T(KC_A)`

### Custom Hold-Tap (Advanced)

For fine-tuning the hold/tap behavior (flavor, timing, etc.):

```dts
behaviors {
    hm: homerow_mods {
        compatible = "zmk,behavior-hold-tap";
        #binding-cells = <2>;
        tapping-term-ms = <200>;      // Time threshold for hold vs tap
        quick-tap-ms = <150>;         // Re-tap window (prevents hold on fast typing)
        flavor = "tap-preferred";     // See flavors below
        bindings = <&kp>, <&kp>;      // Hold behavior, Tap behavior
    };
};

// Usage: &hm LSHFT A (hold=Shift, tap=A)
```

### Hold-Tap Flavors

| Flavor | Behavior |
|---|---|
| `hold-preferred` | Defaults to hold. Most like QMK default. |
| `balanced` | Decides based on whether another key is pressed AND released. Good for home row mods. |
| `tap-preferred` | Defaults to tap. Best for fast typists. |
| `tap-unless-interrupted` | Tap unless another key is pressed during the hold. |

---

## 5. Sticky Keys (One-Shot)

Press and release — the modifier/layer stays active for the NEXT keypress only.

```dts
&sk LSHFT      // One-shot Shift (QMK: OSM(MOD_LSFT))
&sl 1          // One-shot Layer 1 (QMK: OSL(1))
```

Configuration:

```dts
&sk {
    release-after-ms = <2000>;   // Auto-release after 2 seconds
    quick-release;                // Release sticky on next key press (not release)
};
```

---

## 6. Combos

Press multiple keys simultaneously to trigger an action. **ZMK native feature** — QMK also has combos but the syntax is completely different.

```dts
/ {
    combos {
        compatible = "zmk,combos";

        /* Press J + K simultaneously = ESC */
        combo_esc {
            timeout-ms = <50>;       // Max time between key presses
            key-positions = <31 32>; // Physical key position indices
            bindings = <&kp ESC>;
            layers = <0>;            // Only active on layer 0 (optional)
        };

        /* Press Q + W = Tab */
        combo_tab {
            timeout-ms = <50>;
            key-positions = <1 2>;
            bindings = <&kp TAB>;
        };
    };
};
```

> **How to find key positions:** Count through your layout's matrix transform, starting at 0, left-to-right, top-to-bottom.

---

## 7. Macros

### Simple Macro (type a string)

```dts
macros {
    email_macro: email_macro {
        compatible = "zmk,behavior-macro";
        #binding-cells = <0>;
        bindings = <&kp M &kp E &kp AT &kp E &kp X &kp DOT &kp C &kp O &kp M>;
        // Types: me@ex.com
    };
};
```

### Macro with Modifiers (hold then release)

```dts
macros {
    ctrl_alt_del: ctrl_alt_del {
        compatible = "zmk,behavior-macro";
        #binding-cells = <0>;
        bindings =
            <&macro_press &kp LCTRL &kp LALT>,
            <&macro_tap &kp DEL>,
            <&macro_release &kp LCTRL &kp LALT>;
    };
};
```

### Macro with Timing

```dts
macros {
    slow_macro: slow_macro {
        compatible = "zmk,behavior-macro";
        #binding-cells = <0>;
        wait-ms = <30>;     // Wait between each action
        tap-ms = <30>;      // How long each tap is held
        bindings = <&kp H &kp E &kp L &kp L &kp O>;
    };
};
```

### Macro as Hold Key (pause for release)

```dts
macros {
    shift_click: shift_click {
        compatible = "zmk,behavior-macro";
        #binding-cells = <0>;
        bindings =
            <&macro_press &kp LSHFT>,
            <&macro_press &mkp LCLK>,
            <&macro_pause_for_release>,      // Key stays held until you release
            <&macro_release &mkp LCLK &kp LSHFT>;
    };
};
```

---

## 8. Conditional Layers

Activate a layer automatically when two other layers are active simultaneously. Great for "tri-layer" setups.

```dts
/ {
    conditional_layers {
        compatible = "zmk,conditional-layers";

        /* When Layer 1 AND Layer 2 are both active → activate Layer 3 */
        tri_layer {
            if-layers = <1 2>;
            then-layer = <3>;
        };
    };
};
```

**Use case:** Hold SYMBOL (layer 1) + MOVE (layer 2) simultaneously → NUMPAD (layer 3) activates. No need for a separate key!

QMK equivalent: `update_tri_layer()` in `process_record_user()`.

---

## 9. Caps Word

A smarter Caps Lock — automatically types in CAPS until you press a non-letter key (space, enter, etc.). Numbers and underscore keep it active.

```dts
&caps_word    // Use in keymap directly (built-in behavior)
```

Configuration:

```dts
&caps_word {
    continue-list = <UNDERSCORE MINUS BSPC>;  // Keys that don't deactivate Caps Word
};
```

QMK equivalent: `CAPS_WORD` (QMK also has this since 2022).

---

## 10. Key Repeat

Repeats the last pressed key. Useful with combos.

```dts
&key_repeat    // Built-in behavior, use directly in keymap
```

---

## 11. Bluetooth Management

ZMK supports up to 5 Bluetooth profiles (devices you can switch between).

| Binding | Action |
|---|---|
| `&bt BT_SEL 0` | Select BT profile 0 (0-4) |
| `&bt BT_NXT` | Next BT profile |
| `&bt BT_PRV` | Previous BT profile |
| `&bt BT_CLR` | Clear current profile's pairing |
| `&bt BT_CLR_ALL` | Clear ALL pairings |
| `&bt BT_DISC 0` | Disconnect profile 0 (keep pairing) |
| `&out OUT_USB` | Force USB output |
| `&out OUT_BLE` | Force Bluetooth output |
| `&out OUT_TOG` | Toggle USB/BLE |

**Example layer:**

```dts
layer_bt {
    bindings = <
        &bt BT_SEL 0  &bt BT_SEL 1  &bt BT_SEL 2  &bt BT_SEL 3  &bt BT_SEL 4
        &bt BT_CLR    &bt BT_CLR_ALL &out OUT_USB   &out OUT_BLE   &none
    >;
};
```

> **Tip:** Put BT_CLR on an awkward combo or layer to avoid accidentally unpairing.

---

## 12. RGB Underglow

Requires `CONFIG_ZMK_RGB_UNDERGLOW=y` in `.conf`.

| Binding | Action |
|---|---|
| `&rgb_ug RGB_TOG` | Toggle RGB on/off |
| `&rgb_ug RGB_EFF` | Next effect |
| `&rgb_ug RGB_EFR` | Previous effect |
| `&rgb_ug RGB_BRI` | Increase brightness |
| `&rgb_ug RGB_BRD` | Decrease brightness |
| `&rgb_ug RGB_SPI` | Speed up animation |
| `&rgb_ug RGB_SPD` | Slow down animation |
| `&rgb_ug RGB_HUI` | Increase hue |
| `&rgb_ug RGB_HUD` | Decrease hue |
| `&rgb_ug RGB_SAI` | Increase saturation |
| `&rgb_ug RGB_SAD` | Decrease saturation |
| `&rgb_ug RGB_ON` | Force RGB on |
| `&rgb_ug RGB_OFF` | Force RGB off |
| `&rgb_ug RGB_COLOR_HSB(h,s,b)` | Set specific color (HSB values 0-360, 0-100, 0-100) |

---

## 13. Backlight

Per-key LEDs (if hardware supports it). Requires `CONFIG_ZMK_BACKLIGHT=y`.

| Binding | Action |
|---|---|
| `&bl BL_TOG` | Toggle backlight |
| `&bl BL_INC` | Increase brightness |
| `&bl BL_DEC` | Decrease brightness |
| `&bl BL_ON` | Backlight on |
| `&bl BL_OFF` | Backlight off |
| `&bl BL_SET 50` | Set to 50% brightness |

---

## 14. Pointing Devices (Mouse)

Requires `CONFIG_ZMK_MOUSE=y` in `.conf`.

### Mouse Movement

```dts
&mmv MOVE_UP       // Move cursor up
&mmv MOVE_DOWN     // Move cursor down
&mmv MOVE_LEFT     // Move cursor left
&mmv MOVE_RIGHT    // Move cursor right
```

### Mouse Buttons

```dts
&mkp LCLK    // Left click   (MB1)
&mkp RCLK    // Right click  (MB2)
&mkp MCLK    // Middle click (MB3)
&mkp MB4     // Mouse button 4 (back)
&mkp MB5     // Mouse button 5 (forward)
```

### Scroll

```dts
&msc SCRL_UP       // Scroll up
&msc SCRL_DOWN     // Scroll down
&msc SCRL_LEFT     // Scroll left
&msc SCRL_RIGHT    // Scroll right
```

### Tuning (in your keymap file)

```dts
#define ZMK_POINTING_DEFAULT_MOVE_VAL 1200   // Mouse cursor speed (default 600)
#define ZMK_POINTING_DEFAULT_SCRL_VAL 35     // Scroll speed (default 10)

&mmv {
    time-to-max-speed-ms = <400>;   // Ramp-up time
    acceleration-exponent = <1>;     // 0=linear, 1=accelerated
};
```

---

## 15. Encoders (Sensors)

### Basic Encoder Config

Encoders are called "sensors" in ZMK. Each layer can have its own binding.

```dts
/* In each layer: */
sensor-bindings = <&inc_dec_kp C_VOL_UP C_VOL_DN>;
//                  Clockwise    Counter-clockwise
```

### Common Encoder Bindings

```dts
// Volume control
sensor-bindings = <&inc_dec_kp C_VOL_UP C_VOL_DN>;

// Page Up / Page Down
sensor-bindings = <&inc_dec_kp PG_UP PG_DN>;

// Scroll (using custom behavior)
scroll_encoder: scroll_encoder {
    compatible = "zmk,behavior-sensor-rotate";
    #sensor-binding-cells = <0>;
    bindings = <&msc SCRL_DOWN>, <&msc SCRL_UP>;
    tap-ms = <30>;
};
// Then: sensor-bindings = <&scroll_encoder>;

// Arrow keys (horizontal scroll through tabs, etc.)
sensor-bindings = <&inc_dec_kp RIGHT LEFT>;

// Ctrl+Z / Ctrl+Y (Undo/Redo)
sensor-bindings = <&inc_dec_kp LC(Y) LC(Z)>;

// Brightness
sensor-bindings = <&inc_dec_kp C_BRI_UP C_BRI_DN>;
```

### Encoder Push Button

The encoder click is a regular key position in the matrix. Bind it like any other key:

```dts
&kp C_MUTE    // Mute on encoder click
&td_mute_play // Tap-dance: tap=mute, double=play
```

---

## 16. Power Management & Sleep

### .conf Settings

```ini
# Enable deep sleep
CONFIG_ZMK_SLEEP=y

# Time before deep sleep (in ms) — 2 hours = 7200000
CONFIG_ZMK_IDLE_SLEEP_TIMEOUT=7200000

# Time before idle (screen off, etc.) — default 30000 (30s)
CONFIG_ZMK_IDLE_TIMEOUT=30000
```

### Soft Off (in keymap)

```dts
&soft_off    // Puts the keyboard into ultra-low-power mode
             // Requires physical button press to wake up
```

### System Reset / Bootloader

```dts
&sys_reset    // Resets the MCU (QMK: QK_RBT)
&bootloader   // Enters bootloader mode for flashing (QMK: QK_BOOT)
```

> **Tip:** Put `&bootloader` and `&sys_reset` on both halves of a split keyboard, on a hard-to-reach layer to avoid accidents.

---

## 17. Configuration (.conf file)

The `.conf` file (`config/eyelash_sofle.conf`) is like QMK's `config.h` + `rules.mk` combined.

### Essential Settings

```ini
# ── Bluetooth ──
CONFIG_BT_CTLR_TX_PWR_PLUS_8=y       # Max Bluetooth power (better range)
CONFIG_ZMK_BLE_EXPERIMENTAL_CONN=y    # Improved BLE connection (experimental)

# ── Display ──
CONFIG_ZMK_DISPLAY=y                  # Enable OLED/display

# ── Mouse/Pointing ──
CONFIG_ZMK_MOUSE=y                    # Enable mouse keys/pointing

# ── RGB ──
CONFIG_ZMK_RGB_UNDERGLOW=y            # Enable RGB underglow
CONFIG_ZMK_BACKLIGHT=y                # Enable per-key backlight

# ── Encoders ──
CONFIG_EC11=y                         # Enable EC11 rotary encoder driver
CONFIG_EC11_TRIGGER_GLOBAL_THREAD=y   # Encoder interrupt handling

# ── Power ──
CONFIG_ZMK_SLEEP=y                    # Enable deep sleep
CONFIG_ZMK_IDLE_SLEEP_TIMEOUT=3600000 # Sleep after 1 hour

# ── Debounce ──
CONFIG_ZMK_KSCAN_DEBOUNCE_PRESS_MS=8     # Press debounce (default 5)
CONFIG_ZMK_KSCAN_DEBOUNCE_RELEASE_MS=8   # Release debounce (default 5)

# ── HID ──
CONFIG_ZMK_HID_REPORT_TYPE_NKRO=y    # N-Key Rollover (like QMK's NKRO)
# CONFIG_ZMK_HID_CONSUMER_REPORT_USAGES_BASIC=y  # Compatibility mode for some OSes

# ── Dongle Display ──
CONFIG_ZMK_DONGLE_DISPLAY_DONGLE_BATTERY=y   # Show dongle battery on display
# CONFIG_ZMK_DONGLE_DISPLAY_MAC_MODIFIERS=y   # macOS-style modifier icons
```

---

## 18. Building & Flashing

### GitHub Actions (Recommended)

1. Push your changes to GitHub
2. GitHub Actions automatically builds firmware
3. Download the `.uf2` files from the Actions artifacts
4. Put the board in bootloader mode (double-press reset or `&bootloader` key)
5. Drag `.uf2` onto the USB drive that appears

### Local Build (Advanced)

```bash
# Install west (Zephyr's build tool)
pip install west

# Initialize workspace
west init -l config/
west update

# Build for dongle (central)
west build -s zmk/app -b seeeduino_xiao_ble -- \
    -DSHIELD=eyelash_sofle_central_dongle \
    -DZMK_CONFIG="$(pwd)/config"

# Build for left half
west build -s zmk/app -b seeeduino_xiao_ble -- \
    -DSHIELD=eyelash_sofle_peripheral_left \
    -DZMK_CONFIG="$(pwd)/config"

# Build for right half
west build -s zmk/app -b seeeduino_xiao_ble -- \
    -DSHIELD=eyelash_sofle_peripheral_right \
    -DZMK_CONFIG="$(pwd)/config"
```

### When to Flash What

| Changed | Flash |
|---|---|
| Keymap only | Dongle only (central) |
| `.conf` settings | ALL three (dongle + left + right) |
| Bluetooth issues | ALL three (clear profiles too) |

---

## 19. Common Gotchas for QMK Users

### 1. **Bracket naming is swapped**
```
QMK: KC_LBRC = [    KC_LCBR = {
ZMK:    LBKT = [       LBRC = {
```

### 2. **No `process_record_user()` function**
ZMK doesn't have a C callback for key events. Everything is declared in the keymap/devicetree. Use macros, behaviors, and combos to achieve the same results.

### 3. **No VIAL/VIA support**
ZMK doesn't support runtime keymap editing via VIA/VIAL. You must edit the keymap file and reflash. However, ZMK Studio (in development) aims to fill this gap.

### 4. **Layer numbers matter**
Layers are numbered by their order in the keymap (0, 1, 2, ...). Unlike QMK, you can't use `enum` names. Reference layers by number.

### 5. **Tap-dance behaviors have no index**
QMK: `TD(TD_ESC_GRV)` references by enum index.
ZMK: `&td_esc_grv` references by node name.

### 6. **Split keyboards flash differently**
- QMK: Flash both halves with the same firmware
- ZMK: Each half gets its OWN firmware (peripheral_left, peripheral_right, central/dongle)

### 7. **No `#define` for layer names**
ZMK uses raw numbers. If you want readability, add `#define` at the top:
```c
#define QWERTY 0
#define SYMBOL 1
#define MOVE   2
#define NUMPAD 3
```
Then use `&mo SYMBOL` instead of `&mo 1`.

### 8. **`&trans` vs `&none`**
- `&trans` = transparent, falls through to the layer below (QMK `_______`)
- `&none` = explicitly does nothing, blocks fall-through (QMK `XXXXXXX`)

### 9. **Consumer keycodes need `C_` prefix**
Media keys in ZMK use the `C_` prefix: `C_MUTE`, `C_VOL_UP`, `C_PP`, `C_NEXT`, etc.

### 10. **RGB commands use `&rgb_ug` prefix**
Not just `RGB_TOG` — you need `&rgb_ug RGB_TOG`.

---

## 20. Debugging Tips

### Check Build Logs
If the build fails on GitHub Actions, check the workflow logs. Common errors:
- **Missing semicolon** in devicetree
- **Wrong number of bindings** (must match the matrix layout exactly)
- **Unknown keycode** (check spelling, ZMK names differ from QMK)

### Bluetooth Pairing Issues
1. Clear pairing on the keyboard: `&bt BT_CLR`
2. Remove the device from your OS Bluetooth settings
3. Re-pair

### Key Not Working
- Check if you have `&none` instead of `&trans` on a higher layer
- Verify the key count in each layer matches the matrix (this board = 64 keys)
- Check your `.conf` for missing feature flags

### Useful Resources
- **ZMK Docs:** https://zmk.dev/docs
- **ZMK Key Codes:** https://zmk.dev/docs/keymaps/list-of-keycodes
- **ZMK Behaviors:** https://zmk.dev/docs/keymaps/behaviors/key-press
- **Keymap Editor (GUI):** https://nickcoutsos.github.io/keymap-editor/

---

## Quick Template: Adding a New Behavior

```dts
/ {
    behaviors {
        my_behavior: my_behavior {
            compatible = "zmk,behavior-<TYPE>";
            #binding-cells = <N>;     // 0 for tap-dance/macro, 2 for hold-tap
            // ... config properties ...
            bindings = <&kp A>, <&kp B>;
        };
    };

    combos {
        compatible = "zmk,combos";
        my_combo {
            timeout-ms = <50>;
            key-positions = <POS1 POS2>;
            bindings = <&my_behavior>;
        };
    };

    macros {
        my_macro: my_macro {
            compatible = "zmk,behavior-macro";
            #binding-cells = <0>;
            bindings = <&kp H &kp I>;
        };
    };

    conditional_layers {
        compatible = "zmk,conditional-layers";
        tri_layer {
            if-layers = <1 2>;
            then-layer = <3>;
        };
    };

    keymap {
        compatible = "zmk,keymap";
        layer_0 { bindings = <...>; };
    };
};
```
