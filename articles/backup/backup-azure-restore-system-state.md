---
title: "Azure yedekleme: Sistem durumunu geri yükle tooa Windows Server | Microsoft Docs"
description: "Windows Server sistem durumu azure'da bir yedekten geri yüklemek için adım açıklama tarafından adım."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/18/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: a45506507f53e2744350d3b6b2e52f1db415de4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-system-state-toowindows-server"></a><span data-ttu-id="ad17e-103">Sistem durumunu geri yükle tooWindows sunucu</span><span class="sxs-lookup"><span data-stu-id="ad17e-103">Restore System State tooWindows Server</span></span>

<span data-ttu-id="ad17e-104">Bu makalede nasıl toorestore Windows Server sistem durumu yedeklemeleri Azure kurtarma Hizmetleri kasası açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ad17e-104">This article explains how toorestore Windows Server System State backups from an Azure Recovery Services vault.</span></span> <span data-ttu-id="ad17e-105">toorestore sistem durumu, bir sistem durumu yedeklemesi olması gerekir (Merhaba yönergelerinde kullanılarak oluşturulan [sistem durumu yedekleme](backup-azure-system-state.md#back-up-windows-server-system-state-preview)) ve hello yüklediğinizden emin olun [hello Microsoft Azure Recovery en son sürümü Hizmetleri (MARS) aracısı](http://aka.ms/azurebackup_agent).</span><span class="sxs-lookup"><span data-stu-id="ad17e-105">toorestore System State, you must have a System State backup (created using hello instructions in [Back up System State](backup-azure-system-state.md#back-up-windows-server-system-state-preview)), and make sure you have installed hello [latest version of hello Microsoft Azure Recovery Services (MARS) agent](http://aka.ms/azurebackup_agent).</span></span> <span data-ttu-id="ad17e-106">Azure kurtarma Hizmetleri Kasası'nı Windows Server Sistem Durumu verilerini kurtarma iki adımlı bir işlemdir:</span><span class="sxs-lookup"><span data-stu-id="ad17e-106">Recovering Windows Server System State data from an Azure Recovery Services vault is a two-step process:</span></span>

1. <span data-ttu-id="ad17e-107">Sistem durumu, Azure yedekleme dosyalarını farklı geri yükle.</span><span class="sxs-lookup"><span data-stu-id="ad17e-107">Restore System State as files from Azure Backup.</span></span> <span data-ttu-id="ad17e-108">Azure yedekleme dosyalarından olarak sistem durum geri yüklerken şunlardan birini yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ad17e-108">When restoring System State as files from Azure Backup, you can either:</span></span>
  * <span data-ttu-id="ad17e-109">Sistem durumunu geri yükle toohello burada hello yedeklemeleri gerçekleştirilecek, aynı sunucuya veya</span><span class="sxs-lookup"><span data-stu-id="ad17e-109">Restore System State toohello same server where hello backups were taken, or</span></span>
  * <span data-ttu-id="ad17e-110">Sistem durumunu geri yükle dosya tooan alternatif sunucusu.</span><span class="sxs-lookup"><span data-stu-id="ad17e-110">Restore System State file tooan alternate server.</span></span>

2. <span data-ttu-id="ad17e-111">Geri hello sistem durumu dosyaları tooa Windows Server uygulayın.</span><span class="sxs-lookup"><span data-stu-id="ad17e-111">Apply hello restored System State files tooa Windows Server.</span></span>


## <a name="recover-system-state-files-toohello-same-server"></a><span data-ttu-id="ad17e-112">Sistem durumunu kurtarma dosyaları toohello aynı sunucu</span><span class="sxs-lookup"><span data-stu-id="ad17e-112">Recover System State files toohello same server</span></span>
<span data-ttu-id="ad17e-113">Aşağıdaki adımları hello nasıl tooroll, Windows Server yapılandırması tooa önceki durumuna geri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ad17e-113">hello following steps explain how tooroll back your Windows Server configuration tooa previous state.</span></span> <span data-ttu-id="ad17e-114">Sunucunuz, kararlı durum bilinen yapılandırma geri tooa çalışırken çok yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="ad17e-114">Rolling your server configuration back tooa known, stable state, can be extremely valuable.</span></span> <span data-ttu-id="ad17e-115">Kurtarma Hizmetleri Kasası'nı adımları geri yükleme hello sunucunun sistem durumunu izleyen hello.</span><span class="sxs-lookup"><span data-stu-id="ad17e-115">hello following steps restore hello server's System State from a Recovery Services vault.</span></span> 

