---
title: "Azure vm'lerinde – planlama ve uygulama NetWeaver aaaSAP | Microsoft Docs"
description: "Azure sanal makinelerde planlama (VM'ler) – SAP NetWeaver ve Uygulama Kılavuzu"
services: virtual-machines-windows
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 2b58a419-c892-4722-8cb6-2f8beef4430c
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 11/08/2016
ms.author: sedusch
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 53d63240760282b409f7e9412e8240689bcbcc6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sap-netweaver-on-azure-windows-virtual-machines-vms--planning-and-implementation-guide"></a>SAP NetWeaver Azure Windows sanal makinelerde (VM'ler) – planlama ve Uygulama Kılavuzu
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

[azure-cli]:../../cli-install-nodejs.md
[azure-portal]:https://portal.azure.com
[azure-ps]:/powershell/azureps-cmdlets-docs
[azure-quickstart-templates-github]:https://github.com/Azure/azure-quickstart-templates
[azure-script-ps]:https://go.microsoft.com/fwlink/p/?LinkID=395017
[azure-subscription-service-limits]:../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../azure-subscription-service-limits.md#subscription-limits

[dbms-guide]:sap-dbms-guide.md
[dbms-guide-2.1]:sap-dbms-guide.md#c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f
[dbms-guide-2.2]:sap-dbms-guide.md#c8e566f9-21b7-4457-9f7f-126036971a91
[dbms-guide-2.3]:sap-dbms-guide.md#10b041ef-c177-498a-93ed-44b3441ab152
[dbms-guide-2]:sap-dbms-guide.md#65fa79d6-a85f-47ee-890b-22e794f51a64
[dbms-guide-3]:sap-dbms-guide.md#871dfc27-e509-4222-9370-ab1de77021c3
[dbms-guide-5.5.1]:sap-dbms-guide.md#0fef0e79-d3fe-4ae2-85af-73666a6f7268
[dbms-guide-5.5.2]:sap-dbms-guide.md#f9071eff-9d72-4f47-9da4-1852d782087b
[dbms-guide-5.6]:sap-dbms-guide.md#1b353e38-21b3-4310-aeb6-a77e7c8e81c8
[dbms-guide-5.8]:sap-dbms-guide.md#9053f720-6f3b-4483-904d-15dc54141e30
[dbms-guide-5]:sap-dbms-guide.md#3264829e-075e-4d25-966e-a49dad878737
[dbms-guide-8.4.1]:sap-dbms-guide.md#b48cfe3b-48e9-4f5b-a783-1d29155bd573
[dbms-guide-8.4.2]:sap-dbms-guide.md#23c78d3b-ca5a-4e72-8a24-645d141a3f5d
[dbms-guide-8.4.3]:sap-dbms-guide.md#77cd2fbb-307e-4cbf-a65f-745553f72d2c
[dbms-guide-8.4.4]:sap-dbms-guide.md#f77c1436-9ad8-44fb-a331-8671342de818
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

[deployment-guide]:sap-deployment-guide.md
[deployment-guide-2.2]:sap-deployment-guide.md#42ee2bdb-1efc-4ec7-ab31-fe4c22769b94
[deployment-guide-3.1.2]:sap-deployment-guide.md#3688666f-281f-425b-a312-a77e7db2dfab
[deployment-guide-3.2]:sap-deployment-guide.md#db477013-9060-4602-9ad4-b0316f8bb281
[deployment-guide-3.3]:sap-deployment-guide.md#54a1fc6d-24fd-4feb-9c57-ac588a55dff2
[deployment-guide-3.4]:sap-deployment-guide.md#a9a60133-a763-4de8-8986-ac0fa33aa8c1
[deployment-guide-3]:sap-deployment-guide.md#b3253ee3-d63b-4d74-a49b-185e76c4088e
[deployment-guide-4.1]:sap-deployment-guide.md#604bcec2-8b6e-48d2-a944-61b0f5dee2f7
[deployment-guide-4.2]:sap-deployment-guide.md#7ccf6c3e-97ae-4a7a-9c75-e82c37beb18e
[deployment-guide-4.3]:sap-deployment-guide.md#31d9ecd6-b136-4c73-b61e-da4a29bbc9cc
[deployment-guide-4.4.2]:sap-deployment-guide.md#6889ff12-eaaf-4f3c-97e1-7c9edc7f7542
[deployment-guide-4.4]:sap-deployment-guide.md#c7cbb0dc-52a4-49db-8e03-83e7edc2927d
[deployment-guide-4.5.1]:sap-deployment-guide.md#987cf279-d713-4b4c-8143-6b11589bb9d4
[deployment-guide-4.5.2]:sap-deployment-guide.md#408f3779-f422-4413-82f8-c57a23b4fc2f
[deployment-guide-4.5]:sap-deployment-guide.md#d98edcd3-f2a1-49f7-b26a-07448ceb60ca
[deployment-guide-5.1]:sap-deployment-guide.md#bb61ce92-8c5c-461f-8c53-39f5e5ed91f2
[deployment-guide-5.2]:sap-deployment-guide.md#e2d592ff-b4ea-4a53-a91a-e5521edb6cd1
[deployment-guide-5.3]:sap-deployment-guide.md#fe25a7da-4e4e-4388-8907-8abc2d33cfd8

[deployment-guide-configure-monitoring-scenario-1]:sap-deployment-guide.md#ec323ac3-1de9-4c3a-b770-4ff701def65b
[deployment-guide-configure-proxy]:sap-deployment-guide.md#baccae00-6f79-4307-ade4-40292ce4e02d
[deployment-guide-figure-100]:./media/virtual-machines-shared-sap-deployment-guide/100-deploy-vm-image.png
[deployment-guide-figure-1000]:./media/virtual-machines-shared-sap-deployment-guide/1000-service-properties.png
[deployment-guide-figure-11]:sap-deployment-guide.md#figure-11
[deployment-guide-figure-1100]:./media/virtual-machines-shared-sap-deployment-guide/1100-azperflib.png
[deployment-guide-figure-1200]:./media/virtual-machines-shared-sap-deployment-guide/1200-cmd-test-login.png
[deployment-guide-figure-1300]:./media/virtual-machines-shared-sap-deployment-guide/1300-cmd-test-executed.png
[deployment-guide-figure-14]:sap-deployment-guide.md#figure-14
[deployment-guide-figure-1400]:./media/virtual-machines-shared-sap-deployment-guide/1400-azperflib-error-servicenotstarted.png
[deployment-guide-figure-300]:./media/virtual-machines-shared-sap-deployment-guide/300-deploy-private-image.png
[deployment-guide-figure-400]:./media/virtual-machines-shared-sap-deployment-guide/400-deploy-using-disk.png
[deployment-guide-figure-5]:sap-deployment-guide.md#figure-5
[deployment-guide-figure-50]:./media/virtual-machines-shared-sap-deployment-guide/50-forced-tunneling-suse.png
[deployment-guide-figure-500]:./media/virtual-machines-shared-sap-deployment-guide/500-install-powershell.png
[deployment-guide-figure-6]:sap-deployment-guide.md#figure-6
[deployment-guide-figure-600]:./media/virtual-machines-shared-sap-deployment-guide/600-powershell-version.png
[deployment-guide-figure-7]:sap-deployment-guide.md#figure-7
[deployment-guide-figure-700]:./media/virtual-machines-shared-sap-deployment-guide/700-install-powershell-installed.png
[deployment-guide-figure-760]:./media/virtual-machines-shared-sap-deployment-guide/760-azure-cli-version.png
[deployment-guide-figure-900]:./media/virtual-machines-shared-sap-deployment-guide/900-cmd-update-executed.png
[deployment-guide-figure-azure-cli-installed]:sap-deployment-guide.md#402488e5-f9bb-4b29-8063-1c5f52a892d0
[deployment-guide-figure-azure-cli-version]:sap-deployment-guide.md#0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda
[deployment-guide-install-vm-agent-windows]:sap-deployment-guide.md#b2db5c9a-a076-42c6-9835-16945868e866
[deployment-guide-troubleshooting-chapter]:sap-deployment-guide.md#564adb4f-5c95-4041-9616-6635e83a810b

[deploy-template-cli]:../../resource-group-template-deploy-cli.md
[deploy-template-portal]:../../resource-group-template-deploy-portal.md
[deploy-template-powershell]:../../resource-group-template-deploy.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:sap-get-started.md
[getting-started-dbms]:sap-get-started.md#1343ffe1-8021-4ce6-a08d-3a1553a4db82
[getting-started-deployment]:sap-get-started.md#6aadadd2-76b5-46d8-8713-e8d63630e955
[getting-started-planning]:sap-get-started.md#3da0389e-708b-4e82-b2a2-e92f132df89c

[getting-started-windows-classic]:classic/sap-get-started.mdsap-dbms-guide.md
[getting-started-windows-classic-dbms]:classic/sap-get-started.mdsap-dbms-guide.md#c5b77a14-f6b4-44e9-acab-4d28ff72a930
[getting-started-windows-classic-deployment]:classic/sap-get-started.mdsap-dbms-guide.md#f84ea6ce-bbb4-41f7-9965-34d31b0098ea
[getting-started-windows-classic-dr]:classic/sap-get-started.mdsap-dbms-guide.md#cff10b4a-01a5-4dc3-94b6-afb8e55757d3
[getting-started-windows-classic-ha-sios]:classic/sap-get-started.mdsap-dbms-guide.md#4bb7512c-0fa0-4227-9853-4004281b1037
[getting-started-windows-classic-planning]:classic/sap-get-started.mdsap-dbms-guide.md#f2a5e9d8-49e4-419e-9900-af783173481c

