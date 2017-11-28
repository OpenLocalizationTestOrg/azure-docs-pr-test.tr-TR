---
title: "Azure SQL Data Warehouse veritabanlarında aaaManage | Microsoft Docs"
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
ms.openlocfilehash: caec6572c4ab395107c3b095adc69a53eae8bd88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-databases-in-azure-sql-data-warehouse"></a><span data-ttu-id="7f370-104">Azure SQL Data Warehouse veritabanlarında yönetme</span><span class="sxs-lookup"><span data-stu-id="7f370-104">Manage databases in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="7f370-105">SQL veri ambarı veritabanlarınızı yönetme birçok nokta otomatikleştirir.</span><span class="sxs-lookup"><span data-stu-id="7f370-105">SQL Data Warehouse automates many aspects of managing your databases.</span></span> <span data-ttu-id="7f370-106">Örneğin, yalnızca tooadjust gerekir ve Merhaba sağ düzeyini işlem kaynaklarını ödeme ve SQL Data Warehouse izin tooscale performans ölçeğini genişletme ve geri ölçeklendirme tüm hello işini yapın.</span><span class="sxs-lookup"><span data-stu-id="7f370-106">For example, tooscale performance you only need tooadjust and pay for hello right level of compute resources, and then let SQL Data Warehouse do all hello work of scaling out and scaling back.</span></span>

<span data-ttu-id="7f370-107">Performansınızı gereken yanı sıra uzun süre çalışan sorgularda sorun giderme, iş yükü tooidentify toomonitor kuşkusuz isteyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="7f370-107">You will undoubtedly want toomonitor your workload tooidentify your performance needs as well as troubleshoot long-running queries.</span></span> <span data-ttu-id="7f370-108">Kullanıcılar ve oturum açmalar için birkaç güvenlik görevlerini toomanage izinleri de tooperform gerekir.</span><span class="sxs-lookup"><span data-stu-id="7f370-108">You will also need tooperform a few security tasks toomanage permissions for users and logins.</span></span>

<span data-ttu-id="7f370-109">Bu genel bakışta bu yönlerini SQL veri ambarı yönetimi ele alınmaktadır.</span><span class="sxs-lookup"><span data-stu-id="7f370-109">This overview covers these aspects of managing SQL Data Warehouse.</span></span>

* <span data-ttu-id="7f370-110">Yönetim araçları</span><span class="sxs-lookup"><span data-stu-id="7f370-110">Management tools</span></span>
* <span data-ttu-id="7f370-111">Bilgi işlem</span><span class="sxs-lookup"><span data-stu-id="7f370-111">Scale Compute</span></span>
* <span data-ttu-id="7f370-112">Duraklatma ve sürdürme</span><span class="sxs-lookup"><span data-stu-id="7f370-112">Pause and Resume</span></span>
* <span data-ttu-id="7f370-113">Performansı en iyi uygulamalar</span><span class="sxs-lookup"><span data-stu-id="7f370-113">Performance Best Practices</span></span>
* <span data-ttu-id="7f370-114">Sorgu izlemesi</span><span class="sxs-lookup"><span data-stu-id="7f370-114">Query Monitoring</span></span>
* <span data-ttu-id="7f370-115">Güvenlik</span><span class="sxs-lookup"><span data-stu-id="7f370-115">Security</span></span>
* <span data-ttu-id="7f370-116">Yedekleme ve geri yükleme</span><span class="sxs-lookup"><span data-stu-id="7f370-116">Backup and restore</span></span>

