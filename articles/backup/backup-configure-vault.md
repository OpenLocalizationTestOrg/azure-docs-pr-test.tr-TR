---
title: "Dosyaları ve klasörleri yedeklemek için kullanım Azure Yedekleme aracısı | Microsoft Docs"
description: "Microsoft Azure Yedekleme aracısı Windows dosya ve klasörlerinizi Azure'a yedeklemek için kullanın. Bir kurtarma Hizmetleri kasası oluşturmanız, yedekleme aracısını yüklemek, yedekleme ilkesi tanımlama ve dosya ve klasörleri ilk yedeklemeyi çalıştırın."
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
ms.openlocfilehash: b95dc0a83d8e5618effb573353f419e1837d30c5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="back-up-a-windows-server-or-client-to-azure-using-the-resource-manager-deployment-model"></a><span data-ttu-id="4c29f-105">Resource Manager dağıtım modelini kullanarak Windows Server veya istemcisini Azure’a yedekleme</span><span class="sxs-lookup"><span data-stu-id="4c29f-105">Back up a Windows Server or client to Azure using the Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4c29f-106">Azure portal</span><span class="sxs-lookup"><span data-stu-id="4c29f-106">Azure portal</span></span>](backup-configure-vault.md)
> * [<span data-ttu-id="4c29f-107">Klasik portal</span><span class="sxs-lookup"><span data-stu-id="4c29f-107">Classic portal</span></span>](backup-configure-vault-classic.md)
>
>

<span data-ttu-id="4c29f-108">Bu makalede, Windows Server (veya Windows istemcisi) yedekleme açıklanmaktadır dosya ve klasörleri Azure Resource Manager dağıtım modelini kullanarak yedekleme ile azure'a.</span><span class="sxs-lookup"><span data-stu-id="4c29f-108">This article explains how to back up your Windows Server (or Windows client) files and folders to Azure with Azure Backup using the Resource Manager deployment model.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/backup-deployment-models.md)]

![Yedekleme işlemi adımları](./media/backup-configure-vault/initial-backup-process.png)

## <a name="before-you-start"></a><span data-ttu-id="4c29f-110">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="4c29f-110">Before you start</span></span>
<span data-ttu-id="4c29f-111">Bir sunucu veya istemci için Azure yedekleme için bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4c29f-111">To back up a server or client to Azure, you need an Azure account.</span></span> <span data-ttu-id="4c29f-112">Yoksa, oluşturabileceğiniz bir [ücretsiz bir hesap](https://azure.microsoft.com/free/) yalnızca birkaç dakika içinde.</span><span class="sxs-lookup"><span data-stu-id="4c29f-112">If you don't have one, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="4c29f-113">Kurtarma Hizmetleri kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="4c29f-113">Create a Recovery Services vault</span></span>
<span data-ttu-id="4c29f-114">Kurtarma Hizmetleri kasası tüm yedeklemeleri ve zaman içinde oluşturduğunuz kurtarma noktalarını depolayan bir varlıktır.</span><span class="sxs-lookup"><span data-stu-id="4c29f-114">A Recovery Services vault is an entity that stores all the backups and recovery points you create over time.</span></span> <span data-ttu-id="4c29f-115">Kurtarma Hizmetleri kasası, korumalı dosyalara ve klasörlere uygulanan yedekleme ilkesini de içerir.</span><span class="sxs-lookup"><span data-stu-id="4c29f-115">The Recovery Services vault also contains the backup policy applied to the protected files and folders.</span></span> <span data-ttu-id="4c29f-116">Kurtarma Hizmetleri kasası oluşturduğunuzda, aynı zamanda uygun depolama artıklığı seçeneği işaretlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4c29f-116">When you create a Recovery Services vault, you should also select the appropriate storage redundancy option.</span></span>

