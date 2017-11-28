---
title: "birden çok Azure SQL veritabanı aaaRun analytics sorguları | Microsoft Docs"
description: "Analytics veritabanına çevrimdışı analiz için Kiracı veritabanlarından veri ayıklamak"
keywords: "sql veritabanı öğreticisi"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: billgib; sstein
ms.openlocfilehash: f2664e4aafd2fecc98d20d229342bca19b0b08c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="extract-data-from-tenant-databases-into-an-analytics-database-for-offline-analysis"></a><span data-ttu-id="4f040-104">Analytics veritabanına çevrimdışı analiz için Kiracı veritabanlarından veri ayıklamak</span><span class="sxs-lookup"><span data-stu-id="4f040-104">Extract data from tenant databases into an analytics database for offline analysis</span></span>

<span data-ttu-id="4f040-105">Bu öğreticide, her bir kiracı veritabanını bir esnek iş toorun sorguları kullanın.</span><span class="sxs-lookup"><span data-stu-id="4f040-105">In this tutorial, you use an elastic job toorun queries against each tenant database.</span></span> <span data-ttu-id="4f040-106">Merhaba iş bilet satış verileri ayıklar ve çözümleme için bir analytics veritabanı (veya veri ambarı) yükler.</span><span class="sxs-lookup"><span data-stu-id="4f040-106">hello job extracts ticket sales data and loads it into an analytics database (or data warehouse) for analysis.</span></span> <span data-ttu-id="4f040-107">Merhaba Analizi veritabanı ise tüm kiracılar, bu günlük işletimsel verilerden tooextract Öngörüler sorgulanan.</span><span class="sxs-lookup"><span data-stu-id="4f040-107">hello analytics database is then queried tooextract insights from this day-to-day operational data of all tenants.</span></span>


<span data-ttu-id="4f040-108">Bu öğreticide şunların nasıl yapıldığını öğrenirsiniz:</span><span class="sxs-lookup"><span data-stu-id="4f040-108">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4f040-109">Merhaba Kiracı analytics veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4f040-109">Create hello tenant analytics database</span></span>
> * <span data-ttu-id="4f040-110">Zamanlanmış iş tooretrieve veri oluşturun ve hello analytics veritabanını doldurma</span><span class="sxs-lookup"><span data-stu-id="4f040-110">Create a scheduled job tooretrieve data and populate hello analytics database</span></span>

<span data-ttu-id="4f040-111">Bu öğretici, Önkoşullar aşağıdaki yapma emin hello karşılanmadığı toocomplete:</span><span class="sxs-lookup"><span data-stu-id="4f040-111">toocomplete this tutorial, make sure hello following prerequisites are met:</span></span>

