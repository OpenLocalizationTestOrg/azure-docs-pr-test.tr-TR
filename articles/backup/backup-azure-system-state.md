---
title: "Windows sistem durumu tooAzure yukarı aaaBack | Microsoft Docs"
description: "Merhaba sistem durumunu Windows Server ve/veya Windows bilgisayarları tooAzure tooback öğrenin."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: carmonm
editor: 
keywords: "nasıl toobackup; nasıl tooback; Yedekleme dosyaları ve klasörleri"
ms.assetid: 5b15ebf1-2214-4722-b937-96e2be8872bb
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: saurse;markgal
ms.openlocfilehash: be5d4be81af981c10de82add9fe962a730753cf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-windows-system-state-in-resource-manager-deployment"></a><span data-ttu-id="80daf-104">Resource Manager dağıtım Windows sistem durumu yedekleme</span><span class="sxs-lookup"><span data-stu-id="80daf-104">Back up Windows system state in Resource Manager deployment</span></span>
<span data-ttu-id="80daf-105">Bu makalede, Windows Server sisteminizi tooback durum tooAzure nasıl açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="80daf-105">This article explains how tooback up your Windows Server system state tooAzure.</span></span> <span data-ttu-id="80daf-106">Eğitmen hedeflenen toowalk olan hello temel bilgileri size.</span><span class="sxs-lookup"><span data-stu-id="80daf-106">It's a tutorial intended toowalk you through hello basics.</span></span>

