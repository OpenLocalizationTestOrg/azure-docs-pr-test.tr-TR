---
title: "Azure bölgeler arasında Azure Iaas Vm'leri aaaMigrate | Microsoft Docs"
description: "Azure Site Recovery toomigrate Azure Iaas sanal makineleri bir Azure bölgesi tooanother kullanın."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8a29e0d9-0010-4739-972f-02b8bdf360f6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: c84dc77716b8d19969eab60707ed1332ca39b893
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-azure-iaas-virtual-machines-between-azure-regions-with-azure-site-recovery"></a><span data-ttu-id="ff889-103">Azure Site Recovery ile Azure bölgeler arasında Azure Iaas sanal makineleri geçirme</span><span class="sxs-lookup"><span data-stu-id="ff889-103">Migrate Azure IaaS virtual machines between Azure regions with Azure Site Recovery</span></span>
## <a name="overview"></a><span data-ttu-id="ff889-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="ff889-104">Overview</span></span>
<span data-ttu-id="ff889-105">Site Recovery tooAzure Hoş Geldiniz!</span><span class="sxs-lookup"><span data-stu-id="ff889-105">Welcome tooAzure Site Recovery!</span></span> <span data-ttu-id="ff889-106">Bu makalede, Azure bölgeler arasında toomigrate Azure VM'ler istiyorsanız kullanın.</span><span class="sxs-lookup"><span data-stu-id="ff889-106">Use this article if you want toomigrate Azure VMs between Azure regions.</span></span> <span data-ttu-id="ff889-107">Başlamadan önce dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="ff889-107">Before you start, note that:</span></span>

* <span data-ttu-id="ff889-108">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeline sahiptir: Azure Resource Manager ve klasik.</span><span class="sxs-lookup"><span data-stu-id="ff889-108">Azure has two different deployment models for creating and working with resources: Azure Resource Manager and classic.</span></span> <span data-ttu-id="ff889-109">Ayrıca Azure iki portala – hello Klasik dağıtım modelini destekleyen Klasik Azure portalı hello ve her iki dağıtım modeline de destek Azure portal hello sahiptir.</span><span class="sxs-lookup"><span data-stu-id="ff889-109">Azure also has two portals – hello Azure classic portal that supports hello classic deployment model, and hello Azure portal with support for both deployment models.</span></span> <span data-ttu-id="ff889-110">geçiş için Kaynak Yöneticisi'nde veya Klasik Site Recovery yapılandırmakta olup olmadığını hello temel adımlar aynı hello.</span><span class="sxs-lookup"><span data-stu-id="ff889-110">hello basic steps for migration are hello same whether you're configuring Site Recovery in Resource Manager or in classic.</span></span> <span data-ttu-id="ff889-111">Ancak kullanıcı Arabirimi yönergeleri hello ve ekran görüntüleri bu makalede Azure portal hello için ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="ff889-111">However hello UI instructions and screenshots in this article are relevant for hello Azure portal.</span></span>
* <span data-ttu-id="ff889-112">**Şu anda yalnızca tek bir bölge tooanother geçirebilirsiniz. Bir Azure bölgesi tooanother VM'ler başarısız olabilir, ancak siz bunları geri yeniden kapatamazsınız.**</span><span class="sxs-lookup"><span data-stu-id="ff889-112">**Currently you can only migrate from one region tooanother. You can fail over VMs from one Azure region tooanother, but you can't fail them back again.**</span></span>

<span data-ttu-id="ff889-113">Tüm yorumlarınızı ve sorularınızı bu makalenin veya hello hello altındaki sonrası [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="ff889-113">Post any comments or questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff889-114">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ff889-114">Prerequisites</span></span>
<span data-ttu-id="ff889-115">İşte bu dağıtım için gerekenler:</span><span class="sxs-lookup"><span data-stu-id="ff889-115">Here's what you need for this deployment:</span></span>

* <span data-ttu-id="ff889-116">**Iaas sanal makineleri**: toomigrate istediğiniz sanal makineleri hello.</span><span class="sxs-lookup"><span data-stu-id="ff889-116">**IaaS virtual machines**: hello VMs you want toomigrate.</span></span> <span data-ttu-id="ff889-117">Bu sanal makineleri fiziksel makineleri düşünerek geçirin.</span><span class="sxs-lookup"><span data-stu-id="ff889-117">You migrate these VMs by treating them as physical machines.</span></span>

## <a name="deployment-steps"></a><span data-ttu-id="ff889-118">Dağıtım adımları</span><span class="sxs-lookup"><span data-stu-id="ff889-118">Deployment steps</span></span>
<span data-ttu-id="ff889-119">Bu bölümde hello yeni Azure portalında hello dağıtım adımları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ff889-119">This section describes hello deployment steps in hello new Azure portal.</span></span>

1. <span data-ttu-id="ff889-120">[Bir kasa oluşturun](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="ff889-120">[Create a vault](site-recovery-vmware-to-azure.md).</span></span>
2. <span data-ttu-id="ff889-121">[Çoğaltmayı etkinleştirme](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="ff889-121">[Enable replication](site-recovery-vmware-to-azure.md).</span></span> <span data-ttu-id="ff889-122">Merhaba toomigrate istediğiniz ve Azure kaynağı olarak seçin VM'ler çoğaltmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="ff889-122">Enable replication for hello VMs you want toomigrate, and choose Azure as source.</span></span> 
3. <span data-ttu-id="ff889-123">[Planlanmamış bir yük devretme çalıştırmak](site-recovery-failover.md).</span><span class="sxs-lookup"><span data-stu-id="ff889-123">[ Run an unplanned failover](site-recovery-failover.md).</span></span> <span data-ttu-id="ff889-124">İlk çoğaltma tamamlandıktan sonra planlanmamış bir yük devretme bir Azure bölgesi tooanother çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ff889-124">After initial replication is complete, you can run an unplanned failover from one Azure region tooanother.</span></span> <span data-ttu-id="ff889-125">İsteğe bağlı olarak, bir kurtarma planı oluşturun ve bölgeler arasında birden çok sanal makine planlanmamış yük devretme, toomigrate çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ff889-125">Optionally, you can create a recovery plan and run an unplanned failover, toomigrate multiple virtual machines between regions.</span></span> <span data-ttu-id="ff889-126">[Daha fazla bilgi edinin](site-recovery-create-recovery-plans.md) kurtarma planları hakkında.</span><span class="sxs-lookup"><span data-stu-id="ff889-126">[Learn more](site-recovery-create-recovery-plans.md) about recovery plans.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff889-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ff889-127">Next steps</span></span>
<span data-ttu-id="ff889-128">Diğer çoğaltma senaryolarda hakkında daha fazla bilgi [Azure Site Recovery nedir?](site-recovery-overview.md)</span><span class="sxs-lookup"><span data-stu-id="ff889-128">Learn more about other replication scenarios in [What is Azure Site Recovery?](site-recovery-overview.md)</span></span>
