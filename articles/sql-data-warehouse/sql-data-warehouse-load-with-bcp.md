---
title: "bcp yardımcı programını kullanarak SQL Veri Ambarı'na veri yükleme | Microsoft Belgeleri"
description: "bcp'nin ne olduğunu ve veri depolama senaryolarında nasıl kullanılacağını öğrenin."
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
ms.openlocfilehash: 7596eac10fdf53380d85128265430ce07b551fe3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-with-bcp"></a><span data-ttu-id="38cb3-103">BCP ile veri yükleme</span><span class="sxs-lookup"><span data-stu-id="38cb3-103">Load data with bcp</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="38cb3-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="38cb3-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)  
> * [<span data-ttu-id="38cb3-105">Data Factory</span><span class="sxs-lookup"><span data-stu-id="38cb3-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [<span data-ttu-id="38cb3-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="38cb3-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [<span data-ttu-id="38cb3-107">BCP</span><span class="sxs-lookup"><span data-stu-id="38cb3-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)
> 
> 

<span data-ttu-id="38cb3-108">**[bcp][bcp]**; SQL Server, veri dosyaları ve SQL Veri Ambarı arasında veri kopyalamanıza olanak sağlayan bir komut satırı toplu yükleme yardımcı programıdır.</span><span class="sxs-lookup"><span data-stu-id="38cb3-108">**[bcp][bcp]** is a command-line bulk load utility that allows you to copy data between SQL Server, data files, and SQL Data Warehouse.</span></span> <span data-ttu-id="38cb3-109">Çok sayıda satırı SQL Data Warehouse tablolarına aktarmak veya SQL Server tablolarından veri dosyalarına veri aktarmak için bcp yardımcı programını kullanın.</span><span class="sxs-lookup"><span data-stu-id="38cb3-109">Use bcp to import large numbers of rows into SQL Data Warehouse tables or to export data from SQL Server tables into data files.</span></span> <span data-ttu-id="38cb3-110">queryout seçeneğiyle kullanılmadığı sürece bcp programını kullanmak için Transact-SQL ile ilgili herhangi bir bilginizin olması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="38cb3-110">Except when used with the queryout option, bcp requires no knowledge of Transact-SQL.</span></span>

<span data-ttu-id="38cb3-111">bcp, nispeten küçük veri kümelerini SQL Data Warehouse veritabanına aktarmanın veya SQL Data Warehouse'dan dışarı aktarmanın hızlı ve kolay bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="38cb3-111">bcp is a quick and easy way to move smaller data sets into and out of a SQL Data Warehouse database.</span></span> <span data-ttu-id="38cb3-112">bcp aracılığıyla yükleme/ayıklama işlemi gerçekleştirmek için önerilen tam veri miktarı, Azure veri merkezine yönelik ağ bağlantınıza göre değişir.</span><span class="sxs-lookup"><span data-stu-id="38cb3-112">The exact amount of data that is recommended to load/extract via bcp will depend on you network connection to the Azure data center.</span></span>  <span data-ttu-id="38cb3-113">Genel olarak, boyut tabloları bcp aracılığıyla kolayca yüklenip ayıklanabilir ancak büyük miktarda veriyi yüklemek veya ayıklamak için bcp'nin kullanılması önerilmez.</span><span class="sxs-lookup"><span data-stu-id="38cb3-113">Generally, dimension tables can be loaded and extracted readily with bcp, however, bcp is not recommended for loading or extracting large volumes of data.</span></span>  <span data-ttu-id="38cb3-114">SQL Data Warehouse'un yüksek düzeyde paralel işleme mimarisinden faydalanma konusunda daha başarılı olduğundan, büyük miktarlarda veri yükleme ve ayıklama işlemleri için Polybase aracının kullanılması önerilir.</span><span class="sxs-lookup"><span data-stu-id="38cb3-114">Polybase is the recommended tool for loading and extracting large volumes of data as it does a better job leveraging the massively parallel processing architecture of SQL Data Warehouse.</span></span>

<span data-ttu-id="38cb3-115">bcp ile yapabilecekleriniz:</span><span class="sxs-lookup"><span data-stu-id="38cb3-115">With bcp you can:</span></span>

