---
title: "Azure kullanarak aaaRestore veri tooa Windows Server veya Windows İstemcisi hello Klasik dağıtım modeli | Microsoft Docs"
description: "Bilgi nasıl toorestore bir Windows Server veya Windows İstemcisi."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 85585dfc-c764-4e8c-8f0e-40b969640ac2
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: 4d1458d5233c4f55004ecfa95cbf7b3b18a03dde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-files-tooa-windows-server-or-windows-client-machine-using-hello-classic-deployment-model"></a><span data-ttu-id="24e8e-103">Dosyaları tooa Windows server veya Windows istemci makinesi hello Klasik dağıtım modeli kullanılarak geri yükleme</span><span class="sxs-lookup"><span data-stu-id="24e8e-103">Restore files tooa Windows server or Windows client machine using hello classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="24e8e-104">Klasik portal</span><span class="sxs-lookup"><span data-stu-id="24e8e-104">Classic portal</span></span>](backup-azure-restore-windows-server-classic.md)
> * [<span data-ttu-id="24e8e-105">Azure portal</span><span class="sxs-lookup"><span data-stu-id="24e8e-105">Azure portal</span></span>](backup-azure-restore-windows-server.md)
>
>

<span data-ttu-id="24e8e-106">Bu makalede, bir yedekten toorecover verinin nasıl kasa ve tooa sunucu veya bilgisayar geri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="24e8e-106">This article explains how toorecover data from a backup vault and restore it tooa server or computer.</span></span> <span data-ttu-id="24e8e-107">Mart 2017'dan başlayarak, hello Klasik portalda yedekleme kasaları artık oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24e8e-107">Starting in March 2017, you can no longer create backup vaults in hello classic portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="24e8e-108">Şimdi, yedekleme kasaları tooRecovery Hizmetleri kasaları yükseltebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24e8e-108">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="24e8e-109">Ayrıntılar için hello makalesine bakın [kurtarma Hizmetleri kasası bir yedekleme kasası tooa yükseltme](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="24e8e-109">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="24e8e-110">Microsoft tooupgrade önerir tooRecovery Hizmetleri kasalarının yedekleme kasaları.</span><span class="sxs-lookup"><span data-stu-id="24e8e-110">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="24e8e-111">**15 Ekim 2017**, artık mümkün toouse PowerShell toocreate yedekleme kasaları olacaktır.</span><span class="sxs-lookup"><span data-stu-id="24e8e-111">**October 15, 2017**, you will no longer be able toouse PowerShell toocreate Backup vaults.</span></span> <br/> <span data-ttu-id="24e8e-112">**1 Kasım 2017'den itibaren**:</span><span class="sxs-lookup"><span data-stu-id="24e8e-112">**Starting November 1, 2017**:</span></span>
>- <span data-ttu-id="24e8e-113">Kalan tüm yedekleme kasaları otomatik olarak yükseltilen tooRecovery Hizmetleri kasalarının olacaktır.</span><span class="sxs-lookup"><span data-stu-id="24e8e-113">Any remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="24e8e-114">Mümkün tooaccess hello Klasik Portalı'nda, yedekleme verilerinizi olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="24e8e-114">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="24e8e-115">Bunun yerine, hello Azure portal tooaccess kurtarma Hizmetleri kasalarının, yedekleme verilerinizi kullanın.</span><span class="sxs-lookup"><span data-stu-id="24e8e-115">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

<span data-ttu-id="24e8e-116">toorestore veri hello Microsoft Azure kurtarma Hizmetleri (MARS) aracısı hello Veri Kurtarma Sihirbazı'nı kullanın.</span><span class="sxs-lookup"><span data-stu-id="24e8e-116">toorestore data, you use hello Recover Data wizard in hello Microsoft Azure Recovery Services (MARS) agent.</span></span> <span data-ttu-id="24e8e-117">Verileri geri yüklediğinizde, mümkün olur:</span><span class="sxs-lookup"><span data-stu-id="24e8e-117">When you restore data, it is possible to:</span></span>

* <span data-ttu-id="24e8e-118">Aynı makine hangi hello yedeklerden geri yükleme veri toohello gerçekleştirilecek.</span><span class="sxs-lookup"><span data-stu-id="24e8e-118">Restore data toohello same machine from which hello backups were taken.</span></span>
* <span data-ttu-id="24e8e-119">Veri tooan alternatif makine geri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="24e8e-119">Restore data tooan alternate machine.</span></span>

<span data-ttu-id="24e8e-120">Ocak 2017 ' Microsoft, Önizleme update toohello MARS Aracısı yayımladı.</span><span class="sxs-lookup"><span data-stu-id="24e8e-120">In January 2017, Microsoft released a Preview update toohello MARS agent.</span></span> <span data-ttu-id="24e8e-121">Hata düzeltmeleri yanı sıra, bu güncelleştirme anlık toomount sağlayan geri yükleme, yazılabilir kurtarma noktası anlık görüntü kurtarma birimi olarak sağlar.</span><span class="sxs-lookup"><span data-stu-id="24e8e-121">Along with bug fixes, this update enables Instant Restore, which allows you toomount a writeable recovery point snapshot as a recovery volume.</span></span> <span data-ttu-id="24e8e-122">Ardından, böylece seçerek dosyaları geri yükleme hello kurtarma birimi ve kopyalama dosyaları tooa yerel bilgisayara keşfedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24e8e-122">You can then explore hello recovery volume and copy files tooa local computer thereby selectively restoring files.</span></span>

