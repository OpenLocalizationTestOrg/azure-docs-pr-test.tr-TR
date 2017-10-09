---
title: "Azure Site RECOVERY'yi kullanarak aaaPrepare Azure kaynaklarını tooreplicate Hyper-V Vm'lerini (System Center VMM olmadan) tooAzure | Microsoft Docs"
description: "Azure Site Recovery kullanarak Hyper-V Vm'lerini (VMM olmadan) tooAzure çoğaltma başlamadan önce Azure yerinde gerekenler açıklanmaktadır"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 28fa722c-675e-4637-98eb-7ccbf3806d69
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: f659e300c39253b0eaf7218bee9d39b11682edb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-prepare-azure-resources-for-hyper-v-replication-tooazure"></a><span data-ttu-id="1b7c7-103">5. adım: Hyper-V çoğaltma tooAzure için Azure kaynaklarını hazırlama</span><span class="sxs-lookup"><span data-stu-id="1b7c7-103">Step 5: Prepare Azure resources for Hyper-V replication tooAzure</span></span>

<span data-ttu-id="1b7c7-104">Merhaba yönergeleri kullanın Bu makale tooprepare Azure kaynakları, çoğaltabilirsiniz böylece şirket içi Hyper-V Vm'lerini (System Center VMM olmadan) hello kullanarak tooAzure [Azure Site Recovery](site-recovery-overview.md) hizmet.</span><span class="sxs-lookup"><span data-stu-id="1b7c7-104">Use hello instructions in this article tooprepare Azure resources so that you can replicate on-premises Hyper-V VMs (without System Center VMM) tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="1b7c7-105">Bu makaleyi okuduktan sonra hello altındaki tüm yorumlar post veya üzerinde hello teknik sorular sormak [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="1b7c7-105">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="1b7c7-106">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="1b7c7-106">Before you start</span></span>