* <span data-ttu-id="38cb3-116">Basit bir komut satırı yardımcı programını kullanarak SQL Data Warehouse'a veri yükleme.</span><span class="sxs-lookup"><span data-stu-id="38cb3-116">Use a simple command-line utility to load data into SQL Data Warehouse.</span></span>
* <span data-ttu-id="38cb3-117">Basit bir komut satırı yardımcı programını kullanarak SQL Data Warehouse'dan veri ayıklama.</span><span class="sxs-lookup"><span data-stu-id="38cb3-117">Use a simple command-line utility to extract data from SQL Data Warehouse.</span></span>

<span data-ttu-id="38cb3-118">Bu öğreticide şunları nasıl yapacağınızı gösterilecek:</span><span class="sxs-lookup"><span data-stu-id="38cb3-118">This tutorial will show you how to:</span></span>

* <span data-ttu-id="38cb3-119">bcp in komutunu kullanarak bir tabloya veri aktarma</span><span class="sxs-lookup"><span data-stu-id="38cb3-119">Import data into a table using the bcp in command</span></span>
* <span data-ttu-id="38cb3-120">bcp out komutunu kullanarak bir tablodaki verileri dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="38cb3-120">Export data from a table uisng the bcp out command</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="38cb3-121">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="38cb3-121">Prerequisites</span></span>
<span data-ttu-id="38cb3-122">Bu öğreticide ilerleyebilmeniz için şunlar gereklidir:</span><span class="sxs-lookup"><span data-stu-id="38cb3-122">To step through this tutorial, you need:</span></span>

* <span data-ttu-id="38cb3-123">SQL Data Warehouse veritabanı</span><span class="sxs-lookup"><span data-stu-id="38cb3-123">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="38cb3-124">bcp komut satırı yardımcı programının yüklü olması</span><span class="sxs-lookup"><span data-stu-id="38cb3-124">The bcp command line utility installed</span></span>
* <span data-ttu-id="38cb3-125">SQLCMD komut satırı yardımcı programının yüklü olması</span><span class="sxs-lookup"><span data-stu-id="38cb3-125">The SQLCMD command line utility installed</span></span>

> [!NOTE]
> <span data-ttu-id="38cb3-126">bcp ve sqlcmd yardımcı programlarını [Microsoft İndirme Merkezi][Microsoft Download Center]'nden indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38cb3-126">You can download the bcp and sqlcmd utilities from the [Microsoft Download Center][Microsoft Download Center].</span></span>
> 
> 

## <a name="import-data-into-sql-data-warehouse"></a><span data-ttu-id="38cb3-127">SQL Data Warehouse'a veri aktarma</span><span class="sxs-lookup"><span data-stu-id="38cb3-127">Import data into SQL Data Warehouse</span></span>
<span data-ttu-id="38cb3-128">Bu öğreticide, Azure SQL Data Warehouse'da bir tablo oluşturup tabloya veri aktaracaksınız.</span><span class="sxs-lookup"><span data-stu-id="38cb3-128">In this tutorial, you will create a table in Azure SQL Data Warehouse and import data into the table.</span></span>

### <a name="step-1-create-a-table-in-azure-sql-data-warehouse"></a><span data-ttu-id="38cb3-129">1. Adım: Azure SQL Data Warehouse'da tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="38cb3-129">Step 1: Create a table in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="38cb3-130">Örneğinizde bir tablo oluşturmak için aşağıdaki sorguyu çalıştırmak üzere bir komut isteminden sqlcmd yardımcı programını kullanın:</span><span class="sxs-lookup"><span data-stu-id="38cb3-130">From a command prompt, use sqlcmd to run the following query to create a table on your instance:</span></span>

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
> <span data-ttu-id="38cb3-131">SQL Veri Ambarı'nda tablo oluşturma ve WITH yan tümcesinde bulunan seçenekler hakkında daha fazla bilgi için bkz. [Tabloya Genel Bakış][Table Overview] veya [CREATE TABLE söz dizimi][CREATE TABLE syntax].</span><span class="sxs-lookup"><span data-stu-id="38cb3-131">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse and the  options available in the WITH clause.</span></span>
> 
> 

