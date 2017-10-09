---
title: "Windows dosya ve klasörleri tooAzure (Resource Manager) ayarlama aaaBack | Microsoft Docs"
description: "Windows dosya ve klasörleri tooAzure bir Resource Manager dağıtımında yukarı tooback öğrenin."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "nasıl toobackup; nasıl tooback; Yedekleme dosyaları ve klasörleri"
ms.assetid: 5b15ebf1-2214-4722-b937-96e2be8872bb
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 8/15/2017
ms.author: markgal;
ms.openlocfilehash: 07d6580a84d5092ed2c61bf86ff5fcb148423ef2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="first-look-back-up-files-and-folders-in-resource-manager-deployment"></a><span data-ttu-id="6c3f7-104">İlk bakış: Resource Manager dağıtımında dosya ve klasörleri yedekleme</span><span class="sxs-lookup"><span data-stu-id="6c3f7-104">First look: back up files and folders in Resource Manager deployment</span></span>
<span data-ttu-id="6c3f7-105">Bu makalede açıklanır nasıl bir Resource Manager dağıtım kullanarak tooback, Windows Server (veya Windows bilgisayarı) dosyaları ve klasörleri tooAzure.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-105">This article explains how tooback up your Windows Server (or Windows computer) files and folders tooAzure using a Resource Manager deployment.</span></span> <span data-ttu-id="6c3f7-106">Eğitmen hedeflenen toowalk olan hello temel bilgileri size.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-106">It's a tutorial intended toowalk you through hello basics.</span></span> <span data-ttu-id="6c3f7-107">Azure Backup ile tooget çalışmaya istiyorsanız hello doğru yerde demektir.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-107">If you want tooget started using Azure Backup, you're in hello right place.</span></span>

