---
title: aaaUse bcp tooload verileri SQL Data Warehouse | Microsoft Docs
description: "BCP'nin ne olduğunu öğrenin ve nasıl toouse veri depolama senaryolarında için."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: f9467d11-fcd6-4131-a65a-2022d2c32d24
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 09a2980585097644924c71899f9e74fb32fbc26d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-bcp"></a><span data-ttu-id="78795-103">BCP ile veri yükleme</span><span class="sxs-lookup"><span data-stu-id="78795-103">Load data with bcp</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="78795-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="78795-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)  
> * [<span data-ttu-id="78795-105">Data Factory</span><span class="sxs-lookup"><span data-stu-id="78795-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [<span data-ttu-id="78795-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="78795-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [<span data-ttu-id="78795-107">BCP</span><span class="sxs-lookup"><span data-stu-id="78795-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)
> 
> 

<span data-ttu-id="78795-108">**[BCP] [ bcp]**  SQL Server, veri dosyaları ve SQL Data Warehouse arasında toocopy veri sağlayan bir komut satırı toplu yükleme yardımcı programıdır.</span><span class="sxs-lookup"><span data-stu-id="78795-108">**[bcp][bcp]** is a command-line bulk load utility that allows you toocopy data between SQL Server, data files, and SQL Data Warehouse.</span></span> <span data-ttu-id="78795-109">BCP tooimport çok sayıda satırı SQL Data Warehouse tablolar veya veri dosyaları SQL Server tablolarına tooexport verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="78795-109">Use bcp tooimport large numbers of rows into SQL Data Warehouse tables or tooexport data from SQL Server tables into data files.</span></span> <span data-ttu-id="78795-110">Merhaba queryout seçeneğiyle kullanılmadığı sürece dışında Transact-SQL olanağıyla bcp gerektirir.</span><span class="sxs-lookup"><span data-stu-id="78795-110">Except when used with hello queryout option, bcp requires no knowledge of Transact-SQL.</span></span>

<span data-ttu-id="78795-111">BCP bir hızlı ve kolay bir yol toomove daha küçük veri kümeleri içine ve dışına SQL veri ambarı veritabanı var.</span><span class="sxs-lookup"><span data-stu-id="78795-111">bcp is a quick and easy way toomove smaller data sets into and out of a SQL Data Warehouse database.</span></span> <span data-ttu-id="78795-112">Hello tam tooload/extract bcp aracılığıyla önerilen veri miktarına bağlıdır bağlantı toohello Azure veri merkezi ağ üzerinde.</span><span class="sxs-lookup"><span data-stu-id="78795-112">hello exact amount of data that is recommended tooload/extract via bcp will depend on you network connection toohello Azure data center.</span></span>  <span data-ttu-id="78795-113">Genel olarak, boyut tabloları bcp aracılığıyla kolayca yüklenip ayıklanabilir ancak büyük miktarda veriyi yüklemek veya ayıklamak için bcp'nin kullanılması önerilmez.</span><span class="sxs-lookup"><span data-stu-id="78795-113">Generally, dimension tables can be loaded and extracted readily with bcp, however, bcp is not recommended for loading or extracting large volumes of data.</span></span>  <span data-ttu-id="78795-114">Polybase aracı yükleme ve SQL Data Warehouse hello yüksek düzeyde paralel işleme mimarisi yararlanarak daha iyi iş yaptığı gibi büyük miktarda veriyi ayıklanması için önerilen hello eder.</span><span class="sxs-lookup"><span data-stu-id="78795-114">Polybase is hello recommended tool for loading and extracting large volumes of data as it does a better job leveraging hello massively parallel processing architecture of SQL Data Warehouse.</span></span>

<span data-ttu-id="78795-115">bcp ile yapabilecekleriniz:</span><span class="sxs-lookup"><span data-stu-id="78795-115">With bcp you can:</span></span>

