---
title: "Azure Site Kurtarma'yı kullanarak Azure (System Center VMM ile) Hyper-V sanal makineleri çoğaltmak için Azure kaynaklarını hazırlama | Microsoft Docs"
description: "Azure Site RECOVERY'yi kullanarak Azure'a, Hyper-V Vm'lerini (VMM ile) çoğaltma başlamadan önce Azure yerinde gerekenler açıklanmaktadır"
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
ms.openlocfilehash: 63b005f37ab5e15e8a1b4645446d65f1529f1bbd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="step-5-prepare-azure-resources-for-hyper-v-replication-with-vmm-to-azure"></a><span data-ttu-id="c7db2-103">5. adım: (VMM ile) Hyper-V çoğaltma Azure için Azure kaynaklarını hazırlama</span><span class="sxs-lookup"><span data-stu-id="c7db2-103">Step 5: Prepare Azure resources for Hyper-V replication (with VMM) to Azure</span></span>

<span data-ttu-id="c7db2-104">Doğruladıktan sonra [ağ gereksinimleri](vmm-to-azure-walkthrough-network.md), böylece System Center Virtual Machine Manager (VMM) bulutlarında şirket içi Hyper-V Vm'lerini Azure'a çoğaltabilirsiniz Azure kaynaklarını hazırlamak için bu makaledeki yönergeleri kullanın kullanarak [Azure Site Recovery](site-recovery-overview.md) hizmet.</span><span class="sxs-lookup"><span data-stu-id="c7db2-104">After verifying [network requirements](vmm-to-azure-walkthrough-network.md), use the instructions in this article to prepare Azure resources so that you can replicate on-premises Hyper-V VMs in System Center Virtual Machine Manager (VMM) clouds to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="c7db2-105">Bu makaleyi okuduktan sonra altındaki bir yorum gönderin ya da teknik sorular [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="c7db2-105">After reading this article, post any comments at the bottom, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-an-azure-account"></a><span data-ttu-id="c7db2-106">Bir Azure hesabı ayarlama</span><span class="sxs-lookup"><span data-stu-id="c7db2-106">Set up an Azure account</span></span>

- <span data-ttu-id="c7db2-107">Alma bir [Microsoft Azure hesabı](http://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="c7db2-107">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="c7db2-108">[Ücretsiz deneme sürümüyle](https://azure.microsoft.com/pricing/free-trial/) başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c7db2-108">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="c7db2-109">Site Recovery, altında coğrafi kullanılabilirlik kısmına desteklenen bölgeleri kontrol [Azure Site Recovery fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="c7db2-109">Check the supported regions for Site Recovery, Under Geographic Availability in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="c7db2-110">Hakkında bilgi edinin [Site Recovery fiyatlandırma](site-recovery-faq.md#pricing)ve alma [fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="c7db2-110">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get the [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="c7db2-111">Azure hesabınızda doğru olduğundan emin olun [izinleri](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)Azure VM'ler oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="c7db2-111">Make sure your Azure account has the correct [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)to create Azure VMs.</span></span> <span data-ttu-id="c7db2-112">[Daha fazla bilgi edinin](../active-directory/role-based-access-built-in-roles.md) Azure rol tabanlı erişim denetimi hakkında.</span><span class="sxs-lookup"><span data-stu-id="c7db2-112">[Learn more](../active-directory/role-based-access-built-in-roles.md) about Azure role-based access control.</span></span>


## <a name="set-up-an-azure-network"></a><span data-ttu-id="c7db2-113">Azure ağı ayarlama</span><span class="sxs-lookup"><span data-stu-id="c7db2-113">Set up an Azure network</span></span>

- <span data-ttu-id="c7db2-114">Ayarlanmış bir [Azure ağ](../virtual-network/virtual-network-get-started-vnet-subnet.md).</span><span class="sxs-lookup"><span data-stu-id="c7db2-114">Set up an [Azure network](../virtual-network/virtual-network-get-started-vnet-subnet.md).</span></span> <span data-ttu-id="c7db2-115">Yük devretme sonrasında oluşturulduğunda azure sanal makineleri bu ağda yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="c7db2-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="c7db2-116">Ağın kurtarma Hizmetleri kasasıyla aynı bölgede olması gerekir</span><span class="sxs-lookup"><span data-stu-id="c7db2-116">The network should be in the same region as the Recovery Services vault</span></span>
- <span data-ttu-id="c7db2-117">Azure portalında Site Recovery ayarlanan ağlar kullanabilir [Resource Manager](../resource-manager-deployment-model.md), ya da Klasik modda.</span><span class="sxs-lookup"><span data-stu-id="c7db2-117">Site Recovery in the Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="c7db2-118">Başlamadan önce bir ağ ayarlamanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="c7db2-118">We recommend you set up a network before you begin.</span></span> <span data-ttu-id="c7db2-119">Aksi takdirde, Site Recovery dağıtımı sırasında yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c7db2-119">If you don't, you need to do it during Site Recovery deployment.</span></span>
- <span data-ttu-id="c7db2-120">Hakkında bilgi edinin [sanal ağ fiyatlandırma](https://azure.microsoft.com/pricing/details/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="c7db2-120">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="c7db2-121">Azure depolama hesabı ayarlama</span><span class="sxs-lookup"><span data-stu-id="c7db2-121">Set up an Azure storage account</span></span>

- <span data-ttu-id="c7db2-122">Site Recovery, şirket içi makineler Azure depolama alanına çoğaltır.</span><span class="sxs-lookup"><span data-stu-id="c7db2-122">Site Recovery replicates on-premises machines to Azure storage.</span></span> <span data-ttu-id="c7db2-123">Yük devretme gerçekleştikten sonra azure VM'ler depolama biriminden oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c7db2-123">Azure VMs are created from the storage after failover occurs.</span></span>
- <span data-ttu-id="c7db2-124">Standart/Premium'u ayarlama ayarlamak [Azure depolama hesabı](../storage/common/storage-create-storage-account.md#create-a-storage-account) Azure'a çoğaltılan verileri tutmak için.</span><span class="sxs-lookup"><span data-stu-id="c7db2-124">Set up a standard/premium [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) to hold data replicated to Azure.</span></span>
- <span data-ttu-id="c7db2-125">[Premium depolama](../storage/common/storage-premium-storage.md) genellikle bir tutarlı bir şekilde yüksek g/ç performans ve düşük gecikme süresi konak g/ç yoğun iş yükleri için gereken sanal makineleri için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c7db2-125">[Premium storage](../storage/common/storage-premium-storage.md) is typically used for virtual machines that need a consistently high IO performance, and low latency to host IO intensive workloads.</span></span>
- <span data-ttu-id="c7db2-126">Çoğaltılan veriler için bir premium depolama hesabı kullanmak istiyorsanız, şirket içi verilerde gerçekleşen değişiklikleri yakalayan çoğaltma günlüklerini depolamak üzere ek bir standart depolama hesabı da ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c7db2-126">If you want to use a premium account to store replicated data, you also need a standard storage account to store replication logs that capture ongoing changes to on-premises data.</span></span>
- <span data-ttu-id="c7db2-127">Kullanmak istediğiniz kaynak modeline bağlı olarak Azure vm'lerinde hesabı ayarlamanız [Resource Manager moduna](../storage/common/storage-create-storage-account.md), veya [Klasik modda](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="c7db2-127">Depending on the resource model you want to use for failed over Azure VMs, you set up an account in [Resource Manager mode](../storage/common/storage-create-storage-account.md), or [classic mode](../storage/common/storage-create-storage-account.md).</span></span>
- <span data-ttu-id="c7db2-128">Başlamadan önce bir depolama hesabı ayarlamanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="c7db2-128">We recommend that you set up a storage account before you begin.</span></span> <span data-ttu-id="c7db2-129">Bunu yapmazsanız Site Recovery dağıtımı sırasında yapmak için gerekir.</span><span class="sxs-lookup"><span data-stu-id="c7db2-129">If you don't you need to do it during Site Recovery deployment.</span></span> <span data-ttu-id="c7db2-130">Hesapları kurtarma Hizmetleri kasasıyla aynı bölgede olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c7db2-130">The accounts must be in the same region as the Recovery Services vault.</span></span>
- <span data-ttu-id="c7db2-131">Site Recovery tarafından kullanılan aynı abonelik içindeki kaynak grupları arasında veya farklı Aboneliklerdeki depolama hesaplarına taşınamıyor.</span><span class="sxs-lookup"><span data-stu-id="c7db2-131">You can't move storage accounts used by Site Recovery across resource groups within the same subscription, or across different subscriptions.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c7db2-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c7db2-132">Next steps</span></span>

<span data-ttu-id="c7db2-133">Git [6. adım: VMM hazırlama](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="c7db2-133">Go to [Step 6: Prepare VMM](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span></span>
