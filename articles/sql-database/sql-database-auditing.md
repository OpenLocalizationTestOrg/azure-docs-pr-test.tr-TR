---
title: "Azure SQL veritabanı denetimi ile çalışmaya başlama | Microsoft Docs"
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
ms.openlocfilehash: f4324a59b5fa4c2e1ab5b1d7fc7e5fe986ea80f8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-sql-database-auditing"></a><span data-ttu-id="55ad3-103">SQL veritabanı denetimini kullanmaya başlayın</span><span class="sxs-lookup"><span data-stu-id="55ad3-103">Get started with SQL database auditing</span></span>
<span data-ttu-id="55ad3-104">Azure SQL veritabanı denetimi veritabanı olaylarını ve Azure depolama hesabınızdaki bunları Denetim günlüğüne yazar izler.</span><span class="sxs-lookup"><span data-stu-id="55ad3-104">Azure SQL database auditing tracks database events and writes them to an audit log in your Azure storage account.</span></span> <span data-ttu-id="55ad3-105">Ayrıca denetleme:</span><span class="sxs-lookup"><span data-stu-id="55ad3-105">Auditing also:</span></span>

* <span data-ttu-id="55ad3-106">Yönetmeliklere uygunluğu korumanıza, veritabanı etkinliklerini anlamanıza ve ifade eden tutarsızlıklar ve iş endişeleri veya güvenlik ihlalleri hakkında daha fazla bilgi kavramanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="55ad3-106">Helps you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

* <span data-ttu-id="55ad3-107">Etkinleştirir ve uyumluluk garanti etmez ancak Uyumluluk standartlara uyulması kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="55ad3-107">Enables and facilitates adherence to compliance standards, although it doesn't guarantee compliance.</span></span> <span data-ttu-id="55ad3-108">Bu destek standartları uyumluluğu Azure hakkında daha fazla bilgi programlar için bkz: [Azure Güven Merkezi](https://azure.microsoft.com/support/trust-center/compliance/).</span><span class="sxs-lookup"><span data-stu-id="55ad3-108">For more information about Azure programs that support standards compliance, see the [Azure Trust Center](https://azure.microsoft.com/support/trust-center/compliance/).</span></span>


## <span data-ttu-id="55ad3-109"><a id="subheading-1"></a>Genel Bakış denetim azure SQL veritabanı</span><span class="sxs-lookup"><span data-stu-id="55ad3-109"><a id="subheading-1"></a>Azure SQL database auditing overview</span></span>
<span data-ttu-id="55ad3-110">SQL veritabanı için denetimi kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="55ad3-110">You can use SQL database auditing to:</span></span>


* <span data-ttu-id="55ad3-111">**Korumak** seçili olayların bir denetim izi.</span><span class="sxs-lookup"><span data-stu-id="55ad3-111">**Retain** an audit trail of selected events.</span></span> <span data-ttu-id="55ad3-112">Denetlenecek veritabanı eylemleri kategorilerini tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="55ad3-112">You can define categories of database actions to be audited.</span></span>
* <span data-ttu-id="55ad3-113">**Rapor** veritabanı etkinlik.</span><span class="sxs-lookup"><span data-stu-id="55ad3-113">**Report** on database activity.</span></span> <span data-ttu-id="55ad3-114">Etkinlik ve olay Raporlama ile hızlı bir şekilde başlamak için önceden yapılandırılmış raporları ve panoyu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="55ad3-114">You can use preconfigured reports and a dashboard to get started quickly with activity and event reporting.</span></span>
* <span data-ttu-id="55ad3-115">**Analiz** raporlar.</span><span class="sxs-lookup"><span data-stu-id="55ad3-115">**Analyze** reports.</span></span> <span data-ttu-id="55ad3-116">Şüpheli olayları, olağan dışı etkinliği ve eğilimleri bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="55ad3-116">You can find suspicious events, unusual activity, and trends.</span></span>

