---
title: "Azure yedekleme kasaları ve sunucuları Klasik dağıtım modelini kullanarak Azure yönetmek | Microsoft Docs"
description: "Azure yedekleme kasaları ve sunucuları yönetmek nasıl öğrenmek için bu öğreticiyi kullanın."
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
ms.openlocfilehash: 91451b2cdc42ed05ef7c1ba9c66ad5b4b45dd788
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-azure-backup-vaults-and-servers-using-the-classic-deployment-model"></a><span data-ttu-id="ca5d1-103">Klasik dağıtım modelini kullanarak Azure Backup kasa ve sunucularını yönetme</span><span class="sxs-lookup"><span data-stu-id="ca5d1-103">Manage Azure Backup vaults and servers using the classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ca5d1-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ca5d1-104">Resource Manager</span></span>](backup-azure-manage-windows-server.md)
> * [<span data-ttu-id="ca5d1-105">Klasik</span><span class="sxs-lookup"><span data-stu-id="ca5d1-105">Classic</span></span>](backup-azure-manage-windows-server-classic.md)
>
>

<span data-ttu-id="ca5d1-106">Bu makalede, Klasik Azure portalı ve Microsoft Azure Yedekleme aracısı aracılığıyla sunulan yedekleme yönetim görevlerini genel bir bakış bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-106">In this article you'll find an overview of the backup management tasks available through the Azure classic portal and the Microsoft Azure Backup agent.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ca5d1-107">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ca5d1-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ca5d1-108">Bu makalede, Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-108">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="ca5d1-109">Microsoft, yeni dağıtımların çoğunun Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ca5d1-110">Artık Backup kasalarınızı Kurtarma Hizmetleri kasalarına yükseltebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-110">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="ca5d1-111">Ayrıntılı bilgi için [Backup kasasını Kurtarma Hizmetleri kasasına yükseltme](backup-azure-upgrade-backup-to-recovery-services.md) makalesine bakın.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-111">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="ca5d1-112">Microsoft, Backup kasalarınızı Kurtarma Hizmetleri kasalarına yükseltmenizi önerir.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-112">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="ca5d1-113">15 Ekim 2017’den itibaren, PowerShell kullanarak Backup kasaları oluşturamayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-113">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="ca5d1-114">**1 Kasım 2017’ye kadar**:</span><span class="sxs-lookup"><span data-stu-id="ca5d1-114">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="ca5d1-115">Yükseltilmemiş olan tüm Backup kasaları Kurtarma Hizmetleri kasalarına otomatik olarak yükseltilecektir.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-115">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="ca5d1-116">Klasik portalda yedekleme verilerinize erişemeyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-116">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="ca5d1-117">Bunun yerine, Kurtarma Hizmetleri kasalarındaki yedekleme verilerinize erişmek için Azure portalını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-117">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

