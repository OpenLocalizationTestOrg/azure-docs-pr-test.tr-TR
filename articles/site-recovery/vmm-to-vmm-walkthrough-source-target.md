---
title: "Kaynak ve hedef Hyper-V çoğaltma Azure Site Recovery ile ikincil site için ayarlama | Microsoft Docs"
description: "Kaynak ve hedef Azure Site Recovery ile ikincil VMM sitesi için Hyper-V sanal makineleri çoğaltırken ayarlamak açıklar."
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
ms.openlocfilehash: 07135e9b5e619971a59cc22ec68a0a4e8bcaabe1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="step-6-set-up-the-replication-source-and-target"></a><span data-ttu-id="d9aff-103">6. adım: çoğaltma kaynağı ve hedef ayarlama</span><span class="sxs-lookup"><span data-stu-id="d9aff-103">Step 6: Set up the replication source and target</span></span>


<span data-ttu-id="d9aff-104">Kurtarma Hizmetleri oluşturduktan sonra için Hyper-V çoğaltmasını içeren ikincil VMM sitesi için kasa [Azure Site Recovery](site-recovery-overview.md), kaynak ve hedef çoğaltma konumları ayarlamak için bu makaleyi kullanın.</span><span class="sxs-lookup"><span data-stu-id="d9aff-104">After creating a Recovery Services vault for Hyper-V replication to a secondary VMM site with [Azure Site Recovery](site-recovery-overview.md), use this article to set up the source and target replication locations.</span></span> 

<span data-ttu-id="d9aff-105">Bu makaleyi okuduktan sonra yapmak istediğiniz tüm yorumları makalenin alt kısmında veya [Azure Kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)'nda paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d9aff-105">After reading this article, post any comments at the bottom, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="set-up-the-source-environment"></a><span data-ttu-id="d9aff-106">Kaynak ortamı ayarlama</span><span class="sxs-lookup"><span data-stu-id="d9aff-106">Set up the source environment</span></span>

<span data-ttu-id="d9aff-107">Azure Site kurtarma sağlayıcısı VMM sunucularında yükleme ve bulmak ve sunucuları kasaya kaydetmek.</span><span class="sxs-lookup"><span data-stu-id="d9aff-107">Install the Azure Site Recovery Provider on VMM servers, and discover and register servers in the vault.</span></span>

1. <span data-ttu-id="d9aff-108">Tıklatın **1. adım: altyapıyı hazırlama** > **kaynak**.</span><span class="sxs-lookup"><span data-stu-id="d9aff-108">Click **Step 1: Prepare Infrastructure** > **Source**.</span></span>

    ![Kaynağı ayarlama](./media/vmm-to-vmm-walkthrough-source-target/goals-source.png)
2. <span data-ttu-id="d9aff-110">**Kaynağı ayarla** kısmında, bir VMM sunucusu eklemek için **+ VMM**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d9aff-110">In **Prepare source**, click **+ VMM** to add a VMM server.</span></span>

    ![Kaynağı ayarlama](./media/vmm-to-vmm-walkthrough-source-target/set-source1.png)
