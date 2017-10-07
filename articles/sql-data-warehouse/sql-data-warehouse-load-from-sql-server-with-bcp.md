---
title: "aaaLoad verileri SQL Server'dan Azure SQL veri ambarında (bcp) | Microsoft Docs"
description: "Küçük boyutlu veriler için SQL Server tooflat dosyalarından bcp tooexport verileri ve hello veri içeri aktarma doğrudan Azure SQL Data Warehouse'a kullanır."
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
ms.openlocfilehash: a03b5403d123e8814ae73a7cce8e6851c8b264a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-flat-files"></a><span data-ttu-id="d47d1-103">SQL Server'dan Azure SQL Data Warehouse'a veri yükleme (düz dosyalar)</span><span class="sxs-lookup"><span data-stu-id="d47d1-103">Load data from SQL Server into Azure SQL Data Warehouse (flat files)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d47d1-104">SSIS</span><span class="sxs-lookup"><span data-stu-id="d47d1-104">SSIS</span></span>](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [<span data-ttu-id="d47d1-105">PolyBase</span><span class="sxs-lookup"><span data-stu-id="d47d1-105">PolyBase</span></span>](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [<span data-ttu-id="d47d1-106">bcp</span><span class="sxs-lookup"><span data-stu-id="d47d1-106">bcp</span></span>](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

<span data-ttu-id="d47d1-107">Küçük veri kümeleri için hello bcp komut satırı yardımcı programını tooexport verileri SQL Server'dan kullanın ve tooAzure SQL veri ambarı doğrudan yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d47d1-107">For small data sets, you can use hello bcp command-line utility tooexport data from SQL Server and then load it directly tooAzure SQL Data Warehouse.</span></span>

<span data-ttu-id="d47d1-108">Bu öğreticide bcp'yi kullanarak şunları yapacaksınız:</span><span class="sxs-lookup"><span data-stu-id="d47d1-108">In this tutorial, you will use bcp to:</span></span>

* <span data-ttu-id="d47d1-109">Bir tablodan hello bcp out komutunu kullanarak SQL Server'dan dışarı aktar (veya basit bir örnek dosyası oluşturma)</span><span class="sxs-lookup"><span data-stu-id="d47d1-109">Export a table from from SQL Server by using hello bcp out command (or create a simple sample file)</span></span>
* <span data-ttu-id="d47d1-110">Düz dosya tooSQL veri ambarı hello tablosundan alma.</span><span class="sxs-lookup"><span data-stu-id="d47d1-110">Import hello table from a flat file tooSQL Data Warehouse.</span></span>
* <span data-ttu-id="d47d1-111">İstatistikleri hello yüklenen veriler üzerinde oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d47d1-111">Create statistics on hello loaded data.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="d47d1-112">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="d47d1-112">Before you begin</span></span>
### <a name="prerequisites"></a><span data-ttu-id="d47d1-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d47d1-113">Prerequisites</span></span>
<span data-ttu-id="d47d1-114">toostep Bu öğreticide, aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="d47d1-114">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="d47d1-115">SQL Data Warehouse veritabanı</span><span class="sxs-lookup"><span data-stu-id="d47d1-115">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="d47d1-116">Merhaba bcp komut satırı yardımcı programının yüklü olması</span><span class="sxs-lookup"><span data-stu-id="d47d1-116">hello bcp command-line utility installed</span></span>
* <span data-ttu-id="d47d1-117">Merhaba sqlcmd komut satırı yardımcı programının yüklü olması</span><span class="sxs-lookup"><span data-stu-id="d47d1-117">hello sqlcmd command-line utility installed</span></span>

<span data-ttu-id="d47d1-118">Hello hello bcp ve sqlcmd yardımcı programlarını indirebilirsiniz [Microsoft Download Center][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="d47d1-118">You can download hello bcp and sqlcmd utilities from hello [Microsoft Download Center][Microsoft Download Center].</span></span>

### <a name="data-in-ascii-or-utf-16-format"></a><span data-ttu-id="d47d1-119">ASCII veya UTF-16 biçimindeki veriler</span><span class="sxs-lookup"><span data-stu-id="d47d1-119">Data in ASCII or UTF-16 format</span></span>
<span data-ttu-id="d47d1-120">Bu öğreticiyi kendi verilerinizle deniyorsanız verilerinizin toouse hello ASCII veya UTF-8 bcp desteklemediğinden UTF-16 kodlamasını gerekir.</span><span class="sxs-lookup"><span data-stu-id="d47d1-120">If you are trying this tutorial with your own data, your data needs toouse hello ASCII or UTF-16 encoding since bcp does not support UTF-8.</span></span> 

<span data-ttu-id="d47d1-121">PolyBase UTF-8'i destekler ancak henüz UTF-16'yi desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="d47d1-121">PolyBase supports UTF-8 but doesn't yet support UTF-16.</span></span> <span data-ttu-id="d47d1-122">PolyBase ile toocombine bcp istiyorsanız SQL Server'dan dışarı aktardıktan sonra tootransform hello veri tooUTF-8 gerektiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="d47d1-122">Note that if you want toocombine bcp with PolyBase you will need tootransform hello data tooUTF-8 after it is exported from SQL Server.</span></span> 

## <a name="1-create-a-destination-table"></a><span data-ttu-id="d47d1-123">1. Hedef tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="d47d1-123">1. Create a destination table</span></span>
<span data-ttu-id="d47d1-124">SQL veri ambarındaki hello yük hello hedef tablo olacak bir tablo tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="d47d1-124">Define a table in SQL Data Warehouse that will be hello destination table for hello load.</span></span> <span data-ttu-id="d47d1-125">Merhaba tablodaki Hello sütun toohello veriler, her satır, veri dosyanızın karşılık gelmelidir.</span><span class="sxs-lookup"><span data-stu-id="d47d1-125">hello columns in hello table must correspond toohello data in each row of your data file.</span></span>

<span data-ttu-id="d47d1-126">toocreate tablo, bir komut istemi açın ve sqlcmd.exe toorun hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="d47d1-126">toocreate a table, open a command prompt and use sqlcmd.exe toorun hello following command:</span></span>

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


## <a name="2-create-a-source-data-file"></a><span data-ttu-id="d47d1-127">2. Kaynak veri dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="d47d1-127">2. Create a source data file</span></span>
<span data-ttu-id="d47d1-128">Veri satırlarını yeni bir metin dosyasına aşağıdaki not defteri ve kopyalama hello açın ve ardından bu dosya tooyour yerel geçici dizin, C:\Temp\DimDate2.txt kaydedin.</span><span class="sxs-lookup"><span data-stu-id="d47d1-128">Open Notepad and copy hello following lines of data into a new text file and then save this file tooyour local temp directory, C:\Temp\DimDate2.txt.</span></span> <span data-ttu-id="d47d1-129">Bu veri ASCII biçimindedir.</span><span class="sxs-lookup"><span data-stu-id="d47d1-129">This data is in ASCII format.</span></span>

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

<span data-ttu-id="d47d1-130">(İsteğe bağlı) tooexport bir SQL Server veritabanından kendi verilerinizi bir komut istemi açın ve hello aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d47d1-130">(Optional) tooexport your own data from a SQL Server database, open a command prompt and run hello following command.</span></span> <span data-ttu-id="d47d1-131">TableName (Tablo Adı), ServerName (Sunucu Adı), DatabaseName (Veritabanı Adı), Username (Kullanıcı Adı) ve Password (Parola) alanlarına kendi bilgilerinizi yazın.</span><span class="sxs-lookup"><span data-stu-id="d47d1-131">Replace TableName, ServerName, DatabaseName, Username, and Password with your own information.</span></span>

```sql
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t ','
```



## <a name="3-load-hello-data"></a><span data-ttu-id="d47d1-132">3. Merhaba veri yükleme</span><span class="sxs-lookup"><span data-stu-id="d47d1-132">3. Load hello data</span></span>
<span data-ttu-id="d47d1-133">tooload hello verileri, bir komut istemi açın ve aşağıdaki komut, sunucu adı, veritabanı adı, kullanıcı adı ve parola alanlarına kendi bilgilerinizi hello değerleri değiştirerek hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d47d1-133">tooload hello data, open a command prompt and run hello following command, replacing hello values for Server Name, Database name, Username, and Password with your own information.</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="d47d1-134">Bu komut tooverify hello verilerin düzgün şekilde yüklendiğini kullanın</span><span class="sxs-lookup"><span data-stu-id="d47d1-134">Use this command tooverify hello data was loaded properly</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="d47d1-135">Merhaba sonuçları aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="d47d1-135">hello results should look like this:</span></span>

| <span data-ttu-id="d47d1-136">DateId</span><span class="sxs-lookup"><span data-stu-id="d47d1-136">DateId</span></span> | <span data-ttu-id="d47d1-137">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="d47d1-137">CalendarQuarter</span></span> | <span data-ttu-id="d47d1-138">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="d47d1-138">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d47d1-139">20150101</span><span class="sxs-lookup"><span data-stu-id="d47d1-139">20150101</span></span> |<span data-ttu-id="d47d1-140">1</span><span class="sxs-lookup"><span data-stu-id="d47d1-140">1</span></span> |<span data-ttu-id="d47d1-141">3</span><span class="sxs-lookup"><span data-stu-id="d47d1-141">3</span></span> |
| <span data-ttu-id="d47d1-142">20150201</span><span class="sxs-lookup"><span data-stu-id="d47d1-142">20150201</span></span> |<span data-ttu-id="d47d1-143">1</span><span class="sxs-lookup"><span data-stu-id="d47d1-143">1</span></span> |<span data-ttu-id="d47d1-144">3</span><span class="sxs-lookup"><span data-stu-id="d47d1-144">3</span></span> |
| <span data-ttu-id="d47d1-145">20150301</span><span class="sxs-lookup"><span data-stu-id="d47d1-145">20150301</span></span> |<span data-ttu-id="d47d1-146">1</span><span class="sxs-lookup"><span data-stu-id="d47d1-146">1</span></span> |<span data-ttu-id="d47d1-147">3</span><span class="sxs-lookup"><span data-stu-id="d47d1-147">3</span></span> |
| <span data-ttu-id="d47d1-148">20150401</span><span class="sxs-lookup"><span data-stu-id="d47d1-148">20150401</span></span> |<span data-ttu-id="d47d1-149">2</span><span class="sxs-lookup"><span data-stu-id="d47d1-149">2</span></span> |<span data-ttu-id="d47d1-150">4</span><span class="sxs-lookup"><span data-stu-id="d47d1-150">4</span></span> |
| <span data-ttu-id="d47d1-151">20150501</span><span class="sxs-lookup"><span data-stu-id="d47d1-151">20150501</span></span> |<span data-ttu-id="d47d1-152">2</span><span class="sxs-lookup"><span data-stu-id="d47d1-152">2</span></span> |<span data-ttu-id="d47d1-153">4</span><span class="sxs-lookup"><span data-stu-id="d47d1-153">4</span></span> |
| <span data-ttu-id="d47d1-154">20150601</span><span class="sxs-lookup"><span data-stu-id="d47d1-154">20150601</span></span> |<span data-ttu-id="d47d1-155">2</span><span class="sxs-lookup"><span data-stu-id="d47d1-155">2</span></span> |<span data-ttu-id="d47d1-156">4</span><span class="sxs-lookup"><span data-stu-id="d47d1-156">4</span></span> |
| <span data-ttu-id="d47d1-157">20150701</span><span class="sxs-lookup"><span data-stu-id="d47d1-157">20150701</span></span> |<span data-ttu-id="d47d1-158">3</span><span class="sxs-lookup"><span data-stu-id="d47d1-158">3</span></span> |<span data-ttu-id="d47d1-159">1</span><span class="sxs-lookup"><span data-stu-id="d47d1-159">1</span></span> |
| <span data-ttu-id="d47d1-160">20150801</span><span class="sxs-lookup"><span data-stu-id="d47d1-160">20150801</span></span> |<span data-ttu-id="d47d1-161">3</span><span class="sxs-lookup"><span data-stu-id="d47d1-161">3</span></span> |<span data-ttu-id="d47d1-162">1</span><span class="sxs-lookup"><span data-stu-id="d47d1-162">1</span></span> |
| <span data-ttu-id="d47d1-163">20150801</span><span class="sxs-lookup"><span data-stu-id="d47d1-163">20150801</span></span> |<span data-ttu-id="d47d1-164">3</span><span class="sxs-lookup"><span data-stu-id="d47d1-164">3</span></span> |<span data-ttu-id="d47d1-165">1</span><span class="sxs-lookup"><span data-stu-id="d47d1-165">1</span></span> |
| <span data-ttu-id="d47d1-166">20151001</span><span class="sxs-lookup"><span data-stu-id="d47d1-166">20151001</span></span> |<span data-ttu-id="d47d1-167">4</span><span class="sxs-lookup"><span data-stu-id="d47d1-167">4</span></span> |<span data-ttu-id="d47d1-168">2</span><span class="sxs-lookup"><span data-stu-id="d47d1-168">2</span></span> |
| <span data-ttu-id="d47d1-169">20151101</span><span class="sxs-lookup"><span data-stu-id="d47d1-169">20151101</span></span> |<span data-ttu-id="d47d1-170">4</span><span class="sxs-lookup"><span data-stu-id="d47d1-170">4</span></span> |<span data-ttu-id="d47d1-171">2</span><span class="sxs-lookup"><span data-stu-id="d47d1-171">2</span></span> |
| <span data-ttu-id="d47d1-172">20151201</span><span class="sxs-lookup"><span data-stu-id="d47d1-172">20151201</span></span> |<span data-ttu-id="d47d1-173">4</span><span class="sxs-lookup"><span data-stu-id="d47d1-173">4</span></span> |<span data-ttu-id="d47d1-174">2</span><span class="sxs-lookup"><span data-stu-id="d47d1-174">2</span></span> |

## <a name="4-create-statistics"></a><span data-ttu-id="d47d1-175">4. İstatistik oluşturma</span><span class="sxs-lookup"><span data-stu-id="d47d1-175">4. Create statistics</span></span>
<span data-ttu-id="d47d1-176">SQL Data Warehouse henüz istatistiklerin otomatik olarak oluşturulup güncelleştirilmesini desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="d47d1-176">SQL Data Warehouse does not yet support auto-create or auto-update statistics.</span></span> <span data-ttu-id="d47d1-177">tooget hello en iyi sorgu performansını, hello ilk yükleme sonrasında veya hello verilerde önemli değişikliklerden sonra tüm tabloların tüm sütunlar üzerinde önemli toocreate istatistikleri değil.</span><span class="sxs-lookup"><span data-stu-id="d47d1-177">tooget hello best query performance, it's important toocreate statistics on all columns of all tables after hello first load or after any substantial changes occur in hello data.</span></span> <span data-ttu-id="d47d1-178">İstatistiklerin ayrıntılı bir açıklaması için bkz [istatistikleri][Statistics].</span><span class="sxs-lookup"><span data-stu-id="d47d1-178">For a detailed explanation of statistics, see [Statistics][Statistics].</span></span> 

<span data-ttu-id="d47d1-179">Çalışma hello aşağıdaki yeni yüklenen tablonuzda istatistik toocreate komutu.</span><span class="sxs-lookup"><span data-stu-id="d47d1-179">Run hello following command toocreate statistics on your newly loaded table.</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="5-export-data-from-sql-data-warehouse"></a><span data-ttu-id="d47d1-180">5. SQL Data Warehouse'dan veri aktarma</span><span class="sxs-lookup"><span data-stu-id="d47d1-180">5. Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="d47d1-181">Fun için yalnızca geri SQL Data warehouse'dan hello verileri dışarı aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d47d1-181">For fun, you can export hello data that you just loaded back out of SQL Data Warehouse.</span></span>  <span data-ttu-id="d47d1-182">Merhaba komutu tooexport olan tam olarak hello SQL Server'dan veri aktarma aynıdır.</span><span class="sxs-lookup"><span data-stu-id="d47d1-182">hello command tooexport is exactly hello same as exporting from SQL Server.</span></span>

<span data-ttu-id="d47d1-183">Ancak, hello sonuçlarda bir fark yoktur.</span><span class="sxs-lookup"><span data-stu-id="d47d1-183">However, there is a difference in hello results.</span></span> <span data-ttu-id="d47d1-184">Veri verdiğinizde hello verileri SQL Data warehouse'da dağıtılmış konumlarda depolandığı her işlem düğümü veri toohello çıkış dosyasına yazar.</span><span class="sxs-lookup"><span data-stu-id="d47d1-184">Since hello data is stored in distributed locations within SQL Data Warehouse, when you export data each Compute node writes it data toohello output file.</span></span> <span data-ttu-id="d47d1-185">Merhaba hello veri hello çıktı dosyasına büyük olasılıkla toobe hello giriş dosyasındaki hello verileri hello sırasını farklı sırasıdır.</span><span class="sxs-lookup"><span data-stu-id="d47d1-185">hello order of hello data in hello output file is likely toobe different than hello order of hello data in hello input file.</span></span>

### <a name="export-a-table-and-compare-exported-results"></a><span data-ttu-id="d47d1-186">Bir tabloyu dışarı aktarma ve dışarı aktarılan sonuçları karşılaştırma</span><span class="sxs-lookup"><span data-stu-id="d47d1-186">Export a table and compare exported results</span></span>
<span data-ttu-id="d47d1-187">toosee dışarı aktarılan verileri Merhaba, bir komut istemi açın ve kendi parametrelerinizi kullanarak bu komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d47d1-187">toosee hello exported data, open a command prompt and run this command using your own parameters.</span></span> <span data-ttu-id="d47d1-188">ServerName hello Azure mantıksal SQL Sunucunuz adıdır.</span><span class="sxs-lookup"><span data-stu-id="d47d1-188">ServerName is hello name of your Azure logical SQL Server.</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="d47d1-189">Merhaba yeni dosyayı açarak verilerin doğru verildiğinden hello doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d47d1-189">You can verify hello data was exported correctly by opening hello new file.</span></span> <span data-ttu-id="d47d1-190">Merhaba dosyasındaki Hello verileri hello metinle eşleşmelidir ancak büyük olasılıkla farklı bir sırada sıralanır:</span><span class="sxs-lookup"><span data-stu-id="d47d1-190">hello data in hello file should match hello text below, but will likely be sorted in a different order:</span></span>

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

### <a name="export-hello-results-of-a-query"></a><span data-ttu-id="d47d1-191">Merhaba bir sorgunun sonuçlarını dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="d47d1-191">Export hello results of a query</span></span>
<span data-ttu-id="d47d1-192">Merhaba kullanabilirsiniz **queryout** bcp tooexport hello hello tüm tabloyu dışarı yerine bir sorgunun sonuçlarını işlevi.</span><span class="sxs-lookup"><span data-stu-id="d47d1-192">You can use hello **queryout** function of bcp tooexport hello results of a query instead of exporting hello entire table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d47d1-193">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d47d1-193">Next steps</span></span>
<span data-ttu-id="d47d1-194">Yüklemeye genel bakış için bkz. [SQL Veri Ambarı'na veri yükleme][Load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="d47d1-194">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="d47d1-195">Geliştirme ile ilgili daha fazla ipucu için bkz. [SQL Veri Ambarı’nda geliştirmeye genel bakış][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="d47d1-195">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>
<span data-ttu-id="d47d1-196">Bkz: [tablo genel bakışı] [ Table Overview] veya [CREATE TABLE söz dizimi] [ CREATE TABLE syntax] SQL Data Warehouse'da tablo oluşturma hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="d47d1-196">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse.</span></span>

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
