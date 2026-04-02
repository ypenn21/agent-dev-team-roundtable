---
name: kill-port
description: Kills a process listening on a specific port. Use this skill when a server fails to start because a port is already in use (e.g., EADDRINUSE) or when explicitly asked to free up a port.
---
# Killing Processes on Port XXXX

When a process is blocking a specific port and needs to be terminated, use the local custom script `npx kill-port`.

## How to use

Run the following command, replacing `$PORT` with the actual port number (e.g., 3000, 8080):

```bash
npx kill-port <port_number>
```

### Examples

- If a web server fails to start due to port 3000 being in use:
  ```bash
  npx kill-port 3000
  ```

- If you need to stop whatever is running on port 8080:
  ```bash
  npx kill-port 8080
  ```

### Important Notes
- This uses a custom script installed on this machine.
- Do not attempt to use `lsof` or `netstat` to find PIDs and kill them manually unless `npx kill-port` fails. This script is the preferred and safest method.
