---
title: Azure SQL Data warehouse'da aaaAuditing | Microsoft Docs
description: "Azure SQL Data Warehouse'da denetimi ile çalışmaya başlama"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: 0e6af148-b218-4b43-bb5f-907917d20330
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 08/21/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 948de74fa052ef206cf1aa65c0d81f084b18cb00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="auditing-in-azure-sql-data-warehouse"></a><span data-ttu-id="dcb6c-103">Azure SQL veri ambarı'nda denetleme</span><span class="sxs-lookup"><span data-stu-id="dcb6c-103">Auditing in Azure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="dcb6c-104">Denetim</span><span class="sxs-lookup"><span data-stu-id="dcb6c-104">Auditing</span></span>](sql-data-warehouse-auditing-overview.md)
> * [<span data-ttu-id="dcb6c-105">Tehdit algılama</span><span class="sxs-lookup"><span data-stu-id="dcb6c-105">Threat detection</span></span>](sql-data-warehouse-security-threat-detection.md)
> 
> 

<span data-ttu-id="dcb6c-106">SQL veri ambarı denetim toorecord olayları, veritabanı tooan Denetim günlüğüne Azure depolama hesabınızdaki sağlar.</span><span class="sxs-lookup"><span data-stu-id="dcb6c-106">SQL Data Warehouse auditing allows you toorecord events in your database tooan audit log in your Azure Storage account.</span></span> <span data-ttu-id="dcb6c-107">Denetim, yönetmeliklere uygunluğu korumanıza, veritabanı etkinliklerini anlamanıza ve ifade eden tutarsızlıklar ve iş endişeleri veya güvenlik ihlalleri hakkında daha fazla bilgi kavramanıza yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="dcb6c-107">Auditing can help you maintain regulatory compliance, understand  database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span> <span data-ttu-id="dcb6c-108">Ayrıca SQL Data Warehouse denetim Microsoft Power BI ile ayrıntıya raporlama ve analiz için ile tümleştirir.</span><span class="sxs-lookup"><span data-stu-id="dcb6c-108">SQL Data Warehouse auditing also integrates with Microsoft Power BI for drill-down reporting and analysis.</span></span>

<span data-ttu-id="dcb6c-109">Denetleme Araçları etkinleştirmek ve bağlılığı toocompliance standartları kolaylaştırmak ancak Uyumluluk garanti etmez.</span><span class="sxs-lookup"><span data-stu-id="dcb6c-109">Auditing tools enable and facilitate adherence toocompliance standards but don't guarantee compliance.</span></span> <span data-ttu-id="dcb6c-110">Bu destek standartları uyumluluğu Azure hakkında daha fazla bilgi programları hello bakın <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Azure Güven Merkezi</a>.</span><span class="sxs-lookup"><span data-stu-id="dcb6c-110">For more information about Azure programs that support standards compliance, see hello <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Azure Trust Center</a>.</span></span>

* <span data-ttu-id="dcb6c-111">[Veritabanı denetim temelleri]</span><span class="sxs-lookup"><span data-stu-id="dcb6c-111">[Database Auditing basics]</span></span>
* <span data-ttu-id="dcb6c-112">[Veritabanınız için denetimi ayarlamanız]</span><span class="sxs-lookup"><span data-stu-id="dcb6c-112">[Set up auditing for your database]</span></span>
* <span data-ttu-id="dcb6c-113">[Denetim günlüklerini ve raporları analiz eder.]</span><span class="sxs-lookup"><span data-stu-id="dcb6c-113">[Analyze audit logs and reports]</span></span>

## <span data-ttu-id="dcb6c-114"><a id="subheading-1"></a>Azure SQL veri ambarı veritabanı denetimi temelleri</span><span class="sxs-lookup"><span data-stu-id="dcb6c-114"><a id="subheading-1"></a>Azure SQL Data Warehouse Database Auditing basics</span></span>
<span data-ttu-id="dcb6c-115">SQL veri ambarı veritabanı denetimi yapmanıza olanak sağlar:</span><span class="sxs-lookup"><span data-stu-id="dcb6c-115">SQL Data Warehouse database auditing allows you to:</span></span>

