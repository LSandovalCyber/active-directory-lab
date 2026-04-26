# Ubuntu Network Configuration (Static IP Setup)

This document outlines the process of configuring a static IP address on the Ubuntu client within an isolated internal network in a VirtualBox lab environment.

## Objective

Configure a static IP address on the Ubuntu client machine within an isolated internal network to enable communication with other virtual machines in the lab.

---

## Initial State

* Ubuntu installed in VirtualBox
* Connected to an **Internal Network (intnet)**
* No DHCP server present
* No IP address assigned to `enp0s3`

---

## Steps Performed

### 1. Verified Network Interface

Command used:

```bash
ip a
```

Observed:

* `lo` (loopback interface)
* `enp0s3` present but **no IPv4 address assigned**

---

### 2. Attempted Netplan Configuration

Edited file:

```bash
/etc/netplan/01-netcfg.yaml
```

Configured:

* Disabled DHCP
* Assigned static IP `192.168.56.20/24`

Encountered issues:

* YAML indentation error
* Conflicting configuration file:

  * `/etc/netplan/01-network-manager-all.yaml`
* Netplan not applying configuration correctly

---

### 3. Identified Configuration Conflict

Found multiple netplan files:

```bash
ls /etc/netplan/
```

Conflict caused by:

* `NetworkManager` overriding static configuration

---

### 4. Resolved Conflict

Actions taken:

* Removed conflicting file:

```bash
sudo rm /etc/netplan/01-network-manager-all.yaml
```

* Corrected permissions:

```bash
sudo chmod 600 /etc/netplan/01-netcfg.yaml
```

---

### 5. Switched to NetworkManager Configuration

Due to netplan issues, configured network via GUI:

Steps:

* Opened Wired Settings
* Navigated to IPv4 tab
* Changed method from DHCP → Manual

Configured:

* IP Address: `192.168.56.20`
* Netmask: `255.255.255.0`
* Gateway: (left blank)

---

### 6. Verified Configuration

Command used:

```bash
ip a
```

Result:

* `enp0s3` successfully assigned:

```text
inet 192.168.56.20/24
```

---

## Key Takeaways

* Internal networks do not provide DHCP by default
* Netplan configurations can conflict when multiple files exist
* YAML formatting must be precise (indentation-sensitive)
* NetworkManager may override manual netplan settings
* Static IP configuration is critical for controlled lab environments
