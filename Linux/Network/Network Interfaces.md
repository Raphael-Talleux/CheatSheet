# Network Interfaces

## Description

A network interface is a network access point for your machine.

Stored in: `/sys/class/net/`  
Configured with: `ip link`

Interfaces can be:

- **Physical** – linked to real hardware: Ethernet card (`eth0`, `enp3s0`, ...), Wi-Fi card (`wlan0`)  
- **Virtual** – created by software for specific purposes:
    - `lo` : loopback (internal communication on the machine)
    - `tun0`/`tap0` : VPN or network tunnels
    - `docker0` : interfaces created by Docker for containers


## Attributes

| Attribute| Description | `ip` Command |
|---------------------|------------|------------------------|
| **Name** | Interface name (`eth0`, `wlan0`, `lo`) | `ip link show` |
| **State** | UP = active, DOWN = inactive | `ip link set <iface> up/down` |
| **MAC Address** | Unique hardware identifier | `ip link show` |
| **MTU** | Maximum Transmission Unit: max packet size | `ip link show` |
| **Flags** | Indicators: broadcast, multicast, loopback, etc. | `ip link show` |
| **IP Addresses** | Assigned IPv4 and IPv6 addresses | `ip addr show` |
| **Associated Routes** | How packets are sent to other networks | `ip route show` |


## Options

Activate / deactivate an interface:  
```bash
sudo ip link set enp3s0 up   # Activate / Activer
sudo ip link set enp3s0 down # Deactivate / Désactiver
````

Change MAC address:

```bash
sudo ip link set dev enp3s0 address 02:01:02:03:04:05
```

Change MTU:

```bash
sudo ip link set dev enp3s0 mtu 1400
```