### <a name="to-create-a-recovery-services-vault"></a><span data-ttu-id="4c29f-117">Kurtarma Hizmetleri kasası oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="4c29f-117">To create a Recovery Services vault</span></span>
1. <span data-ttu-id="4c29f-118">Önceden yapmadıysanız Azure aboneliğinizi kullanarak [Azure Portal](https://portal.azure.com/)'da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="4c29f-118">If you haven't already done so, sign in to the [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="4c29f-119">Hub menüsünde **Diğer hizmetler**'e tıklayın ve kaynak listesinde **Kurtarma Hizmetleri** yazıp **Kurtarma Hizmetleri kasaları** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4c29f-119">On the Hub menu, click **More services** and in the list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![Kurtarma Hizmetleri Kasası oluşturma 1. adım](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="4c29f-121">Abonelikte kurtarma hizmetleri kasaları varsa kasalar listelenir.</span><span class="sxs-lookup"><span data-stu-id="4c29f-121">If there are recovery services vaults in the subscription, the vaults are listed.</span></span>

3. <span data-ttu-id="4c29f-122">**Kurtarma Hizmetleri kasaları** menüsünde **Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4c29f-122">On the **Recovery Services vaults** menu, click **Add**.</span></span>

    ![Kurtarma Hizmetleri Kasası oluşturma 2. adım](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="4c29f-124">Kurtarma Hizmetleri kasası dikey penceresi açılır ve sizden bir **Ad**, **Abonelik**, **Kaynak Grubu** ve **Konum** sağlamanızı ister.</span><span class="sxs-lookup"><span data-stu-id="4c29f-124">The Recovery Services vault blade opens, prompting you to provide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Kurtarma Hizmetleri Kasası Oluşturma 3. adım](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="4c29f-126">**Ad** alanına, kasayı tanımlayacak kolay bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="4c29f-126">For **Name**, enter a friendly name to identify the vault.</span></span> <span data-ttu-id="4c29f-127">Adın Azure aboneliği için benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4c29f-127">The name needs to be unique for the Azure subscription.</span></span> <span data-ttu-id="4c29f-128">2 ila 50 karakterden oluşan bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="4c29f-128">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="4c29f-129">Ad bir harf ile başlamalıdır ve yalnızca harf, rakam ve kısa çizgi içerebilir.</span><span class="sxs-lookup"><span data-stu-id="4c29f-129">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="4c29f-130">**Abonelik** bölümündeki açılır menüyü kullanarak Azure aboneliğini seçin.</span><span class="sxs-lookup"><span data-stu-id="4c29f-130">In the **Subscription** section, use the drop-down menu to choose the Azure subscription.</span></span> <span data-ttu-id="4c29f-131">Yalnızca bir abonelik kullanıyorsanız bu abonelik görüntülenir ve sonraki adıma atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c29f-131">If you use only one subscription, that subscription appears and you can skip to the next step.</span></span> <span data-ttu-id="4c29f-132">Hangi aboneliğin kullanılacağından emin değilseniz varsayılan (veya önerilen) aboneliği kullanın.</span><span class="sxs-lookup"><span data-stu-id="4c29f-132">If you are not sure which subscription to use, use the default (or suggested) subscription.</span></span> <span data-ttu-id="4c29f-133">Yalnızca kuruluş hesabınızın birden çok Azure aboneliği ile ilişkili olması durumunda birden çok seçenek olur.</span><span class="sxs-lookup"><span data-stu-id="4c29f-133">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="4c29f-134">**Kaynak grubu** bölümünde:</span><span class="sxs-lookup"><span data-stu-id="4c29f-134">In the **Resource group** section:</span></span>

    * <span data-ttu-id="4c29f-135">Yeni bir Kaynak grubu oluşturmak istiyorsanız **Yeni oluştur**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="4c29f-135">select **Create new** if you want to create a new Resource group.</span></span>
    <span data-ttu-id="4c29f-136">Veya</span><span class="sxs-lookup"><span data-stu-id="4c29f-136">Or</span></span>
    * <span data-ttu-id="4c29f-137">**Var olanı kullan**’ı seçin ve açılır menüyü kullanarak mevcut Kaynak gruplarının listesine bakın.</span><span class="sxs-lookup"><span data-stu-id="4c29f-137">select **Use existing** and click the drop-down menu to see the available list of Resource groups.</span></span>

  <span data-ttu-id="4c29f-138">Kaynak grupları hakkında eksiksiz bilgiler için bkz. [Azure Resource Manager’a genel bakış](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4c29f-138">For complete information on Resource groups, see the [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="4c29f-139">Kasa için coğrafi bölgeyi seçmek üzere **Konum**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4c29f-139">Click **Location** to select the geographic region for the vault.</span></span> <span data-ttu-id="4c29f-140">Bu seçim, yedekleme verilerinizin gönderildiği coğrafi bölgeyi belirler.</span><span class="sxs-lookup"><span data-stu-id="4c29f-140">This choice determines the geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="4c29f-141">Kurtarma Hizmetleri kasası dikey penceresinin alt kısmındaki **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4c29f-141">At the bottom of the Recovery Services vault blade, click **Create**.</span></span>

  <span data-ttu-id="4c29f-142">Kurtarma Hizmetleri kasasının oluşturulması birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="4c29f-142">It can take several minutes for the Recovery Services vault to be created.</span></span> <span data-ttu-id="4c29f-143">Portalın sağ üst kısmından durum bildirimlerini izleyin.</span><span class="sxs-lookup"><span data-stu-id="4c29f-143">Monitor the status notifications in the upper right-hand area of the portal.</span></span> <span data-ttu-id="4c29f-144">Kasanız oluşturulduktan sonra Kurtarma Hizmetleri kasaları listesinde görünür.</span><span class="sxs-lookup"><span data-stu-id="4c29f-144">Once your vault is created, it appears in the list of Recovery Services vaults.</span></span> <span data-ttu-id="4c29f-145">Birkaç dakika sonra kasayı görmezseniz **Yenile**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4c29f-145">If after several minutes you don't see your vault, click **Refresh**.</span></span>

  ![Yenile düğmesine tıklayın](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

  <span data-ttu-id="4c29f-147">Kasanızı Kurtarma Hizmetleri kasaları listesinde gördükten sonra, depolama yedekliliğini ayarlamaya hazır olursunuz.</span><span class="sxs-lookup"><span data-stu-id="4c29f-147">Once you see your vault in the list of Recovery Services vaults, you are ready to set the storage redundancy.</span></span>


### <a name="set-storage-redundancy"></a><span data-ttu-id="4c29f-148">Küme depolama artıklığı</span><span class="sxs-lookup"><span data-stu-id="4c29f-148">Set storage redundancy</span></span>
<span data-ttu-id="4c29f-149">Bir Kurtarma Hizmetleri kasasını ilk oluşturduğunuzda depolamanın nasıl çoğaltılacağını belirlersiniz.</span><span class="sxs-lookup"><span data-stu-id="4c29f-149">When you first create a Recovery Services vault you determine how storage is replicated.</span></span>

1. <span data-ttu-id="4c29f-150">**Kurtarma Hizmetleri kasaları** dikey penceresinden yeni kasaya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4c29f-150">From the **Recovery Services vaults** blade, click the new vault.</span></span>

    ![Kurtarma Hizmetleri kasası listesinden yeni kasayı seçin](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="4c29f-152">Kasayı seçtiğinizde **Kurtarma Hizmetleri kasası** dikey penceresi daralır ve Ayarlar dikey penceresi (*en üstünde kasanın adı bulunur*) ve ile kasa ayrıntıları dikey penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="4c29f-152">When you select the vault, the **Recovery Services vault** blade narrows, and the Settings blade (*which has the name of the vault at the top*) and the vault details blade open.</span></span>

    ![Yeni kasa için depolama yapılandırmasını görüntüleme](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)

2. <span data-ttu-id="4c29f-154">Yeni kasanın Ayarlar dikey penceresinde dikey kaydırma çubuğunu kullanarak Yönet bölümüne inin ve **Yedekleme Altyapısı**’na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4c29f-154">In the new vault's Settings blade, use the vertical slide to scroll down to the Manage section, and click **Backup Infrastructure**.</span></span>

  <span data-ttu-id="4c29f-155">Yedekleme Altyapısı dikey penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="4c29f-155">The Backup Infrastructure blade opens.</span></span>

3. <span data-ttu-id="4c29f-156">Yedekleme Altyapısı dikey penceresinde, **Yedekleme Yapılandırması**’na tıklayarak **Yedekleme Yapılandırması** dikey penceresini açın.</span><span class="sxs-lookup"><span data-stu-id="4c29f-156">In the Backup Infrastructure blade, click **Backup Configuration** to open the **Backup Configuration** blade.</span></span>

  ![Yeni kasa için depolama yapılandırması ayarlama](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)

4. <span data-ttu-id="4c29f-158">Kasanız için uygun depolama çoğaltma seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="4c29f-158">Choose the appropriate storage replication option for your vault.</span></span>

  ![depolama yapılandırması seçenekleri](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

  <span data-ttu-id="4c29f-160">Varsayılan olarak, kasanız coğrafi olarak yedekli depolamaya sahiptir.</span><span class="sxs-lookup"><span data-stu-id="4c29f-160">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="4c29f-161">Azure'ı birincil yedek depolama uç noktası olarak kullanıyorsanız, **Coğrafi olarak yedekli** seçeneğini kullanmaya devam edin.</span><span class="sxs-lookup"><span data-stu-id="4c29f-161">If you use Azure as a primary backup storage endpoint, continue to use **Geo-redundant**.</span></span> <span data-ttu-id="4c29f-162">Azure’u birincil yedek depolama uç noktası olarak kullanmıyorsanız, Azure depolama maliyetlerini azaltan **Yerel olarak yedekli** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="4c29f-162">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces the Azure storage costs.</span></span> <span data-ttu-id="4c29f-163">[Coğrafi olarak yedekli](../storage/common/storage-redundancy.md#geo-redundant-storage) ve [yerel olarak yedekli](../storage/common/storage-redundancy.md#locally-redundant-storage) depolama seçenekleri hakkında daha fazla bilgiyi [Depolama yedekliliğine genel bakış](../storage/common/storage-redundancy.md) bölümünden edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c29f-163">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="4c29f-164">Bir kasa oluşturduğunuza göre indirme ve Microsoft Azure kurtarma Hizmetleri Aracısı'nı yükleyerek, kasa kimlik bilgilerini indirme ve aracı kasaya kaydetmek için bu kimlik bilgilerini kullanarak dosyaları ve klasörleri yedeklemek için altyapınızı hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="4c29f-164">Now that you've created a vault, prepare your infrastructure to back up files and folders by downloading and installing the Microsoft Azure Recovery Services agent, downloading vault credentials, and then using those credentials to register the agent with the vault.</span></span>

## <a name="configure-the-vault"></a><span data-ttu-id="4c29f-165">Kasa yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4c29f-165">Configure the vault</span></span>

1. <span data-ttu-id="4c29f-166">Kurtarma Hizmetleri kasası dikey penceresinin (yeni oluşturduğunuz kasa için) Başlarken bölümünde **Yedekle**’ye tıklayın, ardından **Yedeklemeye Başlama** dikey penceresinde **Yedekleme hedefi**’ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4c29f-166">On the Recovery Services vault blade (for the vault you just created), in the Getting Started section, click **Backup**, then on the **Getting Started with Backup** blade, select **Backup goal**.</span></span>

  ![Yedekleme hedefi dikey penceresini açma](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

  <span data-ttu-id="4c29f-168">**Yedekleme Hedefi** dikey penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="4c29f-168">The **Backup Goal** blade opens.</span></span> <span data-ttu-id="4c29f-169">Kurtarma Hizmetleri kasası önceden yapılandırılmışsa, sonra **yedekleme hedefi** dikey pencere açılır tıkladığınızda **yedekleme** kurtarma Hizmetleri kasası dikey penceresi.</span><span class="sxs-lookup"><span data-stu-id="4c29f-169">If the Recovery Services vault has been previously configured, then the **Backup Goal** blades opens when you click **Backup** on the Recovery Services vault blade.</span></span>

  ![Yedekleme hedefi dikey penceresini açma](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="4c29f-171">**İş yükünüz nerede çalışıyor?** açılır menüsünden **Şirket içi**’ni seçin.</span><span class="sxs-lookup"><span data-stu-id="4c29f-171">From the **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

  <span data-ttu-id="4c29f-172">Windows Server veya Windows bilgisayarınız Azure üzerinde olmayan fiziksel bir makine olduğu için **Şirket içi** seçeneğini belirlersiniz.</span><span class="sxs-lookup"><span data-stu-id="4c29f-172">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="4c29f-173">**Neleri yedeklemek istiyorsunuz?** menüsünden **Dosyalar ve klasörler**'i seçin ve **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4c29f-173">From the **What do you want to backup?** menu, select **Files and folders**, and click **OK**.</span></span>

  ![Dosya ve klasörleri yedekleme](./media/backup-try-azure-backup-in-10-mins/set-file-folder.png)

  <span data-ttu-id="4c29f-175">Tamam'a tıkladıktan sonra **Yedekleme hedefi**’nin yanında bir onay işareti görünür ve **Altyapıyı hazırlama** dikey penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="4c29f-175">After clicking OK, a checkmark appears next to **Backup goal**, and the **Prepare infrastructure** blade opens.</span></span>

  ![Yedekleme hedefi yapılandırılmıştır, bundan sonra altyapıyı hazırlayın](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="4c29f-177">**Altyapıyı hazırlama** dikey penceresinde **Windows Server veya Windows İstemcisi için Aracı'yı indir** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4c29f-177">On the **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

  ![altyapıyı hazırlama](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

  <span data-ttu-id="4c29f-179">Windows Server Essential kullanıyorsanız Windows Server Essential aracısını indirmeyi seçin.</span><span class="sxs-lookup"><span data-stu-id="4c29f-179">If you are using Windows Server Essential, then choose to download the agent for Windows Server Essential.</span></span> <span data-ttu-id="4c29f-180">Açılır menü, MARSAgentInstaller.exe dosyasını çalıştırma veya kaydetme seçeneğini sunar.</span><span class="sxs-lookup"><span data-stu-id="4c29f-180">A pop-up menu prompts you to run or save MARSAgentInstaller.exe.</span></span>

  ![MARSAgentInstaller iletişim kutusu](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="4c29f-182">İndirme açılır penceresinde **Kaydet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4c29f-182">In the download pop-up menu, click **Save**.</span></span>

  <span data-ttu-id="4c29f-183">Varsayılan olarak, **MARSagentinstaller.exe** dosyası İndirilenler klasörünüze kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="4c29f-183">By default, the **MARSagentinstaller.exe** file is saved to your Downloads folder.</span></span> <span data-ttu-id="4c29f-184">Yükleyici tamamlandığında yükleyiciyi çalıştırmak veya klasörü açmak isteyip istemediğinizi soran bir açılır pencere görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="4c29f-184">When the installer completes, you will see a pop-up asking if you want to run the installer, or open the folder.</span></span>

  ![altyapıyı hazırlama](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

  <span data-ttu-id="4c29f-186">Aracıyı yüklemeniz henüz gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="4c29f-186">You don't need to install the agent yet.</span></span> <span data-ttu-id="4c29f-187">Kasa kimlik bilgilerini indirdikten sonra aracıyı yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c29f-187">You can install the agent after you have downloaded the vault credentials.</span></span>

6. <span data-ttu-id="4c29f-188">**Altyapıyı hazırlama** dikey penceresinde **İndir**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4c29f-188">On the **Prepare infrastructure** blade, click **Download**.</span></span>

  ![kasa kimlik bilgilerini indirme](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

  <span data-ttu-id="4c29f-190">Kasa kimlik bilgileri, İndirmeler klasörünüze indirilir.</span><span class="sxs-lookup"><span data-stu-id="4c29f-190">The vault credentials download to your Downloads folder.</span></span> <span data-ttu-id="4c29f-191">Kasa kimlik bilgilerini indirme tamamlandıktan sonra kimlik bilgilerini açmak veya kaydetmek isteyip istemediğinizi soran bir açılır pencere görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="4c29f-191">After the vault credentials finish downloading, you see a pop-up asking if you want to open or save the credentials.</span></span> <span data-ttu-id="4c29f-192">**Kaydet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4c29f-192">Click **Save**.</span></span> <span data-ttu-id="4c29f-193">Yanlışlıkla **Aç**’a tıklarsanız, kasa kimlik bilgilerini açmaya çalışan iletişim kutusu başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="4c29f-193">If you accidentally click **Open**, let the dialog that attempts to open the vault credentials, fail.</span></span> <span data-ttu-id="4c29f-194">Kasa kimlik bilgilerini açamazsınız.</span><span class="sxs-lookup"><span data-stu-id="4c29f-194">You cannot open the vault credentials.</span></span> <span data-ttu-id="4c29f-195">Sonraki adıma geçin.</span><span class="sxs-lookup"><span data-stu-id="4c29f-195">Proceed to the next step.</span></span> <span data-ttu-id="4c29f-196">Kasa kimlik bilgileri İndirmeler klasöründedir.</span><span class="sxs-lookup"><span data-stu-id="4c29f-196">The vault credentials are in the Downloads folder.</span></span>   

  ![kasa kimlik bilgilerini indirme tamamlandı](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-the-agent"></a><span data-ttu-id="4c29f-198">Aracıyı yükleme ve kaydetme</span><span class="sxs-lookup"><span data-stu-id="4c29f-198">Install and register the agent</span></span>

> [!NOTE]
> <span data-ttu-id="4c29f-199">Azure portal üzerinden yedeklemeyi etkinleştirme olanağı henüz mevcut değildir.</span><span class="sxs-lookup"><span data-stu-id="4c29f-199">Enabling backup through the Azure portal is not available, yet.</span></span> <span data-ttu-id="4c29f-200">Dosya ve klasörlerinizi yedeklemek üzere Microsoft Azure Kurtarma Hizmetleri Aracısı'nı kullanın.</span><span class="sxs-lookup"><span data-stu-id="4c29f-200">Use the Microsoft Azure Recovery Services Agent to back up your files and folders.</span></span>
>

1. <span data-ttu-id="4c29f-201">İndirilenler klasöründen (veya diğer kayıtlı konumdan) **MARSagentinstaller.exe** dosyasını bulun ve dosyaya çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4c29f-201">Locate and double-click the **MARSagentinstaller.exe** from the Downloads folder (or other saved location).</span></span>

  <span data-ttu-id="4c29f-202">Yükleyici, Kurtarma Hizmetleri aracısı ayıklama, yükleme ve kaydetme sırasında bir dizi ileti sunar.</span><span class="sxs-lookup"><span data-stu-id="4c29f-202">The installer provides a series of messages as it extracts, installs, and registers the Recovery Services agent.</span></span>

  ![Kurtarma Hizmetleri aracısı yükleyici kimlik bilgilerini çalıştırma](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="4c29f-204">Microsoft Azure Kurtarma Hizmetleri Aracısı Kurulum Sihirbazı'nı tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="4c29f-204">Complete the Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="4c29f-205">Sihirbazı tamamlamak için şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="4c29f-205">To complete the wizard, you need to:</span></span>

  * <span data-ttu-id="4c29f-206">Yükleme ve önbellek klasörü için bir konum seçin.</span><span class="sxs-lookup"><span data-stu-id="4c29f-206">Choose a location for the installation and cache folder.</span></span>
  * <span data-ttu-id="4c29f-207">İnternet'e bağlanmak için bir ara sunucu kullanıyorsanız ara sunucu bilgilerinizi sağlayın.</span><span class="sxs-lookup"><span data-stu-id="4c29f-207">Provide your proxy server info if you use a proxy server to connect to the internet.</span></span>
  * <span data-ttu-id="4c29f-208">Kimliği doğrulanmış bir ara sunucu kullanıyorsanız kullanıcı adı ve parola bilgilerinizi sağlayın.</span><span class="sxs-lookup"><span data-stu-id="4c29f-208">Provide your user name and password details if you use an authenticated proxy.</span></span>
  * <span data-ttu-id="4c29f-209">İndirilen kasa kimlik bilgilerini sağlayın</span><span class="sxs-lookup"><span data-stu-id="4c29f-209">Provide the downloaded vault credentials</span></span>
  * <span data-ttu-id="4c29f-210">Şifreleme parolasını güvenli bir konuma kaydedin.</span><span class="sxs-lookup"><span data-stu-id="4c29f-210">Save the encryption passphrase in a secure location.</span></span>

  > [!NOTE]
  > <span data-ttu-id="4c29f-211">Parolayı kaybeder veya unutursanız Microsoft, yedekleme verilerini kurtarmanıza yardımcı olamaz.</span><span class="sxs-lookup"><span data-stu-id="4c29f-211">If you lose or forget the passphrase, Microsoft cannot help recover the backup data.</span></span> <span data-ttu-id="4c29f-212">Dosyayı güvenli bir konuma kaydedin.</span><span class="sxs-lookup"><span data-stu-id="4c29f-212">Save the file in a secure location.</span></span> <span data-ttu-id="4c29f-213">Bu dosya, bir yedeklemeyi geri yüklemek için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="4c29f-213">It is required to restore a backup.</span></span>
  >
  >

<span data-ttu-id="4c29f-214">Aracı artık yüklenmiş ve makineniz kasaya kaydedilmiştir.</span><span class="sxs-lookup"><span data-stu-id="4c29f-214">The agent is now installed and your machine is registered to the vault.</span></span> <span data-ttu-id="4c29f-215">Yedeklemenizi yapılandırıp zamanlamak için hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="4c29f-215">You're ready to configure and schedule your backup.</span></span>

## <a name="network-and-connectivity-requirements"></a><span data-ttu-id="4c29f-216">Ağ ve Bağlantı Gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="4c29f-216">Network and Connectivity Requirements</span></span>

<span data-ttu-id="4c29f-217">Makine/proxy sınırlı Internet erişimi, güvenlik duvarı ayarlarını makine/proxy aşağıdaki URL'ler izin verecek şekilde yapılandırıldığından emin olun:</span><span class="sxs-lookup"><span data-stu-id="4c29f-217">If your machine/proxy has limited internet access, ensure that firewall settings on the machine/proxy are configured to allow the following URLs:</span></span> <br>
    1. <span data-ttu-id="4c29f-218">www.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="4c29f-218">www.msftncsi.com</span></span>
    2. <span data-ttu-id="4c29f-219">*.Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="4c29f-219">*.Microsoft.com</span></span>
    3. <span data-ttu-id="4c29f-220">*.WindowsAzure.com</span><span class="sxs-lookup"><span data-stu-id="4c29f-220">*.WindowsAzure.com</span></span>
    4. <span data-ttu-id="4c29f-221">*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="4c29f-221">*.microsoftonline.com</span></span>
    5. <span data-ttu-id="4c29f-222">*.windows.ne</span><span class="sxs-lookup"><span data-stu-id="4c29f-222">*.windows.ne</span></span>


## <a name="create-the-backup-policy"></a><span data-ttu-id="4c29f-223">Yedekleme ilkesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="4c29f-223">Create the backup policy</span></span>
<span data-ttu-id="4c29f-224">Yedekleme kurtarma noktası alınma zamanlaması ve kurtarma noktalarının bekletileceği süre ilkesidir.</span><span class="sxs-lookup"><span data-stu-id="4c29f-224">The backup policy is the schedule when recovery points are taken, and the length of time the recovery points are retained.</span></span> <span data-ttu-id="4c29f-225">Microsoft Azure Yedekleme aracısı, dosyalar ve klasörler için yedekleme ilkesi oluşturmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="4c29f-225">Use the Microsoft Azure Backup agent to create the backup policy for files and folders.</span></span>

### <a name="to-create-a-backup-schedule"></a><span data-ttu-id="4c29f-226">Bir yedekleme zamanlaması oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="4c29f-226">To create a backup schedule</span></span>
1. <span data-ttu-id="4c29f-227">Microsoft Azure yedekleme Aracısı'nı açın.</span><span class="sxs-lookup"><span data-stu-id="4c29f-227">Open the Microsoft Azure Backup agent.</span></span> <span data-ttu-id="4c29f-228">Bunu, makinenizde **Microsoft Azure Backup** aramasını yaparak bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c29f-228">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Azure Backup aracısını başlatma](./media/backup-configure-vault/snap-in-search.png)
2. <span data-ttu-id="4c29f-230">Yedekleme aracının içinde **Eylemler** bölmesinde tıklatın **yedekleme zamanlaması** yedeklemeyi Zamanlama Sihirbazı başlatmak için.</span><span class="sxs-lookup"><span data-stu-id="4c29f-230">In the Backup agent's **Actions** pane, click **Schedule Backup** to launch the Schedule Backup Wizard.</span></span>

    ![Windows Server yedeklemesini zamanlama](./media/backup-configure-vault/schedule-first-backup.png)

3. <span data-ttu-id="4c29f-232">Üzerinde **Başlarken** sayfa zamanlama Yedekleme Sihirbazı'nın tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="4c29f-232">On the **Getting started** page of the Schedule Backup Wizard, click **Next**.</span></span>
4. <span data-ttu-id="4c29f-233">Üzerinde **yedeklenecek öğeleri seçin** sayfasında, **öğeleri Ekle**.</span><span class="sxs-lookup"><span data-stu-id="4c29f-233">On the **Select Items to Backup** page, click **Add Items**.</span></span>

  <span data-ttu-id="4c29f-234">Öğeleri seçin iletişim kutusu açılır.</span><span class="sxs-lookup"><span data-stu-id="4c29f-234">The Select Items dialog opens.</span></span>

5. <span data-ttu-id="4c29f-235">Dosya ve koruyun ve ardından istediğiniz klasörleri seçin **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="4c29f-235">Select the files and folders that you want to protect, and then click **OK**.</span></span>
6. <span data-ttu-id="4c29f-236">İçinde **yedeklenecek öğeleri seçin** sayfasında, **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="4c29f-236">In the **Select Items to Backup** page, click **Next**.</span></span>
7. <span data-ttu-id="4c29f-237">Üzerinde **yedekleme zamanlamasını belirtin** sayfasında, yedekleme zamanlamasını belirtin ve tıklayın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="4c29f-237">On the **Specify Backup Schedule** page, specify the backup schedule and click **Next**.</span></span>

    <span data-ttu-id="4c29f-238">Günlük (en fazla günde üç kez olmak üzere) veya haftalık yedeklemeler zamanlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c29f-238">You can schedule daily (at a maximum rate of three times per day) or weekly backups.</span></span>

    ![Windows Server Yedekleme öğeleri](./media/backup-configure-vault/specify-backup-schedule-close.png)

   > [!NOTE]
   > <span data-ttu-id="4c29f-240">Yedekleme zamanlamasını belirtme konusunda daha fazla bilgi için [Bant altyapınızın yerini alması için Azure Windows Server Backup'ı kullanma](backup-azure-backup-cloud-as-tape.md) makalesine bakın.</span><span class="sxs-lookup"><span data-stu-id="4c29f-240">For more information about how to specify the backup schedule, see the article [Use Azure Backup to replace your tape infrastructure](backup-azure-backup-cloud-as-tape.md).</span></span>
   >
   >

8. <span data-ttu-id="4c29f-241">Üzerinde **bekletme ilkesi seçin** belirli bekletme ilkeleri sayfasında, tıklatın ve yedek kopya için **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="4c29f-241">On the **Select Retention Policy** page, choose the specific retention policies the for the backup copy and click **Next**.</span></span>

    <span data-ttu-id="4c29f-242">Bekletme İlkesi yedekleme depolanan süreyi belirtir.</span><span class="sxs-lookup"><span data-stu-id="4c29f-242">The retention policy specifies the duration which the backup is stored.</span></span> <span data-ttu-id="4c29f-243">Tüm yedekleme noktaları için bir "sabit ilke" belirtmek yerine, yedeklemenin gerçekleşme zamanını temel alan farklı bekletme ilkeleri belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c29f-243">Rather than just specifying a “flat policy” for all backup points, you can specify different retention policies based on when the backup occurs.</span></span> <span data-ttu-id="4c29f-244">Günlük, haftalık, aylık ve yıllık bekletme ilkelerini gereksinimlerinizi karşılayacak şekilde değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c29f-244">You can modify the daily, weekly, monthly, and yearly retention policies to meet your needs.</span></span>
9. <span data-ttu-id="4c29f-245">İlk Yedekleme Türünü Seçin sayfasında ilk yedekleme türünü seçin.</span><span class="sxs-lookup"><span data-stu-id="4c29f-245">On the Choose Initial Backup Type page, choose the initial backup type.</span></span> <span data-ttu-id="4c29f-246">**Ağ üzerinden otomatik olarak** seçeneğini işaretli bırakın ve ardından **İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4c29f-246">Leave the option **Automatically over the network** selected, and then click **Next**.</span></span>

    <span data-ttu-id="4c29f-247">Otomatik olarak ağ üzerinden veya çevrimdışı yedekleme yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c29f-247">You can back up automatically over the network, or you can back up offline.</span></span> <span data-ttu-id="4c29f-248">Bu makalenin sonraki bölümlerinde otomatik olarak yedekleme işlemi açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="4c29f-248">The remainder of this article describes the process for backing up automatically.</span></span> <span data-ttu-id="4c29f-249">Çevrimdışı yedekleme işlemini tercih ediyorsanız ek bilgi için [Azure Backup'ta çevrimdışı yedekleme iş akışı](backup-azure-backup-import-export.md) makalesini gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="4c29f-249">If you prefer to do an offline backup, review the article [Offline backup workflow in Azure Backup](backup-azure-backup-import-export.md) for additional information.</span></span>
10. <span data-ttu-id="4c29f-250">Onay sayfasında bilgileri gözden geçirin ve ardından **Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4c29f-250">On the Confirmation page, review the information, and then click **Finish**.</span></span>
11. <span data-ttu-id="4c29f-251">Sihirbaz yedekleme zamanlamasını oluşturduktan sonra **Kapat**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4c29f-251">After the wizard finishes creating the backup schedule, click **Close**.</span></span>

### <a name="enable-network-throttling"></a><span data-ttu-id="4c29f-252">Ağ azaltmayı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="4c29f-252">Enable network throttling</span></span>
<span data-ttu-id="4c29f-253">Microsoft Azure Yedekleme aracısı, ağ azaltma sağlar.</span><span class="sxs-lookup"><span data-stu-id="4c29f-253">The Microsoft Azure Backup agent provides network throttling.</span></span> <span data-ttu-id="4c29f-254">Veri aktarımı sırasında ağ bant genişliğinin nasıl kullanıldığını denetimleri azaltma.</span><span class="sxs-lookup"><span data-stu-id="4c29f-254">Throttling controls how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="4c29f-255">Bu denetim sırasında verilerin yedeklemeniz gerekiyorsa, çalışma saatleri ancak Yedekleme işleminin diğer Internet trafiğine engel olmasını istiyor musunuz yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="4c29f-255">This control can be helpful if you need to back up data during work hours but do not want the backup process to interfere with other Internet traffic.</span></span> <span data-ttu-id="4c29f-256">Azaltma yedeklemek ve geri yükleme etkinlikleri için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="4c29f-256">Throttling applies to back up and restore activities.</span></span>

> [!NOTE]
> <span data-ttu-id="4c29f-257">Ağ azaltma (hizmet paketleri ile) Windows Server 2008 R2 SP1, Windows Server 2008 SP2 veya Windows 7 üzerinde kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="4c29f-257">Network throttling is not available on Windows Server 2008 R2 SP1, Windows Server 2008 SP2, or Windows 7 (with service packs).</span></span> <span data-ttu-id="4c29f-258">Özellik azaltma Azure Backup ağ hizmet kalitesi (QoS) yerel işletim sisteminde ilgilenir.</span><span class="sxs-lookup"><span data-stu-id="4c29f-258">The Azure Backup network throttling feature engages Quality of Service (QoS) on the local operating system.</span></span> <span data-ttu-id="4c29f-259">Azure Backup bu işletim sistemlerini korumak için de, QoS bu platformlarda kullanılabilir sürümü Azure Backup ağ azaltma ile çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="4c29f-259">Though Azure Backup can protect these operating systems, the version of QoS available on these platforms doesn't work with Azure Backup network throttling.</span></span> <span data-ttu-id="4c29f-260">Ağ azaltma kullanılabilir tüm diğer bağlı [desteklenen işletim sistemleri](backup-azure-backup-faq.md).</span><span class="sxs-lookup"><span data-stu-id="4c29f-260">Network throttling can be used on all other [supported operating systems](backup-azure-backup-faq.md).</span></span>
>
>

<span data-ttu-id="4c29f-261">**Ağ azaltma etkinleştirmek için**</span><span class="sxs-lookup"><span data-stu-id="4c29f-261">**To enable network throttling**</span></span>

1. <span data-ttu-id="4c29f-262">Microsoft Azure Yedekleme aracısı, tıklatın **özelliklerini değiştirme**.</span><span class="sxs-lookup"><span data-stu-id="4c29f-262">In the Microsoft Azure Backup agent, click **Change Properties**.</span></span>

    ![Özelliklerini değiştir](./media/backup-configure-vault/change-properties.png)
2. <span data-ttu-id="4c29f-264">Üzerinde **azaltma** sekmesine **yedekleme işlemleri için Internet bant genişliği kullanımı daraltmayı etkinleştir** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="4c29f-264">On the **Throttling** tab, select the **Enable internet bandwidth usage throttling for backup operations** check box.</span></span>

    ![Ağ azaltma](./media/backup-configure-vault/throttling-dialog.png)
3. <span data-ttu-id="4c29f-266">Azaltma etkinleştirdikten sonra sırasında yedek veri aktarımı için izin verilen bant genişliğini belirtin **çalışma saatleri** ve **çalışılmayan saatler**.</span><span class="sxs-lookup"><span data-stu-id="4c29f-266">After you have enabled throttling, specify the allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="4c29f-267">Bant genişliği değerler 512 kilobit / saniye (Kbps) başlar ve 1,023 megabayt (MBps) saniyede gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c29f-267">The bandwidth values begin at 512 kilobits per second (Kbps) and can go up to 1,023 megabytes per second (MBps).</span></span> <span data-ttu-id="4c29f-268">Ayrıca başlangıç belirleyin ve için son **çalışma saatleri**, ve haftanın hangi günleri dikkate alınan iş günlerini.</span><span class="sxs-lookup"><span data-stu-id="4c29f-268">You can also designate the start and finish for **Work hours**, and which days of the week are considered work days.</span></span> <span data-ttu-id="4c29f-269">Belirtilen iş saatleri kabul dışında saat saat İş dışı.</span><span class="sxs-lookup"><span data-stu-id="4c29f-269">Hours outside of designated work hours are considered non-work hours.</span></span>
4. <span data-ttu-id="4c29f-270">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4c29f-270">Click **OK**.</span></span>

### <a name="to-back-up-files-and-folders-for-the-first-time"></a><span data-ttu-id="4c29f-271">Dosya ve klasörleri ilk kez yedeklemek için</span><span class="sxs-lookup"><span data-stu-id="4c29f-271">To back up files and folders for the first time</span></span>
1. <span data-ttu-id="4c29f-272">Yedekleme aracı tıklatın **Şimdi Yedekle** ağ üzerinden ilk doldurma işlemini tamamlamak için.</span><span class="sxs-lookup"><span data-stu-id="4c29f-272">In the backup agent, click **Back Up Now** to complete the initial seeding over the network.</span></span>

    ![Windows Server şimdi yedekle](./media/backup-configure-vault/backup-now.png)
2. <span data-ttu-id="4c29f-274">Onay sayfasında, Şimdi Yedekle Sihirbazı'nın makineyi yedeklemek için kullanacağı ayarları gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="4c29f-274">On the Confirmation page, review the settings that the Back Up Now Wizard will use to back up the machine.</span></span> <span data-ttu-id="4c29f-275">Ardından **Yedekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4c29f-275">Then click **Back Up**.</span></span>
3. <span data-ttu-id="4c29f-276">Sihirbazı kapatmak için **Kapat**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4c29f-276">Click **Close** to close the wizard.</span></span> <span data-ttu-id="4c29f-277">Bunu yedekleme işlemi tamamlanmadan önce yaparsanız sihirbaz arka planda çalışmaya devam eder.</span><span class="sxs-lookup"><span data-stu-id="4c29f-277">If you do this before the backup process finishes, the wizard continues to run in the background.</span></span>

<span data-ttu-id="4c29f-278">İlk yedekleme tamamlandıktan sonra, Yedekleme konsolunda **İş tamamlandı** durumu görünür.</span><span class="sxs-lookup"><span data-stu-id="4c29f-278">After the initial backup is completed, the **Job completed** status appears in the Backup console.</span></span>

![IR tamamlandı](./media/backup-configure-vault/ircomplete.png)

## <a name="questions"></a><span data-ttu-id="4c29f-280">Sorularınız mı var?</span><span class="sxs-lookup"><span data-stu-id="4c29f-280">Questions?</span></span>
<span data-ttu-id="4c29f-281">Sorularınız varsa veya dahil edilmesini istediğiniz herhangi bir özellik varsa [bize geri bildirim gönderin](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="4c29f-281">If you have questions, or if there is any feature that you would like to see included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4c29f-282">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4c29f-282">Next steps</span></span>
<span data-ttu-id="4c29f-283">Sanal makineler veya diğer iş yüklerini yedekleme hakkında ek bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="4c29f-283">For additional information about backing up VMs or other workloads, see:</span></span>

* <span data-ttu-id="4c29f-284">Dosya ve klasörlerinizi yedeklediğinize göre artık [kasa ve sunucularınızı yönetebilirsiniz](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="4c29f-284">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="4c29f-285">Bir yedeklemeyi geri yüklemeniz gerekirse [dosyaları bir Windows makinesine geri yüklemek](backup-azure-restore-windows-server.md) için bu makaleyi kullanın.</span><span class="sxs-lookup"><span data-stu-id="4c29f-285">If you need to restore a backup, use this article to [restore files to a Windows machine](backup-azure-restore-windows-server.md).</span></span>
