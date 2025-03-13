# PowerShell 

## what is PowerShell 

PowerShell is a powerful command-line shell and scripting language designed for system administration and automation, primarily on Windows but also available on macOS and Linux. 

## Use cases 

### Automation
- **Enables the automation of repetitive tasks**, such as:
  - User management
  - System configuration
  - Software deployment
- **Benefits**:
  - Saves time
  - Reduces human error

### System Management
- **Provides deep access to**:
  - System settings
  - Processes
  - Services
- **Allows IT professionals to**:
  - Manage and troubleshoot Windows, macOS, and Linux systems efficiently

### Integration
- **Seamlessly integrates with**:
  - Other Microsoft products (e.g., Active Directory, Exchange, Azure)
  - REST APIs
- **Essential for managing modern IT environments**, including:
  - Cloud infrastructures
  - Hybrid infrastructures

# ISE (integrated Scripting Environment)

### what is the ISE

PowerShell ISE (Integrated Scripting Environment) is a graphical application included with Windows PowerShell that provides a user-friendly interface for writing, testing, and debugging PowerShell scripts.

if you want to run ISE, you can simply type the following command in powershell or you can search it using your desktop search bar. 


```powershell
ise 
```

### Main Benefit of Using ISE
- **IntelliSense**:  
  ISE (Integrated Scripting Environment) provides **IntelliSense**, which offers:
  - Auto-completion for commands, parameters, and variables.
  - Real-time syntax checking and error highlighting.
  - Improved productivity and reduced typing errors for script development.

# Version check 

we can check which version we are using by using the following command : 

```powershell
$psversiontable
```
![version check powershell](/images/power.JPG)

### How to switch between versions 

we can change to a older version of PowerShell if we run the following command :

```powershell
powershell -version 3 
```

- If we need to revert to an older version like version 2 then the process is different: 

### Revert to PowerShell Version 2

1. **Open Control Panel**:
   - Go to **Control Panel > Programs > Programs and Features**.

2. **Turn Windows Features On or Off**:
   - Click **Turn Windows features on or off** in the left-hand menu.

3. **Enable .NET Framework 3.5**:
   - Check the box for **.NET Framework 3.5 (includes .NET 2.0 and 3.0)**.  
     (This triggers a download/installation if not already installed.)


![version check powershell](/images/power2.JPG)


4. **Enable PowerShell 2.0**:
   - In the same window, check the box for **Windows PowerShell 2.0** and click **OK**.

5. **Restart Your System**:
   - Restart your computer for the changes to take effect.


# How to install the lastest version of powershell 

The following command will download the latest version for windows : 

```powershell
 iex "& {$(irm https://aka.ms/install-powershell.ps1)} -UseMSI"
```



- **Breakdown of the Command**:
  - `iex`:  
    - Short for `Invoke-Expression`.  
    - This cmdlet executes a string as a PowerShell command.
  - `& { ... }`:  
    - The `&` operator executes a script block, which is enclosed in `{ ... }`.
  - `$(irm https://aka.ms/install-powershell.ps1)`:  
    - `irm`: Short for `Invoke-RestMethod`, which downloads content from a URL.  
    - The URL `https://aka.ms/install-powershell.ps1` points to a PowerShell script hosted by Microsoft.  
    - `$()` ensures the result of `irm` is executed as part of the script block.
  - `-UseMSI`:  
    - This is a parameter passed to the downloaded script, instructing it to use the MSI installer for installation (instead of other methods like ZIP).

# PowerShell vs CMD 

### Key Difference:
- CMD: Simpler, but limited to basic tasks and has inconsistent syntax across commands.
- PowerShell: More advanced, extensible, and designed for automation and system management, with a consistent and object-oriented syntax.

This comparison highlights PowerShell’s superiority for modern IT tasks, while CMD remains useful for quick, basic operations. The consistent syntax in PowerShell makes it easier to learn and use compared to CMD’s varied syntax.

# Parameters 

The basic syntax structure follows the rule of "verb-noun" / `get-service` 

