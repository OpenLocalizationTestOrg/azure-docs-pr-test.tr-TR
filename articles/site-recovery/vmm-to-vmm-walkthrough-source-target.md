---
title: "Merhaba kaynak ve hedef Hyper-V çoğaltma tooa Azure Site Recovery ile ikincil site için aaaSet | Microsoft Docs"
description: "Tooset yukarı hello kaynak ve ne zaman hedef nasıl açıklanmaktadır Hyper-V Vm'lerini çoğaltma toosecondary VMM site Azure Site Recovery ile."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: fa7809f1-7633-425f-b25d-d10d004e8d0b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 451cb4413ca5c09777a7faf512b1c8ea43e695f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-set-up-hello-replication-source-and-target"></a><span data-ttu-id="5776a-103">6. adım: hello çoğaltma kaynağı ve hedef ayarlama</span><span class="sxs-lookup"><span data-stu-id="5776a-103">Step 6: Set up hello replication source and target</span></span>


<span data-ttu-id="5776a-104">Hyper-V çoğaltma tooa içeren ikincil VMM sitesi için bir kurtarma Hizmetleri oluşturduktan sonra kasa [Azure Site Recovery](site-recovery-overview.md), bu makale tooset hello kaynağını kullanın ve hedef çoğaltma konumları.</span><span class="sxs-lookup"><span data-stu-id="5776a-104">After creating a Recovery Services vault for Hyper-V replication tooa secondary VMM site with [Azure Site Recovery](site-recovery-overview.md), use this article tooset up hello source and target replication locations.</span></span> 

