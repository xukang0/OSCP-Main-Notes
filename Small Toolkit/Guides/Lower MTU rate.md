
```
sudo ip l s dev tun0 mtu 1250
```

### 2. How do you lower MTU in Kali?

First, identify your network interfaces:

```
ip a
```

Suppose your VPN interface is `tun0`.

Check its current MTU:

```
ip link show tun0
```

You might see:

```
mtu 1500
```

Temporarily lower it to 1400:

```
sudo ip link set dev tun0 mtu 1400
```

Verify:

```
ip link show tun0
```

You can experiment with 1400, 1380, or 1300 if necessary.

To restore the original value:

```
sudo ip link set dev tun0 mtu 1500
```

### 3. When is this relevant to OSCP?

This is particularly relevant when using:

- OpenVPN to connect to OffSec labs.
    
- Ligolo-ng for pivoting.
    
- Chisel tunnels.
    
- SSH port forwarding.
    
- Other encapsulated network connections.
    

For example, if your OpenVPN connection is established but SSH sessions to lab machines keep hanging, lowering the VPN interface MTU is one troubleshooting technique worth trying.

The key takeaway: Lowering MTU doesn't make your network faster. It reduces packet size to avoid packet-delivery problems caused by network limitations, fragmentation, or tunnel overhead.