![version check powershell](/images/power4.JPG)

### Types of required parameters:
Required parameters generally start with two double `[[-Name] <String[]>]`
Another form is when the parameter starts and ends with itself enclosed in brackets followed by a string `[-LogName] <String>`

### Optional parameter:

Single brackets are not required but optional `[-DependentServices]`


# Module 

In PowerShell, a module is a package that contains cmdlets, functions, scripts, variables, and other resources that can be used to perform specific tasks. Modules are a way to organise, distribute, and reuse powershell code. They make it easier to manage and extend powershells functionality. 

- I will show a example of a module later on 

#### Types of Modules: 


- **Script Modules**:
  - Defined in a `.psm1` file.
  - Contains PowerShell scripts and functions.
  - Example: A custom module for managing user accounts.

- **Binary Modules**:
  - Compiled code written in languages like C#.
  - Typically distributed as `.dll` files.
  - Example: Modules provided by Microsoft for managing Active Directory.

- **Manifest Modules**:
  - Defined by a `.psd1` manifest file.
  - Can include scripts, binary modules, or other resources.
  - Example: The PSReadLine module for improving the PowerShell console experience.

- **Dynamic Modules**:
  - Created at runtime using the `New-Module` cmdlet.
  - Not persisted to disk and exists only in memory.


# Alias 

In powershell, an alias is a shorcut or alternate name for a cmdlet, function, script, or executable. Aliases allow you to use shorter or more familiar names for commands, making it faster and easier to work in the shell. 

```powershell 
New-Alias -Name svc -Value Get-Service
```

- **Common Built-in Aliases**:
  - PowerShell comes with many built-in aliases for convenience. Here are some examples:
    - `dir` → `Get-ChildItem`
    - `cd` → `Set-Location`
    - `ls` → `Get-ChildItem` (Unix-like systems)
    - `cls` → `Clear-Host`
    - `rm` → `Remove-Item`
    - `echo` → `Write-Output`
    - `ps` → `Get-Process`


# Running unsupported CMD commands in PowerShell 

![icacls pic](/images/power9.JPG)

The icacls command is a CMD utility for managing file and folder permissions (Access Control Lists or ACLs). The examples in the image show how to grant permissions to the "Backup Operators" group.

- **Command Breakdown**:
  - `icacls c:\test /grant "backup operators":(f)(ci)(oi)`
    - `c:\test`: The target directory.
    - `/grant`: Grants permissions.
    - `"backup operators"`: The user or group to which permissions are granted.
    - `(f)`: Full control.
    - `(ci)`: Container inherit (applies to subdirectories).
    - `(oi)`: Object inherit (applies to files).

- **Key Points**:
  - `--%` is the stop-parsing symbol in PowerShell.
    - It tells PowerShell to treat everything after it as literal text.
    - Useful for running CMD commands, external executables, or scripts with special characters.

![icacls pic](/images/power11.JPG)


```powershell

# I just created a file in my C drive and we providing permissions 

New-Item -ItemType Directory -path C:\test
icacls --% C:\test /grant "backup operators":(oi)(ci)(f)

# Removing Exisiting Flags for a user 

icacls C:\test /remove:John   

```


- The above code is an exmaple of Inheritance Flags, these only apply permissions to the folder, its files, and subfolders. 


| **Flag** | **Full Name**            | **Description**                                                                 |
|----------|--------------------------|---------------------------------------------------------------------------------|
| **(OI)** | Object Inherit           | Applies the permission to files within the folder.                              |
| **(CI)** | Container Inherit        | Applies the permission to subfolders within the folder.                         |
| **(IO)** | Inherit Only             | Applies the permission only to child objects (files/subfolders), not the parent.|
| **(NP)** | No Propagate Inherit     | Prevents the permission from being inherited by further nested objects.         |