<span data-ttu-id="5776a-105">Bu makaleyi okuduktan sonra tüm yorumlar hello altındaki ya da hello sonrası [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="5776a-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="set-up-hello-source-environment"></a><span data-ttu-id="5776a-106">Merhaba kaynak ortamını ayarlama</span><span class="sxs-lookup"><span data-stu-id="5776a-106">Set up hello source environment</span></span>

<span data-ttu-id="5776a-107">Hello Azure Site kurtarma sağlayıcısı VMM sunucularında yükleme ve bulmak ve sunucuları hello kasaya kaydetmek.</span><span class="sxs-lookup"><span data-stu-id="5776a-107">Install hello Azure Site Recovery Provider on VMM servers, and discover and register servers in hello vault.</span></span>

1. <span data-ttu-id="5776a-108">Tıklatın **1. adım: altyapıyı hazırlama** > **kaynak**.</span><span class="sxs-lookup"><span data-stu-id="5776a-108">Click **Step 1: Prepare Infrastructure** > **Source**.</span></span>

    ![Kaynağı ayarlama](./media/vmm-to-vmm-walkthrough-source-target/goals-source.png)
2. <span data-ttu-id="5776a-110">İçinde **kaynağı**, tıklatın **+ VMM** tooadd bir VMM sunucusu.</span><span class="sxs-lookup"><span data-stu-id="5776a-110">In **Prepare source**, click **+ VMM** tooadd a VMM server.</span></span>

    ![Kaynağı ayarlama](./media/vmm-to-vmm-walkthrough-source-target/set-source1.png)
3. <span data-ttu-id="5776a-112">İçinde **Sunucu Ekle**, denetleyin **System Center VMM sunucusunun** görünür **sunucu türü** ve hello VMM sunucusunun hello karşılayan [Önkoşullar](#prerequisites).</span><span class="sxs-lookup"><span data-stu-id="5776a-112">In **Add Server**, check that **System Center VMM server** appears in **Server type** and that hello VMM server meets hello [prerequisites](#prerequisites).</span></span>
4. <span data-ttu-id="5776a-113">Hello Azure Site Recovery sağlayıcısı yükleme dosyasını indirin.</span><span class="sxs-lookup"><span data-stu-id="5776a-113">Download hello Azure Site Recovery Provider installation file.</span></span>
5. <span data-ttu-id="5776a-114">Merhaba kayıt anahtarını indirin.</span><span class="sxs-lookup"><span data-stu-id="5776a-114">Download hello registration key.</span></span> <span data-ttu-id="5776a-115">Kurulumu çalıştırırken buna ihtiyacınız olur.</span><span class="sxs-lookup"><span data-stu-id="5776a-115">You need this when you run setup.</span></span> <span data-ttu-id="5776a-116">Merhaba anahtar, oluşturulduktan sonra beş gün boyunca geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="5776a-116">hello key is valid for five days after you generate it.</span></span>

    ![Kaynağı ayarlama](./media/vmm-to-vmm-walkthrough-source-target/set-source3.png)
6. <span data-ttu-id="5776a-118">Hello Azure Site Recovery sağlayıcısı hello VMM sunucusuna yükleyin.</span><span class="sxs-lookup"><span data-stu-id="5776a-118">Install hello Azure Site Recovery Provider on hello VMM server.</span></span> <span data-ttu-id="5776a-119">Gerekmeyen tooexplicitly herhangi bir şey Hyper-V ana bilgisayar sunucuları üzerinde yükleyin.</span><span class="sxs-lookup"><span data-stu-id="5776a-119">You don't need tooexplicitly install anything on Hyper-V host servers.</span></span>


## <a name="install-hello-azure-site-recovery-provider"></a><span data-ttu-id="5776a-120">Hello Azure Site Recovery sağlayıcısı yükleme</span><span class="sxs-lookup"><span data-stu-id="5776a-120">Install hello Azure Site Recovery Provider</span></span>

1. <span data-ttu-id="5776a-121">Her VMM sunucusunda Hello sağlayıcı kurulum dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5776a-121">Run hello Provider setup file on each VMM server.</span></span> <span data-ttu-id="5776a-122">VMM bir kümede dağıtılıyorsa, yüklediğiniz ilk kez hello aşağıdaki hello yapın:</span><span class="sxs-lookup"><span data-stu-id="5776a-122">If VMM is deployed in a cluster, do hello following hello first time you install:</span></span>
    -  <span data-ttu-id="5776a-123">Hello sağlayıcısı etkin bir düğümüne yükleyin ve hello yükleme tooregister hello VMM sunucusu hello kasasında tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="5776a-123">Install hello provider on an active node, and finish hello installation tooregister hello VMM server in hello vault.</span></span>
    - <span data-ttu-id="5776a-124">Ardından, hello sağlayıcısı üzerinde hello diğer düğümlere yükleyin.</span><span class="sxs-lookup"><span data-stu-id="5776a-124">Then, install hello Provider on hello other nodes.</span></span> <span data-ttu-id="5776a-125">Küme düğümleri tüm çalışmalı hello hello sağlayıcısı aynı sürümü.</span><span class="sxs-lookup"><span data-stu-id="5776a-125">Cluster nodes should all run hello same version of hello Provider.</span></span>
2. <span data-ttu-id="5776a-126">Kurulum, birkaç ön koşul denetimlerini çalıştırır ve izni toostop hello VMM hizmeti ister.</span><span class="sxs-lookup"><span data-stu-id="5776a-126">Setup runs a few prerequisite checks, and requests permission toostop hello VMM service.</span></span> <span data-ttu-id="5776a-127">Kurulum bittiğinde VMM hizmeti hello otomatik olarak yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="5776a-127">hello VMM service will be restarted automatically when setup finishes.</span></span> <span data-ttu-id="5776a-128">Bir VMM kümesinde yüklerseniz, istendiğinde toostop hello küme rolünü demektir.</span><span class="sxs-lookup"><span data-stu-id="5776a-128">If you install on a VMM cluster, you're prompted toostop hello Cluster role.</span></span>
3. <span data-ttu-id="5776a-129">İçinde **Microsoft Update**, sağlayıcı güncelleştirmeleri Microsoft Update ilkenize uygun yüklendiğini toospecify seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5776a-129">In **Microsoft Update**, you can opt in toospecify that provider updates are installed in accordance with your Microsoft Update policy.</span></span>
4. <span data-ttu-id="5776a-130">İçinde **yükleme**kabul edin veya hello varsayılan yükleme konumunu değiştirmek ve tıklatın **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="5776a-130">In **Installation**, accept or modify hello default installation location, and click **Install**.</span></span>

    ![Yükleme konumu](./media/vmm-to-vmm-walkthrough-source-target/provider-location.png)
5. <span data-ttu-id="5776a-132">Yükleme tamamlandıktan sonra tıklayın **kaydetmek** hello kasadaki tooregister hello sunucu.</span><span class="sxs-lookup"><span data-stu-id="5776a-132">After installation is complete, click **Register** tooregister hello server in hello vault.</span></span>

    ![Yükleme konumu](./media/vmm-to-vmm-walkthrough-source-target/provider-register.png)
6. <span data-ttu-id="5776a-134">İçinde **kasa adı**, hangi hello sunucunun kaydedileceği hello kasasının hello adını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="5776a-134">In **Vault name**, verify hello name of hello vault in which hello server will be registered.</span></span> <span data-ttu-id="5776a-135">*İleri*’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5776a-135">Click *Next*.</span></span>

    ![Sunucu kaydı](./media/vmm-to-vmm-walkthrough-source-target/vaultcred.png)
7. <span data-ttu-id="5776a-137">İçinde **Internet bağlantısı**, hello VMM sunucusunda çalışan hello sağlayıcısı tooAzure nasıl bağlandığını belirtin.</span><span class="sxs-lookup"><span data-stu-id="5776a-137">In **Internet Connection**, specify how hello provider running on hello VMM server connects tooAzure.</span></span>

    ![İnternet Ayarları](./media/vmm-to-vmm-walkthrough-source-target/proxydetails.png)

   - <span data-ttu-id="5776a-139">Bu hello sağlayıcısına bağlanmak doğrudan toohello belirtebilirsiniz Internet veya bir proxy üzerinden.</span><span class="sxs-lookup"><span data-stu-id="5776a-139">You can specify that hello provider should connect directly toohello internet, or via a proxy.</span></span>
   - <span data-ttu-id="5776a-140">Gerekiyorsa proxy ayarlarını belirtin.</span><span class="sxs-lookup"><span data-stu-id="5776a-140">Specify proxy settings if needed.</span></span>
   - <span data-ttu-id="5776a-141">Bir proxy kullanıyorsanız, VMM RunAs hesabı (DRAProxyAccount) belirtilen hello kullanılarak otomatik olarak oluşturulan proxy kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="5776a-141">If you use a proxy, a VMM RunAs account (DRAProxyAccount) is created automatically using hello specified proxy credentials.</span></span> <span data-ttu-id="5776a-142">Bu hesap başarıyla doğrulanabilmesi hello proxy sunucusunu yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="5776a-142">Configure hello proxy server so that this account can authenticate successfully.</span></span> <span data-ttu-id="5776a-143">Merhaba RunAs hesabı ayarları hello VMM konsolundan değiştirilebilir > **ayarları** > **güvenlik** > **farklı çalıştır hesapları**.</span><span class="sxs-lookup"><span data-stu-id="5776a-143">hello RunAs account settings can be modified in hello VMM console > **Settings** > **Security** > **Run As Accounts**.</span></span> <span data-ttu-id="5776a-144">Merhaba VMM hizmet tooupdate değişiklikleri yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="5776a-144">Restart hello VMM service tooupdate changes.</span></span>
8. <span data-ttu-id="5776a-145">İçinde **kayıt anahtarı**seçin hello anahtarı Azure Site Recovery'den indirdiğiniz ve toohello VMM sunucuya kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="5776a-145">In **Registration Key**, select hello key that you downloaded from Azure Site Recovery and copied toohello VMM server.</span></span>
9. <span data-ttu-id="5776a-146">Merhaba şifreleme ayarı yalnızca VMM Bulutları tooAzure Hyper-V sanal makineleri çoğaltma yapıyorsanız kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5776a-146">hello encryption setting is only used when you're replicating Hyper-V VMs in VMM clouds tooAzure.</span></span> <span data-ttu-id="5776a-147">İkincil site tooa çoğaltıyorsanız kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="5776a-147">If you're replicating tooa secondary site it's not used.</span></span>
10. <span data-ttu-id="5776a-148">İçinde **sunucu adı**, hello kasasında bir kolay ad tooidentify hello VMM sunucusu belirtin.</span><span class="sxs-lookup"><span data-stu-id="5776a-148">In **Server name**, specify a friendly name tooidentify hello VMM server in hello vault.</span></span> <span data-ttu-id="5776a-149">Bir küme yapılandırmasında hello VMM kümesi rolü adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="5776a-149">In a cluster configuration specify hello VMM cluster role name.</span></span>
11. <span data-ttu-id="5776a-150">İçinde **Eşitle bulut meta verileri**hello kasası ile Merhaba VMM sunucusundaki tüm Bulutlar için toosynchronize meta verileri istediğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="5776a-150">In **Synchronize cloud metadata**, select whether you want toosynchronize metadata for all clouds on hello VMM server with hello vault.</span></span> <span data-ttu-id="5776a-151">Bu eylem, yalnızca bir kez her sunucuda toohappen gerekir.</span><span class="sxs-lookup"><span data-stu-id="5776a-151">This action only needs toohappen once on each server.</span></span> <span data-ttu-id="5776a-152">Tüm bulutlar toosynchronize istemiyorsanız bu ayarı işaretsiz bırakın ve hello hello VMM konsolundaki bulut özellikleri ayrı ayrı her Bulutu eşitleyin.</span><span class="sxs-lookup"><span data-stu-id="5776a-152">If you don't want toosynchronize all clouds, you can leave this setting unchecked, and synchronize each cloud individually in hello cloud properties in hello VMM console.</span></span>
12. <span data-ttu-id="5776a-153">Tıklatın **sonraki** toocomplete hello işlemi.</span><span class="sxs-lookup"><span data-stu-id="5776a-153">Click **Next** toocomplete hello process.</span></span> <span data-ttu-id="5776a-154">Kayıttan sonra Azure Site Recovery tarafından hello VMM sunucusundan meta veriler alınır.</span><span class="sxs-lookup"><span data-stu-id="5776a-154">After registration, metadata from hello VMM server is retrieved by Azure Site Recovery.</span></span> <span data-ttu-id="5776a-155">Merhaba sunucu üzerinde hello görüntülenen **VMM sunucuları** hello sekmesinde **sunucuları** hello kasası sayfasında.</span><span class="sxs-lookup"><span data-stu-id="5776a-155">hello server is displayed on hello **VMM Servers** tab on hello **Servers** page in hello vault.</span></span>

    ![Sunucu](./media/vmm-to-vmm-walkthrough-source-target/provider13.png)
13. <span data-ttu-id="5776a-157">Merhaba sunucu hello Site Recovery konsolunda kullanılabilir duruma getirildikten sonra **kaynak** > **kaynağı** hello VMM sunucusu ve select hello bulut hello Hyper-V ana bilgisayar bulunduğu seçin.</span><span class="sxs-lookup"><span data-stu-id="5776a-157">After hello server is available in hello Site Recovery console, in **Source** > **Prepare source** select hello VMM server, and select hello cloud in which hello Hyper-V host is located.</span></span> <span data-ttu-id="5776a-158">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5776a-158">Then click **OK**.</span></span>

<span data-ttu-id="5776a-159">Merhaba sağlayıcısı hello komut satırından da yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5776a-159">You can also install hello provider from hello command line:</span></span>

[!INCLUDE [site-recovery-rw-provider-command-line](../../includes/site-recovery-rw-provider-command-line.md)]


## <a name="set-up-hello-target-environment"></a><span data-ttu-id="5776a-160">Merhaba hedef ortamını ayarlama</span><span class="sxs-lookup"><span data-stu-id="5776a-160">Set up hello target environment</span></span>

<span data-ttu-id="5776a-161">Merhaba hedef VMM sunucusunu ve Bulutu seçin:</span><span class="sxs-lookup"><span data-stu-id="5776a-161">Select hello target VMM server and cloud:</span></span>

1. <span data-ttu-id="5776a-162">Tıklatın **altyapıyı hazırlama** > **hedef**ve toouse istediğiniz select hello hedef VMM sunucusu.</span><span class="sxs-lookup"><span data-stu-id="5776a-162">Click **Prepare infrastructure** > **Target**, and select hello target VMM server you want toouse.</span></span>
2. <span data-ttu-id="5776a-163">Site Recovery ile eşitlenmiş Bulutlar hello sunucuda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="5776a-163">Clouds on hello server that are synchronized with Site Recovery will be displayed.</span></span> <span data-ttu-id="5776a-164">Merhaba hedef bulut seçin.</span><span class="sxs-lookup"><span data-stu-id="5776a-164">Select hello target cloud.</span></span>

   ![Hedef](./media/vmm-to-vmm-walkthrough-source-target/target-vmm.png)



## <a name="next-steps"></a><span data-ttu-id="5776a-166">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5776a-166">Next steps</span></span>

<span data-ttu-id="5776a-167">Çok Git[adım 7: ağ eşlemesini yapılandırma](vmm-to-vmm-walkthrough-network-mapping.md).</span><span class="sxs-lookup"><span data-stu-id="5776a-167">Go too[Step 7: Configure network mapping](vmm-to-vmm-walkthrough-network-mapping.md).</span></span>
