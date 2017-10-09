---
title: "Merhaba kaynak ve hedef Azure Site Recovery ile Hyper-V çoğaltma tooAzure (System Center VMM olmadan) için yukarı aaaSet | Microsoft Docs"
description: "Azure Site Recovery ile Hyper-V sanal makineleri tooAzure depolama çoğaltma için kaynak ve hedef ayarlarını Hello adımları tooset özetler"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d2010d85-77fd-4dea-84f3-1c960ed4c63f
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 105b90e6ac053d5b842c54a36c460a26d0f5c2ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-hyper-v-replication-tooazure"></a><span data-ttu-id="cceb4-103">8. adım: hello kaynak ve hedef Hyper-V çoğaltma tooAzure için ayarlama</span><span class="sxs-lookup"><span data-stu-id="cceb4-103">Step 8: Set up hello source and target for Hyper-V replication tooAzure</span></span>

<span data-ttu-id="cceb4-104">Bu makalede nasıl çoğaltırken tooconfigure kaynak ve hedef ayarları şirket içi Hyper-V sanal makineleri (System Center VMM olmadan) tooAzure hello kullanarak [Azure Site Recovery](site-recovery-overview.md) hello Azure portal hizmeti.</span><span class="sxs-lookup"><span data-stu-id="cceb4-104">This article describes how tooconfigure source and target settings when replicating on-premises Hyper-V virtual machines (without System Center VMM) tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="cceb4-105">POST açıklamaları ve soruları hello altındaki bu makalenin veya hello [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="cceb4-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-hello-source-environment"></a><span data-ttu-id="cceb4-106">Merhaba kaynak ortamını ayarlama</span><span class="sxs-lookup"><span data-stu-id="cceb4-106">Set up hello source environment</span></span>

<span data-ttu-id="cceb4-107">Merhaba Hyper-V sitesini kurmak, hello Azure Site Recovery sağlayıcısı ve hello Azure kurtarma Hizmetleri aracısını Hyper-V ana bilgisayarlarına yükleyin ve hello site hello kasaya kaydetmek.</span><span class="sxs-lookup"><span data-stu-id="cceb4-107">Set up hello Hyper-V site, install hello Azure Site Recovery Provider and hello Azure Recovery Services agent on Hyper-V hosts, and register hello site in hello vault.</span></span>

1. <span data-ttu-id="cceb4-108">İçinde **altyapıyı hazırlama**, tıklatın **kaynak**.</span><span class="sxs-lookup"><span data-stu-id="cceb4-108">In **Prepare Infrastructure**, click **Source**.</span></span> <span data-ttu-id="cceb4-109">Hyper-V konakları veya kümeleri için kapsayıcı olarak yeni bir Hyper-V sitesi tooadd tıklatın **+ Hyper-V sitesi**.</span><span class="sxs-lookup"><span data-stu-id="cceb4-109">tooadd a new Hyper-V site as a container for your Hyper-V hosts or clusters, click **+Hyper-V Site**.</span></span>

    ![Kaynağı ayarlama](./media/hyper-v-site-walkthrough-source-target/set-source1.png)
2. <span data-ttu-id="cceb4-111">İçinde **oluşturma Hyper-V sitesi**, başlangıç sitesi için bir ad belirtin.</span><span class="sxs-lookup"><span data-stu-id="cceb4-111">In **Create Hyper-V site**, specify a name for hello site.</span></span> <span data-ttu-id="cceb4-112">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cceb4-112">Then click **OK**.</span></span> <span data-ttu-id="cceb4-113">Şimdi, oluşturduğunuz ve tıklatın hello siteyi seçin **+ Hyper-V Server** tooadd server toohello sitesi.</span><span class="sxs-lookup"><span data-stu-id="cceb4-113">Now, select hello site you created, and click **+Hyper-V Server** tooadd a server toohello site.</span></span>

    ![Kaynağı ayarlama](./media/hyper-v-site-walkthrough-source-target/set-source2.png)

3. <span data-ttu-id="cceb4-115">İçinde **Sunucu Ekle** > **sunucu türü**, denetleyin **Hyper-V server** görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="cceb4-115">In **Add Server** > **Server type**, check that **Hyper-V server** is displayed.</span></span>

    - <span data-ttu-id="cceb4-116">İstediğiniz tooadd hello ile uyumlu hello Hyper-V sunucu emin olun [Önkoşullar](#on-premises-prerequisites), ve olduğu mümkün tooaccess hello belirtilen URL'leri.</span><span class="sxs-lookup"><span data-stu-id="cceb4-116">Make sure that hello Hyper-V server you want tooadd complies with hello [prerequisites](#on-premises-prerequisites), and is able tooaccess hello specified URLs.</span></span>
    - <span data-ttu-id="cceb4-117">Hello Azure Site Recovery sağlayıcısı yükleme dosyasını indirin.</span><span class="sxs-lookup"><span data-stu-id="cceb4-117">Download hello Azure Site Recovery Provider installation file.</span></span> <span data-ttu-id="cceb4-118">Bu dosya tooinstall hello sağlayıcısı çalıştırın ve her Hyper-V ana kurtarma Hizmetleri aracısını hello.</span><span class="sxs-lookup"><span data-stu-id="cceb4-118">You run this file tooinstall hello Provider and hello Recovery Services agent on each Hyper-V host.</span></span>

    ![Kaynağı ayarlama](./media/hyper-v-site-walkthrough-source-target/set-source3.png)


## <a name="install-hello-provider-and-agent"></a><span data-ttu-id="cceb4-120">Merhaba sağlayıcı ve aracı yükleme</span><span class="sxs-lookup"><span data-stu-id="cceb4-120">Install hello Provider and agent</span></span>

1. <span data-ttu-id="cceb4-121">Her ana bilgisayarda Hello sağlayıcı kurulum dosyasını çalıştırın toohello Hyper-V sitesi eklendi.</span><span class="sxs-lookup"><span data-stu-id="cceb4-121">Run hello Provider setup file on each host you added toohello Hyper-V site.</span></span> <span data-ttu-id="cceb4-122">Hyper-V kümesi üzerinde yüklüyorsanız, her küme düğümünde Kurulumu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="cceb4-122">If you're installing on a Hyper-V cluster, run setup on each cluster node.</span></span> <span data-ttu-id="cceb4-123">Düğümleri arasında geçirmek olsa bile yükleme ve her Hyper-V küme düğümü kaydetme VM'ler korunduğunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="cceb4-123">Installing and registering each Hyper-V cluster node ensures that VMs are protected, even if they migrate across nodes.</span></span>
2. <span data-ttu-id="cceb4-124">**Microsoft Update** kısmından güncelleştirmeleri seçebilirsiniz. Böylece, Sağlayıcı güncelleştirmeleri Microsoft Update ilkenize uygun şekilde yüklenir.</span><span class="sxs-lookup"><span data-stu-id="cceb4-124">In **Microsoft Update**, you can opt in for updates so that Provider updates are installed in accordance with your Microsoft Update policy.</span></span>
3. <span data-ttu-id="cceb4-125">İçinde **yükleme**, kabul etmek veya hello varsayılan sağlayıcı yükleme konumunu değiştirmek ve tıklatın **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="cceb4-125">In **Installation**, accept or modify hello default Provider installation location and click **Install**.</span></span>
4. <span data-ttu-id="cceb4-126">İçinde **kasa ayarlarını**, tıklatın **Gözat** indirdiğiniz tooselect hello kasa anahtarı dosyasını.</span><span class="sxs-lookup"><span data-stu-id="cceb4-126">In **Vault Settings**, click **Browse** tooselect hello vault key file that you downloaded.</span></span> <span data-ttu-id="cceb4-127">Hello Azure Site Recovery abonelik hello kasa adı belirtin ve hello Hyper-V site toowhich hello Hyper-V sunucusuna ait.</span><span class="sxs-lookup"><span data-stu-id="cceb4-127">Specify hello Azure Site Recovery subscription, hello vault name, and hello Hyper-V site toowhich hello Hyper-V server belongs.</span></span>

    ![Sunucu kaydı](./media/hyper-v-site-walkthrough-source-target/provider3.png)

5. <span data-ttu-id="cceb4-129">İçinde **Proxy ayarlarını**, Hyper-V konakları üzerinde çalışan sağlayıcı üzerinden Site Recovery tooAzure bağlanır hello hello Internet nasıl belirtin.</span><span class="sxs-lookup"><span data-stu-id="cceb4-129">In **Proxy Settings**, specify how hello Provider running on Hyper-V hosts connects tooAzure Site Recovery over hello internet.</span></span>

    * <span data-ttu-id="cceb4-130">Merhaba sağlayıcısı tooconnect doğrudan select istiyorsanız **tooAzure Site Recovery Ara sunucu olmadan doğrudan bağlan**.</span><span class="sxs-lookup"><span data-stu-id="cceb4-130">If you want hello Provider tooconnect directly select **Connect directly tooAzure Site Recovery without a proxy**.</span></span>
    * <span data-ttu-id="cceb4-131">Var olan ara sunucunuz kimlik doğrulaması gerektiren veya hello sağlayıcı bağlantısı için özel bir ara sunucu toouse istiyorsanız, seçin **tooAzure Site kurtarma proxy sunucusu kullanarak bağlanmak**.</span><span class="sxs-lookup"><span data-stu-id="cceb4-131">If your existing proxy requires authentication, or you want toouse a custom proxy for hello Provider connection, select **Connect tooAzure Site Recovery using a proxy server**.</span></span>
    * <span data-ttu-id="cceb4-132">Bir proxy sunucu kullanıyorsanız:</span><span class="sxs-lookup"><span data-stu-id="cceb4-132">If you use a proxy:</span></span>
        - <span data-ttu-id="cceb4-133">Başlangıç adresi, bağlantı noktası ve kimlik bilgilerini belirtin</span><span class="sxs-lookup"><span data-stu-id="cceb4-133">Specify hello address, port, and credentials</span></span>
        - <span data-ttu-id="cceb4-134">Hello açıklanan emin hello URL'leri olun [Önkoşullar](#prerequisites) hello proxy üzerinden izin verilir.</span><span class="sxs-lookup"><span data-stu-id="cceb4-134">Make sure hello URLs described in hello [prerequisites](#prerequisites) are allowed through hello proxy.</span></span>

    ![internet](./media/hyper-v-site-walkthrough-source-target/provider7.png)

6. <span data-ttu-id="cceb4-136">Yükleme tamamlandıktan sonra tıklatın **kaydetmek** hello kasadaki tooregister hello sunucu.</span><span class="sxs-lookup"><span data-stu-id="cceb4-136">After installation finishes, click **Register** tooregister hello server in hello vault.</span></span>

    ![Yükleme konumu](./media/hyper-v-site-walkthrough-source-target/provider2.png)

7. <span data-ttu-id="cceb4-138">Kayıt tamamlandıktan sonra hello Hyper-V sunucusundan meta veriler, Azure Site Recovery tarafından alınır ve hello sunucu görüntülenir **Site Recovery altyapısı** > **Hyper-V konakları**.</span><span class="sxs-lookup"><span data-stu-id="cceb4-138">After registration finishes, metadata from hello Hyper-V server is retrieved by Azure Site Recovery, and hello server is displayed in **Site Recovery Infrastructure** > **Hyper-V Hosts**.</span></span>


## <a name="set-up-hello-target-environment"></a><span data-ttu-id="cceb4-139">Merhaba hedef ortamını ayarlama</span><span class="sxs-lookup"><span data-stu-id="cceb4-139">Set up hello target environment</span></span>

<span data-ttu-id="cceb4-140">Çoğaltma için Hello Azure depolama hesabı belirtin ve hello Azure ağ toowhich Azure Vm'lerinin yük devretme sonrasında bağlanır.</span><span class="sxs-lookup"><span data-stu-id="cceb4-140">Specify hello Azure storage account for replication, and hello Azure network toowhich Azure VMs will connect after failover.</span></span>

1. <span data-ttu-id="cceb4-141">Tıklatın **altyapıyı hazırlama** > **hedef**.</span><span class="sxs-lookup"><span data-stu-id="cceb4-141">Click **Prepare infrastructure** > **Target**.</span></span>
2. <span data-ttu-id="cceb4-142">Merhaba abonelik ve yük devretme sonrasında toocreate hello Azure VM'ler istediğiniz hello kaynak grubunu seçin.</span><span class="sxs-lookup"><span data-stu-id="cceb4-142">Select hello subscription and hello resource group in which you want toocreate hello Azure VMs after failover.</span></span> <span data-ttu-id="cceb4-143">Merhaba dağıtımı seçin model toouse (Klasik veya resource management) azure'da hello VM'ler istiyor.</span><span class="sxs-lookup"><span data-stu-id="cceb4-143">Choose hello deployment model that you want toouse in Azure (classic or resource management) for hello VMs.</span></span>

3. <span data-ttu-id="cceb4-144">Site Recovery, bir veya birden çok uyumlu Azure depolama hesabınızın ve ağınızın olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="cceb4-144">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

    - <span data-ttu-id="cceb4-145">Bir depolama hesabınız yoksa tıklatın **+ depolama** toocreate bir Resource Manager tabanlı hesap satır içi.</span><span class="sxs-lookup"><span data-stu-id="cceb4-145">If you don't have a storage account, click **+Storage** toocreate a Resource Manager-based account inline.</span></span> 
    - <span data-ttu-id="cceb4-146">Bir Azure ağı yoksa tıklatın **+ ağ** toocreate bir Resource Manager tabanlı ağ satır içi.</span><span class="sxs-lookup"><span data-stu-id="cceb4-146">If you don't have a Azure network, click **+Network** toocreate a Resource Manager-based network inline.</span></span>






## <a name="next-steps"></a><span data-ttu-id="cceb4-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cceb4-147">Next steps</span></span>

<span data-ttu-id="cceb4-148">Çok Git[adım 9: bir çoğaltma ilkesini ayarlayın](hyper-v-site-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="cceb4-148">Go too[Step 9: Set up a replication policy](hyper-v-site-walkthrough-replication.md)</span></span>
