---
title: "Azure SQL Data Warehouse veritabanlarında yönetme | Microsoft Docs"
description: "SQL veri ambarı veritabanlarını yönetmeye genel bakış. Yönetim Araçları, Dwu ve sorgu performansı, iyi bir güvenlik ilkeleri oluşturma ve veri bozulması veya bölgesel bir kesintinin bir veritabanını geri yükleme sorunlarını giderme genişleme performans içerir."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 8576fdb3-71fe-4b3b-a4e0-5e8a7f148acf
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: b14d0aad5a1f50c225391dbab27ec6240423a65a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-databases-in-azure-sql-data-warehouse"></a><span data-ttu-id="afda5-104">Azure SQL Data Warehouse veritabanlarında yönetme</span><span class="sxs-lookup"><span data-stu-id="afda5-104">Manage databases in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="afda5-105">SQL veri ambarı veritabanlarınızı yönetme birçok nokta otomatikleştirir.</span><span class="sxs-lookup"><span data-stu-id="afda5-105">SQL Data Warehouse automates many aspects of managing your databases.</span></span> <span data-ttu-id="afda5-106">Örneğin, performans ölçeklendirmek için ayarlamak ve işlem kaynaklarını doğru düzeyde için ödeme ve SQL Data Warehouse ölçeğini genişletme ve geri ölçeklendirme tüm yapması izin vermek yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="afda5-106">For example, to scale performance you only need to adjust and pay for the right level of compute resources, and then let SQL Data Warehouse do all the work of scaling out and scaling back.</span></span>

<span data-ttu-id="afda5-107">Kuşkusuz yanı sıra performans gereksinimlerinizi belirlemek için uzun süre çalışan sorgularda sorun giderme, iş yükünü izlemek isteyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="afda5-107">You will undoubtedly want to monitor your workload to identify your performance needs as well as troubleshoot long-running queries.</span></span> <span data-ttu-id="afda5-108">Kullanıcı ve oturum açma izinlerini yönetmek için birkaç güvenlik görevlerini gerçekleştirmek gerekir.</span><span class="sxs-lookup"><span data-stu-id="afda5-108">You will also need to perform a few security tasks to manage permissions for users and logins.</span></span>

<span data-ttu-id="afda5-109">Bu genel bakışta bu yönlerini SQL veri ambarı yönetimi ele alınmaktadır.</span><span class="sxs-lookup"><span data-stu-id="afda5-109">This overview covers these aspects of managing SQL Data Warehouse.</span></span>

* <span data-ttu-id="afda5-110">Yönetim araçları</span><span class="sxs-lookup"><span data-stu-id="afda5-110">Management tools</span></span>
* <span data-ttu-id="afda5-111">Bilgi işlem</span><span class="sxs-lookup"><span data-stu-id="afda5-111">Scale Compute</span></span>
* <span data-ttu-id="afda5-112">Duraklatma ve sürdürme</span><span class="sxs-lookup"><span data-stu-id="afda5-112">Pause and Resume</span></span>
* <span data-ttu-id="afda5-113">Performansı en iyi uygulamalar</span><span class="sxs-lookup"><span data-stu-id="afda5-113">Performance Best Practices</span></span>
* <span data-ttu-id="afda5-114">Sorgu izlemesi</span><span class="sxs-lookup"><span data-stu-id="afda5-114">Query Monitoring</span></span>
* <span data-ttu-id="afda5-115">Güvenlik</span><span class="sxs-lookup"><span data-stu-id="afda5-115">Security</span></span>
* <span data-ttu-id="afda5-116">Yedekleme ve geri yükleme</span><span class="sxs-lookup"><span data-stu-id="afda5-116">Backup and restore</span></span>

## <a name="management-tools"></a><span data-ttu-id="afda5-117">Yönetim araçları</span><span class="sxs-lookup"><span data-stu-id="afda5-117">Management tools</span></span>
<span data-ttu-id="afda5-118">SQL Data Warehouse veritabanlarında yönetmek için çeşitli araçları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="afda5-118">You can use a variety of tools to manage databases in SQL Data Warehouse.</span></span> <span data-ttu-id="afda5-119">Veritabanları yönetirken, yapmanız gereken görevinin her türü için aracı Tercihler geliştireceksiniz.</span><span class="sxs-lookup"><span data-stu-id="afda5-119">As you manage databases, you will develop tool preferences for each type of task you need to perform.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="afda5-120">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="afda5-120">Azure portal</span></span>
<span data-ttu-id="afda5-121">[Azure portal] [ Azure portal] burada oluşturabilir, güncelleştirme ve veritabanlarını silin ve veritabanı kaynaklarını izleme web tabanlı portal değil.</span><span class="sxs-lookup"><span data-stu-id="afda5-121">The [Azure portal][Azure portal] is a web-based portal where you can create, update, and delete databases and monitor database resources.</span></span> <span data-ttu-id="afda5-122">Bu harika bir araçtır yalnızca veri ambarı veritabanlarını, az sayıda yönetme Azure ile çalışmaya Başlarken veya hızlı bir şekilde bir şey yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="afda5-122">This tool is great is if you're just getting started with Azure, managing a small number of data warehouse databases, or need to quickly do something.</span></span>