* <span data-ttu-id="dcb6c-116">**Korumak** seçili olayların bir denetim izi.</span><span class="sxs-lookup"><span data-stu-id="dcb6c-116">**Retain** an audit trail of selected events.</span></span> <span data-ttu-id="dcb6c-117">Denetlenecek veritabanı Eylemler toobe kategorilerini tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dcb6c-117">You can define categories of database actions  toobe audited.</span></span>
* <span data-ttu-id="dcb6c-118">**Rapor** veritabanı etkinlik.</span><span class="sxs-lookup"><span data-stu-id="dcb6c-118">**Report** on database activity.</span></span> <span data-ttu-id="dcb6c-119">Önceden yapılandırılmış raporları ve etkinlik ve olay Raporlama ile hızlı şekilde kullanmaya bir Pano tooget kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dcb6c-119">You can use preconfigured reports and a dashboard tooget started quickly with activity and event reporting.</span></span>
* <span data-ttu-id="dcb6c-120">**Analiz** raporlar.</span><span class="sxs-lookup"><span data-stu-id="dcb6c-120">**Analyze** reports.</span></span> <span data-ttu-id="dcb6c-121">Şüpheli olayları, olağan dışı etkinliği ve eğilimleri bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dcb6c-121">You can find suspicious events, unusual activity, and trends.</span></span>

<span data-ttu-id="dcb6c-122">Olay kategorileri aşağıdaki Merhaba denetimini yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="dcb6c-122">You can configure auditing for hello following event categories:</span></span>

<span data-ttu-id="dcb6c-123">**Düz SQL** ve **parametreli SQL** olarak sınıflandırılan hangi hello için toplanan denetim günlükleri</span><span class="sxs-lookup"><span data-stu-id="dcb6c-123">**Plain SQL** and **Parameterized SQL** for which hello collected audit logs are classified as</span></span>  

* <span data-ttu-id="dcb6c-124">**Erişim toodata**</span><span class="sxs-lookup"><span data-stu-id="dcb6c-124">**Access toodata**</span></span>
* <span data-ttu-id="dcb6c-125">**Şema değişiklikleri (DDL)**</span><span class="sxs-lookup"><span data-stu-id="dcb6c-125">**Schema changes (DDL)**</span></span>
* <span data-ttu-id="dcb6c-126">**Veri değişiklikleri (DML)**</span><span class="sxs-lookup"><span data-stu-id="dcb6c-126">**Data changes (DML)**</span></span>
* <span data-ttu-id="dcb6c-127">**Hesapları, rolleri ve izinleri (DCL)**</span><span class="sxs-lookup"><span data-stu-id="dcb6c-127">**Accounts, roles, and permissions (DCL)**</span></span>
* <span data-ttu-id="dcb6c-128">**Saklı yordam**, **oturum açma** ve **işlem yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="dcb6c-128">**Stored Procedure**, **Login** and, **Transaction Management**.</span></span>

<span data-ttu-id="dcb6c-129">Her bir olay kategorisi için Denetim, **başarı** ve **hatası** işlemleri ayrı olarak yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="dcb6c-129">For each Event Category, Auditing of **Success** and **Failure** operations are configured separately.</span></span>

<span data-ttu-id="dcb6c-130">Merhaba hello etkinlikleri ve denetlenen olayları hakkında daha fazla bilgi için bkz: <a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">denetim günlük biçimi başvurusu (doc dosya indirme)</a>.</span><span class="sxs-lookup"><span data-stu-id="dcb6c-130">For more information about hello activities and events audited, see hello <a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">Audit Log Format Reference (doc file download)</a>.</span></span>

<span data-ttu-id="dcb6c-131">Denetim günlükleri, Azure depolama hesabında depolanır.</span><span class="sxs-lookup"><span data-stu-id="dcb6c-131">Audit logs are stored in your Azure storage account.</span></span> <span data-ttu-id="dcb6c-132">Bir denetim günlük Bekletme dönemi tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dcb6c-132">You can define an audit log retention period.</span></span>

<span data-ttu-id="dcb6c-133">Bir denetim ilkesi, belirli bir veritabanı veya varsayılan sunucu ilkesi olarak tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="dcb6c-133">An auditing policy can be defined for a specific database or as a default server policy.</span></span> <span data-ttu-id="dcb6c-134">Varsayılan sunucu denetim ilkesi tooall veritabanları tanımlanmış bir özel geçersiz kılma veritabanı denetim ilkesi olmayan bir sunucu üzerinde uygulanır.</span><span class="sxs-lookup"><span data-stu-id="dcb6c-134">A default server auditing policy applies tooall databases on a server, which do not have a specific overriding database auditing policy defined.</span></span>

