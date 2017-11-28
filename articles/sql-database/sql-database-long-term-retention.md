---
title: "aaaStore Azure SQL veritabanı yedeklemeleri için too10 yıl ayarlama | Microsoft Docs"
description: "Azure SQL veritabanı depolanmasını yedekler too10 yıl nasıl destekler? öğrenin."
keywords: 
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: 
ms.assetid: 66fdb8b8-5903-4d3a-802e-af08d204566e
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 12/22/2016
ms.author: sashan
ms.openlocfilehash: 5825ebd4e3bd66b59b13aea603d377ef814a1df3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="store-azure-sql-database-backups-for-up-too10-years"></a><span data-ttu-id="ad6bf-103">Too10 yıl yedeklemek için Azure SQL veritabanı yedeklemelerini depolamak</span><span class="sxs-lookup"><span data-stu-id="ad6bf-103">Store Azure SQL Database backups for up too10 years</span></span>
<span data-ttu-id="ad6bf-104">Birçok uygulama yasal varsa, uyumluluk ya da diğer iş amaçlı gerektiren tooretain veritabanı yedeklemeleri hello ötesinde 7-35 gün Azure SQL veritabanı tarafından sağlanan [otomatik yedeklemeler](sql-database-automated-backups.md).</span><span class="sxs-lookup"><span data-stu-id="ad6bf-104">Many applications have regulatory, compliance, or other business purposes that require you tooretain database backups beyond hello 7-35 days provided by Azure SQL Database [automatic backups](sql-database-automated-backups.md).</span></span> <span data-ttu-id="ad6bf-105">Merhaba uzun vadeli yedekleme bekletme özelliğini kullanarak, bir Azure kurtarma Hizmetleri kasasını için too10 yıl içinde SQL veritabanı yedeklerinizi depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-105">By using hello long-term backup retention feature, you can store your SQL database backups in an Azure Recovery Services vault for up too10 years.</span></span> <span data-ttu-id="ad6bf-106">Too1, kasa başına 000 veritabanlarını yedeklemek depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-106">You can store up too1,000 databases per vault.</span></span> <span data-ttu-id="ad6bf-107">Ardından herhangi bir yedekleme hello kasa toorestore seçebileceğiniz yeni bir veritabanı olarak.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-107">You then can select any backup in hello vault toorestore it as a new database.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ad6bf-108">Uzun vadeli yedekleme bekletme olduğundan şu anda önizlemede ve bölgeler aşağıdaki hello kullanılabilir: Avustralya Doğu, Avustralya Güneydoğu, Brezilya Güney, Orta ABD, Doğu Asya, Doğu ABD, Doğu ABD 2, Hindistan Orta, Hindistan Güney, Japonya Doğu, Japonya Batı, Kuzey Orta ABD, Kuzey Avrupa, Orta Güney ABD, Güneydoğu Asya, Batı Avrupa ve Batı ABD.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-108">Long-term backup retention is currently in preview and available in hello following regions: Australia East, Australia Southeast, Brazil South, Central US, East Asia, East US, East US 2, India Central, India South, Japan East, Japan West, North Central US, North Europe, South Central US, Southeast Asia, West Europe, and West US.</span></span>
>

> [!NOTE]
> <span data-ttu-id="ad6bf-109">Kasa başına too200 veritabanlarını 24 saatlik dönem boyunca etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-109">You can enable up too200 databases per vault during a 24-hour period.</span></span> <span data-ttu-id="ad6bf-110">Her sunucu toominimize hello etkisini bu sınır için ayrı bir kasa kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-110">We recommend that you use a separate vault for each server toominimize hello impact of this limit.</span></span> 
> 

## <a name="how-sql-database-long-term-backup-retention-works"></a><span data-ttu-id="ad6bf-111">SQL veritabanı uzun vadeli yedekleme bekletme nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="ad6bf-111">How SQL Database long-term backup retention works</span></span>

<span data-ttu-id="ad6bf-112">Uzun vadeli yedekleme bekletme ile bir SQL veritabanı sunucusuna Azure kurtarma Hizmetleri kasası ile ilişkilendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-112">With long-term backup retention, you can associate a SQL database server with an Azure Recovery Services vault.</span></span> 

