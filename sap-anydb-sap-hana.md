---

copyright:
  years: 2021
lastupdated: "2021-3-23"

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

# AnyDB - SAP HANA Database
{: #anydb-hana-db}

The SAP systems in a landscape have specific requirements for servers, operating systems, network setup, and supported storage.
{: shortdesc}

Deployment of SAP AnyDB on IBM Cloud is similar to deployments with infrastructure with on-premises data centers. Therefore, use the information that is provided from SAP and the RDBMS providers.

To assist your project's planning phase, more design considerations are provided for **SAP AnyDB - SAP HANA Database** with {{site.data.keyword.ibm_cloud_sap}}.

## SAP HANA Database Overview 
{: #anydb-hana-overview-SAP}

SAP HANA offers a robust set of capabilities, including database management, database administration, data security, multi-model processing, application development, and data virtualization.

The SAP HANA database  is  a hybrid  in-memory  database that  combines row-based, column-based, and object-based  database  technology.Itallows  online  transaction  processing  (OLTP)  and  online  analytical processing (OLAP) on one system, without the need for redundant data storage or aggregates.

It  is  optimized  to  exploit  the  processing  capabilities  of  multi-core  /  CPU  architectures.  With  this architecture, SAP applications can benefit from current bar down technologies.

The [SAP  HANA  database](http://tekslate.com/tutorials/sap-hana-tutorials-interview-questions/) is the heart of SAP’s in-memory  technology  offering,  helping  customers  to improve their operational efficiency, agility, and flexibility.

## Overview of SAP HANA databasefor SAP NW with IBM Cloud
{: #anydb-hana-overview}

Before you start deploying the SAP HANA database, ensure that:

 * Check all relevant SAP and SAP HANA database information and prerequisites (for example, SAP Notes); including versions and fix pack levels of MS SQL Server that are supported
 * All required packages are installed for the relevant OS that you are using for MSSQL

## Documentation of SAP HANA database
{: #anydb-hana-documentation}

SAP HANA hardware and software requirements are described in the SAP HANA Master Guide at: 

* [SAP HANA Hardware and Software Requirements](https://help.sap.com/viewer/eb3777d5495d46c5b2fa773206bbfb46/2.0.01/en-US/d3d1cf20bb5710149b57fd794c827a4e.html) 

SAP HANA support on SAP-certified Cloud IaaS: 

* [Certified and Supported SAP HANA Hardware – Ceritified IaaS Platforms](https://www.sap.com/dmc/exp/2014-09-02-hana-hardware/enEN/#/solutions?filters=iaas;ve:28) 

SAP HANA and SAP NetWeaver on UNIX/Linux: 

* [Installation of SAP Systems Based on the Application Server ABAP of SAP NetWeaver 7.3 EHP1 to 7.52 on UNIX: SAP HANA Database](https://help.sap.com/viewer/910828cec5d14d6685da380aec1dc4ae/CURRENT_VERSION/en-US/9420dabb130e4ae1996b3f39e202cc6e.html) 

* [Installation of SAP Systems Based on the Application Server Java of SAP NetWeaver 7.5 and SAP Solution Manager 7.2 SR2 Java on UNIX: SAP HANA Database](https://help.sap.com/viewer/3aa4caa3bd634a22bdc572d82d1311ec/CURRENT_VERSION/en-US/9420dabb130e4ae1996b3f39e202cc6e.html) 

* [Installation of SAP ABAP S/4HANA and BW/4HANA Systems on UNIX: SAP HANA 2.0 Database](https://help.sap.com/viewer/39c32e9783f6439e871410848f61544c/CURRENT_VERSION_SWPM20/en-US/1937febc57ad4d81a213fca9b3e031a5.html)

HANA and SAP NetWeaver on Windows: 

* [Installation of SAP Systems Based on the Application Server ABAP of SAP NetWeaver 7.3 EHP1 to 7.52 on Windows: SAP HANA Database](https://help.sap.com/viewer/2703bed525eb478c935bc312b3c3b0a6/CURRENT_VERSION/en-US/9420dabb130e4ae1996b3f39e202cc6e.html)

* [Installation of SAP Systems Based on the Application Server Java of SAP NetWeaver 7.5 and SAP Solution Manager 7.2 SR2 Java on Windows: SAP HANA Database] (https://help.sap.com/viewer/14ccd8beec6f4651905783bc469bce5d/CURRENT_VERSION/en-US/9420dabb130e4ae1996b3f39e202cc6e.html)

* [Installation of SAP ABAP S/4HANA and BW/4HANA Systems on Windows: SAP HANA 2.0 Database](https://help.sap.com/viewer/3741bfe0345f4892ae190ee7cfc53d4c/CURRENT_VERSION_SWPM20/en-US/1937febc57ad4d81a213fca9b3e031a5.html) 

## SAP on SAP HANA using Intel Bare Metal 
{: #anydb-hana-documentation-bm}

See [SAP Note 2414097 - SAP Applications on IBM Cloud: Supported DB/OS and IBM Cloud Bare Metal Server Types](https://launchpad.support.sap.com/#/notes/2414097) for supported SAP HANA database versions. 

A sample configuration is shown in: 

* [Quick Study Tutorial - SAP NetWeaver deployment to Bare Metal on Classic Infrastructure, using RHEL](https://cloud.ibm.com/docs/sap?topic=sap-quickstudy-bm-netweaver-rhel) 

* [Quick Study Tutorial - SAP NetWeaver deployment to Bare Metal on Classic Infrastructure, using Windows Server](https://cloud.ibm.com/docs/sap?topic=sap-quickstudy-bm-netweaver-wins) 

## SAP on SAP HANA using Intel Virtual Servers (Gen2) 
{: #anydb-hana-documentation-bm}

See [SAP Note 2927211 - SAP Applications on IBM Virtual Private Cloud: Supported DB/OS and IBM Gen 2 Virtual Server Instances](https://launchpad.support.sap.com/#/notes/2927211) for supported MSSQL database versions. 

A sample configuration is shown in: 

* [Quick Study Tutorial - SAP NetWeaver deployment to Intel Virtual Server (Gen2) on VPC Infrastructure, using RHEL](https://cloud.ibm.com/docs/sap?topic=sap-quickstudy-vs-gen2-netweaver-rhel) 

* [Quick Study Tutorial - SAP NetWeaver deployment to Intel Virtual Server (Gen2) on VPC Infrastructure that uses Windows Server](https://cloud.ibm.com/docs/sap?topic=sap-quickstudy-vs-gen2-netweaver-wins) 