## <a name="management-portal-tasks"></a><span data-ttu-id="ca5d1-118">Yönetim Portalı görevleri</span><span class="sxs-lookup"><span data-stu-id="ca5d1-118">Management portal tasks</span></span>
1. <span data-ttu-id="ca5d1-119">Oturum [Yönetim Portalı](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="ca5d1-119">Sign in to the [Management Portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="ca5d1-120">Tıklatın **kurtarma Hizmetleri**, hızlı başlangıç sayfasını görüntülemek için yedekleme kasasının adını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-120">Click **Recovery Services**, then click the name of backup vault to view the Quick Start page.</span></span>

    ![Kurtarma Hizmetleri](./media/backup-azure-manage-windows-server-classic/rs-left-nav.png)

<span data-ttu-id="ca5d1-122">Sayfanın üst kısmındaki hızlı başlangıç seçenekleri belirleyerek, kullanılabilir yönetim görevlerini görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-122">By selecting the options at the top of the Quick Start page, you can see the available management tasks.</span></span>

![Sekmeleri yönetme](./media/backup-azure-manage-windows-server-classic/qs-page.png)

### <a name="dashboard"></a><span data-ttu-id="ca5d1-124">Pano</span><span class="sxs-lookup"><span data-stu-id="ca5d1-124">Dashboard</span></span>
<span data-ttu-id="ca5d1-125">Seçin **Pano** sunucusu için kullanım genel bakış için.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-125">Select **Dashboard** to see the usage overview for the server.</span></span> <span data-ttu-id="ca5d1-126">**Kullanıma genel bakış** içerir:</span><span class="sxs-lookup"><span data-stu-id="ca5d1-126">The **usage overview** includes:</span></span>

* <span data-ttu-id="ca5d1-127">Bulut için kayıtlı Windows sunucuları sayısı</span><span class="sxs-lookup"><span data-stu-id="ca5d1-127">The number of Windows Servers registered to cloud</span></span>
* <span data-ttu-id="ca5d1-128">Bulutta korumalı Azure sanal makine sayısı</span><span class="sxs-lookup"><span data-stu-id="ca5d1-128">The number of Azure virtual machines protected in cloud</span></span>
* <span data-ttu-id="ca5d1-129">Azure'da tüketilen toplam depolama alanı</span><span class="sxs-lookup"><span data-stu-id="ca5d1-129">The total storage consumed in Azure</span></span>
* <span data-ttu-id="ca5d1-130">En son işlerin durumunu</span><span class="sxs-lookup"><span data-stu-id="ca5d1-130">The status of recent jobs</span></span>

<span data-ttu-id="ca5d1-131">Pano alt kısmında, aşağıdaki görevleri gerçekleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ca5d1-131">At the bottom of the Dashboard you can perform the following tasks:</span></span>

* <span data-ttu-id="ca5d1-132">**Sertifika yönetmek** - sunucuyu kaydetmek ve ardından bu sertifikayı güncelleştirmek için kullanmak için bir sertifika kullanıldıysa.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-132">**Manage certificate** - If a certificate was used to register the server, then use this to update the certificate.</span></span> <span data-ttu-id="ca5d1-133">Kasa kimlik bilgileri kullanıyorsanız kullanmayın **Yönet sertifika**.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-133">If you are using vault credentials, do not use **Manage certificate**.</span></span>
* <span data-ttu-id="ca5d1-134">**Silme** -geçerli yedekleme kasası siler.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-134">**Delete** - Deletes the current backup vault.</span></span> <span data-ttu-id="ca5d1-135">Bir yedekleme kasası artık kullanılıyorsa, depolama alanı boşaltmak için silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-135">If a backup vault is no longer being used, you can delete it to free up storage space.</span></span> <span data-ttu-id="ca5d1-136">**Silme** tüm kayıtlı sunucuları kasadan silindikten sonra yalnızca etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-136">**Delete** is only enabled after all registered servers have been deleted from the vault.</span></span>

![Yedekleme Pano görevleri](./media/backup-azure-manage-windows-server-classic/dashboard-tasks.png)

## <a name="registered-items"></a><span data-ttu-id="ca5d1-138">Kayıtlı öğeler</span><span class="sxs-lookup"><span data-stu-id="ca5d1-138">Registered items</span></span>
<span data-ttu-id="ca5d1-139">Seçin **kayıtlı öğeler** bu kasaya kayıtlı sunucularının adlarını görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-139">Select **Registered Items** to view the names of the servers that are registered to this vault.</span></span>

![Kayıtlı öğeler](./media/backup-azure-manage-windows-server-classic/registered-items.png)

<span data-ttu-id="ca5d1-141">**Türü** filtre varsayılanları için Azure sanal makine.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-141">The **Type** filter defaults to Azure Virtual Machine.</span></span> <span data-ttu-id="ca5d1-142">Bu kasaya kayıtlı sunucularının adlarını görüntülemek için seçin **Windows server** açılan menüden.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-142">To view the names of the servers that are registered to this vault, select **Windows server** from the drop down menu.</span></span>

<span data-ttu-id="ca5d1-143">Buradan, aşağıdaki görevleri gerçekleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ca5d1-143">From here you can perform the following tasks:</span></span>

* <span data-ttu-id="ca5d1-144">**Yeniden kayda izin** - kullanabileceğiniz bir sunucu için bu seçenek belirlendiğinde, **Kayıt Sihirbazı'nı** yedeklemeyle sunucuyu kaydetmek için şirket içi Microsoft Azure Yedekleme aracısı, ikinci kez Kasa.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-144">**Allow Re-registration** - When this option is selected for a server you can use the **Registration Wizard** in the on-premises Microsoft Azure Backup agent to register the server with the backup vault a second time.</span></span> <span data-ttu-id="ca5d1-145">Sertifika bir hata nedeniyle yeniden kaydetmeniz gerekebilir veya bir sunucusunun derlenmeye sahip.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-145">You might need to re-register due to an error in the certificate or if a server had to be rebuilt.</span></span>
* <span data-ttu-id="ca5d1-146">**Silme** -bir sunucu yedek Kasası'nı siler.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-146">**Delete** - Deletes a server from the backup vault.</span></span> <span data-ttu-id="ca5d1-147">Tüm sunucuyla ilişkili tüm depolanmış veriler hemen silinir.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-147">All of the stored data associated with the server is deleted immediately.</span></span>

    ![Kayıtlı öğeleri görevleri](./media/backup-azure-manage-windows-server-classic/registered-items-tasks.png)

## <a name="protected-items"></a><span data-ttu-id="ca5d1-149">Korumalı öğeler</span><span class="sxs-lookup"><span data-stu-id="ca5d1-149">Protected items</span></span>
<span data-ttu-id="ca5d1-150">Seçin **korunan öğeler** sunucularından yedeklenen öğeleri görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-150">Select **Protected Items** to view the items that have been backed up from the servers.</span></span>

![Korumalı öğeler](./media/backup-azure-manage-windows-server-classic/protected-items.png)

## <a name="configure"></a><span data-ttu-id="ca5d1-152">Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ca5d1-152">Configure</span></span>
<span data-ttu-id="ca5d1-153">Gelen **yapılandırma** sekmesini uygun depolama artıklığı seçeneği seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-153">From the **Configure** tab you can select the appropriate storage redundancy option.</span></span> <span data-ttu-id="ca5d1-154">Depolama artıklığı seçeneği seçmek için en iyi bir kasası oluşturduktan sonra ve herhangi bir makine için kayıtlı önce sağ saattir.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-154">The best time to select the storage redundancy option is right after creating a vault and before any machines are registered to it.</span></span>

> [!WARNING]
> <span data-ttu-id="ca5d1-155">Bir öğe Kasası'na kaydedildikten sonra depolama artıklığı seçeneği kilitli ve değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-155">Once an item has been registered to the vault, the storage redundancy option is locked and cannot be modified.</span></span>
>
>

![Yapılandırma](./media/backup-azure-manage-windows-server-classic/configure.png)

<span data-ttu-id="ca5d1-157">Bu makalede daha fazla bilgi için bkz: [depolama artıklığı](../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="ca5d1-157">See this article for more information about [storage redundancy](../storage/common/storage-redundancy.md).</span></span>

## <a name="microsoft-azure-backup-agent-tasks"></a><span data-ttu-id="ca5d1-158">Microsoft Azure Yedekleme aracısı görevleri</span><span class="sxs-lookup"><span data-stu-id="ca5d1-158">Microsoft Azure Backup agent tasks</span></span>
### <a name="console"></a><span data-ttu-id="ca5d1-159">Konsol</span><span class="sxs-lookup"><span data-stu-id="ca5d1-159">Console</span></span>
<span data-ttu-id="ca5d1-160">Açık **Microsoft Azure Yedekleme aracısı** (makinenizi arayarak bulabilirsiniz *Microsoft Azure yedekleme*).</span><span class="sxs-lookup"><span data-stu-id="ca5d1-160">Open the **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

![Yedekleme aracısı](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)

<span data-ttu-id="ca5d1-162">Gelen **Eylemler** aşağıdaki yönetim görevlerini gerçekleştirebilirsiniz yedekleme aracısını konsol sağında kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="ca5d1-162">From the **Actions** available at the right of the backup agent console you can perform the following management tasks:</span></span>

* <span data-ttu-id="ca5d1-163">Sunucuyu kaydetmek</span><span class="sxs-lookup"><span data-stu-id="ca5d1-163">Register Server</span></span>
* <span data-ttu-id="ca5d1-164">Yedekleme zamanlaması</span><span class="sxs-lookup"><span data-stu-id="ca5d1-164">Schedule Backup</span></span>
* <span data-ttu-id="ca5d1-165">Şimdi Yedekle</span><span class="sxs-lookup"><span data-stu-id="ca5d1-165">Back Up now</span></span>
* <span data-ttu-id="ca5d1-166">Özelliklerini değiştir</span><span class="sxs-lookup"><span data-stu-id="ca5d1-166">Change Properties</span></span>

![Aracı konsol eylemleri](./media/backup-azure-manage-windows-server-classic/console-actions.png)

> [!NOTE]
> <span data-ttu-id="ca5d1-168">İçin **verileri kurtarabilirsiniz**, bkz: [bir Windows server veya Windows istemci makinesi dosyaları geri yükle](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="ca5d1-168">To **Recover Data**, see [Restore files to a Windows server or Windows client machine](backup-azure-restore-windows-server.md).</span></span>
>
>

### <a name="modify-an-existing-backup"></a><span data-ttu-id="ca5d1-169">Varolan bir yedeği değiştirme</span><span class="sxs-lookup"><span data-stu-id="ca5d1-169">Modify an existing backup</span></span>
1. <span data-ttu-id="ca5d1-170">Microsoft Azure yedekleme Aracısı'nı **yedekleme zamanlaması**.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-170">In the Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Windows Server yedeklemesini zamanlama](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
2. <span data-ttu-id="ca5d1-172">İçinde **Yedekleme Zamanlama Sihirbazı** bırakın **yedekleme öğeleri veya saatler için değişiklik yapma** seçeneğe ve tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-172">In the **Schedule Backup Wizard** leave the **Make changes to backup items or times** option selected and click **Next**.</span></span>

    ![Zamanlanmış yedekleme değiştirme](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
3. <span data-ttu-id="ca5d1-174">Ekleme veya öğeleri değiştirmek isteyip istemediğinizi **yedeklenecek öğeleri seçin** ekran tıklatın **öğeleri Ekle**.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-174">If you want to add or change items, on the **Select Items to Backup** screen click **Add Items**.</span></span>

    <span data-ttu-id="ca5d1-175">Ayrıca ayarlayabilirsiniz **dışarıda bırakma ayarları** Sihirbazı'nda bu sayfadan.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-175">You can also set **Exclusion Settings** from this page in the wizard.</span></span> <span data-ttu-id="ca5d1-176">Dosya türleri ekleme yordamı okuma ya da dosyaları hariç tutmak istiyorsanız [dışarıda bırakma ayarları](#exclusion-settings).</span><span class="sxs-lookup"><span data-stu-id="ca5d1-176">If you want to exclude files or file types read the procedure for adding [exclusion settings](#exclusion-settings).</span></span>
4. <span data-ttu-id="ca5d1-177">Dosya ve, önce yedeklemek istediğiniz klasörleri seçin **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-177">Select the files and folders you want to back up and click **Okay**.</span></span>

    ![Öğe ekle](./media/backup-azure-manage-windows-server-classic/add-items-modify.png)
5. <span data-ttu-id="ca5d1-179">Belirtin **yedekleme zamanlaması** tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-179">Specify the **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="ca5d1-180">(En fazla günde 3 kereye) günlük veya haftalık yedeklemeler zamanlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-180">You can schedule daily (at a maximum of 3 times per day) or weekly backups.</span></span>

    ![Yedekleme zamanlamasını belirtin](./media/backup-azure-manage-windows-server-classic/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > <span data-ttu-id="ca5d1-182">Yedekleme zamanlaması belirtme açıklanmıştır bu ayrıntılı [makale](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="ca5d1-182">Specifying the backup schedule is explained in detail in this [article](backup-azure-backup-cloud-as-tape.md).</span></span>
   >
   >
6. <span data-ttu-id="ca5d1-183">Seçin **Bekletme İlkesi** tıklatın ve yedek kopya için **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-183">Select the **Retention Policy** for the backup copy and click **Next**.</span></span>

    ![Bekletme İlkesi seçin](./media/backup-azure-manage-windows-server-classic/select-retention-policy-modify.png)
7. <span data-ttu-id="ca5d1-185">Üzerinde **onay** ekranı bilgileri gözden geçirin ve tıklatın **son**.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-185">On the **Confirmation** screen review the information and click **Finish**.</span></span>
8. <span data-ttu-id="ca5d1-186">Oluşturma Sihirbazı'nı tamamladıktan sonra **yedekleme zamanlaması**, tıklatın **Kapat**.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-186">Once the wizard finishes creating the **backup schedule**, click **Close**.</span></span>

    <span data-ttu-id="ca5d1-187">Korumayı değiştirdikten sonra yedeklemeler doğru giderek tetikleyen olduğunu onaylayabilirsiniz **işleri** sekmesi ve değişiklikler yedekleme işleri yansıtılır onaylama.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-187">After modifying protection, you can confirm that backups are triggering correctly by going to the **Jobs** tab and confirming that changes are reflected in the backup jobs.</span></span>

### <a name="enable-network-throttling"></a><span data-ttu-id="ca5d1-188">Ağ azaltmayı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="ca5d1-188">Enable Network Throttling</span></span>
<span data-ttu-id="ca5d1-189">Azure Backup aracısını, veri aktarımı sırasında ağ bant genişliğinin nasıl kullanıldığını denetlemenize olanak tanıyan bir azaltma sekmesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-189">The Azure Backup agent provides a Throttling tab which allows you to control how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="ca5d1-190">Bu denetim sırasında verilerin yedeklemeniz gerekiyorsa, çalışma saatleri ancak Yedekleme işleminin diğer internet trafiğine engel olmasını istiyor musunuz yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-190">This control can be helpful if you need to back up data during work hours but do not want the backup process to interfere with other internet traffic.</span></span> <span data-ttu-id="ca5d1-191">Verilerin azaltma aktarımı yedeklemek ve geri yükleme etkinlikleri için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-191">Throttling of data transfer applies to back up and restore activities.</span></span>  

<span data-ttu-id="ca5d1-192">Azaltmayı etkinleştirmek için:</span><span class="sxs-lookup"><span data-stu-id="ca5d1-192">To enable throttling:</span></span>

1. <span data-ttu-id="ca5d1-193">İçinde **Backup Aracısı**, tıklatın **özelliklerini değiştirme**.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-193">In the **Backup agent**, click **Change Properties**.</span></span>
2. <span data-ttu-id="ca5d1-194">Seçin **yedekleme işlemleri için Internet bant genişliği kullanımı daraltmayı etkinleştir** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-194">Select the **Enable internet bandwidth usage throttling for backup operations** checkbox.</span></span>

    ![Ağ azaltma](./media/backup-azure-manage-windows-server-classic/throttling-dialog.png)
3. <span data-ttu-id="ca5d1-196">Azaltma etkinleştirdikten sonra sırasında yedek veri aktarımı için izin verilen bant genişliğini belirtin **çalışma saatleri** ve **çalışılmayan saatler**.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-196">Once you have enabled throttling, specify the allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="ca5d1-197">Bant genişliği değerler 512 KB / saniye (Kbps) başlar ve en fazla 1023 MB / saniye (Mbps) gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-197">The bandwidth values begin at 512 kilobytes per second (Kbps) and can go up to 1023 megabytes per second (Mbps).</span></span> <span data-ttu-id="ca5d1-198">Ayrıca başlangıç belirleyin ve için son **çalışma saatleri**, ve haftanın hangi günleri iş dikkate gün.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-198">You can also designate the start and finish for **Work hours**, and which days of the week are considered Work days.</span></span> <span data-ttu-id="ca5d1-199">Belirtilen iş saatleri dışında saat İş dışı saatler olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-199">The time outside of the designated Work hours is considered to be non-work hours.</span></span>
4. <span data-ttu-id="ca5d1-200">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-200">Click **OK**.</span></span>

## <a name="exclusion-settings"></a><span data-ttu-id="ca5d1-201">Dışlama ayarları</span><span class="sxs-lookup"><span data-stu-id="ca5d1-201">Exclusion settings</span></span>
1. <span data-ttu-id="ca5d1-202">Açık **Microsoft Azure Yedekleme aracısı** (makinenizi arayarak bulabilirsiniz *Microsoft Azure yedekleme*).</span><span class="sxs-lookup"><span data-stu-id="ca5d1-202">Open the **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

    ![Açık Yedekleme aracısı](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)
2. <span data-ttu-id="ca5d1-204">Microsoft Azure yedekleme Aracısı'nı **yedekleme zamanlaması**.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-204">In the Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Windows Server yedeklemesini zamanlama](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
3. <span data-ttu-id="ca5d1-206">Yedekleme zamanlaması Sihirbazı'nı bırakın, **yedekleme öğeleri veya saatler için değişiklik yapma** seçeneğe ve tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-206">In the Schedule Backup Wizard leave the **Make changes to backup items or times** option selected and click **Next**.</span></span>

    ![Bir zamanlamayı değiştirmek](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
4. <span data-ttu-id="ca5d1-208">Tıklatın **dışlama ayarları**.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-208">Click **Exclusions Settings**.</span></span>

    ![Çıkarılacak öğeleri seçin](./media/backup-azure-manage-windows-server-classic/exclusion-settings.png)
5. <span data-ttu-id="ca5d1-210">Tıklatın **dışlama eklemek**.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-210">Click **Add Exclusion**.</span></span>

    ![Özel durumları ekleme](./media/backup-azure-manage-windows-server-classic/add-exclusion.png)
6. <span data-ttu-id="ca5d1-212">Konum seçin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-212">Select the location and then, click **OK**.</span></span>

    ![Dışlama için bir konum seçin](./media/backup-azure-manage-windows-server-classic/exclusion-location.png)
7. <span data-ttu-id="ca5d1-214">Dosya uzantısını Ekle **dosya türü** alan.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-214">Add the file extension in the **File Type** field.</span></span>

    ![Dosya türüne göre Dışla](./media/backup-azure-manage-windows-server-classic/exclude-file-type.png)

    <span data-ttu-id="ca5d1-216">.Mp3 uzantı ekleme</span><span class="sxs-lookup"><span data-stu-id="ca5d1-216">Adding an .mp3 extension</span></span>

    ![Dosya türü örneği](./media/backup-azure-manage-windows-server-classic/exclude-mp3.png)

    <span data-ttu-id="ca5d1-218">Başka bir uzantı eklemek için tıklatın **dışlama Ekle** ve (.jpeg uzantı eklemeden) başka bir dosya türü uzantısını girin.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-218">To add another extension, click **Add Exclusion** and enter another file type extension (adding a .jpeg extension).</span></span>

    ![Başka bir dosya türü örneği](./media/backup-azure-manage-windows-server-classic/exclude-jpg.png)
8. <span data-ttu-id="ca5d1-220">Tüm uzantıları eklediğinizde, tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-220">When you've added all the extensions, click **OK**.</span></span>
9. <span data-ttu-id="ca5d1-221">Yedeklemeyi zamanlama Sihirbazı tıklayarak devam **sonraki** kadar **onay sayfası**, ardından **son**.</span><span class="sxs-lookup"><span data-stu-id="ca5d1-221">Continue through the Schedule Backup Wizard by clicking **Next** until the **Confirmation page**, then click **Finish**.</span></span>

    ![Dışlama onayı](./media/backup-azure-manage-windows-server-classic/finish-exclusions.png)

## <a name="next-steps"></a><span data-ttu-id="ca5d1-223">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ca5d1-223">Next steps</span></span>
* [<span data-ttu-id="ca5d1-224">Windows Server veya Windows İstemcisi Azure'dan geri yükleme</span><span class="sxs-lookup"><span data-stu-id="ca5d1-224">Restore Windows Server or Windows Client from Azure</span></span>](backup-azure-restore-windows-server.md)
* <span data-ttu-id="ca5d1-225">Azure yedekleme hakkında daha fazla bilgi için bkz: [Azure Yedekleme'ye Genel Bakış](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="ca5d1-225">To learn more about Azure Backup, see [Azure Backup Overview](backup-introduction-to-azure-backup.md)</span></span>
* <span data-ttu-id="ca5d1-226">Ziyaret [Azure yedekleme Forumu](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span><span class="sxs-lookup"><span data-stu-id="ca5d1-226">Visit the [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span></span>
