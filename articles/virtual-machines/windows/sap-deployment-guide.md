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
# <a name="deploy-sap-on-windows-vms-in-azure"></a><span data-ttu-id="e5404-103">Windows sanal makineleri Azure üzerinde SAP dağıtma</span><span class="sxs-lookup"><span data-stu-id="e5404-103">Deploy SAP on Windows VMs in Azure</span></span>
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

<span data-ttu-id="e5404-115">Azure sanal makinelerin olası en kısa süre içinde ve uzun tedarik döngüleri olmadan işlem ve depolama kaynaklarını gereken kuruluşlar için hello çözümü şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="e5404-115">Azure Virtual Machines is hello solution for organizations that need compute and storage resources, in minimal time, and without lengthy procurement cycles.</span></span> <span data-ttu-id="e5404-116">Azure'da Azure sanal makineleri toodeploy Klasik uygulamalar, SAP NetWeaver tabanlı uygulamalar gibi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5404-116">You can use Azure Virtual Machines toodeploy classical applications, like SAP NetWeaver-based applications, in Azure.</span></span> <span data-ttu-id="e5404-117">Bir uygulamanın güvenilirlik ve kullanılabilirlik ek şirket içi kaynaklar olmadan genişletir.</span><span class="sxs-lookup"><span data-stu-id="e5404-117">Extend an application's reliability and availability without additional on-premises resources.</span></span> <span data-ttu-id="e5404-118">Azure sanal makineleri şirket içi bağlantılar, Azure sanal makineler, kuruluşunuzun şirket içi etki alanları, özel Bulutlar ve SAP sistem yatay tümleştirebilir şekilde destekler.</span><span class="sxs-lookup"><span data-stu-id="e5404-118">Azure Virtual Machines supports cross-premises connectivity, so you can integrate Azure Virtual Machines into your organization's on-premises domains, private clouds, and SAP system landscape.</span></span>

<span data-ttu-id="e5404-119">Bu makalede, azure'da Windows sanal makineler (VM'ler) üzerinde hello adımları toodeploy SAP uygulamalar kapsar.</span><span class="sxs-lookup"><span data-stu-id="e5404-119">In this article, we cover hello steps toodeploy SAP applications on Windows virtual machines (VMs) in Azure.</span></span> <span data-ttu-id="e5404-120">Bu makalede hello bilgileri derlemeler [Azure sanal makineleri planlama ve uygulama için Windows üzerinde SAP][planning-guide].</span><span class="sxs-lookup"><span data-stu-id="e5404-120">This article builds on hello information in [Azure Virtual Machines planning and implementation for SAP on Windows][planning-guide].</span></span> <span data-ttu-id="e5404-121">Aynı zamanda, SAP yükleme belgelerini ve yükleme ve SAP yazılım dağıtma hello birincil kaynaklardır SAP Notlar tamamlar.</span><span class="sxs-lookup"><span data-stu-id="e5404-121">It also complements SAP installation documentation and SAP Notes, which are hello primary resources for installing and deploying SAP software.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e5404-122">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e5404-122">Prerequisites</span></span>
<span data-ttu-id="e5404-123">SAP yazılım dağıtımı için Azure sanal makinesi ayarlanıyor birden çok adımlar ve kaynaklar içerir.</span><span class="sxs-lookup"><span data-stu-id="e5404-123">Setting up an Azure virtual machine for SAP software deployment involves multiple steps and resources.</span></span> <span data-ttu-id="e5404-124">Başlamadan önce azure'da Windows sanal makinelerde SAP yazılımını yüklemek için hello önkoşulları karşıladığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="e5404-124">Before you start, make sure that you meet hello prerequisites for installing SAP software on Windows virtual machines in Azure.</span></span>

### <a name="local-computer"></a><span data-ttu-id="e5404-125">Yerel bilgisayar</span><span class="sxs-lookup"><span data-stu-id="e5404-125">Local computer</span></span>
<span data-ttu-id="e5404-126">Windows veya Linux sanal makineleri toomanage, PowerShell Betiği ve hello Azure portalını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5404-126">toomanage Windows or Linux VMs, you can use a PowerShell script and hello Azure portal.</span></span> <span data-ttu-id="e5404-127">Her iki Araçlar, Windows 7 veya sonraki bir Windows sürümü çalıştıran yerel bir bilgisayar gerekir.</span><span class="sxs-lookup"><span data-stu-id="e5404-127">For both tools, you need a local computer running Windows 7 or a later version of Windows.</span></span> <span data-ttu-id="e5404-128">Linux sanal makineleri ve bu görev için toouse Linux bilgisayarı istiyorsanız yalnızca toomanage istiyorsanız Azure CLI kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5404-128">If you want toomanage only Linux VMs and you want toouse a Linux computer for this task, you can use Azure CLI.</span></span>

### <a name="internet-connection"></a><span data-ttu-id="e5404-129">Internet bağlantısı</span><span class="sxs-lookup"><span data-stu-id="e5404-129">Internet connection</span></span>
<span data-ttu-id="e5404-130">toodownload ve çalışma hello araçları ve SAP yazılım dağıtımı için gerekli olan komut dosyaları, olmalısınız toohello Internet bağlı.</span><span class="sxs-lookup"><span data-stu-id="e5404-130">toodownload and run hello tools and scripts that are required for SAP software deployment, you must be connected toohello Internet.</span></span> <span data-ttu-id="e5404-131">Merhaba hello Gelişmiş izleme uzantısı SAP için Azure çalışan Azure VM Internet erişimi toohello da gerekir.</span><span class="sxs-lookup"><span data-stu-id="e5404-131">hello Azure VM that is running hello Azure Enhanced Monitoring Extension for SAP also needs access toohello Internet.</span></span> <span data-ttu-id="e5404-132">Bölümünde açıklandığı gibi Hello Azure VM bir Azure sanal ağı veya şirket içi etki alanının parçasıysa, hello ilgili proxy ayarlarının belirlendiğini emin olun [hello proxy yapılandırma][deployment-guide-configure-proxy].</span><span class="sxs-lookup"><span data-stu-id="e5404-132">If hello Azure VM is part of an Azure virtual network or on-premises domain, make sure that hello relevant proxy settings are set, as described in [Configure hello proxy][deployment-guide-configure-proxy].</span></span>

### <a name="microsoft-azure-subscription"></a><span data-ttu-id="e5404-133">Microsoft Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="e5404-133">Microsoft Azure subscription</span></span>
<span data-ttu-id="e5404-134">Etkin bir Azure hesabı gerekir.</span><span class="sxs-lookup"><span data-stu-id="e5404-134">You need an active Azure account.</span></span>

### <a name="topology-and-networking"></a><span data-ttu-id="e5404-135">Topoloji ve ağ iletişimi</span><span class="sxs-lookup"><span data-stu-id="e5404-135">Topology and networking</span></span>
<span data-ttu-id="e5404-136">Toodefine hello topoloji ve hello Azure SAP dağıtımının mimarisini gerekir:</span><span class="sxs-lookup"><span data-stu-id="e5404-136">You need toodefine hello topology and architecture of hello SAP deployment in Azure:</span></span>

* <span data-ttu-id="e5404-137">Azure depolama hesapları toobe kullanılan</span><span class="sxs-lookup"><span data-stu-id="e5404-137">Azure storage accounts toobe used</span></span>
* <span data-ttu-id="e5404-138">Toodeploy hello SAP sistem istediğiniz sanal ağ</span><span class="sxs-lookup"><span data-stu-id="e5404-138">Virtual network where you want toodeploy hello SAP system</span></span>
* <span data-ttu-id="e5404-139">Kaynak grubu toowhich toodeploy hello SAP sistem istiyor</span><span class="sxs-lookup"><span data-stu-id="e5404-139">Resource group toowhich you want toodeploy hello SAP system</span></span>
* <span data-ttu-id="e5404-140">Toodeploy hello SAP sistem istediğiniz azure bölgesi</span><span class="sxs-lookup"><span data-stu-id="e5404-140">Azure region where you want toodeploy hello SAP system</span></span>
* <span data-ttu-id="e5404-141">SAP yapılandırma (iki katmanlı veya üç katmanlı)</span><span class="sxs-lookup"><span data-stu-id="e5404-141">SAP configuration (two-tier or three-tier)</span></span>
* <span data-ttu-id="e5404-142">VM boyutları ve ek sanal sabit diskleri (VHD) toobe hello sayısını toohello VM'ler takılı</span><span class="sxs-lookup"><span data-stu-id="e5404-142">VM sizes and hello number of additional virtual hard disks (VHDs) toobe mounted toohello VMs</span></span>
* <span data-ttu-id="e5404-143">SAP düzeltme ve aktarım sistem (CTS) yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e5404-143">SAP Correction and Transport System (CTS) configuration</span></span>

<span data-ttu-id="e5404-144">Oluşturun ve hello SAP yazılım dağıtım işlemi başlamadan önce Azure depolama hesapları veya Azure sanal ağını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e5404-144">Create and configure Azure storage accounts or Azure virtual networks before you begin hello SAP software deployment process.</span></span> <span data-ttu-id="e5404-145">Hakkında bilgi için toocreate ve bu kaynakları yapılandırmak için bkz: [Azure sanal makineleri planlama ve uygulama için Windows üzerinde SAP][planning-guide].</span><span class="sxs-lookup"><span data-stu-id="e5404-145">For information about how toocreate and configure these resources, see [Azure Virtual Machines planning and implementation for SAP on Windows][planning-guide].</span></span>

### <a name="sap-sizing"></a><span data-ttu-id="e5404-146">SAP boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="e5404-146">SAP sizing</span></span>
<span data-ttu-id="e5404-147">SAP boyutlandırma için bilgisinden hello bildirin:</span><span class="sxs-lookup"><span data-stu-id="e5404-147">Know hello following information, for SAP sizing:</span></span>

* <span data-ttu-id="e5404-148">Merhaba SAP hızlı Boyutlandırıcı aracı ve hello SAP uygulama performans standart (SAP) numarasını kullanarak SAP iş yükü, örneğin, öngörülen</span><span class="sxs-lookup"><span data-stu-id="e5404-148">Projected SAP workload, for example, by using hello SAP Quick Sizer tool, and hello SAP Application Performance Standard (SAPS) number</span></span>
* <span data-ttu-id="e5404-149">Merhaba SAP sisteminin gerekli CPU ve bellek kaynak tüketimi</span><span class="sxs-lookup"><span data-stu-id="e5404-149">Required CPU resource and memory consumption of hello SAP system</span></span>
* <span data-ttu-id="e5404-150">Saniye başına gerekli giriş/çıkış (g/ç) işlemleri</span><span class="sxs-lookup"><span data-stu-id="e5404-150">Required input/output (I/O) operations per second</span></span>
* <span data-ttu-id="e5404-151">Azure VM'ler arasında nihai iletişimin ağ bant genişliği gerekli</span><span class="sxs-lookup"><span data-stu-id="e5404-151">Required network bandwidth of eventual communication between VMs in Azure</span></span>
* <span data-ttu-id="e5404-152">Şirket içi varlıklar ve hello Azure dağıtılan SAP sistemi arasındaki gerekli ağ bant genişliği</span><span class="sxs-lookup"><span data-stu-id="e5404-152">Required network bandwidth between on-premises assets and hello Azure-deployed SAP system</span></span>

### <a name="resource-groups"></a><span data-ttu-id="e5404-153">Kaynak grupları</span><span class="sxs-lookup"><span data-stu-id="e5404-153">Resource groups</span></span>
<span data-ttu-id="e5404-154">Azure Kaynak Yöneticisi'nde, kaynak grupları toomanage tüm hello uygulama kaynakları Azure aboneliğinizde kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5404-154">In Azure Resource Manager, you can use resource groups toomanage all hello application resources in your Azure subscription.</span></span> <span data-ttu-id="e5404-155">Daha fazla bilgi için bkz: [Azure Resource Manager'a genel bakış][resource-group-overview].</span><span class="sxs-lookup"><span data-stu-id="e5404-155">For more information, see [Azure Resource Manager overview][resource-group-overview].</span></span>

## <a name="resources"></a><span data-ttu-id="e5404-156">Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="e5404-156">Resources</span></span>

### <span data-ttu-id="e5404-157"><a name="42ee2bdb-1efc-4ec7-ab31-fe4c22769b94"></a>SAP kaynakları</span><span class="sxs-lookup"><span data-stu-id="e5404-157"><a name="42ee2bdb-1efc-4ec7-ab31-fe4c22769b94"></a>SAP resources</span></span>
<span data-ttu-id="e5404-158">SAP yazılım dağıtımınızı ayarlarken, SAP kaynakları aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="e5404-158">When you are setting up your SAP software deployment, you need hello following SAP resources:</span></span>

* <span data-ttu-id="e5404-159">SAP Not [1928533], sahip olduğu:</span><span class="sxs-lookup"><span data-stu-id="e5404-159">SAP Note [1928533], which has:</span></span>
  * <span data-ttu-id="e5404-160">SAP yazılım hello dağıtımı için desteklenen Azure VM boyutlarını listesi</span><span class="sxs-lookup"><span data-stu-id="e5404-160">List of Azure VM sizes that are supported for hello deployment of SAP software</span></span>
  * <span data-ttu-id="e5404-161">Azure VM boyutlarını önemli kapasite bilgilerini</span><span class="sxs-lookup"><span data-stu-id="e5404-161">Important capacity information for Azure VM sizes</span></span>
  * <span data-ttu-id="e5404-162">Desteklenen bir SAP yazılım ve işletim sistemi (OS) ve veritabanı birleşimler</span><span class="sxs-lookup"><span data-stu-id="e5404-162">Supported SAP software, and operating system (OS) and database combinations</span></span>
  * <span data-ttu-id="e5404-163">Windows ve Microsoft Azure Linux için gerekli SAP çekirdek sürümü</span><span class="sxs-lookup"><span data-stu-id="e5404-163">Required SAP kernel version for Windows and Linux on Microsoft Azure</span></span>

* <span data-ttu-id="e5404-164">SAP Not [2015553] azure'da SAP desteklenen SAP yazılım dağıtımları için önkoşulları listeler.</span><span class="sxs-lookup"><span data-stu-id="e5404-164">SAP Note [2015553] lists prerequisites for SAP-supported SAP software deployments in Azure.</span></span>
* <span data-ttu-id="e5404-165">SAP Not [2178632] ayrıntılı Azure SAP için bildirilen tüm izleme ölçümleri hakkında bilgi sağlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="e5404-165">SAP Note [2178632] has detailed information about all monitoring metrics reported for SAP in Azure.</span></span>
* <span data-ttu-id="e5404-166">SAP Not [1409604] hello SAP konak Aracısı Windows Azure için gereken sürümü vardır.</span><span class="sxs-lookup"><span data-stu-id="e5404-166">SAP Note [1409604] has hello required SAP Host Agent version for Windows in Azure.</span></span>
* <span data-ttu-id="e5404-167">SAP Not [2191498] hello Azure Linux için SAP konak Aracısı sürümünü istedi.</span><span class="sxs-lookup"><span data-stu-id="e5404-167">SAP Note [2191498] has hello required SAP Host Agent version for Linux in Azure.</span></span>
* <span data-ttu-id="e5404-168">SAP Not [2243692] Linux Azure üzerinde SAP lisanslama hakkında bilgi vardır.</span><span class="sxs-lookup"><span data-stu-id="e5404-168">SAP Note [2243692] has information about SAP licensing on Linux in Azure.</span></span>
* <span data-ttu-id="e5404-169">SAP Not [1984787] SUSE Linux Enterprise Server 12 hakkında genel bilgi yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="e5404-169">SAP Note [1984787] has general information about SUSE Linux Enterprise Server 12.</span></span>
* <span data-ttu-id="e5404-170">SAP Not [2002167] Red Hat Enterprise Linux ilgili genel bilgilerin 7.x.</span><span class="sxs-lookup"><span data-stu-id="e5404-170">SAP Note [2002167] has general information about Red Hat Enterprise Linux 7.x.</span></span>
* <span data-ttu-id="e5404-171">SAP Not [1999351] hello Azure Gelişmiş izleme uzantısı SAP için ek sorun giderme bilgileri içeriyor.</span><span class="sxs-lookup"><span data-stu-id="e5404-171">SAP Note [1999351] has additional troubleshooting information for hello Azure Enhanced Monitoring Extension for SAP.</span></span>
* <span data-ttu-id="e5404-172">[SAP topluluk WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) SAP notları Linux için gerekli tüm sahiptir.</span><span class="sxs-lookup"><span data-stu-id="e5404-172">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) has all required SAP Notes for Linux.</span></span>
* <span data-ttu-id="e5404-173">Parçası olan SAP özgü PowerShell cmdlet'leri [Azure PowerShell][azure-ps].</span><span class="sxs-lookup"><span data-stu-id="e5404-173">SAP-specific PowerShell cmdlets that are part of [Azure PowerShell][azure-ps].</span></span>
* <span data-ttu-id="e5404-174">Parçası olan SAP özgü Azure CLI komutları [Azure CLI][azure-cli].</span><span class="sxs-lookup"><span data-stu-id="e5404-174">SAP-specific Azure CLI commands that are part of [Azure CLI][azure-cli].</span></span>

[comment]: <> (SAP Not 1409604 SAP konak aracı için MSSedusch Yapılacaklar eklemek ARM düzeltme eki düzeyi)

### <a name="microsoft-resources"></a><span data-ttu-id="e5404-176">Microsoft kaynakları</span><span class="sxs-lookup"><span data-stu-id="e5404-176">Microsoft resources</span></span>
<span data-ttu-id="e5404-177">Bu Microsoft makaleler Azure SAP dağıtımlarda kapsar:</span><span class="sxs-lookup"><span data-stu-id="e5404-177">These Microsoft articles cover SAP deployments in Azure:</span></span>

