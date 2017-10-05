---
title: Bir Exchange Server'a Azure yedekleme ile System Center 2012 R2 DPM yedekleme | Microsoft Docs
description: "System Center 2012 R2 DPM kullanarak Azure yedekleme için bir Exchange server'ı Yedekle öğrenin"
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
ms.openlocfilehash: 2a0e416440e55cfde70cbd20d40c99fb29b4229c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="back-up-an-exchange-server-to-azure-backup-with-system-center-2012-r2-dpm"></a><span data-ttu-id="dbc14-103">System Center 2012 R2 DPM ile Azure Backup’a Exchange sunucusu yedekleme</span><span class="sxs-lookup"><span data-stu-id="dbc14-103">Back up an Exchange server to Azure Backup with System Center 2012 R2 DPM</span></span>
<span data-ttu-id="dbc14-104">Bu makalede Azure yedekleme için bir Microsoft Exchange sunucusunu yedeklemek için System Center 2012 R2 Data Protection Manager (DPM) sunucusunun nasıl yapılandırılacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="dbc14-104">This article describes how to configure a System Center 2012 R2 Data Protection Manager (DPM) server to back up a Microsoft Exchange server to  Azure Backup.</span></span>  

## <a name="updates"></a><span data-ttu-id="dbc14-105">Güncellemeler</span><span class="sxs-lookup"><span data-stu-id="dbc14-105">Updates</span></span>
<span data-ttu-id="dbc14-106">Azure yedekleme ile DPM sunucusu başarıyla kaydetmek için System Center 2012 R2 DPM ve Azure Yedekleme aracısı en son sürümü için en son güncelleştirme paketini yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="dbc14-106">To successfully register the DPM server with Azure Backup, you must install the latest update rollup for System Center 2012 R2 DPM and the latest version of the Azure Backup Agent.</span></span> <span data-ttu-id="dbc14-107">En son güncelleştirme paketini gelen alma [Microsoft Catalog](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=System%20Center%202012%20R2%20Data%20protection%20manager).</span><span class="sxs-lookup"><span data-stu-id="dbc14-107">Get the latest update rollup from the [Microsoft Catalog](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=System%20Center%202012%20R2%20Data%20protection%20manager).</span></span>

