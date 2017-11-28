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
ms.date: 05/05/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 662dd793390d7f6138b160ed86259d13391336aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machines-high-availability-for-sap-netweaver"></a><span data-ttu-id="2f526-103">SAP NetWeaver için Azure sanal makineleri yüksek kullanılabilirlik</span><span class="sxs-lookup"><span data-stu-id="2f526-103">Azure Virtual Machines high availability for SAP NetWeaver</span></span>

[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[1999351]:https://launchpad.support.sap.com/#/notes/1999351
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2243692]:https://launchpad.support.sap.com/#/notes/2243692

[sap-installation-guides]:http://service.sap.com/instguides

[azure-subscription-service-limits]:../../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md

[dbms-guide]:../../virtual-machines-windows-sap-dbms-guide.md

[deployment-guide]:deployment-guide.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:get-started.md

[ha-guide]:sap-high-availability-guide.md

[planning-guide]:planning-guide.md
[planning-guide-11]:planning-guide.md
[planning-guide-2.1]:planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803
[planning-guide-2.2]:planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10

[planning-guide-microsoft-azure-networking]:planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f

[sap-ha-guide]:sap-high-availability-guide.md
[sap-ha-guide-2]:#42b8f600-7ba3-4606-b8a5-53c4f026da08
[sap-ha-guide-4]:#8ecf3ba0-67c0-4495-9c14-feec1a2255b7
[sap-ha-guide-8]:#78092dbe-165b-454c-92f5-4972bdbef9bf
[sap-ha-guide-8.1]:#c87a8d3f-b1dc-4d2f-b23c-da4b72977489
[sap-ha-guide-8.9]:#fe0bd8b5-2b43-45e3-8295-80bee5415716
[sap-ha-guide-8.11]:#661035b2-4d0f-4d31-86f8-dc0a50d78158
[sap-ha-guide-8.12]:#0d67f090-7928-43e0-8772-5ccbf8f59aab
[sap-ha-guide-8.12.1]:#5eecb071-c703-4ccc-ba6d-fe9c6ded9d79
[sap-ha-guide-8.12.3]:#5c8e5482-841e-45e1-a89d-a05c0907c868
[sap-ha-guide-8.12.3.1]:#1c2788c3-3648-4e82-9e0d-e058e475e2a3
[sap-ha-guide-8.12.3.2]:#dd41d5a2-8083-415b-9878-839652812102
[sap-ha-guide-8.12.3.3]:#d9c1fc8e-8710-4dff-bec2-1f535db7b006
[sap-ha-guide-9]:#a06f0b49-8a7a-42bf-8b0d-c12026c5746b
[sap-ha-guide-9.1]:#31c6bd4f-51df-4057-9fdf-3fcbc619c170
[sap-ha-guide-9.1.1]:#a97ad604-9094-44fe-a364-f89cb39bf097

[sap-ha-multi-sid-guide]:sap-high-availability-multi-sid.md (SAP multi-SID high-availability configuration)


[sap-ha-guide-figure-1000]:./media/virtual-machines-shared-sap-high-availability-guide/1000-wsfc-for-sap-ascs-on-azure.png
[sap-ha-guide-figure-1001]:./media/virtual-machines-shared-sap-high-availability-guide/1001-wsfc-on-azure-ilb.png
[sap-ha-guide-figure-1002]:./media/virtual-machines-shared-sap-high-availability-guide/1002-wsfc-sios-on-azure-ilb.png
[sap-ha-guide-figure-2000]:./media/virtual-machines-shared-sap-high-availability-guide/2000-wsfc-sap-as-ha-on-azure.png
[sap-ha-guide-figure-2001]:./media/virtual-machines-shared-sap-high-availability-guide/2001-wsfc-sap-ascs-ha-on-azure.png
[sap-ha-guide-figure-2003]:./media/virtual-machines-shared-sap-high-availability-guide/2003-wsfc-sap-dbms-ha-on-azure.png
[sap-ha-guide-figure-2004]:./media/virtual-machines-shared-sap-high-availability-guide/2004-wsfc-sap-ha-e2e-archit-template1-on-azure.png
[sap-ha-guide-figure-2005]:./media/virtual-machines-shared-sap-high-availability-guide/2005-wsfc-sap-ha-e2e-arch-template2-on-azure.png

[sap-ha-guide-figure-3000]:./media/virtual-machines-shared-sap-high-availability-guide/3000-template-parameters-sap-ha-arm-on-azure.png
[sap-ha-guide-figure-3001]:./media/virtual-machines-shared-sap-high-availability-guide/3001-configuring-dns-servers-for-Azure-vnet.png
[sap-ha-guide-figure-3002]:./media/virtual-machines-shared-sap-high-availability-guide/3002-configuring-static-IP-address-for-network-card-of-each-vm.png
[sap-ha-guide-figure-3003]:./media/virtual-machines-shared-sap-high-availability-guide/3003-setup-static-ip-address-ilb-for-ascs-instance.png
[sap-ha-guide-figure-3004]:./media/virtual-machines-shared-sap-high-availability-guide/3004-default-ascs-scs-ilb-balancing-rules-for-azure-ilb.png
[sap-ha-guide-figure-3005]:./media/virtual-machines-shared-sap-high-availability-guide/3005-changing-ascs-scs-default-ilb-rules-for-azure-ilb.png
[sap-ha-guide-figure-3006]:./media/virtual-machines-shared-sap-high-availability-guide/3006-adding-vm-to-domain.png
[sap-ha-guide-figure-3007]:./media/virtual-machines-shared-sap-high-availability-guide/3007-config-wsfc-1.png
[sap-ha-guide-figure-3008]:./media/virtual-machines-shared-sap-high-availability-guide/3008-config-wsfc-2.png
[sap-ha-guide-figure-3009]:./media/virtual-machines-shared-sap-high-availability-guide/3009-config-wsfc-3.png
[sap-ha-guide-figure-3010]:./media/virtual-machines-shared-sap-high-availability-guide/3010-config-wsfc-4.png
[sap-ha-guide-figure-3011]:./media/virtual-machines-shared-sap-high-availability-guide/3011-config-wsfc-5.png
[sap-ha-guide-figure-3012]:./media/virtual-machines-shared-sap-high-availability-guide/3012-config-wsfc-6.png
[sap-ha-guide-figure-3013]:./media/virtual-machines-shared-sap-high-availability-guide/3013-config-wsfc-7.png
[sap-ha-guide-figure-3014]:./media/virtual-machines-shared-sap-high-availability-guide/3014-config-wsfc-8.png
[sap-ha-guide-figure-3015]:./media/virtual-machines-shared-sap-high-availability-guide/3015-config-wsfc-9.png
[sap-ha-guide-figure-3016]:./media/virtual-machines-shared-sap-high-availability-guide/3016-config-wsfc-10.png
[sap-ha-guide-figure-3017]:./media/virtual-machines-shared-sap-high-availability-guide/3017-config-wsfc-11.png
[sap-ha-guide-figure-3018]:./media/virtual-machines-shared-sap-high-availability-guide/3018-config-wsfc-12.png
[sap-ha-guide-figure-3019]:./media/virtual-machines-shared-sap-high-availability-guide/3019-assign-permissions-on-share-for-cluster-name-object.png
[sap-ha-guide-figure-3020]:./media/virtual-machines-shared-sap-high-availability-guide/3020-change-object-type-include-computer-objects.png
[sap-ha-guide-figure-3021]:./media/virtual-machines-shared-sap-high-availability-guide/3021-check-box-for-computer-objects.png
[sap-ha-guide-figure-3022]:./media/virtual-machines-shared-sap-high-availability-guide/3022-set-security-attributes-for-cluster-name-object-on-file-share-quorum.png
[sap-ha-guide-figure-3023]:./media/virtual-machines-shared-sap-high-availability-guide/3023-call-configure-cluster-quorum-setting-wizard.png
[sap-ha-guide-figure-3024]:./media/virtual-machines-shared-sap-high-availability-guide/3024-selection-screen-different-quorum-configurations.png
[sap-ha-guide-figure-3025]:./media/virtual-machines-shared-sap-high-availability-guide/3025-selection-screen-file-share-witness.png
[sap-ha-guide-figure-3026]:./media/virtual-machines-shared-sap-high-availability-guide/3026-define-file-share-location-for-witness-share.png
[sap-ha-guide-figure-3027]:./media/virtual-machines-shared-sap-high-availability-guide/3027-successful-reconfiguration-cluster-file-share-witness.png
[sap-ha-guide-figure-3028]:./media/virtual-machines-shared-sap-high-availability-guide/3028-install-dot-net-framework-35.png
[sap-ha-guide-figure-3029]:./media/virtual-machines-shared-sap-high-availability-guide/3029-install-dot-net-framework-35-progress.png
[sap-ha-guide-figure-3030]:./media/virtual-machines-shared-sap-high-availability-guide/3030-sios-installer.png
[sap-ha-guide-figure-3031]:./media/virtual-machines-shared-sap-high-availability-guide/3031-first-screen-sios-data-keeper-installation.png
[sap-ha-guide-figure-3032]:./media/virtual-machines-shared-sap-high-availability-guide/3032-data-keeper-informs-service-be-disabled.png
[sap-ha-guide-figure-3033]:./media/virtual-machines-shared-sap-high-availability-guide/3033-user-selection-sios-data-keeper.png
[sap-ha-guide-figure-3034]:./media/virtual-machines-shared-sap-high-availability-guide/3034-domain-user-sios-data-keeper.png
[sap-ha-guide-figure-3035]:./media/virtual-machines-shared-sap-high-availability-guide/3035-provide-sios-data-keeper-license.png
[sap-ha-guide-figure-3036]:./media/virtual-machines-shared-sap-high-availability-guide/3036-data-keeper-management-config-tool.png
[sap-ha-guide-figure-3037]:./media/virtual-machines-shared-sap-high-availability-guide/3037-tcp-ip-address-first-node-data-keeper.png
[sap-ha-guide-figure-3038]:./media/virtual-machines-shared-sap-high-availability-guide/3038-create-replication-sios-job.png
[sap-ha-guide-figure-3039]:./media/virtual-machines-shared-sap-high-availability-guide/3039-define-sios-replication-job-name.png
[sap-ha-guide-figure-3040]:./media/virtual-machines-shared-sap-high-availability-guide/3040-define-sios-source-node.png
[sap-ha-guide-figure-3041]:./media/virtual-machines-shared-sap-high-availability-guide/3041-define-sios-target-node.png
[sap-ha-guide-figure-3042]:./media/virtual-machines-shared-sap-high-availability-guide/3042-define-sios-synchronous-replication.png
[sap-ha-guide-figure-3043]:./media/virtual-machines-shared-sap-high-availability-guide/3043-enable-sios-replicated-volume-as-cluster-volume.png
[sap-ha-guide-figure-3044]:./media/virtual-machines-shared-sap-high-availability-guide/3044-data-keeper-synchronous-mirroring-for-SAP-gui.png
[sap-ha-guide-figure-3045]:./media/virtual-machines-shared-sap-high-availability-guide/3045-replicated-disk-by-data-keeper-in-wsfc.png
[sap-ha-guide-figure-3046]:./media/virtual-machines-shared-sap-high-availability-guide/3046-dns-entry-sap-ascs-virtual-name-ip.png
[sap-ha-guide-figure-3047]:./media/virtual-machines-shared-sap-high-availability-guide/3047-dns-manager.png
[sap-ha-guide-figure-3048]:./media/virtual-machines-shared-sap-high-availability-guide/3048-default-cluster-probe-port.png
[sap-ha-guide-figure-3049]:./media/virtual-machines-shared-sap-high-availability-guide/3049-cluster-probe-port-after.png
[sap-ha-guide-figure-3050]:./media/virtual-machines-shared-sap-high-availability-guide/3050-service-type-ers-delayed-automatic.png
[sap-ha-guide-figure-5000]:./media/virtual-machines-shared-sap-high-availability-guide/5000-wsfc-sap-sid-node-a.png
[sap-ha-guide-figure-5001]:./media/virtual-machines-shared-sap-high-availability-guide/5001-sios-replicating-local-volume.png
[sap-ha-guide-figure-5002]:./media/virtual-machines-shared-sap-high-availability-guide/5002-wsfc-sap-sid-node-b.png
[sap-ha-guide-figure-5003]:./media/virtual-machines-shared-sap-high-availability-guide/5003-sios-replicating-local-volume-b-to-a.png

[sap-ha-guide-figure-6003]:./media/virtual-machines-shared-sap-high-availability-guide/6003-sap-multi-sid-full-landscape.png

