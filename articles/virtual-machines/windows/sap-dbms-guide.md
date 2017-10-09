---
title: "aaaSAP NetWeaver – Azure vm'lerinde DBMS Dağıtım Kılavuzu | Microsoft Docs"
description: "SAP NetWeaver Azure sanal makinelerde (VM'ler) – DBMS Dağıtım Kılavuzu"
services: virtual-machines-windows,virtual-network,storage
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: e0e05b5e-47aa-4c1e-bf83-0d62ee8f614e
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 11/08/2016
ms.author: sedusch
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a56b8f6b3b26fa10e01a25a251a3e4a7bfc77e2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sap-netweaver-on-azure-windows-virtual-machines-vms--dbms-deployment-guide"></a>SAP NetWeaver Azure Windows sanal makinelerde (VM'ler) – DBMS Dağıtım Kılavuzu
[767598 ]:https://launchpad.support.sap.com/#/notes/767598
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
[dbms-guide-2.1]:#c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f 
[dbms-guide-2.2]:#c8e566f9-21b7-4457-9f7f-126036971a91 
[dbms-guide-2.3]:#10b041ef-c177-498a-93ed-44b3441ab152 
[dbms-guide-2]:#65fa79d6-a85f-47ee-890b-22e794f51a64 
[dbms-guide-3]:#871dfc27-e509-4222-9370-ab1de77021c3 
[dbms-guide-5.5.1]:#0fef0e79-d3fe-4ae2-85af-73666a6f7268 
[dbms-guide-5.5.2]:#f9071eff-9d72-4f47-9da4-1852d782087b 
[dbms-guide-5.6]:#1b353e38-21b3-4310-aeb6-a77e7c8e81c8 
[dbms-guide-5.8]:#9053f720-6f3b-4483-904d-15dc54141e30 
[dbms-guide-5]:#3264829e-075e-4d25-966e-a49dad878737 
[dbms-guide-8.4.1]:#b48cfe3b-48e9-4f5b-a783-1d29155bd573 
[dbms-guide-8.4.2]:#23c78d3b-ca5a-4e72-8a24-645d141a3f5d 
[dbms-guide-8.4.3]:#77cd2fbb-307e-4cbf-a65f-745553f72d2c 
[dbms-guide-8.4.4]:#f77c1436-9ad8-44fb-a331-8671342de818 
[dbms-guide-900-sap-cache-server-on-premises]:#642f746c-e4d4-489d-bf63-73e80177a0a8

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

[getting-started-windows-classic]:../virtual-machines-windows-classic-sap-get-started.md
[getting-started-windows-classic-dbms]:../virtual-machines-windows-classic-sap-get-started.md#c5b77a14-f6b4-44e9-acab-4d28ff72a930
[getting-started-windows-classic-deployment]:../virtual-machines-windows-classic-sap-get-started.md#f84ea6ce-bbb4-41f7-9965-34d31b0098ea
[getting-started-windows-classic-dr]:../virtual-machines-windows-classic-sap-get-started.md#cff10b4a-01a5-4dc3-94b6-afb8e55757d3
[getting-started-windows-classic-ha-sios]:../virtual-machines-windows-classic-sap-get-started.md#4bb7512c-0fa0-4227-9853-4004281b1037
[getting-started-windows-classic-planning]:../virtual-machines-windows-classic-sap-get-started.md#f2a5e9d8-49e4-419e-9900-af783173481c

