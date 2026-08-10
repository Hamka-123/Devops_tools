# 🖥️ WSL Remote Automation

A small automation utility for working with **WSL running on a remote Windows Server** from a macOS client over SSH.

The tool combines PowerShell and Bash to simplify a workflow where commands need to travel through several execution environments:

```text id="x9k5jm"
macOS
  │
  │ SSH
  ▼
Windows Server
  │
  │ PowerShell / wsl.exe
  ▼
WSL
  │
  │ Bash
  ▼
Linux commands
```

## 🎯 Purpose

The utility was created to simplify repetitive operations when working with WSL on a remote Windows machine.

It helps with:

* discovering available WSL distributions;
* selecting the target distribution interactively;
* passing Bash commands from Windows into WSL;
* handling Windows/Unix line-ending differences;
* executing a predefined set of Linux commands;
* making the remote workflow easier to reproduce.

---

## 🛠️ Requirements

### Client

* macOS
* OpenSSH client

### Remote server

* Windows Server
* OpenSSH Server
* WSL
* at least one installed WSL distribution
* PowerShell

---

# 🚀 Quick Start

## 1. Enable SSH on Windows Server

Run PowerShell as Administrator:

```powershell
Start-Service sshd
```

If the SSH firewall rule does not already exist:

```powershell
New-NetFirewallRule `
  -Name "SSH" `
  -DisplayName "SSH 22" `
  -Direction Inbound `
  -Protocol TCP `
  -LocalPort 22 `
  -Action Allow
```

Verify that the SSH service is running:

```powershell
Get-Service sshd
```

---

## 2. Prepare the Scripts

The utility uses two scripts:

```text id="2l4g9x"
script.ps1
commands.sh
```

### `script.ps1`

The PowerShell script acts as the Windows-side controller.

It:

* discovers available WSL distributions;
* allows the user to select a distribution;
* prepares commands for execution;
* invokes `wsl.exe`;
* passes the commands into the selected Linux environment.

### `commands.sh`

The Bash script contains the Linux-side commands to execute inside WSL.

Example operations include:

```bash id="3v1j9c"
sudo apt update
df -h
ln -s ...
```

The command set can be extended depending on the task.

---

# ▶️ Running the Tool

Connect to the Windows Server from macOS:

```bash id="n0o6jd"
ssh user@192.168.1.233
```

Run the PowerShell controller:

```powershell id="r5b6cd"
powershell.exe -ExecutionPolicy Bypass -File .\script.ps1
```

The script detects available WSL distributions and starts the selected environment.

---

# 🔤 Line Endings: CRLF vs LF

One of the practical problems this utility addresses is the difference between Windows and Unix line endings.

Windows commonly uses:

```text
CRLF
```

while Linux expects:

```text
LF
```

If `commands.sh` contains Windows-style line endings, Linux may interpret the carriage-return character as part of a command:

```text
\r: command not found
```

Make sure the Bash script is saved using **LF** line endings.

In VS Code, the current line-ending format is shown in the bottom-right corner of the editor.

You can also check or convert the file from the command line:

```bash
file commands.sh
```

---

# 🔐 SSH Without a Password

For repeated use, SSH key authentication is more convenient than entering a password every time.

Generate a key if necessary:

```bash
ssh-keygen
```

Then copy the public key to the remote machine:

```bash
ssh-copy-id user@192.168.1.233
```

After configuring key-based authentication, the connection can be established without an interactive password prompt.

---

# 🔧 Extending the Tool

The Linux-side workflow is intentionally kept separate from the Windows-side controller.

To add another Linux operation, update:

```text
commands.sh
```

For example:

```bash
sudo apt update
df -h
tree
```

The PowerShell controller does not need to know the details of each Linux command.

This separation makes it possible to reuse the same Windows/WSL transport layer with different command sets.

---

# 🧩 Execution Model

The complete workflow can be summarized as:

```text id="2j5qcf"
SSH connection
      │
      ▼
Windows Server
      │
      ▼
script.ps1
      │
      ├── Discover WSL distributions
      │
      ├── Select distribution
      │
      ▼
    wsl.exe
      │
      ▼
commands.sh
      │
      ▼
Linux / WSL
```

---

# 📌 Status

**Personal DevOps utility / automation tool**

Created to simplify a specific remote Windows Server → WSL workflow and to keep the solution available as a reusable tool.

The implementation can be extended as additional remote WSL automation scenarios appear.
