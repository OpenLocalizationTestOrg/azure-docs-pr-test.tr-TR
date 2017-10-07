---
title: "Sanal makineler aaaAzure planlama ve uygulama için SAP NetWeaver | Microsoft Docs"
description: "Azure sanal makineleri planlama ve uygulama SAP NetWeaver için"
services: virtual-machines-linux,virtual-machines-windows
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: d7c59cc1-b2d0-4d90-9126-628f9c7a5538
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 11/08/2016
ms.author: sedusch
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0d1e9fa13d847e4d8abb3c34fd352d1f4ece3717
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machines-planning-and-implementation-for-sap-netweaver"></a>Azure sanal makineleri planlama ve uygulama SAP NetWeaver için
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
[2069760]:https://launchpad.support.sap.com/#/notes/2069760
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
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md#subscription-limits

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

[deploy-template-cli]:../../../resource-group-template-deploy-cli.md
[deploy-template-portal]:../../../resource-group-template-deploy-portal.md
[deploy-template-powershell]:../../../resource-group-template-deploy.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:get-started.md
[getting-started-dbms]:get-started.md#1343ffe1-8021-4ce6-a08d-3a1553a4db82
[getting-started-deployment]:get-started.md#6aadadd2-76b5-46d8-8713-e8d63630e955
[getting-started-planning]:get-started.md#3da0389e-708b-4e82-b2a2-e92f132df89c

[getting-started-windows-classic]:../../virtual-machines-windows-classic-sap-get-started.md
[getting-started-windows-classic-dbms]:../../virtual-machines-windows-classic-sap-get-started.md#c5b77a14-f6b4-44e9-acab-4d28ff72a930
[getting-started-windows-classic-deployment]:../../virtual-machines-windows-classic-sap-get-started.md#f84ea6ce-bbb4-41f7-9965-34d31b0098ea
[getting-started-windows-classic-dr]:../../virtual-machines-windows-classic-sap-get-started.md#cff10b4a-01a5-4dc3-94b6-afb8e55757d3
[getting-started-windows-classic-ha-sios]:../../virtual-machines-windows-classic-sap-get-started.md#4bb7512c-0fa0-4227-9853-4004281b1037
[getting-started-windows-classic-planning]:../../virtual-machines-windows-classic-sap-get-started.md#f2a5e9d8-49e4-419e-9900-af783173481c

