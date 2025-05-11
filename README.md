Technical detail:

- We use kali linux to simulate the DDoS attack and mitigation.
- The kali linux is hosted using a win11, with 36 cores and 16GB memory assigned.
- We use mininet to build the network topology and simulate the attack
- We have 31 attackers, 1 normal user, and 1 victim server. The attackers and the users are connected to the server via a switch.
- Attackers and user have 1 core each. The server has 4 cores to simulate a low-end server.
- The users will ping the server every 2 seconds to simulate a normal behavior.
- We conducted syn,udp,http flood attack. Payload of packages are all 1200 bytes
- Each experiment consists of 65 seconds
  0-5, attacker do nothing, only user pinging
  6-65, attacks

- Because we use hping3 package flood setting to simulate the attack, it is hard to calculate the exact number of sent packages from the attackers.
  We can only count the received package of the server, however, many are dropped

- The conclusion is that these flood attacks aim to exhaust the CPU rather than the bandwidth of the server.

Mitigation

- Ratelimit. The rate of each package was set to 100 bytes. However, of no use since the vulnerability is CPU
- Whitelist. Use one switch for whitelist user and another switch for non-whitelist user.
  The defense switch’s policy was set to accept 10 requests per second.
  (GMU hopper actually use a white list allowing only GMU IPs to access - you need a VPN if you are not on campus)
