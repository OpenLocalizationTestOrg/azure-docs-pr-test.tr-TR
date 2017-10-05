---
title: Verileri SQL Server'dan Azure SQL Data warehouse'a (bcp) | Microsoft Docs
description: "Küçük boyutlu veriler söz konusu olduğunda SQL Server'dan düz dosyalara veri aktarmak ve verileri doğrudan Azure SQL Data Warehouse'a aktarmak için bcp yardımcı programını kullanın."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: f87d8d7c-8276-43c5-90e7-d4ccc0e3a224
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: dae7b5f7456f4ec0daf60d55f9c38b780896ff83
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-flat-files"></a><span data-ttu-id="16b1b-103">SQL Server'dan Azure SQL Data Warehouse'a veri yükleme (düz dosyalar)</span><span class="sxs-lookup"><span data-stu-id="16b1b-103">Load data from SQL Server into Azure SQL Data Warehouse (flat files)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="16b1b-104">SSIS</span><span class="sxs-lookup"><span data-stu-id="16b1b-104">SSIS</span></span>](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [<span data-ttu-id="16b1b-105">PolyBase</span><span class="sxs-lookup"><span data-stu-id="16b1b-105">PolyBase</span></span>](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [<span data-ttu-id="16b1b-106">bcp</span><span class="sxs-lookup"><span data-stu-id="16b1b-106">bcp</span></span>](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

<span data-ttu-id="16b1b-107">Küçük veri kümeleri söz konusu olduğunda SQL Server'dan veri aktarmak ve doğrudan Azure SQL Data Warehouse'a yüklemek için bcp komut satırı yardımcı programını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="16b1b-107">For small data sets, you can use the bcp command-line utility to export data from SQL Server and then load it directly to Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="16b1b-108">Bu öğreticide bcp'yi kullanarak şunları yapacaksınız:</span><span class="sxs-lookup"><span data-stu-id="16b1b-108">In this tutorial, you will use bcp to:</span></span>

* <span data-ttu-id="16b1b-109">bcp out komutunu kullanarak SQL Server'daki bir tabloyu dışarı aktarma (veya basit bir örnek dosya oluşturma)</span><span class="sxs-lookup"><span data-stu-id="16b1b-109">Export a table from from SQL Server by using the bcp out command (or create a simple sample file)</span></span>
* <span data-ttu-id="16b1b-110">Tabloyu bir düz dosyadan SQL Data Warehouse'a aktarın.</span><span class="sxs-lookup"><span data-stu-id="16b1b-110">Import the table from a flat file to SQL Data Warehouse.</span></span>
* <span data-ttu-id="16b1b-111">Yüklenen verilere ilişkin istatistikler oluşturun.</span><span class="sxs-lookup"><span data-stu-id="16b1b-111">Create statistics on the loaded data.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="16b1b-112">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="16b1b-112">Before you begin</span></span>
### <a name="prerequisites"></a><span data-ttu-id="16b1b-113">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="16b1b-113">Prerequisites</span></span>
<span data-ttu-id="16b1b-114">Bu öğreticide ilerleyebilmeniz için şunlar gereklidir:</span><span class="sxs-lookup"><span data-stu-id="16b1b-114">To step through this tutorial, you need:</span></span>

* <span data-ttu-id="16b1b-115">SQL Data Warehouse veritabanı</span><span class="sxs-lookup"><span data-stu-id="16b1b-115">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="16b1b-116">bcp komut satırı yardımcı programının yüklü olması</span><span class="sxs-lookup"><span data-stu-id="16b1b-116">The bcp command-line utility installed</span></span>
* <span data-ttu-id="16b1b-117">sqlcmd komut satırı yardımcı programının yüklü olması</span><span class="sxs-lookup"><span data-stu-id="16b1b-117">The sqlcmd command-line utility installed</span></span>

<span data-ttu-id="16b1b-118">bcp ve sqlcmd yardımcı programlarını [Microsoft İndirme Merkezi][Microsoft Download Center]'nden indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="16b1b-118">You can download the bcp and sqlcmd utilities from the [Microsoft Download Center][Microsoft Download Center].</span></span>