[sap-templates-3-tier-multisid-xscs-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs%2Fazuredeploy.json
[sap-templates-3-tier-multisid-xscs-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs-md%2Fazuredeploy.json
[sap-templates-3-tier-multisid-db-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[sap-templates-3-tier-multisid-db-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db-md%2Fazuredeploy.json
[sap-templates-3-tier-multisid-apps-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-apps%2Fazuredeploy.json
[sap-templates-3-tier-multisid-apps-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-apps-md%2Fazuredeploy.json

[virtual-machines-azure-resource-manager-architecture-benefits-arm]:../../../azure-resource-manager/resource-group-overview.md#the-benefits-of-using-resource-manager

[virtual-machines-manage-availability]:../../virtual-machines-windows-manage-availability.md



<span data-ttu-id="2f526-109">Azure sanal makinelerin işlem, depolama ve ağ kaynaklarına, en az sürede ve uzun tedarik döngüleri olmadan gereken kuruluşlar için hello çözümü şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="2f526-109">Azure Virtual Machines is hello solution for organizations that need compute, storage, and network resources, in minimal time, and without lengthy procurement cycles.</span></span> <span data-ttu-id="2f526-110">Azure sanal makineleri toodeploy Klasik uygulamaları SAP NetWeaver tabanlı ABAP, Java ve ABAP + Java yığını gibi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f526-110">You can use Azure Virtual Machines toodeploy classic applications like SAP NetWeaver-based ABAP, Java, and an ABAP+Java stack.</span></span> <span data-ttu-id="2f526-111">Güvenilirlik ve kullanılabilirlik ek şirket içi kaynaklar olmadan genişletir.</span><span class="sxs-lookup"><span data-stu-id="2f526-111">Extend reliability and availability without additional on-premises resources.</span></span> <span data-ttu-id="2f526-112">Azure sanal makineleri şirket içi bağlantılar, Azure sanal makineler, kuruluşunuzun şirket içi etki alanları, özel Bulutlar ve SAP sistem yatay tümleştirebilir şekilde destekler.</span><span class="sxs-lookup"><span data-stu-id="2f526-112">Azure Virtual Machines supports cross-premises connectivity, so you can integrate Azure Virtual Machines into your organization's on-premises domains, private clouds, and SAP system landscape.</span></span>

<span data-ttu-id="2f526-113">Bu makalede, toodeploy yüksek kullanılabilirlik SAP sistemleri Azure'da hello Azure Resource Manager dağıtım modelini kullanarak alabilecek hello adımları kapsar.</span><span class="sxs-lookup"><span data-stu-id="2f526-113">In this article, we cover hello steps that you can take toodeploy high-availability SAP systems in Azure by using hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="2f526-114">Biz bu ana görevlerinde ilerlemenizde:</span><span class="sxs-lookup"><span data-stu-id="2f526-114">We walk you through these major tasks:</span></span>

* <span data-ttu-id="2f526-115">Merhaba, doğru SAP notlar ve yükleme kılavuzları, hello listelenen Bul [kaynakları] [ sap-ha-guide-2] bölümü.</span><span class="sxs-lookup"><span data-stu-id="2f526-115">Find hello right SAP Notes and installation guides, listed in hello [Resources][sap-ha-guide-2] section.</span></span> <span data-ttu-id="2f526-116">Bu makalede SAP yükleme belgelerini tamamlar ve yardımcı olabilecek hello birincil kaynaklardır SAP notları yükleyip belirli platformlar SAP yazılımı dağıtın.</span><span class="sxs-lookup"><span data-stu-id="2f526-116">This article complements SAP installation documentation and SAP Notes, which are hello primary resources that can help you install and deploy SAP software on specific platforms.</span></span>
* <span data-ttu-id="2f526-117">Merhaba farklarını hello Azure Resource Manager dağıtım modeli ve hello Azure Klasik dağıtım modeli hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="2f526-117">Learn hello differences between hello Azure Resource Manager deployment model and hello Azure classic deployment model.</span></span>
* <span data-ttu-id="2f526-118">Azure dağıtımınız için doğru hello modeli seçebilmeniz için Windows Server Yük Devretme Kümelemesi çekirdek modları hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="2f526-118">Learn about Windows Server Failover Clustering quorum modes, so you can select hello model that is right for your Azure deployment.</span></span>
* <span data-ttu-id="2f526-119">Azure hizmetlerinde paylaşılan Windows Server Yük Devretme Kümelemesi depolama hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="2f526-119">Learn about Windows Server Failover Clustering shared storage in Azure services.</span></span>
* <span data-ttu-id="2f526-120">Korunmasına nasıl yardımcı toohelp başarısızlık durumunu tek nokta bileşenleri gibi gelişmiş iş uygulama programlama (ABAP) SAP merkezi Hizmetleri (ASCS) öğrenin / SAP merkezi Hizmetleri (SCS) ve veritabanı yönetim sistemi (DBMS) ve yedek bileşenlerin SAP gibi Azure uygulama sunucusu.</span><span class="sxs-lookup"><span data-stu-id="2f526-120">Learn how toohelp protect single-point-of-failure components like Advanced Business Application Programming (ABAP) SAP Central Services (ASCS)/SAP Central Services (SCS) and database management systems (DBMS), and redundant components like SAP Application Server, in Azure.</span></span>
* <span data-ttu-id="2f526-121">Adım adım örnek bir yükleme ve bir Windows Server Yük Devretme Kümelemesi küme azure'da yüksek kullanılabilirlik SAP sisteminde yapılandırmasının, Azure Kaynak Yöneticisi'ni kullanarak izleyin.</span><span class="sxs-lookup"><span data-stu-id="2f526-121">Follow a step-by-step example of an installation and configuration of a high-availability SAP system in a Windows Server Failover Clustering cluster in Azure by using Azure Resource Manager.</span></span>
* <span data-ttu-id="2f526-122">Ek adımlar gerekli toouse Windows Server Yük Devretme Kümelemesi azure'da, ancak, bir şirket içi dağıtımda gerekli olmayan hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="2f526-122">Learn about additional steps required toouse Windows Server Failover Clustering in Azure, but which are not needed in an on-premises deployment.</span></span>

<span data-ttu-id="2f526-123">toosimplify dağıtımı ve yapılandırması, bu makalede, kullandığımız SAP üç katmanlı yüksek kullanılabilirlik Resource Manager şablonları hello.</span><span class="sxs-lookup"><span data-stu-id="2f526-123">toosimplify deployment and configuration, in this article, we use hello SAP three-tier high-availability Resource Manager templates.</span></span> <span data-ttu-id="2f526-124">Merhaba şablonları bir yüksek kullanılabilirlik SAP sistemi için gereksinim duyduğunuz hello tüm altyapının dağıtımını otomatik hale getirme.</span><span class="sxs-lookup"><span data-stu-id="2f526-124">hello templates automate deployment of hello entire infrastructure that you need for a high-availability SAP system.</span></span> <span data-ttu-id="2f526-125">Merhaba altyapı SAP uygulama performans standart (SAP) boyutlandırma SAP sisteminizin de destekler.</span><span class="sxs-lookup"><span data-stu-id="2f526-125">hello infrastructure also supports SAP Application Performance Standard (SAPS) sizing of your SAP system.</span></span>

## <span data-ttu-id="2f526-126"><a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a>Önkoşulları</span><span class="sxs-lookup"><span data-stu-id="2f526-126"><a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a> Prerequisites</span></span>
<span data-ttu-id="2f526-127">Başlamadan önce aşağıdaki bölümlerde hello açıklanan hello önkoşulları karşıladığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="2f526-127">Before you start, make sure that you meet hello prerequisites that are described in hello following sections.</span></span> <span data-ttu-id="2f526-128">Tüm kaynaklar listelenen hello emin toocheck de [kaynakları] [ sap-ha-guide-2] bölümü.</span><span class="sxs-lookup"><span data-stu-id="2f526-128">Also, be sure toocheck all resources listed in hello [Resources][sap-ha-guide-2] section.</span></span>

<span data-ttu-id="2f526-129">Bu makalede, Azure Resource Manager şablonları için kullandığımız [üç katmanlı SAP NetWeaver yönetilen diskleri kullanarak](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md/).</span><span class="sxs-lookup"><span data-stu-id="2f526-129">In this article, we use Azure Resource Manager templates for [three-tier SAP NetWeaver using Managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md/).</span></span> <span data-ttu-id="2f526-130">Şablonları yararlı bir genel bakış için bkz: [SAP Azure Resource Manager şablonları](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/).</span><span class="sxs-lookup"><span data-stu-id="2f526-130">For a helpful overview of templates, see [SAP Azure Resource Manager templates](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/).</span></span>

## <span data-ttu-id="2f526-131"><a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a>Kaynakları</span><span class="sxs-lookup"><span data-stu-id="2f526-131"><a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a> Resources</span></span>
<span data-ttu-id="2f526-132">Bu makaleler Azure SAP dağıtımlarda kapsar:</span><span class="sxs-lookup"><span data-stu-id="2f526-132">These articles cover SAP deployments in Azure:</span></span>

* <span data-ttu-id="2f526-133">[Azure sanal makineleri planlama ve uygulama SAP NetWeaver için][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="2f526-133">[Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide]</span></span>
* <span data-ttu-id="2f526-134">[SAP NetWeaver için Azure sanal makineler dağıtımı][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="2f526-134">[Azure Virtual Machines deployment for SAP NetWeaver][deployment-guide]</span></span>
* <span data-ttu-id="2f526-135">[SAP NetWeaver için Azure sanal makineleri DBMS dağıtımı][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="2f526-135">[Azure Virtual Machines DBMS deployment for SAP NetWeaver][dbms-guide]</span></span>
* <span data-ttu-id="2f526-136">[Azure sanal makineler için yüksek oranda kullanılabilirlik SAP NetWeaver (Bu Kılavuzu)][sap-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="2f526-136">[Azure Virtual Machines high availability for SAP NetWeaver (this guide)][sap-ha-guide]</span></span>

> [!NOTE]
> <span data-ttu-id="2f526-137">Mümkün olduğunda, SAP Yükleme Kılavuzu'na başvuran bir bağlantı toohello sunuyoruz (Merhaba bkz [SAP yükleme kılavuzları][sap-installation-guides]).</span><span class="sxs-lookup"><span data-stu-id="2f526-137">Whenever possible, we give you a link toohello referring SAP installation guide (see hello [SAP installation guides][sap-installation-guides]).</span></span> <span data-ttu-id="2f526-138">Önkoşullar ve hello yükleme işlemi, onun bir fikir tooread hello SAP NetWeaver yükleme dikkatle kılavuzları hakkında bilgi için.</span><span class="sxs-lookup"><span data-stu-id="2f526-138">For prerequisites and information about hello installation process, it's a good idea tooread hello SAP NetWeaver installation guides carefully.</span></span> <span data-ttu-id="2f526-139">Bu makalede yalnızca Azure sanal makineler ile kullanabileceğiniz SAP NetWeaver tabanlı sistemler için belirli görevler yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="2f526-139">This article covers only specific tasks for SAP NetWeaver-based systems that you can use with Azure Virtual Machines.</span></span>
>
>

<span data-ttu-id="2f526-140">Bu SAP Notlar SAP Azure içinde ilgili toohello konu şunlardır:</span><span class="sxs-lookup"><span data-stu-id="2f526-140">These SAP Notes are related toohello topic of SAP in Azure:</span></span>

| <span data-ttu-id="2f526-141">Not numarası</span><span class="sxs-lookup"><span data-stu-id="2f526-141">Note number</span></span> | <span data-ttu-id="2f526-142">Başlık</span><span class="sxs-lookup"><span data-stu-id="2f526-142">Title</span></span> |
| --- | --- |
| <span data-ttu-id="2f526-143">[1928533]</span><span class="sxs-lookup"><span data-stu-id="2f526-143">[1928533]</span></span> |<span data-ttu-id="2f526-144">Azure üzerinde SAP uygulamaları: desteklenen ürünler ve boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="2f526-144">SAP Applications on Azure: Supported Products and Sizing</span></span> |
| <span data-ttu-id="2f526-145">[2015553]</span><span class="sxs-lookup"><span data-stu-id="2f526-145">[2015553]</span></span> |<span data-ttu-id="2f526-146">Microsoft Azure üzerinde SAP: Destek önkoşulları</span><span class="sxs-lookup"><span data-stu-id="2f526-146">SAP on Microsoft Azure: Support Prerequisites</span></span> |
| <span data-ttu-id="2f526-147">[1999351]</span><span class="sxs-lookup"><span data-stu-id="2f526-147">[1999351]</span></span> |<span data-ttu-id="2f526-148">Azure için SAP izleme Gelişmiş</span><span class="sxs-lookup"><span data-stu-id="2f526-148">Enhanced Azure Monitoring for SAP</span></span> |
| <span data-ttu-id="2f526-149">[2178632]</span><span class="sxs-lookup"><span data-stu-id="2f526-149">[2178632]</span></span> |<span data-ttu-id="2f526-150">Microsoft Azure üzerinde SAP için ölçümleri izleme anahtarı</span><span class="sxs-lookup"><span data-stu-id="2f526-150">Key Monitoring Metrics for SAP on Microsoft Azure</span></span> |
| <span data-ttu-id="2f526-151">[1999351]</span><span class="sxs-lookup"><span data-stu-id="2f526-151">[1999351]</span></span> |<span data-ttu-id="2f526-152">Windows sanallaştırma: İzleme Gelişmiş</span><span class="sxs-lookup"><span data-stu-id="2f526-152">Virtualization on Windows: Enhanced Monitoring</span></span> |
| <span data-ttu-id="2f526-153">[2243692]</span><span class="sxs-lookup"><span data-stu-id="2f526-153">[2243692]</span></span> |<span data-ttu-id="2f526-154">SAP DBMS örneği için Azure Premium SSD depolama kullanımı</span><span class="sxs-lookup"><span data-stu-id="2f526-154">Use of Azure Premium SSD Storage for SAP DBMS Instance</span></span> |

<span data-ttu-id="2f526-155">Merhaba hakkında daha fazla bilgi [Azure abonelikleri sınırlamaları][azure-subscription-service-limits-subscription]genel varsayılan sınırlamalar ve en fazla sınırlamalar dahil olmak üzere.</span><span class="sxs-lookup"><span data-stu-id="2f526-155">Learn more about hello [limitations of Azure subscriptions][azure-subscription-service-limits-subscription], including general default limitations and maximum limitations.</span></span>

## <span data-ttu-id="2f526-156"><a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>Yüksek kullanılabilirlik SAP hello Azure Klasik dağıtım modeli ve Azure Resource Manager ile</span><span class="sxs-lookup"><span data-stu-id="2f526-156"><a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>High-availability SAP with Azure Resource Manager vs. hello Azure classic deployment model</span></span>
<span data-ttu-id="2f526-157">Hello Azure Resource Manager ve Azure Klasik dağıtım modelleri alanları aşağıdaki hello farklı durum vardır:</span><span class="sxs-lookup"><span data-stu-id="2f526-157">hello Azure Resource Manager and Azure classic deployment models are different in hello following areas:</span></span>

- <span data-ttu-id="2f526-158">Kaynak grupları</span><span class="sxs-lookup"><span data-stu-id="2f526-158">Resource groups</span></span>
- <span data-ttu-id="2f526-159">Azure iç yük dengeleyici bağımlılığını hello Azure kaynak grubu</span><span class="sxs-lookup"><span data-stu-id="2f526-159">Azure internal load balancer dependency on hello Azure resource group</span></span>
- <span data-ttu-id="2f526-160">SAP çoklu SID senaryolar için destek</span><span class="sxs-lookup"><span data-stu-id="2f526-160">Support for SAP multi-SID scenarios</span></span>

### <span data-ttu-id="2f526-161"><a name="f76af273-1993-4d83-b12d-65deeae23686"></a>Kaynak grupları</span><span class="sxs-lookup"><span data-stu-id="2f526-161"><a name="f76af273-1993-4d83-b12d-65deeae23686"></a> Resource groups</span></span>
<span data-ttu-id="2f526-162">Azure Kaynak Yöneticisi'nde, kaynak grupları toomanage tüm hello uygulama kaynakları Azure aboneliğinizde kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f526-162">In Azure Resource Manager, you can use resource groups toomanage all hello application resources in your Azure subscription.</span></span> <span data-ttu-id="2f526-163">Tüm kaynaklara sahip bir kaynak grubunda tümleşik bir yaklaşım hello aynı yaşam döngüsü.</span><span class="sxs-lookup"><span data-stu-id="2f526-163">An integrated approach, in a resource group, all resources have hello same life cycle.</span></span> <span data-ttu-id="2f526-164">Tüm kaynaklar hello aynı örneğin, oluşturulan zaman ve bunların hello silinir aynı anda.</span><span class="sxs-lookup"><span data-stu-id="2f526-164">For example, all resources are created at hello same time and they are deleted at hello same time.</span></span> <span data-ttu-id="2f526-165">[Kaynak grupları](../../../azure-resource-manager/resource-group-overview.md#resource-groups) hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="2f526-165">Learn more about [resource groups](../../../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>

### <span data-ttu-id="2f526-166"><a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a>Azure iç yük dengeleyici bağımlılığını hello Azure kaynak grubu</span><span class="sxs-lookup"><span data-stu-id="2f526-166"><a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a> Azure internal load balancer dependency on hello Azure resource group</span></span>

<span data-ttu-id="2f526-167">Hello Azure Klasik dağıtım modelinde hello Azure iç yük dengeleyici (Azure Yük Dengeleyici Hizmeti) ile Merhaba bulut hizmeti arasında bir bağımlılık yoktur.</span><span class="sxs-lookup"><span data-stu-id="2f526-167">In hello Azure classic deployment model, there is a dependency between hello Azure internal load balancer (Azure Load Balancer service) and hello cloud service.</span></span> <span data-ttu-id="2f526-168">Her iç yük dengeleyici bir bulut hizmeti gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="2f526-168">Every internal load balancer needs one cloud service.</span></span>

<span data-ttu-id="2f526-169">Azure Kaynak Yöneticisi'nde, her Azure kaynak bir Azure kaynak grubu yerleştirilen toobe gerekir ve bu da Azure yük dengeleyici için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="2f526-169">In Azure Resource Manager, every Azure resource needs toobe placed into an Azure resource group, and this is valid for Azure Load Balancer as well.</span></span> <span data-ttu-id="2f526-170">Ancak, hiçbir gerek toohave bir Azure kaynak grubu başına Azure yük dengeleyici, örneğin bir Azure kaynak grubu birden çok Azure yük Dengeleyiciler içerebilir.</span><span class="sxs-lookup"><span data-stu-id="2f526-170">However, there is no need toohave one Azure resource group per Azure load balancer, e.g. one Azure resource group can contain multiple Azure Load Balancers.</span></span> <span data-ttu-id="2f526-171">Merhaba daha basit ve daha esnek ortamıdır.</span><span class="sxs-lookup"><span data-stu-id="2f526-171">hello environment is simpler and more flexible.</span></span> 

### <a name="support-for-sap-multi-sid-scenarios"></a><span data-ttu-id="2f526-172">SAP çoklu SID senaryolar için destek</span><span class="sxs-lookup"><span data-stu-id="2f526-172">Support for SAP multi-SID scenarios</span></span>

<span data-ttu-id="2f526-173">Azure Kaynak Yöneticisi'nde, birden çok SAP sistem tanımlayıcısı (SID) ASCS/SCS örnekleri bir küme içinde yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f526-173">In Azure Resource Manager, you can install multiple SAP system identifier (SID) ASCS/SCS instances in one cluster.</span></span> <span data-ttu-id="2f526-174">Çoklu SID örnekleri her Azure iç yük dengeleyici için birden fazla IP adresine yönelik destek nedeniyle mümkündür.</span><span class="sxs-lookup"><span data-stu-id="2f526-174">Multi-SID instances are possible because of support for multiple IP addresses for each Azure internal load balancer.</span></span>

<span data-ttu-id="2f526-175">toouse Azure Klasik dağıtım modeli Merhaba, açıklanan hello yordamları izleyin [SAP NetWeaver azure'da: SIOS DataKeeper ile azure'da Windows Server Yük Devretme Kümelemesi kullanarak SAP ASCS/SCS kümeleme örneklerini](http://go.microsoft.com/fwlink/?LinkId=613056).</span><span class="sxs-lookup"><span data-stu-id="2f526-175">toouse hello Azure classic deployment model, follow hello procedures described in [SAP NetWeaver in Azure: Clustering SAP ASCS/SCS instances by using Windows Server Failover Clustering in Azure with SIOS DataKeeper](http://go.microsoft.com/fwlink/?LinkId=613056).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2f526-176">SAP yüklemeleri için hello Azure Resource Manager dağıtım modeli kullanmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="2f526-176">We strongly recommend that you use hello Azure Resource Manager deployment model for your SAP installations.</span></span> <span data-ttu-id="2f526-177">Merhaba Klasik dağıtım modelinde bulunmayan birçok avantaj sunar.</span><span class="sxs-lookup"><span data-stu-id="2f526-177">It offers many benefits that are not available in hello classic deployment model.</span></span> <span data-ttu-id="2f526-178">Azure hakkında daha fazla bilgi [dağıtım modellerini][virtual-machines-azure-resource-manager-architecture-benefits-arm].</span><span class="sxs-lookup"><span data-stu-id="2f526-178">Learn more about Azure [deployment models][virtual-machines-azure-resource-manager-architecture-benefits-arm].</span></span>   
>
>

## <span data-ttu-id="2f526-179"><a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a>Windows Server Yük Devretme Kümelemesi</span><span class="sxs-lookup"><span data-stu-id="2f526-179"><a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a> Windows Server Failover Clustering</span></span>
<span data-ttu-id="2f526-180">Windows Server Yük Devretme Kümelemesi hello yüksek kullanılabilirlik SAP ASCS/SCS yükleme ve Windows'da DBMS temelini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2f526-180">Windows Server Failover Clustering is hello foundation of a high-availability SAP ASCS/SCS installation and DBMS in Windows.</span></span>

<span data-ttu-id="2f526-181">Bir yük devretme kümesi, uygulamaların ve hizmetlerin kullanılabilirliğini tooincrease hello birlikte çalışan 1 + n bağımsız sunucular (düğümler) grubudur.</span><span class="sxs-lookup"><span data-stu-id="2f526-181">A failover cluster is a group of 1+n independent servers (nodes) that work together tooincrease hello availability of applications and services.</span></span> <span data-ttu-id="2f526-182">Bir düğüm hatası oluşursa, Windows Server Yük Devretme Kümelemesi hello sayısı bir sağlıklı korurken oluşabilecek hesaplar küme tooprovide uygulamalar ve hizmetler.</span><span class="sxs-lookup"><span data-stu-id="2f526-182">If a node failure occurs, Windows Server Failover Clustering calculates hello number of failures that can occur while maintaining a healthy cluster tooprovide applications and services.</span></span> <span data-ttu-id="2f526-183">Farklı bir çekirdek modu tooachieve Yük Devretme Kümelemesi seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f526-183">You can choose from different quorum modes tooachieve failover clustering.</span></span>

### <span data-ttu-id="2f526-184"><a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a>Çekirdek modu</span><span class="sxs-lookup"><span data-stu-id="2f526-184"><a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a> Quorum modes</span></span>
<span data-ttu-id="2f526-185">Windows Server Yük Devretme Kümelemesi kullanırken dört çekirdek modlarından seçim yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2f526-185">You can choose from four quorum modes when you use Windows Server Failover Clustering:</span></span>

* <span data-ttu-id="2f526-186">**Düğüm çoğunluğu**.</span><span class="sxs-lookup"><span data-stu-id="2f526-186">**Node Majority**.</span></span> <span data-ttu-id="2f526-187">Merhaba kümedeki her düğüme oy kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="2f526-187">Each node of hello cluster can vote.</span></span> <span data-ttu-id="2f526-188">Küme işlevleriyle yalnızca Çoğunluk oyu, diğer bir deyişle, yarısından fazlası hello oyları ile Merhaba.</span><span class="sxs-lookup"><span data-stu-id="2f526-188">hello cluster functions only with a majority of votes, that is, with more than half hello votes.</span></span> <span data-ttu-id="2f526-189">Bu seçenek eşit sayıda düğüme sahip kümeler için önerilir.</span><span class="sxs-lookup"><span data-stu-id="2f526-189">We recommend this option for clusters that have an uneven number of nodes.</span></span> <span data-ttu-id="2f526-190">Örneğin, üç yedi düğümlü bir küme düğümünde başarısız olabilir ve hello küme durağan Çoğunluk erişir ve toorun devam eder.</span><span class="sxs-lookup"><span data-stu-id="2f526-190">For example, three nodes in a seven-node cluster can fail, and hello cluster stills achieves a majority and continues toorun.</span></span>  
* <span data-ttu-id="2f526-191">**Düğüm ve Disk Çoğunluğu**.</span><span class="sxs-lookup"><span data-stu-id="2f526-191">**Node and Disk Majority**.</span></span> <span data-ttu-id="2f526-192">Her düğüm ve hello küme depolama atanmış bir disk (bir disk tanığı) ne zaman kullanılabilir olduğunu ve iletişim oy kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="2f526-192">Each node and a designated disk (a disk witness) in hello cluster storage can vote when they are available and in communication.</span></span> <span data-ttu-id="2f526-193">Merhaba küme işlevleriyle yalnızca hello çoğunu oylarının, diğer bir deyişle, yarısından fazlası hello oyları ile.</span><span class="sxs-lookup"><span data-stu-id="2f526-193">hello cluster functions only with a majority of hello votes, that is, with more than half hello votes.</span></span> <span data-ttu-id="2f526-194">Bu mod, bir küme ortamında düğümlerinin çift sayıda mantıklıdır.</span><span class="sxs-lookup"><span data-stu-id="2f526-194">This mode makes sense in a cluster environment with an even number of nodes.</span></span> <span data-ttu-id="2f526-195">Yarı hello düğümler ve hello disk çevrimiçi hello küme sağlam durumda kalır.</span><span class="sxs-lookup"><span data-stu-id="2f526-195">If half hello nodes and hello disk are online, hello cluster remains in a healthy state.</span></span>
* <span data-ttu-id="2f526-196">**Düğüm ve dosya paylaşımı çoğunluğu**.</span><span class="sxs-lookup"><span data-stu-id="2f526-196">**Node and File Share Majority**.</span></span> <span data-ttu-id="2f526-197">Yönetici hello bir dosya paylaşımı (dosya paylaşım tanığı) oluşturur her düğüm artı, hello düğüm ve dosya paylaşımı kullanılabilir ve iletişimde oy kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="2f526-197">Each node plus a designated file share (a file share witness) that hello administrator creates can vote, regardless of whether hello nodes and file share are available and in communication.</span></span> <span data-ttu-id="2f526-198">Merhaba küme işlevleriyle yalnızca hello çoğunu oylarının, diğer bir deyişle, yarısından fazlası hello oyları ile.</span><span class="sxs-lookup"><span data-stu-id="2f526-198">hello cluster functions only with a majority of hello votes, that is, with more than half hello votes.</span></span> <span data-ttu-id="2f526-199">Bu mod, bir küme ortamında düğümlerinin çift sayıda mantıklıdır.</span><span class="sxs-lookup"><span data-stu-id="2f526-199">This mode makes sense in a cluster environment with an even number of nodes.</span></span> <span data-ttu-id="2f526-200">Benzer toohello düğüm ve Disk Çoğunluğu modu olan, ancak Tanık diski yerine bir Tanık dosya paylaşımı kullanır.</span><span class="sxs-lookup"><span data-stu-id="2f526-200">It's similar toohello Node and Disk Majority mode, but it uses a witness file share instead of a witness disk.</span></span> <span data-ttu-id="2f526-201">Bu mod kolay tooimplement bağlıdır, ancak hello dosyasını paylaşırsanız, kendisini yüksek oranda kullanılabilir değil, tek bir hata noktası olabilir.</span><span class="sxs-lookup"><span data-stu-id="2f526-201">This mode is easy tooimplement, but if hello file share itself is not highly available, it might become a single point of failure.</span></span>
* <span data-ttu-id="2f526-202">**Çoğunluk yok: Yalnızca Disk**.</span><span class="sxs-lookup"><span data-stu-id="2f526-202">**No Majority: Disk Only**.</span></span> <span data-ttu-id="2f526-203">bir düğüm kullanılabilir ve belirli bir disk hello küme depolama ile iletişim ise hello küme çekirdeği vardır.</span><span class="sxs-lookup"><span data-stu-id="2f526-203">hello cluster has a quorum if one node is available and in communication with a specific disk in hello cluster storage.</span></span> <span data-ttu-id="2f526-204">Ayrıca, disk ile iletişimi yalnızca hello düğümlerini hello kümeye katılabilir.</span><span class="sxs-lookup"><span data-stu-id="2f526-204">Only hello nodes that also are in communication with that disk can join hello cluster.</span></span> <span data-ttu-id="2f526-205">Bu mod kullanmamanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="2f526-205">We recommend that you do not use this mode.</span></span>
 

## <span data-ttu-id="2f526-206"><a name="fdfee875-6e66-483a-a343-14bbaee33275"></a>Şirket içi Windows Server Yük devretme</span><span class="sxs-lookup"><span data-stu-id="2f526-206"><a name="fdfee875-6e66-483a-a343-14bbaee33275"></a> Windows Server Failover Clustering on-premises</span></span>
<span data-ttu-id="2f526-207">Şekil 1 iki düğümden oluşan bir küme gösterir.</span><span class="sxs-lookup"><span data-stu-id="2f526-207">Figure 1 shows a cluster of two nodes.</span></span> <span data-ttu-id="2f526-208">Merhaba, hello düğümler arasında ağ bağlantısı başarısız olur ve her iki düğüm kalması ve çalıştıran, bir çekirdek disk veya dosya paylaşımı hangi düğümün tooprovide hello kümenin uygulamaları ve Hizmetleri devam edecek belirler.</span><span class="sxs-lookup"><span data-stu-id="2f526-208">If hello network connection between hello nodes fails and both nodes stay up and running, a quorum disk or file share determines which node will continue tooprovide hello cluster's applications and services.</span></span> <span data-ttu-id="2f526-209">erişim toohello çekirdek diski veya dosya paylaşımı hello düğüm Hizmetleri devam etmenizi sağlar hello olandır.</span><span class="sxs-lookup"><span data-stu-id="2f526-209">hello node that has access toohello quorum disk or file share is hello node that ensures that services continue.</span></span>

<span data-ttu-id="2f526-210">Bu örnek iki düğümlü bir küme kullandığından, hello düğüm ve dosya paylaşımı çoğunluğu çekirdek modu kullanın.</span><span class="sxs-lookup"><span data-stu-id="2f526-210">Because this example uses a two-node cluster, we use hello Node and File Share Majority quorum mode.</span></span> <span data-ttu-id="2f526-211">Merhaba düğüm ve Disk Çoğunluğu geçerli bir seçenek de olur.</span><span class="sxs-lookup"><span data-stu-id="2f526-211">hello Node and Disk Majority also is a valid option.</span></span> <span data-ttu-id="2f526-212">Bir üretim ortamında, bir çekirdek disk kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="2f526-212">In a production environment, we recommend that you use a quorum disk.</span></span> <span data-ttu-id="2f526-213">Ağ ve depolama sistemi teknolojisi toomake kullanabilirsiniz, yüksek oranda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="2f526-213">You can use network and storage system technology toomake it highly available.</span></span>

![Şekil 1: Bir Windows Server Yük Devretme Kümelemesi yapılandırma için SAP ASCS/SCS Azure örneği][sap-ha-guide-figure-1000]

<span data-ttu-id="2f526-215">_**Şekil 1:** bir Windows Server Yük Devretme Kümelemesi yapılandırma için SAP ASCS/SCS Azure örneği_</span><span class="sxs-lookup"><span data-stu-id="2f526-215">_**Figure 1:** Example of a Windows Server Failover Clustering configuration for SAP ASCS/SCS in Azure_</span></span>

### <span data-ttu-id="2f526-216"><a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a>Paylaşılan depolama alanı</span><span class="sxs-lookup"><span data-stu-id="2f526-216"><a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a> Shared storage</span></span>
<span data-ttu-id="2f526-217">Şekil 1 iki düğümlü paylaşılan depolama kümesi ayrıca gösterir.</span><span class="sxs-lookup"><span data-stu-id="2f526-217">Figure 1 also shows a two-node shared storage cluster.</span></span> <span data-ttu-id="2f526-218">Bir şirket içi paylaşılan depolama Küme Paylaşılan depolama hello kümedeki tüm düğümlerin algıla.</span><span class="sxs-lookup"><span data-stu-id="2f526-218">In an on-premises shared storage cluster, all nodes in hello cluster detect shared storage.</span></span> <span data-ttu-id="2f526-219">Kilitleme mekanizması hello veri bozulmaya karşı korur.</span><span class="sxs-lookup"><span data-stu-id="2f526-219">A locking mechanism protects hello data from corruption.</span></span> <span data-ttu-id="2f526-220">Tüm düğümler, başka bir düğüm başarısız olursa algılayabilir.</span><span class="sxs-lookup"><span data-stu-id="2f526-220">All nodes can detect if another node fails.</span></span> <span data-ttu-id="2f526-221">Bir düğüm başarısız olursa, hello kalan düğümü hello depolama kaynakları aittir ve hizmetlerin kullanılabilirliğini hello sağlar.</span><span class="sxs-lookup"><span data-stu-id="2f526-221">If one node fails, hello remaining node takes ownership of hello storage resources and ensures hello availability of services.</span></span>

> [!NOTE]
> <span data-ttu-id="2f526-222">SQL Server ile gibi bazı DBMS uygulamalarla yüksek kullanılabilirlik için Paylaşılan diskleri gerekmez.</span><span class="sxs-lookup"><span data-stu-id="2f526-222">You don't need shared disks for high availability with some DBMS applications, like with SQL Server.</span></span> <span data-ttu-id="2f526-223">SQL Server Always On hello yerel bir küme düğümü toohello yerel disk başka bir küme düğümünün diskten DBMS veri ve günlük dosyalarını çoğaltır.</span><span class="sxs-lookup"><span data-stu-id="2f526-223">SQL Server Always On replicates DBMS data and log files from hello local disk of one cluster node toohello local disk of another cluster node.</span></span> <span data-ttu-id="2f526-224">Bu durumda, paylaşılan bir diskin hello Windows Küme yapılandırması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="2f526-224">In that case, hello Windows cluster configuration doesn't need a shared disk.</span></span>
>
>

### <span data-ttu-id="2f526-225"><a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a>Ağ ve ad çözümlemesi</span><span class="sxs-lookup"><span data-stu-id="2f526-225"><a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a> Networking and name resolution</span></span>
<span data-ttu-id="2f526-226">İstemci bilgisayarları hello küme DNS sunucusu sağlar, hello bir sanal IP adresi ve bir sanal ana bilgisayar adı üzerinden ulaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f526-226">Client computers reach hello cluster over a virtual IP address and a virtual host name that hello DNS server provides.</span></span> <span data-ttu-id="2f526-227">Merhaba içi düğümleri ve hello DNS sunucusu birden çok IP adresi işleyebilir.</span><span class="sxs-lookup"><span data-stu-id="2f526-227">hello on-premises nodes and hello DNS server can handle multiple IP addresses.</span></span>

<span data-ttu-id="2f526-228">Tipik bir kurulumunda iki veya daha fazla ağ bağlantıları kullanın:</span><span class="sxs-lookup"><span data-stu-id="2f526-228">In a typical setup, you use two or more network connections:</span></span>

* <span data-ttu-id="2f526-229">Adanmış bağlantı toohello depolama</span><span class="sxs-lookup"><span data-stu-id="2f526-229">A dedicated connection toohello storage</span></span>
* <span data-ttu-id="2f526-230">Merhaba sinyal için bir küme iç ağ bağlantısı</span><span class="sxs-lookup"><span data-stu-id="2f526-230">A cluster-internal network connection for hello heartbeat</span></span>
* <span data-ttu-id="2f526-231">Genel bir ağ istemcileri tooconnect toohello küme kullanın</span><span class="sxs-lookup"><span data-stu-id="2f526-231">A public network that clients use tooconnect toohello cluster</span></span>

## <span data-ttu-id="2f526-232"><a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a>Azure'da Windows Server Yük devretme</span><span class="sxs-lookup"><span data-stu-id="2f526-232"><a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a> Windows Server Failover Clustering in Azure</span></span>
<span data-ttu-id="2f526-233">Toobare metal veya özel bulut dağıtımları karşılaştırıldığında Azure sanal makineleri ek adımlar tooconfigure Windows Server Yük Devretme Kümelemesi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="2f526-233">Compared toobare metal or private cloud deployments, Azure Virtual Machines requires additional steps tooconfigure Windows Server Failover Clustering.</span></span> <span data-ttu-id="2f526-234">Paylaşılan bir küme diski derlerken hello SAP ASCS/SCS örneği için birkaç IP adresleri ve sanal ana bilgisayar adları tooset gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f526-234">When you build a shared cluster disk, you need tooset several IP addresses and virtual host names for hello SAP ASCS/SCS instance.</span></span>

<span data-ttu-id="2f526-235">Bu makalede, anahtar kavramlar açıklanmaktadır ve ek adımlar gerekli toobuild bir SAP yüksek kullanılabilirlik merkezi Hizmetleri küme azure'da hello.</span><span class="sxs-lookup"><span data-stu-id="2f526-235">In this article, we discuss key concepts and hello additional steps required toobuild an SAP high-availability central services cluster in Azure.</span></span> <span data-ttu-id="2f526-236">Nasıl tooset hello üçüncü taraf aracı SIOS DataKeeper ayarlama ve nasıl tooconfigure hello Azure iç yük dengeleyici gösteriyoruz.</span><span class="sxs-lookup"><span data-stu-id="2f526-236">We show you how tooset up hello third-party tool SIOS DataKeeper, and how tooconfigure hello Azure internal load balancer.</span></span> <span data-ttu-id="2f526-237">Bu araçlar toocreate Windows Yük devretme, dosya paylaşım tanığı Azure ile kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f526-237">You can use these tools toocreate a Windows failover cluster with a file share witness in Azure.</span></span>

![Şekil 2: Windows Server Yük devretme kümeleme yapılandırmasında Azure olmayan paylaşılan bir disk][sap-ha-guide-figure-1001]

<span data-ttu-id="2f526-239">_**Şekil 2:** Windows Server Yük devretme kümeleme yapılandırmasında Azure olmayan paylaşılan bir disk_</span><span class="sxs-lookup"><span data-stu-id="2f526-239">_**Figure 2:** Windows Server Failover Clustering configuration in Azure without a shared disk_</span></span>

### <span data-ttu-id="2f526-240"><a name="1a464091-922b-48d7-9d08-7cecf757f341"></a>Paylaşılan disk Azure ile SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="2f526-240"><a name="1a464091-922b-48d7-9d08-7cecf757f341"></a> Shared disk in Azure with SIOS DataKeeper</span></span>
<span data-ttu-id="2f526-241">Yüksek kullanılabilirlik SAP ASCS/SCS örneği için paylaşılan depolama küme.</span><span class="sxs-lookup"><span data-stu-id="2f526-241">You need cluster shared storage for a high-availability SAP ASCS/SCS instance.</span></span> <span data-ttu-id="2f526-242">Eylül 2016 ' Azure paylaşılan depolama alanı, sunmaz gibi toocreate bir paylaşılan depolama kümesi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f526-242">As of September 2016, Azure doesn't offer shared storage that you can use toocreate a shared storage cluster.</span></span> <span data-ttu-id="2f526-243">Üçüncü taraf yazılım SIOS DataKeeper Cluster Edition toocreate Küme Paylaşılan depolama taklit eden bir yansıtılmış depolama kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f526-243">You can use third-party software SIOS DataKeeper Cluster Edition toocreate a mirrored storage that simulates cluster shared storage.</span></span> <span data-ttu-id="2f526-244">gerçek zamanlı zaman uyumlu veri çoğaltma Hello SIOS çözümü sağlar.</span><span class="sxs-lookup"><span data-stu-id="2f526-244">hello SIOS solution provides real-time synchronous data replication.</span></span> <span data-ttu-id="2f526-245">Bu küme için paylaşılan disk kaynağı nasıl oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f526-245">This is how you can create a shared disk resource for a cluster:</span></span>

1. <span data-ttu-id="2f526-246">Bir ek disk tooeach hello sanal makineleri (VM'ler) bir Windows küme yapılandırmasında ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2f526-246">Attach an additional disk tooeach of hello virtual machines (VMs) in a Windows cluster configuration.</span></span>
2. <span data-ttu-id="2f526-247">SIOS DataKeeper Cluster Edition her iki sanal makine düğümde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2f526-247">Run SIOS DataKeeper Cluster Edition on both virtual machine nodes.</span></span>
3. <span data-ttu-id="2f526-248">Böylece hello bağlı ek disk hello kaynak sanal makine toohello bağlı ek disk birimi hello hedef sanal makinenin birimden Merhaba içeriğine yansıtan SIOS DataKeeper Cluster Edition yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="2f526-248">Configure SIOS DataKeeper Cluster Edition so that it mirrors hello content of hello additional disk attached volume from hello source virtual machine toohello additional disk attached volume of hello target virtual machine.</span></span> <span data-ttu-id="2f526-249">SIOS DataKeeper hello kaynak ve hedef yerel birimleri soyutlar ve bunları tooWindows sunucu Yük Devretme Kümelemesi bir paylaşılan disk olarak sunar.</span><span class="sxs-lookup"><span data-stu-id="2f526-249">SIOS DataKeeper abstracts hello source and target local volumes, and then presents them tooWindows Server Failover Clustering as one shared disk.</span></span>

<span data-ttu-id="2f526-250">Hakkında daha fazla bilgi almak [SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/).</span><span class="sxs-lookup"><span data-stu-id="2f526-250">Get more information about [SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/).</span></span>

![Şekil 3: Windows Server Yük devretme kümeleme yapılandırmasında SIOS DataKeeper ile Azure][sap-ha-guide-figure-1002]

<span data-ttu-id="2f526-252">_**Şekil 3:** SIOS DataKeeper ile azure'da Windows Server Yük Devretme Kümelemesi yapılandırma_</span><span class="sxs-lookup"><span data-stu-id="2f526-252">_**Figure 3:** Windows Server Failover Clustering configuration in Azure with SIOS DataKeeper_</span></span>

> [!NOTE]
> <span data-ttu-id="2f526-253">SQL Server gibi bazı DBMS ürünleri ile yüksek kullanılabilirlik için Paylaşılan diskleri gerekmez.</span><span class="sxs-lookup"><span data-stu-id="2f526-253">You don't need shared disks for high availability with some DBMS products, like SQL Server.</span></span> <span data-ttu-id="2f526-254">SQL Server Always On hello yerel bir küme düğümü toohello yerel disk başka bir küme düğümünün diskten DBMS veri ve günlük dosyalarını çoğaltır.</span><span class="sxs-lookup"><span data-stu-id="2f526-254">SQL Server Always On replicates DBMS data and log files from hello local disk of one cluster node toohello local disk of another cluster node.</span></span> <span data-ttu-id="2f526-255">Bu durumda, paylaşılan bir diskin hello Windows Küme yapılandırması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="2f526-255">In this case, hello Windows cluster configuration doesn't need a shared disk.</span></span>
>
>

### <span data-ttu-id="2f526-256"><a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a>Azure ad çözümleme</span><span class="sxs-lookup"><span data-stu-id="2f526-256"><a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a> Name resolution in Azure</span></span>
<span data-ttu-id="2f526-257">Hello Azure bulut platformu hello seçeneği tooconfigure sanal IP adresleri, kayan IP adresleri gibi sunmuyor.</span><span class="sxs-lookup"><span data-stu-id="2f526-257">hello Azure cloud platform doesn't offer hello option tooconfigure virtual IP addresses, such as floating IP addresses.</span></span> <span data-ttu-id="2f526-258">Bir sanal IP adresi tooreach hello küme kaynağını hello bulutta bir alternatif çözüm tooset gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f526-258">You need an alternative solution tooset up a virtual IP address tooreach hello cluster resource in hello cloud.</span></span>
<span data-ttu-id="2f526-259">Azure hello Azure Yük Dengeleyici Hizmeti bir iç yük dengeleyici sahiptir.</span><span class="sxs-lookup"><span data-stu-id="2f526-259">Azure has an internal load balancer in hello Azure Load Balancer service.</span></span> <span data-ttu-id="2f526-260">Merhaba iç yük dengeleyici ile istemcileri hello küme hello küme sanal IP adresi ulaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f526-260">With hello internal load balancer, clients reach hello cluster over hello cluster virtual IP address.</span></span>
<span data-ttu-id="2f526-261">Toodeploy hello iç yük dengeleyici hello küme düğümleri içeren hello kaynak grubundaki gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f526-261">You need toodeploy hello internal load balancer in hello resource group that contains hello cluster nodes.</span></span> <span data-ttu-id="2f526-262">Ardından, kuralları ile Merhaba araştırma hello iç yük dengeleyici bağlantı noktaları iletme tüm gerekli bağlantı noktası yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="2f526-262">Then, configure all necessary port forwarding rules with hello probe ports of hello internal load balancer.</span></span>
<span data-ttu-id="2f526-263">Merhaba istemcileri hello sanal ana bilgisayar adını bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="2f526-263">hello clients can connect via hello virtual host name.</span></span> <span data-ttu-id="2f526-264">Merhaba DNS sunucusu hello küme IP adresi ve hello kümesinin etkin düğümü toohello iletme hello iç yük dengeleyici tanıtıcıları bağlantı noktası çözümler.</span><span class="sxs-lookup"><span data-stu-id="2f526-264">hello DNS server resolves hello cluster IP address, and hello internal load balancer handles port forwarding toohello active node of hello cluster.</span></span>

## <span data-ttu-id="2f526-265"><a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a>SAP NetWeaver yüksek kullanılabilirlik Azure altyapısı olarak-hizmet (Iaas)</span><span class="sxs-lookup"><span data-stu-id="2f526-265"><a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a> SAP NetWeaver high availability in Azure Infrastructure-as-a-Service (IaaS)</span></span>
<span data-ttu-id="2f526-266">tooachieve SAP yazılım bileşenleri için ihtiyacınız tooprotect hello bileşenleri aşağıdaki gibi uygulama yüksek kullanılabilirlik, SAP:</span><span class="sxs-lookup"><span data-stu-id="2f526-266">tooachieve SAP application high availability, such as for SAP software components, you need tooprotect hello following components:</span></span>

* <span data-ttu-id="2f526-267">SAP uygulama sunucusu örneği</span><span class="sxs-lookup"><span data-stu-id="2f526-267">SAP Application Server instance</span></span>
* <span data-ttu-id="2f526-268">SAP ASCS/SCS örneği</span><span class="sxs-lookup"><span data-stu-id="2f526-268">SAP ASCS/SCS instance</span></span>
* <span data-ttu-id="2f526-269">DBMS sunucu</span><span class="sxs-lookup"><span data-stu-id="2f526-269">DBMS server</span></span>

<span data-ttu-id="2f526-270">Yüksek kullanılabilirlik senaryolarını SAP bileşenlerinde koruma hakkında daha fazla bilgi için bkz: [Azure sanal makineleri planlama ve uygulama SAP NetWeaver için][planning-guide-11].</span><span class="sxs-lookup"><span data-stu-id="2f526-270">For more information about protecting SAP components in high-availability scenarios, see [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide-11].</span></span>

### <span data-ttu-id="2f526-271"><a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a>Yüksek kullanılabilirlik SAP uygulama sunucusu</span><span class="sxs-lookup"><span data-stu-id="2f526-271"><a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a> High-availability SAP Application Server</span></span>
<span data-ttu-id="2f526-272">Belirli bir yüksek kullanılabilirlik çözümü hello SAP uygulama sunucusu ile iletişim örnekleri için genellikle gerekmez.</span><span class="sxs-lookup"><span data-stu-id="2f526-272">You usually don't need a specific high-availability solution for hello SAP Application Server and dialog instances.</span></span> <span data-ttu-id="2f526-273">Artıklık tarafından yüksek kullanılabilirlik elde etmek ve iletişim birden çok başka durumlarda, Azure sanal makineleri yapılandıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="2f526-273">You achieve high availability by redundancy, and you'll configure multiple dialog instances in different instances of Azure Virtual Machines.</span></span> <span data-ttu-id="2f526-274">İki durumlarda, Azure sanal makinelerinde yüklü en az iki SAP uygulama örneğinin olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f526-274">You should have at least two SAP application instances installed in two instances of Azure Virtual Machines.</span></span>

![Şekil 4: Yüksek oranda kullanılabilirlik SAP uygulama sunucusu][sap-ha-guide-figure-2000]

<span data-ttu-id="2f526-276">_**Şekil 4:** yüksek kullanılabilirlik SAP uygulama sunucusu_</span><span class="sxs-lookup"><span data-stu-id="2f526-276">_**Figure 4:** High-availability SAP Application Server_</span></span>

<span data-ttu-id="2f526-277">Tüm sanal makinelerin konak SAP uygulama sunucusu örnekleri aynı Azure kullanılabilirlik kümesi hello yerleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f526-277">You must place all virtual machines that host SAP Application Server instances in hello same Azure availability set.</span></span> <span data-ttu-id="2f526-278">Bir Azure kullanılabilirlik kümesi sağlar:</span><span class="sxs-lookup"><span data-stu-id="2f526-278">An Azure availability set ensures that:</span></span>

* <span data-ttu-id="2f526-279">Tüm sanal makineleri hello parçası olan aynı yükseltme etki alanı.</span><span class="sxs-lookup"><span data-stu-id="2f526-279">All virtual machines are part of hello same upgrade domain.</span></span> <span data-ttu-id="2f526-280">Bir yükseltme etki alanı gibi hello sanal makineleri hello güncelleştirilmemiş emin olur planlı bakım kapalı kalma süresi sırasında aynı anda.</span><span class="sxs-lookup"><span data-stu-id="2f526-280">An upgrade domain, for example, makes sure that hello virtual machines aren't updated at hello same time during planned maintenance downtime.</span></span>
* <span data-ttu-id="2f526-281">Tüm sanal makineleri hello parçası olan aynı hata etki alanı.</span><span class="sxs-lookup"><span data-stu-id="2f526-281">All virtual machines are part of hello same fault domain.</span></span> <span data-ttu-id="2f526-282">Hata etki alanı, örneğin, böylece hiç tek hata noktası hello tüm sanal makinelerin kullanılabilirliğini etkiler dağıtılan sanal makineler olduğundan emin olur.</span><span class="sxs-lookup"><span data-stu-id="2f526-282">A fault domain, for example, makes sure that virtual machines are deployed so that no single point of failure affects hello availability of all virtual machines.</span></span>

<span data-ttu-id="2f526-283">Hakkında daha fazla çok bilgi[hello sanal makinelerin kullanılabilirliğini yönetme][virtual-machines-manage-availability].</span><span class="sxs-lookup"><span data-stu-id="2f526-283">Learn more about how too[manage hello availability of virtual machines][virtual-machines-manage-availability].</span></span>

<span data-ttu-id="2f526-284">Yalnızca yönetilmeyen disk: hello Azure depolama hesabına olası tek hata noktası olduğundan, önemli toohave olan en az iki Azure depolama hesapları, en az iki sanal makineye dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="2f526-284">Unmanaged disk only: Because hello Azure storage account is a potential single point of failure, it's important toohave at least two Azure storage accounts, in which at least two virtual machines are distributed.</span></span> <span data-ttu-id="2f526-285">İdeal bir kurulumunda hello diskler, SAP iletişim örneği çalıştıran her bir sanal makinenin farklı depolama hesabında dağıtılması.</span><span class="sxs-lookup"><span data-stu-id="2f526-285">In an ideal setup, hello disks of each virtual machine that is running an SAP dialog instance would be deployed in a different storage account.</span></span>

### <span data-ttu-id="2f526-286"><a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a>Yüksek kullanılabilirlik SAP ASCS/SCS örneği</span><span class="sxs-lookup"><span data-stu-id="2f526-286"><a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a> High-availability SAP ASCS/SCS instance</span></span>
<span data-ttu-id="2f526-287">Şekil 5, yüksek kullanılabilirlik SAP ASCS/SCS örneğinin bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="2f526-287">Figure 5 is an example of a high-availability SAP ASCS/SCS instance.</span></span>

![Şekil 5: Yüksek oranda kullanılabilirlik SAP ASCS/SCS örneği][sap-ha-guide-figure-2001]

<span data-ttu-id="2f526-289">_**Şekil 5:** yüksek kullanılabilirlik SAP ASCS/SCS örneği_</span><span class="sxs-lookup"><span data-stu-id="2f526-289">_**Figure 5:** High-availability SAP ASCS/SCS instance_</span></span>

#### <span data-ttu-id="2f526-290"><a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a>Windows Server Yük Devretme Kümelemesi Azure ile yüksek kullanılabilirlik SAP ASCS/SCS örneği</span><span class="sxs-lookup"><span data-stu-id="2f526-290"><a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a> SAP ASCS/SCS instance high availability with Windows Server Failover Clustering in Azure</span></span>
<span data-ttu-id="2f526-291">Toobare metal veya özel bulut dağıtımları karşılaştırıldığında Azure sanal makineleri ek adımlar tooconfigure Windows Server Yük Devretme Kümelemesi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="2f526-291">Compared toobare metal or private cloud deployments, Azure Virtual Machines requires additional steps tooconfigure Windows Server Failover Clustering.</span></span> <span data-ttu-id="2f526-292">Windows Yük devretme toobuild, paylaşılan bir küme diski, birden fazla IP adresi, birçok sanal ana bilgisayar adlarını ve Azure iç yük dengeleyiciye SAP ASCS/SCS örneği kümeleme için gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f526-292">toobuild a Windows failover cluster, you need a shared cluster disk, several IP addresses, several virtual host names, and an Azure internal load balancer for clustering an SAP ASCS/SCS instance.</span></span> <span data-ttu-id="2f526-293">Biz bu hello makalenin sonraki bölümlerinde daha ayrıntılı ele alınmıştır.</span><span class="sxs-lookup"><span data-stu-id="2f526-293">We discuss this in more detail later in hello article.</span></span>

![Şekil 6: Windows Server Yük Devretme Kümelemesi için SIOS DataKeeper kullanarak bir SAP ASCS/SCS yapılandırmasında Azure][sap-ha-guide-figure-1002]

<span data-ttu-id="2f526-295">_**Şekil 6:** Windows Server Yük Devretme Kümelemesi SIOS DataKeeper ile azure'da SAP ASCS/SCS yapılandırma_</span><span class="sxs-lookup"><span data-stu-id="2f526-295">_**Figure 6:** Windows Server Failover Clustering for an SAP ASCS/SCS configuration in Azure with SIOS DataKeeper_</span></span>

### <span data-ttu-id="2f526-296"><a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a>Yüksek kullanılabilirlik DBMS örneği</span><span class="sxs-lookup"><span data-stu-id="2f526-296"><a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a>High-availability DBMS instance</span></span>
<span data-ttu-id="2f526-297">Merhaba DBMS de tek bir iletişim noktası bir SAP içinde sistemidir.</span><span class="sxs-lookup"><span data-stu-id="2f526-297">hello DBMS also is a single point of contact in an SAP system.</span></span> <span data-ttu-id="2f526-298">Tooprotect gereken bir yüksek kullanılabilirlik çözümü kullanarak.</span><span class="sxs-lookup"><span data-stu-id="2f526-298">You need tooprotect it by using a high-availability solution.</span></span> <span data-ttu-id="2f526-299">Şekil 7, Azure'da bir SQL Server Always On yüksek kullanılabilirlik çözümü gösterir, Windows Server Yük Devretme Kümelemesi ile hello Azure iç yük dengeleyici.</span><span class="sxs-lookup"><span data-stu-id="2f526-299">Figure 7 shows a SQL Server Always On high-availability solution in Azure, with Windows Server Failover Clustering and hello Azure internal load balancer.</span></span> <span data-ttu-id="2f526-300">SQL Server Always On kendi DBMS çoğaltma kullanılarak DBMS veri ve günlük dosyalarını çoğaltır.</span><span class="sxs-lookup"><span data-stu-id="2f526-300">SQL Server Always On replicates DBMS data and log files by using its own DBMS replication.</span></span> <span data-ttu-id="2f526-301">Bu durumda, paylaşılan diskleri, hangi hello tüm kurulumu basitleştirir küme.</span><span class="sxs-lookup"><span data-stu-id="2f526-301">In this case, you don't need cluster shared disks, which simplifies hello entire setup.</span></span>

![Şekil 7: SQL Server Always On ile bir yüksek kullanılabilirlik SAP DBMS örneği][sap-ha-guide-figure-2003]

<span data-ttu-id="2f526-303">_**Şekil 7:** SQL Server Always On ile bir yüksek kullanılabilirlik SAP DBMS örneği_</span><span class="sxs-lookup"><span data-stu-id="2f526-303">_**Figure 7:** Example of a high-availability SAP DBMS, with SQL Server Always On_</span></span>

<span data-ttu-id="2f526-304">Hello Azure Resource Manager dağıtım modelini kullanarak Azure SQL Server Kümelemesi hakkında daha fazla bilgi için bu makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="2f526-304">For more information about clustering SQL Server in Azure by using hello Azure Resource Manager deployment model, see these articles:</span></span>

* <span data-ttu-id="2f526-305">[Always On kullanılabilirlik grubu Azure sanal makinelerinde el ile Kaynak Yöneticisi'ni kullanarak yapılandırmak] [virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]</span><span class="sxs-lookup"><span data-stu-id="2f526-305">[Configure Always On availability group in Azure Virtual Machines manually by using Resource Manager][virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]</span></span>
* <span data-ttu-id="2f526-306">[Always On kullanılabilirlik grubu için bir Azure iç yük dengeleyici Azure'da yapılandırın] [virtual-machines-windows-portal-sql-alwayson-int-listener]</span><span class="sxs-lookup"><span data-stu-id="2f526-306">[Configure an Azure internal load balancer for an Always On availability group in Azure][virtual-machines-windows-portal-sql-alwayson-int-listener]</span></span>

## <span data-ttu-id="2f526-307"><a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a>Uçtan uca yüksek kullanılabilirlik dağıtım senaryoları</span><span class="sxs-lookup"><span data-stu-id="2f526-307"><a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a> End-to-end high-availability deployment scenarios</span></span>

### <a name="deployment-scenario-using-architectural-template-1"></a><span data-ttu-id="2f526-308">Mimari şablonu 1'i kullanarak dağıtım senaryosu</span><span class="sxs-lookup"><span data-stu-id="2f526-308">Deployment scenario using Architectural Template 1</span></span>

<span data-ttu-id="2f526-309">Şekil 8 için azure'da bir SAP NetWeaver yüksek kullanılabilirlik mimari örneği gösterilmiştir **bir** SAP sistem.</span><span class="sxs-lookup"><span data-stu-id="2f526-309">Figure 8 shows an example of an SAP NetWeaver high-availability architecture in Azure for **one** SAP system.</span></span> <span data-ttu-id="2f526-310">Bu senaryo aşağıdaki gibi kurun:</span><span class="sxs-lookup"><span data-stu-id="2f526-310">This scenario is set up as follows:</span></span>

- <span data-ttu-id="2f526-311">Tek bir adanmış küme hello SAP ASCS/SCS örneği için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2f526-311">One dedicated cluster is used for hello SAP ASCS/SCS instance.</span></span>
- <span data-ttu-id="2f526-312">Tek bir adanmış küme hello DBMS örneği için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2f526-312">One dedicated cluster is used for hello DBMS instance.</span></span>
- <span data-ttu-id="2f526-313">SAP uygulama sunucusu örnekleri kendi özel VM'ler dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="2f526-313">SAP Application Server instances are deployed in their own dedicated VMs.</span></span>

![Şekil 8: yüksek oranda kullanılabilirlik mimari şablonu, 1 ile ayrılmış küme ASCS/SCS ve DBMS için SAP][sap-ha-guide-figure-2004]

<span data-ttu-id="2f526-315">_**Şekil 8:** ASCS/SCS ve DBMS ayrılmış kümelerine şablonu 1 mimari yüksek kullanılabilirlik, SAP_</span><span class="sxs-lookup"><span data-stu-id="2f526-315">_**Figure 8:** SAP high-availability Architectural Template 1, dedicated clusters for ASCS/SCS and DBMS_</span></span>

### <a name="deployment-scenario-using-architectural-template-2"></a><span data-ttu-id="2f526-316">Mimari şablon 2 kullanarak dağıtım senaryosu</span><span class="sxs-lookup"><span data-stu-id="2f526-316">Deployment scenario using Architectural Template 2</span></span>

<span data-ttu-id="2f526-317">Şekil 9 için azure'da bir SAP NetWeaver yüksek kullanılabilirlik mimari örneği gösterir **bir** SAP sistem.</span><span class="sxs-lookup"><span data-stu-id="2f526-317">Figure 9 shows an example of an SAP NetWeaver high-availability architecture in Azure for **one** SAP system.</span></span> <span data-ttu-id="2f526-318">Bu senaryo aşağıdaki gibi kurun:</span><span class="sxs-lookup"><span data-stu-id="2f526-318">This scenario is set up as follows:</span></span>

- <span data-ttu-id="2f526-319">Ayrılmış bir küme için kullanıldığından **her ikisi de** SAP ASCS/SCS örneği ve DBMS hello hello.</span><span class="sxs-lookup"><span data-stu-id="2f526-319">One dedicated cluster is used for **both** hello SAP ASCS/SCS instance and hello DBMS.</span></span>
- <span data-ttu-id="2f526-320">SAP uygulama sunucusu örnekleri kendi özel VM'ler içinde dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="2f526-320">SAP Application Server instances are deployed in own dedicated VMs.</span></span>

![Şekil 9: yüksek oranda kullanılabilirlik mimari şablon 2 ile ayrılmış bir küme ASCS/SCS için ve ayrılmış bir küme DBMS için SAP][sap-ha-guide-figure-2005]

<span data-ttu-id="2f526-322">_**Şekil 9:** SAP yüksek kullanılabilirlik mimari şablon 2 ile ayrılmış bir küme ASCS/SCS için ve DBMS için ayrılmış bir küme_</span><span class="sxs-lookup"><span data-stu-id="2f526-322">_**Figure 9:** SAP high-availability Architectural Template 2, with a dedicated cluster for ASCS/SCS and a dedicated cluster for DBMS_</span></span>

### <a name="deployment-scenario-using-architectural-template-3"></a><span data-ttu-id="2f526-323">Mimari şablonu 3 kullanan dağıtım senaryosu</span><span class="sxs-lookup"><span data-stu-id="2f526-323">Deployment scenario using Architectural Template 3</span></span>

<span data-ttu-id="2f526-324">Şekil 10 için azure'da bir SAP NetWeaver yüksek kullanılabilirlik mimari örneği gösterilir **iki** ile sistemleri, SAP &lt;SID1&gt; ve &lt;SID2&gt;.</span><span class="sxs-lookup"><span data-stu-id="2f526-324">Figure 10 shows an example of an SAP NetWeaver high-availability architecture in Azure for **two** SAP systems, with &lt;SID1&gt; and &lt;SID2&gt;.</span></span> <span data-ttu-id="2f526-325">Bu senaryo aşağıdaki gibi kurun:</span><span class="sxs-lookup"><span data-stu-id="2f526-325">This scenario is set up as follows:</span></span>

- <span data-ttu-id="2f526-326">Ayrılmış bir küme için kullanıldığından **her ikisi de** hello SAP ASCS/SCS SID1 örneği *ve* hello SAP ASCS/SCS SID2 örneği (bir küme için).</span><span class="sxs-lookup"><span data-stu-id="2f526-326">One dedicated cluster is used for **both** hello SAP ASCS/SCS SID1 instance *and* hello SAP ASCS/SCS SID2 instance (one cluster).</span></span>
- <span data-ttu-id="2f526-327">Tek bir adanmış küme DBMS SID1 için kullanılır ve başka bir ayrılmış küme DBMS SID2 için kullanılır (iki küme).</span><span class="sxs-lookup"><span data-stu-id="2f526-327">One dedicated cluster is used for DBMS SID1, and another dedicated cluster is used for DBMS SID2 (two clusters).</span></span>
- <span data-ttu-id="2f526-328">SAP uygulama sunucusu örnekleri hello SAP sistem SID1 için kendi özel VM'ler vardır.</span><span class="sxs-lookup"><span data-stu-id="2f526-328">SAP Application Server instances for hello SAP system SID1 have their own dedicated VMs.</span></span>
- <span data-ttu-id="2f526-329">SAP uygulama sunucusu örnekleri hello SAP sistem SID2 için kendi özel VM'ler vardır.</span><span class="sxs-lookup"><span data-stu-id="2f526-329">SAP Application Server instances for hello SAP system SID2 have their own dedicated VMs.</span></span>

![Şekil 10: yüksek kullanılabilirlik mimari şablonu 3, ile ayrılmış bir küme farklı ASCS/SCS örnekleri için SAP][sap-ha-guide-figure-6003]

<span data-ttu-id="2f526-331">_**Şekil 10:** SAP yüksek kullanılabilirlik mimari şablonu 3, ile ayrılmış bir küme için farklı ASCS/SCS örnekleri_</span><span class="sxs-lookup"><span data-stu-id="2f526-331">_**Figure 10:** SAP high-availability Architectural Template 3, with a dedicated cluster for different ASCS/SCS instances_</span></span>

## <span data-ttu-id="2f526-332"><a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a>Merhaba altyapıyı hazırlama</span><span class="sxs-lookup"><span data-stu-id="2f526-332"><a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a> Prepare hello infrastructure</span></span>

### <a name="prepare-hello-infrastructure-for-architectural-template-1"></a><span data-ttu-id="2f526-333">Mimari şablonu 1 için Hello altyapıyı hazırlama</span><span class="sxs-lookup"><span data-stu-id="2f526-333">Prepare hello infrastructure for Architectural Template 1</span></span>
<span data-ttu-id="2f526-334">Azure Resource Manager şablonları SAP için gerekli kaynakları dağıtımını kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="2f526-334">Azure Resource Manager templates for SAP help simplify deployment of required resources.</span></span>

<span data-ttu-id="2f526-335">Merhaba üç katmanlı şablonları Azure Kaynak Yöneticisi'nde de yüksek kullanılabilirlik senaryoları gibi mimari şablon iki küme olan 1'de destekler.</span><span class="sxs-lookup"><span data-stu-id="2f526-335">hello three-tier templates in Azure Resource Manager also support high-availability scenarios, such as in Architectural Template 1, which has two clusters.</span></span> <span data-ttu-id="2f526-336">Her küme bir SAP tek hata SAP ASCS/SCS ve DBMS noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="2f526-336">Each cluster is an SAP single point of failure for SAP ASCS/SCS and DBMS.</span></span>

<span data-ttu-id="2f526-337">İşte burada hello Örnek senaryo Biz bu makalede açıklamak için Azure Resource Manager şablonları elde edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2f526-337">Here's where you can get Azure Resource Manager templates for hello example scenario we describe in this article:</span></span>

* [<span data-ttu-id="2f526-338">Azure Market görüntüsü</span><span class="sxs-lookup"><span data-stu-id="2f526-338">Azure Marketplace image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image)  
* [<span data-ttu-id="2f526-339">Yönetilen diskleri kullanarak azure Market görüntüsü</span><span class="sxs-lookup"><span data-stu-id="2f526-339">Azure Marketplace image using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md)  
* [<span data-ttu-id="2f526-340">Özel görüntü</span><span class="sxs-lookup"><span data-stu-id="2f526-340">Custom image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image)
* [<span data-ttu-id="2f526-341">Özel görüntü yönetilen diskleri kullanma</span><span class="sxs-lookup"><span data-stu-id="2f526-341">Custom image using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-md)

<span data-ttu-id="2f526-342">tooprepare hello altyapısı mimari şablon 1:</span><span class="sxs-lookup"><span data-stu-id="2f526-342">tooprepare hello infrastructure for Architectural Template 1:</span></span>

- <span data-ttu-id="2f526-343">Merhaba hello üzerinde Azure portal'ın **parametreleri** dikey penceresinde hello **SYSTEMAVAILABILITY** kutusunda **HA**.</span><span class="sxs-lookup"><span data-stu-id="2f526-343">In hello Azure portal, on hello **Parameters** blade, in hello **SYSTEMAVAILABILITY** box, select **HA**.</span></span>

  ![Şekil 11: Ayarlamak SAP yüksek kullanılabilirlik Azure Resource Manager parametreleri][sap-ha-guide-figure-3000]

<span data-ttu-id="2f526-345">_**Şekil 11:** ayarlamak SAP yüksek kullanılabilirlik Azure Resource Manager parametreleri_</span><span class="sxs-lookup"><span data-stu-id="2f526-345">_**Figure 11:** Set SAP high-availability Azure Resource Manager parameters_</span></span>


  <span data-ttu-id="2f526-346">Merhaba şablonları oluşturun:</span><span class="sxs-lookup"><span data-stu-id="2f526-346">hello templates create:</span></span>

  * <span data-ttu-id="2f526-347">**Sanal makineler**:</span><span class="sxs-lookup"><span data-stu-id="2f526-347">**Virtual machines**:</span></span>
    * <span data-ttu-id="2f526-348">SAP uygulama sunucusu sanal makineleri: <*SAPSystemSID*> - dı - <*numarası*></span><span class="sxs-lookup"><span data-stu-id="2f526-348">SAP Application Server virtual machines: <*SAPSystemSID*>-di-<*Number*></span></span>
    * <span data-ttu-id="2f526-349">ASCS/SCS küme sanal makineler: <*SAPSystemSID*> - ascs - <*numarası*></span><span class="sxs-lookup"><span data-stu-id="2f526-349">ASCS/SCS cluster virtual machines: <*SAPSystemSID*>-ascs-<*Number*></span></span>
    * <span data-ttu-id="2f526-350">DBMS küme: <*SAPSystemSID*> - db - <*numarası*></span><span class="sxs-lookup"><span data-stu-id="2f526-350">DBMS cluster: <*SAPSystemSID*>-db-<*Number*></span></span>

  * <span data-ttu-id="2f526-351">**Ağ kartları ilişkili IP adresleriyle tüm sanal makineler için**:</span><span class="sxs-lookup"><span data-stu-id="2f526-351">**Network cards for all virtual machines, with associated IP addresses**:</span></span>
    * <span data-ttu-id="2f526-352"><*SAPSystemSID*> - NIC - dı - <*numarası*></span><span class="sxs-lookup"><span data-stu-id="2f526-352"><*SAPSystemSID*>-nic-di-<*Number*></span></span>
    * <span data-ttu-id="2f526-353"><*SAPSystemSID*> - NIC - ascs - <*numarası*></span><span class="sxs-lookup"><span data-stu-id="2f526-353"><*SAPSystemSID*>-nic-ascs-<*Number*></span></span>
    * <span data-ttu-id="2f526-354"><*SAPSystemSID*> - NIC - db - <*numarası*></span><span class="sxs-lookup"><span data-stu-id="2f526-354"><*SAPSystemSID*>-nic-db-<*Number*></span></span>

  * <span data-ttu-id="2f526-355">**Azure depolama hesapları (yalnızca yönetilmeyen diskler)**</span><span class="sxs-lookup"><span data-stu-id="2f526-355">**Azure storage accounts (unmanaged disks only)**</span></span>

  * <span data-ttu-id="2f526-356">**Kullanılabilirlik grupları** için:</span><span class="sxs-lookup"><span data-stu-id="2f526-356">**Availability groups** for:</span></span>
    * <span data-ttu-id="2f526-357">SAP uygulama sunucusu sanal makineleri: <*SAPSystemSID*> - avset - dı</span><span class="sxs-lookup"><span data-stu-id="2f526-357">SAP Application Server virtual machines: <*SAPSystemSID*>-avset-di</span></span>
    * <span data-ttu-id="2f526-358">SAP ASCS/SCS küme sanal makineler: <*SAPSystemSID*> - avset - ascs</span><span class="sxs-lookup"><span data-stu-id="2f526-358">SAP ASCS/SCS cluster virtual machines: <*SAPSystemSID*>-avset-ascs</span></span>
    * <span data-ttu-id="2f526-359">DBMS küme sanal makineler: <*SAPSystemSID*> - avset - db</span><span class="sxs-lookup"><span data-stu-id="2f526-359">DBMS cluster virtual machines: <*SAPSystemSID*>-avset-db</span></span>

  * <span data-ttu-id="2f526-360">**Azure iç yük dengeleyici**:</span><span class="sxs-lookup"><span data-stu-id="2f526-360">**Azure internal load balancer**:</span></span>
    * <span data-ttu-id="2f526-361">Merhaba ASCS/SCS örneği ve IP adresi için tüm bağlantı noktaları ile <*SAPSystemSID*> - lb - ascs</span><span class="sxs-lookup"><span data-stu-id="2f526-361">With all ports for hello ASCS/SCS instance and IP address <*SAPSystemSID*>-lb-ascs</span></span>
    * <span data-ttu-id="2f526-362">Merhaba SQL Server DBMS ve IP adresi için tüm bağlantı noktaları ile <*SAPSystemSID*> - lb - db</span><span class="sxs-lookup"><span data-stu-id="2f526-362">With all ports for hello SQL Server DBMS and IP address <*SAPSystemSID*>-lb-db</span></span>

  * <span data-ttu-id="2f526-363">**Ağ güvenlik grubu**: <*SAPSystemSID*> - nsg - ascs-0</span><span class="sxs-lookup"><span data-stu-id="2f526-363">**Network security group**: <*SAPSystemSID*>-nsg-ascs-0</span></span>  
    * <span data-ttu-id="2f526-364">Açık bir dış Uzak Masaüstü Protokolü (RDP) bağlantı noktası toohello ile <*SAPSystemSID*> - ascs - 0 sanal makine</span><span class="sxs-lookup"><span data-stu-id="2f526-364">With an open external Remote Desktop Protocol (RDP) port toohello <*SAPSystemSID*>-ascs-0 virtual machine</span></span>

> [!NOTE]
> <span data-ttu-id="2f526-365">Tüm IP adresleri hello ağ kartları ve Azure iç yük dengeleyicileri **dinamik** varsayılan olarak.</span><span class="sxs-lookup"><span data-stu-id="2f526-365">All IP addresses of hello network cards and Azure internal load balancers are **dynamic** by default.</span></span> <span data-ttu-id="2f526-366">Çok değiştirme**statik** IP adresleri.</span><span class="sxs-lookup"><span data-stu-id="2f526-366">Change them too**static** IP addresses.</span></span> <span data-ttu-id="2f526-367">Biz açıklamak nasıl toodo bu hello makalenin sonraki bölümlerinde yer.</span><span class="sxs-lookup"><span data-stu-id="2f526-367">We describe how toodo this later in hello article.</span></span>
>
>

### <span data-ttu-id="2f526-368"><a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a>Kurumsal ağ bağlantısı (şirket içi) toouse üretimde olan sanal makineleri dağıtma</span><span class="sxs-lookup"><span data-stu-id="2f526-368"><a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a> Deploy virtual machines with corporate network connectivity (cross-premises) toouse in production</span></span>
<span data-ttu-id="2f526-369">Üretim SAP sistemleri için Azure sanal makinelerle dağıtımı [kurumsal ağ bağlantısı (şirket içi)] [ planning-guide-2.2] Azure siteden siteye VPN veya Azure ExpressRoute kullanarak.</span><span class="sxs-lookup"><span data-stu-id="2f526-369">For production SAP systems, deploy Azure virtual machines with [corporate network connectivity (cross-premises)][planning-guide-2.2] by using Azure Site-to-Site VPN or Azure ExpressRoute.</span></span>

> [!NOTE]
> <span data-ttu-id="2f526-370">Azure Virtual Network örneğinizi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f526-370">You can use your Azure Virtual Network instance.</span></span> <span data-ttu-id="2f526-371">Merhaba sanal ağ ve alt ağ zaten oluşturulmuş hazırlanmış ve.</span><span class="sxs-lookup"><span data-stu-id="2f526-371">hello virtual network and subnet have already been created and prepared.</span></span>
>
>

1.  <span data-ttu-id="2f526-372">Merhaba hello üzerinde Azure portal'ın **parametreleri** dikey penceresinde hello **NEWOREXISTINGSUBNET** kutusunda **varolan**.</span><span class="sxs-lookup"><span data-stu-id="2f526-372">In hello Azure portal, on hello **Parameters** blade, in hello **NEWOREXISTINGSUBNET** box, select **existing**.</span></span>
2.  <span data-ttu-id="2f526-373">Merhaba, **SUBNETID** kutusunda, hello tam dize, hazırlanan Azure ağınızın burada planladığınız toodeploy Azure sanal makinelerinizi SubnetID ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2f526-373">In hello **SUBNETID** box, add hello full string of your prepared Azure network SubnetID where you plan toodeploy your Azure virtual machines.</span></span>
3.  <span data-ttu-id="2f526-374">tooget tüm Azure ağ alt ağların bir listesine bu PowerShell komutunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="2f526-374">tooget a list of all Azure network subnets, run this PowerShell command:</span></span>

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets
  ```

  <span data-ttu-id="2f526-375">Merhaba **kimliği** alan gösterir hello **SUBNETID**.</span><span class="sxs-lookup"><span data-stu-id="2f526-375">hello **ID** field shows hello **SUBNETID**.</span></span>
4. <span data-ttu-id="2f526-376">tooget tüm listesini **SUBNETID** değerleri, bu PowerShell komutunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="2f526-376">tooget a list of all **SUBNETID** values, run this PowerShell command:</span></span>

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets.Id
  ```

  <span data-ttu-id="2f526-377">Merhaba **SUBNETID** şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="2f526-377">hello **SUBNETID** looks like this:</span></span>

  ```
  /subscriptions/<SubscriptionId>/resourceGroups/<VPNName>/providers/Microsoft.Network/virtualNetworks/azureVnet/subnets/<SubnetName>
  ```

### <span data-ttu-id="2f526-378"><a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a>Test ve demo için yalnızca bulut SAP örnekleri dağıtma</span><span class="sxs-lookup"><span data-stu-id="2f526-378"><a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a> Deploy cloud-only SAP instances for test and demo</span></span>
<span data-ttu-id="2f526-379">Yüksek kullanılabilirlik SAP sisteminizi bir yalnızca bulut dağıtım modelinde dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f526-379">You can deploy your high-availability SAP system in a cloud-only deployment model.</span></span> <span data-ttu-id="2f526-380">Bu tür bir dağıtım öncelikle tanıtım ve test kullanım durumları için yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="2f526-380">This kind of deployment primarily is useful for demo and test use cases.</span></span> <span data-ttu-id="2f526-381">Üretim kullanım durumları için uygun değildir.</span><span class="sxs-lookup"><span data-stu-id="2f526-381">It's not suited for production use cases.</span></span>

- <span data-ttu-id="2f526-382">Merhaba hello üzerinde Azure portal'ın **parametreleri** dikey penceresinde hello **NEWOREXISTINGSUBNET** kutusunda **yeni**.</span><span class="sxs-lookup"><span data-stu-id="2f526-382">In hello Azure portal, on hello **Parameters** blade, in hello **NEWOREXISTINGSUBNET** box, select **new**.</span></span> <span data-ttu-id="2f526-383">Merhaba bırakın **SUBNETID** alanı boş.</span><span class="sxs-lookup"><span data-stu-id="2f526-383">Leave hello **SUBNETID** field empty.</span></span>

  <span data-ttu-id="2f526-384">Azure sanal ağ ve alt hello Hello SAP Azure Resource Manager şablonu otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2f526-384">hello SAP Azure Resource Manager template automatically creates hello Azure virtual network and subnet.</span></span>

> [!NOTE]
> <span data-ttu-id="2f526-385">Ayrıca toodeploy gereken Active Directory için en az bir ayrılmış sanal makine ve DNS'de hello aynı Azure sanal ağı örneği.</span><span class="sxs-lookup"><span data-stu-id="2f526-385">You also need toodeploy at least one dedicated virtual machine for Active Directory and DNS in hello same Azure Virtual Network instance.</span></span> <span data-ttu-id="2f526-386">Merhaba şablonu, bu sanal makineleri oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="2f526-386">hello template doesn't create these virtual machines.</span></span>
>
>


### <a name="prepare-hello-infrastructure-for-architectural-template-2"></a><span data-ttu-id="2f526-387">Mimari şablon 2 Hello altyapıyı hazırlama</span><span class="sxs-lookup"><span data-stu-id="2f526-387">Prepare hello infrastructure for Architectural Template 2</span></span>

<span data-ttu-id="2f526-388">SAP toohelp basitleştirmek için gerekli altyapı kaynaklarıdır dağıtım SAP mimari şablon 2 için bu Azure Resource Manager şablonu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f526-388">You can use this Azure Resource Manager template for SAP toohelp simplify deployment of required infrastructure resources for SAP Architectural Template 2.</span></span>

<span data-ttu-id="2f526-389">İşte, bu dağıtım senaryosu için Azure Resource Manager şablonları burada alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2f526-389">Here's where you can get Azure Resource Manager templates for this deployment scenario:</span></span>

* [<span data-ttu-id="2f526-390">Azure Market görüntüsü</span><span class="sxs-lookup"><span data-stu-id="2f526-390">Azure Marketplace image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged)  
* [<span data-ttu-id="2f526-391">Yönetilen diskleri kullanarak azure Market görüntüsü</span><span class="sxs-lookup"><span data-stu-id="2f526-391">Azure Marketplace image using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged-md)  
* [<span data-ttu-id="2f526-392">Özel görüntü</span><span class="sxs-lookup"><span data-stu-id="2f526-392">Custom image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged)
* [<span data-ttu-id="2f526-393">Özel görüntü yönetilen diskleri kullanma</span><span class="sxs-lookup"><span data-stu-id="2f526-393">Custom image using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged-md)


### <a name="prepare-hello-infrastructure-for-architectural-template-3"></a><span data-ttu-id="2f526-394">Mimari şablonu 3 Hello altyapıyı hazırlama</span><span class="sxs-lookup"><span data-stu-id="2f526-394">Prepare hello infrastructure for Architectural Template 3</span></span>

<span data-ttu-id="2f526-395">Hello altyapıyı hazırlama ve yapılandırma için SAP **çoklu SID**.</span><span class="sxs-lookup"><span data-stu-id="2f526-395">You can prepare hello infrastructure and configure SAP for **multi-SID**.</span></span> <span data-ttu-id="2f526-396">Örneğin, ek bir SAP ASCS/SCS örneğine ekleyebileceğiniz bir *varolan* küme yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="2f526-396">For example, you can add an additional SAP ASCS/SCS instance into an *existing* cluster configuration.</span></span> <span data-ttu-id="2f526-397">Daha fazla bilgi için bkz: [var olan bir küme yapılandırması toocreate bir SAP çoklu SID yapılandırma ek bir SAP ASCS/SCS örneğine Azure Kaynak Yöneticisi'nde yapılandırma][sap-ha-multi-sid-guide].</span><span class="sxs-lookup"><span data-stu-id="2f526-397">For more information, see [Configure an additional SAP ASCS/SCS instance into an existing cluster configuration toocreate an SAP multi-SID configuration in Azure Resource Manager][sap-ha-multi-sid-guide].</span></span>

<span data-ttu-id="2f526-398">Yeni bir SID çoklu küme toocreate istiyorsanız hello multi-SID kullanabilirsiniz [GitHub hızlı başlangıç şablonlarında](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="2f526-398">If you want toocreate a new multi-SID cluster, you can use hello multi-SID [quickstart templates on GitHub](https://github.com/Azure/azure-quickstart-templates).</span></span>
<span data-ttu-id="2f526-399">Yeni bir SID çoklu küme toocreate, üç şablonları aşağıdaki toodeploy hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="2f526-399">toocreate a new multi-SID cluster, you need toodeploy hello following three templates:</span></span>

* [<span data-ttu-id="2f526-400">ASCS/SCS şablonu</span><span class="sxs-lookup"><span data-stu-id="2f526-400">ASCS/SCS template</span></span>](#ASCS-SCS-template)
* [<span data-ttu-id="2f526-401">Veritabanı şablonu</span><span class="sxs-lookup"><span data-stu-id="2f526-401">Database template</span></span>](#database-template)
* [<span data-ttu-id="2f526-402">Uygulama sunucuları şablonu</span><span class="sxs-lookup"><span data-stu-id="2f526-402">Application servers template</span></span>](#application-servers-template)

<span data-ttu-id="2f526-403">Merhaba aşağıdaki bölümlerde hello şablonları ve hello şablonlarındaki tooprovide ihtiyacınız hello parametreleri hakkında daha fazla ayrıntı sahip.</span><span class="sxs-lookup"><span data-stu-id="2f526-403">hello following sections have more details about hello templates and hello parameters you need tooprovide in hello templates.</span></span>

#### <span data-ttu-id="2f526-404"><a name="ASCS-SCS-template"></a>ASCS/SCS şablonu</span><span class="sxs-lookup"><span data-stu-id="2f526-404"><a name="ASCS-SCS-template"></a> ASCS/SCS template</span></span>

<span data-ttu-id="2f526-405">Merhaba ASCS/SCS şablonu toocreate birden çok ASCS/SCS örneği barındıran bir Windows Server Yük devretme kümesi kullanabileceğiniz iki sanal makine dağıtır.</span><span class="sxs-lookup"><span data-stu-id="2f526-405">hello ASCS/SCS template deploys two virtual machines that you can use toocreate a Windows Server failover cluster that hosts multiple ASCS/SCS instances.</span></span>

<span data-ttu-id="2f526-406">Merhaba ASCS/SCS multi-SID şablonunda hello yukarı tooset [ASCS/SCS çoklu SID şablonu] [ sap-templates-3-tier-multisid-xscs-marketplace-image] veya [ASCS/SCS çoklu SID şablonu yönetilen diskleri kullanarak] [ sap-templates-3-tier-multisid-xscs-marketplace-image-md], hello şu parametreler için değerler girin:</span><span class="sxs-lookup"><span data-stu-id="2f526-406">tooset up hello ASCS/SCS multi-SID template, in hello [ASCS/SCS multi-SID template][sap-templates-3-tier-multisid-xscs-marketplace-image] or [ASCS/SCS multi-SID template using Managed Disks][sap-templates-3-tier-multisid-xscs-marketplace-image-md], enter values for hello following parameters:</span></span>

  - <span data-ttu-id="2f526-407">**Kaynak önek**.</span><span class="sxs-lookup"><span data-stu-id="2f526-407">**Resource Prefix**.</span></span>  <span data-ttu-id="2f526-408">Kullanılan tooprefix olan hello kaynak öneki hello dağıtımı sırasında oluşturulan tüm kaynakları ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="2f526-408">Set hello resource prefix, which is used tooprefix all resources that are created during hello deployment.</span></span> <span data-ttu-id="2f526-409">Merhaba kaynakları tooonly bir SAP sistemine ait olmadığından hello kaynak hello öneki hello bir SAP sistem SID'si değil.</span><span class="sxs-lookup"><span data-stu-id="2f526-409">Because hello resources do not belong tooonly one SAP system, hello prefix of hello resource is not hello SID of one SAP system.</span></span>  <span data-ttu-id="2f526-410">Merhaba önek arasında olmalıdır **üç ve altı karakter**.</span><span class="sxs-lookup"><span data-stu-id="2f526-410">hello prefix must be between **three and six characters**.</span></span>
  - <span data-ttu-id="2f526-411">**Yığın türü**.</span><span class="sxs-lookup"><span data-stu-id="2f526-411">**Stack Type**.</span></span> <span data-ttu-id="2f526-412">Merhaba yığını hello SAP sistem türünü seçin.</span><span class="sxs-lookup"><span data-stu-id="2f526-412">Select hello stack type of hello SAP system.</span></span> <span data-ttu-id="2f526-413">Merhaba yığını türüne bağlı olarak, Azure yük dengeleyici (ABAP veya yalnızca Java) bir veya iki (ABAP + Java) özel IP adresleri SAP sistem başına var.</span><span class="sxs-lookup"><span data-stu-id="2f526-413">Depending on hello stack type, Azure Load Balancer has one (ABAP or Java only) or two (ABAP+Java) private IP addresses per SAP system.</span></span>
  -  <span data-ttu-id="2f526-414">**İşletim sistemi türü**.</span><span class="sxs-lookup"><span data-stu-id="2f526-414">**OS Type**.</span></span> <span data-ttu-id="2f526-415">Merhaba sanal makinelerin Hello işletim sistemini seçin.</span><span class="sxs-lookup"><span data-stu-id="2f526-415">Select hello operating system of hello virtual machines.</span></span>
  -  <span data-ttu-id="2f526-416">**SAP sistem sayısı**.</span><span class="sxs-lookup"><span data-stu-id="2f526-416">**SAP System Count**.</span></span> <span data-ttu-id="2f526-417">Merhaba numarasını seçin SAP sistemlerinin bu kümedeki tooinstall istiyor.</span><span class="sxs-lookup"><span data-stu-id="2f526-417">Select hello number of SAP systems you want tooinstall in this cluster.</span></span>
  -  <span data-ttu-id="2f526-418">**Sistem kullanılabilirliğini**.</span><span class="sxs-lookup"><span data-stu-id="2f526-418">**System Availability**.</span></span> <span data-ttu-id="2f526-419">Seçin **HA**.</span><span class="sxs-lookup"><span data-stu-id="2f526-419">Select **HA**.</span></span>
  -  <span data-ttu-id="2f526-420">**Yönetici kullanıcı adı ve yönetici parolası**.</span><span class="sxs-lookup"><span data-stu-id="2f526-420">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="2f526-421">Kullanılan toosign toohello makinede olabilir yeni bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2f526-421">Create a new user that can be used toosign in toohello machine.</span></span>
  -  <span data-ttu-id="2f526-422">**Yeni veya var olan bir alt ağ**.</span><span class="sxs-lookup"><span data-stu-id="2f526-422">**New Or Existing Subnet**.</span></span> <span data-ttu-id="2f526-423">Yeni sanal ağ ve alt oluşturulmalıdır veya mevcut bir alt kullanılmalıdır gerekip gerekmediğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="2f526-423">Set whether a new virtual network and subnet should be created, or an existing subnet should be used.</span></span> <span data-ttu-id="2f526-424">Bağlı tooyour şirket içi ağ bir sanal ağ zaten varsa, seçin **varolan**.</span><span class="sxs-lookup"><span data-stu-id="2f526-424">If you already have a virtual network that is connected tooyour on-premises network, select **existing**.</span></span>
  -  <span data-ttu-id="2f526-425">**Alt ağ kimliği**. Kümesi hello kimliği hello alt toowhich hello sanal makinelerin bağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f526-425">**Subnet Id**. Set hello ID of hello subnet toowhich hello virtual machines should be connected.</span></span> <span data-ttu-id="2f526-426">Sanal özel ağ (VPN) veya ExpressRoute sanal ağ tooconnect hello sanal makine tooyour şirket içi ağın Hello alt ağ seçin.</span><span class="sxs-lookup"><span data-stu-id="2f526-426">Select hello subnet of your virtual private network (VPN) or ExpressRoute virtual network tooconnect hello virtual machine tooyour on-premises network.</span></span> <span data-ttu-id="2f526-427">Merhaba kimliği genellikle şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="2f526-427">hello ID usually looks like this:</span></span>

   <span data-ttu-id="2f526-428">/Subscriptions/ <*abonelik kimliği*> /resourceGroups/ <*kaynak grubu adı*> /providers/Microsoft.Network/virtualNetworks/ <*sanal ağ adı*> /subnets/ <*alt ağ adı*></span><span class="sxs-lookup"><span data-stu-id="2f526-428">/subscriptions/<*subscription id*>/resourceGroups/<*resource group name*>/providers/Microsoft.Network/virtualNetworks/<*virtual network name*>/subnets/<*subnet name*></span></span>

<span data-ttu-id="2f526-429">Merhaba şablon birden çok SAP sistemlerini destekleyen bir Azure yük dengeleyici örneği dağıtır.</span><span class="sxs-lookup"><span data-stu-id="2f526-429">hello template deploys one Azure Load Balancer instance, which supports multiple SAP systems.</span></span>

- <span data-ttu-id="2f526-430">Merhaba ASCS örnekleri örnek numarası 00, 10, 20 yapılandırılmış...</span><span class="sxs-lookup"><span data-stu-id="2f526-430">hello ASCS instances are configured for instance number 00, 10, 20...</span></span>
- <span data-ttu-id="2f526-431">Merhaba SCS örnekleri örnek numarası 01, 11, 21 yapılandırılmış...</span><span class="sxs-lookup"><span data-stu-id="2f526-431">hello SCS instances are configured for instance number 01, 11, 21...</span></span>
- <span data-ttu-id="2f526-432">Merhaba ASCS kuyruğa çoğaltma sunucusuna (ERS) (yalnızca Linux) örnekleri örnek numarası 02, 12, 22 yapılandırılmış...</span><span class="sxs-lookup"><span data-stu-id="2f526-432">hello ASCS Enqueue Replication Server (ERS) (Linux only) instances are configured for instance number 02, 12, 22...</span></span>
- <span data-ttu-id="2f526-433">Merhaba SCS ERS (yalnızca Linux) örnekleri örneği için 03, 13, 23 sayısı yapılandırılan...</span><span class="sxs-lookup"><span data-stu-id="2f526-433">hello SCS ERS (Linux only) instances are configured for instance number 03, 13, 23...</span></span>

<span data-ttu-id="2f526-434">Merhaba yük dengeleyici içeren 1 (Linux için 2) VIP(s), ASCS/SCS için 1 x VIP ve 1 x VIP ERS (yalnızca Linux) için.</span><span class="sxs-lookup"><span data-stu-id="2f526-434">hello load balancer contains 1 (2 for Linux) VIP(s), 1x VIP for ASCS/SCS and 1x VIP for ERS (Linux only).</span></span>

<span data-ttu-id="2f526-435">Merhaba aşağıdaki listede tüm Yük Dengeleme kuralları (burada x hello hello SAP sistem, örneğin, 1, 2, 3... sayısıdır) içerir:</span><span class="sxs-lookup"><span data-stu-id="2f526-435">hello following list contains all load balancing rules (where x is hello number of hello SAP system, for example, 1, 2, 3...):</span></span>
- <span data-ttu-id="2f526-436">Her SAP sistemi için Windows özel bağlantı noktaları: 445, 5985</span><span class="sxs-lookup"><span data-stu-id="2f526-436">Windows-specific ports for every SAP system: 445, 5985</span></span>
- <span data-ttu-id="2f526-437">ASCS bağlantı noktası (örnek numarasını x0): 32 x 0, 36 x 0, 39 x 0, 81 x 0, 5 x 013, 5 x 014, 5 x 016</span><span class="sxs-lookup"><span data-stu-id="2f526-437">ASCS ports (instance number x0): 32x0, 36x0, 39x0, 81x0, 5x013, 5x014, 5x016</span></span>
- <span data-ttu-id="2f526-438">SCS bağlantı noktası (örnek numarasını x1): 32 x 1, 33 x 1, 39 x 1, 81 x 1, 5 x 113, 5 x 114, 5 x 116</span><span class="sxs-lookup"><span data-stu-id="2f526-438">SCS ports (instance number x1): 32x1, 33x1, 39x1, 81x1, 5x113, 5x114, 5x116</span></span>
- <span data-ttu-id="2f526-439">ASCS ERS bağlantı noktaları (örnek numarasını x2) Linux'ta: 33 x 2, 5 x 213, 5 x 214, 5 x 216</span><span class="sxs-lookup"><span data-stu-id="2f526-439">ASCS ERS ports on Linux (instance number x2): 33x2, 5x213, 5x214, 5x216</span></span>
- <span data-ttu-id="2f526-440">SCS ERS bağlantı noktaları (örnek numarasını x3) Linux'ta: 33 x 3, 5 x 313, 5 x 314, 5 x 316</span><span class="sxs-lookup"><span data-stu-id="2f526-440">SCS ERS ports on Linux (instance number x3): 33x3, 5x313, 5x314, 5x316</span></span>

<span data-ttu-id="2f526-441">Merhaba yük dengeleyici yapılandırılmış toouse hello araştırma bağlantı noktaları (burada x hello hello SAP sistem, örneğin, 1, 2, 3... sayısıdır) aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="2f526-441">hello load balancer is configured toouse hello following probe ports (where x is hello number of hello SAP system, for example, 1, 2, 3...):</span></span>
- <span data-ttu-id="2f526-442">ASCS/SCS iç yük dengeleyici araştırması bağlantı noktası: 620 x 0</span><span class="sxs-lookup"><span data-stu-id="2f526-442">ASCS/SCS internal load balancer probe port: 620x0</span></span>
- <span data-ttu-id="2f526-443">ERS iç yük dengeleyici araştırması bağlantı noktası (yalnızca Linux): 621 x 2</span><span class="sxs-lookup"><span data-stu-id="2f526-443">ERS internal load balancer probe port (Linux only): 621x2</span></span>

#### <span data-ttu-id="2f526-444"><a name="database-template"></a>Veritabanı şablonu</span><span class="sxs-lookup"><span data-stu-id="2f526-444"><a name="database-template"></a> Database template</span></span>

<span data-ttu-id="2f526-445">Merhaba veritabanı şablonu bir dağıtır veya tooinstall kullanabileceğiniz iki sanal makine için bir SAP sistem ilişkisel veritabanı yönetim sistemine (RDBMS) hello.</span><span class="sxs-lookup"><span data-stu-id="2f526-445">hello database template deploys one or two virtual machines that you can use tooinstall hello relational database management system (RDBMS) for one SAP system.</span></span> <span data-ttu-id="2f526-446">Beş SAP sistemleri için bir ASCS/SCS şablonu dağıtırsanız, örneğin, toodeploy bu şablonu beş kez gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f526-446">For example, if you deploy an ASCS/SCS template for five SAP systems, you need toodeploy this template five times.</span></span>

<span data-ttu-id="2f526-447">Merhaba, hello veritabanı çoklu SID şablonu tooset [veritabanı çoklu SID şablonu] [ sap-templates-3-tier-multisid-db-marketplace-image] veya [yönetilen diskleri kullanarak veritabanı çoklu SID şablonu] [ sap-templates-3-tier-multisid-db-marketplace-image-md], hello şu parametreler için değerler girin:</span><span class="sxs-lookup"><span data-stu-id="2f526-447">tooset up hello database multi-SID template, in hello [database multi-SID template][sap-templates-3-tier-multisid-db-marketplace-image] or [database multi-SID template using Managed Disks][sap-templates-3-tier-multisid-db-marketplace-image-md], enter values for hello following parameters:</span></span>

  -  <span data-ttu-id="2f526-448">**SAP sistem kimliği**. Merhaba tooinstall istediğiniz SAP sistemi Hello SAP sistem Kimliğini girin.</span><span class="sxs-lookup"><span data-stu-id="2f526-448">**Sap System Id**. Enter hello SAP system ID of hello SAP system you want tooinstall.</span></span> <span data-ttu-id="2f526-449">Merhaba kimliği önek olarak dağıtılan hello kaynaklar için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2f526-449">hello ID will be used as a prefix for hello resources that are deployed.</span></span>
  -  <span data-ttu-id="2f526-450">**İşletim sistemi türü**.</span><span class="sxs-lookup"><span data-stu-id="2f526-450">**Os Type**.</span></span> <span data-ttu-id="2f526-451">Merhaba sanal makinelerin Hello işletim sistemini seçin.</span><span class="sxs-lookup"><span data-stu-id="2f526-451">Select hello operating system of hello virtual machines.</span></span>
  -  <span data-ttu-id="2f526-452">**DbType**.</span><span class="sxs-lookup"><span data-stu-id="2f526-452">**Dbtype**.</span></span> <span data-ttu-id="2f526-453">Merhaba türünü seçin hello veritabanı hello kümede tooinstall istiyor.</span><span class="sxs-lookup"><span data-stu-id="2f526-453">Select hello type of hello database you want tooinstall on hello cluster.</span></span> <span data-ttu-id="2f526-454">Seçin **SQL** tooinstall Microsoft SQL Server istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="2f526-454">Select **SQL** if you want tooinstall Microsoft SQL Server.</span></span> <span data-ttu-id="2f526-455">Seçin **HANA** hello sanal makinelerde tooinstall SAP HANA planlıyorsanız.</span><span class="sxs-lookup"><span data-stu-id="2f526-455">Select **HANA** if you plan tooinstall SAP HANA on hello virtual machines.</span></span> <span data-ttu-id="2f526-456">Tooselect hello doğru işletim sistemi türü olduğundan emin olun: seçin **Windows** HANA için Linux dağıtımı seçin ve SQL için.</span><span class="sxs-lookup"><span data-stu-id="2f526-456">Make sure tooselect hello correct operating system type: select **Windows** for SQL, and select a Linux distribution for HANA.</span></span> <span data-ttu-id="2f526-457">Merhaba, sanal makineler olacaktır bağlı toohello Azure yük dengeleyici toosupport seçili hello veritabanı türü yapılandırılır:</span><span class="sxs-lookup"><span data-stu-id="2f526-457">hello Azure Load Balancer that is connected toohello virtual machines will be configured toosupport hello selected database type:</span></span>
    * <span data-ttu-id="2f526-458">**SQL**.</span><span class="sxs-lookup"><span data-stu-id="2f526-458">**SQL**.</span></span> <span data-ttu-id="2f526-459">Merhaba yük dengeleyici Yük Dengeleme bağlantı noktası 1433 olur.</span><span class="sxs-lookup"><span data-stu-id="2f526-459">hello load balancer will load-balance port 1433.</span></span> <span data-ttu-id="2f526-460">Bu bağlantı noktası için SQL Server Always On kurulumunuzu emin toouse olun.</span><span class="sxs-lookup"><span data-stu-id="2f526-460">Make sure toouse this port for your SQL Server Always On setup.</span></span>
    * <span data-ttu-id="2f526-461">**HANA**.</span><span class="sxs-lookup"><span data-stu-id="2f526-461">**HANA**.</span></span> <span data-ttu-id="2f526-462">Merhaba yük dengeleyici Yük Dengeleme 35015 ve 35017 bağlantı noktalarını olur.</span><span class="sxs-lookup"><span data-stu-id="2f526-462">hello load balancer will load-balance ports 35015 and 35017.</span></span> <span data-ttu-id="2f526-463">İle örnek numarasını emin tooinstall SAP HANA olun **50**.</span><span class="sxs-lookup"><span data-stu-id="2f526-463">Make sure tooinstall SAP HANA with instance number **50**.</span></span>
    <span data-ttu-id="2f526-464">Merhaba yük dengeleyici araştırması bağlantı noktasını 62550 kullanır.</span><span class="sxs-lookup"><span data-stu-id="2f526-464">hello load balancer will use probe port 62550.</span></span>
  -  <span data-ttu-id="2f526-465">**SAP sistem boyutu**.</span><span class="sxs-lookup"><span data-stu-id="2f526-465">**Sap System Size**.</span></span> <span data-ttu-id="2f526-466">SAP hello yeni sistem kümesi hello sayısını sağlar.</span><span class="sxs-lookup"><span data-stu-id="2f526-466">Set hello number of SAPS hello new system will provide.</span></span> <span data-ttu-id="2f526-467">Kaç tane SAP hello sistem gerektirir emin değilseniz, SAP teknolojisi iş ortağı veya sistem Tümleştirici isteyin.</span><span class="sxs-lookup"><span data-stu-id="2f526-467">If you are not sure how many SAPS hello system will require, ask your SAP Technology Partner or System Integrator.</span></span>
  -  <span data-ttu-id="2f526-468">**Sistem kullanılabilirliğini**.</span><span class="sxs-lookup"><span data-stu-id="2f526-468">**System Availability**.</span></span> <span data-ttu-id="2f526-469">Seçin **HA**.</span><span class="sxs-lookup"><span data-stu-id="2f526-469">Select **HA**.</span></span>
  -  <span data-ttu-id="2f526-470">**Yönetici kullanıcı adı ve yönetici parolası**.</span><span class="sxs-lookup"><span data-stu-id="2f526-470">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="2f526-471">Kullanılan toosign toohello makinede olabilir yeni bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2f526-471">Create a new user that can be used toosign in toohello machine.</span></span>
  -  <span data-ttu-id="2f526-472">**Alt ağ kimliği**. Merhaba hello ASCS/SCS şablonu hello dağıtımı sırasında kullanılan hello alt ağ Kimliğini veya hello oluşturulduğu hello alt ağ Kimliğini hello ASCS/SCS şablon dağıtımı bir parçası olarak girin.</span><span class="sxs-lookup"><span data-stu-id="2f526-472">**Subnet Id**. Enter hello ID of hello subnet that you used during hello deployment of hello ASCS/SCS template, or hello ID of hello subnet that was created as part of hello ASCS/SCS template deployment.</span></span>

#### <span data-ttu-id="2f526-473"><a name="application-servers-template"></a>Uygulama sunucuları şablonu</span><span class="sxs-lookup"><span data-stu-id="2f526-473"><a name="application-servers-template"></a> Application servers template</span></span>

<span data-ttu-id="2f526-474">Merhaba uygulama sunucuları şablonu iki veya daha fazla sanal SAP uygulama sunucusu örneklerinin bir SAP sistemi için kullanılabilecek makineler dağıtır.</span><span class="sxs-lookup"><span data-stu-id="2f526-474">hello application servers template deploys two or more virtual machines that can be used as SAP Application Server instances for one SAP system.</span></span> <span data-ttu-id="2f526-475">Beş SAP sistemleri için bir ASCS/SCS şablonu dağıtırsanız, örneğin, toodeploy bu şablonu beş kez gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f526-475">For example, if you deploy an ASCS/SCS template for five SAP systems, you need toodeploy this template five times.</span></span>

<span data-ttu-id="2f526-476">Merhaba uygulama sunucuları çoklu SID şablonunda, hello yukarı tooset [uygulama sunucuları çoklu SID şablonu] [ sap-templates-3-tier-multisid-apps-marketplace-image] veya [uygulama sunucuları çoklu SID şablonu yönetilen disklerikullanma] [ sap-templates-3-tier-multisid-apps-marketplace-image-md], hello şu parametreler için değerler girin:</span><span class="sxs-lookup"><span data-stu-id="2f526-476">tooset up hello application servers multi-SID template, in hello [application servers multi-SID template][sap-templates-3-tier-multisid-apps-marketplace-image] or [application servers multi-SID template using Managed Disks][sap-templates-3-tier-multisid-apps-marketplace-image-md], enter values for hello following parameters:</span></span>

  -  <span data-ttu-id="2f526-477">**SAP sistem kimliği**. Merhaba tooinstall istediğiniz SAP sistemi Hello SAP sistem Kimliğini girin.</span><span class="sxs-lookup"><span data-stu-id="2f526-477">**Sap System Id**. Enter hello SAP system ID of hello SAP system you want tooinstall.</span></span> <span data-ttu-id="2f526-478">Merhaba kimliği önek olarak dağıtılan hello kaynaklar için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2f526-478">hello ID will be used as a prefix for hello resources that are deployed.</span></span>
  -  <span data-ttu-id="2f526-479">**İşletim sistemi türü**.</span><span class="sxs-lookup"><span data-stu-id="2f526-479">**Os Type**.</span></span> <span data-ttu-id="2f526-480">Merhaba sanal makinelerin Hello işletim sistemini seçin.</span><span class="sxs-lookup"><span data-stu-id="2f526-480">Select hello operating system of hello virtual machines.</span></span>
  -  <span data-ttu-id="2f526-481">**SAP sistem boyutu**.</span><span class="sxs-lookup"><span data-stu-id="2f526-481">**Sap System Size**.</span></span> <span data-ttu-id="2f526-482">SAP hello yeni sistem Hello sayısını sağlar.</span><span class="sxs-lookup"><span data-stu-id="2f526-482">hello number of SAPS hello new system will provide.</span></span> <span data-ttu-id="2f526-483">Kaç tane SAP hello sistem gerektirir emin değilseniz, SAP teknolojisi iş ortağı veya sistem Tümleştirici isteyin.</span><span class="sxs-lookup"><span data-stu-id="2f526-483">If you are not sure how many SAPS hello system will require, ask your SAP Technology Partner or System Integrator.</span></span>
  -  <span data-ttu-id="2f526-484">**Sistem kullanılabilirliğini**.</span><span class="sxs-lookup"><span data-stu-id="2f526-484">**System Availability**.</span></span> <span data-ttu-id="2f526-485">Seçin **HA**.</span><span class="sxs-lookup"><span data-stu-id="2f526-485">Select **HA**.</span></span>
  -  <span data-ttu-id="2f526-486">**Yönetici kullanıcı adı ve yönetici parolası**.</span><span class="sxs-lookup"><span data-stu-id="2f526-486">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="2f526-487">Kullanılan toosign toohello makinede olabilir yeni bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2f526-487">Create a new user that can be used toosign in toohello machine.</span></span>
  -  <span data-ttu-id="2f526-488">**Alt ağ kimliği**. Merhaba hello ASCS/SCS şablonu hello dağıtımı sırasında kullanılan hello alt ağ Kimliğini veya hello oluşturulduğu hello alt ağ Kimliğini hello ASCS/SCS şablon dağıtımı bir parçası olarak girin.</span><span class="sxs-lookup"><span data-stu-id="2f526-488">**Subnet Id**. Enter hello ID of hello subnet that you used during hello deployment of hello ASCS/SCS template, or hello ID of hello subnet that was created as part of hello ASCS/SCS template deployment.</span></span>


### <span data-ttu-id="2f526-489"><a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a>Azure sanal ağı</span><span class="sxs-lookup"><span data-stu-id="2f526-489"><a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a> Azure virtual network</span></span>
<span data-ttu-id="2f526-490">Bizim örneğimizde, hello Azure sanal ağı hello adres alanı 10.0.0.0/16 şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="2f526-490">In our example, hello address space of hello Azure virtual network is 10.0.0.0/16.</span></span> <span data-ttu-id="2f526-491">Adlı bir alt ağ yok **alt**, 10.0.0.0/24 adres aralığı olan.</span><span class="sxs-lookup"><span data-stu-id="2f526-491">There is one subnet called **Subnet**, with an address range of 10.0.0.0/24.</span></span> <span data-ttu-id="2f526-492">Bu sanal ağda, tüm sanal makineler ve iç yük dengeleyicileri dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="2f526-492">All virtual machines and internal load balancers are deployed in this virtual network.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2f526-493">Toohello ağ ayarlarını hello konuk işletim sistemi içinde herhangi bir değişiklik yapmayın.</span><span class="sxs-lookup"><span data-stu-id="2f526-493">Don't make any changes toohello network settings inside hello guest operating system.</span></span> <span data-ttu-id="2f526-494">Bu IP adresleri, DNS sunucuları ve alt ağ içerir.</span><span class="sxs-lookup"><span data-stu-id="2f526-494">This includes IP addresses, DNS servers, and subnet.</span></span> <span data-ttu-id="2f526-495">Azure'da tüm ağ ayarlarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="2f526-495">Configure all your network settings in Azure.</span></span> <span data-ttu-id="2f526-496">Merhaba Dinamik Ana Bilgisayar Yapılandırma Protokolü (DHCP) hizmetini ayarlarınızı yayar.</span><span class="sxs-lookup"><span data-stu-id="2f526-496">hello Dynamic Host Configuration Protocol (DHCP) service propagates your settings.</span></span>
>
>

### <span data-ttu-id="2f526-497"><a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a>DNS IP adresleri</span><span class="sxs-lookup"><span data-stu-id="2f526-497"><a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a> DNS IP addresses</span></span>

<span data-ttu-id="2f526-498">DNS IP adresleri tooset hello gerekli, aşağıdaki adımları hello.</span><span class="sxs-lookup"><span data-stu-id="2f526-498">tooset hello required DNS IP addresses, do hello following steps.</span></span>

1.  <span data-ttu-id="2f526-499">Hello hello üzerinde Azure portal'ın **DNS sunucuları** dikey penceresinde olduğundan emin olun, sanal ağ **DNS sunucuları** seçeneği çok ayarlamak**özel DNS**.</span><span class="sxs-lookup"><span data-stu-id="2f526-499">In hello Azure portal, on hello **DNS servers** blade, make sure that your virtual network **DNS servers** option is set too**Custom DNS**.</span></span>
2.  <span data-ttu-id="2f526-500">Sahip olduğunuz ağ Hello türüne göre ayarlarınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="2f526-500">Select your settings based on hello type of network you have.</span></span> <span data-ttu-id="2f526-501">Daha fazla bilgi için kaynakları aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="2f526-501">For more information, see hello following resources:</span></span>
    * <span data-ttu-id="2f526-502">[Kurumsal ağ bağlantısı (şirket içi)][planning-guide-2.2]: hello hello şirket içi DNS sunucularının IP adreslerini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2f526-502">[Corporate network connectivity (cross-premises)][planning-guide-2.2]: Add hello IP addresses of hello on-premises DNS servers.</span></span>  
    <span data-ttu-id="2f526-503">Azure'da çalışan şirket içi DNS sunucuları toohello sanal makineleri genişletebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f526-503">You can extend on-premises DNS servers toohello virtual machines that are running in Azure.</span></span> <span data-ttu-id="2f526-504">Bu senaryoda hello Azure hello IP adreslerini ekleyebilirsiniz hello DNS hizmetinin çalıştığı sanal makineler.</span><span class="sxs-lookup"><span data-stu-id="2f526-504">In that scenario, you can add hello IP addresses of hello Azure virtual machines on which you run hello DNS service.</span></span>
    * <span data-ttu-id="2f526-505">[Yalnızca bulut dağıtım][planning-guide-2.1]: hello ek bir sanal makineyi dağıtmak, bir DNS sunucusu olarak hizmet veren aynı sanal ağ örneği.</span><span class="sxs-lookup"><span data-stu-id="2f526-505">[Cloud-only deployment][planning-guide-2.1]: Deploy an additional virtual machine in hello same Virtual Network instance that serves as a DNS server.</span></span> <span data-ttu-id="2f526-506">Hello Azure Hello IP adreslerini eklemek toorun DNS hizmetini ayarlama sanal makineler.</span><span class="sxs-lookup"><span data-stu-id="2f526-506">Add hello IP addresses of hello Azure virtual machines that you've set up toorun DNS service.</span></span>

    ![Şekil 12: Azure sanal ağı için DNS sunucularını yapılandırın][sap-ha-guide-figure-3001]

    <span data-ttu-id="2f526-508">_**Şekil 12:** Yapılandır DNS sunucuları için Azure sanal ağ_</span><span class="sxs-lookup"><span data-stu-id="2f526-508">_**Figure 12:** Configure DNS servers for Azure Virtual Network_</span></span>

  > [!NOTE]
  > <span data-ttu-id="2f526-509">Merhaba DNS sunucularının IP adreslerini hello değiştirirseniz, toorestart hello Azure sanal makineleri tooapply gereksinim hello değişiklik ve hello yeni DNS sunucularını yayar.</span><span class="sxs-lookup"><span data-stu-id="2f526-509">If you change hello IP addresses of hello DNS servers, you need toorestart hello Azure virtual machines tooapply hello change and propagate hello new DNS servers.</span></span>
  >
  >

<span data-ttu-id="2f526-510">Bizim örneğimizde, hello DNS hizmeti yüklenir ve bu Windows sanal makinelerde yapılandırılır:</span><span class="sxs-lookup"><span data-stu-id="2f526-510">In our example, hello DNS service is installed and configured on these Windows virtual machines:</span></span>

| <span data-ttu-id="2f526-511">Sanal makine rolü</span><span class="sxs-lookup"><span data-stu-id="2f526-511">Virtual machine role</span></span> | <span data-ttu-id="2f526-512">Sanal makine ana bilgisayar adı</span><span class="sxs-lookup"><span data-stu-id="2f526-512">Virtual machine host name</span></span> | <span data-ttu-id="2f526-513">Ağ kartı adı</span><span class="sxs-lookup"><span data-stu-id="2f526-513">Network card name</span></span> | <span data-ttu-id="2f526-514">Statik IP adresi</span><span class="sxs-lookup"><span data-stu-id="2f526-514">Static IP address</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2f526-515">İlk DNS sunucusu</span><span class="sxs-lookup"><span data-stu-id="2f526-515">First DNS server</span></span> |<span data-ttu-id="2f526-516">domcontr-0</span><span class="sxs-lookup"><span data-stu-id="2f526-516">domcontr-0</span></span> |<span data-ttu-id="2f526-517">pr1-NIC-domcontr-0</span><span class="sxs-lookup"><span data-stu-id="2f526-517">pr1-nic-domcontr-0</span></span> |<span data-ttu-id="2f526-518">10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="2f526-518">10.0.0.10</span></span> |
| <span data-ttu-id="2f526-519">İkinci DNS sunucusu</span><span class="sxs-lookup"><span data-stu-id="2f526-519">Second DNS server</span></span> |<span data-ttu-id="2f526-520">domcontr-1</span><span class="sxs-lookup"><span data-stu-id="2f526-520">domcontr-1</span></span> |<span data-ttu-id="2f526-521">pr1-NIC-domcontr-1</span><span class="sxs-lookup"><span data-stu-id="2f526-521">pr1-nic-domcontr-1</span></span> |<span data-ttu-id="2f526-522">10.0.0.11</span><span class="sxs-lookup"><span data-stu-id="2f526-522">10.0.0.11</span></span> |

### <span data-ttu-id="2f526-523"><a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a>Ana bilgisayar adları ve hello SAP ASCS/SCS kümelenmiş örneği ve DBMS kümelenmiş örneği için statik IP adresleri</span><span class="sxs-lookup"><span data-stu-id="2f526-523"><a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a> Host names and static IP addresses for hello SAP ASCS/SCS clustered instance and DBMS clustered instance</span></span>

<span data-ttu-id="2f526-524">Şirket içi dağıtım için bu ayrılmış ana bilgisayar adlarını ve IP adreslerini gerekir:</span><span class="sxs-lookup"><span data-stu-id="2f526-524">For on-premises deployment, you need these reserved host names and IP addresses:</span></span>

| <span data-ttu-id="2f526-525">Sanal ana bilgisayar adı rolü</span><span class="sxs-lookup"><span data-stu-id="2f526-525">Virtual host name role</span></span> | <span data-ttu-id="2f526-526">Sanal ana bilgisayar adı</span><span class="sxs-lookup"><span data-stu-id="2f526-526">Virtual host name</span></span> | <span data-ttu-id="2f526-527">Sanal statik IP adresi</span><span class="sxs-lookup"><span data-stu-id="2f526-527">Virtual static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2f526-528">SAP ASCS/SCS ilk küme sanal ana bilgisayar adı (küme yönetimi)</span><span class="sxs-lookup"><span data-stu-id="2f526-528">SAP ASCS/SCS first cluster virtual host name (for cluster management)</span></span> |<span data-ttu-id="2f526-529">pr1 ascs VIR</span><span class="sxs-lookup"><span data-stu-id="2f526-529">pr1-ascs-vir</span></span> |<span data-ttu-id="2f526-530">10.0.0.42</span><span class="sxs-lookup"><span data-stu-id="2f526-530">10.0.0.42</span></span> |
| <span data-ttu-id="2f526-531">SAP ASCS/SCS örnek sanal ana bilgisayar adı</span><span class="sxs-lookup"><span data-stu-id="2f526-531">SAP ASCS/SCS instance virtual host name</span></span> |<span data-ttu-id="2f526-532">pr1 ascs sap</span><span class="sxs-lookup"><span data-stu-id="2f526-532">pr1-ascs-sap</span></span> |<span data-ttu-id="2f526-533">10.0.0.43</span><span class="sxs-lookup"><span data-stu-id="2f526-533">10.0.0.43</span></span> |
| <span data-ttu-id="2f526-534">SAP DBMS ikinci küme sanal ana bilgisayar adı (küme yönetimi)</span><span class="sxs-lookup"><span data-stu-id="2f526-534">SAP DBMS second cluster virtual host name (cluster management)</span></span> |<span data-ttu-id="2f526-535">pr1 dbms VIR</span><span class="sxs-lookup"><span data-stu-id="2f526-535">pr1-dbms-vir</span></span> |<span data-ttu-id="2f526-536">10.0.0.32</span><span class="sxs-lookup"><span data-stu-id="2f526-536">10.0.0.32</span></span> |

<span data-ttu-id="2f526-537">Merhaba kümesi oluşturduğunuzda, sanal ana bilgisayar adlarını hello oluşturma **pr1 ascs VIR** ve **pr1 dbms VIR** ve hello ilişkili hello kümenin kendisi yönetmek IP adresleri.</span><span class="sxs-lookup"><span data-stu-id="2f526-537">When you create hello cluster, create hello virtual host names **pr1-ascs-vir** and **pr1-dbms-vir** and hello associated IP addresses that manage hello cluster itself.</span></span> <span data-ttu-id="2f526-538">Hakkında bilgi için toodo buna ek olarak, bkz: [toplamak küme düğümleri bir küme yapılandırmasında][sap-ha-guide-8.12.1].</span><span class="sxs-lookup"><span data-stu-id="2f526-538">For information about how toodo this, see [Collect cluster nodes in a cluster configuration][sap-ha-guide-8.12.1].</span></span>

<span data-ttu-id="2f526-539">Diğer iki sanal ana bilgisayar adlarını hello el ile oluşturabilirsiniz **pr1 ascs sap** ve **pr1 dbms sap**, hello ilişkili hello DNS sunucusu, IP adresleri ve.</span><span class="sxs-lookup"><span data-stu-id="2f526-539">You can manually create hello other two virtual host names, **pr1-ascs-sap** and **pr1-dbms-sap**, and hello associated IP addresses, on hello DNS server.</span></span> <span data-ttu-id="2f526-540">Merhaba kümelenmiş SAP ASCS/SCS örneği ve kümelenmiş hello DBMS örneği bu kaynakları kullanın.</span><span class="sxs-lookup"><span data-stu-id="2f526-540">hello clustered SAP ASCS/SCS instance and hello clustered DBMS instance use these resources.</span></span> <span data-ttu-id="2f526-541">Hakkında bilgi için toodo buna ek olarak, bkz: [kümelenmiş bir SAP ASCS/SCS örneği için bir sanal ana bilgisayar adı oluşturmak][sap-ha-guide-9.1.1].</span><span class="sxs-lookup"><span data-stu-id="2f526-541">For information about how toodo this, see [Create a virtual host name for a clustered SAP ASCS/SCS instance][sap-ha-guide-9.1.1].</span></span>

### <span data-ttu-id="2f526-542"><a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a>Statik IP adresleri hello SAP sanal makineler için ayarlama</span><span class="sxs-lookup"><span data-stu-id="2f526-542"><a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a> Set static IP addresses for hello SAP virtual machines</span></span>
<span data-ttu-id="2f526-543">Kümenizdeki hello sanal makineleri toouse dağıttıktan sonra tüm sanal makineler için tooset statik IP adresleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f526-543">After you deploy hello virtual machines toouse in your cluster, you need tooset static IP addresses for all virtual machines.</span></span> <span data-ttu-id="2f526-544">Bunu hello Azure sanal ağ yapılandırması ve hello konuk işletim sistemi içinde değil.</span><span class="sxs-lookup"><span data-stu-id="2f526-544">Do this in hello Azure Virtual Network configuration, and not in hello guest operating system.</span></span>

1.  <span data-ttu-id="2f526-545">Hello Azure portal, seçin **kaynak grubu** > **ağ kartı** > **ayarları** > **IP adresi** .</span><span class="sxs-lookup"><span data-stu-id="2f526-545">In hello Azure portal, select **Resource Group** > **Network Card** > **Settings** > **IP Address**.</span></span>
2.  <span data-ttu-id="2f526-546">Merhaba üzerinde **IP adreslerini** dikey altında **atama**seçin **statik**.</span><span class="sxs-lookup"><span data-stu-id="2f526-546">On hello **IP addresses** blade, under **Assignment**, select **Static**.</span></span> <span data-ttu-id="2f526-547">Merhaba, **IP adresi** kutusuna, toouse istediğiniz hello IP adresini girin.</span><span class="sxs-lookup"><span data-stu-id="2f526-547">In hello **IP address** box, enter hello IP address that you want toouse.</span></span>

  > [!NOTE]
  > <span data-ttu-id="2f526-548">Merhaba ağ kartı hello IP adresini değiştirirseniz, toorestart hello Azure sanal makineleri tooapply gereksinim hello değiştirin.</span><span class="sxs-lookup"><span data-stu-id="2f526-548">If you change hello IP address of hello network card, you need toorestart hello Azure virtual machines tooapply hello change.</span></span>  
  >
  >

  ![Şekil 13: hello ağ kartı her bir sanal makine için statik IP adresi ayarlayın][sap-ha-guide-figure-3002]

  <span data-ttu-id="2f526-550">_**Şekil 13:** ayarlamak hello ağ kartı her bir sanal makine için statik IP adresleri_</span><span class="sxs-lookup"><span data-stu-id="2f526-550">_**Figure 13:** Set static IP addresses for hello network card of each virtual machine_</span></span>

  <span data-ttu-id="2f526-551">Bu, tüm ağ arabirimleri için diğer bir deyişle, Active Directory DNS hizmetiniz için toouse istediğiniz sanal makineleri de dahil olmak üzere tüm sanal makineler için tekrarlayın.</span><span class="sxs-lookup"><span data-stu-id="2f526-551">Repeat this step for all network interfaces, that is, for all virtual machines, including virtual machines that you want toouse for your Active Directory/DNS service.</span></span>

<span data-ttu-id="2f526-552">Bizim örneğimizde, bu sanal makineleri ve statik IP adresleri vardır:</span><span class="sxs-lookup"><span data-stu-id="2f526-552">In our example, we have these virtual machines and static IP addresses:</span></span>

| <span data-ttu-id="2f526-553">Sanal makine rolü</span><span class="sxs-lookup"><span data-stu-id="2f526-553">Virtual machine role</span></span> | <span data-ttu-id="2f526-554">Sanal makine ana bilgisayar adı</span><span class="sxs-lookup"><span data-stu-id="2f526-554">Virtual machine host name</span></span> | <span data-ttu-id="2f526-555">Ağ kartı adı</span><span class="sxs-lookup"><span data-stu-id="2f526-555">Network card name</span></span> | <span data-ttu-id="2f526-556">Statik IP adresi</span><span class="sxs-lookup"><span data-stu-id="2f526-556">Static IP address</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2f526-557">İlk SAP uygulama sunucusu örneği</span><span class="sxs-lookup"><span data-stu-id="2f526-557">First SAP Application Server instance</span></span> |<span data-ttu-id="2f526-558">pr1 dı 0</span><span class="sxs-lookup"><span data-stu-id="2f526-558">pr1-di-0</span></span> |<span data-ttu-id="2f526-559">pr1-NIC-dı-0</span><span class="sxs-lookup"><span data-stu-id="2f526-559">pr1-nic-di-0</span></span> |<span data-ttu-id="2f526-560">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="2f526-560">10.0.0.50</span></span> |
| <span data-ttu-id="2f526-561">İkinci SAP uygulama sunucusu örneği</span><span class="sxs-lookup"><span data-stu-id="2f526-561">Second SAP Application Server instance</span></span> |<span data-ttu-id="2f526-562">pr1 dı 1</span><span class="sxs-lookup"><span data-stu-id="2f526-562">pr1-di-1</span></span> |<span data-ttu-id="2f526-563">pr1-NIC-dı-1</span><span class="sxs-lookup"><span data-stu-id="2f526-563">pr1-nic-di-1</span></span> |<span data-ttu-id="2f526-564">10.0.0.51</span><span class="sxs-lookup"><span data-stu-id="2f526-564">10.0.0.51</span></span> |
| <span data-ttu-id="2f526-565">...</span><span class="sxs-lookup"><span data-stu-id="2f526-565">...</span></span> |<span data-ttu-id="2f526-566">...</span><span class="sxs-lookup"><span data-stu-id="2f526-566">...</span></span> |<span data-ttu-id="2f526-567">...</span><span class="sxs-lookup"><span data-stu-id="2f526-567">...</span></span> |<span data-ttu-id="2f526-568">...</span><span class="sxs-lookup"><span data-stu-id="2f526-568">...</span></span> |
| <span data-ttu-id="2f526-569">Son SAP uygulama sunucusu örneği</span><span class="sxs-lookup"><span data-stu-id="2f526-569">Last SAP Application Server instance</span></span> |<span data-ttu-id="2f526-570">pr1 dı 5</span><span class="sxs-lookup"><span data-stu-id="2f526-570">pr1-di-5</span></span> |<span data-ttu-id="2f526-571">pr1-NIC-dı-5</span><span class="sxs-lookup"><span data-stu-id="2f526-571">pr1-nic-di-5</span></span> |<span data-ttu-id="2f526-572">10.0.0.55</span><span class="sxs-lookup"><span data-stu-id="2f526-572">10.0.0.55</span></span> |
| <span data-ttu-id="2f526-573">İlk küme düğümüne ASCS/SCS örneği için</span><span class="sxs-lookup"><span data-stu-id="2f526-573">First cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="2f526-574">pr1 ascs 0</span><span class="sxs-lookup"><span data-stu-id="2f526-574">pr1-ascs-0</span></span> |<span data-ttu-id="2f526-575">pr1-NIC-ascs-0</span><span class="sxs-lookup"><span data-stu-id="2f526-575">pr1-nic-ascs-0</span></span> |<span data-ttu-id="2f526-576">10.0.0.40</span><span class="sxs-lookup"><span data-stu-id="2f526-576">10.0.0.40</span></span> |
| <span data-ttu-id="2f526-577">İkinci küme düğümü ASCS/SCS örneği için</span><span class="sxs-lookup"><span data-stu-id="2f526-577">Second cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="2f526-578">pr1 ascs 1</span><span class="sxs-lookup"><span data-stu-id="2f526-578">pr1-ascs-1</span></span> |<span data-ttu-id="2f526-579">pr1-NIC-ascs-1</span><span class="sxs-lookup"><span data-stu-id="2f526-579">pr1-nic-ascs-1</span></span> |<span data-ttu-id="2f526-580">10.0.0.41</span><span class="sxs-lookup"><span data-stu-id="2f526-580">10.0.0.41</span></span> |
| <span data-ttu-id="2f526-581">İlk küme düğümüne DBMS örneği için</span><span class="sxs-lookup"><span data-stu-id="2f526-581">First cluster node for DBMS instance</span></span> |<span data-ttu-id="2f526-582">pr1-db-0</span><span class="sxs-lookup"><span data-stu-id="2f526-582">pr1-db-0</span></span> |<span data-ttu-id="2f526-583">pr1-NIC-db-0</span><span class="sxs-lookup"><span data-stu-id="2f526-583">pr1-nic-db-0</span></span> |<span data-ttu-id="2f526-584">10.0.0.30</span><span class="sxs-lookup"><span data-stu-id="2f526-584">10.0.0.30</span></span> |
| <span data-ttu-id="2f526-585">DBMS örneği için ikinci küme düğümü</span><span class="sxs-lookup"><span data-stu-id="2f526-585">Second cluster node for DBMS instance</span></span> |<span data-ttu-id="2f526-586">pr1-db-1</span><span class="sxs-lookup"><span data-stu-id="2f526-586">pr1-db-1</span></span> |<span data-ttu-id="2f526-587">pr1-NIC-db-1</span><span class="sxs-lookup"><span data-stu-id="2f526-587">pr1-nic-db-1</span></span> |<span data-ttu-id="2f526-588">10.0.0.31</span><span class="sxs-lookup"><span data-stu-id="2f526-588">10.0.0.31</span></span> |

### <span data-ttu-id="2f526-589"><a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a>Hello Azure iç yük dengeleyici için statik bir IP adresi ayarlayın</span><span class="sxs-lookup"><span data-stu-id="2f526-589"><a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a> Set a static IP address for hello Azure internal load balancer</span></span>

<span data-ttu-id="2f526-590">Merhaba SAP Azure Resource Manager şablonu hello SAP ASCS/SCS örnek küme ve hello DBMS küme için kullanılan bir Azure iç yük dengeleyici oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2f526-590">hello SAP Azure Resource Manager template creates an Azure internal load balancer that is used for hello SAP ASCS/SCS instance cluster and hello DBMS cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2f526-591">Merhaba SAP ASCS/SCS olan hello hello sanal ana bilgisayar adı, IP adresi hello aynı başlangıç IP adresi hello SAP ASCS/SCS iç yük dengeleyici olarak: **pr1 lb ascs**.</span><span class="sxs-lookup"><span data-stu-id="2f526-591">hello IP address of hello virtual host name of hello SAP ASCS/SCS is hello same as hello IP address of hello SAP ASCS/SCS internal load balancer: **pr1-lb-ascs**.</span></span>
> <span data-ttu-id="2f526-592">Merhaba hello sanal DBMS olduğu hello adını IP adresini hello aynı başlangıç IP adresi hello DBMS iç yük dengeleyici olarak: **pr1 lb dbms**.</span><span class="sxs-lookup"><span data-stu-id="2f526-592">hello IP address of hello virtual name of hello DBMS is hello same as hello IP address of hello DBMS internal load balancer: **pr1-lb-dbms**.</span></span>
>
>

<span data-ttu-id="2f526-593">Yük Dengeleyici tooset hello Azure iç için statik bir IP adresi:</span><span class="sxs-lookup"><span data-stu-id="2f526-593">tooset a static IP address for hello Azure internal load balancer:</span></span>

1.  <span data-ttu-id="2f526-594">Merhaba ilk dağıtım hello iç yük dengeleyici IP adresi çok ayarlar**dinamik**.</span><span class="sxs-lookup"><span data-stu-id="2f526-594">hello initial deployment sets hello internal load balancer IP address too**Dynamic**.</span></span> <span data-ttu-id="2f526-595">Merhaba hello üzerinde Azure portal'ın **IP adreslerini** dikey altında **atama**seçin **statik**.</span><span class="sxs-lookup"><span data-stu-id="2f526-595">In hello Azure portal, on hello **IP addresses** blade, under **Assignment**, select **Static**.</span></span>
2.  <span data-ttu-id="2f526-596">Başlangıç IP adresi hello iç yük dengeleyicisi ayarlayın **pr1 lb ascs** toohello IP adresini hello SAP ASCS/SCS örneğinin hello sanal ana bilgisayar adı.</span><span class="sxs-lookup"><span data-stu-id="2f526-596">Set hello IP address of hello internal load balancer **pr1-lb-ascs** toohello IP address of hello virtual host name of hello SAP ASCS/SCS instance.</span></span>
3.  <span data-ttu-id="2f526-597">Başlangıç IP adresi hello iç yük dengeleyicisi ayarlayın **pr1 lb dbms** toohello IP adresini hello DBMS örneğinin hello sanal ana bilgisayar adı.</span><span class="sxs-lookup"><span data-stu-id="2f526-597">Set hello IP address of hello internal load balancer **pr1-lb-dbms** toohello IP address of hello virtual host name of hello DBMS instance.</span></span>

  ![Şekil 14: hello SAP ASCS/SCS örneği için hello iç yük dengeleyici için statik IP adresleri ayarlayın.][sap-ha-guide-figure-3003]

  <span data-ttu-id="2f526-599">_**Şekil 14:** hello SAP ASCS/SCS örneği için hello iç yük dengeleyici için statik IP adresleri ayarlayın_</span><span class="sxs-lookup"><span data-stu-id="2f526-599">_**Figure 14:** Set static IP addresses for hello internal load balancer for hello SAP ASCS/SCS instance_</span></span>

<span data-ttu-id="2f526-600">Bizim örneğimizde, biz bu statik IP adresine sahip iki Azure iç yük dengeleyicileri vardır:</span><span class="sxs-lookup"><span data-stu-id="2f526-600">In our example, we have two Azure internal load balancers that have these static IP addresses:</span></span>

| <span data-ttu-id="2f526-601">Azure iç yük dengeleyici rol</span><span class="sxs-lookup"><span data-stu-id="2f526-601">Azure internal load balancer role</span></span> | <span data-ttu-id="2f526-602">Azure iç yük dengeleyicisi adı</span><span class="sxs-lookup"><span data-stu-id="2f526-602">Azure internal load balancer name</span></span> | <span data-ttu-id="2f526-603">Statik IP adresi</span><span class="sxs-lookup"><span data-stu-id="2f526-603">Static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2f526-604">SAP ASCS/SCS iç yük dengeleyici örneği</span><span class="sxs-lookup"><span data-stu-id="2f526-604">SAP ASCS/SCS instance internal load balancer</span></span> |<span data-ttu-id="2f526-605">pr1 lb ascs</span><span class="sxs-lookup"><span data-stu-id="2f526-605">pr1-lb-ascs</span></span> |<span data-ttu-id="2f526-606">10.0.0.43</span><span class="sxs-lookup"><span data-stu-id="2f526-606">10.0.0.43</span></span> |
| <span data-ttu-id="2f526-607">SAP DBMS iç yük dengeleyici</span><span class="sxs-lookup"><span data-stu-id="2f526-607">SAP DBMS internal load balancer</span></span> |<span data-ttu-id="2f526-608">pr1 lb dbms</span><span class="sxs-lookup"><span data-stu-id="2f526-608">pr1-lb-dbms</span></span> |<span data-ttu-id="2f526-609">10.0.0.33</span><span class="sxs-lookup"><span data-stu-id="2f526-609">10.0.0.33</span></span> |


### <span data-ttu-id="2f526-610"><a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a>Varsayılan ASCS/SCS Yük Dengeleme kuralları hello Azure iç yük dengeleyici için</span><span class="sxs-lookup"><span data-stu-id="2f526-610"><a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a> Default ASCS/SCS load balancing rules for hello Azure internal load balancer</span></span>

<span data-ttu-id="2f526-611">Merhaba SAP Azure Resource Manager şablonu ihtiyacınız hello bağlantı noktalarını oluşturur:</span><span class="sxs-lookup"><span data-stu-id="2f526-611">hello SAP Azure Resource Manager template creates hello ports you need:</span></span>
* <span data-ttu-id="2f526-612">Bir ABAP ASCS örneğiyle hello varsayılan örnek numarasını **00**</span><span class="sxs-lookup"><span data-stu-id="2f526-612">An ABAP ASCS instance, with hello default instance number **00**</span></span>
* <span data-ttu-id="2f526-613">Bir Java SCS örneğiyle hello varsayılan örnek numarasını **01**</span><span class="sxs-lookup"><span data-stu-id="2f526-613">A Java SCS instance, with hello default instance number **01**</span></span>

<span data-ttu-id="2f526-614">SAP ASCS/SCS örneğinizi yüklediğinizde hello varsayılan örnek numarasını kullanmalıdır **00** ABAP ASCS örneği ve hello varsayılan örneği numaranızı için **01** Java SCS Örneğiniz için.</span><span class="sxs-lookup"><span data-stu-id="2f526-614">When you install your SAP ASCS/SCS instance, you must use hello default instance number **00** for your ABAP ASCS instance and hello default instance number **01** for your Java SCS instance.</span></span>

<span data-ttu-id="2f526-615">Ardından, gerekli iç Yük Dengeleme hello SAP NetWeaver bağlantı noktaları için uç noktaları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2f526-615">Next, create required internal load balancing endpoints for hello SAP NetWeaver ports.</span></span>

<span data-ttu-id="2f526-616">İç Yük Dengeleme uç noktaları, ilk olarak, bu Yük Dengeleme hello SAP NetWeaver ABAP ASCS bağlantı noktaları için uç noktalar oluşturmak toocreate gerekli:</span><span class="sxs-lookup"><span data-stu-id="2f526-616">toocreate required internal load balancing endpoints, first, create these load balancing endpoints for hello SAP NetWeaver ABAP ASCS ports:</span></span>

| <span data-ttu-id="2f526-617">Hizmet/Yük Dengeleme kuralı adı</span><span class="sxs-lookup"><span data-stu-id="2f526-617">Service/load balancing rule name</span></span> | <span data-ttu-id="2f526-618">Varsayılan bağlantı noktası numaraları</span><span class="sxs-lookup"><span data-stu-id="2f526-618">Default port numbers</span></span> | <span data-ttu-id="2f526-619">Somut için bağlantı noktalarını (ASCS örneği ile örnek numarasını 00) (ERS 10 ile)</span><span class="sxs-lookup"><span data-stu-id="2f526-619">Concrete ports for (ASCS instance with instance number 00) (ERS with 10)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2f526-620">Sıraya alma sunucu / *lbrule3200*</span><span class="sxs-lookup"><span data-stu-id="2f526-620">Enqueue Server / *lbrule3200*</span></span> |<span data-ttu-id="2f526-621">32 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="2f526-621">32<*InstanceNumber*></span></span> |<span data-ttu-id="2f526-622">3200</span><span class="sxs-lookup"><span data-stu-id="2f526-622">3200</span></span> |
| <span data-ttu-id="2f526-623">ABAP ileti sunucusu / *lbrule3600*</span><span class="sxs-lookup"><span data-stu-id="2f526-623">ABAP Message Server / *lbrule3600*</span></span> |<span data-ttu-id="2f526-624">36 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="2f526-624">36<*InstanceNumber*></span></span> |<span data-ttu-id="2f526-625">3600</span><span class="sxs-lookup"><span data-stu-id="2f526-625">3600</span></span> |
| <span data-ttu-id="2f526-626">İç ABAP ileti / *lbrule3900*</span><span class="sxs-lookup"><span data-stu-id="2f526-626">Internal ABAP Message / *lbrule3900*</span></span> |<span data-ttu-id="2f526-627">39 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="2f526-627">39<*InstanceNumber*></span></span> |<span data-ttu-id="2f526-628">3900</span><span class="sxs-lookup"><span data-stu-id="2f526-628">3900</span></span> |
| <span data-ttu-id="2f526-629">Sunucu HTTP iletisi / *Lbrule8100*</span><span class="sxs-lookup"><span data-stu-id="2f526-629">Message Server HTTP / *Lbrule8100*</span></span> |<span data-ttu-id="2f526-630">81 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="2f526-630">81<*InstanceNumber*></span></span> |<span data-ttu-id="2f526-631">8100</span><span class="sxs-lookup"><span data-stu-id="2f526-631">8100</span></span> |
| <span data-ttu-id="2f526-632">SAP başlangıç hizmet ASCS HTTP / *Lbrule50013*</span><span class="sxs-lookup"><span data-stu-id="2f526-632">SAP Start Service ASCS HTTP / *Lbrule50013*</span></span> |<span data-ttu-id="2f526-633">5 <*InstanceNumber*> 13</span><span class="sxs-lookup"><span data-stu-id="2f526-633">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="2f526-634">50013</span><span class="sxs-lookup"><span data-stu-id="2f526-634">50013</span></span> |
| <span data-ttu-id="2f526-635">SAP başlangıç hizmet ASCS HTTPS / *Lbrule50014*</span><span class="sxs-lookup"><span data-stu-id="2f526-635">SAP Start Service ASCS HTTPS / *Lbrule50014*</span></span> |<span data-ttu-id="2f526-636">5 <*InstanceNumber*> 14</span><span class="sxs-lookup"><span data-stu-id="2f526-636">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="2f526-637">50014</span><span class="sxs-lookup"><span data-stu-id="2f526-637">50014</span></span> |
| <span data-ttu-id="2f526-638">Sıraya alma çoğaltma / *Lbrule50016*</span><span class="sxs-lookup"><span data-stu-id="2f526-638">Enqueue Replication / *Lbrule50016*</span></span> |<span data-ttu-id="2f526-639">5 <*InstanceNumber*> 16</span><span class="sxs-lookup"><span data-stu-id="2f526-639">5<*InstanceNumber*>16</span></span> |<span data-ttu-id="2f526-640">50016</span><span class="sxs-lookup"><span data-stu-id="2f526-640">50016</span></span> |
| <span data-ttu-id="2f526-641">SAP başlangıç hizmeti ERS HTTP *Lbrule51013*</span><span class="sxs-lookup"><span data-stu-id="2f526-641">SAP Start Service ERS HTTP *Lbrule51013*</span></span> |<span data-ttu-id="2f526-642">5 <*InstanceNumber*> 13</span><span class="sxs-lookup"><span data-stu-id="2f526-642">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="2f526-643">51013</span><span class="sxs-lookup"><span data-stu-id="2f526-643">51013</span></span> |
| <span data-ttu-id="2f526-644">SAP başlangıç hizmeti ERS HTTP *Lbrule51014*</span><span class="sxs-lookup"><span data-stu-id="2f526-644">SAP Start Service ERS HTTP *Lbrule51014*</span></span> |<span data-ttu-id="2f526-645">5 <*InstanceNumber*> 14</span><span class="sxs-lookup"><span data-stu-id="2f526-645">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="2f526-646">51014</span><span class="sxs-lookup"><span data-stu-id="2f526-646">51014</span></span> |
| <span data-ttu-id="2f526-647">RM win *Lbrule5985*</span><span class="sxs-lookup"><span data-stu-id="2f526-647">Win RM *Lbrule5985*</span></span> | |<span data-ttu-id="2f526-648">5985</span><span class="sxs-lookup"><span data-stu-id="2f526-648">5985</span></span> |
| <span data-ttu-id="2f526-649">Dosya Paylaşımı *Lbrule445*</span><span class="sxs-lookup"><span data-stu-id="2f526-649">File Share *Lbrule445*</span></span> | |<span data-ttu-id="2f526-650">445</span><span class="sxs-lookup"><span data-stu-id="2f526-650">445</span></span> |

<span data-ttu-id="2f526-651">_**Tablo 1:** bağlantı noktası numaralarını hello SAP NetWeaver ABAP ASCS örnekleri_</span><span class="sxs-lookup"><span data-stu-id="2f526-651">_**Table 1:** Port numbers of hello SAP NetWeaver ABAP ASCS instances_</span></span>

<span data-ttu-id="2f526-652">Ardından, bu Yük Dengeleme hello SAP NetWeaver Java SCS bağlantı noktaları için uç nokta oluşturun:</span><span class="sxs-lookup"><span data-stu-id="2f526-652">Then, create these load balancing endpoints for hello SAP NetWeaver Java SCS ports:</span></span>

| <span data-ttu-id="2f526-653">Hizmet/Yük Dengeleme kuralı adı</span><span class="sxs-lookup"><span data-stu-id="2f526-653">Service/load balancing rule name</span></span> | <span data-ttu-id="2f526-654">Varsayılan bağlantı noktası numaraları</span><span class="sxs-lookup"><span data-stu-id="2f526-654">Default port numbers</span></span> | <span data-ttu-id="2f526-655">Somut için bağlantı noktalarını (SCS örneği ile örnek numarasını 01) (ERS 11 ile)</span><span class="sxs-lookup"><span data-stu-id="2f526-655">Concrete ports for (SCS instance with instance number 01) (ERS with 11)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2f526-656">Sıraya alma sunucu / *lbrule3201*</span><span class="sxs-lookup"><span data-stu-id="2f526-656">Enqueue Server / *lbrule3201*</span></span> |<span data-ttu-id="2f526-657">32 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="2f526-657">32<*InstanceNumber*></span></span> |<span data-ttu-id="2f526-658">3201</span><span class="sxs-lookup"><span data-stu-id="2f526-658">3201</span></span> |
| <span data-ttu-id="2f526-659">Ağ Geçidi sunucusu / *lbrule3301*</span><span class="sxs-lookup"><span data-stu-id="2f526-659">Gateway Server / *lbrule3301*</span></span> |<span data-ttu-id="2f526-660">33 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="2f526-660">33<*InstanceNumber*></span></span> |<span data-ttu-id="2f526-661">3301</span><span class="sxs-lookup"><span data-stu-id="2f526-661">3301</span></span> |
| <span data-ttu-id="2f526-662">Java ileti sunucusu / *lbrule3900*</span><span class="sxs-lookup"><span data-stu-id="2f526-662">Java Message Server / *lbrule3900*</span></span> |<span data-ttu-id="2f526-663">39 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="2f526-663">39<*InstanceNumber*></span></span> |<span data-ttu-id="2f526-664">3901</span><span class="sxs-lookup"><span data-stu-id="2f526-664">3901</span></span> |
| <span data-ttu-id="2f526-665">Sunucu HTTP iletisi / *Lbrule8101*</span><span class="sxs-lookup"><span data-stu-id="2f526-665">Message Server HTTP / *Lbrule8101*</span></span> |<span data-ttu-id="2f526-666">81 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="2f526-666">81<*InstanceNumber*></span></span> |<span data-ttu-id="2f526-667">8101</span><span class="sxs-lookup"><span data-stu-id="2f526-667">8101</span></span> |
| <span data-ttu-id="2f526-668">SAP başlangıç hizmet SCS HTTP / *Lbrule50113*</span><span class="sxs-lookup"><span data-stu-id="2f526-668">SAP Start Service SCS HTTP / *Lbrule50113*</span></span> |<span data-ttu-id="2f526-669">5 <*InstanceNumber*> 13</span><span class="sxs-lookup"><span data-stu-id="2f526-669">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="2f526-670">50113</span><span class="sxs-lookup"><span data-stu-id="2f526-670">50113</span></span> |
| <span data-ttu-id="2f526-671">SAP başlangıç hizmet SCS HTTPS / *Lbrule50114*</span><span class="sxs-lookup"><span data-stu-id="2f526-671">SAP Start Service SCS HTTPS / *Lbrule50114*</span></span> |<span data-ttu-id="2f526-672">5 <*InstanceNumber*> 14</span><span class="sxs-lookup"><span data-stu-id="2f526-672">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="2f526-673">50114</span><span class="sxs-lookup"><span data-stu-id="2f526-673">50114</span></span> |
| <span data-ttu-id="2f526-674">Sıraya alma çoğaltma / *Lbrule50116*</span><span class="sxs-lookup"><span data-stu-id="2f526-674">Enqueue Replication / *Lbrule50116*</span></span> |<span data-ttu-id="2f526-675">5 <*InstanceNumber*> 16</span><span class="sxs-lookup"><span data-stu-id="2f526-675">5<*InstanceNumber*>16</span></span> |<span data-ttu-id="2f526-676">50116</span><span class="sxs-lookup"><span data-stu-id="2f526-676">50116</span></span> |
| <span data-ttu-id="2f526-677">SAP başlangıç hizmeti ERS HTTP *Lbrule51113*</span><span class="sxs-lookup"><span data-stu-id="2f526-677">SAP Start Service ERS HTTP *Lbrule51113*</span></span> |<span data-ttu-id="2f526-678">5 <*InstanceNumber*> 13</span><span class="sxs-lookup"><span data-stu-id="2f526-678">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="2f526-679">51113</span><span class="sxs-lookup"><span data-stu-id="2f526-679">51113</span></span> |
| <span data-ttu-id="2f526-680">SAP başlangıç hizmeti ERS HTTP *Lbrule51114*</span><span class="sxs-lookup"><span data-stu-id="2f526-680">SAP Start Service ERS HTTP *Lbrule51114*</span></span> |<span data-ttu-id="2f526-681">5 <*InstanceNumber*> 14</span><span class="sxs-lookup"><span data-stu-id="2f526-681">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="2f526-682">51114</span><span class="sxs-lookup"><span data-stu-id="2f526-682">51114</span></span> |
| <span data-ttu-id="2f526-683">RM win *Lbrule5985*</span><span class="sxs-lookup"><span data-stu-id="2f526-683">Win RM *Lbrule5985*</span></span> | |<span data-ttu-id="2f526-684">5985</span><span class="sxs-lookup"><span data-stu-id="2f526-684">5985</span></span> |
| <span data-ttu-id="2f526-685">Dosya Paylaşımı *Lbrule445*</span><span class="sxs-lookup"><span data-stu-id="2f526-685">File Share *Lbrule445*</span></span> | |<span data-ttu-id="2f526-686">445</span><span class="sxs-lookup"><span data-stu-id="2f526-686">445</span></span> |

<span data-ttu-id="2f526-687">_**Tablo 2:** bağlantı noktası numaralarını hello SAP NetWeaver Java SCS örnekleri_</span><span class="sxs-lookup"><span data-stu-id="2f526-687">_**Table 2:** Port numbers of hello SAP NetWeaver Java SCS instances_</span></span>

![Şekil 15: varsayılan ASCS/SCS Yük Dengeleme kuralları hello Azure iç yük dengeleyici için][sap-ha-guide-figure-3004]

<span data-ttu-id="2f526-689">_**Şekil 15:** varsayılan ASCS/SCS Yük Dengeleme kuralları hello Azure iç yük dengeleyici için_</span><span class="sxs-lookup"><span data-stu-id="2f526-689">_**Figure 15:** Default ASCS/SCS load balancing rules for hello Azure internal load balancer_</span></span>

<span data-ttu-id="2f526-690">Merhaba yük dengeleyici hello IP adresi ayarlamak **pr1 lb dbms** toohello IP adresini hello DBMS örneğinin hello sanal ana bilgisayar adı.</span><span class="sxs-lookup"><span data-stu-id="2f526-690">Set hello IP address of hello load balancer **pr1-lb-dbms** toohello IP address of hello virtual host name of hello DBMS instance.</span></span>

### <span data-ttu-id="2f526-691"><a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a>Merhaba ASCS/SCS varsayılan Yük Dengeleme kuralları hello Azure iç yük dengeleyici için değiştirme</span><span class="sxs-lookup"><span data-stu-id="2f526-691"><a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a> Change hello ASCS/SCS default load balancing rules for hello Azure internal load balancer</span></span>

<span data-ttu-id="2f526-692">Merhaba SAP ASCS veya SCS örnekleri için toouse farklı numaraları istiyorsanız, hello adları ve değerleri kendi bağlantı noktalarının varsayılan değerleri değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f526-692">If you want toouse different numbers for hello SAP ASCS or SCS instances, you must change hello names and values of their ports from default values.</span></span>

1.  <span data-ttu-id="2f526-693">Hello Azure portal, seçin  **<* SID*> - lb - ascs yük dengeleyici ** > **Yük Dengeleme kuralları**.</span><span class="sxs-lookup"><span data-stu-id="2f526-693">In hello Azure portal, select **<*SID*>-lb-ascs load balancer** > **Load Balancing Rules**.</span></span>
2.  <span data-ttu-id="2f526-694">Tüm Yük Dengeleme toohello SAP ASCS veya SCS örnek ait kuralları için bu değerleri değiştirin:</span><span class="sxs-lookup"><span data-stu-id="2f526-694">For all load balancing rules that belong toohello SAP ASCS or SCS instance, change these values:</span></span>

  * <span data-ttu-id="2f526-695">Ad</span><span class="sxs-lookup"><span data-stu-id="2f526-695">Name</span></span>
  * <span data-ttu-id="2f526-696">Bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="2f526-696">Port</span></span>
  * <span data-ttu-id="2f526-697">Arka uç bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="2f526-697">Back-end port</span></span>

  <span data-ttu-id="2f526-698">Örneğin, toochange hello varsayılan ASCS örneği numarasından 00 too31 istiyorsanız, Tablo 1'de listelenen tüm bağlantı noktaları toomake hello değişiklikleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f526-698">For example, if you want toochange hello default ASCS instance number from 00 too31, you need toomake hello changes for all ports listed in Table 1.</span></span>

  <span data-ttu-id="2f526-699">Bağlantı noktası için bir güncelleştirme örneği *lbrule3200*.</span><span class="sxs-lookup"><span data-stu-id="2f526-699">Here's an example of an update for port *lbrule3200*.</span></span>

  ![Şekil 16: Merhaba ASCS/SCS varsayılan Yük Dengeleme kuralları hello Azure iç yük dengeleyici için değiştirme][sap-ha-guide-figure-3005]

  <span data-ttu-id="2f526-701">_**Şekil 16:** değişiklik hello ASCS/SCS varsayılan Yük Dengeleme kuralları hello Azure iç yük dengeleyici için_</span><span class="sxs-lookup"><span data-stu-id="2f526-701">_**Figure 16:** Change hello ASCS/SCS default load balancing rules for hello Azure internal load balancer_</span></span>

### <span data-ttu-id="2f526-702"><a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a>Windows sanal makineleri toohello etki alanı ekleme</span><span class="sxs-lookup"><span data-stu-id="2f526-702"><a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a> Add Windows virtual machines toohello domain</span></span>

<span data-ttu-id="2f526-703">Bir statik IP adresi toohello sanal makineleri atadıktan sonra hello sanal makineleri toohello etki alanına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2f526-703">After you assign a static IP address toohello virtual machines, add hello virtual machines toohello domain.</span></span>

![Şekil 17: bir sanal makine tooa etki alanına ekleme][sap-ha-guide-figure-3006]

<span data-ttu-id="2f526-705">_**Şekil 17:** bir sanal makine tooa etki alanına ekleme_</span><span class="sxs-lookup"><span data-stu-id="2f526-705">_**Figure 17:** Add a virtual machine tooa domain_</span></span>

### <span data-ttu-id="2f526-706"><a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a>Kayıt defteri girdilerini hello SAP ASCS/SCS örneği her iki küme düğümleri üzerinde ekleyin</span><span class="sxs-lookup"><span data-stu-id="2f526-706"><a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a> Add registry entries on both cluster nodes of hello SAP ASCS/SCS instance</span></span>

<span data-ttu-id="2f526-707">Azure yük dengeleyici hello bağlantıları ayarlanmış bir süre boyunca boşta olduğunda kapanır bağlantıları (boşta zaman aşımı) zaman bir iç yük dengeleyici sahiptir.</span><span class="sxs-lookup"><span data-stu-id="2f526-707">Azure Load Balancer has an internal load balancer that closes connections when hello connections are idle for a set period of time (an idle timeout).</span></span> <span data-ttu-id="2f526-708">Merhaba ilk sıraya alma/dequeue gereksinimlerini toobe gönderilen istek hemen SAP iş iletişim örnekleri açık bağlantıları toohello SAP sıraya alma işlemlerinde işleyin.</span><span class="sxs-lookup"><span data-stu-id="2f526-708">SAP work processes in dialog instances open connections toohello SAP enqueue process as soon as hello first enqueue/dequeue request needs toobe sent.</span></span> <span data-ttu-id="2f526-709">Bu bağlantılar genellikle hello iş işlemi kadar kurulan kalmasını veya hello sıraya alma işlemi yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="2f526-709">These connections usually remain established until hello work process or hello enqueue process restarts.</span></span> <span data-ttu-id="2f526-710">Ancak, belirlenen süre Hello bağlantı boşta kalırsa Azure iç yük dengeleyici kapanır hello bağlantıları hello.</span><span class="sxs-lookup"><span data-stu-id="2f526-710">However, if hello connection is idle for a set period of time, hello Azure internal load balancer closes hello connections.</span></span> <span data-ttu-id="2f526-711">Artık yoksa hello SAP iş işlemi hello bağlantı toohello sıraya alma işlemini yeniden kurar çünkü bu bir sorun değildir.</span><span class="sxs-lookup"><span data-stu-id="2f526-711">This isn't a problem because hello SAP work process reestablishes hello connection toohello enqueue process if it no longer exists.</span></span> <span data-ttu-id="2f526-712">Bu etkinlikler SAP işlemlerin hello Geliştirici izlemeleri belgelenen, ancak bunlar büyük miktarda ek içerik bu izlemeler oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2f526-712">These activities are documented in hello developer traces of SAP processes, but they create a large amount of extra content in those traces.</span></span> <span data-ttu-id="2f526-713">İyi bir fikir toochange hello TCP/IP'yi olan `KeepAliveTime` ve `KeepAliveInterval` her iki küme düğümlerinde.</span><span class="sxs-lookup"><span data-stu-id="2f526-713">It's a good idea toochange hello TCP/IP `KeepAliveTime` and `KeepAliveInterval` on both cluster nodes.</span></span> <span data-ttu-id="2f526-714">Bu değişiklikler hello TCP/IP parametreleri parametrelerle hello makalenin sonraki bölümlerinde açıklanan SAP profili ile birleştirin.</span><span class="sxs-lookup"><span data-stu-id="2f526-714">Combine these changes in hello TCP/IP parameters with SAP profile parameters, described later in hello article.</span></span>

<span data-ttu-id="2f526-715">tooadd kayıt defteri girdileri hello SAP ASCS/SCS örneğinin her iki küme düğümlerinde ilk olarak, bu Windows kayıt defteri girdileri SAP ASCS/SCS için hem Windows Küme düğümlerinde ekleyin:</span><span class="sxs-lookup"><span data-stu-id="2f526-715">tooadd registry entries on both cluster nodes of hello SAP ASCS/SCS instance, first, add these Windows registry entries on both Windows cluster nodes for SAP ASCS/SCS:</span></span>

| <span data-ttu-id="2f526-716">Yol</span><span class="sxs-lookup"><span data-stu-id="2f526-716">Path</span></span> | <span data-ttu-id="2f526-717">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span><span class="sxs-lookup"><span data-stu-id="2f526-717">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span></span> |
| --- | --- |
| <span data-ttu-id="2f526-718">Değişken adı</span><span class="sxs-lookup"><span data-stu-id="2f526-718">Variable name</span></span> |`KeepAliveTime` |
| <span data-ttu-id="2f526-719">Değişken türü</span><span class="sxs-lookup"><span data-stu-id="2f526-719">Variable type</span></span> |<span data-ttu-id="2f526-720">REG_DWORD (ondalık)</span><span class="sxs-lookup"><span data-stu-id="2f526-720">REG_DWORD (Decimal)</span></span> |
| <span data-ttu-id="2f526-721">Değer</span><span class="sxs-lookup"><span data-stu-id="2f526-721">Value</span></span> |<span data-ttu-id="2f526-722">120000</span><span class="sxs-lookup"><span data-stu-id="2f526-722">120000</span></span> |
| <span data-ttu-id="2f526-723">Bağlantı toodocumentation</span><span class="sxs-lookup"><span data-stu-id="2f526-723">Link toodocumentation</span></span> |[<span data-ttu-id="2f526-724">https://technet.microsoft.com/en-us/library/cc957549.aspx</span><span class="sxs-lookup"><span data-stu-id="2f526-724">https://technet.microsoft.com/en-us/library/cc957549.aspx</span></span>](https://technet.microsoft.com/en-us/library/cc957549.aspx) |

<span data-ttu-id="2f526-725">_**Tablo 3:** değişiklik hello ilk TCP/IP'yi parametresi_</span><span class="sxs-lookup"><span data-stu-id="2f526-725">_**Table 3:** Change hello first TCP/IP parameter_</span></span>

<span data-ttu-id="2f526-726">Daha sonra bu Windows kayıt defteri girdileri SAP ASCS/SCS için hem Windows küme düğümlerine ekleyin:</span><span class="sxs-lookup"><span data-stu-id="2f526-726">Then, add this Windows registry entries on both Windows cluster nodes for SAP ASCS/SCS:</span></span>

| <span data-ttu-id="2f526-727">Yol</span><span class="sxs-lookup"><span data-stu-id="2f526-727">Path</span></span> | <span data-ttu-id="2f526-728">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span><span class="sxs-lookup"><span data-stu-id="2f526-728">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span></span> |
| --- | --- |
| <span data-ttu-id="2f526-729">Değişken adı</span><span class="sxs-lookup"><span data-stu-id="2f526-729">Variable name</span></span> |`KeepAliveInterval` |
| <span data-ttu-id="2f526-730">Değişken türü</span><span class="sxs-lookup"><span data-stu-id="2f526-730">Variable type</span></span> |<span data-ttu-id="2f526-731">REG_DWORD (ondalık)</span><span class="sxs-lookup"><span data-stu-id="2f526-731">REG_DWORD (Decimal)</span></span> |
| <span data-ttu-id="2f526-732">Değer</span><span class="sxs-lookup"><span data-stu-id="2f526-732">Value</span></span> |<span data-ttu-id="2f526-733">120000</span><span class="sxs-lookup"><span data-stu-id="2f526-733">120000</span></span> |
| <span data-ttu-id="2f526-734">Bağlantı toodocumentation</span><span class="sxs-lookup"><span data-stu-id="2f526-734">Link toodocumentation</span></span> |[<span data-ttu-id="2f526-735">https://technet.microsoft.com/en-us/library/cc957548.aspx</span><span class="sxs-lookup"><span data-stu-id="2f526-735">https://technet.microsoft.com/en-us/library/cc957548.aspx</span></span>](https://technet.microsoft.com/en-us/library/cc957548.aspx) |

<span data-ttu-id="2f526-736">_**Tablo 4:** değişiklik hello ikinci TCP/IP'yi parametresi_</span><span class="sxs-lookup"><span data-stu-id="2f526-736">_**Table 4:** Change hello second TCP/IP parameter_</span></span>

<span data-ttu-id="2f526-737">**tooapply hello değişiklikler, her iki küme düğümünü yeniden**.</span><span class="sxs-lookup"><span data-stu-id="2f526-737">**tooapply hello changes, restart both cluster nodes**.</span></span>

### <span data-ttu-id="2f526-738"><a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a>Bir Windows Server Yük Devretme Kümelemesi küme SAP ASCS/SCS örneği için ayarlama</span><span class="sxs-lookup"><span data-stu-id="2f526-738"><a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a> Set up a Windows Server Failover Clustering cluster for an SAP ASCS/SCS instance</span></span>

<span data-ttu-id="2f526-739">Bir Windows Server Yük Devretme Kümelemesi küme SAP ASCS/SCS örneği için ayarlama, bu görevleri içerir:</span><span class="sxs-lookup"><span data-stu-id="2f526-739">Setting up a Windows Server Failover Clustering cluster for an SAP ASCS/SCS instance involves these tasks:</span></span>

- <span data-ttu-id="2f526-740">Bir küme yapılandırmasında Hello küme düğümleri toplama</span><span class="sxs-lookup"><span data-stu-id="2f526-740">Collecting hello cluster nodes in a cluster configuration</span></span>
- <span data-ttu-id="2f526-741">Bir küme dosya paylaşımı tanığı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="2f526-741">Configuring a cluster file share witness</span></span>

#### <span data-ttu-id="2f526-742"><a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a>Bir küme yapılandırmasında Hello küme düğümleri Topla</span><span class="sxs-lookup"><span data-stu-id="2f526-742"><a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a> Collect hello cluster nodes in a cluster configuration</span></span>

1.  <span data-ttu-id="2f526-743">Hello Ekle rol ve Özellik Ekleme Sihirbazı, Yük Devretme Kümelemesi tooboth küme düğümlerine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2f526-743">In hello Add Role and Features Wizard, add failover clustering tooboth cluster nodes.</span></span>
2.  <span data-ttu-id="2f526-744">Merhaba yük devretme kümesini yedeklerken, yük devretme kümesi Yöneticisi'ni kullanarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="2f526-744">Set up hello failover cluster by using Failover Cluster Manager.</span></span> <span data-ttu-id="2f526-745">Yük Devretme Kümesi Yöneticisi'nde seçin **küme oluşturma**ve ardından yalnızca hello ilk küme, düğümü A. hello adı ekleyin Merhaba İkinci düğüm henüz eklemeyin; bir sonraki adımda hello İkinci düğüm ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="2f526-745">In Failover Cluster Manager, select **Create Cluster**, and then add only hello name of hello first cluster, node A. Do not add hello second node yet; you'll add hello second node in a later step.</span></span>

  ![Şekil 18: hello sunucusunu veya hello ilk küme düğümüne sanal makine adı ekleyin][sap-ha-guide-figure-3007]

  <span data-ttu-id="2f526-747">_**Şekil 18:** hello ilk küme düğümünün Ekle hello sunucu veya sanal makine adı_</span><span class="sxs-lookup"><span data-stu-id="2f526-747">_**Figure 18:** Add hello server or virtual machine name of hello first cluster node_</span></span>

3.  <span data-ttu-id="2f526-748">Merhaba ağ (sanal ana bilgisayar adı) hello kümenin adını girin.</span><span class="sxs-lookup"><span data-stu-id="2f526-748">Enter hello network name (virtual host name) of hello cluster.</span></span>

  ![Şekil 19: hello küme adını girin][sap-ha-guide-figure-3008]

  <span data-ttu-id="2f526-750">_**Şekil 19:** hello küme adını girin_</span><span class="sxs-lookup"><span data-stu-id="2f526-750">_**Figure 19:** Enter hello cluster name_</span></span>

4.  <span data-ttu-id="2f526-751">Merhaba küme oluşturduktan sonra bir küme doğrulama testi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2f526-751">After you've created hello cluster, run a cluster validation test.</span></span>

  ![Şekil 20: hello küme doğrulama denetimini Çalıştır][sap-ha-guide-figure-3009]

  <span data-ttu-id="2f526-753">_**Şekil 20:** hello küme doğrulama denetimini Çalıştır_</span><span class="sxs-lookup"><span data-stu-id="2f526-753">_**Figure 20:** Run hello cluster validation check_</span></span>

  <span data-ttu-id="2f526-754">Bu noktada hello işleminde disklerle ilgili tüm uyarılar yoksayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f526-754">You can ignore any warnings about disks at this point in hello process.</span></span> <span data-ttu-id="2f526-755">Bir dosya paylaşımı tanığı ve hello SIOS diskler daha sonra paylaşılan ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="2f526-755">You'll add a file share witness and hello SIOS shared disks later.</span></span> <span data-ttu-id="2f526-756">Bu aşamada, bir çekirdek sahibi olma hakkında tooworry gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="2f526-756">At this stage, you don't need tooworry about having a quorum.</span></span>

  ![Şekil 21: Çekirdek disk bulunamadı][sap-ha-guide-figure-3010]

  <span data-ttu-id="2f526-758">_**Şekil 21:** çekirdek disk bulunamadı_</span><span class="sxs-lookup"><span data-stu-id="2f526-758">_**Figure 21:** No quorum disk is found_</span></span>

  ![Şekil 22: Çekirdek küme kaynağının yeni bir IP adresi gerekiyor.][sap-ha-guide-figure-3011]

  <span data-ttu-id="2f526-760">_**Şekil 22:** çekirdek küme kaynağının yeni bir IP adresi gerekiyor_</span><span class="sxs-lookup"><span data-stu-id="2f526-760">_**Figure 22:** Core cluster resource needs a new IP address_</span></span>

5.  <span data-ttu-id="2f526-761">Merhaba çekirdek Küme hizmeti Hello IP adresini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="2f526-761">Change hello IP address of hello core cluster service.</span></span> <span data-ttu-id="2f526-762">Başlangıç IP adresi hello çekirdek Küme hizmetinin, değiştirene kadar tooone hello sanal makine düğümlerinin hello sunucusunun hello IP adresini işaret ettiğinden hello küme başlatılamıyor.</span><span class="sxs-lookup"><span data-stu-id="2f526-762">hello cluster can't start until you change hello IP address of hello core cluster service, because hello IP address of hello server points tooone of hello virtual machine nodes.</span></span> <span data-ttu-id="2f526-763">Merhaba üzerinde bunu **özellikleri** hello çekirdek küme hizmetin IP kaynak sayfası.</span><span class="sxs-lookup"><span data-stu-id="2f526-763">Do this on hello **Properties** page of hello core cluster service's IP resource.</span></span>

  <span data-ttu-id="2f526-764">Örneğin, bir IP adresi tooassign ihtiyacımız (örneğimizde **10.0.0.42**) hello küme sanal ana bilgisayar adı için **pr1 ascs VIR**.</span><span class="sxs-lookup"><span data-stu-id="2f526-764">For example, we need tooassign an IP address (in our example, **10.0.0.42**) for hello cluster virtual host name **pr1-ascs-vir**.</span></span>

  ![Şekil 23: hello Özellikleri iletişim kutusunda hello IP adresini değiştirme][sap-ha-guide-figure-3012]

  <span data-ttu-id="2f526-766">_**Şekil 23:** hello içinde **özellikleri** iletişim kutusu, hello IP adresini Değiştir_</span><span class="sxs-lookup"><span data-stu-id="2f526-766">_**Figure 23:** In hello **Properties** dialog box, change hello IP address_</span></span>

  ![Şekil 24: hello küme için ayrılmış başlangıç IP adresi atayın][sap-ha-guide-figure-3013]

  <span data-ttu-id="2f526-768">_**Şekil 24:** hello küme için ayrılmış başlangıç IP adresi atayın_</span><span class="sxs-lookup"><span data-stu-id="2f526-768">_**Figure 24:** Assign hello IP address that is reserved for hello cluster_</span></span>

6.  <span data-ttu-id="2f526-769">Merhaba küme sanal ana bilgisayar adı çevrimiçi duruma getirin.</span><span class="sxs-lookup"><span data-stu-id="2f526-769">Bring hello cluster virtual host name online.</span></span>

  ![Şekil 25: Küme çekirdek hizmeti çalışır durumda ve çalıştığından ve hello ile IP adresini düzeltin][sap-ha-guide-figure-3014]

  <span data-ttu-id="2f526-771">_**Şekil 25:** çalışan ile Merhaba IP adresini düzeltin ve küme çekirdek hizmetidir ayarlama_</span><span class="sxs-lookup"><span data-stu-id="2f526-771">_**Figure 25:** Cluster core service is up and running, and with hello correct IP address_</span></span>

7.  <span data-ttu-id="2f526-772">Merhaba ikinci küme düğümünü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2f526-772">Add hello second cluster node.</span></span>

  <span data-ttu-id="2f526-773">Merhaba çekirdek Küme hizmeti çalışır durumda olduğundan, hello İkinci düğüm ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f526-773">Now that hello core cluster service is up and running, you can add hello second cluster node.</span></span>

  ![Şekil 26: hello İkinci düğüm ekleme][sap-ha-guide-figure-3015]

  <span data-ttu-id="2f526-775">_**Şekil 26:** Ekle hello ikinci küme düğümü_</span><span class="sxs-lookup"><span data-stu-id="2f526-775">_**Figure 26:** Add hello second cluster node_</span></span>

8.  <span data-ttu-id="2f526-776">Merhaba ikinci küme düğümü konağı için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="2f526-776">Enter a name for hello second cluster node host.</span></span>

  ![Şekil 27: hello ikinci küme düğümü ana bilgisayar adı girin][sap-ha-guide-figure-3016]

  <span data-ttu-id="2f526-778">_**Şekil 27:** hello ikinci küme düğümü ana bilgisayar adını girin_</span><span class="sxs-lookup"><span data-stu-id="2f526-778">_**Figure 27:** Enter hello second cluster node host name_</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="2f526-779">Bu hello denetleyin **tüm uygun depolama toohello küme eklemek** onay kutusu **değil** seçili.</span><span class="sxs-lookup"><span data-stu-id="2f526-779">Be sure that hello **Add all eligible storage toohello cluster** check box is **NOT** selected.</span></span>  
  >
  >

  ![Şekil 28: hello onay kutusunu işaretlemeyin][sap-ha-guide-figure-3017]

  <span data-ttu-id="2f526-781">_**Şekil 28:** yapmak **değil** hello onay kutusunu seçin_</span><span class="sxs-lookup"><span data-stu-id="2f526-781">_**Figure 28:** Do **not** select hello check box_</span></span>

  <span data-ttu-id="2f526-782">Çekirdek ve diskleri ilgili uyarılar yoksayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f526-782">You can ignore warnings about quorum and disks.</span></span> <span data-ttu-id="2f526-783">Bölümünde açıklandığı gibi daha sonra hello çekirdek ve Paylaşım hello disk komutunu ayarlarız [SIOS DataKeeper Cluster Edition yükleme SAP ASCS/SCS küme paylaşım diski için][sap-ha-guide-8.12.3].</span><span class="sxs-lookup"><span data-stu-id="2f526-783">You'll set hello quorum and share hello disk later, as described in [Installing SIOS DataKeeper Cluster Edition for SAP ASCS/SCS cluster share disk][sap-ha-guide-8.12.3].</span></span>

  ![Şekil 29: hello disk çekirdek ilgili uyarılar yoksay][sap-ha-guide-figure-3018]

  <span data-ttu-id="2f526-785">_**Şekil 29:** hello disk çekirdek ilgili uyarılar yoksay_</span><span class="sxs-lookup"><span data-stu-id="2f526-785">_**Figure 29:** Ignore warnings about hello disk quorum_</span></span>


#### <span data-ttu-id="2f526-786"><a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a>Bir küme dosya paylaşımı tanığı Yapılandır</span><span class="sxs-lookup"><span data-stu-id="2f526-786"><a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a> Configure a cluster file share witness</span></span>

<span data-ttu-id="2f526-787">Bir küme dosya paylaşımı tanığı yapılandırma, bu görevleri içerir:</span><span class="sxs-lookup"><span data-stu-id="2f526-787">Configuring a cluster file share witness involves these tasks:</span></span>

- <span data-ttu-id="2f526-788">Bir dosya paylaşımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2f526-788">Creating a file share</span></span>
- <span data-ttu-id="2f526-789">Yük Devretme Kümesi Yöneticisi'nde Hello dosya paylaşım tanığı çekirdek ayarlama</span><span class="sxs-lookup"><span data-stu-id="2f526-789">Setting hello file share witness quorum in Failover Cluster Manager</span></span>

##### <span data-ttu-id="2f526-790"><a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a>Dosya paylaşımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2f526-790"><a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a> Create a file share</span></span>

1.  <span data-ttu-id="2f526-791">Dosya paylaşım tanığı yerine bir çekirdek diski seçin.</span><span class="sxs-lookup"><span data-stu-id="2f526-791">Select a file share witness instead of a quorum disk.</span></span> <span data-ttu-id="2f526-792">Bu seçenek SIOS DataKeeper destekler.</span><span class="sxs-lookup"><span data-stu-id="2f526-792">SIOS DataKeeper supports this option.</span></span>

  <span data-ttu-id="2f526-793">Bu makalede Hello örneklerde, Azure'da çalışan hello Active Directory DNS sunucusu hello dosya paylaşım tanığı açıktır.</span><span class="sxs-lookup"><span data-stu-id="2f526-793">In hello examples in this article, hello file share witness is on hello Active Directory/DNS server that is running in Azure.</span></span> <span data-ttu-id="2f526-794">Merhaba dosya paylaşım tanığı olarak adlandırılır **domcontr 0**.</span><span class="sxs-lookup"><span data-stu-id="2f526-794">hello file share witness is called **domcontr-0**.</span></span> <span data-ttu-id="2f526-795">Bir VPN bağlantısı tooAzure (aracılığıyla, siteden siteye VPN veya Azure ExpressRoute) yapılandırılmış çünkü Active Directory/Hizmeti şirket içi ve uygun toorun bir dosya değil. DNS sunucunuzun Tanık paylaşır.</span><span class="sxs-lookup"><span data-stu-id="2f526-795">Because you would have configured a VPN connection tooAzure (via Site-to-Site VPN or Azure ExpressRoute), your Active Directory/DNS service is on-premises and isn't suitable toorun a file share witness.</span></span>

  > [!NOTE]
  > <span data-ttu-id="2f526-796">Yalnızca şirket içi Active Directory DNS hizmeti çalışıyorsa, dosya paylaşım tanığı hello Active Directory/DNS Windows işletim sistemlerinde, şirket içi çalışan yapılandırmayın.</span><span class="sxs-lookup"><span data-stu-id="2f526-796">If your Active Directory/DNS service runs only on-premises, don't configure your file share witness on hello Active Directory/DNS Windows operating system that is running on-premises.</span></span> <span data-ttu-id="2f526-797">Azure ve Active Directory DNS şirket içi çalışan küme düğümleri arasındaki ağ gecikmesi çok büyük ve bağlantı sorunlarına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="2f526-797">Network latency between cluster nodes running in Azure and Active Directory/DNS on-premises might be too large and cause connectivity issues.</span></span> <span data-ttu-id="2f526-798">Emin tooconfigure hello dosya paylaşım tanığı Kapat toohello küme düğümünde çalışan bir Azure sanal makinesi üzerinde olabilir.</span><span class="sxs-lookup"><span data-stu-id="2f526-798">Be sure tooconfigure hello file share witness on an Azure virtual machine that is running close toohello cluster node.</span></span>  
  >
  >

  <span data-ttu-id="2f526-799">Merhaba çekirdek sürücüde en az 1024 MB boş disk alanı gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f526-799">hello quorum drive needs at least 1,024 MB of free space.</span></span> <span data-ttu-id="2f526-800">2.048 MB boş disk alanı hello çekirdek sürücüsü için öneririz.</span><span class="sxs-lookup"><span data-stu-id="2f526-800">We recommend 2,048 MB of free space for hello quorum drive.</span></span>

2.  <span data-ttu-id="2f526-801">Merhaba küme adı nesnesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2f526-801">Add hello cluster name object.</span></span>

  ![Şekil 30: hello paylaşımı hello küme adı nesnesi için hello izinleri atayın][sap-ha-guide-figure-3019]

  <span data-ttu-id="2f526-803">_**Şekil 30:** hello küme adı nesnesi için hello paylaşımındaki hello izinler atama_</span><span class="sxs-lookup"><span data-stu-id="2f526-803">_**Figure 30:** Assign hello permissions on hello share for hello cluster name object_</span></span>

  <span data-ttu-id="2f526-804">Merhaba izinleri hello paylaşımı hello küme adı nesnesi için hello yetkilisi toochange veri dahil emin olun (örneğimizde **pr1 ascs VIR$**).</span><span class="sxs-lookup"><span data-stu-id="2f526-804">Be sure that hello permissions include hello authority toochange data in hello share for hello cluster name object (in our example, **pr1-ascs-vir$**).</span></span>

3.  <span data-ttu-id="2f526-805">tooadd hello küme adı nesnesi toohello listesinde **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="2f526-805">tooadd hello cluster name object toohello list, select **Add**.</span></span> <span data-ttu-id="2f526-806">Merhaba filtre toocheck bilgisayar nesnelerini, toplama toothose şekil 31'de gösterilen için değiştirin.</span><span class="sxs-lookup"><span data-stu-id="2f526-806">Change hello filter toocheck for computer objects, in addition toothose shown in Figure 31.</span></span>

  ![Şekil 31: Değişiklik hello nesne türleri tooinclude bilgisayarlar][sap-ha-guide-figure-3020]

  <span data-ttu-id="2f526-808">_**Şekil 31:** değiştirmek hello nesne türleri tooinclude bilgisayarlar_</span><span class="sxs-lookup"><span data-stu-id="2f526-808">_**Figure 31:** Change hello Object Types tooinclude computers_</span></span>

  ![Şekil 32: hello bilgisayarlar onay kutusunu seçin][sap-ha-guide-figure-3021]

  <span data-ttu-id="2f526-810">_**Şekil 32:** Select hello **bilgisayarlar** onay kutusu_</span><span class="sxs-lookup"><span data-stu-id="2f526-810">_**Figure 32:** Select hello **Computers** check box_</span></span>

4.  <span data-ttu-id="2f526-811">Şekil 31'de gösterildiği gibi hello küme adı nesnesi girin.</span><span class="sxs-lookup"><span data-stu-id="2f526-811">Enter hello cluster name object as shown in Figure 31.</span></span> <span data-ttu-id="2f526-812">Merhaba kaydı zaten oluşturulduğundan, Şekil 30 gösterildiği gibi hello izinleri değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f526-812">Because hello record has already been created, you can change hello permissions, as shown in Figure 30.</span></span>

5.  <span data-ttu-id="2f526-813">Select hello **güvenlik** hello paylaşım ayarlayın ve ardından sekmesinde daha ayrıntılı hello küme adı nesnesi için izinleri.</span><span class="sxs-lookup"><span data-stu-id="2f526-813">Select hello **Security** tab of hello share, and then set more detailed permissions for hello cluster name object.</span></span>

  ![Şekil 33: Hello güvenlik özelliklerini ayarla hello dosya paylaşımı çekirdeğe hello küme adı nesnesi][sap-ha-guide-figure-3022]

  <span data-ttu-id="2f526-815">_**Şekil 33:** hello dosya paylaşımı çekirdek üzerinde hello küme adı nesnesi için hello güvenlik özniteliklerini ayarlama_</span><span class="sxs-lookup"><span data-stu-id="2f526-815">_**Figure 33:** Set hello security attributes for hello cluster name object on hello file share quorum_</span></span>

##### <span data-ttu-id="2f526-816"><a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a>Yük Devretme Kümesi Yöneticisi'nde Hello dosya paylaşım tanığı çekirdek ayarlayın</span><span class="sxs-lookup"><span data-stu-id="2f526-816"><a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a> Set hello file share witness quorum in Failover Cluster Manager</span></span>

1.  <span data-ttu-id="2f526-817">Merhaba yapılandırma çekirdek Ayarlama Sihirbazı'nı açın.</span><span class="sxs-lookup"><span data-stu-id="2f526-817">Open hello Configure Quorum Setting Wizard.</span></span>

  ![Şekil 34: hello yapılandırma küme çekirdeği ayar Sihirbazı Başlat][sap-ha-guide-figure-3023]

  <span data-ttu-id="2f526-819">_**Şekil 34:** başlangıç hello küme çekirdeği yapılandırma ayarı Sihirbazı_</span><span class="sxs-lookup"><span data-stu-id="2f526-819">_**Figure 34:** Start hello Configure Cluster Quorum Setting Wizard_</span></span>

2.  <span data-ttu-id="2f526-820">Merhaba üzerinde **seçin Çekirdek yapılandırmasını** sayfasında **hello çekirdek tanığı Seç**.</span><span class="sxs-lookup"><span data-stu-id="2f526-820">On hello **Select Quorum Configuration** page, select **Select hello quorum witness**.</span></span>

  ![Şekil 35: aralarından seçim yapabileceğiniz Çekirdek yapılandırmaları][sap-ha-guide-figure-3024]

  <span data-ttu-id="2f526-822">_**Şekil 35:** seçim yapabileceğiniz Çekirdek yapılandırmaları_</span><span class="sxs-lookup"><span data-stu-id="2f526-822">_**Figure 35:** Quorum configurations you can choose from_</span></span>

3.  <span data-ttu-id="2f526-823">Merhaba üzerinde **çekirdek tanığı Seç** sayfasında **bir dosya paylaşımı tanığı Yapılandır**.</span><span class="sxs-lookup"><span data-stu-id="2f526-823">On hello **Select Quorum Witness** page, select **Configure a file share witness**.</span></span>

  ![Şekil 36: Select hello dosya paylaşım tanığı][sap-ha-guide-figure-3025]

  <span data-ttu-id="2f526-825">_**Şekil 36:** hello dosya paylaşım tanığı seçin_</span><span class="sxs-lookup"><span data-stu-id="2f526-825">_**Figure 36:** Select hello file share witness_</span></span>

4.  <span data-ttu-id="2f526-826">Merhaba UNC yolu toohello dosya paylaşımı girin (örneğimizde \\domcontr 0\FSW).</span><span class="sxs-lookup"><span data-stu-id="2f526-826">Enter hello UNC path toohello file share (in our example, \\domcontr-0\FSW).</span></span> <span data-ttu-id="2f526-827">toosee hello değişiklikleri yapabilirsiniz, select listesi **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="2f526-827">toosee a list of hello changes you can make, select **Next**.</span></span>

  ![Şekil 37: hello Tanık paylaşımı için hello dosya paylaşım konumunu tanımlayın][sap-ha-guide-figure-3026]

  <span data-ttu-id="2f526-829">_**Şekil 37:** hello Tanık paylaşımı için hello dosya paylaşım konumunu tanımlayın_</span><span class="sxs-lookup"><span data-stu-id="2f526-829">_**Figure 37:** Define hello file share location for hello witness share_</span></span>

5.  <span data-ttu-id="2f526-830">Seçin ve ardından hello değişiklikleri **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="2f526-830">Select hello changes you want, and then select **Next**.</span></span> <span data-ttu-id="2f526-831">Toosuccessfully ihtiyacınız şekil 38 gösterildiği gibi hello küme yapılandırmasını yeniden yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="2f526-831">You need toosuccessfully reconfigure hello cluster configuration as shown in Figure 38.</span></span>  

  ![Şekil 38: hello küme yeniden yapılandırılması onayı][sap-ha-guide-figure-3027]

  <span data-ttu-id="2f526-833">_**Şekil 38:** hello küme yeniden yapılandırılması onayı_</span><span class="sxs-lookup"><span data-stu-id="2f526-833">_**Figure 38:** Confirmation that you've reconfigured hello cluster_</span></span>

<span data-ttu-id="2f526-834">Hello Windows Yük devretme kümesi başarıyla yükledikten sonra değişiklikler toosome eşikleri tooadapt yük devretme algılama tooconditions Azure'da yapılan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f526-834">After installing hello Windows Failover Cluster successfully, changes need toobe made toosome thresholds tooadapt failover detection tooconditions in Azure.</span></span> <span data-ttu-id="2f526-835">Merhaba değiştirilen parametreleri toobe belgelenmiştir bu blog: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/.</span><span class="sxs-lookup"><span data-stu-id="2f526-835">hello parameters toobe changed are documented in this blog: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/ .</span></span> <span data-ttu-id="2f526-836">Merhaba yapı, iki VM varsayarak Windows Küme yapılandırması ASCS/SCS içindir aynı alt ağda Merhaba, hello aşağıdaki parametreleri değiştirilen toobe toothese değerlerine ihtiyacı vardır:</span><span class="sxs-lookup"><span data-stu-id="2f526-836">Assuming that your two VMs that build hello Windows Cluster Configuration for ASCS/SCS are in hello same SubNet, hello following parameters need toobe changed toothese values:</span></span>
- <span data-ttu-id="2f526-837">SameSubNetDelay = 2</span><span class="sxs-lookup"><span data-stu-id="2f526-837">SameSubNetDelay = 2</span></span>
- <span data-ttu-id="2f526-838">SameSubNetThreshold = 15</span><span class="sxs-lookup"><span data-stu-id="2f526-838">SameSubNetThreshold = 15</span></span>

<span data-ttu-id="2f526-839">Bu ayarları müşterilerle test ve iyi güvenliğinin aşılmasına toobe yeterince esnektir hello bir tarafta sağlanan.</span><span class="sxs-lookup"><span data-stu-id="2f526-839">These settings were tested with customers and provided a good compromise toobe resilient enough on hello one side.</span></span> <span data-ttu-id="2f526-840">Üzerinde Hello diğer yandan bu ayarları hızlı gerçek hata koşulları SAP yazılım veya düğüm/VM hatasında yeterli yük sağlama.</span><span class="sxs-lookup"><span data-stu-id="2f526-840">On hello other hand those settings were providing fast enough failover in real error conditions on SAP software or node/VM failure.</span></span> 

### <span data-ttu-id="2f526-841"><a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a>Merhaba SAP ASCS/SCS küme paylaşım disk için SIOS DataKeeper küme Edition'ı yükleme</span><span class="sxs-lookup"><span data-stu-id="2f526-841"><a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a> Install SIOS DataKeeper Cluster Edition for hello SAP ASCS/SCS cluster share disk</span></span>

<span data-ttu-id="2f526-842">Artık Azure üzerinde çalışan bir Windows Server Yük Devretme Kümelemesi yapılandırma vardır.</span><span class="sxs-lookup"><span data-stu-id="2f526-842">You now have a working Windows Server Failover Clustering configuration in Azure.</span></span> <span data-ttu-id="2f526-843">Ancak, tooinstall SAP ASCS/SCS örneği bir paylaşılan disk kaynağı gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f526-843">But, tooinstall an SAP ASCS/SCS instance, you need a shared disk resource.</span></span> <span data-ttu-id="2f526-844">Azure'da hello paylaşılan disk kaynakları ihtiyacınız oluşturulamıyor.</span><span class="sxs-lookup"><span data-stu-id="2f526-844">You cannot create hello shared disk resources you need in Azure.</span></span> <span data-ttu-id="2f526-845">SIOS DataKeeper Cluster Edition toocreate paylaşılan disk kaynakları kullanabilir üçüncü taraf bir çözümdür.</span><span class="sxs-lookup"><span data-stu-id="2f526-845">SIOS DataKeeper Cluster Edition is a third-party solution you can use toocreate shared disk resources.</span></span>

<span data-ttu-id="2f526-846">Merhaba SAP ASCS/SCS SIOS DataKeeper Cluster Edition yüklemek küme paylaşım disk bu görevleri içerir:</span><span class="sxs-lookup"><span data-stu-id="2f526-846">Installing SIOS DataKeeper Cluster Edition for hello SAP ASCS/SCS cluster share disk involves these tasks:</span></span>

- <span data-ttu-id="2f526-847">.NET Framework 3.5 Hello ekleme</span><span class="sxs-lookup"><span data-stu-id="2f526-847">Adding hello .NET Framework 3.5</span></span>
- <span data-ttu-id="2f526-848">SIOS DataKeeper yükleme</span><span class="sxs-lookup"><span data-stu-id="2f526-848">Installing SIOS DataKeeper</span></span>
- <span data-ttu-id="2f526-849">SIOS DataKeeper ayarlama</span><span class="sxs-lookup"><span data-stu-id="2f526-849">Setting up SIOS DataKeeper</span></span>

#### <span data-ttu-id="2f526-850"><a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a>.NET Framework 3.5 Hello ekleme</span><span class="sxs-lookup"><span data-stu-id="2f526-850"><a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a> Add hello .NET Framework 3.5</span></span>
<span data-ttu-id="2f526-851">Merhaba Microsoft .NET Framework 3.5 otomatik olarak etkinleştirilmiş veya Windows Server 2012 R2'de yüklü değil.</span><span class="sxs-lookup"><span data-stu-id="2f526-851">hello Microsoft .NET Framework 3.5 isn't automatically activated or installed on Windows Server 2012 R2.</span></span> <span data-ttu-id="2f526-852">SIOS DataKeeper hello .NET Framework toobe DataKeeper yüklemek, tüm düğümlerde gerektirdiğinden, hello konuk işletim sisteminde hello kümedeki tüm sanal makinelerin hello .NET Framework 3.5 yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f526-852">Because SIOS DataKeeper requires hello .NET Framework toobe on all nodes that you install DataKeeper on, you must install hello .NET Framework 3.5 on hello guest operating system of all virtual machines in hello cluster.</span></span>

<span data-ttu-id="2f526-853">İki yolu tooadd hello .NET Framework 3.5 vardır:</span><span class="sxs-lookup"><span data-stu-id="2f526-853">There are two ways tooadd hello .NET Framework 3.5:</span></span>

- <span data-ttu-id="2f526-854">Merhaba Ekle roller ve Özellikler Sihirbazı Windows şekil 39 gösterildiği gibi kullanın.</span><span class="sxs-lookup"><span data-stu-id="2f526-854">Use hello Add Roles and Features Wizard in Windows as shown in Figure 39.</span></span>

  ![Şekil 39: hello .NET Framework 3.5 hello Ekle roller ve Özellikler Sihirbazı kullanarak yükleme][sap-ha-guide-figure-3028]

  <span data-ttu-id="2f526-856">_**Şekil 39:** hello Ekle roller ve Özellikler Sihirbazı kullanarak yükleme hello .NET Framework 3.5_</span><span class="sxs-lookup"><span data-stu-id="2f526-856">_**Figure 39:** Install hello .NET Framework 3.5 by using hello Add Roles and Features Wizard_</span></span>

  ![Şekil 40: yükleme ilerleme çubuğu hello .NET Framework 3.5 hello Ekle roller ve Özellikler Sihirbazı'nı kullanarak yüklediğinizde][sap-ha-guide-figure-3029]

  <span data-ttu-id="2f526-858">_**Şekil 40:** çubuğu hello .NET Framework 3.5 hello Ekle roller ve Özellikler Sihirbazı'nı kullanarak yüklediğinizde, yükleme ilerleme durumu_</span><span class="sxs-lookup"><span data-stu-id="2f526-858">_**Figure 40:** Installation progress bar when you install hello .NET Framework 3.5 by using hello Add Roles and Features Wizard_</span></span>

- <span data-ttu-id="2f526-859">Merhaba komut satırı aracı dism.exe kullanın.</span><span class="sxs-lookup"><span data-stu-id="2f526-859">Use hello command-line tool dism.exe.</span></span> <span data-ttu-id="2f526-860">Bu yükleme türü için tooaccess hello SxS dizin hello Windows yükleme medyası üzerinde gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f526-860">For this type of installation, you need tooaccess hello SxS directory on hello Windows installation media.</span></span> <span data-ttu-id="2f526-861">Yükseltilmiş bir komut istemine yazın:</span><span class="sxs-lookup"><span data-stu-id="2f526-861">At an elevated command prompt, type:</span></span>

  ```
  Dism /online /enable-feature /featurename:NetFx3 /All /Source:installation_media_drive:\sources\sxs /LimitAccess
  ```

#### <span data-ttu-id="2f526-862"><a name="dd41d5a2-8083-415b-9878-839652812102"></a>SIOS DataKeeper yükleyin</span><span class="sxs-lookup"><span data-stu-id="2f526-862"><a name="dd41d5a2-8083-415b-9878-839652812102"></a> Install SIOS DataKeeper</span></span>

<span data-ttu-id="2f526-863">Merhaba kümedeki her düğümde SIOS DataKeeper Cluster Edition yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2f526-863">Install SIOS DataKeeper Cluster Edition on each node in hello cluster.</span></span> <span data-ttu-id="2f526-864">toocreate sanal paylaşılan depolama SIOS DataKeeper ile eşitlenen bir yansıtma oluşturun ve Küme Paylaşılan depolama benzetimi.</span><span class="sxs-lookup"><span data-stu-id="2f526-864">toocreate virtual shared storage with SIOS DataKeeper, create a synced mirror and then simulate cluster shared storage.</span></span>

<span data-ttu-id="2f526-865">Merhaba SIOS yazılımı yüklemeden önce hello etki alanı kullanıcısı oluşturun **DataKeeperSvc**.</span><span class="sxs-lookup"><span data-stu-id="2f526-865">Before you install hello SIOS software, create hello domain user **DataKeeperSvc**.</span></span>

> [!NOTE]
> <span data-ttu-id="2f526-866">Merhaba eklemek **DataKeeperSvc** kullanıcı toohello **yerel yönetici** her iki küme düğümlerinde grup.</span><span class="sxs-lookup"><span data-stu-id="2f526-866">Add hello **DataKeeperSvc** user toohello **Local Administrator** group on both cluster nodes.</span></span>
>
>

<span data-ttu-id="2f526-867">tooinstall SIOS DataKeeper:</span><span class="sxs-lookup"><span data-stu-id="2f526-867">tooinstall SIOS DataKeeper:</span></span>

1.  <span data-ttu-id="2f526-868">Merhaba SIOS yazılım her iki küme düğümlerine yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2f526-868">Install hello SIOS software on both cluster nodes.</span></span>

  ![SIOS yükleyici][sap-ha-guide-figure-3030]

  ![Şekil 41: Merhaba SIOS DataKeeper Yükleme'nın ilk sayfasında][sap-ha-guide-figure-3031]

  <span data-ttu-id="2f526-871">_**Şekil 41:** hello SIOS DataKeeper Yükleme'nın ilk sayfasında_</span><span class="sxs-lookup"><span data-stu-id="2f526-871">_**Figure 41:** First page of hello SIOS DataKeeper installation_</span></span>

2.  <span data-ttu-id="2f526-872">Şekil 42 gösterilen hello iletişim kutusunda seçin **Evet**.</span><span class="sxs-lookup"><span data-stu-id="2f526-872">In hello dialog box shown in Figure 42, select **Yes**.</span></span>

  ![Şekil 42: Bir hizmeti devre dışı bırakılacak DataKeeper size bildirir][sap-ha-guide-figure-3032]

  <span data-ttu-id="2f526-874">_**Şekil 42:** DataKeeper bildirir, bir hizmeti devre dışı bırakılacak_</span><span class="sxs-lookup"><span data-stu-id="2f526-874">_**Figure 42:** DataKeeper informs you that a service will be disabled_</span></span>

3.  <span data-ttu-id="2f526-875">Şekil 43 gösterilen hello iletişim kutusunda seçtiğiniz olan öneririz **etki alanı veya sunucu hesabı**.</span><span class="sxs-lookup"><span data-stu-id="2f526-875">In hello dialog box shown in Figure 43, we recommend that you select **Domain or Server account**.</span></span>

  ![Şekil 43: Kullanıcı Seçimi SIOS DataKeeper için][sap-ha-guide-figure-3033]

  <span data-ttu-id="2f526-877">_**Şekil 43:** SIOS DataKeeper için kullanıcı seçimi_</span><span class="sxs-lookup"><span data-stu-id="2f526-877">_**Figure 43:** User selection for SIOS DataKeeper_</span></span>

4.  <span data-ttu-id="2f526-878">Merhaba etki alanı hesabı kullanıcı adı ve SIOS DataKeeper için oluşturduğunuz parola girin.</span><span class="sxs-lookup"><span data-stu-id="2f526-878">Enter hello domain account user name and passwords that you created for SIOS DataKeeper.</span></span>

  ![Şekil 44: Merhaba SIOS DataKeeper yükleme hello etki alanı kullanıcı adı ve parola girin][sap-ha-guide-figure-3034]

  <span data-ttu-id="2f526-880">_**Şekil 44:** Merhaba SIOS DataKeeper yükleme hello etki alanı kullanıcı adı ve parola girin_</span><span class="sxs-lookup"><span data-stu-id="2f526-880">_**Figure 44:** Enter hello domain user name and password for hello SIOS DataKeeper installation_</span></span>

5.  <span data-ttu-id="2f526-881">Şekil 45 gösterildiği gibi SIOS DataKeeper örneğinizin Hello lisans anahtarını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2f526-881">Install hello license key for your SIOS DataKeeper instance as shown in Figure 45.</span></span>

  ![Şekil 45: SIOS DataKeeper lisans anahtarınızı girin][sap-ha-guide-figure-3035]

  <span data-ttu-id="2f526-883">_**Şekil 45:** SIOS DataKeeper lisans anahtarınızı girin_</span><span class="sxs-lookup"><span data-stu-id="2f526-883">_**Figure 45:** Enter your SIOS DataKeeper license key_</span></span>

6.  <span data-ttu-id="2f526-884">İstendiğinde, hello sanal makineyi yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="2f526-884">When prompted, restart hello virtual machine.</span></span>

#### <span data-ttu-id="2f526-885"><a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a>SIOS DataKeeper ayarlayın</span><span class="sxs-lookup"><span data-stu-id="2f526-885"><a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a> Set up SIOS DataKeeper</span></span>

<span data-ttu-id="2f526-886">Her iki düğümde SIOS DataKeeper yükledikten sonra toostart hello yapılandırması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f526-886">After you install SIOS DataKeeper on both nodes, you need toostart hello configuration.</span></span> <span data-ttu-id="2f526-887">Merhaba hello yapılandırma hello sanal makinelerin tooeach toohave zaman uyumlu veri çoğaltma hello ilave diskler arasında bağlı hedefidir.</span><span class="sxs-lookup"><span data-stu-id="2f526-887">hello goal of hello configuration is toohave synchronous data replication between hello additional disks attached tooeach of hello virtual machines.</span></span>

1.  <span data-ttu-id="2f526-888">Merhaba DataKeeper yönetim ve yapılandırma aracını başlatmak ve ardından **Connect Server**.</span><span class="sxs-lookup"><span data-stu-id="2f526-888">Start hello DataKeeper Management and Configuration tool, and then select **Connect Server**.</span></span> <span data-ttu-id="2f526-889">(Şekil 46 bu seçenek kırmızı daire içine alınmıştır.)</span><span class="sxs-lookup"><span data-stu-id="2f526-889">(In Figure 46, this option is circled in red.)</span></span>

  ![Şekil 46: SIOS DataKeeper yönetim ve yapılandırma aracı][sap-ha-guide-figure-3036]

  <span data-ttu-id="2f526-891">_**Şekil 46:** SIOS DataKeeper yönetim ve yapılandırma aracı_</span><span class="sxs-lookup"><span data-stu-id="2f526-891">_**Figure 46:** SIOS DataKeeper Management and Configuration tool_</span></span>

2.  <span data-ttu-id="2f526-892">Merhaba adı girin veya TCP/IP adresi aracının hello ilk düğüm hello yönetimi ve yapılandırması için ve ikinci adım, hello İkinci düğüm bağlanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f526-892">Enter hello name or TCP/IP address of hello first node hello Management and Configuration tool should connect to, and, in a second step, hello second node.</span></span>

  ![Şekil 47: Ekle hello adı veya TCP/IP adresi aracının hello ilk düğüm hello yönetimi ve yapılandırması için ve ikinci adım, hello İkinci düğüm bağlanmanız gerekir][sap-ha-guide-figure-3037]

  <span data-ttu-id="2f526-894">_**Şekil 47:** Ekle hello adı veya TCP/IP adresi aracının hello ilk düğüm hello yönetimi ve yapılandırması bağlanmak için ve ikinci adım, hello ikinci düğümü_</span><span class="sxs-lookup"><span data-stu-id="2f526-894">_**Figure 47:** Insert hello name or TCP/IP address of hello first node hello Management and Configuration tool should connect to, and in a second step, hello second node_</span></span>

3.  <span data-ttu-id="2f526-895">Merhaba iki düğüm arasında Hello çoğaltma işi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2f526-895">Create hello replication job between hello two nodes.</span></span>

  ![Şekil 48: bir çoğaltma işi oluşturma][sap-ha-guide-figure-3038]

  <span data-ttu-id="2f526-897">_**Şekil 48:** çoğaltma işi oluşturma_</span><span class="sxs-lookup"><span data-stu-id="2f526-897">_**Figure 48:** Create a replication job_</span></span>

  <span data-ttu-id="2f526-898">Sihirbaz çoğaltma iş oluşturma hello işleminde size rehberlik eder.</span><span class="sxs-lookup"><span data-stu-id="2f526-898">A wizard guides you through hello process of creating a replication job.</span></span>
4.  <span data-ttu-id="2f526-899">Merhaba adı, TCP/IP adresi ve hello kaynak düğüm disk birimi tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="2f526-899">Define hello name, TCP/IP address, and disk volume of hello source node.</span></span>

  ![Şekil 49: hello çoğaltma işi hello adını tanımlayın][sap-ha-guide-figure-3039]

  <span data-ttu-id="2f526-901">_**Şekil 49:** hello çoğaltma işi hello adını tanımlayın_</span><span class="sxs-lookup"><span data-stu-id="2f526-901">_**Figure 49:** Define hello name of hello replication job_</span></span>

  ![Şekil 50: hello geçerli kaynak düğüm olmalıdır hello düğüm için hello temel veri tanımlama][sap-ha-guide-figure-3040]

  <span data-ttu-id="2f526-903">_**Şekil 50:** hello geçerli kaynak düğüm olmalıdır hello düğüm için hello temel veri tanımlama_</span><span class="sxs-lookup"><span data-stu-id="2f526-903">_**Figure 50:** Define hello base data for hello node, which should be hello current source node_</span></span>

5.  <span data-ttu-id="2f526-904">Merhaba adı, TCP/IP adresi ve hello hedef düğüm disk birimi tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="2f526-904">Define hello name, TCP/IP address, and disk volume of hello target node.</span></span>

  ![Şekil 51: hello geçerli hedef düğümü olmalı hello düğüm için hello temel veri tanımlama][sap-ha-guide-figure-3041]

  <span data-ttu-id="2f526-906">_**Şekil 51:** hello geçerli hedef düğümü olmalı hello düğüm için hello temel veri tanımlama_</span><span class="sxs-lookup"><span data-stu-id="2f526-906">_**Figure 51:** Define hello base data for hello node, which should be hello current target node_</span></span>

6.  <span data-ttu-id="2f526-907">Merhaba sıkıştırma algoritmaları tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="2f526-907">Define hello compression algorithms.</span></span> <span data-ttu-id="2f526-908">Bizim örneğimizde, hello çoğaltma akışını sıkıştırmak öneririz.</span><span class="sxs-lookup"><span data-stu-id="2f526-908">In our example, we recommend that you compress hello replication stream.</span></span> <span data-ttu-id="2f526-909">Özellikle yeniden eşitleme durumlarda hello çoğaltma akışı hello sıkıştırmasını yeniden eşitleme zamanı önemli ölçüde azaltır.</span><span class="sxs-lookup"><span data-stu-id="2f526-909">Especially in resynchronization situations, hello compression of hello replication stream dramatically reduces resynchronization time.</span></span> <span data-ttu-id="2f526-910">Sıkıştırma hello CPU ve RAM kaynaklarını bir sanal makinenin kullandığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="2f526-910">Note that compression uses hello CPU and RAM resources of a virtual machine.</span></span> <span data-ttu-id="2f526-911">Merhaba sıkıştırma oranı arttıkça, bu nedenle kullanılan CPU kaynakları hacmi hello.</span><span class="sxs-lookup"><span data-stu-id="2f526-911">As hello compression rate increases, so does hello volume of CPU resources used.</span></span> <span data-ttu-id="2f526-912">Bu ayarı daha sonra da ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f526-912">You also can adjust this setting later.</span></span>

7.  <span data-ttu-id="2f526-913">Ayar başka bir gereksinim toocheck olan olup olmadığını zaman uyumsuz veya zaman uyumlu olarak hello çoğaltma gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="2f526-913">Another setting you need toocheck is whether hello replication occurs asynchronously or synchronously.</span></span> <span data-ttu-id="2f526-914">*SAP ASCS/SCS yapılandırmaları koruduğunuzda, zaman uyumlu çoğaltma kullanmalısınız*.</span><span class="sxs-lookup"><span data-stu-id="2f526-914">*When you protect SAP ASCS/SCS configurations, you must use synchronous replication*.</span></span>  

  ![Şekil 52: çoğaltma ayrıntılarını tanımlayın][sap-ha-guide-figure-3042]

  <span data-ttu-id="2f526-916">_**Şekil 52:** çoğaltma ayrıntılarını tanımlayın_</span><span class="sxs-lookup"><span data-stu-id="2f526-916">_**Figure 52:** Define replication details_</span></span>

8.  <span data-ttu-id="2f526-917">Merhaba çoğaltma işlemiyle çoğaltılır hello birim gösterilen tooa Windows Server Yük Devretme Kümelemesi küme yapılandırması paylaşılan bir disk olarak olup olmayacağını tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="2f526-917">Define whether hello volume that is replicated by hello replication job should be represented tooa Windows Server Failover Clustering cluster configuration as a shared disk.</span></span> <span data-ttu-id="2f526-918">Merhaba SAP ASCS/SCS yapılandırmasını seçin **Evet** çoğaltılan birim olarak bir küme birimi olarak kullanabileceği bir paylaşılan disk küme görür hello Windows hello böylece.</span><span class="sxs-lookup"><span data-stu-id="2f526-918">For hello SAP ASCS/SCS configuration, select **Yes** so that hello Windows cluster sees hello replicated volume as a shared disk that it can use as a cluster volume.</span></span>

  ![Şekil 53: Evet tooset çoğaltılan hello toplu küme birimi seçin.][sap-ha-guide-figure-3043]

  <span data-ttu-id="2f526-920">_**Şekil 53:** seçin **Evet** tooset hello çoğaltılan birimi bir küme birimi olarak_</span><span class="sxs-lookup"><span data-stu-id="2f526-920">_**Figure 53:** Select **Yes** tooset hello replicated volume as a cluster volume_</span></span>

  <span data-ttu-id="2f526-921">Merhaba birim oluşturulduktan sonra hello DataKeeper yönetim ve yapılandırma aracı o hello çoğaltma işi etkin olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="2f526-921">After hello volume is created, hello DataKeeper Management and Configuration tool shows that hello replication job is active.</span></span>

  ![Şekil 54: DataKeeper SAP ASCS/SCS paylaşım disk hello için zaman uyumlu yansıtma etkindir][sap-ha-guide-figure-3044]

  <span data-ttu-id="2f526-923">_**Şekil 54:** hello SAP ASCS/SCS paylaşmak disk için DataKeeper zaman uyumlu yansıtma etkin olduğu_</span><span class="sxs-lookup"><span data-stu-id="2f526-923">_**Figure 54:** DataKeeper synchronous mirroring for hello SAP ASCS/SCS share disk is active_</span></span>

  <span data-ttu-id="2f526-924">Yük Devretme Kümesi Yöneticisi şimdi şekil 55 gösterildiği gibi hello disk DataKeeper disk olarak gösterir.</span><span class="sxs-lookup"><span data-stu-id="2f526-924">Failover Cluster Manager now shows hello disk as a DataKeeper disk, as shown in Figure 55.</span></span>

  ![Şekil 55: Yük devretme kümesi Yöneticisi'ni DataKeeper çoğaltılan hello disk gösterir.][sap-ha-guide-figure-3045]

  <span data-ttu-id="2f526-926">_**Şekil 55:** yük devretme kümesi Yöneticisi, çoğaltılan bu DataKeeper hello disk gösterir_</span><span class="sxs-lookup"><span data-stu-id="2f526-926">_**Figure 55:** Failover Cluster Manager shows hello disk that DataKeeper replicated_</span></span>

## <span data-ttu-id="2f526-927"><a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a>Merhaba SAP NetWeaver sistemini yükleyin</span><span class="sxs-lookup"><span data-stu-id="2f526-927"><a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a> Install hello SAP NetWeaver system</span></span>

<span data-ttu-id="2f526-928">Kurulumları hello DBMS sistemine bağlı olarak farklılık gösterdiğinden biz hello DBMS kurulumunu açıklayan olmaz.</span><span class="sxs-lookup"><span data-stu-id="2f526-928">We won’t describe hello DBMS setup because setups vary depending on hello DBMS system you use.</span></span> <span data-ttu-id="2f526-929">Ancak, yüksek kullanılabilirlik sorunları hello DBMS ile Merhaba işlevler hello farklı DBMS satıcılar için Azure desteği ile giderilen varsayalım.</span><span class="sxs-lookup"><span data-stu-id="2f526-929">However, we assume that high-availability concerns with hello DBMS are addressed with hello functionalities hello different DBMS vendors support for Azure.</span></span> <span data-ttu-id="2f526-930">Örneğin, her zaman açık veya Oracle veritabanları için SQL Server ve Oracle Data Guard için veritabanı yansıtma.</span><span class="sxs-lookup"><span data-stu-id="2f526-930">For example, Always On or database mirroring for SQL Server, and Oracle Data Guard for Oracle databases.</span></span> <span data-ttu-id="2f526-931">Bu makalede kullanırız hello senaryosunda, size daha fazla koruma toohello DBMS ekleyemiyor.</span><span class="sxs-lookup"><span data-stu-id="2f526-931">In hello scenario we use in this article, we didn't add more protection toohello DBMS.</span></span>

<span data-ttu-id="2f526-932">Bu tür bir Azure kümelenmiş SAP ASCS/SCS yapılandırmasında farklı DBMS Hizmetleri etkileşim, özel durumlar vardır.</span><span class="sxs-lookup"><span data-stu-id="2f526-932">There are no special considerations when different DBMS services interact with this kind of clustered SAP ASCS/SCS configuration in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="2f526-933">SAP NetWeaver ABAP sistemleri, Java sistemleri ve ABAP + Java sistemleri Hello yükleme yordamları neredeyse aynıdır.</span><span class="sxs-lookup"><span data-stu-id="2f526-933">hello installation procedures of SAP NetWeaver ABAP systems, Java systems, and ABAP+Java systems are almost identical.</span></span> <span data-ttu-id="2f526-934">Merhaba en önemli fark, bir SAP ABAP sistemi bir ASCS örneği sahip olur.</span><span class="sxs-lookup"><span data-stu-id="2f526-934">hello most significant difference is that an SAP ABAP system has one ASCS instance.</span></span> <span data-ttu-id="2f526-935">Merhaba SAP Java sistem bir SCS örneği vardır.</span><span class="sxs-lookup"><span data-stu-id="2f526-935">hello SAP Java system has one SCS instance.</span></span> <span data-ttu-id="2f526-936">bir ASCS örneği Hello SAP ABAP + Java sistem sahiptir ve çalışır durumda bir SCS örneği hello aynı Microsoft yük devretme küme grubu.</span><span class="sxs-lookup"><span data-stu-id="2f526-936">hello SAP ABAP+Java system has one ASCS instance and one SCS instance running in hello same Microsoft failover cluster group.</span></span> <span data-ttu-id="2f526-937">Her SAP NetWeaver yükleme yığınının yükleme farkları açıkça belirtilen.</span><span class="sxs-lookup"><span data-stu-id="2f526-937">Any installation differences for each SAP NetWeaver installation stack are explicitly mentioned.</span></span> <span data-ttu-id="2f526-938">Diğer tüm bölümleri olan Merhaba, aynı varsayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f526-938">You can assume that all other parts are hello same.</span></span>  
>
>

### <span data-ttu-id="2f526-939"><a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a>Bir yüksek kullanılabilirlik ASCS/SCS örneğiyle SAP yükleyin</span><span class="sxs-lookup"><span data-stu-id="2f526-939"><a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a> Install SAP with a high-availability ASCS/SCS instance</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2f526-940">Unutmayın, sayfa dosyası üzerinde DataKeeper tooplace yansıtılmış birimler.</span><span class="sxs-lookup"><span data-stu-id="2f526-940">Be sure not tooplace your page file on DataKeeper mirrored volumes.</span></span> <span data-ttu-id="2f526-941">Yansıtılmış birimler DataKeeper desteklemez.</span><span class="sxs-lookup"><span data-stu-id="2f526-941">DataKeeper does not support mirrored volumes.</span></span> <span data-ttu-id="2f526-942">Merhaba varsayılan olduğu hello geçici D sürücüsündeki bir Azure sanal makine, sayfa dosyası bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f526-942">You can leave your page file on hello temporary drive D of an Azure virtual machine, which is hello default.</span></span> <span data-ttu-id="2f526-943">Bunu zaten yoksa, hello Windows sayfa dosyası toodrive D: Azure sanal makinenizin taşıyın.</span><span class="sxs-lookup"><span data-stu-id="2f526-943">If it's not already there, move hello Windows page file toodrive D: of your Azure virtual machine.</span></span>
>
>

<span data-ttu-id="2f526-944">Bir yüksek kullanılabilirlik ASCS/SCS örneğiyle SAP yüklemek, bu görevleri içerir:</span><span class="sxs-lookup"><span data-stu-id="2f526-944">Installing SAP with a high-availability ASCS/SCS instance involves these tasks:</span></span>

- <span data-ttu-id="2f526-945">Kümelenmiş hello SAP ASCS/SCS örneği için bir sanal ana bilgisayar adı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2f526-945">Creating a virtual host name for hello clustered SAP ASCS/SCS instance</span></span>
- <span data-ttu-id="2f526-946">Merhaba SAP ilk küme düğümüne yükleme</span><span class="sxs-lookup"><span data-stu-id="2f526-946">Installing hello SAP first cluster node</span></span>
- <span data-ttu-id="2f526-947">Merhaba SAP profili hello ASCS/SCS örneğinin değiştirme</span><span class="sxs-lookup"><span data-stu-id="2f526-947">Modifying hello SAP profile of hello ASCS/SCS instance</span></span>
- <span data-ttu-id="2f526-948">Sonda bağlantı noktası ekleme</span><span class="sxs-lookup"><span data-stu-id="2f526-948">Adding a probe port</span></span>
- <span data-ttu-id="2f526-949">Merhaba Windows Güvenlik Duvarı araştırma bağlantı noktası açma</span><span class="sxs-lookup"><span data-stu-id="2f526-949">Opening hello Windows firewall probe port</span></span>

#### <span data-ttu-id="2f526-950"><a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a>Kümelenmiş hello SAP ASCS/SCS örneği için bir sanal ana bilgisayar adı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2f526-950"><a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a> Create a virtual host name for hello clustered SAP ASCS/SCS instance</span></span>

1.  <span data-ttu-id="2f526-951">Merhaba Windows DNS Yöneticisi'nde hello ASCS/SCS örneğinin hello sanal ana bilgisayar adı için bir DNS girişi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2f526-951">In hello Windows DNS manager, create a DNS entry for hello virtual host name of hello ASCS/SCS instance.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="2f526-952">Merhaba ASCS/SCS örneği olmalıdır hello toohello sanal ana bilgisayar adı atamak IP adresi hello aynı tooAzure yük dengeleyiciye atanan hello IP adresi olarak (**<*SID*> - lb - ascs **).</span><span class="sxs-lookup"><span data-stu-id="2f526-952">hello IP address that you assign toohello virtual host name of hello ASCS/SCS instance must be hello same as hello IP address that you assigned tooAzure Load Balancer (**<*SID*>-lb-ascs**).</span></span>  
  >
  >

  <span data-ttu-id="2f526-953">Merhaba hello sanal SAP ASCS/SCS ana bilgisayar adının IP adresini (**pr1 ascs sap**) olan hello aynı başlangıç IP adresi Azure yük dengeleyici olarak (**pr1 lb ascs**).</span><span class="sxs-lookup"><span data-stu-id="2f526-953">hello IP address of hello virtual SAP ASCS/SCS host name (**pr1-ascs-sap**) is hello same as hello IP address of Azure Load Balancer (**pr1-lb-ascs**).</span></span>

  ![Şekil 56: hello DNS girdisini hello SAP ASCS/SCS küme sanal adı ve TCP/IP adresi tanımlayın][sap-ha-guide-figure-3046]

  <span data-ttu-id="2f526-955">_**Şekil 56:** hello DNS girdisini hello SAP ASCS/SCS küme sanal adı ve TCP/IP adresi tanımlayın_</span><span class="sxs-lookup"><span data-stu-id="2f526-955">_**Figure 56:** Define hello DNS entry for hello SAP ASCS/SCS cluster virtual name and TCP/IP address_</span></span>

2.  <span data-ttu-id="2f526-956">toodefine hello IP adresi atanmış toohello sanal ana bilgisayar adını, select **DNS Yöneticisi'ni** > **etki alanı**.</span><span class="sxs-lookup"><span data-stu-id="2f526-956">toodefine hello IP address assigned toohello virtual host name, select **DNS Manager** > **Domain**.</span></span>

  ![Şekil 57: Yeni sanal adı ve TCP/IP adresi SAP ASCS/SCS kümesi yapılandırması için][sap-ha-guide-figure-3047]

  <span data-ttu-id="2f526-958">_**Şekil 57:** yeni sanal adı ve TCP/IP adresi SAP ASCS/SCS küme yapılandırması_</span><span class="sxs-lookup"><span data-stu-id="2f526-958">_**Figure 57:** New virtual name and TCP/IP address for SAP ASCS/SCS cluster configuration_</span></span>

#### <span data-ttu-id="2f526-959"><a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a>Merhaba SAP ilk küme düğümüne yükleyin</span><span class="sxs-lookup"><span data-stu-id="2f526-959"><a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a> Install hello SAP first cluster node</span></span>

1.  <span data-ttu-id="2f526-960">Merhaba ilk küme düğümü seçeneği küme düğümünde A. yürütme Örneğin, hello üzerinde **pr1 ascs 0** ana bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="2f526-960">Execute hello first cluster node option on cluster node A. For example, on hello **pr1-ascs-0** host.</span></span>
2.  <span data-ttu-id="2f526-961">tookeep hello varsayılan bağlantı noktalarını hello Azure iç yük dengeleyici, seçin:</span><span class="sxs-lookup"><span data-stu-id="2f526-961">tookeep hello default ports for hello Azure internal load balancer, select:</span></span>

  * <span data-ttu-id="2f526-962">**ABAP sistem**: **ASCS** örnek numarasını **00**</span><span class="sxs-lookup"><span data-stu-id="2f526-962">**ABAP system**: **ASCS** instance number **00**</span></span>
  * <span data-ttu-id="2f526-963">**Java sistem**: **SCS** örnek numarasını **01**</span><span class="sxs-lookup"><span data-stu-id="2f526-963">**Java system**: **SCS** instance number **01**</span></span>
  * <span data-ttu-id="2f526-964">**ABAP + Java sistem**: **ASCS** örnek numarasını **00** ve **SCS** örnek numarasını **01**</span><span class="sxs-lookup"><span data-stu-id="2f526-964">**ABAP+Java system**: **ASCS** instance number **00** and **SCS** instance number **01**</span></span>

  <span data-ttu-id="2f526-965">toouse örnek sayılar, hello ABAP ASCS 00 dışında örneği ve 01 hello Java SCS örneği için öncelikle toochange hello Azure iç yük dengeleyici varsayılan Yük Dengeleme kuralları, açıklanan gerekir [değişiklik hello ASCS/SCS varsayılan yükleme Dengeleme hello Azure iç yük dengeleyici kuralları][sap-ha-guide-8.9].</span><span class="sxs-lookup"><span data-stu-id="2f526-965">toouse instance numbers other than 00 for hello ABAP ASCS instance and 01 for hello Java SCS instance, first you need toochange hello Azure internal load balancer default load balancing rules, described in [Change hello ASCS/SCS default load balancing rules for hello Azure internal load balancer][sap-ha-guide-8.9].</span></span>

<span data-ttu-id="2f526-966">Merhaba sonraki birkaç görevleri hello standart SAP yükleme belgelerinde açıklanan değil.</span><span class="sxs-lookup"><span data-stu-id="2f526-966">hello next few tasks aren't described in hello standard SAP installation documentation.</span></span>

> [!NOTE]
> <span data-ttu-id="2f526-967">Merhaba SAP yükleme belgelerini nasıl tooinstall hello ilk ASCS/SCS küme düğümüne açıklar.</span><span class="sxs-lookup"><span data-stu-id="2f526-967">hello SAP installation documentation describes how tooinstall hello first ASCS/SCS cluster node.</span></span>
>
>

#### <span data-ttu-id="2f526-968"><a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a>Merhaba SAP profili hello ASCS/SCS örneğinin değiştirme</span><span class="sxs-lookup"><span data-stu-id="2f526-968"><a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a> Modify hello SAP profile of hello ASCS/SCS instance</span></span>

<span data-ttu-id="2f526-969">Yeni bir profil parametre tooadd gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f526-969">You need tooadd a new profile parameter.</span></span> <span data-ttu-id="2f526-970">Hello profil parametre çok uzun süre boşta olduğunda kapanmasını SAP iş süreçlerini ve hello enqueue sunucu arasındaki bağlantıları engeller.</span><span class="sxs-lookup"><span data-stu-id="2f526-970">hello profile parameter prevents connections between SAP work processes and hello enqueue server from closing when they are idle for too long.</span></span> <span data-ttu-id="2f526-971">Biz hello sorun senaryoda bahsedilen [hello SAP ASCS/SCS örneği her iki küme düğümleri üzerinde kayıt defteri girdisini eklemeniz][sap-ha-guide-8.11].</span><span class="sxs-lookup"><span data-stu-id="2f526-971">We mentioned hello problem scenario in [Add registry entries on both cluster nodes of hello SAP ASCS/SCS instance][sap-ha-guide-8.11].</span></span> <span data-ttu-id="2f526-972">Bu bölümde Ayrıca iki değişiklikleri toosome temel TCP/IP bağlantı parametrelerini sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="2f526-972">In that section, we also introduced two changes toosome basic TCP/IP connection parameters.</span></span> <span data-ttu-id="2f526-973">İkinci adımda, tooset hello enqueue sunucu toosend gereken bir `keep_alive` hello bağlantıları hello Azure iç yük dengeleyicinin boşta kalma eşiği isabet yok böylece sinyal.</span><span class="sxs-lookup"><span data-stu-id="2f526-973">In a second step, you need tooset hello enqueue server toosend a `keep_alive` signal so that hello connections don't hit hello Azure internal load balancer's idle threshold.</span></span>

<span data-ttu-id="2f526-974">toomodify hello hello ASCS/SCS örneğinin SAP profili:</span><span class="sxs-lookup"><span data-stu-id="2f526-974">toomodify hello SAP profile of hello ASCS/SCS instance:</span></span>

1.  <span data-ttu-id="2f526-975">Bu profil parametresi toohello SAP ASCS/SCS örneği profili ekleyin:</span><span class="sxs-lookup"><span data-stu-id="2f526-975">Add this profile parameter toohello SAP ASCS/SCS instance profile:</span></span>

  ```
  enque/encni/set_so_keepalive = true
  ```
  <span data-ttu-id="2f526-976">Bizim örneğimizde, hello yol şudur:</span><span class="sxs-lookup"><span data-stu-id="2f526-976">In our example, hello path is:</span></span>

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_ASCS00_pr1-ascs-sap`

  <span data-ttu-id="2f526-977">Örneğin, toohello SAP SCS profili ve karşılık gelen yol örneği:</span><span class="sxs-lookup"><span data-stu-id="2f526-977">For example, toohello SAP SCS instance profile and corresponding path:</span></span>

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_SCS01_pr1-ascs-sap`

2.  <span data-ttu-id="2f526-978">tooapply hello değişiklikleri hello SAP ASCS /SCS örneğini yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="2f526-978">tooapply hello changes, restart hello SAP ASCS /SCS instance.</span></span>

#### <span data-ttu-id="2f526-979"><a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a>Bir araştırma bağlantı noktası ekleme</span><span class="sxs-lookup"><span data-stu-id="2f526-979"><a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a> Add a probe port</span></span>

<span data-ttu-id="2f526-980">Merhaba iç yük dengeleyicinin araştırma işlevselliği toomake hello tüm küme yapılandırması iş Azure yük dengeleyici ile kullanın.</span><span class="sxs-lookup"><span data-stu-id="2f526-980">Use hello internal load balancer's probe functionality toomake hello entire cluster configuration work with Azure Load Balancer.</span></span> <span data-ttu-id="2f526-981">Hello Azure iç yük dengeleyici genellikle hello gelen iş yükü katılımcı sanal makineler arasında eşit olarak dağıtır.</span><span class="sxs-lookup"><span data-stu-id="2f526-981">hello Azure internal load balancer usually distributes hello incoming workload equally between participating virtual machines.</span></span> <span data-ttu-id="2f526-982">Ancak, tek örnek etkin olmadığından bu bazı küme yapılandırmaları çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="2f526-982">However, this won't work in some cluster configurations because only one instance is active.</span></span> <span data-ttu-id="2f526-983">Merhaba diğer örnek pasif ve hello iş yükü hiçbirini kabul edemez.</span><span class="sxs-lookup"><span data-stu-id="2f526-983">hello other instance is passive and can’t accept any of hello workload.</span></span> <span data-ttu-id="2f526-984">Hello Azure iç yük dengeleyici atar yalnızca tooan etkin örneği çalışırken bir araştırma işlevsellik yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="2f526-984">A probe functionality helps when hello Azure internal load balancer assigns work only tooan active instance.</span></span> <span data-ttu-id="2f526-985">Merhaba araştırma işlevsellikle hello iç yük dengeleyici hangi örnekleri etkin olduğunu ve yalnızca hello örneği hello iş yükü ile hedef algılayabilir.</span><span class="sxs-lookup"><span data-stu-id="2f526-985">With hello probe functionality, hello internal load balancer can detect which instances are active, and then target only hello instance with hello workload.</span></span>

<span data-ttu-id="2f526-986">tooadd sonda bağlantı noktası:</span><span class="sxs-lookup"><span data-stu-id="2f526-986">tooadd a probe port:</span></span>

1.  <span data-ttu-id="2f526-987">Merhaba geçerli denetleyin **ProbePort** hello aşağıdaki PowerShell komutunu çalıştırarak ayarlama.</span><span class="sxs-lookup"><span data-stu-id="2f526-987">Check hello current **ProbePort** setting by running hello following PowerShell command.</span></span> <span data-ttu-id="2f526-988">Merhaba sanal makineleri biri içinde ondan hello küme yapılandırmasında yürütün.</span><span class="sxs-lookup"><span data-stu-id="2f526-988">Execute it from within one of hello virtual machines in hello cluster configuration.</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter
  ```

2.  <span data-ttu-id="2f526-989">Bir araştırma bağlantı noktasını tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="2f526-989">Define a probe port.</span></span> <span data-ttu-id="2f526-990">Merhaba varsayılan araştırma bağlantı noktası numarası **0**.</span><span class="sxs-lookup"><span data-stu-id="2f526-990">hello default probe port number is **0**.</span></span> <span data-ttu-id="2f526-991">Bizim örneğimizde, araştırma bağlantı noktası kullanırız **62000**.</span><span class="sxs-lookup"><span data-stu-id="2f526-991">In our example, we use probe port **62000**.</span></span>

  ![Şekil 58: hello küme yapılandırması araştırma bağlantı noktası varsayılan olarak 0 olur.][sap-ha-guide-figure-3048]

  <span data-ttu-id="2f526-993">_**Şekil 58:** hello varsayılan küme yapılandırması araştırma bağlantı noktası: 0_</span><span class="sxs-lookup"><span data-stu-id="2f526-993">_**Figure 58:** hello default cluster configuration probe port is 0_</span></span>

  <span data-ttu-id="2f526-994">başlangıç bağlantı noktası numarası SAP Azure Resource Manager şablonları tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="2f526-994">hello port number is defined in SAP Azure Resource Manager templates.</span></span> <span data-ttu-id="2f526-995">PowerShell hello bağlantı noktası numarası atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f526-995">You can assign hello port number in PowerShell.</span></span>

  <span data-ttu-id="2f526-996">tooset hello için yeni bir ProbePort değeri  **SAP <*SID*> PowerShell Betiği aşağıdaki hello çalıştırmak IP ** küme kaynağı.</span><span class="sxs-lookup"><span data-stu-id="2f526-996">tooset a new ProbePort value for hello **SAP <*SID*> IP** cluster resource, run hello following PowerShell script.</span></span> <span data-ttu-id="2f526-997">Merhaba PowerShell değişkenleri ortamınız için güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="2f526-997">Update hello PowerShell variables for your environment.</span></span> <span data-ttu-id="2f526-998">Merhaba betik çalıştıktan sonra istendiğinde toorestart hello SAP küme grubu tooactivate hello değişiklikleri olması.</span><span class="sxs-lookup"><span data-stu-id="2f526-998">After hello script runs, you'll be prompted toorestart hello SAP cluster group tooactivate hello changes.</span></span>

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

  <span data-ttu-id="2f526-999">Merhaba aldıktan sonra  **SAP <*SID*> ** Küme rolünü, doğrulayın **ProbePort** toohello yeni değerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="2f526-999">After you bring hello **SAP <*SID*>** cluster role online, verify that **ProbePort** is set toohello new value.</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter

  ```

  ![Şekil 59: hello yeni değeri ayarlandıktan sonra hello küme bağlantı noktası araştırma][sap-ha-guide-figure-3049]

  <span data-ttu-id="2f526-1001">_**Şekil 59:** hello yeni değeri ayarlandıktan sonra hello küme bağlantı noktası araştırma_</span><span class="sxs-lookup"><span data-stu-id="2f526-1001">_**Figure 59:** Probe hello cluster port after you set hello new value_</span></span>

#### <span data-ttu-id="2f526-1002"><a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a>Merhaba Windows Güvenlik Duvarı araştırma bağlantı noktasını açın</span><span class="sxs-lookup"><span data-stu-id="2f526-1002"><a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a> Open hello Windows firewall probe port</span></span>

<span data-ttu-id="2f526-1003">Tooopen her iki küme düğümlerinde Windows Güvenlik Duvarı araştırma bağlantı gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f526-1003">You need tooopen a Windows firewall probe port on both cluster nodes.</span></span> <span data-ttu-id="2f526-1004">Komut dosyası tooopen bir Windows Güvenlik Duvarı araştırma bağlantı noktasını aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="2f526-1004">Use hello following script tooopen a Windows firewall probe port.</span></span> <span data-ttu-id="2f526-1005">Merhaba PowerShell değişkenleri ortamınız için güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="2f526-1005">Update hello PowerShell variables for your environment.</span></span>

  ```PowerShell
  $ProbePort = 62000   # ProbePort of hello Azure Internal Load Balancer

  New-NetFirewallRule -Name AzureProbePort -DisplayName "Rule for Azure Probe Port" -Direction Inbound -Action Allow -Protocol TCP -LocalPort $ProbePort
  ```

<span data-ttu-id="2f526-1006">Merhaba **ProbePort** çok ayarlanır**62000**.</span><span class="sxs-lookup"><span data-stu-id="2f526-1006">hello **ProbePort** is set too**62000**.</span></span> <span data-ttu-id="2f526-1007">Merhaba dosya paylaşımına erişmek artık  **\\\ascsha-clsap\sapmnt** diğer konakları, gibi kadar **ascsha dbas**.</span><span class="sxs-lookup"><span data-stu-id="2f526-1007">Now you can access hello file share **\\\ascsha-clsap\sapmnt** from other hosts, such as from **ascsha-dbas**.</span></span>

### <span data-ttu-id="2f526-1008"><a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a>Merhaba veritabanı örneğini yükleyin</span><span class="sxs-lookup"><span data-stu-id="2f526-1008"><a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a> Install hello database instance</span></span>

<span data-ttu-id="2f526-1009">tooinstall hello veritabanı örneği, hello SAP yükleme belgelerini açıklanan hello süreci izleyin.</span><span class="sxs-lookup"><span data-stu-id="2f526-1009">tooinstall hello database instance, follow hello process described in hello SAP installation documentation.</span></span>

### <span data-ttu-id="2f526-1010"><a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a>Merhaba ikinci küme düğümü yükleme</span><span class="sxs-lookup"><span data-stu-id="2f526-1010"><a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a> Install hello second cluster node</span></span>

<span data-ttu-id="2f526-1011">tooinstall hello ikinci küme, hello SAP Yükleme Kılavuzu'na hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="2f526-1011">tooinstall hello second cluster, follow hello steps in hello SAP installation guide.</span></span>

### <span data-ttu-id="2f526-1012"><a name="094bc895-31d4-4471-91cc-1513b64e406a"></a>Merhaba SAP ERS Windows hizmet örneği Hello başlangıç türünü değiştirme</span><span class="sxs-lookup"><span data-stu-id="2f526-1012"><a name="094bc895-31d4-4471-91cc-1513b64e406a"></a> Change hello start type of hello SAP ERS Windows service instance</span></span>

<span data-ttu-id="2f526-1013">Merhaba SAP ERS Windows hizmeti başlangıç türünü Hello çok değiştirme**otomatik (Gecikmeli Başlatma)** her iki küme düğümlerinde.</span><span class="sxs-lookup"><span data-stu-id="2f526-1013">Change hello start type of hello SAP ERS Windows service too**Automatic (Delayed Start)** on both cluster nodes.</span></span>

![Şekil 60: hello SAP ERS örneği toodelayed otomatik hello hizmet türünü değiştir][sap-ha-guide-figure-3050]

<span data-ttu-id="2f526-1015">_**Şekil 60:** hello hizmet türünü hello SAP ERS örneği toodelayed otomatik_</span><span class="sxs-lookup"><span data-stu-id="2f526-1015">_**Figure 60:** Change hello service type for hello SAP ERS instance toodelayed automatic_</span></span>

### <span data-ttu-id="2f526-1016"><a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a>Merhaba SAP birincil uygulama sunucusu yükleme</span><span class="sxs-lookup"><span data-stu-id="2f526-1016"><a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a> Install hello SAP Primary Application Server</span></span>

<span data-ttu-id="2f526-1017">Merhaba birincil uygulama sunucusu (PAS) örneğini yükleyin <*SID*> - dı - 0 hello sanal makinede, belirlediğiniz toohost hello PAS.</span><span class="sxs-lookup"><span data-stu-id="2f526-1017">Install hello Primary Application Server (PAS) instance <*SID*>-di-0 on hello virtual machine that you've designated toohost hello PAS.</span></span> <span data-ttu-id="2f526-1018">Azure veya DataKeeper özgü ayarları bir bağımlılık yoktur.</span><span class="sxs-lookup"><span data-stu-id="2f526-1018">There are no dependencies on Azure or DataKeeper-specific settings.</span></span>

### <span data-ttu-id="2f526-1019"><a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a>Merhaba SAP ek uygulama sunucusu yükleme</span><span class="sxs-lookup"><span data-stu-id="2f526-1019"><a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a> Install hello SAP Additional Application Server</span></span>

<span data-ttu-id="2f526-1020">Bir SAP ek uygulama sunucusu (AAS) tüm hello sanal SAP uygulama sunucusu örneği toohost tasarladığınız makinelere yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2f526-1020">Install an SAP Additional Application Server (AAS) on all hello virtual machines that you've designated toohost an SAP Application Server instance.</span></span> <span data-ttu-id="2f526-1021">Örneğin, <*SID*> - dı - 1 çok <*SID*> - di -&lt;n&gt;.</span><span class="sxs-lookup"><span data-stu-id="2f526-1021">For example, on <*SID*>-di-1 too<*SID*>-di-&lt;n&gt;.</span></span>

> [!NOTE]
> <span data-ttu-id="2f526-1022">Yüksek kullanılabilirlik SAP NetWeaver sistem hello yüklemesini tamamlar.</span><span class="sxs-lookup"><span data-stu-id="2f526-1022">This finishes hello installation of a high-availability SAP NetWeaver system.</span></span> <span data-ttu-id="2f526-1023">Ardından, yük devretme testi ile devam edin.</span><span class="sxs-lookup"><span data-stu-id="2f526-1023">Next, proceed with failover testing.</span></span>
>


## <span data-ttu-id="2f526-1024"><a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a>Test Hello SAP ASCS/SCS örneği yük devretme ve SIOS çoğaltma</span><span class="sxs-lookup"><span data-stu-id="2f526-1024"><a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a> Test hello SAP ASCS/SCS instance failover and SIOS replication</span></span>
<span data-ttu-id="2f526-1025">Bu kolay tootest ve yük devretme kümesi Yöneticisi'ni ve hello SIOS DataKeeper yönetimi ve yapılandırması aracını kullanarak bir SAP ASCS/SCS örneği yük devretme ve SIOS disk çoğaltması izleyin.</span><span class="sxs-lookup"><span data-stu-id="2f526-1025">It's easy tootest and monitor an SAP ASCS/SCS instance failover and SIOS disk replication by using Failover Cluster Manager and hello SIOS DataKeeper Management and Configuration tool.</span></span>

### <span data-ttu-id="2f526-1026"><a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a>SAP ASCS/SCS örneği bir küme düğümünde çalışıyor</span><span class="sxs-lookup"><span data-stu-id="2f526-1026"><a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a> SAP ASCS/SCS instance is running on cluster node A</span></span>

<span data-ttu-id="2f526-1027">Merhaba **SAP PR1** küme grubu A'daki küme düğümünde çalışıyor Örneğin, **pr1 ascs 0**.</span><span class="sxs-lookup"><span data-stu-id="2f526-1027">hello **SAP PR1** cluster group is running on cluster node A. For example, on **pr1-ascs-0**.</span></span> <span data-ttu-id="2f526-1028">Merhaba parçası olan paylaşılan hello disk sürücüsü S, Ata **SAP PR1** küme grubu ve hangi hello ASCS/SCS örnek kullanan, toocluster düğümü A.</span><span class="sxs-lookup"><span data-stu-id="2f526-1028">Assign hello shared disk drive S, which is part of hello **SAP PR1** cluster group, and which hello ASCS/SCS instance uses, toocluster node A.</span></span>

![Şekil 61: Yük devretme kümesi Yöneticisi: merhaba < SID > SAP küme grubu, bir küme düğümünde çalışıyor][sap-ha-guide-figure-5000]

<span data-ttu-id="2f526-1030">_**Şekil 61:** yük devretme kümesi Yöneticisi: SAP merhaba <*SID*> Küme grubu, bir küme düğümünde çalışıyor_</span><span class="sxs-lookup"><span data-stu-id="2f526-1030">_**Figure 61:** Failover Cluster Manager: hello SAP <*SID*> cluster group is running on cluster node A_</span></span>

<span data-ttu-id="2f526-1031">Merhaba SIOS DataKeeper yönetim ve Yapılandırma Aracı'nda verileri sürücüsünden hello kaynak birim S küme düğümünde bir toohello hedef birim sürücü S B. küme düğümünde eşzamanlı olarak çoğaltılır, hello paylaşılan disk görebilirsiniz Örneğin, gelen çoğaltılır **pr1 ascs 0 [10.0.0.40]** çok**pr1 ascs 1 [10.0.0.41]**.</span><span class="sxs-lookup"><span data-stu-id="2f526-1031">In hello SIOS DataKeeper Management and Configuration tool, you can see that hello shared disk data is synchronously replicated from hello source volume drive S on cluster node A toohello target volume drive S on cluster node B. For example, it's replicated from **pr1-ascs-0 [10.0.0.40]** too**pr1-ascs-1 [10.0.0.41]**.</span></span>

![Şekil 62: SIOS DataKeeper içinde hello yerel birim B toocluster düğümü küme düğümünden Çoğalt][sap-ha-guide-figure-5001]

<span data-ttu-id="2f526-1033">_**Şekil 62:** SIOS DataKeeper içinde hello yerel birim B toocluster düğümü küme düğümünden Çoğalt_</span><span class="sxs-lookup"><span data-stu-id="2f526-1033">_**Figure 62:** In SIOS DataKeeper, replicate hello local volume from cluster node A toocluster node B_</span></span>

### <span data-ttu-id="2f526-1034"><a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a>Yük devretme işlemini düğümü toonode B</span><span class="sxs-lookup"><span data-stu-id="2f526-1034"><a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a> Failover from node A toonode B</span></span>

1.  <span data-ttu-id="2f526-1035">Bu seçenekler tooinitiate birini hello SAP yük devretmesi seçin <*SID*> Küme grubu küme düğümü toocluster düğümünden B:</span><span class="sxs-lookup"><span data-stu-id="2f526-1035">Choose one of these options tooinitiate a failover of hello SAP <*SID*> cluster group from cluster node A toocluster node B:</span></span>
  - <span data-ttu-id="2f526-1036">Yük Devretme Kümesi Yöneticisi'ni kullanın</span><span class="sxs-lookup"><span data-stu-id="2f526-1036">Use Failover Cluster Manager</span></span>  
  - <span data-ttu-id="2f526-1037">Yük devretme kümesi PowerShell kullanma</span><span class="sxs-lookup"><span data-stu-id="2f526-1037">Use Failover Cluster PowerShell</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPClusterGroup = "SAP $SAPSID"
  Move-ClusterGroup -Name $SAPClusterGroup

  ```
2.  <span data-ttu-id="2f526-1038">Küme düğümü bir hello Windows konuk işletim sistemi içinde yeniden (Bu hello SAP otomatik olarak yük devretmesi başlatır <*SID*> Küme düğümü toonode B grubundan).</span><span class="sxs-lookup"><span data-stu-id="2f526-1038">Restart cluster node A within hello Windows guest operating system (this initiates an automatic failover of hello SAP <*SID*> cluster group from node A toonode B).</span></span>  
3.  <span data-ttu-id="2f526-1039">Küme düğümü hello Azure portal A'dan yeniden (Bu hello SAP otomatik olarak yük devretmesi başlatır <*SID*> Küme düğümü toonode B grubundan).</span><span class="sxs-lookup"><span data-stu-id="2f526-1039">Restart cluster node A from hello Azure portal (this initiates an automatic failover of hello SAP <*SID*> cluster group from node A toonode B).</span></span>  
4.  <span data-ttu-id="2f526-1040">Azure PowerShell kullanarak küme düğümü bir yeniden başlatma (Bu hello SAP otomatik olarak yük devretmesi başlatır <*SID*> Küme düğümü toonode B grubundan).</span><span class="sxs-lookup"><span data-stu-id="2f526-1040">Restart cluster node A by using Azure PowerShell (this initiates an automatic failover of hello SAP <*SID*> cluster group from node A toonode B).</span></span>

  <span data-ttu-id="2f526-1041">Yük devretme sonrasında, SAP merhaba <*SID*> Küme grubu b küme düğümünde çalışıyor Örneğin, üzerinde çalıştırıldığı **pr1 ascs 1**.</span><span class="sxs-lookup"><span data-stu-id="2f526-1041">After failover, hello SAP <*SID*> cluster group is running on cluster node B. For example, it's running on **pr1-ascs-1**.</span></span>

  ![Şekil 63: Yük devretme kümesi Yöneticisi'nde hello SAP < SID > Küme grubu B küme düğümünde çalışıyor][sap-ha-guide-figure-5002]

  <span data-ttu-id="2f526-1043">_**Şekil 63**: yük devretme kümesi Yöneticisi'nde hello SAP <*SID*> Küme grubu B küme düğümünde çalışıyor_</span><span class="sxs-lookup"><span data-stu-id="2f526-1043">_**Figure 63**: In Failover Cluster Manager, hello SAP <*SID*> cluster group is running on cluster node B_</span></span>

  <span data-ttu-id="2f526-1044">Merhaba paylaşılan disk artık takılı kümede düğüm B. SIOS DataKeeper veri sürücüsünden kaynak birim S A. küme düğümünde Küme düğümü B tootarget birimin sürücü S çoğaltma Örneğin, gelen çoğaltma **pr1 ascs 1 [10.0.0.41]** çok**pr1 ascs 0 [10.0.0.40]**.</span><span class="sxs-lookup"><span data-stu-id="2f526-1044">hello shared disk is now mounted on cluster node B. SIOS DataKeeper is replicating data from source volume drive S on cluster node B tootarget volume drive S on cluster node A. For example, it's replicating from **pr1-ascs-1 [10.0.0.41]** too**pr1-ascs-0 [10.0.0.40]**.</span></span>

  ![Şekil 64: Hello yerel birim SIOS DataKeeper, küme düğümü B toocluster düğümünden A çoğaltır.][sap-ha-guide-figure-5003]

  <span data-ttu-id="2f526-1046">_**Şekil 64:** SIOS DataKeeper çoğaltır hello yerel birim küme düğümü B toocluster düğümünden A_</span><span class="sxs-lookup"><span data-stu-id="2f526-1046">_**Figure 64:** SIOS DataKeeper replicates hello local volume from cluster node B toocluster node A_</span></span>
