# Hardware Build Guide

## Wiring Diagram

```
  ┌─────────────────────────────────────────────────────────┐
  │                    RASPBERRY PI 5                       │
  │                                                         │
  │   CSI-0 ◄── 15-pin FPC ── OV5640 module               │
  │              (camera_num=0)    + Blue filter glued/     │
  │                                  mounted on lens        │
  │                                                         │
  │   CSI-1 ◄── 15-pin FPC ── OV5640 module               │
  │              (camera_num=1)    + Green filter           │
  │                                                         │
  │   USB-A port 1 ◄── USB-C cable ──┐                    │
  │   USB-A port 2 ◄── USB-C cable ──┼──┐                 │
  └───────────────────────────────────┼──┼─────────────────┘
                                      │  │
              ┌───────────────────────┘  │
              │                          │
   ┌──────────▼───────────────┐  ┌──────▼────────────────┐
   │   ESP32-P4 Board #1      │  │  ESP32-P4 Board #2    │
   │   Serial: "MSPEC-RED"    │  │  Serial: "MSPEC-NIR"  │
   │                          │  │                        │
   │   DVP ◄── OV5640 module  │  │  DVP ◄── OV5640       │
   │           + Red filter   │  │          + IR filter   │
   └──────────────────────────┘  └────────────────────────┘
```

## Step-by-Step Assembly

### 1. Mount Filters on OV5640 Modules

The OV5640 module's M12 lens is typically 6-8mm diameter. Use a 1"x1" (25.4mm) square Edmund filter.

Options for mounting:
- **Tape:** Simple, temporary. Place filter flat against lens housing.
- **3D-printed holder:** Design a clip/sleeve that holds the filter in front of the lens.
- **Thread adapter:** If your OV5640 module has M12 threads, you can design a threaded ring holder.

### 2. Remove IR-Cut Filter (NIR Camera Only)

The OV5640 module has a small glass IR-cut filter between the lens and sensor. For the NIR camera:

1. Carefully unscrew the M12 lens from the module
2. Locate the small glass plate (usually blue/purple tint) between lens mount and sensor
3. Gently pry it out with tweezers — it's usually held by adhesive or a retaining ring
4. Reassemble the lens

**Do NOT remove the IR-cut on the Blue, Green, or Red cameras.**

### 3. Connect CSI Cameras

- Use 15-pin FPC ribbon cables
- CSI-0 connector on RPi 5 → Blue camera
- CSI-1 connector on RPi 5 → Green camera
- Lift the connector latch, insert cable (contacts facing the board), close latch

### 4. Connect ESP32-P4 Boards

- Wire OV5640 DVP modules to ESP32-P4 DVP pins (see firmware/README.md for pin map)
- Connect ESP32-P4 USB-C ports to RPi 5 USB-A ports with **data-capable** USB cables
- Power: ESP32-P4 draws power from USB — should be sufficient from RPi 5 at 5V/5A

### 5. White Reference

Place a matte white card (printer paper works for prototyping) at the REF_REGION position in the scene. This is used for flat-field calibration.

## Physical Layout Tips

- Mount all 4 cameras as close together as possible to minimise parallax
- Aim all cameras at the same scene from the same angle
- For field work, consider a 3D-printed bracket that holds all 4 cameras in a 2x2 grid
- The white reference card should be visible to ALL 4 cameras simultaneously
