---
title: "Exchange server tooAzure System Center 2012 R2 DPM yedeklemesiyle yukarı aaaBack | Microsoft Docs"
description: "Bilgi nasıl tooback bir Exchange server tooAzure yukarı yedekleme System Center 2012 R2 DPM kullanma"
services: backup
documentationcenter: 
author: MaanasSaran
manager: NKolli1
editor: 
ms.assetid: 13f32256-888e-416e-a78b-40c2a26a5939
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: masaran;jimpark;delhan;trinadhk;markgal
ms.openlocfilehash: fa99296d095c180333474b6d419ebc5ec727547a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-an-exchange-server-tooazure-backup-with-system-center-2012-r2-dpm"></a><span data-ttu-id="7f6cf-103">Exchange server tooAzure System Center 2012 R2 DPM yedeklemesiyle yedekleyin</span><span class="sxs-lookup"><span data-stu-id="7f6cf-103">Back up an Exchange server tooAzure Backup with System Center 2012 R2 DPM</span></span>
<span data-ttu-id="7f6cf-104">Bu makalede nasıl tooconfigure System Center 2012 R2 Data Protection Manager (DPM) sunucu tooback bir Microsoft Exchange sunucusu çok Azure yedekleme.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-104">This article describes how tooconfigure a System Center 2012 R2 Data Protection Manager (DPM) server tooback up a Microsoft Exchange server too Azure Backup.</span></span>  

## <a name="updates"></a><span data-ttu-id="7f6cf-105">Güncelleştirmeler</span><span class="sxs-lookup"><span data-stu-id="7f6cf-105">Updates</span></span>
<span data-ttu-id="7f6cf-106">toosuccessfully kayıt hello DPM sunucusu Azure yedekleme ile hello Azure Yedekleme aracısı System Center 2012 R2 DPM ve hello en son sürümü için en son güncelleştirme toplaması hello yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-106">toosuccessfully register hello DPM server with Azure Backup, you must install hello latest update rollup for System Center 2012 R2 DPM and hello latest version of hello Azure Backup Agent.</span></span> <span data-ttu-id="7f6cf-107">Hello Hello en son güncelleştirme paketi Al [Microsoft Catalog](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=System%20Center%202012%20R2%20Data%20protection%20manager).</span><span class="sxs-lookup"><span data-stu-id="7f6cf-107">Get hello latest update rollup from hello [Microsoft Catalog](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=System%20Center%202012%20R2%20Data%20protection%20manager).</span></span>

