---
title: "Azure bölgeler arasında Azure Iaas Vm'leri geçirme | Microsoft Docs"
description: "Azure Iaas sanal makineleri bir Azure bölgesinden diğerine geçirmek için Azure Site Recovery kullanın."
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
ms.openlocfilehash: ef2972c077a2b1dd2b2fd6ce53cc6560520ea870
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="migrate-azure-iaas-virtual-machines-between-azure-regions-with-azure-site-recovery"></a><span data-ttu-id="48355-103">Azure Site Recovery ile Azure bölgeler arasında Azure Iaas sanal makineleri geçirme</span><span class="sxs-lookup"><span data-stu-id="48355-103">Migrate Azure IaaS virtual machines between Azure regions with Azure Site Recovery</span></span>
## <a name="overview"></a><span data-ttu-id="48355-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="48355-104">Overview</span></span>
<span data-ttu-id="48355-105">Azure Site Recovery'ye hoş geldiniz!</span><span class="sxs-lookup"><span data-stu-id="48355-105">Welcome to Azure Site Recovery!</span></span> <span data-ttu-id="48355-106">Azure VM'ler Azure bölgeler arasında geçirmek istiyorsanız bu makaleyi kullanın.</span><span class="sxs-lookup"><span data-stu-id="48355-106">Use this article if you want to migrate Azure VMs between Azure regions.</span></span> <span data-ttu-id="48355-107">Başlamadan önce dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="48355-107">Before you start, note that:</span></span>

* <span data-ttu-id="48355-108">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeline sahiptir: Azure Resource Manager ve klasik.</span><span class="sxs-lookup"><span data-stu-id="48355-108">Azure has two different deployment models for creating and working with resources: Azure Resource Manager and classic.</span></span> <span data-ttu-id="48355-109">Ayrıca Azure iki portala sahiptir: Klasik dağıtım modelini destekleyen klasik Azure portalı ve her iki dağıtım modeline de destek sağlayan Azure portalı.</span><span class="sxs-lookup"><span data-stu-id="48355-109">Azure also has two portals – the Azure classic portal that supports the classic deployment model, and the Azure portal with support for both deployment models.</span></span> <span data-ttu-id="48355-110">Site Recovery Kaynak Yöneticisi'nde veya Klasik yapılandırmakta olup olmadığını geçiş için temel adımlar aynıdır.</span><span class="sxs-lookup"><span data-stu-id="48355-110">The basic steps for migration are the same whether you're configuring Site Recovery in Resource Manager or in classic.</span></span> <span data-ttu-id="48355-111">Ancak kullanıcı Arabirimi yönergeleri ve ekran görüntüleri bu makalede Azure portal ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="48355-111">However the UI instructions and screenshots in this article are relevant for the Azure portal.</span></span>
* <span data-ttu-id="48355-112">**Şu anda yalnızca bir bölgesinden diğerine geçirebilirsiniz. Bir Azure bölgesinden Vm'lere devredebildiğini, ancak siz bunları geri yeniden kapatamazsınız.**</span><span class="sxs-lookup"><span data-stu-id="48355-112">**Currently you can only migrate from one region to another. You can fail over VMs from one Azure region to another, but you can't fail them back again.**</span></span>

<span data-ttu-id="48355-113">Tüm yorumlarınızı ve sorularınızı bu makalenin alt kısmında veya [Azure Kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)'nda paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48355-113">Post any comments or questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="48355-114">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="48355-114">Prerequisites</span></span>
<span data-ttu-id="48355-115">İşte bu dağıtım için gerekenler:</span><span class="sxs-lookup"><span data-stu-id="48355-115">Here's what you need for this deployment:</span></span>

* <span data-ttu-id="48355-116">**Iaas sanal makineleri**: geçiş yapmak istediğiniz sanal makineleri.</span><span class="sxs-lookup"><span data-stu-id="48355-116">**IaaS virtual machines**: The VMs you want to migrate.</span></span> <span data-ttu-id="48355-117">Bu sanal makineleri fiziksel makineleri düşünerek geçirin.</span><span class="sxs-lookup"><span data-stu-id="48355-117">You migrate these VMs by treating them as physical machines.</span></span>

## <a name="deployment-steps"></a><span data-ttu-id="48355-118">Dağıtım adımları</span><span class="sxs-lookup"><span data-stu-id="48355-118">Deployment steps</span></span>
<span data-ttu-id="48355-119">Bu bölümde, yeni Azure portalında dağıtım adımları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="48355-119">This section describes the deployment steps in the new Azure portal.</span></span>

1. <span data-ttu-id="48355-120">[Bir kasa oluşturun](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="48355-120">[Create a vault](site-recovery-vmware-to-azure.md).</span></span>
2. <span data-ttu-id="48355-121">[Çoğaltmayı etkinleştirme](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="48355-121">[Enable replication](site-recovery-vmware-to-azure.md).</span></span> <span data-ttu-id="48355-122">Geçirmek istediğiniz VM'ler için çoğaltmayı etkinleştirmek ve Azure kaynağı olarak seçin.</span><span class="sxs-lookup"><span data-stu-id="48355-122">Enable replication for the VMs you want to migrate, and choose Azure as source.</span></span> 
3. <span data-ttu-id="48355-123">[Planlanmamış bir yük devretme çalıştırmak](site-recovery-failover.md).</span><span class="sxs-lookup"><span data-stu-id="48355-123">[ Run an unplanned failover](site-recovery-failover.md).</span></span> <span data-ttu-id="48355-124">İlk çoğaltma tamamlandıktan sonra planlanmamış bir yük devretme bir Azure bölgesinden diğerine çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48355-124">After initial replication is complete, you can run an unplanned failover from one Azure region to another.</span></span> <span data-ttu-id="48355-125">İsteğe bağlı olarak, bir kurtarma planı oluşturmak ve birden çok sanal makine bölgeler arasında geçirmek için planlanmamış yük devretme, çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="48355-125">Optionally, you can create a recovery plan and run an unplanned failover, to migrate multiple virtual machines between regions.</span></span> <span data-ttu-id="48355-126">[Daha fazla bilgi edinin](site-recovery-create-recovery-plans.md) kurtarma planları hakkında.</span><span class="sxs-lookup"><span data-stu-id="48355-126">[Learn more](site-recovery-create-recovery-plans.md) about recovery plans.</span></span>

## <a name="next-steps"></a><span data-ttu-id="48355-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="48355-127">Next steps</span></span>
<span data-ttu-id="48355-128">Diğer çoğaltma senaryolarda hakkında daha fazla bilgi [Azure Site Recovery nedir?](site-recovery-overview.md)</span><span class="sxs-lookup"><span data-stu-id="48355-128">Learn more about other replication scenarios in [What is Azure Site Recovery?](site-recovery-overview.md)</span></span>