* <span data-ttu-id="ad6bf-113">Merhaba kasası oluşturmanız gerekir hello hello SQL server oluşturulan aynı Azure aboneliği ve de aynı hello coğrafi bölge ve kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-113">You must create hello vault in hello same Azure subscription that created hello SQL server and in hello same geographic region and resource group.</span></span> 
* <span data-ttu-id="ad6bf-114">Ardından, herhangi bir veritabanı için bir bekletme ilkesi de yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-114">You then configure a retention policy for any database.</span></span> <span data-ttu-id="ad6bf-115">Hello İlkesi nedenler hello haftalık tam veritabanı yedeklemeleri toobe toohello kurtarma Hizmetleri kasası kopyalanır ve hello belirtilen saklama dönemini (too10 yıl) korunur.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-115">hello policy causes hello weekly full database backups toobe copied toohello Recovery Services vault and retained for hello specified retention period (up too10 years).</span></span> 
* <span data-ttu-id="ad6bf-116">Ardından, bu yedeklemeler tooa yeni veritabanı hello abonelik herhangi bir sunucuya birinden hello veritabanını geri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-116">You can then restore hello database from any of these backups tooa new database in any server in hello subscription.</span></span> <span data-ttu-id="ad6bf-117">Azure depolama mevcut yedeklerden bir kopyasını oluşturur ve hello kopyalama performans hello varolan veritabanı üzerinde bir etkisi yoktur.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-117">Azure storage creates a copy from existing backups, and hello copy has no performance impact on hello existing database.</span></span>

