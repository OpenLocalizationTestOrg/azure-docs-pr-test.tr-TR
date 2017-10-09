---
title: "Merhaba kaynak ve hedef Azure Site Recovery ile fiziksel sunucu çoğaltma tooAzure için aaaSet | Microsoft Docs"
description: "Merhaba adımları tooset hello Azure Site Recovery hizmeti ile fiziksel sunucuları tooAzure depolama çoğaltma için kaynak ve hedef ayarlarını özetler"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 2e3d03bc-4e53-4590-8a01-f702d3cc9500
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: e75ef23174d77509bf54380eba8f251a7337a45f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-hello-source-and-target-for-physical-server-replication-tooazure"></a><span data-ttu-id="0688e-103">7. adım: hello kaynak ve hedef fiziksel sunucu çoğaltma tooAzure için ayarlama</span><span class="sxs-lookup"><span data-stu-id="0688e-103">Step 7: Set up hello source and target for physical server replication tooAzure</span></span>

<span data-ttu-id="0688e-104">Bu makalede nasıl çoğaltırken tooconfigure kaynak ve hedef ayarları şirket içi fiziksel sunucuların tooAzure hello kullanarak [Azure Site Recovery](site-recovery-overview.md) hello Azure portal hizmeti.</span><span class="sxs-lookup"><span data-stu-id="0688e-104">This article describes how tooconfigure source and target settings when replicating on-premises physical servers tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="0688e-105">POST açıklamaları ve soruları hello altındaki bu makalenin veya hello [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="0688e-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-hello-source-environment"></a><span data-ttu-id="0688e-106">Merhaba kaynak ortamını ayarlama</span><span class="sxs-lookup"><span data-stu-id="0688e-106">Set up hello source environment</span></span>

<span data-ttu-id="0688e-107">Merhaba yapılandırma sunucusunu ayarlamayı, hello kasaya kaydetmek ve makineleri Bul</span><span class="sxs-lookup"><span data-stu-id="0688e-107">Set up hello configuration server, register it in hello vault, and discover machines.</span></span>

1. <span data-ttu-id="0688e-108">Tıklatın **Site kurtarma** > **1. adım: altyapıyı hazırlama** > **kaynak**.</span><span class="sxs-lookup"><span data-stu-id="0688e-108">Click **Site Recovery** > **Step 1: Prepare Infrastructure** > **Source**.</span></span>
2. <span data-ttu-id="0688e-109">Yapılandırma sunucusu yoksa, tıklatın **+ yapılandırma sunucusu**.</span><span class="sxs-lookup"><span data-stu-id="0688e-109">If you don’t have a configuration server, click **+Configuration server**.</span></span>
3. <span data-ttu-id="0688e-110">İçinde **Sunucu Ekle**, denetleyin **yapılandırma sunucusu** görünür **sunucu türü**.</span><span class="sxs-lookup"><span data-stu-id="0688e-110">In **Add Server**, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="0688e-111">Merhaba Site Recovery birleşik Kurulumu yükleme dosyasını indirin.</span><span class="sxs-lookup"><span data-stu-id="0688e-111">Download hello Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="0688e-112">Merhaba kasa kayıt anahtarını indirin.</span><span class="sxs-lookup"><span data-stu-id="0688e-112">Download hello vault registration key.</span></span> <span data-ttu-id="0688e-113">Birleşik Kurulum'u çalıştırdığınızda bu gerekir.</span><span class="sxs-lookup"><span data-stu-id="0688e-113">You need this when you run Unified Setup.</span></span> <span data-ttu-id="0688e-114">Merhaba anahtar, oluşturulduktan sonra beş gün boyunca geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="0688e-114">hello key is valid for five days after you generate it.</span></span>

   ![Kaynağı ayarlama](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-hello-configuration-server-in-hello-vault"></a><span data-ttu-id="0688e-116">Merhaba kasasına Hello yapılandırma sunucusuna kaydedin</span><span class="sxs-lookup"><span data-stu-id="0688e-116">Register hello configuration server in hello vault</span></span>

<span data-ttu-id="0688e-117">, Önce hello aşağıdaki başlayın, ardından birleşik Kurulum tooinstall hello yapılandırma sunucusu, hello işlem sunucusu ve hello ana hedef sunucusunda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="0688e-117">Do hello following before you start, then run Unified Setup tooinstall hello configuration server, hello process server, and hello master target server.</span></span> <span data-ttu-id="0688e-118">Merhaba video hello bileşenleri VMware VM tooAzure çoğaltma için kurulacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="0688e-118">hello video describes setting up hello components for VMware VM tooAzure replication.</span></span> <span data-ttu-id="0688e-119">Ancak, hello aynı işlem fiziksel sunucu tooAzure çoğaltma için geçerli değil.</span><span class="sxs-lookup"><span data-stu-id="0688e-119">However, hello same process is valid for physical server tooAzure replication.</span></span>

- <span data-ttu-id="0688e-120">Merhaba yapılandırma sunucusunda VM, o hello sistem saati ile eşitlenir emin olun bir [saat sunucusu](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span><span class="sxs-lookup"><span data-stu-id="0688e-120">On hello configuration server VM, make sure that hello system clock is synchronized with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span></span> <span data-ttu-id="0688e-121">Eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="0688e-121">It should match.</span></span> <span data-ttu-id="0688e-122">Önde 15 dakika ise veya arkasında kurulum başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="0688e-122">If it's 15 minutes in front or behind, setup might fail.</span></span>
- <span data-ttu-id="0688e-123">Kurulum hello configuration server makinesinde yerel yönetici olarak çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="0688e-123">Run setup as a Local Administrator on hello configuration server machine.</span></span>
- <span data-ttu-id="0688e-124">TLS 1.0 hello VM etkin olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="0688e-124">Make sure TLS 1.0 is enabled on hello VM.</span></span>


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="0688e-125">Merhaba yapılandırma sunucusu da yüklenebilir [hello komut satırından](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="0688e-125">hello configuration server can also be installed [from hello command line](http://aka.ms/installconfigsrv).</span></span>




## <a name="set-up-hello-target-environment"></a><span data-ttu-id="0688e-126">Merhaba hedef ortamını ayarlama</span><span class="sxs-lookup"><span data-stu-id="0688e-126">Set up hello target environment</span></span>

<span data-ttu-id="0688e-127">Merhaba hedef ortamını ayarlama önce bir Azure depolama hesabı ve sanal ağ kurulumu olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="0688e-127">Before you set up hello target environment, make sure you have an Azure storage account and virtual network set up.</span></span>

1. <span data-ttu-id="0688e-128">Tıklatın **altyapıyı hazırlama** > **hedef**, ve hello toouse istediğiniz Azure aboneliğini seçin.</span><span class="sxs-lookup"><span data-stu-id="0688e-128">Click **Prepare infrastructure** > **Target**, and select hello Azure subscription you want toouse.</span></span>
2. <span data-ttu-id="0688e-129">Belirtin, hedef dağıtım modeli Resource Manager tabanlı veya Klasik olup.</span><span class="sxs-lookup"><span data-stu-id="0688e-129">Specify whether your target deployment model is Resource Manager-based, or classic.</span></span>
3. <span data-ttu-id="0688e-130">Site Recovery, bir veya birden çok uyumlu Azure depolama hesabınızın ve ağınızın olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="0688e-130">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

   ![Hedef](./media/physical-walkthrough-source-target/gs-target.png)

4. <span data-ttu-id="0688e-132">Bir depolama hesabı veya ağı oluşturmadıysanız, tıklatın **+ depolama hesabı** veya **+ ağ**, toocreate bir Resource Manager hesabı ya da ağ satır içi.</span><span class="sxs-lookup"><span data-stu-id="0688e-132">If you haven't created a storage account or network, click **+Storage account** or **+Network**, toocreate a Resource Manager account or network inline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0688e-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0688e-133">Next steps</span></span>

<span data-ttu-id="0688e-134">Çok Git[adım 8: bir çoğaltma ilkesini ayarlayın](physical-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="0688e-134">Go too[Step 8: Set up a replication policy](physical-walkthrough-replication.md)</span></span>
