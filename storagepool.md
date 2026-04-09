---  
title: "Network Based Storage Pools"  
id: "network-based-storage-pools"  
author: "Toby Knudsen"  
date: "2026-04-02"  
version: "1.3"  
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
## Background Objectives  
Network-based storage pools allow multiple systems to access shared storage over a network instead of relying on local disks. This is commonly used in enterprise environments for centralizing data, improving scalability, and simplifying backups. In this lab, you will connect to a shared storage resource between VMs and verify that data can be accessed across the network.  
  
## Step 1: Verify Network Connectivity  
Before accessing shared storage, confirm that your VMs can communicate.  
```bash
Run:  
ping -c 4 <target_vm_ip>  
```
Did the ping work? (Yes/No)  
  
### Reflection Question  
- Why is network connectivity required before accessing shared storage?  
  
## Step 2: Identify Available Network Storage  
Check if a shared storage resource is available.  
```bash
Run:  
showmount -e <target_vm_ip>  
```
Do you see any shared directories? (Yes/No)  
  
### Reflection Question  
- What does the list of exported directories tell you about available storage?  
  
## Step 3: Create a Mount Point  
You need a directory to attach the network storage.  
```bash 
Run:  
sudo mkdir -p /mnt/shared_storage  
```
What directory did you create? /mnt/shared_storage  
  
### Reflection Question  
- Why do you need a mount point before accessing network storage?  
  
## Step 4: Mount the Network Storage  
Connect to the shared storage pool.  
```bash
Run:  
sudo mount -t nfs <target_vm_ip>:/shared /mnt/shared_storage  
```
Did the mount complete successfully? (Yes/No)  
  
### Reflection Question  
- What does mounting actually do in terms of system access?  
  
## Step 5: Verify Mounted Storage  
Confirm the storage is mounted correctly.  
```bash  
Run:  
df -h  
```  
Do you see the mounted share listed? (Yes/No)  
  
### Reflection Question  
- Why is it important to verify that the storage is mounted?  
  
## Step 6: Access Shared Files  
Navigate into the mounted directory.  
```bash
Run:  
cd /mnt/shared_storage  
ls  
```  
Do you see files in the shared storage? (Yes/No)  
  
### Reflection Question  
- What does seeing files here confirm about the network storage?  
  
## Step 7: Create a Test File  
Test writing to the shared storage.  
```bash
Run:  
touch testfile.txt  
ls
```
Did your file appear? (Yes/No)  
  
### Reflection Question  
- Why is testing write access important for shared storage?  
  
## Step 8: Verify from Another VM  
Switch to another VM and check if the file exists.  
```bash
Run:  
cd /mnt/shared_storage  
ls  
```
Do you see the same file? (Yes/No)  
  
### Reflection Question  
- What does this confirm about how storage pools work across systems?  
  
## Step 9: Unmount Storage  
Clean up by disconnecting the storage.  
```bash
Run:  
sudo umount /mnt/shared_storage  
```
Verify: 
```
df -h  
```
Is the mount removed? (Yes/No)  
  
### Reflection Question  
- Why is it important to properly unmount network storage?  
  
## Finished!  
  
## Assessment  
Assessment 1: 
```bash
Run:  
ping -c 4 <target_vm_ip>  
```
Assessment 2:  
Identify available shared directories  
  
Assessment 3:  
Mount the shared storage  
  
Assessment 4:  
Verify mount using:
```bash
df -h  
```
Assessment 5:  
```
Create and verify a test file  
```  
## FAQs  
What is network-based storage?  
It is storage that is accessed over a network instead of being physically attached to a single machine.  
  
Why use storage pools?  
They allow multiple systems to access shared data, making management and scaling easier.  
  
What is NFS?  
Network File System (NFS) is a protocol that allows file sharing between systems over a network.  
  
## Related Skills & Roles  
- Cybersecurity Analyst  
- Network Administrator  
- Systems Engineer  
- Cloud Engineer