> [!TIP]
> <span data-ttu-id="ad6bf-118">Bir nasıl tooguide için bkz: [yapılandırma ve Azure SQL veritabanı uzun vadeli yedekleme bekletme geri](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="ad6bf-118">For a how-tooguide, see [Configure and restore from Azure SQL Database long-term backup retention](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="enable-long-term-backup-retention"></a><span data-ttu-id="ad6bf-119">Uzun vadeli yedekleme bekletme etkinleştir</span><span class="sxs-lookup"><span data-stu-id="ad6bf-119">Enable long-term backup retention</span></span>

<span data-ttu-id="ad6bf-120">bir veritabanı için uzun vadeli yedekleme bekletme tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="ad6bf-120">tooconfigure long-term backup retention for a database:</span></span>

1. <span data-ttu-id="ad6bf-121">Hello bir Azure kurtarma Hizmetleri kasası oluşturma, SQL veritabanı sunucusu olarak aynı bölge, abonelik ve kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-121">Create an Azure Recovery Services vault in hello same region, subscription, and resource group as your SQL database server.</span></span> 
2. <span data-ttu-id="ad6bf-122">Merhaba sunucu toohello kasaya kaydedin.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-122">Register hello server toohello vault.</span></span>
3. <span data-ttu-id="ad6bf-123">Bir Azure kurtarma Hizmetleri koruma ilkesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-123">Create an Azure Recovery Services protection policy.</span></span>
4. <span data-ttu-id="ad6bf-124">Uzun vadeli yedekleme bekletme gerektiren hello koruma İlkesi toohello veritabanları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-124">Apply hello protection policy toohello databases that require long-term backup retention.</span></span>

<span data-ttu-id="ad6bf-125">tooconfigure, Yönet'i ve bir Azure kurtarma Hizmetleri kasası Otomatik yedeklemelerin uzun vadeli yedekleme bekletme bir veritabanını geri, hello aşağıdakilerden birini yapın:</span><span class="sxs-lookup"><span data-stu-id="ad6bf-125">tooconfigure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault, do either of hello following:</span></span>

* <span data-ttu-id="ad6bf-126">Hello Azure portal kullanarak: tıklatın **uzun vadeli yedekleme bekletme**, bir veritabanı seçin ve ardından **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-126">Using hello Azure portal: Click **Long-term backup retention**, select a database, and then click **Configure**.</span></span> 

   ![Uzun vadeli yedekleme bekletme için bir veritabanı seçin](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

* <span data-ttu-id="ad6bf-128">PowerShell kullanarak: çok Git[yapılandırma ve Azure SQL veritabanı uzun vadeli yedekleme bekletme geri](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="ad6bf-128">Using PowerShell: Go too[Configure and restore from Azure SQL Database long-term backup retention](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="restore-a-database-thats-stored-with-hello-long-term-backup-retention-feature"></a><span data-ttu-id="ad6bf-129">Merhaba uzun vadeli yedekleme bekletme özelliğiyle depolanan bir veritabanını geri yükle</span><span class="sxs-lookup"><span data-stu-id="ad6bf-129">Restore a database that's stored with hello long-term backup retention feature</span></span>

<span data-ttu-id="ad6bf-130">uzun vadeli yedekleme bekletme yedekten toorecover:</span><span class="sxs-lookup"><span data-stu-id="ad6bf-130">toorecover from a long-term backup retention backup:</span></span>

1. <span data-ttu-id="ad6bf-131">Liste hello kasası hello yedekleme depolandığı.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-131">List hello vault where hello backup is stored.</span></span>
2. <span data-ttu-id="ad6bf-132">Eşlenen tooyour mantıksal sunucu listesi hello kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-132">List hello container that is mapped tooyour logical server.</span></span>
3. <span data-ttu-id="ad6bf-133">Eşlenen tooyour veritabanı hello kasa içinde listesi hello veri kaynağı.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-133">List hello data source within hello vault that is mapped tooyour database.</span></span>
4. <span data-ttu-id="ad6bf-134">Kullanılabilir toorestore listesi hello kurtarma noktalarını.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-134">List hello recovery points that are available toorestore.</span></span>
5. <span data-ttu-id="ad6bf-135">Merhaba kurtarma noktası toohello hedef sunucudan aboneliğinizi içinde Hello veritabanını geri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-135">Restore hello database from hello recovery point toohello target server within your subscription.</span></span>

<span data-ttu-id="ad6bf-136">tooconfigure, Yönet'i ve bir Azure kurtarma Hizmetleri kasası Otomatik yedeklemelerin uzun vadeli yedekleme bekletme bir veritabanını geri, hello aşağıdakilerden birini yapın:</span><span class="sxs-lookup"><span data-stu-id="ad6bf-136">tooconfigure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault, do either of hello following:</span></span>

* <span data-ttu-id="ad6bf-137">Hello Azure portal kullanarak: çok Git[hello Azure portalı Yönet uzun vadeli yedekleme bekletme kullanarak](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="ad6bf-137">Using hello Azure portal: Go too[Manage long-term backup retention using hello Azure portal](sql-database-long-term-backup-retention-configure.md).</span></span> 

* <span data-ttu-id="ad6bf-138">PowerShell kullanarak: çok Git[uzun vadeli yedekleme bekletme PowerShell kullanarak yönetme](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="ad6bf-138">Using PowerShell: Go too[Manage long-term backup retention using PowerShell](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="get-pricing-for-long-term-backup-retention"></a><span data-ttu-id="ad6bf-139">Uzun vadeli yedekleme bekletme için fiyatlandırma Al</span><span class="sxs-lookup"><span data-stu-id="ad6bf-139">Get pricing for long-term backup retention</span></span>

<span data-ttu-id="ad6bf-140">SQL veritabanı uzun vadeli yedekleme bekletme ücret toohello göre [oranları fiyatlandırma Azure yedekleme Hizmetleri](https://azure.microsoft.com/pricing/details/backup/).</span><span class="sxs-lookup"><span data-stu-id="ad6bf-140">Long-term backup retention of a SQL database is charged according toohello [Azure backup services pricing rates](https://azure.microsoft.com/pricing/details/backup/).</span></span>

<span data-ttu-id="ad6bf-141">Merhaba SQL veritabanı sunucusuna kayıtlı toohello kasası sonra hello kasasında depolanan hello haftalık yedekleri tarafından kullanılan toplam depolama hello için ücretlendirilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-141">After hello SQL database server is registered toohello vault, you are charged for hello total storage that's used by hello weekly backups stored in hello vault.</span></span>

## <a name="view-available-backups-that-are-stored-in-long-term-backup-retention"></a><span data-ttu-id="ad6bf-142">Uzun vadeli yedekleme bekletme içinde depolanan kullanılabilir yedekleri görüntüle</span><span class="sxs-lookup"><span data-stu-id="ad6bf-142">View available backups that are stored in long-term backup retention</span></span>

<span data-ttu-id="ad6bf-143">tooconfigure, Yönet'i ve hello Azure portal kullanarak bir veritabanını bir Azure kurtarma Hizmetleri kasası Otomatik yedeklemelerin uzun vadeli yedekleme bekletme geri, hello aşağıdakilerden birini yapın:</span><span class="sxs-lookup"><span data-stu-id="ad6bf-143">tooconfigure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault by using hello Azure portal, do either of hello following:</span></span>

* <span data-ttu-id="ad6bf-144">Hello Azure portal kullanarak: çok Git[hello Azure portalı Yönet uzun vadeli yedekleme bekletme kullanarak](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="ad6bf-144">Using hello Azure portal: Go too[Manage long-term backup retention using hello Azure portal](sql-database-long-term-backup-retention-configure.md).</span></span> 

* <span data-ttu-id="ad6bf-145">PowerShell kullanarak: çok Git[uzun vadeli yedekleme bekletme PowerShell kullanarak yönetme](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="ad6bf-145">Using PowerShell: Go too[Manage long-term backup retention using PowerShell](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="disable-long-term-retention"></a><span data-ttu-id="ad6bf-146">Uzun vadeli bekletme devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="ad6bf-146">Disable long-term retention</span></span>

<span data-ttu-id="ad6bf-147">Merhaba kurtarma hizmeti üzerinde bekletme ilkesi sağlanan hello bağlı olarak yedeklemeler hello temizlenmesi otomatik olarak yönetir.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-147">hello recovery service automatically handles hello cleanup of backups based on hello provided retention policy.</span></span> 

<span data-ttu-id="ad6bf-148">belirli veritabanı toohello kasa için gönderen hello yedeklemeleri toostop hello bekletme ilkesi bu veritabanı için kaldırın.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-148">toostop sending hello backups for a specific database toohello vault, remove hello retention policy for that database.</span></span>
  
```
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName 'RG1' -ServerName 'Server1' -DatabaseName 'DB1' -State 'Disabled' -ResourceId $policy.Id
```

> [!NOTE]
> <span data-ttu-id="ad6bf-149">Merhaba kasasına zaten olan hello yedeklemeleri etkilenmez.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-149">hello backups that are already in hello vault are unaffected.</span></span> <span data-ttu-id="ad6bf-150">Kendi saklama süresi sona erdiğinde, bunlar hello kurtarma hizmeti tarafından otomatik olarak silinir.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-150">They are automatically deleted by hello recovery service when their retention period expires.</span></span>

## <a name="long-term-backup-retention-faq"></a><span data-ttu-id="ad6bf-151">Uzun vadeli yedekleme bekletme SSS</span><span class="sxs-lookup"><span data-stu-id="ad6bf-151">Long-term backup retention FAQ</span></span>

<span data-ttu-id="ad6bf-152">**El ile de hello kasasında belirli yedeklemelerinize silebilmek için?**</span><span class="sxs-lookup"><span data-stu-id="ad6bf-152">**Can I manually delete specific backups in hello vault?**</span></span>

<span data-ttu-id="ad6bf-153">Şu anda değil.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-153">Not currently.</span></span> <span data-ttu-id="ad6bf-154">Merhaba saklama süresi sona erdiğinde hello kasası yedekler otomatik olarak temizlenir.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-154">hello vault automatically cleans up backups when hello retention period has expired.</span></span>

<span data-ttu-id="ad6bf-155">**My server toostore yedeklemeleri toomore bir kasa daha kayıt mi?**</span><span class="sxs-lookup"><span data-stu-id="ad6bf-155">**Can I register my server toostore backups toomore than one vault?**</span></span>

<span data-ttu-id="ad6bf-156">Hayır, aynı anda yedeklemeleri tooonly bir kasa şu anda depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-156">No, you can currently store backups tooonly one vault at a time.</span></span>

<span data-ttu-id="ad6bf-157">**Farklı Aboneliklerde kasası ve sunucu olabilir?**</span><span class="sxs-lookup"><span data-stu-id="ad6bf-157">**Can I have a vault and server in different subscriptions?**</span></span>

<span data-ttu-id="ad6bf-158">Merhaba kasası ve sunucu hello Hayır, şu anda olmalıdır aynı abonelik ve kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-158">No, currently hello vault and server must be in hello same subscription and resource group.</span></span>

<span data-ttu-id="ad6bf-159">**I my sunucunun bölgesinden farklı bir bölgede oluşturulan bir kasa kullanabilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="ad6bf-159">**Can I use a vault that I created in a region that's different from my server’s region?**</span></span>

<span data-ttu-id="ad6bf-160">Hayır, hello kasası ve sunucu olmalıdır hello aynı bölge toominimize zaman kopyalayın ve trafiği ücretlere kaçının.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-160">No, hello vault and server must be in hello same region toominimize copy time and avoid traffic charges.</span></span>

<span data-ttu-id="ad6bf-161">**Kaç tane veritabanları t bir kasaya depolayabilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="ad6bf-161">**How many databases can I store in one vault?**</span></span>

<span data-ttu-id="ad6bf-162">Şu anda too1, kasa başına 000 veritabanlarını yedeklemek destekliyoruz.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-162">Currently, we support up too1,000 databases per vault.</span></span> 

<span data-ttu-id="ad6bf-163">**Abonelik başına kaç tane kasalarını oluşturabilirim?**</span><span class="sxs-lookup"><span data-stu-id="ad6bf-163">**How many vaults can I create per subscription?**</span></span>

<span data-ttu-id="ad6bf-164">Abonelik başına too25 kasa oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-164">You can create up too25 vaults per subscription.</span></span>

<span data-ttu-id="ad6bf-165">**Kasa başına günde kaç tane veritabanları yapılandırabilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="ad6bf-165">**How many databases can I configure per day per vault?**</span></span>

<span data-ttu-id="ad6bf-166">Günde bir kasa başına 200 veritabanları ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-166">You can set up 200 databases per day per vault.</span></span>

<span data-ttu-id="ad6bf-167">**Uzun vadeli yedekleme bekletme esnek havuzları ile çalışır mı?**</span><span class="sxs-lookup"><span data-stu-id="ad6bf-167">**Does long-term backup retention work with elastic pools?**</span></span>

<span data-ttu-id="ad6bf-168">Evet.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-168">Yes.</span></span> <span data-ttu-id="ad6bf-169">Herhangi bir veritabanı hello havuzunda hello bekletme ilkesi ile yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-169">Any database in hello pool can be configured with hello retention policy.</span></span>

<span data-ttu-id="ad6bf-170">**Merhaba yedekleme oluşturulduğu hello zaman seçebilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="ad6bf-170">**Can I choose hello time at which hello backup is created?**</span></span>

<span data-ttu-id="ad6bf-171">Hayır, SQL veritabanı hello yedekleme zamanlaması toominimize hello performans etkisini veritabanlarınızı denetler.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-171">No, SQL Database controls hello backup schedule toominimize hello performance impact on your databases.</span></span>

<span data-ttu-id="ad6bf-172">**Saydam veri şifreleme için veritabanı etkin var. Bunu hello kasayla kullanabilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="ad6bf-172">**I have transparent data encryption enabled for my database. Can I use it with hello vault?**</span></span> 

<span data-ttu-id="ad6bf-173">Evet, saydam veri şifreleme desteklenir.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-173">Yes, transparent data encryption is supported.</span></span> <span data-ttu-id="ad6bf-174">Merhaba özgün veritabanı artık mevcut olsa bile hello kasadan hello veritabanını geri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-174">You can restore hello database from hello vault even if hello original database no longer exists.</span></span>

<span data-ttu-id="ad6bf-175">**Aboneliğimi askıya alınırsa hello kasasında hello yedeklemeleri ile ne olur?**</span><span class="sxs-lookup"><span data-stu-id="ad6bf-175">**What happens with hello backups in hello vault if my subscription is suspended?**</span></span> 

<span data-ttu-id="ad6bf-176">Aboneliğiniz askıya alınırsa hello varolan veritabanları ve yedeklemeleri korur.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-176">If your subscription is suspended, we retain hello existing databases and backups.</span></span> <span data-ttu-id="ad6bf-177">Yeni yedeklemeler kopyalanan toohello kasası olup olmadığı.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-177">New backups are not copied toohello vault.</span></span> <span data-ttu-id="ad6bf-178">Merhaba aboneliği yeniden sonra hello hizmet yedeklemeleri toohello kasası kopyalama devam eder.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-178">After you reactivate hello subscription, hello service resumes copying backups toohello vault.</span></span> <span data-ttu-id="ad6bf-179">Kasanızı hello abonelik askıya alınmadan önce var. kopyalanan hello yedeklemeler kullanarak erişilebilir toohello geri yükleme işlemleri olur.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-179">Your vault becomes accessible toohello restore operations by using hello backups that were copied there before hello subscription was suspended.</span></span> 

<span data-ttu-id="ad6bf-180">**I indirin veya toohello SQL server geri toohello SQL veritabanı yedekleme dosyaları erişim alabilirim?**</span><span class="sxs-lookup"><span data-stu-id="ad6bf-180">**Can I get access toohello SQL database backup files so I can download or restore them toohello SQL server?**</span></span>

<span data-ttu-id="ad6bf-181">Hayır, şu anda.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-181">No, not currently.</span></span>

<span data-ttu-id="ad6bf-182">**Olası toohave olan birden çok, bir SQL bekletme ilkesi içinde (günlük, haftalık, aylık, Yıllık) zamanlar.**</span><span class="sxs-lookup"><span data-stu-id="ad6bf-182">**Is it possible toohave multiple schedules (daily, weekly, monthly, yearly) within a SQL retention policy.**</span></span>

<span data-ttu-id="ad6bf-183">Hayır, birden çok zamanlamaları, yalnızca sanal makine yedeklemeler için şu anda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-183">No, multiple schedules are currently available only for virtual machine backups.</span></span>

<span data-ttu-id="ad6bf-184">**Ne biz uzun vadeli yedekleme bekletme aktif coğrafi çoğaltma ikincil veritabanı bir veritabanı üzerinde ayarlama?**</span><span class="sxs-lookup"><span data-stu-id="ad6bf-184">**What if we set up long-term backup retention on a database that is an active geo-replication secondary database?**</span></span>

<span data-ttu-id="ad6bf-185">Biz yedeklemeleri çoğaltmaları yok tuttuğundan, da şu anda ikincil veritabanlarında uzun vadeli yedekleme bekletme için bir seçenek yoktur.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-185">Because we don't take backups on replicas, there is currently no option for long-term backup retention on secondary databases.</span></span> <span data-ttu-id="ad6bf-186">Ancak, bu nedenle kullanıcılar tooset aktif coğrafi çoğaltma ikincil veritabanında uzun vadeli yedekleme bekletme ayarlama önemlidir:</span><span class="sxs-lookup"><span data-stu-id="ad6bf-186">However, it is important for users tooset up long-term backup retention on an active geo-replication secondary database for these reasons:</span></span>
* <span data-ttu-id="ad6bf-187">Bir yük devretme olur ve bir birincil veritabanı hello veritabanı hale biz tam karşıya yüklenen toovault olduğu yedekleme, alın.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-187">When a failover happens and hello database becomes a primary database, we take a full backup, which is uploaded toovault.</span></span>
* <span data-ttu-id="ad6bf-188">Hiçbir ek yok uzun vadeli yedekleme bekletme ikincil bir veritabanı üzerinde ayarlamak için maliyet toohello müşteri.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-188">There is no extra cost toohello customer for setting up long-term backup retention on a secondary database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad6bf-189">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ad6bf-189">Next steps</span></span>
<span data-ttu-id="ad6bf-190">Veritabanı Yedeklemeleri yanlışlıkla Bozulması veya silinmesi verileri korumak için herhangi bir iş sürekliliği ve olağanüstü durum kurtarma stratejiniz temel parçası oldukları.</span><span class="sxs-lookup"><span data-stu-id="ad6bf-190">Because database backups protect data from accidental corruption or deletion, they're an essential part of any business continuity and disaster recovery strategy.</span></span> <span data-ttu-id="ad6bf-191">toolearn hakkında diğer SQL veritabanı iş sürekliliği çözümleri Merhaba, bkz: [iş sürekliliğine genel bakış](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="ad6bf-191">toolearn about hello other SQL Database business-continuity solutions, see [Business continuity overview](sql-database-business-continuity.md).</span></span>