| **Permission**      | **Description**                                                                 |
|----------------------|---------------------------------------------------------------------------------|
| **Read (R)**         | Allows viewing or reading the file/folder.                                      |
| **Write (W)**        | Allows modifying or deleting the file/folder.                                  |
| **Execute (X)**      | Allows running the file (if it's an executable) or traversing the folder.      |
| **Full Control (F)** | Grants all permissions, including modifying permissions and deleting the object.|
| **Modify (M)**       | Combines Read, Write, Execute, and Delete permissions.                         |


How They Work Together

Inheritance flags determine where the permissions apply (e.g., files, subfolders).

Permission types determine what actions are allowed (e.g., Read, Write, Execute)




# OGV (Out-GridView)
 
 










# Commands 

| **Command**                              | **Description**                                                                 | **Example**                                                                 |
|------------------------------------------|---------------------------------------------------------------------------------|-----------------------------------------------------------------------------|
| `Get-Command`                            | Lists all available commands in PowerShell.                                      | `Get-Command`                                                               |
| `Get-Help`                               | Displays help information about a command.                                       | `Get-Help Get-Process`                                                     |
| `Get-Process`                            | Retrieves information about running processes.                                   | `Get-Process`                                                              |
| `Get-Service`                            | Lists all services on the system.                                               | `Get-Service`                                                              |
| `Start-Service`                          | Starts a stopped service.                                                       | `Start-Service -Name "Spooler"`                                            |
| `Stop-Service`                           | Stops a running service.                                                        | `Stop-Service -Name "Spooler"`                                             |
| `Restart-Service`                        | Restarts a service.                                                             | `Restart-Service -Name "Spooler"`                                          |
| `Get-ChildItem` (`dir`, `ls`)            | Lists files and directories in a specified location.                            | `Get-ChildItem C:\`                                                        |
| `Set-Location` (`cd`)                    | Changes the current directory.                                                  | `Set-Location C:\Windows`                                                  |
| `New-Item`                               | Creates a new file or directory.                                                | `New-Item -Path "C:\NewFolder" -ItemType Directory`                        |
| `Remove-Item` (`rm`, `del`)              | Deletes a file or directory.                                                    | `Remove-Item C:\OldFile.txt`                                               |
| `Copy-Item` (`cp`)                       | Copies a file or directory.                                                     | `Copy-Item C:\File.txt C:\Backup\File.txt`                                 |
| `Move-Item` (`mv`)                       | Moves a file or directory.                                                      | `Move-Item C:\File.txt C:\NewLocation\File.txt`                            |
| `Rename-Item`                            | Renames a file or directory.                                                    | `Rename-Item C:\OldName.txt NewName.txt`                                   |
| `Get-Content` (`cat`, `type`)            | Displays the contents of a file.                                                | `Get-Content C:\File.txt`                                                  |
| `Set-Content`                            | Writes content to a file.                                                       | `Set-Content C:\File.txt "Hello, World!"`                                  |
| `Add-Content`                            | Appends content to a file.                                                      | `Add-Content C:\File.txt "New Line"`                                       |
| `Get-EventLog`                           | Retrieves event log entries.                                                    | `Get-EventLog -LogName System`                                             |
| `Clear-EventLog`                         | Clears entries from an event log.                                               | `Clear-EventLog -LogName Application`                                      |
| `Get-HotFix`                             | Lists installed hotfixes.                                                       | `Get-HotFix`                                                               |
| `Test-Connection` (`ping`)               | Sends ICMP echo requests to a remote computer.                                  | `Test-Connection google.com`                                               |
| `Invoke-WebRequest` (`curl`, `wget`)     | Sends HTTP/HTTPS requests and retrieves web content.                            | `Invoke-WebRequest -Uri "https://example.com"`                             |
| `Export-Csv`                             | Exports data to a CSV file.                                                     | `Get-Process \| Export-Csv processes.csv`                                  |
| `Import-Csv`                             | Imports data from a CSV file.                                                   | `Import-Csv processes.csv`                                                 |
| `Where-Object` (`?`)                     | Filters objects based on a condition.                                           | `Get-Process \| Where-Object { $_.CPU -gt 50 }`                            |
| `Select-Object` (`select`)               | Selects specific properties of an object.                                       | `Get-Process \| Select-Object Name, CPU`                                   |
| `Sort-Object` (`sort`)                   | Sorts objects by a property.                                                    | `Get-Process \| Sort-Object CPU -Descending`                               |
| `Format-Table` (`ft`)                    | Displays output in a table format.                                              | `Get-Process \| Format-Table Name, CPU`                                    |
| `Format-List` (`fl`)                     | Displays output as a list of properties.                                        | `Get-Process \| Format-List *`                                             |
| `Format-Wide` (`fw`)                     | Displays output in a wide format (multiple columns).                            | `Get-Process \| Format-Wide -Column 4`                                     |
| `Group-Object` (`group`)                 | Groups objects by a property.                                                   | `Get-Process \| Group-Object Status`                                       |
| `Measure-Object`                         | Calculates statistics (e.g., sum, average) for numeric properties.              | `Get-Process \| Measure-Object CPU -Average`                               |
| `Get-Member` (`gm`)                      | Displays properties and methods of an object.                                   | `Get-Process \| Get-Member`                                                |
| `Invoke-Command`                         | Runs commands on remote computers.                                              | `Invoke-Command -ComputerName Server01 -ScriptBlock { Get-Process }`       |
| `Enter-PSSession`                        | Starts an interactive session with a remote computer.                           | `Enter-PSSession -ComputerName Server01`                                   |
| `Exit-PSSession`                         | Exits an interactive remote session.                                            | `Exit-PSSession`                                                           |
| `New-PSSession`                          | Creates a persistent connection to a remote computer.                           | `New-PSSession -ComputerName Server01`                                     |
| `Get-PSSession`                          | Lists active PowerShell sessions.                                               | `Get-PSSession`                                                            |
| `Remove-PSSession`                       | Closes a PowerShell session.                                                    | `Remove-PSSession -Session $session`                                       |
| `Get-Alias`                              | Lists all aliases (shortcuts for commands).                                     | `Get-Alias`                                                                |
| `Set-Alias`                              | Creates or changes an alias.                                                    | `Set-Alias np Notepad`                                                     |
| `Get-History`                            | Displays the command history.                                                   | `Get-History`                                                              |
| `Invoke-History` (`r`)                   | Re-runs a command from the history.                                             | `Invoke-History 5`                                                         |
| `Clear-History`                          | Clears the command history.                                                     | `Clear-History`                                                            |
| `Get-Variable`                           | Lists all variables in the current session.                                     | `Get-Variable`                                                             |
| `Set-Variable`                           | Creates or changes a variable.                                                  | `Set-Variable -Name "MyVar" -Value "Hello"`                                |
| `Remove-Variable`                        | Deletes a variable.                                                             | `Remove-Variable -Name "MyVar"`                                            |
| `Get-ExecutionPolicy`                    | Displays the current execution policy.                                          | `Get-ExecutionPolicy`                                                      |
| `Set-ExecutionPolicy`                    | Changes the execution policy (e.g., to allow script execution).                 | `Set-ExecutionPolicy RemoteSigned`                                         |
| `Get-Date`                               | Retrieves the current date and time.                                            | `Get-Date`                                                                 |
| `Start-Process`                          | Starts a new process.                                                           | `Start-Process notepad`                                                    |
| `Stop-Process`                           | Stops a running process.                                                        | `Stop-Process -Name "notepad"`                                             |
| `Get-NetIPAddress`                       | Retrieves IP address configuration.                                             | `Get-NetIPAddress`                                                         |
| `Test-NetConnection`                     | Tests network connectivity to a remote host.                                    | `Test-NetConnection google.com`                                            |
| `Get-Disk`                               | Retrieves disk information.                                                     | `Get-Disk`                                                                 |
| `Get-Partition`                          | Retrieves partition information.                                                | `Get-Partition`                                                            |
| `Get-Volume`                             | Retrieves volume information.                                                   | `Get-Volume`                                                               |