<span data-ttu-id="dcb6c-135">Denetimi kullanıyorsanız onay denetim ayarlamadan önce bir ["Alt düzey istemci."](sql-data-warehouse-auditing-downlevel-clients.md)</span><span class="sxs-lookup"><span data-stu-id="dcb6c-135">Before setting up audit auditing check if you are using a ["Downlevel Client."](sql-data-warehouse-auditing-downlevel-clients.md)</span></span>

## <span data-ttu-id="dcb6c-136"><a id="subheading-2"></a>Veritabanınız için denetimi ayarlamanız</span><span class="sxs-lookup"><span data-stu-id="dcb6c-136"><a id="subheading-2"></a>Set up auditing for your database</span></span>
1. <span data-ttu-id="dcb6c-137">Merhaba başlatma <a href="https://portal.azure.com" target="_blank">Azure portal</a>.</span><span class="sxs-lookup"><span data-stu-id="dcb6c-137">Launch hello <a href="https://portal.azure.com" target="_blank">Azure portal</a>.</span></span>
2. <span data-ttu-id="dcb6c-138">Toohello Git **ayarları** hello tooaudit istediğiniz SQL Data Warehouse dikey.</span><span class="sxs-lookup"><span data-stu-id="dcb6c-138">Go toohello **Settings** blade of hello SQL Data Warehouse you want tooaudit.</span></span> <span data-ttu-id="dcb6c-139">Merhaba, **ayarları** dikey penceresinde, select **denetim ve tehdit algılama**.</span><span class="sxs-lookup"><span data-stu-id="dcb6c-139">In hello **Settings** blade, select **Auditing & Threat detection**.</span></span>
   
    ![][1]
3. <span data-ttu-id="dcb6c-140">Ardından, hello tıklayarak denetimi etkinleştirmek **ON** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="dcb6c-140">Next, enable auditing by clicking hello **ON** button.</span></span>
   
    ![][3]
4. <span data-ttu-id="dcb6c-141">Yapılandırma dikey penceresi denetim hello seçin **depolama ayrıntıları** tooopen hello denetim günlüklerini depolama dikey.</span><span class="sxs-lookup"><span data-stu-id="dcb6c-141">In hello auditing configuration blade, select **STORAGE DETAILS** tooopen hello Audit Logs Storage blade.</span></span> <span data-ttu-id="dcb6c-142">Merhaba burada günlükleri kaydedileceği Azure depolama hesabı, hello seçip saklama süresi.</span><span class="sxs-lookup"><span data-stu-id="dcb6c-142">Select hello Azure storage account where logs will be saved and, hello retention period.</span></span> 
>[!TIP]
><span data-ttu-id="dcb6c-143">Aynı depolama hesabı en hello dışında tüm denetlenen veritabanları tooget hello için önceden yapılandırılmış kullanım hello şablonları bildirir.</span><span class="sxs-lookup"><span data-stu-id="dcb6c-143">Use hello same storage account for all audited databases tooget hello most out of hello pre-configured reports templates.</span></span>
   
    ![][4]
5. <span data-ttu-id="dcb6c-144">Merhaba tıklatın **Tamam** düğme toosave hello depolama ayrıntıları yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="dcb6c-144">Click hello **OK** button toosave hello storage details configuration.</span></span>
6. <span data-ttu-id="dcb6c-145">Altında **tarafından olay günlüğü**, tıklatın **başarı** ve **hatası** toolog tüm olayları veya tek tek olay kategorilerini seçin.</span><span class="sxs-lookup"><span data-stu-id="dcb6c-145">Under **LOGGING BY EVENT**, click **SUCCESS** and **FAILURE** toolog all events, or choose individual event categories.</span></span>
7. <span data-ttu-id="dcb6c-146">Bir veritabanı için Denetim yapılandırıyorsanız, tooalter hello bağlantı dizesi verileri denetleme doğru yakalanır, istemci tooensure gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="dcb6c-146">If you are configuring Auditing for a database, you may need tooalter hello connection string of your client tooensure data auditing is correctly captured.</span></span> <span data-ttu-id="dcb6c-147">Merhaba denetleyin [hello bağlantı dizesinde değişiklik sunucu FDQN](sql-data-warehouse-auditing-downlevel-clients.md) alt düzey istemci bağlantıları için konu.</span><span class="sxs-lookup"><span data-stu-id="dcb6c-147">Check hello [Modify Server FDQN in hello connection string](sql-data-warehouse-auditing-downlevel-clients.md) topic for downlevel client connections.</span></span>
8. <span data-ttu-id="dcb6c-148">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dcb6c-148">Click **OK**.</span></span>

