---
title: "Azure Site Kurtarma'yı kullanarak Azure (System Center VMM olmadan) Hyper-V sanal makineleri çoğaltmak için Azure kaynaklarını hazırlama | Microsoft Docs"
description: "Hyper-V Vm'lerini (VMM olmadan) Azure Site RECOVERY'yi kullanarak Azure'a çoğaltma başlamadan önce Azure yerinde gerekenler açıklanmaktadır"
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
ms.openlocfilehash: 1a30cadaab7e053184f0be133f1da5bfddc1fd91
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="step-5-prepare-azure-resources-for-hyper-v-replication-to-azure"></a><span data-ttu-id="5ea6a-103">5. adım: Hyper-V çoğaltma Azure Azure kaynaklarını hazırlama</span><span class="sxs-lookup"><span data-stu-id="5ea6a-103">Step 5: Prepare Azure resources for Hyper-V replication to Azure</span></span>

<span data-ttu-id="5ea6a-104">Azure kullanarak şirket içi Hyper-V sanal makinelerini (System Center VMM olmadan) çoğaltabilirsiniz böylece Azure kaynaklarını hazırlamak için bu makaledeki yönergeleri kullanın [Azure Site Recovery](site-recovery-overview.md) hizmet.</span><span class="sxs-lookup"><span data-stu-id="5ea6a-104">Use the instructions in this article to prepare Azure resources so that you can replicate on-premises Hyper-V VMs (without System Center VMM) to Azure using the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="5ea6a-105">Bu makaleyi okuduktan sonra altındaki bir yorum gönderin ya da teknik sorular [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="5ea6a-105">After reading this article, post any comments at the bottom, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="5ea6a-106">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="5ea6a-106">Before you start</span></span>

<span data-ttu-id="5ea6a-107">Okuma olduğundan emin olun [önkoşulları](hyper-v-site-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="5ea6a-107">Make sure you've read the [prerequisites](hyper-v-site-walkthrough-prerequisites.md)</span></span>

## <a name="set-up-an-azure-account"></a><span data-ttu-id="5ea6a-108">Bir Azure hesabı ayarlama</span><span class="sxs-lookup"><span data-stu-id="5ea6a-108">Set up an Azure account</span></span>

- <span data-ttu-id="5ea6a-109">Alma bir [Microsoft Azure hesabı](http://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="5ea6a-109">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="5ea6a-110">[Ücretsiz deneme sürümüyle](https://azure.microsoft.com/pricing/free-trial/) başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ea6a-110">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="5ea6a-111">Site Recovery, altında coğrafi kullanılabilirlik kısmına desteklenen bölgeleri kontrol [Azure Site Recovery fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="5ea6a-111">Check the supported regions for Site Recovery, Under Geographic Availability in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="5ea6a-112">Hakkında bilgi edinin [Site Recovery fiyatlandırma](site-recovery-faq.md#pricing)ve alma [fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="5ea6a-112">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get the [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>


## <a name="set-up-an-azure-network"></a><span data-ttu-id="5ea6a-113">Azure ağı ayarlama</span><span class="sxs-lookup"><span data-stu-id="5ea6a-113">Set up an Azure network</span></span>

- <span data-ttu-id="5ea6a-114">Azure ağı ayarlama ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="5ea6a-114">Set up an Azure network.</span></span> <span data-ttu-id="5ea6a-115">Yük devretme sonrasında oluşturulduğunda azure sanal makineleri bu ağda yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="5ea6a-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="5ea6a-116">Ağın kurtarma Hizmetleri kasasıyla aynı bölgede olması gerekir</span><span class="sxs-lookup"><span data-stu-id="5ea6a-116">The network should be in the same region as the Recovery Services vault</span></span>
- <span data-ttu-id="5ea6a-117">Azure portalında Site Recovery ayarlanan ağlar kullanabilir [Resource Manager](../resource-manager-deployment-model.md), ya da Klasik modda.</span><span class="sxs-lookup"><span data-stu-id="5ea6a-117">Site Recovery in the Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="5ea6a-118">Başlamadan önce bir ağ ayarlamanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="5ea6a-118">We recommend you set up a network before you begin.</span></span> <span data-ttu-id="5ea6a-119">Aksi takdirde, Site Recovery dağıtımı sırasında yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5ea6a-119">If you don't, you need to do it during Site Recovery deployment.</span></span>
- <span data-ttu-id="5ea6a-120">Hakkında bilgi edinin [sanal ağ fiyatlandırma](https://azure.microsoft.com/pricing/details/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="5ea6a-120">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="5ea6a-121">Azure depolama hesabı ayarlama</span><span class="sxs-lookup"><span data-stu-id="5ea6a-121">Set up an Azure storage account</span></span>

- <span data-ttu-id="5ea6a-122">Site Recovery, şirket içi makineler Azure depolama alanına çoğaltır.</span><span class="sxs-lookup"><span data-stu-id="5ea6a-122">Site Recovery replicates on-premises machines to Azure storage.</span></span> <span data-ttu-id="5ea6a-123">Yük devretme gerçekleştikten sonra azure VM'ler depolama biriminden oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="5ea6a-123">Azure VMs are created from the storage after failover occurs.</span></span>
- <span data-ttu-id="5ea6a-124">Standart/Premium'u ayarlama ayarlamak [Azure depolama hesabı](../storage/common/storage-create-storage-account.md#create-a-storage-account) Azure'a çoğaltılan verileri tutmak için.</span><span class="sxs-lookup"><span data-stu-id="5ea6a-124">Set up a standard/premium [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) to hold data replicated to Azure.</span></span>
- <span data-ttu-id="5ea6a-125">[Premium depolama](../storage/common/storage-premium-storage.md) genellikle bir tutarlı bir şekilde yüksek g/ç performans ve düşük gecikme süresi konak g/ç yoğun iş yükleri için gereken sanal makineleri için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5ea6a-125">[Premium storage](../storage/common/storage-premium-storage.md) is typically used for virtual machines that need a consistently high IO performance, and low latency to host IO intensive workloads.</span></span>
- <span data-ttu-id="5ea6a-126">Çoğaltılan veriler için bir premium depolama hesabı kullanmak istiyorsanız, şirket içi verilerde gerçekleşen değişiklikleri yakalayan çoğaltma günlüklerini depolamak üzere ek bir standart depolama hesabı da ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5ea6a-126">If you want to use a premium account to store replicated data, you also need a standard storage account to store replication logs that capture ongoing changes to on-premises data.</span></span>
- <span data-ttu-id="5ea6a-127">Kullanmak istediğiniz kaynak modeline bağlı olarak Azure vm'lerinde hesabı ayarlamanız [Resource Manager moduna](../storage/common/storage-create-storage-account.md), veya [Klasik modda](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="5ea6a-127">Depending on the resource model you want to use for failed over Azure VMs, you set up an account in [Resource Manager mode](../storage/common/storage-create-storage-account.md), or [classic mode](../storage/common/storage-create-storage-account.md).</span></span>
- <span data-ttu-id="5ea6a-128">Başlamadan önce bir depolama hesabı ayarlamanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="5ea6a-128">We recommend that you set up a storage account before you begin.</span></span> <span data-ttu-id="5ea6a-129">Bunu yapmazsanız Site Recovery dağıtımı sırasında yapmak için gerekir.</span><span class="sxs-lookup"><span data-stu-id="5ea6a-129">If you don't you need to do it during Site Recovery deployment.</span></span> <span data-ttu-id="5ea6a-130">Hesapları kurtarma Hizmetleri kasasıyla aynı bölgede olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5ea6a-130">The accounts must be in the same region as the Recovery Services vault.</span></span>
- <span data-ttu-id="5ea6a-131">Site Recovery tarafından kullanılan aynı abonelik içindeki kaynak grupları arasında veya farklı Aboneliklerdeki depolama hesaplarına taşınamıyor.</span><span class="sxs-lookup"><span data-stu-id="5ea6a-131">You can't move storage accounts used by Site Recovery across resource groups within the same subscription, or across different subscriptions.</span></span>


## <a name="next-steps"></a><span data-ttu-id="5ea6a-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5ea6a-132">Next steps</span></span>

<span data-ttu-id="5ea6a-133">Git [adım 6: hazırlama Hyper-V kaynakları](hyper-v-site-walkthrough-prepare-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="5ea6a-133">Go to [Step 6: Prepare Hyper-V resources](hyper-v-site-walkthrough-prepare-hyper-v.md)</span></span>
