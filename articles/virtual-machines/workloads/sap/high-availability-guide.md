---
title: "Sanal makineler yüksek kullanılabilirlik için SAP NetWeaver aaaAzure | Microsoft Docs"
description: "SAP NetWeaver için Azure sanal makineler üzerinde yüksek kullanılabilirlik Kılavuzu"
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: goraco
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 5e514964-c907-4324-b659-16dd825f6f87
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 12/07/2016
ms.author: goraco
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 927409830065573248a43427eb382448ca07b6e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-for-sap-netweaver-on-azure-vms"></a><span data-ttu-id="6639f-103">Azure vm'lerinde SAP NetWeaver için yüksek kullanılabilirlik</span><span class="sxs-lookup"><span data-stu-id="6639f-103">High availability for SAP NetWeaver on Azure VMs</span></span>

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

[sap-installation-guides]:http://service.sap.com/instguides

[azure-cli]:../../../cli-install-nodejs.md
[azure-portal]:https://portal.azure.com
[azure-ps]:https://docs.microsoft.com/powershell/azureps-cmdlets-docs
[azure-quickstart-templates-github]:https://github.com/Azure/azure-quickstart-templates
[azure-script-ps]:https://go.microsoft.com/fwlink/p/?LinkID=395017
[azure-subscription-service-limits]:../../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md

[dbms-guide]:../../virtual-machines-windows-sap-dbms-guide.md
[dbms-guide-2.1]:../../virtual-machines-windows-sap-dbms-guide.md#c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f
[dbms-guide-2.2]:../../virtual-machines-windows-sap-dbms-guide.md#c8e566f9-21b7-4457-9f7f-126036971a91
[dbms-guide-2.3]:../../virtual-machines-windows-sap-dbms-guide.md#10b041ef-c177-498a-93ed-44b3441ab152
[dbms-guide-2]:../../virtual-machines-windows-sap-dbms-guide.md#65fa79d6-a85f-47ee-890b-22e794f51a64
[dbms-guide-3]:../../virtual-machines-windows-sap-dbms-guide.md#871dfc27-e509-4222-9370-ab1de77021c3
[dbms-guide-5.5.1]:../../virtual-machines-windows-sap-dbms-guide.md#0fef0e79-d3fe-4ae2-85af-73666a6f7268
[dbms-guide-5.5.2]:../../virtual-machines-windows-sap-dbms-guide.md#f9071eff-9d72-4f47-9da4-1852d782087b
[dbms-guide-5.6]:../../virtual-machines-windows-sap-dbms-guide.md#1b353e38-21b3-4310-aeb6-a77e7c8e81c8
[dbms-guide-5.8]:../../virtual-machines-windows-sap-dbms-guide.md#9053f720-6f3b-4483-904d-15dc54141e30
[dbms-guide-5]:../../virtual-machines-windows-sap-dbms-guide.md#3264829e-075e-4d25-966e-a49dad878737
[dbms-guide-8.4.1]:../../virtual-machines-windows-sap-dbms-guide.md#b48cfe3b-48e9-4f5b-a783-1d29155bd573
[dbms-guide-8.4.2]:../../virtual-machines-windows-sap-dbms-guide.md#23c78d3b-ca5a-4e72-8a24-645d141a3f5d
[dbms-guide-8.4.3]:../../virtual-machines-windows-sap-dbms-guide.md#77cd2fbb-307e-4cbf-a65f-745553f72d2c
[dbms-guide-8.4.4]:../../virtual-machines-windows-sap-dbms-guide.md#f77c1436-9ad8-44fb-a331-8671342de818
[dbms-guide-900-sap-cache-server-on-premises]:../../virtual-machines-windows-sap-dbms-guide.md#642f746c-e4d4-489d-bf63-73e80177a0a8

[dbms-guide-figure-100]:media/virtual-machines-shared-sap-dbms-guide/100_storage_account_types.png
[dbms-guide-figure-200]:media/virtual-machines-shared-sap-dbms-guide/200-ha-set-for-dbms-ha.png
[dbms-guide-figure-300]:media/virtual-machines-shared-sap-dbms-guide/300-reference-config-iaas.png
[dbms-guide-figure-400]:media/virtual-machines-shared-sap-dbms-guide/400-sql-2012-backup-to-blob-storage.png
[dbms-guide-figure-500]:media/virtual-machines-shared-sap-dbms-guide/500-sql-2012-backup-to-blob-storage-different-containers.png
[dbms-guide-figure-600]:media/virtual-machines-shared-sap-dbms-guide/600-iaas-maxdb.png
[dbms-guide-figure-700]:media/virtual-machines-shared-sap-dbms-guide/700-livecach-prod.png
[dbms-guide-figure-800]:media/virtual-machines-shared-sap-dbms-guide/800-azure-vm-sap-content-server.png
[dbms-guide-figure-900]:media/virtual-machines-shared-sap-dbms-guide/900-sap-cache-server-on-premises.png

[deployment-guide]:../../virtual-machines-windows-sap-deployment-guide.md
[deployment-guide-2.2]:../../virtual-machines-windows-sap-deployment-guide.md#42ee2bdb-1efc-4ec7-ab31-fe4c22769b94
[deployment-guide-3.1.2]:../../virtual-machines-windows-sap-deployment-guide.md#3688666f-281f-425b-a312-a77e7db2dfab
[deployment-guide-3.2]:../../virtual-machines-windows-sap-deployment-guide.md#db477013-9060-4602-9ad4-b0316f8bb281
[deployment-guide-3.3]:../../virtual-machines-windows-sap-deployment-guide.md#54a1fc6d-24fd-4feb-9c57-ac588a55dff2
[deployment-guide-3.4]:../../virtual-machines-windows-sap-deployment-guide.md#a9a60133-a763-4de8-8986-ac0fa33aa8c1
[deployment-guide-3]:../../virtual-machines-windows-sap-deployment-guide.md#b3253ee3-d63b-4d74-a49b-185e76c4088e
[deployment-guide-4.1]:../../virtual-machines-windows-sap-deployment-guide.md#604bcec2-8b6e-48d2-a944-61b0f5dee2f7
[deployment-guide-4.2]:../../virtual-machines-windows-sap-deployment-guide.md#7ccf6c3e-97ae-4a7a-9c75-e82c37beb18e
[deployment-guide-4.3]:../../virtual-machines-windows-sap-deployment-guide.md#31d9ecd6-b136-4c73-b61e-da4a29bbc9cc
[deployment-guide-4.4.2]:../../virtual-machines-windows-sap-deployment-guide.md#6889ff12-eaaf-4f3c-97e1-7c9edc7f7542
[deployment-guide-4.4]:../../virtual-machines-windows-sap-deployment-guide.md#c7cbb0dc-52a4-49db-8e03-83e7edc2927d
[deployment-guide-4.5.1]:../../virtual-machines-windows-sap-deployment-guide.md#987cf279-d713-4b4c-8143-6b11589bb9d4
[deployment-guide-4.5.2]:../../virtual-machines-windows-sap-deployment-guide.md#408f3779-f422-4413-82f8-c57a23b4fc2f
[deployment-guide-4.5]:../../virtual-machines-windows-sap-deployment-guide.md#d98edcd3-f2a1-49f7-b26a-07448ceb60ca
[deployment-guide-5.1]:../../virtual-machines-windows-sap-deployment-guide.md#bb61ce92-8c5c-461f-8c53-39f5e5ed91f2
[deployment-guide-5.2]:../../virtual-machines-windows-sap-deployment-guide.md#e2d592ff-b4ea-4a53-a91a-e5521edb6cd1
[deployment-guide-5.3]:../../virtual-machines-windows-sap-deployment-guide.md#fe25a7da-4e4e-4388-8907-8abc2d33cfd8

[deployment-guide-configure-monitoring-scenario-1]:../../virtual-machines-windows-sap-deployment-guide.md#ec323ac3-1de9-4c3a-b770-4ff701def65b
[deployment-guide-configure-proxy]:../../virtual-machines-windows-sap-deployment-guide.md#baccae00-6f79-4307-ade4-40292ce4e02d
[deployment-guide-figure-100]:media/virtual-machines-shared-sap-deployment-guide/100-deploy-vm-image.png
[deployment-guide-figure-1000]:media/virtual-machines-shared-sap-deployment-guide/1000-service-properties.png
[deployment-guide-figure-11]:../../virtual-machines-windows-sap-deployment-guide.md#figure-11
[deployment-guide-figure-1100]:media/virtual-machines-shared-sap-deployment-guide/1100-azperflib.png
[deployment-guide-figure-1200]:media/virtual-machines-shared-sap-deployment-guide/1200-cmd-test-login.png
[deployment-guide-figure-1300]:media/virtual-machines-shared-sap-deployment-guide/1300-cmd-test-executed.png
[deployment-guide-figure-14]:../../virtual-machines-windows-sap-deployment-guide.md#figure-14
[deployment-guide-figure-1400]:media/virtual-machines-shared-sap-deployment-guide/1400-azperflib-error-servicenotstarted.png
[deployment-guide-figure-300]:media/virtual-machines-shared-sap-deployment-guide/300-deploy-private-image.png
[deployment-guide-figure-400]:media/virtual-machines-shared-sap-deployment-guide/400-deploy-using-disk.png
[deployment-guide-figure-5]:../../virtual-machines-windows-sap-deployment-guide.md#figure-5
[deployment-guide-figure-50]:media/virtual-machines-shared-sap-deployment-guide/50-forced-tunneling-suse.png
[deployment-guide-figure-500]:media/virtual-machines-shared-sap-deployment-guide/500-install-powershell.png
[deployment-guide-figure-6]:../../virtual-machines-windows-sap-deployment-guide.md#figure-6
[deployment-guide-figure-600]:media/virtual-machines-shared-sap-deployment-guide/600-powershell-version.png
[deployment-guide-figure-7]:../../virtual-machines-windows-sap-deployment-guide.md#figure-7
[deployment-guide-figure-700]:media/virtual-machines-shared-sap-deployment-guide/700-install-powershell-installed.png
[deployment-guide-figure-760]:media/virtual-machines-shared-sap-deployment-guide/760-azure-cli-version.png
[deployment-guide-figure-900]:media/virtual-machines-shared-sap-deployment-guide/900-cmd-update-executed.png
[deployment-guide-figure-azure-cli-installed]:../../virtual-machines-windows-sap-deployment-guide.md#402488e5-f9bb-4b29-8063-1c5f52a892d0
[deployment-guide-figure-azure-cli-version]:../../virtual-machines-windows-sap-deployment-guide.md#0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda
[deployment-guide-install-vm-agent-windows]:../../virtual-machines-windows-sap-deployment-guide.md#b2db5c9a-a076-42c6-9835-16945868e866
[deployment-guide-troubleshooting-chapter]:../../virtual-machines-windows-sap-deployment-guide.md#564adb4f-5c95-4041-9616-6635e83a810b

[deploy-template-cli]:../../../resource-group-template-deploy.md#deploy-with-azure-cli-for-mac-linux-and-windows
[deploy-template-portal]:../../../resource-group-template-deploy.md#deploy-with-the-preview-portal
[deploy-template-powershell]:../../../resource-group-template-deploy.md#deploy-with-powershell

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:../../virtual-machines-windows-sap-get-started.md
[getting-started-dbms]:../../virtual-machines-windows-sap-get-started.md#1343ffe1-8021-4ce6-a08d-3a1553a4db82
[getting-started-deployment]:../../virtual-machines-windows-sap-get-started.md#6aadadd2-76b5-46d8-8713-e8d63630e955
[getting-started-planning]:../../virtual-machines-windows-sap-get-started.md#3da0389e-708b-4e82-b2a2-e92f132df89c

[getting-started-windows-classic]:../../virtual-machines-windows-classic-sap-get-started.md
[getting-started-windows-classic-dbms]:../../virtual-machines-windows-classic-sap-get-started.md#c5b77a14-f6b4-44e9-acab-4d28ff72a930
[getting-started-windows-classic-deployment]:../../virtual-machines-windows-classic-sap-get-started.md#f84ea6ce-bbb4-41f7-9965-34d31b0098ea
[getting-started-windows-classic-dr]:../../virtual-machines-windows-classic-sap-get-started.md#cff10b4a-01a5-4dc3-94b6-afb8e55757d3
[getting-started-windows-classic-ha-sios]:../../virtual-machines-windows-classic-sap-get-started.md#4bb7512c-0fa0-4227-9853-4004281b1037
[getting-started-windows-classic-planning]:../../virtual-machines-windows-classic-sap-get-started.md#f2a5e9d8-49e4-419e-9900-af783173481c

