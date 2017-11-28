---
title: "Azure tooa Windows Server veya Windows bilgisayarı aaaRestore verileri | Microsoft Docs"
description: "Azure tooa Windows Server veya Windows bilgisayarı toorestore verilerin depolanma öğrenin."
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
ms.openlocfilehash: 11335495e448986a74f1733406f87e04331641d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-files-tooa-windows-server-or-windows-client-machine-using-resource-manager-deployment-model"></a><span data-ttu-id="b772e-103">Dosyaları tooa Windows server veya Windows istemci makinesi Resource Manager dağıtım modelini kullanarak geri yükleme</span><span class="sxs-lookup"><span data-stu-id="b772e-103">Restore files tooa Windows server or Windows client machine using Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b772e-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="b772e-104">Azure portal</span></span>](backup-azure-restore-windows-server.md)
> * [<span data-ttu-id="b772e-105">Klasik portal</span><span class="sxs-lookup"><span data-stu-id="b772e-105">Classic portal</span></span>](backup-azure-restore-windows-server-classic.md)
>
>

<span data-ttu-id="b772e-106">Bu makalede açıklanır nasıl bir yedekleme kasası toorestore verileri.</span><span class="sxs-lookup"><span data-stu-id="b772e-106">This article explains how toorestore data from a backup vault.</span></span> <span data-ttu-id="b772e-107">toorestore veri hello Microsoft Azure kurtarma Hizmetleri (MARS) aracısı hello Veri Kurtarma Sihirbazı'nı kullanın.</span><span class="sxs-lookup"><span data-stu-id="b772e-107">toorestore data, you use hello Recover Data wizard in hello Microsoft Azure Recovery Services (MARS) agent.</span></span> <span data-ttu-id="b772e-108">Verileri geri yüklediğinizde, mümkün olur:</span><span class="sxs-lookup"><span data-stu-id="b772e-108">When you restore data, it is possible to:</span></span>

* <span data-ttu-id="b772e-109">Aynı makine hangi hello yedeklerden geri yükleme veri toohello gerçekleştirilecek.</span><span class="sxs-lookup"><span data-stu-id="b772e-109">Restore data toohello same machine from which hello backups were taken.</span></span>
* <span data-ttu-id="b772e-110">Veri tooan alternatif makine geri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="b772e-110">Restore data tooan alternate machine.</span></span>

<span data-ttu-id="b772e-111">Ocak 2017 ' Microsoft, Önizleme update toohello MARS Aracısı yayımladı.</span><span class="sxs-lookup"><span data-stu-id="b772e-111">In January 2017, Microsoft released a Preview update toohello MARS agent.</span></span> <span data-ttu-id="b772e-112">Hata düzeltmeleri yanı sıra, bu güncelleştirme anlık toomount sağlayan geri yükleme, yazılabilir kurtarma noktası anlık görüntü kurtarma birimi olarak sağlar.</span><span class="sxs-lookup"><span data-stu-id="b772e-112">Along with bug fixes, this update enables Instant Restore, which allows you toomount a writeable recovery point snapshot as a recovery volume.</span></span> <span data-ttu-id="b772e-113">Ardından, böylece seçerek dosyaları geri yükleme hello kurtarma birimi ve kopyalama dosyaları tooa yerel bilgisayara keşfedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b772e-113">You can then explore hello recovery volume and copy files tooa local computer thereby selectively restoring files.</span></span>

