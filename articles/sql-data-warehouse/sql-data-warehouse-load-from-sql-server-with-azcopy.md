---
title: Azure SQL Data Warehouse'a (PolyBase) SQL Server'a aaaLoad verilerden | Microsoft Docs
description: "SQL Server tooflat dosyaları, AZCopy tooimport veri tooAzure blob depolama ve PolyBase tooingest hello veri BCP tooexport verilerini Azure SQL Data Warehouse'a kullanır."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 4d42786a-fb28-43c9-9c3b-72d19c0ecc11
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 89e2a91bc97642e9fc18545cb802b42d8dc4ad95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-azcopy"></a><span data-ttu-id="6b241-103">SQL Server'dan Azure SQL Data Warehouse'a veri yükleme (AZCopy)</span><span class="sxs-lookup"><span data-stu-id="6b241-103">Load data from SQL Server into Azure SQL Data Warehouse (AZCopy)</span></span>
<span data-ttu-id="6b241-104">BCP ve AZCopy komut satırı yardımcı programlarını tooload verileri SQL Server tooAzure blob depolama biriminden kullanın.</span><span class="sxs-lookup"><span data-stu-id="6b241-104">Use bcp and AZCopy command-line utilities tooload data from SQL Server tooAzure blob storage.</span></span> <span data-ttu-id="6b241-105">Daha sonra PolyBase veya Azure Data Factory tooload hello verileri Azure SQL Data Warehouse'a kullanın.</span><span class="sxs-lookup"><span data-stu-id="6b241-105">Then use PolyBase or Azure Data Factory tooload hello data into Azure SQL Data Warehouse.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="6b241-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="6b241-106">Prerequisites</span></span>
<span data-ttu-id="6b241-107">toostep Bu öğreticide, aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="6b241-107">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="6b241-108">SQL Data Warehouse veritabanı</span><span class="sxs-lookup"><span data-stu-id="6b241-108">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="6b241-109">Merhaba bcp komut satırı yardımcı programının yüklü olması</span><span class="sxs-lookup"><span data-stu-id="6b241-109">hello bcp command line utility installed</span></span>
* <span data-ttu-id="6b241-110">Merhaba SQLCMD komut satırı yardımcı programının yüklü olması</span><span class="sxs-lookup"><span data-stu-id="6b241-110">hello SQLCMD command line utility installed</span></span>