[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056

[install-extension-cli]:virtual-machines-linux-enable-aem.md

[Logo_Linux]:media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:media/virtual-machines-shared-sap-shared/Windows.png

[msdn-set-azurermvmaemextension]:https://msdn.microsoft.com/library/azure/mt670598.aspx

[planning-guide]:planning-guide.md  
[planning-guide-1.2]:planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff
[planning-guide-11]:planning-guide.md#7cf991a1-badd-40a9-944e-7baae842a058
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
[planning-guide-figure-2500]:media/virtual-machines-shared-sap-planning-guide/planning-monitoring-overview-2502.png
[planning-guide-figure-2600]:media/virtual-machines-shared-sap-planning-guide/2600-sap-router-connection.png
[planning-guide-figure-2700]:media/virtual-machines-shared-sap-planning-guide/2700-exposed-sap-portal.png
[planning-guide-figure-2800]:media/virtual-machines-shared-sap-planning-guide/2800-endpoint-config.png
[planning-guide-figure-2900]:media/virtual-machines-shared-sap-planning-guide/2900-azure-ha-sap-ha.png
[planning-guide-figure-2901]:media/virtual-machines-shared-sap-planning-guide/2901-azure-ha-sap-ha-md.png
[planning-guide-figure-300]:media/virtual-machines-shared-sap-planning-guide/300-vpn-s2s.png
[planning-guide-figure-3000]:media/virtual-machines-shared-sap-planning-guide/3000-sap-ha-on-azure.png
[planning-guide-figure-3200]:media/virtual-machines-shared-sap-planning-guide/3200-sap-ha-with-sql.png
[planning-guide-figure-3201]:media/virtual-machines-shared-sap-planning-guide/3201-sap-ha-with-sql-md.png
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
[sap-pam]:https://support.sap.com/pam
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
[virtual-machines-linux-capture-image-resource-manager-capture]:../../linux/capture-image.md#step-2-capture-the-vm
[virtual-machines-windows-capture-image-resource-manager]:../../windows/capture-image.md
[virtual-machines-windows-capture-image]:../../virtual-machines-windows-generalize-vhd.md
[virtual-machines-windows-capture-image-prepare-the-vm-for-image-capture]:../../virtual-machines-windows-generalize-vhd.md
[virtual-machines-linux-configure-raid]:../../linux/configure-raid.md
[virtual-machines-linux-configure-lvm]:../../linux/configure-lvm.md
[virtual-machines-linux-classic-create-upload-vhd-step-1]:../../virtual-machines-linux-classic-create-upload-vhd.md#step-1-prepare-the-image-to-be-uploaded
[virtual-machines-linux-create-upload-vhd-suse]:../../linux/suse-create-upload-vhd.md
[virtual-machines-linux-create-upload-vhd-oracle]:../../linux/oracle-create-upload-vhd.md
[virtual-machines-linux-redhat-create-upload-vhd]:../../linux/redhat-create-upload-vhd.md
[virtual-machines-linux-how-to-attach-disk]:../../linux/add-disk.md
[virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]:../../linux/add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk
[virtual-machines-linux-tutorial]:../../linux/quick-create-cli.md
[virtual-machines-linux-update-agent]:../../linux/update-agent.md
[virtual-machines-manage-availability]:../../linux/manage-availability.md
[virtual-machines-ps-create-preconfigure-windows-resource-manager-vms]:virtual-machines-windows-create-powershell.md
[virtual-machines-sizes-linux]:../../linux/sizes.md
[virtual-machines-sizes-windows]:../../windows/sizes.md
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
[virtual-networks-multiple-nics-windows]:../../windows/multiple-nics.md
[virtual-networks-multiple-nics-linux]:../../linux/multiple-nics.md
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
[capture-image-linux-step-2-create-vm-image]:../../linux/capture-image.md#step-2-create-vm-image

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

Microsoft Azure, uzun tedarik döngüleri olmadan en az sürede şirketler tooacquire işlem ve depolama kaynaklarını sağlar. Azure sanal makineleri SAP NetWeaver Azure uygulamalara dayalı gibi şirketler toodeploy Klasik uygulamaları izin verir ve daha fazla kaynak kullanılabilir şirket içi gerek kalmadan, güvenilirlik ve kullanılabilirlik genişletme. Azure sanal makine hizmetleri de şirket içi bağlantılar, hangi etkinleştirir şirketler tooactively tümleştirmek Azure sanal makineler kendi şirket içi etki alanlarına, kendi özel Bulutlar ve bunların SAP sistem yatay destekler.
Bu teknik incelemede hello temelleri Microsoft Azure sanal makinesi açıklar ve Azure SAP NetWeaver yüklemeleri için planlama ve uygulama ile ilgili bir kılavuz sağlar ve bu nedenle hello belge tooread başlatmadan önce olmalıdır SAP NetWeaver Azure ile ilgili gerçek dağıtımları.
Merhaba kağıt hazırlandı hello SAP yükleme belgelerini ve yüklemeleri ve SAP yazılımı dağıtımları için birincil kaynaklar hello temsil SAP Notlar platformları verilir.

## <a name="summary"></a>Özet
Bulut bilgi işlem, daha da fazla önem hello BT endüstri içinde toolarge ve çokuluslu şirketler yukarı küçük şirketlerden elde yaygın olarak kullanılan bir terimdir.

Microsoft Azure hello paylaşılabilen çok sayıda yeni olanakları sunan Microsoft bulut hizmetleri platformu ' dir. Şimdi değil sınırlı tootechnical veya bütçeleme kısıtlamaları; bu nedenle müşterilerin hello bulutta bir hizmet olarak mümkün toorapidly sağlama ve devre dışı bırakma sağlama uygulamaları önerilir. Donanım altyapısını zamandan ve yatırım yapmak yerine, şirketler Merhaba uygulaması, iş süreçlerini ve onun avantajlarını müşteriler ve kullanıcılar için odaklanabilirsiniz.

Microsoft, Microsoft Azure Sanal Makine Hizmetleri ile kapsamlı bir Hizmet Olarak Altyapı (IaaS) platformu sunmaktadır. SAP NetWeaver tabanlı uygulamalar, Azure Sanal Makinelerinde (IaaS) desteklenmektedir. Bu teknik nasıl tooplan ve uygulama SAP NetWeaver Microsoft Azure içindeki seçim hello platform olarak tabanlı uygulamaları açıklar.

Merhaba kağıt kendisini iki ana yönlere odaklanır:

* Merhaba ilk bölümü Azure üzerinde SAP NetWeaver tabanlı uygulamalar için iki desteklenen dağıtım desenleri açıklar. Ayrıca, Azure genel işleme aklınızda SAP dağıtımlarla anlatır.
* Merhaba iki farklı senaryolar Hello ilk bölümünde açıklanan uygulama hello ikinci bölümü ayrıntıları.

Ek kaynaklar için bölüm bkz [kaynakları] [ planning-guide-1.2] bu belgedeki.

### <a name="definitions-upfront"></a>Önceden tanımları
Merhaba belge boyunca aşağıdaki koşulları hello kullanın:

* Iaas: Hizmet olarak altyapı
* PaaS: Hizmet olarak Platform
* SaaS: Hizmet olarak yazılım
* ARM: Azure Kaynak Yöneticisi
* SAP bileşen: tek tek SAP gibi bir uygulama ECC, bant genişliği, çözüm Yöneticisi veya EP'deki  SAP bileşenleri geleneksel ABAP veya Java teknolojiler ya da olmayan-tabanlı NetWeaver uygulama iş nesneleri gibi temel alabilir.
* SAP ortamı: bir veya daha fazla SAP bileşenleri tooperform geliştirme, QAS, eğitim, DR veya üretim gibi işletme işlevi mantıksal olarak gruplandırılır.
* SAP yatay: Bu toohello Müşteri'nin tüm SAP varlıkları başvuruyor BT yatay. Merhaba SAP yatay tüm üretim ve üretim dışı ortamlar içerir.
* SAP sistem: hello birleşimi DBMS katman ve uygulama katmanı, örneğin, bir SAP ERP geliştirme sistemi, SAP BW test sistemini, SAP CRM üretim sistem vb... Azure dağıtımlarda, desteklenen toodivide olmadığından bu iki katmanı şirket içi ve Azure arasında. Şirket içi SAP sistem ya da bu anlamına gelir dağıtılan veya Azure'da dağıtılır. Ancak, Azure veya şirket içi SAP yatay hello farklı sistemlerini dağıtabilirsiniz. Örneğin, azure'da hello SAP CRM geliştirme ve test sistemlerini dağıtmak ancak SAP CRM üretim sistem şirket içi hello.
* Yalnızca bulut dağıtım: Burada bir site siteye hello Azure aboneliğine bağlı değil ya da ExpressRoute bağlantı toohello şirket içi ağ altyapısı dağıtımı. Ortak Azure belgelerine bu tür dağıtımlar da 'Yalnızca bulut' dağıtımları açıklanmıştır. Bu yöntem ile dağıtılan sanal makineleri yoluyla erişilir Internet hello ve atanan toohello VM'ler için Azure'da bir ortak IP adresi ve/veya ortak bir DNS adı. Şirket içi Active Directory (AD) için Microsoft Windows hello ve DNS dağıtımları bu tür tooAzure genişletilmedi. Bu nedenle hello VM'ler hello şirket içi Active Directory parçası değildir. Aynı, örneğin, OpenLDAP + kullanarak Kerberos Linux uygulamaları için geçerlidir.

> [!NOTE]
> Bu belgede yalnızca bulut dağıtımında tam SAP Windows'un özel olarak Azure Active Directory uzantısız çalışıyor olarak tanımlanan / OpenLDAP veya şirket içi genel Buluta ad çözümlemesi. Yalnızca bulut yapılandırmaları, üretim SAP sistemleri veya SAP STMS veya diğer şirket içi kaynakları Azure ve şirket içi bulunan kaynaklar üzerinde barındırılan SAP sistemleri arasında kullanılan toobe gereken yeri yapılandırması için desteklenmez.
>
>

* Şirket içi: VM'ler dağıtılan tooan siteden siteye, çok siteli veya ExpressRoute bağlantısı hello şirket içi inizdeki ve Azure arasında sahip Azure aboneliğinizin bulunduğu bir senaryoyu açıklar. Ortak Azure belgelerine dağıtımları bu tür şirket içi senaryoları açıklanmıştır. Merhaba hello bağlantı tooextend şirket içi etki alanları, şirket içi Active Directory/OpenLDAP ve DNS Azure'da şirket içi nedeni. Merhaba şirket içi yatay hello aboneliğin Azure varlıklar genişletilmiş toohello olduğu. Bu uzantı, hello VM'ler hello şirket içi etki alanının parçası olabilir. Merhaba şirket içi etki alanının etki alanı kullanıcıları hello sunucularına erişebilir ve Hizmetleri üzerindeki VM'ler (DBMS Hizmetleri gibi) çalıştırabilirsiniz. Dağıtılan VM'ler şirket içi ve Azure dağıtılan VM'ler arasında iletişim ve ad çözümleme mümkündür. Bu çoğu SAP varlıklar toobe dağıtılmış bekliyoruz hello senaryodur. Daha fazla bilgi için bkz: [bu] [ vpn-gateway-cross-premises-options] makale ve [bu][vpn-gateway-site-to-site-create].

> [!NOTE]
> Şirket içi dağıtımları SAP sistemleri çalışan Azure sanal makineleri bir şirket içi etki alanının üyesi olduğu SAP sistemlerinin üretim SAP sistemleri için desteklenir. Şirketler arası yapılandırmalar bölümleri dağıtmak için desteklenen veya Azure'da SAP Windows'un tamamlayın. Azure'da hello tam SAP yatay bile çalışan, şirket içi etki alanı ve REKLAM/OpenLDAP parçası olan bu VM'lerin olması gerektirir. Merhaba belgelerine önceki sürümlerinde, biz hello terim 'Karma' şirket içi bağlantılar şirket içi ve Azure arasında olduğunu hello aslında burada kökü karma BT senaryoları hakkında açıklandı. Ayrıca, bu hello VM'ler için Azure'da hello parçası olan hello olgu Active Directory şirket içi / OpenLDAP.
>
>

Bazı Microsoft belgeleri şirketler arası senaryoları özellikle DBMS HA yapılandırmaları için biraz farklı bir şekilde açıklanmıştır. Merhaba SAP ilgili belgeleri Hello durumda hello şirketler arası senaryo toohaving yalnızca hello SAP yatay şirket içi ve Azure arasında dağıtılmış bir siteden siteye veya özel (ExpressRoute) bağlantısı ve hello olgu boils.  

### <a name="e55d1e22-c2c8-460b-9897-64622a34fdff"></a>Kaynakları
Merhaba aşağıdaki ek kılavuzlar için SAP dağıtımlarını azure'da hello konu kullanılabilir:

* [Azure sanal makineleri planlama ve uygulama SAP NetWeaver (Bu belgenin) için][planning-guide]
* [SAP NetWeaver için Azure sanal makineler dağıtımı][deployment-guide]
* [SAP NetWeaver için Azure sanal makineleri DBMS dağıtımı][dbms-guide]

> [!IMPORTANT]
> Olası SAP Yükleme Kılavuzu'na başvuran bir bağlantı toohello yerde kullanılan (başvuru InstGuide-01, bkz: <http://service.sap.com/instguides>). Toohello Önkoşullar ve yükleme işlemi, hello SAP NetWeaver yükleme kılavuzları geldiğinde her zaman bu belgeyi yalnızca bir Microsoft Azure sanal makinede yüklü SAP NetWeaver sistemler için belirli görevler kapsadığından dikkatlice okuyun olması gerekir.
>
>

SAP notları aşağıdaki hello Azure üzerinde SAP ilgili toohello konu şunlardır:

| Not numarası | Başlık |
| --- | --- |
| [1928533] |Azure üzerinde SAP uygulamaları: desteklenen ürünler ve boyutlandırma |
| [2015553] |Microsoft Azure üzerinde SAP: Destek önkoşulları |
| [1999351] |Gelişmiş Azure için SAP izleme sorunlarını giderme |
| [2178632] |Microsoft Azure üzerinde SAP için ölçümleri izleme anahtarı |
| [1409604] |Windows sanallaştırma: İzleme Gelişmiş |
| [2191498] |Azure ile Linux üzerinde SAP: İzleme Gelişmiş |
| [2243692] |Microsoft Azure (Iaas) VM Linux'ta: SAP lisans sorunları |
| [1984787] |SUSE LINUX Enterprise Server 12: Yükleme notları |
| [2002167] |Red Hat Enterprise Linux 7.x: yükleme ve yükseltme |
| [2069760] |Oracle Linux 7.x SAP yükleme ve yükseltme |
| [1597355] |Linux takas alanı önerisi |

Ayrıca hello okuma [SCN Wiki](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) , Linux için tüm SAP notlar içerir.

Genel varsayılan sınırlamalar ve Azure abonelikleri maksimum sınırlamaları bulunabilir [bu makalede][azure-subscription-service-limits-subscription].

## <a name="possible-scenarios"></a>Olası senaryolar
SAP çok hello en kritik kuruluşların uygulamalardan biri olarak görülür. Merhaba mimarisi ve işlemler bu uygulamaların çoğunlukla çok karmaşık ve kullanılabilirlik ve performans gereksinimlerini karşıladığınızdan emin olma önemlidir.

Bu nedenle işletmenin dikkatle hakkında uygulamaları genel bulut ortamında, seçilen hello bulut sağlayıcısı bağımsız çalıştırılabilir toothink vardır.

SAP NetWeaver dağıtmak için olası sistem türleri tabanlı uygulamaları içinde genel bulut ortamlarında aşağıda listelenmiştir:

1. Orta ölçekli üretim sistemleri
2. Geliştirme sistemleri
3. Test sistemleri
4. Prototip sistemleri
5. Öğrenme / tanıtım sistemleri

Sipariş toosuccessfully SAP sistemleri Azure Iaas veya Iaas genel dağıtmak, önemli toounderstand hello önemli farklılıkları hello teklifleri geleneksel outsourcers veya barındırıcılar ve Iaas teklifleri. Merhaba geleneksel barındırma sağlayıcısı veya dış kaynak altyapısı (ağ, depolama ve sunucu türü) toohello iş yüküne uyum sağlar ancak toohost bir müşterinin istediği, bunun yerine hello Müşteri'nin sorumluluk toochoose hello sağ iş yükü Iaas dağıtımları için olur.

İlk adım olarak, müşteriler aşağıdaki öğelerindeki tooverify hello gerekir:

* Merhaba SAP desteklenen Azure VM türleri
* Azure'da Hello SAP desteklenen ürünler/yayınlar
* Hello hello belirli SAP Azure'da yayımlar için desteklenen işletim sistemi ve DBMS yayınlar
* Farklı Azure SKU'ları tarafından sağlanan SAP işleme

Merhaba yanıtlar toothese sorular SAP notta okunabilir [1928533].

İkinci bir adım olarak, Azure kaynak ve bant genişliği sınırlamaları karşılaştırıldığında toobe tooactual kaynak tüketimini şirket içi sistemleri gerekir. Bu nedenle, müşterilerin gerek toobe hello farklı özellikleri tanıdık SAP hello alanı ile desteklenen Azure türleri hello:

* CPU ve bellek kaynakları farklı VM türler ve
* IOPS bant genişliği farklı VM türler ve
* Farklı VM türler özelliklerini ağ.

Bu verilerin çoğunu bulunabilir [burada (Linux)] [ virtual-machines-sizes-linux] ve [burada (Windows)][virtual-machines-sizes-windows].

Yukarıdaki hello bağlantıyı listelenen sınırları hello unutmayın konusunda üst sınırı. Merhaba sınırlarını hello kaynaklardan herhangi birini, örneğin IOPS tüm koşullar altında sağlanabilir olduğunu anlamına gelmez. Merhaba ancak seçilen bir VM türüne hello CPU ve bellek kaynakları durumlardır. SAP tarafından desteklenen hello VM türlerinde hello CPU ve bellek kaynakları zaman hello VM içinde tüketimi için ayrılmış ve bu nedenle herhangi bir noktada kullanılabilir.

Merhaba Microsoft Azure platformu diğer Iaas platformlar gibi bir çok kiracılı platformudur. Başka bir deyişle, depolama, ağ ve diğer kaynakları kiracılar arasında paylaşılır. Akıllı azaltma ve kota mantığı kazanmadan ciddi bir şekilde başka bir kiracı (gürültülü komşu) hello performansını etkileyen gelen kullanılan tooprevent bir kiracı ' dir. Azure mantığında yaşadı bant genişliği tookeep Varyanslar çalışır ancak küçük, yüksek oranda paylaşılan platformları, şirket içi dağıtımlarına kaynak/bant genişliği kullanılabilirliği, toointroduce büyük sapmalar birçok müşteri kullanılan tooin daha eğilimlidir. Sonuç olarak, farklı ağ veya depolama g/ç (Merhaba birim yanı sıra gecikme) ilgili bant genişliği düzeylerinden dakika toominute karşılaşabilirsiniz. Azure SAP sistemde bir şirket içi sistemde daha büyük sapmalar karşılaşabilir hello olasılık hesaba toobe gerekir.

Tooevaluate kullanılabilirlik gereksinimlerini bir son adımdır. Olabilir, Azure altyapı temel bu hello güncelleştirilmiş tooget gerekiyor ve yeniden VM'ler toobe çalıştıran hello ana gerektirir. Bu durumlarda, bu konaklarda çalışan sanal makineler kapatılması ve de yeniden. belirli bir bölge için çekirdek olmayan iş saatleri sırasında Hello zamanlama böyle bakım yapılır ancak yeniden başlatma gerçekleşir birkaç saatlerde hello olası görece geniş bir penceredir. Vardır toomitigate bazı teknolojiler hello olabilir Azure platformu içinde yapılandırılmış veya tüm hello böyle güncelleştirmeleri etkiler. Gelecekteki yeniliklerini Azure platformu, DBMS hello ve SAP uygulamadan toominimize hello etkisini gibi yeniden tasarlanmıştır.

Toosuccessfully dağıtmanız Azure SAP sisteme, hello SAP sistemleri işletim sistemi, veritabanı, şirket içi ve SAP uygulamaları hello SAP Azure destek matrisi, hello kaynakları hello Azure altyapısı içinde uygun sağlayabilir ve hangi görünmesi gerekir Kullanılabilirlik SLA Microsoft Azure'un sunduğu hello ile çalışabilirsiniz. Bu sistemlere tanımlandığı gibi iki dağıtım senaryosu aşağıdaki hello birinde toodecide gerekir.

### <a name="1625df66-4cc6-4d60-9202-de8a0b77f803"></a>Yalnızca bulut - Azure sanal makine dağıtımlarınızı hello bağımlılıkları olmadan şirket içi müşteri ağ
![SAP demo veya Azure'da dağıtılan eğitim senaryo ile tek VM][planning-guide-figure-100]

Bu senaryo SAP ve SAP olmayan yazılım'ın tüm hello bileşenleri tek bir VM içinde yüklendiği eğitimleri veya tanıtım sistemleri için genel bir durumdur. Bu dağıtım senaryosunda, üretim SAP sistemleri desteklenmez. Genel olarak, bu senaryonun gereksinimlerine hello uyuyor:

* Merhaba VM'ler kendilerini hello genel ağ üzerinden erişilebilir. Merhaba VM'ler toohello içinde çalışan hello uygulamalar için doğrudan ağ bağlantısı içi hello gösterileri veya eğitimleri içeriğe sahip olan ya da hello şirket ağı veya hello müşteri gerekli değildir.
* Merhaba eğitimleri veya tanıtım senaryo temsil eden birden çok VM durumunda ağ iletişimleri ve ad çözümleme hello VM'ler arasında toowork gerekir. Ancak VM'ler hello kümesi arasındaki iletişimi VM'ler birkaç kümesi yan yana girişim dağıtılabilir böylece yalıtılmış toobe gerekir.  
* Internet bağlantısı hello son kullanıcı tooremote oturumu için sanal makineleri Azure üzerinde barındırılan toohello içine gereklidir. Merhaba konuk işletim sistemi bağlı olarak, Terminal Hizmetleri/RDS veya VNC/ssh kullanılan tooaccess hello VM tooeither hello eğitim görevleri yerine getirmek veya hello gösterileri gerçekleştirin. SAP gibi 3200, 3300 & 3600 can bağlantı noktaları, aynı zamanda ortaya hello SAP uygulama örneği herhangi Internet bağlantılı masaüstünden erişilebilir.
* Merhaba SAP sistemleri (ve yalnızca son kullanıcı erişimi için ortak Internet bağlantısı gerektirir ve bir bağlantı tooother azure'da VM gerektirmez Azure tek başına senaryoda VM(s)) temsil eder.
* SAPGUI ve tarayıcı yüklenir ve hello üzerinde doğrudan VM çalıştırılır.
* VM toohello özgün durumunun hızlı bir sıfırlama ve yeni dağıtım, özgün durumuna yeniden gereklidir.
* Tanıtım ve eğitim senaryoları Hello durumda hangi gerçekleşen birden çok VM, bir Active Directory / OpenLDAP ve/veya DNS hizmeti VM'ler her kümesi için gereklidir.

![Sanal makinenin bir tanıtım veya bir Azure bulut hizmeti eğitim senaryoda temsil eden, Grup][planning-guide-figure-200]

Burada her hello kümesinin hello VM adları olan hello aynı gerek toobe paralel olarak dağıtılan sanal makine her hello hello aklınızda tookeep ayarlar önemlidir.

### <a name="f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10"></a>Şirket içi - tek dağıtımını ya da Azure hello şirket içi ağınıza tam olarak tümleştirilmiş hello zorunluluğu ile içine birden çok SAP VM
![VPN siteden siteye bağlantı (şirket içi)][planning-guide-figure-300]

Bu senaryo, birçok olası dağıtım desenlerle bir şirket içi senaryodur. Basit hello SAP yatay şirket içi bazı bölümleri ve diğer bölümleri hello SAP yatay, Azure üzerinde çalışan olarak açıklanan olabilir. Merhaba SAP bileşenleri bir parçası Azure üzerinde çalışan hello olgu tüm yönlerini son kullanıcılar için saydam olmalıdır. Bu nedenle SAP aktarım düzeltme sistem (STMS), RFC iletişimi yazdırma Merhaba, Azure üzerinde çalışan hello SAP sistemler için güvenlik (SSO gibi) vb.'ın sorunsuz bir şekilde çalışır. Ancak hello şirketler arası senaryo da burada hello tam SAP yatay Azure'da hello Müşteri'nin etki alanı ile çalışır ve Azure'da DNS genişletilmiş bir senaryo açıklanmaktadır.

> [!NOTE]
> Üretken SAP sistemleri çalıştırmak için desteklenen hello dağıtım senaryosu budur.
>
>

Okuma [bu makalede] [ vpn-gateway-create-site-to-site-rm-powershell] hakkında daha fazla bilgi için tooconnect tooMicrosoft Azure şirket içi ağ

> [!IMPORTANT]
> Azure ve şirket içi müşteri dağıtımlar arasında şirketler arası senaryolar hakkında varsayılır, tüm SAP sistemleri hello bazda arıyoruz. Olan senaryoları *desteklenmiyor* için şirket içi senaryolar şunlardır:
>
> * SAP uygulamaları farklı katmanlar farklı dağıtım yöntemleri çalışıyor. Örneğin hello DBMS katman şirket içi ancak hello SAP uygulama katmanı Azure Vm'leri olarak (veya tersi) dağıtılan VM'ler içinde çalışır.
> * Azure ve bazı şirket içi SAP katmanda bazı bileşenleri. Örneğin, şirket içi ve Azure sanal makineleri arasındaki hello SAP uygulama katmanı örneklerini bölme.
> * Bir sistem SAP örnekleri birden çok Azure bölgeleri üzerinde çalışan sanal makineler dağıtımını desteklenmiyor.
>
> Bu kısıtlamalar Hello nedeni, çok düşük gecikme süresi yüksek performanslı bir ağ özellikle hello uygulama örnekleri ile bir SAP sisteminin hello DBMS katman arasındaki bir SAP sistemi içinde hello gereksinimdir.
>
>

### <a name="supported-os-and-database-releases"></a>Desteklenen işletim sistemi ve veritabanı sürümleri
* Bu makalede Azure sanal makine Hizmetleri'ni listelenen için desteklenen Microsoft sunucu yazılımı: <http://support.microsoft.com/kb/2721672>.
* İşletim sistemi sürümleri desteklenir, SAP yazılım ile birlikte Azure sanal makine hizmetlerini desteklenen veritabanı sistemi sürümleri SAP notta belgelenen [1928533].
* SAP uygulamaları ve Azure sanal makine hizmetlerini desteklenen sürümler SAP notta belgelenmiştir [1928533].
* Yalnızca 64 Bit görüntüleri desteklenen toorun SAP senaryolar için azure'da Konuk VM olarak verilmiştir. Bu, aynı zamanda yalnızca 64-bit SAP uygulamaları ve veritabanları desteklenir anlamına gelir.

## <a name="microsoft-azure-virtual-machine-services"></a>Microsoft Azure sanal makine Hizmetleri
Merhaba Microsoft Azure Hizmetleri platform barındırılan ve Microsoft veri merkezleri işletilen Internet ölçeğinde bulut platformudur. Merhaba platform hello Microsoft Azure sanal makine Hizmetleri (bir hizmet veya Iaas olarak altyapı) ve zengin bir Platform olarak hizmet (PaaS) özellikleri kümesi içerir.

Hello Azure platformu teknoloji eylemli hello gereksinimini azaltır ve altyapı satın alır. Koruma basitleştirir ve uygulamaları işletim isteğe bağlı hesaplama ve depolama toohost sağlayarak ölçekleme ve web uygulaması ve bağlı uygulamaları yönetme. Altyapı yönetimi, yüksek kullanılabilirlik için tasarlanmış bir platformuyla otomatik ve dinamik toomatch kullanımı ihtiyaçları Kullandıkça Öde fiyatlandırma modeli hello seçeneğiyle ölçeklendirme.

![Microsoft Azure sanal makine hizmetlerini konumlandırma][planning-guide-figure-400]

Azure sanal makine Services ile Microsoft (bkz: Şekil 4) Iaas örnekleri toodeploy özel sunucu görüntüleri tooAzure etkinleştirildiğini. Merhaba azure'da sanal makineler Hyper-V sanal sabit sürücülerde (VHD) temel alır ve konuk işletim sistemi olarak farklı işletim sistemlerine yükleyebilirsiniz toorun vardır.

İşletimsel açısından bakıldığında, Azure sanal makine hizmeti benzer sunar hello şirket içinde dağıtılan sanal makineleri olarak karşılaşır. Bununla birlikte, gerek duymadığınız hello önemli avantajı vardır tooprocure, yönetmek ve hello altyapısını yönetme. Geliştiriciler ve Yöneticiler bu sanal makineleri içindeki hello işletim sistemi görüntüsünün tam denetime sahiptir. Yöneticiler uzaktan toothose sanal makineleri tooperform Bakım ve görevler gibi yazılım dağıtım görevlerini sorun gidermeye oturum açabilir. Hesaba toodeployment içinde hello yalnızca kısıtlamaları hello boyutları ve Azure Vm'leri özelliklerini var. Bunlar gibi ince olmayabilir bu şirket içinde yapılabilir gibi ayrıntılı yapılandırma. VM türlerinin bileşimini temsil eden bir seçenek vardır:

* Vcpu'lar sayısı,
* Bellek
* Eklenebilecek VHD'ler sayısı,
* Ağ ve depolama bant genişlikleri.

Merhaba boyutu ve çeşitli farklı sanal makinelerin boyutları sınırlamaları sunulan bir tabloda görülme [bu makalede (Linux)] [ virtual-machines-sizes-linux] ve [bu makalede (Windows)] [ virtual-machines-sizes-windows].

Anladıkça, farklı aileleri ya da sanal makineleri dizi vardır. Sanal makineleri aileleri aşağıdaki hello ayırt edebilirsiniz:

* A0 A7 VM türleri: Bu tüm SAP için sertifikalıdır. Azure Iaas ile sunulan ilk VM dizisi.
* A8-A11 VM türleri: yüksek performanslı örnekleri bilgi işlem. Farklı daha iyi gerçekleştirme çalışan diğer A-series VM'ler daha ana işlem.
* Dv2/D-serisi VM türler: A0 A7 daha iyi gerçekleştirme. Merhaba VM türlerinin tümü SAP ile sertifikalı.
* DS/DSv2 serisi VM türler: benzer tooD/Dv2-serisi, ancak mümkün tooconnect tooAzure Premium depolama olan (bölüm bkz [Azure Premium Storage] [ planning-guide-3.3.2] bu belgenin). Yeniden tüm VM türleri SAP ile sertifikalı.
* G-serisi VM türler: yüksek bellek VM türler.
* GS serisi VM türler: G-serisi gibi ancak hello seçeneği toouse Azure Premium Storage da dahil olmak üzere (bölüm bkz [Azure Premium Storage] [ planning-guide-3.3.2] bu belgenin). GS serisi VM'ler veritabanı sunucusu olarak kullanıldığında, DB veri ve işlem günlük dosyaları için zorunlu toouse Premium depolama.

Farklı VM serisinin aynı CPU ve bellek yapılandırmalarını hello bulabilirsiniz. Bununla birlikte, bunlar hello işleme performansını bu Vm'lere hello farklı serisi dışında baktığınızda önemli ölçüde değişebilir. Sahip olmasına rağmen aynı hello CPU ve bellek yapılandırma. Merhaba temel alınan ana bilgisayar sunucu donanımı hello farklı VM türler hello giriş farklı verimlilik vardı nedenidir.  Genellikle verimliliği performansından gösterilen hello fark hello hello fiyatına da yansıtılır farklı VM'ler.

Tüm farklı VM dizisi Merhaba Azure bölgeleri (Azure bölgeleri sonraki bölüme bakın) her birinde sunulan. Ayrıca tüm sanal makineleri veya VM seri için SAP sertifikalı unutmayın.

> [!IMPORTANT]
> SAP NetWeaver tabanlı uygulamaları Hello kullanılmak VM türleri ve yapılandırmaları yalnızca hello alt listelenen SAP notta [1928533] desteklenir.
>
>

### <a name="be80d1b9-a463-4845-bd35-f4cebdb5424a"></a>Azure bölgeleri
Microsoft, böylece çağrılan 'bölgelere Azure' toodeploy sanal makineleri sağlar. Bir Azure bölgesi yakınında içinde bulunan bir veya birden çok veri merkezleri olabilir. Merhaba Dünya Microsoft coğrafi bölgelerde hello çoğu için en az iki Azure bölgeleri vardır. Örneğin, Avrupa'da bir Azure Bölgesi 'Kuzey Avrupa' ve 'Batı Avrupa' yok. Böylece teknik veya doğal afetler hello hem Azure bölgelerde etkilemez coğrafi bölge içindeki iki tür Azure bölgeleri yeterince önemli uzaklığı tarafından ayrılmış olan aynı coğrafi bölge. Microsoft sürekli olarak farklı coğrafi bölgeler yeni Azure bölgelerde çıkışı genel oluşturuyor olduğundan, bu bölgeler hello sayısı sürekli büyüyen ve Ara 2015'ten itibaren ek bölgeler önceden duyurulmuş 20 Azure bölgesiyle hello sayısına ulaşıldı. Bir müşteri olarak SAP sistemleri hello iki Azure bölgeleri Çin'de dahil olmak üzere tüm bu bölgeler, içine dağıtabilirsiniz. Azure bölgeler hakkında güncel güncel bilgiler için bu Web sitesine bakın: <https://azure.microsoft.com/regions/>

### <a name="8d8ad4b8-6093-4b91-ac36-ea56d80dbf77"></a>Merhaba Microsoft Azure sanal makine kavramı
Microsoft Azure altyapı (Iaas) çözümü toohost sanal makineler ile benzer işlevler bir şirket içi sanallaştırma çözümü olarak sunar. Hangi dağıtım ve yönetim yetenekleri de sunar mümkün toocreate sanal makinelerden hello Azure portal, PowerShell veya CLI, içinde olduğu.

Azure Resource Manager bildirim temelli bir şablon kullanarak uygulamalarınızı tooprovision sağlar. Tek bir şablonda birden çok hizmeti bağımlılıklarıyla birlikte dağıtabilirsiniz. Merhaba kullandığınız aynı şablon toorepeatedly her aşaması sırasında uygulamanızın hello uygulama yaşam döngüsü veya dağıtın.

Resource Manager şablonları kullanma hakkında daha fazla bilgi şurada bulunabilir:

* [Dağıtmak ve Azure Resource Manager şablonları ve hello Azure CLI kullanarak sanal makineleri yönetme] [.. /.. / linux/create-ssh-secured-vm-from-template.md]
* [Azure Resource Manager ve PowerShell kullanarak sanal makineleri yönetme][virtual-machines-deploy-rmtemplates-powershell]
* <https://Azure.microsoft.com/documentation/Templates/>

Başka bir ilginç hello özelliği toocreate görüntüleri sanal makinelerden tooprepare mümkün tooquickly olan depoları gereksinimlerinizi karşılayacak sanal makine örnekleri dağıtma belirli sağlayan özelliktir.

Sanal makinelerden görüntüleri oluşturma hakkında daha fazla bilgi bulunabilir [bu makalede (Linux)] [ virtual-machines-linux-capture-image-resource-manager] ve [bu makalede (Windows)] [ virtual-machines-windows-capture-image-resource-manager].

#### <a name="df49dc09-141b-4f34-a4a2-990913b30358"></a>Hata etki alanları
Hata etki alanlarını hata, veri merkezleri ve fiziksel dikey veya raf hata etki alanı kabul edilebilir sırada yer alan çok yakından ilgili toohello fiziksel altyapı fiziksel bir birimi temsil eder, hello iki arasında doğrudan bire bir eşleme yoktur.

Microsoft Azure sanal makine Hizmetleri'ndeki bir SAP sisteminin bir parçası olarak birden çok sanal makine dağıttığınızda, farklı hata böylece hello hello gereksinimleri toplantı etki alanları, uygulamanıza hello Azure yapı denetleyicisi toodeploy etkileyebilir. Microsoft Azure SLA. Ancak, dağıtım hata etki alanı Azure ölçek birimi (yüzlerce işlem düğümleri veya depolama düğümleri ve ağ koleksiyonu) hello ya da VM'ler tooa hello atamasının belirli hata etki alanı üzerinde sahip olmadığınız bir şey doğrudan denetim. Sipariş toodirect hello Azure yapı denetleyicisi toodeploy içinde bir dizi farklı hata etki alanları üzerinden VM'ler, dağıtım sırasında tooassign bir Azure kullanılabilirlik kümesi toohello VM'ler gerekir. Bölüm Azure kullanılabilirlik kümeleri hakkında daha fazla bilgi için bkz: [Azure kullanılabilirlik kümeleri] [ planning-guide-3.2.3] bu belgedeki.

#### <a name="fc1ac8b2-e54a-487c-8581-d3cc6625e560"></a>Yükseltme etki alanları
Yükseltme etki alanlarının bir VM içinde birden çok VM çalıştıran SAP örneklerinin oluşan bir SAP sistemi içinde nasıl güncelleştirileceğini toodetermine yardımcı bir birimi temsil eder. Microsoft Azure yükseltme oluştuğunda, bu yükseltme etki alanları tek tek güncelleştirme hello süreci devam ettiği. Farklı yükseltme etki alanları VM'ler dağıtım sırasında yayarak kısmen potansiyel kesintiler SAP sisteminizi koruyabilirsiniz. İçinde farklı yükseltme etki alanları yayılan bir SAP sisteminin hello VM'ler tooforce Azure toodeploy sipariş, her bir VM Dağıtım sırasında tooset belirli bir özniteliği gerekir. Benzer tooFault etki alanları, bir Azure ölçek birimi birden fazla yükseltme etki alanlarına bölünür. Sipariş toodirect hello Azure yapı denetleyicisi toodeploy içinde bir dizi farklı yükseltme etki alanları üzerinden VM'ler, dağıtım sırasında tooassign bir Azure kullanılabilirlik kümesi toohello VM'ler gerekir. Bölüm Azure kullanılabilirlik kümeleri hakkında daha fazla bilgi için bkz: [Azure kullanılabilirlik kümeleri] [ planning-guide-3.2.3] aşağıda.

#### <a name="18810088-f9be-4c97-958a-27996255c665"></a>Azure kullanılabilirlik kümeleri
Azure sanal makineleri bir Azure kullanılabilirlik kümesi içinde hello Azure yapı denetleyicisi tarafından farklı hata ve yükseltme etki alanları dağıtılır. farklı hata ve yükseltme etki alanları üzerinden hello dağıtım Hello amacı altyapı Bakımı hello durumunun veya bir hata etki alanı içinde bir hatası engeller SAP sistemin tüm sanal makineleri kapatmak tooprevent budur. Varsayılan olarak, sanal makineleri bir kullanılabilirlik kümesinin parçası değildir. bir VM Hello katılım bir kullanılabilirlik kümesindeki dağıtım zamanında veya daha sonra yeniden yapılandırılması ve bir VM yeniden dağıtımını tarafından tanımlanır.

Kullanılabilirlik kümeleri arasında ilişki tooFault ve yükseltme etki alanları, Azure kullanılabilirlik kümeleri ve hello yol toounderstand hello kavramı okuma [bu makalede][virtual-machines-manage-availability]

bir json şablonu aracılığıyla ARM toodefine kullanılabilirlik kümelerini görmek [rest API belirtimlerin hello](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2015-06-15/swagger/compute.json) ve "kullanılabilirlik" arayın.

### <a name="a72afa26-4bf4-4a25-8cf7-855d6032157f"></a>Depolama: Microsoft Azure depolama ve veri diskleri
Microsoft Azure sanal makineleri farklı depolama türlerini kullanın. Azure sanal makine hizmetlerini SAP uygulama depolama bu iki ana türleri arasındaki önemli toounderstand hello farkları olur:

* Kalıcı olmayan, geçici depolama alanı.
* Kalıcı depolama.

Merhaba kalıcı olmayan depolama çalışan sanal makineleri doğrudan bağlı toohello olan ve hello işlem düğümlerinde kendilerini – hello yerel örnek depolama (geçici depolama) bulunur. Merhaba boyutu hello hello hello dağıtım başlatıldığında seçilen sanal makine boyutuna bağlıdır. Bu depolama türü volatile ve bu nedenle hello disk bir sanal makine örneğini yeniden başlatıldığında başlatılır. Genellikle, Başlangıç disk belleği dosyası başlangıç işletim sistemi için bu geçici bir diskte yer alır.

- - -
> ![Windows][Logo_Windows] Windows
>
> Windows Vm'lerinde sürücü D:\ dağıtılan bir VM olarak hello temp sürücüsü bağlı.
>
> ![Linux][Logo_Linux] Linux
>
> Linux VM'ler üzerinde /mnt/resource veya /mnt takılı. Daha fazla ayrıntıları buraya bakın:
>
> * [Nasıl tooAttach veri diski tooa Linux sanal makine][virtual-machines-linux-how-to-attach-disk]
> * <https://docs.microsoft.com/Azure/Storage/Storage-About-Disks-and-vhds-Linux#Temporary-disk>
>
>

- - -
hello ana bilgisayar sunucusunun kendisi üzerinde depolandığından hello gerçek volatile sürücüdür. Merhaba VM bir dağıtımın taşınsa (örneğin son toomaintenance hello konak veya kapatma ve yeniden başlatma) hello sürücü Merhaba içeriğine kaybolur. Bu nedenle, bir seçenek toostore değil Bu sürücüde herhangi bir önemli veri. Bu depolama türü için kullanılan medya türünü Hello neye benzediğini gösteren, Haziran 2015'ten itibaren çok farklı performans özellikleri olan farklı VM dizisi farklıdır:

* A5-A7: Çok sınırlı performans. Sayfa dosyası dışındaki her şey için önerilmez
* A8-A11: Bazı on bin IOPS ile çok iyi performans özellikleri ve > 1GB/sn verim.
* D-serisi: Bazı sonra bin IOPS ile çok iyi performans özellikleri ve > 1GB/sn verim.
* DS serisi: Bazı on bin IOPS ile çok iyi performans özellikleri ve > 1GB/sn verim.
* G-serisi: Bazı on bin IOPS ile çok iyi performans özellikleri ve > 1GB/sn verim.
* GS serisi: Bazı on bin IOPS ile çok iyi performans özellikleri ve > 1GB/sn verim.

Yukarıdaki deyimleri SAP ile sertifikalı toohello VM türleri uyguladığınızı. Merhaba VM dizisi mükemmel IOPS ve üretilen iş ile bazı DBMS özellikleri tarafından Dengeleme için uygun. Daha fazla bilgi için bkz: Merhaba [DBMS Dağıtım Kılavuzu'na][dbms-guide].

Microsoft Azure depolama kalıcı depolama ve hello tipik düzeyde koruma ve SAN depolama alanı üzerinde görülen artıklık sağlar. Azure depolama birimine dayalı sanal sabit hello Azure depolama hizmetleri içinde bulunan disk (VHD) disklerdir. Merhaba yerel işletim sistemi diski (Windows C:\, Linux/dev/sda1) Azure Storage hello üzerinde depolanır ve ek birimler/takılı toohello VM depolanan vardır, çok diskler.

Bu olası tooupload varolan bir VHD'yi şirket içi veya Azure içinde boş olanlardan oluşturmak ve bu toodeployed VM'lerin ekleyin.

Oluşturma veya bir VHD Azure depolama alanına karşıya yükleme sonra bu olası toomount ve varolan sanal makine ve (takılmamış) VHD varolan toocopy bu tooan ekleyin.

Bu VHD kalıcı olarak veri ve bu değişikliklerin yeniden başlatmadan ve bir sanal makine örneğini yeniden güvenlidir. Örneği silinse bile bu VHD güvende ve dağıtılması veya işletim sistemi olmayan diskleri durumunda takılı tooother VM'ler olabilir.

Merhaba içinde Azure Storage farklı artıklık düzeylerinin ağ yapılandırılabilir:

* Seçilebilen en düşük düzeydir 'hello içindeki hello verilerin eşdeğer toothree çoğaltma olan yerel artıklık', aynı veri merkezinde bir Azure bölgesinin (bölüm bkz [Azure bölgeleri][planning-guide-3.1]).
* Aynı Azure bölgesindeki farklı veri merkezleri içinde üzerinden hangi yayma hello üç görüntüleri hello bölge olarak yedekli depolama.
* Varsayılan artıklık düzeyidir hello barındırılan başka bir Azure bölgesi hello verileri başka bir üç görüntülerini zaman uyumsuz olarak hello içerik yarlar coğrafi artıklık aynı coğrafi bölge.

Ayrıca bu makalede hello farklı artıklık seçenekleri ile ilgili en üstünde hello tablosuna bakın: <https://azure.microsoft.com/pricing/details/storage/>

Azure Storage hakkında daha fazla bilgi şurada bulunabilir:

* <https://Azure.microsoft.com/documentation/Services/Storage/>
* <https://Azure.microsoft.com/Services/Site-Recovery>
* <https://docs.microsoft.com/REST/api/storageservices/Understanding-Block-BLOBS--Append-BLOBS--and-Page-BLOBS>
* <https://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/Azure-disk-Encryption-for-Linux-and-Windows-Virtual-Machines-Public-Preview.aspx>

#### <a name="azure-standard-storage"></a>Standart Azure depolama
Azure Iaas yayımlandığında azure standart depolama hello kullanılabilir depolama türündeydi. Tek disk başına zorlanan IOPS kotaları vardı. Gecikme yaşadı genellikle dağıtılan SAN/NAS cihazları Gelişmiş SAP sistemler için şirket içi barındırılan olarak aynı sınıf hello değildi. Bununla birlikte, Azure Standard Storage oluyor uygulamasına yol açıyordu yüzlerce için yeterli hello bu sırada Azure üzerinde dağıtılan SAP sistemleri.

Azure standart depolama hesaplarında depolanan diskleri depolanan hello gerçek veri depolama işlemleri, giden veri aktarımları ve seçilen artıklığı seçeneği hello birim göre ücretlendirilen. Merhaba en fazla 1 TB boyutu en fazla disk oluşturulabilir, ancak bu boş kaldığı sürece ücretsizdir. Bir VHD 100 GB ile sonra doldurduğunuzda değil, VHD ile oluşturulan hello nominal boyutu hello ve 100 GB depolama için sizden ücret kesilir.

#### <a name="ff5ad0f9-f7f4-4022-9102-af07aef3bc92"></a>Azure Premium depolama
Nisan 2015'te, Microsoft Azure Premium Storage kullanıma sunmuştur. Premium depolama hello hedef tooprovide ile sunulan:

* Daha iyi g/ç gecikmesi.
* Daha iyi verimlilik.
* G/ç gecikmesi daha az sonuçlarındaki.

Bu amaç için hangi hello iki en önemli olan birçok değişikliğin yapılmadığı:

* Hello Azure depolama düğümleri SSD diskleri kullanımı
* Tarafından desteklenen yeni bir okuma önbelleği hello Azure işlem düğümünün yerel SSD

Ters tooStandard depolama burada özellikler değişmemiştir veya hello disk (VHD), hello boyutu bağımlı Premium depolama şu anda bu makalede gösterilen üç farklı disk kategoriler yok: <https://azure.microsoft.com/ Fiyatlandırma/Ayrıntılar/depolama/yönetilmeyen-diskleri />

IOP/disk ve disk işleme/disk hello disklerin hello boyutu kategorisine göre bağımlı bakın

Premium Storage hello durumda maliyet temel tür diskleri, ancak böyle bir diskin hello hello disk içinde depolanan hello veri miktarını bağımsız hello boyutu kategori depolanan hello gerçek veri birimi değil.

Ayrıca, diskleri gösterilen hello boyutu kategoriye doğrudan eşleme değil Premium depolama oluşturabilirsiniz. Özellikle diskleri standart depolama biriminden Premium depolama alanına kopyalama işlemi sırasında bu hello durumda olabilir. Böyle durumlarda, bir eşleme toohello sonraki en büyük Premium depolama diski seçeneği gerçekleştirilir.

Yalnızca belirli VM serisi hello Azure Premium Storage ' yararlanabilir unutmayın. DEC 2015'ten itibaren hello DS - ve GS serisi bunlar. Merhaba DS serisi olduğu temelde hello aynı D-serisi DS serisi hello özelliği toomount Premium depolama olduğunu hello durumla VM'ler tabanlı olarak ayrıca Azure Standard Storage üzerinde barındırılan toodisks. Aynı şey G serisi karşılaştırıldığında tooGS-seri için geçerli değil.

Merhaba DS serisi Vm'lerde hello parçası çıkış denetimi varsa [bu makalede (Linux)] [ virtual-machines-sizes-linux] ve [bu makalede (Windows)][virtual-machines-sizes-windows], sizin fark ettiğinizden veri birimi sınırlamaları tooPremium depolama disklerde hello kesinliği hello VM düzeyi vardır. Ayrıca farklı DS serisi veya GS serisi VM'ler bakımından toohello sayısında bağlanabilir veri disklerinin farklı sınırlamaları vardır. Bu sınırlar da yukarıdaki hello makalesinde belgelenmiştir. Ancak aslında, örneğin, 32 x P30 diskleri tooa bağlamanız halinde tek DS14 VM hello en yüksek verimlilik P30 disk x 32 alabileceğiniz değil, anlamına gelir. Bunun yerine hello makale sınırları veri üretimini belirtildiği gibi VM düzeyinde en yüksek verimlilik hello.

Premium depolama hakkında daha fazla bilgi şurada bulunabilir: <http://azure.microsoft.com/blog/2015/04/16/azure-premium-storage-now-generally-available-2>

#### <a name="c55b2c6e-3ca1-4476-be16-16c81927550f"></a>Yönetilen diskleri
Yeni bir kaynak türü Azure kaynağı Azure depolama hesaplarında depolanan VHD yerine kullanılan Yöneticisi'nde yönetilen disklerdir. Kullanılabilirlik kümesi hello sanal makinenin oldukları tooand bu nedenle sanal makine ve hello sanal makinede çalışan hello Hizmetleri kullanılabilirliğini artırmak hello bağlı hello ile yönetilen diskleri otomatik olarak hizalayın. Daha fazla bilgi için hello okuma [genel bakış makalesi](https://docs.microsoft.com/azure/storage/storage-managed-disks-overview).

Merhaba dağıtım ve sanal makinelerin yönetimini basitleştirmek için tooyou kullanım yönetilen disk öneririz.
SAP şu anda yalnızca Premium yönetilen diskleri destekler. Daha fazla bilgi için SAP not okuma [1928533].

#### <a name="azure-storage-accounts"></a>Azure Depolama Hesapları
Hizmetleri veya azure'da VM dağıtırken dağıtımı VHD'ler VM görüntüleri ve Azure Storage hesapları olarak adlandırılan birimler halinde düzenlenebilir. Bir Azure dağıtımı planlarken toocarefully gereken Azure hello kısıtlamaları göz önünde bulundurun. Merhaba bir yandan, depolama hesapları, sınırlı sayıda Azure abonelik başına yoktur. Her Azure depolama hesabı VHD dosyaları, çok sayıda tutabilir rağmen bir sabit bir sınır yoktur hello üzerinde depolama hesabı başına IOPS toplam sayısı. SAP VM'ler yüzlerce önemli GÇ çağrı oluşturuluyor DBMS sistemleriyle dağıtırken olduğu birden çok Azure depolama hesapları arasında yüksek IOPS DBMS VM'ler toodistribute önerilir. Tooexceed hello geçerli sınırlandırma Azure Storage hesapları, abonelik başına dikkatli olunması gerekir. Depolama hello veritabanı dağıtımı bir SAP sistemi için hayati bir parçası olduğundan, bu kavram zaten başvurulan hello bölümlerinde daha ayrıntılı ele alınmıştır [DBMS Dağıtım Kılavuzu'na][dbms-guide].

Azure Storage hesapları hakkında daha fazla bilgi bulunabilir [bu makalede][storage-scalability-targets]. Bu makaleyi okuduktan, hello sınırlamaları Azure standart depolama hesapları ve Premium depolama hesapları arasındaki farkları olduğunu unutmayın. Temel farklılıkları hello gibi bir depolama hesabında depolanan verilerin hacmi ' dir. Standart depolama hello büyüklük Premium Storage ile büyük birimdir. Merhaba üzerinde hello standart depolama hesabı diğer taraftaki ancak böyle bir kısıtlama Hello Azure Premium depolama hesabı vardır ('Toplam istek oranı' sütununa bakın) IOP cinsinden ciddi bir şekilde sınırlıdır. Ayrıntıları ve bu farklılıklar sonuçlarını SAP sistemleri, özellikle hello DBMS sunucularda hello dağıtımları ele alırken aşağıdakiler ele alınacaktır.

Bir depolama hesabında hello olasılığı toocreate farklı kapsayıcılar hello amacını düzenleme ve farklı VHD'ler kategorilere ayırmak için sahip. Bu kapsayıcılar, örneğin, ayrı VHD'leri farklı VM'ler için genellikle kullanılır. Yalnızca bir kapsayıcı veya tek bir Azure depolama hesabı altında birden çok kapsayıcı kullanarak hiçbir performans etkileri vardır.

Azure içinde hello tooprovide hello Azure içinde VHD için benzersiz bir ad gerekiyor adlandırma bağlantı izleyen bir VHD ad aşağıdaki gibidir:

    http(s)://<storage account name>.blob.core.windows.net/<container name>/<vhd name>

Yukarıda sözü edilen hello dize olarak toouniquely hello Azure depolama alanında depolanan VHD tanımlamak.

### <a name="61678387-8868-435d-9f8c-450b2424f5bd"></a>Microsoft Azure ağ iletişimi
Microsoft Azure istiyoruz tüm senaryoları hello eşlenmesini sağlayan bir ağ altyapısı sağlar SAP yazılımıyla toorealize. Merhaba özellikleri şunlardır:

* Dışında doğrudan Windows Terminal Hizmetleri veya ssh/VNC üzerinden VM'ler toohello hello erişimden
* Erişim tooservices ve hello VM'ler içinde uygulamalar tarafından kullanılan belirli bağlantı noktaları
* İç iletişim ve Azure Vm'leri olarak dağıtılan VM'ler grubu arasındaki ad çözümlemesi
* Bir müşterinin şirket içi ağı arasındaki hello Azure ağı şirket içi bağlantılar
* Azure siteler arasında çapraz Azure bölgesini ya da veri merkezi bağlantısı

Daha fazla bilgi şurada bulunabilir: <https://azure.microsoft.com/documentation/services/virtual-network/>

Birçok farklı olanaklar tooconfigure adı ve IP çözümleme Azure vardır. Bu belgede, Azure DNS (Karşıtlık toodefining içinde kendi bir DNS hizmeti) kullanmanın hello varsayılan yalnızca bulut senaryoları bağlıdır. Ayrıca kendi DNS sunucusunu ayarlama yerine kullanılabilecek yeni bir Azure DNS hizmeti vardır. Daha fazla bilgi bulunabilir [bu makalede] [ virtual-networks-manage-dns-in-vnet] ve [bu sayfayı](https://azure.microsoft.com/services/dns/).

Şirket içi senaryolarda, biz hello olgu üzerinde FQDN'yi bu hello OpenLDAP/AD/DNS genişletilmişse VPN veya özel bağlantı tooAzure şirket içi. Belirli senaryolar aşağıda belirtildiği gibi gerekli toohave Azure üzerinde yüklü bir AD/OpenLDAP çoğaltma olması olabilir.

Ağ iletişimi olduğundan ve ad çözümlemesi bir SAP sistemi için hello veritabanı dağıtım sürecinin hayati bir parçası ise, bu kavram hello bölümlerinde daha ayrıntılı ele alınmıştır [DBMS Dağıtım Kılavuzu'na][dbms-guide].

##### <a name="azure-virtual-networks"></a>Azure Sanal Ağları
Bir Azure sanal ağı oluşturarak Azure DHCP işlevleri tarafından ayrılan hello özel IP adresleri hello adres aralığı tanımlayabilirsiniz. Şirket içi senaryolarda tanımlanan başlangıç IP adresi aralığı hala DHCP kullanarak Azure tarafından ayrılmış. Ancak, etki alanı adı çözümleme (Merhaba VM'ler bir şirket içi etki alanının bir parçası olduğunu varsayarak) şirket içi gerçekleştirilir ve bu nedenle farklı Azure Cloud Services ötesinde adresleri çözebilirsiniz.

Her sanal makinede Azure gereksinimlerini toobe tooa sanal ağ bağlandı.

Daha fazla ayrıntı bulunabilir [bu makalede] [ resource-groups-networking] ve [bu sayfayı](https://azure.microsoft.com/documentation/services/virtual-network/).

[comment]: <> (MShermannd Yapılacaklar bulamadı hello OpenLDAP konu + ARM içeren bir makale;)
[comment]: <> (MSSedusch < https://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL>)

> [!NOTE]
> Varsayılan olarak, bir VM dağıtıldıktan sonra hello sanal ağ yapılandırması değiştirilemiyor. Merhaba TCP/IP ayarları toohello Azure DHCP sunucusu bırakılmalıdır. Varsayılan, dinamik IP ataması davranıştır.
>
>

Hello hello sanal ağ kartının MAC adresi, örneğin yeniden boyutlandırma ve hello Windows sonra değiştirebilir veya Linux konuk işletim sistemi hello yeni ağ kartı seçer ve DHCP, tooassign hello IP ve DNS adreslerini bu durumda otomatik olarak kullanır.

##### <a name="static-ip-assignment"></a>Statik IP ataması
Sabit olası tooassign olduğunu veya bir Azure sanal ağı içinde tooVMs ayrılmış IP adresleri. Bir Azure sanal ağında Hello VM'ler çalıştıran harika olasılığı tooleverage gerekli veya bazı senaryolar için gerekli değilse bu işlevselliği açar. Merhaba IP ataması hello VM, hello VM çalışıp çalışmadığını veya kapatma bağımsız hello varlığını geçerli kalır. Sonuç olarak, tootake ihtiyacınız hello IP adresleri aralığı hello sanal ağ için tanımlarken, sanal makineleri (VM'ler çalıştığından ve durdurulmuş) genel sayısını göz önüne hello. Merhaba VM ve ağ arabirimiyle silinir kadar veya başlangıç IP adresi yeniden XML'deki atanan kadar Hello IP adresi atanmış olarak kalır. Daha fazla bilgi için okuma [bu makalede][virtual-networks-static-private-ip-arm-pportal].

##### <a name="multiple-nics-per-vm"></a>VM başına birden çok NIC
Bir Azure sanal makine için birden çok sanal ağ arabirim kartı (Vnıc) tanımlayabilirsiniz. Merhaba özelliği toohave ile birden çok vNICs tooset nerede, örneğin, istemci trafiğini bir Vnıc yönlendirilir ve arka uç trafiği ikinci Vnıc yönlendirilir ağ trafiği ayrımı yukarı başlatabilirsiniz. Farklı sınırlamaları vardır VM hello türü bağımlı vNICs toohello sayısı tahminini. Tam Ayrıntılar, işlevsellik ve sınırlamaları aşağıdaki makalelerde bulunabilir:

* [Birden çok NIC ile bir Windows VM oluşturma][virtual-networks-multiple-nics-windows]
* [Birden çok NIC ile bir Linux VM oluşturma][virtual-networks-multiple-nics-linux]
* [Birden çok NIC bir şablon kullanarak sanal makineleri dağıtma][virtual-network-deploy-multinic-arm-template]
* [Birden çok NIC PowerShell kullanarak sanal makineleri dağıtma][virtual-network-deploy-multinic-arm-ps]
* [Birden çok NIC hello Azure CLI kullanarak sanal makineleri dağıtma][virtual-network-deploy-multinic-arm-cli]

#### <a name="site-to-site-connectivity"></a>Siteden siteye bağlantı
Şirket içi Azure Vm'leri ve şirket içi saydam ve kalıcı bir VPN bağlantısıyla bağlı olur. Bu, beklenen toobecome hello en yaygın SAP dağıtım modelinde Azure olur. Merhaba işlemsel yordamlara ve Azure SAP durumlarda işlemlerle saydam çalışmalıdır varsayılır. Bu, mümkün tooprint bu sistemler dışında olması yanı sıra SAP aktarım yönetim sistemi (TMS) tootransport dağıtılan şirket içi Azure tooa test sistem içinde bir geliştirme sistemden değişiklikleri hello kullanmak anlamına gelir. Daha fazla belge siteden siteye geçici bulunabilir [bu makalede][vpn-gateway-create-site-to-site-rm-powershell]

##### <a name="vpn-tunnel-device"></a>VPN tüneli aygıtı
Siteden siteye bağlantı (şirket içi veri merkezi tooAzure veri merkezi) toocreate sipariş, tooeither ihtiyacınız almak ve bir VPN cihazı yapılandırma ya da Windows Server ile birlikte bir yazılım bileşeni olarak Yönlendirme ve Uzaktan Erişim hizmeti (, tanıtılan RRAS) kullanın 2012.

* [PowerShell kullanarak siteden siteye VPN bağlantısı olan bir sanal ağ oluşturma][vpn-gateway-create-site-to-site-rm-powershell]
* [Siteden siteye VPN Gateway bağlantıları için VPN cihazları hakkında][vpn-gateway-about-vpn-devices]
* [VPN ağ geçidi SSS][vpn-gateway-vpn-faq]

![Şirket içi ve Azure arasında siteden siteye bağlantı][planning-guide-figure-600]

Yukarıdaki şekilde Hello iki Azure abonelikleri Azure sanal ağlarda IP adresi alt aralıklara kullanımı için ayrılmış olan gösterir. Merhaba Hello bağlantısını ağ tooAzure VPN kurulan şirket içi.

#### <a name="point-to-site-vpn"></a>Noktadan siteye VPN
Noktadan siteye VPN her istemci makine tooconnect kendi VPN ile Azure'da gerektirir. Konumundaki arıyoruz hello SAP senaryoları için noktadan siteye bağlantı pratik değil. Bu nedenle, daha ayrıntılı başvuru toopoint siteden siteye VPN bağlantısı verilir.

Daha fazla bilgi şurada bulunabilir
* [Bir noktadan siteye bağlantı tooa VNet yapılandırma hello Azure portalını kullanma](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)
* [Bir noktadan siteye bağlantı tooa VNet yapılandırma PowerShell'i kullanma](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps)

#### <a name="multi-site-vpn"></a>Çok siteli VPN
Azure ayrıca günümüzde hello olasılığı toocreate çok siteli VPN bağlantısı için bir Azure aboneliği sunar. Daha önce tek bir abonelik sınırlı tooone siteden siteye VPN bağlantısı oluştu. Bu sınırlama tek bir abonelik için çok siteli VPN bağlantılarıyla yerine geçti. Bu şirketler arası yapılandırmalar aracılığıyla belirli bir abonelik için bir Azure Bölgesi'birden fazla olası tooleverage kolaylaştırır.

Daha fazla belge için lütfen bkz [bu makalede][vpn-gateway-create-site-to-site-rm-powershell]

[comment]: <> (ARM belge bağlantı MShermannd Yapılacaklar bulundu)

#### <a name="vnet-toovnet-connection"></a>VNet tooVNet bağlantı
Çok siteli VPN kullanarak, tooconfigure her hello bölgelerinin ayrı bir Azure sanal ağ gerekir. Ancak çok sık hello farklı bölgelerdeki hello yazılım bileşenleri birbirleriyle iletişim hello gereksinimi vardır. İdeal olarak bu iletişimi bir Azure bölgesi tooon içi ve orada toohello yönlendirileceğini olmayan diğer Azure bölgesi. tooshortcut, Azure hello olasılığı tooconfigure bir Azure sanal ağında Azure sanal ağı başka bir bölgede bulunan bir bölge tooanother öğesinden bir bağlantı sunar. Bu işlev, VNet-VNet bağlantı olarak adlandırılır. Bu işlevsellik hakkında daha fazla bilgi şurada bulunabilir: <https://azure.microsoft.com/documentation/articles/vpn-gateway-vnet-vnet-rm-ps/>.

#### <a name="private-connection-tooazure--expressroute"></a>Özel bağlantı tooAzure – ExpressRoute
Microsoft Azure ExpressRoute birlikte bulundurma ortamında veya Azure veri merkezleri ve her iki hello müşterinin şirket içi altyapı arasında özel bağlantılar hello oluşturulmasına izin verir. ExpressRoute çeşitli MPLS tarafından sunulan (paket anahtarlamalı) VPN sağlayıcılar veya diğer ağ hizmeti sağlayıcıları. ExpressRoute bağlantıları hello Git değil genel Internet. ExpressRoute bağlantıları hello Internet daha yüksek güvenlik, daha fazla güvenilirlik birden çok paralel devreler, yüksek hız ve genel bağlantılara daha düşük gecikme sunar.

Azure ExpressRoute ve burada teklifleri hakkında daha fazla ayrıntı bulabilirsiniz:

* <https://Azure.microsoft.com/documentation/Services/expressroute/>
* <https://Azure.microsoft.com/pricing/details/expressroute/>
* <https://Azure.microsoft.com/documentation/articles/expressroute-faqs/>

Burada açıklandığı gibi bir expressroute bağlantı hattı üzerinden birden çok Azure aboneliği hızlı rota sağlar

* <https://Azure.microsoft.com/documentation/articles/expressroute-howto-linkvnet-ARM/>
* <https://Azure.microsoft.com/documentation/articles/expressroute-howto-circuit-ARM/>

#### <a name="forced-tunneling-in-case-of-cross-premises"></a>Zorlanan tünel şirket içi durumunda
Siteden siteye, noktadan siteye veya ExpressRoute aracılığıyla şirket içi etki alanlarına katılma VM'ler için toomake hello Internet proxy ayarları tüm hello kullanıcılar da bu VM'ler için dağıtıldığını emin gerekir. Varsayılan olarak, bu sanal makineleri veya Internet hello şirket proxy üzerinden geçecek değil, ancak doğrudan Azure toohello bağlanması bir tarayıcı tooaccess hello kullanarak kullanıcıların çalışan yazılım Internet. Ancak, yazılım ve hizmetlerinin toocheck sorumluluk hello proxy olduğundan bile hello proxy ayarı % 100 çözüm toodirect hello trafik hello şirket proxy'si aracılığıyla değil. Merhaba VM çalıştıran yazılım yapmamanın, ya da bir yönetici hello ayarlarını yönetir, trafik toohello Internet yeniden detoured doğrudan Azure toohello Internet üzerinden.

Tooavoid Bu sipariş, şirket içi ve Azure arasında siteden siteye bağlantı zorlamalı tüneli yapılandırabilirsiniz. Merhaba hello zorlamalı tüneli özelliğinin ayrıntılı açıklaması burada yayımlanan <https://azure.microsoft.com/documentation/articles/vpn-gateway-forced-tunneling-rm/>

ExpressRoute ile zorlamalı tünel hello ExpressRoute BGP yoluyla varsayılan yolun tanıtılması müşteriler tarafından etkinleştirilmişse eşliği oturumlarını.

#### <a name="summary-of-azure-networking"></a>Azure ağı özeti
Bu bölümde Azure ağ ilgili birçok önemli noktalar yer. Merhaba ana noktaları bir özeti aşağıda verilmiştir:

* Azure sanal ağlar tooyour kendi gereksinimlerine göre hello ağ tooset sağlar
* Azure sanal ağları çevrelerini tooassign IP adresi aralıkları tooVMs olması veya sabit IP adresleri tooVMs atayın
* tooset bir siteden siteye ve noktadan siteye bağlantı toocreate bir Azure sanal ağı önce gerekir
* Bir sanal makine dağıtıldıktan sonra toohello VM sanal ağ atanan olası toochange hello artık değildir

### <a name="quotas-in-azure-virtual-machine-services"></a>Azure sanal makine Hizmetleri kotaları
Biz toobe hello olgu hakkında hello depolama birimini temizlemek ve ağ altyapısı hello Azure altyapı hizmetleri, çeşitli çalışan sanal makineler arasında paylaşılır. Ve yalnızca hello müşterinin kendi veri merkezlerini olduğu gibi bazı hello altyapı kaynakların aşırı sağlama yer tooa derece gerçekleştirin. disk, CPU, ağ ve diğer kotaları toolimit hello kaynak tüketimini ve toopreserve tutarlı ve belirleyici performans Hello Microsoft Azure platformu kullanır.  Merhaba farklı VM türler (A5, A6, vb.) farklı kotalar diskler, CPU, RAM, hello sayısı için sahip ve ağ.

> [!NOTE]
> SAP tarafından desteklenen hello VM türleri CPU ve bellek kaynakları hello ana bilgisayar düğümlerinde önceden ayrılmış. Bu, hello VM dağıtıldığında, hello kaynakların hello konaktaki hello VM türü tarafından tanımlandığı şekilde kullanılabilir olmasını anlamına gelir.
>
>

Ne zaman kotaları her sanal makine boyutu için planlama ve SAP Azure çözümlerini boyutlandırma hello dikkate alınmalıdır. Merhaba VM kotaları açıklanmıştır [burada (Linux)] [ virtual-machines-sizes-linux] ve [burada (Windows)][virtual-machines-sizes-windows].

açıklanan hello kota hello teorik en yüksek değerleri temsil eder.  disk başına IOPS Hello sınırı küçük IOs (8 kb) ile elde edilen ancak büyük IOs (1 Mb) büyük olasılıkla elde değil.  Merhaba IOPS sınırı tek disk hello ayrıntı düzeyi zorlanır.

Bir kaba karar ağacı toodecide Azure sanal makine hizmetlerini ve özelliklerini bir SAP sistemi uygun olup olmadığını veya mevcut bir sistemi sipariş toodeploy hello Azure, sistemde farklı şekilde yapılandırılmış toobe gerekip gerekmediğini hello karar ağacı aşağıdaki kullanılabilir:

![Karar ağacı toodecide özelliği toodeploy Azure üzerinde SAP][planning-guide-figure-700]

**1. adım**: hello en önemli bilgileri toostart ile olan belirli bir SAP sistem hello SAP gereksinimi. Merhaba SAP gereksinimleri gerek toobe Hello SAP Sistem zaten olsa bile hello DBMS ve hello SAP uygulama bölümlerini, ayrılmış şirket içi bir katman 2 yapılandırmasında dağıtıldı. Varolan sistemler için SAP toohello donanımı genellikle belirlenen veya tahmini ilgili hello üzerinde mevcut SAP kıyaslamaları temel. Merhaba sonuçları şurada bulunabilir: <http://global.sap.com/campaigns/benchmark/index.epx>.
Yeni dağıtılan SAP sistemleri hello SAP hello sistem gereksinimleriyle belirlemelisiniz boyutlandırma alıştırma çalıştınız.
Azure üzerinde bu blog ve ekli belgeyi SAP boyutlandırma için Ayrıca bkz: <http://blogs.msdn.com/b/saponsqlserver/archive/2015/12/01/new-white-paper-on-sizing-sap-solutions-on-azure-public-cloud.aspx>

**2. adım**: varolan sistemler için g/ç birim hello ve saniyede g/ç işlemleri hello DBMS sunucuda ölçülebilir. Yeni planlı sistemler için alıştırma hello yeni sistem için de boyutlandırma hello kaba fikir edinmek hello g/ç gereksinimlerinin hello DBMS yan vermesi gerekir. Emin değilseniz, sonunda tooconduct bir kavram kanıtı gerekir.

**3. adım**: karşılaştırma hello SAP gereksinimi hello hello SAP hello farklı VM türler Azure DBMS sunucusuyla sağlayabilir. SAP Hello bilgi hello farklı Azure VM türlerinde SAP notta belgelenen [1928533]. Merhaba veritabanı katmanı dağıtımların hello çoğunluğu ölçeğini olmayan bir SAP NetWeaver sistemi hello katman olduğundan hello odak hello DBMS VM üzerinde ilk olmalıdır. Buna karşılık, hello SAP uygulama katmanı dışa genişletilebilir. Merhaba SAP hiçbiri destekleniyorsa Azure VM türleri gerekli hello SAP dağıtabilir, planlanan hello SAP sisteminin hello iş yükü Azure üzerinde çalıştırılamaz. Hello sistemi için toochange hello iş yükü birime gereksinim veya toodeploy hello sistem şirket içi ya da gerekir.

**Adım 4**: belirtildiği gibi [burada (Linux)] [ virtual-machines-sizes-linux] ve [burada (Windows)][virtual-machines-sizes-windows], Azure disk başına IOPS kota zorlar Standart depolama veya Premium depolama kullanıp bağımsız. Merhaba VM türü bağımlı, takılabilir veri diski hello sayısı değişir. Sonuç olarak, her hello farklı VM türler elde edilebilir maksimum IOPS birkaç hesaplayabilirsiniz. Merhaba veritabanı dosya düzeni bağımlı, diskleri toobecome hello konuk işletim sistemi içinde tek bir birim şeritler. Ancak, dağıtılan bir SAP sisteminin geçerli IOPS birimi Hello hello en büyük VM türüne Azure ve hiçbir fırsat toocompensate daha fazla belleğe sahip olup olmadığını hesaplanan hello sınırları aşarsa, hello SAP sistem hello iş yükünü ciddi bir şekilde etkilenebilir. Böyle durumlarda, burada Azure hello sistemde dağıtmamanız noktası isabet.

**5. adım**: SAP sistemleri, özellikle de, şirket içi 2 katmanlı yapılandırmalarında dağıtılırsa, hello olasılığı olan hello sistem Azure üzerinde 3 katmanlı yapılandırmada yapılandırılan toobe gerekebilir. Bu adımda, ölçeği genişletilemez ve hangi hello CPU ve bellek kaynakları farklı Azure VM türleri teklif hello uyar değil hello SAP uygulama katmanında bir bileşen olup toocheck gerekir. Gerçekten varsa bu tür bir bileşeni, Azure'da hello SAP sistem ve iş yükünü dağıtılamıyor. Ancak birden fazla Azure VM'yi hello SAP uygulama bileşenlerini ölçeklendirebilirsiniz, Azure'da hello sistem dağıtılabilir.

**Adım 6**: hello DBMS ve SAP uygulama katmanı bileşenleri Azure Vm'lerde çalıştırılabilir, hello yapılandırma ile regard için tanımlanan toobe gerekir:

* Azure VM sayısı
* Merhaba ayrı bileşenler için VM türler
* DBMS VM tooprovide VHD'ler sayısında yeterli IOPS

## <a name="managing-azure-assets"></a>Azure varlıklarını yönetme
### <a name="azure-portal"></a>Azure Portal
Hello Azure portal üç arabirimleri toomanage Azure VM dağıtımlarının biridir. görüntülerden sanal makineleri dağıtma gibi hello temel yönetim görevleri hello Azure portal yapılabilir. Ayrıca, depolama hesapları, sanal ağlar, oluşturulmasını hello ve diğer Azure ayrıca görevleri hello Azure portal çok iyi işleyebilir bileşenlerdir. Ancak, şirket içi tooAzure VHD'ler yükleyerek veya azure'daki bir VHD kopyalama gibi işlevselliği, üçüncü taraf araçları veya PowerShell veya CLI üzerinden Yönetimi gerektiren görevleri değildir.

![Microsoft Azure portal - sanal makineye genel bakış][planning-guide-figure-800]

[comment]: <> (MSSedusch * < https://azure.microsoft.com/documentation/articles/virtual-networks-create-vnet-arm-pportal/>)
[comment]: <> (MSSedusch * < https://azure.microsoft.com/documentation/articles/virtual-machines-windows-tutorial/>)

Yönetim ve yapılandırma görevlerini hello sanal makine örneği için Azure portal hello içinde mümkündür.

Yeniden başlatma ve bir sanal makineyi kapatmak makinenin yanı sıra da ekleme, detach ve veri diskleri hello sanal makine örneği, toocapture hello örneği görüntü hazırlık için oluşturabilir ve hello sanal makine örneğinin hello boyutunu yapılandırın.

Hello Azure portal temel işlevleri toodeploy sağlar ve VM'ler ve diğer Azure hizmetleriyle birçok yapılandırın. Ancak tüm kullanılamaz işlevselliği hello Azure portal tarafından ele alınmıştır. Hello Azure portalı, bu olası tooperform görevler gibi değil:

* VHD'ler tooAzure karşıya yükleme
* Sanal makineleri kopyalama

[comment]: <> (MShermannd Yapılacaklar Otomasyon hakkında neler SAP VM'ler için hizmet?)
[comment]: <> (Bu sırada olası birden çok VM os MSSedusch dağıtımı)
[comment]: <> (Ayrıca MSSedusch Otomasyon dağıtım ile ilgili herhangi bir türde hello Azure portal ile mümkün değil. Birden çok VM komut dosyalı dağıtımı gibi görevleri hello Azure portal mümkün değildir.)

### <a name="management-via-microsoft-azure-powershell-cmdlets"></a>Microsoft Azure PowerShell cmdlet'leri aracılığıyla Yönetimi
Windows PowerShell yaygın sayıda Azure sistemlerinde dağıtma müşteriler tarafından benimsenen güçlü ve Genişletilebilir bir çerçevedir. PowerShell cmdlet'leri Masaüstü, dizüstü bilgisayar veya özel yönetim istasyon Hello yüklendikten sonra PowerShell cmdlet'leri hello uzaktan çalıştırılabilir.

işlem tooenable hello kullanımı Azure PowerShell cmdlet'leri için yerel Masaüstü/dizüstü hello ve ile kullanım için olanlar hello tooconfigure hello nasıl Azure aboneliklerinden açıklanan [bu makalede][powershell-install-configure].

Ayrıntılı adımlar nasıl tooinstall, güncelleştirme ve hello Azure PowerShell cmdlet'lerini yapılandırmak da bulunabilir [bu hello Dağıtım Kılavuzu'nun][deployment-guide-4.1].

Müşteri Deneyimi kadarki PowerShell (PS) kesinlikle hello VM'ler dağıtımında toocreate özel adımlar ve daha güçlü aracı toodeploy VM'ler hello olduğunu olmuştur. Tüm SAP örnekleri Azure'da çalışan hello müşteriler hello Azure portal yapın veya hatta PS cmdlet'lerini kullanarak PS cmdlet'leri toosupplement yönetim görevlerini kullanarak özel olarak toomanage Azure dağıtımları. Hello Azure özgü cmdlet'leri paylaşımı hello olduğundan aynı 2000'den fazla Windows ile ilgili cmdlet'leri hello adlandırma kolay bir görev için Windows yöneticileri tooleverage bu cmdlet'leri kalır.

Örnek buraya bakın: <http://blogs.technet.com/b/keithmayer/archive/2015/07/07/18-steps-for-end-to-end-iaas-provisioning-in-the-cloud-with-azure-resource-manager-arm-powershell-and-desired-state-configuration-dsc.aspx>

[comment]: <> (MShermannd Yapılacaklar açıklamak sınandığında yeni CLI komutu)
Hello Azure Monitoring uzantısı SAP için dağıtım (bölüm bkz [Azure izlemesi çözümünü SAP] [ planning-guide-9.1] bu belgedeki) PowerShell veya CLI aracılığıyla yalnızca mümkündür. Bu nedenle zorunlu tooset çalışıyor ve PowerShell veya CLI dağıtırken veya Azure SAP NetWeaver sistemde yönetme yapılandırın.  

Azure daha fazla işlevsellik sağlayan gibi hello cmdlet'lerinin bir güncelleştirme gerektiren toobe eklenen yeni PS cmdlet'leri adımıdır. Bu nedenle algılama toocheck hello Azure karşıdan site en az hello ayda kolaylaştırır <https://azure.microsoft.com/downloads/> hello cmdlet yeni bir sürümü için. Merhaba sürümün üstünde Hello yeni sürümü yüklü.

PowerShell Azure ile ilgili genel bir listesi için komutları burada denetleyin: <https://docs.microsoft.com/powershell/azure/overview>.

### <a name="management-via-microsoft-azure-cli-commands"></a>Microsoft Azure CLI komutları aracılığıyla Yönetimi
Linux kullanan ve toomanage Azure istediğiniz müşteriler için bir seçenek kaynakları Powershell olmayabilir. Microsoft Azure CLI alternatif olarak sunar.
Hello Azure CLI açık kaynak, bir dizi hello Azure platformu ile çalışmak için platformlar arası komutları sağlar. Hello Azure CLI aynı işlevselliği hello Azure portalında bulunan hello çoğunu sağlar.

Yükleme, yapılandırma ve nasıl tooaccomplish toouse CLI komutları hakkında bilgi için Azure görevleri bakın.

* [Hello Azure CLI yükleme][xplat-cli]
* [Dağıtmak ve Azure Resource Manager şablonları ve hello Azure CLI kullanarak sanal makineleri yönetme] [.. /.. / linux/create-ssh-secured-vm-from-template.md]
* [Mac, Linux ve Windows Azure Resource Manager ile için Hello Azure CLI kullanma][xplat-cli-azure-resource-manager]

Ayrıca bölümünü okuyun [Linux VM'ler için Azure CLI] [ deployment-guide-4.5.2] hello içinde [Dağıtım Kılavuzu] [ planning-guide] toouse Azure CLI toodeploy nasıl hello Azure izleme hakkında SAP için uzantısı.

## <a name="different-ways-toodeploy-vms-for-sap-in-azure"></a>Farklı şekillerde toodeploy VM'ler için azure'da SAP
Bu bölümde, hello farklı şekillerde toodeploy azure'da VM öğrenin. VHD ve VM'ler için Azure'da işlenmesini yanı sıra ek hazırlık yordamlar bu bölümde ele alınmıştır.

### <a name="deployment-of-vms-for-sap"></a>VM dağıtımı için SAP
Microsoft Azure diskleri ilişkili ve toodeploy VM'ler birden çok yol sunar. Bu nedenle hello VM'ler hazırlıklar dağıtım hello yöntemine bağlı olarak değişebilir olduğundan çok önemli toounderstand hello farklar kalır. Genel olarak, biz hello aşağıdaki senaryoları göz atın:

#### <a name="4d175f1b-7353-4137-9d2f-817683c26e53"></a>VM genelleştirilmiş olmayan bir disk ile şirket içi tooAzure taşıma
Şirket içi tooAzure belirli bir SAP sistemden toomove planlayın. Bu hello hello işletim sistemi içeren VHD yükleyerek yapılabilir, SAP ikili dosyaları ve DBMS ikili dosyaları hello artı VHD'ler hello veri ve günlük dosyaları hello DBMS tooAzure ile Merhaba. Buna karşılık çok[Senaryo #2 aşağıdaki][planning-guide-5.1.2]hello ana bilgisayar adı, SAP SID tutmak ve SAP kullanıcı hesapları hello Azure VM hello şirket içi ortamda yapılandırılmış gibi. Bu nedenle, hello görüntü genelleme gerekli değildir. Bölümlere bakın [VM genelleştirilmiş olmayan bir disk ile şirket içi tooAzure geçiş hazırlığı] [ planning-guide-5.2.1] şirket içi hazırlık adımları ve genelleştirilmiş VMs veya VHD'ler tooAzure karşıya yükleme için bu belgenin. Okuma bölüm [Senaryo 3: şirket içi SAP ile genelleştirilmiş Azure VHD kullanarak bir VM taşınan] [ deployment-guide-3.4] hello içinde [Dağıtım Kılavuzu'na] [ deployment-guide] Bu tür bir görüntü azure'da dağıtmanın ayrıntılı adımlar için.

#### <a name="e18f7839-c0e2-4385-b1e6-4538453a285c"></a>Bir müşteriye özgü görüntüsü olan bir VM dağıtma
Toospecific düzeltme eki gereksinimleri, işletim sistemi veya DBMS sürümü hello Azure Marketi sağlanan hello görüntülerinde gereksinimlerinize değil. Bu nedenle, daha sonra birkaç kez dağıtılabilir kendi 'özel' işletim sistemi/DBMS VM görüntüsü kullanarak bir VM'i toocreate gerekebilir. tooprepare çoğaltmak için 'özel' görüntüsü, aşağıdaki öğelerindeki hello kabul toobe vardır:

- - -
> ![Windows][Logo_Windows] Windows
>
> Burada Ayrıntılar için bkz: <https://docs.microsoft.com/azure/virtual-machines/windows/upload-generalized-managed> hello Windows ayarları (örneğin, Windows SID ve ana bilgisayar adı) soyutlanır/genelleştirilmiş hello şirket içi üzerinde olmalıdır VM hello sysprep komutu ile.
>
>
> ![Linux][Logo_Linux] Linux
>
> Bu makaleler için açıklanan başlangıç adımları [SUSE][virtual-machines-linux-create-upload-vhd-suse], [Red Hat][virtual-machines-linux-redhat-create-upload-vhd], veya [Oracle Linux] [ virtual-machines-linux-create-upload-vhd-oracle], tooprepare VHD toobe karşıya tooAzure.
>
>

- - -
(Özellikle 2 katmanlı sistemler için), şirket içi VM'deki SAP içerik zaten yüklediyseniz, hello Azure VM hello örneği aracılığıyla hello dağıtımını yeniden adlandırdıktan sonra hello tarafından SAP yazılım sağlama desteklenen yordamı hello SAP sistem ayarlarını uyarlayabilirsiniz Yöneticisi (SAP Not [1619720]). Bölümlere bakın [için SAP müşteriye özgü görüntüsü olan bir VM dağıtımı için hazırlık] [ planning-guide-5.2.2] ve [şirket içi tooAzure VHD'den karşıya] [ planning-guide-5.3.2]şirket içi hazırlık adımları ve genelleştirilmiş bir VM tooAzure karşıya yükleme için bu belgenin. Okuma bölüm [Senaryo 2: özel bir görüntü ile bir VM için SAP dağıtma] [ deployment-guide-3.3] hello içinde [Dağıtım Kılavuzu'na] [ deployment-guide] dağıtma ayrıntılı adımlar için Bu tür bir görüntüde Azure.

#### <a name="deploying-a-vm-out-of-hello-azure-marketplace"></a>Hello Azure Market dışında bir VM dağıtma
Bir Microsoft veya üçüncü taraf toouse hello Azure Marketi toodeploy VM görüntüsünü VM sağlanan istediğinizi. Azure VM dağıtımı sonra hello izleyin aynı kılavuzları ve Araçlar tooinstall hello SAP yazılım ve/veya DBMS VM içinde bir şirket içi ortamda yaptığınız gibi. Bölüm daha ayrıntılı dağıtımı açıklaması için lütfen bkz [Senaryo 1: hello SAP için Azure Market dışında bir VM dağıtma] [ deployment-guide-3.2] hello içinde [Dağıtım Kılavuzu'na] [ deployment-guide].

### <a name="6ffb9f41-a292-40bf-9e70-8204448559e7"></a>Azure için sanal makineleri SAP ile hazırlama
Azure'da Vm'leri karşıya yüklemeden önce toomake emin hello sanal makineleri ve VHD belirli gereksinimleri karşılamanız gerekir. Kullanılan hello dağıtım yöntemine bağlı olarak küçük farklılıklar vardır.

#### <a name="1b287330-944b-495d-9ea7-94b83aff73ef"></a>VM genelleştirilmiş olmayan bir disk ile şirket içi tooAzure geçiş için hazırlama
Bir ortak dağıtım toomove şirket içi tooAzure bir SAP sistemi çalıştıran mevcut bir VM'yi yöntemidir. VM ve hello hello VM yalnızca çalışmalı Azure kullanarak SAP sisteminde hello aynı ana bilgisayar adı ve büyük olasılıkla aynı hello SAP SID'si. Bu durumda hello konuk işletim sistemi, VM için birden çok dağıtım genelleştirilmiş değil. Azure'da Hello şirket içi ağ Genişletilmiş (bölüm bkz [şirket içi - tek dağıtımını ya da Azure hello şirket içi ağınıza tam olarak tümleştirilmiş hello zorunluluğu ile içine birden çok SAP VM] [ planning-guide-2.2] bu belgedeki), sonra bile hello aynı etki alanı hesapları bu şirket içi önce kullanılan olarak VM hello içinde kullanılabilir.

Kendi Azure VM Disk hazırlanırken gereksinimleri şunlardır:

* Başlangıçta hello VHD içeren hello işletim sistemi yalnızca en büyük boyutu 127 GB olabilir. Bu sınırlama hello Mart 2015 sonunda ortadan. Başka bir Azure depolama VHD de barındırılan olarak artık hello hello işletim sistemini içeren VHD boyutu too1TB yukarı olabilir.
* VHD biçiminde sabit hello toobe gerekir. Dinamik VHD veya VHDx biçiminde VHD'ler henüz Azure üzerinde desteklenmez. Dinamik VHD hello VHD PowerShell cmdlet'leri veya CLI ile karşıya yüklediğinizde dönüştürülmüş toostatic VHD'ler olacaktır
* Takılı toohello VM olan ve Azure toohello VM gerek toobe de sabit bir VHD biçiminde, yeniden takılmasını VHD'ler. Lütfen okuyun [bu makalede (Linux)](https://docs.microsoft.com/azure/storage/storage-about-disks-and-vhds-linux) ve [bu makalede (Windows)](https://docs.microsoft.com/azure/storage/storage-about-disks-and-vhds-windows) veri diski boyutu sınırları için. Dinamik VHD hello VHD PowerShell cmdlet'leri veya CLI ile karşıya yüklediğinizde dönüştürülmüş toostatic VHD'ler olacaktır
* Microsoft destek ya da, hizmetler ve uygulamalar toorun bağlamının olarak VM dağıtılan hello kadar atanabilir ve daha uygun kullanıcılar tarafından kullanılan yönetici ayrıcalıklarına sahip başka bir yerel hesap kullanılabilir ekleyin.
* Bir yalnızca bulut dağıtım senaryosu kullanmanın hello çalışması için (bölüm bkz [salt bulut - Azure sanal makine dağıtımlarınızı hello bağımlılıkları olmadan şirket içi müşteri ağ] [ planning-guide-2.1] bu Bu dağıtım yöntemi, Azure'da hello Azure diski dağıtıldığında hesapları çalışmayabilir etki alanı ile birlikte belge). Bu, özellikle kullanılan toorun Hizmetleri hello DBMS veya SAP uygulamaları gibi olan hesapları için geçerlidir. Bu nedenle bu tür etki alanı hesaplarıyla VM yerel tooreplace gerekir ve hello VM hello şirket içi etki alanı hesapları silin. Şirket içi etki alanı kullanıcıları hello VM görüntüsünde tutma değil bir sorun VM hello dağıtılan hello senaryo bölümde açıklandığı gibi şirketler arası olduğunda [şirket içi - tek dağıtımını ya da Azure olma hello gereksinimiyle içine birden çok SAP VM Merhaba şirket içi ağınıza tam olarak tümleşiktir] [ planning-guide-2.2] bu belgedeki.
* Etki alanı hesapları DBMS oturumu açma kullanılan veya hello sistem şirket içi ve bu VM'lerin çalışırken kullanıcılar yalnızca bulut senaryolarda dağıtılan toobe beklenen hello etki alanı kullanıcıları silinmiş toobe gerekir. Merhaba yerel yönetici artı başka bir VM yerel kullanıcı eklendiğini bir oturum açma/kullanıcı olarak hello yöneticileri olarak DBMS içine emin toomake gerekir.
* Bu hello belirli dağıtım senaryosu için gerekebilecek gibi diğer yerel hesaplar ekleyin.

- - -
> ![Windows][Logo_Windows] Windows
>
> Bu senaryoda hello VM hiçbir genelleme (sysprep) gerekli tooupload olan ve hello Azure VM dağıtabilirsiniz.
> D:\ kullanılmıyorsa bu sürücüye emin olun.
> Bölümde açıklandığı gibi bağlı diskler için disk otomatik bağlama ayarlamak [bağlı diskler için otomatik bağlama ayarı] [ planning-guide-5.5.3] bu belgedeki.
>
> ![Linux][Logo_Linux] Linux
>
> Bu senaryoda hiçbir Genelleştirme (waagent-deprovision) hello VM gerekli tooupload olan ve hello Azure VM dağıtın.
> / Mnt/kaynak kullanılmaz ve tüm diskleri UUID bağlandığından emin olun. Hello işletim sistemi diski için hello önyükleme yükleyicisi giriş de hello UUID tabanlı bağlama gösterdiğinden emin olmalısınız.
>
>

- - -
#### <a name="57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3"></a>SAP için müşteriye özgü görüntüsü olan bir VM dağıtımı için hazırlama
Genelleştirilmiş bir işletim sistemi içeren VHD dosyaları kapsayıcıları Azure depolama hesapları veya yönetilen Disk görüntü olarak depolanır. Merhaba VHD veya yönetilen Disk görüntü kaynağı dağıtım şablonu dosyalarınızı olarak bölümde açıklandığı gibi başvurarak bu tür bir görüntüden yeni bir VM dağıtabilirsiniz [Senaryo 2: özel bir görüntü ile bir VM için SAP dağıtma] [ deployment-guide-3.3]Merhaba, [Dağıtım Kılavuzu'na][deployment-guide].

Kendi Azure VM görüntüsü hazırlanırken gereksinimleri şunlardır:

* Başlangıçta hello VHD içeren hello işletim sistemi yalnızca en büyük boyutu 127 GB olabilir. Bu sınırlama hello Mart 2015 sonunda ortadan. Başka bir Azure depolama VHD de barındırılan olarak artık hello hello işletim sistemini içeren VHD boyutu too1TB yukarı olabilir.
* VHD biçiminde sabit hello toobe gerekir. Dinamik VHD veya VHDx biçiminde VHD'ler henüz Azure üzerinde desteklenmez. Dinamik VHD hello VHD PowerShell cmdlet'leri veya CLI ile karşıya yüklediğinizde dönüştürülmüş toostatic VHD'ler olacaktır
* Takılı toohello VM olan ve Azure toohello VM gerek toobe de sabit bir VHD biçiminde, yeniden takılmasını VHD'ler. Lütfen okuyun [bu makalede (Linux)](https://docs.microsoft.com/azure/storage/storage-about-disks-and-vhds-linux) ve [bu makalede (Windows)](https://docs.microsoft.com/azure/storage/storage-about-disks-and-vhds-windows) veri diski boyutu sınırları için. Dinamik VHD hello VHD PowerShell cmdlet'leri veya CLI ile karşıya yüklediğinizde dönüştürülmüş toostatic VHD'ler olacaktır
* Tüm etki alanı kullanıcıları hello VM kullanıcılar bir yalnızca bulut senaryosunda yok olarak kaydedilen hello bu yana (bölüm bkz [salt bulut - Azure sanal makine dağıtımlarınızı hello bağımlılıkları olmadan şirket içi müşteri ağ] [ planning-guide-2.1] bu belgenin), böyle bir etki alanı hesapları hello görüntüsünü Azure'da dağıtıldığında çalışmayabilir kullanarak hizmetleri. Bu, özellikle DBMS veya SAP uygulamaları gibi kullanılan toorun hizmetlerini olan hesapları için geçerlidir. Bu nedenle bu tür etki alanı hesaplarıyla VM yerel tooreplace gerekir ve hello VM hello şirket içi etki alanı hesapları silin. Şirket içi etki alanı kullanıcıları hello VM görüntüsünde tutma olabilir bir sorun VM hello dağıtılan hello senaryo bölümde açıklandığı gibi şirketler arası olduğunda [şirket içi - tek dağıtımını ya da Azure hello gereksinimi ile içine birden çok SAP VM Merhaba şirket içi ağınıza tam olarak tümleştirilmiş] [ planning-guide-2.2] bu belgedeki.
* Microsoft destek sorun araştırmalar ya da, hizmetler ve uygulamalar toorun bağlamının olarak VM dağıtılan hello kadar atanabilir ve daha uygun kullanıcılar tarafından kullanılan yönetici ayrıcalıklarına sahip başka bir yerel hesap kullanılabilir ekleyin.
* Yalnızca bulut dağıtımları ve burada etki alanı hesapları DBMS oturumu açma kullanılan veya sistem şirket içi çalıştırırken kullanıcılar Merhaba, hello etki alanı kullanıcıları silinmesi gerekir. Merhaba yerel yönetici artı başka bir VM yerel kullanıcı eklendiğini hello DBMS yöneticileri olarak bir oturum açma/kullanıcı olarak emin toomake gerekir.
* Bu hello belirli dağıtım senaryosu için gerekebilecek gibi diğer yerel hesaplar ekleyin.
* SAP NetWeaver yüklemesini Hello görüntüsünü içeren ve hello özgün adı hello Azure dağıtım hello noktada hello ana bilgisayar adından adlandırılmasını olasıdır, önerilen toocopy hello en son sürümlerini hello SAP yazılım sağlama Yöneticisi DVD'sini olur Merhaba şablonu. Yeni bir kopyasını kullanmaya hemen yeniden adlandırma işlevselliği tooadapt değiştirilen hello ana bilgisayar adı ve/veya değişiklik hello hello SAP sistemi hello içinde SID'si VM görüntüsü dağıtılan sağlanan bu tooeasily kullanım hello SAP olanak sağlar.

- - -
> ![Windows][Logo_Windows] Windows
>
> Sürücü D:\ değil bölümde açıklandığı gibi disklerdeki kümesi disk otomatik bağlama kullanıldığından emin olun [bağlı diskler için otomatik bağlama ayarı] [ planning-guide-5.5.3] bu belgedeki.
>
> ![Linux][Logo_Linux] Linux
>
> / Mnt/kaynak kullanılmaz ve tüm diskleri UUID bağlandığından emin olun. Merhaba işletim sistemi diski için hello önyükleme yükleyicisi girişi de hello UUID tabanlı bağlama gösterdiğinden emin olun.
>
>

- - -
* SAP GUI (için yönetim ve Kurulum amacıyla) bu tür bir şablonda önceden yüklenebilir.
* Bu yazılım hello ile çalışabilirsiniz sürece VM'ler şirket içi senaryolarda başarıyla yüklenebilmesi için gerekli toorun hello yeniden adlandırmak VM Merhaba diğer yazılım.

Merhaba VM yeterince hazırlanır toobe genel ve sonunda bağımsız/kullanıcıları hesapları hello kullanılamaz olarak Azure dağıtım senaryosu hedeflenen, böyle bir görüntüyü genelleme hello son hazırlık adımı yürütülür.

##### <a name="generalizing-a-vm"></a>Bir VM genelleme
- - -
> ![Windows][Logo_Windows] Windows
>
> Merhaba son tooa VM bir yönetici hesabıyla toolog adımdır. 'Yönetici' olarak bir Windows komut penceresi açın. Too%Windir%\Windows\System32\sysprep gidin ve sysprep.exe yürütün.
> Küçük bir pencere görüntülenir. Önemli toocheck hello 'Generalize' seçeneği olan (Merhaba varsayılan olarak atanmamış checked) ve onun 'Yeniden başlatma' too'Shutdown varsayılandan hello kapatma seçeneği Değiştir '. Bu yordamı hello sysprep işleminin yürütülen şirket içi hello VM konuk işletim sistemini olduğunu varsayar.
> Zaten Azure'da çalışan bir VM ile tooperform hello yordamı istiyorsanız açıklanan başlangıç adımları izleyin [bu makalede](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/capture-image-resource).
>
> ![Linux][Logo_Linux] Linux
>
> [Nasıl toocapture Resource Manager şablonu olarak Linux sanal makine toouse][capture-image-linux-step-2-create-vm-image]
>
>

- - -
### <a name="transferring-vms-and-vhds-between-on-premises-tooazure"></a>Sanal makineleri ve VHD şirket içi tooAzure arasında aktarma
VM görüntüleri ve diskleri tooAzure karşıya hello Azure portal mümkün olmadığından, toouse Azure PowerShell cmdlet'lerini veya CLI gerekir. Diğer bir olasılık hello Aracı 'AzCopy' hello kullanılır. Merhaba aracı VHD'leri (her iki yönde) şirket içi ve Azure arasında kopyalayabilirsiniz. Ayrıca, Azure bölgeler arasında VHD'ler de kopyalayabilirsiniz. Lütfen bakın [bu belgeleri] [ storage-use-azcopy] karşıdan yükleme ve AzCopy kullanımı.

Üçüncü bir alternatif toouse çeşitli üçüncü taraf GUI tabanlı araçlar da olacaktır. Bununla birlikte, lütfen bu araçları Azure sayfa Bloblarını destekliyorsanız emin olun. Toouse Azure sayfa blobu ihtiyacımız bizim amacıyla depolamak için (Merhaba farklar burada açıklanmıştır: <https://docs.microsoft.com/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs>). Ayrıca Azure tarafından sağlanan hello hello VM'ler ve karşıya toobe gereken VHD'ler sıkıştırma içinde çok verimli araçlardır. Bu önemlidir, çünkü bu verimliliği sıkıştırma (yine de hello karşıya yükleme bağlantı toohello hello şirket içi tesis ve hello Azure dağıtım bölge Internet'ten hedeflenen bağlı olarak değişir) hello karşıya yükleme süresini azaltır. Bu, VM veya VHD Avrupa konumu toohello ABD tabanlı Azure veri merkezleri karşıya daha uzun sürer gelen karşıya aynı VM'ler/VHD'ler toohello Avrupa Azure veri merkezlerinde hello Orta bir varsayılır.

#### <a name="a43e40e6-1acc-4633-9816-8f095d5a7b6a"></a>Şirket içi tooAzure VHD'den karşıya yükleme
var olan VM veya hello VHD'den şirket içi böyle bir VM ağı veya VHD gereken toomeet hello gereksinimleri bölümde listelenen tooupload [VM genelleştirilmiş olmayan bir disk ile şirket içi tooAzure geçiş hazırlığı] [ planning-guide-5.2.1] bu belgenin.

Bu tür bir VM genelleştirilmiş toobe gerekmez ve hello durumu ve hello kapanışında içi yan sonra sahip şekli karşıya yüklenebilir. Merhaba aynı herhangi bir işletim sistemini içermeyen ek VHD'ler için geçerlidir.

##### <a name="uploading-a-vhd-and-making-it-an-azure-disk"></a>Bir VHD yüklemek ve bir Azure diski yapma
Bu durumda biz tooupload ile veya olmadan bir işletim sisteminde, bir VHD istediğiniz ve tooa bir veri diski olarak VM bağlama veya işletim sistemi diski olarak kullanın. Bu çok adımlı bir işlemdir

**PowerShell**

* Tooyour abonelikle oturum *Login-AzureRmAccount*
* İçeriğiniz ile Merhaba aboneliği ayarlamak *Set-AzureRmContext* ve parametre Subscriptionıd veya varlığıyla SubscriptionName - <https://docs.microsoft.com/powershell/module/azurerm.profile/set-azurermcontext>
* Karşıya yükleme VHD ile Merhaba *Ekle AzureRmVhd* tooan Azure depolama hesabı - bkz <https://docs.microsoft.com/powershell/module/azurerm.compute/add-azurermvhd>
* (İsteğe bağlı) VHD hello yönetilen bir Disk oluşturma ile *yeni AzureRmDisk* -bkz <https://docs.microsoft.com/powershell/module/azurerm.compute/new-azurermdisk>
* Yeni bir VM yapılandırması toohello VHD hello işletim sistemi diski veya yönetilen diskle ayarlanmış *kümesi AzureRmVMOSDisk* -bkz <https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmosdisk>
* Merhaba VM yapılandırma ile yeni bir VM oluşturun *New-AzureRmVM* -bkz <https://docs.microsoft.com/powershell/module/azurerm.compute/new-azurermvm>
* Bir veri diski tooa ekleme yeni VM ile *Ekle AzureRmVMDataDisk* -bkz <https://docs.microsoft.com/powershell/module/azurerm.compute/add-azurermvmdatadisk>

**Azure CLI 2.0**

* Tooyour abonelikle oturum *az oturum açma*
* Aboneliğinizi seçin *az hesabı kümesi--abonelik`<subscription name or id`>*
* Karşıya yükleme VHD ile Merhaba *az depolama blob karşıya yükleme* -bkz [kullanma hello Azure Storage ile Azure CLI][storage-azure-cli]
* (İsteğe bağlı) VHD hello yönetilen bir Disk oluşturma ile *az disketi* -https://docs.microsoft.com/cli/azure/disk#create bakın
* İle işletim sistemi diski olarak Hello karşıya VHD veya yönetilen Disk belirten yeni bir VM oluşturmak *az vm oluşturma* ve parametre *--attach-os-disk*
* Bir veri diski tooa ekleme yeni VM ile *az vm diskini* ve parametre *--yeni*

**Şablon**

* Merhaba VHD Powershell veya Azure CLI ile karşıya yükle
* (İsteğe bağlı) Merhaba VHD Powershell, Azure CLI veya hello Azure portal ile yönetilen bir Disk oluşturun
* Gösterildiği gibi hello VHD başvuran bir JSON şablonu ile Merhaba VM dağıtmak [Bu örnek JSON şablonunu](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json) ya da gösterildiği gibi yönetilen diskleri kullanarak [Bu örnek JSON şablonunu](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/sap-2-tier-user-disk-md/azuredeploy.json).

#### <a name="deployment-of-a-vm-image"></a>Bir VM görüntüsü dağıtımını
var olan VM veya hello VHD'den şirket içi isteğe bağlı olarak sipariş toouse bir Azure VM görüntü olarak bu tür bir VM ağ veya VHD ihtiyacınız bölümde listelenen toomeet hello gereksinimleri tooupload [için SAPmüşteriyeözgügörüntüsüolanbirVMdağıtımıiçinhazırlık] [ planning-guide-5.2.2] bu belgenin.

* Kullanım *sysprep* Windows veya *waagent-deprovision* Linux toogeneralize üzerinde VM - bkz [Sysprep Teknik Başvurusu](https://technet.microsoft.com/library/cc766049.aspx) Windows için veya [nasıl toocapture bir Resource Manager şablonu olarak Linux sanal makine toouse] [ capture-image-linux-step-2-create-vm-image] Linux için
* Tooyour abonelikle oturum *Login-AzureRmAccount*
* İçeriğiniz ile Merhaba aboneliği ayarlamak *Set-AzureRmContext* ve parametre Subscriptionıd veya varlığıyla SubscriptionName - <https://docs.microsoft.com/powershell/module/azurerm.profile/set-azurermcontext>
* Karşıya yükleme VHD ile Merhaba *Ekle AzureRmVhd* tooan Azure depolama hesabı - bkz <https://docs.microsoft.com/powershell/module/azurerm.compute/add-azurermvhd>
* (İsteğe bağlı) VHD hello yönetilen bir Disk görüntüsü oluşturma ile *yeni AzureRmImage* -bkz <https://docs.microsoft.com/powershell/module/azurerm.compute/new-azurermimage>
* Yeni bir VM yapılandırması toothe Hello OS diskini ayarlayın
  * VHD ile *kümesi AzureRmVMOSDisk - SourceImageUri - CreateOption fromImage* -bkz <https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmosdisk>
  * Disk görüntüsü yönetilen *kümesi AzureRmVMSourceImage* -bkz <https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmsourceimage>
* Merhaba VM yapılandırma ile yeni bir VM oluşturun *New-AzureRmVM* -bkz <https://docs.microsoft.com/powershell/module/azurerm.compute/new-azurermvm>

**Azure CLI 2.0**

* Kullanım *sysprep* Windows veya *waagent-deprovision* Linux toogeneralize üzerinde VM - bkz [Sysprep Teknik Başvurusu](https://technet.microsoft.com/library/cc766049.aspx) Windows için veya [nasıl toocapture bir Resource Manager şablonu olarak Linux sanal makine toouse] [ capture-image-linux-step-2-create-vm-image] Linux için
* Tooyour abonelikle oturum *az oturum açma*
* Aboneliğinizi seçin *az hesabı kümesi--abonelik`<subscription name or id`>*
* Karşıya yükleme VHD ile Merhaba *az depolama blob karşıya yükleme* -bkz [kullanma hello Azure Storage ile Azure CLI][storage-azure-cli]
* (İsteğe bağlı) VHD hello yönetilen bir Disk görüntüsü oluşturma ile *az görüntü oluşturma* -https://docs.microsoft.com/cli/azure/image#create bakın
* İle işletim sistemi diski olarak Hello karşıya VHD veya Disk görüntüsü yönetilen belirten yeni bir VM oluşturmak *az vm oluşturma* ve parametre *--görüntüsü*

**Şablon**

* Kullanım *sysprep* Windows veya *waagent-deprovision* Linux toogeneralize üzerinde VM - bkz [Sysprep Teknik Başvurusu](https://technet.microsoft.com/library/cc766049.aspx) Windows için veya [nasıl toocapture bir Resource Manager şablonu olarak Linux sanal makine toouse] [ capture-image-linux-step-2-create-vm-image] Linux için
* Merhaba VHD Powershell veya Azure CLI ile karşıya yükle
* (İsteğe bağlı) Merhaba VHD Powershell, Azure CLI veya hello Azure portal ile yönetilen bir Disk görüntüsü oluşturun
* Gösterildiği gibi hello görüntü VHD başvuran bir JSON şablonu ile Merhaba VM dağıtmak [Bu örnek JSON şablonunu](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/sap-2-tier-user-image/azuredeploy.json) veya kullanarak hello yönetilen Disk görüntüsü gösterildiği gibi [Bu örnek JSON şablonunu](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json).

#### <a name="downloading-vhds-or-managed-disks-tooon-premises"></a>VHD'leri veya yönetilen diskleri tooon içi indirme
Bir hizmet olarak Azure altyapısı mümkün tooupload VHD'leri ve SAP sistemleri yalnızca olma tek yönlü bir yol değil. SAP taşıyabilirsiniz Azure sistemlerden de hello şirket içi dünyaya yedekleyin.

İndirme hello VHD'leri veya yönetilen diskleri hello Hello süre boyunca etkin olamaz. Bile takılı tooVMs olan diskleri indirirken kapatılır ve serbest VM gereksinimlerini toobe hello. Ardından yeni bir sistemi kullanılan tooset edileceği, şirket içi ve kabul edilebilir değilse hello hello süresi sırasında indirin ve sistem azure'da hello hello yeni sistem kurulumu hello içerik toodownload hello veritabanı yalnızca istiyorsanız hala işletimsel olabilir , bir diske sıkıştırılmış veritabanı yedeklemesi gerçekleştirerek uzun bir kesinti süresini önler ve ayrıca hello işletim sistemi temel VM indirmek yerine bu diski hemen indirin.

#### <a name="powershell"></a>PowerShell

  * Yönetilen bir Disk indirme  
  İlk tooget erişim toohello blob hello yönetilen Disk, temel alınan ihtiyacınız var. Sonra hello temel blob tooa yeni depolama hesabı kopyalayın ve bu depolama hesabından hello blob indirin.

  ```powershell
  $access = Grant-AzureRmDiskAccess -ResourceGroupName <resource group> -DiskName <disk name> -Access Read -DurationInSecond 3600
  $key = (Get-AzureRmStorageAccountKey -ResourceGroupName <resource group> -Name <storage account name>)[0].Value
  $destContext = (New-AzureStorageContext -StorageAccountName <storage account name -StorageAccountKey $key)
  Start-AzureStorageBlobCopy -AbsoluteUri $access.AccessSAS -DestContainer <container name> -DestBlob <blob name> -DestContext $destContext
  # Wait for blob copy toofinish
  Get-AzureStorageBlobCopyState -Container <container name> -Blob <blob name> -Context $destContext
  Save-AzureRmVhd -SourceUri <blob in new storage account> -LocalFilePath <local file path> -StorageKey $key
  # Wait for download toofinish
  Revoke-AzureRmDiskAccess -ResourceGroupName <resource group> -DiskName <disk name>
  ```

  * Bir VHD indirme  
  Hello SAP sistem durdurulur ve hello VM kapatılır, kullanabileceğiniz hello hello PowerShell cmdlet'ini Kaydet AzureRmVhd hedef toodownload hello VHD diskleri toohello şirket içi world destekleyen şirket içi. Merhaba hello hello 'Depolama bölüm' bulabileceğiniz VHD hello URL'sini gerekir, sipariş toodo içinde hello VHD olması gereken yerde tooknow Azure portal (Merhaba VHD oluşturulduğu gerek toonavigate toohello depolama hesabı ve hello depolama kapsayıcısı) ve gerektiğinde kopyalanır.

  Ardından yalnızca hello parametresi SourceUri hello VHD toodownload ve hello LocalFilePath hello URL'si olarak hello fiziksel konumu hello (adı dahil) VHD olarak tanımlayarak hello komutu yararlanabilirsiniz. Merhaba komutu gibi görünebilir:

  ```powerhell
  Save-AzureRmVhd -ResourceGroupName <resource group name of storage account> -SourceUri http://<storage account name>.blob.core.windows.net/<container name>/sapidedata.vhd -LocalFilePath E:\Azure_downloads\sapidesdata.vhd
  ```

  Merhaba Kaydet AzureRmVhd cmdlet daha fazla ayrıntı için lütfen burayı <https://docs.microsoft.com/powershell/module/azurerm.compute/save-azurermvhd>.

#### <a name="cli-20"></a>CLI 2.0
  * Yönetilen bir Disk indirme  
  İlk tooget erişim toohello blob hello yönetilen Disk, temel alınan ihtiyacınız var. Sonra hello temel blob tooa yeni depolama hesabı kopyalayın ve bu depolama hesabından hello blob indirin.
  ```
  az disk grant-access --ids "/subscriptions/<subscription id>/resourceGroups/<resource group>/providers/Microsoft.Compute/disks/<disk name>" --duration-in-seconds 3600
  az storage blob download --sas-token "<sas token>" --account-name <account name> --container-name <container name> --name <blob name> --file <local file>
  az disk revoke-access --ids "/subscriptions/<subscription id>/resourceGroups/<resource group>/providers/Microsoft.Compute/disks/<disk name>"
  ```

  * Bir VHD indirme   
  Merhaba SAP sistem durduruldu ve hello VM kapatılır sonra hello Azure CLI komutunu kullanabilirsiniz _azure depolama blob yükleme_ hello şirket içi hedefte toodownload hello VHD geri toohello şirket içi world diskler. Merhaba adı ve hello hello 'Depolama bölüm' bulabileceğiniz VHD hello kapsayıcının Merhaba gereksinim duyduğunuz, sipariş toodo Azure portal (Merhaba VHD oluşturulduğu gerek toonavigate toohello depolama hesabı ve hello depolama kapsayıcısı) ve tooknow gerektiğinde nerede Merhaba VHD için kopyalanmalıdır.

  Ardından yalnızca hello parametreleri blob ve hello VHD toodownload ve hello hedef kapsayıcının hello fiziksel hedef konumu hello (adı dahil) VHD olarak tanımlama hello komutu yararlanabilirsiniz. Merhaba komutu gibi görünebilir:

  ```
  az storage blob download --name <name of hello VHD toodownload> --container-name <container of hello VHD toodownload> --account-name <storage account name of hello VHD toodownload> --account-key <storage account key> --file <destination of hello VHD toodownload>
  ```

### <a name="transferring-vms-and-disks-within-azure"></a>VM'ler ve Azure içinde diskleri aktarma
#### <a name="copying-sap-systems-within-azure"></a>Azure içinde SAP sistemleri kopyalama
SAP sistem ya da bir SAP uygulama katmanı destekleyen bile bir adanmış DBMS sunucusu olasılıkla ya da ' % s'hello OS hello ikililerini içeren veya veri hello birden çok disk oluşur ve dosyalar hello SAP veritabanının oturum. Diskleri kopyalamanın Azure işlevleri hello ne hello diskleri tooa yerel disk kaydetme Azure işlevselliğini sahip birden çok disk eşzamanlı anlık görüntü bir eşitleme mekanizması. Bu nedenle, hello hello durumunu kopyaladığınız veya bu takılı olsa bile diskleri kaydedilmiş hello karşı aynı VM farklı olacaktır. Başka bir deyişle, farklı veri ve hello farklı disklerde bulunan logfile(s) sahip olmanın hello somut durumda hello uçtaki hello veritabanı tutarsız olabilir.

**Sonuç: Sipariş toocopy veya toostop hello SAP sistem gerekir ve ayrıca gerekir bir SAP sistem yapılandırmasının bir parçası olan diskleri kaydetme VM hello aşağı tooshut dağıtıldı. Yalnızca kopyalama veya diskleri tooeither hello kümesini indirmek Azure veya şirket içi hello SAP sistem bir kopyasını oluşturun.**

Veri diskleri Azure depolama hesabınız VHD dosyaları olarak depolanır ve doğrudan bağlı tooa sanal makineye bağlanabilir veya bir görüntü olarak kullanılabilir. Bu durumda, hello VHD kopyalanan tooanother ekli toohello sanal makine olan önce konumdur. azure'da hello VHD dosyasının tam adı Hello Azure içinde benzersiz olmalıdır. Zaten daha önce belirtildiği gibi hello tür benzer bir üç kısımlı ad adıdır:

    http(s)://<storage account name>.blob.core.windows.net/<container name>/<vhd name>

Veri diskleri yönetilen diskleri de olabilir. Bu durumda, yönetilen Disk hello yeni yönetilen Disk ekli toohello sanal makine olan önce kullanılan toocreate ' dir. Merhaba yönetilen Disk Hello adı kaynak grubunda benzersiz olmalıdır.

##### <a name="powershell"></a>PowerShell
Azure PowerShell cmdlet'leri toocopy VHD gösterildiği gibi kullanabilirsiniz [bu makalede][storage-powershell-guide-full-copy-vhd]. Yeni bir yönetilen Disk toocreate kullanın yeni AzureRmDiskConfig ve yeni AzureRmDisk hello aşağıdaki örnekte gösterildiği gibi.

```powershell
$config = New-AzureRmDiskConfig -CreateOption Copy -SourceUri "/subscriptions/<subscription id>/resourceGroups/<resource group>/providers/Microsoft.Compute/disks/<disk name>" -Location <location>
New-AzureRmDisk -ResourceGroupName <resource group name> -DiskName <disk name> -Disk $config
```

##### <a name="cli-20"></a>CLI 2.0
Azure CLI toocopy VHD gösterildiği gibi kullanabilirsiniz [bu makalede][storage-azure-cli-copy-blobs]. Yeni bir yönetilen Disk toocreate kullanmak *az disketi* hello aşağıdaki örnekte gösterildiği gibi.

```
az disk create --source "/subscriptions/<subscription id>/resourceGroups/<resource group>/providers/Microsoft.Compute/disks/<disk name>" --name <disk name> --resource-group <resource group name> --location <location>
```

##### <a name="azure-storage-tools"></a>Azure Storage araçları
* <http://storageexplorer.com/>

Azure depolama gezginleri Professional sürümleri şurada bulunabilir:

* <http://www.cerebrata.com/>
* <http://clumsyleaf.com/products/cloudxplorer>

bir VHD'nin depolama hesabındaki Hello kopyasını yalnızca birkaç saniye (benzer tooSAN donanım anlık görüntüleri yavaş kopyalama ve kopyalama ile yazma oluşturma) alan bir işlemdir. Merhaba VHD dosyasının bir kopyasını oluşturduktan sonra tooa sanal makine ya da bir görüntü tooattach olarak hello VHD toovirtual makinelerin kopyalar kullanımı ekleyebilirsiniz.

##### <a name="powershell"></a>PowerShell
```powershell
# attach a vhd tooa vm
$vm = Get-AzureRmVM -ResourceGroupName <resource group name> -Name <vm name>
$vm = Add-AzureRmVMDataDisk -VM $vm -Name newdatadisk -VhdUri <path toovhd> -Caching <caching option> -DiskSizeInGB $null -Lun <lun, for example 0> -CreateOption attach
$vm | Update-AzureRmVM

# attach a managed disk tooa vm
$vm = Get-AzureRmVM -ResourceGroupName <resource group name> -Name <vm name>
$vm = Add-AzureRmVMDataDisk -VM $vm -Name newdatadisk -ManagedDiskId <managed disk id> -Caching <caching option> -DiskSizeInGB $null -Lun <lun, for example 0> -CreateOption attach
$vm | Update-AzureRmVM

# attach a copy of hello vhd tooa vm
$vm = Get-AzureRmVM -ResourceGroupName <resource group name> -Name <vm name>
$vm = Add-AzureRmVMDataDisk -VM $vm -Name <disk name> -VhdUri <new path of vhd> -SourceImageUri <path tooimage vhd> -Caching <caching option> -DiskSizeInGB $null -Lun <lun, for example 0> -CreateOption fromImage
$vm | Update-AzureRmVM

# attach a copy of hello managed disk tooa vm
$vm = Get-AzureRmVM -ResourceGroupName <resource group name> -Name <vm name>
$diskConfig = New-AzureRmDiskConfig -Location $vm.Location -CreateOption Copy -SourceUri <source managed disk id>
$disk = New-AzureRmDisk -DiskName <disk name> -Disk $diskConfig -ResourceGroupName <resource group name>
$vm = Add-AzureRmVMDataDisk -VM $vm -Caching <caching option> -Lun <lun, for example 0> -CreateOption attach -ManagedDiskId $disk.Id
$vm | Update-AzureRmVM
```
##### <a name="cli-20"></a>CLI 2.0
```

# attach a vhd tooa vm
az vm unmanaged-disk attach --resource-group <resource group name> --vm-name <vm name> --vhd-uri <path toovhd>

# attach a managed disk tooa vm
az vm disk attach --resource-group <resource group name> --vm-name <vm name> --disk <managed disk id>

# attach a copy of hello vhd tooa vm
# this scenario is currently not possible with Azure CLI. A workaround is toomanually copy hello vhd toohello destination.

# attach a copy of a managed disk tooa vm
az disk create --name <new disk name> --resource-group <resource group name> --location <location of target virtual machine> --source <source managed disk id>
az vm disk attach --disk <new disk name or managed disk id> --resource-group <resource group name> --vm-name <vm name> --caching <caching option> --lun <lun, for example 0>
```

#### <a name="9789b076-2011-4afa-b2fe-b07a8aba58a1"></a>Azure depolama hesapları arasında diskleri kopyalama
Bu görev hello Azure portalı üzerinde gerçekleştirilemiyor. Azure PowerShell cmdlet'leri, Azure CLI veya bir üçüncü taraf depolama tarayıcı kullanabilirsiniz. PowerShell cmdlet'leri hello veya CLI komutları oluşturabilir ve depolama hesapları ve hello Azure aboneliği içindeki bölgeler arasında hello özelliği tooasynchronously kopyalama BLOB'ları içeren BLOB yönetebilirsiniz.

##### <a name="powershell"></a>PowerShell
Bu gibi durumlarda, VHD ayrıca abonelikler arasında kopyalayabilirsiniz. Daha fazla bilgi için okuma [bu makalede][storage-powershell-guide-full-copy-vhd].

Merhaba PS cmdlet mantığı Hello temel akışı şu şekildedir:

* Hello için bir depolama hesabı bağlamını oluşturun **kaynak** depolama hesabıyla *yeni AzureStorageContext* -bkz <https://msdn.microsoft.com/library/dn806380.aspx>
* Hello için bir depolama hesabı bağlamını oluşturun **hedef** depolama hesabıyla *yeni AzureStorageContext* -bkz <https://msdn.microsoft.com/library/dn806380.aspx>
* Merhaba kopyayla Başlat

```powershell
Start-AzureStorageBlobCopy -SrcBlob <source blob name> -SrcContainer <source container name> -SrcContext <variable containing context of source storage account> -DestBlob <target blob name> -DestContainer <target container name> -DestContext <variable containing context of target storage account>
```

* Döngü ile Merhaba kopyasında Hello durumunu denetleme

```powershell
Get-AzureStorageBlobCopyState -Blob <target blob name> -Container <target container name> -Context <variable containing context of target storage account>
```

* Yukarıda açıklandığı gibi Hello yeni VHD tooa sanal makine ekleyin.

Örnekler için bkz [bu makalede][storage-powershell-guide-full-copy-vhd].

##### <a name="cli-20"></a>CLI 2.0
* Merhaba kopyayla Başlat

```
az storage blob copy start --source-blob <source blob name> --source-container <source container name> --source-account-name <source storage account name> --source-account-key <source storage account key> --destination-container <target container name> --destination-blob <target blob name> --account-name <target storage account name> --account-key <target storage account name>
```

* Merhaba, Hello durumunu denetlemek döngü ile kopyalama

```
az storage blob show --name <target blob name> --container <target container name> --account-name <target storage account name> --account-key <target storage account name>
```

* Yukarıda açıklandığı gibi Hello yeni VHD tooa sanal makine ekleyin.

Örnekler için bkz [bu makalede][storage-azure-cli-copy-blobs].

### <a name="disk-handling"></a>Disk işleme
#### <a name="4efec401-91e0-40c0-8e64-f2dceadff646"></a>SAP dağıtımları için VM/disk yapısı
İdeal olarak bir VM hello yapısını işlenmesini hello ve ilişkili hello diskleri çok basit olmalıdır. Şirket içi yüklemelerde sunucu yüklemesi yapılandırılması, birçok yolu müşteriler geliştirmiştir.

* Merhaba işletim sistemi içeren bir temel disk ve tüm hello ikili dosyaları DBMS ve/veya SAP hello. Mart 2015 tarihinden itibaren bu disk boyutu, sınırlı önceki kısıtlamaları yerine too1TB yukarı too127GB olabilir.
* (Merhaba DBMS destekliyorsa) hello DBMS içeren bir veya birden çok disk hello SAP veritabanı dosyası ve hello günlük dosyası hello DBMS geçici depolama alanı, oturum açın. Merhaba veritabanı günlük IOPS gereksinimleri yüksekse, birden çok disk birimindeki gerekli sipariş tooreach hello IOPS toostripe gerekir.
* Hello SAP veritabanında bir veya iki veritabanı dosyalarının ve hello DBMS geçici veri dosyalarını da (Merhaba DBMS destekliyorsa) içeren disk sayısı.

![Azure Iaas VM SAP için başvuru yapılandırması][planning-guide-figure-1300]

[comment]: <> (MShermannd Yapılacaklar açıklamak Linux yapısı)

- - -
> ![Windows][Logo_Windows] Windows
>
> Birçok müşteri ile yapılandırmaları nerede, örneğin, SAP ve DBMS ikili dosyaları hello OS yüklendiği hello c:\ sürücüsünü yüklenmedi gördük. Bunun çeşitli nedenleri vardı, ancak biz geri toohello kök oluştu, bunu genellikle hello sürücüleri küçük ve işletim sistemi yükseltmeleri ek alan 10-15 yıl önce gerekli değil. Bugünlerde artık çok sık koşulların her ikisi de geçerli değildir. Bugün hello c:\ sürücüsü, büyük hacimli diskleri veya sanal makineleri eşlenebilir. Sipariş tookeep dağıtımlarda kendi yapısında basit olduğu toofollow aşağıdaki dağıtım düzeni Azure SAP NetWeaver sistemleri için önerilen
>
> Merhaba Windows işletim sistemi disk belleği dosyası hello D: sürücüsü (kalıcı olmayan disk) üzerinde olmalıdır
>
> ![Linux][Logo_Linux] Linux
>
> Merhaba Linux takas /mnt/mnt/kaynak altında açıklandığı gibi Linux'ta yerleştirin [bu makalede][virtual-machines-linux-agent-user-guide]. Merhaba takas dosyası hello yapılandırma dosyasında hello Linux Aracısı /etc/waagent.conf yapılandırılabilir. Ekleme veya değiştirme ayarları aşağıdaki hello:
>
>

```
ResourceDisk.EnableSwap=y
ResourceDisk.SwapSizeMB=30720
```

tooactivate hello değişiklikleri, gereksinim duyduğunuz toorestart Linux Aracısı ile Merhaba

```
sudo service waagent restart
```

SAP Not okuyun [1597355] hello hakkında daha fazla ayrıntı için önerilen takas dosyası boyutu

- - -
Merhaba DBMS veri dosyaları ve Azure üzerinde barındırılan bu diskleri depolama hello türü için kullanılan disk Hello sayısı hello IOPS gereksinimleri ve gerekli hello gecikme tarafından belirlenen. Tam kotaları açıklanmıştır [bu makalede (Linux)] [ virtual-machines-sizes-linux] ve [bu makalede (Windows)][virtual-machines-sizes-windows].

Son 2 yıl SAP dağıtımları hello üzerinden deneyimi bize olarak özetlenir bazı dersleri öğrettin:

* IOPS trafiği toodifferent veri dosyalarını değil her zaman aynı varolan müşteri sistemleri farklı veri boyutta beri kendi SAP veritabanları temsil eden dosyaları hello. Sonuç olarak LUN olanlar dışında yontulmuş birden çok disk tooplace hello veri dosyaları üzerinde daha iyi bir RAID Yapılandırması'nı kullanarak toobe kullanıma açık. Özellikle Azure standart burada isabet bir IOPS oranı hello kotası hello DBMS işlem günlüğü karşı tek bir disk depolama ile durumlarda vardı. Bu tür senaryolarda hello Premium Storage kullanılması önerilir veya alternatif olarak birden çok standart depolama bir araya getirildiği bir yazılım disklerle RAID.

- - -
> ![Windows][Logo_Windows] Windows
>
> * [Azure Virtual Machines'de SQL Server için performans en iyi yöntemler][virtual-machines-sql-server-performance-best-practices]
>
> ![Linux][Logo_Linux] Linux
>
> * [Yazılım RAID Linux üzerinde yapılandırma][virtual-machines-linux-configure-raid]
> * [Azure'da bir Linux VM LVM yapılandırın][virtual-machines-linux-configure-lvm]
> * [Azure depolama gizli bilgiler ve Linux g/ç en iyi duruma getirme](http://blogs.msdn.com/b/igorpag/archive/2014/10/23/azure-storage-secrets-and-linux-i-o-optimizations.aspx)
>
>

- - -
* Premium depolama önemli daha iyi performans, özellikle kritik işlem günlük yazma gösteriliyor. Beklenen toodeliver üretim performans gibi SAP senaryoları için toouse Azure Premium Storage yararlanabilirsiniz VM-serisi önemle önerilir.

Hello işletim sistemi içeren bu hello disk göz önünde bulundurun ve öneririz gibi SAP ikili dosyaları hello ve hello veritabanı (temel VM) de artık sınırlı too127GB değil. Artık too1TB boyutu yukarı olabilir. Bu gerekli dosya, örneğin dahil olmak üzere tüm hello yeterli alan tookeep olması, toplu iş günlüklerini SAP.

Daha fazla öneri ve özellikle DBMS VM'ler için daha fazla ayrıntı hello Lütfen başvurun [DBMS Dağıtım Kılavuzu][dbms-guide]

#### <a name="disk-handling"></a>Disk işleme
Çoğu senaryoda VM hello toocreate ek diskleri sipariş toodeploy hello SAP veritabanında gerekir. Biz bölüm diskleri sayısının hello hakkında dikkat edilecek noktalar açıklandı [SAP dağıtımları için VM/disk yapısının] [ planning-guide-5.5.1] bu belgenin. Hello Azure portal tooattach sağlar ve temel bir VM dağıtıldıktan sonra Disk ayırma. Merhaba diskler bağlı/ayrılmış hello VM yukarı olduğunda ve ne zaman durduruldu yanı sıra çalışan olabilir. Bu anda olmayan mevcut bir diski tooanother VM bağlı veya bir disk eklerken hello Azure portal tooattach boş disk sunar.

**Not**: diskleri ekli tooone VM yalnızca belirli bir zamanda olabilir.

![Attach / detach Azure Standard Storage disklerle][planning-guide-figure-1400]

Yeni bir sanal makine Hello dağıtımı sırasında toouse yönetilen diskleri istediğiniz veya Azure depolama hesaplarında disklerinizi yerleştirin olup olmadığını karar verebilirsiniz. Premium depolama toouse istiyorsanız, yönetilen diskleri kullanmanızı öneririz.

Ardından, yeni ve boş bir disk toocreate istediğiniz veya tooselect kullanılabilir olmalı ve daha önce yüklenen bir mevcut disk isteyip istemediğinizi toohello VM şimdi bağlı olup olmadığını toodecide gerekir.

**Önemli**:, **yok** toouse ana bilgisayar önbelleğe alma standart Azure Storage ile istiyor. Hiçbiri hello varsayılan olarak hello konak önbelleği tercihi bırakmanız gerekir. Merhaba g/ç özelliğini genellikle normal g/ç trafiği veritabanı veri dosyası gibi salt okunur ise Azure Premium Storage ile okuma önbelleği etkinleştirmeniz gerekir. Veritabanı işlem günlüğü dosyasını durumunda, önbelleğe alma önerilir.

- - -
> ![Windows][Logo_Windows] Windows
>
> [Nasıl tooattach bir veri diski hello Azure portalı][virtual-machines-linux-attach-disk-portal]
>
> Diskleri bağlıysa, toohello VM tooopen hello Windows Disk Yöneticisi'ni toolog gerekir. Otomatik bağlama bölümde önerildiği gibi etkin değilse [bağlı diskler için otomatik bağlama ayarı][planning-guide-5.5.3], hello yeni eklenen birim gereken çevrimiçi alınır ve başlatılan toobe.
>
> ![Linux][Logo_Linux] Linux
>
> Diskleri bağlı değilse toohello VM toolog gerekir ve açıklandığı gibi hello diskleri başlatma [bu makalede][virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]
>
>

- - -
Merhaba yeni disk boş disk ise, tooformat hello de disk gerekir. Biçimlendirme için özellikle DBMS için hello çıplak dağıtımlar için olduğu gibi aynı önerileri DBMS geçerli veri ve günlük dosyaları hello.

Zaten bölümde belirtildiği [Microsoft Azure sanal makine kavram hello][planning-guide-3.2], bir Azure Storage hesabı g/ç birim bakımından sonsuz kaynaklarını sağlamıyor IOPS ve veri birimi. Genellikle DBMS VM'ler en bu tarafından etkilenir. Sipariş toostay hello Azure depolama hesabı toplu hello sınırının içinde birkaç yüksek g/ç birim VM'ler toodeploy varsa en iyi toouse her VM için ayrı bir depolama hesabı olabilir. Toosee gerekir aksi takdirde, bu sanal makineleri tek her depolama hesabının hello sınırını basarsa olmadan farklı depolama hesapları arasında nasıl dengeleyebilirsiniz. Daha fazla ayrıntı hello açıklanan [DBMS Dağıtım Kılavuzu'na][dbms-guide]. Ayrıca, saf SAP uygulama server Vm'lerinin veya ek VHD'ler sonunda gerektirebilir diğer VM'ler için aklınızda sınırlamalara tutmanız gerekir. Yönetilen Disk kullanırsanız, bu kısıtlama geçerli değildir. Premium depolama toouse planlıyorsanız, yönetilen Disk kullanmanızı öneririz.

Depolama hesapları için uygun olan başka bir konu hello VHD'ler bir depolama hesabında alma olup olmadığını coğrafi olarak çoğaltılmış ' dir. Coğrafi çoğaltma etkin veya hello depolama hesabı düzeyi ve değil hello VM düzeyinde devre dışı. Coğrafi çoğaltma etkinleştirilirse, aynı bölgede depolama hesabı başka bir Azure veri merkezi içinde içine çoğaltılması hello içinde hello VHD'ler hello. Bu karar vermeden önce kısıtlama aşağıdaki hello hakkında düşünmek:

Azure coğrafi çoğaltma her VHD bir VM üzerinde yerel olarak çalışır ve kronolojik sırada hello IOs bir VM'de birden çok VHD arasında çoğaltılmaz. Bu nedenle, hello temsil herhangi ek bağlı VHD'ler toohello VM yanı sıra temel VM hello VHD yinelenir birbirine bağımsızdır. Bu, farklı VHD'ler hello hello değişiklikleri arasında eşitleme olduğu anlamına gelir. Merhaba IOs hello olgu yinelenir hello sırayla bağımsız olarak, coğrafi çoğaltma değil birden çok VHD dağıtılmış kendi veritabanlarını sahip veritabanı sunucuları için değer bunlar yazılan anlamına gelir. Toplama toohello DBMS'da, aynı zamanda olabilir burada yazma veya işlemler verileri farklı VHD'leri ve önemli tookeep hello değişiklikleri sırasını olduğu işlemek diğer uygulamaları. Bu gereksinimi varsa, Azure coğrafi çoğaltma etkinleştirilmemelidir. Bağımlı olup gerekir veya bir dizi VM'ler için ancak başka bir küme için coğrafi çoğaltma isterseniz, zaten VM'ler ve bunların ilişkili VHD'leri coğrafi etkin veya devre dışı çoğaltma sahip farklı depolama hesaplarına sınıflandırabilirsiniz.

#### <a name="17e0d543-7e8c-4160-a7da-dd7117a1ad9d"></a>Otomatik bağlama bağlı diskler için ayarlama
- - -
> ![Windows][Logo_Windows] Windows
>
> İsteğe bağlı olarak kendi görüntüleri veya diskleri oluşturulan VM'ler için gerekli toocheck olduğu ve büyük olasılıkla hello otomatik bağlama parametresi olarak ayarlayın. Bu parametre ayarı, bir yeniden başlatma veya Azure toomount hello yeniden bağlı/sürücüleri otomatik olarak yeniden takılı sonra hello VM izin verir.
> Merhaba parametre hello Azure Marketi Microsoft tarafından sağlanan hello görüntüleri için ayarlanır.
>
> Sipariş tooset hello otomatik bağlama hello komut satırı yürütülebilir diskpart.exe burada hello belgelerine başvurun:
>
> * [DiskPart komut satırı seçenekleri](https://technet.microsoft.com/library/bb490893.aspx)
> * [Otomatik bağlama](http://technet.microsoft.com/library/cc753703.aspx)
>
> Yönetici olarak Hello Windows komut satırı penceresi açık olmalıdır.
>
> Diskleri bağlıysa, toohello VM tooopen hello Windows Disk Yöneticisi'ni toolog gerekir. Otomatik bağlama bölümde önerildiği gibi etkin değilse [bağlı diskler için otomatik bağlama ayarı][planning-guide-5.5.3], hello yeni birim bağlı > Çevrimiçi alınır ve başlatılan toobe gerekiyor.
>
> ![Linux][Logo_Linux] Linux
>
> Bölümünde açıklandığı gibi tooinitialize yeni eklenen boş bir disk gerekir [bu makalede][virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux].
> Ayrıca tooadd yeni diskler toohello /etc/fstab gerekir.
>
>

- - -
### <a name="final-deployment"></a>Son dağıtım
Merhaba son dağıtım ve özellikle bakımından toohello dağıtımınızla birlikte SAP genişletilmiş izleme, tam adımlar toohello başvurun [Dağıtım Kılavuzu'na][deployment-guide].

## <a name="accessing-sap-systems-running-within-azure-vms"></a>Azure VM'ler içinde çalışan SAP sistemler erişme
Yalnızca bulut senaryoları için tooconnect toothose SAP sistemleri arasında hello isteyebilirsiniz SAP GUI kullanarak genel internet. Bu durumlarda, hello aşağıdaki yordamları uygulanan toobe gerekir.

Aşağıdakiler ele alınacaktır hello belgenin sonraki bölümlerinde, diğer ana senaryo, bir siteden siteye (VPN tüneli) veya Azure ExpressRoute bağlantısı hello şirket içi sistemleri ve Azure sistemleri arasında olan şirket içi dağıtımlarda bağlanan tooSAP sistemleri hello.

### <a name="remote-access-toosap-systems"></a>Uzaktan erişim tooSAP sistemleri
Azure Resource Manager ile Merhaba eski Klasik modelde varsayılan uç nokta yok artık gibi vardır. Bir Azure ARM VM tüm bağlantı noktalarının açık olduğunu sürece:

1. Hiçbir ağ güvenlik grubu hello alt ağ veya hello ağ arabirimi için tanımlanır. Ağ trafiği tooAzure VM'ler sözde "ağ güvenlik grupları" güvenli hale getirilebilir. Daha fazla bilgi için bkz: [bir ağ güvenlik grubu (NSG) nedir?][virtual-networks-nsg]
2. Azure yük dengeleyici hello ağ arabirimi için tanımlanır   

Bölümünde açıklandığı gibi Hello mimarisi birbirinden Klasik modeli ve ARM bkz [bu makalede][virtual-machines-azure-resource-manager-architecture].

#### <a name="configuration-of-hello-sap-system-and-sap-gui-connectivity-for-cloud-only-scenario"></a>Merhaba SAP sistem ve SAP GUI bağlantısı yalnızca bulut senaryosu için yapılandırma
Lütfen ayrıntıları toothis konu tanımlayan bu makalesine bakın: <http://blogs.msdn.com/b/saponsqlserver/archive/2014/06/24/sap-gui-connection-closed-when-connecting-to-sap-system-in-azure.aspx>

#### <a name="changing-firewall-settings-within-vm"></a>VM dahilinde güvenlik duvarı ayarlarını değiştirme
Sanal makineler tooallow gerekli tooconfigure hello güvenlik duvarını olabilir gelen trafiği tooyour SAP sistem.

- - -
> ![Windows][Logo_Windows] Windows
>
> Varsayılan olarak, hello Azure dağıtılan VM dahilinde Windows Güvenlik Duvarı etkinleştirilir. Açılan tooallow hello SAP bağlantı noktası toobe şimdi gerekir, aksi takdirde hello SAP GUI mümkün tooconnect olmaz.
> toodo bu:
>
> * Denetim masası\sistem ve güvenlik\windows güvenlik duvarı too'Advanced ayarları.
> * Şimdi gelen kuralları ve seçtiğiniz 'Yeni Kural' ni sağ tıklatın.
> * Hello aşağıdaki Sihirbazı yeni bir 'Bağlantı noktası' Kural toocreate seçtiniz.
> * Merhaba sonraki adımda hello Sihirbazı'nın, TCP ve türü hello ayarı tooopen istediğiniz başlangıç bağlantı noktası numarası bırakın. Bizim SAP örnek kimliği 00 olduğundan, biz 3200 sürdü. Farklı bir örnek numarasını örneğiniz varsa, daha önce hello örnek sayısına göre tanımlanan hello bağlantı noktası açık olmalıdır.
> * Merhaba sonraki bölümünde Başlangıç Sihirbazı, tooleave hello öğesi 'İşaretli bağlantı izin ver' gereklidir.
> * Hello kural etki alanı, özel ve ortak ağ için geçerli olup olmayacağını hello sonraki adımda hello Sihirbazı'nın toodefine gerekir. Lütfen gerekli tooyour gerekiyorsa bunu ayarlayın. Ancak, SAP GUI ile dışında hello hello ortak ağ üzerinden bağlantı, toohave hello kural toohello ortak ağ gerekir.
> * Merhaba hello sihirbazının son adımı, hello kural adı ve 'Son' tuşuna basarak kaydedin
>
> Merhaba kural hemen etkin olur.
>
> ![Bağlantı noktası kuralı tanımı][planning-guide-figure-1600]
>
> ![Linux][Logo_Linux] Linux
>
> Merhaba Linux hello Azure Marketi görüntülerinde hello iptables Güvenlik Duvarı varsayılan olarak etkinleştirmeyin ve hello bağlantı tooyour SAP sistem çalışması gerekir. İptables veya başka bir güvenlik duvarı etkinleştirilirse, lütfen iptables toohello belgelerine bakın veya hello kullanılan güvenlik duvarı tooallow gelen tcp trafiğine çok bağlantı noktası 32xx (xx olduğu hello sistem numarası SAP sisteminizin).
>
>

- - -
#### <a name="security-recommendations"></a>Güvenlik önerileri
Merhaba SAP GUI çalışıyor, ancak ilk hello portunu toohello SAP ileti sunucu işlemi (bağlantı noktası 36xx) bağlanan hello SAP örnekleri (bağlantı noktası 32xx) tooany hemen bağlanmaz. Merhaba hello çok aynı bağlantı noktası geçmiş içinde hello ileti sunucusu tarafından hello iç iletişim toohello uygulama örnekleri için kullanıldı. tooprevent yanlışlıkla Azure hello iç ileti Server'da iletişim bağlantı noktalarını değiştirilebilir iletişim kurmasını uygulama sunucuları şirket içi. Merhaba SAP ileti sunucusu kendi uygulama örnekleri tooa farklı bağlantı noktası numarası, projeyi test etme için geliştirme kopyasını gibi şirket içi sistemlerden klonlanmış sistemler arasında toochange hello iç iletişimi önerilir VS. Bu hello varsayılan profili parametresiyle yapılabilir:

> rdisp/msserv_internal
>
>

açıklandığı gibi [hello SAP ileti sunucusu için güvenlik ayarları](https://help.sap.com/saphelp_nwpi71/helpdata/en/47/c56a6938fb2d65e10000000a42189c/content.htm)

## <a name="96a77628-a05e-475d-9df3-fb82217e8f14"></a>SAP örneklerinin yalnızca bulut dağıtımının kavramları
### <a name="3e9c3690-da67-421a-bc3f-12c520d99a30"></a>SAP demo/senaryo eğitimi NetWeaver tek VM
![Tek başına VM SAP demo sistemler hello ile aynı VM adları çalıştıran, yalıtılmış Azure bulut Hizmetleri][planning-guide-figure-1700]

Bu senaryoda (bölüm bkz [yalnızca bulut] [ planning-guide-2.1] bu belgenin) hello tam eğitim/tanıtım senaryo bulunduğu bir tipik eğitim/tanıtım sistem senaryosu tek bir VM'de uyguluyorsanız. Merhaba dağıtım VM görüntü şablonları üzerinden yapılır varsayalım. Ayrıca bu hello sahip hello VM'ler ile dağıtılan bu demo/eğitimleri VM'ler gerek toobe katları aynı varsayıyoruz adı.

Merhaba varsayılır bölüm bazı bölümlerinde açıklandığı gibi bir VM görüntüsü oluşturulan [SAP Azure VM'lerin hazırlanıyor] [ planning-guide-5.2] bu belgedeki.

olayları tooimplement hello senaryonun Hello dizisi şöyle görünür:

##### <a name="powershell"></a>PowerShell
* Her eğitim/tanıtım yatay için yeni bir kaynak grubu oluştur

```powershell
$rgName = "SAPERPDemo1"
New-AzureRmResourceGroup -Name $rgName -Location "North Europe"
```
* Toouse yönetilen diskleri istemiyorsanız, yeni bir depolama hesabı oluşturma

```powershell
$suffix = Get-Random -Minimum 100000 -Maximum 999999
$account = New-AzureRmStorageAccount -ResourceGroupName $rgName -Name "saperpdemo$suffix" -SkuName Standard_LRS -Kind "Storage" -Location "North Europe"
```

* Yeni bir sanal ağ oluştur her eğitim/tanıtım yatay tooenable hello kullanımını hello için aynı ana bilgisayar adı ve IP adresleri. Merhaba sanal ağ, yalnızca SSH için trafiği tooport 3389 tooenable Uzak Masaüstü erişimi ve bağlantı noktası 22 izin veren bir ağ güvenlik grubu tarafından korunuyor.

```powershell
# Create a new Virtual Network
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name SAPERPDemoNSGRDP -Protocol * -SourcePortRange * -DestinationPortRange 3389 -Access Allow -Direction Inbound -SourceAddressPrefix * -DestinationAddressPrefix * -Priority 100
$sshRule = New-AzureRmNetworkSecurityRuleConfig -Name SAPERPDemoNSGSSH -Protocol * -SourcePortRange * -DestinationPortRange 22 -Access Allow -Direction Inbound -SourceAddressPrefix * -DestinationAddressPrefix * -Priority 101
$nsg = New-AzureRmNetworkSecurityGroup -Name SAPERPDemoNSG -ResourceGroupName $rgName -Location  "North Europe" -SecurityRules $rdpRule,$sshRule

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name Subnet1 -AddressPrefix  10.0.1.0/24 -NetworkSecurityGroup $nsg
$vnet = New-AzureRmVirtualNetwork -Name SAPERPDemoVNet -ResourceGroupName $rgName -Location "North Europe"  -AddressPrefix 10.0.1.0/24 -Subnet $subnetConfig
```

* Merhaba kullanılan tooaccess hello sanal makineden olabilecek yeni bir ortak IP adresi oluşturma Internet

```powershell
# Create a public IP address with a DNS name
$pip = New-AzureRmPublicIpAddress -Name SAPERPDemoPIP -ResourceGroupName $rgName -Location "North Europe" -DomainNameLabel $rgName.ToLower() -AllocationMethod Dynamic
```

* Merhaba sanal makine için yeni bir ağ arabirimi oluştur

```powershell
# Create a new Network Interface
$nic = New-AzureRmNetworkInterface -Name SAPERPDemoNIC -ResourceGroupName $rgName -Location "North Europe" -Subnet $vnet.Subnets[0] -PublicIpAddress $pip
```

* Bir sanal makine oluşturun. Merhaba yalnızca bulut senaryosu için her VM hello olacaktır aynı adı. Merhaba hello SAP NetWeaver bu VM'lerin durumlarda olacaktır SAP SID'si hello aynı de. Azure kaynak grubu içinde hello hello VM hello adını toobe benzersiz gerekiyor, ancak farklı Azure kaynak gruplarını VM'ler ile Merhaba çalıştırabilirsiniz aynı adı. Varsayılan 'Yönetici' hesabının Windows hello veya Linux ' kök' geçerli değil. Bu nedenle, yeni bir yönetici kullanıcı adı ile birlikte bir parola tanımlanan toobe gerekir. Merhaba VM Hello boyutu da tanımlanan toobe gerekir.

```powershell
#####
# Create a new virtual machine with an official image from hello Azure Marketplace
#####
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vmconfig = New-AzureRmVMConfig -VMName SAPERPDemo -VMSize Standard_D11

# select image
$vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -PublisherName "MicrosoftWindowsServer" -Offer "WindowsServer" -Skus "2012-R2-Datacenter" -Version "latest"
$vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Windows -ComputerName "SAPERPDemo" -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
# $vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -PublisherName "SUSE" -Offer "SLES-SAP" -Skus "12-SP1" -Version "latest"
# $vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -PublisherName "RedHat" -Offer "RHEL" -Skus "7.2" -Version "latest"
# $vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -PublisherName "Oracle" -Offer "Oracle-Linux" -Skus "7.2" -Version "latest"
# $vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Linux -ComputerName "SAPERPDemo" -Credential $cred

$vmconfig = Add-AzureRmVMNetworkInterface -VM $vmconfig -Id $nic.Id

$vmconfig = Set-AzureRmVMBootDiagnostics -Disable -VM $vmconfig
$vm = New-AzureRmVM -ResourceGroupName $rgName -Location "North Europe" -VM $vmconfig
```

```powershell
#####
# Create a new virtual machine with a VHD that contains hello private image that you want toouse
#####
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vmconfig = New-AzureRmVMConfig -VMName SAPERPDemo -VMSize Standard_D11

$vmconfig = Add-AzureRmVMNetworkInterface -VM $vmconfig -Id $nic.Id

$diskName="osfromimage"
$osDiskUri=$account.PrimaryEndpoints.Blob.ToString() + "vhds/" + $diskName  + ".vhd"

$vmconfig = Set-AzureRmVMOSDisk -VM $vmconfig -Name $diskName -VhdUri $osDiskUri -CreateOption fromImage -SourceImageUri <path tooVHD that contains hello OS image> -Windows
$vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Windows -ComputerName "SAPERPDemo" -Credential $cred
#$vmconfig = Set-AzureRmVMOSDisk -VM $vmconfig -Name $diskName -VhdUri $osDiskUri -CreateOption fromImage -SourceImageUri <path tooVHD that contains hello OS image> -Linux
#$vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Linux -ComputerName "SAPERPDemo" -Credential $cred

$vmconfig = Set-AzureRmVMBootDiagnostics -Disable -VM $vmconfig
$vm = New-AzureRmVM -ResourceGroupName $rgName -Location "North Europe" -VM $vmconfig
```

```powershell
#####
# Create a new virtual machine with a Managed Disk Image
#####
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vmconfig = New-AzureRmVMConfig -VMName SAPERPDemo -VMSize Standard_D11

$vmconfig = Add-AzureRmVMNetworkInterface -VM $vmconfig -Id $nic.Id

$vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -Id <Id of Managed Disk Image>
$vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Windows -ComputerName "SAPERPDemo" -Credential $cred
#$vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Linux -ComputerName "SAPERPDemo" -Credential $cred

$vmconfig = Set-AzureRmVMBootDiagnostics -Disable -VM $vmconfig
$vm = New-AzureRmVM -ResourceGroupName $rgName -Location "North Europe" -VM $vmconfig
```

* İsteğe bağlı olarak ek disk ekleyin ve gerekli içerik geri yükleyin. Tüm blob adları (URL'leri toohello BLOB'lar) Azure içinde benzersiz olduğunu unutmayın.

```powershell
# Optional: Attach additional VHD data disks
$vm = Get-AzureRmVM -ResourceGroupName $rgName -Name SAPERPDemo
$dataDiskUri = $account.PrimaryEndpoints.Blob.ToString() + "vhds/datadisk.vhd"
Add-AzureRmVMDataDisk -VM $vm -Name datadisk -VhdUri $dataDiskUri -DiskSizeInGB 1023 -CreateOption empty | Update-AzureRmVM

# Optional: Attach additional Managed Disks
$vm = Get-AzureRmVM -ResourceGroupName $rgName -Name SAPERPDemo
Add-AzureRmVMDataDisk -VM $vm -Name datadisk -DiskSizeInGB 1023 -CreateOption empty -Lun 0 | Update-AzureRmVM
```

##### <a name="cli"></a>CLI
Aşağıdaki örnek kod hello Linux üzerinde kullanılabilir. Windows, lütfen PowerShell yukarıda açıklandığı gibi kullanın veya hello örnek toouse % rgName %$rgName yerine uyum hem hello Windows komutunu kullanarak hello ortam değişkenini *ayarlamak*.

* Her eğitim/tanıtım yatay için yeni bir kaynak grubu oluştur

```
rgName=SAPERPDemo1
rgNameLower=saperpdemo1
az group create --name $rgName --location "North Europe"
```

* Yeni depolama hesabı oluşturma

```
az storage account create --resource-group $rgName --location "North Europe" --kind Storage --sku Standard_LRS --name $rgNameLower
```

* Yeni bir sanal ağ oluştur her eğitim/tanıtım yatay tooenable hello kullanımını hello için aynı ana bilgisayar adı ve IP adresleri. Merhaba sanal ağ, yalnızca SSH için trafiği tooport 3389 tooenable Uzak Masaüstü erişimi ve bağlantı noktası 22 izin veren bir ağ güvenlik grubu tarafından korunuyor.

```
az network nsg create --resource-group $rgName --location "North Europe" --name SAPERPDemoNSG
az network nsg rule create --resource-group $rgName --nsg-name SAPERPDemoNSG --name SAPERPDemoNSGRDP --protocol \* --source-address-prefix \* --source-port-range \* --destination-address-prefix \* --destination-port-range 3389 --access Allow --priority 100 --direction Inbound
az network nsg rule create --resource-group $rgName --nsg-name SAPERPDemoNSG --name SAPERPDemoNSGSSH --protocol \* --source-address-prefix \* --source-port-range \* --destination-address-prefix \* --destination-port-range 22 --access Allow --priority 101 --direction Inbound

az network vnet create --resource-group $rgName --name SAPERPDemoVNet --location "North Europe" --address-prefixes 10.0.1.0/24
az network vnet subnet create --resource-group $rgName --vnet-name SAPERPDemoVNet --name Subnet1 --address-prefix 10.0.1.0/24 --network-security-group SAPERPDemoNSG
```

* Merhaba kullanılan tooaccess hello sanal makineden olabilecek yeni bir ortak IP adresi oluşturma Internet

```
az network public-ip create --resource-group $rgName --name SAPERPDemoPIP --location "North Europe" --dns-name $rgNameLower --allocation-method Dynamic
```

* Merhaba sanal makine için yeni bir ağ arabirimi oluştur

```
az network nic create --resource-group $rgName --location "North Europe" --name SAPERPDemoNIC --public-ip-address SAPERPDemoPIP --subnet Subnet1 --vnet-name SAPERPDemoVNet
```

* Bir sanal makine oluşturun. Merhaba yalnızca bulut senaryosu için her VM hello olacaktır aynı adı. Merhaba hello SAP NetWeaver bu VM'lerin durumlarda olacaktır SAP SID'si hello aynı de. Azure kaynak grubu içinde hello hello VM hello adını toobe benzersiz gerekiyor, ancak farklı Azure kaynak gruplarını VM'ler ile Merhaba çalıştırabilirsiniz aynı adı. Varsayılan 'Yönetici' hesabının Windows hello veya Linux ' kök' geçerli değil. Bu nedenle, yeni bir yönetici kullanıcı adı ile birlikte bir parola tanımlanan toobe gerekir. Merhaba VM Hello boyutu da tanımlanan toobe gerekir.

```
#####
# Create virtual machines using storage accounts
#####
az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest --admin-username <username> --admin-password <password> --size Standard_D11 --use-unmanaged-disk --storage-account $rgNameLower --storage-container-name vhds --os-disk-name os
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image SUSE:SLES-SAP:12-SP1:latest --admin-username <username> --admin-password <password> --size Standard_D11 --use-unmanaged-disk --storage-account $rgNameLower --storage-container-name vhds --os-disk-name os --authentication-type password
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image RedHat:RHEL:7.2:latest --admin-username <username> --admin-password <password> --size Standard_D11 --use-unmanaged-disk --storage-account $rgNameLower --storage-container-name vhds --os-disk-name os --authentication-type password
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image "Oracle:Oracle-Linux:7.2:latest" --admin-username <username> --admin-password <password> --size Standard_D11 --use-unmanaged-disk --storage-account $rgNameLower --storage-container-name vhds --os-disk-name os --authentication-type password

#####
# Create virtual machines using Managed Disks
#####
az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest --admin-username <username> --admin-password <password> --size Standard_DS11_v2 --os-disk-name os
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image SUSE:SLES-SAP:12-SP1:latest --admin-username <username> --admin-password <password> --size Standard_DS11_v2 --os-disk-name os --authentication-type password
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image RedHat:RHEL:7.2:latest --admin-username <username> --admin-password <password> --size Standard_DS11_v2 --os-disk-name os --authentication-type password
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image "Oracle:Oracle-Linux:7.2:latest" --admin-username <username> --admin-password <password> --size Standard_DS11_v2 --os-disk-name os --authentication-type password
```

```
#####
# Create a new virtual machine with a VHD that contains hello private image that you want toouse
#####
az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --os-type Windows --admin-username <username> --admin-password <password> --size Standard_D11 --use-unmanaged-disk --storage-account $rgNameLower --storage-container-name vhds --os-disk-name os --image <path tooimage vhd>
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --os-type Linux --admin-username <username> --admin-password <password> --size Standard_D11 --use-unmanaged-disk --storage-account $rgNameLower --storage-container-name vhds --os-disk-name os --image <path tooimage vhd> --authentication-type password

#####
# Create a new virtual machine with a Managed Disk Image
#####
az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --admin-username <username> --admin-password <password> --size Standard_DS11_v2 --os-disk-name os --image <managed disk image id>
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --admin-username <username> --admin-password <password> --size Standard_DS11_v2 --os-disk-name os --image <managed disk image id> --authentication-type password
```

* İsteğe bağlı olarak ek disk ekleyin ve gerekli içerik geri yükleyin. Tüm blob adları (URL'leri toohello BLOB'lar) Azure içinde benzersiz olduğunu unutmayın.

```
# Optional: Attach additional VHD data disks
az vm unmanaged-disk attach --resource-group $rgName --vm-name SAPERPDemo --size-gb 1023 --vhd-uri https://$rgNameLower.blob.core.windows.net/vhds/data.vhd  --new

# Optional: Attach additional Managed Disks
az vm disk attach --resource-group $rgName --vm-name SAPERPDemo --size-gb 1023 --disk datadisk --new
```

##### <a name="template"></a>Şablon
Github'da hello azure hızlı başlangıç şablonlarını deposunda hello örnek şablonları kullanabilirsiniz.

* [Basit Linux VM](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-linux)
* [Basit bir Windows VM](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows)
* [Görüntüden VM](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image)

### <a name="implement-a-set-of-vms-which-need-toocommunicate-within-azure"></a>Azure içinde toocommunicate gereken sanal makineleri kümesini uygular
Bu yalnızca bulut eğitim ve gösterim amaçları için tipik bir senaryo burada hello demo/senaryo eğitim hello temsil eden yazılım birden çok VM yayılan bir senaryodur. hello farklı bileşenleri hello farklı VM'ler gerek toocommunicate birbirleri ile yüklenir. Yeniden, bu senaryoda, bir şirket içi ağ iletişimi veya şirket içi senaryo gereklidir.

Bu senaryo bir bölümde açıklanan hello yükleme uzantısıdır [tek VM SAP demo/senaryo eğitimi NetWeaver ile] [ planning-guide-7.1] bu belgenin. Bu durumda daha fazla sanal makine tooan varolan bir kaynak grubu eklenir. Hello aşağıdaki örnek hello eğitim yatay bir SAP ASCS/SCS VM'i, DBMS ve SAP uygulama sunucusu örneği VM çalıştıran VM oluşur.

Bu senaryo oluşturmadan önce önce hello senaryoda zaten kullandı temel ayarları hakkında toothink gerekir.

#### <a name="resource-group-and-virtual-machine-naming"></a>Kaynak grubu ve sanal makine adlandırma
Tüm kaynak grubu adları benzersiz olmalıdır. Kendi adlandırma şeması kaynaklarınızın gibi geliştirmek `<rg-name`>-soneki.

Merhaba sanal makine adı toobe hello kaynak grubunda benzersiz sahiptir.

#### <a name="set-up-network-for-communication-between-hello-different-vms"></a>Ağ arasındaki iletişim için ayarlanmış farklı VM'ler hello
![Bir Azure sanal ağ içindeki VM'ler kümesi][planning-guide-figure-1900]

aynı eğitim/tanıtım Windows'un hello klonlar ile çakışma adlandırma tooprevent için her yatay toocreate bir Azure sanal ağı gerekir. DNS ad çözümlemesi Azure tarafından sağlanacak veya Azure (toobe daha fazla burada tartışılan) dışında kendi DNS sunucusunu yapılandırabilirsiniz. Bu senaryoda, biz kendi DNS yapılandırmayın. Bir Azure sanal ağı içindeki tüm sanal makineler için ana bilgisayar adları üzerinden iletişim etkinleştirilecek.

Merhaba tooseparate eğitim veya tanıtım Windows'un sanal ağlar ve yalnızca kaynak grupları olabilir tarafından nedenleri:

* Merhaba SAP yatay gereksinimlerini ayarlandığı kendi AD/OpenLDAP ve her bir hello Windows'un bir etki alanı sunucusu gereksinimlerini toobe bölümü.  
* ayarlama, gerek toowork sabit IP adresleriyle bileşenleri taşıdığından SAP yatay hello.

Azure sanal ağlar ve nasıl toodefine bunları bulunabilir hakkında daha fazla ayrıntı [bu makalede][virtual-networks-create-vnet-arm-pportal].

## <a name="deploying-sap-vms-with-corporate-network-connectivity-cross-premises"></a>SAP VM'ler şirket ağ bağlantısı (şirket içi) ile dağıtma
Bir SAP yatay çalıştırın ve çıplak için birinci sınıf DBMS sunucuları arasında toodivide hello dağıtım istiyorsanız, SAP sistemleri ve Azure Iaas şirket içi sanallaştırılmış ortamlar uygulama katmanları ve daha küçük 2 katmanı için yapılandırılmış. Merhaba temel bir SAP yatay içinde SAP sistemleri toocommunicate birbirleriyle ve hello şirkette, kendi dağıtım biçiminde bağımsız dağıtılan birçok diğer yazılım bileşenleri ile gerektiğini varsayılır. Ayrıca olmamalıdır hello son SAP GUI veya diğer arabirimleri ile bağlanan kullanıcı için hello dağıtım form tarafından sunulan herhangi bir fark. Biz varsa, bu koşullar yalnızca karşılanabilir hello şirket içi Active Directory/OpenLDAP ve DNS hizmetleri genişletilmiş toohello site-için-site/çok siteler bağlantısı veya Azure ExpressRoute gibi özel bağlantıları üzerinden Azure sistemler.

Daha fazla arka plan SAP azure'da hello uygulama ayrıntılarını üzerinde sipariş tooget içinde tooread bölüm öneririz [kavramları, Cloud-Only dağıtım SAP örneklerinin] [ planning-guide-7] açıklayan bu belgenin hello temelleri bazıları oluşturur, Azure ve nasıl bunlar Azure SAP uygulamalarda kullanılmalıdır.

### <a name="scenario-of-an-sap-landscape"></a>Bir SAP yatay senaryosu
Merhaba şirketler arası senaryo kabaca gibi aşağıdaki hello grafik açıklanabilir:

![Şirket içi ve Azure varlıklar arasında siteden siteye bağlantı][planning-guide-figure-2100]

Yukarıda gösterilen hello senaryosu burada hello AD/OpenLDAP şirket içi ve DNS tooAzure genişletilmiş bir senaryo açıklanmaktadır. Merhaba şirket içi tarafında, belirli bir IP adres aralığı Azure abonelik başına ayrılmıştır. Başlangıç IP adresi aralığı tooan Azure Virtual Network hello Azure yan üzerinde atanır.

#### <a name="security-considerations"></a>Güvenlikle ilgili dikkat edilmesi gerekenler
SSL/TLS tarayıcı erişimi için veya VPN tabanlı bağlantılar için sistem toohello Azure erişim gibi hello minimum gereksinim hello güvenli iletişim protokolü kullanılır Hizmetleri. Merhaba şirketler hello VPN bağlantısı kendi şirket ağınız ve Azure arasında çok farklı şekilde ele varsayılır. Bazı şirketler blankly tüm hello bağlantı noktalarını açmanız. Diğer bazı şirketler toobe çok kesin hangi bağlantı noktalarının ihtiyaç duydukları tooopen, vb. isteyebilirsiniz.

Tipik SAP aşağıda hello tablosundaki iletişim bağlantı noktaları listelenir. Temel olarak yeterli tooopen hello SAP ağ geçidi bağlantı noktası olur.

| Hizmet | Bağlantı noktası adı | Örnek `<nn`> 01 = | Varsayılan aralığı (min-maks.) | Açıklama |
| --- | --- | --- | --- | --- |
| Dağıtıcı |sapdp`<nn>` bakın * |3201 |3200 – 3299 |Windows için SAP GUI ve Java tarafından kullanılan SAP göndericisi |
| İleti sunucusu |sapms`<sid`> bkz ** |3600 |Ücretsiz sapms`<anySID`> |SID SAP sistem kimliği = |
| Ağ geçidi |sapgw`<nn`> bkz * |3301 |Boş |SAP ağ geçidi, CPIC ve RFC iletişim için kullanılan |
| SAP yönlendirici |sapdp99 |3299 |Boş |Yalnızca CI (Merkezi örneği) hizmeti adlarının yüklendikten sonra /etc/services tooan rastgele değer atanabilir. |

*) nn = SAP örnek sayısı

*) SID SAP sistem kimliği =

Farklı SAP ürünler için gereken bağlantı noktaları hakkında daha ayrıntılı bilgi veya hizmetleri SAP ürünleri tarafından şurada bulunabilir <http://scn.sap.com/docs/DOC-17124>.
Bu belgeyle hello VPN cihazı belirli SAP ürünleri ve senaryoları için gerekli bağlantı noktaları mümkün tooopen ayrılmış olmalıdır.

Diğer güvenlik ölçer VM'ler böyle bir senaryoda dağıtma toocreate olabilir bir [ağ güvenlik grubu] [ virtual-networks-nsg] toodefine erişim kuralları.

### <a name="dealing-with-different-virtual-machine-series"></a>Farklı sanal makine serisi postalarla
Son 12 ay Hello seyri içinde Microsoft ya da Vcpu, bellek sayısı farklı pek çok daha fazla VM türleri eklenmiş veya daha önemli donanım üzerinde çalıştığı. Bu tüm VM'lerin SAP ile desteklenir (bkz: desteklenen VM SAP Not türlerinde [1928533]). Bu VM'lerin bazıları farklı ana bilgisayar donanım nesli üzerinde çalıştırın. Bu konak donanım nesli yer hello ayrıntı düzeyi, bir Azure ölçek birimi dağıtılır. Burada seçtiğiniz çalıştırılamaz hello farklı VM boyutları aynı ölçek birimi hello anlamına gelir durumlarda gerçekleşebilir. Bir kullanılabilirlik kümesi hello özelliği toospan ölçek birimleri farklı donanımda sınırlıdır.  Tek bir SAP sistem ya da farklı kullanılabilirlik kümeleri içinde farklı SAP sistemleri hello SAP uygulama katmanı G-serisi vm'lerde, olacaktır ve toorun hello A5 A11 vm'lerde DBMS isterseniz örnek toodeploy zorunlu için.

#### <a name="printing-on-a-local-network-printer-from-sap-instance-in-azure"></a>SAP örneğinden Azure yerel ağ yazıcısı yazdırma
##### <a name="printing-over-tcpip-in-cross-premises-scenario"></a>TCP/IP üzerinden şirket içi senaryoda yazdırma
Şirket içi TCP/IP tabanlı ağ yazıcıları Azure VM'deki ayarlama genel hello aynı varsayılmıştır şirket ağınıza VPN siteden siteye tünel veya ExpressRoute bağlantı kuruldu sahip olur.

- - -
> ![Windows][Logo_Windows] Windows
>
> toodo bu:
>
> * Bazı ağ yazıcıları bir Azure VM yazıcınızın yukarı kolay tooset hale getiren bir Yapılandırma Sihirbazı ile gelir. Herhangi bir Sihirbazı yazılım varsa hello yazıcı yukarı tooset toocreate yeni bir TCP/IP yazıcı bağlantı noktasını yazıcı hello "manual" biçimi ile dağıtılır.
> * Açık Denetim Masası -> cihazlar ve yazıcılar Yazıcı Ekle ->
> * TCP/IP adresi veya ana bilgisayar adı kullanarak bir yazıcı Ekle'yi seçin
> * Hello hello yazıcı IP adresini yazın
> * Yazıcı bağlantı noktasını standart 9100
> * Gerekirse hello uygun yazıcı sürücüsü el ile yükleyin.
>
> ![Linux][Logo_Linux] Linux
>
> * yalnızca Windows için ağ yazıcısı gibi hello standart yordamı tooinstall izleyin
> * Merhaba ortak Linux kılavuzları için izlemeniz yeterlidir [SUSE](https://www.suse.com/documentation/sles-12/book_sle_deployment/data/sec_y2_hw_print.html) veya [Red Hat ve Oracle Linux](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/sec-Printer_Configuration.html) nasıl tooadd yazıcı.
>
>

- - -
![Ağ yazdırma][planning-guide-figure-2200]

##### <a name="host-based-printer-over-smb-shared-printer-in-cross-premises-scenario"></a>Ana bilgisayar tabanlı yazıcıya SMB (paylaşılan yazıcı) üzerinden şirket içi senaryosu
Ana bilgisayar tabanlı yazıcılar tasarım gereği ağ ile uyumlu değildir. Ancak, bir ağdaki bilgisayarlar arasında hello yazıcı bağlı tooa gücü açma bilgisayar olduğu sürece bir ana bilgisayar tabanlı yazıcı paylaşılabilir. Şirket bağlanmak siteden siteye ya da ExpressRoute ağ ve yerel yazıcınızın paylaşın. Hello SMB protokolü NetBIOS yerine DNS ad hizmeti kullanır. Merhaba NetBIOS ana bilgisayar adını hello DNS ana bilgisayar adından farklı olabilir. Merhaba standart olarak hello NetBIOS ana bilgisayar adı ve hello DNS ana bilgisayar adıyla aynı olduğundan emin olur. Merhaba DNS etki alanı hello NetBIOS ad alanında mantıklı değildir. Buna göre hello DNS ana bilgisayar adını içeren tam DNS ana bilgisayar adı hello ve DNS etki alanı hello NetBIOS ad alanında kullanılmamalıdır.

Merhaba yazıcı paylaşımı hello ağda benzersiz bir ad tarafından tanımlanır:

* Ana bilgisayar adı hello SMB konağının (her zaman gereklidir).
* (Her zaman gereklidir) hello paylaşımının adı.
* Yazıcı Paylaşımı hello değilse hello etki alanının adını SAP sistem aynı etki alanında.
* Ek olarak, bir kullanıcı adı ve parola gerekli tooaccess hello yazıcı paylaşımı olabilir.

Nasıl yapılır:

- - -
> ![Windows][Logo_Windows] Windows
>
> Yerel yazıcı paylaşın.
> Hello Azure VM, Windows Gezgini hello ve hello yazıcı hello paylaşım adı, türü açın.
> Bir yazıcı Yükleme Sihirbazı'nı hello yükleme işleminde size kılavuzluk.
>
> ![Linux][Logo_Linux] Linux
>
> İşte bazı örnekler içinde Linux ağ yazıcıları yapılandırma veya bölüm de dahil olmak üzere ilgili belgelerin Linux içinde yazdırma ilgili. Merhaba çalışacak şekilde Azure Linux VM'de VM hello sürece VPN bir parçasıdır:
>
> * SLES <https://en.opensuse.org/SDB:Printing_via_SMB_ (Samba) _Share_or_Windows_Share>
> * RHEL veya Oracle Linux <https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/System_Administrators_Guide/sec-Printer_Configuration.html#s1-printing-smb-printer>
>
>

- - -
##### <a name="usb-printer-printer-forwarding"></a>USB yazıcı (Yazıcı iletme)
Merhaba Uzak Masaüstü Hizmetleri tooprovide kullanıcılar hello erişim Azure hello yeteneği tootheir yerel yazıcı cihazları uzak bir oturumda kullanılabilir değil.

- - -
> ![Windows][Logo_Windows] Windows
>
> Windows ile yazdırma hakkında daha fazla bilgi şurada bulunabilir: <http://technet.microsoft.com/library/jj590748.aspx>.
>
>

- - -
#### <a name="integration-of-sap-azure-systems-into-correction-and-transport-system-tms-in-cross-premises"></a>SAP tümleştirme Azure sistemlere düzeltme ve şirket içi (TMS) sistemde taşıma
SAP değiştirme ve taşıma sistem (TMS) gereksinimlerini yapılandırılmış toobe tooexport hello ve hello yatay sistemler arasında taşıma isteği alın. Merhaba kalite güvence (QA) ve üretken sistemleri (PRD) şirket içi ise hello geliştirme örnekleri SAP sisteminin (Geliştirme) Azure içinde bulunduğu varsayılmaktadır. Ayrıca, bir merkezi aktarım dizini olduğunu varsayın.

##### <a name="configuring-hello-transport-domain"></a>Hello aktarım etki alanını yapılandırma
Belirlenmiş taşıması etki alanı denetleyicisi açıklandığı gibi hello gibi hello sistemde aktarım etki alanınızı yapılandırmak [yapılandırma hello aktarım etki alanı denetleyicisi](http://help.sap.com/erp2005_ehp_04/helpdata/en/44/b4a0b47acc11d1899e0000e829fbbd/content.htm). Sistem kullanıcısı TMSADM oluşturulur ve hello RFC hedef oluşturulan gereklidir. Merhaba işlem SM59 kullanarak bu RFC bağlantıları kontrol edebilirsiniz. Ana bilgisayar adı çözümlemesi, aktarım etki alanı genelinde etkinleştirilmesi gerekir.

Nasıl yapılır:

* Senaryomuzda hello QAS sistem hello CTS etki alanı denetleyicisidir içi vermiştir. İşlem STMS çağırın. Merhaba TMS iletişim kutusu görüntülenir. Bir taşıma etki alanı yapılandırma iletişim kutusu görüntülenir. (Aktarım etki alanı henüz yapılandırmadıysanız yalnızca bu iletişim kutusu görünür.)
* Bu otomatik olarak oluşturulan hello kullanıcı TMSADM yetkili olduğu emin olun (SM59 ABAP bağlantı -> -> TMSADM@E61.DOMAIN_E61 -> ayrıntıları -> Utilities(M) yetkilendirme Test ->). İşlem Başlangıç ekranında Hello bu SAP sistem artık hello aşağıda gösterildiği gibi hello aktarım etki alanı denetleyicisi olarak çalışır STMS göstermesi gerekir:

![Hareketin STMS hello etki alanı denetleyicisinde ilk ekran][planning-guide-figure-2300]

#### <a name="including-sap-systems-in-hello-transport-domain"></a>SAP sistemleri hello aktarım etki alanına dahil
Merhaba sırası aktarım etki alanında bir SAP sistemi dahil olmak üzere aşağıdaki gibi görünür:

* Hello Azure geliştirme sisteminde, toohello taşıma sistemi (istemci 000) gidin ve işlem STMS çağırın. Diğer yapılandırma hello iletişim kutusundan seçin ve etki alanındaki dahil sistemiyle devam edin. Merhaba etki alanı denetleyicisi hedef konak belirtin ([SAP sistemlerinde de dahil olmak üzere hello aktarım etki alanı](http://help.sap.com/erp2005_ehp_04/helpdata/en/44/b4a0c17acc11d1899e0000e829fbbd/content.htm?frameset=/en/44/b4a0b47acc11d1899e0000e829fbbd/frameset.htm)). Merhaba sistem hello aktarım etki alanında bulunan bekleme toobe sunulmuştur.
* Güvenlik nedenleriyle, ardından isteğiniz toogo geri toohello etki alanı denetleyicisi tooconfirm sahip. Sisteme genel bakış ve Onayla seçim hello bekleme sistemi. Ardından hello istem ve hello yapılandırma dağıtılmış onaylayın.

Bu SAP Sistem şimdi tüm hello hakkında gerekli bilgileri hello diğer SAP sistemlerinde hello aktarım etki alanı içerir. Merhaba aynı zaman hello adresi hello yeni SAP sisteminin veri tooall hello diğer SAP sistemleri ve hello SAP sistem hello aktarım profilinde hello aktarım denetimin programının girilen gönderilir. RFC'leri ve erişim toohello aktarım dizini hello etki alanının çalışıp çalışmadığını denetleyin.

Her zamanki gibi hello belgelerinde açıklandığı gibi aktarım sisteminizin Hello yapılandırmaya devam [değiştirme ve taşıma sistemi](http://help.sap.com/saphelp_nw70ehp3/helpdata/en/48/c4300fca5d581ce10000000a42189c/content.htm?frameset=/en/44/b4a0b47acc11d1899e0000e829fbbd/frameset.htm).

Nasıl yapılır:

* Şirket içi, STMS doğru yapılandırıldığından emin olun.
* Merhaba hostname hello aktarım etki alanı denetleyicisi, sanal makinenize Azure ve tersine visa çözülebilir emin olun.
* İşlem STMS diğer yapılandırma -> çağrı -> Sistem etki alanındaki içerir.
* Şirket içi TMS sistemde hello Hello bağlantısında onaylayın.
* Taşıma yolları, grupları ve Katmanlar her zamanki gibi yapılandırın.

Siteden siteye bağlanan şirketler arası içinde senaryoları, şirket içi ve Azure arasında hello gecikme hala önemli olabilir. Geliştirme ve test sistemleri tooproduction nesnelerde taşıma hello sırası izleyin veya taşımaları uygulama hakkında düşünün veya destek paketleri toohello farklı sistemleri, fark hello merkezi aktarım hello konumunu bağımlı Dizin, bazı hello sistemlerinin veri okunurken veya hello merkezi aktarım dizininde yazılırken yüksek gecikme karşılaşır. Merhaba benzer tooSAP yatay yapılandırmaları hello farklı sistemleri hello veri merkezleri arasında önemli uzaklıklı farklı veri merkezleri aracılığıyla burada yayılır durumdur.

İçinde bu tür gecikme geçici toowork sipariş ve hızlı okuma veya ayarlayabilirsiniz iki STMS taşıma ve etki alanları (bir şirket içi. bir hello sistemleriyle Azure ve bağlantı hello aktarım alanlarında hello aktarım dizininden tooor yazma çalışma hello sistemleri Lütfen bu kavram hello SAP TMS olarak arkasında hello ilkeleri açıklayan bu belgelere bakın: <http://help.sap.com/saphelp_me60/helpdata/en/c4/6045377b52253de10000009b38f889/content.htm?frameset=/en/57/ 38dd924eb711d182bf0000e829fbfe/frameset.htm>.

Nasıl yapılır:

* Her bir konum (şirket içi ve Azure) aktarım etki alanı ayarlama işlemi STMS kullanarak <http://help.sap.com/saphelp_nw70ehp3/helpdata/en/44/b4a0b47acc11d1899e0000e829fbbd/content.htm>
* Merhaba etki alanlarını etki alanı ile bağlantıyı ve hello iki etki alanı arasında hello bağlantı onaylayın.
  <http://help.SAP.com/saphelp_nw73ehp1/helpdata/en/a3/139838280c4f18e10000009b38f8cf/Content.htm>
* Merhaba yapılandırma bağlı toohello sistemi dağıtın.

#### <a name="rfc-traffic-between-sap-instances-located-in-azure-and-on-premises-cross-premises"></a>Azure ve şirket içi (şirket içi) bulunan SAP örnekleri arasında RFC trafiği
RFC trafiği şirket içi sistemlerini arasında ve azure'a toowork gerekir. bir bağlantı tooset çağırın işlem SM59 kaynak sistemde toodefine ihtiyaç duyacağınız hello hedef sistem doğru bir RFC bağlantısı. Merhaba, RFC bir bağlantının benzer toohello standart kurulum yapılandırmadır.

Merhaba şirketler arası senaryosunda, aynı etki alanı içinde olan birbirleriyle toocommunicate gereken çalışma SAP sistemleri hello VM'ler hello varsayalım. Bu nedenle hello SAP sistemleri arasında bir RFC bağlantısı kurulumu hello kurulum adımlarını ve şirket içi senaryolarda girişleri farklı değildir.

#### <a name="accessing-local-fileshares-from-sap-instances-located-in-azure-or-vice-versa"></a>Azure veya tersi bulunan SAP örneklerinden erişilirken 'local' fileshares
Azure'da bulunan SAP örnekleri hello Kurumsal şirket içinde olan tooaccess dosya paylaşımları gerekir. Ayrıca, şirket içi SAP örnekleri Azure'da bulunan tooaccess dosya paylaşımları gerekir. tooenable hello dosya paylaşımları hello izinleri ve paylaşım seçeneklerini hello yerel sistemde yapılandırmanız gerekir. Merhaba VPN veya Azure ve veri merkeziniz arasında ExpressRoute bağlantı emin tooopen hello bağlantı noktalarını olun.

## <a name="supportability"></a>Desteklenebilirlik
### <a name="6f0a47f3-a289-4090-a053-2521618a28c3"></a>Azure için SAP izleme çözümü
Sipariş tooenable hello görev kritik SAP sistemlerinin Azure hello SAP üzerinde izleme izleme araçları SAPOSCOL veya SAP konak Aracısı SAP için bir Azure izleme uzantısı aracılığıyla hello Azure sanal makine hizmeti konak verileri alın. SAP tarafından Hello taleplerini belirli tooSAP uygulamaları olduğundan, Microsoft olmayan toogenerically uygulama gerekli hello işlevsellik Azure karar ancak müşteriler toodeploy hello gerekli izleme bileşenleri ve yapılandırmaları tootheir için bırakın Azure'da çalışan sanal makineler. Ancak, bileşenler izleme hello dağıtımı ve yaşam döngüsü yönetimini çoğunlukla Azure tarafından otomatik olarak yapılır.

#### <a name="solution-design"></a>Çözüm tasarımı
Merhaba çözüm Azure VM aracısı ve uzantısı çerçevesini hello mimarisine tabanlı SAP izleme tooenable geliştirmiştir. Merhaba hello Azure VM aracısı ve uzantısı framework'ün bir VM içinde hello Azure VM uzantısı galerisinde kullanılabilir yazılım uygulamaları tooallow yüklemesini olur. tooallow (durumlarda hello Azure Monitoring uzantısı SAP gibi) bu kavramı arkasında fikirdir ilkesine Merhaba, bu tür bir yazılım dağıtım zamanında bir VM ve hello yapılandırmasını özel işlevsellik dağıtımını hello.

belirli Azure VM uzantıları VM hello Azure portal de VM oluşturmayı varsayılan olarak Windows VM'ler eklenen hello içinde işlenmesini sağlar ' Azure VM aracısının' Hello. SUSE, Red Hat veya Oracle Linux durumunda hello VM Aracısı zaten Azure Market görüntüsü parçasıdır. Linux VM'den karşıya durumda şirket içi tooAzure hello VM Aracısı el ile yüklenen toobe sahiptir.

SAP şöyle için azure'da hello izleme çözümünün temel yapı taşlarının hello:

![Microsoft Azure uzantısı bileşenleri][planning-guide-figure-2400]

Merhaba blok Yukarıdaki diyagramda gösterildiği gibi bir izleme çözümü için SAP hello parçası hello Azure VM görüntüsü ve Azure işlemleri tarafından yönetilen bir genel çoğaltılan depo Azure uzantısı galerisinde barındırılır. Bunu hello hello Azure SAP toowork uygulamasıyla Azure işlemleri toopublish yeni sürümlerini hello Azure Monitoring uzantısı SAP için çalışan hello birleşik SAP/MS takım sorumluluğundadır.

Yeni bir Windows VM dağıttığınızda, hello 'Azure VM Aracısı' hello VM otomatik olarak eklenir. Merhaba bu aracının toocoordinate hello yükleme ve yapılandırmasını hello Azure uzantıları SAP NetWeaver sistemlerinin izlenmesi için işlevdir. Linux VM'ler için hello Azure VM Aracısı hello Azure Market işletim sistemi görüntüsünün parçası zaten var.

Ancak, halen hello müşteri tarafından yürütülen toobe gereken bir adım yoktur. Merhaba etkinleştirme ve yapılandırma hello performans koleksiyonunun budur. Merhaba işlem toohello 'configuration' bir PowerShell komut dosyası veya CLI komutu tarafından otomatik olarak ilgili. Merhaba PowerShell Betiği hello açıklandığı gibi hello Microsoft Azure Script Center indirilebilir [Dağıtım Kılavuzu'na][deployment-guide].

Merhaba hello genel mimarisi için SAP izleme çözümü Azure şuna benzer:

![SAP NetWeaver için izleme çözümü azure][planning-guide-figure-2500]

**Merhaba tam nasıl-tooand için dağıtımları sırasında bu PowerShell cmdlet'lerini veya CLI komutunu kullanarak, ayrıntılı adımlar için hello verilen hello yönergeleri [Dağıtım Kılavuzu'na][deployment-guide].**

### <a name="integration-of-azure-located-sap-instance-into-saprouter"></a>Azure tümleştirilmesi SAProuter SAP örneğine bulunan
Azure'da çalışan SAP örnekleri toobe SAProuter erişilebilir de gerekir.

![SAP yönlendirici ağ bağlantısı][planning-guide-figure-2600]

Bir SAProuter hello TCP/IP'yi sistemleri arasındaki iletişimi doğrudan IP bağlantısı yoksa katılımcı sağlar. Bu, uçtan uca bağlantı hello iletişimi iş ortakları arasında ağ düzeyinde gerekli olduğunu hello avantajı sağlar. Merhaba SAProuter varsayılan 3299 numaralı bağlantı noktasında dinliyor.
tooconnect SAP örnekleri SAProuter toogive hello SAProuter dize ve ana bilgisayar adına sahip tüm girişimi tooconnect gerekir.

## <a name="sap-netweaver-as-java"></a>SAP NetWeaver AS Java
Şu ana kadar hello odak hello belgenin SAP NetWeaver genel yanıtlandı veya SAP NetWeaver ABAP yığını hello. Bu küçük bölümünde hello SAP Java yığını için belirli konuları listelenmiştir. SAP NetWeaver Java özel olarak tabanlı uygulamaları en önemli hello hello SAP Enterprise Portal biridir. SAP PI ve SAP çözüm Manager hello SAP NetWeaver ABAP ve Java yığınları kullanmak gibi diğer SAP NetWeaver tabanlı uygulamaları. Bu nedenle, kesinlikle yoktur gerek tooconsider belirli yönlerini ilgili toohello SAP NetWeaver Java yığın de.

### <a name="sap-enterprise-portal"></a>SAP Enterprise Portal
Şirket içi senaryolarda dağıtıyorsanız hello Kurulum SAP portalı bir Azure sanal makine üzerinde bir şirket içi yüklemesinden farklı değildir. DNS şirket tarafından yapılır hello itibaren başlangıç bağlantı noktası ayarlarını hello ayrı ayrı örnekleri yapılandırılmış şirket içi yapılabilir. Merhaba önerileri ve şu ana kadar bu belgede açıklanan kısıtlamaları SAP Enterprise Portal veya hello SAP NetWeaver Java yığını gibi bir uygulama için genel olarak uygulanır.

![Sunulan SAP portalı][planning-guide-figure-2700]

Siteden siteye VPN tüneli ya da ExpressRoute aracılığıyla şirket ağına bağlı toohello olsa da Hello sanal makine konağı bir özel dağıtım bazı müşteriler tarafından hello doğrudan hello SAP Enterprise Portal toohello Internet riskini senaryodur. Böyle bir senaryo için belirli bağlantı noktalarını açın ve güvenlik duvarı veya ağ güvenlik grubu tarafından engellenmediğinden emin toomake sahip. Merhaba aynı mekanizması tooconnect tooan SAP Java şirket içi bir yalnızca bulut senaryosunda örneğinden istediğinizde uygulanan toobe gerekir.

Merhaba ilk URI portalıdır http (s):`<Portalserver`>: 5XX00/irj burada hello bağlantı noktası biçimlendirilmiş 50000 tarafından artı (Systemnumber × 100). Merhaba varsayılan portal URI, SAP 00 sistemidir `<dns name`>.`<azure region` >.Cloudapp.azure.com:PublicPort/irj. Daha fazla ayrıntı için göz atın sahip <http://help.sap.com/saphelp_nw70ehp1/helpdata/de/a2/f9d7fed2adc340ab462ae159d19509/frameset.htm>.

![Uç nokta yapılandırması][planning-guide-figure-2800]

Toocustomize hello URL ve/veya bağlantı noktaları, SAP Enterprise Portal'ın istiyorsanız, bu belgeleri gözden geçirin:

* [Değişiklik portalı URL'si](http://wiki.scn.sap.com/wiki/display/EP/Change+Portal+URL)
* [Varsayılan bağlantı noktası numaralarını, Portal bağlantı noktası numaralarını değiştirme](http://wiki.scn.sap.com/wiki/display/NWTech/Change+Default++port+numbers%2C+Portal+port+numbers)

## <a name="high-availability-ha-and-disaster-recovery-dr-for-sap-netweaver-running-on-azure-virtual-machines"></a>Yüksek kullanılabilirlik (HA) ve Azure sanal makinelerde çalışan SAP NetWeaver için olağanüstü durum kurtarma (DR)
### <a name="definition-of-terminologies"></a>Terimler tanımı
Merhaba terim **yüksek kullanılabilirlik (HA)** genellikle ilgili tooa iş sürekliliği BT hizmetlerinin yoluyla sağlayarak BT kesintilerini en aza indiren teknoloji ayarlanmış yedekli, hataya dayanıklı veya yük devretme korumalı bileşenleri Merhaba içinde **aynı** veri merkezi. Örneğimizde, içinde bir Azure bölgesi.

**Olağanüstü Durum Kurtarma (DR)** BT Hizmetleri kesintiyi en aza indirmenizi ve bunların kurtarma ayrıca ancak çapraz hedeflediği **farklı** genellikle veri merkezleri, yüzlerce kilometre uzakta bulunur. Bu örnekte genellikle hello içinde farklı Azure bölgeler arasında aynı coğrafi bölge veya sizin tarafınızdan bir müşteri olarak belirlenen.

### <a name="overview-of-high-availability"></a>Yüksek kullanılabilirlik genel bakış
Biz SAP iki kısma azure'da yüksek kullanılabilirlik hakkında hello tartışma ayırabilirsiniz:

* **Azure altyapı yüksek kullanılabilirlik**, örneğin HA (VM) işlem, ağ, depolama vb. ve onun avantajlarını SAP uygulama kullanılabilirliği artırma için.
* **SAP uygulama yüksek kullanılabilirlik**, örneğin HA, SAP yazılım bileşenleri:
  * SAP uygulama sunucuları
  * SAP ASCS/SCS örneği
  * Veritabanı sunucusu

ve Azure altyapı HA nasıl birleştirilebilir.

Azure SAP yüksek kullanılabilirlik, bir şirket içi fiziksel veya sanal ortamda bazı karşılaştırıldığında fark tooSAP yüksek kullanılabilirlik sahiptir. Merhaba aşağıdaki kağıt SAP kullanılarak açıklar Windows sanallaştırılmış ortamlarda standart SAP yüksek kullanılabilirlik yapılandırmaları: <http://scn.sap.com/docs/DOC-44415>. Windows için mevcut değil gibi sapinst tümleşik SAP-HA için yapılandırmaya Linux yoktur. SAP HA ile ilgili şirket içi Linux için daha fazla bilgi burada bulabilirsiniz: <http://scn.sap.com/docs/DOC-8541>.

### <a name="azure-infrastructure-high-availability"></a>Azure altyapı yüksek kullanılabilirlik
Şu anda bir tek VM SLA % 99,9. tooget hakkında bir fikir hello çarpımını yalnızca oluşturabilirsiniz gibi tek bir VM'ye hello kullanılabilirliğini görünebilir nasıl farklı kullanılabilir Azure SLA hello: <https://azure.microsoft.com/support/legal/sla/>.

Merhaba hello hesaplama 30 gün içinde her ay veya 43200 dakika temelini oluşturur. Bu nedenle, %0,05 kapalı kalma süresi too21.6 karşılık gelen dakika. Her zamanki gibi hello hello farklı hizmetlerin kullanılabilirliğini yolu izleyerek hello çarpın:

(Kullanılabilirlik hizmeti #1/100) * (kullanılabilirlik hizmeti #2/100) * (kullanılabilirlik hizmeti #3/100) *...

Benzer:

(99,95/100) * (99,9/100) * (99,9/100) = 0.9975 veya %99.75 genel kullanılabilirlik.

#### <a name="virtual-machine-vm-high-availability"></a>Sanal makine (VM) yüksek kullanılabilirlik
İki tür sanal makinelerinizi hello kullanılabilirliğini etkileyebilecek Azure platformu olay vardır: planlanan Bakım ve planlanmayan Bakım.

* Planlı bakım olaylardır Azure platformu tooimprove temel Microsoft toohello tarafından yapılan düzenli güncelleştirmeler genel güvenilirliğini, performansını ve sanal makinelerinizi çalıştıracağınız hello platform altyapısına güvenliğini.
* Plansız bakım olayları Hello donanım ya da sanal makineniz için temel alınan fiziksel altyapı herhangi bir yolla hatalı oluşur. Buna yerel ağ hataları, yerel disk hataları veya raf düzeyinde diğer hatalar dahildir. Bu tür bir arıza tespit edildiğinde hello Azure platformu, sanal makine, sanal makine tooa sağlıklı fiziksel sunucu barındırma hello sağlıksız fiziksel sunucudan otomatik olarak geçirin. Bu gibi olaylar ender olsa da, sanal makine tooreboot da neden olabilir.

Bu belgede daha fazla ayrıntı bulunabilir: <http://azure.microsoft.com/documentation/articles/virtual-machines-manage-availability>

#### <a name="azure-storage-redundancy"></a>Azure depolama artıklığı
Merhaba Microsoft Azure depolama hesabınızdaki her zaman çoğaltılmış tooensure dayanıklılık ve yüksek kullanılabilirlik, hello Azure depolama SLA bile geçici donanım arızalarında hello yüzünü toplantı verilerdir.

Azure Storage üç görüntüleri hello verilerin varsayılan olarak engelliyor olduğundan, RAID5 veya birden çok Azure disklere RAID1 yok gerekli.

Bu makalede daha fazla ayrıntı bulunabilir: <http://azure.microsoft.com/documentation/articles/storage-redundancy/>

#### <a name="utilizing-azure-infrastructure-vm-restart-tooachieve-higher-availability-of-sap-applications"></a>Azure VM Altyapı yeniden tooAchieve "Daha yüksek kullanılabilirliğini" SAP uygulamaları kullanma
Değil toouse işlevler Windows Server Yük Devretme Kümelemesi (WSFC) veya Linux'ta Pacemaker gibi karar verirseniz (şu anda SLES 12 ve daha yüksek yalnızca desteklenir), Azure VM yeniden başlatma olduğundan kullanılan tooprotect SAP sistemine karşı Merhaba, planlanmış ve Planlanmamış kapalı kalma süresi Azure fiziksel sunucu altyapısı ve genel temel Azure platformu.

> [!NOTE]
> Azure VM yeniden öncelikle VM'ler ve uygulamaları korur, önemli toomention olur. VM yeniden başlatma yok sunar SAP uygulamalar için yüksek kullanılabilirlik, ancak belirli bir düzeyde altyapı kullanılabilirlik sunar ve bu nedenle dolaylı olarak "daha yüksek kullanılabilirliğini" SAP sistemleri. Bu toorestart VM konak planlanmış veya planlanmamış kesinti sonra hello sürmesi için hiçbir SLA bulunmaktadır. Bu nedenle, bu yöntem 'yüksek oranda kullanılabilirlik' SAP sistemine (A) SCS veya DBMS gibi kritik bileşenleri için uygun değil.
>
>

Başka bir önemli altyapısı için yüksek kullanılabilirlik depolama öğesidir. Örneğin Azure depolama SLA %99,9 kullanılabilirlik olur. Varsa, disklerle tüm VM'ler tek Azure depolama hesabı, olası Azure Storage, Azure depolama hesabında yerleştirilir tüm sanal makineleri ve bu VM'lerin içinde çalışan aynı zamanda tüm SAP bileşenleri kullanılamama kullanılamazlık neden olacak içine dağıtır.  

Tüm sanal makineleri tek tek Azure Storage hesabınıza yerine koyma, ayrılmış bir depolama de kullanabilirsiniz hesapları her VM için ve bu şekilde, birden çok bağımsız Azure depolama hesapları kullanarak genel VM ve SAP uygulama kullanılabilirliği artırın.

Azure yönetilen diskleri hello hata etki alanı için bağlı hello sanal makinenin otomatik olarak yerleştirilir. Yerleştirdiğiniz iki sanal makine bir kullanılabilirlik kümesi ve yönetilen diskleri kullanın, hello platform farklı hata etki alanlarına da hello yönetilen diskleri dağıtma ilgilenebilmek. Premium depolama toouse planlıyorsanız, diskleri yönetme de kullanarak önerilir.

Azure altyapı HA ve depolama hesapları kullanan bir SAP NetWeaver sisteminin örnek mimarisi şöyle:

![Azure altyapı HA tooachieve SAP uygulaması "daha yüksek" kullanılabilirlik kullanma][planning-guide-figure-2900]

Azure altyapı HA ve yönetilen diskleri kullanan bir SAP NetWeaver sisteminin örnek mimarisi şöyle:

![Azure altyapı HA tooachieve SAP uygulaması "daha yüksek" kullanılabilirlik kullanma][planning-guide-figure-2901]

İçin kritik SAP bileşenleri hello kadarki aşağıdaki elde:

* SAP uygulama sunucuları (AS) yüksek kullanılabilirlik

  SAP uygulama sunucu örnekleri yedekli bileşenleridir. Her SAP örneği farklı bir Azure hata ve yükseltme etki alanında çalışan kendi VM üzerinde dağıtıldığında (bölümlere bakın [hata etki alanlarını] [ planning-guide-3.2.1] ve [yükseltme etki alanları][planning-guide-3.2.2]). Bu Azure kullanılabilirlik kümeleri kullanarak sağlamış (bölüm bkz [Azure kullanılabilirlik kümeleri][planning-guide-3.2.3]). Olası planlanmış veya planlanmamış kullanılamama Azure hatası veya yükseltme etki alanı kendi SAP AS VM'ler sınırlı sayıda kullanılamama neden olacak örnekleri.

  Örnek, kendi Azure depolama hesabında yerleştirilir – bir Azure depolama hesabı potansiyel olarak kullanım dışı kalması kendi SAP AS ile yalnızca bir VM kullanılamama neden olacak şekilde her SAP örneği. Ancak, bir Azure depolama hesapları sınırı içinde bir Azure aboneliği olduğunu unutmayın. tooensure hello VM yeniden başlatıldıktan sonra (A) SCS örneği otomatik olarak Başlat tooset hello Autostart (A) SCS örneği parametresinde Başlat bölümde açıklanan profili emin olun [SAP örnekleri için Otomatik Başlat'ı kullanarak] [ planning-guide-11.5].
  Lütfen bölüm okuyun [SAP uygulama sunucuları için yüksek kullanılabilirlik] [ planning-guide-11.4.1] daha fazla ayrıntı için.

  Yönetilen diskleri kullansanız bile, bu diskler ayrıca bir Azure depolama hesabında depolanır ve bir depolama kesinti bir olayda kullanılamıyor olabilir.

* *Daha yüksek* SAP kullanılabilirlik (A) SCS örneği

  Burada size Azure VM yeniden tooprotect hello VM yüklü SAP (A) SCS örneğiyle kullanın. Hello Azure planlanmış veya Planlanmamış kapalı kalma süresi durumunun sunucularının, sanal makineleri başka bir kullanılabilir sunucusunda yeniden başlatılacak. Daha önce belirtildiği gibi Azure VM yeniden öncelikle VM'ler ve uygulamaları korur, (A) SCS örneği bu durumda hello. Merhaba VM yeniden biz dolaylı olarak SAP (A) SCS örneğinin "daha yüksek kullanılabilirlik" ulaşması. tooinsure hello VM yeniden başlatıldıktan sonra (A) SCS örneği otomatik olarak Başlat tooset Autostart parametre (A) SCS örneğinde Başlat bölümde açıklanan profili emin olun [SAP örnekleri için Otomatik Başlat'ı kullanarak][planning-guide-11.5]. Bu, tek bir VM'de çalıştıran hello (A) SCS örneği bir tek hata noktası (SPOF) olarak hello tüm SAP yatay hello kullanılabilirliğini determinative çarpanını hello anlamına gelir.

* *Daha yüksek* DBMS sunucu kullanılabilirliği

  Burada, benzer toohello SAP (A) SCS örnek kullanım örneği, size Azure VM yeniden tooprotect hello VM yüklü DBMS yazılımıyla kullanmak ve biz "daha yüksek kullanılabilirliğini" DBMS yazılım VM yeniden aracılığıyla elde etmek.
  Tek bir VM'de çalıştıran DBMS ayrıca bir SPOF ve hello tüm SAP yatay hello kullanılabilirliğini determinative çarpanını hello şeklindedir.

### <a name="sap-application-high-availability-on-azure-iaas"></a>SAP Azure Iaas uygulama yüksek kullanılabilirlik
tooachieve tam SAP sistem yüksek kullanılabilirlik, ihtiyacımız tooprotect örnek yedekli SAP uygulama sunucuları için tüm kritik SAP sistemi bileşenleri ve SAP (A) SCS örneği ve DBMS gibi benzersiz bileşenler (örneğin tek hata noktası).

#### <a name="5d9d36f9-9058-435d-8367-5ad05f00de77"></a>SAP uygulama sunucuları için yüksek kullanılabilirlik
Merhaba SAP uygulama sunucuları/iletişim örnekleri için belirli yüksek kullanılabilirlik çözümü hakkında gerekli toothink değil. Yüksek kullanılabilirlik artıklık ve böylece yalnızca elde yeterli bunlardan farklı sanal makinelere sahip. Bunlar tüm VM'ler hello aynı Azure kullanılabilirlik kümesi tooavoid hello güncelleştirilmiş hello yerleştirilmelidir planlı bakım kapalı kalma süresi sırasında aynı anda. farklı yükseltme ve hata etki alanı içinde bir Azure ölçek birimi hello temel işlevselliği bölümde zaten sunulmuştur [yükseltme etki alanları][planning-guide-3.2.2]. Azure kullanılabilirlik kümeleri bölümde sunulan [Azure kullanılabilirlik kümeleri] [ planning-guide-3.2.3] bu belgenin.

Hiçbir sonsuz sayıda hata ve yükseltme Azure ölçek birimi içinde Azure kullanılabilirlik kümesi tarafından kullanılan etki alanları yoktur. Bu, bir kullanılabilirlik kümesine VM'lerin sayısını koyma, er geç birden fazla VM hello aynı hatası veya yükseltme etki alanı sona eriyor, anlamına gelir.

Örnekleri kendi özel VM'ler birkaç SAP uygulama sunucusu dağıtma ve biz beş yükseltme etki alanları var olduğunu varsayarsak resim aşağıdaki hello hello sonunda ortaya çıkar. Hello gerçek max arıza ve güncelleştirme etki alanlarının sayısı bir kullanılabilirlik kümesi içinde hello gelecekteki değiştirebilirsiniz:

![HA azure'da SAP uygulama sunucuları][planning-guide-figure-3000]

Bu belgede daha fazla ayrıntı bulunabilir: <http://azure.microsoft.com/documentation/articles/virtual-machines-manage-availability>

#### <a name="high-availability-for-hello-sap-ascs-instance-on-windows"></a>Yüksek kullanılabilirlik için Windows hello SAP (A) SCS örneği
Windows Server Yük devretme kümesi (WSFC) bir sık kullanılan çözüm tooprotect hello SAP (A) SCS örneğidir. Ayrıca, bir "HA yükleme" biçiminde sapinst içine tümleşiktir. Bu anda hello Azure altyapı mümkün tooprovide hello işlevselliği tooset aynı şekilde gerçekleştirilir gibi şirket içi hello gerekli Windows Server Yük devretme hello yedeklemek değildir.

Ocak 2016 itibariyle hello Azure bulut platformu hello Windows işletim sistemi çalıştıran bir Küme Paylaşılan birimi iki Azure VM'ler arasında paylaşılan bir disk kullanarak hello olasılığını sağlamaz.

Geçerli bir çözüm ancak hello WSFC tümleştirilebilir zaman uyumlu ve saydam disk çoğaltma tarafından paylaşılan bir birim sağlayan 3. taraf yazılımların kullanımdır. Bu yaklaşım, yalnızca o hello etkin küme düğümünde hello disk birini zamanında bir noktada kopyalar mümkün tooaccess olduğu anlamına gelir. Bu HA Ocak 2016 itibariyle desteklenen tooprotect hello SAP (A) SCS SIOS DataKeeper 3. taraf yazılımlarla birlikte Windows konuk işletim sistemi Azure vm'lerinde örneğinde yapılandırmadır.

Merhaba SIOS DataKeeper çözüm sağlayarak bir paylaşılan disk küme kaynak tooWindows yük devretme kümeleri sağlar:

* Windows küme yapılandırmasında olan hello sanal makineleri (VM'ler) tooeach bağlı ek bir Azure VHD
* Her iki VM düğümler üzerinde çalışan SIOS DataKeeper Cluster Edition
* SIOS DataKeeper Cluster Edition, zaman uyumlu olarak hello ek Merhaba içeriğine yansıtan bir şekilde yapılandırılmış olan VHD kaynak VM'ler tooadditional bağlı VHD birimden hedef VM birim eklendi.
* SIOS DataKeeper hello kaynak ve hedef yerel birimleri özetleyen ve yük devretme kümesi olarak tek bir paylaşılan disk tooWindows sunma.

Tüm ayrıntılar hakkında yönergeler bulabilirsiniz tooinstall SIOS DataKeeper ve SAP ile Windows Yük devretme hello içinde [SAP ASCS SIOS DataKeeper ile azure'da Windows Server Yük devretme kullanarak örneğini Kümeleme] [ ha-guide-classic]teknik incelemesi.

#### <a name="high-availability-for-hello-sap-ascs-instance-on-linux"></a>Linux hello SAP (A) SCS örneği için yüksek kullanılabilirlik
DEC 2015'ten itibaren ayrıca Azure Linux VM'ler için WSFC eşdeğer tooshared disk yok. Alternatif çözümleri için SIOS Windows gibi 3. taraf yazılım kullanarak SAP Linux Azure üzerinde çalışan için henüz doğrulanmaz.

#### <a name="high-availability-for-hello-sap-database-instance"></a>Merhaba SAP veritabanı örneği için yüksek kullanılabilirlik
Merhaba normal SAP DBMS HA Kurulum iki DBMS Vm'lerde DBMS yüksek kullanılabilirlik işlevselliğini kullanıldığı dayanır hello etkin DBMS örneği toohello tooreplicate verilerden bir pasif DBMS örneğine VM ikinci.

Yüksek kullanılabilirlik ve olağanüstü durum kurtarma işlevi için genel yanı sıra belirli DBMS DBMS hello açıklanan [DBMS Dağıtım Kılavuzu'na][dbms-guide].

#### <a name="end-to-end-high-availability-for-hello-complete-sap-system"></a>Uçtan uca yüksek kullanılabilirlik için hello tam SAP sistem
Bir tam SAP NetWeaver HA mimarisinde Azure - iki örnekleri şunlardır biri Windows ve Linux için bir tane.

Yönetilmeyen yalnızca diskler: aşağıda açıklandığı gibi hello kavramları biraz hello dağıtılan VM sayısı hello abonelik başına depolama hesaplarının maksimum sınırı aşan ve birçok SAP sistemi dağıttığınızda tehlikeye toobe gerekebilir. Böyle durumlarda, sanal makineleri VHD'ler bir depolama hesabında birleştirilmiş toobe gerekir. Genellikle VHD'ler, SAP uygulama katmanı farklı SAP sistemlerinin VM'ler birleştirerek bunu.  Biz de bir Azure depolama hesabında farklı SAP sistemlerinin farklı DBMS VM'ler farklı VHD'leri birleşik. Böylece Azure depolama hesapları hello IOPS sınırları göz önünde bulundurarak (<https://azure.microsoft.com/documentation/articles/storage-scalability-targets>)


##### <a name="windowslogowindows-ha-on-windows"></a>![Windows][Logo_Windows] HA Windows
![Azure Iaas SQL Server ile SAP NetWeaver uygulama HA mimarisi][planning-guide-figure-3200]

Azure yapıları aşağıdaki hello hello SAP NetWeaver sistemi toominimize etkisi altyapı sorunları ve düzeltme eki uygulama ana bilgisayar için kullanılır:

* Merhaba tam sistem (gerekli - DBMS katman, (A) SCS örneği ve tam uygulama katmanı gerek toorun aynı konuma hello) Azure üzerinde dağıtılır.
* Merhaba tam sistem (gerekli) bir Azure aboneliği içinde çalışır.
* Merhaba tam sistem bir Azure sanal (gerekli) ağ içinde çalışır.
* Merhaba hello VM'ler bir SAP sisteminin üç kullanılabilirlik kümeleri içine ayrılmasıdır olası toohello ait bile tüm hello VM'ler ile aynı sanal ağ.
* Bir SAP sistem DBMS örneklerini çalışan tüm sanal makineler, bir kullanılabilirlik kümesinde ' dir. SQL Server AlwaysOn veya Oracle Data Guard gibi özellikleri kullanılır, yerel DBMS yüksek kullanılabilirlik bu yana sistem başına DBMS örneği çalıştıran birden fazla VM olduğunu varsayalım.
* DBMS örnekleri çalışan tüm sanal makineler kendi depolama hesabı kullanın. DBMS veri ve günlük dosyaları hello verileri eşitlemek DBMS yüksek kullanılabilirlik işlevler kullanılarak bir depolama hesabı tooanother depolama hesabından çoğaltılır. Bir depolama hesabı olarak kullanım dışı kalması bir SQL Windows Küme düğümü ancak hello tüm SQL Server hizmeti değil kullanılamama neden olur.
* (A) bir SAP sistem SCS örneğini çalışan tüm sanal makineler, bir kullanılabilirlik kümesinde ' dir. Bir Windows Server Yük devretme kümesi (WSFC) bu sanal makineleri tooprotect hello (A) SCS örneği içinde yapılandırılır.
* (A) SCS örnekleri çalışan tüm sanal makineler kendi depolama hesabı kullanın. (A) SCS örnek dosyaları ve SAP genel klasör SIOS DataKeeper çoğaltma'yı kullanarak bir depolama hesabı tooanother depolama hesabından çoğaltılır. Bir depolama hesabı olarak kullanım dışı kalması biri (A) kullanılamama neden olacak SCS Windows Küme düğümü, ancak tüm hello değil (A) SCS hizmet.
* Merhaba SAP uygulama sunucusu katmanı temsil eden tüm hello VM'ler, bir üçüncü kullanılabilirlik kümesinde ' dir.
* SAP uygulama sunucuları çalışan tüm hello sanal makineler kendi depolama hesabı kullanın. Bir depolama hesabı olarak kullanım dışı kalması burada diğer SAP AS devam toorun bir SAP uygulama sunucusu olarak kullanım dışı kalması neden olur.

Merhaba aşağıdaki aynı yönetilen diskleri kullanarak yatay Resimli hello tahmin edin.

![Azure Iaas SQL Server ile SAP NetWeaver uygulama HA mimarisi][planning-guide-figure-3201]

##### <a name="linuxlogolinux-ha-on-linux"></a>![Linux][Logo_Linux] HA Linux
Hello için SAP HA Linux Azure üzerinde temelde aynı Windows yukarıda açıklanan hello mimarisidir. Ocak 2016 itibariyle henüz Linux Azure üzerinde desteklenen SAP (A) SCS HA çözümü yoktur

Sonuç olarak Ocak 2016 SAP Linux Azure sistem alamayacağınız gibi HA hello (A) SCS örnek için eksik bir SAP Windows Azure sistemi olarak aynı kullanılabilirlik hello ve tek örnekli SAP ana veritabanı hello.

### <a name="4e165b58-74ca-474f-a7f4-5e695a93204f"></a>SAP örnekleri için Otomatik Başlat'ı kullanma
SAP hello OS hello VM içinde hello başlangıcı hemen sonra toostart SAP örnekleri hello işlevsellik sunmazdı. Merhaba tam adımlar SAP Bilgi Bankası makalesinde belgelenmiş [1909114]. Ancak, SAP hello örneği yeniden başlatıldığında, sırayla hiçbir denetim olduğundan toouse hello artık ayarı VM başına birden çok örneği çalıştırdığınızda veya birden fazla VM etkilenen olduğu varsayılarak öneren değil. Bir süre sonra yeniden tek bir VM VM ve hello durumda bir SAP uygulama sunucusu örneği tipik Azure senaryosunu varsayıldığında, hello Autostart gerçekten kritik değildir ve bu parametre ekleyerek etkinleştirilebilir:

    Autostart = 1

Hello profil hello SAP ABAP ve/veya Java örneğinin başlatın.

> [!NOTE]
> Merhaba Autostart parametre bazı downfalls de sahip olabilir. Merhaba hello örneğinin Windows/Linux hizmeti başlatıldı işlerken daha ayrıntılı olarak hello parametre Tetikleyicileri SAP ABAP veya Java örneği başlangıcı hello. Merhaba işletim sistemi önyüklendiğinde, kesinlikle hello durumdur. Ancak, SAP hizmetleri yeniden de SUM gibi SAP yazılım yaşam döngüsü yönetimi işlevleri için ortak bir şey diğer güncelleştirir veya veya yükseltir. Bu işlevler hiç otomatik olarak yeniden örneği toobe beklenmiyor. Bu nedenle, hello Autostart parametresi gibi görevleri çalıştırmadan önce devre dışı bırakılması gerekir. Merhaba Autostart parametresi SCS/ASCS/CI gibi kümelenir SAP örnekleri için de kullanılmamalıdır.
>
>

SAP için autostart'ile ilgili ek bilgiler burada örnekleri bakın:

* [Başlat/Durdur SAP yanı sıra, UNIX sunucusu Başlat/Durdur](http://scn.sap.com/community/unix/blog/2012/08/07/startstop-sap-along-with-your-unix-server-startstop)
* [Başlatma ve durdurma SAP NetWeaver yönetim aracıları](https://help.sap.com/saphelp_nwpi711/helpdata/en/49/9a15525b20423ee10000000a421938/content.htm)
* [Nasıl tooenable otomatik HANA veritabanına, Başlat](http://www.freehanatutorials.com/2012/10/how-to-enable-auto-start-of-hana.html)

### <a name="larger-3-tier-sap-systems"></a>Daha büyük 3 katmanlı SAP sistemleri
3 katmanlı SAP yapılandırmaları yüksek kullanılabilirlik yönlerini zaten önceki bölümlerde ele. Ancak sistemleri hello DBMS sunucu gereksinimleri olduğu çok büyük hakkında toohave Azure'da bulunan, ancak hello SAP uygulama katmanı Azure'da dağıtılan?

#### <a name="location-of-3-tier-sap-configurations"></a>3 katmanlı SAP yapılandırmaları konumu
Şu desteklenen toosplit hello uygulama katmanı kendisini veya Merhaba uygulaması ve şirket içi ve Azure arasında DBMS katmanı değil. Ya da tamamen şirket içinde dağıtılabilir bir SAP sistemidir veya Azure'da. Bu da desteklenen toohave değil Azure'da hello uygulama sunucuları bazıları şirket içi ve diğerlerinin çalıştırın. Başlangıç noktası hello tartışma hello olmasıdır. Biz de toohave hello DBMS bir SAP sistemi bileşenlerinin desteklemediğinden ve SAP uygulama sunucusu katmanı iki farklı Azure bölgelerde dağıtılan hello. Örneğin DBMS Orta ABD, Batı ABD ve SAP uygulama katmanında. Bu tür yapılandırmaları desteklemediğinden için hello gecikme hello SAP NetWeaver mimarisi duyarlılığını nedenidir.

Ancak, geçen yıl veri hello süresince merkezi ortakları ortak konumları tooAzure bölgeler geliştirmiştir. Bu ortak konumları genellikle çok yakın bir yerde konumlandırıldığında toohello fiziksel Azure verinin bir Azure bölgesi merkezlerinizde içindedir. Merhaba kısa uzaklık ve Azure ExpressRoute aracılığıyla konuma ortak hello varlıkları bağlantı 2ms'den az kadar olan bir gecikme neden olabilir. Böyle durumlarda, bu tür bir birlikte bulundurma ve azure'da hello SAP uygulama katmanı toolocate hello DBMS katman (depolama SAN/NAS dahil) mümkündür. DEC 2015'ten itibaren biz tüm dağıtımları gibi yok. Ancak SAP olmayan uygulama dağıtımları farklı müşterilerle zaten bu yaklaşımı kullanarak.

### <a name="offline-backup-of-sap-systems"></a>Çevrimdışı Yedekleme, SAP sistemleri
Merhaba bağımlı (Katman 2 veya 3 katmanlı) var. seçilen SAP yapılandırma gereksinimini tooback yukarı olabilir. Merhaba VM kendisini artı toohave hello veritabanının bir yedeğini Hello içeriği. Merhaba DBMS ilgili yedeklemeleri veritabanı yöntemleriyle bitti beklenen toobe ' dir. Ayrıntılı bir açıklama hello farklı veritabanları için bulunabilir [DBMS Kılavuzu][dbms-guide]. Üzerindeki diğer yandan Merhaba, hello SAP veri (Merhaba veritabanı içeriği de dahil) bir çevrimdışı şekilde bu bölümde açıklandığı gibi veya çevrimiçi hello sonraki bölümde açıklandığı gibi yedeklenebilir.

Merhaba Çevrimdışı Yedekleme temelde hello VM hello Azure portal aracılığıyla bir kapatma ve hello temel VM disk artı tüm bağlı disklerde toohello VM kopyasını gerektirir. Bu, hello VM zaman görüntüdeki noktası ve onun ilişkili disk korur. Farklı bir Azure Storage hesabınıza toocopy hello 'yedeklemeleri' önerilir. Bu nedenle bölümde açıklanan yordamı hello [Azure depolama hesapları arasında diskleri kopyalama] [ planning-guide-5.4.2] bu belgenin geçerli olur.
Hello Azure kullanarak hello kapatma yanı sıra bir portal ayrıca Powershell veya CLI burada açıklandığı gibi bunu yapabilirsiniz: <https://azure.microsoft.com/documentation/articles/virtual-machines-deploy-rmtemplates-powershell/>

Bu durumda, bir geri yükleme oluşur hello silmek temel VM de hello özgün diskleri hello gibi temel VM ve bağlı diskler, geri kopyalama hello kaydedilmiş diskleri toohello özgün depolama hesabı veya kaynak grubu yönetilen diskleri ve hello sistemini yeniden dağıtmak için.
Bu makalede nasıl tooscript bu işlemi bir örnek gösterilmektedir Powershell: <http://www.westerndevs.com/azure-snapshots/>

Lütfen yukarıda açıklandığı gibi bir VM yedeğinin geri yeni bir donanım anahtarı oluşturduğundan emin tooinstall yeni bir SAP lisans olun.

### <a name="online-backup-of-an-sap-system"></a>SAP sistemin çevrimiçi yedekleme
DBMS, DBMS özgü yöntemleriyle gerçekleştirilir, hello açıklandığı gibi hello yedeklemeyi [DBMS Kılavuzu][dbms-guide].

Azure sanal makine yedekleme işlevini kullanarak diğer VM'ler hello SAP sistem içinde yedeklenebilir. Azure sanal makine yedeklemesi erken 2015'te tanıtılan ve bu arada standart yöntemi tooback tam bir Azure VM'de yukarı olur. Azure yedekleme Azure'da hello yedeklemeleri depolar ve geri yükleme bir VM'nin yeniden sağlar.

> [!NOTE]
> DEC 2015'ten itibaren VM Yedekleme kullanarak SAP için kullanılan hello benzersiz VM kimliği korumaz lisans. Bu VM yedekten yeni bir SAP lisans anahtarı yüklemesini hello VM geri gibi değerlendirilir toobe yeni bir VM gerektirdiği anlamına gelir ve yerine geçecek kaydedilmiş olan eski biri değil.
>
> ![Windows][Logo_Windows] Windows
>
> Teorik olarak, Hello DBMS sistem hello Windows VSS destekliyorsa, tutarlı bir şekilde de çalıştırma veritabanları yedeklenebilir VM'ler (birim gölge kopyası hizmeti <https://msdn.microsoft.com/library/windows/desktop/bb968832 (v=vs.85).aspx >), örneğin, SQL sunucusu yok.
> Ancak, zaman içinde nokta geri yükler veritabanları Azure VM yedeklemelerin dayalı mümkün olmayan unutmayın. Bu nedenle, Azure VM Backup kalmak yerine DBMS işlevsellikle veritabanlarının yedeklerini tooperform önerilir.
>
> Azure sanal makine yedekleme ile tanıdık tooget Lütfen başlatın burada: <https://docs.microsoft.com/azure/backup/backup-azure-vms>.
>
> Diğer olasılıklar toouse birlikte Microsoft Data Protection Manager bir Azure VM ve Azure yedekleme yedekleme/geri yükleme veritabanlarına yüklendiği. Daha fazla bilgi şurada bulunabilir: <https://docs.microsoft.com/azure/backup/backup-azure-dpm-introduction>.  
>
> ![Linux][Logo_Linux] Linux
>
> Hiçbir eşdeğer tooWindows Linux VSS yoktur. Bu nedenle yalnızca dosya tutarlı yedeklemeler olası ancak değil uygulamayla tutarlı yedeklemeler altındadır. Merhaba SAP DBMS yedekleme yapılmalıdır DBMS işlevselliğini kullanma. Merhaba hello SAP ilgili verileri içeren dosya sistemi, örneğin, burada açıklandığı gibi tar kullanarak kaydedilebilir: <http://help.sap.com/saphelp_nw70ehp2/helpdata/en/d3/c0da3ccbb04d35b186041ba6ac301f/content.htm>
>
>

### <a name="azure-as-dr-site-for-production-sap-landscapes"></a>Üretim SAP Windows'un için DR sitesi olarak Azure
Mid 2014 bu yana uzantıları toovarious bileşenleri Hyper-V, System Center ve Azure çevresinde şirket üzerinde Hyper-V tabanlı çalışan sanal makineler için DR sitesi olarak Azure hello kullanımını etkinleştirin.

Bu çözümün nasıl toodeploy olan ayrıntılı bir blog burada belgelenen: <http://blogs.msdn.com/b/saponsqlserver/archive/2014/11/19/protecting-sap-solutions-with-azure-site-recovery.aspx>.

## <a name="summary"></a>Özet
Hello Azure SAP sistemler için yüksek oranda kullanılabilirlik önemli noktalar şunlardır:

* Merhaba SAP tek hata noktası bu anda, tam olarak korunamıyor şekilde şirket içi dağıtımlarda yapılabilir gibi aynı hello. Merhaba paylaşılan Disk kümelerini henüz Azure'da hello 3 taraf yazılımları kullanmadan oluşturulamıyor, nedenidir.
* Merhaba DBMS katmanı için paylaşılan disk küme teknolojisine bağlı değildir toouse DBMS işlevselliğini gerekir. Ayrıntılar hello belgelenmiştir [DBMS Kılavuzu][dbms-guide].
* toominimize hello etkisi'hello Azure altyapısı veya ana bilgisayar bakım hata etki alanları içindeki sorunları Azure kullanılabilirlik kümeleri kullanmanız gerekir:
  * Toohave bir önerilen hello SAP uygulama katman için kullanılabilirlik kümesi.
  * Merhaba SAP DBMS katman için ayrı bir kullanılabilirlik kümesi toohave önerilir.
  * Farklı SAP sistemleri VM'ler için aynı kullanılabilirlik kümesi tooapply hello önerilmez.
  * Yönetilen toouse Premium diskleri önerilir.
* Merhaba SAP DBMS katman yedekleme amaçları doğrultusunda, lütfen hello denetleyin [DBMS Kılavuzu][dbms-guide].
* Genellikle daha hızlı tooredeploy basit iletişim örnekleri olduğundan SAP iletişim örneği yedekleme az mantıklıdır.
* Hello farklı örneklerinin tüm hello profilleri hello hello genel dizin hello SAP sistem ve onunla içeren VM yedekleme anlamlı ve Windows Yedekleme ile gerçekleştirilmelidir veya, örneğin, hedef Linux üzerinde. Hello kullanarak yukarı daha kolay tooback olun Windows Server 2008 (R2) ve Windows Server 2012 (R2) arasındaki farklar olduğundan daha yeni Windows Server sürümleri, toorun Windows konuk işletim sistemi olarak Windows Server 2012 (R2) öneririz.
