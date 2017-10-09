---
title: "Azure SQL veritabanlarının aaaManage grupları | Microsoft Docs"
description: "Oluşturulması ve esnek bir iş yönetimi yol."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: f858344d-085b-4022-935e-1b5fa20adbac
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: a73c4fb24c332fae0e917c18272724cccd56f29a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-scaled-out-azure-sql-databases-using-elastic-jobs-preview"></a><span data-ttu-id="8ef6b-103">Oluşturma ve esnek işleri (Önizleme) kullanarak Azure SQL veritabanlarını ölçeklendirilmiş yönetme</span><span class="sxs-lookup"><span data-stu-id="8ef6b-103">Create and manage scaled out Azure SQL Databases using elastic jobs (preview)</span></span>


<span data-ttu-id="8ef6b-104">**Esnek veritabanı iş** şema değişiklikleri, kimlik bilgileri yönetimi, başvuru veri güncelleştirmeleri, performans verileri toplama veya Kiracı (müşteri) telemetri koleksiyonu gibi yönetim işlemlerini yürüterek veritabanlarının gruplarının yönetimi kolaylaştırabilir.</span><span class="sxs-lookup"><span data-stu-id="8ef6b-104">**Elastic Database jobs** simplify management of groups of databases by executing administrative operations such as schema changes, credentials management, reference data updates, performance data collection or tenant (customer) telemetry collection.</span></span> <span data-ttu-id="8ef6b-105">Esnek veritabanı iş hello Azure portal ve PowerShell cmdlet'leri aracılığıyla şu anda mevcut değil.</span><span class="sxs-lookup"><span data-stu-id="8ef6b-105">Elastic Database jobs is currently available through hello Azure portal and PowerShell cmdlets.</span></span> <span data-ttu-id="8ef6b-106">Ancak, tüm veritabanları arasında tooexecution hello Azure portal yüzeyleri işlevsellik sınırlı bir [esnek havuz (Önizleme)](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="8ef6b-106">However, hello Azure portal surfaces reduced functionality limited tooexecution across all databases in an [elastic pool (preview)](sql-database-elastic-pool.md).</span></span> <span data-ttu-id="8ef6b-107">tooaccess ek özellikleri ve bir grubu özel tanımlı bir koleksiyon veya bir parça dahil olmak üzere veritabanları arasında betiklerinin yürütülmesi ayarlayın (kullanılarak oluşturulan [esnek veritabanı istemci Kitaplığı](sql-database-elastic-scale-introduction.md)), bkz: [oluşturma ve yönetme PowerShell kullanarak işleri](sql-database-elastic-jobs-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="8ef6b-107">tooaccess additional features and execution of scripts across a group of databases including a custom-defined collection or a shard set (created using [Elastic Database client library](sql-database-elastic-scale-introduction.md)), see [Creating and managing jobs using PowerShell](sql-database-elastic-jobs-powershell.md).</span></span> <span data-ttu-id="8ef6b-108">İşleri hakkında daha fazla bilgi için bkz: [esnek veritabanı işleri genel bakış](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8ef6b-108">For more information about jobs, see [Elastic Database jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="8ef6b-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8ef6b-109">Prerequisites</span></span>
* <span data-ttu-id="8ef6b-110">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="8ef6b-110">An Azure subscription.</span></span> <span data-ttu-id="8ef6b-111">Ücretsiz deneme için bkz: [ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8ef6b-111">For a free trial, see [Free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="8ef6b-112">Bir esnek havuz.</span><span class="sxs-lookup"><span data-stu-id="8ef6b-112">An elastic pool.</span></span> <span data-ttu-id="8ef6b-113">Bkz: [esnek havuzları hakkında](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="8ef6b-113">See [About elastic pools](sql-database-elastic-pool.md).</span></span>
* <span data-ttu-id="8ef6b-114">Esnek veritabanı iş hizmet bileşenlerini yükleme.</span><span class="sxs-lookup"><span data-stu-id="8ef6b-114">Installation of elastic database job service components.</span></span> <span data-ttu-id="8ef6b-115">Bkz: [hello esnek veritabanı iş hizmetini yükleme](sql-database-elastic-jobs-service-installation.md).</span><span class="sxs-lookup"><span data-stu-id="8ef6b-115">See [Installing hello elastic database job service](sql-database-elastic-jobs-service-installation.md).</span></span>

## <a name="creating-jobs"></a><span data-ttu-id="8ef6b-116">İşleri oluşturuluyor</span><span class="sxs-lookup"><span data-stu-id="8ef6b-116">Creating jobs</span></span>
1. <span data-ttu-id="8ef6b-117">Hello kullanarak [Azure portal](https://portal.azure.com), var olan bir esnek veritabanı iş havuzundan tıklatın **oluşturma işi**.</span><span class="sxs-lookup"><span data-stu-id="8ef6b-117">Using hello [Azure portal](https://portal.azure.com), from an existing elastic database job pool, click **Create job**.</span></span>
2. <span data-ttu-id="8ef6b-118">Hello kullanıcı adı ve parolayı (işleri yükleme sırasında oluşturulan) hello veritabanı yöneticisinin hello işleri denetim veritabanı (meta veri depolama alanı işleri için) yazın.</span><span class="sxs-lookup"><span data-stu-id="8ef6b-118">Type in hello username and password of hello database administrator (created at installation of Jobs) for hello jobs control database (metadata storage for jobs).</span></span>
   
    ![Merhaba iş adı yazın veya kodda yapıştırın ve Çalıştır'ı tıklatın][1]
3. <span data-ttu-id="8ef6b-120">Merhaba, **işi oluştur** dikey penceresinde hello işi için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="8ef6b-120">In hello **Create Job** blade, type a name for hello job.</span></span>
4. <span data-ttu-id="8ef6b-121">Merhaba kullanıcı adı ve parola tooconnect toohello hedef veritabanları komut dosyası yürütme toosucceed için yeterli izinlere sahip yazın.</span><span class="sxs-lookup"><span data-stu-id="8ef6b-121">Type hello user name and password tooconnect toohello target databases with sufficient permissions for script execution toosucceed.</span></span>
5. <span data-ttu-id="8ef6b-122">Merhaba T-SQL komut dosyası yazın veya yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="8ef6b-122">Paste or type in hello T-SQL script.</span></span>
6. <span data-ttu-id="8ef6b-123">Tıklatın **kaydetmek** ve ardından **çalıştırmak**.</span><span class="sxs-lookup"><span data-stu-id="8ef6b-123">Click **Save** and then click **Run**.</span></span>
   
    ![İşleri oluşturma ve çalıştırma][5]

## <a name="run-idempotent-jobs"></a><span data-ttu-id="8ef6b-125">Idempotent işleri çalıştırma</span><span class="sxs-lookup"><span data-stu-id="8ef6b-125">Run idempotent jobs</span></span>
<span data-ttu-id="8ef6b-126">Bir veritabanları kümesi karşı bir komut çalıştırdığınızda, hello betik ıdempotent olduğundan emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8ef6b-126">When you run a script against a set of databases, you must be sure that hello script is idempotent.</span></span> <span data-ttu-id="8ef6b-127">Diğer bir deyişle, onu önce tamamlanmamış bir durumda başarısız olmuş olsa bile hello betik birden çok kez mümkün toorun olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8ef6b-127">That is, hello script must be able toorun multiple times, even if it has failed before in an incomplete state.</span></span> <span data-ttu-id="8ef6b-128">Bir komut dosyası başarısız olduğunda, başarılı olana dek gibi hello iş otomatik olarak yeniden denenecek (sınırlarda hello yeniden deneme mantığı sonunda hello yeniden deneniyor olmaz).</span><span class="sxs-lookup"><span data-stu-id="8ef6b-128">For example, when a script fails, hello job will be automatically retried until it succeeds (within limits, as hello retry logic will eventually cease hello retrying).</span></span> <span data-ttu-id="8ef6b-129">Merhaba yolu toodo bu toouse hello bir "IF var" yan tümcesi ve yeni bir nesne oluşturmadan önce bulunan örnek silin.</span><span class="sxs-lookup"><span data-stu-id="8ef6b-129">hello way toodo this is toouse hello an "IF EXISTS" clause and delete any found instance before creating a new object.</span></span> <span data-ttu-id="8ef6b-130">Örneği burada gösterilir:</span><span class="sxs-lookup"><span data-stu-id="8ef6b-130">An example is shown here:</span></span>

    IF EXISTS (SELECT name FROM sys.indexes
            WHERE name = N'IX_ProductVendor_VendorID')
    DROP INDEX IX_ProductVendor_VendorID ON Purchasing.ProductVendor;
    GO
    CREATE INDEX IX_ProductVendor_VendorID
    ON Purchasing.ProductVendor (VendorID);

<span data-ttu-id="8ef6b-131">Alternatif olarak, yeni bir örneğini oluşturmadan önce bir "IF değil var" yan tümcesi kullanın:</span><span class="sxs-lookup"><span data-stu-id="8ef6b-131">Alternatively, use an "IF NOT EXISTS" clause before creating a new instance:</span></span>

    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
     CREATE TABLE TestTable(
      TestTableId INT PRIMARY KEY IDENTITY,
      InsertionTime DATETIME2
     );
    END
    GO

    INSERT INTO TestTable(InsertionTime) VALUES (sysutcdatetime());
    GO

<span data-ttu-id="8ef6b-132">Bu komut dosyası ardından daha önce oluşturduğunuz hello tablosunu güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="8ef6b-132">This script then updates hello table created previously.</span></span>

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN

    ALTER TABLE TestTable

    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO


## <a name="checking-job-status"></a><span data-ttu-id="8ef6b-133">İş durumunu denetleme</span><span class="sxs-lookup"><span data-stu-id="8ef6b-133">Checking job status</span></span>
<span data-ttu-id="8ef6b-134">Bir işi başladıktan sonra üzerinde ilerleme durumunu denetleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8ef6b-134">After a job has begun, you can check on its progress.</span></span>

1. <span data-ttu-id="8ef6b-135">Merhaba esnek havuz sayfasından tıklatın **yönetmek işleri**.</span><span class="sxs-lookup"><span data-stu-id="8ef6b-135">From hello elastic pool page, click **Manage jobs**.</span></span>
   
    !["Yönet projeler"'i tıklatın][2]
2. <span data-ttu-id="8ef6b-137">Merhaba adına bir işin (a) tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8ef6b-137">Click on hello name (a) of a job.</span></span> <span data-ttu-id="8ef6b-138">Merhaba **durum** "Tamamlandı" veya "Başarısız" olabilir</span><span class="sxs-lookup"><span data-stu-id="8ef6b-138">hello **STATUS** can be "Completed" or "Failed."</span></span> <span data-ttu-id="8ef6b-139">Merhaba işin ayrıntılarına (b), tarih ve saati oluşturma ve çalıştırma görünür.</span><span class="sxs-lookup"><span data-stu-id="8ef6b-139">hello job's details appear (b) with its date and time of creation and running.</span></span> <span data-ttu-id="8ef6b-140">Tarih ve saat ayrıntılarını vermiş hello havuzundaki her veritabanında hello betik hello ilerlemesini gösterir hello aşağıda Hello listesi (c).</span><span class="sxs-lookup"><span data-stu-id="8ef6b-140">hello list (c) below hello that shows hello progress of hello script against each database in hello pool, giving its date and time details.</span></span>
   
    ![Tamamlanmış iş denetleniyor][3]

## <a name="checking-failed-jobs"></a><span data-ttu-id="8ef6b-142">İşlerini denetimi başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="8ef6b-142">Checking failed jobs</span></span>
<span data-ttu-id="8ef6b-143">Bir işi başarısız olursa, yürütme günlüğü bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="8ef6b-143">If a job fails, a log of its execution can found.</span></span> <span data-ttu-id="8ef6b-144">Ayrıntılarını hello başarısız işi toosee Hello adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8ef6b-144">Click hello name of hello failed job toosee its details.</span></span>

![Başarısız işi denetleyin][4]

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-create-and-manage/screen-1.png
[2]: ./media/sql-database-elastic-jobs-create-and-manage/click-manage-jobs.png
[3]: ./media/sql-database-elastic-jobs-create-and-manage/running-jobs.png
[4]: ./media/sql-database-elastic-jobs-create-and-manage/failed.png
[5]: ./media/sql-database-elastic-jobs-create-and-manage/screen-2.png