[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056

[ha-guide]:high-availability-guide.md

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

[sap-ha-guide]:high-availability-guide.md
[sap-ha-guide-1]:high-availability-guide.md#217c5479-5595-4cd8-870d-15ab00d4f84c
[sap-ha-guide-2]:high-availability-guide.md#42b8f600-7ba3-4606-b8a5-53c4f026da08
[sap-ha-guide-3]:high-availability-guide.md#42156640c6-01cf-45a9-b225-4baa678b24f1
[sap-ha-guide-3.1]:high-availability-guide.md#f76af273-1993-4d83-b12d-65deeae23686
[sap-ha-guide-3.2]:high-availability-guide.md#3e85fbe0-84b1-4892-87af-d9b65ff91860
[sap-ha-guide-4]:high-availability-guide.md#8ecf3ba0-67c0-4495-9c14-feec1a2255b7
[sap-ha-guide-4.1]:high-availability-guide.md#1a3c5408-b168-46d6-99f5-4219ad1b1ff2
[sap-ha-guide-5]:high-availability-guide.md#fdfee875-6e66-483a-a343-14bbaee33275
[sap-ha-guide-5.1]:high-availability-guide.md#be21cf3e-fb01-402b-9955-54fbecf66592
[sap-ha-guide-5.2]:high-availability-guide.md#ff7a9a06-2bc5-4b20-860a-46cdb44669cd
[sap-ha-guide-6]:high-availability-guide.md#2ddba413-a7f5-4e4e-9a51-87908879c10a
[sap-ha-guide-6.1]:high-availability-guide.md#1a464091-922b-48d7-9d08-7cecf757f341
[sap-ha-guide-6.2]:high-availability-guide.md#44641e18-a94e-431f-95ff-303ab65e0bcb
[sap-ha-guide-7]:high-availability-guide.md#2e3fec50-241e-441b-8708-0b1864f66dfa
[sap-ha-guide-7.1]:high-availability-guide.md#93faa747-907e-440a-b00a-1ae0a89b1c0e
[sap-ha-guide-7.2]:high-availability-guide.md#f559c285-ee68-4eec-add1-f60fe7b978db
[sap-ha-guide-7.2.1]:high-availability-guide.md#b5b1fd0b-1db4-4d49-9162-de07a0132a51
[sap-ha-guide-7.3]:high-availability-guide.md#ddd878a0-9c2f-4b8e-8968-26ce60be1027
[sap-ha-guide-7.4]:high-availability-guide.md#045252ed-0277-4fc8-8f46-c5a29694a816
[sap-ha-guide-8]:high-availability-guide.md#78092dbe-165b-454c-92f5-4972bdbef9bf
[sap-ha-guide-8.1]:high-availability-guide.md#c87a8d3f-b1dc-4d2f-b23c-da4b72977489
[sap-ha-guide-8.2]:high-availability-guide.md#7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310
[sap-ha-guide-8.3]:high-availability-guide.md#47d5300a-a830-41d4-83dd-1a0d1ffdbe6a
[sap-ha-guide-8.4]:high-availability-guide.md#b22d7b3b-4343-40ff-a319-097e13f62f9e
[sap-ha-guide-8.5]:high-availability-guide.md#9fbd43c0-5850-4965-9726-2a921d85d73f
[sap-ha-guide-8.6]:high-availability-guide.md#84c019fe-8c58-4dac-9e54-173efd4b2c30
[sap-ha-guide-8.7]:high-availability-guide.md#7a8f3e9b-0624-4051-9e41-b73fff816a9e
[sap-ha-guide-8.8]:high-availability-guide.md#f19bd997-154d-4583-a46e-7f5a69d0153c
[sap-ha-guide-8.9]:high-availability-guide.md#fe0bd8b5-2b43-45e3-8295-80bee5415716
[sap-ha-guide-8.10]:high-availability-guide.md#e69e9a34-4601-47a3-a41c-d2e11c626c0c
[sap-ha-guide-8.11]:high-availability-guide.md#661035b2-4d0f-4d31-86f8-dc0a50d78158
[sap-ha-guide-8.12]:high-availability-guide.md#0d67f090-7928-43e0-8772-5ccbf8f59aab
[sap-ha-guide-8.12.1]:high-availability-guide.md#5eecb071-c703-4ccc-ba6d-fe9c6ded9d79
[sap-ha-guide-8.12.2]:high-availability-guide.md#e49a4529-50c9-4dcf-bde7-15a0c21d21ca
[sap-ha-guide-8.12.2.1]:high-availability-guide.md#06260b30-d697-4c4d-b1c9-d22c0bd64855
[sap-ha-guide-8.12.2.2]:high-availability-guide.md#4c08c387-78a0-46b1-9d27-b497b08cac3d
[sap-ha-guide-8.12.3]:high-availability-guide.md#5c8e5482-841e-45e1-a89d-a05c0907c868
[sap-ha-guide-8.12.3.1]:high-availability-guide.md#1c2788c3-3648-4e82-9e0d-e058e475e2a3
[sap-ha-guide-8.12.3.2]:high-availability-guide.md#dd41d5a2-8083-415b-9878-839652812102
[sap-ha-guide-8.12.3.3]:high-availability-guide.md#d9c1fc8e-8710-4dff-bec2-1f535db7b006
[sap-ha-guide-9]:high-availability-guide.md#a06f0b49-8a7a-42bf-8b0d-c12026c5746b
[sap-ha-guide-9.1]:high-availability-guide.md#31c6bd4f-51df-4057-9fdf-3fcbc619c170
[sap-ha-guide-9.1.1]:high-availability-guide.md#a97ad604-9094-44fe-a364-f89cb39bf097
[sap-ha-guide-9.1.2]:high-availability-guide.md#eb5af918-b42f-4803-bb50-eff41f84b0b0
[sap-ha-guide-9.1.3]:high-availability-guide.md#e4caaab2-e90f-4f2c-bc84-2cd2e12a9556
[sap-ha-guide-9.1.4]:high-availability-guide.md#10822f4f-32e7-4871-b63a-9b86c76ce761
[sap-ha-guide-9.1.5]:high-availability-guide.md#4498c707-86c0-4cde-9c69-058a7ab8c3ac
[sap-ha-guide-9.2]:high-availability-guide.md#85d78414-b21d-4097-92b6-34d8bcb724b7
[sap-ha-guide-9.3]:high-availability-guide.md#8a276e16-f507-4071-b829-cdc0a4d36748
[sap-ha-guide-9.4]:high-availability-guide.md#094bc895-31d4-4471-91cc-1513b64e406a
[sap-ha-guide-9.5]:high-availability-guide.md#2477e58f-c5a7-4a5d-9ae3-7b91022cafb5
[sap-ha-guide-9.6]:high-availability-guide.md#0ba4a6c1-cc37-4bcf-a8dc-025de4263772
[sap-ha-guide-10]:high-availability-guide.md#18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9
[sap-ha-guide-10.1]:high-availability-guide.md#65fdef0f-9f94-41f9-b314-ea45bbfea445
[sap-ha-guide-10.2]:high-availability-guide.md#5e959fa9-8fcd-49e5-a12c-37f6ba07b916
[sap-ha-guide-10.3]:high-availability-guide.md#755a6b93-0099-4533-9f6d-5c9a613878b5

[sap-ha-multi-sid-guide]:high-availability-multi-sid.md (SAP multi-SID high-availability configuration)


[sap-ha-guide-figure-1000]:media/virtual-machines-shared-sap-high-availability-guide/1000-wsfc-for-sap-ascs-on-azure.png
[sap-ha-guide-figure-1001]:media/virtual-machines-shared-sap-high-availability-guide/1001-wsfc-on-azure-ilb.png
[sap-ha-guide-figure-1002]:media/virtual-machines-shared-sap-high-availability-guide/1002-wsfc-sios-on-azure-ilb.png
[sap-ha-guide-figure-2000]:media/virtual-machines-shared-sap-high-availability-guide/2000-wsfc-sap-as-ha-on-azure.png
[sap-ha-guide-figure-2001]:media/virtual-machines-shared-sap-high-availability-guide/2001-wsfc-sap-ascs-ha-on-azure.png
[sap-ha-guide-figure-2003]:media/virtual-machines-shared-sap-high-availability-guide/2003-wsfc-sap-dbms-ha-on-azure.png
[sap-ha-guide-figure-2004]:media/virtual-machines-shared-sap-high-availability-guide/2004-wsfc-sap-ha-e2e-archit-template1-on-azure.png
[sap-ha-guide-figure-2005]:media/virtual-machines-shared-sap-high-availability-guide/2005-wsfc-sap-ha-e2e-arch-template2-on-azure.png

[sap-ha-guide-figure-3000]:media/virtual-machines-shared-sap-high-availability-guide/3000-template-parameters-sap-ha-arm-on-azure.png
[sap-ha-guide-figure-3001]:media/virtual-machines-shared-sap-high-availability-guide/3001-configuring-dns-servers-for-Azure-vnet.png
[sap-ha-guide-figure-3002]:media/virtual-machines-shared-sap-high-availability-guide/3002-configuring-static-IP-address-for-network-card-of-each-vm.png
[sap-ha-guide-figure-3003]:media/virtual-machines-shared-sap-high-availability-guide/3003-setup-static-ip-address-ilb-for-ascs-instance.png
[sap-ha-guide-figure-3004]:media/virtual-machines-shared-sap-high-availability-guide/3004-default-ascs-scs-ilb-balancing-rules-for-azure-ilb.png
[sap-ha-guide-figure-3005]:media/virtual-machines-shared-sap-high-availability-guide/3005-changing-ascs-scs-default-ilb-rules-for-azure-ilb.png
[sap-ha-guide-figure-3006]:media/virtual-machines-shared-sap-high-availability-guide/3006-adding-vm-to-domain.png
[sap-ha-guide-figure-3007]:media/virtual-machines-shared-sap-high-availability-guide/3007-config-wsfc-1.png
[sap-ha-guide-figure-3008]:media/virtual-machines-shared-sap-high-availability-guide/3008-config-wsfc-2.png
[sap-ha-guide-figure-3009]:media/virtual-machines-shared-sap-high-availability-guide/3009-config-wsfc-3.png
[sap-ha-guide-figure-3010]:media/virtual-machines-shared-sap-high-availability-guide/3010-config-wsfc-4.png
[sap-ha-guide-figure-3011]:media/virtual-machines-shared-sap-high-availability-guide/3011-config-wsfc-5.png
[sap-ha-guide-figure-3012]:media/virtual-machines-shared-sap-high-availability-guide/3012-config-wsfc-6.png
[sap-ha-guide-figure-3013]:media/virtual-machines-shared-sap-high-availability-guide/3013-config-wsfc-7.png
[sap-ha-guide-figure-3014]:media/virtual-machines-shared-sap-high-availability-guide/3014-config-wsfc-8.png
[sap-ha-guide-figure-3015]:media/virtual-machines-shared-sap-high-availability-guide/3015-config-wsfc-9.png
[sap-ha-guide-figure-3016]:media/virtual-machines-shared-sap-high-availability-guide/3016-config-wsfc-10.png
[sap-ha-guide-figure-3017]:media/virtual-machines-shared-sap-high-availability-guide/3017-config-wsfc-11.png
[sap-ha-guide-figure-3018]:media/virtual-machines-shared-sap-high-availability-guide/3018-config-wsfc-12.png
[sap-ha-guide-figure-3019]:media/virtual-machines-shared-sap-high-availability-guide/3019-assign-permissions-on-share-for-cluster-name-object.png
[sap-ha-guide-figure-3020]:media/virtual-machines-shared-sap-high-availability-guide/3020-change-object-type-include-computer-objects.png
[sap-ha-guide-figure-3021]:media/virtual-machines-shared-sap-high-availability-guide/3021-check-box-for-computer-objects.png
[sap-ha-guide-figure-3022]:media/virtual-machines-shared-sap-high-availability-guide/3022-set-security-attributes-for-cluster-name-object-on-file-share-quorum.png
[sap-ha-guide-figure-3023]:media/virtual-machines-shared-sap-high-availability-guide/3023-call-configure-cluster-quorum-setting-wizard.png
[sap-ha-guide-figure-3024]:media/virtual-machines-shared-sap-high-availability-guide/3024-selection-screen-different-quorum-configurations.png
[sap-ha-guide-figure-3025]:media/virtual-machines-shared-sap-high-availability-guide/3025-selection-screen-file-share-witness.png
[sap-ha-guide-figure-3026]:media/virtual-machines-shared-sap-high-availability-guide/3026-define-file-share-location-for-witness-share.png
[sap-ha-guide-figure-3027]:media/virtual-machines-shared-sap-high-availability-guide/3027-successful-reconfiguration-cluster-file-share-witness.png
[sap-ha-guide-figure-3028]:media/virtual-machines-shared-sap-high-availability-guide/3028-install-dot-net-framework-35.png
[sap-ha-guide-figure-3029]:media/virtual-machines-shared-sap-high-availability-guide/3029-install-dot-net-framework-35-progress.png
[sap-ha-guide-figure-3030]:media/virtual-machines-shared-sap-high-availability-guide/3030-sios-installer.png
[sap-ha-guide-figure-3031]:media/virtual-machines-shared-sap-high-availability-guide/3031-first-screen-sios-data-keeper-installation.png
[sap-ha-guide-figure-3032]:media/virtual-machines-shared-sap-high-availability-guide/3032-data-keeper-informs-service-be-disabled.png
[sap-ha-guide-figure-3033]:media/virtual-machines-shared-sap-high-availability-guide/3033-user-selection-sios-data-keeper.png
[sap-ha-guide-figure-3034]:media/virtual-machines-shared-sap-high-availability-guide/3034-domain-user-sios-data-keeper.png
[sap-ha-guide-figure-3035]:media/virtual-machines-shared-sap-high-availability-guide/3035-provide-sios-data-keeper-license.png
[sap-ha-guide-figure-3036]:media/virtual-machines-shared-sap-high-availability-guide/3036-data-keeper-management-config-tool.png
[sap-ha-guide-figure-3037]:media/virtual-machines-shared-sap-high-availability-guide/3037-tcp-ip-address-first-node-data-keeper.png
[sap-ha-guide-figure-3038]:media/virtual-machines-shared-sap-high-availability-guide/3038-create-replication-sios-job.png
[sap-ha-guide-figure-3039]:media/virtual-machines-shared-sap-high-availability-guide/3039-define-sios-replication-job-name.png
[sap-ha-guide-figure-3040]:media/virtual-machines-shared-sap-high-availability-guide/3040-define-sios-source-node.png
[sap-ha-guide-figure-3041]:media/virtual-machines-shared-sap-high-availability-guide/3041-define-sios-target-node.png
[sap-ha-guide-figure-3042]:media/virtual-machines-shared-sap-high-availability-guide/3042-define-sios-synchronous-replication.png
[sap-ha-guide-figure-3043]:media/virtual-machines-shared-sap-high-availability-guide/3043-enable-sios-replicated-volume-as-cluster-volume.png
[sap-ha-guide-figure-3044]:media/virtual-machines-shared-sap-high-availability-guide/3044-data-keeper-synchronous-mirroring-for-SAP-gui.png
[sap-ha-guide-figure-3045]:media/virtual-machines-shared-sap-high-availability-guide/3045-replicated-disk-by-data-keeper-in-wsfc.png
[sap-ha-guide-figure-3046]:media/virtual-machines-shared-sap-high-availability-guide/3046-dns-entry-sap-ascs-virtual-name-ip.png
[sap-ha-guide-figure-3047]:media/virtual-machines-shared-sap-high-availability-guide/3047-dns-manager.png
[sap-ha-guide-figure-3048]:media/virtual-machines-shared-sap-high-availability-guide/3048-default-cluster-probe-port.png
[sap-ha-guide-figure-3049]:media/virtual-machines-shared-sap-high-availability-guide/3049-cluster-probe-port-after.png
[sap-ha-guide-figure-3050]:media/virtual-machines-shared-sap-high-availability-guide/3050-service-type-ers-delayed-automatic.png
[sap-ha-guide-figure-5000]:media/virtual-machines-shared-sap-high-availability-guide/5000-wsfc-sap-sid-node-a.png
[sap-ha-guide-figure-5001]:media/virtual-machines-shared-sap-high-availability-guide/5001-sios-replicating-local-volume.png
[sap-ha-guide-figure-5002]:media/virtual-machines-shared-sap-high-availability-guide/5002-wsfc-sap-sid-node-b.png
[sap-ha-guide-figure-5003]:media/virtual-machines-shared-sap-high-availability-guide/5003-sios-replicating-local-volume-b-to-a.png

[sap-ha-guide-figure-6003]:media/virtual-machines-shared-sap-high-availability-guide/6003-sap-multi-sid-full-landscape.png

[powershell-install-configure]:https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[resource-group-authoring-templates]:../../../resource-group-authoring-templates.md
[resource-group-overview]:../../../../../azure-resource-manager/resource-group-overview.md
[resource-groups-networking]:../../../virtual-network/resource-groups-networking.md
[sap-pam]:https://support.sap.com/pam (SAP Product Availability Matrix)
[sap-templates-2-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-2-tier-os-disk]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-disk%2Fazuredeploy.json
[sap-templates-2-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-image%2Fazuredeploy.json
[sap-templates-3-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-3-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-user-image%2Fazuredeploy.json
[sap-templates-3-tier-multisid-xscs-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs%2Fazuredeploy.json
[sap-templates-3-tier-multisid-db-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[sap-templates-3-tier-multisid-apps-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-apps%2Fazuredeploy.json
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
[virtual-machines-windows-attach-disk-portal]:../../virtual-machines-windows-attach-disk-portal.md
[virtual-machines-azure-resource-manager-architecture]:../../../azure-resource-manager/resource-group-overview.md
[virtual-machines-azure-resource-manager-architecture-benefits-arm]:../../../azure-resource-manager/resource-group-overview.md#the-benefits-of-using-resource-manager
[virtual-machines-azurerm-versus-azuresm]:virtual-machines-windows-compare-deployment-models.md
[virtual-machines-windows-classic-configure-oracle-data-guard]:../../virtual-machines-windows-classic-configure-oracle-data-guard.md
[virtual-machines-linux-cli-deploy-templates]:../../linux/cli-deploy-templates.md
[virtual-machines-deploy-rmtemplates-powershell]:../../virtual-machines-windows-ps-manage.md
[virtual-machines-linux-agent-user-guide]:../../linux/agent-user-guide.md
[virtual-machines-linux-agent-user-guide-command-line-options]:../../linux/agent-user-guide.md#command-line-options
[virtual-machines-linux-capture-image]:../../linux/capture-image.md
[virtual-machines-linux-capture-image-capture]:../../linux/capture-image.md#capture-the-vm
[virtual-machines-windows-capture-image]:../../virtual-machines-windows-capture-image.md
[virtual-machines-windows-capture-image-capture]:../../virtual-machines-windows-capture-image.md#capture-the-vm
[virtual-machines-linux-configure-lvm]:../../linux/configure-lvm.md
[virtual-machines-linux-configure-raid]:../../linux/configure-raid.md
[virtual-machines-linux-classic-create-upload-vhd-step-1]:../../virtual-machines-linux-classic-create-upload-vhd.md#step-1-prepare-the-image-to-be-uploaded
[virtual-machines-linux-create-upload-vhd-suse]:../../linux/suse-create-upload-vhd.md
[virtual-machines-linux-redhat-create-upload-vhd]:../../linux/redhat-create-upload-vhd.md
[virtual-machines-linux-how-to-attach-disk]:../../linux/add-disk.md
[virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]:../../linux/add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk
[virtual-machines-linux-tutorial]:../../linux/quick-create-cli.md
[virtual-machines-linux-update-agent]:../../linux/update-agent.md
[virtual-machines-manage-availability]:../../virtual-machines-windows-manage-availability.md
[virtual-machines-ps-create-preconfigure-windows-resource-manager-vms]:../../virtual-machines-windows-ps-create.md
[virtual-machines-sizes]:../../virtual-machines-windows-sizes.md
[virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]:../../windows/sql/virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md
[virtual-machines-windows-portal-sql-alwayson-int-listener]:../../windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md
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
[vpn-gateway-site-to-site-create]:../../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md
[vpn-gateway-vpn-faq]:../../../vpn-gateway/vpn-gateway-vpn-faq.md
[xplat-cli]:../../../cli-install-nodejs.md
[xplat-cli-azure-resource-manager]:../../../xplat-cli-azure-resource-manager.md


<span data-ttu-id="6639f-109">Azure sanal makinelerin işlem, depolama ve ağ kaynaklarına, en az sürede ve uzun tedarik döngüleri olmadan gereken kuruluşlar için hello çözümü şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="6639f-109">Azure Virtual Machines is hello solution for organizations that need compute, storage, and network resources, in minimal time, and without lengthy procurement cycles.</span></span> <span data-ttu-id="6639f-110">Azure sanal makineleri toodeploy Klasik uygulamaları SAP NetWeaver tabanlı ABAP, Java ve ABAP + Java yığını gibi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6639f-110">You can use Azure Virtual Machines toodeploy classic applications like SAP NetWeaver-based ABAP, Java, and an ABAP+Java stack.</span></span> <span data-ttu-id="6639f-111">Güvenilirlik ve kullanılabilirlik ek şirket içi kaynaklar olmadan genişletir.</span><span class="sxs-lookup"><span data-stu-id="6639f-111">Extend reliability and availability without additional on-premises resources.</span></span> <span data-ttu-id="6639f-112">Azure sanal makineleri şirket içi bağlantılar, Azure sanal makineler, kuruluşunuzun şirket içi etki alanları, özel Bulutlar ve SAP sistem yatay tümleştirebilir şekilde destekler.</span><span class="sxs-lookup"><span data-stu-id="6639f-112">Azure Virtual Machines supports cross-premises connectivity, so you can integrate Azure Virtual Machines into your organization's on-premises domains, private clouds, and SAP system landscape.</span></span>

<span data-ttu-id="6639f-113">Bu makalede, toodeploy yüksek kullanılabilirlik SAP sistemleri Azure'da hello Azure Resource Manager dağıtım modelini kullanarak alabilecek hello adımları kapsar.</span><span class="sxs-lookup"><span data-stu-id="6639f-113">In this article, we cover hello steps that you can take toodeploy high-availability SAP systems in Azure by using hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="6639f-114">Biz bu ana görevlerinde ilerlemenizde:</span><span class="sxs-lookup"><span data-stu-id="6639f-114">We walk you through these major tasks:</span></span>

* <span data-ttu-id="6639f-115">Merhaba, doğru SAP notlar ve yükleme kılavuzları, hello listelenen Bul [kaynakları] [ sap-ha-guide-2] bölümü.</span><span class="sxs-lookup"><span data-stu-id="6639f-115">Find hello right SAP Notes and installation guides, listed in hello [Resources][sap-ha-guide-2] section.</span></span> <span data-ttu-id="6639f-116">Bu makalede SAP yükleme belgelerini tamamlar ve yardımcı olabilecek hello birincil kaynaklardır SAP notları yükleyip belirli platformlar SAP yazılımı dağıtın.</span><span class="sxs-lookup"><span data-stu-id="6639f-116">This article complements SAP installation documentation and SAP Notes, which are hello primary resources that can help you install and deploy SAP software on specific platforms.</span></span>
* <span data-ttu-id="6639f-117">Merhaba farklarını hello Azure Resource Manager dağıtım modeli ve hello Azure Klasik dağıtım modeli hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="6639f-117">Learn hello differences between hello Azure Resource Manager deployment model and hello Azure classic deployment model.</span></span>
* <span data-ttu-id="6639f-118">Azure dağıtımınız için doğru hello modeli seçebilmeniz için Windows Server Yük Devretme Kümelemesi çekirdek modları hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="6639f-118">Learn about Windows Server Failover Clustering quorum modes, so you can select hello model that is right for your Azure deployment.</span></span>
* <span data-ttu-id="6639f-119">Azure hizmetlerinde paylaşılan Windows Server Yük Devretme Kümelemesi depolama hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="6639f-119">Learn about Windows Server Failover Clustering shared storage in Azure services.</span></span>
* <span data-ttu-id="6639f-120">Korunmasına nasıl yardımcı toohelp başarısızlık durumunu tek nokta bileşenleri gibi gelişmiş iş uygulama programlama (ABAP) SAP merkezi Hizmetleri (ASCS) öğrenin / SAP merkezi Hizmetleri (SCS) ve veritabanı yönetim sistemi (DBMS) ve yedek bileşenlerin SAP gibi Azure uygulama sunucusu.</span><span class="sxs-lookup"><span data-stu-id="6639f-120">Learn how toohelp protect single-point-of-failure components like Advanced Business Application Programming (ABAP) SAP Central Services (ASCS)/SAP Central Services (SCS) and database management systems (DBMS), and redundant components like SAP Application Server, in Azure.</span></span>
* <span data-ttu-id="6639f-121">Adım adım örnek bir yükleme ve bir Windows Server Yük Devretme Kümelemesi küme azure'da yüksek kullanılabilirlik SAP sisteminde yapılandırmasının, Azure Kaynak Yöneticisi'ni kullanarak izleyin.</span><span class="sxs-lookup"><span data-stu-id="6639f-121">Follow a step-by-step example of an installation and configuration of a high-availability SAP system in a Windows Server Failover Clustering cluster in Azure by using Azure Resource Manager.</span></span>
* <span data-ttu-id="6639f-122">Ek adımlar gerekli toouse Windows Server Yük Devretme Kümelemesi azure'da, ancak, bir şirket içi dağıtımda gerekli olmayan hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="6639f-122">Learn about additional steps required toouse Windows Server Failover Clustering in Azure, but which are not needed in an on-premises deployment.</span></span>

<span data-ttu-id="6639f-123">toosimplify dağıtımı ve yapılandırması, bu makalede, kullandığımız SAP üç katmanlı yüksek kullanılabilirlik Resource Manager şablonları hello.</span><span class="sxs-lookup"><span data-stu-id="6639f-123">toosimplify deployment and configuration, in this article, we use hello SAP three-tier high-availability Resource Manager templates.</span></span> <span data-ttu-id="6639f-124">Merhaba şablonları bir yüksek kullanılabilirlik SAP sistemi için gereksinim duyduğunuz hello tüm altyapının dağıtımını otomatik hale getirme.</span><span class="sxs-lookup"><span data-stu-id="6639f-124">hello templates automate deployment of hello entire infrastructure that you need for a high-availability SAP system.</span></span> <span data-ttu-id="6639f-125">Merhaba altyapı SAP uygulama performans standart (SAP) boyutlandırma SAP sisteminizin de destekler.</span><span class="sxs-lookup"><span data-stu-id="6639f-125">hello infrastructure also supports SAP Application Performance Standard (SAPS) sizing of your SAP system.</span></span>

## <span data-ttu-id="6639f-126"><a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a>Önkoşulları</span><span class="sxs-lookup"><span data-stu-id="6639f-126"><a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a> Prerequisites</span></span>
<span data-ttu-id="6639f-127">Başlamadan önce aşağıdaki bölümlerde hello açıklanan hello önkoşulları karşıladığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="6639f-127">Before you start, make sure that you meet hello prerequisites that are described in hello following sections.</span></span> <span data-ttu-id="6639f-128">Tüm kaynaklar listelenen hello emin toocheck de [kaynakları] [ sap-ha-guide-2] bölümü.</span><span class="sxs-lookup"><span data-stu-id="6639f-128">Also, be sure toocheck all resources listed in hello [Resources][sap-ha-guide-2] section.</span></span>

<span data-ttu-id="6639f-129">Bu makalede, Azure Resource Manager şablonları için kullandığımız [üç katmanlı SAP NetWeaver](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image/).</span><span class="sxs-lookup"><span data-stu-id="6639f-129">In this article, we use Azure Resource Manager templates for [three-tier SAP NetWeaver](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image/).</span></span> <span data-ttu-id="6639f-130">Şablonları yararlı bir genel bakış için bkz: [SAP Azure Resource Manager şablonları](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/).</span><span class="sxs-lookup"><span data-stu-id="6639f-130">For a helpful overview of templates, see [SAP Azure Resource Manager templates](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/).</span></span>

## <span data-ttu-id="6639f-131"><a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a>Kaynakları</span><span class="sxs-lookup"><span data-stu-id="6639f-131"><a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a> Resources</span></span>
<span data-ttu-id="6639f-132">Bu makaleler Azure SAP dağıtımlarda kapsar:</span><span class="sxs-lookup"><span data-stu-id="6639f-132">These articles cover SAP deployments in Azure:</span></span>

* <span data-ttu-id="6639f-133">[Azure sanal makineleri planlama ve uygulama SAP NetWeaver için][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="6639f-133">[Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide]</span></span>
* <span data-ttu-id="6639f-134">[SAP NetWeaver için Azure sanal makineler dağıtımı][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="6639f-134">[Azure Virtual Machines deployment for SAP NetWeaver][deployment-guide]</span></span>
* <span data-ttu-id="6639f-135">[SAP NetWeaver için Azure sanal makineleri DBMS dağıtımı][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="6639f-135">[Azure Virtual Machines DBMS deployment for SAP NetWeaver][dbms-guide]</span></span>
* <span data-ttu-id="6639f-136">[Azure sanal makineler için yüksek oranda kullanılabilirlik SAP NetWeaver (Bu Kılavuzu)][sap-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="6639f-136">[Azure Virtual Machines high availability for SAP NetWeaver (this guide)][sap-ha-guide]</span></span>

> [!NOTE]
> <span data-ttu-id="6639f-137">Mümkün olduğunda, SAP Yükleme Kılavuzu'na başvuran bir bağlantı toohello sunuyoruz (Merhaba bkz [SAP yükleme kılavuzları][sap-installation-guides]).</span><span class="sxs-lookup"><span data-stu-id="6639f-137">Whenever possible, we give you a link toohello referring SAP installation guide (see hello [SAP installation guides][sap-installation-guides]).</span></span> <span data-ttu-id="6639f-138">Önkoşullar ve hello yükleme işlemi, onun bir fikir tooread hello SAP NetWeaver yükleme dikkatle kılavuzları hakkında bilgi için.</span><span class="sxs-lookup"><span data-stu-id="6639f-138">For prerequisites and information about hello installation process, it's a good idea tooread hello SAP NetWeaver installation guides carefully.</span></span> <span data-ttu-id="6639f-139">Bu makalede yalnızca Azure sanal makineler ile kullanabileceğiniz SAP NetWeaver tabanlı sistemler için belirli görevler yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="6639f-139">This article covers only specific tasks for SAP NetWeaver-based systems that you can use with Azure Virtual Machines.</span></span>
>
>

<span data-ttu-id="6639f-140">Bu SAP Notlar SAP Azure içinde ilgili toohello konu şunlardır:</span><span class="sxs-lookup"><span data-stu-id="6639f-140">These SAP Notes are related toohello topic of SAP in Azure:</span></span>

| <span data-ttu-id="6639f-141">Not numarası</span><span class="sxs-lookup"><span data-stu-id="6639f-141">Note number</span></span> | <span data-ttu-id="6639f-142">Başlık</span><span class="sxs-lookup"><span data-stu-id="6639f-142">Title</span></span> |
| --- | --- |
| <span data-ttu-id="6639f-143">[1928533]</span><span class="sxs-lookup"><span data-stu-id="6639f-143">[1928533]</span></span> |<span data-ttu-id="6639f-144">Azure üzerinde SAP uygulamaları: desteklenen ürünler ve boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="6639f-144">SAP Applications on Azure: Supported Products and Sizing</span></span> |
| <span data-ttu-id="6639f-145">[2015553]</span><span class="sxs-lookup"><span data-stu-id="6639f-145">[2015553]</span></span> |<span data-ttu-id="6639f-146">Microsoft Azure üzerinde SAP: Destek önkoşulları</span><span class="sxs-lookup"><span data-stu-id="6639f-146">SAP on Microsoft Azure: Support Prerequisites</span></span> |
| <span data-ttu-id="6639f-147">[1999351]</span><span class="sxs-lookup"><span data-stu-id="6639f-147">[1999351]</span></span> |<span data-ttu-id="6639f-148">Azure için SAP izleme Gelişmiş</span><span class="sxs-lookup"><span data-stu-id="6639f-148">Enhanced Azure Monitoring for SAP</span></span> |
| <span data-ttu-id="6639f-149">[2178632]</span><span class="sxs-lookup"><span data-stu-id="6639f-149">[2178632]</span></span> |<span data-ttu-id="6639f-150">Microsoft Azure üzerinde SAP için ölçümleri izleme anahtarı</span><span class="sxs-lookup"><span data-stu-id="6639f-150">Key Monitoring Metrics for SAP on Microsoft Azure</span></span> |
| <span data-ttu-id="6639f-151">[1999351]</span><span class="sxs-lookup"><span data-stu-id="6639f-151">[1999351]</span></span> |<span data-ttu-id="6639f-152">Windows sanallaştırma: İzleme Gelişmiş</span><span class="sxs-lookup"><span data-stu-id="6639f-152">Virtualization on Windows: Enhanced Monitoring</span></span> |
| <span data-ttu-id="6639f-153">[2243692]</span><span class="sxs-lookup"><span data-stu-id="6639f-153">[2243692]</span></span> |<span data-ttu-id="6639f-154">SAP DBMS örneği için Azure Premium SSD depolama kullanımı</span><span class="sxs-lookup"><span data-stu-id="6639f-154">Use of Azure Premium SSD Storage for SAP DBMS Instance</span></span> |

<span data-ttu-id="6639f-155">Merhaba hakkında daha fazla bilgi [Azure abonelikleri sınırlamaları][azure-subscription-service-limits-subscription]genel varsayılan sınırlamalar ve en fazla sınırlamalar dahil olmak üzere.</span><span class="sxs-lookup"><span data-stu-id="6639f-155">Learn more about hello [limitations of Azure subscriptions][azure-subscription-service-limits-subscription], including general default limitations and maximum limitations.</span></span>

## <span data-ttu-id="6639f-156"><a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>Yüksek kullanılabilirlik SAP hello Azure Klasik dağıtım modeli ve Azure Resource Manager ile</span><span class="sxs-lookup"><span data-stu-id="6639f-156"><a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>High-availability SAP with Azure Resource Manager vs. hello Azure classic deployment model</span></span>
<span data-ttu-id="6639f-157">Hello Azure Resource Manager ve Azure Klasik dağıtım modelleri alanları aşağıdaki hello farklı durum vardır:</span><span class="sxs-lookup"><span data-stu-id="6639f-157">hello Azure Resource Manager and Azure classic deployment models are different in hello following areas:</span></span>

- <span data-ttu-id="6639f-158">Kaynak grupları</span><span class="sxs-lookup"><span data-stu-id="6639f-158">Resource groups</span></span>
- <span data-ttu-id="6639f-159">Azure iç yük dengeleyici bağımlılığını hello Azure kaynak grubu</span><span class="sxs-lookup"><span data-stu-id="6639f-159">Azure internal load balancer dependency on hello Azure resource group</span></span>
- <span data-ttu-id="6639f-160">SAP çoklu SID senaryolar için destek</span><span class="sxs-lookup"><span data-stu-id="6639f-160">Support for SAP multi-SID scenarios</span></span>

### <span data-ttu-id="6639f-161"><a name="f76af273-1993-4d83-b12d-65deeae23686"></a>Kaynak grupları</span><span class="sxs-lookup"><span data-stu-id="6639f-161"><a name="f76af273-1993-4d83-b12d-65deeae23686"></a> Resource groups</span></span>
<span data-ttu-id="6639f-162">Azure Kaynak Yöneticisi'nde, kaynak grupları toomanage tüm hello uygulama kaynakları Azure aboneliğinizde kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6639f-162">In Azure Resource Manager, you can use resource groups toomanage all hello application resources in your Azure subscription.</span></span> <span data-ttu-id="6639f-163">Tüm kaynaklara sahip bir kaynak grubunda tümleşik bir yaklaşım hello aynı yaşam döngüsü.</span><span class="sxs-lookup"><span data-stu-id="6639f-163">An integrated approach, in a resource group, all resources have hello same life cycle.</span></span> <span data-ttu-id="6639f-164">Tüm kaynaklar hello aynı örneğin, oluşturulan zaman ve bunların hello silinir aynı anda.</span><span class="sxs-lookup"><span data-stu-id="6639f-164">For example, all resources are created at hello same time and they are deleted at hello same time.</span></span> <span data-ttu-id="6639f-165">[Kaynak grupları](../../../azure-resource-manager/resource-group-overview.md#resource-groups) hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="6639f-165">Learn more about [resource groups](../../../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>

### <span data-ttu-id="6639f-166"><a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a>Azure iç yük dengeleyici bağımlılığını hello Azure kaynak grubu</span><span class="sxs-lookup"><span data-stu-id="6639f-166"><a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a> Azure internal load balancer dependency on hello Azure resource group</span></span>

<span data-ttu-id="6639f-167">Hello Azure Klasik dağıtım modelinde hello Azure iç yük dengeleyici (Azure Yük Dengeleyici Hizmeti) ile Merhaba bulut hizmeti grubu arasında bir bağımlılık yoktur.</span><span class="sxs-lookup"><span data-stu-id="6639f-167">In hello Azure classic deployment model, there is a dependency between hello Azure internal load balancer (Azure Load Balancer service) and hello cloud service group.</span></span> <span data-ttu-id="6639f-168">Her iç yük dengeleyici bir bulut hizmeti grubu olması gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="6639f-168">Every internal load balancer needs one cloud service group.</span></span>

<span data-ttu-id="6639f-169">Azure Kaynak Yöneticisi'nde, bir Azure kaynak grubu toouse Azure yük dengeleyici gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="6639f-169">In Azure Resource Manager, you don't need an Azure resource group toouse Azure Load Balancer.</span></span> <span data-ttu-id="6639f-170">Merhaba daha basit ve daha esnek ortamıdır.</span><span class="sxs-lookup"><span data-stu-id="6639f-170">hello environment is simpler and more flexible.</span></span>

### <a name="support-for-sap-multi-sid-scenarios"></a><span data-ttu-id="6639f-171">SAP çoklu SID senaryolar için destek</span><span class="sxs-lookup"><span data-stu-id="6639f-171">Support for SAP multi-SID scenarios</span></span>

<span data-ttu-id="6639f-172">Azure Kaynak Yöneticisi'nde, birden çok SAP sistem tanımlayıcısı (SID) ASCS/SCS örnekleri bir küme içinde yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6639f-172">In Azure Resource Manager, you can install multiple SAP system identifier (SID) ASCS/SCS instances in one cluster.</span></span> <span data-ttu-id="6639f-173">Çoklu SID örnekleri her Azure iç yük dengeleyici için birden fazla IP adresine yönelik destek nedeniyle mümkündür.</span><span class="sxs-lookup"><span data-stu-id="6639f-173">Multi-SID instances are possible because of support for multiple IP addresses for each Azure internal load balancer.</span></span>

<span data-ttu-id="6639f-174">toouse Azure Klasik dağıtım modeli Merhaba, açıklanan hello yordamları izleyin [SAP NetWeaver azure'da: SIOS DataKeeper ile azure'da Windows Server Yük Devretme Kümelemesi kullanarak SAP ASCS/SCS kümeleme örneklerini](http://go.microsoft.com/fwlink/?LinkId=613056).</span><span class="sxs-lookup"><span data-stu-id="6639f-174">toouse hello Azure classic deployment model, follow hello procedures described in [SAP NetWeaver in Azure: Clustering SAP ASCS/SCS instances by using Windows Server Failover Clustering in Azure with SIOS DataKeeper](http://go.microsoft.com/fwlink/?LinkId=613056).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6639f-175">SAP yüklemeleri için hello Azure Resource Manager dağıtım modeli kullanmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="6639f-175">We strongly recommend that you use hello Azure Resource Manager deployment model for your SAP installations.</span></span> <span data-ttu-id="6639f-176">Merhaba Klasik dağıtım modelinde bulunmayan birçok avantaj sunar.</span><span class="sxs-lookup"><span data-stu-id="6639f-176">It offers many benefits that are not available in hello classic deployment model.</span></span> <span data-ttu-id="6639f-177">Azure hakkında daha fazla bilgi [dağıtım modellerini][virtual-machines-azure-resource-manager-architecture-benefits-arm].</span><span class="sxs-lookup"><span data-stu-id="6639f-177">Learn more about Azure [deployment models][virtual-machines-azure-resource-manager-architecture-benefits-arm].</span></span>   
>
>

## <span data-ttu-id="6639f-178"><a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a>Windows Server Yük Devretme Kümelemesi</span><span class="sxs-lookup"><span data-stu-id="6639f-178"><a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a> Windows Server Failover Clustering</span></span>
<span data-ttu-id="6639f-179">Windows Server Yük Devretme Kümelemesi hello yüksek kullanılabilirlik SAP ASCS/SCS yükleme ve Windows'da DBMS temelini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6639f-179">Windows Server Failover Clustering is hello foundation of a high-availability SAP ASCS/SCS installation and DBMS in Windows.</span></span>

<span data-ttu-id="6639f-180">Bir yük devretme kümesi, uygulamaların ve hizmetlerin kullanılabilirliğini tooincrease hello birlikte çalışan 1 + n bağımsız sunucular (düğümler) grubudur.</span><span class="sxs-lookup"><span data-stu-id="6639f-180">A failover cluster is a group of 1+n independent servers (nodes) that work together tooincrease hello availability of applications and services.</span></span> <span data-ttu-id="6639f-181">Bir düğüm hatası oluşursa, Windows Server Yük Devretme Kümelemesi hello sayısı bir sağlıklı korurken oluşabilecek hesaplar küme tooprovide uygulamalar ve hizmetler.</span><span class="sxs-lookup"><span data-stu-id="6639f-181">If a node failure occurs, Windows Server Failover Clustering calculates hello number of failures that can occur while maintaining a healthy cluster tooprovide applications and services.</span></span> <span data-ttu-id="6639f-182">Farklı bir çekirdek modu tooachieve Yük Devretme Kümelemesi seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6639f-182">You can choose from different quorum modes tooachieve failover clustering.</span></span>

### <span data-ttu-id="6639f-183"><a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a>Çekirdek modu</span><span class="sxs-lookup"><span data-stu-id="6639f-183"><a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a> Quorum modes</span></span>
<span data-ttu-id="6639f-184">Windows Server Yük Devretme Kümelemesi kullanırken dört çekirdek modlarından seçim yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6639f-184">You can choose from four quorum modes when you use Windows Server Failover Clustering:</span></span>

* <span data-ttu-id="6639f-185">**Düğüm çoğunluğu**.</span><span class="sxs-lookup"><span data-stu-id="6639f-185">**Node Majority**.</span></span> <span data-ttu-id="6639f-186">Merhaba kümedeki her düğüme oy kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="6639f-186">Each node of hello cluster can vote.</span></span> <span data-ttu-id="6639f-187">Küme işlevleriyle yalnızca Çoğunluk oyu, diğer bir deyişle, yarısından fazlası hello oyları ile Merhaba.</span><span class="sxs-lookup"><span data-stu-id="6639f-187">hello cluster functions only with a majority of votes, that is, with more than half hello votes.</span></span> <span data-ttu-id="6639f-188">Bu seçenek eşit sayıda düğüme sahip kümeler için önerilir.</span><span class="sxs-lookup"><span data-stu-id="6639f-188">We recommend this option for clusters that have an uneven number of nodes.</span></span> <span data-ttu-id="6639f-189">Örneğin, üç yedi düğümlü bir küme düğümünde başarısız olabilir ve hello küme durağan Çoğunluk erişir ve toorun devam eder.</span><span class="sxs-lookup"><span data-stu-id="6639f-189">For example, three nodes in a seven-node cluster can fail, and hello cluster stills achieves a majority and continues toorun.</span></span>  
* <span data-ttu-id="6639f-190">**Düğüm ve Disk Çoğunluğu**.</span><span class="sxs-lookup"><span data-stu-id="6639f-190">**Node and Disk Majority**.</span></span> <span data-ttu-id="6639f-191">Her düğüm ve hello küme depolama atanmış bir disk (bir disk tanığı) ne zaman kullanılabilir olduğunu ve iletişim oy kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="6639f-191">Each node and a designated disk (a disk witness) in hello cluster storage can vote when they are available and in communication.</span></span> <span data-ttu-id="6639f-192">Merhaba küme işlevleriyle yalnızca hello çoğunu oylarının, diğer bir deyişle, yarısından fazlası hello oyları ile.</span><span class="sxs-lookup"><span data-stu-id="6639f-192">hello cluster functions only with a majority of hello votes, that is, with more than half hello votes.</span></span> <span data-ttu-id="6639f-193">Bu mod, bir küme ortamında düğümlerinin çift sayıda mantıklıdır.</span><span class="sxs-lookup"><span data-stu-id="6639f-193">This mode makes sense in a cluster environment with an even number of nodes.</span></span> <span data-ttu-id="6639f-194">Yarı hello düğümler ve hello disk çevrimiçi hello küme sağlam durumda kalır.</span><span class="sxs-lookup"><span data-stu-id="6639f-194">If half hello nodes and hello disk are online, hello cluster remains in a healthy state.</span></span>
* <span data-ttu-id="6639f-195">**Düğüm ve dosya paylaşımı çoğunluğu**.</span><span class="sxs-lookup"><span data-stu-id="6639f-195">**Node and File Share Majority**.</span></span> <span data-ttu-id="6639f-196">Yönetici hello bir dosya paylaşımı (dosya paylaşım tanığı) oluşturur her düğüm artı, hello düğüm ve dosya paylaşımı kullanılabilir ve iletişimde oy kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="6639f-196">Each node plus a designated file share (a file share witness) that hello administrator creates can vote, regardless of whether hello nodes and file share are available and in communication.</span></span> <span data-ttu-id="6639f-197">Merhaba küme işlevleriyle yalnızca hello çoğunu oylarının, diğer bir deyişle, yarısından fazlası hello oyları ile.</span><span class="sxs-lookup"><span data-stu-id="6639f-197">hello cluster functions only with a majority of hello votes, that is, with more than half hello votes.</span></span> <span data-ttu-id="6639f-198">Bu mod, bir küme ortamında düğümlerinin çift sayıda mantıklıdır.</span><span class="sxs-lookup"><span data-stu-id="6639f-198">This mode makes sense in a cluster environment with an even number of nodes.</span></span> <span data-ttu-id="6639f-199">Benzer toohello düğüm ve Disk Çoğunluğu modu olan, ancak Tanık diski yerine bir Tanık dosya paylaşımı kullanır.</span><span class="sxs-lookup"><span data-stu-id="6639f-199">It's similar toohello Node and Disk Majority mode, but it uses a witness file share instead of a witness disk.</span></span> <span data-ttu-id="6639f-200">Bu mod kolay tooimplement bağlıdır, ancak hello dosyasını paylaşırsanız, kendisini yüksek oranda kullanılabilir değil, tek bir hata noktası olabilir.</span><span class="sxs-lookup"><span data-stu-id="6639f-200">This mode is easy tooimplement, but if hello file share itself is not highly available, it might become a single point of failure.</span></span>
* <span data-ttu-id="6639f-201">**Çoğunluk yok: Yalnızca Disk**.</span><span class="sxs-lookup"><span data-stu-id="6639f-201">**No Majority: Disk Only**.</span></span> <span data-ttu-id="6639f-202">bir düğüm kullanılabilir ve belirli bir disk hello küme depolama ile iletişim ise hello küme çekirdeği vardır.</span><span class="sxs-lookup"><span data-stu-id="6639f-202">hello cluster has a quorum if one node is available and in communication with a specific disk in hello cluster storage.</span></span> <span data-ttu-id="6639f-203">Ayrıca, disk ile iletişimi yalnızca hello düğümlerini hello kümeye katılabilir.</span><span class="sxs-lookup"><span data-stu-id="6639f-203">Only hello nodes that also are in communication with that disk can join hello cluster.</span></span> <span data-ttu-id="6639f-204">Bu mod kullanmamanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="6639f-204">We recommend that you do not use this mode.</span></span>
 

## <span data-ttu-id="6639f-205"><a name="fdfee875-6e66-483a-a343-14bbaee33275"></a>Şirket içi Windows Server Yük devretme</span><span class="sxs-lookup"><span data-stu-id="6639f-205"><a name="fdfee875-6e66-483a-a343-14bbaee33275"></a> Windows Server Failover Clustering on-premises</span></span>
<span data-ttu-id="6639f-206">Şekil 1 iki düğümden oluşan bir küme gösterir.</span><span class="sxs-lookup"><span data-stu-id="6639f-206">Figure 1 shows a cluster of two nodes.</span></span> <span data-ttu-id="6639f-207">Merhaba, hello düğümler arasında ağ bağlantısı başarısız olur ve her iki düğüm kalması ve çalıştıran, bir çekirdek disk veya dosya paylaşımı hangi düğümün tooprovide hello kümenin uygulamaları ve Hizmetleri devam edecek belirler.</span><span class="sxs-lookup"><span data-stu-id="6639f-207">If hello network connection between hello nodes fails and both nodes stay up and running, a quorum disk or file share determines which node will continue tooprovide hello cluster's applications and services.</span></span> <span data-ttu-id="6639f-208">erişim toohello çekirdek diski veya dosya paylaşımı hello düğüm Hizmetleri devam etmenizi sağlar hello olandır.</span><span class="sxs-lookup"><span data-stu-id="6639f-208">hello node that has access toohello quorum disk or file share is hello node that ensures that services continue.</span></span>

<span data-ttu-id="6639f-209">Bu örnek iki düğümlü bir küme kullandığından, hello düğüm ve dosya paylaşımı çoğunluğu çekirdek modu kullanın.</span><span class="sxs-lookup"><span data-stu-id="6639f-209">Because this example uses a two-node cluster, we use hello Node and File Share Majority quorum mode.</span></span> <span data-ttu-id="6639f-210">Merhaba düğüm ve Disk Çoğunluğu geçerli bir seçenek de olur.</span><span class="sxs-lookup"><span data-stu-id="6639f-210">hello Node and Disk Majority also is a valid option.</span></span> <span data-ttu-id="6639f-211">Bir üretim ortamında, bir çekirdek disk kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="6639f-211">In a production environment, we recommend that you use a quorum disk.</span></span> <span data-ttu-id="6639f-212">Ağ ve depolama sistemi teknolojisi toomake kullanabilirsiniz, yüksek oranda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="6639f-212">You can use network and storage system technology toomake it highly available.</span></span>

![Şekil 1: Bir Windows Server Yük Devretme Kümelemesi yapılandırma için SAP ASCS/SCS Azure örneği][sap-ha-guide-figure-1000]

<span data-ttu-id="6639f-214">_**Şekil 1:** bir Windows Server Yük Devretme Kümelemesi yapılandırma için SAP ASCS/SCS Azure örneği_</span><span class="sxs-lookup"><span data-stu-id="6639f-214">_**Figure 1:** Example of a Windows Server Failover Clustering configuration for SAP ASCS/SCS in Azure_</span></span>

### <span data-ttu-id="6639f-215"><a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a>Paylaşılan depolama alanı</span><span class="sxs-lookup"><span data-stu-id="6639f-215"><a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a> Shared storage</span></span>
<span data-ttu-id="6639f-216">Şekil 1 iki düğümlü paylaşılan depolama kümesi ayrıca gösterir.</span><span class="sxs-lookup"><span data-stu-id="6639f-216">Figure 1 also shows a two-node shared storage cluster.</span></span> <span data-ttu-id="6639f-217">Bir şirket içi paylaşılan depolama Küme Paylaşılan depolama hello kümedeki tüm düğümlerin algıla.</span><span class="sxs-lookup"><span data-stu-id="6639f-217">In an on-premises shared storage cluster, all nodes in hello cluster detect shared storage.</span></span> <span data-ttu-id="6639f-218">Kilitleme mekanizması hello veri bozulmaya karşı korur.</span><span class="sxs-lookup"><span data-stu-id="6639f-218">A locking mechanism protects hello data from corruption.</span></span> <span data-ttu-id="6639f-219">Tüm düğümler, başka bir düğüm başarısız olursa algılayabilir.</span><span class="sxs-lookup"><span data-stu-id="6639f-219">All nodes can detect if another node fails.</span></span> <span data-ttu-id="6639f-220">Bir düğüm başarısız olursa, hello kalan düğümü hello depolama kaynakları aittir ve hizmetlerin kullanılabilirliğini hello sağlar.</span><span class="sxs-lookup"><span data-stu-id="6639f-220">If one node fails, hello remaining node takes ownership of hello storage resources and ensures hello availability of services.</span></span>

> [!NOTE]
> <span data-ttu-id="6639f-221">SQL Server ile gibi bazı DBMS uygulamalarla yüksek kullanılabilirlik için Paylaşılan diskleri gerekmez.</span><span class="sxs-lookup"><span data-stu-id="6639f-221">You don't need shared disks for high availability with some DBMS applications, like with SQL Server.</span></span> <span data-ttu-id="6639f-222">SQL Server Always On hello yerel bir küme düğümü toohello yerel disk başka bir küme düğümünün diskten DBMS veri ve günlük dosyalarını çoğaltır.</span><span class="sxs-lookup"><span data-stu-id="6639f-222">SQL Server Always On replicates DBMS data and log files from hello local disk of one cluster node toohello local disk of another cluster node.</span></span> <span data-ttu-id="6639f-223">Bu durumda, paylaşılan bir diskin hello Windows Küme yapılandırması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="6639f-223">In that case, hello Windows cluster configuration doesn't need a shared disk.</span></span>
>
>

### <span data-ttu-id="6639f-224"><a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a>Ağ ve ad çözümlemesi</span><span class="sxs-lookup"><span data-stu-id="6639f-224"><a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a> Networking and name resolution</span></span>
<span data-ttu-id="6639f-225">İstemci bilgisayarları hello küme DNS sunucusu sağlar, hello bir sanal IP adresi ve bir sanal ana bilgisayar adı üzerinden ulaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6639f-225">Client computers reach hello cluster over a virtual IP address and a virtual host name that hello DNS server provides.</span></span> <span data-ttu-id="6639f-226">Merhaba içi düğümleri ve hello DNS sunucusu birden çok IP adresi işleyebilir.</span><span class="sxs-lookup"><span data-stu-id="6639f-226">hello on-premises nodes and hello DNS server can handle multiple IP addresses.</span></span>

<span data-ttu-id="6639f-227">Tipik bir kurulumunda iki veya daha fazla ağ bağlantıları kullanın:</span><span class="sxs-lookup"><span data-stu-id="6639f-227">In a typical setup, you use two or more network connections:</span></span>

* <span data-ttu-id="6639f-228">Adanmış bağlantı toohello depolama</span><span class="sxs-lookup"><span data-stu-id="6639f-228">A dedicated connection toohello storage</span></span>
* <span data-ttu-id="6639f-229">Merhaba sinyal için bir küme iç ağ bağlantısı</span><span class="sxs-lookup"><span data-stu-id="6639f-229">A cluster-internal network connection for hello heartbeat</span></span>
* <span data-ttu-id="6639f-230">Genel bir ağ istemcileri tooconnect toohello küme kullanın</span><span class="sxs-lookup"><span data-stu-id="6639f-230">A public network that clients use tooconnect toohello cluster</span></span>

## <span data-ttu-id="6639f-231"><a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a>Azure'da Windows Server Yük devretme</span><span class="sxs-lookup"><span data-stu-id="6639f-231"><a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a> Windows Server Failover Clustering in Azure</span></span>
<span data-ttu-id="6639f-232">Toobare metal veya özel bulut dağıtımları karşılaştırıldığında Azure sanal makineleri ek adımlar tooconfigure Windows Server Yük Devretme Kümelemesi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="6639f-232">Compared toobare metal or private cloud deployments, Azure Virtual Machines requires additional steps tooconfigure Windows Server Failover Clustering.</span></span> <span data-ttu-id="6639f-233">Paylaşılan bir küme diski derlerken hello SAP ASCS/SCS örneği için birkaç IP adresleri ve sanal ana bilgisayar adları tooset gerekir.</span><span class="sxs-lookup"><span data-stu-id="6639f-233">When you build a shared cluster disk, you need tooset several IP addresses and virtual host names for hello SAP ASCS/SCS instance.</span></span>

<span data-ttu-id="6639f-234">Bu makalede, anahtar kavramlar açıklanmaktadır ve ek adımlar gerekli toobuild bir SAP yüksek kullanılabilirlik merkezi Hizmetleri küme azure'da hello.</span><span class="sxs-lookup"><span data-stu-id="6639f-234">In this article, we discuss key concepts and hello additional steps required toobuild an SAP high-availability central services cluster in Azure.</span></span> <span data-ttu-id="6639f-235">Nasıl tooset hello üçüncü taraf aracı SIOS DataKeeper ayarlama ve nasıl tooconfigure hello Azure iç yük dengeleyici gösteriyoruz.</span><span class="sxs-lookup"><span data-stu-id="6639f-235">We show you how tooset up hello third-party tool SIOS DataKeeper, and how tooconfigure hello Azure internal load balancer.</span></span> <span data-ttu-id="6639f-236">Bu araçlar toocreate Windows Yük devretme, dosya paylaşım tanığı Azure ile kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6639f-236">You can use these tools toocreate a Windows failover cluster with a file share witness in Azure.</span></span>

![Şekil 2: Windows Server Yük devretme kümeleme yapılandırmasında Azure olmayan paylaşılan bir disk][sap-ha-guide-figure-1001]

<span data-ttu-id="6639f-238">_**Şekil 2:** Windows Server Yük devretme kümeleme yapılandırmasında Azure olmayan paylaşılan bir disk_</span><span class="sxs-lookup"><span data-stu-id="6639f-238">_**Figure 2:** Windows Server Failover Clustering configuration in Azure without a shared disk_</span></span>

### <span data-ttu-id="6639f-239"><a name="1a464091-922b-48d7-9d08-7cecf757f341"></a>Paylaşılan disk Azure ile SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="6639f-239"><a name="1a464091-922b-48d7-9d08-7cecf757f341"></a> Shared disk in Azure with SIOS DataKeeper</span></span>
<span data-ttu-id="6639f-240">Yüksek kullanılabilirlik SAP ASCS/SCS örneği için paylaşılan depolama küme.</span><span class="sxs-lookup"><span data-stu-id="6639f-240">You need cluster shared storage for a high-availability SAP ASCS/SCS instance.</span></span> <span data-ttu-id="6639f-241">Eylül 2016 ' Azure paylaşılan depolama alanı, sunmaz gibi toocreate bir paylaşılan depolama kümesi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6639f-241">As of September 2016, Azure doesn't offer shared storage that you can use toocreate a shared storage cluster.</span></span> <span data-ttu-id="6639f-242">Üçüncü taraf yazılım SIOS DataKeeper Cluster Edition toocreate Küme Paylaşılan depolama taklit eden bir yansıtılmış depolama kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6639f-242">You can use third-party software SIOS DataKeeper Cluster Edition toocreate a mirrored storage that simulates cluster shared storage.</span></span> <span data-ttu-id="6639f-243">gerçek zamanlı zaman uyumlu veri çoğaltma Hello SIOS çözümü sağlar.</span><span class="sxs-lookup"><span data-stu-id="6639f-243">hello SIOS solution provides real-time synchronous data replication.</span></span> <span data-ttu-id="6639f-244">Bu küme için paylaşılan disk kaynağı nasıl oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6639f-244">This is how you can create a shared disk resource for a cluster:</span></span>

1. <span data-ttu-id="6639f-245">Ek Azure sanal sabit disk (VHD) tooeach hello sanal makineleri (VM'ler) bir Windows küme yapılandırmasında ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6639f-245">Attach an additional Azure virtual hard disk (VHD) tooeach of hello virtual machines (VMs) in a Windows cluster configuration.</span></span>
2. <span data-ttu-id="6639f-246">SIOS DataKeeper Cluster Edition her iki sanal makine düğümde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6639f-246">Run SIOS DataKeeper Cluster Edition on both virtual machine nodes.</span></span>
3. <span data-ttu-id="6639f-247">Merhaba ek bağlı VHD birimden hello kaynak sanal makine toohello ek bağlı VHD birim hello hedef sanal makinenin Merhaba içeriğine yansıtan SIOS DataKeeper Cluster Edition yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="6639f-247">Configure SIOS DataKeeper Cluster Edition so that it mirrors hello content of hello additional VHD attached volume from hello source virtual machine toohello additional VHD attached volume of hello target virtual machine.</span></span> <span data-ttu-id="6639f-248">SIOS DataKeeper hello kaynak ve hedef yerel birimleri soyutlar ve bunları tooWindows sunucu Yük Devretme Kümelemesi bir paylaşılan disk olarak sunar.</span><span class="sxs-lookup"><span data-stu-id="6639f-248">SIOS DataKeeper abstracts hello source and target local volumes, and then presents them tooWindows Server Failover Clustering as one shared disk.</span></span>

<span data-ttu-id="6639f-249">Hakkında daha fazla bilgi almak [SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/).</span><span class="sxs-lookup"><span data-stu-id="6639f-249">Get more information about [SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/).</span></span>

![Şekil 3: Windows Server Yük devretme kümeleme yapılandırmasında SIOS DataKeeper ile Azure][sap-ha-guide-figure-1002]

<span data-ttu-id="6639f-251">_**Şekil 3:** SIOS DataKeeper ile azure'da Windows Server Yük Devretme Kümelemesi yapılandırma_</span><span class="sxs-lookup"><span data-stu-id="6639f-251">_**Figure 3:** Windows Server Failover Clustering configuration in Azure with SIOS DataKeeper_</span></span>

> [!NOTE]
> <span data-ttu-id="6639f-252">SQL Server gibi bazı DBMS ürünleri ile yüksek kullanılabilirlik için Paylaşılan diskleri gerekmez.</span><span class="sxs-lookup"><span data-stu-id="6639f-252">You don't need shared disks for high availability with some DBMS products, like SQL Server.</span></span> <span data-ttu-id="6639f-253">SQL Server Always On hello yerel bir küme düğümü toohello yerel disk başka bir küme düğümünün diskten DBMS veri ve günlük dosyalarını çoğaltır.</span><span class="sxs-lookup"><span data-stu-id="6639f-253">SQL Server Always On replicates DBMS data and log files from hello local disk of one cluster node toohello local disk of another cluster node.</span></span> <span data-ttu-id="6639f-254">Bu durumda, paylaşılan bir diskin hello Windows Küme yapılandırması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="6639f-254">In this case, hello Windows cluster configuration doesn't need a shared disk.</span></span>
>
>

### <span data-ttu-id="6639f-255"><a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a>Azure ad çözümleme</span><span class="sxs-lookup"><span data-stu-id="6639f-255"><a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a> Name resolution in Azure</span></span>
<span data-ttu-id="6639f-256">Hello Azure bulut platformu hello seçeneği tooconfigure sanal IP adresleri, kayan IP adresleri gibi sunmuyor.</span><span class="sxs-lookup"><span data-stu-id="6639f-256">hello Azure cloud platform doesn't offer hello option tooconfigure virtual IP addresses, such as floating IP addresses.</span></span> <span data-ttu-id="6639f-257">Bir sanal IP adresi tooreach hello küme kaynağını hello bulutta bir alternatif çözüm tooset gerekir.</span><span class="sxs-lookup"><span data-stu-id="6639f-257">You need an alternative solution tooset up a virtual IP address tooreach hello cluster resource in hello cloud.</span></span>
<span data-ttu-id="6639f-258">Azure hello Azure Yük Dengeleyici Hizmeti bir iç yük dengeleyici sahiptir.</span><span class="sxs-lookup"><span data-stu-id="6639f-258">Azure has an internal load balancer in hello Azure Load Balancer service.</span></span> <span data-ttu-id="6639f-259">Merhaba iç yük dengeleyici ile istemcileri hello küme hello küme sanal IP adresi ulaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6639f-259">With hello internal load balancer, clients reach hello cluster over hello cluster virtual IP address.</span></span>
<span data-ttu-id="6639f-260">Toodeploy hello iç yük dengeleyici hello küme düğümleri içeren hello kaynak grubundaki gerekir.</span><span class="sxs-lookup"><span data-stu-id="6639f-260">You need toodeploy hello internal load balancer in hello resource group that contains hello cluster nodes.</span></span> <span data-ttu-id="6639f-261">Ardından, kuralları ile Merhaba araştırma hello iç yük dengeleyici bağlantı noktaları iletme tüm gerekli bağlantı noktası yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="6639f-261">Then, configure all necessary port forwarding rules with hello probe ports of hello internal load balancer.</span></span>
<span data-ttu-id="6639f-262">Merhaba istemcileri hello sanal ana bilgisayar adını bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="6639f-262">hello clients can connect via hello virtual host name.</span></span> <span data-ttu-id="6639f-263">Merhaba DNS sunucusu hello küme IP adresi ve hello kümesinin etkin düğümü toohello iletme hello iç yük dengeleyici tanıtıcıları bağlantı noktası çözümler.</span><span class="sxs-lookup"><span data-stu-id="6639f-263">hello DNS server resolves hello cluster IP address, and hello internal load balancer handles port forwarding toohello active node of hello cluster.</span></span>

## <span data-ttu-id="6639f-264"><a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a>SAP NetWeaver yüksek kullanılabilirlik Azure altyapısı olarak-hizmet (Iaas)</span><span class="sxs-lookup"><span data-stu-id="6639f-264"><a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a> SAP NetWeaver high availability in Azure Infrastructure-as-a-Service (IaaS)</span></span>
<span data-ttu-id="6639f-265">tooachieve SAP yazılım bileşenleri için ihtiyacınız tooprotect hello bileşenleri aşağıdaki gibi uygulama yüksek kullanılabilirlik, SAP:</span><span class="sxs-lookup"><span data-stu-id="6639f-265">tooachieve SAP application high availability, such as for SAP software components, you need tooprotect hello following components:</span></span>

* <span data-ttu-id="6639f-266">SAP uygulama sunucusu örneği</span><span class="sxs-lookup"><span data-stu-id="6639f-266">SAP Application Server instance</span></span>
* <span data-ttu-id="6639f-267">SAP ASCS/SCS örneği</span><span class="sxs-lookup"><span data-stu-id="6639f-267">SAP ASCS/SCS instance</span></span>
* <span data-ttu-id="6639f-268">DBMS sunucu</span><span class="sxs-lookup"><span data-stu-id="6639f-268">DBMS server</span></span>

<span data-ttu-id="6639f-269">Yüksek kullanılabilirlik senaryolarını SAP bileşenlerinde koruma hakkında daha fazla bilgi için bkz: [Azure sanal makineleri planlama ve uygulama SAP NetWeaver için](planning-guide.md).</span><span class="sxs-lookup"><span data-stu-id="6639f-269">For more information about protecting SAP components in high-availability scenarios, see [Azure Virtual Machines planning and implementation for SAP NetWeaver](planning-guide.md).</span></span>

### <span data-ttu-id="6639f-270"><a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a>Yüksek kullanılabilirlik SAP uygulama sunucusu</span><span class="sxs-lookup"><span data-stu-id="6639f-270"><a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a> High-availability SAP Application Server</span></span>
<span data-ttu-id="6639f-271">Belirli bir yüksek kullanılabilirlik çözümü hello SAP uygulama sunucusu ile iletişim örnekleri için genellikle gerekmez.</span><span class="sxs-lookup"><span data-stu-id="6639f-271">You usually don't need a specific high-availability solution for hello SAP Application Server and dialog instances.</span></span> <span data-ttu-id="6639f-272">Artıklık tarafından yüksek kullanılabilirlik elde etmek ve iletişim birden çok başka durumlarda, Azure sanal makineleri yapılandıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="6639f-272">You achieve high availability by redundancy, and you'll configure multiple dialog instances in different instances of Azure Virtual Machines.</span></span> <span data-ttu-id="6639f-273">İki durumlarda, Azure sanal makinelerinde yüklü en az iki SAP uygulama örneğinin olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="6639f-273">You should have at least two SAP application instances installed in two instances of Azure Virtual Machines.</span></span>

![Şekil 4: Yüksek oranda kullanılabilirlik SAP uygulama sunucusu][sap-ha-guide-figure-2000]

<span data-ttu-id="6639f-275">_**Şekil 4:** yüksek kullanılabilirlik SAP uygulama sunucusu_</span><span class="sxs-lookup"><span data-stu-id="6639f-275">_**Figure 4:** High-availability SAP Application Server_</span></span>

<span data-ttu-id="6639f-276">Tüm sanal makinelerin konak SAP uygulama sunucusu örnekleri aynı Azure kullanılabilirlik kümesi hello yerleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6639f-276">You must place all virtual machines that host SAP Application Server instances in hello same Azure availability set.</span></span> <span data-ttu-id="6639f-277">Bir Azure kullanılabilirlik kümesi sağlar:</span><span class="sxs-lookup"><span data-stu-id="6639f-277">An Azure availability set ensures that:</span></span>

* <span data-ttu-id="6639f-278">Tüm sanal makineleri hello parçası olan aynı yükseltme etki alanı.</span><span class="sxs-lookup"><span data-stu-id="6639f-278">All virtual machines are part of hello same upgrade domain.</span></span> <span data-ttu-id="6639f-279">Bir yükseltme etki alanı gibi hello sanal makineleri hello güncelleştirilmemiş emin olur planlı bakım kapalı kalma süresi sırasında aynı anda.</span><span class="sxs-lookup"><span data-stu-id="6639f-279">An upgrade domain, for example, makes sure that hello virtual machines aren't updated at hello same time during planned maintenance downtime.</span></span>
* <span data-ttu-id="6639f-280">Tüm sanal makineleri hello parçası olan aynı hata etki alanı.</span><span class="sxs-lookup"><span data-stu-id="6639f-280">All virtual machines are part of hello same fault domain.</span></span> <span data-ttu-id="6639f-281">Hata etki alanı, örneğin, böylece hiç tek hata noktası hello tüm sanal makinelerin kullanılabilirliğini etkiler dağıtılan sanal makineler olduğundan emin olur.</span><span class="sxs-lookup"><span data-stu-id="6639f-281">A fault domain, for example, makes sure that virtual machines are deployed so that no single point of failure affects hello availability of all virtual machines.</span></span>

<span data-ttu-id="6639f-282">Hakkında daha fazla çok bilgi[hello sanal makinelerin kullanılabilirliğini yönetme][virtual-machines-manage-availability].</span><span class="sxs-lookup"><span data-stu-id="6639f-282">Learn more about how too[manage hello availability of virtual machines][virtual-machines-manage-availability].</span></span>

<span data-ttu-id="6639f-283">Hello Azure depolama hesabına olası tek hata noktası olduğundan, önemli toohave olan en az iki Azure depolama hesapları, en az iki sanal makineye dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="6639f-283">Because hello Azure storage account is a potential single point of failure, it's important toohave at least two Azure storage accounts, in which at least two virtual machines are distributed.</span></span> <span data-ttu-id="6639f-284">İdeal bir kurulumunda hello diskler, SAP iletişim örneği çalıştıran her bir sanal makinenin farklı depolama hesabında dağıtılması.</span><span class="sxs-lookup"><span data-stu-id="6639f-284">In an ideal setup, hello disks of each virtual machine that is running an SAP dialog instance would be deployed in a different storage account.</span></span>

### <span data-ttu-id="6639f-285"><a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a>Yüksek kullanılabilirlik SAP ASCS/SCS örneği</span><span class="sxs-lookup"><span data-stu-id="6639f-285"><a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a> High-availability SAP ASCS/SCS instance</span></span>
<span data-ttu-id="6639f-286">Şekil 5, yüksek kullanılabilirlik SAP ASCS/SCS örneğinin bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="6639f-286">Figure 5 is an example of a high-availability SAP ASCS/SCS instance.</span></span>

![Şekil 5: Yüksek oranda kullanılabilirlik SAP ASCS/SCS örneği][sap-ha-guide-figure-2001]

<span data-ttu-id="6639f-288">_**Şekil 5:** yüksek kullanılabilirlik SAP ASCS/SCS örneği_</span><span class="sxs-lookup"><span data-stu-id="6639f-288">_**Figure 5:** High-availability SAP ASCS/SCS instance_</span></span>

#### <span data-ttu-id="6639f-289"><a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a>Windows Server Yük Devretme Kümelemesi Azure ile yüksek kullanılabilirlik SAP ASCS/SCS örneği</span><span class="sxs-lookup"><span data-stu-id="6639f-289"><a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a> SAP ASCS/SCS instance high availability with Windows Server Failover Clustering in Azure</span></span>
<span data-ttu-id="6639f-290">Toobare metal veya özel bulut dağıtımları karşılaştırıldığında Azure sanal makineleri ek adımlar tooconfigure Windows Server Yük Devretme Kümelemesi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="6639f-290">Compared toobare metal or private cloud deployments, Azure Virtual Machines requires additional steps tooconfigure Windows Server Failover Clustering.</span></span> <span data-ttu-id="6639f-291">Windows Yük devretme toobuild, paylaşılan bir küme diski, birden fazla IP adresi, birçok sanal ana bilgisayar adlarını ve Azure iç yük dengeleyiciye SAP ASCS/SCS örneği kümeleme için gerekir.</span><span class="sxs-lookup"><span data-stu-id="6639f-291">toobuild a Windows failover cluster, you need a shared cluster disk, several IP addresses, several virtual host names, and an Azure internal load balancer for clustering an SAP ASCS/SCS instance.</span></span> <span data-ttu-id="6639f-292">Biz bu hello makalenin sonraki bölümlerinde daha ayrıntılı ele alınmıştır.</span><span class="sxs-lookup"><span data-stu-id="6639f-292">We discuss this in more detail later in hello article.</span></span>

![Şekil 6: Windows Server Yük Devretme Kümelemesi için SIOS DataKeeper kullanarak bir SAP ASCS/SCS yapılandırmasında Azure][sap-ha-guide-figure-1002]

<span data-ttu-id="6639f-294">_**Şekil 6:** Windows Server Yük Devretme Kümelemesi SIOS DataKeeper ile azure'da SAP ASCS/SCS yapılandırma_</span><span class="sxs-lookup"><span data-stu-id="6639f-294">_**Figure 6:** Windows Server Failover Clustering for an SAP ASCS/SCS configuration in Azure with SIOS DataKeeper_</span></span>

### <span data-ttu-id="6639f-295"><a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a>Yüksek kullanılabilirlik DBMS örneği</span><span class="sxs-lookup"><span data-stu-id="6639f-295"><a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a>High-availability DBMS instance</span></span>
<span data-ttu-id="6639f-296">Merhaba DBMS de tek bir iletişim noktası bir SAP içinde sistemidir.</span><span class="sxs-lookup"><span data-stu-id="6639f-296">hello DBMS also is a single point of contact in an SAP system.</span></span> <span data-ttu-id="6639f-297">Tooprotect gereken bir yüksek kullanılabilirlik çözümü kullanarak.</span><span class="sxs-lookup"><span data-stu-id="6639f-297">You need tooprotect it by using a high-availability solution.</span></span> <span data-ttu-id="6639f-298">Şekil 7, Azure'da bir SQL Server Always On yüksek kullanılabilirlik çözümü gösterir, Windows Server Yük Devretme Kümelemesi ile hello Azure iç yük dengeleyici.</span><span class="sxs-lookup"><span data-stu-id="6639f-298">Figure 7 shows a SQL Server Always On high-availability solution in Azure, with Windows Server Failover Clustering and hello Azure internal load balancer.</span></span> <span data-ttu-id="6639f-299">SQL Server Always On kendi DBMS çoğaltma kullanılarak DBMS veri ve günlük dosyalarını çoğaltır.</span><span class="sxs-lookup"><span data-stu-id="6639f-299">SQL Server Always On replicates DBMS data and log files by using its own DBMS replication.</span></span> <span data-ttu-id="6639f-300">Bu durumda, paylaşılan diskleri, hangi hello tüm kurulumu basitleştirir küme.</span><span class="sxs-lookup"><span data-stu-id="6639f-300">In this case, you don't need cluster shared disks, which simplifies hello entire setup.</span></span>

![Şekil 7: SQL Server Always On ile bir yüksek kullanılabilirlik SAP DBMS örneği][sap-ha-guide-figure-2003]

<span data-ttu-id="6639f-302">_**Şekil 7:** SQL Server Always On ile bir yüksek kullanılabilirlik SAP DBMS örneği_</span><span class="sxs-lookup"><span data-stu-id="6639f-302">_**Figure 7:** Example of a high-availability SAP DBMS, with SQL Server Always On_</span></span>

<span data-ttu-id="6639f-303">Hello Azure Resource Manager dağıtım modelini kullanarak Azure SQL Server Kümelemesi hakkında daha fazla bilgi için bu makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="6639f-303">For more information about clustering SQL Server in Azure by using hello Azure Resource Manager deployment model, see these articles:</span></span>

* <span data-ttu-id="6639f-304">[Always On kullanılabilirlik grubu Resource Manager kullanarak Azure sanal makinelerinde el ile yapılandırın.][virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]</span><span class="sxs-lookup"><span data-stu-id="6639f-304">[Configure Always On availability group in Azure Virtual Machines manually by using Resource Manager][virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]</span></span>
* <span data-ttu-id="6639f-305">[Azure'da Azure iç yük dengeleyiciye Always On kullanılabilirlik grubu için yapılandırın][virtual-machines-windows-portal-sql-alwayson-int-listener]</span><span class="sxs-lookup"><span data-stu-id="6639f-305">[Configure an Azure internal load balancer for an Always On availability group in Azure][virtual-machines-windows-portal-sql-alwayson-int-listener]</span></span>

## <span data-ttu-id="6639f-306"><a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a>Uçtan uca yüksek kullanılabilirlik dağıtım senaryoları</span><span class="sxs-lookup"><span data-stu-id="6639f-306"><a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a> End-to-end high-availability deployment scenarios</span></span>

### <a name="deployment-scenario-using-architectural-template-1"></a><span data-ttu-id="6639f-307">Mimari şablonu 1'i kullanarak dağıtım senaryosu</span><span class="sxs-lookup"><span data-stu-id="6639f-307">Deployment scenario using Architectural Template 1</span></span>

<span data-ttu-id="6639f-308">Şekil 8 için azure'da bir SAP NetWeaver yüksek kullanılabilirlik mimari örneği gösterilmiştir **bir** SAP sistem.</span><span class="sxs-lookup"><span data-stu-id="6639f-308">Figure 8 shows an example of an SAP NetWeaver high-availability architecture in Azure for **one** SAP system.</span></span> <span data-ttu-id="6639f-309">Bu senaryo aşağıdaki gibi kurun:</span><span class="sxs-lookup"><span data-stu-id="6639f-309">This scenario is set up as follows:</span></span>

- <span data-ttu-id="6639f-310">Tek bir adanmış küme hello SAP ASCS/SCS örneği için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6639f-310">One dedicated cluster is used for hello SAP ASCS/SCS instance.</span></span>
- <span data-ttu-id="6639f-311">Tek bir adanmış küme hello DBMS örneği için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6639f-311">One dedicated cluster is used for hello DBMS instance.</span></span>
- <span data-ttu-id="6639f-312">SAP uygulama sunucusu örnekleri kendi özel VM'ler dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="6639f-312">SAP Application Server instances are deployed in their own dedicated VMs.</span></span>

![Şekil 8: yüksek oranda kullanılabilirlik mimari şablonu, 1 ile ayrılmış küme ASCS/SCS ve DBMS için SAP][sap-ha-guide-figure-2004]

<span data-ttu-id="6639f-314">_**Şekil 8:** ASCS/SCS ve DBMS ayrılmış kümelerine şablonu 1 mimari yüksek kullanılabilirlik, SAP_</span><span class="sxs-lookup"><span data-stu-id="6639f-314">_**Figure 8:** SAP high-availability Architectural Template 1, dedicated clusters for ASCS/SCS and DBMS_</span></span>

### <a name="deployment-scenario-using-architectural-template-2"></a><span data-ttu-id="6639f-315">Mimari şablon 2 kullanarak dağıtım senaryosu</span><span class="sxs-lookup"><span data-stu-id="6639f-315">Deployment scenario using Architectural Template 2</span></span>

<span data-ttu-id="6639f-316">Şekil 9 için azure'da bir SAP NetWeaver yüksek kullanılabilirlik mimari örneği gösterir **bir** SAP sistem.</span><span class="sxs-lookup"><span data-stu-id="6639f-316">Figure 9 shows an example of an SAP NetWeaver high-availability architecture in Azure for **one** SAP system.</span></span> <span data-ttu-id="6639f-317">Bu senaryo aşağıdaki gibi kurun:</span><span class="sxs-lookup"><span data-stu-id="6639f-317">This scenario is set up as follows:</span></span>

- <span data-ttu-id="6639f-318">Ayrılmış bir küme için kullanıldığından **her ikisi de** SAP ASCS/SCS örneği ve DBMS hello hello.</span><span class="sxs-lookup"><span data-stu-id="6639f-318">One dedicated cluster is used for **both** hello SAP ASCS/SCS instance and hello DBMS.</span></span>
- <span data-ttu-id="6639f-319">SAP uygulama sunucusu örnekleri kendi özel VM'ler içinde dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="6639f-319">SAP Application Server instances are deployed in own dedicated VMs.</span></span>

![Şekil 9: yüksek oranda kullanılabilirlik mimari şablon 2 ile ayrılmış bir küme ASCS/SCS için ve ayrılmış bir küme DBMS için SAP][sap-ha-guide-figure-2005]

<span data-ttu-id="6639f-321">_**Şekil 9:** SAP yüksek kullanılabilirlik mimari şablon 2 ile ayrılmış bir küme ASCS/SCS için ve DBMS için ayrılmış bir küme_</span><span class="sxs-lookup"><span data-stu-id="6639f-321">_**Figure 9:** SAP high-availability Architectural Template 2, with a dedicated cluster for ASCS/SCS and a dedicated cluster for DBMS_</span></span>

### <a name="deployment-scenario-using-architectural-template-3"></a><span data-ttu-id="6639f-322">Mimari şablonu 3 kullanan dağıtım senaryosu</span><span class="sxs-lookup"><span data-stu-id="6639f-322">Deployment scenario using Architectural Template 3</span></span>

<span data-ttu-id="6639f-323">Şekil 10 için azure'da bir SAP NetWeaver yüksek kullanılabilirlik mimari örneği gösterilir **iki** ile sistemleri, SAP &lt;SID1&gt; ve &lt;SID2&gt;.</span><span class="sxs-lookup"><span data-stu-id="6639f-323">Figure 10 shows an example of an SAP NetWeaver high-availability architecture in Azure for **two** SAP systems, with &lt;SID1&gt; and &lt;SID2&gt;.</span></span> <span data-ttu-id="6639f-324">Bu senaryo aşağıdaki gibi kurun:</span><span class="sxs-lookup"><span data-stu-id="6639f-324">This scenario is set up as follows:</span></span>

- <span data-ttu-id="6639f-325">Ayrılmış bir küme için kullanıldığından **her ikisi de** hello SAP ASCS/SCS SID1 örneği *ve* hello SAP ASCS/SCS SID2 örneği (bir küme için).</span><span class="sxs-lookup"><span data-stu-id="6639f-325">One dedicated cluster is used for **both** hello SAP ASCS/SCS SID1 instance *and* hello SAP ASCS/SCS SID2 instance (one cluster).</span></span>
- <span data-ttu-id="6639f-326">Tek bir adanmış küme DBMS SID1 için kullanılır ve başka bir ayrılmış küme DBMS SID2 için kullanılır (iki küme).</span><span class="sxs-lookup"><span data-stu-id="6639f-326">One dedicated cluster is used for DBMS SID1, and another dedicated cluster is used for DBMS SID2 (two clusters).</span></span>
- <span data-ttu-id="6639f-327">SAP uygulama sunucusu örnekleri hello SAP sistem SID1 için kendi özel VM'ler vardır.</span><span class="sxs-lookup"><span data-stu-id="6639f-327">SAP Application Server instances for hello SAP system SID1 have their own dedicated VMs.</span></span>
- <span data-ttu-id="6639f-328">SAP uygulama sunucusu örnekleri hello SAP sistem SID2 için kendi özel VM'ler vardır.</span><span class="sxs-lookup"><span data-stu-id="6639f-328">SAP Application Server instances for hello SAP system SID2 have their own dedicated VMs.</span></span>

![Şekil 10: yüksek kullanılabilirlik mimari şablonu 3, ile ayrılmış bir küme farklı ASCS/SCS örnekleri için SAP][sap-ha-guide-figure-6003]

<span data-ttu-id="6639f-330">_**Şekil 10:** SAP yüksek kullanılabilirlik mimari şablonu 3, ile ayrılmış bir küme için farklı ASCS/SCS örnekleri_</span><span class="sxs-lookup"><span data-stu-id="6639f-330">_**Figure 10:** SAP high-availability Architectural Template 3, with a dedicated cluster for different ASCS/SCS instances_</span></span>

## <span data-ttu-id="6639f-331"><a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a>Merhaba altyapıyı hazırlama</span><span class="sxs-lookup"><span data-stu-id="6639f-331"><a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a> Prepare hello infrastructure</span></span>

### <a name="prepare-hello-infrastructure-for-architectural-template-1"></a><span data-ttu-id="6639f-332">Mimari şablonu 1 için Hello altyapıyı hazırlama</span><span class="sxs-lookup"><span data-stu-id="6639f-332">Prepare hello infrastructure for Architectural Template 1</span></span>
<span data-ttu-id="6639f-333">Azure Resource Manager şablonları SAP için gerekli kaynakları dağıtımını kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="6639f-333">Azure Resource Manager templates for SAP help simplify deployment of required resources.</span></span>

<span data-ttu-id="6639f-334">Merhaba üç katmanlı şablonları Azure Kaynak Yöneticisi'nde de yüksek kullanılabilirlik senaryoları gibi mimari şablon iki küme olan 1'de destekler.</span><span class="sxs-lookup"><span data-stu-id="6639f-334">hello three-tier templates in Azure Resource Manager also support high-availability scenarios, such as in Architectural Template 1, which has two clusters.</span></span> <span data-ttu-id="6639f-335">Her küme bir SAP tek hata SAP ASCS/SCS ve DBMS noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="6639f-335">Each cluster is an SAP single point of failure for SAP ASCS/SCS and DBMS.</span></span>

<span data-ttu-id="6639f-336">İşte burada hello Örnek senaryo Biz bu makalede açıklamak için Azure Resource Manager şablonları elde edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6639f-336">Here's where you can get Azure Resource Manager templates for hello example scenario we describe in this article:</span></span>

* [<span data-ttu-id="6639f-337">Azure Market görüntüsü</span><span class="sxs-lookup"><span data-stu-id="6639f-337">Azure Marketplace image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image)  
* [<span data-ttu-id="6639f-338">Özel görüntü</span><span class="sxs-lookup"><span data-stu-id="6639f-338">Custom image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image)

<span data-ttu-id="6639f-339">tooprepare hello altyapısı mimari şablon 1:</span><span class="sxs-lookup"><span data-stu-id="6639f-339">tooprepare hello infrastructure for Architectural Template 1:</span></span>

- <span data-ttu-id="6639f-340">Merhaba hello üzerinde Azure portal'ın **parametreleri** dikey penceresinde hello **SYSTEMAVAILABILITY** kutusunda **HA**.</span><span class="sxs-lookup"><span data-stu-id="6639f-340">In hello Azure portal, on hello **Parameters** blade, in hello **SYSTEMAVAILABILITY** box, select **HA**.</span></span>

  ![Şekil 11: Ayarlamak SAP yüksek kullanılabilirlik Azure Resource Manager parametreleri][sap-ha-guide-figure-3000]

<span data-ttu-id="6639f-342">_**Şekil 11:** ayarlamak SAP yüksek kullanılabilirlik Azure Resource Manager parametreleri_</span><span class="sxs-lookup"><span data-stu-id="6639f-342">_**Figure 11:** Set SAP high-availability Azure Resource Manager parameters_</span></span>


  <span data-ttu-id="6639f-343">Merhaba şablonları oluşturun:</span><span class="sxs-lookup"><span data-stu-id="6639f-343">hello templates create:</span></span>

  * <span data-ttu-id="6639f-344">**Sanal makineler**:</span><span class="sxs-lookup"><span data-stu-id="6639f-344">**Virtual machines**:</span></span>
    * <span data-ttu-id="6639f-345">SAP uygulama sunucusu sanal makineleri: <*SAPSystemSID*> - dı - <*numarası*></span><span class="sxs-lookup"><span data-stu-id="6639f-345">SAP Application Server virtual machines: <*SAPSystemSID*>-di-<*Number*></span></span>
    * <span data-ttu-id="6639f-346">ASCS/SCS küme sanal makineler: <*SAPSystemSID*> - ascs - <*numarası*></span><span class="sxs-lookup"><span data-stu-id="6639f-346">ASCS/SCS cluster virtual machines: <*SAPSystemSID*>-ascs-<*Number*></span></span>
    * <span data-ttu-id="6639f-347">DBMS küme: <*SAPSystemSID*> - db - <*numarası*></span><span class="sxs-lookup"><span data-stu-id="6639f-347">DBMS cluster: <*SAPSystemSID*>-db-<*Number*></span></span>

  * <span data-ttu-id="6639f-348">**Ağ kartları ilişkili IP adresleriyle tüm sanal makineler için**:</span><span class="sxs-lookup"><span data-stu-id="6639f-348">**Network cards for all virtual machines, with associated IP addresses**:</span></span>
    * <span data-ttu-id="6639f-349"><*SAPSystemSID*> - NIC - dı - <*numarası*></span><span class="sxs-lookup"><span data-stu-id="6639f-349"><*SAPSystemSID*>-nic-di-<*Number*></span></span>
    * <span data-ttu-id="6639f-350"><*SAPSystemSID*> - NIC - ascs - <*numarası*></span><span class="sxs-lookup"><span data-stu-id="6639f-350"><*SAPSystemSID*>-nic-ascs-<*Number*></span></span>
    * <span data-ttu-id="6639f-351"><*SAPSystemSID*> - NIC - db - <*numarası*></span><span class="sxs-lookup"><span data-stu-id="6639f-351"><*SAPSystemSID*>-nic-db-<*Number*></span></span>

  * <span data-ttu-id="6639f-352">**Azure depolama hesapları**</span><span class="sxs-lookup"><span data-stu-id="6639f-352">**Azure storage accounts**</span></span>

  * <span data-ttu-id="6639f-353">**Kullanılabilirlik grupları** için:</span><span class="sxs-lookup"><span data-stu-id="6639f-353">**Availability groups** for:</span></span>
    * <span data-ttu-id="6639f-354">SAP uygulama sunucusu sanal makineleri: <*SAPSystemSID*> - avset - dı</span><span class="sxs-lookup"><span data-stu-id="6639f-354">SAP Application Server virtual machines: <*SAPSystemSID*>-avset-di</span></span>
    * <span data-ttu-id="6639f-355">SAP ASCS/SCS küme sanal makineler: <*SAPSystemSID*> - avset - ascs</span><span class="sxs-lookup"><span data-stu-id="6639f-355">SAP ASCS/SCS cluster virtual machines: <*SAPSystemSID*>-avset-ascs</span></span>
    * <span data-ttu-id="6639f-356">DBMS küme sanal makineler: <*SAPSystemSID*> - avset - db</span><span class="sxs-lookup"><span data-stu-id="6639f-356">DBMS cluster virtual machines: <*SAPSystemSID*>-avset-db</span></span>

  * <span data-ttu-id="6639f-357">**Azure iç yük dengeleyici**:</span><span class="sxs-lookup"><span data-stu-id="6639f-357">**Azure internal load balancer**:</span></span>
    * <span data-ttu-id="6639f-358">Merhaba ASCS/SCS örneği ve IP adresi için tüm bağlantı noktaları ile <*SAPSystemSID*> - lb - ascs</span><span class="sxs-lookup"><span data-stu-id="6639f-358">With all ports for hello ASCS/SCS instance and IP address <*SAPSystemSID*>-lb-ascs</span></span>
    * <span data-ttu-id="6639f-359">Merhaba SQL Server DBMS ve IP adresi için tüm bağlantı noktaları ile <*SAPSystemSID*> - lb - db</span><span class="sxs-lookup"><span data-stu-id="6639f-359">With all ports for hello SQL Server DBMS and IP address <*SAPSystemSID*>-lb-db</span></span>

  * <span data-ttu-id="6639f-360">**Ağ güvenlik grubu**: <*SAPSystemSID*> - nsg - ascs-0</span><span class="sxs-lookup"><span data-stu-id="6639f-360">**Network security group**: <*SAPSystemSID*>-nsg-ascs-0</span></span>  
    * <span data-ttu-id="6639f-361">Açık bir dış Uzak Masaüstü Protokolü (RDP) bağlantı noktası toohello ile <*SAPSystemSID*> - ascs - 0 sanal makine</span><span class="sxs-lookup"><span data-stu-id="6639f-361">With an open external Remote Desktop Protocol (RDP) port toohello <*SAPSystemSID*>-ascs-0 virtual machine</span></span>

> [!NOTE]
> <span data-ttu-id="6639f-362">Tüm IP adresleri hello ağ kartları ve Azure iç yük dengeleyicileri **dinamik** varsayılan olarak.</span><span class="sxs-lookup"><span data-stu-id="6639f-362">All IP addresses of hello network cards and Azure internal load balancers are **dynamic** by default.</span></span> <span data-ttu-id="6639f-363">Çok değiştirme**statik** IP adresleri.</span><span class="sxs-lookup"><span data-stu-id="6639f-363">Change them too**static** IP addresses.</span></span> <span data-ttu-id="6639f-364">Biz açıklamak nasıl toodo bu hello makalenin sonraki bölümlerinde yer.</span><span class="sxs-lookup"><span data-stu-id="6639f-364">We describe how toodo this later in hello article.</span></span>
>
>

### <span data-ttu-id="6639f-365"><a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a>Kurumsal ağ bağlantısı (şirket içi) toouse üretimde olan sanal makineleri dağıtma</span><span class="sxs-lookup"><span data-stu-id="6639f-365"><a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a> Deploy virtual machines with corporate network connectivity (cross-premises) toouse in production</span></span>
<span data-ttu-id="6639f-366">Üretim SAP sistemleri için Azure sanal makinelerle dağıtımı [kurumsal ağ bağlantısı (şirket içi)] [ planning-guide-2.2] Azure siteden siteye VPN veya Azure ExpressRoute kullanarak.</span><span class="sxs-lookup"><span data-stu-id="6639f-366">For production SAP systems, deploy Azure virtual machines with [corporate network connectivity (cross-premises)][planning-guide-2.2] by using Azure Site-to-Site VPN or Azure ExpressRoute.</span></span>

> [!NOTE]
> <span data-ttu-id="6639f-367">Azure Virtual Network örneğinizi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6639f-367">You can use your Azure Virtual Network instance.</span></span> <span data-ttu-id="6639f-368">Merhaba sanal ağ ve alt ağ zaten oluşturulmuş hazırlanmış ve.</span><span class="sxs-lookup"><span data-stu-id="6639f-368">hello virtual network and subnet have already been created and prepared.</span></span>
>
>

1.  <span data-ttu-id="6639f-369">Merhaba hello üzerinde Azure portal'ın **parametreleri** dikey penceresinde hello **NEWOREXISTINGSUBNET** kutusunda **varolan**.</span><span class="sxs-lookup"><span data-stu-id="6639f-369">In hello Azure portal, on hello **Parameters** blade, in hello **NEWOREXISTINGSUBNET** box, select **existing**.</span></span>
2.  <span data-ttu-id="6639f-370">Merhaba, **SUBNETID** kutusunda, hello tam dize, hazırlanan Azure ağınızın burada planladığınız toodeploy Azure sanal makinelerinizi SubnetID ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6639f-370">In hello **SUBNETID** box, add hello full string of your prepared Azure network SubnetID where you plan toodeploy your Azure virtual machines.</span></span>
3.  <span data-ttu-id="6639f-371">tooget tüm Azure ağ alt ağların bir listesine bu PowerShell komutunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="6639f-371">tooget a list of all Azure network subnets, run this PowerShell command:</span></span>

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets
  ```

  <span data-ttu-id="6639f-372">Merhaba **kimliği** alan gösterir hello **SUBNETID**.</span><span class="sxs-lookup"><span data-stu-id="6639f-372">hello **ID** field shows hello **SUBNETID**.</span></span>
4. <span data-ttu-id="6639f-373">tooget tüm listesini **SUBNETID** değerleri, bu PowerShell komutunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="6639f-373">tooget a list of all **SUBNETID** values, run this PowerShell command:</span></span>

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets.Id
  ```

  <span data-ttu-id="6639f-374">Merhaba **SUBNETID** şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="6639f-374">hello **SUBNETID** looks like this:</span></span>

  ```
  /subscriptions/<SubscriptionId>/resourceGroups/<VPNName>/providers/Microsoft.Network/virtualNetworks/azureVnet/subnets/<SubnetName>
  ```

### <span data-ttu-id="6639f-375"><a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a>Test ve demo için yalnızca bulut SAP örnekleri dağıtma</span><span class="sxs-lookup"><span data-stu-id="6639f-375"><a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a> Deploy cloud-only SAP instances for test and demo</span></span>
<span data-ttu-id="6639f-376">Yüksek kullanılabilirlik SAP sisteminizi bir yalnızca bulut dağıtım modelinde dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6639f-376">You can deploy your high-availability SAP system in a cloud-only deployment model.</span></span> <span data-ttu-id="6639f-377">Bu tür bir dağıtım öncelikle tanıtım ve test kullanım durumları için yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="6639f-377">This kind of deployment primarily is useful for demo and test use cases.</span></span> <span data-ttu-id="6639f-378">Üretim kullanım durumları için uygun değildir.</span><span class="sxs-lookup"><span data-stu-id="6639f-378">It's not suited for production use cases.</span></span>

- <span data-ttu-id="6639f-379">Merhaba hello üzerinde Azure portal'ın **parametreleri** dikey penceresinde hello **NEWOREXISTINGSUBNET** kutusunda **yeni**.</span><span class="sxs-lookup"><span data-stu-id="6639f-379">In hello Azure portal, on hello **Parameters** blade, in hello **NEWOREXISTINGSUBNET** box, select **new**.</span></span> <span data-ttu-id="6639f-380">Merhaba bırakın **SUBNETID** alanı boş.</span><span class="sxs-lookup"><span data-stu-id="6639f-380">Leave hello **SUBNETID** field empty.</span></span>

  <span data-ttu-id="6639f-381">Azure sanal ağ ve alt hello Hello SAP Azure Resource Manager şablonu otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6639f-381">hello SAP Azure Resource Manager template automatically creates hello Azure virtual network and subnet.</span></span>

> [!NOTE]
> <span data-ttu-id="6639f-382">Ayrıca toodeploy gereken Active Directory için en az bir ayrılmış sanal makine ve DNS'de hello aynı Azure sanal ağı örneği.</span><span class="sxs-lookup"><span data-stu-id="6639f-382">You also need toodeploy at least one dedicated virtual machine for Active Directory and DNS in hello same Azure Virtual Network instance.</span></span> <span data-ttu-id="6639f-383">Merhaba şablonu, bu sanal makineleri oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="6639f-383">hello template doesn't create these virtual machines.</span></span>
>
>


### <a name="prepare-hello-infrastructure-for-architectural-template-2"></a><span data-ttu-id="6639f-384">Mimari şablon 2 Hello altyapıyı hazırlama</span><span class="sxs-lookup"><span data-stu-id="6639f-384">Prepare hello infrastructure for Architectural Template 2</span></span>

<span data-ttu-id="6639f-385">SAP toohelp basitleştirmek için gerekli altyapı kaynaklarıdır dağıtım SAP mimari şablon 2 için bu Azure Resource Manager şablonu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6639f-385">You can use this Azure Resource Manager template for SAP toohelp simplify deployment of required infrastructure resources for SAP Architectural Template 2.</span></span>

<span data-ttu-id="6639f-386">İşte, bu dağıtım senaryosu için Azure Resource Manager şablonları burada alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6639f-386">Here's where you can get Azure Resource Manager templates for this deployment scenario:</span></span>

* [<span data-ttu-id="6639f-387">Azure Market görüntüsü</span><span class="sxs-lookup"><span data-stu-id="6639f-387">Azure Marketplace image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged)  
* [<span data-ttu-id="6639f-388">Özel görüntü</span><span class="sxs-lookup"><span data-stu-id="6639f-388">Custom image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged)


### <a name="prepare-hello-infrastructure-for-architectural-template-3"></a><span data-ttu-id="6639f-389">Mimari şablonu 3 Hello altyapıyı hazırlama</span><span class="sxs-lookup"><span data-stu-id="6639f-389">Prepare hello infrastructure for Architectural Template 3</span></span>

<span data-ttu-id="6639f-390">Hello altyapıyı hazırlama ve yapılandırma için SAP **çoklu SID**.</span><span class="sxs-lookup"><span data-stu-id="6639f-390">You can prepare hello infrastructure and configure SAP for **multi-SID**.</span></span> <span data-ttu-id="6639f-391">Örneğin, ek bir SAP ASCS/SCS örneğine ekleyebileceğiniz bir *varolan* küme yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="6639f-391">For example, you can add an additional SAP ASCS/SCS instance into an *existing* cluster configuration.</span></span> <span data-ttu-id="6639f-392">Daha fazla bilgi için bkz: [var olan bir küme yapılandırması toocreate bir SAP çoklu SID yapılandırma ek bir SAP ASCS/SCS örneğine Azure Kaynak Yöneticisi'nde yapılandırma][sap-ha-multi-sid-guide].</span><span class="sxs-lookup"><span data-stu-id="6639f-392">For more information, see [Configure an additional SAP ASCS/SCS instance into an existing cluster configuration toocreate an SAP multi-SID configuration in Azure Resource Manager][sap-ha-multi-sid-guide].</span></span>

<span data-ttu-id="6639f-393">Yeni bir SID çoklu küme toocreate istiyorsanız hello multi-SID kullanabilirsiniz [GitHub hızlı başlangıç şablonlarında](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="6639f-393">If you want toocreate a new multi-SID cluster, you can use hello multi-SID [quickstart templates on GitHub](https://github.com/Azure/azure-quickstart-templates).</span></span>
<span data-ttu-id="6639f-394">Yeni bir SID çoklu küme toocreate, üç şablonları aşağıdaki toodeploy hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="6639f-394">toocreate a new multi-SID cluster, you need toodeploy hello following three templates:</span></span>

* [<span data-ttu-id="6639f-395">ASCS/SCS şablonu</span><span class="sxs-lookup"><span data-stu-id="6639f-395">ASCS/SCS template</span></span>](#ASCS-SCS-template)
* [<span data-ttu-id="6639f-396">Veritabanı şablonu</span><span class="sxs-lookup"><span data-stu-id="6639f-396">Database template</span></span>](#database-template)
* [<span data-ttu-id="6639f-397">Uygulama sunucuları şablonu</span><span class="sxs-lookup"><span data-stu-id="6639f-397">Application servers template</span></span>](#application-servers-template)

<span data-ttu-id="6639f-398">Merhaba aşağıdaki bölümlerde hello şablonları ve hello şablonlarındaki tooprovide ihtiyacınız hello parametreleri hakkında daha fazla ayrıntı sahip.</span><span class="sxs-lookup"><span data-stu-id="6639f-398">hello following sections have more details about hello templates and hello parameters you need tooprovide in hello templates.</span></span>

#### <span data-ttu-id="6639f-399"><a name="ASCS-SCS-template"></a>ASCS/SCS şablonu</span><span class="sxs-lookup"><span data-stu-id="6639f-399"><a name="ASCS-SCS-template"></a> ASCS/SCS template</span></span>

<span data-ttu-id="6639f-400">Merhaba ASCS/SCS şablonu toocreate birden çok ASCS/SCS örneği barındıran bir Windows Server Yük devretme kümesi kullanabileceğiniz iki sanal makine dağıtır.</span><span class="sxs-lookup"><span data-stu-id="6639f-400">hello ASCS/SCS template deploys two virtual machines that you can use toocreate a Windows Server failover cluster that hosts multiple ASCS/SCS instances.</span></span>

<span data-ttu-id="6639f-401">Merhaba ASCS/SCS multi-SID şablonunda hello yukarı tooset [ASCS/SCS çoklu SID şablonu][sap-templates-3-tier-multisid-xscs-marketplace-image], hello şu parametreler için değerler girin:</span><span class="sxs-lookup"><span data-stu-id="6639f-401">tooset up hello ASCS/SCS multi-SID template, in hello [ASCS/SCS multi-SID template][sap-templates-3-tier-multisid-xscs-marketplace-image], enter values for hello following parameters:</span></span>

  - <span data-ttu-id="6639f-402">**Kaynak önek**.</span><span class="sxs-lookup"><span data-stu-id="6639f-402">**Resource Prefix**.</span></span>  <span data-ttu-id="6639f-403">Kullanılan tooprefix olan hello kaynak öneki hello dağıtımı sırasında oluşturulan tüm kaynakları ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="6639f-403">Set hello resource prefix, which is used tooprefix all resources that are created during hello deployment.</span></span> <span data-ttu-id="6639f-404">Merhaba kaynakları tooonly bir SAP sistemine ait olmadığından hello kaynak hello öneki hello bir SAP sistem SID'si değil.</span><span class="sxs-lookup"><span data-stu-id="6639f-404">Because hello resources do not belong tooonly one SAP system, hello prefix of hello resource is not hello SID of one SAP system.</span></span>  <span data-ttu-id="6639f-405">Merhaba önek arasında olmalıdır **üç ve altı karakter**.</span><span class="sxs-lookup"><span data-stu-id="6639f-405">hello prefix must be between **three and six characters**.</span></span>
  - <span data-ttu-id="6639f-406">**Yığın türü**.</span><span class="sxs-lookup"><span data-stu-id="6639f-406">**Stack Type**.</span></span> <span data-ttu-id="6639f-407">Merhaba yığını hello SAP sistem türünü seçin.</span><span class="sxs-lookup"><span data-stu-id="6639f-407">Select hello stack type of hello SAP system.</span></span> <span data-ttu-id="6639f-408">Merhaba yığını türüne bağlı olarak, Azure yük dengeleyici (ABAP veya yalnızca Java) bir veya iki (ABAP + Java) özel IP adresleri SAP sistem başına var.</span><span class="sxs-lookup"><span data-stu-id="6639f-408">Depending on hello stack type, Azure Load Balancer has one (ABAP or Java only) or two (ABAP+Java) private IP addresses per SAP system.</span></span>
  -  <span data-ttu-id="6639f-409">**İşletim sistemi türü**.</span><span class="sxs-lookup"><span data-stu-id="6639f-409">**OS Type**.</span></span> <span data-ttu-id="6639f-410">Merhaba sanal makinelerin Hello işletim sistemini seçin.</span><span class="sxs-lookup"><span data-stu-id="6639f-410">Select hello operating system of hello virtual machines.</span></span>
  -  <span data-ttu-id="6639f-411">**SAP sistem sayısı**.</span><span class="sxs-lookup"><span data-stu-id="6639f-411">**SAP System Count**.</span></span> <span data-ttu-id="6639f-412">Merhaba numarasını seçin SAP sistemlerinin bu kümedeki tooinstall istiyor.</span><span class="sxs-lookup"><span data-stu-id="6639f-412">Select hello number of SAP systems you want tooinstall in this cluster.</span></span>
  -  <span data-ttu-id="6639f-413">**Sistem kullanılabilirliğini**.</span><span class="sxs-lookup"><span data-stu-id="6639f-413">**System Availability**.</span></span> <span data-ttu-id="6639f-414">Seçin **HA**.</span><span class="sxs-lookup"><span data-stu-id="6639f-414">Select **HA**.</span></span>
  -  <span data-ttu-id="6639f-415">**Yönetici kullanıcı adı ve yönetici parolası**.</span><span class="sxs-lookup"><span data-stu-id="6639f-415">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="6639f-416">Kullanılan toosign toohello makinede olabilir yeni bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6639f-416">Create a new user that can be used toosign in toohello machine.</span></span>
  -  <span data-ttu-id="6639f-417">**Yeni veya var olan bir alt ağ**.</span><span class="sxs-lookup"><span data-stu-id="6639f-417">**New Or Existing Subnet**.</span></span> <span data-ttu-id="6639f-418">Yeni sanal ağ ve alt oluşturulmalıdır veya mevcut bir alt kullanılmalıdır gerekip gerekmediğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="6639f-418">Set whether a new virtual network and subnet should be created, or an existing subnet should be used.</span></span> <span data-ttu-id="6639f-419">Bağlı tooyour şirket içi ağ bir sanal ağ zaten varsa, seçin **varolan**.</span><span class="sxs-lookup"><span data-stu-id="6639f-419">If you already have a virtual network that is connected tooyour on-premises network, select **existing**.</span></span>
  -  <span data-ttu-id="6639f-420">**Alt ağ kimliği**. Kümesi hello kimliği hello alt toowhich hello sanal makinelerin bağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="6639f-420">**Subnet Id**. Set hello ID of hello subnet toowhich hello virtual machines should be connected.</span></span> <span data-ttu-id="6639f-421">Sanal özel ağ (VPN) veya ExpressRoute sanal ağ tooconnect hello sanal makine tooyour şirket içi ağın Hello alt ağ seçin.</span><span class="sxs-lookup"><span data-stu-id="6639f-421">Select hello subnet of your virtual private network (VPN) or ExpressRoute virtual network tooconnect hello virtual machine tooyour on-premises network.</span></span> <span data-ttu-id="6639f-422">Merhaba kimliği genellikle şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="6639f-422">hello ID usually looks like this:</span></span>

   <span data-ttu-id="6639f-423">/Subscriptions/ <*abonelik kimliği*> /resourceGroups/ <*kaynak grubu adı*> /providers/Microsoft.Network/virtualNetworks/ <*sanal ağ adı*> /subnets/ <*alt ağ adı*></span><span class="sxs-lookup"><span data-stu-id="6639f-423">/subscriptions/<*subscription id*>/resourceGroups/<*resource group name*>/providers/Microsoft.Network/virtualNetworks/<*virtual network name*>/subnets/<*subnet name*></span></span>

<span data-ttu-id="6639f-424">Merhaba şablon birden çok SAP sistemlerini destekleyen bir Azure yük dengeleyici örneği dağıtır.</span><span class="sxs-lookup"><span data-stu-id="6639f-424">hello template deploys one Azure Load Balancer instance, which supports multiple SAP systems.</span></span>

- <span data-ttu-id="6639f-425">Merhaba ASCS örnekleri örnek numarası 00, 10, 20 yapılandırılmış...</span><span class="sxs-lookup"><span data-stu-id="6639f-425">hello ASCS instances are configured for instance number 00, 10, 20...</span></span>
- <span data-ttu-id="6639f-426">Merhaba SCS örnekleri örnek numarası 01, 11, 21 yapılandırılmış...</span><span class="sxs-lookup"><span data-stu-id="6639f-426">hello SCS instances are configured for instance number 01, 11, 21...</span></span>
- <span data-ttu-id="6639f-427">Merhaba ASCS kuyruğa çoğaltma sunucusuna (ERS) (yalnızca Linux) örnekleri örnek numarası 02, 12, 22 yapılandırılmış...</span><span class="sxs-lookup"><span data-stu-id="6639f-427">hello ASCS Enqueue Replication Server (ERS) (Linux only) instances are configured for instance number 02, 12, 22...</span></span>
- <span data-ttu-id="6639f-428">Merhaba SCS ERS (yalnızca Linux) örnekleri örneği için 03, 13, 23 sayısı yapılandırılan...</span><span class="sxs-lookup"><span data-stu-id="6639f-428">hello SCS ERS (Linux only) instances are configured for instance number 03, 13, 23...</span></span>

<span data-ttu-id="6639f-429">Merhaba yük dengeleyici içeren 1 (Linux için 2) VIP(s), ASCS/SCS için 1 x VIP ve 1 x VIP ERS (yalnızca Linux) için.</span><span class="sxs-lookup"><span data-stu-id="6639f-429">hello load balancer contains 1 (2 for Linux) VIP(s), 1x VIP for ASCS/SCS and 1x VIP for ERS (Linux only).</span></span>

<span data-ttu-id="6639f-430">Merhaba aşağıdaki listede tüm Yük Dengeleme kuralları (burada x hello hello SAP sistem, örneğin, 1, 2, 3... sayısıdır) içerir:</span><span class="sxs-lookup"><span data-stu-id="6639f-430">hello following list contains all load balancing rules (where x is hello number of hello SAP system, for example, 1, 2, 3...):</span></span>
- <span data-ttu-id="6639f-431">Her SAP sistemi için Windows özel bağlantı noktaları: 445, 5985</span><span class="sxs-lookup"><span data-stu-id="6639f-431">Windows-specific ports for every SAP system: 445, 5985</span></span>
- <span data-ttu-id="6639f-432">ASCS bağlantı noktası (örnek numarasını x0): 32 x 0, 36 x 0, 39 x 0, 81 x 0, 5 x 013, 5 x 014, 5 x 016</span><span class="sxs-lookup"><span data-stu-id="6639f-432">ASCS ports (instance number x0): 32x0, 36x0, 39x0, 81x0, 5x013, 5x014, 5x016</span></span>
- <span data-ttu-id="6639f-433">SCS bağlantı noktası (örnek numarasını x1): 32 x 1, 33 x 1, 39 x 1, 81 x 1, 5 x 113, 5 x 114, 5 x 116</span><span class="sxs-lookup"><span data-stu-id="6639f-433">SCS ports (instance number x1): 32x1, 33x1, 39x1, 81x1, 5x113, 5x114, 5x116</span></span>
- <span data-ttu-id="6639f-434">ASCS ERS bağlantı noktaları (örnek numarasını x2) Linux'ta: 33 x 2, 5 x 213, 5 x 214, 5 x 216</span><span class="sxs-lookup"><span data-stu-id="6639f-434">ASCS ERS ports on Linux (instance number x2): 33x2, 5x213, 5x214, 5x216</span></span>
- <span data-ttu-id="6639f-435">SCS ERS bağlantı noktaları (örnek numarasını x3) Linux'ta: 33 x 3, 5 x 313, 5 x 314, 5 x 316</span><span class="sxs-lookup"><span data-stu-id="6639f-435">SCS ERS ports on Linux (instance number x3): 33x3, 5x313, 5x314, 5x316</span></span>

<span data-ttu-id="6639f-436">Merhaba yük dengeleyici yapılandırılmış toouse hello araştırma bağlantı noktaları (burada x hello hello SAP sistem, örneğin, 1, 2, 3... sayısıdır) aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="6639f-436">hello load balancer is configured toouse hello following probe ports (where x is hello number of hello SAP system, for example, 1, 2, 3...):</span></span>
- <span data-ttu-id="6639f-437">ASCS/SCS iç yük dengeleyici araştırması bağlantı noktası: 620 x 0</span><span class="sxs-lookup"><span data-stu-id="6639f-437">ASCS/SCS internal load balancer probe port: 620x0</span></span>
- <span data-ttu-id="6639f-438">ERS iç yük dengeleyici araştırması bağlantı noktası (yalnızca Linux): 621 x 2</span><span class="sxs-lookup"><span data-stu-id="6639f-438">ERS internal load balancer probe port (Linux only): 621x2</span></span>

#### <span data-ttu-id="6639f-439"><a name="database-template"></a>Veritabanı şablonu</span><span class="sxs-lookup"><span data-stu-id="6639f-439"><a name="database-template"></a> Database template</span></span>

<span data-ttu-id="6639f-440">Merhaba veritabanı şablonu bir dağıtır veya tooinstall kullanabileceğiniz iki sanal makine için bir SAP sistem ilişkisel veritabanı yönetim sistemine (RDBMS) hello.</span><span class="sxs-lookup"><span data-stu-id="6639f-440">hello database template deploys one or two virtual machines that you can use tooinstall hello relational database management system (RDBMS) for one SAP system.</span></span> <span data-ttu-id="6639f-441">Beş SAP sistemleri için bir ASCS/SCS şablonu dağıtırsanız, örneğin, toodeploy bu şablonu beş kez gerekir.</span><span class="sxs-lookup"><span data-stu-id="6639f-441">For example, if you deploy an ASCS/SCS template for five SAP systems, you need toodeploy this template five times.</span></span>

<span data-ttu-id="6639f-442">Merhaba, hello veritabanı çoklu SID şablonu tooset [veritabanı çoklu SID şablonu][sap-templates-3-tier-multisid-db-marketplace-image], hello şu parametreler için değerler girin:</span><span class="sxs-lookup"><span data-stu-id="6639f-442">tooset up hello database multi-SID template, in hello [database multi-SID template][sap-templates-3-tier-multisid-db-marketplace-image], enter values for hello following parameters:</span></span>

  -  <span data-ttu-id="6639f-443">**SAP sistem kimliği**. Merhaba tooinstall istediğiniz SAP sistemi Hello SAP sistem Kimliğini girin.</span><span class="sxs-lookup"><span data-stu-id="6639f-443">**Sap System Id**. Enter hello SAP system ID of hello SAP system you want tooinstall.</span></span> <span data-ttu-id="6639f-444">Merhaba kimliği önek olarak dağıtılan hello kaynaklar için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6639f-444">hello ID will be used as a prefix for hello resources that are deployed.</span></span>
  -  <span data-ttu-id="6639f-445">**İşletim sistemi türü**.</span><span class="sxs-lookup"><span data-stu-id="6639f-445">**Os Type**.</span></span> <span data-ttu-id="6639f-446">Merhaba sanal makinelerin Hello işletim sistemini seçin.</span><span class="sxs-lookup"><span data-stu-id="6639f-446">Select hello operating system of hello virtual machines.</span></span>
  -  <span data-ttu-id="6639f-447">**DbType**.</span><span class="sxs-lookup"><span data-stu-id="6639f-447">**Dbtype**.</span></span> <span data-ttu-id="6639f-448">Merhaba türünü seçin hello veritabanı hello kümede tooinstall istiyor.</span><span class="sxs-lookup"><span data-stu-id="6639f-448">Select hello type of hello database you want tooinstall on hello cluster.</span></span> <span data-ttu-id="6639f-449">Seçin **SQL** tooinstall Microsoft SQL Server istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="6639f-449">Select **SQL** if you want tooinstall Microsoft SQL Server.</span></span> <span data-ttu-id="6639f-450">Seçin **HANA** hello sanal makinelerde tooinstall SAP HANA planlıyorsanız.</span><span class="sxs-lookup"><span data-stu-id="6639f-450">Select **HANA** if you plan tooinstall SAP HANA on hello virtual machines.</span></span> <span data-ttu-id="6639f-451">Tooselect hello doğru işletim sistemi türü olduğundan emin olun: seçin **Windows** HANA için Linux dağıtımı seçin ve SQL için.</span><span class="sxs-lookup"><span data-stu-id="6639f-451">Make sure tooselect hello correct operating system type: select **Windows** for SQL, and select a Linux distribution for HANA.</span></span> <span data-ttu-id="6639f-452">Merhaba, sanal makineler olacaktır bağlı toohello Azure yük dengeleyici toosupport seçili hello veritabanı türü yapılandırılır:</span><span class="sxs-lookup"><span data-stu-id="6639f-452">hello Azure Load Balancer that is connected toohello virtual machines will be configured toosupport hello selected database type:</span></span>
    * <span data-ttu-id="6639f-453">**SQL**.</span><span class="sxs-lookup"><span data-stu-id="6639f-453">**SQL**.</span></span> <span data-ttu-id="6639f-454">Merhaba yük dengeleyici Yük Dengeleme bağlantı noktası 1433 olur.</span><span class="sxs-lookup"><span data-stu-id="6639f-454">hello load balancer will load-balance port 1433.</span></span> <span data-ttu-id="6639f-455">Bu bağlantı noktası için SQL Server Always On kurulumunuzu emin toouse olun.</span><span class="sxs-lookup"><span data-stu-id="6639f-455">Make sure toouse this port for your SQL Server Always On setup.</span></span>
    * <span data-ttu-id="6639f-456">**HANA**.</span><span class="sxs-lookup"><span data-stu-id="6639f-456">**HANA**.</span></span> <span data-ttu-id="6639f-457">Merhaba yük dengeleyici Yük Dengeleme 35015 ve 35017 bağlantı noktalarını olur.</span><span class="sxs-lookup"><span data-stu-id="6639f-457">hello load balancer will load-balance ports 35015 and 35017.</span></span> <span data-ttu-id="6639f-458">İle örnek numarasını emin tooinstall SAP HANA olun **50**.</span><span class="sxs-lookup"><span data-stu-id="6639f-458">Make sure tooinstall SAP HANA with instance number **50**.</span></span>
    <span data-ttu-id="6639f-459">Merhaba yük dengeleyici araştırması bağlantı noktasını 62550 kullanır.</span><span class="sxs-lookup"><span data-stu-id="6639f-459">hello load balancer will use probe port 62550.</span></span>
  -  <span data-ttu-id="6639f-460">**SAP sistem boyutu**.</span><span class="sxs-lookup"><span data-stu-id="6639f-460">**Sap System Size**.</span></span> <span data-ttu-id="6639f-461">SAP hello yeni sistem kümesi hello sayısını sağlar.</span><span class="sxs-lookup"><span data-stu-id="6639f-461">Set hello number of SAPS hello new system will provide.</span></span> <span data-ttu-id="6639f-462">Kaç tane SAP hello sistem gerektirir emin değilseniz, SAP teknolojisi iş ortağı veya sistem Tümleştirici isteyin.</span><span class="sxs-lookup"><span data-stu-id="6639f-462">If you are not sure how many SAPS hello system will require, ask your SAP Technology Partner or System Integrator.</span></span>
  -  <span data-ttu-id="6639f-463">**Sistem kullanılabilirliğini**.</span><span class="sxs-lookup"><span data-stu-id="6639f-463">**System Availability**.</span></span> <span data-ttu-id="6639f-464">Seçin **HA**.</span><span class="sxs-lookup"><span data-stu-id="6639f-464">Select **HA**.</span></span>
  -  <span data-ttu-id="6639f-465">**Yönetici kullanıcı adı ve yönetici parolası**.</span><span class="sxs-lookup"><span data-stu-id="6639f-465">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="6639f-466">Kullanılan toosign toohello makinede olabilir yeni bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6639f-466">Create a new user that can be used toosign in toohello machine.</span></span>
  -  <span data-ttu-id="6639f-467">**Alt ağ kimliği**. Merhaba hello ASCS/SCS şablonu hello dağıtımı sırasında kullanılan hello alt ağ Kimliğini veya hello oluşturulduğu hello alt ağ Kimliğini hello ASCS/SCS şablon dağıtımı bir parçası olarak girin.</span><span class="sxs-lookup"><span data-stu-id="6639f-467">**Subnet Id**. Enter hello ID of hello subnet that you used during hello deployment of hello ASCS/SCS template, or hello ID of hello subnet that was created as part of hello ASCS/SCS template deployment.</span></span>

#### <span data-ttu-id="6639f-468"><a name="application-servers-template"></a>Uygulama sunucuları şablonu</span><span class="sxs-lookup"><span data-stu-id="6639f-468"><a name="application-servers-template"></a> Application servers template</span></span>

<span data-ttu-id="6639f-469">Merhaba uygulama sunucuları şablonu iki veya daha fazla sanal SAP uygulama sunucusu örneklerinin bir SAP sistemi için kullanılabilecek makineler dağıtır.</span><span class="sxs-lookup"><span data-stu-id="6639f-469">hello application servers template deploys two or more virtual machines that can be used as SAP Application Server instances for one SAP system.</span></span> <span data-ttu-id="6639f-470">Beş SAP sistemleri için bir ASCS/SCS şablonu dağıtırsanız, örneğin, toodeploy bu şablonu beş kez gerekir.</span><span class="sxs-lookup"><span data-stu-id="6639f-470">For example, if you deploy an ASCS/SCS template for five SAP systems, you need toodeploy this template five times.</span></span>

<span data-ttu-id="6639f-471">Merhaba uygulama sunucuları çoklu SID şablonunda, hello yukarı tooset [uygulama sunucuları çoklu SID şablonu][sap-templates-3-tier-multisid-apps-marketplace-image], hello şu parametreler için değerler girin:</span><span class="sxs-lookup"><span data-stu-id="6639f-471">tooset up hello application servers multi-SID template, in hello [application servers multi-SID template][sap-templates-3-tier-multisid-apps-marketplace-image], enter values for hello following parameters:</span></span>

  -  <span data-ttu-id="6639f-472">**SAP sistem kimliği**. Merhaba tooinstall istediğiniz SAP sistemi Hello SAP sistem Kimliğini girin.</span><span class="sxs-lookup"><span data-stu-id="6639f-472">**Sap System Id**. Enter hello SAP system ID of hello SAP system you want tooinstall.</span></span> <span data-ttu-id="6639f-473">Merhaba kimliği önek olarak dağıtılan hello kaynaklar için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6639f-473">hello ID will be used as a prefix for hello resources that are deployed.</span></span>
  -  <span data-ttu-id="6639f-474">**İşletim sistemi türü**.</span><span class="sxs-lookup"><span data-stu-id="6639f-474">**Os Type**.</span></span> <span data-ttu-id="6639f-475">Merhaba sanal makinelerin Hello işletim sistemini seçin.</span><span class="sxs-lookup"><span data-stu-id="6639f-475">Select hello operating system of hello virtual machines.</span></span>
  -  <span data-ttu-id="6639f-476">**SAP sistem boyutu**.</span><span class="sxs-lookup"><span data-stu-id="6639f-476">**Sap System Size**.</span></span> <span data-ttu-id="6639f-477">SAP hello yeni sistem Hello sayısını sağlar.</span><span class="sxs-lookup"><span data-stu-id="6639f-477">hello number of SAPS hello new system will provide.</span></span> <span data-ttu-id="6639f-478">Kaç tane SAP hello sistem gerektirir emin değilseniz, SAP teknolojisi iş ortağı veya sistem Tümleştirici isteyin.</span><span class="sxs-lookup"><span data-stu-id="6639f-478">If you are not sure how many SAPS hello system will require, ask your SAP Technology Partner or System Integrator.</span></span>
  -  <span data-ttu-id="6639f-479">**Sistem kullanılabilirliğini**.</span><span class="sxs-lookup"><span data-stu-id="6639f-479">**System Availability**.</span></span> <span data-ttu-id="6639f-480">Seçin **HA**.</span><span class="sxs-lookup"><span data-stu-id="6639f-480">Select **HA**.</span></span>
  -  <span data-ttu-id="6639f-481">**Yönetici kullanıcı adı ve yönetici parolası**.</span><span class="sxs-lookup"><span data-stu-id="6639f-481">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="6639f-482">Kullanılan toosign toohello makinede olabilir yeni bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6639f-482">Create a new user that can be used toosign in toohello machine.</span></span>
  -  <span data-ttu-id="6639f-483">**Alt ağ kimliği**. Merhaba hello ASCS/SCS şablonu hello dağıtımı sırasında kullanılan hello alt ağ Kimliğini veya hello oluşturulduğu hello alt ağ Kimliğini hello ASCS/SCS şablon dağıtımı bir parçası olarak girin.</span><span class="sxs-lookup"><span data-stu-id="6639f-483">**Subnet Id**. Enter hello ID of hello subnet that you used during hello deployment of hello ASCS/SCS template, or hello ID of hello subnet that was created as part of hello ASCS/SCS template deployment.</span></span>


### <span data-ttu-id="6639f-484"><a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a>Azure sanal ağı</span><span class="sxs-lookup"><span data-stu-id="6639f-484"><a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a> Azure virtual network</span></span>
<span data-ttu-id="6639f-485">Bizim örneğimizde, hello Azure sanal ağı hello adres alanı 10.0.0.0/16 şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="6639f-485">In our example, hello address space of hello Azure virtual network is 10.0.0.0/16.</span></span> <span data-ttu-id="6639f-486">Adlı bir alt ağ yok **alt**, 10.0.0.0/24 adres aralığı olan.</span><span class="sxs-lookup"><span data-stu-id="6639f-486">There is one subnet called **Subnet**, with an address range of 10.0.0.0/24.</span></span> <span data-ttu-id="6639f-487">Bu sanal ağda, tüm sanal makineler ve iç yük dengeleyicileri dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="6639f-487">All virtual machines and internal load balancers are deployed in this virtual network.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6639f-488">Toohello ağ ayarlarını hello konuk işletim sistemi içinde herhangi bir değişiklik yapmayın.</span><span class="sxs-lookup"><span data-stu-id="6639f-488">Don't make any changes toohello network settings inside hello guest operating system.</span></span> <span data-ttu-id="6639f-489">Bu IP adresleri, DNS sunucuları ve alt ağ içerir.</span><span class="sxs-lookup"><span data-stu-id="6639f-489">This includes IP addresses, DNS servers, and subnet.</span></span> <span data-ttu-id="6639f-490">Azure'da tüm ağ ayarlarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="6639f-490">Configure all your network settings in Azure.</span></span> <span data-ttu-id="6639f-491">Merhaba Dinamik Ana Bilgisayar Yapılandırma Protokolü (DHCP) hizmetini ayarlarınızı yayar.</span><span class="sxs-lookup"><span data-stu-id="6639f-491">hello Dynamic Host Configuration Protocol (DHCP) service propagates your settings.</span></span>
>
>

### <span data-ttu-id="6639f-492"><a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a>DNS IP adresleri</span><span class="sxs-lookup"><span data-stu-id="6639f-492"><a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a> DNS IP addresses</span></span>

<span data-ttu-id="6639f-493">DNS IP adresleri tooset hello gerekli, aşağıdaki adımları hello.</span><span class="sxs-lookup"><span data-stu-id="6639f-493">tooset hello required DNS IP addresses, do hello following steps.</span></span>

1.  <span data-ttu-id="6639f-494">Hello hello üzerinde Azure portal'ın **DNS sunucuları** dikey penceresinde olduğundan emin olun, sanal ağ **DNS sunucuları** seçeneği çok ayarlamak**özel DNS**.</span><span class="sxs-lookup"><span data-stu-id="6639f-494">In hello Azure portal, on hello **DNS servers** blade, make sure that your virtual network **DNS servers** option is set too**Custom DNS**.</span></span>
2.  <span data-ttu-id="6639f-495">Sahip olduğunuz ağ Hello türüne göre ayarlarınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="6639f-495">Select your settings based on hello type of network you have.</span></span> <span data-ttu-id="6639f-496">Daha fazla bilgi için kaynakları aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="6639f-496">For more information, see hello following resources:</span></span>
    * <span data-ttu-id="6639f-497">[Kurumsal ağ bağlantısı (şirket içi)][planning-guide-2.2]: hello hello şirket içi DNS sunucularının IP adreslerini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6639f-497">[Corporate network connectivity (cross-premises)][planning-guide-2.2]: Add hello IP addresses of hello on-premises DNS servers.</span></span>  
    <span data-ttu-id="6639f-498">Azure'da çalışan şirket içi DNS sunucuları toohello sanal makineleri genişletebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6639f-498">You can extend on-premises DNS servers toohello virtual machines that are running in Azure.</span></span> <span data-ttu-id="6639f-499">Bu senaryoda hello Azure hello IP adreslerini ekleyebilirsiniz hello DNS hizmetinin çalıştığı sanal makineler.</span><span class="sxs-lookup"><span data-stu-id="6639f-499">In that scenario, you can add hello IP addresses of hello Azure virtual machines on which you run hello DNS service.</span></span>
    * <span data-ttu-id="6639f-500">[Yalnızca bulut dağıtım][planning-guide-2.1]: hello ek bir sanal makineyi dağıtmak, bir DNS sunucusu olarak hizmet veren aynı sanal ağ örneği.</span><span class="sxs-lookup"><span data-stu-id="6639f-500">[Cloud-only deployment][planning-guide-2.1]: Deploy an additional virtual machine in hello same Virtual Network instance that serves as a DNS server.</span></span> <span data-ttu-id="6639f-501">Hello Azure Hello IP adreslerini eklemek toorun DNS hizmetini ayarlama sanal makineler.</span><span class="sxs-lookup"><span data-stu-id="6639f-501">Add hello IP addresses of hello Azure virtual machines that you've set up toorun DNS service.</span></span>

    ![Şekil 12: Azure sanal ağı için DNS sunucularını yapılandırın][sap-ha-guide-figure-3001]

    <span data-ttu-id="6639f-503">_**Şekil 12:** Yapılandır DNS sunucuları için Azure sanal ağ_</span><span class="sxs-lookup"><span data-stu-id="6639f-503">_**Figure 12:** Configure DNS servers for Azure Virtual Network_</span></span>

  > [!NOTE]
  > <span data-ttu-id="6639f-504">Merhaba DNS sunucularının IP adreslerini hello değiştirirseniz, toorestart hello Azure sanal makineleri tooapply gereksinim hello değişiklik ve hello yeni DNS sunucularını yayar.</span><span class="sxs-lookup"><span data-stu-id="6639f-504">If you change hello IP addresses of hello DNS servers, you need toorestart hello Azure virtual machines tooapply hello change and propagate hello new DNS servers.</span></span>
  >
  >

<span data-ttu-id="6639f-505">Bizim örneğimizde, hello DNS hizmeti yüklenir ve bu Windows sanal makinelerde yapılandırılır:</span><span class="sxs-lookup"><span data-stu-id="6639f-505">In our example, hello DNS service is installed and configured on these Windows virtual machines:</span></span>

| <span data-ttu-id="6639f-506">Sanal makine rolü</span><span class="sxs-lookup"><span data-stu-id="6639f-506">Virtual machine role</span></span> | <span data-ttu-id="6639f-507">Sanal makine ana bilgisayar adı</span><span class="sxs-lookup"><span data-stu-id="6639f-507">Virtual machine host name</span></span> | <span data-ttu-id="6639f-508">Ağ kartı adı</span><span class="sxs-lookup"><span data-stu-id="6639f-508">Network card name</span></span> | <span data-ttu-id="6639f-509">Statik IP adresi</span><span class="sxs-lookup"><span data-stu-id="6639f-509">Static IP address</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6639f-510">İlk DNS sunucusu</span><span class="sxs-lookup"><span data-stu-id="6639f-510">First DNS server</span></span> |<span data-ttu-id="6639f-511">domcontr-0</span><span class="sxs-lookup"><span data-stu-id="6639f-511">domcontr-0</span></span> |<span data-ttu-id="6639f-512">pr1-NIC-domcontr-0</span><span class="sxs-lookup"><span data-stu-id="6639f-512">pr1-nic-domcontr-0</span></span> |<span data-ttu-id="6639f-513">10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="6639f-513">10.0.0.10</span></span> |
| <span data-ttu-id="6639f-514">İkinci DNS sunucusu</span><span class="sxs-lookup"><span data-stu-id="6639f-514">Second DNS server</span></span> |<span data-ttu-id="6639f-515">domcontr-1</span><span class="sxs-lookup"><span data-stu-id="6639f-515">domcontr-1</span></span> |<span data-ttu-id="6639f-516">pr1-NIC-domcontr-1</span><span class="sxs-lookup"><span data-stu-id="6639f-516">pr1-nic-domcontr-1</span></span> |<span data-ttu-id="6639f-517">10.0.0.11</span><span class="sxs-lookup"><span data-stu-id="6639f-517">10.0.0.11</span></span> |

### <span data-ttu-id="6639f-518"><a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a>Ana bilgisayar adları ve hello SAP ASCS/SCS kümelenmiş örneği ve DBMS kümelenmiş örneği için statik IP adresleri</span><span class="sxs-lookup"><span data-stu-id="6639f-518"><a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a> Host names and static IP addresses for hello SAP ASCS/SCS clustered instance and DBMS clustered instance</span></span>

<span data-ttu-id="6639f-519">Şirket içi dağıtım için bu ayrılmış ana bilgisayar adlarını ve IP adreslerini gerekir:</span><span class="sxs-lookup"><span data-stu-id="6639f-519">For on-premises deployment, you need these reserved host names and IP addresses:</span></span>

| <span data-ttu-id="6639f-520">Sanal ana bilgisayar adı rolü</span><span class="sxs-lookup"><span data-stu-id="6639f-520">Virtual host name role</span></span> | <span data-ttu-id="6639f-521">Sanal ana bilgisayar adı</span><span class="sxs-lookup"><span data-stu-id="6639f-521">Virtual host name</span></span> | <span data-ttu-id="6639f-522">Sanal statik IP adresi</span><span class="sxs-lookup"><span data-stu-id="6639f-522">Virtual static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6639f-523">SAP ASCS/SCS ilk küme sanal ana bilgisayar adı (küme yönetimi)</span><span class="sxs-lookup"><span data-stu-id="6639f-523">SAP ASCS/SCS first cluster virtual host name (for cluster management)</span></span> |<span data-ttu-id="6639f-524">pr1 ascs VIR</span><span class="sxs-lookup"><span data-stu-id="6639f-524">pr1-ascs-vir</span></span> |<span data-ttu-id="6639f-525">10.0.0.42</span><span class="sxs-lookup"><span data-stu-id="6639f-525">10.0.0.42</span></span> |
| <span data-ttu-id="6639f-526">SAP ASCS/SCS örnek sanal ana bilgisayar adı</span><span class="sxs-lookup"><span data-stu-id="6639f-526">SAP ASCS/SCS instance virtual host name</span></span> |<span data-ttu-id="6639f-527">pr1 ascs sap</span><span class="sxs-lookup"><span data-stu-id="6639f-527">pr1-ascs-sap</span></span> |<span data-ttu-id="6639f-528">10.0.0.43</span><span class="sxs-lookup"><span data-stu-id="6639f-528">10.0.0.43</span></span> |
| <span data-ttu-id="6639f-529">SAP DBMS ikinci küme sanal ana bilgisayar adı (küme yönetimi)</span><span class="sxs-lookup"><span data-stu-id="6639f-529">SAP DBMS second cluster virtual host name (cluster management)</span></span> |<span data-ttu-id="6639f-530">pr1 dbms VIR</span><span class="sxs-lookup"><span data-stu-id="6639f-530">pr1-dbms-vir</span></span> |<span data-ttu-id="6639f-531">10.0.0.32</span><span class="sxs-lookup"><span data-stu-id="6639f-531">10.0.0.32</span></span> |

<span data-ttu-id="6639f-532">Merhaba kümesi oluşturduğunuzda, sanal ana bilgisayar adlarını hello oluşturma **pr1 ascs VIR** ve **pr1 dbms VIR** ve hello ilişkili hello kümenin kendisi yönetmek IP adresleri.</span><span class="sxs-lookup"><span data-stu-id="6639f-532">When you create hello cluster, create hello virtual host names **pr1-ascs-vir** and **pr1-dbms-vir** and hello associated IP addresses that manage hello cluster itself.</span></span> <span data-ttu-id="6639f-533">Hakkında bilgi için toodo buna ek olarak, bkz: [toplamak küme düğümleri bir küme yapılandırmasında][sap-ha-guide-8.12.1].</span><span class="sxs-lookup"><span data-stu-id="6639f-533">For information about how toodo this, see [Collect cluster nodes in a cluster configuration][sap-ha-guide-8.12.1].</span></span>

<span data-ttu-id="6639f-534">Diğer iki sanal ana bilgisayar adlarını hello el ile oluşturabilirsiniz **pr1 ascs sap** ve **pr1 dbms sap**, hello ilişkili hello DNS sunucusu, IP adresleri ve.</span><span class="sxs-lookup"><span data-stu-id="6639f-534">You can manually create hello other two virtual host names, **pr1-ascs-sap** and **pr1-dbms-sap**, and hello associated IP addresses, on hello DNS server.</span></span> <span data-ttu-id="6639f-535">Merhaba kümelenmiş SAP ASCS/SCS örneği ve kümelenmiş hello DBMS örneği bu kaynakları kullanın.</span><span class="sxs-lookup"><span data-stu-id="6639f-535">hello clustered SAP ASCS/SCS instance and hello clustered DBMS instance use these resources.</span></span> <span data-ttu-id="6639f-536">Hakkında bilgi için toodo buna ek olarak, bkz: [kümelenmiş bir SAP ASCS/SCS örneği için bir sanal ana bilgisayar adı oluşturmak][sap-ha-guide-9.1.1].</span><span class="sxs-lookup"><span data-stu-id="6639f-536">For information about how toodo this, see [Create a virtual host name for a clustered SAP ASCS/SCS instance][sap-ha-guide-9.1.1].</span></span>

### <span data-ttu-id="6639f-537"><a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a>Statik IP adresleri hello SAP sanal makineler için ayarlama</span><span class="sxs-lookup"><span data-stu-id="6639f-537"><a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a> Set static IP addresses for hello SAP virtual machines</span></span>
<span data-ttu-id="6639f-538">Kümenizdeki hello sanal makineleri toouse dağıttıktan sonra tüm sanal makineler için tooset statik IP adresleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="6639f-538">After you deploy hello virtual machines toouse in your cluster, you need tooset static IP addresses for all virtual machines.</span></span> <span data-ttu-id="6639f-539">Bunu hello Azure sanal ağ yapılandırması ve hello konuk işletim sistemi içinde değil.</span><span class="sxs-lookup"><span data-stu-id="6639f-539">Do this in hello Azure Virtual Network configuration, and not in hello guest operating system.</span></span>

1.  <span data-ttu-id="6639f-540">Hello Azure portal, seçin **kaynak grubu** > **ağ kartı** > **ayarları** > **IP adresi** .</span><span class="sxs-lookup"><span data-stu-id="6639f-540">In hello Azure portal, select **Resource Group** > **Network Card** > **Settings** > **IP Address**.</span></span>
2.  <span data-ttu-id="6639f-541">Merhaba üzerinde **IP adreslerini** dikey altında **atama**seçin **statik**.</span><span class="sxs-lookup"><span data-stu-id="6639f-541">On hello **IP addresses** blade, under **Assignment**, select **Static**.</span></span> <span data-ttu-id="6639f-542">Merhaba, **IP adresi** kutusuna, toouse istediğiniz hello IP adresini girin.</span><span class="sxs-lookup"><span data-stu-id="6639f-542">In hello **IP address** box, enter hello IP address that you want toouse.</span></span>

  > [!NOTE]
  > <span data-ttu-id="6639f-543">Merhaba ağ kartı hello IP adresini değiştirirseniz, toorestart hello Azure sanal makineleri tooapply gereksinim hello değiştirin.</span><span class="sxs-lookup"><span data-stu-id="6639f-543">If you change hello IP address of hello network card, you need toorestart hello Azure virtual machines tooapply hello change.</span></span>  
  >
  >

  ![Şekil 13: hello ağ kartı her bir sanal makine için statik IP adresi ayarlayın][sap-ha-guide-figure-3002]

  <span data-ttu-id="6639f-545">_**Şekil 13:** ayarlamak hello ağ kartı her bir sanal makine için statik IP adresleri_</span><span class="sxs-lookup"><span data-stu-id="6639f-545">_**Figure 13:** Set static IP addresses for hello network card of each virtual machine_</span></span>

  <span data-ttu-id="6639f-546">Bu, tüm ağ arabirimleri için diğer bir deyişle, Active Directory DNS hizmetiniz için toouse istediğiniz sanal makineleri de dahil olmak üzere tüm sanal makineler için tekrarlayın.</span><span class="sxs-lookup"><span data-stu-id="6639f-546">Repeat this step for all network interfaces, that is, for all virtual machines, including virtual machines that you want toouse for your Active Directory/DNS service.</span></span>

<span data-ttu-id="6639f-547">Bizim örneğimizde, bu sanal makineleri ve statik IP adresleri vardır:</span><span class="sxs-lookup"><span data-stu-id="6639f-547">In our example, we have these virtual machines and static IP addresses:</span></span>

| <span data-ttu-id="6639f-548">Sanal makine rolü</span><span class="sxs-lookup"><span data-stu-id="6639f-548">Virtual machine role</span></span> | <span data-ttu-id="6639f-549">Sanal makine ana bilgisayar adı</span><span class="sxs-lookup"><span data-stu-id="6639f-549">Virtual machine host name</span></span> | <span data-ttu-id="6639f-550">Ağ kartı adı</span><span class="sxs-lookup"><span data-stu-id="6639f-550">Network card name</span></span> | <span data-ttu-id="6639f-551">Statik IP adresi</span><span class="sxs-lookup"><span data-stu-id="6639f-551">Static IP address</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6639f-552">İlk SAP uygulama sunucusu örneği</span><span class="sxs-lookup"><span data-stu-id="6639f-552">First SAP Application Server instance</span></span> |<span data-ttu-id="6639f-553">pr1 dı 0</span><span class="sxs-lookup"><span data-stu-id="6639f-553">pr1-di-0</span></span> |<span data-ttu-id="6639f-554">pr1-NIC-dı-0</span><span class="sxs-lookup"><span data-stu-id="6639f-554">pr1-nic-di-0</span></span> |<span data-ttu-id="6639f-555">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="6639f-555">10.0.0.50</span></span> |
| <span data-ttu-id="6639f-556">İkinci SAP uygulama sunucusu örneği</span><span class="sxs-lookup"><span data-stu-id="6639f-556">Second SAP Application Server instance</span></span> |<span data-ttu-id="6639f-557">pr1 dı 1</span><span class="sxs-lookup"><span data-stu-id="6639f-557">pr1-di-1</span></span> |<span data-ttu-id="6639f-558">pr1-NIC-dı-1</span><span class="sxs-lookup"><span data-stu-id="6639f-558">pr1-nic-di-1</span></span> |<span data-ttu-id="6639f-559">10.0.0.51</span><span class="sxs-lookup"><span data-stu-id="6639f-559">10.0.0.51</span></span> |
| <span data-ttu-id="6639f-560">...</span><span class="sxs-lookup"><span data-stu-id="6639f-560">...</span></span> |<span data-ttu-id="6639f-561">...</span><span class="sxs-lookup"><span data-stu-id="6639f-561">...</span></span> |<span data-ttu-id="6639f-562">...</span><span class="sxs-lookup"><span data-stu-id="6639f-562">...</span></span> |<span data-ttu-id="6639f-563">...</span><span class="sxs-lookup"><span data-stu-id="6639f-563">...</span></span> |
| <span data-ttu-id="6639f-564">Son SAP uygulama sunucusu örneği</span><span class="sxs-lookup"><span data-stu-id="6639f-564">Last SAP Application Server instance</span></span> |<span data-ttu-id="6639f-565">pr1 dı 5</span><span class="sxs-lookup"><span data-stu-id="6639f-565">pr1-di-5</span></span> |<span data-ttu-id="6639f-566">pr1-NIC-dı-5</span><span class="sxs-lookup"><span data-stu-id="6639f-566">pr1-nic-di-5</span></span> |<span data-ttu-id="6639f-567">10.0.0.55</span><span class="sxs-lookup"><span data-stu-id="6639f-567">10.0.0.55</span></span> |
| <span data-ttu-id="6639f-568">İlk küme düğümüne ASCS/SCS örneği için</span><span class="sxs-lookup"><span data-stu-id="6639f-568">First cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="6639f-569">pr1 ascs 0</span><span class="sxs-lookup"><span data-stu-id="6639f-569">pr1-ascs-0</span></span> |<span data-ttu-id="6639f-570">pr1-NIC-ascs-0</span><span class="sxs-lookup"><span data-stu-id="6639f-570">pr1-nic-ascs-0</span></span> |<span data-ttu-id="6639f-571">10.0.0.40</span><span class="sxs-lookup"><span data-stu-id="6639f-571">10.0.0.40</span></span> |
| <span data-ttu-id="6639f-572">İkinci küme düğümü ASCS/SCS örneği için</span><span class="sxs-lookup"><span data-stu-id="6639f-572">Second cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="6639f-573">pr1 ascs 1</span><span class="sxs-lookup"><span data-stu-id="6639f-573">pr1-ascs-1</span></span> |<span data-ttu-id="6639f-574">pr1-NIC-ascs-1</span><span class="sxs-lookup"><span data-stu-id="6639f-574">pr1-nic-ascs-1</span></span> |<span data-ttu-id="6639f-575">10.0.0.41</span><span class="sxs-lookup"><span data-stu-id="6639f-575">10.0.0.41</span></span> |
| <span data-ttu-id="6639f-576">İlk küme düğümüne DBMS örneği için</span><span class="sxs-lookup"><span data-stu-id="6639f-576">First cluster node for DBMS instance</span></span> |<span data-ttu-id="6639f-577">pr1-db-0</span><span class="sxs-lookup"><span data-stu-id="6639f-577">pr1-db-0</span></span> |<span data-ttu-id="6639f-578">pr1-NIC-db-0</span><span class="sxs-lookup"><span data-stu-id="6639f-578">pr1-nic-db-0</span></span> |<span data-ttu-id="6639f-579">10.0.0.30</span><span class="sxs-lookup"><span data-stu-id="6639f-579">10.0.0.30</span></span> |
| <span data-ttu-id="6639f-580">DBMS örneği için ikinci küme düğümü</span><span class="sxs-lookup"><span data-stu-id="6639f-580">Second cluster node for DBMS instance</span></span> |<span data-ttu-id="6639f-581">pr1-db-1</span><span class="sxs-lookup"><span data-stu-id="6639f-581">pr1-db-1</span></span> |<span data-ttu-id="6639f-582">pr1-NIC-db-1</span><span class="sxs-lookup"><span data-stu-id="6639f-582">pr1-nic-db-1</span></span> |<span data-ttu-id="6639f-583">10.0.0.31</span><span class="sxs-lookup"><span data-stu-id="6639f-583">10.0.0.31</span></span> |

### <span data-ttu-id="6639f-584"><a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a>Hello Azure iç yük dengeleyici için statik bir IP adresi ayarlayın</span><span class="sxs-lookup"><span data-stu-id="6639f-584"><a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a> Set a static IP address for hello Azure internal load balancer</span></span>

<span data-ttu-id="6639f-585">Merhaba SAP Azure Resource Manager şablonu hello SAP ASCS/SCS örnek küme ve hello DBMS küme için kullanılan bir Azure iç yük dengeleyici oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6639f-585">hello SAP Azure Resource Manager template creates an Azure internal load balancer that is used for hello SAP ASCS/SCS instance cluster and hello DBMS cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6639f-586">Merhaba SAP ASCS/SCS olan hello hello sanal ana bilgisayar adı, IP adresi hello aynı başlangıç IP adresi hello SAP ASCS/SCS iç yük dengeleyici olarak: **pr1 lb ascs**.</span><span class="sxs-lookup"><span data-stu-id="6639f-586">hello IP address of hello virtual host name of hello SAP ASCS/SCS is hello same as hello IP address of hello SAP ASCS/SCS internal load balancer: **pr1-lb-ascs**.</span></span>
> <span data-ttu-id="6639f-587">Merhaba hello sanal DBMS olduğu hello adını IP adresini hello aynı başlangıç IP adresi hello DBMS iç yük dengeleyici olarak: **pr1 lb dbms**.</span><span class="sxs-lookup"><span data-stu-id="6639f-587">hello IP address of hello virtual name of hello DBMS is hello same as hello IP address of hello DBMS internal load balancer: **pr1-lb-dbms**.</span></span>
>
>

<span data-ttu-id="6639f-588">Yük Dengeleyici tooset hello Azure iç için statik bir IP adresi:</span><span class="sxs-lookup"><span data-stu-id="6639f-588">tooset a static IP address for hello Azure internal load balancer:</span></span>

1.  <span data-ttu-id="6639f-589">Merhaba ilk dağıtım hello iç yük dengeleyici IP adresi çok ayarlar**dinamik**.</span><span class="sxs-lookup"><span data-stu-id="6639f-589">hello initial deployment sets hello internal load balancer IP address too**Dynamic**.</span></span> <span data-ttu-id="6639f-590">Merhaba hello üzerinde Azure portal'ın **IP adreslerini** dikey altında **atama**seçin **statik**.</span><span class="sxs-lookup"><span data-stu-id="6639f-590">In hello Azure portal, on hello **IP addresses** blade, under **Assignment**, select **Static**.</span></span>
2.  <span data-ttu-id="6639f-591">Başlangıç IP adresi hello iç yük dengeleyicisi ayarlayın **pr1 lb ascs** toohello IP adresini hello SAP ASCS/SCS örneğinin hello sanal ana bilgisayar adı.</span><span class="sxs-lookup"><span data-stu-id="6639f-591">Set hello IP address of hello internal load balancer **pr1-lb-ascs** toohello IP address of hello virtual host name of hello SAP ASCS/SCS instance.</span></span>
3.  <span data-ttu-id="6639f-592">Başlangıç IP adresi hello iç yük dengeleyicisi ayarlayın **pr1 lb dbms** toohello IP adresini hello DBMS örneğinin hello sanal ana bilgisayar adı.</span><span class="sxs-lookup"><span data-stu-id="6639f-592">Set hello IP address of hello internal load balancer **pr1-lb-dbms** toohello IP address of hello virtual host name of hello DBMS instance.</span></span>

  ![Şekil 14: hello SAP ASCS/SCS örneği için hello iç yük dengeleyici için statik IP adresleri ayarlayın.][sap-ha-guide-figure-3003]

  <span data-ttu-id="6639f-594">_**Şekil 14:** hello SAP ASCS/SCS örneği için hello iç yük dengeleyici için statik IP adresleri ayarlayın_</span><span class="sxs-lookup"><span data-stu-id="6639f-594">_**Figure 14:** Set static IP addresses for hello internal load balancer for hello SAP ASCS/SCS instance_</span></span>

<span data-ttu-id="6639f-595">Bizim örneğimizde, biz bu statik IP adresine sahip iki Azure iç yük dengeleyicileri vardır:</span><span class="sxs-lookup"><span data-stu-id="6639f-595">In our example, we have two Azure internal load balancers that have these static IP addresses:</span></span>

| <span data-ttu-id="6639f-596">Azure iç yük dengeleyici rol</span><span class="sxs-lookup"><span data-stu-id="6639f-596">Azure internal load balancer role</span></span> | <span data-ttu-id="6639f-597">Azure iç yük dengeleyicisi adı</span><span class="sxs-lookup"><span data-stu-id="6639f-597">Azure internal load balancer name</span></span> | <span data-ttu-id="6639f-598">Statik IP adresi</span><span class="sxs-lookup"><span data-stu-id="6639f-598">Static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6639f-599">SAP ASCS/SCS iç yük dengeleyici örneği</span><span class="sxs-lookup"><span data-stu-id="6639f-599">SAP ASCS/SCS instance internal load balancer</span></span> |<span data-ttu-id="6639f-600">pr1 lb ascs</span><span class="sxs-lookup"><span data-stu-id="6639f-600">pr1-lb-ascs</span></span> |<span data-ttu-id="6639f-601">10.0.0.43</span><span class="sxs-lookup"><span data-stu-id="6639f-601">10.0.0.43</span></span> |
| <span data-ttu-id="6639f-602">SAP DBMS iç yük dengeleyici</span><span class="sxs-lookup"><span data-stu-id="6639f-602">SAP DBMS internal load balancer</span></span> |<span data-ttu-id="6639f-603">pr1 lb dbms</span><span class="sxs-lookup"><span data-stu-id="6639f-603">pr1-lb-dbms</span></span> |<span data-ttu-id="6639f-604">10.0.0.33</span><span class="sxs-lookup"><span data-stu-id="6639f-604">10.0.0.33</span></span> |


### <span data-ttu-id="6639f-605"><a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a>Varsayılan ASCS/SCS Yük Dengeleme kuralları hello Azure iç yük dengeleyici için</span><span class="sxs-lookup"><span data-stu-id="6639f-605"><a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a> Default ASCS/SCS load balancing rules for hello Azure internal load balancer</span></span>

<span data-ttu-id="6639f-606">Merhaba SAP Azure Resource Manager şablonu ihtiyacınız hello bağlantı noktalarını oluşturur:</span><span class="sxs-lookup"><span data-stu-id="6639f-606">hello SAP Azure Resource Manager template creates hello ports you need:</span></span>
* <span data-ttu-id="6639f-607">Bir ABAP ASCS örneğiyle hello varsayılan örnek numarasını **00**</span><span class="sxs-lookup"><span data-stu-id="6639f-607">An ABAP ASCS instance, with hello default instance number **00**</span></span>
* <span data-ttu-id="6639f-608">Bir Java SCS örneğiyle hello varsayılan örnek numarasını **01**</span><span class="sxs-lookup"><span data-stu-id="6639f-608">A Java SCS instance, with hello default instance number **01**</span></span>

<span data-ttu-id="6639f-609">SAP ASCS/SCS örneğinizi yüklediğinizde hello varsayılan örnek numarasını kullanmalıdır **00** ABAP ASCS örneği ve hello varsayılan örneği numaranızı için **01** Java SCS Örneğiniz için.</span><span class="sxs-lookup"><span data-stu-id="6639f-609">When you install your SAP ASCS/SCS instance, you must use hello default instance number **00** for your ABAP ASCS instance and hello default instance number **01** for your Java SCS instance.</span></span>

<span data-ttu-id="6639f-610">Ardından, gerekli iç Yük Dengeleme hello SAP NetWeaver bağlantı noktaları için uç noktaları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6639f-610">Next, create required internal load balancing endpoints for hello SAP NetWeaver ports.</span></span>

<span data-ttu-id="6639f-611">İç Yük Dengeleme uç noktaları, ilk olarak, bu Yük Dengeleme hello SAP NetWeaver ABAP ASCS bağlantı noktaları için uç noktalar oluşturmak toocreate gerekli:</span><span class="sxs-lookup"><span data-stu-id="6639f-611">toocreate required internal load balancing endpoints, first, create these load balancing endpoints for hello SAP NetWeaver ABAP ASCS ports:</span></span>

| <span data-ttu-id="6639f-612">Hizmet/Yük Dengeleme kuralı adı</span><span class="sxs-lookup"><span data-stu-id="6639f-612">Service/load balancing rule name</span></span> | <span data-ttu-id="6639f-613">Varsayılan bağlantı noktası numaraları</span><span class="sxs-lookup"><span data-stu-id="6639f-613">Default port numbers</span></span> | <span data-ttu-id="6639f-614">Somut için bağlantı noktalarını (ASCS örneği ile örnek numarasını 00) (ERS 10 ile)</span><span class="sxs-lookup"><span data-stu-id="6639f-614">Concrete ports for (ASCS instance with instance number 00) (ERS with 10)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6639f-615">Sıraya alma sunucu / *lbrule3200*</span><span class="sxs-lookup"><span data-stu-id="6639f-615">Enqueue Server / *lbrule3200*</span></span> |<span data-ttu-id="6639f-616">32 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="6639f-616">32<*InstanceNumber*></span></span> |<span data-ttu-id="6639f-617">3200</span><span class="sxs-lookup"><span data-stu-id="6639f-617">3200</span></span> |
| <span data-ttu-id="6639f-618">ABAP ileti sunucusu / *lbrule3600*</span><span class="sxs-lookup"><span data-stu-id="6639f-618">ABAP Message Server / *lbrule3600*</span></span> |<span data-ttu-id="6639f-619">36 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="6639f-619">36<*InstanceNumber*></span></span> |<span data-ttu-id="6639f-620">3600</span><span class="sxs-lookup"><span data-stu-id="6639f-620">3600</span></span> |
| <span data-ttu-id="6639f-621">İç ABAP ileti / *lbrule3900*</span><span class="sxs-lookup"><span data-stu-id="6639f-621">Internal ABAP Message / *lbrule3900*</span></span> |<span data-ttu-id="6639f-622">39 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="6639f-622">39<*InstanceNumber*></span></span> |<span data-ttu-id="6639f-623">3900</span><span class="sxs-lookup"><span data-stu-id="6639f-623">3900</span></span> |
| <span data-ttu-id="6639f-624">Sunucu HTTP iletisi / *Lbrule8100*</span><span class="sxs-lookup"><span data-stu-id="6639f-624">Message Server HTTP / *Lbrule8100*</span></span> |<span data-ttu-id="6639f-625">81 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="6639f-625">81<*InstanceNumber*></span></span> |<span data-ttu-id="6639f-626">8100</span><span class="sxs-lookup"><span data-stu-id="6639f-626">8100</span></span> |
| <span data-ttu-id="6639f-627">SAP başlangıç hizmet ASCS HTTP / *Lbrule50013*</span><span class="sxs-lookup"><span data-stu-id="6639f-627">SAP Start Service ASCS HTTP / *Lbrule50013*</span></span> |<span data-ttu-id="6639f-628">5 <*InstanceNumber*> 13</span><span class="sxs-lookup"><span data-stu-id="6639f-628">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="6639f-629">50013</span><span class="sxs-lookup"><span data-stu-id="6639f-629">50013</span></span> |
| <span data-ttu-id="6639f-630">SAP başlangıç hizmet ASCS HTTPS / *Lbrule50014*</span><span class="sxs-lookup"><span data-stu-id="6639f-630">SAP Start Service ASCS HTTPS / *Lbrule50014*</span></span> |<span data-ttu-id="6639f-631">5 <*InstanceNumber*> 14</span><span class="sxs-lookup"><span data-stu-id="6639f-631">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="6639f-632">50014</span><span class="sxs-lookup"><span data-stu-id="6639f-632">50014</span></span> |
| <span data-ttu-id="6639f-633">Sıraya alma çoğaltma / *Lbrule50016*</span><span class="sxs-lookup"><span data-stu-id="6639f-633">Enqueue Replication / *Lbrule50016*</span></span> |<span data-ttu-id="6639f-634">5 <*InstanceNumber*> 16</span><span class="sxs-lookup"><span data-stu-id="6639f-634">5<*InstanceNumber*>16</span></span> |<span data-ttu-id="6639f-635">50016</span><span class="sxs-lookup"><span data-stu-id="6639f-635">50016</span></span> |
| <span data-ttu-id="6639f-636">SAP başlangıç hizmeti ERS HTTP *Lbrule51013*</span><span class="sxs-lookup"><span data-stu-id="6639f-636">SAP Start Service ERS HTTP *Lbrule51013*</span></span> |<span data-ttu-id="6639f-637">5 <*InstanceNumber*> 13</span><span class="sxs-lookup"><span data-stu-id="6639f-637">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="6639f-638">51013</span><span class="sxs-lookup"><span data-stu-id="6639f-638">51013</span></span> |
| <span data-ttu-id="6639f-639">SAP başlangıç hizmeti ERS HTTP *Lbrule51014*</span><span class="sxs-lookup"><span data-stu-id="6639f-639">SAP Start Service ERS HTTP *Lbrule51014*</span></span> |<span data-ttu-id="6639f-640">5 <*InstanceNumber*> 14</span><span class="sxs-lookup"><span data-stu-id="6639f-640">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="6639f-641">51014</span><span class="sxs-lookup"><span data-stu-id="6639f-641">51014</span></span> |
| <span data-ttu-id="6639f-642">RM win *Lbrule5985*</span><span class="sxs-lookup"><span data-stu-id="6639f-642">Win RM *Lbrule5985*</span></span> | |<span data-ttu-id="6639f-643">5985</span><span class="sxs-lookup"><span data-stu-id="6639f-643">5985</span></span> |
| <span data-ttu-id="6639f-644">Dosya Paylaşımı *Lbrule445*</span><span class="sxs-lookup"><span data-stu-id="6639f-644">File Share *Lbrule445*</span></span> | |<span data-ttu-id="6639f-645">445</span><span class="sxs-lookup"><span data-stu-id="6639f-645">445</span></span> |

<span data-ttu-id="6639f-646">_**Tablo 1:** bağlantı noktası numaralarını hello SAP NetWeaver ABAP ASCS örnekleri_</span><span class="sxs-lookup"><span data-stu-id="6639f-646">_**Table 1:** Port numbers of hello SAP NetWeaver ABAP ASCS instances_</span></span>

<span data-ttu-id="6639f-647">Ardından, bu Yük Dengeleme hello SAP NetWeaver Java SCS bağlantı noktaları için uç nokta oluşturun:</span><span class="sxs-lookup"><span data-stu-id="6639f-647">Then, create these load balancing endpoints for hello SAP NetWeaver Java SCS ports:</span></span>

| <span data-ttu-id="6639f-648">Hizmet/Yük Dengeleme kuralı adı</span><span class="sxs-lookup"><span data-stu-id="6639f-648">Service/load balancing rule name</span></span> | <span data-ttu-id="6639f-649">Varsayılan bağlantı noktası numaraları</span><span class="sxs-lookup"><span data-stu-id="6639f-649">Default port numbers</span></span> | <span data-ttu-id="6639f-650">Somut için bağlantı noktalarını (SCS örneği ile örnek numarasını 01) (ERS 11 ile)</span><span class="sxs-lookup"><span data-stu-id="6639f-650">Concrete ports for (SCS instance with instance number 01) (ERS with 11)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6639f-651">Sıraya alma sunucu / *lbrule3201*</span><span class="sxs-lookup"><span data-stu-id="6639f-651">Enqueue Server / *lbrule3201*</span></span> |<span data-ttu-id="6639f-652">32 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="6639f-652">32<*InstanceNumber*></span></span> |<span data-ttu-id="6639f-653">3201</span><span class="sxs-lookup"><span data-stu-id="6639f-653">3201</span></span> |
| <span data-ttu-id="6639f-654">Ağ Geçidi sunucusu / *lbrule3301*</span><span class="sxs-lookup"><span data-stu-id="6639f-654">Gateway Server / *lbrule3301*</span></span> |<span data-ttu-id="6639f-655">33 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="6639f-655">33<*InstanceNumber*></span></span> |<span data-ttu-id="6639f-656">3301</span><span class="sxs-lookup"><span data-stu-id="6639f-656">3301</span></span> |
| <span data-ttu-id="6639f-657">Java ileti sunucusu / *lbrule3900*</span><span class="sxs-lookup"><span data-stu-id="6639f-657">Java Message Server / *lbrule3900*</span></span> |<span data-ttu-id="6639f-658">39 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="6639f-658">39<*InstanceNumber*></span></span> |<span data-ttu-id="6639f-659">3901</span><span class="sxs-lookup"><span data-stu-id="6639f-659">3901</span></span> |
| <span data-ttu-id="6639f-660">Sunucu HTTP iletisi / *Lbrule8101*</span><span class="sxs-lookup"><span data-stu-id="6639f-660">Message Server HTTP / *Lbrule8101*</span></span> |<span data-ttu-id="6639f-661">81 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="6639f-661">81<*InstanceNumber*></span></span> |<span data-ttu-id="6639f-662">8101</span><span class="sxs-lookup"><span data-stu-id="6639f-662">8101</span></span> |
| <span data-ttu-id="6639f-663">SAP başlangıç hizmet SCS HTTP / *Lbrule50113*</span><span class="sxs-lookup"><span data-stu-id="6639f-663">SAP Start Service SCS HTTP / *Lbrule50113*</span></span> |<span data-ttu-id="6639f-664">5 <*InstanceNumber*> 13</span><span class="sxs-lookup"><span data-stu-id="6639f-664">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="6639f-665">50113</span><span class="sxs-lookup"><span data-stu-id="6639f-665">50113</span></span> |
| <span data-ttu-id="6639f-666">SAP başlangıç hizmet SCS HTTPS / *Lbrule50114*</span><span class="sxs-lookup"><span data-stu-id="6639f-666">SAP Start Service SCS HTTPS / *Lbrule50114*</span></span> |<span data-ttu-id="6639f-667">5 <*InstanceNumber*> 14</span><span class="sxs-lookup"><span data-stu-id="6639f-667">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="6639f-668">50114</span><span class="sxs-lookup"><span data-stu-id="6639f-668">50114</span></span> |
| <span data-ttu-id="6639f-669">Sıraya alma çoğaltma / *Lbrule50116*</span><span class="sxs-lookup"><span data-stu-id="6639f-669">Enqueue Replication / *Lbrule50116*</span></span> |<span data-ttu-id="6639f-670">5 <*InstanceNumber*> 16</span><span class="sxs-lookup"><span data-stu-id="6639f-670">5<*InstanceNumber*>16</span></span> |<span data-ttu-id="6639f-671">50116</span><span class="sxs-lookup"><span data-stu-id="6639f-671">50116</span></span> |
| <span data-ttu-id="6639f-672">SAP başlangıç hizmeti ERS HTTP *Lbrule51113*</span><span class="sxs-lookup"><span data-stu-id="6639f-672">SAP Start Service ERS HTTP *Lbrule51113*</span></span> |<span data-ttu-id="6639f-673">5 <*InstanceNumber*> 13</span><span class="sxs-lookup"><span data-stu-id="6639f-673">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="6639f-674">51113</span><span class="sxs-lookup"><span data-stu-id="6639f-674">51113</span></span> |
| <span data-ttu-id="6639f-675">SAP başlangıç hizmeti ERS HTTP *Lbrule51114*</span><span class="sxs-lookup"><span data-stu-id="6639f-675">SAP Start Service ERS HTTP *Lbrule51114*</span></span> |<span data-ttu-id="6639f-676">5 <*InstanceNumber*> 14</span><span class="sxs-lookup"><span data-stu-id="6639f-676">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="6639f-677">51114</span><span class="sxs-lookup"><span data-stu-id="6639f-677">51114</span></span> |
| <span data-ttu-id="6639f-678">RM win *Lbrule5985*</span><span class="sxs-lookup"><span data-stu-id="6639f-678">Win RM *Lbrule5985*</span></span> | |<span data-ttu-id="6639f-679">5985</span><span class="sxs-lookup"><span data-stu-id="6639f-679">5985</span></span> |
| <span data-ttu-id="6639f-680">Dosya Paylaşımı *Lbrule445*</span><span class="sxs-lookup"><span data-stu-id="6639f-680">File Share *Lbrule445*</span></span> | |<span data-ttu-id="6639f-681">445</span><span class="sxs-lookup"><span data-stu-id="6639f-681">445</span></span> |

<span data-ttu-id="6639f-682">_**Tablo 2:** bağlantı noktası numaralarını hello SAP NetWeaver Java SCS örnekleri_</span><span class="sxs-lookup"><span data-stu-id="6639f-682">_**Table 2:** Port numbers of hello SAP NetWeaver Java SCS instances_</span></span>

![Şekil 15: varsayılan ASCS/SCS Yük Dengeleme kuralları hello Azure iç yük dengeleyici için][sap-ha-guide-figure-3004]

<span data-ttu-id="6639f-684">_**Şekil 15:** varsayılan ASCS/SCS Yük Dengeleme kuralları hello Azure iç yük dengeleyici için_</span><span class="sxs-lookup"><span data-stu-id="6639f-684">_**Figure 15:** Default ASCS/SCS load balancing rules for hello Azure internal load balancer_</span></span>

<span data-ttu-id="6639f-685">Merhaba yük dengeleyici hello IP adresi ayarlamak **pr1 lb dbms** toohello IP adresini hello DBMS örneğinin hello sanal ana bilgisayar adı.</span><span class="sxs-lookup"><span data-stu-id="6639f-685">Set hello IP address of hello load balancer **pr1-lb-dbms** toohello IP address of hello virtual host name of hello DBMS instance.</span></span>

### <span data-ttu-id="6639f-686"><a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a>Merhaba ASCS/SCS varsayılan Yük Dengeleme kuralları hello Azure iç yük dengeleyici için değiştirme</span><span class="sxs-lookup"><span data-stu-id="6639f-686"><a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a> Change hello ASCS/SCS default load balancing rules for hello Azure internal load balancer</span></span>

<span data-ttu-id="6639f-687">Merhaba SAP ASCS veya SCS örnekleri için toouse farklı numaraları istiyorsanız, hello adları ve değerleri kendi bağlantı noktalarının varsayılan değerleri değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6639f-687">If you want toouse different numbers for hello SAP ASCS or SCS instances, you must change hello names and values of their ports from default values.</span></span>

1.  <span data-ttu-id="6639f-688">Hello Azure portal, seçin  **<* SID*> - lb - ascs yük dengeleyici ** > **Yük Dengeleme kuralları**.</span><span class="sxs-lookup"><span data-stu-id="6639f-688">In hello Azure portal, select **<*SID*>-lb-ascs load balancer** > **Load Balancing Rules**.</span></span>
2.  <span data-ttu-id="6639f-689">Tüm Yük Dengeleme toohello SAP ASCS veya SCS örnek ait kuralları için bu değerleri değiştirin:</span><span class="sxs-lookup"><span data-stu-id="6639f-689">For all load balancing rules that belong toohello SAP ASCS or SCS instance, change these values:</span></span>

  * <span data-ttu-id="6639f-690">Ad</span><span class="sxs-lookup"><span data-stu-id="6639f-690">Name</span></span>
  * <span data-ttu-id="6639f-691">Bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="6639f-691">Port</span></span>
  * <span data-ttu-id="6639f-692">Arka uç bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="6639f-692">Back-end port</span></span>

  <span data-ttu-id="6639f-693">Örneğin, toochange hello varsayılan ASCS örneği numarasından 00 too31 istiyorsanız, Tablo 1'de listelenen tüm bağlantı noktaları toomake hello değişiklikleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="6639f-693">For example, if you want toochange hello default ASCS instance number from 00 too31, you need toomake hello changes for all ports listed in Table 1.</span></span>

  <span data-ttu-id="6639f-694">Bağlantı noktası için bir güncelleştirme örneği *lbrule3200*.</span><span class="sxs-lookup"><span data-stu-id="6639f-694">Here's an example of an update for port *lbrule3200*.</span></span>

  ![Şekil 16: Merhaba ASCS/SCS varsayılan Yük Dengeleme kuralları hello Azure iç yük dengeleyici için değiştirme][sap-ha-guide-figure-3005]

  <span data-ttu-id="6639f-696">_**Şekil 16:** değişiklik hello ASCS/SCS varsayılan Yük Dengeleme kuralları hello Azure iç yük dengeleyici için_</span><span class="sxs-lookup"><span data-stu-id="6639f-696">_**Figure 16:** Change hello ASCS/SCS default load balancing rules for hello Azure internal load balancer_</span></span>

### <span data-ttu-id="6639f-697"><a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a>Windows sanal makineleri toohello etki alanı ekleme</span><span class="sxs-lookup"><span data-stu-id="6639f-697"><a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a> Add Windows virtual machines toohello domain</span></span>

<span data-ttu-id="6639f-698">Bir statik IP adresi toohello sanal makineleri atadıktan sonra hello sanal makineleri toohello etki alanına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6639f-698">After you assign a static IP address toohello virtual machines, add hello virtual machines toohello domain.</span></span>

![Şekil 17: bir sanal makine tooa etki alanına ekleme][sap-ha-guide-figure-3006]

<span data-ttu-id="6639f-700">_**Şekil 17:** bir sanal makine tooa etki alanına ekleme_</span><span class="sxs-lookup"><span data-stu-id="6639f-700">_**Figure 17:** Add a virtual machine tooa domain_</span></span>

### <span data-ttu-id="6639f-701"><a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a>Kayıt defteri girdilerini hello SAP ASCS/SCS örneği her iki küme düğümleri üzerinde ekleyin</span><span class="sxs-lookup"><span data-stu-id="6639f-701"><a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a> Add registry entries on both cluster nodes of hello SAP ASCS/SCS instance</span></span>

<span data-ttu-id="6639f-702">Azure yük dengeleyici hello bağlantıları ayarlanmış bir süre boyunca boşta olduğunda kapanır bağlantıları (boşta zaman aşımı) zaman bir iç yük dengeleyici sahiptir.</span><span class="sxs-lookup"><span data-stu-id="6639f-702">Azure Load Balancer has an internal load balancer that closes connections when hello connections are idle for a set period of time (an idle timeout).</span></span> <span data-ttu-id="6639f-703">Merhaba ilk sıraya alma/dequeue gereksinimlerini toobe gönderilen istek hemen SAP iş iletişim örnekleri açık bağlantıları toohello SAP sıraya alma işlemlerinde işleyin.</span><span class="sxs-lookup"><span data-stu-id="6639f-703">SAP work processes in dialog instances open connections toohello SAP enqueue process as soon as hello first enqueue/dequeue request needs toobe sent.</span></span> <span data-ttu-id="6639f-704">Bu bağlantılar genellikle hello iş işlemi kadar kurulan kalmasını veya hello sıraya alma işlemi yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="6639f-704">These connections usually remain established until hello work process or hello enqueue process restarts.</span></span> <span data-ttu-id="6639f-705">Ancak, belirlenen süre Hello bağlantı boşta kalırsa Azure iç yük dengeleyici kapanır hello bağlantıları hello.</span><span class="sxs-lookup"><span data-stu-id="6639f-705">However, if hello connection is idle for a set period of time, hello Azure internal load balancer closes hello connections.</span></span> <span data-ttu-id="6639f-706">Artık yoksa hello SAP iş işlemi hello bağlantı toohello sıraya alma işlemini yeniden kurar çünkü bu bir sorun değildir.</span><span class="sxs-lookup"><span data-stu-id="6639f-706">This isn't a problem because hello SAP work process reestablishes hello connection toohello enqueue process if it no longer exists.</span></span> <span data-ttu-id="6639f-707">Bu etkinlikler SAP işlemlerin hello Geliştirici izlemeleri belgelenen, ancak bunlar büyük miktarda ek içerik bu izlemeler oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6639f-707">These activities are documented in hello developer traces of SAP processes, but they create a large amount of extra content in those traces.</span></span> <span data-ttu-id="6639f-708">İyi bir fikir toochange hello TCP/IP'yi olan `KeepAliveTime` ve `KeepAliveInterval` her iki küme düğümlerinde.</span><span class="sxs-lookup"><span data-stu-id="6639f-708">It's a good idea toochange hello TCP/IP `KeepAliveTime` and `KeepAliveInterval` on both cluster nodes.</span></span> <span data-ttu-id="6639f-709">Bu değişiklikler hello TCP/IP parametreleri parametrelerle hello makalenin sonraki bölümlerinde açıklanan SAP profili ile birleştirin.</span><span class="sxs-lookup"><span data-stu-id="6639f-709">Combine these changes in hello TCP/IP parameters with SAP profile parameters, described later in hello article.</span></span>

<span data-ttu-id="6639f-710">tooadd kayıt defteri girdileri hello SAP ASCS/SCS örneğinin her iki küme düğümlerinde ilk olarak, bu Windows kayıt defteri girdileri SAP ASCS/SCS için hem Windows Küme düğümlerinde ekleyin:</span><span class="sxs-lookup"><span data-stu-id="6639f-710">tooadd registry entries on both cluster nodes of hello SAP ASCS/SCS instance, first, add these Windows registry entries on both Windows cluster nodes for SAP ASCS/SCS:</span></span>

| <span data-ttu-id="6639f-711">Yol</span><span class="sxs-lookup"><span data-stu-id="6639f-711">Path</span></span> | <span data-ttu-id="6639f-712">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span><span class="sxs-lookup"><span data-stu-id="6639f-712">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span></span> |
| --- | --- |
| <span data-ttu-id="6639f-713">Değişken adı</span><span class="sxs-lookup"><span data-stu-id="6639f-713">Variable name</span></span> |`KeepAliveTime` |
| <span data-ttu-id="6639f-714">Değişken türü</span><span class="sxs-lookup"><span data-stu-id="6639f-714">Variable type</span></span> |<span data-ttu-id="6639f-715">REG_DWORD (ondalık)</span><span class="sxs-lookup"><span data-stu-id="6639f-715">REG_DWORD (Decimal)</span></span> |
| <span data-ttu-id="6639f-716">Değer</span><span class="sxs-lookup"><span data-stu-id="6639f-716">Value</span></span> |<span data-ttu-id="6639f-717">120000</span><span class="sxs-lookup"><span data-stu-id="6639f-717">120000</span></span> |
| <span data-ttu-id="6639f-718">Bağlantı toodocumentation</span><span class="sxs-lookup"><span data-stu-id="6639f-718">Link toodocumentation</span></span> |[<span data-ttu-id="6639f-719">https://technet.microsoft.com/en-us/library/cc957549.aspx</span><span class="sxs-lookup"><span data-stu-id="6639f-719">https://technet.microsoft.com/en-us/library/cc957549.aspx</span></span>](https://technet.microsoft.com/en-us/library/cc957549.aspx) |

<span data-ttu-id="6639f-720">_**Tablo 3:** değişiklik hello ilk TCP/IP'yi parametresi_</span><span class="sxs-lookup"><span data-stu-id="6639f-720">_**Table 3:** Change hello first TCP/IP parameter_</span></span>

<span data-ttu-id="6639f-721">Daha sonra bu Windows kayıt defteri girdileri SAP ASCS/SCS için hem Windows küme düğümlerine ekleyin:</span><span class="sxs-lookup"><span data-stu-id="6639f-721">Then, add this Windows registry entries on both Windows cluster nodes for SAP ASCS/SCS:</span></span>

| <span data-ttu-id="6639f-722">Yol</span><span class="sxs-lookup"><span data-stu-id="6639f-722">Path</span></span> | <span data-ttu-id="6639f-723">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span><span class="sxs-lookup"><span data-stu-id="6639f-723">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span></span> |
| --- | --- |
| <span data-ttu-id="6639f-724">Değişken adı</span><span class="sxs-lookup"><span data-stu-id="6639f-724">Variable name</span></span> |`KeepAliveInterval` |
| <span data-ttu-id="6639f-725">Değişken türü</span><span class="sxs-lookup"><span data-stu-id="6639f-725">Variable type</span></span> |<span data-ttu-id="6639f-726">REG_DWORD (ondalık)</span><span class="sxs-lookup"><span data-stu-id="6639f-726">REG_DWORD (Decimal)</span></span> |
| <span data-ttu-id="6639f-727">Değer</span><span class="sxs-lookup"><span data-stu-id="6639f-727">Value</span></span> |<span data-ttu-id="6639f-728">120000</span><span class="sxs-lookup"><span data-stu-id="6639f-728">120000</span></span> |
| <span data-ttu-id="6639f-729">Bağlantı toodocumentation</span><span class="sxs-lookup"><span data-stu-id="6639f-729">Link toodocumentation</span></span> |[<span data-ttu-id="6639f-730">https://technet.microsoft.com/en-us/library/cc957548.aspx</span><span class="sxs-lookup"><span data-stu-id="6639f-730">https://technet.microsoft.com/en-us/library/cc957548.aspx</span></span>](https://technet.microsoft.com/en-us/library/cc957548.aspx) |

<span data-ttu-id="6639f-731">_**Tablo 4:** değişiklik hello ikinci TCP/IP'yi parametresi_</span><span class="sxs-lookup"><span data-stu-id="6639f-731">_**Table 4:** Change hello second TCP/IP parameter_</span></span>

<span data-ttu-id="6639f-732">**tooapply hello değişiklikler, her iki küme düğümünü yeniden**.</span><span class="sxs-lookup"><span data-stu-id="6639f-732">**tooapply hello changes, restart both cluster nodes**.</span></span>

### <span data-ttu-id="6639f-733"><a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a>Bir Windows Server Yük Devretme Kümelemesi küme SAP ASCS/SCS örneği için ayarlama</span><span class="sxs-lookup"><span data-stu-id="6639f-733"><a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a> Set up a Windows Server Failover Clustering cluster for an SAP ASCS/SCS instance</span></span>

<span data-ttu-id="6639f-734">Bir Windows Server Yük Devretme Kümelemesi küme SAP ASCS/SCS örneği için ayarlama, bu görevleri içerir:</span><span class="sxs-lookup"><span data-stu-id="6639f-734">Setting up a Windows Server Failover Clustering cluster for an SAP ASCS/SCS instance involves these tasks:</span></span>

- <span data-ttu-id="6639f-735">Bir küme yapılandırmasında Hello küme düğümleri toplama</span><span class="sxs-lookup"><span data-stu-id="6639f-735">Collecting hello cluster nodes in a cluster configuration</span></span>
- <span data-ttu-id="6639f-736">Bir küme dosya paylaşımı tanığı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6639f-736">Configuring a cluster file share witness</span></span>

#### <span data-ttu-id="6639f-737"><a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a>Bir küme yapılandırmasında Hello küme düğümleri Topla</span><span class="sxs-lookup"><span data-stu-id="6639f-737"><a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a> Collect hello cluster nodes in a cluster configuration</span></span>

1.  <span data-ttu-id="6639f-738">Hello Ekle rol ve Özellik Ekleme Sihirbazı, Yük Devretme Kümelemesi tooboth küme düğümlerine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6639f-738">In hello Add Role and Features Wizard, add failover clustering tooboth cluster nodes.</span></span>
2.  <span data-ttu-id="6639f-739">Merhaba yük devretme kümesini yedeklerken, yük devretme kümesi Yöneticisi'ni kullanarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="6639f-739">Set up hello failover cluster by using Failover Cluster Manager.</span></span> <span data-ttu-id="6639f-740">Yük Devretme Kümesi Yöneticisi'nde seçin **küme oluşturma**ve ardından yalnızca hello ilk küme, düğümü A. hello adı ekleyin Merhaba İkinci düğüm henüz eklemeyin; bir sonraki adımda hello İkinci düğüm ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="6639f-740">In Failover Cluster Manager, select **Create Cluster**, and then add only hello name of hello first cluster, node A. Do not add hello second node yet; you'll add hello second node in a later step.</span></span>

  ![Şekil 18: hello sunucusunu veya hello ilk küme düğümüne sanal makine adı ekleyin][sap-ha-guide-figure-3007]

  <span data-ttu-id="6639f-742">_**Şekil 18:** hello ilk küme düğümünün Ekle hello sunucu veya sanal makine adı_</span><span class="sxs-lookup"><span data-stu-id="6639f-742">_**Figure 18:** Add hello server or virtual machine name of hello first cluster node_</span></span>

3.  <span data-ttu-id="6639f-743">Merhaba ağ (sanal ana bilgisayar adı) hello kümenin adını girin.</span><span class="sxs-lookup"><span data-stu-id="6639f-743">Enter hello network name (virtual host name) of hello cluster.</span></span>

  ![Şekil 19: hello küme adını girin][sap-ha-guide-figure-3008]

  <span data-ttu-id="6639f-745">_**Şekil 19:** hello küme adını girin_</span><span class="sxs-lookup"><span data-stu-id="6639f-745">_**Figure 19:** Enter hello cluster name_</span></span>

4.  <span data-ttu-id="6639f-746">Merhaba küme oluşturduktan sonra bir küme doğrulama testi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6639f-746">After you've created hello cluster, run a cluster validation test.</span></span>

  ![Şekil 20: hello küme doğrulama denetimini Çalıştır][sap-ha-guide-figure-3009]

  <span data-ttu-id="6639f-748">_**Şekil 20:** hello küme doğrulama denetimini Çalıştır_</span><span class="sxs-lookup"><span data-stu-id="6639f-748">_**Figure 20:** Run hello cluster validation check_</span></span>

  <span data-ttu-id="6639f-749">Bu noktada hello işleminde disklerle ilgili tüm uyarılar yoksayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6639f-749">You can ignore any warnings about disks at this point in hello process.</span></span> <span data-ttu-id="6639f-750">Bir dosya paylaşımı tanığı ve hello SIOS diskler daha sonra paylaşılan ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="6639f-750">You'll add a file share witness and hello SIOS shared disks later.</span></span> <span data-ttu-id="6639f-751">Bu aşamada, bir çekirdek sahibi olma hakkında tooworry gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="6639f-751">At this stage, you don't need tooworry about having a quorum.</span></span>

  ![Şekil 21: Çekirdek disk bulunamadı][sap-ha-guide-figure-3010]

  <span data-ttu-id="6639f-753">_**Şekil 21:** çekirdek disk bulunamadı_</span><span class="sxs-lookup"><span data-stu-id="6639f-753">_**Figure 21:** No quorum disk is found_</span></span>

  ![Şekil 22: Çekirdek küme kaynağının yeni bir IP adresi gerekiyor.][sap-ha-guide-figure-3011]

  <span data-ttu-id="6639f-755">_**Şekil 22:** çekirdek küme kaynağının yeni bir IP adresi gerekiyor_</span><span class="sxs-lookup"><span data-stu-id="6639f-755">_**Figure 22:** Core cluster resource needs a new IP address_</span></span>

5.  <span data-ttu-id="6639f-756">Merhaba çekirdek Küme hizmeti Hello IP adresini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="6639f-756">Change hello IP address of hello core cluster service.</span></span> <span data-ttu-id="6639f-757">Başlangıç IP adresi hello çekirdek Küme hizmetinin, değiştirene kadar tooone hello sanal makine düğümlerinin hello sunucusunun hello IP adresini işaret ettiğinden hello küme başlatılamıyor.</span><span class="sxs-lookup"><span data-stu-id="6639f-757">hello cluster can't start until you change hello IP address of hello core cluster service, because hello IP address of hello server points tooone of hello virtual machine nodes.</span></span> <span data-ttu-id="6639f-758">Merhaba üzerinde bunu **özellikleri** hello çekirdek küme hizmetin IP kaynak sayfası.</span><span class="sxs-lookup"><span data-stu-id="6639f-758">Do this on hello **Properties** page of hello core cluster service's IP resource.</span></span>

  <span data-ttu-id="6639f-759">Örneğin, bir IP adresi tooassign ihtiyacımız (örneğimizde **10.0.0.42**) hello küme sanal ana bilgisayar adı için **pr1 ascs VIR**.</span><span class="sxs-lookup"><span data-stu-id="6639f-759">For example, we need tooassign an IP address (in our example, **10.0.0.42**) for hello cluster virtual host name **pr1-ascs-vir**.</span></span>

  ![Şekil 23: hello Özellikleri iletişim kutusunda hello IP adresini değiştirme][sap-ha-guide-figure-3012]

  <span data-ttu-id="6639f-761">_**Şekil 23:** hello içinde **özellikleri** iletişim kutusu, hello IP adresini Değiştir_</span><span class="sxs-lookup"><span data-stu-id="6639f-761">_**Figure 23:** In hello **Properties** dialog box, change hello IP address_</span></span>

  ![Şekil 24: hello küme için ayrılmış başlangıç IP adresi atayın][sap-ha-guide-figure-3013]

  <span data-ttu-id="6639f-763">_**Şekil 24:** hello küme için ayrılmış başlangıç IP adresi atayın_</span><span class="sxs-lookup"><span data-stu-id="6639f-763">_**Figure 24:** Assign hello IP address that is reserved for hello cluster_</span></span>

6.  <span data-ttu-id="6639f-764">Merhaba küme sanal ana bilgisayar adı çevrimiçi duruma getirin.</span><span class="sxs-lookup"><span data-stu-id="6639f-764">Bring hello cluster virtual host name online.</span></span>

  ![Şekil 25: Küme çekirdek hizmeti çalışır durumda ve çalıştığından ve hello ile IP adresini düzeltin][sap-ha-guide-figure-3014]

  <span data-ttu-id="6639f-766">_**Şekil 25:** çalışan ile Merhaba IP adresini düzeltin ve küme çekirdek hizmetidir ayarlama_</span><span class="sxs-lookup"><span data-stu-id="6639f-766">_**Figure 25:** Cluster core service is up and running, and with hello correct IP address_</span></span>

7.  <span data-ttu-id="6639f-767">Merhaba ikinci küme düğümünü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6639f-767">Add hello second cluster node.</span></span>

  <span data-ttu-id="6639f-768">Merhaba çekirdek Küme hizmeti çalışır durumda olduğundan, hello İkinci düğüm ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6639f-768">Now that hello core cluster service is up and running, you can add hello second cluster node.</span></span>

  ![Şekil 26: hello İkinci düğüm ekleme][sap-ha-guide-figure-3015]

  <span data-ttu-id="6639f-770">_**Şekil 26:** Ekle hello ikinci küme düğümü_</span><span class="sxs-lookup"><span data-stu-id="6639f-770">_**Figure 26:** Add hello second cluster node_</span></span>

8.  <span data-ttu-id="6639f-771">Merhaba ikinci küme düğümü konağı için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="6639f-771">Enter a name for hello second cluster node host.</span></span>

  ![Şekil 27: hello ikinci küme düğümü ana bilgisayar adı girin][sap-ha-guide-figure-3016]

  <span data-ttu-id="6639f-773">_**Şekil 27:** hello ikinci küme düğümü ana bilgisayar adını girin_</span><span class="sxs-lookup"><span data-stu-id="6639f-773">_**Figure 27:** Enter hello second cluster node host name_</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="6639f-774">Bu hello denetleyin **tüm uygun depolama toohello küme eklemek** onay kutusu **değil** seçili.</span><span class="sxs-lookup"><span data-stu-id="6639f-774">Be sure that hello **Add all eligible storage toohello cluster** check box is **NOT** selected.</span></span>  
  >
  >

  ![Şekil 28: hello onay kutusunu işaretlemeyin][sap-ha-guide-figure-3017]

  <span data-ttu-id="6639f-776">_**Şekil 28:** yapmak **değil** hello onay kutusunu seçin_</span><span class="sxs-lookup"><span data-stu-id="6639f-776">_**Figure 28:** Do **not** select hello check box_</span></span>

  <span data-ttu-id="6639f-777">Çekirdek ve diskleri ilgili uyarılar yoksayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6639f-777">You can ignore warnings about quorum and disks.</span></span> <span data-ttu-id="6639f-778">Bölümünde açıklandığı gibi daha sonra hello çekirdek ve Paylaşım hello disk komutunu ayarlarız [SIOS DataKeeper Cluster Edition yükleme SAP ASCS/SCS küme paylaşım diski için][sap-ha-guide-8.12.3].</span><span class="sxs-lookup"><span data-stu-id="6639f-778">You'll set hello quorum and share hello disk later, as described in [Installing SIOS DataKeeper Cluster Edition for SAP ASCS/SCS cluster share disk][sap-ha-guide-8.12.3].</span></span>

  ![Şekil 29: hello disk çekirdek ilgili uyarılar yoksay][sap-ha-guide-figure-3018]

  <span data-ttu-id="6639f-780">_**Şekil 29:** hello disk çekirdek ilgili uyarılar yoksay_</span><span class="sxs-lookup"><span data-stu-id="6639f-780">_**Figure 29:** Ignore warnings about hello disk quorum_</span></span>


#### <span data-ttu-id="6639f-781"><a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a>Bir küme dosya paylaşımı tanığı Yapılandır</span><span class="sxs-lookup"><span data-stu-id="6639f-781"><a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a> Configure a cluster file share witness</span></span>

<span data-ttu-id="6639f-782">Bir küme dosya paylaşımı tanığı yapılandırma, bu görevleri içerir:</span><span class="sxs-lookup"><span data-stu-id="6639f-782">Configuring a cluster file share witness involves these tasks:</span></span>

- <span data-ttu-id="6639f-783">Bir dosya paylaşımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6639f-783">Creating a file share</span></span>
- <span data-ttu-id="6639f-784">Yük Devretme Kümesi Yöneticisi'nde Hello dosya paylaşım tanığı çekirdek ayarlama</span><span class="sxs-lookup"><span data-stu-id="6639f-784">Setting hello file share witness quorum in Failover Cluster Manager</span></span>

##### <span data-ttu-id="6639f-785"><a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a>Dosya paylaşımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6639f-785"><a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a> Create a file share</span></span>

1.  <span data-ttu-id="6639f-786">Dosya paylaşım tanığı yerine bir çekirdek diski seçin.</span><span class="sxs-lookup"><span data-stu-id="6639f-786">Select a file share witness instead of a quorum disk.</span></span> <span data-ttu-id="6639f-787">Bu seçenek SIOS DataKeeper destekler.</span><span class="sxs-lookup"><span data-stu-id="6639f-787">SIOS DataKeeper supports this option.</span></span>

  <span data-ttu-id="6639f-788">Bu makalede Hello örneklerde, Azure'da çalışan hello Active Directory DNS sunucusu hello dosya paylaşım tanığı açıktır.</span><span class="sxs-lookup"><span data-stu-id="6639f-788">In hello examples in this article, hello file share witness is on hello Active Directory/DNS server that is running in Azure.</span></span> <span data-ttu-id="6639f-789">Merhaba dosya paylaşım tanığı olarak adlandırılır **domcontr 0**.</span><span class="sxs-lookup"><span data-stu-id="6639f-789">hello file share witness is called **domcontr-0**.</span></span> <span data-ttu-id="6639f-790">Bir VPN bağlantısı tooAzure (aracılığıyla, siteden siteye VPN veya Azure ExpressRoute) yapılandırılmış çünkü Active Directory/Hizmeti şirket içi ve uygun toorun bir dosya değil. DNS sunucunuzun Tanık paylaşır.</span><span class="sxs-lookup"><span data-stu-id="6639f-790">Because you would have configured a VPN connection tooAzure (via Site-to-Site VPN or Azure ExpressRoute), your Active Directory/DNS service is on-premises and isn't suitable toorun a file share witness.</span></span>

  > [!NOTE]
  > <span data-ttu-id="6639f-791">Yalnızca şirket içi Active Directory DNS hizmeti çalışıyorsa, dosya paylaşım tanığı hello Active Directory/DNS Windows işletim sistemlerinde, şirket içi çalışan yapılandırmayın.</span><span class="sxs-lookup"><span data-stu-id="6639f-791">If your Active Directory/DNS service runs only on-premises, don't configure your file share witness on hello Active Directory/DNS Windows operating system that is running on-premises.</span></span> <span data-ttu-id="6639f-792">Azure ve Active Directory DNS şirket içi çalışan küme düğümleri arasındaki ağ gecikmesi çok büyük ve bağlantı sorunlarına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="6639f-792">Network latency between cluster nodes running in Azure and Active Directory/DNS on-premises might be too large and cause connectivity issues.</span></span> <span data-ttu-id="6639f-793">Emin tooconfigure hello dosya paylaşım tanığı Kapat toohello küme düğümünde çalışan bir Azure sanal makinesi üzerinde olabilir.</span><span class="sxs-lookup"><span data-stu-id="6639f-793">Be sure tooconfigure hello file share witness on an Azure virtual machine that is running close toohello cluster node.</span></span>  
  >
  >

  <span data-ttu-id="6639f-794">Merhaba çekirdek sürücüde en az 1024 MB boş disk alanı gerekir.</span><span class="sxs-lookup"><span data-stu-id="6639f-794">hello quorum drive needs at least 1,024 MB of free space.</span></span> <span data-ttu-id="6639f-795">2.048 MB boş disk alanı hello çekirdek sürücüsü için öneririz.</span><span class="sxs-lookup"><span data-stu-id="6639f-795">We recommend 2,048 MB of free space for hello quorum drive.</span></span>

2.  <span data-ttu-id="6639f-796">Merhaba küme adı nesnesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6639f-796">Add hello cluster name object.</span></span>

  ![Şekil 30: hello paylaşımı hello küme adı nesnesi için hello izinleri atayın][sap-ha-guide-figure-3019]

  <span data-ttu-id="6639f-798">_**Şekil 30:** hello küme adı nesnesi için hello paylaşımındaki hello izinler atama_</span><span class="sxs-lookup"><span data-stu-id="6639f-798">_**Figure 30:** Assign hello permissions on hello share for hello cluster name object_</span></span>

  <span data-ttu-id="6639f-799">Merhaba izinleri hello paylaşımı hello küme adı nesnesi için hello yetkilisi toochange veri dahil emin olun (örneğimizde **pr1 ascs VIR$**).</span><span class="sxs-lookup"><span data-stu-id="6639f-799">Be sure that hello permissions include hello authority toochange data in hello share for hello cluster name object (in our example, **pr1-ascs-vir$**).</span></span>

3.  <span data-ttu-id="6639f-800">tooadd hello küme adı nesnesi toohello listesinde **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="6639f-800">tooadd hello cluster name object toohello list, select **Add**.</span></span> <span data-ttu-id="6639f-801">Merhaba filtre toocheck bilgisayar nesnelerini, toplama toothose şekil 31'de gösterilen için değiştirin.</span><span class="sxs-lookup"><span data-stu-id="6639f-801">Change hello filter toocheck for computer objects, in addition toothose shown in Figure 31.</span></span>

  ![Şekil 31: Değişiklik hello nesne türleri tooinclude bilgisayarlar][sap-ha-guide-figure-3020]

  <span data-ttu-id="6639f-803">_**Şekil 31:** değiştirmek hello nesne türleri tooinclude bilgisayarlar_</span><span class="sxs-lookup"><span data-stu-id="6639f-803">_**Figure 31:** Change hello Object Types tooinclude computers_</span></span>

  ![Şekil 32: hello bilgisayarlar onay kutusunu seçin][sap-ha-guide-figure-3021]

  <span data-ttu-id="6639f-805">_**Şekil 32:** Select hello **bilgisayarlar** onay kutusu_</span><span class="sxs-lookup"><span data-stu-id="6639f-805">_**Figure 32:** Select hello **Computers** check box_</span></span>

4.  <span data-ttu-id="6639f-806">Şekil 31'de gösterildiği gibi hello küme adı nesnesi girin.</span><span class="sxs-lookup"><span data-stu-id="6639f-806">Enter hello cluster name object as shown in Figure 31.</span></span> <span data-ttu-id="6639f-807">Merhaba kaydı zaten oluşturulduğundan, Şekil 30 gösterildiği gibi hello izinleri değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6639f-807">Because hello record has already been created, you can change hello permissions, as shown in Figure 30.</span></span>

5.  <span data-ttu-id="6639f-808">Select hello **güvenlik** hello paylaşım ayarlayın ve ardından sekmesinde daha ayrıntılı hello küme adı nesnesi için izinleri.</span><span class="sxs-lookup"><span data-stu-id="6639f-808">Select hello **Security** tab of hello share, and then set more detailed permissions for hello cluster name object.</span></span>

  ![Şekil 33: Hello güvenlik özelliklerini ayarla hello dosya paylaşımı çekirdeğe hello küme adı nesnesi][sap-ha-guide-figure-3022]

  <span data-ttu-id="6639f-810">_**Şekil 33:** hello dosya paylaşımı çekirdek üzerinde hello küme adı nesnesi için hello güvenlik özniteliklerini ayarlama_</span><span class="sxs-lookup"><span data-stu-id="6639f-810">_**Figure 33:** Set hello security attributes for hello cluster name object on hello file share quorum_</span></span>

##### <span data-ttu-id="6639f-811"><a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a>Yük Devretme Kümesi Yöneticisi'nde Hello dosya paylaşım tanığı çekirdek ayarlayın</span><span class="sxs-lookup"><span data-stu-id="6639f-811"><a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a> Set hello file share witness quorum in Failover Cluster Manager</span></span>

1.  <span data-ttu-id="6639f-812">Merhaba yapılandırma çekirdek Ayarlama Sihirbazı'nı açın.</span><span class="sxs-lookup"><span data-stu-id="6639f-812">Open hello Configure Quorum Setting Wizard.</span></span>

  ![Şekil 34: hello yapılandırma küme çekirdeği ayar Sihirbazı Başlat][sap-ha-guide-figure-3023]

  <span data-ttu-id="6639f-814">_**Şekil 34:** başlangıç hello küme çekirdeği yapılandırma ayarı Sihirbazı_</span><span class="sxs-lookup"><span data-stu-id="6639f-814">_**Figure 34:** Start hello Configure Cluster Quorum Setting Wizard_</span></span>

2.  <span data-ttu-id="6639f-815">Merhaba üzerinde **seçin Çekirdek yapılandırmasını** sayfasında **hello çekirdek tanığı Seç**.</span><span class="sxs-lookup"><span data-stu-id="6639f-815">On hello **Select Quorum Configuration** page, select **Select hello quorum witness**.</span></span>

  ![Şekil 35: aralarından seçim yapabileceğiniz Çekirdek yapılandırmaları][sap-ha-guide-figure-3024]

  <span data-ttu-id="6639f-817">_**Şekil 35:** seçim yapabileceğiniz Çekirdek yapılandırmaları_</span><span class="sxs-lookup"><span data-stu-id="6639f-817">_**Figure 35:** Quorum configurations you can choose from_</span></span>

3.  <span data-ttu-id="6639f-818">Merhaba üzerinde **çekirdek tanığı Seç** sayfasında **bir dosya paylaşımı tanığı Yapılandır**.</span><span class="sxs-lookup"><span data-stu-id="6639f-818">On hello **Select Quorum Witness** page, select **Configure a file share witness**.</span></span>

  ![Şekil 36: Select hello dosya paylaşım tanığı][sap-ha-guide-figure-3025]

  <span data-ttu-id="6639f-820">_**Şekil 36:** hello dosya paylaşım tanığı seçin_</span><span class="sxs-lookup"><span data-stu-id="6639f-820">_**Figure 36:** Select hello file share witness_</span></span>

4.  <span data-ttu-id="6639f-821">Merhaba UNC yolu toohello dosya paylaşımı girin (örneğimizde \\domcontr 0\FSW).</span><span class="sxs-lookup"><span data-stu-id="6639f-821">Enter hello UNC path toohello file share (in our example, \\domcontr-0\FSW).</span></span> <span data-ttu-id="6639f-822">toosee hello değişiklikleri yapabilirsiniz, select listesi **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="6639f-822">toosee a list of hello changes you can make, select **Next**.</span></span>

  ![Şekil 37: hello Tanık paylaşımı için hello dosya paylaşım konumunu tanımlayın][sap-ha-guide-figure-3026]

  <span data-ttu-id="6639f-824">_**Şekil 37:** hello Tanık paylaşımı için hello dosya paylaşım konumunu tanımlayın_</span><span class="sxs-lookup"><span data-stu-id="6639f-824">_**Figure 37:** Define hello file share location for hello witness share_</span></span>

5.  <span data-ttu-id="6639f-825">Seçin ve ardından hello değişiklikleri **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="6639f-825">Select hello changes you want, and then select **Next**.</span></span> <span data-ttu-id="6639f-826">Toosuccessfully ihtiyacınız şekil 38 gösterildiği gibi hello küme yapılandırmasını yeniden yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="6639f-826">You need toosuccessfully reconfigure hello cluster configuration as shown in Figure 38.</span></span>  

  ![Şekil 38: hello küme yeniden yapılandırılması onayı][sap-ha-guide-figure-3027]

  <span data-ttu-id="6639f-828">_**Şekil 38:** hello küme yeniden yapılandırılması onayı_</span><span class="sxs-lookup"><span data-stu-id="6639f-828">_**Figure 38:** Confirmation that you've reconfigured hello cluster_</span></span>

<span data-ttu-id="6639f-829">Hello Windows Yük devretme kümesi başarıyla yükledikten sonra değişiklikler toosome eşikleri tooadapt yük devretme algılama tooconditions Azure'da yapılan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="6639f-829">After installing hello Windows Failover Cluster successfully, changes need toobe made toosome thresholds tooadapt failover detection tooconditions in Azure.</span></span> <span data-ttu-id="6639f-830">Merhaba değiştirilen parametreleri toobe belgelenmiştir bu blog: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/.</span><span class="sxs-lookup"><span data-stu-id="6639f-830">hello parameters toobe changed are documented in this blog: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/ .</span></span> <span data-ttu-id="6639f-831">Merhaba yapı, iki VM varsayarak Windows Küme yapılandırması ASCS/SCS içindir aynı alt ağda Merhaba, hello aşağıdaki parametreleri değiştirilen toobe toothese değerlerine ihtiyacı vardır:</span><span class="sxs-lookup"><span data-stu-id="6639f-831">Assuming that your two VMs that build hello Windows Cluster Configuration for ASCS/SCS are in hello same SubNet, hello following parameters need toobe changed toothese values:</span></span>
- <span data-ttu-id="6639f-832">SameSubNetDelay = 2</span><span class="sxs-lookup"><span data-stu-id="6639f-832">SameSubNetDelay = 2</span></span>
- <span data-ttu-id="6639f-833">SameSubNetThreshold = 15</span><span class="sxs-lookup"><span data-stu-id="6639f-833">SameSubNetThreshold = 15</span></span>

<span data-ttu-id="6639f-834">Bu ayarları müşterilerle test ve iyi güvenliğinin aşılmasına toobe yeterince esnektir hello bir tarafta sağlanan.</span><span class="sxs-lookup"><span data-stu-id="6639f-834">These settings were tested with customers and provided a good compromise toobe resilient enough on hello one side.</span></span> <span data-ttu-id="6639f-835">Üzerinde Hello diğer yandan bu ayarları hızlı gerçek hata koşulları SAP yazılım veya düğüm/VM hatasında yeterli yük sağlama.</span><span class="sxs-lookup"><span data-stu-id="6639f-835">On hello other hand those settings were providing fast enough failover in real error conditions on SAP software or node/VM failure.</span></span> 

### <span data-ttu-id="6639f-836"><a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a>Merhaba SAP ASCS/SCS küme paylaşım disk için SIOS DataKeeper küme Edition'ı yükleme</span><span class="sxs-lookup"><span data-stu-id="6639f-836"><a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a> Install SIOS DataKeeper Cluster Edition for hello SAP ASCS/SCS cluster share disk</span></span>

<span data-ttu-id="6639f-837">Artık Azure üzerinde çalışan bir Windows Server Yük Devretme Kümelemesi yapılandırma vardır.</span><span class="sxs-lookup"><span data-stu-id="6639f-837">You now have a working Windows Server Failover Clustering configuration in Azure.</span></span> <span data-ttu-id="6639f-838">Ancak, tooinstall SAP ASCS/SCS örneği bir paylaşılan disk kaynağı gerekir.</span><span class="sxs-lookup"><span data-stu-id="6639f-838">But, tooinstall an SAP ASCS/SCS instance, you need a shared disk resource.</span></span> <span data-ttu-id="6639f-839">Azure'da hello paylaşılan disk kaynakları ihtiyacınız oluşturulamıyor.</span><span class="sxs-lookup"><span data-stu-id="6639f-839">You cannot create hello shared disk resources you need in Azure.</span></span> <span data-ttu-id="6639f-840">SIOS DataKeeper Cluster Edition toocreate paylaşılan disk kaynakları kullanabilir üçüncü taraf bir çözümdür.</span><span class="sxs-lookup"><span data-stu-id="6639f-840">SIOS DataKeeper Cluster Edition is a third-party solution you can use toocreate shared disk resources.</span></span>

<span data-ttu-id="6639f-841">Merhaba SAP ASCS/SCS SIOS DataKeeper Cluster Edition yüklemek küme paylaşım disk bu görevleri içerir:</span><span class="sxs-lookup"><span data-stu-id="6639f-841">Installing SIOS DataKeeper Cluster Edition for hello SAP ASCS/SCS cluster share disk involves these tasks:</span></span>

- <span data-ttu-id="6639f-842">.NET Framework 3.5 Hello ekleme</span><span class="sxs-lookup"><span data-stu-id="6639f-842">Adding hello .NET Framework 3.5</span></span>
- <span data-ttu-id="6639f-843">SIOS DataKeeper yükleme</span><span class="sxs-lookup"><span data-stu-id="6639f-843">Installing SIOS DataKeeper</span></span>
- <span data-ttu-id="6639f-844">SIOS DataKeeper ayarlama</span><span class="sxs-lookup"><span data-stu-id="6639f-844">Setting up SIOS DataKeeper</span></span>

#### <span data-ttu-id="6639f-845"><a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a>.NET Framework 3.5 Hello ekleme</span><span class="sxs-lookup"><span data-stu-id="6639f-845"><a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a> Add hello .NET Framework 3.5</span></span>
<span data-ttu-id="6639f-846">Merhaba Microsoft .NET Framework 3.5 otomatik olarak etkinleştirilmiş veya Windows Server 2012 R2'de yüklü değil.</span><span class="sxs-lookup"><span data-stu-id="6639f-846">hello Microsoft .NET Framework 3.5 isn't automatically activated or installed on Windows Server 2012 R2.</span></span> <span data-ttu-id="6639f-847">SIOS DataKeeper hello .NET Framework toobe DataKeeper yüklemek, tüm düğümlerde gerektirdiğinden, hello konuk işletim sisteminde hello kümedeki tüm sanal makinelerin hello .NET Framework 3.5 yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6639f-847">Because SIOS DataKeeper requires hello .NET Framework toobe on all nodes that you install DataKeeper on, you must install hello .NET Framework 3.5 on hello guest operating system of all virtual machines in hello cluster.</span></span>

<span data-ttu-id="6639f-848">İki yolu tooadd hello .NET Framework 3.5 vardır:</span><span class="sxs-lookup"><span data-stu-id="6639f-848">There are two ways tooadd hello .NET Framework 3.5:</span></span>

- <span data-ttu-id="6639f-849">Merhaba Ekle roller ve Özellikler Sihirbazı Windows şekil 39 gösterildiği gibi kullanın.</span><span class="sxs-lookup"><span data-stu-id="6639f-849">Use hello Add Roles and Features Wizard in Windows as shown in Figure 39.</span></span>

  ![Şekil 39: hello .NET Framework 3.5 hello Ekle roller ve Özellikler Sihirbazı kullanarak yükleme][sap-ha-guide-figure-3028]

  <span data-ttu-id="6639f-851">_**Şekil 39:** hello Ekle roller ve Özellikler Sihirbazı kullanarak yükleme hello .NET Framework 3.5_</span><span class="sxs-lookup"><span data-stu-id="6639f-851">_**Figure 39:** Install hello .NET Framework 3.5 by using hello Add Roles and Features Wizard_</span></span>

  ![Şekil 40: yükleme ilerleme çubuğu hello .NET Framework 3.5 hello Ekle roller ve Özellikler Sihirbazı'nı kullanarak yüklediğinizde][sap-ha-guide-figure-3029]

  <span data-ttu-id="6639f-853">_**Şekil 40:** çubuğu hello .NET Framework 3.5 hello Ekle roller ve Özellikler Sihirbazı'nı kullanarak yüklediğinizde, yükleme ilerleme durumu_</span><span class="sxs-lookup"><span data-stu-id="6639f-853">_**Figure 40:** Installation progress bar when you install hello .NET Framework 3.5 by using hello Add Roles and Features Wizard_</span></span>

- <span data-ttu-id="6639f-854">Merhaba komut satırı aracı dism.exe kullanın.</span><span class="sxs-lookup"><span data-stu-id="6639f-854">Use hello command-line tool dism.exe.</span></span> <span data-ttu-id="6639f-855">Bu yükleme türü için tooaccess hello SxS dizin hello Windows yükleme medyası üzerinde gerekir.</span><span class="sxs-lookup"><span data-stu-id="6639f-855">For this type of installation, you need tooaccess hello SxS directory on hello Windows installation media.</span></span> <span data-ttu-id="6639f-856">Yükseltilmiş bir komut istemine yazın:</span><span class="sxs-lookup"><span data-stu-id="6639f-856">At an elevated command prompt, type:</span></span>

  ```
  Dism /online /enable-feature /featurename:NetFx3 /All /Source:installation_media_drive:\sources\sxs /LimitAccess
  ```

#### <span data-ttu-id="6639f-857"><a name="dd41d5a2-8083-415b-9878-839652812102"></a>SIOS DataKeeper yükleyin</span><span class="sxs-lookup"><span data-stu-id="6639f-857"><a name="dd41d5a2-8083-415b-9878-839652812102"></a> Install SIOS DataKeeper</span></span>

<span data-ttu-id="6639f-858">Merhaba kümedeki her düğümde SIOS DataKeeper Cluster Edition yükleyin.</span><span class="sxs-lookup"><span data-stu-id="6639f-858">Install SIOS DataKeeper Cluster Edition on each node in hello cluster.</span></span> <span data-ttu-id="6639f-859">toocreate sanal paylaşılan depolama SIOS DataKeeper ile eşitlenen bir yansıtma oluşturun ve Küme Paylaşılan depolama benzetimi.</span><span class="sxs-lookup"><span data-stu-id="6639f-859">toocreate virtual shared storage with SIOS DataKeeper, create a synced mirror and then simulate cluster shared storage.</span></span>

<span data-ttu-id="6639f-860">Merhaba SIOS yazılımı yüklemeden önce hello etki alanı kullanıcısı oluşturun **DataKeeperSvc**.</span><span class="sxs-lookup"><span data-stu-id="6639f-860">Before you install hello SIOS software, create hello domain user **DataKeeperSvc**.</span></span>

> [!NOTE]
> <span data-ttu-id="6639f-861">Merhaba eklemek **DataKeeperSvc** kullanıcı toohello **yerel yönetici** her iki küme düğümlerinde grup.</span><span class="sxs-lookup"><span data-stu-id="6639f-861">Add hello **DataKeeperSvc** user toohello **Local Administrator** group on both cluster nodes.</span></span>
>
>

<span data-ttu-id="6639f-862">tooinstall SIOS DataKeeper:</span><span class="sxs-lookup"><span data-stu-id="6639f-862">tooinstall SIOS DataKeeper:</span></span>

1.  <span data-ttu-id="6639f-863">Merhaba SIOS yazılım her iki küme düğümlerine yükleyin.</span><span class="sxs-lookup"><span data-stu-id="6639f-863">Install hello SIOS software on both cluster nodes.</span></span>

  ![SIOS yükleyici][sap-ha-guide-figure-3030]

  ![Şekil 41: Merhaba SIOS DataKeeper Yükleme'nın ilk sayfasında][sap-ha-guide-figure-3031]

  <span data-ttu-id="6639f-866">_**Şekil 41:** hello SIOS DataKeeper Yükleme'nın ilk sayfasında_</span><span class="sxs-lookup"><span data-stu-id="6639f-866">_**Figure 41:** First page of hello SIOS DataKeeper installation_</span></span>

2.  <span data-ttu-id="6639f-867">Şekil 42 gösterilen hello iletişim kutusunda seçin **Evet**.</span><span class="sxs-lookup"><span data-stu-id="6639f-867">In hello dialog box shown in Figure 42, select **Yes**.</span></span>

  ![Şekil 42: Bir hizmeti devre dışı bırakılacak DataKeeper size bildirir][sap-ha-guide-figure-3032]

  <span data-ttu-id="6639f-869">_**Şekil 42:** DataKeeper bildirir, bir hizmeti devre dışı bırakılacak_</span><span class="sxs-lookup"><span data-stu-id="6639f-869">_**Figure 42:** DataKeeper informs you that a service will be disabled_</span></span>

3.  <span data-ttu-id="6639f-870">Şekil 43 gösterilen hello iletişim kutusunda seçtiğiniz olan öneririz **etki alanı veya sunucu hesabı**.</span><span class="sxs-lookup"><span data-stu-id="6639f-870">In hello dialog box shown in Figure 43, we recommend that you select **Domain or Server account**.</span></span>

  ![Şekil 43: Kullanıcı Seçimi SIOS DataKeeper için][sap-ha-guide-figure-3033]

  <span data-ttu-id="6639f-872">_**Şekil 43:** SIOS DataKeeper için kullanıcı seçimi_</span><span class="sxs-lookup"><span data-stu-id="6639f-872">_**Figure 43:** User selection for SIOS DataKeeper_</span></span>

4.  <span data-ttu-id="6639f-873">Merhaba etki alanı hesabı kullanıcı adı ve SIOS DataKeeper için oluşturduğunuz parola girin.</span><span class="sxs-lookup"><span data-stu-id="6639f-873">Enter hello domain account user name and passwords that you created for SIOS DataKeeper.</span></span>

  ![Şekil 44: Merhaba SIOS DataKeeper yükleme hello etki alanı kullanıcı adı ve parola girin][sap-ha-guide-figure-3034]

  <span data-ttu-id="6639f-875">_**Şekil 44:** Merhaba SIOS DataKeeper yükleme hello etki alanı kullanıcı adı ve parola girin_</span><span class="sxs-lookup"><span data-stu-id="6639f-875">_**Figure 44:** Enter hello domain user name and password for hello SIOS DataKeeper installation_</span></span>

5.  <span data-ttu-id="6639f-876">Şekil 45 gösterildiği gibi SIOS DataKeeper örneğinizin Hello lisans anahtarını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="6639f-876">Install hello license key for your SIOS DataKeeper instance as shown in Figure 45.</span></span>

  ![Şekil 45: SIOS DataKeeper lisans anahtarınızı girin][sap-ha-guide-figure-3035]

  <span data-ttu-id="6639f-878">_**Şekil 45:** SIOS DataKeeper lisans anahtarınızı girin_</span><span class="sxs-lookup"><span data-stu-id="6639f-878">_**Figure 45:** Enter your SIOS DataKeeper license key_</span></span>

6.  <span data-ttu-id="6639f-879">İstendiğinde, hello sanal makineyi yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="6639f-879">When prompted, restart hello virtual machine.</span></span>

#### <span data-ttu-id="6639f-880"><a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a>SIOS DataKeeper ayarlayın</span><span class="sxs-lookup"><span data-stu-id="6639f-880"><a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a> Set up SIOS DataKeeper</span></span>

<span data-ttu-id="6639f-881">Her iki düğümde SIOS DataKeeper yükledikten sonra toostart hello yapılandırması gerekir.</span><span class="sxs-lookup"><span data-stu-id="6639f-881">After you install SIOS DataKeeper on both nodes, you need toostart hello configuration.</span></span> <span data-ttu-id="6639f-882">Merhaba hello yapılandırma hello ek bağlı VHD'ler tooeach hello sanal makinelerin arasında toohave eşzamanlı veri çoğaltma hedefidir.</span><span class="sxs-lookup"><span data-stu-id="6639f-882">hello goal of hello configuration is toohave synchronous data replication between hello additional VHDs attached tooeach of hello virtual machines.</span></span>

1.  <span data-ttu-id="6639f-883">Merhaba DataKeeper yönetim ve yapılandırma aracını başlatmak ve ardından **Connect Server**.</span><span class="sxs-lookup"><span data-stu-id="6639f-883">Start hello DataKeeper Management and Configuration tool, and then select **Connect Server**.</span></span> <span data-ttu-id="6639f-884">(Şekil 46 bu seçenek kırmızı daire içine alınmıştır.)</span><span class="sxs-lookup"><span data-stu-id="6639f-884">(In Figure 46, this option is circled in red.)</span></span>

  ![Şekil 46: SIOS DataKeeper yönetim ve yapılandırma aracı][sap-ha-guide-figure-3036]

  <span data-ttu-id="6639f-886">_**Şekil 46:** SIOS DataKeeper yönetim ve yapılandırma aracı_</span><span class="sxs-lookup"><span data-stu-id="6639f-886">_**Figure 46:** SIOS DataKeeper Management and Configuration tool_</span></span>

2.  <span data-ttu-id="6639f-887">Merhaba adı girin veya TCP/IP adresi aracının hello ilk düğüm hello yönetimi ve yapılandırması için ve ikinci adım, hello İkinci düğüm bağlanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6639f-887">Enter hello name or TCP/IP address of hello first node hello Management and Configuration tool should connect to, and, in a second step, hello second node.</span></span>

  ![Şekil 47: Ekle hello adı veya TCP/IP adresi aracının hello ilk düğüm hello yönetimi ve yapılandırması için ve ikinci adım, hello İkinci düğüm bağlanmanız gerekir][sap-ha-guide-figure-3037]

  <span data-ttu-id="6639f-889">_**Şekil 47:** Ekle hello adı veya TCP/IP adresi aracının hello ilk düğüm hello yönetimi ve yapılandırması bağlanmak için ve ikinci adım, hello ikinci düğümü_</span><span class="sxs-lookup"><span data-stu-id="6639f-889">_**Figure 47:** Insert hello name or TCP/IP address of hello first node hello Management and Configuration tool should connect to, and in a second step, hello second node_</span></span>

3.  <span data-ttu-id="6639f-890">Merhaba iki düğüm arasında Hello çoğaltma işi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6639f-890">Create hello replication job between hello two nodes.</span></span>

  ![Şekil 48: bir çoğaltma işi oluşturma][sap-ha-guide-figure-3038]

  <span data-ttu-id="6639f-892">_**Şekil 48:** çoğaltma işi oluşturma_</span><span class="sxs-lookup"><span data-stu-id="6639f-892">_**Figure 48:** Create a replication job_</span></span>

  <span data-ttu-id="6639f-893">Sihirbaz çoğaltma iş oluşturma hello işleminde size rehberlik eder.</span><span class="sxs-lookup"><span data-stu-id="6639f-893">A wizard guides you through hello process of creating a replication job.</span></span>
4.  <span data-ttu-id="6639f-894">Merhaba adı, TCP/IP adresi ve hello kaynak düğüm disk birimi tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="6639f-894">Define hello name, TCP/IP address, and disk volume of hello source node.</span></span>

  ![Şekil 49: hello çoğaltma işi hello adını tanımlayın][sap-ha-guide-figure-3039]

  <span data-ttu-id="6639f-896">_**Şekil 49:** hello çoğaltma işi hello adını tanımlayın_</span><span class="sxs-lookup"><span data-stu-id="6639f-896">_**Figure 49:** Define hello name of hello replication job_</span></span>

  ![Şekil 50: hello geçerli kaynak düğüm olmalıdır hello düğüm için hello temel veri tanımlama][sap-ha-guide-figure-3040]

  <span data-ttu-id="6639f-898">_**Şekil 50:** hello geçerli kaynak düğüm olmalıdır hello düğüm için hello temel veri tanımlama_</span><span class="sxs-lookup"><span data-stu-id="6639f-898">_**Figure 50:** Define hello base data for hello node, which should be hello current source node_</span></span>

5.  <span data-ttu-id="6639f-899">Merhaba adı, TCP/IP adresi ve hello hedef düğüm disk birimi tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="6639f-899">Define hello name, TCP/IP address, and disk volume of hello target node.</span></span>

  ![Şekil 51: hello geçerli hedef düğümü olmalı hello düğüm için hello temel veri tanımlama][sap-ha-guide-figure-3041]

  <span data-ttu-id="6639f-901">_**Şekil 51:** hello geçerli hedef düğümü olmalı hello düğüm için hello temel veri tanımlama_</span><span class="sxs-lookup"><span data-stu-id="6639f-901">_**Figure 51:** Define hello base data for hello node, which should be hello current target node_</span></span>

6.  <span data-ttu-id="6639f-902">Merhaba sıkıştırma algoritmaları tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="6639f-902">Define hello compression algorithms.</span></span> <span data-ttu-id="6639f-903">Bizim örneğimizde, hello çoğaltma akışını sıkıştırmak öneririz.</span><span class="sxs-lookup"><span data-stu-id="6639f-903">In our example, we recommend that you compress hello replication stream.</span></span> <span data-ttu-id="6639f-904">Özellikle yeniden eşitleme durumlarda hello çoğaltma akışı hello sıkıştırmasını yeniden eşitleme zamanı önemli ölçüde azaltır.</span><span class="sxs-lookup"><span data-stu-id="6639f-904">Especially in resynchronization situations, hello compression of hello replication stream dramatically reduces resynchronization time.</span></span> <span data-ttu-id="6639f-905">Sıkıştırma hello CPU ve RAM kaynaklarını bir sanal makinenin kullandığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="6639f-905">Note that compression uses hello CPU and RAM resources of a virtual machine.</span></span> <span data-ttu-id="6639f-906">Merhaba sıkıştırma oranı arttıkça, bu nedenle kullanılan CPU kaynakları hacmi hello.</span><span class="sxs-lookup"><span data-stu-id="6639f-906">As hello compression rate increases, so does hello volume of CPU resources used.</span></span> <span data-ttu-id="6639f-907">Bu ayarı daha sonra da ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6639f-907">You also can adjust this setting later.</span></span>

7.  <span data-ttu-id="6639f-908">Ayar başka bir gereksinim toocheck olan olup olmadığını zaman uyumsuz veya zaman uyumlu olarak hello çoğaltma gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="6639f-908">Another setting you need toocheck is whether hello replication occurs asynchronously or synchronously.</span></span> <span data-ttu-id="6639f-909">*SAP ASCS/SCS yapılandırmaları koruduğunuzda, zaman uyumlu çoğaltma kullanmalısınız*.</span><span class="sxs-lookup"><span data-stu-id="6639f-909">*When you protect SAP ASCS/SCS configurations, you must use synchronous replication*.</span></span>  

  ![Şekil 52: çoğaltma ayrıntılarını tanımlayın][sap-ha-guide-figure-3042]

  <span data-ttu-id="6639f-911">_**Şekil 52:** çoğaltma ayrıntılarını tanımlayın_</span><span class="sxs-lookup"><span data-stu-id="6639f-911">_**Figure 52:** Define replication details_</span></span>

8.  <span data-ttu-id="6639f-912">Merhaba çoğaltma işlemiyle çoğaltılır hello birim gösterilen tooa Windows Server Yük Devretme Kümelemesi küme yapılandırması paylaşılan bir disk olarak olup olmayacağını tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="6639f-912">Define whether hello volume that is replicated by hello replication job should be represented tooa Windows Server Failover Clustering cluster configuration as a shared disk.</span></span> <span data-ttu-id="6639f-913">Merhaba SAP ASCS/SCS yapılandırmasını seçin **Evet** çoğaltılan birim olarak bir küme birimi olarak kullanabileceği bir paylaşılan disk küme görür hello Windows hello böylece.</span><span class="sxs-lookup"><span data-stu-id="6639f-913">For hello SAP ASCS/SCS configuration, select **Yes** so that hello Windows cluster sees hello replicated volume as a shared disk that it can use as a cluster volume.</span></span>

  ![Şekil 53: Evet tooset çoğaltılan hello toplu küme birimi seçin.][sap-ha-guide-figure-3043]

  <span data-ttu-id="6639f-915">_**Şekil 53:** seçin **Evet** tooset hello çoğaltılan birimi bir küme birimi olarak_</span><span class="sxs-lookup"><span data-stu-id="6639f-915">_**Figure 53:** Select **Yes** tooset hello replicated volume as a cluster volume_</span></span>

  <span data-ttu-id="6639f-916">Merhaba birim oluşturulduktan sonra hello DataKeeper yönetim ve yapılandırma aracı o hello çoğaltma işi etkin olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="6639f-916">After hello volume is created, hello DataKeeper Management and Configuration tool shows that hello replication job is active.</span></span>

  ![Şekil 54: DataKeeper SAP ASCS/SCS paylaşım disk hello için zaman uyumlu yansıtma etkindir][sap-ha-guide-figure-3044]

  <span data-ttu-id="6639f-918">_**Şekil 54:** hello SAP ASCS/SCS paylaşmak disk için DataKeeper zaman uyumlu yansıtma etkin olduğu_</span><span class="sxs-lookup"><span data-stu-id="6639f-918">_**Figure 54:** DataKeeper synchronous mirroring for hello SAP ASCS/SCS share disk is active_</span></span>

  <span data-ttu-id="6639f-919">Yük Devretme Kümesi Yöneticisi şimdi şekil 55 gösterildiği gibi hello disk DataKeeper disk olarak gösterir.</span><span class="sxs-lookup"><span data-stu-id="6639f-919">Failover Cluster Manager now shows hello disk as a DataKeeper disk, as shown in Figure 55.</span></span>

  ![Şekil 55: Yük devretme kümesi Yöneticisi'ni DataKeeper çoğaltılan hello disk gösterir.][sap-ha-guide-figure-3045]

  <span data-ttu-id="6639f-921">_**Şekil 55:** yük devretme kümesi Yöneticisi, çoğaltılan bu DataKeeper hello disk gösterir_</span><span class="sxs-lookup"><span data-stu-id="6639f-921">_**Figure 55:** Failover Cluster Manager shows hello disk that DataKeeper replicated_</span></span>

## <span data-ttu-id="6639f-922"><a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a>Merhaba SAP NetWeaver sistemini yükleyin</span><span class="sxs-lookup"><span data-stu-id="6639f-922"><a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a> Install hello SAP NetWeaver system</span></span>

<span data-ttu-id="6639f-923">Kurulumları hello DBMS sistemine bağlı olarak farklılık gösterdiğinden biz hello DBMS kurulumunu açıklayan olmaz.</span><span class="sxs-lookup"><span data-stu-id="6639f-923">We won’t describe hello DBMS setup because setups vary depending on hello DBMS system you use.</span></span> <span data-ttu-id="6639f-924">Ancak, yüksek kullanılabilirlik sorunları hello DBMS ile Merhaba işlevler hello farklı DBMS satıcılar için Azure desteği ile giderilen varsayalım.</span><span class="sxs-lookup"><span data-stu-id="6639f-924">However, we assume that high-availability concerns with hello DBMS are addressed with hello functionalities hello different DBMS vendors support for Azure.</span></span> <span data-ttu-id="6639f-925">Örneğin, her zaman açık veya Oracle veritabanları için SQL Server ve Oracle Data Guard için veritabanı yansıtma.</span><span class="sxs-lookup"><span data-stu-id="6639f-925">For example, Always On or database mirroring for SQL Server, and Oracle Data Guard for Oracle databases.</span></span> <span data-ttu-id="6639f-926">Bu makalede kullanırız hello senaryosunda, size daha fazla koruma toohello DBMS ekleyemiyor.</span><span class="sxs-lookup"><span data-stu-id="6639f-926">In hello scenario we use in this article, we didn't add more protection toohello DBMS.</span></span>

<span data-ttu-id="6639f-927">Bu tür bir Azure kümelenmiş SAP ASCS/SCS yapılandırmasında farklı DBMS Hizmetleri etkileşim, özel durumlar vardır.</span><span class="sxs-lookup"><span data-stu-id="6639f-927">There are no special considerations when different DBMS services interact with this kind of clustered SAP ASCS/SCS configuration in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="6639f-928">SAP NetWeaver ABAP sistemleri, Java sistemleri ve ABAP + Java sistemleri Hello yükleme yordamları neredeyse aynıdır.</span><span class="sxs-lookup"><span data-stu-id="6639f-928">hello installation procedures of SAP NetWeaver ABAP systems, Java systems, and ABAP+Java systems are almost identical.</span></span> <span data-ttu-id="6639f-929">Merhaba en önemli fark, bir SAP ABAP sistemi bir ASCS örneği sahip olur.</span><span class="sxs-lookup"><span data-stu-id="6639f-929">hello most significant difference is that an SAP ABAP system has one ASCS instance.</span></span> <span data-ttu-id="6639f-930">Merhaba SAP Java sistem bir SCS örneği vardır.</span><span class="sxs-lookup"><span data-stu-id="6639f-930">hello SAP Java system has one SCS instance.</span></span> <span data-ttu-id="6639f-931">bir ASCS örneği Hello SAP ABAP + Java sistem sahiptir ve çalışır durumda bir SCS örneği hello aynı Microsoft yük devretme küme grubu.</span><span class="sxs-lookup"><span data-stu-id="6639f-931">hello SAP ABAP+Java system has one ASCS instance and one SCS instance running in hello same Microsoft failover cluster group.</span></span> <span data-ttu-id="6639f-932">Her SAP NetWeaver yükleme yığınının yükleme farkları açıkça belirtilen.</span><span class="sxs-lookup"><span data-stu-id="6639f-932">Any installation differences for each SAP NetWeaver installation stack are explicitly mentioned.</span></span> <span data-ttu-id="6639f-933">Diğer tüm bölümleri olan Merhaba, aynı varsayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6639f-933">You can assume that all other parts are hello same.</span></span>  
>
>

### <span data-ttu-id="6639f-934"><a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a>Bir yüksek kullanılabilirlik ASCS/SCS örneğiyle SAP yükleyin</span><span class="sxs-lookup"><span data-stu-id="6639f-934"><a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a> Install SAP with a high-availability ASCS/SCS instance</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6639f-935">Unutmayın, sayfa dosyası üzerinde DataKeeper tooplace yansıtılmış birimler.</span><span class="sxs-lookup"><span data-stu-id="6639f-935">Be sure not tooplace your page file on DataKeeper mirrored volumes.</span></span> <span data-ttu-id="6639f-936">Yansıtılmış birimler DataKeeper desteklemez.</span><span class="sxs-lookup"><span data-stu-id="6639f-936">DataKeeper does not support mirrored volumes.</span></span> <span data-ttu-id="6639f-937">Merhaba varsayılan olduğu hello geçici D sürücüsündeki bir Azure sanal makine, sayfa dosyası bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6639f-937">You can leave your page file on hello temporary drive D of an Azure virtual machine, which is hello default.</span></span> <span data-ttu-id="6639f-938">Bunu zaten yoksa, Azure sanal makinenizin hello Windows sayfa dosyası toodrive D taşıyın.</span><span class="sxs-lookup"><span data-stu-id="6639f-938">If it's not already there, move hello Windows page file toodrive D of your Azure virtual machine.</span></span>
>
>

<span data-ttu-id="6639f-939">Bir yüksek kullanılabilirlik ASCS/SCS örneğiyle SAP yüklemek, bu görevleri içerir:</span><span class="sxs-lookup"><span data-stu-id="6639f-939">Installing SAP with a high-availability ASCS/SCS instance involves these tasks:</span></span>

- <span data-ttu-id="6639f-940">Kümelenmiş hello SAP ASCS/SCS örneği için bir sanal ana bilgisayar adı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6639f-940">Creating a virtual host name for hello clustered SAP ASCS/SCS instance</span></span>
- <span data-ttu-id="6639f-941">Merhaba SAP ilk küme düğümüne yükleme</span><span class="sxs-lookup"><span data-stu-id="6639f-941">Installing hello SAP first cluster node</span></span>
- <span data-ttu-id="6639f-942">Merhaba SAP profili hello ASCS/SCS örneğinin değiştirme</span><span class="sxs-lookup"><span data-stu-id="6639f-942">Modifying hello SAP profile of hello ASCS/SCS instance</span></span>
- <span data-ttu-id="6639f-943">Sonda bağlantı noktası ekleme</span><span class="sxs-lookup"><span data-stu-id="6639f-943">Adding a probe port</span></span>
- <span data-ttu-id="6639f-944">Merhaba Windows Güvenlik Duvarı araştırma bağlantı noktası açma</span><span class="sxs-lookup"><span data-stu-id="6639f-944">Opening hello Windows firewall probe port</span></span>

#### <span data-ttu-id="6639f-945"><a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a>Kümelenmiş hello SAP ASCS/SCS örneği için bir sanal ana bilgisayar adı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6639f-945"><a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a> Create a virtual host name for hello clustered SAP ASCS/SCS instance</span></span>

1.  <span data-ttu-id="6639f-946">Merhaba Windows DNS Yöneticisi'nde hello ASCS/SCS örneğinin hello sanal ana bilgisayar adı için bir DNS girişi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6639f-946">In hello Windows DNS manager, create a DNS entry for hello virtual host name of hello ASCS/SCS instance.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="6639f-947">Merhaba ASCS/SCS örneği olmalıdır hello toohello sanal ana bilgisayar adı atamak IP adresi hello aynı tooAzure yük dengeleyiciye atanan hello IP adresi olarak (**<*SID*> - lb - ascs **).</span><span class="sxs-lookup"><span data-stu-id="6639f-947">hello IP address that you assign toohello virtual host name of hello ASCS/SCS instance must be hello same as hello IP address that you assigned tooAzure Load Balancer (**<*SID*>-lb-ascs**).</span></span>  
  >
  >

  <span data-ttu-id="6639f-948">Merhaba hello sanal SAP ASCS/SCS ana bilgisayar adının IP adresini (**pr1 ascs sap**) olan hello aynı başlangıç IP adresi Azure yük dengeleyici olarak (**pr1 lb ascs**).</span><span class="sxs-lookup"><span data-stu-id="6639f-948">hello IP address of hello virtual SAP ASCS/SCS host name (**pr1-ascs-sap**) is hello same as hello IP address of Azure Load Balancer (**pr1-lb-ascs**).</span></span>

  ![Şekil 56: hello DNS girdisini hello SAP ASCS/SCS küme sanal adı ve TCP/IP adresi tanımlayın][sap-ha-guide-figure-3046]

  <span data-ttu-id="6639f-950">_**Şekil 56:** hello DNS girdisini hello SAP ASCS/SCS küme sanal adı ve TCP/IP adresi tanımlayın_</span><span class="sxs-lookup"><span data-stu-id="6639f-950">_**Figure 56:** Define hello DNS entry for hello SAP ASCS/SCS cluster virtual name and TCP/IP address_</span></span>

2.  <span data-ttu-id="6639f-951">toodefine hello IP adresi atanmış toohello sanal ana bilgisayar adını, select **DNS Yöneticisi'ni** > **etki alanı**.</span><span class="sxs-lookup"><span data-stu-id="6639f-951">toodefine hello IP address assigned toohello virtual host name, select **DNS Manager** > **Domain**.</span></span>

  ![Şekil 57: Yeni sanal adı ve TCP/IP adresi SAP ASCS/SCS kümesi yapılandırması için][sap-ha-guide-figure-3047]

  <span data-ttu-id="6639f-953">_**Şekil 57:** yeni sanal adı ve TCP/IP adresi SAP ASCS/SCS küme yapılandırması_</span><span class="sxs-lookup"><span data-stu-id="6639f-953">_**Figure 57:** New virtual name and TCP/IP address for SAP ASCS/SCS cluster configuration_</span></span>

#### <span data-ttu-id="6639f-954"><a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a>Merhaba SAP ilk küme düğümüne yükleyin</span><span class="sxs-lookup"><span data-stu-id="6639f-954"><a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a> Install hello SAP first cluster node</span></span>

1.  <span data-ttu-id="6639f-955">Merhaba ilk küme düğümü seçeneği küme düğümünde A. yürütme Örneğin, hello üzerinde **pr1 ascs 0** ana bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="6639f-955">Execute hello first cluster node option on cluster node A. For example, on hello **pr1-ascs-0** host.</span></span>
2.  <span data-ttu-id="6639f-956">tookeep hello varsayılan bağlantı noktalarını hello Azure iç yük dengeleyici, seçin:</span><span class="sxs-lookup"><span data-stu-id="6639f-956">tookeep hello default ports for hello Azure internal load balancer, select:</span></span>

  * <span data-ttu-id="6639f-957">**ABAP sistem**: **ASCS** örnek numarasını **00**</span><span class="sxs-lookup"><span data-stu-id="6639f-957">**ABAP system**: **ASCS** instance number **00**</span></span>
  * <span data-ttu-id="6639f-958">**Java sistem**: **SCS** örnek numarasını **01**</span><span class="sxs-lookup"><span data-stu-id="6639f-958">**Java system**: **SCS** instance number **01**</span></span>
  * <span data-ttu-id="6639f-959">**ABAP + Java sistem**: **ASCS** örnek numarasını **00** ve **SCS** örnek numarasını **01**</span><span class="sxs-lookup"><span data-stu-id="6639f-959">**ABAP+Java system**: **ASCS** instance number **00** and **SCS** instance number **01**</span></span>

  <span data-ttu-id="6639f-960">toouse örnek sayılar, hello ABAP ASCS 00 dışında örneği ve 01 hello Java SCS örneği için öncelikle toochange hello Azure iç yük dengeleyici varsayılan Yük Dengeleme kuralları, açıklanan gerekir [değişiklik hello ASCS/SCS varsayılan yükleme Dengeleme hello Azure iç yük dengeleyici kuralları][sap-ha-guide-8.9].</span><span class="sxs-lookup"><span data-stu-id="6639f-960">toouse instance numbers other than 00 for hello ABAP ASCS instance and 01 for hello Java SCS instance, first you need toochange hello Azure internal load balancer default load balancing rules, described in [Change hello ASCS/SCS default load balancing rules for hello Azure internal load balancer][sap-ha-guide-8.9].</span></span>

<span data-ttu-id="6639f-961">Merhaba sonraki birkaç görevleri hello standart SAP yükleme belgelerinde açıklanan değil.</span><span class="sxs-lookup"><span data-stu-id="6639f-961">hello next few tasks aren't described in hello standard SAP installation documentation.</span></span>

> [!NOTE]
> <span data-ttu-id="6639f-962">Merhaba SAP yükleme belgelerini nasıl tooinstall hello ilk ASCS/SCS küme düğümüne açıklar.</span><span class="sxs-lookup"><span data-stu-id="6639f-962">hello SAP installation documentation describes how tooinstall hello first ASCS/SCS cluster node.</span></span>
>
>

#### <span data-ttu-id="6639f-963"><a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a>Merhaba SAP profili hello ASCS/SCS örneğinin değiştirme</span><span class="sxs-lookup"><span data-stu-id="6639f-963"><a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a> Modify hello SAP profile of hello ASCS/SCS instance</span></span>

<span data-ttu-id="6639f-964">Yeni bir profil parametre tooadd gerekir.</span><span class="sxs-lookup"><span data-stu-id="6639f-964">You need tooadd a new profile parameter.</span></span> <span data-ttu-id="6639f-965">Hello profil parametre çok uzun süre boşta olduğunda kapanmasını SAP iş süreçlerini ve hello enqueue sunucu arasındaki bağlantıları engeller.</span><span class="sxs-lookup"><span data-stu-id="6639f-965">hello profile parameter prevents connections between SAP work processes and hello enqueue server from closing when they are idle for too long.</span></span> <span data-ttu-id="6639f-966">Biz hello sorun senaryoda bahsedilen [hello SAP ASCS/SCS örneği her iki küme düğümleri üzerinde kayıt defteri girdisini eklemeniz][sap-ha-guide-8.11].</span><span class="sxs-lookup"><span data-stu-id="6639f-966">We mentioned hello problem scenario in [Add registry entries on both cluster nodes of hello SAP ASCS/SCS instance][sap-ha-guide-8.11].</span></span> <span data-ttu-id="6639f-967">Bu bölümde Ayrıca iki değişiklikleri toosome temel TCP/IP bağlantı parametrelerini sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="6639f-967">In that section, we also introduced two changes toosome basic TCP/IP connection parameters.</span></span> <span data-ttu-id="6639f-968">İkinci adımda, tooset hello enqueue sunucu toosend gereken bir `keep_alive` hello bağlantıları hello Azure iç yük dengeleyicinin boşta kalma eşiği isabet yok böylece sinyal.</span><span class="sxs-lookup"><span data-stu-id="6639f-968">In a second step, you need tooset hello enqueue server toosend a `keep_alive` signal so that hello connections don't hit hello Azure internal load balancer's idle threshold.</span></span>

<span data-ttu-id="6639f-969">toomodify hello hello ASCS/SCS örneğinin SAP profili:</span><span class="sxs-lookup"><span data-stu-id="6639f-969">toomodify hello SAP profile of hello ASCS/SCS instance:</span></span>

1.  <span data-ttu-id="6639f-970">Bu profil parametresi toohello SAP ASCS/SCS örneği profili ekleyin:</span><span class="sxs-lookup"><span data-stu-id="6639f-970">Add this profile parameter toohello SAP ASCS/SCS instance profile:</span></span>

  ```
  enque/encni/set_so_keepalive = true
  ```
  <span data-ttu-id="6639f-971">Bizim örneğimizde, hello yol şudur:</span><span class="sxs-lookup"><span data-stu-id="6639f-971">In our example, hello path is:</span></span>

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_ASCS00_pr1-ascs-sap`

  <span data-ttu-id="6639f-972">Örneğin, toohello SAP SCS profili ve karşılık gelen yol örneği:</span><span class="sxs-lookup"><span data-stu-id="6639f-972">For example, toohello SAP SCS instance profile and corresponding path:</span></span>

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_SCS01_pr1-ascs-sap`

2.  <span data-ttu-id="6639f-973">tooapply hello değişiklikleri hello SAP ASCS /SCS örneğini yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="6639f-973">tooapply hello changes, restart hello SAP ASCS /SCS instance.</span></span>

#### <span data-ttu-id="6639f-974"><a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a>Bir araştırma bağlantı noktası ekleme</span><span class="sxs-lookup"><span data-stu-id="6639f-974"><a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a> Add a probe port</span></span>

<span data-ttu-id="6639f-975">Merhaba iç yük dengeleyicinin araştırma işlevselliği toomake hello tüm küme yapılandırması iş Azure yük dengeleyici ile kullanın.</span><span class="sxs-lookup"><span data-stu-id="6639f-975">Use hello internal load balancer's probe functionality toomake hello entire cluster configuration work with Azure Load Balancer.</span></span> <span data-ttu-id="6639f-976">Hello Azure iç yük dengeleyici genellikle hello gelen iş yükü katılımcı sanal makineler arasında eşit olarak dağıtır.</span><span class="sxs-lookup"><span data-stu-id="6639f-976">hello Azure internal load balancer usually distributes hello incoming workload equally between participating virtual machines.</span></span> <span data-ttu-id="6639f-977">Ancak, tek örnek etkin olmadığından bu bazı küme yapılandırmaları çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="6639f-977">However, this won't work in some cluster configurations because only one instance is active.</span></span> <span data-ttu-id="6639f-978">Merhaba diğer örnek pasif ve hello iş yükü hiçbirini kabul edemez.</span><span class="sxs-lookup"><span data-stu-id="6639f-978">hello other instance is passive and can’t accept any of hello workload.</span></span> <span data-ttu-id="6639f-979">Hello Azure iç yük dengeleyici atar yalnızca tooan etkin örneği çalışırken bir araştırma işlevsellik yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="6639f-979">A probe functionality helps when hello Azure internal load balancer assigns work only tooan active instance.</span></span> <span data-ttu-id="6639f-980">Merhaba araştırma işlevsellikle hello iç yük dengeleyici hangi örnekleri etkin olduğunu ve yalnızca hello örneği hello iş yükü ile hedef algılayabilir.</span><span class="sxs-lookup"><span data-stu-id="6639f-980">With hello probe functionality, hello internal load balancer can detect which instances are active, and then target only hello instance with hello workload.</span></span>

<span data-ttu-id="6639f-981">tooadd sonda bağlantı noktası:</span><span class="sxs-lookup"><span data-stu-id="6639f-981">tooadd a probe port:</span></span>

1.  <span data-ttu-id="6639f-982">Merhaba geçerli denetleyin **ProbePort** hello aşağıdaki PowerShell komutunu çalıştırarak ayarlama.</span><span class="sxs-lookup"><span data-stu-id="6639f-982">Check hello current **ProbePort** setting by running hello following PowerShell command.</span></span> <span data-ttu-id="6639f-983">Merhaba sanal makineleri biri içinde ondan hello küme yapılandırmasında yürütün.</span><span class="sxs-lookup"><span data-stu-id="6639f-983">Execute it from within one of hello virtual machines in hello cluster configuration.</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter
  ```

2.  <span data-ttu-id="6639f-984">Bir araştırma bağlantı noktasını tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="6639f-984">Define a probe port.</span></span> <span data-ttu-id="6639f-985">Merhaba varsayılan araştırma bağlantı noktası numarası **0**.</span><span class="sxs-lookup"><span data-stu-id="6639f-985">hello default probe port number is **0**.</span></span> <span data-ttu-id="6639f-986">Bizim örneğimizde, araştırma bağlantı noktası kullanırız **62000**.</span><span class="sxs-lookup"><span data-stu-id="6639f-986">In our example, we use probe port **62000**.</span></span>

  ![Şekil 58: hello küme yapılandırması araştırma bağlantı noktası varsayılan olarak 0 olur.][sap-ha-guide-figure-3048]

  <span data-ttu-id="6639f-988">_**Şekil 58:** hello varsayılan küme yapılandırması araştırma bağlantı noktası: 0_</span><span class="sxs-lookup"><span data-stu-id="6639f-988">_**Figure 58:** hello default cluster configuration probe port is 0_</span></span>

  <span data-ttu-id="6639f-989">başlangıç bağlantı noktası numarası SAP Azure Resource Manager şablonları tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="6639f-989">hello port number is defined in SAP Azure Resource Manager templates.</span></span> <span data-ttu-id="6639f-990">PowerShell hello bağlantı noktası numarası atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6639f-990">You can assign hello port number in PowerShell.</span></span>

  <span data-ttu-id="6639f-991">tooset hello için yeni bir ProbePort değeri  **SAP <*SID*> PowerShell Betiği aşağıdaki hello çalıştırmak IP ** küme kaynağı.</span><span class="sxs-lookup"><span data-stu-id="6639f-991">tooset a new ProbePort value for hello **SAP <*SID*> IP** cluster resource, run hello following PowerShell script.</span></span> <span data-ttu-id="6639f-992">Merhaba PowerShell değişkenleri ortamınız için güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="6639f-992">Update hello PowerShell variables for your environment.</span></span> <span data-ttu-id="6639f-993">Merhaba betik çalıştıktan sonra istendiğinde toorestart hello SAP küme grubu tooactivate hello değişiklikleri olması.</span><span class="sxs-lookup"><span data-stu-id="6639f-993">After hello script runs, you'll be prompted toorestart hello SAP cluster group tooactivate hello changes.</span></span>

  ```PowerShell
  $SAPSID = "PR1"      # SAP <SID>
  $ProbePort = 62000   # ProbePort of hello Azure Internal Load Balancer

  Clear-Host
  $SAPClusterRoleName = "SAP $SAPSID"
  $SAPIPresourceName = "SAP $SAPSID IP"
  $SAPIPResourceClusterParameters =  Get-ClusterResource $SAPIPresourceName | Get-ClusterParameter
  $IPAddress = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "Address" }).Value
  $NetworkName = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "Network" }).Value
  $SubnetMask = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "SubnetMask" }).Value
  $OverrideAddressMatch = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "OverrideAddressMatch" }).Value
  $EnableDhcp = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "EnableDhcp" }).Value
  $OldProbePort = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "ProbePort" }).Value

  $var = Get-ClusterResource | Where-Object {  $_.name -eq $SAPIPresourceName  }

  Write-Host "Current configuration parameters for SAP IP cluster resource '$SAPIPresourceName' are:" -ForegroundColor Cyan
  Get-ClusterResource -Name $SAPIPresourceName | Get-ClusterParameter

  Write-Host
  Write-Host "Current probe port property of hello SAP cluster resource '$SAPIPresourceName' is '$OldProbePort'." -ForegroundColor Cyan
  Write-Host
  Write-Host "Setting hello new probe port property of hello SAP cluster resource '$SAPIPresourceName' too'$ProbePort' ..." -ForegroundColor Cyan
  Write-Host

  $var | Set-ClusterParameter -Multiple @{"Address"=$IPAddress;"ProbePort"=$ProbePort;"Subnetmask"=$SubnetMask;"Network"=$NetworkName;"OverrideAddressMatch"=$OverrideAddressMatch;"EnableDhcp"=$EnableDhcp}

  Write-Host

  $ActivateChanges = Read-Host "Do you want tootake restart SAP cluster role '$SAPClusterRoleName', tooactivate hello changes (yes/no)?"

  if($ActivateChanges -eq "yes"){
  Write-Host
  Write-Host "Activating changes..." -ForegroundColor Cyan

  Write-Host
  write-host "Taking SAP cluster IP resource '$SAPIPresourceName' offline ..." -ForegroundColor Cyan
  Stop-ClusterResource -Name $SAPIPresourceName
  sleep 5

  Write-Host "Starting SAP cluster role '$SAPClusterRoleName' ..." -ForegroundColor Cyan
  Start-ClusterGroup -Name $SAPClusterRoleName

  Write-Host "New ProbePort parameter is active." -ForegroundColor Green
  Write-Host

  Write-Host "New configuration parameters for SAP IP cluster resource '$SAPIPresourceName':" -ForegroundColor Cyan
  Write-Host
  Get-ClusterResource -Name $SAPIPresourceName | Get-ClusterParameter
  }else
  {
  Write-Host "Changes are not activated."
  }
  ```

  <span data-ttu-id="6639f-994">Merhaba aldıktan sonra  **SAP <*SID*> ** Küme rolünü, doğrulayın **ProbePort** toohello yeni değerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="6639f-994">After you bring hello **SAP <*SID*>** cluster role online, verify that **ProbePort** is set toohello new value.</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter

  ```

  ![Şekil 59: hello yeni değeri ayarlandıktan sonra hello küme bağlantı noktası araştırma][sap-ha-guide-figure-3049]

  <span data-ttu-id="6639f-996">_**Şekil 59:** hello yeni değeri ayarlandıktan sonra hello küme bağlantı noktası araştırma_</span><span class="sxs-lookup"><span data-stu-id="6639f-996">_**Figure 59:** Probe hello cluster port after you set hello new value_</span></span>

#### <span data-ttu-id="6639f-997"><a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a>Merhaba Windows Güvenlik Duvarı araştırma bağlantı noktasını açın</span><span class="sxs-lookup"><span data-stu-id="6639f-997"><a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a> Open hello Windows firewall probe port</span></span>

<span data-ttu-id="6639f-998">Tooopen her iki küme düğümlerinde Windows Güvenlik Duvarı araştırma bağlantı gerekir.</span><span class="sxs-lookup"><span data-stu-id="6639f-998">You need tooopen a Windows firewall probe port on both cluster nodes.</span></span> <span data-ttu-id="6639f-999">Komut dosyası tooopen bir Windows Güvenlik Duvarı araştırma bağlantı noktasını aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="6639f-999">Use hello following script tooopen a Windows firewall probe port.</span></span> <span data-ttu-id="6639f-1000">Merhaba PowerShell değişkenleri ortamınız için güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="6639f-1000">Update hello PowerShell variables for your environment.</span></span>

  ```PowerShell
  $ProbePort = 62000   # ProbePort of hello Azure Internal Load Balancer

  New-NetFirewallRule -Name AzureProbePort -DisplayName "Rule for Azure Probe Port" -Direction Inbound -Action Allow -Protocol TCP -LocalPort $ProbePort
  ```

<span data-ttu-id="6639f-1001">Merhaba **ProbePort** çok ayarlanır**62000**.</span><span class="sxs-lookup"><span data-stu-id="6639f-1001">hello **ProbePort** is set too**62000**.</span></span> <span data-ttu-id="6639f-1002">Merhaba dosya paylaşımına erişmek artık  **\\\ascsha-clsap\sapmnt** diğer konakları, gibi kadar **ascsha dbas**.</span><span class="sxs-lookup"><span data-stu-id="6639f-1002">Now you can access hello file share **\\\ascsha-clsap\sapmnt** from other hosts, such as from **ascsha-dbas**.</span></span>

### <span data-ttu-id="6639f-1003"><a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a>Merhaba veritabanı örneğini yükleyin</span><span class="sxs-lookup"><span data-stu-id="6639f-1003"><a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a> Install hello database instance</span></span>

<span data-ttu-id="6639f-1004">tooinstall hello veritabanı örneği, hello SAP yükleme belgelerini açıklanan hello süreci izleyin.</span><span class="sxs-lookup"><span data-stu-id="6639f-1004">tooinstall hello database instance, follow hello process described in hello SAP installation documentation.</span></span>

### <span data-ttu-id="6639f-1005"><a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a>Merhaba ikinci küme düğümü yükleme</span><span class="sxs-lookup"><span data-stu-id="6639f-1005"><a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a> Install hello second cluster node</span></span>

<span data-ttu-id="6639f-1006">tooinstall hello ikinci küme, hello SAP Yükleme Kılavuzu'na hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="6639f-1006">tooinstall hello second cluster, follow hello steps in hello SAP installation guide.</span></span>

### <span data-ttu-id="6639f-1007"><a name="094bc895-31d4-4471-91cc-1513b64e406a"></a>Merhaba SAP ERS Windows hizmet örneği Hello başlangıç türünü değiştirme</span><span class="sxs-lookup"><span data-stu-id="6639f-1007"><a name="094bc895-31d4-4471-91cc-1513b64e406a"></a> Change hello start type of hello SAP ERS Windows service instance</span></span>

<span data-ttu-id="6639f-1008">Merhaba SAP ERS Windows hizmeti başlangıç türünü Hello çok değiştirme**otomatik (Gecikmeli Başlatma)** her iki küme düğümlerinde.</span><span class="sxs-lookup"><span data-stu-id="6639f-1008">Change hello start type of hello SAP ERS Windows service too**Automatic (Delayed Start)** on both cluster nodes.</span></span>

![Şekil 60: hello SAP ERS örneği toodelayed otomatik hello hizmet türünü değiştir][sap-ha-guide-figure-3050]

<span data-ttu-id="6639f-1010">_**Şekil 60:** hello hizmet türünü hello SAP ERS örneği toodelayed otomatik_</span><span class="sxs-lookup"><span data-stu-id="6639f-1010">_**Figure 60:** Change hello service type for hello SAP ERS instance toodelayed automatic_</span></span>

### <span data-ttu-id="6639f-1011"><a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a>Merhaba SAP birincil uygulama sunucusu yükleme</span><span class="sxs-lookup"><span data-stu-id="6639f-1011"><a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a> Install hello SAP Primary Application Server</span></span>

<span data-ttu-id="6639f-1012">Merhaba birincil uygulama sunucusu (PAS) örneğini yükleyin <*SID*> - dı - 0 hello sanal makinede, belirlediğiniz toohost hello PAS.</span><span class="sxs-lookup"><span data-stu-id="6639f-1012">Install hello Primary Application Server (PAS) instance <*SID*>-di-0 on hello virtual machine that you've designated toohost hello PAS.</span></span> <span data-ttu-id="6639f-1013">Azure veya DataKeeper özgü ayarları bir bağımlılık yoktur.</span><span class="sxs-lookup"><span data-stu-id="6639f-1013">There are no dependencies on Azure or DataKeeper-specific settings.</span></span>

### <span data-ttu-id="6639f-1014"><a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a>Merhaba SAP ek uygulama sunucusu yükleme</span><span class="sxs-lookup"><span data-stu-id="6639f-1014"><a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a> Install hello SAP Additional Application Server</span></span>

<span data-ttu-id="6639f-1015">Bir SAP ek uygulama sunucusu (AAS) tüm hello sanal SAP uygulama sunucusu örneği toohost tasarladığınız makinelere yükleyin.</span><span class="sxs-lookup"><span data-stu-id="6639f-1015">Install an SAP Additional Application Server (AAS) on all hello virtual machines that you've designated toohost an SAP Application Server instance.</span></span> <span data-ttu-id="6639f-1016">Örneğin, <*SID*> - dı - 1 çok <*SID*> - di -&lt;n&gt;.</span><span class="sxs-lookup"><span data-stu-id="6639f-1016">For example, on <*SID*>-di-1 too<*SID*>-di-&lt;n&gt;.</span></span>

> [!NOTE]
> <span data-ttu-id="6639f-1017">Yüksek kullanılabilirlik SAP NetWeaver sistem hello yüklemesini tamamlar.</span><span class="sxs-lookup"><span data-stu-id="6639f-1017">This finishes hello installation of a high-availability SAP NetWeaver system.</span></span> <span data-ttu-id="6639f-1018">Ardından, yük devretme testi ile devam edin.</span><span class="sxs-lookup"><span data-stu-id="6639f-1018">Next, proceed with failover testing.</span></span>
>


## <span data-ttu-id="6639f-1019"><a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a>Test Hello SAP ASCS/SCS örneği yük devretme ve SIOS çoğaltma</span><span class="sxs-lookup"><span data-stu-id="6639f-1019"><a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a> Test hello SAP ASCS/SCS instance failover and SIOS replication</span></span>
<span data-ttu-id="6639f-1020">Bu kolay tootest ve yük devretme kümesi Yöneticisi'ni ve hello SIOS DataKeeper yönetimi ve yapılandırması aracını kullanarak bir SAP ASCS/SCS örneği yük devretme ve SIOS disk çoğaltması izleyin.</span><span class="sxs-lookup"><span data-stu-id="6639f-1020">It's easy tootest and monitor an SAP ASCS/SCS instance failover and SIOS disk replication by using Failover Cluster Manager and hello SIOS DataKeeper Management and Configuration tool.</span></span>

### <span data-ttu-id="6639f-1021"><a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a>SAP ASCS/SCS örneği bir küme düğümünde çalışıyor</span><span class="sxs-lookup"><span data-stu-id="6639f-1021"><a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a> SAP ASCS/SCS instance is running on cluster node A</span></span>

<span data-ttu-id="6639f-1022">Merhaba **SAP PR1** küme grubu A'daki küme düğümünde çalışıyor Örneğin, **pr1 ascs 0**.</span><span class="sxs-lookup"><span data-stu-id="6639f-1022">hello **SAP PR1** cluster group is running on cluster node A. For example, on **pr1-ascs-0**.</span></span> <span data-ttu-id="6639f-1023">Merhaba parçası olan paylaşılan hello disk sürücüsü S, Ata **SAP PR1** küme grubu ve hangi hello ASCS/SCS örnek kullanan, toocluster düğümü A.</span><span class="sxs-lookup"><span data-stu-id="6639f-1023">Assign hello shared disk drive S, which is part of hello **SAP PR1** cluster group, and which hello ASCS/SCS instance uses, toocluster node A.</span></span>

![Şekil 61: Yük devretme kümesi Yöneticisi: merhaba < SID > SAP küme grubu, bir küme düğümünde çalışıyor][sap-ha-guide-figure-5000]

<span data-ttu-id="6639f-1025">_**Şekil 61:** yük devretme kümesi Yöneticisi: SAP merhaba <*SID*> Küme grubu, bir küme düğümünde çalışıyor_</span><span class="sxs-lookup"><span data-stu-id="6639f-1025">_**Figure 61:** Failover Cluster Manager: hello SAP <*SID*> cluster group is running on cluster node A_</span></span>

<span data-ttu-id="6639f-1026">Merhaba SIOS DataKeeper yönetim ve Yapılandırma Aracı'nda verileri sürücüsünden hello kaynak birim S küme düğümünde bir toohello hedef birim sürücü S B. küme düğümünde eşzamanlı olarak çoğaltılır, hello paylaşılan disk görebilirsiniz Örneğin, gelen çoğaltılır **pr1 ascs 0 [10.0.0.40]** çok**pr1 ascs 1 [10.0.0.41]**.</span><span class="sxs-lookup"><span data-stu-id="6639f-1026">In hello SIOS DataKeeper Management and Configuration tool, you can see that hello shared disk data is synchronously replicated from hello source volume drive S on cluster node A toohello target volume drive S on cluster node B. For example, it's replicated from **pr1-ascs-0 [10.0.0.40]** too**pr1-ascs-1 [10.0.0.41]**.</span></span>

![Şekil 62: SIOS DataKeeper içinde hello yerel birim B toocluster düğümü küme düğümünden Çoğalt][sap-ha-guide-figure-5001]

<span data-ttu-id="6639f-1028">_**Şekil 62:** SIOS DataKeeper içinde hello yerel birim B toocluster düğümü küme düğümünden Çoğalt_</span><span class="sxs-lookup"><span data-stu-id="6639f-1028">_**Figure 62:** In SIOS DataKeeper, replicate hello local volume from cluster node A toocluster node B_</span></span>

### <span data-ttu-id="6639f-1029"><a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a>Yük devretme işlemini düğümü toonode B</span><span class="sxs-lookup"><span data-stu-id="6639f-1029"><a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a> Failover from node A toonode B</span></span>

1.  <span data-ttu-id="6639f-1030">Bu seçenekler tooinitiate birini hello SAP yük devretmesi seçin <*SID*> Küme grubu küme düğümü toocluster düğümünden B:</span><span class="sxs-lookup"><span data-stu-id="6639f-1030">Choose one of these options tooinitiate a failover of hello SAP <*SID*> cluster group from cluster node A toocluster node B:</span></span>
  - <span data-ttu-id="6639f-1031">Yük Devretme Kümesi Yöneticisi'ni kullanın</span><span class="sxs-lookup"><span data-stu-id="6639f-1031">Use Failover Cluster Manager</span></span>  
  - <span data-ttu-id="6639f-1032">Yük devretme kümesi PowerShell kullanma</span><span class="sxs-lookup"><span data-stu-id="6639f-1032">Use Failover Cluster PowerShell</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPClusterGroup = "SAP $SAPSID"
  Move-ClusterGroup -Name $SAPClusterGroup

  ```
2.  <span data-ttu-id="6639f-1033">Küme düğümü bir hello Windows konuk işletim sistemi içinde yeniden (Bu hello SAP otomatik olarak yük devretmesi başlatır <*SID*> Küme düğümü toonode B grubundan).</span><span class="sxs-lookup"><span data-stu-id="6639f-1033">Restart cluster node A within hello Windows guest operating system (this initiates an automatic failover of hello SAP <*SID*> cluster group from node A toonode B).</span></span>  
3.  <span data-ttu-id="6639f-1034">Küme düğümü hello Azure portal A'dan yeniden (Bu hello SAP otomatik olarak yük devretmesi başlatır <*SID*> Küme düğümü toonode B grubundan).</span><span class="sxs-lookup"><span data-stu-id="6639f-1034">Restart cluster node A from hello Azure portal (this initiates an automatic failover of hello SAP <*SID*> cluster group from node A toonode B).</span></span>  
4.  <span data-ttu-id="6639f-1035">Azure PowerShell kullanarak küme düğümü bir yeniden başlatma (Bu hello SAP otomatik olarak yük devretmesi başlatır <*SID*> Küme düğümü toonode B grubundan).</span><span class="sxs-lookup"><span data-stu-id="6639f-1035">Restart cluster node A by using Azure PowerShell (this initiates an automatic failover of hello SAP <*SID*> cluster group from node A toonode B).</span></span>

  <span data-ttu-id="6639f-1036">Yük devretme sonrasında, SAP merhaba <*SID*> Küme grubu b küme düğümünde çalışıyor Örneğin, üzerinde çalıştırıldığı **pr1 ascs 1**.</span><span class="sxs-lookup"><span data-stu-id="6639f-1036">After failover, hello SAP <*SID*> cluster group is running on cluster node B. For example, it's running on **pr1-ascs-1**.</span></span>

  ![Şekil 63: Yük devretme kümesi Yöneticisi'nde hello SAP < SID > Küme grubu B küme düğümünde çalışıyor][sap-ha-guide-figure-5002]

  <span data-ttu-id="6639f-1038">_**Şekil 63**: yük devretme kümesi Yöneticisi'nde hello SAP <*SID*> Küme grubu B küme düğümünde çalışıyor_</span><span class="sxs-lookup"><span data-stu-id="6639f-1038">_**Figure 63**: In Failover Cluster Manager, hello SAP <*SID*> cluster group is running on cluster node B_</span></span>

  <span data-ttu-id="6639f-1039">Merhaba paylaşılan disk artık takılı kümede düğüm B. SIOS DataKeeper veri sürücüsünden kaynak birim S A. küme düğümünde Küme düğümü B tootarget birimin sürücü S çoğaltma Örneğin, gelen çoğaltma **pr1 ascs 1 [10.0.0.41]** çok**pr1 ascs 0 [10.0.0.40]**.</span><span class="sxs-lookup"><span data-stu-id="6639f-1039">hello shared disk is now mounted on cluster node B. SIOS DataKeeper is replicating data from source volume drive S on cluster node B tootarget volume drive S on cluster node A. For example, it's replicating from **pr1-ascs-1 [10.0.0.41]** too**pr1-ascs-0 [10.0.0.40]**.</span></span>

  ![Şekil 64: Hello yerel birim SIOS DataKeeper, küme düğümü B toocluster düğümünden A çoğaltır.][sap-ha-guide-figure-5003]

  <span data-ttu-id="6639f-1041">_**Şekil 64:** SIOS DataKeeper çoğaltır hello yerel birim küme düğümü B toocluster düğümünden A_</span><span class="sxs-lookup"><span data-stu-id="6639f-1041">_**Figure 64:** SIOS DataKeeper replicates hello local volume from cluster node B toocluster node A_</span></span>