<span data-ttu-id="afda5-123">Azure portalı ile çalışmaya başlamak için bkz: [SQL veri ambarı (Azure portalı) oluşturma][Create a SQL Data Warehouse (Azure portal)].</span><span class="sxs-lookup"><span data-stu-id="afda5-123">To get started with the Azure portal, see [Create a SQL Data Warehouse (Azure portal)][Create a SQL Data Warehouse (Azure portal)].</span></span>

### <a name="sql-server-data-tools-in-visual-studio"></a><span data-ttu-id="afda5-124">SQL Server veri araçları Visual Studio</span><span class="sxs-lookup"><span data-stu-id="afda5-124">SQL Server Data Tools in Visual Studio</span></span>
<span data-ttu-id="afda5-125">[SQL Server veri Araçları] [ SQL Server Data Tools] (SSDT) Visual Studio için bağlanmanıza olanak sağlayan yönetmek ve veritabanlarınızı geliştirin.</span><span class="sxs-lookup"><span data-stu-id="afda5-125">[SQL Server Data Tools][SQL Server Data Tools] (SSDT) in Visual Studio allows you to connect to, manage, and develop your databases.</span></span> <span data-ttu-id="afda5-126">Bir uygulama geliştiricisi Visual Studio'ya veya diğer tümleşik geliştirme ortamlarını (IDE) hakkında bilgi sahibi değilseniz, Visual Studio'da SSDT kullanmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="afda5-126">If you're an application developer familiar with Visual Studio or other integrated development environments (IDEs), try using SSDT in Visual Studio.</span></span>

<span data-ttu-id="afda5-127">SSDT görselleştirme, bağlanmak ve SQL Data Warehouse veritabanlarında komut dosyaları yürütme olanak tanıyan SQL Server Nesne Gezgini içerir.</span><span class="sxs-lookup"><span data-stu-id="afda5-127">SSDT includes the SQL Server Object Explorer which enables you to visualize, connect, and execute scripts against SQL Data Warehouse databases.</span></span> <span data-ttu-id="afda5-128">Hızlı bir şekilde SQL veri ambarı'na bağlanmak için basitçe tıklayabilirsiniz **Visual Studio'da Aç** ne zaman veritabanı görüntüleme Azure Klasik Portalı'nda ayrıntıları çubuğu komut düğmesi.</span><span class="sxs-lookup"><span data-stu-id="afda5-128">To quickly connect to SQL Data Warehouse, you can simply click the **Open in Visual Studio** button in the command bar when viewing the database details in the Azure Classic Portal.</span></span>  

<span data-ttu-id="afda5-129">Visual Studio'da SSDT ile çalışmaya başlamak için bkz: [sorgu Azure SQL Data Warehouse Visual Studio ile][Query Azure SQL Data Warehouse with Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="afda5-129">To get started with SSDT in Visual Studio, see [Query Azure SQL Data Warehouse with Visual Studio][Query Azure SQL Data Warehouse with Visual Studio].</span></span>

### <a name="command-line-tools"></a><span data-ttu-id="afda5-130">Komut satırı araçları</span><span class="sxs-lookup"><span data-stu-id="afda5-130">Command-line tools</span></span>
<span data-ttu-id="afda5-131">Komut satırı araçlarını, iş yüklerini otomatikleştirmek için idealdir.</span><span class="sxs-lookup"><span data-stu-id="afda5-131">Command line tools are ideal for automating your workloads.</span></span>  <span data-ttu-id="afda5-132">PowerShell ve sqlcmd işlemlerinizi otomatikleştirmek için iki harika yöntemleridir.</span><span class="sxs-lookup"><span data-stu-id="afda5-132">PowerShell and sqlcmd are two great ways to automate your processes.</span></span>  <span data-ttu-id="afda5-133">Çok sayıda mantıksal sunucuları yönetme ve gerekli görevleri komut dosyası ve daha sonra otomatik olarak kaynak değişiklikleri bir üretim ortamında dağıtmak için bu araçları öneririz.</span><span class="sxs-lookup"><span data-stu-id="afda5-133">We recommend these tools for managing a large number of logical servers and deploying resource changes in a production environment as the tasks necessary can be scripted and then automated.</span></span>

