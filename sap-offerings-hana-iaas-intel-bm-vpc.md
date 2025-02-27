---

copyright:
  years: 2020, 2021, 2022
lastupdated: "2022-01-28"

keywords: SAP, {{site.data.keyword.cloud_notm}} SAP-Certified Infrastructure, {{site.data.keyword.ibm_cloud_sap}}, SAP Workloads

subcollection: sap

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:external: target="_blank" .external}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:note: .note}
{:tip: .tip}
{:important: .important}

# Bare metal servers certified profiles on VPC infrastructure for SAP HANA
{: #hana-iaas-offerings-profiles-intel-bm-vpc}

## Profiles list
{: #hana-iaas-intel-bm-vpc-list}

The following table gives you an overview of the SAP-certified profiles with bare metal servers for VPC:

| **Profile** | **vCPU** | **Memory (RAM GiB)** | **SAPS** | **SAP HANA\nProcessing Type** |
| --- | --- | --- | --- | --- |
| **Balanced** | | | | |
| bx2d-metal-96x384 | 96 | 384 | 123,630 | OLTP/OLAP |
| bx2d-metal-192x768 | 192 | 768 | 255,000 | OLTP/OLAP |
| **Compute optimized** | | | | |
| cx2d-metal-96x192 | 96 | 192 | 101,070| OLTP/OLAP |
| **Memory optimized** | | | | |
| mx2d-metal-96x768 | 96 | 768 | 126,830 | OLTP/OLAP |
{: caption="Table 1. {{site.data.keyword.cloud_notm}} Bare Metal Servers for VPC certified for SAP HANA" caption-side="bottom"}


For more information, see [SAP Note ####### - SAP Applications on IBM Cloud Virtual Private Cloud (VPC) Infrastructure environment](https://launchpad.support.sap.com/#/notes/#######){: external}. The vCPUs in the above list are CPU cores and their secondary threads. The term vCPU is kept for an easier comparison with their virtual counterparts.

For SAP HANA deployments using IBM Cloud Bare Metal Servers for VPC, only single-node deployments are supported. This means multi-node / scale-out is not currently supported.
{: important}


## Understanding Bare Metal Server profile names
{: #hana-iaas-intel-bm-vpc-names}

With IBM Cloud Bare Metal Servers for VPC, the profile families that are certified for SAP are: *Balanced*, *Memory Optimized*, and *Compute optimized*.
- *Balanced* family profiles, provide a good mix of performance and scalability for more common workloads.
- *Compute optimized* family profiles, provide more compute power, thus the have more cores with less memory
- *Memory optimized* family profiles are to the best advantage for memory intensive workloads, such as intensive database applications and in-memory analytics workloads, and are especially designed for SAP HANA workloads.

For more information, see [Bare metal server profiles](/docs/vpc?topic=vpc-bare-metal-servers-profile).

The first letter of the profile name indicates the profile family mentioned above:

| First letter | Characteristics of the related profile family |
| --- | --- |
| b | *Balanced* family, CPU to Memory 1:2 |
| c | *Compute Optimized*  family, CPU to Memory ratio 1:4 |
| m | *Memory Optimized* family, higher CPU to Memory ratio 1:8 |
{: caption="Table 2. {{site.data.keyword.cloud_notm}} Bare Metal Servers for VPC Profile Families" caption-side="top"}

<br/>
The Bare Metual Server profile names are contextual and sequential. See the following example:

| Profile name | Naming convention component | What it means |
| --- | --- | --- |
| mx2d-metal-96x768 | m | *Memory Optimized* family |
| | x | Intel x86_64 CPU Architecture |
| | 2 | The generation for the underlying hardware |
| | — | _spacer_ |
| | 96 | 96 vCPU |
| | x | _spacer_ |
| | 768 | 788 GiB RAM |
{: caption="Table 3. Profile naming for SAP HANA" caption-side="top"}


## Profiles available on Hourly Consumption Billing
{: #hana-iaas-intel-bm-vpc-hourly}

All {{site.data.keyword.cloud_notm}} Bare Metal Servers for VPC are available with Hourly Consumption Billing, which includes Suspend Discounts and Sustained Usage Discounts. With Suspend Discounts, storage charges occur only if the server is in Shutdown state. With Sustained Usage Discount, the more a server is used, the less the cost per hour.

## Storage specifications
{: #hana-iaas-intel-bm-vpc-storage-specs}

When the bare metal server profiles for SAP HANA are initially provisioned, the servers all have one pre-configured disk (sda) attached with the following basic layout:

| File system | Partition | Storage type | size |
| --- | --- | --- | --- |
| | `sda1` | Pre-configured BIOS volume | 1 MB |
| `/boot/efi` | `sda2` | Pre-configured boot volume | 100 MB |
| `/` | `sda3` | Pre-configured root volume | 9.9 GB |
{: caption="Table 4. Storage configuration of the default bare metal server deployment (boot volume)" caption-side="top"}


In addition to the above listed partitions, bare metal servers for VPC have 8 to 16 NVMEs – depending on their size – which need to be configured after the server deployment.

To fulfill the KPIs defined for SAP HANA, each profile needs different storage volumes which are listed in details in the following sections. **These are mandatory storage configurations, not sample storage configurations**, because they are the tested and certified storage layouts that comply to **SAP HANA Tailored Data Center Integration** (TDI) Phase 5. It's highly recommended to stick to these given specifications.

Customers who want to choose different layouts are advised to follow the [SAP HANA TDI Overview](https://www.sap.com/documents/2017/09/e6519450-d47c-0010-82c7-eda71af511fa.html){: external} and [SAP HANA TDI FAQ](https://www.sap.com/documents/2016/05/e8705aae-717c-0010-82c7-eda71af511fa.html){: external} when configuring different layouts. Then they must run SAP's performance measurement tool HCMT - see [SAP Note 2493172 - SAP HANA Hardware and Cloud Measurement Tools](https://launchpad.support.sap.com/#/notes/2493172){: external} and follow the instructions of the [HCMT guide](https://help.sap.com/viewer/product/HANA_HW_CLOUD_TOOLS/latest/en-US){: external}. 
{: important}

File shares are NOT to be used for SAP HANA installations, however they can be deployed and mounted in arbitrary ways to provide additions storage, e.g. for backups, as needed.
{: note}

[SAP's recommended file system layout](https://help.sap.com/viewer/2c1988d620e04368aa4103bf26f17727/2.0.latest/en-US/4c24d332a37b4a3caad3e634f9900a45.html){: external} must be available for SAP HANA deployment. 

### Bare metal servers for VPC - Storage Layouts
{: #hana-iaas-intel-bm-vpc-mx2-profiles}

The following table shows the required physical volumes, related volume groups, logical volumes, and their characteristics:

| Profile | File\nsystem | Logical\nVolume | LV Size\n(GB) | Volume Group | Physical\nVolume | PV Size\n(TB) |
| --- | --- | --- | --- | --- | --- | --- |
| `cx2d-metal-96x192`  | `/hana/shared` | `hana_shared_lv` | 192 | `vg0` | `nvme0n1-`\n`nvme3n1-` | 11.6 |
| | `/hana/data` | `hana_data_lv` | min. 576 | `vg1` | `nvme4n1-`\n`nvme7n1-` | 11.6 |
| | `/hana/log` |  | 192 | `vg0` | | | 
| --- | --- | --- | --- | --- | --- | --- |
| `bx2d-metal-96x384`  | `/hana/shared` | `hana_shared_lv` | 384 | `vg0` | `nvme0n1-`\n`nvme3n1-` | 11.6 |
| | `/hana/data` | `hana_data_lv` | min. 1152 | `vg1` | `nvme4n1-`\n`nvme7n1-` | 11.6 |
| | `/hana/log` |  | 384 | `vg0` | | | 
| `bx2d-metal-192x768`  | `/hana/shared` | `hana_shared_lv` | 768 | `vg0` | `nvme0n1-`\n`nvme3n1-` | 11.6 |
| | `/hana/data` | `hana_data_lv` | min. 2304 | `vg1` | `nvme4n1-`\n`nvme7n1-` | 11.6 |
| | `/hana/log` |  | 512 | `vg0` | | | 
| --- | --- | --- | --- | --- | --- | --- |
| `mx2d-metal-96x768`  | `/hana/shared` | `hana_shared_lv` | 768 | `vg0` | `nvme0n1-`\n`nvme3n1-` | 11.6 |
| | `/hana/data` | `hana_data_lv` | min. 2304 | `vg1` | `nvme4n1-`\n`nvme7n1-` | 11.6 |
| | `/hana/log` |  | 512 | `vg0` | | | 
{: caption="Table 5. Storage layout for Bare metal servers for VPC" caption-side="top"}

<br/>
<br/>
Note, that both volume groups vg0 and vg1 are not fully utilized. Remaining space can be used to extend the above sizes, which are only minimum sizes, or can be used for other purposes. However, I/O load should NOT be pointed at the remaining space, since that will impact SAP HANA’s performance.

In order to ensure a higher level of availability and failure resilience, RAID10 logical volumes are build on-top the under-laying NVMEs, based on Linux’s logical volume manager.

Below, you will see a step-by-step guide for setting up the volume groups, logical volumes and file systems. Size information differ and can be retrieved from the above table.

1. After logging in to the OS, first of all install the lvm2 package, if not installed already

    ```
    [root@mx2d-metal-96x768 ~]# yum install lvm2
    ```

2. The above applies to RHEL, on SLES use ‘zypper in’ instead. Now, create the volume groups.

    ```
    [root@mx2d-metal-96x768 ~]# vgcreate vg0 /dev/nvme0n1 /dev/nvme1n1 /dev/nvme2n1 /dev/nvme3n1
    [root@mx2d-metal-96x768 ~]# vgcreate vg1 /dev/nvme4n1 /dev/nvme5n1 /dev/nvme6n1 /dev/nvme7n1
    ```

3. After creating the volume groups, logical volumes need to be created on-top of those

    ```
    [root@mx2d-metal-96x768 ~]# lvcreate --type raid10 -i 2 -m 1 -L 768G -I 64 -n hana_shared_lv vg0
    ```

4. Note, `768G` needs to be adapted to the hana_shared volume size specific to your memory size in the table above. Sizes for hana_log can be found there, too, and will have to be adapted in the command below as well.

    ```
    [root@mx2d-metal-96x768 ~]# lvcreate --type raid10 -i 2 -m 1 -L 512G -I 64 -n hana_log_lv vg0
    ```

1. Finally, hana_data needs to be created; either the size information is adapted by the use of `-L` option according to the table above, or the entire volume group is utilized by `-l 100%FREE` as follows:

    ```
    [root@mx2d-metal-96x768 ~]# lvcreate --type raid10 -i 2 -m 1 -l 100%FREE -I 64 -n hana_data_lv vg1
    ```

2. File systems need to be created on the logical volumes, we use XFS here, and will mount by label. That is not a requirement and can be adapted according to your needs:

    ```
    [root@mx2d-metal-96x768 ~]# mkfs.xfs -L HANA_SHARED -K /dev/mapper/vg0-hana_shared_lv
    [root@mx2d-metal-96x768 ~]# mkfs.xfs -L HANA_LOG -K /dev/mapper/vg0-hana_log_lv
    [root@mx2d-metal-96x768 ~]# mkfs.xfs -L HANA_DATA -K /dev/mapper/vg1-hana_data_lv
    ```

3. By adding the following lines to /etc/fstab and creating the required directory paths with mkdir, you can now mount the file systems.

    ```
    LABEL=HANA_SHARED /hana/shared xfs defaults 0 0
    LABEL=HANA_LOG /hana/log xfs defaults,swalloc,inode64 0 0
    LABEL=HANA_DATA /hana/data xfs defaults,largeio,swalloc,inode64 0 0
    ```

1. Please, follow [SAP note 2777782](https://launchpad.support.sap.com/#/notes/2777782) for RHEL and [SAP note 2684254](https://launchpad.support.sap.com/#/notes/2684254) for SLES to adapt your OS configuration settings according to the requirements for SAP HANA.