### <a name="data-in-ascii-or-utf-16-format"></a><span data-ttu-id="16b1b-119">ASCII veya UTF-16 biçimindeki veriler</span><span class="sxs-lookup"><span data-stu-id="16b1b-119">Data in ASCII or UTF-16 format</span></span>
<span data-ttu-id="16b1b-120">UTF-8 biçimi bcp tarafından desteklenmediğinden, bu öğreticiyi kendi verilerinizle deniyorsanız verilerinizin ASCII veya UTF-16 kodlamasını kullanıyor olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="16b1b-120">If you are trying this tutorial with your own data, your data needs to use the ASCII or UTF-16 encoding since bcp does not support UTF-8.</span></span> 

<span data-ttu-id="16b1b-121">PolyBase UTF-8'i destekler ancak henüz UTF-16'yi desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="16b1b-121">PolyBase supports UTF-8 but doesn't yet support UTF-16.</span></span> <span data-ttu-id="16b1b-122">bcp ve PolyBase'i birleştirmek istiyorsanız verileri SQL Server'dan dışarı aktardıktan sonra UTF-8 biçimine dönüştürmeniz gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="16b1b-122">Note that if you want to combine bcp with PolyBase you will need to transform the data to UTF-8 after it is exported from SQL Server.</span></span> 

## <a name="1-create-a-destination-table"></a><span data-ttu-id="16b1b-123">1. Hedef tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="16b1b-123">1. Create a destination table</span></span>
<span data-ttu-id="16b1b-124">SQL Data Warehouse'da daha sonra yükleme için hedef tablo olacak bir tablo tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="16b1b-124">Define a table in SQL Data Warehouse that will be the destination table for the load.</span></span> <span data-ttu-id="16b1b-125">Tablodaki sütunlar, veri dosyanızın tüm satırlarındaki verilere karşılık gelmelidir.</span><span class="sxs-lookup"><span data-stu-id="16b1b-125">The columns in the table must correspond to the data in each row of your data file.</span></span>

<span data-ttu-id="16b1b-126">Tablo oluşturmak için bir komut istemi açın ve sqlcmd.exe dosyasını kullanarak şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="16b1b-126">To create a table, open a command prompt and use sqlcmd.exe to run the following command:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    CREATE TABLE DimDate2
    (
        DateId INT NOT NULL,
        CalendarQuarter TINYINT NOT NULL,
        FiscalQuarter TINYINT NOT NULL
    )
    WITH
    (
        CLUSTERED COLUMNSTORE INDEX,
        DISTRIBUTION = ROUND_ROBIN
    );
