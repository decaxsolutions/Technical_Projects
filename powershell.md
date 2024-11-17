# PowerShell

Here’s a list of **useful PowerShell commands** for automation and tasks frequently performed by **system administrators** and **network administrators**:

***

#### **1. General System Administration**

**System Information**

*   Get system information:

    ```powershell
    Get-ComputerInfo
    ```
*   Check OS version:

    ```powershell
    [System.Environment]::OSVersion
    ```

**Manage Services**

*   List all services:

    ```powershell
    Get-Service
    ```
*   Start, stop, or restart a service:

    ```powershell
    Start-Service -Name "ServiceName"
    Stop-Service -Name "ServiceName"
    Restart-Service -Name "ServiceName"
    ```

**Manage Processes**

*   List running processes:

    ```powershell
    Get-Process
    ```
*   Kill a process:

    ```powershell
    Stop-Process -Name "ProcessName" -Force
    ```

***

#### **2. File and Folder Management**

**File Operations**

*   Create a file:

    ```powershell
    New-Item -Path "C:\Example.txt" -ItemType File
    ```
*   Read a file:

    ```powershell
    Get-Content -Path "C:\Example.txt"
    ```
*   Write to a file:

    ```powershell
    Set-Content -Path "C:\Example.txt" -Value "Hello, World!"
    ```

**Folder Operations**

*   Create a folder:

    ```powershell
    New-Item -Path "C:\NewFolder" -ItemType Directory
    ```
*   Copy a folder:

    ```powershell
    Copy-Item -Path "C:\SourceFolder" -Destination "C:\DestinationFolder" -Recurse
    ```

**Search for Files**

*   Search for a file in a directory:

    ```powershell
    Get-ChildItem -Path "C:\Folder" -Filter "*.txt" -Recurse
    ```

***

#### **3. User and Group Management**

**Active Directory Commands (requires `Active Directory` module)**

*   Add a new user:

    ```powershell
    New-ADUser -Name "John Doe" -SamAccountName "jdoe" -UserPrincipalName "jdoe@example.com" -Path "OU=Users,DC=example,DC=com"
    ```
*   Add a user to a group:

    ```powershell
    Add-ADGroupMember -Identity "GroupName" -Members "jdoe"
    ```
*   List group members:

    ```powershell
    Get-ADGroupMember -Identity "GroupName"
    ```

**Local User Commands**

*   Create a local user:

    ```powershell
    New-LocalUser -Name "LocalUser" -Password (ConvertTo-SecureString "Password123" -AsPlainText -Force)
    ```
*   Add a local user to a group:

    ```powershell
    Add-LocalGroupMember -Group "Administrators" -Member "LocalUser"
    ```

***

#### **4. Networking**

**Network Configuration**

*   View IP configuration:

    ```powershell
    Get-NetIPConfiguration
    ```
*   Set a static IP:

    ```powershell
    New-NetIPAddress -InterfaceAlias "Ethernet0" -IPAddress "192.168.1.100" -PrefixLength 24 -DefaultGateway "192.168.1.1"
    ```
*   Configure DNS servers:

    ```powershell
    Set-DnsClientServerAddress -InterfaceAlias "Ethernet0" -ServerAddresses "8.8.8.8","8.8.4.4"
    ```

**Network Diagnostics**

*   Test network connectivity (ping equivalent):

    ```powershell
    Test-Connection -ComputerName "8.8.8.8"
    ```
*   Display open network connections:

    ```powershell
    Get-NetTCPConnection
    ```

***

#### **5. System Monitoring and Troubleshooting**

**Disk Management**

*   Check free disk space:

    ```powershell
    Get-PSDrive -PSProvider FileSystem
    ```
*   Format a disk:

    ```powershell
    Format-Volume -DriveLetter F -FileSystem NTFS
    ```

**Event Logs**

*   View system logs:

    ```powershell
    Get-EventLog -LogName "System" -Newest 10
    ```
*   Export logs:

    ```powershell
    Get-EventLog -LogName "Application" | Export-Csv -Path "C:\ApplicationLogs.csv"
    ```

**Process Monitoring**

*   Check high CPU usage:

    ```powershell
    Get-Process | Sort-Object CPU -Descending | Select-Object -First 10
    ```

***

#### **6. Automation and Scripting**

**Scheduled Tasks**

*   Create a scheduled task:

    ```powershell
    New-ScheduledTaskAction -Execute "notepad.exe" | 
    Register-ScheduledTask -TaskName "OpenNotepad" -Trigger (New-ScheduledTaskTrigger -Once -At "2:00PM")
    ```
*   View scheduled tasks:

    ```powershell
    Get-ScheduledTask
    ```

**Run Remote Commands**

*   Execute a command on a remote machine:

    ```powershell
    Invoke-Command -ComputerName "RemotePC" -ScriptBlock { Get-Service }
    ```
*   Enable remote PowerShell:

    ```powershell
    Enable-PSRemoting -Force
    ```

***

#### **7. Security and Auditing**

**Audit Logs**

*   Get recent failed logins:

    ```powershell
    Get-WinEvent -LogName Security | Where-Object { $_.Id -eq 4625 } | Select-Object TimeCreated, Message
    ```

**Permissions**

*   Get folder permissions:

    ```powershell
    Get-Acl -Path "C:\Folder" | Format-List
    ```
*   Set folder permissions:

    ```powershell
    $acl = Get-Acl "C:\Folder"
    $rule = New-Object System.Security.AccessControl.FileSystemAccessRule("UserName", "FullControl", "Allow")
    $acl.SetAccessRule($rule)
    Set-Acl -Path "C:\Folder" -AclObject $acl
    ```

***

#### **8. Useful Shortcuts**

*   List all PowerShell modules:

    ```powershell
    Get-Module -ListAvailable
    ```
*   Import a module:

    ```powershell
    Import-Module ActiveDirectory
    ```
*   Get help for a command:

    ```powershell
    Get-Help Get-Process -Full
    ```

***

These commands cover a broad range of tasks that sysadmins and network admins perform regularly.
