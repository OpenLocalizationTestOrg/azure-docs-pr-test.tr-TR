---
title: "aaaLoad örnek verileri SQL veri ambarında | Microsoft Docs"
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
ms.openlocfilehash: 3459c42f3aae51c27fd35db7874faf99e1e577e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="load-sample-data-into-sql-data-warehouse"></a><span data-ttu-id="30cec-103">SQL Data Warehouse'a örnek veri yükleme</span><span class="sxs-lookup"><span data-stu-id="30cec-103">Load sample data into SQL Data Warehouse</span></span>
<span data-ttu-id="30cec-104">Bu basit adımları tooload ve sorgu hello Adventure Works örnek veritabanını izleyin.</span><span class="sxs-lookup"><span data-stu-id="30cec-104">Follow these simple steps tooload and query hello Adventure Works Sample database.</span></span> <span data-ttu-id="30cec-105">Bu komut, ilk sqlcmd toorun tabloları ve görünümleri oluşturacak olan SQL kullanın.</span><span class="sxs-lookup"><span data-stu-id="30cec-105">These scripts first use sqlcmd toorun SQL which will create tables and views.</span></span> <span data-ttu-id="30cec-106">Tablo oluşturulduktan sonra hello betikleri bcp tooload verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="30cec-106">Once tables have been created, hello scripts will use bcp tooload data.</span></span>  <span data-ttu-id="30cec-107">Sqlcmd ve yüklü bcp zaten sahip değilseniz, bu bağlantıları çok izleyin[bcp yüklemek] [ install bcp] ve çok[sqlcmd yüklemek][install sqlcmd].</span><span class="sxs-lookup"><span data-stu-id="30cec-107">If you don't already have sqlcmd and bcp installed, follow these links too[install bcp][install bcp] and too[install sqlcmd][install sqlcmd].</span></span>

## <a name="load-sample-data"></a><span data-ttu-id="30cec-108">Örnek verileri yükleme</span><span class="sxs-lookup"><span data-stu-id="30cec-108">Load sample data</span></span>
1. <span data-ttu-id="30cec-109">Merhaba karşıdan [SQL Data Warehouse için Adventure Works örnek komut dosyaları] [ Adventure Works Sample Scripts for SQL Data Warehouse] zip dosyası.</span><span class="sxs-lookup"><span data-stu-id="30cec-109">Download hello [Adventure Works Sample Scripts for SQL Data Warehouse][Adventure Works Sample Scripts for SQL Data Warehouse] zip file.</span></span>
2. <span data-ttu-id="30cec-110">Yerel makinenizde indirilen ZIP tooa dizininden Hello dosyaları ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="30cec-110">Extract hello files from downloaded zip tooa directory on your local machine.</span></span>
3. <span data-ttu-id="30cec-111">Ayıklanan hello dosya aw_create.bat düzenleyin ve değişkenleri hello dosya hello üstünde bulunan aşağıdaki hello ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="30cec-111">Edit hello extracted file aw_create.bat and set hello following variables found at hello top of hello file.</span></span>  <span data-ttu-id="30cec-112">Hiçbir boşluk arasındaki hello "=" hello parametre emin tooleave olabilir.</span><span class="sxs-lookup"><span data-stu-id="30cec-112">Be sure tooleave no whitespace between hello "=" and hello parameter.</span></span>  <span data-ttu-id="30cec-113">Düzenlemeleriniz nasıl görünebileceği örnekleri aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="30cec-113">Below are examples of how your edits might look.</span></span>
   
    ```
    server=mylogicalserver.database.windows.net
    user=mydwuser
    password=Mydwpassw0rd
    database=mydwdatabase
    ```
