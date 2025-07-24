# How to install Glances on Proxmox - the correct way

Background: Messing with the externally managed Python 3 packages on Proxmox isn't recommendet and seem to break functionality. At least that's why I experienced after installing Glances (the traditional way) and in combination with networking setting IP addresses using `ifupdown2`. My assumption therefore is that the Python dependencies required by Glances somehow interfere with the dependencies managed by Proxmox.

This installation method uses `pipx` in order to create an isolated environment for Glances to run in.

## 1. Install pipx

```bash
apt update
apt install pipx
```

## 2. Install Glances

```bash
pipx install 'glances[all]'
```

## 3. Start Glances once

```bash
/root/.local/bin/glances -w
```

(press Ctrl+C to stop)

## 4. Run Glances as a systemd service


**Create a new service file**

```bash
nano /etc/systemd/system/glances.service
```

**Copy and paste the following lines, then save and exit the editor**

```plaintext
[Unit]
Description=Glances Monitoring Tool
After=network.target

[Service]
ExecStart=/root/.local/bin/glances -w
Restart=always

[Install]
WantedBy=multi-user.target
```

**Enable and start the service**

```bash
systemctl enable glances.service
systemctl start glances.service
```

**Now check if the service is running**

```
systemctl status glances.service
```