"
```


## <a name="2-create-a-source-data-file"></a><span data-ttu-id="16b1b-127">2. Kaynak veri dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="16b1b-127">2. Create a source data file</span></span>
<span data-ttu-id="16b1b-128">Not Defteri'ni açın ve yeni bir metin dosyasına aşağıdaki veri satırlarını kopyalayıp dosyayı yerel geçici dizininize (C:\Temp\DimDate2.txt) kaydedin.</span><span class="sxs-lookup"><span data-stu-id="16b1b-128">Open Notepad and copy the following lines of data into a new text file and then save this file to your local temp directory, C:\Temp\DimDate2.txt.</span></span> <span data-ttu-id="16b1b-129">Bu veri ASCII biçimindedir.</span><span class="sxs-lookup"><span data-stu-id="16b1b-129">This data is in ASCII format.</span></span>

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

<span data-ttu-id="16b1b-130">(İsteğe bağlı) SQL Server veritabanından kendi verilerinizi dışarı aktarmak için bir komut istemi açın ve aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="16b1b-130">(Optional) To export your own data from a SQL Server database, open a command prompt and run the following command.</span></span> <span data-ttu-id="16b1b-131">TableName (Tablo Adı), ServerName (Sunucu Adı), DatabaseName (Veritabanı Adı), Username (Kullanıcı Adı) ve Password (Parola) alanlarına kendi bilgilerinizi yazın.</span><span class="sxs-lookup"><span data-stu-id="16b1b-131">Replace TableName, ServerName, DatabaseName, Username, and Password with your own information.</span></span>

```sql
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t ','
```



## <a name="3-load-the-data"></a><span data-ttu-id="16b1b-132">3. Verileri yükleme</span><span class="sxs-lookup"><span data-stu-id="16b1b-132">3. Load the data</span></span>
<span data-ttu-id="16b1b-133">Verileri yüklemek için bir komut satırı açın; Sunucu Adı, Veritabanı Adı, Kullanıcı Adı ve Parola alanlarına kendi bilgilerinizi yazarak aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="16b1b-133">To load the data, open a command prompt and run the following command, replacing the values for Server Name, Database name, Username, and Password with your own information.</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="16b1b-134">Bu komutu kullanarak verilerin düzgün şekilde yüklendiğini doğrulayın</span><span class="sxs-lookup"><span data-stu-id="16b1b-134">Use this command to verify the data was loaded properly</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="16b1b-135">Sonuçlar şu şekilde görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="16b1b-135">The results should look like this:</span></span>

| <span data-ttu-id="16b1b-136">DateId</span><span class="sxs-lookup"><span data-stu-id="16b1b-136">DateId</span></span> | <span data-ttu-id="16b1b-137">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="16b1b-137">CalendarQuarter</span></span> | <span data-ttu-id="16b1b-138">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="16b1b-138">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="16b1b-139">20150101</span><span class="sxs-lookup"><span data-stu-id="16b1b-139">20150101</span></span> |<span data-ttu-id="16b1b-140">1</span><span class="sxs-lookup"><span data-stu-id="16b1b-140">1</span></span> |<span data-ttu-id="16b1b-141">3</span><span class="sxs-lookup"><span data-stu-id="16b1b-141">3</span></span> |
| <span data-ttu-id="16b1b-142">20150201</span><span class="sxs-lookup"><span data-stu-id="16b1b-142">20150201</span></span> |<span data-ttu-id="16b1b-143">1</span><span class="sxs-lookup"><span data-stu-id="16b1b-143">1</span></span> |<span data-ttu-id="16b1b-144">3</span><span class="sxs-lookup"><span data-stu-id="16b1b-144">3</span></span> |
| <span data-ttu-id="16b1b-145">20150301</span><span class="sxs-lookup"><span data-stu-id="16b1b-145">20150301</span></span> |<span data-ttu-id="16b1b-146">1</span><span class="sxs-lookup"><span data-stu-id="16b1b-146">1</span></span> |<span data-ttu-id="16b1b-147">3</span><span class="sxs-lookup"><span data-stu-id="16b1b-147">3</span></span> |
| <span data-ttu-id="16b1b-148">20150401</span><span class="sxs-lookup"><span data-stu-id="16b1b-148">20150401</span></span> |<span data-ttu-id="16b1b-149">2</span><span class="sxs-lookup"><span data-stu-id="16b1b-149">2</span></span> |<span data-ttu-id="16b1b-150">4</span><span class="sxs-lookup"><span data-stu-id="16b1b-150">4</span></span> |
| <span data-ttu-id="16b1b-151">20150501</span><span class="sxs-lookup"><span data-stu-id="16b1b-151">20150501</span></span> |<span data-ttu-id="16b1b-152">2</span><span class="sxs-lookup"><span data-stu-id="16b1b-152">2</span></span> |<span data-ttu-id="16b1b-153">4</span><span class="sxs-lookup"><span data-stu-id="16b1b-153">4</span></span> |
| <span data-ttu-id="16b1b-154">20150601</span><span class="sxs-lookup"><span data-stu-id="16b1b-154">20150601</span></span> |<span data-ttu-id="16b1b-155">2</span><span class="sxs-lookup"><span data-stu-id="16b1b-155">2</span></span> |<span data-ttu-id="16b1b-156">4</span><span class="sxs-lookup"><span data-stu-id="16b1b-156">4</span></span> |
| <span data-ttu-id="16b1b-157">20150701</span><span class="sxs-lookup"><span data-stu-id="16b1b-157">20150701</span></span> |<span data-ttu-id="16b1b-158">3</span><span class="sxs-lookup"><span data-stu-id="16b1b-158">3</span></span> |<span data-ttu-id="16b1b-159">1</span><span class="sxs-lookup"><span data-stu-id="16b1b-159">1</span></span> |
| <span data-ttu-id="16b1b-160">20150801</span><span class="sxs-lookup"><span data-stu-id="16b1b-160">20150801</span></span> |<span data-ttu-id="16b1b-161">3</span><span class="sxs-lookup"><span data-stu-id="16b1b-161">3</span></span> |<span data-ttu-id="16b1b-162">1</span><span class="sxs-lookup"><span data-stu-id="16b1b-162">1</span></span> |
| <span data-ttu-id="16b1b-163">20150801</span><span class="sxs-lookup"><span data-stu-id="16b1b-163">20150801</span></span> |<span data-ttu-id="16b1b-164">3</span><span class="sxs-lookup"><span data-stu-id="16b1b-164">3</span></span> |<span data-ttu-id="16b1b-165">1</span><span class="sxs-lookup"><span data-stu-id="16b1b-165">1</span></span> |
| <span data-ttu-id="16b1b-166">20151001</span><span class="sxs-lookup"><span data-stu-id="16b1b-166">20151001</span></span> |<span data-ttu-id="16b1b-167">4</span><span class="sxs-lookup"><span data-stu-id="16b1b-167">4</span></span> |<span data-ttu-id="16b1b-168">2</span><span class="sxs-lookup"><span data-stu-id="16b1b-168">2</span></span> |
| <span data-ttu-id="16b1b-169">20151101</span><span class="sxs-lookup"><span data-stu-id="16b1b-169">20151101</span></span> |<span data-ttu-id="16b1b-170">4</span><span class="sxs-lookup"><span data-stu-id="16b1b-170">4</span></span> |<span data-ttu-id="16b1b-171">2</span><span class="sxs-lookup"><span data-stu-id="16b1b-171">2</span></span> |
| <span data-ttu-id="16b1b-172">20151201</span><span class="sxs-lookup"><span data-stu-id="16b1b-172">20151201</span></span> |<span data-ttu-id="16b1b-173">4</span><span class="sxs-lookup"><span data-stu-id="16b1b-173">4</span></span> |<span data-ttu-id="16b1b-174">2</span><span class="sxs-lookup"><span data-stu-id="16b1b-174">2</span></span> |

## <a name="4-create-statistics"></a><span data-ttu-id="16b1b-175">4. İstatistik oluşturma</span><span class="sxs-lookup"><span data-stu-id="16b1b-175">4. Create statistics</span></span>
<span data-ttu-id="16b1b-176">SQL Data Warehouse henüz istatistiklerin otomatik olarak oluşturulup güncelleştirilmesini desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="16b1b-176">SQL Data Warehouse does not yet support auto-create or auto-update statistics.</span></span> <span data-ttu-id="16b1b-177">Sorgularınızdan en iyi performansı elde edebilmeniz için ilk yüklemeden veya verilerdeki önemli değişikliklerden sonra istatistiklerin tüm sütunlarda oluşturulması önemlidir.</span><span class="sxs-lookup"><span data-stu-id="16b1b-177">To get the best query performance, it's important to create statistics on all columns of all tables after the first load or after any substantial changes occur in the data.</span></span> <span data-ttu-id="16b1b-178">İstatistiklerin ayrıntılı bir açıklaması için bkz [istatistikleri][Statistics].</span><span class="sxs-lookup"><span data-stu-id="16b1b-178">For a detailed explanation of statistics, see [Statistics][Statistics].</span></span> 

<span data-ttu-id="16b1b-179">Yeni yüklenen tablonuzda istatistik oluşturmak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="16b1b-179">Run the following command to create statistics on your newly loaded table.</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="5-export-data-from-sql-data-warehouse"></a><span data-ttu-id="16b1b-180">5. SQL Data Warehouse'dan veri aktarma</span><span class="sxs-lookup"><span data-stu-id="16b1b-180">5. Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="16b1b-181">Alıştırma yapmak için biraz önce SQL Data Warehouse'dan yüklediğiniz verileri tekrar dışarı aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="16b1b-181">For fun, you can export the data that you just loaded back out of SQL Data Warehouse.</span></span>  <span data-ttu-id="16b1b-182">Dışarı aktarma komutu, SQL Server'dan veri aktarma komutuyla tamamen aynıdır.</span><span class="sxs-lookup"><span data-stu-id="16b1b-182">The command to export is exactly the same as exporting from SQL Server.</span></span>

<span data-ttu-id="16b1b-183">Ancak sonuçlarda bir fark görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="16b1b-183">However, there is a difference in the results.</span></span> <span data-ttu-id="16b1b-184">Veriler SQL Data Warehouse'da dağıtılmış konumlarda depolandığı için, dışarı veri aktardığınızda her bir İşlem düğümü kendi verisini çıkış dosyasına yazar.</span><span class="sxs-lookup"><span data-stu-id="16b1b-184">Since the data is stored in distributed locations within SQL Data Warehouse, when you export data each Compute node writes it data to the output file.</span></span> <span data-ttu-id="16b1b-185">Çıkış dosyasındaki veri sırası, giriş dosyasındaki veri sırasından farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="16b1b-185">The order of the data in the output file is likely to be different than the order of the data in the input file.</span></span>

### <a name="export-a-table-and-compare-exported-results"></a><span data-ttu-id="16b1b-186">Bir tabloyu dışarı aktarma ve dışarı aktarılan sonuçları karşılaştırma</span><span class="sxs-lookup"><span data-stu-id="16b1b-186">Export a table and compare exported results</span></span>
<span data-ttu-id="16b1b-187">Dışarı aktarılan verileri görmek için bir komut istemi açın ve kendi parametrelerinizi kullanarak bu komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="16b1b-187">To see the exported data, open a command prompt and run this command using your own parameters.</span></span> <span data-ttu-id="16b1b-188">ServerName, Azure mantıksal SQL Server'ınızın adıdır.</span><span class="sxs-lookup"><span data-stu-id="16b1b-188">ServerName is the name of your Azure logical SQL Server.</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="16b1b-189">Yeni dosyayı açarak verilerin düzgün bir şekilde dışarı aktarıldığını doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="16b1b-189">You can verify the data was exported correctly by opening the new file.</span></span> <span data-ttu-id="16b1b-190">Dosyadaki veriler aşağıdaki metinle eşleşmelidir ancak sıraları farklı olabilir:</span><span class="sxs-lookup"><span data-stu-id="16b1b-190">The data in the file should match the text below, but will likely be sorted in a different order:</span></span>

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

### <a name="export-the-results-of-a-query"></a><span data-ttu-id="16b1b-191">Bir sorgunun sonuçlarını dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="16b1b-191">Export the results of a query</span></span>
<span data-ttu-id="16b1b-192">Tüm tabloyu dışarı aktarmak yerine, bcp yardımcı programının **queryout** işlevini kullanarak bir sorgunun sonuçlarını dışarı aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="16b1b-192">You can use the **queryout** function of bcp to export the results of a query instead of exporting the entire table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="16b1b-193">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="16b1b-193">Next steps</span></span>
<span data-ttu-id="16b1b-194">Yüklemeye genel bakış için bkz. [SQL Veri Ambarı'na veri yükleme][Load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="16b1b-194">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="16b1b-195">Geliştirme ile ilgili daha fazla ipucu için bkz. [SQL Veri Ambarı’nda geliştirmeye genel bakış][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="16b1b-195">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>
<span data-ttu-id="16b1b-196">Bkz: [tablo genel bakışı] [ Table Overview] veya [CREATE TABLE söz dizimi] [ CREATE TABLE syntax] SQL Data Warehouse'da tablo oluşturma hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="16b1b-196">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse.</span></span>

<!--Image references-->

<!--Article references-->

[Load data into SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[Table Overview]: ./sql-data-warehouse-tables-overview.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