### <a name="dynamic-management-views"></a><span data-ttu-id="afda5-134">Dinamik Yönetim görünümlerini</span><span class="sxs-lookup"><span data-stu-id="afda5-134">Dynamic management views</span></span>
<span data-ttu-id="afda5-135">Dmv'leri SQL veri ambarını yönetme ekmek ve ezmesi ' dir.</span><span class="sxs-lookup"><span data-stu-id="afda5-135">DMVs are the bread and butter of managing SQL Data Warehouse.</span></span> <span data-ttu-id="afda5-136">Portalda ortaya çıkarır neredeyse tüm bilgi üzerinde Dmv'leri kullanır.</span><span class="sxs-lookup"><span data-stu-id="afda5-136">Almost all information that surfaces in the portal relies on DMVs.</span></span> <span data-ttu-id="afda5-137">SQL veri ambarı Dmv'leri listesini görmek için bkz: [SQL veri ambarı sistem görünümleri][SQL Data Warehouse system views].</span><span class="sxs-lookup"><span data-stu-id="afda5-137">To see a list of SQL Data Warehouse DMVs, see [SQL Data Warehouse system views][SQL Data Warehouse system views].</span></span>

<span data-ttu-id="afda5-138">Başlamak için bkz: [bağlanma ve sorgu sqlcmd ile][Connect and query with sqlcmd], ve [veritabanı (PowerShell) oluşturma][Create a database (PowerShell)].</span><span class="sxs-lookup"><span data-stu-id="afda5-138">To get started, see [Connect and query with sqlcmd][Connect and query with sqlcmd], and [Create a database (PowerShell)][Create a database (PowerShell)].</span></span>

## <a name="scale-compute"></a><span data-ttu-id="afda5-139">Bilgi işlem</span><span class="sxs-lookup"><span data-stu-id="afda5-139">Scale compute</span></span>
<span data-ttu-id="afda5-140">SQL veri ambarı'nda performans out veya geri artırarak veya azaltarak işlem kaynakları CPU, bellek ve g/ç bant genişliği tarafından hızlı bir şekilde ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="afda5-140">In SQL Data Warehouse, you can quickly scale performance out or back by increasing or decreasing compute resources of CPU, memory, and I/O bandwidth.</span></span> <span data-ttu-id="afda5-141">Performans ölçeklendirmek için yapmanız gereken tek şey SQL Data Warehouse veritabanınıza ayırır veri ambarı birimlerini (Dwu'lar) sayısını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="afda5-141">To scale performance, all you need to do is adjust the number of data warehouse units (DWUs) that SQL Data Warehouse allocates to your database.</span></span> <span data-ttu-id="afda5-142">SQL veri ambarı hızlı bir şekilde değişiklik yapar ve donanım veya yazılım için temel alınan tüm değişiklikleri işler.</span><span class="sxs-lookup"><span data-stu-id="afda5-142">SQL Data Warehouse quickly makes the change and handles all the underlying changes to hardware or software.</span></span>

<span data-ttu-id="afda5-143">Dwu ölçeklendirme hakkında daha fazla bilgi için bkz: [ölçeklendirme performans].</span><span class="sxs-lookup"><span data-stu-id="afda5-143">To learn more about scaling DWUs, see [Scale performance].</span></span>

## <a name="pause-and-resume"></a><span data-ttu-id="afda5-144">Duraklatma ve sürdürme</span><span class="sxs-lookup"><span data-stu-id="afda5-144">Pause and resume</span></span>
<span data-ttu-id="afda5-145">Maliyet tasarrufu sağlamak duraklatma ve sürdürme işlem kaynakları isteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="afda5-145">To save costs, you can pause and resume compute resources on-demand.</span></span> <span data-ttu-id="afda5-146">Örneğin, veritabanı gece sırasında ve hafta sonları kullandığınız olmaz, bu saatlerde duraklatma ve gün boyunca sürdürün.</span><span class="sxs-lookup"><span data-stu-id="afda5-146">For example, if you won't be using the database during the night and on weekends, you can pause it during those times, and resume it during the day.</span></span> <span data-ttu-id="afda5-147">Veritabanı duraklatıldığında Dwu için sizden ücret olmaz.</span><span class="sxs-lookup"><span data-stu-id="afda5-147">You won't be charged for DWUs while the database is paused.</span></span>

