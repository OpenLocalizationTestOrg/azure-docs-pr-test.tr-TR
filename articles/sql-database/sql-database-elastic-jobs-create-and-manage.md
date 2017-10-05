---
title: "Azure SQL veritabanlarının gruplarını yönetme | Microsoft Docs"
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
ms.openlocfilehash: d30cc74778e0b36dd632c2f040ce80d1ca8af5a5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-scaled-out-azure-sql-databases-using-elastic-jobs-preview"></a><span data-ttu-id="cebde-103">Oluşturma ve esnek işleri (Önizleme) kullanarak Azure SQL veritabanlarını ölçeklendirilmiş yönetme</span><span class="sxs-lookup"><span data-stu-id="cebde-103">Create and manage scaled out Azure SQL Databases using elastic jobs (preview)</span></span>


<span data-ttu-id="cebde-104">**Esnek veritabanı iş** şema değişiklikleri, kimlik bilgileri yönetimi, başvuru veri güncelleştirmeleri, performans verileri toplama veya Kiracı (müşteri) telemetri koleksiyonu gibi yönetim işlemlerini yürüterek veritabanlarının gruplarının yönetimi kolaylaştırabilir.</span><span class="sxs-lookup"><span data-stu-id="cebde-104">**Elastic Database jobs** simplify management of groups of databases by executing administrative operations such as schema changes, credentials management, reference data updates, performance data collection or tenant (customer) telemetry collection.</span></span> <span data-ttu-id="cebde-105">Esnek veritabanı iş PowerShell cmdlet'leri ve Azure portal şu anda mevcut değil.</span><span class="sxs-lookup"><span data-stu-id="cebde-105">Elastic Database jobs is currently available through the Azure portal and PowerShell cmdlets.</span></span> <span data-ttu-id="cebde-106">Ancak, Azure portal yüzeyleri tüm veritabanları arasında yürütme için sınırlı işlevsellik sınırlı bir [esnek havuz (Önizleme)](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="cebde-106">However, the Azure portal surfaces reduced functionality limited to execution across all databases in an [elastic pool (preview)](sql-database-elastic-pool.md).</span></span> <span data-ttu-id="cebde-107">Ek özellikler ve betiklerinin yürütülmesi özel tanımlı bir koleksiyon veya bir parça dahil olmak üzere veritabanları grubu erişmek için (kullanılarak oluşturulan [esnek veritabanı istemci Kitaplığı](sql-database-elastic-scale-introduction.md)), bkz: [oluşturma ve PowerShell kullanarak işleri yönetme](sql-database-elastic-jobs-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="cebde-107">To access additional features and execution of scripts across a group of databases including a custom-defined collection or a shard set (created using [Elastic Database client library](sql-database-elastic-scale-introduction.md)), see [Creating and managing jobs using PowerShell](sql-database-elastic-jobs-powershell.md).</span></span> <span data-ttu-id="cebde-108">İşleri hakkında daha fazla bilgi için bkz: [esnek veritabanı işleri genel bakış](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cebde-108">For more information about jobs, see [Elastic Database jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="cebde-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="cebde-109">Prerequisites</span></span>
* <span data-ttu-id="cebde-110">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="cebde-110">An Azure subscription.</span></span> <span data-ttu-id="cebde-111">Ücretsiz deneme için bkz: [ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cebde-111">For a free trial, see [Free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="cebde-112">Bir esnek havuz.</span><span class="sxs-lookup"><span data-stu-id="cebde-112">An elastic pool.</span></span> <span data-ttu-id="cebde-113">Bkz: [esnek havuzları hakkında](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="cebde-113">See [About elastic pools](sql-database-elastic-pool.md).</span></span>
* <span data-ttu-id="cebde-114">Esnek veritabanı iş hizmet bileşenlerini yükleme.</span><span class="sxs-lookup"><span data-stu-id="cebde-114">Installation of elastic database job service components.</span></span> <span data-ttu-id="cebde-115">Bkz: [esnek veritabanı iş hizmetini yükleme](sql-database-elastic-jobs-service-installation.md).</span><span class="sxs-lookup"><span data-stu-id="cebde-115">See [Installing the elastic database job service](sql-database-elastic-jobs-service-installation.md).</span></span>

## <a name="creating-jobs"></a><span data-ttu-id="cebde-116">İşleri oluşturuluyor</span><span class="sxs-lookup"><span data-stu-id="cebde-116">Creating jobs</span></span>
1. <span data-ttu-id="cebde-117">Kullanarak [Azure portal](https://portal.azure.com), var olan bir esnek veritabanı iş havuzundan tıklatın **oluşturma işi**.</span><span class="sxs-lookup"><span data-stu-id="cebde-117">Using the [Azure portal](https://portal.azure.com), from an existing elastic database job pool, click **Create job**.</span></span>
2. <span data-ttu-id="cebde-118">Kullanıcı adı ve parolayı (işleri yükleme sırasında oluşturulan) veritabanı yöneticisi, iş kontrol veritabanına (meta veri depolama alanı işleri için) yazın.</span><span class="sxs-lookup"><span data-stu-id="cebde-118">Type in the username and password of the database administrator (created at installation of Jobs) for the jobs control database (metadata storage for jobs).</span></span>
   
    ![İş adı yazın veya kodda yapıştırın ve Çalıştır'ı tıklatın][1]
3. <span data-ttu-id="cebde-120">İçinde **işi oluştur** dikey penceresinde, iş için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="cebde-120">In the **Create Job** blade, type a name for the job.</span></span>
4. <span data-ttu-id="cebde-121">Betik yürütme işleminin başarılı olması yeterli izinlere sahip hedef veritabanlarına bağlanmak için parola ve kullanıcı adını yazın.</span><span class="sxs-lookup"><span data-stu-id="cebde-121">Type the user name and password to connect to the target databases with sufficient permissions for script execution to succeed.</span></span>
5. <span data-ttu-id="cebde-122">T-SQL betiği yazın veya yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="cebde-122">Paste or type in the T-SQL script.</span></span>
6. <span data-ttu-id="cebde-123">Tıklatın **kaydetmek** ve ardından **çalıştırmak**.</span><span class="sxs-lookup"><span data-stu-id="cebde-123">Click **Save** and then click **Run**.</span></span>
   
    ![İşleri oluşturma ve çalıştırma][5]

## <a name="run-idempotent-jobs"></a><span data-ttu-id="cebde-125">Idempotent işleri çalıştırma</span><span class="sxs-lookup"><span data-stu-id="cebde-125">Run idempotent jobs</span></span>
<span data-ttu-id="cebde-126">Bir veritabanları kümesi karşı bir komut çalıştırdığınızda, komut dosyası ıdempotent olduğundan emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="cebde-126">When you run a script against a set of databases, you must be sure that the script is idempotent.</span></span> <span data-ttu-id="cebde-127">Diğer bir deyişle, onu önce tamamlanmamış bir durumda başarısız olmuş olsa bile komut dosyası birden çok kez çalıştırmanız mümkün olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="cebde-127">That is, the script must be able to run multiple times, even if it has failed before in an incomplete state.</span></span> <span data-ttu-id="cebde-128">Bir komut dosyası başarısız olduğunda, başarılı olana dek Örneğin, iş otomatik olarak yeniden denenecek (sınırlarda yeniden deneme mantığı sonunda yeniden deneniyor olmaz).</span><span class="sxs-lookup"><span data-stu-id="cebde-128">For example, when a script fails, the job will be automatically retried until it succeeds (within limits, as the retry logic will eventually cease the retrying).</span></span> <span data-ttu-id="cebde-129">Bunu yapmanın yolu kullanmaktır bir "IF var" yan tümcesi ve yeni bir nesne oluşturmadan önce bulunan örnek silin.</span><span class="sxs-lookup"><span data-stu-id="cebde-129">The way to do this is to use the an "IF EXISTS" clause and delete any found instance before creating a new object.</span></span> <span data-ttu-id="cebde-130">Örneği burada gösterilir:</span><span class="sxs-lookup"><span data-stu-id="cebde-130">An example is shown here:</span></span>

    IF EXISTS (SELECT name FROM sys.indexes
            WHERE name = N'IX_ProductVendor_VendorID')
    DROP INDEX IX_ProductVendor_VendorID ON Purchasing.ProductVendor;
    GO
    CREATE INDEX IX_ProductVendor_VendorID
    ON Purchasing.ProductVendor (VendorID);

<span data-ttu-id="cebde-131">Alternatif olarak, yeni bir örneğini oluşturmadan önce bir "IF değil var" yan tümcesi kullanın:</span><span class="sxs-lookup"><span data-stu-id="cebde-131">Alternatively, use an "IF NOT EXISTS" clause before creating a new instance:</span></span>

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

<span data-ttu-id="cebde-132">Bu komut dosyası ardından daha önce oluşturduğunuz tablosunu güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="cebde-132">This script then updates the table created previously.</span></span>

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN

    ALTER TABLE TestTable

    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO


## <a name="checking-job-status"></a><span data-ttu-id="cebde-133">İş durumunu denetleme</span><span class="sxs-lookup"><span data-stu-id="cebde-133">Checking job status</span></span>
<span data-ttu-id="cebde-134">Bir işi başladıktan sonra üzerinde ilerleme durumunu denetleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cebde-134">After a job has begun, you can check on its progress.</span></span>

1. <span data-ttu-id="cebde-135">Esnek havuz sayfasından tıklatın **yönetmek işleri**.</span><span class="sxs-lookup"><span data-stu-id="cebde-135">From the elastic pool page, click **Manage jobs**.</span></span>
   
    !["Yönet projeler"'i tıklatın][2]
2. <span data-ttu-id="cebde-137">Adına bir işin (a) tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cebde-137">Click on the name (a) of a job.</span></span> <span data-ttu-id="cebde-138">**Durum** "Tamamlandı" veya "Başarısız" olabilir</span><span class="sxs-lookup"><span data-stu-id="cebde-138">The **STATUS** can be "Completed" or "Failed."</span></span> <span data-ttu-id="cebde-139">İş ayrıntıları, tarih ve saati oluşturma ve çalıştırma (b) görünür.</span><span class="sxs-lookup"><span data-stu-id="cebde-139">The job's details appear (b) with its date and time of creation and running.</span></span> <span data-ttu-id="cebde-140">, Aşağıdaki listeden (c), tarih ve saat ayrıntılarını vermiş havuzunda her veritabanında betik ilerlemesini gösterir.</span><span class="sxs-lookup"><span data-stu-id="cebde-140">The list (c) below the that shows the progress of the script against each database in the pool, giving its date and time details.</span></span>
   
    ![Tamamlanmış iş denetleniyor][3]

## <a name="checking-failed-jobs"></a><span data-ttu-id="cebde-142">İşlerini denetimi başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="cebde-142">Checking failed jobs</span></span>
<span data-ttu-id="cebde-143">Bir işi başarısız olursa, yürütme günlüğü bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="cebde-143">If a job fails, a log of its execution can found.</span></span> <span data-ttu-id="cebde-144">Ayrıntılarını görmek için başarısız iş adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cebde-144">Click the name of the failed job to see its details.</span></span>

![Başarısız işi denetleyin][4]

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-create-and-manage/screen-1.png
[2]: ./media/sql-database-elastic-jobs-create-and-manage/click-manage-jobs.png
[3]: ./media/sql-database-elastic-jobs-create-and-manage/running-jobs.png
[4]: ./media/sql-database-elastic-jobs-create-and-manage/failed.png
[5]: ./media/sql-database-elastic-jobs-create-and-manage/screen-2.png