## <a name="management-tools"></a><span data-ttu-id="7f370-117">Yönetim araçları</span><span class="sxs-lookup"><span data-stu-id="7f370-117">Management tools</span></span>
<span data-ttu-id="7f370-118">SQL veri ambarı'nda çeşitli araçlar toomanage veritabanlarıyla kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7f370-118">You can use a variety of tools toomanage databases in SQL Data Warehouse.</span></span> <span data-ttu-id="7f370-119">Veritabanları yönetirken, aracı Tercihler geliştireceksiniz görevinin her türü için tooperform gerekir.</span><span class="sxs-lookup"><span data-stu-id="7f370-119">As you manage databases, you will develop tool preferences for each type of task you need tooperform.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="7f370-120">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="7f370-120">Azure portal</span></span>
<span data-ttu-id="7f370-121">Merhaba [Azure portal] [ Azure portal] burada oluşturabilir, güncelleştirme ve veritabanlarını silin ve veritabanı kaynaklarını izleme web tabanlı portal değil.</span><span class="sxs-lookup"><span data-stu-id="7f370-121">hello [Azure portal][Azure portal] is a web-based portal where you can create, update, and delete databases and monitor database resources.</span></span> <span data-ttu-id="7f370-122">Bu harika bir araçtır, yalnızca veri ambarı veritabanlarını, az sayıda yönetme Azure ile çalışmaya Başlarken veya tooquickly bir şey yapmanız gerekmiyor.</span><span class="sxs-lookup"><span data-stu-id="7f370-122">This tool is great is if you're just getting started with Azure, managing a small number of data warehouse databases, or need tooquickly do something.</span></span>

<span data-ttu-id="7f370-123">Hello Azure portal ile çalışmaya tooget bkz [SQL veri ambarı (Azure portalı) oluşturma][Create a SQL Data Warehouse (Azure portal)].</span><span class="sxs-lookup"><span data-stu-id="7f370-123">tooget started with hello Azure portal, see [Create a SQL Data Warehouse (Azure portal)][Create a SQL Data Warehouse (Azure portal)].</span></span>

### <a name="sql-server-data-tools-in-visual-studio"></a><span data-ttu-id="7f370-124">SQL Server veri araçları Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7f370-124">SQL Server Data Tools in Visual Studio</span></span>
<span data-ttu-id="7f370-125">[SQL Server veri Araçları] [ SQL Server Data Tools] (SSDT) Visual Studio'da, yönetmek ve veritabanlarınızı geliştirmek tooconnect sağlar.</span><span class="sxs-lookup"><span data-stu-id="7f370-125">[SQL Server Data Tools][SQL Server Data Tools] (SSDT) in Visual Studio allows you tooconnect to, manage, and develop your databases.</span></span> <span data-ttu-id="7f370-126">Bir uygulama geliştiricisi Visual Studio'ya veya diğer tümleşik geliştirme ortamlarını (IDE) hakkında bilgi sahibi değilseniz, Visual Studio'da SSDT kullanmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="7f370-126">If you're an application developer familiar with Visual Studio or other integrated development environments (IDEs), try using SSDT in Visual Studio.</span></span>

<span data-ttu-id="7f370-127">SSDT hello toovisualize sağlayan SQL Server Nesne Gezgini içerir, bağlanmak ve SQL Data Warehouse veritabanlarında komut dosyalarını çalıştır.</span><span class="sxs-lookup"><span data-stu-id="7f370-127">SSDT includes hello SQL Server Object Explorer which enables you toovisualize, connect, and execute scripts against SQL Data Warehouse databases.</span></span> <span data-ttu-id="7f370-128">tooquickly tooSQL veri ambarına bağlanmak, hello tıklamanız yeterlidir **Visual Studio'da Aç** hello veritabanı ayrıntıları hello Klasik Azure portalı görüntülerken hello komut çubuğu düğmesini.</span><span class="sxs-lookup"><span data-stu-id="7f370-128">tooquickly connect tooSQL Data Warehouse, you can simply click hello **Open in Visual Studio** button in hello command bar when viewing hello database details in hello Azure Classic Portal.</span></span>  

<span data-ttu-id="7f370-129">Visual Studio'da SSDT kullanmaya tooget bkz [sorgu Azure SQL Data Warehouse Visual Studio ile][Query Azure SQL Data Warehouse with Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="7f370-129">tooget started with SSDT in Visual Studio, see [Query Azure SQL Data Warehouse with Visual Studio][Query Azure SQL Data Warehouse with Visual Studio].</span></span>