## <span data-ttu-id="dcb6c-149"><a id="subheading-3"></a>Denetim günlüklerini ve raporları analiz eder.</span><span class="sxs-lookup"><span data-stu-id="dcb6c-149"><a id="subheading-3"></a>Analyze audit logs and reports</span></span>
<span data-ttu-id="dcb6c-150">Denetim günlüklerini toplanan deposu tablolarla koleksiyonunda bir **SQLDBAuditLogs** hello Kurulum sırasında seçtiğiniz Azure depolama hesabı önek.</span><span class="sxs-lookup"><span data-stu-id="dcb6c-150">Audit logs are aggregated in a collection of Store Tables with a **SQLDBAuditLogs** prefix in hello Azure storage account you chose during setup.</span></span> <span data-ttu-id="dcb6c-151">Bir aracı gibi kullanarak günlük dosyalarını görüntüleyebilirsiniz <a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Azure Storage Gezgini</a>.</span><span class="sxs-lookup"><span data-stu-id="dcb6c-151">You can view log files using a tool such as <a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Azure Storage Explorer</a>.</span></span>

<span data-ttu-id="dcb6c-152">Önceden yapılandırılmış Pano rapor şablonu olarak kullanılabilir bir <a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">indirilebilir Excel elektronik tablosu</a> toohelp günlük verileri hızlı bir şekilde çözümleyin.</span><span class="sxs-lookup"><span data-stu-id="dcb6c-152">A preconfigured dashboard report template is available as a <a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">downloadable Excel spreadsheet</a> toohelp you quickly analyze log data.</span></span> <span data-ttu-id="dcb6c-153">Denetim günlüklerini toouse hello şablonunda, gereksinim duyduğunuz Excel 2013 veya üstü ve indirebilirsiniz Power Query <a href="http://www.microsoft.com/download/details.aspx?id=39379">burada</a>.</span><span class="sxs-lookup"><span data-stu-id="dcb6c-153">toouse hello template on your audit logs, you need Excel 2013 or later and Power Query, which you can download <a href="http://www.microsoft.com/download/details.aspx?id=39379">here</a>.</span></span>

<span data-ttu-id="dcb6c-154">Merhaba şablon kurgusal örnek veriler olan ve doğrudan Azure storage hesabınızdan, Denetim günlüğü Power Query tooimport ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dcb6c-154">hello template has fictional sample data in it, and you can set up Power Query tooimport your audit log directly from your Azure storage account.</span></span>

## <span data-ttu-id="dcb6c-155"><a id="subheading-4"></a>Depolama anahtarını yeniden üretme</span><span class="sxs-lookup"><span data-stu-id="dcb6c-155"><a id="subheading-4"></a>Storage key regeneration</span></span>
<span data-ttu-id="dcb6c-156">Üretimde, depolama alanınızın düzenli aralıklarla anahtarları büyük olasılıkla toorefresh demektir.</span><span class="sxs-lookup"><span data-stu-id="dcb6c-156">In production, you are likely toorefresh your storage keys periodically.</span></span> <span data-ttu-id="dcb6c-157">Anahtarlarınızı yenilerken toosave hello İlkesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="dcb6c-157">When refreshing your keys, you need toosave hello policy.</span></span> <span data-ttu-id="dcb6c-158">Merhaba işlem aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="dcb6c-158">hello process is as follows:</span></span>

1. <span data-ttu-id="dcb6c-159">(Bölüm denetimi hello kurulumunda yukarıda) yapılandırma dikey penceresi denetim hello hello anahtarının **depolama erişim tuşu** gelen *birincil* çok*ikincil* ve  **Kaydet**.</span><span class="sxs-lookup"><span data-stu-id="dcb6c-159">In hello auditing configuration blade (described above in hello setup auditing section) switch hello **Storage Access Key** from *Primary* too*Secondary* and **SAVE**.</span></span>

   ![][4]