<span data-ttu-id="55ad3-117">Farklı türlerde olay kategorisi için Denetim açıklandığı şekilde yapılandırabilirsiniz [veritabanınız için denetimi ayarlamanız](#subheading-2) bölümü.</span><span class="sxs-lookup"><span data-stu-id="55ad3-117">You can configure auditing for different types of event categories, as explained in the [Set up auditing for your database](#subheading-2) section.</span></span>

<span data-ttu-id="55ad3-118">Denetim günlükleri, Azure aboneliğinizde Azure Blob depolama alanına yazılır.</span><span class="sxs-lookup"><span data-stu-id="55ad3-118">Audit logs are written to Azure Blob storage on your Azure subscription.</span></span>


## <span data-ttu-id="55ad3-119"><a id="subheading-8"></a>Sunucu düzeyinde ve veritabanı düzeyi denetim ilkesi tanımlayın</span><span class="sxs-lookup"><span data-stu-id="55ad3-119"><a id="subheading-8"></a>Define server-level vs. database-level auditing policy</span></span>

<span data-ttu-id="55ad3-120">Bir denetim ilkesi, belirli bir veritabanı veya varsayılan sunucu ilkesi olarak tanımlanabilir:</span><span class="sxs-lookup"><span data-stu-id="55ad3-120">An auditing policy can be defined for a specific database or as a default server policy:</span></span>

* <span data-ttu-id="55ad3-121">Sunucudaki tüm mevcut ve yeni oluşturulan veritabanları için bir sunucu ilkesi uygulanır.</span><span class="sxs-lookup"><span data-stu-id="55ad3-121">A server policy applies to all existing and newly created databases on the server.</span></span>

* <span data-ttu-id="55ad3-122">Varsa *sunucu blob denetimi etkin*, onu *veritabanı için her zaman geçerli* (diğer bir deyişle, veritabanı denetlenmez), bağımsız olarak veritabanı denetim ayarları.</span><span class="sxs-lookup"><span data-stu-id="55ad3-122">If *server blob auditing is enabled*, it *always applies to the database* (that is, the database will be audited), regardless of the database auditing settings.</span></span>

* <span data-ttu-id="55ad3-123">Veritabanı üzerinde BLOB denetiminin etkinleştirilmesi, sunucu üzerinde etkinleştirmenin yanı sıra olur *değil* geçersiz kılabilir veya sunucu blob denetimi ayarlarından herhangi birini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="55ad3-123">Enabling blob auditing on the database, in addition to enabling it on the server, will *not* override or change any of the settings of the server blob auditing.</span></span> <span data-ttu-id="55ad3-124">Her iki denetimleri yan yana yer alır.</span><span class="sxs-lookup"><span data-stu-id="55ad3-124">Both audits will exist side by side.</span></span> <span data-ttu-id="55ad3-125">Diğer bir deyişle, veritabanı (kez sunucu İlkesi ve bir kez tarafından veritabanı İlkesi) iki kez paralel olarak denetlenecektir.</span><span class="sxs-lookup"><span data-stu-id="55ad3-125">In other words, the database will be audited twice in parallel (once by the server policy and once by the database policy).</span></span>

   > [!NOTE]
   > <span data-ttu-id="55ad3-126">Sunucu blob denetlenmesi ve veritabanı blob birlikte denetimi sürece etkinleştirme kaçınmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="55ad3-126">You should avoid enabling both server blob auditing and database blob auditing together, unless:</span></span>
    > * <span data-ttu-id="55ad3-127">Farklı bir kullanmak istediğiniz *depolama hesabı* veya *saklama dönemi* belirli bir veritabanı için.</span><span class="sxs-lookup"><span data-stu-id="55ad3-127">You want to use a different *storage account* or *retention period* for a specific database.</span></span>
    > * <span data-ttu-id="55ad3-128">Olay türlerini veya belirli bir veritabanı için olay türlerinden farklı kategorileri veya veritabanlarını sunucuda geri kalanı için denetlenen kategorileri denetlemek istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="55ad3-128">You want to audit event types or categories for a specific database that differ from event types or categories that are being audited for the rest of the databases on the server.</span></span> <span data-ttu-id="55ad3-129">Örneğin, yalnızca belirli bir veritabanı için denetlenmesi gereken tablo ekler olabilir.</span><span class="sxs-lookup"><span data-stu-id="55ad3-129">For example, you might have table inserts that need to be audited only for a specific database.</span></span>
   > 
   > <span data-ttu-id="55ad3-130">Aksi takdirde, yalnızca sunucu düzeyinde blob denetlemeyi etkinleştirme ve devre dışı tüm veritabanları için veritabanı düzeyinde denetimi bırakın önerilir.</span><span class="sxs-lookup"><span data-stu-id="55ad3-130">Otherwise, we recommended that you enable only server-level blob auditing and leave the database-level auditing disabled for all databases.</span></span>


## <span data-ttu-id="55ad3-131"><a id="subheading-2"></a>Veritabanınız için denetimi ayarlamanız</span><span class="sxs-lookup"><span data-stu-id="55ad3-131"><a id="subheading-2"></a>Set up auditing for your database</span></span>
<span data-ttu-id="55ad3-132">Aşağıdaki bölümde denetim Azure Portalı'nı kullanarak yapılandırmayı açıklar.</span><span class="sxs-lookup"><span data-stu-id="55ad3-132">The following section describes the configuration of auditing using the Azure portal.</span></span>

1. <span data-ttu-id="55ad3-133">[Azure Portal](https://portal.azure.com) gidin.</span><span class="sxs-lookup"><span data-stu-id="55ad3-133">Go to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="55ad3-134">Git **ayarları** denetlemek istediğiniz SQL veritabanı/SQL server'ın dikey.</span><span class="sxs-lookup"><span data-stu-id="55ad3-134">Go to the **Settings** blade of the SQL database/SQL server you want to audit.</span></span> <span data-ttu-id="55ad3-135">İçinde **ayarları** dikey penceresinde, select **denetim ve tehdit algılama**.</span><span class="sxs-lookup"><span data-stu-id="55ad3-135">In the **Settings** blade, select **Auditing & Threat detection**.</span></span>

    <span data-ttu-id="55ad3-136"><a id="auditing-screenshot"></a>![Gezinti Bölmesi][1]</span><span class="sxs-lookup"><span data-stu-id="55ad3-136"><a id="auditing-screenshot"></a> ![Navigation pane][1]</span></span>
3. <span data-ttu-id="55ad3-137">(Bu sunucudaki tüm mevcut ve yeni oluşturulan veritabanları için uygulanır) bir sunucu denetim ilkesini ayarlamak tercih ederseniz, seçebileceğiniz **sunucu ayarlarını görüntüleyin** veritabanı denetim dikey penceresinde bağlantı.</span><span class="sxs-lookup"><span data-stu-id="55ad3-137">If you prefer to set up a server auditing policy (which will apply to all existing and newly created databases on this server), you can select the **View server settings** link in the database auditing blade.</span></span> <span data-ttu-id="55ad3-138">Daha sonra görüntülemek veya sunucunun denetim ayarları değiştirin.</span><span class="sxs-lookup"><span data-stu-id="55ad3-138">You can then view or modify the server auditing settings.</span></span>

    ![Gezinti Bölmesi][2]
4. <span data-ttu-id="55ad3-140">İçin veritabanı düzeyinde (ek olarak veya sunucu düzeyinde denetimi yerine), blob denetimi etkinleştirmeyi tercih ediyorsanız **denetim**seçin **ON**ve **türü denetimi**, seçin **Blob**.</span><span class="sxs-lookup"><span data-stu-id="55ad3-140">If you prefer to enable blob auditing on the database level (in addition to or instead of server-level auditing), for **Auditing**, select **ON**, and for **Auditing type**, select  **Blob**.</span></span>

    <span data-ttu-id="55ad3-141">Sunucu blob denetimi etkinse, veritabanı yapılandırılmış denetim yan yana sunucu blob denetim yer alır.</span><span class="sxs-lookup"><span data-stu-id="55ad3-141">If server blob auditing is enabled, the database-configured audit will exist side by side with the server blob audit.</span></span>  

    ![Gezinti Bölmesi][3]
5. <span data-ttu-id="55ad3-143">Açmak için **denetim günlüklerini depolama** dikey penceresinde, select **depolama ayrıntıları**.</span><span class="sxs-lookup"><span data-stu-id="55ad3-143">To open the **Audit Logs Storage** blade, select **Storage Details**.</span></span> <span data-ttu-id="55ad3-144">Burada günlükleri kaydedilecek ve sonra eski günlükleri silinecek saklama dönemi, ardından Azure depolama hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="55ad3-144">Select the Azure storage account where logs will be saved, and then select the retention period, after which the old logs will be deleted.</span></span> <span data-ttu-id="55ad3-145">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="55ad3-145">Then click **OK**.</span></span> 
   >[!TIP] 
   ><span data-ttu-id="55ad3-146">En iyi denetim raporları şablonları almak için denetlenen tüm veritabanları için aynı depolama hesabı kullanın.</span><span class="sxs-lookup"><span data-stu-id="55ad3-146">To get the most out of the auditing reports templates, use the same storage account for all audited databases.</span></span> 

    <span data-ttu-id="55ad3-147"><a id="storage-screenshot"></a>![Gezinti Bölmesi][4]</span><span class="sxs-lookup"><span data-stu-id="55ad3-147"><a id="storage-screenshot"></a> ![Navigation pane][4]</span></span>
6. <span data-ttu-id="55ad3-148">Denetlenen olayları özelleştirmek istiyorsanız, PowerShell veya REST API bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="55ad3-148">If you want to customize the audited events, you can do this via PowerShell or the REST API.</span></span> <span data-ttu-id="55ad3-149">Daha fazla ayrıntı için bkz: [Otomasyon (PowerShell/REST API'si)](#subheading-7) bölümü.</span><span class="sxs-lookup"><span data-stu-id="55ad3-149">For more details, see the [Automation (PowerShell/REST API)](#subheading-7) section.</span></span>
7. <span data-ttu-id="55ad3-150">Denetim ayarlarını yapılandırdıktan sonra yeni tehdit algılama özelliğini açmak ve güvenlik uyarıları almak için e-postaları yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="55ad3-150">After you've configured your auditing settings, you can turn on the new threat detection feature and configure emails to receive security alerts.</span></span> <span data-ttu-id="55ad3-151">Tehdit algılama kullandığınızda, olası güvenlik tehditlerini gösteren anormal veritabanı etkinliklerini öngörülü uyarılar alırsınız.</span><span class="sxs-lookup"><span data-stu-id="55ad3-151">When you use threat detection, you receive proactive alerts on anomalous database activities that can indicate potential security threats.</span></span> <span data-ttu-id="55ad3-152">Daha fazla ayrıntı için bkz: [tehdit algılama ile çalışmaya başlama](sql-database-threat-detection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="55ad3-152">For more details, see [Getting started with threat detection](sql-database-threat-detection-get-started.md).</span></span>
8. <span data-ttu-id="55ad3-153">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="55ad3-153">Click **Save**.</span></span>





## <span data-ttu-id="55ad3-154"><a id="subheading-3"></a>Denetim günlüklerini ve raporları analiz eder.</span><span class="sxs-lookup"><span data-stu-id="55ad3-154"><a id="subheading-3"></a>Analyze audit logs and reports</span></span>
<span data-ttu-id="55ad3-155">Denetim günlükleri, Kurulum sırasında seçtiğiniz Azure depolama hesabında toplanır.</span><span class="sxs-lookup"><span data-stu-id="55ad3-155">Audit logs are aggregated in the Azure storage account you chose during setup.</span></span> <span data-ttu-id="55ad3-156">Gibi bir araç kullanarak denetim günlüklerini keşfedebilirsiniz [Azure Storage Gezgini](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="55ad3-156">You can explore audit logs by using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

<span data-ttu-id="55ad3-157">BLOB denetim günlüklerini adlı bir kapsayıcı içindeki blob dosya koleksiyonu olarak kaydedilir **sqldbauditlogs**.</span><span class="sxs-lookup"><span data-stu-id="55ad3-157">Blob auditing logs are saved as a collection of blob files within a container named **sqldbauditlogs**.</span></span>

<span data-ttu-id="55ad3-158">Hiyerarşi blob denetim günlüklerini depolama klasörü, blob adlandırma kuralları ve günlük biçimi hakkında daha fazla ayrıntı için bkz: [Blob denetim günlük biçimi başvurusu (.docx dosya indirme)](https://go.microsoft.com/fwlink/?linkid=829599).</span><span class="sxs-lookup"><span data-stu-id="55ad3-158">For further details about the hierarchy of the blob audit logs storage folder, blob naming conventions, and log format, see the [Blob Audit Log Format Reference (.docx file download)](https://go.microsoft.com/fwlink/?linkid=829599).</span></span>

<span data-ttu-id="55ad3-159">Blob denetim günlüklerini görüntülemek için kullanabileceğiniz birkaç yöntem vardır:</span><span class="sxs-lookup"><span data-stu-id="55ad3-159">There are several methods you can use to view blob auditing logs:</span></span>

* <span data-ttu-id="55ad3-160">Kullanım [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="55ad3-160">Use the [Azure portal](https://portal.azure.com).</span></span>  <span data-ttu-id="55ad3-161">İlgili veritabanını açın.</span><span class="sxs-lookup"><span data-stu-id="55ad3-161">Open the relevant database.</span></span> <span data-ttu-id="55ad3-162">Veritabanının üstündeki **denetim ve tehdit algılama** dikey penceresinde tıklatın **denetim günlüklerini görüntüle**.</span><span class="sxs-lookup"><span data-stu-id="55ad3-162">At the top of the database's **Auditing & Threat detection** blade, click **View audit logs**.</span></span>

    ![Gezinti Bölmesi][7]

    <span data-ttu-id="55ad3-164">Bir **denetim kayıtları** dikey penceresi açılır ve kendisinden, günlükleri görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="55ad3-164">An **Audit records** blade opens, from which you'll be able to view the logs.</span></span>

    - <span data-ttu-id="55ad3-165">Belirli tarihleri tıklatarak görüntüleyebileceğiniz **filtre** en üstündeki **denetim kayıtları** dikey.</span><span class="sxs-lookup"><span data-stu-id="55ad3-165">You can view specific dates by clicking **Filter** at the top of the **Audit records** blade.</span></span>
    - <span data-ttu-id="55ad3-166">Bir sunucu İlkesi veya veritabanı ilke denetimi tarafından oluşturulan denetim kayıtları arasında geçiş yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="55ad3-166">You can switch between audit records that were created by a server policy or database policy audit.</span></span>

       ![Gezinti Bölmesi][8]

* <span data-ttu-id="55ad3-168">Bir sistem işlevi kullanın **sys.fn_get_audit_file** (Denetim günlüğü verilerini tablo biçiminde döndürmek için T-SQL).</span><span class="sxs-lookup"><span data-stu-id="55ad3-168">Use the system function **sys.fn_get_audit_file** (T-SQL) to return the audit log data in tabular format.</span></span> <span data-ttu-id="55ad3-169">Bu işlev kullanma hakkında daha fazla bilgi için bkz: [sys.fn_get_audit_file belgelerine](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="55ad3-169">For more information on using this function, see the [sys.fn_get_audit_file documentation](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql).</span></span>


* <span data-ttu-id="55ad3-170">Kullanım **denetim dosyaları birleştirme** SQL Server Management Studio'da (SSMS 17 ile başlayarak):</span><span class="sxs-lookup"><span data-stu-id="55ad3-170">Use **Merge Audit Files** in SQL Server Management Studio (starting with SSMS 17):</span></span>  
    1. <span data-ttu-id="55ad3-171">SSMS menüsünden seçin **dosya** > **açık** > **denetim dosyaları birleştirme**.</span><span class="sxs-lookup"><span data-stu-id="55ad3-171">From the SSMS menu, select **File** > **Open** > **Merge Audit Files**.</span></span>

        ![Gezinti Bölmesi][9]
    2. <span data-ttu-id="55ad3-173">**Denetim dosyaları Ekle** iletişim kutusu açılır.</span><span class="sxs-lookup"><span data-stu-id="55ad3-173">The **Add Audit Files** dialog box opens.</span></span> <span data-ttu-id="55ad3-174">Aşağıdakilerden birini seçin **Ekle** Seçenekleri denetim dosyalarını yerel bir sürücüden birleştirme ya da Azure (size gerekecek Azure Storage ayrıntıları ve hesap anahtarı sağlamak) depolama biriminden almak isteyip istemediğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="55ad3-174">Select one of the **Add** options to choose whether to merge audit files from a local disk or import them from Azure Storage (you will be required to provide your Azure Storage details and account key).</span></span>

    3. <span data-ttu-id="55ad3-175">Birleştirme için tüm dosyaları ekledikten sonra tıklatın **Tamam** birleştirme işlemini tamamlamak için.</span><span class="sxs-lookup"><span data-stu-id="55ad3-175">After all files to merge have been added, click **OK** to complete the merge operation.</span></span>

    4. <span data-ttu-id="55ad3-176">Burada, görüntülemek ve analiz edin, yanı sıra bir XEL'e ya da CSV dosyası veya tablo dışa SSMS birleştirilmiş dosya açılır.</span><span class="sxs-lookup"><span data-stu-id="55ad3-176">The merged file opens in SSMS, where you can view and analyze it, as well as export it to an XEL or CSV file or to a table.</span></span>

* <span data-ttu-id="55ad3-177">Kullanım [eşitleme uygulama](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration) , oluşturduk.</span><span class="sxs-lookup"><span data-stu-id="55ad3-177">Use the [sync application](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration) that we have created.</span></span> <span data-ttu-id="55ad3-178">Azure üzerinde çalışır ve Operations Management Suite (OMS) SQL denetim günlüklerini OMS göndermek için günlük analizi genel API'leri kullanır.</span><span class="sxs-lookup"><span data-stu-id="55ad3-178">It runs in Azure and utilizes Operations Management Suite (OMS) Log Analytics public APIs to push SQL audit logs into OMS.</span></span> <span data-ttu-id="55ad3-179">Eşitleme uygulamanın OMS günlük analizi Pano tüketimi için OMS günlük analizi SQL denetim günlüklerini iter.</span><span class="sxs-lookup"><span data-stu-id="55ad3-179">The sync application pushes SQL audit logs into OMS Log Analytics for consumption via the OMS Log Analytics dashboard.</span></span> 

* <span data-ttu-id="55ad3-180">Power BI kullanın.</span><span class="sxs-lookup"><span data-stu-id="55ad3-180">Use Power BI.</span></span> <span data-ttu-id="55ad3-181">Görüntülemek ve denetim günlüğü verilerini Power bı'da analiz edin.</span><span class="sxs-lookup"><span data-stu-id="55ad3-181">You can view and analyze audit log data in Power BI.</span></span> <span data-ttu-id="55ad3-182">Daha fazla bilgi edinmek [Power BI ve erişim indirilebilir bir şablon](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/).</span><span class="sxs-lookup"><span data-stu-id="55ad3-182">Learn more about [Power BI, and access a downloadable template](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/).</span></span>

* <span data-ttu-id="55ad3-183">Günlük dosyaları gibi bir araç kullanarak veya Portalı aracılığıyla Azure depolama blob kapsayıcısını indirin [Azure Storage Gezgini](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="55ad3-183">Download log files from your Azure Storage blob container via the portal or by using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).</span></span>
    * <span data-ttu-id="55ad3-184">Bir günlük dosyası yerel olarak indirdikten sonra açın, görüntülemek ve SSMS'ndeki günlükleri çözümlemek için dosyayı çift tıklayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="55ad3-184">After you have downloaded a log file locally, you can double-click the file to open, view, and analyze the logs in SSMS.</span></span>
    * <span data-ttu-id="55ad3-185">Ayrıca, Azure Storage Gezgini ile aynı anda birden çok dosya indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="55ad3-185">You can also download multiple files simultaneously via Azure Storage Explorer.</span></span> <span data-ttu-id="55ad3-186">Özel bir alt klasör (örneğin, belirli bir tarihteki tüm günlük dosyalarını içeren bir alt) sağ tıklayın ve **Farklı Kaydet** içinde yerel bir klasöre kaydeder.</span><span class="sxs-lookup"><span data-stu-id="55ad3-186">Right-click a specific subfolder (for example, a subfolder that includes all log files for a specific date) and select **Save as** to save in a local folder.</span></span>

* <span data-ttu-id="55ad3-187">Ek yöntemleri:</span><span class="sxs-lookup"><span data-stu-id="55ad3-187">Additional methods:</span></span>
   * <span data-ttu-id="55ad3-188">Pek çok dosya (veya önceki öğeyi bu listede açıklandığı gibi tüm bir gün için günlük dosyalarını içeren bir alt klasörü) indirdikten sonra bunları yerel olarak daha önce açıklanan SSMS birleştirme Denetim dosyalarını yönergelerde açıklandığı gibi birleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="55ad3-188">After downloading several files (or a subfolder that includes log files for an entire day, as described in the previous item in this list), you can merge them locally as described in the SSMS Merge Audit Files instructions described earlier.</span></span>

   * <span data-ttu-id="55ad3-189">Görünüm blob denetimi programlı olarak günlüğe kaydeder:</span><span class="sxs-lookup"><span data-stu-id="55ad3-189">View blob auditing logs programmatically:</span></span>

     * <span data-ttu-id="55ad3-190">Kullanım [genişletilmiş olaylar okuyucu](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/) C# Kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="55ad3-190">Use the [Extended Events Reader](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/) C# library.</span></span>
     * <span data-ttu-id="55ad3-191">[Sorgu genişletilmiş olaylar dosyaları](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/) PowerShell kullanarak.</span><span class="sxs-lookup"><span data-stu-id="55ad3-191">[Query Extended Events Files](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/) by using PowerShell.</span></span>




## <span data-ttu-id="55ad3-192"><a id="subheading-5"></a>Üretim uygulamaları</span><span class="sxs-lookup"><span data-stu-id="55ad3-192"><a id="subheading-5"></a>Production practices</span></span>
<!--The description in this section refers to preceding screen captures.-->

### <span data-ttu-id="55ad3-193"><a id="subheading-6">Coğrafi olarak çoğaltılmış veritabanları denetleme</a></span><span class="sxs-lookup"><span data-stu-id="55ad3-193"><a id="subheading-6">Auditing geo-replicated databases</a></span></span>
<span data-ttu-id="55ad3-194">Coğrafi olarak çoğaltılmış veritabanları kullandığınızda, birincil veritabanı, ikincil veritabanı ya da her ikisini de denetim türüne bağlı olarak denetimini ayarlamak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="55ad3-194">When you use geo-replicated databases, it is possible to set up auditing on either the primary database, the secondary database, or both, depending on the audit type.</span></span>

<span data-ttu-id="55ad3-195">(Blob denetimi açmak veya kapatmak denetim ayarları yalnızca birincil veritabanından açılabilir olduğunu unutmayın) bu yönergeleri izleyin:</span><span class="sxs-lookup"><span data-stu-id="55ad3-195">Follow these instructions (remember that blob auditing can be turned on or off only from the primary database auditing settings):</span></span>

* <span data-ttu-id="55ad3-196">**Birincil veritabanı**.</span><span class="sxs-lookup"><span data-stu-id="55ad3-196">**Primary database**.</span></span> <span data-ttu-id="55ad3-197">BLOB, sunucuda veya veritabanının kendisi, Denetim açıklandığı gibi açıldıktan [veritabanınız için denetimi ayarlamanız](#subheading-2) bölümü.</span><span class="sxs-lookup"><span data-stu-id="55ad3-197">Turn on blob auditing, either on the server or on the database itself, as described in the [Set up auditing for your database](#subheading-2) section.</span></span>
* <span data-ttu-id="55ad3-198">**İkincil veritabanı**.</span><span class="sxs-lookup"><span data-stu-id="55ad3-198">**Secondary database**.</span></span> <span data-ttu-id="55ad3-199">Bölümünde açıklandığı gibi birincil veritabanında BLOB denetim açıldıktan [veritabanınız için denetimi ayarlamanız](#subheading-2) bölümü.</span><span class="sxs-lookup"><span data-stu-id="55ad3-199">Turn on blob auditing on the primary database, as described in the [Set up auditing for your database](#subheading-2) section.</span></span> 
   * <span data-ttu-id="55ad3-200">Üzerinde BLOB denetimi etkinleştirilmelidir *birincil veritabanının kendisi*, sunucu değil.</span><span class="sxs-lookup"><span data-stu-id="55ad3-200">Blob auditing must be enabled on the *primary database itself*, not the server.</span></span>
   * <span data-ttu-id="55ad3-201">BLOB denetimi birincil veritabanında etkinleştirildikten sonra aynı zamanda ikincil veritabanı etkin hale.</span><span class="sxs-lookup"><span data-stu-id="55ad3-201">After blob auditing is enabled on the primary database, it will also become enabled on the secondary database.</span></span>

     >[!IMPORTANT]
     ><span data-ttu-id="55ad3-202">Varsayılan olarak, ikincil veritabanı için depolama ayarlarını çapraz bölge trafiği neden bu birincil veritabanının aynı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="55ad3-202">By default, the storage settings for the secondary database will be identical to those of the primary database, causing cross-regional traffic.</span></span> <span data-ttu-id="55ad3-203">Bu ikincil sunucuda blob denetimi ve yerel depolama için ikincil sunucu depolama ayarlarında yapılandırma etkinleştirerek önleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="55ad3-203">You can avoid this by enabling blob auditing on the secondary server and configuring local storage in the secondary server storage settings.</span></span> <span data-ttu-id="55ad3-204">Bu ikincil veritabanı ve denetim günlüklerinin yerel depolama alanına kaydediliyor her veritabanı sonucunda için depolama konumu geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="55ad3-204">This will override the storage location for the secondary database and result in each database saving its audit logs to local storage.</span></span>  
<br>

### <span data-ttu-id="55ad3-205"><a id="subheading-6">Depolama anahtarını yeniden üretme</a></span><span class="sxs-lookup"><span data-stu-id="55ad3-205"><a id="subheading-6">Storage key regeneration</a></span></span>
<span data-ttu-id="55ad3-206">Üretimde büyük bir olasılıkla depolama anahtarlarınızı düzenli aralıklarla yenileyin.</span><span class="sxs-lookup"><span data-stu-id="55ad3-206">In production, you are likely to refresh your storage keys periodically.</span></span> <span data-ttu-id="55ad3-207">Anahtarlarınızı yenilerken denetim ilkesi yeniden kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="55ad3-207">When refreshing your keys, you need to resave the auditing policy.</span></span> <span data-ttu-id="55ad3-208">İşlem aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="55ad3-208">The process is as follows:</span></span>

1. <span data-ttu-id="55ad3-209">Açık **depolama ayrıntıları** dikey.</span><span class="sxs-lookup"><span data-stu-id="55ad3-209">Open the **Storage Details** blade.</span></span> <span data-ttu-id="55ad3-210">İçinde **depolama erişim tuşu** kutusunda **ikincil**, tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="55ad3-210">In the **Storage Access Key** box, select **Secondary**, and click **OK**.</span></span> <span data-ttu-id="55ad3-211">Ardından **kaydetmek** denetim yapılandırma dikey pencerenin üstündeki.</span><span class="sxs-lookup"><span data-stu-id="55ad3-211">Then click **Save** at the top of the auditing configuration blade.</span></span>

    ![Gezinti Bölmesi][5]
2. <span data-ttu-id="55ad3-213">Depolama yapılandırma dikey penceresine gidin ve birincil erişim anahtarını yeniden oluşturma.</span><span class="sxs-lookup"><span data-stu-id="55ad3-213">Go to the storage configuration blade and regenerate the primary access key.</span></span>

    ![Gezinti Bölmesi][6]
3. <span data-ttu-id="55ad3-215">Birincil ikincil depolama erişim anahtarı yeniden denetim yapılandırma dikey penceresine, anahtar ve ardından Git **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="55ad3-215">Go back to the auditing configuration blade, switch the storage access key from secondary to primary, and then click **OK**.</span></span> <span data-ttu-id="55ad3-216">Ardından **kaydetmek** denetim yapılandırma dikey pencerenin üstündeki.</span><span class="sxs-lookup"><span data-stu-id="55ad3-216">Then click **Save** at the top of the auditing configuration blade.</span></span>
4. <span data-ttu-id="55ad3-217">Depolama yapılandırma dikey penceresine geri dönün ve (için Hazırlanmakta sonraki anahtarın yenileme döngüsü) ikincil erişim anahtarını yeniden oluşturma.</span><span class="sxs-lookup"><span data-stu-id="55ad3-217">Go back to the storage configuration blade and regenerate the secondary access key (in preparation for the next key's refresh cycle).</span></span>

## <span data-ttu-id="55ad3-218"><a id="subheading-7"></a>Otomasyon (PowerShell/REST API)</span><span class="sxs-lookup"><span data-stu-id="55ad3-218"><a id="subheading-7"></a>Automation (PowerShell/REST API)</span></span>
<span data-ttu-id="55ad3-219">Azure SQL veritabanı'nda aşağıdaki Otomasyon araçları kullanarak denetim da yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="55ad3-219">You can also configure auditing in Azure SQL Database by using the following automation tools:</span></span>

* <span data-ttu-id="55ad3-220">**PowerShell cmdlet'leri**:</span><span class="sxs-lookup"><span data-stu-id="55ad3-220">**PowerShell cmdlets**:</span></span>

   * <span data-ttu-id="55ad3-221">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span><span class="sxs-lookup"><span data-stu-id="55ad3-221">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span></span>
   * <span data-ttu-id="55ad3-222">[Get-AzureRMSqlServerAuditingPolicy][102]</span><span class="sxs-lookup"><span data-stu-id="55ad3-222">[Get-AzureRMSqlServerAuditingPolicy][102]</span></span>
   * <span data-ttu-id="55ad3-223">[Remove-AzureRMSqlDatabaseAuditing][103]</span><span class="sxs-lookup"><span data-stu-id="55ad3-223">[Remove-AzureRMSqlDatabaseAuditing][103]</span></span>
   * <span data-ttu-id="55ad3-224">[Remove-AzureRMSqlServerAuditing][104]</span><span class="sxs-lookup"><span data-stu-id="55ad3-224">[Remove-AzureRMSqlServerAuditing][104]</span></span>
   * <span data-ttu-id="55ad3-225">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span><span class="sxs-lookup"><span data-stu-id="55ad3-225">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span></span>
   * <span data-ttu-id="55ad3-226">[Set-AzureRMSqlServerAuditingPolicy][106]</span><span class="sxs-lookup"><span data-stu-id="55ad3-226">[Set-AzureRMSqlServerAuditingPolicy][106]</span></span>
   * <span data-ttu-id="55ad3-227">[Kullanım AzureRMSqlServerAuditingPolicy][107]</span><span class="sxs-lookup"><span data-stu-id="55ad3-227">[Use-AzureRMSqlServerAuditingPolicy][107]</span></span>

   <span data-ttu-id="55ad3-228">Bir komut dosyası örneği için bkz: [denetim ve tehdit algılama PowerShell kullanarak yapılandırmanız](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="55ad3-228">For a script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span></span>

* <span data-ttu-id="55ad3-229">**REST API - Blob denetimi**:</span><span class="sxs-lookup"><span data-stu-id="55ad3-229">**REST API - Blob auditing**:</span></span>

   * [<span data-ttu-id="55ad3-230">Denetim İlkesi veritabanı Blob güncelle</span><span class="sxs-lookup"><span data-stu-id="55ad3-230">Create or Update Database Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt695939.aspx)
   * [<span data-ttu-id="55ad3-231">Oluşturma veya güncelleştirme sunucusu Blob Denetim İlkesi</span><span class="sxs-lookup"><span data-stu-id="55ad3-231">Create or Update Server Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt771861.aspx)
   * [<span data-ttu-id="55ad3-232">Denetim İlkesi veritabanı Blob alma</span><span class="sxs-lookup"><span data-stu-id="55ad3-232">Get Database Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt695938.aspx)
   * [<span data-ttu-id="55ad3-233">Denetim İlkesi Sunucu Blob alma</span><span class="sxs-lookup"><span data-stu-id="55ad3-233">Get Server Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt771860.aspx)
   * [<span data-ttu-id="55ad3-234">İşlem sonucu denetim sunucu Blob alma</span><span class="sxs-lookup"><span data-stu-id="55ad3-234">Get Server Blob Auditing Operation Result</span></span>](https://msdn.microsoft.com/library/azure/mt771862.aspx)


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
