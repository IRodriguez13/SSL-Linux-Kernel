##  SharpCore Subsystem for Linux (SSL)

> A lightweight, cross-platform, developer-friendly Linux virtualization subsystem.  
> Runs Alpine-based kernels in seconds using QEMU and .NET as CLI env 

---

## 🚀 What is SSL?

**SharpCore Subsystem for Linux (SSL)** is a developer-first alternative to WSL2.  
It provides a fully virtualized, portable Linux subsystem — without relying on Windows internals or heavyweight tools like Docker Desktop.

Built with ❤️ in .NET, and powered by QEMU + Alpine Linux, SSL is:

- 🔓 **Open source**
- 🪶 **Lightweight**
- 🧩 **Cross-platform** (Linux, Windows, macOS)
- 🛠️ **Customizable kernel** (forkable, patchable)
- 🧠 **Educational** (step-by-step logs and mounting checks)

---

## 🧩 Key Features

| Feature                           | Status         | Description |
|----------------------------------|----------------|-------------|
| ✅ Folder Mounting (VirtFS 9p)    | Full           | Mount host folders into the VM using virtio-9p |
| ✅ Dynamic Port Forwarding        | Full           | Automatically finds a free host port for communication |
| ✅ Preflight Checks               | Full           | Validates image, paths, ports, zombie processes |
| ✅ Configurable Shared Folder     | Full           | Auto-assigns path depending on your OS |
| ✅ CLI-based VM Manager (C#)      | Full           | Launch, test, and interact with the VM via command line |
| ✅ Regional Keyboard Support      | Full           | Latin American layout pre-configured (settable) |
| ✅ Auto Shutdown Cleanup          | Full           | Ensures no zombie QEMU left behind |
| ⚠️ GUI Apps Support (X11)         | Partial        | X11-compatible apps supported via XQuartz / VcXsrv / Xorg |
| 🚧 Cross-platform Installer       | In progress    | Avalonia-powered GUI installer with environment detection |
| 🚧 SSL Kernel Fork (Alpine-based) | Planned        | Minimal, performant Linux kernel with community patches |

---

## 🔧 Architecture Overview

Host System (Windows / Linux / macOS)
  |
  |---> SharpCore CLI (dotnet tool)
  |       |---- PreflightCheck()   🔍
  |       |----- QemuBridgeConnection 🔌
  |
  |---------> QEMU VM (Alpine-based)
          |------------- /mnt/hostshare       📂
          |--------------- Port 5000            🌐
          |-------------- DISPLAY=:0.0         🖼️

---

## 🖼️ GUI Apps Support (Experimental)

To run GUI Linux apps from SSL:

### On Windows:
1. Install [VcXsrv](https://sourceforge.net/projects/vcxsrv/)
2. Set: `export DISPLAY=host.docker.internal:0.0`

### On macOS:
1. Install [XQuartz](https://www.xquartz.org/)
2. Set: `export DISPLAY=host.docker.internal:0.0`

### On Linux:
1. Make sure `Xorg` is running
2. Run `xhost +` before launching SSL

---

## 🧪 Kernel Features

SSL ships with an Alpine Linux-based kernel that includes:

- Virtio modules for 9p mounting
- QEMU guest agent (optional)
- Minimal userland (apk, bash, busybox)
- Shared folder mount script (`/etc/local.d/mount-shared.sh`)
- Healthcheck script (`/etc/local.d/hostshare-healthcheck.start`)
- GUI testing tools: `xauth`, `xterm`, `xclock`

---

## 🔐 Goals

- Give devs full control over their Linux environment
- Avoid vendor lock-in (no Hyper-V, no Docker Desktop)
- Offer a truly **portable** VM-based dev env with real Linux kernel
- Support community contributions via kernel patching and CLI plugins

---

## 📦 Project Structure

```bash
SharpCore/
├── ShpCore.CLI/              # .NET CLI tool to launch the VM
├── ShpCore.Kernel/           # VM subsystem logic (C# bridge)
├── alpine-sharpcore.qcow2    # The actual disk image
├── qemu-options-default.json # Default QEMU launch flags
├── README.md
```
---

# Launch the VM from CLI

- **make vm-start** For launching the VM with the custom settings on *qemu-options.json*
- **make vm-shutdown**: kill the vm process 
- **make vm-test**: Runs the health-check for the vm environment 
- **make test**: Runs the testing suite
- **make build**: Builds the CLI solution


---
## 🧠 Who is this for?
- Developers tired of bloated tools

- Power users who want full visibility

- Educators teaching Linux from the inside out

- Tinkerers building their own subsystems & Docker alternatives

---
## 📢 Contributing
### We welcome contributions — but with care.

If you **want to send patches, suggestions, or help evolve the SSL kernel**, CLI, or installer, please follow these guidelines:

- Follow our coding conventions (A CONTRIBUTING.md and style guide will be available soon.)

- Prefer feature branches (e.g., SSL-feature/SSL-gui-support)

- Use descriptive commits and submit PRs with context

- Do not push raw kernel patches without context or break compatibility

- Fork and experiment freely!

### 📩 You can reach the core maintainer directly at:
- <ivanrwcm25@gmail.com>

---
## 📖 Docs & Wiki  (Soon)
### We’ll document:

- Excluded kernel subsystems and rationale (to keep things minimal)

- How to build your own fork from scratch

- Debugging the virtual machine lifecycle

- System compatibility matrix

- All that will live in the SharpCore Wiki (soon).
---
## ⚖️ License
- This project is licensed under the GNU General Public License v2 (GPLv2) —
same as the upstream Linux kernel, to stay aligned with community-driven OSS philosophy.

- Please refer to LICENSE file for details.

