---
title: Exchange server tooAzure yedekleme Azure yedekleme sunucusu ile ayarlama aaaBack | Microsoft Docs
description: "Bilgi nasıl tooback bir Exchange server tooAzure yukarı yedekleme Azure yedekleme sunucusu kullanarak"
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
ms.openlocfilehash: db874161151fc57c5b79c41531e18d577f567f66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-an-exchange-server-tooazure-backup-with-azure-backup-server"></a><span data-ttu-id="4ea9e-103">Exchange server tooAzure yedekleme Azure yedekleme sunucusu ile yedekleyin</span><span class="sxs-lookup"><span data-stu-id="4ea9e-103">Back up an Exchange server tooAzure Backup with Azure Backup Server</span></span>
<span data-ttu-id="4ea9e-104">Bu makalede nasıl tooconfigure Microsoft Azure yedekleme sunucusu (MABS) tooback bir Microsoft Exchange server tooAzure ayarlama.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-104">This article describes how tooconfigure Microsoft Azure Backup Server (MABS) tooback up a Microsoft Exchange server tooAzure.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="4ea9e-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="4ea9e-105">Prerequisites</span></span>
<span data-ttu-id="4ea9e-106">Devam etmeden önce Azure yedekleme sunucusu olduğundan emin olun [yüklü ve hazırlanan](backup-azure-microsoft-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="4ea9e-106">Before you continue, make sure that Azure Backup Server is [installed and prepared](backup-azure-microsoft-azure-backup.md).</span></span>

## <a name="mabs-protection-agent"></a><span data-ttu-id="4ea9e-107">MABS koruma Aracısı</span><span class="sxs-lookup"><span data-stu-id="4ea9e-107">MABS protection agent</span></span>
<span data-ttu-id="4ea9e-108">tooinstall hello MABS koruma Aracısı hello Exchange sunucusunda şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="4ea9e-108">tooinstall hello MABS protection agent on hello Exchange server, follow these steps:</span></span>

1. <span data-ttu-id="4ea9e-109">Merhaba güvenlik duvarları doğru şekilde yapılandırıldığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-109">Make sure that hello firewalls are correctly configured.</span></span> <span data-ttu-id="4ea9e-110">Bkz: [hello aracı için güvenlik duvarı özel durumlarını yapılandırma](https://technet.microsoft.com/library/Hh758204.aspx).</span><span class="sxs-lookup"><span data-stu-id="4ea9e-110">See [Configure firewall exceptions for hello agent](https://technet.microsoft.com/library/Hh758204.aspx).</span></span>
2. <span data-ttu-id="4ea9e-111">Tıklayarak hello Exchange sunucusunda Hello aracı yükleme **Yönetim > aracıları > yükleme** MABS Yönetici konsolunda.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-111">Install hello agent on hello Exchange server by clicking **Management > Agents > Install** in MABS Administrator Console.</span></span> <span data-ttu-id="4ea9e-112">Bkz: [yükleme hello MABS koruma Aracısı](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) ayrıntılı adımlar için.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-112">See [Install hello MABS protection agent](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) for detailed steps.</span></span>

## <a name="create-a-protection-group-for-hello-exchange-server"></a><span data-ttu-id="4ea9e-113">Merhaba Exchange sunucusu için bir koruma grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="4ea9e-113">Create a protection group for hello Exchange server</span></span>
1. <span data-ttu-id="4ea9e-114">Hello MABS Yönetici Konsolu, tıklatın **koruma**ve ardından **yeni** hello aracı Şerit tooopen hello üzerinde **yeni koruma grubu oluşturma** Sihirbazı.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-114">In hello MABS Administrator Console, click **Protection**, and then click **New** on hello tool ribbon tooopen hello **Create New Protection Group** wizard.</span></span>
2. <span data-ttu-id="4ea9e-115">Merhaba üzerinde **Hoş Geldiniz** hello Sihirbazı'nı ekranın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-115">On hello **Welcome** screen of hello wizard click **Next**.</span></span>
3. <span data-ttu-id="4ea9e-116">Merhaba üzerinde **koruma grubu türünü seçin** ekranında, seçin **sunucuları** tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-116">On hello **Select protection group type** screen, select **Servers** and click **Next**.</span></span>
4. <span data-ttu-id="4ea9e-117">Select hello Exchange server veritabanına tooprotect istediğiniz ve tıklayın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-117">Select hello Exchange server database that you want tooprotect and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4ea9e-118">Exchange 2013 koruyorsanız hello denetleyin [Exchange 2013 önkoşulları](https://technet.microsoft.com/library/dn751029.aspx).</span><span class="sxs-lookup"><span data-stu-id="4ea9e-118">If you are protecting Exchange 2013, check hello [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).</span></span>
   >
   >

    <span data-ttu-id="4ea9e-119">Aşağıdaki örneğine hello hello Exchange 2010 veritabanı seçilir.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-119">In hello following example, hello Exchange 2010 database is selected.</span></span>

    ![Grup üyelerini seçin](./media/backup-azure-backup-exchange-server/select-group-members.png)
5. <span data-ttu-id="4ea9e-121">Merhaba veri koruma yöntemini seçin.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-121">Select hello data protection method.</span></span>

    <span data-ttu-id="4ea9e-122">Merhaba koruma grubu adı ve aşağıdaki seçenekleri şu hello her ikisini de seçin:</span><span class="sxs-lookup"><span data-stu-id="4ea9e-122">Name hello protection group, and then select both of hello following options:</span></span>

   * <span data-ttu-id="4ea9e-123">Disk kullanılan kısa vadeli koruma istiyorum.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-123">I want short-term protection using Disk.</span></span>
   * <span data-ttu-id="4ea9e-124">Çevrimiçi koruma istiyorum.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-124">I want online protection.</span></span>
6. <span data-ttu-id="4ea9e-125">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-125">Click **Next**.</span></span>
7. <span data-ttu-id="4ea9e-126">Select hello **Eseutil'i Çalıştır toocheck veri bütünlüğü** toocheck hello hello Exchange Server veritabanlarının bütünlüğünü istiyorsanız seçeneği.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-126">Select hello **Run Eseutil toocheck data integrity** option if you want toocheck hello integrity of hello Exchange Server databases.</span></span>

    <span data-ttu-id="4ea9e-127">Bu seçeneği belirledikten sonra yedekleme tutarlılığı denetleniyor hello çalıştırarak oluşturulan MABS tooavoid hello g/ç trafiği üzerinde çalıştırılacak **eseutil** hello Exchange sunucusundaki komutu.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-127">After you select this option, backup consistency checking will be run on MABS tooavoid hello I/O traffic that’s generated by running hello **eseutil** command on hello Exchange server.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4ea9e-128">toouse bu seçenek, hello Ese.dll ve Eseutil.exe dosyalarını toohello C:\Program Files\Microsoft Azure Backup\DPM\DPM\bin hello MAB sunucusunda dizinine kopyalamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-128">toouse this option, you must copy hello Ese.dll and Eseutil.exe files toohello C:\Program Files\Microsoft Azure Backup\DPM\DPM\bin directory on hello MAB server.</span></span> <span data-ttu-id="4ea9e-129">Aksi takdirde, aşağıdaki hata hello tetiklenir:</span><span class="sxs-lookup"><span data-stu-id="4ea9e-129">Otherwise, hello following error is triggered:</span></span>  
   > <span data-ttu-id="4ea9e-130">![Eseutil hata](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span><span class="sxs-lookup"><span data-stu-id="4ea9e-130">![eseutil error](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span></span>
   >
   >
8. <span data-ttu-id="4ea9e-131">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-131">Click **Next**.</span></span>
9. <span data-ttu-id="4ea9e-132">Select hello veritabanı için **kopya yedekleme**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-132">Select hello database for **Copy Backup**, and then click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4ea9e-133">Bir veritabanı en az bir DAG kopyası için "tam yedekleme" seçeneğini belirlemezseniz günlükler kesilmez.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-133">If you do not select “Full backup” for at least one DAG copy of a database, logs will not be truncated.</span></span>
   >
   >
10. <span data-ttu-id="4ea9e-134">Merhaba hedeflerini yapılandırma **kısa vadeli yedekleme**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-134">Configure hello goals for **Short-Term backup**, and then click **Next**.</span></span>
11. <span data-ttu-id="4ea9e-135">Merhaba kullanılabilir disk alanını gözden geçirin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-135">Review hello available disk space, and then click **Next**.</span></span>
12. <span data-ttu-id="4ea9e-136">Hangi hello MAB sunucu hello ilk çoğaltma oluşturur ve ardından başlangıç saati seçin **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-136">Select hello time at which hello MAB Server will create hello initial replication, and then click **Next**.</span></span>
13. <span data-ttu-id="4ea9e-137">Merhaba tutarlılık denetimi seçeneklerini seçin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-137">Select hello consistency check options, and then click **Next**.</span></span>
14. <span data-ttu-id="4ea9e-138">Tooback tooAzure yedeklemek istediğiniz ve ardından hello veritabanı seçin **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-138">Choose hello database that you want tooback up tooAzure, and then click **Next**.</span></span> <span data-ttu-id="4ea9e-139">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="4ea9e-139">For example:</span></span>

    ![Çevrimiçi koruma verilerini belirtin](./media/backup-azure-backup-exchange-server/specify-online-protection-data.png)
15. <span data-ttu-id="4ea9e-141">İçin Hello zamanlama tanımla **Azure Backup**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-141">Define hello schedule for **Azure Backup**, and then click **Next**.</span></span> <span data-ttu-id="4ea9e-142">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="4ea9e-142">For example:</span></span>

    ![Çevrimiçi Yedekleme zamanlamasını belirtin](./media/backup-azure-backup-exchange-server/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="4ea9e-144">Çevrimiçi kurtarma noktası hızlı temel unutmayın tam kurtarma noktaları.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-144">Note Online recovery points are based on express full recovery points.</span></span> <span data-ttu-id="4ea9e-145">Bu nedenle, hello çevrimiçi kurtarma noktası zamanlama belirtilen hello süredir hello sonra tam kurtarma noktası express.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-145">Therefore, you must schedule hello online recovery point after hello time that’s specified for hello express full recovery point.</span></span>
    >
    >
16. <span data-ttu-id="4ea9e-146">Merhaba bekletme ilkesi yapılandırma **Azure Backup**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-146">Configure hello retention policy for **Azure Backup**, and then click **Next**.</span></span>
17. <span data-ttu-id="4ea9e-147">Çevrimiçi çoğaltma seçeneğini belirleyin ve tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-147">Choose an online replication option and click **Next**.</span></span>

    <span data-ttu-id="4ea9e-148">Büyük bir veritabanınız varsa, hello ilk yedekleme toobe hello ağ üzerinden oluşturulan uzun bir süredir ele geçirebilir.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-148">If you have a large database, it could take a long time for hello initial backup toobe created over hello network.</span></span> <span data-ttu-id="4ea9e-149">tooavoid bu sorunu çevrimdışı yedekleme oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-149">tooavoid this issue, you can create an offline backup.</span></span>  

    ![Çevrimiçi bekletme ilkesini belirtin](./media/backup-azure-backup-exchange-server/specify-online-retention-policy.png)
18. <span data-ttu-id="4ea9e-151">Hello ayarlarını onaylayın ve ardından **Grup Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-151">Confirm hello settings, and then click **Create Group**.</span></span>
19. <span data-ttu-id="4ea9e-152">**Kapat**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-152">Click **Close**.</span></span>

## <a name="recover-hello-exchange-database"></a><span data-ttu-id="4ea9e-153">Merhaba Exchange veritabanını kurtarma</span><span class="sxs-lookup"><span data-stu-id="4ea9e-153">Recover hello Exchange database</span></span>
1. <span data-ttu-id="4ea9e-154">bir Exchange veritabanı toorecover tıklatın **kurtarma** hello MABS Yönetici Konsolu içinde.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-154">toorecover an Exchange database, click **Recovery** in hello MABS Administrator Console.</span></span>
2. <span data-ttu-id="4ea9e-155">Toorecover istediğiniz hello Exchange veritabanını bulun.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-155">Locate hello Exchange database that you want toorecover.</span></span>
3. <span data-ttu-id="4ea9e-156">Merhaba çevrimiçi bir kurtarma noktası seçin *kurtarma süresini* aşağı açılan liste.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-156">Select an online recovery point from hello *recovery time* drop-down list.</span></span>
4. <span data-ttu-id="4ea9e-157">Tıklatın **kurtarmak** toostart hello **Kurtarma Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-157">Click **Recover** toostart hello **Recovery Wizard**.</span></span>

<span data-ttu-id="4ea9e-158">Çevrimiçi kurtarma noktaları için beş kurtarma türü vardır:</span><span class="sxs-lookup"><span data-stu-id="4ea9e-158">For online recovery points, there are five recovery types:</span></span>

* <span data-ttu-id="4ea9e-159">**Toooriginal Exchange Server konumuna Kurtar:** hello veriler, kurtarılan toohello özgün Exchange server olacaktır.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-159">**Recover toooriginal Exchange Server location:** hello data will be recovered toohello original Exchange server.</span></span>
* <span data-ttu-id="4ea9e-160">**Exchange Server üzerindeki tooanother veritabanını Kurtar:** hello veriler, kurtarılan tooanother veritabanı başka bir Exchange sunucusu üzerinde olacaktır.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-160">**Recover tooanother database on an Exchange Server:** hello data will be recovered tooanother database on another Exchange server.</span></span>
* <span data-ttu-id="4ea9e-161">**Tooa kurtarma veritabanına Kurtar:** hello veriler, kurtarılan tooan Exchange kurtarma veritabanına (RDB) olacaktır.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-161">**Recover tooa Recovery Database:** hello data will be recovered tooan Exchange Recovery Database (RDB).</span></span>
* <span data-ttu-id="4ea9e-162">**Kopya tooa ağ klasörüne:** hello veriler, kurtarılan tooa ağ klasörüne olacaktır.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-162">**Copy tooa network folder:** hello data will be recovered tooa network folder.</span></span>
* <span data-ttu-id="4ea9e-163">**Tootape kopyalayın:** bir bant kitaplığınız veya ekli ve yapılandırılmış MABS, hello kurtarma noktası olacaktır bir tek başına bant sürücüsünü tooa boş bant kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-163">**Copy tootape:** If you have a tape library or a stand-alone tape drive attached and configured on MABS, hello recovery point will be copied tooa free tape.</span></span>

    ![Çevrimiçi çoğaltma seçin](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a><span data-ttu-id="4ea9e-165">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4ea9e-165">Next steps</span></span>
* [<span data-ttu-id="4ea9e-166">Azure Backup ile ilgili SSS</span><span class="sxs-lookup"><span data-stu-id="4ea9e-166">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)