### <a name="command-line-tools"></a><span data-ttu-id="7f370-130">Komut satırı araçları</span><span class="sxs-lookup"><span data-stu-id="7f370-130">Command-line tools</span></span>
<span data-ttu-id="7f370-131">Komut satırı araçlarını, iş yüklerini otomatikleştirmek için idealdir.</span><span class="sxs-lookup"><span data-stu-id="7f370-131">Command line tools are ideal for automating your workloads.</span></span>  <span data-ttu-id="7f370-132">PowerShell ve sqlcmd olan iki yolları tooautomate işlemlerinizi.</span><span class="sxs-lookup"><span data-stu-id="7f370-132">PowerShell and sqlcmd are two great ways tooautomate your processes.</span></span>  <span data-ttu-id="7f370-133">Çok sayıda mantıksal sunucuları yönetme ve gerekli hello görevleri komut dosyası ve daha sonra otomatik olarak kaynak değişiklikleri bir üretim ortamında dağıtmak için bu araçları öneririz.</span><span class="sxs-lookup"><span data-stu-id="7f370-133">We recommend these tools for managing a large number of logical servers and deploying resource changes in a production environment as hello tasks necessary can be scripted and then automated.</span></span>

### <a name="dynamic-management-views"></a><span data-ttu-id="7f370-134">Dinamik Yönetim görünümlerini</span><span class="sxs-lookup"><span data-stu-id="7f370-134">Dynamic management views</span></span>
<span data-ttu-id="7f370-135">Dmv'leri SQL veri ambarını yönetme hello ekmek ve ezmesi ' dir.</span><span class="sxs-lookup"><span data-stu-id="7f370-135">DMVs are hello bread and butter of managing SQL Data Warehouse.</span></span> <span data-ttu-id="7f370-136">Merhaba Portalı'nda ortaya çıkarır neredeyse tüm bilgi üzerinde Dmv'leri kullanır.</span><span class="sxs-lookup"><span data-stu-id="7f370-136">Almost all information that surfaces in hello portal relies on DMVs.</span></span> <span data-ttu-id="7f370-137">toosee SQL veri ambarı Dmv'leri listesini görmek [SQL veri ambarı sistem görünümleri][SQL Data Warehouse system views].</span><span class="sxs-lookup"><span data-stu-id="7f370-137">toosee a list of SQL Data Warehouse DMVs, see [SQL Data Warehouse system views][SQL Data Warehouse system views].</span></span>

<span data-ttu-id="7f370-138">başlatıldı, tooget bkz [bağlanma ve sorgu sqlcmd ile][Connect and query with sqlcmd], ve [veritabanı (PowerShell) oluşturma][Create a database (PowerShell)].</span><span class="sxs-lookup"><span data-stu-id="7f370-138">tooget started, see [Connect and query with sqlcmd][Connect and query with sqlcmd], and [Create a database (PowerShell)][Create a database (PowerShell)].</span></span>

## <a name="scale-compute"></a><span data-ttu-id="7f370-139">Bilgi işlem</span><span class="sxs-lookup"><span data-stu-id="7f370-139">Scale compute</span></span>
<span data-ttu-id="7f370-140">SQL veri ambarı'nda performans out veya geri artırarak veya azaltarak işlem kaynakları CPU, bellek ve g/ç bant genişliği tarafından hızlı bir şekilde ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7f370-140">In SQL Data Warehouse, you can quickly scale performance out or back by increasing or decreasing compute resources of CPU, memory, and I/O bandwidth.</span></span> <span data-ttu-id="7f370-141">tooscale performans tek toodo ihtiyacınız olan SQL Data Warehouse tooyour veritabanı ayırır veri ambarı birimi (Dwu) hello sayısını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="7f370-141">tooscale performance, all you need toodo is adjust hello number of data warehouse units (DWUs) that SQL Data Warehouse allocates tooyour database.</span></span> <span data-ttu-id="7f370-142">SQL veri ambarı hızlı bir şekilde değiştirmek hello yapar ve tüm hello temel değişiklikleri toohardware veya yazılım işler.</span><span class="sxs-lookup"><span data-stu-id="7f370-142">SQL Data Warehouse quickly makes hello change and handles all hello underlying changes toohardware or software.</span></span>

<span data-ttu-id="7f370-143">Dwu, ölçeklendirme hakkında daha fazla toolearn bkz [ölçeklendirme performans].</span><span class="sxs-lookup"><span data-stu-id="7f370-143">toolearn more about scaling DWUs, see [Scale performance].</span></span>