> [!NOTE]
> <span data-ttu-id="dbc14-108">Bu makaledeki örneklerde, Azure Yedekleme aracısı 2.0.8719.0 sürümü yüklendi ve güncelleştirme paketi 6 System Center 2012 R2 DPM üzerinde yüklü.</span><span class="sxs-lookup"><span data-stu-id="dbc14-108">For the examples in this article, version 2.0.8719.0 of the Azure Backup Agent is installed, and Update Rollup 6 is installed on System Center 2012 R2 DPM.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="dbc14-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="dbc14-109">Prerequisites</span></span>
<span data-ttu-id="dbc14-110">Devam etmeden önce emin olun tüm [Önkoşullar](backup-azure-dpm-introduction.md#prerequisites) iş yüklerini korumak için Microsoft Azure Yedekleme kullanılarak karşılandığından.</span><span class="sxs-lookup"><span data-stu-id="dbc14-110">Before you continue, make sure that all the [prerequisites](backup-azure-dpm-introduction.md#prerequisites) for using Microsoft Azure Backup to protect workloads have been met.</span></span> <span data-ttu-id="dbc14-111">Bu Önkoşullar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="dbc14-111">These prerequisites include the following:</span></span>

* <span data-ttu-id="dbc14-112">Bir yedekleme kasası Azure sitede oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="dbc14-112">A backup vault on the Azure site has been created.</span></span>
* <span data-ttu-id="dbc14-113">DPM sunucusuna aracısını ve kasa kimlik bilgileri indirildi.</span><span class="sxs-lookup"><span data-stu-id="dbc14-113">Agent and vault credentials have been downloaded to the DPM server.</span></span>
* <span data-ttu-id="dbc14-114">Aracıyı DPM sunucusuna yüklenir.</span><span class="sxs-lookup"><span data-stu-id="dbc14-114">The agent is installed on the DPM server.</span></span>
* <span data-ttu-id="dbc14-115">Kasa kimlik bilgileri, DPM sunucusunu kaydetmek için kullanılmıştır.</span><span class="sxs-lookup"><span data-stu-id="dbc14-115">The vault credentials were used to register the DPM server.</span></span>
* <span data-ttu-id="dbc14-116">Lütfen Exchange 2016 koruyorsanız, DPM 2012 R2 UR9 veya sonraki bir sürüme yükseltin</span><span class="sxs-lookup"><span data-stu-id="dbc14-116">If you are protecting Exchange 2016, please upgrade to DPM 2012 R2 UR9 or later</span></span>

## <a name="dpm-protection-agent"></a><span data-ttu-id="dbc14-117">DPM koruma Aracısı</span><span class="sxs-lookup"><span data-stu-id="dbc14-117">DPM protection agent</span></span>
<span data-ttu-id="dbc14-118">Exchange sunucusunda DPM koruma aracısı yüklemek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="dbc14-118">To install the DPM protection agent on the Exchange server, follow these steps:</span></span>

1. <span data-ttu-id="dbc14-119">Güvenlik duvarları doğru şekilde yapılandırıldığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="dbc14-119">Make sure that the firewalls are correctly configured.</span></span> <span data-ttu-id="dbc14-120">Bkz: [aracı için güvenlik duvarı özel durumlarını yapılandırma](https://technet.microsoft.com/library/Hh758204.aspx).</span><span class="sxs-lookup"><span data-stu-id="dbc14-120">See [Configure firewall exceptions for the agent](https://technet.microsoft.com/library/Hh758204.aspx).</span></span>
2. <span data-ttu-id="dbc14-121">Aracısı'nı tıklatarak Exchange sunucusunda yükleyin **Yönetim > aracıları > yükleme** DPM yönetici Konsolu'ndaki.</span><span class="sxs-lookup"><span data-stu-id="dbc14-121">Install the agent on the Exchange server by clicking **Management > Agents > Install** in DPM Administrator Console.</span></span> <span data-ttu-id="dbc14-122">Bkz: [DPM koruma Aracısı yükleme](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) ayrıntılı adımlar için.</span><span class="sxs-lookup"><span data-stu-id="dbc14-122">See [Install the DPM protection agent](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) for detailed steps.</span></span>

## <a name="create-a-protection-group-for-the-exchange-server"></a><span data-ttu-id="dbc14-123">Exchange server için bir koruma grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="dbc14-123">Create a protection group for the Exchange server</span></span>
1. <span data-ttu-id="dbc14-124">DPM Yönetici Konsolu'nda **koruma**ve ardından **yeni** açmak için araç şeridinde **yeni koruma grubu oluşturma** Sihirbazı.</span><span class="sxs-lookup"><span data-stu-id="dbc14-124">In the DPM Administrator Console, click **Protection**, and then click **New** on the tool ribbon to open the **Create New Protection Group** wizard.</span></span>
2. <span data-ttu-id="dbc14-125">Üzerinde **Hoş Geldiniz** Sihirbazı'nı ekranın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="dbc14-125">On the **Welcome** screen of the wizard click **Next**.</span></span>
3. <span data-ttu-id="dbc14-126">Üzerinde **koruma grubu türünü seçin** ekranında, seçin **sunucuları** tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="dbc14-126">On the **Select protection group type** screen, select **Servers** and click **Next**.</span></span>
4. <span data-ttu-id="dbc14-127">Tıklatıp korumak istediğiniz Exchange server veritabanını seçin **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="dbc14-127">Select the Exchange server database that you want to protect and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="dbc14-128">Exchange 2013 koruyorsanız, denetleme [Exchange 2013 önkoşulları](https://technet.microsoft.com/library/dn751029.aspx).</span><span class="sxs-lookup"><span data-stu-id="dbc14-128">If you are protecting Exchange 2013, check the [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).</span></span>
   >
   >

    <span data-ttu-id="dbc14-129">Aşağıdaki örnekte, Exchange 2010 veritabanı seçilir.</span><span class="sxs-lookup"><span data-stu-id="dbc14-129">In the following example, the Exchange 2010 database is selected.</span></span>

    ![Grup üyelerini seçin](./media/backup-azure-backup-exchange-server/select-group-members.png)
5. <span data-ttu-id="dbc14-131">Veri koruma yöntemini seçin.</span><span class="sxs-lookup"><span data-stu-id="dbc14-131">Select the data protection method.</span></span>

    <span data-ttu-id="dbc14-132">Koruma grubu adı ve her ikisi de aşağıdaki seçeneklerden birini seçin:</span><span class="sxs-lookup"><span data-stu-id="dbc14-132">Name the protection group, and then select both of the following options:</span></span>

   * <span data-ttu-id="dbc14-133">Disk kullanılan kısa vadeli koruma istiyorum.</span><span class="sxs-lookup"><span data-stu-id="dbc14-133">I want short-term protection using Disk.</span></span>
   * <span data-ttu-id="dbc14-134">Çevrimiçi koruma istiyorum.</span><span class="sxs-lookup"><span data-stu-id="dbc14-134">I want online protection.</span></span>
6. <span data-ttu-id="dbc14-135">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dbc14-135">Click **Next**.</span></span>
7. <span data-ttu-id="dbc14-136">Seçin **veri bütünlüğünü denetlemek için Eseutil'i Çalıştır** Exchange Server veritabanlarının bütünlüğünü kontrol etmek istiyorsanız seçeneği.</span><span class="sxs-lookup"><span data-stu-id="dbc14-136">Select the **Run Eseutil to check data integrity** option if you want to check the integrity of the Exchange Server databases.</span></span>

    <span data-ttu-id="dbc14-137">Bu seçeneği belirledikten sonra yedekleme tutarlılığı denetleniyor çalıştırarak oluşturulan g/ç trafiği önlemek için DPM sunucusunda çalıştırılır **eseutil** Exchange sunucusundaki komutu.</span><span class="sxs-lookup"><span data-stu-id="dbc14-137">After you select this option, backup consistency checking will be run on the DPM server to avoid the I/O traffic that’s generated by running the **eseutil** command on the Exchange server.</span></span>

   > [!NOTE]
   > <span data-ttu-id="dbc14-138">Bu seçeneği kullanmak için DPM sunucusunda C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin dizinine Ese.dll ve Eseutil.exe dosyalarını kopyalamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="dbc14-138">To use this option, you must copy the Ese.dll and Eseutil.exe files to the C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin directory on the DPM server.</span></span> <span data-ttu-id="dbc14-139">Aksi takdirde, aşağıdaki hata tetiklenir:</span><span class="sxs-lookup"><span data-stu-id="dbc14-139">Otherwise, the following error is triggered:</span></span>  
   > <span data-ttu-id="dbc14-140">![Eseutil hata](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span><span class="sxs-lookup"><span data-stu-id="dbc14-140">![eseutil error](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span></span>
   >
   >
8. <span data-ttu-id="dbc14-141">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dbc14-141">Click **Next**.</span></span>
9. <span data-ttu-id="dbc14-142">Veritabanı için seçin **kopya yedekleme**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="dbc14-142">Select the database for **Copy Backup**, and then click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="dbc14-143">Bir veritabanı en az bir DAG kopyası için "tam yedekleme" seçeneğini belirlemezseniz günlükler kesilmez.</span><span class="sxs-lookup"><span data-stu-id="dbc14-143">If you do not select “Full backup” for at least one DAG copy of a database, logs will not be truncated.</span></span>
   >
   >
10. <span data-ttu-id="dbc14-144">Hedefler için yapılandırma **kısa vadeli yedekleme**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="dbc14-144">Configure the goals for **Short-Term backup**, and then click **Next**.</span></span>
11. <span data-ttu-id="dbc14-145">Kullanılabilir disk alanını gözden geçirin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="dbc14-145">Review the available disk space, and then click **Next**.</span></span>
12. <span data-ttu-id="dbc14-146">Hangi DPM sunucusunu ilk çoğaltma oluşturur ve ardından istediğiniz saati seçin **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="dbc14-146">Select the time at which the DPM server will create the initial replication, and then click **Next**.</span></span>
13. <span data-ttu-id="dbc14-147">Tutarlılık denetimi seçeneklerini seçin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="dbc14-147">Select the consistency check options, and then click **Next**.</span></span>
14. <span data-ttu-id="dbc14-148">Azure'a yedeklemek ve ardından istediğiniz veritabanını seçin **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="dbc14-148">Choose the database that you want to back up to Azure, and then click **Next**.</span></span> <span data-ttu-id="dbc14-149">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="dbc14-149">For example:</span></span>

    ![Çevrimiçi koruma verilerini belirtin](./media/backup-azure-backup-exchange-server/specify-online-protection-data.png)
15. <span data-ttu-id="dbc14-151">İçin zamanlama tanımla **Azure Backup**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="dbc14-151">Define the schedule for **Azure Backup**, and then click **Next**.</span></span> <span data-ttu-id="dbc14-152">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="dbc14-152">For example:</span></span>

    ![Çevrimiçi Yedekleme zamanlamasını belirtin](./media/backup-azure-backup-exchange-server/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="dbc14-154">Çevrimiçi kurtarma noktası hızlı temel unutmayın tam kurtarma noktaları.</span><span class="sxs-lookup"><span data-stu-id="dbc14-154">Note Online recovery points are based on express full recovery points.</span></span> <span data-ttu-id="dbc14-155">Bu nedenle, belirtilen süre için hızlı tam kurtarma noktası sonra çevrimiçi kurtarma noktası zamanlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="dbc14-155">Therefore, you must schedule the online recovery point after the time that’s specified for the express full recovery point.</span></span>
    >
    >
16. <span data-ttu-id="dbc14-156">Bekletme İlkesi yapılandırma **Azure Backup**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="dbc14-156">Configure the retention policy for **Azure Backup**, and then click **Next**.</span></span>
17. <span data-ttu-id="dbc14-157">Çevrimiçi çoğaltma seçeneğini belirleyin ve tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="dbc14-157">Choose an online replication option and click **Next**.</span></span>

    <span data-ttu-id="dbc14-158">Büyük bir veritabanınız varsa, ağ üzerinden oluşturulacak ilk yedekleme uzun bir süredir ele geçirebilir.</span><span class="sxs-lookup"><span data-stu-id="dbc14-158">If you have a large database, it could take a long time for the initial backup to be created over the network.</span></span> <span data-ttu-id="dbc14-159">Bu sorunu önlemek için Çevrimdışı Yedekleme oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dbc14-159">To avoid this issue, you can create an offline backup.</span></span>  

    ![Çevrimiçi bekletme ilkesini belirtin](./media/backup-azure-backup-exchange-server/specify-online-retention-policy.png)
18. <span data-ttu-id="dbc14-161">Ayarları onaylayın ve ardından **Grup Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="dbc14-161">Confirm the settings, and then click **Create Group**.</span></span>
19. <span data-ttu-id="dbc14-162">**Kapat**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dbc14-162">Click **Close**.</span></span>

## <a name="recover-the-exchange-database"></a><span data-ttu-id="dbc14-163">Exchange veritabanını kurtarma</span><span class="sxs-lookup"><span data-stu-id="dbc14-163">Recover the Exchange database</span></span>
1. <span data-ttu-id="dbc14-164">Bir Exchange veritabanını kurtarmak için **kurtarma** DPM Yönetici Konsolu'nun.</span><span class="sxs-lookup"><span data-stu-id="dbc14-164">To recover an Exchange database, click **Recovery** in the DPM Administrator Console.</span></span>
2. <span data-ttu-id="dbc14-165">Kurtarmak istediğiniz Exchange veritabanı bulun.</span><span class="sxs-lookup"><span data-stu-id="dbc14-165">Locate the Exchange database that you want to recover.</span></span>
3. <span data-ttu-id="dbc14-166">Bir çevrimiçi kurtarma noktası seçin *kurtarma süresini* aşağı açılan liste.</span><span class="sxs-lookup"><span data-stu-id="dbc14-166">Select an online recovery point from the *recovery time* drop-down list.</span></span>
4. <span data-ttu-id="dbc14-167">Tıklatın **kurtarmak** başlatmak için **Kurtarma Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="dbc14-167">Click **Recover** to start the **Recovery Wizard**.</span></span>

<span data-ttu-id="dbc14-168">Çevrimiçi kurtarma noktaları için beş kurtarma türü vardır:</span><span class="sxs-lookup"><span data-stu-id="dbc14-168">For online recovery points, there are five recovery types:</span></span>

* <span data-ttu-id="dbc14-169">**Özgün Exchange Server konumuna Kurtar:** verileri özgün Exchange Server'a kurtarılır.</span><span class="sxs-lookup"><span data-stu-id="dbc14-169">**Recover to original Exchange Server location:** The data will be recovered to the original Exchange server.</span></span>
* <span data-ttu-id="dbc14-170">**Exchange Server üzerindeki başka bir veritabanına Kurtar:** verileri başka bir Exchange server üzerindeki başka bir veritabanına kurtarıldı.</span><span class="sxs-lookup"><span data-stu-id="dbc14-170">**Recover to another database on an Exchange Server:** The data will be recovered to another database on another Exchange server.</span></span>
* <span data-ttu-id="dbc14-171">**Kurtarma veritabanına Kurtar:** verileri bir Exchange kurtarma veritabanına (RDB) kurtarılacak.</span><span class="sxs-lookup"><span data-stu-id="dbc14-171">**Recover to a Recovery Database:** The data will be recovered to an Exchange Recovery Database (RDB).</span></span>
* <span data-ttu-id="dbc14-172">**Bir ağ klasörüne kopyala:** verileri bir ağ klasörüne kurtarılacak.</span><span class="sxs-lookup"><span data-stu-id="dbc14-172">**Copy to a network folder:** The data will be recovered to a network folder.</span></span>
* <span data-ttu-id="dbc14-173">**Banda Kopyala:** bir bant kitaplığını veya bağlı ve DPM sunucusunda yapılandırılmış tek başına bant sürücüsü varsa, kurtarma noktası bir boş banda kopyalanacak.</span><span class="sxs-lookup"><span data-stu-id="dbc14-173">**Copy to tape:** If you have a tape library or a stand-alone tape drive attached and configured on the DPM server, the recovery point will be copied to a free tape.</span></span>

    ![Çevrimiçi çoğaltma seçin](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a><span data-ttu-id="dbc14-175">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="dbc14-175">Next steps</span></span>
* [<span data-ttu-id="dbc14-176">Azure Backup ile ilgili SSS</span><span class="sxs-lookup"><span data-stu-id="dbc14-176">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)
