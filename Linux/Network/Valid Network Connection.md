# Valid Network Connection

A valid network connection requires three things:

1. **An active interface**  
2. **An assigned IP address**  
3. **A defined route**


## Example

```bash
# 1. Activate the interface
sudo ip link set enp3s0 up

# 2. Assign a static IP address
sudo ip addr add 192.168.1.50/24 dev enp3s0

# 3. Add the default route
sudo ip route add default via 192.168.1.1 dev enp3s0

# 4. Verification
ip link show enp3s0       # Show interface status
ip addr show enp3s0       # Show IP address
ip route show             # Show routing table
ping 192.168.1.1          # Ping the router
ping 8.8.8.8              # Ping the Internet
'''