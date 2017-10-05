---
title: "Birden çok Azure SQL veritabanına göre analiz sorguları çalıştırma | Microsoft Docs"
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
ms.openlocfilehash: 4e32407d5f321198358e07980907c3420aaf56c6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="extract-data-from-tenant-databases-into-an-analytics-database-for-offline-analysis"></a><span data-ttu-id="8a544-104">Analytics veritabanına çevrimdışı analiz için Kiracı veritabanlarından veri ayıklamak</span><span class="sxs-lookup"><span data-stu-id="8a544-104">Extract data from tenant databases into an analytics database for offline analysis</span></span>

<span data-ttu-id="8a544-105">Bu öğreticide, her Kiracı veritabanına karşı sorguları çalıştırmak için esnek bir işi kullanın.</span><span class="sxs-lookup"><span data-stu-id="8a544-105">In this tutorial, you use an elastic job to run queries against each tenant database.</span></span> <span data-ttu-id="8a544-106">İş bilet satış verileri ayıklar ve çözümleme için bir analytics veritabanı (veya veri ambarı) yükler.</span><span class="sxs-lookup"><span data-stu-id="8a544-106">The job extracts ticket sales data and loads it into an analytics database (or data warehouse) for analysis.</span></span> <span data-ttu-id="8a544-107">Analytics veritabanı sonra tüm kiracılar bu günlük işletimsel verilerden öngörüleri ayıklamak için sorgulanır.</span><span class="sxs-lookup"><span data-stu-id="8a544-107">The analytics database is then queried to extract insights from this day-to-day operational data of all tenants.</span></span>


<span data-ttu-id="8a544-108">Bu öğreticide şunların nasıl yapıldığını öğrenirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8a544-108">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8a544-109">Kiracı analiz veritabanını oluşturma</span><span class="sxs-lookup"><span data-stu-id="8a544-109">Create the tenant analytics database</span></span>
> * <span data-ttu-id="8a544-110">Verileri almak ve analiz veritabanını doldurmak için zamanlanmış bir iş oluşturma</span><span class="sxs-lookup"><span data-stu-id="8a544-110">Create a scheduled job to retrieve data and populate the analytics database</span></span>

<span data-ttu-id="8a544-111">Bu öğreticiyi tamamlamak için aşağıdaki ön koşulların karşılandığından emin olun:</span><span class="sxs-lookup"><span data-stu-id="8a544-111">To complete this tutorial, make sure the following prerequisites are met:</span></span>

