# SoundIQ 🎧

An unofficial Flutter app for controlling **Soundpeats Air 4 Pro** earbuds — without the official app.

Built by reverse engineering the Bluetooth HCI protocol using `btsnoop_hci.log` analysis.

---

## Features

- 🔊 **ANC Control** — Normal / ANC / Transparency mode
- 🔋 **Battery Level** — Left & Right earbud separately
- 🎮 **Game Mode** — Low latency toggle
- 👆 **Touch Controls** — Enable / Disable
- 👂 **In-ear Detection** — Auto pause toggle
- 🖐️ **Gesture Control** — Customize all 8 gestures (single/double/triple tap, long press)
- 🎵 **Equalizer** — 15 presets + 5-band custom EQ
- 🔓 **Extended EQ** — ±24dB range for rooted devices

---

## Protocol

Communicates via **Bluetooth Classic SPP (Serial Port Profile)**.

All commands are in the format:
```
FF 04 00 [TYPE] 00 0A 03 [KEY] [VALUE]
```

| Feature | Key | Values |
|---------|-----|--------|
| ANC Mode | `0x11` | `0x00`=Normal, `0x01`=ANC, `0x02`=Transparency |
| Game Mode | `0x0F` | `0x00`=Off, `0x01`=On |
| Touch Lock | `0x13` | `0x00`=Off, `0x01`=On |
| In-ear Detection | `0x0D` | `0x00`=Off, `0x01`=On |
| Gesture | `0xAB` | `[slot, action]` |

### Gesture Slots
| Slot | Value |
|------|-------|
| Left Single Tap | `0x01` |
| Right Single Tap | `0x02` |
| Left Double Tap | `0x03` |
| Right Double Tap | `0x04` |
| Left Triple Tap | `0x05` |
| Right Triple Tap | `0x06` |
| Left Long Press | `0x09` |
| Right Long Press | `0x0A` |

### Gesture Actions
| Action | Value |
|--------|-------|
| Undefined | `0x00` |
| Volume Up | `0x01` |
| Volume Down | `0x02` |
| Play/Pause | `0x03` |
| Game Mode | `0x04` |
| Previous Track | `0x05` |
| Next Track | `0x06` |
| Noise Cancelling | `0x07` |
| Voice Assistant | `0x08` |

---

## Setup

```bash
git clone https://github.com/yourusername/soundiq
cd soundiq
flutter pub get
flutter run
```

### Requirements
- Flutter 3.x+
- Android 5.0+ (API 21+)
- Soundpeats Air 4 Pro paired via Bluetooth settings

### Known Issue
`flutter_bluetooth_serial` package needs a manual fix:

In `~/.pub-cache/hosted/pub.dev/flutter_bluetooth_serial-0.4.0/android/build.gradle` add:
```groovy
android {
    namespace "io.github.edufolly.flutterbluetoothserial"
    compileSdkVersion 34
    // ...
    buildToolsVersion '34.0.0'
}
```

---

## Dependencies

- `flutter_bluetooth_serial` — Bluetooth SPP connection
- `permission_handler` — Bluetooth permissions

---

## Disclaimer

This is an **unofficial** app, not affiliated with Soundpeats. Use at your own risk.
Protocol was reverse engineered from Bluetooth HCI logs for personal use.
