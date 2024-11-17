# Scripting Automation

**PowerShell Automation Examples**

**1. Automate WSUS Patching**

This script automates checking and applying updates from a Windows Server Update Services (WSUS) server.

```powershell
# Import Windows Update Module
Import-Module PSWindowsUpdate

# Check for updates and install them
Get-WindowsUpdate -AcceptAll -Install -IgnoreReboot

# Export update report to a CSV file
Get-WindowsUpdate | Export-Csv -Path "C:\Reports\WSUSUpdates.csv" -NoTypeInformation

# Reboot the system if required
if (Test-PendingReboot) {
    Restart-Computer -Force
}
```

***

**2. Monitor Failed Login Attempts**

Script to monitor and report failed login attempts from the Windows Security Event Log.

```powershell
# Query failed login attempts
Get-WinEvent -FilterHashtable @{
    LogName = 'Security';
    ID = 4625;
    StartTime = (Get-Date).AddHours(-1)
} | ForEach-Object {
    [PSCustomObject]@{
        TimeCreated = $_.TimeCreated
        AccountName = ($_.Properties[5].Value)
        WorkstationName = ($_.Properties[11].Value)
    }
} | Export-Csv -Path "C:\Reports\FailedLogins.csv" -NoTypeInformation
```

***

**3. Check Disk Space on Remote Servers**

Automate the process of checking free disk space on multiple servers.

```powershell
# List of servers
$servers = @("Server1", "Server2", "Server3")

# Check disk space
foreach ($server in $servers) {
    Get-WmiObject -Class Win32_LogicalDisk -ComputerName $server |
    Where-Object { $_.DriveType -eq 3 } |
    Select-Object DeviceID, @{Name="FreeSpace(GB)";Expression={($_.FreeSpace/1GB).ToString("F2")}} |
    Export-Csv -Path "C:\Reports\DiskSpace_$server.csv" -Append -NoTypeInformation
}
```

***

**4. Automate AWS Instance Management**

Manage AWS EC2 instances using PowerShell with the AWS Tools for PowerShell module.

```powershell
# List all EC2 instances
Get-EC2Instance | Select-Object -Property InstanceId, State.Name, Tags

# Start an EC2 instance
Start-EC2Instance -InstanceId "i-0abcd1234efgh5678"

# Stop an EC2 instance
Stop-EC2Instance -InstanceId "i-0abcd1234efgh5678"
```

***

#### **Python Automation Examples**

**1. Automate Nessus Vulnerability Report Parsing**

Parse Nessus reports to identify critical vulnerabilities.

```python
import csv

def parse_nessus_report(file_path):
    with open(file_path, 'r') as report:
        reader = csv.DictReader(report)
        for row in reader:
            if row['Risk'] == 'Critical':
                print(f"Critical vulnerability found: {row['Plugin Name']} on {row['Host']}")

parse_nessus_report('nessus_scan_report.csv')
```

***

**2. Automate AWS S3 Bucket Cleanup**

Identify and delete unused objects in an AWS S3 bucket.

```python
import boto3

s3 = boto3.client('s3')
bucket_name = 'example-bucket'

def delete_unused_objects():
    objects = s3.list_objects_v2(Bucket=bucket_name)
    for obj in objects.get('Contents', []):
        if obj['Size'] == 0:  # Example condition for unused objects
            print(f"Deleting empty object: {obj['Key']}")
            s3.delete_object(Bucket=bucket_name, Key=obj['Key'])

delete_unused_objects()
```

***

**3. Automate Security Group Audits in AWS**

List security groups with overly permissive rules.

```python
import boto3

ec2 = boto3.client('ec2')

def check_security_groups():
    security_groups = ec2.describe_security_groups()
    for sg in security_groups['SecurityGroups']:
        for permission in sg['IpPermissions']:
            for ip_range in permission.get('IpRanges', []):
                if ip_range['CidrIp'] == '0.0.0.0/0':
                    print(f"Security group {sg['GroupName']} has overly permissive rule for {permission['IpProtocol']}.")

check_security_groups()
```

***

**4. Log Anomaly Detection with Machine Learning**

Use Python to detect anomalies in log files using a simple machine learning model.

```python
import pandas as pd
from sklearn.ensemble import IsolationForest

# Load log data
logs = pd.read_csv('log_data.csv')

# Train anomaly detection model
model = IsolationForest(contamination=0.05)
logs['anomaly'] = model.fit_predict(logs[['event_code', 'timestamp']])

# Output anomalies
anomalies = logs[logs['anomaly'] == -1]
print("Detected anomalies:")
print(anomalies)
```

***

#### **General Tips**

1. **Document**: Include comments to explain each step.
2. **Secure Credentials**: Use environment variables or secret management tools for sensitive data.
3. **Test**: Verify your scripts in a test environment before deployment.
4. **Visualize Results**: Generate reports (e.g., CSV or dashboards) to make automation outputs actionable.
