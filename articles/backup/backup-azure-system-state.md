---
title: "Azure için Windows sistem durumu yedekleme | Microsoft Docs"
description: "Sistem durumunu Windows Server ve/veya Windows bilgisayarları için Azure yedekleme öğrenin."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: carmonm
editor: 
keywords: "yedekleme nasıl yapılır; yedekleme; dosya ve klasör yedekleme"
ms.assetid: 5b15ebf1-2214-4722-b937-96e2be8872bb
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: saurse;markgal
ms.openlocfilehash: 6fbd96935f444d8b0c6d068ebd0d28e612f19816
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="back-up-windows-system-state-in-resource-manager-deployment"></a><span data-ttu-id="a6ba4-104">Resource Manager dağıtım Windows sistem durumu yedekleme</span><span class="sxs-lookup"><span data-stu-id="a6ba4-104">Back up Windows system state in Resource Manager deployment</span></span>
<span data-ttu-id="a6ba4-105">Bu makalede, Azure için Windows Server sistem durumunu yedekleme açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-105">This article explains how to back up your Windows Server system state to Azure.</span></span> <span data-ttu-id="a6ba4-106">Bu, size temel işlemler boyunca yol göstermeye yönelik bir öğreticidir.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-106">It's a tutorial intended to walk you through the basics.</span></span>

<span data-ttu-id="a6ba4-107">Azure Backup hakkında daha fazla bilgi edinmek istiyorsanız bu [genel bakışı](backup-introduction-to-azure-backup.md) okuyun.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-107">If you want to know more about Azure Backup, read this [overview](backup-introduction-to-azure-backup.md).</span></span>

