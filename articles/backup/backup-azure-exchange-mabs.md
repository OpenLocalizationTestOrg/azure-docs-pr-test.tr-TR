---
title: Azure yedekleme sunucusu Azure yedekleme bir Exchange sunucusu yedekleme | Microsoft Docs
description: "Azure yedekleme sunucusu kullanarak Azure yedekleme için bir Exchange server'ı Yedekle öğrenin"
services: backup
documentationcenter: 
author: pvrk
manager: shivamg
editor: 
ms.assetid: e46557e8-2eaf-4ee0-99ea-00fbb8687dca
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: pullabhk
ms.openlocfilehash: 60b784fd00013c2b9504f8635c6b5c4c592563be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="back-up-an-exchange-server-to-azure-backup-with-azure-backup-server"></a><span data-ttu-id="700c2-103">Azure yedekleme ile Azure yedekleme sunucusu için bir Exchange server'ı Yedekle</span><span class="sxs-lookup"><span data-stu-id="700c2-103">Back up an Exchange server to Azure Backup with Azure Backup Server</span></span>
<span data-ttu-id="700c2-104">Bu makalede, Azure için Microsoft Exchange sunucusunu yedeklemek için Microsoft Azure yedekleme sunucusu (MABS) yapılandırmak açıklar.</span><span class="sxs-lookup"><span data-stu-id="700c2-104">This article describes how to configure Microsoft Azure Backup Server (MABS) to back up a Microsoft Exchange server to Azure.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="700c2-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="700c2-105">Prerequisites</span></span>
<span data-ttu-id="700c2-106">Devam etmeden önce Azure yedekleme sunucusu olduğundan emin olun [yüklü ve hazırlanan](backup-azure-microsoft-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="700c2-106">Before you continue, make sure that Azure Backup Server is [installed and prepared](backup-azure-microsoft-azure-backup.md).</span></span>

## <a name="mabs-protection-agent"></a><span data-ttu-id="700c2-107">MABS koruma Aracısı</span><span class="sxs-lookup"><span data-stu-id="700c2-107">MABS protection agent</span></span>
<span data-ttu-id="700c2-108">Exchange server üzerinde MABS koruma aracısı yüklemek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="700c2-108">To install the MABS protection agent on the Exchange server, follow these steps:</span></span>

1. <span data-ttu-id="700c2-109">Güvenlik duvarları doğru şekilde yapılandırıldığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="700c2-109">Make sure that the firewalls are correctly configured.</span></span> <span data-ttu-id="700c2-110">Bkz: [aracı için güvenlik duvarı özel durumlarını yapılandırma](https://technet.microsoft.com/library/Hh758204.aspx).</span><span class="sxs-lookup"><span data-stu-id="700c2-110">See [Configure firewall exceptions for the agent](https://technet.microsoft.com/library/Hh758204.aspx).</span></span>
2. <span data-ttu-id="700c2-111">Aracısı'nı tıklatarak Exchange sunucusunda yükleyin **Yönetim > aracıları > yükleme** MABS Yönetici konsolunda.</span><span class="sxs-lookup"><span data-stu-id="700c2-111">Install the agent on the Exchange server by clicking **Management > Agents > Install** in MABS Administrator Console.</span></span> <span data-ttu-id="700c2-112">Bkz: [MABS koruma aracısını yüklemek](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) ayrıntılı adımlar için.</span><span class="sxs-lookup"><span data-stu-id="700c2-112">See [Install the MABS protection agent](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) for detailed steps.</span></span>

## <a name="create-a-protection-group-for-the-exchange-server"></a><span data-ttu-id="700c2-113">Exchange server için bir koruma grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="700c2-113">Create a protection group for the Exchange server</span></span>
1. <span data-ttu-id="700c2-114">MABS Yönetici Konsolu'nda **koruma**ve ardından **yeni** açmak için araç şeridinde **yeni koruma grubu oluşturma** Sihirbazı.</span><span class="sxs-lookup"><span data-stu-id="700c2-114">In the MABS Administrator Console, click **Protection**, and then click **New** on the tool ribbon to open the **Create New Protection Group** wizard.</span></span>
2. <span data-ttu-id="700c2-115">Üzerinde **Hoş Geldiniz** Sihirbazı'nı ekranın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="700c2-115">On the **Welcome** screen of the wizard click **Next**.</span></span>
3. <span data-ttu-id="700c2-116">Üzerinde **koruma grubu türünü seçin** ekranında, seçin **sunucuları** tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="700c2-116">On the **Select protection group type** screen, select **Servers** and click **Next**.</span></span>
4. <span data-ttu-id="700c2-117">Tıklatıp korumak istediğiniz Exchange server veritabanını seçin **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="700c2-117">Select the Exchange server database that you want to protect and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="700c2-118">Exchange 2013 koruyorsanız, denetleme [Exchange 2013 önkoşulları](https://technet.microsoft.com/library/dn751029.aspx).</span><span class="sxs-lookup"><span data-stu-id="700c2-118">If you are protecting Exchange 2013, check the [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).</span></span>
   >
   >

    <span data-ttu-id="700c2-119">Aşağıdaki örnekte, Exchange 2010 veritabanı seçilir.</span><span class="sxs-lookup"><span data-stu-id="700c2-119">In the following example, the Exchange 2010 database is selected.</span></span>

    ![Grup üyelerini seçin](./media/backup-azure-backup-exchange-server/select-group-members.png)
5. <span data-ttu-id="700c2-121">Veri koruma yöntemini seçin.</span><span class="sxs-lookup"><span data-stu-id="700c2-121">Select the data protection method.</span></span>

    <span data-ttu-id="700c2-122">Koruma grubu adı ve her ikisi de aşağıdaki seçeneklerden birini seçin:</span><span class="sxs-lookup"><span data-stu-id="700c2-122">Name the protection group, and then select both of the following options:</span></span>

   * <span data-ttu-id="700c2-123">Disk kullanılan kısa vadeli koruma istiyorum.</span><span class="sxs-lookup"><span data-stu-id="700c2-123">I want short-term protection using Disk.</span></span>
   * <span data-ttu-id="700c2-124">Çevrimiçi koruma istiyorum.</span><span class="sxs-lookup"><span data-stu-id="700c2-124">I want online protection.</span></span>
6. <span data-ttu-id="700c2-125">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="700c2-125">Click **Next**.</span></span>
7. <span data-ttu-id="700c2-126">Seçin **veri bütünlüğünü denetlemek için Eseutil'i Çalıştır** Exchange Server veritabanlarının bütünlüğünü kontrol etmek istiyorsanız seçeneği.</span><span class="sxs-lookup"><span data-stu-id="700c2-126">Select the **Run Eseutil to check data integrity** option if you want to check the integrity of the Exchange Server databases.</span></span>

    <span data-ttu-id="700c2-127">Bu seçeneği belirledikten sonra yedekleme tutarlılığı denetleniyor çalıştırarak oluşturulan g/ç trafiği önlemek için MABS üzerinde çalıştırılacak **eseutil** Exchange sunucusundaki komutu.</span><span class="sxs-lookup"><span data-stu-id="700c2-127">After you select this option, backup consistency checking will be run on MABS to avoid the I/O traffic that’s generated by running the **eseutil** command on the Exchange server.</span></span>

   > [!NOTE]
   > <span data-ttu-id="700c2-128">Bu seçeneği kullanmak için Ese.dll ve Eseutil.exe dosyalarını MAB sunucusunda C:\Program Files\Microsoft Azure Backup\DPM\DPM\bin dizinine kopyalamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="700c2-128">To use this option, you must copy the Ese.dll and Eseutil.exe files to the C:\Program Files\Microsoft Azure Backup\DPM\DPM\bin directory on the MAB server.</span></span> <span data-ttu-id="700c2-129">Aksi takdirde, aşağıdaki hata tetiklenir:</span><span class="sxs-lookup"><span data-stu-id="700c2-129">Otherwise, the following error is triggered:</span></span>  
   > <span data-ttu-id="700c2-130">![Eseutil hata](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span><span class="sxs-lookup"><span data-stu-id="700c2-130">![eseutil error](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span></span>
   >
   >
8. <span data-ttu-id="700c2-131">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="700c2-131">Click **Next**.</span></span>
9. <span data-ttu-id="700c2-132">Veritabanı için seçin **kopya yedekleme**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="700c2-132">Select the database for **Copy Backup**, and then click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="700c2-133">Bir veritabanı en az bir DAG kopyası için "tam yedekleme" seçeneğini belirlemezseniz günlükler kesilmez.</span><span class="sxs-lookup"><span data-stu-id="700c2-133">If you do not select “Full backup” for at least one DAG copy of a database, logs will not be truncated.</span></span>
   >
   >
10. <span data-ttu-id="700c2-134">Hedefler için yapılandırma **kısa vadeli yedekleme**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="700c2-134">Configure the goals for **Short-Term backup**, and then click **Next**.</span></span>
11. <span data-ttu-id="700c2-135">Kullanılabilir disk alanını gözden geçirin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="700c2-135">Review the available disk space, and then click **Next**.</span></span>
12. <span data-ttu-id="700c2-136">Hangi MAB sunucunun ilk çoğaltma oluşturur ve ardından istediğiniz saati seçin **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="700c2-136">Select the time at which the MAB Server will create the initial replication, and then click **Next**.</span></span>
13. <span data-ttu-id="700c2-137">Tutarlılık denetimi seçeneklerini seçin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="700c2-137">Select the consistency check options, and then click **Next**.</span></span>
14. <span data-ttu-id="700c2-138">Azure'a yedeklemek ve ardından istediğiniz veritabanını seçin **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="700c2-138">Choose the database that you want to back up to Azure, and then click **Next**.</span></span> <span data-ttu-id="700c2-139">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="700c2-139">For example:</span></span>

    ![Çevrimiçi koruma verilerini belirtin](./media/backup-azure-backup-exchange-server/specify-online-protection-data.png)
15. <span data-ttu-id="700c2-141">İçin zamanlama tanımla **Azure Backup**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="700c2-141">Define the schedule for **Azure Backup**, and then click **Next**.</span></span> <span data-ttu-id="700c2-142">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="700c2-142">For example:</span></span>

    ![Çevrimiçi Yedekleme zamanlamasını belirtin](./media/backup-azure-backup-exchange-server/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="700c2-144">Çevrimiçi kurtarma noktası hızlı temel unutmayın tam kurtarma noktaları.</span><span class="sxs-lookup"><span data-stu-id="700c2-144">Note Online recovery points are based on express full recovery points.</span></span> <span data-ttu-id="700c2-145">Bu nedenle, belirtilen süre için hızlı tam kurtarma noktası sonra çevrimiçi kurtarma noktası zamanlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="700c2-145">Therefore, you must schedule the online recovery point after the time that’s specified for the express full recovery point.</span></span>
    >
    >
16. <span data-ttu-id="700c2-146">Bekletme İlkesi yapılandırma **Azure Backup**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="700c2-146">Configure the retention policy for **Azure Backup**, and then click **Next**.</span></span>
17. <span data-ttu-id="700c2-147">Çevrimiçi çoğaltma seçeneğini belirleyin ve tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="700c2-147">Choose an online replication option and click **Next**.</span></span>

    <span data-ttu-id="700c2-148">Büyük bir veritabanınız varsa, ağ üzerinden oluşturulacak ilk yedekleme uzun bir süredir ele geçirebilir.</span><span class="sxs-lookup"><span data-stu-id="700c2-148">If you have a large database, it could take a long time for the initial backup to be created over the network.</span></span> <span data-ttu-id="700c2-149">Bu sorunu önlemek için Çevrimdışı Yedekleme oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="700c2-149">To avoid this issue, you can create an offline backup.</span></span>  

    ![Çevrimiçi bekletme ilkesini belirtin](./media/backup-azure-backup-exchange-server/specify-online-retention-policy.png)
18. <span data-ttu-id="700c2-151">Ayarları onaylayın ve ardından **Grup Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="700c2-151">Confirm the settings, and then click **Create Group**.</span></span>
19. <span data-ttu-id="700c2-152">**Kapat**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="700c2-152">Click **Close**.</span></span>

## <a name="recover-the-exchange-database"></a><span data-ttu-id="700c2-153">Exchange veritabanını kurtarma</span><span class="sxs-lookup"><span data-stu-id="700c2-153">Recover the Exchange database</span></span>
1. <span data-ttu-id="700c2-154">Bir Exchange veritabanını kurtarmak için **kurtarma** MABS Yönetici konsolunda.</span><span class="sxs-lookup"><span data-stu-id="700c2-154">To recover an Exchange database, click **Recovery** in the MABS Administrator Console.</span></span>
2. <span data-ttu-id="700c2-155">Kurtarmak istediğiniz Exchange veritabanı bulun.</span><span class="sxs-lookup"><span data-stu-id="700c2-155">Locate the Exchange database that you want to recover.</span></span>
3. <span data-ttu-id="700c2-156">Bir çevrimiçi kurtarma noktası seçin *kurtarma süresini* aşağı açılan liste.</span><span class="sxs-lookup"><span data-stu-id="700c2-156">Select an online recovery point from the *recovery time* drop-down list.</span></span>
4. <span data-ttu-id="700c2-157">Tıklatın **kurtarmak** başlatmak için **Kurtarma Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="700c2-157">Click **Recover** to start the **Recovery Wizard**.</span></span>

<span data-ttu-id="700c2-158">Çevrimiçi kurtarma noktaları için beş kurtarma türü vardır:</span><span class="sxs-lookup"><span data-stu-id="700c2-158">For online recovery points, there are five recovery types:</span></span>

* <span data-ttu-id="700c2-159">**Özgün Exchange Server konumuna Kurtar:** verileri özgün Exchange Server'a kurtarılır.</span><span class="sxs-lookup"><span data-stu-id="700c2-159">**Recover to original Exchange Server location:** The data will be recovered to the original Exchange server.</span></span>
* <span data-ttu-id="700c2-160">**Exchange Server üzerindeki başka bir veritabanına Kurtar:** verileri başka bir Exchange server üzerindeki başka bir veritabanına kurtarıldı.</span><span class="sxs-lookup"><span data-stu-id="700c2-160">**Recover to another database on an Exchange Server:** The data will be recovered to another database on another Exchange server.</span></span>
* <span data-ttu-id="700c2-161">**Kurtarma veritabanına Kurtar:** verileri bir Exchange kurtarma veritabanına (RDB) kurtarılacak.</span><span class="sxs-lookup"><span data-stu-id="700c2-161">**Recover to a Recovery Database:** The data will be recovered to an Exchange Recovery Database (RDB).</span></span>
* <span data-ttu-id="700c2-162">**Bir ağ klasörüne kopyala:** verileri bir ağ klasörüne kurtarılacak.</span><span class="sxs-lookup"><span data-stu-id="700c2-162">**Copy to a network folder:** The data will be recovered to a network folder.</span></span>
* <span data-ttu-id="700c2-163">**Banda Kopyala:** bir bant kitaplığını veya bağlı ve MABS üzerinde yapılandırılmış tek başına bant sürücüsü varsa, kurtarma noktası bir boş banda kopyalanacak.</span><span class="sxs-lookup"><span data-stu-id="700c2-163">**Copy to tape:** If you have a tape library or a stand-alone tape drive attached and configured on MABS, the recovery point will be copied to a free tape.</span></span>

    ![Çevrimiçi çoğaltma seçin](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a><span data-ttu-id="700c2-165">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="700c2-165">Next steps</span></span>
* [<span data-ttu-id="700c2-166">Azure Backup ile ilgili SSS</span><span class="sxs-lookup"><span data-stu-id="700c2-166">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)
