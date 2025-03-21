# **ZaneyOS FAQ (v2.3)**  
- **Revision:** v1.06  
- **Date:** 20-Mar-2025  

---

<details>
<summary><strong>What is ZaneyOS and Why Was It Created?</strong></summary>

Originally, **ZaneyOS** was simply a **personal configuration** stored in a Git repository to **promote NixOS and Hyprland**, offering a **stable and working** setup. It was **never intended** as a full-fledged NixOS distribution.  

The name **ZaneyOS** started as an inside joke among friends. The goal is for users to **fork, modify, and customize** it to fit their own needs. If you find bugs or add features, contributions are always welcome!  

> **Note:** **ZaneyOS is NOT a standalone distro.** There are **no plans** to provide an installation ISO.

</details>

---

## **System Configuration**

<details>
<summary><strong>How Do I Change the Timezone?</strong></summary>

1. Edit the file:  
   ```bash
   ~/zaneyos/modules/core/system.nix
   ```
2. Modify the line:  
   ```nix
   time.timeZone = "America/New_York";
   ```
3. Save and rebuild using:  
   ```bash
   fr  # Flake Rebuild alias
   ```

</details>

<details>
<summary><strong>How Do I Configure Monitor Settings?</strong></summary>

- Monitor settings are in:  
  ```bash
  ~/zaneyos/hosts/<HOSTNAME>/variables.nix
  ```
- Format:  
  ```bash
  monitor=<video_adapter>,<resolution>@<refresh_rate>,auto,<scale>
  ```

**Example Configs:**
```nix
extraMonitorSettings = "monitor=eDP-1,1920x1080@60,auto,1";
```

```nix
extraMonitorSettings = "
  monitor=eDP-1,1920x1080@60,auto,auto
  monitor=HDMI-A-1,2560x1440@75,auto,auto
";
```

- To list monitors:  
  ```bash
  hyprctl monitors
  ```

- GUI alternative: **nwg-displays**, similar to `arandr`, will generate a compatible `monitors.conf`.

</details>

<details>
<summary><strong>How Do I Change the Hostname?</strong></summary>

1. Copy the current host directory:  
   ```bash
   cp -rp ~/zaneyos/hosts/OLD-HOSTNAME ~/zaneyos/hosts/NEW-HOSTNAME
   ```
2. Edit `flake.nix`:  
   ```nix
   host = "NEW-HOSTNAME";
   ```
3. Add the changes to Git:  
   ```bash
   git add .
   ```
4. Rebuild and reboot:  
   ```bash
   fr
   ```

</details>

<details>
<summary><strong>How Do I Change the Kernel Version?</strong></summary>

1. Edit the **hardware.nix** file for the host:  
   ```bash
   ~/zaneyos/hosts/<HOSTNAME>/hardware.nix
   ```
2. Add or update this line:  
   ```nix
   boot.kernelPackages = lib.mkForce pkgs.linuxPackages_6_12;
   ```
3. Apply the change:  
   ```bash
   fr
   ```

</details>

---

## **Package Management**

<details>
<summary><strong>How Do I Install New Applications?</strong></summary>

- **For all hosts:**  
  Edit:  
  ```bash
  ~/zaneyos/modules/core/packages.nix
  ```

- **For a specific host:**  
  Edit:  
  ```bash
  ~/zaneyos/hosts/<HOSTNAME>/host-packages.nix
  ```

- Then rebuild the system:  
  ```bash
  fr
  ```

</details>

<details>
<summary><strong>How Do I Update Installed Packages?</strong></summary>

Run the following command:  
```bash
fu  # Flake Update
```

</details>

<details>
<summary><strong>How Do I Remove Old Generations?</strong></summary>

To delete **all but the current generation**:  
```bash
ncg  # NixOS Clean Generations
```

> ⚠️ Make sure you're currently booted into the latest generation before running this.

</details>

---
