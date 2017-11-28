---
title: "SQL Data Warehouse'a örnek veri yükleme | Microsoft Docs"
description: "SQL Data Warehouse'a örnek veri yükleme"
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: e338ecf8-cfee-419b-b7b6-98108d381c62
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 1e0df958a2f18fe1e988168918e5cfd293f84e64
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="load-sample-data-into-sql-data-warehouse"></a><span data-ttu-id="16124-103">SQL Data Warehouse'a örnek veri yükleme</span><span class="sxs-lookup"><span data-stu-id="16124-103">Load sample data into SQL Data Warehouse</span></span>
<span data-ttu-id="16124-104">Yük ve Adventure Works örnek veritabanını sorgulamak için basit adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="16124-104">Follow these simple steps to load and query the Adventure Works Sample database.</span></span> <span data-ttu-id="16124-105">Bu komut dosyalarını sqlcmd tabloları ve görünümleri oluşturacak olan SQL çalıştırmak için ilk olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="16124-105">These scripts first use sqlcmd to run SQL which will create tables and views.</span></span> <span data-ttu-id="16124-106">Tabloları oluşturduktan sonra komut dosyaları veri yüklemek için bcp kullanır.</span><span class="sxs-lookup"><span data-stu-id="16124-106">Once tables have been created, the scripts will use bcp to load data.</span></span>  <span data-ttu-id="16124-107">Sqlcmd ve yüklü bcp zaten sahip değilseniz, bu bağlantıları izleyin [bcp yüklemek] [ install bcp] ve [sqlcmd yüklemek][install sqlcmd].</span><span class="sxs-lookup"><span data-stu-id="16124-107">If you don't already have sqlcmd and bcp installed, follow these links to [install bcp][install bcp] and to [install sqlcmd][install sqlcmd].</span></span>

## <a name="load-sample-data"></a><span data-ttu-id="16124-108">Örnek verileri yükleme</span><span class="sxs-lookup"><span data-stu-id="16124-108">Load sample data</span></span>
1. <span data-ttu-id="16124-109">Karşıdan [SQL Data Warehouse için Adventure Works örnek komut dosyaları] [ Adventure Works Sample Scripts for SQL Data Warehouse] zip dosyası.</span><span class="sxs-lookup"><span data-stu-id="16124-109">Download the [Adventure Works Sample Scripts for SQL Data Warehouse][Adventure Works Sample Scripts for SQL Data Warehouse] zip file.</span></span>
2. <span data-ttu-id="16124-110">Dosyaları indirilen ZIP yerel makinenizde bir dizine ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="16124-110">Extract the files from downloaded zip to a directory on your local machine.</span></span>
3. <span data-ttu-id="16124-111">Ayıklanan dosya aw_create.bat düzenleyin ve dosyanın üst kısmında bulunan aşağıdaki değişkenleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="16124-111">Edit the extracted file aw_create.bat and set the following variables found at the top of the file.</span></span>  <span data-ttu-id="16124-112">Hiçbir boşluk arasında ayırdığınızdan emin olun "=" ve parametresi.</span><span class="sxs-lookup"><span data-stu-id="16124-112">Be sure to leave no whitespace between the "=" and the parameter.</span></span>  <span data-ttu-id="16124-113">Düzenlemeleriniz nasıl görünebileceği örnekleri aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="16124-113">Below are examples of how your edits might look.</span></span>
   
    ```
    server=mylogicalserver.database.windows.net
    user=mydwuser
    password=Mydwpassw0rd
    database=mydwdatabase
    ```
4. <span data-ttu-id="16124-114">Bir Windows komut isteminden düzenlenen aw_create.bat çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="16124-114">From a Windows cmd prompt, run the edited aw_create.bat.</span></span>  <span data-ttu-id="16124-115">Düzenlenen aw_create.bat sürümünüz kaydettiğiniz dizininde olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="16124-115">Be sure you are in the directory where you saved your edited version of aw_create.bat.</span></span>
   <span data-ttu-id="16124-116">Bu komut dosyası olacak...</span><span class="sxs-lookup"><span data-stu-id="16124-116">This script will...</span></span>
   
   * <span data-ttu-id="16124-117">Adventure Works tablolar veya veritabanınızda zaten görünümleri bırakın</span><span class="sxs-lookup"><span data-stu-id="16124-117">Drop any Adventure Works tables or views that already exist in your database</span></span>
   * <span data-ttu-id="16124-118">Adventure Works tablolar ve görünümler oluşturma</span><span class="sxs-lookup"><span data-stu-id="16124-118">Create the Adventure Works tables and views</span></span>
   * <span data-ttu-id="16124-119">BCP kullanarak her Adventure Works tablosu yükleme</span><span class="sxs-lookup"><span data-stu-id="16124-119">Load each Adventure Works table using bcp</span></span>
   * <span data-ttu-id="16124-120">Her Adventure Works tablo satır sayılarını doğrula</span><span class="sxs-lookup"><span data-stu-id="16124-120">Validate the row counts for each Adventure Works table</span></span>
   * <span data-ttu-id="16124-121">Her sütun için her Adventure Works tablo istatistikleri Topla</span><span class="sxs-lookup"><span data-stu-id="16124-121">Collect statistics on every column for each Adventure Works table</span></span>