> [!NOTE]
> <span data-ttu-id="b772e-114">Merhaba [Ocak 2017 Azure Backup güncelleştirmesini](https://support.microsoft.com/en-us/help/3216528?preview) toouse toorestore verilerin anlık geri yüklemek istiyorsanız gereklidir.</span><span class="sxs-lookup"><span data-stu-id="b772e-114">hello [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) is required if you want toouse Instant Restore toorestore data.</span></span> <span data-ttu-id="b772e-115">Ayrıca hello destek makalesinde listelenen yerel ayarlar kasalarında hello yedekleme verilerini korunmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b772e-115">Also hello backup data must be protected in vaults in locales listed in hello support article.</span></span> <span data-ttu-id="b772e-116">Merhaba başvurun [Ocak 2017 Azure Backup güncelleştirmesini](https://support.microsoft.com/en-us/help/3216528?preview) hello son anlık geri yükleme desteği yerel ayarların listesi için.</span><span class="sxs-lookup"><span data-stu-id="b772e-116">Consult hello [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) for hello latest list of locales that support Instant Restore.</span></span> <span data-ttu-id="b772e-117">Anlık geri yükleme **değil** tüm bölgelerde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b772e-117">Instant Restore is **not** currently available in all locales.</span></span>
>

<span data-ttu-id="b772e-118">Anlık geri yükleme hello Klasik Portalı'nda, Kurtarma Hizmetleri kasalarının hello Azure portal'ın kullanımda ve yedekleme kasaları için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b772e-118">Instant Restore is available for use in Recovery Services vaults in hello Azure portal and Backup vaults in hello classic portal.</span></span> <span data-ttu-id="b772e-119">Toouse anlık geri yüklemek istiyorsanız, hello MARS güncelleştirmeyi indirin ve anlık geri Bahsediyor hello yordamları izleyin.</span><span class="sxs-lookup"><span data-stu-id="b772e-119">If you want toouse Instant Restore, download hello MARS update, and follow hello procedures that mention Instant Restore.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="use-instant-restore-toorecover-data-toohello-same-machine"></a><span data-ttu-id="b772e-120">Anlık geri toorecover veri toohello kullanmak aynı makine</span><span class="sxs-lookup"><span data-stu-id="b772e-120">Use Instant Restore toorecover data toohello same machine</span></span>

<span data-ttu-id="b772e-121">Dosya ve istek toorestore yanlışlıkla sildiyseniz, (hangi hello yedekleme alınır) aynı makine hello aşağıdaki adımları toohello hello verileri kurtarmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="b772e-121">If you accidentally deleted a file and wish toorestore it toohello same machine (from which hello backup is taken), hello following steps will help you recover hello data.</span></span>

1. <span data-ttu-id="b772e-122">Açık hello **Microsoft Azure yedekleme** içinde Vurgu.</span><span class="sxs-lookup"><span data-stu-id="b772e-122">Open hello **Microsoft Azure Backup** snap in.</span></span> <span data-ttu-id="b772e-123">Merhaba ek bileşeninde yüklendiği bilmiyorsanız, hello bilgisayar veya sunucu için arama **Microsoft Azure yedekleme**.</span><span class="sxs-lookup"><span data-stu-id="b772e-123">If you don't know where hello snap in was installed, search hello computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="b772e-124">Merhaba masaüstü uygulaması hello arama sonuçlarında görüntülenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="b772e-124">hello desktop app should appear in hello search results.</span></span>

2. <span data-ttu-id="b772e-125">Tıklatın **verileri kurtarabilirsiniz** toostart hello Sihirbazı.</span><span class="sxs-lookup"><span data-stu-id="b772e-125">Click **Recover Data** toostart hello wizard.</span></span>

    ![Verileri kurtarma](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="b772e-127">Merhaba üzerinde **Başlarken** bölmesi, toorestore hello veri toohello aynı sunucu bilgisayar seçin veya **bu sunucu (`<server name>`)** tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="b772e-127">On hello **Getting Started** pane, toorestore hello data toohello same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![Bu sunucu seçeneği toorestore hello veri toohello seçin aynı makine](./media/backup-azure-restore-windows-server/samemachine_gettingstarted_instantrestore.png)

4. <span data-ttu-id="b772e-129">Merhaba üzerinde **seçin kurtarma moduna** bölmesinde seçin **dosyalara ve klasörlere** ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="b772e-129">On hello **Select Recovery Mode** pane, choose **Individual files and folders** and then click **Next**.</span></span>

    ![Gözatma dosyaları](./media/backup-azure-restore-windows-server/samemachine_selectrecoverymode_instantrestore.png)

5. <span data-ttu-id="b772e-131">Merhaba üzerinde **birim seçin ve tarih** bölmesi, hello dosyaları ve/veya toorestore istediğiniz klasörleri içeren bir select hello birimi.</span><span class="sxs-lookup"><span data-stu-id="b772e-131">On hello **Select Volume and Date** pane, select hello volume that contains hello files and/or folders you want toorestore.</span></span>

    <span data-ttu-id="b772e-132">Merhaba takvimde bir kurtarma noktası seçin.</span><span class="sxs-lookup"><span data-stu-id="b772e-132">On hello calendar, select a recovery point.</span></span> <span data-ttu-id="b772e-133">Zaman içinde herhangi bir kurtarma noktasından geri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b772e-133">You can restore from any recovery point in time.</span></span> <span data-ttu-id="b772e-134">İçinde tarihleri **kalın** hello en az bir kurtarma noktası kullanılabilirliğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="b772e-134">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="b772e-135">Birden fazla kurtarma noktası mevcutsa, bir tarih seçtikten sonra hello hello belirli bir kurtarma noktası seçin **zaman** açılır menü.</span><span class="sxs-lookup"><span data-stu-id="b772e-135">Once you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span>

    ![Birimi ve tarih](./media/backup-azure-restore-windows-server/samemachine_selectvolumedate_instantrestore.png)

6. <span data-ttu-id="b772e-137">Merhaba kurtarma noktası toorestore seçtikten sonra tıklatın **bağlama**.</span><span class="sxs-lookup"><span data-stu-id="b772e-137">Once you have chosen hello recovery point toorestore, click **Mount**.</span></span>

    <span data-ttu-id="b772e-138">Azure yedekleme hello yerel kurtarma noktası bağlar ve kurtarma birimi olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="b772e-138">Azure Backup mounts hello local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="b772e-139">Hello üzerinde **Gözat ve kurtarma dosyaları** bölmesinde tıklatın **Gözat** tooopen Windows Gezgini, Bul hello dosya ve klasörleri istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="b772e-139">On hello **Browse and Recover Files** pane, click **Browse** tooopen Windows Explorer and find hello files and folders you want.</span></span>

    ![Kurtarma Seçenekleri](./media/backup-azure-restore-windows-server/samemachine_browserecover_instantrestore.png)


8. <span data-ttu-id="b772e-141">Windows Gezgini, kopyalama hello dosyaları ve/veya klasörleri de toorestore istediğiniz ve tooany konumu yerel toohello sunucusu veya bilgisayar yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="b772e-141">In Windows Explorer, copy hello files and/or folders you want toorestore and paste them tooany location local toohello server or computer.</span></span> <span data-ttu-id="b772e-142">Açın veya hello dosyaları doğrudan hello kurtarma birimi akış ve hello sürümleri kurtarılan doğru doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="b772e-142">You can open or stream hello files directly from hello recovery volume and verify hello correct versions are recovered.</span></span>

    ![Dosyaları ve klasörleri takılı birim toolocal konumdan kopyalama ve yapıştırma](./media/backup-azure-restore-windows-server/samemachine_copy_instantrestore.png)

9. <span data-ttu-id="b772e-144">İşiniz bittiğinde geri yükleme hello dosyaları ve/veya klasörlerde hello **göz atın ve kurtarma dosyaları** bölmesinde tıklatın **çıkarma**.</span><span class="sxs-lookup"><span data-stu-id="b772e-144">When you are finished restoring hello files and/or folders, on hello **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="b772e-145">Ardından **Evet** tooconfirm toounmount hello birim istiyor.</span><span class="sxs-lookup"><span data-stu-id="b772e-145">Then click **Yes** tooconfirm that you want toounmount hello volume.</span></span>

    ![Merhaba birim çıkarın ve onaylayın](./media/backup-azure-restore-windows-server/samemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="b772e-147">Çıkarma değil tıklatırsanız, hello kurtarma birimi zaman takıldı hello zamandan 6 saat boyunca bağlı kalır.</span><span class="sxs-lookup"><span data-stu-id="b772e-147">If you do not click Unmount, hello Recovery Volume will remain mounted for 6 hours from hello time when it was mounted.</span></span> <span data-ttu-id="b772e-148">Ancak, genişletilmiş değerine kadar devam eden bir dosya kopyalama durumunda 24 saat maksimum hello bağlama zamanı geldi.</span><span class="sxs-lookup"><span data-stu-id="b772e-148">However, hello mount time is extended upto a maximum of 24 hours in case of an ongoing file-copy.</span></span> <span data-ttu-id="b772e-149">Merhaba birim bağlıyken hiçbir yedekleme işlemleri çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b772e-149">No backup operations will run while hello volume is mounted.</span></span> <span data-ttu-id="b772e-150">Merhaba kurtarma birimi kaldırılan tamamlandıktan sonra tüm zamanlanmış yedekleme işlemi toorun hello birimin zaman bağlı, hello süre boyunca çalışır.</span><span class="sxs-lookup"><span data-stu-id="b772e-150">Any backup operation scheduled toorun during hello time when hello volume is mounted, will run after hello recovery volume is unmounted.</span></span>
    >


## <a name="use-instant-restore-toorestore-data-tooan-alternate-machine"></a><span data-ttu-id="b772e-151">Toorestore veri tooan alternatif makine anında geri kullanın</span><span class="sxs-lookup"><span data-stu-id="b772e-151">Use Instant Restore toorestore data tooan alternate machine</span></span>
<span data-ttu-id="b772e-152">Tüm sunucunuzu kaybolursa, verileri Azure yedekleme tooa farklı makineden kurtarmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b772e-152">If your entire server is lost, you can still recover data from Azure Backup tooa different machine.</span></span> <span data-ttu-id="b772e-153">Aşağıdaki adımları hello hello iş akışı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="b772e-153">hello following steps illustrate hello workflow.</span></span>


<span data-ttu-id="b772e-154">Bu adımlarda kullanılan hello terminolojisi içerir:</span><span class="sxs-lookup"><span data-stu-id="b772e-154">hello terminology used in these steps includes:</span></span>

* <span data-ttu-id="b772e-155">*Kaynak makine* – hello özgün makine hangi hello yedekten alındığı ve hangi şu anda kullanılamıyor.</span><span class="sxs-lookup"><span data-stu-id="b772e-155">*Source machine* – hello original machine from which hello backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="b772e-156">*Hedef makine* – hello makine toowhich hello verilerin kurtarıldığı.</span><span class="sxs-lookup"><span data-stu-id="b772e-156">*Target machine* – hello machine toowhich hello data is being recovered.</span></span>
* <span data-ttu-id="b772e-157">*Örnek kasa* – hello kurtarma Hizmetleri kasası toowhich hello *kaynak makine* ve *hedef makine* kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="b772e-157">*Sample vault* – hello Recovery Services vault toowhich hello *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="b772e-158">Yedeklemeler, geri yüklenen tooa hedef makine hello işletim sisteminin önceki bir sürümünü çalıştıran olamaz.</span><span class="sxs-lookup"><span data-stu-id="b772e-158">Backups can't be restored tooa target machine running an earlier version of hello operating system.</span></span> <span data-ttu-id="b772e-159">Örneğin, bir Windows bilgisayarı olabilir 7'den alınan bir yedeklemeyi bilgisayar bir Windows 8 veya daha sonra geri.</span><span class="sxs-lookup"><span data-stu-id="b772e-159">For example, a backup taken from a Windows 7 computer can be restored on a Windows 8, or later, computer.</span></span> <span data-ttu-id="b772e-160">Bir Windows 8 bilgisayardan alınan bir yedeklemeyi geri yüklenen tooa Windows 7 bilgisayar olamaz.</span><span class="sxs-lookup"><span data-stu-id="b772e-160">A backup taken from a Windows 8 computer cannot be restored tooa Windows 7 computer.</span></span>
>
>

1. <span data-ttu-id="b772e-161">Açık hello **Microsoft Azure yedekleme** hello üzerinde içinde Vurgu *hedef makine*.</span><span class="sxs-lookup"><span data-stu-id="b772e-161">Open hello **Microsoft Azure Backup** snap in on hello *Target machine*.</span></span>

2. <span data-ttu-id="b772e-162">Merhaba olun *hedef makine* ve hello *kaynak makine* aynı kurtarma Hizmetleri kasası kayıtlı toohello şunlardır.</span><span class="sxs-lookup"><span data-stu-id="b772e-162">Ensure hello *Target machine* and hello *Source machine* are registered toohello same Recovery Services vault.</span></span>

3. <span data-ttu-id="b772e-163">Tıklatın **verileri kurtarabilirsiniz** tooopen hello **Veri Kurtarma Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="b772e-163">Click **Recover Data** tooopen hello **Recover Data wizard**.</span></span>

    ![Verileri kurtarma](./media/backup-azure-restore-windows-server/recover.png)

4. <span data-ttu-id="b772e-165">Merhaba üzerinde **Başlarken** bölmesinde, **başka bir sunucu**</span><span class="sxs-lookup"><span data-stu-id="b772e-165">On hello **Getting Started** pane, select **Another server**</span></span>

    ![Başka bir sunucu](./media/backup-azure-restore-windows-server/alternatemachine_gettingstarted_instantrestore.png)

5. <span data-ttu-id="b772e-167">Toohello karşılık gelen hello kasa kimlik bilgilerini sağlayın *örnek kasa*, tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="b772e-167">Provide hello vault credential file that corresponds toohello *Sample vault*, and click **Next**.</span></span>

    <span data-ttu-id="b772e-168">Merhaba kasa kimlik bilgilerini geçersiz (veya süresi dolmuş) varsa, yeni bir kasa kimlik bilgilerini hello indirin *örnek kasa* hello Azure Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="b772e-168">If hello vault credential file is invalid (or expired), download a new vault credential file from hello *Sample vault* in hello Azure portal.</span></span> <span data-ttu-id="b772e-169">Geçerli kasa kimlik bilgileri sağladığınızda, yedekleme kasası karşılık gelen hello hello adı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b772e-169">Once you provide a valid vault credential, hello name of hello corresponding Backup Vault appears.</span></span>


6. <span data-ttu-id="b772e-170">Merhaba üzerinde **yedekleme sunucusu seçin** bölmesinde, select hello *kaynak makine* görüntülenmesini makineler hello listesinden ve hello parola girin.</span><span class="sxs-lookup"><span data-stu-id="b772e-170">On hello **Select Backup Server** pane, select hello *Source machine* from hello list of displayed machines and provide hello passphrase.</span></span> <span data-ttu-id="b772e-171">Ardından **İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b772e-171">Then click **Next**.</span></span>

    ![Makineler listesi](./media/backup-azure-restore-windows-server/alternatemachine_selectmachine_instantrestore.png)

7. <span data-ttu-id="b772e-173">Merhaba üzerinde **seçin kurtarma moduna** bölmesinde seçin **dosyalara ve klasörlere** tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="b772e-173">On hello **Select Recovery Mode** pane, select **Individual files and folders** and click **Next**.</span></span>

    ![Arama](./media/backup-azure-restore-windows-server/alternatemachine_selectrecoverymode_instantrestore.png)

8. <span data-ttu-id="b772e-175">Merhaba üzerinde **birim seçin ve tarih** bölmesi, hello dosyaları ve/veya toorestore istediğiniz klasörleri içeren bir select hello birimi.</span><span class="sxs-lookup"><span data-stu-id="b772e-175">On hello **Select Volume and Date** pane, select hello volume that contains hello files and/or folders you want toorestore.</span></span>

    <span data-ttu-id="b772e-176">Merhaba takvimde bir kurtarma noktası seçin.</span><span class="sxs-lookup"><span data-stu-id="b772e-176">On hello calendar, select a recovery point.</span></span> <span data-ttu-id="b772e-177">Zaman içinde herhangi bir kurtarma noktasından geri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b772e-177">You can restore from any recovery point in time.</span></span> <span data-ttu-id="b772e-178">İçinde tarihleri **kalın** hello en az bir kurtarma noktası kullanılabilirliğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="b772e-178">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="b772e-179">Birden fazla kurtarma noktası mevcutsa, bir tarih seçtikten sonra hello hello belirli bir kurtarma noktası seçin **zaman** açılır menü.</span><span class="sxs-lookup"><span data-stu-id="b772e-179">Once you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span>

    ![Arama öğeleri](./media/backup-azure-restore-windows-server/alternatemachine_selectvolumedate_instantrestore.png)

9. <span data-ttu-id="b772e-181">Tıklatın **bağlama** toolocally bağlama hello kurtarma noktası olarak bir kurtarma birimde, *hedef makine*.</span><span class="sxs-lookup"><span data-stu-id="b772e-181">Click **Mount** toolocally mount hello recovery point as a recovery volume on your *Target machine*.</span></span>

10. <span data-ttu-id="b772e-182">Hello üzerinde **Gözat ve kurtarma dosyaları** bölmesinde tıklatın **Gözat** tooopen Windows Gezgini, Bul hello dosya ve klasörleri istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="b772e-182">On hello **Browse and Recover Files** pane, click **Browse** tooopen Windows Explorer and find hello files and folders you want.</span></span>

    ![Şifreleme](./media/backup-azure-restore-windows-server/alternatemachine_browserecover_instantrestore.png)

11. <span data-ttu-id="b772e-184">Windows Gezgini'nde, hello dosyaları ve/veya klasörleri hello kurtarma birimden kopyalayıp bunları tooyour *hedef makine* konumu.</span><span class="sxs-lookup"><span data-stu-id="b772e-184">In Windows Explorer, copy hello files and/or folders from hello recovery volume and paste them tooyour *Target machine* location.</span></span> <span data-ttu-id="b772e-185">Açın veya hello dosyaları doğrudan hello kurtarma birimi akış ve hello sürümleri kurtarılan doğru doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="b772e-185">You can open or stream hello files directly from hello recovery volume and verify hello correct versions are recovered.</span></span>

    ![Şifreleme](./media/backup-azure-restore-windows-server/alternatemachine_copy_instantrestore.png)

12. <span data-ttu-id="b772e-187">İşiniz bittiğinde geri yükleme hello dosyaları ve/veya klasörlerde hello **göz atın ve kurtarma dosyaları** bölmesinde tıklatın **çıkarma**.</span><span class="sxs-lookup"><span data-stu-id="b772e-187">When you are finished restoring hello files and/or folders, on hello **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="b772e-188">Ardından **Evet** tooconfirm toounmount hello birim istiyor.</span><span class="sxs-lookup"><span data-stu-id="b772e-188">Then click **Yes** tooconfirm that you want toounmount hello volume.</span></span>

    ![Şifreleme](./media/backup-azure-restore-windows-server/alternatemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="b772e-190">Çıkarma değil tıklatırsanız, hello kurtarma birimi zaman takıldı hello zamandan 6 saat boyunca bağlı kalır.</span><span class="sxs-lookup"><span data-stu-id="b772e-190">If you do not click Unmount, hello Recovery Volume will remain mounted for 6 hours from hello time when it was mounted.</span></span> <span data-ttu-id="b772e-191">Ancak, genişletilmiş değerine kadar devam eden bir dosya kopyalama durumunda 24 saat maksimum hello bağlama zamanı geldi.</span><span class="sxs-lookup"><span data-stu-id="b772e-191">However, hello mount time is extended upto a maximum of 24 hours in case of an ongoing file-copy.</span></span> <span data-ttu-id="b772e-192">Merhaba birim bağlıyken hiçbir yedekleme işlemleri çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b772e-192">No backup operations will run while hello volume is mounted.</span></span> <span data-ttu-id="b772e-193">Merhaba kurtarma birimi kaldırılan tamamlandıktan sonra tüm zamanlanmış yedekleme işlemi toorun hello birimin zaman bağlı, hello süre boyunca çalışır.</span><span class="sxs-lookup"><span data-stu-id="b772e-193">Any backup operation scheduled toorun during hello time when hello volume is mounted, will run after hello recovery volume is unmounted.</span></span>
    >

## <a name="troubleshooting"></a><span data-ttu-id="b772e-194">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="b772e-194">Troubleshooting</span></span>
<span data-ttu-id="b772e-195">Azure Backup hello kurtarma birimi başarıyla tıklama bile birkaç dakika sonra bağlamaz varsa **bağlama** veya başarısız toomount hello kurtarma birimi bir veya daha fazla hata ile normalde kurtarma toobegin hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="b772e-195">If Azure Backup does not successfully mount hello recovery volume even after several minutes of clicking **Mount** or fails toomount hello recovery volume with one or more errors, follow hello steps below toobegin recovering normally.</span></span>

1.  <span data-ttu-id="b772e-196">Birkaç dakika çalışıyor durumda hello devam eden bağlama işlemi iptal edin.</span><span class="sxs-lookup"><span data-stu-id="b772e-196">Cancel hello ongoing mount process in case it has been running for several minutes.</span></span>

2.  <span data-ttu-id="b772e-197">Merhaba üzerinde hello Azure yedekleme Aracısı'nın en son sürüm olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="b772e-197">Ensure that you are on hello latest version of hello Azure Backup agent.</span></span> <span data-ttu-id="b772e-198">Merhaba sürüm bilgilerini Azure yedekleme Aracısı'nın çıkışı toofind tıklayın **hakkında Microsoft Azure kurtarma Hizmetleri Aracısı** hello üzerinde **Eylemler** Microsoft Azure yedekleme bölmesinde konsol ve o hello eminolun **Sürüm** eşit tooor belirtilen hello sürümden daha yüksek sayıdır [bu makalede](https://go.microsoft.com/fwlink/?linkid=229525).</span><span class="sxs-lookup"><span data-stu-id="b772e-198">toofind out hello version information of Azure Backup agent, click on **About Microsoft Azure Recovery Services Agent** on hello **Actions** pane of Microsoft Azure Backup console and ensure that hello **Version** number is equal tooor higher than hello version mentioned in [this article](https://go.microsoft.com/fwlink/?linkid=229525).</span></span> <span data-ttu-id="b772e-199">Merhaba en son sürümü karşıdan [burada](https://go.microsoft.com/fwLink/?LinkID=288905)</span><span class="sxs-lookup"><span data-stu-id="b772e-199">You can download hello latest version from [here](https://go.microsoft.com/fwLink/?LinkID=288905)</span></span>

3.  <span data-ttu-id="b772e-200">Çok Git**Aygıt Yöneticisi'ni** -> **depolama alanı denetleyicileri** ve, bulabilmesini sağlama **Microsoft iSCSI başlatıcısı**.</span><span class="sxs-lookup"><span data-stu-id="b772e-200">Go too**Device Manager** -> **Storage Controllers** and ensure that you can locate **Microsoft iSCSI Initiator**.</span></span> <span data-ttu-id="b772e-201">Bulabiliyorsa, doğrudan toostep 7 aşağıdaki gidin.</span><span class="sxs-lookup"><span data-stu-id="b772e-201">If you can locate it, directly go toostep 7 below.</span></span> 

4.  <span data-ttu-id="b772e-202">Adım 3'te belirtildiği gibi Microsoft iSCSI başlatıcısı hizmetinin bulamazsanız, bir giriş altında bulabilirsiniz toosee denetleyin **Aygıt Yöneticisi'ni** -> **depolama alanı denetleyicileri** adlı  **Bilinmeyen aygıt** donanım kimliği ile **ROOT\ISCSIPRT**.</span><span class="sxs-lookup"><span data-stu-id="b772e-202">If you cannot locate Microsoft iSCSI Initiator service as mentioned in step 3, check toosee if you can find an entry under **Device Manager** -> **Storage Controllers** called **Unknown Device** with Hardware ID **ROOT\ISCSIPRT**.</span></span>

5.  <span data-ttu-id="b772e-203">Sağ tıklayın **bilinmeyen aygıt** seçip **sürücü yazılımı güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="b772e-203">Right click on **Unknown Device** and select **Update Driver Software**.</span></span>

6.  <span data-ttu-id="b772e-204">Merhaba seçeneği çok seçerek güncelleştirme hello sürücü **otomatik olarak güncelleştirilen sürücü yazılım Ara**.</span><span class="sxs-lookup"><span data-stu-id="b772e-204">Update hello driver by selecting hello option too **Search automatically for updated driver software**.</span></span> <span data-ttu-id="b772e-205">Hello güncelleştirmesinin tamamlanması değiştirmek **bilinmeyen aygıt** çok**Microsoft iSCSI başlatıcısı** aşağıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="b772e-205">Completion of hello update should change **Unknown Device** too**Microsoft iSCSI Initiator** as shown below.</span></span> 

    ![Şifreleme](./media/backup-azure-restore-windows-server/UnknowniSCSIDevice.png)

7.  <span data-ttu-id="b772e-207">Çok Git**Görev Yöneticisi'ni** -> **hizmetler (yerel)** -> **Microsoft iSCSI başlatıcısı hizmetini**.</span><span class="sxs-lookup"><span data-stu-id="b772e-207">Go too**Task Manager** -> **Services (Local)** -> **Microsoft iSCSI Initiator Service**.</span></span> 

    ![Şifreleme](./media/backup-azure-restore-windows-server/MicrosoftInitiatorServiceRunning.png)
    
8.  <span data-ttu-id="b772e-209">Tıklayarak, hello hizmetini sağ tıklayarak Hello Microsoft iSCSI başlatıcısı hizmetinin yeniden **durdurmak** ve sağ yeniden tıklatıp tıklayarak daha fazla **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="b772e-209">Restart hello Microsoft iSCSI Initiator service by right-clicking on hello service, clicking on **Stop** and further right clicking again and clicking on **Start**.</span></span>

9.  <span data-ttu-id="b772e-210">Anlık geri yükleme özelliğini kullanarak kurtarma yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="b772e-210">Retry recovering using Instant Restore.</span></span> 

<span data-ttu-id="b772e-211">Merhaba kurtarma yine başarısız olursa, sunucu/istemci yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="b772e-211">If hello recovery still fails, reboot your server/client.</span></span> <span data-ttu-id="b772e-212">Yeniden başlatma arzu değil veya hello kurtarma başarısız hello sunucu bile makine yeniden başlatıldıktan sonra başka bir makineden kurtarmayı deneyin ve çok giderek Azure desteği ile iletişim kurun[Azure Portal](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) ve bir destek isteği gönderiliyor.</span><span class="sxs-lookup"><span data-stu-id="b772e-212">If a reboot is not desirable or hello recovery still fails even after rebooting hello server, try recovering from an Alternate Machine, and contact Azure Support by going too[Azure Portal](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) and submitting a support request.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b772e-213">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b772e-213">Next steps</span></span>
* <span data-ttu-id="b772e-214">Dosya ve klasörleri kurtarma yaptıktan, yapabilecekleriniz [Yedeklemelerinizin yönetmek](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="b772e-214">Now that you've recovered your files and folders, you can [manage your backups](backup-azure-manage-windows-server.md).</span></span>