2. <span data-ttu-id="dcb6c-160">Git toohello depolama yapılandırma dikey ve **yeniden** hello *birincil erişim anahtarını*.</span><span class="sxs-lookup"><span data-stu-id="dcb6c-160">Go toohello storage configuration blade and **regenerate** hello *Primary Access Key*.</span></span>
3. <span data-ttu-id="dcb6c-161">Yapılandırma dikey penceresinde, anahtar hello denetim toohello dönün **depolama erişim tuşu** gelen *ikincil* çok*birincil* ve basın **KAYDETMEK**.</span><span class="sxs-lookup"><span data-stu-id="dcb6c-161">Go back toohello auditing configuration blade, switch hello **Storage Access Key** from *Secondary* too*Primary* and press **SAVE**.</span></span>
4. <span data-ttu-id="dcb6c-162">Toohello depolama UI geri dönün ve **yeniden** hello *ikincil erişim anahtarını* (hello için hazırlık olarak sonraki anahtarları döngüsü yenileyin.</span><span class="sxs-lookup"><span data-stu-id="dcb6c-162">Go back toohello storage UI and **regenerate** hello *Secondary Access Key* (as preparation for hello next keys refresh cycle.</span></span>

## <span data-ttu-id="dcb6c-163"><a id="subheading-5"></a>Otomasyon (PowerShell/REST API)</span><span class="sxs-lookup"><span data-stu-id="dcb6c-163"><a id="subheading-5"></a>Automation (PowerShell/REST API)</span></span>
<span data-ttu-id="dcb6c-164">Otomasyon araçları aşağıdaki hello kullanarak Azure SQL Data Warehouse'da denetim da yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="dcb6c-164">You can also configure auditing in Azure SQL Data Warehouse by using hello following automation tools:</span></span>

* <span data-ttu-id="dcb6c-165">**PowerShell cmdlet'leri**:</span><span class="sxs-lookup"><span data-stu-id="dcb6c-165">**PowerShell cmdlets**:</span></span>

   * <span data-ttu-id="dcb6c-166">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span><span class="sxs-lookup"><span data-stu-id="dcb6c-166">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span></span>
   * <span data-ttu-id="dcb6c-167">[Get-AzureRMSqlServerAuditingPolicy][102]</span><span class="sxs-lookup"><span data-stu-id="dcb6c-167">[Get-AzureRMSqlServerAuditingPolicy][102]</span></span>
   * <span data-ttu-id="dcb6c-168">[Remove-AzureRMSqlDatabaseAuditing][103]</span><span class="sxs-lookup"><span data-stu-id="dcb6c-168">[Remove-AzureRMSqlDatabaseAuditing][103]</span></span>
   * <span data-ttu-id="dcb6c-169">[Remove-AzureRMSqlServerAuditing][104]</span><span class="sxs-lookup"><span data-stu-id="dcb6c-169">[Remove-AzureRMSqlServerAuditing][104]</span></span>
   * <span data-ttu-id="dcb6c-170">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span><span class="sxs-lookup"><span data-stu-id="dcb6c-170">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span></span>
   * <span data-ttu-id="dcb6c-171">[Set-AzureRMSqlServerAuditingPolicy][106]</span><span class="sxs-lookup"><span data-stu-id="dcb6c-171">[Set-AzureRMSqlServerAuditingPolicy][106]</span></span>
   * <span data-ttu-id="dcb6c-172">[Kullanım AzureRMSqlServerAuditingPolicy][107]</span><span class="sxs-lookup"><span data-stu-id="dcb6c-172">[Use-AzureRMSqlServerAuditingPolicy][107]</span></span>

<!--Anchors-->
[Veritabanı denetim temelleri]: #subheading-1
[Veritabanınız için denetimi ayarlamanız]: #subheading-2
[Denetim günlüklerini ve raporları analiz eder.]: #subheading-3


<!--Image references-->
[1]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing.png
[2]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-inherit.png
[3]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-enable.png
[4]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-storage-account.png
[5]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-dashboard.png


<!--Link references-->
[101]: /powershell/module/azurerm.sql/get-azurermsqldatabaseauditingpolicy
[102]: /powershell/module/azurerm.sql/Get-AzureRMSqlServerAuditingPolicy
[103]: /powershell/module/azurerm.sql/Remove-AzureRMSqlDatabaseAuditing
[104]: /powershell/module/azurerm.sql/Remove-AzureRMSqlServerAuditing
[105]: /powershell/module/azurerm.sql/Set-AzureRMSqlDatabaseAuditingPolicy
[106]: /powershell/module/azurerm.sql/Set-AzureRMSqlServerAuditingPolicy
[107]: /powershell/module/azurerm.sql/Use-AzureRMSqlServerAuditingPolicy