---
title: "Merhaba kaynak ve hedef Azure Site Recovery ile Hyper-V çoğaltma tooAzure (System Center VMM ile) için yukarı aaaSet | Microsoft Docs"
description: "Hyper-V sanal makineleri çoğaltma VMM Bulutları tooAzure depolama Azure Site Recovery ile kaynak ve hedef ayarlar Hello adımları tooset özetler"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5edb6d87-25a5-40fe-b6f1-ddf7b55a6b31
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/25/2017
ms.author: raynew
ms.openlocfilehash: 3f8c5386cb64527c775aef636980bac098ee9905
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-hyper-v-with-vmm-replication-tooazure"></a><span data-ttu-id="6b5f5-103">8. adım: hello kaynak ve hedef Hyper-V (VMM ile) çoğaltma tooAzure için ayarlama</span><span class="sxs-lookup"><span data-stu-id="6b5f5-103">Step 8: Set up hello source and target for Hyper-V (with VMM) replication tooAzure</span></span>

<span data-ttu-id="6b5f5-104">Sonra [bir kasa oluşturarak](vmm-to-azure-walkthrough-create-vault.md) ve neleri belirtme tooreplicate istediğiniz, bu makale tooconfigure kaynağı kullanmak ve şirket içi Hyper-V sanal makineleri System Center Virtual Machine Manager (VMM) çoğaltırken ayarları hedef Hello kullanarak bulut tooAzure [Azure Site Recovery](site-recovery-overview.md) hello Azure portal hizmeti.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-104">After [creating a vault](vmm-to-azure-walkthrough-create-vault.md) and specifying what you want tooreplicate, use this article tooconfigure source and target settings when replicating on-premises Hyper-V virtual machines in System Center Virtual Machine Manager (VMM) clouds tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="6b5f5-105">POST açıklamaları ve soruları hello altındaki bu makalenin veya hello [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="6b5f5-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-hello-source-environment"></a><span data-ttu-id="6b5f5-106">Merhaba kaynak ortamını ayarlama</span><span class="sxs-lookup"><span data-stu-id="6b5f5-106">Set up hello source environment</span></span>

<span data-ttu-id="6b5f5-107">S1.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-107">S1.</span></span> <span data-ttu-id="6b5f5-108">**Altyapıyı Hazırlama** > **Kaynak** seçeneklerine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-108">Click **Prepare Infrastructure** > **Source**.</span></span>

    ![Set up source](./media/vmm-to-azure-walkthrough-source-target/set-source1.png)

2. <span data-ttu-id="6b5f5-109">İçinde **kaynağı**, tıklatın **+ VMM** tooadd bir VMM sunucusu.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-109">In **Prepare source**, click **+ VMM** tooadd a VMM server.</span></span>

    ![Kaynağı ayarlama](./media/vmm-to-azure-walkthrough-source-target/set-source2.png)