## <a name="pause-and-resume"></a><span data-ttu-id="7f370-144">Duraklatma ve sürdürme</span><span class="sxs-lookup"><span data-stu-id="7f370-144">Pause and resume</span></span>
<span data-ttu-id="7f370-145">toosave maliyetleri'nın, duraklatma ve sürdürme işlem kaynakları isteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="7f370-145">toosave costs, you can pause and resume compute resources on-demand.</span></span> <span data-ttu-id="7f370-146">Örneğin, hello veritabanı hello gece sırasında ve hafta sonları kullandığınız olmaz, bu saatlerde duraklatma ve hello günde sürdürün.</span><span class="sxs-lookup"><span data-stu-id="7f370-146">For example, if you won't be using hello database during hello night and on weekends, you can pause it during those times, and resume it during hello day.</span></span> <span data-ttu-id="7f370-147">Merhaba veritabanı duraklatıldığında Dwu için sizden ücret olmaz.</span><span class="sxs-lookup"><span data-stu-id="7f370-147">You won't be charged for DWUs while hello database is paused.</span></span>

<span data-ttu-id="7f370-148">Daha fazla bilgi için bkz: [duraklatma işlem][Pause compute], ve [sürdürme işlem][Resume compute].</span><span class="sxs-lookup"><span data-stu-id="7f370-148">For more information, see [Pause compute][Pause compute], and [Resume compute][Resume compute].</span></span>

## <a name="performance-best-practices"></a><span data-ttu-id="7f370-149">Performansı en iyi uygulamalar</span><span class="sxs-lookup"><span data-stu-id="7f370-149">Performance Best Practices</span></span>
<span data-ttu-id="7f370-150">Merhaba ipuçları ve en iyi sağ hello başından iş püf noktaları bulma ile yeni bir teknoloji Başlarken, çok fazla kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7f370-150">When getting started with a new technology, discovering hello tips and tricks that work best right from hello start can save you lots of time.</span></span>  <span data-ttu-id="7f370-151">Bizim konuları çoğunu tamamında en iyi yöntemler bulacaksınız.</span><span class="sxs-lookup"><span data-stu-id="7f370-151">You will find best practices throughout many of our topics.</span></span>

<span data-ttu-id="7f370-152">toosee, iş yükü geliştirilirken en önemli noktalar hello birçok özetini görmek [SQL veri ambarı en iyi uygulamalar][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="7f370-152">toosee many a summary of hello most important considerations when developing your workload, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

## <a name="query-monitoring"></a><span data-ttu-id="7f370-153">Sorgu izlemesi</span><span class="sxs-lookup"><span data-stu-id="7f370-153">Query Monitoring</span></span>
<span data-ttu-id="7f370-154">Bazen bir sorgu uzun çalışıyor, ancak hello sorunlu hangi biri olduğundan emin değil.</span><span class="sxs-lookup"><span data-stu-id="7f370-154">Sometimes a query is running too long, but you aren't sure of which one is hello culprit.</span></span> <span data-ttu-id="7f370-155">SQL veri ambarı, sorgu çok uzun sürüyor dinamik yönetim görünümlerini (Dmv'leri toofigure kullanabilirsiniz) sahiptir.</span><span class="sxs-lookup"><span data-stu-id="7f370-155">SQL Data Warehouse has dynamic management views (DMVs) that you can use toofigure out which query is taking too long.</span></span>

