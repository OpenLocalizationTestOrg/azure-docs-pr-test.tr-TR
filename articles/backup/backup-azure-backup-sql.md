---
title: "DPM kullanarak SQL Server iş yükleri için Azure yedeklemeyi | Microsoft Docs"
description: "Azure Yedekleme hizmetini kullanarak SQL Server veritabanlarını yedekleme için bir giriş"
services: backup
documentationcenter: 
author: adigan
manager: Nkolli
editor: 
ms.assetid: 59df5bec-d959-457d-8731-7b20f7f1013e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adigan;giridham;jimpark;markgal;trinadhk
ms.openlocfilehash: c9edc066ea2edc9cd4b8453047d5584a588174dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="back-up-sql-server-to-azure-as-a-dpm-workload"></a><span data-ttu-id="be712-103">SQL Server'ı Azure'a DPM iş yükü yedekle</span><span class="sxs-lookup"><span data-stu-id="be712-103">Back up SQL Server to Azure as a DPM workload</span></span>
<span data-ttu-id="be712-104">Bu makalede Azure Yedekleme'yi kullanarak SQL Server veritabanlarının yedekleme için yapılandırma adımlarını size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="be712-104">This article leads you through the configuration steps for backup of SQL Server databases using Azure Backup.</span></span>

<span data-ttu-id="be712-105">Azure için SQL Server veritabanlarını yedeklemek için bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="be712-105">To back up SQL Server databases to Azure, you need an Azure account.</span></span> <span data-ttu-id="be712-106">Bir hesabınız yoksa yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be712-106">If you don’t have an account, you can create a free trial account in just couple of minutes.</span></span> <span data-ttu-id="be712-107">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="be712-107">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="be712-108">Azure ve Azure kurtarma için SQL Server Veritabanı yedeğinin yönetim üç adımdan oluşur:</span><span class="sxs-lookup"><span data-stu-id="be712-108">The management of SQL Server database backup to Azure and recovery from Azure involves three steps:</span></span>