1. <span data-ttu-id="ad17e-116">Açık hello **Microsoft Azure yedekleme** ek bileşenini.</span><span class="sxs-lookup"><span data-stu-id="ad17e-116">Open hello **Microsoft Azure Backup** snap-in.</span></span> <span data-ttu-id="ad17e-117">Merhaba ek bileşenini yüklendiği bilmiyorsanız, hello bilgisayar veya sunucu için arama **Microsoft Azure yedekleme**.</span><span class="sxs-lookup"><span data-stu-id="ad17e-117">If you don't know where hello snap-in was installed, search hello computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="ad17e-118">Merhaba masaüstü uygulaması hello arama sonuçlarında görüntülenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="ad17e-118">hello desktop app should appear in hello search results.</span></span>

2. <span data-ttu-id="ad17e-119">Tıklatın **verileri kurtarabilirsiniz** toostart hello Sihirbazı.</span><span class="sxs-lookup"><span data-stu-id="ad17e-119">Click **Recover Data** toostart hello wizard.</span></span>

    ![Verileri kurtarma](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="ad17e-121">Merhaba üzerinde **Başlarken** bölmesi, toorestore hello veri toohello aynı sunucu bilgisayar seçin veya **bu sunucu (`<server name>`)** tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="ad17e-121">On hello **Getting Started** pane, toorestore hello data toohello same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![Bu sunucu seçeneği toorestore hello veri toohello seçin aynı makine](./media/backup-azure-restore-system-state/samemachine.png)

4. <span data-ttu-id="ad17e-123">Merhaba üzerinde **seçin kurtarma moduna** bölmesinde seçin **sistem durumu** ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="ad17e-123">On hello **Select Recovery Mode** pane, choose **System State** and then click **Next**.</span></span>

    ![Gözatma dosyaları](./media/backup-azure-restore-system-state/recover-type-selection.png)

5. <span data-ttu-id="ad17e-125">Merhaba takvimde **birim seçin ve tarih** bölmesinde seçin kurtarma noktası.</span><span class="sxs-lookup"><span data-stu-id="ad17e-125">On hello calendar in **Select Volume and Date** pane, select a recovery point.</span></span> 

    <span data-ttu-id="ad17e-126">Zaman içinde herhangi bir kurtarma noktasından geri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ad17e-126">You can restore from any recovery point in time.</span></span> <span data-ttu-id="ad17e-127">İçinde tarihleri **kalın** hello en az bir kurtarma noktası kullanılabilirliğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="ad17e-127">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="ad17e-128">Birden fazla kurtarma noktası mevcutsa, bir tarih seçtikten sonra hello hello belirli bir kurtarma noktası seçin **zaman** açılır menü.</span><span class="sxs-lookup"><span data-stu-id="ad17e-128">Once you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span>

    ![Birimi ve tarih](./media/backup-azure-restore-system-state/select-date.png)

6. <span data-ttu-id="ad17e-130">Merhaba kurtarma noktası toorestore seçtikten sonra tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="ad17e-130">Once you have chosen hello recovery point toorestore, click **Next**.</span></span>

    <span data-ttu-id="ad17e-131">Azure yedekleme hello yerel kurtarma noktası bağlar ve kurtarma birimi olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="ad17e-131">Azure Backup mounts hello local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="ad17e-132">Merhaba sonraki bölme hello hedef hello için sistem durumu dosyaları kurtarılan belirtin ve tıklatın **Gözat** tooopen Windows Gezgini, Bul hello dosya ve klasörleri istiyor.</span><span class="sxs-lookup"><span data-stu-id="ad17e-132">On hello next pane, specify hello destination for hello recovered System State files and click **Browse** tooopen Windows Explorer and find hello files and folders you want.</span></span> <span data-ttu-id="ad17e-133">Merhaba seçeneği **böylece her iki sürümünü de sahip kopya oluşturma**, hello tüm sistem durumu arşiv hello kopyasını oluşturmak yerine var olan bir sistem durumu Dosya arşiv tek tek dosyaların kopyalarını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ad17e-133">hello option, **Create copies so that you have both versions**, creates copies of individual files in an existing System State file archive instead of creating hello copy of hello entire System State archive.</span></span>

    ![Kurtarma Seçenekleri](./media/backup-azure-restore-system-state/recover-as-files.png)

8. <span data-ttu-id="ad17e-135">Merhaba kurtarma Hello ayrıntılarını doğrulayın **onay** bölmesinde ve tıklatın **kurtarmak**.</span><span class="sxs-lookup"><span data-stu-id="ad17e-135">Verify hello details of recovery on hello **Confirmation** pane and click **Recover**.</span></span>

   ![Kurtarma tooacknowledge hello kurtarma eylemini tıklatın](./media/backup-azure-restore-system-state/confirm-recovery.png)

9. <span data-ttu-id="ad17e-137">Kopya hello *WindowsImageBackup* hello kurtarma hedef tooa kritik olmayan birim hello sunucusunun dizin.</span><span class="sxs-lookup"><span data-stu-id="ad17e-137">Copy hello *WindowsImageBackup* directory in hello Recovery destination tooa non-critical volume of hello server.</span></span> <span data-ttu-id="ad17e-138">Genellikle, Windows işletim sistemi birimi hello hello kritik birim değil.</span><span class="sxs-lookup"><span data-stu-id="ad17e-138">Usually, hello Windows OS volume is hello critical volume.</span></span>

10. <span data-ttu-id="ad17e-139">Merhaba kurtarma başarılı olduktan sonra hello hello bölümdeki adımları [Uygula geri sistem durumu dosyaları toohello Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-files-to-the-windows-server), toocomplete hello sistem durumu kurtarma işlemi.</span><span class="sxs-lookup"><span data-stu-id="ad17e-139">Once hello recovery is successful, follow hello steps in hello section, [Apply restored System State files toohello Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-files-to-the-windows-server), toocomplete hello System State recovery process.</span></span>

## <a name="recover-system-state-files-tooan-alternate-server"></a><span data-ttu-id="ad17e-140">Sistem durumunu kurtarma dosyaları tooan diğer sunucu</span><span class="sxs-lookup"><span data-stu-id="ad17e-140">Recover System State files tooan alternate server</span></span>

<span data-ttu-id="ad17e-141">Windows Server'ınızın bozuk veya erişilemez durumda ve toorestore istiyorsanız, Windows Server sistem durumu kurtarma tarafından tooa kararlı durum Merhaba, başka bir sunucudan hello bozuk sunucunun sistem durumu geri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ad17e-141">If your Windows Server is corrupted or inaccessible, and you want toorestore it tooa stable state by recovering hello Windows Server System State, you can restore hello corrupted server's System State from another server.</span></span> <span data-ttu-id="ad17e-142">Adımları toohello geri yükleme Sistem Durumu'nu ayrı bir sunucu üzerinde aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="ad17e-142">Use hello following steps toohello restore System State on a separate server.</span></span>  

<span data-ttu-id="ad17e-143">Bu adımlarda kullanılan hello terminolojisi içerir:</span><span class="sxs-lookup"><span data-stu-id="ad17e-143">hello terminology used in these steps includes:</span></span>

- <span data-ttu-id="ad17e-144">*Kaynak makine* – hello özgün makine hangi hello yedekten alındığı ve hangi şu anda kullanılamıyor.</span><span class="sxs-lookup"><span data-stu-id="ad17e-144">*Source machine* – hello original machine from which hello backup was taken and which is currently unavailable.</span></span>
- <span data-ttu-id="ad17e-145">*Hedef makine* – hello makine toowhich hello verilerin kurtarıldığı.</span><span class="sxs-lookup"><span data-stu-id="ad17e-145">*Target machine* – hello machine toowhich hello data is being recovered.</span></span>
- <span data-ttu-id="ad17e-146">*Örnek kasa* – hello kurtarma Hizmetleri kasası toowhich hello *kaynak makine* ve *hedef makine* kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="ad17e-146">*Sample vault* – hello Recovery Services vault toowhich hello *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="ad17e-147">Bir makineden alınan yedekleri geri yüklenen tooa makine hello işletim sisteminin önceki bir sürümünü çalıştıran olamaz.</span><span class="sxs-lookup"><span data-stu-id="ad17e-147">Backups taken from one machine cannot be restored tooa machine running an earlier version of hello operating system.</span></span> <span data-ttu-id="ad17e-148">Örneğin, bir Windows Server makine olamaz 2016'dan alınan yedeklemeler tooWindows Server 2012 R2 geri.</span><span class="sxs-lookup"><span data-stu-id="ad17e-148">For example, backups taken from a Windows Server 2016 machine can't be restored tooWindows Server 2012 R2.</span></span> <span data-ttu-id="ad17e-149">Ancak, hello ters mümkündür.</span><span class="sxs-lookup"><span data-stu-id="ad17e-149">However, hello inverse is possible.</span></span> <span data-ttu-id="ad17e-150">Windows Server 2012 R2 toorestore Windows Server 2016 yedeklemelerden kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ad17e-150">You can use backups from Windows Server 2012 R2 toorestore Windows Server 2016.</span></span>
>

1. <span data-ttu-id="ad17e-151">Açık hello **Microsoft Azure yedekleme** ek bileşenini hello *hedef makine*.</span><span class="sxs-lookup"><span data-stu-id="ad17e-151">Open hello **Microsoft Azure Backup** snap-in on hello *Target machine*.</span></span>
2. <span data-ttu-id="ad17e-152">Bu hello olun *hedef makine* ve hello *kaynak makine* aynı kurtarma Hizmetleri kasası kayıtlı toohello şunlardır.</span><span class="sxs-lookup"><span data-stu-id="ad17e-152">Ensure that hello *Target machine* and hello *Source machine* are registered toohello same Recovery Services vault.</span></span>
3. <span data-ttu-id="ad17e-153">Tıklatın **verileri kurtarabilirsiniz** tooinitiate hello iş akışı.</span><span class="sxs-lookup"><span data-stu-id="ad17e-153">Click **Recover Data** tooinitiate hello workflow.</span></span>

    ![Verileri kurtarma](./media/backup-azure-restore-windows-server-classic/recover.png)

4. <span data-ttu-id="ad17e-155">Seçin **başka bir sunucu**</span><span class="sxs-lookup"><span data-stu-id="ad17e-155">Select **Another server**</span></span>

    ![Başka bir sunucu](./media/backup-azure-restore-system-state/anotherserver.png)

5. <span data-ttu-id="ad17e-157">Toohello karşılık gelen hello kasa kimlik bilgilerini sağlayın *örnek kasa*.</span><span class="sxs-lookup"><span data-stu-id="ad17e-157">Provide hello vault credential file that corresponds toohello *Sample vault*.</span></span> <span data-ttu-id="ad17e-158">Merhaba kasa kimlik bilgilerini geçersiz (veya süresi dolmuş) varsa, yeni bir kasa kimlik bilgilerini hello indirin *örnek kasa* hello Azure Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="ad17e-158">If hello vault credential file is invalid (or expired), download a new vault credential file from hello *Sample vault* in hello Azure portal.</span></span> <span data-ttu-id="ad17e-159">Merhaba kasa kimlik bilgilerini sağlanan sonra hello kasa kimlik bilgileri dosyasıyla ilişkili hello kurtarma Hizmetleri kasası görünür.</span><span class="sxs-lookup"><span data-stu-id="ad17e-159">Once hello vault credential file is provided, hello Recovery Services vault associated with hello vault credential file appears.</span></span>

6. <span data-ttu-id="ad17e-160">Merhaba Hello yedekleme sunucusu seçin bölmesinde seçin *kaynak makine* görüntülenmesini makineler hello listesinden.</span><span class="sxs-lookup"><span data-stu-id="ad17e-160">On hello Select Backup Server pane, select hello *Source machine* from hello list of displayed machines.</span></span>

    ![Makineler listesi](./media/backup-azure-restore-windows-server-classic/machinelist.png)

7. <span data-ttu-id="ad17e-162">Merhaba seçin kurtarma moduna bölmesinde seçin **sistem durumu** tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="ad17e-162">On hello Select Recovery Mode pane, choose **System State** and click **Next**.</span></span> 

    ![Arama](./media/backup-azure-restore-system-state/recover-type-selection.png)

8. <span data-ttu-id="ad17e-164">Merhaba hello Takvim üzerinde **birim seçin ve tarih** bölmesinde seçin kurtarma noktası.</span><span class="sxs-lookup"><span data-stu-id="ad17e-164">On hello Calendar in hello **Select Volume and Date** pane, select a recovery point.</span></span> <span data-ttu-id="ad17e-165">Zaman içinde herhangi bir kurtarma noktasından geri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ad17e-165">You can restore from any recovery point in time.</span></span> <span data-ttu-id="ad17e-166">İçinde tarihleri **kalın** hello en az bir kurtarma noktası kullanılabilirliğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="ad17e-166">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="ad17e-167">Birden fazla kurtarma noktası mevcutsa, bir tarih seçtikten sonra hello hello belirli bir kurtarma noktası seçin **zaman** açılır menü.</span><span class="sxs-lookup"><span data-stu-id="ad17e-167">Once  you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span> 

    ![Arama öğeleri](./media/backup-azure-restore-system-state/select-date.png)

9. <span data-ttu-id="ad17e-169">Merhaba kurtarma noktası toorestore seçtikten sonra tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="ad17e-169">Once you have chosen hello recovery point toorestore, click **Next**.</span></span>

10. <span data-ttu-id="ad17e-170">Merhaba üzerinde **sistem durumu kurtarma modunu seçin** bölmesinde istediğiniz sistem durumu dosyaları kurtarılan toobe hello hedefini belirtin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="ad17e-170">On hello **Select System State Recovery Mode** pane, specify hello destination where you want System State files toobe recovered, then click **Next**.</span></span>

    ![Şifreleme](./media/backup-azure-restore-system-state/recover-as-files.png)

    <span data-ttu-id="ad17e-172">Merhaba seçeneği **böylece her iki sürümünü de sahip kopya oluşturma**, hello tüm sistem durumu arşiv hello kopyasını oluşturmak yerine var olan bir sistem durumu Dosya arşiv tek tek dosyaların kopyalarını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ad17e-172">hello option, **Create copies so that you have both versions**, creates copies of individual files in an existing System State file archive instead of creating hello copy of hello entire System State archive.</span></span>

11. <span data-ttu-id="ad17e-173">Kurtarma hello onay bölmesinde Hello ayrıntılarını doğrulayın ve tıklatın **kurtarmak**.</span><span class="sxs-lookup"><span data-stu-id="ad17e-173">Verify hello details of recovery on hello Confirmation pane, and click **Recover**.</span></span> 

    ![Merhaba Kurtar düğmesi tooconfirm hello kurtarma işlemi'ı tıklatın](./media/backup-azure-restore-system-state/confirm-recovery.png)

12. <span data-ttu-id="ad17e-175">Kopya hello *WindowsImageBackup* directory tooa kritik olmayan birim hello sunucusunun (örneğin D:\).</span><span class="sxs-lookup"><span data-stu-id="ad17e-175">Copy hello *WindowsImageBackup* directory tooa non-critical volume of hello server (for example D:\).</span></span> <span data-ttu-id="ad17e-176">Genellikle Windows işletim sistemi birimi hello hello kritik birim değil.</span><span class="sxs-lookup"><span data-stu-id="ad17e-176">Usually hello Windows OS volume is hello critical volume.</span></span>

13. <span data-ttu-id="ad17e-177">toocomplete hello kurtarma işlemi, kullanım hello aşağıdaki bölümü çok[geri hello sistem durumu dosyaları bir Windows sunucusu üzerindeki geçerli](backup-azure-restore-system-state.md#apply-restored-system-state-on-a-windows-server).</span><span class="sxs-lookup"><span data-stu-id="ad17e-177">toocomplete hello recovery process, use hello following section too[apply hello restored System State files on a Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-on-a-windows-server).</span></span>




## <a name="apply-restored-system-state-on-a-windows-server"></a><span data-ttu-id="ad17e-178">Bir Windows sunucusuna geri yüklenen sistem durumu Uygula</span><span class="sxs-lookup"><span data-stu-id="ad17e-178">Apply restored System State on a Windows Server</span></span>

<span data-ttu-id="ad17e-179">Azure kurtarma Hizmetleri aracısını kullanarak dosyaları olarak sistem durumu kurtardı sonra kullanım hello Windows Server Yedekleme yardımcı programı tooapply hello sistem durumu tooWindows sunucu kurtarıldı.</span><span class="sxs-lookup"><span data-stu-id="ad17e-179">Once you have recovered System State as files using Azure Recovery Services Agent, use hello Windows Server Backup utility tooapply hello recovered System State tooWindows Server.</span></span> <span data-ttu-id="ad17e-180">Windows Server Yedekleme yardımcı programı Hello hello sunucuda zaten var.</span><span class="sxs-lookup"><span data-stu-id="ad17e-180">hello Windows Server Backup utility is already available on hello server.</span></span> <span data-ttu-id="ad17e-181">Aşağıdaki adımları hello tooapply hello sistem durumu nasıl kurtarılır açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ad17e-181">hello following steps explain how tooapply hello recovered System State.</span></span>

1. <span data-ttu-id="ad17e-182">Sunucunuzun kullanım hello aşağıdaki komutları tooreboot *dizin hizmetleri onarım modunda*.</span><span class="sxs-lookup"><span data-stu-id="ad17e-182">Use hello following commands tooreboot your server in *Directory Services Repair Mode*.</span></span> <span data-ttu-id="ad17e-183">Yükseltilmiş bir komut istemi'nde:</span><span class="sxs-lookup"><span data-stu-id="ad17e-183">In an elevated command prompt:</span></span>

    ```
    PS C:\> Bcdedit /set safeboot dsrepair
    PS C:\> Shutdown /r /t 0
    ```

2. <span data-ttu-id="ad17e-184">Merhaba yeniden başlatıldıktan sonra hello Windows Server Yedekleme ek bileşenini açın.</span><span class="sxs-lookup"><span data-stu-id="ad17e-184">After hello reboot, open hello Windows Server Backup snap-in.</span></span> <span data-ttu-id="ad17e-185">Merhaba ek bileşenini yüklendiği bilmiyorsanız, hello bilgisayar veya sunucu için arama **Windows Server Yedekleme**.</span><span class="sxs-lookup"><span data-stu-id="ad17e-185">If you don't know where hello snap-in was installed, search hello computer or server for **Windows Server Backup**.</span></span>

    <span data-ttu-id="ad17e-186">Merhaba Masaüstü uygulama hello arama sonuçlarında görünür.</span><span class="sxs-lookup"><span data-stu-id="ad17e-186">hello desktop app appears in hello search results.</span></span>

3. <span data-ttu-id="ad17e-187">Merhaba ek bileşeninde, seçin **yerel yedekleme**.</span><span class="sxs-lookup"><span data-stu-id="ad17e-187">In hello snap-in, select **Local Backup**.</span></span>

    ![Yerel yedekleme toorestore buradan seçin](./media/backup-azure-restore-system-state/win-server-backup-local-backup.png)

4. <span data-ttu-id="ad17e-189">Merhaba de hello yerel yedekleme konsolunda üzerinde **Eylemler bölmesinde**, tıklatın **kurtarmak** tooopen hello Kurtarma Sihirbazı.</span><span class="sxs-lookup"><span data-stu-id="ad17e-189">On hello Local Backup console, in hello **Actions Pane**, click **Recover** tooopen hello Recovery Wizard.</span></span>

5. <span data-ttu-id="ad17e-190">Merhaba seçeneğini **başka bir konumda depolanan bir yedek**, tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="ad17e-190">Select hello option, **A backup stored in another location**, and click **Next**.</span></span>

   ![toorecover tooa farklı bir sunucu seçin](./media/backup-azure-restore-system-state/backup-stored-in-diff-location.png)

6. <span data-ttu-id="ad17e-192">Merhaba konum türü belirtirken seçin **uzaktan paylaşılan klasörünü** , sistem durumu yedeklemesi kurtarılan tooanother sunucusuysa.</span><span class="sxs-lookup"><span data-stu-id="ad17e-192">When specifying hello location type, select **Remote shared folder** if your System State backup was recovered tooanother server.</span></span> <span data-ttu-id="ad17e-193">Sistem durumu yerel olarak yapılıyorsa, ardından **yerel sürücüler**.</span><span class="sxs-lookup"><span data-stu-id="ad17e-193">If your System State was recovered locally, then select **Local drives**.</span></span> 

    ![seçin olup olmadığını yerel sunucu ya da başka bir toorecovery](./media/backup-azure-restore-system-state/ss-recovery-remote-shared-folder.png)

7. <span data-ttu-id="ad17e-195">Merhaba yolu toohello girin *WindowsImageBackup* dizin veya hello sistem durumu dosyaları kurtarma Azure Kurtarma'yı kullanarak bir parçası olarak kurtarılan bu dizin (örneğin, D:\WindowsImageBackup) içeren hello yerel sürücüyü seçin Aracı ve tıklatın Hizmetleri **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="ad17e-195">Enter hello path toohello *WindowsImageBackup* directory, or choose hello local drive containing this directory (for example, D:\WindowsImageBackup), recovered as part of hello System State files recovery using Azure Recovery Services Agent and click **Next**.</span></span>

    ![yol toohello paylaşılan dosya](./media/backup-azure-restore-system-state/ss-recovery-remote-folder.png)

8. <span data-ttu-id="ad17e-197">Toorestore istediğiniz ve tıklatın select hello sistem durumu sürüm **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="ad17e-197">Select hello System State version that you want toorestore, and click **Next**.</span></span>

9. <span data-ttu-id="ad17e-198">Merhaba kurtarma türünü seçin bölmesinde seçin **sistem durumu** tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="ad17e-198">In hello Select Recovery Type pane, select **System State** and click **Next**.</span></span>

10. <span data-ttu-id="ad17e-199">Merhaba sistem durumu kurtarma konumunu Hello için seçin **özgün konumuna**, tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="ad17e-199">For hello location of hello System State Recovery, select **Original Location**, and click **Next**.</span></span>

11. <span data-ttu-id="ad17e-200">Hello onayı ayrıntıları gözden geçirin, hello yeniden başlatma ayarlarını doğrulayın ve tıklatın **kurtarmak** tooapplly hello geri sistem durumu dosyaları.</span><span class="sxs-lookup"><span data-stu-id="ad17e-200">Review hello confirmation details, verify hello reboot settings, and click **Recover** tooapplly hello restored System State files.</span></span>

    ![başlatma hello sistem durumu dosyaları geri yükle](./media/backup-azure-restore-system-state/launch-ss-recovery.png)

## <a name="special-considerations-for-system-state-recovery-on-active-directory-server"></a><span data-ttu-id="ad17e-202">Active Directory sunucuda sistem durumu kurtarma için özel hususlar</span><span class="sxs-lookup"><span data-stu-id="ad17e-202">Special considerations for System State recovery on Active Directory server</span></span>

<span data-ttu-id="ad17e-203">Sistem durumu yedeklemesi Active Directory verilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="ad17e-203">System State backup includes Active Directory data.</span></span> <span data-ttu-id="ad17e-204">Adımları toorestore Active Directory etki alanı hizmeti (AD DS) geçerli durumu tooa önceki durumunu izleyen hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="ad17e-204">Use hello following steps toorestore Active Directory Domain Service (AD DS) from its current state tooa previous state.</span></span>

1. <span data-ttu-id="ad17e-205">Merhaba etki alanı denetleyicisi Dizin Hizmetleri geri yükleme modu (DSRM) yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="ad17e-205">Restart hello domain controller in Directory Services Restore Mode (DSRM).</span></span>
2. <span data-ttu-id="ad17e-206">Merhaba adımları [burada](https://technet.microsoft.com/en-us/library/cc794755(v=ws.10).aspx) toouse Windows Server Yedekleme cmdlet'leri toorecover AD DS.</span><span class="sxs-lookup"><span data-stu-id="ad17e-206">Follow hello steps [here](https://technet.microsoft.com/en-us/library/cc794755(v=ws.10).aspx) toouse Windows Server Backup cmdlets toorecover AD DS.</span></span>


## <a name="troubleshoot-failed-system-state-restore"></a><span data-ttu-id="ad17e-207">Başarısız sistem durumu geri yükleme sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="ad17e-207">Troubleshoot failed System State restore</span></span>

<span data-ttu-id="ad17e-208">Sistem durumu uygulama hello önceki işlem başarıyla tamamlanmazsa, Windows Server'ınızın hello Windows Kurtarma Ortamı'nı (Win RE) toorecover kullanın.</span><span class="sxs-lookup"><span data-stu-id="ad17e-208">If hello previous process of applying System State does not complete successfully, use hello Windows Recovery Environment (Win RE) toorecover your Windows Server.</span></span> <span data-ttu-id="ad17e-209">Merhaba aşağıdaki adımlarda açıklanmaktadır nasıl toorecover Win yeniden kullanma.</span><span class="sxs-lookup"><span data-stu-id="ad17e-209">hello following steps explain how toorecover using Win RE.</span></span> <span data-ttu-id="ad17e-210">Yalnızca Windows Server normalde bir sistem durumu geri yüklendikten sonra önyükleme yapmaz, bu seçeneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="ad17e-210">Use This option only if Windows Server does not boot normally after a System State restore.</span></span> <span data-ttu-id="ad17e-211">işlemi aşağıdaki hello sistem dışı verileri, dikkatli siler.</span><span class="sxs-lookup"><span data-stu-id="ad17e-211">hello following process erases non-system data, use caution.</span></span> 

1. <span data-ttu-id="ad17e-212">Windows Server'ınızın Windows Kurtarma Ortamı'nı (Win RE) hello önyükleyin.</span><span class="sxs-lookup"><span data-stu-id="ad17e-212">Boot your Windows Server into hello Windows Recovery Environment (Win RE).</span></span>

2. <span data-ttu-id="ad17e-213">Sorun giderme hello üç kullanılabilir seçenekleri seçin.</span><span class="sxs-lookup"><span data-stu-id="ad17e-213">Select Troubleshoot from hello three available options.</span></span>

    ![Açılış menüsü](./media/backup-azure-restore-system-state/winre-1.png)

3. <span data-ttu-id="ad17e-215">Merhaba gelen **Gelişmiş Seçenekler** ekran, select **komut istemi** hello server yönetici kullanıcı adı ve parolasını girin.</span><span class="sxs-lookup"><span data-stu-id="ad17e-215">From hello **Advanced Options** screen, select **Command Prompt** and provide hello server administrator username and password.</span></span>

   ![Açılış menüsü](./media/backup-azure-restore-system-state/winre-2.png)

4. <span data-ttu-id="ad17e-217">Merhaba server yönetici kullanıcı adı ve parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="ad17e-217">Provide hello server administrator username and password.</span></span>

    ![Açılış menüsü](./media/backup-azure-restore-system-state/winre-3.png)

5. <span data-ttu-id="ad17e-219">Yönetici modunda hello komut istemi açın, aşağıdaki komut tooget hello sistem durumu yedekleme sürümlerini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ad17e-219">When you open hello command prompt in administrator mode, run following command tooget hello System State backup versions.</span></span>

    ```
    Wbadmin get versions -backuptarget:<Volume where WindowsImageBackup folder is copied>:
    ```
    ![Sistem Durumu yedekleme sürümlerini alma](./media/backup-azure-restore-system-state/winre-4.png)

6. <span data-ttu-id="ad17e-221">Komut tooget aşağıdaki hello hello yedeklemeye kullanılabilir tüm birimleri çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ad17e-221">Run hello following command tooget all volumes available in hello backup.</span></span>

    ```
    Wbadmin get items -version:<copy version from above step> -backuptarget:<Backup volume>
    ```

    ![Sistem Durumu yedekleme sürümlerini alma](./media/backup-azure-restore-system-state/winre-5.png)

7. <span data-ttu-id="ad17e-223">Merhaba aşağıdaki komutu hello sistem durumu yedeklemesi parçası olan tüm birimleri kurtarır.</span><span class="sxs-lookup"><span data-stu-id="ad17e-223">hello following command recovers all volumes that are part of hello System State Backup.</span></span> <span data-ttu-id="ad17e-224">Bu adım yalnızca hello sistem durumu parçası olan hello kritik birimler kurtarır unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ad17e-224">Note that this step recovers only hello critical volumes that are part of hello System State.</span></span> <span data-ttu-id="ad17e-225">Tüm sistem dışı veriler silinir.</span><span class="sxs-lookup"><span data-stu-id="ad17e-225">All non-System data is erased.</span></span>

    ```
    Wbadmin start recovery -items:C: -itemtype:Volume -version:<Backupversion> -backuptarget:<backup target volume>
    ```
     ![Sistem Durumu yedekleme sürümlerini alma](./media/backup-azure-restore-system-state/winre-6.png)



## <a name="next-steps"></a><span data-ttu-id="ad17e-227">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ad17e-227">Next steps</span></span>
* <span data-ttu-id="ad17e-228">Dosya ve klasörleri kurtarma yaptıktan, yapabilecekleriniz [Yedeklemelerinizin yönetmek](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="ad17e-228">Now that you've recovered your files and folders, you can [manage your backups](backup-azure-manage-windows-server.md).</span></span>
