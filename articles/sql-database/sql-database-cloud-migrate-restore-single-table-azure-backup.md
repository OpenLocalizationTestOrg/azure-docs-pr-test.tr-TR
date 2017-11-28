---
title: "Azure SQL veritabanı yedeğinden tek bir tabloyu aaaRestore | Microsoft Docs"
description: "Nasıl toorestore tek bir tablo Azure SQL veritabanı yedeğinden öğrenin."
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: 340b41bd-9df8-47fb-adfc-03216de38a5e
ms.service: sql-database
ms.custom: business continuity
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: 696d2ac87a70bccdf063bfecb8255723404aa5bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorestore-a-single-table-from-an-azure-sql-database-backup"></a><span data-ttu-id="10774-103">Nasıl toorestore tek bir tablo bir Azure SQL veritabanı yedeğinden</span><span class="sxs-lookup"><span data-stu-id="10774-103">How toorestore a single table from an Azure SQL Database backup</span></span>
<span data-ttu-id="10774-104">İçinde yanlışlıkla bir SQL veritabanında bazı verileri değiştiren bir durum karşılaşabilirsiniz ve şimdi toorecover hello tek etkilenen tablo istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="10774-104">You may encounter a situation in which you accidentally modified some data in a SQL database and now you want toorecover hello single affected table.</span></span> <span data-ttu-id="10774-105">Tek bir nasıl toorestore tablo hello SQL veritabanı birinden bir veritabanında bu makalede [otomatik yedeklemeler](sql-database-automated-backups.md).</span><span class="sxs-lookup"><span data-stu-id="10774-105">This article describes how toorestore a single table in a database from one of hello SQL Database [automatic backups](sql-database-automated-backups.md).</span></span>

## <a name="preparation-steps-rename-hello-table-and-restore-a-copy-of-hello-database"></a><span data-ttu-id="10774-106">Hazırlık adımları: hello tablo yeniden adlandırın ve hello veritabanının bir kopyasını geri yükleme</span><span class="sxs-lookup"><span data-stu-id="10774-106">Preparation steps: Rename hello table and restore a copy of hello database</span></span>
1. <span data-ttu-id="10774-107">Azure SQL veritabanınızı geri hello kopyayla tooreplace istediğiniz Hello tabloda tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="10774-107">Identify hello table in your Azure SQL database that you want tooreplace with hello restored copy.</span></span> <span data-ttu-id="10774-108">Microsoft SQL Management Studio'yu toorename hello tabloyu kullanın.</span><span class="sxs-lookup"><span data-stu-id="10774-108">Use Microsoft SQL Management Studio toorename hello table.</span></span> <span data-ttu-id="10774-109">Örneğin, hello tablo olarak yeniden adlandırın &lt;tablo adı&gt;_old.</span><span class="sxs-lookup"><span data-stu-id="10774-109">For example, rename hello table as &lt;table name&gt;_old.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="10774-110">engellenme, tooavoid adlandırdığınız hello tablo üzerinde çalışan herhangi bir etkinlik olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="10774-110">tooavoid being blocked, make sure that there's no activity running on hello table that you are renaming.</span></span> <span data-ttu-id="10774-111">Sorunlarla karşılaşırsanız, bir bakım penceresi sırasında bu yordamı gerçekleştirmek emin olun.</span><span class="sxs-lookup"><span data-stu-id="10774-111">If you encounter issues, make sure that perform this procedure during a maintenance window.</span></span>
   >