* <span data-ttu-id="e5404-178">[Azure sanal makineleri planlama ve uygulama Windows üzerinde SAP için][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="e5404-178">[Azure Virtual Machines planning and implementation for SAP on Windows][planning-guide]</span></span>
* <span data-ttu-id="e5404-179">[Windows (Bu makalede) SAP için Azure sanal makineler dağıtımı][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="e5404-179">[Azure Virtual Machines deployment for SAP on Windows (this article)][deployment-guide]</span></span>
* <span data-ttu-id="e5404-180">[SAP Windows için Azure sanal makineleri DBMS dağıtımı][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="e5404-180">[Azure Virtual Machines DBMS deployment for SAP on Windows][dbms-guide]</span></span>
* <span data-ttu-id="e5404-181">[Azure portalı][azure-portal]</span><span class="sxs-lookup"><span data-stu-id="e5404-181">[Azure portal][azure-portal]</span></span>

## <span data-ttu-id="e5404-182"><a name="b3253ee3-d63b-4d74-a49b-185e76c4088e"></a>Azure vm'lerinde SAP yazılım için dağıtım senaryoları</span><span class="sxs-lookup"><span data-stu-id="e5404-182"><a name="b3253ee3-d63b-4d74-a49b-185e76c4088e"></a>Deployment scenarios for SAP software on Azure VMs</span></span>
<span data-ttu-id="e5404-183">Sanal makineleri ve ilişkili diskler azure'da dağıtmak için birçok seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="e5404-183">You have multiple options for deploying VMs and associated disks in Azure.</span></span> <span data-ttu-id="e5404-184">Vm'leriniz seçtiğiniz hello dağıtım türüne göre dağıtım için farklı adımlar tooprepare sürebilir dağıtım seçenekleri arasındaki önemli toounderstand hello farklar demektir.</span><span class="sxs-lookup"><span data-stu-id="e5404-184">It's important toounderstand hello differences between deployment options, because you might take different steps tooprepare your VMs for deployment based on hello deployment type you choose.</span></span>

### <span data-ttu-id="e5404-185"><a name="db477013-9060-4602-9ad4-b0316f8bb281"></a>Senaryo 1: hello SAP için Azure Marketi VM'den dağıtma</span><span class="sxs-lookup"><span data-stu-id="e5404-185"><a name="db477013-9060-4602-9ad4-b0316f8bb281"></a>Scenario 1: Deploying a VM from hello Azure Marketplace for SAP</span></span>
<span data-ttu-id="e5404-186">Microsoft tarafından sağlanan bir görüntüyü kullanabilir ya da üçüncü hello Azure Marketi toodeploy VM göre taraf.</span><span class="sxs-lookup"><span data-stu-id="e5404-186">You can use an image provided by Microsoft or by a third party in hello Azure Marketplace toodeploy your VM.</span></span> <span data-ttu-id="e5404-187">bazı standart bir işletim sistemi görüntüleri Windows Server ve farklı Linux dağıtımları Hello Market sunar.</span><span class="sxs-lookup"><span data-stu-id="e5404-187">hello Marketplace offers some standard OS images of Windows Server and different Linux distributions.</span></span> <span data-ttu-id="e5404-188">Ayrıca, veritabanı yönetimi içeren bir görüntü dağıtabilirsiniz sistemi (DBMS) SKU'ları, örneğin, Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e5404-188">You also can deploy an image that includes database management system (DBMS) SKUs, for example, Microsoft SQL Server.</span></span> <span data-ttu-id="e5404-189">Görüntüleri DBMS SKU'ları ile kullanma hakkında daha fazla bilgi için bkz: [Linux üzerinde SAP için Azure sanal makineleri DBMS dağıtım][dbms-guide].</span><span class="sxs-lookup"><span data-stu-id="e5404-189">For more information about using images with DBMS SKUs, see [Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide].</span></span>

<span data-ttu-id="e5404-190">Merhaba aşağıdaki akış çizelgesi hello SAP özgü hello Azure Marketi VM'den dağıtma adımları sırasını göstermektedir:</span><span class="sxs-lookup"><span data-stu-id="e5404-190">hello following flowchart shows hello SAP-specific sequence of steps for deploying a VM from hello Azure Marketplace:</span></span>

![VM dağıtımı için bir VM hello Azure Market görüntüsünden kullanarak SAP sistemleri akış çizelgesi][deployment-guide-figure-100]

#### <a name="create-a-virtual-machine-by-using-hello-azure-portal"></a><span data-ttu-id="e5404-192">Hello Azure portal kullanarak bir sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="e5404-192">Create a virtual machine by using hello Azure portal</span></span>
<span data-ttu-id="e5404-193">Merhaba en kolay yolu toocreate hello Azure Marketi görüntüden yeni bir sanal makineyle hello Azure portal kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="e5404-193">hello easiest way toocreate a new virtual machine with an image from hello Azure Marketplace is by using hello Azure portal.</span></span>

1.  <span data-ttu-id="e5404-194">Çok Git<https://portal.azure.com/#create>.</span><span class="sxs-lookup"><span data-stu-id="e5404-194">Go too<https://portal.azure.com/#create>.</span></span>  <span data-ttu-id="e5404-195">Veya hello Azure portalı menüsünde, seçin **+ yeni**.</span><span class="sxs-lookup"><span data-stu-id="e5404-195">Or, in hello Azure portal menu, select **+ New**.</span></span>
2.  <span data-ttu-id="e5404-196">Seçin **işlem**ve ardından işletim sistemi toodeploy istediğiniz hello türünü seçin.</span><span class="sxs-lookup"><span data-stu-id="e5404-196">Select **Compute**, and then select hello type of operating system you want toodeploy.</span></span> <span data-ttu-id="e5404-197">Örneğin, Windows Server 2012 R2, SUSE Linux Enterprise Server 12 (SLES 12) veya Red Hat Enterprise Linux 7.2 (RHEL 7.2).</span><span class="sxs-lookup"><span data-stu-id="e5404-197">For example, Windows Server 2012 R2, SUSE Linux Enterprise Server 12 (SLES 12), or Red Hat Enterprise Linux 7.2 (RHEL 7.2).</span></span> <span data-ttu-id="e5404-198">Merhaba varsayılan liste görünümü, tüm desteklenen işletim sistemlerini göstermez.</span><span class="sxs-lookup"><span data-stu-id="e5404-198">hello default list view does not show all supported operating systems.</span></span> <span data-ttu-id="e5404-199">Seçin **tümünü görmek** tam listesi için.</span><span class="sxs-lookup"><span data-stu-id="e5404-199">Select **see all** for a full list.</span></span> <span data-ttu-id="e5404-200">SAP yazılım dağıtımı için desteklenen işletim sistemleri hakkında daha fazla bilgi için bkz. SAP Not [1928533].</span><span class="sxs-lookup"><span data-stu-id="e5404-200">For more information about supported operating systems for SAP software deployment, see SAP Note [1928533].</span></span>
3.  <span data-ttu-id="e5404-201">Merhaba sonraki sayfada, hüküm ve koşulları gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="e5404-201">On hello next page, review terms and conditions.</span></span>
4.  <span data-ttu-id="e5404-202">Merhaba, **dağıtım modeli seçin** kutusunda, seçin **Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="e5404-202">In hello **Select a deployment model** box, select **Resource Manager**.</span></span>
5.  <span data-ttu-id="e5404-203">**Oluştur**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="e5404-203">Select **Create**.</span></span>

<span data-ttu-id="e5404-204">Başlangıç Sihirbazı, gerekli hello parametreleri toocreate hello sanal makine boyunca size yol gösterir, ayrıca ağ arabirimleri ve depolama hesapları gibi kaynaklara tooall gerekli.</span><span class="sxs-lookup"><span data-stu-id="e5404-204">hello wizard guides you through setting hello required parameters toocreate hello virtual machine, in addition tooall required resources, like network interfaces and storage accounts.</span></span> <span data-ttu-id="e5404-205">Bu parametreler bazıları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="e5404-205">Some of these parameters are:</span></span>

1. <span data-ttu-id="e5404-206">**Temel kavramları**:</span><span class="sxs-lookup"><span data-stu-id="e5404-206">**Basics**:</span></span>
  * <span data-ttu-id="e5404-207">**Ad**: hello kaynağın (Merhaba sanal makine adı) hello adı.</span><span class="sxs-lookup"><span data-stu-id="e5404-207">**Name**: hello name of hello resource (hello virtual machine name).</span></span>
 * <span data-ttu-id="e5404-208">**Kullanıcı adı ve parola** veya **SSH ortak anahtarını**: hello kullanıcı hello sağlama işlemi sırasında oluşturulan hello kullanıcı adını ve parolasını girin.</span><span class="sxs-lookup"><span data-stu-id="e5404-208">**Username and password** or **SSH public key**: Enter hello username and password of hello user that is created during hello provisioning.</span></span> <span data-ttu-id="e5404-209">Bir Linux sanal makine için toohello makinede toosign kullanmak hello genel güvenli Kabuk (SSH) anahtarını girebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5404-209">For a Linux virtual machine, you can enter hello public Secure Shell (SSH) key that you use toosign in toohello machine.</span></span>
 * <span data-ttu-id="e5404-210">**Abonelik**: hello abonelik toouse tooprovision hello yeni sanal makine istediğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="e5404-210">**Subscription**: Select hello subscription that you want toouse tooprovision hello new virtual machine.</span></span>
 * <span data-ttu-id="e5404-211">**Kaynak grubu**: hello VM hello kaynak grubunun hello adı.</span><span class="sxs-lookup"><span data-stu-id="e5404-211">**Resource group**: hello name of hello resource group for hello VM.</span></span> <span data-ttu-id="e5404-212">Yeni kaynak grubu veya hello adını zaten bir kaynak grubu ya da hello adını girebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5404-212">You can enter either hello name of a new resource group or hello name of a resource group that already exists.</span></span>
 * <span data-ttu-id="e5404-213">**Konum**: Burada toodeploy hello yeni bir sanal makine.</span><span class="sxs-lookup"><span data-stu-id="e5404-213">**Location**: Where toodeploy hello new virtual machine.</span></span> <span data-ttu-id="e5404-214">Tooconnect hello sanal makine tooyour şirket içi ağ istiyorsanız, Azure tooyour şirket içi ağ bağlanan sanal ağ hello hello konumu seçtiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="e5404-214">If you want tooconnect hello virtual machine tooyour on-premises network, make sure you select hello location of hello virtual network that connects Azure tooyour on-premises network.</span></span> <span data-ttu-id="e5404-215">Daha fazla bilgi için bkz: [Microsoft Azure ağ] [ planning-guide-microsoft-azure-networking] içinde [Azure sanal makineleri planlama ve uygulama Linux üzerinde SAP için] [ planning-guide].</span><span class="sxs-lookup"><span data-stu-id="e5404-215">For more information, see [Microsoft Azure networking][planning-guide-microsoft-azure-networking] in [Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide].</span></span>
2. <span data-ttu-id="e5404-216">**Boyutu**:</span><span class="sxs-lookup"><span data-stu-id="e5404-216">**Size**:</span></span>

     <span data-ttu-id="e5404-217">Desteklenen VM türlerinin listesi için bkz. SAP Not [1928533].</span><span class="sxs-lookup"><span data-stu-id="e5404-217">For a list of supported VM types, see SAP Note [1928533].</span></span> <span data-ttu-id="e5404-218">Toouse Azure Premium Storage istiyorsanız hello doğru VM türü seçtiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="e5404-218">Be sure you select hello correct VM type if you want toouse Azure Premium Storage.</span></span> <span data-ttu-id="e5404-219">Premium depolama tüm VM türleri desteklemez.</span><span class="sxs-lookup"><span data-stu-id="e5404-219">Not all VM types support Premium Storage.</span></span> <span data-ttu-id="e5404-220">Daha fazla bilgi için bkz: [Depolama: Microsoft Azure depolama ve veri diskleri] [ planning-guide-storage-microsoft-azure-storage-and-data-disks] ve [Azure Premium Storage] [ planning-guide-azure-premium-storage] içinde [ Azure sanal makineleri planlama ve uygulama Linux üzerinde SAP için][planning-guide].</span><span class="sxs-lookup"><span data-stu-id="e5404-220">For more information, see [Storage: Microsoft Azure Storage and data disks][planning-guide-storage-microsoft-azure-storage-and-data-disks] and [Azure Premium Storage][planning-guide-azure-premium-storage] in [Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide].</span></span>

3. <span data-ttu-id="e5404-221">**Ayarları**:</span><span class="sxs-lookup"><span data-stu-id="e5404-221">**Settings**:</span></span>
   * <span data-ttu-id="e5404-222">**Depolama hesabı**: mevcut bir depolama hesabını seçin veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e5404-222">**Storage account**: Select an existing storage account or create a new one.</span></span> <span data-ttu-id="e5404-223">Tüm depolama türlerini, SAP uygulamaları çalıştırmak için çalışır.</span><span class="sxs-lookup"><span data-stu-id="e5404-223">Not all storage types work for running SAP applications.</span></span> <span data-ttu-id="e5404-224">Depolama türleri hakkında daha fazla bilgi için bkz: [Microsoft Azure depolama] [ dbms-guide-2.3] içinde [Linux üzerinde SAP için Azure sanal makineleri DBMS dağıtım] [ dbms-guide].</span><span class="sxs-lookup"><span data-stu-id="e5404-224">For more information about storage types, see [Microsoft Azure Storage][dbms-guide-2.3] in [Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide].</span></span>
   * <span data-ttu-id="e5404-225">**Sanal ağ** ve **alt**: bağlı tooyour şirket içi ağ select hello sanal ağ intranetinize ile toointegrate hello sanal makine.</span><span class="sxs-lookup"><span data-stu-id="e5404-225">**Virtual network** and **Subnet**: toointegrate hello virtual machine with your intranet, select hello virtual network that is connected tooyour on-premises network.</span></span>
   * <span data-ttu-id="e5404-226">**Genel IP adresi**: toouse istediğiniz veya parametreleri toocreate yeni bir ortak IP adresi girin hello genel IP adresi seçin.</span><span class="sxs-lookup"><span data-stu-id="e5404-226">**Public IP address**: Select hello public IP address that you want toouse, or enter parameters toocreate a new public IP address.</span></span> <span data-ttu-id="e5404-227">Bir ortak IP adresi tooaccess hello Internet sanal makineniz kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5404-227">You can use a public IP address tooaccess your virtual machine over hello Internet.</span></span> <span data-ttu-id="e5404-228">Bir ağ güvenlik grubu toohelp güvenli erişim tooyour sanal makine de oluşturduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="e5404-228">Make sure that you also create a network security group toohelp secure access tooyour virtual machine.</span></span>
   * <span data-ttu-id="e5404-229">**Ağ güvenlik grubu**: daha fazla bilgi için bkz: [kontrol ağ trafiği akışını ağ güvenlik gruplarıyla][virtual-networks-nsg].</span><span class="sxs-lookup"><span data-stu-id="e5404-229">**Network security group**: For more information, see [Control network traffic flow with network security groups][virtual-networks-nsg].</span></span>
   * <span data-ttu-id="e5404-230">**Kullanılabilirlik**: bir kullanılabilirlik kümesi seçin veya hello parametreleri toocreate yeni bir kullanılabilirlik girin ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e5404-230">**Availability**: Select an availability set, or enter hello parameters toocreate a new availability set.</span></span> <span data-ttu-id="e5404-231">Daha fazla bilgi için bkz: [Azure kullanılabilirlik kümeleri][planning-guide-3.2.3].</span><span class="sxs-lookup"><span data-stu-id="e5404-231">For more information, see [Azure availability sets][planning-guide-3.2.3].</span></span>
   * <span data-ttu-id="e5404-232">**İzleme**: seçebileceğiniz **devre dışı** Tanılama izleme.</span><span class="sxs-lookup"><span data-stu-id="e5404-232">**Monitoring**: You can select **Disable** for monitoring diagnostics.</span></span> <span data-ttu-id="e5404-233">Merhaba komutları tooenable hello Monitoring Azure Gelişmiş uzantısı ile çalıştırdığınızda otomatik olarak açıklandığı gibi etkinleştirilir [yapılandırma izleme][deployment-guide-configure-monitoring-scenario-1].</span><span class="sxs-lookup"><span data-stu-id="e5404-233">It is enabled automatically when you run hello commands tooenable hello Azure Enhanced Monitoring Extension, as described in [Configure monitoring][deployment-guide-configure-monitoring-scenario-1].</span></span>

4. <span data-ttu-id="e5404-234">**Özet**:</span><span class="sxs-lookup"><span data-stu-id="e5404-234">**Summary**:</span></span>

  <span data-ttu-id="e5404-235">Seçimlerinizi gözden geçirin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="e5404-235">Review your selections, and then select **OK**.</span></span>

<span data-ttu-id="e5404-236">Sanal makineniz seçtiğiniz hello kaynak grubunda dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="e5404-236">Your virtual machine is deployed in hello resource group you selected.</span></span>

#### <a name="create-a-virtual-machine-by-using-a-template"></a><span data-ttu-id="e5404-237">Bir şablonu kullanarak bir sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="e5404-237">Create a virtual machine by using a template</span></span>
<span data-ttu-id="e5404-238">Hello yayımlanan hello SAP şablonlarından birini kullanarak bir sanal makine oluşturabilirsiniz [azure hızlı başlangıç şablonlarını GitHub deposunu][azure-quickstart-templates-github].</span><span class="sxs-lookup"><span data-stu-id="e5404-238">You can create a virtual machine by using one of hello SAP templates published in hello [azure-quickstart-templates GitHub repository][azure-quickstart-templates-github].</span></span> <span data-ttu-id="e5404-239">Ayrıca el ile bir sanal makine hello kullanarak oluşturabileceğiniz [Azure portal][virtual-machines-windows-tutorial], [PowerShell][virtual-machines-ps-create-preconfigure-windows-resource-manager-vms], veya [Azure CLI ][virtual-machines-linux-tutorial].</span><span class="sxs-lookup"><span data-stu-id="e5404-239">You also can manually create a virtual machine by using hello [Azure portal][virtual-machines-windows-tutorial], [PowerShell][virtual-machines-ps-create-preconfigure-windows-resource-manager-vms], or [Azure CLI][virtual-machines-linux-tutorial].</span></span>

* <span data-ttu-id="e5404-240">[**İki katmanlı yapılandırma (yalnızca bir sanal makine) şablonu** (sap-2-katman-Market-görüntü)][sap-templates-2-tier-marketplace-image]</span><span class="sxs-lookup"><span data-stu-id="e5404-240">[**Two-tier configuration (only one virtual machine) template** (sap-2-tier-marketplace-image)][sap-templates-2-tier-marketplace-image]</span></span>

  <span data-ttu-id="e5404-241">toocreate yalnızca bir sanal makine kullanarak iki katmanlı sistem bu şablonu kullanın.</span><span class="sxs-lookup"><span data-stu-id="e5404-241">toocreate a two-tier system by using only one virtual machine, use this template.</span></span>
* <span data-ttu-id="e5404-242">[**Üç katmanlı yapılandırma (birden çok sanal makine) şablonu** (sap-3-katman-Market-görüntü)][sap-templates-3-tier-marketplace-image]</span><span class="sxs-lookup"><span data-stu-id="e5404-242">[**Three-tier configuration (multiple virtual machines) template** (sap-3-tier-marketplace-image)][sap-templates-3-tier-marketplace-image]</span></span>

  <span data-ttu-id="e5404-243">toocreate kullanarak birden çok sanal makine, bir üç katmanlı sistem bu şablonu kullanın.</span><span class="sxs-lookup"><span data-stu-id="e5404-243">toocreate a three-tier system by using multiple virtual machines, use this template.</span></span>

<span data-ttu-id="e5404-244">Hello Azure portalı, şu parametreler hello şablonunun hello girin:</span><span class="sxs-lookup"><span data-stu-id="e5404-244">In hello Azure portal, enter hello following parameters for hello template:</span></span>

1. <span data-ttu-id="e5404-245">**Temel kavramları**:</span><span class="sxs-lookup"><span data-stu-id="e5404-245">**Basics**:</span></span>
  * <span data-ttu-id="e5404-246">**Abonelik**: hello abonelik toouse toodeploy hello şablonu.</span><span class="sxs-lookup"><span data-stu-id="e5404-246">**Subscription**: hello subscription toouse toodeploy hello template.</span></span>
  * <span data-ttu-id="e5404-247">**Kaynak grubu**: hello kaynak grubu toouse toodeploy hello şablonu.</span><span class="sxs-lookup"><span data-stu-id="e5404-247">**Resource group**: hello resource group toouse toodeploy hello template.</span></span> <span data-ttu-id="e5404-248">Yeni bir kaynak grubu oluşturabilir veya varolan bir kaynak grubu hello abonelikte seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5404-248">You can create a new resource group, or you can select an existing resource group in hello subscription.</span></span>
  * <span data-ttu-id="e5404-249">**Konum**: Burada toodeploy hello şablonu.</span><span class="sxs-lookup"><span data-stu-id="e5404-249">**Location**: Where toodeploy hello template.</span></span> <span data-ttu-id="e5404-250">Varolan bir kaynak grubu seçtiyseniz, bu kaynak grubunun hello konumu kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e5404-250">If you selected an existing resource group, hello location of that resource group is used.</span></span>

2. <span data-ttu-id="e5404-251">**Ayarları**:</span><span class="sxs-lookup"><span data-stu-id="e5404-251">**Settings**:</span></span>
  * <span data-ttu-id="e5404-252">**SAP sistem kimliği**: Merhaba SAP sistem kimliği (SID).</span><span class="sxs-lookup"><span data-stu-id="e5404-252">**SAP System ID**: hello SAP System ID (SID).</span></span>
  * <span data-ttu-id="e5404-253">**İşletim sistemi türü**: Merhaba örneğin toodeploy, istediğiniz işletim sistemi, Windows Server 2012 R2, SUSE Linux Enterprise Server 12 (SLES 12) veya Red Hat Enterprise Linux 7.2 (RHEL 7.2).</span><span class="sxs-lookup"><span data-stu-id="e5404-253">**OS type**: hello operating system you want toodeploy, for example, Windows Server 2012 R2, SUSE Linux Enterprise Server 12 (SLES 12), or Red Hat Enterprise Linux 7.2 (RHEL 7.2).</span></span>

    <span data-ttu-id="e5404-254">Merhaba varsayılan liste görünümü, tüm desteklenen işletim sistemlerini göstermez.</span><span class="sxs-lookup"><span data-stu-id="e5404-254">hello default list view does not show all supported operating systems.</span></span> <span data-ttu-id="e5404-255">Seçin **tümünü görmek** tam listesi için.</span><span class="sxs-lookup"><span data-stu-id="e5404-255">Select **see all** for a full list.</span></span> <span data-ttu-id="e5404-256">SAP yazılım dağıtımı için desteklenen işletim sistemleri hakkında daha fazla bilgi için bkz. SAP Not [1928533].</span><span class="sxs-lookup"><span data-stu-id="e5404-256">For more information about supported operating systems for SAP software deployment, see SAP Note [1928533].</span></span>
  * <span data-ttu-id="e5404-257">**SAP sistem boyutu**: Merhaba hello SAP sistem boyutu.</span><span class="sxs-lookup"><span data-stu-id="e5404-257">**SAP system size**: hello size of hello SAP system.</span></span>

    <span data-ttu-id="e5404-258">SAP hello yeni sistem Hello sayısını sağlar.</span><span class="sxs-lookup"><span data-stu-id="e5404-258">hello number of SAPS hello new system provides.</span></span> <span data-ttu-id="e5404-259">Kaç tane SAP hello sistemi gerektirir emin değilseniz, SAP teknolojisi iş ortağı veya sistem Tümleştirici isteyin.</span><span class="sxs-lookup"><span data-stu-id="e5404-259">If you are not sure how many SAPS hello system requires, ask your SAP Technology Partner or System Integrator.</span></span>
  * <span data-ttu-id="e5404-260">**Sistem kullanılabilirliğini** (yalnızca üç katmanlı şablon): Merhaba sistem kullanılabilirlik.</span><span class="sxs-lookup"><span data-stu-id="e5404-260">**System availability** (three-tier template only): hello system availability.</span></span>

    <span data-ttu-id="e5404-261">Seçin **HA** yüksek kullanılabilirlik yüklemesi için uygun bir yapılandırma için.</span><span class="sxs-lookup"><span data-stu-id="e5404-261">Select **HA** for a configuration that is suitable for a high-availability installation.</span></span> <span data-ttu-id="e5404-262">İki veritabanı sunucuları ve iki sunucu için ABAP SAP merkezi Hizmetleri (ASCS) oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e5404-262">Two database servers and two servers for ABAP SAP Central Services (ASCS) are created.</span></span>
  * <span data-ttu-id="e5404-263">**Depolama türü** (yalnızca iki katmanlı şablon): Merhaba depolama toouse türü.</span><span class="sxs-lookup"><span data-stu-id="e5404-263">**Storage type** (two-tier template only): hello type of storage toouse.</span></span>

    <span data-ttu-id="e5404-264">Daha büyük sistemler için yüksek oranda Azure Premium Storage kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="e5404-264">For larger systems, we highly recommend using Azure Premium Storage.</span></span> <span data-ttu-id="e5404-265">Depolama türleri hakkında daha fazla bilgi için şu kaynaklara bakın:</span><span class="sxs-lookup"><span data-stu-id="e5404-265">For more information about storage types, see these resources:</span></span>
      * <span data-ttu-id="e5404-266">[SAP DBMS örneği için Azure Premium SSD depolama kullanımı][2367194]</span><span class="sxs-lookup"><span data-stu-id="e5404-266">[Use of Azure Premium SSD Storage for SAP DBMS Instance][2367194]</span></span>
      * <span data-ttu-id="e5404-267">[Microsoft Azure depolama] [ dbms-guide-2.3] içinde [Linux üzerinde SAP için Azure sanal makineleri DBMS dağıtımı][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="e5404-267">[Microsoft Azure Storage][dbms-guide-2.3] in [Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide]</span></span>
      * <span data-ttu-id="e5404-268">[Premium Storage: Azure sanal makine iş yükleri için yüksek performanslı depolama][storage-premium-storage-preview-portal]</span><span class="sxs-lookup"><span data-stu-id="e5404-268">[Premium Storage: High-performance storage for Azure Virtual Machine workloads][storage-premium-storage-preview-portal]</span></span>
      * <span data-ttu-id="e5404-269">[Giriş tooMicrosoft Azure depolama][storage-introduction]</span><span class="sxs-lookup"><span data-stu-id="e5404-269">[Introduction tooMicrosoft Azure Storage][storage-introduction]</span></span>
  * <span data-ttu-id="e5404-270">**Yönetici kullanıcı adı** ve **yönetici parolası**: bir kullanıcı adı ve parola.</span><span class="sxs-lookup"><span data-stu-id="e5404-270">**Admin username** and **Admin password**: A username and password.</span></span>
    <span data-ttu-id="e5404-271">Yeni bir kullanıcı, toohello sanal makinede imzalamak için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e5404-271">A new user is created, for signing in toohello virtual machine.</span></span>
  * <span data-ttu-id="e5404-272">**Yeni veya var olan bir alt ağ**: yeni bir sanal ağ ve alt ağ oluşturulur veya mevcut bir alt kullanılan belirler.</span><span class="sxs-lookup"><span data-stu-id="e5404-272">**New or existing subnet**: Determines whether a new virtual network and subnet are  created or an existing subnet is used.</span></span> <span data-ttu-id="e5404-273">Bağlı tooyour şirket içi ağ bir sanal ağ zaten varsa, seçin **varolan**.</span><span class="sxs-lookup"><span data-stu-id="e5404-273">If you already have a virtual network that is connected tooyour on-premises network, select **Existing**.</span></span>
  * <span data-ttu-id="e5404-274">**Alt ağ kimliği**: hello kimliği hello alt hello sanal makinelerin bağlanması için.</span><span class="sxs-lookup"><span data-stu-id="e5404-274">**Subnet ID**: hello ID of hello subnet hello virtual machines will connect to.</span></span> <span data-ttu-id="e5404-275">Sanal özel ağ (VPN) veya Azure ExpressRoute sanal ağ toouse tooconnect hello sanal makine tooyour şirket içi ağın Hello alt ağ seçin.</span><span class="sxs-lookup"><span data-stu-id="e5404-275">Select hello subnet of your virtual private network (VPN) or Azure ExpressRoute virtual network toouse tooconnect hello virtual machine tooyour on-premises network.</span></span> <span data-ttu-id="e5404-276">Merhaba kimliği genellikle şu şekilde görünür: /subscriptions/&lt;abonelik kimliği > /resourceGroups/&lt;kaynak grubu adı > /providers/Microsoft.Network/virtualNetworks/&lt;sanal ağ adı > /subnets/&lt;alt ağ adı ></span><span class="sxs-lookup"><span data-stu-id="e5404-276">hello ID usually looks like this: /subscriptions/&lt;subscription id>/resourceGroups/&lt;resource group name>/providers/Microsoft.Network/virtualNetworks/&lt;virtual network name>/subnets/&lt;subnet name></span></span>

3. <span data-ttu-id="e5404-277">**Hüküm ve koşullar**:</span><span class="sxs-lookup"><span data-stu-id="e5404-277">**Terms and conditions**:</span></span>  
    <span data-ttu-id="e5404-278">Gözden geçirin ve hello yasal koşulları kabul edin.</span><span class="sxs-lookup"><span data-stu-id="e5404-278">Review and accept hello legal terms.</span></span>

4.  <span data-ttu-id="e5404-279">Seçin **satın alma**.</span><span class="sxs-lookup"><span data-stu-id="e5404-279">Select **Purchase**.</span></span>

<span data-ttu-id="e5404-280">hello Azure Marketi görüntüden kullandığınızda hello Azure VM Aracısı varsayılan olarak dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="e5404-280">hello Azure VM Agent is deployed by default when you use an image from hello Azure Marketplace.</span></span>

#### <a name="configure-proxy-settings"></a><span data-ttu-id="e5404-281">Proxy ayarlarını yapılandır</span><span class="sxs-lookup"><span data-stu-id="e5404-281">Configure proxy settings</span></span>
<span data-ttu-id="e5404-282">Şirket içi ağınıza nasıl yapılandırıldığına bağlı olarak, VM hello proxy yukarı tooset gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="e5404-282">Depending on how your on-premises network is configured, you might need tooset up hello proxy on your VM.</span></span> <span data-ttu-id="e5404-283">VM bağlı tooyour şirket içi ağ VPN ya da ExpressRoute aracılığıyla ise, hello VM değil mümkün tooaccess hello Internet olması ve olmaz mümkün toodownload gerekli hello uzantıları veya izleme verilerini topla.</span><span class="sxs-lookup"><span data-stu-id="e5404-283">If your VM is connected tooyour on-premises network via VPN or ExpressRoute, hello VM might not be able tooaccess hello Internet, and won't be able toodownload hello required extensions or collect monitoring data.</span></span> <span data-ttu-id="e5404-284">Daha fazla bilgi için bkz: [hello proxy yapılandırma][deployment-guide-configure-proxy].</span><span class="sxs-lookup"><span data-stu-id="e5404-284">For more information, see [Configure hello proxy][deployment-guide-configure-proxy].</span></span>

#### <a name="join-a-domain-windows-only"></a><span data-ttu-id="e5404-285">(Yalnızca Windows) etki alanına Katıl</span><span class="sxs-lookup"><span data-stu-id="e5404-285">Join a domain (Windows only)</span></span>
<span data-ttu-id="e5404-286">Azure dağıtımınıza bağlı tooan şirket içi Active Directory veya DNS bir Azure siteden siteye VPN bağlantısı veya ExpressRoute aracılığıyla örneğiyse (Bu adlı *şirketler arası* içinde [Azure sanal makineleri planlama ve Linux üzerinde SAP uygulamasını][planning-guide]), o hello VM bir şirket içi etki alanına katılma beklenir.</span><span class="sxs-lookup"><span data-stu-id="e5404-286">If your Azure deployment is connected tooan on-premises Active Directory or DNS instance via an Azure site-to-site VPN connection or ExpressRoute (this is called *cross-premises* in [Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]), it is expected that hello VM is joining an on-premises domain.</span></span> <span data-ttu-id="e5404-287">Bu görev için konuları hakkında daha fazla bilgi için bkz: [VM tooan şirket içi etki alanına (yalnızca Windows) katılma][deployment-guide-4.3].</span><span class="sxs-lookup"><span data-stu-id="e5404-287">For more information about considerations for this task, see [Join a VM tooan on-premises domain (Windows only)][deployment-guide-4.3].</span></span>

#### <span data-ttu-id="e5404-288"><a name="ec323ac3-1de9-4c3a-b770-4ff701def65b"></a>İzlemeyi Yapılandır</span><span class="sxs-lookup"><span data-stu-id="e5404-288"><a name="ec323ac3-1de9-4c3a-b770-4ff701def65b"></a>Configure monitoring</span></span>
<span data-ttu-id="e5404-289">ortamınızı açıklandığı gibi hello Azure Monitoring uzantısı SAP için ayarlamak SAP desteklediğinden emin toobe [yapılandırma hello Azure Gelişmiş izleme uzantısı SAP][deployment-guide-4.5].</span><span class="sxs-lookup"><span data-stu-id="e5404-289">toobe sure your environment supports SAP, set up hello Azure Monitoring Extension for SAP as described in [Configure hello Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span> <span data-ttu-id="e5404-290">SAP izleme ve gerekli en düşük sürümlerinde SAP çekirdek ve SAP konak Aracısı, listelenen hello kaynakları Hello önkoşullarını denetlemek [SAP kaynakları][deployment-guide-2.2].</span><span class="sxs-lookup"><span data-stu-id="e5404-290">Check hello prerequisites for SAP monitoring, and required minimum versions of SAP Kernel and SAP Host Agent, in hello resources listed in [SAP resources][deployment-guide-2.2].</span></span>

#### <a name="monitoring-check"></a><span data-ttu-id="e5404-291">Onay izleme</span><span class="sxs-lookup"><span data-stu-id="e5404-291">Monitoring check</span></span>
<span data-ttu-id="e5404-292">İzleme çalışıp çalışmadığını, açıklandığı gibi denetleyin [denetler ve uçtan uca izleme ayarlamak için sorun giderme][deployment-guide-troubleshooting-chapter].</span><span class="sxs-lookup"><span data-stu-id="e5404-292">Check whether monitoring is working, as described in [Checks and troubleshooting for setting up end-to-end monitoring][deployment-guide-troubleshooting-chapter].</span></span>

#### <a name="post-deployment-steps"></a><span data-ttu-id="e5404-293">Dağıtım sonrası adımlar</span><span class="sxs-lookup"><span data-stu-id="e5404-293">Post-deployment steps</span></span>
<span data-ttu-id="e5404-294">Oluşturduktan sonra hello VM ve VM hello dağıtılır, hello VM tooinstall gerekli hello yazılım bileşenleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="e5404-294">After you create hello VM and hello VM is deployed, you need tooinstall hello required software components in hello VM.</span></span> <span data-ttu-id="e5404-295">Merhaba dağıtım/yazılım yükleme sırası nedeniyle bu tür bir VM dağıtımı, yüklü hello yazılım toobe zaten ya da Azure, başka bir VM üzerinde veya kullanılabilir bir disk olarak kullanılabilir olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e5404-295">Because of hello deployment/software installation sequence in this type of VM deployment, hello software toobe installed must already be available, either in Azure, on another VM, or as a disk that can be attached.</span></span> <span data-ttu-id="e5404-296">Veya hangi bağlantı toohello varlıklar (yükleme paylaşımları) şirket içi bir şirket içi senaryo kullanarak verilen göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="e5404-296">Or, consider using a cross-premises scenario, in which connectivity toohello on-premises assets (installation shares) is given.</span></span>

<span data-ttu-id="e5404-297">Azure'da VM dağıttıktan sonra izleme hello aynı VM yazarken yönergeleri ve araçları tooinstall hello SAP yazılımı bir şirket içi ortamda gerekir.</span><span class="sxs-lookup"><span data-stu-id="e5404-297">After you deploy your VM in Azure, follow hello same guidelines and tools tooinstall hello SAP software on your VM as you would in an on-premises environment.</span></span> <span data-ttu-id="e5404-298">bir Azure VM tooinstall SAP yazılımı, hem SAP ve Microsoft karşıya yükleyin ve Azure VHD'lerde hello SAP yükleme medyası depolama öneririz ya da tüm hello sahip bir dosya sunucusu olarak çalışan bir Azure VM oluşturma SAP yükleme medyasını gereklidir.</span><span class="sxs-lookup"><span data-stu-id="e5404-298">tooinstall SAP software on an Azure VM, both SAP and Microsoft recommend that you upload and store hello SAP installation media on Azure VHDs, or that you create an Azure VM that works as a file server that has all hello required SAP installation media.</span></span>

[comment]: <> (MSSedusch neden toorecommend bir dosya yönetimi örneğin ihtiyacımız Yapılacaklar, dosya sunucusu veya VHD? Şirket içi çok farklı olan?)

### <span data-ttu-id="e5404-300"><a name="54a1fc6d-24fd-4feb-9c57-ac588a55dff2"></a>2. Senaryo: özel bir görüntü ile bir VM için SAP dağıtma</span><span class="sxs-lookup"><span data-stu-id="e5404-300"><a name="54a1fc6d-24fd-4feb-9c57-ac588a55dff2"></a>Scenario 2: Deploying a VM with a custom image for SAP</span></span>
<span data-ttu-id="e5404-301">Bir işletim sistemi veya DBMS farklı sürümlerini farklı düzeltme eki gereksinimleri olduğundan, hello Azure Marketi Bul hello görüntüleri ihtiyaçlarınızı karşılamayabilir.</span><span class="sxs-lookup"><span data-stu-id="e5404-301">Because different versions of an operating system or DBMS have different patch requirements, hello images you find in hello Azure Marketplace might not meet your needs.</span></span> <span data-ttu-id="e5404-302">Bunun yerine, daha sonra yeniden dağıtabilirsiniz kendi işletim sistemi/DBMS VM görüntüsünü kullanarak toocreate VM isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5404-302">You might instead want toocreate a VM by using your own OS/DBMS VM image, which you can deploy again later.</span></span>
<span data-ttu-id="e5404-303">Windows için toocreate daha Linux için farklı adımlar toocreate özel bir görüntü kullanın.</span><span class="sxs-lookup"><span data-stu-id="e5404-303">You use different steps toocreate a private image for Linux than toocreate one for Windows.</span></span>

- - -
> ![Windows][Logo_Windows] <span data-ttu-id="e5404-305">Windows</span><span class="sxs-lookup"><span data-stu-id="e5404-305">Windows</span></span>
>
> <span data-ttu-id="e5404-306">tooprepare hello üzerinde birden çok sanal makineler, hello Windows ayarları (örneğin, Windows SID ve ana bilgisayar adı) soyutlanır genelleştirilmiş veya gereken toodeploy kullanabileceğiniz bir Windows görüntüsünü VM şirket içi.</span><span class="sxs-lookup"><span data-stu-id="e5404-306">tooprepare a Windows image that you can use toodeploy multiple virtual machines, hello Windows settings (like Windows SID and hostname) must be abstracted or generalized on hello on-premises VM.</span></span> <span data-ttu-id="e5404-307">Kullanabileceğiniz [sysprep](https://msdn.microsoft.com/library/hh825084.aspx) toodo bu.</span><span class="sxs-lookup"><span data-stu-id="e5404-307">You can use [sysprep](https://msdn.microsoft.com/library/hh825084.aspx) toodo this.</span></span>
>
> ![Linux][Logo_Linux] <span data-ttu-id="e5404-309">Linux</span><span class="sxs-lookup"><span data-stu-id="e5404-309">Linux</span></span>
>
> <span data-ttu-id="e5404-310">birden çok sanal makine toodeploy kullanabileceğiniz bir Linux görüntüsü tooprepare, bazı Linux ayarları olmalıdır soyutlanır veya üzerinde genelleştirilmiş hello şirket içi VM.</span><span class="sxs-lookup"><span data-stu-id="e5404-310">tooprepare a Linux image that you can use toodeploy multiple virtual machines, some Linux settings must be abstracted or generalized on hello on-premises VM.</span></span> <span data-ttu-id="e5404-311">Kullanabileceğiniz `waagent -deprovision` toodo bu.</span><span class="sxs-lookup"><span data-stu-id="e5404-311">You can use `waagent -deprovision`  toodo this.</span></span> <span data-ttu-id="e5404-312">Daha fazla bilgi için bkz: [Azure üzerinde çalışan Linux sanal makine yakalama] [ virtual-machines-linux-capture-image] ve hello [Azure Linux Aracısı Kullanıcı Kılavuzu'na][virtual-machines-linux-agent-user-guide-command-line-options].</span><span class="sxs-lookup"><span data-stu-id="e5404-312">For more information, see [Capture a Linux virtual machine running on Azure][virtual-machines-linux-capture-image] and hello [Azure Linux agent user guide][virtual-machines-linux-agent-user-guide-command-line-options].</span></span>
>
>

- - -
<span data-ttu-id="e5404-313">Hazırlama ve özel bir görüntü oluşturun ve toocreate kullanmak birden çok yeni VM.</span><span class="sxs-lookup"><span data-stu-id="e5404-313">You can prepare and create a custom image, and then use it toocreate multiple new VMs.</span></span> <span data-ttu-id="e5404-314">Bu açıklanan [Azure sanal makineleri planlama ve uygulama Linux üzerinde SAP için][planning-guide].</span><span class="sxs-lookup"><span data-stu-id="e5404-314">This is described in [Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide].</span></span> <span data-ttu-id="e5404-315">Veritabanınızı ayarlama SAP yazılım sağlama Yöneticisi tooinstall yeni bir SAP sistemi kullanarak ya da içerik (ekli toohello sanal makine bir VHD'den bir veritabanı yedeklemesini geri yükler) veya doğrudan bir veritabanı yedeği, Azure depolama biriminden geri, DBMS Bunu destekler.</span><span class="sxs-lookup"><span data-stu-id="e5404-315">Set up your database content either by using SAP Software Provisioning Manager tooinstall a new SAP system (restores a database backup from a VHD that's attached toohello virtual machine) or by directly restoring a database backup from Azure storage, if your DBMS supports it.</span></span> <span data-ttu-id="e5404-316">Daha fazla bilgi için bkz: [Linux üzerinde SAP için Azure sanal makineleri DBMS dağıtım][dbms-guide].</span><span class="sxs-lookup"><span data-stu-id="e5404-316">For more information, see [Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide].</span></span> <span data-ttu-id="e5404-317">(Özellikle iki katmanlı sistemler için), şirket içi VM üzerinde bir SAP sistemi zaten yüklü değilse, hello SAP sistem ayarlarını hello Azure VM hello dağıtımdan sonra SAP yazılım sağlama tarafından desteklenen hello sistemi yeniden adlandırılamadı yordamı kullanarak uyarlayabilirsiniz Yöneticisi (SAP Not [1619720]).</span><span class="sxs-lookup"><span data-stu-id="e5404-317">If you have already installed an SAP system on your on-premises VM (especially for two-tier systems), you can adapt hello SAP system settings after hello deployment of hello Azure VM by using hello System Rename procedure supported by SAP Software Provisioning Manager (SAP Note [1619720]).</span></span> <span data-ttu-id="e5404-318">Aksi takdirde hello Azure VM dağıttıktan sonra hello SAP yazılım yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5404-318">Otherwise, you can install hello SAP software after you deploy hello Azure VM.</span></span>

<span data-ttu-id="e5404-319">Merhaba aşağıdaki akış çizelgesi hello SAP özgü özel bir görüntü VM'den dağıtma adımları sırasını göstermektedir:</span><span class="sxs-lookup"><span data-stu-id="e5404-319">hello following flowchart shows hello SAP-specific sequence of steps for deploying a VM from a custom image:</span></span>

![VM dağıtımı için bir VM görüntüsü özel Marketi'ndeki kullanarak SAP sistemleri akış çizelgesi][deployment-guide-figure-300]

#### <a name="create-hello-virtual-machine"></a><span data-ttu-id="e5404-321">Merhaba sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="e5404-321">Create hello virtual machine</span></span>
<span data-ttu-id="e5404-322">toocreate hello Azure portal, özel bir işletim sistemi görüntüsünü kullanarak bir dağıtım SAP şablonları aşağıdaki hello birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="e5404-322">toocreate a deployment by using a private OS image from hello Azure portal, use one of hello following SAP templates.</span></span> <span data-ttu-id="e5404-323">Bu şablonlar hello yayımlanan [azure hızlı başlangıç şablonlarını GitHub deposunu][azure-quickstart-templates-github].</span><span class="sxs-lookup"><span data-stu-id="e5404-323">These templates are published in hello [azure-quickstart-templates GitHub repository][azure-quickstart-templates-github].</span></span> <span data-ttu-id="e5404-324">Ayrıca el ile bir sanal makine kullanarak oluşturabileceğiniz [PowerShell][virtual-machines-upload-image-windows-resource-manager].</span><span class="sxs-lookup"><span data-stu-id="e5404-324">You also can manually create a virtual machine, by using [PowerShell][virtual-machines-upload-image-windows-resource-manager].</span></span>

* <span data-ttu-id="e5404-325">[**İki katmanlı yapılandırma (yalnızca bir sanal makine) şablonu** (sap-2-katman-kullanıcı-görüntü)][sap-templates-2-tier-user-image]</span><span class="sxs-lookup"><span data-stu-id="e5404-325">[**Two-tier configuration (only one virtual machine) template** (sap-2-tier-user-image)][sap-templates-2-tier-user-image]</span></span>

  <span data-ttu-id="e5404-326">toocreate yalnızca bir sanal makine kullanarak iki katmanlı sistem bu şablonu kullanın.</span><span class="sxs-lookup"><span data-stu-id="e5404-326">toocreate a two-tier system by using only one virtual machine, use this template.</span></span>
* <span data-ttu-id="e5404-327">[**Üç katmanlı yapılandırma (birden çok sanal makine) şablonu** (sap-3-katman-kullanıcı-görüntü)][sap-templates-3-tier-user-image]</span><span class="sxs-lookup"><span data-stu-id="e5404-327">[**Three-tier configuration (multiple virtual machines) template** (sap-3-tier-user-image)][sap-templates-3-tier-user-image]</span></span>

  <span data-ttu-id="e5404-328">toocreate birden çok sanal makine ya da kendi işletim sistemi görüntüsü kullanarak üç katmanlı sistem bu şablonu kullanın.</span><span class="sxs-lookup"><span data-stu-id="e5404-328">toocreate a three-tier system by using multiple virtual machines or your own OS image, use this template.</span></span>

<span data-ttu-id="e5404-329">Hello Azure portalı, şu parametreler hello şablonunun hello girin:</span><span class="sxs-lookup"><span data-stu-id="e5404-329">In hello Azure portal, enter hello following parameters for hello template:</span></span>

1. <span data-ttu-id="e5404-330">**Temel kavramları**:</span><span class="sxs-lookup"><span data-stu-id="e5404-330">**Basics**:</span></span>
  * <span data-ttu-id="e5404-331">**Abonelik**: hello abonelik toouse toodeploy hello şablonu.</span><span class="sxs-lookup"><span data-stu-id="e5404-331">**Subscription**: hello subscription toouse toodeploy hello template.</span></span>
  * <span data-ttu-id="e5404-332">**Kaynak grubu**: hello kaynak grubu toouse toodeploy hello şablonu.</span><span class="sxs-lookup"><span data-stu-id="e5404-332">**Resource group**: hello resource group toouse toodeploy hello template.</span></span> <span data-ttu-id="e5404-333">Yeni bir kaynak grubu oluşturun veya varolan bir kaynak grubu hello abonelikte seçin.</span><span class="sxs-lookup"><span data-stu-id="e5404-333">You can create a new resource group or select an existing resource group in hello subscription.</span></span>
  * <span data-ttu-id="e5404-334">**Konum**: Burada toodeploy hello şablonu.</span><span class="sxs-lookup"><span data-stu-id="e5404-334">**Location**: Where toodeploy hello template.</span></span> <span data-ttu-id="e5404-335">Varolan bir kaynak grubu seçtiyseniz, bu kaynak grubunun hello konumu kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e5404-335">If you selected an existing resource group, hello location of that resource group is used.</span></span>
2. <span data-ttu-id="e5404-336">**Ayarları**:</span><span class="sxs-lookup"><span data-stu-id="e5404-336">**Settings**:</span></span>
  * <span data-ttu-id="e5404-337">**SAP sistem kimliği**: Merhaba SAP sistem kimliği</span><span class="sxs-lookup"><span data-stu-id="e5404-337">**SAP System ID**: hello SAP System ID.</span></span>
  * <span data-ttu-id="e5404-338">**İşletim sistemi türü**: Merhaba toodeploy (Windows veya Linux) istediğiniz işletim sistemi türü.</span><span class="sxs-lookup"><span data-stu-id="e5404-338">**OS type**: hello operating system type you want toodeploy (Windows or Linux).</span></span>
  * <span data-ttu-id="e5404-339">**SAP sistem boyutu**: Merhaba hello SAP sistem boyutu.</span><span class="sxs-lookup"><span data-stu-id="e5404-339">**SAP system size**: hello size of hello SAP system.</span></span>

    <span data-ttu-id="e5404-340">SAP hello yeni sistem Hello sayısını sağlar.</span><span class="sxs-lookup"><span data-stu-id="e5404-340">hello number of SAPS hello new system provides.</span></span> <span data-ttu-id="e5404-341">Kaç tane SAP hello sistemi gerektirir emin değilseniz, SAP teknolojisi iş ortağı veya sistem Tümleştirici isteyin.</span><span class="sxs-lookup"><span data-stu-id="e5404-341">If you are not sure how many SAPS hello system requires, ask your SAP Technology Partner or System Integrator.</span></span>
  * <span data-ttu-id="e5404-342">**Sistem kullanılabilirliğini** (yalnızca üç katmanlı şablon): Merhaba sistem kullanılabilirlik.</span><span class="sxs-lookup"><span data-stu-id="e5404-342">**System availability** (three-tier template only): hello system availability.</span></span>

    <span data-ttu-id="e5404-343">Seçin **HA** yüksek kullanılabilirlik yüklemesi için uygun bir yapılandırma için.</span><span class="sxs-lookup"><span data-stu-id="e5404-343">Select **HA** for a configuration that is suitable for a high-availability installation.</span></span> <span data-ttu-id="e5404-344">İki veritabanı sunucuları ve iki sunucu ASCS için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e5404-344">Two database servers and two servers for ASCS are created.</span></span>
  * <span data-ttu-id="e5404-345">**Depolama türü** (yalnızca iki katmanlı şablon): Merhaba depolama toouse türü.</span><span class="sxs-lookup"><span data-stu-id="e5404-345">**Storage type** (two-tier template only): hello type of storage toouse.</span></span>

    <span data-ttu-id="e5404-346">Daha büyük sistemler için yüksek oranda Azure Premium Storage kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="e5404-346">For larger systems, we highly recommend using Azure Premium Storage.</span></span> <span data-ttu-id="e5404-347">Depolama türleri hakkında daha fazla bilgi için kaynakları aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="e5404-347">For more information about storage types, see hello following resources:</span></span>
      * <span data-ttu-id="e5404-348">[SAP DBMS örneği için Azure Premium SSD depolama kullanımı][2367194]</span><span class="sxs-lookup"><span data-stu-id="e5404-348">[Use of Azure Premium SSD Storage for SAP DBMS Instance][2367194]</span></span>
      * <span data-ttu-id="e5404-349">[Microsoft Azure depolama] [ dbms-guide-2.3] içinde [Linux üzerinde SAP için Azure sanal makineleri DBMS dağıtımı][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="e5404-349">[Microsoft Azure Storage][dbms-guide-2.3] in [Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide]</span></span>
      * <span data-ttu-id="e5404-350">[Premium Storage: Azure sanal makine iş yükleri için yüksek performanslı depolama][storage-premium-storage-preview-portal]</span><span class="sxs-lookup"><span data-stu-id="e5404-350">[Premium Storage: High-performance storage for Azure virtual machine workloads][storage-premium-storage-preview-portal]</span></span>
      * <span data-ttu-id="e5404-351">[Giriş tooMicrosoft Azure depolama][storage-introduction]</span><span class="sxs-lookup"><span data-stu-id="e5404-351">[Introduction tooMicrosoft Azure Storage][storage-introduction]</span></span>
  * <span data-ttu-id="e5404-352">**Kullanıcı görüntüsü VHD URİ'si**: hello özel işletim sistemi görüntüsü VHD, örneğin, https:// URI'sini hello&lt;accountname >.blob.core.windows.net/vhds/userimage.vhd.</span><span class="sxs-lookup"><span data-stu-id="e5404-352">**User image VHD URI**: hello URI of hello private OS image VHD, for example, https://&lt;accountname>.blob.core.windows.net/vhds/userimage.vhd.</span></span>
  * <span data-ttu-id="e5404-353">**Kullanıcı görüntü depolama hesabı**: hello hello özel işletim sistemi görüntüsünün depolandığı, örneğin, hello depolama hesabının adını &lt;accountname > https:// içinde&lt;accountname >.blob.core.windows.net/vhds/userimage.vhd.</span><span class="sxs-lookup"><span data-stu-id="e5404-353">**User image storage account**: hello name of hello storage account where hello private OS image is stored, for example, &lt;accountname> in https://&lt;accountname>.blob.core.windows.net/vhds/userimage.vhd.</span></span>
  * <span data-ttu-id="e5404-354">**Yönetici kullanıcı adı** ve **yönetici parolası**: Merhaba kullanıcı adı ve parola.</span><span class="sxs-lookup"><span data-stu-id="e5404-354">**Admin username** and **Admin password**: hello username and password.</span></span>

    <span data-ttu-id="e5404-355">Yeni bir kullanıcı, toohello sanal makinede imzalamak için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e5404-355">A new user is created, for signing in toohello virtual machine.</span></span>
  * <span data-ttu-id="e5404-356">**Yeni veya var olan bir alt ağ**: yeni bir sanal ağ ve alt ağ oluşturulur veya mevcut bir alt kullanılan belirler.</span><span class="sxs-lookup"><span data-stu-id="e5404-356">**New or existing subnet**: Determines whether a new virtual network and subnet is created or an existing subnet is used.</span></span> <span data-ttu-id="e5404-357">Bağlı tooyour şirket içi ağ bir sanal ağ zaten varsa, seçin **varolan**.</span><span class="sxs-lookup"><span data-stu-id="e5404-357">If you already have a virtual network that is connected tooyour on-premises network, select **Existing**.</span></span>
  * <span data-ttu-id="e5404-358">**Alt ağ kimliği**: hello kimliği hello alt toowhich hello sanal makinelerin bağlanması için.</span><span class="sxs-lookup"><span data-stu-id="e5404-358">**Subnet ID**: hello ID of hello subnet toowhich hello virtual machines will connect to.</span></span> <span data-ttu-id="e5404-359">VPN ya da ExpressRoute sanal ağ toouse tooconnect hello sanal makine tooyour Şirket ağınızın Hello alt ağ seçin.</span><span class="sxs-lookup"><span data-stu-id="e5404-359">Select hello subnet of your VPN or ExpressRoute virtual network toouse tooconnect hello virtual machine tooyour on-premises network.</span></span> <span data-ttu-id="e5404-360">Merhaba kimliği genellikle şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="e5404-360">hello ID usually looks like this:</span></span>

    <span data-ttu-id="e5404-361">/Subscriptions/&lt;abonelik kimliği > /resourceGroups/&lt;kaynak grubu adı > /providers/Microsoft.Network/virtualNetworks/&lt;sanal ağ adı > /subnets/&lt;alt ağ adı ></span><span class="sxs-lookup"><span data-stu-id="e5404-361">/subscriptions/&lt;subscription id>/resourceGroups/&lt;resource group name>/providers/Microsoft.Network/virtualNetworks/&lt;virtual network name>/subnets/&lt;subnet name></span></span>

3. <span data-ttu-id="e5404-362">**Hüküm ve koşullar**:</span><span class="sxs-lookup"><span data-stu-id="e5404-362">**Terms and conditions**:</span></span>  
    <span data-ttu-id="e5404-363">Gözden geçirin ve hello yasal koşulları kabul edin.</span><span class="sxs-lookup"><span data-stu-id="e5404-363">Review and accept hello legal terms.</span></span>

4.  <span data-ttu-id="e5404-364">Seçin **satın alma**.</span><span class="sxs-lookup"><span data-stu-id="e5404-364">Select **Purchase**.</span></span>

#### <a name="install-hello-vm-agent-linux-only"></a><span data-ttu-id="e5404-365">Merhaba VM Aracısı (yalnızca Linux) yükleyin</span><span class="sxs-lookup"><span data-stu-id="e5404-365">Install hello VM Agent (Linux only)</span></span>
<span data-ttu-id="e5404-366">hello önceki bölümde açıklanan toouse hello şablonları Linux Aracısı hello kullanıcı görüntüsü veya başlangıç dağıtımı yüklü olması gereken hello başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="e5404-366">toouse hello templates described in hello preceding section, hello Linux Agent must already be installed in hello user image, or hello deployment will fail.</span></span> <span data-ttu-id="e5404-367">Karşıdan yükleyip hello VM Aracısı hello kullanıcı görüntüde açıklandığı gibi [indirme, yükleme ve hello Azure VM Aracısı etkinleştirme][deployment-guide-4.4].</span><span class="sxs-lookup"><span data-stu-id="e5404-367">Download and install hello VM Agent in hello user image as described in [Download, install, and enable hello Azure VM Agent][deployment-guide-4.4].</span></span> <span data-ttu-id="e5404-368">Merhaba şablonları kullanmıyorsanız, daha sonra VM Aracısı hello da yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5404-368">If you don’t use hello templates, you also can install hello VM Agent later.</span></span>

#### <a name="join-a-domain-windows-only"></a><span data-ttu-id="e5404-369">(Yalnızca Windows) etki alanına Katıl</span><span class="sxs-lookup"><span data-stu-id="e5404-369">Join a domain (Windows only)</span></span>
<span data-ttu-id="e5404-370">Azure dağıtımınıza bağlı tooan şirket içi Active Directory veya DNS Azure siteden siteye VPN bağlantısı veya Azure ExpressRoute üzerinden örneğiyse (Bu adlı *şirketler arası* içinde [Azure sanal makineler Planlama ve uygulama Linux üzerinde SAP için][planning-guide]), o hello VM bir şirket içi etki alanına katılma beklenir.</span><span class="sxs-lookup"><span data-stu-id="e5404-370">If your Azure deployment is connected tooan on-premises Active Directory or DNS instance via an Azure site-to-site VPN connection or Azure ExpressRoute (this is called *cross-premises* in [Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]), it is expected that hello VM is joining an on-premises domain.</span></span> <span data-ttu-id="e5404-371">Bu adım için ilgili önemli noktalar hakkında daha fazla bilgi için bkz: [VM tooan şirket içi etki alanına (yalnızca Windows) katılma][deployment-guide-4.3].</span><span class="sxs-lookup"><span data-stu-id="e5404-371">For more information about considerations for this step, see [Join a VM tooan on-premises domain (Windows only)][deployment-guide-4.3].</span></span>

#### <a name="configure-proxy-settings"></a><span data-ttu-id="e5404-372">Proxy ayarlarını yapılandır</span><span class="sxs-lookup"><span data-stu-id="e5404-372">Configure proxy settings</span></span>
<span data-ttu-id="e5404-373">Şirket içi ağınıza nasıl yapılandırıldığına bağlı olarak, VM hello proxy yukarı tooset gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="e5404-373">Depending on how your on-premises network is configured, you might need tooset up hello proxy on your VM.</span></span> <span data-ttu-id="e5404-374">VM bağlı tooyour şirket içi ağ VPN ya da ExpressRoute aracılığıyla ise, hello VM değil mümkün tooaccess hello Internet olması ve olmaz mümkün toodownload gerekli hello uzantıları veya izleme verilerini topla.</span><span class="sxs-lookup"><span data-stu-id="e5404-374">If your VM is connected tooyour on-premises network via VPN or ExpressRoute, hello VM might not be able tooaccess hello Internet, and won't be able toodownload hello required extensions or collect monitoring data.</span></span> <span data-ttu-id="e5404-375">Daha fazla bilgi için bkz: [hello proxy yapılandırma][deployment-guide-configure-proxy].</span><span class="sxs-lookup"><span data-stu-id="e5404-375">For more information, see [Configure hello proxy][deployment-guide-configure-proxy].</span></span>

#### <a name="configure-monitoring"></a><span data-ttu-id="e5404-376">İzlemeyi Yapılandır</span><span class="sxs-lookup"><span data-stu-id="e5404-376">Configure monitoring</span></span>
<span data-ttu-id="e5404-377">ortamınızı açıklandığı gibi hello Azure Monitoring uzantısı SAP için ayarlamak SAP desteklediğinden emin toobe [yapılandırma hello Azure Gelişmiş izleme uzantısı SAP][deployment-guide-4.5].</span><span class="sxs-lookup"><span data-stu-id="e5404-377">toobe sure your environment supports SAP, set up hello Azure Monitoring Extension for SAP as described in [Configure hello Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span> <span data-ttu-id="e5404-378">SAP izleme ve gerekli en düşük sürümlerinde SAP çekirdek ve SAP konak Aracısı, listelenen hello kaynakları Hello önkoşullarını denetlemek [SAP kaynakları][deployment-guide-2.2].</span><span class="sxs-lookup"><span data-stu-id="e5404-378">Check hello prerequisites for SAP monitoring, and required minimum versions of SAP Kernel and SAP Host Agent, in hello resources listed in [SAP resources][deployment-guide-2.2].</span></span>

#### <a name="monitoring-check"></a><span data-ttu-id="e5404-379">Onay izleme</span><span class="sxs-lookup"><span data-stu-id="e5404-379">Monitoring check</span></span>
<span data-ttu-id="e5404-380">İzleme çalışıp çalışmadığını, açıklandığı gibi denetleyin [denetler ve uçtan uca izleme ayarlamak için sorun giderme][deployment-guide-troubleshooting-chapter].</span><span class="sxs-lookup"><span data-stu-id="e5404-380">Check whether monitoring is working, as described in [Checks and troubleshooting for setting up end-to-end monitoring][deployment-guide-troubleshooting-chapter].</span></span>




### <span data-ttu-id="e5404-381"><a name="a9a60133-a763-4de8-8986-ac0fa33aa8c1"></a>Senaryo 3: şirket içi VM genelleştirilmiş Azure VHD SAP ile kullanarak taşıma</span><span class="sxs-lookup"><span data-stu-id="e5404-381"><a name="a9a60133-a763-4de8-8986-ac0fa33aa8c1"></a>Scenario 3: Moving an on-premises VM by using a non-generalized Azure VHD with SAP</span></span>
<span data-ttu-id="e5404-382">Bu senaryoda, bir şirket içi ortamına tooAzure belirli bir SAP sistemden toomove planlayın.</span><span class="sxs-lookup"><span data-stu-id="e5404-382">In this scenario, you plan toomove a specific SAP system from an on-premises environment tooAzure.</span></span> <span data-ttu-id="e5404-383">Hello hello işletim sistemi, hello SAP ikili dosyaları, sahip VHD yükleyerek bunu ve sonunda DBMS ikili dosyalarının yanı sıra, hello VHD'ler hello verilerle Merhaba ve günlük hello DBMS, tooAzure dosyaları.</span><span class="sxs-lookup"><span data-stu-id="e5404-383">You can do this by uploading hello VHD that has hello OS, hello SAP binaries, and eventually hello DBMS binaries, plus hello VHDs with hello data and log files of hello DBMS, tooAzure.</span></span> <span data-ttu-id="e5404-384">İçinde açıklanan hello senaryosu aksine [Senaryo 2: özel bir görüntü ile bir VM için SAP dağıtma][deployment-guide-3.3], bu durumda, hello ana bilgisayar adı, SAP SID tutmak ve SAP kullanıcı hesapları hello Azure VM oldukları için Merhaba şirket içi ortamda yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="e5404-384">Unlike hello scenario described in [Scenario 2: Deploying a VM with a custom image for SAP][deployment-guide-3.3], in this case, you keep hello hostname, SAP SID, and SAP user accounts in hello Azure VM, because they were configured in hello on-premises environment.</span></span> <span data-ttu-id="e5404-385">Toogeneralize hello OS gerekmez.</span><span class="sxs-lookup"><span data-stu-id="e5404-385">You do not need toogeneralize hello OS.</span></span> <span data-ttu-id="e5404-386">Bu senaryo için burada hello SAP yatay parçası şirket içi çalışır ve kısmını Azure üzerinde çalışan en sık toocross içi senaryoları geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="e5404-386">This scenario applies most often toocross-premises scenarios where part of hello SAP landscape runs on-premises and part of it runs on Azure.</span></span>

<span data-ttu-id="e5404-387">Bu senaryoda, hello VM Aracısı dağıtımı sırasında otomatik olarak yüklenmez.</span><span class="sxs-lookup"><span data-stu-id="e5404-387">In this scenario, hello VM Agent is not automatically installed during deployment.</span></span> <span data-ttu-id="e5404-388">Hello VM aracısı ve hello Gelişmiş izleme uzantısı SAP için Azure SAP toorun için gerekli olduğundan, her iki toodownload, yükleme ve etkinleştirme gereken el ile Merhaba sanal makineyi oluşturduktan sonra bileşenleri.</span><span class="sxs-lookup"><span data-stu-id="e5404-388">Because hello VM Agent and hello Azure Enhanced Monitoring Extension for SAP required for toorun SAP, you need toodownload, install, and enable both components manually after you create hello virtual machine.</span></span>

<span data-ttu-id="e5404-389">Hello Azure VM Aracısı hakkında daha fazla bilgi için kaynakları aşağıdaki hello bakın.</span><span class="sxs-lookup"><span data-stu-id="e5404-389">For more information about hello Azure VM Agent, see hello following resources.</span></span>

[comment]: <> (MSSedusch Yapılacaklar güncelleştirme Windows bağlantıyı)

- - -
> ![Windows][Logo_Windows] <span data-ttu-id="e5404-392">Windows</span><span class="sxs-lookup"><span data-stu-id="e5404-392">Windows</span></span>
>
> <span data-ttu-id="e5404-393"><http://blogs.msdn.com/b/wats/archive/2014/02/17/bginfo-Guest-Agent-Extension-for-Azure-VMs.aspx></span><span class="sxs-lookup"><span data-stu-id="e5404-393"><http://blogs.msdn.com/b/wats/archive/2014/02/17/bginfo-guest-agent-extension-for-azure-vms.aspx></span></span>
>
> ![Linux][Logo_Linux] <span data-ttu-id="e5404-395">Linux</span><span class="sxs-lookup"><span data-stu-id="e5404-395">Linux</span></span>
>
> <span data-ttu-id="e5404-396">[Azure Linux Aracısı Kullanıcı Kılavuzu][virtual-machines-linux-agent-user-guide]</span><span class="sxs-lookup"><span data-stu-id="e5404-396">[Azure Linux Agent User Guide][virtual-machines-linux-agent-user-guide]</span></span>
>
>

- - -

<span data-ttu-id="e5404-397">Aşağıdaki akış çizelgesi hello genelleştirilmiş Azure VHD kullanarak bir şirket içi VM taşıma adımları hello sırasını göstermektedir:</span><span class="sxs-lookup"><span data-stu-id="e5404-397">hello following flowchart shows hello sequence of steps for moving an on-premises VM by using a non-generalized Azure VHD:</span></span>

![VM dağıtımı için bir VM disk kullanarak SAP sistemleri akış çizelgesi][deployment-guide-figure-400]

<span data-ttu-id="e5404-399">Merhaba disk zaten karşıya ve Azure'da tanımlanan varsayılarak (bkz [Azure sanal makineleri planlama ve uygulama Linux üzerinde SAP için][planning-guide]), yapmak hello görevleri açıklanan hello sonraki birkaç bölümler.</span><span class="sxs-lookup"><span data-stu-id="e5404-399">Assuming that hello disk is already uploaded and defined in Azure (see [Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]), do hello tasks described in hello next few sections.</span></span>

#### <a name="create-a-virtual-machine"></a><span data-ttu-id="e5404-400">Sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="e5404-400">Create a virtual machine</span></span>
<span data-ttu-id="e5404-401">toocreate hello Azure portal aracılığıyla özel bir işletim sistemi diski kullanarak bir dağıtım hello yayımlanan hello SAP şablonu kullanın [azure hızlı başlangıç şablonlarını GitHub deposunu][azure-quickstart-templates-github].</span><span class="sxs-lookup"><span data-stu-id="e5404-401">toocreate a deployment by using a private OS disk through hello Azure portal, use hello SAP template published in hello [azure-quickstart-templates GitHub repository][azure-quickstart-templates-github].</span></span> <span data-ttu-id="e5404-402">Ayrıca el ile bir sanal makine PowerShell kullanarak oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5404-402">You also can manually create a virtual machine, by using PowerShell.</span></span>

* <span data-ttu-id="e5404-403">[**İki katmanlı yapılandırma (yalnızca bir sanal makine) şablonu** (sap-2-katman-kullanıcı-disk)][sap-templates-2-tier-os-disk]</span><span class="sxs-lookup"><span data-stu-id="e5404-403">[**Two-tier configuration (only one virtual machine) template** (sap-2-tier-user-disk)][sap-templates-2-tier-os-disk]</span></span>

  <span data-ttu-id="e5404-404">toocreate yalnızca bir sanal makine kullanarak iki katmanlı sistem bu şablonu kullanın.</span><span class="sxs-lookup"><span data-stu-id="e5404-404">toocreate a two-tier system by using only one virtual machine, use this template.</span></span>

<span data-ttu-id="e5404-405">Hello Azure portalı, şu parametreler hello şablonunun hello girin:</span><span class="sxs-lookup"><span data-stu-id="e5404-405">In hello Azure portal, enter hello following parameters for hello template:</span></span>

1. <span data-ttu-id="e5404-406">**Temel kavramları**:</span><span class="sxs-lookup"><span data-stu-id="e5404-406">**Basics**:</span></span>
  * <span data-ttu-id="e5404-407">**Abonelik**: hello abonelik toouse toodeploy hello şablonu.</span><span class="sxs-lookup"><span data-stu-id="e5404-407">**Subscription**: hello subscription toouse toodeploy hello template.</span></span>
  * <span data-ttu-id="e5404-408">**Kaynak grubu**: hello kaynak grubu toouse toodeploy hello şablonu.</span><span class="sxs-lookup"><span data-stu-id="e5404-408">**Resource group**: hello resource group toouse toodeploy hello template.</span></span> <span data-ttu-id="e5404-409">Yeni bir kaynak grubu oluşturun veya varolan bir kaynak grubu hello abonelikte seçin.</span><span class="sxs-lookup"><span data-stu-id="e5404-409">You can create a new resource group or select an existing resource group in hello subscription.</span></span>
  * <span data-ttu-id="e5404-410">**Konum**: Burada toodeploy hello şablonu.</span><span class="sxs-lookup"><span data-stu-id="e5404-410">**Location**: Where toodeploy hello template.</span></span> <span data-ttu-id="e5404-411">Varolan bir kaynak grubu seçtiyseniz, bu kaynak grubunun hello konumu kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e5404-411">If you selected an existing resource group, hello location of that resource group is used.</span></span>
2. <span data-ttu-id="e5404-412">**Ayarları**:</span><span class="sxs-lookup"><span data-stu-id="e5404-412">**Settings**:</span></span>
  * <span data-ttu-id="e5404-413">**SAP sistem kimliği**: Merhaba SAP sistem kimliği</span><span class="sxs-lookup"><span data-stu-id="e5404-413">**SAP System ID**: hello SAP System ID.</span></span>
  * <span data-ttu-id="e5404-414">**İşletim sistemi türü**: Merhaba toodeploy (Windows veya Linux) istediğiniz işletim sistemi türü.</span><span class="sxs-lookup"><span data-stu-id="e5404-414">**OS type**: hello operating system type you want toodeploy (Windows or Linux).</span></span>
  * <span data-ttu-id="e5404-415">**SAP sistem boyutu**: Merhaba hello SAP sistem boyutu.</span><span class="sxs-lookup"><span data-stu-id="e5404-415">**SAP system size**: hello size of hello SAP system.</span></span>

    <span data-ttu-id="e5404-416">SAP hello yeni sistem Hello sayısını sağlar.</span><span class="sxs-lookup"><span data-stu-id="e5404-416">hello number of SAPS hello new system provides.</span></span> <span data-ttu-id="e5404-417">Kaç tane SAP hello sistemi gerektirir emin değilseniz, SAP teknolojisi iş ortağı veya sistem Tümleştirici isteyin.</span><span class="sxs-lookup"><span data-stu-id="e5404-417">If you are not sure how many SAPS hello system requires, ask your SAP Technology Partner or System Integrator.</span></span>
  * <span data-ttu-id="e5404-418">**Depolama türü** (yalnızca iki katmanlı şablon): Merhaba depolama toouse türü.</span><span class="sxs-lookup"><span data-stu-id="e5404-418">**Storage type** (two-tier template only): hello type of storage toouse.</span></span>

    <span data-ttu-id="e5404-419">Daha büyük sistemler için yüksek oranda Azure Premium Storage kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="e5404-419">For larger systems, we highly recommend using Azure Premium Storage.</span></span> <span data-ttu-id="e5404-420">Depolama türleri hakkında daha fazla bilgi için kaynakları aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="e5404-420">For more information about storage types, see hello following resources:</span></span>
      * <span data-ttu-id="e5404-421">[SAP DBMS örneği için Azure Premium SSD depolama kullanımı][2367194]</span><span class="sxs-lookup"><span data-stu-id="e5404-421">[Use of Azure Premium SSD Storage for SAP DBMS Instance][2367194]</span></span>
      * <span data-ttu-id="e5404-422">[Microsoft Azure depolama] [ dbms-guide-2.3] içinde [Linux üzerinde SAP için Azure sanal makine DBMS dağıtımı][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="e5404-422">[Microsoft Azure Storage][dbms-guide-2.3] in [Azure Virtual Machine DBMS deployment for SAP on Linux][dbms-guide]</span></span>
      * <span data-ttu-id="e5404-423">[Premium Storage: Azure sanal makine iş yükleri için yüksek performanslı depolama][storage-premium-storage-preview-portal]</span><span class="sxs-lookup"><span data-stu-id="e5404-423">[Premium Storage: High-performance storage for Azure Virtual Machine workloads][storage-premium-storage-preview-portal]</span></span>
      * <span data-ttu-id="e5404-424">[Giriş tooMicrosoft Azure depolama][storage-introduction]</span><span class="sxs-lookup"><span data-stu-id="e5404-424">[Introduction tooMicrosoft Azure Storage][storage-introduction]</span></span>
  * <span data-ttu-id="e5404-425">**İşletim sistemi diski VHD URİ'si**: hello özel işletim sistemi diski, örneğin, https:// URI'sini hello&lt;accountname >.blob.core.windows.net/vhds/osdisk.vhd.</span><span class="sxs-lookup"><span data-stu-id="e5404-425">**OS disk VHD URI**: hello URI of hello private OS disk, for example, https://&lt;accountname>.blob.core.windows.net/vhds/osdisk.vhd.</span></span>
  * <span data-ttu-id="e5404-426">**Yeni veya var olan bir alt ağ**: yeni bir sanal ağ ve alt ağ oluşturulur veya mevcut bir alt kullanılan olup olmadığını belirler.</span><span class="sxs-lookup"><span data-stu-id="e5404-426">**New or existing subnet**: Determines whether a new virtual network and subnet are created, or an existing subnet is used.</span></span> <span data-ttu-id="e5404-427">Bağlı tooyour şirket içi ağ bir sanal ağ zaten varsa, seçin **varolan**.</span><span class="sxs-lookup"><span data-stu-id="e5404-427">If you already have a virtual network that is connected tooyour on-premises network, select **Existing**.</span></span>
  * <span data-ttu-id="e5404-428">**Alt ağ kimliği**: hello kimliği hello alt toowhich hello sanal makinelerin bağlanması için.</span><span class="sxs-lookup"><span data-stu-id="e5404-428">**Subnet ID**: hello ID of hello subnet toowhich hello virtual machines will connect to.</span></span> <span data-ttu-id="e5404-429">VPN veya Azure ExpressRoute sanal ağ toouse tooconnect hello sanal makine tooyour Şirket ağınızın Hello alt ağ seçin.</span><span class="sxs-lookup"><span data-stu-id="e5404-429">Select hello subnet of your VPN or Azure ExpressRoute virtual network toouse tooconnect hello virtual machine tooyour on-premises network.</span></span> <span data-ttu-id="e5404-430">Merhaba kimliği genellikle şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="e5404-430">hello ID usually looks like this:</span></span>

    <span data-ttu-id="e5404-431">/Subscriptions/&lt;abonelik kimliği > /resourceGroups/&lt;kaynak grubu adı > /providers/Microsoft.Network/virtualNetworks/&lt;sanal ağ adı > /subnets/&lt;alt ağ adı ></span><span class="sxs-lookup"><span data-stu-id="e5404-431">/subscriptions/&lt;subscription id>/resourceGroups/&lt;resource group name>/providers/Microsoft.Network/virtualNetworks/&lt;virtual network name>/subnets/&lt;subnet name></span></span>

3. <span data-ttu-id="e5404-432">**Hüküm ve koşullar**:</span><span class="sxs-lookup"><span data-stu-id="e5404-432">**Terms and conditions**:</span></span>  
    <span data-ttu-id="e5404-433">Gözden geçirin ve hello yasal koşulları kabul edin.</span><span class="sxs-lookup"><span data-stu-id="e5404-433">Review and accept hello legal terms.</span></span>

4.  <span data-ttu-id="e5404-434">Seçin **satın alma**.</span><span class="sxs-lookup"><span data-stu-id="e5404-434">Select **Purchase**.</span></span>

#### <a name="install-hello-vm-agent"></a><span data-ttu-id="e5404-435">Merhaba VM Aracısı yükleme</span><span class="sxs-lookup"><span data-stu-id="e5404-435">Install hello VM Agent</span></span>
<span data-ttu-id="e5404-436">Şablonları açıklanan toouse hello hello önceki bölümde, hello VM Aracısı hello işletim sistemi disk üzerinde yüklü olmalıdır veya başlangıç dağıtımı başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="e5404-436">toouse hello templates described in hello preceding section, hello VM Agent must be installed on hello OS disk, or hello deployment will fail.</span></span> <span data-ttu-id="e5404-437">Karşıdan yükleyip hello VM Aracısı hello VM açıklandığı gibi [indirme, yükleme ve hello Azure VM Aracısı etkinleştirme][deployment-guide-4.4].</span><span class="sxs-lookup"><span data-stu-id="e5404-437">Download and install hello VM Agent in hello VM, as described in [Download, install, and enable hello Azure VM Agent][deployment-guide-4.4].</span></span>

<span data-ttu-id="e5404-438">Hello önceki bölümde açıklanan hello şablonları kullanmıyorsanız, daha sonra hello VM Aracısı da yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5404-438">If you don’t use hello templates described in hello preceding section, you can also install hello VM Agent afterwards.</span></span>

#### <a name="join-a-domain-windows-only"></a><span data-ttu-id="e5404-439">(Yalnızca Windows) etki alanına Katıl</span><span class="sxs-lookup"><span data-stu-id="e5404-439">Join a domain (Windows only)</span></span>
<span data-ttu-id="e5404-440">Azure dağıtımınıza bağlı tooan şirket içi Active Directory veya DNS bir Azure siteden siteye VPN bağlantısı veya ExpressRoute aracılığıyla örneğiyse (Bu adlı *şirketler arası* içinde [Azure sanal makineleri planlama ve Linux üzerinde SAP uygulamasını][planning-guide]), o hello VM bir şirket içi etki alanına katılma beklenir.</span><span class="sxs-lookup"><span data-stu-id="e5404-440">If your Azure deployment is connected tooan on-premises Active Directory or DNS instance via an Azure site-to-site VPN connection or ExpressRoute (this is called *cross-premises* in [Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]), it is expected that hello VM is joining an on-premises domain.</span></span> <span data-ttu-id="e5404-441">Bu görev için konuları hakkında daha fazla bilgi için bkz: [VM tooan şirket içi etki alanına (yalnızca Windows) katılma][deployment-guide-4.3].</span><span class="sxs-lookup"><span data-stu-id="e5404-441">For more information about considerations for this task, see [Join a VM tooan on-premises domain (Windows only)][deployment-guide-4.3].</span></span>

#### <a name="configure-proxy-settings"></a><span data-ttu-id="e5404-442">Proxy ayarlarını yapılandır</span><span class="sxs-lookup"><span data-stu-id="e5404-442">Configure proxy settings</span></span>
<span data-ttu-id="e5404-443">Şirket içi ağınıza nasıl yapılandırıldığına bağlı olarak, VM hello proxy yukarı tooset gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="e5404-443">Depending on how your on-premises network is configured, you might need tooset up hello proxy on your VM.</span></span> <span data-ttu-id="e5404-444">VM bağlı tooyour şirket içi ağ VPN ya da ExpressRoute aracılığıyla ise, hello VM değil mümkün tooaccess hello Internet olması ve olmaz mümkün toodownload gerekli hello uzantıları veya izleme verilerini topla.</span><span class="sxs-lookup"><span data-stu-id="e5404-444">If your VM is connected tooyour on-premises network via VPN or ExpressRoute, hello VM might not be able tooaccess hello Internet, and won't be able toodownload hello required extensions or collect monitoring data.</span></span> <span data-ttu-id="e5404-445">Daha fazla bilgi için bkz: [hello proxy yapılandırma][deployment-guide-configure-proxy].</span><span class="sxs-lookup"><span data-stu-id="e5404-445">For more information, see [Configure hello proxy][deployment-guide-configure-proxy].</span></span>

#### <a name="configure-monitoring"></a><span data-ttu-id="e5404-446">İzlemeyi Yapılandır</span><span class="sxs-lookup"><span data-stu-id="e5404-446">Configure monitoring</span></span>
<span data-ttu-id="e5404-447">ortamınızı açıklandığı gibi hello Azure Monitoring uzantısı SAP için ayarlamak SAP desteklediğinden emin toobe [yapılandırma hello Azure Gelişmiş izleme uzantısı SAP][deployment-guide-4.5].</span><span class="sxs-lookup"><span data-stu-id="e5404-447">toobe sure your environment supports SAP, set up hello Azure Monitoring Extension for SAP as described in [Configure hello Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span> <span data-ttu-id="e5404-448">SAP izleme ve gerekli en düşük sürümlerinde SAP çekirdek ve SAP konak Aracısı, listelenen hello kaynakları Hello önkoşullarını denetlemek [SAP kaynakları][deployment-guide-2.2].</span><span class="sxs-lookup"><span data-stu-id="e5404-448">Check hello prerequisites for SAP monitoring, and required minimum versions of SAP Kernel and SAP Host Agent, in hello resources listed in [SAP resources][deployment-guide-2.2].</span></span>

#### <a name="monitoring-check"></a><span data-ttu-id="e5404-449">Onay izleme</span><span class="sxs-lookup"><span data-stu-id="e5404-449">Monitoring check</span></span>
<span data-ttu-id="e5404-450">İzleme çalışıp çalışmadığını, açıklandığı gibi denetleyin [denetler ve uçtan uca izleme ayarlamak için sorun giderme][deployment-guide-troubleshooting-chapter].</span><span class="sxs-lookup"><span data-stu-id="e5404-450">Check whether monitoring is working, as described in [Checks and troubleshooting for setting up end-to-end monitoring][deployment-guide-troubleshooting-chapter].</span></span>

## <a name="update-hello-monitoring-configuration-for-sap"></a><span data-ttu-id="e5404-451">SAP için izleme yapılandırmasını Hello güncelleştir</span><span class="sxs-lookup"><span data-stu-id="e5404-451">Update hello monitoring configuration for SAP</span></span>
<span data-ttu-id="e5404-452">Herhangi bir senaryo aşağıdaki hello Hello SAP İzleme yapılandırmasını güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="e5404-452">Update hello SAP monitoring configuration in any of hello following scenarios:</span></span>
* <span data-ttu-id="e5404-453">Merhaba birleşik Microsoft/SAP takım izleme kapasiteleri hello genişletir ve daha fazla veya daha az sayaçları ister.</span><span class="sxs-lookup"><span data-stu-id="e5404-453">hello joint Microsoft/SAP team extends hello monitoring capabilities and requests more or fewer counters.</span></span>
* <span data-ttu-id="e5404-454">Microsoft izleme verilerini hello teslim eden hello Azure altyapının yeni bir sürümünü kullanıma sunmaktadır ve SAP gereksinimlerini toobe Merhaba Azure Gelişmiş izleme uzantısı toothose değişiklikleri uyarlanan.</span><span class="sxs-lookup"><span data-stu-id="e5404-454">Microsoft introduces a new version of hello underlying Azure infrastructure that delivers hello monitoring data, and hello Azure Enhanced Monitoring Extension for SAP needs toobe adapted toothose changes.</span></span>
* <span data-ttu-id="e5404-455">Ek VHD'ler tooyour Azure VM bağlayın veya bir VHD'yi kaldırın.</span><span class="sxs-lookup"><span data-stu-id="e5404-455">You mount additional VHDs tooyour Azure VM or you remove a VHD.</span></span> <span data-ttu-id="e5404-456">Bu senaryoda, depolama ile ilgili veriler hello koleksiyonu güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="e5404-456">In this scenario, update hello collection of storage-related data.</span></span> <span data-ttu-id="e5404-457">Ekleyerek veya silerek uç noktaları veya IP atayarak yapılandırmanızı değiştirme adresleri tooa VM hello izleme yapılandırması etkilemez.</span><span class="sxs-lookup"><span data-stu-id="e5404-457">Changing your configuration by adding or deleting endpoints or by assigning IP addresses tooa VM does not affect hello monitoring configuration.</span></span>
* <span data-ttu-id="e5404-458">Hello boyutunu Azure VM, örneğin, boyutu A5 tooany diğer VM boyutunu değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e5404-458">You change hello size of your Azure VM, for example, from size A5 tooany other VM size.</span></span>
* <span data-ttu-id="e5404-459">Yeni ağ arabirimleri tooyour Azure VM ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e5404-459">You add new network interfaces tooyour Azure VM.</span></span>

<span data-ttu-id="e5404-460">izleme ayarları, aşağıdaki hello tarafından altyapısını izleme güncelleştirme hello tooupdate adımları [yapılandırma hello Azure Gelişmiş izleme uzantısı SAP][deployment-guide-4.5].</span><span class="sxs-lookup"><span data-stu-id="e5404-460">tooupdate monitoring settings, update hello monitoring infrastructure by following hello steps in [Configure hello Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span>

## <a name="detailed-tasks-for-sap-software-deployment-on-a-windows-vm"></a><span data-ttu-id="e5404-461">Bir Windows VM üzerinde SAP yazılım dağıtımı için ayrıntılı görevleri</span><span class="sxs-lookup"><span data-stu-id="e5404-461">Detailed tasks for SAP software deployment on a Windows VM</span></span>
<span data-ttu-id="e5404-462">Bu bölümde belirli görevlerle hello yapılandırma ve dağıtım işlemindeki adımları açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="e5404-462">This section has detailed steps for doing specific tasks in hello configuration and deployment process.</span></span>

### <span data-ttu-id="e5404-463"><a name="604bcec2-8b6e-48d2-a944-61b0f5dee2f7"></a>Azure PowerShell cmdlet'lerini dağıtma</span><span class="sxs-lookup"><span data-stu-id="e5404-463"><a name="604bcec2-8b6e-48d2-a944-61b0f5dee2f7"></a>Deploy Azure PowerShell cmdlets</span></span>
1.  <span data-ttu-id="e5404-464">Çok Git[Microsoft Azure indirmeleri](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="e5404-464">Go too[Microsoft Azure Downloads](https://azure.microsoft.com/downloads/).</span></span>
2.  <span data-ttu-id="e5404-465">Altında **komut satırı araçları**altında **PowerShell**seçin **Windows yükleme**.</span><span class="sxs-lookup"><span data-stu-id="e5404-465">Under **Command-line tools**, under **PowerShell**, select **Windows install**.</span></span>
3.  <span data-ttu-id="e5404-466">İndirilen hello dosyası (örneğin, WindowsAzurePowershellGet.3f.3f.3fnew.exe) için hello Microsoft İndirme Yöneticisi iletişim kutusunda seçin **çalıştırmak**.</span><span class="sxs-lookup"><span data-stu-id="e5404-466">In hello Microsoft Download Manager dialog box, for hello downloaded file (for example, WindowsAzurePowershellGet.3f.3f.3fnew.exe), select **Run**.</span></span>
4.  <span data-ttu-id="e5404-467">Microsoft Web Platformu Yükleyicisi (Microsoft Web PI) toorun seçin **Evet**.</span><span class="sxs-lookup"><span data-stu-id="e5404-467">toorun Microsoft Web Platform Installer (Microsoft Web PI), select **Yes**.</span></span>
5.  <span data-ttu-id="e5404-468">Bu görünür benzer bir sayfa:</span><span class="sxs-lookup"><span data-stu-id="e5404-468">A page that looks like this appears:</span></span>

  <span data-ttu-id="e5404-469">![Azure PowerShell cmdlet'leri yükleme sayfası][deployment-guide-figure-500]<a name="figure-5"></a></span><span class="sxs-lookup"><span data-stu-id="e5404-469">![Installation page for Azure PowerShell cmdlets][deployment-guide-figure-500]<a name="figure-5"></a></span></span>

6.  <span data-ttu-id="e5404-470">Seçin **yükleme**ve hello Microsoft Yazılımı Lisans koşulları kabul edin.</span><span class="sxs-lookup"><span data-stu-id="e5404-470">Select **Install**, and then accept hello Microsoft Software License Terms.</span></span>
7.  <span data-ttu-id="e5404-471">PowerShell yüklü.</span><span class="sxs-lookup"><span data-stu-id="e5404-471">PowerShell is installed.</span></span> <span data-ttu-id="e5404-472">Seçin **son** tooclose hello Yükleme Sihirbazı'nı.</span><span class="sxs-lookup"><span data-stu-id="e5404-472">Select **Finish** tooclose hello installation wizard.</span></span>

<span data-ttu-id="e5404-473">Genellikle aylık güncelleştirilen güncelleştirmeleri toohello için PowerShell cmdlet'leri, sık sık denetleyin.</span><span class="sxs-lookup"><span data-stu-id="e5404-473">Check frequently for updates toohello PowerShell cmdlets, which usually are updated monthly.</span></span> <span data-ttu-id="e5404-474">Merhaba en kolay yolu toocheck güncelleştirmeleri için yükleme adımları, adım 5'te gösterilen toohello yükleme sayfasını önceki toodo hello ' dir.</span><span class="sxs-lookup"><span data-stu-id="e5404-474">hello easiest way toocheck for updates is toodo hello preceding installation steps, up toohello installation page shown in step 5.</span></span> <span data-ttu-id="e5404-475">Adım 5'te gösterilen hello sayfasında Hello yayın tarihini ve sürüm numarasını hello cmdlet'leri dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="e5404-475">hello release date and release number of hello cmdlets are included on hello page shown in step 5.</span></span> <span data-ttu-id="e5404-476">SAP notta aksi belirtilmediği sürece [1928533] veya SAP Not [2015553], hello en son sürümü Azure PowerShell cmdlet'leri ile çalışma öneririz.</span><span class="sxs-lookup"><span data-stu-id="e5404-476">Unless stated otherwise in SAP Note [1928533] or SAP Note [2015553], we recommend that you work with hello latest version of Azure PowerShell cmdlets.</span></span>

<span data-ttu-id="e5404-477">Merhaba, bilgisayarınızda yüklü olan Azure PowerShell cmdlet'lerini toocheck hello sürümü bu PowerShell komutunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e5404-477">toocheck hello version of hello Azure PowerShell cmdlets that are installed on your computer, run this PowerShell command:</span></span>
```powershell
Import-Module Azure
(Get-Module Azure).Version
```
<span data-ttu-id="e5404-478">Merhaba sonuç şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="e5404-478">hello result looks like this:</span></span>

<span data-ttu-id="e5404-479">![Azure PowerShell cmdlet sürüm denetiminin sonucu.][deployment-guide-figure-600]
<a name="figure-6"></a></span><span class="sxs-lookup"><span data-stu-id="e5404-479">![Result of Azure PowerShell cmdlet version check][deployment-guide-figure-600]
<a name="figure-6"></a></span></span>

<span data-ttu-id="e5404-480">Bilgisayarınızda yüklü hello Azure cmdlet sürümü hello geçerli sürüm ise hello Yükleme Sihirbazı'nın ilk sayfasında hello ekleyerek belirtir **(yüklü)** toohello ürün başlığı (ekran aşağıdaki hello bakın).</span><span class="sxs-lookup"><span data-stu-id="e5404-480">If hello Azure cmdlet version installed on your computer is hello current version, hello first page of hello installation wizard indicates it by adding **(Installed)** toohello product title (see hello following screenshot).</span></span> <span data-ttu-id="e5404-481">PowerShell Azure cmdlet'lerini güncel değil.</span><span class="sxs-lookup"><span data-stu-id="e5404-481">Your PowerShell Azure cmdlets are up-to-date.</span></span> <span data-ttu-id="e5404-482">tooclose hello Yükleme Sihirbazı, select **çıkış**.</span><span class="sxs-lookup"><span data-stu-id="e5404-482">tooclose hello installation wizard, select **Exit**.</span></span>

<span data-ttu-id="e5404-483">![Azure PowerShell cmdlet'leri bu hello en son sürümünü gösteren Azure PowerShell cmdlet'leri için yükleme sayfasını yüklenir][deployment-guide-figure-700]
<a name="figure-7"></a></span><span class="sxs-lookup"><span data-stu-id="e5404-483">![Installation page for Azure PowerShell cmdlets indicating that hello most recent version of Azure PowerShell cmdlets are installed][deployment-guide-figure-700]
<a name="figure-7"></a></span></span>

### <span data-ttu-id="e5404-484"><a name="1ded9453-1330-442a-86ea-e0fd8ae8cab3"></a>Azure CLI dağıtma</span><span class="sxs-lookup"><span data-stu-id="e5404-484"><a name="1ded9453-1330-442a-86ea-e0fd8ae8cab3"></a>Deploy Azure CLI</span></span>
1.  <span data-ttu-id="e5404-485">Çok Git[Microsoft Azure indirmeleri](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="e5404-485">Go too[Microsoft Azure Downloads](https://azure.microsoft.com/downloads/).</span></span>
2.  <span data-ttu-id="e5404-486">Altında **komut satırı araçları**altında **Azure komut satırı arabirimi**seçin hello **yükleme** işletim sisteminizin bağlantı.</span><span class="sxs-lookup"><span data-stu-id="e5404-486">Under **Command-line tools**, under **Azure command-line interface**, select hello **Install** link for your operating system.</span></span>
3.  <span data-ttu-id="e5404-487">İndirilen hello dosyası (örneğin, WindowsAzureXPlatCLI.3f.3f.3fnew.exe) için hello Microsoft İndirme Yöneticisi iletişim kutusunda seçin **çalıştırmak**.</span><span class="sxs-lookup"><span data-stu-id="e5404-487">In hello Microsoft Download Manager dialog box, for hello downloaded file (for example, WindowsAzureXPlatCLI.3f.3f.3fnew.exe), select **Run**.</span></span>
4.  <span data-ttu-id="e5404-488">Microsoft Web Platformu Yükleyicisi (Microsoft Web PI) toorun seçin **Evet**.</span><span class="sxs-lookup"><span data-stu-id="e5404-488">toorun Microsoft Web Platform Installer (Microsoft Web PI), select **Yes**.</span></span>
5.  <span data-ttu-id="e5404-489">Bu görünür benzer bir sayfa:</span><span class="sxs-lookup"><span data-stu-id="e5404-489">A page that looks like this appears:</span></span>

  <span data-ttu-id="e5404-490">![Azure PowerShell cmdlet'leri yükleme sayfası][deployment-guide-figure-500]<a name="figure-5"></a></span><span class="sxs-lookup"><span data-stu-id="e5404-490">![Installation page for Azure PowerShell cmdlets][deployment-guide-figure-500]<a name="figure-5"></a></span></span>

6.  <span data-ttu-id="e5404-491">Seçin **yükleme**ve hello Microsoft Yazılımı Lisans koşulları kabul edin.</span><span class="sxs-lookup"><span data-stu-id="e5404-491">Select **Install**, and then accept hello Microsoft Software License Terms.</span></span>
7.  <span data-ttu-id="e5404-492">Azure CLI yüklenir.</span><span class="sxs-lookup"><span data-stu-id="e5404-492">Azure CLI is installed.</span></span> <span data-ttu-id="e5404-493">Seçin **son** tooclose hello Yükleme Sihirbazı'nı.</span><span class="sxs-lookup"><span data-stu-id="e5404-493">Select **Finish** tooclose hello installation wizard.</span></span>

<span data-ttu-id="e5404-494">Sık sık güncelleştirmeler tooAzure genellikle her ay güncelleştirilen CLI denetleyin.</span><span class="sxs-lookup"><span data-stu-id="e5404-494">Check frequently for updates tooAzure CLI, which usually is updated monthly.</span></span> <span data-ttu-id="e5404-495">Merhaba en kolay yolu toocheck güncelleştirmeleri için yükleme adımları, adım 5'te gösterilen toohello yükleme sayfasını önceki toodo hello ' dir.</span><span class="sxs-lookup"><span data-stu-id="e5404-495">hello easiest way toocheck for updates is toodo hello preceding installation steps, up toohello installation page shown in step 5.</span></span>


<span data-ttu-id="e5404-496">Bilgisayarınızda yüklü olan Azure CLI toocheck hello sürümü bu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e5404-496">toocheck hello version of Azure CLI that is installed on your computer, run this command:</span></span>
```
azure --version
```

<span data-ttu-id="e5404-497">Merhaba sonuç şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="e5404-497">hello result looks like this:</span></span>

<span data-ttu-id="e5404-498">![Azure CLI sürüm denetiminin sonucu.][deployment-guide-figure-760]
<a name="0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda"></a></span><span class="sxs-lookup"><span data-stu-id="e5404-498">![Result of Azure CLI version check][deployment-guide-figure-760]
<a name="0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda"></a></span></span>

### <span data-ttu-id="e5404-499"><a name="31d9ecd6-b136-4c73-b61e-da4a29bbc9cc"></a>Bir VM tooan şirket içi etki (yalnızca Windows)</span><span class="sxs-lookup"><span data-stu-id="e5404-499"><a name="31d9ecd6-b136-4c73-b61e-da4a29bbc9cc"></a>Join a VM tooan on-premises domain (Windows only)</span></span>
<span data-ttu-id="e5404-500">Bir şirket içi senaryosunda SAP VM'ler dağıtırsanız, şirket içi Active Directory ve DNS Azure'da, burada genişletilmiş onu hello VM'ler bir şirket içi etki alanına katılma beklenir.</span><span class="sxs-lookup"><span data-stu-id="e5404-500">If you deploy SAP VMs in a cross-premises scenario, where on-premises Active Directory and DNS are extended in Azure, it is expected that hello VMs are joining an on-premises domain.</span></span> <span data-ttu-id="e5404-501">VM tooan şirket içi etki alanı toojoin uygulamanız ayrıntılı adımlar hello ve hello gereken ek yazılım toobe bir şirket içi etki alanının üyesi değişir müşteri tarafından.</span><span class="sxs-lookup"><span data-stu-id="e5404-501">hello detailed steps you take toojoin a VM tooan on-premises domain, and hello additional software required toobe a member of an on-premises domain, varies by customer.</span></span> <span data-ttu-id="e5404-502">Genellikle, toojoin VM tooan içi etki alanı, kötü amaçlı yazılımdan koruma yazılımı ve yedekleme ya da izleme yazılım gibi tooinstall ek yazılım gerekir.</span><span class="sxs-lookup"><span data-stu-id="e5404-502">Usually, toojoin a VM tooan on-premises domain, you need tooinstall additional software, like antimalware software, and backup or monitoring software.</span></span>

<span data-ttu-id="e5404-503">Bu senaryoda, ayrıca toomake hello Windows hello Konuk VM yerel sistem hesabı (S-1-5-18) sahip bir VM, ortamınızdaki bir etki alanına katıldığında Internet proxy ayarlarını zorlanır, aynı proxy ayarlarını hello emin gerekir.</span><span class="sxs-lookup"><span data-stu-id="e5404-503">In this scenario, you also need toomake sure that if Internet proxy settings are forced when a VM joins a domain in your environment, hello Windows Local System Account (S-1-5-18) in hello Guest VM has hello same proxy settings.</span></span> <span data-ttu-id="e5404-504">Merhaba kolay tooforce hello proxy etki alanı toosystems hello etki alanındaki geçerli Grup İlkesi kullanarak bir seçenektir.</span><span class="sxs-lookup"><span data-stu-id="e5404-504">hello easiest option is tooforce hello proxy by using a domain Group Policy, which applies toosystems in hello domain.</span></span>

### <span data-ttu-id="e5404-505"><a name="c7cbb0dc-52a4-49db-8e03-83e7edc2927d"></a>İndirme, yükleme ve hello Azure VM Aracısı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="e5404-505"><a name="c7cbb0dc-52a4-49db-8e03-83e7edc2927d"></a>Download, install, and enable hello Azure VM Agent</span></span>
<span data-ttu-id="e5404-506">(Örneğin, hello sysprep veya Windows Sistem Hazırlama aracı kökenli olmayan bir görüntü) genelleştirilmiş olmayan bir işletim sistemi görüntüsünden dağıtılan sanal makineler için toomanually indirme, yükleme ve etkinleştirme hello Azure VM Aracısı gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="e5404-506">For virtual machines that are deployed from an OS image that is not generalized (for example, an image that doesn't originate in hello Windows System Preparation, or sysprep, tool), you need toomanually download, install, and enable hello Azure VM Agent.</span></span>

<span data-ttu-id="e5404-507">Hello Azure Marketi VM'den dağıtırsanız, bu adım gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="e5404-507">If you deploy a VM from hello Azure Marketplace, this step is not required.</span></span> <span data-ttu-id="e5404-508">Hello Azure Marketi görüntülerden hello Azure VM Aracısı zaten var.</span><span class="sxs-lookup"><span data-stu-id="e5404-508">Images from hello Azure Marketplace already have hello Azure VM Agent.</span></span>

#### <span data-ttu-id="e5404-509"><a name="b2db5c9a-a076-42c6-9835-16945868e866"></a>Windows</span><span class="sxs-lookup"><span data-stu-id="e5404-509"><a name="b2db5c9a-a076-42c6-9835-16945868e866"></a>Windows</span></span>
1.  <span data-ttu-id="e5404-510">Hello Azure VM aracısı yükleyin:</span><span class="sxs-lookup"><span data-stu-id="e5404-510">Download hello Azure VM Agent:</span></span>
  1.  <span data-ttu-id="e5404-511">Merhaba karşıdan [Azure VM Aracısı Yükleyici paketi](https://go.microsoft.com/fwlink/?LinkId=394789).</span><span class="sxs-lookup"><span data-stu-id="e5404-511">Download hello [Azure VM Agent installer package](https://go.microsoft.com/fwlink/?LinkId=394789).</span></span>
  2.  <span data-ttu-id="e5404-512">Merhaba VM Aracısı MSI paketini bir kişisel bilgisayar veya sunucu üzerinde yerel olarak depolar.</span><span class="sxs-lookup"><span data-stu-id="e5404-512">Store hello VM Agent MSI package locally on a personal computer or server.</span></span>
2.  <span data-ttu-id="e5404-513">Hello Azure VM aracısı yükleyin:</span><span class="sxs-lookup"><span data-stu-id="e5404-513">Install hello Azure VM Agent:</span></span>
  1.  <span data-ttu-id="e5404-514">Connect toohello Uzak Masaüstü Protokolü (RDP) kullanılarak Azure VM dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="e5404-514">Connect toohello deployed Azure VM by using Remote Desktop Protocol (RDP).</span></span>
  2.  <span data-ttu-id="e5404-515">Bir Windows Gezgini penceresinde hello VM üzerinde ve hello VM Aracısı hello MSI dosyası için select hello hedef dizini açın.</span><span class="sxs-lookup"><span data-stu-id="e5404-515">Open a Windows Explorer window on hello VM and select hello target directory for hello MSI file of hello VM Agent.</span></span>
  3.  <span data-ttu-id="e5404-516">Hello Azure VM Aracısı yükleyici MSI dosyası, yerel bilgisayar/sunucu toohello hedef dizininden hello VM Aracısı VM hello üzerinde sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="e5404-516">Drag hello Azure VM Agent Installer MSI file from your local computer/server toohello target directory of hello VM Agent on hello VM.</span></span>
  4.  <span data-ttu-id="e5404-517">Merhaba VM Hello MSI dosyasına çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e5404-517">Double-click hello MSI file on hello VM.</span></span>
3.  <span data-ttu-id="e5404-518">Birleştirilmiş tooon içi etki alanları olan VM'ler için açıklandığı gibi nihai Internet proxy ayarlarını hello VM, ayrıca toohello Windows yerel sistem hesabı (S-1-5-18) uyguladığınızdan emin olun [hello proxy yapılandırma] [ deployment-guide-configure-proxy].</span><span class="sxs-lookup"><span data-stu-id="e5404-518">For VMs that are joined tooon-premises domains, make sure that eventual Internet proxy settings also apply toohello Windows Local System account (S-1-5-18) in hello VM, as described in [Configure hello proxy][deployment-guide-configure-proxy].</span></span> <span data-ttu-id="e5404-519">Merhaba VM Aracısı bu bağlamda çalıştırır ve toobe mümkün tooconnect tooAzure gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="e5404-519">hello VM Agent runs in this context and needs toobe able tooconnect tooAzure.</span></span>

<span data-ttu-id="e5404-520">Kullanıcı etkileşimi gerekli tooupdate hello Azure VM Aracısı değildir.</span><span class="sxs-lookup"><span data-stu-id="e5404-520">No user interaction is required tooupdate hello Azure VM Agent.</span></span> <span data-ttu-id="e5404-521">Merhaba VM Aracısı otomatik olarak güncelleştirilir ve VM yeniden başlatma gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="e5404-521">hello VM Agent is automatically updated, and does not require a VM restart.</span></span>

#### <span data-ttu-id="e5404-522"><a name="6889ff12-eaaf-4f3c-97e1-7c9edc7f7542"></a>Linux</span><span class="sxs-lookup"><span data-stu-id="e5404-522"><a name="6889ff12-eaaf-4f3c-97e1-7c9edc7f7542"></a>Linux</span></span>
<span data-ttu-id="e5404-523">Linux için komutları tooinstall hello VM aracısı aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="e5404-523">Use hello following commands tooinstall hello VM Agent for Linux:</span></span>

* <span data-ttu-id="e5404-524">**SUSE Linux Enterprise Server (SLES)**</span><span class="sxs-lookup"><span data-stu-id="e5404-524">**SUSE Linux Enterprise Server (SLES)**</span></span>

  ```
  sudo zypper install WALinuxAgent
  ```

* <span data-ttu-id="e5404-525">**Red Hat Enterprise Linux (RHEL)**</span><span class="sxs-lookup"><span data-stu-id="e5404-525">**Red Hat Enterprise Linux (RHEL)**</span></span>

  ```
  sudo yum install WALinuxAgent
  ```

<span data-ttu-id="e5404-526">Merhaba Aracısı zaten yüklüyse, tooupdate hello Azure Linux Aracısı hello bölümünde açıklanan adımları [github'dan VM toohello en son sürümünü güncelleştirme hello Azure Linux Aracısı][virtual-machines-linux-update-agent].</span><span class="sxs-lookup"><span data-stu-id="e5404-526">If hello agent is already installed, tooupdate hello Azure Linux Agent, do hello steps described in [Update hello Azure Linux Agent on a VM toohello latest version from GitHub][virtual-machines-linux-update-agent].</span></span>

### <span data-ttu-id="e5404-527"><a name="baccae00-6f79-4307-ade4-40292ce4e02d"></a>Merhaba proxy ayarlarını yapılandır</span><span class="sxs-lookup"><span data-stu-id="e5404-527"><a name="baccae00-6f79-4307-ade4-40292ce4e02d"></a>Configure hello proxy</span></span>
<span data-ttu-id="e5404-528">tooconfigure hello proxy Windows hello adımlar Linux içinde hello proxy yapılandırma hello yolu farklıdır.</span><span class="sxs-lookup"><span data-stu-id="e5404-528">hello steps you take tooconfigure hello proxy in Windows are different from hello way you configure hello proxy in Linux.</span></span>

#### <a name="windows"></a><span data-ttu-id="e5404-529">Windows</span><span class="sxs-lookup"><span data-stu-id="e5404-529">Windows</span></span>
<span data-ttu-id="e5404-530">Proxy ayarları doğru şekilde hello Internet tooaccess hello yerel sistem hesabı için ayarlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e5404-530">Proxy settings must be set up correctly for hello Local System account tooaccess hello Internet.</span></span> <span data-ttu-id="e5404-531">Proxy ayarlarını Grup İlkesi tarafından ayarlanmamışsa, hello yerel sistem hesabı için hello ayarlarını yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5404-531">If your proxy settings are not set by Group Policy, you can configure hello settings for hello Local System account.</span></span>

1. <span data-ttu-id="e5404-532">Çok Git**Başlat**, girin **gpedit.msc**ve ardından **Enter**.</span><span class="sxs-lookup"><span data-stu-id="e5404-532">Go too**Start**, enter **gpedit.msc**, and then select **Enter**.</span></span>
2. <span data-ttu-id="e5404-533">Seçin **Bilgisayar Yapılandırması** > **Yönetim Şablonları** > **Windows bileşenleri** > **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="e5404-533">Select **Computer Configuration** > **Administrative Templates** > **Windows Components** > **Internet Explorer**.</span></span> <span data-ttu-id="e5404-534">Bu hello ayarı emin olun **proxy ayarlarını makine başına (yerine kullanıcı başına) olun** devre dışı veya yapılandırılmamış.</span><span class="sxs-lookup"><span data-stu-id="e5404-534">Make sure that hello setting **Make proxy settings per-machine (rather than per-user)** is disabled or not configured.</span></span>
3. <span data-ttu-id="e5404-535">İçinde **Denetim Masası**, çok Git**ağ ve Paylaşım Merkezi** > **Internet Seçenekleri**.</span><span class="sxs-lookup"><span data-stu-id="e5404-535">In **Control Panel**, go too**Network and Sharing Center** > **Internet Options**.</span></span>
4. <span data-ttu-id="e5404-536">Merhaba üzerinde **bağlantıları** sekmesi, select hello **LAN Ayarları** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e5404-536">On hello **Connections** tab, select hello **LAN settings** button.</span></span>
5. <span data-ttu-id="e5404-537">Clear hello **ayarları otomatik olarak algıla** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="e5404-537">Clear hello **Automatically detect settings** check box.</span></span>
6. <span data-ttu-id="e5404-538">Select hello **AĞINIZ için bir proxy sunucu kullanacak** onay kutusunu işaretleyin ve ardından hello proxy adresi ve bağlantı noktası girin.</span><span class="sxs-lookup"><span data-stu-id="e5404-538">Select hello **Use a proxy server for your LAN** check box, and then enter hello proxy address and port.</span></span>
7. <span data-ttu-id="e5404-539">Select hello **Gelişmiş** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e5404-539">Select hello **Advanced** button.</span></span>
8. <span data-ttu-id="e5404-540">Merhaba, **özel durumları** kutusuna, başlangıç IP adresi girin **168.63.129.16**.</span><span class="sxs-lookup"><span data-stu-id="e5404-540">In hello **Exceptions** box, enter hello IP address **168.63.129.16**.</span></span> <span data-ttu-id="e5404-541">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="e5404-541">Select **OK**.</span></span>


#### <a name="linux"></a><span data-ttu-id="e5404-542">Linux</span><span class="sxs-lookup"><span data-stu-id="e5404-542">Linux</span></span>
<span data-ttu-id="e5404-543">Merhaba yapılandırma dosyasındaki hello konumda bulunan Microsoft Azure Konuk Aracısı Hello doğru proxy yapılandırma \\vb.\\waagent.conf.</span><span class="sxs-lookup"><span data-stu-id="e5404-543">Configure hello correct proxy in hello configuration file of hello Microsoft Azure Guest Agent, which is located at \\etc\\waagent.conf.</span></span>

<span data-ttu-id="e5404-544">Şu parametreler hello ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="e5404-544">Set hello following parameters:</span></span>

1.  <span data-ttu-id="e5404-545">**HTTP proxy konağını**.</span><span class="sxs-lookup"><span data-stu-id="e5404-545">**HTTP proxy host**.</span></span> <span data-ttu-id="e5404-546">Örneğin, çok ayarlamak**proxy.corp.local**.</span><span class="sxs-lookup"><span data-stu-id="e5404-546">For example, set it too**proxy.corp.local**.</span></span>
  ```
  HttpProxy.Host=<proxy host>

  ```
2.  <span data-ttu-id="e5404-547">**HTTP proxy bağlantı noktası**.</span><span class="sxs-lookup"><span data-stu-id="e5404-547">**HTTP proxy port**.</span></span> <span data-ttu-id="e5404-548">Örneğin, çok ayarlamak**80**.</span><span class="sxs-lookup"><span data-stu-id="e5404-548">For example, set it too**80**.</span></span>
  ```
  HttpProxy.Port=<port of hello proxy host>

  ```
3.  <span data-ttu-id="e5404-549">Merhaba aracıyı yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="e5404-549">Restart hello agent.</span></span>

  ```
  sudo service waagent restart
  ```

<span data-ttu-id="e5404-550">Merhaba proxy ayarları \\vb.\\waagent.conf gerekli toohello VM uzantıları de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="e5404-550">hello proxy settings in \\etc\\waagent.conf also apply toohello required VM extensions.</span></span> <span data-ttu-id="e5404-551">Toouse istiyorsanız Azure depoları Merhaba, hello trafiği toothese depoları değil olduğuna, şirket içi intranetiniz üzerinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="e5404-551">If you want toouse hello Azure repositories, make sure that hello traffic toothese repositories is not going through your on-premises intranet.</span></span> <span data-ttu-id="e5404-552">Kullanıcı tanımlı oluşturduysanız yollar tooenable zorlamalı tünel, trafik toohello depoları yönlendiren bir rota eklediğinizden emin olun doğrudan toohello Internet ve siteden siteye VPN bağlantısı üzerinden değil.</span><span class="sxs-lookup"><span data-stu-id="e5404-552">If you created user-defined routes tooenable forced tunneling, make sure that you add a route that routes traffic toohello repositories directly toohello Internet, and not through your site-to-site VPN connection.</span></span>

* <span data-ttu-id="e5404-553">**SLES**</span><span class="sxs-lookup"><span data-stu-id="e5404-553">**SLES**</span></span>

  <span data-ttu-id="e5404-554">Başlangıç IP adresi listelenen için tooadd yollar da gerekir \\vb.\\regionserverclnt.cfg.</span><span class="sxs-lookup"><span data-stu-id="e5404-554">You also need tooadd routes for hello IP addresses listed in \\etc\\regionserverclnt.cfg.</span></span> <span data-ttu-id="e5404-555">Merhaba aşağıdaki şekilde bir örnek gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="e5404-555">hello following figure shows an example:</span></span>

  ![Zorlamalı tünel oluşturma][deployment-guide-figure-50]


* <span data-ttu-id="e5404-557">**RHEL**</span><span class="sxs-lookup"><span data-stu-id="e5404-557">**RHEL**</span></span>

  <span data-ttu-id="e5404-558">Merhaba konakları Hello IP adreslerini listelenen için tooadd yollar da gerekir \\vb.\\yum.repos.d\\rhui yük dengeleyicileri.</span><span class="sxs-lookup"><span data-stu-id="e5404-558">You also need tooadd routes for hello IP addresses of hello hosts listed in \\etc\\yum.repos.d\\rhui-load-balancers.</span></span> <span data-ttu-id="e5404-559">Örneğin, Şekil önceki hello bakın.</span><span class="sxs-lookup"><span data-stu-id="e5404-559">For an example, see hello preceding figure.</span></span>

<span data-ttu-id="e5404-560">Kullanıcı tanımlı yollar hakkında daha fazla bilgi için bkz: [kullanıcı tanımlı yollar ve IP iletimini][virtual-networks-udr-overview].</span><span class="sxs-lookup"><span data-stu-id="e5404-560">For more information about user-defined routes, see [User-defined routes and IP forwarding][virtual-networks-udr-overview].</span></span>

### <span data-ttu-id="e5404-561"><a name="d98edcd3-f2a1-49f7-b26a-07448ceb60ca"></a>Hello Azure Gelişmiş izleme uzantısı SAP yapılandırın</span><span class="sxs-lookup"><span data-stu-id="e5404-561"><a name="d98edcd3-f2a1-49f7-b26a-07448ceb60ca"></a>Configure hello Azure Enhanced Monitoring Extension for SAP</span></span>
<span data-ttu-id="e5404-562">Ne zaman hazırlıklı hello VM açıklandığı gibi [VM'ler Azure üzerinde SAP için dağıtım senaryoları][deployment-guide-3], hello Azure VM Aracısı hello sanal makineye yüklenir.</span><span class="sxs-lookup"><span data-stu-id="e5404-562">When you've prepared hello VM as described in [Deployment scenarios of VMs for SAP on Azure][deployment-guide-3], hello Azure VM Agent is installed on hello virtual machine.</span></span> <span data-ttu-id="e5404-563">Merhaba sonraki toodeploy hello Azure Gelişmiş izleme uzantısı hello Azure uzantısı deposuna hello genel Azure veri merkezleri içinde kullanılabilir SAP adımdır.</span><span class="sxs-lookup"><span data-stu-id="e5404-563">hello next step is toodeploy hello Azure Enhanced Monitoring Extension for SAP, which is available in hello Azure Extension Repository in hello global Azure datacenters.</span></span> <span data-ttu-id="e5404-564">Daha fazla bilgi için bkz: [Azure sanal makineleri planlama ve uygulama Linux üzerinde SAP için][planning-guide-9.1].</span><span class="sxs-lookup"><span data-stu-id="e5404-564">For more information, see [Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide-9.1].</span></span>

<span data-ttu-id="e5404-565">PowerShell veya Azure CLI tooinstall kullanın ve hello Azure Gelişmiş izleme uzantısı SAP yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e5404-565">You can use PowerShell or Azure CLI tooinstall and configure hello Azure Enhanced Monitoring Extension for SAP.</span></span> <span data-ttu-id="e5404-566">Windows makine kullanarak bir Windows veya Linux VM tooinstall hello uzantısını görmek [Azure PowerShell][deployment-guide-4.5.1].</span><span class="sxs-lookup"><span data-stu-id="e5404-566">tooinstall hello extension on a Windows or Linux VM by using a Windows machine, see [Azure PowerShell][deployment-guide-4.5.1].</span></span> <span data-ttu-id="e5404-567">bir Linux Masaüstü kullanarak bir Linux VM tooinstall hello uzantısı bkz [Azure CLI][deployment-guide-4.5.2].</span><span class="sxs-lookup"><span data-stu-id="e5404-567">tooinstall hello extension on a Linux VM by using a Linux desktop, see [Azure CLI][deployment-guide-4.5.2].</span></span>

#### <span data-ttu-id="e5404-568"><a name="987cf279-d713-4b4c-8143-6b11589bb9d4"></a>Linux ve Windows VM'ler için Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e5404-568"><a name="987cf279-d713-4b4c-8143-6b11589bb9d4"></a>Azure PowerShell for Linux and Windows VMs</span></span>
<span data-ttu-id="e5404-569">tooinstall hello Gelişmiş izleme uzantısı SAP için Azure PowerShell kullanarak:</span><span class="sxs-lookup"><span data-stu-id="e5404-569">tooinstall hello Azure Enhanced Monitoring Extension for SAP by using PowerShell:</span></span>

1. <span data-ttu-id="e5404-570">Merhaba hello Azure PowerShell cmdlet'ini en son sürümünü yüklediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="e5404-570">Make sure that you have installed hello latest version of hello Azure PowerShell cmdlet.</span></span> <span data-ttu-id="e5404-571">Daha fazla bilgi için bkz: [dağıtımı Azure PowerShell cmdlet'lerini][deployment-guide-4.1].</span><span class="sxs-lookup"><span data-stu-id="e5404-571">For more information, see [Deploying Azure PowerShell cmdlets][deployment-guide-4.1].</span></span>  
2. <span data-ttu-id="e5404-572">Merhaba aşağıdaki PowerShell cmdlet'ini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e5404-572">Run hello following PowerShell cmdlet.</span></span>
  <span data-ttu-id="e5404-573">Kullanılabilir ortamlar listesi için çalıştırın `commandlet Get-AzureRmEnvironment`.</span><span class="sxs-lookup"><span data-stu-id="e5404-573">For a list of available environments, run `commandlet Get-AzureRmEnvironment`.</span></span> <span data-ttu-id="e5404-574">Ortak Azure, ortamınızı toouse istiyorsanız **AzureCloud**.</span><span class="sxs-lookup"><span data-stu-id="e5404-574">If you want toouse public Azure, your environment is **AzureCloud**.</span></span> <span data-ttu-id="e5404-575">Çin'de Azure için seçin **AzureChinaCloud**.</span><span class="sxs-lookup"><span data-stu-id="e5404-575">For Azure in China, select **AzureChinaCloud**.</span></span>


      ```powershell
      $env = Get-AzureRmEnvironment -Name <name of hello environment>
      Login-AzureRmAccount -Environment $env
      Set-AzureRmContext -SubscriptionName <subscription name>

      Set-AzureRmVMAEMExtension -ResourceGroupName <resource group name> -VMName <virtual machine name>
      ```

<span data-ttu-id="e5404-576">Hesap verilerinizi girip hello Azure sanal makinesi tanımlamak sonra hello betik gerekli hello uzantıları dağıtır ve gerekli hello özelliklerini etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="e5404-576">After you enter your account data and identify hello Azure virtual machine, hello script deploys hello required extensions and enables hello required features.</span></span> <span data-ttu-id="e5404-577">Bu işlem birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="e5404-577">This can take several minutes.</span></span>
<span data-ttu-id="e5404-578">Hakkında daha fazla bilgi için `Set-AzureRmVMAEMExtension`, bkz: [kümesi AzureRmVMAEMExtension][msdn-set-azurermvmaemextension].</span><span class="sxs-lookup"><span data-stu-id="e5404-578">For more information about `Set-AzureRmVMAEMExtension`, see [Set-AzureRmVMAEMExtension][msdn-set-azurermvmaemextension].</span></span>

![SAP özgü aktarılmadığı Azure cmdlet kümesi AzureRmVMAEMExtension][deployment-guide-figure-900]

<span data-ttu-id="e5404-580">Merhaba `Set-AzureRmVMAEMExtension` yapılandırma tüm hello adımları tooconfigure konak için SAP izleme yapar.</span><span class="sxs-lookup"><span data-stu-id="e5404-580">hello `Set-AzureRmVMAEMExtension` configuration does all hello steps tooconfigure host monitoring for SAP.</span></span>

<span data-ttu-id="e5404-581">Merhaba komut dosyası çıkışını bilgisinden hello içerir:</span><span class="sxs-lookup"><span data-stu-id="e5404-581">hello script output includes hello following information:</span></span>

* <span data-ttu-id="e5404-582">Onay, hello temel VHD (ile Merhaba OS) ve tüm ek VHD'leri izleme VM yapılandırılmış toohello bağladı.</span><span class="sxs-lookup"><span data-stu-id="e5404-582">Confirmation that monitoring for hello base VHD (with hello OS) and all additional VHDs mounted toohello VM has been configured.</span></span>
* <span data-ttu-id="e5404-583">Merhaba sonraki iki iletileri belirli bir depolama hesabı için depolama ölçümleri hello yapılandırmasını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="e5404-583">hello next two messages confirm hello configuration of Storage Metrics for a specific storage account.</span></span>
* <span data-ttu-id="e5404-584">Tek satırlık bir çıktı hello gerçek güncelleştirme hello izleme yapılandırmasının hello durumunu verir.</span><span class="sxs-lookup"><span data-stu-id="e5404-584">One line of output gives hello status of hello actual update of hello monitoring configuration.</span></span>
* <span data-ttu-id="e5404-585">Başka bir satır çıktı hello yapılandırmayı dağıtılan ya da güncelleştirilmiş onaylar.</span><span class="sxs-lookup"><span data-stu-id="e5404-585">Another line of output confirms that hello configuration has been deployed or updated.</span></span>
* <span data-ttu-id="e5404-586">çıktının son satırında Hello bilgilendirme amaçlıdır.</span><span class="sxs-lookup"><span data-stu-id="e5404-586">hello last line of output is informational.</span></span> <span data-ttu-id="e5404-587">Sınama hello izleme yapılandırma seçeneklerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="e5404-587">It shows your options for testing hello monitoring configuration.</span></span>

<span data-ttu-id="e5404-588">Gelişmiş Azure Monitoring tüm adımları başarıyla yürütüldü ve hello gerekli verileri, o hello Azure altyapısı sağlar toocheck devam hello Gelişmiş izleme uzantısı SAP, Azure için hello hazırlık denetimi ile açıklandığı gibi [Gelişmiş Azure izlemesi için SAP için hazırlık denetimi][deployment-guide-5.1].</span><span class="sxs-lookup"><span data-stu-id="e5404-588">toocheck that all steps of Azure Enhanced Monitoring have been executed successfully, and that hello Azure Infrastructure provides hello necessary data, proceed with hello readiness check for hello Azure Enhanced Monitoring Extension for SAP, as described in [Readiness check for Azure Enhanced Monitoring for SAP][deployment-guide-5.1].</span></span> <span data-ttu-id="e5404-589">Azure tanılama toocollect hello ilgili verileri 15-30 dakika bekleyin.</span><span class="sxs-lookup"><span data-stu-id="e5404-589">Wait 15-30 minutes for Azure Diagnostics toocollect hello relevant data.</span></span>

#### <span data-ttu-id="e5404-590"><a name="408f3779-f422-4413-82f8-c57a23b4fc2f"></a>Linux VM'ler için Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e5404-590"><a name="408f3779-f422-4413-82f8-c57a23b4fc2f"></a>Azure CLI for Linux VMs</span></span>
<span data-ttu-id="e5404-591">tooinstall hello Azure CLI kullanarak Azure Gelişmiş izleme uzantısı SAP:</span><span class="sxs-lookup"><span data-stu-id="e5404-591">tooinstall hello Azure Enhanced Monitoring Extension for SAP by using Azure CLI:</span></span>

1. <span data-ttu-id="e5404-592">Bölümünde açıklandığı gibi Azure CLI yükleme [yükleme hello Azure CLI][azure-cli].</span><span class="sxs-lookup"><span data-stu-id="e5404-592">Install Azure CLI, as described in [Install hello Azure CLI][azure-cli].</span></span>
2. <span data-ttu-id="e5404-593">Azure hesabınızla oturum açın:</span><span class="sxs-lookup"><span data-stu-id="e5404-593">Sign in with your Azure account:</span></span>

  ```
  azure login
  ```

3. <span data-ttu-id="e5404-594">TooAzure Resource Manager moduna geçin:</span><span class="sxs-lookup"><span data-stu-id="e5404-594">Switch tooAzure Resource Manager mode:</span></span>

  ```
  azure config mode arm
  ```

4. <span data-ttu-id="e5404-595">Azure Gelişmiş izlemeyi etkinleştir:</span><span class="sxs-lookup"><span data-stu-id="e5404-595">Enable Azure Enhanced Monitoring:</span></span>

  ```
  azure vm enable-aem <resource-group-name> <vm-name>
  ```

5. <span data-ttu-id="e5404-596">Bu hello Azure Gelişmiş izleme uzantısı hello Azure Linux VM etkin olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="e5404-596">Verify that hello Azure Enhanced Monitoring Extension is active on hello Azure Linux VM.</span></span> <span data-ttu-id="e5404-597">Onay olup dosya hello \\var\\lib\\AzureEnhancedMonitor\\PerfCounters bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e5404-597">Check whether hello file \\var\\lib\\AzureEnhancedMonitor\\PerfCounters exists.</span></span> <span data-ttu-id="e5404-598">Bir komut isteminde varsa Azure Gelişmiş İzleyicisi Merhaba tarafından toplanan bu komut toodisplay bilgilerini çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e5404-598">If it exists, at a command prompt, run this command toodisplay information collected by hello Azure Enhanced Monitor:</span></span>
```
cat /var/lib/AzureEnhancedMonitor/PerfCounters
```

<span data-ttu-id="e5404-599">Merhaba çıktı şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="e5404-599">hello output looks like this:</span></span>
```
2;cpu;Current Hw Frequency;;0;2194.659;MHz;60;1444036656;saplnxmon;
2;cpu;Max Hw Frequency;;0;2194.659;MHz;0;1444036656;saplnxmon;
…
…
```

## <span data-ttu-id="e5404-600"><a name="564adb4f-5c95-4041-9616-6635e83a810b"></a>Denetim ve uçtan uca izleme için sorun giderme</span><span class="sxs-lookup"><span data-stu-id="e5404-600"><a name="564adb4f-5c95-4041-9616-6635e83a810b"></a>Checks and troubleshooting for end-to-end monitoring</span></span>
<span data-ttu-id="e5404-601">Azure VM dağıtılan ve hello ilgili Azure izleme altyapıyı ayarladıktan sonra hello Azure Gelişmiş izleme uzantısı hello bileşenlerinin tümünü beklendiği gibi çalışıp çalışmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="e5404-601">After you have deployed your Azure VM and set up hello relevant Azure monitoring infrastructure, check whether all hello components of hello Azure Enhanced Monitoring Extension are working as expected.</span></span>

<span data-ttu-id="e5404-602">Bölümünde açıklandığı gibi hello Azure Gelişmiş izleme uzantısı SAP için Hello hazırlık denetimini Çalıştır [hello Azure Gelişmiş izleme uzantısı SAP için hazırlık denetimi][deployment-guide-5.1].</span><span class="sxs-lookup"><span data-stu-id="e5404-602">Run hello readiness check for hello Azure Enhanced Monitoring Extension for SAP as described in [Readiness check for hello Azure Enhanced Monitoring Extension for SAP][deployment-guide-5.1].</span></span> <span data-ttu-id="e5404-603">Tüm hazırlık denetimi sonuçları pozitif ve tüm ilgili performans sayaçları Tamam görünür, Azure İzleme'ı başarıyla kuruldu.</span><span class="sxs-lookup"><span data-stu-id="e5404-603">If all readiness check results are positive and all relevant performance counters appear OK, Azure monitoring successfully set up.</span></span> <span data-ttu-id="e5404-604">SAP konak hello SAP notları açıklanan Aracısı hello yüklemesi devam edebilmeniz [SAP kaynakları][deployment-guide-2.2].</span><span class="sxs-lookup"><span data-stu-id="e5404-604">You can proceed with hello installation of SAP Host Agent described in hello SAP Notes in [SAP resources][deployment-guide-2.2].</span></span> <span data-ttu-id="e5404-605">Merhaba hazırlık denetimi açıklandığı gibi hello Azure izleme altyapı için hello sistem durumu denetimi Çalıştır sayaçları eksik olduğunu gösteriyorsa [izleme Azure altyapısı yapılandırması için sistem durumu denetimi] [ deployment-guide-5.2].</span><span class="sxs-lookup"><span data-stu-id="e5404-605">If hello readiness check indicates that counters are missing, run hello health check for hello Azure monitoring infrastructure, as described in [Health check for Azure monitoring infrastructure configuration][deployment-guide-5.2].</span></span> <span data-ttu-id="e5404-606">Daha fazla sorun giderme seçenekleri için bkz: [Azure sorun giderme için SAP izleme][deployment-guide-5.3].</span><span class="sxs-lookup"><span data-stu-id="e5404-606">For more troubleshooting options, see [Troubleshooting Azure monitoring for SAP][deployment-guide-5.3].</span></span>

### <span data-ttu-id="e5404-607"><a name="bb61ce92-8c5c-461f-8c53-39f5e5ed91f2"></a>Hello Azure Gelişmiş izleme uzantısı SAP hazır olma durumunu denetle</span><span class="sxs-lookup"><span data-stu-id="e5404-607"><a name="bb61ce92-8c5c-461f-8c53-39f5e5ed91f2"></a>Readiness check for hello Azure Enhanced Monitoring Extension for SAP</span></span>
<span data-ttu-id="e5404-608">Bu onay SAP uygulamanız içinde görünür tüm performans ölçümlerinin altyapısını izleme Azure arka plandaki hello tarafından sağlanan emin olur.</span><span class="sxs-lookup"><span data-stu-id="e5404-608">This check makes sure that all performance metrics that appear inside your SAP application are provided by hello underlying Azure monitoring infrastructure.</span></span>

#### <a name="run-hello-readiness-check-on-a-windows-vm"></a><span data-ttu-id="e5404-609">Bir Windows VM üzerinde Hello hazırlık denetimi Çalıştır</span><span class="sxs-lookup"><span data-stu-id="e5404-609">Run hello readiness check on a Windows VM</span></span>

1.  <span data-ttu-id="e5404-610">Toohello Azure sanal makinesi oturum (bir yönetici hesabı kullanarak gerekli değildir).</span><span class="sxs-lookup"><span data-stu-id="e5404-610">Sign in toohello Azure virtual machine (using an admin account is not necessary).</span></span>
2.  <span data-ttu-id="e5404-611">Bir komut istemi penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="e5404-611">Open a Command Prompt window.</span></span>
3.  <span data-ttu-id="e5404-612">Merhaba komut isteminde hello dizin toohello yükleme klasörü hello Azure Gelişmiş izleme uzantısı SAP değiştirin: C:\\paketleri\\eklentileri\\ Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;sürüm >\\bırak</span><span class="sxs-lookup"><span data-stu-id="e5404-612">At hello command prompt, change hello directory toohello installation folder of hello Azure Enhanced Monitoring Extension for SAP: C:\\Packages\\Plugins\\Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;version>\\drop</span></span>

  <span data-ttu-id="e5404-613">Merhaba *sürüm* hello yolu toohello izleme uzantısı değişebilir.</span><span class="sxs-lookup"><span data-stu-id="e5404-613">hello *version* in hello path toohello monitoring extension might vary.</span></span> <span data-ttu-id="e5404-614">Klasörleri birden fazla sürümünü hello izleme uzantısı hello yükleme klasöründe, onay hello yapılandırmasını hello AzureEnhancedMonitoring Windows hizmeti için görürseniz ve olarak anahtar toohello klasörü belirtilen *yolu tooexecutable* .</span><span class="sxs-lookup"><span data-stu-id="e5404-614">If you see folders for multiple versions of hello monitoring extension in hello installation folder, check hello configuration of hello AzureEnhancedMonitoring Windows service, and then switch toohello folder indicated as *Path tooexecutable*.</span></span>

  ![Hizmet çalışıyor özelliklerini Azure Gelişmiş izleme uzantısı SAP hello][deployment-guide-figure-1000]

4.  <span data-ttu-id="e5404-616">Merhaba komut isteminde çalıştırmak **azperflib.exe** hiçbir parametre olmadan.</span><span class="sxs-lookup"><span data-stu-id="e5404-616">At hello command prompt, run **azperflib.exe** without any parameters.</span></span>

  > [!NOTE]
  > <span data-ttu-id="e5404-617">Azperflib.exe bir döngüde çalışır ve her 60 saniyede toplanan hello sayaçlarını güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="e5404-617">Azperflib.exe runs in a loop and updates hello collected counters every 60 seconds.</span></span> <span data-ttu-id="e5404-618">tooend hello döngü, Kapat hello komut istemi penceresi.</span><span class="sxs-lookup"><span data-stu-id="e5404-618">tooend hello loop, close hello Command Prompt window.</span></span>
  >
  >

<span data-ttu-id="e5404-619">Hello Azure Gelişmiş izleme uzantısı yüklü değil ya da hello AzureEnhancedMonitoring hizmeti çalışmıyorsa, hello uzantısı düzgün yapılandırılmamış.</span><span class="sxs-lookup"><span data-stu-id="e5404-619">If hello Azure Enhanced Monitoring Extension is not installed, or hello AzureEnhancedMonitoring service is not running, hello extension has not been configured correctly.</span></span> <span data-ttu-id="e5404-620">Nasıl toodeploy hello uzantısı hakkında ayrıntılı bilgi için bkz: [sorun giderme için SAP Azure izleme altyapısının hello][deployment-guide-5.3].</span><span class="sxs-lookup"><span data-stu-id="e5404-620">For detailed information about how toodeploy hello extension, see [Troubleshooting hello Azure monitoring infrastructure for SAP][deployment-guide-5.3].</span></span>

##### <a name="check-hello-output-of-azperflibexe"></a><span data-ttu-id="e5404-621">Azperflib.exe onay hello çıktısı</span><span class="sxs-lookup"><span data-stu-id="e5404-621">Check hello output of azperflib.exe</span></span>
<span data-ttu-id="e5404-622">Tüm Azure performans sayaçları için SAP doldurulmuş Azperflib.exe çıktısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="e5404-622">Azperflib.exe output shows all populated Azure performance counters for SAP.</span></span> <span data-ttu-id="e5404-623">Toplanan sayaçlarının listesi hello Hello altındaki hello durumunu Azure İzleme Özeti ve sistem durumu gösterge gösterir.</span><span class="sxs-lookup"><span data-stu-id="e5404-623">At hello bottom of hello list of collected counters, a summary and health indicator show hello status of Azure monitoring.</span></span>

<span data-ttu-id="e5404-624">![Sistem durumu denetimi herhangi bir sorun mevcut olduğunu gösteren azperflib.exe çalıştırarak çıktısı][deployment-guide-figure-1100]
<a name="figure-11"></a></span><span class="sxs-lookup"><span data-stu-id="e5404-624">![Output of health check by executing azperflib.exe, which indicates that no problems exist][deployment-guide-figure-1100]
<a name="figure-11"></a></span></span>

<span data-ttu-id="e5404-625">Merhaba döndürülen hello sonuç denetleme **sayaçları toplam** bildirilen boş olarak ve için çıktı **sistem durumu**şekil önceki hello gösterilen.</span><span class="sxs-lookup"><span data-stu-id="e5404-625">Check hello result returned for hello **Counters total** output, which is reported as empty, and for **Health status**, shown in hello preceding figure.</span></span>

<span data-ttu-id="e5404-626">Merhaba elde edilen değerleri aşağıdaki gibi yorumlar:</span><span class="sxs-lookup"><span data-stu-id="e5404-626">Interpret hello resulting values as follows:</span></span>

| <span data-ttu-id="e5404-627">Azperflib.exe sonuç değerleri</span><span class="sxs-lookup"><span data-stu-id="e5404-627">Azperflib.exe result values</span></span> | <span data-ttu-id="e5404-628">Azure sistem durumunu izleme</span><span class="sxs-lookup"><span data-stu-id="e5404-628">Azure monitoring health status</span></span> |
| --- | --- |
| <span data-ttu-id="e5404-629">**API çağrıları - mevcut değil**</span><span class="sxs-lookup"><span data-stu-id="e5404-629">**API Calls - not available**</span></span> | <span data-ttu-id="e5404-630">Kullanılabilir değil sayaçları ya da geçerli değil toohello sanal makine yapılandırması olabilir veya hatalardır.</span><span class="sxs-lookup"><span data-stu-id="e5404-630">Counters that are not available might be either not applicable toohello virtual machine configuration, or are errors.</span></span> <span data-ttu-id="e5404-631">Bkz: **sistem durumu**.</span><span class="sxs-lookup"><span data-stu-id="e5404-631">See **Health status**.</span></span> |
| <span data-ttu-id="e5404-632">**Sayaçları toplam - boş**</span><span class="sxs-lookup"><span data-stu-id="e5404-632">**Counters total - empty**</span></span> |<span data-ttu-id="e5404-633">iki Azure depolama sayaçları aşağıdaki hello boş olabilir:</span><span class="sxs-lookup"><span data-stu-id="e5404-633">hello following two Azure storage counters can be empty:</span></span> <ul><li><span data-ttu-id="e5404-634">Depolama alanından Op gecikme okuma sunucu milisaniye</span><span class="sxs-lookup"><span data-stu-id="e5404-634">Storage Read Op Latency Server msec</span></span></li><li><span data-ttu-id="e5404-635">Depolama alanından Op gecikme okuma E2E milisaniye</span><span class="sxs-lookup"><span data-stu-id="e5404-635">Storage Read Op Latency E2E msec</span></span></li></ul><span data-ttu-id="e5404-636">Diğer tüm sayaçları değerlere sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e5404-636">All other counters must have values.</span></span> |
| <span data-ttu-id="e5404-637">**Sistem durumu**</span><span class="sxs-lookup"><span data-stu-id="e5404-637">**Health status**</span></span> |<span data-ttu-id="e5404-638">Yalnızca Tamam IF dönüş durumu **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="e5404-638">Only OK if return status shows **OK**.</span></span> |
| <span data-ttu-id="e5404-639">**Tanılama**</span><span class="sxs-lookup"><span data-stu-id="e5404-639">**Diagnostics**</span></span> |<span data-ttu-id="e5404-640">Sistem durumu hakkında ayrıntılı bilgiler.</span><span class="sxs-lookup"><span data-stu-id="e5404-640">Detailed information about health status.</span></span> |

<span data-ttu-id="e5404-641">Merhaba, **sistem durumu** değeri değil **Tamam**, hello yönergeleri izleyin [izleme Azure altyapısı yapılandırması için sistem durumu denetimi] [ deployment-guide-5.2].</span><span class="sxs-lookup"><span data-stu-id="e5404-641">If hello **Health status** value is not **OK**, follow hello instructions in [Health check for Azure monitoring infrastructure configuration][deployment-guide-5.2].</span></span>

#### <a name="run-hello-readiness-check-on-a-linux-vm"></a><span data-ttu-id="e5404-642">Bir Linux VM üzerinde Hello hazırlık denetimi Çalıştır</span><span class="sxs-lookup"><span data-stu-id="e5404-642">Run hello readiness check on a Linux VM</span></span>

1.  <span data-ttu-id="e5404-643">SSH kullanarak toohello Azure sanal makinesine bağlanın.</span><span class="sxs-lookup"><span data-stu-id="e5404-643">Connect toohello Azure Virtual Machine by using SSH.</span></span>

2.  <span data-ttu-id="e5404-644">Hello Azure Gelişmiş izleme uzantısı Hello çıktısını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="e5404-644">Check hello output of hello Azure Enhanced Monitoring Extension.</span></span>

  <span data-ttu-id="e5404-645">a.</span><span class="sxs-lookup"><span data-stu-id="e5404-645">a.</span></span>  <span data-ttu-id="e5404-646">`more /var/lib/AzureEnhancedMonitor/PerfCounters` öğesini çalıştırın</span><span class="sxs-lookup"><span data-stu-id="e5404-646">Run `more /var/lib/AzureEnhancedMonitor/PerfCounters`</span></span>

   <span data-ttu-id="e5404-647">**Beklenen sonucu**: performans sayaçları listesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="e5404-647">**Expected result**: Returns list of performance counters.</span></span> <span data-ttu-id="e5404-648">Merhaba dosya boş olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="e5404-648">hello file should not be empty.</span></span>

 <span data-ttu-id="e5404-649">b.</span><span class="sxs-lookup"><span data-stu-id="e5404-649">b.</span></span> <span data-ttu-id="e5404-650">`cat /var/lib/AzureEnhancedMonitor/PerfCounters | grep Error` öğesini çalıştırın</span><span class="sxs-lookup"><span data-stu-id="e5404-650">Run `cat /var/lib/AzureEnhancedMonitor/PerfCounters | grep Error`</span></span>

   <span data-ttu-id="e5404-651">**Beklenen sonucu**: hello hata olduğu döndürür tek bir çizgi **hiçbiri**, örneğin, **3; config; Hata; 0; 0; yok; 0; 1456416792; tst servercs;**</span><span class="sxs-lookup"><span data-stu-id="e5404-651">**Expected result**: Returns one line where hello error is **none**, for example, **3;config;Error;;0;0;none;0;1456416792;tst-servercs;**</span></span>

  <span data-ttu-id="e5404-652">c.</span><span class="sxs-lookup"><span data-stu-id="e5404-652">c.</span></span> <span data-ttu-id="e5404-653">`more /var/lib/AzureEnhancedMonitor/LatestErrorRecord` öğesini çalıştırın</span><span class="sxs-lookup"><span data-stu-id="e5404-653">Run `more /var/lib/AzureEnhancedMonitor/LatestErrorRecord`</span></span>

    <span data-ttu-id="e5404-654">**Beklenen sonucu**: boş olarak döndürür veya yok.</span><span class="sxs-lookup"><span data-stu-id="e5404-654">**Expected result**: Returns as empty or does not exist.</span></span>

<span data-ttu-id="e5404-655">Merhaba önceki onay başarılı olmazsa, bu ek denetimler çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e5404-655">If hello preceding check was not successful, run these additional checks:</span></span>

1.  <span data-ttu-id="e5404-656">Bu hello waagent yüklü ve etkin olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="e5404-656">Make sure that hello waagent is installed and enabled.</span></span>

  <span data-ttu-id="e5404-657">a.</span><span class="sxs-lookup"><span data-stu-id="e5404-657">a.</span></span>  <span data-ttu-id="e5404-658">`sudo ls -al /var/lib/waagent/` öğesini çalıştırın</span><span class="sxs-lookup"><span data-stu-id="e5404-658">Run `sudo ls -al /var/lib/waagent/`</span></span>

      <span data-ttu-id="e5404-659">**Beklenen sonucu**: hello hello waagent dizinin içeriğini listeler.</span><span class="sxs-lookup"><span data-stu-id="e5404-659">**Expected result**: Lists hello content of hello waagent directory.</span></span>

  <span data-ttu-id="e5404-660">b.</span><span class="sxs-lookup"><span data-stu-id="e5404-660">b.</span></span>  <span data-ttu-id="e5404-661">`ps -ax | grep waagent` öğesini çalıştırın</span><span class="sxs-lookup"><span data-stu-id="e5404-661">Run `ps -ax | grep waagent`</span></span>

   <span data-ttu-id="e5404-662">**Beklenen sonucu**: için benzer bir giriş görüntüler:`python /usr/sbin/waagent -daemon`</span><span class="sxs-lookup"><span data-stu-id="e5404-662">**Expected result**: Displays one entry similar to: `python /usr/sbin/waagent -daemon`</span></span>

2. <span data-ttu-id="e5404-663">Linux tanılama uzantısı yüklü ve etkin bu hello emin olun.</span><span class="sxs-lookup"><span data-stu-id="e5404-663">Make sure that hello Linux Diagnostic Extension is installed and enabled.</span></span>

  <span data-ttu-id="e5404-664">a.</span><span class="sxs-lookup"><span data-stu-id="e5404-664">a.</span></span>  <span data-ttu-id="e5404-665">`sudo sh -c 'ls -al /var/lib/waagent/Microsoft.OSTCExtensions.LinuxDiagnostic-'` öğesini çalıştırın</span><span class="sxs-lookup"><span data-stu-id="e5404-665">Run `sudo sh -c 'ls -al /var/lib/waagent/Microsoft.OSTCExtensions.LinuxDiagnostic-'`</span></span>

   <span data-ttu-id="e5404-666">**Beklenen sonucu**: hello hello Linux tanılama uzantısını dizinin içeriğini listeler.</span><span class="sxs-lookup"><span data-stu-id="e5404-666">**Expected result**: Lists hello content of hello Linux Diagnostic Extension directory.</span></span>

 <span data-ttu-id="e5404-667">b.</span><span class="sxs-lookup"><span data-stu-id="e5404-667">b.</span></span> <span data-ttu-id="e5404-668">`ps -ax | grep diagnostic` öğesini çalıştırın</span><span class="sxs-lookup"><span data-stu-id="e5404-668">Run `ps -ax | grep diagnostic`</span></span>

   <span data-ttu-id="e5404-669">**Beklenen sonucu**: için benzer bir giriş görüntüler:`python /var/lib/waagent/Microsoft.OSTCExtensions.LinuxDiagnostic-2.0.92/diagnostic.py -daemon`</span><span class="sxs-lookup"><span data-stu-id="e5404-669">**Expected result**: Displays one entry similar to: `python /var/lib/waagent/Microsoft.OSTCExtensions.LinuxDiagnostic-2.0.92/diagnostic.py -daemon`</span></span>

3.   <span data-ttu-id="e5404-670">Bu hello Azure Gelişmiş izleme uzantısı yüklü olduğundan ve çalıştığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="e5404-670">Make sure that hello Azure Enhanced Monitoring Extension is installed and running.</span></span>

  <span data-ttu-id="e5404-671">a.</span><span class="sxs-lookup"><span data-stu-id="e5404-671">a.</span></span>  <span data-ttu-id="e5404-672">`sudo sh -c 'ls -al /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-/'` öğesini çalıştırın</span><span class="sxs-lookup"><span data-stu-id="e5404-672">Run `sudo sh -c 'ls -al /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-/'`</span></span>

    <span data-ttu-id="e5404-673">**Beklenen sonucu**: hello hello Azure Gelişmiş izleme uzantısı dizinin içeriğini listeler.</span><span class="sxs-lookup"><span data-stu-id="e5404-673">**Expected result**: Lists hello content of hello Azure Enhanced Monitoring Extension directory.</span></span>

  <span data-ttu-id="e5404-674">b.</span><span class="sxs-lookup"><span data-stu-id="e5404-674">b.</span></span> <span data-ttu-id="e5404-675">`ps -ax | grep AzureEnhanced` öğesini çalıştırın</span><span class="sxs-lookup"><span data-stu-id="e5404-675">Run `ps -ax | grep AzureEnhanced`</span></span>

     <span data-ttu-id="e5404-676">**Beklenen sonucu**: için benzer bir giriş görüntüler:`python /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-2.0.0.2/handler.py daemon`</span><span class="sxs-lookup"><span data-stu-id="e5404-676">**Expected result**: Displays one entry similar to: `python /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-2.0.0.2/handler.py daemon`</span></span>

3. <span data-ttu-id="e5404-677">SAP konak Aracısı SAP Not açıklandığı gibi yüklemeniz [1031096]ve hello çıktısını kontrol `saposcol`.</span><span class="sxs-lookup"><span data-stu-id="e5404-677">Install SAP Host Agent as described in SAP Note [1031096], and check hello output of `saposcol`.</span></span>

  <span data-ttu-id="e5404-678">a.</span><span class="sxs-lookup"><span data-stu-id="e5404-678">a.</span></span>  <span data-ttu-id="e5404-679">`/usr/sap/hostctrl/exe/saposcol -d` öğesini çalıştırın</span><span class="sxs-lookup"><span data-stu-id="e5404-679">Run `/usr/sap/hostctrl/exe/saposcol -d`</span></span>

  <span data-ttu-id="e5404-680">b.</span><span class="sxs-lookup"><span data-stu-id="e5404-680">b.</span></span>  <span data-ttu-id="e5404-681">`dump ccm` öğesini çalıştırın</span><span class="sxs-lookup"><span data-stu-id="e5404-681">Run `dump ccm`</span></span>

  <span data-ttu-id="e5404-682">c.</span><span class="sxs-lookup"><span data-stu-id="e5404-682">c.</span></span>  <span data-ttu-id="e5404-683">Onay olup hello **Virtualization_Configuration\Enhanced izleme erişim** ölçümüdür **doğru**.</span><span class="sxs-lookup"><span data-stu-id="e5404-683">Check whether hello **Virtualization_Configuration\Enhanced Monitoring Access** metric is **true**.</span></span>

<span data-ttu-id="e5404-684">Yüklü bir SAP NetWeaver ABAP uygulama sunucusu zaten varsa, işlem ST06 açın ve Gelişmiş izleme etkin olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="e5404-684">If you already have an SAP NetWeaver ABAP application server installed, open transaction ST06 and check whether enhanced monitoring is enabled.</span></span>

<span data-ttu-id="e5404-685">Tüm bu denetimlerin başarısız olursa, ve nasıl tooredeploy hello uzantısı hakkında ayrıntılı bilgi için bkz: [sorun giderme için SAP Azure izleme altyapısının hello][deployment-guide-5.3].</span><span class="sxs-lookup"><span data-stu-id="e5404-685">If any of these checks fail, and for detailed information about how tooredeploy hello extension, see [Troubleshooting hello Azure monitoring infrastructure for SAP][deployment-guide-5.3].</span></span>

### <span data-ttu-id="e5404-686"><a name="e2d592ff-b4ea-4a53-a91a-e5521edb6cd1"></a>Sistem durumu izleme Azure altyapısı yapılandırmasını Merhaba kontrol edin</span><span class="sxs-lookup"><span data-stu-id="e5404-686"><a name="e2d592ff-b4ea-4a53-a91a-e5521edb6cd1"></a>Health check for hello Azure monitoring infrastructure configuration</span></span>
<span data-ttu-id="e5404-687">Bazı izleme verilerini hello teslim edilmez varsa doğru belirtildiği gibi hello test açıklanan [Gelişmiş Azure izlemesi için SAP için hazırlık denetimi][deployment-guide-5.1]çalıştırın hello `Test-AzureRmVMAEMExtension` cmdlet toocheck olup hello Azure altyapısı ve izleme uzantısı için SAP hello izleme doğru şekilde yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="e5404-687">If some of hello monitoring data is not delivered correctly as indicated by hello test described in [Readiness check for Azure Enhanced Monitoring for SAP][deployment-guide-5.1], run hello `Test-AzureRmVMAEMExtension` cmdlet toocheck whether hello Azure monitoring infrastructure and hello monitoring extension for SAP are configured correctly.</span></span>

1.  <span data-ttu-id="e5404-688">Bölümünde açıklandığı gibi hello hello Azure PowerShell cmdlet'ini, en son sürümünü yüklediğinizden emin olun [dağıtımı Azure PowerShell cmdlet'lerini][deployment-guide-4.1].</span><span class="sxs-lookup"><span data-stu-id="e5404-688">Make sure that you have installed hello latest version of hello Azure PowerShell cmdlet, as described in [Deploying Azure PowerShell cmdlets][deployment-guide-4.1].</span></span>
2.  <span data-ttu-id="e5404-689">Merhaba aşağıdaki PowerShell cmdlet'ini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e5404-689">Run hello following PowerShell cmdlet.</span></span> <span data-ttu-id="e5404-690">Kullanılabilir ortamlar listesi için hello cmdlet'i çalıştırmak `Get-AzureRmEnvironment`.</span><span class="sxs-lookup"><span data-stu-id="e5404-690">For a list of available environments, run hello cmdlet `Get-AzureRmEnvironment`.</span></span> <span data-ttu-id="e5404-691">toouse ortak Azure, select hello **AzureCloud** ortamı.</span><span class="sxs-lookup"><span data-stu-id="e5404-691">toouse public Azure, select hello **AzureCloud** environment.</span></span> <span data-ttu-id="e5404-692">Çin'de Azure için seçin **AzureChinaCloud**.</span><span class="sxs-lookup"><span data-stu-id="e5404-692">For Azure in China, select **AzureChinaCloud**.</span></span>
  ```powershell
  $env = Get-AzureRmEnvironment -Name <name of hello environment>
  Login-AzureRmAccount -Environment $env
  Set-AzureRmContext -SubscriptionName <subscription name>
  Test-AzureRmVMAEMExtension -ResourceGroupName <resource group name> -VMName <virtual machine name>
  ```

3.  <span data-ttu-id="e5404-693">Hesap verilerinizi girin ve hello Azure sanal makine belirleyin.</span><span class="sxs-lookup"><span data-stu-id="e5404-693">Enter your account data and identify hello Azure virtual machine.</span></span>

  ![SAP özgü giriş sayfasında Azure cmdlet Test VMConfigForSAP_GUI][deployment-guide-figure-1200]

4. <span data-ttu-id="e5404-695">Merhaba betik testleri hello hello sanal makinenin yapılandırmasını, seçin.</span><span class="sxs-lookup"><span data-stu-id="e5404-695">hello script tests hello configuration of hello virtual machine you select.</span></span>

  ![Hello Azure izleme altyapısının başarılı test SAP için çıktısı][deployment-guide-figure-1300]

<span data-ttu-id="e5404-697">Her sistem durumu denetimi sonucu olduğundan emin olun **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="e5404-697">Make sure that every health check result is **OK**.</span></span> <span data-ttu-id="e5404-698">Bazı denetimleri değil görüntülerseniz **Tamam**, açıklandığı gibi hello güncelleştirme cmdlet'i çalıştırmak [yapılandırma hello Azure Gelişmiş izleme uzantısı SAP][deployment-guide-4.5].</span><span class="sxs-lookup"><span data-stu-id="e5404-698">If some checks do not display **OK**, run hello update cmdlet as described in [Configure hello Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span> <span data-ttu-id="e5404-699">15 dakika bekleyin ve tekrar hello denetimleri açıklanan [Gelişmiş Azure izlemesi için SAP için hazırlık denetimi] [ deployment-guide-5.1] ve [Azure izleme altyapı yapılandırmaiçinsistemdurumudenetimi] [deployment-guide-5.2].</span><span class="sxs-lookup"><span data-stu-id="e5404-699">Wait 15 minutes, and repeat hello checks described in [Readiness check for Azure Enhanced Monitoring for SAP][deployment-guide-5.1] and [Health check for Azure Monitoring Infrastructure Configuration][deployment-guide-5.2].</span></span> <span data-ttu-id="e5404-700">Merhaba denetimleri hala bazı veya tüm sayaçları ile ilgili bir sorun gösteriyorsa, bkz: [sorun giderme için SAP Azure izleme altyapısının hello][deployment-guide-5.3].</span><span class="sxs-lookup"><span data-stu-id="e5404-700">If hello checks still indicate a problem with some or all counters, see [Troubleshooting hello Azure monitoring infrastructure for SAP][deployment-guide-5.3].</span></span>

### <span data-ttu-id="e5404-701"><a name="fe25a7da-4e4e-4388-8907-8abc2d33cfd8"></a>Hello Azure izleme altyapısının SAP için sorun giderme</span><span class="sxs-lookup"><span data-stu-id="e5404-701"><a name="fe25a7da-4e4e-4388-8907-8abc2d33cfd8"></a>Troubleshooting hello Azure monitoring infrastructure for SAP</span></span>

#### <a name="windowslogowindows-azure-performance-counters-do-not-show-up-at-all"></a>![Windows][Logo_Windows] <span data-ttu-id="e5404-703">Azure performans sayaçları hiç görünmüyor</span><span class="sxs-lookup"><span data-stu-id="e5404-703">Azure performance counters do not show up at all</span></span>
<span data-ttu-id="e5404-704">Merhaba AzureEnhancedMonitoring Windows hizmeti Azure performans ölçümleri toplar.</span><span class="sxs-lookup"><span data-stu-id="e5404-704">hello AzureEnhancedMonitoring Windows service collects performance metrics in Azure.</span></span> <span data-ttu-id="e5404-705">Merhaba hizmet doğru şekilde yüklenmemiş veya VM ile çalışmıyorsa, performans ölçümleri toplanabilir.</span><span class="sxs-lookup"><span data-stu-id="e5404-705">If hello service has not been installed correctly or if it is not running in your VM, no performance metrics can be collected.</span></span>

##### <a name="hello-installation-directory-of-hello-azure-enhanced-monitoring-extension-is-empty"></a><span data-ttu-id="e5404-706">Merhaba yükleme dizini hello Azure Gelişmiş izleme uzantısı, boştur</span><span class="sxs-lookup"><span data-stu-id="e5404-706">hello installation directory of hello Azure Enhanced Monitoring Extension is empty</span></span>

###### <a name="issue"></a><span data-ttu-id="e5404-707">Sorun</span><span class="sxs-lookup"><span data-stu-id="e5404-707">Issue</span></span>
<span data-ttu-id="e5404-708">Merhaba yükleme dizini C:\\paketleri\\eklentileri\\Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;sürüm >\\açılan boştur.</span><span class="sxs-lookup"><span data-stu-id="e5404-708">hello installation directory C:\\Packages\\Plugins\\Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;version>\\drop is empty.</span></span>

###### <a name="solution"></a><span data-ttu-id="e5404-709">Çözüm</span><span class="sxs-lookup"><span data-stu-id="e5404-709">Solution</span></span>
<span data-ttu-id="e5404-710">Merhaba uzantısı yüklü değil.</span><span class="sxs-lookup"><span data-stu-id="e5404-710">hello extension is not installed.</span></span> <span data-ttu-id="e5404-711">(Daha önce açıklandığı gibi) bu proxy sorunu olup olmadığını belirler.</span><span class="sxs-lookup"><span data-stu-id="e5404-711">Determine whether this is a proxy issue (as described earlier).</span></span> <span data-ttu-id="e5404-712">Toorestart hello makine ya da yeniden çalıştır hello gerekebilecek `Set-AzureRmVMAEMExtension` yapılandırma komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="e5404-712">You might need toorestart hello machine or rerun hello `Set-AzureRmVMAEMExtension` configuration script.</span></span>

##### <a name="service-for-azure-enhanced-monitoring-does-not-exist"></a><span data-ttu-id="e5404-713">Gelişmiş Azure izlemesi için hizmet yok</span><span class="sxs-lookup"><span data-stu-id="e5404-713">Service for Azure Enhanced Monitoring does not exist</span></span>

###### <a name="issue"></a><span data-ttu-id="e5404-714">Sorun</span><span class="sxs-lookup"><span data-stu-id="e5404-714">Issue</span></span>
<span data-ttu-id="e5404-715">Merhaba AzureEnhancedMonitoring Windows hizmeti yok.</span><span class="sxs-lookup"><span data-stu-id="e5404-715">hello AzureEnhancedMonitoring Windows service does not exist.</span></span>

<span data-ttu-id="e5404-716">Azperflib.exe çıktı bir hata oluşturur:</span><span class="sxs-lookup"><span data-stu-id="e5404-716">Azperflib.exe output throws an error:</span></span>

<span data-ttu-id="e5404-717">![Azperflib.exe yürütülmesi hello Azure Gelişmiş izleme uzantısı hello hizmeti SAP için çalışmadığını gösterir][deployment-guide-figure-1400]
<a name="figure-14"></a></span><span class="sxs-lookup"><span data-stu-id="e5404-717">![Execution of azperflib.exe indicates that hello service of hello Azure Enhanced Monitoring Extension for SAP is not running][deployment-guide-figure-1400]
<a name="figure-14"></a></span></span>

###### <a name="solution"></a><span data-ttu-id="e5404-718">Çözüm</span><span class="sxs-lookup"><span data-stu-id="e5404-718">Solution</span></span>
<span data-ttu-id="e5404-719">Merhaba hizmet mevcut değilse hello Azure Gelişmiş izleme uzantısı SAP doğru şekilde yüklenmedi.</span><span class="sxs-lookup"><span data-stu-id="e5404-719">If hello service does not exist, hello Azure Enhanced Monitoring Extension for SAP has not been installed correctly.</span></span> <span data-ttu-id="e5404-720">Dağıtım senaryonuz için açıklanan başlangıç adımları kullanarak Hello uzantısı dağıtmanız [VM'ler Azure SAP için dağıtım senaryoları][deployment-guide-3].</span><span class="sxs-lookup"><span data-stu-id="e5404-720">Redeploy hello extension by using hello steps described for your deployment scenario in [Deployment scenarios of VMs for SAP in Azure][deployment-guide-3].</span></span>

<span data-ttu-id="e5404-721">Bir saat sonra hello uzantısı dağıttıktan sonra yeniden hello Azure performans sayaçları hello Azure VM sağlanan olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="e5404-721">After you deploy hello extension, after one hour, check again whether hello Azure performance counters are provided in hello Azure VM.</span></span>

##### <a name="service-for-azure-enhanced-monitoring-exists-but-fails-toostart"></a><span data-ttu-id="e5404-722">Azure Gelişmiş izleme hizmeti var, ancak toostart başarısız</span><span class="sxs-lookup"><span data-stu-id="e5404-722">Service for Azure Enhanced Monitoring exists, but fails toostart</span></span>

###### <a name="issue"></a><span data-ttu-id="e5404-723">Sorun</span><span class="sxs-lookup"><span data-stu-id="e5404-723">Issue</span></span>
<span data-ttu-id="e5404-724">Merhaba AzureEnhancedMonitoring Windows hizmeti var ve etkinleştirilir, ancak toostart başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="e5404-724">hello AzureEnhancedMonitoring Windows service exists and is enabled, but fails toostart.</span></span> <span data-ttu-id="e5404-725">Daha fazla bilgi için hello uygulama olay günlüğünü denetleyin.</span><span class="sxs-lookup"><span data-stu-id="e5404-725">For more information, check hello application event log.</span></span>

###### <a name="solution"></a><span data-ttu-id="e5404-726">Çözüm</span><span class="sxs-lookup"><span data-stu-id="e5404-726">Solution</span></span>
<span data-ttu-id="e5404-727">Merhaba yapılandırması doğru değil.</span><span class="sxs-lookup"><span data-stu-id="e5404-727">hello configuration is incorrect.</span></span> <span data-ttu-id="e5404-728">Bölümünde açıklandığı gibi hello VM uzantısı izleme hello yeniden [yapılandırma hello Azure Gelişmiş izleme uzantısı SAP][deployment-guide-4.5].</span><span class="sxs-lookup"><span data-stu-id="e5404-728">Restart hello monitoring extension for hello VM, as described in [Configure hello Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span>

#### <a name="windowslogowindows-some-azure-performance-counters-are-missing"></a>![Windows][Logo_Windows] <span data-ttu-id="e5404-730">Bazı Azure performans sayaçları kayboluyor</span><span class="sxs-lookup"><span data-stu-id="e5404-730">Some Azure performance counters are missing</span></span>
<span data-ttu-id="e5404-731">Merhaba AzureEnhancedMonitoring Windows hizmeti Azure performans ölçümleri toplar.</span><span class="sxs-lookup"><span data-stu-id="e5404-731">hello AzureEnhancedMonitoring Windows service collects performance metrics in Azure.</span></span> <span data-ttu-id="e5404-732">Merhaba hizmet çeşitli kaynaklardan veri alır.</span><span class="sxs-lookup"><span data-stu-id="e5404-732">hello service gets data from several sources.</span></span> <span data-ttu-id="e5404-733">Bazı yapılandırma verilerini yerel olarak toplanır ve bazı performans ölçümleri Azure tanılama salt okunurdur.</span><span class="sxs-lookup"><span data-stu-id="e5404-733">Some configuration data is collected locally, and some performance metrics are read from Azure Diagnostics.</span></span> <span data-ttu-id="e5404-734">Depolama sayaçları hello depolama abonelik düzeyinde, oturum açmasını kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e5404-734">Storage counters are used from your logging on hello storage subscription level.</span></span>

<span data-ttu-id="e5404-735">SAP Not kullanarak sorun giderme olursa [1999351] hello sorunu çözümlemek için değil, hello yeniden `Set-AzureRmVMAEMExtension` yapılandırma komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="e5404-735">If troubleshooting by using SAP Note [1999351] doesn't resolve hello issue, rerun hello `Set-AzureRmVMAEMExtension` configuration script.</span></span> <span data-ttu-id="e5404-736">Hemen etkinleştirildikten sonra depolama analytics veya tanılama sayaçları oluşturulamaz, saat toowait olabilir.</span><span class="sxs-lookup"><span data-stu-id="e5404-736">You might have toowait an hour because storage analytics or diagnostics counters might not be created immediately after they are enabled.</span></span> <span data-ttu-id="e5404-737">Merhaba sorun devam ederse hello OP NT AZR BC Windows bileşeni veya BC-OP-LNX-AZR Linux sanal makine için bir SAP Müşteri Destek iletide açın.</span><span class="sxs-lookup"><span data-stu-id="e5404-737">If hello problem persists, open an SAP customer support message on hello component BC-OP-NT-AZR for Windows or BC-OP-LNX-AZR for a Linux virtual machine.</span></span>

#### <a name="linuxlogolinux-azure-performance-counters-do-not-show-up-at-all"></a>![Linux][Logo_Linux] <span data-ttu-id="e5404-739">Azure performans sayaçları hiç görünmüyor</span><span class="sxs-lookup"><span data-stu-id="e5404-739">Azure performance counters do not show up at all</span></span>
<span data-ttu-id="e5404-740">Azure performans ölçümlerini bir arka plan programı tarafından toplanır.</span><span class="sxs-lookup"><span data-stu-id="e5404-740">Performance metrics in Azure are collected by a daemon.</span></span> <span data-ttu-id="e5404-741">Merhaba arka plan programı çalışmıyorsa, performans ölçümleri toplanabilir.</span><span class="sxs-lookup"><span data-stu-id="e5404-741">If hello daemon is not running, no performance metrics can be collected.</span></span>

##### <a name="hello-installation-directory-of-hello-azure-enhanced-monitoring-extension-is-empty"></a><span data-ttu-id="e5404-742">Merhaba yükleme dizini hello Gelişmiş Azure Monitoring uzantısı, boştur</span><span class="sxs-lookup"><span data-stu-id="e5404-742">hello installation directory of hello Azure Enhanced Monitoring extension is empty</span></span>

###### <a name="issue"></a><span data-ttu-id="e5404-743">Sorun</span><span class="sxs-lookup"><span data-stu-id="e5404-743">Issue</span></span>
<span data-ttu-id="e5404-744">Merhaba dizin \\var\\lib\\waagent\\ hello Gelişmiş Azure Monitoring uzantısı için bir alt yok.</span><span class="sxs-lookup"><span data-stu-id="e5404-744">hello directory \\var\\lib\\waagent\\ does not have a subdirectory for hello Azure Enhanced Monitoring extension.</span></span>

###### <a name="solution"></a><span data-ttu-id="e5404-745">Çözüm</span><span class="sxs-lookup"><span data-stu-id="e5404-745">Solution</span></span>
<span data-ttu-id="e5404-746">Merhaba uzantısı yüklü değil.</span><span class="sxs-lookup"><span data-stu-id="e5404-746">hello extension is not installed.</span></span> <span data-ttu-id="e5404-747">(Daha önce açıklandığı gibi) bu proxy sorunu olup olmadığını belirler.</span><span class="sxs-lookup"><span data-stu-id="e5404-747">Determine whether this is a proxy issue (as described earlier).</span></span> <span data-ttu-id="e5404-748">Toorestart hello makine ve/veya yeniden çalıştır hello gerekebilecek `Set-AzureRmVMAEMExtension` yapılandırma komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="e5404-748">You might need toorestart hello machine and/or rerun hello `Set-AzureRmVMAEMExtension` configuration script.</span></span>

#### <a name="linuxlogolinux-some-azure-performance-counters-are-missing"></a>![Linux][Logo_Linux] <span data-ttu-id="e5404-750">Bazı Azure performans sayaçları kayboluyor</span><span class="sxs-lookup"><span data-stu-id="e5404-750">Some Azure performance counters are missing</span></span>
<span data-ttu-id="e5404-751">Azure'da performans ölçümleri, çeşitli kaynaklardan veri aldığı bir arka plan programı tarafından toplanır.</span><span class="sxs-lookup"><span data-stu-id="e5404-751">Performance metrics in Azure are collected by a daemon, which gets data from several sources.</span></span> <span data-ttu-id="e5404-752">Bazı yapılandırma verilerini yerel olarak toplanır ve bazı performans ölçümleri Azure tanılama salt okunurdur.</span><span class="sxs-lookup"><span data-stu-id="e5404-752">Some configuration data is collected locally, and some performance metrics are read from Azure Diagnostics.</span></span> <span data-ttu-id="e5404-753">Depolama sayaçları hello günlükleri depolama aboneliğinizde gelmektedir.</span><span class="sxs-lookup"><span data-stu-id="e5404-753">Storage counters come from hello logs in your storage subscription.</span></span>

<span data-ttu-id="e5404-754">Bilinen sorunların eksiksiz ve güncel listesi için bkz. SAP Not [1999351], Gelişmiş Azure izlemesi için SAP için ek sorun giderme bilgileri içeriyor.</span><span class="sxs-lookup"><span data-stu-id="e5404-754">For a complete and up-to-date list of known issues, see SAP Note [1999351], which has additional troubleshooting information for Enhanced Azure Monitoring for SAP.</span></span>

<span data-ttu-id="e5404-755">SAP Not kullanarak sorun giderme olursa [1999351] yok hello sorunu çözün, hello yeniden `Set-AzureRmVMAEMExtension` açıklandığı gibi yapılandırma komut dosyası [yapılandırma hello Azure Gelişmiş izleme uzantısı SAP][deployment-guide-4.5].</span><span class="sxs-lookup"><span data-stu-id="e5404-755">If troubleshooting by using SAP Note [1999351] does not resolve hello issue, rerun hello `Set-AzureRmVMAEMExtension` configuration script as described in [Configure hello Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span> <span data-ttu-id="e5404-756">Hemen etkinleştirildikten sonra depolama analytics veya tanılama sayaçları oluşturulmuş olabilir değil çünkü bir saate toowait olabilir.</span><span class="sxs-lookup"><span data-stu-id="e5404-756">You might have toowait for an hour because storage analytics or diagnostics counters might not be created immediately after they are enabled.</span></span> <span data-ttu-id="e5404-757">Merhaba sorun devam ederse hello OP NT AZR BC Windows bileşeni veya BC-OP-LNX-AZR Linux sanal makine için bir SAP Müşteri Destek iletide açın.</span><span class="sxs-lookup"><span data-stu-id="e5404-757">If hello problem persists, open an SAP customer support message on hello component BC-OP-NT-AZR for Windows or BC-OP-LNX-AZR for a Linux virtual machine.</span></span>