> [!NOTE]
> <span data-ttu-id="6b241-111">Hello hello bcp ve sqlcmd yardımcı programlarını indirebilirsiniz [Microsoft Download Center][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="6b241-111">You can download hello bcp and sqlcmd utilities from hello [Microsoft Download Center][Microsoft Download Center].</span></span>
> 
> 

## <a name="import-data-into-sql-data-warehouse"></a><span data-ttu-id="6b241-112">SQL Data Warehouse'a veri aktarma</span><span class="sxs-lookup"><span data-stu-id="6b241-112">Import data into SQL Data Warehouse</span></span>
<span data-ttu-id="6b241-113">Bu öğreticide, Azure SQL Data Warehouse'da bir tablo oluşturup hello tabloya veri alma.</span><span class="sxs-lookup"><span data-stu-id="6b241-113">In this tutorial, you will create a table in Azure SQL Data Warehouse and import data into hello table.</span></span>

### <a name="step-1-create-a-table-in-azure-sql-data-warehouse"></a><span data-ttu-id="6b241-114">1. Adım: Azure SQL Data Warehouse'da tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="6b241-114">Step 1: Create a table in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="6b241-115">Bir komut isteminden sqlcmd toorun hello sorgu toocreate tablo aşağıdaki Örneğinizde kullanın:</span><span class="sxs-lookup"><span data-stu-id="6b241-115">From a command prompt, use sqlcmd toorun hello following query toocreate a table on your instance:</span></span>

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

> [!NOTE]
> <span data-ttu-id="6b241-116">Bkz: [tablo genel bakışı] [ Table Overview] veya [CREATE TABLE söz dizimi] [ CREATE TABLE syntax] SQL veri ambarı ve hello tablo oluşturma hakkında daha fazla bilgi  Merhaba WITH yan tümcesinde bulunan seçenekler.</span><span class="sxs-lookup"><span data-stu-id="6b241-116">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse and hello  options available in hello WITH clause.</span></span>
> 
> 

### <a name="step-2-create-a-source-data-file"></a><span data-ttu-id="6b241-117">2. Adım: Kaynak veri dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="6b241-117">Step 2: Create a source data file</span></span>
<span data-ttu-id="6b241-118">Veri satırlarını yeni bir metin dosyasına aşağıdaki not defteri ve kopyalama hello açın ve ardından bu dosya tooyour yerel geçici dizin, C:\Temp\DimDate2.txt kaydedin.</span><span class="sxs-lookup"><span data-stu-id="6b241-118">Open Notepad and copy hello following lines of data into a new text file and then save this file tooyour local temp directory, C:\Temp\DimDate2.txt.</span></span>

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

> [!NOTE]
> <span data-ttu-id="6b241-119">Önemli tooremember olan bcp.exe hello UTF-8 dosya kodlamasını desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="6b241-119">It is important tooremember that bcp.exe does not support hello UTF-8 file encoding.</span></span> <span data-ttu-id="6b241-120">bcp.exe dosyasını kullanırken lütfen ASCII dosyalarını veya UTF-16 kodlu dosyaları kullanın.</span><span class="sxs-lookup"><span data-stu-id="6b241-120">Please use ASCII files or UTF-16 encoded files when using bcp.exe.</span></span>
> 
> 

### <a name="step-3-connect-and-import-hello-data"></a><span data-ttu-id="6b241-121">3. adım: Bağlanma ve hello veri alma</span><span class="sxs-lookup"><span data-stu-id="6b241-121">Step 3: Connect and import hello data</span></span>
<span data-ttu-id="6b241-122">BCP kullanarak bağlanın ve komutu değiştirerek hello değerleri uygun şekilde aşağıdaki hello kullanarak hello veri içeri aktarın:</span><span class="sxs-lookup"><span data-stu-id="6b241-122">Using bcp, you can connect and import hello data using hello following command replacing hello values as appropriate:</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="6b241-123">Merhaba sqlcmd kullanarak sorgu aşağıdaki hello çalıştırarak verilerin yüklendiğini doğrulayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6b241-123">You can verify hello data was loaded by running hello following query using sqlcmd:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="6b241-124">Bu, sonuçları aşağıdaki hello döndürmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="6b241-124">This should return hello following results:</span></span>

| <span data-ttu-id="6b241-125">DateId</span><span class="sxs-lookup"><span data-stu-id="6b241-125">DateId</span></span> | <span data-ttu-id="6b241-126">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="6b241-126">CalendarQuarter</span></span> | <span data-ttu-id="6b241-127">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="6b241-127">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6b241-128">20150101</span><span class="sxs-lookup"><span data-stu-id="6b241-128">20150101</span></span> |<span data-ttu-id="6b241-129">1</span><span class="sxs-lookup"><span data-stu-id="6b241-129">1</span></span> |<span data-ttu-id="6b241-130">3</span><span class="sxs-lookup"><span data-stu-id="6b241-130">3</span></span> |
| <span data-ttu-id="6b241-131">20150201</span><span class="sxs-lookup"><span data-stu-id="6b241-131">20150201</span></span> |<span data-ttu-id="6b241-132">1</span><span class="sxs-lookup"><span data-stu-id="6b241-132">1</span></span> |<span data-ttu-id="6b241-133">3</span><span class="sxs-lookup"><span data-stu-id="6b241-133">3</span></span> |
| <span data-ttu-id="6b241-134">20150301</span><span class="sxs-lookup"><span data-stu-id="6b241-134">20150301</span></span> |<span data-ttu-id="6b241-135">1</span><span class="sxs-lookup"><span data-stu-id="6b241-135">1</span></span> |<span data-ttu-id="6b241-136">3</span><span class="sxs-lookup"><span data-stu-id="6b241-136">3</span></span> |
| <span data-ttu-id="6b241-137">20150401</span><span class="sxs-lookup"><span data-stu-id="6b241-137">20150401</span></span> |<span data-ttu-id="6b241-138">2</span><span class="sxs-lookup"><span data-stu-id="6b241-138">2</span></span> |<span data-ttu-id="6b241-139">4</span><span class="sxs-lookup"><span data-stu-id="6b241-139">4</span></span> |
| <span data-ttu-id="6b241-140">20150501</span><span class="sxs-lookup"><span data-stu-id="6b241-140">20150501</span></span> |<span data-ttu-id="6b241-141">2</span><span class="sxs-lookup"><span data-stu-id="6b241-141">2</span></span> |<span data-ttu-id="6b241-142">4</span><span class="sxs-lookup"><span data-stu-id="6b241-142">4</span></span> |
| <span data-ttu-id="6b241-143">20150601</span><span class="sxs-lookup"><span data-stu-id="6b241-143">20150601</span></span> |<span data-ttu-id="6b241-144">2</span><span class="sxs-lookup"><span data-stu-id="6b241-144">2</span></span> |<span data-ttu-id="6b241-145">4</span><span class="sxs-lookup"><span data-stu-id="6b241-145">4</span></span> |
| <span data-ttu-id="6b241-146">20150701</span><span class="sxs-lookup"><span data-stu-id="6b241-146">20150701</span></span> |<span data-ttu-id="6b241-147">3</span><span class="sxs-lookup"><span data-stu-id="6b241-147">3</span></span> |<span data-ttu-id="6b241-148">1</span><span class="sxs-lookup"><span data-stu-id="6b241-148">1</span></span> |
| <span data-ttu-id="6b241-149">20150801</span><span class="sxs-lookup"><span data-stu-id="6b241-149">20150801</span></span> |<span data-ttu-id="6b241-150">3</span><span class="sxs-lookup"><span data-stu-id="6b241-150">3</span></span> |<span data-ttu-id="6b241-151">1</span><span class="sxs-lookup"><span data-stu-id="6b241-151">1</span></span> |
| <span data-ttu-id="6b241-152">20150801</span><span class="sxs-lookup"><span data-stu-id="6b241-152">20150801</span></span> |<span data-ttu-id="6b241-153">3</span><span class="sxs-lookup"><span data-stu-id="6b241-153">3</span></span> |<span data-ttu-id="6b241-154">1</span><span class="sxs-lookup"><span data-stu-id="6b241-154">1</span></span> |
| <span data-ttu-id="6b241-155">20151001</span><span class="sxs-lookup"><span data-stu-id="6b241-155">20151001</span></span> |<span data-ttu-id="6b241-156">4</span><span class="sxs-lookup"><span data-stu-id="6b241-156">4</span></span> |<span data-ttu-id="6b241-157">2</span><span class="sxs-lookup"><span data-stu-id="6b241-157">2</span></span> |
| <span data-ttu-id="6b241-158">20151101</span><span class="sxs-lookup"><span data-stu-id="6b241-158">20151101</span></span> |<span data-ttu-id="6b241-159">4</span><span class="sxs-lookup"><span data-stu-id="6b241-159">4</span></span> |<span data-ttu-id="6b241-160">2</span><span class="sxs-lookup"><span data-stu-id="6b241-160">2</span></span> |
| <span data-ttu-id="6b241-161">20151201</span><span class="sxs-lookup"><span data-stu-id="6b241-161">20151201</span></span> |<span data-ttu-id="6b241-162">4</span><span class="sxs-lookup"><span data-stu-id="6b241-162">4</span></span> |<span data-ttu-id="6b241-163">2</span><span class="sxs-lookup"><span data-stu-id="6b241-163">2</span></span> |

### <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="6b241-164">4. Adım: Yeni yüklenmiş verilerinize ilişkin İstatistikler oluşturma</span><span class="sxs-lookup"><span data-stu-id="6b241-164">Step 4: Create Statistics on your newly loaded data</span></span>
<span data-ttu-id="6b241-165">Azure SQL Data Warehouse henüz istatistiklerin otomatik olarak oluşturulup güncelleştirilmesini desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="6b241-165">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span> <span data-ttu-id="6b241-166">Sipariş tooget hello en iyi performansı sorgularınızı, istatistikleri hello ilk yükleme işleminden sonra tüm tabloların tüm sütunlarda oluşturulması önemlidir veya hello verilerde önemli değişikliklerden.</span><span class="sxs-lookup"><span data-stu-id="6b241-166">In order tooget hello best performance from your queries, it's important that statistics be created on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span> <span data-ttu-id="6b241-167">Merhaba istatistikleri ayrıntılı bir açıklaması için bkz [istatistikleri] [ Statistics] konu hello geliştirme grubunu konuda.</span><span class="sxs-lookup"><span data-stu-id="6b241-167">For a detailed explanation of statistics, see hello [Statistics][Statistics] topic in hello Develop group of topics.</span></span> <span data-ttu-id="6b241-168">Nasıl toocreate istatistik oluşturacağınıza yönelik hello Bu örnekte yüklenen, hızlı bir örnek aşağıda verilmiştir</span><span class="sxs-lookup"><span data-stu-id="6b241-168">Below is a quick example of how toocreate statistics on hello tabled loaded in this example</span></span>

<span data-ttu-id="6b241-169">Bir sqlcmd isteminden CREATE STATISTICS deyimlerini aşağıdaki hello yürütün:</span><span class="sxs-lookup"><span data-stu-id="6b241-169">Execute hello following CREATE STATISTICS statements from a sqlcmd prompt:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="export-data-from-sql-data-warehouse"></a><span data-ttu-id="6b241-170">SQL Data Warehouse'dan veri aktarma</span><span class="sxs-lookup"><span data-stu-id="6b241-170">Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="6b241-171">Bu öğreticide SQL Data Warehouse'da bulunan bir tablodan veri dosyası oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="6b241-171">In this tutorial, you will create a data file from a table in SQL Data Warehouse.</span></span> <span data-ttu-id="6b241-172">Biz hello verileri DimDate2_export.txt adlı tooa yeni bir veri dosyası oluşturduğumuz verecektir.</span><span class="sxs-lookup"><span data-stu-id="6b241-172">We will export hello data we created above tooa new data file called DimDate2_export.txt.</span></span>

### <a name="step-1-export-hello-data"></a><span data-ttu-id="6b241-173">1. adım: hello verileri dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="6b241-173">Step 1: Export hello data</span></span>
<span data-ttu-id="6b241-174">Hello bcp yardımcı programını kullanarak, bağlanın ve komutu değiştirerek hello değerleri uygun şekilde aşağıdaki hello kullanarak verileri dışarı aktarma:</span><span class="sxs-lookup"><span data-stu-id="6b241-174">Using hello bcp utility, you can connect and export data using hello following command replacing hello values as appropriate:</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="6b241-175">Merhaba yeni dosyayı açarak verilerin doğru verildiğinden hello doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6b241-175">You can verify hello data was exported correctly by opening hello new file.</span></span> <span data-ttu-id="6b241-176">Merhaba dosyasındaki Hello verileri hello metinle eşleşmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="6b241-176">hello data in hello file should match hello text below:</span></span>

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

> [!NOTE]
> <span data-ttu-id="6b241-177">Toohello yapısı dağıtılmış sistemlerin hello veri sırası SQL Data Warehouse veritabanlarında aynı hello olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="6b241-177">Due toohello nature of distributed systems, hello data order may not be hello same across SQL Data Warehouse databases.</span></span> <span data-ttu-id="6b241-178">Başka bir seçenektir toouse hello **queryout** bcp toowrite bir sorgu işlevinin ayıklamak yerine hello tüm tabloyu dışarı aktarma.</span><span class="sxs-lookup"><span data-stu-id="6b241-178">Another option is toouse hello **queryout** function of bcp toowrite a query extract rather than export hello entire table.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="6b241-179">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6b241-179">Next steps</span></span>
<span data-ttu-id="6b241-180">Yüklemeye genel bakış için bkz. [SQL Veri Ambarı'na veri yükleme][Load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="6b241-180">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="6b241-181">Geliştirme ile ilgili daha fazla ipucu için bkz. [SQL Veri Ambarı’nda geliştirmeye genel bakış][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="6b241-181">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

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
