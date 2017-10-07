---
title: "Dosya ve klasörleri aaaUse Azure Yedekleme aracısı tooback | Microsoft Docs"
description: "Windows dosya ve klasörleri tooAzure yukarı Hello Microsoft Azure Yedekleme aracısı tooback kullanın. Kurtarma Hizmetleri kasası oluşturma, hello yedekleme aracısını yüklemek, hello yedekleme ilkenizi tanımlayın ve hello dosyalar ve klasörler üzerinde hello ilk yedeklemeyi çalıştırın."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "Yedekleme kasası; bir Windows server'ı Yedekle; Yedekleme pencereleri;"
ms.assetid: 7f5b1943-b3c1-4ddb-8fb7-3560533c68d5
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: be203c24841971872b5c6e7cf260a2fa5c58ac47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-windows-server-or-client-tooazure-using-hello-resource-manager-deployment-model"></a><span data-ttu-id="34228-105">Merhaba Resource Manager dağıtım modelini kullanarak bir Windows Server ya da istemci tooAzure yedekleyin</span><span class="sxs-lookup"><span data-stu-id="34228-105">Back up a Windows Server or client tooAzure using hello Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="34228-106">Azure portal</span><span class="sxs-lookup"><span data-stu-id="34228-106">Azure portal</span></span>](backup-configure-vault.md)
> * [<span data-ttu-id="34228-107">Klasik portal</span><span class="sxs-lookup"><span data-stu-id="34228-107">Classic portal</span></span>](backup-configure-vault-classic.md)
>
>

<span data-ttu-id="34228-108">Bu makalede, Resource Manager dağıtım modeli kullanarak Azure Backup ile tooback, Windows Server (veya Windows istemcisi) dosya ve klasörleri tooAzure hello nasıl açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="34228-108">This article explains how tooback up your Windows Server (or Windows client) files and folders tooAzure with Azure Backup using hello Resource Manager deployment model.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/backup-deployment-models.md)]

![Yedekleme işlemi adımları](./media/backup-configure-vault/initial-backup-process.png)

