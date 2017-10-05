---
title: "Azure veri geri bir Windows Server veya Windows bilgisayarı | Microsoft Docs"
description: "Windows Server veya Windows bilgisayarı Azure'a depolanan veri geri yüklemeyi öğrenin."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 742f4b9e-c0ab-4eeb-8e22-ee29b83c22c4
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/16/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: 231dd61f95267b3a504ed70e9b3a5abc470b69b2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="restore-files-to-a-windows-server-or-windows-client-machine-using-resource-manager-deployment-model"></a><span data-ttu-id="384be-103">Resource Manager dağıtım modelini kullanarak bir Windows sunucusu veya Windows istemci makinesine dosyaları geri yükleme</span><span class="sxs-lookup"><span data-stu-id="384be-103">Restore files to a Windows server or Windows client machine using Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="384be-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="384be-104">Azure portal</span></span>](backup-azure-restore-windows-server.md)
> * [<span data-ttu-id="384be-105">Klasik portal</span><span class="sxs-lookup"><span data-stu-id="384be-105">Classic portal</span></span>](backup-azure-restore-windows-server-classic.md)
>
>

<span data-ttu-id="384be-106">Bu makalede, verileri bir yedekleme Kasası'nı geri yüklemek açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="384be-106">This article explains how to restore data from a backup vault.</span></span> <span data-ttu-id="384be-107">Verileri geri yüklemek için Microsoft Azure kurtarma Hizmetleri (MARS) aracısı Veri Kurtarma Sihirbazı'nı kullanın.</span><span class="sxs-lookup"><span data-stu-id="384be-107">To restore data, you use the Recover Data wizard in the Microsoft Azure Recovery Services (MARS) agent.</span></span> <span data-ttu-id="384be-108">Verileri geri yüklediğinizde, mümkün olur:</span><span class="sxs-lookup"><span data-stu-id="384be-108">When you restore data, it is possible to:</span></span>

* <span data-ttu-id="384be-109">Veri yedekleri gerçekleştirilecek aynı makineye geri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="384be-109">Restore data to the same machine from which the backups were taken.</span></span>
* <span data-ttu-id="384be-110">Verileri başka bir makineye geri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="384be-110">Restore data to an alternate machine.</span></span>

<span data-ttu-id="384be-111">Ocak 2017 ' Microsoft MARS aracısı için Önizleme güncelleştirme yayımladı.</span><span class="sxs-lookup"><span data-stu-id="384be-111">In January 2017, Microsoft released a Preview update to the MARS agent.</span></span> <span data-ttu-id="384be-112">Hata düzeltmeleri yanı sıra, bu güncelleştirme, anlık yazılabilir kurtarma noktası anlık görüntü kurtarma birimi olarak bağlamak izin veren geri yükleme sağlar.</span><span class="sxs-lookup"><span data-stu-id="384be-112">Along with bug fixes, this update enables Instant Restore, which allows you to mount a writeable recovery point snapshot as a recovery volume.</span></span> <span data-ttu-id="384be-113">Ardından böylece seçerek dosyaları geri yükleme yerel bir bilgisayara kurtarma birimi ve kopyalama dosyalarını gözden geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="384be-113">You can then explore the recovery volume and copy files to a local computer thereby selectively restoring files.</span></span>

