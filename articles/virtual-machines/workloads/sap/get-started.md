---
title: "Azure vm'lerinde SAP aaaGetting Başlarken | Microsoft Docs"
description: "Microsoft Azure sanal makineleri (VM'ler) üzerinde çalışan SAP çözümleri hakkında bilgi edinin"
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: ad8e5c75-0cf6-4564-ae62-ea1246b4e5f2
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/29/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0ac390f8e1c802505b8f9304a12868364fa60f80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-for-hosting-and-running-sap-workload-scenarios"></a><span data-ttu-id="7fcbe-103">Barındırma ve SAP iş yükü senaryoları çalıştıran için Azure'ı kullanma</span><span class="sxs-lookup"><span data-stu-id="7fcbe-103">Using Azure for hosting and running SAP workload scenarios</span></span>
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

[azure-cli]:../../../cli-install-nodejs.md
[azure-portal]:https://portal.azure.com
[azure-ps]:/powershell/azureps-cmdlets-docs
[azure-quickstart-templates-github]:https://github.com/Azure/azure-quickstart-templates
[azure-script-ps]:https://go.microsoft.com/fwlink/p/?LinkID=395017
[azure-subscription-service-limits]:../../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md#subscription

[dbms-guide]:dbms-guide.md 
[dbms-guide-2.1]:dbms-guide.md#c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f 
[dbms-guide-2.2]:dbms-guide.md#c8e566f9-21b7-4457-9f7f-126036971a91 
[dbms-guide-2.3]:dbms-guide.md#10b041ef-c177-498a-93ed-44b3441ab152 
[dbms-guide-2]:dbms-guide.md#65fa79d6-a85f-47ee-890b-22e794f51a64 
[dbms-guide-3]:dbms-guide.md#871dfc27-e509-4222-9370-ab1de77021c3 
[dbms-guide-5.5.1]:dbms-guide.md#0fef0e79-d3fe-4ae2-85af-73666a6f7268 
[dbms-guide-5.5.2]:dbms-guide.md#f9071eff-9d72-4f47-9da4-1852d782087b
[dbms-guide-5.6]:dbms-guide.md#1b353e38-21b3-4310-aeb6-a77e7c8e81c8 
[dbms-guide-5.8]:dbms-guide.md#9053f720-6f3b-4483-904d-15dc54141e30 
[dbms-guide-5]:dbms-guide.md#3264829e-075e-4d25-966e-a49dad878737 
[dbms-guide-8.4.1]:dbms-guide.md#b48cfe3b-48e9-4f5b-a783-1d29155bd573 
[dbms-guide-8.4.2]:dbms-guide.md#23c78d3b-ca5a-4e72-8a24-645d141a3f5d 
[dbms-guide-8.4.3]:dbms-guide.md#77cd2fbb-307e-4cbf-a65f-745553f72d2c 
[dbms-guide-8.4.4]:dbms-guide.md#f77c1436-9ad8-44fb-a331-8671342de818 
[dbms-guide-900-sap-cache-server-on-premises]:dbms-guide.md#642f746c-e4d4-489d-bf63-73e80177a0a8

[dbms-guide-figure-100]:media/virtual-machines-shared-sap-dbms-guide/100_storage_account_types.png
[dbms-guide-figure-200]:media/virtual-machines-shared-sap-dbms-guide/200-ha-set-for-dbms-ha.png
[dbms-guide-figure-300]:media/virtual-machines-shared-sap-dbms-guide/300-reference-config-iaas.png
[dbms-guide-figure-400]:media/virtual-machines-shared-sap-dbms-guide/400-sql-2012-backup-to-blob-storage.png
[dbms-guide-figure-500]:media/virtual-machines-shared-sap-dbms-guide/500-sql-2012-backup-to-blob-storage-different-containers.png
[dbms-guide-figure-600]:media/virtual-machines-shared-sap-dbms-guide/600-iaas-maxdb.png
[dbms-guide-figure-700]:media/virtual-machines-shared-sap-dbms-guide/700-livecach-prod.png
[dbms-guide-figure-800]:media/virtual-machines-shared-sap-dbms-guide/800-azure-vm-sap-content-server.png
[dbms-guide-figure-900]:media/virtual-machines-shared-sap-dbms-guide/900-sap-cache-server-on-premises.png

[deployment-guide]:deployment-guide.md 
[deployment-guide-2.2]:deployment-guide.md#42ee2bdb-1efc-4ec7-ab31-fe4c22769b94 
[deployment-guide-3.1.2]:deployment-guide.md#3688666f-281f-425b-a312-a77e7db2dfab 
[deployment-guide-3.2]:deployment-guide.md#db477013-9060-4602-9ad4-b0316f8bb281 
[deployment-guide-3.3]:deployment-guide.md#54a1fc6d-24fd-4feb-9c57-ac588a55dff2 
[deployment-guide-3.4]:deployment-guide.md#a9a60133-a763-4de8-8986-ac0fa33aa8c1
[deployment-guide-3]:deployment-guide.md#b3253ee3-d63b-4d74-a49b-185e76c4088e 
[deployment-guide-4.1]:deployment-guide.md#604bcec2-8b6e-48d2-a944-61b0f5dee2f7 
[deployment-guide-4.2]:deployment-guide.md#7ccf6c3e-97ae-4a7a-9c75-e82c37beb18e 
[deployment-guide-4.3]:deployment-guide.md#31d9ecd6-b136-4c73-b61e-da4a29bbc9cc 
[deployment-guide-4.4.2]:deployment-guide.md#6889ff12-eaaf-4f3c-97e1-7c9edc7f7542 
[deployment-guide-4.4]:deployment-guide.md#c7cbb0dc-52a4-49db-8e03-83e7edc2927d 
[deployment-guide-4.5.1]:deployment-guide.md#987cf279-d713-4b4c-8143-6b11589bb9d4 
[deployment-guide-4.5.2]:deployment-guide.md#408f3779-f422-4413-82f8-c57a23b4fc2f 
[deployment-guide-4.5]:deployment-guide.md#d98edcd3-f2a1-49f7-b26a-07448ceb60ca 
[deployment-guide-5.1]:deployment-guide.md#bb61ce92-8c5c-461f-8c53-39f5e5ed91f2
[deployment-guide-5.2]:deployment-guide.md#e2d592ff-b4ea-4a53-a91a-e5521edb6cd1 
[deployment-guide-5.3]:deployment-guide.md#fe25a7da-4e4e-4388-8907-8abc2d33cfd8 
[deployment-guide-configure-monitoring-scenario-1]:deployment-guide.md#ec323ac3-1de9-4c3a-b770-4ff701def65b 
[deployment-guide-configure-proxy]:deployment-guide.md#baccae00-6f79-4307-ade4-40292ce4e02d 
[deployment-guide-figure-100]:media/virtual-machines-shared-sap-deployment-guide/100-deploy-vm-image.png
[deployment-guide-figure-1000]:media/virtual-machines-shared-sap-deployment-guide/1000-service-properties.png
[deployment-guide-figure-11]:deployment-guide.md#figure-11
[deployment-guide-figure-1100]:media/virtual-machines-shared-sap-deployment-guide/1100-azperflib.png
[deployment-guide-figure-1200]:media/virtual-machines-shared-sap-deployment-guide/1200-cmd-test-login.png
[deployment-guide-figure-1300]:media/virtual-machines-shared-sap-deployment-guide/1300-cmd-test-executed.png
[deployment-guide-figure-14]:deployment-guide.md#figure-14
[deployment-guide-figure-1400]:media/virtual-machines-shared-sap-deployment-guide/1400-azperflib-error-servicenotstarted.png
[deployment-guide-figure-300]:media/virtual-machines-shared-sap-deployment-guide/300-deploy-private-image.png
[deployment-guide-figure-400]:media/virtual-machines-shared-sap-deployment-guide/400-deploy-using-disk.png
[deployment-guide-figure-5]:deployment-guide.md#figure-5
[deployment-guide-figure-50]:media/virtual-machines-shared-sap-deployment-guide/50-forced-tunneling-suse.png
[deployment-guide-figure-500]:media/virtual-machines-shared-sap-deployment-guide/500-install-powershell.png
[deployment-guide-figure-6]:deployment-guide.md#figure-6
[deployment-guide-figure-600]:media/virtual-machines-shared-sap-deployment-guide/600-powershell-version.png
[deployment-guide-figure-7]:deployment-guide.md#figure-7
[deployment-guide-figure-700]:media/virtual-machines-shared-sap-deployment-guide/700-install-powershell-installed.png
[deployment-guide-figure-760]:media/virtual-machines-shared-sap-deployment-guide/760-azure-cli-version.png
[deployment-guide-figure-900]:media/virtual-machines-shared-sap-deployment-guide/900-cmd-update-executed.png
[deployment-guide-figure-azure-cli-installed]:deployment-guide.md#402488e5-f9bb-4b29-8063-1c5f52a892d0
[deployment-guide-figure-azure-cli-version]:deployment-guide.md#0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda
[deployment-guide-install-vm-agent-windows]:deployment-guide.md#b2db5c9a-a076-42c6-9835-16945868e866
[deployment-guide-troubleshooting-chapter]:deployment-guide.md#564adb4f-5c95-4041-9616-6635e83a810b 
[deploy-template-cli]:../../../resource-group-template-deploy.md
[deploy-template-portal]:../../../resource-group-template-deploy.md
[deploy-template-powershell]:../../../resource-group-template-deploy.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:get-started.md
[getting-started-dbms]:get-started.md#1343ffe1-8021-4ce6-a08d-3a1553a4db82
[getting-started-deployment]:get-started.md#6aadadd2-76b5-46d8-8713-e8d63630e955
[getting-started-planning]:get-started.md#3da0389e-708b-4e82-b2a2-e92f132df89c


