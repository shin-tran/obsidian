
```bash
# List devices
iwctl device list
# Scan for networks
iwctl station wlan0 scan
# List networks
iwctl station wlan0 get-networks
# Connect with password
iwctl --passphrase=YourPassword station wlan0 connect "MyWiFi"

# Vào iwd không cần gõ iwctl phía trước
iwctl
exit
```

```bash
# Chuyển mặc định về chế độ dòng lệnh (Multi-user target)
sudo systemctl set-default multi-user.target
reboot

# Dùng lại tạm thời GUI
sudo systemctl start [sddm|gdm|lightdm]

# Chuyền mặc định về GUI
sudo systemctl set-default graphical.target
```
