---
title: "aaaGet başlatılan Azure SQL veritabanı denetimi ile | Microsoft Docs"
description: "Azure SQL veritabanı denetimi ile çalışmaya başlama"
services: sql-database
documentationcenter: 
author: giladm
manager: jhubbard
editor: giladm
ms.assetid: 89c2a155-c2fb-4b67-bc19-9b4e03c6d3bc
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: giladm
ms.openlocfilehash: 5494c602d702ac41992520f900c393a98cc7c989
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-database-auditing"></a><span data-ttu-id="e0460-103">SQL veritabanı denetimini kullanmaya başlayın</span><span class="sxs-lookup"><span data-stu-id="e0460-103">Get started with SQL database auditing</span></span>
<span data-ttu-id="e0460-104">Azure SQL veritabanı denetimi veritabanı olaylarını izler ve bunları Azure depolama hesabınızdaki tooan denetim günlüğünü yazar.</span><span class="sxs-lookup"><span data-stu-id="e0460-104">Azure SQL database auditing tracks database events and writes them tooan audit log in your Azure storage account.</span></span> <span data-ttu-id="e0460-105">Ayrıca denetleme:</span><span class="sxs-lookup"><span data-stu-id="e0460-105">Auditing also:</span></span>

* <span data-ttu-id="e0460-106">Yönetmeliklere uygunluğu korumanıza, veritabanı etkinliklerini anlamanıza ve ifade eden tutarsızlıklar ve iş endişeleri veya güvenlik ihlalleri hakkında daha fazla bilgi kavramanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="e0460-106">Helps you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

* <span data-ttu-id="e0460-107">Etkinleştirir ve uyumluluk garanti etmez ancak bağlılığı toocompliance standartları kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="e0460-107">Enables and facilitates adherence toocompliance standards, although it doesn't guarantee compliance.</span></span> <span data-ttu-id="e0460-108">Bu destek standartları uyumluluğu Azure hakkında daha fazla bilgi programları hello bakın [Azure Güven Merkezi](https://azure.microsoft.com/support/trust-center/compliance/).</span><span class="sxs-lookup"><span data-stu-id="e0460-108">For more information about Azure programs that support standards compliance, see hello [Azure Trust Center](https://azure.microsoft.com/support/trust-center/compliance/).</span></span>


## <span data-ttu-id="e0460-109"><a id="subheading-1"></a>Genel Bakış denetim azure SQL veritabanı</span><span class="sxs-lookup"><span data-stu-id="e0460-109"><a id="subheading-1"></a>Azure SQL database auditing overview</span></span>
<span data-ttu-id="e0460-110">SQL veritabanı için denetimi kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e0460-110">You can use SQL database auditing to:</span></span>


* <span data-ttu-id="e0460-111">**Korumak** seçili olayların bir denetim izi.</span><span class="sxs-lookup"><span data-stu-id="e0460-111">**Retain** an audit trail of selected events.</span></span> <span data-ttu-id="e0460-112">Denetlenecek veritabanı Eylemler toobe kategorilerini tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e0460-112">You can define categories of database actions toobe audited.</span></span>
* <span data-ttu-id="e0460-113">**Rapor** veritabanı etkinlik.</span><span class="sxs-lookup"><span data-stu-id="e0460-113">**Report** on database activity.</span></span> <span data-ttu-id="e0460-114">Önceden yapılandırılmış raporları ve etkinlik ve olay Raporlama ile hızlı şekilde kullanmaya bir Pano tooget kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e0460-114">You can use preconfigured reports and a dashboard tooget started quickly with activity and event reporting.</span></span>
* <span data-ttu-id="e0460-115">**Analiz** raporlar.</span><span class="sxs-lookup"><span data-stu-id="e0460-115">**Analyze** reports.</span></span> <span data-ttu-id="e0460-116">Şüpheli olayları, olağan dışı etkinliği ve eğilimleri bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e0460-116">You can find suspicious events, unusual activity, and trends.</span></span>

