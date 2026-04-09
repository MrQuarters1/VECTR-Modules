---
title: "Network Based Storage Pools (VECTR VM Lab)"
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

### Assessment 1:
```bash
Verify connectivity using ping -c 4 <target_vm_ip>
```
### Assessment 2:
Identify available shared directories using 
```bash
showmount -e <target_vm_ip>
```
### Assessment 3:
``` bash
Create a mount point and mount the shared storage
```
### Assessment 4:
``` bash
Verify the mount using df -h
```
### Assessment 5:
```bash
Access the shared storage and confirm files are visible
```
### Assessment 6:
```bash
Create and verify a test file in the shared storage
```
### Assessment 7:
```bash
Verify file visibility from another VM
```
### Assessment 8:
```bash
Unmount the storage and confirm it is removed
```