1. <span data-ttu-id="be712-109">Azure SQL Server veritabanlarını korumak için bir yedekleme ilkesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="be712-109">Create a backup policy to protect SQL Server databases to Azure.</span></span>
2. <span data-ttu-id="be712-110">İsteğe bağlı Azure yedek kopyalarını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="be712-110">Create on-demand backup copies to Azure.</span></span>
3. <span data-ttu-id="be712-111">Veritabanını Azure'dan kurtarma.</span><span class="sxs-lookup"><span data-stu-id="be712-111">Recover the database from Azure.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="be712-112">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="be712-112">Before you start</span></span>
<span data-ttu-id="be712-113">Başlamadan önce emin tüm [Önkoşullar](backup-azure-dpm-introduction.md#prerequisites) iş yüklerini korumak için Microsoft Azure Yedekleme kullanılarak karşılandığından.</span><span class="sxs-lookup"><span data-stu-id="be712-113">Before you begin, ensure that all the [prerequisites](backup-azure-dpm-introduction.md#prerequisites) for using Microsoft Azure Backup to protect workloads have been met.</span></span> <span data-ttu-id="be712-114">Önkoşullar gibi görevleri kapsar: bir yedekleme kasası oluşturma, kasa kimlik bilgilerini indirme, Azure yedekleme Aracısı'nı yükleme ve sunucu kasası ile kaydediliyor.</span><span class="sxs-lookup"><span data-stu-id="be712-114">The prerequisites cover tasks such as: creating a backup vault, downloading vault credentials, installing the Azure Backup Agent, and registering the server with the vault.</span></span>

## <a name="create-a-backup-policy-to-protect-sql-server-databases-to-azure"></a><span data-ttu-id="be712-115">Azure SQL Server veritabanlarını korumak için bir yedekleme İlkesi Oluştur</span><span class="sxs-lookup"><span data-stu-id="be712-115">Create a backup policy to protect SQL Server databases to Azure</span></span>
1. <span data-ttu-id="be712-116">DPM sunucusunda **koruma** çalışma.</span><span class="sxs-lookup"><span data-stu-id="be712-116">On the DPM server, click the **Protection** workspace.</span></span>
2. <span data-ttu-id="be712-117">Araç şeridinde tıklatın **yeni** yeni bir koruma grubu oluşturulamıyor.</span><span class="sxs-lookup"><span data-stu-id="be712-117">On the tool ribbon, click **New** to create a new protection group.</span></span>

    ![Koruma grubu oluşturma](./media/backup-azure-backup-sql/protection-group.png)
3. <span data-ttu-id="be712-119">DPM gösterir yönlendirme ile başlangıç ekranı oluşturma ile ilgili bir **koruma grubu**.</span><span class="sxs-lookup"><span data-stu-id="be712-119">DPM shows the start screen with the guidance on creating a **Protection Group**.</span></span> <span data-ttu-id="be712-120">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="be712-120">Click **Next**.</span></span>
4. <span data-ttu-id="be712-121">Seçin **sunucuları**.</span><span class="sxs-lookup"><span data-stu-id="be712-121">Select **Servers**.</span></span>

    ![Koruma grubu türü - 'Sunucuları' seçin](./media/backup-azure-backup-sql/pg-servers.png)
5. <span data-ttu-id="be712-123">Yedeklenecek veritabanlarını mevcut olduğu SQL Server makinesinde genişletin.</span><span class="sxs-lookup"><span data-stu-id="be712-123">Expand the SQL Server machine where the databases to be backed up are present.</span></span> <span data-ttu-id="be712-124">DPM, o sunucudan yedeklenebilir çeşitli veri kaynakları gösterir.</span><span class="sxs-lookup"><span data-stu-id="be712-124">DPM shows various data sources that can be backed up from that server.</span></span> <span data-ttu-id="be712-125">Genişletme **tüm SQL paylaşımları** ve yedeklenmesi için (Bu durumda biz seçili ReportServer$ MSDPM2012 ve ReportServer$ MSDPM2012TempDB) veritabanlarını seçin.</span><span class="sxs-lookup"><span data-stu-id="be712-125">Expand the **All SQL Shares** and select the databases (in this case we selected ReportServer$MSDPM2012 and ReportServer$MSDPM2012TempDB) to be backed up.</span></span> <span data-ttu-id="be712-126">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="be712-126">Click **Next**.</span></span>

    ![SQL DB seçin](./media/backup-azure-backup-sql/pg-databases.png)
6. <span data-ttu-id="be712-128">Koruma grubu için bir ad ve seçin **çevrimiçi koruma istiyorum** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="be712-128">Provide a name for the protection group and select the **I want online Protection** checkbox.</span></span>

    ![Veri koruma yöntemini - kısa süreli disk ve çevrimiçi Azure](./media/backup-azure-backup-sql/pg-name.png)
7. <span data-ttu-id="be712-130">İçinde **kısa vadeli hedefleri belirtin** ekranında, diske yedekleme noktaları oluşturmak için gerekli girişleri içerir.</span><span class="sxs-lookup"><span data-stu-id="be712-130">In the **Specify Short-Term Goals** screen, include the necessary inputs to create backup points to disk.</span></span>

    <span data-ttu-id="be712-131">Burada, gösteriliyor **bekletme aralığı** ayarlanır *5 gün*, **eşitleme sıklığı** için bir kez ayarlanır her *15 dakika* yedekleme alınır sıklığı olduğu.</span><span class="sxs-lookup"><span data-stu-id="be712-131">Here we see that **Retention range** is set to *5 days*, **Synchronization frequency** is set to once every *15 minutes* which is the frequency at which backup is taken.</span></span> <span data-ttu-id="be712-132">**Hızlı tam yedekleme** ayarlanır *fiyatlara*.</span><span class="sxs-lookup"><span data-stu-id="be712-132">**Express Full Backup** is set to *8:00 P.M*.</span></span>

    ![Kısa vadeli hedefleri](./media/backup-azure-backup-sql/pg-shortterm.png)

   > [!NOTE]
   > <span data-ttu-id="be712-134">8:00 PM (göre ekran giriş), bir yedekleme noktasının önceki günün 8:00 PM yedekleme noktasından değiştirilmiş verileri aktararak her gün oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="be712-134">At 8:00 PM (according to the screen input) a backup point is created every day by transferring the data that has been modified from the previous day’s 8:00 PM backup point.</span></span> <span data-ttu-id="be712-135">Bu işlem çağrılırken **hızlı tam yedekleme**.</span><span class="sxs-lookup"><span data-stu-id="be712-135">This process is called **Express Full Backup**.</span></span> <span data-ttu-id="be712-136">Günlükleri eşzamanlı işlem sırasında her 15 dakikada varsa 9: 00'da – veritabanını kurtarmak için gerekirse son günlüklerini tekrarlamak tarafından oluşturulan noktası sonra hızlı tam yedekleme noktası (Bu durumda 8 pm).</span><span class="sxs-lookup"><span data-stu-id="be712-136">While the transaction logs are synchronized every 15 minutes, if there is a need to recover the database at 9:00 PM – then the point is created by replaying the logs from the last express full backup point (8pm in this case).</span></span>
   >
   >

8. <span data-ttu-id="be712-137">**İleri**’ye tıklayın</span><span class="sxs-lookup"><span data-stu-id="be712-137">Click **Next**</span></span>

    <span data-ttu-id="be712-138">DPM, genel depolama alanı ve olası disk alanı kullanımını gösterir.</span><span class="sxs-lookup"><span data-stu-id="be712-138">DPM shows the overall storage space available and the potential disk space utilization.</span></span>

    ![Disk ayırma](./media/backup-azure-backup-sql/pg-storage.png)

    <span data-ttu-id="be712-140">Varsayılan olarak, DPM ilk yedek kopya için kullanılan veri kaynağı (SQL Server veritabanı) başına tek bir birim oluşturur.</span><span class="sxs-lookup"><span data-stu-id="be712-140">By default, DPM creates one volume per data source (SQL Server database) which is used for the initial backup copy.</span></span> <span data-ttu-id="be712-141">Bu yaklaşımı kullanarak, Mantıksal Disk Yöneticisi (LDM) DPM koruma 300 veri kaynakları (SQL Server veritabanları) için sınırlar.</span><span class="sxs-lookup"><span data-stu-id="be712-141">Using this approach, the Logical Disk Manager (LDM) limits DPM protection to 300 data sources (SQL Server databases).</span></span> <span data-ttu-id="be712-142">Bu sınırlamaya geçici bir çözüm için seçin **DPM depolama Havuzu'ndaki verileri birlikte bulundur**, seçeneği.</span><span class="sxs-lookup"><span data-stu-id="be712-142">To work around this limitation, select the **Co-locate data in DPM Storage Pool**, option.</span></span> <span data-ttu-id="be712-143">Bu seçeneği kullanırsanız, DPM tek bir birimde birden çok veri kaynağı için en fazla 2000 SQL veritabanlarını korumak DPM sağlayan kullanır.</span><span class="sxs-lookup"><span data-stu-id="be712-143">If you use this option, DPM uses a single volume for multiple data sources, which allows DPM to protect up to 2000 SQL databases.</span></span>

    <span data-ttu-id="be712-144">Varsa **birimleri otomatik olarak büyütün** seçeneği seçildiğinde, üretim verileri büyüdükçe, DPM artan yedekleme birimi için hesap.</span><span class="sxs-lookup"><span data-stu-id="be712-144">If **Automatically grow the volumes** option is selected, DPM can account for the increased backup volume as the production data grows.</span></span> <span data-ttu-id="be712-145">Varsa **birimleri otomatik olarak büyütün** seçeneği seçili değilse, DPM koruma grubundaki veri kaynakları için kullanılan yedekleme depolama sınırlar.</span><span class="sxs-lookup"><span data-stu-id="be712-145">If **Automatically grow the volumes** option is not selected, DPM limits the backup storage used to the data sources in the protection group.</span></span>
9. <span data-ttu-id="be712-146">Yöneticiler, bant genişliği tıkanıklık önlemek için bu ilk yedekleme el ile (Kapalı ağ) aktarılması veya ağ üzerinden seçeneği sunulur.</span><span class="sxs-lookup"><span data-stu-id="be712-146">Administrators are given the choice of transferring this initial backup manually (off network) to avoid bandwidth congestion or over the network.</span></span> <span data-ttu-id="be712-147">Bunlar, ilk aktarımı oluşabilir zaman da yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be712-147">They can also configure the time at which the initial transfer can happen.</span></span> <span data-ttu-id="be712-148">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="be712-148">Click **Next**.</span></span>

    ![İlk çoğaltma yöntemi](./media/backup-azure-backup-sql/pg-manual.png)

    <span data-ttu-id="be712-150">İlk yedekleme kopyasının tüm veri kaynağı (SQL Server veritabanı) sunucusundan aktarımını üretim (SQL Server makinesinde) DPM sunucusuna gerektirir.</span><span class="sxs-lookup"><span data-stu-id="be712-150">The initial backup copy requires transfer of the entire data source (SQL Server database) from production server (SQL Server machine) to the DPM server.</span></span> <span data-ttu-id="be712-151">Bu veri büyük olabilir ve ağ üzerinden veri aktarırken bant genişliği aşabilir.</span><span class="sxs-lookup"><span data-stu-id="be712-151">This data might be large, and transferring the data over the network could exceed bandwidth.</span></span> <span data-ttu-id="be712-152">Bu nedenle, ilk yedekleme aktarmak Yöneticiler seçebilirsiniz: **el ile** (çıkarılabilir medya kullanarak) bant genişliği tıkanıklık önlemek için veya **otomatik olarak ağ üzerinden** (bir belirtilen zamanda).</span><span class="sxs-lookup"><span data-stu-id="be712-152">For this reason, administrators can choose to transfer the initial backup: **Manually** (using removable media) to avoid bandwidth congestion, or **Automatically over the network** (at a specified time).</span></span>

    <span data-ttu-id="be712-153">İlk Yedekleme tamamlandıktan sonra yedekleri geri kalanı ilk yedek kopyanın artımlı yedeklemelerin olduğu.</span><span class="sxs-lookup"><span data-stu-id="be712-153">Once the initial backup is complete, the rest of the backups are incremental backups on the initial backup copy.</span></span> <span data-ttu-id="be712-154">Artımlı yedeklemeler küçük olma eğilimindedir ve ağ üzerinden kolayca aktarılır.</span><span class="sxs-lookup"><span data-stu-id="be712-154">Incremental backups tend to be small and are easily transferred across the network.</span></span>
10. <span data-ttu-id="be712-155">Tutarlılık denetimi çalıştırın ve tıklatın istediğinizde seçin **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="be712-155">Choose when you want the consistency check to run and click **Next**.</span></span>

    ![Tutarlılık denetimi](./media/backup-azure-backup-sql/pg-consistent.png)

    <span data-ttu-id="be712-157">DPM, yedekleme noktası bütünlüğünü denetlemek için bir tutarlılık gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be712-157">DPM can perform a consistency check to check the integrity of the backup point.</span></span> <span data-ttu-id="be712-158">Yedekleme dosyasının (SQL Server makinesinde bu senaryoda) üretim sunucusunda ve yedeklenmiş verileri DPM, bu dosya için sağlama toplamı hesaplar.</span><span class="sxs-lookup"><span data-stu-id="be712-158">It calculates the checksum of the backup file on the production server (SQL Server machine in this scenario) and the backed-up data for that file at DPM.</span></span> <span data-ttu-id="be712-159">Bir çakışma olması durumunda, DPM, yedeklenen dosyasının bozuk olduğunun varsayılır.</span><span class="sxs-lookup"><span data-stu-id="be712-159">In the case of a conflict, it is assumed that the backed-up file at DPM is corrupt.</span></span> <span data-ttu-id="be712-160">DPM, yedeklenen verileri sağlama toplamı eşleşmezliği karşılık gelen blokları göndererek rectifies.</span><span class="sxs-lookup"><span data-stu-id="be712-160">DPM rectifies the backed-up data by sending the blocks corresponding to the checksum mismatch.</span></span> <span data-ttu-id="be712-161">Tutarlılık denetimi performansı yoğun bir işlem olduğundan, yöneticilerin tutarlılık denetimi zamanlaması veya otomatik olarak çalıştırarak seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="be712-161">As the consistency check is a performance-intensive operation, administrators have the option of scheduling the consistency check or running it automatically.</span></span>
11. <span data-ttu-id="be712-162">Veri kaynaklarının çevrimiçi korumasını belirtmek için Azure ve seçeneğini korunacak veritabanı seçin **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="be712-162">To specify online protection of the datasources, select the databases to be protected to Azure and click **Next**.</span></span>

    ![Veri kaynakları seçin](./media/backup-azure-backup-sql/pg-sqldatabases.png)
12. <span data-ttu-id="be712-164">Yöneticiler, yedekleme zamanlamaları ve kuruluşun ilkelerini uygun bekletme ilkeleri seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be712-164">Administrators can choose backup schedules and retention policies that suit their organization policies.</span></span>

    ![Zamanlama ve bekletme](./media/backup-azure-backup-sql/pg-schedule.png)

    <span data-ttu-id="be712-166">Bu örnekte, yedeklemeleri günde bir kez 12: 00'dan ve 8 PM (ekranın alt bölümünün) alınır</span><span class="sxs-lookup"><span data-stu-id="be712-166">In this example, backups are taken once a day at 12:00 PM and 8 PM (bottom part of the screen)</span></span>

    > [!NOTE]
    > <span data-ttu-id="be712-167">Hızlı Kurtarma için diskte birkaç kısa vadeli kurtarma noktaları için iyi bir uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="be712-167">It’s a good practice to have a few short-term recovery points on disk, for quick recovery.</span></span> <span data-ttu-id="be712-168">Bu kurtarma noktaları "işletimsel kurtarma için" kullanılır.</span><span class="sxs-lookup"><span data-stu-id="be712-168">These recovery points are used for “operational recovery".</span></span> <span data-ttu-id="be712-169">Azure yüksek SLA ile iyi site dışı konumu olarak hizmet verir ve kullanılabilirliğini garanti.</span><span class="sxs-lookup"><span data-stu-id="be712-169">Azure serves as a good offsite location with higher SLAs and guaranteed availability.</span></span>
    >
    >

    <span data-ttu-id="be712-170">**En iyi uygulaması**: DPM kullanarak yerel disk yedekleme tamamlandıktan sonra zamanlanmış Azure yedeklemeler emin olun.</span><span class="sxs-lookup"><span data-stu-id="be712-170">**Best Practice**: Make sure that Azure Backups are scheduled after the completion of local disk backups using DPM.</span></span> <span data-ttu-id="be712-171">Bu, Azure'a kopyalanacak en son disk yedeklemesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="be712-171">This enables the latest disk backup to be copied to Azure.</span></span>

13. <span data-ttu-id="be712-172">Bekletme İlkesi zamanlamayı seçin.</span><span class="sxs-lookup"><span data-stu-id="be712-172">Choose the retention policy schedule.</span></span> <span data-ttu-id="be712-173">Bekletme İlkesi nasıl çalıştığı hakkında bilgi sırasında sağlanan [bant altyapısı Makalenizi değiştirmek için Azure Yedekleme'yi](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="be712-173">The details on how the retention policy works are provided at [Use Azure Backup to replace your tape infrastructure article](backup-azure-backup-cloud-as-tape.md).</span></span>

    ![Bekletme İlkesi](./media/backup-azure-backup-sql/pg-retentionschedule.png)

    <span data-ttu-id="be712-175">Bu örnekte:</span><span class="sxs-lookup"><span data-stu-id="be712-175">In this example:</span></span>

    * <span data-ttu-id="be712-176">Yedekleme günde bir kez 12: 00'dan ve 8 PM (ekranın alt bölümünün) alınır ve 180 gün için korunur.</span><span class="sxs-lookup"><span data-stu-id="be712-176">Backups are taken once a day at 12:00 PM and 8 PM (bottom part of the screen) and are retained for 180 days.</span></span>
    * <span data-ttu-id="be712-177">Cumartesi 12: 00'da bir yedekleme</span><span class="sxs-lookup"><span data-stu-id="be712-177">The backup on Saturday at 12:00 P.M.</span></span> <span data-ttu-id="be712-178">104 hafta boyunca tutulur</span><span class="sxs-lookup"><span data-stu-id="be712-178">is retained for 104 weeks</span></span>
    * <span data-ttu-id="be712-179">Son Cumartesi 12: 00'da bir yedekleme</span><span class="sxs-lookup"><span data-stu-id="be712-179">The backup on Last Saturday at 12:00 P.M.</span></span> <span data-ttu-id="be712-180">60 ay korunur</span><span class="sxs-lookup"><span data-stu-id="be712-180">is retained for 60 months</span></span>
    * <span data-ttu-id="be712-181">Son Cumartesi 12: 00'da Mart yedekleme</span><span class="sxs-lookup"><span data-stu-id="be712-181">The backup on Last Saturday of March at 12:00 P.M.</span></span> <span data-ttu-id="be712-182">10 yılı aşkın korunur</span><span class="sxs-lookup"><span data-stu-id="be712-182">is retained for 10 years</span></span>
14. <span data-ttu-id="be712-183">Tıklatın **sonraki** ve Azure'a ilk yedek kopyayı aktarmak için uygun seçeneği belirleyin.</span><span class="sxs-lookup"><span data-stu-id="be712-183">Click **Next** and select the appropriate option for transferring the initial backup copy to Azure.</span></span> <span data-ttu-id="be712-184">Seçebileceğiniz **otomatik olarak ağ üzerinden** veya **Çevrimdışı Yedekleme**.</span><span class="sxs-lookup"><span data-stu-id="be712-184">You can choose **Automatically over the network** or **Offline Backup**.</span></span>

    * <span data-ttu-id="be712-185">**Ağ üzerinden otomatik olarak** yedekleme için seçilen zamanlamaya göre yedekleme verileri Azure'a aktarır.</span><span class="sxs-lookup"><span data-stu-id="be712-185">**Automatically over the network** transfers the backup data to Azure as per the schedule chosen for backup.</span></span>
    * <span data-ttu-id="be712-186">Nasıl **Çevrimdışı Yedekleme** works açıklanmıştır adresindeki [Çevrimdışı Yedekleme iş akışı Azure Yedekleme'de](backup-azure-backup-import-export.md).</span><span class="sxs-lookup"><span data-stu-id="be712-186">How **Offline Backup** works is explained at [Offline Backup workflow in Azure Backup](backup-azure-backup-import-export.md).</span></span>

    <span data-ttu-id="be712-187">İlk yedek kopyayı Azure ve seçeneğini göndermek için ilgili aktarım mekanizması seçin **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="be712-187">Choose the relevant transfer mechanism to send the initial backup copy to Azure and click **Next**.</span></span>
15. <span data-ttu-id="be712-188">İlke ayrıntıları gözden geçirin sonra **Özet** ekranında, tıklayın **Grup Oluştur** iş akışını tamamlamak için düğmesini.</span><span class="sxs-lookup"><span data-stu-id="be712-188">Once you review the policy details in the **Summary** screen, click on the **Create group** button to complete the workflow.</span></span> <span data-ttu-id="be712-189">Tıklayabilirsiniz **Kapat** düğmesini tıklatın ve çalışma alanı izleme işin ilerleme durumunu izleyin.</span><span class="sxs-lookup"><span data-stu-id="be712-189">You can click the **Close** button and monitor the job progress in Monitoring workspace.</span></span>

    ![Devam eden için koruma grubu oluşturma](./media/backup-azure-backup-sql/pg-summary.png)

## <a name="on-demand-backup-of-a-sql-server-database"></a><span data-ttu-id="be712-191">İsteğe bağlı bir SQL Server veritabanının yedeğini</span><span class="sxs-lookup"><span data-stu-id="be712-191">On-demand backup of a SQL Server database</span></span>
<span data-ttu-id="be712-192">Bir yedekleme İlkesi önceki adımlarda oluşturduğunuz sırada "kurtarma noktası" yalnızca ilk yedek oluştuğunda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="be712-192">While the previous steps created a backup policy, a “recovery point” is created only when the first backup occurs.</span></span> <span data-ttu-id="be712-193">İlkenin etkisini gösterip için Zamanlayıcı için beklemek yerine, tetikleyici kurtarma oluşturulması aşağıdaki adımları el ile gelin.</span><span class="sxs-lookup"><span data-stu-id="be712-193">Rather than waiting for the scheduler to kick in, the steps below trigger the creation of a recovery point manually.</span></span>

1. <span data-ttu-id="be712-194">Koruma grubu durumunu görüntüleyene kadar bekleyin **Tamam** kurtarma noktası oluşturmadan önce veritabanı için.</span><span class="sxs-lookup"><span data-stu-id="be712-194">Wait until the protection group status shows **OK** for the database before creating the recovery point.</span></span>

    ![Koruma grubu üyeleri](./media/backup-azure-backup-sql/sqlbackup-recoverypoint.png)
2. <span data-ttu-id="be712-196">Sağ tıklatın ve veritabanı **kurtarma noktası oluştur**.</span><span class="sxs-lookup"><span data-stu-id="be712-196">Right-click on the database and select **Create Recovery Point**.</span></span>

    ![Çevrimiçi kurtarma noktası oluştur](./media/backup-azure-backup-sql/sqlbackup-createrp.png)
3. <span data-ttu-id="be712-198">Seçin **çevrimiçi koruma** açılan menüsüne ve ardından içinde **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="be712-198">Choose **Online Protection** in the drop-down menu and click **OK**.</span></span> <span data-ttu-id="be712-199">Bu, Azure'da bir kurtarma noktası oluşturma başlatır.</span><span class="sxs-lookup"><span data-stu-id="be712-199">This starts the creation of a recovery point in Azure.</span></span>

    ![Kurtarma noktası oluştur](./media/backup-azure-backup-sql/sqlbackup-azure.png)
4. <span data-ttu-id="be712-201">İçinde iş ilerleme durumunu görüntüleyebilirsiniz **izleme** burada bulabilirsiniz etmekte olan bir çalışma alanında bir içinde gösterilen gibi iş sonraki şekilde.</span><span class="sxs-lookup"><span data-stu-id="be712-201">You can view the job progress in the **Monitoring** workspace where you'll find an in progress job like the one depicted in the next figure.</span></span>

    ![İzleme konsolu](./media/backup-azure-backup-sql/sqlbackup-monitoring.png)

## <a name="recover-a-sql-server-database-from-azure"></a><span data-ttu-id="be712-203">SQL Server veritabanını Azure'dan kurtarma</span><span class="sxs-lookup"><span data-stu-id="be712-203">Recover a SQL Server database from Azure</span></span>
<span data-ttu-id="be712-204">Aşağıdaki adımlar, bir Korunan varlık (SQL Server veritabanı) Azure yedeklemeden kurtarmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="be712-204">The following steps are required to recover a protected entity (SQL Server database) from Azure.</span></span>

1. <span data-ttu-id="be712-205">DPM sunucusu Yönetim Konsolu'nu açın.</span><span class="sxs-lookup"><span data-stu-id="be712-205">Open the DPM server Management Console.</span></span> <span data-ttu-id="be712-206">Gidin **kurtarma** burada görebilirsiniz sunucuları çalışma DPM tarafından yedeklenen.</span><span class="sxs-lookup"><span data-stu-id="be712-206">Navigate to **Recovery** workspace where you can see the servers backed up by DPM.</span></span> <span data-ttu-id="be712-207">Gerekli veritabanında (Bu örnek ReportServer$ MSDPM2012) göz atın.</span><span class="sxs-lookup"><span data-stu-id="be712-207">Browse the required database (in this case ReportServer$MSDPM2012).</span></span> <span data-ttu-id="be712-208">Seçin bir **kurtarma** ile biten zaman **çevrimiçi**.</span><span class="sxs-lookup"><span data-stu-id="be712-208">Select a **Recovery from** time which ends with **Online**.</span></span>

    ![Kurtarma noktası seçin](./media/backup-azure-backup-sql/sqlbackup-restorepoint.png)
2. <span data-ttu-id="be712-210">Veritabanı adını sağ tıklatıp **kurtarmak**.</span><span class="sxs-lookup"><span data-stu-id="be712-210">Right-click the database name and click **Recover**.</span></span>

    ![Azure'dan kurtarma](./media/backup-azure-backup-sql/sqlbackup-recover.png)
3. <span data-ttu-id="be712-212">DPM, kurtarma noktası ayrıntılarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="be712-212">DPM shows the details of the recovery point.</span></span> <span data-ttu-id="be712-213">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="be712-213">Click **Next**.</span></span> <span data-ttu-id="be712-214">Veritabanının üzerine yazmak için kurtarma türünü seçin **özgün SQL Server örneğine Kurtar**.</span><span class="sxs-lookup"><span data-stu-id="be712-214">To overwrite the database, select the recovery type **Recover to original instance of SQL Server**.</span></span> <span data-ttu-id="be712-215">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="be712-215">Click **Next**.</span></span>

    ![Özgün konuma Kurtar](./media/backup-azure-backup-sql/sqlbackup-recoveroriginal.png)

    <span data-ttu-id="be712-217">Bu örnekte, DPM, başka bir SQL Server örneğine veya tek başına bir ağ klasörüne kurtarma veritabanının verir.</span><span class="sxs-lookup"><span data-stu-id="be712-217">In this example, DPM allows recovery of the database to another SQL Server instance or to a standalone network folder.</span></span>
4. <span data-ttu-id="be712-218">İçinde **belirtin Kurtarma Seçenekleri** ekran, Kurtarma tarafından kullanılan bant genişliğini azaltmak için ağ bant genişliği kullanımını azaltma gibi kurtarma seçenekleri seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be712-218">In the **Specify Recovery options** screen, you can select the recovery options like Network bandwidth usage throttling to throttle the bandwidth used by recovery.</span></span> <span data-ttu-id="be712-219">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="be712-219">Click **Next**.</span></span>
5. <span data-ttu-id="be712-220">İçinde **Özet** ekran, o ana kadarki sağlanan tüm kurtarma yapılandırmaları bakın.</span><span class="sxs-lookup"><span data-stu-id="be712-220">In the **Summary** screen, you see all the recovery configurations provided so far.</span></span> <span data-ttu-id="be712-221">Tıklatın **kurtarmak**.</span><span class="sxs-lookup"><span data-stu-id="be712-221">Click **Recover**.</span></span>

    <span data-ttu-id="be712-222">Kurtarılan veritabanı kurtarma durumunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="be712-222">The Recovery status shows the database being recovered.</span></span> <span data-ttu-id="be712-223">Tıklayabilirsiniz **kapatmak** sihirbazı kapatın ve devam eden görüntülemek için **izleme** çalışma.</span><span class="sxs-lookup"><span data-stu-id="be712-223">You can click **Close** to close the wizard and view the progress in the **Monitoring** workspace.</span></span>

    ![Kurtarma işlemini başlatın](./media/backup-azure-backup-sql/sqlbackup-recoverying.png)

    <span data-ttu-id="be712-225">Kurtarma tamamlandıktan sonra geri yüklenen veritabanı tutarlı uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="be712-225">Once the recovery is completed, the restored database is application consistent.</span></span>

### <a name="next-steps"></a><span data-ttu-id="be712-226">Sonraki Adımlar:</span><span class="sxs-lookup"><span data-stu-id="be712-226">Next Steps:</span></span>
<span data-ttu-id="be712-227">• [Azure Backup ile ilgili SSS](backup-azure-backup-faq.md)</span><span class="sxs-lookup"><span data-stu-id="be712-227">•    [Azure Backup FAQ](backup-azure-backup-faq.md)</span></span>