* <span data-ttu-id="78795-116">Basit komut satırı yardımcı programını tooload verileri SQL Data Warehouse'a kullanın.</span><span class="sxs-lookup"><span data-stu-id="78795-116">Use a simple command-line utility tooload data into SQL Data Warehouse.</span></span>
* <span data-ttu-id="78795-117">Basit komut satırı yardımcı programını tooextract verileri SQL veri ambarından kullanın.</span><span class="sxs-lookup"><span data-stu-id="78795-117">Use a simple command-line utility tooextract data from SQL Data Warehouse.</span></span>

<span data-ttu-id="78795-118">Bu öğreticide şunları nasıl yapacağınızı gösterilecek:</span><span class="sxs-lookup"><span data-stu-id="78795-118">This tutorial will show you how to:</span></span>

* <span data-ttu-id="78795-119">Merhaba bcp in komutunu kullanarak bir tabloya veri al</span><span class="sxs-lookup"><span data-stu-id="78795-119">Import data into a table using hello bcp in command</span></span>
* <span data-ttu-id="78795-120">Veri tablosu sıcaklıklarını hello bcp out komutunu dışarı aktarın</span><span class="sxs-lookup"><span data-stu-id="78795-120">Export data from a table uisng hello bcp out command</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="78795-121">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="78795-121">Prerequisites</span></span>
<span data-ttu-id="78795-122">toostep Bu öğreticide, aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="78795-122">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="78795-123">SQL Data Warehouse veritabanı</span><span class="sxs-lookup"><span data-stu-id="78795-123">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="78795-124">Merhaba bcp komut satırı yardımcı programının yüklü olması</span><span class="sxs-lookup"><span data-stu-id="78795-124">hello bcp command line utility installed</span></span>
* <span data-ttu-id="78795-125">Merhaba SQLCMD komut satırı yardımcı programının yüklü olması</span><span class="sxs-lookup"><span data-stu-id="78795-125">hello SQLCMD command line utility installed</span></span>

