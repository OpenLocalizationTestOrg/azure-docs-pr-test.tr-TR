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
# <a name="high-availability-for-sap-netweaver-on-azure-vms"></a>Azure vm'lerinde SAP NetWeaver için yüksek kullanılabilirlik

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


Azure sanal makinelerin işlem, depolama ve ağ kaynaklarına, en az sürede ve uzun tedarik döngüleri olmadan gereken kuruluşlar için hello çözümü şeklindedir. Azure sanal makineleri toodeploy Klasik uygulamaları SAP NetWeaver tabanlı ABAP, Java ve ABAP + Java yığını gibi kullanabilirsiniz. Güvenilirlik ve kullanılabilirlik ek şirket içi kaynaklar olmadan genişletir. Azure sanal makineleri şirket içi bağlantılar, Azure sanal makineler, kuruluşunuzun şirket içi etki alanları, özel Bulutlar ve SAP sistem yatay tümleştirebilir şekilde destekler.

Bu makalede, toodeploy yüksek kullanılabilirlik SAP sistemleri Azure'da hello Azure Resource Manager dağıtım modelini kullanarak alabilecek hello adımları kapsar. Biz bu ana görevlerinde ilerlemenizde:

* Merhaba, doğru SAP notlar ve yükleme kılavuzları, hello listelenen Bul [kaynakları] [ sap-ha-guide-2] bölümü. Bu makalede SAP yükleme belgelerini tamamlar ve yardımcı olabilecek hello birincil kaynaklardır SAP notları yükleyip belirli platformlar SAP yazılımı dağıtın.
* Merhaba farklarını hello Azure Resource Manager dağıtım modeli ve hello Azure Klasik dağıtım modeli hakkında bilgi edinin.
* Azure dağıtımınız için doğru hello modeli seçebilmeniz için Windows Server Yük Devretme Kümelemesi çekirdek modları hakkında bilgi edinin.
* Azure hizmetlerinde paylaşılan Windows Server Yük Devretme Kümelemesi depolama hakkında bilgi edinin.
* Korunmasına nasıl yardımcı toohelp başarısızlık durumunu tek nokta bileşenleri gibi gelişmiş iş uygulama programlama (ABAP) SAP merkezi Hizmetleri (ASCS) öğrenin / SAP merkezi Hizmetleri (SCS) ve veritabanı yönetim sistemi (DBMS) ve yedek bileşenlerin SAP gibi Azure uygulama sunucusu.
* Adım adım örnek bir yükleme ve bir Windows Server Yük Devretme Kümelemesi küme azure'da yüksek kullanılabilirlik SAP sisteminde yapılandırmasının, Azure Kaynak Yöneticisi'ni kullanarak izleyin.
* Ek adımlar gerekli toouse Windows Server Yük Devretme Kümelemesi azure'da, ancak, bir şirket içi dağıtımda gerekli olmayan hakkında bilgi edinin.

toosimplify dağıtımı ve yapılandırması, bu makalede, kullandığımız SAP üç katmanlı yüksek kullanılabilirlik Resource Manager şablonları hello. Merhaba şablonları bir yüksek kullanılabilirlik SAP sistemi için gereksinim duyduğunuz hello tüm altyapının dağıtımını otomatik hale getirme. Merhaba altyapı SAP uygulama performans standart (SAP) boyutlandırma SAP sisteminizin de destekler.

## <a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a>Önkoşulları
Başlamadan önce aşağıdaki bölümlerde hello açıklanan hello önkoşulları karşıladığından emin olun. Tüm kaynaklar listelenen hello emin toocheck de [kaynakları] [ sap-ha-guide-2] bölümü.

Bu makalede, Azure Resource Manager şablonları için kullandığımız [üç katmanlı SAP NetWeaver](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image/). Şablonları yararlı bir genel bakış için bkz: [SAP Azure Resource Manager şablonları](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/).

## <a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a>Kaynakları
Bu makaleler Azure SAP dağıtımlarda kapsar:

* [Azure sanal makineleri planlama ve uygulama SAP NetWeaver için][planning-guide]
* [SAP NetWeaver için Azure sanal makineler dağıtımı][deployment-guide]
* [SAP NetWeaver için Azure sanal makineleri DBMS dağıtımı][dbms-guide]
* [Azure sanal makineler için yüksek oranda kullanılabilirlik SAP NetWeaver (Bu Kılavuzu)][sap-ha-guide]

> [!NOTE]
> Mümkün olduğunda, SAP Yükleme Kılavuzu'na başvuran bir bağlantı toohello sunuyoruz (Merhaba bkz [SAP yükleme kılavuzları][sap-installation-guides]). Önkoşullar ve hello yükleme işlemi, onun bir fikir tooread hello SAP NetWeaver yükleme dikkatle kılavuzları hakkında bilgi için. Bu makalede yalnızca Azure sanal makineler ile kullanabileceğiniz SAP NetWeaver tabanlı sistemler için belirli görevler yer almaktadır.
>
>

Bu SAP Notlar SAP Azure içinde ilgili toohello konu şunlardır:

| Not numarası | Başlık |
| --- | --- |
| [1928533] |Azure üzerinde SAP uygulamaları: desteklenen ürünler ve boyutlandırma |
| [2015553] |Microsoft Azure üzerinde SAP: Destek önkoşulları |
| [1999351] |Azure için SAP izleme Gelişmiş |
| [2178632] |Microsoft Azure üzerinde SAP için ölçümleri izleme anahtarı |
| [1999351] |Windows sanallaştırma: İzleme Gelişmiş |
| [2243692] |SAP DBMS örneği için Azure Premium SSD depolama kullanımı |

Merhaba hakkında daha fazla bilgi [Azure abonelikleri sınırlamaları][azure-subscription-service-limits-subscription]genel varsayılan sınırlamalar ve en fazla sınırlamalar dahil olmak üzere.

## <a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>Yüksek kullanılabilirlik SAP hello Azure Klasik dağıtım modeli ve Azure Resource Manager ile
Hello Azure Resource Manager ve Azure Klasik dağıtım modelleri alanları aşağıdaki hello farklı durum vardır:

- Kaynak grupları
- Azure iç yük dengeleyici bağımlılığını hello Azure kaynak grubu
- SAP çoklu SID senaryolar için destek

### <a name="f76af273-1993-4d83-b12d-65deeae23686"></a>Kaynak grupları
Azure Kaynak Yöneticisi'nde, kaynak grupları toomanage tüm hello uygulama kaynakları Azure aboneliğinizde kullanabilirsiniz. Tüm kaynaklara sahip bir kaynak grubunda tümleşik bir yaklaşım hello aynı yaşam döngüsü. Tüm kaynaklar hello aynı örneğin, oluşturulan zaman ve bunların hello silinir aynı anda. [Kaynak grupları](../../../azure-resource-manager/resource-group-overview.md#resource-groups) hakkında daha fazla bilgi edinin.

### <a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a>Azure iç yük dengeleyici bağımlılığını hello Azure kaynak grubu

Hello Azure Klasik dağıtım modelinde hello Azure iç yük dengeleyici (Azure Yük Dengeleyici Hizmeti) ile Merhaba bulut hizmeti grubu arasında bir bağımlılık yoktur. Her iç yük dengeleyici bir bulut hizmeti grubu olması gerekiyor.

Azure Kaynak Yöneticisi'nde, bir Azure kaynak grubu toouse Azure yük dengeleyici gerek yoktur. Merhaba daha basit ve daha esnek ortamıdır.

### <a name="support-for-sap-multi-sid-scenarios"></a>SAP çoklu SID senaryolar için destek

Azure Kaynak Yöneticisi'nde, birden çok SAP sistem tanımlayıcısı (SID) ASCS/SCS örnekleri bir küme içinde yükleyebilirsiniz. Çoklu SID örnekleri her Azure iç yük dengeleyici için birden fazla IP adresine yönelik destek nedeniyle mümkündür.

