# Type-1 Hypervisor - Proxmox VE

This folder contains the screenshots, procedure, and results for the **Type-1 Hypervisor (Proxmox VE)** part of the hypervisor performance experiment.

## Objective

To set up a virtual machine using **Proxmox VE**, a Type-1 hypervisor, and evaluate its CPU performance using the **Sysbench CPU benchmark**.

## Requirements

* A server or PC with Proxmox VE installed
* Web browser to access the Proxmox web interface
* Ubuntu ISO file
* Internet connection for installing Sysbench inside the VM

## Machine Specifications

| Component        | Configuration  |
| ---------------- | -------------- |
| Operating System | Ubuntu         |
| CPU              | 2 vCPU         |
| RAM              | 2 GB           |
| Disk             | 20 GB          |
| Network          | `vmbr0` Bridge |

## Procedure

1. Opened the Proxmox web interface at `https://<PROXMOX_SERVER_IP>:8006`.
2. Accepted the security warning caused by the self-signed Proxmox certificate.
3. Logged in using the provided credentials.
4. Created a new virtual machine with the following configuration:

   * **Name:** `CC-Experiment1-Type1`
   * **OS:** Ubuntu ISO
   * **ISO Storage:** `local`
   * **Disk:** 20 GB (`local-lvm`)
   * **CPU:** 1 socket, 2 cores (2 vCPU)
   * **Memory:** 2048 MiB (2 GB)
   * **Network:** Bridge `vmbr0`
5. Started the virtual machine and opened the Proxmox Console.
6. Installed Ubuntu and logged into the VM.
7. Checked the VM configuration and resource usage using:

   * `hostnamectl`
   * `lscpu`
   * `free -h`
   * `df -h`
   * `top`
8. Installed Sysbench inside the Ubuntu VM.
9. Ran the Sysbench CPU benchmark.
10. Monitored CPU, memory, network, and disk usage from the Proxmox VM Summary page.
11. Shut down the VM using `sudo poweroff`.

## Commands Used

### Install Sysbench

```bash
sudo apt update
sudo apt install sysbench -y
```

### Check Sysbench Version

```bash
sysbench --version
```

### Run CPU Benchmark

```bash
sysbench cpu --cpu-max-prime=20000 run
```

### Check System Information

```bash
hostnamectl
lscpu
free -h
df -h
top
```

### Shut Down VM

```bash
sudo poweroff
```

## Screenshots

The following screenshots are included in this folder:

| Screenshot        | Description                           |
| ----------------- | ------------------------------------- |
| `lspuT.jpg`       | `lscpu` output showing CPU details    |
| `free -h (2).jpg` | `free -h` output showing memory usage |
| `SysbenchT1.jpg`  | Sysbench CPU benchmark result         |

## Lab Done / Implementation

The Ubuntu virtual machine was successfully created and configured in **Proxmox VE** with 2 vCPUs, 2 GB RAM, 20 GB storage, and a bridged network connection.

The VM was successfully started, Ubuntu was installed, system information was verified, and the Sysbench CPU benchmark was executed.

## Result

The following result was obtained from the Sysbench CPU benchmark:

**Command:**

```bash
sysbench cpu --cpu-max-prime=20000 run
```

### CPU Performance

* **Events per Second:** 1453.98

### General Statistics

* **Total Time:** 10.0030 seconds
* **Total Number of Events:** 14548

### Latency

* **Minimum:** 0.57 ms
* **Average:** 0.69 ms
* **Maximum:** 1.24 ms
* **95th Percentile:** 0.74 ms

## Conclusion

The Proxmox VE Type-1 hypervisor successfully hosted the Ubuntu virtual machine and allowed the CPU benchmark to be performed using Sysbench. The VM achieved **1453.98 events per second** during the CPU test.

The experiment demonstrates the process of creating, configuring, monitoring, and benchmarking a virtual machine using **Proxmox VE**.