### <a name="step-2-create-a-source-data-file"></a><span data-ttu-id="38cb3-132">2. Adım: Kaynak veri dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="38cb3-132">Step 2: Create a source data file</span></span>
<span data-ttu-id="38cb3-133">Not Defteri'ni açın ve yeni bir metin dosyasına aşağıdaki veri satırlarını kopyalayıp dosyayı yerel geçici dizininize (C:\Temp\DimDate2.txt) kaydedin.</span><span class="sxs-lookup"><span data-stu-id="38cb3-133">Open Notepad and copy the following lines of data into a new text file and then save this file to your local temp directory, C:\Temp\DimDate2.txt.</span></span>

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
> <span data-ttu-id="38cb3-134">bcp.exe dosyasının UTF-8 dosya kodlamasını desteklemediğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="38cb3-134">It is important to remember that bcp.exe does not support the UTF-8 file encoding.</span></span> <span data-ttu-id="38cb3-135">bcp.exe dosyasını kullanırken lütfen ASCII dosyalarını veya UTF-16 kodlu dosyaları kullanın.</span><span class="sxs-lookup"><span data-stu-id="38cb3-135">Please use ASCII files or UTF-16 encoded files when using bcp.exe.</span></span>
> 
> 

### <a name="step-3-connect-and-import-the-data"></a><span data-ttu-id="38cb3-136">3. Adım: Bağlanma ve verileri içeri aktarma</span><span class="sxs-lookup"><span data-stu-id="38cb3-136">Step 3: Connect and import the data</span></span>
<span data-ttu-id="38cb3-137">bcp ile aşağıdaki komutu kullanıp değerleri uygun şekilde değiştirerek bağlanabilir ve verileri içeri aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38cb3-137">Using bcp, you can connect and import the data using the following command replacing the values as appropriate:</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="38cb3-138">sqlcmd ile aşağıdaki sorguyu çalıştırarak verilerin yüklendiğini doğrulayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="38cb3-138">You can verify the data was loaded by running the following query using sqlcmd:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="38cb3-139">Bu işlem sonrasında şu sonuçların döndürülmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="38cb3-139">This should return the following results:</span></span>