<span data-ttu-id="80daf-107">Tooknow Azure yedekleme hakkında daha fazla bilgi istiyorsanız, bu okuma [genel bakış](backup-introduction-to-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="80daf-107">If you want tooknow more about Azure Backup, read this [overview](backup-introduction-to-azure-backup.md).</span></span>

<span data-ttu-id="80daf-108">Azure aboneliğiniz yoksa istediğiniz Azure hizmetine erişmenizi sağlayan [ücretsiz bir hesap](https://azure.microsoft.com/free/) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="80daf-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) that lets you access any Azure service.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="80daf-109">Kurtarma hizmetleri kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="80daf-109">Create a recovery services vault</span></span>
<span data-ttu-id="80daf-110">tooback dosya ve klasörleri toocreate toostore hello verilerin istediğiniz hello bölgede bir kurtarma Hizmetleri kasası gerekir.</span><span class="sxs-lookup"><span data-stu-id="80daf-110">tooback up your files and folders, you need toocreate a Recovery Services vault in hello region where you want toostore hello data.</span></span> <span data-ttu-id="80daf-111">Çoğaltılan depolama alanınızın nasıl istediğiniz toodetermine de gerekir.</span><span class="sxs-lookup"><span data-stu-id="80daf-111">You also need toodetermine how you want your storage replicated.</span></span>

### <a name="toocreate-a-recovery-services-vault"></a><span data-ttu-id="80daf-112">toocreate bir kurtarma Hizmetleri kasası</span><span class="sxs-lookup"><span data-stu-id="80daf-112">toocreate a Recovery Services vault</span></span>
1. <span data-ttu-id="80daf-113">Zaten yapmadıysanız, toohello içinde oturum [Azure Portal](https://portal.azure.com/) Azure aboneliğinizi kullanarak.</span><span class="sxs-lookup"><span data-stu-id="80daf-113">If you haven't already done so, sign in toohello [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="80daf-114">Merhaba Hub menüsünde **daha fazla hizmet** ve kaynakları hello listesinde yazın **kurtarma Hizmetleri** tıklatıp **kurtarma Hizmetleri kasaları**.</span><span class="sxs-lookup"><span data-stu-id="80daf-114">On hello Hub menu, click **More services** and in hello list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![Kurtarma Hizmetleri Kasası oluşturma 1. adım](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="80daf-116">Merhaba abonelikte kurtarma Hizmetleri kasaları varsa hello kasalarını listelenir.</span><span class="sxs-lookup"><span data-stu-id="80daf-116">If there are recovery services vaults in hello subscription, hello vaults are listed.</span></span>
3. <span data-ttu-id="80daf-117">Merhaba üzerinde **kurtarma Hizmetleri kasaları** menüsünde tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="80daf-117">On hello **Recovery Services vaults** menu, click **Add**.</span></span>

    ![Kurtarma Hizmetleri Kasası oluşturma 2. adım](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="80daf-119">Merhaba kurtarma Hizmetleri kasası dikey penceresi açılır tooprovide isteyen bir **adı**, **abonelik**, **kaynak grubu**, ve **konumu**.</span><span class="sxs-lookup"><span data-stu-id="80daf-119">hello Recovery Services vault blade opens, prompting you tooprovide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Kurtarma Hizmetleri Kasası Oluşturma 3. adım](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="80daf-121">İçin **adı**, bir kolay ad tooidentify hello kasası girin.</span><span class="sxs-lookup"><span data-stu-id="80daf-121">For **Name**, enter a friendly name tooidentify hello vault.</span></span> <span data-ttu-id="80daf-122">Merhaba adı toobe hello Azure aboneliği için benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="80daf-122">hello name needs toobe unique for hello Azure subscription.</span></span> <span data-ttu-id="80daf-123">2 ila 50 karakterden oluşan bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="80daf-123">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="80daf-124">Ad bir harf ile başlamalıdır ve yalnızca harf, rakam ve kısa çizgi içerebilir.</span><span class="sxs-lookup"><span data-stu-id="80daf-124">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="80daf-125">Merhaba, **abonelik** bölümünde, hello açılır menü toochoose hello Azure aboneliği kullanın.</span><span class="sxs-lookup"><span data-stu-id="80daf-125">In hello **Subscription** section, use hello drop-down menu toochoose hello Azure subscription.</span></span> <span data-ttu-id="80daf-126">Yalnızca bir abonelik kullanırsanız, bu abonelik görünür ve toohello sonraki adımı atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="80daf-126">If you use only one subscription, that subscription appears and you can skip toohello next step.</span></span> <span data-ttu-id="80daf-127">Hangi abonelik toouse emin değilseniz, hello varsayılan kullanın (veya önerilen) aboneliği.</span><span class="sxs-lookup"><span data-stu-id="80daf-127">If you are not sure which subscription toouse, use hello default (or suggested) subscription.</span></span> <span data-ttu-id="80daf-128">Yalnızca kuruluş hesabınızın birden çok Azure aboneliği ile ilişkili olması durumunda birden çok seçenek olur.</span><span class="sxs-lookup"><span data-stu-id="80daf-128">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="80daf-129">Merhaba, **kaynak grubu** bölümü:</span><span class="sxs-lookup"><span data-stu-id="80daf-129">In hello **Resource group** section:</span></span>

    * <span data-ttu-id="80daf-130">seçin **Yeni Oluştur** toocreate bir kaynak grubu istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="80daf-130">select **Create new** if you want toocreate a Resource group.</span></span>
    <span data-ttu-id="80daf-131">Veya</span><span class="sxs-lookup"><span data-stu-id="80daf-131">Or</span></span>
    * <span data-ttu-id="80daf-132">seçin **var olanı kullan** ve hello açılır menü toosee hello kullanılabilir kaynak gruplarının listesini'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="80daf-132">select **Use existing** and click hello drop-down menu toosee hello available list of Resource groups.</span></span>

  <span data-ttu-id="80daf-133">Kaynak grupları hakkında tam bilgi için bkz: Merhaba [Azure Resource Manager'a genel bakış](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="80daf-133">For complete information on Resource groups, see hello [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="80daf-134">Tıklatın **konumu** tooselect hello hello kasa için coğrafi bölgeyi.</span><span class="sxs-lookup"><span data-stu-id="80daf-134">Click **Location** tooselect hello geographic region for hello vault.</span></span> <span data-ttu-id="80daf-135">Bu seçim, yedekleme verilerinizi burada gönderilen hello coğrafi bölgeyi belirler.</span><span class="sxs-lookup"><span data-stu-id="80daf-135">This choice determines hello geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="80daf-136">Merhaba kurtarma Hizmetleri kasası dikey penceresinde Hello altındaki tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="80daf-136">At hello bottom of hello Recovery Services vault blade, click **Create**.</span></span>

    <span data-ttu-id="80daf-137">Oluşturulan toobe kurtarma Hizmetleri kasası hello için birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="80daf-137">It can take several minutes for hello Recovery Services vault toobe created.</span></span> <span data-ttu-id="80daf-138">Merhaba portal hello üst sağ bölmesinde Hello durum bildirimlerini izleyin.</span><span class="sxs-lookup"><span data-stu-id="80daf-138">Monitor hello status notifications in hello upper right-hand area of hello portal.</span></span> <span data-ttu-id="80daf-139">Kasanız oluşturulduktan sonra hello kurtarma Hizmetleri kasaları listesinde görünür.</span><span class="sxs-lookup"><span data-stu-id="80daf-139">Once your vault is created, it appears in hello list of Recovery Services vaults.</span></span> <span data-ttu-id="80daf-140">Birkaç dakika sonra kasayı görmezseniz **Yenile**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="80daf-140">If after several minutes you don't see your vault, click **Refresh**.</span></span>

    ![Yenile düğmesine tıklayın](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    <span data-ttu-id="80daf-142">Kasanızı kurtarma Hizmetleri kasalarının hello listesinde gördüğünüz verdikten sonra hazır tooset hello depolama artıklığı demektir.</span><span class="sxs-lookup"><span data-stu-id="80daf-142">Once you see your vault in hello list of Recovery Services vaults, you are ready tooset hello storage redundancy.</span></span>

### <a name="set-storage-redundancy-for-hello-vault"></a><span data-ttu-id="80daf-143">Depolama artıklığı hello kasası için ayarlama</span><span class="sxs-lookup"><span data-stu-id="80daf-143">Set storage redundancy for hello vault</span></span>
<span data-ttu-id="80daf-144">Kurtarma Hizmetleri kasası oluşturduğunuzda, depolama artıklığı istediğiniz yapılandırılmış hello biçimde olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="80daf-144">When you create a Recovery Services vault, make sure storage redundancy is configured hello way you want.</span></span>

1. <span data-ttu-id="80daf-145">Merhaba gelen **kurtarma Hizmetleri kasaları** dikey penceresinde hello yeni kasaya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="80daf-145">From hello **Recovery Services vaults** blade, click hello new vault.</span></span>

    ![Kurtarma Hizmetleri kasası hello listeden Hello yeni kasa seçin](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="80daf-147">Merhaba kasası seçtiğinizde hello **kurtarma Hizmetleri kasası** dikey daraltır ve hello ayarları dikey (*hello üstünde hello kasasının hello ada sahip*) ve hello kasa Ayrıntılar dikey penceresini açın.</span><span class="sxs-lookup"><span data-stu-id="80daf-147">When you select hello vault, hello **Recovery Services vault** blade narrows, and hello Settings blade (*which has hello name of hello vault at hello top*) and hello vault details blade open.</span></span>

    ![Yeni kasa için Görünüm hello depolama yapılandırması](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)
2. <span data-ttu-id="80daf-149">Merhaba yeni kasasının ayarlar dikey penceresinde hello dikey slayt tooscroll toohello Yönet bölümüne aşağı kullanın ve'ı tıklatın **Yedekleme Altyapısı**.</span><span class="sxs-lookup"><span data-stu-id="80daf-149">In hello new vault's Settings blade, use hello vertical slide tooscroll down toohello Manage section, and click **Backup Infrastructure**.</span></span>
    <span data-ttu-id="80daf-150">Merhaba yedekleme altyapısı dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="80daf-150">hello Backup Infrastructure blade opens.</span></span>
3. <span data-ttu-id="80daf-151">Merhaba yedekleme altyapısı dikey penceresinde tıklayın **yedekleme yapılandırması** tooopen hello **yedekleme yapılandırması** dikey.</span><span class="sxs-lookup"><span data-stu-id="80daf-151">In hello Backup Infrastructure blade, click **Backup Configuration** tooopen hello **Backup Configuration** blade.</span></span>

    ![Yeni kasa Hello depolama yapılandırmasını ayarlayın](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. <span data-ttu-id="80daf-153">Kasanız için Hello uygun depolama çoğaltma seçeneğini seçin.</span><span class="sxs-lookup"><span data-stu-id="80daf-153">Choose hello appropriate storage replication option for your vault.</span></span>

    ![depolama yapılandırması seçenekleri](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    <span data-ttu-id="80daf-155">Varsayılan olarak, kasanız coğrafi olarak yedekli depolamaya sahiptir.</span><span class="sxs-lookup"><span data-stu-id="80daf-155">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="80daf-156">Azure birincil yedekleme alanı uç noktası kullanıyorsanız, toouse devam **coğrafi olarak yedekli**.</span><span class="sxs-lookup"><span data-stu-id="80daf-156">If you use Azure as a primary backup storage endpoint, continue toouse **Geo-redundant**.</span></span> <span data-ttu-id="80daf-157">Birincil yedekleme alanı uç noktası Azure kullanmıyorsanız, ardından **yerel olarak yedekli**, hello Azure depolama maliyetlerini azaltır.</span><span class="sxs-lookup"><span data-stu-id="80daf-157">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces hello Azure storage costs.</span></span> <span data-ttu-id="80daf-158">[Coğrafi olarak yedekli](../storage/common/storage-redundancy.md#geo-redundant-storage) ve [yerel olarak yedekli](../storage/common/storage-redundancy.md#locally-redundant-storage) depolama seçenekleri hakkında daha fazla bilgiyi [Depolama yedekliliğine genel bakış](../storage/common/storage-redundancy.md) bölümünden edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="80daf-158">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="80daf-159">Bir kasa oluşturduğunuza göre Windows sistem durumunu yedekleme için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="80daf-159">Now that you've created a vault, configure it for backing up Windows System State.</span></span>

## <a name="configure-hello-vault"></a><span data-ttu-id="80daf-160">Merhaba kasası yapılandırma</span><span class="sxs-lookup"><span data-stu-id="80daf-160">Configure hello vault</span></span>
1. <span data-ttu-id="80daf-161">Açık kurtarma Hizmetleri kasası dikey (Merhaba kasa), yeni oluşturduğunuz, hello Başlarken bölümünde Merhaba, tıklatın **yedekleme**, sonra da hello **yedekleme ile çalışmaya başlama** dikey penceresinde, select  **Yedekleme hedefi**.</span><span class="sxs-lookup"><span data-stu-id="80daf-161">On hello Recovery Services vault blade (for hello vault you just created), in hello Getting Started section, click **Backup**, then on hello **Getting Started with Backup** blade, select **Backup goal**.</span></span>

    ![Yedekleme hedefi dikey penceresini açma](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

    <span data-ttu-id="80daf-163">Merhaba **yedekleme hedefi** dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="80daf-163">hello **Backup Goal** blade opens.</span></span>

    ![Yedekleme hedefi dikey penceresini açma](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="80daf-165">Merhaba gelen **, iş yükünü çalıştırdığı?** açılır menüsünde, select **şirket içi**.</span><span class="sxs-lookup"><span data-stu-id="80daf-165">From hello **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

    <span data-ttu-id="80daf-166">Windows Server veya Windows bilgisayarınız Azure üzerinde olmayan fiziksel bir makine olduğu için **Şirket içi** seçeneğini belirlersiniz.</span><span class="sxs-lookup"><span data-stu-id="80daf-166">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="80daf-167">Merhaba gelen **neler toobackup istediğiniz?** menüsünde, select **sistem durumu**, tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="80daf-167">From hello **What do you want toobackup?** menu, select **System State**, and click **OK**.</span></span>

    ![Dosya ve klasörleri yedekleme](./media/backup-azure-system-state/backup-goal-system-state.png)

    <span data-ttu-id="80daf-169">Tamam'ı tıklattıktan sonra bir onay işareti çok sonraki görünür**yedekleme hedefi**ve hello **altyapıyı hazırlama** dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="80daf-169">After clicking OK, a checkmark appears next too**Backup goal**, and hello **Prepare infrastructure** blade opens.</span></span>

    ![Yedekleme hedefi yapılandırılmıştır, bundan sonra altyapıyı hazırlayın](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="80daf-171">Merhaba üzerinde **altyapıyı hazırlama** dikey penceresinde tıklatın **karşıdan aracısı için Windows Server veya Windows İstemcisi**.</span><span class="sxs-lookup"><span data-stu-id="80daf-171">On hello **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

    ![altyapıyı hazırlama](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

    <span data-ttu-id="80daf-173">Windows Server temel kullanıyorsanız, Windows Server temel için toodownload hello Aracısı seçin.</span><span class="sxs-lookup"><span data-stu-id="80daf-173">If you are using Windows Server Essential, then choose toodownload hello agent for Windows Server Essential.</span></span> <span data-ttu-id="80daf-174">Açılır menü toorun komut istemleri veya MARSAgentInstaller.exe kaydedin.</span><span class="sxs-lookup"><span data-stu-id="80daf-174">A pop-up menu prompts you toorun or save MARSAgentInstaller.exe.</span></span>

    ![MARSAgentInstaller iletişim kutusu](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="80daf-176">Merhaba indirme açılır menüsünde tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="80daf-176">In hello download pop-up menu, click **Save**.</span></span>

    <span data-ttu-id="80daf-177">Varsayılan olarak, hello **MARSagentinstaller.exe** dosya tooyour indirmeler klasörüne kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="80daf-177">By default, hello **MARSagentinstaller.exe** file is saved tooyour Downloads folder.</span></span> <span data-ttu-id="80daf-178">Merhaba yükleyici tamamladığında, toorun hello yükleyici istediğiniz veya hello klasörünü açın, isteyen bir açılır pencere görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="80daf-178">When hello installer completes, you will see a pop-up asking if you want toorun hello installer, or open hello folder.</span></span>

    ![altyapıyı hazırlama](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

    <span data-ttu-id="80daf-180">Tooinstall hello Aracısı henüz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="80daf-180">You don't need tooinstall hello agent yet.</span></span> <span data-ttu-id="80daf-181">Merhaba kasa kimlik bilgileri indirdikten sonra hello aracısını yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="80daf-181">You can install hello agent after you have downloaded hello vault credentials.</span></span>

6. <span data-ttu-id="80daf-182">Merhaba üzerinde **altyapıyı hazırlama** dikey penceresinde tıklatın **karşıdan**.</span><span class="sxs-lookup"><span data-stu-id="80daf-182">On hello **Prepare infrastructure** blade, click **Download**.</span></span>

    ![kasa kimlik bilgilerini indirme](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

    <span data-ttu-id="80daf-184">Merhaba kasa kimlik bilgileri tooyour indirmeler klasörüne indirin.</span><span class="sxs-lookup"><span data-stu-id="80daf-184">hello vault credentials download tooyour Downloads folder.</span></span> <span data-ttu-id="80daf-185">Hello kasa kimlik bilgilerini indirme işlemini tamamladıktan sonra tooopen istediğiniz veya hello kimlik bilgilerini Kaydet isteyen bir açılır pencere görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="80daf-185">After hello vault credentials finish downloading, you see a pop-up asking if you want tooopen or save hello credentials.</span></span> <span data-ttu-id="80daf-186">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="80daf-186">Click **Save**.</span></span> <span data-ttu-id="80daf-187">Yanlışlıkla tıklatırsanız **açık**, tooopen hello kasa kimlik bilgileri çalışır hello iletişim sağlar, başarısız.</span><span class="sxs-lookup"><span data-stu-id="80daf-187">If you accidentally click **Open**, let hello dialog that attempts tooopen hello vault credentials, fail.</span></span> <span data-ttu-id="80daf-188">Merhaba kasa kimlik bilgileri açamıyor.</span><span class="sxs-lookup"><span data-stu-id="80daf-188">You cannot open hello vault credentials.</span></span> <span data-ttu-id="80daf-189">Toohello sonraki adıma geçin.</span><span class="sxs-lookup"><span data-stu-id="80daf-189">Proceed toohello next step.</span></span> <span data-ttu-id="80daf-190">Merhaba kasa kimlik bilgileri hello indirme klasöründe yer alır.</span><span class="sxs-lookup"><span data-stu-id="80daf-190">hello vault credentials are in hello Downloads folder.</span></span>   

    ![kasa kimlik bilgilerini indirme tamamlandı](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-hello-agent"></a><span data-ttu-id="80daf-192">Yükleme ve hello Aracısı kaydedin</span><span class="sxs-lookup"><span data-stu-id="80daf-192">Install and register hello agent</span></span>

> [!NOTE]
> <span data-ttu-id="80daf-193">Hello Azure portal üzerinden yedeklemeyi etkinleştirme olanağı henüz kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="80daf-193">Enabling backup through hello Azure portal is not available, yet.</span></span> <span data-ttu-id="80daf-194">Windows Server sistem durumu yedeklemesi Hello Microsoft Azure kurtarma Hizmetleri Aracısı tooback kullanın.</span><span class="sxs-lookup"><span data-stu-id="80daf-194">Use hello Microsoft Azure Recovery Services Agent tooback up Windows Server System State.</span></span>
>

1. <span data-ttu-id="80daf-195">Bulun ve çift hello **MARSagentinstaller.exe** hello yükleme klasöründen (veya diğer kayıtlı konumdan).</span><span class="sxs-lookup"><span data-stu-id="80daf-195">Locate and double-click hello **MARSagentinstaller.exe** from hello Downloads folder (or other saved location).</span></span>

    <span data-ttu-id="80daf-196">Merhaba yükleyici, bir dizi ileti ayıklar gibi yükler ve hello kurtarma Hizmetleri aracısını kaydeder sağlar.</span><span class="sxs-lookup"><span data-stu-id="80daf-196">hello installer provides a series of messages as it extracts, installs, and registers hello Recovery Services agent.</span></span>

    ![Kurtarma Hizmetleri aracısı yükleyici kimlik bilgilerini çalıştırma](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="80daf-198">Merhaba Microsoft Azure kurtarma Hizmetleri Aracısı Kurulum Sihirbazı tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="80daf-198">Complete hello Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="80daf-199">toocomplete Başlangıç Sihirbazı, şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="80daf-199">toocomplete hello wizard, you need to:</span></span>

   * <span data-ttu-id="80daf-200">Merhaba yükleme ve önbellek klasörü için bir konum seçin.</span><span class="sxs-lookup"><span data-stu-id="80daf-200">Choose a location for hello installation and cache folder.</span></span>
   * <span data-ttu-id="80daf-201">Bir proxy sunucu tooconnect toohello kullanırsanız, Ara sunucu bilgilerinizi sağlayın Internet.</span><span class="sxs-lookup"><span data-stu-id="80daf-201">Provide your proxy server info if you use a proxy server tooconnect toohello internet.</span></span>
   * <span data-ttu-id="80daf-202">Kimliği doğrulanmış bir ara sunucu kullanıyorsanız kullanıcı adı ve parola bilgilerinizi sağlayın.</span><span class="sxs-lookup"><span data-stu-id="80daf-202">Provide your user name and password details if you use an authenticated proxy.</span></span>
   * <span data-ttu-id="80daf-203">Merhaba indirilen kasa kimlik bilgilerini sağlayın</span><span class="sxs-lookup"><span data-stu-id="80daf-203">Provide hello downloaded vault credentials</span></span>
   * <span data-ttu-id="80daf-204">Merhaba şifreleme parolası güvenli bir konuma kaydedin.</span><span class="sxs-lookup"><span data-stu-id="80daf-204">Save hello encryption passphrase in a secure location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="80daf-205">Kaybeder veya hello parolayı unutursanız Microsoft hello yedekleme verilerini kurtarmanıza yardımcı olamaz.</span><span class="sxs-lookup"><span data-stu-id="80daf-205">If you lose or forget hello passphrase, Microsoft cannot help recover hello backup data.</span></span> <span data-ttu-id="80daf-206">Merhaba dosyayı güvenli bir konuma kaydedin.</span><span class="sxs-lookup"><span data-stu-id="80daf-206">Save hello file in a secure location.</span></span> <span data-ttu-id="80daf-207">Gerekli toorestore bir yedekleme olur.</span><span class="sxs-lookup"><span data-stu-id="80daf-207">It is required toorestore a backup.</span></span>
     >
     >

<span data-ttu-id="80daf-208">Merhaba aracı artık yüklenmiş ve kayıtlı toohello kasasına makineniz olduğu.</span><span class="sxs-lookup"><span data-stu-id="80daf-208">hello agent is now installed and your machine is registered toohello vault.</span></span> <span data-ttu-id="80daf-209">Hazır tooconfigure olduğunuz ve yedekleme zamanlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="80daf-209">You're ready tooconfigure and schedule your backup.</span></span>

## <a name="back-up-windows-server-system-state-preview"></a><span data-ttu-id="80daf-210">Windows Server sistem durumunu (Önizleme) yedekleme</span><span class="sxs-lookup"><span data-stu-id="80daf-210">Back up Windows Server System State (Preview)</span></span>
<span data-ttu-id="80daf-211">Merhaba ilk yedekleme üç görevleri içerir:</span><span class="sxs-lookup"><span data-stu-id="80daf-211">hello initial backup includes three tasks:</span></span>

* <span data-ttu-id="80daf-212">Sistem durumu yedeklemesi hello Azure Backup aracısını kullanan etkinleştir</span><span class="sxs-lookup"><span data-stu-id="80daf-212">Enable System State Backup using hello Azure Backup agent</span></span>
* <span data-ttu-id="80daf-213">Merhaba yedekleme zamanlaması</span><span class="sxs-lookup"><span data-stu-id="80daf-213">Schedule hello backup</span></span>
* <span data-ttu-id="80daf-214">Dosya ve klasörleri hello için ilk kez yedekleme</span><span class="sxs-lookup"><span data-stu-id="80daf-214">Back up files and folders for hello first time</span></span>

<span data-ttu-id="80daf-215">toocomplete hello ilk yedekleme, kullanım hello Microsoft Azure kurtarma Hizmetleri Aracısı.</span><span class="sxs-lookup"><span data-stu-id="80daf-215">toocomplete hello initial backup, use hello Microsoft Azure Recovery Services agent.</span></span>

### <a name="tooenable-system-state-backup-using-hello-azure-backup-agent"></a><span data-ttu-id="80daf-216">tooenable sistem durumu yedeklemesi Hello Azure yedekleme Aracısı'nı kullanma</span><span class="sxs-lookup"><span data-stu-id="80daf-216">tooenable System State backup using hello Azure Backup agent</span></span>

1. <span data-ttu-id="80daf-217">Bir PowerShell oturumunda komut toostop hello Azure yedekleme altyapısı aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="80daf-217">In a PowerShell session, run hello following command toostop hello Azure Backup engine.</span></span>

  ```
  PS C:\> Net stop obengine
  ```

2. <span data-ttu-id="80daf-218">Merhaba Windows kayıt defterini açın.</span><span class="sxs-lookup"><span data-stu-id="80daf-218">Open hello Windows Registry.</span></span>

  ```
  PS C:\> regedit.exe
  ```

3. <span data-ttu-id="80daf-219">Aşağıdaki kayıt defteri anahtarı hello hello DWord değerini belirtilen ekleyin.</span><span class="sxs-lookup"><span data-stu-id="80daf-219">Add hello following registry key with hello specified DWord Value.</span></span>

  | <span data-ttu-id="80daf-220">Kayıt defteri yolu</span><span class="sxs-lookup"><span data-stu-id="80daf-220">Registry path</span></span> | <span data-ttu-id="80daf-221">Kayıt defteri anahtarı</span><span class="sxs-lookup"><span data-stu-id="80daf-221">Registry key</span></span> | <span data-ttu-id="80daf-222">DWord değeri</span><span class="sxs-lookup"><span data-stu-id="80daf-222">DWord value</span></span> |
  |---------------|--------------|-------------|
  | <span data-ttu-id="80daf-223">HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span><span class="sxs-lookup"><span data-stu-id="80daf-223">HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span></span> | <span data-ttu-id="80daf-224">TurnOffSSBFeature</span><span class="sxs-lookup"><span data-stu-id="80daf-224">TurnOffSSBFeature</span></span> | <span data-ttu-id="80daf-225">2</span><span class="sxs-lookup"><span data-stu-id="80daf-225">2</span></span> |

4. <span data-ttu-id="80daf-226">Yükseltilmiş bir komut istemi komutunda aşağıdaki hello yürüterek Hello Backup altyapısını yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="80daf-226">Restart hello Backup engine by executing hello following command in an elevated command prompt.</span></span>

  ```
  PS C:\> Net start obengine
  ```

### <a name="tooschedule-hello-backup-job"></a><span data-ttu-id="80daf-227">tooschedule hello yedekleme işi</span><span class="sxs-lookup"><span data-stu-id="80daf-227">tooschedule hello backup job</span></span>

1. <span data-ttu-id="80daf-228">Merhaba Microsoft Azure kurtarma Hizmetleri Aracısı'nı açın.</span><span class="sxs-lookup"><span data-stu-id="80daf-228">Open hello Microsoft Azure Recovery Services agent.</span></span> <span data-ttu-id="80daf-229">Bunu, makinenizde **Microsoft Azure Backup** aramasını yaparak bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="80daf-229">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Hello Azure kurtarma Hizmetleri aracısını başlatma](./media/backup-try-azure-backup-in-10-mins/snap-in-search.png)

2. <span data-ttu-id="80daf-231">Merhaba kurtarma Hizmetleri aracısında tıklatın **yedekleme zamanlaması**.</span><span class="sxs-lookup"><span data-stu-id="80daf-231">In hello Recovery Services agent, click **Schedule Backup**.</span></span>

    ![Windows Server yedeklemesini zamanlama](./media/backup-try-azure-backup-in-10-mins/schedule-first-backup.png)

3. <span data-ttu-id="80daf-233">Merhaba üzerinde hello yedeklemeyi Zamanlama Sihirbazı sayfasında Başlarken, tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="80daf-233">On hello Getting started page of hello Schedule Backup Wizard, click **Next**.</span></span>

4. <span data-ttu-id="80daf-234">Merhaba öğeleri seçin tooBackup sayfasında, tıklatın **öğeleri Ekle**.</span><span class="sxs-lookup"><span data-stu-id="80daf-234">On hello Select Items tooBackup page, click **Add Items**.</span></span>

5. <span data-ttu-id="80daf-235">Seçin **sistem durumu** ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="80daf-235">Select **System State** and then click **OK**.</span></span>

6. <span data-ttu-id="80daf-236">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="80daf-236">Click **Next**.</span></span>

7. <span data-ttu-id="80daf-237">Merhaba sistem durumu yedekleme ve bekletme zamanlama otomatik olarak her Pazar yukarı tooback 9:00 PM yerel zaman olarak ayarlanır ve hello Bekletme dönemi olarak ayarlanmış too60 gün.</span><span class="sxs-lookup"><span data-stu-id="80daf-237">hello System State Backup and Retention schedule is automatically set tooback up every Sunday at 9:00 PM local time, and hello retention period is set too60 days.</span></span>

   > [!NOTE]
   > <span data-ttu-id="80daf-238">Sistem Durumu yedekleme ve bekletme ilkesi otomatik olarak yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="80daf-238">System State backup and retention policy is automatically configured.</span></span> <span data-ttu-id="80daf-239">Dosyaları ve klasörleri ayrıca toohello Windows Server sistem durumu yedekleme dosyası yedeklerini hello Sihirbazı'ndan için yalnızca hello yedekleme ve bekletme ilkesi belirtin.</span><span class="sxs-lookup"><span data-stu-id="80daf-239">If you back up Files and Folders in addition toohello Windows Server System State, specify only hello Backup and Retention policy for file backups from hello wizard.</span></span> 
   >

8. <span data-ttu-id="80daf-240">Merhaba onay sayfasında hello bilgileri gözden geçirin ve ardından **son**.</span><span class="sxs-lookup"><span data-stu-id="80daf-240">On hello Confirmation page, review hello information, and then click **Finish**.</span></span>

9. <span data-ttu-id="80daf-241">Merhaba Sihirbazı hello yedekleme zamanlamasını oluşturduktan sonra tıklayın **Kapat**.</span><span class="sxs-lookup"><span data-stu-id="80daf-241">After hello wizard finishes creating hello backup schedule, click **Close**.</span></span>

### <a name="tooback-up-windows-server-system-state-for-hello-first-time"></a><span data-ttu-id="80daf-242">Windows Server sistem durumunun tooback hello ilk kez için</span><span class="sxs-lookup"><span data-stu-id="80daf-242">tooback up Windows Server System State for hello first time</span></span>

1. <span data-ttu-id="80daf-243">Windows Server için bir yeniden başlatma gerektiren bekleyen güncelleştirme bulunmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="80daf-243">Make sure there are no pending updates for Windows Server that require a reboot.</span></span>

2. <span data-ttu-id="80daf-244">Merhaba kurtarma Hizmetleri aracısında tıklatın **Şimdi Yedekle** toocomplete hello hello ağ üzerinden dengeli ilk.</span><span class="sxs-lookup"><span data-stu-id="80daf-244">In hello Recovery Services agent, click **Back Up Now** toocomplete hello initial seeding over hello network.</span></span>

    ![Windows Server şimdi yedekle](./media/backup-try-azure-backup-in-10-mins/backup-now.png)

3. <span data-ttu-id="80daf-246">Merhaba onay sayfasında, Şimdi Yedekle sihirbazı hello hello ayarları gözden geçir hello makineyi tooback kullanır.</span><span class="sxs-lookup"><span data-stu-id="80daf-246">On hello Confirmation page, review hello settings that hello Back Up Now Wizard will use tooback up hello machine.</span></span> <span data-ttu-id="80daf-247">Ardından **Yedekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="80daf-247">Then click **Back Up**.</span></span>

4. <span data-ttu-id="80daf-248">Tıklatın **Kapat** tooclose hello Sihirbazı.</span><span class="sxs-lookup"><span data-stu-id="80daf-248">Click **Close** tooclose hello wizard.</span></span> <span data-ttu-id="80daf-249">Merhaba Sihirbazı Hello yedekleme işlemi tamamlanmadan önce kapatırsanız, Başlangıç Sihirbazı'nı toorun hello arka planda devam eder.</span><span class="sxs-lookup"><span data-stu-id="80daf-249">If you close hello wizard before hello backup process finishes, hello wizard continues toorun in hello background.</span></span>

5. <span data-ttu-id="80daf-250">Dosya ve klasörleri sunucunuzda, ayrıca toohello Windows Server sistem durumu yedekleme yapıyorsanız, hello Şimdi Yedekle Sihirbazı yalnızca dosyaların yedeğini alın.</span><span class="sxs-lookup"><span data-stu-id="80daf-250">If you back up Files and Folders on your server, in addition toohello Windows Server System State, hello Backup Now wizard will only back up files.</span></span> <span data-ttu-id="80daf-251">tooperform geçici bir sistem durumu yedekleme, hello aşağıdaki PowerShell komutunu kullanın:</span><span class="sxs-lookup"><span data-stu-id="80daf-251">tooperform an ad hoc System State back up, use hello following PowerShell command:</span></span>

    ```
    PS C:\> Start-OBSystemStateBackup
    ```

  <span data-ttu-id="80daf-252">Merhaba ilk Yedekleme tamamlandıktan sonra hello **işi tamamlandı** durum hello yedekleme konsolunda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="80daf-252">After hello initial backup is completed, hello **Job completed** status appears in hello Backup console.</span></span>

  ![IR tamamlandı](./media/backup-try-azure-backup-in-10-mins/ircomplete.png)

## <a name="frequently-asked-questions"></a><span data-ttu-id="80daf-254">Sık sorulan sorular</span><span class="sxs-lookup"><span data-stu-id="80daf-254">Frequently asked questions</span></span>

<span data-ttu-id="80daf-255">Merhaba aşağıdaki sorular ve yanıtlar tamamlayıcı bilgiler sağlar.</span><span class="sxs-lookup"><span data-stu-id="80daf-255">hello following questions and answers provide supplementary information.</span></span>

### <a name="what-is-hello-staging-volume"></a><span data-ttu-id="80daf-256">Merhaba hazırlama toplu nedir?</span><span class="sxs-lookup"><span data-stu-id="80daf-256">What is hello Staging Volume?</span></span>

<span data-ttu-id="80daf-257">Merhaba hazırlama toplu burada hello yerel olarak kullanılabilir, Windows Server Yedekleme hello sistem durumu yedeklemesi aşamaları hello Ara konumunu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="80daf-257">hello Staging Volume represents hello intermediate location where hello natively available, Windows Server Backup stages hello System State Backup.</span></span> <span data-ttu-id="80daf-258">Azure Backup Aracısı sonra sıkıştırır ve bu Ara yedekleme şifreler ve güvenli HTTPS protokolünü toohello ile kurtarma Hizmetleri kasası yapılandırılmış gönderir.</span><span class="sxs-lookup"><span data-stu-id="80daf-258">Azure Backup agent then compresses and encrypts this intermediate backup and sends it via secure HTTPS Protocol toohello configured Recovery Services Vault.</span></span> <span data-ttu-id="80daf-259">**Bir Windows işletim biriminde hello hazırlama toplu oluşturmak önerilir. Sistem durumu yedeklemeleri sorunları gözlemlerseniz, hazırlama biriminiz hello konumunu denetimi hello ilk sorun giderme adımdır.**</span><span class="sxs-lookup"><span data-stu-id="80daf-259">**We strongly recommended you establish hello Staging Volume in a non-Windows-OS volume. If you observe problems with System State Backups, checking hello location of your Staging Volume is hello first troubleshooting step.**</span></span> 

### <a name="how-can-i-change-hello-staging-volume-path-specified-in-hello-azure-backup-agent"></a><span data-ttu-id="80daf-260">Merhaba hazırlama birimi hello Azure Backup aracısını belirtilen yolu nasıl değiştirebilir miyim?</span><span class="sxs-lookup"><span data-stu-id="80daf-260">How can I change hello Staging Volume Path specified in hello Azure Backup agent?</span></span>

<span data-ttu-id="80daf-261">Merhaba hazırlama toplu hello önbellek klasöründe varsayılan olarak bulunur.</span><span class="sxs-lookup"><span data-stu-id="80daf-261">hello Staging Volume is located in hello cache folder by default.</span></span> 

1. <span data-ttu-id="80daf-262">toochange bu konum, aşağıdaki komutta (yükseltilmiş bir komut istemi) kullanım hello:</span><span class="sxs-lookup"><span data-stu-id="80daf-262">toochange this location, use hello following command (in an elevated command prompt):</span></span>
  ```
  PS C:\> Net stop obengine
  ```

2. <span data-ttu-id="80daf-263">Ardından klasörle hello yolu toohello yeni hazırlama toplu kayıt defteri girdileri aşağıdaki hello güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="80daf-263">Then update hello following registry entries with hello path toohello new Staging Volume folder.</span></span>

  |<span data-ttu-id="80daf-264">Kayıt defteri yolu</span><span class="sxs-lookup"><span data-stu-id="80daf-264">Registry path</span></span>|<span data-ttu-id="80daf-265">Kayıt defteri anahtarı</span><span class="sxs-lookup"><span data-stu-id="80daf-265">Registry key</span></span>|<span data-ttu-id="80daf-266">Değer</span><span class="sxs-lookup"><span data-stu-id="80daf-266">Value</span></span>|
  |-------------|------------|-----|
  |<span data-ttu-id="80daf-267">HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span><span class="sxs-lookup"><span data-stu-id="80daf-267">HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span></span> | <span data-ttu-id="80daf-268">SSBStagingPath</span><span class="sxs-lookup"><span data-stu-id="80daf-268">SSBStagingPath</span></span> | <span data-ttu-id="80daf-269">Yeni hazırlama toplu konumu</span><span class="sxs-lookup"><span data-stu-id="80daf-269">new staging volume location</span></span> |

<span data-ttu-id="80daf-270">Merhaba hazırlama yolu büyük küçük harfe duyarlıdır ve ne hello sunucusunda mevcut olarak hello tam aynı büyük/küçük harf olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="80daf-270">hello Staging Path is case sensitive and must be hello exact same casing as what exists on hello server.</span></span> 

3. <span data-ttu-id="80daf-271">Merhaba hazırlama birimi yolu değiştirdiğinizde, hello Backup altyapısını yeniden başlatın:</span><span class="sxs-lookup"><span data-stu-id="80daf-271">Once you change hello Staging volume path, restart hello Backup engine:</span></span>
  ```
  PS C:\> Net start obengine
  ```
4. <span data-ttu-id="80daf-272">Değiştirilen hello yolu, açık hello Microsoft Azure kurtarma Hizmetleri aracısını ve tetikleyici geçici bir sistem durumu yedeğini toopick.</span><span class="sxs-lookup"><span data-stu-id="80daf-272">toopick up hello changed path, open hello Microsoft Azure Recovery Services agent and trigger an ad hoc backup of System State.</span></span>

### <a name="why-is-hello-system-state-default-retention-set-too60-days"></a><span data-ttu-id="80daf-273">Neden hello sistem durumu too60 gün varsayılan saklama ayarlanmış mı?</span><span class="sxs-lookup"><span data-stu-id="80daf-273">Why is hello System State default retention set too60 days?</span></span>

<span data-ttu-id="80daf-274">bir sistem durumu yedeklemesi kullanım ömrünü Hello olduğu hello hello Windows Server Active Directory rol hello "kullanım ömrü" ayarı ile aynı.</span><span class="sxs-lookup"><span data-stu-id="80daf-274">hello useful life of a system state backup is hello same as hello "tombstone lifetime" setting for hello Windows Server Active Directory role.</span></span> <span data-ttu-id="80daf-275">Merhaba hello silinmiş öğe işareti yaşam süresi girişi için varsayılan değer 60 gündür.</span><span class="sxs-lookup"><span data-stu-id="80daf-275">hello default value for hello tombstone lifetime entry is 60 days.</span></span> <span data-ttu-id="80daf-276">Bu değer hello dizin hizmeti (NTDS) yapılandırma nesnesi üzerinde ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="80daf-276">This value can be set on hello Directory Service (NTDS) config object.</span></span>

### <a name="how-do-i-change-hello-default-backup-and-retention-policy-for-system-state"></a><span data-ttu-id="80daf-277">Merhaba varsayılan yedekleme ve bekletme ilkesi için sistem durumu nasıl değiştiririm?</span><span class="sxs-lookup"><span data-stu-id="80daf-277">How do I change hello default Backup and Retention Policy for System State?</span></span>

<span data-ttu-id="80daf-278">toochange hello varsayılan yedekleme ve bekletme ilkesi sistem durumu için:</span><span class="sxs-lookup"><span data-stu-id="80daf-278">toochange hello default Backup and Retention Policy for System State:</span></span>
1. <span data-ttu-id="80daf-279">Merhaba Backup altyapısını durdurun.</span><span class="sxs-lookup"><span data-stu-id="80daf-279">Stop hello Backup engine.</span></span> <span data-ttu-id="80daf-280">Komutu yükseltilmiş komut isteminden aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="80daf-280">Run hello following command from an elevated command prompt.</span></span>

  ```
  PS C:\> Net stop obengine
  ```

2. <span data-ttu-id="80daf-281">Ekleme veya kayıt defteri anahtarı girişleri HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider aşağıdaki hello güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="80daf-281">Add or update hello following registry key entries in HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider.</span></span>

  |<span data-ttu-id="80daf-282">Kayıt defteri adı</span><span class="sxs-lookup"><span data-stu-id="80daf-282">Registry Name</span></span>|<span data-ttu-id="80daf-283">Açıklama</span><span class="sxs-lookup"><span data-stu-id="80daf-283">Description</span></span>|<span data-ttu-id="80daf-284">Değer</span><span class="sxs-lookup"><span data-stu-id="80daf-284">Value</span></span>|
  |-------------|-----------|-----|
  |<span data-ttu-id="80daf-285">SSBScheduleTime</span><span class="sxs-lookup"><span data-stu-id="80daf-285">SSBScheduleTime</span></span>|<span data-ttu-id="80daf-286">Merhaba yedekleme tooconfigure hello saati kullanılır.</span><span class="sxs-lookup"><span data-stu-id="80daf-286">Used tooconfigure hello time of hello backup.</span></span> <span data-ttu-id="80daf-287">9 yerel saati varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="80daf-287">Default is 9PM local time.</span></span>|<span data-ttu-id="80daf-288">DWord: Biçimi 9:30 yerel saati 2130 örneğin SSDD (ondalık)</span><span class="sxs-lookup"><span data-stu-id="80daf-288">DWord: Format HHMM (Decimal) for example 2130 for 9:30PM local time</span></span>|
  |<span data-ttu-id="80daf-289">SSBScheduleDays</span><span class="sxs-lookup"><span data-stu-id="80daf-289">SSBScheduleDays</span></span>|<span data-ttu-id="80daf-290">Sistem durumu yedeklemesi sırasında hello zaman gerçekleştirilmelidir kullanılan tooconfigure hello günleri saat belirtildi.</span><span class="sxs-lookup"><span data-stu-id="80daf-290">Used tooconfigure hello days when System State Backup must be performed at hello specified time.</span></span> <span data-ttu-id="80daf-291">Tek tek basamak hello haftanın günleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="80daf-291">Individual digits specify days of hello week.</span></span> <span data-ttu-id="80daf-292">0 Pazar gösteren, 1. Pazartesi, vb..</span><span class="sxs-lookup"><span data-stu-id="80daf-292">0 represents Sunday, 1 is Monday, and so on.</span></span> <span data-ttu-id="80daf-293">Varsayılan yedekleme için Pazar günüdür.</span><span class="sxs-lookup"><span data-stu-id="80daf-293">Default day for backup is Sunday.</span></span>|<span data-ttu-id="80daf-294">DWord: gün hello hafta toorun yedekleme (örneğin 1230 Pazartesi, Salı, Çarşamba ve Pazar yedeklemeler zamanlar ondalık).</span><span class="sxs-lookup"><span data-stu-id="80daf-294">DWord: days of hello week toorun backup (decimal) for example 1230 schedules backups on Monday, Tuesday, Wednesday, and Sunday.</span></span>|
  |<span data-ttu-id="80daf-295">SSBRetentionDays</span><span class="sxs-lookup"><span data-stu-id="80daf-295">SSBRetentionDays</span></span>|<span data-ttu-id="80daf-296">Kullanılan tooconfigure hello gün tooretain yedekleme.</span><span class="sxs-lookup"><span data-stu-id="80daf-296">Used tooconfigure hello days tooretain backup.</span></span> <span data-ttu-id="80daf-297">Varsayılan değer 60'tır.</span><span class="sxs-lookup"><span data-stu-id="80daf-297">Default value is 60.</span></span> <span data-ttu-id="80daf-298">Değer izin verilen en fazla 180'dir.</span><span class="sxs-lookup"><span data-stu-id="80daf-298">Maximum allowed value is 180.</span></span>|<span data-ttu-id="80daf-299">DWord: Gün tooretain yedekleme (ondalık).</span><span class="sxs-lookup"><span data-stu-id="80daf-299">DWord: Days tooretain backup (decimal).</span></span>|

3. <span data-ttu-id="80daf-300">Komut toorestart hello yedekleme altyapısı aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="80daf-300">Use hello following command toorestart hello backup engine.</span></span>
    ```
    PS C:\> Net start obengine
    ```

4. <span data-ttu-id="80daf-301">Merhaba Microsoft Kurtarma Hizmetleri Aracısı'nı açın.</span><span class="sxs-lookup"><span data-stu-id="80daf-301">Open hello Microsoft Recovery Services agent.</span></span>

5. <span data-ttu-id="80daf-302">Tıklatın **yedekleme zamanlaması** ve ardından **sonraki** yansıtılan hello değişiklikleri görene kadar.</span><span class="sxs-lookup"><span data-stu-id="80daf-302">Click **Schedule Backup** and then click **Next** until you see hello changes reflected.</span></span>

6. <span data-ttu-id="80daf-303">Tıklatın **son** tooapply hello değişiklikleri.</span><span class="sxs-lookup"><span data-stu-id="80daf-303">Click **Finish** tooapply hello changes.</span></span>


## <a name="questions"></a><span data-ttu-id="80daf-304">Sorularınız mı var?</span><span class="sxs-lookup"><span data-stu-id="80daf-304">Questions?</span></span>
<span data-ttu-id="80daf-305">Sorularınız varsa veya herhangi bir özellik varsa dahil, toosee istediğiniz [Geri bildirimlerinizi bize gönderin](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="80daf-305">If you have questions, or if there is any feature that you would like toosee included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="80daf-306">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="80daf-306">Next steps</span></span>
* <span data-ttu-id="80daf-307">[Windows makinelerini yedekleme](backup-configure-vault.md) konusunda daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="80daf-307">Get more details about [backing up Windows machines](backup-configure-vault.md).</span></span>
* <span data-ttu-id="80daf-308">Dosya ve klasörlerinizi yedeklediğinize göre artık [kasa ve sunucularınızı yönetebilirsiniz](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="80daf-308">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="80daf-309">Toorestore yedekleme ihtiyacınız varsa, bu makalede çok kullanmak[dosyaları tooa Windows makinesine geri](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="80daf-309">If you need toorestore a backup, use this article too[restore files tooa Windows machine](backup-azure-restore-windows-server.md).</span></span>