* <span data-ttu-id="4f040-112">Merhaba Wingtip SaaS uygulaması dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="4f040-112">hello Wingtip SaaS app is deployed.</span></span> <span data-ttu-id="4f040-113">beş dakikadan kısa toodeploy bakın [dağıtma ve Merhaba Wingtip SaaS uygulaması keşfedin.](sql-database-saas-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="4f040-113">toodeploy in less than five minutes, see [Deploy and explore hello Wingtip SaaS application](sql-database-saas-tutorial.md)</span></span>
* <span data-ttu-id="4f040-114">Azure PowerShell’in yüklendiğinden.</span><span class="sxs-lookup"><span data-stu-id="4f040-114">Azure PowerShell is installed.</span></span> <span data-ttu-id="4f040-115">Ayrıntılar için bkz. [Azure PowerShell’i kullanmaya başlama](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span><span class="sxs-lookup"><span data-stu-id="4f040-115">For details, see [Getting started with Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span></span>
* <span data-ttu-id="4f040-116">Merhaba SQL Server Management Studio (SSMS) en son sürümü yüklü.</span><span class="sxs-lookup"><span data-stu-id="4f040-116">hello latest version of SQL Server Management Studio (SSMS) is installed.</span></span> [<span data-ttu-id="4f040-117">SSMS’yi İndirin ve Yükleyin</span><span class="sxs-lookup"><span data-stu-id="4f040-117">Download and Install SSMS</span></span>](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

## <a name="tenant-operational-analytics-pattern"></a><span data-ttu-id="4f040-118">Kiracı İşlem Analizi düzeni</span><span class="sxs-lookup"><span data-stu-id="4f040-118">Tenant Operational Analytics pattern</span></span>

<span data-ttu-id="4f040-119">SaaS uygulamaları ile Merhaba harika fırsatları hello bulutta depolanan toouse hello zengin Kiracı veri biridir.</span><span class="sxs-lookup"><span data-stu-id="4f040-119">One of hello great opportunities with SaaS applications is toouse hello rich tenant data that is stored in hello cloud.</span></span> <span data-ttu-id="4f040-120">Bu veri toogain fikir hello işlemi ve uygulamanızı ve kiracılarınızın kullanımı için kullanın.</span><span class="sxs-lookup"><span data-stu-id="4f040-120">Use this data toogain insights into hello operation and usage of your application, and your tenants.</span></span> <span data-ttu-id="4f040-121">Bu veriler özelliği development, kullanılabilirlik yenilikleri ve diğer hello uygulama ve platform yatırım yönlendirebilir.</span><span class="sxs-lookup"><span data-stu-id="4f040-121">This data can guide feature development, usability improvements, and other investments in hello app and platform.</span></span> <span data-ttu-id="4f040-122">Tek bir çok kiracılı veritabanında olduğunda bu verilere erişmek kolaydır, ancak binlerce veritabanında büyük ölçekli olarak dağıtıldığında çok kolay değildir.</span><span class="sxs-lookup"><span data-stu-id="4f040-122">Accessing this data when it's in a single multi-tenant database is easy, but not so easy when distributed at scale across potentially thousands of databases.</span></span> <span data-ttu-id="4f040-123">Bir yaklaşım tooaccessing Bu, sorgu sonuçlarından sonucu döndürerek bir çıktı veritabanı ve tablo yakalanan iş yürütme toobe etkinleştirmek toouse esnek iş verilerdir.</span><span class="sxs-lookup"><span data-stu-id="4f040-123">One approach tooaccessing this data is toouse Elastic jobs, which enable result-returning query results from job execution toobe captured in an output database and table.</span></span>

## <a name="get-hello-wingtip-application-scripts"></a><span data-ttu-id="4f040-124">Merhaba Wingtip uygulama komut dosyaları alma</span><span class="sxs-lookup"><span data-stu-id="4f040-124">Get hello Wingtip application scripts</span></span>

<span data-ttu-id="4f040-125">Merhaba Wingtip SaaS komut dosyaları ve uygulama kaynak koduna hello kullanılabilir [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github depo.</span><span class="sxs-lookup"><span data-stu-id="4f040-125">hello Wingtip SaaS scripts and application source code are available in hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github repo.</span></span> <span data-ttu-id="4f040-126">[Adımları toodownload hello Wingtip SaaS betikleri](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).</span><span class="sxs-lookup"><span data-stu-id="4f040-126">[Steps toodownload hello Wingtip SaaS scripts](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).</span></span>

## <a name="deploy-a-database-for-tenant-analytics-results"></a><span data-ttu-id="4f040-127">Kiracı analiz sonuçları için bir veritabanı dağıtma</span><span class="sxs-lookup"><span data-stu-id="4f040-127">Deploy a database for tenant analytics results</span></span>

<span data-ttu-id="4f040-128">Bu öğretici bir veritabanı dağıtılan toocapture hello sonuçları döndüren sorgular içeren komut dosyası iş yürütme sonuçları toohave gerektirir.</span><span class="sxs-lookup"><span data-stu-id="4f040-128">This tutorial requires you toohave a database deployed toocapture hello results from job execution of scripts, which contain results-returning queries.</span></span> <span data-ttu-id="4f040-129">Bu amaçla tenantanalytics adlı bir veritabanı oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="4f040-129">Let's create a database called tenantanalytics for this purpose.</span></span>

1. <span data-ttu-id="4f040-130">Aç... \\Öğrenme modülleri\\işletimsel Analytics\\Kiracı Analytics\\*Demo TenantAnalyticsDB.ps1* hello içinde *PowerShell ISE* ve ayarlayın Aşağıdaki değeri hello:</span><span class="sxs-lookup"><span data-stu-id="4f040-130">Open …\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*Demo-TenantAnalyticsDB.ps1* in hello *PowerShell ISE* and set hello following value:</span></span>
   * <span data-ttu-id="4f040-131">**$DemoScenario** = **2** *İşlem analizi veritabanını dağıtma*</span><span class="sxs-lookup"><span data-stu-id="4f040-131">**$DemoScenario** = **2** *Deploy operational analytics database*</span></span>
1. <span data-ttu-id="4f040-132">Tuşuna **F5** toorun hello tanıtım betiği (Bu çağrıları hello *dağıtma TenantAnalyticsDB.ps1* komut dosyası) hello Kiracı analytics veritabanı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4f040-132">Press **F5** toorun hello demo script (that calls hello *Deploy-TenantAnalyticsDB.ps1* script) which creates hello tenant analytics database.</span></span>

## <a name="create-some-data-for-hello-demo"></a><span data-ttu-id="4f040-133">Merhaba gösteri için bazı veriler oluşturun</span><span class="sxs-lookup"><span data-stu-id="4f040-133">Create some data for hello demo</span></span>

1. <span data-ttu-id="4f040-134">Aç... \\Öğrenme modülleri\\işletimsel Analytics\\Kiracı Analytics\\*Demo TenantAnalyticsDB.ps1* hello içinde *PowerShell ISE* ve ayarlayın Aşağıdaki değeri hello:</span><span class="sxs-lookup"><span data-stu-id="4f040-134">Open …\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*Demo-TenantAnalyticsDB.ps1* in hello *PowerShell ISE* and set hello following value:</span></span>
   * <span data-ttu-id="4f040-135">**$DemoScenario** = **1** *Tüm mekanlardaki etkinlikler için bilet satın alma*</span><span class="sxs-lookup"><span data-stu-id="4f040-135">**$DemoScenario** = **1** *Purchase tickets for events at all venues*</span></span>
1. <span data-ttu-id="4f040-136">Tuşuna **F5** toorun hello komut dosyası ve geçmiş satın bileti oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4f040-136">Press **F5** toorun hello script and create ticket purchasing history.</span></span>


## <a name="create-a-scheduled-job-tooretrieve-tenant-analytics-about-ticket-purchases"></a><span data-ttu-id="4f040-137">Zamanlanmış iş tooretrieve Kiracı analytics bilet satın alma işlemleri hakkında oluşturma</span><span class="sxs-lookup"><span data-stu-id="4f040-137">Create a scheduled job tooretrieve tenant analytics about ticket purchases</span></span>

<span data-ttu-id="4f040-138">Bu komut dosyası iş tooretrieve bilet satın alma bilgileri tüm kiracılardan oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4f040-138">This script creates a job tooretrieve ticket purchase information from all tenants.</span></span> <span data-ttu-id="4f040-139">Tek bir tabloya toplanan sonra bilet desenleri hello kiracılar arasında satın alma hakkında zengin ayrıntılı ölçümler elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4f040-139">Once aggregated into a single table, you can gain rich insightful metrics about ticket purchasing patterns across hello tenants.</span></span>

1. <span data-ttu-id="4f040-140">SSMS açmak ve toohello katalog -&lt;kullanıcı&gt;. database.windows.net sunucu</span><span class="sxs-lookup"><span data-stu-id="4f040-140">Open SSMS and connect toohello catalog-&lt;user&gt;.database.windows.net server</span></span>
1. <span data-ttu-id="4f040-141">...\\Öğrenme Modülleri\\İşlem Analizi\\Kiracı Analizleri\\*TicketPurchasesfromAllTenants.sql*’i açın</span><span class="sxs-lookup"><span data-stu-id="4f040-141">Open ...\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*TicketPurchasesfromAllTenants.sql*</span></span>
1. <span data-ttu-id="4f040-142">Değiştirme &lt;kullanıcı&gt;, hello kullanıcı adını kullan hello betik hello üstündeki hello Wingtip SaaS uygulama dağıtıldığında kullanılan **sp\_ekleme\_hedef\_grup\_üye** ve **sp\_ekleme\_iş**</span><span class="sxs-lookup"><span data-stu-id="4f040-142">Modify &lt;User&gt;, use hello user name used when you deployed hello Wingtip SaaS app at hello top of hello script, **sp\_add\_target\_group\_member** and **sp\_add\_jobstep**</span></span>
1. <span data-ttu-id="4f040-143">Sağ tıklayın, seçin **bağlantı**ve toohello katalog - bağlanmak&lt;kullanıcı&gt;. database.windows.net sunucusu zaten bağlıysa,</span><span class="sxs-lookup"><span data-stu-id="4f040-143">Right click, select **Connection**, and connect toohello catalog-&lt;User&gt;.database.windows.net server, if not already connected</span></span>
1. <span data-ttu-id="4f040-144">Bağlı toohello olduğundan emin olun **jobaccount** veritabanı ve tuşuna **F5** hello komut dosyasını çalıştırmak için</span><span class="sxs-lookup"><span data-stu-id="4f040-144">Ensure you are connected toohello **jobaccount** database and press **F5** to run hello script</span></span>

* <span data-ttu-id="4f040-145">**SP\_ekleme\_hedef\_grup** hello hedef grup adı oluşturur *TenantGroup*, tooadd hedef üyeleri ihtiyacımız artık.</span><span class="sxs-lookup"><span data-stu-id="4f040-145">**sp\_add\_target\_group** creates hello target group name *TenantGroup*, now we need tooadd target members.</span></span>
* <span data-ttu-id="4f040-146">**SP\_ekleme\_hedef\_grup\_üye** ekler bir *server* hedef sunucu (Bu hello customer1 - Not içindeki tüm veritabanları uymak açısından gerekli olduğunu üye türü &lt;Kullanıcı&gt; hello Kiracı veritabanları içeren sunucu) hello işinde işi aynı anda yürütme bulunması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4f040-146">**sp\_add\_target\_group\_member** adds a *server* target member type, which deems all databases within that server (note this is hello customer1-&lt;User&gt; server containing hello tenant databases) at time of job execution should be included in hello job.</span></span>
* <span data-ttu-id="4f040-147">**sp\_add\_job**, “Tüm Kiracıların Bilet Satın Alma İşlemleri” adında yeni bir haftalık olarak zamanlanmış iş oluşturur</span><span class="sxs-lookup"><span data-stu-id="4f040-147">**sp\_add\_job** creates a new weekly scheduled job called “Ticket Purchases from all Tenants”</span></span>
* <span data-ttu-id="4f040-148">**SP\_ekleme\_iş** hello işi adımı T-SQL komut metni tooretrieve içeren tüm hello bilet satın alma bilgileri tüm kiracılar ve sonuç olarak adlandırılan bir tabloya kümesini döndüren kopyalama hello oluşturur  *AllTicketsPurchasesfromAllTenants*</span><span class="sxs-lookup"><span data-stu-id="4f040-148">**sp\_add\_jobstep** creates hello job step containing T-SQL command text tooretrieve all hello ticket purchase information from all tenants and copy hello returning result set into a table called *AllTicketsPurchasesfromAllTenants*</span></span>
* <span data-ttu-id="4f040-149">Merhaba kalan görünümleri hello komut hello varlığını hello nesneleri ve izleme iş yürütme görüntüler.</span><span class="sxs-lookup"><span data-stu-id="4f040-149">hello remaining views in hello script display hello existence of hello objects and monitor job execution.</span></span> <span data-ttu-id="4f040-150">Gözden hello durum hello değerinden **yaşam döngüsü** sütun toomonitor hello durumu.</span><span class="sxs-lookup"><span data-stu-id="4f040-150">Review hello status value from hello **lifecycle** column toomonitor hello status.</span></span> <span data-ttu-id="4f040-151">Bir kez, başarılı, hello işi tüm Kiracı veritabanları başarıyla tamamlandı ve hello hello içeren iki ek veritabanları başvuru tablosu.</span><span class="sxs-lookup"><span data-stu-id="4f040-151">Once, Succeeded, hello job has successfully finished on all tenant databases and hello two additional databases containing hello reference table.</span></span>

<span data-ttu-id="4f040-152">Başarılı bir şekilde hello betiğini çalıştırmaya benzer sonuçlarında neden olur:</span><span class="sxs-lookup"><span data-stu-id="4f040-152">Successfully running hello script should result in similar results:</span></span>

![sonuçlar](media/sql-database-saas-tutorial-tenant-analytics/ticket-purchases-job.png)

## <a name="create-a-job-tooretrieve-a-summary-count-of-ticket-purchases-from-all-tenants"></a><span data-ttu-id="4f040-154">Bilet Özet sayısını tüm kiracılardan satın alma işi tooretrieve oluşturma</span><span class="sxs-lookup"><span data-stu-id="4f040-154">Create a job tooretrieve a summary count of ticket purchases from all tenants</span></span>

<span data-ttu-id="4f040-155">Bu komut tüm bilet satın alma işi tooretrieve toplamı tüm kiracılardan oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4f040-155">This script creates a job tooretrieve sum of all ticket purchases from all tenants.</span></span>

1. <span data-ttu-id="4f040-156">SSMS açmak ve toohello *katalog -&lt;kullanıcı&gt;. database.windows.net* sunucu</span><span class="sxs-lookup"><span data-stu-id="4f040-156">Open SSMS and connect toohello *catalog-&lt;User&gt;.database.windows.net* server</span></span>
1. <span data-ttu-id="4f040-157">Açık hello dosyası... \\Modülleri öğrenme\\sağlamak ve Katalog\\işletimsel Analytics\\Kiracı Analytics\\*sonuçları TicketPurchasesfromAllTenants.sql*</span><span class="sxs-lookup"><span data-stu-id="4f040-157">Open hello file …\\Learning Modules\\Provision and Catalog\\Operational Analytics\\Tenant Analytics\\*Results-TicketPurchasesfromAllTenants.sql*</span></span>
1. <span data-ttu-id="4f040-158">Değiştirme &lt;kullanıcı&gt;, hello kullanıcı adını kullan hello kodda hello hello Wingtip SaaS uygulama dağıtıldığında kullanılan **sp\_ekleme\_iş** saklı yordamı</span><span class="sxs-lookup"><span data-stu-id="4f040-158">Modify &lt;User&gt;, use hello user name used when you deployed hello Wingtip SaaS app in hello script, in hello **sp\_add\_jobstep** stored procedure</span></span>
1. <span data-ttu-id="4f040-159">Sağ tıklayın, seçin **bağlantı**ve toohello katalog - bağlanmak&lt;kullanıcı&gt;. database.windows.net sunucusu zaten bağlıysa,</span><span class="sxs-lookup"><span data-stu-id="4f040-159">Right click, select **Connection**, and connect toohello catalog-&lt;User&gt;.database.windows.net server, if not already connected</span></span>
1. <span data-ttu-id="4f040-160">Bağlı toohello olduğundan emin olun **tenantanalytics** veritabanı ve tuşuna **F5** hello komut dosyasını çalıştırmak için</span><span class="sxs-lookup"><span data-stu-id="4f040-160">Ensure you are connected toohello **tenantanalytics** database and press **F5** to run hello script</span></span>

<span data-ttu-id="4f040-161">Başarılı bir şekilde hello betiğini çalıştırmaya benzer sonuçlarında neden olur:</span><span class="sxs-lookup"><span data-stu-id="4f040-161">Successfully running hello script should result in similar results:</span></span>

![sonuçlar](media/sql-database-saas-tutorial-tenant-analytics/total-sales.png)



* <span data-ttu-id="4f040-163">**sp\_add\_job**, “ResultsTicketsOrders” adında yeni bir haftalık zamanlanmış iş oluşturur</span><span class="sxs-lookup"><span data-stu-id="4f040-163">**sp\_add\_job** creates a new weekly scheduled job called “ResultsTicketsOrders”</span></span>

* <span data-ttu-id="4f040-164">**SP\_ekleme\_iş** hello işi adımı T-SQL komut metni tooretrieve içeren tüm kiracılar ve CountofTicketOrders adlı bir tabloya ayarlamak sonucu döndürerek kopyalama hello tüm hello bilet satın alma bilgileri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4f040-164">**sp\_add\_jobstep** creates hello job step containing T-SQL command text tooretrieve all hello ticket purchase information from all tenants and copy hello returning result set into a table called CountofTicketOrders</span></span>

* <span data-ttu-id="4f040-165">Merhaba kalan görünümleri hello komut hello varlığını hello nesneleri ve izleme iş yürütme görüntüler.</span><span class="sxs-lookup"><span data-stu-id="4f040-165">hello remaining views in hello script display hello existence of hello objects and monitor job execution.</span></span> <span data-ttu-id="4f040-166">Gözden hello durum hello değerinden **yaşam döngüsü** sütun toomonitor hello durumu.</span><span class="sxs-lookup"><span data-stu-id="4f040-166">Review hello status value from hello **lifecycle** column toomonitor hello status.</span></span> <span data-ttu-id="4f040-167">Bir kez, başarılı, hello işi tüm Kiracı veritabanları başarıyla tamamlandı ve hello hello içeren iki ek veritabanları başvuru tablosu.</span><span class="sxs-lookup"><span data-stu-id="4f040-167">Once, Succeeded, hello job has successfully finished on all tenant databases and hello two additional databases containing hello reference table.</span></span>


## <a name="next-steps"></a><span data-ttu-id="4f040-168">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4f040-168">Next steps</span></span>

<span data-ttu-id="4f040-169">Bu öğreticide, şunları öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="4f040-169">In this tutorial you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4f040-170">Kiracı analiz veritabanını dağıtma</span><span class="sxs-lookup"><span data-stu-id="4f040-170">Deploy a tenant analytics database</span></span>
> * <span data-ttu-id="4f040-171">Zamanlanmış iş tooretrieve analitik veri kiracılar arasında oluşturma</span><span class="sxs-lookup"><span data-stu-id="4f040-171">Create a scheduled job tooretrieve analytical data across tenants</span></span>

<span data-ttu-id="4f040-172">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="4f040-172">Congratulations!</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4f040-173">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="4f040-173">Additional resources</span></span>

* <span data-ttu-id="4f040-174">Ek [hello Wingtip SaaS uygulamasına yapı öğreticileri](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span><span class="sxs-lookup"><span data-stu-id="4f040-174">Additional [tutorials that build upon hello Wingtip SaaS application](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span></span>
* [<span data-ttu-id="4f040-175">Esnek İşler</span><span class="sxs-lookup"><span data-stu-id="4f040-175">Elastic Jobs</span></span>](sql-database-elastic-jobs-overview.md)
