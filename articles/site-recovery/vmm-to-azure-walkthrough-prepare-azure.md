---
title: "Azure Site RECOVERY'yi kullanarak aaaPrepare Azure kaynaklarını tooreplicate (System Center VMM ile) Hyper-V sanal makineleri tooAzure | Microsoft Docs"
description: "Hyper-V Vm'lerini (VMM ile) tooAzure çoğaltmaya Azure Site Recovery kullanmaya başlamadan önce Azure yerinde gerekenler açıklanmaktadır"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 1568bdc3-e767-477b-b040-f13699ab5644
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 86bfbab7722fe5bd5b93b92e398d1d441505d3b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-prepare-azure-resources-for-hyper-v-replication-with-vmm-tooazure"></a><span data-ttu-id="a6a1c-103">5. adım: Hyper-V çoğaltma (VMM ile) tooAzure için Azure kaynaklarını hazırlama</span><span class="sxs-lookup"><span data-stu-id="a6a1c-103">Step 5: Prepare Azure resources for Hyper-V replication (with VMM) tooAzure</span></span>

<span data-ttu-id="a6a1c-104">Doğruladıktan sonra [ağ gereksinimleri](vmm-to-azure-walkthrough-network.md), bu makale tooprepare Azure hello yönergeleri kullanın kaynakları şirket içi Hyper-V sanal makinelerini System Center Virtual Machine Manager (VMM) bulutlarında tooAzure içinde çoğaltabilirsiniz böylece kullanma Merhaba [Azure Site Recovery](site-recovery-overview.md) hizmet.</span><span class="sxs-lookup"><span data-stu-id="a6a1c-104">After verifying [network requirements](vmm-to-azure-walkthrough-network.md), use hello instructions in this article tooprepare Azure resources so that you can replicate on-premises Hyper-V VMs in System Center Virtual Machine Manager (VMM) clouds tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="a6a1c-105">Bu makaleyi okuduktan sonra hello altındaki tüm yorumlar post veya üzerinde hello teknik sorular sormak [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="a6a1c-105">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-an-azure-account"></a><span data-ttu-id="a6a1c-106">Bir Azure hesabı ayarlama</span><span class="sxs-lookup"><span data-stu-id="a6a1c-106">Set up an Azure account</span></span>

- <span data-ttu-id="a6a1c-107">Alma bir [Microsoft Azure hesabı](http://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="a6a1c-107">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="a6a1c-108">[Ücretsiz deneme sürümüyle](https://azure.microsoft.com/pricing/free-trial/) başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6a1c-108">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="a6a1c-109">Site Recovery, altında coğrafi kullanılabilirlik kısmına hello desteklenen bölgeleri kontrol [Azure Site Recovery fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="a6a1c-109">Check hello supported regions for Site Recovery, Under Geographic Availability in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="a6a1c-110">Hakkında bilgi edinin [Site Recovery fiyatlandırma](site-recovery-faq.md#pricing)ve hello [fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="a6a1c-110">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get hello [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="a6a1c-111">Azure hesabınızda hello doğru olduğundan emin olun [izinleri](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)toocreate Azure VM'ler.</span><span class="sxs-lookup"><span data-stu-id="a6a1c-111">Make sure your Azure account has hello correct [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)toocreate Azure VMs.</span></span> <span data-ttu-id="a6a1c-112">[Daha fazla bilgi edinin](../active-directory/role-based-access-built-in-roles.md) Azure rol tabanlı erişim denetimi hakkında.</span><span class="sxs-lookup"><span data-stu-id="a6a1c-112">[Learn more](../active-directory/role-based-access-built-in-roles.md) about Azure role-based access control.</span></span>


## <a name="set-up-an-azure-network"></a><span data-ttu-id="a6a1c-113">Azure ağı ayarlama</span><span class="sxs-lookup"><span data-stu-id="a6a1c-113">Set up an Azure network</span></span>

- <span data-ttu-id="a6a1c-114">Ayarlanmış bir [Azure ağ](../virtual-network/virtual-network-get-started-vnet-subnet.md).</span><span class="sxs-lookup"><span data-stu-id="a6a1c-114">Set up an [Azure network](../virtual-network/virtual-network-get-started-vnet-subnet.md).</span></span> <span data-ttu-id="a6a1c-115">Yük devretme sonrasında oluşturulduğunda azure sanal makineleri bu ağda yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="a6a1c-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="a6a1c-116">Merhaba ağ hello olmalıdır hello aynı bölgede kurtarma Hizmetleri kasası</span><span class="sxs-lookup"><span data-stu-id="a6a1c-116">hello network should be in hello same region as hello Recovery Services vault</span></span>
- <span data-ttu-id="a6a1c-117">Site Kurtarma'hello Azure portalı bölümünde ayarladığınız ağlar kullanabilir [Resource Manager](../resource-manager-deployment-model.md), ya da Klasik modda.</span><span class="sxs-lookup"><span data-stu-id="a6a1c-117">Site Recovery in hello Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="a6a1c-118">Başlamadan önce bir ağ ayarlamanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="a6a1c-118">We recommend you set up a network before you begin.</span></span> <span data-ttu-id="a6a1c-119">Bunu yapmazsanız, toodo gerekir, Site Recovery dağıtımı sırasında.</span><span class="sxs-lookup"><span data-stu-id="a6a1c-119">If you don't, you need toodo it during Site Recovery deployment.</span></span>
- <span data-ttu-id="a6a1c-120">Hakkında bilgi edinin [sanal ağ fiyatlandırma](https://azure.microsoft.com/pricing/details/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="a6a1c-120">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="a6a1c-121">Azure depolama hesabı ayarlama</span><span class="sxs-lookup"><span data-stu-id="a6a1c-121">Set up an Azure storage account</span></span>

- <span data-ttu-id="a6a1c-122">Site Recovery, şirket içi makineler tooAzure depolama çoğaltır.</span><span class="sxs-lookup"><span data-stu-id="a6a1c-122">Site Recovery replicates on-premises machines tooAzure storage.</span></span> <span data-ttu-id="a6a1c-123">Yük devretme gerçekleştikten sonra azure VM'ler hello depolama biriminden oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="a6a1c-123">Azure VMs are created from hello storage after failover occurs.</span></span>
- <span data-ttu-id="a6a1c-124">Standart/Premium'u ayarlama ayarlamak [Azure depolama hesabı](../storage/common/storage-create-storage-account.md#create-a-storage-account) toohold veri çoğaltılan tooAzure.</span><span class="sxs-lookup"><span data-stu-id="a6a1c-124">Set up a standard/premium [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) toohold data replicated tooAzure.</span></span>
- <span data-ttu-id="a6a1c-125">[Premium depolama](../storage/common/storage-premium-storage.md) sanal makineler için bir tutarlı bir şekilde yüksek g/ç performans ve düşük gecikme süresi toohost g/ç yoğun iş yükleri gerek genellikle kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a6a1c-125">[Premium storage](../storage/common/storage-premium-storage.md) is typically used for virtual machines that need a consistently high IO performance, and low latency toohost IO intensive workloads.</span></span>
- <span data-ttu-id="a6a1c-126">Toouse istiyorsanız premium hesap toostore veri çoğaltılan, yakalama devam eden tooon içi verileri değiştiren bir standart depolama hesabı toostore çoğaltma günlükleri de gerekir.</span><span class="sxs-lookup"><span data-stu-id="a6a1c-126">If you want toouse a premium account toostore replicated data, you also need a standard storage account toostore replication logs that capture ongoing changes tooon-premises data.</span></span>
- <span data-ttu-id="a6a1c-127">Merhaba kaynak modeline bağlı olarak toouse Azure vm'lerinde istediğiniz, hesap ayarlama [Resource Manager moduna](../storage/common/storage-create-storage-account.md), veya [Klasik modda](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="a6a1c-127">Depending on hello resource model you want toouse for failed over Azure VMs, you set up an account in [Resource Manager mode](../storage/common/storage-create-storage-account.md), or [classic mode](../storage/common/storage-create-storage-account.md).</span></span>
- <span data-ttu-id="a6a1c-128">Başlamadan önce bir depolama hesabı ayarlamanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="a6a1c-128">We recommend that you set up a storage account before you begin.</span></span> <span data-ttu-id="a6a1c-129">Bunu yapmazsanız toodo gerekir, Site Recovery dağıtımı sırasında.</span><span class="sxs-lookup"><span data-stu-id="a6a1c-129">If you don't you need toodo it during Site Recovery deployment.</span></span> <span data-ttu-id="a6a1c-130">Merhaba hesapları hello olmalıdır hello aynı bölgede kurtarma Hizmetleri kasası.</span><span class="sxs-lookup"><span data-stu-id="a6a1c-130">hello accounts must be in hello same region as hello Recovery Services vault.</span></span>
- <span data-ttu-id="a6a1c-131">Depolama hesapları kullanılan Site Recovery tarafından hello içindeki kaynak grupları arasında aynı taşıyamazsınız aboneliği ya da farklı Aboneliklerdeki.</span><span class="sxs-lookup"><span data-stu-id="a6a1c-131">You can't move storage accounts used by Site Recovery across resource groups within hello same subscription, or across different subscriptions.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a6a1c-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a6a1c-132">Next steps</span></span>

<span data-ttu-id="a6a1c-133">Çok Git[adım 6: VMM hazırlama](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="a6a1c-133">Go too[Step 6: Prepare VMM](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span></span>