## <a name="before-you-start"></a><span data-ttu-id="34228-110">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="34228-110">Before you start</span></span>
<span data-ttu-id="34228-111">bir sunucu veya istemci tooAzure tooback, bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="34228-111">tooback up a server or client tooAzure, you need an Azure account.</span></span> <span data-ttu-id="34228-112">Yoksa, oluşturabileceğiniz bir [ücretsiz bir hesap](https://azure.microsoft.com/free/) yalnızca birkaç dakika içinde.</span><span class="sxs-lookup"><span data-stu-id="34228-112">If you don't have one, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="34228-113">Kurtarma Hizmetleri kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="34228-113">Create a Recovery Services vault</span></span>
<span data-ttu-id="34228-114">Kurtarma Hizmetleri kasası tüm hello yedeklemeleri ve zaman içinde oluşturduğunuz kurtarma noktalarını depolayan bir varlıktır.</span><span class="sxs-lookup"><span data-stu-id="34228-114">A Recovery Services vault is an entity that stores all hello backups and recovery points you create over time.</span></span> <span data-ttu-id="34228-115">Hello kurtarma Hizmetleri kasası ayrıca hello uygulanan yedekleme ilkesini toohello korumalı dosyaları ve klasörleri içerir.</span><span class="sxs-lookup"><span data-stu-id="34228-115">hello Recovery Services vault also contains hello backup policy applied toohello protected files and folders.</span></span> <span data-ttu-id="34228-116">Kurtarma Hizmetleri kasası oluşturduğunuzda, aynı zamanda hello uygun depolama artıklığı seçeneği işaretlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="34228-116">When you create a Recovery Services vault, you should also select hello appropriate storage redundancy option.</span></span>

### <a name="toocreate-a-recovery-services-vault"></a><span data-ttu-id="34228-117">toocreate bir kurtarma Hizmetleri kasası</span><span class="sxs-lookup"><span data-stu-id="34228-117">toocreate a Recovery Services vault</span></span>
1. <span data-ttu-id="34228-118">Zaten yapmadıysanız, toohello içinde oturum [Azure Portal](https://portal.azure.com/) Azure aboneliğinizi kullanarak.</span><span class="sxs-lookup"><span data-stu-id="34228-118">If you haven't already done so, sign in toohello [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="34228-119">Merhaba Hub menüsünde **daha fazla hizmet** ve kaynakları hello listesinde yazın **kurtarma Hizmetleri** tıklatıp **kurtarma Hizmetleri kasaları**.</span><span class="sxs-lookup"><span data-stu-id="34228-119">On hello Hub menu, click **More services** and in hello list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![Kurtarma Hizmetleri Kasası oluşturma 1. adım](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="34228-121">Merhaba abonelikte kurtarma Hizmetleri kasaları varsa hello kasalarını listelenir.</span><span class="sxs-lookup"><span data-stu-id="34228-121">If there are recovery services vaults in hello subscription, hello vaults are listed.</span></span>

3. <span data-ttu-id="34228-122">Merhaba üzerinde **kurtarma Hizmetleri kasaları** menüsünde tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="34228-122">On hello **Recovery Services vaults** menu, click **Add**.</span></span>

    ![Kurtarma Hizmetleri Kasası oluşturma 2. adım](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="34228-124">Merhaba kurtarma Hizmetleri kasası dikey penceresi açılır tooprovide isteyen bir **adı**, **abonelik**, **kaynak grubu**, ve **konumu**.</span><span class="sxs-lookup"><span data-stu-id="34228-124">hello Recovery Services vault blade opens, prompting you tooprovide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Kurtarma Hizmetleri Kasası Oluşturma 3. adım](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="34228-126">İçin **adı**, bir kolay ad tooidentify hello kasası girin.</span><span class="sxs-lookup"><span data-stu-id="34228-126">For **Name**, enter a friendly name tooidentify hello vault.</span></span> <span data-ttu-id="34228-127">Merhaba adı toobe hello Azure aboneliği için benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="34228-127">hello name needs toobe unique for hello Azure subscription.</span></span> <span data-ttu-id="34228-128">2 ila 50 karakterden oluşan bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="34228-128">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="34228-129">Ad bir harf ile başlamalıdır ve yalnızca harf, rakam ve kısa çizgi içerebilir.</span><span class="sxs-lookup"><span data-stu-id="34228-129">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="34228-130">Merhaba, **abonelik** bölümünde, hello açılır menü toochoose hello Azure aboneliği kullanın.</span><span class="sxs-lookup"><span data-stu-id="34228-130">In hello **Subscription** section, use hello drop-down menu toochoose hello Azure subscription.</span></span> <span data-ttu-id="34228-131">Yalnızca bir abonelik kullanırsanız, bu abonelik görünür ve toohello sonraki adımı atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34228-131">If you use only one subscription, that subscription appears and you can skip toohello next step.</span></span> <span data-ttu-id="34228-132">Hangi abonelik toouse emin değilseniz, hello varsayılan kullanın (veya önerilen) aboneliği.</span><span class="sxs-lookup"><span data-stu-id="34228-132">If you are not sure which subscription toouse, use hello default (or suggested) subscription.</span></span> <span data-ttu-id="34228-133">Yalnızca kuruluş hesabınızın birden çok Azure aboneliği ile ilişkili olması durumunda birden çok seçenek olur.</span><span class="sxs-lookup"><span data-stu-id="34228-133">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="34228-134">Merhaba, **kaynak grubu** bölümü:</span><span class="sxs-lookup"><span data-stu-id="34228-134">In hello **Resource group** section:</span></span>

    * <span data-ttu-id="34228-135">seçin **Yeni Oluştur** toocreate yeni bir kaynak grubu istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="34228-135">select **Create new** if you want toocreate a new Resource group.</span></span>
    <span data-ttu-id="34228-136">Veya</span><span class="sxs-lookup"><span data-stu-id="34228-136">Or</span></span>
    * <span data-ttu-id="34228-137">seçin **var olanı kullan** ve hello açılır menü toosee hello kullanılabilir kaynak gruplarının listesini'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="34228-137">select **Use existing** and click hello drop-down menu toosee hello available list of Resource groups.</span></span>

  <span data-ttu-id="34228-138">Kaynak grupları hakkında tam bilgi için bkz: Merhaba [Azure Resource Manager'a genel bakış](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="34228-138">For complete information on Resource groups, see hello [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="34228-139">Tıklatın **konumu** tooselect hello hello kasa için coğrafi bölgeyi.</span><span class="sxs-lookup"><span data-stu-id="34228-139">Click **Location** tooselect hello geographic region for hello vault.</span></span> <span data-ttu-id="34228-140">Bu seçim, yedekleme verilerinizi burada gönderilen hello coğrafi bölgeyi belirler.</span><span class="sxs-lookup"><span data-stu-id="34228-140">This choice determines hello geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="34228-141">Merhaba kurtarma Hizmetleri kasası dikey penceresinde Hello altındaki tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="34228-141">At hello bottom of hello Recovery Services vault blade, click **Create**.</span></span>

  <span data-ttu-id="34228-142">Oluşturulan toobe kurtarma Hizmetleri kasası hello için birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="34228-142">It can take several minutes for hello Recovery Services vault toobe created.</span></span> <span data-ttu-id="34228-143">Merhaba portal hello üst sağ bölmesinde Hello durum bildirimlerini izleyin.</span><span class="sxs-lookup"><span data-stu-id="34228-143">Monitor hello status notifications in hello upper right-hand area of hello portal.</span></span> <span data-ttu-id="34228-144">Kasanız oluşturulduktan sonra hello kurtarma Hizmetleri kasaları listesinde görünür.</span><span class="sxs-lookup"><span data-stu-id="34228-144">Once your vault is created, it appears in hello list of Recovery Services vaults.</span></span> <span data-ttu-id="34228-145">Birkaç dakika sonra kasayı görmezseniz **Yenile**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="34228-145">If after several minutes you don't see your vault, click **Refresh**.</span></span>

  ![Yenile düğmesine tıklayın](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

  <span data-ttu-id="34228-147">Kasanızı kurtarma Hizmetleri kasalarının hello listesinde gördüğünüz verdikten sonra hazır tooset hello depolama artıklığı demektir.</span><span class="sxs-lookup"><span data-stu-id="34228-147">Once you see your vault in hello list of Recovery Services vaults, you are ready tooset hello storage redundancy.</span></span>


### <a name="set-storage-redundancy"></a><span data-ttu-id="34228-148">Küme depolama artıklığı</span><span class="sxs-lookup"><span data-stu-id="34228-148">Set storage redundancy</span></span>
<span data-ttu-id="34228-149">Bir Kurtarma Hizmetleri kasasını ilk oluşturduğunuzda depolamanın nasıl çoğaltılacağını belirlersiniz.</span><span class="sxs-lookup"><span data-stu-id="34228-149">When you first create a Recovery Services vault you determine how storage is replicated.</span></span>

1. <span data-ttu-id="34228-150">Merhaba gelen **kurtarma Hizmetleri kasaları** dikey penceresinde hello yeni kasaya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="34228-150">From hello **Recovery Services vaults** blade, click hello new vault.</span></span>

    ![Kurtarma Hizmetleri kasası hello listeden Hello yeni kasa seçin](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="34228-152">Merhaba kasası seçtiğinizde hello **kurtarma Hizmetleri kasası** dikey daraltır ve hello ayarları dikey (*hello üstünde hello kasasının hello ada sahip*) ve hello kasa Ayrıntılar dikey penceresini açın.</span><span class="sxs-lookup"><span data-stu-id="34228-152">When you select hello vault, hello **Recovery Services vault** blade narrows, and hello Settings blade (*which has hello name of hello vault at hello top*) and hello vault details blade open.</span></span>

    ![Yeni kasa için Görünüm hello depolama yapılandırması](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)

2. <span data-ttu-id="34228-154">Merhaba yeni kasasının ayarlar dikey penceresinde hello dikey slayt tooscroll toohello Yönet bölümüne aşağı kullanın ve'ı tıklatın **Yedekleme Altyapısı**.</span><span class="sxs-lookup"><span data-stu-id="34228-154">In hello new vault's Settings blade, use hello vertical slide tooscroll down toohello Manage section, and click **Backup Infrastructure**.</span></span>

  <span data-ttu-id="34228-155">Merhaba yedekleme altyapısı dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="34228-155">hello Backup Infrastructure blade opens.</span></span>

3. <span data-ttu-id="34228-156">Merhaba yedekleme altyapısı dikey penceresinde tıklayın **yedekleme yapılandırması** tooopen hello **yedekleme yapılandırması** dikey.</span><span class="sxs-lookup"><span data-stu-id="34228-156">In hello Backup Infrastructure blade, click **Backup Configuration** tooopen hello **Backup Configuration** blade.</span></span>

  ![Yeni kasa Hello depolama yapılandırmasını ayarlayın](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)

4. <span data-ttu-id="34228-158">Kasanız için Hello uygun depolama çoğaltma seçeneğini seçin.</span><span class="sxs-lookup"><span data-stu-id="34228-158">Choose hello appropriate storage replication option for your vault.</span></span>

  ![depolama yapılandırması seçenekleri](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

  <span data-ttu-id="34228-160">Varsayılan olarak, kasanız coğrafi olarak yedekli depolamaya sahiptir.</span><span class="sxs-lookup"><span data-stu-id="34228-160">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="34228-161">Azure birincil yedekleme alanı uç noktası kullanıyorsanız, toouse devam **coğrafi olarak yedekli**.</span><span class="sxs-lookup"><span data-stu-id="34228-161">If you use Azure as a primary backup storage endpoint, continue toouse **Geo-redundant**.</span></span> <span data-ttu-id="34228-162">Birincil yedekleme alanı uç noktası Azure kullanmıyorsanız, ardından **yerel olarak yedekli**, hello Azure depolama maliyetlerini azaltır.</span><span class="sxs-lookup"><span data-stu-id="34228-162">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces hello Azure storage costs.</span></span> <span data-ttu-id="34228-163">[Coğrafi olarak yedekli](../storage/common/storage-redundancy.md#geo-redundant-storage) ve [yerel olarak yedekli](../storage/common/storage-redundancy.md#locally-redundant-storage) depolama seçenekleri hakkında daha fazla bilgiyi [Depolama yedekliliğine genel bakış](../storage/common/storage-redundancy.md) bölümünden edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34228-163">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="34228-164">Bir kasa oluşturduğunuza göre indirme ve hello Microsoft Azure kurtarma Hizmetleri aracısını yükleyerek, kasa kimlik bilgilerini indirme ve bu kimlik bilgileri tooregister hello aracısını kullanarak, altyapı tooback dosya ve klasörleri hazırlama Merhaba kasası.</span><span class="sxs-lookup"><span data-stu-id="34228-164">Now that you've created a vault, prepare your infrastructure tooback up files and folders by downloading and installing hello Microsoft Azure Recovery Services agent, downloading vault credentials, and then using those credentials tooregister hello agent with hello vault.</span></span>

## <a name="configure-hello-vault"></a><span data-ttu-id="34228-165">Merhaba kasası yapılandırma</span><span class="sxs-lookup"><span data-stu-id="34228-165">Configure hello vault</span></span>

1. <span data-ttu-id="34228-166">Açık kurtarma Hizmetleri kasası dikey (Merhaba kasa), yeni oluşturduğunuz, hello Başlarken bölümünde Merhaba, tıklatın **yedekleme**, sonra da hello **yedekleme ile çalışmaya başlama** dikey penceresinde, select  **Yedekleme hedefi**.</span><span class="sxs-lookup"><span data-stu-id="34228-166">On hello Recovery Services vault blade (for hello vault you just created), in hello Getting Started section, click **Backup**, then on hello **Getting Started with Backup** blade, select **Backup goal**.</span></span>

  ![Yedekleme hedefi dikey penceresini açma](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

  <span data-ttu-id="34228-168">Merhaba **yedekleme hedefi** dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="34228-168">hello **Backup Goal** blade opens.</span></span> <span data-ttu-id="34228-169">Kurtarma Hizmetleri kasası hello önceden yapılandırılmışsa, ardından hello **yedekleme hedefi** dikey pencere açılır tıkladığınızda **yedekleme** hello kurtarma Hizmetleri kasası dikey penceresi.</span><span class="sxs-lookup"><span data-stu-id="34228-169">If hello Recovery Services vault has been previously configured, then hello **Backup Goal** blades opens when you click **Backup** on hello Recovery Services vault blade.</span></span>

  ![Yedekleme hedefi dikey penceresini açma](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="34228-171">Merhaba gelen **, iş yükünü çalıştırdığı?** açılır menüsünde, select **şirket içi**.</span><span class="sxs-lookup"><span data-stu-id="34228-171">From hello **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

  <span data-ttu-id="34228-172">Windows Server veya Windows bilgisayarınız Azure üzerinde olmayan fiziksel bir makine olduğu için **Şirket içi** seçeneğini belirlersiniz.</span><span class="sxs-lookup"><span data-stu-id="34228-172">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="34228-173">Merhaba gelen **neler toobackup istediğiniz?** menüsünde, select **dosya ve klasörleri**, tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="34228-173">From hello **What do you want toobackup?** menu, select **Files and folders**, and click **OK**.</span></span>

  ![Dosya ve klasörleri yedekleme](./media/backup-try-azure-backup-in-10-mins/set-file-folder.png)

  <span data-ttu-id="34228-175">Tamam'ı tıklattıktan sonra bir onay işareti çok sonraki görünür**yedekleme hedefi**ve hello **altyapıyı hazırlama** dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="34228-175">After clicking OK, a checkmark appears next too**Backup goal**, and hello **Prepare infrastructure** blade opens.</span></span>

  ![Yedekleme hedefi yapılandırılmıştır, bundan sonra altyapıyı hazırlayın](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="34228-177">Merhaba üzerinde **altyapıyı hazırlama** dikey penceresinde tıklatın **karşıdan aracısı için Windows Server veya Windows İstemcisi**.</span><span class="sxs-lookup"><span data-stu-id="34228-177">On hello **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

  ![altyapıyı hazırlama](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

  <span data-ttu-id="34228-179">Windows Server temel kullanıyorsanız, Windows Server temel için toodownload hello Aracısı seçin.</span><span class="sxs-lookup"><span data-stu-id="34228-179">If you are using Windows Server Essential, then choose toodownload hello agent for Windows Server Essential.</span></span> <span data-ttu-id="34228-180">Açılır menü toorun komut istemleri veya MARSAgentInstaller.exe kaydedin.</span><span class="sxs-lookup"><span data-stu-id="34228-180">A pop-up menu prompts you toorun or save MARSAgentInstaller.exe.</span></span>

  ![MARSAgentInstaller iletişim kutusu](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="34228-182">Merhaba indirme açılır menüsünde tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="34228-182">In hello download pop-up menu, click **Save**.</span></span>

  <span data-ttu-id="34228-183">Varsayılan olarak, hello **MARSagentinstaller.exe** dosya tooyour indirmeler klasörüne kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="34228-183">By default, hello **MARSagentinstaller.exe** file is saved tooyour Downloads folder.</span></span> <span data-ttu-id="34228-184">Merhaba yükleyici tamamladığında, toorun hello yükleyici istediğiniz veya hello klasörünü açın, isteyen bir açılır pencere görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="34228-184">When hello installer completes, you will see a pop-up asking if you want toorun hello installer, or open hello folder.</span></span>

  ![altyapıyı hazırlama](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

  <span data-ttu-id="34228-186">Tooinstall hello Aracısı henüz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="34228-186">You don't need tooinstall hello agent yet.</span></span> <span data-ttu-id="34228-187">Merhaba kasa kimlik bilgileri indirdikten sonra hello aracısını yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34228-187">You can install hello agent after you have downloaded hello vault credentials.</span></span>

6. <span data-ttu-id="34228-188">Merhaba üzerinde **altyapıyı hazırlama** dikey penceresinde tıklatın **karşıdan**.</span><span class="sxs-lookup"><span data-stu-id="34228-188">On hello **Prepare infrastructure** blade, click **Download**.</span></span>

  ![kasa kimlik bilgilerini indirme](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

  <span data-ttu-id="34228-190">Merhaba kasa kimlik bilgileri tooyour indirmeler klasörüne indirin.</span><span class="sxs-lookup"><span data-stu-id="34228-190">hello vault credentials download tooyour Downloads folder.</span></span> <span data-ttu-id="34228-191">Hello kasa kimlik bilgilerini indirme işlemini tamamladıktan sonra tooopen istediğiniz veya hello kimlik bilgilerini Kaydet isteyen bir açılır pencere görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="34228-191">After hello vault credentials finish downloading, you see a pop-up asking if you want tooopen or save hello credentials.</span></span> <span data-ttu-id="34228-192">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="34228-192">Click **Save**.</span></span> <span data-ttu-id="34228-193">Yanlışlıkla tıklatırsanız **açık**, tooopen hello kasa kimlik bilgileri çalışır hello iletişim sağlar, başarısız.</span><span class="sxs-lookup"><span data-stu-id="34228-193">If you accidentally click **Open**, let hello dialog that attempts tooopen hello vault credentials, fail.</span></span> <span data-ttu-id="34228-194">Merhaba kasa kimlik bilgileri açamıyor.</span><span class="sxs-lookup"><span data-stu-id="34228-194">You cannot open hello vault credentials.</span></span> <span data-ttu-id="34228-195">Toohello sonraki adıma geçin.</span><span class="sxs-lookup"><span data-stu-id="34228-195">Proceed toohello next step.</span></span> <span data-ttu-id="34228-196">Merhaba kasa kimlik bilgileri hello indirme klasöründe yer alır.</span><span class="sxs-lookup"><span data-stu-id="34228-196">hello vault credentials are in hello Downloads folder.</span></span>   

  ![kasa kimlik bilgilerini indirme tamamlandı](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-hello-agent"></a><span data-ttu-id="34228-198">Yükleme ve hello Aracısı kaydedin</span><span class="sxs-lookup"><span data-stu-id="34228-198">Install and register hello agent</span></span>

> [!NOTE]
> <span data-ttu-id="34228-199">Hello Azure portal üzerinden yedeklemeyi etkinleştirme olanağı henüz kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="34228-199">Enabling backup through hello Azure portal is not available, yet.</span></span> <span data-ttu-id="34228-200">Dosya ve klasörleri Hello Microsoft Azure kurtarma Hizmetleri Aracısı tooback kullanın.</span><span class="sxs-lookup"><span data-stu-id="34228-200">Use hello Microsoft Azure Recovery Services Agent tooback up your files and folders.</span></span>
>

1. <span data-ttu-id="34228-201">Bulun ve çift hello **MARSagentinstaller.exe** hello yükleme klasöründen (veya diğer kayıtlı konumdan).</span><span class="sxs-lookup"><span data-stu-id="34228-201">Locate and double-click hello **MARSagentinstaller.exe** from hello Downloads folder (or other saved location).</span></span>

  <span data-ttu-id="34228-202">Merhaba yükleyici, bir dizi ileti ayıklar gibi yükler ve hello kurtarma Hizmetleri aracısını kaydeder sağlar.</span><span class="sxs-lookup"><span data-stu-id="34228-202">hello installer provides a series of messages as it extracts, installs, and registers hello Recovery Services agent.</span></span>

  ![Kurtarma Hizmetleri aracısı yükleyici kimlik bilgilerini çalıştırma](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="34228-204">Merhaba Microsoft Azure kurtarma Hizmetleri Aracısı Kurulum Sihirbazı tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="34228-204">Complete hello Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="34228-205">toocomplete Başlangıç Sihirbazı, şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="34228-205">toocomplete hello wizard, you need to:</span></span>

  * <span data-ttu-id="34228-206">Merhaba yükleme ve önbellek klasörü için bir konum seçin.</span><span class="sxs-lookup"><span data-stu-id="34228-206">Choose a location for hello installation and cache folder.</span></span>
  * <span data-ttu-id="34228-207">Bir proxy sunucu tooconnect toohello kullanırsanız, Ara sunucu bilgilerinizi sağlayın Internet.</span><span class="sxs-lookup"><span data-stu-id="34228-207">Provide your proxy server info if you use a proxy server tooconnect toohello internet.</span></span>
  * <span data-ttu-id="34228-208">Kimliği doğrulanmış bir ara sunucu kullanıyorsanız kullanıcı adı ve parola bilgilerinizi sağlayın.</span><span class="sxs-lookup"><span data-stu-id="34228-208">Provide your user name and password details if you use an authenticated proxy.</span></span>
  * <span data-ttu-id="34228-209">Merhaba indirilen kasa kimlik bilgilerini sağlayın</span><span class="sxs-lookup"><span data-stu-id="34228-209">Provide hello downloaded vault credentials</span></span>
  * <span data-ttu-id="34228-210">Merhaba şifreleme parolası güvenli bir konuma kaydedin.</span><span class="sxs-lookup"><span data-stu-id="34228-210">Save hello encryption passphrase in a secure location.</span></span>

  > [!NOTE]
  > <span data-ttu-id="34228-211">Kaybeder veya hello parolayı unutursanız Microsoft hello yedekleme verilerini kurtarmanıza yardımcı olamaz.</span><span class="sxs-lookup"><span data-stu-id="34228-211">If you lose or forget hello passphrase, Microsoft cannot help recover hello backup data.</span></span> <span data-ttu-id="34228-212">Merhaba dosyayı güvenli bir konuma kaydedin.</span><span class="sxs-lookup"><span data-stu-id="34228-212">Save hello file in a secure location.</span></span> <span data-ttu-id="34228-213">Gerekli toorestore bir yedekleme olur.</span><span class="sxs-lookup"><span data-stu-id="34228-213">It is required toorestore a backup.</span></span>
  >
  >

<span data-ttu-id="34228-214">Merhaba aracı artık yüklenmiş ve kayıtlı toohello kasasına makineniz olduğu.</span><span class="sxs-lookup"><span data-stu-id="34228-214">hello agent is now installed and your machine is registered toohello vault.</span></span> <span data-ttu-id="34228-215">Hazır tooconfigure olduğunuz ve yedekleme zamanlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34228-215">You're ready tooconfigure and schedule your backup.</span></span>

## <a name="network-and-connectivity-requirements"></a><span data-ttu-id="34228-216">Ağ ve Bağlantı Gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="34228-216">Network and Connectivity Requirements</span></span>

<span data-ttu-id="34228-217">Makine/proxy Internet erişimi sınırlı hello makine/proxy üzerinde güvenlik duvarı ayarlarını aşağıdaki URL'lere yapılandırılmış tooallow hello olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="34228-217">If your machine/proxy has limited internet access, ensure that firewall settings on hello machine/proxy are configured tooallow hello following URLs:</span></span> <br>
    1. <span data-ttu-id="34228-218">www.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="34228-218">www.msftncsi.com</span></span>
    2. <span data-ttu-id="34228-219">*.Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="34228-219">*.Microsoft.com</span></span>
    3. <span data-ttu-id="34228-220">*.WindowsAzure.com</span><span class="sxs-lookup"><span data-stu-id="34228-220">*.WindowsAzure.com</span></span>
    4. <span data-ttu-id="34228-221">*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="34228-221">*.microsoftonline.com</span></span>
    5. <span data-ttu-id="34228-222">*.windows.ne</span><span class="sxs-lookup"><span data-stu-id="34228-222">*.windows.ne</span></span>


## <a name="create-hello-backup-policy"></a><span data-ttu-id="34228-223">Merhaba yedekleme ilkesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="34228-223">Create hello backup policy</span></span>
<span data-ttu-id="34228-224">Kurtarma noktaları alınır ve hello kurtarma noktalarının bekletileceği süre hello hello yedekleme İlkesi hello zamanlamadır.</span><span class="sxs-lookup"><span data-stu-id="34228-224">hello backup policy is hello schedule when recovery points are taken, and hello length of time hello recovery points are retained.</span></span> <span data-ttu-id="34228-225">Merhaba Microsoft Azure Yedekleme aracısı toocreate hello yedekleme ilkesinin dosya ve klasörler için kullanın.</span><span class="sxs-lookup"><span data-stu-id="34228-225">Use hello Microsoft Azure Backup agent toocreate hello backup policy for files and folders.</span></span>

### <a name="toocreate-a-backup-schedule"></a><span data-ttu-id="34228-226">toocreate bir yedekleme zamanlaması</span><span class="sxs-lookup"><span data-stu-id="34228-226">toocreate a backup schedule</span></span>
1. <span data-ttu-id="34228-227">Merhaba Microsoft Azure yedekleme Aracısı'nı açın.</span><span class="sxs-lookup"><span data-stu-id="34228-227">Open hello Microsoft Azure Backup agent.</span></span> <span data-ttu-id="34228-228">Bunu, makinenizde **Microsoft Azure Backup** aramasını yaparak bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34228-228">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Hello Azure Backup aracısını başlatma](./media/backup-configure-vault/snap-in-search.png)
2. <span data-ttu-id="34228-230">Merhaba yedekleme aracısının içinde **Eylemler** bölmesinde tıklatın **yedekleme zamanlaması** toolaunch hello yedeklemeyi Zamanlama Sihirbazı.</span><span class="sxs-lookup"><span data-stu-id="34228-230">In hello Backup agent's **Actions** pane, click **Schedule Backup** toolaunch hello Schedule Backup Wizard.</span></span>

    ![Windows Server yedeklemesini zamanlama](./media/backup-configure-vault/schedule-first-backup.png)

3. <span data-ttu-id="34228-232">Merhaba üzerinde **Başlarken** hello yedeklemeyi Zamanlama Sihirbazı sayfasını tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="34228-232">On hello **Getting started** page of hello Schedule Backup Wizard, click **Next**.</span></span>
4. <span data-ttu-id="34228-233">Merhaba üzerinde **öğeleri seçin tooBackup** sayfasında, **öğeleri Ekle**.</span><span class="sxs-lookup"><span data-stu-id="34228-233">On hello **Select Items tooBackup** page, click **Add Items**.</span></span>

  <span data-ttu-id="34228-234">Merhaba öğeleri seçin iletişim kutusu açılır.</span><span class="sxs-lookup"><span data-stu-id="34228-234">hello Select Items dialog opens.</span></span>

5. <span data-ttu-id="34228-235">Merhaba dosyalar ve klasörler tooprotect istediğiniz ve ardından seçin **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="34228-235">Select hello files and folders that you want tooprotect, and then click **OK**.</span></span>
6. <span data-ttu-id="34228-236">Merhaba, **öğeleri seçin tooBackup** sayfasında, **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="34228-236">In hello **Select Items tooBackup** page, click **Next**.</span></span>
7. <span data-ttu-id="34228-237">Merhaba üzerinde **yedekleme zamanlamasını belirtin** sayfasında, hello yedekleme zamanlamasını ve tıklatın belirtin **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="34228-237">On hello **Specify Backup Schedule** page, specify hello backup schedule and click **Next**.</span></span>

    <span data-ttu-id="34228-238">Günlük (en fazla günde üç kez olmak üzere) veya haftalık yedeklemeler zamanlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34228-238">You can schedule daily (at a maximum rate of three times per day) or weekly backups.</span></span>

    ![Windows Server Yedekleme öğeleri](./media/backup-configure-vault/specify-backup-schedule-close.png)

   > [!NOTE]
   > <span data-ttu-id="34228-240">Merhaba makale nasıl toospecify hello yedekleme zamanlaması hakkında daha fazla bilgi için bkz: [kullanım Azure yedekleme tooreplace bant altyapınızın](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="34228-240">For more information about how toospecify hello backup schedule, see hello article [Use Azure Backup tooreplace your tape infrastructure](backup-azure-backup-cloud-as-tape.md).</span></span>
   >
   >

8. <span data-ttu-id="34228-241">Merhaba üzerinde **bekletme ilkesi seçin** sayfasında hello belirli bekletme ilkeleri hello hello yedek kopya seçin ve tıklayın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="34228-241">On hello **Select Retention Policy** page, choose hello specific retention policies hello for hello backup copy and click **Next**.</span></span>

    <span data-ttu-id="34228-242">Merhaba bekletme ilkesi hangi hello yedekleme depolanan hello süresini belirtir.</span><span class="sxs-lookup"><span data-stu-id="34228-242">hello retention policy specifies hello duration which hello backup is stored.</span></span> <span data-ttu-id="34228-243">Yalnızca tüm yedekleme noktaları için "sabit ilke" belirtmek yerine, hello yedekleme gerçekleştiğinde göre farklı bekletme ilkeleri belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34228-243">Rather than just specifying a “flat policy” for all backup points, you can specify different retention policies based on when hello backup occurs.</span></span> <span data-ttu-id="34228-244">Merhaba günlük, haftalık, aylık ve yıllık bekletme ilkeleri toomeet gereksinimlerinizi değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34228-244">You can modify hello daily, weekly, monthly, and yearly retention policies toomeet your needs.</span></span>
9. <span data-ttu-id="34228-245">Merhaba ilk yedekleme türünü seçin sayfasında hello ilk yedekleme türünü seçin.</span><span class="sxs-lookup"><span data-stu-id="34228-245">On hello Choose Initial Backup Type page, choose hello initial backup type.</span></span> <span data-ttu-id="34228-246">Merhaba seçeneği bırakın **hello ağ üzerinden otomatik olarak** seçili ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="34228-246">Leave hello option **Automatically over hello network** selected, and then click **Next**.</span></span>

    <span data-ttu-id="34228-247">Otomatik olarak hello ağ üzerinden yedekleyebilir veya çevrimdışı yedekleme yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34228-247">You can back up automatically over hello network, or you can back up offline.</span></span> <span data-ttu-id="34228-248">Bu makalenin sonraki bölümlerinde Hello otomatik olarak yedekleme hello işlemini açıklar.</span><span class="sxs-lookup"><span data-stu-id="34228-248">hello remainder of this article describes hello process for backing up automatically.</span></span> <span data-ttu-id="34228-249">Çevrimdışı Yedekleme toodo tercih ederseniz, hello makalesini inceleyin [Azure backup'ta Çevrimdışı Yedekleme iş akışı](backup-azure-backup-import-export.md) ek bilgi için.</span><span class="sxs-lookup"><span data-stu-id="34228-249">If you prefer toodo an offline backup, review hello article [Offline backup workflow in Azure Backup](backup-azure-backup-import-export.md) for additional information.</span></span>
10. <span data-ttu-id="34228-250">Merhaba onay sayfasında hello bilgileri gözden geçirin ve ardından **son**.</span><span class="sxs-lookup"><span data-stu-id="34228-250">On hello Confirmation page, review hello information, and then click **Finish**.</span></span>
11. <span data-ttu-id="34228-251">Merhaba Sihirbazı hello yedekleme zamanlamasını oluşturduktan sonra tıklayın **Kapat**.</span><span class="sxs-lookup"><span data-stu-id="34228-251">After hello wizard finishes creating hello backup schedule, click **Close**.</span></span>

### <a name="enable-network-throttling"></a><span data-ttu-id="34228-252">Ağ azaltmayı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="34228-252">Enable network throttling</span></span>
<span data-ttu-id="34228-253">Merhaba Microsoft Azure Yedekleme aracısı, ağ azaltma sağlar.</span><span class="sxs-lookup"><span data-stu-id="34228-253">hello Microsoft Azure Backup agent provides network throttling.</span></span> <span data-ttu-id="34228-254">Veri aktarımı sırasında ağ bant genişliğinin nasıl kullanıldığını denetimleri azaltma.</span><span class="sxs-lookup"><span data-stu-id="34228-254">Throttling controls how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="34228-255">Bu denetim verileri tooback çalışma saatlerinde gerekir, ancak diğer Internet trafiği ile Merhaba yedekleme işlemi toointerfere istiyor musunuz yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="34228-255">This control can be helpful if you need tooback up data during work hours but do not want hello backup process toointerfere with other Internet traffic.</span></span> <span data-ttu-id="34228-256">Azaltma yukarıya tooback uygular ve geri yükleme etkinlikleri.</span><span class="sxs-lookup"><span data-stu-id="34228-256">Throttling applies tooback up and restore activities.</span></span>

> [!NOTE]
> <span data-ttu-id="34228-257">Ağ azaltma (hizmet paketleri ile) Windows Server 2008 R2 SP1, Windows Server 2008 SP2 veya Windows 7 üzerinde kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="34228-257">Network throttling is not available on Windows Server 2008 R2 SP1, Windows Server 2008 SP2, or Windows 7 (with service packs).</span></span> <span data-ttu-id="34228-258">özellik azaltma hello Azure Backup ağ hizmet kalitesi (QoS) hello yerel işletim sisteminde ilgilenir.</span><span class="sxs-lookup"><span data-stu-id="34228-258">hello Azure Backup network throttling feature engages Quality of Service (QoS) on hello local operating system.</span></span> <span data-ttu-id="34228-259">Azure Backup bu işletim sistemlerini korumak için de, QoS bu platformlarda kullanılabilir hello sürümü Azure Backup ağ azaltma ile çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="34228-259">Though Azure Backup can protect these operating systems, hello version of QoS available on these platforms doesn't work with Azure Backup network throttling.</span></span> <span data-ttu-id="34228-260">Ağ azaltma kullanılabilir tüm diğer bağlı [desteklenen işletim sistemleri](backup-azure-backup-faq.md).</span><span class="sxs-lookup"><span data-stu-id="34228-260">Network throttling can be used on all other [supported operating systems](backup-azure-backup-faq.md).</span></span>
>
>

<span data-ttu-id="34228-261">**tooenable ağ azaltma**</span><span class="sxs-lookup"><span data-stu-id="34228-261">**tooenable network throttling**</span></span>

1. <span data-ttu-id="34228-262">Merhaba Microsoft Azure yedekleme aracı tıklatın **özelliklerini değiştirme**.</span><span class="sxs-lookup"><span data-stu-id="34228-262">In hello Microsoft Azure Backup agent, click **Change Properties**.</span></span>

    ![Özelliklerini değiştir](./media/backup-configure-vault/change-properties.png)
2. <span data-ttu-id="34228-264">Merhaba üzerinde **azaltma** sekmesi, select hello **yedekleme işlemleri için Internet bant genişliği kullanımı daraltmayı etkinleştir** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="34228-264">On hello **Throttling** tab, select hello **Enable internet bandwidth usage throttling for backup operations** check box.</span></span>

    ![Ağ azaltma](./media/backup-configure-vault/throttling-dialog.png)
3. <span data-ttu-id="34228-266">Azaltma etkinleştirdikten sonra sırasında yedek veri aktarımı için bant genişliği izin verilen hello belirtin **çalışma saatleri** ve **çalışılmayan saatler**.</span><span class="sxs-lookup"><span data-stu-id="34228-266">After you have enabled throttling, specify hello allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="34228-267">Merhaba bant genişliği değerler 512 kilobit / saniye (Kbps) başlar ve too1, 023 megabayt (MBps) saniyede yukarı gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34228-267">hello bandwidth values begin at 512 kilobits per second (Kbps) and can go up too1,023 megabytes per second (MBps).</span></span> <span data-ttu-id="34228-268">Ayrıca hello başlangıç belirleyin ve için son **çalışma saatleri**, ve hello haftanın hangi günleri dikkate alınan iş günlerini.</span><span class="sxs-lookup"><span data-stu-id="34228-268">You can also designate hello start and finish for **Work hours**, and which days of hello week are considered work days.</span></span> <span data-ttu-id="34228-269">Belirtilen iş saatleri kabul dışında saat saat İş dışı.</span><span class="sxs-lookup"><span data-stu-id="34228-269">Hours outside of designated work hours are considered non-work hours.</span></span>
4. <span data-ttu-id="34228-270">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="34228-270">Click **OK**.</span></span>

### <a name="tooback-up-files-and-folders-for-hello-first-time"></a><span data-ttu-id="34228-271">Dosya ve klasörleri ilk kez hello için tooback</span><span class="sxs-lookup"><span data-stu-id="34228-271">tooback up files and folders for hello first time</span></span>
1. <span data-ttu-id="34228-272">Merhaba yedekleme aracısını içinde tıklatın **Şimdi Yedekle** toocomplete hello hello ağ üzerinden dengeli ilk.</span><span class="sxs-lookup"><span data-stu-id="34228-272">In hello backup agent, click **Back Up Now** toocomplete hello initial seeding over hello network.</span></span>

    ![Windows Server şimdi yedekle](./media/backup-configure-vault/backup-now.png)
2. <span data-ttu-id="34228-274">Merhaba onay sayfasında, Şimdi Yedekle sihirbazı hello hello ayarları gözden geçir hello makineyi tooback kullanır.</span><span class="sxs-lookup"><span data-stu-id="34228-274">On hello Confirmation page, review hello settings that hello Back Up Now Wizard will use tooback up hello machine.</span></span> <span data-ttu-id="34228-275">Ardından **Yedekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="34228-275">Then click **Back Up**.</span></span>
3. <span data-ttu-id="34228-276">Tıklatın **Kapat** tooclose hello Sihirbazı.</span><span class="sxs-lookup"><span data-stu-id="34228-276">Click **Close** tooclose hello wizard.</span></span> <span data-ttu-id="34228-277">Merhaba yedekleme işlemi tamamlanmadan önce bunu yaparsanız, Başlangıç Sihirbazı'nı toorun hello arka planda devam eder.</span><span class="sxs-lookup"><span data-stu-id="34228-277">If you do this before hello backup process finishes, hello wizard continues toorun in hello background.</span></span>

<span data-ttu-id="34228-278">Merhaba ilk Yedekleme tamamlandıktan sonra hello **işi tamamlandı** durum hello yedekleme konsolunda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="34228-278">After hello initial backup is completed, hello **Job completed** status appears in hello Backup console.</span></span>

![IR tamamlandı](./media/backup-configure-vault/ircomplete.png)

## <a name="questions"></a><span data-ttu-id="34228-280">Sorularınız mı var?</span><span class="sxs-lookup"><span data-stu-id="34228-280">Questions?</span></span>
<span data-ttu-id="34228-281">Sorularınız varsa veya herhangi bir özellik varsa dahil, toosee istediğiniz [Geri bildirimlerinizi bize gönderin](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="34228-281">If you have questions, or if there is any feature that you would like toosee included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="34228-282">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="34228-282">Next steps</span></span>
<span data-ttu-id="34228-283">Sanal makineler veya diğer iş yüklerini yedekleme hakkında ek bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="34228-283">For additional information about backing up VMs or other workloads, see:</span></span>

* <span data-ttu-id="34228-284">Dosya ve klasörlerinizi yedeklediğinize göre artık [kasa ve sunucularınızı yönetebilirsiniz](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="34228-284">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="34228-285">Toorestore yedekleme ihtiyacınız varsa, bu makalede çok kullanmak[dosyaları tooa Windows makinesine geri](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="34228-285">If you need toorestore a backup, use this article too[restore files tooa Windows machine](backup-azure-restore-windows-server.md).</span></span>