<span data-ttu-id="e0460-117">Farklı türlerde olay kategorisi için Denetim hello açıklandığı gibi yapılandırabileceğiniz [veritabanınız için denetimi ayarlamanız](#subheading-2) bölümü.</span><span class="sxs-lookup"><span data-stu-id="e0460-117">You can configure auditing for different types of event categories, as explained in hello [Set up auditing for your database](#subheading-2) section.</span></span>

<span data-ttu-id="e0460-118">Denetim günlüklerini tooAzure Blob storage, Azure aboneliğinizde yazılır.</span><span class="sxs-lookup"><span data-stu-id="e0460-118">Audit logs are written tooAzure Blob storage on your Azure subscription.</span></span>


## <span data-ttu-id="e0460-119"><a id="subheading-8"></a>Sunucu düzeyinde ve veritabanı düzeyi denetim ilkesi tanımlayın</span><span class="sxs-lookup"><span data-stu-id="e0460-119"><a id="subheading-8"></a>Define server-level vs. database-level auditing policy</span></span>

<span data-ttu-id="e0460-120">Bir denetim ilkesi, belirli bir veritabanı veya varsayılan sunucu ilkesi olarak tanımlanabilir:</span><span class="sxs-lookup"><span data-stu-id="e0460-120">An auditing policy can be defined for a specific database or as a default server policy:</span></span>

* <span data-ttu-id="e0460-121">Bir sunucu ilkesi tooall mevcut ve yeni oluşturulan veritabanları hello sunucu üzerinde uygulanır.</span><span class="sxs-lookup"><span data-stu-id="e0460-121">A server policy applies tooall existing and newly created databases on hello server.</span></span>

* <span data-ttu-id="e0460-122">Varsa *sunucu blob denetimi etkin*, onu *toohello veritabanı her zaman geçerli* (diğer bir deyişle, hello veritabanı denetlenmez), bağımsız olarak hello veritabanı denetim ayarları.</span><span class="sxs-lookup"><span data-stu-id="e0460-122">If *server blob auditing is enabled*, it *always applies toohello database* (that is, hello database will be audited), regardless of hello database auditing settings.</span></span>

* <span data-ttu-id="e0460-123">Merhaba veritabanında toplama tooenabling üzerinde hello sunucuda denetim blob etkinleştirme olacak *değil* geçersiz kılabilir veya hello sunucu blob denetleme hello ayarlardan herhangi birini değiştirmek.</span><span class="sxs-lookup"><span data-stu-id="e0460-123">Enabling blob auditing on hello database, in addition tooenabling it on hello server, will *not* override or change any of hello settings of hello server blob auditing.</span></span> <span data-ttu-id="e0460-124">Her iki denetimleri yan yana yer alır.</span><span class="sxs-lookup"><span data-stu-id="e0460-124">Both audits will exist side by side.</span></span> <span data-ttu-id="e0460-125">Diğer bir deyişle, hello veritabanı (kez hello sunucu İlkesi ve bir kez tarafından hello veritabanı İlkesi) iki kez paralel olarak denetlenecektir.</span><span class="sxs-lookup"><span data-stu-id="e0460-125">In other words, hello database will be audited twice in parallel (once by hello server policy and once by hello database policy).</span></span>

   > [!NOTE]
   > <span data-ttu-id="e0460-126">Sunucu blob denetlenmesi ve veritabanı blob birlikte denetimi sürece etkinleştirme kaçınmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="e0460-126">You should avoid enabling both server blob auditing and database blob auditing together, unless:</span></span>
    > * <span data-ttu-id="e0460-127">Farklı bir toouse istediğiniz *depolama hesabı* veya *saklama dönemi* belirli bir veritabanı için.</span><span class="sxs-lookup"><span data-stu-id="e0460-127">You want toouse a different *storage account* or *retention period* for a specific database.</span></span>
    > * <span data-ttu-id="e0460-128">Olay türlerinden farklı belirli bir veritabanı veya hello sunucudaki hello veritabanları hello geri kalanı için denetlenen kategorileri için tooaudit olay türleri veya kategoriler istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="e0460-128">You want tooaudit event types or categories for a specific database that differ from event types or categories that are being audited for hello rest of hello databases on hello server.</span></span> <span data-ttu-id="e0460-129">Örneğin, yalnızca belirli bir veritabanı için denetlenen toobe gereken tablo ekler olabilir.</span><span class="sxs-lookup"><span data-stu-id="e0460-129">For example, you might have table inserts that need toobe audited only for a specific database.</span></span>
   > 
   > <span data-ttu-id="e0460-130">Aksi takdirde, yalnızca sunucu düzeyinde blob denetimi ve veritabanı düzeyinde hello tüm veritabanları için devre dışı bırak denetimi etkinleştirmeniz önerilir.</span><span class="sxs-lookup"><span data-stu-id="e0460-130">Otherwise, we recommended that you enable only server-level blob auditing and leave hello database-level auditing disabled for all databases.</span></span>


## <span data-ttu-id="e0460-131"><a id="subheading-2"></a>Veritabanınız için denetimi ayarlamanız</span><span class="sxs-lookup"><span data-stu-id="e0460-131"><a id="subheading-2"></a>Set up auditing for your database</span></span>
<span data-ttu-id="e0460-132">Merhaba aşağıdaki bölümde hello Azure portal kullanarak denetim hello yapılandırmasını açıklar.</span><span class="sxs-lookup"><span data-stu-id="e0460-132">hello following section describes hello configuration of auditing using hello Azure portal.</span></span>

1. <span data-ttu-id="e0460-133">Toohello Git [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e0460-133">Go toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e0460-134">Toohello Git **ayarları** hello tooaudit istediğiniz SQL veritabanı/SQL server dikey.</span><span class="sxs-lookup"><span data-stu-id="e0460-134">Go toohello **Settings** blade of hello SQL database/SQL server you want tooaudit.</span></span> <span data-ttu-id="e0460-135">Merhaba, **ayarları** dikey penceresinde, select **denetim ve tehdit algılama**.</span><span class="sxs-lookup"><span data-stu-id="e0460-135">In hello **Settings** blade, select **Auditing & Threat detection**.</span></span>

    <span data-ttu-id="e0460-136"><a id="auditing-screenshot"></a>![Gezinti Bölmesi][1]</span><span class="sxs-lookup"><span data-stu-id="e0460-136"><a id="auditing-screenshot"></a> ![Navigation pane][1]</span></span>
3. <span data-ttu-id="e0460-137">(Bu sunucuda tooall mevcut ve yeni oluşturulan veritabanları uygulanır) olan bir sunucu denetim ilkesi yukarı tooset tercih ederseniz, hello seçebilirsiniz **sunucu ayarlarını görüntüleyin** hello veritabanı denetim dikey penceresinde bağlantı.</span><span class="sxs-lookup"><span data-stu-id="e0460-137">If you prefer tooset up a server auditing policy (which will apply tooall existing and newly created databases on this server), you can select hello **View server settings** link in hello database auditing blade.</span></span> <span data-ttu-id="e0460-138">Daha sonra görüntülemek veya hello sunucu denetim ayarlarını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e0460-138">You can then view or modify hello server auditing settings.</span></span>

    ![Gezinti Bölmesi][2]
4. <span data-ttu-id="e0460-140">Tooenable hello veritabanı düzeyi (toplama tooor) sunucu düzeyinde denetimi yerine, blob denetimi için tercih ederseniz **denetim**seçin **ON**ve **türü denetimi** , seçin **Blob**.</span><span class="sxs-lookup"><span data-stu-id="e0460-140">If you prefer tooenable blob auditing on hello database level (in addition tooor instead of server-level auditing), for **Auditing**, select **ON**, and for **Auditing type**, select  **Blob**.</span></span>

    <span data-ttu-id="e0460-141">Sunucu blob denetimi etkinse hello veritabanı yapılandırılmış denetim hello sunucu blob denetim yan yana yer alır.</span><span class="sxs-lookup"><span data-stu-id="e0460-141">If server blob auditing is enabled, hello database-configured audit will exist side by side with hello server blob audit.</span></span>  

    ![Gezinti Bölmesi][3]
5. <span data-ttu-id="e0460-143">tooopen hello **denetim günlüklerini depolama** dikey penceresinde, select **depolama ayrıntıları**.</span><span class="sxs-lookup"><span data-stu-id="e0460-143">tooopen hello **Audit Logs Storage** blade, select **Storage Details**.</span></span> <span data-ttu-id="e0460-144">Burada günlükleri kaydedilecek ve hangi hello sonra eski günlükleri silinecek hello saklama dönemi ardından hello Azure depolama hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="e0460-144">Select hello Azure storage account where logs will be saved, and then select hello retention period, after which hello old logs will be deleted.</span></span> <span data-ttu-id="e0460-145">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e0460-145">Then click **OK**.</span></span> 
   >[!TIP] 
   ><span data-ttu-id="e0460-146">Merhaba Denetim raporları şablonları, kullanım dışı en tooget hello hello denetlenen tüm veritabanları için aynı depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="e0460-146">tooget hello most out of hello auditing reports templates, use hello same storage account for all audited databases.</span></span> 

    <span data-ttu-id="e0460-147"><a id="storage-screenshot"></a>![Gezinti Bölmesi][4]</span><span class="sxs-lookup"><span data-stu-id="e0460-147"><a id="storage-screenshot"></a> ![Navigation pane][4]</span></span>
6. <span data-ttu-id="e0460-148">Toocustomize denetlenen hello olayları istiyorsanız, bunu PowerShell ile yapmak veya REST API hello.</span><span class="sxs-lookup"><span data-stu-id="e0460-148">If you want toocustomize hello audited events, you can do this via PowerShell or hello REST API.</span></span> <span data-ttu-id="e0460-149">Daha fazla ayrıntı için bkz: Merhaba [Otomasyon (PowerShell/REST API'si)](#subheading-7) bölümü.</span><span class="sxs-lookup"><span data-stu-id="e0460-149">For more details, see hello [Automation (PowerShell/REST API)](#subheading-7) section.</span></span>
7. <span data-ttu-id="e0460-150">Denetim ayarlarını yapılandırdıktan sonra yeni tehdit algılama özelliğini hello açın ve e-postaları tooreceive güvenlik uyarılarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e0460-150">After you've configured your auditing settings, you can turn on hello new threat detection feature and configure emails tooreceive security alerts.</span></span> <span data-ttu-id="e0460-151">Tehdit algılama kullandığınızda, olası güvenlik tehditlerini gösteren anormal veritabanı etkinliklerini öngörülü uyarılar alırsınız.</span><span class="sxs-lookup"><span data-stu-id="e0460-151">When you use threat detection, you receive proactive alerts on anomalous database activities that can indicate potential security threats.</span></span> <span data-ttu-id="e0460-152">Daha fazla ayrıntı için bkz: [tehdit algılama ile çalışmaya başlama](sql-database-threat-detection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e0460-152">For more details, see [Getting started with threat detection](sql-database-threat-detection-get-started.md).</span></span>
8. <span data-ttu-id="e0460-153">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e0460-153">Click **Save**.</span></span>





## <span data-ttu-id="e0460-154"><a id="subheading-3"></a>Denetim günlüklerini ve raporları analiz eder.</span><span class="sxs-lookup"><span data-stu-id="e0460-154"><a id="subheading-3"></a>Analyze audit logs and reports</span></span>
<span data-ttu-id="e0460-155">Denetim günlüklerini hello Kurulum sırasında seçtiğiniz Azure depolama hesabında toplanır.</span><span class="sxs-lookup"><span data-stu-id="e0460-155">Audit logs are aggregated in hello Azure storage account you chose during setup.</span></span> <span data-ttu-id="e0460-156">Gibi bir araç kullanarak denetim günlüklerini keşfedebilirsiniz [Azure Storage Gezgini](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="e0460-156">You can explore audit logs by using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

<span data-ttu-id="e0460-157">BLOB denetim günlüklerini adlı bir kapsayıcı içindeki blob dosya koleksiyonu olarak kaydedilir **sqldbauditlogs**.</span><span class="sxs-lookup"><span data-stu-id="e0460-157">Blob auditing logs are saved as a collection of blob files within a container named **sqldbauditlogs**.</span></span>

<span data-ttu-id="e0460-158">Merhaba hello hiyerarşisini başlangıç blob denetim günlüklerini depolama klasörü, blob adlandırma kuralları ve günlük biçimi hakkında daha fazla ayrıntı için bkz: [Blob denetim günlük biçimi başvurusu (.docx dosya indirme)](https://go.microsoft.com/fwlink/?linkid=829599).</span><span class="sxs-lookup"><span data-stu-id="e0460-158">For further details about hello hierarchy of hello blob audit logs storage folder, blob naming conventions, and log format, see hello [Blob Audit Log Format Reference (.docx file download)](https://go.microsoft.com/fwlink/?linkid=829599).</span></span>

<span data-ttu-id="e0460-159">Günlükleri denetlemeyi tooview blob kullanabileceğiniz birkaç yöntem vardır:</span><span class="sxs-lookup"><span data-stu-id="e0460-159">There are several methods you can use tooview blob auditing logs:</span></span>

* <span data-ttu-id="e0460-160">Kullanım hello [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e0460-160">Use hello [Azure portal](https://portal.azure.com).</span></span>  <span data-ttu-id="e0460-161">Açık hello ilgili veritabanı.</span><span class="sxs-lookup"><span data-stu-id="e0460-161">Open hello relevant database.</span></span> <span data-ttu-id="e0460-162">Merhaba veritabanının AT hello üst **denetim ve tehdit algılama** dikey penceresinde tıklatın **denetim günlüklerini görüntüle**.</span><span class="sxs-lookup"><span data-stu-id="e0460-162">At hello top of hello database's **Auditing & Threat detection** blade, click **View audit logs**.</span></span>

    ![Gezinti Bölmesi][7]

    <span data-ttu-id="e0460-164">Bir **denetim kayıtları** içinden olmanız mümkün tooview hello günlükler dikey penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="e0460-164">An **Audit records** blade opens, from which you'll be able tooview hello logs.</span></span>

    - <span data-ttu-id="e0460-165">Belirli tarihleri tıklatarak görüntüleyebileceğiniz **filtre** hello hello üstündeki **denetim kayıtları** dikey.</span><span class="sxs-lookup"><span data-stu-id="e0460-165">You can view specific dates by clicking **Filter** at hello top of hello **Audit records** blade.</span></span>
    - <span data-ttu-id="e0460-166">Bir sunucu İlkesi veya veritabanı ilke denetimi tarafından oluşturulan denetim kayıtları arasında geçiş yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e0460-166">You can switch between audit records that were created by a server policy or database policy audit.</span></span>

       ![Gezinti Bölmesi][8]

* <span data-ttu-id="e0460-168">Merhaba sistem işlevi kullanın **sys.fn_get_audit_file** (T-SQL) tooreturn hello denetim günlüğü verilerini tablo biçiminde.</span><span class="sxs-lookup"><span data-stu-id="e0460-168">Use hello system function **sys.fn_get_audit_file** (T-SQL) tooreturn hello audit log data in tabular format.</span></span> <span data-ttu-id="e0460-169">Bu işlev kullanma hakkında daha fazla bilgi için bkz: Merhaba [sys.fn_get_audit_file belgelerine](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="e0460-169">For more information on using this function, see hello [sys.fn_get_audit_file documentation](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql).</span></span>


* <span data-ttu-id="e0460-170">Kullanım **denetim dosyaları birleştirme** SQL Server Management Studio'da (SSMS 17 ile başlayarak):</span><span class="sxs-lookup"><span data-stu-id="e0460-170">Use **Merge Audit Files** in SQL Server Management Studio (starting with SSMS 17):</span></span>  
    1. <span data-ttu-id="e0460-171">Merhaba SSMS menüsünden seçin **dosya** > **açık** > **denetim dosyaları birleştirme**.</span><span class="sxs-lookup"><span data-stu-id="e0460-171">From hello SSMS menu, select **File** > **Open** > **Merge Audit Files**.</span></span>

        ![Gezinti Bölmesi][9]
    2. <span data-ttu-id="e0460-173">Merhaba **denetim dosyaları Ekle** iletişim kutusu açılır.</span><span class="sxs-lookup"><span data-stu-id="e0460-173">hello **Add Audit Files** dialog box opens.</span></span> <span data-ttu-id="e0460-174">Merhaba birini seçin **Ekle** toomerge denetim bir yerel dosyaları olup olmadığını seçmek için seçenekler disk veya bunları Azure depolama alanından içeri aktarın (, gerekli tooprovide Azure Storage ayrıntılarını ve hesap anahtarı olacaktır).</span><span class="sxs-lookup"><span data-stu-id="e0460-174">Select one of hello **Add** options to choose whether toomerge audit files from a local disk or import them from Azure Storage (you will be required tooprovide your Azure Storage details and account key).</span></span>

    3. <span data-ttu-id="e0460-175">Tüm dosyaları toomerge eklendikten sonra tıklatın **Tamam** toocomplete hello birleştirme işlemi.</span><span class="sxs-lookup"><span data-stu-id="e0460-175">After all files toomerge have been added, click **OK** toocomplete hello merge operation.</span></span>

    4. <span data-ttu-id="e0460-176">Merhaba birleştirilmiş dosya burada görüntüleyebilir ve, isteğe bağlı olarak verme tooan XEL'e veya CSV dosyası veya tooa tablo hem analiz SSMS açılır.</span><span class="sxs-lookup"><span data-stu-id="e0460-176">hello merged file opens in SSMS, where you can view and analyze it, as well as export it tooan XEL or CSV file or tooa table.</span></span>

* <span data-ttu-id="e0460-177">Kullanım hello [eşitleme uygulama](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration) , oluşturduk.</span><span class="sxs-lookup"><span data-stu-id="e0460-177">Use hello [sync application](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration) that we have created.</span></span> <span data-ttu-id="e0460-178">Azure üzerinde çalışır ve Operations Management Suite (OMS) günlük analizi Genel API toopush SQL denetim günlüklerini OMS kullanır.</span><span class="sxs-lookup"><span data-stu-id="e0460-178">It runs in Azure and utilizes Operations Management Suite (OMS) Log Analytics public APIs toopush SQL audit logs into OMS.</span></span> <span data-ttu-id="e0460-179">Merhaba eşitleme uygulaması hello OMS günlük analizi Pano tüketimi için OMS günlük analizi SQL denetim günlüklerini iter.</span><span class="sxs-lookup"><span data-stu-id="e0460-179">hello sync application pushes SQL audit logs into OMS Log Analytics for consumption via hello OMS Log Analytics dashboard.</span></span> 

* <span data-ttu-id="e0460-180">Power BI kullanın.</span><span class="sxs-lookup"><span data-stu-id="e0460-180">Use Power BI.</span></span> <span data-ttu-id="e0460-181">Görüntülemek ve denetim günlüğü verilerini Power bı'da analiz edin.</span><span class="sxs-lookup"><span data-stu-id="e0460-181">You can view and analyze audit log data in Power BI.</span></span> <span data-ttu-id="e0460-182">Daha fazla bilgi edinmek [Power BI ve erişim indirilebilir bir şablon](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/).</span><span class="sxs-lookup"><span data-stu-id="e0460-182">Learn more about [Power BI, and access a downloadable template](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/).</span></span>

* <span data-ttu-id="e0460-183">Günlük dosyaları gibi bir araç kullanarak veya hello Portalı aracılığıyla Azure depolama blob kapsayıcısını indirin [Azure Storage Gezgini](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="e0460-183">Download log files from your Azure Storage blob container via hello portal or by using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).</span></span>
    * <span data-ttu-id="e0460-184">Bir günlük dosyası yerel olarak indirdikten sonra hello dosya tooopen çift tıklayarak görüntülemek ve SSMS içinde hello günlüklerini analiz edin.</span><span class="sxs-lookup"><span data-stu-id="e0460-184">After you have downloaded a log file locally, you can double-click hello file tooopen, view, and analyze hello logs in SSMS.</span></span>
    * <span data-ttu-id="e0460-185">Ayrıca, Azure Storage Gezgini ile aynı anda birden çok dosya indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e0460-185">You can also download multiple files simultaneously via Azure Storage Explorer.</span></span> <span data-ttu-id="e0460-186">Özel bir alt klasör (örneğin, belirli bir tarihteki tüm günlük dosyalarını içeren bir alt) sağ tıklayın ve **Farklı Kaydet** yerel bir klasörde toosave.</span><span class="sxs-lookup"><span data-stu-id="e0460-186">Right-click a specific subfolder (for example, a subfolder that includes all log files for a specific date) and select **Save as** toosave in a local folder.</span></span>

* <span data-ttu-id="e0460-187">Ek yöntemleri:</span><span class="sxs-lookup"><span data-stu-id="e0460-187">Additional methods:</span></span>
   * <span data-ttu-id="e0460-188">Pek çok dosya (veya hello önceki öğesi bu listede açıklandığı gibi tüm bir gün için günlük dosyalarını içeren bir alt klasörü) indirdikten sonra bunları yerel olarak daha önce açıklanan hello SSMS birleştirme Denetim dosyalarını yönergelerde açıklandığı gibi birleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e0460-188">After downloading several files (or a subfolder that includes log files for an entire day, as described in hello previous item in this list), you can merge them locally as described in hello SSMS Merge Audit Files instructions described earlier.</span></span>

   * <span data-ttu-id="e0460-189">Görünüm blob denetimi programlı olarak günlüğe kaydeder:</span><span class="sxs-lookup"><span data-stu-id="e0460-189">View blob auditing logs programmatically:</span></span>

     * <span data-ttu-id="e0460-190">Kullanım hello [genişletilmiş olaylar okuyucu](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/) C# Kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="e0460-190">Use hello [Extended Events Reader](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/) C# library.</span></span>
     * <span data-ttu-id="e0460-191">[Sorgu genişletilmiş olaylar dosyaları](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/) PowerShell kullanarak.</span><span class="sxs-lookup"><span data-stu-id="e0460-191">[Query Extended Events Files](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/) by using PowerShell.</span></span>




## <span data-ttu-id="e0460-192"><a id="subheading-5"></a>Üretim uygulamaları</span><span class="sxs-lookup"><span data-stu-id="e0460-192"><a id="subheading-5"></a>Production practices</span></span>
<!--hello description in this section refers toopreceding screen captures.-->

### <span data-ttu-id="e0460-193"><a id="subheading-6">Coğrafi olarak çoğaltılmış veritabanları denetleme</a></span><span class="sxs-lookup"><span data-stu-id="e0460-193"><a id="subheading-6">Auditing geo-replicated databases</a></span></span>
<span data-ttu-id="e0460-194">Coğrafi olarak çoğaltılmış veritabanları kullanırken hello birincil veritabanı, hello ikincil veritabanı ya da her ikisini de hello denetim türüne bağlı olarak denetim yukarı olası tooset olur.</span><span class="sxs-lookup"><span data-stu-id="e0460-194">When you use geo-replicated databases, it is possible tooset up auditing on either hello primary database, hello secondary database, or both, depending on hello audit type.</span></span>

<span data-ttu-id="e0460-195">(Blob denetimi açmak veya kapatmak denetim ayarları yalnızca hello birincil veritabanından açılabilir olduğunu unutmayın) bu yönergeleri izleyin:</span><span class="sxs-lookup"><span data-stu-id="e0460-195">Follow these instructions (remember that blob auditing can be turned on or off only from hello primary database auditing settings):</span></span>

* <span data-ttu-id="e0460-196">**Birincil veritabanı**.</span><span class="sxs-lookup"><span data-stu-id="e0460-196">**Primary database**.</span></span> <span data-ttu-id="e0460-197">BLOB, hello sunucusunda veya hello veritabanının kendisi, Denetim hello açıklandığı gibi açıldıktan [veritabanınız için denetimi ayarlamanız](#subheading-2) bölümü.</span><span class="sxs-lookup"><span data-stu-id="e0460-197">Turn on blob auditing, either on hello server or on hello database itself, as described in hello [Set up auditing for your database](#subheading-2) section.</span></span>
* <span data-ttu-id="e0460-198">**İkincil veritabanı**.</span><span class="sxs-lookup"><span data-stu-id="e0460-198">**Secondary database**.</span></span> <span data-ttu-id="e0460-199">Hello açıklandığı gibi hello birincil veritabanında BLOB denetim açıldıktan [veritabanınız için denetimi ayarlamanız](#subheading-2) bölümü.</span><span class="sxs-lookup"><span data-stu-id="e0460-199">Turn on blob auditing on hello primary database, as described in hello [Set up auditing for your database](#subheading-2) section.</span></span> 
   * <span data-ttu-id="e0460-200">BLOB denetimi üzerinde hello etkinleştirilmelidir *birincil veritabanının kendisi*, hello sunucusu değil.</span><span class="sxs-lookup"><span data-stu-id="e0460-200">Blob auditing must be enabled on hello *primary database itself*, not hello server.</span></span>
   * <span data-ttu-id="e0460-201">BLOB denetimi hello birincil veritabanında etkinleştirildikten sonra aynı zamanda hello ikincil veritabanı üzerinde etkin hale.</span><span class="sxs-lookup"><span data-stu-id="e0460-201">After blob auditing is enabled on hello primary database, it will also become enabled on hello secondary database.</span></span>

     >[!IMPORTANT]
     ><span data-ttu-id="e0460-202">Varsayılan olarak, hello ikincil veritabanının hello depolama ayarlarını hello birincil veritabanının aynı toothose çapraz bölge trafiği neden olur.</span><span class="sxs-lookup"><span data-stu-id="e0460-202">By default, hello storage settings for hello secondary database will be identical toothose of hello primary database, causing cross-regional traffic.</span></span> <span data-ttu-id="e0460-203">Bu blob hello ikincil sunucuda denetim ve yerel depolama hello ikincil sunucu depolama ayarlarında yapılandırma etkinleştirerek önleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e0460-203">You can avoid this by enabling blob auditing on hello secondary server and configuring local storage in hello secondary server storage settings.</span></span> <span data-ttu-id="e0460-204">Bu hello ikincil veritabanı ve denetim günlüklerini toolocal depolama alanı kaydetme her veritabanı sonucunda hello depolama konumu geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="e0460-204">This will override hello storage location for hello secondary database and result in each database saving its audit logs toolocal storage.</span></span>  
<br>

### <span data-ttu-id="e0460-205"><a id="subheading-6">Depolama anahtarını yeniden üretme</a></span><span class="sxs-lookup"><span data-stu-id="e0460-205"><a id="subheading-6">Storage key regeneration</a></span></span>
<span data-ttu-id="e0460-206">Üretimde, depolama alanınızın düzenli aralıklarla anahtarları büyük olasılıkla toorefresh demektir.</span><span class="sxs-lookup"><span data-stu-id="e0460-206">In production, you are likely toorefresh your storage keys periodically.</span></span> <span data-ttu-id="e0460-207">Anahtarlarınızı yenilerken tooresave hello Denetim İlkesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="e0460-207">When refreshing your keys, you need tooresave hello auditing policy.</span></span> <span data-ttu-id="e0460-208">Merhaba işlem aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="e0460-208">hello process is as follows:</span></span>

1. <span data-ttu-id="e0460-209">Açık hello **depolama ayrıntıları** dikey.</span><span class="sxs-lookup"><span data-stu-id="e0460-209">Open hello **Storage Details** blade.</span></span> <span data-ttu-id="e0460-210">Merhaba, **depolama erişim tuşu** kutusunda **ikincil**, tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="e0460-210">In hello **Storage Access Key** box, select **Secondary**, and click **OK**.</span></span> <span data-ttu-id="e0460-211">Ardından **kaydetmek** yapılandırma dikey penceresi denetim hello hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="e0460-211">Then click **Save** at hello top of hello auditing configuration blade.</span></span>

    ![Gezinti Bölmesi][5]
2. <span data-ttu-id="e0460-213">Toohello depolama yapılandırma dikey gidin ve hello birincil erişim anahtarını yeniden oluşturma.</span><span class="sxs-lookup"><span data-stu-id="e0460-213">Go toohello storage configuration blade and regenerate hello primary access key.</span></span>

    ![Gezinti Bölmesi][6]
3. <span data-ttu-id="e0460-215">Yapılandırma dikey penceresi denetim toohello geri dönün, geçiş hello depolama erişim ikincil tooprimary anahtarından ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="e0460-215">Go back toohello auditing configuration blade, switch hello storage access key from secondary tooprimary, and then click **OK**.</span></span> <span data-ttu-id="e0460-216">Ardından **kaydetmek** yapılandırma dikey penceresi denetim hello hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="e0460-216">Then click **Save** at hello top of hello auditing configuration blade.</span></span>
4. <span data-ttu-id="e0460-217">Toohello depolama yapılandırma dikey ve üretme hello ikincil erişim tuşu (Merhaba sonraki anahtarın yenileme döngüsü için hazırlık) geri dönün.</span><span class="sxs-lookup"><span data-stu-id="e0460-217">Go back toohello storage configuration blade and regenerate hello secondary access key (in preparation for hello next key's refresh cycle).</span></span>

## <span data-ttu-id="e0460-218"><a id="subheading-7"></a>Otomasyon (PowerShell/REST API)</span><span class="sxs-lookup"><span data-stu-id="e0460-218"><a id="subheading-7"></a>Automation (PowerShell/REST API)</span></span>
<span data-ttu-id="e0460-219">Otomasyon araçları aşağıdaki hello kullanarak Azure SQL veritabanı'nda denetim da yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e0460-219">You can also configure auditing in Azure SQL Database by using hello following automation tools:</span></span>

* <span data-ttu-id="e0460-220">**PowerShell cmdlet'leri**:</span><span class="sxs-lookup"><span data-stu-id="e0460-220">**PowerShell cmdlets**:</span></span>

   * <span data-ttu-id="e0460-221">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span><span class="sxs-lookup"><span data-stu-id="e0460-221">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span></span>
   * <span data-ttu-id="e0460-222">[Get-AzureRMSqlServerAuditingPolicy][102]</span><span class="sxs-lookup"><span data-stu-id="e0460-222">[Get-AzureRMSqlServerAuditingPolicy][102]</span></span>
   * <span data-ttu-id="e0460-223">[Remove-AzureRMSqlDatabaseAuditing][103]</span><span class="sxs-lookup"><span data-stu-id="e0460-223">[Remove-AzureRMSqlDatabaseAuditing][103]</span></span>
   * <span data-ttu-id="e0460-224">[Remove-AzureRMSqlServerAuditing][104]</span><span class="sxs-lookup"><span data-stu-id="e0460-224">[Remove-AzureRMSqlServerAuditing][104]</span></span>
   * <span data-ttu-id="e0460-225">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span><span class="sxs-lookup"><span data-stu-id="e0460-225">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span></span>
   * <span data-ttu-id="e0460-226">[Set-AzureRMSqlServerAuditingPolicy][106]</span><span class="sxs-lookup"><span data-stu-id="e0460-226">[Set-AzureRMSqlServerAuditingPolicy][106]</span></span>
   * <span data-ttu-id="e0460-227">[Kullanım AzureRMSqlServerAuditingPolicy][107]</span><span class="sxs-lookup"><span data-stu-id="e0460-227">[Use-AzureRMSqlServerAuditingPolicy][107]</span></span>

   <span data-ttu-id="e0460-228">Bir komut dosyası örneği için bkz: [denetim ve tehdit algılama PowerShell kullanarak yapılandırmanız](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e0460-228">For a script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span></span>

* <span data-ttu-id="e0460-229">**REST API - Blob denetimi**:</span><span class="sxs-lookup"><span data-stu-id="e0460-229">**REST API - Blob auditing**:</span></span>

   * [<span data-ttu-id="e0460-230">Denetim İlkesi veritabanı Blob güncelle</span><span class="sxs-lookup"><span data-stu-id="e0460-230">Create or Update Database Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt695939.aspx)
   * [<span data-ttu-id="e0460-231">Oluşturma veya güncelleştirme sunucusu Blob Denetim İlkesi</span><span class="sxs-lookup"><span data-stu-id="e0460-231">Create or Update Server Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt771861.aspx)
   * [<span data-ttu-id="e0460-232">Denetim İlkesi veritabanı Blob alma</span><span class="sxs-lookup"><span data-stu-id="e0460-232">Get Database Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt695938.aspx)
   * [<span data-ttu-id="e0460-233">Denetim İlkesi Sunucu Blob alma</span><span class="sxs-lookup"><span data-stu-id="e0460-233">Get Server Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt771860.aspx)
   * [<span data-ttu-id="e0460-234">İşlem sonucu denetim sunucu Blob alma</span><span class="sxs-lookup"><span data-stu-id="e0460-234">Get Server Blob Auditing Operation Result</span></span>](https://msdn.microsoft.com/library/azure/mt771862.aspx)


<!--Anchors-->
[Azure SQL Database Auditing overview]: #subheading-1
[Set up auditing for your database]: #subheading-2
[Analyze audit logs and reports]: #subheading-3
[Practices for usage in production]: #subheading-5
[Storage Key Regeneration]: #subheading-6
[Automation (PowerShell / REST API)]: #subheading-7
[Blob/Table differences in Server auditing policy inheritance]: (#subheading-8)  

<!--Image references-->
[1]: ./media/sql-database-auditing-get-started/1_auditing_get_started_settings.png
[2]: ./media/sql-database-auditing-get-started/2_auditing_get_started_server_inherit.png
[3]: ./media/sql-database-auditing-get-started/3_auditing_get_started_turn_on.png
[4]: ./media/sql-database-auditing-get-started/4_auditing_get_started_storage_details.png
[5]: ./media/sql-database-auditing-get-started/5_auditing_get_started_storage_key_regeneration.png
[6]: ./media/sql-database-auditing-get-started/6_auditing_get_started_regenerate_key.png
[7]: ./media/sql-database-auditing-get-started/7_auditing_get_started_blob_view_audit_logs.png
[8]: ./media/sql-database-auditing-get-started/8_auditing_get_started_blob_audit_records.png
[9]: ./media/sql-database-auditing-get-started/9_auditing_get_started_ssms_1.png
[10]: ./media/sql-database-auditing-get-started/10_auditing_get_started_ssms_2.png

[101]: /powershell/module/azurerm.sql/get-azurermsqldatabaseauditingpolicy
[102]: /powershell/module/azurerm.sql/Get-AzureRMSqlServerAuditingPolicy
[103]: /powershell/module/azurerm.sql/Remove-AzureRMSqlDatabaseAuditing
[104]: /powershell/module/azurerm.sql/Remove-AzureRMSqlServerAuditing
[105]: /powershell/module/azurerm.sql/Set-AzureRMSqlDatabaseAuditingPolicy
[106]: /powershell/module/azurerm.sql/Set-AzureRMSqlServerAuditingPolicy
[107]: /powershell/module/azurerm.sql/Use-AzureRMSqlServerAuditingPolicy
