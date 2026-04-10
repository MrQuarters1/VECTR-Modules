# Network Based Storage Pools 

## Background

Network-based storage allows multiple systems to access shared data over a network rather than storing everything locally on a single machine. This approach is commonly used in enterprise environments to centralize data, improve scalability, and simplify backup and recovery processes. Instead of each system maintaining its own storage, resources can be shared and managed more efficiently.

One common method of implementing this is through the Network File System (NFS), which enables systems to mount remote directories as if they were part of the local filesystem. In this lab, you will connect to a shared storage resource between virtual machines, verify that it is accessible, and confirm that data can be read and written across systems.
  
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
  
## Step 1: Verify Network Connectivity  
Before accessing shared storage, confirm that your VMs can communicate.  
```bash
Run:  
ping -c 4 <target_vm_ip>  
```
Did the ping work? (Yes/No)  
  
### Reflection Questions  
- Why is network connectivity required before accessing shared storage?
- What might be causing issues if the ping fails?
## Step 2: Identify Available Network Storage  
Check if a shared storage resource is available.  
```bash
Run:  
showmount -e <target_vm_ip>  
```
Do you see any shared directories? (Yes/No)  
  
### Reflection Questions 
- What does the list of exported directories tell you about available storage?
- Why is it important to know what resources are shared before mounting?
  
## Step 3: Create a Mount Point  
You need a directory to attach the network storage.  
```bash 
Run:  
sudo mkdir -p /mnt/shared_storage  
```
What directory did you create? /mnt/shared_storage  
  
### Reflection Questions  
- Why do you need a mount point before accessing network storage?
- What could happen if you mount to the wrong directory?
  
## Step 4: Mount the Network Storage  
Connect to the shared storage pool.  
```bash
Run:  
sudo mount -t nfs <target_vm_ip>:/shared /mnt/shared_storage  
```
Did the mount complete successfully? (Yes/No)  
  
### Reflection Questions  
- What does mounting actually do in terms of system access?
- Why is the correct path important when mounting storage?
  
## Step 5: Verify Mounted Storage  
Confirm the storage is mounted correctly.  
```bash  
Run:  
df -h  
```  
Do you see the mounted share listed? (Yes/No)  
  
### Reflection Questions  
- Why is it important to verify that the storage is mounted?
- What could go wrong if the mount appears but is not functioning properly?
  
## Step 6: Access Shared Files  
Navigate into the mounted directory.  
```bash
Run:  
cd /mnt/shared_storage  
ls  
```  
Do you see files in the shared storage? (Yes/No)  
  
### Reflection Questions  
- What does seeing files here confirm about the network storage?
- What might it mean if the directory appears empty?
  
## Step 7: Create a Test File  
Test writing to the shared storage.  
```bash
Run:  
touch testfile.txt  
ls
```
Did your file appear? (Yes/No)  
  
### Reflection Questions  
- Why is testing write access important for shared storage?
- What issues could prevent you from creating files?
  
## Step 8: Verify from Another VM  
Switch to another VM and check if the file exists.  
```bash
Run:  
cd /mnt/shared_storage  
ls  
```
Do you see the same file? (Yes/No)  
  
### Reflection Questions
- What does this confirm about how storage pools work across systems?
- Why is shared visibility important in real-world environments?
  
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
- What problems could occur if storage is not unmounted correctly?
  

