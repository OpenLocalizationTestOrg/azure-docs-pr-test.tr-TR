---
title: "Azure yedekleme: Bir Windows Server sistem durumunu geri yükle | Microsoft Docs"
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
ms.openlocfilehash: 320c85f8045d9b72cf7f430d2e2736ba8e5ec269
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="restore-system-state-to-windows-server"></a><span data-ttu-id="856ad-103">Windows Server sistem durumunu geri yükle</span><span class="sxs-lookup"><span data-stu-id="856ad-103">Restore System State to Windows Server</span></span>

<span data-ttu-id="856ad-104">Bu makalede, Azure kurtarma Hizmetleri Kasası'nı Windows Server sistem durumu yedeği açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="856ad-104">This article explains how to restore Windows Server System State backups from an Azure Recovery Services vault.</span></span> <span data-ttu-id="856ad-105">Sistem durumunu geri yüklemek için bir sistem durumu yedeklemesi olmalıdır ('ndaki yönergeleri kullanarak oluşturduğunuz [sistem durumu yedekleme](backup-azure-system-state.md#back-up-windows-server-system-state-preview)) ve yüklediğinizden emin olun [en son sürümünü Microsoft Azure Recovery Services'ın (MARS) Aracı](http://aka.ms/azurebackup_agent).</span><span class="sxs-lookup"><span data-stu-id="856ad-105">To restore System State, you must have a System State backup (created using the instructions in [Back up System State](backup-azure-system-state.md#back-up-windows-server-system-state-preview)), and make sure you have installed the [latest version of the Microsoft Azure Recovery Services (MARS) agent](http://aka.ms/azurebackup_agent).</span></span> <span data-ttu-id="856ad-106">Azure kurtarma Hizmetleri Kasası'nı Windows Server Sistem Durumu verilerini kurtarma iki adımlı bir işlemdir:</span><span class="sxs-lookup"><span data-stu-id="856ad-106">Recovering Windows Server System State data from an Azure Recovery Services vault is a two-step process:</span></span>

1. <span data-ttu-id="856ad-107">Sistem durumu, Azure yedekleme dosyalarını farklı geri yükle.</span><span class="sxs-lookup"><span data-stu-id="856ad-107">Restore System State as files from Azure Backup.</span></span> <span data-ttu-id="856ad-108">Azure yedekleme dosyalarından olarak sistem durum geri yüklerken şunlardan birini yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="856ad-108">When restoring System State as files from Azure Backup, you can either:</span></span>
  * <span data-ttu-id="856ad-109">Burada yedeklemeleri gerçekleştirilecek, geri yükleme sistem durumu aynı sunucuya veya</span><span class="sxs-lookup"><span data-stu-id="856ad-109">Restore System State to the same server where the backups were taken, or</span></span>
  * <span data-ttu-id="856ad-110">Başka bir sunucu dosyasına sistem durumunu geri yükle.</span><span class="sxs-lookup"><span data-stu-id="856ad-110">Restore System State file to an alternate server.</span></span>

2. <span data-ttu-id="856ad-111">Geri yüklenen sistem durumu dosyaları, Windows Server için geçerli.</span><span class="sxs-lookup"><span data-stu-id="856ad-111">Apply the restored System State files to a Windows Server.</span></span>


## <a name="recover-system-state-files-to-the-same-server"></a><span data-ttu-id="856ad-112">Aynı sunucu sistem durumunu kurtarma dosyaları</span><span class="sxs-lookup"><span data-stu-id="856ad-112">Recover System State files to the same server</span></span>
<span data-ttu-id="856ad-113">Aşağıdaki adımlar, Windows Server yapılandırmanızı önceki bir duruma geri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="856ad-113">The following steps explain how to roll back your Windows Server configuration to a previous state.</span></span> <span data-ttu-id="856ad-114">Sunucu yapılandırması için bilinen, kararlı bir duruma geri, son derece yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="856ad-114">Rolling your server configuration back to a known, stable state, can be extremely valuable.</span></span> <span data-ttu-id="856ad-115">Aşağıdaki adımlar sunucunun sistem durumu kurtarma Hizmetleri Kasası'nı geri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="856ad-115">The following steps restore the server's System State from a Recovery Services vault.</span></span> 

1. <span data-ttu-id="856ad-116">Açık **Microsoft Azure yedekleme** ek bileşenini.</span><span class="sxs-lookup"><span data-stu-id="856ad-116">Open the **Microsoft Azure Backup** snap-in.</span></span> <span data-ttu-id="856ad-117">Ek bileşenini yüklendiği bilmiyorsanız, bilgisayar veya sunucu için arama **Microsoft Azure yedekleme**.</span><span class="sxs-lookup"><span data-stu-id="856ad-117">If you don't know where the snap-in was installed, search the computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="856ad-118">Masaüstü uygulaması arama sonuçlarında görüntülenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="856ad-118">The desktop app should appear in the search results.</span></span>

2. <span data-ttu-id="856ad-119">Tıklatın **verileri kurtarabilirsiniz** Sihirbazı'nı başlatın.</span><span class="sxs-lookup"><span data-stu-id="856ad-119">Click **Recover Data** to start the wizard.</span></span>

    ![Verileri kurtarma](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="856ad-121">Üzerinde **Başlarken** verileri aynı sunucu veya bilgisayara geri yüklemek için bölmeyi seçin **bu sunucunun (`<server name>`)** tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="856ad-121">On the **Getting Started** pane, to restore the data to the same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![Bu sunucu seçeneği aynı makineye verileri geri yüklemek için](./media/backup-azure-restore-system-state/samemachine.png)

4. <span data-ttu-id="856ad-123">Üzerinde **seçin kurtarma moduna** bölmesinde seçin **sistem durumu** ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="856ad-123">On the **Select Recovery Mode** pane, choose **System State** and then click **Next**.</span></span>

    ![Gözatma dosyaları](./media/backup-azure-restore-system-state/recover-type-selection.png)

5. <span data-ttu-id="856ad-125">Takvimde **birim seçin ve tarih** bölmesinde seçin kurtarma noktası.</span><span class="sxs-lookup"><span data-stu-id="856ad-125">On the calendar in **Select Volume and Date** pane, select a recovery point.</span></span> 

    <span data-ttu-id="856ad-126">Zaman içinde herhangi bir kurtarma noktasından geri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="856ad-126">You can restore from any recovery point in time.</span></span> <span data-ttu-id="856ad-127">İçinde tarihleri **kalın** en az bir kurtarma noktası kullanılabilirliğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="856ad-127">Dates in **bold** indicate the availability of at least one recovery point.</span></span> <span data-ttu-id="856ad-128">Birden fazla kurtarma noktası mevcutsa, bir tarih seçtikten sonra belirli bir kurtarma noktasından seçin **zaman** açılır menü.</span><span class="sxs-lookup"><span data-stu-id="856ad-128">Once you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span></span>

    ![Birimi ve tarih](./media/backup-azure-restore-system-state/select-date.png)

6. <span data-ttu-id="856ad-130">Geri yüklemek için kurtarma noktası seçtikten sonra tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="856ad-130">Once you have chosen the recovery point to restore, click **Next**.</span></span>

    <span data-ttu-id="856ad-131">Azure yedekleme, yerel kurtarma noktası bağlar ve kurtarma birimi olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="856ad-131">Azure Backup mounts the local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="856ad-132">Sonraki bölmesinde, kurtarılan sistem durumu dosyaları hedefini belirtin ve tıklatın **Gözat** Windows Gezgini'ni açın ve istediğiniz klasörleri ve dosyaları bulmak için.</span><span class="sxs-lookup"><span data-stu-id="856ad-132">On the next pane, specify the destination for the recovered System State files and click **Browse** to open Windows Explorer and find the files and folders you want.</span></span> <span data-ttu-id="856ad-133">Seçenek **böylece her iki sürümünü de sahip kopya oluşturma**, tüm sistem durumu arşiv kopyasını oluşturmak yerine var olan bir sistem durumu Dosya arşiv tek tek dosyaların kopyalarını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="856ad-133">The option, **Create copies so that you have both versions**, creates copies of individual files in an existing System State file archive instead of creating the copy of the entire System State archive.</span></span>

    ![Kurtarma Seçenekleri](./media/backup-azure-restore-system-state/recover-as-files.png)

8. <span data-ttu-id="856ad-135">Kurtarma ayrıntılarını doğrulayın **onay** bölmesinde ve tıklatın **kurtarmak**.</span><span class="sxs-lookup"><span data-stu-id="856ad-135">Verify the details of recovery on the **Confirmation** pane and click **Recover**.</span></span>

   ![kurtarma eylemi onaylamak için Kurtar'ı tıklatın](./media/backup-azure-restore-system-state/confirm-recovery.png)

9. <span data-ttu-id="856ad-137">Kopya *WindowsImageBackup* sunucunun kritik olmayan bir birim için kurtarma hedef dizin.</span><span class="sxs-lookup"><span data-stu-id="856ad-137">Copy the *WindowsImageBackup* directory in the Recovery destination to a non-critical volume of the server.</span></span> <span data-ttu-id="856ad-138">Genellikle, Windows işletim sistemi birimi kritik bir birimdir.</span><span class="sxs-lookup"><span data-stu-id="856ad-138">Usually, the Windows OS volume is the critical volume.</span></span>

10. <span data-ttu-id="856ad-139">Kurtarma başarılı olduktan sonra bölümdeki adımları [Uygula Windows Server için sistem durumu dosyaları geri](backup-azure-restore-system-state.md#apply-restored-system-state-files-to-the-windows-server), sistem durumu kurtarma işlemini tamamlamak için.</span><span class="sxs-lookup"><span data-stu-id="856ad-139">Once the recovery is successful, follow the steps in the section, [Apply restored System State files to the Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-files-to-the-windows-server), to complete the System State recovery process.</span></span>

## <a name="recover-system-state-files-to-an-alternate-server"></a><span data-ttu-id="856ad-140">Başka bir sunucu sistem durumunu kurtarma dosyaları</span><span class="sxs-lookup"><span data-stu-id="856ad-140">Recover System State files to an alternate server</span></span>

<span data-ttu-id="856ad-141">Windows Server'ınızın bozuk veya erişilemez durumda ise ve Windows Server sistem durumunu kurtarma tarafından kararlı bir duruma geri yüklemek istediğiniz, başka bir sunucudan bozuk sunucunun sistem durumu geri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="856ad-141">If your Windows Server is corrupted or inaccessible, and you want to restore it to a stable state by recovering the Windows Server System State, you can restore the corrupted server's System State from another server.</span></span> <span data-ttu-id="856ad-142">Ayrı bir sunucuda sistem durumu geri yükleme için aşağıdaki adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="856ad-142">Use the following steps to the restore System State on a separate server.</span></span>  

<span data-ttu-id="856ad-143">Bu adımlarda kullanılan terminolojiyi içerir:</span><span class="sxs-lookup"><span data-stu-id="856ad-143">The terminology used in these steps includes:</span></span>

- <span data-ttu-id="856ad-144">*Kaynak makine* – özgün makineden yedeğin alındığı ve hangi şu anda kullanılamıyor.</span><span class="sxs-lookup"><span data-stu-id="856ad-144">*Source machine* – The original machine from which the backup was taken and which is currently unavailable.</span></span>
- <span data-ttu-id="856ad-145">*Hedef makine* – olduğu verilerin kurtarıldığı makine.</span><span class="sxs-lookup"><span data-stu-id="856ad-145">*Target machine* – The machine to which the data is being recovered.</span></span>
- <span data-ttu-id="856ad-146">*Örnek kasa* – kurtarma Hizmetleri kasası için *kaynak makine* ve *hedef makine* kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="856ad-146">*Sample vault* – The Recovery Services vault to which the *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="856ad-147">Bir makineden alınan yedeklemeler, işletim sisteminin önceki bir sürümünü çalıştıran bir bilgisayara geri yüklenemez.</span><span class="sxs-lookup"><span data-stu-id="856ad-147">Backups taken from one machine cannot be restored to a machine running an earlier version of the operating system.</span></span> <span data-ttu-id="856ad-148">Örneğin, bir Windows Server 2016 makineden alınan yedeklemeler Windows Server 2012 R2'ye geri yüklenemez.</span><span class="sxs-lookup"><span data-stu-id="856ad-148">For example, backups taken from a Windows Server 2016 machine can't be restored to Windows Server 2012 R2.</span></span> <span data-ttu-id="856ad-149">Ancak, ters mümkündür.</span><span class="sxs-lookup"><span data-stu-id="856ad-149">However, the inverse is possible.</span></span> <span data-ttu-id="856ad-150">Windows Server 2016 geri yüklemek için Windows Server 2012 R2 yedeklemelerden kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="856ad-150">You can use backups from Windows Server 2012 R2 to restore Windows Server 2016.</span></span>
>

1. <span data-ttu-id="856ad-151">Açık **Microsoft Azure yedekleme** ek bileşenini *hedef makine*.</span><span class="sxs-lookup"><span data-stu-id="856ad-151">Open the **Microsoft Azure Backup** snap-in on the *Target machine*.</span></span>
2. <span data-ttu-id="856ad-152">Emin *hedef makine* ve *kaynak makine* aynı kurtarma Hizmetleri kasasına kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="856ad-152">Ensure that the *Target machine* and the *Source machine* are registered to the same Recovery Services vault.</span></span>
3. <span data-ttu-id="856ad-153">Tıklatın **verileri kurtarabilirsiniz** iş akışını başlatmak için.</span><span class="sxs-lookup"><span data-stu-id="856ad-153">Click **Recover Data** to initiate the workflow.</span></span>

    ![Verileri kurtarma](./media/backup-azure-restore-windows-server-classic/recover.png)

4. <span data-ttu-id="856ad-155">Seçin **başka bir sunucu**</span><span class="sxs-lookup"><span data-stu-id="856ad-155">Select **Another server**</span></span>

    ![Başka bir sunucu](./media/backup-azure-restore-system-state/anotherserver.png)

5. <span data-ttu-id="856ad-157">Karşılık gelen kasa kimlik bilgilerini sağlayın *örnek kasa*.</span><span class="sxs-lookup"><span data-stu-id="856ad-157">Provide the vault credential file that corresponds to the *Sample vault*.</span></span> <span data-ttu-id="856ad-158">Kasa kimlik bilgilerini geçersiz (veya süresi dolmuş) varsa, yeni bir kasa kimlik bilgileri dosyasını indirin *örnek kasa* Azure portalında.</span><span class="sxs-lookup"><span data-stu-id="856ad-158">If the vault credential file is invalid (or expired), download a new vault credential file from the *Sample vault* in the Azure portal.</span></span> <span data-ttu-id="856ad-159">Kasa kimlik bilgilerini sağlanan sonra kasa kimlik bilgileri dosyasıyla ilişkili kurtarma Hizmetleri kasası görünür.</span><span class="sxs-lookup"><span data-stu-id="856ad-159">Once the vault credential file is provided, the Recovery Services vault associated with the vault credential file appears.</span></span>

6. <span data-ttu-id="856ad-160">Yedekleme sunucusu seçin bölmesinde seçin *kaynak makine* görüntülenmesini makineler listesinden.</span><span class="sxs-lookup"><span data-stu-id="856ad-160">On the Select Backup Server pane, select the *Source machine* from the list of displayed machines.</span></span>

    ![Makineler listesi](./media/backup-azure-restore-windows-server-classic/machinelist.png)

7. <span data-ttu-id="856ad-162">Seçim kurtarma moduna bölmesinde seçin **sistem durumu** tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="856ad-162">On the Select Recovery Mode pane, choose **System State** and click **Next**.</span></span> 

    ![Arama](./media/backup-azure-restore-system-state/recover-type-selection.png)

8. <span data-ttu-id="856ad-164">Takvimde **birim seçin ve tarih** bölmesinde seçin kurtarma noktası.</span><span class="sxs-lookup"><span data-stu-id="856ad-164">On the Calendar in the **Select Volume and Date** pane, select a recovery point.</span></span> <span data-ttu-id="856ad-165">Zaman içinde herhangi bir kurtarma noktasından geri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="856ad-165">You can restore from any recovery point in time.</span></span> <span data-ttu-id="856ad-166">İçinde tarihleri **kalın** en az bir kurtarma noktası kullanılabilirliğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="856ad-166">Dates in **bold** indicate the availability of at least one recovery point.</span></span> <span data-ttu-id="856ad-167">Birden fazla kurtarma noktası mevcutsa, bir tarih seçtikten sonra belirli bir kurtarma noktasından seçin **zaman** açılır menü.</span><span class="sxs-lookup"><span data-stu-id="856ad-167">Once  you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span></span> 

    ![Arama öğeleri](./media/backup-azure-restore-system-state/select-date.png)

9. <span data-ttu-id="856ad-169">Geri yüklemek için kurtarma noktası seçtikten sonra tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="856ad-169">Once you have chosen the recovery point to restore, click **Next**.</span></span>

10. <span data-ttu-id="856ad-170">Üzerinde **sistem durumu kurtarma modunu seçin** bölmesinde sistem durumu dosyaları kurtarılması ve ardından istediğiniz hedef belirtin **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="856ad-170">On the **Select System State Recovery Mode** pane, specify the destination where you want System State files to be recovered, then click **Next**.</span></span>

    ![Şifreleme](./media/backup-azure-restore-system-state/recover-as-files.png)

    <span data-ttu-id="856ad-172">Seçenek **böylece her iki sürümünü de sahip kopya oluşturma**, tüm sistem durumu arşiv kopyasını oluşturmak yerine var olan bir sistem durumu Dosya arşiv tek tek dosyaların kopyalarını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="856ad-172">The option, **Create copies so that you have both versions**, creates copies of individual files in an existing System State file archive instead of creating the copy of the entire System State archive.</span></span>

11. <span data-ttu-id="856ad-173">Onay bölmesinde kurtarma ayrıntılarını doğrulayın ve tıklatın **kurtarmak**.</span><span class="sxs-lookup"><span data-stu-id="856ad-173">Verify the details of recovery on the Confirmation pane, and click **Recover**.</span></span> 

    ![kurtarma işlemini onaylamak için kurtarma düğmesini tıklatın.](./media/backup-azure-restore-system-state/confirm-recovery.png)

12. <span data-ttu-id="856ad-175">Kopya *WindowsImageBackup* sunucunun kritik olmayan bir birime dizin (örneğin D:\).</span><span class="sxs-lookup"><span data-stu-id="856ad-175">Copy the *WindowsImageBackup* directory to a non-critical volume of the server (for example D:\).</span></span> <span data-ttu-id="856ad-176">Genellikle Windows işletim sistemi birimi kritik bir birimdir.</span><span class="sxs-lookup"><span data-stu-id="856ad-176">Usually the Windows OS volume is the critical volume.</span></span>

13. <span data-ttu-id="856ad-177">Kurtarma işlemini tamamlamak için aşağıdaki bölümü kullanın [geri yüklenen sistem durumu dosyaları bir Windows sunucusu üzerindeki geçerli](backup-azure-restore-system-state.md#apply-restored-system-state-on-a-windows-server).</span><span class="sxs-lookup"><span data-stu-id="856ad-177">To complete the recovery process, use the following section to [apply the restored System State files on a Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-on-a-windows-server).</span></span>




## <a name="apply-restored-system-state-on-a-windows-server"></a><span data-ttu-id="856ad-178">Bir Windows sunucusuna geri yüklenen sistem durumu Uygula</span><span class="sxs-lookup"><span data-stu-id="856ad-178">Apply restored System State on a Windows Server</span></span>

<span data-ttu-id="856ad-179">Azure kurtarma Hizmetleri aracısını kullanarak dosyaları olarak sistem durumu kez kurtardı, Windows Server kurtarılan sistem durumu uygulamak için Windows Server Yedekleme yardımcı programı kullanın.</span><span class="sxs-lookup"><span data-stu-id="856ad-179">Once you have recovered System State as files using Azure Recovery Services Agent, use the Windows Server Backup utility to apply the recovered System State to Windows Server.</span></span> <span data-ttu-id="856ad-180">Windows Server Yedekleme yardımcı programı, sunucu üzerinde zaten mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="856ad-180">The Windows Server Backup utility is already available on the server.</span></span> <span data-ttu-id="856ad-181">Aşağıdaki adımlar, kurtarılan sistem durumunu uygulamak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="856ad-181">The following steps explain how to apply the recovered System State.</span></span>

1. <span data-ttu-id="856ad-182">Sunucuyu yeniden başlatmak için aşağıdaki komutları kullanın *dizin hizmetleri onarım modunda*.</span><span class="sxs-lookup"><span data-stu-id="856ad-182">Use the following commands to reboot your server in *Directory Services Repair Mode*.</span></span> <span data-ttu-id="856ad-183">Yükseltilmiş bir komut istemi'nde:</span><span class="sxs-lookup"><span data-stu-id="856ad-183">In an elevated command prompt:</span></span>

    ```
    PS C:\> Bcdedit /set safeboot dsrepair
    PS C:\> Shutdown /r /t 0
    ```

2. <span data-ttu-id="856ad-184">Yeniden başlatıldıktan sonra Windows Server Yedekleme ek bileşenini açın.</span><span class="sxs-lookup"><span data-stu-id="856ad-184">After the reboot, open the Windows Server Backup snap-in.</span></span> <span data-ttu-id="856ad-185">Ek bileşenini yüklendiği bilmiyorsanız, bilgisayar veya sunucu için arama **Windows Server Yedekleme**.</span><span class="sxs-lookup"><span data-stu-id="856ad-185">If you don't know where the snap-in was installed, search the computer or server for **Windows Server Backup**.</span></span>

    <span data-ttu-id="856ad-186">Masaüstü uygulama arama sonuçlarında görünür.</span><span class="sxs-lookup"><span data-stu-id="856ad-186">The desktop app appears in the search results.</span></span>

3. <span data-ttu-id="856ad-187">Ek bileşeninde, seçin **yerel yedekleme**.</span><span class="sxs-lookup"><span data-stu-id="856ad-187">In the snap-in, select **Local Backup**.</span></span>

    ![buradan geri yüklemek için yerel yedekleme seçin](./media/backup-azure-restore-system-state/win-server-backup-local-backup.png)

4. <span data-ttu-id="856ad-189">Yerel yedekleme konsolunda içinde **Eylemler bölmesi**, tıklatın **kurtarmak** Kurtarma Sihirbazı'nı açmak için.</span><span class="sxs-lookup"><span data-stu-id="856ad-189">On the Local Backup console, in the **Actions Pane**, click **Recover** to open the Recovery Wizard.</span></span>

5. <span data-ttu-id="856ad-190">Seçeneğini **başka bir konumda depolanan bir yedek**, tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="856ad-190">Select the option, **A backup stored in another location**, and click **Next**.</span></span>

   ![farklı bir sunucuya kurtarmak seçin](./media/backup-azure-restore-system-state/backup-stored-in-diff-location.png)

6. <span data-ttu-id="856ad-192">Konum türü belirtirken seçin **uzaktan paylaşılan klasörünü** , sistem durumu yedeklemesi başka bir sunucuya kurtarıldı.</span><span class="sxs-lookup"><span data-stu-id="856ad-192">When specifying the location type, select **Remote shared folder** if your System State backup was recovered to another server.</span></span> <span data-ttu-id="856ad-193">Sistem durumu yerel olarak yapılıyorsa, ardından **yerel sürücüler**.</span><span class="sxs-lookup"><span data-stu-id="856ad-193">If your System State was recovered locally, then select **Local drives**.</span></span> 

    ![Yerel sunucu ya da başka bir kurtarma olup olmadığını seçin](./media/backup-azure-restore-system-state/ss-recovery-remote-shared-folder.png)

7. <span data-ttu-id="856ad-195">Yolu girin *WindowsImageBackup* dizini ya da Azure kurtarma Hizmetleri kullanarak sistem durumu dosyaları kurtarmanın bir parçası kurtarılan bu dizin (örneğin, D:\WindowsImageBackup) içeren yerel sürücüyü seçin Aracı ve tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="856ad-195">Enter the path to the *WindowsImageBackup* directory, or choose the local drive containing this directory (for example, D:\WindowsImageBackup), recovered as part of the System State files recovery using Azure Recovery Services Agent and click **Next**.</span></span>

    ![Paylaşılan dosyasının yolu](./media/backup-azure-restore-system-state/ss-recovery-remote-folder.png)

8. <span data-ttu-id="856ad-197">Tıklatın ve geri yüklemek istediğiniz sistem durumu sürümü seçin **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="856ad-197">Select the System State version that you want to restore, and click **Next**.</span></span>

9. <span data-ttu-id="856ad-198">Kurtarma türünü seçin bölmesinde seçin **sistem durumu** tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="856ad-198">In the Select Recovery Type pane, select **System State** and click **Next**.</span></span>

10. <span data-ttu-id="856ad-199">Sistem durumu kurtarma konumunu seçin **özgün konumuna**, tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="856ad-199">For the location of the System State Recovery, select **Original Location**, and click **Next**.</span></span>

11. <span data-ttu-id="856ad-200">Onay ayrıntılarını gözden geçirin, yeniden başlatma ayarları doğrulayın ve tıklatın **kurtarmak** applly geri yüklenen sistem durumu için dosyaları.</span><span class="sxs-lookup"><span data-stu-id="856ad-200">Review the confirmation details, verify the reboot settings, and click **Recover** to applly the restored System State files.</span></span>

    ![Geri Yüklemeyi Başlat sistem durumu dosyaları](./media/backup-azure-restore-system-state/launch-ss-recovery.png)

## <a name="special-considerations-for-system-state-recovery-on-active-directory-server"></a><span data-ttu-id="856ad-202">Active Directory sunucuda sistem durumu kurtarma için özel hususlar</span><span class="sxs-lookup"><span data-stu-id="856ad-202">Special considerations for System State recovery on Active Directory server</span></span>

<span data-ttu-id="856ad-203">Sistem durumu yedeklemesi Active Directory verilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="856ad-203">System State backup includes Active Directory data.</span></span> <span data-ttu-id="856ad-204">Aşağıdaki adımlarda Active Directory etki alanı hizmeti (AD DS) geri yüklemek için önceki bir duruma geçerli durumunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="856ad-204">Use the following steps to restore Active Directory Domain Service (AD DS) from its current state to a previous state.</span></span>

1. <span data-ttu-id="856ad-205">Etki alanı denetleyicisi Dizin Hizmetleri geri yükleme modu (DSRM) yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="856ad-205">Restart the domain controller in Directory Services Restore Mode (DSRM).</span></span>
2. <span data-ttu-id="856ad-206">Adımları [burada](https://technet.microsoft.com/en-us/library/cc794755(v=ws.10).aspx) AD DS kurtarmak için Windows Server Yedekleme cmdlet'lerini kullanmak için.</span><span class="sxs-lookup"><span data-stu-id="856ad-206">Follow the steps [here](https://technet.microsoft.com/en-us/library/cc794755(v=ws.10).aspx) to use Windows Server Backup cmdlets to recover AD DS.</span></span>


## <a name="troubleshoot-failed-system-state-restore"></a><span data-ttu-id="856ad-207">Başarısız sistem durumu geri yükleme sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="856ad-207">Troubleshoot failed System State restore</span></span>

<span data-ttu-id="856ad-208">Sistem durumu uygulama önceki işlem başarıyla tamamlanmazsa, Windows sunucunuzu kurtarmak için Windows Kurtarma Ortamı'nı (Win RE) kullanın.</span><span class="sxs-lookup"><span data-stu-id="856ad-208">If the previous process of applying System State does not complete successfully, use the Windows Recovery Environment (Win RE) to recover your Windows Server.</span></span> <span data-ttu-id="856ad-209">Aşağıdaki adımlar, Win RE kullanarak kurtarma açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="856ad-209">The following steps explain how to recover using Win RE.</span></span> <span data-ttu-id="856ad-210">Yalnızca Windows Server normalde bir sistem durumu geri yüklendikten sonra önyükleme yapmaz, bu seçeneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="856ad-210">Use This option only if Windows Server does not boot normally after a System State restore.</span></span> <span data-ttu-id="856ad-211">Aşağıdaki işlem sistem dışı verileri, dikkatli siler.</span><span class="sxs-lookup"><span data-stu-id="856ad-211">The following process erases non-system data, use caution.</span></span> 

1. <span data-ttu-id="856ad-212">Windows Server'ınızın Windows Kurtarma Ortamı'nı (Win RE) içine önyükleme yapın.</span><span class="sxs-lookup"><span data-stu-id="856ad-212">Boot your Windows Server into the Windows Recovery Environment (Win RE).</span></span>

2. <span data-ttu-id="856ad-213">Sorun giderme üç kullanılabilir seçenekler arasından seçin.</span><span class="sxs-lookup"><span data-stu-id="856ad-213">Select Troubleshoot from the three available options.</span></span>

    ![Açılış menüsü](./media/backup-azure-restore-system-state/winre-1.png)

3. <span data-ttu-id="856ad-215">Gelen **Gelişmiş Seçenekler** ekran, select **komut istemi** server yönetici kullanıcı adı ve parolasını girin.</span><span class="sxs-lookup"><span data-stu-id="856ad-215">From the **Advanced Options** screen, select **Command Prompt** and provide the server administrator username and password.</span></span>

   ![Açılış menüsü](./media/backup-azure-restore-system-state/winre-2.png)

4. <span data-ttu-id="856ad-217">Sunucu yönetici kullanıcı adı ve parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="856ad-217">Provide the server administrator username and password.</span></span>

    ![Açılış menüsü](./media/backup-azure-restore-system-state/winre-3.png)

5. <span data-ttu-id="856ad-219">Yönetici modunda bir komut istemi açın, sistem durumu yedekleme sürümlerini almak için komutu aşağıdaki çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="856ad-219">When you open the command prompt in administrator mode, run following command to get the System State backup versions.</span></span>

    ```
    Wbadmin get versions -backuptarget:<Volume where WindowsImageBackup folder is copied>:
    ```
    ![Sistem Durumu yedekleme sürümlerini alma](./media/backup-azure-restore-system-state/winre-4.png)

6. <span data-ttu-id="856ad-221">Yedekleme kullanılabilir tüm birimleri almak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="856ad-221">Run the following command to get all volumes available in the backup.</span></span>

    ```
    Wbadmin get items -version:<copy version from above step> -backuptarget:<Backup volume>
    ```

    ![Sistem Durumu yedekleme sürümlerini alma](./media/backup-azure-restore-system-state/winre-5.png)

7. <span data-ttu-id="856ad-223">Aşağıdaki komut, sistem durumu yedeklemesi parçası olan tüm birimleri kurtarır.</span><span class="sxs-lookup"><span data-stu-id="856ad-223">The following command recovers all volumes that are part of the System State Backup.</span></span> <span data-ttu-id="856ad-224">Bu adım yalnızca sistem durumu parçası olan kritik birimleri kurtarır unutmayın.</span><span class="sxs-lookup"><span data-stu-id="856ad-224">Note that this step recovers only the critical volumes that are part of the System State.</span></span> <span data-ttu-id="856ad-225">Tüm sistem dışı veriler silinir.</span><span class="sxs-lookup"><span data-stu-id="856ad-225">All non-System data is erased.</span></span>

    ```
    Wbadmin start recovery -items:C: -itemtype:Volume -version:<Backupversion> -backuptarget:<backup target volume>
    ```
     ![Sistem Durumu yedekleme sürümlerini alma](./media/backup-azure-restore-system-state/winre-6.png)



## <a name="next-steps"></a><span data-ttu-id="856ad-227">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="856ad-227">Next steps</span></span>
* <span data-ttu-id="856ad-228">Dosya ve klasörleri kurtarma yaptıktan, yapabilecekleriniz [Yedeklemelerinizin yönetmek](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="856ad-228">Now that you've recovered your files and folders, you can [manage your backups](backup-azure-manage-windows-server.md).</span></span>
