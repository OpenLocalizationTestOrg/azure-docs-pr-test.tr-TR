---
title: "Azure bölgeler arasında Azure Vm'lerini çoğaltma | Microsoft Docs"
description: "Azure portalında Azure Site Recovery hizmeti ile Azure bölgeler arasında Azure Vm'lerini çoğaltma için gereken adımları özetler"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: 6dd36239-4363-4538-bf80-a18e71b8ec67
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: 9258613161a61e36b1d0c5796d5763c916d66859
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a><span data-ttu-id="ca014-103">Azure Site Recovery ile bölgeler arasında Azure Vm'lerini çoğaltma</span><span class="sxs-lookup"><span data-stu-id="ca014-103">Replicate Azure VMs between regions with Azure Site Recovery</span></span>

><span data-ttu-id="ca014-104">Bu makalede Azure vm'lerine farklı bir bölgede bir Azure bölgesinde Azure sanal makine (VM) çoğaltmak için gerekli olan adımları genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="ca014-104">This article provides an overview of the steps required to replicate Azure virtual machines (VMs) in one Azure region to Azure VMs in a different region.</span></span> 

>[!NOTE]
>
> <span data-ttu-id="ca014-105">Azure VM çoğaltma şu anda önizlemede değil.</span><span class="sxs-lookup"><span data-stu-id="ca014-105">Azure VM replication is currently in preview.</span></span>

<span data-ttu-id="ca014-106">Bu makalenin veya üzerinde altındaki açıklamaları ve soruları sonrası [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="ca014-106">Post comments and questions at the bottom of this article or on the [Azure Recovery Services forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="step-1-review-architecture"></a><span data-ttu-id="ca014-107">1. adım: Gözden geçirme mimarisi</span><span class="sxs-lookup"><span data-stu-id="ca014-107">Step 1: Review architecture</span></span>

<span data-ttu-id="ca014-108">Dağıtıma başlamadan önce senaryo mimarisinin ve dağıtmak için ihtiyaç duydukları bileşenleri gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="ca014-108">Before you start deployment, review the scenario architecture, and the components you need to deploy.</span></span>

<span data-ttu-id="ca014-109">Git [1. adım: mimarisi gözden geçirin](azure-to-azure-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="ca014-109">Go to [Step 1: Review the architecture](azure-to-azure-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="ca014-110">2. adım: Gözden geçirme önkoşulları</span><span class="sxs-lookup"><span data-stu-id="ca014-110">Step 2: Review prerequisites</span></span>

<span data-ttu-id="ca014-111">Abonelik, sanal ağlar, depolama hesapları ve VM gereksinimleri çeşitli yerlerde Azure önkoşulları olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="ca014-111">Check that you have the Azure prerequisites in places, including a subscription, virtual networks, storage accounts, and VM requirements.</span></span>

<span data-ttu-id="ca014-112">Git [2. adım: Önkoşullar ve sınırlamalar doğrulayın](azure-to-azure-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="ca014-112">Go to [Step 2: Verify prerequisites and limitations](azure-to-azure-walkthrough-prerequisites.md)</span></span>


## <a name="step-3-plan-networking"></a><span data-ttu-id="ca014-113">3. adım: ağ planlama</span><span class="sxs-lookup"><span data-stu-id="ca014-113">Step 3: Plan networking</span></span>

<span data-ttu-id="ca014-114">Giden bağlantı çoğaltmak istediğiniz Azure Vm'lerinde ayarlama ve şirket içi bağlantılarından ayarlanır denetleyin.</span><span class="sxs-lookup"><span data-stu-id="ca014-114">Check that outbound connectivity is set up on Azure VMs you want to replicate, and that connections from on-premises are set up.</span></span>

<span data-ttu-id="ca014-115">Git [4. adım: ağ planı](azure-to-azure-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="ca014-115">Go to [Step 4: Plan networking](azure-to-azure-walkthrough-network.md)</span></span>



## <a name="step-4-create-a-vault"></a><span data-ttu-id="ca014-116">4. adım: bir kasa oluşturma</span><span class="sxs-lookup"><span data-stu-id="ca014-116">Step 4: Create a vault</span></span> 

<span data-ttu-id="ca014-117">Düzenlemek ve çoğaltmayı yönetmek için bir kurtarma Hizmetleri kasasını oluşturup ve kaynak bölge belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ca014-117">You need to set up a Recovery Services vault to orchestrate and manage replication, and specify the source region.</span></span>

<span data-ttu-id="ca014-118">Git [4. adım: bir kasa oluşturun](azure-to-azure-walkthrough-vault.md)</span><span class="sxs-lookup"><span data-stu-id="ca014-118">Go to [Step 4: Create a vault](azure-to-azure-walkthrough-vault.md)</span></span>


## <a name="step-5-enable-replication"></a><span data-ttu-id="ca014-119">5. adım: Çoğaltma etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="ca014-119">Step 5: Enable replication</span></span>


<span data-ttu-id="ca014-120">Çoğaltmayı etkinleştirmek için hedef konum ayarları yapılandırmak, bir çoğaltma ilkesini ayarlayın ve çoğaltmak istediğiniz Azure sanal makineleri seçin.</span><span class="sxs-lookup"><span data-stu-id="ca014-120">To enable replication, you configure target location settings, set up a replication policy, and select the Azure VMs that you want to replicate.</span></span> <span data-ttu-id="ca014-121">Etkinleştirdikten sonra VM başlangıç çoğaltması gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="ca014-121">After enabling, initial replication of the VM occurs.</span></span>

<span data-ttu-id="ca014-122">Git [5. adım: çoğaltmasını etkinleştir](azure-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="ca014-122">Go to [Step 5: Enable replication](azure-to-azure-walkthrough-enable-replication.md)</span></span>


## <a name="step-6-run-a-test-failover"></a><span data-ttu-id="ca014-123">6. adım: yük devretme testi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="ca014-123">Step 6: Run a test failover</span></span>

<span data-ttu-id="ca014-124">İlk çoğaltma sonlandırıldıktan ve değişim çoğaltması çalıştıran sonra her şeyin beklendiği gibi çalıştığından emin olmak için yük devretme testi çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ca014-124">After initial replication finishes, and delta replication is running, you can run a test failover to make sure everything works as expected.</span></span>

<span data-ttu-id="ca014-125">Git [6. adım: yük devretme testi çalıştırma](azure-to-azure-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="ca014-125">Go to [Step 6: Run a test failover](azure-to-azure-walkthrough-test-failover.md)</span></span>