3. <span data-ttu-id="d9aff-112">İçinde **Sunucu Ekle**, denetleyin **System Center VMM sunucusunun** görünür **sunucu türü** ve VMM sunucusu karşılayan [Önkoşullar](#prerequisites).</span><span class="sxs-lookup"><span data-stu-id="d9aff-112">In **Add Server**, check that **System Center VMM server** appears in **Server type** and that the VMM server meets the [prerequisites](#prerequisites).</span></span>
4. <span data-ttu-id="d9aff-113">Azure Site Recovery Sağlayıcısı yükleme dosyasını indirin.</span><span class="sxs-lookup"><span data-stu-id="d9aff-113">Download the Azure Site Recovery Provider installation file.</span></span>
5. <span data-ttu-id="d9aff-114">Kayıt anahtarını indirin.</span><span class="sxs-lookup"><span data-stu-id="d9aff-114">Download the registration key.</span></span> <span data-ttu-id="d9aff-115">Kurulumu çalıştırırken buna ihtiyacınız olur.</span><span class="sxs-lookup"><span data-stu-id="d9aff-115">You need this when you run setup.</span></span> <span data-ttu-id="d9aff-116">Anahtar, oluşturulduktan sonra beş gün boyunca geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="d9aff-116">The key is valid for five days after you generate it.</span></span>

    ![Kaynağı ayarlama](./media/vmm-to-vmm-walkthrough-source-target/set-source3.png)
6. <span data-ttu-id="d9aff-118">VMM sunucusunda Azure Site Recovery Sağlayıcısı'nı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d9aff-118">Install the Azure Site Recovery Provider on the VMM server.</span></span> <span data-ttu-id="d9aff-119">Açıkça şey Hyper-V ana bilgisayar sunucuları üzerinde yüklemeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="d9aff-119">You don't need to explicitly install anything on Hyper-V host servers.</span></span>


## <a name="install-the-azure-site-recovery-provider"></a><span data-ttu-id="d9aff-120">Azure Site kurtarma Sağlayıcısı'nı yüklemek</span><span class="sxs-lookup"><span data-stu-id="d9aff-120">Install the Azure Site Recovery Provider</span></span>

1. <span data-ttu-id="d9aff-121">Sağlayıcı kurulum dosyasını her VMM sunucusunda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d9aff-121">Run the Provider setup file on each VMM server.</span></span> <span data-ttu-id="d9aff-122">VMM bir kümede dağıtılmışsa, aşağıdaki ilk yüklediğinizde yapın:</span><span class="sxs-lookup"><span data-stu-id="d9aff-122">If VMM is deployed in a cluster, do the following the first time you install:</span></span>
    -  <span data-ttu-id="d9aff-123">Etkin bir düğümde bir sağlayıcı yükleyin ve VMM sunucusunu kasaya kaydetmek için yüklemeyi sonlandırın.</span><span class="sxs-lookup"><span data-stu-id="d9aff-123">Install the provider on an active node, and finish the installation to register the VMM server in the vault.</span></span>
    - <span data-ttu-id="d9aff-124">Ardından, sağlayıcı diğer düğümlere yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d9aff-124">Then, install the Provider on the other nodes.</span></span> <span data-ttu-id="d9aff-125">Küme düğümlerini tüm sağlayıcının aynı sürümüne çalıştırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d9aff-125">Cluster nodes should all run the same version of the Provider.</span></span>
2. <span data-ttu-id="d9aff-126">Kurulum, birkaç ön koşul denetimlerini çalıştırır ve VMM hizmetini durdurmak için izin ister.</span><span class="sxs-lookup"><span data-stu-id="d9aff-126">Setup runs a few prerequisite checks, and requests permission to stop the VMM service.</span></span> <span data-ttu-id="d9aff-127">Kurulum bittiğinde VMM hizmeti otomatik olarak yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="d9aff-127">The VMM service will be restarted automatically when setup finishes.</span></span> <span data-ttu-id="d9aff-128">Bir VMM kümesinde yüklerseniz, küme rolünü durdurmanız istenir.</span><span class="sxs-lookup"><span data-stu-id="d9aff-128">If you install on a VMM cluster, you're prompted to stop the Cluster role.</span></span>
3. <span data-ttu-id="d9aff-129">İçinde **Microsoft Update**, sağlayıcı güncelleştirmeleri Microsoft Update ilkenize uygun yüklü olduğunu belirtmek için de seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d9aff-129">In **Microsoft Update**, you can opt in to specify that provider updates are installed in accordance with your Microsoft Update policy.</span></span>
4. <span data-ttu-id="d9aff-130">İçinde **yükleme**kabul edin veya varsayılan yükleme konumunu değiştirmek ve tıklatın **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="d9aff-130">In **Installation**, accept or modify the default installation location, and click **Install**.</span></span>

    ![Yükleme konumu](./media/vmm-to-vmm-walkthrough-source-target/provider-location.png)
5. <span data-ttu-id="d9aff-132">Yükleme tamamlandıktan sonra tıklayın **kaydetmek** sunucuyu kasaya kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="d9aff-132">After installation is complete, click **Register** to register the server in the vault.</span></span>

    ![Yükleme konumu](./media/vmm-to-vmm-walkthrough-source-target/provider-register.png)
6. <span data-ttu-id="d9aff-134">**Kasa adı** alanında, sunucunun kayıtlı olduğu kasanın adını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="d9aff-134">In **Vault name**, verify the name of the vault in which the server will be registered.</span></span> <span data-ttu-id="d9aff-135">*İleri*’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d9aff-135">Click *Next*.</span></span>

    ![Sunucu kaydı](./media/vmm-to-vmm-walkthrough-source-target/vaultcred.png)
7. <span data-ttu-id="d9aff-137">İçinde **Internet bağlantısı**, Azure'a VMM sunucusunda çalışan sağlayıcı nasıl bağlandığını belirtin.</span><span class="sxs-lookup"><span data-stu-id="d9aff-137">In **Internet Connection**, specify how the provider running on the VMM server connects to Azure.</span></span>

    ![İnternet Ayarları](./media/vmm-to-vmm-walkthrough-source-target/proxydetails.png)

   - <span data-ttu-id="d9aff-139">Sağlayıcı İnternete doğrudan ya da bir proxy üzerinden bağlanmalısınız belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d9aff-139">You can specify that the provider should connect directly to the internet, or via a proxy.</span></span>
   - <span data-ttu-id="d9aff-140">Gerekiyorsa proxy ayarlarını belirtin.</span><span class="sxs-lookup"><span data-stu-id="d9aff-140">Specify proxy settings if needed.</span></span>
   - <span data-ttu-id="d9aff-141">Bir proxy kullanıyorsanız, belirtilen proxy kimlik bilgileri kullanılarak otomatik olarak bir VMM RunAs hesabı (DRAProxyAccount) oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d9aff-141">If you use a proxy, a VMM RunAs account (DRAProxyAccount) is created automatically using the specified proxy credentials.</span></span> <span data-ttu-id="d9aff-142">Bu hesabın kimlik doğrulamasını başarıyla gerçekleştirebilmesi için ara sunucuyu yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="d9aff-142">Configure the proxy server so that this account can authenticate successfully.</span></span> <span data-ttu-id="d9aff-143">RunAs hesabı ayarları VMM konsolundan değiştirilebilir > **ayarları** > **güvenlik** > **farklı çalıştır hesapları**.</span><span class="sxs-lookup"><span data-stu-id="d9aff-143">The RunAs account settings can be modified in the VMM console > **Settings** > **Security** > **Run As Accounts**.</span></span> <span data-ttu-id="d9aff-144">Değişiklikleri güncelleştirme için VMM hizmetini yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="d9aff-144">Restart the VMM service to update changes.</span></span>
8. <span data-ttu-id="d9aff-145">**Kayıt Anahtarı** kısmında, Azure Site Recovery'den indirdiğiniz anahtarı seçin ve VMM sunucusuna kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="d9aff-145">In **Registration Key**, select the key that you downloaded from Azure Site Recovery and copied to the VMM server.</span></span>
9. <span data-ttu-id="d9aff-146">Şifreleme ayarı yalnızca Hyper-V sanal makinelerini Azure'daki VMM bulutlarına çoğaltırken kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d9aff-146">The encryption setting is only used when you're replicating Hyper-V VMs in VMM clouds to Azure.</span></span> <span data-ttu-id="d9aff-147">İkincil bir siteye çoğaltma yapıyorsanız kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="d9aff-147">If you're replicating to a secondary site it's not used.</span></span>
10. <span data-ttu-id="d9aff-148">**Sunucu adı** alanında, kasadaki VMM sunucusunu tanımlamak için bir kolay ad belirtin.</span><span class="sxs-lookup"><span data-stu-id="d9aff-148">In **Server name**, specify a friendly name to identify the VMM server in the vault.</span></span> <span data-ttu-id="d9aff-149">Küme yapılandırmasında VMM kümesi rolü adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="d9aff-149">In a cluster configuration specify the VMM cluster role name.</span></span>
11. <span data-ttu-id="d9aff-150">İçinde **Eşitle bulut meta verileri**VMM sunucusundaki tüm bulutların meta verilerini kasayla eşitlemek istediğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="d9aff-150">In **Synchronize cloud metadata**, select whether you want to synchronize metadata for all clouds on the VMM server with the vault.</span></span> <span data-ttu-id="d9aff-151">Bu eylemin her sunucuda yalnızca bir kez gerçekleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="d9aff-151">This action only needs to happen once on each server.</span></span> <span data-ttu-id="d9aff-152">Tüm Bulutları eşitlemek istemiyorsanız bu ayarı işaretsiz bırakın ve her Bulutu VMM konsolundaki bulut özelliklerinde tek tek eşitleyin.</span><span class="sxs-lookup"><span data-stu-id="d9aff-152">If you don't want to synchronize all clouds, you can leave this setting unchecked, and synchronize each cloud individually in the cloud properties in the VMM console.</span></span>
12. <span data-ttu-id="d9aff-153">İşlemi tamamlamak için **İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d9aff-153">Click **Next** to complete the process.</span></span> <span data-ttu-id="d9aff-154">Kayıttan sonra Azure Site Recovery tarafından VMM sunucusundan meta veriler alınır.</span><span class="sxs-lookup"><span data-stu-id="d9aff-154">After registration, metadata from the VMM server is retrieved by Azure Site Recovery.</span></span> <span data-ttu-id="d9aff-155">Sunucu, kasadaki **Sunucular** sayfasında **VMM Sunucuları** sekmesinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d9aff-155">The server is displayed on the **VMM Servers** tab on the **Servers** page in the vault.</span></span>

    ![Sunucu](./media/vmm-to-vmm-walkthrough-source-target/provider13.png)
13. <span data-ttu-id="d9aff-157">Sunucu Site Recovery konsolunda kullanılabilir duruma getirildikten sonra **kaynak** > **kaynağı** VMM sunucusunu seçin ve Hyper-V konağı bulunduğu Bulutu seçin.</span><span class="sxs-lookup"><span data-stu-id="d9aff-157">After the server is available in the Site Recovery console, in **Source** > **Prepare source** select the VMM server, and select the cloud in which the Hyper-V host is located.</span></span> <span data-ttu-id="d9aff-158">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d9aff-158">Then click **OK**.</span></span>

<span data-ttu-id="d9aff-159">Sağlayıcı komut satırından da yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d9aff-159">You can also install the provider from the command line:</span></span>

[!INCLUDE [site-recovery-rw-provider-command-line](../../includes/site-recovery-rw-provider-command-line.md)]


## <a name="set-up-the-target-environment"></a><span data-ttu-id="d9aff-160">Hedef ortamı ayarlama</span><span class="sxs-lookup"><span data-stu-id="d9aff-160">Set up the target environment</span></span>

<span data-ttu-id="d9aff-161">Hedef VMM sunucusunu ve Bulutu seçin:</span><span class="sxs-lookup"><span data-stu-id="d9aff-161">Select the target VMM server and cloud:</span></span>

1. <span data-ttu-id="d9aff-162">Tıklatın **altyapıyı hazırlama** > **hedef**ve kullanmak istediğiniz hedef VMM sunucusunu seçin.</span><span class="sxs-lookup"><span data-stu-id="d9aff-162">Click **Prepare infrastructure** > **Target**, and select the target VMM server you want to use.</span></span>
2. <span data-ttu-id="d9aff-163">Site Recovery ile eşitlenmiş Bulutlar sunucuda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d9aff-163">Clouds on the server that are synchronized with Site Recovery will be displayed.</span></span> <span data-ttu-id="d9aff-164">Hedef bulut seçin.</span><span class="sxs-lookup"><span data-stu-id="d9aff-164">Select the target cloud.</span></span>

   ![Hedef](./media/vmm-to-vmm-walkthrough-source-target/target-vmm.png)



## <a name="next-steps"></a><span data-ttu-id="d9aff-166">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d9aff-166">Next steps</span></span>

<span data-ttu-id="d9aff-167">Git [adım 7: ağ eşlemesini yapılandırma](vmm-to-vmm-walkthrough-network-mapping.md).</span><span class="sxs-lookup"><span data-stu-id="d9aff-167">Go to [Step 7: Configure network mapping](vmm-to-vmm-walkthrough-network-mapping.md).</span></span>
