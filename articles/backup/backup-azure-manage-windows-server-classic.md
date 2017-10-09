---
title: "aaaManage Azure yedekleme kasaları ve sunucuları Azure hello Klasik dağıtım modeli kullanarak | Microsoft Docs"
description: "Bu öğretici toolearn nasıl toomanage Azure yedekleme kasaları ve sunucuları kullanın."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: tysonn
ms.assetid: f175eb12-0905-437f-91fd-eaee03ab6e81
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: markgal;
ms.openlocfilehash: 6c38b04f4a76604bfd639a9b2d58237ce44e2386
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-backup-vaults-and-servers-using-hello-classic-deployment-model"></a><span data-ttu-id="a6389-103">Azure yedekleme kasaları ve hello Klasik dağıtım modelini kullanarak sunucuları yönetme</span><span class="sxs-lookup"><span data-stu-id="a6389-103">Manage Azure Backup vaults and servers using hello classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a6389-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a6389-104">Resource Manager</span></span>](backup-azure-manage-windows-server.md)
> * [<span data-ttu-id="a6389-105">Klasik</span><span class="sxs-lookup"><span data-stu-id="a6389-105">Classic</span></span>](backup-azure-manage-windows-server-classic.md)
>
>

<span data-ttu-id="a6389-106">Bu makalede, hello yedekleme yönetim görevlerini hello Klasik Azure portalı kullanılabilir ve Microsoft Azure Yedekleme aracısı hello genel bakış bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6389-106">In this article you'll find an overview of hello backup management tasks available through hello Azure classic portal and hello Microsoft Azure Backup agent.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a6389-107">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="a6389-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="a6389-108">Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="a6389-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="a6389-109">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="a6389-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a6389-110">Şimdi, yedekleme kasaları tooRecovery Hizmetleri kasaları yükseltebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6389-110">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="a6389-111">Ayrıntılar için hello makalesine bakın [kurtarma Hizmetleri kasası bir yedekleme kasası tooa yükseltme](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="a6389-111">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="a6389-112">Microsoft tooupgrade önerir tooRecovery Hizmetleri kasalarının yedekleme kasaları.</span><span class="sxs-lookup"><span data-stu-id="a6389-112">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="a6389-113">15 Ekim 2017 sonra PowerShell toocreate yedekleme kasaları kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="a6389-113">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="a6389-114">**1 Kasım 2017’ye kadar**:</span><span class="sxs-lookup"><span data-stu-id="a6389-114">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="a6389-115">Kalan tüm yedekleme kasaları otomatik olarak yükseltilen tooRecovery Hizmetleri kasalarının olacaktır.</span><span class="sxs-lookup"><span data-stu-id="a6389-115">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="a6389-116">Mümkün tooaccess hello Klasik Portalı'nda, yedekleme verilerinizi olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="a6389-116">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="a6389-117">Bunun yerine, hello Azure portal tooaccess kurtarma Hizmetleri kasalarının, yedekleme verilerinizi kullanın.</span><span class="sxs-lookup"><span data-stu-id="a6389-117">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="management-portal-tasks"></a><span data-ttu-id="a6389-118">Yönetim Portalı görevleri</span><span class="sxs-lookup"><span data-stu-id="a6389-118">Management portal tasks</span></span>
1. <span data-ttu-id="a6389-119">İçinde toohello oturum [Yönetim Portalı](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="a6389-119">Sign in toohello [Management Portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="a6389-120">Tıklatın **kurtarma Hizmetleri**, ardından yedekleme kasası tooview hello hızlı başlangıç sayfası hello adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a6389-120">Click **Recovery Services**, then click hello name of backup vault tooview hello Quick Start page.</span></span>

    ![Kurtarma Hizmetleri](./media/backup-azure-manage-windows-server-classic/rs-left-nav.png)

<span data-ttu-id="a6389-122">Merhaba sayfanın üst kısmındaki hello hızlı başlangıç Hello seçenekleri belirleyerek, hello kullanılabilir yönetim görevlerini görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6389-122">By selecting hello options at hello top of hello Quick Start page, you can see hello available management tasks.</span></span>

![Sekmeleri yönetme](./media/backup-azure-manage-windows-server-classic/qs-page.png)

### <a name="dashboard"></a><span data-ttu-id="a6389-124">Pano</span><span class="sxs-lookup"><span data-stu-id="a6389-124">Dashboard</span></span>
<span data-ttu-id="a6389-125">Seçin **Pano** toosee hello kullanım hello sunucusu için genel bakış.</span><span class="sxs-lookup"><span data-stu-id="a6389-125">Select **Dashboard** toosee hello usage overview for hello server.</span></span> <span data-ttu-id="a6389-126">Merhaba **kullanıma genel bakış** içerir:</span><span class="sxs-lookup"><span data-stu-id="a6389-126">hello **usage overview** includes:</span></span>

* <span data-ttu-id="a6389-127">toocloud kayıtlı Windows sunucuları Hello sayısı</span><span class="sxs-lookup"><span data-stu-id="a6389-127">hello number of Windows Servers registered toocloud</span></span>
* <span data-ttu-id="a6389-128">Azure sanal makine buluta korumalı Hello sayısı</span><span class="sxs-lookup"><span data-stu-id="a6389-128">hello number of Azure virtual machines protected in cloud</span></span>
* <span data-ttu-id="a6389-129">Azure'da tüketilen hello toplam depolama alanı</span><span class="sxs-lookup"><span data-stu-id="a6389-129">hello total storage consumed in Azure</span></span>
* <span data-ttu-id="a6389-130">en son işlerin Hello durumu</span><span class="sxs-lookup"><span data-stu-id="a6389-130">hello status of recent jobs</span></span>

<span data-ttu-id="a6389-131">Hello Pano Hello altındaki hello aşağıdaki görevleri gerçekleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a6389-131">At hello bottom of hello Dashboard you can perform hello following tasks:</span></span>

* <span data-ttu-id="a6389-132">**Sertifika yönetmek** - bir sertifika kullanılan tooregister hello sunucu sonra bu tooupdate hello sertifika kullanın.</span><span class="sxs-lookup"><span data-stu-id="a6389-132">**Manage certificate** - If a certificate was used tooregister hello server, then use this tooupdate hello certificate.</span></span> <span data-ttu-id="a6389-133">Kasa kimlik bilgileri kullanıyorsanız kullanmayın **Yönet sertifika**.</span><span class="sxs-lookup"><span data-stu-id="a6389-133">If you are using vault credentials, do not use **Manage certificate**.</span></span>
* <span data-ttu-id="a6389-134">**Silme** -siler hello geçerli yedekleme kasası.</span><span class="sxs-lookup"><span data-stu-id="a6389-134">**Delete** - Deletes hello current backup vault.</span></span> <span data-ttu-id="a6389-135">Bir yedekleme kasası artık kullanılmayan depolama alanını toofree silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6389-135">If a backup vault is no longer being used, you can delete it toofree up storage space.</span></span> <span data-ttu-id="a6389-136">**Silme** tüm kayıtlı sunucuları hello kasasından silinmiş sonra yalnızca etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="a6389-136">**Delete** is only enabled after all registered servers have been deleted from hello vault.</span></span>

![Yedekleme Pano görevleri](./media/backup-azure-manage-windows-server-classic/dashboard-tasks.png)

## <a name="registered-items"></a><span data-ttu-id="a6389-138">Kayıtlı öğeler</span><span class="sxs-lookup"><span data-stu-id="a6389-138">Registered items</span></span>
<span data-ttu-id="a6389-139">Seçin **kayıtlı öğeler** tooview hello adları olan hello sunucularının toothis kasasına kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="a6389-139">Select **Registered Items** tooview hello names of hello servers that are registered toothis vault.</span></span>

![Kayıtlı öğeler](./media/backup-azure-manage-windows-server-classic/registered-items.png)

<span data-ttu-id="a6389-141">Merhaba **türü** filtre Varsayılanları tooAzure sanal makine.</span><span class="sxs-lookup"><span data-stu-id="a6389-141">hello **Type** filter defaults tooAzure Virtual Machine.</span></span> <span data-ttu-id="a6389-142">kayıtlı toothis kasası hello sunucuları tooview hello adlarını seçin **Windows server** hello açılan menüsünde.</span><span class="sxs-lookup"><span data-stu-id="a6389-142">tooview hello names of hello servers that are registered toothis vault, select **Windows server** from hello drop down menu.</span></span>

<span data-ttu-id="a6389-143">Buradan hello aşağıdaki görevleri gerçekleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a6389-143">From here you can perform hello following tasks:</span></span>

* <span data-ttu-id="a6389-144">**Yeniden kayda izin** - kullanabileceğiniz bir sunucu için bu seçenek belirlendiğinde, hello **Kayıt Sihirbazı'nı** Server'daki hello şirket içi Microsoft Azure Yedekleme aracısı tooregister hello hello yedekleme kasası ikinci kez .</span><span class="sxs-lookup"><span data-stu-id="a6389-144">**Allow Re-registration** - When this option is selected for a server you can use hello **Registration Wizard** in hello on-premises Microsoft Azure Backup agent tooregister hello server with hello backup vault a second time.</span></span> <span data-ttu-id="a6389-145">Merhaba sertifika veya bir sunucu yeniden toobe sahip tooan hata nedeniyle toore kaydını gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="a6389-145">You might need toore-register due tooan error in hello certificate or if a server had toobe rebuilt.</span></span>
* <span data-ttu-id="a6389-146">**Silme** -hello yedekleme kasasından bir sunucu siler.</span><span class="sxs-lookup"><span data-stu-id="a6389-146">**Delete** - Deletes a server from hello backup vault.</span></span> <span data-ttu-id="a6389-147">Tüm hello sunucuyla ilişkili hello depolanan verileri hemen silinir.</span><span class="sxs-lookup"><span data-stu-id="a6389-147">All of hello stored data associated with hello server is deleted immediately.</span></span>

    ![Kayıtlı öğeleri görevleri](./media/backup-azure-manage-windows-server-classic/registered-items-tasks.png)

## <a name="protected-items"></a><span data-ttu-id="a6389-149">Korumalı öğeler</span><span class="sxs-lookup"><span data-stu-id="a6389-149">Protected items</span></span>
<span data-ttu-id="a6389-150">Seçin **korunan öğeler** hello sunucularından yedeklenmiş tooview hello öğeleri.</span><span class="sxs-lookup"><span data-stu-id="a6389-150">Select **Protected Items** tooview hello items that have been backed up from hello servers.</span></span>

![Korumalı öğeler](./media/backup-azure-manage-windows-server-classic/protected-items.png)

## <a name="configure"></a><span data-ttu-id="a6389-152">Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a6389-152">Configure</span></span>
<span data-ttu-id="a6389-153">Merhaba gelen **yapılandırma** sekmesini hello uygun depolama artıklığı seçeneği seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6389-153">From hello **Configure** tab you can select hello appropriate storage redundancy option.</span></span> <span data-ttu-id="a6389-154">Merhaba en iyi zaman tooselect hello depolama artıklığı seçeneği bir kasa oluşturarak hemen sonra ve herhangi bir makine kayıtlı tooit önce ' dir.</span><span class="sxs-lookup"><span data-stu-id="a6389-154">hello best time tooselect hello storage redundancy option is right after creating a vault and before any machines are registered tooit.</span></span>

> [!WARNING]
> <span data-ttu-id="a6389-155">Bir öğe kayıtlı toohello kasası silindikten sonra hello depolama artıklığı seçeneği kilitli ve değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="a6389-155">Once an item has been registered toohello vault, hello storage redundancy option is locked and cannot be modified.</span></span>
>
>

![Yapılandırma](./media/backup-azure-manage-windows-server-classic/configure.png)

<span data-ttu-id="a6389-157">Bu makalede daha fazla bilgi için bkz: [depolama artıklığı](../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="a6389-157">See this article for more information about [storage redundancy](../storage/common/storage-redundancy.md).</span></span>

## <a name="microsoft-azure-backup-agent-tasks"></a><span data-ttu-id="a6389-158">Microsoft Azure Yedekleme aracısı görevleri</span><span class="sxs-lookup"><span data-stu-id="a6389-158">Microsoft Azure Backup agent tasks</span></span>
### <a name="console"></a><span data-ttu-id="a6389-159">Konsol</span><span class="sxs-lookup"><span data-stu-id="a6389-159">Console</span></span>
<span data-ttu-id="a6389-160">Açık hello **Microsoft Azure Yedekleme aracısı** (makinenizi arayarak bulabilirsiniz *Microsoft Azure yedekleme*).</span><span class="sxs-lookup"><span data-stu-id="a6389-160">Open hello **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

![Yedekleme aracısı](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)

<span data-ttu-id="a6389-162">Merhaba gelen **Eylemler** yönetim görevleri aşağıdaki hello gerçekleştirebilirsiniz hello yedekleme aracısını konsolunun sağ hello bulunabilir:</span><span class="sxs-lookup"><span data-stu-id="a6389-162">From hello **Actions** available at hello right of hello backup agent console you can perform hello following management tasks:</span></span>

* <span data-ttu-id="a6389-163">Sunucuyu kaydetmek</span><span class="sxs-lookup"><span data-stu-id="a6389-163">Register Server</span></span>
* <span data-ttu-id="a6389-164">Yedekleme zamanlaması</span><span class="sxs-lookup"><span data-stu-id="a6389-164">Schedule Backup</span></span>
* <span data-ttu-id="a6389-165">Şimdi Yedekle</span><span class="sxs-lookup"><span data-stu-id="a6389-165">Back Up now</span></span>
* <span data-ttu-id="a6389-166">Özelliklerini değiştir</span><span class="sxs-lookup"><span data-stu-id="a6389-166">Change Properties</span></span>

![Aracı konsol eylemleri](./media/backup-azure-manage-windows-server-classic/console-actions.png)

> [!NOTE]
> <span data-ttu-id="a6389-168">çok**verileri kurtarabilirsiniz**, bkz: [geri dosyaları tooa Windows server veya Windows istemci makinesi](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="a6389-168">too**Recover Data**, see [Restore files tooa Windows server or Windows client machine](backup-azure-restore-windows-server.md).</span></span>
>
>

### <a name="modify-an-existing-backup"></a><span data-ttu-id="a6389-169">Varolan bir yedeği değiştirme</span><span class="sxs-lookup"><span data-stu-id="a6389-169">Modify an existing backup</span></span>
1. <span data-ttu-id="a6389-170">Merhaba Microsoft Azure yedekleme Aracısı'nı **yedekleme zamanlaması**.</span><span class="sxs-lookup"><span data-stu-id="a6389-170">In hello Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Windows Server yedeklemesini zamanlama](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
2. <span data-ttu-id="a6389-172">Merhaba, **yedeklemeyi Zamanlama Sihirbazı** hello bırakın **toobackup öğeler veya kez değişiklik yapma** seçeneğe ve tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="a6389-172">In hello **Schedule Backup Wizard** leave hello **Make changes toobackup items or times** option selected and click **Next**.</span></span>

    ![Zamanlanmış yedekleme değiştirme](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
3. <span data-ttu-id="a6389-174">Tooadd istediğiniz veya öğelerde hello değiştirme **öğeleri seçin tooBackup** ekran tıklatın **öğeleri Ekle**.</span><span class="sxs-lookup"><span data-stu-id="a6389-174">If you want tooadd or change items, on hello **Select Items tooBackup** screen click **Add Items**.</span></span>

    <span data-ttu-id="a6389-175">Ayrıca ayarlayabilirsiniz **dışarıda bırakma ayarları** hello Sihirbazı'nda bu sayfadan.</span><span class="sxs-lookup"><span data-stu-id="a6389-175">You can also set **Exclusion Settings** from this page in hello wizard.</span></span> <span data-ttu-id="a6389-176">Dosya türlerini eklemek için hello yordamı okuma ya da tooexclude dosyaları istiyorsanız [dışarıda bırakma ayarları](#exclusion-settings).</span><span class="sxs-lookup"><span data-stu-id="a6389-176">If you want tooexclude files or file types read hello procedure for adding [exclusion settings](#exclusion-settings).</span></span>
4. <span data-ttu-id="a6389-177">Merhaba dosya ve tooback yedeklemek istediğiniz klasörleri seçin **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="a6389-177">Select hello files and folders you want tooback up and click **Okay**.</span></span>

    ![Öğe ekle](./media/backup-azure-manage-windows-server-classic/add-items-modify.png)
5. <span data-ttu-id="a6389-179">Merhaba belirtin **yedekleme zamanlaması** tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="a6389-179">Specify hello **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="a6389-180">(En fazla günde 3 kereye) günlük veya haftalık yedeklemeler zamanlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6389-180">You can schedule daily (at a maximum of 3 times per day) or weekly backups.</span></span>

    ![Yedekleme zamanlamasını belirtin](./media/backup-azure-manage-windows-server-classic/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > <span data-ttu-id="a6389-182">Bu ayrıntılı açıklanmıştır Hello yedekleme zamanlamasını belirtme [makale](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="a6389-182">Specifying hello backup schedule is explained in detail in this [article](backup-azure-backup-cloud-as-tape.md).</span></span>
   >
   >
6. <span data-ttu-id="a6389-183">Select hello **Bekletme İlkesi** hello yedek kopya ve tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="a6389-183">Select hello **Retention Policy** for hello backup copy and click **Next**.</span></span>

    ![Bekletme İlkesi seçin](./media/backup-azure-manage-windows-server-classic/select-retention-policy-modify.png)
7. <span data-ttu-id="a6389-185">Merhaba üzerinde **onay** ekranında hello bilgileri gözden geçir ve tıklatın **son**.</span><span class="sxs-lookup"><span data-stu-id="a6389-185">On hello **Confirmation** screen review hello information and click **Finish**.</span></span>
8. <span data-ttu-id="a6389-186">Merhaba oluşturma Hello Sihirbazı tamamlandıktan sonra **yedekleme zamanlaması**, tıklatın **Kapat**.</span><span class="sxs-lookup"><span data-stu-id="a6389-186">Once hello wizard finishes creating hello **backup schedule**, click **Close**.</span></span>

    <span data-ttu-id="a6389-187">Korumayı değiştirdikten sonra yedeklemeler giderek toohello tarafından doğru şekilde tetikleme onaylayabilirsiniz **işleri** sekmesi ve değişiklikler hello yansıtılır onaylayan yedekleme işleri.</span><span class="sxs-lookup"><span data-stu-id="a6389-187">After modifying protection, you can confirm that backups are triggering correctly by going toohello **Jobs** tab and confirming that changes are reflected in hello backup jobs.</span></span>

### <a name="enable-network-throttling"></a><span data-ttu-id="a6389-188">Ağ azaltmayı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="a6389-188">Enable Network Throttling</span></span>
<span data-ttu-id="a6389-189">veri aktarımı sırasında ağ bant genişliğinin nasıl kullanıldığını toocontrol sağlayan bir azaltma sekmesi Hello Azure Backup aracısını sağlar.</span><span class="sxs-lookup"><span data-stu-id="a6389-189">hello Azure Backup agent provides a Throttling tab which allows you toocontrol how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="a6389-190">Bu denetim verileri tooback çalışma saatlerinde gerekir, ancak diğer Internet trafiği ile Merhaba yedekleme işlemi toointerfere istiyor musunuz yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="a6389-190">This control can be helpful if you need tooback up data during work hours but do not want hello backup process toointerfere with other internet traffic.</span></span> <span data-ttu-id="a6389-191">Verilerin azaltma aktarımı yukarıya tooback uygular ve geri yükleme etkinlikleri.</span><span class="sxs-lookup"><span data-stu-id="a6389-191">Throttling of data transfer applies tooback up and restore activities.</span></span>  

<span data-ttu-id="a6389-192">tooenable azaltma:</span><span class="sxs-lookup"><span data-stu-id="a6389-192">tooenable throttling:</span></span>

1. <span data-ttu-id="a6389-193">Merhaba, **Backup Aracısı**, tıklatın **özelliklerini değiştirme**.</span><span class="sxs-lookup"><span data-stu-id="a6389-193">In hello **Backup agent**, click **Change Properties**.</span></span>
2. <span data-ttu-id="a6389-194">Select hello **yedekleme işlemleri için Internet bant genişliği kullanımı daraltmayı etkinleştir** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="a6389-194">Select hello **Enable internet bandwidth usage throttling for backup operations** checkbox.</span></span>

    ![Ağ azaltma](./media/backup-azure-manage-windows-server-classic/throttling-dialog.png)
3. <span data-ttu-id="a6389-196">Azaltma etkinleştirdikten sonra sırasında yedek veri aktarımı için bant genişliği izin verilen hello belirtin **çalışma saatleri** ve **çalışılmayan saatler**.</span><span class="sxs-lookup"><span data-stu-id="a6389-196">Once you have enabled throttling, specify hello allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="a6389-197">Merhaba bant genişliği değerler 512 KB / saniye (Kbps) başlar ve too1023 megabayt (Mbps) saniyede yukarı gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6389-197">hello bandwidth values begin at 512 kilobytes per second (Kbps) and can go up too1023 megabytes per second (Mbps).</span></span> <span data-ttu-id="a6389-198">Ayrıca hello başlangıç belirleyin ve için son **çalışma saatleri**, ve hello haftanın hangi günleri iş dikkate gün.</span><span class="sxs-lookup"><span data-stu-id="a6389-198">You can also designate hello start and finish for **Work hours**, and which days of hello week are considered Work days.</span></span> <span data-ttu-id="a6389-199">Merhaba çalışma saatleri belirlenmiş hello dışında dikkate alınan toobe İş dışı saatler saattir.</span><span class="sxs-lookup"><span data-stu-id="a6389-199">hello time outside of hello designated Work hours is considered toobe non-work hours.</span></span>
4. <span data-ttu-id="a6389-200">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a6389-200">Click **OK**.</span></span>

## <a name="exclusion-settings"></a><span data-ttu-id="a6389-201">Dışlama ayarları</span><span class="sxs-lookup"><span data-stu-id="a6389-201">Exclusion settings</span></span>
1. <span data-ttu-id="a6389-202">Açık hello **Microsoft Azure Yedekleme aracısı** (makinenizi arayarak bulabilirsiniz *Microsoft Azure yedekleme*).</span><span class="sxs-lookup"><span data-stu-id="a6389-202">Open hello **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

    ![Açık Yedekleme aracısı](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)
2. <span data-ttu-id="a6389-204">Merhaba Microsoft Azure yedekleme Aracısı'nı **yedekleme zamanlaması**.</span><span class="sxs-lookup"><span data-stu-id="a6389-204">In hello Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Windows Server yedeklemesini zamanlama](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
3. <span data-ttu-id="a6389-206">Merhaba yedeklemeyi Zamanlama Sihirbazı hello bırakın **toobackup öğeler veya kez değişiklik yapma** seçeneğe ve tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="a6389-206">In hello Schedule Backup Wizard leave hello **Make changes toobackup items or times** option selected and click **Next**.</span></span>

    ![Bir zamanlamayı değiştirmek](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
4. <span data-ttu-id="a6389-208">Tıklatın **dışlama ayarları**.</span><span class="sxs-lookup"><span data-stu-id="a6389-208">Click **Exclusions Settings**.</span></span>

    ![Öğeleri tooexclude seçin](./media/backup-azure-manage-windows-server-classic/exclusion-settings.png)
5. <span data-ttu-id="a6389-210">Tıklatın **dışlama eklemek**.</span><span class="sxs-lookup"><span data-stu-id="a6389-210">Click **Add Exclusion**.</span></span>

    ![Özel durumları ekleme](./media/backup-azure-manage-windows-server-classic/add-exclusion.png)
6. <span data-ttu-id="a6389-212">Merhaba konum seçin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="a6389-212">Select hello location and then, click **OK**.</span></span>

    ![Dışlama için bir konum seçin](./media/backup-azure-manage-windows-server-classic/exclusion-location.png)
7. <span data-ttu-id="a6389-214">Hello Hello dosya uzantısını Ekle **dosya türü** alan.</span><span class="sxs-lookup"><span data-stu-id="a6389-214">Add hello file extension in hello **File Type** field.</span></span>

    ![Dosya türüne göre Dışla](./media/backup-azure-manage-windows-server-classic/exclude-file-type.png)

    <span data-ttu-id="a6389-216">.Mp3 uzantı ekleme</span><span class="sxs-lookup"><span data-stu-id="a6389-216">Adding an .mp3 extension</span></span>

    ![Dosya türü örneği](./media/backup-azure-manage-windows-server-classic/exclude-mp3.png)

    <span data-ttu-id="a6389-218">tooadd başka bir uzantı tıklatın **dışlama Ekle** ve (.jpeg uzantı eklemeden) başka bir dosya türü uzantısını girin.</span><span class="sxs-lookup"><span data-stu-id="a6389-218">tooadd another extension, click **Add Exclusion** and enter another file type extension (adding a .jpeg extension).</span></span>

    ![Başka bir dosya türü örneği](./media/backup-azure-manage-windows-server-classic/exclude-jpg.png)
8. <span data-ttu-id="a6389-220">Tüm hello uzantıları eklediğinizde, tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="a6389-220">When you've added all hello extensions, click **OK**.</span></span>
9. <span data-ttu-id="a6389-221">Yedeklemeyi zamanlama Sihirbazı Hello tıklayarak devam **sonraki** hello kadar **onay sayfası**, ardından **son**.</span><span class="sxs-lookup"><span data-stu-id="a6389-221">Continue through hello Schedule Backup Wizard by clicking **Next** until hello **Confirmation page**, then click **Finish**.</span></span>

    ![Dışlama onayı](./media/backup-azure-manage-windows-server-classic/finish-exclusions.png)

## <a name="next-steps"></a><span data-ttu-id="a6389-223">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a6389-223">Next steps</span></span>
* [<span data-ttu-id="a6389-224">Windows Server veya Windows İstemcisi Azure'dan geri yükleme</span><span class="sxs-lookup"><span data-stu-id="a6389-224">Restore Windows Server or Windows Client from Azure</span></span>](backup-azure-restore-windows-server.md)
* <span data-ttu-id="a6389-225">Azure yedekleme hakkında daha fazla toolearn bakın [Azure Yedekleme'ye Genel Bakış](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="a6389-225">toolearn more about Azure Backup, see [Azure Backup Overview](backup-introduction-to-azure-backup.md)</span></span>
* <span data-ttu-id="a6389-226">Merhaba ziyaret [Azure yedekleme Forumu](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span><span class="sxs-lookup"><span data-stu-id="a6389-226">Visit hello [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span></span>
