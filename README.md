# IaCLab: Infrastructure as Code with Vagrant

Two guided labs for **Infrastructure for Big Data** (SETU). You rebuild the 3-node VirtualBox cluster from the manual labs as code with Vagrant, then add software to it and repair a broken Vagrantfile.

| Lab | Time | What you do | Sheet |
| --- | --- | --- | --- |
| A | ~55 min | Bring up a 2-node cluster, work the Vagrant lifecycle (halt, snapshot, provision, rebuild), add node03, change a setting in code | [Guided Lab A](docs/Guided_Lab_A_IaC_Vagrant.pdf) |
| B | ~55 min | Rebuild the cluster from your Lab A Vagrantfile, install Nginx on every node as code, find and fix four faults | [Guided Lab B](docs/Guided_Lab_B_IaC_Vagrant.pdf) |

## Folders

| Folder | Used in |
| --- | --- |
| `labA-cluster/` | Lab A: 2-node cluster you grow to 3 nodes |
| `labB-start/` | Lab B sections 1–2: the 3-node cluster from Lab A (use your own saved Vagrantfile if you have it) |
| `labB-broken/` | Lab B section 3: a Vagrantfile with four faults to find and fix |

## Requirements

- VirtualBox and Vagrant (a Vagrant release that supports your VirtualBox version)
- The `ubuntu/jammy64` box: `vagrant box add ubuntu/jammy64`
- About 3 GB of free RAM (1 GB per node)

## Quick start

```bash
git clone https://github.com/micksetu/IaCLab.git
cd IaCLab/labA-cluster
vagrant up
vagrant ssh node01 -c "ping -c 2 node02"
vagrant destroy -f
```

## Network

The Vagrantfiles create their own VirtualBox NAT Network, **VagrantNet** (10.20.20.0/24, DHCP off), on NIC2 of each VM. NIC1 stays as Vagrant's NAT for `vagrant ssh`. Your manual **BigDataNet** (10.10.10.0/24) and the VMs on it are not touched.

| Node | IP |
| --- | --- |
| node01 | 10.20.20.11 |
| node02 | 10.20.20.12 |
| node03 | 10.20.20.13 |

Inside each VM there is a `student` user with password `student` (lab use only).