<span data-ttu-id="afda5-148">Daha fazla bilgi için bkz: [duraklatma işlem][Pause compute], ve [sürdürme işlem][Resume compute].</span><span class="sxs-lookup"><span data-stu-id="afda5-148">For more information, see [Pause compute][Pause compute], and [Resume compute][Resume compute].</span></span>

## <a name="performance-best-practices"></a><span data-ttu-id="afda5-149">Performansı en iyi uygulamalar</span><span class="sxs-lookup"><span data-stu-id="afda5-149">Performance Best Practices</span></span>
<span data-ttu-id="afda5-150">İpuçları ve en iyi sağ başından iş püf noktalarını bulma çok fazla ile yeni bir teknoloji Başlarken zaman kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="afda5-150">When getting started with a new technology, discovering the tips and tricks that work best right from the start can save you lots of time.</span></span>  <span data-ttu-id="afda5-151">Bizim konuları çoğunu tamamında en iyi yöntemler bulacaksınız.</span><span class="sxs-lookup"><span data-stu-id="afda5-151">You will find best practices throughout many of our topics.</span></span>

<span data-ttu-id="afda5-152">Birçok İş yükünüzün geliştirilirken en önemli konular özetini görmek için bkz: [SQL veri ambarı en iyi uygulamalar][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="afda5-152">To see many a summary of the most important considerations when developing your workload, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

## <a name="query-monitoring"></a><span data-ttu-id="afda5-153">Sorgu izlemesi</span><span class="sxs-lookup"><span data-stu-id="afda5-153">Query Monitoring</span></span>
<span data-ttu-id="afda5-154">Bazen bir sorgu uzun çalışıyor, ancak hangi sorunlu biri emin değil.</span><span class="sxs-lookup"><span data-stu-id="afda5-154">Sometimes a query is running too long, but you aren't sure of which one is the culprit.</span></span> <span data-ttu-id="afda5-155">SQL veri ambarı hangi sorgu çok uzun sürüyor bulmak için kullanabileceğiniz dinamik yönetim görünümlerini (Dmv'leri) sahiptir.</span><span class="sxs-lookup"><span data-stu-id="afda5-155">SQL Data Warehouse has dynamic management views (DMVs) that you can use to figure out which query is taking too long.</span></span>

