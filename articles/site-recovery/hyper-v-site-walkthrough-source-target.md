---
title: "Kaynak ve hedef Hyper-V çoğaltma Azure Site Recovery ile Azure'a (System Center VMM olmadan) için ayarlama | Microsoft Docs"
description: "Hyper-V sanal makineleri çoğaltma Azure Site Recovery ile Azure depolama için kaynak ve hedef ayarları ayarlamak için adımları özetler"
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
ms.openlocfilehash: b38eb3a011d46f2239891ea1d1bcac2a4059a866
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="step-8-set-up-the-source-and-target-for-hyper-v-replication-to-azure"></a><span data-ttu-id="c976a-103">8. adım: kaynak ve hedef Hyper-V çoğaltma Azure için ayarlayın</span><span class="sxs-lookup"><span data-stu-id="c976a-103">Step 8: Set up the source and target for Hyper-V replication to Azure</span></span>

<span data-ttu-id="c976a-104">Bu makalede çoğaltma azure'a, Hyper-V sanal makineleri (System Center VMM olmadan) şirket içi, kaynak ve hedef ayarlarının nasıl yapılandırılacağı kullanarak [Azure Site Recovery](site-recovery-overview.md) Azure portalında hizmet.</span><span class="sxs-lookup"><span data-stu-id="c976a-104">This article describes how to configure source and target settings when replicating on-premises Hyper-V virtual machines (without System Center VMM) to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="c976a-105">POST açıklamaları ve soruları alt bu makalenin veya üzerinde [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="c976a-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-the-source-environment"></a><span data-ttu-id="c976a-106">Kaynak ortamı ayarlama</span><span class="sxs-lookup"><span data-stu-id="c976a-106">Set up the source environment</span></span>

<span data-ttu-id="c976a-107">Hyper-V sitesini kurmak, Azure Site kurtarma Sağlayıcısı'nı ve Azure kurtarma Hizmetleri aracısını Hyper-V ana bilgisayarlarına yükleyin ve site kasaya kaydetmek.</span><span class="sxs-lookup"><span data-stu-id="c976a-107">Set up the Hyper-V site, install the Azure Site Recovery Provider and the Azure Recovery Services agent on Hyper-V hosts, and register the site in the vault.</span></span>

1. <span data-ttu-id="c976a-108">İçinde **altyapıyı hazırlama**, tıklatın **kaynak**.</span><span class="sxs-lookup"><span data-stu-id="c976a-108">In **Prepare Infrastructure**, click **Source**.</span></span> <span data-ttu-id="c976a-109">Hyper-V konakları veya kümeleri için yeni bir Hyper-V sitesi bir kapsayıcı olarak eklemek için tıklatın **+ Hyper-V sitesi**.</span><span class="sxs-lookup"><span data-stu-id="c976a-109">To add a new Hyper-V site as a container for your Hyper-V hosts or clusters, click **+Hyper-V Site**.</span></span>

    ![Kaynağı ayarlama](./media/hyper-v-site-walkthrough-source-target/set-source1.png)
2. <span data-ttu-id="c976a-111">İçinde **oluşturma Hyper-V sitesi**, site için bir ad belirtin.</span><span class="sxs-lookup"><span data-stu-id="c976a-111">In **Create Hyper-V site**, specify a name for the site.</span></span> <span data-ttu-id="c976a-112">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c976a-112">Then click **OK**.</span></span> <span data-ttu-id="c976a-113">Şimdi, oluşturduğunuz ve tıklatın siteyi seçin **+ Hyper-V Server** siteye bir sunucu ekleme.</span><span class="sxs-lookup"><span data-stu-id="c976a-113">Now, select the site you created, and click **+Hyper-V Server** to add a server to the site.</span></span>

    ![Kaynağı ayarlama](./media/hyper-v-site-walkthrough-source-target/set-source2.png)

