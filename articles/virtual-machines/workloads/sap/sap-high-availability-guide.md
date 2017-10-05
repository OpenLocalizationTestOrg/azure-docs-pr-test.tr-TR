---
title: "Azure sanal makineler için yüksek oranda kullanılabilirlik SAP NetWeaver | Microsoft Docs"
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
ms.openlocfilehash: d00db895ffcf9ba9a51e3df2dae5d33c0277dd6f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-virtual-machines-high-availability-for-sap-netweaver"></a><span data-ttu-id="950e2-103">SAP NetWeaver için Azure sanal makineleri yüksek kullanılabilirlik</span><span class="sxs-lookup"><span data-stu-id="950e2-103">Azure Virtual Machines high availability for SAP NetWeaver</span></span>

<span data-ttu-id="950e2-104">[1928533]:https://launchpad.support.sap.com/#/notes/1928533</span><span class="sxs-lookup"><span data-stu-id="950e2-104">[1928533]:https://launchpad.support.sap.com/#/notes/1928533</span></span>
<span data-ttu-id="950e2-105">[1999351]:https://launchpad.support.sap.com/#/notes/1999351</span><span class="sxs-lookup"><span data-stu-id="950e2-105">[1999351]:https://launchpad.support.sap.com/#/notes/1999351</span></span>
<span data-ttu-id="950e2-106">[2015553]:https://launchpad.support.sap.com/#/notes/2015553</span><span class="sxs-lookup"><span data-stu-id="950e2-106">[2015553]:https://launchpad.support.sap.com/#/notes/2015553</span></span>
<span data-ttu-id="950e2-107">[2178632]:https://launchpad.support.sap.com/#/notes/2178632</span><span class="sxs-lookup"><span data-stu-id="950e2-107">[2178632]:https://launchpad.support.sap.com/#/notes/2178632</span></span>
<span data-ttu-id="950e2-108">[2243692]:https://launchpad.support.sap.com/#/notes/2243692</span><span class="sxs-lookup"><span data-stu-id="950e2-108">[2243692]:https://launchpad.support.sap.com/#/notes/2243692</span></span>

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



<span data-ttu-id="950e2-109">Azure sanal makinelerin işlem, depolama ve ağ kaynaklarına, en az sürede ve uzun tedarik döngüleri olmadan gereken kuruluşlar için çözüm şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="950e2-109">Azure Virtual Machines is the solution for organizations that need compute, storage, and network resources, in minimal time, and without lengthy procurement cycles.</span></span> <span data-ttu-id="950e2-110">SAP NetWeaver tabanlı ABAP, Java ve ABAP + Java yığını gibi Klasik uygulamaları dağıtmak için Azure sanal makineleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="950e2-110">You can use Azure Virtual Machines to deploy classic applications like SAP NetWeaver-based ABAP, Java, and an ABAP+Java stack.</span></span> <span data-ttu-id="950e2-111">Güvenilirlik ve kullanılabilirlik ek şirket içi kaynaklar olmadan genişletir.</span><span class="sxs-lookup"><span data-stu-id="950e2-111">Extend reliability and availability without additional on-premises resources.</span></span> <span data-ttu-id="950e2-112">Azure sanal makineleri şirket içi bağlantılar, Azure sanal makineler, kuruluşunuzun şirket içi etki alanları, özel Bulutlar ve SAP sistem yatay tümleştirebilir şekilde destekler.</span><span class="sxs-lookup"><span data-stu-id="950e2-112">Azure Virtual Machines supports cross-premises connectivity, so you can integrate Azure Virtual Machines into your organization's on-premises domains, private clouds, and SAP system landscape.</span></span>

<span data-ttu-id="950e2-113">Bu makalede, Azure Resource Manager dağıtım modelini kullanarak azure'da yüksek kullanılabilirlik SAP sistemlerini dağıtmak için uygulayabileceğiniz adımlar kapsar.</span><span class="sxs-lookup"><span data-stu-id="950e2-113">In this article, we cover the steps that you can take to deploy high-availability SAP systems in Azure by using the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="950e2-114">Biz bu ana görevlerinde ilerlemenizde:</span><span class="sxs-lookup"><span data-stu-id="950e2-114">We walk you through these major tasks:</span></span>

* <span data-ttu-id="950e2-115">Sağ SAP notlar ve yükleme kılavuzları, listelenen Bul [kaynakları] [ sap-ha-guide-2] bölümü.</span><span class="sxs-lookup"><span data-stu-id="950e2-115">Find the right SAP Notes and installation guides, listed in the [Resources][sap-ha-guide-2] section.</span></span> <span data-ttu-id="950e2-116">Bu makalede SAP yükleme belgelerini tamamlar ve yardımcı olabilecek birincil kaynaklardır SAP notları yükleyip belirli platformlar SAP yazılımı dağıtın.</span><span class="sxs-lookup"><span data-stu-id="950e2-116">This article complements SAP installation documentation and SAP Notes, which are the primary resources that can help you install and deploy SAP software on specific platforms.</span></span>
* <span data-ttu-id="950e2-117">Azure Resource Manager dağıtım modeli ve Azure Klasik dağıtım modeli arasındaki farklar hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="950e2-117">Learn the differences between the Azure Resource Manager deployment model and the Azure classic deployment model.</span></span>
* <span data-ttu-id="950e2-118">Azure dağıtımınız için doğru modeli seçebilmeniz için Windows Server Yük Devretme Kümelemesi çekirdek modları hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="950e2-118">Learn about Windows Server Failover Clustering quorum modes, so you can select the model that is right for your Azure deployment.</span></span>
* <span data-ttu-id="950e2-119">Azure hizmetlerinde paylaşılan Windows Server Yük Devretme Kümelemesi depolama hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="950e2-119">Learn about Windows Server Failover Clustering shared storage in Azure services.</span></span>
* <span data-ttu-id="950e2-120">Başarısızlık durumunu tek nokta bileşenleri gibi gelişmiş iş uygulama programlama (ABAP) SAP merkezi Hizmetleri (ASCS) korunmasına yardımcı olmak öğrenin / SAP merkezi Hizmetleri (SCS) ve veritabanı yönetim sistemi (DBMS) ve yedek bileşenlerin gibi Azure SAP uygulama sunucusu.</span><span class="sxs-lookup"><span data-stu-id="950e2-120">Learn how to help protect single-point-of-failure components like Advanced Business Application Programming (ABAP) SAP Central Services (ASCS)/SAP Central Services (SCS) and database management systems (DBMS), and redundant components like SAP Application Server, in Azure.</span></span>
* <span data-ttu-id="950e2-121">Adım adım örnek bir yükleme ve bir Windows Server Yük Devretme Kümelemesi küme azure'da yüksek kullanılabilirlik SAP sisteminde yapılandırmasının, Azure Kaynak Yöneticisi'ni kullanarak izleyin.</span><span class="sxs-lookup"><span data-stu-id="950e2-121">Follow a step-by-step example of an installation and configuration of a high-availability SAP system in a Windows Server Failover Clustering cluster in Azure by using Azure Resource Manager.</span></span>
* <span data-ttu-id="950e2-122">Windows Server Yük Devretme Kümelemesi Azure ancak, bir şirket içi dağıtımda gerekli olmayan kullanmak için gerekli ek adımlar hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="950e2-122">Learn about additional steps required to use Windows Server Failover Clustering in Azure, but which are not needed in an on-premises deployment.</span></span>

<span data-ttu-id="950e2-123">Dağıtım ve yapılandırma, bu makalede, basitleştirmek için SAP üç katmanlı yüksek kullanılabilirlik Resource Manager şablonları kullanırız.</span><span class="sxs-lookup"><span data-stu-id="950e2-123">To simplify deployment and configuration, in this article, we use the SAP three-tier high-availability Resource Manager templates.</span></span> <span data-ttu-id="950e2-124">Şablonlar bir yüksek kullanılabilirlik SAP sistemi için gereksinim duyduğunuz tüm altyapının dağıtımını otomatik hale getirme.</span><span class="sxs-lookup"><span data-stu-id="950e2-124">The templates automate deployment of the entire infrastructure that you need for a high-availability SAP system.</span></span> <span data-ttu-id="950e2-125">Altyapı SAP uygulama performans standart (SAP) boyutlandırma SAP sisteminizin de destekler.</span><span class="sxs-lookup"><span data-stu-id="950e2-125">The infrastructure also supports SAP Application Performance Standard (SAPS) sizing of your SAP system.</span></span>

## <span data-ttu-id="950e2-126"><a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a>Önkoşulları</span><span class="sxs-lookup"><span data-stu-id="950e2-126"><a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a> Prerequisites</span></span>
<span data-ttu-id="950e2-127">Başlamadan önce aşağıdaki bölümlerde açıklanan önkoşulları karşıladığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="950e2-127">Before you start, make sure that you meet the prerequisites that are described in the following sections.</span></span> <span data-ttu-id="950e2-128">Ayrıca, listelenen tüm kaynakları kontrol ettiğinizden emin olun [kaynakları] [ sap-ha-guide-2] bölümü.</span><span class="sxs-lookup"><span data-stu-id="950e2-128">Also, be sure to check all resources listed in the [Resources][sap-ha-guide-2] section.</span></span>

<span data-ttu-id="950e2-129">Bu makalede, Azure Resource Manager şablonları için kullandığımız [üç katmanlı SAP NetWeaver yönetilen diskleri kullanarak](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md/).</span><span class="sxs-lookup"><span data-stu-id="950e2-129">In this article, we use Azure Resource Manager templates for [three-tier SAP NetWeaver using Managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md/).</span></span> <span data-ttu-id="950e2-130">Şablonları yararlı bir genel bakış için bkz: [SAP Azure Resource Manager şablonları](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/).</span><span class="sxs-lookup"><span data-stu-id="950e2-130">For a helpful overview of templates, see [SAP Azure Resource Manager templates](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/).</span></span>

## <span data-ttu-id="950e2-131"><a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a>Kaynakları</span><span class="sxs-lookup"><span data-stu-id="950e2-131"><a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a> Resources</span></span>
<span data-ttu-id="950e2-132">Bu makaleler Azure SAP dağıtımlarda kapsar:</span><span class="sxs-lookup"><span data-stu-id="950e2-132">These articles cover SAP deployments in Azure:</span></span>