<span data-ttu-id="afda5-156">Uzun süre çalışan sorguları bulmak için bkz: [Dmv'leri kullanarak, iş yükünü izlemek][Monitor your workload using DMVs].</span><span class="sxs-lookup"><span data-stu-id="afda5-156">To find long-running queries, see [Monitor your workload using DMVs][Monitor your workload using DMVs].</span></span>

## <a name="security"></a><span data-ttu-id="afda5-157">Güvenlik</span><span class="sxs-lookup"><span data-stu-id="afda5-157">Security</span></span>
<span data-ttu-id="afda5-158">Güvenli bir sistemde korumak için uyarıdaki olabilir ve her tür yetkisiz erişime karşı koruma.</span><span class="sxs-lookup"><span data-stu-id="afda5-158">To maintain a secure system, you must be on the alert and guard against any type of unauthorized access.</span></span> <span data-ttu-id="afda5-159">Güvenlik duvarı kuralları yalnızca yetkili IP adreslerini bağlanabilir karşılandığından emin olmak bir güvenlik sistemi gerekir.</span><span class="sxs-lookup"><span data-stu-id="afda5-159">A security system needs to make sure firewall rules are in place so only authorized IP addresses can connect.</span></span> <span data-ttu-id="afda5-160">Kullanıcı kimlik bilgilerinin düzgün bir kimlik doğrulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="afda5-160">It needs proper authentication of user credentials.</span></span> <span data-ttu-id="afda5-161">Bir kullanıcı veritabanına bağlandı sonra kullanıcı yalnızca en az çeşitli eylemleri gerçekleştirmek için izinlere sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="afda5-161">After a user has connected to the database, the user should only have permissions to perform a minimal number of actions.</span></span> <span data-ttu-id="afda5-162">Verilerin güvenliğini sağlamak için şifreleme kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="afda5-162">To secure data, you can use encryption.</span></span> <span data-ttu-id="afda5-163">Olması önemlidir denetim ve tüm şüpheli etkinlikleri ise olayları yeniden izlemesine şekilde izleme.</span><span class="sxs-lookup"><span data-stu-id="afda5-163">It's also important to have auditing and tracking so you can retrace events if there is any suspicious activity.</span></span>

<span data-ttu-id="afda5-164">Güvenlik yönetme hakkında bilgi edinmek için üzerinden için head [güvenliğine genel bakış][Security overview].</span><span class="sxs-lookup"><span data-stu-id="afda5-164">To learn about managing security, head over to the [Security overview][Security overview].</span></span>

## <a name="backup-and-restore"></a><span data-ttu-id="afda5-165">Yedekleme ve geri yükleme</span><span class="sxs-lookup"><span data-stu-id="afda5-165">Backup and restore</span></span>
<span data-ttu-id="afda5-166">Verilerinizin güvenilir backps sahip, herhangi bir üretim veritabanını önemli bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="afda5-166">Having reliable backps of your data is an essential part of any production database.</span></span> <span data-ttu-id="afda5-167">SQL veri ambarı otomatik olarak düzenli aralıklarla, etkin veritabanlarını yedekleyerek, verilerinizi güvenli tutar.</span><span class="sxs-lookup"><span data-stu-id="afda5-167">SQL Data Warehouse keeps your data safe by automatically backing up your active databases at regular intervals.</span></span> <span data-ttu-id="afda5-168">Bu yedeklemeler, buradan verilerinizi bozulmuş veya yanlışlıkla veri veya veritabanı bırakılan senaryolarından kurtarmanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="afda5-168">These backups allow you to recover from scenarios where you've corrupted your data or accidentally dropped your data or database.</span></span>  <span data-ttu-id="afda5-169">Veri yedekleme zamanlaması için bkz: bekletme ilkesi ve bir veritabanını geri yüklemek nasıl [anlık görüntüden geri][Restore from snapshot].</span><span class="sxs-lookup"><span data-stu-id="afda5-169">For the data backup schedule, retention policy and how to restore a database, see [Restore from snapshot][Restore from snapshot].</span></span>

## <a name="next-steps"></a><span data-ttu-id="afda5-170">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="afda5-170">Next steps</span></span>
<span data-ttu-id="afda5-171">İyi veritabanı tasarım ilkeleri SQL Data Warehouse veritabanınızda yönetmenizi kolaylaştırır kullanma.</span><span class="sxs-lookup"><span data-stu-id="afda5-171">Using good database design principles will make it easier to manage your databases in SQL Data Warehouse.</span></span> <span data-ttu-id="afda5-172">Daha fazla bilgi için üzerinden için head [geliştirmeye genel bakış][Development overview].</span><span class="sxs-lookup"><span data-stu-id="afda5-172">To learn more, head over to the [Development overview][Development overview].</span></span>

<!--Image references-->

<!--Article references-->
[Create a SQL Data Warehouse (Azure Portal)]: sql-data-warehouse-get-started-provision.md
[Create a database (PowerShell)]: sql-data-warehouse-get-started-provision-powershell.md
[connection]: sql-data-warehouse-develop-connections.md
[Query Azure SQL Data Warehouse with Visual Studio]: sql-data-warehouse-query-visual-studio.md
[Connect and query with sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md
[Development overview]: sql-data-warehouse-overview-develop.md
[Monitor your workload using DMVs]: sql-data-warehouse-manage-monitor.md
[Pause compute]: sql-data-warehouse-manage-compute-overview.md#pause-compute-bk
[Restore from snapshot]: sql-data-warehouse-restore-database-overview.md
[Resume compute]: sql-data-warehouse-manage-compute-overview.md#resume-compute-bk
<span data-ttu-id="afda5-173">[ölçeklendirme performans]: sql-data-warehouse-manage-compute-overview.md#scale-compute</span><span class="sxs-lookup"><span data-stu-id="afda5-173">[Scale performance]: sql-data-warehouse-manage-compute-overview.md#scale-compute</span></span>
[Security overview]: sql-data-warehouse-overview-manage-security.md
[SQL Data Warehouse Best Practices]: sql-data-warehouse-best-practices.md
[SQL Data Warehouse system views]: sql-data-warehouse-reference-tsql-system-views.md

<!--MSDN references-->
[SQL Server Data Tools]: https://msdn.microsoft.com/library/mt204009.aspx

<!--Other web references-->
[Azure portal]: http://portal.azure.com/