## <a name="query-sample-data"></a><span data-ttu-id="16124-122">Örnek verileri Sorgulama</span><span class="sxs-lookup"><span data-stu-id="16124-122">Query sample data</span></span>
<span data-ttu-id="16124-123">SQL Data Warehouse'a bazı örnek veriler yüklenen sonra birkaç sorgu hızlı bir şekilde çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="16124-123">Once you've loaded some sample data into your SQL Data Warehouse, you can quickly run a few queries.</span></span>  <span data-ttu-id="16124-124">Bir sorguyu çalıştırmak için yeni oluşturulan Adventure Works veritabanınızda Visual Studio ve SSDT, kullanarak Azure SQL DW açıklandığı gibi bağlanmak [sorgu Visual Studio ile] [ query with Visual Studio] belge.</span><span class="sxs-lookup"><span data-stu-id="16124-124">To run a query, connect to your newly created Adventure Works database in Azure SQL DW using Visual Studio and SSDT, as described in the [query with Visual Studio][query with Visual Studio] document.</span></span>

<span data-ttu-id="16124-125">Çalışanların tüm bilgileri almak için basit select deyimi örneği:</span><span class="sxs-lookup"><span data-stu-id="16124-125">Example of simple select statement to get all the info of the employees:</span></span>

```sql
SELECT * FROM DimEmployee;
```

<span data-ttu-id="16124-126">Her gün tüm satış toplam miktarı bakmak için GROUP BY gibi yapıları kullanarak daha karmaşık bir sorgu örneği:</span><span class="sxs-lookup"><span data-stu-id="16124-126">Example of a more complex query using constructs such as GROUP BY to look at the total amount for all sales on each day:</span></span>

```sql
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

<span data-ttu-id="16124-127">Belirli bir tarihten önce siparişleri filtrelemek için bir WHERE yan tümcesi ile bir SELECT örneği:</span><span class="sxs-lookup"><span data-stu-id="16124-127">Example of a SELECT with a WHERE clause to filter out orders from before a certain date:</span></span>

```
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
WHERE OrderDateKey > '20020801'
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

<span data-ttu-id="16124-128">SQL veri ambarı SQL Server destekleyen neredeyse tüm T-SQL yapılarını destekler.</span><span class="sxs-lookup"><span data-stu-id="16124-128">SQL Data Warehouse supports almost all T-SQL constructs which SQL Server supports.</span></span>  <span data-ttu-id="16124-129">Farkları belgelenmiştir bizim [kodunu taşıma] [ migrate code] belgeleri.</span><span class="sxs-lookup"><span data-stu-id="16124-129">Any differences are documented in our [migrate code][migrate code] documentation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16124-130">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="16124-130">Next steps</span></span>
<span data-ttu-id="16124-131">Nasıl yapılır, bazı sorgular örnek verilerle denemek için ettikten, kullanıma [geliştirmek][develop], [yük][load], veya [ geçiş] [ migrate] SQL veri ambarı.</span><span class="sxs-lookup"><span data-stu-id="16124-131">Now that you've had a chance to try some queries with sample data, check out how to [develop][develop], [load][load], or [migrate][migrate] to SQL Data Warehouse.</span></span>

<!--Image references-->

<!--Article references-->
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[query with Visual Studio]: sql-data-warehouse-query-visual-studio.md
[migrate code]: sql-data-warehouse-migrate-code.md
[install bcp]: sql-data-warehouse-load-with-bcp.md
[install sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md

<!--Other Web references-->
[Adventure Works Sample Scripts for SQL Data Warehouse]: https://migrhoststorage.blob.core.windows.net/sqldwsample/AdventureWorksSQLDW2012.zip