<span data-ttu-id="7f370-156">toofind uzun süre çalışan sorgular, bkz: [Dmv'leri kullanarak, iş yükünü izlemek][Monitor your workload using DMVs].</span><span class="sxs-lookup"><span data-stu-id="7f370-156">toofind long-running queries, see [Monitor your workload using DMVs][Monitor your workload using DMVs].</span></span>

## <a name="security"></a><span data-ttu-id="7f370-157">Güvenlik</span><span class="sxs-lookup"><span data-stu-id="7f370-157">Security</span></span>
<span data-ttu-id="7f370-158">toomaintain güvenli bir sistemde, her tür yetkisiz erişime karşı koruma ve hello uyarıdaki olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7f370-158">toomaintain a secure system, you must be on hello alert and guard against any type of unauthorized access.</span></span> <span data-ttu-id="7f370-159">Bir güvenlik sistemi toomake güvenlik duvarı kuralları yalnızca yetkili IP adreslerini bağlanabilir karşılandığından emin gerekir.</span><span class="sxs-lookup"><span data-stu-id="7f370-159">A security system needs toomake sure firewall rules are in place so only authorized IP addresses can connect.</span></span> <span data-ttu-id="7f370-160">Kullanıcı kimlik bilgilerinin düzgün bir kimlik doğrulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7f370-160">It needs proper authentication of user credentials.</span></span> <span data-ttu-id="7f370-161">Bir kullanıcı toohello veritabanı bağlandı sonra hello kullanıcı yalnızca izinleri tooperform Eylemler en az sayıda sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7f370-161">After a user has connected toohello database, hello user should only have permissions tooperform a minimal number of actions.</span></span> <span data-ttu-id="7f370-162">toosecure veri şifreleme kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7f370-162">toosecure data, you can use encryption.</span></span> <span data-ttu-id="7f370-163">Ayrıca, Denetim ve tüm şüpheli etkinlikleri ise olayları yeniden izlemesine şekilde izleme önemli toohave unutulmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="7f370-163">It's also important toohave auditing and tracking so you can retrace events if there is any suspicious activity.</span></span>

<span data-ttu-id="7f370-164">Güvenlik, head toohello üzerinden yönetmeyle ilgili toolearn [güvenliğine genel bakış][Security overview].</span><span class="sxs-lookup"><span data-stu-id="7f370-164">toolearn about managing security, head over toohello [Security overview][Security overview].</span></span>

## <a name="backup-and-restore"></a><span data-ttu-id="7f370-165">Yedekleme ve geri yükleme</span><span class="sxs-lookup"><span data-stu-id="7f370-165">Backup and restore</span></span>
<span data-ttu-id="7f370-166">Verilerinizin güvenilir backps sahip, herhangi bir üretim veritabanını önemli bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="7f370-166">Having reliable backps of your data is an essential part of any production database.</span></span> <span data-ttu-id="7f370-167">SQL veri ambarı otomatik olarak düzenli aralıklarla, etkin veritabanlarını yedekleyerek, verilerinizi güvenli tutar.</span><span class="sxs-lookup"><span data-stu-id="7f370-167">SQL Data Warehouse keeps your data safe by automatically backing up your active databases at regular intervals.</span></span> <span data-ttu-id="7f370-168">Bu yedeklemeler buradan verilerinizi bozulmuş veya yanlışlıkla veri veya veritabanı bırakılan senaryolardan toorecover izin verin.</span><span class="sxs-lookup"><span data-stu-id="7f370-168">These backups allow you toorecover from scenarios where you've corrupted your data or accidentally dropped your data or database.</span></span>  <span data-ttu-id="7f370-169">Merhaba veri yedekleme zamanlamasını, bekletme ilkesi için ve nasıl toorestore bir veritabanı bkz [anlık görüntüden geri][Restore from snapshot].</span><span class="sxs-lookup"><span data-stu-id="7f370-169">For hello data backup schedule, retention policy and how toorestore a database, see [Restore from snapshot][Restore from snapshot].</span></span>

## <a name="next-steps"></a><span data-ttu-id="7f370-170">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7f370-170">Next steps</span></span>
<span data-ttu-id="7f370-171">İyi veritabanı tasarım ilkeleri kullanarak hale getirir, daha kolay toomanage SQL Data Warehouse veritabanınızda.</span><span class="sxs-lookup"><span data-stu-id="7f370-171">Using good database design principles will make it easier toomanage your databases in SQL Data Warehouse.</span></span> <span data-ttu-id="7f370-172">toolearn daha toohello üzerinden head [geliştirmeye genel bakış][Development overview].</span><span class="sxs-lookup"><span data-stu-id="7f370-172">toolearn more, head over toohello [Development overview][Development overview].</span></span>

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
[ölçeklendirme performans]: sql-data-warehouse-manage-compute-overview.md#scale-compute
[Security overview]: sql-data-warehouse-overview-manage-security.md
[SQL Data Warehouse Best Practices]: sql-data-warehouse-best-practices.md
[SQL Data Warehouse system views]: sql-data-warehouse-reference-tsql-system-views.md

<!--MSDN references-->
[SQL Server Data Tools]: https://msdn.microsoft.com/library/mt204009.aspx

<!--Other web references-->
[Azure portal]: http://portal.azure.com/