| <span data-ttu-id="38cb3-140">DateId</span><span class="sxs-lookup"><span data-stu-id="38cb3-140">DateId</span></span> | <span data-ttu-id="38cb3-141">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="38cb3-141">CalendarQuarter</span></span> | <span data-ttu-id="38cb3-142">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="38cb3-142">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38cb3-143">20150101</span><span class="sxs-lookup"><span data-stu-id="38cb3-143">20150101</span></span> |<span data-ttu-id="38cb3-144">1</span><span class="sxs-lookup"><span data-stu-id="38cb3-144">1</span></span> |<span data-ttu-id="38cb3-145">3</span><span class="sxs-lookup"><span data-stu-id="38cb3-145">3</span></span> |
| <span data-ttu-id="38cb3-146">20150201</span><span class="sxs-lookup"><span data-stu-id="38cb3-146">20150201</span></span> |<span data-ttu-id="38cb3-147">1</span><span class="sxs-lookup"><span data-stu-id="38cb3-147">1</span></span> |<span data-ttu-id="38cb3-148">3</span><span class="sxs-lookup"><span data-stu-id="38cb3-148">3</span></span> |
| <span data-ttu-id="38cb3-149">20150301</span><span class="sxs-lookup"><span data-stu-id="38cb3-149">20150301</span></span> |<span data-ttu-id="38cb3-150">1</span><span class="sxs-lookup"><span data-stu-id="38cb3-150">1</span></span> |<span data-ttu-id="38cb3-151">3</span><span class="sxs-lookup"><span data-stu-id="38cb3-151">3</span></span> |
| <span data-ttu-id="38cb3-152">20150401</span><span class="sxs-lookup"><span data-stu-id="38cb3-152">20150401</span></span> |<span data-ttu-id="38cb3-153">2</span><span class="sxs-lookup"><span data-stu-id="38cb3-153">2</span></span> |<span data-ttu-id="38cb3-154">4</span><span class="sxs-lookup"><span data-stu-id="38cb3-154">4</span></span> |
| <span data-ttu-id="38cb3-155">20150501</span><span class="sxs-lookup"><span data-stu-id="38cb3-155">20150501</span></span> |<span data-ttu-id="38cb3-156">2</span><span class="sxs-lookup"><span data-stu-id="38cb3-156">2</span></span> |<span data-ttu-id="38cb3-157">4</span><span class="sxs-lookup"><span data-stu-id="38cb3-157">4</span></span> |
| <span data-ttu-id="38cb3-158">20150601</span><span class="sxs-lookup"><span data-stu-id="38cb3-158">20150601</span></span> |<span data-ttu-id="38cb3-159">2</span><span class="sxs-lookup"><span data-stu-id="38cb3-159">2</span></span> |<span data-ttu-id="38cb3-160">4</span><span class="sxs-lookup"><span data-stu-id="38cb3-160">4</span></span> |
| <span data-ttu-id="38cb3-161">20150701</span><span class="sxs-lookup"><span data-stu-id="38cb3-161">20150701</span></span> |<span data-ttu-id="38cb3-162">3</span><span class="sxs-lookup"><span data-stu-id="38cb3-162">3</span></span> |<span data-ttu-id="38cb3-163">1</span><span class="sxs-lookup"><span data-stu-id="38cb3-163">1</span></span> |
| <span data-ttu-id="38cb3-164">20150801</span><span class="sxs-lookup"><span data-stu-id="38cb3-164">20150801</span></span> |<span data-ttu-id="38cb3-165">3</span><span class="sxs-lookup"><span data-stu-id="38cb3-165">3</span></span> |<span data-ttu-id="38cb3-166">1</span><span class="sxs-lookup"><span data-stu-id="38cb3-166">1</span></span> |
| <span data-ttu-id="38cb3-167">20150801</span><span class="sxs-lookup"><span data-stu-id="38cb3-167">20150801</span></span> |<span data-ttu-id="38cb3-168">3</span><span class="sxs-lookup"><span data-stu-id="38cb3-168">3</span></span> |<span data-ttu-id="38cb3-169">1</span><span class="sxs-lookup"><span data-stu-id="38cb3-169">1</span></span> |
| <span data-ttu-id="38cb3-170">20151001</span><span class="sxs-lookup"><span data-stu-id="38cb3-170">20151001</span></span> |<span data-ttu-id="38cb3-171">4</span><span class="sxs-lookup"><span data-stu-id="38cb3-171">4</span></span> |<span data-ttu-id="38cb3-172">2</span><span class="sxs-lookup"><span data-stu-id="38cb3-172">2</span></span> |
| <span data-ttu-id="38cb3-173">20151101</span><span class="sxs-lookup"><span data-stu-id="38cb3-173">20151101</span></span> |<span data-ttu-id="38cb3-174">4</span><span class="sxs-lookup"><span data-stu-id="38cb3-174">4</span></span> |<span data-ttu-id="38cb3-175">2</span><span class="sxs-lookup"><span data-stu-id="38cb3-175">2</span></span> |
| <span data-ttu-id="38cb3-176">20151201</span><span class="sxs-lookup"><span data-stu-id="38cb3-176">20151201</span></span> |<span data-ttu-id="38cb3-177">4</span><span class="sxs-lookup"><span data-stu-id="38cb3-177">4</span></span> |<span data-ttu-id="38cb3-178">2</span><span class="sxs-lookup"><span data-stu-id="38cb3-178">2</span></span> |

