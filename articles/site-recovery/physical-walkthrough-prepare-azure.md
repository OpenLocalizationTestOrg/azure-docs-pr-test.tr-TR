---
title: "aaaPrepare Azure kaynaklarını tooreplicate şirket içi fiziksel sunucuların tooAzure Azure Site RECOVERY'yi kullanarak | Microsoft Docs"
description: "Şirket içi sunucular tooAzure, çoğaltma hello Azure Site Recovery hizmeti kullanmaya başlamadan önce Azure yerinde gerekenler açıklanmaktadır"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 4e320d9b-8bb8-46bb-ba21-77c5d16748ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/25/2017
ms.author: raynew
ms.openlocfilehash: b1d008dac278bc7797188a3c9c15f2a3b5fe12d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-prepare-azure-resources-for-physical-server-replication-tooazure"></a><span data-ttu-id="ca3b6-103">5. adım: Fiziksel sunucu çoğaltma tooAzure için Azure kaynaklarını hazırlama</span><span class="sxs-lookup"><span data-stu-id="ca3b6-103">Step 5: Prepare Azure resources for physical server replication tooAzure</span></span>


<span data-ttu-id="ca3b6-104">Bu makale tooprepare Azure Hello yönergeleri kullanın kaynakları böylece şirket içi sunucuları tooAzure hello kullanarak çoğaltabilirsiniz [Azure Site Recovery](site-recovery-overview.md) hizmet.</span><span class="sxs-lookup"><span data-stu-id="ca3b6-104">Use hello instructions in this article tooprepare Azure resources so that you can replicate on-premises servers tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="ca3b6-105">POST açıklamaları ve soruları hello altındaki bu makalenin veya hello [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="ca3b6-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="ca3b6-106">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="ca3b6-106">Before you start</span></span>

<span data-ttu-id="ca3b6-107">Emin olun hello okuma [Önkoşullar](physical-walkthrough-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="ca3b6-107">Make sure you've read hello [prerequisites](physical-walkthrough-prerequisites.md).</span></span>

## <a name="set-up-an-azure-account"></a><span data-ttu-id="ca3b6-108">Bir Azure hesabı ayarlama</span><span class="sxs-lookup"><span data-stu-id="ca3b6-108">Set up an Azure account</span></span>

- <span data-ttu-id="ca3b6-109">Alma bir [Microsoft Azure hesabı](http://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="ca3b6-109">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="ca3b6-110">[Ücretsiz deneme sürümüyle](https://azure.microsoft.com/pricing/free-trial/) başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ca3b6-110">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="ca3b6-111">Site Recovery için desteklenen hello bölgeleri altında denetleyin **coğrafi kullanılabilirlik** içinde [Azure Site Recovery fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="ca3b6-111">Check hello supported regions for Site Recovery, under **Geographic Availability** in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="ca3b6-112">Hakkında bilgi edinin [Site Recovery fiyatlandırma](site-recovery-faq.md#pricing)ve hello [fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="ca3b6-112">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get hello [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>



## <a name="set-up-an-azure-network"></a><span data-ttu-id="ca3b6-113">Azure ağı ayarlama</span><span class="sxs-lookup"><span data-stu-id="ca3b6-113">Set up an Azure network</span></span>

- <span data-ttu-id="ca3b6-114">Azure ağı ayarlama ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ca3b6-114">Set up an Azure network.</span></span> <span data-ttu-id="ca3b6-115">Yük devretme sonrasında oluşturulduğunda azure sanal makineleri bu ağda yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="ca3b6-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="ca3b6-116">Site Kurtarma'hello Azure portalı bölümünde ayarladığınız ağlar kullanabilir [Resource Manager](../resource-manager-deployment-model.md), ya da Klasik modda.</span><span class="sxs-lookup"><span data-stu-id="ca3b6-116">Site Recovery in hello Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="ca3b6-117">Merhaba ağ hello olmalıdır hello aynı bölgede kurtarma Hizmetleri kasası.</span><span class="sxs-lookup"><span data-stu-id="ca3b6-117">hello network should be in hello same region as hello Recovery Services vault.</span></span>
- <span data-ttu-id="ca3b6-118">Hakkında bilgi edinin [sanal ağ fiyatlandırma](https://azure.microsoft.com/pricing/details/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="ca3b6-118">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>
- <span data-ttu-id="ca3b6-119">Daha fazla bilgi edinmek [Azure VM bağlantı](physical-walkthrough-network.md) yük devretme sonrasında.</span><span class="sxs-lookup"><span data-stu-id="ca3b6-119">Learn more about [Azure VM connectivity](physical-walkthrough-network.md) after failover.</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="ca3b6-120">Azure depolama hesabı ayarlama</span><span class="sxs-lookup"><span data-stu-id="ca3b6-120">Set up an Azure storage account</span></span>

- <span data-ttu-id="ca3b6-121">Site Recovery, şirket içi sunucuları tooAzure depolama çoğaltır.</span><span class="sxs-lookup"><span data-stu-id="ca3b6-121">Site Recovery replicates on-premises servers tooAzure storage.</span></span> <span data-ttu-id="ca3b6-122">Yük devretme gerçekleştikten sonra azure VM'ler hello depolama biriminden oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ca3b6-122">Azure VMs are created from hello storage after failover occurs.</span></span>
- <span data-ttu-id="ca3b6-123">Ayarlanmış bir [Azure depolama hesabı](../storage/common/storage-create-storage-account.md#create-a-storage-account) çoğaltılan veriler için.</span><span class="sxs-lookup"><span data-stu-id="ca3b6-123">Set up an [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) for replicated data.</span></span>
- <span data-ttu-id="ca3b6-124">Site Kurtarma'hello Azure portal Kaynak Yöneticisi'nde veya Klasik modda ayarlanmış depolama hesaplarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ca3b6-124">Site Recovery in hello Azure portal can use storage accounts set up in Resource Manager, or in classic mode.</span></span>
- <span data-ttu-id="ca3b6-125">Merhaba depolama hesabı standart olabilir veya [premium](../storage/common/storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="ca3b6-125">hello storage account can be standard or [premium](../storage/common/storage-premium-storage.md).</span></span>
- <span data-ttu-id="ca3b6-126">Premium hesabınızı ayarlarsanız, ek bir standart hesap için günlük verileri gerekir.</span><span class="sxs-lookup"><span data-stu-id="ca3b6-126">If you set up a premium account, you will also need an additional standard account for log data.</span></span>


## <a name="next-steps"></a><span data-ttu-id="ca3b6-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ca3b6-127">Next steps</span></span>

<span data-ttu-id="ca3b6-128">Çok Git[adım 6: bir kasasını oluşturup](physical-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="ca3b6-128">Go too[Step 6: Set up a vault](physical-walkthrough-create-vault.md)</span></span>
