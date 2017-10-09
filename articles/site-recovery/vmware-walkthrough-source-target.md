---
title: "Merhaba kaynak ve hedef Azure Site Recovery ile VMware çoğaltma tooAzure için aaaSet | Microsoft Docs"
description: "Azure Site Recovery ile VMware Vm'lerini tooAzure depolama çoğaltma için kaynak ve hedef ayarlarını Hello adımları tooset özetler"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d99e422e-daf7-4fa8-af3c-af2340340136
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: ef33a44bc5da17afb0442be63f576925f5b9a8b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-vmware-replication-tooazure"></a><span data-ttu-id="8a7d7-103">8. adım: hello kaynak ve hedef VMware çoğaltma tooAzure için ayarlama</span><span class="sxs-lookup"><span data-stu-id="8a7d7-103">Step 8: Set up hello source and target for VMware replication tooAzure</span></span>

<span data-ttu-id="8a7d7-104">Bu makalede nasıl çoğaltırken tooconfigure kaynak ve hedef ayarları şirket içi VMware sanal makineleri tooAzure hello kullanarak [Azure Site Recovery](site-recovery-overview.md) hello Azure portal hizmeti.</span><span class="sxs-lookup"><span data-stu-id="8a7d7-104">This article describes how tooconfigure source and target settings when replicating on-premises VMware virtual machines tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="8a7d7-105">POST açıklamaları ve soruları hello altındaki bu makalenin veya hello [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="8a7d7-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-hello-source-environment"></a><span data-ttu-id="8a7d7-106">Merhaba kaynak ortamını ayarlama</span><span class="sxs-lookup"><span data-stu-id="8a7d7-106">Set up hello source environment</span></span>

<span data-ttu-id="8a7d7-107">Merhaba yapılandırma sunucusunu ayarlamayı, hello kasaya kaydetmek ve Vm'leri bulma.</span><span class="sxs-lookup"><span data-stu-id="8a7d7-107">Set up hello configuration server, register it in hello vault, and discover VMs.</span></span>

1. <span data-ttu-id="8a7d7-108">Tıklatın **Site kurtarma** > **1. adım: altyapıyı hazırlama** > **kaynak**.</span><span class="sxs-lookup"><span data-stu-id="8a7d7-108">Click **Site Recovery** > **Step 1: Prepare Infrastructure** > **Source**.</span></span>
2. <span data-ttu-id="8a7d7-109">Yapılandırma sunucusu yoksa, tıklatın **+ yapılandırma sunucusu**.</span><span class="sxs-lookup"><span data-stu-id="8a7d7-109">If you don’t have a configuration server, click **+Configuration server**.</span></span>
3. <span data-ttu-id="8a7d7-110">İçinde **Sunucu Ekle**, denetleyin **yapılandırma sunucusu** görünür **sunucu türü**.</span><span class="sxs-lookup"><span data-stu-id="8a7d7-110">In **Add Server**, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="8a7d7-111">Merhaba Site Recovery birleşik Kurulumu yükleme dosyasını indirin.</span><span class="sxs-lookup"><span data-stu-id="8a7d7-111">Download hello Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="8a7d7-112">Merhaba kasa kayıt anahtarını indirin.</span><span class="sxs-lookup"><span data-stu-id="8a7d7-112">Download hello vault registration key.</span></span> <span data-ttu-id="8a7d7-113">Birleşik Kurulum'u çalıştırdığınızda bu gerekir.</span><span class="sxs-lookup"><span data-stu-id="8a7d7-113">You need this when you run Unified Setup.</span></span> <span data-ttu-id="8a7d7-114">Merhaba anahtar, oluşturulduktan sonra beş gün boyunca geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="8a7d7-114">hello key is valid for five days after you generate it.</span></span>

   ![Kaynağı ayarlama](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-hello-configuration-server-in-hello-vault"></a><span data-ttu-id="8a7d7-116">Merhaba kasasına Hello yapılandırma sunucusuna kaydedin</span><span class="sxs-lookup"><span data-stu-id="8a7d7-116">Register hello configuration server in hello vault</span></span>

<span data-ttu-id="8a7d7-117">, Önce hello aşağıdaki başlayın, ardından birleşik Kurulum tooinstall hello yapılandırma sunucusu, hello işlem sunucusu ve hello ana hedef sunucusunda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="8a7d7-117">Do hello following before you start, then run Unified Setup tooinstall hello configuration server, hello process server, and hello master target server.</span></span>
    - <span data-ttu-id="8a7d7-118">Hızlı bir video özeti</span><span class="sxs-lookup"><span data-stu-id="8a7d7-118">Get a quick video overview</span></span>

        > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

    - <span data-ttu-id="8a7d7-119">Merhaba yapılandırma sunucusunda VM, o hello sistem saati ile eşitlenir emin olun bir [saat sunucusu](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span><span class="sxs-lookup"><span data-stu-id="8a7d7-119">On hello configuration server VM, make sure that hello system clock is synchronized with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span></span> <span data-ttu-id="8a7d7-120">Eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="8a7d7-120">It should match.</span></span> <span data-ttu-id="8a7d7-121">Önde 15 dakika ise veya arkasında kurulum başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="8a7d7-121">If it's 15 minutes in front or behind, setup might fail.</span></span>
    - <span data-ttu-id="8a7d7-122">Kurulum bir yerel yönetici hello yapılandırma sunucusundaki VM olarak çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="8a7d7-122">Run setup as a Local Administrator on hello configuration server VM.</span></span>
    - <span data-ttu-id="8a7d7-123">TLS 1.0 hello VM etkin olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="8a7d7-123">Make sure TLS 1.0 is enabled on hello VM.</span></span>


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="8a7d7-124">Merhaba yapılandırma sunucusu da yüklenebilir [hello komut satırından](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="8a7d7-124">hello configuration server can also be installed [from hello command line](http://aka.ms/installconfigsrv).</span></span>



## <a name="connect-toovmware-servers"></a><span data-ttu-id="8a7d7-125">TooVMware sunucularına bağlanmak</span><span class="sxs-lookup"><span data-stu-id="8a7d7-125">Connect tooVMware servers</span></span>

<span data-ttu-id="8a7d7-126">tooallow Azure Site Recovery toodiscover şirket içi ortamınızda çalışan sanal makineler, VMware vCenter sunucusu veya Site Recovery ile vSphere ESXi konakları tooconnect gerekir.</span><span class="sxs-lookup"><span data-stu-id="8a7d7-126">tooallow Azure Site Recovery toodiscover virtual machines running in your on-premises environment, you need tooconnect your VMware vCenter Server or vSphere ESXi hosts with Site Recovery.</span></span> <span data-ttu-id="8a7d7-127">Başlamadan önce hello aşağıdakilere dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="8a7d7-127">Note hello following before you start:</span></span>

- <span data-ttu-id="8a7d7-128">Merhaba sunucuda hello vCenter sunucusu veya yönetici ayrıcalıkları olmayan bir hesapla vSphere ana tooSite kurtarma eklerseniz, hello hesabının etkin Bu ayrıcalıkları gerekir:</span><span class="sxs-lookup"><span data-stu-id="8a7d7-128">If you add hello vCenter server or vSphere hosts tooSite Recovery with an account without administrator privileges on hello server, hello account needs these privileges enabled:</span></span>
    - <span data-ttu-id="8a7d7-129">Datacenter, veri deposu, klasör, ana bilgisayar, ağ, kaynak, sanal makine, vSphere dağıtılmış anahtar.</span><span class="sxs-lookup"><span data-stu-id="8a7d7-129">Datacenter, Datastore, Folder, Host, Network, Resource, Virtual machine, vSphere Distributed Switch.</span></span>
    - <span data-ttu-id="8a7d7-130">Merhaba vCenter sunucusu depolama görünümleri izinleri olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8a7d7-130">hello vCenter server needs Storage views permissions.</span></span>
- <span data-ttu-id="8a7d7-131">VMware sunucularını tooSite kurtarma eklediğinizde, 15 dakika alabilir veya onlar için daha uzun tooappear hello Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="8a7d7-131">When you add VMware servers tooSite Recovery, it can take 15 minutes or longer for them tooappear in hello portal.</span></span>

### <a name="add-hello-account-for-automatic-discovery"></a><span data-ttu-id="8a7d7-132">Otomatik bulma için Hello hesabı ekleyin</span><span class="sxs-lookup"><span data-stu-id="8a7d7-132">Add hello account for automatic discovery</span></span>

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="set-up-a-connection"></a><span data-ttu-id="8a7d7-133">Bağlantı kurma</span><span class="sxs-lookup"><span data-stu-id="8a7d7-133">Set up a connection</span></span>

<span data-ttu-id="8a7d7-134">Tooservers şu şekilde bağlanın:</span><span class="sxs-lookup"><span data-stu-id="8a7d7-134">Connect tooservers as follows:</span></span>

1. <span data-ttu-id="8a7d7-135">Seçin **+ vCenter** toostart bir VMware vCenter sunucusu veya bir VMware vSphere ESXi konağı bağlanma.</span><span class="sxs-lookup"><span data-stu-id="8a7d7-135">Select **+vCenter** toostart connecting a VMware vCenter server or a VMware vSphere ESXi host.</span></span>
2. <span data-ttu-id="8a7d7-136">İçinde **vCenter ekleme**hello vSphere ana bilgisayar veya vCenter sunucusu için bir kolay ad belirtin ve sonra başlangıç IP adresi veya hello sunucusunun FQDN'sini belirtin.</span><span class="sxs-lookup"><span data-stu-id="8a7d7-136">In **Add vCenter**, specify a friendly name for hello vSphere host or vCenter server, and then specify hello IP address or FQDN of hello server.</span></span>
3. <span data-ttu-id="8a7d7-137">VMware sunucularınızı farklı bir bağlantı noktası isteklerini yapılandırılmış toolisten olmadıkça hello bağlantı noktası 443'tür bırakın.</span><span class="sxs-lookup"><span data-stu-id="8a7d7-137">Leave hello port as 443 unless your VMware servers are configured toolisten for requests on a different port.</span></span> <span data-ttu-id="8a7d7-138">Tooconnect toohello VMware vCenter veya vSphere ESXi sunucu hello hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="8a7d7-138">Select hello account that is tooconnect toohello VMware vCenter or vSphere ESXi server.</span></span> <span data-ttu-id="8a7d7-139">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8a7d7-139">Click **OK**.</span></span>
4. <span data-ttu-id="8a7d7-140">Site Recovery bağlayan tooVMware sunucuları hello kullanarak belirtilen ayarlarını ve sanal makineleri bulur.</span><span class="sxs-lookup"><span data-stu-id="8a7d7-140">Site Recovery connects tooVMware servers using hello specified settings, and discovers VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="8a7d7-141">Bir sunucu veya ana bilgisayar hello vCenter veya ana bilgisayar sunucusunda yönetici ayrıcalıklarına sahip olmayan bir hesapla ekliyorsanız hello hesabı etkin Bu ayrıcalıkları olduğundan emin olun: Datacenter, veri deposu, klasör, ana bilgisayar, ağ, kaynak, sanal makine ve vSphere dağıtılmış anahtar.</span><span class="sxs-lookup"><span data-stu-id="8a7d7-141">If you're adding a server or host with an account that doesn't have administrator privileges on hello vCenter or host server, make sure that hello account has these privileges enabled: Datacenter, Datastore, Folder, Host, Network, Resource, Virtual machine, and vSphere Distributed Switch.</span></span> <span data-ttu-id="8a7d7-142">Ayrıca, hello VMware vCenter server hello depolama ayrıcalık etkinleştirilmiş görünümlere gerekir.</span><span class="sxs-lookup"><span data-stu-id="8a7d7-142">In addition, hello VMware vCenter server needs hello Storage Views privilege enabled.</span></span>


## <a name="set-up-hello-target-environment"></a><span data-ttu-id="8a7d7-143">Merhaba hedef ortamını ayarlama</span><span class="sxs-lookup"><span data-stu-id="8a7d7-143">Set up hello target environment</span></span>

<span data-ttu-id="8a7d7-144">Merhaba hedef ortamını ayarlama önce bir Azure depolama hesabı ve sanal ağ kurulumu olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="8a7d7-144">Before you set up hello target environment, make sure you have an Azure storage account and virtual network set up.</span></span>

1. <span data-ttu-id="8a7d7-145">Tıklatın **altyapıyı hazırlama** > **hedef**, ve hello toouse istediğiniz Azure aboneliğini seçin.</span><span class="sxs-lookup"><span data-stu-id="8a7d7-145">Click **Prepare infrastructure** > **Target**, and select hello Azure subscription you want toouse.</span></span>
2. <span data-ttu-id="8a7d7-146">Belirtin, hedef dağıtım modeli Resource Manager tabanlı veya Klasik olup.</span><span class="sxs-lookup"><span data-stu-id="8a7d7-146">Specify whether your target deployment model is Resource Manager-based, or classic.</span></span>
3. <span data-ttu-id="8a7d7-147">Site Recovery, bir veya birden çok uyumlu Azure depolama hesabınızın ve ağınızın olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="8a7d7-147">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

   ![Hedef](./media/vmware-walkthrough-source-target/gs-target.png)
4. <span data-ttu-id="8a7d7-149">Bir depolama hesabı veya ağı oluşturmadıysanız, tıklatın **+ depolama hesabı** veya **+ ağ**, toocreate bir Resource Manager hesabı ya da ağ satır içi.</span><span class="sxs-lookup"><span data-stu-id="8a7d7-149">If you haven't created a storage account or network, click **+Storage account** or **+Network**, toocreate a Resource Manager account or network inline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8a7d7-150">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8a7d7-150">Next steps</span></span>

<span data-ttu-id="8a7d7-151">Çok Git[adım 9: bir çoğaltma ilkesini ayarlayın](vmware-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="8a7d7-151">Go too[Step 9: Set up a replication policy](vmware-walkthrough-replication.md)</span></span>