3. <span data-ttu-id="6b5f5-111">İçinde **Sunucu Ekle**, denetleyin **System Center VMM sunucusunun** görünür **sunucu türü** ve hello VMM sunucusunun hello karşılayan [önkoşulları ve URL gereksinimleri](#prerequisites).</span><span class="sxs-lookup"><span data-stu-id="6b5f5-111">In **Add Server**, check that **System Center VMM server** appears in **Server type** and that hello VMM server meets hello [prerequisites and URL requirements](#prerequisites).</span></span>
4. <span data-ttu-id="6b5f5-112">Hello Azure Site Recovery sağlayıcısı yükleme dosyasını indirin.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-112">Download hello Azure Site Recovery Provider installation file.</span></span>
5. <span data-ttu-id="6b5f5-113">Merhaba kayıt anahtarını indirin.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-113">Download hello registration key.</span></span> <span data-ttu-id="6b5f5-114">Kurulumu çalıştırırken buna ihtiyacınız olur.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-114">You need this when you run setup.</span></span> <span data-ttu-id="6b5f5-115">Merhaba anahtar, oluşturulduktan sonra beş gün boyunca geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-115">hello key is valid for five days after you generate it.</span></span>

    ![Kaynağı ayarlama](./media/vmm-to-azure-walkthrough-source-target/set-source3.png)

## <a name="install-hello-provider-on-hello-vmm-server"></a><span data-ttu-id="6b5f5-117">Merhaba sağlayıcısı hello VMM sunucusuna yükleyin</span><span class="sxs-lookup"><span data-stu-id="6b5f5-117">Install hello Provider on hello VMM server</span></span>

1. <span data-ttu-id="6b5f5-118">Merhaba sağlayıcı kurulum dosyasını hello VMM sunucusunda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-118">Run hello Provider setup file on hello VMM server.</span></span>
2. <span data-ttu-id="6b5f5-119">**Microsoft Update** kısmından güncelleştirmeleri seçebilirsiniz. Böylece, Sağlayıcı güncelleştirmeleri Microsoft Update ilkenize uygun şekilde yüklenir.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-119">In **Microsoft Update**, you can opt in for updates so that Provider updates are installed in accordance with your Microsoft Update policy.</span></span>
3. <span data-ttu-id="6b5f5-120">İçinde **yükleme**, kabul etmek veya hello varsayılan sağlayıcı yükleme konumunu değiştirmek ve tıklatın **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-120">In **Installation**, accept or modify hello default Provider installation location and click **Install**.</span></span>

    ![Yükleme konumu](./media/vmm-to-azure-walkthrough-source-target/provider2.png)
4. <span data-ttu-id="6b5f5-122">Yükleme bittiğinde, bilgisayarınızı **kaydetmek** hello kasadaki tooregister hello VMM sunucusu.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-122">When installation finishes, click **Register** tooregister hello VMM server in hello vault.</span></span>
5. <span data-ttu-id="6b5f5-123">Merhaba, **kasa ayarlarını** sayfasında, **Gözat** tooselect hello kasa anahtarı dosyasını.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-123">In hello **Vault Settings** page, click **Browse** tooselect hello vault key file.</span></span> <span data-ttu-id="6b5f5-124">Hello Azure Site Recovery aboneliğine ve hello kasa adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-124">Specify hello Azure Site Recovery subscription and hello vault name.</span></span>

    ![Sunucu kaydı](./media/vmm-to-azure-walkthrough-source-target/provider10.png)
6. <span data-ttu-id="6b5f5-126">İçinde **Internet bağlantısı**, nasıl hello VMM sunucusunda çalışan sağlayıcı üzerinden tooSite kurtarma bağlanacağı hello hello Internet belirtin.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-126">In **Internet Connection**, specify how hello Provider running on hello VMM server will connect tooSite Recovery over hello internet.</span></span>

   * <span data-ttu-id="6b5f5-127">Merhaba sağlayıcısı tooconnect doğrudan istiyorsanız seçin **tooAzure Site Recovery Ara sunucu olmadan doğrudan bağlan**.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-127">If you want hello Provider tooconnect directly, select **Connect directly tooAzure Site Recovery without a proxy**.</span></span>
   * <span data-ttu-id="6b5f5-128">Var olan ara sunucunuz kimlik doğrulaması gerektiren veya toouse özel bir ara sunucu isterseniz seçin **tooAzure Site kurtarma proxy sunucusu kullanarak bağlanmak**.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-128">If your existing proxy requires authentication, or you want toouse a custom proxy, select **Connect tooAzure Site Recovery using a proxy server**.</span></span>
   * <span data-ttu-id="6b5f5-129">Özel bir ara sunucu kullanırsanız, başlangıç adresi, bağlantı noktası ve kimlik bilgilerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-129">If you use a custom proxy, specify hello address, port, and credentials.</span></span>
   * <span data-ttu-id="6b5f5-130">Bir proxy sunucu kullanıyorsanız, zaten açıklanan hello URL'lere izin [Önkoşullar](#on-premises-prerequisites).</span><span class="sxs-lookup"><span data-stu-id="6b5f5-130">If you're using a proxy, you should have already allowed hello URLs described in [prerequisites](#on-premises-prerequisites).</span></span>
   * <span data-ttu-id="6b5f5-131">Özel bir ara sunucu kullanırsanız, VMM RunAs hesabı (DRAProxyAccount) belirtilen hello kullanılarak otomatik olarak oluşturulacak proxy kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-131">If you use a custom proxy, a VMM RunAs account (DRAProxyAccount) will be created automatically using hello specified proxy credentials.</span></span> <span data-ttu-id="6b5f5-132">Bu hesap başarıyla doğrulanabilmesi hello proxy sunucusunu yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-132">Configure hello proxy server so that this account can authenticate successfully.</span></span> <span data-ttu-id="6b5f5-133">Merhaba VMM RunAs hesabı ayarları hello VMM konsolundan değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-133">hello VMM RunAs account settings can be modified in hello VMM console.</span></span> <span data-ttu-id="6b5f5-134">İçinde **ayarları**, genişletin **güvenlik** > **farklı çalıştır hesapları**ve ardından hello DRAProxyAccount parolasını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-134">In **Settings**, expand **Security** > **Run As Accounts**, and then modify hello password for DRAProxyAccount.</span></span> <span data-ttu-id="6b5f5-135">Bu ayar etkinleşir toorestart hello VMM hizmeti gerekmektedir.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-135">You’ll need toorestart hello VMM service so that this setting takes effect.</span></span>

     ![internet](./media/vmm-to-azure-walkthrough-source-target/provider13.png)
7. <span data-ttu-id="6b5f5-137">Kabul edin veya veri şifreleme için otomatik olarak oluşturulan bir SSL sertifikası hello konumunu değiştirin.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-137">Accept or modify hello location of an SSL certificate that’s automatically generated for data encryption.</span></span> <span data-ttu-id="6b5f5-138">Hello Azure Site Recovery portalında Azure tarafından korunan bir bulut için veri şifrelemeyi etkinleştirirseniz, bu sertifika kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-138">This certificate is used if you enable data encryption for a cloud protected by Azure in hello Azure Site Recovery portal.</span></span> <span data-ttu-id="6b5f5-139">Bu sertifikayı güvenli bir yerde saklayın.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-139">Keep this certificate safe.</span></span> <span data-ttu-id="6b5f5-140">Bir yük devretme tooAzure çalıştırdığınızda, veri şifreleme etkinleştirilmişse, toodecrypt, gerekir.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-140">When you run a failover tooAzure you’ll need it toodecrypt, if data encryption is enabled.</span></span>
8. <span data-ttu-id="6b5f5-141">İçinde **sunucu adı**, hello kasasında bir kolay ad tooidentify hello VMM sunucusu belirtin.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-141">In **Server name**, specify a friendly name tooidentify hello VMM server in hello vault.</span></span> <span data-ttu-id="6b5f5-142">Bir küme yapılandırmasında hello VMM kümesi rolü adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-142">In a cluster configuration, specify hello VMM cluster role name.</span></span>
9. <span data-ttu-id="6b5f5-143">Etkinleştirme **bulut meta verilerini eşitle**hello kasası ile Merhaba VMM sunucusundaki tüm Bulutlar için toosynchronize meta verileri istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-143">Enable **Sync cloud metadata**, if you want toosynchronize metadata for all clouds on hello VMM server with hello vault.</span></span> <span data-ttu-id="6b5f5-144">Bu eylem, yalnızca bir kez her sunucuda toohappen gerekir.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-144">This action only needs toohappen once on each server.</span></span> <span data-ttu-id="6b5f5-145">Tüm bulutlar toosynchronize istemiyorsanız bu ayarı işaretsiz bırakın ve her Bulutu ayrı ayrı hello hello VMM konsolundaki bulut özellikleri eşitleyin.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-145">If you don't want toosynchronize all clouds, you can leave this setting unchecked and synchronize each cloud individually in hello cloud properties in hello VMM console.</span></span> <span data-ttu-id="6b5f5-146">Tıklatın **kaydetmek** toocomplete hello işlemi.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-146">Click **Register** toocomplete hello process.</span></span>

    ![Sunucu kaydı](./media/vmm-to-azure-walkthrough-source-target/provider16.png)
10. <span data-ttu-id="6b5f5-148">Kayıt başlar.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-148">Registration starts.</span></span> <span data-ttu-id="6b5f5-149">Kayıt tamamlandıktan sonra hello sunucu görüntülenen **Site Recovery altyapısı** > **VMM sunucuları**.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-149">After registration finishes, hello server is displayed in **Site Recovery Infrastructure** > **VMM Servers**.</span></span>


## <a name="install-hello-azure-recovery-services-agent-on-hyper-v-hosts"></a><span data-ttu-id="6b5f5-150">Hello Azure kurtarma Hizmetleri aracısını Hyper-V ana bilgisayarlarına yükleme</span><span class="sxs-lookup"><span data-stu-id="6b5f5-150">Install hello Azure Recovery Services agent on Hyper-V hosts</span></span>

1. <span data-ttu-id="6b5f5-151">Sağlayıcı hello ayarladıktan sonra hello Azure kurtarma Hizmetleri Aracısı toodownload hello yükleme dosyası gerekir.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-151">After you've set up hello Provider, you need toodownload hello installation file for hello Azure Recovery Services agent.</span></span> <span data-ttu-id="6b5f5-152">Her Hyper-V sunucusu hello VMM bulutu için Kurulumu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-152">Run setup on each Hyper-V server in hello VMM cloud.</span></span>

    ![Hyper-V siteleri](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent1.png)
2. <span data-ttu-id="6b5f5-154">**Önkoşul Denetimi**’nde **İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-154">In **Prerequisites Check**, click **Next**.</span></span> <span data-ttu-id="6b5f5-155">Eksik önkoşullar otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-155">Any missing prerequisites will be automatically installed.</span></span>

    ![Kurtarma Hizmetleri Aracısı Önkoşulları](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent2.png)
3. <span data-ttu-id="6b5f5-157">İçinde **yükleme ayarları**kabul edin veya hello yükleme konumu ve hello önbellek konumunu değiştirin.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-157">In **Installation Settings**, accept or modify hello installation location, and hello cache location.</span></span> <span data-ttu-id="6b5f5-158">Hello önbellek en az 5 GB depolama alanı kullanılabilir olan bir sürücüde yapılandırabilirsiniz, ancak 600 GB veya daha fazla boş alana sahip bir önbellek sürücüsü kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-158">You can configure hello cache on a drive that has at least 5 GB of storage available but we recommend a cache drive with 600 GB or more of free space.</span></span> <span data-ttu-id="6b5f5-159">Ardından **Yükle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-159">Then click **Install**.</span></span>
4. <span data-ttu-id="6b5f5-160">Yükleme tamamlandıktan sonra tıklayın **Kapat** toofinish.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-160">After installation is complete, click **Close** toofinish.</span></span>

    ![MARS Aracısı'nı Kaydetme](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent3.png)

### <a name="command-line-installation"></a><span data-ttu-id="6b5f5-162">Komut satırı yüklemesi</span><span class="sxs-lookup"><span data-stu-id="6b5f5-162">Command line installation</span></span>
<span data-ttu-id="6b5f5-163">Microsoft Azure kurtarma Hizmetleri Aracısı hello komutu aşağıdaki hello kullanarak komut satırından yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6b5f5-163">You can install hello Microsoft Azure Recovery Services Agent from command line using hello following command:</span></span>

     marsagentinstaller.exe /q /nu

### <a name="set-up-internet-proxy-access-toosite-recovery-from-hyper-v-hosts"></a><span data-ttu-id="6b5f5-164">Internet proxy erişim tooSite kurtarma Hyper-V konakları ayarlama</span><span class="sxs-lookup"><span data-stu-id="6b5f5-164">Set up internet proxy access tooSite Recovery from Hyper-V hosts</span></span>

<span data-ttu-id="6b5f5-165">Merhaba kurtarma Hizmetleri aracısını Hyper-V konakları üzerinde çalışan VM çoğaltması için Internet erişimi tooAzure gerekir.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-165">hello Recovery Services agent running on Hyper-V hosts needs internet access tooAzure for VM replication.</span></span> <span data-ttu-id="6b5f5-166">Erişiyorsanız Internet hello bir proxy üzerinden, aşağıdaki gibi ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="6b5f5-166">If you're accessing hello internet through a proxy, set it up as follows:</span></span>

1. <span data-ttu-id="6b5f5-167">Merhaba Hyper-V ana bilgisayarda Hello Microsoft Azure Backup MMC eklentisini açın.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-167">Open hello Microsoft Azure Backup MMC snap-in on hello Hyper-V host.</span></span> <span data-ttu-id="6b5f5-168">Varsayılan olarak, Microsoft Azure yedekleme için bir kısayol hello masaüstünde veya C:\Program Files\Microsoft Azure Recovery Services agent\bin\wabadmin yolunda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-168">By default, a shortcut for Microsoft Azure Backup is available on hello desktop or in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span></span>
2. <span data-ttu-id="6b5f5-169">Merhaba ek bileşeninde, tıklatın **özelliklerini değiştirme**.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-169">In hello snap-in, click **Change Properties**.</span></span>
3. <span data-ttu-id="6b5f5-170">Merhaba üzerinde **Proxy Yapılandırması** sekmesinde, proxy sunucusu bilgilerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-170">On hello **Proxy Configuration** tab, specify proxy server information.</span></span>

    ![MARS Aracısı'nı Kaydetme](./media/vmm-to-azure-walkthrough-source-target/mars-proxy.png)
4. <span data-ttu-id="6b5f5-172">Bu hello aracı hello açıklanan hello URL'leri ulaşmak denetleyin [Önkoşullar](#on-premises-prerequisites).</span><span class="sxs-lookup"><span data-stu-id="6b5f5-172">Check that hello agent can reach hello URLs described in hello [prerequisites](#on-premises-prerequisites).</span></span>

## <a name="set-up-hello-target-environment"></a><span data-ttu-id="6b5f5-173">Merhaba hedef ortamını ayarlama</span><span class="sxs-lookup"><span data-stu-id="6b5f5-173">Set up hello target environment</span></span>
<span data-ttu-id="6b5f5-174">Çoğaltma için kullanılan hello Azure depolama hesabı toobe belirtin ve hello Azure ağ toowhich Azure Vm'lerinin yük devretme sonrasında bağlanır.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-174">Specify hello Azure storage account toobe used for replication, and hello Azure network toowhich Azure VMs will connect after failover.</span></span>

1. <span data-ttu-id="6b5f5-175">Tıklatın **altyapıyı hazırlama** > **hedef**hello aboneliği seçin ve hello devredilen sanal makinelerin toocreate hello istediğiniz kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-175">Click **Prepare infrastructure** > **Target**, select hello subscription and hello resource group where you want toocreate hello failed over virtual machines.</span></span> <span data-ttu-id="6b5f5-176">Toouse (Klasik veya resource management) azure'da hello devredilen sanal makinelerin istediğiniz hello dağıtım modelini seçin.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-176">Choose hello deployment model that you want toouse in Azure (classic or resource management) for hello failed over virtual machines.</span></span>

    ![Depolama](./media/vmm-to-azure-walkthrough-source-target/enablerep3.png)

2. <span data-ttu-id="6b5f5-178">Site Recovery, bir veya birden çok uyumlu Azure depolama hesabınızın ve ağınızın olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-178">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

    ![Depolama](./media/vmm-to-azure-walkthrough-source-target/compatible-storage.png)

3. <span data-ttu-id="6b5f5-180">Bir depolama hesabı oluşturmadıysanız ve toocreate bir istiyorsanız Kaynak Yöneticisi'ni kullanarak tıklatın **+ depolama hesabı** toodo bu işlemi satır içinde.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-180">If you haven't created a storage account, and you want toocreate one using Resource Manager, click **+Storage account** toodo that inline.</span></span>  <span data-ttu-id="6b5f5-181">Merhaba üzerinde **depolama hesabı oluşturma** dikey penceresinde bir hesap adı, türü, abonelik ve konum belirtin.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-181">On hello **Create storage account** blade specify an account name, type, subscription, and location.</span></span> <span data-ttu-id="6b5f5-182">Merhaba hesap hello olmalıdır hello aynı konuma kurtarma Hizmetleri kasası.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-182">hello account should be in hello same location as hello Recovery Services vault.</span></span>

   ![Depolama](./media/vmm-to-azure-walkthrough-source-target/gs-createstorage.png)


   * <span data-ttu-id="6b5f5-184">Merhaba Klasik modeli kullanarak bir depolama hesabı toocreate istiyorsanız, hello Azure portal yapın.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-184">If you want toocreate a storage account using hello classic model, do that in hello Azure portal.</span></span> [<span data-ttu-id="6b5f5-185">Daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="6b5f5-185">Learn more</span></span>](../storage/common/storage-create-storage-account.md)
   * <span data-ttu-id="6b5f5-186">Çoğaltılan veriler için bir premium depolama hesabı kullanıyorsanız, bir ek bir standart depolama hesabı, devam eden değişiklikler tooon içi verilerini yakalama toostore çoğaltma günlükleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-186">If you’re using a premium storage account for replicated data, set up an additional standard storage account, toostore replication logs that capture ongoing changes tooon-premises data.</span></span>
5. <span data-ttu-id="6b5f5-187">Bir Azure ağı oluşturmadıysanız ve toocreate bir istiyorsanız Kaynak Yöneticisi'ni kullanarak tıklatın **+ ağ** toodo bu işlemi satır içinde.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-187">If you haven't created an Azure network, and you want toocreate one using Resource Manager, click **+Network** toodo that inline.</span></span> <span data-ttu-id="6b5f5-188">Merhaba üzerinde **sanal ağ oluştur** dikey penceresinde, bir ağ adı, adres aralığı, alt ağ ayrıntıları, abonelik ve konum belirtin.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-188">On hello **Create virtual network** blade specify a network name, address range, subnet details, subscription, and location.</span></span> <span data-ttu-id="6b5f5-189">Merhaba ağ hello olmalıdır hello aynı konuma kurtarma Hizmetleri kasası.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-189">hello network should be in hello same location as hello Recovery Services vault.</span></span>

   ![Ağ](./media/vmm-to-azure-walkthrough-source-target/gs-createnetwork.png)

   <span data-ttu-id="6b5f5-191">Merhaba Klasik modeli kullanarak bir ağ toocreate istiyorsanız, hello Azure portal yapın.</span><span class="sxs-lookup"><span data-stu-id="6b5f5-191">If you want toocreate a network using hello classic model, do that in hello Azure portal.</span></span> <span data-ttu-id="6b5f5-192">[Daha fazla bilgi edinin](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="6b5f5-192">[Learn more](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).</span></span>





## <a name="next-steps"></a><span data-ttu-id="6b5f5-193">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6b5f5-193">Next steps</span></span>

<span data-ttu-id="6b5f5-194">Çok Git[adım 9: ağ eşlemesini yapılandırma](vmm-to-azure-walkthrough-network-mapping.md)</span><span class="sxs-lookup"><span data-stu-id="6b5f5-194">Go too[Step 9: Configure network mapping](vmm-to-azure-walkthrough-network-mapping.md)</span></span>
