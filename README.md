# PowerTop Tunables Auto-Tune Daemon

This daemon is a systemd unit service that automatically applies the `--auto-tune` command when your device boots. This improves the power optimization of the entire device. It is much more reliable than entering it manually after every reboot. For some, this can be a big help, while others will hardly notice a difference since everyone’s hardware is different.
## Installation
1. PowerTop package installation
<details>
<summary><b>Click to see Installation Commands</b></summary>

| Distribution | Command |
| :--- | :--- |
| **Arch Linux** | `sudo pacman -S powertop` |
| **Fedora** | `sudo dnf install powertop` |
| **Debian/Ubuntu** | `sudo apt install powertop` |

</details>
2. Move `powertop.service` file at this path:`/etc/systemd/system/`
3. How to enable it

To ensure the system “sees” the changes and applies them every time it starts up:

  1. Reload the systemd configurations:
  ```bash
  sudo systemctl daemon-reload
  ```
  2. Enable autostart:
  ```bash
  sudo systemctl enable powertop.service
  ```
  3. Start it right now (without waiting for a reboot):
  ```bash
  sudo systemctl start powertop.service
  ```
Sometimes powertop --auto-tune can cause a USB mouse to stop working (it freezes and becomes unresponsive when waking up). If you encounter this issue, you can add an exception for USB devices to ExecStart by uncommenting or add the following line in the file in [Service] group: `ExecStartPost=/bin/sh -c 'for i in /sys/bus/usb/devices/*/power/control; do echo "on" > "$i"; done'`