<span data-ttu-id="6c3f7-108">Tooknow Azure yedekleme hakkında daha fazla bilgi istiyorsanız, bu okuma [genel bakış](backup-introduction-to-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="6c3f7-108">If you want tooknow more about Azure Backup, read this [overview](backup-introduction-to-azure-backup.md).</span></span>

<span data-ttu-id="6c3f7-109">Azure aboneliğiniz yoksa istediğiniz Azure hizmetine erişmenizi sağlayan [ücretsiz bir hesap](https://azure.microsoft.com/free/) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) that lets you access any Azure service.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="6c3f7-110">Kurtarma hizmetleri kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="6c3f7-110">Create a recovery services vault</span></span>
<span data-ttu-id="6c3f7-111">tooback dosya ve klasörleri toocreate toostore hello verilerin istediğiniz hello bölgede bir kurtarma Hizmetleri kasası gerekir.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-111">tooback up your files and folders, you need toocreate a Recovery Services vault in hello region where you want toostore hello data.</span></span> <span data-ttu-id="6c3f7-112">Çoğaltılan depolama alanınızın nasıl istediğiniz toodetermine de gerekir.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-112">You also need toodetermine how you want your storage replicated.</span></span>

### <a name="toocreate-a-recovery-services-vault"></a><span data-ttu-id="6c3f7-113">toocreate bir kurtarma Hizmetleri kasası</span><span class="sxs-lookup"><span data-stu-id="6c3f7-113">toocreate a Recovery Services vault</span></span>
1. <span data-ttu-id="6c3f7-114">Zaten yapmadıysanız, toohello içinde oturum [Azure Portal](https://portal.azure.com/) Azure aboneliğinizi kullanarak.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-114">If you haven't already done so, sign in toohello [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="6c3f7-115">Merhaba Hub menüsünde **daha fazla hizmet** ve kaynakları hello listesinde yazın **kurtarma Hizmetleri** tıklatıp **kurtarma Hizmetleri kasaları**.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-115">On hello Hub menu, click **More services** and in hello list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![Kurtarma Hizmetleri Kasası oluşturma 1. adım](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="6c3f7-117">Merhaba abonelikte kurtarma Hizmetleri kasaları varsa hello kasalarını listelenir.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-117">If there are recovery services vaults in hello subscription, hello vaults are listed.</span></span>
3. <span data-ttu-id="6c3f7-118">Merhaba üzerinde **kurtarma Hizmetleri kasaları** menüsünde tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-118">On hello **Recovery Services vaults** menu, click **Add**.</span></span>

    ![Kurtarma Hizmetleri Kasası oluşturma 2. adım](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="6c3f7-120">Merhaba kurtarma Hizmetleri kasası dikey penceresi açılır tooprovide isteyen bir **adı**, **abonelik**, **kaynak grubu**, ve **konumu**.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-120">hello Recovery Services vault blade opens, prompting you tooprovide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Kurtarma Hizmetleri Kasası Oluşturma 3. adım](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="6c3f7-122">İçin **adı**, bir kolay ad tooidentify hello kasası girin.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-122">For **Name**, enter a friendly name tooidentify hello vault.</span></span> <span data-ttu-id="6c3f7-123">Merhaba adı toobe hello Azure aboneliği için benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-123">hello name needs toobe unique for hello Azure subscription.</span></span> <span data-ttu-id="6c3f7-124">2 ila 50 karakterden oluşan bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-124">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="6c3f7-125">Ad bir harf ile başlamalıdır ve yalnızca harf, rakam ve kısa çizgi içerebilir.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-125">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="6c3f7-126">Merhaba, **abonelik** bölümünde, hello açılır menü toochoose hello Azure aboneliği kullanın.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-126">In hello **Subscription** section, use hello drop-down menu toochoose hello Azure subscription.</span></span> <span data-ttu-id="6c3f7-127">Yalnızca bir abonelik kullanırsanız, bu abonelik görünür ve toohello sonraki adımı atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-127">If you use only one subscription, that subscription appears and you can skip toohello next step.</span></span> <span data-ttu-id="6c3f7-128">Hangi abonelik toouse emin değilseniz, hello varsayılan kullanın (veya önerilen) aboneliği.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-128">If you are not sure which subscription toouse, use hello default (or suggested) subscription.</span></span> <span data-ttu-id="6c3f7-129">Yalnızca kuruluş hesabınızın birden çok Azure aboneliği ile ilişkili olması durumunda birden çok seçenek olur.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-129">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="6c3f7-130">Merhaba, **kaynak grubu** bölümü:</span><span class="sxs-lookup"><span data-stu-id="6c3f7-130">In hello **Resource group** section:</span></span>

    * <span data-ttu-id="6c3f7-131">seçin **Yeni Oluştur** toocreate yeni bir kaynak grubu istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-131">select **Create new** if you want toocreate a new Resource group.</span></span>
    <span data-ttu-id="6c3f7-132">Veya</span><span class="sxs-lookup"><span data-stu-id="6c3f7-132">Or</span></span>
    * <span data-ttu-id="6c3f7-133">seçin **var olanı kullan** ve hello açılır menü toosee hello kullanılabilir kaynak gruplarının listesini'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-133">select **Use existing** and click hello drop-down menu toosee hello available list of Resource groups.</span></span>

  <span data-ttu-id="6c3f7-134">Kaynak grupları hakkında tam bilgi için bkz: Merhaba [Azure Resource Manager'a genel bakış](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6c3f7-134">For complete information on Resource groups, see hello [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="6c3f7-135">Tıklatın **konumu** tooselect hello hello kasa için coğrafi bölgeyi.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-135">Click **Location** tooselect hello geographic region for hello vault.</span></span> <span data-ttu-id="6c3f7-136">Bu seçim, yedekleme verilerinizi burada gönderilen hello coğrafi bölgeyi belirler.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-136">This choice determines hello geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="6c3f7-137">Merhaba kurtarma Hizmetleri kasası dikey penceresinde Hello altındaki tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-137">At hello bottom of hello Recovery Services vault blade, click **Create**.</span></span>

    <span data-ttu-id="6c3f7-138">Oluşturulan toobe kurtarma Hizmetleri kasası hello için birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-138">It can take several minutes for hello Recovery Services vault toobe created.</span></span> <span data-ttu-id="6c3f7-139">Merhaba portal hello üst sağ bölmesinde Hello durum bildirimlerini izleyin.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-139">Monitor hello status notifications in hello upper right-hand area of hello portal.</span></span> <span data-ttu-id="6c3f7-140">Kasanız oluşturulduktan sonra hello kurtarma Hizmetleri kasaları listesinde görünür.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-140">Once your vault is created, it appears in hello list of Recovery Services vaults.</span></span> <span data-ttu-id="6c3f7-141">Birkaç dakika sonra kasayı görmezseniz **Yenile**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-141">If after several minutes you don't see your vault, click **Refresh**.</span></span>

    ![Yenile düğmesine tıklayın](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    <span data-ttu-id="6c3f7-143">Kasanızı kurtarma Hizmetleri kasalarının hello listesinde gördüğünüz verdikten sonra hazır tooset hello depolama artıklığı demektir.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-143">Once you see your vault in hello list of Recovery Services vaults, you are ready tooset hello storage redundancy.</span></span>

### <a name="set-storage-redundancy-for-hello-vault"></a><span data-ttu-id="6c3f7-144">Depolama artıklığı hello kasası için ayarlama</span><span class="sxs-lookup"><span data-stu-id="6c3f7-144">Set storage redundancy for hello vault</span></span>
<span data-ttu-id="6c3f7-145">Kurtarma Hizmetleri kasası oluşturduğunuzda, depolama artıklığı istediğiniz yapılandırılmış hello biçimde olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-145">When you create a Recovery Services vault, make sure storage redundancy is configured hello way you want.</span></span>

1. <span data-ttu-id="6c3f7-146">Merhaba gelen **kurtarma Hizmetleri kasaları** dikey penceresinde hello yeni kasaya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-146">From hello **Recovery Services vaults** blade, click hello new vault.</span></span>

    ![Kurtarma Hizmetleri kasası hello listeden Hello yeni kasa seçin](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="6c3f7-148">Merhaba kasası seçtiğinizde hello **kurtarma Hizmetleri kasası** dikey daraltır ve hello ayarları dikey (*hello üstünde hello kasasının hello ada sahip*) ve hello kasa Ayrıntılar dikey penceresini açın.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-148">When you select hello vault, hello **Recovery Services vault** blade narrows, and hello Settings blade (*which has hello name of hello vault at hello top*) and hello vault details blade open.</span></span>

    ![Yeni kasa için Görünüm hello depolama yapılandırması](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)
2. <span data-ttu-id="6c3f7-150">Merhaba yeni kasasının ayarlar dikey penceresinde hello dikey slayt tooscroll toohello Yönet bölümüne aşağı kullanın ve'ı tıklatın **Yedekleme Altyapısı**.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-150">In hello new vault's Settings blade, use hello vertical slide tooscroll down toohello Manage section, and click **Backup Infrastructure**.</span></span>
    <span data-ttu-id="6c3f7-151">Merhaba yedekleme altyapısı dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-151">hello Backup Infrastructure blade opens.</span></span>
3. <span data-ttu-id="6c3f7-152">Merhaba yedekleme altyapısı dikey penceresinde tıklayın **yedekleme yapılandırması** tooopen hello **yedekleme yapılandırması** dikey.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-152">In hello Backup Infrastructure blade, click **Backup Configuration** tooopen hello **Backup Configuration** blade.</span></span>

    ![Yeni kasa Hello depolama yapılandırmasını ayarlayın](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. <span data-ttu-id="6c3f7-154">Kasanız için Hello uygun depolama çoğaltma seçeneğini seçin.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-154">Choose hello appropriate storage replication option for your vault.</span></span>

    ![depolama yapılandırması seçenekleri](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    <span data-ttu-id="6c3f7-156">Varsayılan olarak, kasanız coğrafi olarak yedekli depolamaya sahiptir.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-156">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="6c3f7-157">Azure birincil yedekleme alanı uç noktası kullanıyorsanız, toouse devam **coğrafi olarak yedekli**.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-157">If you use Azure as a primary backup storage endpoint, continue toouse **Geo-redundant**.</span></span> <span data-ttu-id="6c3f7-158">Birincil yedekleme alanı uç noktası Azure kullanmıyorsanız, ardından **yerel olarak yedekli**, hello Azure depolama maliyetlerini azaltır.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-158">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces hello Azure storage costs.</span></span> <span data-ttu-id="6c3f7-159">[Coğrafi olarak yedekli](../storage/common/storage-redundancy.md#geo-redundant-storage) ve [yerel olarak yedekli](../storage/common/storage-redundancy.md#locally-redundant-storage) depolama seçenekleri hakkında daha fazla bilgiyi [Depolama yedekliliğine genel bakış](../storage/common/storage-redundancy.md) bölümünden edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-159">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="6c3f7-160">Bir kasa oluşturduğunuza göre dosya ve klasörleri yedeklemek için yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-160">Now that you've created a vault, configure it for backing up files and folders.</span></span>

## <a name="configure-hello-vault"></a><span data-ttu-id="6c3f7-161">Merhaba kasası yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6c3f7-161">Configure hello vault</span></span>
1. <span data-ttu-id="6c3f7-162">Açık kurtarma Hizmetleri kasası dikey (Merhaba kasa), yeni oluşturduğunuz, hello Başlarken bölümünde Merhaba, tıklatın **yedekleme**, sonra da hello **yedekleme ile çalışmaya başlama** dikey penceresinde, select  **Yedekleme hedefi**.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-162">On hello Recovery Services vault blade (for hello vault you just created), in hello Getting Started section, click **Backup**, then on hello **Getting Started with Backup** blade, select **Backup goal**.</span></span>

    ![Yedekleme hedefi dikey penceresini açma](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

    <span data-ttu-id="6c3f7-164">Merhaba **yedekleme hedefi** dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-164">hello **Backup Goal** blade opens.</span></span>

    ![Yedekleme hedefi dikey penceresini açma](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="6c3f7-166">Merhaba gelen **, iş yükünü çalıştırdığı?** açılır menüsünde, select **şirket içi**.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-166">From hello **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

    <span data-ttu-id="6c3f7-167">Windows Server veya Windows bilgisayarınız Azure üzerinde olmayan fiziksel bir makine olduğu için **Şirket içi** seçeneğini belirlersiniz.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-167">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="6c3f7-168">Merhaba gelen **neler toobackup istediğiniz?** menüsünde, select **dosya ve klasörleri**, tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-168">From hello **What do you want toobackup?** menu, select **Files and folders**, and click **OK**.</span></span>

    ![Dosya ve klasörleri yedekleme](./media/backup-try-azure-backup-in-10-mins/set-file-folder.png)

    <span data-ttu-id="6c3f7-170">Tamam'ı tıklattıktan sonra bir onay işareti çok sonraki görünür**yedekleme hedefi**ve hello **altyapıyı hazırlama** dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-170">After clicking OK, a checkmark appears next too**Backup goal**, and hello **Prepare infrastructure** blade opens.</span></span>

    ![Yedekleme hedefi yapılandırılmıştır, bundan sonra altyapıyı hazırlayın](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="6c3f7-172">Merhaba üzerinde **altyapıyı hazırlama** dikey penceresinde tıklatın **karşıdan aracısı için Windows Server veya Windows İstemcisi**.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-172">On hello **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

    ![altyapıyı hazırlama](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

    <span data-ttu-id="6c3f7-174">Windows Server temel kullanıyorsanız, Windows Server temel için toodownload hello Aracısı seçin.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-174">If you are using Windows Server Essential, then choose toodownload hello agent for Windows Server Essential.</span></span> <span data-ttu-id="6c3f7-175">Açılır menü toorun komut istemleri veya MARSAgentInstaller.exe kaydedin.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-175">A pop-up menu prompts you toorun or save MARSAgentInstaller.exe.</span></span>

    ![MARSAgentInstaller iletişim kutusu](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="6c3f7-177">Merhaba indirme açılır menüsünde tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-177">In hello download pop-up menu, click **Save**.</span></span>

    <span data-ttu-id="6c3f7-178">Varsayılan olarak, hello **MARSagentinstaller.exe** dosya tooyour indirmeler klasörüne kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-178">By default, hello **MARSagentinstaller.exe** file is saved tooyour Downloads folder.</span></span> <span data-ttu-id="6c3f7-179">Merhaba yükleyici tamamladığında, toorun hello yükleyici istediğiniz veya hello klasörünü açın, isteyen bir açılır pencere görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-179">When hello installer completes, you will see a pop-up asking if you want toorun hello installer, or open hello folder.</span></span>

    ![altyapıyı hazırlama](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

    <span data-ttu-id="6c3f7-181">Tooinstall hello Aracısı henüz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-181">You don't need tooinstall hello agent yet.</span></span> <span data-ttu-id="6c3f7-182">Merhaba kasa kimlik bilgileri indirdikten sonra hello aracısını yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-182">You can install hello agent after you have downloaded hello vault credentials.</span></span>

6. <span data-ttu-id="6c3f7-183">Merhaba üzerinde **altyapıyı hazırlama** dikey penceresinde tıklatın **karşıdan**.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-183">On hello **Prepare infrastructure** blade, click **Download**.</span></span>

    ![kasa kimlik bilgilerini indirme](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

    <span data-ttu-id="6c3f7-185">Merhaba kasa kimlik bilgileri tooyour indirmeler klasörüne indirin.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-185">hello vault credentials download tooyour Downloads folder.</span></span> <span data-ttu-id="6c3f7-186">Hello kasa kimlik bilgilerini indirme işlemini tamamladıktan sonra tooopen istediğiniz veya hello kimlik bilgilerini Kaydet isteyen bir açılır pencere görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-186">After hello vault credentials finish downloading, you see a pop-up asking if you want tooopen or save hello credentials.</span></span> <span data-ttu-id="6c3f7-187">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-187">Click **Save**.</span></span> <span data-ttu-id="6c3f7-188">Yanlışlıkla tıklatırsanız **açık**, tooopen hello kasa kimlik bilgileri çalışır hello iletişim sağlar, başarısız.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-188">If you accidentally click **Open**, let hello dialog that attempts tooopen hello vault credentials, fail.</span></span> <span data-ttu-id="6c3f7-189">Merhaba kasa kimlik bilgileri açamıyor.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-189">You cannot open hello vault credentials.</span></span> <span data-ttu-id="6c3f7-190">Toohello sonraki adıma geçin.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-190">Proceed toohello next step.</span></span> <span data-ttu-id="6c3f7-191">Merhaba kasa kimlik bilgileri hello indirme klasöründe yer alır.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-191">hello vault credentials are in hello Downloads folder.</span></span>   

    ![kasa kimlik bilgilerini indirme tamamlandı](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-hello-agent"></a><span data-ttu-id="6c3f7-193">Yükleme ve hello Aracısı kaydedin</span><span class="sxs-lookup"><span data-stu-id="6c3f7-193">Install and register hello agent</span></span>

> [!NOTE]
> <span data-ttu-id="6c3f7-194">Hello Azure portal üzerinden yedeklemeyi etkinleştirme olanağı henüz kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-194">Enabling backup through hello Azure portal is not available, yet.</span></span> <span data-ttu-id="6c3f7-195">Dosya ve klasörleri Hello Microsoft Azure kurtarma Hizmetleri Aracısı tooback kullanın.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-195">Use hello Microsoft Azure Recovery Services Agent tooback up your files and folders.</span></span>
>

1. <span data-ttu-id="6c3f7-196">Bulun ve çift hello **MARSagentinstaller.exe** hello yükleme klasöründen (veya diğer kayıtlı konumdan).</span><span class="sxs-lookup"><span data-stu-id="6c3f7-196">Locate and double-click hello **MARSagentinstaller.exe** from hello Downloads folder (or other saved location).</span></span>

    <span data-ttu-id="6c3f7-197">Merhaba yükleyici, bir dizi ileti ayıklar gibi yükler ve hello kurtarma Hizmetleri aracısını kaydeder sağlar.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-197">hello installer provides a series of messages as it extracts, installs, and registers hello Recovery Services agent.</span></span>

    ![Kurtarma Hizmetleri aracısı yükleyici kimlik bilgilerini çalıştırma](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="6c3f7-199">Merhaba Microsoft Azure kurtarma Hizmetleri Aracısı Kurulum Sihirbazı tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-199">Complete hello Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="6c3f7-200">toocomplete Başlangıç Sihirbazı, şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="6c3f7-200">toocomplete hello wizard, you need to:</span></span>

   * <span data-ttu-id="6c3f7-201">Merhaba yükleme ve önbellek klasörü için bir konum seçin.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-201">Choose a location for hello installation and cache folder.</span></span>
   * <span data-ttu-id="6c3f7-202">Bir proxy sunucu tooconnect toohello kullanırsanız, Ara sunucu bilgilerinizi sağlayın Internet.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-202">Provide your proxy server info if you use a proxy server tooconnect toohello internet.</span></span>
   * <span data-ttu-id="6c3f7-203">Kimliği doğrulanmış bir ara sunucu kullanıyorsanız kullanıcı adı ve parola bilgilerinizi sağlayın.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-203">Provide your user name and password details if you use an authenticated proxy.</span></span>
   * <span data-ttu-id="6c3f7-204">Merhaba indirilen kasa kimlik bilgilerini sağlayın</span><span class="sxs-lookup"><span data-stu-id="6c3f7-204">Provide hello downloaded vault credentials</span></span>
   * <span data-ttu-id="6c3f7-205">Merhaba şifreleme parolası güvenli bir konuma kaydedin.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-205">Save hello encryption passphrase in a secure location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="6c3f7-206">Kaybeder veya hello parolayı unutursanız Microsoft hello yedekleme verilerini kurtarmanıza yardımcı olamaz.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-206">If you lose or forget hello passphrase, Microsoft cannot help recover hello backup data.</span></span> <span data-ttu-id="6c3f7-207">Merhaba dosyayı güvenli bir konuma kaydedin.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-207">Save hello file in a secure location.</span></span> <span data-ttu-id="6c3f7-208">Gerekli toorestore bir yedekleme olur.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-208">It is required toorestore a backup.</span></span>
     >
     >

<span data-ttu-id="6c3f7-209">Merhaba aracı artık yüklenmiş ve kayıtlı toohello kasasına makineniz olduğu.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-209">hello agent is now installed and your machine is registered toohello vault.</span></span> <span data-ttu-id="6c3f7-210">Hazır tooconfigure olduğunuz ve yedekleme zamanlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-210">You're ready tooconfigure and schedule your backup.</span></span>

## <a name="network-and-connectivity-requirements"></a><span data-ttu-id="6c3f7-211">Ağ ve Bağlantı Gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="6c3f7-211">Network and Connectivity Requirements</span></span>

<span data-ttu-id="6c3f7-212">Makine/proxy Internet erişimi sınırlı hello mcahine/proxy üzerinde güvenlik duvarı ayarlarını aşağıdaki URL'lere yapılandırılmış tooallow hello olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="6c3f7-212">If your machine/proxy has limited internet access, ensure that firewall settings on hello mcahine/proxy are configured tooallow hello following URLs:</span></span> <br>
    1. <span data-ttu-id="6c3f7-213">www.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="6c3f7-213">www.msftncsi.com</span></span>
    2. <span data-ttu-id="6c3f7-214">*.Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="6c3f7-214">*.Microsoft.com</span></span>
    3. <span data-ttu-id="6c3f7-215">*.WindowsAzure.com</span><span class="sxs-lookup"><span data-stu-id="6c3f7-215">*.WindowsAzure.com</span></span>
    4. <span data-ttu-id="6c3f7-216">*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="6c3f7-216">*.microsoftonline.com</span></span>
    5. <span data-ttu-id="6c3f7-217">*.windows.ne</span><span class="sxs-lookup"><span data-stu-id="6c3f7-217">*.windows.ne</span></span>

## <a name="back-up-your-files-and-folders"></a><span data-ttu-id="6c3f7-218">Dosya ve klasörlerinizi yedekleme</span><span class="sxs-lookup"><span data-stu-id="6c3f7-218">Back up your files and folders</span></span>
<span data-ttu-id="6c3f7-219">Merhaba ilk yedekleme iki anahtar görev içerir:</span><span class="sxs-lookup"><span data-stu-id="6c3f7-219">hello initial backup includes two key tasks:</span></span>

* <span data-ttu-id="6c3f7-220">Merhaba yedekleme zamanlaması</span><span class="sxs-lookup"><span data-stu-id="6c3f7-220">Schedule hello backup</span></span>
* <span data-ttu-id="6c3f7-221">Dosya ve klasörleri hello için ilk kez yedekleme</span><span class="sxs-lookup"><span data-stu-id="6c3f7-221">Back up files and folders for hello first time</span></span>

<span data-ttu-id="6c3f7-222">toocomplete hello ilk yedekleme, kullanım hello Microsoft Azure kurtarma Hizmetleri Aracısı.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-222">toocomplete hello initial backup, use hello Microsoft Azure Recovery Services agent.</span></span>

### <a name="tooschedule-hello-backup-job"></a><span data-ttu-id="6c3f7-223">tooschedule hello yedekleme işi</span><span class="sxs-lookup"><span data-stu-id="6c3f7-223">tooschedule hello backup job</span></span>
1. <span data-ttu-id="6c3f7-224">Merhaba Microsoft Azure kurtarma Hizmetleri Aracısı'nı açın.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-224">Open hello Microsoft Azure Recovery Services agent.</span></span> <span data-ttu-id="6c3f7-225">Bunu, makinenizde **Microsoft Azure Backup** aramasını yaparak bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-225">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Hello Azure kurtarma Hizmetleri aracısını başlatma](./media/backup-try-azure-backup-in-10-mins/snap-in-search.png)
2. <span data-ttu-id="6c3f7-227">Merhaba kurtarma Hizmetleri aracısında tıklatın **yedekleme zamanlaması**.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-227">In hello Recovery Services agent, click **Schedule Backup**.</span></span>

    ![Windows Server yedeklemesini zamanlama](./media/backup-try-azure-backup-in-10-mins/schedule-first-backup.png)
3. <span data-ttu-id="6c3f7-229">Merhaba üzerinde hello yedeklemeyi Zamanlama Sihirbazı sayfasında Başlarken, tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-229">On hello Getting started page of hello Schedule Backup Wizard, click **Next**.</span></span>
4. <span data-ttu-id="6c3f7-230">Merhaba öğeleri seçin tooBackup sayfasında, tıklatın **öğeleri Ekle**.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-230">On hello Select Items tooBackup page, click **Add Items**.</span></span>
5. <span data-ttu-id="6c3f7-231">Hello dosya ve klasörlerin tooback yedeklemek istediğiniz ve ardından seçin **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-231">Select hello files and folders that you want tooback up, and then click **Okay**.</span></span>
6. <span data-ttu-id="6c3f7-232">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-232">Click **Next**.</span></span>
7. <span data-ttu-id="6c3f7-233">Merhaba üzerinde **yedekleme zamanlamasını belirtin** sayfasında, hello belirtin **yedekleme zamanlaması** tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-233">On hello **Specify Backup Schedule** page, specify hello **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="6c3f7-234">Günlük (en fazla günde üç kez olmak üzere) veya haftalık yedeklemeler zamanlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-234">You can schedule daily (at a maximum rate of three times per day) or weekly backups.</span></span>

    ![Windows Server Yedekleme öğeleri](./media/backup-try-azure-backup-in-10-mins/specify-backup-schedule-close.png)

   > [!NOTE]
   > <span data-ttu-id="6c3f7-236">Merhaba makale nasıl toospecify hello yedekleme zamanlaması hakkında daha fazla bilgi için bkz: [kullanım Azure yedekleme tooreplace bant altyapınızın](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="6c3f7-236">For more information about how toospecify hello backup schedule, see hello article [Use Azure Backup tooreplace your tape infrastructure](backup-azure-backup-cloud-as-tape.md).</span></span>
   >

8. <span data-ttu-id="6c3f7-237">Merhaba üzerinde **bekletme ilkesi seçin** sayfası, select hello **Bekletme İlkesi** hello yedek kopya.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-237">On hello **Select Retention Policy** page, select hello **Retention Policy** for hello backup copy.</span></span>

    <span data-ttu-id="6c3f7-238">Merhaba bekletme ilkesi hello yedekleme verileri ne kadar süreyle depolanacağını belirtir.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-238">hello retention policy specifies how long hello backup data is stored.</span></span> <span data-ttu-id="6c3f7-239">Tüm yedekleme noktaları için "sabit ilke" belirtmek yerine hello yedekleme gerçekleştiğinde göre farklı bekletme ilkeleri belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-239">Rather than specifying a “flat policy” for all backup points, you can specify different retention policies based on when hello backup occurs.</span></span> <span data-ttu-id="6c3f7-240">Merhaba günlük, haftalık, aylık ve yıllık bekletme ilkeleri toomeet gereksinimlerinizi değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-240">You can modify hello daily, weekly, monthly, and yearly retention policies toomeet your needs.</span></span>
9. <span data-ttu-id="6c3f7-241">Merhaba ilk yedekleme türünü seçin sayfasında hello ilk yedekleme türünü seçin.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-241">On hello Choose Initial Backup Type page, choose hello initial backup type.</span></span> <span data-ttu-id="6c3f7-242">Merhaba seçeneği bırakın **hello ağ üzerinden otomatik olarak** seçili ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-242">Leave hello option **Automatically over hello network** selected, and then click **Next**.</span></span>

    <span data-ttu-id="6c3f7-243">Otomatik olarak hello ağ üzerinden yedekleyebilir veya çevrimdışı yedekleme yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-243">You can back up automatically over hello network, or you can back up offline.</span></span> <span data-ttu-id="6c3f7-244">Bu makalenin sonraki bölümlerinde Hello otomatik olarak yedekleme hello işlemini açıklar.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-244">hello remainder of this article describes hello process for backing up automatically.</span></span> <span data-ttu-id="6c3f7-245">Çevrimdışı Yedekleme toodo tercih ederseniz, hello makalesini inceleyin [Azure backup'ta Çevrimdışı Yedekleme iş akışı](backup-azure-backup-import-export.md) ek bilgi için.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-245">If you prefer toodo an offline backup, review hello article [Offline backup workflow in Azure Backup](backup-azure-backup-import-export.md) for additional information.</span></span>
10. <span data-ttu-id="6c3f7-246">Merhaba onay sayfasında hello bilgileri gözden geçirin ve ardından **son**.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-246">On hello Confirmation page, review hello information, and then click **Finish**.</span></span>
11. <span data-ttu-id="6c3f7-247">Merhaba Sihirbazı hello yedekleme zamanlamasını oluşturduktan sonra tıklayın **Kapat**.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-247">After hello wizard finishes creating hello backup schedule, click **Close**.</span></span>

### <a name="tooback-up-files-and-folders-for-hello-first-time"></a><span data-ttu-id="6c3f7-248">Dosya ve klasörleri ilk kez hello için tooback</span><span class="sxs-lookup"><span data-stu-id="6c3f7-248">tooback up files and folders for hello first time</span></span>
1. <span data-ttu-id="6c3f7-249">Merhaba kurtarma Hizmetleri aracısında tıklatın **Şimdi Yedekle** toocomplete hello hello ağ üzerinden dengeli ilk.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-249">In hello Recovery Services agent, click **Back Up Now** toocomplete hello initial seeding over hello network.</span></span>

    ![Windows Server şimdi yedekle](./media/backup-try-azure-backup-in-10-mins/backup-now.png)
2. <span data-ttu-id="6c3f7-251">Merhaba onay sayfasında, Şimdi Yedekle sihirbazı hello hello ayarları gözden geçir hello makineyi tooback kullanır.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-251">On hello Confirmation page, review hello settings that hello Back Up Now Wizard will use tooback up hello machine.</span></span> <span data-ttu-id="6c3f7-252">Ardından **Yedekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-252">Then click **Back Up**.</span></span>
3. <span data-ttu-id="6c3f7-253">Tıklatın **Kapat** tooclose hello Sihirbazı.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-253">Click **Close** tooclose hello wizard.</span></span> <span data-ttu-id="6c3f7-254">Merhaba Sihirbazı Hello yedekleme işlemi tamamlanmadan önce kapatırsanız, Başlangıç Sihirbazı'nı toorun hello arka planda devam eder.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-254">If you close hello wizard before hello backup process finishes, hello wizard continues toorun in hello background.</span></span>

<span data-ttu-id="6c3f7-255">Merhaba ilk Yedekleme tamamlandıktan sonra hello **işi tamamlandı** durum hello yedekleme konsolunda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-255">After hello initial backup is completed, hello **Job completed** status appears in hello Backup console.</span></span>

![IR tamamlandı](./media/backup-try-azure-backup-in-10-mins/ircomplete.png)

## <a name="questions"></a><span data-ttu-id="6c3f7-257">Sorularınız mı var?</span><span class="sxs-lookup"><span data-stu-id="6c3f7-257">Questions?</span></span>
<span data-ttu-id="6c3f7-258">Sorularınız varsa veya herhangi bir özellik varsa dahil, toosee istediğiniz [Geri bildirimlerinizi bize gönderin](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="6c3f7-258">If you have questions, or if there is any feature that you would like toosee included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c3f7-259">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6c3f7-259">Next steps</span></span>
* <span data-ttu-id="6c3f7-260">[Windows makinelerini yedekleme](backup-configure-vault.md) konusunda daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="6c3f7-260">Get more details about [backing up Windows machines](backup-configure-vault.md).</span></span>
* <span data-ttu-id="6c3f7-261">Dosya ve klasörlerinizi yedeklediğinize göre artık [kasa ve sunucularınızı yönetebilirsiniz](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="6c3f7-261">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="6c3f7-262">Toorestore yedekleme ihtiyacınız varsa, bu makalede çok kullanmak[dosyaları tooa Windows makinesine geri](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="6c3f7-262">If you need toorestore a backup, use this article too[restore files tooa Windows machine](backup-azure-restore-windows-server.md).</span></span>