4. <span data-ttu-id="30cec-114">Bir Windows komut isteminden çalıştırma hello aw_create.bat düzenlenemez.</span><span class="sxs-lookup"><span data-stu-id="30cec-114">From a Windows cmd prompt, run hello edited aw_create.bat.</span></span>  <span data-ttu-id="30cec-115">Düzenlenen aw_create.bat sürümünüz kaydettiğiniz hello dizininde olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="30cec-115">Be sure you are in hello directory where you saved your edited version of aw_create.bat.</span></span>
   <span data-ttu-id="30cec-116">Bu komut dosyası olacak...</span><span class="sxs-lookup"><span data-stu-id="30cec-116">This script will...</span></span>
   
   * <span data-ttu-id="30cec-117">Adventure Works tablolar veya veritabanınızda zaten görünümleri bırakın</span><span class="sxs-lookup"><span data-stu-id="30cec-117">Drop any Adventure Works tables or views that already exist in your database</span></span>
   * <span data-ttu-id="30cec-118">Merhaba Adventure Works tablolar ve görünümler oluşturma</span><span class="sxs-lookup"><span data-stu-id="30cec-118">Create hello Adventure Works tables and views</span></span>
   * <span data-ttu-id="30cec-119">BCP kullanarak her Adventure Works tablosu yükleme</span><span class="sxs-lookup"><span data-stu-id="30cec-119">Load each Adventure Works table using bcp</span></span>
   * <span data-ttu-id="30cec-120">Her Adventure Works tablo Hello satır sayılarını doğrula</span><span class="sxs-lookup"><span data-stu-id="30cec-120">Validate hello row counts for each Adventure Works table</span></span>
   * <span data-ttu-id="30cec-121">Her sütun için her Adventure Works tablo istatistikleri Topla</span><span class="sxs-lookup"><span data-stu-id="30cec-121">Collect statistics on every column for each Adventure Works table</span></span>

## <a name="query-sample-data"></a><span data-ttu-id="30cec-122">Örnek verileri Sorgulama</span><span class="sxs-lookup"><span data-stu-id="30cec-122">Query sample data</span></span>
<span data-ttu-id="30cec-123">SQL Data Warehouse'a bazı örnek veriler yüklenen sonra birkaç sorgu hızlı bir şekilde çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="30cec-123">Once you've loaded some sample data into your SQL Data Warehouse, you can quickly run a few queries.</span></span>  <span data-ttu-id="30cec-124">toorun bir sorgu hello açıklandığı gibi yeni oluşturulan tooyour Adventure Works Visual Studio ve SSDT, kullanarak Azure SQL DW veritabanında bağlanmak [sorgu Visual Studio ile] [ query with Visual Studio] belge.</span><span class="sxs-lookup"><span data-stu-id="30cec-124">toorun a query, connect tooyour newly created Adventure Works database in Azure SQL DW using Visual Studio and SSDT, as described in hello [query with Visual Studio][query with Visual Studio] document.</span></span>

<span data-ttu-id="30cec-125">Basit bir örneği hello çalışan tüm hello bilgilerini deyimi tooget seçin:</span><span class="sxs-lookup"><span data-stu-id="30cec-125">Example of simple select statement tooget all hello info of hello employees:</span></span>

```sql
SELECT * FROM DimEmployee;
```

<span data-ttu-id="30cec-126">GROUP BY toolook gibi yapıları hello toplam tutarı için tüm sales her gün kullanarak daha karmaşık bir sorgu örneği:</span><span class="sxs-lookup"><span data-stu-id="30cec-126">Example of a more complex query using constructs such as GROUP BY toolook at hello total amount for all sales on each day:</span></span>

```sql
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

<span data-ttu-id="30cec-127">WHERE yan tümcesi toofilter belirli bir tarihten önce siparişleri çıkışı ile bir SELECT örneği:</span><span class="sxs-lookup"><span data-stu-id="30cec-127">Example of a SELECT with a WHERE clause toofilter out orders from before a certain date:</span></span>

```
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
WHERE OrderDateKey > '20020801'
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

<span data-ttu-id="30cec-128">SQL veri ambarı SQL Server destekleyen neredeyse tüm T-SQL yapılarını destekler.</span><span class="sxs-lookup"><span data-stu-id="30cec-128">SQL Data Warehouse supports almost all T-SQL constructs which SQL Server supports.</span></span>  <span data-ttu-id="30cec-129">Farkları belgelenmiştir bizim [kodunu taşıma] [ migrate code] belgeleri.</span><span class="sxs-lookup"><span data-stu-id="30cec-129">Any differences are documented in our [migrate code][migrate code] documentation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="30cec-130">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="30cec-130">Next steps</span></span>
<span data-ttu-id="30cec-131">Bazı sorgular örnek verilerle bir fırsat tootry karşılaşmışsınız, nasıl çok denetleyin[geliştirmek][develop], [yük][load], veya [ geçiş] [ migrate] tooSQL veri ambarı.</span><span class="sxs-lookup"><span data-stu-id="30cec-131">Now that you've had a chance tootry some queries with sample data, check out how too[develop][develop], [load][load], or [migrate][migrate] tooSQL Data Warehouse.</span></span>

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
