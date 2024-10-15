**Install Glances**
**Install sudo:**

```javascript
apt update
apt install sudo
```

**Remove EXTERNALLY-MANAGED Marker:**

```javascript
sudo rm -rf /usr/lib/python3.*/EXTERNALLY-MANAGED
```

**Install Required Packages: Ensure you have python3, python3-pip, and python3-psutil installed:**
```
sudo apt update
sudo apt install python3 python3-pip python3-psutil
```
**Install glances**
```
sudo pip3 install glances
```
**Start glances**
```
glances -w
```
**How to make it permament so it does not stope once you are out of shell:**

Create a systemd service file:
```
nano /etc/systemd/system/glances.service
```
**Add the following content:**
```
[Unit]
Description=Glances Monitoring Tool
After=network.target

[Service]
ExecStart=/usr/local/bin/glances -w
Restart=always

[Install]
WantedBy=multi-user.target
```
Save and exit (CTRL + X, then Y)

Enable and start the service:
```
systemctl enable glances.service
systemctl start glances.service
```
Check status:
```
systemctl status glances.service
```
