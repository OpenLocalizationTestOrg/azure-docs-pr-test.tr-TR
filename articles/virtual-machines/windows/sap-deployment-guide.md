---
title: "Sanal makine dağıtımı için Windows üzerinde SAP aaaAzure | Microsoft Docs"
description: "Nasıl toodeploy SAP öğrenin azure'da Windows sanal makinelerde yazılım."
services: virtual-machines-windows
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 22aaa98c-bb9f-472f-b546-0b294e033cda
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 11/08/2016
ms.author: sedusch
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 121e317afc6498a896959e58ebfbdcbef9432ef5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-sap-on-windows-vms-in-azure"></a>Windows sanal makineleri Azure üzerinde SAP dağıtma
[767598]:https://launchpad.support.sap.com/#/notes/767598
[773830]:https://launchpad.support.sap.com/#/notes/773830
[826037]:https://launchpad.support.sap.com/#/notes/826037
[965908]:https://launchpad.support.sap.com/#/notes/965908
[1031096]:https://launchpad.support.sap.com/#/notes/1031096
[1139904]:https://launchpad.support.sap.com/#/notes/1139904
[1173395]:https://launchpad.support.sap.com/#/notes/1173395
[1245200]:https://launchpad.support.sap.com/#/notes/1245200
[1409604]:https://launchpad.support.sap.com/#/notes/1409604
[1558958]:https://launchpad.support.sap.com/#/notes/1558958
[1585981]:https://launchpad.support.sap.com/#/notes/1585981
[1588316]:https://launchpad.support.sap.com/#/notes/1588316
[1590719]:https://launchpad.support.sap.com/#/notes/1590719
[1597355]:https://launchpad.support.sap.com/#/notes/1597355
[1605680]:https://launchpad.support.sap.com/#/notes/1605680
[1619720]:https://launchpad.support.sap.com/#/notes/1619720
[1619726]:https://launchpad.support.sap.com/#/notes/1619726
[1619967]:https://launchpad.support.sap.com/#/notes/1619967
[1750510]:https://launchpad.support.sap.com/#/notes/1750510
[1752266]:https://launchpad.support.sap.com/#/notes/1752266
[1757924]:https://launchpad.support.sap.com/#/notes/1757924
[1757928]:https://launchpad.support.sap.com/#/notes/1757928
[1758182]:https://launchpad.support.sap.com/#/notes/1758182
[1758496]:https://launchpad.support.sap.com/#/notes/1758496
[1772688]:https://launchpad.support.sap.com/#/notes/1772688
[1814258]:https://launchpad.support.sap.com/#/notes/1814258
[1882376]:https://launchpad.support.sap.com/#/notes/1882376
[1909114]:https://launchpad.support.sap.com/#/notes/1909114
[1922555]:https://launchpad.support.sap.com/#/notes/1922555
[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[1941500]:https://launchpad.support.sap.com/#/notes/1941500
[1956005]:https://launchpad.support.sap.com/#/notes/1956005
[1973241]:https://launchpad.support.sap.com/#/notes/1973241
[1984787]:https://launchpad.support.sap.com/#/notes/1984787
[1999351]:https://launchpad.support.sap.com/#/notes/1999351
[2002167]:https://launchpad.support.sap.com/#/notes/2002167
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2039619]:https://launchpad.support.sap.com/#/notes/2039619
[2121797]:https://launchpad.support.sap.com/#/notes/2121797
[2134316]:https://launchpad.support.sap.com/#/notes/2134316
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2191498]:https://launchpad.support.sap.com/#/notes/2191498
[2233094]:https://launchpad.support.sap.com/#/notes/2233094
[2243692]:https://launchpad.support.sap.com/#/notes/2243692
[2367194]:https://launchpad.support.sap.com/#/notes/2367194

[azure-cli]:../../cli-install-nodejs.md
[azure-portal]:https://portal.azure.com
[azure-ps]:/powershell/azureps-cmdlets-docs
[azure-quickstart-templates-github]:https://github.com/Azure/azure-quickstart-templates
[azure-script-ps]:https://go.microsoft.com/fwlink/p/?LinkID=395017
[azure-subscription-service-limits]:../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../azure-subscription-service-limits.md#subscription-limits

[dbms-guide]:sap-dbms-guide.md (Azure Virtual Machines DBMS deployment for SAP on Windows)
[dbms-guide-2.1]:sap-dbms-guide.md#c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f (Caching for VMs and VHDs)
[dbms-guide-2.2]:sap-dbms-guide.md#c8e566f9-21b7-4457-9f7f-126036971a91 (Software RAID)
[dbms-guide-2.3]:sap-dbms-guide.md#10b041ef-c177-498a-93ed-44b3441ab152 (Microsoft Azure Storage)
[dbms-guide-2]:sap-dbms-guide.md#65fa79d6-a85f-47ee-890b-22e794f51a64 (Structure of a RDBMS deployment)
[dbms-guide-3]:sap-dbms-guide.md#871dfc27-e509-4222-9370-ab1de77021c3 (High availability and disaster recovery with Azure VMs)
[dbms-guide-5.5.1]:sap-dbms-guide.md#0fef0e79-d3fe-4ae2-85af-73666a6f7268 (SQL Server 2012 SP1 CU4 and later)
[dbms-guide-5.5.2]:sap-dbms-guide.md#f9071eff-9d72-4f47-9da4-1852d782087b (SQL Server 2012 SP1 CU3 and earlier releases)
[dbms-guide-5.6]:sap-dbms-guide.md#1b353e38-21b3-4310-aeb6-a77e7c8e81c8 (Using a SQL Server image from hello Azure Marketplace)
[dbms-guide-5.8]:sap-dbms-guide.md#9053f720-6f3b-4483-904d-15dc54141e30 (General SQL Server for SAP on Azure summary)
[dbms-guide-5]:sap-dbms-guide.md#3264829e-075e-4d25-966e-a49dad878737 (Specifics tooSQL Server RDBMS)
[dbms-guide-8.4.1]:sap-dbms-guide.md#b48cfe3b-48e9-4f5b-a783-1d29155bd573 (Storage configuration)
[dbms-guide-8.4.2]:sap-dbms-guide.md#23c78d3b-ca5a-4e72-8a24-645d141a3f5d (Backup and restore)
[dbms-guide-8.4.3]:sap-dbms-guide.md#77cd2fbb-307e-4cbf-a65f-745553f72d2c (Performance considerations for backup and restore)
[dbms-guide-8.4.4]:sap-dbms-guide.md#f77c1436-9ad8-44fb-a331-8671342de818 (Other)
[dbms-guide-900-sap-cache-server-on-premises]:sap-dbms-guide.md#642f746c-e4d4-489d-bf63-73e80177a0a8

[dbms-guide-figure-100]:./media/virtual-machines-shared-sap-dbms-guide/100_storage_account_types.png
[dbms-guide-figure-200]:./media/virtual-machines-shared-sap-dbms-guide/200-ha-set-for-dbms-ha.png
[dbms-guide-figure-300]:./media/virtual-machines-shared-sap-dbms-guide/300-reference-config-iaas.png
[dbms-guide-figure-400]:./media/virtual-machines-shared-sap-dbms-guide/400-sql-2012-backup-to-blob-storage.png
[dbms-guide-figure-500]:./media/virtual-machines-shared-sap-dbms-guide/500-sql-2012-backup-to-blob-storage-different-containers.png
[dbms-guide-figure-600]:./media/virtual-machines-shared-sap-dbms-guide/600-iaas-maxdb.png
[dbms-guide-figure-700]:./media/virtual-machines-shared-sap-dbms-guide/700-livecach-prod.png
[dbms-guide-figure-800]:./media/virtual-machines-shared-sap-dbms-guide/800-azure-vm-sap-content-server.png
[dbms-guide-figure-900]:./media/virtual-machines-shared-sap-dbms-guide/900-sap-cache-server-on-premises.png

[deployment-guide]:sap-deployment-guide.md (Azure Virtual Machines deployment for SAP on Windows)
[deployment-guide-2.2]:#42ee2bdb-1efc-4ec7-ab31-fe4c22769b94 (SAP resources)
[deployment-guide-3.1.2]:#3688666f-281f-425b-a312-a77e7db2dfab (Deploying a VM by using a custom image)
[deployment-guide-3.2]:#db477013-9060-4602-9ad4-b0316f8bb281 (Scenario 1: Deploying a VM from hello Azure Marketplace for SAP)
[deployment-guide-3.3]:#54a1fc6d-24fd-4feb-9c57-ac588a55dff2 (Scenario 2: Deploying a VM with a custom image for SAP)
[deployment-guide-3.4]:#a9a60133-a763-4de8-8986-ac0fa33aa8c1 (Scenario 3: Moving a VM from on-premises using a non-generalized Azure VHD with SAP)
[deployment-guide-3]:#b3253ee3-d63b-4d74-a49b-185e76c4088e (Deployment scenarios of VMs for SAP on Microsoft Azure)
[deployment-guide-4.1]:#604bcec2-8b6e-48d2-a944-61b0f5dee2f7 (Deploying Azure PowerShell cmdlets)
[deployment-guide-4.2]:#7ccf6c3e-97ae-4a7a-9c75-e82c37beb18e (Download and import SAP-relevant PowerShell cmdlets)
[deployment-guide-4.3]:#31d9ecd6-b136-4c73-b61e-da4a29bbc9cc (Join a VM tooan on-premises domain - Windows only)
[deployment-guide-4.4.2]:#6889ff12-eaaf-4f3c-97e1-7c9edc7f7542 (Linux)
[deployment-guide-4.4]:#c7cbb0dc-52a4-49db-8e03-83e7edc2927d (Download, install, and enable hello Azure VM Agent)
[deployment-guide-4.5.1]:#987cf279-d713-4b4c-8143-6b11589bb9d4 (Azure PowerShell)
[deployment-guide-4.5.2]:#408f3779-f422-4413-82f8-c57a23b4fc2f (Azure CLI)
[deployment-guide-4.5]:#d98edcd3-f2a1-49f7-b26a-07448ceb60ca (Configure hello Azure Enhanced Monitoring Extension for SAP)
[deployment-guide-5.1]:#bb61ce92-8c5c-461f-8c53-39f5e5ed91f2 (Readiness check for Azure Enhanced Monitoring for SAP)
[deployment-guide-5.2]:#e2d592ff-b4ea-4a53-a91a-e5521edb6cd1 (Health check for hello Azure monitoring infrastructure)
[deployment-guide-5.3]:#fe25a7da-4e4e-4388-8907-8abc2d33cfd8 (Troubleshooting Azure monitoring for SAP)

[deployment-guide-configure-monitoring-scenario-1]:#ec323ac3-1de9-4c3a-b770-4ff701def65b (Configure monitoring)
[deployment-guide-configure-proxy]:#baccae00-6f79-4307-ade4-40292ce4e02d (Configure hello proxy)
[deployment-guide-figure-100]:./media/virtual-machines-shared-sap-deployment-guide/100-deploy-vm-image.png
[deployment-guide-figure-1000]:./media/virtual-machines-shared-sap-deployment-guide/1000-service-properties.png
[deployment-guide-figure-11]:#figure-11
[deployment-guide-figure-1100]:./media/virtual-machines-shared-sap-deployment-guide/1100-azperflib.png
[deployment-guide-figure-1200]:./media/virtual-machines-shared-sap-deployment-guide/1200-cmd-test-login.png
[deployment-guide-figure-1300]:./media/virtual-machines-shared-sap-deployment-guide/1300-cmd-test-executed.png
[deployment-guide-figure-14]:#figure-14
[deployment-guide-figure-1400]:./media/virtual-machines-shared-sap-deployment-guide/1400-azperflib-error-servicenotstarted.png
[deployment-guide-figure-300]:./media/virtual-machines-shared-sap-deployment-guide/300-deploy-private-image.png
[deployment-guide-figure-400]:./media/virtual-machines-shared-sap-deployment-guide/400-deploy-using-disk.png
[deployment-guide-figure-5]:#figure-5
[deployment-guide-figure-50]:./media/virtual-machines-shared-sap-deployment-guide/50-forced-tunneling-suse.png
[deployment-guide-figure-500]:./media/virtual-machines-shared-sap-deployment-guide/500-install-powershell.png
[deployment-guide-figure-6]:#figure-6
[deployment-guide-figure-600]:./media/virtual-machines-shared-sap-deployment-guide/600-powershell-version.png
[deployment-guide-figure-7]:#figure-7
[deployment-guide-figure-700]:./media/virtual-machines-shared-sap-deployment-guide/700-install-powershell-installed.png
[deployment-guide-figure-760]:./media/virtual-machines-shared-sap-deployment-guide/760-azure-cli-version.png
[deployment-guide-figure-900]:./media/virtual-machines-shared-sap-deployment-guide/900-cmd-update-executed.png
[deployment-guide-figure-azure-cli-installed]:#402488e5-f9bb-4b29-8063-1c5f52a892d0
[deployment-guide-figure-azure-cli-version]:#0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda
[deployment-guide-install-vm-agent-windows]:#b2db5c9a-a076-42c6-9835-16945868e866
[deployment-guide-troubleshooting-chapter]:#564adb4f-5c95-4041-9616-6635e83a810b (Checks and troubleshooting for setting up end-to-end monitoring)

[deploy-template-cli]:../../resource-group-template-deploy-cli.md
[deploy-template-portal]:../../resource-group-template-deploy-portal.md
[deploy-template-powershell]:../../resource-group-template-deploy.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:sap-get-started.md
[getting-started-dbms]:sap-get-started.md#1343ffe1-8021-4ce6-a08d-3a1553a4db82
[getting-started-deployment]:sap-get-started.md#6aadadd2-76b5-46d8-8713-e8d63630e955
[getting-started-planning]:sap-get-started.md#3da0389e-708b-4e82-b2a2-e92f132df89c

