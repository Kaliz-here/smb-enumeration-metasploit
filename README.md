# SMB Enumeration Using Metasploit

## Project Overview
A hands-on cybersecurity lab focused on understanding SMB service enumeration using the Metasploit Framework.

## Objectives
- Understand the SMB service and TCP port 445.
- Identify SMB enumeration modules in Metasploit.
- Run authorized lab-based enumeration.
- Analyze command output and document observations.
- Learn security implications and defensive recommendations.

## Lab Environment
- Operating System: Kali Linux
- Framework: Metasploit
- Target: Authorized lab machine
- Testing Scope: SMB enumeration only

## Methodology
1. Identify relevant SMB enumeration modules.
2. Select the appropriate module for the lab.
3. Configure the authorized target.
4. Execute the enumeration and analyze the output.
5. Save evidence and document verified findings.

## Results
Practical execution and results will be documented here after testing.

## Security Recommendations
- Restrict SMB access to trusted systems.
- Use appropriate share permissions.
- Disable SMBv1 where it is not required.
- Keep systems patched and monitor SMB activity.

## Disclaimer
All testing is limited to systems I own or have explicit authorization to assess.


## Practical 1: SMB Version Enumeration with Metasploit

### Objective
Identify the SMB service and collect basic service fingerprinting information on an authorized lab target.

### Lab Details
- **Tool:** Metasploit Framework
- **Module:** `auxiliary/scanner/smb/smb_version`
- **Target:** `192.168.1.45`
- **Port:** `445/TCP`

### Observed Results
- SMB service detected.
- Metasploit fingerprinting classified the host as Unix.
- SMB signing was reported as not required.
- Scan completed for 1 configured host.
  
### Evidence
Screenshot: `screenshots/metasploit-smb-version-scan.png.png`


## Practical 2: SMB Share Enumeration

### Objective
Discover SMB shares exposed by an authorized lab server using Metasploit.

### Lab Details
- **Tool:** Metasploit Framework
- **Module:** `auxiliary/scanner/smb/smb_enumshares`
- **Target:** `192.168.1.45`
- **Observed port:** `139/TCP`

### Observed Results
- `print$` — DISK; Printer Drivers
- `tmp` — DISK; description: `oh noes!`
- `opt` — DISK
- `IPC$` — IPC
- `ADMIN$` — IPC, as reported by the module
- Server identification: `metasploitable server (Samba 3.0.20-Debian)`

### Analysis
The scan discovered multiple SMB shares and identified a Samba server banner. Share discovery alone does not establish read/write permissions or prove that the shares are vulnerable.

### Security Recommendations
- Upgrade unsupported Samba versions to a supported release.
- Restrict SMB access to trusted hosts and networks.
- Review share permissions and disable unnecessary shares.
- Avoid exposing SMB services directly to untrusted networks.

### Evidence
Screenshots: `screenshots/metasploit-smb-shares.png`

### Learning Outcome
Practiced configuring a Metasploit auxiliary module, enumerating SMB shares, and interpreting share types and server identification.


## Practical 3: Anonymous SMB Share Access Verification

### Objective
Verify whether an SMB share can be accessed without providing a username or password in an authorized lab environment.

### Tools Used
- Kali Linux
- `smbclient`

### Target
- Lab IP: `192.168.1.45`
- Share: `tmp`

### Commands Used
```bash
smbclient -L //192.168.1.45 -N
smbclient //192.168.1.45/tmp -N
```

Inside the SMB session:
```text
ls
exit
```

### Observed Results
- Anonymous login was successful.
- The server listed available SMB shares.
- Anonymous access to the `tmp` share was successful.
- Directory listing was available, showing entries such as `.ICE-unix` and `.X11-unix`.

### Security Analysis
Anonymous access can expose filenames and directory structure. The security impact depends on the sensitivity of the exposed information and the permissions granted to anonymous users. File read or write access was not verified in this practical.

### Recommendations
- Disable anonymous access if it is not required.
- Restrict SMB shares to authorized users.
- Review share and filesystem permissions.
- Keep Samba updated to a supported version.

### Evidence
Screenshot : `screenshots/smb-anonymous-tmp-listing.png`

### Learning Outcome
Practiced listing SMB shares, connecting to a share anonymously, and verifying directory-listing access with `smbclient`.

