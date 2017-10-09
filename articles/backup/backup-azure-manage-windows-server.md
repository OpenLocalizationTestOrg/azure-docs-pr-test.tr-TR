---
title: "aaaManage Azure kurtarma Hizmetleri kasa ve sunucularınızı | Microsoft Docs"
description: "Bu öğretici toolearn nasıl toomanage Azure kurtarma Hizmetleri kasaları ve sunucuları kullanın."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: tysonn
ms.assetid: 4eea984b-7ed6-4600-ac60-99d2e9cb6d8a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markgal
ms.openlocfilehash: b4c35c86faa0828b3c63a13b85c095c0cbaba50e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-recovery-services-vaults-and-servers-for-windows-machines"></a><span data-ttu-id="bc039-103">Windows makineleri için Azure kurtarma hizmetleri kasaları ile sunucularını izleme ve yönetme</span><span class="sxs-lookup"><span data-stu-id="bc039-103">Monitor and manage Azure recovery services vaults and servers for Windows machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bc039-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bc039-104">Resource Manager</span></span>](backup-azure-manage-windows-server.md)
> * [<span data-ttu-id="bc039-105">Klasik</span><span class="sxs-lookup"><span data-stu-id="bc039-105">Classic</span></span>](backup-azure-manage-windows-server-classic.md)
>
>

<span data-ttu-id="bc039-106">Bu makalede, yedekleme izleme ve yönetim görevlerini hello Azure portal ve hello Microsoft Azure Yedekleme aracısı kullanılabilir hello genel bir bakış bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc039-106">In this article you'll find an overview of hello backup monitor and management tasks available through hello Azure portal and hello Microsoft Azure Backup agent.</span></span> <span data-ttu-id="bc039-107">Bu makalede, zaten bir Azure aboneliğiniz varsa ve en az bir kurtarma Hizmetleri kasası oluşturdunuz varsayılır.</span><span class="sxs-lookup"><span data-stu-id="bc039-107">This article assumes you already have an Azure subscription and have created at least one Recovery Services vault.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]


## <a name="open-a-recovery-services-vault"></a><span data-ttu-id="bc039-108">Kurtarma Hizmetleri kasası açın</span><span class="sxs-lookup"><span data-stu-id="bc039-108">Open a Recovery Services vault</span></span>

<span data-ttu-id="bc039-109">Merhaba kurtarma Hizmetleri kasa Panosu hello ayrıntıları veya bir kurtarma Hizmetleri kasası özniteliklerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="bc039-109">hello Recovery Services vault dashboard shows you hello details or attributes of a Recovery Services vault.</span></span>

