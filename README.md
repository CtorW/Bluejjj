# Arch/Hyprland Bluetooth Fix Script (`fixblue.sh`)

This script automates the common troubleshooting steps required to establish a stable and functional Bluetooth stack on an Arch Linux system, particularly when using the Hyprland Wayland compositor and the PipeWire audio backend.

It resolves typical conflicts (like residual PulseAudio Bluetooth packages) and ensures all necessary services and packages are installed and correctly configured for Bluetooth audio (A2DP/HSP/HFP) via PipeWire.

## Prerequisites

*   **Operating System:** Arch Linux or an Arch-based distribution.
*   **User Permissions:** The script must be run with root privileges (`sudo`).
*   **Audio Backend:** This script is designed for systems using PipeWire for audio management.

## Installation and Usage

1.  **Save the Script:** Save the content of the script as `fixblue.sh`.
2.  **Make Executable:** Grant execution permissions to the script:
    ```bash
    chmod +x fixblue.sh
    ```
3.  **Run the Fix:** Execute the script using `sudo`:
    ```bash
    sudo ./fixblue.sh
    ```

## Key Actions Performed

The `fixblue.sh` script performs the following actions:

*   **Prerequisite Check:** Verifies that the script is run as root and that `pacman` is available.
*   **Conflict Cleanup:**
    *   Removes the potentially conflicting package `pulseaudio-bluetooth`.
    *   Clears old pairing data from `/var/lib/bluetooth` to allow for fresh device pairing.
*   **Package Installation:** Installs or updates the following essential packages:
    *   `bluez` and `bluez-utils` (The core Bluetooth stack and utilities like `bluetoothctl`).
    *   `pipewire`, `pipewire-pulse`, and `wireplumber` (The complete PipeWire audio stack).
    *   `blueman` (A common graphical Bluetooth manager suitable for Hyprland).
    *   `linux-firmware` (To ensure the latest Bluetooth device firmware is present).
*   **Service Management:**
    *   Checks and unblocks Bluetooth devices using `rfkill`.
    *   Enables and starts the system service `bluetooth.service`.
*   **PipeWire Configuration:** Enables and starts the necessary user services for PipeWire integration, including `pipewire-pulse.service` and `wireplumber.service`.

## Post-Reboot Instructions

For all service changes to be fully applied to your user session, a reboot is required.

1.  **Reboot:**
    ```bash
    reboot
    ```
2.  **Connect Devices:** After logging back into Hyprland, you can manage your Bluetooth devices using the graphical utility:
    ```bash
    blueman-manager
    ```
    Alternatively, you can use the command-line tool `bluetoothctl`.