* <span data-ttu-id="950e2-133">[Azure sanal makineleri planlama ve uygulama SAP NetWeaver için][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="950e2-133">[Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide]</span></span>
* <span data-ttu-id="950e2-134">[SAP NetWeaver için Azure sanal makineler dağıtımı][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="950e2-134">[Azure Virtual Machines deployment for SAP NetWeaver][deployment-guide]</span></span>
* <span data-ttu-id="950e2-135">[SAP NetWeaver için Azure sanal makineleri DBMS dağıtımı][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="950e2-135">[Azure Virtual Machines DBMS deployment for SAP NetWeaver][dbms-guide]</span></span>
* <span data-ttu-id="950e2-136">[Azure sanal makineler için yüksek oranda kullanılabilirlik SAP NetWeaver (Bu Kılavuzu)][sap-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="950e2-136">[Azure Virtual Machines high availability for SAP NetWeaver (this guide)][sap-ha-guide]</span></span>

> [!NOTE]
> <span data-ttu-id="950e2-137">Mümkün olduğunda, bir bağlantıya başvuran SAP Yükleme Kılavuzu'na sunuyoruz (bkz [SAP yükleme kılavuzları][sap-installation-guides]).</span><span class="sxs-lookup"><span data-stu-id="950e2-137">Whenever possible, we give you a link to the referring SAP installation guide (see the [SAP installation guides][sap-installation-guides]).</span></span> <span data-ttu-id="950e2-138">Önkoşullar ve yükleme işlemiyle ilgili bilgi için SAP NetWeaver yükleme kılavuzları dikkatle okuyun iyi bir fikirdir.</span><span class="sxs-lookup"><span data-stu-id="950e2-138">For prerequisites and information about the installation process, it's a good idea to read the SAP NetWeaver installation guides carefully.</span></span> <span data-ttu-id="950e2-139">Bu makalede yalnızca Azure sanal makineler ile kullanabileceğiniz SAP NetWeaver tabanlı sistemler için belirli görevler yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="950e2-139">This article covers only specific tasks for SAP NetWeaver-based systems that you can use with Azure Virtual Machines.</span></span>
>
>

<span data-ttu-id="950e2-140">Bu SAP Notlar Azure SAP konu ilişkili:</span><span class="sxs-lookup"><span data-stu-id="950e2-140">These SAP Notes are related to the topic of SAP in Azure:</span></span>

| <span data-ttu-id="950e2-141">Not numarası</span><span class="sxs-lookup"><span data-stu-id="950e2-141">Note number</span></span> | <span data-ttu-id="950e2-142">Başlık</span><span class="sxs-lookup"><span data-stu-id="950e2-142">Title</span></span> |
| --- | --- |
| <span data-ttu-id="950e2-143">[1928533]</span><span class="sxs-lookup"><span data-stu-id="950e2-143">[1928533]</span></span> |<span data-ttu-id="950e2-144">Azure üzerinde SAP uygulamaları: desteklenen ürünler ve boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="950e2-144">SAP Applications on Azure: Supported Products and Sizing</span></span> |
| <span data-ttu-id="950e2-145">[2015553]</span><span class="sxs-lookup"><span data-stu-id="950e2-145">[2015553]</span></span> |<span data-ttu-id="950e2-146">Microsoft Azure üzerinde SAP: Destek önkoşulları</span><span class="sxs-lookup"><span data-stu-id="950e2-146">SAP on Microsoft Azure: Support Prerequisites</span></span> |
| <span data-ttu-id="950e2-147">[1999351]</span><span class="sxs-lookup"><span data-stu-id="950e2-147">[1999351]</span></span> |<span data-ttu-id="950e2-148">Azure için SAP izleme Gelişmiş</span><span class="sxs-lookup"><span data-stu-id="950e2-148">Enhanced Azure Monitoring for SAP</span></span> |
| <span data-ttu-id="950e2-149">[2178632]</span><span class="sxs-lookup"><span data-stu-id="950e2-149">[2178632]</span></span> |<span data-ttu-id="950e2-150">Microsoft Azure üzerinde SAP için ölçümleri izleme anahtarı</span><span class="sxs-lookup"><span data-stu-id="950e2-150">Key Monitoring Metrics for SAP on Microsoft Azure</span></span> |
| <span data-ttu-id="950e2-151">[1999351]</span><span class="sxs-lookup"><span data-stu-id="950e2-151">[1999351]</span></span> |<span data-ttu-id="950e2-152">Windows sanallaştırma: İzleme Gelişmiş</span><span class="sxs-lookup"><span data-stu-id="950e2-152">Virtualization on Windows: Enhanced Monitoring</span></span> |
| <span data-ttu-id="950e2-153">[2243692]</span><span class="sxs-lookup"><span data-stu-id="950e2-153">[2243692]</span></span> |<span data-ttu-id="950e2-154">SAP DBMS örneği için Azure Premium SSD depolama kullanımı</span><span class="sxs-lookup"><span data-stu-id="950e2-154">Use of Azure Premium SSD Storage for SAP DBMS Instance</span></span> |

<span data-ttu-id="950e2-155">Daha fazla bilgi edinmek [Azure abonelikleri sınırlamaları][azure-subscription-service-limits-subscription]genel varsayılan sınırlamalar ve en fazla sınırlamalar dahil olmak üzere.</span><span class="sxs-lookup"><span data-stu-id="950e2-155">Learn more about the [limitations of Azure subscriptions][azure-subscription-service-limits-subscription], including general default limitations and maximum limitations.</span></span>

## <span data-ttu-id="950e2-156"><a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>Azure Klasik dağıtım modeli ve Azure Resource Manager ile yüksek kullanılabilirlik SAP</span><span class="sxs-lookup"><span data-stu-id="950e2-156"><a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>High-availability SAP with Azure Resource Manager vs. the Azure classic deployment model</span></span>
<span data-ttu-id="950e2-157">Azure Resource Manager ve Azure Klasik dağıtım modellerine aşağıdaki alanlarda farklıdır:</span><span class="sxs-lookup"><span data-stu-id="950e2-157">The Azure Resource Manager and Azure classic deployment models are different in the following areas:</span></span>

- <span data-ttu-id="950e2-158">Kaynak grupları</span><span class="sxs-lookup"><span data-stu-id="950e2-158">Resource groups</span></span>
- <span data-ttu-id="950e2-159">Azure kaynak grubu Azure iç yük dengeleyici bağımlılığı</span><span class="sxs-lookup"><span data-stu-id="950e2-159">Azure internal load balancer dependency on the Azure resource group</span></span>
- <span data-ttu-id="950e2-160">SAP çoklu SID senaryolar için destek</span><span class="sxs-lookup"><span data-stu-id="950e2-160">Support for SAP multi-SID scenarios</span></span>

### <span data-ttu-id="950e2-161"><a name="f76af273-1993-4d83-b12d-65deeae23686"></a>Kaynak grupları</span><span class="sxs-lookup"><span data-stu-id="950e2-161"><a name="f76af273-1993-4d83-b12d-65deeae23686"></a> Resource groups</span></span>
<span data-ttu-id="950e2-162">Azure Kaynak Yöneticisi'nde, Azure aboneliğinizde tüm uygulama kaynakları yönetmek için kaynak gruplarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="950e2-162">In Azure Resource Manager, you can use resource groups to manage all the application resources in your Azure subscription.</span></span> <span data-ttu-id="950e2-163">Tümleşik bir yaklaşım, aynı yaşam döngüsü tüm kaynaklar bir kaynak grubunda sahiptir.</span><span class="sxs-lookup"><span data-stu-id="950e2-163">An integrated approach, in a resource group, all resources have the same life cycle.</span></span> <span data-ttu-id="950e2-164">Örneğin, tüm kaynaklar aynı anda oluşturulur ve aynı anda silinir.</span><span class="sxs-lookup"><span data-stu-id="950e2-164">For example, all resources are created at the same time and they are deleted at the same time.</span></span> <span data-ttu-id="950e2-165">[Kaynak grupları](../../../azure-resource-manager/resource-group-overview.md#resource-groups) hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="950e2-165">Learn more about [resource groups](../../../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>

### <span data-ttu-id="950e2-166"><a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a>Azure kaynak grubu Azure iç yük dengeleyici bağımlılığı</span><span class="sxs-lookup"><span data-stu-id="950e2-166"><a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a> Azure internal load balancer dependency on the Azure resource group</span></span>

<span data-ttu-id="950e2-167">Azure Klasik dağıtım modelinde Azure iç yük dengeleyici (Azure Yük Dengeleyici Hizmeti) ve bulut hizmeti arasında bir bağımlılık yoktur.</span><span class="sxs-lookup"><span data-stu-id="950e2-167">In the Azure classic deployment model, there is a dependency between the Azure internal load balancer (Azure Load Balancer service) and the cloud service.</span></span> <span data-ttu-id="950e2-168">Her iç yük dengeleyici bir bulut hizmeti gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="950e2-168">Every internal load balancer needs one cloud service.</span></span>

<span data-ttu-id="950e2-169">Azure Kaynak Yöneticisi'nde, her Azure kaynak bir Azure kaynak grubu yerleştirilmesi gerekir ve bu da Azure yük dengeleyici için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="950e2-169">In Azure Resource Manager, every Azure resource needs to be placed into an Azure resource group, and this is valid for Azure Load Balancer as well.</span></span> <span data-ttu-id="950e2-170">Ancak, Azure yük dengeleyici başına bir Azure kaynak grubu için gerek yoktur, örneğin bir Azure kaynak grubu birden çok Azure yük Dengeleyiciler içerebilir.</span><span class="sxs-lookup"><span data-stu-id="950e2-170">However, there is no need to have one Azure resource group per Azure load balancer, e.g. one Azure resource group can contain multiple Azure Load Balancers.</span></span> <span data-ttu-id="950e2-171">, Daha basit ve daha esnek ortamıdır.</span><span class="sxs-lookup"><span data-stu-id="950e2-171">The environment is simpler and more flexible.</span></span> 

### <a name="support-for-sap-multi-sid-scenarios"></a><span data-ttu-id="950e2-172">SAP çoklu SID senaryolar için destek</span><span class="sxs-lookup"><span data-stu-id="950e2-172">Support for SAP multi-SID scenarios</span></span>

<span data-ttu-id="950e2-173">Azure Kaynak Yöneticisi'nde, birden çok SAP sistem tanımlayıcısı (SID) ASCS/SCS örnekleri bir küme içinde yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="950e2-173">In Azure Resource Manager, you can install multiple SAP system identifier (SID) ASCS/SCS instances in one cluster.</span></span> <span data-ttu-id="950e2-174">Çoklu SID örnekleri her Azure iç yük dengeleyici için birden fazla IP adresine yönelik destek nedeniyle mümkündür.</span><span class="sxs-lookup"><span data-stu-id="950e2-174">Multi-SID instances are possible because of support for multiple IP addresses for each Azure internal load balancer.</span></span>

<span data-ttu-id="950e2-175">Azure Klasik dağıtım modelini kullanmak için açıklanan yordamları izleyin [SAP NetWeaver azure'da: SIOS DataKeeper ile azure'da Windows Server Yük Devretme Kümelemesi kullanarak SAP ASCS/SCS kümeleme örneklerini](http://go.microsoft.com/fwlink/?LinkId=613056).</span><span class="sxs-lookup"><span data-stu-id="950e2-175">To use the Azure classic deployment model, follow the procedures described in [SAP NetWeaver in Azure: Clustering SAP ASCS/SCS instances by using Windows Server Failover Clustering in Azure with SIOS DataKeeper](http://go.microsoft.com/fwlink/?LinkId=613056).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="950e2-176">SAP yüklemeleri için Azure Resource Manager dağıtım modeli kullanmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="950e2-176">We strongly recommend that you use the Azure Resource Manager deployment model for your SAP installations.</span></span> <span data-ttu-id="950e2-177">Klasik dağıtım modelinde bulunmayan birçok avantaj sunar.</span><span class="sxs-lookup"><span data-stu-id="950e2-177">It offers many benefits that are not available in the classic deployment model.</span></span> <span data-ttu-id="950e2-178">Azure hakkında daha fazla bilgi [dağıtım modellerini][virtual-machines-azure-resource-manager-architecture-benefits-arm].</span><span class="sxs-lookup"><span data-stu-id="950e2-178">Learn more about Azure [deployment models][virtual-machines-azure-resource-manager-architecture-benefits-arm].</span></span>   
>
>

## <span data-ttu-id="950e2-179"><a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a>Windows Server Yük Devretme Kümelemesi</span><span class="sxs-lookup"><span data-stu-id="950e2-179"><a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a> Windows Server Failover Clustering</span></span>
<span data-ttu-id="950e2-180">Windows Server Yük Devretme Kümelemesi, yüksek kullanılabilirlik SAP ASCS/SCS yükleme ve Windows'da DBMS temelidir.</span><span class="sxs-lookup"><span data-stu-id="950e2-180">Windows Server Failover Clustering is the foundation of a high-availability SAP ASCS/SCS installation and DBMS in Windows.</span></span>

<span data-ttu-id="950e2-181">Bir yük devretme kümesi, uygulamaların ve hizmetlerin kullanılabilirliğini artırmak için birlikte çalışan 1 + n bağımsız sunucular (düğümler) grubudur.</span><span class="sxs-lookup"><span data-stu-id="950e2-181">A failover cluster is a group of 1+n independent servers (nodes) that work together to increase the availability of applications and services.</span></span> <span data-ttu-id="950e2-182">Bir düğüm hatası oluşursa, Windows Server Yük Devretme Kümelemesi uygulamaları ve hizmetleri sağlamak için iyi bir küme korurken oluşabilir sayısı hesaplar.</span><span class="sxs-lookup"><span data-stu-id="950e2-182">If a node failure occurs, Windows Server Failover Clustering calculates the number of failures that can occur while maintaining a healthy cluster to provide applications and services.</span></span> <span data-ttu-id="950e2-183">Yük Devretme Kümelemesi elde etmek için farklı bir çekirdek modlarından seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="950e2-183">You can choose from different quorum modes to achieve failover clustering.</span></span>

### <span data-ttu-id="950e2-184"><a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a>Çekirdek modu</span><span class="sxs-lookup"><span data-stu-id="950e2-184"><a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a> Quorum modes</span></span>
<span data-ttu-id="950e2-185">Windows Server Yük Devretme Kümelemesi kullanırken dört çekirdek modlarından seçim yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="950e2-185">You can choose from four quorum modes when you use Windows Server Failover Clustering:</span></span>

* <span data-ttu-id="950e2-186">**Düğüm çoğunluğu**.</span><span class="sxs-lookup"><span data-stu-id="950e2-186">**Node Majority**.</span></span> <span data-ttu-id="950e2-187">Kümedeki her düğüm oy kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="950e2-187">Each node of the cluster can vote.</span></span> <span data-ttu-id="950e2-188">Küme yalnızca oyları, çoğunu ile başka bir deyişle, yarısından fazlası oyları ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="950e2-188">The cluster functions only with a majority of votes, that is, with more than half the votes.</span></span> <span data-ttu-id="950e2-189">Bu seçenek eşit sayıda düğüme sahip kümeler için önerilir.</span><span class="sxs-lookup"><span data-stu-id="950e2-189">We recommend this option for clusters that have an uneven number of nodes.</span></span> <span data-ttu-id="950e2-190">Örneğin, üç yedi düğümlü bir küme düğümünde başarısız olabilir ve küme durağan Çoğunluk erişir ve çalışmaya devam eder.</span><span class="sxs-lookup"><span data-stu-id="950e2-190">For example, three nodes in a seven-node cluster can fail, and the cluster stills achieves a majority and continues to run.</span></span>  
* <span data-ttu-id="950e2-191">**Düğüm ve Disk Çoğunluğu**.</span><span class="sxs-lookup"><span data-stu-id="950e2-191">**Node and Disk Majority**.</span></span> <span data-ttu-id="950e2-192">Her düğüm ve küme depolama alanındaki ayrılan disk (bir disk tanığı) ne zaman kullanılabilir olduğunu ve iletişim oy kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="950e2-192">Each node and a designated disk (a disk witness) in the cluster storage can vote when they are available and in communication.</span></span> <span data-ttu-id="950e2-193">Küme yalnızca oyları çoğunu ile başka bir deyişle, yarısından fazlası oyları ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="950e2-193">The cluster functions only with a majority of the votes, that is, with more than half the votes.</span></span> <span data-ttu-id="950e2-194">Bu mod, bir küme ortamında düğümlerinin çift sayıda mantıklıdır.</span><span class="sxs-lookup"><span data-stu-id="950e2-194">This mode makes sense in a cluster environment with an even number of nodes.</span></span> <span data-ttu-id="950e2-195">Yarı düğüm ve disk çevrimiçi ise, küme sağlam durumda kalır.</span><span class="sxs-lookup"><span data-stu-id="950e2-195">If half the nodes and the disk are online, the cluster remains in a healthy state.</span></span>
* <span data-ttu-id="950e2-196">**Düğüm ve dosya paylaşımı çoğunluğu**.</span><span class="sxs-lookup"><span data-stu-id="950e2-196">**Node and File Share Majority**.</span></span> <span data-ttu-id="950e2-197">Her düğüm artı yönetici oluşturur bir dosya paylaşımı (dosya paylaşım tanığı), düğümler ve dosya paylaşımı kullanılabilir ve iletişimde oy kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="950e2-197">Each node plus a designated file share (a file share witness) that the administrator creates can vote, regardless of whether the nodes and file share are available and in communication.</span></span> <span data-ttu-id="950e2-198">Küme yalnızca oyları çoğunu ile başka bir deyişle, yarısından fazlası oyları ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="950e2-198">The cluster functions only with a majority of the votes, that is, with more than half the votes.</span></span> <span data-ttu-id="950e2-199">Bu mod, bir küme ortamında düğümlerinin çift sayıda mantıklıdır.</span><span class="sxs-lookup"><span data-stu-id="950e2-199">This mode makes sense in a cluster environment with an even number of nodes.</span></span> <span data-ttu-id="950e2-200">Düğüm ve Disk Çoğunluğu moduna benzer, ancak Tanık diski yerine bir Tanık dosya paylaşımı kullanır.</span><span class="sxs-lookup"><span data-stu-id="950e2-200">It's similar to the Node and Disk Majority mode, but it uses a witness file share instead of a witness disk.</span></span> <span data-ttu-id="950e2-201">Bu mod uygulanması kolaydır, ancak dosya paylaşımı kendisini yüksek oranda kullanılabilir değil, tek bir hata noktası olabilir.</span><span class="sxs-lookup"><span data-stu-id="950e2-201">This mode is easy to implement, but if the file share itself is not highly available, it might become a single point of failure.</span></span>
* <span data-ttu-id="950e2-202">**Çoğunluk yok: Yalnızca Disk**.</span><span class="sxs-lookup"><span data-stu-id="950e2-202">**No Majority: Disk Only**.</span></span> <span data-ttu-id="950e2-203">Bir düğüm kullanılabilir ve küme depolama alanındaki belirli bir diskle iletişimi ise küme çekirdeği vardır.</span><span class="sxs-lookup"><span data-stu-id="950e2-203">The cluster has a quorum if one node is available and in communication with a specific disk in the cluster storage.</span></span> <span data-ttu-id="950e2-204">Ayrıca, disk ile iletişimi olan düğümler kümeye katılabilir.</span><span class="sxs-lookup"><span data-stu-id="950e2-204">Only the nodes that also are in communication with that disk can join the cluster.</span></span> <span data-ttu-id="950e2-205">Bu mod kullanmamanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="950e2-205">We recommend that you do not use this mode.</span></span>
 

## <span data-ttu-id="950e2-206"><a name="fdfee875-6e66-483a-a343-14bbaee33275"></a>Şirket içi Windows Server Yük devretme</span><span class="sxs-lookup"><span data-stu-id="950e2-206"><a name="fdfee875-6e66-483a-a343-14bbaee33275"></a> Windows Server Failover Clustering on-premises</span></span>
<span data-ttu-id="950e2-207">Şekil 1 iki düğümden oluşan bir küme gösterir.</span><span class="sxs-lookup"><span data-stu-id="950e2-207">Figure 1 shows a cluster of two nodes.</span></span> <span data-ttu-id="950e2-208">Düğüm başarısız olur ve hem düğümleri Kal yukarı ve çalışan, bir çekirdek disk veya dosya arasında ağ bağlantısı paylaşırsanız, hangi düğümün kümenin uygulamaları ve hizmetleri sağlamaya devam edecek belirler.</span><span class="sxs-lookup"><span data-stu-id="950e2-208">If the network connection between the nodes fails and both nodes stay up and running, a quorum disk or file share determines which node will continue to provide the cluster's applications and services.</span></span> <span data-ttu-id="950e2-209">Çekirdek disk veya dosya paylaşımına erişimi olduğundan düğüm Hizmetleri devam etmenizi sağlayan olandır.</span><span class="sxs-lookup"><span data-stu-id="950e2-209">The node that has access to the quorum disk or file share is the node that ensures that services continue.</span></span>

<span data-ttu-id="950e2-210">Bu örnek iki düğümlü bir küme kullandığından, düğüm ve dosya paylaşımı çoğunluğu çekirdek modu kullanırız.</span><span class="sxs-lookup"><span data-stu-id="950e2-210">Because this example uses a two-node cluster, we use the Node and File Share Majority quorum mode.</span></span> <span data-ttu-id="950e2-211">Düğüm ve Disk Çoğunluğu geçerli bir seçenek de değil.</span><span class="sxs-lookup"><span data-stu-id="950e2-211">The Node and Disk Majority also is a valid option.</span></span> <span data-ttu-id="950e2-212">Bir üretim ortamında, bir çekirdek disk kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="950e2-212">In a production environment, we recommend that you use a quorum disk.</span></span> <span data-ttu-id="950e2-213">Yüksek oranda kullanılabilir yapmak için ağ ve depolama sistemi teknolojisi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="950e2-213">You can use network and storage system technology to make it highly available.</span></span>

![Şekil 1: Bir Windows Server Yük Devretme Kümelemesi yapılandırma için SAP ASCS/SCS Azure örneği][sap-ha-guide-figure-1000]

<span data-ttu-id="950e2-215">_**Şekil 1:** bir Windows Server Yük Devretme Kümelemesi yapılandırma için SAP ASCS/SCS Azure örneği_</span><span class="sxs-lookup"><span data-stu-id="950e2-215">_**Figure 1:** Example of a Windows Server Failover Clustering configuration for SAP ASCS/SCS in Azure_</span></span>

### <span data-ttu-id="950e2-216"><a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a>Paylaşılan depolama alanı</span><span class="sxs-lookup"><span data-stu-id="950e2-216"><a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a> Shared storage</span></span>
<span data-ttu-id="950e2-217">Şekil 1 iki düğümlü paylaşılan depolama kümesi ayrıca gösterir.</span><span class="sxs-lookup"><span data-stu-id="950e2-217">Figure 1 also shows a two-node shared storage cluster.</span></span> <span data-ttu-id="950e2-218">Bir şirket içi paylaşılan depolama Küme Paylaşılan depolama alanı kümedeki tüm düğümlerin algıla.</span><span class="sxs-lookup"><span data-stu-id="950e2-218">In an on-premises shared storage cluster, all nodes in the cluster detect shared storage.</span></span> <span data-ttu-id="950e2-219">Kilitleme mekanizması veri bozulmaya karşı korur.</span><span class="sxs-lookup"><span data-stu-id="950e2-219">A locking mechanism protects the data from corruption.</span></span> <span data-ttu-id="950e2-220">Tüm düğümler, başka bir düğüm başarısız olursa algılayabilir.</span><span class="sxs-lookup"><span data-stu-id="950e2-220">All nodes can detect if another node fails.</span></span> <span data-ttu-id="950e2-221">Bir düğüm başarısız olursa, kalan düğümü depolama kaynakları aittir ve hizmetlerin kullanılabilirliğini sağlar.</span><span class="sxs-lookup"><span data-stu-id="950e2-221">If one node fails, the remaining node takes ownership of the storage resources and ensures the availability of services.</span></span>

> [!NOTE]
> <span data-ttu-id="950e2-222">SQL Server ile gibi bazı DBMS uygulamalarla yüksek kullanılabilirlik için Paylaşılan diskleri gerekmez.</span><span class="sxs-lookup"><span data-stu-id="950e2-222">You don't need shared disks for high availability with some DBMS applications, like with SQL Server.</span></span> <span data-ttu-id="950e2-223">SQL Server Always On başka bir küme düğümüne yerel diske bir küme düğümünde yerel diskten DBMS veri ve günlük dosyalarını çoğaltır.</span><span class="sxs-lookup"><span data-stu-id="950e2-223">SQL Server Always On replicates DBMS data and log files from the local disk of one cluster node to the local disk of another cluster node.</span></span> <span data-ttu-id="950e2-224">Bu durumda, paylaşılan bir disk Windows Küme yapılandırması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="950e2-224">In that case, the Windows cluster configuration doesn't need a shared disk.</span></span>
>
>

### <span data-ttu-id="950e2-225"><a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a>Ağ ve ad çözümlemesi</span><span class="sxs-lookup"><span data-stu-id="950e2-225"><a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a> Networking and name resolution</span></span>
<span data-ttu-id="950e2-226">İstemci bilgisayarlar, bir sanal IP adresi ve DNS sunucusu sağlayan bir sanal ana bilgisayar adı üzerinden küme ulaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="950e2-226">Client computers reach the cluster over a virtual IP address and a virtual host name that the DNS server provides.</span></span> <span data-ttu-id="950e2-227">Şirket içi düğümler ve DNS sunucusu birden çok IP adresi işleyebilir.</span><span class="sxs-lookup"><span data-stu-id="950e2-227">The on-premises nodes and the DNS server can handle multiple IP addresses.</span></span>

<span data-ttu-id="950e2-228">Tipik bir kurulumunda iki veya daha fazla ağ bağlantıları kullanın:</span><span class="sxs-lookup"><span data-stu-id="950e2-228">In a typical setup, you use two or more network connections:</span></span>

* <span data-ttu-id="950e2-229">Depolama için ayrılmış bir bağlantı</span><span class="sxs-lookup"><span data-stu-id="950e2-229">A dedicated connection to the storage</span></span>
* <span data-ttu-id="950e2-230">Sinyal için bir küme iç ağ bağlantısı</span><span class="sxs-lookup"><span data-stu-id="950e2-230">A cluster-internal network connection for the heartbeat</span></span>
* <span data-ttu-id="950e2-231">İstemcilerin kümeye bağlanmak için kullandığı bir ortak ağ</span><span class="sxs-lookup"><span data-stu-id="950e2-231">A public network that clients use to connect to the cluster</span></span>

## <span data-ttu-id="950e2-232"><a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a>Azure'da Windows Server Yük devretme</span><span class="sxs-lookup"><span data-stu-id="950e2-232"><a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a> Windows Server Failover Clustering in Azure</span></span>
<span data-ttu-id="950e2-233">Çıplak metal veya özel bulut dağıtımları karşılaştırıldığında, Azure sanal makineleri Windows Server Yük Devretme Kümelemesi yapılandırmak için ek adımlar gerektirir.</span><span class="sxs-lookup"><span data-stu-id="950e2-233">Compared to bare metal or private cloud deployments, Azure Virtual Machines requires additional steps to configure Windows Server Failover Clustering.</span></span> <span data-ttu-id="950e2-234">Paylaşılan bir küme diski oluşturma sırasında birkaç IP adresleri ve sanal ana bilgisayar adları SAP ASCS/SCS örneği için ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="950e2-234">When you build a shared cluster disk, you need to set several IP addresses and virtual host names for the SAP ASCS/SCS instance.</span></span>

<span data-ttu-id="950e2-235">Bu makalede, temel kavramları ve Azure bir SAP yüksek kullanılabilirlik merkezi Hizmetleri küme oluşturmak için gereken ek adımlar açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="950e2-235">In this article, we discuss key concepts and the additional steps required to build an SAP high-availability central services cluster in Azure.</span></span> <span data-ttu-id="950e2-236">Üçüncü taraf aracı SIOS DataKeeper ayarlamak nasıl ve Azure iç yük dengeleyici yapılandırmak nasıl gösteriyoruz.</span><span class="sxs-lookup"><span data-stu-id="950e2-236">We show you how to set up the third-party tool SIOS DataKeeper, and how to configure the Azure internal load balancer.</span></span> <span data-ttu-id="950e2-237">Dosya paylaşım tanığı Azure ile Windows Yük devretme kümesi oluşturmak için bu araçları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="950e2-237">You can use these tools to create a Windows failover cluster with a file share witness in Azure.</span></span>

![Şekil 2: Windows Server Yük devretme kümeleme yapılandırmasında Azure olmayan paylaşılan bir disk][sap-ha-guide-figure-1001]

<span data-ttu-id="950e2-239">_**Şekil 2:** Windows Server Yük devretme kümeleme yapılandırmasında Azure olmayan paylaşılan bir disk_</span><span class="sxs-lookup"><span data-stu-id="950e2-239">_**Figure 2:** Windows Server Failover Clustering configuration in Azure without a shared disk_</span></span>

### <span data-ttu-id="950e2-240"><a name="1a464091-922b-48d7-9d08-7cecf757f341"></a>Paylaşılan disk Azure ile SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="950e2-240"><a name="1a464091-922b-48d7-9d08-7cecf757f341"></a> Shared disk in Azure with SIOS DataKeeper</span></span>
<span data-ttu-id="950e2-241">Yüksek kullanılabilirlik SAP ASCS/SCS örneği için paylaşılan depolama küme.</span><span class="sxs-lookup"><span data-stu-id="950e2-241">You need cluster shared storage for a high-availability SAP ASCS/SCS instance.</span></span> <span data-ttu-id="950e2-242">Eylül 2016 itibariyle Azure paylaşılan depolama küme oluşturmak için kullanabileceğiniz paylaşılan depolama sunmuyor.</span><span class="sxs-lookup"><span data-stu-id="950e2-242">As of September 2016, Azure doesn't offer shared storage that you can use to create a shared storage cluster.</span></span> <span data-ttu-id="950e2-243">Üçüncü taraf yazılım SIOS DataKeeper Cluster Edition, Küme Paylaşılan depolama benzetim yansıtılmış bir depolama alanı oluşturmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="950e2-243">You can use third-party software SIOS DataKeeper Cluster Edition to create a mirrored storage that simulates cluster shared storage.</span></span> <span data-ttu-id="950e2-244">Gerçek zamanlı zaman uyumlu veri çoğaltma SIOS çözümü sağlar.</span><span class="sxs-lookup"><span data-stu-id="950e2-244">The SIOS solution provides real-time synchronous data replication.</span></span> <span data-ttu-id="950e2-245">Bu küme için paylaşılan disk kaynağı nasıl oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="950e2-245">This is how you can create a shared disk resource for a cluster:</span></span>

1. <span data-ttu-id="950e2-246">Windows küme yapılandırmasında sanal makinelerinin (VM'ler) her biri için ek bir disk ekleyin.</span><span class="sxs-lookup"><span data-stu-id="950e2-246">Attach an additional disk to each of the virtual machines (VMs) in a Windows cluster configuration.</span></span>
2. <span data-ttu-id="950e2-247">SIOS DataKeeper Cluster Edition her iki sanal makine düğümde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="950e2-247">Run SIOS DataKeeper Cluster Edition on both virtual machine nodes.</span></span>
3. <span data-ttu-id="950e2-248">Hedef sanal makineye bağlı ek disk birimi kaynak sanal makinedeki bağlı ek disk birimi içeriği yansıtan SIOS DataKeeper Cluster Edition yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="950e2-248">Configure SIOS DataKeeper Cluster Edition so that it mirrors the content of the additional disk attached volume from the source virtual machine to the additional disk attached volume of the target virtual machine.</span></span> <span data-ttu-id="950e2-249">SIOS DataKeeper kaynak ve hedef yerel birimleri soyutlar ve Windows Server Yük Devretme Kümelemesi bir paylaşılan disk için gösterir.</span><span class="sxs-lookup"><span data-stu-id="950e2-249">SIOS DataKeeper abstracts the source and target local volumes, and then presents them to Windows Server Failover Clustering as one shared disk.</span></span>

<span data-ttu-id="950e2-250">Hakkında daha fazla bilgi almak [SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/).</span><span class="sxs-lookup"><span data-stu-id="950e2-250">Get more information about [SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/).</span></span>

![Şekil 3: Windows Server Yük devretme kümeleme yapılandırmasında SIOS DataKeeper ile Azure][sap-ha-guide-figure-1002]

<span data-ttu-id="950e2-252">_**Şekil 3:** SIOS DataKeeper ile azure'da Windows Server Yük Devretme Kümelemesi yapılandırma_</span><span class="sxs-lookup"><span data-stu-id="950e2-252">_**Figure 3:** Windows Server Failover Clustering configuration in Azure with SIOS DataKeeper_</span></span>

> [!NOTE]
> <span data-ttu-id="950e2-253">SQL Server gibi bazı DBMS ürünleri ile yüksek kullanılabilirlik için Paylaşılan diskleri gerekmez.</span><span class="sxs-lookup"><span data-stu-id="950e2-253">You don't need shared disks for high availability with some DBMS products, like SQL Server.</span></span> <span data-ttu-id="950e2-254">SQL Server Always On başka bir küme düğümüne yerel diske bir küme düğümünde yerel diskten DBMS veri ve günlük dosyalarını çoğaltır.</span><span class="sxs-lookup"><span data-stu-id="950e2-254">SQL Server Always On replicates DBMS data and log files from the local disk of one cluster node to the local disk of another cluster node.</span></span> <span data-ttu-id="950e2-255">Bu durumda, paylaşılan bir disk Windows Küme yapılandırması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="950e2-255">In this case, the Windows cluster configuration doesn't need a shared disk.</span></span>
>
>

### <span data-ttu-id="950e2-256"><a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a>Azure ad çözümleme</span><span class="sxs-lookup"><span data-stu-id="950e2-256"><a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a> Name resolution in Azure</span></span>
<span data-ttu-id="950e2-257">Azure bulut platformu kayan IP adresleri gibi sanal IP adreslerini yapılandırma seçeneği sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="950e2-257">The Azure cloud platform doesn't offer the option to configure virtual IP addresses, such as floating IP addresses.</span></span> <span data-ttu-id="950e2-258">Küme kaynağı bulutta ulaşmak için sanal bir IP adresi ayarlamak için alternatif bir çözüm gerekir.</span><span class="sxs-lookup"><span data-stu-id="950e2-258">You need an alternative solution to set up a virtual IP address to reach the cluster resource in the cloud.</span></span>
<span data-ttu-id="950e2-259">Azure Azure yük dengeleyici hizmetinde bir iç yük dengeleyici sahiptir.</span><span class="sxs-lookup"><span data-stu-id="950e2-259">Azure has an internal load balancer in the Azure Load Balancer service.</span></span> <span data-ttu-id="950e2-260">İç yük dengeleyici ile istemcileri kümenin küme sanal IP adresi ulaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="950e2-260">With the internal load balancer, clients reach the cluster over the cluster virtual IP address.</span></span>
<span data-ttu-id="950e2-261">Küme düğümleri içeren kaynak grubunda iç yük dengeleyicisi dağıtmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="950e2-261">You need to deploy the internal load balancer in the resource group that contains the cluster nodes.</span></span> <span data-ttu-id="950e2-262">Ardından, kuralları araştırmasıyla iç yük dengeleyicisi bağlantı noktaları iletme tüm gerekli bağlantı noktası yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="950e2-262">Then, configure all necessary port forwarding rules with the probe ports of the internal load balancer.</span></span>
<span data-ttu-id="950e2-263">İstemcileri sanal ana bilgisayar adını bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="950e2-263">The clients can connect via the virtual host name.</span></span> <span data-ttu-id="950e2-264">DNS sunucusu küme IP adresi ve kümesinin etkin düğümü iletme iç yük dengeleyici tanıtıcıları bağlantı noktası çözümler.</span><span class="sxs-lookup"><span data-stu-id="950e2-264">The DNS server resolves the cluster IP address, and the internal load balancer handles port forwarding to the active node of the cluster.</span></span>

## <span data-ttu-id="950e2-265"><a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a>SAP NetWeaver yüksek kullanılabilirlik Azure altyapısı olarak-hizmet (Iaas)</span><span class="sxs-lookup"><span data-stu-id="950e2-265"><a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a> SAP NetWeaver high availability in Azure Infrastructure-as-a-Service (IaaS)</span></span>
<span data-ttu-id="950e2-266">SAP yazılım bileşenleri için SAP uygulama yüksek kullanılabilirlik, gibi elde etmek için aşağıdaki bileşenler korumak gerekir:</span><span class="sxs-lookup"><span data-stu-id="950e2-266">To achieve SAP application high availability, such as for SAP software components, you need to protect the following components:</span></span>

* <span data-ttu-id="950e2-267">SAP uygulama sunucusu örneği</span><span class="sxs-lookup"><span data-stu-id="950e2-267">SAP Application Server instance</span></span>
* <span data-ttu-id="950e2-268">SAP ASCS/SCS örneği</span><span class="sxs-lookup"><span data-stu-id="950e2-268">SAP ASCS/SCS instance</span></span>
* <span data-ttu-id="950e2-269">DBMS sunucu</span><span class="sxs-lookup"><span data-stu-id="950e2-269">DBMS server</span></span>

<span data-ttu-id="950e2-270">Yüksek kullanılabilirlik senaryolarını SAP bileşenlerinde koruma hakkında daha fazla bilgi için bkz: [Azure sanal makineleri planlama ve uygulama SAP NetWeaver için][planning-guide-11].</span><span class="sxs-lookup"><span data-stu-id="950e2-270">For more information about protecting SAP components in high-availability scenarios, see [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide-11].</span></span>

### <span data-ttu-id="950e2-271"><a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a>Yüksek kullanılabilirlik SAP uygulama sunucusu</span><span class="sxs-lookup"><span data-stu-id="950e2-271"><a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a> High-availability SAP Application Server</span></span>
<span data-ttu-id="950e2-272">SAP uygulama sunucusu ile iletişim örnekleri için belirli bir yüksek kullanılabilirlik çözümü genellikle gerekmez.</span><span class="sxs-lookup"><span data-stu-id="950e2-272">You usually don't need a specific high-availability solution for the SAP Application Server and dialog instances.</span></span> <span data-ttu-id="950e2-273">Artıklık tarafından yüksek kullanılabilirlik elde etmek ve iletişim birden çok başka durumlarda, Azure sanal makineleri yapılandıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="950e2-273">You achieve high availability by redundancy, and you'll configure multiple dialog instances in different instances of Azure Virtual Machines.</span></span> <span data-ttu-id="950e2-274">İki durumlarda, Azure sanal makinelerinde yüklü en az iki SAP uygulama örneğinin olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="950e2-274">You should have at least two SAP application instances installed in two instances of Azure Virtual Machines.</span></span>

![Şekil 4: Yüksek oranda kullanılabilirlik SAP uygulama sunucusu][sap-ha-guide-figure-2000]

<span data-ttu-id="950e2-276">_**Şekil 4:** yüksek kullanılabilirlik SAP uygulama sunucusu_</span><span class="sxs-lookup"><span data-stu-id="950e2-276">_**Figure 4:** High-availability SAP Application Server_</span></span>

<span data-ttu-id="950e2-277">Ana bilgisayar SAP uygulama sunucusu örneklerinin aynı Azure kullanılabilirlik kümesi tüm sanal makineler yerleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="950e2-277">You must place all virtual machines that host SAP Application Server instances in the same Azure availability set.</span></span> <span data-ttu-id="950e2-278">Bir Azure kullanılabilirlik kümesi sağlar:</span><span class="sxs-lookup"><span data-stu-id="950e2-278">An Azure availability set ensures that:</span></span>

* <span data-ttu-id="950e2-279">Tüm sanal makineleri aynı yükseltme etki alanı'nın bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="950e2-279">All virtual machines are part of the same upgrade domain.</span></span> <span data-ttu-id="950e2-280">Bir yükseltme etki alanı, örneğin, sanal makineler planlı bakım kapalı kalma süresi sırasında aynı anda güncelleştirilmemiş emin olur.</span><span class="sxs-lookup"><span data-stu-id="950e2-280">An upgrade domain, for example, makes sure that the virtual machines aren't updated at the same time during planned maintenance downtime.</span></span>
* <span data-ttu-id="950e2-281">Tüm sanal makineleri aynı hata etki alanı'nın bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="950e2-281">All virtual machines are part of the same fault domain.</span></span> <span data-ttu-id="950e2-282">Hata etki alanı, örneğin, böylece hiç tek hata noktası tüm sanal makinelerin kullanılabilirliğini etkiler dağıtılan sanal makineler olduğundan emin olur.</span><span class="sxs-lookup"><span data-stu-id="950e2-282">A fault domain, for example, makes sure that virtual machines are deployed so that no single point of failure affects the availability of all virtual machines.</span></span>

<span data-ttu-id="950e2-283">Nasıl yapılır hakkında daha fazla bilgi [sanal makinelerin kullanılabilirliğini yönetme][virtual-machines-manage-availability].</span><span class="sxs-lookup"><span data-stu-id="950e2-283">Learn more about how to [manage the availability of virtual machines][virtual-machines-manage-availability].</span></span>

<span data-ttu-id="950e2-284">Yalnızca yönetilmeyen disk: Azure depolama hesabına olası tek hata noktası olduğundan, en az iki sanal makineye dağıtılır, en az iki Azure depolama hesabınızın olması önemlidir.</span><span class="sxs-lookup"><span data-stu-id="950e2-284">Unmanaged disk only: Because the Azure storage account is a potential single point of failure, it's important to have at least two Azure storage accounts, in which at least two virtual machines are distributed.</span></span> <span data-ttu-id="950e2-285">İdeal bir kurulumunda SAP iletişim örneği çalıştıran her bir sanal makine disklerinin farklı depolama hesabında dağıtılması.</span><span class="sxs-lookup"><span data-stu-id="950e2-285">In an ideal setup, the disks of each virtual machine that is running an SAP dialog instance would be deployed in a different storage account.</span></span>

### <span data-ttu-id="950e2-286"><a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a>Yüksek kullanılabilirlik SAP ASCS/SCS örneği</span><span class="sxs-lookup"><span data-stu-id="950e2-286"><a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a> High-availability SAP ASCS/SCS instance</span></span>
<span data-ttu-id="950e2-287">Şekil 5, yüksek kullanılabilirlik SAP ASCS/SCS örneğinin bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="950e2-287">Figure 5 is an example of a high-availability SAP ASCS/SCS instance.</span></span>

![Şekil 5: Yüksek oranda kullanılabilirlik SAP ASCS/SCS örneği][sap-ha-guide-figure-2001]

<span data-ttu-id="950e2-289">_**Şekil 5:** yüksek kullanılabilirlik SAP ASCS/SCS örneği_</span><span class="sxs-lookup"><span data-stu-id="950e2-289">_**Figure 5:** High-availability SAP ASCS/SCS instance_</span></span>

#### <span data-ttu-id="950e2-290"><a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a>Windows Server Yük Devretme Kümelemesi Azure ile yüksek kullanılabilirlik SAP ASCS/SCS örneği</span><span class="sxs-lookup"><span data-stu-id="950e2-290"><a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a> SAP ASCS/SCS instance high availability with Windows Server Failover Clustering in Azure</span></span>
<span data-ttu-id="950e2-291">Çıplak metal veya özel bulut dağıtımları karşılaştırıldığında, Azure sanal makineleri Windows Server Yük Devretme Kümelemesi yapılandırmak için ek adımlar gerektirir.</span><span class="sxs-lookup"><span data-stu-id="950e2-291">Compared to bare metal or private cloud deployments, Azure Virtual Machines requires additional steps to configure Windows Server Failover Clustering.</span></span> <span data-ttu-id="950e2-292">Windows Yük devretme kümesi oluşturmak için paylaşılan bir küme diski, birden fazla IP adresi, birçok sanal ana bilgisayar adlarını ve Azure iç yük dengeleyiciye SAP ASCS/SCS örneği kümeleme için gerekir.</span><span class="sxs-lookup"><span data-stu-id="950e2-292">To build a Windows failover cluster, you need a shared cluster disk, several IP addresses, several virtual host names, and an Azure internal load balancer for clustering an SAP ASCS/SCS instance.</span></span> <span data-ttu-id="950e2-293">Biz bu makalenin sonraki bölümlerinde daha ayrıntılı ele alınmıştır.</span><span class="sxs-lookup"><span data-stu-id="950e2-293">We discuss this in more detail later in the article.</span></span>

![Şekil 6: Windows Server Yük Devretme Kümelemesi için SIOS DataKeeper kullanarak bir SAP ASCS/SCS yapılandırmasında Azure][sap-ha-guide-figure-1002]

<span data-ttu-id="950e2-295">_**Şekil 6:** Windows Server Yük Devretme Kümelemesi SIOS DataKeeper ile azure'da SAP ASCS/SCS yapılandırma_</span><span class="sxs-lookup"><span data-stu-id="950e2-295">_**Figure 6:** Windows Server Failover Clustering for an SAP ASCS/SCS configuration in Azure with SIOS DataKeeper_</span></span>

### <span data-ttu-id="950e2-296"><a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a>Yüksek kullanılabilirlik DBMS örneği</span><span class="sxs-lookup"><span data-stu-id="950e2-296"><a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a>High-availability DBMS instance</span></span>
<span data-ttu-id="950e2-297">DBMS de tek bir kişinin bir SAP sisteminde noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="950e2-297">The DBMS also is a single point of contact in an SAP system.</span></span> <span data-ttu-id="950e2-298">Yüksek kullanılabilirlik çözümü kullanarak korumanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="950e2-298">You need to protect it by using a high-availability solution.</span></span> <span data-ttu-id="950e2-299">Şekil 7, Azure'da bir SQL Server Always On yüksek kullanılabilirlik çözümü gösterir, Windows Server Yük Devretme Kümelemesi ile Azure iç yük dengeleyici.</span><span class="sxs-lookup"><span data-stu-id="950e2-299">Figure 7 shows a SQL Server Always On high-availability solution in Azure, with Windows Server Failover Clustering and the Azure internal load balancer.</span></span> <span data-ttu-id="950e2-300">SQL Server Always On kendi DBMS çoğaltma kullanılarak DBMS veri ve günlük dosyalarını çoğaltır.</span><span class="sxs-lookup"><span data-stu-id="950e2-300">SQL Server Always On replicates DBMS data and log files by using its own DBMS replication.</span></span> <span data-ttu-id="950e2-301">Bu durumda, paylaşılan diskleri, hangi tüm kurulumu basitleştirir küme.</span><span class="sxs-lookup"><span data-stu-id="950e2-301">In this case, you don't need cluster shared disks, which simplifies the entire setup.</span></span>

![Şekil 7: SQL Server Always On ile bir yüksek kullanılabilirlik SAP DBMS örneği][sap-ha-guide-figure-2003]

<span data-ttu-id="950e2-303">_**Şekil 7:** SQL Server Always On ile bir yüksek kullanılabilirlik SAP DBMS örneği_</span><span class="sxs-lookup"><span data-stu-id="950e2-303">_**Figure 7:** Example of a high-availability SAP DBMS, with SQL Server Always On_</span></span>

<span data-ttu-id="950e2-304">Azure Resource Manager dağıtım modelini kullanarak Azure SQL Server Kümelemesi hakkında daha fazla bilgi için bu makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="950e2-304">For more information about clustering SQL Server in Azure by using the Azure Resource Manager deployment model, see these articles:</span></span>

* <span data-ttu-id="950e2-305">[Always On kullanılabilirlik grubu Azure sanal makinelerinde el ile Kaynak Yöneticisi'ni kullanarak yapılandırmak] [virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]</span><span class="sxs-lookup"><span data-stu-id="950e2-305">[Configure Always On availability group in Azure Virtual Machines manually by using Resource Manager][virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]</span></span>
* <span data-ttu-id="950e2-306">[Always On kullanılabilirlik grubu için bir Azure iç yük dengeleyici Azure'da yapılandırın] [virtual-machines-windows-portal-sql-alwayson-int-listener]</span><span class="sxs-lookup"><span data-stu-id="950e2-306">[Configure an Azure internal load balancer for an Always On availability group in Azure][virtual-machines-windows-portal-sql-alwayson-int-listener]</span></span>

## <span data-ttu-id="950e2-307"><a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a>Uçtan uca yüksek kullanılabilirlik dağıtım senaryoları</span><span class="sxs-lookup"><span data-stu-id="950e2-307"><a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a> End-to-end high-availability deployment scenarios</span></span>

### <a name="deployment-scenario-using-architectural-template-1"></a><span data-ttu-id="950e2-308">Mimari şablonu 1'i kullanarak dağıtım senaryosu</span><span class="sxs-lookup"><span data-stu-id="950e2-308">Deployment scenario using Architectural Template 1</span></span>

<span data-ttu-id="950e2-309">Şekil 8 için azure'da bir SAP NetWeaver yüksek kullanılabilirlik mimari örneği gösterilmiştir **bir** SAP sistem.</span><span class="sxs-lookup"><span data-stu-id="950e2-309">Figure 8 shows an example of an SAP NetWeaver high-availability architecture in Azure for **one** SAP system.</span></span> <span data-ttu-id="950e2-310">Bu senaryo aşağıdaki gibi kurun:</span><span class="sxs-lookup"><span data-stu-id="950e2-310">This scenario is set up as follows:</span></span>

- <span data-ttu-id="950e2-311">Tek bir adanmış küme SAP ASCS/SCS örneği için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="950e2-311">One dedicated cluster is used for the SAP ASCS/SCS instance.</span></span>
- <span data-ttu-id="950e2-312">Tek bir adanmış küme DBMS örneği için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="950e2-312">One dedicated cluster is used for the DBMS instance.</span></span>
- <span data-ttu-id="950e2-313">SAP uygulama sunucusu örnekleri kendi özel VM'ler dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="950e2-313">SAP Application Server instances are deployed in their own dedicated VMs.</span></span>

![Şekil 8: yüksek oranda kullanılabilirlik mimari şablonu, 1 ile ayrılmış küme ASCS/SCS ve DBMS için SAP][sap-ha-guide-figure-2004]

<span data-ttu-id="950e2-315">_**Şekil 8:** ASCS/SCS ve DBMS ayrılmış kümelerine şablonu 1 mimari yüksek kullanılabilirlik, SAP_</span><span class="sxs-lookup"><span data-stu-id="950e2-315">_**Figure 8:** SAP high-availability Architectural Template 1, dedicated clusters for ASCS/SCS and DBMS_</span></span>

### <a name="deployment-scenario-using-architectural-template-2"></a><span data-ttu-id="950e2-316">Mimari şablon 2 kullanarak dağıtım senaryosu</span><span class="sxs-lookup"><span data-stu-id="950e2-316">Deployment scenario using Architectural Template 2</span></span>

<span data-ttu-id="950e2-317">Şekil 9 için azure'da bir SAP NetWeaver yüksek kullanılabilirlik mimari örneği gösterir **bir** SAP sistem.</span><span class="sxs-lookup"><span data-stu-id="950e2-317">Figure 9 shows an example of an SAP NetWeaver high-availability architecture in Azure for **one** SAP system.</span></span> <span data-ttu-id="950e2-318">Bu senaryo aşağıdaki gibi kurun:</span><span class="sxs-lookup"><span data-stu-id="950e2-318">This scenario is set up as follows:</span></span>

- <span data-ttu-id="950e2-319">Ayrılmış bir küme için kullanıldığından **her ikisi de** SAP ASCS/SCS örneği ve DBMS.</span><span class="sxs-lookup"><span data-stu-id="950e2-319">One dedicated cluster is used for **both** the SAP ASCS/SCS instance and the DBMS.</span></span>
- <span data-ttu-id="950e2-320">SAP uygulama sunucusu örnekleri kendi özel VM'ler içinde dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="950e2-320">SAP Application Server instances are deployed in own dedicated VMs.</span></span>

![Şekil 9: yüksek oranda kullanılabilirlik mimari şablon 2 ile ayrılmış bir küme ASCS/SCS için ve ayrılmış bir küme DBMS için SAP][sap-ha-guide-figure-2005]

<span data-ttu-id="950e2-322">_**Şekil 9:** SAP yüksek kullanılabilirlik mimari şablon 2 ile ayrılmış bir küme ASCS/SCS için ve DBMS için ayrılmış bir küme_</span><span class="sxs-lookup"><span data-stu-id="950e2-322">_**Figure 9:** SAP high-availability Architectural Template 2, with a dedicated cluster for ASCS/SCS and a dedicated cluster for DBMS_</span></span>

### <a name="deployment-scenario-using-architectural-template-3"></a><span data-ttu-id="950e2-323">Mimari şablonu 3 kullanan dağıtım senaryosu</span><span class="sxs-lookup"><span data-stu-id="950e2-323">Deployment scenario using Architectural Template 3</span></span>

<span data-ttu-id="950e2-324">Şekil 10 için azure'da bir SAP NetWeaver yüksek kullanılabilirlik mimari örneği gösterilir **iki** ile sistemleri, SAP &lt;SID1&gt; ve &lt;SID2&gt;.</span><span class="sxs-lookup"><span data-stu-id="950e2-324">Figure 10 shows an example of an SAP NetWeaver high-availability architecture in Azure for **two** SAP systems, with &lt;SID1&gt; and &lt;SID2&gt;.</span></span> <span data-ttu-id="950e2-325">Bu senaryo aşağıdaki gibi kurun:</span><span class="sxs-lookup"><span data-stu-id="950e2-325">This scenario is set up as follows:</span></span>

- <span data-ttu-id="950e2-326">Ayrılmış bir küme için kullanıldığından **her ikisi de** SAP ASCS/SCS SID1 örneği *ve* SAP ASCS/SCS SID2 örneği (bir küme için).</span><span class="sxs-lookup"><span data-stu-id="950e2-326">One dedicated cluster is used for **both** the SAP ASCS/SCS SID1 instance *and* the SAP ASCS/SCS SID2 instance (one cluster).</span></span>
- <span data-ttu-id="950e2-327">Tek bir adanmış küme DBMS SID1 için kullanılır ve başka bir ayrılmış küme DBMS SID2 için kullanılır (iki küme).</span><span class="sxs-lookup"><span data-stu-id="950e2-327">One dedicated cluster is used for DBMS SID1, and another dedicated cluster is used for DBMS SID2 (two clusters).</span></span>
- <span data-ttu-id="950e2-328">SAP uygulama sunucusu örneklerinin SAP sistemi SID1 için kendi özel VM'ler vardır.</span><span class="sxs-lookup"><span data-stu-id="950e2-328">SAP Application Server instances for the SAP system SID1 have their own dedicated VMs.</span></span>
- <span data-ttu-id="950e2-329">SAP uygulama sunucusu örneklerinin SAP sistemi SID2 için kendi özel VM'ler vardır.</span><span class="sxs-lookup"><span data-stu-id="950e2-329">SAP Application Server instances for the SAP system SID2 have their own dedicated VMs.</span></span>

![Şekil 10: yüksek kullanılabilirlik mimari şablonu 3, ile ayrılmış bir küme farklı ASCS/SCS örnekleri için SAP][sap-ha-guide-figure-6003]

<span data-ttu-id="950e2-331">_**Şekil 10:** SAP yüksek kullanılabilirlik mimari şablonu 3, ile ayrılmış bir küme için farklı ASCS/SCS örnekleri_</span><span class="sxs-lookup"><span data-stu-id="950e2-331">_**Figure 10:** SAP high-availability Architectural Template 3, with a dedicated cluster for different ASCS/SCS instances_</span></span>

## <span data-ttu-id="950e2-332"><a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a>Altyapıyı hazırlama</span><span class="sxs-lookup"><span data-stu-id="950e2-332"><a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a> Prepare the infrastructure</span></span>

### <a name="prepare-the-infrastructure-for-architectural-template-1"></a><span data-ttu-id="950e2-333">Mimari şablonu 1 için altyapıyı hazırlama</span><span class="sxs-lookup"><span data-stu-id="950e2-333">Prepare the infrastructure for Architectural Template 1</span></span>
<span data-ttu-id="950e2-334">Azure Resource Manager şablonları SAP için gerekli kaynakları dağıtımını kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="950e2-334">Azure Resource Manager templates for SAP help simplify deployment of required resources.</span></span>

<span data-ttu-id="950e2-335">Üç katmanlı şablonları Azure Kaynak Yöneticisi'nde de yüksek kullanılabilirlik senaryoları gibi mimari şablon iki küme olan 1'de destekler.</span><span class="sxs-lookup"><span data-stu-id="950e2-335">The three-tier templates in Azure Resource Manager also support high-availability scenarios, such as in Architectural Template 1, which has two clusters.</span></span> <span data-ttu-id="950e2-336">Her küme bir SAP tek hata SAP ASCS/SCS ve DBMS noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="950e2-336">Each cluster is an SAP single point of failure for SAP ASCS/SCS and DBMS.</span></span>

<span data-ttu-id="950e2-337">İşte burada Biz bu makalede açıklayan örnek senaryo için Azure Resource Manager şablonları elde edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="950e2-337">Here's where you can get Azure Resource Manager templates for the example scenario we describe in this article:</span></span>

* [<span data-ttu-id="950e2-338">Azure Market görüntüsü</span><span class="sxs-lookup"><span data-stu-id="950e2-338">Azure Marketplace image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image)  
* [<span data-ttu-id="950e2-339">Yönetilen diskleri kullanarak azure Market görüntüsü</span><span class="sxs-lookup"><span data-stu-id="950e2-339">Azure Marketplace image using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md)  
* [<span data-ttu-id="950e2-340">Özel görüntü</span><span class="sxs-lookup"><span data-stu-id="950e2-340">Custom image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image)
* [<span data-ttu-id="950e2-341">Özel görüntü yönetilen diskleri kullanma</span><span class="sxs-lookup"><span data-stu-id="950e2-341">Custom image using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-md)

<span data-ttu-id="950e2-342">Mimari şablonu 1 için altyapıyı hazırlamak için:</span><span class="sxs-lookup"><span data-stu-id="950e2-342">To prepare the infrastructure for Architectural Template 1:</span></span>

- <span data-ttu-id="950e2-343">Azure portalında üzerinde **parametreleri** dikey penceresindeki **SYSTEMAVAILABILITY** kutusunda **HA**.</span><span class="sxs-lookup"><span data-stu-id="950e2-343">In the Azure portal, on the **Parameters** blade, in the **SYSTEMAVAILABILITY** box, select **HA**.</span></span>

  ![Şekil 11: Ayarlamak SAP yüksek kullanılabilirlik Azure Resource Manager parametreleri][sap-ha-guide-figure-3000]

<span data-ttu-id="950e2-345">_**Şekil 11:** ayarlamak SAP yüksek kullanılabilirlik Azure Resource Manager parametreleri_</span><span class="sxs-lookup"><span data-stu-id="950e2-345">_**Figure 11:** Set SAP high-availability Azure Resource Manager parameters_</span></span>


  <span data-ttu-id="950e2-346">Şablonları oluşturun:</span><span class="sxs-lookup"><span data-stu-id="950e2-346">The templates create:</span></span>

  * <span data-ttu-id="950e2-347">**Sanal makineler**:</span><span class="sxs-lookup"><span data-stu-id="950e2-347">**Virtual machines**:</span></span>
    * <span data-ttu-id="950e2-348">SAP uygulama sunucusu sanal makineleri: <*SAPSystemSID*> - dı - <*numarası*></span><span class="sxs-lookup"><span data-stu-id="950e2-348">SAP Application Server virtual machines: <*SAPSystemSID*>-di-<*Number*></span></span>
    * <span data-ttu-id="950e2-349">ASCS/SCS küme sanal makineler: <*SAPSystemSID*> - ascs - <*numarası*></span><span class="sxs-lookup"><span data-stu-id="950e2-349">ASCS/SCS cluster virtual machines: <*SAPSystemSID*>-ascs-<*Number*></span></span>
    * <span data-ttu-id="950e2-350">DBMS küme: <*SAPSystemSID*> - db - <*numarası*></span><span class="sxs-lookup"><span data-stu-id="950e2-350">DBMS cluster: <*SAPSystemSID*>-db-<*Number*></span></span>

  * <span data-ttu-id="950e2-351">**Ağ kartları ilişkili IP adresleriyle tüm sanal makineler için**:</span><span class="sxs-lookup"><span data-stu-id="950e2-351">**Network cards for all virtual machines, with associated IP addresses**:</span></span>
    * <span data-ttu-id="950e2-352"><*SAPSystemSID*> - NIC - dı - <*numarası*></span><span class="sxs-lookup"><span data-stu-id="950e2-352"><*SAPSystemSID*>-nic-di-<*Number*></span></span>
    * <span data-ttu-id="950e2-353"><*SAPSystemSID*> - NIC - ascs - <*numarası*></span><span class="sxs-lookup"><span data-stu-id="950e2-353"><*SAPSystemSID*>-nic-ascs-<*Number*></span></span>
    * <span data-ttu-id="950e2-354"><*SAPSystemSID*> - NIC - db - <*numarası*></span><span class="sxs-lookup"><span data-stu-id="950e2-354"><*SAPSystemSID*>-nic-db-<*Number*></span></span>

  * <span data-ttu-id="950e2-355">**Azure depolama hesapları (yalnızca yönetilmeyen diskler)**</span><span class="sxs-lookup"><span data-stu-id="950e2-355">**Azure storage accounts (unmanaged disks only)**</span></span>

  * <span data-ttu-id="950e2-356">**Kullanılabilirlik grupları** için:</span><span class="sxs-lookup"><span data-stu-id="950e2-356">**Availability groups** for:</span></span>
    * <span data-ttu-id="950e2-357">SAP uygulama sunucusu sanal makineleri: <*SAPSystemSID*> - avset - dı</span><span class="sxs-lookup"><span data-stu-id="950e2-357">SAP Application Server virtual machines: <*SAPSystemSID*>-avset-di</span></span>
    * <span data-ttu-id="950e2-358">SAP ASCS/SCS küme sanal makineler: <*SAPSystemSID*> - avset - ascs</span><span class="sxs-lookup"><span data-stu-id="950e2-358">SAP ASCS/SCS cluster virtual machines: <*SAPSystemSID*>-avset-ascs</span></span>
    * <span data-ttu-id="950e2-359">DBMS küme sanal makineler: <*SAPSystemSID*> - avset - db</span><span class="sxs-lookup"><span data-stu-id="950e2-359">DBMS cluster virtual machines: <*SAPSystemSID*>-avset-db</span></span>

  * <span data-ttu-id="950e2-360">**Azure iç yük dengeleyici**:</span><span class="sxs-lookup"><span data-stu-id="950e2-360">**Azure internal load balancer**:</span></span>
    * <span data-ttu-id="950e2-361">IP adresi ve ASCS/SCS örneği için tüm bağlantı noktaları ile <*SAPSystemSID*> - lb - ascs</span><span class="sxs-lookup"><span data-stu-id="950e2-361">With all ports for the ASCS/SCS instance and IP address <*SAPSystemSID*>-lb-ascs</span></span>
    * <span data-ttu-id="950e2-362">SQL Server DBMS ve IP adresi için tüm bağlantı noktaları ile <*SAPSystemSID*> - lb - db</span><span class="sxs-lookup"><span data-stu-id="950e2-362">With all ports for the SQL Server DBMS and IP address <*SAPSystemSID*>-lb-db</span></span>

  * <span data-ttu-id="950e2-363">**Ağ güvenlik grubu**: <*SAPSystemSID*> - nsg - ascs-0</span><span class="sxs-lookup"><span data-stu-id="950e2-363">**Network security group**: <*SAPSystemSID*>-nsg-ascs-0</span></span>  
    * <span data-ttu-id="950e2-364">Açık bir dış Uzak Masaüstü Protokolü (RDP) bağlantı noktasına sahip <*SAPSystemSID*> - ascs - 0 sanal makine</span><span class="sxs-lookup"><span data-stu-id="950e2-364">With an open external Remote Desktop Protocol (RDP) port to the <*SAPSystemSID*>-ascs-0 virtual machine</span></span>

> [!NOTE]
> <span data-ttu-id="950e2-365">Tüm IP adresleri ağ kartları ve Azure iç yük dengeleyicileri **dinamik** varsayılan olarak.</span><span class="sxs-lookup"><span data-stu-id="950e2-365">All IP addresses of the network cards and Azure internal load balancers are **dynamic** by default.</span></span> <span data-ttu-id="950e2-366">Bunları değiştirmek **statik** IP adresleri.</span><span class="sxs-lookup"><span data-stu-id="950e2-366">Change them to **static** IP addresses.</span></span> <span data-ttu-id="950e2-367">Biz bu makalenin sonraki bölümlerinde yapılacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="950e2-367">We describe how to do this later in the article.</span></span>
>
>

### <span data-ttu-id="950e2-368"><a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a>Üretimde kullanılacak kurumsal ağ bağlantısı (şirket içi) ile sanal makineleri dağıtma</span><span class="sxs-lookup"><span data-stu-id="950e2-368"><a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a> Deploy virtual machines with corporate network connectivity (cross-premises) to use in production</span></span>
<span data-ttu-id="950e2-369">Üretim SAP sistemleri için Azure sanal makinelerle dağıtımı [kurumsal ağ bağlantısı (şirket içi)] [ planning-guide-2.2] Azure siteden siteye VPN veya Azure ExpressRoute kullanarak.</span><span class="sxs-lookup"><span data-stu-id="950e2-369">For production SAP systems, deploy Azure virtual machines with [corporate network connectivity (cross-premises)][planning-guide-2.2] by using Azure Site-to-Site VPN or Azure ExpressRoute.</span></span>

> [!NOTE]
> <span data-ttu-id="950e2-370">Azure Virtual Network örneğinizi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="950e2-370">You can use your Azure Virtual Network instance.</span></span> <span data-ttu-id="950e2-371">Sanal ağ ve alt ağ zaten oluşturulmuş hazırlanmış ve.</span><span class="sxs-lookup"><span data-stu-id="950e2-371">The virtual network and subnet have already been created and prepared.</span></span>
>
>

1.  <span data-ttu-id="950e2-372">Azure portalında üzerinde **parametreleri** dikey penceresinde, **NEWOREXISTINGSUBNET** kutusunda **varolan**.</span><span class="sxs-lookup"><span data-stu-id="950e2-372">In the Azure portal, on the **Parameters** blade, in the **NEWOREXISTINGSUBNET** box, select **existing**.</span></span>
2.  <span data-ttu-id="950e2-373">İçinde **SUBNETID** kutusunda, hazırlanan Azure alt ağınızı Azure sanal makinelerinizi dağıtmak planladığınız SubnetID tam dizesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="950e2-373">In the **SUBNETID** box, add the full string of your prepared Azure network SubnetID where you plan to deploy your Azure virtual machines.</span></span>
3.  <span data-ttu-id="950e2-374">Tüm Azure ağ alt ağlar listesini almak için bu PowerShell komutunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="950e2-374">To get a list of all Azure network subnets, run this PowerShell command:</span></span>

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets
  ```

  <span data-ttu-id="950e2-375">**Kimliği** alan gösterir **SUBNETID**.</span><span class="sxs-lookup"><span data-stu-id="950e2-375">The **ID** field shows the **SUBNETID**.</span></span>
4. <span data-ttu-id="950e2-376">Tüm listesini almak için **SUBNETID** değerleri, bu PowerShell komutunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="950e2-376">To get a list of all **SUBNETID** values, run this PowerShell command:</span></span>

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets.Id
  ```

  <span data-ttu-id="950e2-377">**SUBNETID** şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="950e2-377">The **SUBNETID** looks like this:</span></span>

  ```
  /subscriptions/<SubscriptionId>/resourceGroups/<VPNName>/providers/Microsoft.Network/virtualNetworks/azureVnet/subnets/<SubnetName>
  ```

### <span data-ttu-id="950e2-378"><a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a>Test ve demo için yalnızca bulut SAP örnekleri dağıtma</span><span class="sxs-lookup"><span data-stu-id="950e2-378"><a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a> Deploy cloud-only SAP instances for test and demo</span></span>
<span data-ttu-id="950e2-379">Yüksek kullanılabilirlik SAP sisteminizi bir yalnızca bulut dağıtım modelinde dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="950e2-379">You can deploy your high-availability SAP system in a cloud-only deployment model.</span></span> <span data-ttu-id="950e2-380">Bu tür bir dağıtım öncelikle tanıtım ve test kullanım durumları için yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="950e2-380">This kind of deployment primarily is useful for demo and test use cases.</span></span> <span data-ttu-id="950e2-381">Üretim kullanım durumları için uygun değildir.</span><span class="sxs-lookup"><span data-stu-id="950e2-381">It's not suited for production use cases.</span></span>

- <span data-ttu-id="950e2-382">Azure portalında üzerinde **parametreleri** dikey penceresindeki **NEWOREXISTINGSUBNET** kutusunda **yeni**.</span><span class="sxs-lookup"><span data-stu-id="950e2-382">In the Azure portal, on the **Parameters** blade, in the **NEWOREXISTINGSUBNET** box, select **new**.</span></span> <span data-ttu-id="950e2-383">Bırakın **SUBNETID** alanı boş.</span><span class="sxs-lookup"><span data-stu-id="950e2-383">Leave the **SUBNETID** field empty.</span></span>

  <span data-ttu-id="950e2-384">SAP Azure Resource Manager şablonu, Azure sanal ağ ve alt otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="950e2-384">The SAP Azure Resource Manager template automatically creates the Azure virtual network and subnet.</span></span>

> [!NOTE]
> <span data-ttu-id="950e2-385">Ayrıca en az bir ayrılmış sanal makine Active Directory ve DNS için aynı Azure sanal ağ örneğinde dağıtmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="950e2-385">You also need to deploy at least one dedicated virtual machine for Active Directory and DNS in the same Azure Virtual Network instance.</span></span> <span data-ttu-id="950e2-386">Şablon, bu sanal makineleri oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="950e2-386">The template doesn't create these virtual machines.</span></span>
>
>


### <a name="prepare-the-infrastructure-for-architectural-template-2"></a><span data-ttu-id="950e2-387">Mimari şablon 2 için altyapıyı hazırlama</span><span class="sxs-lookup"><span data-stu-id="950e2-387">Prepare the infrastructure for Architectural Template 2</span></span>

<span data-ttu-id="950e2-388">Bu Azure Resource Manager şablonu SAP için gerekli altyapı kaynaklarıdır dağıtım SAP mimari şablon 2 basitleştirmeye yardımcı olması için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="950e2-388">You can use this Azure Resource Manager template for SAP to help simplify deployment of required infrastructure resources for SAP Architectural Template 2.</span></span>

<span data-ttu-id="950e2-389">İşte, bu dağıtım senaryosu için Azure Resource Manager şablonları burada alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="950e2-389">Here's where you can get Azure Resource Manager templates for this deployment scenario:</span></span>

* [<span data-ttu-id="950e2-390">Azure Market görüntüsü</span><span class="sxs-lookup"><span data-stu-id="950e2-390">Azure Marketplace image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged)  
* [<span data-ttu-id="950e2-391">Yönetilen diskleri kullanarak azure Market görüntüsü</span><span class="sxs-lookup"><span data-stu-id="950e2-391">Azure Marketplace image using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged-md)  
* [<span data-ttu-id="950e2-392">Özel görüntü</span><span class="sxs-lookup"><span data-stu-id="950e2-392">Custom image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged)
* [<span data-ttu-id="950e2-393">Özel görüntü yönetilen diskleri kullanma</span><span class="sxs-lookup"><span data-stu-id="950e2-393">Custom image using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged-md)


### <a name="prepare-the-infrastructure-for-architectural-template-3"></a><span data-ttu-id="950e2-394">Mimari şablonu 3 için altyapıyı hazırlama</span><span class="sxs-lookup"><span data-stu-id="950e2-394">Prepare the infrastructure for Architectural Template 3</span></span>

<span data-ttu-id="950e2-395">Altyapıyı hazırlama ve yapılandırma için SAP **çoklu SID**.</span><span class="sxs-lookup"><span data-stu-id="950e2-395">You can prepare the infrastructure and configure SAP for **multi-SID**.</span></span> <span data-ttu-id="950e2-396">Örneğin, ek bir SAP ASCS/SCS örneğine ekleyebileceğiniz bir *varolan* küme yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="950e2-396">For example, you can add an additional SAP ASCS/SCS instance into an *existing* cluster configuration.</span></span> <span data-ttu-id="950e2-397">Daha fazla bilgi için bkz: [Azure Kaynak Yöneticisi'nde bir SAP çoklu SID yapılandırması oluşturmak için var olan bir küme yapılandırmasını içine ek SAP ASCS/SCS örnek yapılandırma][sap-ha-multi-sid-guide].</span><span class="sxs-lookup"><span data-stu-id="950e2-397">For more information, see [Configure an additional SAP ASCS/SCS instance into an existing cluster configuration to create an SAP multi-SID configuration in Azure Resource Manager][sap-ha-multi-sid-guide].</span></span>

<span data-ttu-id="950e2-398">Yeni bir SID çoklu küme oluşturmak istiyorsanız, çoklu SID kullanabilirsiniz [GitHub hızlı başlangıç şablonlarında](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="950e2-398">If you want to create a new multi-SID cluster, you can use the multi-SID [quickstart templates on GitHub](https://github.com/Azure/azure-quickstart-templates).</span></span>
<span data-ttu-id="950e2-399">Yeni bir SID çoklu küme oluşturmak için aşağıdaki üç şablonlarını dağıtma gerekir:</span><span class="sxs-lookup"><span data-stu-id="950e2-399">To create a new multi-SID cluster, you need to deploy the following three templates:</span></span>

* [<span data-ttu-id="950e2-400">ASCS/SCS şablonu</span><span class="sxs-lookup"><span data-stu-id="950e2-400">ASCS/SCS template</span></span>](#ASCS-SCS-template)
* [<span data-ttu-id="950e2-401">Veritabanı şablonu</span><span class="sxs-lookup"><span data-stu-id="950e2-401">Database template</span></span>](#database-template)
* [<span data-ttu-id="950e2-402">Uygulama sunucuları şablonu</span><span class="sxs-lookup"><span data-stu-id="950e2-402">Application servers template</span></span>](#application-servers-template)

<span data-ttu-id="950e2-403">Aşağıdaki bölümlerde, şablonları ve şablonları sağlamanız gereken parametreleri hakkında daha fazla ayrıntı sahip.</span><span class="sxs-lookup"><span data-stu-id="950e2-403">The following sections have more details about the templates and the parameters you need to provide in the templates.</span></span>

#### <span data-ttu-id="950e2-404"><a name="ASCS-SCS-template"></a>ASCS/SCS şablonu</span><span class="sxs-lookup"><span data-stu-id="950e2-404"><a name="ASCS-SCS-template"></a> ASCS/SCS template</span></span>

<span data-ttu-id="950e2-405">ASCS/SCS şablonu birden fazla ASCS/SCS örneği barındıran bir Windows Server Yük devretme kümesi oluşturmak için kullanabileceğiniz iki sanal makine dağıtır.</span><span class="sxs-lookup"><span data-stu-id="950e2-405">The ASCS/SCS template deploys two virtual machines that you can use to create a Windows Server failover cluster that hosts multiple ASCS/SCS instances.</span></span>

<span data-ttu-id="950e2-406">ASCS/SCS çoklu SID şablonunu, buna ayarlamak için [ASCS/SCS çoklu SID şablonu] [ sap-templates-3-tier-multisid-xscs-marketplace-image] veya [ASCS/SCS çoklu SID şablonu yönetilen diskleri kullanarak] [ sap-templates-3-tier-multisid-xscs-marketplace-image-md], aşağıdaki parametreler için değerler girin:</span><span class="sxs-lookup"><span data-stu-id="950e2-406">To set up the ASCS/SCS multi-SID template, in the [ASCS/SCS multi-SID template][sap-templates-3-tier-multisid-xscs-marketplace-image] or [ASCS/SCS multi-SID template using Managed Disks][sap-templates-3-tier-multisid-xscs-marketplace-image-md], enter values for the following parameters:</span></span>

  - <span data-ttu-id="950e2-407">**Kaynak önek**.</span><span class="sxs-lookup"><span data-stu-id="950e2-407">**Resource Prefix**.</span></span>  <span data-ttu-id="950e2-408">Dağıtım sırasında oluşturulan tüm kaynakları öneki için kullanılan kaynak öneki ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="950e2-408">Set the resource prefix, which is used to prefix all resources that are created during the deployment.</span></span> <span data-ttu-id="950e2-409">Kaynaklar için yalnızca bir SAP sistemine ait olmadığından kaynak önek bir SAP sistem SID'si değil.</span><span class="sxs-lookup"><span data-stu-id="950e2-409">Because the resources do not belong to only one SAP system, the prefix of the resource is not the SID of one SAP system.</span></span>  <span data-ttu-id="950e2-410">Önek arasında olmalıdır **üç ve altı karakter**.</span><span class="sxs-lookup"><span data-stu-id="950e2-410">The prefix must be between **three and six characters**.</span></span>
  - <span data-ttu-id="950e2-411">**Yığın türü**.</span><span class="sxs-lookup"><span data-stu-id="950e2-411">**Stack Type**.</span></span> <span data-ttu-id="950e2-412">SAP Sistem yığını türünü seçin.</span><span class="sxs-lookup"><span data-stu-id="950e2-412">Select the stack type of the SAP system.</span></span> <span data-ttu-id="950e2-413">Yığın türüne bağlı olarak, Azure yük dengeleyici (ABAP veya yalnızca Java) bir veya iki (ABAP + Java) özel IP adresleri SAP sistem başına var.</span><span class="sxs-lookup"><span data-stu-id="950e2-413">Depending on the stack type, Azure Load Balancer has one (ABAP or Java only) or two (ABAP+Java) private IP addresses per SAP system.</span></span>
  -  <span data-ttu-id="950e2-414">**İşletim sistemi türü**.</span><span class="sxs-lookup"><span data-stu-id="950e2-414">**OS Type**.</span></span> <span data-ttu-id="950e2-415">Sanal makinelerin işletim sistemini seçin.</span><span class="sxs-lookup"><span data-stu-id="950e2-415">Select the operating system of the virtual machines.</span></span>
  -  <span data-ttu-id="950e2-416">**SAP sistem sayısı**.</span><span class="sxs-lookup"><span data-stu-id="950e2-416">**SAP System Count**.</span></span> <span data-ttu-id="950e2-417">SAP sistemleri bu kümede yüklemek istediğiniz sayısını seçin.</span><span class="sxs-lookup"><span data-stu-id="950e2-417">Select the number of SAP systems you want to install in this cluster.</span></span>
  -  <span data-ttu-id="950e2-418">**Sistem kullanılabilirliğini**.</span><span class="sxs-lookup"><span data-stu-id="950e2-418">**System Availability**.</span></span> <span data-ttu-id="950e2-419">Seçin **HA**.</span><span class="sxs-lookup"><span data-stu-id="950e2-419">Select **HA**.</span></span>
  -  <span data-ttu-id="950e2-420">**Yönetici kullanıcı adı ve yönetici parolası**.</span><span class="sxs-lookup"><span data-stu-id="950e2-420">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="950e2-421">Makinede oturum açmak için kullanılan yeni bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="950e2-421">Create a new user that can be used to sign in to the machine.</span></span>
  -  <span data-ttu-id="950e2-422">**Yeni veya var olan bir alt ağ**.</span><span class="sxs-lookup"><span data-stu-id="950e2-422">**New Or Existing Subnet**.</span></span> <span data-ttu-id="950e2-423">Yeni sanal ağ ve alt oluşturulmalıdır veya mevcut bir alt kullanılmalıdır gerekip gerekmediğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="950e2-423">Set whether a new virtual network and subnet should be created, or an existing subnet should be used.</span></span> <span data-ttu-id="950e2-424">Şirket içi ağınıza bağlı bir sanal ağ zaten varsa, seçin **varolan**.</span><span class="sxs-lookup"><span data-stu-id="950e2-424">If you already have a virtual network that is connected to your on-premises network, select **existing**.</span></span>
  -  <span data-ttu-id="950e2-425">**Alt ağ kimliği**.</span><span class="sxs-lookup"><span data-stu-id="950e2-425">**Subnet Id**.</span></span> <span data-ttu-id="950e2-426">Sanal makinelerin bağlanması alt ağ Kimliğini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="950e2-426">Set the ID of the subnet to which the virtual machines should be connected.</span></span> <span data-ttu-id="950e2-427">Sanal özel ağ (VPN) veya sanal makine şirket içi ağınıza bağlamak için ExpressRoute sanal ağ alt ağı seçin.</span><span class="sxs-lookup"><span data-stu-id="950e2-427">Select the subnet of your virtual private network (VPN) or ExpressRoute virtual network to connect the virtual machine to your on-premises network.</span></span> <span data-ttu-id="950e2-428">Kimliği genellikle şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="950e2-428">The ID usually looks like this:</span></span>

   <span data-ttu-id="950e2-429">/Subscriptions/ <*abonelik kimliği*> /resourceGroups/ <*kaynak grubu adı*> /providers/Microsoft.Network/virtualNetworks/ <*sanal ağ adı*> /subnets/ <*alt ağ adı*></span><span class="sxs-lookup"><span data-stu-id="950e2-429">/subscriptions/<*subscription id*>/resourceGroups/<*resource group name*>/providers/Microsoft.Network/virtualNetworks/<*virtual network name*>/subnets/<*subnet name*></span></span>

<span data-ttu-id="950e2-430">Şablon birden çok SAP sistemlerini destekleyen bir Azure yük dengeleyici örneği dağıtır.</span><span class="sxs-lookup"><span data-stu-id="950e2-430">The template deploys one Azure Load Balancer instance, which supports multiple SAP systems.</span></span>

- <span data-ttu-id="950e2-431">ASCS örnekleri örnek numarası 00, 10, 20 yapılandırılmış...</span><span class="sxs-lookup"><span data-stu-id="950e2-431">The ASCS instances are configured for instance number 00, 10, 20...</span></span>
- <span data-ttu-id="950e2-432">SCS örnekleri örnek numarası 01, 11, 21 yapılandırılmış...</span><span class="sxs-lookup"><span data-stu-id="950e2-432">The SCS instances are configured for instance number 01, 11, 21...</span></span>
- <span data-ttu-id="950e2-433">ASCS kuyruğa çoğaltma sunucusuna (ERS) (yalnızca Linux) örnekleri örnek numarası 02, 12, 22 yapılandırılmış...</span><span class="sxs-lookup"><span data-stu-id="950e2-433">The ASCS Enqueue Replication Server (ERS) (Linux only) instances are configured for instance number 02, 12, 22...</span></span>
- <span data-ttu-id="950e2-434">SCS ERS (yalnızca Linux) örnekleri örneği için 03, 13, 23 sayısı yapılandırılan...</span><span class="sxs-lookup"><span data-stu-id="950e2-434">The SCS ERS (Linux only) instances are configured for instance number 03, 13, 23...</span></span>

<span data-ttu-id="950e2-435">Yük Dengeleyici 1 (Linux için 2) içeren VIP(s), ASCS/SCS için 1 x VIP ve 1 x VIP ERS (yalnızca Linux) için.</span><span class="sxs-lookup"><span data-stu-id="950e2-435">The load balancer contains 1 (2 for Linux) VIP(s), 1x VIP for ASCS/SCS and 1x VIP for ERS (Linux only).</span></span>

<span data-ttu-id="950e2-436">Aşağıdaki listede tüm Yük Dengeleme kuralları (burada x, SAP sisteminin, örneğin, 1, 2, 3... sayıdır) içerir:</span><span class="sxs-lookup"><span data-stu-id="950e2-436">The following list contains all load balancing rules (where x is the number of the SAP system, for example, 1, 2, 3...):</span></span>
- <span data-ttu-id="950e2-437">Her SAP sistemi için Windows özel bağlantı noktaları: 445, 5985</span><span class="sxs-lookup"><span data-stu-id="950e2-437">Windows-specific ports for every SAP system: 445, 5985</span></span>
- <span data-ttu-id="950e2-438">ASCS bağlantı noktası (örnek numarasını x0): 32 x 0, 36 x 0, 39 x 0, 81 x 0, 5 x 013, 5 x 014, 5 x 016</span><span class="sxs-lookup"><span data-stu-id="950e2-438">ASCS ports (instance number x0): 32x0, 36x0, 39x0, 81x0, 5x013, 5x014, 5x016</span></span>
- <span data-ttu-id="950e2-439">SCS bağlantı noktası (örnek numarasını x1): 32 x 1, 33 x 1, 39 x 1, 81 x 1, 5 x 113, 5 x 114, 5 x 116</span><span class="sxs-lookup"><span data-stu-id="950e2-439">SCS ports (instance number x1): 32x1, 33x1, 39x1, 81x1, 5x113, 5x114, 5x116</span></span>
- <span data-ttu-id="950e2-440">ASCS ERS bağlantı noktaları (örnek numarasını x2) Linux'ta: 33 x 2, 5 x 213, 5 x 214, 5 x 216</span><span class="sxs-lookup"><span data-stu-id="950e2-440">ASCS ERS ports on Linux (instance number x2): 33x2, 5x213, 5x214, 5x216</span></span>
- <span data-ttu-id="950e2-441">SCS ERS bağlantı noktaları (örnek numarasını x3) Linux'ta: 33 x 3, 5 x 313, 5 x 314, 5 x 316</span><span class="sxs-lookup"><span data-stu-id="950e2-441">SCS ERS ports on Linux (instance number x3): 33x3, 5x313, 5x314, 5x316</span></span>

<span data-ttu-id="950e2-442">Yük Dengeleyici (burada x, SAP sisteminin, örneğin, 1, 2, 3... sayıdır) aşağıdaki araştırma bağlantı noktalarını kullanacak şekilde yapılandırılır:</span><span class="sxs-lookup"><span data-stu-id="950e2-442">The load balancer is configured to use the following probe ports (where x is the number of the SAP system, for example, 1, 2, 3...):</span></span>
- <span data-ttu-id="950e2-443">ASCS/SCS iç yük dengeleyici araştırması bağlantı noktası: 620 x 0</span><span class="sxs-lookup"><span data-stu-id="950e2-443">ASCS/SCS internal load balancer probe port: 620x0</span></span>
- <span data-ttu-id="950e2-444">ERS iç yük dengeleyici araştırması bağlantı noktası (yalnızca Linux): 621 x 2</span><span class="sxs-lookup"><span data-stu-id="950e2-444">ERS internal load balancer probe port (Linux only): 621x2</span></span>

#### <span data-ttu-id="950e2-445"><a name="database-template"></a>Veritabanı şablonu</span><span class="sxs-lookup"><span data-stu-id="950e2-445"><a name="database-template"></a> Database template</span></span>

<span data-ttu-id="950e2-446">Veritabanı şablonu bir veya iki sanal bir SAP sistem ilişkisel veritabanı yönetim sistemi (RDBMS) yüklemek için kullanabileceğiniz makineleri dağıtır.</span><span class="sxs-lookup"><span data-stu-id="950e2-446">The database template deploys one or two virtual machines that you can use to install the relational database management system (RDBMS) for one SAP system.</span></span> <span data-ttu-id="950e2-447">Örneğin, beş SAP sistemleri için bir ASCS/SCS şablonu dağıtırsanız, bu şablonu beş kez dağıtmak için gerekir.</span><span class="sxs-lookup"><span data-stu-id="950e2-447">For example, if you deploy an ASCS/SCS template for five SAP systems, you need to deploy this template five times.</span></span>

<span data-ttu-id="950e2-448">Veritabanı çoklu SID şablonu ayarlamak için [veritabanı çoklu SID şablonu] [ sap-templates-3-tier-multisid-db-marketplace-image] veya [yönetilen diskleri kullanarak veritabanı çoklu SID şablonu] [ sap-templates-3-tier-multisid-db-marketplace-image-md], aşağıdaki parametreler için değerler girin:</span><span class="sxs-lookup"><span data-stu-id="950e2-448">To set up the database multi-SID template, in the [database multi-SID template][sap-templates-3-tier-multisid-db-marketplace-image] or [database multi-SID template using Managed Disks][sap-templates-3-tier-multisid-db-marketplace-image-md], enter values for the following parameters:</span></span>

  -  <span data-ttu-id="950e2-449">**SAP sistem kimliği**.</span><span class="sxs-lookup"><span data-stu-id="950e2-449">**Sap System Id**.</span></span> <span data-ttu-id="950e2-450">Yüklemek istediğiniz SAP sistem SAP sistem Kimliğini girin.</span><span class="sxs-lookup"><span data-stu-id="950e2-450">Enter the SAP system ID of the SAP system you want to install.</span></span> <span data-ttu-id="950e2-451">Kimliği önek olarak dağıtılan kaynaklar için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="950e2-451">The ID will be used as a prefix for the resources that are deployed.</span></span>
  -  <span data-ttu-id="950e2-452">**İşletim sistemi türü**.</span><span class="sxs-lookup"><span data-stu-id="950e2-452">**Os Type**.</span></span> <span data-ttu-id="950e2-453">Sanal makinelerin işletim sistemini seçin.</span><span class="sxs-lookup"><span data-stu-id="950e2-453">Select the operating system of the virtual machines.</span></span>
  -  <span data-ttu-id="950e2-454">**DbType**.</span><span class="sxs-lookup"><span data-stu-id="950e2-454">**Dbtype**.</span></span> <span data-ttu-id="950e2-455">Kümede yüklemek istediğiniz veritabanını seçin.</span><span class="sxs-lookup"><span data-stu-id="950e2-455">Select the type of the database you want to install on the cluster.</span></span> <span data-ttu-id="950e2-456">Seçin **SQL** Microsoft SQL Server yüklemek istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="950e2-456">Select **SQL** if you want to install Microsoft SQL Server.</span></span> <span data-ttu-id="950e2-457">Seçin **HANA** sanal makinelerde SAP HANA yüklemeyi planlıyorsanız.</span><span class="sxs-lookup"><span data-stu-id="950e2-457">Select **HANA** if you plan to install SAP HANA on the virtual machines.</span></span> <span data-ttu-id="950e2-458">Doğru işletim sistemi türü seçtiğinizden emin olun: seçin **Windows** HANA için Linux dağıtımı seçin ve SQL için.</span><span class="sxs-lookup"><span data-stu-id="950e2-458">Make sure to select the correct operating system type: select **Windows** for SQL, and select a Linux distribution for HANA.</span></span> <span data-ttu-id="950e2-459">Sanal makinelere bağlı Azure yük dengeleyici, seçili veritabanı türünü desteklemek üzere yapılandırılır:</span><span class="sxs-lookup"><span data-stu-id="950e2-459">The Azure Load Balancer that is connected to the virtual machines will be configured to support the selected database type:</span></span>
    * <span data-ttu-id="950e2-460">**SQL**.</span><span class="sxs-lookup"><span data-stu-id="950e2-460">**SQL**.</span></span> <span data-ttu-id="950e2-461">Yük Dengeleyici Yük Dengeleme bağlantı noktası 1433 olur.</span><span class="sxs-lookup"><span data-stu-id="950e2-461">The load balancer will load-balance port 1433.</span></span> <span data-ttu-id="950e2-462">SQL Server Always On ayarlarınızı bu bağlantı noktasını kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="950e2-462">Make sure to use this port for your SQL Server Always On setup.</span></span>
    * <span data-ttu-id="950e2-463">**HANA**.</span><span class="sxs-lookup"><span data-stu-id="950e2-463">**HANA**.</span></span> <span data-ttu-id="950e2-464">Yük Dengeleyici Yük Dengeleme 35015 ve 35017 bağlantı noktalarını olur.</span><span class="sxs-lookup"><span data-stu-id="950e2-464">The load balancer will load-balance ports 35015 and 35017.</span></span> <span data-ttu-id="950e2-465">SAP HANA ile örnek numarasını yüklediğinizden emin olun **50**.</span><span class="sxs-lookup"><span data-stu-id="950e2-465">Make sure to install SAP HANA with instance number **50**.</span></span>
    <span data-ttu-id="950e2-466">Yük Dengeleyici araştırması bağlantı noktasını 62550 kullanır.</span><span class="sxs-lookup"><span data-stu-id="950e2-466">The load balancer will use probe port 62550.</span></span>
  -  <span data-ttu-id="950e2-467">**SAP sistem boyutu**.</span><span class="sxs-lookup"><span data-stu-id="950e2-467">**Sap System Size**.</span></span> <span data-ttu-id="950e2-468">Yeni Sistem sağlayacak SAP sayısını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="950e2-468">Set the number of SAPS the new system will provide.</span></span> <span data-ttu-id="950e2-469">Sistem gerektirir kaç SAP değil eminseniz, SAP teknolojisi iş ortağı veya sistem Tümleştirici isteyin.</span><span class="sxs-lookup"><span data-stu-id="950e2-469">If you are not sure how many SAPS the system will require, ask your SAP Technology Partner or System Integrator.</span></span>
  -  <span data-ttu-id="950e2-470">**Sistem kullanılabilirliğini**.</span><span class="sxs-lookup"><span data-stu-id="950e2-470">**System Availability**.</span></span> <span data-ttu-id="950e2-471">Seçin **HA**.</span><span class="sxs-lookup"><span data-stu-id="950e2-471">Select **HA**.</span></span>
  -  <span data-ttu-id="950e2-472">**Yönetici kullanıcı adı ve yönetici parolası**.</span><span class="sxs-lookup"><span data-stu-id="950e2-472">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="950e2-473">Makinede oturum açmak için kullanılan yeni bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="950e2-473">Create a new user that can be used to sign in to the machine.</span></span>
  -  <span data-ttu-id="950e2-474">**Alt ağ kimliği**.</span><span class="sxs-lookup"><span data-stu-id="950e2-474">**Subnet Id**.</span></span> <span data-ttu-id="950e2-475">ASCS/SCS şablon dağıtımı sırasında kullanılan alt ağ kimliği veya oluşturulmuş alt ağ kimliği ASCS/SCS şablonu dağıtımının bir parçası girin.</span><span class="sxs-lookup"><span data-stu-id="950e2-475">Enter the ID of the subnet that you used during the deployment of the ASCS/SCS template, or the ID of the subnet that was created as part of the ASCS/SCS template deployment.</span></span>

#### <span data-ttu-id="950e2-476"><a name="application-servers-template"></a>Uygulama sunucuları şablonu</span><span class="sxs-lookup"><span data-stu-id="950e2-476"><a name="application-servers-template"></a> Application servers template</span></span>

<span data-ttu-id="950e2-477">Uygulama sunucuları şablonu iki veya daha fazla sanal SAP uygulama sunucusu örneklerinin bir SAP sistemi için kullanılabilecek makineler dağıtır.</span><span class="sxs-lookup"><span data-stu-id="950e2-477">The application servers template deploys two or more virtual machines that can be used as SAP Application Server instances for one SAP system.</span></span> <span data-ttu-id="950e2-478">Örneğin, beş SAP sistemleri için bir ASCS/SCS şablonu dağıtırsanız, bu şablonu beş kez dağıtmak için gerekir.</span><span class="sxs-lookup"><span data-stu-id="950e2-478">For example, if you deploy an ASCS/SCS template for five SAP systems, you need to deploy this template five times.</span></span>

<span data-ttu-id="950e2-479">Uygulama sunucuları çoklu SID şablonu ayarlamak için [uygulama sunucuları çoklu SID şablonu] [ sap-templates-3-tier-multisid-apps-marketplace-image] veya [yönetilen disklerikullanarakuygulamasunucularıçokluSIDşablonu] [ sap-templates-3-tier-multisid-apps-marketplace-image-md], aşağıdaki parametreler için değerler girin:</span><span class="sxs-lookup"><span data-stu-id="950e2-479">To set up the application servers multi-SID template, in the [application servers multi-SID template][sap-templates-3-tier-multisid-apps-marketplace-image] or [application servers multi-SID template using Managed Disks][sap-templates-3-tier-multisid-apps-marketplace-image-md], enter values for the following parameters:</span></span>

  -  <span data-ttu-id="950e2-480">**SAP sistem kimliği**.</span><span class="sxs-lookup"><span data-stu-id="950e2-480">**Sap System Id**.</span></span> <span data-ttu-id="950e2-481">Yüklemek istediğiniz SAP sistem SAP sistem Kimliğini girin.</span><span class="sxs-lookup"><span data-stu-id="950e2-481">Enter the SAP system ID of the SAP system you want to install.</span></span> <span data-ttu-id="950e2-482">Kimliği önek olarak dağıtılan kaynaklar için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="950e2-482">The ID will be used as a prefix for the resources that are deployed.</span></span>
  -  <span data-ttu-id="950e2-483">**İşletim sistemi türü**.</span><span class="sxs-lookup"><span data-stu-id="950e2-483">**Os Type**.</span></span> <span data-ttu-id="950e2-484">Sanal makinelerin işletim sistemini seçin.</span><span class="sxs-lookup"><span data-stu-id="950e2-484">Select the operating system of the virtual machines.</span></span>
  -  <span data-ttu-id="950e2-485">**SAP sistem boyutu**.</span><span class="sxs-lookup"><span data-stu-id="950e2-485">**Sap System Size**.</span></span> <span data-ttu-id="950e2-486">Yeni Sistem sağlayacak SAP sayısı.</span><span class="sxs-lookup"><span data-stu-id="950e2-486">The number of SAPS the new system will provide.</span></span> <span data-ttu-id="950e2-487">Sistem gerektirir kaç SAP değil eminseniz, SAP teknolojisi iş ortağı veya sistem Tümleştirici isteyin.</span><span class="sxs-lookup"><span data-stu-id="950e2-487">If you are not sure how many SAPS the system will require, ask your SAP Technology Partner or System Integrator.</span></span>
  -  <span data-ttu-id="950e2-488">**Sistem kullanılabilirliğini**.</span><span class="sxs-lookup"><span data-stu-id="950e2-488">**System Availability**.</span></span> <span data-ttu-id="950e2-489">Seçin **HA**.</span><span class="sxs-lookup"><span data-stu-id="950e2-489">Select **HA**.</span></span>
  -  <span data-ttu-id="950e2-490">**Yönetici kullanıcı adı ve yönetici parolası**.</span><span class="sxs-lookup"><span data-stu-id="950e2-490">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="950e2-491">Makinede oturum açmak için kullanılan yeni bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="950e2-491">Create a new user that can be used to sign in to the machine.</span></span>
  -  <span data-ttu-id="950e2-492">**Alt ağ kimliği**.</span><span class="sxs-lookup"><span data-stu-id="950e2-492">**Subnet Id**.</span></span> <span data-ttu-id="950e2-493">ASCS/SCS şablon dağıtımı sırasında kullanılan alt ağ kimliği veya oluşturulmuş alt ağ kimliği ASCS/SCS şablonu dağıtımının bir parçası girin.</span><span class="sxs-lookup"><span data-stu-id="950e2-493">Enter the ID of the subnet that you used during the deployment of the ASCS/SCS template, or the ID of the subnet that was created as part of the ASCS/SCS template deployment.</span></span>


### <span data-ttu-id="950e2-494"><a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a>Azure sanal ağı</span><span class="sxs-lookup"><span data-stu-id="950e2-494"><a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a> Azure virtual network</span></span>
<span data-ttu-id="950e2-495">Bizim örneğimizde, Azure sanal ağ adres alanı 10.0.0.0/16 şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="950e2-495">In our example, the address space of the Azure virtual network is 10.0.0.0/16.</span></span> <span data-ttu-id="950e2-496">Adlı bir alt ağ yok **alt**, 10.0.0.0/24 adres aralığı olan.</span><span class="sxs-lookup"><span data-stu-id="950e2-496">There is one subnet called **Subnet**, with an address range of 10.0.0.0/24.</span></span> <span data-ttu-id="950e2-497">Bu sanal ağda, tüm sanal makineler ve iç yük dengeleyicileri dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="950e2-497">All virtual machines and internal load balancers are deployed in this virtual network.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="950e2-498">Ağ ayarları konuk işletim sistemi içinde herhangi bir değişiklik yoktur.</span><span class="sxs-lookup"><span data-stu-id="950e2-498">Don't make any changes to the network settings inside the guest operating system.</span></span> <span data-ttu-id="950e2-499">Bu IP adresleri, DNS sunucuları ve alt ağ içerir.</span><span class="sxs-lookup"><span data-stu-id="950e2-499">This includes IP addresses, DNS servers, and subnet.</span></span> <span data-ttu-id="950e2-500">Azure'da tüm ağ ayarlarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="950e2-500">Configure all your network settings in Azure.</span></span> <span data-ttu-id="950e2-501">Dinamik Ana Bilgisayar Yapılandırma Protokolü (DHCP) hizmeti ayarlarınızı yayar.</span><span class="sxs-lookup"><span data-stu-id="950e2-501">The Dynamic Host Configuration Protocol (DHCP) service propagates your settings.</span></span>
>
>

### <span data-ttu-id="950e2-502"><a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a>DNS IP adresleri</span><span class="sxs-lookup"><span data-stu-id="950e2-502"><a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a> DNS IP addresses</span></span>

<span data-ttu-id="950e2-503">Gerekli DNS IP adreslerini ayarlamak için aşağıdaki adımları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="950e2-503">To set the required DNS IP addresses, do the following steps.</span></span>

1.  <span data-ttu-id="950e2-504">Azure portalında üzerinde **DNS sunucuları** dikey penceresinde olduğundan emin olun, sanal ağınızı **DNS sunucuları** seçeneği **özel DNS**.</span><span class="sxs-lookup"><span data-stu-id="950e2-504">In the Azure portal, on the **DNS servers** blade, make sure that your virtual network **DNS servers** option is set to **Custom DNS**.</span></span>
2.  <span data-ttu-id="950e2-505">Sahip olduğunuz ağ türüne göre ayarlarınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="950e2-505">Select your settings based on the type of network you have.</span></span> <span data-ttu-id="950e2-506">Daha fazla bilgi için aşağıdaki kaynaklara bakın:</span><span class="sxs-lookup"><span data-stu-id="950e2-506">For more information, see the following resources:</span></span>
    * <span data-ttu-id="950e2-507">[Kurumsal ağ bağlantısı (şirket içi)][planning-guide-2.2]: şirket içi DNS sunucularının IP adreslerini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="950e2-507">[Corporate network connectivity (cross-premises)][planning-guide-2.2]: Add the IP addresses of the on-premises DNS servers.</span></span>  
    <span data-ttu-id="950e2-508">Azure'da çalışan sanal makineleri şirket içi DNS sunucularına genişletebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="950e2-508">You can extend on-premises DNS servers to the virtual machines that are running in Azure.</span></span> <span data-ttu-id="950e2-509">Bu senaryoda DNS hizmeti çalışan Azure sanal makinelerin IP adreslerini ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="950e2-509">In that scenario, you can add the IP addresses of the Azure virtual machines on which you run the DNS service.</span></span>
    * <span data-ttu-id="950e2-510">[Yalnızca bulut dağıtım][planning-guide-2.1]: bir DNS sunucusu olarak hizmet veren aynı sanal ağ örneğinde ek bir sanal makine dağıtın.</span><span class="sxs-lookup"><span data-stu-id="950e2-510">[Cloud-only deployment][planning-guide-2.1]: Deploy an additional virtual machine in the same Virtual Network instance that serves as a DNS server.</span></span> <span data-ttu-id="950e2-511">DNS hizmeti çalıştırmak için ayarladığınız Azure sanal makinelerin IP adreslerini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="950e2-511">Add the IP addresses of the Azure virtual machines that you've set up to run DNS service.</span></span>

    ![Şekil 12: Azure sanal ağı için DNS sunucularını yapılandırın][sap-ha-guide-figure-3001]

    <span data-ttu-id="950e2-513">_**Şekil 12:** Yapılandır DNS sunucuları için Azure sanal ağ_</span><span class="sxs-lookup"><span data-stu-id="950e2-513">_**Figure 12:** Configure DNS servers for Azure Virtual Network_</span></span>

  > [!NOTE]
  > <span data-ttu-id="950e2-514">DNS sunucularının IP adreslerini değiştirirseniz, değişikliği uygulamak ve yeni DNS sunucularını yayılması için Azure sanal makineleri yeniden başlatmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="950e2-514">If you change the IP addresses of the DNS servers, you need to restart the Azure virtual machines to apply the change and propagate the new DNS servers.</span></span>
  >
  >

<span data-ttu-id="950e2-515">Bizim örneğimizde, DNS hizmeti yüklenir ve bu Windows sanal makinelerde yapılandırılır:</span><span class="sxs-lookup"><span data-stu-id="950e2-515">In our example, the DNS service is installed and configured on these Windows virtual machines:</span></span>

| <span data-ttu-id="950e2-516">Sanal makine rolü</span><span class="sxs-lookup"><span data-stu-id="950e2-516">Virtual machine role</span></span> | <span data-ttu-id="950e2-517">Sanal makine ana bilgisayar adı</span><span class="sxs-lookup"><span data-stu-id="950e2-517">Virtual machine host name</span></span> | <span data-ttu-id="950e2-518">Ağ kartı adı</span><span class="sxs-lookup"><span data-stu-id="950e2-518">Network card name</span></span> | <span data-ttu-id="950e2-519">Statik IP adresi</span><span class="sxs-lookup"><span data-stu-id="950e2-519">Static IP address</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="950e2-520">İlk DNS sunucusu</span><span class="sxs-lookup"><span data-stu-id="950e2-520">First DNS server</span></span> |<span data-ttu-id="950e2-521">domcontr-0</span><span class="sxs-lookup"><span data-stu-id="950e2-521">domcontr-0</span></span> |<span data-ttu-id="950e2-522">pr1-NIC-domcontr-0</span><span class="sxs-lookup"><span data-stu-id="950e2-522">pr1-nic-domcontr-0</span></span> |<span data-ttu-id="950e2-523">10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="950e2-523">10.0.0.10</span></span> |
| <span data-ttu-id="950e2-524">İkinci DNS sunucusu</span><span class="sxs-lookup"><span data-stu-id="950e2-524">Second DNS server</span></span> |<span data-ttu-id="950e2-525">domcontr-1</span><span class="sxs-lookup"><span data-stu-id="950e2-525">domcontr-1</span></span> |<span data-ttu-id="950e2-526">pr1-NIC-domcontr-1</span><span class="sxs-lookup"><span data-stu-id="950e2-526">pr1-nic-domcontr-1</span></span> |<span data-ttu-id="950e2-527">10.0.0.11</span><span class="sxs-lookup"><span data-stu-id="950e2-527">10.0.0.11</span></span> |

### <span data-ttu-id="950e2-528"><a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a>Ana bilgisayar adları ve SAP ASCS/SCS kümelenmiş örneği ve DBMS kümelenmiş örneği için statik IP adresleri</span><span class="sxs-lookup"><span data-stu-id="950e2-528"><a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a> Host names and static IP addresses for the SAP ASCS/SCS clustered instance and DBMS clustered instance</span></span>

<span data-ttu-id="950e2-529">Şirket içi dağıtım için bu ayrılmış ana bilgisayar adlarını ve IP adreslerini gerekir:</span><span class="sxs-lookup"><span data-stu-id="950e2-529">For on-premises deployment, you need these reserved host names and IP addresses:</span></span>

| <span data-ttu-id="950e2-530">Sanal ana bilgisayar adı rolü</span><span class="sxs-lookup"><span data-stu-id="950e2-530">Virtual host name role</span></span> | <span data-ttu-id="950e2-531">Sanal ana bilgisayar adı</span><span class="sxs-lookup"><span data-stu-id="950e2-531">Virtual host name</span></span> | <span data-ttu-id="950e2-532">Sanal statik IP adresi</span><span class="sxs-lookup"><span data-stu-id="950e2-532">Virtual static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="950e2-533">SAP ASCS/SCS ilk küme sanal ana bilgisayar adı (küme yönetimi)</span><span class="sxs-lookup"><span data-stu-id="950e2-533">SAP ASCS/SCS first cluster virtual host name (for cluster management)</span></span> |<span data-ttu-id="950e2-534">pr1 ascs VIR</span><span class="sxs-lookup"><span data-stu-id="950e2-534">pr1-ascs-vir</span></span> |<span data-ttu-id="950e2-535">10.0.0.42</span><span class="sxs-lookup"><span data-stu-id="950e2-535">10.0.0.42</span></span> |
| <span data-ttu-id="950e2-536">SAP ASCS/SCS örnek sanal ana bilgisayar adı</span><span class="sxs-lookup"><span data-stu-id="950e2-536">SAP ASCS/SCS instance virtual host name</span></span> |<span data-ttu-id="950e2-537">pr1 ascs sap</span><span class="sxs-lookup"><span data-stu-id="950e2-537">pr1-ascs-sap</span></span> |<span data-ttu-id="950e2-538">10.0.0.43</span><span class="sxs-lookup"><span data-stu-id="950e2-538">10.0.0.43</span></span> |
| <span data-ttu-id="950e2-539">SAP DBMS ikinci küme sanal ana bilgisayar adı (küme yönetimi)</span><span class="sxs-lookup"><span data-stu-id="950e2-539">SAP DBMS second cluster virtual host name (cluster management)</span></span> |<span data-ttu-id="950e2-540">pr1 dbms VIR</span><span class="sxs-lookup"><span data-stu-id="950e2-540">pr1-dbms-vir</span></span> |<span data-ttu-id="950e2-541">10.0.0.32</span><span class="sxs-lookup"><span data-stu-id="950e2-541">10.0.0.32</span></span> |

<span data-ttu-id="950e2-542">Kümeyi oluşturduğunuzda, sanal ana bilgisayar adlarını oluşturmak **pr1 ascs VIR** ve **pr1 dbms VIR** ve kümeyi yönetmek ilişkili IP adreslerini.</span><span class="sxs-lookup"><span data-stu-id="950e2-542">When you create the cluster, create the virtual host names **pr1-ascs-vir** and **pr1-dbms-vir** and the associated IP addresses that manage the cluster itself.</span></span> <span data-ttu-id="950e2-543">Bunun nasıl yapılacağı hakkında daha fazla bilgi için bkz: [toplamak küme düğümleri bir küme yapılandırmasında][sap-ha-guide-8.12.1].</span><span class="sxs-lookup"><span data-stu-id="950e2-543">For information about how to do this, see [Collect cluster nodes in a cluster configuration][sap-ha-guide-8.12.1].</span></span>

<span data-ttu-id="950e2-544">Diğer iki sanal ana bilgisayar adlarını, el ile oluşturabilirsiniz **pr1 ascs sap** ve **pr1 dbms sap**ve ilişkili IP adresleri, DNS sunucusu.</span><span class="sxs-lookup"><span data-stu-id="950e2-544">You can manually create the other two virtual host names, **pr1-ascs-sap** and **pr1-dbms-sap**, and the associated IP addresses, on the DNS server.</span></span> <span data-ttu-id="950e2-545">Kümelenmiş SAP ASCS/SCS örneği ve kümelenmiş DBMS örneği bu kaynakları kullanın.</span><span class="sxs-lookup"><span data-stu-id="950e2-545">The clustered SAP ASCS/SCS instance and the clustered DBMS instance use these resources.</span></span> <span data-ttu-id="950e2-546">Bunun nasıl yapılacağı hakkında daha fazla bilgi için bkz: [kümelenmiş bir SAP ASCS/SCS örneği için bir sanal ana bilgisayar adı oluşturmak][sap-ha-guide-9.1.1].</span><span class="sxs-lookup"><span data-stu-id="950e2-546">For information about how to do this, see [Create a virtual host name for a clustered SAP ASCS/SCS instance][sap-ha-guide-9.1.1].</span></span>

### <span data-ttu-id="950e2-547"><a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a>SAP sanal makineler için statik IP adresi ayarlayın</span><span class="sxs-lookup"><span data-stu-id="950e2-547"><a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a> Set static IP addresses for the SAP virtual machines</span></span>
<span data-ttu-id="950e2-548">Kümedeki sanal makinelerin dağıttıktan sonra tüm sanal makineler için statik IP adresi ayarlamak gerekir.</span><span class="sxs-lookup"><span data-stu-id="950e2-548">After you deploy the virtual machines to use in your cluster, you need to set static IP addresses for all virtual machines.</span></span> <span data-ttu-id="950e2-549">Bunu yapmak, Azure sanal ağ yapılandırması ve konuk işletim sistemi içinde değil.</span><span class="sxs-lookup"><span data-stu-id="950e2-549">Do this in the Azure Virtual Network configuration, and not in the guest operating system.</span></span>

1.  <span data-ttu-id="950e2-550">Azure portalında seçin **kaynak grubu** > **ağ kartı** > **ayarları** > **IP adresi**.</span><span class="sxs-lookup"><span data-stu-id="950e2-550">In the Azure portal, select **Resource Group** > **Network Card** > **Settings** > **IP Address**.</span></span>
2.  <span data-ttu-id="950e2-551">Üzerinde **IP adreslerini** dikey altında **atama**seçin **statik**.</span><span class="sxs-lookup"><span data-stu-id="950e2-551">On the **IP addresses** blade, under **Assignment**, select **Static**.</span></span> <span data-ttu-id="950e2-552">İçinde **IP adresi** kutusunda, kullanmak istediğiniz IP adresini girin.</span><span class="sxs-lookup"><span data-stu-id="950e2-552">In the **IP address** box, enter the IP address that you want to use.</span></span>

  > [!NOTE]
  > <span data-ttu-id="950e2-553">Ağ kartı IP adresini değiştirirseniz, değişikliği uygulamak için Azure sanal makineleri yeniden başlatmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="950e2-553">If you change the IP address of the network card, you need to restart the Azure virtual machines to apply the change.</span></span>  
  >
  >

  ![Şekil 13: statik IP adresleri her sanal makinenin ağ kartı için ayarlama][sap-ha-guide-figure-3002]

  <span data-ttu-id="950e2-555">_**Şekil 13:** ayarlamak, her bir sanal makinenin ağ kartı için statik IP adresleri_</span><span class="sxs-lookup"><span data-stu-id="950e2-555">_**Figure 13:** Set static IP addresses for the network card of each virtual machine_</span></span>

  <span data-ttu-id="950e2-556">Tüm sanal makineler için Active Directory DNS hizmetiniz için kullanmak istediğiniz sanal makineleri dahil olan tüm ağ arabirimleri için bu adımı yineleyin.</span><span class="sxs-lookup"><span data-stu-id="950e2-556">Repeat this step for all network interfaces, that is, for all virtual machines, including virtual machines that you want to use for your Active Directory/DNS service.</span></span>

<span data-ttu-id="950e2-557">Bizim örneğimizde, bu sanal makineleri ve statik IP adresleri vardır:</span><span class="sxs-lookup"><span data-stu-id="950e2-557">In our example, we have these virtual machines and static IP addresses:</span></span>

| <span data-ttu-id="950e2-558">Sanal makine rolü</span><span class="sxs-lookup"><span data-stu-id="950e2-558">Virtual machine role</span></span> | <span data-ttu-id="950e2-559">Sanal makine ana bilgisayar adı</span><span class="sxs-lookup"><span data-stu-id="950e2-559">Virtual machine host name</span></span> | <span data-ttu-id="950e2-560">Ağ kartı adı</span><span class="sxs-lookup"><span data-stu-id="950e2-560">Network card name</span></span> | <span data-ttu-id="950e2-561">Statik IP adresi</span><span class="sxs-lookup"><span data-stu-id="950e2-561">Static IP address</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="950e2-562">İlk SAP uygulama sunucusu örneği</span><span class="sxs-lookup"><span data-stu-id="950e2-562">First SAP Application Server instance</span></span> |<span data-ttu-id="950e2-563">pr1 dı 0</span><span class="sxs-lookup"><span data-stu-id="950e2-563">pr1-di-0</span></span> |<span data-ttu-id="950e2-564">pr1-NIC-dı-0</span><span class="sxs-lookup"><span data-stu-id="950e2-564">pr1-nic-di-0</span></span> |<span data-ttu-id="950e2-565">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="950e2-565">10.0.0.50</span></span> |
| <span data-ttu-id="950e2-566">İkinci SAP uygulama sunucusu örneği</span><span class="sxs-lookup"><span data-stu-id="950e2-566">Second SAP Application Server instance</span></span> |<span data-ttu-id="950e2-567">pr1 dı 1</span><span class="sxs-lookup"><span data-stu-id="950e2-567">pr1-di-1</span></span> |<span data-ttu-id="950e2-568">pr1-NIC-dı-1</span><span class="sxs-lookup"><span data-stu-id="950e2-568">pr1-nic-di-1</span></span> |<span data-ttu-id="950e2-569">10.0.0.51</span><span class="sxs-lookup"><span data-stu-id="950e2-569">10.0.0.51</span></span> |
| <span data-ttu-id="950e2-570">...</span><span class="sxs-lookup"><span data-stu-id="950e2-570">...</span></span> |<span data-ttu-id="950e2-571">...</span><span class="sxs-lookup"><span data-stu-id="950e2-571">...</span></span> |<span data-ttu-id="950e2-572">...</span><span class="sxs-lookup"><span data-stu-id="950e2-572">...</span></span> |<span data-ttu-id="950e2-573">...</span><span class="sxs-lookup"><span data-stu-id="950e2-573">...</span></span> |
| <span data-ttu-id="950e2-574">Son SAP uygulama sunucusu örneği</span><span class="sxs-lookup"><span data-stu-id="950e2-574">Last SAP Application Server instance</span></span> |<span data-ttu-id="950e2-575">pr1 dı 5</span><span class="sxs-lookup"><span data-stu-id="950e2-575">pr1-di-5</span></span> |<span data-ttu-id="950e2-576">pr1-NIC-dı-5</span><span class="sxs-lookup"><span data-stu-id="950e2-576">pr1-nic-di-5</span></span> |<span data-ttu-id="950e2-577">10.0.0.55</span><span class="sxs-lookup"><span data-stu-id="950e2-577">10.0.0.55</span></span> |
| <span data-ttu-id="950e2-578">İlk küme düğümüne ASCS/SCS örneği için</span><span class="sxs-lookup"><span data-stu-id="950e2-578">First cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="950e2-579">pr1 ascs 0</span><span class="sxs-lookup"><span data-stu-id="950e2-579">pr1-ascs-0</span></span> |<span data-ttu-id="950e2-580">pr1-NIC-ascs-0</span><span class="sxs-lookup"><span data-stu-id="950e2-580">pr1-nic-ascs-0</span></span> |<span data-ttu-id="950e2-581">10.0.0.40</span><span class="sxs-lookup"><span data-stu-id="950e2-581">10.0.0.40</span></span> |
| <span data-ttu-id="950e2-582">İkinci küme düğümü ASCS/SCS örneği için</span><span class="sxs-lookup"><span data-stu-id="950e2-582">Second cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="950e2-583">pr1 ascs 1</span><span class="sxs-lookup"><span data-stu-id="950e2-583">pr1-ascs-1</span></span> |<span data-ttu-id="950e2-584">pr1-NIC-ascs-1</span><span class="sxs-lookup"><span data-stu-id="950e2-584">pr1-nic-ascs-1</span></span> |<span data-ttu-id="950e2-585">10.0.0.41</span><span class="sxs-lookup"><span data-stu-id="950e2-585">10.0.0.41</span></span> |
| <span data-ttu-id="950e2-586">İlk küme düğümüne DBMS örneği için</span><span class="sxs-lookup"><span data-stu-id="950e2-586">First cluster node for DBMS instance</span></span> |<span data-ttu-id="950e2-587">pr1-db-0</span><span class="sxs-lookup"><span data-stu-id="950e2-587">pr1-db-0</span></span> |<span data-ttu-id="950e2-588">pr1-NIC-db-0</span><span class="sxs-lookup"><span data-stu-id="950e2-588">pr1-nic-db-0</span></span> |<span data-ttu-id="950e2-589">10.0.0.30</span><span class="sxs-lookup"><span data-stu-id="950e2-589">10.0.0.30</span></span> |
| <span data-ttu-id="950e2-590">DBMS örneği için ikinci küme düğümü</span><span class="sxs-lookup"><span data-stu-id="950e2-590">Second cluster node for DBMS instance</span></span> |<span data-ttu-id="950e2-591">pr1-db-1</span><span class="sxs-lookup"><span data-stu-id="950e2-591">pr1-db-1</span></span> |<span data-ttu-id="950e2-592">pr1-NIC-db-1</span><span class="sxs-lookup"><span data-stu-id="950e2-592">pr1-nic-db-1</span></span> |<span data-ttu-id="950e2-593">10.0.0.31</span><span class="sxs-lookup"><span data-stu-id="950e2-593">10.0.0.31</span></span> |

### <span data-ttu-id="950e2-594"><a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a>Azure iç yük dengeleyici için statik bir IP adresi ayarlayın</span><span class="sxs-lookup"><span data-stu-id="950e2-594"><a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a> Set a static IP address for the Azure internal load balancer</span></span>

<span data-ttu-id="950e2-595">SAP Azure Resource Manager şablonu SAP ASCS/SCS örnek küme ve DBMS küme için kullanılan bir Azure iç yük dengeleyici oluşturur.</span><span class="sxs-lookup"><span data-stu-id="950e2-595">The SAP Azure Resource Manager template creates an Azure internal load balancer that is used for the SAP ASCS/SCS instance cluster and the DBMS cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="950e2-596">Sanal ana bilgisayar adını SAP ASCS/SCS IP adresini SAP ASCS/SCS iç yük dengeleyici IP adresi ile aynıdır: **pr1 lb ascs**.</span><span class="sxs-lookup"><span data-stu-id="950e2-596">The IP address of the virtual host name of the SAP ASCS/SCS is the same as the IP address of the SAP ASCS/SCS internal load balancer: **pr1-lb-ascs**.</span></span>
> <span data-ttu-id="950e2-597">DBMS sanal adını IP adresini DBMS iç yük dengeleyici IP adresi ile aynıdır: **pr1 lb dbms**.</span><span class="sxs-lookup"><span data-stu-id="950e2-597">The IP address of the virtual name of the DBMS is the same as the IP address of the DBMS internal load balancer: **pr1-lb-dbms**.</span></span>
>
>

<span data-ttu-id="950e2-598">Azure iç yük dengeleyici için statik bir IP adresi ayarlamak için:</span><span class="sxs-lookup"><span data-stu-id="950e2-598">To set a static IP address for the Azure internal load balancer:</span></span>

1.  <span data-ttu-id="950e2-599">İç yük dengeleyici IP adresi ilk dağıtım ayarlar **dinamik**.</span><span class="sxs-lookup"><span data-stu-id="950e2-599">The initial deployment sets the internal load balancer IP address to **Dynamic**.</span></span> <span data-ttu-id="950e2-600">Azure portalında üzerinde **IP adreslerini** dikey altında **atama**seçin **statik**.</span><span class="sxs-lookup"><span data-stu-id="950e2-600">In the Azure portal, on the **IP addresses** blade, under **Assignment**, select **Static**.</span></span>
2.  <span data-ttu-id="950e2-601">İç yük dengeleyici IP adresi kümesi **pr1 lb ascs** SAP ASCS/SCS örneğinin sanal ana bilgisayar adı IP adresine.</span><span class="sxs-lookup"><span data-stu-id="950e2-601">Set the IP address of the internal load balancer **pr1-lb-ascs** to the IP address of the virtual host name of the SAP ASCS/SCS instance.</span></span>
3.  <span data-ttu-id="950e2-602">İç yük dengeleyici IP adresi kümesi **pr1 lb dbms** DBMS örneğinin sanal ana bilgisayar adı IP adresine.</span><span class="sxs-lookup"><span data-stu-id="950e2-602">Set the IP address of the internal load balancer **pr1-lb-dbms** to the IP address of the virtual host name of the DBMS instance.</span></span>

  ![Şekil 14: SAP ASCS/SCS örneği için iç yük dengeleyici için statik IP adresleri ayarlayın.][sap-ha-guide-figure-3003]

  <span data-ttu-id="950e2-604">_**Şekil 14:** SAP ASCS/SCS örneği için iç yük dengeleyici için statik IP adresleri ayarlayın_</span><span class="sxs-lookup"><span data-stu-id="950e2-604">_**Figure 14:** Set static IP addresses for the internal load balancer for the SAP ASCS/SCS instance_</span></span>

<span data-ttu-id="950e2-605">Bizim örneğimizde, biz bu statik IP adresine sahip iki Azure iç yük dengeleyicileri vardır:</span><span class="sxs-lookup"><span data-stu-id="950e2-605">In our example, we have two Azure internal load balancers that have these static IP addresses:</span></span>

| <span data-ttu-id="950e2-606">Azure iç yük dengeleyici rol</span><span class="sxs-lookup"><span data-stu-id="950e2-606">Azure internal load balancer role</span></span> | <span data-ttu-id="950e2-607">Azure iç yük dengeleyicisi adı</span><span class="sxs-lookup"><span data-stu-id="950e2-607">Azure internal load balancer name</span></span> | <span data-ttu-id="950e2-608">Statik IP adresi</span><span class="sxs-lookup"><span data-stu-id="950e2-608">Static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="950e2-609">SAP ASCS/SCS iç yük dengeleyici örneği</span><span class="sxs-lookup"><span data-stu-id="950e2-609">SAP ASCS/SCS instance internal load balancer</span></span> |<span data-ttu-id="950e2-610">pr1 lb ascs</span><span class="sxs-lookup"><span data-stu-id="950e2-610">pr1-lb-ascs</span></span> |<span data-ttu-id="950e2-611">10.0.0.43</span><span class="sxs-lookup"><span data-stu-id="950e2-611">10.0.0.43</span></span> |
| <span data-ttu-id="950e2-612">SAP DBMS iç yük dengeleyici</span><span class="sxs-lookup"><span data-stu-id="950e2-612">SAP DBMS internal load balancer</span></span> |<span data-ttu-id="950e2-613">pr1 lb dbms</span><span class="sxs-lookup"><span data-stu-id="950e2-613">pr1-lb-dbms</span></span> |<span data-ttu-id="950e2-614">10.0.0.33</span><span class="sxs-lookup"><span data-stu-id="950e2-614">10.0.0.33</span></span> |


### <span data-ttu-id="950e2-615"><a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a>Varsayılan ASCS/SCS Yük Dengeleme kuralları Azure iç yük dengeleyici için</span><span class="sxs-lookup"><span data-stu-id="950e2-615"><a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a> Default ASCS/SCS load balancing rules for the Azure internal load balancer</span></span>

<span data-ttu-id="950e2-616">SAP Azure Resource Manager şablonu gereksinim duyduğunuz bağlantı noktalarını oluşturur:</span><span class="sxs-lookup"><span data-stu-id="950e2-616">The SAP Azure Resource Manager template creates the ports you need:</span></span>
* <span data-ttu-id="950e2-617">Varsayılan örneği numarasıyla ABAP ASCS örneği **00**</span><span class="sxs-lookup"><span data-stu-id="950e2-617">An ABAP ASCS instance, with the default instance number **00**</span></span>
* <span data-ttu-id="950e2-618">Bir Java SCS örneğiyle varsayılan örnek numarasını **01**</span><span class="sxs-lookup"><span data-stu-id="950e2-618">A Java SCS instance, with the default instance number **01**</span></span>

<span data-ttu-id="950e2-619">SAP ASCS/SCS örneğinizi yüklediğinizde, varsayılan örnek numarasını kullanmalıdır **00** ABAP ASCS örneğinizi ve varsayılan örnek sayısı için **01** Java SCS Örneğiniz için.</span><span class="sxs-lookup"><span data-stu-id="950e2-619">When you install your SAP ASCS/SCS instance, you must use the default instance number **00** for your ABAP ASCS instance and the default instance number **01** for your Java SCS instance.</span></span>

<span data-ttu-id="950e2-620">Ardından, gerekli iç Yük Dengeleme SAP NetWeaver bağlantı noktaları için uç noktaları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="950e2-620">Next, create required internal load balancing endpoints for the SAP NetWeaver ports.</span></span>

<span data-ttu-id="950e2-621">Gerekli iç Yük Dengeleme uç noktaları oluşturmak için ilk olarak, bu Yük Dengeleme SAP NetWeaver ABAP ASCS bağlantı noktaları için uç nokta oluşturun:</span><span class="sxs-lookup"><span data-stu-id="950e2-621">To create required internal load balancing endpoints, first, create these load balancing endpoints for the SAP NetWeaver ABAP ASCS ports:</span></span>

| <span data-ttu-id="950e2-622">Hizmet/Yük Dengeleme kuralı adı</span><span class="sxs-lookup"><span data-stu-id="950e2-622">Service/load balancing rule name</span></span> | <span data-ttu-id="950e2-623">Varsayılan bağlantı noktası numaraları</span><span class="sxs-lookup"><span data-stu-id="950e2-623">Default port numbers</span></span> | <span data-ttu-id="950e2-624">Somut için bağlantı noktalarını (ASCS örneği ile örnek numarasını 00) (ERS 10 ile)</span><span class="sxs-lookup"><span data-stu-id="950e2-624">Concrete ports for (ASCS instance with instance number 00) (ERS with 10)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="950e2-625">Sıraya alma sunucu / *lbrule3200*</span><span class="sxs-lookup"><span data-stu-id="950e2-625">Enqueue Server / *lbrule3200*</span></span> |<span data-ttu-id="950e2-626">32 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="950e2-626">32<*InstanceNumber*></span></span> |<span data-ttu-id="950e2-627">3200</span><span class="sxs-lookup"><span data-stu-id="950e2-627">3200</span></span> |
| <span data-ttu-id="950e2-628">ABAP ileti sunucusu / *lbrule3600*</span><span class="sxs-lookup"><span data-stu-id="950e2-628">ABAP Message Server / *lbrule3600*</span></span> |<span data-ttu-id="950e2-629">36 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="950e2-629">36<*InstanceNumber*></span></span> |<span data-ttu-id="950e2-630">3600</span><span class="sxs-lookup"><span data-stu-id="950e2-630">3600</span></span> |
| <span data-ttu-id="950e2-631">İç ABAP ileti / *lbrule3900*</span><span class="sxs-lookup"><span data-stu-id="950e2-631">Internal ABAP Message / *lbrule3900*</span></span> |<span data-ttu-id="950e2-632">39 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="950e2-632">39<*InstanceNumber*></span></span> |<span data-ttu-id="950e2-633">3900</span><span class="sxs-lookup"><span data-stu-id="950e2-633">3900</span></span> |
| <span data-ttu-id="950e2-634">Sunucu HTTP iletisi / *Lbrule8100*</span><span class="sxs-lookup"><span data-stu-id="950e2-634">Message Server HTTP / *Lbrule8100*</span></span> |<span data-ttu-id="950e2-635">81 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="950e2-635">81<*InstanceNumber*></span></span> |<span data-ttu-id="950e2-636">8100</span><span class="sxs-lookup"><span data-stu-id="950e2-636">8100</span></span> |
| <span data-ttu-id="950e2-637">SAP başlangıç hizmet ASCS HTTP / *Lbrule50013*</span><span class="sxs-lookup"><span data-stu-id="950e2-637">SAP Start Service ASCS HTTP / *Lbrule50013*</span></span> |<span data-ttu-id="950e2-638">5 <*InstanceNumber*> 13</span><span class="sxs-lookup"><span data-stu-id="950e2-638">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="950e2-639">50013</span><span class="sxs-lookup"><span data-stu-id="950e2-639">50013</span></span> |
| <span data-ttu-id="950e2-640">SAP başlangıç hizmet ASCS HTTPS / *Lbrule50014*</span><span class="sxs-lookup"><span data-stu-id="950e2-640">SAP Start Service ASCS HTTPS / *Lbrule50014*</span></span> |<span data-ttu-id="950e2-641">5 <*InstanceNumber*> 14</span><span class="sxs-lookup"><span data-stu-id="950e2-641">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="950e2-642">50014</span><span class="sxs-lookup"><span data-stu-id="950e2-642">50014</span></span> |
| <span data-ttu-id="950e2-643">Sıraya alma çoğaltma / *Lbrule50016*</span><span class="sxs-lookup"><span data-stu-id="950e2-643">Enqueue Replication / *Lbrule50016*</span></span> |<span data-ttu-id="950e2-644">5 <*InstanceNumber*> 16</span><span class="sxs-lookup"><span data-stu-id="950e2-644">5<*InstanceNumber*>16</span></span> |<span data-ttu-id="950e2-645">50016</span><span class="sxs-lookup"><span data-stu-id="950e2-645">50016</span></span> |
| <span data-ttu-id="950e2-646">SAP başlangıç hizmeti ERS HTTP *Lbrule51013*</span><span class="sxs-lookup"><span data-stu-id="950e2-646">SAP Start Service ERS HTTP *Lbrule51013*</span></span> |<span data-ttu-id="950e2-647">5 <*InstanceNumber*> 13</span><span class="sxs-lookup"><span data-stu-id="950e2-647">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="950e2-648">51013</span><span class="sxs-lookup"><span data-stu-id="950e2-648">51013</span></span> |
| <span data-ttu-id="950e2-649">SAP başlangıç hizmeti ERS HTTP *Lbrule51014*</span><span class="sxs-lookup"><span data-stu-id="950e2-649">SAP Start Service ERS HTTP *Lbrule51014*</span></span> |<span data-ttu-id="950e2-650">5 <*InstanceNumber*> 14</span><span class="sxs-lookup"><span data-stu-id="950e2-650">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="950e2-651">51014</span><span class="sxs-lookup"><span data-stu-id="950e2-651">51014</span></span> |
| <span data-ttu-id="950e2-652">RM win *Lbrule5985*</span><span class="sxs-lookup"><span data-stu-id="950e2-652">Win RM *Lbrule5985*</span></span> | |<span data-ttu-id="950e2-653">5985</span><span class="sxs-lookup"><span data-stu-id="950e2-653">5985</span></span> |
| <span data-ttu-id="950e2-654">Dosya Paylaşımı *Lbrule445*</span><span class="sxs-lookup"><span data-stu-id="950e2-654">File Share *Lbrule445*</span></span> | |<span data-ttu-id="950e2-655">445</span><span class="sxs-lookup"><span data-stu-id="950e2-655">445</span></span> |

<span data-ttu-id="950e2-656">_**Tablo 1:** bağlantı noktası numaralarını SAP NetWeaver ABAP ASCS örnekleri_</span><span class="sxs-lookup"><span data-stu-id="950e2-656">_**Table 1:** Port numbers of the SAP NetWeaver ABAP ASCS instances_</span></span>

<span data-ttu-id="950e2-657">Ardından, bu Yük Dengeleme SAP NetWeaver Java SCS bağlantı noktaları için uç nokta oluşturun:</span><span class="sxs-lookup"><span data-stu-id="950e2-657">Then, create these load balancing endpoints for the SAP NetWeaver Java SCS ports:</span></span>

| <span data-ttu-id="950e2-658">Hizmet/Yük Dengeleme kuralı adı</span><span class="sxs-lookup"><span data-stu-id="950e2-658">Service/load balancing rule name</span></span> | <span data-ttu-id="950e2-659">Varsayılan bağlantı noktası numaraları</span><span class="sxs-lookup"><span data-stu-id="950e2-659">Default port numbers</span></span> | <span data-ttu-id="950e2-660">Somut için bağlantı noktalarını (SCS örneği ile örnek numarasını 01) (ERS 11 ile)</span><span class="sxs-lookup"><span data-stu-id="950e2-660">Concrete ports for (SCS instance with instance number 01) (ERS with 11)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="950e2-661">Sıraya alma sunucu / *lbrule3201*</span><span class="sxs-lookup"><span data-stu-id="950e2-661">Enqueue Server / *lbrule3201*</span></span> |<span data-ttu-id="950e2-662">32 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="950e2-662">32<*InstanceNumber*></span></span> |<span data-ttu-id="950e2-663">3201</span><span class="sxs-lookup"><span data-stu-id="950e2-663">3201</span></span> |
| <span data-ttu-id="950e2-664">Ağ Geçidi sunucusu / *lbrule3301*</span><span class="sxs-lookup"><span data-stu-id="950e2-664">Gateway Server / *lbrule3301*</span></span> |<span data-ttu-id="950e2-665">33 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="950e2-665">33<*InstanceNumber*></span></span> |<span data-ttu-id="950e2-666">3301</span><span class="sxs-lookup"><span data-stu-id="950e2-666">3301</span></span> |
| <span data-ttu-id="950e2-667">Java ileti sunucusu / *lbrule3900*</span><span class="sxs-lookup"><span data-stu-id="950e2-667">Java Message Server / *lbrule3900*</span></span> |<span data-ttu-id="950e2-668">39 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="950e2-668">39<*InstanceNumber*></span></span> |<span data-ttu-id="950e2-669">3901</span><span class="sxs-lookup"><span data-stu-id="950e2-669">3901</span></span> |
| <span data-ttu-id="950e2-670">Sunucu HTTP iletisi / *Lbrule8101*</span><span class="sxs-lookup"><span data-stu-id="950e2-670">Message Server HTTP / *Lbrule8101*</span></span> |<span data-ttu-id="950e2-671">81 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="950e2-671">81<*InstanceNumber*></span></span> |<span data-ttu-id="950e2-672">8101</span><span class="sxs-lookup"><span data-stu-id="950e2-672">8101</span></span> |
| <span data-ttu-id="950e2-673">SAP başlangıç hizmet SCS HTTP / *Lbrule50113*</span><span class="sxs-lookup"><span data-stu-id="950e2-673">SAP Start Service SCS HTTP / *Lbrule50113*</span></span> |<span data-ttu-id="950e2-674">5 <*InstanceNumber*> 13</span><span class="sxs-lookup"><span data-stu-id="950e2-674">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="950e2-675">50113</span><span class="sxs-lookup"><span data-stu-id="950e2-675">50113</span></span> |
| <span data-ttu-id="950e2-676">SAP başlangıç hizmet SCS HTTPS / *Lbrule50114*</span><span class="sxs-lookup"><span data-stu-id="950e2-676">SAP Start Service SCS HTTPS / *Lbrule50114*</span></span> |<span data-ttu-id="950e2-677">5 <*InstanceNumber*> 14</span><span class="sxs-lookup"><span data-stu-id="950e2-677">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="950e2-678">50114</span><span class="sxs-lookup"><span data-stu-id="950e2-678">50114</span></span> |
| <span data-ttu-id="950e2-679">Sıraya alma çoğaltma / *Lbrule50116*</span><span class="sxs-lookup"><span data-stu-id="950e2-679">Enqueue Replication / *Lbrule50116*</span></span> |<span data-ttu-id="950e2-680">5 <*InstanceNumber*> 16</span><span class="sxs-lookup"><span data-stu-id="950e2-680">5<*InstanceNumber*>16</span></span> |<span data-ttu-id="950e2-681">50116</span><span class="sxs-lookup"><span data-stu-id="950e2-681">50116</span></span> |
| <span data-ttu-id="950e2-682">SAP başlangıç hizmeti ERS HTTP *Lbrule51113*</span><span class="sxs-lookup"><span data-stu-id="950e2-682">SAP Start Service ERS HTTP *Lbrule51113*</span></span> |<span data-ttu-id="950e2-683">5 <*InstanceNumber*> 13</span><span class="sxs-lookup"><span data-stu-id="950e2-683">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="950e2-684">51113</span><span class="sxs-lookup"><span data-stu-id="950e2-684">51113</span></span> |
| <span data-ttu-id="950e2-685">SAP başlangıç hizmeti ERS HTTP *Lbrule51114*</span><span class="sxs-lookup"><span data-stu-id="950e2-685">SAP Start Service ERS HTTP *Lbrule51114*</span></span> |<span data-ttu-id="950e2-686">5 <*InstanceNumber*> 14</span><span class="sxs-lookup"><span data-stu-id="950e2-686">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="950e2-687">51114</span><span class="sxs-lookup"><span data-stu-id="950e2-687">51114</span></span> |
| <span data-ttu-id="950e2-688">RM win *Lbrule5985*</span><span class="sxs-lookup"><span data-stu-id="950e2-688">Win RM *Lbrule5985*</span></span> | |<span data-ttu-id="950e2-689">5985</span><span class="sxs-lookup"><span data-stu-id="950e2-689">5985</span></span> |
| <span data-ttu-id="950e2-690">Dosya Paylaşımı *Lbrule445*</span><span class="sxs-lookup"><span data-stu-id="950e2-690">File Share *Lbrule445*</span></span> | |<span data-ttu-id="950e2-691">445</span><span class="sxs-lookup"><span data-stu-id="950e2-691">445</span></span> |

<span data-ttu-id="950e2-692">_**Tablo 2:** bağlantı noktası numaralarını SAP NetWeaver Java SCS örnekleri_</span><span class="sxs-lookup"><span data-stu-id="950e2-692">_**Table 2:** Port numbers of the SAP NetWeaver Java SCS instances_</span></span>

![Şekil 15: varsayılan ASCS/SCS Yük Dengeleme kuralları Azure iç yük dengeleyici için][sap-ha-guide-figure-3004]

<span data-ttu-id="950e2-694">_**Şekil 15:** varsayılan ASCS/SCS Yük Dengeleme kuralları Azure iç yük dengeleyici için_</span><span class="sxs-lookup"><span data-stu-id="950e2-694">_**Figure 15:** Default ASCS/SCS load balancing rules for the Azure internal load balancer_</span></span>

<span data-ttu-id="950e2-695">Yük Dengeleyici IP adresi kümesi **pr1 lb dbms** DBMS örneğinin sanal ana bilgisayar adı IP adresine.</span><span class="sxs-lookup"><span data-stu-id="950e2-695">Set the IP address of the load balancer **pr1-lb-dbms** to the IP address of the virtual host name of the DBMS instance.</span></span>

### <span data-ttu-id="950e2-696"><a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a>ASCS/SCS varsayılan Yük Dengeleme kuralları Azure iç yük dengeleyici için değiştirme</span><span class="sxs-lookup"><span data-stu-id="950e2-696"><a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a> Change the ASCS/SCS default load balancing rules for the Azure internal load balancer</span></span>

<span data-ttu-id="950e2-697">SAP ASCS veya SCS örnekleri için farklı numaraları kullanmak istiyorsanız, adlarını ve değerlerini kendi bağlantı noktalarının varsayılan değerleri değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="950e2-697">If you want to use different numbers for the SAP ASCS or SCS instances, you must change the names and values of their ports from default values.</span></span>

1.  <span data-ttu-id="950e2-698">Azure portalında seçin  **<* SID*> - lb - ascs yük dengeleyici ** > **Yük Dengeleme kuralları**.</span><span class="sxs-lookup"><span data-stu-id="950e2-698">In the Azure portal, select **<*SID*>-lb-ascs load balancer** > **Load Balancing Rules**.</span></span>
2.  <span data-ttu-id="950e2-699">Tüm Yük Dengeleme SAP ASCS veya SCS örneğine ait kuralları için bu değerleri değiştirin:</span><span class="sxs-lookup"><span data-stu-id="950e2-699">For all load balancing rules that belong to the SAP ASCS or SCS instance, change these values:</span></span>

  * <span data-ttu-id="950e2-700">Ad</span><span class="sxs-lookup"><span data-stu-id="950e2-700">Name</span></span>
  * <span data-ttu-id="950e2-701">Bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="950e2-701">Port</span></span>
  * <span data-ttu-id="950e2-702">Arka uç bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="950e2-702">Back-end port</span></span>

  <span data-ttu-id="950e2-703">Örneğin, varsayılan ASCS örnek numarasını 00-31 değiştirmek istiyorsanız, Tablo 1'de listelenen tüm bağlantı noktaları için değişiklikler yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="950e2-703">For example, if you want to change the default ASCS instance number from 00 to 31, you need to make the changes for all ports listed in Table 1.</span></span>

  <span data-ttu-id="950e2-704">Bağlantı noktası için bir güncelleştirme örneği *lbrule3200*.</span><span class="sxs-lookup"><span data-stu-id="950e2-704">Here's an example of an update for port *lbrule3200*.</span></span>

  ![Şekil 16: ASCS/SCS varsayılan Yük Dengeleme kuralları Azure iç yük dengeleyici için değiştirme][sap-ha-guide-figure-3005]

  <span data-ttu-id="950e2-706">_**Şekil 16:** ASCS/SCS varsayılan Yük Dengeleme kuralları Azure iç yük dengeleyici için değiştirme_</span><span class="sxs-lookup"><span data-stu-id="950e2-706">_**Figure 16:** Change the ASCS/SCS default load balancing rules for the Azure internal load balancer_</span></span>

### <span data-ttu-id="950e2-707"><a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a>Windows sanal makine etki alanına ekleyin</span><span class="sxs-lookup"><span data-stu-id="950e2-707"><a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a> Add Windows virtual machines to the domain</span></span>

<span data-ttu-id="950e2-708">Sanal makineler için statik bir IP adresi atadıktan sonra sanal makine etki alanına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="950e2-708">After you assign a static IP address to the virtual machines, add the virtual machines to the domain.</span></span>

![Şekil 17: bir sanal makine bir etki alanına ekleyin.][sap-ha-guide-figure-3006]

<span data-ttu-id="950e2-710">_**Şekil 17:** bir sanal makine bir etki alanına ekleme_</span><span class="sxs-lookup"><span data-stu-id="950e2-710">_**Figure 17:** Add a virtual machine to a domain_</span></span>

### <span data-ttu-id="950e2-711"><a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a>SAP ASCS/SCS örneği her iki küme düğümleri üzerinde kayıt defteri girdilerini ekleyin</span><span class="sxs-lookup"><span data-stu-id="950e2-711"><a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a> Add registry entries on both cluster nodes of the SAP ASCS/SCS instance</span></span>

<span data-ttu-id="950e2-712">Azure yük dengeleyici bağlantıları ayarlanmış bir süre boyunca boşta olduğunda kapanır bağlantıları (boşta zaman aşımı) zaman bir iç yük dengeleyici sahiptir.</span><span class="sxs-lookup"><span data-stu-id="950e2-712">Azure Load Balancer has an internal load balancer that closes connections when the connections are idle for a set period of time (an idle timeout).</span></span> <span data-ttu-id="950e2-713">İlk sıraya alma/dequeue gönderilmesi gerekiyor isteği hemen SAP iş iletişim örnekleri açık bağlantıları SAP sıraya alma işlemlerinde işleyin.</span><span class="sxs-lookup"><span data-stu-id="950e2-713">SAP work processes in dialog instances open connections to the SAP enqueue process as soon as the first enqueue/dequeue request needs to be sent.</span></span> <span data-ttu-id="950e2-714">Bu bağlantılar genellikle iş işlemi kadar kurulan kalmasını veya sıraya alma işlemi yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="950e2-714">These connections usually remain established until the work process or the enqueue process restarts.</span></span> <span data-ttu-id="950e2-715">Ancak, belirlenen bir süre için bağlantı boşta kalırsa Azure iç yük dengeleyicisi bağlantıları kapatır.</span><span class="sxs-lookup"><span data-stu-id="950e2-715">However, if the connection is idle for a set period of time, the Azure internal load balancer closes the connections.</span></span> <span data-ttu-id="950e2-716">Artık yoksa SAP iş işlemi sıraya alma işlemi için bağlantıyı yeniden kurar çünkü bu bir sorun değildir.</span><span class="sxs-lookup"><span data-stu-id="950e2-716">This isn't a problem because the SAP work process reestablishes the connection to the enqueue process if it no longer exists.</span></span> <span data-ttu-id="950e2-717">Bu etkinlikler SAP işlemlerini Geliştirici izlerini belgelenen, ancak bunlar büyük miktarda ek içerik bu izlemeler oluşturur.</span><span class="sxs-lookup"><span data-stu-id="950e2-717">These activities are documented in the developer traces of SAP processes, but they create a large amount of extra content in those traces.</span></span> <span data-ttu-id="950e2-718">TCP/IP'yi değiştirmek için iyi bir fikirdir `KeepAliveTime` ve `KeepAliveInterval` her iki küme düğümlerinde.</span><span class="sxs-lookup"><span data-stu-id="950e2-718">It's a good idea to change the TCP/IP `KeepAliveTime` and `KeepAliveInterval` on both cluster nodes.</span></span> <span data-ttu-id="950e2-719">Bu değişiklikler makalenin sonraki bölümlerinde açıklanan SAP profili parametreleri TCP/IP'yi parametrelerle ile birleştirin.</span><span class="sxs-lookup"><span data-stu-id="950e2-719">Combine these changes in the TCP/IP parameters with SAP profile parameters, described later in the article.</span></span>

<span data-ttu-id="950e2-720">Kayıt defteri girdileri SAP ASCS/SCS örneği üzerinde her iki küme düğümü eklemek için ilk olarak, bu Windows kayıt defteri girdileri hem Windows Küme düğümlerinde SAP ASCS/SCS için ekleyin:</span><span class="sxs-lookup"><span data-stu-id="950e2-720">To add registry entries on both cluster nodes of the SAP ASCS/SCS instance, first, add these Windows registry entries on both Windows cluster nodes for SAP ASCS/SCS:</span></span>

| <span data-ttu-id="950e2-721">Yol</span><span class="sxs-lookup"><span data-stu-id="950e2-721">Path</span></span> | <span data-ttu-id="950e2-722">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span><span class="sxs-lookup"><span data-stu-id="950e2-722">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span></span> |
| --- | --- |
| <span data-ttu-id="950e2-723">Değişken adı</span><span class="sxs-lookup"><span data-stu-id="950e2-723">Variable name</span></span> |`KeepAliveTime` |
| <span data-ttu-id="950e2-724">Değişken türü</span><span class="sxs-lookup"><span data-stu-id="950e2-724">Variable type</span></span> |<span data-ttu-id="950e2-725">REG_DWORD (ondalık)</span><span class="sxs-lookup"><span data-stu-id="950e2-725">REG_DWORD (Decimal)</span></span> |
| <span data-ttu-id="950e2-726">Değer</span><span class="sxs-lookup"><span data-stu-id="950e2-726">Value</span></span> |<span data-ttu-id="950e2-727">120000</span><span class="sxs-lookup"><span data-stu-id="950e2-727">120000</span></span> |
| <span data-ttu-id="950e2-728">Belgelere bağlantı</span><span class="sxs-lookup"><span data-stu-id="950e2-728">Link to documentation</span></span> |[<span data-ttu-id="950e2-729">https://technet.microsoft.com/en-us/library/cc957549.aspx</span><span class="sxs-lookup"><span data-stu-id="950e2-729">https://technet.microsoft.com/en-us/library/cc957549.aspx</span></span>](https://technet.microsoft.com/en-us/library/cc957549.aspx) |

<span data-ttu-id="950e2-730">_**Tablo 3:** ilk TCP/IP'yi parametre değiştirme_</span><span class="sxs-lookup"><span data-stu-id="950e2-730">_**Table 3:** Change the first TCP/IP parameter_</span></span>

<span data-ttu-id="950e2-731">Daha sonra bu Windows kayıt defteri girdileri SAP ASCS/SCS için hem Windows küme düğümlerine ekleyin:</span><span class="sxs-lookup"><span data-stu-id="950e2-731">Then, add this Windows registry entries on both Windows cluster nodes for SAP ASCS/SCS:</span></span>

| <span data-ttu-id="950e2-732">Yol</span><span class="sxs-lookup"><span data-stu-id="950e2-732">Path</span></span> | <span data-ttu-id="950e2-733">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span><span class="sxs-lookup"><span data-stu-id="950e2-733">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span></span> |
| --- | --- |
| <span data-ttu-id="950e2-734">Değişken adı</span><span class="sxs-lookup"><span data-stu-id="950e2-734">Variable name</span></span> |`KeepAliveInterval` |
| <span data-ttu-id="950e2-735">Değişken türü</span><span class="sxs-lookup"><span data-stu-id="950e2-735">Variable type</span></span> |<span data-ttu-id="950e2-736">REG_DWORD (ondalık)</span><span class="sxs-lookup"><span data-stu-id="950e2-736">REG_DWORD (Decimal)</span></span> |
| <span data-ttu-id="950e2-737">Değer</span><span class="sxs-lookup"><span data-stu-id="950e2-737">Value</span></span> |<span data-ttu-id="950e2-738">120000</span><span class="sxs-lookup"><span data-stu-id="950e2-738">120000</span></span> |
| <span data-ttu-id="950e2-739">Belgelere bağlantı</span><span class="sxs-lookup"><span data-stu-id="950e2-739">Link to documentation</span></span> |[<span data-ttu-id="950e2-740">https://technet.microsoft.com/en-us/library/cc957548.aspx</span><span class="sxs-lookup"><span data-stu-id="950e2-740">https://technet.microsoft.com/en-us/library/cc957548.aspx</span></span>](https://technet.microsoft.com/en-us/library/cc957548.aspx) |

<span data-ttu-id="950e2-741">_**Tablo 4:** ikinci TCP/IP'yi parametre değiştirme_</span><span class="sxs-lookup"><span data-stu-id="950e2-741">_**Table 4:** Change the second TCP/IP parameter_</span></span>

<span data-ttu-id="950e2-742">**Değişiklikleri uygulamak için her iki küme düğümlerini yeniden**.</span><span class="sxs-lookup"><span data-stu-id="950e2-742">**To apply the changes, restart both cluster nodes**.</span></span>

### <span data-ttu-id="950e2-743"><a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a>Bir Windows Server Yük Devretme Kümelemesi küme SAP ASCS/SCS örneği için ayarlama</span><span class="sxs-lookup"><span data-stu-id="950e2-743"><a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a> Set up a Windows Server Failover Clustering cluster for an SAP ASCS/SCS instance</span></span>

<span data-ttu-id="950e2-744">Bir Windows Server Yük Devretme Kümelemesi küme SAP ASCS/SCS örneği için ayarlama, bu görevleri içerir:</span><span class="sxs-lookup"><span data-stu-id="950e2-744">Setting up a Windows Server Failover Clustering cluster for an SAP ASCS/SCS instance involves these tasks:</span></span>

- <span data-ttu-id="950e2-745">Bir küme yapılandırmasında küme düğümleri toplama</span><span class="sxs-lookup"><span data-stu-id="950e2-745">Collecting the cluster nodes in a cluster configuration</span></span>
- <span data-ttu-id="950e2-746">Bir küme dosya paylaşımı tanığı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="950e2-746">Configuring a cluster file share witness</span></span>

#### <span data-ttu-id="950e2-747"><a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a>Bir küme yapılandırmasında küme düğümleri Topla</span><span class="sxs-lookup"><span data-stu-id="950e2-747"><a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a> Collect the cluster nodes in a cluster configuration</span></span>

1.  <span data-ttu-id="950e2-748">Rol Ekle ve Özellik Ekleme Sihirbazı, her iki küme düğümü yük devretme ekleyin.</span><span class="sxs-lookup"><span data-stu-id="950e2-748">In the Add Role and Features Wizard, add failover clustering to both cluster nodes.</span></span>
2.  <span data-ttu-id="950e2-749">Yük devretme kümesini yedeklerken, yük devretme kümesi Yöneticisi'ni kullanarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="950e2-749">Set up the failover cluster by using Failover Cluster Manager.</span></span> <span data-ttu-id="950e2-750">Yük Devretme Kümesi Yöneticisi'nde seçin **küme oluşturma**ve ardından yalnızca ilk küme düğüm A. adı ekleyin İkinci düğümü henüz eklemeyin; İkinci düğümü bir sonraki adımda ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="950e2-750">In Failover Cluster Manager, select **Create Cluster**, and then add only the name of the first cluster, node A. Do not add the second node yet; you'll add the second node in a later step.</span></span>

  ![Şekil 18: ilk küme düğümüne sunucu veya sanal makine adını ekleyin][sap-ha-guide-figure-3007]

  <span data-ttu-id="950e2-752">_**Şekil 18:** ilk küme düğümüne sunucu veya sanal makine adını ekleyin_</span><span class="sxs-lookup"><span data-stu-id="950e2-752">_**Figure 18:** Add the server or virtual machine name of the first cluster node_</span></span>

3.  <span data-ttu-id="950e2-753">Küme ağ adı (sanal ana bilgisayar adı) girin.</span><span class="sxs-lookup"><span data-stu-id="950e2-753">Enter the network name (virtual host name) of the cluster.</span></span>

  ![Şekil 19: küme adını girin][sap-ha-guide-figure-3008]

  <span data-ttu-id="950e2-755">_**Şekil 19:** küme adını girin_</span><span class="sxs-lookup"><span data-stu-id="950e2-755">_**Figure 19:** Enter the cluster name_</span></span>

4.  <span data-ttu-id="950e2-756">Kümeyi oluşturduktan sonra bir küme doğrulama testi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="950e2-756">After you've created the cluster, run a cluster validation test.</span></span>

  ![Şekil 20: küme doğrulama denetimini Çalıştır][sap-ha-guide-figure-3009]

  <span data-ttu-id="950e2-758">_**Şekil 20:** küme doğrulama denetimini Çalıştır_</span><span class="sxs-lookup"><span data-stu-id="950e2-758">_**Figure 20:** Run the cluster validation check_</span></span>

  <span data-ttu-id="950e2-759">Bu noktada işleminde disklerle ilgili tüm uyarılar yoksayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="950e2-759">You can ignore any warnings about disks at this point in the process.</span></span> <span data-ttu-id="950e2-760">Dosya paylaşım tanığı ve SIOS diskler daha sonra paylaşılan ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="950e2-760">You'll add a file share witness and the SIOS shared disks later.</span></span> <span data-ttu-id="950e2-761">Bu aşamada, bir çekirdek sahibi olma hakkında endişelenmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="950e2-761">At this stage, you don't need to worry about having a quorum.</span></span>

  ![Şekil 21: Çekirdek disk bulunamadı][sap-ha-guide-figure-3010]

  <span data-ttu-id="950e2-763">_**Şekil 21:** çekirdek disk bulunamadı_</span><span class="sxs-lookup"><span data-stu-id="950e2-763">_**Figure 21:** No quorum disk is found_</span></span>

  ![Şekil 22: Çekirdek küme kaynağının yeni bir IP adresi gerekiyor.][sap-ha-guide-figure-3011]

  <span data-ttu-id="950e2-765">_**Şekil 22:** çekirdek küme kaynağının yeni bir IP adresi gerekiyor_</span><span class="sxs-lookup"><span data-stu-id="950e2-765">_**Figure 22:** Core cluster resource needs a new IP address_</span></span>

5.  <span data-ttu-id="950e2-766">Çekirdeği Küme hizmetinin IP adresini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="950e2-766">Change the IP address of the core cluster service.</span></span> <span data-ttu-id="950e2-767">Çekirdeği Küme hizmeti, IP adresini değiştirme kadar sanal makine düğümlerinden biri için sunucunun IP adresini işaret ettiğinden küme başlatılamaz.</span><span class="sxs-lookup"><span data-stu-id="950e2-767">The cluster can't start until you change the IP address of the core cluster service, because the IP address of the server points to one of the virtual machine nodes.</span></span> <span data-ttu-id="950e2-768">Bunu yapmak **özellikleri** çekirdek Küme hizmeti IP kaynak sayfası.</span><span class="sxs-lookup"><span data-stu-id="950e2-768">Do this on the **Properties** page of the core cluster service's IP resource.</span></span>

  <span data-ttu-id="950e2-769">Örneğin, bir IP adresi atamak ihtiyacımız (örneğimizde **10.0.0.42**) küme sanal ana bilgisayar adı için **pr1 ascs VIR**.</span><span class="sxs-lookup"><span data-stu-id="950e2-769">For example, we need to assign an IP address (in our example, **10.0.0.42**) for the cluster virtual host name **pr1-ascs-vir**.</span></span>

  ![Şekil 23: Özellikler iletişim kutusunda, IP adresini değiştirme][sap-ha-guide-figure-3012]

  <span data-ttu-id="950e2-771">_**Şekil 23:** içinde **özellikleri** iletişim kutusunda, IP adresini değiştirme_</span><span class="sxs-lookup"><span data-stu-id="950e2-771">_**Figure 23:** In the **Properties** dialog box, change the IP address_</span></span>

  ![Şekil 24: küme için ayrılmış bir IP adresi atayın][sap-ha-guide-figure-3013]

  <span data-ttu-id="950e2-773">_**Şekil 24:** küme için ayrılmış bir IP adresi atayın_</span><span class="sxs-lookup"><span data-stu-id="950e2-773">_**Figure 24:** Assign the IP address that is reserved for the cluster_</span></span>

6.  <span data-ttu-id="950e2-774">Küme sanal ana bilgisayar adı çevrimiçi duruma getirin.</span><span class="sxs-lookup"><span data-stu-id="950e2-774">Bring the cluster virtual host name online.</span></span>

  ![Şekil 25: Küme çekirdek hizmeti çalışır durumda ve çalıştığından ve doğru IP adresi][sap-ha-guide-figure-3014]

  <span data-ttu-id="950e2-776">_**Şekil 25:** küme çekirdek hizmeti çalışır durumda ve çalıştığından ve doğru IP adresi_</span><span class="sxs-lookup"><span data-stu-id="950e2-776">_**Figure 25:** Cluster core service is up and running, and with the correct IP address_</span></span>

7.  <span data-ttu-id="950e2-777">İkinci küme düğümünü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="950e2-777">Add the second cluster node.</span></span>

  <span data-ttu-id="950e2-778">Çekirdeği Küme hizmeti çalışır durumda olduğundan, ikinci küme düğümü ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="950e2-778">Now that the core cluster service is up and running, you can add the second cluster node.</span></span>

  ![Şekil 26: ikinci küme düğümü ekleyin.][sap-ha-guide-figure-3015]

  <span data-ttu-id="950e2-780">_**Şekil 26:** ikinci küme düğümü ekleyin._</span><span class="sxs-lookup"><span data-stu-id="950e2-780">_**Figure 26:** Add the second cluster node_</span></span>

8.  <span data-ttu-id="950e2-781">İkinci küme düğümü ana bilgisayar için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="950e2-781">Enter a name for the second cluster node host.</span></span>

  ![Şekil 27: ikinci küme düğümü ana bilgisayar adı girin][sap-ha-guide-figure-3016]

  <span data-ttu-id="950e2-783">_**Şekil 27:** ikinci küme düğümü ana bilgisayar adını girin_</span><span class="sxs-lookup"><span data-stu-id="950e2-783">_**Figure 27:** Enter the second cluster node host name_</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="950e2-784">Olduğundan emin olun **tüm uygun depolamayı kümeye eklemek** onay kutusu **değil** seçili.</span><span class="sxs-lookup"><span data-stu-id="950e2-784">Be sure that the **Add all eligible storage to the cluster** check box is **NOT** selected.</span></span>  
  >
  >

  ![Şekil 28: onay kutusunu seçin][sap-ha-guide-figure-3017]

  <span data-ttu-id="950e2-786">_**Şekil 28:** yapmak **değil** onay kutusunu seçin_</span><span class="sxs-lookup"><span data-stu-id="950e2-786">_**Figure 28:** Do **not** select the check box_</span></span>

  <span data-ttu-id="950e2-787">Çekirdek ve diskleri ilgili uyarılar yoksayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="950e2-787">You can ignore warnings about quorum and disks.</span></span> <span data-ttu-id="950e2-788">Çekirdek ayarlayın ve diski daha sonra açıklandığı şekilde paylaşma [SIOS DataKeeper Cluster Edition yükleme SAP ASCS/SCS küme paylaşım diski için][sap-ha-guide-8.12.3].</span><span class="sxs-lookup"><span data-stu-id="950e2-788">You'll set the quorum and share the disk later, as described in [Installing SIOS DataKeeper Cluster Edition for SAP ASCS/SCS cluster share disk][sap-ha-guide-8.12.3].</span></span>

  ![Şekil 29: disk çekirdek ilgili uyarılar yoksay][sap-ha-guide-figure-3018]

  <span data-ttu-id="950e2-790">_**Şekil 29:** disk çekirdek ilgili uyarılar yoksay_</span><span class="sxs-lookup"><span data-stu-id="950e2-790">_**Figure 29:** Ignore warnings about the disk quorum_</span></span>


#### <span data-ttu-id="950e2-791"><a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a>Bir küme dosya paylaşımı tanığı Yapılandır</span><span class="sxs-lookup"><span data-stu-id="950e2-791"><a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a> Configure a cluster file share witness</span></span>

<span data-ttu-id="950e2-792">Bir küme dosya paylaşımı tanığı yapılandırma, bu görevleri içerir:</span><span class="sxs-lookup"><span data-stu-id="950e2-792">Configuring a cluster file share witness involves these tasks:</span></span>

- <span data-ttu-id="950e2-793">Bir dosya paylaşımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="950e2-793">Creating a file share</span></span>
- <span data-ttu-id="950e2-794">Yük Devretme Kümesi Yöneticisi'nde dosya paylaşım tanığı çekirdek ayarlama</span><span class="sxs-lookup"><span data-stu-id="950e2-794">Setting the file share witness quorum in Failover Cluster Manager</span></span>

##### <span data-ttu-id="950e2-795"><a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a>Dosya paylaşımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="950e2-795"><a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a> Create a file share</span></span>

1.  <span data-ttu-id="950e2-796">Dosya paylaşım tanığı yerine bir çekirdek diski seçin.</span><span class="sxs-lookup"><span data-stu-id="950e2-796">Select a file share witness instead of a quorum disk.</span></span> <span data-ttu-id="950e2-797">Bu seçenek SIOS DataKeeper destekler.</span><span class="sxs-lookup"><span data-stu-id="950e2-797">SIOS DataKeeper supports this option.</span></span>

  <span data-ttu-id="950e2-798">Bu makaledeki örneklerde, Azure'da çalışan Active Directory/DNS sunucusunun dosya paylaşımı tanığı açıktır.</span><span class="sxs-lookup"><span data-stu-id="950e2-798">In the examples in this article, the file share witness is on the Active Directory/DNS server that is running in Azure.</span></span> <span data-ttu-id="950e2-799">Dosya paylaşım tanığı olarak adlandırılır **domcontr 0**.</span><span class="sxs-lookup"><span data-stu-id="950e2-799">The file share witness is called **domcontr-0**.</span></span> <span data-ttu-id="950e2-800">Azure (aracılığıyla, siteden siteye VPN veya Azure ExpressRoute) bir VPN bağlantısı yapılandırılmış için Active Directory/Hizmeti şirket içi ve bir dosyasını çalıştırmak uygun değil. DNS sunucunuzun Tanık paylaşır.</span><span class="sxs-lookup"><span data-stu-id="950e2-800">Because you would have configured a VPN connection to Azure (via Site-to-Site VPN or Azure ExpressRoute), your Active Directory/DNS service is on-premises and isn't suitable to run a file share witness.</span></span>

  > [!NOTE]
  > <span data-ttu-id="950e2-801">Yalnızca şirket içi Active Directory DNS hizmeti çalışıyorsa, dosya paylaşım tanığı Active Directory/DNS Windows işletim sisteminde şirket içi çalışan yapılandırmayın.</span><span class="sxs-lookup"><span data-stu-id="950e2-801">If your Active Directory/DNS service runs only on-premises, don't configure your file share witness on the Active Directory/DNS Windows operating system that is running on-premises.</span></span> <span data-ttu-id="950e2-802">Azure ve Active Directory DNS şirket içi çalışan küme düğümleri arasındaki ağ gecikmesi çok büyük ve bağlantı sorunlarına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="950e2-802">Network latency between cluster nodes running in Azure and Active Directory/DNS on-premises might be too large and cause connectivity issues.</span></span> <span data-ttu-id="950e2-803">Dosya paylaşım tanığı, küme düğümü yakın çalıştıran Azure sanal makinede yapılandırdığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="950e2-803">Be sure to configure the file share witness on an Azure virtual machine that is running close to the cluster node.</span></span>  
  >
  >

  <span data-ttu-id="950e2-804">Çekirdek sürücüde en az 1024 MB boş disk alanı gerekir.</span><span class="sxs-lookup"><span data-stu-id="950e2-804">The quorum drive needs at least 1,024 MB of free space.</span></span> <span data-ttu-id="950e2-805">2.048 MB boş disk alanı çekirdek sürücüsü için öneririz.</span><span class="sxs-lookup"><span data-stu-id="950e2-805">We recommend 2,048 MB of free space for the quorum drive.</span></span>

2.  <span data-ttu-id="950e2-806">Küme adı nesnesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="950e2-806">Add the cluster name object.</span></span>

  ![Şekil 30: küme adı nesnesi paylaşımı üzerindeki izinleri atama][sap-ha-guide-figure-3019]

  <span data-ttu-id="950e2-808">_**Şekil 30:** küme adı nesnesi paylaşımı üzerindeki izinleri atama_</span><span class="sxs-lookup"><span data-stu-id="950e2-808">_**Figure 30:** Assign the permissions on the share for the cluster name object_</span></span>

  <span data-ttu-id="950e2-809">İzinleri küme adı nesnesi için paylaşım uygulamasında verileri değiştirme yetkisi içeren emin olun (örneğimizde **pr1 ascs VIR$**).</span><span class="sxs-lookup"><span data-stu-id="950e2-809">Be sure that the permissions include the authority to change data in the share for the cluster name object (in our example, **pr1-ascs-vir$**).</span></span>

3.  <span data-ttu-id="950e2-810">Küme adı nesnesi listesine eklemek için seçin **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="950e2-810">To add the cluster name object to the list, select **Add**.</span></span> <span data-ttu-id="950e2-811">Şekil 31'de gösterilen ek olarak bilgisayar nesneleri denetlemek için filtreyi değiştirin.</span><span class="sxs-lookup"><span data-stu-id="950e2-811">Change the filter to check for computer objects, in addition to those shown in Figure 31.</span></span>

  ![Şekil 31: Değişiklik bilgisayarları dahil etme nesne türleri][sap-ha-guide-figure-3020]

  <span data-ttu-id="950e2-813">_**Şekil 31:** bilgisayarları dahil etme nesne türlerini değiştirme_</span><span class="sxs-lookup"><span data-stu-id="950e2-813">_**Figure 31:** Change the Object Types to include computers_</span></span>

  ![Şekil 32: bilgisayarlar onay kutusunu seçin][sap-ha-guide-figure-3021]

  <span data-ttu-id="950e2-815">_**Şekil 32:** seçin **bilgisayarlar** onay kutusu_</span><span class="sxs-lookup"><span data-stu-id="950e2-815">_**Figure 32:** Select the **Computers** check box_</span></span>

4.  <span data-ttu-id="950e2-816">Küme adı nesnesi şekil 31'de gösterildiği gibi girin.</span><span class="sxs-lookup"><span data-stu-id="950e2-816">Enter the cluster name object as shown in Figure 31.</span></span> <span data-ttu-id="950e2-817">Kaydı zaten oluşturulduğundan, Şekil 30 gösterildiği gibi izinlerini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="950e2-817">Because the record has already been created, you can change the permissions, as shown in Figure 30.</span></span>

5.  <span data-ttu-id="950e2-818">Seçin **güvenlik** paylaşım ayarlayın ve ardından sekmesinde daha ayrıntılı küme adı nesnesi için izinleri.</span><span class="sxs-lookup"><span data-stu-id="950e2-818">Select the **Security** tab of the share, and then set more detailed permissions for the cluster name object.</span></span>

  ![Şekil 33: dosya paylaşımı çekirdeği küme adı nesnesi için güvenlik özniteliklerini ayarlama][sap-ha-guide-figure-3022]

  <span data-ttu-id="950e2-820">_**Şekil 33:** dosya paylaşımı çekirdeği küme adı nesnesi için güvenlik özniteliklerini ayarla_</span><span class="sxs-lookup"><span data-stu-id="950e2-820">_**Figure 33:** Set the security attributes for the cluster name object on the file share quorum_</span></span>

##### <span data-ttu-id="950e2-821"><a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a>Yük Devretme Kümesi Yöneticisi'nde dosya paylaşım tanığı çekirdek ayarlayın</span><span class="sxs-lookup"><span data-stu-id="950e2-821"><a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a> Set the file share witness quorum in Failover Cluster Manager</span></span>

1.  <span data-ttu-id="950e2-822">Açık çekirdek Ayarlama Sihirbazı'nı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="950e2-822">Open the Configure Quorum Setting Wizard.</span></span>

  ![Şekil 34: yapılandırma küme çekirdeği Ayarlama Sihirbazı'nı Başlat][sap-ha-guide-figure-3023]

  <span data-ttu-id="950e2-824">_**Şekil 34:** yapılandırma küme çekirdeği Ayarlama Sihirbazı'nı Başlat_</span><span class="sxs-lookup"><span data-stu-id="950e2-824">_**Figure 34:** Start the Configure Cluster Quorum Setting Wizard_</span></span>

2.  <span data-ttu-id="950e2-825">Üzerinde **seçin Çekirdek yapılandırmasını** sayfasında **çekirdek tanığı Seç**.</span><span class="sxs-lookup"><span data-stu-id="950e2-825">On the **Select Quorum Configuration** page, select **Select the quorum witness**.</span></span>

  ![Şekil 35: aralarından seçim yapabileceğiniz Çekirdek yapılandırmaları][sap-ha-guide-figure-3024]

  <span data-ttu-id="950e2-827">_**Şekil 35:** seçim yapabileceğiniz Çekirdek yapılandırmaları_</span><span class="sxs-lookup"><span data-stu-id="950e2-827">_**Figure 35:** Quorum configurations you can choose from_</span></span>

3.  <span data-ttu-id="950e2-828">Üzerinde **çekirdek tanığı Seç** sayfasında **bir dosya paylaşımı tanığı Yapılandır**.</span><span class="sxs-lookup"><span data-stu-id="950e2-828">On the **Select Quorum Witness** page, select **Configure a file share witness**.</span></span>

  ![Şekil 36: dosya paylaşım tanığı seçin][sap-ha-guide-figure-3025]

  <span data-ttu-id="950e2-830">_**Şekil 36:** dosya paylaşım tanığı seçin_</span><span class="sxs-lookup"><span data-stu-id="950e2-830">_**Figure 36:** Select the file share witness_</span></span>

4.  <span data-ttu-id="950e2-831">Dosya Paylaşımı için UNC yolunu girin (örneğimizde \\domcontr 0\FSW).</span><span class="sxs-lookup"><span data-stu-id="950e2-831">Enter the UNC path to the file share (in our example, \\domcontr-0\FSW).</span></span> <span data-ttu-id="950e2-832">Yapabilirsiniz yapılan değişikliklerin bir listesi görmek için seçin **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="950e2-832">To see a list of the changes you can make, select **Next**.</span></span>

  ![Şekil 37: Tanık paylaşımı için dosya paylaşım konumunu tanımlayın][sap-ha-guide-figure-3026]

  <span data-ttu-id="950e2-834">_**Şekil 37:** Tanık paylaşımı için dosya paylaşım konumunu tanımlayın_</span><span class="sxs-lookup"><span data-stu-id="950e2-834">_**Figure 37:** Define the file share location for the witness share_</span></span>

5.  <span data-ttu-id="950e2-835">Seçin ve ardından değişiklikleri **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="950e2-835">Select the changes you want, and then select **Next**.</span></span> <span data-ttu-id="950e2-836">Küme yapılandırmasını şekil 38 gösterildiği gibi başarılı bir şekilde yeniden yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="950e2-836">You need to successfully reconfigure the cluster configuration as shown in Figure 38.</span></span>  

  ![Şekil 38: küme yeniden yapılandırılması onayı][sap-ha-guide-figure-3027]

  <span data-ttu-id="950e2-838">_**Şekil 38:** kümeye yeniden yapılandırılması onayı_</span><span class="sxs-lookup"><span data-stu-id="950e2-838">_**Figure 38:** Confirmation that you've reconfigured the cluster_</span></span>

<span data-ttu-id="950e2-839">Windows Yük devretme kümesi başarıyla yükledikten sonra değişiklikler bazı eşikleri Azure koşullar için yük devretme algılama uyarlamak için yapılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="950e2-839">After installing the Windows Failover Cluster successfully, changes need to be made to some thresholds to adapt failover detection to conditions in Azure.</span></span> <span data-ttu-id="950e2-840">Değiştirilecek parametreleri bu blog belgelenmiştir: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/.</span><span class="sxs-lookup"><span data-stu-id="950e2-840">The parameters to be changed are documented in this blog: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/ .</span></span> <span data-ttu-id="950e2-841">Windows Küme yapılandırması ASCS/SCS için derleme, iki VM aynı alt ağda olduğu varsayımıyla, aşağıdaki parametreleri bu değerleri değiştirilmesi gerekebilir:</span><span class="sxs-lookup"><span data-stu-id="950e2-841">Assuming that your two VMs that build the Windows Cluster Configuration for ASCS/SCS are in the same SubNet, the following parameters need to be changed to these values:</span></span>
- <span data-ttu-id="950e2-842">SameSubNetDelay = 2</span><span class="sxs-lookup"><span data-stu-id="950e2-842">SameSubNetDelay = 2</span></span>
- <span data-ttu-id="950e2-843">SameSubNetThreshold = 15</span><span class="sxs-lookup"><span data-stu-id="950e2-843">SameSubNetThreshold = 15</span></span>

<span data-ttu-id="950e2-844">Bu ayarları müşterilerle test ve bir tarafta yeterince dayanıklı olması için iyi bir güvenlik açığı sağlanan.</span><span class="sxs-lookup"><span data-stu-id="950e2-844">These settings were tested with customers and provided a good compromise to be resilient enough on the one side.</span></span> <span data-ttu-id="950e2-845">Öte yandan bu ayarları gerçek hata koşulları yeterli yük SAP yazılım veya düğüm/VM hatada sağlama hızlı.</span><span class="sxs-lookup"><span data-stu-id="950e2-845">On the other hand those settings were providing fast enough failover in real error conditions on SAP software or node/VM failure.</span></span> 

### <span data-ttu-id="950e2-846"><a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a>SAP ASCS/SCS küme paylaşım diski için SIOS DataKeeper küme Edition'ı yükleme</span><span class="sxs-lookup"><span data-stu-id="950e2-846"><a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a> Install SIOS DataKeeper Cluster Edition for the SAP ASCS/SCS cluster share disk</span></span>

<span data-ttu-id="950e2-847">Artık Azure üzerinde çalışan bir Windows Server Yük Devretme Kümelemesi yapılandırma vardır.</span><span class="sxs-lookup"><span data-stu-id="950e2-847">You now have a working Windows Server Failover Clustering configuration in Azure.</span></span> <span data-ttu-id="950e2-848">Ancak, SAP ASCS/SCS örneği yüklemek için paylaşılan disk kaynağı gerekir.</span><span class="sxs-lookup"><span data-stu-id="950e2-848">But, to install an SAP ASCS/SCS instance, you need a shared disk resource.</span></span> <span data-ttu-id="950e2-849">İhtiyacınız olan paylaşılan disk kaynakları Azure'da oluşturulamıyor.</span><span class="sxs-lookup"><span data-stu-id="950e2-849">You cannot create the shared disk resources you need in Azure.</span></span> <span data-ttu-id="950e2-850">Paylaşılan disk kaynakları oluşturmak için kullanabileceğiniz bir üçüncü taraf çözümü SIOS DataKeeper küme sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="950e2-850">SIOS DataKeeper Cluster Edition is a third-party solution you can use to create shared disk resources.</span></span>

<span data-ttu-id="950e2-851">SAP ASCS/SCS küme paylaşım diski için SIOS DataKeeper Cluster Edition yüklemek, bu görevleri içerir:</span><span class="sxs-lookup"><span data-stu-id="950e2-851">Installing SIOS DataKeeper Cluster Edition for the SAP ASCS/SCS cluster share disk involves these tasks:</span></span>

- <span data-ttu-id="950e2-852">.NET Framework 3.5 ekleme</span><span class="sxs-lookup"><span data-stu-id="950e2-852">Adding the .NET Framework 3.5</span></span>
- <span data-ttu-id="950e2-853">SIOS DataKeeper yükleme</span><span class="sxs-lookup"><span data-stu-id="950e2-853">Installing SIOS DataKeeper</span></span>
- <span data-ttu-id="950e2-854">SIOS DataKeeper ayarlama</span><span class="sxs-lookup"><span data-stu-id="950e2-854">Setting up SIOS DataKeeper</span></span>

#### <span data-ttu-id="950e2-855"><a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a>.NET Framework 3.5 ekleme</span><span class="sxs-lookup"><span data-stu-id="950e2-855"><a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a> Add the .NET Framework 3.5</span></span>
<span data-ttu-id="950e2-856">Microsoft .NET Framework 3.5 otomatik olarak etkinleştirilmiş veya Windows Server 2012 R2'de yüklü değil.</span><span class="sxs-lookup"><span data-stu-id="950e2-856">The Microsoft .NET Framework 3.5 isn't automatically activated or installed on Windows Server 2012 R2.</span></span> <span data-ttu-id="950e2-857">SIOS DataKeeper DataKeeper yüklemek, tüm düğümlerde olması için .NET Framework'ü gerektirdiğinden, .NET Framework 3.5, kümedeki tüm sanal makineler konuk işletim sisteminde yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="950e2-857">Because SIOS DataKeeper requires the .NET Framework to be on all nodes that you install DataKeeper on, you must install the .NET Framework 3.5 on the guest operating system of all virtual machines in the cluster.</span></span>

<span data-ttu-id="950e2-858">.NET Framework 3.5 eklemek için iki yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="950e2-858">There are two ways to add the .NET Framework 3.5:</span></span>

- <span data-ttu-id="950e2-859">Ekle roller ve Özellikler Sihirbazı'nı Windows şekil 39 gösterildiği gibi kullanın.</span><span class="sxs-lookup"><span data-stu-id="950e2-859">Use the Add Roles and Features Wizard in Windows as shown in Figure 39.</span></span>

  ![Şekil 39: Ekle roller ve Özellikler Sihirbazı'nı kullanarak .NET Framework 3.5 yükleyin.][sap-ha-guide-figure-3028]

  <span data-ttu-id="950e2-861">_**Şekil 39:** Ekle roller ve Özellikler Sihirbazı'nı kullanarak .NET Framework 3.5 yükleyin_</span><span class="sxs-lookup"><span data-stu-id="950e2-861">_**Figure 39:** Install the .NET Framework 3.5 by using the Add Roles and Features Wizard_</span></span>

  ![Şekil 40: yükleme ilerleme çubuğu Ekle roller ve Özellikler Sihirbazı'nı kullanarak .NET Framework 3.5 yüklediğinizde][sap-ha-guide-figure-3029]

  <span data-ttu-id="950e2-863">_**Şekil 40:** Ekle roller ve Özellikler Sihirbazı'nı kullanarak .NET Framework 3.5 yüklediğinizde çubuğu yükleme ilerleme durumu_</span><span class="sxs-lookup"><span data-stu-id="950e2-863">_**Figure 40:** Installation progress bar when you install the .NET Framework 3.5 by using the Add Roles and Features Wizard_</span></span>

- <span data-ttu-id="950e2-864">Komut satırı aracı dism.exe kullanın.</span><span class="sxs-lookup"><span data-stu-id="950e2-864">Use the command-line tool dism.exe.</span></span> <span data-ttu-id="950e2-865">Bu yükleme türü için Windows yükleme medyasında bulunan SxS dizin erişmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="950e2-865">For this type of installation, you need to access the SxS directory on the Windows installation media.</span></span> <span data-ttu-id="950e2-866">Yükseltilmiş bir komut istemine yazın:</span><span class="sxs-lookup"><span data-stu-id="950e2-866">At an elevated command prompt, type:</span></span>

  ```
  Dism /online /enable-feature /featurename:NetFx3 /All /Source:installation_media_drive:\sources\sxs /LimitAccess
  ```

#### <span data-ttu-id="950e2-867"><a name="dd41d5a2-8083-415b-9878-839652812102"></a>SIOS DataKeeper yükleyin</span><span class="sxs-lookup"><span data-stu-id="950e2-867"><a name="dd41d5a2-8083-415b-9878-839652812102"></a> Install SIOS DataKeeper</span></span>

<span data-ttu-id="950e2-868">Kümedeki her düğümde SIOS DataKeeper Cluster Edition yükleyin.</span><span class="sxs-lookup"><span data-stu-id="950e2-868">Install SIOS DataKeeper Cluster Edition on each node in the cluster.</span></span> <span data-ttu-id="950e2-869">SIOS DataKeeper ile sanal paylaşılan depolama alanı oluşturmak için eşitlenen bir yansıtma oluşturmak ve Küme Paylaşılan depolama benzetimini yapma.</span><span class="sxs-lookup"><span data-stu-id="950e2-869">To create virtual shared storage with SIOS DataKeeper, create a synced mirror and then simulate cluster shared storage.</span></span>

<span data-ttu-id="950e2-870">SIOS yazılım yüklemeden önce etki alanı kullanıcısı oluşturun **DataKeeperSvc**.</span><span class="sxs-lookup"><span data-stu-id="950e2-870">Before you install the SIOS software, create the domain user **DataKeeperSvc**.</span></span>

> [!NOTE]
> <span data-ttu-id="950e2-871">Ekleme **DataKeeperSvc** kullanıcıya **yerel yönetici** her iki küme düğümlerinde grup.</span><span class="sxs-lookup"><span data-stu-id="950e2-871">Add the **DataKeeperSvc** user to the **Local Administrator** group on both cluster nodes.</span></span>
>
>

<span data-ttu-id="950e2-872">SIOS DataKeeper yüklemek için:</span><span class="sxs-lookup"><span data-stu-id="950e2-872">To install SIOS DataKeeper:</span></span>

1.  <span data-ttu-id="950e2-873">SIOS yazılım her iki küme düğümlerine yükleyin.</span><span class="sxs-lookup"><span data-stu-id="950e2-873">Install the SIOS software on both cluster nodes.</span></span>

  ![SIOS yükleyici][sap-ha-guide-figure-3030]

  ![Şekil 41: İlk sayfa SIOS DataKeeper yükleme][sap-ha-guide-figure-3031]

  <span data-ttu-id="950e2-876">_**Şekil 41:** SIOS DataKeeper yüklemesinin ilk sayfa_</span><span class="sxs-lookup"><span data-stu-id="950e2-876">_**Figure 41:** First page of the SIOS DataKeeper installation_</span></span>

2.  <span data-ttu-id="950e2-877">Şekil 42 gösterilen iletişim kutusunda seçin **Evet**.</span><span class="sxs-lookup"><span data-stu-id="950e2-877">In the dialog box shown in Figure 42, select **Yes**.</span></span>

  ![Şekil 42: Bir hizmeti devre dışı bırakılacak DataKeeper size bildirir][sap-ha-guide-figure-3032]

  <span data-ttu-id="950e2-879">_**Şekil 42:** DataKeeper bildirir, bir hizmeti devre dışı bırakılacak_</span><span class="sxs-lookup"><span data-stu-id="950e2-879">_**Figure 42:** DataKeeper informs you that a service will be disabled_</span></span>

3.  <span data-ttu-id="950e2-880">Şekil 43 gösterilen iletişim kutusunda seçtiğiniz olan öneririz **etki alanı veya sunucu hesabı**.</span><span class="sxs-lookup"><span data-stu-id="950e2-880">In the dialog box shown in Figure 43, we recommend that you select **Domain or Server account**.</span></span>

  ![Şekil 43: Kullanıcı Seçimi SIOS DataKeeper için][sap-ha-guide-figure-3033]

  <span data-ttu-id="950e2-882">_**Şekil 43:** SIOS DataKeeper için kullanıcı seçimi_</span><span class="sxs-lookup"><span data-stu-id="950e2-882">_**Figure 43:** User selection for SIOS DataKeeper_</span></span>

4.  <span data-ttu-id="950e2-883">SIOS DataKeeper için oluşturduğunuz parola ve etki alanı hesabı kullanıcı adı girin.</span><span class="sxs-lookup"><span data-stu-id="950e2-883">Enter the domain account user name and passwords that you created for SIOS DataKeeper.</span></span>

  ![Şekil 44: SIOS DataKeeper yükleme için etki alanı kullanıcı adı ve parolayı girin][sap-ha-guide-figure-3034]

  <span data-ttu-id="950e2-885">_**Şekil 44:** SIOS DataKeeper yükleme için etki alanı kullanıcı adı ve parolayı girin_</span><span class="sxs-lookup"><span data-stu-id="950e2-885">_**Figure 44:** Enter the domain user name and password for the SIOS DataKeeper installation_</span></span>

5.  <span data-ttu-id="950e2-886">Lisans anahtarı SIOS DataKeeper Örneğiniz için şekil 45 gösterildiği gibi yükleyin.</span><span class="sxs-lookup"><span data-stu-id="950e2-886">Install the license key for your SIOS DataKeeper instance as shown in Figure 45.</span></span>

  ![Şekil 45: SIOS DataKeeper lisans anahtarınızı girin][sap-ha-guide-figure-3035]

  <span data-ttu-id="950e2-888">_**Şekil 45:** SIOS DataKeeper lisans anahtarınızı girin_</span><span class="sxs-lookup"><span data-stu-id="950e2-888">_**Figure 45:** Enter your SIOS DataKeeper license key_</span></span>

6.  <span data-ttu-id="950e2-889">İstendiğinde, sanal makineyi yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="950e2-889">When prompted, restart the virtual machine.</span></span>

#### <span data-ttu-id="950e2-890"><a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a>SIOS DataKeeper ayarlayın</span><span class="sxs-lookup"><span data-stu-id="950e2-890"><a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a> Set up SIOS DataKeeper</span></span>

<span data-ttu-id="950e2-891">Her iki düğümde SIOS DataKeeper yükledikten sonra yapılandırma başlatmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="950e2-891">After you install SIOS DataKeeper on both nodes, you need to start the configuration.</span></span> <span data-ttu-id="950e2-892">Yapılandırma amacı, her sanal makineye bağlı ek diskleri arasında zaman uyumlu veri çoğaltma sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="950e2-892">The goal of the configuration is to have synchronous data replication between the additional disks attached to each of the virtual machines.</span></span>

1.  <span data-ttu-id="950e2-893">DataKeeper yönetim ve Yapılandırma Aracı'nı başlatın ve ardından **Connect Server**.</span><span class="sxs-lookup"><span data-stu-id="950e2-893">Start the DataKeeper Management and Configuration tool, and then select **Connect Server**.</span></span> <span data-ttu-id="950e2-894">(Şekil 46 bu seçenek kırmızı daire içine alınmıştır.)</span><span class="sxs-lookup"><span data-stu-id="950e2-894">(In Figure 46, this option is circled in red.)</span></span>

  ![Şekil 46: SIOS DataKeeper yönetim ve yapılandırma aracı][sap-ha-guide-figure-3036]

  <span data-ttu-id="950e2-896">_**Şekil 46:** SIOS DataKeeper yönetim ve yapılandırma aracı_</span><span class="sxs-lookup"><span data-stu-id="950e2-896">_**Figure 46:** SIOS DataKeeper Management and Configuration tool_</span></span>

2.  <span data-ttu-id="950e2-897">Adını veya yönetim ve yapılandırma aracı için ve ikinci adım, ikinci düğümü bağlanmalısınız ilk düğümü TCP/IP'yi adresini girin.</span><span class="sxs-lookup"><span data-stu-id="950e2-897">Enter the name or TCP/IP address of the first node the Management and Configuration tool should connect to, and, in a second step, the second node.</span></span>

  ![Şekil 47: ad ekleyin veya TCP/IP adresi ilk düğümün yönetim ve yapılandırma aracı için ve ikinci adım, ikinci düğümü bağlanmanız gerekir][sap-ha-guide-figure-3037]

  <span data-ttu-id="950e2-899">_**Şekil 47:** adını veya yönetimi ve yapılandırması aracı bağlanmak için ve ikinci adım, ikinci düğümü ilk düğümde TCP/IP'yi adresini Ekle_</span><span class="sxs-lookup"><span data-stu-id="950e2-899">_**Figure 47:** Insert the name or TCP/IP address of the first node the Management and Configuration tool should connect to, and in a second step, the second node_</span></span>

3.  <span data-ttu-id="950e2-900">İki düğüm arasında çoğaltma işi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="950e2-900">Create the replication job between the two nodes.</span></span>

  ![Şekil 48: bir çoğaltma işi oluşturma][sap-ha-guide-figure-3038]

  <span data-ttu-id="950e2-902">_**Şekil 48:** çoğaltma işi oluşturma_</span><span class="sxs-lookup"><span data-stu-id="950e2-902">_**Figure 48:** Create a replication job_</span></span>

  <span data-ttu-id="950e2-903">Sihirbaz, bir çoğaltma işi oluşturma işleminde size rehberlik eder.</span><span class="sxs-lookup"><span data-stu-id="950e2-903">A wizard guides you through the process of creating a replication job.</span></span>
4.  <span data-ttu-id="950e2-904">Adı, TCP/IP adresi ve kaynak düğüm disk birimi tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="950e2-904">Define the name, TCP/IP address, and disk volume of the source node.</span></span>

  ![Şekil 49: çoğaltma işi adını tanımlayın][sap-ha-guide-figure-3039]

  <span data-ttu-id="950e2-906">_**Şekil 49:** çoğaltma işi adını tanımlayın_</span><span class="sxs-lookup"><span data-stu-id="950e2-906">_**Figure 49:** Define the name of the replication job_</span></span>

  ![Şekil 50: geçerli kaynak düğüm olmalıdır düğümü için temel veri tanımlama][sap-ha-guide-figure-3040]

  <span data-ttu-id="950e2-908">_**Şekil 50:** geçerli kaynak düğüm olmalıdır düğümü için temel veri tanımlama_</span><span class="sxs-lookup"><span data-stu-id="950e2-908">_**Figure 50:** Define the base data for the node, which should be the current source node_</span></span>

5.  <span data-ttu-id="950e2-909">Adı, TCP/IP adresi ve hedef düğüm disk birimi tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="950e2-909">Define the name, TCP/IP address, and disk volume of the target node.</span></span>

  ![Şekil 51: geçerli hedef düğümü olmalı düğümü için temel veri tanımlama][sap-ha-guide-figure-3041]

  <span data-ttu-id="950e2-911">_**Şekil 51:** geçerli hedef düğüm olmalıdır düğümü için temel veri tanımlama_</span><span class="sxs-lookup"><span data-stu-id="950e2-911">_**Figure 51:** Define the base data for the node, which should be the current target node_</span></span>

6.  <span data-ttu-id="950e2-912">Sıkıştırma algoritmaları tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="950e2-912">Define the compression algorithms.</span></span> <span data-ttu-id="950e2-913">Bizim örneğimizde, çoğaltma akışını sıkıştırmak öneririz.</span><span class="sxs-lookup"><span data-stu-id="950e2-913">In our example, we recommend that you compress the replication stream.</span></span> <span data-ttu-id="950e2-914">Özellikle yeniden eşitleme durumlarda çoğaltma akışı sıkıştırma yeniden eşitleme süresini önemli ölçüde azaltır.</span><span class="sxs-lookup"><span data-stu-id="950e2-914">Especially in resynchronization situations, the compression of the replication stream dramatically reduces resynchronization time.</span></span> <span data-ttu-id="950e2-915">Sıkıştırma, bir sanal makinenin CPU ve RAM kaynakları kullandığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="950e2-915">Note that compression uses the CPU and RAM resources of a virtual machine.</span></span> <span data-ttu-id="950e2-916">Sıkıştırma oranı arttıkça, birimin kullanılan CPU kaynaklarının da artar.</span><span class="sxs-lookup"><span data-stu-id="950e2-916">As the compression rate increases, so does the volume of CPU resources used.</span></span> <span data-ttu-id="950e2-917">Bu ayarı daha sonra da ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="950e2-917">You also can adjust this setting later.</span></span>

7.  <span data-ttu-id="950e2-918">Kontrol etmeniz başka bir ayar olup çoğaltma zaman uyumsuz veya zaman uyumlu olarak gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="950e2-918">Another setting you need to check is whether the replication occurs asynchronously or synchronously.</span></span> <span data-ttu-id="950e2-919">*SAP ASCS/SCS yapılandırmaları koruduğunuzda, zaman uyumlu çoğaltma kullanmalısınız*.</span><span class="sxs-lookup"><span data-stu-id="950e2-919">*When you protect SAP ASCS/SCS configurations, you must use synchronous replication*.</span></span>  

  ![Şekil 52: çoğaltma ayrıntılarını tanımlayın][sap-ha-guide-figure-3042]

  <span data-ttu-id="950e2-921">_**Şekil 52:** çoğaltma ayrıntılarını tanımlayın_</span><span class="sxs-lookup"><span data-stu-id="950e2-921">_**Figure 52:** Define replication details_</span></span>

8.  <span data-ttu-id="950e2-922">Çoğaltma işlemiyle çoğaltılır birimi paylaşılan bir disk olarak Windows Server Yük Devretme Kümelemesi küme yapılandırması için temsil olup olmadığını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="950e2-922">Define whether the volume that is replicated by the replication job should be represented to a Windows Server Failover Clustering cluster configuration as a shared disk.</span></span> <span data-ttu-id="950e2-923">SAP ASCS/SCS yapılandırmasını seçin **Evet** Windows Küme çoğaltılan birim küme birimi olarak kullanabileceği bir paylaşılan disk olarak görebilmesi için.</span><span class="sxs-lookup"><span data-stu-id="950e2-923">For the SAP ASCS/SCS configuration, select **Yes** so that the Windows cluster sees the replicated volume as a shared disk that it can use as a cluster volume.</span></span>

  ![Şekil 53: çoğaltılan birim küme birimi olarak ayarlamak için Evet'i seçin][sap-ha-guide-figure-3043]

  <span data-ttu-id="950e2-925">_**Şekil 53:** seçin **Evet** çoğaltılan birim küme birimi olarak ayarlamak için_</span><span class="sxs-lookup"><span data-stu-id="950e2-925">_**Figure 53:** Select **Yes** to set the replicated volume as a cluster volume_</span></span>

  <span data-ttu-id="950e2-926">Birim oluşturulduktan sonra DataKeeper yönetim ve yapılandırma aracı çoğaltma işi etkin olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="950e2-926">After the volume is created, the DataKeeper Management and Configuration tool shows that the replication job is active.</span></span>

  ![Şekil 54: DataKeeper SAP ASCS/SCS paylaşım disk için zaman uyumlu yansıtma etkindir][sap-ha-guide-figure-3044]

  <span data-ttu-id="950e2-928">_**Şekil 54:** disk SAP ASCS/SCS paylaşmak için DataKeeper zaman uyumlu yansıtma etkin olduğu_</span><span class="sxs-lookup"><span data-stu-id="950e2-928">_**Figure 54:** DataKeeper synchronous mirroring for the SAP ASCS/SCS share disk is active_</span></span>

  <span data-ttu-id="950e2-929">Yük Devretme Kümesi Yöneticisi şimdi şekil 55 gösterildiği gibi diski bir DataKeeper disk olarak gösterir.</span><span class="sxs-lookup"><span data-stu-id="950e2-929">Failover Cluster Manager now shows the disk as a DataKeeper disk, as shown in Figure 55.</span></span>

  ![Şekil 55: Yük devretme kümesi Yöneticisi'ni DataKeeper çoğaltılan disk gösterir.][sap-ha-guide-figure-3045]

  <span data-ttu-id="950e2-931">_**Şekil 55:** yük devretme kümesi Yöneticisi, çoğaltılan bu DataKeeper disk gösterir_</span><span class="sxs-lookup"><span data-stu-id="950e2-931">_**Figure 55:** Failover Cluster Manager shows the disk that DataKeeper replicated_</span></span>

## <span data-ttu-id="950e2-932"><a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a>SAP NetWeaver sistemini yükleyin</span><span class="sxs-lookup"><span data-stu-id="950e2-932"><a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a> Install the SAP NetWeaver system</span></span>

<span data-ttu-id="950e2-933">Kurulumları DBMS sistemine bağlı olarak farklılık gösterdiğinden biz DBMS kurulumunu açıklayan olmaz.</span><span class="sxs-lookup"><span data-stu-id="950e2-933">We won’t describe the DBMS setup because setups vary depending on the DBMS system you use.</span></span> <span data-ttu-id="950e2-934">Ancak, farklı DBMS satıcılar için Azure desteği işlevler ile DBMS ile yüksek kullanılabilirlik sorunlarının giderilmesini varsayalım.</span><span class="sxs-lookup"><span data-stu-id="950e2-934">However, we assume that high-availability concerns with the DBMS are addressed with the functionalities the different DBMS vendors support for Azure.</span></span> <span data-ttu-id="950e2-935">Örneğin, her zaman açık veya Oracle veritabanları için SQL Server ve Oracle Data Guard için veritabanı yansıtma.</span><span class="sxs-lookup"><span data-stu-id="950e2-935">For example, Always On or database mirroring for SQL Server, and Oracle Data Guard for Oracle databases.</span></span> <span data-ttu-id="950e2-936">Bu makalede kullanırız senaryosunda, size daha fazla koruma DBMS ekleyemiyor.</span><span class="sxs-lookup"><span data-stu-id="950e2-936">In the scenario we use in this article, we didn't add more protection to the DBMS.</span></span>

<span data-ttu-id="950e2-937">Bu tür bir Azure kümelenmiş SAP ASCS/SCS yapılandırmasında farklı DBMS Hizmetleri etkileşim, özel durumlar vardır.</span><span class="sxs-lookup"><span data-stu-id="950e2-937">There are no special considerations when different DBMS services interact with this kind of clustered SAP ASCS/SCS configuration in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="950e2-938">SAP NetWeaver ABAP sistemleri, Java sistemleri ve ABAP + Java sistemleri yükleme yordamları neredeyse aynıdır.</span><span class="sxs-lookup"><span data-stu-id="950e2-938">The installation procedures of SAP NetWeaver ABAP systems, Java systems, and ABAP+Java systems are almost identical.</span></span> <span data-ttu-id="950e2-939">En önemli fark, bir SAP ABAP sistemi bir ASCS örneği sahip olur.</span><span class="sxs-lookup"><span data-stu-id="950e2-939">The most significant difference is that an SAP ABAP system has one ASCS instance.</span></span> <span data-ttu-id="950e2-940">SAP Java sistem bir SCS örneği vardır.</span><span class="sxs-lookup"><span data-stu-id="950e2-940">The SAP Java system has one SCS instance.</span></span> <span data-ttu-id="950e2-941">SAP ABAP + Java sistem bir ASCS örneği ve aynı Microsoft yük devretme küme grubunda çalışan bir SCS örneğine sahip.</span><span class="sxs-lookup"><span data-stu-id="950e2-941">The SAP ABAP+Java system has one ASCS instance and one SCS instance running in the same Microsoft failover cluster group.</span></span> <span data-ttu-id="950e2-942">Her SAP NetWeaver yükleme yığınının yükleme farkları açıkça belirtilen.</span><span class="sxs-lookup"><span data-stu-id="950e2-942">Any installation differences for each SAP NetWeaver installation stack are explicitly mentioned.</span></span> <span data-ttu-id="950e2-943">Diğer tüm bölümleri aynı olduğunu kabul edilebilir.</span><span class="sxs-lookup"><span data-stu-id="950e2-943">You can assume that all other parts are the same.</span></span>  
>
>

### <span data-ttu-id="950e2-944"><a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a>Bir yüksek kullanılabilirlik ASCS/SCS örneğiyle SAP yükleyin</span><span class="sxs-lookup"><span data-stu-id="950e2-944"><a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a> Install SAP with a high-availability ASCS/SCS instance</span></span>

> [!IMPORTANT]
> <span data-ttu-id="950e2-945">Sayfa dosyanızı DataKeeper yansıtılmış birimler üzerinde değil yerleştirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="950e2-945">Be sure not to place your page file on DataKeeper mirrored volumes.</span></span> <span data-ttu-id="950e2-946">Yansıtılmış birimler DataKeeper desteklemez.</span><span class="sxs-lookup"><span data-stu-id="950e2-946">DataKeeper does not support mirrored volumes.</span></span> <span data-ttu-id="950e2-947">Varsayılan seçenek geçici D sürücüsündeki bir Azure sanal makine, sayfa dosyası bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="950e2-947">You can leave your page file on the temporary drive D of an Azure virtual machine, which is the default.</span></span> <span data-ttu-id="950e2-948">Bunu zaten yoksa, Windows disk belleği dosyası Azure sanal makinenizin D: sürücüye taşıyın.</span><span class="sxs-lookup"><span data-stu-id="950e2-948">If it's not already there, move the Windows page file to drive D: of your Azure virtual machine.</span></span>
>
>

<span data-ttu-id="950e2-949">Bir yüksek kullanılabilirlik ASCS/SCS örneğiyle SAP yüklemek, bu görevleri içerir:</span><span class="sxs-lookup"><span data-stu-id="950e2-949">Installing SAP with a high-availability ASCS/SCS instance involves these tasks:</span></span>

- <span data-ttu-id="950e2-950">Kümelenmiş SAP ASCS/SCS örneği için bir sanal ana bilgisayar adı oluşturma</span><span class="sxs-lookup"><span data-stu-id="950e2-950">Creating a virtual host name for the clustered SAP ASCS/SCS instance</span></span>
- <span data-ttu-id="950e2-951">SAP ilk küme düğümüne yükleme</span><span class="sxs-lookup"><span data-stu-id="950e2-951">Installing the SAP first cluster node</span></span>
- <span data-ttu-id="950e2-952">SAP profili ASCS/SCS örneğinin değiştirme</span><span class="sxs-lookup"><span data-stu-id="950e2-952">Modifying the SAP profile of the ASCS/SCS instance</span></span>
- <span data-ttu-id="950e2-953">Sonda bağlantı noktası ekleme</span><span class="sxs-lookup"><span data-stu-id="950e2-953">Adding a probe port</span></span>
- <span data-ttu-id="950e2-954">Windows Güvenlik Duvarı araştırma bağlantı noktası açma</span><span class="sxs-lookup"><span data-stu-id="950e2-954">Opening the Windows firewall probe port</span></span>

#### <span data-ttu-id="950e2-955"><a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a>Kümelenmiş SAP ASCS/SCS örneği için bir sanal ana bilgisayar adı oluşturma</span><span class="sxs-lookup"><span data-stu-id="950e2-955"><a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a> Create a virtual host name for the clustered SAP ASCS/SCS instance</span></span>

1.  <span data-ttu-id="950e2-956">Windows DNS Yöneticisi'nde ASCS/SCS örneğinin sanal ana bilgisayar adı için bir DNS girişi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="950e2-956">In the Windows DNS manager, create a DNS entry for the virtual host name of the ASCS/SCS instance.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="950e2-957">ASCS/SCS örneğinin sanal ana bilgisayar adı atamak IP adresi Azure yük dengeleyiciye atanan IP adresi ile aynı olmalıdır (**<*SID*> - lb - ascs **).</span><span class="sxs-lookup"><span data-stu-id="950e2-957">The IP address that you assign to the virtual host name of the ASCS/SCS instance must be the same as the IP address that you assigned to Azure Load Balancer (**<*SID*>-lb-ascs**).</span></span>  
  >
  >

  <span data-ttu-id="950e2-958">IP adresi sanal SAP ASCS/SCS ana bilgisayar adının (**pr1 ascs sap**) Azure yük dengeleyici IP adresi ile aynıdır (**pr1 lb ascs**).</span><span class="sxs-lookup"><span data-stu-id="950e2-958">The IP address of the virtual SAP ASCS/SCS host name (**pr1-ascs-sap**) is the same as the IP address of Azure Load Balancer (**pr1-lb-ascs**).</span></span>

  ![Şekil 56: SAP ASCS/SCS küme sanal adı ve TCP/IP adresi için DNS girişini tanımlayın][sap-ha-guide-figure-3046]

  <span data-ttu-id="950e2-960">_**Şekil 56:** SAP ASCS/SCS küme sanal adı ve TCP/IP adresi için DNS girişini tanımlayın_</span><span class="sxs-lookup"><span data-stu-id="950e2-960">_**Figure 56:** Define the DNS entry for the SAP ASCS/SCS cluster virtual name and TCP/IP address_</span></span>

2.  <span data-ttu-id="950e2-961">Sanal ana bilgisayar adı atanmış bir IP adresi tanımlamak için seçin **DNS Yöneticisi'ni** > **etki alanı**.</span><span class="sxs-lookup"><span data-stu-id="950e2-961">To define the IP address assigned to the virtual host name, select **DNS Manager** > **Domain**.</span></span>

  ![Şekil 57: Yeni sanal adı ve TCP/IP adresi SAP ASCS/SCS kümesi yapılandırması için][sap-ha-guide-figure-3047]

  <span data-ttu-id="950e2-963">_**Şekil 57:** yeni sanal adı ve TCP/IP adresi SAP ASCS/SCS küme yapılandırması_</span><span class="sxs-lookup"><span data-stu-id="950e2-963">_**Figure 57:** New virtual name and TCP/IP address for SAP ASCS/SCS cluster configuration_</span></span>

#### <span data-ttu-id="950e2-964"><a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a>SAP ilk küme düğümüne yükleyin</span><span class="sxs-lookup"><span data-stu-id="950e2-964"><a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a> Install the SAP first cluster node</span></span>

1.  <span data-ttu-id="950e2-965">İlk küme düğümü seçeneği küme düğümünde A. yürütme Örneğin, **pr1 ascs 0** ana bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="950e2-965">Execute the first cluster node option on cluster node A. For example, on the **pr1-ascs-0** host.</span></span>
2.  <span data-ttu-id="950e2-966">Azure iç yük dengeleyicisi için bağlantı noktalarını varsayılan tutmak için seçin:</span><span class="sxs-lookup"><span data-stu-id="950e2-966">To keep the default ports for the Azure internal load balancer, select:</span></span>

  * <span data-ttu-id="950e2-967">**ABAP sistem**: **ASCS** örnek numarasını **00**</span><span class="sxs-lookup"><span data-stu-id="950e2-967">**ABAP system**: **ASCS** instance number **00**</span></span>
  * <span data-ttu-id="950e2-968">**Java sistem**: **SCS** örnek numarasını **01**</span><span class="sxs-lookup"><span data-stu-id="950e2-968">**Java system**: **SCS** instance number **01**</span></span>
  * <span data-ttu-id="950e2-969">**ABAP + Java sistem**: **ASCS** örnek numarasını **00** ve **SCS** örnek numarasını **01**</span><span class="sxs-lookup"><span data-stu-id="950e2-969">**ABAP+Java system**: **ASCS** instance number **00** and **SCS** instance number **01**</span></span>

  <span data-ttu-id="950e2-970">Örnek sayıları ABAP ASCS örneği ve Java SCS örneğinin 01 00 dışında kullanmak için öncelikle Azure iç yük dengeleyici varsayılan Yük Dengeleme kuralları, açıklanan değiştirmek gerekir [ASCS/SCS varsayılan Yük Dengeleme kuralları Azure iç yük dengeleyici için değiştirme][sap-ha-guide-8.9].</span><span class="sxs-lookup"><span data-stu-id="950e2-970">To use instance numbers other than 00 for the ABAP ASCS instance and 01 for the Java SCS instance, first you need to change the Azure internal load balancer default load balancing rules, described in [Change the ASCS/SCS default load balancing rules for the Azure internal load balancer][sap-ha-guide-8.9].</span></span>

<span data-ttu-id="950e2-971">Sonraki birkaç görevleri standart SAP yükleme belgelerinde açıklanan değil.</span><span class="sxs-lookup"><span data-stu-id="950e2-971">The next few tasks aren't described in the standard SAP installation documentation.</span></span>

> [!NOTE]
> <span data-ttu-id="950e2-972">SAP yükleme belgelerini ilk ASCS/SCS küme düğümüne yüklemeyi açıklar.</span><span class="sxs-lookup"><span data-stu-id="950e2-972">The SAP installation documentation describes how to install the first ASCS/SCS cluster node.</span></span>
>
>

#### <span data-ttu-id="950e2-973"><a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a>SAP profili ASCS/SCS örneğinin değiştirme</span><span class="sxs-lookup"><span data-stu-id="950e2-973"><a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a> Modify the SAP profile of the ASCS/SCS instance</span></span>

<span data-ttu-id="950e2-974">Yeni bir profil parametre eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="950e2-974">You need to add a new profile parameter.</span></span> <span data-ttu-id="950e2-975">Profil parametre çok uzun süre boşta olduğunda kapanmasını SAP iş süreçlerini ve kuyruğa sunucu arasındaki bağlantıları engeller.</span><span class="sxs-lookup"><span data-stu-id="950e2-975">The profile parameter prevents connections between SAP work processes and the enqueue server from closing when they are idle for too long.</span></span> <span data-ttu-id="950e2-976">Biz sorun senaryoda bahsedilen [SAP ASCS/SCS örneği her iki küme düğümleri üzerinde kayıt defteri girdisini eklemeniz][sap-ha-guide-8.11].</span><span class="sxs-lookup"><span data-stu-id="950e2-976">We mentioned the problem scenario in [Add registry entries on both cluster nodes of the SAP ASCS/SCS instance][sap-ha-guide-8.11].</span></span> <span data-ttu-id="950e2-977">Bu bölümde ayrıca bazı temel TCP/IP bağlantı parametrelerini iki değişiklik sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="950e2-977">In that section, we also introduced two changes to some basic TCP/IP connection parameters.</span></span> <span data-ttu-id="950e2-978">İkinci adımda, sıraya alma sunucusunu gönderecek şekilde ayarlamanız gerekir. bir `keep_alive` bağlantılar Azure iç yük dengeleyicinin boşta kalma eşiği isabet yok böylece sinyal.</span><span class="sxs-lookup"><span data-stu-id="950e2-978">In a second step, you need to set the enqueue server to send a `keep_alive` signal so that the connections don't hit the Azure internal load balancer's idle threshold.</span></span>

<span data-ttu-id="950e2-979">ASCS/SCS örneğinin SAP profilini değiştirmek için:</span><span class="sxs-lookup"><span data-stu-id="950e2-979">To modify the SAP profile of the ASCS/SCS instance:</span></span>

1.  <span data-ttu-id="950e2-980">Bu profil parametre SAP ASCS/SCS örneği profiline ekleyin:</span><span class="sxs-lookup"><span data-stu-id="950e2-980">Add this profile parameter to the SAP ASCS/SCS instance profile:</span></span>

  ```
  enque/encni/set_so_keepalive = true
  ```
  <span data-ttu-id="950e2-981">Bizim örneğimizde, yol şudur:</span><span class="sxs-lookup"><span data-stu-id="950e2-981">In our example, the path is:</span></span>

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_ASCS00_pr1-ascs-sap`

  <span data-ttu-id="950e2-982">Örneğin, SAP SCS profili ve karşılık gelen yol örneği:</span><span class="sxs-lookup"><span data-stu-id="950e2-982">For example, to the SAP SCS instance profile and corresponding path:</span></span>

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_SCS01_pr1-ascs-sap`

2.  <span data-ttu-id="950e2-983">Değişiklikleri uygulamak için SAP ASCS /SCS örneğini yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="950e2-983">To apply the changes, restart the SAP ASCS /SCS instance.</span></span>

#### <span data-ttu-id="950e2-984"><a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a>Bir araştırma bağlantı noktası ekleme</span><span class="sxs-lookup"><span data-stu-id="950e2-984"><a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a> Add a probe port</span></span>

<span data-ttu-id="950e2-985">Azure yük dengeleyici ile çalışma tüm küme yapılandırmasını yapmak için iç yük dengeleyicinin araştırma işlevini kullanın.</span><span class="sxs-lookup"><span data-stu-id="950e2-985">Use the internal load balancer's probe functionality to make the entire cluster configuration work with Azure Load Balancer.</span></span> <span data-ttu-id="950e2-986">Azure iç yük dengeleyicisi genellikle gelen iş yükü katılımcı sanal makineler arasında eşit olarak dağıtır.</span><span class="sxs-lookup"><span data-stu-id="950e2-986">The Azure internal load balancer usually distributes the incoming workload equally between participating virtual machines.</span></span> <span data-ttu-id="950e2-987">Ancak, tek örnek etkin olmadığından bu bazı küme yapılandırmaları çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="950e2-987">However, this won't work in some cluster configurations because only one instance is active.</span></span> <span data-ttu-id="950e2-988">Diğer örnek pasif ve herhangi bir iş yükü kabul edemez.</span><span class="sxs-lookup"><span data-stu-id="950e2-988">The other instance is passive and can’t accept any of the workload.</span></span> <span data-ttu-id="950e2-989">Azure iç yük dengeleyici yalnızca etkin bir örneği için iş atarken araştırma işlevler yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="950e2-989">A probe functionality helps when the Azure internal load balancer assigns work only to an active instance.</span></span> <span data-ttu-id="950e2-990">Araştırma işlevsellikle iç yük dengeleyicisi hangi örnekleri etkin olduğunu ve yalnızca iş yükü örneğiyle hedef algılayabilir.</span><span class="sxs-lookup"><span data-stu-id="950e2-990">With the probe functionality, the internal load balancer can detect which instances are active, and then target only the instance with the workload.</span></span>

<span data-ttu-id="950e2-991">Sonda bağlantı noktası eklemek için:</span><span class="sxs-lookup"><span data-stu-id="950e2-991">To add a probe port:</span></span>

1.  <span data-ttu-id="950e2-992">Geçerli denetleyin **ProbePort** aşağıdaki PowerShell komutunu çalıştırarak ayarlama.</span><span class="sxs-lookup"><span data-stu-id="950e2-992">Check the current **ProbePort** setting by running the following PowerShell command.</span></span> <span data-ttu-id="950e2-993">Sanal makineler biri içinde ondan küme yapılandırmasında yürütün.</span><span class="sxs-lookup"><span data-stu-id="950e2-993">Execute it from within one of the virtual machines in the cluster configuration.</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter
  ```

2.  <span data-ttu-id="950e2-994">Bir araştırma bağlantı noktasını tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="950e2-994">Define a probe port.</span></span> <span data-ttu-id="950e2-995">Varsayılan araştırma bağlantı noktası numarası **0**.</span><span class="sxs-lookup"><span data-stu-id="950e2-995">The default probe port number is **0**.</span></span> <span data-ttu-id="950e2-996">Bizim örneğimizde, araştırma bağlantı noktası kullanırız **62000**.</span><span class="sxs-lookup"><span data-stu-id="950e2-996">In our example, we use probe port **62000**.</span></span>

  ![Şekil 58: Küme yapılandırmasını araştırma bağlantı noktası varsayılan olarak 0 olur.][sap-ha-guide-figure-3048]

  <span data-ttu-id="950e2-998">_**Şekil 58:** varsayılan küme yapılandırması araştırma bağlantı noktası 0'dır_</span><span class="sxs-lookup"><span data-stu-id="950e2-998">_**Figure 58:** The default cluster configuration probe port is 0_</span></span>

  <span data-ttu-id="950e2-999">Bağlantı noktası numarasını SAP Azure Resource Manager şablonları tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="950e2-999">The port number is defined in SAP Azure Resource Manager templates.</span></span> <span data-ttu-id="950e2-1000">PowerShell'de bağlantı noktası numarası atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="950e2-1000">You can assign the port number in PowerShell.</span></span>

  <span data-ttu-id="950e2-1001">Yeni bir ProbePort değerini ayarlamak için  **SAP <*SID*> şu PowerShell betiğini çalıştırın IP ** küme kaynağı.</span><span class="sxs-lookup"><span data-stu-id="950e2-1001">To set a new ProbePort value for the **SAP <*SID*> IP** cluster resource, run the following PowerShell script.</span></span> <span data-ttu-id="950e2-1002">Ortamınız için PowerShell değişkenleri güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="950e2-1002">Update the PowerShell variables for your environment.</span></span> <span data-ttu-id="950e2-1003">Betik çalıştıktan sonra değişiklikleri etkinleştirmek için SAP küme grubu yeniden başlatmanız istenir.</span><span class="sxs-lookup"><span data-stu-id="950e2-1003">After the script runs, you'll be prompted to restart the SAP cluster group to activate the changes.</span></span>

  ```PowerShell
  $SAPSID = "PR1"      # SAP <SID>
  $ProbePort = 62000   # ProbePort of the Azure Internal Load Balancer

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
  Write-Host "Current probe port property of the SAP cluster resource '$SAPIPresourceName' is '$OldProbePort'." -ForegroundColor Cyan
  Write-Host
  Write-Host "Setting the new probe port property of the SAP cluster resource '$SAPIPresourceName' to '$ProbePort' ..." -ForegroundColor Cyan
  Write-Host

  $var | Set-ClusterParameter -Multiple @{"Address"=$IPAddress;"ProbePort"=$ProbePort;"Subnetmask"=$SubnetMask;"Network"=$NetworkName;"OverrideAddressMatch"=$OverrideAddressMatch;"EnableDhcp"=$EnableDhcp}

  Write-Host

  $ActivateChanges = Read-Host "Do you want to take restart SAP cluster role '$SAPClusterRoleName', to activate the changes (yes/no)?"

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

  <span data-ttu-id="950e2-1004">Bunu yaptıktan sonra  **SAP <*SID*> ** Küme rolünü, doğrulayın **ProbePort** yeni değere ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="950e2-1004">After you bring the **SAP <*SID*>** cluster role online, verify that **ProbePort** is set to the new value.</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter

  ```

  ![Şekil 59: yeni değer ayarlandıktan sonra küme bağlantı noktası araştırma][sap-ha-guide-figure-3049]

  <span data-ttu-id="950e2-1006">_**Şekil 59:** yeni değer ayarlandıktan sonra küme bağlantı noktası araştırma_</span><span class="sxs-lookup"><span data-stu-id="950e2-1006">_**Figure 59:** Probe the cluster port after you set the new value_</span></span>

#### <span data-ttu-id="950e2-1007"><a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a>Windows Güvenlik Duvarı araştırma bağlantı noktasını açın</span><span class="sxs-lookup"><span data-stu-id="950e2-1007"><a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a> Open the Windows firewall probe port</span></span>

<span data-ttu-id="950e2-1008">Her iki küme düğümlerinde Windows Güvenlik Duvarı araştırma bağlantı açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="950e2-1008">You need to open a Windows firewall probe port on both cluster nodes.</span></span> <span data-ttu-id="950e2-1009">Bir Windows Güvenlik Duvarı araştırma bağlantı noktasını açmak için aşağıdaki komut dosyasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="950e2-1009">Use the following script to open a Windows firewall probe port.</span></span> <span data-ttu-id="950e2-1010">Ortamınız için PowerShell değişkenleri güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="950e2-1010">Update the PowerShell variables for your environment.</span></span>

  ```PowerShell
  $ProbePort = 62000   # ProbePort of the Azure Internal Load Balancer

  New-NetFirewallRule -Name AzureProbePort -DisplayName "Rule for Azure Probe Port" -Direction Inbound -Action Allow -Protocol TCP -LocalPort $ProbePort
  ```

<span data-ttu-id="950e2-1011">**ProbePort** ayarlanır **62000**.</span><span class="sxs-lookup"><span data-stu-id="950e2-1011">The **ProbePort** is set to **62000**.</span></span> <span data-ttu-id="950e2-1012">Dosya paylaşımına erişebilirsiniz artık  **\\\ascsha-clsap\sapmnt** diğer konakları, gibi kadar **ascsha dbas**.</span><span class="sxs-lookup"><span data-stu-id="950e2-1012">Now you can access the file share **\\\ascsha-clsap\sapmnt** from other hosts, such as from **ascsha-dbas**.</span></span>

### <span data-ttu-id="950e2-1013"><a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a>Veritabanı örneğini yükleyin</span><span class="sxs-lookup"><span data-stu-id="950e2-1013"><a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a> Install the database instance</span></span>

<span data-ttu-id="950e2-1014">Veritabanı örneği yüklemek için SAP yükleme belgelerinde açıklanan işlemi izleyin.</span><span class="sxs-lookup"><span data-stu-id="950e2-1014">To install the database instance, follow the process described in the SAP installation documentation.</span></span>

### <span data-ttu-id="950e2-1015"><a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a>İkinci küme düğümü yükleme</span><span class="sxs-lookup"><span data-stu-id="950e2-1015"><a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a> Install the second cluster node</span></span>

<span data-ttu-id="950e2-1016">İkinci küme yüklemek için SAP Yükleme Kılavuzu'ndaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="950e2-1016">To install the second cluster, follow the steps in the SAP installation guide.</span></span>

### <span data-ttu-id="950e2-1017"><a name="094bc895-31d4-4471-91cc-1513b64e406a"></a>SAP ERS Windows hizmet örneği başlangıç türünü değiştirme</span><span class="sxs-lookup"><span data-stu-id="950e2-1017"><a name="094bc895-31d4-4471-91cc-1513b64e406a"></a> Change the start type of the SAP ERS Windows service instance</span></span>

<span data-ttu-id="950e2-1018">SAP ERS Windows hizmeti başlangıç türünü değiştirme **otomatik (Gecikmeli Başlatma)** her iki küme düğümlerinde.</span><span class="sxs-lookup"><span data-stu-id="950e2-1018">Change the start type of the SAP ERS Windows service to **Automatic (Delayed Start)** on both cluster nodes.</span></span>

![Şekil 60: SAP ERS örneği için hizmet türü Gecikmeli otomatik olarak değiştirin.][sap-ha-guide-figure-3050]

<span data-ttu-id="950e2-1020">_**Şekil 60:** SAP ERS örneğe otomatik Gecikmeli hizmet türünü değiştir_</span><span class="sxs-lookup"><span data-stu-id="950e2-1020">_**Figure 60:** Change the service type for the SAP ERS instance to delayed automatic_</span></span>

### <span data-ttu-id="950e2-1021"><a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a>SAP birincil uygulama sunucusu yükleme</span><span class="sxs-lookup"><span data-stu-id="950e2-1021"><a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a> Install the SAP Primary Application Server</span></span>

<span data-ttu-id="950e2-1022">Birincil uygulama sunucusu (PAS) örneğini yükleyin <*SID*> - dı - 0 PAS barındırmak için belirlediğiniz sanal makinede.</span><span class="sxs-lookup"><span data-stu-id="950e2-1022">Install the Primary Application Server (PAS) instance <*SID*>-di-0 on the virtual machine that you've designated to host the PAS.</span></span> <span data-ttu-id="950e2-1023">Azure veya DataKeeper özgü ayarları bir bağımlılık yoktur.</span><span class="sxs-lookup"><span data-stu-id="950e2-1023">There are no dependencies on Azure or DataKeeper-specific settings.</span></span>

### <span data-ttu-id="950e2-1024"><a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a>SAP ek uygulama sunucusu yükleme</span><span class="sxs-lookup"><span data-stu-id="950e2-1024"><a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a> Install the SAP Additional Application Server</span></span>

<span data-ttu-id="950e2-1025">Bir SAP ek uygulama sunucusu (AAS) tüm sanal SAP uygulama sunucusu örneği barındırmak için belirlediğiniz makinelere yükleyin.</span><span class="sxs-lookup"><span data-stu-id="950e2-1025">Install an SAP Additional Application Server (AAS) on all the virtual machines that you've designated to host an SAP Application Server instance.</span></span> <span data-ttu-id="950e2-1026">Örneğin, <*SID*> - dı - 1 için <*SID*> - di -&lt;n&gt;.</span><span class="sxs-lookup"><span data-stu-id="950e2-1026">For example, on <*SID*>-di-1 to <*SID*>-di-&lt;n&gt;.</span></span>

> [!NOTE]
> <span data-ttu-id="950e2-1027">Bu, bir yüksek kullanılabilirlik SAP NetWeaver sistemi yüklemesini tamamlar.</span><span class="sxs-lookup"><span data-stu-id="950e2-1027">This finishes the installation of a high-availability SAP NetWeaver system.</span></span> <span data-ttu-id="950e2-1028">Ardından, yük devretme testi ile devam edin.</span><span class="sxs-lookup"><span data-stu-id="950e2-1028">Next, proceed with failover testing.</span></span>
>


## <span data-ttu-id="950e2-1029"><a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a>SIOS çoğaltma ve SAP ASCS/SCS örneği yük devretme testi</span><span class="sxs-lookup"><span data-stu-id="950e2-1029"><a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a> Test the SAP ASCS/SCS instance failover and SIOS replication</span></span>
<span data-ttu-id="950e2-1030">Yük Devretme Kümesi Yöneticisi'ni ve SIOS DataKeeper yönetimi ve yapılandırması aracını kullanarak bir SAP ASCS/SCS örneği yük devretme ve SIOS disk çoğaltması izlemek ve test kolaydır.</span><span class="sxs-lookup"><span data-stu-id="950e2-1030">It's easy to test and monitor an SAP ASCS/SCS instance failover and SIOS disk replication by using Failover Cluster Manager and the SIOS DataKeeper Management and Configuration tool.</span></span>

### <span data-ttu-id="950e2-1031"><a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a>SAP ASCS/SCS örneği bir küme düğümünde çalışıyor</span><span class="sxs-lookup"><span data-stu-id="950e2-1031"><a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a> SAP ASCS/SCS instance is running on cluster node A</span></span>

<span data-ttu-id="950e2-1032">**SAP PR1** küme grubu A'daki küme düğümünde çalışıyor Örneğin, **pr1 ascs 0**.</span><span class="sxs-lookup"><span data-stu-id="950e2-1032">The **SAP PR1** cluster group is running on cluster node A. For example, on **pr1-ascs-0**.</span></span> <span data-ttu-id="950e2-1033">Paylaşılan disk bölümü olan sürücü S, ata, **SAP PR1** küme grubu ve a düğümünü kümeye ASCS/SCS örneği kullanan</span><span class="sxs-lookup"><span data-stu-id="950e2-1033">Assign the shared disk drive S, which is part of the **SAP PR1** cluster group, and which the ASCS/SCS instance uses, to cluster node A.</span></span>

![Şekil 61: Yük devretme kümesi Yöneticisi: SAP < SID > Küme grubu, bir küme düğümünde çalışıyor][sap-ha-guide-figure-5000]

<span data-ttu-id="950e2-1035">_**Şekil 61:** yük devretme kümesi Yöneticisi: SAP <*SID*> Küme grubu, bir küme düğümünde çalışıyor_</span><span class="sxs-lookup"><span data-stu-id="950e2-1035">_**Figure 61:** Failover Cluster Manager: The SAP <*SID*> cluster group is running on cluster node A_</span></span>

<span data-ttu-id="950e2-1036">SIOS DataKeeper yönetim ve Yapılandırma Aracı'nda paylaşılan disk verilerini zaman uyumlu olarak küme düğümü bir kaynak birim sürücüsünden S küme düğümünde B. hedef birim sürücü S için çoğaltıldığından emin görebilirsiniz Örneğin, gelen çoğaltılır **pr1 ascs 0 [10.0.0.40]** için **pr1 ascs 1 [10.0.0.41]**.</span><span class="sxs-lookup"><span data-stu-id="950e2-1036">In the SIOS DataKeeper Management and Configuration tool, you can see that the shared disk data is synchronously replicated from the source volume drive S on cluster node A to the target volume drive S on cluster node B. For example, it's replicated from **pr1-ascs-0 [10.0.0.40]** to **pr1-ascs-1 [10.0.0.41]**.</span></span>

![Şekil 62: SIOS DataKeeper içinde yerel birim küme düğümünden bir küme düğümüne B çoğaltma][sap-ha-guide-figure-5001]

<span data-ttu-id="950e2-1038">_**Şekil 62:** SIOS DataKeeper içinde yerel birim küme düğümünden bir küme düğümüne B çoğaltma_</span><span class="sxs-lookup"><span data-stu-id="950e2-1038">_**Figure 62:** In SIOS DataKeeper, replicate the local volume from cluster node A to cluster node B_</span></span>

### <span data-ttu-id="950e2-1039"><a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a>Bir düğümden yük devretme düğümüne B</span><span class="sxs-lookup"><span data-stu-id="950e2-1039"><a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a> Failover from node A to node B</span></span>

1.  <span data-ttu-id="950e2-1040">Bir yük devretme SAP başlatmak için bu seçeneklerden birini <*SID*> küme grubuna bir küme düğümünden küme düğümü B:</span><span class="sxs-lookup"><span data-stu-id="950e2-1040">Choose one of these options to initiate a failover of the SAP <*SID*> cluster group from cluster node A to cluster node B:</span></span>
  - <span data-ttu-id="950e2-1041">Yük Devretme Kümesi Yöneticisi'ni kullanın</span><span class="sxs-lookup"><span data-stu-id="950e2-1041">Use Failover Cluster Manager</span></span>  
  - <span data-ttu-id="950e2-1042">Yük devretme kümesi PowerShell kullanma</span><span class="sxs-lookup"><span data-stu-id="950e2-1042">Use Failover Cluster PowerShell</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPClusterGroup = "SAP $SAPSID"
  Move-ClusterGroup -Name $SAPClusterGroup

  ```
2.  <span data-ttu-id="950e2-1043">Küme düğümü bir Windows konuk işletim sistemi içinde yeniden (Bu SAP otomatik bir yük devretme başlatır <*SID*> düğümünden bir küme grubu B düğümü için).</span><span class="sxs-lookup"><span data-stu-id="950e2-1043">Restart cluster node A within the Windows guest operating system (this initiates an automatic failover of the SAP <*SID*> cluster group from node A to node B).</span></span>  
3.  <span data-ttu-id="950e2-1044">Küme düğümü bir Azure portalından yeniden (Bu SAP otomatik bir yük devretme başlatır <*SID*> düğümünden bir küme grubu B düğümü için).</span><span class="sxs-lookup"><span data-stu-id="950e2-1044">Restart cluster node A from the Azure portal (this initiates an automatic failover of the SAP <*SID*> cluster group from node A to node B).</span></span>  
4.  <span data-ttu-id="950e2-1045">Azure PowerShell kullanarak küme düğümü bir yeniden başlatma (Bu SAP otomatik olarak yük devretmesi başlatır <*SID*> düğümünden bir küme grubu B düğümü için).</span><span class="sxs-lookup"><span data-stu-id="950e2-1045">Restart cluster node A by using Azure PowerShell (this initiates an automatic failover of the SAP <*SID*> cluster group from node A to node B).</span></span>

  <span data-ttu-id="950e2-1046">SAP yük devretme sonrasında <*SID*> Küme grubu b küme düğümünde çalışıyor Örneğin, üzerinde çalıştırıldığı **pr1 ascs 1**.</span><span class="sxs-lookup"><span data-stu-id="950e2-1046">After failover, the SAP <*SID*> cluster group is running on cluster node B. For example, it's running on **pr1-ascs-1**.</span></span>

  ![Şekil 63: Yük devretme kümesi Yöneticisi'nde SAP < SID > Küme grubu B küme düğümünde çalışıyor][sap-ha-guide-figure-5002]

  <span data-ttu-id="950e2-1048">_**Şekil 63**: yük devretme kümesi Yöneticisi'nde, SAP <*SID*> Küme grubu B küme düğümünde çalışıyor_</span><span class="sxs-lookup"><span data-stu-id="950e2-1048">_**Figure 63**: In Failover Cluster Manager, the SAP <*SID*> cluster group is running on cluster node B_</span></span>

  <span data-ttu-id="950e2-1049">Paylaşılan disk artık takılı kümede düğüm B. SIOS DataKeeper veri sürücüsünden kaynak birim S B küme düğümünde Küme düğümünde A. hedef birim sürücü S için çoğaltma Örneğin, gelen çoğaltma **pr1 ascs 1 [10.0.0.41]** için **pr1 ascs 0 [10.0.0.40]**.</span><span class="sxs-lookup"><span data-stu-id="950e2-1049">The shared disk is now mounted on cluster node B. SIOS DataKeeper is replicating data from source volume drive S on cluster node B to target volume drive S on cluster node A. For example, it's replicating from **pr1-ascs-1 [10.0.0.41]** to **pr1-ascs-0 [10.0.0.40]**.</span></span>

  ![Şekil 64: Yerel birim SIOS DataKeeper, küme düğümü bir küme düğümünden B çoğaltır.][sap-ha-guide-figure-5003]

  <span data-ttu-id="950e2-1051">_**Şekil 64:** SIOS DataKeeper çoğaltır yerel birim düğüm bir küme için küme düğümünden B_</span><span class="sxs-lookup"><span data-stu-id="950e2-1051">_**Figure 64:** SIOS DataKeeper replicates the local volume from cluster node B to cluster node A_</span></span>
