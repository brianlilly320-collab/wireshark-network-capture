
# Network Packet Capture & UDP Stream Analysis with Wireshark

A hands-on networking lab demonstrating live packet sniffing and stream isolation on a virtualized Linux environment using **Wireshark**.

---

## 📋 Overview

This lab focuses on capturing real-time network traffic across a virtual Ethernet interface (eth0) and applying display filters to isolate specific User Datagram Protocol (UDP) conversations for protocol and payload inspection.

---

## 🛠️ Lab Environment & Tools

* **Host OS:** Windows 11
* **Hypervisor:** Oracle VM VirtualBox
* **Guest OS:** Linux (Kali / Debian-based)
* **Network Interface:** eth0 (Virtual Ethernet Adapter)
* **Protocol Analyzer:** Wireshark

---

## ⚙️ Configuration & Methodology

### 1. Live Interface Capture
* Launched **Wireshark** inside the Linux guest VM.
* Selected the primary network interface (eth0) and started a live packet capture session (Capturing from eth0).

### 2. Stream Isolation via Display Filter
To eliminate background noise and focus on a single communication session, the following display filter was applied:

udp.stream eq 0


* **Filter Purpose:** Isolates all packets belonging exclusively to the first captured UDP conversation (stream index 0).
* **Status:** Valid syntax confirmed (indicated by the green filter bar).

---

## 🖥️ Wireshark Interface Breakdown

| Pane | Purpose in Lab |
| :--- | :--- |
| **Packet List (Top)** | Displays captured frames matching udp.stream eq 0 with columns for No., Time, Source, Destination, Protocol, Length, and Info. |
| **Packet Details (Middle)** | Expands the selected packet into layered protocol headers (Frame, Ethernet II, IPv4/IPv6, UDP). |
| **Packet Bytes (Bottom)** | Shows the raw hexadecimal and ASCII representation of the packet payload. |

---

## 🚀 How to Reproduce

1. Boot your Linux virtual machine in **Oracle VirtualBox**.
2. Open a terminal or application menu and launch **Wireshark** (with root/packet-capture privileges).
3. Double-click **eth0** to begin capturing live traffic.
4. Generate UDP traffic (e.g., via DNS lookup nslookup example.com or netcat -u).
5. Enter udp.stream eq 0 in the display filter bar and press **Enter** to isolate the first UDP stream.
6. Right-click any captured packet and select **Follow > UDP Stream** to inspect the full payload exchange.

---

## 📝 Notes & Observations

* When no matching UDP stream has been initialized yet, the Packet List pane remains empty while the capture engine actively listens on eth0.
* Ensure VirtualBox network settings (NAT / Bridged / Internal Network) match your target traffic scope before capturing.
