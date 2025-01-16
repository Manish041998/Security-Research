# Windows Command Reference for Security Analysis

## Techniques Table
| **Command**         | **Description**                                                                 | **Attacker's Purpose**                                                                                  |
|---------------------|-----------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------|
| `ver`              | Displays the Windows version.                                               | Identifies the OS version to tailor attacks (e.g., compatible exploits).                               |
| `systeminfo`       | Lists detailed system information, including OS build, hardware, and hotfixes. | Gathers information on installed patches, hardware, and OS for vulnerability identification.          |
| `ipconfig`         | Shows network configuration details like IP address, DNS, and gateway.        | Collects network information to locate targets or misconfigured systems.                              |
| `route`            | Displays the routing table for network traffic.                              | Identifies network routes to understand potential pathways for lateral movement.                       |
| `arp`              | Displays the ARP table (MAC-to-IP mappings).                                 | Maps connected devices in the network to identify targets.                                             |
| `netstat`          | Shows active network connections, listening ports, and their states.         | Discovers open ports and active connections for reconnaissance or pivoting.                           |
| `net`              | A suite of subcommands for managing network resources and users              | Gathers user, group, and shared resource details to find misconfigurations or potential entry points. |
| `whoami`           | Displays the current user and security group memberships.                    | Confirms privileges and checks group memberships for possible privilege escalation.                    |
| `wmic`             | Queries system management information (e.g., user accounts, processes).      | Enumerates users, processes, and services to identify vulnerabilities or attack opportunities.         |
| `set`              | Displays environment variables.                                              | Finds useful environment variables for potential exploitation (e.g., paths, credentials, or temporary files). |
| `netsh`            | Manages network and firewall settings.                                       | Checks firewall rules to identify allowed programs or open ports for bypassing security.              |
| `tasklist`         | Displays running processes and associated services.                          | Identifies active processes for privilege escalation or identifying security software.                 |
| `powershell get-hotfix` | Lists installed updates on the system.                                  | Identifies missing updates for known vulnerabilities to exploit.                                      |
| `reg query`        | Queries registry keys and values.                                            | Inspects critical registry entries for persistence mechanisms, security settings, or misconfigurations. |
| `dir`              | Lists the contents of directories, including file names and attributes.      | Finds sensitive files, such as configurations or credentials.                                         |
| `tree`             | Displays the directory structure in a tree format.                           | Quickly maps the folder hierarchy to locate valuable files or paths.                                  |

---

## Breakdown by Discovery Subcategories

### 1. System Information Gathering
- **Commands:**
  - `ver`
  - `systeminfo`
  - `set`

### 2. Network Configuration and Connectivity
- **Commands:**
  - `ipconfig -all`
  - `ipconfig /displaydns`
  - `route print`
  - `arp -a`
  - `netstat -a -n`

### 3. User Enumeration
- **Commands:**
  - `whoami /all`: List current user and associated privileges.
  - `wmic useraccount get name,sid`: Retrieve all local user accounts and their SIDs.
  - `net user`: Retrieve local user account details.
  - `net localgroup`: List local groups and group memberships.

### 4. Shared Resources and Connections
- **Commands:**
  - `net share`: Enumerate shared resources.
  - `net use`: List mapped network drives and active SMB connections.

### 5. System Configuration
- **Commands:**
  - `net accounts`: Retrieve account policies such as password policies.
  - `net config`: List workstation or server configurations.
  - `net time \127.0.0.1`: Query the system time of the local machine.

### 6. Firewall and Security Policies
- **Commands:**
  - `netsh firewall show portopening`
  - `netsh firewall show allowedprogram`
  - `netsh firewall show config`

### 7. Process and Service Enumeration
- **Commands:**
  - `tasklist /v`
  - `tasklist /svc`

### 8. Patch and Hotfix Information
- **Commands:**
  - `echo . | powershell get-hotfix`

### 9. Registry Enumeration
- **Commands:**
  - `reg query HKLM\Software\Microsoft\Windows\CurrentVersion\Policies\System /s`: List all registry values in the System policies section.
  - `reg query HKLM\Software\Microsoft\Windows\CurrentVersion\Policies\System /v EnableLUA`: Check the status of User Account Control (UAC).
  - `reg query HKCU\Software\Microsoft\Windows\CurrentVersion\Run`: List startup programs for the current user.
  - `reg query HKLM\Software\Microsoft\Windows\CurrentVersion\Run`: List startup programs for all users.
  - `reg query HKLM\Software\Microsoft\Windows\CurrentVersion\RunOnce`: List one-time startup programs.
  - `reg query HKLM\Software\Wow6432Node\Microsoft\Windows\CurrentVersion\Run`: List 32-bit startup programs for all users.
  - `reg query HKLM\Software\Wow6432Node\Microsoft\Windows\CurrentVersion\RunOnce`: List one-time 32-bit startup programs.

### 10. File and Directory Enumeration
- **Commands:**
  - `dir /x c:\`: List files and directories on the root of the C drive (with short names).
  - `dir /x c:\users\`: List files and directories in the Users folder.
  - `dir %tmp%`: List files and directories in the temporary folder.
  - `dir "c:\program files (x86)" /x`: List files in the Program Files (x86) folder.
  - `dir "c:\program files" /x`: List files in the Program Files folder.
  - `tree "%UserProfile%\Desktop" /A`: Display a tree structure of the user's desktop folder.
  - `tree "%UserProfile%\Documents" /A`: Display a tree structure of the user's documents folder.
  - `tree "%UserProfile%\Downloads" /A`: Display a tree structure of the user's downloads folder.
  - `dir /x "c:\windows\microsoft.net\framework"`: List files in the .NET Framework directory.