[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056

[ha-guide]:sap-high-availability-guide.md

[install-extension-cli]:virtual-machines-linux-enable-aem.md

[Logo_Linux]:./media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:./media/virtual-machines-shared-sap-shared/Windows.png

[msdn-set-azurermvmaemextension]:https://msdn.microsoft.com/library/azure/mt670598.aspx

[planning-guide]:sap-planning-guide.md
[planning-guide-1.2]:sap-planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff
[planning-guide-11.4]:sap-planning-guide.md#7cf991a1-badd-40a9-944e-7baae842a058
[planning-guide-11.4.1]:sap-planning-guide.md#5d9d36f9-9058-435d-8367-5ad05f00de77
[planning-guide-11.5]:sap-planning-guide.md#4e165b58-74ca-474f-a7f4-5e695a93204f
[planning-guide-2.1]:sap-planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803
[planning-guide-2.2]:sap-planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10
[planning-guide-3.1]:sap-planning-guide.md#be80d1b9-a463-4845-bd35-f4cebdb5424a
[planning-guide-3.2.1]:sap-planning-guide.md#df49dc09-141b-4f34-a4a2-990913b30358
[planning-guide-3.2.2]:sap-planning-guide.md#fc1ac8b2-e54a-487c-8581-d3cc6625e560
[planning-guide-3.2.3]:sap-planning-guide.md#18810088-f9be-4c97-958a-27996255c665
[planning-guide-3.2]:sap-planning-guide.md#8d8ad4b8-6093-4b91-ac36-ea56d80dbf77
[planning-guide-3.3.2]:sap-planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92
[planning-guide-5.1.1]:sap-planning-guide.md#4d175f1b-7353-4137-9d2f-817683c26e53
[planning-guide-5.1.2]:sap-planning-guide.md#e18f7839-c0e2-4385-b1e6-4538453a285c
[planning-guide-5.2.1]:sap-planning-guide.md#1b287330-944b-495d-9ea7-94b83aff73ef
[planning-guide-5.2.2]:sap-planning-guide.md#57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3
[planning-guide-5.2]:sap-planning-guide.md#6ffb9f41-a292-40bf-9e70-8204448559e7
[planning-guide-5.3.1]:sap-planning-guide.md#6e835de8-40b1-4b71-9f18-d45b20959b79
[planning-guide-5.3.2]:sap-planning-guide.md#a43e40e6-1acc-4633-9816-8f095d5a7b6a
[planning-guide-5.4.2]:sap-planning-guide.md#9789b076-2011-4afa-b2fe-b07a8aba58a1
[planning-guide-5.5.1]:sap-planning-guide.md#4efec401-91e0-40c0-8e64-f2dceadff646
[planning-guide-5.5.3]:sap-planning-guide.md#17e0d543-7e8c-4160-a7da-dd7117a1ad9d
[planning-guide-7.1]:sap-planning-guide.md#3e9c3690-da67-421a-bc3f-12c520d99a30
[planning-guide-7]:sap-planning-guide.md#96a77628-a05e-475d-9df3-fb82217e8f14
[planning-guide-9.1]:sap-planning-guide.md#6f0a47f3-a289-4090-a053-2521618a28c3
[planning-guide-azure-premium-storage]:sap-planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92

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
[planning-guide-microsoft-azure-networking]:sap-planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:sap-planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f

[powershell-install-configure]:/powershell/azureps-cmdlets-docs
[resource-group-authoring-templates]:../../resource-group-authoring-templates.md
[resource-group-overview]:../../azure-resource-manager/resource-group-overview.md
[resource-groups-networking]:../../virtual-network/resource-groups-networking.md
[sap-pam]:https://support.sap.com/pam
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
[virtual-machines-linux-cli-deploy-templates]:../linux/cli-deploy-templates.md
[virtual-machines-deploy-rmtemplates-powershell]:../virtual-machines-windows-ps-manage.md
[virtual-machines-linux-agent-user-guide]:../linux/agent-user-guide.md
[virtual-machines-linux-agent-user-guide-command-line-options]:../linux/agent-user-guide.md#command-line-options
[virtual-machines-linux-capture-image]:../linux/capture-image.md
[virtual-machines-linux-capture-image-capture]:../linux/capture-image.md#step-2-create-vm-image
[virtual-machines-windows-capture-image]:../virtual-machines-windows-create-vm-generalized.md
[virtual-machines-windows-capture-image-prepare-the-vm-for-image-capture]:../virtual-machines-windows-create-vm-generalized.md
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

Microsoft Azure, uzun tedarik döngüleri olmadan en az sürede şirketler tooacquire işlem ve depolama kaynaklarını sağlar. Azure sanal makineleri SAP NetWeaver Azure uygulamalara dayalı gibi şirketler toodeploy Klasik uygulamaları izin verir ve daha fazla kaynak kullanılabilir şirket içi gerek kalmadan, güvenilirlik ve kullanılabilirlik genişletme. Azure sanal makine hizmetleri de şirket içi bağlantılar, hangi etkinleştirir şirketler tooactively tümleştirmek Azure sanal makineler kendi şirket içi etki alanlarına, kendi özel Bulutlar ve bunların SAP sistem yatay destekler.
Bu teknik incelemede hello temelleri Microsoft Azure sanal makinesi açıklar ve Azure SAP NetWeaver yüklemeleri için planlama ve uygulama ile ilgili bir kılavuz sağlar ve bu nedenle hello belge tooread başlatmadan önce olmalıdır SAP NetWeaver Azure ile ilgili gerçek dağıtımları.
Merhaba kağıt hazırlandı hello SAP yükleme belgelerini ve yüklemeleri ve SAP yazılımı dağıtımları için hello birincil kaynakları temsil eden SAP Notlar platformları verilir.

## <a name="summary"></a>Özet
Bulut bilgi işlem, daha da fazla önem hello BT endüstri içinde toolarge ve çokuluslu şirketler yukarı küçük şirketlerden elde yaygın olarak kullanılan bir terimdir.

Microsoft Azure hello paylaşılabilen çok sayıda yeni olanakları sunan Microsoft bulut hizmetleri platformu ' dir. Şimdi değil sınırlı tootechnical veya bütçeleme kısıtlamaları; bu nedenle müşterilerin hello bulutta bir hizmet olarak mümkün toorapidly sağlama ve devre dışı bırakma sağlama uygulamaları önerilir. Donanım altyapısını zamandan ve yatırım yapmak yerine, şirketler Merhaba uygulaması, iş süreçlerini ve onun avantajlarını müşteriler ve kullanıcılar için odaklanabilirsiniz.

Microsoft, Microsoft Azure Sanal Makine Hizmetleri ile kapsamlı bir Hizmet Olarak Altyapı (IaaS) platformu sunmaktadır. SAP NetWeaver tabanlı uygulamalar, Azure Sanal Makinelerinde (IaaS) desteklenmektedir. Bu teknik nasıl tooplan ve uygulama SAP NetWeaver Microsoft Azure içindeki seçim hello platform olarak tabanlı uygulamaları anlatmaktadır.

Merhaba kağıt kendisini iki ana yönlere odaklanır:

* Merhaba ilk bölümü SAP NetWeaver tabanlı uygulamalar için iki desteklenen dağıtım desenler Azure üzerinde anlatmaktadır. Ayrıca, Azure genel işleme aklınızda SAP dağıtımlarla de anlatmaktadır.
* Merhaba ikinci bölümü hello ilk bölümünde açıklanan uygulama hello iki farklı senaryolar ayrıntılarını kaydeder.

Ek kaynaklar için bölüm bkz [kaynakları] [ planning-guide-1.2] bu belgedeki.

### <a name="definitions-upfront"></a>Önceden tanımları
Merhaba belge boyunca aşağıdaki koşulları hello kullanacağız:

* Iaas: Hizmet olarak altyapı.
* PaaS: Hizmet olarak Platform.
* SaaS: Hizmet olarak yazılım.
* ARM: Azure Kaynak Yöneticisi
* SAP bileşen: tek tek SAP gibi bir uygulama ECC, bant genişliği, çözüm Yöneticisi veya EP'deki  SAP bileşenleri geleneksel ABAP veya Java teknolojiler ya da olmayan-tabanlı NetWeaver uygulama iş nesneleri gibi temel alabilir.
* SAP ortamı: bir veya daha fazla SAP bileşenleri tooperform geliştirme QAS, eğitim DR veya üretim gibi işletme işlevi mantıksal olarak gruplandırılır.
* SAP yatay: Bu toohello Müşteri'nin tüm SAP varlıkları başvuruyor BT yatay. Merhaba SAP yatay tüm üretim ve üretim dışı ortamlar içerir.
* SAP sistem: hello birleşimi DBMS katman ve örneğin bir SAP ERP geliştirme sistemi, SAP BW test sistemini, SAP CRM üretim sistem vb. uygulama katmanı.. Azure'da şirket içi ve Azure arasında iki Bu katmanlar toodivide olmayan dağıtımlar desteklenir. Şirket içi SAP sistem ya da bu anlamına gelir dağıtılan veya Azure'da dağıtılır. Ancak, Azure veya şirket içi SAP yatay hello farklı sistemlerini dağıtabilirsiniz. Örneğin, azure'da hello SAP CRM geliştirme ve test sistemlerini dağıtmak ancak SAP CRM üretim sistem şirket içi hello.
* Yalnızca bulut dağıtım: Burada bir site siteye hello Azure aboneliğine bağlı değil ya da ExpressRoute bağlantı toohello şirket içi ağ altyapısı dağıtımı. Ortak Azure belgelerine bu tür dağıtımlar da 'Yalnızca bulut' dağıtımları açıklanmıştır. Bu yöntem ile dağıtılan sanal makineleri yoluyla erişilir Internet hello ve atanan toohello VM'ler için Azure'da bir ortak IP adresi ve/veya ortak bir DNS adı. Şirket içi Active Directory (AD) için Microsoft Windows hello ve DNS dağıtımları bu tür tooAzure genişletilmedi. Bu nedenle hello VM'ler hello şirket içi Active Directory parçası değildir. Aynı Örneğin OpenLDAP + Kerberos kullanarak Linux uygulamaları için geçerlidir.

> [!NOTE]
> Bu belgede yalnızca bulut dağıtımları tam SAP Windows'un özel olarak Azure Active Directory uzantısız çalışıyor olarak tanımlanan / OpenLDAP veya şirket içi genel Buluta ad çözümlemesi. Yalnızca bulut yapılandırmaları, üretim SAP sistemleri veya SAP STMS veya diğer şirket içi kaynakları Azure ve şirket içi bulunan kaynaklar üzerinde barındırılan SAP sistemleri arasında kullanılan toobe gereken yeri yapılandırması için desteklenmez.
>
>

* Şirket içi: VM'ler dağıtılan tooan-siteye, çok siteli sahip Azure aboneliği veya ExpressRoute bağlantısı hello şirket içi inizdeki ve Azure arasında olduğu bir senaryo açıklanmaktadır. Ortak Azure belgelerine dağıtımları bu tür şirket içi senaryoları açıklanmıştır. Merhaba neden hello bağlantı tooextend şirket içi etki alanları için şirket içi Active Directory / OpenLDAP ve DNS Azure'da şirket. Merhaba şirket içi yatay hello aboneliğin Azure varlıklar genişletilmiş toohello olduğu. Bu uzantı, hello VM'ler hello şirket içi etki alanının parçası olabilir. Merhaba şirket içi etki alanının etki alanı kullanıcıları hello sunucularına erişebilir ve Hizmetleri üzerindeki VM'ler (DBMS Hizmetleri gibi) çalıştırabilirsiniz. Dağıtılan VM'ler şirket içi ve Azure dağıtılan VM'ler arasında iletişim ve ad çözümleme mümkündür. Bu çoğu SAP varlıklar toobe dağıtılmış bekliyoruz hello senaryodur.  Bkz: [bu] [ vpn-gateway-cross-premises-options] makale ve [bu] [ vpn-gateway-site-to-site-create] daha fazla bilgi için.

> [!NOTE]
> Şirket içi dağıtımları SAP sistemleri çalışan Azure sanal makineleri bir şirket içi etki alanının üyesi olduğu SAP sistemlerinin üretim SAP sistemleri için desteklenir. Şirketler arası yapılandırmalar bölümleri dağıtmak için desteklenen veya Azure'da SAP Windows'un tamamlayın. Azure'da hello tam SAP yatay bile çalışan gerektirir bu şirket içi etki alanı ve REKLAM parçası olan sanal makineleri sahip / OpenLDAP. Merhaba belgelerinin önceki sürümleri biz hello terim 'Karma' şirket içi bağlantılar şirket içi ve Azure arasında olduğunu hello aslında burada kökü karma BT senaryoları hakkında açıklandı. Ayrıca, bu hello VM'ler için Azure'da hello parçası olan hello olgu Active Directory şirket içi / OpenLDAP.
>
>

Bazı Microsoft belgeleri şirketler arası senaryoları özellikle DBMS HA yapılandırmaları için biraz farklı bir şekilde açıklanmıştır. Hello hello SAP durumunun belgeleri ilgili, hello şirketler arası senaryo hello SAP yatay şirket içi ve Azure arasında dağıtılmış bir siteden siteye veya özel (ExpressRoute) bağlantısı ve hello olgu yalnızca toohaving boils.  

### <a name="e55d1e22-c2c8-460b-9897-64622a34fdff"></a>Kaynakları
Merhaba aşağıdaki ek kılavuzlar için SAP dağıtımlarını azure'da hello konu kullanılabilir:

* [SAP NetWeaver Azure Virtual Machines'de (VM'ler) – planlama ve Uygulama Kılavuzu'na (Bu belgenin)][planning-guide]
* [SAP NetWeaver Azure sanal makinelerde (VM'ler) – dağıtım kılavuzu][deployment-guide]
* [SAP NetWeaver Azure sanal makinelerde (VM'ler) – DBMS Dağıtım Kılavuzu][dbms-guide]
* [SAP NetWeaver Azure sanal makinelerde (VM'ler) – yüksek kullanılabilirlik Dağıtım Kılavuzu][ha-guide]

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

Lütfen hello okuyun [SCN Wiki](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) , Linux için tüm SAP notlar içerir.

Genel varsayılan sınırlamalar ve Azure abonelikleri maksimum sınırlamaları bulunabilir [bu makalede][azure-subscription-service-limits-subscription]

## <a name="possible-scenarios"></a>Olası senaryolar
SAP çok hello en kritik kuruluşların uygulamalardan biri olarak görülür. Merhaba mimarisi ve işlemler bu uygulamaların çoğunlukla çok karmaşık ve kullanılabilirlik ve performans gereksinimlerini karşıladığınızdan emin olma önemlidir.

Bu nedenle işletmenin dikkatle hakkında uygulamaları genel bulut ortamında, seçilen hello bulut sağlayıcısı bağımsız çalıştırılabilir toothink vardır.

SAP NetWeaver dağıtmak için olası sistem türleri tabanlı uygulamaları içinde genel bulut ortamlarında aşağıda listelenmiştir:

1. Orta ölçekli üretim sistemleri
2. Geliştirme sistemleri
3. Test sistemleri
4. Prototip sistemleri
5. Öğrenme / tanıtım sistemleri

Sipariş toosuccessfully SAP sistemleri Azure Iaas veya Iaas genel dağıtmak, önemli toounderstand hello önemli farklılıkları hello teklifleri geleneksel outsourcers veya barındırıcılar ve Iaas teklifleri. Merhaba geleneksel barındırma sağlayıcısı veya dış kaynak altyapısı (ağ, depolama ve sunucu türü) toohello iş yükü Uyarlanır ancak toohost bir müşterinin istediği, bunun yerine hello Müşteri'nin sorumluluk toochoose hello sağ iş yükü Iaas dağıtımları için olur.

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

Bu verilerin çoğunu bulunabilir [burada][virtual-machines-sizes]

Yukarıdaki hello bağlantıyı listelenen sınırları hello unutmayın konusunda üst sınırı. Bunu gelmez hello herhangi bir hello kaynaklar için sınırlar, örneğin tüm koşullar altında IOPS sağlanabilir. Merhaba ancak seçilen bir VM türüne hello CPU ve bellek kaynakları durumlardır. SAP tarafından desteklenen hello VM türlerinde hello CPU ve bellek kaynakları zaman hello VM içinde tüketimi için ayrılmış ve bu nedenle herhangi bir noktada kullanılabilir.

Merhaba Microsoft Azure platformu diğer Iaas platformlar gibi bir çok kiracılı platformudur. Başka bir deyişle, depolama, ağ ve diğer kaynakları kiracılar arasında paylaşılır. Akıllı azaltma ve kota mantığı kazanmadan ciddi bir şekilde başka bir kiracı (gürültülü komşu) hello performansını etkileyen gelen kullanılan tooprevent bir kiracı ' dir. Azure çalıştığında tookeep Varyanslar yaşadı bant genişliği küçük, yüksek oranda paylaşılan platformlarda mantığında eğilimindedir olmalarına rağmen toointroduce büyük sapmalar kaynak/bant genişliği kullanılabilirliğini müşteriler çok daha kullanılan tooin, şirket içi dağıtımlarına ' dir. Sonuç olarak, farklı bakımından toonetworking ya da depolama g/ç (Merhaba birim yanı sıra gecikme) bant genişliği düzeylerinden dakika toominute karşılaşabilirsiniz. Azure SAP sistemde bir şirket içi sistemde daha büyük sapmalar karşılaşabilir hello olasılık hesaba toobe gerekir.

Tooevaluate kullanılabilirlik gereksinimlerini bir son adımdır. Olabilir, Azure altyapı temel bu hello güncelleştirilmiş tooget gerekiyor ve yeniden VM'ler toobe çalıştıran hello ana gerektirir. Bu durumlarda, bu konaklarda çalışan sanal makineler kapatılması ve de yeniden. belirli bir bölge için çekirdek olmayan iş saatleri sırasında Hello zamanlama böyle bakım yapılır ancak yeniden başlatma gerçekleşir birkaç saatlerde hello olası görece geniş bir penceredir. Vardır toomitigate bazı teknolojiler hello olabilir Azure platformu içinde yapılandırılmış veya tüm hello böyle güncelleştirmeleri etkiler. DBMS ve SAP uygulama gelecekteki yeniliklerini hello Azure platformu, toominimize hello etkisini gibi yeniden tasarlanmıştır.

Toosuccessfully dağıtmanız Azure SAP sisteme, hello şirket içi SAP sistemleri işletim sistemi, veritabanı ve SAP uygulamaları gerekir SAP Azure destek matrisi hello üzerinde görünür, uygun hello kaynakları hello içinde Azure altyapı sağlayabilir ve hangi olabilir Kullanılabilirlik SLA Microsoft Azure'un sunduğu hello ile çalışır. Bu sistemlere tanımlandığı gibi iki dağıtım senaryosu aşağıdaki hello birinde toodecide gerekir.

### <a name="1625df66-4cc6-4d60-9202-de8a0b77f803"></a>Yalnızca bulut - Azure sanal makine dağıtımlarınızı hello bağımlılıkları olmadan şirket içi müşteri ağ
![SAP demo veya Azure'da dağıtılan eğitim senaryo ile tek VM][planning-guide-figure-100]

Bu senaryo SAP ve SAP olmayan yazılım'ın tüm hello bileşenleri tek bir VM içinde yüklendiği eğitimleri veya tanıtım sistemleri için genel bir durumdur. Bu dağıtım senaryosunda, üretim SAP sistemleri desteklenmez. Genel olarak, bu senaryonun gereksinimlerine hello uyuyor:

* Merhaba VM'ler kendilerini hello genel ağ üzerinden erişilebilir. Merhaba VM'ler toohello içinde çalışan hello uygulamalar için doğrudan ağ bağlantısı içi hello gösterileri veya eğitimleri içeriğe sahip olan ya da hello şirket ağı veya hello müşteri gerekli değildir.
* Merhaba eğitimleri veya tanıtım senaryo temsil eden birden çok VM durumunda ağ iletişimleri ve ad çözümleme hello VM'ler arasında toowork gerekir. Ancak VM'ler hello kümesi arasındaki iletişimi VM'ler birkaç kümesi yan yana girişim dağıtılabilir böylece yalıtılmış toobe gerekir.  
* Internet bağlantısı hello son kullanıcı tooremote oturumu için sanal makineleri Azure üzerinde barındırılan toohello içine gereklidir. Merhaba konuk işletim sistemi bağlı olarak, Terminal Hizmetleri/RDS veya VNC/ssh kullanılan tooaccess hello VM tooeither hello eğitim görevleri yerine getirmek veya hello gösterileri gerçekleştirin. SAP gibi 3200, 3300 & 3600 can bağlantı noktaları, aynı zamanda ortaya hello SAP uygulama örneği herhangi Internet bağlantılı masaüstünden erişilebilir.
* Merhaba SAP sistemleri (ve yalnızca son kullanıcı erişimi için ortak Internet bağlantısı gerektirir ve bir bağlantı tooother azure'da VM gerektirmez Azure tek başına senaryoda VM(s)) temsil eder.
* SAPGUI ve tarayıcı yüklenir ve hello üzerinde doğrudan VM çalıştırılır.
* VM toohello özgün durumunun hızlı bir sıfırlama ve yeni dağıtım, özgün durumuna yeniden gereklidir.
* Tanıtım ve birden çok VM, bir Active Directory gerçekleşen eğitim senaryoları hello durumda / OpenLDAP ve/veya DNS hizmeti VM'ler her kümesi için gereklidir.

![Sanal makinenin bir tanıtım veya bir Azure bulut hizmeti eğitim senaryoda temsil eden, Grup][planning-guide-figure-200]

Burada her hello kümesinin hello VM adları olan hello aynı gerek toobe paralel olarak dağıtılan sanal makine her hello hello aklınızda tookeep ayarlar önemlidir.

### <a name="f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10"></a>Şirket içi - tek dağıtımını ya da Azure hello şirket içi ağınıza tam olarak tümleştirilmiş hello zorunluluğu ile içine birden çok SAP VM
![VPN siteden siteye bağlantı (şirket içi)][planning-guide-figure-300]

Bu senaryo, birçok olası dağıtım desenlerle bir şirket içi senaryodur. Basit hello SAP yatay şirket içi bazı bölümleri ve diğer bölümleri hello SAP yatay, Azure üzerinde çalışan olarak açıklanan olabilir. Merhaba SAP bileşenleri bir parçası Azure üzerinde çalışan hello olgu tüm yönlerini son kullanıcılar için saydam olmalıdır. Bu nedenle Merhaba SAP aktarım düzeltme sistem (STMS), RFC iletişimi, yazdırma, güvenlik (SSO gibi) vb. Azure üzerinde çalışan hello SAP sistemleri için sorunsuz bir şekilde çalışır. Ancak hello şirketler arası senaryo da burada hello tam SAP yatay Azure'da hello Müşteri'nin etki alanı ile çalışır ve Azure'da DNS genişletilmiş bir senaryo açıklanmaktadır.

> [!NOTE]
> Üretken SAP sistemleri çalıştırmak için desteklenen hello dağıtım senaryosu budur.
>
>

Okuma [bu makalede] [ vpn-gateway-create-site-to-site-rm-powershell] hakkında daha fazla bilgi için tooconnect tooMicrosoft Azure şirket içi ağ

> [!IMPORTANT]
> Azure ve şirket içi müşteri dağıtımlar arasında şirketler arası senaryolar hakkında varsayılır, tüm SAP sistemleri hello bazda arıyoruz. Olan senaryoları *desteklenmiyor* için şirket içi senaryolar şunlardır:
>
> * SAP uygulamaları farklı katmanlar farklı dağıtım yöntemleri çalışıyor. Örneğin Merhaba DBMS katman şirket içi ancak hello SAP uygulama katmanı Azure Vm'leri olarak (veya tersi) dağıtılan VM'ler içinde çalışır.
> * Azure ve bazı şirket içi SAP katmanda bazı bileşenleri. Örneğin Şirket içi ve Azure sanal makineleri arasındaki hello SAP uygulama katmanı örneklerini bölme.
> * Bir sistem SAP örnekleri birden çok Azure bölgeleri üzerinde çalışan sanal makineler dağıtımını desteklenmiyor.
>
> Bu kısıtlamalar Hello nedeni, özellikle hello uygulama örnekleri ile SAP sisteminin hello DBMS katman arasındaki bir SAP sistem içinde çok düşük gecikme süresi yüksek performanslı ağ hello gereksinimdir.
>
>

### <a name="supported-os-and-database-releases"></a>Desteklenen işletim sistemi ve veritabanı sürümleri
* Bu makalede Azure sanal makine Hizmetleri'ni listelenen için desteklenen Microsoft sunucu yazılımı: <http://support.microsoft.com/kb/2721672>.
* İşletim sistemi sürümleri desteklenir, SAP yazılım ile birlikte Azure sanal makine hizmetlerini desteklenen veritabanı sistemi sürümleri SAP notta belgelenen [1928533].
* SAP uygulamaları ve Azure sanal makine hizmetlerini desteklenen sürümler SAP notta belgelenmiştir [1928533].
* Yalnızca 64 Bit görüntüleri desteklenen toorun SAP senaryolar için azure'da Konuk VM olarak verilmiştir. Bu, aynı zamanda yalnızca 64-bit SAP uygulamaları ve veritabanları desteklenir anlamına gelir.

## <a name="microsoft-azure-virtual-machine-services"></a>Microsoft Azure sanal makine Hizmetleri
Merhaba Microsoft Azure Hizmetleri platform barındırılan ve Microsoft veri merkezleri işletilen Internet ölçeğinde bulut platformudur. Merhaba platform hello Microsoft Azure sanal makine Hizmetleri (bir hizmet veya Iaas olarak altyapı) ve zengin bir Platform olarak hizmet (PaaS) özellikleri kümesi içerir.

Hello Azure platformu teknoloji eylemli hello gereksinimini azaltır ve altyapı satın alır. Koruma kolaylaştırır ve uygulamaların isteğe bağlı hesaplama ve depolama toohost sağlayarak işletim, ölçeklendirme ve web uygulaması ve bağlı uygulamaları yönetme. Altyapı yönetimi, yüksek kullanılabilirlik için tasarlanmış bir platformuyla otomatik ve dinamik toomatch kullanımı ihtiyaçları Kullandıkça Öde fiyatlandırma modeli hello seçeneğiyle ölçeklendirme.

![Microsoft Azure sanal makine hizmetlerini konumlandırma][planning-guide-figure-400]

Azure sanal makine Services ile Microsoft (bkz: Şekil 4) Iaas örnekleri toodeploy özel sunucu görüntüleri tooAzure etkinleştirildiğini. Merhaba azure'da sanal makineler Hyper-V sanal sabit sürücülerde (VHD) temel alır ve konuk işletim sistemi olarak farklı işletim sistemlerine yükleyebilirsiniz toorun vardır.

İşletimsel açısından bakıldığında, Azure sanal makine hizmeti benzer sunar hello şirket içinde dağıtılan sanal makineleri olarak karşılaşır. Bununla birlikte, gerek duymadığınız hello önemli avantajı vardır tooprocure, yönetmek ve hello altyapısını yönetme. Geliştiriciler ve Yöneticiler bu sanal makineleri içindeki hello işletim sistemi görüntüsünün tam denetime sahiptir. Yöneticiler, bu sanal makineleri tooperform Bakım ve görevler gibi yazılım dağıtım görevlerini sorun giderme uzaktan oturum açabilir. Hesaba toodeployment içinde hello yalnızca kısıtlamaları hello boyutları ve Azure Vm'leri özelliklerini var. Bunlar gibi ince olmayabilir bu şirket içinde yapılabilir gibi ayrıntılı yapılandırma. VM türlerinin bileşimini temsil eden bir seçenek vardır:

* Vcpu'lar sayısı,
* Bellek
* Eklenebilecek VHD'ler sayısı,
* Ağ ve depolama bant genişlikleri.

Merhaba boyutu ve çeşitli farklı sanal makinelerin boyutları sınırlamaları sunulan bir tabloda görülme [bu makalede][virtual-machines-sizes]

Fark gibi farklı aileleri ya da sanal makineleri dizi vardır. DEC 2015'ten itibaren VM'ler aileleri aşağıdaki hello ayırt edebilirsiniz:

* A0 A7 VM türleri: Bu tüm SAP için sertifikalıdır. Azure Iaas ile sunulan ilk VM dizisi.
* A8-A11 VM türleri: yüksek performanslı örnekleri bilgi işlem. Farklı daha iyi gerçekleştirme çalışan diğer A-series VM'ler daha ana işlem.
* D-serisi VM türler: A0 A7 daha iyi gerçekleştirme. Merhaba VM türlerinin tümü SAP ile sertifikalı.
* DS serisi VM türler: D-serisi olarak aynı ana bilgisayarları kullanın, ancak mümkün tooconnect tooAzure Premium Storage yok (bölüm bkz [Azure Premium Storage] [ planning-guide-3.3.2] bu belgenin). Yeniden tüm VM türleri SAP ile sertifikalı.
* G-serisi VM türler: yüksek bellek VM türler.
* GS serisi VM türler: G-serisi gibi ancak hello seçeneği toouse Azure Premium Storage da dahil olmak üzere (bölüm bkz [Azure Premium Storage] [ planning-guide-3.3.2] bu belgenin). GS serisi VM'ler veritabanı sunucusu olarak kullanıldığında DB veri ve işlem günlük dosyaları için zorunlu toouse Premium depolama.

Farklı VM serisinin aynı CPU ve bellek yapılandırmalarını hello bulabilirsiniz. Bununla birlikte, bunlar hello işleme performansını bu Vm'lere hello farklı serisi dışında baktığınızda önemli ölçüde değişebilir. Sahip olmasına rağmen aynı hello CPU ve bellek yapılandırma. Merhaba temel alınan ana bilgisayar sunucu donanımı hello farklı VM türler hello giriş farklı verimlilik vardı nedenidir.  Genellikle verimliliği performansından gösterilen hello fark hello hello fiyatına da yansıtılır farklı VM'ler.

Lütfen tüm farklı VM dizisi Merhaba Azure bölgeleri (Azure bölgeleri sonraki bölüme bakın) her birinde sunulan unutmayın. Ayrıca tüm sanal makineleri veya VM seri için SAP sertifikalı unutmayın.

> [!IMPORTANT]
> SAP NetWeaver tabanlı uygulamaları Hello kullanılmak VM türleri ve yapılandırmaları yalnızca hello alt listelenen SAP notta [1928533] desteklenir.
>
>

### <a name="be80d1b9-a463-4845-bd35-f4cebdb5424a"></a>Azure bölgeleri
Microsoft, böylece çağrılan 'bölgelere Azure' toodeploy sanal makineleri sağlar. Bir Azure bölgesi yakınında içinde bulunan bir veya birden çok veri merkezleri olabilir. Merhaba Dünya Microsoft coğrafi bölgelerde hello çoğu için en az iki Azure bölgeleri vardır. Örneğin Avrupa'da bir Azure Bölgesi 'Kuzey Avrupa' ve 'Batı Avrupa' yok. Böylece teknik veya doğal afetler hello hem Azure bölgelerde etkilemez coğrafi bölge içindeki iki tür Azure bölgeleri yeterince önemli uzaklığı tarafından ayrılmış olan aynı coğrafi bölge. Microsoft sürekli olarak farklı coğrafi bölgeler yeni Azure bölgelerde çıkışı genel oluşturuyor olduğundan, bu bölgeler hello sayısı sürekli büyüyen ve Ara 2015'ten itibaren ek bölgeler önceden duyurulmuş 20 Azure bölgesiyle hello sayısına ulaşıldı. Bir müşteri olarak SAP sistemleri hello iki Azure bölgeleri Çin'de dahil olmak üzere tüm bu bölgeler, içine dağıtabilirsiniz. Azure bölgeleri hakkında bilgi geçerli toodate yedeklemek için bu Web sitesine bakın: <https://azure.microsoft.com/regions/>

### <a name="8d8ad4b8-6093-4b91-ac36-ea56d80dbf77"></a>Merhaba Microsoft Azure sanal makine kavramı
Microsoft Azure altyapı (Iaas) çözümü toohost sanal makineler ile benzer işlevler bir şirket içi sanallaştırma çözümü olarak sunar. Hangi dağıtım ve yönetim yetenekleri de sunar mümkün toocreate sanal makinelerden hello Azure Portal, PowerShell veya CLI, içinde olduğu.

Azure Resource Manager bildirim temelli bir şablon kullanarak uygulamalarınızı tooprovision sağlar. Tek bir şablonda birden çok hizmeti bağımlılıklarıyla birlikte dağıtabilirsiniz. Merhaba kullandığınız aynı şablon toorepeatedly her aşaması sırasında uygulamanızın hello uygulama yaşam döngüsü veya dağıtın.

ARM şablonları kullanma hakkında daha fazla bilgi şurada bulunabilir:

* [Dağıtma ve Azure Resource Manager şablonları ve hello Azure CLI kullanarak sanal makineleri yönetme][virtual-machines-linux-cli-deploy-templates]
* [Azure Resource Manager ve PowerShell kullanarak sanal makineleri yönetme][virtual-machines-deploy-rmtemplates-powershell]
* <https://Azure.microsoft.com/documentation/Templates/>

Başka bir ilginç hello özelliği toocreate görüntüleri sanal makinelerden tooprepare mümkün tooquickly olan depoları gereksinimlerinizi karşılayan sanal makine örnekleri dağıtma belirli sağlayan özelliktir.

Sanal makinelerden görüntüleri oluşturma hakkında daha fazla bilgi bulunabilir [bu makalede (Windows)] [ virtual-machines-windows-capture-image] veya [bu makalede (Linux)][virtual-machines-linux-capture-image].

#### <a name="df49dc09-141b-4f34-a4a2-990913b30358"></a>Hata etki alanları
Hata etki alanlarını hata, veri merkezleri ve fiziksel dikey veya raf hata etki alanı kabul edilebilir sırada yer alan çok yakından ilgili toohello fiziksel altyapı fiziksel bir birimi temsil eder, hello iki arasında doğrudan bire bir eşleme yoktur.

Microsoft Azure sanal makine Hizmetleri'ndeki bir SAP sisteminin bir parçası olarak birden çok sanal makine dağıttığınızda, farklı hata böylece hello hello gereksinimleri toplantı etki alanları, uygulamanıza hello Azure yapı denetleyicisi toodeploy etkileyebilir. Microsoft Azure SLA. Ancak, dağıtım hata etki alanı Azure ölçek birimi (yüzlerce işlem düğümleri veya depolama düğümleri ve ağ koleksiyonu) hello ya da VM'ler tooa hello atamasının belirli hata etki alanı üzerinde sahip olmadığınız bir şey doğrudan denetim. Sipariş toodirect hello Azure yapı denetleyicisi toodeploy içinde bir dizi farklı hata etki alanları üzerinden VM'ler, dağıtım sırasında tooassign bir Azure kullanılabilirlik kümesi toohello VM'ler gerekir. Bölüm Azure kullanılabilirlik kümeleri hakkında daha fazla bilgi için bkz: [Azure kullanılabilirlik kümeleri] [ planning-guide-3.2.3] bu belgedeki.

#### <a name="fc1ac8b2-e54a-487c-8581-d3cc6625e560"></a>Yükseltme etki alanları
Yükseltme etki alanlarının bir VM içinde birden çok VM çalıştıran SAP örneklerinin oluşan bir SAP sistemi içinde nasıl güncelleştirileceği toodetermine yardımcı bir birimi temsil eder. Microsoft Azure yükseltme oluştuğunda, bu yükseltme etki alanları tek tek güncelleştirme hello süreci devam ettiği. Dağıtım sırasında farklı yükseltme etki alanları VM'ler yayarak kısmen potansiyel kesintiler SAP sisteminizi koruyabilirsiniz. İçinde farklı yükseltme etki alanları yayılan bir SAP sisteminin hello VM'ler tooforce Azure toodeploy sipariş, her bir VM Dağıtım sırasında tooset belirli bir özniteliği gerekir. Benzer tooFault etki alanları, bir Azure ölçek birimi birden fazla yükseltme etki alanlarına bölünür. Sipariş toodirect hello Azure yapı denetleyicisi toodeploy içinde bir dizi farklı yükseltme etki alanları üzerinden VM'ler, dağıtım sırasında tooassign bir Azure kullanılabilirlik kümesi toohello VM'ler gerekir. Bölüm Azure kullanılabilirlik kümeleri hakkında daha fazla bilgi için bkz: [Azure kullanılabilirlik kümeleri] [ planning-guide-3.2.3] aşağıda.

#### <a name="18810088-f9be-4c97-958a-27996255c665"></a>Azure kullanılabilirlik kümeleri
Azure sanal makineleri bir Azure kullanılabilirlik kümesi içinde hello Azure yapı denetleyicisi tarafından farklı hata ve yükseltme etki alanları dağıtılacaktır. farklı hata ve yükseltme etki alanları üzerinden hello dağıtım Hello amacı altyapı Bakımı hello durumunun veya bir hata etki alanı içinde bir hatası engeller SAP sistemin tüm sanal makineleri kapatmak tooprevent budur. Varsayılan olarak, sanal makineleri bir kullanılabilirlik kümesinin parçası değildir. bir VM Hello katılım bir kullanılabilirlik kümesindeki dağıtım zamanında veya daha sonra yeniden yapılandırılması ve bir VM yeniden dağıtımını tarafından tanımlanır.

Kullanılabilirlik kümeleri arasında ilişki tooFault ve yükseltme etki alanları, Azure kullanılabilirlik kümeleri ve hello yol toounderstand hello kavramı okuyun [bu makalede][virtual-machines-manage-availability]

bir json şablonu aracılığıyla ARM toodefine kullanılabilirlik kümelerini görmek [rest API belirtimlerin hello](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2015-06-15/swagger/compute.json) ve "kullanılabilirlik" arayın.

### <a name="a72afa26-4bf4-4a25-8cf7-855d6032157f"></a>Depolama: Microsoft Azure depolama ve veri diskleri
Microsoft Azure sanal makineleri farklı depolama türlerini kullanın. SAP Azure sanal makine hizmetlerini uygularken bu iki ana depolama türleri arasındaki önemli toounderstand hello farklar olduğu:

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
> * <http://blogs.msdn.com/b/mast/archive/2013/12/07/Understanding-the-Temporary-drive-on-Windows-Azure-Virtual-Machines.aspx>
>
>

- - -
hello ana bilgisayar sunucusunun kendisi üzerinde depolandığından hello gerçek volatile sürücüdür. Merhaba VM bir dağıtımın taşınsa (örn. son toomaintenance hello konak veya kapatma ve yeniden başlatma) hello sürücü Merhaba içeriğine kaybolur. Bu nedenle, bir seçenek toostore değil Bu sürücüde herhangi bir önemli veri. Bu depolama türü için kullanılan medya türünü Hello neye benzediğini gösteren, Haziran 2015'ten itibaren çok farklı performans özellikleri olan farklı VM dizisi farklıdır:

* A5-A7: Çok sınırlı performans. Sayfa dosyası dışındaki her şey için önerilmez
* A8-A11: Bazı on bin IOPS ile çok iyi performans özellikleri ve > 1GB/sn verim.
* D-serisi: Bazı sonra bin IOPS ile çok iyi performans özellikleri ve > 1GB/sn verim.
* DS serisi: Bazı on bin IOPS ile çok iyi performans özellikleri ve > 1GB/sn verim.
* G-serisi: Bazı on bin IOPS ile çok iyi performans özellikleri ve > 1GB/sn verim.
* GS serisi: Bazı on bin IOPS ile çok iyi performans özellikleri ve > 1GB/sn verim.

Yukarıdaki deyimleri SAP ile sertifikalı toohello VM türleri uyguladığınızı. Merhaba VM dizisi mükemmel IOPS ve üretilen iş ile bazı DBMS özellikleri tarafından Dengeleme için uygun. Lütfen hello bakın [DBMS Dağıtım Kılavuzu'na] [ dbms-guide] daha fazla ayrıntı için.

Microsoft Azure depolama kalıcı depolama ve hello tipik düzeyde koruma ve SAN depolama alanı üzerinde görülen artıklık sağlar. Azure depolama birimine dayalı sanal sabit hello Azure depolama hizmetleri içinde bulunan disk (VHD) disklerdir. Merhaba yerel işletim sistemi diski (Windows C:\, Linux / (/ dev/sda1)) Azure Storage hello üzerinde depolanır ve ek birimler/takılı toohello VM depolanan vardır, çok diskler.

Bu olası tooupload varolan bir VHD'yi şirket içi veya Azure içinde boş olanlardan oluşturmak ve bu toodeployed VM'lerin ekleyin. Bu VHD Azure diskleri olarak başvurulur.

Oluşturma veya bir VHD Azure depolama alanına karşıya yükleme sonra bu olası toomount ve varolan sanal makine ve (takılmamış) VHD varolan toocopy bu tooan ekleyin.

Bu VHD kalıcı olarak veri ve bu değişikliklerin yeniden başlatmadan ve bir sanal makine örneğini yeniden güvenlidir. Örneği silinse bile bu VHD güvende ve dağıtılması veya işletim sistemi olmayan diskleri durumunda takılı tooother VM'ler olabilir.

Merhaba içinde Azure Storage farklı artıklık düzeylerinin ağ yapılandırılabilir:

* Seçilebilen en düşük düzeydir 'hello içindeki hello verilerin eşdeğer toothree çoğaltma olan yerel artıklık', aynı veri merkezinde bir Azure bölgesinin (bölüm bkz [Azure bölgeleri][planning-guide-3.1]).
* Merhaba üç görüntüleri içinde farklı veri merkezlerinde üzerinden yayılır bölge olarak yedekli depolama hello aynı Azure bölgesi.
* Varsayılan artıklık düzeyidir hello barındırılan başka bir Azure bölgesi hello verileri başka bir 3 görüntülerini zaman uyumsuz olarak hello içerik yarlar coğrafi artıklık aynı coğrafi bölge.

Ayrıca bu makalede bakımından toohello farklı artıklık seçenekleri üstünde hello tablosuna bakın: <https://azure.microsoft.com/pricing/details/storage/>

Daha fazla bilgi için bakımından tooAzure depolama burada bulunabilir:

* <https://Azure.microsoft.com/documentation/Services/Storage/>
* <https://Azure.microsoft.com/Services/Site-Recovery>
* <https://msdn.microsoft.com/library/windowsazure/ee691964.aspx>
* <https://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/Azure-disk-Encryption-for-Linux-and-Windows-Virtual-Machines-Public-Preview.aspx>

#### <a name="azure-standard-storage"></a>Standart Azure depolama
Azure Iaas yayımlandığında azure standart BLOB Depolama hello kullanılabilir depolama türündeydi. IOPS kota tek VHD uygulanmıyor vardı. Gecikme yaşadı genellikle dağıtılan SAN/NAS cihazları Gelişmiş SAP sistemler için şirket içi barındırılan olarak aynı sınıf hello değildi. Bununla birlikte, Azure Standard Storage oluyor uygulamasına yol açıyordu yüzlerce için yeterli hello bu sırada Azure üzerinde dağıtılan SAP sistemleri.

Azure Standard Storage depolanan hello gerçek veri depolama işlemleri, giden veri aktarımları ve seçilen artıklığı seçeneği hello birim göre ücretlendirilir. Birçok VHD boyutu hello en fazla 1 TB sırasında oluşturulabilir, ancak bu boş kaldığı sürece ücretsizdir. Bir VHD 100 GB ile sonra doldurduğunuzda değil, VHD ile oluşturulan hello nominal boyutu hello ve 100 GB depolamak için ücretlendirilir.

#### <a name="ff5ad0f9-f7f4-4022-9102-af07aef3bc92"></a>Azure Premium depolama
Nisan 2015'te Microsoft Azure Premium Storage kullanıma sunmuştur. Premium depolama hello hedef tooprovide ile sunulan:

* Daha iyi g/ç gecikmesi.
* Daha iyi verimlilik.
* G/ç gecikmesi daha az sonuçlarındaki.

Bu amaç için çok değişiklikler kullanıma sunulmuştur hangi hello en önemli ikisidir:

* Hello Azure depolama düğümleri SSD diskleri kullanımı
* Tarafından desteklenen yeni bir okuma önbelleği hello Azure işlem düğümünün yerel SSD

İçinde tooStandard depolama burada özellikler değişmemiştir hello boyutu veya hello disk (VHD), bağımlı Premium depolama şu anda bu makalenin hello SSS bölümüne önce hello sonunda gösterilen 3 farklı disk kategorisi vardır: <https:/ /Azure.microsoft.com/pricing/details/Storage/>

IOP/VHD ve disk işleme/VHD hello disklerin hello boyutu kategorisine göre bağımlı bakın

Premium Storage hello durumda maliyet temel gibi VHD'ler, ancak böyle bir VHD, VHD hello içinde depolanan hello veri miktarını hello bağımsız hello boyutu kategorisini depolanan hello gerçek veri birimi değil.

Ayrıca, VHD gösterilen hello boyutu kategoriye doğrudan eşleme değil Premium depolama oluşturabilirsiniz. Özellikle VHD'ler standart depolama biriminden Premium depolama alanına kopyalama işlemi sırasında bu hello durumda olabilir. Böyle durumlarda, bir eşleme toohello sonraki en büyük Premium depolama diski seçeneği gerçekleştirilir.

Yalnızca belirli VM serisi hello Azure Premium Storage ' yararlanabilir unutmayın. DEC 2015'ten itibaren hello DS - ve GS serisi bunlar. Merhaba DS serisi olduğu temelde hello aynı D-serisi DS serisi hello özelliği toomount Premium depolama olduğunu hello durumla VM'ler tabanlı olarak ayrıca Azure Standard Storage üzerinde barındırılan tooVHDs. Aynı şey G serisi karşılaştırıldığında tooGS-seri için geçerli değil.

Merhaba DS serisi Vm'lerde hello parçası çıkış denetimi varsa [bu makalede] [ virtual-machines-sizes] olduğunu veri birimi sınırlamaları tooPremium depolama VHD'ler hello VM düzeyi hello ayrıntı düzeyi de fark. Ayrıca farklı DS serisi veya GS serisi VM'ler bakımından toohello sayısında bağlanabilir VHD farklı sınırlamaları vardır. Bu sınırlar da yukarıdaki hello makalesinde belgelenmiştir. Ancak aslında bu örneğin 32 x P30 diskleri/VHD'ler tooa bağlamanız halinde tek DS14 VM, hello en yüksek verimlilik P30 disk x 32 edinebileceğiniz değil anlamına gelir. Bunun yerine hello hello makalede anlatıldığı şekilde VM düzeyinde en fazla üretilen veri işleme sınırlar.

Premium depolama hakkında daha fazla bilgi şurada bulunabilir: <http://azure.microsoft.com/blog/2015/04/16/azure-premium-storage-now-generally-available-2>

#### <a name="azure-storage-accounts"></a>Azure Depolama Hesapları
Hizmetleri veya azure'da VM dağıtırken dağıtımı VHD'ler VM görüntüleri ve Azure Storage hesapları olarak adlandırılan birimler halinde düzenlenmiş olması gerekir. Bir Azure dağıtımı planlarken toocarefully gereken Azure hello kısıtlamaları göz önünde bulundurun. Merhaba bir yandan, depolama hesapları, sınırlı sayıda Azure abonelik başına yoktur. Her Azure depolama hesabı VHD dosyaları, çok sayıda tutabilir rağmen bir sabit bir sınır yoktur hello üzerinde depolama hesabı başına IOPS toplam sayısı. SAP VM'ler yüzlerce önemli GÇ çağrı oluşturuluyor DBMS sistemleriyle dağıtırken olduğu birden çok Azure depolama hesapları arasında yüksek IOPS DBMS VM'ler toodistribute önerilir. Tooexceed hello geçerli sınırlandırma Azure Storage hesapları, abonelik başına dikkatli olunması gerekir. Depolama hello veritabanı dağıtımı bir SAP sistemi için hayati bir parçası olduğundan, bu kavram zaten başvurulan hello bölümlerinde daha ayrıntılı ele alınmıştır [DBMS Dağıtım Kılavuzu'na][dbms-guide].

Azure Storage hesapları hakkında daha fazla bilgi bulunabilir [bu makalede][storage-scalability-targets]. Bu makaleyi okuduktan, hello sınırlamaları Azure standart depolama hesapları ve Premium depolama hesapları arasındaki farkları olduğunu unutmayın. Temel farklılıkları hello gibi bir depolama hesabında depolanan verilerin hacmi ' dir. Standart depolama hello büyüklük Premium Storage ile büyük birimdir. Merhaba diğer tarafı hello standart depolama hesabı ancak böyle bir kısıtlama Hello Azure Premium depolama hesabı vardır ('Toplam istek oranı' sütununa bakın) IOP cinsinden ciddi bir şekilde sınırlıdır. Ayrıntıları ve bu farklılıklar sonuçlarını SAP sistemleri, özellikle hello DBMS sunucularda hello dağıtımları ele alırken aşağıdakiler ele alınacaktır.

Bir depolama hesabında hello olasılığı toocreate farklı kapsayıcılar hello amacını düzenleme ve farklı VHD'ler kategorilere ayırmak için sahip. Bu genellikle kullanılan tooe.g kapsayıcılardır. farklı VM'ler VHD'leri ayırın. Yalnızca bir kapsayıcı veya tek bir Azure depolama hesabı altında birden çok kapsayıcı kullanarak hiçbir performans etkileri vardır.

Azure içinde hello tooprovide hello Azure içinde VHD için benzersiz bir ad gerekiyor adlandırma bağlantı izleyen bir VHD ad aşağıdaki gibidir:

    http(s)://<storage account name>.blob.core.windows.net/<container name>/<vhd name>

Yukarıda sözü edilen hello dize olarak toouniquely hello Azure depolama alanında depolanan VHD tanımlamak.

### <a name="61678387-8868-435d-9f8c-450b2424f5bd"></a>Microsoft Azure ağ iletişimi
Microsoft Azure istiyoruz tüm senaryoları hello eşlenmesini sağlayan bir ağ altyapısı sağlayacaktır SAP yazılımıyla toorealize. Merhaba özellikleri şunlardır:

* Dışında doğrudan Windows Terminal Hizmetleri veya ssh/VNC üzerinden VM'ler toohello hello erişimden
* Erişim tooservices ve hello VM'ler içinde uygulamalar tarafından kullanılan belirli bağlantı noktaları
* İç iletişim ve Azure Vm'leri olarak dağıtılan VM'ler grubu arasındaki ad çözümlemesi
* Bir müşterinin şirket içi ağı arasındaki hello Azure ağı şirket içi bağlantılar
* Azure siteler arasında çapraz Azure bölgesini ya da veri merkezi bağlantısı

Daha fazla bilgi şurada bulunabilir: <https://azure.microsoft.com/documentation/services/virtual-network/>

Çok sayıda farklı olanaklar tooconfigure adı ve IP çözümleme Azure vardır. Bu belgede, Azure DNS (Karşıtlık toodefining içinde kendi bir DNS hizmeti) kullanmanın hello varsayılan yalnızca bulut senaryoları bağlıdır. Ayrıca kendi DNS sunucusunu ayarlama yerine kullanılabilecek yeni bir Azure DNS hizmeti vardır. Daha fazla bilgi bulunabilir [bu makalede] [ virtual-networks-manage-dns-in-vnet] ve [bu sayfayı](https://azure.microsoft.com/services/dns/).

Şirket içi hello hello olgu üzerinde bağlı şirketler arası senaryolar için VPN veya özel bağlantı tooAzure OpenLDAP/AD/DNS genişletilmiştir. Belirli senaryolar aşağıda belirtildiği gibi gerekli toohave Azure üzerinde yüklü bir AD/OpenLDAP çoğaltma olması olabilir.

Ağ iletişimi olduğundan ve ad çözümlemesi bir SAP sistemi için hello veritabanı dağıtım sürecinin hayati bir parçası ise, bu kavram hello bölümlerinde daha ayrıntılı ele alınmıştır [DBMS Dağıtım Kılavuzu'na][dbms-guide].

##### <a name="azure-virtual-networks"></a>Azure Sanal Ağları
Bir Azure sanal ağı oluşturarak Azure DHCP işlevleri tarafından ayrılan hello özel IP adresleri hello adres aralığı tanımlayabilirsiniz. Şirket içi senaryolarda tanımlanan başlangıç IP adresi aralığı hala DHCP kullanarak Azure tarafından ayrılır. Ancak, etki alanı adı çözümleme (Merhaba VM'ler bir şirket içi etki alanının bir parçası olduğunu varsayarak) şirket içi gerçekleştirilir ve bu nedenle farklı Azure Cloud Services ötesinde adresleri çözebilirsiniz.

[comment]: <> (Hala gerekli MSSedusch? Yapılacaklar ilk Azure sanal ağı ilişkili tooan benzeşim grubu oluştu. İle Azure sanal ağında sınırlı toohello Azure ölçek birimi benzeşim grubu atanan bu hello aldı. Merhaba sonunda bu yüksetlmesi hello sanal ağ hello Azure ölçek birimi kısıtlı toohello kaynaklar oluştu. Bu tarihten sonra değişti ve artık Azure sanal ağlar arasında birden fazla Azure ölçek birimi uzatabilirsiniz. Ancak, gerektiren Azure sanal ağlar olduğunu ** NOT ** artık oluşturma zamanında benzeşim grupları ile ilişkilendirilmiş. Biz zaten daha önce yıl önce bir ters toorecommendations aşağıdakileri yapmalısınız bahsedilen ** Azure benzeşim grupları artık yararlanan değil **. Ayrıntılar için lütfen bkz. < https://azure.microsoft.com/blog/regional-virtual-networks/>)

Her sanal makinede Azure gereksinimlerini toobe tooa sanal ağ bağlandı.

Daha fazla ayrıntı bulunabilir [bu makalede] [ resource-groups-networking] ve [bu sayfayı](https://azure.microsoft.com/documentation/services/virtual-network/).

[comment]: <> (MShermannd Yapılacaklar bulamadı hello OpenLDAP konu + ARM içeren bir makale;)
[comment]: <> (MSSedusch < https://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL>)

> [!NOTE]
> Varsayılan olarak, bir VM dağıtıldıktan sonra hello sanal ağ yapılandırması değiştirilemiyor. Merhaba TCP/IP ayarları toohello Azure DHCP sunucusu bırakılmalıdır. Varsayılan, dinamik IP ataması davranıştır.
>
>

Hello MAC adresi hello sanal ağ kartının örneğin Yeniden Boyutlandır ve hello Windows sonra değişebilir veya Linux konuk işletim sistemi hello yeni ağ kartı seçer ve DHCP, tooassign hello IP ve DNS adreslerini bu durumda otomatik olarak kullanır.

##### <a name="static-ip-assignment"></a>Statik IP ataması
Sabit olası tooassign olduğunu veya bir Azure sanal ağı içinde tooVMs ayrılmış IP adresleri. Bir Azure sanal ağında Hello VM'ler çalıştıran harika olasılığı tooleverage gerekli veya bazı senaryolar için gerekli değilse bu işlevselliği açar. Merhaba IP ataması hello VM, hello VM çalışıp çalışmadığını veya kapatma bağımsız hello varlığını geçerli kalır. Sonuç olarak, tootake ihtiyacınız hello IP adresleri aralığı hello sanal ağ için tanımlarken, sanal makineleri (VM'ler çalıştığından ve durdurulmuş) genel sayısını göz önüne hello. Merhaba VM ve ağ arabirimiyle silinir kadar veya başlangıç IP adresi yeniden XML'deki atanan kadar Hello IP adresi atanmış olarak kalır. Lütfen ayrıntılı bilgilere bakın [bu makalede][virtual-networks-static-private-ip-arm-pportal].

##### <a name="multiple-nics-per-vm"></a>VM başına birden çok NIC
Bir Azure sanal makine için birden çok sanal ağ arabirim kartı (Vnıc) tanımlayabilirsiniz. Merhaba özelliği toohave ile birden çok vNICs tooset burada örneğin istemci trafiğini bir Vnıc yönlendirilir ve arka uç trafiği ikinci Vnıc yönlendirilir ağ trafiği ayrımı yukarı başlatabilirsiniz. Farklı sınırlamaları vardır VM hello türü bağımlı vNICs toohello sayısı tahminini. Tam Ayrıntılar, işlevsellik ve sınırlamaları aşağıdaki makalelerde bulunabilir:

* [Bir VM ile birden çok NIC oluşturun][virtual-networks-multiple-nics]
* [Birden çok NIC bir şablon kullanarak sanal makineleri dağıtma][virtual-network-deploy-multinic-arm-template]
* [Birden çok NIC PowerShell kullanarak sanal makineleri dağıtma][virtual-network-deploy-multinic-arm-ps]
* [Birden çok NIC hello Azure CLI kullanarak sanal makineleri dağıtma][virtual-network-deploy-multinic-arm-cli]

#### <a name="site-to-site-connectivity"></a>Siteden siteye bağlantı
Şirket içi Azure Vm'leri ve şirket içi saydam ve kalıcı bir VPN bağlantısıyla bağlı olur. Bu, beklenen toobecome hello en yaygın SAP dağıtım modelinde Azure olur. Merhaba işlemsel yordamlara ve Azure SAP durumlarda işlemlerle saydam çalışmalıdır varsayılır. Bu, mümkün tooprint bu sistemler dışında olması yanı sıra SAP aktarım yönetim sistemi (TMS) tootransport geliştirme sistemden dağıtılan şirket içi Azure tooa test sisteminde değişiklikleri hello kullanmak anlamına gelir. Daha fazla belge siteden siteye geçici bulunabilir [bu makalede][vpn-gateway-create-site-to-site-rm-powershell]

##### <a name="vpn-tunnel-device"></a>VPN tüneli aygıtı
Siteden siteye bağlantı (şirket içi veri merkezi tooAzure veri merkezi) toocreate sipariş, tooeither gerekir almak ve bir VPN cihazı yapılandırma ya da Windows Server ile birlikte bir yazılım bileşeni olarak Yönlendirme ve Uzaktan Erişim hizmeti (, tanıtılan RRAS) kullanın 2012.

* [PowerShell kullanarak siteden siteye VPN bağlantısı olan bir sanal ağ oluşturma][vpn-gateway-create-site-to-site-rm-powershell]
* [Siteden siteye VPN Gateway bağlantıları için VPN cihazları hakkında][vpn-gateway-about-vpn-devices]
* [VPN ağ geçidi SSS][vpn-gateway-vpn-faq]

![Şirket içi ve Azure arasında siteden siteye bağlantı][planning-guide-figure-600]

Yukarıdaki şekilde Hello iki Azure abonelikleri Azure sanal ağlarda IP adresi alt aralıklara kullanımı için ayrılmış olan gösterir. Merhaba Hello bağlantısını ağ tooAzure VPN kurulan şirket içi.

#### <a name="point-to-site-vpn"></a>Noktadan siteye VPN
Noktadan siteye VPN her istemci makine tooconnect kendi VPN ile Azure'da gerektirir. Konumundaki arıyoruz hello SAP senaryoları için noktadan siteye bağlantı pratik değil. Bu nedenle, daha ayrıntılı başvuru toopoint siteden siteye VPN bağlantısı verilir.

[comment]: <> (MSSedusch--Daha fazla bilgi şurada bulunabilir)
[comment]: <> (MShermannd Yapılacaklar bağlantı artık geçerli; Ancak ARM yine de desteklenmiyor - sonraki bağlantıya bakın)
[comment]: <> (MSSedusch--< http://msdn.microsoft.com/library/azure/dn133798.aspx>.)
[comment]: <> (MShermannd Yapılacaklar noktası tooSite henüz ARM ile desteklenmiyor)
[comment]: <> (MSSedusch--< https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/>)

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
Biz toobe hello olgu hakkında hello depolama birimini temizlemek ve ağ altyapısı hello Azure altyapı hizmetleri, çeşitli çalışan sanal makineler arasında paylaşılır. Ve yalnızca hello müşterinin kendi veri merkezlerini olduğu gibi bazı hello altyapı kaynakların aşırı sağlama yer tooa derece gerçekleştirin. disk, CPU, ağ ve diğer kotaları toolimit hello kaynak tüketimini ve toopreserve tutarlı ve belirleyici performans Hello Microsoft Azure platformu kullanır.  disk, CPU, RAM ve ağ hello sayısı için farklı kotalar Hello farklı VM türler (A5, A6, vb.) sahip.

> [!NOTE]
> SAP tarafından desteklenen hello VM türleri CPU ve bellek kaynakları hello ana bilgisayar düğümlerinde önceden ayrılmış. Bu hello VM dağıtıldığında, hello kaynakları hello konaktaki hello VM türü tarafından tanımlandığı şekilde kullanılabilir olması anlamına gelir.
>
>

Ne zaman kotaları her sanal makine boyutu için planlama ve SAP Azure çözümlerini boyutlandırma hello dikkate alınmalıdır.  Merhaba VM kotaları açıklanmıştır [burada][virtual-machines-sizes].

açıklanan hello kota hello teorik en yüksek değerleri temsil eder.  VHD başına IOPS Hello sınırı küçük IOs (8 kb) ile elde edilen ancak büyük IOs (1 Mb) büyük olasılıkla elde değil.  Merhaba IOPS sınırı tek VHD'ler hello ayrıntı düzeyi zorlanır.

Bir kaba karar ağacı toodecide Azure sanal makine hizmetlerini ve özelliklerini bir SAP sistemi uygun olup olmadığını veya mevcut bir sistemi sipariş toodeploy hello Azure, sistemde farklı şekilde yapılandırılmış toobe gerekip gerekmediğini hello karar ağacı aşağıdaki kullanılabilir:

![Karar ağacı toodecide özelliği toodeploy Azure üzerinde SAP][planning-guide-figure-700]

**1. adım**: hello en önemli bilgileri toostart ile olan belirli bir SAP sistem hello SAP gereksinimi. Merhaba SAP gereksinimleri gerek toobe Hello SAP Sistem zaten olsa bile hello DBMS ve hello SAP uygulama bölümlerini, ayrılmış şirket içi bir katman 2 yapılandırmasında dağıtıldı. Varolan sistemler için SAP toohello donanımı genellikle belirlenen veya tahmini ilgili hello üzerinde mevcut SAP kıyaslamaları temel. Merhaba sonuçları şurada bulunabilir: <http://global.sap.com/campaigns/benchmark/index.epx>.
Yeni dağıtılan SAP sistemleri hello SAP hello sistem gereksinimleriyle belirlemelisiniz boyutlandırma alıştırma çalıştınız.
Azure üzerinde bu blog ve ekli belgeyi SAP boyutlandırma için Ayrıca bkz: <http://blogs.msdn.com/b/saponsqlserver/archive/2015/12/01/new-white-paper-on-sizing-sap-solutions-on-azure-public-cloud.aspx>

**2. adım**: varolan sistemler için g/ç birim hello ve saniyede g/ç işlemleri hello DBMS sunucuda ölçülebilir. Yeni planlı sistemler için alıştırma hello yeni sistem için de boyutlandırma hello kaba fikir edinmek hello g/ç gereksinimlerinin hello DBMS yan vermesi gerekir. Emin değilseniz, sonunda tooconduct bir kavram kanıtı gerekir.

**3. adım**: karşılaştırma hello SAP gereksinimi hello hello SAP hello farklı VM türler Azure DBMS sunucusuyla sağlayabilir. SAP Hello bilgi hello farklı Azure VM türlerinde SAP notta belgelenen [1928533]. Merhaba veritabanı katmanı çıkışı dağıtımların hello çoğunluğu ölçeklenmez SAP NetWeaver sistem hello katman olduğundan hello odak hello DBMS VM üzerinde ilk olmalıdır. Buna karşılık, hello SAP uygulama katmanı dışa genişletilebilir. Merhaba SAP hiçbiri destekleniyorsa Azure VM türleri gerekli hello SAP dağıtabilir, planlanan hello SAP sisteminin hello iş yükü Azure üzerinde çalıştırılamaz. Hello sistemi için toochange hello iş yükü birime gereksinim veya toodeploy hello sistem şirket içi ya da gerekir.

**Adım 4**: belirtildiği gibi [burada][virtual-machines-sizes], Azure üretilmesini VHD bağımsız başına IOPS kota standart depolama veya Premium depolama kullanın. Merhaba VM türü bağımlı, takılabilir VHD'ler hello sayısı değişir. Sonuç olarak, her hello farklı VM türler elde edilebilir maksimum IOPS birkaç hesaplayabilirsiniz. Merhaba veritabanı dosya düzeni bağımlı, VHD toobecome hello konuk işletim sistemi içinde tek bir birim şeritler. Ancak, dağıtılan bir SAP sisteminin geçerli IOPS birimi Hello hello en büyük VM türüne Azure ve hiçbir fırsat toocompensate daha fazla belleğe sahip olup olmadığını hesaplanan hello sınırları aşarsa, hello SAP sistem hello iş yükünü ciddi bir şekilde etkilenebilir. Böyle durumlarda, burada Azure hello sistemde dağıtmamanız noktası isabet.

**5. adım**: özellikle SAP içinde şirket içi 2 katmanlı yapılandırmalarında sistemlerini dağıtılan, hello olasılığını hello sistem Azure üzerinde 3 katmanlı yapılandırmada yapılandırılan toobe gerekebilir. Bu adımda, ölçeği genişletilemez ve hangi hello CPU ve bellek kaynakları farklı Azure VM türleri teklif hello uyar değil hello SAP uygulama katmanında bir bileşen olup toocheck gerekir. Gerçekten varsa bu tür bir bileşeni, Azure'da hello SAP sistem ve iş yükünü dağıtılamıyor. Ancak, genişleme varsa birden fazla Azure VM'yi, hello sistem bileşenlerine Azure'da dağıtılabilir SAP uygulama hello.

**Adım 6**: hello DBMS ve SAP uygulama katmanı bileşenleri Azure Vm'lerde çalıştırılabilir, hello yapılandırma ile regard için tanımlanan toobe gerekir:

* Azure VM sayısı
* Merhaba ayrı bileşenler için VM türler
* DBMS VM tooprovide VHD'ler sayısında yeterli IOPS

## <a name="managing-azure-assets"></a>Azure varlıklarını yönetme
### <a name="azure-portal"></a>Azure Portal
Hello Azure Portal üç arabirimleri toomanage Azure VM dağıtımlarının biridir. görüntülerden sanal makineleri dağıtma gibi hello temel yönetim görevleri hello Azure Portal yapılabilir. Ayrıca, depolama hesapları, sanal ağlar ve diğer Azure bileşenlerinin hello oluşturma olduğundan ayrıca görevleri hello Azure Portal çok iyi işleyebilir. Ancak, VHD'leri karşıya gibi işlevselliği tooAzure veya azure'daki bir VHD kopyalama olan üçüncü taraf araçlarını veya PowerShell veya CLI üzerinden Yönetimi gerektiren görevleri şirket içi.

![Microsoft Azure Portal - sanal makineye genel bakış][planning-guide-figure-800]

[comment]: <> (MSSedusch * < https://azure.microsoft.com/documentation/articles/virtual-networks-create-vnet-arm-pportal/>)
[comment]: <> (MSSedusch * < https://azure.microsoft.com/documentation/articles/virtual-machines-windows-tutorial/>)

Yönetim ve yapılandırma görevlerini hello sanal makine örneği için Azure Portal hello içinde mümkündür.

Yeniden başlatmak ve bir sanal makineyi kapatmak makinenin yanı sıra da eklemek, ayırmak ve veri diskleri hello sanal makine örneği, toocapture hello örneği görüntü hazırlık için oluşturabilir ve hello sanal makine örneğinin hello boyutunu yapılandırın.

Hello Azure Portal temel işlevleri toodeploy sağlar ve VM'ler ve diğer Azure hizmetleriyle birçok yapılandırın. Ancak tüm kullanılamaz işlevselliği hello Azure Portal tarafından ele alınmıştır. Hello Azure portalı, bu olası tooperform görevler gibi değil:

* VHD'ler tooAzure karşıya yükleme
* Sanal makineleri kopyalama

[comment]: <> (MShermannd Yapılacaklar Otomasyon hakkında neler SAP VM'ler için hizmet?)
[comment]: <> (Bu sırada olası birden çok VM os MSSedusch dağıtımı)
[comment]: <> (Ayrıca MSSedusch Otomasyon dağıtım ile ilgili herhangi bir türde hello Azure portal ile mümkün değil. Birden çok VM komut dosyalı dağıtımı gibi görevleri hello Azure Portal mümkün değildir.)

### <a name="management-via-microsoft-azure-powershell-cmdlets"></a>Microsoft Azure PowerShell cmdlet'leri aracılığıyla Yönetimi
Windows PowerShell yaygın sayıda Azure sistemlerinde dağıtma müşteriler tarafından benimsenen güçlü ve Genişletilebilir bir çerçevedir. PowerShell cmdlet'leri Masaüstü, dizüstü bilgisayar veya özel yönetim istasyon Hello yüklendikten sonra PowerShell cmdlet'leri hello uzaktan çalıştırılabilir.

işlem tooenable hello kullanımı Azure PowerShell cmdlet'leri için yerel Masaüstü/dizüstü hello ve ile kullanım için olanlar hello tooconfigure hello nasıl Azure aboneliklerinden açıklanan [bu makalede][powershell-install-configure].

Ayrıntılı adımlar nasıl tooinstall, güncelleştirme ve hello Azure PowerShell cmdlet'lerini yapılandırmak da bulunabilir [bu hello Dağıtım Kılavuzu'nun][deployment-guide-4.1].

Müşteri Deneyimi kadarki PowerShell (PS) kesinlikle hello VM'ler dağıtımında toocreate özel adımlar ve daha güçlü aracı toodeploy VM'ler hello olduğunu olmuştur. Tüm SAP örnekleri Azure'da çalışan hello müşteriler hello Azure Portal yapın veya hatta PS cmdlet'lerini kullanarak PS cmdlet'leri toosupplement yönetim görevlerini kullanarak özel olarak toomanage Azure dağıtımları. Windows 2000'den fazla ilgili cmdlet'leri hello olarak aynı adlandırma kuralı Hello Azure belirli cmdlet'lerini paylaşımı hello olduğundan, kolay bir görev için Windows yöneticileri tooleverage bu cmdlet'leri kalır.

Örnek buraya bakın: <http://blogs.technet.com/b/keithmayer/archive/2015/07/07/18-steps-for-end-to-end-iaas-provisioning-in-the-cloud-with-azure-resource-manager-arm-powershell-and-desired-state-configuration-dsc.aspx>

[comment]: <> (MShermannd Yapılacaklar açıklamak sınandığında yeni CLI komutu)
Hello Azure Monitoring uzantısı SAP için dağıtım (bölüm bkz [Azure izlemesi çözümünü SAP] [ planning-guide-9.1] bu belgedeki) PowerShell veya CLI aracılığıyla yalnızca mümkündür. Bu nedenle zorunlu toosetup olduğunu ve PowerShell veya CLI dağıtırken veya Azure SAP NetWeaver sistemde yönetme yapılandırın.  

Azure daha fazla işlevsellik sağlayan gibi hello cmdlet'lerinin bir güncelleştirme gerektiren toobe eklenen yeni PS cmdlet'leri adımıdır. Bu nedenle algılama toocheck hello Azure karşıdan site en az hello ayda kolaylaştırır <https://azure.microsoft.com/downloads/> hello cmdlet yeni bir sürümü için. Merhaba yeni sürümü yalnızca hello sürümün üzerine yüklenir.

PowerShell komutları denetleyin burada Azure genel listesi ilgili: <https://msdn.microsoft.com/library/azure/dn708514.aspx>.

### <a name="management-via-microsoft-azure-cli-commands"></a>Microsoft Azure CLI komutları aracılığıyla Yönetimi
Linux kullanan ve toomanage Azure istediğiniz müşteriler için bir seçenek kaynakları Powershell olmayabilir. Microsoft Azure CLI alternatif olarak sunar.
Hello Azure CLI açık kaynak, bir dizi hello Azure platformu ile çalışmak için platformlar arası komutları sağlar. Hello Azure CLI aynı işlevselliği hello Azure portalında bulunan hello çoğunu sağlar.

Yükleme, yapılandırma ve nasıl tooaccomplish toouse CLI komutları hakkında bilgi için Azure görevleri bakın.

* [Hello Azure CLI yükleme][xplat-cli]
* [Dağıtma ve Azure Resource Manager şablonları ve hello Azure CLI kullanarak sanal makineleri yönetme][virtual-machines-linux-cli-deploy-templates]
* [Mac, Linux ve Windows Azure Resource Manager ile için Hello Azure CLI kullanma][xplat-cli-azure-resource-manager]

Lütfen bölüm okuyun [Linux VM'ler için Azure CLI] [ deployment-guide-4.5.2] hello içinde [Dağıtım Kılavuzu'na] [ planning-guide] nasıl toouse Azure CLI toodeploy hello Azure üzerinde SAP için izleme uzantısı.

## <a name="different-ways-toodeploy-vms-for-sap-in-azure"></a>Farklı şekillerde toodeploy VM'ler için azure'da SAP
Bu bölümde hello farklı şekillerde toodeploy azure'da VM öğreneceksiniz. VHD ve VM'ler için Azure'da işlenmesini yanı sıra ek hazırlık yordamlar bu bölümde ele alınmıştır.

### <a name="deployment-of-vms-for-sap"></a>VM dağıtımı için SAP
Microsoft Azure diskleri ilişkili ve toodeploy VM'ler birden çok yol sunar. Bu nedenle hello VM'ler hazırlıklar dağıtım hello yöntemine bağlı olarak değişebilir olduğundan çok önemli toounderstand hello farklar kalır. Genel olarak, biz hello aşağıdaki senaryoları göz atın:

#### <a name="4d175f1b-7353-4137-9d2f-817683c26e53"></a>VM genelleştirilmiş olmayan bir disk ile şirket içi tooAzure taşıma
Şirket içi tooAzure belirli bir SAP sistemden toomove planlayın. Bu hello hello işletim sistemi içeren VHD yükleyerek yapılabilir, SAP ikili dosyaları ve DBMS ikili dosyaları artı hello VHD'ler hello verilerle Merhaba ve günlük hello DBMS tooAzure dosyaları. Buna karşılık çok[Senaryo #2 aşağıdaki][planning-guide-5.1.2]hello ana bilgisayar adı, SAP SID tutmak ve SAP kullanıcı hesaplarında hello şirket içi ortamda yapılandırılmış olarak Azure VM hello. Bu nedenle, hello görüntü genelleme gerekli değildir. Lütfen bölümlere bakın [VM genelleştirilmiş olmayan bir disk ile şirket içi tooAzure geçiş hazırlığı] [ planning-guide-5.2.1] şirket içi hazırlık adımları ve karşıya yükleme genelleştirilmiş VMs veya VHD'ler için bu belgenin tooAzure. Bölüm okuyun [Senaryo 3: şirket içi SAP ile genelleştirilmiş Azure VHD kullanarak bir VM taşınan] [ deployment-guide-3.4] hello içinde [Dağıtım Kılavuzu'na] [ deployment-guide]böyle bir görüntü azure'da dağıtmanın ayrıntılı adımlar için.

#### <a name="e18f7839-c0e2-4385-b1e6-4538453a285c"></a>Bir müşteri belirli görüntüsü olan bir VM dağıtma
Toospecific düzeltme eki gereksinimleri, işletim sistemi veya DBMS sürümü hello Azure Marketi sağlanan hello görüntülerinde gereksinimlerinize değil. Bu nedenle, daha sonra birkaç kez dağıtılabilen 'özel' kendi işletim sistemi/DBMS VM görüntüsü kullanarak bir VM'i toocreate gerekebilir. tooprepare çoğaltmak için 'özel' görüntüsü, aşağıdaki öğelerindeki hello kabul toobe vardır:


[comment]: <> (MSSedusch > daha fazla ayrıntı buraya bakın:)
[comment]: <> (MShermannd Yapılacaklar ilk Klasik modeli hakkında bağlantıdır. Bir Azure belge makalesi bulunamadı)
[comment]: <> (MSSedusch >< https://azure.microsoft.com/documentation/articles/virtual-machines-create-upload-vhd-windows-server/>)
[comment]: <> (MSSedusch >< http://blogs.technet.com/b/blainbar/archive/2014/09/12/modernizing-your-infrastructure-with-hybrid-cloud-using-custom-vm-images-and-resource-groups-in-microsoft-azure-part-21-blain-barton.aspx>)
- - -
> ![Windows][Logo_Windows] Windows
>
> Hello ayarları (örneğin, Windows SID ve ana bilgisayar adı) soyutlanır/üzerinde hello genelleştirilmiş gerekir Windows VM hello sysprep komutu şirket içi.
>
>
> ![Linux][Logo_Linux] Linux
>
> Lütfen bu makaleler için açıklanan başlangıç adımları [SUSE] [ virtual-machines-linux-create-upload-vhd-suse] veya [Red Hat] [ virtual-machines-linux-redhat-create-upload-vhd] tooprepare VHD toobe karşıya tooAzure.
>
>

- - -
(Özellikle 2 katmanlı sistemler için), şirket içi VM'deki SAP içerik zaten yüklediyseniz, hello Azure VM hello örneği aracılığıyla hello dağıtımını yeniden adlandırdıktan sonra hello tarafından SAP yazılım sağlama desteklenen yordamı hello SAP sistem ayarlarını uyarlayabilirsiniz Yöneticisi (SAP Not [1619720]). Bölümlere bakın [için SAP Müşteri belirli bir resim'yle bir VM'yi dağıtmak için hazırlık] [ planning-guide-5.2.2] ve [şirket içi tooAzure VHD'den karşıya] [ planning-guide-5.3.2]şirket içi hazırlık adımları ve genelleştirilmiş bir VM tooAzure karşıya yükleme için bu belgenin. Bölüm okuyun [Senaryo 2: özel bir görüntü ile bir VM için SAP dağıtma] [ deployment-guide-3.3] hello içinde [Dağıtım Kılavuzu'na] [ deployment-guide] ayrıntılı adımları için Bu tür bir resim Azure dağıtma.

#### <a name="deploying-a-vm-out-of-hello-azure-marketplace"></a>Hello Azure Market dışında bir VM dağıtma
3. taraf hello Azure Marketi toodeploy VM görüntüsünü VM sağlanan veya toouse Microsoft istersiniz. Azure VM dağıtımı sonra hello izleyin aynı kılavuzları ve Araçlar tooinstall hello SAP yazılım ve/veya DBMS VM içinde bir şirket içi ortamda yaptığınız gibi. Bölüm daha ayrıntılı dağıtımı açıklaması için lütfen bkz [Senaryo 1: hello SAP için Azure Market dışında bir VM dağıtma] [ deployment-guide-3.2] hello içinde [Dağıtım Kılavuzu'na] [ deployment-guide].

### <a name="6ffb9f41-a292-40bf-9e70-8204448559e7"></a>Azure için sanal makineleri SAP ile hazırlama
Azure'da Vm'leri karşıya yüklemeden önce toomake emin hello sanal makineleri ve VHD belirli gereksinimleri karşılamanız gerekir. Kullanılan hello dağıtım yöntemine bağlı olarak küçük farklılıklar vardır.

#### <a name="1b287330-944b-495d-9ea7-94b83aff73ef"></a>VM genelleştirilmiş olmayan bir disk ile şirket içi tooAzure geçiş için hazırlama
Bir ortak dağıtım toomove şirket içi tooAzure bir SAP sistemi çalıştıran mevcut bir VM'yi yöntemidir. VM ve hello hello VM yalnızca çalışmalı Azure kullanarak SAP sisteminde hello aynı ana bilgisayar adı ve büyük olasılıkla aynı hello SAP SID'si. Bu durumda hello konuk işletim sistemi, VM için birden çok dağıtım genelleştirilmiş değil. Azure'da Hello şirket içi ağ Genişletilmiş (bölüm bkz [şirket içi - tek dağıtımını ya da Azure hello şirket içi ağınıza tam olarak tümleştirilmiş hello zorunluluğu ile içine birden çok SAP VM] [ planning-guide-2.2] bu belgedeki), sonra bile hello aynı etki alanı hesapları bu şirket içi önce kullanılan olarak VM hello içinde kullanılabilir.

Kendi Azure VM Disk hazırlanırken gereksinimleri şunlardır:

* Başlangıçta hello VHD içeren hello işletim sistemi yalnızca en büyük boyutu 127 GB olabilir. Bu sınırlama hello Mart 2015 sonunda ortadan. Başka bir Azure depolama VHD de barındırılan olarak artık hello hello işletim sistemini içeren VHD boyutu too1TB yukarı olabilir.

[comment]: <> (MShermannd Yapılacaklar varsa toocheck CLI ayrıca toostatic dönüştürür)
* VHD biçiminde sabit hello toobe gerekir. Dinamik VHD veya VHDx biçiminde VHD'ler henüz Azure üzerinde desteklenmez. Dinamik VHD hello VHD PowerShell cmdlet'leri veya CLI ile karşıya yüklediğinizde dönüştürülmüş toostatic VHD'ler olacaktır
* Takılı toohello VM olan ve Azure toohello VM gerek toobe de sabit bir VHD biçiminde, yeniden takılmasını VHD'ler. Merhaba aynı boyutunda hello işletim sistemi diski toodata diskleri geçerlidir. VHD'ler, 1 TB maksimum boyuta sahip olabilir. Dinamik VHD hello VHD PowerShell cmdlet'leri veya CLI ile karşıya yüklediğinizde dönüştürülmüş toostatic VHD'ler olacaktır
* Microsoft destek ya da, hizmetler ve uygulamalar toorun bağlamının olarak VM dağıtılan hello kadar atanabilir ve daha uygun kullanıcılar tarafından kullanılan yönetici ayrıcalıklarına sahip başka bir yerel hesap kullanılabilir ekleyin.
* Bir yalnızca bulut dağıtım senaryosu kullanmanın hello çalışması için (bölüm bkz [salt bulut - Azure sanal makine dağıtımlarınızı hello bağımlılıkları olmadan şirket içi müşteri ağ] [ planning-guide-2.1] bu Bu dağıtım yöntemi, Azure'da hello Azure diski dağıtıldığında hesapları çalışmayabilir etki alanı ile birlikte belge). Bu, özellikle kullanılan toorun Hizmetleri hello DBMS veya SAP uygulamaları gibi olan hesapları için geçerlidir. Bu nedenle bu tür etki alanı hesaplarıyla VM yerel tooreplace gerekir ve hello VM hello şirket içi etki alanı hesapları silin. Şirket içi etki alanı kullanıcıları hello VM görüntüsünde tutma değil bir sorun hello VM hello şirketler arası senaryoda bölümde açıklandığı gibi dağıtıldığında [şirket içi - tek dağıtımını ya da Azure olma hello gereksinimiyle içine birden çok SAP VM Merhaba şirket içi ağınıza tam olarak tümleşiktir] [ planning-guide-2.2] bu belgedeki.
* Etki alanı hesapları DBMS oturumu açma kullanılan veya hello sistem şirket içi ve bu VM'lerin çalışırken kullanıcılar yalnızca bulut senaryolarda dağıtılan toobe beklenen hello etki alanı kullanıcıları silinmiş toobe gerekir. Merhaba yerel yönetici artı başka bir VM yerel kullanıcı eklendiğini bir oturum açma/kullanıcı olarak hello yöneticileri olarak DBMS içine emin toomake gerekir.
* Bu hello belirli dağıtım senaryosu için gerekebilecek gibi diğer yerel hesaplar ekleyin.

- - -
> ![Windows][Logo_Windows] Windows
>
> Bu senaryoda hello VM hiçbir genelleme (sysprep) gerekli tooupload olan ve hello Azure VM dağıtabilirsiniz.
> Sürücü D:\ değil bölümde açıklandığı gibi disklerdeki kümesi disk otomatik bağlama kullanıldığından emin olun [bağlı diskler için otomatik bağlama ayarı] [ planning-guide-5.5.3] bu belgedeki.
>
> ![Linux][Logo_Linux] Linux
>
> Bu senaryoda hiçbir Genelleştirme (waagent-deprovision) hello VM gerekli tooupload olan ve hello Azure VM dağıtın.
> / Mnt/kaynak kullanılmaz ve tüm diskleri UUID bağlandığından emin olun. Hello işletim sistemi diski için hello önyükleme yükleyicisi girişi de hello UUID tabanlı bağlama gösterdiğinden emin olmalısınız.
>
>

- - -
#### <a name="57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3"></a>SAP için belirli bir müşteri resim'yle bir VM'yi dağıtmak için hazırlama
Genelleştirilmiş bir işletim sistemi içeren VHD dosyaları de Azure depolama hesaplarındaki kapsayıcılar depolanır. Merhaba VHD dağıtım şablonu dosyalarınızda VHD kaynağı olarak bölümde açıklandığı gibi başvurarak bu tür bir görüntüden VHD yeni bir VM dağıtabilirsiniz [Senaryo 2: özel bir görüntü ile bir VM için SAP dağıtma] [ deployment-guide-3.3] Merhaba, [Dağıtım Kılavuzu'na][deployment-guide].

Kendi Azure VM görüntüsü hazırlanırken gereksinimleri şunlardır:

* Başlangıçta hello VHD içeren hello işletim sistemi yalnızca en büyük boyutu 127 GB olabilir. Bu sınırlama hello Mart 2015 sonunda ortadan. Başka bir Azure depolama VHD de barındırılan olarak artık hello hello işletim sistemini içeren VHD boyutu too1TB yukarı olabilir.

[comment]: <> (MShermannd Yapılacaklar varsa toocheck CLI ayrıca toostatic dönüştürür)
* VHD biçiminde sabit hello toobe gerekir. Dinamik VHD veya VHDx biçiminde VHD'ler henüz Azure üzerinde desteklenmez. Dinamik VHD hello VHD PowerShell cmdlet'leri veya CLI ile karşıya yüklediğinizde dönüştürülmüş toostatic VHD'ler olacaktır
* Takılı toohello VM olan ve Azure toohello VM gerek toobe de sabit bir VHD biçiminde, yeniden takılmasını VHD'ler. Merhaba aynı boyutunda hello işletim sistemi diski toodata diskleri geçerlidir. VHD'ler, 1 TB maksimum boyuta sahip olabilir. Dinamik VHD hello VHD PowerShell cmdlet'leri veya CLI ile karşıya yüklediğinizde dönüştürülmüş toostatic VHD'ler olacaktır
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
> / Mnt/kaynak kullanılmaz ve tüm diskleri UUID bağlandığından emin olun. Merhaba işletim sistemi disk hello önyükleme yükleyicisi girdi ayrıca hello UUID tabanlı bağlama yansıtır emin olun.
>
>

- - -
* SAP GUI (için yönetim ve Kurulum amacıyla) bu tür bir şablonda önceden yüklenebilir.
* Bu yazılım hello ile çalışabilirsiniz sürece gerekli toorun hello VM'ler şirket içi senaryolarda başarıyla yüklenebilmesi için diğer yazılım VM hello yeniden adlandırın.

Merhaba VM yeterince hazırlanır toobe genel ve sonunda bağımsız/kullanıcıları hesapları hello kullanılamaz olarak Azure dağıtım senaryosu hedeflenen, böyle bir görüntüyü genelleme hello son hazırlık adımı yürütülür.

##### <a name="generalizing-a-vm"></a>Bir VM genelleme
- - -
[comment]: <> (MShermannd Yapılacaklar sahip toofind daha iyi makaleler / genelleştirme hakkında belge hello VM'ler için ARM)
> ![Windows][Logo_Windows] Windows
>
> Merhaba son tooa VM bir yönetici hesabıyla toolog adımdır. 'Yönetici' olarak bir Windows komut penceresi açın. Too...\Windows\System32\sysprep gidin ve sysprep.exe yürütün.
> Küçük bir pencere görüntülenir. Önemli toocheck hello 'Generalize' seçeneği olan (Merhaba varsayılan olarak atanmamış checked) ve onun 'Yeniden başlatma' too'Shutdown varsayılandan hello kapatma seçeneği Değiştir '. Bu yordamı hello sysprep işleminin yürütülen şirket içi hello VM konuk işletim sistemini olduğunu varsayar.
> Zaten Azure'da çalışan bir VM ile tooperform hello yordamı istiyorsanız açıklanan başlangıç adımları izleyin [bu makalede][virtual-machines-windows-capture-image].
>
> ![Linux][Logo_Linux] Linux
>
> [Nasıl toocapture Resource Manager şablonu olarak Linux sanal makine toouse][virtual-machines-linux-capture-image]
>
>

- - -
### <a name="transferring-vms-and-vhds-between-on-premises-tooazure"></a>Sanal makineleri ve VHD şirket içi tooAzure arasında aktarma
VM görüntüleri ve diskleri tooAzure karşıya hello Azure Portal mümkün olmadığından, toouse Azure PowerShell cmdlet'lerini veya CLI gerekir. Diğer bir olasılık hello Aracı 'AzCopy' hello kullanılır. Merhaba aracı VHD'leri (her iki yönde) şirket içi ve Azure arasında kopyalayabilirsiniz. Ayrıca, Azure bölgeler arasında VHD'ler de kopyalayabilirsiniz. Lütfen bakın [bu belgeleri] [ storage-use-azcopy] karşıdan yükleme ve AzCopy kullanımı.

Üçüncü bir alternatif toouse çeşitli üçüncü taraf GUI yönelik araçlar da olacaktır. Bununla birlikte, lütfen bu araçları Azure sayfa Bloblarını destekliyorsanız emin olun. Toouse Azure sayfa blobu ihtiyacımız bizim amacıyla depolamak için (Merhaba farklar burada açıklanmıştır: <https://msdn.microsoft.com/library/windowsazure/ee691964.aspx>). Ayrıca Azure tarafından sağlanan hello hello VM'ler ve karşıya toobe gereken VHD'ler sıkıştırma içinde çok verimli araçlardır. Bu önemlidir, çünkü bu verimliliği sıkıştırma (yine de hello karşıya yükleme bağlantı toohello hello şirket içi tesis ve hello Azure dağıtım bölge Internet'ten hedeflenen bağlı olarak değişir) hello karşıya yükleme süresini azaltır. Bu, VM veya VHD Avrupa konumu toohello dayalı ABD Azure veri merkezleri karşıya daha uzun sürer gelen karşıya aynı VM'ler/VHD'ler toohello Avrupa Azure veri merkezlerinde hello Orta bir varsayılır.

#### <a name="a43e40e6-1acc-4633-9816-8f095d5a7b6a"></a>Şirket içi tooAzure VHD'den karşıya yükleme
var olan VM veya hello VHD'den şirket içi böyle bir VM ağı veya VHD gereken toomeet hello gereksinimleri bölümde listelenen tooupload [VM genelleştirilmiş olmayan bir disk ile şirket içi tooAzure geçiş hazırlığı] [ planning-guide-5.2.1] bu belgenin.

Bu tür bir VM genelleştirilmiş toobe gerekmez ve hello durumu ve hello kapanışında içi yan sonra sahip şekli karşıya yüklenebilir. Merhaba aynı herhangi bir işletim sistemini içermeyen ek VHD'ler için geçerlidir.

##### <a name="uploading-a-vhd-and-making-it-an-azure-disk"></a>Bir VHD yüklemek ve bir Azure diski yapma
Bu durumda biz tooupload ile veya olmadan bir işletim sisteminde, bir VHD istediğiniz ve tooa bir veri diski olarak VM bağlama veya işletim sistemi diski olarak kullanın. Bu çok adımlı bir işlemdir

**PowerShell**

* Oturum açma tooyour abonelikle *Login-AzureRmAccount*
* İçeriğiniz ile Merhaba aboneliği ayarlamak *Set-AzureRmContext* ve parametre Subscriptionıd veya varlığıyla SubscriptionName - <https://msdn.microsoft.com/library/mt619263.aspx>
* Karşıya yükleme VHD ile Merhaba *Ekle AzureRmVhd* tooan Azure depolama hesabı - bkz <https://msdn.microsoft.com/library/mt603554.aspx>
* Yeni bir VM yapılandırması toohello VHD kümesi hello işletim sistemi diski ile *kümesi AzureRmVMOSDisk* -bkz <https://msdn.microsoft.com/library/mt603746.aspx>
* Merhaba VM yapılandırma ile yeni bir VM oluşturun *New-AzureRmVM* -bkz <https://msdn.microsoft.com/library/mt603754.aspx>
* Bir veri diski tooa ekleme yeni VM ile *Ekle AzureRmVMDataDisk* -bkz <https://msdn.microsoft.com/library/mt603673.aspx>

**Azure CLI**

* Anahtar tooAzure Resource Manager moduyla *azure config modu arm*
* Oturum açma tooyour abonelikle *azure oturum açma*
* Aboneliğinizi seçin *azure hesabı ayarlama`<subscription name or id`>*
* Karşıya yükleme VHD ile Merhaba *azure depolama blob karşıya yükleme* -bkz [kullanma hello Azure Storage ile Azure CLI][storage-azure-cli]
* Merhaba karşıya VHD ile işletim sistemi diski olarak belirterek yeni bir VM oluşturmak *azure vm oluşturma* ve parametre -d
* Bir veri diski tooa ekleme yeni VM ile *vm disk attach-yeni*

**Şablon**

* Merhaba VHD Powershell veya Azure CLI ile karşıya yükle
* Gösterildiği gibi hello VHD başvuran bir JSON şablonu ile Merhaba VM dağıtmak [Bu örnek JSON şablonunu](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-from-specialized-vhd/azuredeploy.json).

#### <a name="deployment-of-a-vm-image"></a>Bir VM görüntüsü dağıtımını
var olan VM veya hello VHD'den şirket içi isteğe bağlı olarak sipariş toouse bir Azure VM görüntü olarak bu tür bir VM ağ veya VHD ihtiyacınız bölümde listelenen toomeet hello gereksinimleri tooupload [için SAP Müşteri belirli bir resim'yle bir VM'yi dağıtmak için hazırlık] [ planning-guide-5.2.2] bu belgenin.

* Kullanım *sysprep* Windows veya *waagent-deprovision* Linux toogeneralize üzerinde VM - bkz [nasıl toocapture bir Windows sanal makinesi hello Resource Manager dağıtım modeli] [ virtual-machines-windows-capture-image-prepare-the-vm-for-image-capture] veya [nasıl toocapture Resource Manager şablonu olarak Linux sanal makine toouse][virtual-machines-linux-capture-image-capture]
* Oturum açma tooyour abonelikle *Login-AzureRmAccount*
* İçeriğiniz ile Merhaba aboneliği ayarlamak *Set-AzureRmContext* ve parametre Subscriptionıd veya varlığıyla SubscriptionName - <https://msdn.microsoft.com/library/mt619263.aspx>
* Karşıya yükleme VHD ile Merhaba *Ekle AzureRmVhd* tooan Azure depolama hesabı - bkz <https://msdn.microsoft.com/library/mt603554.aspx>
* Yeni bir VM yapılandırması toohello VHD kümesi hello işletim sistemi diski ile *kümesi AzureRmVMOSDisk - SourceImageUri - CreateOption fromImage* -bkz <https://msdn.microsoft.com/library/mt603746.aspx>
* Merhaba VM yapılandırma ile yeni bir VM oluşturun *New-AzureRmVM* -bkz <https://msdn.microsoft.com/library/mt603754.aspx>

**Azure CLI**

* Kullanım *sysprep* Windows veya *waagent-deprovision* Linux toogeneralize üzerinde VM - bkz [nasıl toocapture bir Windows sanal makinesi hello Resource Manager dağıtım modeli] [ virtual-machines-windows-capture-image-prepare-the-vm-for-image-capture] veya [nasıl toocapture Resource Manager şablonu olarak Linux sanal makine toouse] [ virtual-machines-linux-capture-image-capture] Linux için
* Anahtar tooAzure Resource Manager moduyla *azure config modu arm*
* Oturum açma tooyour abonelikle *azure oturum açma*
* Aboneliğinizi seçin *azure hesabı ayarlama`<subscription name or id`>*
* Karşıya yükleme VHD ile Merhaba *azure depolama blob karşıya yükleme* -bkz [kullanma hello Azure Storage ile Azure CLI][storage-azure-cli]
* Merhaba karşıya VHD ile işletim sistemi diski olarak belirterek yeni bir VM oluşturmak *azure vm oluşturma* ve parametre -Q

**Şablon**

* Kullanım *sysprep* Windows veya *waagent-deprovision* Linux toogeneralize üzerinde VM - bkz [nasıl toocapture bir Windows sanal makinesi hello Resource Manager dağıtım modeli] [ virtual-machines-windows-capture-image-prepare-the-vm-for-image-capture] veya [nasıl toocapture Resource Manager şablonu olarak Linux sanal makine toouse] [ virtual-machines-linux-capture-image-capture] Linux için
* Merhaba VHD Powershell veya Azure CLI ile karşıya yükle
* Gösterildiği gibi hello görüntü VHD başvuran bir JSON şablonu ile Merhaba VM dağıtmak [Bu örnek JSON şablonunu](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json).

#### <a name="downloading-vhds-tooon-premises"></a>VHD'ler tooon içi indirme
Bir hizmet olarak Azure altyapısı mümkün tooupload VHD'leri ve SAP sistemleri yalnızca olma tek yönlü bir yol değil. SAP taşıyabilirsiniz Azure sistemlerden de hello şirket içi dünyaya yedekleyin.

Merhaba indirme Hello süre boyunca hello VHD'ler etkin olamaz. Hatta takılı tooVMs olan VHD indirirken hello VM toobe kapatma gerekir. Ardından yeni bir sistemi kullanılan tooset edileceği, şirket içi ve kabul edilebilir değilse hello hello süresi sırasında indirin ve sistem azure'da hello hello yeni sistem kurulumu hello içerik toodownload hello veritabanı yalnızca istiyorsanız hala işletimsel olabilir , bir VHD'ye sıkıştırılmış veritabanı yedeklemesi gerçekleştirerek uzun bir kesinti süresini önler ve ayrıca indirmek yerine VHD işletim sistemi temel VM hello hemen indirin.

#### <a name="powershell"></a>PowerShell
Hello SAP sistem durdurulur ve hello VM kapatıldı, kullanabileceğiniz hello hello PowerShell cmdlet'ini Kaydet AzureRmVhd hedef toodownload hello VHD diskleri toohello şirket içi world destekleyen şirket içi. Merhaba Azure Portal (Merhaba VHD oluşturulduğu gerek toonavigate toohello depolama hesabı ve hello depolama kapsayıcısı) hello hello 'Depolama bölüm' bulabileceğiniz VHD hello URL'sini gerekir, toodo ve hello VHD olması gereken yerde tooknow gerekir kopyalanır.

Ardından yalnızca hello parametresi SourceUri hello VHD toodownload ve hello LocalFilePath hello URL'si olarak hello fiziksel konumu hello (adı dahil) VHD olarak tanımlayarak hello komutu yararlanabilirsiniz. Merhaba komutu gibi görünebilir:

```powerhell
Save-AzureRmVhd -ResourceGroupName <resource group name of storage account> -SourceUri http://<storage account name>.blob.core.windows.net/<container name>/sapidedata.vhd -LocalFilePath E:\Azure_downloads\sapidesdata.vhd
```

Merhaba Kaydet AzureRmVhd cmdlet daha fazla ayrıntı için lütfen burayı <https://msdn.microsoft.com/library/mt622705.aspx>.

#### <a name="cli"></a>CLI
Merhaba SAP sistem durdurulur ve hello VM kapatıldı, kullanabileceğiniz hello Azure CLI komutu azure depolama blob yükleme hello üzerinde hedef toodownload hello VHD diskleri toohello şirket içi world destekleyen şirket içi. Merhaba adı ve hello hello 'Depolama bölüm' bulabileceğiniz VHD hello kapsayıcının hello Azure Portal (Merhaba VHD oluşturulduğu gerek toonavigate toohello depolama hesabı ve hello depolama kapsayıcısı) gereksinim duyduğunuz, toodo ve tooknow gerekir nerede Merhaba VHD için kopyalanmalıdır.

Ardından yalnızca hello parametreleri blob ve hello VHD toodownload ve hello hedef kapsayıcının hello fiziksel hedef konumu hello (adı dahil) VHD olarak tanımlama hello komutu yararlanabilirsiniz. Merhaba komutu gibi görünebilir:

```
azure storage blob download --blob <name of hello VHD toodownload> --container <container of hello VHD toodownload> --account-name <storage account name of hello VHD toodownload> --account-key <storage account key> --destination <destination of hello VHD toodownload>
```

### <a name="transferring-vms-and-vhds-within-azure"></a>Sanal makineleri ve VHD Azure içinde aktarma
#### <a name="copying-sap-systems-within-azure"></a>Azure içinde SAP sistemleri kopyalama
SAP sistem veya SAP uygulama katmanı destekleyen bile bir adanmış DBMS sunucusu büyük olasılıkla ya da ' % s'hello OS hello ikililerini içeren veya veri hello birkaç VHD'leri oluşur ve dosyalar hello SAP veritabanının oturum. VHD'ler kopyalama Azure işlevselliğini hello ne hello VHD'ler toodisk kaydetme Azure işlevleri, anlık görüntü eşzamanlı olarak birden çok VHD misiniz bir eşitleme mekanizması vardır. Bu nedenle, hello hello durumunu kopyaladığınız veya bu takılı olsa bile VHD'ler kaydedilmiş hello karşı aynı VM farklı olacaktır. Bu durumda farklı VHD'ler Merhaba, hello son veritabanında hello farklı veri ve içerdiği logfile(s) sahip olmanın hello somut tutarsız olacağını anlamına gelir.

**Sonuç: Sipariş toocopy veya toostop hello SAP sistem gerekir ve ayrıca gerekir bir SAP sistem yapılandırmasının bir parçası olan VHD kaydetme VM hello aşağı tooshut dağıtıldı. Yalnızca sonra kopyalayabilirsiniz veya yükleme hello VHD'ler tooeither kümesi Azure veya şirket içi hello SAP sistem bir kopyasını oluşturun.**

Veri diskleri Azure depolama hesabınız VHD dosyaları olarak depolanır ve doğrudan tooa sanal makine eklemek veya bir görüntü olarak kullanılması olabilir. Bu durumda, beeing toohello sanal makineye bağlı önce hello VHD kopyalanan tooanother konum değil. azure'da hello VHD dosyasının tam adı Hello Azure içinde benzersiz olmalıdır. Zaten daha önce belirtildiği gibi hello tür benzer bir üç kısımlı ad adıdır:

    http(s)://<storage account name>.blob.core.windows.net/<container name>/<vhd name>

##### <a name="powershell"></a>PowerShell
Azure PowerShell cmdlet'leri toocopy VHD gösterildiği gibi kullanabilirsiniz [bu makalede][storage-powershell-guide-full-copy-vhd].

##### <a name="cli"></a>CLI
Azure CLI toocopy VHD gösterildiği gibi kullanabilirsiniz [bu makalede][storage-azure-cli-copy-blobs]

##### <a name="azure-storage-tools"></a>Azure Storage araçları
* <http://azurestorageexplorer.Codeplex.com/Releases/View/125870>

Ayrıca vardır, burada bulunan Azure depolama gezginleri professional sürümleri:

* <http://www.cerebrata.com/>
* <http://clumsyleaf.com/products/cloudxplorer>

bir VHD'nin depolama hesabındaki Hello kopyasını yalnızca birkaç saniye (benzer tooSAN donanım anlık görüntüleri yavaş kopyalama ve kopyalama ile yazma oluşturma) alan bir işlemdir. Merhaba VHD dosyasının bir kopyasını oluşturduktan sonra tooa sanal makine ya da bir görüntü tooattach olarak hello VHD toovirtual makinelerin kopyalar kullanımı ekleyebilirsiniz.

##### <a name="powershell"></a>PowerShell
```powershell
# attach a vhd tooa vm
$vm = Get-AzureRmVM -ResourceGroupName <resource group name> -Name <vm name>
$vm = Add-AzureRmVMDataDisk -VM $vm -Name newdatadisk -VhdUri <path toovhd> -Caching <caching option> -DiskSizeInGB $null -Lun <lun e.g. 0> -CreateOption attach
$vm | Update-AzureRmVM

# attach a copy of hello vhd tooa vm
$vm = Get-AzureRmVM -ResourceGroupName <resource group name> -Name <vm name>
$vm = Add-AzureRmVMDataDisk -VM $vm -Name newdatadisk -VhdUri <new path of vhd> -SourceImageUri <path tooimage vhd> -Caching <caching option> -DiskSizeInGB $null -Lun <lun e.g. 0> -CreateOption fromImage
$vm | Update-AzureRmVM
```
##### <a name="cli"></a>CLI
```
azure config mode arm

# attach a vhd tooa vm
azure vm disk attach <resource group name> <vm name> <path toovhd>

# attach a copy of hello vhd tooa vm
# this scenario is currently not possible with Azure CLI. A workaround is toomanually copy hello vhd toohello destination.
```

#### <a name="9789b076-2011-4afa-b2fe-b07a8aba58a1"></a>Azure depolama hesapları arasında diskleri kopyalama
Bu görev hello Azure portalı üzerinde gerçekleştirilemiyor. ISE Azure PowerShell cmdlet'leri, Azure CLI veya bir üçüncü taraf depolama tarayıcı kullanabilirsiniz. PowerShell cmdlet'leri hello veya CLI komutları oluşturabilir ve depolama hesapları ve hello Azure aboneliği içindeki bölgeler arasında hello özelliği tooasynchronously kopyalama BLOB'ları içeren BLOB yönetebilirsiniz.

##### <a name="powershell"></a>PowerShell
VHD'ler abonelikler arasında kopyalama de mümkündür. Daha fazla bilgi için okuma [bu makalede][storage-powershell-guide-full-copy-vhd].

Merhaba PS cmdlet mantığı Hello temel akışı şu şekildedir:

* İle Merhaba kaynak depolama hesabı için bir depolama hesabı bağlamını oluşturun *yeni AzureStorageContext* -bkz <https://msdn.microsoft.com/library/dn806380.aspx>
* İle Merhaba hedef depolama hesabı için bir depolama hesabı bağlamını oluşturun *yeni AzureStorageContext* -bkz <https://msdn.microsoft.com/library/dn806380.aspx>
* Merhaba kopyayla Başlat

```powershell
Start-AzureStorageBlobCopy -SrcBlob <source blob name> -SrcContainer <source container name> -SrcContext <variable containing context of source storage account> -DestBlob <target blob name> -DestContainer <target container name> -DestContext <variable containing context of target storage account>
```

* Döngü ile Merhaba kopyasında Hello durumunu denetleme

```powershell
Get-AzureStorageBlobCopyState -Blob <target blob name> -Container <target container name> -Context <variable containing context of target storage account>
```

* Yukarıda açıklandığı gibi Hello yeni VHD tooa sanal makine ekleyin.

Örnekler için bkz [bu makalede][storage-powershell-guide-full-copy-vhd]

##### <a name="cli"></a>CLI
* Merhaba kopyayla Başlat

```
  azure storage blob copy start --source-blob <source blob name> --source-container <source container name> --account-name <source storage account name> --account-key <source storage account key> --dest-container <target container name> --dest-blob <target blob name> --dest-account-name <target storage account name> --dest-account-key <target storage account name>
```

* Merhaba, Hello durumunu denetlemek döngü ile kopyalama

```
azure storage blob copy show --blob <target blob name> --container <target container name> --account-name <target storage account name> --account-key <target storage account name>
```

* Yukarıda açıklandığı gibi Hello yeni VHD tooa sanal makine ekleyin.

Örnekler için bkz [bu makalede][storage-azure-cli-copy-blobs]

### <a name="disk-handling"></a>Disk işleme
#### <a name="4efec401-91e0-40c0-8e64-f2dceadff646"></a>SAP dağıtımları için VM/VHD yapısı
İdeal olarak bir VM hello yapısını işlenmesini hello ve ilişkili hello VHD'ler çok basit olmalıdır. Şirket içi yüklemelerde sunucu yüklemesi yapılandırılması, birçok yolu müşteriler geliştirmiştir.

* Merhaba işletim sistemi içeren bir temel VHD ve tüm hello ikili dosyaları DBMS ve/veya SAP hello. Mart 2015 tarihinden itibaren bu VHD boyutu, sınırlı önceki kısıtlamaları yerine too1TB yukarı too127GB olabilir.
* Bir ya da (Merhaba DBMS destekliyorsa), hello SAP veritabanının hello DBMS günlük dosyasını ve hello DBMS geçici depolama alanı hello günlük dosyası içeren birden çok VHD. Merhaba veritabanı günlük IOPS gereksinimleri yüksekse, sipariş tooreach hello IOPS toplu gereken birden çok VHD toostripe gerekir.
* Hello SAP veritabanında bir veya iki veritabanı dosyalarının ve hello DBMS geçici veri dosyalarını da (Merhaba DBMS destekliyorsa) içeren VHD sayısı.

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
Merhaba DBMS veri dosyaları ve Azure üzerinde barındırılan bu VHD depolama hello türü için kullanılan VHD'ler Hello sayısı hello IOPS gereksinimleri ve gerekli hello gecikme tarafından belirlenmesi. Tam kotaları açıklanmıştır [bu makalede][virtual-machines-sizes]

Son 2 yıl SAP dağıtımları hello üzerinden deneyimi bize olarak özetlenir bazı dersleri öğrettin:

* IOPS trafiği toodifferent veri dosyalarını değil her zaman aynı varolan müşteri sistemleri farklı veri boyutta beri kendi SAP veritabanları temsil eden dosyaları hello. Sonuç olarak LUN olanlar dışında yontulmuş birden çok VHD tooplace hello veri dosyaları üzerinde daha iyi bir RAID Yapılandırması'nı kullanarak toobe kullanıma açık. Özellikle Azure standart depolama burada isabet bir IOPS oranı hello kota hello DBMS işlem günlüğü karşı tek VHD ile durumlarda vardı. Premium depolama gibi senaryoları hello kullanımda önerilir veya alternatif olarak bir yazılım RAID ile birden çok standart depolama VHD toplama.

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

Bu hello hello işletim sistemi içeren VHD göz önünde bulundurun ve öneririz gibi SAP ikili dosyaları hello ve hello veritabanı (temel VM) de artık sınırlı too127GB değil. Artık too1TB boyutu yukarı olabilir. Bu yeterli alan tookeep olması gereken tüm gerekli dosya örn. SAP toplu iş günlükleri de dahil olmak üzere hello.

Daha fazla öneri ve özellikle DBMS VM'ler için daha fazla ayrıntı hello Lütfen başvurun [DBMS Dağıtım Kılavuzu][dbms-guide]

#### <a name="disk-handling"></a>Disk işleme
Çoğu senaryoda VM hello toocreate ek diskleri sipariş toodeploy hello SAP veritabanında gerekir. Biz VHD'ler sayısının bölümdeki hello hakkında dikkat edilecek noktalar açıklandı [SAP dağıtımları için VM/VHD yapısı] [ planning-guide-5.5.1] bu belgenin. Hello Azure Portal tooattach sağlar ve bir taban VM dağıtıldıktan sonra Disk ayırma. Merhaba diskler bağlı/ayrılmış hello VM yukarı olduğunda ve ne zaman durduruldu yanı sıra çalışan olabilir. Bir disk eklerken hello Azure Portal tooattach boş disk sunar. veya bu anda olmayan bir mevcut disk tooanother VM eklendi.

**Not**: VHD ekli tooone VM yalnızca belirli bir zamanda olabilir.

![Attach / detach Azure Standard Storage disklerle][planning-guide-figure-1400]

(Bu, aynı depolama hesabındaki temel VM hello içinde aynıdır hello oluşturulması) yeni ve boş bir VHD veya tooselect kullanılabilir olmalı ve daha önce yüklenen varolan bir VHD'yi toohello VM şimdi bağlı isteyip istemediğinizi toocreate istediğinizi toodecide gerekir.

**Önemli**:, **yok** toouse ana bilgisayar önbelleğe alma standart Azure Storage ile istiyor. Hiçbiri hello varsayılan olarak hello konak önbelleği tercihi bırakmanız gerekir. Merhaba g/ç özelliğini genellikle normal g/ç trafiği veritabanı veri dosyası gibi salt okunur ise Azure Premium Storage ile okuma önbelleği etkinleştirmeniz gerekir. Veritabanı işlem günlüğü dosyasını durumunda, önbelleğe alma önerilir.

- - -
> ![Windows][Logo_Windows] Windows
>
> [Nasıl tooattach bir veri diski hello Azure portalı][virtual-machines-windows-attach-disk-portal]
>
> Diskleri bağlıysa, hello VM tooopen hello Windows Disk Yöneticisi'ni de toolog gerekir. Otomatik bağlama bölümde önerildiği gibi etkin değilse [bağlı diskler için otomatik bağlama ayarı][planning-guide-5.5.3], hello yeni eklenen birim gereken çevrimiçi alınır ve başlatılan toobe.
>
> ![Linux][Logo_Linux] Linux
>
> Diskleri bağlıysa, toolog içinde VM hello ve gerekir açıklandığı gibi hello diskleri başlatma [bu makalede][virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]
>
>

- - -
Merhaba yeni disk boş disk ise, tooformat hello de disk gerekir. Biçimlendirme için özellikle DBMS için hello çıplak dağıtımlar için olduğu gibi aynı önerileri DBMS geçerli veri ve günlük dosyaları hello.

Zaten bölümde belirtildiği [Microsoft Azure sanal makine kavram hello][planning-guide-3.2], bir Azure Storage hesabı g/ç birim bakımından sonsuz kaynaklarını sağlamıyor IOPS ve veri birimi. Genellikle DBMS VM'ler en bu tarafından etkilenir. Sipariş toostay hello Azure depolama hesabı toplu hello sınırının içinde birkaç yüksek g/ç birim VM'ler toodeploy varsa en iyi toouse her VM için ayrı bir depolama hesabı olabilir. Toosee gerekir aksi takdirde, bu sanal makineleri tek her depolama hesabının hello sınırını basarsa olmadan farklı depolama hesapları arasında nasıl dengeleyebilirsiniz. Daha fazla ayrıntı hello açıklanan [DBMS Dağıtım Kılavuzu'na][dbms-guide]. Ayrıca, saf SAP uygulama server Vm'lerinin veya ek VHD'ler sonunda gerektirebilir diğer VM'ler için aklınızda sınırlamalara tutmanız gerekir.

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
> * [DiskPart komut satırı seçenekleri](https://technet.microsoft.com/library/cc766465.aspx)
> * [Otomatik bağlama](http://technet.microsoft.com/library/cc753703.aspx)
>
> Yönetici olarak Hello Windows komut satırı penceresi açık olmalıdır.
>
> Diskleri bağlıysa, hello VM tooopen hello Windows Disk Yöneticisi'ni de toolog gerekir. Otomatik bağlama bölümde önerildiği gibi etkin değilse [bağlı diskler için otomatik bağlama ayarı][planning-guide-5.5.3], hello yeni birim bağlı > Çevrimiçi alınır ve başlatılan toobe gerekiyor.
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
> * Toogive hello ihtiyacınız Hello son adımda hello Sihirbazı, bir ad kural ve 'Son' tuşuna basarak hello kural kaydedin
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

açıklandığı gibi: <https://help.sap.com/saphelp_nwpi71/helpdata/en/47/c56a6938fb2d65e10000000a42189c/content.htm>

## <a name="96a77628-a05e-475d-9df3-fb82217e8f14"></a>SAP örneklerinin yalnızca bulut dağıtımının kavramları
### <a name="3e9c3690-da67-421a-bc3f-12c520d99a30"></a>SAP demo/senaryo eğitimi NetWeaver tek VM
![Tek başına VM SAP Demo sistemler hello ile aynı VM adları çalıştıran, yalıtılmış Azure bulut Hizmetleri][planning-guide-figure-1700]

Bu senaryoda (bölüm bkz [yalnızca bulut] [ planning-guide-2.1] bu belgenin) biz hello tam eğitim/tanıtım senaryo tek bir VM içinde barındırılan burada tipik eğitim/tanıtım sistem senaryosu uygulama. Merhaba dağıtım VM görüntü şablonları üzerinden yapılır varsayalım. Ayrıca bu hello sahip hello VM'ler ile dağıtılan bu demo/eğitimleri VM'ler gerek toobe katları aynı varsayıyoruz adı.

Merhaba varsayılır bölüm bazı bölümlerinde açıklandığı gibi bir VM görüntüsü oluşturulan [SAP Azure VM'lerin hazırlanıyor] [ planning-guide-5.2] bu belgedeki.

olayları tooimplement hello senaryonun Hello dizisi şöyle görünür:

[comment]: <> (MShermannd Yapılacaklar sahip tooprovide ARM örnek / açıklaması kullanarak json şablonunu + ARM sanal ağ içinde benzersiz VM adı ile ilgili açıklama)   
##### <a name="powershell"></a>PowerShell
* Her eğitim/tanıtım yatay için yeni bir kaynak kaydının grubu oluştur

```powershell
$rgName = "SAPERPDemo1"
New-AzureRmResourceGroup -Name $rgName -Location "North Europe"
```

* Yeni depolama hesabı oluşturma

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
# $vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -PublisherName "SUSE" -Offer "SLES" -Skus "12" -Version "latest"
# $vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -PublisherName "RedHat" -Offer "RHEL" -Skus "7.2" -Version "latest"
# $vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Linux -ComputerName "SAPERPDemo" -Credential $cred

$vmconfig = Add-AzureRmVMNetworkInterface -VM $vmconfig -Id $nic.Id

$diskName="os"
$osDiskUri=$account.PrimaryEndpoints.Blob.ToString() + "vhds/" + $diskName  + ".vhd"
$vmconfig = Set-AzureRmVMOSDisk -VM $vmconfig -Name $diskName -VhdUri $osDiskUri -CreateOption fromImage
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

$vm = New-AzureRmVM -ResourceGroupName $rgName -Location "North Europe" -VM $vmconfig
```

* İsteğe bağlı olarak ek disk ekleyin ve gerekli içerik geri yükleyin. Tüm blob adları (URL'leri toohello BLOB'lar) Azure içinde benzersiz olduğunu unutmayın.

```powershell
# Optional: Attach additional data disks
$vm = Get-AzureRmVM -ResourceGroupName $rgName -Name SAPERPDemo
$dataDiskUri = $account.PrimaryEndpoints.Blob.ToString() + "vhds/datadisk.vhd"
Add-AzureRmVMDataDisk -VM $vm -Name datadisk -VhdUri $dataDiskUri -DiskSizeInGB 1023 -CreateOption empty | Update-AzureRmVM
```

##### <a name="cli"></a>CLI
Aşağıdaki örnek kod hello Linux üzerinde kullanılabilir. Windows, lütfen PowerShell yukarıda açıklandığı gibi kullanın veya hello örnek toouse % rgName %$rgName yerine uyum hem hello Windows komutunu kullanarak hello ortam değişkenini *ayarlamak*.

* Her eğitim/tanıtım yatay için yeni bir kaynak kaydının grubu oluştur

```
rgName=SAPERPDemo1
rgNameLower=saperpdemo1
azure group create $rgName "North Europe"
```

* Yeni depolama hesabı oluşturma

```
azure storage account create --resource-group $rgName --location "North Europe" --kind Storage --sku-name LRS $rgNameLower
```

* Yeni bir sanal ağ oluştur her eğitim/tanıtım yatay tooenable hello kullanımını hello için aynı ana bilgisayar adı ve IP adresleri. Merhaba sanal ağ, yalnızca SSH için trafiği tooport 3389 tooenable Uzak Masaüstü erişimi ve bağlantı noktası 22 izin veren bir ağ güvenlik grubu tarafından korunuyor.

```
azure network nsg create --resource-group $rgName --location "North Europe" --name SAPERPDemoNSG
azure network nsg rule create --resource-group $rgName --nsg-name SAPERPDemoNSG --name SAPERPDemoNSGRDP --protocol \* --source-address-prefix \* --source-port-range \* --destination-address-prefix \* --destination-port-range 3389 --access Allow --priority 100 --direction Inbound
azure network nsg rule create --resource-group $rgName --nsg-name SAPERPDemoNSG --name SAPERPDemoNSGSSH --protocol \* --source-address-prefix \* --source-port-range \* --destination-address-prefix \* --destination-port-range 22 --access Allow --priority 101 --direction Inbound

azure network vnet create --resource-group $rgName --name SAPERPDemoVNet --location "North Europe" --address-prefixes 10.0.1.0/24
azure network vnet subnet create --resource-group $rgName --vnet-name SAPERPDemoVNet --name Subnet1 --address-prefix 10.0.1.0/24 --network-security-group-name SAPERPDemoNSG
```

* Merhaba kullanılan tooaccess hello sanal makineden olabilecek yeni bir ortak IP adresi oluşturma Internet

```
azure network public-ip create --resource-group $rgName --name SAPERPDemoPIP --location "North Europe" --domain-name-label $rgNameLower --allocation-method Dynamic
```

* Merhaba sanal makine için yeni bir ağ arabirimi oluştur

```
azure network nic create --resource-group $rgName --location "North Europe" --name SAPERPDemoNIC --public-ip-name SAPERPDemoPIP --subnet-name Subnet1 --subnet-vnet-name SAPERPDemoVNet
```

* Bir sanal makine oluşturun. Merhaba yalnızca bulut senaryosu için her VM hello olacaktır aynı adı. Merhaba hello SAP NetWeaver bu VM'lerin durumlarda olacaktır SAP SID'si hello aynı de. Azure kaynak grubu içinde hello hello VM hello adını toobe benzersiz gerekiyor, ancak farklı Azure kaynak gruplarını VM'ler ile Merhaba çalıştırabilirsiniz aynı adı. Varsayılan 'Yönetici' hesabının Windows hello veya Linux ' kök' geçerli değil. Bu nedenle, yeni bir yönetici kullanıcı adı ile birlikte bir parola tanımlanan toobe gerekir. Merhaba VM Hello boyutu da tanımlanan toobe gerekir.

```
azure vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nic-name SAPERPDemoNIC --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest --os-type Windows --admin-username <username> --admin-password <password> --vm-size Standard_D11 --os-disk-vhd https://$rgNameLower.blob.core.windows.net/vhds/os.vhd --disable-boot-diagnostics
# azure vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nic-name SAPERPDemoNIC --image-urn SUSE:SLES:12:latest --os-type Linux --admin-username <username> --admin-password <password> --vm-size Standard_D11 --os-disk-vhd https://$rgNameLower.blob.core.windows.net/vhds/os.vhd --disable-boot-diagnostics
# azure vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nic-name SAPERPDemoNIC --image-urn RedHat:RHEL:7.2:latest --os-type Linux --admin-username <username> --admin-password <password> --vm-size Standard_D11 --os-disk-vhd https://$rgNameLower.blob.core.windows.net/vhds/os.vhd --disable-boot-diagnostics
```

```
#####
# Create a new virtual machine with a VHD that contains hello private image that you want toouse
#####
azure vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nic-name SAPERPDemoNIC --os-type Windows --admin-username <username> --admin-password <password> --vm-size Standard_D11 --os-disk-vhd https://$rgNameLower.blob.core.windows.net/vhds/os.vhd -Q <path tooimage vhd> --disable-boot-diagnostics
#azure vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nic-name SAPERPDemoNIC --os-type Linux --admin-username <username> --admin-password <password> --vm-size Standard_D11 --os-disk-vhd https://$rgNameLower.blob.core.windows.net/vhds/os.vhd -Q <path tooimage vhd> --disable-boot-diagnostics
```

* İsteğe bağlı olarak ek disk ekleyin ve gerekli içerik geri yükleyin. Tüm blob adları (URL'leri toohello BLOB'lar) Azure içinde benzersiz olduğunu unutmayın.

```
# Optional: Attach additional data disks
azure vm disk attach-new --resource-group $rgName --vm-name SAPERPDemo --size-in-gb 1023 --vhd-name datadisk
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

#### <a name="setup-network-for-communication-between-hello-different-vms"></a>Kurulum ağ arasındaki iletişim için hello farklı sanal makineler
![Bir Azure sanal ağ içindeki VM'ler kümesi][planning-guide-figure-1900]

aynı eğitim/tanıtım Windows'un hello klonlar ile çakışma adlandırma tooprevent için her yatay toocreate bir Azure sanal ağı gerekir. DNS ad çözümlemesi Azure tarafından sağlanacak veya Azure (toobe daha fazla burada tartışılan) dışında kendi DNS sunucusunu yapılandırabilirsiniz. Bu senaryoda, biz kendi DNS yapılandırmayın. Bir Azure sanal ağı içindeki tüm sanal makineler için ana bilgisayar adları üzerinden iletişim etkinleştirilecek.

Merhaba tooseparate eğitim veya tanıtım Windows'un sanal ağlar ve yalnızca kaynak grupları olabilir tarafından nedenleri:

* Merhaba SAP yatay gereksinimlerini ayarlandığı kendi AD/OpenLDAP ve her bir hello Windows'un bir etki alanı sunucusu gereksinimlerini toobe bölümü.  
* ayarlama, gerek toowork sabit IP adresleriyle bileşenleri taşıdığından SAP yatay hello.

Azure sanal ağlar ve nasıl toodefine bunları bulunabilir hakkında daha fazla ayrıntı [bu makalede][virtual-networks-create-vnet-arm-pportal].

## <a name="deploying-sap-vms-with-corporate-network-connectivity-cross-premises"></a>SAP VM'ler şirket ağ bağlantısı (şirket içi) ile dağıtma
SAP yatay çalıştırın ve çıplak için birinci sınıf DBMS sunucuları arasında toodivide hello dağıtım istiyorsanız, SAP sistemleri ve Azure Iaas şirket içi sanallaştırılmış ortamlar uygulama katmanları ve daha küçük 2 katmanı için yapılandırılmış. Merhaba temel bir SAP yatay içinde SAP sistemleri toocommunicate birbirleriyle ve hello şirkette, kendi dağıtım biçiminde bağımsız dağıtılan birçok diğer yazılım bileşenleri ile gerektiğini varsayılır. Ayrıca olmamalıdır hello son SAP GUI veya diğer arabirimleri ile bağlanan kullanıcı için hello dağıtım form tarafından sunulan herhangi bir fark. Biz varsa, bu koşullar yalnızca karşılanabilir hello şirket içi Active Directory/OpenLDAP ve DNS hizmetleri genişletilmiş toohello site-için-site/çok siteler bağlantısı veya Azure ExpressRoute gibi özel bağlantıları üzerinden Azure sistemler.

Daha fazla arka plan SAP azure'da hello uygulama ayrıntılarını üzerinde sipariş tooget içinde tooread bölüm öneririz [kavramları, Cloud-Only dağıtım SAP örneklerinin] [ planning-guide-7] açıklayan bu belgenin hello temelleri bazıları oluşturur, Azure ve nasıl bunlar Azure SAP uygulamalarda kullanılmalıdır.

### <a name="scenario-of-a-sap-landscape"></a>SAP yatay senaryosu
Merhaba şirketler arası senaryo, kabaca grafik hello aşağıdaki gibi açıklanabilir:

![Şirket içi ve Azure varlıklar arasında siteden siteye bağlantı][planning-guide-figure-2100]

Merhaba yukarıda gösterilen senaryo burada hello şirket içi AD/OpenLDAP bir senaryoyu açıklar ve DNS tooAzure genişletilir. Merhaba şirket içi tarafında, belirli bir IP adres aralığı Azure abonelik başına ayrılmıştır. Başlangıç IP adresi aralığı tooan Azure Virtual Network hello Azure yan üzerinde atanır.

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
Son 12 ay Hello seyri içinde Microsoft ya da Vcpu, bellek sayısı farklı pek çok daha fazla VM türleri eklenmiş veya daha önemli donanım üzerinde çalıştığı. Bu tüm VM'lerin SAP ile desteklenir (bkz: desteklenen VM SAP Not türlerinde [1928533]). Bu VM'lerin bazıları farklı ana bilgisayar donanım nesli üzerinde çalıştırın. Bu konak donanım nesli yer hello ayrıntı düzeyi, bir Azure ölçek birimi dağıtılır. Burada seçtiğiniz çalıştırılamaz hello farklı VM boyutları aynı ölçek birimi hello anlamına gelir durumlarda gerçekleşebilir. Bir kullanılabilirlik kümesi hello özelliği toospan ölçek birimleri farklı donanımda sınırlıdır.  Örneğin tek bir SAP sistem ya da farklı içinde farklı SAP sistemleri kullanılabilirlik ayarlar, istediğiniz varsa toorun A5 A11 vm'lerde DBMS hello ve SAP uygulama katmanı G-serisi vm'lerde Merhaba, zorla toodeploy olacaktır.

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
> * Merhaba ortak Linux kılavuzları için izlemeniz yeterlidir [SUSE](https://www.suse.com/documentation/sles-12/book_sle_deployment/data/sec_y2_hw_print.html) veya [Red Hat](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/sec-Printer_Configuration.html) nasıl tooadd yazıcı.
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
> Hello Azure VM hello Windows Gezgini ve hello yazıcı hello paylaşım adında türünü açın.
> Bir yazıcı Yükleme Sihirbazı'nı hello yükleme işleminde size kılavuzluk.
>
> ![Linux][Logo_Linux] Linux
>
> İşte bazı örnekler içinde Linux ağ yazıcıları yapılandırma veya bölüm de dahil olmak üzere ilgili belgelerin Linux içinde yazdırma ilgili. Merhaba çalışacak şekilde Azure Linux VM'de VM hello sürece VPN bir parçasıdır:
>
> * SLES <https://en.opensuse.org/SDB:Printing_via_SMB_ (Samba) _Share_or_Windows_Share>
> * RHEL <https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/s1-printing-smb-printer.html>
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

* Hello Azure geliştirme sisteminde toohello taşıma sistemi (istemci 000) gidin ve işlem STMS çağırın. Diğer yapılandırma hello iletişim kutusundan seçin ve etki alanındaki dahil sistemiyle devam edin. Merhaba etki alanı denetleyicisi hedef konak belirtin ([SAP sistemlerinde de dahil olmak üzere hello aktarım etki alanı](http://help.sap.com/erp2005_ehp_04/helpdata/en/44/b4a0c17acc11d1899e0000e829fbbd/content.htm?frameset=/en/44/b4a0b47acc11d1899e0000e829fbbd/frameset.htm)). Merhaba sistem hello aktarım etki alanında bulunan bekleme toobe sunulmuştur.
* Güvenlik nedenleriyle, ardından isteğiniz toogo geri toohello etki alanı denetleyicisi tooconfirm sahip. Sisteme genel bakış ve Onayla seçim hello bekleme sistemi. Ardından hello istem ve hello yapılandırma dağıtılmış onaylayın.

Bu SAP Sistem şimdi tüm hello hakkında gerekli bilgileri hello diğer SAP sistemlerinde hello aktarım etki alanı içerir. Merhaba aynı zaman hello adresi hello yeni SAP sisteminin veri tooall hello diğer SAP sistemleri ve hello SAP sistem hello aktarım profilinde hello aktarım denetimin programının girilen gönderilir. RFC'leri ve erişim toohello aktarım dizini hello etki alanının çalışıp çalışmadığını denetleyin.

Her zamanki gibi hello belgelerinde açıklandığı gibi aktarım sisteminizin Hello yapılandırmaya devam [değiştirme ve taşıma sistemi](http://help.sap.com/saphelp_nw70ehp3/helpdata/en/48/c4300fca5d581ce10000000a42189c/content.htm?frameset=/en/44/b4a0b47acc11d1899e0000e829fbbd/frameset.htm).

Nasıl yapılır:

* Şirket içi, STMS doğru yapılandırıldığından emin olun.
* Merhaba hostname hello aktarım etki alanı denetleyicisi, sanal makinenize Azure ve tersine visa çözülebilir emin olun.
* İşlem STMS diğer yapılandırma -> çağrı -> Sistem etki alanındaki içerir.
* Şirket içi TMS sistemde hello Hello bağlantısında onaylayın.
* Taşıma yolları, grupları ve Katmanlar her zamanki gibi yapılandırın.

Siteden siteye bağlanan şirketler arası senaryolarda, şirket içi ve Azure arasında hello gecikme hala önemli olabilir. Geliştirme ve test sistemleri tooproduction nesnelerde taşıma hello sırası izleyin veya taşımaları uygulama hakkında düşünün veya destek paketleri toohello farklı sistemleri, fark hello merkezi aktarım hello konumunu bağımlı Dizin, bazı hello sistemlerinin veri okunurken veya hello merkezi aktarım dizininde yazılırken yüksek gecikme karşılaşır. Merhaba benzer tooSAP yatay yapılandırmaları hello farklı sistemleri hello veri merkezleri arasında önemli uzaklıklı farklı veri merkezleri aracılığıyla burada yayılır durumdur.

İçinde bu tür gecikme geçici toowork sipariş ve hızlı okuma veya iki STMS taşıma ve etki alanları (bir şirket içi. bir Azure ve bağlantı hello aktarım etki alanlarında hello sistemleriyle Kurulum hello aktarım dizininden tooor yazma çalışma hello sistemleri Lütfen bu kavram hello SAP TMS olarak arkasında hello ilkeleri açıklayan bu belgelere bakın: <http://help.sap.com/saphelp_me60/helpdata/en/c4/6045377b52253de10000009b38f889/content.htm?frameset=/en/57/ 38dd924eb711d182bf0000e829fbfe/frameset.htm>.

Nasıl yapılır:

* Her bir konum (şirket içi ve Azure) aktarım etki alanı ayarlama işlemi STMS kullanarak <http://help.sap.com/saphelp_nw70ehp3/helpdata/en/44/b4a0b47acc11d1899e0000e829fbbd/content.htm>
* Merhaba etki alanlarını etki alanı ile bağlantıyı ve hello iki etki alanı arasında hello bağlantı onaylayın.
  <http://help.SAP.com/saphelp_nw73ehp1/helpdata/en/a3/139838280c4f18e10000009b38f8cf/Content.htm>
* Merhaba yapılandırma bağlı toohello sistemi dağıtın.

#### <a name="rfc-traffic-between-sap-instances-located-in-azure-and-on-premises-cross-premises"></a>Azure ve şirket içi (şirket içi) bulunan SAP örnekleri arasında RFC trafiği
RFC trafiği şirket içi sistemlerini arasında ve azure'a toowork gerekir. toosetup bağlantı çağrısı işlem SM59 kaynak sistemde toodefine gereken yeri bir RFC bağlantısı hello hedef sistem bulunun. Merhaba, RFC bir bağlantının benzer toohello standart kurulum yapılandırmadır.

Merhaba şirketler arası senaryosunda, aynı etki alanı içinde olan birbirleriyle toocommunicate gereken çalışma SAP sistemleri hello VM'ler hello varsayalım. Bu nedenle hello SAP sistemleri arasında bir RFC bağlantısı kurulumu hello kurulum adımlarını ve şirket içi senaryolarda girişleri farklı değildir.

#### <a name="accessing-local-fileshares-from-sap-instances-located-in-azure-or-vice-versa"></a>Azure veya tersi bulunan SAP örneklerinden erişilirken 'local' fileshares
Azure'da bulunan SAP örnekleri hello Kurumsal şirket içinde olan tooaccess dosya paylaşımları gerekir. Ayrıca, şirket içi SAP örnekleri Azure'da bulunan tooaccess dosya paylaşımları gerekir. tooenable hello dosya paylaşımları hello izinleri ve paylaşım seçeneklerini hello yerel sistemde yapılandırmanız gerekir. Merhaba VPN veya Azure ve veri merkeziniz arasında ExpressRoute bağlantı emin tooopen hello bağlantı noktalarını olun.

## <a name="supportability"></a>Desteklenebilirlik
### <a name="6f0a47f3-a289-4090-a053-2521618a28c3"></a>Azure için SAP izleme çözümü
Sipariş tooenable hello görev kritik SAP sistemlerinin Azure hello SAP üzerinde izleme izleme araçları SAPOSCOL veya SAP konak Aracısı SAP için bir Azure izleme uzantısı aracılığıyla hello Azure sanal makine hizmeti konak verileri alın. SAP tarafından Hello taleplerini belirli tooSAP uygulamaları olduğundan, Microsoft olmayan toogenerically uygulama gerekli hello işlevsellik Azure karar ancak müşteriler toodeploy hello gerekli izleme bileşenleri ve yapılandırmaları tootheir için bırakın Azure'da çalışan sanal makineler. Ancak, bileşenler izleme hello dağıtımı ve yaşam döngüsü yönetimini çoğunlukla Azure tarafından otomatik olarak yapılır.

#### <a name="solution-design"></a>Çözüm tasarımı
Merhaba çözüm Azure VM aracısı ve uzantısı çerçevesini hello mimarisine tabanlı SAP izleme tooenable geliştirmiştir. Merhaba hello Azure VM aracısı ve uzantısı framework'ün bir VM içinde hello Azure VM uzantısı galerisinde kullanılabilir yazılım uygulamaları tooallow yüklemesini olur. tooallow (durumlarda hello Azure Monitoring uzantısı SAP gibi) bu kavramı arkasında fikirdir ilkesine Merhaba, bu tür bir yazılım dağıtım zamanında bir VM ve hello yapılandırmasını özel işlevsellik dağıtımını hello.

Şubat 2014 bu yana hello 'Azure VM Aracısı', VM hello Azure Portal de VM oluşturmayı varsayılan olarak Windows VM'ler eklenen hello içinde belirli Azure VM uzantıları işleme sağlar. SUSE veya Red Hat Linux hello durumunda VM Aracısı zaten Azure Market görüntüsü parçasıdır. Linux VM'den karşıya durumda şirket içi tooAzure hello VM Aracısı el ile yüklenen toobe sahiptir.

SAP şöyle için azure'da hello izleme çözümünün temel yapı taşlarının hello:

![Microsoft Azure uzantısı bileşenleri][planning-guide-figure-2400]

Merhaba blok Yukarıdaki diyagramda gösterildiği gibi bir izleme çözümü için SAP hello parçası hello Azure VM görüntüsü ve Azure işlemleri tarafından yönetilen bir genel çoğaltılan depo Azure uzantısı galerisinde barındırılır. Bunu hello hello Azure SAP toowork uygulamasıyla Azure işlemleri toopublish yeni sürümlerini hello Azure Monitoring uzantısı SAP için çalışan hello birleşik SAP/MS takım sorumluluğundadır. Bu Azure Monitoring uzantısı SAP için hello Microsoft Azure tanılama (WAD) uzantısı veya Linux Azure tanılama (LAD) tooget hello gerekli bilgileri kullanır.

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

Merhaba ilk URI portalıdır http (s):`<Portalserver`>: 5XX00/irj burada hello bağlantı noktası biçimlendirilmiş 50000 tarafından artı (Systemnumber × 100). Merhaba varsayılan portal URI, SAP 00 sistemidir `<dns name`>.`<azure region` >.Cloudapp.azure.com:PublicPort/irj. Daha fazla ayrıntı için bir görünüme sahip bir <http://help.sap.com/saphelp_nw70ehp1/helpdata/de/a2/f9d7fed2adc340ab462ae159d19509/frameset.htm>.

![Uç nokta yapılandırması][planning-guide-figure-2800]

Toocustomize hello URL ve/veya bağlantı noktaları, SAP Enterprise Portal'ın istiyorsanız, bu belgeleri gözden geçirin:

* [Değişiklik portalı URL'si](http://wiki.scn.sap.com/wiki/display/EP/Change+Portal+URL)
* [Varsayılan bağlantı noktası numaralarını, Portal bağlantı noktası numaralarını değiştirme](http://wiki.scn.sap.com/wiki/display/NWTech/Change+Default++port+numbers%2C+Portal+port+numbers)

<a name="7cf991a1-badd-40a9-944e-7baae842a058"></a>
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
Kullanılabilir hiçbir tek VM SLA Azure sanal makinelerde şu anda. tooget hakkında bir fikir hello çarpımını yalnızca oluşturabilirsiniz gibi tek bir VM'ye hello kullanılabilirliğini görünebilir nasıl farklı kullanılabilir Azure SLA hello: <https://azure.microsoft.com/support/legal/sla/>.

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
Microsoft Azure Storage hesabınız Hello veriler her zaman çoğaltılmış tooensure dayanıklılık ve yüksek kullanılabilirlik, hello Azure depolama SLA bile geçici donanım arızalarında hello yüzünü toplantı bağlıdır

Azure Storage hello veri 3 görüntülerini varsayılan olarak engelliyor olduğundan, RAID5 veya birden çok Azure disklere RAID1 yok gerekli.

Bu makalede daha fazla ayrıntı bulunabilir: <http://azure.microsoft.com/documentation/articles/storage-redundancy/>

#### <a name="utilizing-azure-infrastructure-vm-restart-tooachieve-higher-availability-of-sap-applications"></a>Azure VM Altyapı yeniden tooAchieve "Daha yüksek kullanılabilirliğini" SAP uygulamaları kullanma
Değil toouse işlevler gibi Windows Server Yük Devretme Kümelemesi (WSFC) karar verin ya da Linux eşdeğer (ikinci hello bir henüz desteklenmiyor Azure üzerinde SAP yazılım ile birlikte), Azure VM yeniden kullanılan tooprotect SAP sistemine karşı planlanan ve Planlanmamış kapalı kalma süresi hello Azure fiziksel sunucu altyapısı ve genel temel Azure platformu.

> [!NOTE]
> Azure VM yeniden öncelikle VM'ler ve uygulamaları korur, önemli toomention olur. VM yeniden başlatma yok sunar SAP uygulamalar için yüksek kullanılabilirlik, ancak belirli bir düzeyde altyapı kullanılabilirlik sunar ve bu nedenle dolaylı olarak "daha yüksek kullanılabilirliğini" SAP sistemleri. Bu toorestart VM konak planlanmış veya planlanmamış kesinti sonra hello sürmesi için hiçbir SLA bulunmaktadır. Bu nedenle, bu yöntem 'yüksek oranda kullanılabilirlik' SAP sisteminin (A) SCS veya DBMS gibi kritik bileşenleri için uygun değil.
>
>

Başka bir önemli altyapısı için yüksek kullanılabilirlik depolama öğesidir. Örneğin Azure depolama SLA %99,9 kullanılabilirlik ' dir. Varsa, disklerle tüm VM'ler tek Azure depolama hesabı, olası Azure Storage, Azure depolama hesabında yerleştirilir tüm sanal makineleri ve bu VM'lerin içinde çalışan aynı zamanda tüm SAP bileşenleri kullanılamama kullanılamazlık neden olacak içine dağıtır.  

Tüm sanal makineleri tek tek Azure Storage hesabınıza yerine koyma, ayrılmış bir depolama de kullanabilirsiniz hesapları her VM için ve bu şekilde, birden çok bağımsız Azure depolama hesapları kullanarak genel VM ve SAP uygulama kullanılabilirliği artırın.

Azure altyapı kullanan bir SAP NetWeaver sistemin bir örnek mimarisi HA şöyle:

![Azure altyapı HA tooachieve SAP uygulaması "daha yüksek" kullanılabilirlik kullanma][planning-guide-figure-2900]

İçin kritik SAP bileşenleri hello kadarki aşağıdaki elde:

* SAP uygulama sunucuları (AS) yüksek kullanılabilirlik

SAP uygulama sunucu örnekleri yedekli bileşenleridir. Her SAP örneği farklı bir Azure hata ve yükseltme etki alanında çalışan kendi VM üzerinde dağıtıldığında (bölümlere bakın [hata etki alanlarını] [ planning-guide-3.2.1] ve [yükseltme etki alanları][planning-guide-3.2.2]). Bu Azure kullanılabilirlik kümeleri kullanarak sağlamış (bölüm bkz [Azure kullanılabilirlik kümeleri][planning-guide-3.2.3]). Olası planlanmış veya planlanmamış kullanılamama Azure hatası veya yükseltme etki alanı kendi SAP AS VM'ler sınırlı sayıda kullanılamama neden olacak örnekleri.
Örnek, kendi Azure depolama hesabında yerleştirilir – bir Azure depolama hesabı potansiyel olarak kullanım dışı kalması kendi SAP AS ile yalnızca bir VM kullanılamama neden olacak şekilde her SAP örneği. Ancak, bir Azure depolama hesapları sınırı içinde bir Azure aboneliği olduğunu unutmayın. tooensure hello VM yeniden başlatıldıktan sonra (A) SCS örneği otomatik olarak Başlat tooset Autostart parametre (A) SCS örneğinde Başlat bölümde açıklanan profili emin olun [SAP örnekleri için Otomatik Başlat'ı kullanarak][planning-guide-11.5].
Lütfen bölüm okuyun [SAP uygulama sunucuları için yüksek kullanılabilirlik] [ planning-guide-11.4.1] daha fazla ayrıntı için.

* *Daha yüksek* SAP kullanılabilirlik (A) SCS örneği

Burada size Azure VM yeniden tooprotect hello VM yüklü SAP (A) SCS örneğiyle kullanın. Hello Azure planlanmış veya Planlanmamış kapalı kalma süresi durumunun sunucularının, sanal makineleri başka bir kullanılabilir sunucusunda yeniden başlatılacak. Daha önce belirtildiği gibi Azure VM yeniden öncelikle VM'ler ve uygulamaları korur, (A) SCS örneği bu durumda hello. Merhaba VM yeniden biz dolaylı olarak SAP (A) SCS örneğinin "daha yüksek kullanılabilirlik" ulaşması. tooinsure hello VM yeniden başlatıldıktan sonra (A) SCS örneği otomatik olarak Başlat tooset Autostart parametre (A) SCS örneğinde Başlat bölümde açıklanan profili emin olun [SAP örnekleri için Otomatik Başlat'ı kullanarak][planning-guide-11.5]. Bu, tek bir VM'de çalıştıran hello (A) SCS örneği bir tek hata noktası (SPOF) olarak hello tüm SAP yatay hello kullanılabilirliğini determinative çarpanını hello anlamına gelir.

* *Daha yüksek* DBMS sunucu kullanılabilirliği

Burada, benzer toohello SAP (A) SCS örnek kullanım örneği, size Azure VM yeniden tooprotect hello VM yüklü DBMS yazılımıyla kullanmak ve biz "daha yüksek kullanılabilirliğini" DBMS yazılım VM yeniden aracılığıyla elde etmek.
Tek bir VM'de çalıştıran DBMS ayrıca bir SPOF ve hello tüm SAP yatay hello kullanılabilirliğini determinative çarpanını hello şeklindedir.

### <a name="sap-application-high-availability-on-azure-iaas"></a>SAP Azure Iaas uygulama yüksek kullanılabilirlik
tooachieve tam SAP sistem yüksek kullanılabilirlik, benzersiz bileşenler (örneğin tek hata noktası) gibi ve tüm kritik SAP sistem bileşenleri, örneğin yedek SAP uygulama sunucuları, tooprotect ihtiyacımız SAP (A) SCS örneği ve DBMS.

#### <a name="5d9d36f9-9058-435d-8367-5ad05f00de77"></a>SAP uygulama sunucuları için yüksek kullanılabilirlik
Merhaba SAP uygulama sunucuları/iletişim örnekleri için belirli yüksek kullanılabilirlik çözümü hakkında gerekli toothink değil. Yüksek kullanılabilirlik artıklık ve böylece yalnızca elde yeterli bunlardan farklı sanal makinelere sahip. Bunlar tüm VM'ler hello aynı Azure kullanılabilirlik kümesi tooavoid hello güncelleştirilmiş hello yerleştirilmelidir planlı bakım kapalı kalma süresi sırasında aynı anda. farklı yükseltme ve hata etki alanı içinde bir Azure ölçek birimi hello temel işlevselliği bölümde zaten sunulmuştur [yükseltme etki alanları][planning-guide-3.2.2]. Azure kullanılabilirlik kümeleri bölümde sunulan [Azure kullanılabilirlik kümeleri] [ planning-guide-3.2.3] bu belgenin.

Hiçbir sonsuz sayıda hata ve yükseltme Azure ölçek birimi içinde Azure kullanılabilirlik kümesi tarafından kullanılan etki alanları yoktur. Bu, bir kullanılabilirlik kümesinde er geç hello aynı hatası veya yükseltme etki alanında birden fazla VM sonlanır hello olgu içine VM'lerin sayısını koyma anlamına gelir

Örnekleri kendi özel VM'ler birkaç SAP uygulama sunucusu dağıtma ve biz 5 yükseltme etki alanları var olduğunu varsayarsak resim aşağıdaki hello hello sonunda ortaya çıkar. Hello gerçek max arıza ve güncelleştirme etki alanlarının sayısı bir kullanılabilirlik kümesi içinde hello gelecekteki değiştirebilirsiniz:

![HA azure'da SAP uygulama sunucuları][planning-guide-figure-3000]

Bu belgede daha fazla ayrıntı bulunabilir: <http://azure.microsoft.com/documentation/articles/virtual-machines-manage-availability>

#### <a name="high-availability-for-hello-sap-ascs-instance-on-windows"></a>Yüksek kullanılabilirlik için Windows hello SAP (A) SCS örneği
Windows Server Yük devretme kümesi (WSFC) bir sık kullanılan çözüm tooprotect hello SAP (A) SCS örneğidir. Ayrıca, "HA yükleme" biçiminde sapinst içine tümleştirilmiştir. Bu anda hello Azure altyapı mümkün tooprovide hello işlevselliği tooset aynı şekilde gerçekleştirilir gibi şirket içi hello gerekli Windows Server Yük devretme hello yedeklemek değildir.

Ocak 2016 itibariyle hello Azure bulut platformu hello Windows işletim sistemi çalıştıran bir Küme Paylaşılan birimi iki Azure VM'ler arasında paylaşılan bir disk kullanarak hello olasılığını sağlamaz.

Geçerli bir çözüm ancak hello WSFC tümleştirilebilir zaman uyumlu ve saydam disk çoğaltma tarafından paylaşılan bir birim sağlayan 3. taraf yazılımların kullanımdır. Bu yaklaşım, yalnızca o hello etkin küme düğümünde hello disk birini zamanında bir noktada kopyalar mümkün tooaccess olduğu anlamına gelir. Bu HA Ocak 2016 itibariyle desteklenen tooprotect hello SAP (A) SCS SIOS DataKeeper 3. taraf yazılımlarla birlikte Windows konuk işletim sistemi Azure vm'lerinde örneğinde yapılandırmadır.

Merhaba SIOS DataKeeper çözüm sağlayarak bir paylaşılan disk küme kaynak tooWindows yük devretme kümeleri sağlar:

* Windows küme yapılandırmasında olan hello sanal makineleri (VM'ler) tooeach bağlı ek bir Azure VHD
* Her iki VM düğümler üzerinde çalışan SIOS DataKeeper Cluster Edition
* SIOS DataKeeper Cluster Edition, zaman uyumlu olarak hello ek Merhaba içeriğine yansıtan bir şekilde yapılandırılmış olan VHD kaynak VM'ler tooadditional bağlı VHD birimden hedef VM birim eklendi.
* SIOS DataKeeper hello kaynak ve hedef yerel birimleri özetleyen ve yük devretme kümesi olarak tek bir paylaşılan disk tooWindows sunma.

Tüm ayrıntılar hakkında yönergeler bulabilirsiniz tooinstall SIOS Datakeeper ve SAP ile Windows Yük devretme hello içinde [SAP ASCS SIOS DataKeeper ile azure'da Windows Server Yük devretme kullanarak örneğini Kümeleme] [ ha-guide-classic]teknik incelemesi.

#### <a name="high-availability-for-hello-sap-ascs-instance-on-linux"></a>Linux hello SAP (A) SCS örneği için yüksek kullanılabilirlik
DEC 2015'ten itibaren ayrıca Azure Linux VM'ler için WSFC eşdeğer tooshared disk yok. Alternatif çözümleri için SIOS Windows gibi 3. taraf yazılım kullanarak SAP Linux Azure üzerinde çalışan için henüz doğrulanmaz.

#### <a name="high-availability-for-hello-sap-database-instance"></a>Merhaba SAP veritabanı örneği için yüksek kullanılabilirlik
Merhaba normal SAP DBMS HA Kurulum iki DBMS Vm'lerde DBMS yüksek kullanılabilirlik işlevselliğini kullanıldığı dayanır hello etkin DBMS örneği toohello tooreplicate verilerden bir pasif DBMS örneğine VM ikinci.

Yüksek kullanılabilirlik ve olağanüstü durum kurtarma işlevi için genel yanı sıra belirli DBMS DBMS hello açıklanan [DBMS Dağıtım Kılavuzu'na][dbms-guide].

#### <a name="end-to-end-high-availability-for-hello-complete-sap-system"></a>Uçtan uca yüksek kullanılabilirlik için hello tam SAP sistem
Bir tam SAP NetWeaver HA mimarisinde Azure - iki örnekleri şunlardır biri Windows ve Linux için bir tane.
Aşağıda açıklandığı gibi hello kavramları biraz hello dağıtılan VM sayısı hello abonelik başına depolama hesaplarının maksimum sınırı aşan ve birçok SAP sistemi dağıttığınızda tehlikeye toobe gerekebilir. Böyle durumlarda, sanal makineleri VHD'ler bir depolama hesabında birleştirilmiş toobe gerekir. Genellikle VHD'ler, SAP uygulama katmanı farklı SAP sistemlerinin VM'ler birleştirerek bunu.  Biz de bir Azure depolama hesabında farklı SAP sistemlerinin farklı DBMS VM'ler farklı VHD'leri birleşik. Böylece Azure depolama hesapları hello IOPS sınırları göz önünde bulundurarak ( <https://azure.microsoft.com/documentation/articles/storage-scalability-targets> )

##### <a name="windowslogowindows-ha-on-windows"></a>![Windows][Logo_Windows] HA Windows
![Azure Iaas SQL Server ile SAP NetWeaver uygulama HA mimarisi][planning-guide-figure-3200]

Azure yapıları aşağıdaki hello hello SAP NetWeaver sistemi toominimize etkisi altyapı sorunları ve düzeltme eki uygulama ana bilgisayar için kullanılır:

* Merhaba tam sistem (gerekli - DBMS katman, (A) SCS örneği ve tam uygulama katmanı gerek toorun aynı konuma hello) Azure üzerinde dağıtılır.
* Merhaba tam sistem (gerekli) bir Azure aboneliği içinde çalışır.
* Merhaba tam sistem bir Azure sanal (gerekli) ağ içinde çalışır.
* Merhaba hello VM'ler bir SAP sisteminin üç kullanılabilirlik kümeleri içine ayrılmasıdır olası toohello ait bile tüm hello VM'ler ile aynı sanal ağ.
* Bir SAP sistem DBMS örneklerini çalışan tüm sanal makineler, bir kullanılabilirlik kümesinde ' dir. SQL Server AlwaysOn veya Oracle Data Guard gibi özellikleri kullanılır, yerel DBMS yüksek kullanılabilirlik bu yana sistem başına DBMS örneği çalıştıran birden fazla VM olduğunu varsayalım.
* DBMS örnekleri çalışan tüm sanal makineler kendi depolama hesabı kullanın. DBMS veri ve günlük dosyaları hello verileri eşitlemek DBMS yüksek kullanılabilirlik işlevler kullanılarak bir depolama hesabı tooanother depolama hesabından çoğaltılır. Bir depolama hesabı olarak kullanım dışı kalması bir SQL Windows Küme düğümü ancak hello tüm SQL Server hizmeti değil kullanılamama neden olur.
* (A) bir SAP sistem SCS örneğini çalışan tüm sanal makineler, bir kullanılabilirlik kümesinde ' dir. Bu VM'lerin içinde Windows Server Yük devretme kümesi (WSFC) tooprotect (A) SCS örneği yapılandırın.
* (A) SCS örnekleri çalışan tüm sanal makineler kendi depolama hesabı kullanın. (A) SCS örnek dosyaları ve SAP genel klasör SIOS DataKeeper çoğaltma'yı kullanarak bir depolama hesabı tooanother depolama hesabından çoğaltılır. Bir depolama hesabı olarak kullanım dışı kalması biri (A) kullanılamama neden olacak SCS Windows Küme düğümü, ancak tüm hello değil (A) SCS hizmet.
* Merhaba SAP uygulama sunucusu katmanı temsil eden tüm hello VM'ler, bir üçüncü kullanılabilirlik kümesinde ' dir.
* SAP uygulama sunucuları çalışan tüm hello sanal makineler kendi depolama hesabı kullanın. Bir depolama hesabı olarak kullanım dışı kalması burada diğer SAP AS devam toorun bir SAP uygulama sunucusu olarak kullanım dışı kalması neden olur.

##### <a name="linuxlogolinux-ha-on-linux"></a>![Linux][Logo_Linux] HA Linux
Hello için SAP HA Linux Azure üzerinde temelde aynı Windows yukarıda açıklanan hello mimarisidir. Ocak 2016 itibariyle iki kısıtlamalar vardır ancak:

* yalnızca SAP ana 16 şu anda Linux Azure üzerinde herhangi bir ana çoğaltma özelliği desteklenir.
* Azure üzerinde Linux'ta henüz desteklenen SAP (A) SCS HA çözümü yoktur

Sonuç olarak Ocak 2016 SAP Linux Azure sistem alamayacağınız gibi HA hello (A) SCS örnek için eksik bir SAP Windows Azure sistemi olarak aynı kullanılabilirlik hello ve tek örnekli SAP ana veritabanı hello.

### <a name="4e165b58-74ca-474f-a7f4-5e695a93204f"></a>SAP örnekleri için Otomatik Başlat'ı kullanma
SAP hello OS hello VM içinde hello başlangıcı hemen sonra toostart SAP örnekleri hello işlevsellik sunmazdı. Merhaba tam adımlar SAP Bilgi Bankası makalesinde belgelenmiş [1909114] - parametre Autostart kullanılarak otomatik olarak toostart SAP örnekleri nasıl. Ancak, SAP hello örneği yeniden başlatıldığında, sırayla hiçbir denetim olduğundan toouse hello artık ayarı VM başına birden çok örneği çalıştırdığınızda veya birden fazla VM etkilenen olduğu varsayılarak öneren değil. Bir süre sonra yeniden tek bir VM VM ve hello durumda bir SAP uygulama sunucusu örneği tipik Azure senaryosunu varsayıldığında, hello Autostart gerçekten kritik değildir ve bu parametre ekleyerek etkinleştirilebilir:

    Autostart = 1

Hello profil hello SAP ABAP ve/veya Java örneğinin başlatın.

> [!NOTE]
> Merhaba Autostart parametre bazı downfalls de sahip olabilir. Merhaba hello örneğinin Windows/Linux hizmeti başlatıldı işlerken daha ayrıntılı olarak hello parametre Tetikleyicileri SAP ABAP veya Java örneğinin başlangıç hello. Merhaba işletim sistemleri yedekleme yüklediğinde, kesinlikle hello durumdur. Ancak, SAP hizmetleri yeniden de SUM gibi SAP yazılım yaşam döngüsü yönetimi işlevleri için ortak bir şey diğer güncelleştirir veya veya yükseltir. Bu işlevler hiç otomatik olarak yeniden örneği toobe beklenmiyor. Bu nedenle, hello Autostart parametresi gibi görevleri çalıştırmadan önce devre dışı bırakılması gerekir. Merhaba Autostart parametresi SCS/ASCS/CI gibi kümelenir SAP örnekleri için de kullanılmamalıdır.
>
>

SAP için autostart'ile ilgili ek bilgiler burada örnekleri bakın:

* [Başlat/Durdur SAP yanı sıra, UNIX sunucusu Başlat/Durdur](http://scn.sap.com/community/unix/blog/2012/08/07/startstop-sap-along-with-your-unix-server-startstop)
* [Başlatma ve durdurma SAP NetWeaver yönetim aracıları](https://help.sap.com/saphelp_nwpi711/helpdata/en/49/9a15525b20423ee10000000a421938/content.htm)
* [Nasıl tooenable otomatik HANA veritabanına, Başlat](http://www.freehanatutorials.com/2012/10/how-to-enable-auto-start-of-hana.html)

### <a name="larger-3-tier-sap-systems"></a>Daha büyük 3 katmanlı SAP sistemleri
3 katmanlı SAP yapılandırmaları yüksek kullanılabilirlik yönlerini zaten önceki bölümlerde ele. Ancak sistemleri hello DBMS sunucu gereksinimleri olduğu çok büyük hakkında toohave Azure'da bulunan, ancak hello SAP uygulama katmanı Azure'da dağıtılan?

#### <a name="location-of-3-tier-sap-configurations"></a>3 katmanlı SAP yapılandırmaları konumu
Şu desteklenen toosplit hello uygulama katmanı kendisini veya Merhaba uygulaması ve şirket içi ve Azure arasında DBMS katmanı değil. SAP sistemidir ya da tamamen şirket içinde dağıtılabilir veya Azure'da. Bu da desteklenen toohave değil Azure'da hello uygulama sunucuları bazıları şirket içi ve diğerlerinin çalıştırın. Başlangıç noktası hello tartışma hello olmasıdır. Biz de toohave hello DBMS SAP sistem bileşenlerinin desteklemediğinden ve SAP uygulama sunucusu katmanı iki farklı Azure bölgelerde dağıtılan hello. Örneğin DBMS Orta ABD, Batı ABD ve SAP uygulama katmanında. Bu tür yapılandırmaları desteklemediğinden için hello gecikme hello SAP NetWeaver mimarisi duyarlılığını nedenidir.

Ancak, geçen yıl veri hello süresince merkezi ortakları ortak konumları tooAzure bölgeler geliştirmiştir. Bu ortak konumları genellikle çok yakın bir yerde konumlandırıldığında toohello fiziksel Azure verinin bir Azure bölgesi merkezlerinizde içindedir. Merhaba kısa uzaklık ve Azure ExpressRoute aracılığıyla konuma ortak hello varlıkları bağlantı 2ms'den az kadar olan bir gecikme neden olabilir. Böyle durumlarda, bu tür bir birlikte bulundurma ve azure'da hello SAP uygulama katmanı toolocate hello DBMS katman (depolama SAN/NAS dahil) mümkündür. DEC 2015'ten itibaren biz tüm dağıtımları gibi yok. Ancak SAP olmayan uygulama dağıtımları farklı müşterilerle zaten bu yaklaşımı kullanarak.

### <a name="offline-backup-of-sap-systems"></a>Çevrimdışı Yedekleme, SAP sistemleri
Merhaba bağımlı (Katman 2 veya 3 katmanlı) var. seçilen SAP yapılandırma gereksinimini toobackup olabilir. Merhaba VM kendisini artı toohave hello veritabanının bir yedeğini Hello içeriği. Merhaba DBMS yedeklemeleri veritabanı yöntemleriyle bitti beklenen toobe ilişkilidir. Ayrıntılı bir açıklama hello farklı veritabanları için bulunabilir [DBMS Kılavuzu][dbms-guide]. Üzerindeki diğer yandan Merhaba, hello SAP veri (Merhaba veritabanı içeriği de dahil) bir çevrimdışı şekilde bu bölümde açıklandığı gibi veya çevrimiçi hello sonraki bölümde açıklandığı gibi yedeklenebilir.

Merhaba Çevrimdışı Yedekleme temelde hello VM hello Azure Portal aracılığıyla kapatılmasını gerektirir ve bir kopyasını hello temel VM disk artı tüm VHD'ler toohello VM bağlı. Bu, hello VM zaman görüntüdeki noktası ve onun ilişkili disk korur. Farklı bir Azure Storage hesabınıza toocopy hello 'yedeklemeleri' önerilir. Bu nedenle bölümde açıklanan yordamı hello [Azure depolama hesapları arasında diskleri kopyalama] [ planning-guide-5.4.2] bu belgenin geçerli olur.
Bunun yanında, kapatma kullanarak hello hello Azure portalı bir de Powershell veya CLI burada açıklandığı gibi bunu yapabilirsiniz: <https://azure.microsoft.com/documentation/articles/virtual-machines-deploy-rmtemplates-powershell/>

Bu durumda, bir geri yükleme hello silmek oluşur hello hello özgün disklerin yanı sıra temel VM VM temel ve VHD takılı, kaydedilen geri hello VHD'ler toohello kopyalama, özgün depolama hesabı ve ardından yeniden dağıtırken sistem hello.
Bu makalede nasıl tooscript bu işlemi bir örnek gösterilmektedir Powershell: <http://www.westerndevs.com/azure-snapshots/>

Lütfen restoing yukarıda açıklandığı gibi bir VM yedeğinin yeni bir donanım anahtarı oluşturduğundan emin tooinstall yeni bir SAP lisans olun.

### <a name="online-backup-of-an-sap-system"></a>SAP sistemin çevrimiçi yedekleme
Hello açıklandığı gibi hello DBMS yedeğini DBMS belirli yöntemleriyle gerçekleştirilir [DBMS Kılavuzu][dbms-guide].

Azure sanal makine yedekleme işlevini kullanarak diğer VM'ler hello SAP sistem içinde yedeklenebilir. Azure sanal makine yedeklemesi erken 2015'te tanıtılan ve bu arada standart yöntemi toobackup bir tam VM azure'da. Azure yedekleme Azure'da hello yedeklemeleri depolar ve geri yükleme bir VM'nin yeniden sağlar.

> [!NOTE]
> DEC 2015'ten itibaren VM Yedekleme kullanarak SAP için kullanılan hello benzersiz VM kimliği korumaz lisans. Bu VM yedekten yeni bir SAP lisans anahtarı yüklemesini hello VM geri gibi değerlendirilir toobe yeni bir VM gerektirdiği anlamına gelir ve yerine geçecek kaydedilmiş olan eski biri değil.
> Ocak 2016 itibariyle Azure VM Backup dağıtılan VM'ler ile Azure Resourc Manager henüz desteklemiyor.
>
> ![Windows][Logo_Windows] Windows
>
> Teorik olarak Hello DBMS sistemlerini destekleyen Windows VSS Merhaba, tutarlı bir şekilde de çalıştırma veritabanları yedeklenebilir VM'ler (birim gölge kopyası hizmeti <https://msdn.microsoft.com/library/windows/desktop/bb968832 (v=vs.85).aspx > ) SQL Server örneğin yaptığı gibi.
> Ancak, zaman içinde nokta geri yükler veritabanları Azure VM yedeklemelerin dayalı mümkün olmayan unutmayın. Bu nedenle, Azure VM Backup kalmak yerine DBMS işlevsellikle veritabanlarının yedeklerini tooperform önerilir
>
> Azure sanal makine yedekleme ile tanıdık tooget Lütfen başlatın burada: <https://azure.microsoft.com/documentation/articles/backup-azure-vms/>.
>
> Diğer olasılıklar toouse birlikte Microsoft Data Protection Manager bir Azure VM ve Azure yedekleme yedekleme/geri yükleme veritabanlarına yüklendiği. Daha fazla bilgi şurada bulunabilir: <https://azure.microsoft.com/documentation/articles/backup-azure-dpm-introduction/>.  
>
> ![Linux][Logo_Linux] Linux
>
> Hiçbir eşdeğer tooWindows Linux VSS yoktur. Bu nedenle yalnızca dosya tutarlı yedeklemeler olası ancak değil uygulamayla tutarlı yedeklemeler altındadır. Merhaba SAP DBMS yedekleme yapılmalıdır DBMS işlevselliğini kullanma. Merhaba hello SAP içeren dosya sistemi veri örneğin tar açıklandığı gibi burada kullanarak kaydedilebilir ilgili: <http://help.sap.com/saphelp_nw70ehp2/helpdata/en/d3/c0da3ccbb04d35b186041ba6ac301f/content.htm>
>
>

### <a name="azure-as-dr-site-for-production-sap-landscapes"></a>Üretim SAP Windows'un için DR sitesi olarak Azure
Mid 2014 bu yana uzantıları toovarious bileşenleri Hyper-V, System Center ve Azure çevresinde şirket üzerinde Hyper-V tabanlı çalışan sanal makineler için DR sitesi olarak Azure hello kullanımını etkinleştirin.

Bu çözümün nasıl toodeploy olan ayrıntılı bir blog burada belgelenen: <http://blogs.msdn.com/b/saponsqlserver/archive/2014/11/19/protecting-sap-solutions-with-azure-site-recovery.aspx>

## <a name="summary"></a>Özet
Hello Azure SAP sistemler için yüksek oranda kullanılabilirlik önemli noktalar şunlardır:

* Merhaba SAP tek hata noktası bu anda, tam olarak korunamıyor şekilde şirket içi dağıtımlarda yapılabilir gibi aynı hello. Merhaba paylaşılan Disk kümelerini henüz Azure'da hello 3 taraf yazılımları kullanmadan oluşturulamıyor, nedenidir.
* Merhaba DBMS katmanı için paylaşılan disk küme teknolojisine bağlı değildir toouse DBMS işlevselliğini gerekir. Ayrıntılar hello belgelenmiştir [DBMS Kılavuzu][dbms-guide].
* toominimize hello etkisi'hello Azure altyapısı veya ana bilgisayar bakım hata etki alanları içindeki sorunları Azure kullanılabilirlik kümeleri kullanmanız gerekir:
  * Toohave bir önerilen hello SAP uygulama katman için kullanılabilirlik kümesi.
  * Merhaba SAP DBMS katman için ayrı bir kullanılabilirlik kümesi toohave önerilir.
  * Farklı SAP sistemleri VM'ler için aynı kullanılabilirlik kümesi tooapply hello önerilmez.
* Merhaba SAP DBMS katman yedekleme amaçları doğrultusunda, lütfen hello denetleyin [DBMS Kılavuzu][dbms-guide].
* Genellikle daha hızlı tooredeploy basit iletişim örnekleri olduğundan SAP iletişim örneği yedekleme az mantıklıdır.
* Tüm hello profilleri hello farklı örneklerinin hello hello genel dizin hello SAP sistem ve onunla içeren VM yedekleme anlamlı ve Windows Yedekleme ile gerçekleştirilmelidir veya Linux'ta örneğin hedef. Daha kolay toobackup olun Windows Server 2008 (R2) ve Windows Server 2012 (R2) arasındaki farklar olduğundan daha yeni hello kullanarak Windows Server sürümleri, toorun Windows konuk işletim sistemi olarak Windows Server 2012 (R2) öneririz.
