# NetSeer

**Lightweight Network Visibility and Traffic Intelligence for Edge Devices**

NetSeer is a minimal yet powerful network observation and visualization tool designed to run efficiently on small form-factor devices like the Raspberry Pi Zero.
It passively inspects packets, summarizes flow data, and presents insights through a simple LAN-accessible web dashboard.

Whether you’re monitoring a home lab, experimenting with IoT segmentation, or visualizing network behavior in real time — NetSeer gives you visibility without the noise.

---

## 🚀 Overview

Traditional network analyzers are either **too heavy** or **too limited** for small edge nodes.
NetSeer bridges that gap — combining eBPF-powered packet capture with lightweight analytics and visualization.

**Core Goals:**

* Zero external dependencies or cloud connections
* Run entirely on LAN or isolated networks
* Intuitive, web-based interface for live packet summaries
* Modular backend for experimentation with BPF, psutil, and custom metrics

**Designed for:**

* Raspberry Pi / ARM boards
* Home networks, test labs, and air-gapped environments
* Developers and researchers exploring local network behavior

---

## 🧩 Architecture

```
        ┌────────────────────┐
        │  Network Interface │
        └──────────┬─────────┘
                   │
             eBPF Capture (bcc)
                   │
        ┌──────────▼──────────┐
        │  NetSeer Core (py)  │
        │  ├─ Flow Analysis    │
        │  ├─ Protocol Stats   │
        │  └─ System Metrics   │
        └──────────┬──────────┘
                   │
            REST + Web UI
                   │
        ┌──────────▼──────────┐
        │  LAN Dashboard      │
        └─────────────────────┘
```

The system combines **BCC (BPF Compiler Collection)** for kernel-level packet inspection with **Python-based summarization** for real-time visualization.

---

## ⚙️ Installation

### 1. From source

<details><summary>Expand for details</summary>

1. **Clone the repository or download the sources**

   ```bash
   git clone https://github.com/yourusername/netseer.git
   cd netseer
   ```

2. **Install BCC (BPF Compiler Collection) for Python**

   On Debian/Ubuntu:

   ```bash
   sudo apt install python3-bcc
   ```

   On Fedora:

   ```bash
   sudo dnf install python3-bcc
   ```

3. **Install dependencies**

   ```bash
   pip install --user psutil setuptools
   ```

4. **Install NetSeer**

   ```bash
   python3 setup.py install --user
   ```

   To view other build/install options:

   ```bash
   python3 setup.py --help
   ```

5. **(Optional)** Run directly without installing

   ```bash
   python3 netseer.py
   ```

</details>

---

## 🌐 Accessing the Web Dashboard

Once NetSeer is running, open your browser and visit:

```
http://<your-device-ip>:5100
```

You’ll see:

* Live packet summaries
* Active hosts and flows
* Protocol breakdowns (TCP, UDP, ICMP)
* Device resource stats (CPU, memory, network IO)

---

## 🧱 System Integration (Optional)

You can set up NetSeer as a background service:

```bash
sudo nano /etc/systemd/system/netseer.service
```

```ini
[Unit]
Description=NetSeer Network Monitor
After=network.target

[Service]
ExecStart=/usr/bin/python3 /home/pi/netseer/netseer.py
Restart=always
User=pi

[Install]
WantedBy=multi-user.target
```

Enable and start:

```bash
sudo systemctl enable netseer
sudo systemctl start netseer
```

---

## 📈 Future Roadmap

* [ ] Live traffic map (D3.js or lightweight React UI)
* [ ] Prometheus-compatible metrics exporter
* [ ] Custom rule-based alerting
* [ ] Sensor chaining for multi-node visibility
* [ ] Integration with DNS Sinkhole logs

---

## 🔒 Security Notes

NetSeer runs locally and does **not** transmit data externally.
No packets leave your network; no analytics are shared.
For safety, avoid exposing the dashboard to the internet directly — use LAN or VPN access only.

---

## 📚 License

See [LICENSE](./LICENSE) for full text.

---

## 🧭 Why NetSeer?

Because network visibility shouldn’t require a data center.
NetSeer is about **understanding your traffic** — quietly, efficiently, and entirely under your control.