[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056

[ha-guide]:sap-high-availability-guide.md

[install-extension-cli]:virtual-machines-linux-enable-aem.md

[Logo_Linux]:./media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:./media/virtual-machines-shared-sap-shared/Windows.png

[msdn-set-azurermvmaemextension]:https://msdn.microsoft.com/library/azure/mt670598.aspx

[planning-guide]:sap-planning-guide.md  
[planning-guide-1.2]:sap-planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff 
[planning-guide-11]:sap-planning-guide.md#7cf991a1-badd-40a9-944e-7baae842a058 
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
[virtual-machines-azure-resource-manager-architecture]:../../resource-manager-deployment-model.md
[virtual-machines-azurerm-versus-azuresm]:../../resource-manager-deployment-model.md
[virtual-machines-windows-classic-configure-oracle-data-guard]:../virtual-machines-windows-classic-configure-oracle-data-guard.md
[virtual-machines-linux-cli-deploy-templates]:../linux/cli-deploy-templates.md (Deploy and manage virtual machines by using Azure Resource Manager templates and hello Azure CLI)
[virtual-machines-deploy-rmtemplates-powershell]:../virtual-machines-windows-ps-manage.md (Manage virtual machines using Azure Resource Manager and PowerShell)
[virtual-machines-linux-agent-user-guide]:../linux/agent-user-guide.md
[virtual-machines-linux-agent-user-guide-command-line-options]:../linux/agent-user-guide.md#command-line-options
[virtual-machines-linux-capture-image]:../linux/capture-image.md
[virtual-machines-linux-capture-image-resource-manager]:../linux/capture-image.md
[virtual-machines-linux-capture-image-resource-manager-capture]:../linux/capture-image.md#step-2-capture-the-vm
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

Bu kılavuz uygulama ve Microsoft azure'da hello SAP yazılım dağıtma konusunda hello belgelerine bir parçasıdır. Bu kılavuzu okumadan önce lütfen hello okuyun [planlama ve Uygulama Kılavuzu][planning-guide]. Bu belge çeşitli ilişkisel veritabanı yönetim sistemi (RDBMS) ve hizmet (Iaas) özellikleri hello Azure altyapısı kullanan ilgili ürünler SAP Microsoft Azure Virtual Machines'de (VM'ler) ile birlikte hello dağıtımı kapsar.

verilen platformları Hello kağıt hazırlandı hello SAP yükleme belgelerini ve yüklemeleri ve SAP yazılımı dağıtımları için hello birincil kaynakları temsil eden bir SAP notları

## <a name="general-considerations"></a>Genel konular
Bu bölümde, Azure Vm'leri DBMS sistemlerinde sunulan SAP çalışan konuları ilgili. Bu bölümde toospecific DBMS sistemleri birkaç başvuruları vardır. Bunun yerine hello belirli DBMS sistemlere sonra bu bölümde, bu makale içinde işlenir.

### <a name="definitions-upfront"></a>Önceden tanımları
Merhaba belge boyunca aşağıdaki koşulları hello kullanacağız:

* Iaas: Hizmet olarak altyapı.
* PaaS: Hizmet olarak Platform.
* SaaS: Hizmet olarak yazılım.
* SAP bileşen: tek tek SAP gibi bir uygulama ECC, bant genişliği, çözüm Yöneticisi veya EP'deki  SAP bileşenleri geleneksel ABAP veya Java teknolojiler ya da olmayan-tabanlı NetWeaver uygulama iş nesneleri gibi temel alabilir.
* SAP ortamı: bir veya daha fazla SAP bileşenleri tooperform geliştirme QAS, eğitim DR veya üretim gibi işletme işlevi mantıksal olarak gruplandırılır.
* SAP yatay: Bu toohello Müşteri'nin tüm SAP varlıkları başvuruyor BT yatay. Merhaba SAP yatay tüm üretim ve üretim dışı ortamlar içerir.
* SAP sistem: hello birleşimi DBMS katman ve örneğin bir SAP ERP geliştirme sistemi, SAP BW test sistemini, SAP CRM üretim sistem vb. uygulama katmanı. Azure'da şirket içi ve Azure arasında iki Bu katmanlar toodivide olmayan dağıtımlar desteklenir. Şirket içi SAP sistem ya da bu anlamına gelir dağıtılan veya Azure'da dağıtılır. Ancak, Azure veya şirket içi SAP yatay hello farklı sistemlerini dağıtabilirsiniz. Örneğin, azure'da hello SAP CRM geliştirme ve test sistemlerini dağıtmak ancak SAP CRM üretim sistem şirket içi hello.
* Yalnızca bulut dağıtım: Burada bir site siteye hello Azure aboneliğine bağlı değil ya da ExpressRoute bağlantı toohello şirket içi ağ altyapısı dağıtımı. Ortak Azure belgelerine bu tür dağıtımlar da 'Yalnızca bulut' dağıtımları açıklanmıştır. Bu yöntem ile dağıtılan sanal makineleri hello Internet erişilen ve ortak Internet uç toohello VM'ler için Azure'da atanır. Merhaba şirket içi Active Directory (AD) ve bu tür dağıtımlarda tooAzure DNS genişletilmiş değil. Bu nedenle hello VM'ler hello şirket içi Active Directory parçası değildir. Not: Bu belgede yalnızca bulut dağıtımları yalnızca Azure Active Directory veya ad çözümlemesi uzantısı olmadan şirket içi genel buluta çalıştıran tam SAP Windows'un olarak tanımlanır. Yalnızca bulut yapılandırmaları, üretim SAP sistemleri veya SAP STMS veya diğer şirket içi kaynakları Azure ve şirket içi bulunan kaynaklar üzerinde barındırılan SAP sistemleri arasında kullanılan toobe gereken yeri yapılandırması için desteklenmez.
* Şirket içi: VM'ler dağıtılan tooan-siteye, çok siteli sahip Azure aboneliği veya ExpressRoute bağlantısı hello şirket içi inizdeki ve Azure arasında olduğu bir senaryo açıklanmaktadır. Ortak Azure belgelerine dağıtımları bu tür şirket içi senaryoları açıklanmıştır. Merhaba hello bağlantı tooextend şirket içi etki alanları, şirket içi Active Directory ve DNS Azure'da şirket içi nedeni. Merhaba şirket içi yatay hello aboneliğin Azure varlıklar genişletilmiş toohello olduğu. Bu uzantı, hello VM'ler hello şirket içi etki alanının parçası olabilir. Merhaba şirket içi etki alanının etki alanı kullanıcıları hello sunucularına erişebilir ve Hizmetleri üzerindeki VM'ler (DBMS Hizmetleri gibi) çalıştırabilirsiniz. Şirket içi iletişim ve ad çözümleme VM'ler arasında dağıtılır ve Azure'da dağıtılan VM'ler mümkündür. SAP varlıklar azure'da dağıtmak için bu toobe hello en yaygın senaryo bekliyoruz. Bkz: [bu] [ vpn-gateway-cross-premises-options] makale ve [bu] [ vpn-gateway-site-to-site-create] daha fazla bilgi için.

> [!NOTE]
> Şirket içi dağıtımları SAP sistemleri çalışan Azure sanal makineleri bir şirket içi etki alanının üyesi olduğu SAP sistemlerinin üretim SAP sistemleri için desteklenir. Şirketler arası yapılandırmalar bölümleri dağıtmak için desteklenen veya Azure'da SAP Windows'un tamamlayın. Azure'da hello tam SAP yatay bile çalışan, şirket içi etki alanı ve REKLAM parçası olan bu VM'lerin olması gerektirir. Merhaba belgelerinin önceki sürümleri biz hello terim 'Karma' şirket içi bağlantılar şirket içi ve Azure arasında olduğunu hello aslında burada kökü karma BT senaryoları hakkında açıklandı. Bu durumda 'Karma' de hello VM'ler için Azure'da hello parçası olduğu anlamına gelir Active Directory şirket içi.
>
>

Bazı Microsoft belgeleri şirketler arası senaryoları özellikle DBMS HA yapılandırmaları için biraz farklı bir şekilde açıklanmıştır. Hello hello SAP durumunun belgeleri ilgili, hello şirketler arası senaryo hello SAP yatay şirket içi ve Azure arasında dağıtılmış bir siteden siteye veya özel (ExpressRoute) bağlantısı ve toohello olgu yalnızca toohaving boils.

### <a name="resources"></a>Kaynaklar
Merhaba aşağıdaki kılavuzlara SAP dağıtımlarını azure'da hello konu için kullanılabilir:

* [Azure sanal makinelerde planlama (VM'ler) – SAP NetWeaver ve Uygulama Kılavuzu][planning-guide]
* [SAP NetWeaver Azure sanal makinelerde (VM'ler) – dağıtım kılavuzu][deployment-guide]
* [SAP NetWeaver Azure Virtual Machines'de (VM'ler) – DBMS Deployment Guide (Bu belgenin)][dbms-guide]
* [SAP NetWeaver Azure sanal makinelerde (VM'ler) – yüksek kullanılabilirlik Dağıtım Kılavuzu][ha-guide]

SAP notları aşağıdaki hello Azure üzerinde SAP ilgili toohello konu şunlardır:

| Not numarası | Başlık |
| --- | --- |
| [1928533] |Azure üzerinde SAP uygulamaları: desteklenen ürünler ve Azure VM türleri |
| [2015553] |Microsoft Azure üzerinde SAP: Destek önkoşulları |
| [1999351] |Gelişmiş Azure için SAP izleme sorunlarını giderme |
| [2178632] |Microsoft Azure üzerinde SAP için ölçümleri izleme anahtarı |
| [1409604] |Windows sanallaştırma: İzleme Gelişmiş |
| [2191498] |Azure ile Linux üzerinde SAP: İzleme Gelişmiş |
| [2039619] |Microsoft Azure kullanarak SAP uygulamaları Oracle veritabanı hello: desteklenen ürünleri ve sürümleri |
| [2233094] |DB6: Linux, UNIX ve Windows - ek bilgi için IBM DB2 kullanarak Azure SAP uygulamaları |
| [2243692] |Microsoft Azure (Iaas) VM Linux'ta: SAP lisans sorunları |
| [1984787] |SUSE LINUX Enterprise Server 12: Yükleme notları |
| [2002167] |Red Hat Enterprise Linux 7.x: yükleme ve yükseltme |

Lütfen hello okuyun [SCN Wiki](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) , Linux için tüm SAP notlar içerir.

Merhaba Microsoft Azure Mimarisi ve Microsoft Azure sanal makineleri nasıl dağıtılır ve işletilen hakkında bilgiye sahip olmalıdır. Daha fazla bilgiyi burada bulabilirsiniz <https://azure.microsoft.com/documentation/>

> [!NOTE]
> Ki **değil** Microsoft Azure platformu hello Microsoft Azure platformu bir hizmet (PaaS) teklifleri tartışma. Bu raporda yalnızca şirket içi ortamınızda hello DBMS çalışır gibi bir veritabanı yönetim sistemi (DBMS) Microsoft Azure sanal makineleri (Iaas) hakkında çalışıyor. Veritabanı özellikleri ve İşlevler bu iki teklifler arasında çok farklı olan ve birbirleri ile mixed olmalıdır değildir. Ayrıca bkz: <https://azure.microsoft.com/services/sql-database/>
>
>

Biz Iaas ele olduğundan, genel hello Windows, Linux ve DBMS yükleme ve yapılandırma olan temelde hello herhangi bir sanal makine veya şirket içi yüklemek çıplak metal makine ile aynı. Ancak, Iaas kullanırken farklı olacak bazı mimarisi ve sistem yönetimi uygulaması karar vardır. Merhaba bu belgenin amacı, sizin için Iaas kullanırken hazırlanmalıdır tooexplain hello belirli mimari ve sistem yönetimi farklılıklar ' dir.

Genel olarak, hello genel Bu yazıda ele alınacaktır farkının şunlardır:

* Merhaba uygun verileri dosya düzeni sahip SAP sistemleri tooensure Hello uygun VM/VHD düzenini planlama ve işleminizi iş yükü için yeterli IOPS elde edebilirsiniz.
* Iaas kullanırken ağ durumları.
* Belirli veritabanı özellikleri toouse sipariş toooptimize hello veritabanı düzeni.
* Iaas yedekleme ve geri yükleme konuları.
* Görüntü dağıtımı için farklı türleri kullanma.
* Azure Iaas yüksek kullanılabilirlik.

## <a name="65fa79d6-a85f-47ee-890b-22e794f51a64"></a>RDBMS dağıtım yapısı
Bu bölümde sırayla izleyin, gerekli toounderstand ne içinde sunulan [bu] [ deployment-guide-3] hello bölüm [Dağıtım Kılavuzu'na][deployment-guide]. Hakkında bilgi hello farklı VM-serisi ve ve Azure standart ve Premium depolama farklar farkları anlaşılan ve gerekir bu bölümü okumadan önce bilinen.

Mart 2015 kadar Azure bir işletim sistemini içeren VHD sınırlı too127 GB boyutunda yoktu. Bu sınırlama Mart 2015'te kaldırılmış (daha fazla bilgi onay için <https://azure.microsoft.com/blog/2015/03/25/azure-vm-os-drive-limit-octupled/> ). VHD'lerde buradan içeren hello işletim sistemi sahip hello aynı boyutta gibi herhangi bir VHD'yi. Bununla birlikte, biz yine hello işletim sistemi, DBMS ve nihai SAP ikili dosyaları hello veritabanı dosyalarından ayrı olduğu dağıtım yapısını tercih eder. Bu nedenle, Azure sanal makinelerde çalışan SAP sistemleri hello temel VM (veya VHD) hello işletim sistemiyle yüklenen veritabanı yönetim sistemi yürütülebilir dosyalarının ve SAP yürütülebilir olacaktır bekliyoruz. Merhaba DBMS veri ve günlük dosyalarını ayrı VHD dosyaları, Azure Storage (standart veya Premium Storage) depolanır ve mantıksal diskleri toohello özgün Azure işletim sistemi görüntüsü VM bağlı.

(Örneğin hello DS serisi veya GS serisi VM'ler kullanarak) ve Azure standart veya Premium Storage yok yararlanarak üzerinde bağımlıdır belgelenen diğer Azure kotalarda [burada][virtual-machines-sizes]. Azure Vhd'lerinizi planlarken, toofind hello iyi dengeyi hello kotaları hello için aşağıdakiler gerekir:

* veri dosyalarının sayısını Hello.
* Merhaba dosyalarını içeren VHD Hello sayısı.
* tek bir VHD Hello IOPS kotalar.
* VHD başına Hello veri işleme.
* VM boyutu başına ek VHD'ler olası Hello sayısı.
* Merhaba genel depolama verimliliğini VM sağlayabilir.

Azure VHD sürücüsü başına IOP kota zorlar. Bu kotalar Azure Standard Storage ve Premium depolama üzerinde barındırılan VHD için farklıdır. G/ç gecikmeleri hello iki depolama türlerini Premium Etkenler daha iyi g/ç gecikmeleri teslim depolama ile arasında çok farklı olacaktır. Her hello farklı VM türler mümkün tooattach olan VHD sınırlı sayıda sahip. Yalnızca belirli VM türleri Azure Premium Storage yararlanabilirsiniz başka bir kısıtlamadır. Başka bir deyişle, hello kararı belirli bir VM türü için yalnızca hello CPU ve bellek gereksinimleri tarafından aynı zamanda IOPS, hello tarafından genellikle hello VHD'ler sayısıyla ölçeklenir veya Premium depolama diskleri türünü hello gecikme süresi ve disk işleme gereksinimleri güdümlü değil. Özellikle Premium depolama ile bir VHD hello boyutuna da hello sayısı IOPS ve her VHD tarafından elde toobe gereken üretilen iş belirlenmesine.

Genel IOPS oranı, bağlanmış, VHD hello sayısı hello ve VM tüm bağlı birlikte hello boyutunu hello hello olgu SAP sistem toobe olarak kendi şirket içi dağıtıma göre farklı bir Azure yapılandırması neden olabilir. Merhaba IOPS sınırları LUN başına genellikle şirket içi dağıtımlarda yapılandırılabilir. Azure Storage ile bu sınırları sabit veya hello disk türünün Premium depolama bağımlı olduğu gibi ise. Bu nedenle şirket içi dağıtımlar ile biz SAP gibi özel yürütülebilir dosyaları için birçok farklı birimler kullanmak ve DBMS veya geçici veritabanları veya tablo alanları için özel birimler hello veritabanı sunucuları müşteri yapılandırmalarını konusuna bakın. Bu tür bir şirket içi sistem taşınan tooAzure olduğunda, yürütülebilir dosyalar veya ya da çok fazla IOPS değil gerçekleştirmeyin veritabanları için bir VHD israfı tarafından tooa atık olası IOPS bant genişliğinin neden olabilir. Bu nedenle, Azure Vm'lerde bu hello DBMS ve SAP yürütülebilir dosyalar yüklenmesi hello işletim sistemi disk üzerinde mümkünse öneririz.

Merhaba hello veritabanı dosyalarını ve günlük dosyaları ve Azure kullanılan depolama hello türü yerleşimini tanımlanmalıdır IOPS, gecikme ve verimlilik gereksinimleri. Sipariş toohave hello işlem günlüğü için yeterli IOPS hello işlem günlüğü için birden çok VHD dosyası ya da daha büyük bir Premium depolama diski kullanan zorlanmış tooleverage olabilir. Bir yalnızca oluşturmayı tercih durumda, bir yazılım hello hello işlem günlüğü yer alacağı VHD ile (örneğin Windows depolama havuzu için Windows veya MDADM ve LVM (mantıksal birim Yöneticisi) Linux için) RAID.

- - -
> ![Windows][Logo_Windows] Windows
>
> Sürücü Azure VM'deki D:\ hello Azure işlem düğümü üzerinde bazı yerel diskler tarafından yedeklenen bir kalıcı olmayan bir sürücüdür. Kalıcı olmayan olduğundan, bu hello VM yeniden başlatıldığında hello D:\ sürücüsüne üzerinde yapılan değişiklikler toohello içerik kaybolur anlamına gelir. "Herhangi bir değişiklik" demek isteriz kaydedilen dosyalar, oluşturulan dizinleri, yüklü uygulamalar vb..
>
> ![Linux][Logo_Linux] Linux
>
> Linux Azure VM'ler, otomatik olarak bir sürücü hello Azure işlem düğümünde yerel disk ile desteklenir ve kalıcı olmayan bir sürücü /mnt/resource bağlayın. Kalıcı olmayan olduğundan, bu hello VM yeniden başlatıldığında tüm yapılan değişiklikler toocontent /mnt/resource içinde kaybolur anlamına gelir. Herhangi bir değişiklik tarafından demek isteriz kaydedilen dosyaları, oluşturulan dizinleri, yüklü uygulamalar vb..
>
>

- - -
Hello Azure VM-serisi bağımlı, hello yerel hello disklerde olduğu gibi kategorilere düğümünü Göster farklı performans hesaplama:

* A0-A7: Çok sınırlı performans. Windows disk belleği dosyası dışındaki her şey için kullanılabilir değil
* A8-A11: Bazı on bin IOPS ile çok iyi performans özellikleri ve > 1GB/sn verim
* D-serisi: Bazı on bin IOPS ile çok iyi performans özellikleri ve > 1GB/sn verim
* DS serisi: Bazı on bin IOPS ile çok iyi performans özellikleri ve > 1GB/sn verim
* G-serisi: Bazı on bin IOPS ile çok iyi performans özellikleri ve > 1GB/sn verim
* GS serisi: Bazı on bin IOPS ile çok iyi performans özellikleri ve > 1GB/sn verim

Yukarıdaki deyimleri SAP ile sertifikalı toohello VM türleri uyguladığınızı. Merhaba VM dizisi mükemmel IOPS ve üretilen iş ile tempdb veya geçici tablo alanı gibi bazı DBMS özellikleri tarafından Dengeleme için uygun.

### <a name="c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f"></a>Sanal makineleri ve VHD için önbelleğe alma
Bu diskleri/VHD'ler hello portalı üzerinden veya ne zaman biz karşıya yüklenen VHD tooVMs Bağla oluşturuyoruz, biz olup olmadığını hello VM ve Azure depolama alanında bulunan bu VHD arasında hello g/ç trafiği önbelleğe alınmış seçebilirsiniz. Azure standart ve Premium depolama önbellek bu tür için iki farklı teknoloji kullanın. Her iki durumda da hello önbelleğe kendisini disk üzerinde aynı sürücüleri kullanılan hello hello geçici hello VM, (D:\ Windows) veya Linux'ta /mnt/resource diskle.

İçin Azure Standard Storage hello olası önbellek türleri şunlardır:

* Önbelleğe alma
* Okuma
* Okuma ve yazma önbelleği

Sipariş tooget tutarlı ve belirleyici performans, hello tüm VHD'ler için Azure Standard Storage önbelleğe almayı içeren ayarlamalısınız **DBMS ilgili veri dosyalarını, günlük dosyalarını ve tablo alanı too'NONE'**. Merhaba VM Merhaba önbelleğe alma ile Merhaba varsayılan kalabilir.

Azure Premium Storage için önbellek seçeneklerini aşağıdaki hello mevcuttur:

* Önbelleğe alma
* Okuma

Azure Premium Storage için öneri olan tooleverage **veri dosyaları için okuma** hello SAP veritabanının ve seçtiğiniz **günlük dosyalarını VHD(s) hello için önbelleğe alma**.

### <a name="c8e566f9-21b7-4457-9f7f-126036971a91"></a>Yazılım RAID
Önceden belirtildiği yukarıdaki gibi hello sayısı VHD'ler yapılandırabilirsiniz ve hello arasında hello veritabanı dosyaları için bir Azure VM VHD veya Premium depolama sağlayacak maksimum IOPS türü disk toobalance hello IOPS sayısını ihtiyacınız olacaktır. Farklı VHD hello toobuild yazılım RAID biter toodeal IOPS VHD'ler üzerinde yük hello ile en kolay yolu. Ardından hello SAP DBMS, veri dosyalarının sayısını LUN hello yazılım RAID dışında yontulmuş hello yerleştirin. Hello gereksinimleri de tooconsider hello kullanım Premium Storage isteyebilirsiniz bağımlı iki hello itibaren üç farklı Premium depolama diskleri standart depolama birimine dayalı VHD'ler daha yüksek IOPS kota sağlar. Yanında daha iyi g/ç gecikmesi Azure Premium Storage tarafından sağlanan önemli hello.

Aynı toohello işlem günlüğü hello farklı DBMS sistemlerinin geçerlidir. Merhaba DBMS sistemleri hello dosyalardan biri aynı anda yalnızca yazma bu yana çok bunları yalnızca daha fazla Tlog dosyaları ekleme ile korumaz. Tek standart tabanlı depolama yüksek IOPS hızları gerekirse VHD teslim edebilir, birden çok standart depolama VHD şeritler veya, yüksek IOPS hızları ötesinde Etkenler daha düşük gecikme süresi hello yazmak için de sağlayan daha büyük bir Premium depolama disk türü kullanabilir miyim / İşletim sistemi hello işlem günlüğüne.

Hangi yazılım kullanarak favor Azure dağıtımlarda yaşadı durumlar RAID şunlardır:

* İşlem günlüğü/Yinele günlüğü Azure için tek bir VHD sağladığından daha fazla IOPS gerektirir. Yukarıda belirtildiği gibi bu yazılım RAID kullanarak birden çok VHD bir LUN oluşturarak çözülebilir.
* Düzensiz g/ç iş yükü dağıtımı hello farklı veri dosyalarını üzerinden hello SAP veritabanı. Bu gibi durumlarda bir hello kota yerine genellikle basarsa bir veri dosyası yaşayabilirsiniz. Diğer veri dosyalarını Kapat toohello IOPS kota tek VHD bile alamıyorsanız ise. Böyle durumlarda hello toobuild bir kolay çözümdür yazılım RAID kullanarak birden çok VHD üzerinden LUN.
* Tanımadığınız hangi hello tam g/ç iş yükü verileri dosya başına olması ve yalnızca kabaca ne hello bilmeniz IOPS iş yükü hello DBMS karşı genel sağlamasıdır. Kolay toodo toobuild bir LUN hello ile bir yazılım RAID yardımcı olur. Bu LUN'u arkasında birden çok VHD kotaları Hello toplamını IOPS bilinen hello sonra karşılamak oranı.

- - -
> ![Windows][Logo_Windows] Windows
>
> Daha önceki Windows sürümlerinde Windows şeritleme etkili olduğundan Windows Server 2012 veya daha yüksek depolama alanları kullanımını tercih edilir. Lütfen, toocreate hello Windows depolama havuzları ve depolama alanları PowerShell komutlarıyla işletim sistemi olarak Windows Server 2012 kullanırken gerektiğini unutmayın. Merhaba PowerShell komutlarını şurada bulunabilir <https://technet.microsoft.com/library/jj851254.aspx>
>
> ![Linux][Logo_Linux] Linux
>
> Yalnızca MDADM ve LVM (mantıksal birim Yöneticisi) desteklenen toobuild yazılım RAID Linux'ta içindir. Daha fazla bilgi için aşağıdaki makaleler hello okuyun:
>
> * [Yazılım RAID Linux üzerinde yapılandırma] [ virtual-machines-linux-configure-raid] (için MDADM)
> * [Azure'da bir Linux VM LVM yapılandırın][virtual-machines-linux-configure-lvm]
>
>

- - -
Azure Premium Storage ile mümkün toowork genellikle olan VM-serisi yararlanarak dikkat edilmesi gereken noktalar şunlardır:

* Olan g/ç gecikme için taleplerini toowhat SAN/NAS cihazları teslim kapatın.
* Azure Standard Storage sunabilir daha Etkenler daha iyi g/ç gecikmesi için isteğe bağlı.
* Belirli bir VM'ye karşı birden çok standart depolama VHD ile ne elde edilebilir daha yüksek IOPS VM başına yazın.

Bu yana Hello Azure Storage arka plandaki her VHD tooat en az üç depolama düğümleri basit RAID 0 şeritleme kullanılabilir çoğaltır. Hiçbir gerek tooimplement RAID5 veya RAID1 yoktur.

### <a name="10b041ef-c177-498a-93ed-44b3441ab152"></a>Microsoft Azure depolama
Microsoft Azure depolama depolar (OS ile) temel VM ve VHD veya BLOB tooat en az 3 ayrı depolama düğümleri hello. Bir depolama hesabı oluştururken yoktur koruma seçimine aşağıda gösterildiği gibi:

![Azure depolama hesabı için etkin coğrafi çoğaltma][dbms-guide-figure-100]

Azure Storage yerel çoğaltma (yerel olarak yedekli) birkaç müşteri toodeploy göze tooinfrastructure hatası nedeniyle veri kaybına karşı koruma düzeyleri sağlar. Beşinci bir değişim hello birinin ilk üç olan ile 4 farklı seçenekler olan yukarıda gösterildiği gibi. Bunları yakın arayan biz ayırt edebilirsiniz:

* **Premium yerel olarak yedekli depolama (LRS)**: Azure Premium depolama g/Ç kullanımı yoğun iş yükleri çalıştıran sanal makineler için yüksek performanslı, düşük gecikmeli disk desteği sunar. Merhaba içindeki hello verilerin 3 çoğaltmaları vardır bir Azure bölgesi, aynı Azure veri merkezi. Merhaba kopyalar farklı hata ve yükseltme etki alanları olacaktır (bkz için [bu] [ planning-guide-3.2] hello bölümde [Planlama Kılavuzu][planning-guide]). Hizmet tooa depolama düğüm hatası veya disk arızası nedeniyle dışına giderek hello veri çoğaltma olması durumunda, yeni bir çoğaltma otomatik olarak oluşturulur.
* **Yerel olarak yedekli depolama (LRS)**: Bu durumda hello içindeki hello verilerin 3 çoğaltmaları vardır bir Azure bölgesi, aynı Azure veri merkezi. Merhaba kopyalar farklı hata ve yükseltme etki alanları olacaktır (bkz için [bu] [ planning-guide-3.2] hello bölümde [Planlama Kılavuzu][planning-guide]). Hizmet tooa depolama düğüm hatası veya disk arızası nedeniyle dışına giderek hello veri çoğaltma olması durumunda, yeni bir çoğaltma otomatik olarak oluşturulur.
* **Coğrafi olarak yedekli depolama (GRS)**: Bu durumda, ek bir akış bir zaman uyumsuz çoğaltma yok hello durumlarda çoğunu olan başka bir Azure bölgesi hello veri 3 çoğaltmaları hello aynı coğrafi bölgede (örneğin, Kuzey Avrupa ve Batı Avrupa). Vardır; böylece 6 çoğaltmaları toplamda bu 3 ek yinelemede neden olacaktır. Bu bir çeşitlemesi, hello coğrafi çoğaltılan Azure bölgesi hello veri okuma amacıyla (okuma erişimli coğrafi olarak yedekli) kullanıldığı bir ektir.
* **Bölge olarak yedekli depolama (ZRS)**: Bu durumda veri kalır hello hello 3 çoğaltmalarının hello aynı Azure bölgesi. İçinde anlatıldığı gibi [bu] [ planning-guide-3.1] hello bölüm [Planlama Kılavuzu] [ planning-guide] bir Azure bölgesinin bir sayı veri merkezleri içinde yakın bir yerde konumlandırıldığında olabilir. LRS Hello durumda hello çoğaltmaları bir Azure bölgesi hale hello farklı veri merkezlerinde dağıtılması.

Daha fazla bilgi bulunabilir [burada][storage-redundancy].

> [!NOTE]
> DBMS dağıtımları için coğrafi olarak yedekli depolama hello kullanımı önerilmez.
>
> Azure depolama coğrafi çoğaltma zaman uyumsuz olarak çağrılır. Tek tek VHD çoğaltılmasını tek VM kilit adımda eşitlenmemiş tooa bağladı. Bu nedenle, farklı VHD'ler dağıtılan veya bir yazılım üzerinde birden çok VHD tabanlı RAID karşı dağıtılan uygun tooreplicate DBMS dosyaları şu değil. DBMS yazılım hello kalıcı disk depolama farklı LUN'ları ve temel diskleri/VHD/dağılımı arasında tam olarak eşitlenir gerektirir. G/ç yazma etkinlikleri çeşitli mekanizmalar toosequence DBMS yazılım kullanır ve bir DBMS bunlar bile birkaç milisaniye farklı ise hello çoğaltma tarafından hedeflenen hello disk depolama bozuk olduğunu bildirir. Bu nedenle bir gerçekten veritabanı yapılandırması birden çok VHD arasında coğrafi olarak çoğaltılmış uzatılmış veritabanıyla isterse, bu tür bir çoğaltma veritabanı anlamına gelir ve işlevsellik ile gerçekleştirilen toobe gerekir. Bir Azure depolama coğrafi çoğaltma tooperform üzerinde bu işlemi güvenmemelisiniz.
>
> Merhaba, bir örnek sistemiyle basit tooexplain sorunudur. Azure'da hello DBMS veri dosyaları artı bir VHD içeren hello işlem günlüğü dosyasını içeren 8 VHD'leri karşıya bir SAP sistemine sahip varsayalım. Her biri bu 9 VHD hello veri toohello veri veya işlem günlük dosyaları yazılmış olup olmadığını toothem toohello DBMS göre tutarlı bir yönteminde yazılan veriler sahip olur.
>
> Sırayla tooproperly coğrafi-replicate hello veri ve tutarlı veritabanı görüntüsü, hello içerik korumak tüm dokuz VHD'leri sahip toobe hello tam sırası hello g/ç işlemlerinde coğrafi olarak çoğaltılmış olan yürütülen dokuz hello karşı farklı VHD'ler. Ancak, Azure Storage coğrafi çoğaltma VHD'ler arasındaki toodeclare bağımlılıkları izin vermiyor. Bu Microsoft Azure Storage coğrafi çoğaltma bu dokuz farklı VHD'ler hello içeriği olan diğer ilgili tooeach ve hello veri değişikliklerini hello sipariş hello g/ç işlemlerinde çoğaltırken tutarlı olduğunu oldu hello olgu hakkında bilmiyor anlamına gelir. Tüm hello 9 VHD'ler arasında.
>
> Hello coğrafi olarak çoğaltılmış görüntüleri hello senaryoda tutarlı veritabanı görüntüsü sağlamaz, aynı zamanda yoktur ciddi bir şekilde gerçekleştirebileceğiniz coğrafi olarak yedekli depolama ile görünür bir performans cezası yüksek olması olasılığını yanı sıra performansını etkiler. Özet olarak, bu tür bir depolama artıklığı DBMS türü iş yükleri için kullanmayın.
>
>

#### <a name="mapping-vhds-into-azure-virtual-machine-service-storage-accounts"></a>Azure sanal makinesi hizmeti depolama hesaplarına veri VHD'ler eşleme
Bir Azure depolama hesabı yalnızca bir yönetici yapısıyla, aynı zamanda bir konu sınırlamalar ' dir. Merhaba sınırlamalar olup olmadığını biz Azure Standard Storage hesabını veya bir Azure Premium depolama hesabı hakkında konuşun üzerinde farklılık gösterir ancak. Merhaba tam özelliklerini ve sınırlamalarını listelenen [burada][storage-scalability-targets]

İsteğe bağlı olarak Azure Standard Storage için önemli toonote olacak şekilde bir sınır yoktur hello IOPS her depolama hesabı üzerinde (satır 'Toplam istek oranı' içeren [hello makale][storage-scalability-targets]). Ayrıca, 100 depolama hesaplarının (itibariyle, Temmuz 2015) Azure abonelik başına ilk bir sınırı yoktur. Bu nedenle, Azure Standard Storage kullanırken birden çok depolama hesapları arasında sanal makineleri IOPS toobalance önerilir. Mümkünse, ideal olarak kullanan bir depolama hesabı tek bir VM ise. Böylece biz Azure Standard Storage üzerinde barındırılan her VHD, kota sınırına burada ulaşabilir DBMS dağıtımları hakkında konuşun varsa, 30-40 VHD'ler Azure Standard Storage kullanır Azure depolama hesabı başına yalnızca dağıtmanız gerekir. Merhaba üzerinde Azure Premium Storage yararlanır ve toostore büyük veritabanı birimler, istediğiniz diğer yandan, IOPS'ye göre daha iyi olabilir. Ancak Azure Premium Storage hesabını bir Azure standart depolama hesabı veri hacmi şekilde daha kısıtlayıcı. Sonuç olarak, hello veri birimi sınırı basarsa önce Azure Premium Storage hesabını içinde VHD'leri sınırlı sayıda yalnızca dağıtabilirsiniz. Bir "sanal SAN'ı" olarak Azure Storage hesabını hello son düşünün adresindeki, IOPS ve/veya kapasite özellikleri sınırlıdır. Sonuç olarak, hello görev, toodefine hello düzenini hello hello farklı SAP sistemleri hello farklı 'sanal SAN cihazları üzerinde' VHD'leri veya Azure Storage hesapları şirket içi dağıtımlar olduğu gibi kalır.

Azure için standart depolama farklı depolama hesapları tooa toopresent depodan önerilmez tek VM mümkünse.

Merhaba DS veya GS serisi Azure VM'lerin kullanarak ancak olası toomount VHD'ler Azure standart depolama hesapları ve Premium depolama hesapları var. DBMS verilere sahip olmak ancak yedeklemeleri standart depolama alanına yazma gibi kullanım örnekleri VHD'ler yedeklenen ve böyle heterojen depolama burada işlevden toomind Premium depolama günlük dosyalarını gelir.

Müşteri dağıtımları ve test yaklaşık 30 too40 tek Azure standart depolama hesabı kabul edilebilir performans üzerinde veritabanı veri dosyalarını ve günlük dosyalarını içeren VHD sağlanabilir göre. Daha önce belirtildiği gibi hello Azure Premium Storage hesabını içerebileceğinden büyük olasılıkla toobe hello veri kapasitesi ve değil IOPS kısıtlamasıdır.

SAN cihazları ile şirket içi, paylaşımı bazı sipariş tooeventually izleme gerektirdiği bir Azure depolama hesabı üzerinde performans sorunlarını algıla. Hello Azure Monitoring uzantısı SAP için ve hello Azure Portal olan kullanılan toodetect olabilir araçları meşgul GÇ performansın teslim Azure depolama hesapları.  Bu durum algılanırsa toomove meşgul VM'ler tooanother Azure depolama hesabı önerilir. Lütfen toohello bakın [Dağıtım Kılavuzu'na] [ deployment-guide] tooactivate hello SAP izleme yeteneklerini nasıl ana bilgisayar ile ilgili ayrıntılar için.

En iyi uygulamalar Azure Standard Storage ve Azure standart depolama hesapları etrafında özetlemeye başka bir makaleye burada bulunabilir <https://blogs.msdn.com/b/mast/archive/2014/10/14/configuring-azure-virtual-machines-for-optimal-storage-performance.aspx>

#### <a name="moving-deployed-dbms-vms-from-azure-standard-storage-tooazure-premium-storage"></a>DBMS VM'ler Azure Standard Storage tooAzure Premium depolama dağıtılan taşıma
Biz müşteri olarak toomove Azure Standard Storage dağıtılan bir VM'den Azure Premium depolama alanına istediğiniz oldukça bazı senaryolar karşılaşırsınız. Bu fiziksel olarak hello veri taşımadan mümkün değildir. Çeşitli yolları tooachieve hello hedefi vardır:

* Yalnızca yeni bir Azure Premium Storage hesabınıza tüm VHD'ler, temel VHD yanı sıra veri VHD'ler kopyalayabilirsiniz. Çok sık VHD'ler hello sayısı değil hello veri birimi gerekli hello olgu nedeniyle Azure Standard Storage seçtiniz. Ancak bu kadar sayıda VHD'ler IOPS hello nedeniyle gerekli. TooAzure Premium ile idare depolama taşıma göre daha az VHD'ler tooachieve bazı IOPS verimlilik hello. Azure storage'da standart hello için ödeme veri ve hello nominal disk boyutu kullandığınız hello olgu verildiğinde, VHD hello sayısı gerçekten maliyet açısından önemli değil. Ancak, Azure Premium Storage ile Merhaba nominal disk boyutu için ödeme. Bu nedenle, hello müşteri çoğunu tookeep hello numaradan Premium Storage içinde Azure VHD hello sayı gerekli tooachieve hello IOPS verimlilik gerekli deneyin. Bu nedenle, müşterilerin çoğu basit bir 1:1 hello şekilde karşı kopyalama karar verin.
* Henüz olup, SAP veritabanınızın veritabanı yedeği içeren tek bir VHD bağlayın. Merhaba yedeklemeden sonra hello VHD içeren hello yedekleme de dahil olmak üzere tüm VHD'leri çıkarın ve kopyalama hello VHD temel ve VHD hello yedekleme ile bir Azure Premium Storage hesabınıza hello. Merhaba temel VHD ve bağlama hello VHD hello yedeklemeyle VM dayalı hello dağıtırsınız. Artık ek boş Premium depolama kullanılan toorestore hello veritabanına olan disklerde hello VM oluşturun. Bu, o hello DBMS hello geri yükleme işleminin bir parçası toochange, yolları toohello veri ve günlük dosyaları verir varsayar.
* Diğer bir olasılık, burada yalnızca hello yedekleme VHD Azure Premium depolama alanına kopyalayın ve yeni dağıtılan ve yüklenen bir VM'ye karşı ekleme hello eski işlemi, çeşididir.
* Merhaba dördüncü olasılığı toochange hello veritabanınızın veri dosyalarının sayısını içinde need olduğunuzda seçmelisiniz. Böyle bir durumda içeri/dışarı aktarma kullanarak bir SAP homojen sistem kopyasını gerçekleştirmelisiniz. PUT bu dosyaları bir Azure Premium Storage hesabına kopyalanır bir VHD'yi verin ve tooa toorun hello alma işlemleriyle kullandığınız VM ekleyin. Çoğunlukla toodecrease hello veri dosyalarının sayısını istediğinizde müşteriler bu olasılığı kullanın.

### <a name="deployment-of-vms-for-sap-in-azure"></a>VM dağıtımı Azure SAP için
Microsoft Azure diskleri ilişkili ve toodeploy VM'ler birden çok yol sunar. Böylece hello VM'ler hazırlıklar dağıtım hello yolu bağımlı değişebilir olduğundan çok önemli toounderstand hello farklar kalır. Genel olarak, biz hello aşağıdaki bölümlerde açıklanan hello senaryoları içine bakın.

#### <a name="deploying-a-vm-from-hello-azure-marketplace"></a>Hello Azure Marketi VM'den dağıtma
3. taraf hello Azure Marketi toodeploy görüntüden VM sağlanan veya tootake Microsoft ister. Azure VM dağıtımı sonra hello izleyin aynı kılavuzları ve Araçlar tooinstall bir şirket içi ortamda yaptığınız gibi VM içinde SAP yazılım hello. Hello Azure VM içinde hello SAP yazılımını yükleme, SAP ve Microsoft tooupload önerilir ve hello SAP yükleme medyasını Azure VHD'leri veya toocreate bir Azure VM 'tüm hello gerekli SAP yükleme medyasını içeren bir dosya sunucusu olarak' çalışma depolamak.

#### <a name="deploying-a-vm-with-a-customer-specific-generalized-image"></a>Bir VM müşteri belirli genelleştirilmiş bir yansıma ile dağıtma
Bakımından tooyour işletim sistemi veya DBMS sürümü toospecific düzeltme eki gereksinimleri hello Azure Marketi sağlanan hello görüntülerinde gereksinimlerinize değil. Bu nedenle, daha sonra birkaç kez dağıtılabilen 'özel' kendi işletim sistemi/DBMS VM görüntüsü kullanarak bir VM'i toocreate gerekebilir. tooprepare çoğaltmak için 'özel' görüntüsü, işletim sistemi üzerinde hello genelleştirilmiş gerekir hello VM şirket içi. Lütfen toohello bakın [Dağıtım Kılavuzu'na] [ deployment-guide] hakkında ayrıntılar için toogeneralize VM.

(Özellikle 2 katmanlı sistemler için), şirket içi VM'deki SAP içerik zaten yüklediyseniz, hello Azure VM hello örneği aracılığıyla hello dağıtımını yeniden adlandırdıktan sonra hello tarafından SAP yazılım sağlama desteklenen yordamı hello SAP sistem ayarlarını uyarlayabilirsiniz Yöneticisi (SAP Not [1619720]). Aksi takdirde hello Azure VM daha sonra hello dağıtımını sonra hello SAP yazılım yükleyebilirsiniz.

Hello SAP uygulama tarafından kullanılan hello veritabanı içeriğini itibariyle, ya da hello içerik yeni bir SAP yüklemesiyle oluşturabilirsiniz ya da içeriğinizi Azure'da hello DBMS toodirectly özelliklerini yararlanarak veya VHD DBMS veritabanı Yedeğiyle kullanarak aktarabilirsiniz Microsoft Azure depolama alanına yedekleme. Bu durumda, ayrıca VHD'ler DBMS veri hello ile hazırlamanız dosyaları şirket içi oturum ve bu diskleri olarak Azure'a aktarabilir. Ancak, şirket içi tooAzure yüklendiğinden DBMS veri aktarımını hello şirket içi hazırlanmış toobe gereken VHD diskler üzerinde çalışır.

#### <a name="moving-a-vm-from-on-premises-tooazure-with-a-non-generalized-disk"></a>VM genelleştirilmiş olmayan bir disk ile şirket içi tooAzure taşıma
Şirket içi tooAzure (yükseltme ve shift) belirli bir SAP sistemden toomove planlayın. Bu hello hello işletim sistemi içeren VHD yükleyerek yapılabilir, SAP ikili dosyaları ve nihai DBMS ikili dosyaları hello artı VHD'ler hello veri ve günlük dosyaları hello DBMS tooAzure ile Merhaba. Merhaba şirket içi ortamda yapılandırılmış gibi #2 yukarıdaki tooscenario, hello ana bilgisayar adı, SAP SID ve SAP kullanıcı hesapları hello Azure VM bulundurun. Bu nedenle, hello görüntü genelleme gerekli değildir. Bu durumda, çoğunlukla hello SAP yatay parçası şirket içi ve bölümleri Azure üzerinde çalıştırıldığı şirketler arası senaryolar için uygulanır.

## <a name="871dfc27-e509-4222-9370-ab1de77021c3"></a>Yüksek kullanılabilirlik ve olağanüstü durum kurtarma Azure VM'ler ile
SAP ve DBMS dağıtımları için kullanırız toodifferent bileşenleri uygulanacak yüksek kullanılabilirlik (HA) ve olağanüstü durum kurtarma (DR) işlevlerini aşağıdaki hello Azure sunar

### <a name="vms-deployed-on-azure-nodes"></a>Azure düğümleri üzerinde dağıtılan VM'ler
Hello Azure platformu, dağıtılan VM'ler için dinamik geçiş gibi özellikler sunmaz. Başka bir deyişle, varsa bakım gerekli bir VM dağıtıldığı bir sunucu kümesinde, hello VM durdurulup yeniden tooget gerekiyor. Azure bakım kullanarak, bu nedenle sunucuları kümeleri içinde yükseltme etki alanları olarak adlandırılan gerçekleştirilir. Bir seferde yalnızca bir yükseltme etki sağlanıyor. Bu tür bir yeniden başlatma sırasında olacaktır hizmet VM'yi kapatın hello sırasında VM yeniden ve Bakım gerçekleştirilir. Çoğu DBMS satıcısı ancak hello birincil düğüm kullanılamıyorsa, başka bir düğümde hello DBMS Hizmetleri hızlı bir şekilde yeniden başlatılacak yüksek kullanılabilirlik ve olağanüstü durum kurtarma işlevsellik sağlar. Hello Azure platformu işlevselliği toodistribute VM'ler, depolama ve diğer Azure hizmetleriyle Bakım veya altyapı hataları planlanmış yükseltme etki alanları tooensure arasında yalnızca küçük bir alt kümesini sanal makineleri veya hizmetleri etkileyebilecek sunar.  Dikkatli planlama ile olası tooachieve kullanılabilirlik düzeyleri karşılaştırılabilir tooon içi altyapılar olur.

Microsoft Azure kullanılabilirlik kümeleri VM'ler mantıksal bir gruplandırması olan veya yalnızca sağlayacak şekilde bir düğümün kapanması herhangi bir noktada ( OkumazamanındaVM'lersağlarHizmetlerivediğerhizmetleridağıtılmıştoodifferenthataveyükseltmeetkialanlarıbirkümeiçindeolan[bu] [ virtual-machines-manage-availability] daha fazla ayrıntı için makale).

Burada görüldüğü gibi VM'ler sunulurken amacına göre yapılandırılmış toobe gerekir:

![Kullanılabilirlik kümesi'nin bir tanımı DBMS HA yapılandırmaları için][dbms-guide-figure-200]

DBMS dağıtımlarını (kullanılan hello tek tek DBMS HA işlevselliğini bağımsız olarak) yüksek oranda kullanılabilir yapılandırmaları toocreate istiyoruz, hello DBMS VM'ler gerekir:

* Merhaba VM'ler toohello eklemek aynı Azure sanal ağ (<https://azure.microsoft.com/documentation/services/virtual-network/>)
* Merhaba hello HA yapılandırmasının VM'ler hello olmalıdır aynı alt ağ. Ad çözümlemesi hello farklı alt ağlar arasında yalnızca bulut dağıtımında mümkün değil, yalnızca IP çözümleme çalışmayacak. Şirket içi dağıtımlar için siteden siteye veya ExpressRoute bağlantısı kullanarak en az bir alt ağla zaten kurulur. Ad çözümlemesi yapılması toohello according şirket içi AD ilkeleri ve ağ altyapısı.

[comment]: <> (MSSedusch Yapılacaklar Test ARM halen true olduğunda)

#### <a name="ip-addresses"></a>IP Adresleri
Toosetup hello VM'ler HA yapılandırmaları için esnek bir şekilde önerilir. IP adreslerini tooaddress hello HA ortaklarınızın hello HA yapılandırma içinde güvenmek, statik IP adresleri kullanılmadığı sürece Azure'da güvenilir değil. Azure'da iki "Kapat" kavram vardır:

* Azure Portal ya da Azure PowerShell cmdlet Stop-AzureRmVM kapatıldı: Bu durumda hello sanal makine kapatma alır ve XML'deki ayrılmış. Merhaba depolama için kullanılan erişimliye hello yalnızca ücretleri; bu nedenle Azure hesabınız artık bu VM için ücretlendirilir. Ancak, hello ağ arabiriminin hello özel IP adresini statik olduysa, başlangıç IP adresi serbest ve onu yeniden hello VM yeniden sonra atanan hello eski IP adresi hello ağ arabirimini alır garanti edilmez. Merhaba gerçekleştirme hello Azure Portal kapatmak veya Stop-AzureRmVM çağırarak otomatik olarak ayırmayı neden olur. Toodeallocat hello makinesi kullanımı Stop-AzureRmVM - StayProvisioned istemiyorsanız
* Merhaba VM OS düzeyinden kapatmak, hello VM kapatılır ve XML'deki tahsis. Ancak, bu durumda, Azure hesabınız hala hello VM kapatma olduğunu hello olgusuna karşın ücretlendirilir. Böyle bir durumda hello hello IP adresi tooa atamasının durdurulmuş VM değişmeden kalır. Hello kapatılıyor VM'den içinde otomatik olarak ayırmayı zorlayacak değil.

DHCP ayarları şirket içi ilkelerinde farklı olsa bile şirketler arası senaryolar için bile, varsayılan olarak bir kapatma ve ayırmayı hello devre dışı bırakma atamasının hello VM IP adreslerinden anlamına gelir.

* Merhaba özel bir statik IP adresi tooa ağ arabirimi olarak atarsa açıklanan [burada][virtual-networks-reserved-private-ip].
* Böyle bir durumda Hello ağ arabirimi silinmez sürece başlangıç IP adresi sabit kalır.

> [!IMPORTANT]
> Merhaba toosetup önerilir Temizle sipariş tookeep hello tüm dağıtımında basit ve yönetilebilir bir DBMS HA veya DR yapılandırmasında Azure içinde farklı VM'ler söz konusu hello arasında işlevsel bir ad çözümlemesi olacak şekilde ortaklık VM'ler hello.
>
>

## <a name="deployment-of-host-monitoring"></a>İzleme ana bilgisayarı dağıtımı
SAP uygulamaları Azure Virtual Machines'de verimli kullanımı SAP hello özelliği tooget hello Azure sanal makineleri çalıştıran fiziksel ana hello verilerden izleme ana bilgisayarı gerektirir. Belirli bir SAP HostAgent düzeltme eki düzeyi gerekir bu özelliği SAPOSCOL ve SAP HostAgent de sağlar. Merhaba tam düzeltme eki düzeyine SAP notta belgelenen [1409604].

Ana bilgisayar veri tooSAPOSCOL teslim bileşenleri dağıtımını ve bu bileşenlerin SAPHostAgent ve hello yaşam döngüsü yönetimi ile ilgili Hello Ayrıntılar için lütfen toohello başvurun [Dağıtım Kılavuzu][deployment-guide]

## <a name="3264829e-075e-4d25-966e-a49dad878737"></a>SQL Server özellikleri tooMicrosoft
### <a name="sql-server-iaas"></a>SQL Server Iaas
Microsoft Azure ile başlayarak, Windows Server Platformu tooAzure sanal makineler üzerinde oluşturulmuş, var olan SQL Server uygulamalarınızın kolayca geçirebilirsiniz. Bir sanal makinede SQL Server, bu uygulamaları tooMicrosoft Azure kolayca geçiş yaparak, tooreduce hello toplam sahip olma maliyetini dağıtım, yönetim ve Bakım Kurumsal avantajlarına uygulama sağlar. Bir Azure sanal makinesinde SQL Server ile yöneticiler ve geliştiriciler kullanılabilir aynı geliştirme ve Yönetim Araçları şirket içi hello kullanmaya devam edebilirsiniz.

> [!IMPORTANT]
> Biz hello Microsoft Azure platformu bir hizmet teklifi bir platformu olan Microsoft Azure SQL veritabanı ele değil unutmayın. Bu yazıdaki Hello tartışma şirket içi dağıtımlarda Azure Virtual Machines'de, yararlanmayı hello Azure hizmet yeteneğini olarak altyapı tanındığı hello SQL Server ürün hakkında çalışıyor. Veritabanı özellikleri ve İşlevler bu iki teklifler arasında farklı ve birbirleri ile mixed olmalıdır değildir. Ayrıca bkz: <https://azure.microsoft.com/services/sql-database/>
>
>

Tooreview önerilir [bu] [ virtual-machines-sql-server-infrastructure-services] devam etmeden önce belgeleri.

Hello yukarıdaki hello bağlantıyı altında hello belge bölümlerini aşağıdaki bölümlerde parçalarını birleştirilir ve belirtilen. SAP ile ilgili detaylar da açıklanan ve bazı kavramları daha ayrıntılı olarak açıklanmıştır. Ancak, hello SQL Server belirli belgeleri okuma önce hello belgeleri ilk yukarıda aracılığıyla toowork önerilir.

Iaas belirli bilgiler devam etmeden önce bilmeniz gereken bazı SQL Server vardır:

* **Sanal makine SLA**: Burada bulunan Azure'da çalışan sanal makineler için bir SLA yoktur: <https://azure.microsoft.com/support/legal/sla/>  
* **SQL sürüm desteği**: SAP müşteriler için desteklediğimiz SQL Server 2008 R2 ve Microsoft Azure sanal makinesi üzerinde daha yüksek. Önceki sürümleri desteklenmez. Bu genel gözden [destek deyimi](https://support.microsoft.com/kb/956893) daha fazla ayrıntı için. Lütfen Genel SQL Server 2008 Microsoft tarafından da desteklendiğini unutmayın. Ancak toosignificant, tanıtılan SAP ile SQL Server 2008 R2 için SQL Server 2008 R2 hello en düşük sürüm SAP için bir işlevdir. SQL Server 2012 ve 2014 (doğrudan Azure Storage karşı yedekleme gibi) hello Iaas senaryosu içine daha derin Tümleştirmesi ile genişletilmiş aklınızda bulundurun. Bu nedenle, biz bu kağıt tooSQL Server 2012 ve en son düzeltme eki düzeyiyle 2014 Azure için kısıtlayın.
* **SQL özellik desteği**: en SQL Server özellikleri, bazı özel durumlar ile Microsoft Azure sanal makinelerinde desteklenir. **SQL Server Paylaşılan diskleri kullanarak Yük Devretme Kümelemesi desteklenmiyor**.  Veritabanı yansıtma, AlwaysOn Kullanılabilirlik grupları, çoğaltma, günlük aktarma ve hizmet Aracısı tek bir Azure bölge içinde desteklenen gibi teknolojileri dağıtılmış. SQL Server AlwaysOn de desteklenir farklı Azure bölgeler arasında burada açıklandığı gibi: <https://blogs.technet.com/b/dataplatforminsider/archive/2014/06/19/sql-server-alwayson-availability-groups-supported-between-microsoft-azure-regions.aspx>.  Gözden geçirme hello [destek deyimi](https://support.microsoft.com/kb/956893) daha fazla ayrıntı için. Nasıl toodeploy AlwaysOn yapılandırmasını gösterilen üzerinde örnek [bu] [ virtual-machines-workload-template-sql-alwayson] makalesi. Ayrıca, en iyi yöntemler belgelenen hello denetleyin [burada][virtual-machines-sql-server-infrastructure-services]
* **SQL performans**: Microsoft Azure barındırılan sanal makinelerin karşılaştırma tooother genel bulut sanallaştırma teklifleri, ancak tek tek sonuç çok iyi gerçekleştirecek değişebilir emin duyuyoruz. Kullanıma [bu] [ virtual-machines-sql-server-performance-best-practices] makalesi.
* **Azure Marketi'nden görüntüleri kullanarak**: hello en hızlı yolu toodeploy yeni bir Microsoft Azure VM olduğu toouse hello Azure Marketi görüntüden. SQL Server içeren hello Azure Market görüntülerini vardır. SQL Server zaten yüklü hello görüntüleri hemen SAP NetWeaver uygulamaları için kullanılamaz. Merhaba hello varsayılan SQL Server Harmanlama bu görüntüleri ve SAP NetWeaver sistemleri için gerekli olmayan hello harmanlama içinde yüklü nedenidir. İçinde bu tür görüntüleri toouse sipariş, bölümde belgelenen hello adımları gözden geçirin [görüntüleri hello Microsoft Azure Market dışında bir SQL Server'ı kullanarak][dbms-guide-5.6].
* Kullanıma [fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/) daha fazla bilgi için. Merhaba [SQL Server 2012 lisans Kılavuzu](https://download.microsoft.com/download/7/3/C/73CAD4E0-D0B5-4BE5-AB49-D5B886A5AE00/SQL_Server_2012_Licensing_Reference_Guide.pdf) ve [SQL Server 2014 lisans Kılavuzu](https://download.microsoft.com/download/B/4/E/B4E604D9-9D38-4BBA-A927-56E4C872E41C/SQL_Server_2014_Licensing_Guide.pdf) de önemli bir kaynaktır.

### <a name="sql-server-configuration-guidelines-for-sap-related-sql-server-installations-in-azure-vms"></a>Azure vm'lerinde SQL Server yüklemelerini SAP için SQL Server yapılandırma yönergeleri ilgili
#### <a name="recommendations-on-vmvhd-structure-for-sap-related-sql-server-deployments"></a>SQL Server dağıtımları VM/VHD yapısı hakkında öneriler SAP için ilgili
Merhaba Genel Açıklama uygun olarak SQL Server yürütülebilir dosyalar bulunabilir veya hello sistem sürücüsüne hello VM'ın temel VHD yüklü (C: sürücüsü\).  Genellikle, hello SQL Server sistem veritabanlarının en yüksek düzeyde SAP NetWeaver iş yükü tarafından kullanılmaz. Bu nedenle hello sistem veritabanları (master, msdb ve model) SQL Server'ın C:\ sürücüsü hello üzerinde kalabilir. Bir özel durum, daha yüksek veri birimi veya hello sığamıyorsa g/ç işlemleri birimi gerektirebilir hello durumda bazı SAP ERP ve tüm BW iş yükleri, tempdb olabilir özgün VM. Bu tür sistemler için aşağıdaki adımları hello gerçekleştirilmelidir:

* Merhaba birincil tempdb veri dosyaları toohello taşıma hello SAP veritabanının hello birincil veri dosyaları olarak aynı mantıksal sürücü.
* Merhaba, tüm ek tempdb veri dosyaları tooeach hello SAP kullanıcı veritabanı veri dosyasını içeren diğer mantıksal sürücüler ekleyin.
* Merhaba kullanıcı veritabanının günlük dosyası içeren hello tempdb günlük dosyası toohello mantıksal sürücü ekleyin.
* **Yalnızca yerel SSD kullanmak VM türleri için** hello işlem düğümü tempdb veri ve günlük dosyaları D:\ sürücüsüne hello yerleştirilmiş olabilir. Bununla birlikte, olabilecek birden çok tempdb veri dosyalarını toouse önerilir. Merhaba üzerinde VM türüne göre D:\ sürücüsüne birimlerin farklı unutmayın.

Bu yapılandırmalar tempdb tooconsume hello sistem sürücüsünün tooprovide mümkün olandan daha fazla alan etkinleştirin. Sipariş toodetermine hello uygun tempdb boyutu, bir şirket içi varolan sistemlerde hello tempdb boyutları kontrol edebilirsiniz. Ayrıca, bu tür bir yapılandırma IOPS numaraları hello sistem sürücüsü ile sağlanan tempdb karşı etkinleştirir. Yeniden hello IOPS numaraları, tempdb üzerinde toosee beklediğiniz türetilemeyeceğini böylece şirket içi çalışan sistemlerde kullanılan toomonitor g/ç iş yükü tempdb karşı olabilir.

SAP veritabanı ile SQL Server çalıştığı ve tempdb veri ve günlük dosyası tempdb hello D:\ sürücüsüne nereye yerleştirileceğini bir VM yapılandırması gibi görünür:

![Azure Iaas VM SAP için başvuru yapılandırması][dbms-guide-figure-300]

Farklı boyutlarda hello VM türü üzerinde bağımlı bu hello D:\ sürücüsüne sahip unutmayın. Zorlanmış toopair tempdb veri olabilir hello boyut gereksinimini tempdb bağımlı ve günlük dosyaları hello ile veritabanı veri SAP ve günlük dosyaları D:\ sürücüsüne çok küçük olduğu durumlarda.

#### <a name="formatting-hello-vhds"></a>Merhaba VHD'ler biçimlendirme
SQL Server hello SQL Server veri ve günlük içeren VHD için NTFS blok boyutu için dosyaları 64 K olmalıdır. Hiçbir gerek tooformat hello D:\ sürücüsüne yoktur. Bu sürücü önceden biçimlendirilmiş gelir.

Merhaba geri yüklemek veya veritabanları oluşturmayı hello veri dosyalarını hello dosyaları Merhaba içeriğine sıfırlama tarafından başlatılıyor değil, aşağıdakilerden emin olmanız gerekir emin sipariş toomake hello kullanıcı bağlamı hello SQL Server hizmetinin çalıştığını belirli bir iznine sahiptir. Genellikle hello Windows Yönetici grubundaki kullanıcılar bu izinlere sahip. Merhaba SQL Server hizmeti hello kullanıcı bağlamında Windows yönetici olmayan kullanıcı çalıştırırsanız, o kullanıcı hello kullanıcı hakkı 'Birim bakım görevlerini' tooassign gerekir.  Bu Microsoft Bilgi Bankası makalesi Hello ayrıntıları bakın: <https://support.microsoft.com/kb/2574695>

#### <a name="impact-of-database-compression"></a>Veritabanı Sıkıştırma etkisi
Burada g/ç bant genişliği sınırlayıcı bir etmen haline gelebilir yapılandırmalarında IOPS azaltır her ölçü bir Azure gibi bir Iaas senaryosu çalıştırabilirsiniz toostretch hello iş yükü yardımcı olabilir. Varolan bir SAP karşıya tooAzure veritabanları önce bu nedenle, henüz yapıldığında, SQL Server sayfasında sıkıştırma uygulama SAP ve Microsoft tarafından önerilir.

Merhaba öneri tooperform veritabanı sıkıştırma tooAzure karşıya yüklemeden önce dışında iki nedenleri verilmiştir:

* karşıya veri toobe Hello miktarını düşüktür.
* varsayılarak g/ç gecikmesi şirket içi daha az veya daha fazla CPU veya daha yüksek g/ç bant genişliği ile daha güçlü donanım kullanabilirsiniz hello sıkıştırma yürütme hello süresi kısadır.
* Daha küçük veritabanı boyutları disk ayırmayı tooless maliyetlerini neden olabilir

Şirket içi yaptığı gibi veritabanı sıkıştırma de bir Azure sanal makinelerde çalışır. Nasıl toocompress varolan bir SAP SQL Server veritabanını lütfen burayı hakkında daha fazla bilgi: <https://blogs.msdn.com/b/saponsqlserver/archive/2010/10/08/compressing-an-sap-database-using-report-msscompress.aspx>

### <a name="sql-server-2014--storing-database-files-directly-on-azure-blog-storage"></a>SQL Server 2014 – veritabanı dosyaları doğrudan üzerinde Azure blogu depolama
SQL Server 2014 hello olasılığı toostore veritabanı dosyaları doğrudan Azure Blob deposu hello VHD etrafında ' sarmalayıcı' olmadan açılır. Standart Azure depolama veya daha küçük VM türleri kullanmaya özellikle bu uygulanabiliyordu IOPS takılı toosome küçük VM türler olabilir VHD'ler sınırlı sayıda tarafından hello sınırları burada üstesinden senaryolara olanak sağlar. Bu, ancak SQL Server'ın sistem veritabanları için kullanıcı veritabanlarını için çalışır. Ayrıca, SQL Server'ın veri ve günlük dosyaları için çalışır. SAP SQL Server'ı toodeploy isterseniz bu şekilde yerine veritabanı 'VHD'ler kaydırma' Lütfen hello aşağıdakileri göz önünde bulundurun:

* Merhaba kullanılan depolama hesabı gereksinimlerini toobe VM SQL Server çalıştıran kullanılan toodeploy hello olan bir hello gibi aynı Azure bölgesindeki hello.
* Farklı Azure depolama hesapları daha önce bakımından toodistribute VHD'ler listelenen konular dağıtımları da bu yöntem için geçerlidir. Anlamına gelir, g/ç işlemlerinin sayısı hello Azure depolama hesabı hello sınırları karşı hello.

[comment]: <> (MSSedusch Yapılacaklar ancak yoktur bunu ağ bant genişliği ve depolama bant genişliği değil, kullanacaksınız?)

Bu dağıtım türü hakkındaki ayrıntıları burada listelenir: <https://msdn.microsoft.com/library/dn385720.aspx>

Azure Premium Storage üzerinde doğrudan sipariş toostore SQL Server veri dosyaları burada belgelenen toohave en az bir SQL Server 2014 düzeltme eki yayın gerekir: <https://support.microsoft.com/kb/3063054>. Azure Standard Storage SQL Server veri dosyalarını depolamak yayımlanan hello sürümü SQL Server 2014 ile çalışır. Ancak, hello çok aynı düzeltme ekleri hello SQL Server veri dosyaları ve yedekler için Azure Blob Storage'nın doğrudan kullanımını daha güvenilir hale düzeltmeleri başka bir dizi içerir. Bu nedenle toouse bu düzeltme ekleri genel öneririz.

### <a name="sql-server-2014-buffer-pool-extension"></a>SQL Server 2014 arabellek havuzu genişletme
SQL Server 2014 arabellek havuzu genişletme olarak adlandırılan yeni bir özellik sunulmuştur. Bu işlev bir sunucunun yerel SSD veya VM tarafından yedeklenen bir ikinci düzey önbellek ile bellekte tutulan SQL Server'ın hello arabellek havuzu genişletir. Bu tookeep 'ın bellek' verilerin daha büyük bir çalışma kümesi sağlar. Karşılaştırılan tooaccessing Azure Standard Storage hello Azure VM'deki yerel SSD'ler üzerinde depolanan hello arabellek havuzu hello uzantısı Access'e birçok faktöre daha hızlıdır.  Bu nedenle, mükemmel IOPS ve üretilen iş hello VM türleri hello yerel D:\ sürücüsüne yararlanarak IOPS Azure depolama karşı yükler ve sorguların yanıt sürelerini önemli ölçüde artırmak bir çok makul bir yolu tooreduce hello olabilir. Bu, özellikle Premium depolama kullanıldığında geçerlidir. Premium depolama ve hello Premium Azure okuma önbelleği hello işlem düğümü üzerinde hello kullanımı durumunda, veri dosyaları için önerilen gibi büyük fark beklenir. Her iki önbellekleri (SQL Server arabellek havuzu genişletme ve Premium depolama okuma önbelleği) hello işlem düğümleri hello yerel diskler kullanıyorsanız nedenidir.
Bu işlevsellik hakkında daha fazla ayrıntı için lütfen bu belgelere bakın: <https://msdn.microsoft.com/library/dn133176.aspx>

### <a name="backuprecovery-considerations-for-sql-server"></a>SQL Server için yedekleme/kurtarma konuları
SQL Server Azure'a dağıtırken yedekleme yönteminize gözden geçirilmesi gerekir. Merhaba sistem üretken sistem olsa bile, SQL Server tarafından barındırılan hello SAP veritabanında düzenli aralıklarla yedeklenmelidir. Azure Storage üç görüntüleri tutar, bir yedekleme şimdi saygı toocompensating depolama çökmeyle daha az önemlidir. uygun bir yedekleme ve kurtarma planı korumak için hello öncelik zaman kurtarma özellikleri noktasında sağlayarak mantıksal/el ile hataları dengeleyebilirsiniz daha fazla nedenidir. Merhaba hedef tooeither kullanım yedeklemeleri toorestore hello veritabanı yedeklemesi olacak şekilde tooa belirli noktası Azure tooseed zaman ya da toouse hello yedeklere içinde başka bir sistem hello varolan veritabanı kopyalayarak. Örneğin, bir katman 2 SAP yapılandırma tooa 3 katmanlı sistem kurulumundan hello aynı aktaramıyor bir yedeğini geri tarafından sistem.

Üç farklı şekilde toobackup SQL Server tooAzure depolama vardır:

1. SQL Server 2012 CU4 ve daha yüksek can yerel yedekleme veritabanları tooa URL. Bu hello blog ayrıntılı [SQL Server 2014 – bölümü 5 – yedekleme/geri yükleme geliştirmeleri yeni işlevselliği](https://blogs.msdn.com/b/saponsqlserver/archive/2014/02/15/new-functionality-in-sql-server-2014-part-5-backup-restore-enhancements.aspx). Bölüm bkz [SQL Server 2012 SP1 CU4 ve daha sonra][dbms-guide-5.5.1].
2. SQL Server sürümleri önceki tooSQL 2012 CU4, yeniden yönlendirme işlevselliği toobackup tooa VHD kullanın ve temel olarak yapılandırılmış bir Azure depolama konumu doğru hello yazma akışı taşıyın. Bölüm bkz [SQL Server 2012 SP1 CU3 ve önceki sürümler][dbms-guide-5.5.2].
3. Merhaba son tooperform geleneksel SQL Server Yedekleme toodisk komutu bir VHD disk cihaza yöntemidir.  Bu aynı toohello şirket içi dağıtım modeli ve bu belgede ayrıntılı ele alınmamıştır.

#### <a name="0fef0e79-d3fe-4ae2-85af-73666a6f7268"></a>SQL Server 2012 SP1 CU4 ve sonraki sürümler
Bu işlev toodirectly yedekleme tooAzure BLOB Depolama sağlar. Bu yöntem, VHD ve IOPS kapasite kullanılmasına neden olur tooother Azure VHD'ler yedekleme gerekir. Merhaba temelde bu olur:

 ![SQL Server 2012 yedekleme tooMicrosoft Azure Storage BLOBUNA kullanma][dbms-guide-figure-400]

Merhaba avantajı, bu durumda bir toospend VHD'ler toostore SQL Server yedekleri üzerinde gerekmez olur. Bu nedenle ayrılmış daha az VHD'lerin sahip ve VHD IOPS hello tüm bant genişliği veri ve günlük dosyaları için kullanılabilir. Lütfen bir yedekleme hello en büyük boyutu bu makalede 'Sınırlamaları' hello bölümünde açıklandığı gibi sınırlı tooa en fazla 1 TB olduğunu unutmayın: <https://msdn.microsoft.com/library/dn435916.aspx#limitations>. SQL Server Yedekleme sıkıştırma kullanılarak rağmen yedekleme boyutu Merhaba, 1 TB boyutunda aşacak, işlevsellik bölümde açıklanan hello [SQL Server 2012 SP1 CU3 ve önceki sürümler] [ dbms-guide-5.5.2] bu belgede gerekiyor kullanılan toobe.

[İlgili belgelere](https://msdn.microsoft.com/library/dn449492.aspx) hello geri yükleme Azure Blob depolamaya karşılık yedeklerden veritabanlarının açıklayan önerilir değil toorestore doğrudan Azure BLOB depolama alanından hello yedeklemeleri ise > 25 GB. Bu makalede Hello öneri, performans değerlendirmeleri ve toofunctional kısıtlamaları nedeniyle değil yalnızca esas alır. Bu nedenle, farklı koşullar bir olay temelinde uygulanabilir.

Bu yedekleme türünü ayarlamak ve diğer işlevden nasıl belgelerine bulunabilir [bu](https://msdn.microsoft.com/library/dn466438.aspx) Öğreticisi

Adımlar hello dizisini örneği okunabilir [burada](https://msdn.microsoft.com/library/dn435916.aspx).

Yedeklemeleri otomatikleştirme, en yüksek önem toomake hello BLOB'lar her yedekleme için farklı adlandırılmış emin olur. Aksi takdirde bunların üzerine yazılacak ve hello restore zinciri bozulur.

Değil toomix şeyler hello 3 farklı yedekleme türleri arasında yukarı sırayla önerilir toocreate farklı kapsayıcılar yedeklemeler için kullanılan hello depolama hesabı altında değil. Merhaba kapsayıcılara VM tarafından yalnızca veya VM ve yedekleme türüne göre olabilir. Merhaba şema gibi görünebilir:

 ![SQL Server 2012 yedekleme tooMicrosoft Azure Storage BLOBUNA – ayrı depolama hesabı altında farklı kapsayıcılar kullanma][dbms-guide-figure-500]

Yukarıdaki, hello yedeklemeleri aynı depolama hesabı hello burada hello gerçekleştirilen değil hello örnek VM'ler dağıtılır. Özellikle hello yedekleri için yeni bir depolama hesabı olacaktır. İçindeki Hello depolama hesaplarını, yedekleme ve hello VM adı hello türünün bir matris oluşturulan farklı kapsayıcılar olacaktır. Bu tür bir kesimlere ayırma hello daha kolay tooadministrate hello yedeklerini yapar farklı VM'ler.

bir doğrudan hello yedeklemeler, yazar hello BLOB'ları değil hello VM VHD'leri toohello sayısı ekleniyor. Bu nedenle bir durum, hello özel VM SKU hello veriler için oluşturulmuş VHD'ler hello maksimum en üst düzeye ve işlem günlük dosyası ve bir depolama kapsayıcısı karşı yedek çalıştırmaya devam.

#### <a name="f9071eff-9d72-4f47-9da4-1852d782087b"></a>SQL Server 2012 SP1 CU3 ve önceki sürümleri
hello ilk adımı gerçekleştirmeniz gerekir sipariş tooachieve doğrudan Azure Storage'a karşı yedek çok bağlantılı toodownload hello MSI olacaktır[bu](https://www.microsoft.com/download/details.aspx?id=40740) KBA makalesi.

Merhaba x64 yükleme dosyasını ve hello belgelerine indirin. Merhaba dosya adlı bir program yükler: 'Microsoft SQL Server Yedekleme tooMicrosoft Azure Aracı'. Merhaba belgelerini hello ürünün baştan sona okuyun.  Merhaba aracı temelde hello aşağıdaki şekilde çalışır:

* SQL sunucu tarafı Hello hello SQL Server Yedekleme için bir disk konumu tanımlanır (Merhaba D:\ sürücüsüne bu kullanmayın).
* Merhaba aracı yedeklemeleri toodifferent Azure Storage kapsayıcıları kullanılan toodirect farklı türlerde olabilen toodefine kuralları izin verir.
* Merhaba kuralları yerinde olduktan sonra hello aracı hello VHD/diskleri toohello daha önce tanımlanan Azure depolama konumu, yedek tooone hello hello yazma akışı yönlendirir.
* Merhaba aracı birkaç KB boyutunda küçük saplama dosyası hello hello SQL Server için tanımlanan VHD/Disk üzerinde yedekleme bırakır. **Azure depolama biriminden yeniden gerekli toorestore olduğundan bu dosyayı hello depolama konumunda bırakılmalıdır.**
  * Kayıp hello saplama dosya (örneğin aracılığıyla hello saplama dosyası bulunan hello depolama medyası kaybı) ve Microsoft Azure depolama hesabı tooa yedekleme hello seçeneği seçtiniz, hello saplama dosyası aracılığıyla Microsoft Azure Storage tarafından kurtarabilir. içinde yerleştirildiği hello depolama kapsayıcıdan yükleniyor. Merhaba saplama dosyası ardından hello aracı yapılandırılmış toodetect ve karşıya yükleme toohello olduğu bir hello yerel makinedeki klasörüne yerleştirebilirsiniz hello ile aynı kapsayıcı şifreleme hello özgün kuralla kullandıysanız aynı şifreleme parolası.

Bu, hello şema de, bir Azure depolama konumu doğrudan adresi sağlanıyor SQL Server sürümleri için yerinde SQL Server'ın daha yeni sürümleri için yukarıda açıklandığı gibi yerleştirilebileceği anlamına gelir.

Bu yöntem kullanılmamalıdır yedekleme yukarı yerel olarak Azure Storage karşı destekleyen daha yeni SQL Server sürümleri ile. Merhaba yerel yedekleme sınırlamaları Azure içine Azure içine yerel yedekleme yürütme burada engelliyor durumlardır.

#### <a name="other-possibilities-toobackup-sql-server-databases"></a>Diğer olasılıklar toobackup SQL Server veritabanları
Diğer olasılıklar toobackup veritabanları tooattach ek VHD'ler tooa üzerinde toostore yedeklemeleri kullanmak VM olur. Toomake emin gerekir durumda o hello VHD'ler çalışmıyor tam. Merhaba durum söz konusuysa toounmount hello VHD gerekir ve bu nedenle toospeak 'arşivlemek' ve yeni bir boş VHD ile değiştirin. Bu yol giderseniz, hello VHD'ler hello veritabanı dosyaları hello olanları ayrı Azure depolama hesaplarından içinde bu VHD'leri tookeep istiyorsunuz.

İkinci bir olasılık toouse bağlı pek çok VHD'ye sahip olabilir büyük bir VM olabilir. Örneğin D14 32VHDs ile. Depolama alanları toobuild, paylaşımlar, oluşturduğunuz esnek bir ortam kullanılan sonra yedekleme hedefleri olarak hello farklı DBMS sunucuları için kullanın.

Bazı en iyi uygulamalar belgelenen [burada](https://blogs.msdn.com/b/sqlcat/archive/2015/02/26/large-sql-server-database-backup-on-an-azure-vm-and-archiving.aspx) de.

#### <a name="performance-considerations-for-backupsrestores"></a>Yedekleme/geri yüklemeler için başarım düşünceleri
Çıplak dağıtımlar olduğu gibi yedekleme/geri yükleme performans paralel şekilde kaç tane birimleri okunabilir ve hangi hello verimlilik bu birimlerin olabilir bağlıdır. Ayrıca, hello yedekleme sıkıştırma tarafından kullanılan CPU tüketimi yalnızca too8 CPU iş parçacıklarını ile sanal makineleri üzerinde önemli bir rol oynayabilir. Bu nedenle, bir kabul edebilirsiniz:

* Merhaba VHD'ler daha az hello sayısı toostore hello veri dosyaları, hello kullanılan küçük, genel üretilen işi okuma hello.
* Merhaba VM CPU iş parçacıkları daha küçük hello sayısı Merhaba, yedekleme sıkıştırma daha ciddi hello etkisini hello.
* Merhaba daha az hedefleri (BLOB veya VHD) toowrite yedekleme Merhaba, daha az hello verimlilik hello.
* daha küçük hello VM boyutu Merhaba, daha küçük hello depolama verimliliği kota yazma ve okuma Azure depolama biriminden hello. Bağımsız olup hello yedeklemeler Azure Blob doğrudan depolanır veya Azure BLOB'ları yeniden depolanan VHD olup depolanır.

Microsoft Azure Storage BLOBUNA daha yeni sürümlerde hello yedekleme hedefi olarak kullanırken, belirli her yedekleme için kısıtlı toodesignating yalnızca bir URL hedefi olan.

Ancak hello 'Microsoft SQL Server Yedekleme tooMicrosoft Azure Aracı' eski sürümleri kullanırken, birden fazla dosya hedef tanımlayabilirsiniz. Birden fazla hedef hello yedekleme ölçeklendirebilirsiniz ve hello hello yedekleme verimini daha yüksektir. Bundan sonra birden çok dosyalarında de hello Azure depolama hesabı neden olacaktır. Bizim bir kesinlikle bir hello yedekleme uzantılarıyla elde hello verimlilik elde edebilirsiniz birden çok dosya hedefleri kullanarak SQL Server 2012 SP1 CU4 üzerinde gelen uygulanan. Ayrıca hello yerel yedekleme olduğu gibi hello 1 TB sınırı tarafından Azure'da engellenmez.

Ancak, göz önünde bulundurmanız, hello verimliliği de hello hello yedekleme için kullandığınız Azure depolama hesabı hello konumunu bağlı. Sanal makineleri çalıştıran farklı bir bölgede hello daha toolocate hello depolama hesabı hakkında bir fikir olabilir. Örneğin Batı Avrupa'da hello VM yapılandırması çalıştırıldı ancak hello depolama Kuzey Avrupa'da yukarı karşı tooback kullandığınız hesabı put. Kesinlikle hello yedekleme verimlilik üzerinde etkisi olacaktır ve burada hello hedef depolama ve sanal makineleri hello durumlarda mümkün toobe hello çalıştıran göründüğü olası değil toogenerate 150 MB/sn verimde olduğu aynı bölgesel veri merkezi.

#### <a name="managing-backup-blobs"></a>Yedekleme BLOB'ları yönetme
Yoktur gereksinim toomanage hello yedeklemeler, kendi. Merhaba Beklenti birçok BLOB'lar sık işlem günlüğü yedeklemeleri yürüterek oluşturulacak olduğundan, bu BLOB yönetim kolayca hello Azure Portal bırakacak. Bu nedenle recommendable tooleverage bir Azure Storage Gezgini olur. Bir Azure depolama hesabı toomanage yardımcı olan çeşitli iyi kullanılabilir olanlarla vardır

* Microsoft Visual Studio Azure SDK'sı (<https://azure.microsoft.com/downloads/>)
* Microsoft Azure Depolama Gezgini (<https://azure.microsoft.com/downloads/>)
* 3. taraf araçları

[comment]: <> (ARM üzerinde henüz desteklenmiyor)
[comment]: <> (### Azure VM yedekleme)
[comment]: <> (Merhaba SAP sistem VM, Azure sanal makine yedekleme işlevi kullanılarak yedeklenebilir. Azure sanal makine yedeklemesi erken hello yıl 2015 sunulan ve bu arada standart yöntemi toobackup bir tam VM azure'da. Azure yedekleme Azure'da hello yedeklemeleri depolar ve geri yükleme bir VM'nin yeniden sağlar.)
[comment]: <> (Merhaba DBMS sistemlerini destekleyen Windows VSS birim gölge kopyası hizmeti Merhaba, tutarlı bir şekilde de çalıştırma veritabanları yedeklenebilir VM'ler < SQL sunucusu olarak https://msdn.microsoft.com/library/windows/desktop/bb968832.aspx> yapar. Azure VM Yedekleme kullanarak geri yüklenebilen bir şekilde tooget tooa böylece SAP veritabanı yedekleme. Ancak, zaman içinde nokta geri yükler veritabanları Azure VM yedeklemelerin dayalı mümkün olmadığını unutmayın. Bu nedenle, Azure VM Backup kalmak yerine DBMS işlevsellikle veritabanlarının yedeklerini tooperform hello önerilir.)
[comment]: <> (Azure sanal makine yedekleme ile tanıdık tooget Lütfen başlatın burada < https://azure.microsoft.com/documentation/services/backup/>)

### <a name="1b353e38-21b3-4310-aeb6-a77e7c8e81c8"></a>Merhaba Microsoft Azure Market dışında bir SQL Server görüntüleri kullanma
Microsoft sanal makineleri hello zaten SQL Server sürümleri içeren Azure Market sunar. SQL Server ve Windows için lisanslar gerektirir SAP müşteriler için bu SQL Server zaten yüklü olan VM'ler yukarı dönen göre lisans bir fırsat toobasically kapak hello ihtiyacı olabilir. Sipariş toouse SAP, bu tür görüntülerde yapılan toobe ilgili önemli noktalar aşağıdaki hello gerekir:

* Merhaba SQL Server olmayan değerlendirme sürümleri, Azure Marketi'nden dağıtılan yalnızca bir 'Yalnızca Windows' VM'den daha yüksek maliyetleri alın. Lütfen bu makaleler toocompare fiyatları bakın: <https://azure.microsoft.com/pricing/details/virtual-machines/> ve <https://azure.microsoft.com/pricing/details/virtual-machines/#Sql>.
* Yalnızca SQL Server 2012 gibi SAP tarafından desteklenen SQL Server sürümleri de kullanabilirsiniz.
* hangi hello Azure Marketi sunulan hello VM'ler yüklü hello SQL Server örneğinin Hello harmanlaması hello harmanlama SAP NetWeaver hello SQL Server örneği toorun gerektirir değil. Hello harmanlama hello yönde olsa hello bölümü aşağıdaki ile değiştirebilirsiniz.

#### <a name="changing-hello-sql-server-collation-of-a-microsoft-windowssql-server-vm"></a>Merhaba SQL Server Harmanlama bir Microsoft Windows/SQL Server VM düzenini değiştirme
SAP NetWeaver uygulamalar tarafından gerekli olan toouse hello harmanlama yukarı hello Azure Marketi Hello SQL Server görüntülerinin ayarlanmamış olduğundan, hemen hello dağıtımdan sonra değiştirilen toobe gerekir. SQL Server 2012 için bu hello ile yapılabilir adımları izleyerek hello VM dağıtıldıktan ve yönetici edebilir hemen hello içine toolog VM dağıtılabilir:

* 'Yönetici olarak' bir Windows komut penceresi açın.
* Merhaba dizin tooC:\Program Files\Microsoft SQL Server\110\Setup Bootstrap\SQLServer2012 değiştirin.
* Merhaba komutu yürütün: Setup.exe/QUIET/eylem REBUILDDATABASE/InstanceName = MSSQLSERVER /SQLSYSADMINACCOUNTS = =`<local_admin_account_name`> /SQLCOLLATION SQL_Latin1_General_Cp850_BIN2 =   
  * `<local_admin_account_name`> merhaba yönetici hesabıyla hello Merhaba VM hello Galerisi üzerinden ilk kez dağıtırken tanımlanan hello hesabıdır.

Merhaba işlem yalnızca birkaç dakika sürer. Merhaba adım hello doğru sonucu ile sonuçlandı olup olmadığını emin sipariş toomake Lütfen hello aşağıdaki adımları gerçekleştirin:

* SQL Server Management Studio’yu açın.
* Bir sorgu penceresi açın.
* Merhaba komutu sp_helpsort hello SQL Server ana veritabanında yürütün.

İstenen hello sonuç gibi görünmelidir:

    Latin1-General, binary code point comparison sort for Unicode Data, SQL Server Sort Order 40 on Code Page 850 for non-Unicode Data

Merhaba sonuç değilse SAP dağıtma DURDURUN ve neden hello Kurulum komutu beklendiği gibi çalışmadı araştırın. Biri yukarıdaki hello daha farklı SQL Server kod sayfaları ile SQL Server örneği üzerine SAP NetWeaver uygulamalarının dağıtımını olan **değil** desteklenir.

### <a name="sql-server-high-availability-for-sap-in-azure"></a>SQL Server yüksek kullanılabilirlik için SAP Azure
Bu makalede daha önce belirtildiği gibi hello eski SQL Server yüksek kullanılabilirlik işlevselliği hello kullanımı için gerekli olan hiçbir olasılığı toocreate paylaşılan depolama birimi yok. Bu işlev, bir Windows Server Yük devretme kümesi (paylaşılan disk hello kullanıcı veritabanlarını (ve tempdb sonunda) kullanarak WSFC) iki veya daha fazla SQL Server örnekleri yüklenir. Ayrıca SAP tarafından desteklenmeyen hello uzun zaman standart yüksek kullanılabilirlik yöntem budur. Azure paylaşılan depolama desteklemediğinden, SQL Server yüksek kullanılabilirlik yapılandırmaları bir paylaşılan disk küme yapılandırmasına sahip gerçekleşen alamazsınız. Ancak, diğer birçok yüksek kullanılabilirlik yöntemi hala olası ve hello aşağıdaki bölümlerde açıklanmıştır.

[comment]: <> (Hala başvuruyor tooASM makaledir)
[comment]: <> (Azure SQL Server için Hello farklı belirli yüksek kullanılabilirlik teknolojileri kullanılabilir okumadan önce daha fazla ayrıntı ve işaretçiler sağlayan çok iyi bir belge yok [burada] [ Virtual-Machines-SQL-Server-High-availability-and-Disaster-Recovery-Solutions])

#### <a name="sql-server-log-shipping"></a>SQL Server günlük aktarma
Yüksek kullanılabilirlik (HA) hello yöntemlerini SQL Server günlük aktarma biridir. Merhaba HA yapılandırmasında katılan hello VM'ler ad çözümlemesi çalışma varsa, herhangi bir sorun yoktur ve azure'da hello Kurulum şirket içi yapılan herhangi bir ayar farklı değil. Yalnızca IP çözümleme üzerinde toorely önerilmez. Bakımından günlük aktarma ve günlük aktarma geçici hello ilkeleri toosetting Lütfen bu belgeleri denetleyin:

<https://technet.microsoft.com/library/ms187103.aspx>

Sipariş tooreally herhangi bir yüksek oranda kullanılabilirlik elde etmek, bir toodeploy hello gibi bir günlük aktarma yapılandırma toobe içinde içinde aynı Azure kullanılabilirlik kümesi hello olan VM'ler gerekiyor.

#### <a name="database-mirroring"></a>Veritabanı yansıtma
SAP tarafından desteklenen gibi veritabanı yansıtma (SAP nota bakın [965908]) hello SAP bağlantı dizesi bir yük devretme ortağı tanımlama kullanır. İki VM hello olan bu hello varsayıyoruz Hello şirketler arası durumlarda, aynı etki alanında ve hello kullanıcı bağlamı hello iki SQL Server örnekleri altında çalışmakta etki alanı kullanıcıları ve hello iki SQL Server örnekleri dahil edilen yeterli ayrıcalıklara sahip. Bu nedenle, veritabanı yansıtma azure'da hello kurulumu tipik şirket içi kurulum/yapılandırma farklı değildir.

Yalnızca bulut dağıtımında toohave hello en kolay yöntem olarak başka bir etki alanı kurulum içinde Azure toohave bu DBMS VM'ler (ve ideal özel SAP VM'ler) içinde bir etki alanı.

Bir etki alanı mümkün değilse, sertifikaları uç noktalar burada açıklandığı şekilde yansıtma hello veritabanı için de kullanabilirsiniz: <https://technet.microsoft.com/library/ms191477.aspx>

Bir öğretici tooset yukarı veritabanı yansıtma Azure şurada bulunabilir: <https://technet.microsoft.com/library/ms189852.aspx>

#### <a name="alwayson"></a>AlwaysOn
AlwaysOn SAP şirket içi desteklenenler (SAP nota bakın [1772688]), SAP Azure ile birlikte kullanılan desteklenen toobe değil. Azure paylaşılan mümkün toocreate diskleri değil misiniz hello olgu biri farklı VM'ler arasında bir AlwaysOn Windows Server Yük devretme kümesi (WSFC) yapılandırması oluşturulamıyor anlamına gelmez. Bu yalnızca, hello olasılığı toouse paylaşılan disk hello küme yapılandırmasında bir çekirdek olarak sahip olmadığını anlamına gelir. Bu nedenle Azure AlwaysOn WSFC yapılandırmasında oluşturmak ve paylaşılan disk kullanır hello çekirdek türü seçin değil yeterlidir. Hello Azure ortamı bu VM'lerin içinde dağıtılan VM'ler adıyla hello ve hello VM'ler hello olmalıdır çözümlenmelidir aynı etki alanı. Bu seçenek, yalnızca Azure ve şirket içi dağıtımları için geçerlidir. Merhaba SQL Server kullanılabilirlik grubu dinleyicisini (değil toobe hello ile Azure kullanılabilirlik kümesi kafası) dağıtma geçici bazı özel durumlar vardır Azure bu anda izin vermiyorsa bu yana toosimply mümkün olduğu gibi bir AD/DNS nesne oluşturma Şirket içi. Bu nedenle, bazı farklı yükleme gerekli tooovercome hello Azure belirli bir davranışı adımlardır.

Bir kullanılabilirlik grubu dinleyicisi kullanarak bazı noktalar şunlardır:

* Bir kullanılabilirlik grubu dinleyicisi kullanarak yalnızca hello VM, işletim sistemi konuk olarak Windows Server 2012 veya Windows Server 2012 R2 ile mümkün değildir. Windows Server 2012 için bu düzeltme eki uygulandığından emin toomake gerekir: <https://support.microsoft.com/kb/2854082>
* Windows Server 2008 R2 bu düzeltme eki yok ve AlwaysOn gereksinim toobe hello aynı kullanılan bir yük devretme ortağı hello bağlantı dizesinde belirterek şekilde veritabanı yansıtma (aracılığıyla SAP default.pfl parametresi dbs/mss/sunucu hello – SAP nota bakın [965908]).
* Bir kullanılabilirlik grubu dinleyicisi, hello veritabanı VM'ler kullanarak gerektiğinde bağlı toobe tooa yük dengeleyici ayrılmış. Ad çözümlemesi yalnızca bulut dağıtımlarında da duyar tüm sanal makineleri bir SAP sisteminin (uygulama sunucuları, DBMS sunucusu ve (A) SCS sunucusu) olan hello aynı sanal ağ veya bir SAP uygulama katmanı hello bakım hello etc\host dosyasının gerektirir Sipariş tooget hello VM adları hello SQL Server Vm'lerinin çözümlendi. Azure her iki VM arada kapatma olduğu durumlarda yeni IP adresleri atama, sipariş tooavoid içinde bir statik IP adresleri (statik IP adresi açıklanan tanımlama hello AlwaysOn yapılandırmasında bu VM'lerin toohello ağ arabirimleri atamanız gerekir [bu] [ virtual-networks-reserved-private-ip] makale)

[comment]: <> (Eski blogları)
[comment]: <> (< https://blogs.msdn.com/b/alwaysonpro/archive/2014/08/29/recommendations-and-best-practices-when-deploying-sql-server-alwayson-availability-groups-in-windows-azure-iaas.aspx>, < https://blogs.technet.com/b/rmilne/archive/2015/07/27/how-to-set-static-ip-on-azure-vm.aspx>)
* Merhaba WSFC küme yapılandırma burada hello küme gereken özel bir IP adresi atandığında, Azure geçerli işlevselliği ile Merhaba küme adı atamanız gerekir çünkü gerekli özel adımlar vardır hello hello düğümü hello küme aynı IP adresi oluşturulur. Bu, el ile adım gerçekleştirilen tooassign farklı bir IP adresi toohello kümeye olması gerektiği anlamına gelir.
* Merhaba kullanılabilirlik grubu dinleyicisi Azure'da hello birincil ve ikincil çoğaltmaları hello kullanılabilirlik grubunun çalışan toohello VM'ye atanan TCP/IP'yi uç ile oluşturulan toobe geçiyor.
* Bu uç noktalar ACL ile gerek toosecure olabilir.

[comment]: <> (Yapılacaklar eski blogu)
[comment]: <> (ayrıntılı adımlar hello ve Azure üzerinde bir AlwaysOn yapılandırmasını yükleme necessities en iyi şekilde hello öğretici kullanılabilir [here][virtual-machines-windows-classic-ps-sql-alwayson-availability-groups] taramasını yaşadığı)
[comment]: <> (AlwaysOn kurulumuna hello Azure galerisinde üzerinden önceden yapılandırılmış < https://blogs.technet.com/b/dataplatforminsider/archive/2014/08/25/sql-server-alwayson-offering-in-microsoft-azure-portal-gallery.aspx>)
[comment]: <> (Bir kullanılabilirlik grubu dinleyicisi oluşturma [this][virtual-machines-windows-classic-ps-sql-int-listener] öğreticide en iyi açıklanan)
[comment]: <> (Güvenliğini sağlama ağ uç nokta ACL'leri ile en iyi burada açıklanmıştır:)
[comment]: <> (* < https://michaelwasham.com/windows-azure-powershell-reference-guide/network-access-control-list-capability-in-windows-azure-powershell/>)
[comment]: <> (* < https://blogs.technet.com/b/heyscriptingguy/archive/2013/08/31/weekend-scripter-creating-acls-for-windows-azure-endpoints-part-1-of-2.aspx>)
[comment]: <> (* < https://blogs.technet.com/b/heyscriptingguy/archive/2013/09/01/weekend-scripter-creating-acls-for-windows-azure-endpoints-part-2-of-2.aspx>)  
[comment]: <> (* < https://blogs.technet.com/b/heyscriptingguy/archive/2013/09/18/creating-acls-for-windows-azure-endpoints.aspx>)

Bu, farklı Azure bölgeleri de olası toodeploy bir SQL Server AlwaysOn Kullanılabilirlik grubu gösterir. Bu işlev hello Azure VNet-Vnet bağlantısı özelliğinden yararlanır ([daha fazla ayrıntı][virtual-networks-configure-vnet-to-vnet-connection]).

[comment]: <> (Yapılacaklar eski blogu)
[comment]: <> (Böyle bir senaryoda Hello kurulum SQL Server AlwaysOn Kullanılabilirlik grupları burada açıklanan: < https://blogs.technet.com/b/dataplatforminsider/archive/2014/06/19/sql-server-alwayson-availability-groups-supported-between-microsoft-azure-regions.aspx>.)

#### <a name="summary-on-sql-server-high-availability-in-azure"></a>SQL Server yüksek kullanılabilirlik Azure özeti
Azure Storage hello içeriği koruduğu hello olgu verildiğinde, yoktur daha az bir nedenle tooinsist etkin bekleme görüntüde. Bu, yüksek kullanılabilirlik senaryonuzun gereken tooonly anlamına gelir durumlarda aşağıdaki hello karşı koruma:

* Merhaba VM kullanılamazlık son toomaintenance azure'da hello sunucu kümesinde veya başka bir nedenle bir bütün olarak
* Yazılım sorunları hello SQL Server örneği
* Burada verileri silinir ve zaman içinde nokta kurtarma gerekli el ile hatadan koruma

Günlük aktarma tarafından hello üçüncü durumda yalnızca kapsamında olabilir ancak bir veritabanı yansıtma veya AlwaysOn, hello ilk iki durumlarda konulabilecek karşıdır eşleşen teknolojileri bakarak.

Toobalance gerekir AlwaysOn, karşılaştırılan tooDatabase daha karmaşık kurulum Merhaba, AlwaysOn ile Merhaba avantajları yansıtma. Bu avantajlar gibi listelenir:

* Okunabilir ikincil kopya.
* İkincil çoğaltmaları yedeklemelerden.
* Daha iyi ölçeklenebilirlik.
* Daha çok bir ikincil çoğaltma.

### <a name="9053f720-6f3b-4483-904d-15dc54141e30"></a>SAP Azure özeti için genel SQL Server
Bu kılavuzdaki birçok önerileri vardır ve bu birden çok kez Azure dağıtımınızı planlama önce okumanız önerilir. Genel olarak, yine de emin toofollow hello Azure belirli noktalarında üst on genel DBMS olabilir:

[comment]: <> (2.3 daha yüksek verimlilik miktardan? Bir VHD?)
1. Merhaba son DBMS sürüm, çoğu avantajları Azure'da hello olan SQL Server 2014 gibi kullanın. SQL Server için SQL Server 2012 SP1 CU4 hangi Azure Storage sunmayı yedekleme hello özelliğini içerir budur. Ancak, SAP birlikte en az öneririz SQL Server 2014 SP1 CU1 veya SQL Server 2012 SP2 ve hello son CU.
2. SAP sistem yatay Azure toobalance hello veri dosya düzeni ve Azure kısıtlamaları dikkatle planlayın:
   * Çok fazla VHD'ler yoktur, ancak gerekli IOPS ulaşabilir yeterli tooensure sahip.
   * IOPS de Azure depolama hesabı sınırlı olduğunu ve depolama hesapları her Azure aboneliği sınırlı olduğunu unutmayın ([daha fazla ayrıntı][azure-subscription-service-limits]).
   * Yalnızca stripe tooachieve daha yüksek işleme gerekiyorsa VHD'ler arasında.
3. Kalıcı olmayan ve bu sürücüde herhangi bir şey Windows yeniden başlatma sırasında kaybolur gibi hello D:\ sürücüsüne üzerinde Kalıcılık gerektiren herhangi bir dosya put veya hiçbir zaman yazılımını yükleyin.
4. Azure VHD için Azure Standard Storage önbelleğe alma kullanmayın.
5. Coğrafi olarak çoğaltılmış Azure depolama hesapları kullanmayın.  Yerel olarak yedekli DBMS iş yükleri için kullanın.
6. DBMS satıcınızın HA/DR çözüm tooreplicate veritabanı verileri kullanın.
7. Her zaman ad çözümlemesi kullanın, IP adreslerini güvenmeyin.
8. Merhaba yüksek veritabanı sıkıştırma olası kullanın. SQL Server için sayfa sıkıştırma budur.
9. SQL Server hello Azure Marketi görüntülerden kullanırken dikkatli olun. Hello SQL Server birini kullanıyorsanız, herhangi bir SAP NetWeaver sistemini yüklemeden önce hello örneği harmanlaması değiştirmeniz gerekir.
10. Yükleme ve açıklandığı gibi hello Azure için SAP izleme ana bilgisayarı yapılandırma [Dağıtım Kılavuzu'na][deployment-guide].

## <a name="specifics-toosap-ase-on-windows"></a>Özellikleri tooSAP Windows ana
Microsoft Azure ile başlayarak, var olan, SAP ana uygulamaları tooAzure sanal makineleri kolayca geçirebilirsiniz. SAP ana bir sanal makinede, bu uygulamaları tooMicrosoft Azure kolayca geçiş yaparak, tooreduce hello toplam sahip olma maliyetini dağıtım, yönetim ve Bakım Kurumsal avantajlarına uygulama sağlar. SAP ana bir Azure sanal makine ile yöneticiler ve geliştiriciler kullanılabilir aynı geliştirme ve Yönetim Araçları şirket içi hello kullanmaya devam edebilirsiniz.

Merhaba, burada bulunan Azure sanal makineler için bir SLA yoktur: <https://azure.microsoft.com/support/legal/sla>

Microsoft Azure barındırılan sanal makinelerin çok iyi karşılaştırma tooother genel bulut sanallaştırma teklifleri, ancak tek tek sonuç gerçekleştirecek değişebilir emin duyuyoruz. SAP sayıda farklı SAP sertifikalı VM SKU'ları ayrı SAP Not içinde sağlanacaktır hello boyutlandırma SAP [1928533].

İfadeler ve Azure Storage, SAP dağıtım VM'ler veya SAP izleme şekilde toohello kullanımı önerilerine SAP ana toodeployments hello, bu belgenin ilk dört bölüm belirtildiği gibi SAP uygulamaları ile birlikte uygulanır.

### <a name="sap-ase-version-support"></a>SAP ana sürüm desteği
Şu anda destekler SAP ana sürüm 16,0 SAP Business Suite ürünlerle kullanmak üzere SAP. SAP ana sunucu veya SAP Business ürünleri yalnızca aracılığıyla sağlanan Suite ile kullanılan JDBC ve ODBC sürücüleri toobe için tüm güncelleştirmeleri hello SAP hizmet Market'ten: <https://support.sap.com/swdc>.

Yüklemeleri şirket için olduğu gibi hello SAP ana sunucu için veya hello JDBC ve ODBC sürücüleri için güncelleştirmeleri doğrudan Sybase sitelerinden yüklemeyin. Düzeltme ekleri hakkında ayrıntılı bilgi için SAP Business Suite ürünleri şirket içi ile kullanım için desteklenir ve SAP notları aşağıdaki hello Azure sanal makinelerinde bakın:

* [1590719]
* [1973241]

SAP Business Suite SAP ana üzerinde çalıştırma hakkında genel bilgi hello bulunabilir [SCN](https://scn.sap.com/community/ase)

### <a name="sap-ase-configuration-guidelines-for-sap-related-sap-ase-installations-in-azure-vms"></a>SAP için SAP ana yapılandırma yönergeleri SAP ana Azure VM'ler yüklemelerde ilgili
#### <a name="structure-of-hello-sap-ase-deployment"></a>Merhaba SAP ana dağıtım yapısı
Merhaba Genel Açıklama uygun olarak SAP ana yürütülebilir dosyalar bulunabilir veya hello sistem sürücüsüne hello VM'ın temel VHD yüklü (c: sürücüsü\). Genellikle, çoğu hello SAP ana sistem ve araçları veritabanlarının gerçekten sabit SAP NetWeaver iş yükü tarafından yararlanılabilir değil. Bu nedenle sistem hello ve araçları veritabanları (master, model, saptools, sybmgmtdb, sybsystemdb) de hello C:\drive üzerinde kalabilir.

İstisna tüm iş tabloları ve daha yüksek veri birimi veya hello özgün sığamıyorsa g/ç işlemleri birimi gerektirebilir, bazı SAP ERP ve tüm BW iş yükleri durumunda SAP ana tarafından oluşturulan geçici tabloları içeren hello geçici veritabanı olabilir VM'ın temel VHD (c: sürücüsü\).

Merhaba bağlı olarak kullanılan SAPInst/SWPM sürümü tooinstall hello sistem, hello veritabanı içerebilir:

* SAP ana yüklerken oluşturulan tek bir SAP ana tempdb
* SAP ana ve SAP yükleme yordamını hello tarafından oluşturulan bir ek saptempdb yükleyerek oluşturulan bir SAP ana tempdb
* SAP ana ve el ile oluşturulan bir ek tempdb yükleyerek oluşturulan bir SAP ana tempdb (örn. SAP Not aşağıdaki [1752266]) toomeet ERP/BW belirli tempdb gereksinimleri

Belirli ERP veya tüm BW iş yükleri durumunda, hesaba tooperformance içinde tookeep hello tempdb aygıtları C:\ dışında bir sürücüde ayrıca oluşturulan hello tempdb (SWPM veya el ile) mantıklıdır. Hiçbir ek tempdb varsa toocreate bir önerilir (SAP Not [1752266]).

Bu tür sistemleri hello için aşağıdaki adımları ayrıca tempdb oluşturulan Merhaba gerçekleştirilmelidir:

* Merhaba ilk tempdb aygıt toohello ilk aygıt hello SAP veritabanının taşıma
* Merhaba hello SAP veritabanının aygıtları içeren VHD, tempdb aygıtları tooeach Ekle

Bu yapılandırma etkinleştirir tempdb tooeither hello sistem sürücüsünün tooprovide mümkün olandan daha fazla alanı kullanabilir. Bir başvuru olarak bir şirket içi varolan sistemlerde hello tempdb aygıt boyutları kontrol edebilirsiniz. Veya bu tür bir yapılandırma IOPS numaraları hello sistem sürücüsü ile sağlanan tempdb karşı olanak sağlar. Yeniden şirket içi çalışan sistemlerde kullanılan toomonitor g/ç iş yükü tempdb karşı olabilir.

Hiçbir zaman herhangi bir SAP ana aygıtı hello hello VM D:\ sürücüsüne yerleştirin. Merhaba tempdb tutulan hello nesneleri yalnızca geçici olsa bile, bu da toohello tempdb geçerlidir.

#### <a name="impact-of-database-compression"></a>Veritabanı Sıkıştırma etkisi
Burada g/ç bant genişliği sınırlayıcı bir etmen haline gelebilir yapılandırmalarında IOPS azaltır her ölçü bir Azure gibi bir Iaas senaryosu çalıştırabilirsiniz toostretch hello iş yükü yardımcı olabilir. Bu nedenle, varolan bir SAP veritabanı tooAzure karşıya yüklemeden önce SAP ana sıkıştırma kullandığınız emin toomake önemle tavsiye edilir.

zaten uygulanmadı varsa tooAzure karşıya yüklemeden önce hello öneri tooperform sıkıştırma dışında çeşitli nedenleri verilmiştir:

* verileri karşıya toobe tooAzure Hello miktarını düşük olduğu
* g/ç gecikmesi şirket içi daha az veya daha fazla CPU veya daha yüksek g/ç bant genişliği ile daha güçlü donanım kullanabilirsiniz varsayılarak hello hello sıkıştırma yürütme süresini kısadır
* Daha küçük veritabanı boyutları disk ayırmayı tooless maliyetlerini neden olabilir

Veri ve LOB sıkıştırma şirket içi yaptığı gibi Azure sanal makinelerinde barındırılan bir VM'nin çalışır. Sıkıştırma zaten varsa toocheck varolan SAP ASE'de kullanma hakkında daha fazla ayrıntı için veritabanı danışın SAP Not [1750510].

#### <a name="using-dbacockpit-toomonitor-database-instances"></a>DBACockpit toomonitor veritabanı örnekleri kullanma
SAP ana veritabanı platform olarak kullanan SAP sistemleri için hello DBACockpit işlem DBACockpit katıştırılmış tarayıcı pencerelerini veya Webdynpro olarak erişilebilir. Ancak izleme için tam işlevsellik hello ve hello Webdynpro uygulamasında hello DBACockpit yalnızca yönetme hello veritabanı kullanılamıyor.

Olarak ile şirket içi çeşitli adımlar sistemleri hello Webdynpro uyarlamasını hello DBACockpit tarafından kullanılan tüm SAP NetWeaver işlevselliği tooenable gereklidir. Lütfen SAP Not izleyin [1245200] tooenable hello webdynpros kullanımını ve oluşturmak hello olanları gerekli. Ne zaman hello Internet iletişimi Yöneticisi'ni (ICM) ile birlikte yapılandıracağınız notları yukarıda hello aşağıdaki hello yönergelerinde http ve https bağlantıları için kullanılan bağlantı noktaları toobe hello. Merhaba varsayılan ayarı http için şöyle görünür:

> ICM/server_port_0 KOR = HTTP bağlantı noktası = 8000, PROCTIMEOUT = 600, zaman AŞIMI = 600 =
>
> ICM/server_port_1 KOR = = HTTPS, bağlantı noktası 443$, PROCTIMEOUT = 600, zaman AŞIMI = 600 =
>
>

ve işlem DBACockpit üretilen hello bağlantılar benzer toothis arar:

> https://`<fullyqualifiedhostname`>: sap/44300/bc/sap/webdynpro/dba_cockpit
>
> http://`<fullyqualifiedhostname`>: sap/8000/bc/sap/webdynpro/dba_cockpit
>
>

Bağlı olarak varsa ve site siteye, hello Azure sanal makine barındırma hello SAP sistemine bağlı nasıl çok siteli veya ExpressRoute toomake emin gerekir (şirket içi dağıtım), ICM çözülebilir tam bir ana bilgisayar üzerinde hello kullanıyor makine, tooopen çalıştığınız DBACockpit gelen hello. Lütfen SAP nota bakın [773830] gerekirse ICM nasıl belirlediğini toounderstand profili parametreleri ve kümesi parametre ICM/host_name_full bağlı olarak tam ana bilgisayar adı açıkça hello..

Şirket içi bağlantılar şirket içi ve Azure arasında olmadan yalnızca bulut senaryosunda hello VM dağıtılmışsa, bir ortak IP adresi ve bir domainlabel toodefine gerekir. Merhaba Genel DNS adını hello VM Hello biçimi ardından şuna benzeyecektir:

> `<custom domainlabel`>. `<azure region`>. cloudapp.azure.com
>
>

Daha fazla ayrıntı toohello DNS adı bulunabilir ilgili [burada][virtual-machines-azurerm-versus-azuresm].

DNS adı'hello Azure VM hello bağlantısının benzer şekilde görünebilir hello SAP profili parametre ICM/host_name_full toohello ayar:

> sap/https://mydomainlabel.westeurope.cloudapp.NET:44300/bc/sap/webdynpro/dba_cockpit
>
> sap/http://mydomainlabel.westeurope.cloudapp.NET:8000/bc/sap/webdynpro/dba_cockpit
>
>

Bu durumda, toomake emin gerekir:

* Hello Azure Portal hello TCP/IP bağlantı noktaları, gelen kuralları toohello ağ güvenlik grubu ile ICM toocommunicate kullanılan ekleme
* Gelen kuralları toohello Windows Güvenlik Duvarı yapılandırmasını hello TCP/IP'yi kullanılan bağlantı noktaları toocommunicate hello ICM ile ekleme

Kullanılabilir tüm düzeltmeler otomatik bir alma işlemi için önerilen tooperiodically hello düzeltme koleksiyonu SAP Not geçerli tooyour SAP sürüm Uygula:

* [1558958]
* [1619967]
* [1882376]

SAP notları aşağıdaki hello SAP ana DBA Pilot hakkında daha fazla bilgi bulunabilir:

* [1605680]
* [1757924]
* [1757928]
* [1758182]
* [1758496]    
* [1814258]
* [1922555]
* [1956005]

#### <a name="backuprecovery-considerations-for-sap-ase"></a>SAP ana yedekleme/kurtarma değerlendirmeleri
SAP ana Azure'a dağıtırken yedekleme yönteminize gözden geçirilmesi gerekir. Merhaba sistem üretken sistem olsa bile, SAP ana tarafından barındırılan hello SAP veritabanında düzenli aralıklarla yedeklenmelidir. Azure Storage üç görüntüleri tutar, bir yedekleme şimdi saygı toocompensating depolama çökmeyle daha az önemlidir. Merhaba uygun bir yedekleme ve geri yükleme planı korumak için birincil zaman kurtarma özellikleri noktasında sağlayarak mantıksal/el ile hataları dengeleyebilirsiniz daha fazla nedenidir. Merhaba hedef tooeither kullanım yedeklemeleri toorestore hello veritabanı yedeklemesi olacak şekilde tooa belirli noktası Azure tooseed zaman ya da toouse hello yedeklere içinde başka bir sistem hello varolan veritabanı kopyalayarak. Örneğin, bir katman 2 SAP yapılandırma tooa 3 katmanlı sistem kurulumundan hello aynı aktaramıyor bir yedeğini geri tarafından sistem.

Şekilde şirket içi yaptığı gibi yedekleme ve geri yükleme Azure works veritabanında aynı hello. SAP notlara bakın:

* [1588316]
* [1585981]

Döküm yapılandırmaları oluşturma ve zamanlama yedeklemeler daha fazla ayrıntı için. Strateji ve yapılandırabileceğiniz gereksinimlerine bağlı olarak veritabanı ve günlük VHD'ler varolan hello birini üzerine toodisk dökümleri veya hello yedekleme için ek bir VHD'yi ekleyin.  Bu bir hata durumunda veri kaybı tooreduce hello tehlike hiçbir veritabanı aygıtı bulunduğu bir VHD toouse önerilir.

Veri ve LOB yanı sıra sıkıştırma SAP ana yedekleme sıkıştırma da sağlar. daha az yer hello veritabanı ve günlük ile toooccupy dökümleri toouse yedekleme sıkıştırma önerilir. Lütfen SAP nota bakın [1588316] daha fazla bilgi için. Sıkıştırma hello yedekleme de önemli tooreduce hello toodownload yedekleri ya da hello Azure sanal makine tooon içi gelen yedekleme dökümleri içeren VHD düşünüyorsanız, aktarılan verileri toobe miktarıdır.

Sürücü D:\ döküm hedef veritabanı veya günlük olarak kullanmayın.

#### <a name="performance-considerations-for-backupsrestores"></a>Yedekleme/geri yüklemeler için başarım düşünceleri
Çıplak dağıtımlar olduğu gibi yedekleme/geri yükleme performans paralel şekilde kaç tane birimleri okunabilir ve hangi hello verimlilik bu birimlerin olabilir bağlıdır. Ayrıca, hello yedekleme sıkıştırma tarafından kullanılan CPU tüketimi yalnızca too8 CPU iş parçacıklarını ile sanal makineleri üzerinde önemli bir rol oynayabilir. Bu nedenle, bir kabul edebilirsiniz:

* Merhaba VHD'ler daha az hello sayısı toostore hello veritabanı cihazlar, hello kullanılan küçük, genel üretilen işi okuma hello
* Merhaba VM CPU iş parçacıkları daha küçük hello sayısı Merhaba, yedekleme sıkıştırma daha ciddi hello etkisini hello
* daha az hedefleri (Stripe dizinleri, VHD) toowrite hello yedekleme Merhaba, daha az hello verimlilik hello

hedefleri toowrite toothere tooincrease hello sayısı gereksinimlerinize bağlı olarak kullanılan/birleştirilmiş olabilen iki seçenek vardır:

* Şeritli birim üzerinde sipariş tooimprove hello IOPS üretilen işi içinde birden fazla bağlı Vhd'lere üzerinden Hello yedekleme hedef birim bölümlemesine
* Birden fazla hedef dizin toowrite hello dökümünü almak için kullandığı SAP ana düzeyde döküm yapılandırması oluşturma

Bir birim üzerinde birden fazla bağlı Vhd'lere bölümlemesine bu kılavuzun önceki bölümlerinde açıklanan. Kullanma hakkında daha fazla bilgi için birden fazla dizine hello SAP ana döküm yapılandırmasında kullanılan toocreate hello döküm hello yapılandırmasına olan saklı yordam sp_config_dump toohello belgelerine başvurun [Sybase Bilgi Merkezi](http://infocenter.sybase.com/help/index.jsp).

### <a name="disaster-recovery-with-azure-vms"></a>Azure VM'ler ile olağanüstü durum kurtarma
#### <a name="data-replication-with-sap-sybase-replication-server"></a>SAP Sybase çoğaltma sunucusu ile veri çoğaltma
Merhaba ile SAP Sybase çoğaltma sunucusuna (SRS) SAP ana sıcak bekleme çözümü tootransfer veritabanı işlemleri tooa uzak konumlara zaman uyumsuz olarak sağlar.

Merhaba yükleme ve works'ün SRS de işlevsel olarak şirket içi yaptığı gibi Azure sanal makine Hizmetleri'nde barındırılan bir VM'de işlemi.

SAP çoğaltma sunucusu aracılığıyla ana HADR sonraki bir sürümüyle planlanmaktadır. İle test edilebilir ve kullanılabilir olduğunda hemen Microsoft Azure platform için yayımlanan.

## <a name="specifics-toosap-ase-on-linux"></a>Linux üzerinde özellikleri tooSAP ana
Microsoft Azure ile başlayarak, var olan, SAP ana uygulamaları tooAzure sanal makineleri kolayca geçirebilirsiniz. SAP ana bir sanal makinede, bu uygulamaları tooMicrosoft Azure kolayca geçiş yaparak, tooreduce hello toplam sahip olma maliyetini dağıtım, yönetim ve Bakım Kurumsal avantajlarına uygulama sağlar. SAP ana bir Azure sanal makine ile yöneticiler ve geliştiriciler kullanılabilir aynı geliştirme ve Yönetim Araçları şirket içi hello kullanmaya devam edebilirsiniz.

Azure VM'ler, önemli tooknow hello burada bulunan resmi SLA dağıtmak için: <https://azure.microsoft.com/support/legal/sla>

SAP boyutlandırma bilgileri ve SAP VM SKU'ları sertifikalı listesini, SAP notta sağlanacaktır [1928533]. Azure sanal makineleri burada bulunabilir belgeleri boyutlandırma ek SAP <http://blogs.msdn.com/b/saponsqlserver/archive/2015/06/19/how-to-size-sap-systems-running-on-azure-vms.aspx> ve burada <http://blogs.msdn.com/b/saponsqlserver/archive/2015/12/01/new-white-paper-on-sizing-sap-solutions-on-azure-public-cloud.aspx>

İfadeler ve Azure Storage, SAP dağıtım VM'ler veya SAP izleme şekilde toohello kullanımı önerilerine SAP ana toodeployments hello, bu belgenin ilk dört bölüm belirtildiği gibi SAP uygulamaları ile birlikte uygulanır.

Merhaba aşağıdaki iki SAP notları Linux ve ana ana hakkında genel bilgi hello bulut şunları içerir:

* [2134316]
* [1941500]

### <a name="sap-ase-version-support"></a>SAP ana sürüm desteği
Şu anda destekler SAP ana sürüm 16,0 SAP Business Suite ürünlerle kullanmak üzere SAP. SAP ana sunucu veya SAP Business ürünleri yalnızca aracılığıyla sağlanan Suite ile kullanılan JDBC ve ODBC sürücüleri toobe için tüm güncelleştirmeleri hello SAP hizmet Market'ten: <https://support.sap.com/swdc>.

Yüklemeleri şirket için olduğu gibi hello SAP ana sunucu için veya hello JDBC ve ODBC sürücüleri için güncelleştirmeleri doğrudan Sybase sitelerinden yüklemeyin. Düzeltme ekleri hakkında ayrıntılı bilgi için SAP Business Suite ürünleri şirket içi ile kullanım için desteklenir ve SAP notları aşağıdaki hello Azure sanal makinelerinde bakın:

* [1590719]
* [1973241]

SAP Business Suite SAP ana üzerinde çalıştırma hakkında genel bilgi hello bulunabilir [SCN](https://scn.sap.com/community/ase)

### <a name="sap-ase-configuration-guidelines-for-sap-related-sap-ase-installations-in-azure-vms"></a>SAP için SAP ana yapılandırma yönergeleri SAP ana Azure VM'ler yüklemelerde ilgili
#### <a name="structure-of-hello-sap-ase-deployment"></a>Merhaba SAP ana dağıtım yapısı
Merhaba Genel Açıklama uygun olarak SAP ana yürütülebilir dosyalar bulunabilir veya hello kök dosya sistemi hello VM (/sybase) içine yüklü. Genellikle, çoğu hello SAP ana sistem ve araçları veritabanlarının gerçekten sabit SAP NetWeaver iş yükü tarafından yararlanılabilir değil. Bu nedenle sistem hello ve araçları veritabanları (master, model, saptools, sybmgmtdb, sybsystemdb) hello kök dosya sisteminde de kalabilir.

İstisna tüm iş tabloları ve daha yüksek veri birimi veya hello özgün sığamıyorsa g/ç işlemleri birimi gerektirebilir, bazı SAP ERP ve tüm BW iş yükleri durumunda SAP ana tarafından oluşturulan geçici tabloları içeren hello geçici veritabanı olabilir Sanal makinenin işletim sistemi diski.

Merhaba bağlı olarak kullanılan SAPInst/SWPM sürümü tooinstall hello sistem, hello veritabanı içerebilir:

* SAP ana yüklerken oluşturulan tek bir SAP ana tempdb
* SAP ana ve SAP yükleme yordamını hello tarafından oluşturulan bir ek saptempdb yükleyerek oluşturulan bir SAP ana tempdb
* SAP ana ve el ile oluşturulan bir ek tempdb yükleyerek oluşturulan bir SAP ana tempdb (örn. SAP Not aşağıdaki [1752266]) toomeet ERP/BW belirli tempdb gereksinimleri

Belirli ERP veya tüm BW iş yükleri durumunda anlamlı tookeep hello tempdb aygıtları tek bir Azure veri diski ya da Linux RAID tarafından temsil edilebilir bir ayrı bir dosya sistemine ayrıca oluşturulan hello tempdb (SWPM veya el ile) şekilde tooperformance içinde yapar. birden çok Azure veri diski kapsayıcı. Hiçbir ek tempdb varsa toocreate bir önerilir (SAP Not [1752266]).

Bu tür sistemleri hello için aşağıdaki adımları ayrıca tempdb oluşturulan Merhaba gerçekleştirilmelidir:

* Merhaba ilk tempdb dizini toohello ilk dosya sistemi hello SAP veritabanını taşıma
* Merhaba hello SAP veritabanının filesystem içeren VHD, tempdb dizinleri tooeach Ekle

Bu yapılandırma etkinleştirir tempdb tooeither hello sistem sürücüsünün tooprovide mümkün olandan daha fazla alanı kullanabilir. Bir başvuru olarak bir şirket içi varolan sistemlerde hello tempdb dizini boyutları kontrol edebilirsiniz. Veya bu tür bir yapılandırma IOPS numaraları hello sistem sürücüsü ile sağlanan tempdb karşı olanak sağlar. Yeniden şirket içi çalışan sistemlerde kullanılan toomonitor g/ç iş yükü tempdb karşı olabilir.

Hiçbir zaman herhangi bir SAP ana dizin /mnt veya hello VM /mnt/resource üzerine yerleştirin. Kalıcı olmayan bir varsayılan Azure VM geçici alanı /mnt veya /mnt/resource olduğundan hello tempdb tutulan hello nesneleri yalnızca geçici olsa bile, bu da toohello tempdb geçerlidir. Hello Azure VM geçici alanı hakkında daha fazla ayrıntı bulunabilir [bu makalede][virtual-machines-linux-how-to-attach-disk]

#### <a name="impact-of-database-compression"></a>Veritabanı Sıkıştırma etkisi
Burada g/ç bant genişliği sınırlayıcı bir etmen haline gelebilir yapılandırmalarında IOPS azaltır her ölçü bir Azure gibi bir Iaas senaryosu çalıştırabilirsiniz toostretch hello iş yükü yardımcı olabilir. Bu nedenle, varolan bir SAP veritabanı tooAzure karşıya yüklemeden önce SAP ana sıkıştırma kullandığınız emin toomake önemle tavsiye edilir.

zaten uygulanmadı varsa tooAzure karşıya yüklemeden önce hello öneri tooperform sıkıştırma dışında çeşitli nedenleri verilmiştir:

* verileri karşıya toobe tooAzure Hello miktarını düşük olduğu
* g/ç gecikmesi şirket içi daha az veya daha fazla CPU veya daha yüksek g/ç bant genişliği ile daha güçlü donanım kullanabilirsiniz varsayılarak hello hello sıkıştırma yürütme süresini kısadır
* Daha küçük veritabanı boyutları disk ayırmayı tooless maliyetlerini neden olabilir

Veri ve LOB sıkıştırma şirket içi yaptığı gibi Azure sanal makinelerinde barındırılan bir VM'nin çalışır. Sıkıştırma zaten varsa toocheck varolan SAP ASE'de kullanma hakkında daha fazla ayrıntı için veritabanı danışın SAP Not [1750510]. Ayrıca bkz. SAP Not [2121797] veritabanı sıkıştırma ilgili ek bilgi.

#### <a name="using-dbacockpit-toomonitor-database-instances"></a>DBACockpit toomonitor veritabanı örnekleri kullanma
SAP ana veritabanı platform olarak kullanan SAP sistemleri için hello DBACockpit işlem DBACockpit katıştırılmış tarayıcı pencerelerini veya Webdynpro olarak erişilebilir. Ancak izleme için tam işlevsellik hello ve hello Webdynpro uygulamasında hello DBACockpit yalnızca yönetme hello veritabanı kullanılamıyor.

Olarak ile şirket içi çeşitli adımlar sistemleri hello Webdynpro uyarlamasını hello DBACockpit tarafından kullanılan tüm SAP NetWeaver işlevselliği tooenable gereklidir. Lütfen SAP Not izleyin [1245200] tooenable hello webdynpros kullanımını ve oluşturmak hello olanları gerekli. Ne zaman hello Internet iletişimi Yöneticisi'ni (ICM) ile birlikte yapılandıracağınız notları yukarıda hello aşağıdaki hello yönergelerinde http ve https bağlantıları için kullanılan bağlantı noktaları toobe hello. Merhaba varsayılan ayarı http için şöyle görünür:

> ICM/server_port_0 KOR = HTTP bağlantı noktası = 8000, PROCTIMEOUT = 600, zaman AŞIMI = 600 =
>
> ICM/server_port_1 KOR = = HTTPS, bağlantı noktası 443$, PROCTIMEOUT = 600, zaman AŞIMI = 600 =
>
>

ve işlem DBACockpit üretilen hello bağlantılar benzer toothis arar:

> https://`<fullyqualifiedhostname`>: sap/44300/bc/sap/webdynpro/dba_cockpit
>
> http://`<fullyqualifiedhostname`>: sap/8000/bc/sap/webdynpro/dba_cockpit
>
>

Bağlı olarak varsa ve site siteye, hello Azure sanal makine barındırma hello SAP sistemine bağlı nasıl çok siteli veya ExpressRoute toomake emin gerekir (şirket içi dağıtım), ICM çözülebilir tam bir ana bilgisayar üzerinde hello kullanıyor makine, tooopen çalıştığınız DBACockpit gelen hello. Lütfen SAP nota bakın [773830] gerekirse ICM nasıl belirlediğini toounderstand profili parametreleri ve kümesi parametre ICM/host_name_full bağlı olarak tam ana bilgisayar adı açıkça hello..

Şirket içi bağlantılar şirket içi ve Azure arasında olmadan yalnızca bulut senaryosunda hello VM dağıtılmışsa, bir ortak IP adresi ve bir domainlabel toodefine gerekir. Merhaba Genel DNS adını hello VM Hello biçimi ardından şuna benzeyecektir:

> `<custom domainlabel`>. `<azure region`>. cloudapp.azure.com
>
>

Daha fazla ayrıntı toohello DNS adı bulunabilir ilgili [burada][virtual-machines-azurerm-versus-azuresm].

DNS adı'hello Azure VM hello bağlantısının benzer şekilde görünebilir hello SAP profili parametre ICM/host_name_full toohello ayar:

> sap/https://mydomainlabel.westeurope.cloudapp.NET:44300/bc/sap/webdynpro/dba_cockpit
>
> sap/http://mydomainlabel.westeurope.cloudapp.NET:8000/bc/sap/webdynpro/dba_cockpit
>
>

Bu durumda, toomake emin gerekir:

* Hello Azure Portal hello TCP/IP bağlantı noktaları, gelen kuralları toohello ağ güvenlik grubu ile ICM toocommunicate kullanılan ekleme
* Gelen kuralları toohello Windows Güvenlik Duvarı yapılandırmasını hello TCP/IP'yi kullanılan bağlantı noktaları toocommunicate hello ICM ile ekleme

Kullanılabilir tüm düzeltmeler otomatik bir alma işlemi için önerilen tooperiodically hello düzeltme koleksiyonu SAP Not geçerli tooyour SAP sürüm Uygula:

* [1558958]
* [1619967]
* [1882376]

SAP notları aşağıdaki hello SAP ana DBA Pilot hakkında daha fazla bilgi bulunabilir:

* [1605680]
* [1757924]
* [1757928]
* [1758182]
* [1758496]    
* [1814258]
* [1922555]
* [1956005]

#### <a name="backuprecovery-considerations-for-sap-ase"></a>SAP ana yedekleme/kurtarma değerlendirmeleri
SAP ana Azure'a dağıtırken yedekleme yönteminize gözden geçirilmesi gerekir. Merhaba sistem üretken sistem olsa bile, SAP ana tarafından barındırılan hello SAP veritabanında düzenli aralıklarla yedeklenmelidir. Azure Storage üç görüntüleri tutar, bir yedekleme şimdi saygı toocompensating depolama çökmeyle daha az önemlidir. Merhaba uygun bir yedekleme ve geri yükleme planı korumak için birincil zaman kurtarma özellikleri noktasında sağlayarak mantıksal/el ile hataları dengeleyebilirsiniz daha fazla nedenidir. Merhaba hedef tooeither kullanım yedeklemeleri toorestore hello veritabanı yedeklemesi olacak şekilde tooa belirli noktası Azure tooseed zaman ya da toouse hello yedeklere içinde başka bir sistem hello varolan veritabanı kopyalayarak. Örneğin, bir katman 2 SAP yapılandırma tooa 3 katmanlı sistem kurulumundan hello aynı aktaramıyor bir yedeğini geri tarafından sistem.

Şekilde şirket içi yaptığı gibi yedekleme ve geri yükleme Azure works veritabanında aynı hello. SAP notlara bakın:

* [1588316]
* [1585981]

Döküm yapılandırmaları oluşturma ve zamanlama yedeklemeler daha fazla ayrıntı için. Strateji ve yapılandırabileceğiniz gereksinimlerine bağlı olarak veritabanı ve günlük VHD'ler varolan hello birini üzerine toodisk dökümleri veya hello yedekleme için ek bir VHD'yi ekleyin.  Bu bir hata durumunda veri kaybı tooreduce hello tehlike hiçbir veritabanı dizin/dosya bulunduğu bir VHD toouse önerilir.

Veri ve LOB yanı sıra sıkıştırma SAP ana yedekleme sıkıştırma da sağlar. daha az yer hello veritabanı ve günlük ile toooccupy dökümleri toouse yedekleme sıkıştırma önerilir. Lütfen SAP nota bakın [1588316] daha fazla bilgi için. Sıkıştırma hello yedekleme de önemli tooreduce hello toodownload yedekleri ya da hello Azure sanal makine tooon içi gelen yedekleme dökümleri içeren VHD düşünüyorsanız, aktarılan verileri toobe miktarıdır.

Hello Azure VM geçici alanı /mnt veya /mnt/resource döküm hedef veritabanı veya günlük olarak kullanmayın.

#### <a name="performance-considerations-for-backupsrestores"></a>Yedekleme/geri yüklemeler için başarım düşünceleri
Çıplak dağıtımlar olduğu gibi yedekleme/geri yükleme performans paralel şekilde kaç tane birimleri okunabilir ve hangi hello verimlilik bu birimlerin olabilir bağlıdır. Ayrıca, hello yedekleme sıkıştırma tarafından kullanılan CPU tüketimi yalnızca too8 CPU iş parçacıklarını ile sanal makineleri üzerinde önemli bir rol oynayabilir. Bu nedenle, bir kabul edebilirsiniz:

* Merhaba VHD'ler daha az hello sayısı toostore hello veritabanı cihazlar, hello kullanılan küçük, genel üretilen işi okuma hello
* Merhaba VM CPU iş parçacıkları daha küçük hello sayısı Merhaba, yedekleme sıkıştırma daha ciddi hello etkisini hello
* Merhaba daha az hedefleri (Linux yazılım RAID VHD'ler) toowrite yedekleme Merhaba, daha az hello verimlilik hello

hedefleri toowrite toothere tooincrease hello sayısı gereksinimlerinize bağlı olarak kullanılan/birleştirilmiş olabilen iki seçenek vardır:

* Şeritli birim üzerinde sipariş tooimprove hello IOPS üretilen işi içinde birden fazla bağlı Vhd'lere üzerinden Hello yedekleme hedef birim bölümlemesine
* Birden fazla hedef dizin toowrite hello dökümünü almak için kullandığı SAP ana düzeyde döküm yapılandırması oluşturma

Bir birim üzerinde birden fazla bağlı Vhd'lere bölümlemesine bu kılavuzun önceki bölümlerinde açıklanan. Kullanma hakkında daha fazla bilgi için birden fazla dizine hello SAP ana döküm yapılandırmasında kullanılan toocreate hello döküm hello yapılandırmasına olan saklı yordam sp_config_dump toohello belgelerine başvurun [Sybase Bilgi Merkezi](http://infocenter.sybase.com/help/index.jsp).

### <a name="disaster-recovery-with-azure-vms"></a>Azure VM'ler ile olağanüstü durum kurtarma
#### <a name="data-replication-with-sap-sybase-replication-server"></a>SAP Sybase çoğaltma sunucusu ile veri çoğaltma
Merhaba ile SAP Sybase çoğaltma sunucusuna (SRS) SAP ana sıcak bekleme çözümü tootransfer veritabanı işlemleri tooa uzak konumlara zaman uyumsuz olarak sağlar.

Merhaba yükleme ve works'ün SRS de işlevsel olarak şirket içi yaptığı gibi Azure sanal makine Hizmetleri'nde barındırılan bir VM'de işlemi.

SAP çoğaltma sunucusu aracılığıyla ana HADR bu anda desteklenmez. İle test ve gelecekteki hello içinde Microsoft Azure platformu için yayımlanan olabilir.

## <a name="specifics-toooracle-database-on-windows"></a>Özellikleri tooOracle Windows veritabanı
Midyear 2013 itibaren Oracle yazılım Oracle toorun Microsoft Windows Hyper-V ve Azure tarafından desteklenir. Bu makale tooget, Windows Hyper-V ve Azure Oracle tarafından hello genel desteği hakkında daha fazla ayrıntı okuyun: <https://blogs.oracle.com/cloud/entry/oracle_and_microsoft_join_forces>

Genel destek Merhaba, belirli bir senaryoyu hello Oracle veritabanları yararlanarak SAP uygulamalarının de desteklenir. Ayrıntılar hello belgenin bu bölümü adlandırılır.

### <a name="oracle-version-support"></a>Oracle sürüm desteği
Oracle ve SAP Oracle Azure sanal makineler üzerinde çalışan SAP Not aşağıdaki hello bulunabilir, desteklenen karşılık gelen işletim sistemi sürümleri ile ilgili tüm ayrıntıları [2039619]

SAP Business Suite Oracle üzerinde çalıştırma hakkında genel bilgi SCN üzerinde bulunabilir: <https://scn.sap.com/community/oracle>

### <a name="oracle-configuration-guidelines-for-sap-installations-in-azure-vms"></a>SAP yüklemelerde Azure VM'ler için Oracle yapılandırma yönergeleri
#### <a name="storage-configuration"></a>Depolama yapılandırması
Yalnızca tek bir örneği NTFS biçimli diskler kullanarak Oracle desteklenir. Tüm veritabanı dosyaları temel VHD disklerde hello NTFS dosya sistemi depolanması gerekir. Bu VHD takılı toohello Azure VM olan ve Azure sayfa BLOB Depolama birimine dayalı (<https://msdn.microsoft.com/library/azure/ee691964.aspx>).
Her türlü ağ sürücülerine veya Azure dosya services gibi uzak paylaşımları:

* <https://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-Microsoft-Azure-File-Service.aspx>
* <https://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-Connections-to-Microsoft-Azure-Files.aspx>

olan **değil** Oracle veritabanı dosyaları için desteklenen!

Azure Azure sayfa BLOB Depolama birimine dayalı VHD'ler kullanarak, bu belgede bölüm yapılan deyimleri hello [sanal makineleri ve VHD için önbelleğe alma] [ dbms-guide-2.1] ve [Microsoft Azure depolama] [ dbms-guide-2.3] toodeployments hello Oracle veritabanı da ile uygulayın.

Daha önce hello Genel bölümünde hello belgenin açıklandığı gibi Azure VHD'ler için IOPS işleme kotalar mevcut. Merhaba tam kotaları hello VM türüne bağlı olarak kullanılır. Kendi kotaları ile VM türlerinin bir listesini bulunabilir [burada][virtual-machines-sizes]

tooidentify hello desteklenen Azure VM türleri, lütfen tooSAP Not bakın [1928533]

Merhaba geçerli IOPS kota disk başına hello gereksinimleri karşılayan sürece tüm hello DB dosyaları olası toostore olan tek tek Azure VHD bağlanır.

Daha fazla IOPS gerekirse, toouse penceresi depolama havuzları (yalnızca Windows Server 2012'de kullanılabilir ve üzeri) veya Windows 2008 R2 toocreate için büyük bir mantıksal aygıt birden çok bağlama VHD diskleri bölümlemesine Windows kesinlikle önerilir. Ayrıca bkz. bölüm [yazılım RAID] [ dbms-guide-2.2] bu belgenin. Bu yaklaşım hello Yönetim genel gider toomanage hello disk alanı basitleştirir ve hello çaba önler toomanually arasında birden çok bağlı VHD dosyaları dağıtın.

#### <a name="backup--restore"></a>Yedekleme / Geri Yükleme
Yedekleme için / işlevlerin geri yüklenmesi, SAP BR hello * araçları Oracle desteklenen hello aynı şekilde standart Windows Server işletim sistemleri ve üzerinde Hyper-V gibi. Oracle kurtarma Yöneticisi'ni (RMAN) yedeklemeler toodisk ve geri yükleme diskten için de desteklenir.

#### <a name="high-availability"></a>Yüksek kullanılabilirlik
[comment]: <> (bağlantı tooASM başvurur)
Oracle Data Guard, yüksek kullanılabilirlik ve olağanüstü durum kurtarma amacıyla desteklenir. Ayrıntılar bulunabilir [bu] [ virtual-machines-windows-classic-configure-oracle-data-guard] belgeleri.

#### <a name="other"></a>Diğer
Azure kullanılabilirlik kümeleri veya SAP izleme gibi tüm diğer genel konular hello hello Oracle veritabanı da VM'lerin dağıtımlar için bu belgenin ilk üç bölümde açıklandığı gibi geçerlidir.

## <a name="specifics-for-hello-sap-maxdb-database-on-windows"></a>SAP MaxDB veritabanı Windows hello için özellikleri
### <a name="sap-maxdb-version-support"></a>SAP MaxDB sürüm desteği
Şu anda destekler SAP MaxDB sürüm 7,9 Azure SAP NetWeaver tabanlı ürünleriyle kullanmak için SAP. SAP hizmet Market'ten sağlanan SAP MaxDB sunucu veya SAP NetWeaver tabanlı ürünleri ile kullanılan JDBC ve ODBC sürücüleri toobe için tüm güncelleştirmeleri yalnızca hello <https://support.sap.com/swdc>.
SAP NetWeaver SAP MaxDB üzerinde çalıştırma hakkında genel bilgi adresinde bulunabilir <https://scn.sap.com/community/maxdb>.

### <a name="supported-microsoft-windows-versions-and-azure-vm-types-for-sap-maxdb-dbms"></a>SAP MaxDB DBMS için desteklenen Microsoft Windows sürümleri ve Azure VM türleri
Azure üzerinde SAP MaxDB DBMS için toofind desteklenen hello Microsoft Windows sürümü bakın:

* [SAP ürün kullanılabilirliği matrisi (PAM)][sap-pam]
* SAP Not [1928533]

Merhaba işletim sisteminin Microsoft Windows 2012 R2 Microsoft Windows toouse hello en yeni sürümü önerilir.

### <a name="available-sap-maxdb-documentation"></a>Kullanılabilir SAP MaxDB belgeleri
SAP Not aşağıdaki hello SAP MaxDB belgelerine hello güncelleştirilmiş listesini bulabilirsiniz [767598 ]

### <a name="sap-maxdb-configuration-guidelines-for-sap-installations-in-azure-vms"></a>SAP yüklemelerde Azure VM'ler için SAP MaxDB yapılandırma yönergeleri
#### <a name="b48cfe3b-48e9-4f5b-a783-1d29155bd573"></a>Depolama yapılandırması
SAP MaxDB için Azure depolama en iyi uygulamaları izleyin hello genel öneriler bölümde belirtildiği [RDBMS dağıtım yapısı][dbms-guide-2].

> [!IMPORTANT]
> Diğer veritabanlarında olduğu gibi SAP MaxDB veri ve günlük dosyalarını da sahiptir. Ancak, SAP MaxDB terminolojisinde hello doğru "Birim" ("dosyası değil") bir terimdir. Örneğin, SAP MaxDB vardır veri ve günlük birimler. Bu işletim sistemi disk birimleri ile karıştırmayın.
>
>

Kısacası, gerekir:

* Merhaba SAP MaxDB veri ve günlük birimler (yani dosyaları) çok tutan hello Azure depolama hesabı**yerel olarak yedekli depolama (LRS)** bölümde belirtildiği gibi [Microsoft Azure depolama] [ dbms-guide-2.3].
* Günlük birimler (yani dosyaları) için hello GÇ yolundan SAP MaxDB veri birimler (yani dosyaları) için ayrı hello g/ç yolu. Bu, SAP MaxDB veri birimler (yani dosyaları) toobe bir mantıksal sürücü üzerinde yüklü olduğundan ve başka bir mantıksal sürücü üzerinde yüklü toobe SAP MaxDB günlük birimler (yani dosyaları) sahip olduğundan anlamına gelir.
* Merhaba uygun dosya SAP MaxDB veri veya günlük birimleri için (yani dosyaları) kullanıp ve Azure standart ya da Azure Premium depolama kullanmadığınıza bağlı olarak her bir Azure blob için bölümde açıklandığı gibi önbelleğe alma ayarlama [VM'ler için önbelleğe alma] [ dbms-guide-2.1].
* Hello geçerli IOPS kota disk başına hello gereksinimleri karşılayan sürece olası toostore hello verileri tek bir bağlı Azure VHD alt birimlerde olduğu ve ayrıca tüm veritabanı günlük birimleri başka bir tek bağlı Azure VHD depolar.
* Daha fazla IOPS ve/veya boşluk gerekirse, toouse Microsoft penceresi depolama havuzları (yalnızca Microsoft Windows Server 2012'de kullanılabilir ve üzeri) ya da Microsoft Windows için Microsoft Windows 2008 R2 toocreate bir büyük mantıksal aygıt bölümlemesine önerilir birden çok bağlama VHD diskleri. Ayrıca bkz. bölüm [yazılım RAID] [ dbms-guide-2.2] bu belgenin. Bu yaklaşım hello Yönetim genel gider toomanage hello disk alanı basitleştirir ve dosyalar arasında birden fazla bağlı Vhd'lere el ile dağıtma hello çaba önler.
* Merhaba yüksek IOPS gereksinimleri için DS serisi ve GS serisi Vm'lerde kullanılabilir olduğu Azure Premium Storage kullanabilirsiniz.

![Azure Iaas VM SAP MaxDB DBMS için başvuru yapılandırması][dbms-guide-figure-600]

#### <a name="23c78d3b-ca5a-4e72-8a24-645d141a3f5d"></a>Yedekleme ve geri yükleme
SAP MaxDB Azure'a dağıtırken, yedekleme yönteminize gözden geçirmeniz gerekir. Merhaba sistem üretken sistem olsa bile, SAP MaxDB tarafından barındırılan hello SAP veritabanında düzenli aralıklarla yedeklenmelidir. Azure Storage üç görüntüleri tutar, bir yedekleme şimdi sisteminizi depolama hatası ve daha önemli işlemsel veya yönetim hatalarına karşı koruma açısından daha az önemlidir. Böylece zaman içinde nokta kurtarma özellikleri sağlayarak mantıksal veya el ile hataları dengeleyebilirsiniz hello uygun yedekleme ve geri yükleme planı korumak için birincil nedenidir. Merhaba hedefi olacak şekilde tooeither kullanım yedeklemeleri toorestore hello veritabanı tooa belirli noktası Azure tooseed zaman ya da toouse hello yedeklere içinde başka bir sistem hello varolan veritabanı kopyalayarak. Örneğin, bir katman 2 SAP yapılandırma tooa 3 katmanlı sistem kurulumundan hello aynı aktaramıyor bir yedeğini geri tarafından sistem.

Yedekleme ve geri yükleme aynı şekilde standart SAP MaxDB kullanabilmek için şirket içi sistemler için yaptığı gibi yedekleme/geri yükleme hello SAP MaxDB belgelerine belgeleri birinde açıklanan araçları Azure works hello veritabanında listelenen SAP notta [767598 ].

#### <a name="77cd2fbb-307e-4cbf-a65f-745553f72d2c"></a>Yedekleme ve geri yükleme için başarım düşünceleri
Çıplak metal dağıtımlarındaki kaç birimleri paralel ve hello bu birimlerin performansı okunabilir'üzerinde yedekleme ve geri yükleme performans bağlıdır. Ayrıca, hello yedekleme sıkıştırma tarafından kullanılan CPU tüketimi too8 CPU iş parçacıklarını ile sanal makineleri üzerinde önemli bir rol yürütebilirsiniz. Bu nedenle, bir kabul edebilirsiniz:

* kullanılan VHD'ler toostore hello veritabanı aygıt daha az hello sayısı Merhaba, daha düşük hello genel üretilen işi okuma hello
* Merhaba VM CPU iş parçacıkları daha küçük hello sayısı Merhaba, yedekleme sıkıştırma daha ciddi hello etkisini hello
* daha az hedefleri (Stripe dizinleri, VHD) toowrite hello yedekleme, hello alt hello verimlilik hello

tooincrease hello sayısı için toowrite hedefler, birlikte, büyük olasılıkla gereksinimlerinize bağlı olarak kullanabileceğiniz iki seçenek vardır:

* Yedekleme için ayrı birimlerin ayrılması
* Sipariş tooimprove hello IOPS verimlilik şeritli disk birimde içinde birden fazla bağlı Vhd'lere üzerinden Hello yedekleme hedef birim bölümlemesine
* Ayrı bir adanmış mantıksal disk aygıtları için sahip:
  * SAP MaxDB yedekleme birimler (yani dosyaları)
  * SAP MaxDB veri birimler (yani dosyaları)
  * SAP MaxDB günlük birimler (yani dosyaları)

Bir birim üzerinde birden fazla bağlı Vhd'lere bölümlemesine ele alınan önceki bölümde [yazılım RAID] [ dbms-guide-2.2] bu belgenin.

#### <a name="f77c1436-9ad8-44fb-a331-8671342de818"></a>Diğer
Azure kullanılabilirlik kümeleri veya SAP izleme gibi tüm diğer genel konular da hello hello SAP MaxDB veritabanı VM'lerin dağıtımlar için bu belgenin ilk üç bölümde açıklandığı gibi geçerlidir.
Diğer SAP MaxDB özgü ayarları saydam tooAzure VM'ler ve SAP notta listelenen farklı belgelerinde açıklanan [767598 ] ve bu SAP Notlar:

* [826037]
* [1139904]
* [1173395]

## <a name="specifics-for-sap-livecache-on-windows"></a>SAP liveCache Windows özellikleri
### <a name="sap-livecache-version-support"></a>SAP liveCache sürüm desteği
SAP liveCache Azure sanal makinelerinde desteklenen en düşük sürümü **SAP LC/LCAPPS 10.0 SP 25** dahil olmak üzere **liveCache 7.9.08.31** ve **LCA yapı 25**, yayımlanan için **EhP 2 SAP SCM 7.0** ve daha yüksek.

### <a name="supported-microsoft-windows-versions-and-azure-vm-types-for-sap-livecache-dbms"></a>SAP liveCache DBMS desteklenen Microsoft Windows sürümleri ve Azure VM türleri
Azure üzerinde SAP liveCache için toofind desteklenen hello Microsoft Windows sürümü bakın:

* [SAP ürün kullanılabilirliği matrisi (PAM)][sap-pam]
* SAP Not [1928533]

Merhaba işletim sisteminin Microsoft Windows 2012 R2 Microsoft Windows toouse hello en yeni sürümü önerilir.

### <a name="sap-livecache-configuration-guidelines-for-sap-installations-in-azure-vms"></a>SAP liveCache SAP yüklemelerde Azure VM'ler için yapılandırma yönergeleri
#### <a name="recommended-azure-vm-types"></a>Azure VM türleri önerilir
SAP liveCache büyük hesaplamaları gerçekleştiren bir uygulama gibi hello tutar ve RAM ve CPU hızı SAP liveCache performans üzerinde büyük bir etkisi vardır.

SAP tarafından desteklenen hello Azure VM türleri için (SAP Not [1928533]), tüm sanal CPU kaynaklarını VM ayrılmış fiziksel CPU kaynaklarına göre hello hiper yönetici tarafından yedeklenen toohello ayrılmış. Hiçbir işleminin (ve bu nedenle hiçbir rekabet CPU kaynakları için) yerini alır.

Benzer şekilde, SAP tarafından desteklenen tüm Azure VM örneği türlerinde hello VM eşlenen % 100 toohello fiziksel bellek – işleminin (atlayarak taahhüt), örneğin, kullanılmaz bellektir.

A-series hello daha % 60 daha hızlı işlemcilere sahip oldukları gibi bu açısından toouse hello yeni D-serisi veya (kombinasyondaki Azure Premium Storage ile) DS serisi Azure VM türü önerilir. Merhaba en yüksek RAM ve CPU yükü G-serisi ve GS serisi (kombinasyondaki Azure Premium Storage ile) VM'ler hello son Intel® Xeon işlemci iki kez hello bellek ve hello D, dört kez hello katı hal sürücüsü depolama (SSD) sahip E5 v3 ailesi ile kullanabileceğiniz / DS serisi.

#### <a name="storage-configuration"></a>Depolama yapılandırması
SAP liveCache SAP MaxDB teknolojisine dayalı olarak, tüm SAP MaxDB bölümde belirtildiği Azure depolama en iyi uygulama önerilerini hello [depolama yapılandırması] [ dbms-guide-8.4.1] da SAP liveCache için geçerlidir.

#### <a name="dedicated-azure-vm-for-livecache"></a>Ayrılmış Azure VM liveCache için
SAP liveCache yoðun hesaplama gücüne kullandıkça verimli kullanım için toodeploy üzerinde ayrılmış bir Azure sanal makine önerilir.

![Azure VM verimli kullanım örneği için liveCache için ayrılmış][dbms-guide-figure-700]

#### <a name="backup-and-restore"></a>Yedekleme ve Geri Yükleme
Yedekleme ve geri yükleme, performans değerlendirmeleri gibi hello ilgili SAP MaxDB bölümlerde açıklanmıştır zaten [yedekleme ve geri yükleme] [ dbms-guide-8.4.2] ve [yedekleme için başarım düşünceleri ve geri yükleme][dbms-guide-8.4.3].

#### <a name="other"></a>Diğer
Tüm genel konular zaten hello açıklanan ilgili SAP MaxDB [bu] [ dbms-guide-8.4.4] bölüm.

## <a name="specifics-for-hello-sap-content-server-on-windows"></a>SAP içerik sunucusu Windows hello için özellikleri
Merhaba SAP içerik sunucusu, farklı biçimlerde elektronik belgeleri gibi ayrı, sunucu tabanlı bileşen toostore içeriktir. Merhaba SAP içerik sunucusu teknolojisi geliştirme tarafından sağlanır ve herhangi bir SAP uygulaması için kullanılan toobe çapraz uygulama. Ayrı bir sistemde yüklü. Tipik içerik, malzeme ve Bilgi Bankası ambarı veya hello mySAP PLM belge yönetim sistemi kaynaklanan teknik çizimler belgelerinden eğitim.

### <a name="sap-content-server-version-support"></a>SAP içerik Server sürüm desteği
SAP şu anda destekler:

* **SAP içerik sunucusu** sürümüyle **6.50 (ve üzeri)**
* **SAP MaxDB sürüm 7,9**
* **Microsoft IIS (Internet Information Server) sürüm 8.0 (ve üzeri)**

SAP içerik bu belgenin yazıldığı hello zaman sunucu toouse hello en yeni sürümü önerilir **6.50 SP4**ve hello en yeni sürümünü **Microsoft IIS 8.5**.

En son desteklenen hello sürümlerinde SAP içerik sunucusu ve Microsoft IIS hello denetleyin [SAP ürün kullanılabilirlik matris (PAM)][sap-pam].

### <a name="supported-microsoft-windows-and-azure-vm-types-for-sap-content-server"></a>SAP içerik sunucusu için desteklenen Microsoft Windows ve Azure VM türleri
Azure üzerinde SAP içerik sunucusu için desteklenen Windows sürümü kullanıma toofind bakın:

* [SAP ürün kullanılabilirliği matrisi (PAM)][sap-pam]
* SAP Not [1928533]

Toouse olan bu belgenin yazıldığı hello zaman Microsoft Windows hello en yeni sürümü önerilir **Windows Server 2012 R2**.

### <a name="sap-content-server-configuration-guidelines-for-sap-installations-in-azure-vms"></a>SAP yüklemelerde Azure VM'ler için SAP içerik sunucusu yapılandırma yönergeleri
#### <a name="storage-configuration"></a>Depolama yapılandırması
SAP içerik sunucusu toostore dosyaları hello SAP MaxDB veritabanında yapılandırırsanız, SAP MaxDB bölümde belirtildiği öneri tüm Azure depolama en iyi yöntemler [depolama yapılandırması] [ dbms-guide-8.4.1] da Merhaba SAP içerik sunucusu senaryo için geçerlidir.

SAP içerik sunucusu toostore dosyaları hello dosya sisteminde yapılandırırsanız olduğu adanmış bir mantıksal sürücü toouse önerilir. Depolama alanları'nı kullanarak sağlar tooalso artış mantıksal disk boyutu ve IOPS verimlilik bölümde açıklandığı gibi [yazılım RAID][dbms-guide-2.2].

#### <a name="sap-content-server-location"></a>SAP içerik sunucusu konumu
SAP içerik sunucusuna sahip hello dağıtılan toobe aynı Azure bölgesinde ve Azure hello SAP sistem dağıtıldığı sanal. Merhaba SAP sistem çalıştığı aynı VM toodeploy SAP içerik sunucusu bileşenlerini adanmış bir Azure VM veya üzerinde hello istediğinizi ücretsiz toodecide olduğunuz.

![Azure VM SAP içerik sunucusu için ayrılmış][dbms-guide-figure-800]

#### <a name="sap-cache-server-location"></a>SAP önbellek sunucusu konumu
Merhaba SAP önbellek sunucusu bir ek sunucu tabanlı bileşen tooprovide erişim too(cached) belgelerini yerel olarak ' dir. Merhaba SAP önbellek sunucusu bir SAP içerik sunucusu hello belgelerin önbelleğe alır. Belgeleri birden çok kez farklı konumlardan alınan toobe varsa toooptimize ağ trafiğini budur. Merhaba genel hello SAP önbellek sunucusu erişen toobe fiziksel olarak Kapat toohello istemci o hello SAP önbellek sunucusu olan kuralıdır.

Burada, iki seçeneğiniz vardır:

1. **İstemci olan bir arka uç SAP sistem** bir arka uç SAP sistemi yapılandırılmış tooaccess SAP içerik sunucusu ise, o SAP sistem bir istemcidir. SAP sistem ve SAP içerik sunucusu hello dağıtılan aynı Azure bölgesinde – hello aynı Azure veri merkezinde – oldukları fiziksel olarak Kapat tooeach diğer. Bu nedenle hiçbir gerek toohave adanmış bir SAP önbellek sunucusu yok. SAP UI istemcileri (SAP GUI ya da web tarayıcısı) erişim hello SAP sistem doğrudan ve hello sistem alır hello SAP içerik sunucusu belgelerden SAP.
2. **İstemci bir şirket içi web tarayıcısı olan** hello SAP içerik sunucusu, doğrudan hello web tarayıcısı tarafından erişilen yapılandırılmış toobe olabilir. Bu durumda, bir web tarayıcısı çalıştıran – şirket içi hello SAP içerik sunucusu, bir istemci olur. Şirket içi veri merkezi ve Azure veri merkezi farklı fiziksel konumlarda (ideal Kapat tooeach diğer) yerleştirilir. Şirket içi veri merkeziniz Azure siteden siteye VPN veya ExpressRoute aracılığıyla bağlanan tooAzure ' dir. Her iki seçenek güvenli VPN ağ bağlantısı tooAzure sunmasına rağmen siteden siteye ağ bağlantısı hello şirket içi veri merkezi ve hello Azure veri merkezi arasında ağ bant genişliği ve gecikme süresi SLA sağlamaz. toospeed erişim toodocuments yukarı hello aşağıdakilerden birini yapabilirsiniz:
   1. Şirket içi SAP önbellek Server yüklemek, Kapat toohello şirket içi web tarayıcısı (seçeneği [bu] [ dbms-guide-900-sap-cache-server-on-premises] Şekil)
   2. Şirket içi veri merkezi ve Azure veri merkezi arasında yüksek hızda ve düşük gecikme süreli Adanmış ağ bağlantısı sağlayan Azure ExpressRoute yapılandırın.

![Seçenek tooinstall SAP önbellek sunucusu şirket içi][dbms-guide-figure-900]
<a name="642f746c-e4d4-489d-bf63-73e80177a0a8"></a>

#### <a name="backup--restore"></a>Yedekleme / Geri Yükleme
Merhaba SAP MaxDB veritabanında hello SAP içerik sunucusu toostore dosyaları yapılandırırsanız, hello yedekleme/geri yükleme yordamı ve performans konuları zaten SAP MaxDB bölümde açıklanan [yedekleme ve geri yükleme] [ dbms-guide-8.4.2] ve bölüm [yedekleme ve geri yükleme için başarım düşünceleri][dbms-guide-8.4.3].

Merhaba dosya sisteminde hello SAP içerik sunucusu toostore dosyaları yapılandırırsanız, bir tooexecute el ile yedekleme/geri yükleme hello dosyanın tamamı yapısının hello belgeleri bulunduğu seçenektir. Benzer tooSAP MaxDB yedekleme/geri yükleme, olmasından toohave yedekleme amaç için ayrılmış disk birimi önerilir.

#### <a name="other"></a>Diğer
Diğer SAP içerik sunucusu belirli ayarlarını saydam tooAzure VM'ler ve çeşitli belgeler ve SAP notları açıklanmıştır:

* <https://Service.SAP.com/contentserver>
* SAP Not [1619726]  

## <a name="specifics-tooibm-db2-for-luw-on-windows"></a>Windows LUW için özellikleri tooIBM DB2
Microsoft Azure ile IBM DB2 üzerinde çalışan Linux, UNIX ve Windows (LUW) tooAzure sanal makineler için mevcut SAP uygulamanızı kolayca geçirebilirsiniz. IBM DB2 LUW için üzerinde SAP ile yöneticiler ve geliştiriciler kullanılabilir olan aynı geliştirme ve Yönetim Araçları şirket içi hello kullanmaya devam edebilirsiniz.
LUW bulunabilir için SAP Business Suite IBM DB2 üzerinde çalışan hakkında genel bilgi hello adresindeki SAP topluluk ağ (SCN) <https://scn.sap.com/community/db2-for-linux-unix-windows>.

Ek bilgi ve Azure üzerinde LUW DB2 üzerinde SAP ilgili güncelleştirmeler için bkz. SAP Not [2233094].

### <a name="ibm-db2-for-linux-unix-and-windows-version-support"></a>IBM DB2 Linux, UNIX ve Windows sürüm desteği
IBM DB2 için Microsoft Azure sanal makine hizmetleri üzerinde LUW üzerinde SAP DB2 sürüm 10.5 sürümünden itibaren desteklenir.

Desteklenen SAP ürünler ve Azure VM türleri hakkında daha fazla bilgi için lütfen tooSAP Not başvurun [1928533].

### <a name="ibm-db2-for-linux-unix-and-windows-configuration-guidelines-for-sap-installations-in-azure-vms"></a>IBM DB2 Linux, UNIX ve SAP yüklemelerde Azure VM'ler için Windows yapılandırma yönergeleri
#### <a name="storage-configuration"></a>Depolama yapılandırması
Tüm veritabanı dosyaları temel VHD disklerde hello NTFS dosya sistemi depolanması gerekir. Bu VHD takılı toohello Azure VM olan ve Azure sayfa BLOB depolama alanına bağlı (<https://msdn.microsoft.com/library/azure/ee691964.aspx>).
Her türlü ağ sürücülerine veya hello Azure Dosya Hizmetleri aşağıdaki gibi uzak paylaşımlara **değil** veritabanı dosyaları için desteklenir:

* <https://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-Microsoft-Azure-File-Service.aspx>
* <https://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-Connections-to-Microsoft-Azure-Files.aspx>

Azure Azure sayfa BLOB Depolama birimine dayalı VHD'ler kullanıyorsanız, bu belgede bölüm yapılan deyimleri hello [RDBMS dağıtım yapısı] [ dbms-guide-2] toodeployments hello IBM DB2 ile LUW için de geçerlidir Veritabanı.

Daha önce hello Genel bölümünde hello belgenin açıklandığı gibi Azure VHD'ler için IOPS işleme kotalar mevcut. Merhaba tam kotaları kullanılan hello VM türüne bağlıdır. Kendi kotaları ile VM türlerinin bir listesini bulunabilir [burada][virtual-machines-sizes]

Merhaba geçerli IOPS kota disk başına yeterli tüm veritabanı dosyaları hello olası toostore olduğu sürece tek tek Azure VHD bağladı.

İçin performans konuları da toochapter "veri güvenliği ve performansı hakkında önemli noktalar için veritabanı dizinlerde" SAP yükleme kılavuzları bakın.

Alternatif olarak, Windows depolama havuzları (yalnızca Windows Server 2012'de kullanılabilir ve üzeri) kullanabilir veya Windows 2008 R2 Windows şeritleme bölümde açıklanan [yazılım RAID] [ dbms-guide-2.2] bu belgenin toocreate bir büyük mantıksal aygıt üzerinden birden çok bağlama VHD diskleri.
Sapdata ve saptmp dizinlerinizi Hello DB2 depolama yollarını içeren hello diskler için bir fiziksel disk sektör boyutu 512 KB belirtmeniz gerekir. Windows depolama havuzlarını kullanırken hello depolama havuzu hello parametresini kullanarak komut satırı arabirimi kullanarak el ile oluşturmanız gerekir "-LogicalSectorSizeDefault". Ayrıntılar için bkz: <https://technet.microsoft.com/library/hh848689.aspx>.

#### <a name="backuprestore"></a>Yedekleme/Geri Yükleme
IBM DB2 için Hello yedekleme/geri yükleme işlevselliği LUW içinde desteklenen hello aynı şekilde standart Windows Server işletim sistemleri ve üzerinde Hyper-V gibi.

Geçerli bir veritabanı yedekleme stratejisi yerinde olduğundan emin olmanız gerekir.

Çıplak dağıtımlar olduğu gibi yedekleme/geri yükleme performans paralel şekilde kaç tane birimleri okunabilir ve hangi hello verimlilik bu birimlerin olabilir bağlıdır. Ayrıca, hello yedekleme sıkıştırma tarafından kullanılan CPU tüketimi yalnızca too8 CPU iş parçacıklarını ile sanal makineleri üzerinde önemli bir rol oynayabilir. Bu nedenle, bir kabul edebilirsiniz:

* Merhaba VHD'ler daha az hello sayısı toostore hello veritabanı cihazlar, hello kullanılan küçük, genel üretilen işi okuma hello
* Merhaba VM CPU iş parçacıkları daha küçük hello sayısı Merhaba, yedekleme sıkıştırma daha ciddi hello etkisini hello
* daha az hedefleri (Stripe dizinleri, VHD) toowrite hello yedekleme, hello alt hello verimlilik hello

hedefleri toowrite tooincrease hello sayısı, kullanılan/birleştirilmiş gereksinimlerinize bağlı olarak iki seçeneğiniz olabilir:

* Şeritli birim üzerinde sipariş tooimprove hello IOPS üretilen işi içinde birden fazla bağlı Vhd'lere üzerinden Hello yedekleme hedef birim bölümlemesine
* Birden fazla hedef dizin toowrite hello yedekleme için kullanma

#### <a name="high-availability-and-disaster-recovery"></a>Yüksek kullanılabilirlik ve olağanüstü durum kurtarma
Microsoft Küme sunucusu (MSCS) desteklenmiyor.

DB2 yüksek kullanılabilirlik olağanüstü durum kurtarma (HADR) desteklenir. Ad çözümlemesi çalışma hello HA yapılandırmasının Hello sanal makineler varsa, azure'da hello Kurulum şirket içi yapılan herhangi bir ayar farklı değil. Yalnızca IP çözümleme üzerinde toorely önerilmez.

Azure depolama coğrafi çoğaltma kullanmayın. Daha fazla bilgi için toochapter başvuran [Microsoft Azure depolama] [ dbms-guide-2.3] ve bölüm [yüksek kullanılabilirlik ve olağanüstü durum kurtarma Azure vm'lerle] [ dbms-guide-3].

#### <a name="other"></a>Diğer
Azure kullanılabilirlik kümeleri veya SAP izleme gibi tüm diğer genel konular hello IBM DB2 LUW için olan VM'ler de dağıtımları için bu belgenin ilk üç bölümde açıklandığı gibi geçerlidir.

Ayrıca toochapter başvuru [Genel SQL Server için Azure özeti SAP][dbms-guide-5.8].