3. <span data-ttu-id="c976a-115">İçinde **Sunucu Ekle** > **sunucu türü**, denetleyin **Hyper-V server** görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="c976a-115">In **Add Server** > **Server type**, check that **Hyper-V server** is displayed.</span></span>

    - <span data-ttu-id="c976a-116">Eklemek istediğiniz Hyper-V server ile uyumlu olduğundan emin olun [Önkoşullar](#on-premises-prerequisites)ve belirtilen URL'leri erişebilir.</span><span class="sxs-lookup"><span data-stu-id="c976a-116">Make sure that the Hyper-V server you want to add complies with the [prerequisites](#on-premises-prerequisites), and is able to access the specified URLs.</span></span>
    - <span data-ttu-id="c976a-117">Azure Site Recovery Sağlayıcısı yükleme dosyasını indirin.</span><span class="sxs-lookup"><span data-stu-id="c976a-117">Download the Azure Site Recovery Provider installation file.</span></span> <span data-ttu-id="c976a-118">Her Hyper-V ana bilgisayarda sağlayıcı ve kurtarma Hizmetleri Aracısı'nı yüklemek için bu dosyayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="c976a-118">You run this file to install the Provider and the Recovery Services agent on each Hyper-V host.</span></span>

    ![Kaynağı ayarlama](./media/hyper-v-site-walkthrough-source-target/set-source3.png)


## <a name="install-the-provider-and-agent"></a><span data-ttu-id="c976a-120">Sağlayıcı ve aracı yükleme</span><span class="sxs-lookup"><span data-stu-id="c976a-120">Install the Provider and agent</span></span>

1. <span data-ttu-id="c976a-121">Sağlayıcıyı Hyper-V siteye eklenen her ana bilgisayarda kurulum dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="c976a-121">Run the Provider setup file on each host you added to the Hyper-V site.</span></span> <span data-ttu-id="c976a-122">Hyper-V kümesi üzerinde yüklüyorsanız, her küme düğümünde Kurulumu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="c976a-122">If you're installing on a Hyper-V cluster, run setup on each cluster node.</span></span> <span data-ttu-id="c976a-123">Düğümleri arasında geçirmek olsa bile yükleme ve her Hyper-V küme düğümü kaydetme VM'ler korunduğunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="c976a-123">Installing and registering each Hyper-V cluster node ensures that VMs are protected, even if they migrate across nodes.</span></span>
2. <span data-ttu-id="c976a-124">**Microsoft Update** kısmından güncelleştirmeleri seçebilirsiniz. Böylece, Sağlayıcı güncelleştirmeleri Microsoft Update ilkenize uygun şekilde yüklenir.</span><span class="sxs-lookup"><span data-stu-id="c976a-124">In **Microsoft Update**, you can opt in for updates so that Provider updates are installed in accordance with your Microsoft Update policy.</span></span>
3. <span data-ttu-id="c976a-125">**Yükleme** bölümünde varsayılan Sağlayıcı yükleme konumunu kabul edin veya değiştirin ve **Yükle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c976a-125">In **Installation**, accept or modify the default Provider installation location and click **Install**.</span></span>
4. <span data-ttu-id="c976a-126">İçinde **kasa ayarlarını**, tıklatın **Gözat** indirdiğiniz kasa anahtarı dosyasını seçin.</span><span class="sxs-lookup"><span data-stu-id="c976a-126">In **Vault Settings**, click **Browse** to select the vault key file that you downloaded.</span></span> <span data-ttu-id="c976a-127">Azure Site Recovery abonelik, kasa adını ve Hyper-V sunucusuna ait olduğu Hyper-V sitesi belirtin.</span><span class="sxs-lookup"><span data-stu-id="c976a-127">Specify the Azure Site Recovery subscription, the vault name, and the Hyper-V site to which the Hyper-V server belongs.</span></span>

    ![Sunucu kaydı](./media/hyper-v-site-walkthrough-source-target/provider3.png)

5. <span data-ttu-id="c976a-129">İçinde **Proxy ayarlarını**, Hyper-V konakları üzerinde çalışan sağlayıcının Azure Site Recovery için Internet üzerinden nasıl bağlandığını belirtin.</span><span class="sxs-lookup"><span data-stu-id="c976a-129">In **Proxy Settings**, specify how the Provider running on Hyper-V hosts connects to Azure Site Recovery over the internet.</span></span>

    * <span data-ttu-id="c976a-130">Sağlayıcı'nın doğrudan bağlanmasını istiyorsanız **Proxy olmadan doğrudan Azure Site Recovery hizmetine bağlan** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="c976a-130">If you want the Provider to connect directly select **Connect directly to Azure Site Recovery without a proxy**.</span></span>
    * <span data-ttu-id="c976a-131">Var olan ara sunucunuz kimlik doğrulaması gerektiren veya sağlayıcı bağlantılarında özel bir ara sunucu kullanmak istiyorsanız **Azure Site Recovery proxy sunucu kullanma Bağlan**.</span><span class="sxs-lookup"><span data-stu-id="c976a-131">If your existing proxy requires authentication, or you want to use a custom proxy for the Provider connection, select **Connect to Azure Site Recovery using a proxy server**.</span></span>
    * <span data-ttu-id="c976a-132">Bir proxy sunucu kullanıyorsanız:</span><span class="sxs-lookup"><span data-stu-id="c976a-132">If you use a proxy:</span></span>
        - <span data-ttu-id="c976a-133">Adresi, bağlantı noktası ve kimlik bilgilerini belirtin</span><span class="sxs-lookup"><span data-stu-id="c976a-133">Specify the address, port, and credentials</span></span>
        - <span data-ttu-id="c976a-134">Bölümünde açıklanan URL'lere emin olun [Önkoşullar](#prerequisites) proxy üzerinden izin verilir.</span><span class="sxs-lookup"><span data-stu-id="c976a-134">Make sure the URLs described in the [prerequisites](#prerequisites) are allowed through the proxy.</span></span>

    ![internet](./media/hyper-v-site-walkthrough-source-target/provider7.png)

6. <span data-ttu-id="c976a-136">Yükleme tamamlandıktan sonra tıklatın **kaydetmek** sunucuyu kasaya kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="c976a-136">After installation finishes, click **Register** to register the server in the vault.</span></span>

    ![Yükleme konumu](./media/hyper-v-site-walkthrough-source-target/provider2.png)

7. <span data-ttu-id="c976a-138">Kayıt tamamlandıktan sonra Hyper-V sunucusundan meta veriler, Azure Site Recovery tarafından alınır ve sunucu görüntülenen **Site Recovery altyapısı** > **Hyper-V konakları**.</span><span class="sxs-lookup"><span data-stu-id="c976a-138">After registration finishes, metadata from the Hyper-V server is retrieved by Azure Site Recovery, and the server is displayed in **Site Recovery Infrastructure** > **Hyper-V Hosts**.</span></span>


## <a name="set-up-the-target-environment"></a><span data-ttu-id="c976a-139">Hedef ortamı ayarlama</span><span class="sxs-lookup"><span data-stu-id="c976a-139">Set up the target environment</span></span>

<span data-ttu-id="c976a-140">Azure depolama hesabı için çoğaltma ve yük devretme sonrasında Azure Vm'lerinin bağlanacağı Azure ağını belirtin.</span><span class="sxs-lookup"><span data-stu-id="c976a-140">Specify the Azure storage account for replication, and the Azure network to which Azure VMs will connect after failover.</span></span>

1. <span data-ttu-id="c976a-141">Tıklatın **altyapıyı hazırlama** > **hedef**.</span><span class="sxs-lookup"><span data-stu-id="c976a-141">Click **Prepare infrastructure** > **Target**.</span></span>
2. <span data-ttu-id="c976a-142">Abonelik ve yük devretme sonrasında Azure sanal makinelerini oluşturmak istediğiniz kaynak grubunu seçin.</span><span class="sxs-lookup"><span data-stu-id="c976a-142">Select the subscription and the resource group in which you want to create the Azure VMs after failover.</span></span> <span data-ttu-id="c976a-143">Azure (Klasik veya resource management) VM'ler için kullanmak istediğiniz dağıtım modelini seçin.</span><span class="sxs-lookup"><span data-stu-id="c976a-143">Choose the deployment model that you want to use in Azure (classic or resource management) for the VMs.</span></span>

3. <span data-ttu-id="c976a-144">Site Recovery, bir veya birden çok uyumlu Azure depolama hesabınızın ve ağınızın olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="c976a-144">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

    - <span data-ttu-id="c976a-145">Bir depolama hesabınız yoksa tıklatın **+ depolama** bir Resource Manager tabanlı hesap satır içi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="c976a-145">If you don't have a storage account, click **+Storage** to create a Resource Manager-based account inline.</span></span> 
    - <span data-ttu-id="c976a-146">Bir Azure ağı yoksa tıklatın **+ ağ** bir Resource Manager tabanlı ağ satır içi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="c976a-146">If you don't have a Azure network, click **+Network** to create a Resource Manager-based network inline.</span></span>






## <a name="next-steps"></a><span data-ttu-id="c976a-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c976a-147">Next steps</span></span>

<span data-ttu-id="c976a-148">Git [adım 9: bir çoğaltma ilkesini ayarlayın](hyper-v-site-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="c976a-148">Go to [Step 9: Set up a replication policy](hyper-v-site-walkthrough-replication.md)</span></span>