> [!NOTE]
> <span data-ttu-id="24e8e-123">Merhaba [Ocak 2017 Azure Backup güncelleştirmesini](https://support.microsoft.com/en-us/help/3216528?preview) toouse toorestore verilerin anlık geri yüklemek istiyorsanız gereklidir.</span><span class="sxs-lookup"><span data-stu-id="24e8e-123">hello [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) is required if you want toouse Instant Restore toorestore data.</span></span> <span data-ttu-id="24e8e-124">Ayrıca hello destek makalesinde listelenen yerel ayarlar kasalarında hello yedekleme verilerini korunmalıdır.</span><span class="sxs-lookup"><span data-stu-id="24e8e-124">Also hello backup data must be protected in vaults in locales listed in hello support article.</span></span> <span data-ttu-id="24e8e-125">Merhaba başvurun [Ocak 2017 Azure Backup güncelleştirmesini](https://support.microsoft.com/en-us/help/3216528?preview) hello son anlık geri yükleme desteği yerel ayarların listesi için.</span><span class="sxs-lookup"><span data-stu-id="24e8e-125">Consult hello [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) for hello latest list of locales that support Instant Restore.</span></span> <span data-ttu-id="24e8e-126">Anlık geri yükleme **değil** tüm bölgelerde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="24e8e-126">Instant Restore is **not** currently available in all locales.</span></span>
>

<span data-ttu-id="24e8e-127">Anlık geri yükleme hello Klasik Portalı'nda, Kurtarma Hizmetleri kasalarının hello Azure portal'ın kullanımda ve yedekleme kasaları için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="24e8e-127">Instant Restore is available for use in Recovery Services vaults in hello Azure portal and Backup vaults in hello classic portal.</span></span> <span data-ttu-id="24e8e-128">Toouse anlık geri yüklemek istiyorsanız, hello MARS güncelleştirmeyi indirin ve anlık geri Bahsediyor hello yordamları izleyin.</span><span class="sxs-lookup"><span data-stu-id="24e8e-128">If you want toouse Instant Restore, download hello MARS update, and follow hello procedures that mention Instant Restore.</span></span>


## <a name="use-instant-restore-toorecover-data-toohello-same-machine"></a><span data-ttu-id="24e8e-129">Anlık geri toorecover veri toohello kullanmak aynı makine</span><span class="sxs-lookup"><span data-stu-id="24e8e-129">Use Instant Restore toorecover data toohello same machine</span></span>

<span data-ttu-id="24e8e-130">Dosya ve istek toorestore yanlışlıkla sildiyseniz, (hangi hello yedekleme alınır) aynı makine hello aşağıdaki adımları toohello hello verileri kurtarmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="24e8e-130">If you accidentally deleted a file and wish toorestore it toohello same machine (from which hello backup is taken), hello following steps will help you recover hello data.</span></span>

1. <span data-ttu-id="24e8e-131">Açık hello **Microsoft Azure yedekleme** içinde Vurgu.</span><span class="sxs-lookup"><span data-stu-id="24e8e-131">Open hello **Microsoft Azure Backup** snap in.</span></span> <span data-ttu-id="24e8e-132">Merhaba ek bileşeninde yüklendiği bilmiyorsanız, hello bilgisayar veya sunucu için arama **Microsoft Azure yedekleme**.</span><span class="sxs-lookup"><span data-stu-id="24e8e-132">If you don't know where hello snap in was installed, search hello computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="24e8e-133">Merhaba masaüstü uygulaması hello arama sonuçlarında görüntülenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="24e8e-133">hello desktop app should appear in hello search results.</span></span>

2. <span data-ttu-id="24e8e-134">Tıklatın **verileri kurtarabilirsiniz** toostart hello Sihirbazı.</span><span class="sxs-lookup"><span data-stu-id="24e8e-134">Click **Recover Data** toostart hello wizard.</span></span>

    ![Verileri kurtarma](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="24e8e-136">Merhaba üzerinde **Başlarken** bölmesi, toorestore hello veri toohello aynı sunucu bilgisayar seçin veya **bu sunucu (`<server name>`)** tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="24e8e-136">On hello **Getting Started** pane, toorestore hello data toohello same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![Bu sunucu seçeneği toorestore hello veri toohello seçin aynı makine](./media/backup-azure-restore-windows-server/samemachine_gettingstarted_instantrestore.png)

4. <span data-ttu-id="24e8e-138">Merhaba üzerinde **seçin kurtarma moduna** bölmesinde seçin **dosyalara ve klasörlere** ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="24e8e-138">On hello **Select Recovery Mode** pane, choose **Individual files and folders** and then click **Next**.</span></span>

    ![Gözatma dosyaları](./media/backup-azure-restore-windows-server/samemachine_selectrecoverymode_instantrestore.png)

5. <span data-ttu-id="24e8e-140">Merhaba üzerinde **birim seçin ve tarih** bölmesi, hello dosyaları ve/veya toorestore istediğiniz klasörleri içeren bir select hello birimi.</span><span class="sxs-lookup"><span data-stu-id="24e8e-140">On hello **Select Volume and Date** pane, select hello volume that contains hello files and/or folders you want toorestore.</span></span>

    <span data-ttu-id="24e8e-141">Merhaba takvimde bir kurtarma noktası seçin.</span><span class="sxs-lookup"><span data-stu-id="24e8e-141">On hello calendar, select a recovery point.</span></span> <span data-ttu-id="24e8e-142">Zaman içinde herhangi bir kurtarma noktasından geri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24e8e-142">You can restore from any recovery point in time.</span></span> <span data-ttu-id="24e8e-143">İçinde tarihleri **kalın** hello en az bir kurtarma noktası kullanılabilirliğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="24e8e-143">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="24e8e-144">Birden fazla kurtarma noktası mevcutsa, bir tarih seçtikten sonra hello hello belirli bir kurtarma noktası seçin **zaman** açılır menü.</span><span class="sxs-lookup"><span data-stu-id="24e8e-144">Once you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span>

    ![Birimi ve tarih](./media/backup-azure-restore-windows-server/samemachine_selectvolumedate_instantrestore.png)

6. <span data-ttu-id="24e8e-146">Merhaba kurtarma noktası toorestore seçtikten sonra tıklatın **bağlama**.</span><span class="sxs-lookup"><span data-stu-id="24e8e-146">Once you have chosen hello recovery point toorestore, click **Mount**.</span></span>

    <span data-ttu-id="24e8e-147">Azure yedekleme hello yerel kurtarma noktası bağlar ve kurtarma birimi olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="24e8e-147">Azure Backup mounts hello local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="24e8e-148">Hello üzerinde **Gözat ve kurtarma dosyaları** bölmesinde tıklatın **Gözat** tooopen Windows Gezgini, Bul hello dosya ve klasörleri istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="24e8e-148">On hello **Browse and Recover Files** pane, click **Browse** tooopen Windows Explorer and find hello files and folders you want.</span></span>

    ![Kurtarma Seçenekleri](./media/backup-azure-restore-windows-server/samemachine_browserecover_instantrestore.png)


8. <span data-ttu-id="24e8e-150">Windows Gezgini, kopyalama hello dosyaları ve/veya klasörleri de toorestore istediğiniz ve tooany konumu yerel toohello sunucusu veya bilgisayar yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="24e8e-150">In Windows Explorer, copy hello files and/or folders you want toorestore and paste them tooany location local toohello server or computer.</span></span> <span data-ttu-id="24e8e-151">Açın veya hello dosyaları doğrudan hello kurtarma birimi akış ve hello sürümleri kurtarılan doğru doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="24e8e-151">You can open or stream hello files directly from hello recovery volume and verify hello correct versions are recovered.</span></span>

    ![Dosyaları ve klasörleri takılı birim toolocal konumdan kopyalama ve yapıştırma](./media/backup-azure-restore-windows-server/samemachine_copy_instantrestore.png)

9. <span data-ttu-id="24e8e-153">İşiniz bittiğinde geri yükleme hello dosyaları ve/veya klasörlerde hello **göz atın ve kurtarma dosyaları** bölmesinde tıklatın **çıkarma**.</span><span class="sxs-lookup"><span data-stu-id="24e8e-153">When you are finished restoring hello files and/or folders, on hello **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="24e8e-154">Ardından **Evet** tooconfirm toounmount hello birim istiyor.</span><span class="sxs-lookup"><span data-stu-id="24e8e-154">Then click **Yes** tooconfirm that you want toounmount hello volume.</span></span>

    ![Merhaba birim çıkarın ve onaylayın](./media/backup-azure-restore-windows-server/samemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="24e8e-156">Çıkarma değil tıklatırsanız, hello kurtarma birimi zaman takıldı hello zamandan altı saat bağlı kalır.</span><span class="sxs-lookup"><span data-stu-id="24e8e-156">If you do not click Unmount, hello Recovery Volume will remain mounted for six hours from hello time when it was mounted.</span></span> <span data-ttu-id="24e8e-157">Merhaba birim bağlıyken hiçbir yedekleme işlemleri çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="24e8e-157">No backup operations will run while hello volume is mounted.</span></span> <span data-ttu-id="24e8e-158">Merhaba kurtarma birimi kaldırılan tamamlandıktan sonra tüm zamanlanmış yedekleme işlemi toorun hello birimin zaman bağlı, hello süre boyunca çalışır.</span><span class="sxs-lookup"><span data-stu-id="24e8e-158">Any backup operation scheduled toorun during hello time when hello volume is mounted, will run after hello recovery volume is unmounted.</span></span>
    >


## <a name="recover-data-toohello-same-machine"></a><span data-ttu-id="24e8e-159">Veri toohello kurtarmak aynı makine</span><span class="sxs-lookup"><span data-stu-id="24e8e-159">Recover data toohello same machine</span></span>
<span data-ttu-id="24e8e-160">Dosya ve istek toorestore yanlışlıkla sildiyseniz, (hangi hello yedekleme alınır) aynı makine hello aşağıdaki adımları toohello hello verileri kurtarmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="24e8e-160">If you accidentally deleted a file and wish toorestore it toohello same machine (from which hello backup is taken), hello following steps will help you recover hello data.</span></span>

1. <span data-ttu-id="24e8e-161">Açık hello **Microsoft Azure yedekleme** içinde Vurgu.</span><span class="sxs-lookup"><span data-stu-id="24e8e-161">Open hello **Microsoft Azure Backup** snap in.</span></span>
2. <span data-ttu-id="24e8e-162">Tıklatın **verileri kurtarabilirsiniz** tooinitiate hello iş akışı.</span><span class="sxs-lookup"><span data-stu-id="24e8e-162">Click **Recover Data** tooinitiate hello workflow.</span></span>

    ![Verileri kurtarma](./media/backup-azure-restore-windows-server-classic/recover.png)
3. <span data-ttu-id="24e8e-164">Select hello  **bu sunucu (*yourmachinename*) ** seçeneğinin toorestore hello yedeklenen hello dosyada aynı makine.</span><span class="sxs-lookup"><span data-stu-id="24e8e-164">Select hello **This server (*yourmachinename*)** option toorestore hello backed up file on hello same machine.</span></span>

    ![Aynı makine](./media/backup-azure-restore-windows-server-classic/samemachine.png)
4. <span data-ttu-id="24e8e-166">Çok seçin**gözatma için dosyaları** veya **dosya aramak için**.</span><span class="sxs-lookup"><span data-stu-id="24e8e-166">Choose too**Browse for files** or **Search for files**.</span></span>

    <span data-ttu-id="24e8e-167">Toorestore düşünüyorsanız, yolu bilinen bir veya daha fazla hello varsayılan seçeneği bırakın.</span><span class="sxs-lookup"><span data-stu-id="24e8e-167">Leave hello default option if you plan toorestore one or more files whose path is known.</span></span> <span data-ttu-id="24e8e-168">Merhaba klasör yapısı hakkında emin değilseniz, ancak bir dosya için toosearch istersiniz, hello çekme **dosya aramak için** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="24e8e-168">If you are not sure about hello folder structure but would like toosearch for a file, pick hello **Search for files** option.</span></span> <span data-ttu-id="24e8e-169">Bu bölümde Hello amaçla biz hello varsayılan seçeneği ile devam eder.</span><span class="sxs-lookup"><span data-stu-id="24e8e-169">For hello purpose of this section, we will proceed with hello default option.</span></span>

    ![Gözatma dosyaları](./media/backup-azure-restore-windows-server-classic/browseandsearch.png)
5. <span data-ttu-id="24e8e-171">Toorestore hello dosya istediğiniz hello birimi seçin.</span><span class="sxs-lookup"><span data-stu-id="24e8e-171">Select hello volume from which you wish toorestore hello file.</span></span>

    <span data-ttu-id="24e8e-172">Zaman içinde herhangi bir noktadan geri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24e8e-172">You can restore from any point in time.</span></span> <span data-ttu-id="24e8e-173">Görüntülenen tarihler **kalın** hello Takvim denetiminde bir geri yükleme noktası hello kullanılabilirliğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="24e8e-173">Dates which appear in **bold** in hello calendar control indicate hello availability of a restore point.</span></span> <span data-ttu-id="24e8e-174">Bir tarih seçildikten sonra yedekleme zamanlaması (ve yedekleme işlemini hello başarısını), temel bir noktası hello zamandan seçebileceğiniz **zaman** açılır.</span><span class="sxs-lookup"><span data-stu-id="24e8e-174">Once a date is selected, based on your backup schedule (and hello success of a backup operation), you can select a point in time from hello **Time** drop down.</span></span>

    ![Birimi ve tarih](./media/backup-azure-restore-windows-server-classic/volanddate.png)
6. <span data-ttu-id="24e8e-176">Merhaba öğeleri toorecover seçin.</span><span class="sxs-lookup"><span data-stu-id="24e8e-176">Select hello items toorecover.</span></span> <span data-ttu-id="24e8e-177">Çoklu seçim klasörleri/dosyaları toorestore istediğiniz kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24e8e-177">You can multi-select folders/files you wish toorestore.</span></span>

    ![Dosya seçme](./media/backup-azure-restore-windows-server-classic/selectfiles.png)
7. <span data-ttu-id="24e8e-179">Merhaba kurtarma parametreleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="24e8e-179">Specify hello recovery parameters.</span></span>

    ![Kurtarma Seçenekleri](./media/backup-azure-restore-windows-server-classic/recoveroptions.png)

   * <span data-ttu-id="24e8e-181">Bir seçeneğiniz toohello özgün konumuna (hangi hello dosya/klasör üzerine yazılacağını) veya hello tooanother konuma geri yüklenmesi, aynı makine.</span><span class="sxs-lookup"><span data-stu-id="24e8e-181">You have an option of restoring toohello original location (in which hello file/folder would be overwritten) or tooanother location in hello same machine.</span></span>
   * <span data-ttu-id="24e8e-182">Merhaba dosya/klasör, istediğiniz toorestore hello hedef konumda mevcut kopyaları oluşturabileceğiniz varsa (Merhaba iki sürümü aynı dosya) hello hedef konumda hello dosyaları üzerine veya, hello hedef mevcut hello dosyaların hello kurtarma işlemini atla.</span><span class="sxs-lookup"><span data-stu-id="24e8e-182">If hello file/folder you wish toorestore exists in hello target location, you can create copies (two versions of hello same file), overwrite hello files in hello target location, or skip hello recovery of hello files which exist in hello target.</span></span>
   * <span data-ttu-id="24e8e-183">Kurtarılmakta hello dosyaları hello ACL'ler geri yüklenmesi hello varsayılan seçeneği bırakın önerilir.</span><span class="sxs-lookup"><span data-stu-id="24e8e-183">It is highly recommended that you leave hello default option of restoring hello ACLs on hello files which are being recovered.</span></span>
8. <span data-ttu-id="24e8e-184">Bu girişleri sağlanan sonra tıklayın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="24e8e-184">Once these inputs are provided, click **Next**.</span></span> <span data-ttu-id="24e8e-185">Merhaba dosyaları toothis makineyi yükler, hello kurtarma akışı başlar.</span><span class="sxs-lookup"><span data-stu-id="24e8e-185">hello recovery workflow, which restores hello files toothis machine, will begin.</span></span>

## <a name="recover-tooan-alternate-machine"></a><span data-ttu-id="24e8e-186">Tooan alternatif makine Kurtar</span><span class="sxs-lookup"><span data-stu-id="24e8e-186">Recover tooan alternate machine</span></span>
<span data-ttu-id="24e8e-187">Tüm sunucunuzu kaybolursa, verileri Azure yedekleme tooa farklı makineden kurtarmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24e8e-187">If your entire server is lost, you can still recover data from Azure Backup tooa different machine.</span></span> <span data-ttu-id="24e8e-188">Aşağıdaki adımları hello hello iş akışı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="24e8e-188">hello following steps illustrate hello workflow.</span></span>  

<span data-ttu-id="24e8e-189">Bu adımlarda kullanılan hello terminolojisi içerir:</span><span class="sxs-lookup"><span data-stu-id="24e8e-189">hello terminology used in these steps includes:</span></span>

* <span data-ttu-id="24e8e-190">*Kaynak makine* – hello özgün makine hangi hello yedekten alındığı ve hangi şu anda kullanılamıyor.</span><span class="sxs-lookup"><span data-stu-id="24e8e-190">*Source machine* – hello original machine from which hello backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="24e8e-191">*Hedef makine* – hello makine toowhich hello verilerin kurtarıldığı.</span><span class="sxs-lookup"><span data-stu-id="24e8e-191">*Target machine* – hello machine toowhich hello data is being recovered.</span></span>
* <span data-ttu-id="24e8e-192">*Örnek kasa* – hello yedekleme kasası toowhich hello *kaynak makine* ve *hedef makine* kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="24e8e-192">*Sample vault* – hello Backup vault toowhich hello *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="24e8e-193">Bir makineden alınan yedeklemeler hello işletim sisteminin önceki bir sürümünü çalıştıran bir makineye geri yüklenemez.</span><span class="sxs-lookup"><span data-stu-id="24e8e-193">Backups taken from a machine cannot be restored on a machine which is running an earlier version of hello operating system.</span></span> <span data-ttu-id="24e8e-194">Yedeklemeler Windows 7 makineden alınır, örneğin, bir Windows 8 veya üstü makine geri yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="24e8e-194">For example, if backups are taken from a Windows 7 machine, it can be restored on a Windows 8 or above machine.</span></span> <span data-ttu-id="24e8e-195">Ancak, hello tam tersini true tutmaz.</span><span class="sxs-lookup"><span data-stu-id="24e8e-195">However, hello vice-versa does not hold true.</span></span>
>
>

1. <span data-ttu-id="24e8e-196">Açık hello **Microsoft Azure yedekleme** hello üzerinde içinde Vurgu *hedef makine*.</span><span class="sxs-lookup"><span data-stu-id="24e8e-196">Open hello **Microsoft Azure Backup** snap in on hello *Target machine*.</span></span>
2. <span data-ttu-id="24e8e-197">Bu hello olun *hedef makine* ve hello *kaynak makine* kayıtlı toohello olan aynı yedekleme kasası.</span><span class="sxs-lookup"><span data-stu-id="24e8e-197">Ensure that hello *Target machine* and hello *Source machine* are registered toohello same backup vault.</span></span>
3. <span data-ttu-id="24e8e-198">Tıklatın **verileri kurtarabilirsiniz** tooinitiate hello iş akışı.</span><span class="sxs-lookup"><span data-stu-id="24e8e-198">Click **Recover Data** tooinitiate hello workflow.</span></span>

    ![Verileri kurtarma](./media/backup-azure-restore-windows-server-classic/recover.png)
4. <span data-ttu-id="24e8e-200">Seçin **başka bir sunucu**</span><span class="sxs-lookup"><span data-stu-id="24e8e-200">Select **Another server**</span></span>

    ![Başka bir sunucu](./media/backup-azure-restore-windows-server-classic/anotherserver.png)
5. <span data-ttu-id="24e8e-202">Toohello karşılık gelen hello kasa kimlik bilgilerini sağlayın *örnek kasa*.</span><span class="sxs-lookup"><span data-stu-id="24e8e-202">Provide hello vault credential file that corresponds toohello *Sample vault*.</span></span> <span data-ttu-id="24e8e-203">Merhaba kasa kimlik bilgilerini geçersiz (veya süresi dolmuş) ise yeni bir kasa kimlik bilgilerini hello indirin *örnek kasa* hello Klasik Azure Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="24e8e-203">If hello vault credential file is invalid (or expired) download a new vault credential file from hello *Sample vault* in hello Azure classic portal.</span></span> <span data-ttu-id="24e8e-204">Merhaba kasa kimlik bilgilerini sağlanan sonra hello yedekleme kasası hello kasa kimlik bilgilerini karşı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="24e8e-204">Once hello vault credential file is provided, hello backup vault against hello vault credential file is displayed.</span></span>
6. <span data-ttu-id="24e8e-205">Select hello *kaynak makine* görüntülenmesini makineler hello listesinden.</span><span class="sxs-lookup"><span data-stu-id="24e8e-205">Select hello *Source machine* from hello list of displayed machines.</span></span>

    ![Makineler listesi](./media/backup-azure-restore-windows-server-classic/machinelist.png)
7. <span data-ttu-id="24e8e-207">Her iki hello seçin **dosya aramak için** veya **gözatma için dosyaları** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="24e8e-207">Select either hello **Search for files** or **Browse for files** option.</span></span> <span data-ttu-id="24e8e-208">Bu bölümde Hello amaçla hello kullanacağız **dosya aramak için** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="24e8e-208">For hello purpose of this section, we will use hello **Search for files** option.</span></span>

    ![Arama](./media/backup-azure-restore-windows-server-classic/search.png)
8. <span data-ttu-id="24e8e-210">Merhaba birimi ve tarih hello sonraki ekranında seçin.</span><span class="sxs-lookup"><span data-stu-id="24e8e-210">Select hello volume and date in hello next screen.</span></span> <span data-ttu-id="24e8e-211">Arama toorestore istediğiniz için hello klasör/dosya adı.</span><span class="sxs-lookup"><span data-stu-id="24e8e-211">Search for hello folder/file name you want toorestore.</span></span>

    ![Arama öğeleri](./media/backup-azure-restore-windows-server-classic/searchitems.png)
9. <span data-ttu-id="24e8e-213">Merhaba dosyaları geri toobe gereken yeri hello konumu seçin.</span><span class="sxs-lookup"><span data-stu-id="24e8e-213">Select hello location where hello files need toobe restored.</span></span>

    ![Geri yükleme konumu](./media/backup-azure-restore-windows-server-classic/restorelocation.png)
10. <span data-ttu-id="24e8e-215">Sırasında sağlanan hello şifreleme parolası sağlamak *kaynak makinenin* kayıt çok*örnek kasa*.</span><span class="sxs-lookup"><span data-stu-id="24e8e-215">Provide hello encryption passphrase that was provided during *Source machine’s* registration too*Sample vault*.</span></span>

    ![Şifreleme](./media/backup-azure-restore-windows-server-classic/encryption.png)
11. <span data-ttu-id="24e8e-217">Merhaba giriş sağlanan sonra tıklayın **kurtarmak**, hangi Tetikleyicileri hello sağlanan dosyaları toohello hedef yedeklenen hello geri yükleme.</span><span class="sxs-lookup"><span data-stu-id="24e8e-217">Once hello input is provided, click **Recover**, which triggers hello restore of hello backed up files toohello destination provided.</span></span>

## <a name="use-instant-restore-toorestore-data-tooan-alternate-machine"></a><span data-ttu-id="24e8e-218">Toorestore veri tooan alternatif makine anında geri kullanın</span><span class="sxs-lookup"><span data-stu-id="24e8e-218">Use Instant Restore toorestore data tooan alternate machine</span></span>
<span data-ttu-id="24e8e-219">Tüm sunucunuzu kaybolursa, verileri Azure yedekleme tooa farklı makineden kurtarmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24e8e-219">If your entire server is lost, you can still recover data from Azure Backup tooa different machine.</span></span> <span data-ttu-id="24e8e-220">Aşağıdaki adımları hello hello iş akışı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="24e8e-220">hello following steps illustrate hello workflow.</span></span>

<span data-ttu-id="24e8e-221">Bu adımlarda kullanılan hello terminolojisi içerir:</span><span class="sxs-lookup"><span data-stu-id="24e8e-221">hello terminology used in these steps includes:</span></span>

* <span data-ttu-id="24e8e-222">*Kaynak makine* – hello özgün makine hangi hello yedekten alındığı ve hangi şu anda kullanılamıyor.</span><span class="sxs-lookup"><span data-stu-id="24e8e-222">*Source machine* – hello original machine from which hello backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="24e8e-223">*Hedef makine* – hello makine toowhich hello verilerin kurtarıldığı.</span><span class="sxs-lookup"><span data-stu-id="24e8e-223">*Target machine* – hello machine toowhich hello data is being recovered.</span></span>
* <span data-ttu-id="24e8e-224">*Örnek kasa* – hello kurtarma Hizmetleri kasası toowhich hello *kaynak makine* ve *hedef makine* kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="24e8e-224">*Sample vault* – hello Recovery Services vault toowhich hello *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="24e8e-225">Yedeklemeler, geri yüklenen tooa hedef makine hello işletim sisteminin önceki bir sürümünü çalıştıran olamaz.</span><span class="sxs-lookup"><span data-stu-id="24e8e-225">Backups can't be restored tooa target machine running an earlier version of hello operating system.</span></span> <span data-ttu-id="24e8e-226">Örneğin, bir Windows bilgisayarı olabilir 7'den alınan bir yedeklemeyi bilgisayar bir Windows 8 veya daha sonra geri.</span><span class="sxs-lookup"><span data-stu-id="24e8e-226">For example, a backup taken from a Windows 7 computer can be restored on a Windows 8, or later, computer.</span></span> <span data-ttu-id="24e8e-227">Bir Windows 8 bilgisayardan alınan bir yedeklemeyi geri yüklenen tooa Windows 7 bilgisayar olamaz.</span><span class="sxs-lookup"><span data-stu-id="24e8e-227">A backup taken from a Windows 8 computer cannot be restored tooa Windows 7 computer.</span></span>
>
>

1. <span data-ttu-id="24e8e-228">Açık hello **Microsoft Azure yedekleme** hello üzerinde içinde Vurgu *hedef makine*.</span><span class="sxs-lookup"><span data-stu-id="24e8e-228">Open hello **Microsoft Azure Backup** snap in on hello *Target machine*.</span></span>

2. <span data-ttu-id="24e8e-229">Merhaba olun *hedef makine* ve hello *kaynak makine* aynı kurtarma Hizmetleri kasası kayıtlı toohello şunlardır.</span><span class="sxs-lookup"><span data-stu-id="24e8e-229">Ensure hello *Target machine* and hello *Source machine* are registered toohello same Recovery Services vault.</span></span>

3. <span data-ttu-id="24e8e-230">Tıklatın **verileri kurtarabilirsiniz** tooopen hello **Veri Kurtarma Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="24e8e-230">Click **Recover Data** tooopen hello **Recover Data wizard**.</span></span>

    ![Verileri kurtarma](./media/backup-azure-restore-windows-server/recover.png)

4. <span data-ttu-id="24e8e-232">Merhaba üzerinde **Başlarken** bölmesinde, **başka bir sunucu**</span><span class="sxs-lookup"><span data-stu-id="24e8e-232">On hello **Getting Started** pane, select **Another server**</span></span>

    ![Başka bir sunucu](./media/backup-azure-restore-windows-server/alternatemachine_gettingstarted_instantrestore.png)

5. <span data-ttu-id="24e8e-234">Toohello karşılık gelen hello kasa kimlik bilgilerini sağlayın *örnek kasa*, tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="24e8e-234">Provide hello vault credential file that corresponds toohello *Sample vault*, and click **Next**.</span></span>

    <span data-ttu-id="24e8e-235">Merhaba kasa kimlik bilgilerini geçersiz (veya süresi dolmuş) varsa, yeni bir kasa kimlik bilgilerini hello indirin *örnek kasa* hello Azure Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="24e8e-235">If hello vault credential file is invalid (or expired), download a new vault credential file from hello *Sample vault* in hello Azure portal.</span></span> <span data-ttu-id="24e8e-236">Geçerli kasa kimlik bilgileri sağladığınızda, yedekleme kasası karşılık gelen hello hello adı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="24e8e-236">Once you provide a valid vault credential, hello name of hello corresponding Backup Vault appears.</span></span>

6. <span data-ttu-id="24e8e-237">Merhaba üzerinde **yedekleme sunucusu seçin** bölmesinde, select hello *kaynak makine* görüntülenmesini makineler hello listesinden ve hello parola girin.</span><span class="sxs-lookup"><span data-stu-id="24e8e-237">On hello **Select Backup Server** pane, select hello *Source machine* from hello list of displayed machines and provide hello passphrase.</span></span> <span data-ttu-id="24e8e-238">Ardından **İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="24e8e-238">Then click **Next**.</span></span>

    ![Makineler listesi](./media/backup-azure-restore-windows-server/alternatemachine_selectmachine_instantrestore.png)

7. <span data-ttu-id="24e8e-240">Merhaba üzerinde **seçin kurtarma moduna** bölmesinde seçin **dosyalara ve klasörlere** tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="24e8e-240">On hello **Select Recovery Mode** pane, select **Individual files and folders** and click **Next**.</span></span>

    ![Arama](./media/backup-azure-restore-windows-server/alternatemachine_selectrecoverymode_instantrestore.png)

8. <span data-ttu-id="24e8e-242">Merhaba üzerinde **birim seçin ve tarih** bölmesi, hello dosyaları ve/veya toorestore istediğiniz klasörleri içeren bir select hello birimi.</span><span class="sxs-lookup"><span data-stu-id="24e8e-242">On hello **Select Volume and Date** pane, select hello volume that contains hello files and/or folders you want toorestore.</span></span>

    <span data-ttu-id="24e8e-243">Merhaba takvimde bir kurtarma noktası seçin.</span><span class="sxs-lookup"><span data-stu-id="24e8e-243">On hello calendar, select a recovery point.</span></span> <span data-ttu-id="24e8e-244">Zaman içinde herhangi bir kurtarma noktasından geri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24e8e-244">You can restore from any recovery point in time.</span></span> <span data-ttu-id="24e8e-245">İçinde tarihleri **kalın** hello en az bir kurtarma noktası kullanılabilirliğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="24e8e-245">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="24e8e-246">Birden fazla kurtarma noktası mevcutsa, bir tarih seçtikten sonra hello hello belirli bir kurtarma noktası seçin **zaman** açılır menü.</span><span class="sxs-lookup"><span data-stu-id="24e8e-246">Once you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span>

    ![Arama öğeleri](./media/backup-azure-restore-windows-server/alternatemachine_selectvolumedate_instantrestore.png)

9. <span data-ttu-id="24e8e-248">Tıklatın **bağlama** toolocally bağlama hello kurtarma noktası olarak bir kurtarma birimde, *hedef makine*.</span><span class="sxs-lookup"><span data-stu-id="24e8e-248">Click **Mount** toolocally mount hello recovery point as a recovery volume on your *Target machine*.</span></span>

10. <span data-ttu-id="24e8e-249">Hello üzerinde **Gözat ve kurtarma dosyaları** bölmesinde tıklatın **Gözat** tooopen Windows Gezgini, Bul hello dosya ve klasörleri istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="24e8e-249">On hello **Browse and Recover Files** pane, click **Browse** tooopen Windows Explorer and find hello files and folders you want.</span></span>

    ![Şifreleme](./media/backup-azure-restore-windows-server/alternatemachine_browserecover_instantrestore.png)

11. <span data-ttu-id="24e8e-251">Windows Gezgini'nde, hello dosyaları ve/veya klasörleri hello kurtarma birimden kopyalayıp bunları tooyour *hedef makine* konumu.</span><span class="sxs-lookup"><span data-stu-id="24e8e-251">In Windows Explorer, copy hello files and/or folders from hello recovery volume and paste them tooyour *Target machine* location.</span></span> <span data-ttu-id="24e8e-252">Açın veya hello dosyaları doğrudan hello kurtarma birimi akış ve hello sürümleri kurtarılan doğru doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="24e8e-252">You can open or stream hello files directly from hello recovery volume and verify hello correct versions are recovered.</span></span>

    ![Şifreleme](./media/backup-azure-restore-windows-server/alternatemachine_copy_instantrestore.png)

12. <span data-ttu-id="24e8e-254">İşiniz bittiğinde geri yükleme hello dosyaları ve/veya klasörlerde hello **göz atın ve kurtarma dosyaları** bölmesinde tıklatın **çıkarma**.</span><span class="sxs-lookup"><span data-stu-id="24e8e-254">When you are finished restoring hello files and/or folders, on hello **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="24e8e-255">Ardından **Evet** tooconfirm toounmount hello birim istiyor.</span><span class="sxs-lookup"><span data-stu-id="24e8e-255">Then click **Yes** tooconfirm that you want toounmount hello volume.</span></span>

    ![Şifreleme](./media/backup-azure-restore-windows-server/alternatemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="24e8e-257">Çıkarma değil tıklatırsanız, hello kurtarma birimi zaman takıldı hello zamandan altı saat bağlı kalır.</span><span class="sxs-lookup"><span data-stu-id="24e8e-257">If you do not click Unmount, hello Recovery Volume will remain mounted for six hours from hello time when it was mounted.</span></span> <span data-ttu-id="24e8e-258">Merhaba birim bağlıyken hiçbir yedekleme işlemleri çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="24e8e-258">No backup operations will run while hello volume is mounted.</span></span> <span data-ttu-id="24e8e-259">Merhaba kurtarma birimi kaldırılan tamamlandıktan sonra tüm zamanlanmış yedekleme işlemi toorun hello birimin zaman bağlı, hello süre boyunca çalışır.</span><span class="sxs-lookup"><span data-stu-id="24e8e-259">Any backup operation scheduled toorun during hello time when hello volume is mounted, will run after hello recovery volume is unmounted.</span></span>
    >


## <a name="next-steps"></a><span data-ttu-id="24e8e-260">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="24e8e-260">Next steps</span></span>
* [<span data-ttu-id="24e8e-261">Azure Backup ile ilgili SSS</span><span class="sxs-lookup"><span data-stu-id="24e8e-261">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)
* <span data-ttu-id="24e8e-262">Merhaba ziyaret [Azure yedekleme Forumu](http://go.microsoft.com/fwlink/p/?LinkId=290933).</span><span class="sxs-lookup"><span data-stu-id="24e8e-262">Visit hello [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933).</span></span>

## <a name="learn-more"></a><span data-ttu-id="24e8e-263">Daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="24e8e-263">Learn more</span></span>
* [<span data-ttu-id="24e8e-264">Azure yedekleme genel bakış</span><span class="sxs-lookup"><span data-stu-id="24e8e-264">Azure Backup Overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=222425)
* [<span data-ttu-id="24e8e-265">Yedekleme Azure sanal makineler</span><span class="sxs-lookup"><span data-stu-id="24e8e-265">Backup Azure virtual machines</span></span>](backup-azure-vms-introduction.md)
* [<span data-ttu-id="24e8e-266">Microsoft iş yüklerini yedekleme</span><span class="sxs-lookup"><span data-stu-id="24e8e-266">Backup up Microsoft workloads</span></span>](backup-azure-dpm-introduction.md)