toouse Azure Klasik dağıtım modeli Merhaba, açıklanan hello yordamları izleyin [SAP NetWeaver azure'da: SIOS DataKeeper ile azure'da Windows Server Yük Devretme Kümelemesi kullanarak SAP ASCS/SCS kümeleme örneklerini](http://go.microsoft.com/fwlink/?LinkId=613056).

> [!IMPORTANT]
> SAP yüklemeleri için hello Azure Resource Manager dağıtım modeli kullanmanız önerilir. Merhaba Klasik dağıtım modelinde bulunmayan birçok avantaj sunar. Azure hakkında daha fazla bilgi [dağıtım modellerini][virtual-machines-azure-resource-manager-architecture-benefits-arm].   
>
>

## <a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a>Windows Server Yük Devretme Kümelemesi
Windows Server Yük Devretme Kümelemesi hello yüksek kullanılabilirlik SAP ASCS/SCS yükleme ve Windows'da DBMS temelini oluşturur.

Bir yük devretme kümesi, uygulamaların ve hizmetlerin kullanılabilirliğini tooincrease hello birlikte çalışan 1 + n bağımsız sunucular (düğümler) grubudur. Bir düğüm hatası oluşursa, Windows Server Yük Devretme Kümelemesi hello sayısı bir sağlıklı korurken oluşabilecek hesaplar küme tooprovide uygulamalar ve hizmetler. Farklı bir çekirdek modu tooachieve Yük Devretme Kümelemesi seçebilirsiniz.

### <a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a>Çekirdek modu
Windows Server Yük Devretme Kümelemesi kullanırken dört çekirdek modlarından seçim yapabilirsiniz:

* **Düğüm çoğunluğu**. Merhaba kümedeki her düğüme oy kullanabilir. Küme işlevleriyle yalnızca Çoğunluk oyu, diğer bir deyişle, yarısından fazlası hello oyları ile Merhaba. Bu seçenek eşit sayıda düğüme sahip kümeler için önerilir. Örneğin, üç yedi düğümlü bir küme düğümünde başarısız olabilir ve hello küme durağan Çoğunluk erişir ve toorun devam eder.  
* **Düğüm ve Disk Çoğunluğu**. Her düğüm ve hello küme depolama atanmış bir disk (bir disk tanığı) ne zaman kullanılabilir olduğunu ve iletişim oy kullanabilir. Merhaba küme işlevleriyle yalnızca hello çoğunu oylarının, diğer bir deyişle, yarısından fazlası hello oyları ile. Bu mod, bir küme ortamında düğümlerinin çift sayıda mantıklıdır. Yarı hello düğümler ve hello disk çevrimiçi hello küme sağlam durumda kalır.
* **Düğüm ve dosya paylaşımı çoğunluğu**. Yönetici hello bir dosya paylaşımı (dosya paylaşım tanığı) oluşturur her düğüm artı, hello düğüm ve dosya paylaşımı kullanılabilir ve iletişimde oy kullanabilir. Merhaba küme işlevleriyle yalnızca hello çoğunu oylarının, diğer bir deyişle, yarısından fazlası hello oyları ile. Bu mod, bir küme ortamında düğümlerinin çift sayıda mantıklıdır. Benzer toohello düğüm ve Disk Çoğunluğu modu olan, ancak Tanık diski yerine bir Tanık dosya paylaşımı kullanır. Bu mod kolay tooimplement bağlıdır, ancak hello dosyasını paylaşırsanız, kendisini yüksek oranda kullanılabilir değil, tek bir hata noktası olabilir.
* **Çoğunluk yok: Yalnızca Disk**. bir düğüm kullanılabilir ve belirli bir disk hello küme depolama ile iletişim ise hello küme çekirdeği vardır. Ayrıca, disk ile iletişimi yalnızca hello düğümlerini hello kümeye katılabilir. Bu mod kullanmamanızı öneririz.
 

## <a name="fdfee875-6e66-483a-a343-14bbaee33275"></a>Şirket içi Windows Server Yük devretme
Şekil 1 iki düğümden oluşan bir küme gösterir. Merhaba, hello düğümler arasında ağ bağlantısı başarısız olur ve her iki düğüm kalması ve çalıştıran, bir çekirdek disk veya dosya paylaşımı hangi düğümün tooprovide hello kümenin uygulamaları ve Hizmetleri devam edecek belirler. erişim toohello çekirdek diski veya dosya paylaşımı hello düğüm Hizmetleri devam etmenizi sağlar hello olandır.

Bu örnek iki düğümlü bir küme kullandığından, hello düğüm ve dosya paylaşımı çoğunluğu çekirdek modu kullanın. Merhaba düğüm ve Disk Çoğunluğu geçerli bir seçenek de olur. Bir üretim ortamında, bir çekirdek disk kullanmanızı öneririz. Ağ ve depolama sistemi teknolojisi toomake kullanabilirsiniz, yüksek oranda kullanılabilir.

![Şekil 1: Bir Windows Server Yük Devretme Kümelemesi yapılandırma için SAP ASCS/SCS Azure örneği][sap-ha-guide-figure-1000]

_**Şekil 1:** bir Windows Server Yük Devretme Kümelemesi yapılandırma için SAP ASCS/SCS Azure örneği_

### <a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a>Paylaşılan depolama alanı
Şekil 1 iki düğümlü paylaşılan depolama kümesi ayrıca gösterir. Bir şirket içi paylaşılan depolama Küme Paylaşılan depolama hello kümedeki tüm düğümlerin algıla. Kilitleme mekanizması hello veri bozulmaya karşı korur. Tüm düğümler, başka bir düğüm başarısız olursa algılayabilir. Bir düğüm başarısız olursa, hello kalan düğümü hello depolama kaynakları aittir ve hizmetlerin kullanılabilirliğini hello sağlar.

> [!NOTE]
> SQL Server ile gibi bazı DBMS uygulamalarla yüksek kullanılabilirlik için Paylaşılan diskleri gerekmez. SQL Server Always On hello yerel bir küme düğümü toohello yerel disk başka bir küme düğümünün diskten DBMS veri ve günlük dosyalarını çoğaltır. Bu durumda, paylaşılan bir diskin hello Windows Küme yapılandırması gerekmez.
>
>

### <a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a>Ağ ve ad çözümlemesi
İstemci bilgisayarları hello küme DNS sunucusu sağlar, hello bir sanal IP adresi ve bir sanal ana bilgisayar adı üzerinden ulaşabilirsiniz. Merhaba içi düğümleri ve hello DNS sunucusu birden çok IP adresi işleyebilir.

Tipik bir kurulumunda iki veya daha fazla ağ bağlantıları kullanın:

* Adanmış bağlantı toohello depolama
* Merhaba sinyal için bir küme iç ağ bağlantısı
* Genel bir ağ istemcileri tooconnect toohello küme kullanın

## <a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a>Azure'da Windows Server Yük devretme
Toobare metal veya özel bulut dağıtımları karşılaştırıldığında Azure sanal makineleri ek adımlar tooconfigure Windows Server Yük Devretme Kümelemesi gerektirir. Paylaşılan bir küme diski derlerken hello SAP ASCS/SCS örneği için birkaç IP adresleri ve sanal ana bilgisayar adları tooset gerekir.

Bu makalede, anahtar kavramlar açıklanmaktadır ve ek adımlar gerekli toobuild bir SAP yüksek kullanılabilirlik merkezi Hizmetleri küme azure'da hello. Nasıl tooset hello üçüncü taraf aracı SIOS DataKeeper ayarlama ve nasıl tooconfigure hello Azure iç yük dengeleyici gösteriyoruz. Bu araçlar toocreate Windows Yük devretme, dosya paylaşım tanığı Azure ile kullanabilirsiniz.

![Şekil 2: Windows Server Yük devretme kümeleme yapılandırmasında Azure olmayan paylaşılan bir disk][sap-ha-guide-figure-1001]

_**Şekil 2:** Windows Server Yük devretme kümeleme yapılandırmasında Azure olmayan paylaşılan bir disk_

### <a name="1a464091-922b-48d7-9d08-7cecf757f341"></a>Paylaşılan disk Azure ile SIOS DataKeeper
Yüksek kullanılabilirlik SAP ASCS/SCS örneği için paylaşılan depolama küme. Eylül 2016 ' Azure paylaşılan depolama alanı, sunmaz gibi toocreate bir paylaşılan depolama kümesi kullanabilirsiniz. Üçüncü taraf yazılım SIOS DataKeeper Cluster Edition toocreate Küme Paylaşılan depolama taklit eden bir yansıtılmış depolama kullanabilirsiniz. gerçek zamanlı zaman uyumlu veri çoğaltma Hello SIOS çözümü sağlar. Bu küme için paylaşılan disk kaynağı nasıl oluşturabilirsiniz.

1. Ek Azure sanal sabit disk (VHD) tooeach hello sanal makineleri (VM'ler) bir Windows küme yapılandırmasında ekleyin.
2. SIOS DataKeeper Cluster Edition her iki sanal makine düğümde çalıştırın.
3. Merhaba ek bağlı VHD birimden hello kaynak sanal makine toohello ek bağlı VHD birim hello hedef sanal makinenin Merhaba içeriğine yansıtan SIOS DataKeeper Cluster Edition yapılandırın. SIOS DataKeeper hello kaynak ve hedef yerel birimleri soyutlar ve bunları tooWindows sunucu Yük Devretme Kümelemesi bir paylaşılan disk olarak sunar.

Hakkında daha fazla bilgi almak [SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/).

![Şekil 3: Windows Server Yük devretme kümeleme yapılandırmasında SIOS DataKeeper ile Azure][sap-ha-guide-figure-1002]

_**Şekil 3:** SIOS DataKeeper ile azure'da Windows Server Yük Devretme Kümelemesi yapılandırma_

> [!NOTE]
> SQL Server gibi bazı DBMS ürünleri ile yüksek kullanılabilirlik için Paylaşılan diskleri gerekmez. SQL Server Always On hello yerel bir küme düğümü toohello yerel disk başka bir küme düğümünün diskten DBMS veri ve günlük dosyalarını çoğaltır. Bu durumda, paylaşılan bir diskin hello Windows Küme yapılandırması gerekmez.
>
>

### <a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a>Azure ad çözümleme
Hello Azure bulut platformu hello seçeneği tooconfigure sanal IP adresleri, kayan IP adresleri gibi sunmuyor. Bir sanal IP adresi tooreach hello küme kaynağını hello bulutta bir alternatif çözüm tooset gerekir.
Azure hello Azure Yük Dengeleyici Hizmeti bir iç yük dengeleyici sahiptir. Merhaba iç yük dengeleyici ile istemcileri hello küme hello küme sanal IP adresi ulaşabilirsiniz.
Toodeploy hello iç yük dengeleyici hello küme düğümleri içeren hello kaynak grubundaki gerekir. Ardından, kuralları ile Merhaba araştırma hello iç yük dengeleyici bağlantı noktaları iletme tüm gerekli bağlantı noktası yapılandırın.
Merhaba istemcileri hello sanal ana bilgisayar adını bağlanabilir. Merhaba DNS sunucusu hello küme IP adresi ve hello kümesinin etkin düğümü toohello iletme hello iç yük dengeleyici tanıtıcıları bağlantı noktası çözümler.

## <a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a>SAP NetWeaver yüksek kullanılabilirlik Azure altyapısı olarak-hizmet (Iaas)
tooachieve SAP yazılım bileşenleri için ihtiyacınız tooprotect hello bileşenleri aşağıdaki gibi uygulama yüksek kullanılabilirlik, SAP:

* SAP uygulama sunucusu örneği
* SAP ASCS/SCS örneği
* DBMS sunucu

Yüksek kullanılabilirlik senaryolarını SAP bileşenlerinde koruma hakkında daha fazla bilgi için bkz: [Azure sanal makineleri planlama ve uygulama SAP NetWeaver için](planning-guide.md).

### <a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a>Yüksek kullanılabilirlik SAP uygulama sunucusu
Belirli bir yüksek kullanılabilirlik çözümü hello SAP uygulama sunucusu ile iletişim örnekleri için genellikle gerekmez. Artıklık tarafından yüksek kullanılabilirlik elde etmek ve iletişim birden çok başka durumlarda, Azure sanal makineleri yapılandıracaksınız. İki durumlarda, Azure sanal makinelerinde yüklü en az iki SAP uygulama örneğinin olması gerekir.

![Şekil 4: Yüksek oranda kullanılabilirlik SAP uygulama sunucusu][sap-ha-guide-figure-2000]

_**Şekil 4:** yüksek kullanılabilirlik SAP uygulama sunucusu_

Tüm sanal makinelerin konak SAP uygulama sunucusu örnekleri aynı Azure kullanılabilirlik kümesi hello yerleştirmeniz gerekir. Bir Azure kullanılabilirlik kümesi sağlar:

* Tüm sanal makineleri hello parçası olan aynı yükseltme etki alanı. Bir yükseltme etki alanı gibi hello sanal makineleri hello güncelleştirilmemiş emin olur planlı bakım kapalı kalma süresi sırasında aynı anda.
* Tüm sanal makineleri hello parçası olan aynı hata etki alanı. Hata etki alanı, örneğin, böylece hiç tek hata noktası hello tüm sanal makinelerin kullanılabilirliğini etkiler dağıtılan sanal makineler olduğundan emin olur.

Hakkında daha fazla çok bilgi[hello sanal makinelerin kullanılabilirliğini yönetme][virtual-machines-manage-availability].

Hello Azure depolama hesabına olası tek hata noktası olduğundan, önemli toohave olan en az iki Azure depolama hesapları, en az iki sanal makineye dağıtılır. İdeal bir kurulumunda hello diskler, SAP iletişim örneği çalıştıran her bir sanal makinenin farklı depolama hesabında dağıtılması.

### <a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a>Yüksek kullanılabilirlik SAP ASCS/SCS örneği
Şekil 5, yüksek kullanılabilirlik SAP ASCS/SCS örneğinin bir örnektir.

![Şekil 5: Yüksek oranda kullanılabilirlik SAP ASCS/SCS örneği][sap-ha-guide-figure-2001]

_**Şekil 5:** yüksek kullanılabilirlik SAP ASCS/SCS örneği_

#### <a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a>Windows Server Yük Devretme Kümelemesi Azure ile yüksek kullanılabilirlik SAP ASCS/SCS örneği
Toobare metal veya özel bulut dağıtımları karşılaştırıldığında Azure sanal makineleri ek adımlar tooconfigure Windows Server Yük Devretme Kümelemesi gerektirir. Windows Yük devretme toobuild, paylaşılan bir küme diski, birden fazla IP adresi, birçok sanal ana bilgisayar adlarını ve Azure iç yük dengeleyiciye SAP ASCS/SCS örneği kümeleme için gerekir. Biz bu hello makalenin sonraki bölümlerinde daha ayrıntılı ele alınmıştır.

![Şekil 6: Windows Server Yük Devretme Kümelemesi için SIOS DataKeeper kullanarak bir SAP ASCS/SCS yapılandırmasında Azure][sap-ha-guide-figure-1002]

_**Şekil 6:** Windows Server Yük Devretme Kümelemesi SIOS DataKeeper ile azure'da SAP ASCS/SCS yapılandırma_

### <a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a>Yüksek kullanılabilirlik DBMS örneği
Merhaba DBMS de tek bir iletişim noktası bir SAP içinde sistemidir. Tooprotect gereken bir yüksek kullanılabilirlik çözümü kullanarak. Şekil 7, Azure'da bir SQL Server Always On yüksek kullanılabilirlik çözümü gösterir, Windows Server Yük Devretme Kümelemesi ile hello Azure iç yük dengeleyici. SQL Server Always On kendi DBMS çoğaltma kullanılarak DBMS veri ve günlük dosyalarını çoğaltır. Bu durumda, paylaşılan diskleri, hangi hello tüm kurulumu basitleştirir küme.

![Şekil 7: SQL Server Always On ile bir yüksek kullanılabilirlik SAP DBMS örneği][sap-ha-guide-figure-2003]

_**Şekil 7:** SQL Server Always On ile bir yüksek kullanılabilirlik SAP DBMS örneği_

Hello Azure Resource Manager dağıtım modelini kullanarak Azure SQL Server Kümelemesi hakkında daha fazla bilgi için bu makalelere bakın:

* [Always On kullanılabilirlik grubu Resource Manager kullanarak Azure sanal makinelerinde el ile yapılandırın.][virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]
* [Azure'da Azure iç yük dengeleyiciye Always On kullanılabilirlik grubu için yapılandırın][virtual-machines-windows-portal-sql-alwayson-int-listener]

## <a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a>Uçtan uca yüksek kullanılabilirlik dağıtım senaryoları

### <a name="deployment-scenario-using-architectural-template-1"></a>Mimari şablonu 1'i kullanarak dağıtım senaryosu

Şekil 8 için azure'da bir SAP NetWeaver yüksek kullanılabilirlik mimari örneği gösterilmiştir **bir** SAP sistem. Bu senaryo aşağıdaki gibi kurun:

- Tek bir adanmış küme hello SAP ASCS/SCS örneği için kullanılır.
- Tek bir adanmış küme hello DBMS örneği için kullanılır.
- SAP uygulama sunucusu örnekleri kendi özel VM'ler dağıtılır.

![Şekil 8: yüksek oranda kullanılabilirlik mimari şablonu, 1 ile ayrılmış küme ASCS/SCS ve DBMS için SAP][sap-ha-guide-figure-2004]

_**Şekil 8:** ASCS/SCS ve DBMS ayrılmış kümelerine şablonu 1 mimari yüksek kullanılabilirlik, SAP_

### <a name="deployment-scenario-using-architectural-template-2"></a>Mimari şablon 2 kullanarak dağıtım senaryosu

Şekil 9 için azure'da bir SAP NetWeaver yüksek kullanılabilirlik mimari örneği gösterir **bir** SAP sistem. Bu senaryo aşağıdaki gibi kurun:

- Ayrılmış bir küme için kullanıldığından **her ikisi de** SAP ASCS/SCS örneği ve DBMS hello hello.
- SAP uygulama sunucusu örnekleri kendi özel VM'ler içinde dağıtılır.

![Şekil 9: yüksek oranda kullanılabilirlik mimari şablon 2 ile ayrılmış bir küme ASCS/SCS için ve ayrılmış bir küme DBMS için SAP][sap-ha-guide-figure-2005]

_**Şekil 9:** SAP yüksek kullanılabilirlik mimari şablon 2 ile ayrılmış bir küme ASCS/SCS için ve DBMS için ayrılmış bir küme_

### <a name="deployment-scenario-using-architectural-template-3"></a>Mimari şablonu 3 kullanan dağıtım senaryosu

Şekil 10 için azure'da bir SAP NetWeaver yüksek kullanılabilirlik mimari örneği gösterilir **iki** ile sistemleri, SAP &lt;SID1&gt; ve &lt;SID2&gt;. Bu senaryo aşağıdaki gibi kurun:

- Ayrılmış bir küme için kullanıldığından **her ikisi de** hello SAP ASCS/SCS SID1 örneği *ve* hello SAP ASCS/SCS SID2 örneği (bir küme için).
- Tek bir adanmış küme DBMS SID1 için kullanılır ve başka bir ayrılmış küme DBMS SID2 için kullanılır (iki küme).
- SAP uygulama sunucusu örnekleri hello SAP sistem SID1 için kendi özel VM'ler vardır.
- SAP uygulama sunucusu örnekleri hello SAP sistem SID2 için kendi özel VM'ler vardır.

![Şekil 10: yüksek kullanılabilirlik mimari şablonu 3, ile ayrılmış bir küme farklı ASCS/SCS örnekleri için SAP][sap-ha-guide-figure-6003]

_**Şekil 10:** SAP yüksek kullanılabilirlik mimari şablonu 3, ile ayrılmış bir küme için farklı ASCS/SCS örnekleri_

## <a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a>Merhaba altyapıyı hazırlama

### <a name="prepare-hello-infrastructure-for-architectural-template-1"></a>Mimari şablonu 1 için Hello altyapıyı hazırlama
Azure Resource Manager şablonları SAP için gerekli kaynakları dağıtımını kolaylaştırır.

Merhaba üç katmanlı şablonları Azure Kaynak Yöneticisi'nde de yüksek kullanılabilirlik senaryoları gibi mimari şablon iki küme olan 1'de destekler. Her küme bir SAP tek hata SAP ASCS/SCS ve DBMS noktasıdır.

İşte burada hello Örnek senaryo Biz bu makalede açıklamak için Azure Resource Manager şablonları elde edebilirsiniz:

* [Azure Market görüntüsü](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image)  
* [Özel görüntü](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image)

tooprepare hello altyapısı mimari şablon 1:

- Merhaba hello üzerinde Azure portal'ın **parametreleri** dikey penceresinde hello **SYSTEMAVAILABILITY** kutusunda **HA**.

  ![Şekil 11: Ayarlamak SAP yüksek kullanılabilirlik Azure Resource Manager parametreleri][sap-ha-guide-figure-3000]

_**Şekil 11:** ayarlamak SAP yüksek kullanılabilirlik Azure Resource Manager parametreleri_


  Merhaba şablonları oluşturun:

  * **Sanal makineler**:
    * SAP uygulama sunucusu sanal makineleri: <*SAPSystemSID*> - dı - <*numarası*>
    * ASCS/SCS küme sanal makineler: <*SAPSystemSID*> - ascs - <*numarası*>
    * DBMS küme: <*SAPSystemSID*> - db - <*numarası*>

  * **Ağ kartları ilişkili IP adresleriyle tüm sanal makineler için**:
    * <*SAPSystemSID*> - NIC - dı - <*numarası*>
    * <*SAPSystemSID*> - NIC - ascs - <*numarası*>
    * <*SAPSystemSID*> - NIC - db - <*numarası*>

  * **Azure depolama hesapları**

  * **Kullanılabilirlik grupları** için:
    * SAP uygulama sunucusu sanal makineleri: <*SAPSystemSID*> - avset - dı
    * SAP ASCS/SCS küme sanal makineler: <*SAPSystemSID*> - avset - ascs
    * DBMS küme sanal makineler: <*SAPSystemSID*> - avset - db

  * **Azure iç yük dengeleyici**:
    * Merhaba ASCS/SCS örneği ve IP adresi için tüm bağlantı noktaları ile <*SAPSystemSID*> - lb - ascs
    * Merhaba SQL Server DBMS ve IP adresi için tüm bağlantı noktaları ile <*SAPSystemSID*> - lb - db

  * **Ağ güvenlik grubu**: <*SAPSystemSID*> - nsg - ascs-0  
    * Açık bir dış Uzak Masaüstü Protokolü (RDP) bağlantı noktası toohello ile <*SAPSystemSID*> - ascs - 0 sanal makine

> [!NOTE]
> Tüm IP adresleri hello ağ kartları ve Azure iç yük dengeleyicileri **dinamik** varsayılan olarak. Çok değiştirme**statik** IP adresleri. Biz açıklamak nasıl toodo bu hello makalenin sonraki bölümlerinde yer.
>
>

### <a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a>Kurumsal ağ bağlantısı (şirket içi) toouse üretimde olan sanal makineleri dağıtma
Üretim SAP sistemleri için Azure sanal makinelerle dağıtımı [kurumsal ağ bağlantısı (şirket içi)] [ planning-guide-2.2] Azure siteden siteye VPN veya Azure ExpressRoute kullanarak.

> [!NOTE]
> Azure Virtual Network örneğinizi kullanabilirsiniz. Merhaba sanal ağ ve alt ağ zaten oluşturulmuş hazırlanmış ve.
>
>

1.  Merhaba hello üzerinde Azure portal'ın **parametreleri** dikey penceresinde hello **NEWOREXISTINGSUBNET** kutusunda **varolan**.
2.  Merhaba, **SUBNETID** kutusunda, hello tam dize, hazırlanan Azure ağınızın burada planladığınız toodeploy Azure sanal makinelerinizi SubnetID ekleyin.
3.  tooget tüm Azure ağ alt ağların bir listesine bu PowerShell komutunu çalıştırın:

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets
  ```

  Merhaba **kimliği** alan gösterir hello **SUBNETID**.
4. tooget tüm listesini **SUBNETID** değerleri, bu PowerShell komutunu çalıştırın:

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets.Id
  ```

  Merhaba **SUBNETID** şöyle görünür:

  ```
  /subscriptions/<SubscriptionId>/resourceGroups/<VPNName>/providers/Microsoft.Network/virtualNetworks/azureVnet/subnets/<SubnetName>
  ```

### <a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a>Test ve demo için yalnızca bulut SAP örnekleri dağıtma
Yüksek kullanılabilirlik SAP sisteminizi bir yalnızca bulut dağıtım modelinde dağıtabilirsiniz. Bu tür bir dağıtım öncelikle tanıtım ve test kullanım durumları için yararlıdır. Üretim kullanım durumları için uygun değildir.

- Merhaba hello üzerinde Azure portal'ın **parametreleri** dikey penceresinde hello **NEWOREXISTINGSUBNET** kutusunda **yeni**. Merhaba bırakın **SUBNETID** alanı boş.

  Azure sanal ağ ve alt hello Hello SAP Azure Resource Manager şablonu otomatik olarak oluşturur.

> [!NOTE]
> Ayrıca toodeploy gereken Active Directory için en az bir ayrılmış sanal makine ve DNS'de hello aynı Azure sanal ağı örneği. Merhaba şablonu, bu sanal makineleri oluşturmaz.
>
>


### <a name="prepare-hello-infrastructure-for-architectural-template-2"></a>Mimari şablon 2 Hello altyapıyı hazırlama

SAP toohelp basitleştirmek için gerekli altyapı kaynaklarıdır dağıtım SAP mimari şablon 2 için bu Azure Resource Manager şablonu kullanabilirsiniz.

İşte, bu dağıtım senaryosu için Azure Resource Manager şablonları burada alabilirsiniz:

* [Azure Market görüntüsü](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged)  
* [Özel görüntü](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged)


### <a name="prepare-hello-infrastructure-for-architectural-template-3"></a>Mimari şablonu 3 Hello altyapıyı hazırlama

Hello altyapıyı hazırlama ve yapılandırma için SAP **çoklu SID**. Örneğin, ek bir SAP ASCS/SCS örneğine ekleyebileceğiniz bir *varolan* küme yapılandırması. Daha fazla bilgi için bkz: [var olan bir küme yapılandırması toocreate bir SAP çoklu SID yapılandırma ek bir SAP ASCS/SCS örneğine Azure Kaynak Yöneticisi'nde yapılandırma][sap-ha-multi-sid-guide].

Yeni bir SID çoklu küme toocreate istiyorsanız hello multi-SID kullanabilirsiniz [GitHub hızlı başlangıç şablonlarında](https://github.com/Azure/azure-quickstart-templates).
Yeni bir SID çoklu küme toocreate, üç şablonları aşağıdaki toodeploy hello gerekir:

* [ASCS/SCS şablonu](#ASCS-SCS-template)
* [Veritabanı şablonu](#database-template)
* [Uygulama sunucuları şablonu](#application-servers-template)

Merhaba aşağıdaki bölümlerde hello şablonları ve hello şablonlarındaki tooprovide ihtiyacınız hello parametreleri hakkında daha fazla ayrıntı sahip.

#### <a name="ASCS-SCS-template"></a>ASCS/SCS şablonu

Merhaba ASCS/SCS şablonu toocreate birden çok ASCS/SCS örneği barındıran bir Windows Server Yük devretme kümesi kullanabileceğiniz iki sanal makine dağıtır.

Merhaba ASCS/SCS multi-SID şablonunda hello yukarı tooset [ASCS/SCS çoklu SID şablonu][sap-templates-3-tier-multisid-xscs-marketplace-image], hello şu parametreler için değerler girin:

  - **Kaynak önek**.  Kullanılan tooprefix olan hello kaynak öneki hello dağıtımı sırasında oluşturulan tüm kaynakları ayarlayın. Merhaba kaynakları tooonly bir SAP sistemine ait olmadığından hello kaynak hello öneki hello bir SAP sistem SID'si değil.  Merhaba önek arasında olmalıdır **üç ve altı karakter**.
  - **Yığın türü**. Merhaba yığını hello SAP sistem türünü seçin. Merhaba yığını türüne bağlı olarak, Azure yük dengeleyici (ABAP veya yalnızca Java) bir veya iki (ABAP + Java) özel IP adresleri SAP sistem başına var.
  -  **İşletim sistemi türü**. Merhaba sanal makinelerin Hello işletim sistemini seçin.
  -  **SAP sistem sayısı**. Merhaba numarasını seçin SAP sistemlerinin bu kümedeki tooinstall istiyor.
  -  **Sistem kullanılabilirliğini**. Seçin **HA**.
  -  **Yönetici kullanıcı adı ve yönetici parolası**. Kullanılan toosign toohello makinede olabilir yeni bir kullanıcı oluşturun.
  -  **Yeni veya var olan bir alt ağ**. Yeni sanal ağ ve alt oluşturulmalıdır veya mevcut bir alt kullanılmalıdır gerekip gerekmediğini belirleyin. Bağlı tooyour şirket içi ağ bir sanal ağ zaten varsa, seçin **varolan**.
  -  **Alt ağ kimliği**. Kümesi hello kimliği hello alt toowhich hello sanal makinelerin bağlanması gerekir. Sanal özel ağ (VPN) veya ExpressRoute sanal ağ tooconnect hello sanal makine tooyour şirket içi ağın Hello alt ağ seçin. Merhaba kimliği genellikle şu şekildedir:

   /Subscriptions/ <*abonelik kimliği*> /resourceGroups/ <*kaynak grubu adı*> /providers/Microsoft.Network/virtualNetworks/ <*sanal ağ adı*> /subnets/ <*alt ağ adı*>

Merhaba şablon birden çok SAP sistemlerini destekleyen bir Azure yük dengeleyici örneği dağıtır.

- Merhaba ASCS örnekleri örnek numarası 00, 10, 20 yapılandırılmış...
- Merhaba SCS örnekleri örnek numarası 01, 11, 21 yapılandırılmış...
- Merhaba ASCS kuyruğa çoğaltma sunucusuna (ERS) (yalnızca Linux) örnekleri örnek numarası 02, 12, 22 yapılandırılmış...
- Merhaba SCS ERS (yalnızca Linux) örnekleri örneği için 03, 13, 23 sayısı yapılandırılan...

Merhaba yük dengeleyici içeren 1 (Linux için 2) VIP(s), ASCS/SCS için 1 x VIP ve 1 x VIP ERS (yalnızca Linux) için.

Merhaba aşağıdaki listede tüm Yük Dengeleme kuralları (burada x hello hello SAP sistem, örneğin, 1, 2, 3... sayısıdır) içerir:
- Her SAP sistemi için Windows özel bağlantı noktaları: 445, 5985
- ASCS bağlantı noktası (örnek numarasını x0): 32 x 0, 36 x 0, 39 x 0, 81 x 0, 5 x 013, 5 x 014, 5 x 016
- SCS bağlantı noktası (örnek numarasını x1): 32 x 1, 33 x 1, 39 x 1, 81 x 1, 5 x 113, 5 x 114, 5 x 116
- ASCS ERS bağlantı noktaları (örnek numarasını x2) Linux'ta: 33 x 2, 5 x 213, 5 x 214, 5 x 216
- SCS ERS bağlantı noktaları (örnek numarasını x3) Linux'ta: 33 x 3, 5 x 313, 5 x 314, 5 x 316

Merhaba yük dengeleyici yapılandırılmış toouse hello araştırma bağlantı noktaları (burada x hello hello SAP sistem, örneğin, 1, 2, 3... sayısıdır) aşağıdaki gibidir:
- ASCS/SCS iç yük dengeleyici araştırması bağlantı noktası: 620 x 0
- ERS iç yük dengeleyici araştırması bağlantı noktası (yalnızca Linux): 621 x 2

#### <a name="database-template"></a>Veritabanı şablonu

Merhaba veritabanı şablonu bir dağıtır veya tooinstall kullanabileceğiniz iki sanal makine için bir SAP sistem ilişkisel veritabanı yönetim sistemine (RDBMS) hello. Beş SAP sistemleri için bir ASCS/SCS şablonu dağıtırsanız, örneğin, toodeploy bu şablonu beş kez gerekir.

Merhaba, hello veritabanı çoklu SID şablonu tooset [veritabanı çoklu SID şablonu][sap-templates-3-tier-multisid-db-marketplace-image], hello şu parametreler için değerler girin:

  -  **SAP sistem kimliği**. Merhaba tooinstall istediğiniz SAP sistemi Hello SAP sistem Kimliğini girin. Merhaba kimliği önek olarak dağıtılan hello kaynaklar için kullanılır.
  -  **İşletim sistemi türü**. Merhaba sanal makinelerin Hello işletim sistemini seçin.
  -  **DbType**. Merhaba türünü seçin hello veritabanı hello kümede tooinstall istiyor. Seçin **SQL** tooinstall Microsoft SQL Server istiyorsanız. Seçin **HANA** hello sanal makinelerde tooinstall SAP HANA planlıyorsanız. Tooselect hello doğru işletim sistemi türü olduğundan emin olun: seçin **Windows** HANA için Linux dağıtımı seçin ve SQL için. Merhaba, sanal makineler olacaktır bağlı toohello Azure yük dengeleyici toosupport seçili hello veritabanı türü yapılandırılır:
    * **SQL**. Merhaba yük dengeleyici Yük Dengeleme bağlantı noktası 1433 olur. Bu bağlantı noktası için SQL Server Always On kurulumunuzu emin toouse olun.
    * **HANA**. Merhaba yük dengeleyici Yük Dengeleme 35015 ve 35017 bağlantı noktalarını olur. İle örnek numarasını emin tooinstall SAP HANA olun **50**.
    Merhaba yük dengeleyici araştırması bağlantı noktasını 62550 kullanır.
  -  **SAP sistem boyutu**. SAP hello yeni sistem kümesi hello sayısını sağlar. Kaç tane SAP hello sistem gerektirir emin değilseniz, SAP teknolojisi iş ortağı veya sistem Tümleştirici isteyin.
  -  **Sistem kullanılabilirliğini**. Seçin **HA**.
  -  **Yönetici kullanıcı adı ve yönetici parolası**. Kullanılan toosign toohello makinede olabilir yeni bir kullanıcı oluşturun.
  -  **Alt ağ kimliği**. Merhaba hello ASCS/SCS şablonu hello dağıtımı sırasında kullanılan hello alt ağ Kimliğini veya hello oluşturulduğu hello alt ağ Kimliğini hello ASCS/SCS şablon dağıtımı bir parçası olarak girin.

#### <a name="application-servers-template"></a>Uygulama sunucuları şablonu

Merhaba uygulama sunucuları şablonu iki veya daha fazla sanal SAP uygulama sunucusu örneklerinin bir SAP sistemi için kullanılabilecek makineler dağıtır. Beş SAP sistemleri için bir ASCS/SCS şablonu dağıtırsanız, örneğin, toodeploy bu şablonu beş kez gerekir.

Merhaba uygulama sunucuları çoklu SID şablonunda, hello yukarı tooset [uygulama sunucuları çoklu SID şablonu][sap-templates-3-tier-multisid-apps-marketplace-image], hello şu parametreler için değerler girin:

  -  **SAP sistem kimliği**. Merhaba tooinstall istediğiniz SAP sistemi Hello SAP sistem Kimliğini girin. Merhaba kimliği önek olarak dağıtılan hello kaynaklar için kullanılır.
  -  **İşletim sistemi türü**. Merhaba sanal makinelerin Hello işletim sistemini seçin.
  -  **SAP sistem boyutu**. SAP hello yeni sistem Hello sayısını sağlar. Kaç tane SAP hello sistem gerektirir emin değilseniz, SAP teknolojisi iş ortağı veya sistem Tümleştirici isteyin.
  -  **Sistem kullanılabilirliğini**. Seçin **HA**.
  -  **Yönetici kullanıcı adı ve yönetici parolası**. Kullanılan toosign toohello makinede olabilir yeni bir kullanıcı oluşturun.
  -  **Alt ağ kimliği**. Merhaba hello ASCS/SCS şablonu hello dağıtımı sırasında kullanılan hello alt ağ Kimliğini veya hello oluşturulduğu hello alt ağ Kimliğini hello ASCS/SCS şablon dağıtımı bir parçası olarak girin.


### <a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a>Azure sanal ağı
Bizim örneğimizde, hello Azure sanal ağı hello adres alanı 10.0.0.0/16 şeklindedir. Adlı bir alt ağ yok **alt**, 10.0.0.0/24 adres aralığı olan. Bu sanal ağda, tüm sanal makineler ve iç yük dengeleyicileri dağıtılır.

> [!IMPORTANT]
> Toohello ağ ayarlarını hello konuk işletim sistemi içinde herhangi bir değişiklik yapmayın. Bu IP adresleri, DNS sunucuları ve alt ağ içerir. Azure'da tüm ağ ayarlarını yapılandırın. Merhaba Dinamik Ana Bilgisayar Yapılandırma Protokolü (DHCP) hizmetini ayarlarınızı yayar.
>
>

### <a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a>DNS IP adresleri

DNS IP adresleri tooset hello gerekli, aşağıdaki adımları hello.

1.  Hello hello üzerinde Azure portal'ın **DNS sunucuları** dikey penceresinde olduğundan emin olun, sanal ağ **DNS sunucuları** seçeneği çok ayarlamak**özel DNS**.
2.  Sahip olduğunuz ağ Hello türüne göre ayarlarınızı seçin. Daha fazla bilgi için kaynakları aşağıdaki hello bakın:
    * [Kurumsal ağ bağlantısı (şirket içi)][planning-guide-2.2]: hello hello şirket içi DNS sunucularının IP adreslerini ekleyin.  
    Azure'da çalışan şirket içi DNS sunucuları toohello sanal makineleri genişletebilirsiniz. Bu senaryoda hello Azure hello IP adreslerini ekleyebilirsiniz hello DNS hizmetinin çalıştığı sanal makineler.
    * [Yalnızca bulut dağıtım][planning-guide-2.1]: hello ek bir sanal makineyi dağıtmak, bir DNS sunucusu olarak hizmet veren aynı sanal ağ örneği. Hello Azure Hello IP adreslerini eklemek toorun DNS hizmetini ayarlama sanal makineler.

    ![Şekil 12: Azure sanal ağı için DNS sunucularını yapılandırın][sap-ha-guide-figure-3001]

    _**Şekil 12:** Yapılandır DNS sunucuları için Azure sanal ağ_

  > [!NOTE]
  > Merhaba DNS sunucularının IP adreslerini hello değiştirirseniz, toorestart hello Azure sanal makineleri tooapply gereksinim hello değişiklik ve hello yeni DNS sunucularını yayar.
  >
  >

Bizim örneğimizde, hello DNS hizmeti yüklenir ve bu Windows sanal makinelerde yapılandırılır:

| Sanal makine rolü | Sanal makine ana bilgisayar adı | Ağ kartı adı | Statik IP adresi |
| --- | --- | --- | --- |
| İlk DNS sunucusu |domcontr-0 |pr1-NIC-domcontr-0 |10.0.0.10 |
| İkinci DNS sunucusu |domcontr-1 |pr1-NIC-domcontr-1 |10.0.0.11 |

### <a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a>Ana bilgisayar adları ve hello SAP ASCS/SCS kümelenmiş örneği ve DBMS kümelenmiş örneği için statik IP adresleri

Şirket içi dağıtım için bu ayrılmış ana bilgisayar adlarını ve IP adreslerini gerekir:

| Sanal ana bilgisayar adı rolü | Sanal ana bilgisayar adı | Sanal statik IP adresi |
| --- | --- | --- |
| SAP ASCS/SCS ilk küme sanal ana bilgisayar adı (küme yönetimi) |pr1 ascs VIR |10.0.0.42 |
| SAP ASCS/SCS örnek sanal ana bilgisayar adı |pr1 ascs sap |10.0.0.43 |
| SAP DBMS ikinci küme sanal ana bilgisayar adı (küme yönetimi) |pr1 dbms VIR |10.0.0.32 |

Merhaba kümesi oluşturduğunuzda, sanal ana bilgisayar adlarını hello oluşturma **pr1 ascs VIR** ve **pr1 dbms VIR** ve hello ilişkili hello kümenin kendisi yönetmek IP adresleri. Hakkında bilgi için toodo buna ek olarak, bkz: [toplamak küme düğümleri bir küme yapılandırmasında][sap-ha-guide-8.12.1].

Diğer iki sanal ana bilgisayar adlarını hello el ile oluşturabilirsiniz **pr1 ascs sap** ve **pr1 dbms sap**, hello ilişkili hello DNS sunucusu, IP adresleri ve. Merhaba kümelenmiş SAP ASCS/SCS örneği ve kümelenmiş hello DBMS örneği bu kaynakları kullanın. Hakkında bilgi için toodo buna ek olarak, bkz: [kümelenmiş bir SAP ASCS/SCS örneği için bir sanal ana bilgisayar adı oluşturmak][sap-ha-guide-9.1.1].

### <a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a>Statik IP adresleri hello SAP sanal makineler için ayarlama
Kümenizdeki hello sanal makineleri toouse dağıttıktan sonra tüm sanal makineler için tooset statik IP adresleri gerekir. Bunu hello Azure sanal ağ yapılandırması ve hello konuk işletim sistemi içinde değil.

1.  Hello Azure portal, seçin **kaynak grubu** > **ağ kartı** > **ayarları** > **IP adresi** .
2.  Merhaba üzerinde **IP adreslerini** dikey altında **atama**seçin **statik**. Merhaba, **IP adresi** kutusuna, toouse istediğiniz hello IP adresini girin.

  > [!NOTE]
  > Merhaba ağ kartı hello IP adresini değiştirirseniz, toorestart hello Azure sanal makineleri tooapply gereksinim hello değiştirin.  
  >
  >

  ![Şekil 13: hello ağ kartı her bir sanal makine için statik IP adresi ayarlayın][sap-ha-guide-figure-3002]

  _**Şekil 13:** ayarlamak hello ağ kartı her bir sanal makine için statik IP adresleri_

  Bu, tüm ağ arabirimleri için diğer bir deyişle, Active Directory DNS hizmetiniz için toouse istediğiniz sanal makineleri de dahil olmak üzere tüm sanal makineler için tekrarlayın.

Bizim örneğimizde, bu sanal makineleri ve statik IP adresleri vardır:

| Sanal makine rolü | Sanal makine ana bilgisayar adı | Ağ kartı adı | Statik IP adresi |
| --- | --- | --- | --- |
| İlk SAP uygulama sunucusu örneği |pr1 dı 0 |pr1-NIC-dı-0 |10.0.0.50 |
| İkinci SAP uygulama sunucusu örneği |pr1 dı 1 |pr1-NIC-dı-1 |10.0.0.51 |
| ... |... |... |... |
| Son SAP uygulama sunucusu örneği |pr1 dı 5 |pr1-NIC-dı-5 |10.0.0.55 |
| İlk küme düğümüne ASCS/SCS örneği için |pr1 ascs 0 |pr1-NIC-ascs-0 |10.0.0.40 |
| İkinci küme düğümü ASCS/SCS örneği için |pr1 ascs 1 |pr1-NIC-ascs-1 |10.0.0.41 |
| İlk küme düğümüne DBMS örneği için |pr1-db-0 |pr1-NIC-db-0 |10.0.0.30 |
| DBMS örneği için ikinci küme düğümü |pr1-db-1 |pr1-NIC-db-1 |10.0.0.31 |

### <a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a>Hello Azure iç yük dengeleyici için statik bir IP adresi ayarlayın

Merhaba SAP Azure Resource Manager şablonu hello SAP ASCS/SCS örnek küme ve hello DBMS küme için kullanılan bir Azure iç yük dengeleyici oluşturur.

> [!IMPORTANT]
> Merhaba SAP ASCS/SCS olan hello hello sanal ana bilgisayar adı, IP adresi hello aynı başlangıç IP adresi hello SAP ASCS/SCS iç yük dengeleyici olarak: **pr1 lb ascs**.
> Merhaba hello sanal DBMS olduğu hello adını IP adresini hello aynı başlangıç IP adresi hello DBMS iç yük dengeleyici olarak: **pr1 lb dbms**.
>
>

Yük Dengeleyici tooset hello Azure iç için statik bir IP adresi:

1.  Merhaba ilk dağıtım hello iç yük dengeleyici IP adresi çok ayarlar**dinamik**. Merhaba hello üzerinde Azure portal'ın **IP adreslerini** dikey altında **atama**seçin **statik**.
2.  Başlangıç IP adresi hello iç yük dengeleyicisi ayarlayın **pr1 lb ascs** toohello IP adresini hello SAP ASCS/SCS örneğinin hello sanal ana bilgisayar adı.
3.  Başlangıç IP adresi hello iç yük dengeleyicisi ayarlayın **pr1 lb dbms** toohello IP adresini hello DBMS örneğinin hello sanal ana bilgisayar adı.

  ![Şekil 14: hello SAP ASCS/SCS örneği için hello iç yük dengeleyici için statik IP adresleri ayarlayın.][sap-ha-guide-figure-3003]

  _**Şekil 14:** hello SAP ASCS/SCS örneği için hello iç yük dengeleyici için statik IP adresleri ayarlayın_

Bizim örneğimizde, biz bu statik IP adresine sahip iki Azure iç yük dengeleyicileri vardır:

| Azure iç yük dengeleyici rol | Azure iç yük dengeleyicisi adı | Statik IP adresi |
| --- | --- | --- |
| SAP ASCS/SCS iç yük dengeleyici örneği |pr1 lb ascs |10.0.0.43 |
| SAP DBMS iç yük dengeleyici |pr1 lb dbms |10.0.0.33 |


### <a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a>Varsayılan ASCS/SCS Yük Dengeleme kuralları hello Azure iç yük dengeleyici için

Merhaba SAP Azure Resource Manager şablonu ihtiyacınız hello bağlantı noktalarını oluşturur:
* Bir ABAP ASCS örneğiyle hello varsayılan örnek numarasını **00**
* Bir Java SCS örneğiyle hello varsayılan örnek numarasını **01**

SAP ASCS/SCS örneğinizi yüklediğinizde hello varsayılan örnek numarasını kullanmalıdır **00** ABAP ASCS örneği ve hello varsayılan örneği numaranızı için **01** Java SCS Örneğiniz için.

Ardından, gerekli iç Yük Dengeleme hello SAP NetWeaver bağlantı noktaları için uç noktaları oluşturun.

İç Yük Dengeleme uç noktaları, ilk olarak, bu Yük Dengeleme hello SAP NetWeaver ABAP ASCS bağlantı noktaları için uç noktalar oluşturmak toocreate gerekli:

| Hizmet/Yük Dengeleme kuralı adı | Varsayılan bağlantı noktası numaraları | Somut için bağlantı noktalarını (ASCS örneği ile örnek numarasını 00) (ERS 10 ile) |
| --- | --- | --- |
| Sıraya alma sunucu / *lbrule3200* |32 <*InstanceNumber*> |3200 |
| ABAP ileti sunucusu / *lbrule3600* |36 <*InstanceNumber*> |3600 |
| İç ABAP ileti / *lbrule3900* |39 <*InstanceNumber*> |3900 |
| Sunucu HTTP iletisi / *Lbrule8100* |81 <*InstanceNumber*> |8100 |
| SAP başlangıç hizmet ASCS HTTP / *Lbrule50013* |5 <*InstanceNumber*> 13 |50013 |
| SAP başlangıç hizmet ASCS HTTPS / *Lbrule50014* |5 <*InstanceNumber*> 14 |50014 |
| Sıraya alma çoğaltma / *Lbrule50016* |5 <*InstanceNumber*> 16 |50016 |
| SAP başlangıç hizmeti ERS HTTP *Lbrule51013* |5 <*InstanceNumber*> 13 |51013 |
| SAP başlangıç hizmeti ERS HTTP *Lbrule51014* |5 <*InstanceNumber*> 14 |51014 |
| RM win *Lbrule5985* | |5985 |
| Dosya Paylaşımı *Lbrule445* | |445 |

_**Tablo 1:** bağlantı noktası numaralarını hello SAP NetWeaver ABAP ASCS örnekleri_

Ardından, bu Yük Dengeleme hello SAP NetWeaver Java SCS bağlantı noktaları için uç nokta oluşturun:

| Hizmet/Yük Dengeleme kuralı adı | Varsayılan bağlantı noktası numaraları | Somut için bağlantı noktalarını (SCS örneği ile örnek numarasını 01) (ERS 11 ile) |
| --- | --- | --- |
| Sıraya alma sunucu / *lbrule3201* |32 <*InstanceNumber*> |3201 |
| Ağ Geçidi sunucusu / *lbrule3301* |33 <*InstanceNumber*> |3301 |
| Java ileti sunucusu / *lbrule3900* |39 <*InstanceNumber*> |3901 |
| Sunucu HTTP iletisi / *Lbrule8101* |81 <*InstanceNumber*> |8101 |
| SAP başlangıç hizmet SCS HTTP / *Lbrule50113* |5 <*InstanceNumber*> 13 |50113 |
| SAP başlangıç hizmet SCS HTTPS / *Lbrule50114* |5 <*InstanceNumber*> 14 |50114 |
| Sıraya alma çoğaltma / *Lbrule50116* |5 <*InstanceNumber*> 16 |50116 |
| SAP başlangıç hizmeti ERS HTTP *Lbrule51113* |5 <*InstanceNumber*> 13 |51113 |
| SAP başlangıç hizmeti ERS HTTP *Lbrule51114* |5 <*InstanceNumber*> 14 |51114 |
| RM win *Lbrule5985* | |5985 |
| Dosya Paylaşımı *Lbrule445* | |445 |

_**Tablo 2:** bağlantı noktası numaralarını hello SAP NetWeaver Java SCS örnekleri_

![Şekil 15: varsayılan ASCS/SCS Yük Dengeleme kuralları hello Azure iç yük dengeleyici için][sap-ha-guide-figure-3004]

_**Şekil 15:** varsayılan ASCS/SCS Yük Dengeleme kuralları hello Azure iç yük dengeleyici için_

Merhaba yük dengeleyici hello IP adresi ayarlamak **pr1 lb dbms** toohello IP adresini hello DBMS örneğinin hello sanal ana bilgisayar adı.

### <a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a>Merhaba ASCS/SCS varsayılan Yük Dengeleme kuralları hello Azure iç yük dengeleyici için değiştirme

Merhaba SAP ASCS veya SCS örnekleri için toouse farklı numaraları istiyorsanız, hello adları ve değerleri kendi bağlantı noktalarının varsayılan değerleri değiştirmeniz gerekir.

1.  Hello Azure portal, seçin  **<* SID*> - lb - ascs yük dengeleyici ** > **Yük Dengeleme kuralları**.
2.  Tüm Yük Dengeleme toohello SAP ASCS veya SCS örnek ait kuralları için bu değerleri değiştirin:

  * Ad
  * Bağlantı noktası
  * Arka uç bağlantı noktası

  Örneğin, toochange hello varsayılan ASCS örneği numarasından 00 too31 istiyorsanız, Tablo 1'de listelenen tüm bağlantı noktaları toomake hello değişiklikleri gerekir.

  Bağlantı noktası için bir güncelleştirme örneği *lbrule3200*.

  ![Şekil 16: Merhaba ASCS/SCS varsayılan Yük Dengeleme kuralları hello Azure iç yük dengeleyici için değiştirme][sap-ha-guide-figure-3005]

  _**Şekil 16:** değişiklik hello ASCS/SCS varsayılan Yük Dengeleme kuralları hello Azure iç yük dengeleyici için_

### <a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a>Windows sanal makineleri toohello etki alanı ekleme

Bir statik IP adresi toohello sanal makineleri atadıktan sonra hello sanal makineleri toohello etki alanına ekleyin.

![Şekil 17: bir sanal makine tooa etki alanına ekleme][sap-ha-guide-figure-3006]

_**Şekil 17:** bir sanal makine tooa etki alanına ekleme_

### <a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a>Kayıt defteri girdilerini hello SAP ASCS/SCS örneği her iki küme düğümleri üzerinde ekleyin

Azure yük dengeleyici hello bağlantıları ayarlanmış bir süre boyunca boşta olduğunda kapanır bağlantıları (boşta zaman aşımı) zaman bir iç yük dengeleyici sahiptir. Merhaba ilk sıraya alma/dequeue gereksinimlerini toobe gönderilen istek hemen SAP iş iletişim örnekleri açık bağlantıları toohello SAP sıraya alma işlemlerinde işleyin. Bu bağlantılar genellikle hello iş işlemi kadar kurulan kalmasını veya hello sıraya alma işlemi yeniden başlatır. Ancak, belirlenen süre Hello bağlantı boşta kalırsa Azure iç yük dengeleyici kapanır hello bağlantıları hello. Artık yoksa hello SAP iş işlemi hello bağlantı toohello sıraya alma işlemini yeniden kurar çünkü bu bir sorun değildir. Bu etkinlikler SAP işlemlerin hello Geliştirici izlemeleri belgelenen, ancak bunlar büyük miktarda ek içerik bu izlemeler oluşturur. İyi bir fikir toochange hello TCP/IP'yi olan `KeepAliveTime` ve `KeepAliveInterval` her iki küme düğümlerinde. Bu değişiklikler hello TCP/IP parametreleri parametrelerle hello makalenin sonraki bölümlerinde açıklanan SAP profili ile birleştirin.

tooadd kayıt defteri girdileri hello SAP ASCS/SCS örneğinin her iki küme düğümlerinde ilk olarak, bu Windows kayıt defteri girdileri SAP ASCS/SCS için hem Windows Küme düğümlerinde ekleyin:

| Yol | HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters |
| --- | --- |
| Değişken adı |`KeepAliveTime` |
| Değişken türü |REG_DWORD (ondalık) |
| Değer |120000 |
| Bağlantı toodocumentation |[https://technet.microsoft.com/en-us/library/cc957549.aspx](https://technet.microsoft.com/en-us/library/cc957549.aspx) |

_**Tablo 3:** değişiklik hello ilk TCP/IP'yi parametresi_

Daha sonra bu Windows kayıt defteri girdileri SAP ASCS/SCS için hem Windows küme düğümlerine ekleyin:

| Yol | HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters |
| --- | --- |
| Değişken adı |`KeepAliveInterval` |
| Değişken türü |REG_DWORD (ondalık) |
| Değer |120000 |
| Bağlantı toodocumentation |[https://technet.microsoft.com/en-us/library/cc957548.aspx](https://technet.microsoft.com/en-us/library/cc957548.aspx) |

_**Tablo 4:** değişiklik hello ikinci TCP/IP'yi parametresi_

**tooapply hello değişiklikler, her iki küme düğümünü yeniden**.

### <a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a>Bir Windows Server Yük Devretme Kümelemesi küme SAP ASCS/SCS örneği için ayarlama

Bir Windows Server Yük Devretme Kümelemesi küme SAP ASCS/SCS örneği için ayarlama, bu görevleri içerir:

- Bir küme yapılandırmasında Hello küme düğümleri toplama
- Bir küme dosya paylaşımı tanığı yapılandırma

#### <a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a>Bir küme yapılandırmasında Hello küme düğümleri Topla

1.  Hello Ekle rol ve Özellik Ekleme Sihirbazı, Yük Devretme Kümelemesi tooboth küme düğümlerine ekleyin.
2.  Merhaba yük devretme kümesini yedeklerken, yük devretme kümesi Yöneticisi'ni kullanarak ayarlayın. Yük Devretme Kümesi Yöneticisi'nde seçin **küme oluşturma**ve ardından yalnızca hello ilk küme, düğümü A. hello adı ekleyin Merhaba İkinci düğüm henüz eklemeyin; bir sonraki adımda hello İkinci düğüm ekleyeceksiniz.

  ![Şekil 18: hello sunucusunu veya hello ilk küme düğümüne sanal makine adı ekleyin][sap-ha-guide-figure-3007]

  _**Şekil 18:** hello ilk küme düğümünün Ekle hello sunucu veya sanal makine adı_

3.  Merhaba ağ (sanal ana bilgisayar adı) hello kümenin adını girin.

  ![Şekil 19: hello küme adını girin][sap-ha-guide-figure-3008]

  _**Şekil 19:** hello küme adını girin_

4.  Merhaba küme oluşturduktan sonra bir küme doğrulama testi çalıştırın.

  ![Şekil 20: hello küme doğrulama denetimini Çalıştır][sap-ha-guide-figure-3009]

  _**Şekil 20:** hello küme doğrulama denetimini Çalıştır_

  Bu noktada hello işleminde disklerle ilgili tüm uyarılar yoksayabilirsiniz. Bir dosya paylaşımı tanığı ve hello SIOS diskler daha sonra paylaşılan ekleyeceksiniz. Bu aşamada, bir çekirdek sahibi olma hakkında tooworry gerek yoktur.

  ![Şekil 21: Çekirdek disk bulunamadı][sap-ha-guide-figure-3010]

  _**Şekil 21:** çekirdek disk bulunamadı_

  ![Şekil 22: Çekirdek küme kaynağının yeni bir IP adresi gerekiyor.][sap-ha-guide-figure-3011]

  _**Şekil 22:** çekirdek küme kaynağının yeni bir IP adresi gerekiyor_

5.  Merhaba çekirdek Küme hizmeti Hello IP adresini değiştirin. Başlangıç IP adresi hello çekirdek Küme hizmetinin, değiştirene kadar tooone hello sanal makine düğümlerinin hello sunucusunun hello IP adresini işaret ettiğinden hello küme başlatılamıyor. Merhaba üzerinde bunu **özellikleri** hello çekirdek küme hizmetin IP kaynak sayfası.

  Örneğin, bir IP adresi tooassign ihtiyacımız (örneğimizde **10.0.0.42**) hello küme sanal ana bilgisayar adı için **pr1 ascs VIR**.

  ![Şekil 23: hello Özellikleri iletişim kutusunda hello IP adresini değiştirme][sap-ha-guide-figure-3012]

  _**Şekil 23:** hello içinde **özellikleri** iletişim kutusu, hello IP adresini Değiştir_

  ![Şekil 24: hello küme için ayrılmış başlangıç IP adresi atayın][sap-ha-guide-figure-3013]

  _**Şekil 24:** hello küme için ayrılmış başlangıç IP adresi atayın_

6.  Merhaba küme sanal ana bilgisayar adı çevrimiçi duruma getirin.

  ![Şekil 25: Küme çekirdek hizmeti çalışır durumda ve çalıştığından ve hello ile IP adresini düzeltin][sap-ha-guide-figure-3014]

  _**Şekil 25:** çalışan ile Merhaba IP adresini düzeltin ve küme çekirdek hizmetidir ayarlama_

7.  Merhaba ikinci küme düğümünü ekleyin.

  Merhaba çekirdek Küme hizmeti çalışır durumda olduğundan, hello İkinci düğüm ekleyebilirsiniz.

  ![Şekil 26: hello İkinci düğüm ekleme][sap-ha-guide-figure-3015]

  _**Şekil 26:** Ekle hello ikinci küme düğümü_

8.  Merhaba ikinci küme düğümü konağı için bir ad girin.

  ![Şekil 27: hello ikinci küme düğümü ana bilgisayar adı girin][sap-ha-guide-figure-3016]

  _**Şekil 27:** hello ikinci küme düğümü ana bilgisayar adını girin_

  > [!IMPORTANT]
  > Bu hello denetleyin **tüm uygun depolama toohello küme eklemek** onay kutusu **değil** seçili.  
  >
  >

  ![Şekil 28: hello onay kutusunu işaretlemeyin][sap-ha-guide-figure-3017]

  _**Şekil 28:** yapmak **değil** hello onay kutusunu seçin_

  Çekirdek ve diskleri ilgili uyarılar yoksayabilirsiniz. Bölümünde açıklandığı gibi daha sonra hello çekirdek ve Paylaşım hello disk komutunu ayarlarız [SIOS DataKeeper Cluster Edition yükleme SAP ASCS/SCS küme paylaşım diski için][sap-ha-guide-8.12.3].

  ![Şekil 29: hello disk çekirdek ilgili uyarılar yoksay][sap-ha-guide-figure-3018]

  _**Şekil 29:** hello disk çekirdek ilgili uyarılar yoksay_


#### <a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a>Bir küme dosya paylaşımı tanığı Yapılandır

Bir küme dosya paylaşımı tanığı yapılandırma, bu görevleri içerir:

- Bir dosya paylaşımı oluşturma
- Yük Devretme Kümesi Yöneticisi'nde Hello dosya paylaşım tanığı çekirdek ayarlama

##### <a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a>Dosya paylaşımı oluşturma

1.  Dosya paylaşım tanığı yerine bir çekirdek diski seçin. Bu seçenek SIOS DataKeeper destekler.

  Bu makalede Hello örneklerde, Azure'da çalışan hello Active Directory DNS sunucusu hello dosya paylaşım tanığı açıktır. Merhaba dosya paylaşım tanığı olarak adlandırılır **domcontr 0**. Bir VPN bağlantısı tooAzure (aracılığıyla, siteden siteye VPN veya Azure ExpressRoute) yapılandırılmış çünkü Active Directory/Hizmeti şirket içi ve uygun toorun bir dosya değil. DNS sunucunuzun Tanık paylaşır.

  > [!NOTE]
  > Yalnızca şirket içi Active Directory DNS hizmeti çalışıyorsa, dosya paylaşım tanığı hello Active Directory/DNS Windows işletim sistemlerinde, şirket içi çalışan yapılandırmayın. Azure ve Active Directory DNS şirket içi çalışan küme düğümleri arasındaki ağ gecikmesi çok büyük ve bağlantı sorunlarına neden olabilir. Emin tooconfigure hello dosya paylaşım tanığı Kapat toohello küme düğümünde çalışan bir Azure sanal makinesi üzerinde olabilir.  
  >
  >

  Merhaba çekirdek sürücüde en az 1024 MB boş disk alanı gerekir. 2.048 MB boş disk alanı hello çekirdek sürücüsü için öneririz.

2.  Merhaba küme adı nesnesi ekleyin.

  ![Şekil 30: hello paylaşımı hello küme adı nesnesi için hello izinleri atayın][sap-ha-guide-figure-3019]

  _**Şekil 30:** hello küme adı nesnesi için hello paylaşımındaki hello izinler atama_

  Merhaba izinleri hello paylaşımı hello küme adı nesnesi için hello yetkilisi toochange veri dahil emin olun (örneğimizde **pr1 ascs VIR$**).

3.  tooadd hello küme adı nesnesi toohello listesinde **Ekle**. Merhaba filtre toocheck bilgisayar nesnelerini, toplama toothose şekil 31'de gösterilen için değiştirin.

  ![Şekil 31: Değişiklik hello nesne türleri tooinclude bilgisayarlar][sap-ha-guide-figure-3020]

  _**Şekil 31:** değiştirmek hello nesne türleri tooinclude bilgisayarlar_

  ![Şekil 32: hello bilgisayarlar onay kutusunu seçin][sap-ha-guide-figure-3021]

  _**Şekil 32:** Select hello **bilgisayarlar** onay kutusu_

4.  Şekil 31'de gösterildiği gibi hello küme adı nesnesi girin. Merhaba kaydı zaten oluşturulduğundan, Şekil 30 gösterildiği gibi hello izinleri değiştirebilirsiniz.

5.  Select hello **güvenlik** hello paylaşım ayarlayın ve ardından sekmesinde daha ayrıntılı hello küme adı nesnesi için izinleri.

  ![Şekil 33: Hello güvenlik özelliklerini ayarla hello dosya paylaşımı çekirdeğe hello küme adı nesnesi][sap-ha-guide-figure-3022]

  _**Şekil 33:** hello dosya paylaşımı çekirdek üzerinde hello küme adı nesnesi için hello güvenlik özniteliklerini ayarlama_

##### <a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a>Yük Devretme Kümesi Yöneticisi'nde Hello dosya paylaşım tanığı çekirdek ayarlayın

1.  Merhaba yapılandırma çekirdek Ayarlama Sihirbazı'nı açın.

  ![Şekil 34: hello yapılandırma küme çekirdeği ayar Sihirbazı Başlat][sap-ha-guide-figure-3023]

  _**Şekil 34:** başlangıç hello küme çekirdeği yapılandırma ayarı Sihirbazı_

2.  Merhaba üzerinde **seçin Çekirdek yapılandırmasını** sayfasında **hello çekirdek tanığı Seç**.

  ![Şekil 35: aralarından seçim yapabileceğiniz Çekirdek yapılandırmaları][sap-ha-guide-figure-3024]

  _**Şekil 35:** seçim yapabileceğiniz Çekirdek yapılandırmaları_

3.  Merhaba üzerinde **çekirdek tanığı Seç** sayfasında **bir dosya paylaşımı tanığı Yapılandır**.

  ![Şekil 36: Select hello dosya paylaşım tanığı][sap-ha-guide-figure-3025]

  _**Şekil 36:** hello dosya paylaşım tanığı seçin_

4.  Merhaba UNC yolu toohello dosya paylaşımı girin (örneğimizde \\domcontr 0\FSW). toosee hello değişiklikleri yapabilirsiniz, select listesi **sonraki**.

  ![Şekil 37: hello Tanık paylaşımı için hello dosya paylaşım konumunu tanımlayın][sap-ha-guide-figure-3026]

  _**Şekil 37:** hello Tanık paylaşımı için hello dosya paylaşım konumunu tanımlayın_

5.  Seçin ve ardından hello değişiklikleri **sonraki**. Toosuccessfully ihtiyacınız şekil 38 gösterildiği gibi hello küme yapılandırmasını yeniden yapılandırın.  

  ![Şekil 38: hello küme yeniden yapılandırılması onayı][sap-ha-guide-figure-3027]

  _**Şekil 38:** hello küme yeniden yapılandırılması onayı_

Hello Windows Yük devretme kümesi başarıyla yükledikten sonra değişiklikler toosome eşikleri tooadapt yük devretme algılama tooconditions Azure'da yapılan toobe gerekir. Merhaba değiştirilen parametreleri toobe belgelenmiştir bu blog: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/. Merhaba yapı, iki VM varsayarak Windows Küme yapılandırması ASCS/SCS içindir aynı alt ağda Merhaba, hello aşağıdaki parametreleri değiştirilen toobe toothese değerlerine ihtiyacı vardır:
- SameSubNetDelay = 2
- SameSubNetThreshold = 15

Bu ayarları müşterilerle test ve iyi güvenliğinin aşılmasına toobe yeterince esnektir hello bir tarafta sağlanan. Üzerinde Hello diğer yandan bu ayarları hızlı gerçek hata koşulları SAP yazılım veya düğüm/VM hatasında yeterli yük sağlama. 

### <a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a>Merhaba SAP ASCS/SCS küme paylaşım disk için SIOS DataKeeper küme Edition'ı yükleme

Artık Azure üzerinde çalışan bir Windows Server Yük Devretme Kümelemesi yapılandırma vardır. Ancak, tooinstall SAP ASCS/SCS örneği bir paylaşılan disk kaynağı gerekir. Azure'da hello paylaşılan disk kaynakları ihtiyacınız oluşturulamıyor. SIOS DataKeeper Cluster Edition toocreate paylaşılan disk kaynakları kullanabilir üçüncü taraf bir çözümdür.

Merhaba SAP ASCS/SCS SIOS DataKeeper Cluster Edition yüklemek küme paylaşım disk bu görevleri içerir:

- .NET Framework 3.5 Hello ekleme
- SIOS DataKeeper yükleme
- SIOS DataKeeper ayarlama

#### <a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a>.NET Framework 3.5 Hello ekleme
Merhaba Microsoft .NET Framework 3.5 otomatik olarak etkinleştirilmiş veya Windows Server 2012 R2'de yüklü değil. SIOS DataKeeper hello .NET Framework toobe DataKeeper yüklemek, tüm düğümlerde gerektirdiğinden, hello konuk işletim sisteminde hello kümedeki tüm sanal makinelerin hello .NET Framework 3.5 yüklemeniz gerekir.

İki yolu tooadd hello .NET Framework 3.5 vardır:

- Merhaba Ekle roller ve Özellikler Sihirbazı Windows şekil 39 gösterildiği gibi kullanın.

  ![Şekil 39: hello .NET Framework 3.5 hello Ekle roller ve Özellikler Sihirbazı kullanarak yükleme][sap-ha-guide-figure-3028]

  _**Şekil 39:** hello Ekle roller ve Özellikler Sihirbazı kullanarak yükleme hello .NET Framework 3.5_

  ![Şekil 40: yükleme ilerleme çubuğu hello .NET Framework 3.5 hello Ekle roller ve Özellikler Sihirbazı'nı kullanarak yüklediğinizde][sap-ha-guide-figure-3029]

  _**Şekil 40:** çubuğu hello .NET Framework 3.5 hello Ekle roller ve Özellikler Sihirbazı'nı kullanarak yüklediğinizde, yükleme ilerleme durumu_

- Merhaba komut satırı aracı dism.exe kullanın. Bu yükleme türü için tooaccess hello SxS dizin hello Windows yükleme medyası üzerinde gerekir. Yükseltilmiş bir komut istemine yazın:

  ```
  Dism /online /enable-feature /featurename:NetFx3 /All /Source:installation_media_drive:\sources\sxs /LimitAccess
  ```

#### <a name="dd41d5a2-8083-415b-9878-839652812102"></a>SIOS DataKeeper yükleyin

Merhaba kümedeki her düğümde SIOS DataKeeper Cluster Edition yükleyin. toocreate sanal paylaşılan depolama SIOS DataKeeper ile eşitlenen bir yansıtma oluşturun ve Küme Paylaşılan depolama benzetimi.

Merhaba SIOS yazılımı yüklemeden önce hello etki alanı kullanıcısı oluşturun **DataKeeperSvc**.

> [!NOTE]
> Merhaba eklemek **DataKeeperSvc** kullanıcı toohello **yerel yönetici** her iki küme düğümlerinde grup.
>
>

tooinstall SIOS DataKeeper:

1.  Merhaba SIOS yazılım her iki küme düğümlerine yükleyin.

  ![SIOS yükleyici][sap-ha-guide-figure-3030]

  ![Şekil 41: Merhaba SIOS DataKeeper Yükleme'nın ilk sayfasında][sap-ha-guide-figure-3031]

  _**Şekil 41:** hello SIOS DataKeeper Yükleme'nın ilk sayfasında_

2.  Şekil 42 gösterilen hello iletişim kutusunda seçin **Evet**.

  ![Şekil 42: Bir hizmeti devre dışı bırakılacak DataKeeper size bildirir][sap-ha-guide-figure-3032]

  _**Şekil 42:** DataKeeper bildirir, bir hizmeti devre dışı bırakılacak_

3.  Şekil 43 gösterilen hello iletişim kutusunda seçtiğiniz olan öneririz **etki alanı veya sunucu hesabı**.

  ![Şekil 43: Kullanıcı Seçimi SIOS DataKeeper için][sap-ha-guide-figure-3033]

  _**Şekil 43:** SIOS DataKeeper için kullanıcı seçimi_

4.  Merhaba etki alanı hesabı kullanıcı adı ve SIOS DataKeeper için oluşturduğunuz parola girin.

  ![Şekil 44: Merhaba SIOS DataKeeper yükleme hello etki alanı kullanıcı adı ve parola girin][sap-ha-guide-figure-3034]

  _**Şekil 44:** Merhaba SIOS DataKeeper yükleme hello etki alanı kullanıcı adı ve parola girin_

5.  Şekil 45 gösterildiği gibi SIOS DataKeeper örneğinizin Hello lisans anahtarını yükleyin.

  ![Şekil 45: SIOS DataKeeper lisans anahtarınızı girin][sap-ha-guide-figure-3035]

  _**Şekil 45:** SIOS DataKeeper lisans anahtarınızı girin_

6.  İstendiğinde, hello sanal makineyi yeniden başlatın.

#### <a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a>SIOS DataKeeper ayarlayın

Her iki düğümde SIOS DataKeeper yükledikten sonra toostart hello yapılandırması gerekir. Merhaba hello yapılandırma hello ek bağlı VHD'ler tooeach hello sanal makinelerin arasında toohave eşzamanlı veri çoğaltma hedefidir.

1.  Merhaba DataKeeper yönetim ve yapılandırma aracını başlatmak ve ardından **Connect Server**. (Şekil 46 bu seçenek kırmızı daire içine alınmıştır.)

  ![Şekil 46: SIOS DataKeeper yönetim ve yapılandırma aracı][sap-ha-guide-figure-3036]

  _**Şekil 46:** SIOS DataKeeper yönetim ve yapılandırma aracı_

2.  Merhaba adı girin veya TCP/IP adresi aracının hello ilk düğüm hello yönetimi ve yapılandırması için ve ikinci adım, hello İkinci düğüm bağlanmanız gerekir.

  ![Şekil 47: Ekle hello adı veya TCP/IP adresi aracının hello ilk düğüm hello yönetimi ve yapılandırması için ve ikinci adım, hello İkinci düğüm bağlanmanız gerekir][sap-ha-guide-figure-3037]

  _**Şekil 47:** Ekle hello adı veya TCP/IP adresi aracının hello ilk düğüm hello yönetimi ve yapılandırması bağlanmak için ve ikinci adım, hello ikinci düğümü_

3.  Merhaba iki düğüm arasında Hello çoğaltma işi oluşturun.

  ![Şekil 48: bir çoğaltma işi oluşturma][sap-ha-guide-figure-3038]

  _**Şekil 48:** çoğaltma işi oluşturma_

  Sihirbaz çoğaltma iş oluşturma hello işleminde size rehberlik eder.
4.  Merhaba adı, TCP/IP adresi ve hello kaynak düğüm disk birimi tanımlayın.

  ![Şekil 49: hello çoğaltma işi hello adını tanımlayın][sap-ha-guide-figure-3039]

  _**Şekil 49:** hello çoğaltma işi hello adını tanımlayın_

  ![Şekil 50: hello geçerli kaynak düğüm olmalıdır hello düğüm için hello temel veri tanımlama][sap-ha-guide-figure-3040]

  _**Şekil 50:** hello geçerli kaynak düğüm olmalıdır hello düğüm için hello temel veri tanımlama_

5.  Merhaba adı, TCP/IP adresi ve hello hedef düğüm disk birimi tanımlayın.

  ![Şekil 51: hello geçerli hedef düğümü olmalı hello düğüm için hello temel veri tanımlama][sap-ha-guide-figure-3041]

  _**Şekil 51:** hello geçerli hedef düğümü olmalı hello düğüm için hello temel veri tanımlama_

6.  Merhaba sıkıştırma algoritmaları tanımlayın. Bizim örneğimizde, hello çoğaltma akışını sıkıştırmak öneririz. Özellikle yeniden eşitleme durumlarda hello çoğaltma akışı hello sıkıştırmasını yeniden eşitleme zamanı önemli ölçüde azaltır. Sıkıştırma hello CPU ve RAM kaynaklarını bir sanal makinenin kullandığına dikkat edin. Merhaba sıkıştırma oranı arttıkça, bu nedenle kullanılan CPU kaynakları hacmi hello. Bu ayarı daha sonra da ayarlayabilirsiniz.

7.  Ayar başka bir gereksinim toocheck olan olup olmadığını zaman uyumsuz veya zaman uyumlu olarak hello çoğaltma gerçekleşir. *SAP ASCS/SCS yapılandırmaları koruduğunuzda, zaman uyumlu çoğaltma kullanmalısınız*.  

  ![Şekil 52: çoğaltma ayrıntılarını tanımlayın][sap-ha-guide-figure-3042]

  _**Şekil 52:** çoğaltma ayrıntılarını tanımlayın_

8.  Merhaba çoğaltma işlemiyle çoğaltılır hello birim gösterilen tooa Windows Server Yük Devretme Kümelemesi küme yapılandırması paylaşılan bir disk olarak olup olmayacağını tanımlayın. Merhaba SAP ASCS/SCS yapılandırmasını seçin **Evet** çoğaltılan birim olarak bir küme birimi olarak kullanabileceği bir paylaşılan disk küme görür hello Windows hello böylece.

  ![Şekil 53: Evet tooset çoğaltılan hello toplu küme birimi seçin.][sap-ha-guide-figure-3043]

  _**Şekil 53:** seçin **Evet** tooset hello çoğaltılan birimi bir küme birimi olarak_

  Merhaba birim oluşturulduktan sonra hello DataKeeper yönetim ve yapılandırma aracı o hello çoğaltma işi etkin olduğunu gösterir.

  ![Şekil 54: DataKeeper SAP ASCS/SCS paylaşım disk hello için zaman uyumlu yansıtma etkindir][sap-ha-guide-figure-3044]

  _**Şekil 54:** hello SAP ASCS/SCS paylaşmak disk için DataKeeper zaman uyumlu yansıtma etkin olduğu_

  Yük Devretme Kümesi Yöneticisi şimdi şekil 55 gösterildiği gibi hello disk DataKeeper disk olarak gösterir.

  ![Şekil 55: Yük devretme kümesi Yöneticisi'ni DataKeeper çoğaltılan hello disk gösterir.][sap-ha-guide-figure-3045]

  _**Şekil 55:** yük devretme kümesi Yöneticisi, çoğaltılan bu DataKeeper hello disk gösterir_

## <a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a>Merhaba SAP NetWeaver sistemini yükleyin

Kurulumları hello DBMS sistemine bağlı olarak farklılık gösterdiğinden biz hello DBMS kurulumunu açıklayan olmaz. Ancak, yüksek kullanılabilirlik sorunları hello DBMS ile Merhaba işlevler hello farklı DBMS satıcılar için Azure desteği ile giderilen varsayalım. Örneğin, her zaman açık veya Oracle veritabanları için SQL Server ve Oracle Data Guard için veritabanı yansıtma. Bu makalede kullanırız hello senaryosunda, size daha fazla koruma toohello DBMS ekleyemiyor.

Bu tür bir Azure kümelenmiş SAP ASCS/SCS yapılandırmasında farklı DBMS Hizmetleri etkileşim, özel durumlar vardır.

> [!NOTE]
> SAP NetWeaver ABAP sistemleri, Java sistemleri ve ABAP + Java sistemleri Hello yükleme yordamları neredeyse aynıdır. Merhaba en önemli fark, bir SAP ABAP sistemi bir ASCS örneği sahip olur. Merhaba SAP Java sistem bir SCS örneği vardır. bir ASCS örneği Hello SAP ABAP + Java sistem sahiptir ve çalışır durumda bir SCS örneği hello aynı Microsoft yük devretme küme grubu. Her SAP NetWeaver yükleme yığınının yükleme farkları açıkça belirtilen. Diğer tüm bölümleri olan Merhaba, aynı varsayabilirsiniz.  
>
>

### <a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a>Bir yüksek kullanılabilirlik ASCS/SCS örneğiyle SAP yükleyin

> [!IMPORTANT]
> Unutmayın, sayfa dosyası üzerinde DataKeeper tooplace yansıtılmış birimler. Yansıtılmış birimler DataKeeper desteklemez. Merhaba varsayılan olduğu hello geçici D sürücüsündeki bir Azure sanal makine, sayfa dosyası bırakabilirsiniz. Bunu zaten yoksa, Azure sanal makinenizin hello Windows sayfa dosyası toodrive D taşıyın.
>
>

Bir yüksek kullanılabilirlik ASCS/SCS örneğiyle SAP yüklemek, bu görevleri içerir:

- Kümelenmiş hello SAP ASCS/SCS örneği için bir sanal ana bilgisayar adı oluşturma
- Merhaba SAP ilk küme düğümüne yükleme
- Merhaba SAP profili hello ASCS/SCS örneğinin değiştirme
- Sonda bağlantı noktası ekleme
- Merhaba Windows Güvenlik Duvarı araştırma bağlantı noktası açma

#### <a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a>Kümelenmiş hello SAP ASCS/SCS örneği için bir sanal ana bilgisayar adı oluşturma

1.  Merhaba Windows DNS Yöneticisi'nde hello ASCS/SCS örneğinin hello sanal ana bilgisayar adı için bir DNS girişi oluşturun.

  > [!IMPORTANT]
  > Merhaba ASCS/SCS örneği olmalıdır hello toohello sanal ana bilgisayar adı atamak IP adresi hello aynı tooAzure yük dengeleyiciye atanan hello IP adresi olarak (**<*SID*> - lb - ascs **).  
  >
  >

  Merhaba hello sanal SAP ASCS/SCS ana bilgisayar adının IP adresini (**pr1 ascs sap**) olan hello aynı başlangıç IP adresi Azure yük dengeleyici olarak (**pr1 lb ascs**).

  ![Şekil 56: hello DNS girdisini hello SAP ASCS/SCS küme sanal adı ve TCP/IP adresi tanımlayın][sap-ha-guide-figure-3046]

  _**Şekil 56:** hello DNS girdisini hello SAP ASCS/SCS küme sanal adı ve TCP/IP adresi tanımlayın_

2.  toodefine hello IP adresi atanmış toohello sanal ana bilgisayar adını, select **DNS Yöneticisi'ni** > **etki alanı**.

  ![Şekil 57: Yeni sanal adı ve TCP/IP adresi SAP ASCS/SCS kümesi yapılandırması için][sap-ha-guide-figure-3047]

  _**Şekil 57:** yeni sanal adı ve TCP/IP adresi SAP ASCS/SCS küme yapılandırması_

#### <a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a>Merhaba SAP ilk küme düğümüne yükleyin

1.  Merhaba ilk küme düğümü seçeneği küme düğümünde A. yürütme Örneğin, hello üzerinde **pr1 ascs 0** ana bilgisayar.
2.  tookeep hello varsayılan bağlantı noktalarını hello Azure iç yük dengeleyici, seçin:

  * **ABAP sistem**: **ASCS** örnek numarasını **00**
  * **Java sistem**: **SCS** örnek numarasını **01**
  * **ABAP + Java sistem**: **ASCS** örnek numarasını **00** ve **SCS** örnek numarasını **01**

  toouse örnek sayılar, hello ABAP ASCS 00 dışında örneği ve 01 hello Java SCS örneği için öncelikle toochange hello Azure iç yük dengeleyici varsayılan Yük Dengeleme kuralları, açıklanan gerekir [değişiklik hello ASCS/SCS varsayılan yükleme Dengeleme hello Azure iç yük dengeleyici kuralları][sap-ha-guide-8.9].

Merhaba sonraki birkaç görevleri hello standart SAP yükleme belgelerinde açıklanan değil.

> [!NOTE]
> Merhaba SAP yükleme belgelerini nasıl tooinstall hello ilk ASCS/SCS küme düğümüne açıklar.
>
>

#### <a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a>Merhaba SAP profili hello ASCS/SCS örneğinin değiştirme

Yeni bir profil parametre tooadd gerekir. Hello profil parametre çok uzun süre boşta olduğunda kapanmasını SAP iş süreçlerini ve hello enqueue sunucu arasındaki bağlantıları engeller. Biz hello sorun senaryoda bahsedilen [hello SAP ASCS/SCS örneği her iki küme düğümleri üzerinde kayıt defteri girdisini eklemeniz][sap-ha-guide-8.11]. Bu bölümde Ayrıca iki değişiklikleri toosome temel TCP/IP bağlantı parametrelerini sunulmuştur. İkinci adımda, tooset hello enqueue sunucu toosend gereken bir `keep_alive` hello bağlantıları hello Azure iç yük dengeleyicinin boşta kalma eşiği isabet yok böylece sinyal.

toomodify hello hello ASCS/SCS örneğinin SAP profili:

1.  Bu profil parametresi toohello SAP ASCS/SCS örneği profili ekleyin:

  ```
  enque/encni/set_so_keepalive = true
  ```
  Bizim örneğimizde, hello yol şudur:

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_ASCS00_pr1-ascs-sap`

  Örneğin, toohello SAP SCS profili ve karşılık gelen yol örneği:

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_SCS01_pr1-ascs-sap`

2.  tooapply hello değişiklikleri hello SAP ASCS /SCS örneğini yeniden başlatın.

#### <a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a>Bir araştırma bağlantı noktası ekleme

Merhaba iç yük dengeleyicinin araştırma işlevselliği toomake hello tüm küme yapılandırması iş Azure yük dengeleyici ile kullanın. Hello Azure iç yük dengeleyici genellikle hello gelen iş yükü katılımcı sanal makineler arasında eşit olarak dağıtır. Ancak, tek örnek etkin olmadığından bu bazı küme yapılandırmaları çalışmaz. Merhaba diğer örnek pasif ve hello iş yükü hiçbirini kabul edemez. Hello Azure iç yük dengeleyici atar yalnızca tooan etkin örneği çalışırken bir araştırma işlevsellik yardımcı olur. Merhaba araştırma işlevsellikle hello iç yük dengeleyici hangi örnekleri etkin olduğunu ve yalnızca hello örneği hello iş yükü ile hedef algılayabilir.

tooadd sonda bağlantı noktası:

1.  Merhaba geçerli denetleyin **ProbePort** hello aşağıdaki PowerShell komutunu çalıştırarak ayarlama. Merhaba sanal makineleri biri içinde ondan hello küme yapılandırmasında yürütün.

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter
  ```

2.  Bir araştırma bağlantı noktasını tanımlayın. Merhaba varsayılan araştırma bağlantı noktası numarası **0**. Bizim örneğimizde, araştırma bağlantı noktası kullanırız **62000**.

  ![Şekil 58: hello küme yapılandırması araştırma bağlantı noktası varsayılan olarak 0 olur.][sap-ha-guide-figure-3048]

  _**Şekil 58:** hello varsayılan küme yapılandırması araştırma bağlantı noktası: 0_

  başlangıç bağlantı noktası numarası SAP Azure Resource Manager şablonları tanımlanır. PowerShell hello bağlantı noktası numarası atayabilirsiniz.

  tooset hello için yeni bir ProbePort değeri  **SAP <*SID*> PowerShell Betiği aşağıdaki hello çalıştırmak IP ** küme kaynağı. Merhaba PowerShell değişkenleri ortamınız için güncelleştirin. Merhaba betik çalıştıktan sonra istendiğinde toorestart hello SAP küme grubu tooactivate hello değişiklikleri olması.

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

  Merhaba aldıktan sonra  **SAP <*SID*> ** Küme rolünü, doğrulayın **ProbePort** toohello yeni değerini ayarlayın.

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter

  ```

  ![Şekil 59: hello yeni değeri ayarlandıktan sonra hello küme bağlantı noktası araştırma][sap-ha-guide-figure-3049]

  _**Şekil 59:** hello yeni değeri ayarlandıktan sonra hello küme bağlantı noktası araştırma_

#### <a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a>Merhaba Windows Güvenlik Duvarı araştırma bağlantı noktasını açın

Tooopen her iki küme düğümlerinde Windows Güvenlik Duvarı araştırma bağlantı gerekir. Komut dosyası tooopen bir Windows Güvenlik Duvarı araştırma bağlantı noktasını aşağıdaki hello kullanın. Merhaba PowerShell değişkenleri ortamınız için güncelleştirin.

  ```PowerShell
  $ProbePort = 62000   # ProbePort of hello Azure Internal Load Balancer

  New-NetFirewallRule -Name AzureProbePort -DisplayName "Rule for Azure Probe Port" -Direction Inbound -Action Allow -Protocol TCP -LocalPort $ProbePort
  ```

Merhaba **ProbePort** çok ayarlanır**62000**. Merhaba dosya paylaşımına erişmek artık  **\\\ascsha-clsap\sapmnt** diğer konakları, gibi kadar **ascsha dbas**.

### <a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a>Merhaba veritabanı örneğini yükleyin

tooinstall hello veritabanı örneği, hello SAP yükleme belgelerini açıklanan hello süreci izleyin.

### <a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a>Merhaba ikinci küme düğümü yükleme

tooinstall hello ikinci küme, hello SAP Yükleme Kılavuzu'na hello adımları izleyin.

### <a name="094bc895-31d4-4471-91cc-1513b64e406a"></a>Merhaba SAP ERS Windows hizmet örneği Hello başlangıç türünü değiştirme

Merhaba SAP ERS Windows hizmeti başlangıç türünü Hello çok değiştirme**otomatik (Gecikmeli Başlatma)** her iki küme düğümlerinde.

![Şekil 60: hello SAP ERS örneği toodelayed otomatik hello hizmet türünü değiştir][sap-ha-guide-figure-3050]

_**Şekil 60:** hello hizmet türünü hello SAP ERS örneği toodelayed otomatik_

### <a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a>Merhaba SAP birincil uygulama sunucusu yükleme

Merhaba birincil uygulama sunucusu (PAS) örneğini yükleyin <*SID*> - dı - 0 hello sanal makinede, belirlediğiniz toohost hello PAS. Azure veya DataKeeper özgü ayarları bir bağımlılık yoktur.

### <a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a>Merhaba SAP ek uygulama sunucusu yükleme

Bir SAP ek uygulama sunucusu (AAS) tüm hello sanal SAP uygulama sunucusu örneği toohost tasarladığınız makinelere yükleyin. Örneğin, <*SID*> - dı - 1 çok <*SID*> - di -&lt;n&gt;.

> [!NOTE]
> Yüksek kullanılabilirlik SAP NetWeaver sistem hello yüklemesini tamamlar. Ardından, yük devretme testi ile devam edin.
>


## <a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a>Test Hello SAP ASCS/SCS örneği yük devretme ve SIOS çoğaltma
Bu kolay tootest ve yük devretme kümesi Yöneticisi'ni ve hello SIOS DataKeeper yönetimi ve yapılandırması aracını kullanarak bir SAP ASCS/SCS örneği yük devretme ve SIOS disk çoğaltması izleyin.

### <a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a>SAP ASCS/SCS örneği bir küme düğümünde çalışıyor

Merhaba **SAP PR1** küme grubu A'daki küme düğümünde çalışıyor Örneğin, **pr1 ascs 0**. Merhaba parçası olan paylaşılan hello disk sürücüsü S, Ata **SAP PR1** küme grubu ve hangi hello ASCS/SCS örnek kullanan, toocluster düğümü A.

![Şekil 61: Yük devretme kümesi Yöneticisi: merhaba < SID > SAP küme grubu, bir küme düğümünde çalışıyor][sap-ha-guide-figure-5000]

_**Şekil 61:** yük devretme kümesi Yöneticisi: SAP merhaba <*SID*> Küme grubu, bir küme düğümünde çalışıyor_

Merhaba SIOS DataKeeper yönetim ve Yapılandırma Aracı'nda verileri sürücüsünden hello kaynak birim S küme düğümünde bir toohello hedef birim sürücü S B. küme düğümünde eşzamanlı olarak çoğaltılır, hello paylaşılan disk görebilirsiniz Örneğin, gelen çoğaltılır **pr1 ascs 0 [10.0.0.40]** çok**pr1 ascs 1 [10.0.0.41]**.

![Şekil 62: SIOS DataKeeper içinde hello yerel birim B toocluster düğümü küme düğümünden Çoğalt][sap-ha-guide-figure-5001]

_**Şekil 62:** SIOS DataKeeper içinde hello yerel birim B toocluster düğümü küme düğümünden Çoğalt_

### <a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a>Yük devretme işlemini düğümü toonode B

1.  Bu seçenekler tooinitiate birini hello SAP yük devretmesi seçin <*SID*> Küme grubu küme düğümü toocluster düğümünden B:
  - Yük Devretme Kümesi Yöneticisi'ni kullanın  
  - Yük devretme kümesi PowerShell kullanma

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPClusterGroup = "SAP $SAPSID"
  Move-ClusterGroup -Name $SAPClusterGroup

  ```
2.  Küme düğümü bir hello Windows konuk işletim sistemi içinde yeniden (Bu hello SAP otomatik olarak yük devretmesi başlatır <*SID*> Küme düğümü toonode B grubundan).  
3.  Küme düğümü hello Azure portal A'dan yeniden (Bu hello SAP otomatik olarak yük devretmesi başlatır <*SID*> Küme düğümü toonode B grubundan).  
4.  Azure PowerShell kullanarak küme düğümü bir yeniden başlatma (Bu hello SAP otomatik olarak yük devretmesi başlatır <*SID*> Küme düğümü toonode B grubundan).

  Yük devretme sonrasında, SAP merhaba <*SID*> Küme grubu b küme düğümünde çalışıyor Örneğin, üzerinde çalıştırıldığı **pr1 ascs 1**.

  ![Şekil 63: Yük devretme kümesi Yöneticisi'nde hello SAP < SID > Küme grubu B küme düğümünde çalışıyor][sap-ha-guide-figure-5002]

  _**Şekil 63**: yük devretme kümesi Yöneticisi'nde hello SAP <*SID*> Küme grubu B küme düğümünde çalışıyor_

  Merhaba paylaşılan disk artık takılı kümede düğüm B. SIOS DataKeeper veri sürücüsünden kaynak birim S A. küme düğümünde Küme düğümü B tootarget birimin sürücü S çoğaltma Örneğin, gelen çoğaltma **pr1 ascs 1 [10.0.0.41]** çok**pr1 ascs 0 [10.0.0.40]**.

  ![Şekil 64: Hello yerel birim SIOS DataKeeper, küme düğümü B toocluster düğümünden A çoğaltır.][sap-ha-guide-figure-5003]

  _**Şekil 64:** SIOS DataKeeper çoğaltır hello yerel birim küme düğümü B toocluster düğümünden A_