### <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="38cb3-179">4. Adım: Yeni yüklenmiş verilerinize ilişkin İstatistikler oluşturma</span><span class="sxs-lookup"><span data-stu-id="38cb3-179">Step 4: Create Statistics on your newly loaded data</span></span>
<span data-ttu-id="38cb3-180">Azure SQL Data Warehouse henüz istatistiklerin otomatik olarak oluşturulup güncelleştirilmesini desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="38cb3-180">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span> <span data-ttu-id="38cb3-181">Sorgularınızdan en iyi performansı elde edebilmeniz için ilk yüklemeden veya verilerdeki önemli değişikliklerden sonra her tablonun her sütununa ilişkin istatistiklerin oluşturulması önemlidir.</span><span class="sxs-lookup"><span data-stu-id="38cb3-181">In order to get the best performance from your queries, it's important that statistics be created on all columns of all tables after the first load or any substantial changes occur in the data.</span></span> <span data-ttu-id="38cb3-182">İstatistikler hakkında ayrıntılı bir açıklama için Geliştirme ile ilgili konu başlığı grubunda yer alan [İstatistikler][Statistics] bölümüne göz atın.</span><span class="sxs-lookup"><span data-stu-id="38cb3-182">For a detailed explanation of statistics, see the [Statistics][Statistics] topic in the Develop group of topics.</span></span> <span data-ttu-id="38cb3-183">Aşağıda bu örnekte yüklenen tablolar için nasıl istatistik oluşturacağınıza yönelik kısa bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="38cb3-183">Below is a quick example of how to create statistics on the tabled loaded in this example</span></span>

<span data-ttu-id="38cb3-184">Bir sqlcmd isteminden şu CREATE STATISTICS deyimlerini yürütün:</span><span class="sxs-lookup"><span data-stu-id="38cb3-184">Execute the following CREATE STATISTICS statements from a sqlcmd prompt:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="export-data-from-sql-data-warehouse"></a><span data-ttu-id="38cb3-185">SQL Data Warehouse'dan veri aktarma</span><span class="sxs-lookup"><span data-stu-id="38cb3-185">Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="38cb3-186">Bu öğreticide SQL Data Warehouse'da bulunan bir tablodan veri dosyası oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="38cb3-186">In this tutorial, you will create a data file from a table in SQL Data Warehouse.</span></span> <span data-ttu-id="38cb3-187">Yukarıda oluşturduğumuz verileri DimDate2_export.txt adlı dosyaya aktaracağız.</span><span class="sxs-lookup"><span data-stu-id="38cb3-187">We will export the data we created above to a new data file called DimDate2_export.txt.</span></span>

### <a name="step-1-export-the-data"></a><span data-ttu-id="38cb3-188">1. Adım: Verileri dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="38cb3-188">Step 1: Export the data</span></span>
<span data-ttu-id="38cb3-189">bcp yardımcı programı ile aşağıdaki komutu kullanıp değerleri uygun şekilde değiştirerek bağlanabilir ve verileri içeri aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38cb3-189">Using the bcp utility, you can connect and export data using the following command replacing the values as appropriate:</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="38cb3-190">Yeni dosyayı açarak verilerin düzgün bir şekilde dışarı aktarıldığını doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38cb3-190">You can verify the data was exported correctly by opening the new file.</span></span> <span data-ttu-id="38cb3-191">Dosyadaki verilerin aşağıdaki metinle eşleşmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="38cb3-191">The data in the file should match the text below:</span></span>

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
> <span data-ttu-id="38cb3-192">Dağıtılmış sistemlerin yapısı gereği, veri sırası SQL Data Warehouse veritabanlarında aynı olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="38cb3-192">Due to the nature of distributed systems, the data order may not be the same across SQL Data Warehouse databases.</span></span> <span data-ttu-id="38cb3-193">Tüm tabloyu dışarı aktarmak yerine, bcp yardımcı programının **queryout** işlevini kullanarak bir sorgu ayıklaması da yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38cb3-193">Another option is to use the **queryout** function of bcp to write a query extract rather than export the entire table.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="38cb3-194">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="38cb3-194">Next steps</span></span>
<span data-ttu-id="38cb3-195">Yüklemeye genel bakış için bkz. [SQL Veri Ambarı'na veri yükleme][Load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="38cb3-195">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="38cb3-196">Geliştirme ile ilgili daha fazla ipucu için bkz. [SQL Veri Ambarı’nda geliştirmeye genel bakış][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="38cb3-196">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

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