> [!NOTE]
> <span data-ttu-id="384be-114">[Ocak 2017 Azure Backup güncelleştirmesini](https://support.microsoft.com/en-us/help/3216528?preview) anlık geri verileri geri yüklemek için kullanmak istiyorsanız gereklidir.</span><span class="sxs-lookup"><span data-stu-id="384be-114">The [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) is required if you want to use Instant Restore to restore data.</span></span> <span data-ttu-id="384be-115">Ayrıca Yedekleme verileri yerel destek makalesinde listelenen kasalarında korunmalıdır.</span><span class="sxs-lookup"><span data-stu-id="384be-115">Also the backup data must be protected in vaults in locales listed in the support article.</span></span> <span data-ttu-id="384be-116">Başvurun [Ocak 2017 Azure Backup güncelleştirmesini](https://support.microsoft.com/en-us/help/3216528?preview) anlık geri yükleme desteği yerel ayarları en son listesi için.</span><span class="sxs-lookup"><span data-stu-id="384be-116">Consult the [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) for the latest list of locales that support Instant Restore.</span></span> <span data-ttu-id="384be-117">Anlık geri yükleme **değil** tüm bölgelerde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="384be-117">Instant Restore is **not** currently available in all locales.</span></span>
>

<span data-ttu-id="384be-118">Anlık geri yükleme Azure portal ve klasik portalda yedekleme kasaları kurtarma Hizmetleri kasalarının kullanmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="384be-118">Instant Restore is available for use in Recovery Services vaults in the Azure portal and Backup vaults in the classic portal.</span></span> <span data-ttu-id="384be-119">Anlık geri kullanmak istiyorsanız, MARS güncelleştirmeyi indirin ve anlık geri Bahsediyor yordamları izleyin.</span><span class="sxs-lookup"><span data-stu-id="384be-119">If you want to use Instant Restore, download the MARS update, and follow the procedures that mention Instant Restore.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="use-instant-restore-to-recover-data-to-the-same-machine"></a><span data-ttu-id="384be-120">Anlık aynı makineye verileri kurtarmak için geri yükleme kullanın</span><span class="sxs-lookup"><span data-stu-id="384be-120">Use Instant Restore to recover data to the same machine</span></span>

<span data-ttu-id="384be-121">Yanlışlıkla silinen bir dosya ve (yedeğin alındığı) aynı makineye geri yüklemek istiyorsanız, aşağıdaki adımları verileri kurtarmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="384be-121">If you accidentally deleted a file and wish to restore it to the same machine (from which the backup is taken), the following steps will help you recover the data.</span></span>

1. <span data-ttu-id="384be-122">Açık **Microsoft Azure yedekleme** içinde Vurgu.</span><span class="sxs-lookup"><span data-stu-id="384be-122">Open the **Microsoft Azure Backup** snap in.</span></span> <span data-ttu-id="384be-123">Ek bileşeninde yüklendiği bilmiyorsanız, bilgisayar veya sunucu için arama **Microsoft Azure yedekleme**.</span><span class="sxs-lookup"><span data-stu-id="384be-123">If you don't know where the snap in was installed, search the computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="384be-124">Masaüstü uygulaması arama sonuçlarında görüntülenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="384be-124">The desktop app should appear in the search results.</span></span>

2. <span data-ttu-id="384be-125">Tıklatın **verileri kurtarabilirsiniz** Sihirbazı'nı başlatın.</span><span class="sxs-lookup"><span data-stu-id="384be-125">Click **Recover Data** to start the wizard.</span></span>

    ![Verileri kurtarma](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="384be-127">Üzerinde **Başlarken** verileri aynı sunucu veya bilgisayara geri yüklemek için bölmeyi seçin **bu sunucunun (`<server name>`)** tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="384be-127">On the **Getting Started** pane, to restore the data to the same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![Bu sunucu seçeneği aynı makineye verileri geri yüklemek için](./media/backup-azure-restore-windows-server/samemachine_gettingstarted_instantrestore.png)

4. <span data-ttu-id="384be-129">Üzerinde **seçin kurtarma moduna** bölmesinde seçin **dosyalara ve klasörlere** ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="384be-129">On the **Select Recovery Mode** pane, choose **Individual files and folders** and then click **Next**.</span></span>

    ![Gözatma dosyaları](./media/backup-azure-restore-windows-server/samemachine_selectrecoverymode_instantrestore.png)

5. <span data-ttu-id="384be-131">Üzerinde **birim seçin ve tarih** bölmesinde, dosyaları ve/veya geri yüklemek istediğiniz klasörleri içeren bir birimi seçin.</span><span class="sxs-lookup"><span data-stu-id="384be-131">On the **Select Volume and Date** pane, select the volume that contains the files and/or folders you want to restore.</span></span>

    <span data-ttu-id="384be-132">Takvimde bir kurtarma noktası seçin.</span><span class="sxs-lookup"><span data-stu-id="384be-132">On the calendar, select a recovery point.</span></span> <span data-ttu-id="384be-133">Zaman içinde herhangi bir kurtarma noktasından geri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="384be-133">You can restore from any recovery point in time.</span></span> <span data-ttu-id="384be-134">İçinde tarihleri **kalın** en az bir kurtarma noktası kullanılabilirliğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="384be-134">Dates in **bold** indicate the availability of at least one recovery point.</span></span> <span data-ttu-id="384be-135">Birden fazla kurtarma noktası mevcutsa, bir tarih seçtikten sonra belirli bir kurtarma noktasından seçin **zaman** açılır menü.</span><span class="sxs-lookup"><span data-stu-id="384be-135">Once you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span></span>

    ![Birimi ve tarih](./media/backup-azure-restore-windows-server/samemachine_selectvolumedate_instantrestore.png)

6. <span data-ttu-id="384be-137">Geri yüklemek için kurtarma noktası seçtikten sonra tıklatın **bağlama**.</span><span class="sxs-lookup"><span data-stu-id="384be-137">Once you have chosen the recovery point to restore, click **Mount**.</span></span>

    <span data-ttu-id="384be-138">Azure yedekleme, yerel kurtarma noktası bağlar ve kurtarma birimi olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="384be-138">Azure Backup mounts the local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="384be-139">Üzerinde **Gözat ve kurtarma dosyaları** bölmesinde tıklatın **Gözat** Windows Gezgini'ni açın ve istediğiniz klasörleri ve dosyaları bulmak için.</span><span class="sxs-lookup"><span data-stu-id="384be-139">On the **Browse and Recover Files** pane, click **Browse** to open Windows Explorer and find the files and folders you want.</span></span>

    ![Kurtarma Seçenekleri](./media/backup-azure-restore-windows-server/samemachine_browserecover_instantrestore.png)


8. <span data-ttu-id="384be-141">Windows Gezgini'nde, dosyaları ve/veya geri yükleme ve sunucu veya bilgisayar için yerel herhangi bir konuma yapıştırmak için istediğiniz klasörleri kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="384be-141">In Windows Explorer, copy the files and/or folders you want to restore and paste them to any location local to the server or computer.</span></span> <span data-ttu-id="384be-142">Açın veya kurtarma birimi dosyalarından doğrudan akış ve doğru sürümlerini kurtarılan doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="384be-142">You can open or stream the files directly from the recovery volume and verify the correct versions are recovered.</span></span>

    ![Dosyaları ve takılı birim klasörlerinden yerel bir konuma kopyalama ve yapıştırma](./media/backup-azure-restore-windows-server/samemachine_copy_instantrestore.png)

9. <span data-ttu-id="384be-144">Dosyaları ve/veya klasörleri üzerinde geri yüklemeyi tamamladıktan sonra **göz atın ve kurtarma dosyaları** bölmesinde tıklatın **çıkarma**.</span><span class="sxs-lookup"><span data-stu-id="384be-144">When you are finished restoring the files and/or folders, on the **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="384be-145">Ardından **Evet** birim kaldırmak istediğinizi onaylamak için.</span><span class="sxs-lookup"><span data-stu-id="384be-145">Then click **Yes** to confirm that you want to unmount the volume.</span></span>

    ![Birim çıkarın ve onaylayın](./media/backup-azure-restore-windows-server/samemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="384be-147">Çıkarma değil tıklatırsanız, Kurtarma birimi zaman takıldı zamandan 6 saat boyunca bağlı kalır.</span><span class="sxs-lookup"><span data-stu-id="384be-147">If you do not click Unmount, the Recovery Volume will remain mounted for 6 hours from the time when it was mounted.</span></span> <span data-ttu-id="384be-148">Ancak, bağlama genişletilmiş değerine kadar devam eden bir dosya kopyalama durumunda 24 saat maksimum saattir.</span><span class="sxs-lookup"><span data-stu-id="384be-148">However, the mount time is extended upto a maximum of 24 hours in case of an ongoing file-copy.</span></span> <span data-ttu-id="384be-149">Birim bağlıyken hiçbir yedekleme işlemleri çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="384be-149">No backup operations will run while the volume is mounted.</span></span> <span data-ttu-id="384be-150">Birimin zaman bağlı, süre içinde çalıştırılmak üzere zamanlanmış herhangi bir yedekleme işlemi kurtarma birimi kaldırılan sonra çalışır.</span><span class="sxs-lookup"><span data-stu-id="384be-150">Any backup operation scheduled to run during the time when the volume is mounted, will run after the recovery volume is unmounted.</span></span>
    >


## <a name="use-instant-restore-to-restore-data-to-an-alternate-machine"></a><span data-ttu-id="384be-151">Verileri başka bir makineye geri yüklemek için anlık geri kullanın</span><span class="sxs-lookup"><span data-stu-id="384be-151">Use Instant Restore to restore data to an alternate machine</span></span>
<span data-ttu-id="384be-152">Tüm sunucunuzu kaybolursa, verileri Azure yedekten başka bir makine kurtarmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="384be-152">If your entire server is lost, you can still recover data from Azure Backup to a different machine.</span></span> <span data-ttu-id="384be-153">Aşağıdaki adımlar, iş akışı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="384be-153">The following steps illustrate the workflow.</span></span>


<span data-ttu-id="384be-154">Bu adımlarda kullanılan terminolojiyi içerir:</span><span class="sxs-lookup"><span data-stu-id="384be-154">The terminology used in these steps includes:</span></span>

* <span data-ttu-id="384be-155">*Kaynak makine* – özgün makineden yedeğin alındığı ve hangi şu anda kullanılamıyor.</span><span class="sxs-lookup"><span data-stu-id="384be-155">*Source machine* – The original machine from which the backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="384be-156">*Hedef makine* – olduğu verilerin kurtarıldığı makine.</span><span class="sxs-lookup"><span data-stu-id="384be-156">*Target machine* – The machine to which the data is being recovered.</span></span>
* <span data-ttu-id="384be-157">*Örnek kasa* – kurtarma Hizmetleri kasası için *kaynak makine* ve *hedef makine* kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="384be-157">*Sample vault* – The Recovery Services vault to which the *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="384be-158">Yedeklemeleri işletim sisteminin önceki bir sürümünü çalıştıran bir hedef bilgisayara geri yüklenemez.</span><span class="sxs-lookup"><span data-stu-id="384be-158">Backups can't be restored to a target machine running an earlier version of the operating system.</span></span> <span data-ttu-id="384be-159">Örneğin, bir Windows bilgisayarı olabilir 7'den alınan bir yedeklemeyi bilgisayar bir Windows 8 veya daha sonra geri.</span><span class="sxs-lookup"><span data-stu-id="384be-159">For example, a backup taken from a Windows 7 computer can be restored on a Windows 8, or later, computer.</span></span> <span data-ttu-id="384be-160">Windows 7 bilgisayara Windows 8 bilgisayardan alınan bir yedeklemeyi geri yüklenemiyor.</span><span class="sxs-lookup"><span data-stu-id="384be-160">A backup taken from a Windows 8 computer cannot be restored to a Windows 7 computer.</span></span>
>
>

1. <span data-ttu-id="384be-161">Açık **Microsoft Azure yedekleme** üzerinde içinde Vurgu *hedef makine*.</span><span class="sxs-lookup"><span data-stu-id="384be-161">Open the **Microsoft Azure Backup** snap in on the *Target machine*.</span></span>

2. <span data-ttu-id="384be-162">Olun *hedef makine* ve *kaynak makine* aynı kurtarma Hizmetleri kasasına kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="384be-162">Ensure the *Target machine* and the *Source machine* are registered to the same Recovery Services vault.</span></span>

3. <span data-ttu-id="384be-163">Tıklatın **verileri kurtarabilirsiniz** açmak için **Veri Kurtarma Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="384be-163">Click **Recover Data** to open the **Recover Data wizard**.</span></span>

    ![Verileri kurtarma](./media/backup-azure-restore-windows-server/recover.png)

4. <span data-ttu-id="384be-165">Üzerinde **Başlarken** bölmesinde, **başka bir sunucu**</span><span class="sxs-lookup"><span data-stu-id="384be-165">On the **Getting Started** pane, select **Another server**</span></span>

    ![Başka bir sunucu](./media/backup-azure-restore-windows-server/alternatemachine_gettingstarted_instantrestore.png)

5. <span data-ttu-id="384be-167">Karşılık gelen kasa kimlik bilgilerini sağlayın *örnek kasa*, tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="384be-167">Provide the vault credential file that corresponds to the *Sample vault*, and click **Next**.</span></span>

    <span data-ttu-id="384be-168">Kasa kimlik bilgilerini geçersiz (veya süresi dolmuş) varsa, yeni bir kasa kimlik bilgileri dosyasını indirin *örnek kasa* Azure portalında.</span><span class="sxs-lookup"><span data-stu-id="384be-168">If the vault credential file is invalid (or expired), download a new vault credential file from the *Sample vault* in the Azure portal.</span></span> <span data-ttu-id="384be-169">Geçerli kasa kimlik bilgileri sağladığınızda, ilgili yedekleme kasasının adını görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="384be-169">Once you provide a valid vault credential, the name of the corresponding Backup Vault appears.</span></span>


6. <span data-ttu-id="384be-170">Üzerinde **yedekleme sunucusu seçin** bölmesinde, select *kaynak makine* görüntülenmesini makineler listesinden ve parola girin.</span><span class="sxs-lookup"><span data-stu-id="384be-170">On the **Select Backup Server** pane, select the *Source machine* from the list of displayed machines and provide the passphrase.</span></span> <span data-ttu-id="384be-171">Ardından **İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="384be-171">Then click **Next**.</span></span>

    ![Makineler listesi](./media/backup-azure-restore-windows-server/alternatemachine_selectmachine_instantrestore.png)

7. <span data-ttu-id="384be-173">Üzerinde **seçin kurtarma moduna** bölmesinde seçin **dosyalara ve klasörlere** tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="384be-173">On the **Select Recovery Mode** pane, select **Individual files and folders** and click **Next**.</span></span>

    ![Arama](./media/backup-azure-restore-windows-server/alternatemachine_selectrecoverymode_instantrestore.png)

8. <span data-ttu-id="384be-175">Üzerinde **birim seçin ve tarih** bölmesinde, dosyaları ve/veya geri yüklemek istediğiniz klasörleri içeren bir birimi seçin.</span><span class="sxs-lookup"><span data-stu-id="384be-175">On the **Select Volume and Date** pane, select the volume that contains the files and/or folders you want to restore.</span></span>

    <span data-ttu-id="384be-176">Takvimde bir kurtarma noktası seçin.</span><span class="sxs-lookup"><span data-stu-id="384be-176">On the calendar, select a recovery point.</span></span> <span data-ttu-id="384be-177">Zaman içinde herhangi bir kurtarma noktasından geri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="384be-177">You can restore from any recovery point in time.</span></span> <span data-ttu-id="384be-178">İçinde tarihleri **kalın** en az bir kurtarma noktası kullanılabilirliğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="384be-178">Dates in **bold** indicate the availability of at least one recovery point.</span></span> <span data-ttu-id="384be-179">Birden fazla kurtarma noktası mevcutsa, bir tarih seçtikten sonra belirli bir kurtarma noktasından seçin **zaman** açılır menü.</span><span class="sxs-lookup"><span data-stu-id="384be-179">Once you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span></span>

    ![Arama öğeleri](./media/backup-azure-restore-windows-server/alternatemachine_selectvolumedate_instantrestore.png)

9. <span data-ttu-id="384be-181">Tıklatın **bağlama** kurtarma birimi olarak kurtarma noktası üzerinde yerel olarak bağlamak için *hedef makine*.</span><span class="sxs-lookup"><span data-stu-id="384be-181">Click **Mount** to locally mount the recovery point as a recovery volume on your *Target machine*.</span></span>

10. <span data-ttu-id="384be-182">Üzerinde **Gözat ve kurtarma dosyaları** bölmesinde tıklatın **Gözat** Windows Gezgini'ni açın ve istediğiniz klasörleri ve dosyaları bulmak için.</span><span class="sxs-lookup"><span data-stu-id="384be-182">On the **Browse and Recover Files** pane, click **Browse** to open Windows Explorer and find the files and folders you want.</span></span>

    ![Şifreleme](./media/backup-azure-restore-windows-server/alternatemachine_browserecover_instantrestore.png)

11. <span data-ttu-id="384be-184">Windows Gezgini'nde, dosyaları ve/veya klasörleri kurtarma birimden kopyalayıp onlara, *hedef makine* konumu.</span><span class="sxs-lookup"><span data-stu-id="384be-184">In Windows Explorer, copy the files and/or folders from the recovery volume and paste them to your *Target machine* location.</span></span> <span data-ttu-id="384be-185">Açın veya kurtarma birimi dosyalarından doğrudan akış ve doğru sürümlerini kurtarılan doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="384be-185">You can open or stream the files directly from the recovery volume and verify the correct versions are recovered.</span></span>

    ![Şifreleme](./media/backup-azure-restore-windows-server/alternatemachine_copy_instantrestore.png)

12. <span data-ttu-id="384be-187">Dosyaları ve/veya klasörleri üzerinde geri yüklemeyi tamamladıktan sonra **göz atın ve kurtarma dosyaları** bölmesinde tıklatın **çıkarma**.</span><span class="sxs-lookup"><span data-stu-id="384be-187">When you are finished restoring the files and/or folders, on the **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="384be-188">Ardından **Evet** birim kaldırmak istediğinizi onaylamak için.</span><span class="sxs-lookup"><span data-stu-id="384be-188">Then click **Yes** to confirm that you want to unmount the volume.</span></span>

    ![Şifreleme](./media/backup-azure-restore-windows-server/alternatemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="384be-190">Çıkarma değil tıklatırsanız, Kurtarma birimi zaman takıldı zamandan 6 saat boyunca bağlı kalır.</span><span class="sxs-lookup"><span data-stu-id="384be-190">If you do not click Unmount, the Recovery Volume will remain mounted for 6 hours from the time when it was mounted.</span></span> <span data-ttu-id="384be-191">Ancak, bağlama genişletilmiş değerine kadar devam eden bir dosya kopyalama durumunda 24 saat maksimum saattir.</span><span class="sxs-lookup"><span data-stu-id="384be-191">However, the mount time is extended upto a maximum of 24 hours in case of an ongoing file-copy.</span></span> <span data-ttu-id="384be-192">Birim bağlıyken hiçbir yedekleme işlemleri çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="384be-192">No backup operations will run while the volume is mounted.</span></span> <span data-ttu-id="384be-193">Birimin zaman bağlı, süre içinde çalıştırılmak üzere zamanlanmış herhangi bir yedekleme işlemi kurtarma birimi kaldırılan sonra çalışır.</span><span class="sxs-lookup"><span data-stu-id="384be-193">Any backup operation scheduled to run during the time when the volume is mounted, will run after the recovery volume is unmounted.</span></span>
    >

## <a name="troubleshooting"></a><span data-ttu-id="384be-194">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="384be-194">Troubleshooting</span></span>
<span data-ttu-id="384be-195">Azure yedekleme kurtarma birimi başarıyla tıklama bile birkaç dakika sonra bağlamaz varsa **bağlama** veya kurtarma birim bir veya daha fazla hata ile başarısız normalde kurtarma başlamak için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="384be-195">If Azure Backup does not successfully mount the recovery volume even after several minutes of clicking **Mount** or fails to mount the recovery volume with one or more errors, follow the steps below to begin recovering normally.</span></span>

1.  <span data-ttu-id="384be-196">Birkaç dakika çalışıyor durumda devam eden bağlama işlemi iptal edin.</span><span class="sxs-lookup"><span data-stu-id="384be-196">Cancel the ongoing mount process in case it has been running for several minutes.</span></span>

2.  <span data-ttu-id="384be-197">Azure yedekleme Aracısı'nın en son sürümde olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="384be-197">Ensure that you are on the latest version of the Azure Backup agent.</span></span> <span data-ttu-id="384be-198">Azure yedekleme Aracısı'nın sürüm bilgileri bulmak için tıklayın **hakkında Microsoft Azure kurtarma Hizmetleri Aracısı** üzerinde **Eylemler** Microsoft Azure yedekleme bölmesinde konsol ve emin**Sürüm** sayıdır eşit veya belirtilen sürümden daha yüksek [bu makalede](https://go.microsoft.com/fwlink/?linkid=229525).</span><span class="sxs-lookup"><span data-stu-id="384be-198">To find out the version information of Azure Backup agent, click on **About Microsoft Azure Recovery Services Agent** on the **Actions** pane of Microsoft Azure Backup console and ensure that the **Version** number is equal to or higher than the version mentioned in [this article](https://go.microsoft.com/fwlink/?linkid=229525).</span></span> <span data-ttu-id="384be-199">En son sürümü karşıdan [burada](https://go.microsoft.com/fwLink/?LinkID=288905)</span><span class="sxs-lookup"><span data-stu-id="384be-199">You can download the latest version from [here](https://go.microsoft.com/fwLink/?LinkID=288905)</span></span>

3.  <span data-ttu-id="384be-200">Git **Aygıt Yöneticisi'ni** -> **depolama alanı denetleyicileri** ve, bulabilmesini sağlama **Microsoft iSCSI başlatıcısı**.</span><span class="sxs-lookup"><span data-stu-id="384be-200">Go to **Device Manager** -> **Storage Controllers** and ensure that you can locate **Microsoft iSCSI Initiator**.</span></span> <span data-ttu-id="384be-201">Bulabiliyorsa, doğrudan adım 7'ye gidin.</span><span class="sxs-lookup"><span data-stu-id="384be-201">If you can locate it, directly go to step 7 below.</span></span> 

4.  <span data-ttu-id="384be-202">Adım 3'te belirtildiği gibi Microsoft iSCSI başlatıcısı hizmetinin bulamazsanız, altında bir giriş bulursanız denetleyin **Aygıt Yöneticisi'ni** -> **depolama alanı denetleyicileri** adlı  **Bilinmeyen aygıt** donanım kimliği ile **ROOT\ISCSIPRT**.</span><span class="sxs-lookup"><span data-stu-id="384be-202">If you cannot locate Microsoft iSCSI Initiator service as mentioned in step 3, check to see if you can find an entry under **Device Manager** -> **Storage Controllers** called **Unknown Device** with Hardware ID **ROOT\ISCSIPRT**.</span></span>

5.  <span data-ttu-id="384be-203">Sağ tıklayın **bilinmeyen aygıt** seçip **sürücü yazılımı güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="384be-203">Right click on **Unknown Device** and select **Update Driver Software**.</span></span>

6.  <span data-ttu-id="384be-204">Seçeneğini seçerek sürücüsünü güncelleştirmek **otomatik olarak güncelleştirilen sürücü yazılım Ara**.</span><span class="sxs-lookup"><span data-stu-id="384be-204">Update the driver by selecting the option to  **Search automatically for updated driver software**.</span></span> <span data-ttu-id="384be-205">Güncelleştirmenin tamamlanması değiştirme **bilinmeyen aygıt** için **Microsoft iSCSI başlatıcısı** aşağıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="384be-205">Completion of the update should change **Unknown Device** to **Microsoft iSCSI Initiator** as shown below.</span></span> 

    ![Şifreleme](./media/backup-azure-restore-windows-server/UnknowniSCSIDevice.png)

7.  <span data-ttu-id="384be-207">Git **Görev Yöneticisi'ni** -> **hizmetler (yerel)** -> **Microsoft iSCSI başlatıcısı hizmetini**.</span><span class="sxs-lookup"><span data-stu-id="384be-207">Go to **Task Manager** -> **Services (Local)** -> **Microsoft iSCSI Initiator Service**.</span></span> 

    ![Şifreleme](./media/backup-azure-restore-windows-server/MicrosoftInitiatorServiceRunning.png)
    
8.  <span data-ttu-id="384be-209">Hizmette tıklayarak sağ tıklayarak Microsoft iSCSI başlatıcısı hizmetini yeniden **durdurmak** ve sağ yeniden tıklatıp tıklayarak daha fazla **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="384be-209">Restart the Microsoft iSCSI Initiator service by right-clicking on the service, clicking on **Stop** and further right clicking again and clicking on **Start**.</span></span>

9.  <span data-ttu-id="384be-210">Anlık geri yükleme özelliğini kullanarak kurtarma yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="384be-210">Retry recovering using Instant Restore.</span></span> 

<span data-ttu-id="384be-211">Kurtarma yine başarısız olursa, sunucu/istemci yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="384be-211">If the recovery still fails, reboot your server/client.</span></span> <span data-ttu-id="384be-212">Yeniden başlatma arzu değil veya bile sunucunun yeniden başlatmanın ardından Kurtarma yine başarısız olursa, alternatif bir makineden kurtarmayı deneyin ve giderek Azure desteği ile iletişim kurun [Azure Portal](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) ve bir destek isteği gönderiliyor.</span><span class="sxs-lookup"><span data-stu-id="384be-212">If a reboot is not desirable or the recovery still fails even after rebooting the server, try recovering from an Alternate Machine, and contact Azure Support by going to [Azure Portal](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) and submitting a support request.</span></span>

## <a name="next-steps"></a><span data-ttu-id="384be-213">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="384be-213">Next steps</span></span>
* <span data-ttu-id="384be-214">Dosya ve klasörleri kurtarma yaptıktan, yapabilecekleriniz [Yedeklemelerinizin yönetmek](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="384be-214">Now that you've recovered your files and folders, you can [manage your backups](backup-azure-manage-windows-server.md).</span></span>
