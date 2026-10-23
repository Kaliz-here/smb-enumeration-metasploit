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
Screenshot: `screenshots/metasploit-smb-version-scan.png`
