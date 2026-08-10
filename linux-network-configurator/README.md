# 🐙 Octopus — Linux Network Configuration Utility

A Bash-based utility for automating Linux network configuration in **offline environments**.

Octopus brings together a set of common network and system configuration tasks into a single executable workflow.

## ✨ Features

Octopus can automate configuration of:

* 🌐 Network interfaces
* 🔀 NAT
* 📡 DHCP
* 🌍 DNS
* 🔐 SSH
* 🧱 `nftables`
* 📦 Offline package installation
* 📋 System configuration reporting

The tool is designed to work without requiring an active Internet connection once all required packages are available on the installation media.

---

## 🎯 Purpose

Octopus was created as a practical Linux networking and system-automation utility.

The main goal is to make a repeatable sequence of configuration steps available through a single entry point instead of executing each operation manually.

It is also a hands-on project for working with:

* Linux networking
* Bash scripting
* `nftables`
* system services
* package management
* offline installation
* filesystem permissions
* system configuration
* automation workflows

> **Note:** Octopus is a personal utility and learning project. It is not intended to replace mature configuration-management or network-management solutions in production environments.

---

## 📦 Project Structure

```text
octopus/
├── autostart.sh
├── get-packages.sh
├── lib_apply.sh
├── lib_init.sh
├── lib_install.sh
├── lib_report.sh
├── nftables.template
├── need_fixes.txt
└── octopus_net_v2.iso
```

### Main components

| File                | Purpose                                    |
| ------------------- | ------------------------------------------ |
| `autostart.sh`      | Main entry point                           |
| `lib_init.sh`       | Initial environment setup                  |
| `lib_install.sh`    | Package installation and preparation       |
| `lib_apply.sh`      | Applies network configuration              |
| `lib_report.sh`     | Generates a system configuration report    |
| `get-packages.sh`   | Prepares required packages for offline use |
| `nftables.template` | Firewall/NAT configuration template        |
| `need_fixes.txt`    | Known issues and pending improvements      |

---

# 🚀 Quick Start

## Requirements

The tool is intended for a Linux environment with:

* Bash
* `sudo` / root privileges
* access to the required installation media
* compatible networking interfaces
* the packages required by the selected configuration

Because the tool modifies system networking and firewall configuration, **root privileges are required**.

---

## Option 1 — Run from ISO

Mount the installation media:

```bash
sudo mkdir -p /mnt/cdrom
sudo mount /dev/sr0 /mnt/cdrom
```

Run the main entry point:

```bash
sudo bash /mnt/cdrom/autostart.sh
```

---

## Option 2 — Run from a local directory

If the project has already been copied to the target machine:

```bash
cd octopus
sudo bash autostart.sh
```

The local-directory workflow is useful for development, testing, and modifying the scripts.

---

# ⚙️ Execution Flow

At a high level, Octopus follows this workflow:

```text
Installation Media / Local Directory
                │
                ▼
          autostart.sh
                │
                ▼
          Environment Setup
                │
                ▼
        Package Preparation
                │
                ▼
       Network Configuration
                │
        ┌───────┼────────┐
        ▼       ▼        ▼
       NAT     DHCP     DNS
                │
                ▼
         SSH / Firewall
                │
                ▼
        Configuration Report
```

The exact operations depend on the configuration and environment.

---

# 📋 Configuration Report

After execution, Octopus generates a system report:

```text
~/machine_report.txt
```

The report is intended to provide a quick overview of the resulting machine configuration and assist with troubleshooting.

---

# 🔒 Temporary Working Directory

During execution, Octopus uses a temporary working directory:

```text
/tmp/octopus_config
```

The scripts and required files may be copied there during execution to provide an isolated working environment.

Temporary files stored under `/tmp` are expected to be removed by the operating system according to the host's temporary-file cleanup policy.

---

# ⚠️ Important

Octopus modifies system-level configuration.

Before running it on a machine you care about:

1. Review the scripts.
2. Verify the target network interfaces.
3. Understand the firewall and NAT rules being applied.
4. Make sure you have a way to recover network access.
5. Test the configuration in a disposable or virtual machine first.

In particular, incorrect network or firewall configuration can make a remote machine inaccessible.

---

# 🧪 Development

The project is primarily implemented in Bash.

When modifying the scripts, test changes in an isolated Linux environment or virtual machine whenever possible.

Recommended development cycle:

```text
Change
  ↓
Run in isolated environment
  ↓
Verify network configuration
  ↓
Check firewall rules
  ↓
Generate report
  ↓
Document the result
```

---

# 🛠️ Known Limitations

This project is intentionally focused on a specific set of Linux networking and system-configuration tasks.

It should not be considered a general-purpose network management framework.

Known limitations and future improvements are tracked in:

```text
need_fixes.txt
```

---

# 📌 Status

**Personal utility / hands-on engineering project**

The project may evolve as new networking and Linux administration requirements are encountered.

---

## License

See the repository license for usage and distribution terms.