> [!NOTE]
> <span data-ttu-id="78795-126">Hello hello bcp ve sqlcmd yardımcı programlarını indirebilirsiniz [Microsoft Download Center][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="78795-126">You can download hello bcp and sqlcmd utilities from hello [Microsoft Download Center][Microsoft Download Center].</span></span>
> 
> 

## <a name="import-data-into-sql-data-warehouse"></a><span data-ttu-id="78795-127">SQL Data Warehouse'a veri aktarma</span><span class="sxs-lookup"><span data-stu-id="78795-127">Import data into SQL Data Warehouse</span></span>
<span data-ttu-id="78795-128">Bu öğreticide, Azure SQL Data Warehouse'da bir tablo oluşturup hello tabloya veri alma.</span><span class="sxs-lookup"><span data-stu-id="78795-128">In this tutorial, you will create a table in Azure SQL Data Warehouse and import data into hello table.</span></span>

### <a name="step-1-create-a-table-in-azure-sql-data-warehouse"></a><span data-ttu-id="78795-129">1. Adım: Azure SQL Data Warehouse'da tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="78795-129">Step 1: Create a table in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="78795-130">Bir komut isteminden sqlcmd toorun hello sorgu toocreate tablo aşağıdaki Örneğinizde kullanın:</span><span class="sxs-lookup"><span data-stu-id="78795-130">From a command prompt, use sqlcmd toorun hello following query toocreate a table on your instance:</span></span>

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
> <span data-ttu-id="78795-131">Bkz: [tablo genel bakışı] [ Table Overview] veya [CREATE TABLE söz dizimi] [ CREATE TABLE syntax] SQL veri ambarı ve hello tablo oluşturma hakkında daha fazla bilgi  Merhaba WITH yan tümcesinde bulunan seçenekler.</span><span class="sxs-lookup"><span data-stu-id="78795-131">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse and hello  options available in hello WITH clause.</span></span>
> 
> 

### <a name="step-2-create-a-source-data-file"></a><span data-ttu-id="78795-132">2. Adım: Kaynak veri dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="78795-132">Step 2: Create a source data file</span></span>
<span data-ttu-id="78795-133">Veri satırlarını yeni bir metin dosyasına aşağıdaki not defteri ve kopyalama hello açın ve ardından bu dosya tooyour yerel geçici dizin, C:\Temp\DimDate2.txt kaydedin.</span><span class="sxs-lookup"><span data-stu-id="78795-133">Open Notepad and copy hello following lines of data into a new text file and then save this file tooyour local temp directory, C:\Temp\DimDate2.txt.</span></span>

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
> <span data-ttu-id="78795-134">Önemli tooremember olan bcp.exe hello UTF-8 dosya kodlamasını desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="78795-134">It is important tooremember that bcp.exe does not support hello UTF-8 file encoding.</span></span> <span data-ttu-id="78795-135">bcp.exe dosyasını kullanırken lütfen ASCII dosyalarını veya UTF-16 kodlu dosyaları kullanın.</span><span class="sxs-lookup"><span data-stu-id="78795-135">Please use ASCII files or UTF-16 encoded files when using bcp.exe.</span></span>
> 
> 

### <a name="step-3-connect-and-import-hello-data"></a><span data-ttu-id="78795-136">3. adım: Bağlanma ve hello veri alma</span><span class="sxs-lookup"><span data-stu-id="78795-136">Step 3: Connect and import hello data</span></span>
<span data-ttu-id="78795-137">BCP kullanarak bağlanın ve komutu değiştirerek hello değerleri uygun şekilde aşağıdaki hello kullanarak hello veri içeri aktarın:</span><span class="sxs-lookup"><span data-stu-id="78795-137">Using bcp, you can connect and import hello data using hello following command replacing hello values as appropriate:</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="78795-138">Merhaba sqlcmd kullanarak sorgu aşağıdaki hello çalıştırarak verilerin yüklendiğini doğrulayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="78795-138">You can verify hello data was loaded by running hello following query using sqlcmd:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="78795-139">Bu, sonuçları aşağıdaki hello döndürmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="78795-139">This should return hello following results:</span></span>

| <span data-ttu-id="78795-140">DateId</span><span class="sxs-lookup"><span data-stu-id="78795-140">DateId</span></span> | <span data-ttu-id="78795-141">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="78795-141">CalendarQuarter</span></span> | <span data-ttu-id="78795-142">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="78795-142">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="78795-143">20150101</span><span class="sxs-lookup"><span data-stu-id="78795-143">20150101</span></span> |<span data-ttu-id="78795-144">1</span><span class="sxs-lookup"><span data-stu-id="78795-144">1</span></span> |<span data-ttu-id="78795-145">3</span><span class="sxs-lookup"><span data-stu-id="78795-145">3</span></span> |
| <span data-ttu-id="78795-146">20150201</span><span class="sxs-lookup"><span data-stu-id="78795-146">20150201</span></span> |<span data-ttu-id="78795-147">1</span><span class="sxs-lookup"><span data-stu-id="78795-147">1</span></span> |<span data-ttu-id="78795-148">3</span><span class="sxs-lookup"><span data-stu-id="78795-148">3</span></span> |
| <span data-ttu-id="78795-149">20150301</span><span class="sxs-lookup"><span data-stu-id="78795-149">20150301</span></span> |<span data-ttu-id="78795-150">1</span><span class="sxs-lookup"><span data-stu-id="78795-150">1</span></span> |<span data-ttu-id="78795-151">3</span><span class="sxs-lookup"><span data-stu-id="78795-151">3</span></span> |
| <span data-ttu-id="78795-152">20150401</span><span class="sxs-lookup"><span data-stu-id="78795-152">20150401</span></span> |<span data-ttu-id="78795-153">2</span><span class="sxs-lookup"><span data-stu-id="78795-153">2</span></span> |<span data-ttu-id="78795-154">4</span><span class="sxs-lookup"><span data-stu-id="78795-154">4</span></span> |
| <span data-ttu-id="78795-155">20150501</span><span class="sxs-lookup"><span data-stu-id="78795-155">20150501</span></span> |<span data-ttu-id="78795-156">2</span><span class="sxs-lookup"><span data-stu-id="78795-156">2</span></span> |<span data-ttu-id="78795-157">4</span><span class="sxs-lookup"><span data-stu-id="78795-157">4</span></span> |
| <span data-ttu-id="78795-158">20150601</span><span class="sxs-lookup"><span data-stu-id="78795-158">20150601</span></span> |<span data-ttu-id="78795-159">2</span><span class="sxs-lookup"><span data-stu-id="78795-159">2</span></span> |<span data-ttu-id="78795-160">4</span><span class="sxs-lookup"><span data-stu-id="78795-160">4</span></span> |
| <span data-ttu-id="78795-161">20150701</span><span class="sxs-lookup"><span data-stu-id="78795-161">20150701</span></span> |<span data-ttu-id="78795-162">3</span><span class="sxs-lookup"><span data-stu-id="78795-162">3</span></span> |<span data-ttu-id="78795-163">1</span><span class="sxs-lookup"><span data-stu-id="78795-163">1</span></span> |
| <span data-ttu-id="78795-164">20150801</span><span class="sxs-lookup"><span data-stu-id="78795-164">20150801</span></span> |<span data-ttu-id="78795-165">3</span><span class="sxs-lookup"><span data-stu-id="78795-165">3</span></span> |<span data-ttu-id="78795-166">1</span><span class="sxs-lookup"><span data-stu-id="78795-166">1</span></span> |
| <span data-ttu-id="78795-167">20150801</span><span class="sxs-lookup"><span data-stu-id="78795-167">20150801</span></span> |<span data-ttu-id="78795-168">3</span><span class="sxs-lookup"><span data-stu-id="78795-168">3</span></span> |<span data-ttu-id="78795-169">1</span><span class="sxs-lookup"><span data-stu-id="78795-169">1</span></span> |
| <span data-ttu-id="78795-170">20151001</span><span class="sxs-lookup"><span data-stu-id="78795-170">20151001</span></span> |<span data-ttu-id="78795-171">4</span><span class="sxs-lookup"><span data-stu-id="78795-171">4</span></span> |<span data-ttu-id="78795-172">2</span><span class="sxs-lookup"><span data-stu-id="78795-172">2</span></span> |
| <span data-ttu-id="78795-173">20151101</span><span class="sxs-lookup"><span data-stu-id="78795-173">20151101</span></span> |<span data-ttu-id="78795-174">4</span><span class="sxs-lookup"><span data-stu-id="78795-174">4</span></span> |<span data-ttu-id="78795-175">2</span><span class="sxs-lookup"><span data-stu-id="78795-175">2</span></span> |
| <span data-ttu-id="78795-176">20151201</span><span class="sxs-lookup"><span data-stu-id="78795-176">20151201</span></span> |<span data-ttu-id="78795-177">4</span><span class="sxs-lookup"><span data-stu-id="78795-177">4</span></span> |<span data-ttu-id="78795-178">2</span><span class="sxs-lookup"><span data-stu-id="78795-178">2</span></span> |

### <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="78795-179">4. Adım: Yeni yüklenmiş verilerinize ilişkin İstatistikler oluşturma</span><span class="sxs-lookup"><span data-stu-id="78795-179">Step 4: Create Statistics on your newly loaded data</span></span>
<span data-ttu-id="78795-180">Azure SQL Data Warehouse henüz istatistiklerin otomatik olarak oluşturulup güncelleştirilmesini desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="78795-180">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span> <span data-ttu-id="78795-181">Sipariş tooget hello en iyi performansı sorgularınızı, istatistikleri hello ilk yükleme işleminden sonra tüm tabloların tüm sütunlarda oluşturulması önemlidir veya hello verilerde önemli değişikliklerden.</span><span class="sxs-lookup"><span data-stu-id="78795-181">In order tooget hello best performance from your queries, it's important that statistics be created on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span> <span data-ttu-id="78795-182">Merhaba istatistikleri ayrıntılı bir açıklaması için bkz [istatistikleri] [ Statistics] konu hello geliştirme grubunu konuda.</span><span class="sxs-lookup"><span data-stu-id="78795-182">For a detailed explanation of statistics, see hello [Statistics][Statistics] topic in hello Develop group of topics.</span></span> <span data-ttu-id="78795-183">Nasıl toocreate istatistik oluşturacağınıza yönelik hello Bu örnekte yüklenen, hızlı bir örnek aşağıda verilmiştir</span><span class="sxs-lookup"><span data-stu-id="78795-183">Below is a quick example of how toocreate statistics on hello tabled loaded in this example</span></span>

<span data-ttu-id="78795-184">Bir sqlcmd isteminden CREATE STATISTICS deyimlerini aşağıdaki hello yürütün:</span><span class="sxs-lookup"><span data-stu-id="78795-184">Execute hello following CREATE STATISTICS statements from a sqlcmd prompt:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="export-data-from-sql-data-warehouse"></a><span data-ttu-id="78795-185">SQL Data Warehouse'dan veri aktarma</span><span class="sxs-lookup"><span data-stu-id="78795-185">Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="78795-186">Bu öğreticide SQL Data Warehouse'da bulunan bir tablodan veri dosyası oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="78795-186">In this tutorial, you will create a data file from a table in SQL Data Warehouse.</span></span> <span data-ttu-id="78795-187">Biz hello verileri DimDate2_export.txt adlı tooa yeni bir veri dosyası oluşturduğumuz verecektir.</span><span class="sxs-lookup"><span data-stu-id="78795-187">We will export hello data we created above tooa new data file called DimDate2_export.txt.</span></span>

### <a name="step-1-export-hello-data"></a><span data-ttu-id="78795-188">1. adım: hello verileri dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="78795-188">Step 1: Export hello data</span></span>
<span data-ttu-id="78795-189">Hello bcp yardımcı programını kullanarak, bağlanın ve komutu değiştirerek hello değerleri uygun şekilde aşağıdaki hello kullanarak verileri dışarı aktarma:</span><span class="sxs-lookup"><span data-stu-id="78795-189">Using hello bcp utility, you can connect and export data using hello following command replacing hello values as appropriate:</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="78795-190">Merhaba yeni dosyayı açarak verilerin doğru verildiğinden hello doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="78795-190">You can verify hello data was exported correctly by opening hello new file.</span></span> <span data-ttu-id="78795-191">Merhaba dosyasındaki Hello verileri hello metinle eşleşmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="78795-191">hello data in hello file should match hello text below:</span></span>

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
> <span data-ttu-id="78795-192">Toohello yapısı dağıtılmış sistemlerin hello veri sırası SQL Data Warehouse veritabanlarında aynı hello olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="78795-192">Due toohello nature of distributed systems, hello data order may not be hello same across SQL Data Warehouse databases.</span></span> <span data-ttu-id="78795-193">Başka bir seçenektir toouse hello **queryout** bcp toowrite bir sorgu işlevinin ayıklamak yerine hello tüm tabloyu dışarı aktarma.</span><span class="sxs-lookup"><span data-stu-id="78795-193">Another option is toouse hello **queryout** function of bcp toowrite a query extract rather than export hello entire table.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="78795-194">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="78795-194">Next steps</span></span>
<span data-ttu-id="78795-195">Yüklemeye genel bakış için bkz. [SQL Veri Ambarı'na veri yükleme][Load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="78795-195">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="78795-196">Geliştirme ile ilgili daha fazla ipucu için bkz. [SQL Veri Ambarı’nda geliştirmeye genel bakış][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="78795-196">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

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