1. <span data-ttu-id="bc039-110">İçinde toohello oturum [Azure Portal](https://portal.azure.com/) Azure aboneliğinizi kullanarak.</span><span class="sxs-lookup"><span data-stu-id="bc039-110">Sign in toohello [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="bc039-111">Merhaba Hub menüsünde **daha Hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="bc039-111">On hello Hub menu, click **More Services**.</span></span>

    ![Kurtarma Hizmetleri kasaları adım 1'in açık listesi](./media/backup-azure-manage-windows-server/open-rs-vault-list.png) <br/>

3. <span data-ttu-id="bc039-113">Kurtarma Hizmetleri kasası tooopen istiyor.</span><span class="sxs-lookup"><span data-stu-id="bc039-113">You want tooopen a Recovery Services vault.</span></span> <span data-ttu-id="bc039-114">Merhaba iletişim kutusunda, yazmaya başlayın **kurtarma Hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="bc039-114">In hello dialog box, start typing **Recovery Services**.</span></span> <span data-ttu-id="bc039-115">Yazmaya başladığınızda, hello filtreleyecek girişinize bağlı.</span><span class="sxs-lookup"><span data-stu-id="bc039-115">As you begin typing, hello list will filter based on your input.</span></span> <span data-ttu-id="bc039-116">Tıklatın **kurtarma Hizmetleri kasaları** toodisplay hello listesi kurtarma Hizmetleri kasaları aboneliğinizde.</span><span class="sxs-lookup"><span data-stu-id="bc039-116">Click **Recovery Services vaults** toodisplay hello list of Recovery Services vaults in your subscription.</span></span>

    ![Kurtarma Hizmetleri Kasası oluşturma 1. adım](./media/backup-azure-manage-windows-server/browse-to-rs-vaults-2.png) <br/>

    <span data-ttu-id="bc039-118">Merhaba kurtarma Hizmetleri kasalarının listesi açılır.</span><span class="sxs-lookup"><span data-stu-id="bc039-118">hello list of Recovery Services vaults opens.</span></span>

    ![Kurtarma Hizmetleri Kasası oluşturma 1. adım](./media/backup-azure-manage-windows-server/list-of-rs-vaults.png) <br/>

4. <span data-ttu-id="bc039-120">Kasa Hello listesinden, hello tooopen istediğiniz kurtarma Hizmetleri kasası hello adını seçin.</span><span class="sxs-lookup"><span data-stu-id="bc039-120">From hello list of vaults, select hello name of hello Recovery Services vault you want tooopen.</span></span> <span data-ttu-id="bc039-121">Merhaba kurtarma Hizmetleri kasası Pano dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="bc039-121">hello Recovery Services vault dashboard blade opens.</span></span>

    ![Kurtarma Hizmetleri kasa Panosu](./media/backup-azure-manage-windows-server/rs-vault-blade.png) <br/>

    <span data-ttu-id="bc039-123">Merhaba kurtarma Hizmetleri kasası açtığınız, hello izleme veya yönetim görevlerinden herhangi birini deneyin.</span><span class="sxs-lookup"><span data-stu-id="bc039-123">Now that you have opened hello Recovery Services vault, try any of hello monitoring or management tasks.</span></span>

## <a name="monitor-backup-jobs-and-alerts"></a><span data-ttu-id="bc039-124">Yedekleme işleri izleme ve uyarılar</span><span class="sxs-lookup"><span data-stu-id="bc039-124">Monitor backup jobs and alerts</span></span>

<span data-ttu-id="bc039-125">İşlerini izleme ve hello uyarıları, gördüğünüz Pano, Kurtarma Hizmetleri Kasası:</span><span class="sxs-lookup"><span data-stu-id="bc039-125">You monitor jobs and alerts from hello Recovery Services vault dashboard, where you see:</span></span>

* <span data-ttu-id="bc039-126">Yedekleme uyarıları ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="bc039-126">Backup alerts details</span></span>
* <span data-ttu-id="bc039-127">Dosyaları ve klasörleri yanı sıra, hello bulutta korunan Azure sanal makineler</span><span class="sxs-lookup"><span data-stu-id="bc039-127">Files and folders, as well as Azure virtual machines protected in hello cloud</span></span>
* <span data-ttu-id="bc039-128">Azure'da tüketilen toplam depolama alanı</span><span class="sxs-lookup"><span data-stu-id="bc039-128">Total storage consumed in Azure</span></span>
* <span data-ttu-id="bc039-129">Yedekleme işi durumu</span><span class="sxs-lookup"><span data-stu-id="bc039-129">Backup job status</span></span>

![Yedekleme Pano görevleri](./media/backup-azure-manage-windows-server/dashboard-tiles.png)

<span data-ttu-id="bc039-131">Her bu kutucukların Hello bilgi tıklandığında ilgili görevleri yöneteceğiniz hello ilişkili dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="bc039-131">Clicking hello information in each of these tiles will open hello associated blade where you manage related tasks.</span></span>

<span data-ttu-id="bc039-132">Merhaba Pano Hello üst kısmından:</span><span class="sxs-lookup"><span data-stu-id="bc039-132">From hello top of hello Dashboard:</span></span>

* <span data-ttu-id="bc039-133">Ayarları kullanılabilir yedekleme görevleri erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="bc039-133">Settings provides access available backup tasks.</span></span>
* <span data-ttu-id="bc039-134">Kasa yedekleme - toohello kurtarma Hizmetleri yeni dosyalar ve klasörler (veya Azure VM'ler) yedekleme yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="bc039-134">Backup - helps you back up new files and folders (or Azure VMs) toohello Recovery Services vault.</span></span>
* <span data-ttu-id="bc039-135">Bir kurtarma Hizmetleri kasası silme - artık kullanılmayan, depolama alanı toofree silin.</span><span class="sxs-lookup"><span data-stu-id="bc039-135">Delete - If a recovery services vault is no longer being used, you can delete it toofree up storage space.</span></span> <span data-ttu-id="bc039-136">Tüm korumalı sunuculardaki hello kasasından silinmiş sonra Sil yalnızca etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="bc039-136">Delete is only enabled after all protected servers have been deleted from hello vault.</span></span>

![Yedekleme Pano görevleri](./media/backup-azure-manage-windows-server/dashboard-tasks.png)

## <a name="alerts-for-backups-using-azure-backup-agent"></a><span data-ttu-id="bc039-138">Azure Yedekleme aracısı kullanarak yedeklemeler için uyarılar:</span><span class="sxs-lookup"><span data-stu-id="bc039-138">Alerts for backups using Azure backup agent:</span></span>
| <span data-ttu-id="bc039-139">Uyarı düzeyi</span><span class="sxs-lookup"><span data-stu-id="bc039-139">Alert Level</span></span> | <span data-ttu-id="bc039-140">Gönderilen uyarıları</span><span class="sxs-lookup"><span data-stu-id="bc039-140">Alerts sent</span></span> |
| --- | --- |
| <span data-ttu-id="bc039-141">Kritik</span><span class="sxs-lookup"><span data-stu-id="bc039-141">Critical</span></span> |<span data-ttu-id="bc039-142">Yedekleme hatası, Kurtarma hatası</span><span class="sxs-lookup"><span data-stu-id="bc039-142">Backup failure, recovery failure</span></span> |
| <span data-ttu-id="bc039-143">Uyarı</span><span class="sxs-lookup"><span data-stu-id="bc039-143">Warning</span></span> |<span data-ttu-id="bc039-144">Yedekleme (toocorruption sorunları daha az yüz dosyaları yedeklenmez ve bir milyondan fazla dosyalar başarıyla yedeklendi olduğunda) uyarılarla tamamlandı</span><span class="sxs-lookup"><span data-stu-id="bc039-144">Backup completed with warnings (when fewer than one hundred files are not backed up due toocorruption issues, and more than one million files are successfully backed up)</span></span> |
| <span data-ttu-id="bc039-145">Bilgilendirme</span><span class="sxs-lookup"><span data-stu-id="bc039-145">Informational</span></span> |<span data-ttu-id="bc039-146">None</span><span class="sxs-lookup"><span data-stu-id="bc039-146">None</span></span> |

## <a name="manage-backup-alerts"></a><span data-ttu-id="bc039-147">Yedekleme Uyarıları yönetme</span><span class="sxs-lookup"><span data-stu-id="bc039-147">Manage Backup alerts</span></span>
<span data-ttu-id="bc039-148">Merhaba tıklatın **yedekleme uyarıları** döşeme tooopen hello **yedekleme uyarıları** dikey uyarıları ve yönetin.</span><span class="sxs-lookup"><span data-stu-id="bc039-148">Click hello **Backup Alerts** tile tooopen hello **Backup Alerts** blade and manage alerts.</span></span>

![Yedekleme uyarıları](./media/backup-azure-manage-windows-server/manage-backup-alerts.png)

<span data-ttu-id="bc039-150">sayısı hello hello yedekleme uyarıları kutucuğu gösterir:</span><span class="sxs-lookup"><span data-stu-id="bc039-150">hello Backup Alerts tile shows you hello number of:</span></span>

* <span data-ttu-id="bc039-151">Son 24 saat içinde çözümlenmemiş kritik uyarılar</span><span class="sxs-lookup"><span data-stu-id="bc039-151">critical alerts unresolved in last 24 hours</span></span>
* <span data-ttu-id="bc039-152">Son 24 saat içinde çözümlenmemiş uyarı bildirimleri</span><span class="sxs-lookup"><span data-stu-id="bc039-152">warning alerts unresolved in last 24 hours</span></span>

<span data-ttu-id="bc039-153">Her bu bağlantıları tıklatarak alır, toohello **yedekleme uyarıları** dikey penceresinde bu uyarıların (kritik veya uyarılan) filtre uygulanmış bir görünümle.</span><span class="sxs-lookup"><span data-stu-id="bc039-153">Clicking on each of these links takes you toohello **Backup Alerts** blade with a filtered view of these alerts (critical or warning).</span></span>

<span data-ttu-id="bc039-154">Merhaba yedekleme uyarıları dikey penceresinden:</span><span class="sxs-lookup"><span data-stu-id="bc039-154">From hello Backup Alerts blade, you:</span></span>

* <span data-ttu-id="bc039-155">Uyarılarınızı ile Merhaba uygun bilgileri tooinclude seçin.</span><span class="sxs-lookup"><span data-stu-id="bc039-155">Choose hello appropriate information tooinclude with your alerts.</span></span>

    ![Sütunları seçin](./media/backup-azure-manage-windows-server/choose-alerts-colunms.png)
* <span data-ttu-id="bc039-157">Uyarıları önem derecesi, durum ve başlangıç/bitiş zamanlarını filtreleyin.</span><span class="sxs-lookup"><span data-stu-id="bc039-157">Filter alerts for severity, status and start/end times.</span></span>

    ![Filtre uyarıları](./media/backup-azure-manage-windows-server/filter-alerts.png)
* <span data-ttu-id="bc039-159">Önem derecesi, sıklığı ve alıcıların bildirimlerini yapılandırma gibi uyarıları Aç veya kapat.</span><span class="sxs-lookup"><span data-stu-id="bc039-159">Configure notifications for severity, frequency and recipients, as well as turn alerts on or off.</span></span>

    ![Filtre uyarıları](./media/backup-azure-manage-windows-server/configure-notifications.png)

<span data-ttu-id="bc039-161">Varsa **başına uyarı** hello seçilen **bildirim** sıklığı hiçbir gruplandırma veya e-postaları düşüş ortaya çıkar.</span><span class="sxs-lookup"><span data-stu-id="bc039-161">If **Per Alert** is selected as hello **Notify** frequency no grouping or reduction in emails occurs.</span></span> <span data-ttu-id="bc039-162">Her uyarı 1 bildiriminde sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="bc039-162">Every alert results in 1 notification.</span></span> <span data-ttu-id="bc039-163">Merhaba varsayılan ayar budur ve hello çözümleme e-posta ayrıca hemen gönderilir.</span><span class="sxs-lookup"><span data-stu-id="bc039-163">This is hello default setting and hello resolution email is also sent out immediately.</span></span>

<span data-ttu-id="bc039-164">Varsa **saatlik Özet** hello seçili **bildirim** çözümlenmemiş hello son bir saat oluşturulan yeni uyarılar sıklığı toohello kullanıcı olduğunu söyleyen bir e-posta gönderilir.</span><span class="sxs-lookup"><span data-stu-id="bc039-164">If **Hourly Digest** is selected as hello **Notify** frequency one email is sent toohello user telling them that there are unresolved new alerts generated in hello last hour.</span></span> <span data-ttu-id="bc039-165">Merhaba hello saat sonunda çözümleme e-posta gönderilir.</span><span class="sxs-lookup"><span data-stu-id="bc039-165">A resolution email is sent out at hello end of hello hour.</span></span>

<span data-ttu-id="bc039-166">Uyarıları önem dereceleri aşağıdaki Merhaba gönderilebilir:</span><span class="sxs-lookup"><span data-stu-id="bc039-166">Alerts can be sent for hello following severity levels:</span></span>

* <span data-ttu-id="bc039-167">Kritik</span><span class="sxs-lookup"><span data-stu-id="bc039-167">critical</span></span>
* <span data-ttu-id="bc039-168">Uyarı</span><span class="sxs-lookup"><span data-stu-id="bc039-168">warning</span></span>
* <span data-ttu-id="bc039-169">Bilgi</span><span class="sxs-lookup"><span data-stu-id="bc039-169">information</span></span>

<span data-ttu-id="bc039-170">Merhaba ile Merhaba uyarıyı devre dışı bırakmak **devre dışı bırak** hello iş ayrıntıları dikey penceresinde düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bc039-170">You inactivate hello alert with hello **inactivate** button in hello job details blade.</span></span> <span data-ttu-id="bc039-171">' I tıklattığınızda devre dışı bırak, çözümleme notları sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="bc039-171">When you click inactivate, you can provide resolution notes.</span></span>

<span data-ttu-id="bc039-172">Merhaba sütunları seçin hello hello uyarısıyla bir parçası olarak tooappear istediğiniz **sütunları seçin** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bc039-172">You choose hello columns you want tooappear as part of hello alert with hello **Choose columns** button.</span></span>

> [!NOTE]
> <span data-ttu-id="bc039-173">Merhaba gelen **ayarları** dikey penceresinde seçerek yedekleme Uyarıları yönetme **izleme ve Raporlar > Uyarı ve olayları > Yedekleme uyarıları** ve ardından **filtre** veya  **Bildirimleri Yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="bc039-173">From hello **Settings** blade, you manage backup alerts by selecting **Monitoring and Reports > Alerts and Events > Backup Alerts** and then clicking **Filter** or **Configure Notifications**.</span></span>
>
>

## <a name="manage-backup-items"></a><span data-ttu-id="bc039-174">Yedekleme öğeleri yönetme</span><span class="sxs-lookup"><span data-stu-id="bc039-174">Manage Backup items</span></span>
<span data-ttu-id="bc039-175">Şirket içi yedeklemeler yönetme hello Yönetim Portalı'nda kullanıma sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="bc039-175">Managing on-premises backups is now available in hello management portal.</span></span> <span data-ttu-id="bc039-176">Merhaba yedekleme bölümünde hello Pano hello **yedekleme öğeleri** kutucuğunda gösterilir yedekleme öğeleri hello sayısı toohello kasası korumalı.</span><span class="sxs-lookup"><span data-stu-id="bc039-176">In hello Backup section of hello dashboard, hello **Backup Items** tile shows hello number of backup items protected toohello vault.</span></span>

<span data-ttu-id="bc039-177">Tıklatın **dosya klasörleri** yedekleme öğeleri döşeme hello içinde.</span><span class="sxs-lookup"><span data-stu-id="bc039-177">Click **File-Folders** in hello Backup Items tile.</span></span>

![Yedekleme öğeleri döşeme](./media/backup-azure-manage-windows-server/backup-items-tile.png)

<span data-ttu-id="bc039-179">Merhaba yedekleme ile Merhaba dikey pencere açılır öğelere kümesi tooFile-klasörü öğesi listelenen her belirli yedekleme gördüğünüz filtre uygulayın.</span><span class="sxs-lookup"><span data-stu-id="bc039-179">hello Backup Items blade opens with hello filter set tooFile-Folder where you see each specific backup item listed.</span></span>

![Yedekleme öğeleri](./media/backup-azure-manage-windows-server/backup-item-list.png)

<span data-ttu-id="bc039-181">Belirli bir yedekleme öğesi hello listeden seçerseniz, bu öğenin temel ayrıntılarını hello bakın.</span><span class="sxs-lookup"><span data-stu-id="bc039-181">If you select a specific backup item from hello list, you see hello essential details for that item.</span></span>

> [!NOTE]
> <span data-ttu-id="bc039-182">Merhaba gelen **ayarları** dikey penceresinde, dosyaları ve klasörleri seçerek yönetme **korumalı öğeler > yedekleme öğeleri** seçilerek **dosya klasörleri** hello açılan menüsünde.</span><span class="sxs-lookup"><span data-stu-id="bc039-182">From hello **Settings** blade, you manage files and folders by selecting **Protected Items > Backup Items** and then selecting **File-Folders** from hello drop down menu.</span></span>
>
>

![Yedekleme öğeleri ayarları](./media/backup-azure-manage-windows-server/backup-files-and-folders.png)

## <a name="manage-backup-jobs"></a><span data-ttu-id="bc039-184">Yedekleme işlerini yönetme</span><span class="sxs-lookup"><span data-stu-id="bc039-184">Manage Backup jobs</span></span>
<span data-ttu-id="bc039-185">(Merhaba şirket içi sunucu tooAzure yedeklerken) şirket içi ve Azure yedeklemeleri için yedekleme işlerinin başlangıç panosunda görünür.</span><span class="sxs-lookup"><span data-stu-id="bc039-185">Backup jobs for both on-premises (when hello on-premises server is backing up tooAzure) and Azure backups are visible in hello dashboard.</span></span>

<span data-ttu-id="bc039-186">Hello hello Pano yedekleme bölümü, hello yedekleme işi kutucuğunu işleri hello sayısını gösterir:</span><span class="sxs-lookup"><span data-stu-id="bc039-186">In hello Backup section of hello dashboard, hello Backup job tile shows hello number of jobs:</span></span>

* <span data-ttu-id="bc039-187">Sürüyor</span><span class="sxs-lookup"><span data-stu-id="bc039-187">in progress</span></span>
* <span data-ttu-id="bc039-188">Hello son 24 saat başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="bc039-188">failed in hello last 24 hours.</span></span>

<span data-ttu-id="bc039-189">toomanage yedekleme işlerinizi tıklatın hello **yedekleme işleri** döşeme, hangi hello yedekleme işleri dikey penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="bc039-189">toomanage your backup jobs, click hello **Backup Jobs** tile, which opens hello Backup Jobs blade.</span></span>

![Yedekleme öğeleri ayarları](./media/backup-azure-manage-windows-server/backup-jobs.png)

<span data-ttu-id="bc039-191">Merhaba bilgi hello yedekleme işleri dikey penceresinde hello ile kullanılabilir değiştirme **sütunları seçin** hello sayfanın üst kısmındaki hello düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bc039-191">You modify hello information available in hello Backup Jobs blade with hello **Choose columns** button at hello top of hello page.</span></span>

<span data-ttu-id="bc039-192">Kullanım hello **filtre** dosyaları ve klasörleri ve Azure sanal makine yedeklemesi arasındaki düğme tooselect.</span><span class="sxs-lookup"><span data-stu-id="bc039-192">Use hello **Filter** button tooselect between Files and folders and Azure virtual machine backup.</span></span>

<span data-ttu-id="bc039-193">Yedeklediğiniz dosya ve klasörleri görmüyorsanız, tıklatın **filtre** hello üst hello sayfasının ve Seç düğmesini **dosya ve klasörleri** hello öğesi türü menüsünde.</span><span class="sxs-lookup"><span data-stu-id="bc039-193">If you don't see your backed up files and folders, click **Filter** button at hello top of hello page and select **Files and folders** from hello Item Type menu.</span></span>

> [!NOTE]
> <span data-ttu-id="bc039-194">Merhaba gelen **ayarları** dikey penceresinde seçerek yedekleme işlerini yönetme **izleme ve raporlama > işleri > yedekleme işleri** seçilerek **dosya klasörleri** hello açılır Menüyü aşağı.</span><span class="sxs-lookup"><span data-stu-id="bc039-194">From hello **Settings** blade, you manage backup jobs by selecting **Monitoring and Reports > Jobs > Backup Jobs** and then selecting **File-Folders** from hello drop down menu.</span></span>
>
>

## <a name="monitor-backup-usage"></a><span data-ttu-id="bc039-195">Yedekleme kullanımını izleme</span><span class="sxs-lookup"><span data-stu-id="bc039-195">Monitor Backup usage</span></span>
<span data-ttu-id="bc039-196">Hello hello Pano yedekleme bölümü, hello yedekleme kullanımı kutucuğu Azure'da tüketilen hello depolamayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="bc039-196">In hello Backup section of hello dashboard, hello Backup Usage tile shows hello storage consumed in Azure.</span></span> <span data-ttu-id="bc039-197">Depolama kullanım için sağlanır:</span><span class="sxs-lookup"><span data-stu-id="bc039-197">Storage usage is provided for:</span></span>

* <span data-ttu-id="bc039-198">Merhaba kasayla ilişkili bulut LRS depolama kullanımı</span><span class="sxs-lookup"><span data-stu-id="bc039-198">Cloud LRS storage usage associated with hello vault</span></span>
* <span data-ttu-id="bc039-199">Merhaba kasayla ilişkili bulut GRS depolama kullanımı</span><span class="sxs-lookup"><span data-stu-id="bc039-199">Cloud GRS storage usage associated with hello vault</span></span>

## <a name="manage-your-production-servers"></a><span data-ttu-id="bc039-200">Üretim sunucularını yönetme</span><span class="sxs-lookup"><span data-stu-id="bc039-200">Manage your production servers</span></span>
<span data-ttu-id="bc039-201">Üretim sunucularınızı toomanage tıklatın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="bc039-201">toomanage your production servers, click **Settings**.</span></span>

<span data-ttu-id="bc039-202">Altında Yönet'i **yedekleme altyapısı > üretim sunucuları**.</span><span class="sxs-lookup"><span data-stu-id="bc039-202">Under Manage click **Backup infrastructure > Production Servers**.</span></span>

<span data-ttu-id="bc039-203">Tüm kullanılabilir üretim sunucularınızın Hello üretim sunucuları dikey listeler.</span><span class="sxs-lookup"><span data-stu-id="bc039-203">hello Production Servers blade lists of all your available production servers.</span></span> <span data-ttu-id="bc039-204">Merhaba listesi tooopen hello sunucu ayrıntıları Server'da tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bc039-204">Click on a server in hello list tooopen hello server details.</span></span>

![Korumalı öğeler](./media/backup-azure-manage-windows-server/production-server-list.png)


## <a name="open-hello-azure-backup-agent"></a><span data-ttu-id="bc039-206">Açık hello Azure Yedekleme aracısı</span><span class="sxs-lookup"><span data-stu-id="bc039-206">Open hello Azure Backup agent</span></span>
<span data-ttu-id="bc039-207">Açık hello **Microsoft Azure Yedekleme aracısı** (, makinenizde arama yaparak Bul *Microsoft Azure yedekleme*).</span><span class="sxs-lookup"><span data-stu-id="bc039-207">Open hello **Microsoft Azure Backup agent** (you find it by searching your machine for *Microsoft Azure Backup*).</span></span>

![Windows Server yedeklemesini zamanlama](./media/backup-azure-manage-windows-server/snap-in-search.png)

<span data-ttu-id="bc039-209">Merhaba gelen **Eylemler** yönetim görevleri aşağıdaki hello gerçekleştirdiğiniz hello yedekleme aracısını konsolunun sağ hello bulunabilir:</span><span class="sxs-lookup"><span data-stu-id="bc039-209">From hello **Actions** available at hello right of hello backup agent console you perform hello following management tasks:</span></span>

* <span data-ttu-id="bc039-210">Sunucuyu kaydetmek</span><span class="sxs-lookup"><span data-stu-id="bc039-210">Register Server</span></span>
* <span data-ttu-id="bc039-211">Yedekleme zamanlaması</span><span class="sxs-lookup"><span data-stu-id="bc039-211">Schedule Backup</span></span>
* <span data-ttu-id="bc039-212">Şimdi Yedekle</span><span class="sxs-lookup"><span data-stu-id="bc039-212">Back Up now</span></span>
* <span data-ttu-id="bc039-213">Özelliklerini değiştir</span><span class="sxs-lookup"><span data-stu-id="bc039-213">Change Properties</span></span>

![Microsoft Azure Yedekleme aracısı konsol Eylemler](./media/backup-azure-manage-windows-server/console-actions.png)

> [!NOTE]
> <span data-ttu-id="bc039-215">çok**verileri kurtarabilirsiniz**, bkz: [geri dosyaları tooa Windows server veya Windows istemci makinesi](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="bc039-215">too**Recover Data**, see [Restore files tooa Windows server or Windows client machine](backup-azure-restore-windows-server.md).</span></span>
>
>

## <a name="modify-hello-backup-schedule"></a><span data-ttu-id="bc039-216">Merhaba yedekleme zamanlamasını Değiştir</span><span class="sxs-lookup"><span data-stu-id="bc039-216">Modify hello backup schedule</span></span>
1. <span data-ttu-id="bc039-217">Merhaba Microsoft Azure yedekleme Aracısı'nı **yedekleme zamanlaması**.</span><span class="sxs-lookup"><span data-stu-id="bc039-217">In hello Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Windows Server yedeklemesini zamanlama](./media/backup-azure-manage-windows-server/schedule-backup.png)
2. <span data-ttu-id="bc039-219">Merhaba, **yedeklemeyi Zamanlama Sihirbazı** hello bırakın **toobackup öğeler veya kez değişiklik yapma** seçeneğe ve tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="bc039-219">In hello **Schedule Backup Wizard** leave hello **Make changes toobackup items or times** option selected and click **Next**.</span></span>

    ![Windows Server yedeklemesini zamanlama](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
3. <span data-ttu-id="bc039-221">Tooadd istediğiniz veya öğelerde hello değiştirme **öğeleri seçin tooBackup** ekran tıklatın **öğeleri Ekle**.</span><span class="sxs-lookup"><span data-stu-id="bc039-221">If you want tooadd or change items, on hello **Select Items tooBackup** screen click **Add Items**.</span></span>

    <span data-ttu-id="bc039-222">Ayrıca ayarlayabilirsiniz **dışarıda bırakma ayarları** hello Sihirbazı'nda bu sayfadan.</span><span class="sxs-lookup"><span data-stu-id="bc039-222">You can also set **Exclusion Settings** from this page in hello wizard.</span></span> <span data-ttu-id="bc039-223">Dosya türlerini eklemek için hello yordamı okuma ya da tooexclude dosyaları istiyorsanız [dışarıda bırakma ayarları](#manage-exclusion-settings).</span><span class="sxs-lookup"><span data-stu-id="bc039-223">If you want tooexclude files or file types read hello procedure for adding [exclusion settings](#manage-exclusion-settings).</span></span>
4. <span data-ttu-id="bc039-224">Merhaba dosya ve tooback yedeklemek istediğiniz klasörleri seçin **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="bc039-224">Select hello files and folders you want tooback up and click **Okay**.</span></span>

    ![Windows Server yedeklemesini zamanlama](./media/backup-azure-manage-windows-server/add-items-modify.png)
5. <span data-ttu-id="bc039-226">Merhaba belirtin **yedekleme zamanlaması** tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="bc039-226">Specify hello **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="bc039-227">(En fazla günde 3 kereye) günlük veya haftalık yedeklemeler zamanlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc039-227">You can schedule daily (at a maximum of 3 times per day) or weekly backups.</span></span>

    ![Windows Server Yedekleme öğeleri](./media/backup-azure-manage-windows-server/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > <span data-ttu-id="bc039-229">Bu ayrıntılı açıklanmıştır Hello yedekleme zamanlamasını belirtme [makale](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="bc039-229">Specifying hello backup schedule is explained in detail in this [article](backup-azure-backup-cloud-as-tape.md).</span></span>
   >

6. <span data-ttu-id="bc039-230">Select hello **Bekletme İlkesi** hello yedek kopya ve tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="bc039-230">Select hello **Retention Policy** for hello backup copy and click **Next**.</span></span>

    ![Windows Server Yedekleme öğeleri](./media/backup-azure-manage-windows-server/select-retention-policy-modify.png)
7. <span data-ttu-id="bc039-232">Merhaba üzerinde **onay** ekranında hello bilgileri gözden geçir ve tıklatın **son**.</span><span class="sxs-lookup"><span data-stu-id="bc039-232">On hello **Confirmation** screen review hello information and click **Finish**.</span></span>
8. <span data-ttu-id="bc039-233">Merhaba oluşturma Hello Sihirbazı tamamlandıktan sonra **yedekleme zamanlaması**, tıklatın **Kapat**.</span><span class="sxs-lookup"><span data-stu-id="bc039-233">Once hello wizard finishes creating hello **backup schedule**, click **Close**.</span></span>

    <span data-ttu-id="bc039-234">Korumayı değiştirdikten sonra yedeklemeler giderek toohello tarafından doğru şekilde tetikleme onaylayabilirsiniz **işleri** sekmesi ve değişiklikler hello yansıtılır onaylayan yedekleme işleri.</span><span class="sxs-lookup"><span data-stu-id="bc039-234">After modifying protection, you can confirm that backups are triggering correctly by going toohello **Jobs** tab and confirming that changes are reflected in hello backup jobs.</span></span>

## <a name="enable-network-throttling"></a><span data-ttu-id="bc039-235">Ağ azaltmayı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="bc039-235">Enable Network Throttling</span></span>

<span data-ttu-id="bc039-236">veri aktarımı sırasında ağ bant genişliğinin nasıl kullanıldığını toocontrol sağlayan bir azaltma sekmesi Hello Azure Backup aracısını sağlar.</span><span class="sxs-lookup"><span data-stu-id="bc039-236">hello Azure Backup agent provides a Throttling tab which allows you toocontrol how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="bc039-237">Bu denetim verileri tooback çalışma saatlerinde gerekir, ancak diğer Internet trafiği ile Merhaba yedekleme işlemi toointerfere istiyor musunuz yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="bc039-237">This control can be helpful if you need tooback up data during work hours but do not want hello backup process toointerfere with other internet traffic.</span></span> <span data-ttu-id="bc039-238">Verilerin azaltma aktarımı yukarıya tooback uygular ve geri yükleme etkinlikleri.</span><span class="sxs-lookup"><span data-stu-id="bc039-238">Throttling of data transfer applies tooback up and restore activities.</span></span>  

<span data-ttu-id="bc039-239">tooenable azaltma:</span><span class="sxs-lookup"><span data-stu-id="bc039-239">tooenable throttling:</span></span>

1. <span data-ttu-id="bc039-240">Merhaba, **Backup Aracısı**, tıklatın **özelliklerini değiştirme**.</span><span class="sxs-lookup"><span data-stu-id="bc039-240">In hello **Backup agent**, click **Change Properties**.</span></span>
2. <span data-ttu-id="bc039-241">Merhaba üzerinde ** sekmesini azaltma, seçin **yedekleme işlemleri için Internet bant genişliği kullanımı daraltmayı etkinleştir**.</span><span class="sxs-lookup"><span data-stu-id="bc039-241">On hello **Throttling tab, select **Enable internet bandwidth usage throttling for backup operations**.</span></span>

    ![Ağ azaltma](./media/backup-azure-manage-windows-server/throttling-dialog.png)

    <span data-ttu-id="bc039-243">Azaltma etkinleştirdikten sonra sırasında yedek veri aktarımı için bant genişliği izin verilen hello belirtin **çalışma saatleri** ve **çalışılmayan saatler**.</span><span class="sxs-lookup"><span data-stu-id="bc039-243">Once you have enabled throttling, specify hello allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="bc039-244">Merhaba bant genişliği değerler 512 KB / saniye (Kbps) başlar ve too1023 megabayt (Mbps) saniyede yukarı gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc039-244">hello bandwidth values begin at 512 kilobytes per second (Kbps) and can go up too1023 megabytes per second (Mbps).</span></span> <span data-ttu-id="bc039-245">Ayrıca hello başlangıç belirleyin ve için son **çalışma saatleri**, ve hello haftanın hangi günleri iş dikkate gün.</span><span class="sxs-lookup"><span data-stu-id="bc039-245">You can also designate hello start and finish for **Work hours**, and which days of hello week are considered Work days.</span></span> <span data-ttu-id="bc039-246">Merhaba çalışma saatleri belirlenmiş hello dışında dikkate alınan toobe İş dışı saatler saattir.</span><span class="sxs-lookup"><span data-stu-id="bc039-246">hello time outside of hello designated Work hours is considered toobe non-work hours.</span></span>
3. <span data-ttu-id="bc039-247">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bc039-247">Click **OK**.</span></span>

## <a name="manage-exclusion-settings"></a><span data-ttu-id="bc039-248">Dışarıda bırakma ayarları yönetme</span><span class="sxs-lookup"><span data-stu-id="bc039-248">Manage exclusion settings</span></span>
1. <span data-ttu-id="bc039-249">Açık hello **Microsoft Azure Yedekleme aracısı** (makinenizi arayarak bulabilirsiniz *Microsoft Azure yedekleme*).</span><span class="sxs-lookup"><span data-stu-id="bc039-249">Open hello **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

    ![Windows Server yedeklemesini zamanlama](./media/backup-azure-manage-windows-server/snap-in-search.png)
2. <span data-ttu-id="bc039-251">Merhaba Microsoft Azure yedekleme Aracısı'nı **yedekleme zamanlaması**.</span><span class="sxs-lookup"><span data-stu-id="bc039-251">In hello Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Windows Server yedeklemesini zamanlama](./media/backup-azure-manage-windows-server/schedule-backup.png)
3. <span data-ttu-id="bc039-253">Merhaba yedeklemeyi Zamanlama Sihirbazı hello bırakın **toobackup öğeler veya kez değişiklik yapma** seçeneğe ve tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="bc039-253">In hello Schedule Backup Wizard leave hello **Make changes toobackup items or times** option selected and click **Next**.</span></span>

    ![Windows Server yedeklemesini zamanlama](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
4. <span data-ttu-id="bc039-255">Tıklatın **dışlama ayarları**.</span><span class="sxs-lookup"><span data-stu-id="bc039-255">Click **Exclusions Settings**.</span></span>

    ![Windows Server yedeklemesini zamanlama](./media/backup-azure-manage-windows-server/exclusion-settings.png)
5. <span data-ttu-id="bc039-257">Tıklatın **dışlama eklemek**.</span><span class="sxs-lookup"><span data-stu-id="bc039-257">Click **Add Exclusion**.</span></span>

    ![Windows Server yedeklemesini zamanlama](./media/backup-azure-manage-windows-server/add-exclusion.png)
6. <span data-ttu-id="bc039-259">Merhaba konum seçin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="bc039-259">Select hello location and then, click **OK**.</span></span>

    ![Windows Server yedeklemesini zamanlama](./media/backup-azure-manage-windows-server/exclusion-location.png)
7. <span data-ttu-id="bc039-261">Hello Hello dosya uzantısını Ekle **dosya türü** alan.</span><span class="sxs-lookup"><span data-stu-id="bc039-261">Add hello file extension in hello **File Type** field.</span></span>

    ![Windows Server yedeklemesini zamanlama](./media/backup-azure-manage-windows-server/exclude-file-type.png)

    <span data-ttu-id="bc039-263">.Mp3 uzantı ekleme</span><span class="sxs-lookup"><span data-stu-id="bc039-263">Adding an .mp3 extension</span></span>

    ![Windows Server yedeklemesini zamanlama](./media/backup-azure-manage-windows-server/exclude-mp3.png)

    <span data-ttu-id="bc039-265">tooadd başka bir uzantı tıklatın **dışlama Ekle** ve (.jpeg uzantı eklemeden) başka bir dosya türü uzantısını girin.</span><span class="sxs-lookup"><span data-stu-id="bc039-265">tooadd another extension, click **Add Exclusion** and enter another file type extension (adding a .jpeg extension).</span></span>

    ![Windows Server yedeklemesini zamanlama](./media/backup-azure-manage-windows-server/exclude-jpg.png)
8. <span data-ttu-id="bc039-267">Tüm hello uzantıları eklediğinizde, tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="bc039-267">When you've added all hello extensions, click **OK**.</span></span>
9. <span data-ttu-id="bc039-268">Yedeklemeyi zamanlama Sihirbazı Hello tıklayarak devam **sonraki** hello kadar **onay sayfası**, ardından **son**.</span><span class="sxs-lookup"><span data-stu-id="bc039-268">Continue through hello Schedule Backup Wizard by clicking **Next** until hello **Confirmation page**, then click **Finish**.</span></span>

    ![Windows Server yedeklemesini zamanlama](./media/backup-azure-manage-windows-server/finish-exclusions.png)

## <a name="frequently-asked-questions"></a><span data-ttu-id="bc039-270">Sık sorulan sorular</span><span class="sxs-lookup"><span data-stu-id="bc039-270">Frequently asked questions</span></span>
<span data-ttu-id="bc039-271">**S1. neden bunu hemen portalında yansıtılan değil hello Azure Yedekleme aracısı, tamamlandı olarak Hello yedekleme işinin durumunu gösterir?**</span><span class="sxs-lookup"><span data-stu-id="bc039-271">**Q1. hello backup job status shows as completed in hello Azure backup agent, why doesn't it get reflected immediately in portal?**</span></span>

<span data-ttu-id="bc039-272">Y1.</span><span class="sxs-lookup"><span data-stu-id="bc039-272">A1.</span></span> <span data-ttu-id="bc039-273">Var. en yüksek gecikmeye hello yedekleme işinin durumu arasında 15 dakika hello Azure Yedekleme aracısı ve hello Azure portal yansıtılır.</span><span class="sxs-lookup"><span data-stu-id="bc039-273">There is at maximum delay of 15 mins between hello backup job status reflected in hello Azure backup agent and hello Azure portal.</span></span>

<span data-ttu-id="bc039-274">**Bir yedekleme işi başarısız olduğunda Q.2 ne kadar süreyle tooraise bir uyarı sürer?**</span><span class="sxs-lookup"><span data-stu-id="bc039-274">**Q.2 When a backup job fails, how long does it take tooraise an alert?**</span></span>

<span data-ttu-id="bc039-275">A.2 bir uyarı hello Azure yedekleme hata 20 dakika içinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="bc039-275">A.2 An alert is raised within 20 mins of hello Azure backup failure.</span></span>

<span data-ttu-id="bc039-276">**S3. Bir e-posta, bildirimleri yapılandırılırsa burada gönderilmez söz konusu var mı?**</span><span class="sxs-lookup"><span data-stu-id="bc039-276">**Q3. Is there a case where an email won’t be sent if notifications are configured?**</span></span>

<span data-ttu-id="bc039-277">Y3.</span><span class="sxs-lookup"><span data-stu-id="bc039-277">A3.</span></span> <span data-ttu-id="bc039-278">Sipariş tooreduce hello aralığını belirterek uyarı sesini içinde Hello bildirim gönderilmeyecek zaman hello durumlarda aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="bc039-278">Below are hello cases when hello notification will not be sent in order tooreduce hello alert noise:</span></span>

* <span data-ttu-id="bc039-279">Bildirimleri saatlik yapılandırıldıysa ve bir uyarı oluşturulur ve hello saat içinde çözümlenen</span><span class="sxs-lookup"><span data-stu-id="bc039-279">If notifications are configured hourly and an alert is raised and resolved within hello hour</span></span>
* <span data-ttu-id="bc039-280">İşleri iptal edilir.</span><span class="sxs-lookup"><span data-stu-id="bc039-280">Job is canceled.</span></span>
* <span data-ttu-id="bc039-281">Özgün yedekleme işi devam ettiğinden ikinci yedekleme işi başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="bc039-281">Second backup job failed because original backup job is in progress.</span></span>

## <a name="troubleshooting-monitoring-issues"></a><span data-ttu-id="bc039-282">İzleme sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="bc039-282">Troubleshooting Monitoring Issues</span></span>
<span data-ttu-id="bc039-283">**Sorun:** işleri ve/veya hello Azure Yedekleme aracısı uyarıları hello Portalı'nda görünmez.</span><span class="sxs-lookup"><span data-stu-id="bc039-283">**Issue:** Jobs and/or alerts from hello Azure Backup agent do not appear in hello portal.</span></span>

<span data-ttu-id="bc039-284">**Sorun giderme adımları:** hello işlemi, ```OBRecoveryServicesManagementAgent```, iş ve uyarı verileri toohello Azure Backup hizmeti hello gönderir.</span><span class="sxs-lookup"><span data-stu-id="bc039-284">**Troubleshooting steps:** hello process, ```OBRecoveryServicesManagementAgent```, sends hello job and alert data toohello Azure Backup service.</span></span> <span data-ttu-id="bc039-285">Bu işlem bazen durumunda takılıp kalabilir veya kapatın.</span><span class="sxs-lookup"><span data-stu-id="bc039-285">Occasionally this process can become stuck or shutdown.</span></span>

1. <span data-ttu-id="bc039-286">tooverify hello işlemi çalışmıyor, açık **Görev Yöneticisi'ni** ve onay hello varsa ```OBRecoveryServicesManagementAgent``` işlem çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="bc039-286">tooverify hello process is not running, open **Task Manager** and check if hello ```OBRecoveryServicesManagementAgent``` process is running.</span></span>
2. <span data-ttu-id="bc039-287">Merhaba işlemi çalışmıyor varsayılarak açmak **Denetim Masası** ve hizmetlerin listesini hello göz atın.</span><span class="sxs-lookup"><span data-stu-id="bc039-287">Assuming that hello process is not running, open **Control Panel** and browse hello list of services.</span></span> <span data-ttu-id="bc039-288">Başlatma veya yeniden **Microsoft Azure kurtarma Hizmetleri yönetim Aracısı**.</span><span class="sxs-lookup"><span data-stu-id="bc039-288">Start or restart **Microsoft Azure Recovery Services Management Agent**.</span></span>

    <span data-ttu-id="bc039-289">Daha fazla bilgi için hello günlüklerine göz atın:</span><span class="sxs-lookup"><span data-stu-id="bc039-289">For further information, browse hello logs at:</span></span><br/><span data-ttu-id="bc039-290">
   `<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*`Örneğin:</span><span class="sxs-lookup"><span data-stu-id="bc039-290">
   `<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*` For example:</span></span><br/>
   `C:\Program Files\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider0.errlog`

## <a name="next-steps"></a><span data-ttu-id="bc039-291">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bc039-291">Next steps</span></span>
* [<span data-ttu-id="bc039-292">Windows Server veya Windows İstemcisi Azure'dan geri yükleme</span><span class="sxs-lookup"><span data-stu-id="bc039-292">Restore Windows Server or Windows Client from Azure</span></span>](backup-azure-restore-windows-server.md)
* <span data-ttu-id="bc039-293">Azure yedekleme hakkında daha fazla toolearn bakın [Azure Yedekleme'ye Genel Bakış](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="bc039-293">toolearn more about Azure Backup, see [Azure Backup Overview](backup-introduction-to-azure-backup.md)</span></span>
* <span data-ttu-id="bc039-294">Merhaba ziyaret [Azure yedekleme Forumu](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span><span class="sxs-lookup"><span data-stu-id="bc039-294">Visit hello [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span></span>