2. <span data-ttu-id="10774-112">Veritabanı tooa noktasının toorecover toousing hello istediğiniz zaman bir yedeğini geri [noktası-In_Time geri](sql-database-recovery-using-backups.md#point-in-time-restore) adımları.</span><span class="sxs-lookup"><span data-stu-id="10774-112">Restore a backup of your database tooa point in time that you want toorecover toousing hello [Point-In_Time Restore](sql-database-recovery-using-backups.md#point-in-time-restore) steps.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="10774-113">Merhaba geri hello veritabanının adını hello DBName + zaman damgası biçimde olacaktır; Örneğin, **Adventureworks2012_2016-01-01T22-12Z**.</span><span class="sxs-lookup"><span data-stu-id="10774-113">hello name of hello restored database will be in hello DBName+TimeStamp format; for example, **Adventureworks2012_2016-01-01T22-12Z**.</span></span> <span data-ttu-id="10774-114">Bu adım hello varolan bir veritabanı adı hello sunucuda üzerine değildir.</span><span class="sxs-lookup"><span data-stu-id="10774-114">This step doesn't overwrite hello existing database name on hello server.</span></span> <span data-ttu-id="10774-115">Bu bir güvenlik önlemi ve amaçlıdır tooallow, tooverify hello geri veritabanı önce geçerli kendi veritabanını bırakın ve üretim kullanımı için geri hello veritabanını yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="10774-115">This is a safety measure, and it's intended tooallow you tooverify hello restored database before they drop their current database and rename hello restored database for production use.</span></span>
   
## <a name="copying-hello-table-from-hello-restored-database-by-using-hello-sql-database-migration-tool"></a><span data-ttu-id="10774-116">Merhaba SQL veritabanı geçiş aracını kullanarak veritabanı hello kopyalama hello tablosundan geri</span><span class="sxs-lookup"><span data-stu-id="10774-116">Copying hello table from hello restored database by using hello SQL Database Migration tool</span></span>

1. <span data-ttu-id="10774-117">Merhaba yükleyip [SQL veritabanı Geçiş Sihirbazı'nı](https://sqlazuremw.codeplex.com).</span><span class="sxs-lookup"><span data-stu-id="10774-117">Download and install hello [SQL Database Migration Wizard](https://sqlazuremw.codeplex.com).</span></span>
2. <span data-ttu-id="10774-118">Merhaba hello SQL veritabanı Geçiş Sihirbazı'nı Aç **seçin işlem** sayfasında, seçin **Çözümle/geçirme altında veritabanına**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="10774-118">Open hello SQL Database Migration Wizard, on hello **Select Process** page, select **Database under Analyze/Migrate**, and then click **Next**.</span></span>

   ![SQL veritabanı Geçiş Sihirbazı - işlemi seçin](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/1.png)

3. <span data-ttu-id="10774-120">Merhaba, **tooServer bağlanmak** iletişim kutusunda, ayarları aşağıdaki hello Uygula:</span><span class="sxs-lookup"><span data-stu-id="10774-120">In hello **Connect tooServer** dialog box, apply hello following settings:</span></span>

   * <span data-ttu-id="10774-121">Sunucu adı: **bilgisayarınızı SQL server**</span><span class="sxs-lookup"><span data-stu-id="10774-121">Server name: **Your SQL server**</span></span>
   * <span data-ttu-id="10774-122">Kimlik doğrulaması: **SQL Server kimlik doğrulaması**</span><span class="sxs-lookup"><span data-stu-id="10774-122">Authentication: **SQL Server Authentication**</span></span>
   * <span data-ttu-id="10774-123">Oturum açma: **, oturum açma**</span><span class="sxs-lookup"><span data-stu-id="10774-123">Login: **Your login**</span></span>
   * <span data-ttu-id="10774-124">Parola: **parolanızı**</span><span class="sxs-lookup"><span data-stu-id="10774-124">Password: **Your password**</span></span>
   * <span data-ttu-id="10774-125">Veritabanı: **Master DB'de (tüm veritabanlarını listeler)**</span><span class="sxs-lookup"><span data-stu-id="10774-125">Database: **Master DB (List all databases)**</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="10774-126">Varsayılan olarak, oturum açma bilgilerinizi hello sihirbaz kaydeder.</span><span class="sxs-lookup"><span data-stu-id="10774-126">By default hello wizard saves your login information.</span></span> <span data-ttu-id="10774-127">Kendisine istemiyorsanız belirleyin **unutursanız oturum açma bilgilerini**.</span><span class="sxs-lookup"><span data-stu-id="10774-127">If you don't want it to, select **Forget Login Information**.</span></span>
   >
   
     ![SQL veritabanı Geçiş Sihirbazı - Kaynak Seç - adım 1](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/2.png)
4. <span data-ttu-id="10774-129">Merhaba, **Kaynağı Seç** iletişim kutusu, geri select hello veritabanı hello adından **hazırlık adımları** bölümünde, kaynağı olarak ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="10774-129">In hello **Select Source** dialog box, select hello restored database name from hello **Preparation steps** section as your source, and then click **Next**.</span></span>
   
    ![SQL veritabanı Geçiş Sihirbazı - Kaynak Seç - adım 2](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/3.png)
5. <span data-ttu-id="10774-131">Merhaba, **seçin nesneleri** iletişim kutusu, select hello **belirli veritabanı nesneleri seçin** seçeneğini ve ardından hello table(or tables) toomigrate toohello hedef sunucu istediğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="10774-131">In hello **Choose Objects** dialog box, select hello **Select specific database objects** option, and then select hello table(or tables) that you want toomigrate toohello target server.</span></span>
   <span data-ttu-id="10774-132">![SQL veritabanı Geçiş Sihirbazı - nesneleri seçin](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/4.png)</span><span class="sxs-lookup"><span data-stu-id="10774-132">![SQL Database Migration wizard - Choose Objects](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/4.png)</span></span>
6. <span data-ttu-id="10774-133">Merhaba üzerinde **komut dosyası Sihirbazı Özet** sayfasında, **Evet** sorulduğunda hazır toogenerate bir SQL betiği olmanıza hakkında.</span><span class="sxs-lookup"><span data-stu-id="10774-133">On hello **Script Wizard Summary** page, click **Yes** when you’re prompted about whether you’re ready toogenerate a SQL script.</span></span> <span data-ttu-id="10774-134">Ayrıca, daha sonra kullanmak için hello seçeneği toosave hello TSQL komut dosyası vardır.</span><span class="sxs-lookup"><span data-stu-id="10774-134">You also have hello option toosave hello TSQL Script for later use.</span></span>
   <span data-ttu-id="10774-135">![SQL veritabanı Geçiş Sihirbazı - komut dosyası Sihirbazı Özeti](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/5.png)</span><span class="sxs-lookup"><span data-stu-id="10774-135">![SQL Database Migration wizard - Script Wizard Summary](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/5.png)</span></span>
7. <span data-ttu-id="10774-136">Merhaba üzerinde **sonuç özeti** sayfasında, **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="10774-136">On hello **Results Summary** page, click **Next**.</span></span>
   <span data-ttu-id="10774-137">![SQL veritabanı Geçiş Sihirbazı - sonuç özeti](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/6.png)</span><span class="sxs-lookup"><span data-stu-id="10774-137">![SQL Database Migration wizard - Results Summary](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/6.png)</span></span>
8. <span data-ttu-id="10774-138">Merhaba üzerinde **Kurulum hedef sunucu bağlantısı** sayfasında, **tooServer bağlanmak**ve ardından aşağıdaki gibi hello ayrıntıları girin:</span><span class="sxs-lookup"><span data-stu-id="10774-138">On hello **Setup Target Server Connection** page, click **Connect tooServer**, and then enter hello details as follows:</span></span>
   
   * <span data-ttu-id="10774-139">**Sunucu adı**: hedef sunucu örneği</span><span class="sxs-lookup"><span data-stu-id="10774-139">**Server Name**: Target server instance</span></span>
   * <span data-ttu-id="10774-140">**Kimlik doğrulama**: **SQL Server kimlik doğrulaması**.</span><span class="sxs-lookup"><span data-stu-id="10774-140">**Authentication**: **SQL Server authentication**.</span></span> <span data-ttu-id="10774-141">Oturum açma kimlik bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="10774-141">Enter your login credentials.</span></span>
   * <span data-ttu-id="10774-142">**Veritabanı**: **Master DB'de (tüm veritabanları liste)**.</span><span class="sxs-lookup"><span data-stu-id="10774-142">**Database**: **Master DB (List all databases)**.</span></span> <span data-ttu-id="10774-143">Bu seçenek hello hedef sunucu üzerindeki tüm hello veritabanlarını listeler.</span><span class="sxs-lookup"><span data-stu-id="10774-143">This option lists all hello databases on hello target server.</span></span>
     
     ![SQL veritabanı Geçiş Sihirbazı - Kurulum hedef sunucu bağlantısı](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/7.png)
9. <span data-ttu-id="10774-145">Tıklatın **Bağlan**seçin toomove hello tabloya istediğiniz ve ardından hello hedef veritabanı **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="10774-145">Click **Connect**, select hello target database that you want toomove hello table to, and then click **Next**.</span></span> <span data-ttu-id="10774-146">Bu daha önce oluşturulan hello betik çalıştıran tamamlanmalıdır ve hello yeni tablo kopyalanan toohello hedef veritabanının taşınır görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="10774-146">This should finish running hello previously generated script, and you should see hello newly moved table copied toohello target database.</span></span>

## <a name="verification-step"></a><span data-ttu-id="10774-147">Doğrulama adımı</span><span class="sxs-lookup"><span data-stu-id="10774-147">Verification step</span></span>

- <span data-ttu-id="10774-148">Sorgu ve test hello yeni tablo toomake hello veri sağlam olduğundan emin kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="10774-148">Query and test hello newly copied table toomake sure that hello data is intact.</span></span> <span data-ttu-id="10774-149">Onaylama sonra yeniden adlandırılmış hello tablo formuna düşürebilir **hazırlık adımları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="10774-149">Upon confirmation, you can drop hello renamed table form **Preparation steps** section.</span></span> <span data-ttu-id="10774-150">(örneğin, &lt;tablo adı&gt;_old).</span><span class="sxs-lookup"><span data-stu-id="10774-150">(for example, &lt;table name&gt;_old).</span></span>

## <a name="next-steps"></a><span data-ttu-id="10774-151">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="10774-151">Next steps</span></span>
[<span data-ttu-id="10774-152">SQL veritabanı otomatik yedekleme</span><span class="sxs-lookup"><span data-stu-id="10774-152">SQL Database automatic backups</span></span>](sql-database-automated-backups.md)