<span data-ttu-id="1b7c7-107">Emin olun hello okuma [önkoşulları](hyper-v-site-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="1b7c7-107">Make sure you've read hello [prerequisites](hyper-v-site-walkthrough-prerequisites.md)</span></span>

## <a name="set-up-an-azure-account"></a><span data-ttu-id="1b7c7-108">Bir Azure hesabı ayarlama</span><span class="sxs-lookup"><span data-stu-id="1b7c7-108">Set up an Azure account</span></span>

- <span data-ttu-id="1b7c7-109">Alma bir [Microsoft Azure hesabı](http://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="1b7c7-109">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="1b7c7-110">[Ücretsiz deneme sürümüyle](https://azure.microsoft.com/pricing/free-trial/) başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1b7c7-110">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="1b7c7-111">Site Recovery, altında coğrafi kullanılabilirlik kısmına hello desteklenen bölgeleri kontrol [Azure Site Recovery fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="1b7c7-111">Check hello supported regions for Site Recovery, Under Geographic Availability in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="1b7c7-112">Hakkında bilgi edinin [Site Recovery fiyatlandırma](site-recovery-faq.md#pricing)ve hello [fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="1b7c7-112">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get hello [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>


## <a name="set-up-an-azure-network"></a><span data-ttu-id="1b7c7-113">Azure ağı ayarlama</span><span class="sxs-lookup"><span data-stu-id="1b7c7-113">Set up an Azure network</span></span>

- <span data-ttu-id="1b7c7-114">Azure ağı ayarlama ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="1b7c7-114">Set up an Azure network.</span></span> <span data-ttu-id="1b7c7-115">Yük devretme sonrasında oluşturulduğunda azure sanal makineleri bu ağda yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="1b7c7-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="1b7c7-116">Merhaba ağ hello olmalıdır hello aynı bölgede kurtarma Hizmetleri kasası</span><span class="sxs-lookup"><span data-stu-id="1b7c7-116">hello network should be in hello same region as hello Recovery Services vault</span></span>
- <span data-ttu-id="1b7c7-117">Site Kurtarma'hello Azure portalı bölümünde ayarladığınız ağlar kullanabilir [Resource Manager](../resource-manager-deployment-model.md), ya da Klasik modda.</span><span class="sxs-lookup"><span data-stu-id="1b7c7-117">Site Recovery in hello Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="1b7c7-118">Başlamadan önce bir ağ ayarlamanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="1b7c7-118">We recommend you set up a network before you begin.</span></span> <span data-ttu-id="1b7c7-119">Bunu yapmazsanız, toodo gerekir, Site Recovery dağıtımı sırasında.</span><span class="sxs-lookup"><span data-stu-id="1b7c7-119">If you don't, you need toodo it during Site Recovery deployment.</span></span>
- <span data-ttu-id="1b7c7-120">Hakkında bilgi edinin [sanal ağ fiyatlandırma](https://azure.microsoft.com/pricing/details/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="1b7c7-120">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="1b7c7-121">Azure depolama hesabı ayarlama</span><span class="sxs-lookup"><span data-stu-id="1b7c7-121">Set up an Azure storage account</span></span>

- <span data-ttu-id="1b7c7-122">Site Recovery, şirket içi makineler tooAzure depolama çoğaltır.</span><span class="sxs-lookup"><span data-stu-id="1b7c7-122">Site Recovery replicates on-premises machines tooAzure storage.</span></span> <span data-ttu-id="1b7c7-123">Yük devretme gerçekleştikten sonra azure VM'ler hello depolama biriminden oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="1b7c7-123">Azure VMs are created from hello storage after failover occurs.</span></span>
- <span data-ttu-id="1b7c7-124">Standart/Premium'u ayarlama ayarlamak [Azure depolama hesabı](../storage/common/storage-create-storage-account.md#create-a-storage-account) toohold veri çoğaltılan tooAzure.</span><span class="sxs-lookup"><span data-stu-id="1b7c7-124">Set up a standard/premium [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) toohold data replicated tooAzure.</span></span>
- <span data-ttu-id="1b7c7-125">[Premium depolama](../storage/common/storage-premium-storage.md) sanal makineler için bir tutarlı bir şekilde yüksek g/ç performans ve düşük gecikme süresi toohost g/ç yoğun iş yükleri gerek genellikle kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1b7c7-125">[Premium storage](../storage/common/storage-premium-storage.md) is typically used for virtual machines that need a consistently high IO performance, and low latency toohost IO intensive workloads.</span></span>
- <span data-ttu-id="1b7c7-126">Toouse istiyorsanız premium hesap toostore veri çoğaltılan, yakalama devam eden tooon içi verileri değiştiren bir standart depolama hesabı toostore çoğaltma günlükleri de gerekir.</span><span class="sxs-lookup"><span data-stu-id="1b7c7-126">If you want toouse a premium account toostore replicated data, you also need a standard storage account toostore replication logs that capture ongoing changes tooon-premises data.</span></span>
- <span data-ttu-id="1b7c7-127">Merhaba kaynak modeline bağlı olarak toouse Azure vm'lerinde istediğiniz, hesap ayarlama [Resource Manager moduna](../storage/common/storage-create-storage-account.md), veya [Klasik modda](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="1b7c7-127">Depending on hello resource model you want toouse for failed over Azure VMs, you set up an account in [Resource Manager mode](../storage/common/storage-create-storage-account.md), or [classic mode](../storage/common/storage-create-storage-account.md).</span></span>
- <span data-ttu-id="1b7c7-128">Başlamadan önce bir depolama hesabı ayarlamanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="1b7c7-128">We recommend that you set up a storage account before you begin.</span></span> <span data-ttu-id="1b7c7-129">Bunu yapmazsanız toodo gerekir, Site Recovery dağıtımı sırasında.</span><span class="sxs-lookup"><span data-stu-id="1b7c7-129">If you don't you need toodo it during Site Recovery deployment.</span></span> <span data-ttu-id="1b7c7-130">Merhaba hesapları hello olmalıdır hello aynı bölgede kurtarma Hizmetleri kasası.</span><span class="sxs-lookup"><span data-stu-id="1b7c7-130">hello accounts must be in hello same region as hello Recovery Services vault.</span></span>
- <span data-ttu-id="1b7c7-131">Depolama hesapları kullanılan Site Recovery tarafından hello içindeki kaynak grupları arasında aynı taşıyamazsınız aboneliği ya da farklı Aboneliklerdeki.</span><span class="sxs-lookup"><span data-stu-id="1b7c7-131">You can't move storage accounts used by Site Recovery across resource groups within hello same subscription, or across different subscriptions.</span></span>


## <a name="next-steps"></a><span data-ttu-id="1b7c7-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1b7c7-132">Next steps</span></span>

<span data-ttu-id="1b7c7-133">Çok Git[adım 6: hazırlama Hyper-V kaynakları](hyper-v-site-walkthrough-prepare-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="1b7c7-133">Go too[Step 6: Prepare Hyper-V resources](hyper-v-site-walkthrough-prepare-hyper-v.md)</span></span>