<span data-ttu-id="a6ba4-108">Azure aboneliğiniz yoksa istediğiniz Azure hizmetine erişmenizi sağlayan [ücretsiz bir hesap](https://azure.microsoft.com/free/) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) that lets you access any Azure service.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="a6ba4-109">Kurtarma hizmetleri kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="a6ba4-109">Create a recovery services vault</span></span>
<span data-ttu-id="a6ba4-110">Dosya ve klasörlerinizi yedeklemek için, verileri depolamak istediğiniz bölgede bir Kurtarma Hizmetleri kasası oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-110">To back up your files and folders, you need to create a Recovery Services vault in the region where you want to store the data.</span></span> <span data-ttu-id="a6ba4-111">Ayrıca, depolama alanınızın nasıl çoğaltılmasını istediğinizi belirlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-111">You also need to determine how you want your storage replicated.</span></span>

### <a name="to-create-a-recovery-services-vault"></a><span data-ttu-id="a6ba4-112">Kurtarma Hizmetleri kasası oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="a6ba4-112">To create a Recovery Services vault</span></span>
1. <span data-ttu-id="a6ba4-113">Önceden yapmadıysanız Azure aboneliğinizi kullanarak [Azure Portal](https://portal.azure.com/)'da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-113">If you haven't already done so, sign in to the [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="a6ba4-114">Hub menüsünde **Diğer hizmetler**'e tıklayın ve kaynak listesinde **Kurtarma Hizmetleri** yazıp **Kurtarma Hizmetleri kasaları** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-114">On the Hub menu, click **More services** and in the list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![Kurtarma Hizmetleri Kasası oluşturma 1. adım](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="a6ba4-116">Abonelikte kurtarma hizmetleri kasaları varsa kasalar listelenir.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-116">If there are recovery services vaults in the subscription, the vaults are listed.</span></span>
3. <span data-ttu-id="a6ba4-117">**Kurtarma Hizmetleri kasaları** menüsünde **Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-117">On the **Recovery Services vaults** menu, click **Add**.</span></span>

    ![Kurtarma Hizmetleri Kasası oluşturma 2. adım](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="a6ba4-119">Kurtarma Hizmetleri kasası dikey penceresi açılır ve sizden bir **Ad**, **Abonelik**, **Kaynak Grubu** ve **Konum** sağlamanızı ister.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-119">The Recovery Services vault blade opens, prompting you to provide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Kurtarma Hizmetleri Kasası Oluşturma 3. adım](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="a6ba4-121">**Ad** alanına, kasayı tanımlayacak kolay bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-121">For **Name**, enter a friendly name to identify the vault.</span></span> <span data-ttu-id="a6ba4-122">Adın Azure aboneliği için benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-122">The name needs to be unique for the Azure subscription.</span></span> <span data-ttu-id="a6ba4-123">2 ila 50 karakterden oluşan bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-123">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="a6ba4-124">Ad bir harf ile başlamalıdır ve yalnızca harf, rakam ve kısa çizgi içerebilir.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-124">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="a6ba4-125">**Abonelik** bölümündeki açılır menüyü kullanarak Azure aboneliğini seçin.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-125">In the **Subscription** section, use the drop-down menu to choose the Azure subscription.</span></span> <span data-ttu-id="a6ba4-126">Yalnızca bir abonelik kullanıyorsanız bu abonelik görüntülenir ve sonraki adıma atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-126">If you use only one subscription, that subscription appears and you can skip to the next step.</span></span> <span data-ttu-id="a6ba4-127">Hangi aboneliğin kullanılacağından emin değilseniz varsayılan (veya önerilen) aboneliği kullanın.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-127">If you are not sure which subscription to use, use the default (or suggested) subscription.</span></span> <span data-ttu-id="a6ba4-128">Yalnızca kuruluş hesabınızın birden çok Azure aboneliği ile ilişkili olması durumunda birden çok seçenek olur.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-128">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="a6ba4-129">**Kaynak grubu** bölümünde:</span><span class="sxs-lookup"><span data-stu-id="a6ba4-129">In the **Resource group** section:</span></span>

    * <span data-ttu-id="a6ba4-130">bir Kaynak grubu oluşturmak istiyorsanız, **Yeni oluştur**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-130">select **Create new** if you want to create a Resource group.</span></span>
    <span data-ttu-id="a6ba4-131">Veya</span><span class="sxs-lookup"><span data-stu-id="a6ba4-131">Or</span></span>
    * <span data-ttu-id="a6ba4-132">**Var olanı kullan**’ı seçin ve açılır menüyü kullanarak mevcut Kaynak gruplarının listesine bakın.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-132">select **Use existing** and click the drop-down menu to see the available list of Resource groups.</span></span>

  <span data-ttu-id="a6ba4-133">Kaynak grupları hakkında eksiksiz bilgiler için bkz. [Azure Resource Manager’a genel bakış](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a6ba4-133">For complete information on Resource groups, see the [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="a6ba4-134">Kasa için coğrafi bölgeyi seçmek üzere **Konum**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-134">Click **Location** to select the geographic region for the vault.</span></span> <span data-ttu-id="a6ba4-135">Bu seçim, yedekleme verilerinizin gönderildiği coğrafi bölgeyi belirler.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-135">This choice determines the geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="a6ba4-136">Kurtarma Hizmetleri kasası dikey penceresinin alt kısmındaki **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-136">At the bottom of the Recovery Services vault blade, click **Create**.</span></span>

    <span data-ttu-id="a6ba4-137">Kurtarma Hizmetleri kasasının oluşturulması birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-137">It can take several minutes for the Recovery Services vault to be created.</span></span> <span data-ttu-id="a6ba4-138">Portalın sağ üst kısmından durum bildirimlerini izleyin.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-138">Monitor the status notifications in the upper right-hand area of the portal.</span></span> <span data-ttu-id="a6ba4-139">Kasanız oluşturulduktan sonra Kurtarma Hizmetleri kasaları listesinde görünür.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-139">Once your vault is created, it appears in the list of Recovery Services vaults.</span></span> <span data-ttu-id="a6ba4-140">Birkaç dakika sonra kasayı görmezseniz **Yenile**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-140">If after several minutes you don't see your vault, click **Refresh**.</span></span>

    ![Yenile düğmesine tıklayın](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    <span data-ttu-id="a6ba4-142">Kasanızı Kurtarma Hizmetleri kasaları listesinde gördükten sonra, depolama yedekliliğini ayarlamaya hazır olursunuz.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-142">Once you see your vault in the list of Recovery Services vaults, you are ready to set the storage redundancy.</span></span>

### <a name="set-storage-redundancy-for-the-vault"></a><span data-ttu-id="a6ba4-143">Kasa için depolama artıklığı ayarlama</span><span class="sxs-lookup"><span data-stu-id="a6ba4-143">Set storage redundancy for the vault</span></span>
<span data-ttu-id="a6ba4-144">Kurtarma Hizmetleri kasası oluşturduğunuzda, depolama yedekliliğinin istediğiniz şekilde yapılandırıldığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-144">When you create a Recovery Services vault, make sure storage redundancy is configured the way you want.</span></span>

1. <span data-ttu-id="a6ba4-145">**Kurtarma Hizmetleri kasaları** dikey penceresinden yeni kasaya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-145">From the **Recovery Services vaults** blade, click the new vault.</span></span>

    ![Kurtarma Hizmetleri kasası listesinden yeni kasayı seçin](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="a6ba4-147">Kasayı seçtiğinizde **Kurtarma Hizmetleri kasası** dikey penceresi daralır ve Ayarlar dikey penceresi (*en üstünde kasanın adı bulunur*) ve ile kasa ayrıntıları dikey penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-147">When you select the vault, the **Recovery Services vault** blade narrows, and the Settings blade (*which has the name of the vault at the top*) and the vault details blade open.</span></span>

    ![Yeni kasa için depolama yapılandırmasını görüntüleme](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)
2. <span data-ttu-id="a6ba4-149">Yeni kasanın Ayarlar dikey penceresinde dikey kaydırma çubuğunu kullanarak Yönet bölümüne inin ve **Yedekleme Altyapısı**’na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-149">In the new vault's Settings blade, use the vertical slide to scroll down to the Manage section, and click **Backup Infrastructure**.</span></span>
    <span data-ttu-id="a6ba4-150">Yedekleme Altyapısı dikey penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-150">The Backup Infrastructure blade opens.</span></span>
3. <span data-ttu-id="a6ba4-151">Yedekleme Altyapısı dikey penceresinde, **Yedekleme Yapılandırması**’na tıklayarak **Yedekleme Yapılandırması** dikey penceresini açın.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-151">In the Backup Infrastructure blade, click **Backup Configuration** to open the **Backup Configuration** blade.</span></span>

    ![Yeni kasa için depolama yapılandırması ayarlama](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. <span data-ttu-id="a6ba4-153">Kasanız için uygun depolama çoğaltma seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-153">Choose the appropriate storage replication option for your vault.</span></span>

    ![depolama yapılandırması seçenekleri](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    <span data-ttu-id="a6ba4-155">Varsayılan olarak, kasanız coğrafi olarak yedekli depolamaya sahiptir.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-155">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="a6ba4-156">Azure'ı birincil yedek depolama uç noktası olarak kullanıyorsanız, **Coğrafi olarak yedekli** seçeneğini kullanmaya devam edin.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-156">If you use Azure as a primary backup storage endpoint, continue to use **Geo-redundant**.</span></span> <span data-ttu-id="a6ba4-157">Azure’u birincil yedek depolama uç noktası olarak kullanmıyorsanız, Azure depolama maliyetlerini azaltan **Yerel olarak yedekli** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-157">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces the Azure storage costs.</span></span> <span data-ttu-id="a6ba4-158">[Coğrafi olarak yedekli](../storage/common/storage-redundancy.md#geo-redundant-storage) ve [yerel olarak yedekli](../storage/common/storage-redundancy.md#locally-redundant-storage) depolama seçenekleri hakkında daha fazla bilgiyi [Depolama yedekliliğine genel bakış](../storage/common/storage-redundancy.md) bölümünden edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-158">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="a6ba4-159">Bir kasa oluşturduğunuza göre Windows sistem durumunu yedekleme için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-159">Now that you've created a vault, configure it for backing up Windows System State.</span></span>

## <a name="configure-the-vault"></a><span data-ttu-id="a6ba4-160">Kasa yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a6ba4-160">Configure the vault</span></span>
1. <span data-ttu-id="a6ba4-161">Kurtarma Hizmetleri kasası dikey penceresinin (yeni oluşturduğunuz kasa için) Başlarken bölümünde **Yedekle**’ye tıklayın, ardından **Yedeklemeye Başlama** dikey penceresinde **Yedekleme hedefi**’ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-161">On the Recovery Services vault blade (for the vault you just created), in the Getting Started section, click **Backup**, then on the **Getting Started with Backup** blade, select **Backup goal**.</span></span>

    ![Yedekleme hedefi dikey penceresini açma](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

    <span data-ttu-id="a6ba4-163">**Yedekleme Hedefi** dikey penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-163">The **Backup Goal** blade opens.</span></span>

    ![Yedekleme hedefi dikey penceresini açma](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="a6ba4-165">**İş yükünüz nerede çalışıyor?** açılır menüsünden **Şirket içi**’ni seçin.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-165">From the **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

    <span data-ttu-id="a6ba4-166">Windows Server veya Windows bilgisayarınız Azure üzerinde olmayan fiziksel bir makine olduğu için **Şirket içi** seçeneğini belirlersiniz.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-166">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="a6ba4-167">Gelen **neleri yedeklemek istiyorsunuz?** menüsünde seçin **sistem durumu**, tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-167">From the **What do you want to backup?** menu, select **System State**, and click **OK**.</span></span>

    ![Dosya ve klasörleri yedekleme](./media/backup-azure-system-state/backup-goal-system-state.png)

    <span data-ttu-id="a6ba4-169">Tamam'a tıkladıktan sonra **Yedekleme hedefi**’nin yanında bir onay işareti görünür ve **Altyapıyı hazırlama** dikey penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-169">After clicking OK, a checkmark appears next to **Backup goal**, and the **Prepare infrastructure** blade opens.</span></span>

    ![Yedekleme hedefi yapılandırılmıştır, bundan sonra altyapıyı hazırlayın](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="a6ba4-171">**Altyapıyı hazırlama** dikey penceresinde **Windows Server veya Windows İstemcisi için Aracı'yı indir** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-171">On the **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

    ![altyapıyı hazırlama](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

    <span data-ttu-id="a6ba4-173">Windows Server Essential kullanıyorsanız Windows Server Essential aracısını indirmeyi seçin.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-173">If you are using Windows Server Essential, then choose to download the agent for Windows Server Essential.</span></span> <span data-ttu-id="a6ba4-174">Açılır menü, MARSAgentInstaller.exe dosyasını çalıştırma veya kaydetme seçeneğini sunar.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-174">A pop-up menu prompts you to run or save MARSAgentInstaller.exe.</span></span>

    ![MARSAgentInstaller iletişim kutusu](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="a6ba4-176">İndirme açılır penceresinde **Kaydet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-176">In the download pop-up menu, click **Save**.</span></span>

    <span data-ttu-id="a6ba4-177">Varsayılan olarak, **MARSagentinstaller.exe** dosyası İndirilenler klasörünüze kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-177">By default, the **MARSagentinstaller.exe** file is saved to your Downloads folder.</span></span> <span data-ttu-id="a6ba4-178">Yükleyici tamamlandığında yükleyiciyi çalıştırmak veya klasörü açmak isteyip istemediğinizi soran bir açılır pencere görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-178">When the installer completes, you will see a pop-up asking if you want to run the installer, or open the folder.</span></span>

    ![altyapıyı hazırlama](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

    <span data-ttu-id="a6ba4-180">Aracıyı yüklemeniz henüz gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-180">You don't need to install the agent yet.</span></span> <span data-ttu-id="a6ba4-181">Kasa kimlik bilgilerini indirdikten sonra aracıyı yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-181">You can install the agent after you have downloaded the vault credentials.</span></span>

6. <span data-ttu-id="a6ba4-182">**Altyapıyı hazırlama** dikey penceresinde **İndir**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-182">On the **Prepare infrastructure** blade, click **Download**.</span></span>

    ![kasa kimlik bilgilerini indirme](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

    <span data-ttu-id="a6ba4-184">Kasa kimlik bilgileri, İndirmeler klasörünüze indirilir.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-184">The vault credentials download to your Downloads folder.</span></span> <span data-ttu-id="a6ba4-185">Kasa kimlik bilgilerini indirme tamamlandıktan sonra kimlik bilgilerini açmak veya kaydetmek isteyip istemediğinizi soran bir açılır pencere görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-185">After the vault credentials finish downloading, you see a pop-up asking if you want to open or save the credentials.</span></span> <span data-ttu-id="a6ba4-186">**Kaydet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-186">Click **Save**.</span></span> <span data-ttu-id="a6ba4-187">Yanlışlıkla **Aç**’a tıklarsanız, kasa kimlik bilgilerini açmaya çalışan iletişim kutusu başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-187">If you accidentally click **Open**, let the dialog that attempts to open the vault credentials, fail.</span></span> <span data-ttu-id="a6ba4-188">Kasa kimlik bilgilerini açamazsınız.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-188">You cannot open the vault credentials.</span></span> <span data-ttu-id="a6ba4-189">Sonraki adıma geçin.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-189">Proceed to the next step.</span></span> <span data-ttu-id="a6ba4-190">Kasa kimlik bilgileri İndirmeler klasöründedir.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-190">The vault credentials are in the Downloads folder.</span></span>   

    ![kasa kimlik bilgilerini indirme tamamlandı](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-the-agent"></a><span data-ttu-id="a6ba4-192">Aracıyı yükleme ve kaydetme</span><span class="sxs-lookup"><span data-stu-id="a6ba4-192">Install and register the agent</span></span>

> [!NOTE]
> <span data-ttu-id="a6ba4-193">Azure portal üzerinden yedeklemeyi etkinleştirme olanağı henüz mevcut değildir.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-193">Enabling backup through the Azure portal is not available, yet.</span></span> <span data-ttu-id="a6ba4-194">Microsoft Azure kurtarma Hizmetleri Aracısı, Windows Server sistem durumunu yedeklemek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-194">Use the Microsoft Azure Recovery Services Agent to back up Windows Server System State.</span></span>
>

1. <span data-ttu-id="a6ba4-195">İndirilenler klasöründen (veya diğer kayıtlı konumdan) **MARSagentinstaller.exe** dosyasını bulun ve dosyaya çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-195">Locate and double-click the **MARSagentinstaller.exe** from the Downloads folder (or other saved location).</span></span>

    <span data-ttu-id="a6ba4-196">Yükleyici, Kurtarma Hizmetleri aracısı ayıklama, yükleme ve kaydetme sırasında bir dizi ileti sunar.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-196">The installer provides a series of messages as it extracts, installs, and registers the Recovery Services agent.</span></span>

    ![Kurtarma Hizmetleri aracısı yükleyici kimlik bilgilerini çalıştırma](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="a6ba4-198">Microsoft Azure Kurtarma Hizmetleri Aracısı Kurulum Sihirbazı'nı tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-198">Complete the Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="a6ba4-199">Sihirbazı tamamlamak için şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="a6ba4-199">To complete the wizard, you need to:</span></span>

   * <span data-ttu-id="a6ba4-200">Yükleme ve önbellek klasörü için bir konum seçin.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-200">Choose a location for the installation and cache folder.</span></span>
   * <span data-ttu-id="a6ba4-201">İnternet'e bağlanmak için bir ara sunucu kullanıyorsanız ara sunucu bilgilerinizi sağlayın.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-201">Provide your proxy server info if you use a proxy server to connect to the internet.</span></span>
   * <span data-ttu-id="a6ba4-202">Kimliği doğrulanmış bir ara sunucu kullanıyorsanız kullanıcı adı ve parola bilgilerinizi sağlayın.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-202">Provide your user name and password details if you use an authenticated proxy.</span></span>
   * <span data-ttu-id="a6ba4-203">İndirilen kasa kimlik bilgilerini sağlayın</span><span class="sxs-lookup"><span data-stu-id="a6ba4-203">Provide the downloaded vault credentials</span></span>
   * <span data-ttu-id="a6ba4-204">Şifreleme parolasını güvenli bir konuma kaydedin.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-204">Save the encryption passphrase in a secure location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="a6ba4-205">Parolayı kaybeder veya unutursanız Microsoft, yedekleme verilerini kurtarmanıza yardımcı olamaz.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-205">If you lose or forget the passphrase, Microsoft cannot help recover the backup data.</span></span> <span data-ttu-id="a6ba4-206">Dosyayı güvenli bir konuma kaydedin.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-206">Save the file in a secure location.</span></span> <span data-ttu-id="a6ba4-207">Bu dosya, bir yedeklemeyi geri yüklemek için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-207">It is required to restore a backup.</span></span>
     >
     >

<span data-ttu-id="a6ba4-208">Aracı artık yüklenmiş ve makineniz kasaya kaydedilmiştir.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-208">The agent is now installed and your machine is registered to the vault.</span></span> <span data-ttu-id="a6ba4-209">Yedeklemenizi yapılandırıp zamanlamak için hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-209">You're ready to configure and schedule your backup.</span></span>

## <a name="back-up-windows-server-system-state-preview"></a><span data-ttu-id="a6ba4-210">Windows Server sistem durumunu (Önizleme) yedekleme</span><span class="sxs-lookup"><span data-stu-id="a6ba4-210">Back up Windows Server System State (Preview)</span></span>
<span data-ttu-id="a6ba4-211">İlk yedekleme üç görevleri içerir:</span><span class="sxs-lookup"><span data-stu-id="a6ba4-211">The initial backup includes three tasks:</span></span>

* <span data-ttu-id="a6ba4-212">Azure Backup aracısını kullanarak sistem durumu yedeklemesi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="a6ba4-212">Enable System State Backup using the Azure Backup agent</span></span>
* <span data-ttu-id="a6ba4-213">Yedeklemeyi zamanlama</span><span class="sxs-lookup"><span data-stu-id="a6ba4-213">Schedule the backup</span></span>
* <span data-ttu-id="a6ba4-214">Dosya ve klasörleri ilk kez yedekleme</span><span class="sxs-lookup"><span data-stu-id="a6ba4-214">Back up files and folders for the first time</span></span>

<span data-ttu-id="a6ba4-215">İlk yedeklemeyi tamamlamak için Microsoft Azure Kurtarma Hizmetleri aracısını kullanın.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-215">To complete the initial backup, use the Microsoft Azure Recovery Services agent.</span></span>

### <a name="to-enable-system-state-backup-using-the-azure-backup-agent"></a><span data-ttu-id="a6ba4-216">Azure Backup Aracısı kullanılarak sistem durumu yedeklemesi etkinleştirmek için</span><span class="sxs-lookup"><span data-stu-id="a6ba4-216">To enable System State backup using the Azure Backup agent</span></span>

1. <span data-ttu-id="a6ba4-217">Bir PowerShell oturumunda Azure Backup altyapısını durdurmak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-217">In a PowerShell session, run the following command to stop the Azure Backup engine.</span></span>

  ```
  PS C:\> Net stop obengine
  ```

2. <span data-ttu-id="a6ba4-218">Windows kayıt defterini açın.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-218">Open the Windows Registry.</span></span>

  ```
  PS C:\> regedit.exe
  ```

3. <span data-ttu-id="a6ba4-219">Aşağıdaki kayıt defteri anahtarı ile belirtilen DWord değerini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-219">Add the following registry key with the specified DWord Value.</span></span>

  | <span data-ttu-id="a6ba4-220">Kayıt defteri yolu</span><span class="sxs-lookup"><span data-stu-id="a6ba4-220">Registry path</span></span> | <span data-ttu-id="a6ba4-221">Kayıt defteri anahtarı</span><span class="sxs-lookup"><span data-stu-id="a6ba4-221">Registry key</span></span> | <span data-ttu-id="a6ba4-222">DWord değeri</span><span class="sxs-lookup"><span data-stu-id="a6ba4-222">DWord value</span></span> |
  |---------------|--------------|-------------|
  | <span data-ttu-id="a6ba4-223">HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span><span class="sxs-lookup"><span data-stu-id="a6ba4-223">HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span></span> | <span data-ttu-id="a6ba4-224">TurnOffSSBFeature</span><span class="sxs-lookup"><span data-stu-id="a6ba4-224">TurnOffSSBFeature</span></span> | <span data-ttu-id="a6ba4-225">2</span><span class="sxs-lookup"><span data-stu-id="a6ba4-225">2</span></span> |

4. <span data-ttu-id="a6ba4-226">Yükseltilmiş bir komut isteminde aşağıdaki komutu çalıştırarak Backup altyapısını yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-226">Restart the Backup engine by executing the following command in an elevated command prompt.</span></span>

  ```
  PS C:\> Net start obengine
  ```

### <a name="to-schedule-the-backup-job"></a><span data-ttu-id="a6ba4-227">Yedekleme işini zamanlamak için</span><span class="sxs-lookup"><span data-stu-id="a6ba4-227">To schedule the backup job</span></span>

1. <span data-ttu-id="a6ba4-228">Microsoft Azure Kurtarma Hizmetleri aracısını açın.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-228">Open the Microsoft Azure Recovery Services agent.</span></span> <span data-ttu-id="a6ba4-229">Bunu, makinenizde **Microsoft Azure Backup** aramasını yaparak bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-229">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Azure Kurtarma Hizmetleri aracısını başlatma](./media/backup-try-azure-backup-in-10-mins/snap-in-search.png)

2. <span data-ttu-id="a6ba4-231">Kurtarma Hizmetleri aracısında, **Yedeklemeyi Zamanla**'ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-231">In the Recovery Services agent, click **Schedule Backup**.</span></span>

    ![Windows Server yedeklemesini zamanlama](./media/backup-try-azure-backup-in-10-mins/schedule-first-backup.png)

3. <span data-ttu-id="a6ba4-233">Yedeklemeyi Zamanlama Sihirbazı'nın Başlarken sayfasında **İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-233">On the Getting started page of the Schedule Backup Wizard, click **Next**.</span></span>

4. <span data-ttu-id="a6ba4-234">Yedeklenecek Öğeleri Seçin sayfasında **Öğe Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-234">On the Select Items to Backup page, click **Add Items**.</span></span>

5. <span data-ttu-id="a6ba4-235">Seçin **sistem durumu** ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-235">Select **System State** and then click **OK**.</span></span>

6. <span data-ttu-id="a6ba4-236">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-236">Click **Next**.</span></span>

7. <span data-ttu-id="a6ba4-237">Sistem Durumu yedekleme ve bekletme zamanlaması her Pazar 9:00 PM yerel zaman yedeklemek için otomatik olarak ayarlanır ve bekletme süresini 60 gün olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-237">The System State Backup and Retention schedule is automatically set to back up every Sunday at 9:00 PM local time, and the retention period is set to 60 days.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a6ba4-238">Sistem Durumu yedekleme ve bekletme ilkesi otomatik olarak yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-238">System State backup and retention policy is automatically configured.</span></span> <span data-ttu-id="a6ba4-239">Dosya ve klasörleri ek olarak Windows Server sistem durumu yedekleme yapıyorsanız, yalnızca yedekleme ve Bekletme İlkesi Sihirbazı'ndan dosyası yedeklerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-239">If you back up Files and Folders in addition to the Windows Server System State, specify only the Backup and Retention policy for file backups from the wizard.</span></span> 
   >

8. <span data-ttu-id="a6ba4-240">Onay sayfasında bilgileri gözden geçirin ve ardından **Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-240">On the Confirmation page, review the information, and then click **Finish**.</span></span>

9. <span data-ttu-id="a6ba4-241">Sihirbaz yedekleme zamanlamasını oluşturduktan sonra **Kapat**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-241">After the wizard finishes creating the backup schedule, click **Close**.</span></span>

### <a name="to-back-up-windows-server-system-state-for-the-first-time"></a><span data-ttu-id="a6ba4-242">İlk kez Windows Server sistem durumunu yedekleme</span><span class="sxs-lookup"><span data-stu-id="a6ba4-242">To back up Windows Server System State for the first time</span></span>

1. <span data-ttu-id="a6ba4-243">Windows Server için bir yeniden başlatma gerektiren bekleyen güncelleştirme bulunmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-243">Make sure there are no pending updates for Windows Server that require a reboot.</span></span>

2. <span data-ttu-id="a6ba4-244">Kurtarma Hizmetleri aracısında, ağ üzerinden ilk doldurma işlemini tamamlamak için **Şimdi Yedekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-244">In the Recovery Services agent, click **Back Up Now** to complete the initial seeding over the network.</span></span>

    ![Windows Server şimdi yedekle](./media/backup-try-azure-backup-in-10-mins/backup-now.png)

3. <span data-ttu-id="a6ba4-246">Onay sayfasında, Şimdi Yedekle Sihirbazı'nın makineyi yedeklemek için kullanacağı ayarları gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-246">On the Confirmation page, review the settings that the Back Up Now Wizard will use to back up the machine.</span></span> <span data-ttu-id="a6ba4-247">Ardından **Yedekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-247">Then click **Back Up**.</span></span>

4. <span data-ttu-id="a6ba4-248">Sihirbazı kapatmak için **Kapat**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-248">Click **Close** to close the wizard.</span></span> <span data-ttu-id="a6ba4-249">Yedekleme işlemi tamamlanmadan önce sihirbazı kapatırsanız, sihirbaz arka planda çalışmaya devam eder.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-249">If you close the wizard before the backup process finishes, the wizard continues to run in the background.</span></span>

5. <span data-ttu-id="a6ba4-250">Sunucunuzda, Windows Server sistem durumu yanı sıra dosya ve klasörlerinizi yedekleme yapıyorsanız Şimdi Yedekle Sihirbazı yalnızca dosyaların yedeğini alın.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-250">If you back up Files and Folders on your server, in addition to the Windows Server System State, the Backup Now wizard will only back up files.</span></span> <span data-ttu-id="a6ba4-251">Geçici bir sistem durumu Yedekleme gerçekleştirmek için aşağıdaki PowerShell komutunu kullanın:</span><span class="sxs-lookup"><span data-stu-id="a6ba4-251">To perform an ad hoc System State back up, use the following PowerShell command:</span></span>

    ```
    PS C:\> Start-OBSystemStateBackup
    ```

  <span data-ttu-id="a6ba4-252">İlk yedekleme tamamlandıktan sonra, Yedekleme konsolunda **İş tamamlandı** durumu görünür.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-252">After the initial backup is completed, the **Job completed** status appears in the Backup console.</span></span>

  ![IR tamamlandı](./media/backup-try-azure-backup-in-10-mins/ircomplete.png)

## <a name="frequently-asked-questions"></a><span data-ttu-id="a6ba4-254">Sık sorulan sorular</span><span class="sxs-lookup"><span data-stu-id="a6ba4-254">Frequently asked questions</span></span>

<span data-ttu-id="a6ba4-255">Aşağıdaki sorular ve yanıtlar tamamlayıcı bilgiler sağlar.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-255">The following questions and answers provide supplementary information.</span></span>

### <a name="what-is-the-staging-volume"></a><span data-ttu-id="a6ba4-256">Hazırlama toplu nedir?</span><span class="sxs-lookup"><span data-stu-id="a6ba4-256">What is the Staging Volume?</span></span>

<span data-ttu-id="a6ba4-257">Hazırlama toplu sistem durumu yedeklemesi yerel olarak kullanılabilir, Windows Server Yedekleme'burada aşamaları Ara konumunu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-257">The Staging Volume represents the intermediate location where the natively available, Windows Server Backup stages the System State Backup.</span></span> <span data-ttu-id="a6ba4-258">Azure Backup Aracısı sonra sıkıştırır ve bu Ara yedekleme şifreler ve güvenli HTTPS protokolü aracılığıyla yapılandırılmış kurtarma Hizmetleri Kasası'na gönderir.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-258">Azure Backup agent then compresses and encrypts this intermediate backup and sends it via secure HTTPS Protocol to the configured Recovery Services Vault.</span></span> <span data-ttu-id="a6ba4-259">**Bir Windows işletim birim hazırlama toplu oluşturmak önerilir. Sistem durumu yedeklemeleri sorunları gözlemlerseniz, hazırlama biriminiz konumunu denetimi ilk sorun giderme adımdır.**</span><span class="sxs-lookup"><span data-stu-id="a6ba4-259">**We strongly recommended you establish the Staging Volume in a non-Windows-OS volume. If you observe problems with System State Backups, checking the location of your Staging Volume is the first troubleshooting step.**</span></span> 

### <a name="how-can-i-change-the-staging-volume-path-specified-in-the-azure-backup-agent"></a><span data-ttu-id="a6ba4-260">Hazırlama birimi Azure Backup aracısını belirtilen yolu nasıl değiştirebilir miyim?</span><span class="sxs-lookup"><span data-stu-id="a6ba4-260">How can I change the Staging Volume Path specified in the Azure Backup agent?</span></span>

<span data-ttu-id="a6ba4-261">Hazırlama toplu varsayılan önbellek klasöründe bulunur.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-261">The Staging Volume is located in the cache folder by default.</span></span> 

1. <span data-ttu-id="a6ba4-262">Bu konumu değiştirmek için (bir yükseltilmiş komut istemi'nde) aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="a6ba4-262">To change this location, use the following command (in an elevated command prompt):</span></span>
  ```
  PS C:\> Net stop obengine
  ```

2. <span data-ttu-id="a6ba4-263">Ardından aşağıdaki kayıt defteri girdilerini yeni hazırlama toplu klasörünün yolu ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-263">Then update the following registry entries with the path to the new Staging Volume folder.</span></span>

  |<span data-ttu-id="a6ba4-264">Kayıt defteri yolu</span><span class="sxs-lookup"><span data-stu-id="a6ba4-264">Registry path</span></span>|<span data-ttu-id="a6ba4-265">Kayıt defteri anahtarı</span><span class="sxs-lookup"><span data-stu-id="a6ba4-265">Registry key</span></span>|<span data-ttu-id="a6ba4-266">Değer</span><span class="sxs-lookup"><span data-stu-id="a6ba4-266">Value</span></span>|
  |-------------|------------|-----|
  |<span data-ttu-id="a6ba4-267">HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span><span class="sxs-lookup"><span data-stu-id="a6ba4-267">HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span></span> | <span data-ttu-id="a6ba4-268">SSBStagingPath</span><span class="sxs-lookup"><span data-stu-id="a6ba4-268">SSBStagingPath</span></span> | <span data-ttu-id="a6ba4-269">Yeni hazırlama toplu konumu</span><span class="sxs-lookup"><span data-stu-id="a6ba4-269">new staging volume location</span></span> |

<span data-ttu-id="a6ba4-270">Hazırlama yolu büyük küçük harfe duyarlıdır ve hangi sunucuda mevcut olarak tam aynı büyük küçük harf olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-270">The Staging Path is case sensitive and must be the exact same casing as what exists on the server.</span></span> 

3. <span data-ttu-id="a6ba4-271">Hazırlama birimi yolu değiştirdiğinizde, Backup altyapısını yeniden başlatın:</span><span class="sxs-lookup"><span data-stu-id="a6ba4-271">Once you change the Staging volume path, restart the Backup engine:</span></span>
  ```
  PS C:\> Net start obengine
  ```
4. <span data-ttu-id="a6ba4-272">Değiştirilen yolun almak için Microsoft Azure kurtarma Hizmetleri Aracısı'nı açın ve sistem durumunun geçici bir yedeklemeyi tetikleyin.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-272">To pick up the changed path, open the Microsoft Azure Recovery Services agent and trigger an ad hoc backup of System State.</span></span>

### <a name="why-is-the-system-state-default-retention-set-to-60-days"></a><span data-ttu-id="a6ba4-273">Neden sistem durumu varsayılan bekletme 60 gün olarak ayarlanır?</span><span class="sxs-lookup"><span data-stu-id="a6ba4-273">Why is the System State default retention set to 60 days?</span></span>

<span data-ttu-id="a6ba4-274">Bir sistem durumu yedeklemesi kullanım ömrünü "kullanım ömrü" ayarı Windows Server Active Directory rolü için aynıdır.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-274">The useful life of a system state backup is the same as the "tombstone lifetime" setting for the Windows Server Active Directory role.</span></span> <span data-ttu-id="a6ba4-275">Silinmiş Öğe işareti yaşam süresi girişi için varsayılan değer 60 gündür.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-275">The default value for the tombstone lifetime entry is 60 days.</span></span> <span data-ttu-id="a6ba4-276">Bu değer dizin hizmeti (NTDS) config nesnede ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-276">This value can be set on the Directory Service (NTDS) config object.</span></span>

### <a name="how-do-i-change-the-default-backup-and-retention-policy-for-system-state"></a><span data-ttu-id="a6ba4-277">Varsayılan yedekleme ve bekletme ilkesi için sistem durumu nasıl değiştiririm?</span><span class="sxs-lookup"><span data-stu-id="a6ba4-277">How do I change the default Backup and Retention Policy for System State?</span></span>

<span data-ttu-id="a6ba4-278">Varsayılan yedekleme ve sistem durumu için bekletme ilkesini değiştirmek için:</span><span class="sxs-lookup"><span data-stu-id="a6ba4-278">To change the default Backup and Retention Policy for System State:</span></span>
1. <span data-ttu-id="a6ba4-279">Backup altyapısını durdurun.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-279">Stop the Backup engine.</span></span> <span data-ttu-id="a6ba4-280">Yükseltilmiş bir komut isteminden aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-280">Run the following command from an elevated command prompt.</span></span>

  ```
  PS C:\> Net stop obengine
  ```

2. <span data-ttu-id="a6ba4-281">Ekleyin veya HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider aşağıdaki kayıt defteri anahtar girişlerinde güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-281">Add or update the following registry key entries in HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider.</span></span>

  |<span data-ttu-id="a6ba4-282">Kayıt defteri adı</span><span class="sxs-lookup"><span data-stu-id="a6ba4-282">Registry Name</span></span>|<span data-ttu-id="a6ba4-283">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a6ba4-283">Description</span></span>|<span data-ttu-id="a6ba4-284">Değer</span><span class="sxs-lookup"><span data-stu-id="a6ba4-284">Value</span></span>|
  |-------------|-----------|-----|
  |<span data-ttu-id="a6ba4-285">SSBScheduleTime</span><span class="sxs-lookup"><span data-stu-id="a6ba4-285">SSBScheduleTime</span></span>|<span data-ttu-id="a6ba4-286">Yedekleme yapılandırmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-286">Used to configure the time of the backup.</span></span> <span data-ttu-id="a6ba4-287">9 yerel saati varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-287">Default is 9PM local time.</span></span>|<span data-ttu-id="a6ba4-288">DWord: Biçimi 9:30 yerel saati 2130 örneğin SSDD (ondalık)</span><span class="sxs-lookup"><span data-stu-id="a6ba4-288">DWord: Format HHMM (Decimal) for example 2130 for 9:30PM local time</span></span>|
  |<span data-ttu-id="a6ba4-289">SSBScheduleDays</span><span class="sxs-lookup"><span data-stu-id="a6ba4-289">SSBScheduleDays</span></span>|<span data-ttu-id="a6ba4-290">Belirtilen zamanda bir sistem durumu yedeklemesi zaman gerçekleştirilmelidir gün yapılandırmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-290">Used to configure the days when System State Backup must be performed at the specified time.</span></span> <span data-ttu-id="a6ba4-291">Tek tek basamak haftanın günleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-291">Individual digits specify days of the week.</span></span> <span data-ttu-id="a6ba4-292">0 Pazar gösteren, 1. Pazartesi, vb..</span><span class="sxs-lookup"><span data-stu-id="a6ba4-292">0 represents Sunday, 1 is Monday, and so on.</span></span> <span data-ttu-id="a6ba4-293">Varsayılan yedekleme için Pazar günüdür.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-293">Default day for backup is Sunday.</span></span>|<span data-ttu-id="a6ba4-294">DWord: Yedekleme (örneğin 1230 Pazartesi, Salı, Çarşamba ve Pazar yedeklemeler zamanlar ondalık) çalıştırmak için haftanın günlerini.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-294">DWord: days of the week to run backup (decimal) for example 1230 schedules backups on Monday, Tuesday, Wednesday, and Sunday.</span></span>|
  |<span data-ttu-id="a6ba4-295">SSBRetentionDays</span><span class="sxs-lookup"><span data-stu-id="a6ba4-295">SSBRetentionDays</span></span>|<span data-ttu-id="a6ba4-296">Yedekleme tutulacağı gün yapılandırmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-296">Used to configure the days to retain backup.</span></span> <span data-ttu-id="a6ba4-297">Varsayılan değer 60'tır.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-297">Default value is 60.</span></span> <span data-ttu-id="a6ba4-298">Değer izin verilen en fazla 180'dir.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-298">Maximum allowed value is 180.</span></span>|<span data-ttu-id="a6ba4-299">DWord: Yedekleme (ondalık) tutulacağı gün sayısı.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-299">DWord: Days to retain backup (decimal).</span></span>|

3. <span data-ttu-id="a6ba4-300">Yedekleme Altyapısı yeniden başlatmak için aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-300">Use the following command to restart the backup engine.</span></span>
    ```
    PS C:\> Net start obengine
    ```

4. <span data-ttu-id="a6ba4-301">Microsoft Kurtarma Hizmetleri Aracısı'nı açın.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-301">Open the Microsoft Recovery Services agent.</span></span>

5. <span data-ttu-id="a6ba4-302">Tıklatın **yedekleme zamanlaması** ve ardından **sonraki** kadar yansıtılan değişiklikleri görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-302">Click **Schedule Backup** and then click **Next** until you see the changes reflected.</span></span>

6. <span data-ttu-id="a6ba4-303">Tıklatın **son** değişiklikleri uygulamak için.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-303">Click **Finish** to apply the changes.</span></span>


## <a name="questions"></a><span data-ttu-id="a6ba4-304">Sorularınız mı var?</span><span class="sxs-lookup"><span data-stu-id="a6ba4-304">Questions?</span></span>
<span data-ttu-id="a6ba4-305">Sorularınız varsa veya dahil edilmesini istediğiniz herhangi bir özellik varsa [bize geri bildirim gönderin](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="a6ba4-305">If you have questions, or if there is any feature that you would like to see included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6ba4-306">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a6ba4-306">Next steps</span></span>
* <span data-ttu-id="a6ba4-307">[Windows makinelerini yedekleme](backup-configure-vault.md) konusunda daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-307">Get more details about [backing up Windows machines](backup-configure-vault.md).</span></span>
* <span data-ttu-id="a6ba4-308">Dosya ve klasörlerinizi yedeklediğinize göre artık [kasa ve sunucularınızı yönetebilirsiniz](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="a6ba4-308">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="a6ba4-309">Bir yedeklemeyi geri yüklemeniz gerekirse [dosyaları bir Windows makinesine geri yüklemek](backup-azure-restore-windows-server.md) için bu makaleyi kullanın.</span><span class="sxs-lookup"><span data-stu-id="a6ba4-309">If you need to restore a backup, use this article to [restore files to a Windows machine](backup-azure-restore-windows-server.md).</span></span>
