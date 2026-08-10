# 🛠️ DevOps Tools

A personal collection of **DevOps tools, scripts, and practical utilities** built to solve recurring infrastructure and engineering tasks.

The repository brings together small, focused tools covering areas such as Linux, networking, performance profiling, remote infrastructure, and automation.

The goal is simple:

> **Build it once, make it useful, document it, and keep it handy.**

---

## 🔧 Tools

### 🐙 [Octopus — Linux Network Configurator](./linux-network-configurator/)

A utility for automating Linux network configuration in offline environments.

**Covers:**

* Network interfaces
* NAT
* DHCP
* DNS
* SSH
* `nftables`
* Offline package installation
* Bash automation

---

### 🔥 [FlameGraph — Linux Performance Profiling](./flamegraph/)

A practical workflow for collecting CPU profiling data with Linux `perf` and visualizing call stacks as interactive Flame Graphs.

**Covers:**

* Linux `perf`
* CPU profiling
* Call-stack collection
* Flame Graph generation
* Performance hotspot analysis

---

### 🖥️ [WSL Remote Automation](./wsl-remote-automation/)

A small utility for automating interaction with WSL running on a remote Windows Server through SSH.

**Covers:**

* SSH
* Windows Server
* PowerShell
* WSL
* Bash
* Cross-platform command execution
* Windows/Linux line-ending handling

---

## 🗂️ Areas

The collection may grow to include utilities for:

* 🐧 **Linux & System Administration**
* 🌐 **Networking**
* 🐳 **Docker & Containers**
* ☸️ **Kubernetes**
* 🏗️ **Infrastructure as Code**
* 🚀 **CI/CD**
* 📊 **Observability & Performance**
* 🗄️ **Databases**
* 📨 **Messaging & Kafka**
* 🔐 **Security**
* 🧰 **Troubleshooting**
* ⚙️ **Automation**

Not every area needs to have a tool yet. This list reflects the types of problems this toolbox is intended to cover.

---

## 💡 Philosophy

Not everything here is intended to replace a mature production tool.

Some utilities exist because:

* a task is repetitive;
* a command sequence is easy to forget;
* troubleshooting requires the same steps repeatedly;
* a small script is faster than setting up a larger tool;
* or building a small utility is a useful way to understand how something works.

The focus is on **practical, reusable solutions rather than complexity for its own sake**.

Each tool has its own documentation and usage instructions.

---

## 📌 Status

This repository is intentionally evolving.

New tools are added when a recurring DevOps or infrastructure problem is worth automating, documenting, or keeping readily available.

---

## ⚠️ Disclaimer

These tools are maintained primarily for **personal use, experimentation, and practical DevOps work**.

Review scripts and configuration changes before running them in production environments.