[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056
[ha-guide]:sap-high-availability-guide.md

[install-extension-cli]:virtual-machines-linux-enable-aem.md

[Logo_Linux]:media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:media/virtual-machines-shared-sap-shared/Windows.png

[msdn-set-azurermvmaemextension]:https://msdn.microsoft.com/library/azure/mt670598.aspx

[planning-guide]:planning-guide.md 
[planning-guide-1.2]:planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff 
[planning-guide-11.4.1]:planning-guide.md#5d9d36f9-9058-435d-8367-5ad05f00de77 
[planning-guide-11.5]:planning-guide.md#4e165b58-74ca-474f-a7f4-5e695a93204f 
[planning-guide-2.1]:planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803 
[planning-guide-2.2]:planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10 
[planning-guide-3.1]:planning-guide.md#be80d1b9-a463-4845-bd35-f4cebdb5424a 
[planning-guide-3.2.1]:planning-guide.md#df49dc09-141b-4f34-a4a2-990913b30358 
[planning-guide-3.2.2]:planning-guide.md#fc1ac8b2-e54a-487c-8581-d3cc6625e560 
[planning-guide-3.2.3]:planning-guide.md#18810088-f9be-4c97-958a-27996255c665 
[planning-guide-3.2]:planning-guide.md#8d8ad4b8-6093-4b91-ac36-ea56d80dbf77 
[planning-guide-3.3.2]:planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92 
[planning-guide-5.1.1]:planning-guide.md#4d175f1b-7353-4137-9d2f-817683c26e53 
[planning-guide-5.1.2]:planning-guide.md#e18f7839-c0e2-4385-b1e6-4538453a285c 
[planning-guide-5.2.1]:planning-guide.md#1b287330-944b-495d-9ea7-94b83aff73ef 
[planning-guide-5.2.2]:planning-guide.md#57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3 
[planning-guide-5.2]:planning-guide.md#6ffb9f41-a292-40bf-9e70-8204448559e7 
[planning-guide-5.3.1]:planning-guide.md#6e835de8-40b1-4b71-9f18-d45b20959b79 
[planning-guide-5.3.2]:planning-guide.md#a43e40e6-1acc-4633-9816-8f095d5a7b6a 
[planning-guide-5.4.2]:planning-guide.md#9789b076-2011-4afa-b2fe-b07a8aba58a1 
[planning-guide-5.5.1]:planning-guide.md#4efec401-91e0-40c0-8e64-f2dceadff646 
[planning-guide-5.5.3]:planning-guide.md#17e0d543-7e8c-4160-a7da-dd7117a1ad9d 
[planning-guide-7.1]:planning-guide.md#3e9c3690-da67-421a-bc3f-12c520d99a30 
[planning-guide-7]:planning-guide.md#96a77628-a05e-475d-9df3-fb82217e8f14 
[planning-guide-9.1]:planning-guide.md#6f0a47f3-a289-4090-a053-2521618a28c3 
[planning-guide-azure-premium-storage]:planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92 

[planning-guide-figure-100]:media/virtual-machines-shared-sap-planning-guide/100-single-vm-in-azure.png
[planning-guide-figure-1300]:media/virtual-machines-shared-sap-planning-guide/1300-ref-config-iaas-for-sap.png
[planning-guide-figure-1400]:media/virtual-machines-shared-sap-planning-guide/1400-attach-detach-disks.png
[planning-guide-figure-1600]:media/virtual-machines-shared-sap-planning-guide/1600-firewall-port-rule.png
[planning-guide-figure-1700]:media/virtual-machines-shared-sap-planning-guide/1700-single-vm-demo.png
[planning-guide-figure-1900]:media/virtual-machines-shared-sap-planning-guide/1900-vm-set-vnet.png
[planning-guide-figure-200]:media/virtual-machines-shared-sap-planning-guide/200-multiple-vms-in-azure.png
[planning-guide-figure-2100]:media/virtual-machines-shared-sap-planning-guide/2100-s2s.png
[planning-guide-figure-2200]:media/virtual-machines-shared-sap-planning-guide/2200-network-printing.png
[planning-guide-figure-2300]:media/virtual-machines-shared-sap-planning-guide/2300-sapgui-stms.png
[planning-guide-figure-2400]:media/virtual-machines-shared-sap-planning-guide/2400-vm-extension-overview.png
[planning-guide-figure-2500]:media/virtual-machines-shared-sap-planning-guide/2500-vm-extension-details.png
[planning-guide-figure-2600]:media/virtual-machines-shared-sap-planning-guide/2600-sap-router-connection.png
[planning-guide-figure-2700]:media/virtual-machines-shared-sap-planning-guide/2700-exposed-sap-portal.png
[planning-guide-figure-2800]:media/virtual-machines-shared-sap-planning-guide/2800-endpoint-config.png
[planning-guide-figure-2900]:media/virtual-machines-shared-sap-planning-guide/2900-azure-ha-sap-ha.png
[planning-guide-figure-300]:media/virtual-machines-shared-sap-planning-guide/300-vpn-s2s.png
[planning-guide-figure-3000]:media/virtual-machines-shared-sap-planning-guide/3000-sap-ha-on-azure.png
[planning-guide-figure-3200]:media/virtual-machines-shared-sap-planning-guide/3200-sap-ha-with-sql.png
[planning-guide-figure-400]:media/virtual-machines-shared-sap-planning-guide/400-vm-services.png
[planning-guide-figure-600]:media/virtual-machines-shared-sap-planning-guide/600-s2s-details.png
[planning-guide-figure-700]:media/virtual-machines-shared-sap-planning-guide/700-decision-tree-deploy-to-azure.png
[planning-guide-figure-800]:media/virtual-machines-shared-sap-planning-guide/800-portal-vm-overview.png
[planning-guide-microsoft-azure-networking]:planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f 

[powershell-install-configure]:https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[resource-group-authoring-templates]:../../../resource-group-authoring-templates.md
[resource-group-overview]:../../../azure-resource-manager/resource-group-overview.md
[resource-groups-networking]:../../../virtual-network/resource-groups-networking.md
[sap-pam]:https://support.sap.com/pam (SAP Product Availability Matrix)
[sap-templates-2-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-2-tier-os-disk]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-disk%2Fazuredeploy.json
[sap-templates-2-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-image%2Fazuredeploy.json
[sap-templates-3-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-3-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-user-image%2Fazuredeploy.json
[storage-azure-cli]:../../../storage/common/storage-azure-cli.md
[storage-azure-cli-copy-blobs]:../../../storage/common/storage-azure-cli.md#copy-blobs
[storage-introduction]:../../../storage/common/storage-introduction.md
[storage-powershell-guide-full-copy-vhd]:../../../storage/common/storage-powershell-guide-full.md#how-to-copy-blobs-from-one-storage-container-to-another
[storage-premium-storage-preview-portal]:../../../storage/common/storage-premium-storage.md
[storage-redundancy]:../../../storage/common/storage-redundancy.md
[storage-scalability-targets]:../../../storage/common/storage-scalability-targets.md
[storage-use-azcopy]:../../../storage/common/storage-use-azcopy.md
[template-201-vm-from-specialized-vhd]:https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd
[templates-101-simple-windows-vm]:https://github.com/Azure/azure-quickstart-templates/tree/master/101-simple-windows-vm
[templates-101-vm-from-user-image]:https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image
[virtual-machines-linux-attach-disk-portal]:../../linux/attach-disk-portal.md
[virtual-machines-azure-resource-manager-architecture]:../../../resource-manager-deployment-model.md
[virtual-machines-azurerm-versus-azuresm]:virtual-machines-linux-compare-deployment-models.md
[virtual-machines-windows-classic-configure-oracle-data-guard]:../../virtual-machines-windows-classic-configure-oracle-data-guard.md
[virtual-machines-linux-cli-deploy-templates]:../../linux/cli-deploy-templates.md 
[virtual-machines-deploy-rmtemplates-powershell]:../../virtual-machines-windows-ps-manage.md 
[virtual-machines-linux-agent-user-guide]:../../linux/agent-user-guide.md
[virtual-machines-linux-agent-user-guide-command-line-options]:../../linux/agent-user-guide.md#command-line-options
[virtual-machines-linux-capture-image]:../../linux/capture-image.md
[virtual-machines-linux-capture-image-resource-manager]:../../linux/capture-image.md
[virtual-machines-linux-capture-image-resource-manager-capture]:../../linux/capture-image.md#capture-the-vm
[virtual-machines-linux-configure-raid]:../../linux/configure-raid.md
[virtual-machines-linux-configure-lvm]:../../linux/configure-lvm.md
[virtual-machines-linux-classic-create-upload-vhd-step-1]:../../virtual-machines-linux-classic-create-upload-vhd.md#step-1-prepare-the-image-to-be-uploaded
[virtual-machines-linux-create-upload-vhd-suse]:../../linux/suse-create-upload-vhd.md
[virtual-machines-linux-redhat-create-upload-vhd]:../../linux/redhat-create-upload-vhd.md
[virtual-machines-linux-how-to-attach-disk]:../../linux/add-disk.md
[virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]:../../linux/add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk
[virtual-machines-linux-tutorial]:../../linux/quick-create-cli.md
[virtual-machines-linux-update-agent]:../../linux/update-agent.md
[virtual-machines-manage-availability]:../../linux/manage-availability.md
[virtual-machines-ps-create-preconfigure-windows-resource-manager-vms]:virtual-machines-windows-create-powershell.md
[virtual-machines-sizes]:../../linux/sizes.md
[virtual-machines-windows-classic-ps-sql-alwayson-availability-groups]:./../../windows/sqlclassic/virtual-machines-windows-classic-ps-sql-alwayson-availability-groups.md
[virtual-machines-windows-classic-ps-sql-int-listener]:./../../windows/sqlclassic/virtual-machines-windows-classic-ps-sql-int-listener.md
[virtual-machines-sql-server-high-availability-and-disaster-recovery-solutions]:./../../windows/sql/virtual-machines-windows-sql-high-availability-dr.md
[virtual-machines-sql-server-infrastructure-services]:./../../windows/sql/virtual-machines-windows-sql-server-iaas-overview.md
[virtual-machines-sql-server-performance-best-practices]:./../../windows/sql/virtual-machines-windows-sql-performance.md
[virtual-machines-upload-image-windows-resource-manager]:../../virtual-machines-windows-upload-image.md
[virtual-machines-windows-tutorial]:../../virtual-machines-windows-hero-tutorial.md
[virtual-machines-workload-template-sql-alwayson]:https://azure.microsoft.com/documentation/templates/sql-server-2014-alwayson-dsc/
[virtual-network-deploy-multinic-arm-cli]:../../../virtual-network/virtual-network-deploy-multinic-arm-cli.md
[virtual-network-deploy-multinic-arm-ps]:../../../virtual-network/virtual-network-deploy-multinic-arm-ps.md
[virtual-network-deploy-multinic-arm-template]:../../../virtual-network/virtual-network-deploy-multinic-arm-template.md
[virtual-networks-configure-vnet-to-vnet-connection]:../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md
[virtual-networks-create-vnet-arm-pportal]:../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md
[virtual-networks-manage-dns-in-vnet]:../../../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md
[virtual-networks-multiple-nics]:../../../virtual-network/virtual-networks-multiple-nics.md
[virtual-networks-nsg]:../../../virtual-network/virtual-networks-nsg.md
[virtual-networks-reserved-private-ip]:../../../virtual-network/virtual-networks-static-private-ip-arm-ps.md
[virtual-networks-static-private-ip-arm-pportal]:../../../virtual-network/virtual-networks-static-private-ip-arm-pportal.md
[virtual-networks-udr-overview]:../../../virtual-network/virtual-networks-udr-overview.md
[vpn-gateway-about-vpn-devices]:../../../vpn-gateway/vpn-gateway-about-vpn-devices.md
[vpn-gateway-create-site-to-site-rm-powershell]:../../../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md
[vpn-gateway-cross-premises-options]:../../../vpn-gateway/vpn-gateway-plan-design.md
[vpn-gateway-site-to-site-create]:../../../vpn-gateway/vpn-gateway-site-to-site-create.md
[vpn-gateway-vpn-faq]:../../../vpn-gateway/vpn-gateway-vpn-faq.md
[xplat-cli]:../../../cli-install-nodejs.md
[xplat-cli-azure-resource-manager]:../../../xplat-cli-azure-resource-manager.md

<span data-ttu-id="7fcbe-104">Microsoft Azure, SAP hazır bulut iş ortağı olarak seçerek, senaryoları ve görev kritik SAP iş yükleri ölçeklenebilir, uyumlu ve işletme kanıtlanmış platformda çalışması mümkün tooreliably demektir.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-104">By choosing Microsoft Azure as your SAP ready cloud partner, you are able tooreliably run your mission critical SAP workloads and scenarios on a scalable, compliant, and enterprise-proven platform.</span></span>  <span data-ttu-id="7fcbe-105">Merhaba ölçeklenebilirlik, esneklik, alma ve Azure'nın tasarruf maliyeti.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-105">Get hello scalability, flexibility, and cost savings of Azure.</span></span> <span data-ttu-id="7fcbe-106">Microsoft ve SAP arasındaki genişletilmiş hello ortaklığı ile Azure - geliştirme ve test ve üretim senaryolarında arasında SAP uygulamaları çalıştırabilir ve tam olarak desteklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-106">With hello expanded partnership between Microsoft and SAP, you can run SAP applications across dev/test and production scenarios in Azure - and be fully supported.</span></span> <span data-ttu-id="7fcbe-107">SAP NetWeaver tooSAP S4/HANA, SAP BI, Linux tooWindows, SAP HANA tooSQL biz, kapsamdaki vardır.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-107">From SAP NetWeaver tooSAP S4/HANA, SAP BI, Linux tooWindows, SAP HANA tooSQL, we have you covered.</span></span> 

<span data-ttu-id="7fcbe-108">SAP NetWeaver senaryolarla barındırma yanı sıra Azure ile ilgili farklı DBMS Merhaba, farklı barındırabilir Azure SAP BI gibi diğer SAP iş yükü senaryoları.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-108">Besides hosting SAP NetWeaver scenarios with hello different DBMS on Azure, you can host different other SAP workload scenarios, like SAP BI on Azure.</span></span> <span data-ttu-id="7fcbe-109">SAP NetWeaver dağıtımları Azure yerel sanal makinelerde ilgili belgeleri "SAP NetWeaver Azure sanal makinelerde." Merhaba bölümünde bulunabilir</span><span class="sxs-lookup"><span data-stu-id="7fcbe-109">Documentation regarding SAP NetWeaver deployments on Azure native Virtual Machines can be found in hello section "SAP NetWeaver on Azure Virtual Machines."</span></span> 

<span data-ttu-id="7fcbe-110">Azure SAP HANA yararlanır CPU ve bellek kaynakları toocover SAP yükü boyutu sürekli büyüyen yerel Azure sanal makine teklifleri sahiptir.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-110">Azure has native Azure Virtual Machine offers that are ever growing in size of CPU and memory resources toocover SAP workload that leverages SAP HANA.</span></span> <span data-ttu-id="7fcbe-111">Bu konu hakkında daha fazla bilgi için SAP HANA Azure sanal makineler üzerinde hello bölümünde hello belgeleri arayın."</span><span class="sxs-lookup"><span data-stu-id="7fcbe-111">For more information on this topic, look up hello documents under hello section SAP HANA on Azure Virtual Machines."</span></span>

<span data-ttu-id="7fcbe-112">SAP HANA Azure Hello benzersizliğini Azure dışında rekabet ayarlar benzersiz bir teklifidir.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-112">hello uniqueness of Azure for SAP HANA is a unique offer that sets Azure apart from competition.</span></span> <span data-ttu-id="7fcbe-113">Daha fazla bellek ve CPU kaynak barındırma sipariş tooenable içinde senaryoları, SAP HANA içeren Azure müşteri hello kullanımını sunar zorlu SAP too20 TB (60 TB genişleme) gerektiren SAP HANA dağıtımlarını yürüten hello amacı için tam donanım ayrılmış S/4HANA ya da diğer SAP HANA iş yükü için bellek.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-113">In order tooenable hosting more memory and CPU resource demanding SAP scenarios involving SAP HANA, Azure offers hello usage of customer dedicated bare-metal hardware for hello purpose of running SAP HANA deployments that require up too20 TB (60 TB scale-out) of memory for S/4HANA or other SAP HANA workload.</span></span> <span data-ttu-id="7fcbe-114">SAP HANA Azure (büyük örnekler) ile ilgili bu benzersiz Azure çözüm toorun SAP HANA hello SAP uygulama katmanı veya yerel Azure sanal makinelerinde barındırılan iş yükü donanımlar Orta katmanı ile ayrılmış hello çıplak donanımda sağlar.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-114">This unique Azure solution of SAP HANA on Azure (Large Instances) allows you toorun SAP HANA on hello dedicated bare-metal hardware with hello SAP application layer or workload middle-ware layer hosted in native Azure Virtual Machines.</span></span> <span data-ttu-id="7fcbe-115">Bu çözüm çeşitli belgelerde "SAP HANA azure'da (büyük örnekler)." Merhaba bölümünde belgelenen</span><span class="sxs-lookup"><span data-stu-id="7fcbe-115">This solution is documented in several documents in hello section "SAP HANA on Azure (Large Instances)."</span></span>   

<span data-ttu-id="7fcbe-116">SAP iş yükü Azure senaryolarda barındırma kimlik tümleştirme ve çoklu oturum açma Azure etkinlik Directory toodifferent SAP bileşenleri ve SAP SaaS kullanma gereksinimleri de oluşturabilir veya PaaS sunar.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-116">Hosting SAP workload scenarios in Azure also can create requirements of Identity integration and Single-Sign-On using Azure Activity Directory toodifferent SAP components and SAP SaaS or PaaS offers.</span></span> <span data-ttu-id="7fcbe-117">Bu tümleştirme ve çoklu oturum açma senaryoları Azure Active Directory (AAD) ve SAP varlıklarla listesini açıklanmıştır ve hello bölümünde belgelenen "AAD SAP kimlik tümleştirme ve çoklu oturum açma."</span><span class="sxs-lookup"><span data-stu-id="7fcbe-117">A list of such integration and Single-Sign-On scenarios with Azure Active Directory (AAD) and SAP entities is described and documented in hello section "AAD SAP Identity Integration and Single-Sign-On."</span></span>


## <a name="sap-hana-on-sap-hana-on-azure-large-instances"></a><span data-ttu-id="7fcbe-118">SAP HANA üzerinde SAP HANA azure'da (büyük örnekleri)</span><span class="sxs-lookup"><span data-stu-id="7fcbe-118">SAP HANA on SAP HANA on Azure (Large Instances)</span></span>

### <a name="overview-and-architecture-of-sap-hana-on-azure-large-instances"></a><span data-ttu-id="7fcbe-119">Genel bakış ve SAP HANA azure'da (büyük örnekler) mimarisi</span><span class="sxs-lookup"><span data-stu-id="7fcbe-119">Overview and architecture of SAP HANA on Azure (Large Instances)</span></span>
<span data-ttu-id="7fcbe-120">Başlık: aaaOverview ve Azure (büyük örnekler) üzerinde SAP HANA mimarisi</span><span class="sxs-lookup"><span data-stu-id="7fcbe-120">title: aaaOverview and Architecture of SAP HANA on Azure (Large Instances)</span></span>

<span data-ttu-id="7fcbe-121">Özet: Bu mimari ve teknik dağıtım kılavuzu üzerinde SAP dağıttığınız bilgileri toohelp sağlar (büyük örnekler) azure'da yeni SAP HANA Azure'da hello.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-121">Summary: This Architecture and Technical Deployment Guide provides information toohelp you deploy SAP on hello new SAP HANA on Azure (Large Instances) in Azure.</span></span> <span data-ttu-id="7fcbe-122">Hedeflenen toobe kapsamlı Kılavuzu bir kapsayıcı özel kurulum SAP çözümleri, ancak ilk ve devam eden işlemler yerine yararlı bilgiler değil.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-122">It is not intended toobe a comprehensive guide covering specific setup of SAP solutions, but rather useful information in your initial deployment and ongoing operations.</span></span> <span data-ttu-id="7fcbe-123">SAP belgelerine değiştirmeniz gerekir değil ilgili SAP HANA toohello yüklemesi (veya hello konuda birçok SAP destek Not hello).</span><span class="sxs-lookup"><span data-stu-id="7fcbe-123">It should not replace SAP documentation related toohello installation of SAP HANA (or hello many SAP Support Notes that cover hello topic).</span></span> <span data-ttu-id="7fcbe-124">Genel bir bakış sağlar ve SAP HANA (büyük örnekler) Azure üzerinde yükleme hello ek ayrıntılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-124">It gives you an overview and provides hello additional detail of installing SAP HANA on Azure (Large Instances).</span></span>

<span data-ttu-id="7fcbe-125">Güncelleştirilmiş: Temmuz 2017</span><span class="sxs-lookup"><span data-stu-id="7fcbe-125">Updated: July 2017</span></span>

[<span data-ttu-id="7fcbe-126">Bu kılavuz burada bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-126">This guide can be found here</span></span>](hana-overview-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="infrastructure-and-connectivity-toosap-hana-on-azure-large-instances"></a><span data-ttu-id="7fcbe-127">Altyapı ve bağlantı tooSAP HANA azure'da (büyük örnekleri)</span><span class="sxs-lookup"><span data-stu-id="7fcbe-127">Infrastructure and connectivity tooSAP HANA on Azure (Large Instances)</span></span>
<span data-ttu-id="7fcbe-128">Başlık: aaaInfrastructure ve bağlantı tooSAP HANA azure'da (büyük örnekleri)</span><span class="sxs-lookup"><span data-stu-id="7fcbe-128">title: aaaInfrastructure and Connectivity tooSAP HANA on Azure (Large Instances)</span></span>

<span data-ttu-id="7fcbe-129">Özet: SAP HANA (büyük örnekler) azure'da hello satın, arasında hello Microsoft Kurumsal hesap ekibi sonlandırıldıktan sonra çeşitli ağ yapılandırmaları sipariş tooensure uygun bağlantısı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-129">Summary: After hello purchase of SAP HANA on Azure (Large Instances) is finalized between you and hello Microsoft enterprise account team, various network configurations are required in order tooensure proper connectivity.</span></span>  <span data-ttu-id="7fcbe-130">Aşağıdaki bilgilerle hello ile paylaşılan toobe sahip bu belge anahatları hello bilgiler gereklidir.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-130">This document outlines hello information that has toobe shared with hello following information is required.</span></span> <span data-ttu-id="7fcbe-131">Bu belge, hangi bilgilerin toobe toplanan ve hangi yapılandırma komut dosyaları çalıştırmak toobe sahip olduğunuz özetlenmektedir.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-131">This document outlines what information has toobe collected and what configuration scripts have toobe run.</span></span> 

<span data-ttu-id="7fcbe-132">Güncelleştirilmiş: Temmuz 2017</span><span class="sxs-lookup"><span data-stu-id="7fcbe-132">Updated: July 2017</span></span>

[<span data-ttu-id="7fcbe-133">Bu kılavuz burada bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-133">This guide can be found here</span></span>](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="install-sap-hana-in-sap-hana-on-azure-large-instances"></a><span data-ttu-id="7fcbe-134">SAP HANA SAP HANA azure'da (büyük örnekler) yükleyin</span><span class="sxs-lookup"><span data-stu-id="7fcbe-134">Install SAP HANA in SAP HANA on Azure (Large Instances)</span></span>
<span data-ttu-id="7fcbe-135">Başlık: aaaInstall SAP HANA üzerinde SAP HANA azure'da (büyük örnekleri)</span><span class="sxs-lookup"><span data-stu-id="7fcbe-135">title: aaaInstall SAP HANA on SAP HANA on Azure (Large Instances)</span></span>

<span data-ttu-id="7fcbe-136">Özet: Bu belgede, Azure büyük örneğinde SAP HANA yüklemek için hello kurulum yordamları özetlemektedir.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-136">Summary: This document outlines hello setup procedures for installing SAP HANA on your Azure Large Instance.</span></span> 

<span data-ttu-id="7fcbe-137">Güncelleştirilmiş: Temmuz 2017</span><span class="sxs-lookup"><span data-stu-id="7fcbe-137">Updated: July 2017</span></span>

[<span data-ttu-id="7fcbe-138">Bu kılavuz burada bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-138">This guide can be found here</span></span>](hana-installation.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="high-availability-and-disaster-recovery-of-sap-hana-on-azure-large-instances"></a><span data-ttu-id="7fcbe-139">SAP HANA (büyük örnekler) azure'da yüksek kullanılabilirlik ve olağanüstü durum kurtarma</span><span class="sxs-lookup"><span data-stu-id="7fcbe-139">High availability and disaster recovery of SAP HANA on Azure (Large Instances)</span></span>
<span data-ttu-id="7fcbe-140">Başlık: aaaHigh kullanılabilirlik ve olağanüstü durum kurtarma, SAP HANA azure'da (büyük örnekleri)</span><span class="sxs-lookup"><span data-stu-id="7fcbe-140">title: aaaHigh Availability and Disaster Recovery of SAP HANA on Azure (Large Instances)</span></span>

<span data-ttu-id="7fcbe-141">Özet: Yüksek kullanılabilirlik (HA) ve olağanüstü durum kurtarma (DR) kritik SAP HANA Azure (büyük örnekler) sunucuları üzerinde çalışan çok önemli yönlerinden markalarıdır.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-141">Summary: High Availability (HA) and Disaster Recovery (DR) are very important aspects of running your mission-critical SAP HANA on Azure (Large Instances) server(s).</span></span> <span data-ttu-id="7fcbe-142">İçeri aktarma toowork SAP ile, sistem Tümleştirici ve/veya Microsoft tooproperly mimari ve sizin için hello sağ HA/DR stratejisi uygulayın.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-142">It's import toowork with SAP, your system integrator, and/or Microsoft tooproperly architect and implement hello right HA/DR strategy for you.</span></span> <span data-ttu-id="7fcbe-143">Kurtarma noktası hedefi (RPO) ve kurtarma süresi hedefi (RTO), belirli tooyour ortamı gibi önemli noktalar dikkate alınmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-143">Important considerations like Recovery Point Objective (RPO) and Recovery Time Objective (RTO), specific tooyour environment, must be considered.</span></span>  <span data-ttu-id="7fcbe-144">Bu belge, tercih edilen düzeyde HA ve DR etkinleştirme seçeneklerinizi açıklar.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-144">This document explains your options for enabling your preferred level of HA and DR.</span></span>

<span data-ttu-id="7fcbe-145">Güncelleştirilmiş: Aralık 2016</span><span class="sxs-lookup"><span data-stu-id="7fcbe-145">Updated: December 2016</span></span>

[<span data-ttu-id="7fcbe-146">Bu belge burada bulunabilir</span><span class="sxs-lookup"><span data-stu-id="7fcbe-146">This document can be found here</span></span>](hana-overview-high-availability-disaster-recovery.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="troubleshooting-and-monitoring-of-sap-hana-on-azure-large-instances"></a><span data-ttu-id="7fcbe-147">SAP HANA Azure (büyük örnekler) ile ilgili izleme ve sorun giderme</span><span class="sxs-lookup"><span data-stu-id="7fcbe-147">Troubleshooting and monitoring of SAP HANA on Azure (Large Instances)</span></span>
<span data-ttu-id="7fcbe-148">Başlık: aaaTroubleshooting ve izleme, SAP HANA azure'da (büyük örnekleri)</span><span class="sxs-lookup"><span data-stu-id="7fcbe-148">title: aaaTroubleshooting and Monitoring of SAP HANA on Azure (Large Instances)</span></span>

<span data-ttu-id="7fcbe-149">Özet: Bu kılavuz, Azure ortamına, SAP HANA izlenmesini oluşturulmasında yararlı yanı sıra ek sorun giderme bilgileri bilgileri kapsar.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-149">Summary: This guide covers information that is useful in establishing monitoring of your SAP HANA on Azure environment as well as additional troubleshooting information.</span></span> 

<span data-ttu-id="7fcbe-150">Güncelleştirilmiş: Aralık 2016</span><span class="sxs-lookup"><span data-stu-id="7fcbe-150">Updated: December 2016</span></span>

[<span data-ttu-id="7fcbe-151">Bu belge burada bulunabilir</span><span class="sxs-lookup"><span data-stu-id="7fcbe-151">This document can be found here</span></span>](troubleshooting-monitoring.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="sap-hana-on-azure-virtual-machines"></a><span data-ttu-id="7fcbe-152">Azure Sanal Makinelerde SAP HANA</span><span class="sxs-lookup"><span data-stu-id="7fcbe-152">SAP HANA on Azure Virtual Machines</span></span>

### <a name="getting-started-with-sap-hana-on-azure"></a><span data-ttu-id="7fcbe-153">SAP HANA Azure üzerinde ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="7fcbe-153">Getting started with SAP HANA on Azure</span></span>
<span data-ttu-id="7fcbe-154">Başlık: Azure vm'lerinde SAP HANA el ile yüklenmesi için aaaQuickstart Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="7fcbe-154">title: aaaQuickstart guide for manual installation of SAP HANA on Azure VMs</span></span>

<span data-ttu-id="7fcbe-155">Özet: Bu Hızlı Başlangıç Kılavuzu, bir tek örnekli SAP HANA sistemi Azure vm'lerinde el ile yükleme tarafından SAP NetWeaver 7.5 ve SAP HANA SP12 tooset yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-155">Summary: This quickstart guide helps tooset up a single-instance SAP HANA system on Azure VMs by a manual installation of SAP NetWeaver 7.5 and SAP HANA SP12.</span></span> <span data-ttu-id="7fcbe-156">Merhaba Kılavuzu hello okuyucu toodeploy sanal makineleri veya sanal ağları da hello Azure portal veya Powershell/CLI dahil olmak üzere üzerinden seçeneği toouse json şablonları nasıl hello gibi Azure Iaas temel kavramları hakkında bilgi sahibi olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-156">hello guide presumes that hello reader is familiar with Azure IaaS basics like how toodeploy virtual machines or virtual networks either via hello Azure portal or Powershell/CLI including hello option toouse json templates.</span></span> <span data-ttu-id="7fcbe-157">Ayrıca hello okuyucu SAP HANA, SAP NetWeaver ve nasıl tooinstall, şirket içi alışkın olduğu beklenir.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-157">Furthermore it's expected that hello reader is familiar with SAP HANA, SAP NetWeaver and how tooinstall it on-premises.</span></span>

<span data-ttu-id="7fcbe-158">Güncelleştirilmiş: Haziran 2017</span><span class="sxs-lookup"><span data-stu-id="7fcbe-158">Updated: June 2017</span></span>

[<span data-ttu-id="7fcbe-159">Bu kılavuz burada bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-159">This guide can be found here</span></span>](hana-get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="s4hana-sap-cal-deployment-on-azure"></a><span data-ttu-id="7fcbe-160">Azure üzerinde S/4HANA SAP CAL dağıtımı</span><span class="sxs-lookup"><span data-stu-id="7fcbe-160">S/4HANA SAP CAL deployment on Azure</span></span>
<span data-ttu-id="7fcbe-161">Başlık: aaaDeploy SAP S/4HANA veya BW/4HANA Azure ile ilgili</span><span class="sxs-lookup"><span data-stu-id="7fcbe-161">title: aaaDeploy SAP S/4HANA or BW/4HANA on Azure</span></span>

<span data-ttu-id="7fcbe-162">Özet: Bu kılavuzda SAP S/4HANA SAP bulut Gereci kitaplığını kullanarak azure'da hello dağıtımını toodemonstrate yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-162">Summary: This guide helps toodemonstrate hello deployment of SAP S/4HANA on Azure using SAP Cloud Appliance Library.</span></span> <span data-ttu-id="7fcbe-163">SAP bulut Gereci kitaplığı, Azure üzerinde toodeploy SAP uygulamaları veren SAP tarafından bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-163">SAP Cloud Appliance Library is a service by SAP that allows toodeploy SAP applications on Azure.</span></span> <span data-ttu-id="7fcbe-164">Merhaba Kılavuzu adım adım hello dağıtım açıklar.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-164">hello guide describes step by step hello deployment.</span></span>

<span data-ttu-id="7fcbe-165">Güncelleştirilmiş: Haziran 2017</span><span class="sxs-lookup"><span data-stu-id="7fcbe-165">Updated: June 2017</span></span>

[<span data-ttu-id="7fcbe-166">Bu kılavuz burada bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-166">This guide can be found here</span></span>](cal-s4h.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="high-availability-of-sap-hana-in-azure-virtual-machines"></a><span data-ttu-id="7fcbe-167">SAP HANA Azure sanal makinelerde yüksek kullanılabilirliği</span><span class="sxs-lookup"><span data-stu-id="7fcbe-167">High Availability of SAP HANA in Azure Virtual Machines</span></span>
<span data-ttu-id="7fcbe-168">Başlık: aaaHigh SAP HANA, kullanılabilirlik Azure sanal makineler üzerinde</span><span class="sxs-lookup"><span data-stu-id="7fcbe-168">title: aaaHigh Availability of SAP HANA on Azure Virtual Machines</span></span>

<span data-ttu-id="7fcbe-169">Özet: Bu kılavuzu hello SUSE 12 OS hello yüksek kullanılabilirlik yapılandırması size ve SAP HANA tooaccommodate HANA sistem çoğaltma otomatik yük devretme ile yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-169">Summary: This guide leads you through hello high availability configuration of hello SUSE 12 OS and SAP HANA tooaccommodate HANA System replication with automatic failover.</span></span> <span data-ttu-id="7fcbe-170">Merhaba Kılavuzu SUSE ve Azure sanal makineleri için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-170">hello guide is specific for SUSE and Azure Virtual Machines.</span></span> <span data-ttu-id="7fcbe-171">Merhaba Kılavuzu henüz Red Hat veya tam veya özel Bulut veya diğer Azure dışı ortak bulut dağıtımları geçerli değildir.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-171">hello guide does not apply yet for Red Hat or bare-metal or private cloud or other non-Azure public cloud deployments.</span></span>

<span data-ttu-id="7fcbe-172">Güncelleştirilmiş: Haziran 2017</span><span class="sxs-lookup"><span data-stu-id="7fcbe-172">Updated: June 2017</span></span>

[<span data-ttu-id="7fcbe-173">Bu kılavuz burada bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-173">This guide can be found here</span></span>](sap-hana-high-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="sap-hana-backup-overview-on-azure-vms"></a><span data-ttu-id="7fcbe-174">SAP HANA Azure vm'lerinde yedeklemeye genel bakış</span><span class="sxs-lookup"><span data-stu-id="7fcbe-174">SAP HANA backup overview on Azure VMs</span></span>
<span data-ttu-id="7fcbe-175">Başlık: Azure sanal makineler üzerinde aaaBackup Kılavuzu SAP HANA için</span><span class="sxs-lookup"><span data-stu-id="7fcbe-175">title: aaaBackup guide for SAP HANA on Azure Virtual Machines</span></span>

<span data-ttu-id="7fcbe-176">Özet: Bu kılavuzda SAP HANA Azure sanal makinelerde çalışan yedekleme olasılıkları hakkında temel bilgiler sağlar.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-176">Summary: This guide provides basic information about backup possibilities running SAP HANA on Azure Virtual Machines.</span></span>

<span data-ttu-id="7fcbe-177">Güncelleştirilmiş: Mart 2017</span><span class="sxs-lookup"><span data-stu-id="7fcbe-177">Updated: March 2017</span></span>

[<span data-ttu-id="7fcbe-178">Bu kılavuz burada bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-178">This guide can be found here</span></span>](sap-hana-backup-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="sap-hana-file-level-backup-on-azure-vms"></a><span data-ttu-id="7fcbe-179">Azure vm'lerinde SAP HANA dosya düzeyinde yedekleme</span><span class="sxs-lookup"><span data-stu-id="7fcbe-179">SAP HANA file level backup on Azure VMs</span></span>
<span data-ttu-id="7fcbe-180">Başlık: aaaSAP HANA yedekleme depolama anlık görüntü tabanlı</span><span class="sxs-lookup"><span data-stu-id="7fcbe-180">title: aaaSAP HANA backup based on storage snapshots</span></span>

<span data-ttu-id="7fcbe-181">Özet: Bu kılavuzda SAP HANA Azure sanal makinelerde çalışan Azure Vm'lerde anlık görüntü tabanlı yedeklemeleri kullanma hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-181">Summary: This guide provides information about using snapshot-based backups on Azure VMs when running SAP HANA on Azure Virtual Machines.</span></span>

<span data-ttu-id="7fcbe-182">Güncelleştirilmiş: Mart 2017</span><span class="sxs-lookup"><span data-stu-id="7fcbe-182">Updated: March 2017</span></span>

[<span data-ttu-id="7fcbe-183">Bu kılavuz burada bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-183">This guide can be found here</span></span>](sap-hana-backup-file-level.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


### <a name="sap-hana-snapshot-based-backups-on-azure-vms"></a><span data-ttu-id="7fcbe-184">SAP HANA tabanlı anlık görüntüsü yedekleri Azure vm'lerinde</span><span class="sxs-lookup"><span data-stu-id="7fcbe-184">SAP HANA snapshot based backups on Azure VMs</span></span>
<span data-ttu-id="7fcbe-185">Başlık: aaaSAP dosya düzeyinde HANA Azure yedekleme</span><span class="sxs-lookup"><span data-stu-id="7fcbe-185">title: aaaSAP HANA Azure Backup on file level</span></span>

<span data-ttu-id="7fcbe-186">Özet: Bu kılavuzda SAP HANA dosya düzeyinde yedekleme SAP HANA Azure sanal makinelerde çalışan kullanma hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-186">Summary: This guide provides information about using SAP HANA file level backup running SAP HANA on Azure Virtual Machines</span></span>

<span data-ttu-id="7fcbe-187">Güncelleştirilmiş: Mart 2017</span><span class="sxs-lookup"><span data-stu-id="7fcbe-187">Updated: March 2017</span></span>

[<span data-ttu-id="7fcbe-188">Bu kılavuz burada bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-188">This guide can be found here</span></span>](sap-hana-backup-storage-snapshots.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


## <a name="sap-netweaver-deployed-on-azure-virtual-machines"></a><span data-ttu-id="7fcbe-189">Azure sanal makinelerinde dağıtılan SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="7fcbe-189">SAP NetWeaver deployed on Azure Virtual Machines</span></span>

### <a name="deploy-sap-ides-system-on-windows-and-sql-server-through-sap-cal-on-azure"></a><span data-ttu-id="7fcbe-190">Windows ve SQL Server aracılığıyla Azure üzerinde SAP CAL SAP IDE sistemi dağıtma</span><span class="sxs-lookup"><span data-stu-id="7fcbe-190">Deploy SAP IDES system on Windows and SQL Server through SAP CAL on Azure</span></span>
<span data-ttu-id="7fcbe-191">Başlık: aaaTesting SAP NetWeaver Microsoft Azure SUSE Linux sanal makineleri üzerinde</span><span class="sxs-lookup"><span data-stu-id="7fcbe-191">title: aaaTesting SAP NetWeaver on Microsoft Azure SUSE Linux VMs</span></span> 

<span data-ttu-id="7fcbe-192">Özet: Bu belgede Windows ve SAP bulut Gereci kitaplığını kullanarak Azure SQL Server'da göre bir SAP IDE sisteminin hello dağıtımı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-192">Summary: This document describes hello deployment of an SAP IDES system based on Windows and SQL Server on Azure using SAP Cloud Appliance Library.</span></span> <span data-ttu-id="7fcbe-193">SAP bulut uygulaması kitaplığı Azure'da hello dağıtım SAP ürünlerin izin veren bir SAP hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-193">SAP Cloud appliance Library is an SAP service that allows hello deployment of SAP products on Azure.</span></span> <span data-ttu-id="7fcbe-194">Bu belge, adım adım bir SAP IDE sistemi hello dağıtımıyla gider.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-194">This document goes step by step through hello deployment of an SAP IDES system.</span></span> <span data-ttu-id="7fcbe-195">Merhaba IDE sistem yalnızca Microsoft Azure üzerinde SAP bulut uygulaması üzerinden dağıtılabilir birkaç diğer düzine uygulamalar için örneğidir.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-195">hello IDES system is just an example for several other dozen applications that can be deployed through SAP Cloud appliance on Microsoft Azure.</span></span>

<span data-ttu-id="7fcbe-196">Güncelleştirilmiş: Haziran 2017</span><span class="sxs-lookup"><span data-stu-id="7fcbe-196">Updated: June 2017</span></span>

[<span data-ttu-id="7fcbe-197">Bu kılavuz burada bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-197">This guide can be found here</span></span>](cal-ides-erp6-erp7-sp3-sql.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


### <a name="quickstart-guide-for-netweaver-on-suse-linux-on-azure"></a><span data-ttu-id="7fcbe-198">SUSE Linux Azure üzerinde NetWeaver için Hızlı Başlangıç Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="7fcbe-198">Quickstart guide for NetWeaver on SUSE Linux on Azure</span></span>
<span data-ttu-id="7fcbe-199">Başlık: aaaTesting SAP NetWeaver Microsoft Azure SUSE Linux sanal makineleri üzerinde</span><span class="sxs-lookup"><span data-stu-id="7fcbe-199">title: aaaTesting SAP NetWeaver on Microsoft Azure SUSE Linux VMs</span></span> 

<span data-ttu-id="7fcbe-200">Özet: Microsoft Azure SUSE Linux sanal makineleri (VM'ler) SAP NetWeaver çalıştırırken çeşitli şeyler tooconsider bu makalede açıklanır.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-200">Summary: This article describes various things tooconsider when you're running SAP NetWeaver on Microsoft Azure SUSE Linux virtual machines (VMs).</span></span> <span data-ttu-id="7fcbe-201">SAP NetWeaver resmi olarak SUSE Linux sanal makineleri Azure üzerinde desteklenir.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-201">SAP NetWeaver is officially supported on SUSE Linux VMs on Azure.</span></span> <span data-ttu-id="7fcbe-202">Linux sürümleri, SAP çekirdek sürümler ve diğer ayrıntıları ilgili tüm ayrıntıları SAP Not 1928533 bulunabilir "Azure SAP uygulamaları: desteklenen ürünleriyle ve Azure VM türler".</span><span class="sxs-lookup"><span data-stu-id="7fcbe-202">All details regarding Linux versions, SAP kernel versions, and other details can be found in SAP Note 1928533 "SAP Applications on Azure: Supported Products and Azure VM types".</span></span>

<span data-ttu-id="7fcbe-203">Güncelleştirilmiş: Eylül 2016</span><span class="sxs-lookup"><span data-stu-id="7fcbe-203">Updated: September 2016</span></span>

[<span data-ttu-id="7fcbe-204">Bu kılavuz burada bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-204">This guide can be found here</span></span>](suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <span data-ttu-id="7fcbe-205"><a name="3da0389e-708b-4e82-b2a2-e92f132df89c"></a>Planlama ve uygulama</span><span class="sxs-lookup"><span data-stu-id="7fcbe-205"><a name="3da0389e-708b-4e82-b2a2-e92f132df89c"></a>Planning and implementation</span></span>
<span data-ttu-id="7fcbe-206">Başlık: aaaAzure sanal makineleri planlama ve uygulama SAP NetWeaver için</span><span class="sxs-lookup"><span data-stu-id="7fcbe-206">title: aaaAzure Virtual Machines planning and implementation for SAP NetWeaver</span></span>

<span data-ttu-id="7fcbe-207">Özet: SAP NetWeaver Azure sanal makinelerde çalışan hakkında düşünüyor bu belgeyi ile Merhaba Kılavuzu toostart ise.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-207">Summary: This document is hello guide toostart with if you are thinking about running SAP NetWeaver in Azure Virtual Machines.</span></span> <span data-ttu-id="7fcbe-208">Bu planlama ve Uygulama Kılavuzu, bir var olan veya planlanan SAP NetWeaver tabanlı sistem dağıtılan tooan Azure sanal makineleri ortamı oluşturulabilir olup olmadığını değerlendirmek yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-208">This planning and implementation guide helps you evaluate whether an existing or planned SAP NetWeaver-based system can be deployed tooan Azure Virtual Machines environment.</span></span> <span data-ttu-id="7fcbe-209">Birden çok SAP NetWeaver dağıtım senaryoları kapsar ve belirli tooAzure SAP yapılandırmaları içerir.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-209">It covers multiple SAP NetWeaver deployment scenarios, and includes SAP configurations that are specific tooAzure.</span></span> <span data-ttu-id="7fcbe-210">Merhaba kağıt listeler ve ihtiyacınız vardır tüm hello gerekli yapılandırma hakkında bilgi hello SAP/Azure yan toorun karma SAP yatay açıklar.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-210">hello paper lists and describes all hello necessary configuration information you’ll need on hello SAP/Azure side toorun a hybrid SAP landscape.</span></span> <span data-ttu-id="7fcbe-211">SAP NetWeaver tabanlı sistemler yüksek kullanılabilirliğini tooensure Iaas'da sürebilir ölçüleri de kapsar.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-211">Measures you can take tooensure high availability of SAP NetWeaver-based systems on IaaS are also covered.</span></span>

<span data-ttu-id="7fcbe-212">Güncelleştirilmiş: Haziran 2017</span><span class="sxs-lookup"><span data-stu-id="7fcbe-212">Updated: June 2017</span></span>

<span data-ttu-id="7fcbe-213">[Bu kılavuz burada bulunabilir.][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="7fcbe-213">[This guide can be found here][planning-guide]</span></span>

### <a name="high-availability-configurations-of-sap-netweaver-in-azure-vms"></a><span data-ttu-id="7fcbe-214">SAP NetWeaver Azure VM'de yüksek kullanılabilirlik yapılandırmaları</span><span class="sxs-lookup"><span data-stu-id="7fcbe-214">High Availability configurations of SAP NetWeaver in Azure VMs</span></span>
<span data-ttu-id="7fcbe-215">Başlık: aaaAzure SAP NetWeaver yüksek oranda kullanılabilir sanal makineler</span><span class="sxs-lookup"><span data-stu-id="7fcbe-215">title: aaaAzure Virtual Machines high availability for SAP NetWeaver</span></span>

<span data-ttu-id="7fcbe-216">Özet: Bu belgede, biz toodeploy yüksek kullanılabilirlik SAP sistemleri Azure'da hello Azure Resource Manager dağıtım modelini kullanarak uygulayabileceğiniz olduğunu hello adımlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-216">Summary: In this document, we cover hello steps that you can take toodeploy high-availability SAP systems in Azure by using hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="7fcbe-217">Biz bu ana görevlerinde ilerlemenizde.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-217">We walk you through these major tasks.</span></span> <span data-ttu-id="7fcbe-218">Merhaba belgede size nasıl tek---bir hata noktası bileşenleri gibi gelişmiş iş uygulama programlama (ABAP) SAP merkezi Hizmetleri (ASCS) tanımlayan / SAP merkezi Hizmetleri (SCS) ve veritabanı yönetim sistemi (DBMS) ve yedek bileşenlerin SAP gibi Uygulama sunucusu Azure Vm'lerde çalıştırılırken korumalı toobe adımıdır.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-218">In hello document, we describe how single-point-of-failure components like Advanced Business Application Programming (ABAP) SAP Central Services (ASCS)/SAP Central Services (SCS) and database management systems (DBMS), and redundant components like SAP Application Server are going toobe protected when running in Azure VMs.</span></span> <span data-ttu-id="7fcbe-219">Adım adım örnek bir yükleme ve bir Windows Server Yük Devretme Kümelemesi küme azure'da yüksek kullanılabilirlik SAP sisteminde yapılandırmasının gösterilen ve bu belgede gösterilen.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-219">A step-by-step example of an installation and configuration of a high-availability SAP system in a Windows Server Failover Clustering cluster in Azure is demonstrated and shown in this document.</span></span>

<span data-ttu-id="7fcbe-220">Güncelleştirilmiş: Haziran 2017</span><span class="sxs-lookup"><span data-stu-id="7fcbe-220">Updated: June 2017</span></span>

[<span data-ttu-id="7fcbe-221">Bu kılavuz burada bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-221">This guide can be found here</span></span>](high-availability-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="realizing-multi-sid-deployments-of-sap-netweaver-in-azure-vms"></a><span data-ttu-id="7fcbe-222">SAP NetWeaver Azure VM'de çoklu SID dağıtımları kullanıldıklarını</span><span class="sxs-lookup"><span data-stu-id="7fcbe-222">Realizing Multi-SID deployments of SAP NetWeaver in Azure VMs</span></span>
<span data-ttu-id="7fcbe-223">Başlık: aaaCreate bir SAP NetWeaver çoklu SID yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7fcbe-223">title: aaaCreate an SAP NetWeaver multi-SID configuration</span></span> 

<span data-ttu-id="7fcbe-224">Özet: Bu belge bir toplama toohello SAP NetWeaver Azure vm'lerinde için yüksek kullanılabilirlik belgesidir.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-224">Summary: This document is an addition toohello document High availability for SAP NetWeaver on Azure VMs.</span></span> <span data-ttu-id="7fcbe-225">Eylül 2016'da sunulan Azure toonew işlev, Azure VM'ler çifti içinde birden çok SAP NetWeaver ASCS/SCS örnekler olası toodeploy demektir.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-225">Due toonew functionality in Azure that got introduced in September 2016, it is possible toodeploy multiple SAP NetWeaver ASCS/SCS instances in a pair of Azure VMs.</span></span> <span data-ttu-id="7fcbe-226">Bu tür bir yapılandırma ile sanal makineleri gerekli toodeploy toorealize yüksek oranda kullanılabilir SAP NetWeaver yapılandırmaları hello sayısını azaltabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-226">With such a configuration, you can reduce hello number of VMs necessary toodeploy toorealize highly available SAP NetWeaver configurations.</span></span> <span data-ttu-id="7fcbe-227">Merhaba kılavuzda hello Kurulum böyle çoklu SID yapılandırmaları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-227">hello guide describes hello setup of such multi-SID configurations.</span></span>

<span data-ttu-id="7fcbe-228">Güncelleştirilmiş: Aralık 2016</span><span class="sxs-lookup"><span data-stu-id="7fcbe-228">Updated: December 2016</span></span>

[<span data-ttu-id="7fcbe-229">Bu kılavuz burada bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-229">This guide can be found here</span></span>](high-availability-multi-sid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <span data-ttu-id="7fcbe-230"><a name="6aadadd2-76b5-46d8-8713-e8d63630e955"></a>Azure VM'ler, SAP NetWeaver dağıtımı</span><span class="sxs-lookup"><span data-stu-id="7fcbe-230"><a name="6aadadd2-76b5-46d8-8713-e8d63630e955"></a>Deployment of SAP NetWeaver in Azure VMs</span></span>
<span data-ttu-id="7fcbe-231">Başlık: aaaAzure SAP NetWeaver için sanal makineler dağıtımı</span><span class="sxs-lookup"><span data-stu-id="7fcbe-231">title: aaaAzure Virtual Machines deployment for SAP NetWeaver</span></span>

<span data-ttu-id="7fcbe-232">Özet: Bu belgede azure'da SAP NetWeaver yazılım toovirtual makineler dağıtma konusunda yordamsal bir Rehber sağlanır.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-232">Summary: This document provides procedural guidance for deploying SAP NetWeaver software toovirtual machines in Azure.</span></span> <span data-ttu-id="7fcbe-233">Bu yazı üç özel dağıtım senaryoları hakkında sorun giderme önerileri hello SAP için Azure izleme uzantıları için de dahil olmak üzere SAP için hello Azure izleme uzantıları etkinleştirme bir Vurgu ile odaklanır.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-233">This paper focuses on three specific deployment scenarios, with an emphasis on enabling hello Azure Monitoring Extensions for SAP, including troubleshooting recommendations for hello Azure Monitoring Extensions for SAP.</span></span> <span data-ttu-id="7fcbe-234">Bu yazı hello planlama ve Uygulama Kılavuzu okuduğunuz varsayılır.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-234">This paper assumes that you’ve read hello planning and implementation guide.</span></span>

<span data-ttu-id="7fcbe-235">Güncelleştirilmiş: Haziran 2017</span><span class="sxs-lookup"><span data-stu-id="7fcbe-235">Updated: June 2017</span></span>

<span data-ttu-id="7fcbe-236">[Bu kılavuz burada bulunabilir.][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="7fcbe-236">[This guide can be found here][deployment-guide]</span></span>

### <span data-ttu-id="7fcbe-237"><a name="1343ffe1-8021-4ce6-a08d-3a1553a4db82"></a>DBMS Dağıtım Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="7fcbe-237"><a name="1343ffe1-8021-4ce6-a08d-3a1553a4db82"></a>DBMS deployment guide</span></span>
<span data-ttu-id="7fcbe-238">Başlık: aaaAzure SAP NetWeaver için sanal makineleri DBMS dağıtımı</span><span class="sxs-lookup"><span data-stu-id="7fcbe-238">title: aaaAzure Virtual Machines DBMS deployment for SAP NetWeaver</span></span>

<span data-ttu-id="7fcbe-239">Özet: Bu yazıda SAP ile birlikte çalışması gerektiğini hello DBMS sistemleri için planlama ve uygulama konuları kapsar.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-239">Summary: This paper covers planning and implementation considerations for hello DBMS systems that should run in conjunction with SAP.</span></span> <span data-ttu-id="7fcbe-240">Merhaba ilk bölümünde genel konular listelenen ve sunulan.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-240">In hello first part, general considerations are listed and presented.</span></span> <span data-ttu-id="7fcbe-241">Merhaba hello kağıt aşağıdaki bölümlerini SAP tarafından desteklenen farklı DBMS Azure toodeployments ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-241">hello following parts of hello paper relate toodeployments of different DBMS in Azure that are supported by SAP.</span></span> <span data-ttu-id="7fcbe-242">Sunulan farklı DBMS SQL Server, SAP ana ve Oracle ' dir.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-242">Different DBMS presented are SQL Server, SAP ASE, and Oracle.</span></span> <span data-ttu-id="7fcbe-243">Bu belirli bölümlerinde, SAP sistemleri Azure üzerinde bu DBMS birlikte çalışmadığı zaman tooaccount sahip konuları ele alınmıştır.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-243">In those specific parts, considerations you have tooaccount for when you are running SAP systems on Azure in conjunction with those DBMS are discussed.</span></span> <span data-ttu-id="7fcbe-244">Konular Azure ile ilgili farklı DBMS SAP uygulamalarla hello kullanım için sunulan hello tarafından desteklenen yedekleme ve yüksek oranda kullanılabilir yöntemleri ister.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-244">Subjects like backup and high availability methods that are supported by hello different DBMS on Azure are presented for hello usage with SAP applications.</span></span>

<span data-ttu-id="7fcbe-245">Güncelleştirilmiş: Haziran 2017</span><span class="sxs-lookup"><span data-stu-id="7fcbe-245">Updated: June 2017</span></span>

<span data-ttu-id="7fcbe-246">[Bu kılavuz burada bulunabilir.][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="7fcbe-246">[This guide can be found here][dbms-guide]</span></span>

### <a name="using-azure-site-recovery-for-sap-workload"></a><span data-ttu-id="7fcbe-247">Azure Site RECOVERY'yi kullanarak SAP iş yükü için</span><span class="sxs-lookup"><span data-stu-id="7fcbe-247">Using Azure Site Recovery for SAP workload</span></span>
<span data-ttu-id="7fcbe-248">Başlık: aaaSAP NetWeaver: Azure Site Recovery ile olağanüstü durum kurtarma çözümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="7fcbe-248">title: aaaSAP NetWeaver: Building a Disaster Recovery Solution with Azure Site Recovery</span></span> 

<span data-ttu-id="7fcbe-249">Özet: Bu belgede Azure Site kurtarma Hizmetleri olağanüstü durum kurtarma senaryolarına işleme hello amacı için nasıl kullanılabileceğini hello biçimini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-249">Summary: This document describes hello way how Azure Site Recovery services can be used for hello purpose of handling disaster recovery scenarios.</span></span> <span data-ttu-id="7fcbe-250">Azure Site kurtarma Hizmetleri kullanarak bir şirket içi SAP yatay için Azure olağanüstü durum kurtarma konumu olarak kullanıldığı durumlarda.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-250">Cases where Azure is used as disaster recovery location for an on-premise SAP landscape using Azure Site Recovery Services.</span></span> <span data-ttu-id="7fcbe-251">Merhaba belgede açıklanan başka bir hello işlemleri Azure (A2A) olağanüstü durum kurtarma durumu ve Azure Site Recovery ile nasıl yönetilir senaryodur.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-251">Another scenario described in hello document is hello Aure-to-Azure (A2A) disaster recovery case and how it is managed with Azure Site Recovery.</span></span>  

<span data-ttu-id="7fcbe-252">Güncelleştirilmiş: Ağustos 2017</span><span class="sxs-lookup"><span data-stu-id="7fcbe-252">Updated: August 2017</span></span>

[<span data-ttu-id="7fcbe-253">Bu kılavuz burada bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="7fcbe-253">This guide can be found here</span></span>](http://aka.ms/asr-sap)