> [!NOTE]
> <span data-ttu-id="7f6cf-108">Bu makaledeki örneklerde Merhaba, hello Azure yedekleme Aracısı'nın 2.0.8719.0 sürümü yüklü ve güncelleştirme paketi 6 System Center 2012 R2 DPM üzerinde yüklü.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-108">For hello examples in this article, version 2.0.8719.0 of hello Azure Backup Agent is installed, and Update Rollup 6 is installed on System Center 2012 R2 DPM.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="7f6cf-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7f6cf-109">Prerequisites</span></span>
<span data-ttu-id="7f6cf-110">Devam etmeden önce tüm hello emin olun [Önkoşullar](backup-azure-dpm-introduction.md#prerequisites) tooprotect iş yükleri için Microsoft Azure Yedekleme kullanılarak karşılandığından.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-110">Before you continue, make sure that all hello [prerequisites](backup-azure-dpm-introduction.md#prerequisites) for using Microsoft Azure Backup tooprotect workloads have been met.</span></span> <span data-ttu-id="7f6cf-111">Bu Önkoşullar hello şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="7f6cf-111">These prerequisites include hello following:</span></span>

* <span data-ttu-id="7f6cf-112">Bir yedekleme kasası hello Azure site üzerinde oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-112">A backup vault on hello Azure site has been created.</span></span>
* <span data-ttu-id="7f6cf-113">Aracısını ve kasa kimlik bilgileri indirilen toohello DPM sunucusunun silinmiş.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-113">Agent and vault credentials have been downloaded toohello DPM server.</span></span>
* <span data-ttu-id="7f6cf-114">Merhaba Aracısı hello DPM sunucusuna yüklenir.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-114">hello agent is installed on hello DPM server.</span></span>
* <span data-ttu-id="7f6cf-115">Merhaba kasa kimlik bilgileri kullanılan tooregister hello DPM sunucusu yoktu.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-115">hello vault credentials were used tooregister hello DPM server.</span></span>
* <span data-ttu-id="7f6cf-116">Lütfen Exchange 2016 koruyorsanız, tooDPM 2012 R2 UR9 yükseltme yapın veya daha yenisi</span><span class="sxs-lookup"><span data-stu-id="7f6cf-116">If you are protecting Exchange 2016, please upgrade tooDPM 2012 R2 UR9 or later</span></span>

## <a name="dpm-protection-agent"></a><span data-ttu-id="7f6cf-117">DPM koruma Aracısı</span><span class="sxs-lookup"><span data-stu-id="7f6cf-117">DPM protection agent</span></span>
<span data-ttu-id="7f6cf-118">tooinstall hello DPM koruma Aracısı hello Exchange sunucusunda şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="7f6cf-118">tooinstall hello DPM protection agent on hello Exchange server, follow these steps:</span></span>

1. <span data-ttu-id="7f6cf-119">Merhaba güvenlik duvarları doğru şekilde yapılandırıldığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-119">Make sure that hello firewalls are correctly configured.</span></span> <span data-ttu-id="7f6cf-120">Bkz: [hello aracı için güvenlik duvarı özel durumlarını yapılandırma](https://technet.microsoft.com/library/Hh758204.aspx).</span><span class="sxs-lookup"><span data-stu-id="7f6cf-120">See [Configure firewall exceptions for hello agent](https://technet.microsoft.com/library/Hh758204.aspx).</span></span>
2. <span data-ttu-id="7f6cf-121">Tıklayarak hello Exchange sunucusunda Hello aracı yükleme **Yönetim > aracıları > yükleme** DPM yönetici Konsolu'ndaki.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-121">Install hello agent on hello Exchange server by clicking **Management > Agents > Install** in DPM Administrator Console.</span></span> <span data-ttu-id="7f6cf-122">Bkz: [yükleme hello DPM koruma Aracısı](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) ayrıntılı adımlar için.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-122">See [Install hello DPM protection agent](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) for detailed steps.</span></span>

## <a name="create-a-protection-group-for-hello-exchange-server"></a><span data-ttu-id="7f6cf-123">Merhaba Exchange sunucusu için bir koruma grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="7f6cf-123">Create a protection group for hello Exchange server</span></span>
1. <span data-ttu-id="7f6cf-124">Hello DPM Yönetici Konsolu, tıklatın **koruma**ve ardından **yeni** hello aracı Şerit tooopen hello üzerinde **yeni koruma grubu oluşturma** Sihirbazı.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-124">In hello DPM Administrator Console, click **Protection**, and then click **New** on hello tool ribbon tooopen hello **Create New Protection Group** wizard.</span></span>
2. <span data-ttu-id="7f6cf-125">Merhaba üzerinde **Hoş Geldiniz** hello Sihirbazı'nı ekranın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-125">On hello **Welcome** screen of hello wizard click **Next**.</span></span>
3. <span data-ttu-id="7f6cf-126">Merhaba üzerinde **koruma grubu türünü seçin** ekranında, seçin **sunucuları** tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-126">On hello **Select protection group type** screen, select **Servers** and click **Next**.</span></span>
4. <span data-ttu-id="7f6cf-127">Select hello Exchange server veritabanına tooprotect istediğiniz ve tıklayın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-127">Select hello Exchange server database that you want tooprotect and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7f6cf-128">Exchange 2013 koruyorsanız hello denetleyin [Exchange 2013 önkoşulları](https://technet.microsoft.com/library/dn751029.aspx).</span><span class="sxs-lookup"><span data-stu-id="7f6cf-128">If you are protecting Exchange 2013, check hello [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).</span></span>
   >
   >

    <span data-ttu-id="7f6cf-129">Aşağıdaki örneğine hello hello Exchange 2010 veritabanı seçilir.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-129">In hello following example, hello Exchange 2010 database is selected.</span></span>

    ![Grup üyelerini seçin](./media/backup-azure-backup-exchange-server/select-group-members.png)
5. <span data-ttu-id="7f6cf-131">Merhaba veri koruma yöntemini seçin.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-131">Select hello data protection method.</span></span>

    <span data-ttu-id="7f6cf-132">Merhaba koruma grubu adı ve aşağıdaki seçenekleri şu hello her ikisini de seçin:</span><span class="sxs-lookup"><span data-stu-id="7f6cf-132">Name hello protection group, and then select both of hello following options:</span></span>

   * <span data-ttu-id="7f6cf-133">Disk kullanılan kısa vadeli koruma istiyorum.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-133">I want short-term protection using Disk.</span></span>
   * <span data-ttu-id="7f6cf-134">Çevrimiçi koruma istiyorum.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-134">I want online protection.</span></span>
6. <span data-ttu-id="7f6cf-135">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-135">Click **Next**.</span></span>
7. <span data-ttu-id="7f6cf-136">Select hello **Eseutil'i Çalıştır toocheck veri bütünlüğü** toocheck hello hello Exchange Server veritabanlarının bütünlüğünü istiyorsanız seçeneği.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-136">Select hello **Run Eseutil toocheck data integrity** option if you want toocheck hello integrity of hello Exchange Server databases.</span></span>

    <span data-ttu-id="7f6cf-137">Bu seçeneği belirledikten sonra yedekleme tutarlılığı denetleniyor hello çalıştırarak hello DPM sunucusu tooavoid hello g/ç trafiği üzerinde çalıştırılacak **eseutil** hello Exchange sunucusundaki komutu.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-137">After you select this option, backup consistency checking will be run on hello DPM server tooavoid hello I/O traffic that’s generated by running hello **eseutil** command on hello Exchange server.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7f6cf-138">toouse bu seçenek, hello Ese.dll ve Eseutil.exe dosyalarını toohello C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin dizin hello DPM sunucusunda kopyalamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-138">toouse this option, you must copy hello Ese.dll and Eseutil.exe files toohello C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin directory on hello DPM server.</span></span> <span data-ttu-id="7f6cf-139">Aksi takdirde, aşağıdaki hata hello tetiklenir:</span><span class="sxs-lookup"><span data-stu-id="7f6cf-139">Otherwise, hello following error is triggered:</span></span>  
   > <span data-ttu-id="7f6cf-140">![Eseutil hata](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span><span class="sxs-lookup"><span data-stu-id="7f6cf-140">![eseutil error](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span></span>
   >
   >
8. <span data-ttu-id="7f6cf-141">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-141">Click **Next**.</span></span>
9. <span data-ttu-id="7f6cf-142">Select hello veritabanı için **kopya yedekleme**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-142">Select hello database for **Copy Backup**, and then click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7f6cf-143">Bir veritabanı en az bir DAG kopyası için "tam yedekleme" seçeneğini belirlemezseniz günlükler kesilmez.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-143">If you do not select “Full backup” for at least one DAG copy of a database, logs will not be truncated.</span></span>
   >
   >
10. <span data-ttu-id="7f6cf-144">Merhaba hedeflerini yapılandırma **kısa vadeli yedekleme**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-144">Configure hello goals for **Short-Term backup**, and then click **Next**.</span></span>
11. <span data-ttu-id="7f6cf-145">Merhaba kullanılabilir disk alanını gözden geçirin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-145">Review hello available disk space, and then click **Next**.</span></span>
12. <span data-ttu-id="7f6cf-146">DPM hangi hello sunucu hello ilk çoğaltma oluşturur ve ardından başlangıç saati seçin **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-146">Select hello time at which hello DPM server will create hello initial replication, and then click **Next**.</span></span>
13. <span data-ttu-id="7f6cf-147">Merhaba tutarlılık denetimi seçeneklerini seçin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-147">Select hello consistency check options, and then click **Next**.</span></span>
14. <span data-ttu-id="7f6cf-148">Tooback tooAzure yedeklemek istediğiniz ve ardından hello veritabanı seçin **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-148">Choose hello database that you want tooback up tooAzure, and then click **Next**.</span></span> <span data-ttu-id="7f6cf-149">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="7f6cf-149">For example:</span></span>

    ![Çevrimiçi koruma verilerini belirtin](./media/backup-azure-backup-exchange-server/specify-online-protection-data.png)
15. <span data-ttu-id="7f6cf-151">İçin Hello zamanlama tanımla **Azure Backup**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-151">Define hello schedule for **Azure Backup**, and then click **Next**.</span></span> <span data-ttu-id="7f6cf-152">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="7f6cf-152">For example:</span></span>

    ![Çevrimiçi Yedekleme zamanlamasını belirtin](./media/backup-azure-backup-exchange-server/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="7f6cf-154">Çevrimiçi kurtarma noktası hızlı temel unutmayın tam kurtarma noktaları.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-154">Note Online recovery points are based on express full recovery points.</span></span> <span data-ttu-id="7f6cf-155">Bu nedenle, hello çevrimiçi kurtarma noktası zamanlama belirtilen hello süredir hello sonra tam kurtarma noktası express.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-155">Therefore, you must schedule hello online recovery point after hello time that’s specified for hello express full recovery point.</span></span>
    >
    >
16. <span data-ttu-id="7f6cf-156">Merhaba bekletme ilkesi yapılandırma **Azure Backup**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-156">Configure hello retention policy for **Azure Backup**, and then click **Next**.</span></span>
17. <span data-ttu-id="7f6cf-157">Çevrimiçi çoğaltma seçeneğini belirleyin ve tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-157">Choose an online replication option and click **Next**.</span></span>

    <span data-ttu-id="7f6cf-158">Büyük bir veritabanınız varsa, hello ilk yedekleme toobe hello ağ üzerinden oluşturulan uzun bir süredir ele geçirebilir.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-158">If you have a large database, it could take a long time for hello initial backup toobe created over hello network.</span></span> <span data-ttu-id="7f6cf-159">tooavoid bu sorunu çevrimdışı yedekleme oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-159">tooavoid this issue, you can create an offline backup.</span></span>  

    ![Çevrimiçi bekletme ilkesini belirtin](./media/backup-azure-backup-exchange-server/specify-online-retention-policy.png)
18. <span data-ttu-id="7f6cf-161">Hello ayarlarını onaylayın ve ardından **Grup Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-161">Confirm hello settings, and then click **Create Group**.</span></span>
19. <span data-ttu-id="7f6cf-162">**Kapat**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-162">Click **Close**.</span></span>

## <a name="recover-hello-exchange-database"></a><span data-ttu-id="7f6cf-163">Merhaba Exchange veritabanını kurtarma</span><span class="sxs-lookup"><span data-stu-id="7f6cf-163">Recover hello Exchange database</span></span>
1. <span data-ttu-id="7f6cf-164">bir Exchange veritabanı toorecover tıklatın **kurtarma** hello DPM Yönetici Konsolu içinde.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-164">toorecover an Exchange database, click **Recovery** in hello DPM Administrator Console.</span></span>
2. <span data-ttu-id="7f6cf-165">Toorecover istediğiniz hello Exchange veritabanını bulun.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-165">Locate hello Exchange database that you want toorecover.</span></span>
3. <span data-ttu-id="7f6cf-166">Merhaba çevrimiçi bir kurtarma noktası seçin *kurtarma süresini* aşağı açılan liste.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-166">Select an online recovery point from hello *recovery time* drop-down list.</span></span>
4. <span data-ttu-id="7f6cf-167">Tıklatın **kurtarmak** toostart hello **Kurtarma Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-167">Click **Recover** toostart hello **Recovery Wizard**.</span></span>

<span data-ttu-id="7f6cf-168">Çevrimiçi kurtarma noktaları için beş kurtarma türü vardır:</span><span class="sxs-lookup"><span data-stu-id="7f6cf-168">For online recovery points, there are five recovery types:</span></span>

* <span data-ttu-id="7f6cf-169">**Toooriginal Exchange Server konumuna Kurtar:** hello veriler, kurtarılan toohello özgün Exchange server olacaktır.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-169">**Recover toooriginal Exchange Server location:** hello data will be recovered toohello original Exchange server.</span></span>
* <span data-ttu-id="7f6cf-170">**Exchange Server üzerindeki tooanother veritabanını Kurtar:** hello veriler, kurtarılan tooanother veritabanı başka bir Exchange sunucusu üzerinde olacaktır.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-170">**Recover tooanother database on an Exchange Server:** hello data will be recovered tooanother database on another Exchange server.</span></span>
* <span data-ttu-id="7f6cf-171">**Tooa kurtarma veritabanına Kurtar:** hello veriler, kurtarılan tooan Exchange kurtarma veritabanına (RDB) olacaktır.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-171">**Recover tooa Recovery Database:** hello data will be recovered tooan Exchange Recovery Database (RDB).</span></span>
* <span data-ttu-id="7f6cf-172">**Kopya tooa ağ klasörüne:** hello veriler, kurtarılan tooa ağ klasörüne olacaktır.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-172">**Copy tooa network folder:** hello data will be recovered tooa network folder.</span></span>
* <span data-ttu-id="7f6cf-173">**Tootape kopyalayın:** bir bant kitaplığınız veya ekli ve yapılandırılmış hello DPM sunucusu, hello kurtarma noktası olacaktır bir tek başına bant sürücüsünü tooa boş bant kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="7f6cf-173">**Copy tootape:** If you have a tape library or a stand-alone tape drive attached and configured on hello DPM server, hello recovery point will be copied tooa free tape.</span></span>

    ![Çevrimiçi çoğaltma seçin](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a><span data-ttu-id="7f6cf-175">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7f6cf-175">Next steps</span></span>
* [<span data-ttu-id="7f6cf-176">Azure Backup ile ilgili SSS</span><span class="sxs-lookup"><span data-stu-id="7f6cf-176">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)
