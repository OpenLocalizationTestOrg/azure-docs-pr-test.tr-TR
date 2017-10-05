---
title: "Azure Site Recovery Azure'u şirket içi fiziksel sunucuları çoğaltmak için Azure kaynaklarını hazırlama | Microsoft Docs"
description: "Şirket içi sunucular Azure Site Recovery hizmetini kullanarak Azure'a, çoğaltma başlamadan önce Azure yerinde gerekenler açıklanmaktadır"
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
ms.openlocfilehash: b7411fa6aba04ffd34f3f4bd03e706ca75afc9c8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="step-5-prepare-azure-resources-for-physical-server-replication-to-azure"></a><span data-ttu-id="724f0-103">5. adım: Fiziksel sunucu çoğaltma Azure Azure kaynaklarını hazırlama</span><span class="sxs-lookup"><span data-stu-id="724f0-103">Step 5: Prepare Azure resources for physical server replication to Azure</span></span>


<span data-ttu-id="724f0-104">Böylece Azure kullanarak şirket içi sunucular çoğaltabilirsiniz Azure kaynaklarını hazırlamak için bu makaledeki yönergeleri kullanın [Azure Site Recovery](site-recovery-overview.md) hizmet.</span><span class="sxs-lookup"><span data-stu-id="724f0-104">Use the instructions in this article to prepare Azure resources so that you can replicate on-premises servers to Azure using the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="724f0-105">POST açıklamaları ve soruları alt bu makalenin veya üzerinde [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="724f0-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="724f0-106">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="724f0-106">Before you start</span></span>

<span data-ttu-id="724f0-107">Okuma olduğundan emin olun [Önkoşullar](physical-walkthrough-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="724f0-107">Make sure you've read the [prerequisites](physical-walkthrough-prerequisites.md).</span></span>

## <a name="set-up-an-azure-account"></a><span data-ttu-id="724f0-108">Bir Azure hesabı ayarlama</span><span class="sxs-lookup"><span data-stu-id="724f0-108">Set up an Azure account</span></span>

- <span data-ttu-id="724f0-109">Alma bir [Microsoft Azure hesabı](http://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="724f0-109">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="724f0-110">[Ücretsiz deneme sürümüyle](https://azure.microsoft.com/pricing/free-trial/) başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="724f0-110">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="724f0-111">Site Recovery için desteklenen bölgeler altında denetleyin **coğrafi kullanılabilirlik** içinde [Azure Site Recovery fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="724f0-111">Check the supported regions for Site Recovery, under **Geographic Availability** in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="724f0-112">Hakkında bilgi edinin [Site Recovery fiyatlandırma](site-recovery-faq.md#pricing)ve alma [fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="724f0-112">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get the [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>



## <a name="set-up-an-azure-network"></a><span data-ttu-id="724f0-113">Azure ağı ayarlama</span><span class="sxs-lookup"><span data-stu-id="724f0-113">Set up an Azure network</span></span>

- <span data-ttu-id="724f0-114">Azure ağı ayarlama ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="724f0-114">Set up an Azure network.</span></span> <span data-ttu-id="724f0-115">Yük devretme sonrasında oluşturulduğunda azure sanal makineleri bu ağda yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="724f0-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="724f0-116">Azure portalında Site Recovery ayarlanan ağlar kullanabilir [Resource Manager](../resource-manager-deployment-model.md), ya da Klasik modda.</span><span class="sxs-lookup"><span data-stu-id="724f0-116">Site Recovery in the Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="724f0-117">Ağın, Kurtarma Hizmetleri kasasıyla aynı konumda olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="724f0-117">The network should be in the same region as the Recovery Services vault.</span></span>
- <span data-ttu-id="724f0-118">Hakkında bilgi edinin [sanal ağ fiyatlandırma](https://azure.microsoft.com/pricing/details/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="724f0-118">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>
- <span data-ttu-id="724f0-119">Daha fazla bilgi edinmek [Azure VM bağlantı](physical-walkthrough-network.md) yük devretme sonrasında.</span><span class="sxs-lookup"><span data-stu-id="724f0-119">Learn more about [Azure VM connectivity](physical-walkthrough-network.md) after failover.</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="724f0-120">Azure depolama hesabı ayarlama</span><span class="sxs-lookup"><span data-stu-id="724f0-120">Set up an Azure storage account</span></span>

- <span data-ttu-id="724f0-121">Site Recovery, şirket içi sunucuları Azure depolama alanına çoğaltır.</span><span class="sxs-lookup"><span data-stu-id="724f0-121">Site Recovery replicates on-premises servers to Azure storage.</span></span> <span data-ttu-id="724f0-122">Yük devretme gerçekleştikten sonra azure VM'ler depolama biriminden oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="724f0-122">Azure VMs are created from the storage after failover occurs.</span></span>
- <span data-ttu-id="724f0-123">Ayarlanmış bir [Azure depolama hesabı](../storage/common/storage-create-storage-account.md#create-a-storage-account) çoğaltılan veriler için.</span><span class="sxs-lookup"><span data-stu-id="724f0-123">Set up an [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) for replicated data.</span></span>
- <span data-ttu-id="724f0-124">Azure portalında Site Recovery Kaynak Yöneticisi'nde veya Klasik modda ayarlanmış depolama hesaplarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="724f0-124">Site Recovery in the Azure portal can use storage accounts set up in Resource Manager, or in classic mode.</span></span>
- <span data-ttu-id="724f0-125">Depolama hesabı standart olabilir veya [premium](../storage/common/storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="724f0-125">The storage account can be standard or [premium](../storage/common/storage-premium-storage.md).</span></span>
- <span data-ttu-id="724f0-126">Premium hesabınızı ayarlarsanız, ek bir standart hesap için günlük verileri gerekir.</span><span class="sxs-lookup"><span data-stu-id="724f0-126">If you set up a premium account, you will also need an additional standard account for log data.</span></span>


## <a name="next-steps"></a><span data-ttu-id="724f0-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="724f0-127">Next steps</span></span>

<span data-ttu-id="724f0-128">Git [adım 6: bir kasasını oluşturup](physical-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="724f0-128">Go to [Step 6: Set up a vault](physical-walkthrough-create-vault.md)</span></span>