[getting-started-windows-classic]:classic/virtual-machines-windows-classic-sap-get-started.md
[getting-started-windows-classic-dbms]:classic/virtual-machines-windows-classic-sap-get-started.md#c5b77a14-f6b4-44e9-acab-4d28ff72a930
[getting-started-windows-classic-deployment]:classic/virtual-machines-windows-classic-sap-get-started.md#f84ea6ce-bbb4-41f7-9965-34d31b0098ea
[getting-started-windows-classic-dr]:classic/virtual-machines-windows-classic-sap-get-started.md#cff10b4a-01a5-4dc3-94b6-afb8e55757d3
[getting-started-windows-classic-ha-sios]:classic/virtual-machines-windows-classic-sap-get-started.md#4bb7512c-0fa0-4227-9853-4004281b1037
[getting-started-windows-classic-planning]:classic/virtual-machines-windows-classic-sap-get-started.md#f2a5e9d8-49e4-419e-9900-af783173481c

[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056

[install-extension-cli]:virtual-machines-windows-enable-aem.md

[Logo_Linux]:./media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:./media/virtual-machines-shared-sap-shared/Windows.png

[msdn-set-azurermvmaemextension]:https://msdn.microsoft.com/library/azure/mt670598.aspx

[planning-guide]:sap-planning-guide.md (Azure Virtual Machines planning and implementation for SAP on Windows)
[planning-guide-1.2]:sap-planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff (Resources)
[planning-guide-11]:sap-planning-guide.md#7cf991a1-badd-40a9-944e-7baae842a058 (High availability and disaster recovery for SAP NetWeaver running on Azure Virtual Machines)
[planning-guide-11.4.1]:sap-planning-guide.md#5d9d36f9-9058-435d-8367-5ad05f00de77 (High availability for SAP Application Servers)
[planning-guide-11.5]:sap-planning-guide.md#4e165b58-74ca-474f-a7f4-5e695a93204f (Using Autostart for SAP instances)
[planning-guide-2.1]:sap-planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803 (Cloud-only - Virtual Machine deployments in Azure without dependencies on hello on-premises customer network)
[planning-guide-2.2]:sap-planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10 (Cross-premises - Deployment of single or multiple SAP VMs in Azure fully integrated with hello on-premises network)
[planning-guide-3.1]:sap-planning-guide.md#be80d1b9-a463-4845-bd35-f4cebdb5424a (Azure regions)
[planning-guide-3.2.1]:sap-planning-guide.md#df49dc09-141b-4f34-a4a2-990913b30358 (Fault domains)
[planning-guide-3.2.2]:sap-planning-guide.md#fc1ac8b2-e54a-487c-8581-d3cc6625e560 (Upgrade domains)
[planning-guide-3.2.3]:sap-planning-guide.md#18810088-f9be-4c97-958a-27996255c665 (Azure availability sets)
[planning-guide-3.2]:sap-planning-guide.md#8d8ad4b8-6093-4b91-ac36-ea56d80dbf77 (Microsoft Azure virtual machines concept)
[planning-guide-3.3.2]:sap-planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92 (Azure Premium Storage)
[planning-guide-5.1.1]:sap-planning-guide.md#4d175f1b-7353-4137-9d2f-817683c26e53 (Moving a VM from on-premises tooAzure with a non-generalized disk)
[planning-guide-5.1.2]:sap-planning-guide.md#e18f7839-c0e2-4385-b1e6-4538453a285c (Deploying a VM with a customer specific image)
[planning-guide-5.2.1]:sap-planning-guide.md#1b287330-944b-495d-9ea7-94b83aff73ef (Preparation for moving a VM from on-premises tooAzure with a non-generalized disk)
[planning-guide-5.2.2]:sap-planning-guide.md#57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3 (Preparation for deploying a VM with a customer specific image for SAP)
[planning-guide-5.2]:sap-planning-guide.md#6ffb9f41-a292-40bf-9e70-8204448559e7 (Preparing VMs with SAP for Azure)
[planning-guide-5.3.1]:sap-planning-guide.md#6e835de8-40b1-4b71-9f18-d45b20959b79 (Difference between an Azure disk and an Azure image)
[planning-guide-5.3.2]:sap-planning-guide.md#a43e40e6-1acc-4633-9816-8f095d5a7b6a (Uploading a VHD from on-premises tooAzure)
[planning-guide-5.4.2]:sap-planning-guide.md#9789b076-2011-4afa-b2fe-b07a8aba58a1 (Copying disks between Azure Storage accounts)
[planning-guide-5.5.1]:sap-planning-guide.md#4efec401-91e0-40c0-8e64-f2dceadff646 (VM/VHD structure for SAP deployments)
[planning-guide-5.5.3]:sap-planning-guide.md#17e0d543-7e8c-4160-a7da-dd7117a1ad9d (Setting automount for attached disks)
[planning-guide-7.1]:sap-planning-guide.md#3e9c3690-da67-421a-bc3f-12c520d99a30 (Single VM with SAP NetWeaver demo/training scenario)
[planning-guide-7]:sap-planning-guide.md#96a77628-a05e-475d-9df3-fb82217e8f14 (Concepts of Cloud-Only deployment of SAP instances)
[planning-guide-9.1]:sap-planning-guide.md#6f0a47f3-a289-4090-a053-2521618a28c3 (Azure Monitoring Solution for SAP)
[planning-guide-azure-premium-storage]:sap-planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92 (Azure Premium Storage)

[planning-guide-figure-100]:./media/virtual-machines-shared-sap-planning-guide/100-single-vm-in-azure.png
[planning-guide-figure-1300]:./media/virtual-machines-shared-sap-planning-guide/1300-ref-config-iaas-for-sap.png
[planning-guide-figure-1400]:./media/virtual-machines-shared-sap-planning-guide/1400-attach-detach-disks.png
[planning-guide-figure-1600]:./media/virtual-machines-shared-sap-planning-guide/1600-firewall-port-rule.png
[planning-guide-figure-1700]:./media/virtual-machines-shared-sap-planning-guide/1700-single-vm-demo.png
[planning-guide-figure-1900]:./media/virtual-machines-shared-sap-planning-guide/1900-vm-set-vnet.png
[planning-guide-figure-200]:./media/virtual-machines-shared-sap-planning-guide/200-multiple-vms-in-azure.png
[planning-guide-figure-2100]:./media/virtual-machines-shared-sap-planning-guide/2100-s2s.png
[planning-guide-figure-2200]:./media/virtual-machines-shared-sap-planning-guide/2200-network-printing.png
[planning-guide-figure-2300]:./media/virtual-machines-shared-sap-planning-guide/2300-sapgui-stms.png
[planning-guide-figure-2400]:./media/virtual-machines-shared-sap-planning-guide/2400-vm-extension-overview.png
[planning-guide-figure-2500]:./media/virtual-machines-shared-sap-planning-guide/2500-vm-extension-details.png
[planning-guide-figure-2600]:./media/virtual-machines-shared-sap-planning-guide/2600-sap-router-connection.png
[planning-guide-figure-2700]:./media/virtual-machines-shared-sap-planning-guide/2700-exposed-sap-portal.png
[planning-guide-figure-2800]:./media/virtual-machines-shared-sap-planning-guide/2800-endpoint-config.png
[planning-guide-figure-2900]:./media/virtual-machines-shared-sap-planning-guide/2900-azure-ha-sap-ha.png
[planning-guide-figure-300]:./media/virtual-machines-shared-sap-planning-guide/300-vpn-s2s.png
[planning-guide-figure-3000]:./media/virtual-machines-shared-sap-planning-guide/3000-sap-ha-on-azure.png
[planning-guide-figure-3200]:./media/virtual-machines-shared-sap-planning-guide/3200-sap-ha-with-sql.png
[planning-guide-figure-400]:./media/virtual-machines-shared-sap-planning-guide/400-vm-services.png
[planning-guide-figure-600]:./media/virtual-machines-shared-sap-planning-guide/600-s2s-details.png
[planning-guide-figure-700]:./media/virtual-machines-shared-sap-planning-guide/700-decision-tree-deploy-to-azure.png
[planning-guide-figure-800]:./media/virtual-machines-shared-sap-planning-guide/800-portal-vm-overview.png
[planning-guide-microsoft-azure-networking]:sap-planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd (Microsoft Azure networking)
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:sap-planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f (Storage: Microsoft Azure Storage and data disks)

[powershell-install-configure]:/powershell/azureps-cmdlets-docs
[resource-group-authoring-templates]:../../resource-group-authoring-templates.md
[resource-group-overview]:../../azure-resource-manager/resource-group-overview.md
[resource-groups-networking]:../../virtual-network/resource-groups-networking.md
[sap-pam]:https://support.sap.com/pam (SAP Product Availability Matrix)
[sap-templates-2-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-2-tier-os-disk]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-disk%2Fazuredeploy.json
[sap-templates-2-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-image%2Fazuredeploy.json
[sap-templates-3-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-3-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-user-image%2Fazuredeploy.json
[storage-azure-cli]:../../storage/storage-azure-cli.md
[storage-azure-cli-copy-blobs]:../../storage/storage-azure-cli.md#copy-blobs
[storage-introduction]:../../storage/storage-introduction.md
[storage-powershell-guide-full-copy-vhd]:../../storage/storage-powershell-guide-full.md#how-to-copy-blobs-from-one-storage-container-to-another
[storage-premium-storage-preview-portal]:../../storage/storage-premium-storage.md
[storage-redundancy]:../../storage/storage-redundancy.md
[storage-scalability-targets]:../../storage/storage-scalability-targets.md
[storage-use-azcopy]:../../storage/storage-use-azcopy.md
[template-201-vm-from-specialized-vhd]:https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd
[templates-101-simple-windows-vm]:https://github.com/Azure/azure-quickstart-templates/tree/master/101-simple-windows-vm
[templates-101-vm-from-user-image]:https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image
[virtual-machines-linux-attach-disk-portal]:../linux/attach-disk-portal.md
[virtual-machines-windows-attach-disk-portal]:../virtual-machines-windows-attach-disk-portal.md
[virtual-machines-azure-resource-manager-architecture]:../../resource-manager-deployment-model.md
[virtual-machines-azurerm-versus-azuresm]:virtual-machines-windows-compare-deployment-models.md
[virtual-machines-windows-classic-configure-oracle-data-guard]:../virtual-machines-windows-classic-configure-oracle-data-guard.md
[virtual-machines-linux-cli-deploy-templates]:../linux/cli-deploy-templates.md (Deploy and manage virtual machines by using Azure Resource Manager templates and hello Azure CLI)
[virtual-machines-deploy-rmtemplates-powershell]:../virtual-machines-windows-ps-manage.md (Manage virtual machines using Azure Resource Manager and PowerShell)
[virtual-machines-linux-agent-user-guide]:../linux/agent-user-guide.md
[virtual-machines-linux-agent-user-guide-command-line-options]:../linux/agent-user-guide.md#command-line-options
[virtual-machines-linux-capture-image]:../linux/capture-image.md
[virtual-machines-linux-capture-image-capture]:../linux/capture-image.md#capture-the-vm
[virtual-machines-windows-capture-image]:../virtual-machines-windows-capture-image.md
[virtual-machines-windows-capture-image-capture]:../virtual-machines-windows-capture-image.md#capture-the-vm
[virtual-machines-linux-configure-lvm]:../linux/configure-lvm.md
[virtual-machines-linux-configure-raid]:../linux/configure-raid.md
[virtual-machines-linux-classic-create-upload-vhd-step-1]:../virtual-machines-linux-classic-create-upload-vhd.md#step-1-prepare-the-image-to-be-uploaded
[virtual-machines-linux-create-upload-vhd-suse]:../linux/suse-create-upload-vhd.md
[virtual-machines-linux-redhat-create-upload-vhd]:../linux/redhat-create-upload-vhd.md
[virtual-machines-linux-how-to-attach-disk]:../linux/add-disk.md
[virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]:../linux/add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk
[virtual-machines-linux-tutorial]:../linux/quick-create-cli.md
[virtual-machines-linux-update-agent]:../linux/update-agent.md
[virtual-machines-manage-availability]:../virtual-machines-windows-manage-availability.md
[virtual-machines-ps-create-preconfigure-windows-resource-manager-vms]:../virtual-machines-windows-ps-create.md
[virtual-machines-sizes]:sizes.md
[virtual-machines-windows-classic-ps-sql-alwayson-availability-groups]:classic/ps-sql-alwayson-availability-groups.md
[virtual-machines-windows-classic-ps-sql-int-listener]:classic/ps-sql-int-listener.md
[virtual-machines-sql-server-high-availability-and-disaster-recovery-solutions]:./sql/virtual-machines-windows-sql-high-availability-dr.md
[virtual-machines-sql-server-infrastructure-services]:./sql/virtual-machines-windows-sql-server-iaas-overview.md
[virtual-machines-sql-server-performance-best-practices]:./sql/virtual-machines-windows-sql-performance.md
[virtual-machines-upload-image-windows-resource-manager]:upload-image.md
[virtual-machines-windows-tutorial]:../virtual-machines-windows-hero-tutorial.md
[virtual-machines-windows-create-vm-specialized]:../virtual-machines-windows-create-vm-specialized.md
[virtual-machines-workload-template-sql-alwayson]:https://azure.microsoft.com/documentation/templates/sql-server-2014-alwayson-dsc/
[virtual-network-deploy-multinic-arm-cli]:../../virtual-network/virtual-network-deploy-multinic-arm-cli.md
[virtual-network-deploy-multinic-arm-ps]:../../virtual-network/virtual-network-deploy-multinic-arm-ps.md
[virtual-network-deploy-multinic-arm-template]:../../virtual-network/virtual-network-deploy-multinic-arm-template.md
[virtual-networks-configure-vnet-to-vnet-connection]:../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md
[virtual-networks-create-vnet-arm-pportal]:../../virtual-network/virtual-networks-create-vnet-arm-pportal.md
[virtual-networks-manage-dns-in-vnet]:../../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md
[virtual-networks-multiple-nics]:../../virtual-network/virtual-networks-multiple-nics.md
[virtual-networks-nsg]:../../virtual-network/virtual-networks-nsg.md
[virtual-networks-reserved-private-ip]:../../virtual-network/virtual-networks-static-private-ip-arm-ps.md
[virtual-networks-static-private-ip-arm-pportal]:../../virtual-network/virtual-networks-static-private-ip-arm-pportal.md
[virtual-networks-udr-overview]:../../virtual-network/virtual-networks-udr-overview.md
[vpn-gateway-about-vpn-devices]:../../vpn-gateway/vpn-gateway-about-vpn-devices.md
[vpn-gateway-create-site-to-site-rm-powershell]:../../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md
[vpn-gateway-cross-premises-options]:../../vpn-gateway/vpn-gateway-plan-design.md
[vpn-gateway-site-to-site-create]:../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md
[vpn-gateway-vpn-faq]:../../vpn-gateway/vpn-gateway-vpn-faq.md
[xplat-cli]:../../cli-install-nodejs.md
[xplat-cli-azure-resource-manager]:../../xplat-cli-azure-resource-manager.md

Azure sanal makinelerin olası en kısa süre içinde ve uzun tedarik döngüleri olmadan işlem ve depolama kaynaklarını gereken kuruluşlar için hello çözümü şeklindedir. Azure'da Azure sanal makineleri toodeploy Klasik uygulamalar, SAP NetWeaver tabanlı uygulamalar gibi kullanabilirsiniz. Bir uygulamanın güvenilirlik ve kullanılabilirlik ek şirket içi kaynaklar olmadan genişletir. Azure sanal makineleri şirket içi bağlantılar, Azure sanal makineler, kuruluşunuzun şirket içi etki alanları, özel Bulutlar ve SAP sistem yatay tümleştirebilir şekilde destekler.

Bu makalede, azure'da Windows sanal makineler (VM'ler) üzerinde hello adımları toodeploy SAP uygulamalar kapsar. Bu makalede hello bilgileri derlemeler [Azure sanal makineleri planlama ve uygulama için Windows üzerinde SAP][planning-guide]. Aynı zamanda, SAP yükleme belgelerini ve yükleme ve SAP yazılım dağıtma hello birincil kaynaklardır SAP Notlar tamamlar.

## <a name="prerequisites"></a>Ön koşullar
SAP yazılım dağıtımı için Azure sanal makinesi ayarlanıyor birden çok adımlar ve kaynaklar içerir. Başlamadan önce azure'da Windows sanal makinelerde SAP yazılımını yüklemek için hello önkoşulları karşıladığından emin olun.

### <a name="local-computer"></a>Yerel bilgisayar
Windows veya Linux sanal makineleri toomanage, PowerShell Betiği ve hello Azure portalını kullanabilirsiniz. Her iki Araçlar, Windows 7 veya sonraki bir Windows sürümü çalıştıran yerel bir bilgisayar gerekir. Linux sanal makineleri ve bu görev için toouse Linux bilgisayarı istiyorsanız yalnızca toomanage istiyorsanız Azure CLI kullanabilirsiniz.

### <a name="internet-connection"></a>Internet bağlantısı
toodownload ve çalışma hello araçları ve SAP yazılım dağıtımı için gerekli olan komut dosyaları, olmalısınız toohello Internet bağlı. Merhaba hello Gelişmiş izleme uzantısı SAP için Azure çalışan Azure VM Internet erişimi toohello da gerekir. Bölümünde açıklandığı gibi Hello Azure VM bir Azure sanal ağı veya şirket içi etki alanının parçasıysa, hello ilgili proxy ayarlarının belirlendiğini emin olun [hello proxy yapılandırma][deployment-guide-configure-proxy].

### <a name="microsoft-azure-subscription"></a>Microsoft Azure aboneliği
Etkin bir Azure hesabı gerekir.

### <a name="topology-and-networking"></a>Topoloji ve ağ iletişimi
Toodefine hello topoloji ve hello Azure SAP dağıtımının mimarisini gerekir:

* Azure depolama hesapları toobe kullanılan
* Toodeploy hello SAP sistem istediğiniz sanal ağ
* Kaynak grubu toowhich toodeploy hello SAP sistem istiyor
* Toodeploy hello SAP sistem istediğiniz azure bölgesi
* SAP yapılandırma (iki katmanlı veya üç katmanlı)
* VM boyutları ve ek sanal sabit diskleri (VHD) toobe hello sayısını toohello VM'ler takılı
* SAP düzeltme ve aktarım sistem (CTS) yapılandırma

Oluşturun ve hello SAP yazılım dağıtım işlemi başlamadan önce Azure depolama hesapları veya Azure sanal ağını yapılandırın. Hakkında bilgi için toocreate ve bu kaynakları yapılandırmak için bkz: [Azure sanal makineleri planlama ve uygulama için Windows üzerinde SAP][planning-guide].

### <a name="sap-sizing"></a>SAP boyutlandırma
SAP boyutlandırma için bilgisinden hello bildirin:

* Merhaba SAP hızlı Boyutlandırıcı aracı ve hello SAP uygulama performans standart (SAP) numarasını kullanarak SAP iş yükü, örneğin, öngörülen
* Merhaba SAP sisteminin gerekli CPU ve bellek kaynak tüketimi
* Saniye başına gerekli giriş/çıkış (g/ç) işlemleri
* Azure VM'ler arasında nihai iletişimin ağ bant genişliği gerekli
* Şirket içi varlıklar ve hello Azure dağıtılan SAP sistemi arasındaki gerekli ağ bant genişliği

### <a name="resource-groups"></a>Kaynak grupları
Azure Kaynak Yöneticisi'nde, kaynak grupları toomanage tüm hello uygulama kaynakları Azure aboneliğinizde kullanabilirsiniz. Daha fazla bilgi için bkz: [Azure Resource Manager'a genel bakış][resource-group-overview].

## <a name="resources"></a>Kaynaklar

### <a name="42ee2bdb-1efc-4ec7-ab31-fe4c22769b94"></a>SAP kaynakları
SAP yazılım dağıtımınızı ayarlarken, SAP kaynakları aşağıdaki hello gerekir:

* SAP Not [1928533], sahip olduğu:
  * SAP yazılım hello dağıtımı için desteklenen Azure VM boyutlarını listesi
  * Azure VM boyutlarını önemli kapasite bilgilerini
  * Desteklenen bir SAP yazılım ve işletim sistemi (OS) ve veritabanı birleşimler
  * Windows ve Microsoft Azure Linux için gerekli SAP çekirdek sürümü

* SAP Not [2015553] azure'da SAP desteklenen SAP yazılım dağıtımları için önkoşulları listeler.
* SAP Not [2178632] ayrıntılı Azure SAP için bildirilen tüm izleme ölçümleri hakkında bilgi sağlanmıştır.
* SAP Not [1409604] hello SAP konak Aracısı Windows Azure için gereken sürümü vardır.
* SAP Not [2191498] hello Azure Linux için SAP konak Aracısı sürümünü istedi.
* SAP Not [2243692] Linux Azure üzerinde SAP lisanslama hakkında bilgi vardır.
* SAP Not [1984787] SUSE Linux Enterprise Server 12 hakkında genel bilgi yer almaktadır.
* SAP Not [2002167] Red Hat Enterprise Linux ilgili genel bilgilerin 7.x.
* SAP Not [1999351] hello Azure Gelişmiş izleme uzantısı SAP için ek sorun giderme bilgileri içeriyor.
* [SAP topluluk WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) SAP notları Linux için gerekli tüm sahiptir.
* Parçası olan SAP özgü PowerShell cmdlet'leri [Azure PowerShell][azure-ps].
* Parçası olan SAP özgü Azure CLI komutları [Azure CLI][azure-cli].

[comment]: <> (SAP Not 1409604 SAP konak aracı için MSSedusch Yapılacaklar eklemek ARM düzeltme eki düzeyi)

### <a name="microsoft-resources"></a>Microsoft kaynakları
Bu Microsoft makaleler Azure SAP dağıtımlarda kapsar:

* [Azure sanal makineleri planlama ve uygulama Windows üzerinde SAP için][planning-guide]
* [Windows (Bu makalede) SAP için Azure sanal makineler dağıtımı][deployment-guide]
* [SAP Windows için Azure sanal makineleri DBMS dağıtımı][dbms-guide]
* [Azure portalı][azure-portal]

## <a name="b3253ee3-d63b-4d74-a49b-185e76c4088e"></a>Azure vm'lerinde SAP yazılım için dağıtım senaryoları
Sanal makineleri ve ilişkili diskler azure'da dağıtmak için birçok seçeneğiniz vardır. Vm'leriniz seçtiğiniz hello dağıtım türüne göre dağıtım için farklı adımlar tooprepare sürebilir dağıtım seçenekleri arasındaki önemli toounderstand hello farklar demektir.

### <a name="db477013-9060-4602-9ad4-b0316f8bb281"></a>Senaryo 1: hello SAP için Azure Marketi VM'den dağıtma
Microsoft tarafından sağlanan bir görüntüyü kullanabilir ya da üçüncü hello Azure Marketi toodeploy VM göre taraf. bazı standart bir işletim sistemi görüntüleri Windows Server ve farklı Linux dağıtımları Hello Market sunar. Ayrıca, veritabanı yönetimi içeren bir görüntü dağıtabilirsiniz sistemi (DBMS) SKU'ları, örneğin, Microsoft SQL Server. Görüntüleri DBMS SKU'ları ile kullanma hakkında daha fazla bilgi için bkz: [Linux üzerinde SAP için Azure sanal makineleri DBMS dağıtım][dbms-guide].

Merhaba aşağıdaki akış çizelgesi hello SAP özgü hello Azure Marketi VM'den dağıtma adımları sırasını göstermektedir:

![VM dağıtımı için bir VM hello Azure Market görüntüsünden kullanarak SAP sistemleri akış çizelgesi][deployment-guide-figure-100]

#### <a name="create-a-virtual-machine-by-using-hello-azure-portal"></a>Hello Azure portal kullanarak bir sanal makine oluşturma
Merhaba en kolay yolu toocreate hello Azure Marketi görüntüden yeni bir sanal makineyle hello Azure portal kullanmaktır.

1.  Çok Git<https://portal.azure.com/#create>.  Veya hello Azure portalı menüsünde, seçin **+ yeni**.
2.  Seçin **işlem**ve ardından işletim sistemi toodeploy istediğiniz hello türünü seçin. Örneğin, Windows Server 2012 R2, SUSE Linux Enterprise Server 12 (SLES 12) veya Red Hat Enterprise Linux 7.2 (RHEL 7.2). Merhaba varsayılan liste görünümü, tüm desteklenen işletim sistemlerini göstermez. Seçin **tümünü görmek** tam listesi için. SAP yazılım dağıtımı için desteklenen işletim sistemleri hakkında daha fazla bilgi için bkz. SAP Not [1928533].
3.  Merhaba sonraki sayfada, hüküm ve koşulları gözden geçirin.
4.  Merhaba, **dağıtım modeli seçin** kutusunda, seçin **Resource Manager**.
5.  **Oluştur**’u seçin.

Başlangıç Sihirbazı, gerekli hello parametreleri toocreate hello sanal makine boyunca size yol gösterir, ayrıca ağ arabirimleri ve depolama hesapları gibi kaynaklara tooall gerekli. Bu parametreler bazıları şunlardır:

1. **Temel kavramları**:
  * **Ad**: hello kaynağın (Merhaba sanal makine adı) hello adı.
 * **Kullanıcı adı ve parola** veya **SSH ortak anahtarını**: hello kullanıcı hello sağlama işlemi sırasında oluşturulan hello kullanıcı adını ve parolasını girin. Bir Linux sanal makine için toohello makinede toosign kullanmak hello genel güvenli Kabuk (SSH) anahtarını girebilirsiniz.
 * **Abonelik**: hello abonelik toouse tooprovision hello yeni sanal makine istediğinizi seçin.
 * **Kaynak grubu**: hello VM hello kaynak grubunun hello adı. Yeni kaynak grubu veya hello adını zaten bir kaynak grubu ya da hello adını girebilirsiniz.
 * **Konum**: Burada toodeploy hello yeni bir sanal makine. Tooconnect hello sanal makine tooyour şirket içi ağ istiyorsanız, Azure tooyour şirket içi ağ bağlanan sanal ağ hello hello konumu seçtiğinizden emin olun. Daha fazla bilgi için bkz: [Microsoft Azure ağ] [ planning-guide-microsoft-azure-networking] içinde [Azure sanal makineleri planlama ve uygulama Linux üzerinde SAP için] [ planning-guide].
2. **Boyutu**:

     Desteklenen VM türlerinin listesi için bkz. SAP Not [1928533]. Toouse Azure Premium Storage istiyorsanız hello doğru VM türü seçtiğinizden emin olun. Premium depolama tüm VM türleri desteklemez. Daha fazla bilgi için bkz: [Depolama: Microsoft Azure depolama ve veri diskleri] [ planning-guide-storage-microsoft-azure-storage-and-data-disks] ve [Azure Premium Storage] [ planning-guide-azure-premium-storage] içinde [ Azure sanal makineleri planlama ve uygulama Linux üzerinde SAP için][planning-guide].

3. **Ayarları**:
   * **Depolama hesabı**: mevcut bir depolama hesabını seçin veya yeni bir tane oluşturun. Tüm depolama türlerini, SAP uygulamaları çalıştırmak için çalışır. Depolama türleri hakkında daha fazla bilgi için bkz: [Microsoft Azure depolama] [ dbms-guide-2.3] içinde [Linux üzerinde SAP için Azure sanal makineleri DBMS dağıtım] [ dbms-guide].
   * **Sanal ağ** ve **alt**: bağlı tooyour şirket içi ağ select hello sanal ağ intranetinize ile toointegrate hello sanal makine.
   * **Genel IP adresi**: toouse istediğiniz veya parametreleri toocreate yeni bir ortak IP adresi girin hello genel IP adresi seçin. Bir ortak IP adresi tooaccess hello Internet sanal makineniz kullanabilirsiniz. Bir ağ güvenlik grubu toohelp güvenli erişim tooyour sanal makine de oluşturduğunuzdan emin olun.
   * **Ağ güvenlik grubu**: daha fazla bilgi için bkz: [kontrol ağ trafiği akışını ağ güvenlik gruplarıyla][virtual-networks-nsg].
   * **Kullanılabilirlik**: bir kullanılabilirlik kümesi seçin veya hello parametreleri toocreate yeni bir kullanılabilirlik girin ayarlayın. Daha fazla bilgi için bkz: [Azure kullanılabilirlik kümeleri][planning-guide-3.2.3].
   * **İzleme**: seçebileceğiniz **devre dışı** Tanılama izleme. Merhaba komutları tooenable hello Monitoring Azure Gelişmiş uzantısı ile çalıştırdığınızda otomatik olarak açıklandığı gibi etkinleştirilir [yapılandırma izleme][deployment-guide-configure-monitoring-scenario-1].

4. **Özet**:

  Seçimlerinizi gözden geçirin ve ardından **Tamam**.

Sanal makineniz seçtiğiniz hello kaynak grubunda dağıtılır.

#### <a name="create-a-virtual-machine-by-using-a-template"></a>Bir şablonu kullanarak bir sanal makine oluşturma
Hello yayımlanan hello SAP şablonlarından birini kullanarak bir sanal makine oluşturabilirsiniz [azure hızlı başlangıç şablonlarını GitHub deposunu][azure-quickstart-templates-github]. Ayrıca el ile bir sanal makine hello kullanarak oluşturabileceğiniz [Azure portal][virtual-machines-windows-tutorial], [PowerShell][virtual-machines-ps-create-preconfigure-windows-resource-manager-vms], veya [Azure CLI ][virtual-machines-linux-tutorial].

* [**İki katmanlı yapılandırma (yalnızca bir sanal makine) şablonu** (sap-2-katman-Market-görüntü)][sap-templates-2-tier-marketplace-image]

  toocreate yalnızca bir sanal makine kullanarak iki katmanlı sistem bu şablonu kullanın.
* [**Üç katmanlı yapılandırma (birden çok sanal makine) şablonu** (sap-3-katman-Market-görüntü)][sap-templates-3-tier-marketplace-image]

  toocreate kullanarak birden çok sanal makine, bir üç katmanlı sistem bu şablonu kullanın.

Hello Azure portalı, şu parametreler hello şablonunun hello girin:

1. **Temel kavramları**:
  * **Abonelik**: hello abonelik toouse toodeploy hello şablonu.
  * **Kaynak grubu**: hello kaynak grubu toouse toodeploy hello şablonu. Yeni bir kaynak grubu oluşturabilir veya varolan bir kaynak grubu hello abonelikte seçebilirsiniz.
  * **Konum**: Burada toodeploy hello şablonu. Varolan bir kaynak grubu seçtiyseniz, bu kaynak grubunun hello konumu kullanılır.

2. **Ayarları**:
  * **SAP sistem kimliği**: Merhaba SAP sistem kimliği (SID).
  * **İşletim sistemi türü**: Merhaba örneğin toodeploy, istediğiniz işletim sistemi, Windows Server 2012 R2, SUSE Linux Enterprise Server 12 (SLES 12) veya Red Hat Enterprise Linux 7.2 (RHEL 7.2).

    Merhaba varsayılan liste görünümü, tüm desteklenen işletim sistemlerini göstermez. Seçin **tümünü görmek** tam listesi için. SAP yazılım dağıtımı için desteklenen işletim sistemleri hakkında daha fazla bilgi için bkz. SAP Not [1928533].
  * **SAP sistem boyutu**: Merhaba hello SAP sistem boyutu.

    SAP hello yeni sistem Hello sayısını sağlar. Kaç tane SAP hello sistemi gerektirir emin değilseniz, SAP teknolojisi iş ortağı veya sistem Tümleştirici isteyin.
  * **Sistem kullanılabilirliğini** (yalnızca üç katmanlı şablon): Merhaba sistem kullanılabilirlik.

    Seçin **HA** yüksek kullanılabilirlik yüklemesi için uygun bir yapılandırma için. İki veritabanı sunucuları ve iki sunucu için ABAP SAP merkezi Hizmetleri (ASCS) oluşturulur.
  * **Depolama türü** (yalnızca iki katmanlı şablon): Merhaba depolama toouse türü.

    Daha büyük sistemler için yüksek oranda Azure Premium Storage kullanmanızı öneririz. Depolama türleri hakkında daha fazla bilgi için şu kaynaklara bakın:
      * [SAP DBMS örneği için Azure Premium SSD depolama kullanımı][2367194]
      * [Microsoft Azure depolama] [ dbms-guide-2.3] içinde [Linux üzerinde SAP için Azure sanal makineleri DBMS dağıtımı][dbms-guide]
      * [Premium Storage: Azure sanal makine iş yükleri için yüksek performanslı depolama][storage-premium-storage-preview-portal]
      * [Giriş tooMicrosoft Azure depolama][storage-introduction]
  * **Yönetici kullanıcı adı** ve **yönetici parolası**: bir kullanıcı adı ve parola.
    Yeni bir kullanıcı, toohello sanal makinede imzalamak için oluşturulur.
  * **Yeni veya var olan bir alt ağ**: yeni bir sanal ağ ve alt ağ oluşturulur veya mevcut bir alt kullanılan belirler. Bağlı tooyour şirket içi ağ bir sanal ağ zaten varsa, seçin **varolan**.
  * **Alt ağ kimliği**: hello kimliği hello alt hello sanal makinelerin bağlanması için. Sanal özel ağ (VPN) veya Azure ExpressRoute sanal ağ toouse tooconnect hello sanal makine tooyour şirket içi ağın Hello alt ağ seçin. Merhaba kimliği genellikle şu şekilde görünür: /subscriptions/&lt;abonelik kimliği > /resourceGroups/&lt;kaynak grubu adı > /providers/Microsoft.Network/virtualNetworks/&lt;sanal ağ adı > /subnets/&lt;alt ağ adı >

3. **Hüküm ve koşullar**:  
    Gözden geçirin ve hello yasal koşulları kabul edin.

4.  Seçin **satın alma**.

hello Azure Marketi görüntüden kullandığınızda hello Azure VM Aracısı varsayılan olarak dağıtılır.

#### <a name="configure-proxy-settings"></a>Proxy ayarlarını yapılandır
Şirket içi ağınıza nasıl yapılandırıldığına bağlı olarak, VM hello proxy yukarı tooset gerekebilir. VM bağlı tooyour şirket içi ağ VPN ya da ExpressRoute aracılığıyla ise, hello VM değil mümkün tooaccess hello Internet olması ve olmaz mümkün toodownload gerekli hello uzantıları veya izleme verilerini topla. Daha fazla bilgi için bkz: [hello proxy yapılandırma][deployment-guide-configure-proxy].

#### <a name="join-a-domain-windows-only"></a>(Yalnızca Windows) etki alanına Katıl
Azure dağıtımınıza bağlı tooan şirket içi Active Directory veya DNS bir Azure siteden siteye VPN bağlantısı veya ExpressRoute aracılığıyla örneğiyse (Bu adlı *şirketler arası* içinde [Azure sanal makineleri planlama ve Linux üzerinde SAP uygulamasını][planning-guide]), o hello VM bir şirket içi etki alanına katılma beklenir. Bu görev için konuları hakkında daha fazla bilgi için bkz: [VM tooan şirket içi etki alanına (yalnızca Windows) katılma][deployment-guide-4.3].

#### <a name="ec323ac3-1de9-4c3a-b770-4ff701def65b"></a>İzlemeyi Yapılandır
ortamınızı açıklandığı gibi hello Azure Monitoring uzantısı SAP için ayarlamak SAP desteklediğinden emin toobe [yapılandırma hello Azure Gelişmiş izleme uzantısı SAP][deployment-guide-4.5]. SAP izleme ve gerekli en düşük sürümlerinde SAP çekirdek ve SAP konak Aracısı, listelenen hello kaynakları Hello önkoşullarını denetlemek [SAP kaynakları][deployment-guide-2.2].

#### <a name="monitoring-check"></a>Onay izleme
İzleme çalışıp çalışmadığını, açıklandığı gibi denetleyin [denetler ve uçtan uca izleme ayarlamak için sorun giderme][deployment-guide-troubleshooting-chapter].

#### <a name="post-deployment-steps"></a>Dağıtım sonrası adımlar
Oluşturduktan sonra hello VM ve VM hello dağıtılır, hello VM tooinstall gerekli hello yazılım bileşenleri gerekir. Merhaba dağıtım/yazılım yükleme sırası nedeniyle bu tür bir VM dağıtımı, yüklü hello yazılım toobe zaten ya da Azure, başka bir VM üzerinde veya kullanılabilir bir disk olarak kullanılabilir olmalıdır. Veya hangi bağlantı toohello varlıklar (yükleme paylaşımları) şirket içi bir şirket içi senaryo kullanarak verilen göz önünde bulundurun.

Azure'da VM dağıttıktan sonra izleme hello aynı VM yazarken yönergeleri ve araçları tooinstall hello SAP yazılımı bir şirket içi ortamda gerekir. bir Azure VM tooinstall SAP yazılımı, hem SAP ve Microsoft karşıya yükleyin ve Azure VHD'lerde hello SAP yükleme medyası depolama öneririz ya da tüm hello sahip bir dosya sunucusu olarak çalışan bir Azure VM oluşturma SAP yükleme medyasını gereklidir.

[comment]: <> (MSSedusch neden toorecommend bir dosya yönetimi örneğin ihtiyacımız Yapılacaklar, dosya sunucusu veya VHD? Şirket içi çok farklı olan?)

### <a name="54a1fc6d-24fd-4feb-9c57-ac588a55dff2"></a>2. Senaryo: özel bir görüntü ile bir VM için SAP dağıtma
Bir işletim sistemi veya DBMS farklı sürümlerini farklı düzeltme eki gereksinimleri olduğundan, hello Azure Marketi Bul hello görüntüleri ihtiyaçlarınızı karşılamayabilir. Bunun yerine, daha sonra yeniden dağıtabilirsiniz kendi işletim sistemi/DBMS VM görüntüsünü kullanarak toocreate VM isteyebilirsiniz.
Windows için toocreate daha Linux için farklı adımlar toocreate özel bir görüntü kullanın.

- - -
> ![Windows][Logo_Windows] Windows
>
> tooprepare hello üzerinde birden çok sanal makineler, hello Windows ayarları (örneğin, Windows SID ve ana bilgisayar adı) soyutlanır genelleştirilmiş veya gereken toodeploy kullanabileceğiniz bir Windows görüntüsünü VM şirket içi. Kullanabileceğiniz [sysprep](https://msdn.microsoft.com/library/hh825084.aspx) toodo bu.
>
> ![Linux][Logo_Linux] Linux
>
> birden çok sanal makine toodeploy kullanabileceğiniz bir Linux görüntüsü tooprepare, bazı Linux ayarları olmalıdır soyutlanır veya üzerinde genelleştirilmiş hello şirket içi VM. Kullanabileceğiniz `waagent -deprovision` toodo bu. Daha fazla bilgi için bkz: [Azure üzerinde çalışan Linux sanal makine yakalama] [ virtual-machines-linux-capture-image] ve hello [Azure Linux Aracısı Kullanıcı Kılavuzu'na][virtual-machines-linux-agent-user-guide-command-line-options].
>
>

- - -
Hazırlama ve özel bir görüntü oluşturun ve toocreate kullanmak birden çok yeni VM. Bu açıklanan [Azure sanal makineleri planlama ve uygulama Linux üzerinde SAP için][planning-guide]. Veritabanınızı ayarlama SAP yazılım sağlama Yöneticisi tooinstall yeni bir SAP sistemi kullanarak ya da içerik (ekli toohello sanal makine bir VHD'den bir veritabanı yedeklemesini geri yükler) veya doğrudan bir veritabanı yedeği, Azure depolama biriminden geri, DBMS Bunu destekler. Daha fazla bilgi için bkz: [Linux üzerinde SAP için Azure sanal makineleri DBMS dağıtım][dbms-guide]. (Özellikle iki katmanlı sistemler için), şirket içi VM üzerinde bir SAP sistemi zaten yüklü değilse, hello SAP sistem ayarlarını hello Azure VM hello dağıtımdan sonra SAP yazılım sağlama tarafından desteklenen hello sistemi yeniden adlandırılamadı yordamı kullanarak uyarlayabilirsiniz Yöneticisi (SAP Not [1619720]). Aksi takdirde hello Azure VM dağıttıktan sonra hello SAP yazılım yükleyebilirsiniz.

Merhaba aşağıdaki akış çizelgesi hello SAP özgü özel bir görüntü VM'den dağıtma adımları sırasını göstermektedir:

![VM dağıtımı için bir VM görüntüsü özel Marketi'ndeki kullanarak SAP sistemleri akış çizelgesi][deployment-guide-figure-300]

#### <a name="create-hello-virtual-machine"></a>Merhaba sanal makine oluşturma
toocreate hello Azure portal, özel bir işletim sistemi görüntüsünü kullanarak bir dağıtım SAP şablonları aşağıdaki hello birini kullanın. Bu şablonlar hello yayımlanan [azure hızlı başlangıç şablonlarını GitHub deposunu][azure-quickstart-templates-github]. Ayrıca el ile bir sanal makine kullanarak oluşturabileceğiniz [PowerShell][virtual-machines-upload-image-windows-resource-manager].

* [**İki katmanlı yapılandırma (yalnızca bir sanal makine) şablonu** (sap-2-katman-kullanıcı-görüntü)][sap-templates-2-tier-user-image]

  toocreate yalnızca bir sanal makine kullanarak iki katmanlı sistem bu şablonu kullanın.
* [**Üç katmanlı yapılandırma (birden çok sanal makine) şablonu** (sap-3-katman-kullanıcı-görüntü)][sap-templates-3-tier-user-image]

  toocreate birden çok sanal makine ya da kendi işletim sistemi görüntüsü kullanarak üç katmanlı sistem bu şablonu kullanın.

Hello Azure portalı, şu parametreler hello şablonunun hello girin:

1. **Temel kavramları**:
  * **Abonelik**: hello abonelik toouse toodeploy hello şablonu.
  * **Kaynak grubu**: hello kaynak grubu toouse toodeploy hello şablonu. Yeni bir kaynak grubu oluşturun veya varolan bir kaynak grubu hello abonelikte seçin.
  * **Konum**: Burada toodeploy hello şablonu. Varolan bir kaynak grubu seçtiyseniz, bu kaynak grubunun hello konumu kullanılır.
2. **Ayarları**:
  * **SAP sistem kimliği**: Merhaba SAP sistem kimliği
  * **İşletim sistemi türü**: Merhaba toodeploy (Windows veya Linux) istediğiniz işletim sistemi türü.
  * **SAP sistem boyutu**: Merhaba hello SAP sistem boyutu.

    SAP hello yeni sistem Hello sayısını sağlar. Kaç tane SAP hello sistemi gerektirir emin değilseniz, SAP teknolojisi iş ortağı veya sistem Tümleştirici isteyin.
  * **Sistem kullanılabilirliğini** (yalnızca üç katmanlı şablon): Merhaba sistem kullanılabilirlik.

    Seçin **HA** yüksek kullanılabilirlik yüklemesi için uygun bir yapılandırma için. İki veritabanı sunucuları ve iki sunucu ASCS için oluşturulur.
  * **Depolama türü** (yalnızca iki katmanlı şablon): Merhaba depolama toouse türü.

    Daha büyük sistemler için yüksek oranda Azure Premium Storage kullanmanızı öneririz. Depolama türleri hakkında daha fazla bilgi için kaynakları aşağıdaki hello bakın:
      * [SAP DBMS örneği için Azure Premium SSD depolama kullanımı][2367194]
      * [Microsoft Azure depolama] [ dbms-guide-2.3] içinde [Linux üzerinde SAP için Azure sanal makineleri DBMS dağıtımı][dbms-guide]
      * [Premium Storage: Azure sanal makine iş yükleri için yüksek performanslı depolama][storage-premium-storage-preview-portal]
      * [Giriş tooMicrosoft Azure depolama][storage-introduction]
  * **Kullanıcı görüntüsü VHD URİ'si**: hello özel işletim sistemi görüntüsü VHD, örneğin, https:// URI'sini hello&lt;accountname >.blob.core.windows.net/vhds/userimage.vhd.
  * **Kullanıcı görüntü depolama hesabı**: hello hello özel işletim sistemi görüntüsünün depolandığı, örneğin, hello depolama hesabının adını &lt;accountname > https:// içinde&lt;accountname >.blob.core.windows.net/vhds/userimage.vhd.
  * **Yönetici kullanıcı adı** ve **yönetici parolası**: Merhaba kullanıcı adı ve parola.

    Yeni bir kullanıcı, toohello sanal makinede imzalamak için oluşturulur.
  * **Yeni veya var olan bir alt ağ**: yeni bir sanal ağ ve alt ağ oluşturulur veya mevcut bir alt kullanılan belirler. Bağlı tooyour şirket içi ağ bir sanal ağ zaten varsa, seçin **varolan**.
  * **Alt ağ kimliği**: hello kimliği hello alt toowhich hello sanal makinelerin bağlanması için. VPN ya da ExpressRoute sanal ağ toouse tooconnect hello sanal makine tooyour Şirket ağınızın Hello alt ağ seçin. Merhaba kimliği genellikle şu şekildedir:

    /Subscriptions/&lt;abonelik kimliği > /resourceGroups/&lt;kaynak grubu adı > /providers/Microsoft.Network/virtualNetworks/&lt;sanal ağ adı > /subnets/&lt;alt ağ adı >

3. **Hüküm ve koşullar**:  
    Gözden geçirin ve hello yasal koşulları kabul edin.

4.  Seçin **satın alma**.

#### <a name="install-hello-vm-agent-linux-only"></a>Merhaba VM Aracısı (yalnızca Linux) yükleyin
hello önceki bölümde açıklanan toouse hello şablonları Linux Aracısı hello kullanıcı görüntüsü veya başlangıç dağıtımı yüklü olması gereken hello başarısız olur. Karşıdan yükleyip hello VM Aracısı hello kullanıcı görüntüde açıklandığı gibi [indirme, yükleme ve hello Azure VM Aracısı etkinleştirme][deployment-guide-4.4]. Merhaba şablonları kullanmıyorsanız, daha sonra VM Aracısı hello da yükleyebilirsiniz.

#### <a name="join-a-domain-windows-only"></a>(Yalnızca Windows) etki alanına Katıl
Azure dağıtımınıza bağlı tooan şirket içi Active Directory veya DNS Azure siteden siteye VPN bağlantısı veya Azure ExpressRoute üzerinden örneğiyse (Bu adlı *şirketler arası* içinde [Azure sanal makineler Planlama ve uygulama Linux üzerinde SAP için][planning-guide]), o hello VM bir şirket içi etki alanına katılma beklenir. Bu adım için ilgili önemli noktalar hakkında daha fazla bilgi için bkz: [VM tooan şirket içi etki alanına (yalnızca Windows) katılma][deployment-guide-4.3].

#### <a name="configure-proxy-settings"></a>Proxy ayarlarını yapılandır
Şirket içi ağınıza nasıl yapılandırıldığına bağlı olarak, VM hello proxy yukarı tooset gerekebilir. VM bağlı tooyour şirket içi ağ VPN ya da ExpressRoute aracılığıyla ise, hello VM değil mümkün tooaccess hello Internet olması ve olmaz mümkün toodownload gerekli hello uzantıları veya izleme verilerini topla. Daha fazla bilgi için bkz: [hello proxy yapılandırma][deployment-guide-configure-proxy].

#### <a name="configure-monitoring"></a>İzlemeyi Yapılandır
ortamınızı açıklandığı gibi hello Azure Monitoring uzantısı SAP için ayarlamak SAP desteklediğinden emin toobe [yapılandırma hello Azure Gelişmiş izleme uzantısı SAP][deployment-guide-4.5]. SAP izleme ve gerekli en düşük sürümlerinde SAP çekirdek ve SAP konak Aracısı, listelenen hello kaynakları Hello önkoşullarını denetlemek [SAP kaynakları][deployment-guide-2.2].

#### <a name="monitoring-check"></a>Onay izleme
İzleme çalışıp çalışmadığını, açıklandığı gibi denetleyin [denetler ve uçtan uca izleme ayarlamak için sorun giderme][deployment-guide-troubleshooting-chapter].




### <a name="a9a60133-a763-4de8-8986-ac0fa33aa8c1"></a>Senaryo 3: şirket içi VM genelleştirilmiş Azure VHD SAP ile kullanarak taşıma
Bu senaryoda, bir şirket içi ortamına tooAzure belirli bir SAP sistemden toomove planlayın. Hello hello işletim sistemi, hello SAP ikili dosyaları, sahip VHD yükleyerek bunu ve sonunda DBMS ikili dosyalarının yanı sıra, hello VHD'ler hello verilerle Merhaba ve günlük hello DBMS, tooAzure dosyaları. İçinde açıklanan hello senaryosu aksine [Senaryo 2: özel bir görüntü ile bir VM için SAP dağıtma][deployment-guide-3.3], bu durumda, hello ana bilgisayar adı, SAP SID tutmak ve SAP kullanıcı hesapları hello Azure VM oldukları için Merhaba şirket içi ortamda yapılandırılmış. Toogeneralize hello OS gerekmez. Bu senaryo için burada hello SAP yatay parçası şirket içi çalışır ve kısmını Azure üzerinde çalışan en sık toocross içi senaryoları geçerlidir.

Bu senaryoda, hello VM Aracısı dağıtımı sırasında otomatik olarak yüklenmez. Hello VM aracısı ve hello Gelişmiş izleme uzantısı SAP için Azure SAP toorun için gerekli olduğundan, her iki toodownload, yükleme ve etkinleştirme gereken el ile Merhaba sanal makineyi oluşturduktan sonra bileşenleri.

Hello Azure VM Aracısı hakkında daha fazla bilgi için kaynakları aşağıdaki hello bakın.

[comment]: <> (MSSedusch Yapılacaklar güncelleştirme Windows bağlantıyı)

- - -
> ![Windows][Logo_Windows] Windows
>
> <http://blogs.msdn.com/b/wats/archive/2014/02/17/bginfo-Guest-Agent-Extension-for-Azure-VMs.aspx>
>
> ![Linux][Logo_Linux] Linux
>
> [Azure Linux Aracısı Kullanıcı Kılavuzu][virtual-machines-linux-agent-user-guide]
>
>

- - -

Aşağıdaki akış çizelgesi hello genelleştirilmiş Azure VHD kullanarak bir şirket içi VM taşıma adımları hello sırasını göstermektedir:

![VM dağıtımı için bir VM disk kullanarak SAP sistemleri akış çizelgesi][deployment-guide-figure-400]

Merhaba disk zaten karşıya ve Azure'da tanımlanan varsayılarak (bkz [Azure sanal makineleri planlama ve uygulama Linux üzerinde SAP için][planning-guide]), yapmak hello görevleri açıklanan hello sonraki birkaç bölümler.

#### <a name="create-a-virtual-machine"></a>Sanal makine oluşturma
toocreate hello Azure portal aracılığıyla özel bir işletim sistemi diski kullanarak bir dağıtım hello yayımlanan hello SAP şablonu kullanın [azure hızlı başlangıç şablonlarını GitHub deposunu][azure-quickstart-templates-github]. Ayrıca el ile bir sanal makine PowerShell kullanarak oluşturabilirsiniz.

* [**İki katmanlı yapılandırma (yalnızca bir sanal makine) şablonu** (sap-2-katman-kullanıcı-disk)][sap-templates-2-tier-os-disk]

  toocreate yalnızca bir sanal makine kullanarak iki katmanlı sistem bu şablonu kullanın.

Hello Azure portalı, şu parametreler hello şablonunun hello girin:

1. **Temel kavramları**:
  * **Abonelik**: hello abonelik toouse toodeploy hello şablonu.
  * **Kaynak grubu**: hello kaynak grubu toouse toodeploy hello şablonu. Yeni bir kaynak grubu oluşturun veya varolan bir kaynak grubu hello abonelikte seçin.
  * **Konum**: Burada toodeploy hello şablonu. Varolan bir kaynak grubu seçtiyseniz, bu kaynak grubunun hello konumu kullanılır.
2. **Ayarları**:
  * **SAP sistem kimliği**: Merhaba SAP sistem kimliği
  * **İşletim sistemi türü**: Merhaba toodeploy (Windows veya Linux) istediğiniz işletim sistemi türü.
  * **SAP sistem boyutu**: Merhaba hello SAP sistem boyutu.

    SAP hello yeni sistem Hello sayısını sağlar. Kaç tane SAP hello sistemi gerektirir emin değilseniz, SAP teknolojisi iş ortağı veya sistem Tümleştirici isteyin.
  * **Depolama türü** (yalnızca iki katmanlı şablon): Merhaba depolama toouse türü.

    Daha büyük sistemler için yüksek oranda Azure Premium Storage kullanmanızı öneririz. Depolama türleri hakkında daha fazla bilgi için kaynakları aşağıdaki hello bakın:
      * [SAP DBMS örneği için Azure Premium SSD depolama kullanımı][2367194]
      * [Microsoft Azure depolama] [ dbms-guide-2.3] içinde [Linux üzerinde SAP için Azure sanal makine DBMS dağıtımı][dbms-guide]
      * [Premium Storage: Azure sanal makine iş yükleri için yüksek performanslı depolama][storage-premium-storage-preview-portal]
      * [Giriş tooMicrosoft Azure depolama][storage-introduction]
  * **İşletim sistemi diski VHD URİ'si**: hello özel işletim sistemi diski, örneğin, https:// URI'sini hello&lt;accountname >.blob.core.windows.net/vhds/osdisk.vhd.
  * **Yeni veya var olan bir alt ağ**: yeni bir sanal ağ ve alt ağ oluşturulur veya mevcut bir alt kullanılan olup olmadığını belirler. Bağlı tooyour şirket içi ağ bir sanal ağ zaten varsa, seçin **varolan**.
  * **Alt ağ kimliği**: hello kimliği hello alt toowhich hello sanal makinelerin bağlanması için. VPN veya Azure ExpressRoute sanal ağ toouse tooconnect hello sanal makine tooyour Şirket ağınızın Hello alt ağ seçin. Merhaba kimliği genellikle şu şekildedir:

    /Subscriptions/&lt;abonelik kimliği > /resourceGroups/&lt;kaynak grubu adı > /providers/Microsoft.Network/virtualNetworks/&lt;sanal ağ adı > /subnets/&lt;alt ağ adı >

3. **Hüküm ve koşullar**:  
    Gözden geçirin ve hello yasal koşulları kabul edin.

4.  Seçin **satın alma**.

#### <a name="install-hello-vm-agent"></a>Merhaba VM Aracısı yükleme
Şablonları açıklanan toouse hello hello önceki bölümde, hello VM Aracısı hello işletim sistemi disk üzerinde yüklü olmalıdır veya başlangıç dağıtımı başarısız olur. Karşıdan yükleyip hello VM Aracısı hello VM açıklandığı gibi [indirme, yükleme ve hello Azure VM Aracısı etkinleştirme][deployment-guide-4.4].

Hello önceki bölümde açıklanan hello şablonları kullanmıyorsanız, daha sonra hello VM Aracısı da yükleyebilirsiniz.

#### <a name="join-a-domain-windows-only"></a>(Yalnızca Windows) etki alanına Katıl
Azure dağıtımınıza bağlı tooan şirket içi Active Directory veya DNS bir Azure siteden siteye VPN bağlantısı veya ExpressRoute aracılığıyla örneğiyse (Bu adlı *şirketler arası* içinde [Azure sanal makineleri planlama ve Linux üzerinde SAP uygulamasını][planning-guide]), o hello VM bir şirket içi etki alanına katılma beklenir. Bu görev için konuları hakkında daha fazla bilgi için bkz: [VM tooan şirket içi etki alanına (yalnızca Windows) katılma][deployment-guide-4.3].

#### <a name="configure-proxy-settings"></a>Proxy ayarlarını yapılandır
Şirket içi ağınıza nasıl yapılandırıldığına bağlı olarak, VM hello proxy yukarı tooset gerekebilir. VM bağlı tooyour şirket içi ağ VPN ya da ExpressRoute aracılığıyla ise, hello VM değil mümkün tooaccess hello Internet olması ve olmaz mümkün toodownload gerekli hello uzantıları veya izleme verilerini topla. Daha fazla bilgi için bkz: [hello proxy yapılandırma][deployment-guide-configure-proxy].

#### <a name="configure-monitoring"></a>İzlemeyi Yapılandır
ortamınızı açıklandığı gibi hello Azure Monitoring uzantısı SAP için ayarlamak SAP desteklediğinden emin toobe [yapılandırma hello Azure Gelişmiş izleme uzantısı SAP][deployment-guide-4.5]. SAP izleme ve gerekli en düşük sürümlerinde SAP çekirdek ve SAP konak Aracısı, listelenen hello kaynakları Hello önkoşullarını denetlemek [SAP kaynakları][deployment-guide-2.2].

#### <a name="monitoring-check"></a>Onay izleme
İzleme çalışıp çalışmadığını, açıklandığı gibi denetleyin [denetler ve uçtan uca izleme ayarlamak için sorun giderme][deployment-guide-troubleshooting-chapter].

## <a name="update-hello-monitoring-configuration-for-sap"></a>SAP için izleme yapılandırmasını Hello güncelleştir
Herhangi bir senaryo aşağıdaki hello Hello SAP İzleme yapılandırmasını güncelleştirin:
* Merhaba birleşik Microsoft/SAP takım izleme kapasiteleri hello genişletir ve daha fazla veya daha az sayaçları ister.
* Microsoft izleme verilerini hello teslim eden hello Azure altyapının yeni bir sürümünü kullanıma sunmaktadır ve SAP gereksinimlerini toobe Merhaba Azure Gelişmiş izleme uzantısı toothose değişiklikleri uyarlanan.
* Ek VHD'ler tooyour Azure VM bağlayın veya bir VHD'yi kaldırın. Bu senaryoda, depolama ile ilgili veriler hello koleksiyonu güncelleştirin. Ekleyerek veya silerek uç noktaları veya IP atayarak yapılandırmanızı değiştirme adresleri tooa VM hello izleme yapılandırması etkilemez.
* Hello boyutunu Azure VM, örneğin, boyutu A5 tooany diğer VM boyutunu değiştirin.
* Yeni ağ arabirimleri tooyour Azure VM ekleyin.

izleme ayarları, aşağıdaki hello tarafından altyapısını izleme güncelleştirme hello tooupdate adımları [yapılandırma hello Azure Gelişmiş izleme uzantısı SAP][deployment-guide-4.5].

## <a name="detailed-tasks-for-sap-software-deployment-on-a-windows-vm"></a>Bir Windows VM üzerinde SAP yazılım dağıtımı için ayrıntılı görevleri
Bu bölümde belirli görevlerle hello yapılandırma ve dağıtım işlemindeki adımları açıklanmıştır.

### <a name="604bcec2-8b6e-48d2-a944-61b0f5dee2f7"></a>Azure PowerShell cmdlet'lerini dağıtma
1.  Çok Git[Microsoft Azure indirmeleri](https://azure.microsoft.com/downloads/).
2.  Altında **komut satırı araçları**altında **PowerShell**seçin **Windows yükleme**.
3.  İndirilen hello dosyası (örneğin, WindowsAzurePowershellGet.3f.3f.3fnew.exe) için hello Microsoft İndirme Yöneticisi iletişim kutusunda seçin **çalıştırmak**.
4.  Microsoft Web Platformu Yükleyicisi (Microsoft Web PI) toorun seçin **Evet**.
5.  Bu görünür benzer bir sayfa:

  ![Azure PowerShell cmdlet'leri yükleme sayfası][deployment-guide-figure-500]<a name="figure-5"></a>

6.  Seçin **yükleme**ve hello Microsoft Yazılımı Lisans koşulları kabul edin.
7.  PowerShell yüklü. Seçin **son** tooclose hello Yükleme Sihirbazı'nı.

Genellikle aylık güncelleştirilen güncelleştirmeleri toohello için PowerShell cmdlet'leri, sık sık denetleyin. Merhaba en kolay yolu toocheck güncelleştirmeleri için yükleme adımları, adım 5'te gösterilen toohello yükleme sayfasını önceki toodo hello ' dir. Adım 5'te gösterilen hello sayfasında Hello yayın tarihini ve sürüm numarasını hello cmdlet'leri dahil edilir. SAP notta aksi belirtilmediği sürece [1928533] veya SAP Not [2015553], hello en son sürümü Azure PowerShell cmdlet'leri ile çalışma öneririz.

Merhaba, bilgisayarınızda yüklü olan Azure PowerShell cmdlet'lerini toocheck hello sürümü bu PowerShell komutunu çalıştırın:
```powershell
Import-Module Azure
(Get-Module Azure).Version
```
Merhaba sonuç şöyle görünür:

![Azure PowerShell cmdlet sürüm denetiminin sonucu.][deployment-guide-figure-600]
<a name="figure-6"></a>

Bilgisayarınızda yüklü hello Azure cmdlet sürümü hello geçerli sürüm ise hello Yükleme Sihirbazı'nın ilk sayfasında hello ekleyerek belirtir **(yüklü)** toohello ürün başlığı (ekran aşağıdaki hello bakın). PowerShell Azure cmdlet'lerini güncel değil. tooclose hello Yükleme Sihirbazı, select **çıkış**.

![Azure PowerShell cmdlet'leri bu hello en son sürümünü gösteren Azure PowerShell cmdlet'leri için yükleme sayfasını yüklenir][deployment-guide-figure-700]
<a name="figure-7"></a>

### <a name="1ded9453-1330-442a-86ea-e0fd8ae8cab3"></a>Azure CLI dağıtma
1.  Çok Git[Microsoft Azure indirmeleri](https://azure.microsoft.com/downloads/).
2.  Altında **komut satırı araçları**altında **Azure komut satırı arabirimi**seçin hello **yükleme** işletim sisteminizin bağlantı.
3.  İndirilen hello dosyası (örneğin, WindowsAzureXPlatCLI.3f.3f.3fnew.exe) için hello Microsoft İndirme Yöneticisi iletişim kutusunda seçin **çalıştırmak**.
4.  Microsoft Web Platformu Yükleyicisi (Microsoft Web PI) toorun seçin **Evet**.
5.  Bu görünür benzer bir sayfa:

  ![Azure PowerShell cmdlet'leri yükleme sayfası][deployment-guide-figure-500]<a name="figure-5"></a>

6.  Seçin **yükleme**ve hello Microsoft Yazılımı Lisans koşulları kabul edin.
7.  Azure CLI yüklenir. Seçin **son** tooclose hello Yükleme Sihirbazı'nı.

Sık sık güncelleştirmeler tooAzure genellikle her ay güncelleştirilen CLI denetleyin. Merhaba en kolay yolu toocheck güncelleştirmeleri için yükleme adımları, adım 5'te gösterilen toohello yükleme sayfasını önceki toodo hello ' dir.


Bilgisayarınızda yüklü olan Azure CLI toocheck hello sürümü bu komutu çalıştırın:
```
azure --version
```

Merhaba sonuç şöyle görünür:

![Azure CLI sürüm denetiminin sonucu.][deployment-guide-figure-760]
<a name="0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda"></a>

### <a name="31d9ecd6-b136-4c73-b61e-da4a29bbc9cc"></a>Bir VM tooan şirket içi etki (yalnızca Windows)
Bir şirket içi senaryosunda SAP VM'ler dağıtırsanız, şirket içi Active Directory ve DNS Azure'da, burada genişletilmiş onu hello VM'ler bir şirket içi etki alanına katılma beklenir. VM tooan şirket içi etki alanı toojoin uygulamanız ayrıntılı adımlar hello ve hello gereken ek yazılım toobe bir şirket içi etki alanının üyesi değişir müşteri tarafından. Genellikle, toojoin VM tooan içi etki alanı, kötü amaçlı yazılımdan koruma yazılımı ve yedekleme ya da izleme yazılım gibi tooinstall ek yazılım gerekir.

Bu senaryoda, ayrıca toomake hello Windows hello Konuk VM yerel sistem hesabı (S-1-5-18) sahip bir VM, ortamınızdaki bir etki alanına katıldığında Internet proxy ayarlarını zorlanır, aynı proxy ayarlarını hello emin gerekir. Merhaba kolay tooforce hello proxy etki alanı toosystems hello etki alanındaki geçerli Grup İlkesi kullanarak bir seçenektir.

### <a name="c7cbb0dc-52a4-49db-8e03-83e7edc2927d"></a>İndirme, yükleme ve hello Azure VM Aracısı etkinleştir
(Örneğin, hello sysprep veya Windows Sistem Hazırlama aracı kökenli olmayan bir görüntü) genelleştirilmiş olmayan bir işletim sistemi görüntüsünden dağıtılan sanal makineler için toomanually indirme, yükleme ve etkinleştirme hello Azure VM Aracısı gerekiyor.

Hello Azure Marketi VM'den dağıtırsanız, bu adım gerekli değildir. Hello Azure Marketi görüntülerden hello Azure VM Aracısı zaten var.

#### <a name="b2db5c9a-a076-42c6-9835-16945868e866"></a>Windows
1.  Hello Azure VM aracısı yükleyin:
  1.  Merhaba karşıdan [Azure VM Aracısı Yükleyici paketi](https://go.microsoft.com/fwlink/?LinkId=394789).
  2.  Merhaba VM Aracısı MSI paketini bir kişisel bilgisayar veya sunucu üzerinde yerel olarak depolar.
2.  Hello Azure VM aracısı yükleyin:
  1.  Connect toohello Uzak Masaüstü Protokolü (RDP) kullanılarak Azure VM dağıtılır.
  2.  Bir Windows Gezgini penceresinde hello VM üzerinde ve hello VM Aracısı hello MSI dosyası için select hello hedef dizini açın.
  3.  Hello Azure VM Aracısı yükleyici MSI dosyası, yerel bilgisayar/sunucu toohello hedef dizininden hello VM Aracısı VM hello üzerinde sürükleyin.
  4.  Merhaba VM Hello MSI dosyasına çift tıklayın.
3.  Birleştirilmiş tooon içi etki alanları olan VM'ler için açıklandığı gibi nihai Internet proxy ayarlarını hello VM, ayrıca toohello Windows yerel sistem hesabı (S-1-5-18) uyguladığınızdan emin olun [hello proxy yapılandırma] [ deployment-guide-configure-proxy]. Merhaba VM Aracısı bu bağlamda çalıştırır ve toobe mümkün tooconnect tooAzure gerekiyor.

Kullanıcı etkileşimi gerekli tooupdate hello Azure VM Aracısı değildir. Merhaba VM Aracısı otomatik olarak güncelleştirilir ve VM yeniden başlatma gerektirmez.

#### <a name="6889ff12-eaaf-4f3c-97e1-7c9edc7f7542"></a>Linux
Linux için komutları tooinstall hello VM aracısı aşağıdaki hello kullan:

* **SUSE Linux Enterprise Server (SLES)**

  ```
  sudo zypper install WALinuxAgent
  ```

* **Red Hat Enterprise Linux (RHEL)**

  ```
  sudo yum install WALinuxAgent
  ```

Merhaba Aracısı zaten yüklüyse, tooupdate hello Azure Linux Aracısı hello bölümünde açıklanan adımları [github'dan VM toohello en son sürümünü güncelleştirme hello Azure Linux Aracısı][virtual-machines-linux-update-agent].

### <a name="baccae00-6f79-4307-ade4-40292ce4e02d"></a>Merhaba proxy ayarlarını yapılandır
tooconfigure hello proxy Windows hello adımlar Linux içinde hello proxy yapılandırma hello yolu farklıdır.

#### <a name="windows"></a>Windows
Proxy ayarları doğru şekilde hello Internet tooaccess hello yerel sistem hesabı için ayarlanması gerekir. Proxy ayarlarını Grup İlkesi tarafından ayarlanmamışsa, hello yerel sistem hesabı için hello ayarlarını yapılandırabilirsiniz.

1. Çok Git**Başlat**, girin **gpedit.msc**ve ardından **Enter**.
2. Seçin **Bilgisayar Yapılandırması** > **Yönetim Şablonları** > **Windows bileşenleri** > **Internet Explorer**. Bu hello ayarı emin olun **proxy ayarlarını makine başına (yerine kullanıcı başına) olun** devre dışı veya yapılandırılmamış.
3. İçinde **Denetim Masası**, çok Git**ağ ve Paylaşım Merkezi** > **Internet Seçenekleri**.
4. Merhaba üzerinde **bağlantıları** sekmesi, select hello **LAN Ayarları** düğmesi.
5. Clear hello **ayarları otomatik olarak algıla** onay kutusu.
6. Select hello **AĞINIZ için bir proxy sunucu kullanacak** onay kutusunu işaretleyin ve ardından hello proxy adresi ve bağlantı noktası girin.
7. Select hello **Gelişmiş** düğmesi.
8. Merhaba, **özel durumları** kutusuna, başlangıç IP adresi girin **168.63.129.16**. **Tamam**’ı seçin.


#### <a name="linux"></a>Linux
Merhaba yapılandırma dosyasındaki hello konumda bulunan Microsoft Azure Konuk Aracısı Hello doğru proxy yapılandırma \\vb.\\waagent.conf.

Şu parametreler hello ayarlayın:

1.  **HTTP proxy konağını**. Örneğin, çok ayarlamak**proxy.corp.local**.
  ```
  HttpProxy.Host=<proxy host>

  ```
2.  **HTTP proxy bağlantı noktası**. Örneğin, çok ayarlamak**80**.
  ```
  HttpProxy.Port=<port of hello proxy host>

  ```
3.  Merhaba aracıyı yeniden başlatın.

  ```
  sudo service waagent restart
  ```

Merhaba proxy ayarları \\vb.\\waagent.conf gerekli toohello VM uzantıları de geçerlidir. Toouse istiyorsanız Azure depoları Merhaba, hello trafiği toothese depoları değil olduğuna, şirket içi intranetiniz üzerinden emin olun. Kullanıcı tanımlı oluşturduysanız yollar tooenable zorlamalı tünel, trafik toohello depoları yönlendiren bir rota eklediğinizden emin olun doğrudan toohello Internet ve siteden siteye VPN bağlantısı üzerinden değil.

* **SLES**

  Başlangıç IP adresi listelenen için tooadd yollar da gerekir \\vb.\\regionserverclnt.cfg. Merhaba aşağıdaki şekilde bir örnek gösterilmektedir:

  ![Zorlamalı tünel oluşturma][deployment-guide-figure-50]


* **RHEL**

  Merhaba konakları Hello IP adreslerini listelenen için tooadd yollar da gerekir \\vb.\\yum.repos.d\\rhui yük dengeleyicileri. Örneğin, Şekil önceki hello bakın.

Kullanıcı tanımlı yollar hakkında daha fazla bilgi için bkz: [kullanıcı tanımlı yollar ve IP iletimini][virtual-networks-udr-overview].

### <a name="d98edcd3-f2a1-49f7-b26a-07448ceb60ca"></a>Hello Azure Gelişmiş izleme uzantısı SAP yapılandırın
Ne zaman hazırlıklı hello VM açıklandığı gibi [VM'ler Azure üzerinde SAP için dağıtım senaryoları][deployment-guide-3], hello Azure VM Aracısı hello sanal makineye yüklenir. Merhaba sonraki toodeploy hello Azure Gelişmiş izleme uzantısı hello Azure uzantısı deposuna hello genel Azure veri merkezleri içinde kullanılabilir SAP adımdır. Daha fazla bilgi için bkz: [Azure sanal makineleri planlama ve uygulama Linux üzerinde SAP için][planning-guide-9.1].

PowerShell veya Azure CLI tooinstall kullanın ve hello Azure Gelişmiş izleme uzantısı SAP yapılandırın. Windows makine kullanarak bir Windows veya Linux VM tooinstall hello uzantısını görmek [Azure PowerShell][deployment-guide-4.5.1]. bir Linux Masaüstü kullanarak bir Linux VM tooinstall hello uzantısı bkz [Azure CLI][deployment-guide-4.5.2].

#### <a name="987cf279-d713-4b4c-8143-6b11589bb9d4"></a>Linux ve Windows VM'ler için Azure PowerShell
tooinstall hello Gelişmiş izleme uzantısı SAP için Azure PowerShell kullanarak:

1. Merhaba hello Azure PowerShell cmdlet'ini en son sürümünü yüklediğinizden emin olun. Daha fazla bilgi için bkz: [dağıtımı Azure PowerShell cmdlet'lerini][deployment-guide-4.1].  
2. Merhaba aşağıdaki PowerShell cmdlet'ini çalıştırın.
  Kullanılabilir ortamlar listesi için çalıştırın `commandlet Get-AzureRmEnvironment`. Ortak Azure, ortamınızı toouse istiyorsanız **AzureCloud**. Çin'de Azure için seçin **AzureChinaCloud**.


      ```powershell
      $env = Get-AzureRmEnvironment -Name <name of hello environment>
      Login-AzureRmAccount -Environment $env
      Set-AzureRmContext -SubscriptionName <subscription name>

      Set-AzureRmVMAEMExtension -ResourceGroupName <resource group name> -VMName <virtual machine name>
      ```

Hesap verilerinizi girip hello Azure sanal makinesi tanımlamak sonra hello betik gerekli hello uzantıları dağıtır ve gerekli hello özelliklerini etkinleştirir. Bu işlem birkaç dakika sürebilir.
Hakkında daha fazla bilgi için `Set-AzureRmVMAEMExtension`, bkz: [kümesi AzureRmVMAEMExtension][msdn-set-azurermvmaemextension].

![SAP özgü aktarılmadığı Azure cmdlet kümesi AzureRmVMAEMExtension][deployment-guide-figure-900]

Merhaba `Set-AzureRmVMAEMExtension` yapılandırma tüm hello adımları tooconfigure konak için SAP izleme yapar.

Merhaba komut dosyası çıkışını bilgisinden hello içerir:

* Onay, hello temel VHD (ile Merhaba OS) ve tüm ek VHD'leri izleme VM yapılandırılmış toohello bağladı.
* Merhaba sonraki iki iletileri belirli bir depolama hesabı için depolama ölçümleri hello yapılandırmasını doğrulayın.
* Tek satırlık bir çıktı hello gerçek güncelleştirme hello izleme yapılandırmasının hello durumunu verir.
* Başka bir satır çıktı hello yapılandırmayı dağıtılan ya da güncelleştirilmiş onaylar.
* çıktının son satırında Hello bilgilendirme amaçlıdır. Sınama hello izleme yapılandırma seçeneklerini gösterir.

Gelişmiş Azure Monitoring tüm adımları başarıyla yürütüldü ve hello gerekli verileri, o hello Azure altyapısı sağlar toocheck devam hello Gelişmiş izleme uzantısı SAP, Azure için hello hazırlık denetimi ile açıklandığı gibi [Gelişmiş Azure izlemesi için SAP için hazırlık denetimi][deployment-guide-5.1]. Azure tanılama toocollect hello ilgili verileri 15-30 dakika bekleyin.

#### <a name="408f3779-f422-4413-82f8-c57a23b4fc2f"></a>Linux VM'ler için Azure CLI
tooinstall hello Azure CLI kullanarak Azure Gelişmiş izleme uzantısı SAP:

1. Bölümünde açıklandığı gibi Azure CLI yükleme [yükleme hello Azure CLI][azure-cli].
2. Azure hesabınızla oturum açın:

  ```
  azure login
  ```

3. TooAzure Resource Manager moduna geçin:

  ```
  azure config mode arm
  ```

4. Azure Gelişmiş izlemeyi etkinleştir:

  ```
  azure vm enable-aem <resource-group-name> <vm-name>
  ```

5. Bu hello Azure Gelişmiş izleme uzantısı hello Azure Linux VM etkin olduğunu doğrulayın. Onay olup dosya hello \\var\\lib\\AzureEnhancedMonitor\\PerfCounters bulunmaktadır. Bir komut isteminde varsa Azure Gelişmiş İzleyicisi Merhaba tarafından toplanan bu komut toodisplay bilgilerini çalıştırın:
```
cat /var/lib/AzureEnhancedMonitor/PerfCounters
```

Merhaba çıktı şu şekildedir:
```
2;cpu;Current Hw Frequency;;0;2194.659;MHz;60;1444036656;saplnxmon;
2;cpu;Max Hw Frequency;;0;2194.659;MHz;0;1444036656;saplnxmon;
…
…
```

## <a name="564adb4f-5c95-4041-9616-6635e83a810b"></a>Denetim ve uçtan uca izleme için sorun giderme
Azure VM dağıtılan ve hello ilgili Azure izleme altyapıyı ayarladıktan sonra hello Azure Gelişmiş izleme uzantısı hello bileşenlerinin tümünü beklendiği gibi çalışıp çalışmadığını denetleyin.

Bölümünde açıklandığı gibi hello Azure Gelişmiş izleme uzantısı SAP için Hello hazırlık denetimini Çalıştır [hello Azure Gelişmiş izleme uzantısı SAP için hazırlık denetimi][deployment-guide-5.1]. Tüm hazırlık denetimi sonuçları pozitif ve tüm ilgili performans sayaçları Tamam görünür, Azure İzleme'ı başarıyla kuruldu. SAP konak hello SAP notları açıklanan Aracısı hello yüklemesi devam edebilmeniz [SAP kaynakları][deployment-guide-2.2]. Merhaba hazırlık denetimi açıklandığı gibi hello Azure izleme altyapı için hello sistem durumu denetimi Çalıştır sayaçları eksik olduğunu gösteriyorsa [izleme Azure altyapısı yapılandırması için sistem durumu denetimi] [ deployment-guide-5.2]. Daha fazla sorun giderme seçenekleri için bkz: [Azure sorun giderme için SAP izleme][deployment-guide-5.3].

### <a name="bb61ce92-8c5c-461f-8c53-39f5e5ed91f2"></a>Hello Azure Gelişmiş izleme uzantısı SAP hazır olma durumunu denetle
Bu onay SAP uygulamanız içinde görünür tüm performans ölçümlerinin altyapısını izleme Azure arka plandaki hello tarafından sağlanan emin olur.

#### <a name="run-hello-readiness-check-on-a-windows-vm"></a>Bir Windows VM üzerinde Hello hazırlık denetimi Çalıştır

1.  Toohello Azure sanal makinesi oturum (bir yönetici hesabı kullanarak gerekli değildir).
2.  Bir komut istemi penceresi açın.
3.  Merhaba komut isteminde hello dizin toohello yükleme klasörü hello Azure Gelişmiş izleme uzantısı SAP değiştirin: C:\\paketleri\\eklentileri\\ Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;sürüm >\\bırak

  Merhaba *sürüm* hello yolu toohello izleme uzantısı değişebilir. Klasörleri birden fazla sürümünü hello izleme uzantısı hello yükleme klasöründe, onay hello yapılandırmasını hello AzureEnhancedMonitoring Windows hizmeti için görürseniz ve olarak anahtar toohello klasörü belirtilen *yolu tooexecutable* .

  ![Hizmet çalışıyor özelliklerini Azure Gelişmiş izleme uzantısı SAP hello][deployment-guide-figure-1000]

4.  Merhaba komut isteminde çalıştırmak **azperflib.exe** hiçbir parametre olmadan.

  > [!NOTE]
  > Azperflib.exe bir döngüde çalışır ve her 60 saniyede toplanan hello sayaçlarını güncelleştirir. tooend hello döngü, Kapat hello komut istemi penceresi.
  >
  >

Hello Azure Gelişmiş izleme uzantısı yüklü değil ya da hello AzureEnhancedMonitoring hizmeti çalışmıyorsa, hello uzantısı düzgün yapılandırılmamış. Nasıl toodeploy hello uzantısı hakkında ayrıntılı bilgi için bkz: [sorun giderme için SAP Azure izleme altyapısının hello][deployment-guide-5.3].

##### <a name="check-hello-output-of-azperflibexe"></a>Azperflib.exe onay hello çıktısı
Tüm Azure performans sayaçları için SAP doldurulmuş Azperflib.exe çıktısını gösterir. Toplanan sayaçlarının listesi hello Hello altındaki hello durumunu Azure İzleme Özeti ve sistem durumu gösterge gösterir.

![Sistem durumu denetimi herhangi bir sorun mevcut olduğunu gösteren azperflib.exe çalıştırarak çıktısı][deployment-guide-figure-1100]
<a name="figure-11"></a>

Merhaba döndürülen hello sonuç denetleme **sayaçları toplam** bildirilen boş olarak ve için çıktı **sistem durumu**şekil önceki hello gösterilen.

Merhaba elde edilen değerleri aşağıdaki gibi yorumlar:

| Azperflib.exe sonuç değerleri | Azure sistem durumunu izleme |
| --- | --- |
| **API çağrıları - mevcut değil** | Kullanılabilir değil sayaçları ya da geçerli değil toohello sanal makine yapılandırması olabilir veya hatalardır. Bkz: **sistem durumu**. |
| **Sayaçları toplam - boş** |iki Azure depolama sayaçları aşağıdaki hello boş olabilir: <ul><li>Depolama alanından Op gecikme okuma sunucu milisaniye</li><li>Depolama alanından Op gecikme okuma E2E milisaniye</li></ul>Diğer tüm sayaçları değerlere sahip olmalıdır. |
| **Sistem durumu** |Yalnızca Tamam IF dönüş durumu **Tamam**. |
| **Tanılama** |Sistem durumu hakkında ayrıntılı bilgiler. |

Merhaba, **sistem durumu** değeri değil **Tamam**, hello yönergeleri izleyin [izleme Azure altyapısı yapılandırması için sistem durumu denetimi] [ deployment-guide-5.2].

#### <a name="run-hello-readiness-check-on-a-linux-vm"></a>Bir Linux VM üzerinde Hello hazırlık denetimi Çalıştır

1.  SSH kullanarak toohello Azure sanal makinesine bağlanın.

2.  Hello Azure Gelişmiş izleme uzantısı Hello çıktısını denetleyin.

  a.  `more /var/lib/AzureEnhancedMonitor/PerfCounters` öğesini çalıştırın

   **Beklenen sonucu**: performans sayaçları listesi döndürür. Merhaba dosya boş olmamalıdır.

 b. `cat /var/lib/AzureEnhancedMonitor/PerfCounters | grep Error` öğesini çalıştırın

   **Beklenen sonucu**: hello hata olduğu döndürür tek bir çizgi **hiçbiri**, örneğin, **3; config; Hata; 0; 0; yok; 0; 1456416792; tst servercs;**

  c. `more /var/lib/AzureEnhancedMonitor/LatestErrorRecord` öğesini çalıştırın

    **Beklenen sonucu**: boş olarak döndürür veya yok.

Merhaba önceki onay başarılı olmazsa, bu ek denetimler çalıştırın:

1.  Bu hello waagent yüklü ve etkin olduğundan emin olun.

  a.  `sudo ls -al /var/lib/waagent/` öğesini çalıştırın

      **Beklenen sonucu**: hello hello waagent dizinin içeriğini listeler.

  b.  `ps -ax | grep waagent` öğesini çalıştırın

   **Beklenen sonucu**: için benzer bir giriş görüntüler:`python /usr/sbin/waagent -daemon`

2. Linux tanılama uzantısı yüklü ve etkin bu hello emin olun.

  a.  `sudo sh -c 'ls -al /var/lib/waagent/Microsoft.OSTCExtensions.LinuxDiagnostic-'` öğesini çalıştırın

   **Beklenen sonucu**: hello hello Linux tanılama uzantısını dizinin içeriğini listeler.

 b. `ps -ax | grep diagnostic` öğesini çalıştırın

   **Beklenen sonucu**: için benzer bir giriş görüntüler:`python /var/lib/waagent/Microsoft.OSTCExtensions.LinuxDiagnostic-2.0.92/diagnostic.py -daemon`

3.   Bu hello Azure Gelişmiş izleme uzantısı yüklü olduğundan ve çalıştığından emin olun.

  a.  `sudo sh -c 'ls -al /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-/'` öğesini çalıştırın

    **Beklenen sonucu**: hello hello Azure Gelişmiş izleme uzantısı dizinin içeriğini listeler.

  b. `ps -ax | grep AzureEnhanced` öğesini çalıştırın

     **Beklenen sonucu**: için benzer bir giriş görüntüler:`python /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-2.0.0.2/handler.py daemon`

3. SAP konak Aracısı SAP Not açıklandığı gibi yüklemeniz [1031096]ve hello çıktısını kontrol `saposcol`.

  a.  `/usr/sap/hostctrl/exe/saposcol -d` öğesini çalıştırın

  b.  `dump ccm` öğesini çalıştırın

  c.  Onay olup hello **Virtualization_Configuration\Enhanced izleme erişim** ölçümüdür **doğru**.

Yüklü bir SAP NetWeaver ABAP uygulama sunucusu zaten varsa, işlem ST06 açın ve Gelişmiş izleme etkin olup olmadığını denetleyin.

Tüm bu denetimlerin başarısız olursa, ve nasıl tooredeploy hello uzantısı hakkında ayrıntılı bilgi için bkz: [sorun giderme için SAP Azure izleme altyapısının hello][deployment-guide-5.3].

### <a name="e2d592ff-b4ea-4a53-a91a-e5521edb6cd1"></a>Sistem durumu izleme Azure altyapısı yapılandırmasını Merhaba kontrol edin
Bazı izleme verilerini hello teslim edilmez varsa doğru belirtildiği gibi hello test açıklanan [Gelişmiş Azure izlemesi için SAP için hazırlık denetimi][deployment-guide-5.1]çalıştırın hello `Test-AzureRmVMAEMExtension` cmdlet toocheck olup hello Azure altyapısı ve izleme uzantısı için SAP hello izleme doğru şekilde yapılandırılır.

1.  Bölümünde açıklandığı gibi hello hello Azure PowerShell cmdlet'ini, en son sürümünü yüklediğinizden emin olun [dağıtımı Azure PowerShell cmdlet'lerini][deployment-guide-4.1].
2.  Merhaba aşağıdaki PowerShell cmdlet'ini çalıştırın. Kullanılabilir ortamlar listesi için hello cmdlet'i çalıştırmak `Get-AzureRmEnvironment`. toouse ortak Azure, select hello **AzureCloud** ortamı. Çin'de Azure için seçin **AzureChinaCloud**.
  ```powershell
  $env = Get-AzureRmEnvironment -Name <name of hello environment>
  Login-AzureRmAccount -Environment $env
  Set-AzureRmContext -SubscriptionName <subscription name>
  Test-AzureRmVMAEMExtension -ResourceGroupName <resource group name> -VMName <virtual machine name>
  ```

3.  Hesap verilerinizi girin ve hello Azure sanal makine belirleyin.

  ![SAP özgü giriş sayfasında Azure cmdlet Test VMConfigForSAP_GUI][deployment-guide-figure-1200]

4. Merhaba betik testleri hello hello sanal makinenin yapılandırmasını, seçin.

  ![Hello Azure izleme altyapısının başarılı test SAP için çıktısı][deployment-guide-figure-1300]

Her sistem durumu denetimi sonucu olduğundan emin olun **Tamam**. Bazı denetimleri değil görüntülerseniz **Tamam**, açıklandığı gibi hello güncelleştirme cmdlet'i çalıştırmak [yapılandırma hello Azure Gelişmiş izleme uzantısı SAP][deployment-guide-4.5]. 15 dakika bekleyin ve tekrar hello denetimleri açıklanan [Gelişmiş Azure izlemesi için SAP için hazırlık denetimi] [ deployment-guide-5.1] ve [Azure izleme altyapı yapılandırmaiçinsistemdurumudenetimi] [deployment-guide-5.2]. Merhaba denetimleri hala bazı veya tüm sayaçları ile ilgili bir sorun gösteriyorsa, bkz: [sorun giderme için SAP Azure izleme altyapısının hello][deployment-guide-5.3].

### <a name="fe25a7da-4e4e-4388-8907-8abc2d33cfd8"></a>Hello Azure izleme altyapısının SAP için sorun giderme

#### <a name="windowslogowindows-azure-performance-counters-do-not-show-up-at-all"></a>![Windows][Logo_Windows] Azure performans sayaçları hiç görünmüyor
Merhaba AzureEnhancedMonitoring Windows hizmeti Azure performans ölçümleri toplar. Merhaba hizmet doğru şekilde yüklenmemiş veya VM ile çalışmıyorsa, performans ölçümleri toplanabilir.

##### <a name="hello-installation-directory-of-hello-azure-enhanced-monitoring-extension-is-empty"></a>Merhaba yükleme dizini hello Azure Gelişmiş izleme uzantısı, boştur

###### <a name="issue"></a>Sorun
Merhaba yükleme dizini C:\\paketleri\\eklentileri\\Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;sürüm >\\açılan boştur.

###### <a name="solution"></a>Çözüm
Merhaba uzantısı yüklü değil. (Daha önce açıklandığı gibi) bu proxy sorunu olup olmadığını belirler. Toorestart hello makine ya da yeniden çalıştır hello gerekebilecek `Set-AzureRmVMAEMExtension` yapılandırma komut dosyası.

##### <a name="service-for-azure-enhanced-monitoring-does-not-exist"></a>Gelişmiş Azure izlemesi için hizmet yok

###### <a name="issue"></a>Sorun
Merhaba AzureEnhancedMonitoring Windows hizmeti yok.

Azperflib.exe çıktı bir hata oluşturur:

![Azperflib.exe yürütülmesi hello Azure Gelişmiş izleme uzantısı hello hizmeti SAP için çalışmadığını gösterir][deployment-guide-figure-1400]
<a name="figure-14"></a>

###### <a name="solution"></a>Çözüm
Merhaba hizmet mevcut değilse hello Azure Gelişmiş izleme uzantısı SAP doğru şekilde yüklenmedi. Dağıtım senaryonuz için açıklanan başlangıç adımları kullanarak Hello uzantısı dağıtmanız [VM'ler Azure SAP için dağıtım senaryoları][deployment-guide-3].

Bir saat sonra hello uzantısı dağıttıktan sonra yeniden hello Azure performans sayaçları hello Azure VM sağlanan olup olmadığını denetleyin.

##### <a name="service-for-azure-enhanced-monitoring-exists-but-fails-toostart"></a>Azure Gelişmiş izleme hizmeti var, ancak toostart başarısız

###### <a name="issue"></a>Sorun
Merhaba AzureEnhancedMonitoring Windows hizmeti var ve etkinleştirilir, ancak toostart başarısız olur. Daha fazla bilgi için hello uygulama olay günlüğünü denetleyin.

###### <a name="solution"></a>Çözüm
Merhaba yapılandırması doğru değil. Bölümünde açıklandığı gibi hello VM uzantısı izleme hello yeniden [yapılandırma hello Azure Gelişmiş izleme uzantısı SAP][deployment-guide-4.5].

#### <a name="windowslogowindows-some-azure-performance-counters-are-missing"></a>![Windows][Logo_Windows] Bazı Azure performans sayaçları kayboluyor
Merhaba AzureEnhancedMonitoring Windows hizmeti Azure performans ölçümleri toplar. Merhaba hizmet çeşitli kaynaklardan veri alır. Bazı yapılandırma verilerini yerel olarak toplanır ve bazı performans ölçümleri Azure tanılama salt okunurdur. Depolama sayaçları hello depolama abonelik düzeyinde, oturum açmasını kullanılır.

SAP Not kullanarak sorun giderme olursa [1999351] hello sorunu çözümlemek için değil, hello yeniden `Set-AzureRmVMAEMExtension` yapılandırma komut dosyası. Hemen etkinleştirildikten sonra depolama analytics veya tanılama sayaçları oluşturulamaz, saat toowait olabilir. Merhaba sorun devam ederse hello OP NT AZR BC Windows bileşeni veya BC-OP-LNX-AZR Linux sanal makine için bir SAP Müşteri Destek iletide açın.

#### <a name="linuxlogolinux-azure-performance-counters-do-not-show-up-at-all"></a>![Linux][Logo_Linux] Azure performans sayaçları hiç görünmüyor
Azure performans ölçümlerini bir arka plan programı tarafından toplanır. Merhaba arka plan programı çalışmıyorsa, performans ölçümleri toplanabilir.

##### <a name="hello-installation-directory-of-hello-azure-enhanced-monitoring-extension-is-empty"></a>Merhaba yükleme dizini hello Gelişmiş Azure Monitoring uzantısı, boştur

###### <a name="issue"></a>Sorun
Merhaba dizin \\var\\lib\\waagent\\ hello Gelişmiş Azure Monitoring uzantısı için bir alt yok.

###### <a name="solution"></a>Çözüm
Merhaba uzantısı yüklü değil. (Daha önce açıklandığı gibi) bu proxy sorunu olup olmadığını belirler. Toorestart hello makine ve/veya yeniden çalıştır hello gerekebilecek `Set-AzureRmVMAEMExtension` yapılandırma komut dosyası.

#### <a name="linuxlogolinux-some-azure-performance-counters-are-missing"></a>![Linux][Logo_Linux] Bazı Azure performans sayaçları kayboluyor
Azure'da performans ölçümleri, çeşitli kaynaklardan veri aldığı bir arka plan programı tarafından toplanır. Bazı yapılandırma verilerini yerel olarak toplanır ve bazı performans ölçümleri Azure tanılama salt okunurdur. Depolama sayaçları hello günlükleri depolama aboneliğinizde gelmektedir.

Bilinen sorunların eksiksiz ve güncel listesi için bkz. SAP Not [1999351], Gelişmiş Azure izlemesi için SAP için ek sorun giderme bilgileri içeriyor.

SAP Not kullanarak sorun giderme olursa [1999351] yok hello sorunu çözün, hello yeniden `Set-AzureRmVMAEMExtension` açıklandığı gibi yapılandırma komut dosyası [yapılandırma hello Azure Gelişmiş izleme uzantısı SAP][deployment-guide-4.5]. Hemen etkinleştirildikten sonra depolama analytics veya tanılama sayaçları oluşturulmuş olabilir değil çünkü bir saate toowait olabilir. Merhaba sorun devam ederse hello OP NT AZR BC Windows bileşeni veya BC-OP-LNX-AZR Linux sanal makine için bir SAP Müşteri Destek iletide açın.