* <span data-ttu-id="8a544-112">Wingtip SaaS uygulaması dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="8a544-112">The Wingtip SaaS app is deployed.</span></span> <span data-ttu-id="8a544-113">Beş dakikadan daha kısa bir süre içinde dağıtmak için bkz: [dağıtma ve Wingtip SaaS uygulamasına keşfedin.](sql-database-saas-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="8a544-113">To deploy in less than five minutes, see [Deploy and explore the Wingtip SaaS application](sql-database-saas-tutorial.md)</span></span>
* <span data-ttu-id="8a544-114">Azure PowerShell’in yüklendiğinden.</span><span class="sxs-lookup"><span data-stu-id="8a544-114">Azure PowerShell is installed.</span></span> <span data-ttu-id="8a544-115">Ayrıntılar için bkz. [Azure PowerShell’i kullanmaya başlama](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span><span class="sxs-lookup"><span data-stu-id="8a544-115">For details, see [Getting started with Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span></span>
* <span data-ttu-id="8a544-116">SQL Server Management Studio’nun (SSMS) en son sürümünün yüklendiğinden.</span><span class="sxs-lookup"><span data-stu-id="8a544-116">The latest version of SQL Server Management Studio (SSMS) is installed.</span></span> [<span data-ttu-id="8a544-117">SSMS’yi İndirin ve Yükleyin</span><span class="sxs-lookup"><span data-stu-id="8a544-117">Download and Install SSMS</span></span>](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

## <a name="tenant-operational-analytics-pattern"></a><span data-ttu-id="8a544-118">Kiracı İşlem Analizi düzeni</span><span class="sxs-lookup"><span data-stu-id="8a544-118">Tenant Operational Analytics pattern</span></span>

<span data-ttu-id="8a544-119">SaaS uygulamalarının sunduğu harika fırsatlardan biri de bulutta depolanan zengin kiracı verilerini kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="8a544-119">One of the great opportunities with SaaS applications is to use the rich tenant data that is stored in the cloud.</span></span> <span data-ttu-id="8a544-120">Uygulamanızın çalışması ve kullanımının yanı sıra kiracılarınızla ilgili bilgi edinmek için bu verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="8a544-120">Use this data to gain insights into the operation and usage of your application, and your tenants.</span></span> <span data-ttu-id="8a544-121">Bu veriler, uygulama ve platform için yapılan özellik geliştirmeleri, kullanılabilirlik iyileştirmeleri ve diğer yatırımlar için rehberlik sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="8a544-121">This data can guide feature development, usability improvements, and other investments in the app and platform.</span></span> <span data-ttu-id="8a544-122">Tek bir çok kiracılı veritabanında olduğunda bu verilere erişmek kolaydır, ancak binlerce veritabanında büyük ölçekli olarak dağıtıldığında çok kolay değildir.</span><span class="sxs-lookup"><span data-stu-id="8a544-122">Accessing this data when it's in a single multi-tenant database is easy, but not so easy when distributed at scale across potentially thousands of databases.</span></span> <span data-ttu-id="8a544-123">Bu verilere erişmenin bir yolu Esnek işleri kullanmaktır. Bu işler, işin yürütüldüğünde sonuç döndüren sorgu sonuçlarının bir çıkış veritabanında ve tabloda yakalanmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="8a544-123">One approach to accessing this data is to use Elastic jobs, which enable result-returning query results from job execution to be captured in an output database and table.</span></span>

## <a name="get-the-wingtip-application-scripts"></a><span data-ttu-id="8a544-124">Wingtip uygulama betiklerini alma</span><span class="sxs-lookup"><span data-stu-id="8a544-124">Get the Wingtip application scripts</span></span>

<span data-ttu-id="8a544-125">Wingtip SaaS komut dosyalarını ve uygulama kaynak koduna kullanılabilir olan [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github depo.</span><span class="sxs-lookup"><span data-stu-id="8a544-125">The Wingtip SaaS scripts and application source code are available in the [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github repo.</span></span> <span data-ttu-id="8a544-126">[Wingtip SaaS komut dosyalarını karşıdan yüklemek için adımları](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).</span><span class="sxs-lookup"><span data-stu-id="8a544-126">[Steps to download the Wingtip SaaS scripts](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).</span></span>

## <a name="deploy-a-database-for-tenant-analytics-results"></a><span data-ttu-id="8a544-127">Kiracı analiz sonuçları için bir veritabanı dağıtma</span><span class="sxs-lookup"><span data-stu-id="8a544-127">Deploy a database for tenant analytics results</span></span>

<span data-ttu-id="8a544-128">Bu öğreticide, sonuç döndüren sorgular içeren betiklerin iş yürütme sonuçlarını almak amacıyla bir veritabanını dağıtmanız gerekmektedir.</span><span class="sxs-lookup"><span data-stu-id="8a544-128">This tutorial requires you to have a database deployed to capture the results from job execution of scripts, which contain results-returning queries.</span></span> <span data-ttu-id="8a544-129">Bu amaçla tenantanalytics adlı bir veritabanı oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="8a544-129">Let's create a database called tenantanalytics for this purpose.</span></span>

1. <span data-ttu-id="8a544-130">*PowerShell ISE*’de …\\Öğrenme Modülleri\\İşlem Analizi\\Kiracı Analizleri\\*Demo-TenantAnalyticsDB.ps1*’i açın ve aşağıdaki değeri ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="8a544-130">Open …\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*Demo-TenantAnalyticsDB.ps1* in the *PowerShell ISE* and set the following value:</span></span>
   * <span data-ttu-id="8a544-131">**$DemoScenario** = **2** *İşlem analizi veritabanını dağıtma*</span><span class="sxs-lookup"><span data-stu-id="8a544-131">**$DemoScenario** = **2** *Deploy operational analytics database*</span></span>
1. <span data-ttu-id="8a544-132">Kiracı analiz veritabanını oluşturan tanıtım betiğini (*Deploy-TenantAnalyticsDB.ps1* betiğini çağırır) çalıştırmak için **F5**’e basın.</span><span class="sxs-lookup"><span data-stu-id="8a544-132">Press **F5** to run the demo script (that calls the *Deploy-TenantAnalyticsDB.ps1* script) which creates the tenant analytics database.</span></span>

## <a name="create-some-data-for-the-demo"></a><span data-ttu-id="8a544-133">Tanıtım için bazı veriler oluşturma</span><span class="sxs-lookup"><span data-stu-id="8a544-133">Create some data for the demo</span></span>

1. <span data-ttu-id="8a544-134">*PowerShell ISE*’de …\\Öğrenme Modülleri\\İşlem Analizi\\Kiracı Analizleri\\*Demo-TenantAnalyticsDB.ps1*’i açın ve aşağıdaki değeri ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="8a544-134">Open …\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*Demo-TenantAnalyticsDB.ps1* in the *PowerShell ISE* and set the following value:</span></span>
   * <span data-ttu-id="8a544-135">**$DemoScenario** = **1** *Tüm mekanlardaki etkinlikler için bilet satın alma*</span><span class="sxs-lookup"><span data-stu-id="8a544-135">**$DemoScenario** = **1** *Purchase tickets for events at all venues*</span></span>
1. <span data-ttu-id="8a544-136">Betiği çalıştırmak ve bilet satın alma geçmişini oluşturmak için **F5**’e basın.</span><span class="sxs-lookup"><span data-stu-id="8a544-136">Press **F5** to run the script and create ticket purchasing history.</span></span>


## <a name="create-a-scheduled-job-to-retrieve-tenant-analytics-about-ticket-purchases"></a><span data-ttu-id="8a544-137">Bilet satın alma işlemleri hakkındaki kiracı analizini almak için zamanlanmış bir iş oluşturma</span><span class="sxs-lookup"><span data-stu-id="8a544-137">Create a scheduled job to retrieve tenant analytics about ticket purchases</span></span>

<span data-ttu-id="8a544-138">Bu betik, tüm kiracılardan bilet satın alma bilgilerini almak için bir iş oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8a544-138">This script creates a job to retrieve ticket purchase information from all tenants.</span></span> <span data-ttu-id="8a544-139">Tek bir tabloda toplandıklarında, kiracıların bilet satın alma düzenleri hakkında zengin bilgiler içeren ölçümler elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8a544-139">Once aggregated into a single table, you can gain rich insightful metrics about ticket purchasing patterns across the tenants.</span></span>

1. <span data-ttu-id="8a544-140">SSMS’yi açın ve catalog-&lt;user&gt;.database.windows.net sunucusuna bağlanın</span><span class="sxs-lookup"><span data-stu-id="8a544-140">Open SSMS and connect to the catalog-&lt;user&gt;.database.windows.net server</span></span>
1. <span data-ttu-id="8a544-141">...\\Öğrenme Modülleri\\İşlem Analizi\\Kiracı Analizleri\\*TicketPurchasesfromAllTenants.sql*’i açın</span><span class="sxs-lookup"><span data-stu-id="8a544-141">Open ...\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*TicketPurchasesfromAllTenants.sql*</span></span>
1. <span data-ttu-id="8a544-142">Değiştirme &lt;kullanıcı&gt;, betik üstündeki Wingtip SaaS uygulama dağıtıldığında kullanılan kullanıcı adı kullan **sp\_ekleme\_hedef\_grup\_üye** ve **sp\_ekleme\_iş**</span><span class="sxs-lookup"><span data-stu-id="8a544-142">Modify &lt;User&gt;, use the user name used when you deployed the Wingtip SaaS app at the top of the script, **sp\_add\_target\_group\_member** and **sp\_add\_jobstep**</span></span>
1. <span data-ttu-id="8a544-143">Sağ tıklayın, seçin **bağlantı**ve Katalog için bağlantı&lt;kullanıcı&gt;. database.windows.net sunucusu zaten bağlıysa,</span><span class="sxs-lookup"><span data-stu-id="8a544-143">Right click, select **Connection**, and connect to the catalog-&lt;User&gt;.database.windows.net server, if not already connected</span></span>
1. <span data-ttu-id="8a544-144">**jobaccount** veritabanına bağlandığınızdan emin olun ve betiği çalıştırmak için **F5**’e basın</span><span class="sxs-lookup"><span data-stu-id="8a544-144">Ensure you are connected to the **jobaccount** database and press **F5** to run the script</span></span>

* <span data-ttu-id="8a544-145">**sp\_add\_target\_group**, *TenantGroup* hedef grubu adını oluşturur, artık hedef üyeleri eklememiz gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="8a544-145">**sp\_add\_target\_group** creates the target group name *TenantGroup*, now we need to add target members.</span></span>
* <span data-ttu-id="8a544-146">**SP\_ekleme\_hedef\_grup\_üye** ekler bir *server* hedef sunucu (Bu customer1Notiçindekitümveritabanlarıuymakaçısındangerekliolduğunuüyetürü&lt; Kullanıcı&gt; server Kiracı veritabanları içeren) işi aynı anda işi yürütme eklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="8a544-146">**sp\_add\_target\_group\_member** adds a *server* target member type, which deems all databases within that server (note this is the customer1-&lt;User&gt; server containing the tenant databases) at time of job execution should be included in the job.</span></span>
* <span data-ttu-id="8a544-147">**sp\_add\_job**, “Tüm Kiracıların Bilet Satın Alma İşlemleri” adında yeni bir haftalık olarak zamanlanmış iş oluşturur</span><span class="sxs-lookup"><span data-stu-id="8a544-147">**sp\_add\_job** creates a new weekly scheduled job called “Ticket Purchases from all Tenants”</span></span>
* <span data-ttu-id="8a544-148">**sp\_add\_jobstep**, tüm kiracıların bilet satın almayla ilgili tüm bilgilerini almak ve dönen sonuç kümesini *AllTicketsPurchasesfromAllTenants* adlı bir tabloya kopyalamak için T-SQL komut metnini içeren iş adımını oluşturur</span><span class="sxs-lookup"><span data-stu-id="8a544-148">**sp\_add\_jobstep** creates the job step containing T-SQL command text to retrieve all the ticket purchase information from all tenants and copy the returning result set into a table called *AllTicketsPurchasesfromAllTenants*</span></span>
* <span data-ttu-id="8a544-149">Betikteki kalan görünümler, nesnelerin varlığını gösterir ve işin yürütülüşünü izler.</span><span class="sxs-lookup"><span data-stu-id="8a544-149">The remaining views in the script display the existence of the objects and monitor job execution.</span></span> <span data-ttu-id="8a544-150">Durumu izlemek için **yaşam döngüsü** sütunundaki durum değerini gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="8a544-150">Review the status value from the **lifecycle** column to monitor the status.</span></span> <span data-ttu-id="8a544-151">İşin başarılı olması, tüm kiracı veritabanlarında ve başvuru tablosunu içeren iki ek veritabanında başarıyla tamamlandığı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="8a544-151">Once, Succeeded, the job has successfully finished on all tenant databases and the two additional databases containing the reference table.</span></span>

<span data-ttu-id="8a544-152">Betiğin başarıyla çalıştırılması, şuna benzer sonuçlar sağlamalıdır:</span><span class="sxs-lookup"><span data-stu-id="8a544-152">Successfully running the script should result in similar results:</span></span>

![sonuçlar](media/sql-database-saas-tutorial-tenant-analytics/ticket-purchases-job.png)

## <a name="create-a-job-to-retrieve-a-summary-count-of-ticket-purchases-from-all-tenants"></a><span data-ttu-id="8a544-154">Tüm kiracılardan bilet satın alma işlemlerinin özet sayımını almak için bir iş oluşturma</span><span class="sxs-lookup"><span data-stu-id="8a544-154">Create a job to retrieve a summary count of ticket purchases from all tenants</span></span>

<span data-ttu-id="8a544-155">Bu betik, tüm kiracılardan bilet satın alma işlemlerinin özetini almak için bir iş oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8a544-155">This script creates a job to retrieve sum of all ticket purchases from all tenants.</span></span>

1. <span data-ttu-id="8a544-156">SSMS’yi açın ve *catalog-&lt;User&gt;.database.windows.net* sunucusuna bağlanın</span><span class="sxs-lookup"><span data-stu-id="8a544-156">Open SSMS and connect to the *catalog-&lt;User&gt;.database.windows.net* server</span></span>
1. <span data-ttu-id="8a544-157">…\\Öğrenme Modülleri\\Sağlama ve Katalog Oluşturma\\İşlem Analizi\\Kiracı Analizleri\\*Results-TicketPurchasesfromAllTenants.sql* dosyasını açın</span><span class="sxs-lookup"><span data-stu-id="8a544-157">Open the file …\\Learning Modules\\Provision and Catalog\\Operational Analytics\\Tenant Analytics\\*Results-TicketPurchasesfromAllTenants.sql*</span></span>
1. <span data-ttu-id="8a544-158">Değiştirme &lt;kullanıcı&gt;, içinde betik Wingtip SaaS uygulama dağıtıldığında kullanılan kullanıcı adı kullan **sp\_ekleme\_iş** saklı yordamı</span><span class="sxs-lookup"><span data-stu-id="8a544-158">Modify &lt;User&gt;, use the user name used when you deployed the Wingtip SaaS app in the script, in the **sp\_add\_jobstep** stored procedure</span></span>
1. <span data-ttu-id="8a544-159">Sağ tıklayın, seçin **bağlantı**ve Katalog için bağlantı&lt;kullanıcı&gt;. database.windows.net sunucusu zaten bağlıysa,</span><span class="sxs-lookup"><span data-stu-id="8a544-159">Right click, select **Connection**, and connect to the catalog-&lt;User&gt;.database.windows.net server, if not already connected</span></span>
1. <span data-ttu-id="8a544-160">**tenantanalytics** veritabanına bağlandığınızdan emin olun ve betiği çalıştırmak için **F5**’e basın</span><span class="sxs-lookup"><span data-stu-id="8a544-160">Ensure you are connected to the **tenantanalytics** database and press **F5** to run the script</span></span>

<span data-ttu-id="8a544-161">Betiğin başarıyla çalıştırılması, şuna benzer sonuçlar sağlamalıdır:</span><span class="sxs-lookup"><span data-stu-id="8a544-161">Successfully running the script should result in similar results:</span></span>

![sonuçlar](media/sql-database-saas-tutorial-tenant-analytics/total-sales.png)



* <span data-ttu-id="8a544-163">**sp\_add\_job**, “ResultsTicketsOrders” adında yeni bir haftalık zamanlanmış iş oluşturur</span><span class="sxs-lookup"><span data-stu-id="8a544-163">**sp\_add\_job** creates a new weekly scheduled job called “ResultsTicketsOrders”</span></span>

* <span data-ttu-id="8a544-164">**sp\_add\_jobstep**, tüm kiracıların bilet satın almayla ilgili tüm bilgilerini almak ve dönen sonuç kümesini CountofTicketOrders adlı bir tabloya kopyalamak için T-SQL komut metnini içeren iş adımını oluşturur</span><span class="sxs-lookup"><span data-stu-id="8a544-164">**sp\_add\_jobstep** creates the job step containing T-SQL command text to retrieve all the ticket purchase information from all tenants and copy the returning result set into a table called CountofTicketOrders</span></span>

* <span data-ttu-id="8a544-165">Betikteki kalan görünümler, nesnelerin varlığını gösterir ve işin yürütülüşünü izler.</span><span class="sxs-lookup"><span data-stu-id="8a544-165">The remaining views in the script display the existence of the objects and monitor job execution.</span></span> <span data-ttu-id="8a544-166">Durumu izlemek için **yaşam döngüsü** sütunundaki durum değerini gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="8a544-166">Review the status value from the **lifecycle** column to monitor the status.</span></span> <span data-ttu-id="8a544-167">İşin başarılı olması, tüm kiracı veritabanlarında ve başvuru tablosunu içeren iki ek veritabanında başarıyla tamamlandığı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="8a544-167">Once, Succeeded, the job has successfully finished on all tenant databases and the two additional databases containing the reference table.</span></span>


## <a name="next-steps"></a><span data-ttu-id="8a544-168">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8a544-168">Next steps</span></span>

<span data-ttu-id="8a544-169">Bu öğreticide, şunları öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="8a544-169">In this tutorial you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8a544-170">Kiracı analiz veritabanını dağıtma</span><span class="sxs-lookup"><span data-stu-id="8a544-170">Deploy a tenant analytics database</span></span>
> * <span data-ttu-id="8a544-171">Kiracılar genelinde analiz verilerini almak için zamanlanmış bir iş oluşturma</span><span class="sxs-lookup"><span data-stu-id="8a544-171">Create a scheduled job to retrieve analytical data across tenants</span></span>

<span data-ttu-id="8a544-172">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="8a544-172">Congratulations!</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8a544-173">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="8a544-173">Additional resources</span></span>

* <span data-ttu-id="8a544-174">Ek [Wingtip SaaS uygulamasına yapı öğreticileri](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span><span class="sxs-lookup"><span data-stu-id="8a544-174">Additional [tutorials that build upon the Wingtip SaaS application](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span></span>
* [<span data-ttu-id="8a544-175">Esnek İşler</span><span class="sxs-lookup"><span data-stu-id="8a544-175">Elastic Jobs</span></span>](sql-database-elastic-jobs-overview.md)
