# README

Description:

It was discovered in an OpenShift Cluster deployed into AWS that the AWS NVME disk order changes after reboot in the Red Hat Enterprise Linux 7 operating system. This impacts docker's storage configuration negatively if you have multiple disks configured. This repo contains two basic playbooks that address the two core use cases.

# Docker storage setup

## Use Case 1: Pre Docker Storage Setup

If you are configuring docker storage for the first time:

ocp-aws-nvme-docker-preinstall.yml

## Use Case 2: Post Docker storage setup

If you have already configured docker storage, disks have changed order, and you need to fix dockers configuration in order to bring up the service:

ocp-aws-nvme-docker-preinstall-fix.yml

# Origin disk setup

 If you are using a separate disk for /var/lib/origin you can use this playbook to setup your disks in advance of installing

 Prior to running the playbook review the variables and set them appropriately. You may also want to limit the run if you have different disk sizes on different nodes.

 | Varibles   | Default   | Options   | Description   |
 |------------|-----------|-----------|---------------|
 | ocp_varliborigin_storage_size | 101 | Integer | Define the size of the disk that you want to use for origin storage. This must be unique or the wrong disk may be selected |
 | ocp_varliborigin_filesytem | xfs | xfs,ext4,ect | Define the filesystem to put on the volume |
 | ocp_lvm_enable | true | true, false | Set if you want to use LVM |
 | ocp_lvm_vg_name | vg-varliborigin | string | The name of the volume group |
 | ocp_lvm_lv_name | lv-varliborigin | string | The name of the logical volume |

 # Etcd disk setup

  If you are using a separate disk for /var/lib/etcd you can use this playbook to setup your disks in advance of installing

  Prior to running the playbook review the variables and set them appropriately. By default this playbook only runs against the group "masters"

  | Varibles   | Default   | Options   | Description   |
  |------------|-----------|-----------|---------------|
  | ocp_varlibetcd_storage_size | 101 | Integer | Define the size of the disk that you want to use for origin storage. This must be unique or the wrong disk may be selected |
  | ocp_varlibetcd_filesytem | xfs | xfs,ext4,ect | Define the filesystem to put on the volume |
  | ocp_lvm_enable | true | true, false | Set if you want to use LVM |
  | ocp_lvm_vg_name | vg-varliborigin | string | The name of the volume group |
  | ocp_lvm_lv_name | lv-varliborigin | string | The name of the logical volume |
