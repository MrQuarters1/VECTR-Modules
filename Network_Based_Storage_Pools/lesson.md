---
title: "Network Based Storage Pools"
id: "network-based-storage-pools"
author: "Toby Knudsen"
date: "2026-04-08"
version: "1.0"
---

## Learning Objectives
- Understand what network-based storage is and why it is used
- Identify how storage pools are accessed over a network
- Mount and interact with a network storage share
- Verify connectivity between VMs and shared storage

## Prerequisites
- none

## Lab Environment Setup
Kali Base + Target VM (same network)
```bash
RUN sudo apt-get update -y
RUN sudo apt-get install nfs-common -y
RUN sudo apt-get install net-tools -y
```
## Assessment
### Assessment 1:
- Verify connectivity using ping -c 4 <target_vm_ip>

### Assessment 2:
- Identify available shared directories using 
- showmount -e <target_vm_ip>
### Assessment 3:
- Create a mount point and mount the shared storage  
### Assessment 4:
- Verify the mount using df -h
### Assessment 5:
- Access the shared storage and confirm files are visible
### Assessment 6:
- Create and verify a test file in the shared storage
### Assessment 7:
- Verify file visibility from another VM
### Assessment 8:
- Unmount the storage and confirm it is removed
### FAQs

What is network-based storage?
- Network-based storage allows multiple systems to access shared data over a network instead of using local disks.

What is NFS?
- NFS (Network File System) is a protocol that allows files to be shared between systems across a network.

Why use storage pools?
- Storage pools centralize data, making it easier to manage, scale, and back up across multiple systems.

Why do you need to mount storage?
- Mounting connects the remote storage to your local filesystem so you can interact with it like a normal directory.

Why is verifying across multiple VMs important?
- It confirms that the storage is truly shared and accessible between different systems on the network.

### Related Skills & Roles
- Cybersecurity Analyst
- Network Administrator
- Systems Engineer
- Cloud Engineer
