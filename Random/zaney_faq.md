# **ZaneyOS FAQ (v2.3)**  

- **Revision:** v1.06  
- **Date:** 20-Mar-2025  

---

## **What is ZaneyOS and Why Was It Created?**  

Originally, **ZaneyOS** was simply a **personal configuration** stored in a Git repository to **promote NixOS and Hyprland**, offering a **stable and working** setup. It was **never intended** as a full-fledged NixOS distribution.  

The name **ZaneyOS** started as an inside joke among friends. The goal is for users to **fork, modify, and customize** it to fit their own needs. If you find bugs or add features, contributions are always welcome!  

> **Note:** **ZaneyOS is NOT a standalone distro.** There are **no plans** to provide an installation ISO.

---

## **System Configuration**  

### **How Do I Change the Timezone?**  
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

---

### **How Do I Configure Monitor Settings?**  
- Monitor settings are in:  
  ```bash
  ~/zaneyos/hosts/<HOSTNAME>/variables.nix
  ```
- Format:  
  ```bash
  monitor=<video_adapter>,<resolution>@<refresh_rate>,auto,<scale>
  ```
- **Example Configurations:**  
  - **Single Monitor:**  
    ```nix
    extraMonitorSettings = "monitor=eDP-1,1920x1080@60,auto,1";
    ```
  - **Multiple Monitors:**  
    ```nix
    extraMonitorSettings = "
      monitor=eDP-1,1920x1080@60,auto,auto
      monitor=HDMI-A-1,2560x1440@75,auto,auto
    ";
    ```
- To find monitor names, run:  
  ```bash
  hyprctl monitors
  ```
- For a **GUI tool**, use **nwg-displays**, similar to `arandr`, which generates a Hyprland-compatible config.

---

## **Package Management**  

### **How Do I Install New Applications?**  
- **For ALL hosts:** Edit:  
  ```bash
  ~/zaneyos/modules/core/packages.nix
  ```
- **For a SPECIFIC host:** Edit:  
  ```bash
  ~/zaneyos/hosts/<HOSTNAME>/host-packages.nix
  ```
- Then, rebuild with:  
  ```bash
  fr  # Flake Rebuild
  ```

---

### **How Do I Update Installed Packages?**  
Run:  
```bash
fu  # Flake Update
```
This fetches and installs the latest package updates.

---

### **How Do I Remove Old Generations?**  
To delete **all but the latest** system generation:  
```bash
ncg  # NixOS Clean Generations
```
> **Note:** Ensure you've **booted into the latest generation** before running this command.

---

## **System Customization**  

### **How Do I Change the Hostname?**  
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

---

### **How Do I Change the Kernel Version?**  
1. Edit the **hardware.nix** file for the host:  
   ```bash
   ~/zaneyos/hosts/<HOSTNAME>/hardware.nix
   ```
2. Modify the **kernelPackages** line:  
   ```nix
   boot.kernelPackages = lib.mkForce pkgs.linuxPackages_6_12;
   ```
3. Apply changes with:  
   ```bash
   fr
   ```

---

## **Stylix & Theming**  

### **How Do I Enable or Disable Stylix?**  
- **Enable Stylix:**  
  Edit `~/zaneyos/modules/core/stylix.nix`, uncomment:  
  ```nix
  stylix.enable = true;
  ```
- **Disable Stylix:**  
  Comment out the `base16Scheme` section.  
- Apply changes:  
  ```bash
  fr
  ```

---

### **How Do I Change the Wallpaper?**  
- Manually:  
  ```bash
  SUPER + ALT + W  # Change wallpaper
  ```
- To auto-change wallpaper every **X seconds**:  
  1. Edit `~/zaneyos/modules/home/scripts/wallsetter`  
  2. Change the **TIMEOUT** value.  
  3. Rebuild with `fr`, then logout or reboot.

---

## **Terminal Configurations**  

### **Kitty Keybindings**  
Configured in:  
```bash
~/zaneyos/modules/home/kitty.nix
```
Default keybindings:  
```bash
CTRL + SHIFT + V      # Paste
CTRL + SHIFT + K      # Scroll up
CTRL + SHIFT + J      # Scroll down
ALT + N              # New window
ALT + W              # Close window
CTRL + SHIFT + ENTER # Split horizontally
```
  
---

### **WezTerm Setup**  
To enable WezTerm:  
1. Edit `~/zaneyos/modules/home/wezterm.nix`:  
   ```nix
   enable = true;
   ```
2. Rebuild:  
   ```bash
   fr
   ```

**WezTerm Default Keybindings:**  
```bash
ALT + T              # Open new tab
ALT + W              # Close current tab
ALT + V              # Vertical split
ALT + H              # Horizontal split
ALT + Arrow Keys     # Move between panes
```

---

## **Updating ZaneyOS**  

### **How Do I Update to a New Version?**  
#### **For v2.3+**  
1. **Backup your config**:  
   ```bash
   cp -rp ~/zaneyos ~/Backup-ZaneyOS
   ```
2. **Pull the latest changes**:  
   ```bash
   git stash && git pull
   ```
3. **Restore your host files**:  
   ```bash
   cp -rp ~/Backup-ZaneyOS/hosts/HOSTNAME ~/zaneyos/hosts
   ```
4. **Rebuild**:  
   ```bash
   git add . && fr
   ```

#### **For v2.0 - 2.2**  
- **No direct update path.** **Reinstall using `install-zaneyos.sh`** and manually migrate your configs.

#### **For v1.x**  
- Completely different structure. **Full reinstall required.**  

---

## **Advanced Topics**  

### **How Do I Configure a Hybrid Intel/NVIDIA Laptop?**  
1. Select `nvidia-laptop` template during installation, or manually set:  
   ```nix
   host = "nvidia-prime";
   ```
2. Configure GPU PCI IDs in:  
   ```bash
   ~/zaneyos/hosts/HYBRID-HOST/variables.nix
   ```
3. Adjust `AQ_DRM_DEVICES` in `hyprland/config.nix` if needed.  
4. **Rebuild and reboot.**  

---

## **Where Can I Learn More?**  
- [NixOS Config Guide](https://www.youtube.com/watch?v=AGVXJ-TIv3Y&t=34s)  
- [Managing NixOS with Git](https://www.youtube.com/watch?v=20BN4gqHwaQ)  
- [Git for Beginners](https://www.youtube.com/watch?v=K6Q31YkorUE)  

---

This keeps **ALL** the original content **but refines it for clarity**. Let me know if you need **further tweaks!**
