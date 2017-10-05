---
title: "Veri yükleme CSV dosyasından Azure SQL veritabanına (bcp) | Microsoft Docs"
description: "Küçük veri boyutları için Azure SQL Veritabanına veri aktarırken bcp kullanır."
services: sql-database
documentationcenter: NA
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 875f9b8d-f1a1-4895-b717-f45570fb7f80
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 84bebab7763bb21f73880a6c8b367a62b0c137d3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="load-data-from-csv-into-azure-sql-database-flat-files"></a><span data-ttu-id="b71ae-103">CSV dosyasından Azure SQL Veritabanı'na veri yükleme (düz dosyalar)</span><span class="sxs-lookup"><span data-stu-id="b71ae-103">Load data from CSV into Azure SQL Database (flat files)</span></span>
<span data-ttu-id="b71ae-104">Bir CSV dosyasından Azure SQL Database’e veri aktarmak için bcp komut satırı yardımcı programını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b71ae-104">You can use the bcp command-line utility to import data from a CSV file into Azure SQL Database.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b71ae-105">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="b71ae-105">Before you begin</span></span>
### <a name="prerequisites"></a><span data-ttu-id="b71ae-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b71ae-106">Prerequisites</span></span>
<span data-ttu-id="b71ae-107">Bu makaledeki adımları tamamlamak için gerekir:</span><span class="sxs-lookup"><span data-stu-id="b71ae-107">To complete the steps in this article, you need:</span></span>

* <span data-ttu-id="b71ae-108">Azure SQL Database mantıksal sunucusu ve veritabanı</span><span class="sxs-lookup"><span data-stu-id="b71ae-108">An Azure SQL Database logical server and database</span></span>
* <span data-ttu-id="b71ae-109">bcp komut satırı yardımcı programının yüklü olması</span><span class="sxs-lookup"><span data-stu-id="b71ae-109">The bcp command-line utility installed</span></span>
* <span data-ttu-id="b71ae-110">sqlcmd komut satırı yardımcı programının yüklü olması</span><span class="sxs-lookup"><span data-stu-id="b71ae-110">The sqlcmd command-line utility installed</span></span>

<span data-ttu-id="b71ae-111">bcp ve sqlcmd yardımcı programlarını [Microsoft İndirme Merkezi][Microsoft Download Center]'nden indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b71ae-111">You can download the bcp and sqlcmd utilities from the [Microsoft Download Center][Microsoft Download Center].</span></span>

### <a name="data-in-ascii-or-utf-16-format"></a><span data-ttu-id="b71ae-112">ASCII veya UTF-16 biçimindeki veriler</span><span class="sxs-lookup"><span data-stu-id="b71ae-112">Data in ASCII or UTF-16 format</span></span>
<span data-ttu-id="b71ae-113">UTF-8 biçimi bcp tarafından desteklenmediğinden, bu öğreticiyi kendi verilerinizle deniyorsanız verilerinizin ASCII veya UTF-16 kodlamasını kullanıyor olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b71ae-113">If you are trying this tutorial with your own data, your data needs to use the ASCII or UTF-16 encoding since bcp does not support UTF-8.</span></span> 

## <a name="1-create-a-destination-table"></a><span data-ttu-id="b71ae-114">1. Hedef tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="b71ae-114">1. Create a destination table</span></span>
<span data-ttu-id="b71ae-115">SQL Veritabanı'nda bir tabloyu hedef tablo olarak tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="b71ae-115">Define a table in SQL Database as the destination table.</span></span> <span data-ttu-id="b71ae-116">Tablodaki sütunlar, veri dosyanızın tüm satırlarındaki verilere karşılık gelmelidir.</span><span class="sxs-lookup"><span data-stu-id="b71ae-116">The columns in the table must correspond to the data in each row of your data file.</span></span>

<span data-ttu-id="b71ae-117">Tablo oluşturmak için bir komut istemi açın ve sqlcmd.exe dosyasını kullanarak şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="b71ae-117">To create a table, open a command prompt and use sqlcmd.exe to run the following command:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    CREATE TABLE DimDate2
    (
        DateId INT NOT NULL,
        CalendarQuarter TINYINT NOT NULL,
        FiscalQuarter TINYINT NOT NULL
    )
    ;
"
```


## <a name="2-create-a-source-data-file"></a><span data-ttu-id="b71ae-118">2. Kaynak veri dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="b71ae-118">2. Create a source data file</span></span>
<span data-ttu-id="b71ae-119">Not Defteri'ni açın ve yeni bir metin dosyasına aşağıdaki veri satırlarını kopyalayıp dosyayı yerel geçici dizininize (C:\Temp\DimDate2.txt) kaydedin.</span><span class="sxs-lookup"><span data-stu-id="b71ae-119">Open Notepad and copy the following lines of data into a new text file and then save this file to your local temp directory, C:\Temp\DimDate2.txt.</span></span> <span data-ttu-id="b71ae-120">Bu veri ASCII biçimindedir.</span><span class="sxs-lookup"><span data-stu-id="b71ae-120">This data is in ASCII format.</span></span>

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

<span data-ttu-id="b71ae-121">(İsteğe bağlı) SQL Server veritabanından kendi verilerinizi dışarı aktarmak için bir komut istemi açın ve aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b71ae-121">(Optional) To export your own data from a SQL Server database, open a command prompt and run the following command.</span></span> <span data-ttu-id="b71ae-122">TableName (Tablo Adı), ServerName (Sunucu Adı), DatabaseName (Veritabanı Adı), Username (Kullanıcı Adı) ve Password (Parola) alanlarına kendi bilgilerinizi yazın.</span><span class="sxs-lookup"><span data-stu-id="b71ae-122">Replace TableName, ServerName, DatabaseName, Username, and Password with your own information.</span></span>

```bcp
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t , 
```

## <a name="3-load-the-data"></a><span data-ttu-id="b71ae-123">3. Verileri yükleme</span><span class="sxs-lookup"><span data-stu-id="b71ae-123">3. Load the data</span></span>
<span data-ttu-id="b71ae-124">Verileri yüklemek için bir komut satırı açın; Sunucu Adı, Veritabanı Adı, Kullanıcı Adı ve Parola alanlarına kendi bilgilerinizi yazarak aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b71ae-124">To load the data, open a command prompt and run the following command, replacing the values for Server Name, Database name, Username, and Password with your own information.</span></span>

```bcp
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ,
```

<span data-ttu-id="b71ae-125">Bu komutu kullanarak verilerin düzgün şekilde yüklendiğini doğrulayın</span><span class="sxs-lookup"><span data-stu-id="b71ae-125">Use this command to verify the data was loaded properly</span></span>

```bcp
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="b71ae-126">Sonuçlar şu şekilde görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="b71ae-126">The results should look like this:</span></span>

| <span data-ttu-id="b71ae-127">DateId</span><span class="sxs-lookup"><span data-stu-id="b71ae-127">DateId</span></span> | <span data-ttu-id="b71ae-128">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="b71ae-128">CalendarQuarter</span></span> | <span data-ttu-id="b71ae-129">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="b71ae-129">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b71ae-130">20150101</span><span class="sxs-lookup"><span data-stu-id="b71ae-130">20150101</span></span> |<span data-ttu-id="b71ae-131">1</span><span class="sxs-lookup"><span data-stu-id="b71ae-131">1</span></span> |<span data-ttu-id="b71ae-132">3</span><span class="sxs-lookup"><span data-stu-id="b71ae-132">3</span></span> |
| <span data-ttu-id="b71ae-133">20150201</span><span class="sxs-lookup"><span data-stu-id="b71ae-133">20150201</span></span> |<span data-ttu-id="b71ae-134">1</span><span class="sxs-lookup"><span data-stu-id="b71ae-134">1</span></span> |<span data-ttu-id="b71ae-135">3</span><span class="sxs-lookup"><span data-stu-id="b71ae-135">3</span></span> |
| <span data-ttu-id="b71ae-136">20150301</span><span class="sxs-lookup"><span data-stu-id="b71ae-136">20150301</span></span> |<span data-ttu-id="b71ae-137">1</span><span class="sxs-lookup"><span data-stu-id="b71ae-137">1</span></span> |<span data-ttu-id="b71ae-138">3</span><span class="sxs-lookup"><span data-stu-id="b71ae-138">3</span></span> |
| <span data-ttu-id="b71ae-139">20150401</span><span class="sxs-lookup"><span data-stu-id="b71ae-139">20150401</span></span> |<span data-ttu-id="b71ae-140">2</span><span class="sxs-lookup"><span data-stu-id="b71ae-140">2</span></span> |<span data-ttu-id="b71ae-141">4</span><span class="sxs-lookup"><span data-stu-id="b71ae-141">4</span></span> |
| <span data-ttu-id="b71ae-142">20150501</span><span class="sxs-lookup"><span data-stu-id="b71ae-142">20150501</span></span> |<span data-ttu-id="b71ae-143">2</span><span class="sxs-lookup"><span data-stu-id="b71ae-143">2</span></span> |<span data-ttu-id="b71ae-144">4</span><span class="sxs-lookup"><span data-stu-id="b71ae-144">4</span></span> |
| <span data-ttu-id="b71ae-145">20150601</span><span class="sxs-lookup"><span data-stu-id="b71ae-145">20150601</span></span> |<span data-ttu-id="b71ae-146">2</span><span class="sxs-lookup"><span data-stu-id="b71ae-146">2</span></span> |<span data-ttu-id="b71ae-147">4</span><span class="sxs-lookup"><span data-stu-id="b71ae-147">4</span></span> |
| <span data-ttu-id="b71ae-148">20150701</span><span class="sxs-lookup"><span data-stu-id="b71ae-148">20150701</span></span> |<span data-ttu-id="b71ae-149">3</span><span class="sxs-lookup"><span data-stu-id="b71ae-149">3</span></span> |<span data-ttu-id="b71ae-150">1</span><span class="sxs-lookup"><span data-stu-id="b71ae-150">1</span></span> |
| <span data-ttu-id="b71ae-151">20150801</span><span class="sxs-lookup"><span data-stu-id="b71ae-151">20150801</span></span> |<span data-ttu-id="b71ae-152">3</span><span class="sxs-lookup"><span data-stu-id="b71ae-152">3</span></span> |<span data-ttu-id="b71ae-153">1</span><span class="sxs-lookup"><span data-stu-id="b71ae-153">1</span></span> |
| <span data-ttu-id="b71ae-154">20150801</span><span class="sxs-lookup"><span data-stu-id="b71ae-154">20150801</span></span> |<span data-ttu-id="b71ae-155">3</span><span class="sxs-lookup"><span data-stu-id="b71ae-155">3</span></span> |<span data-ttu-id="b71ae-156">1</span><span class="sxs-lookup"><span data-stu-id="b71ae-156">1</span></span> |
| <span data-ttu-id="b71ae-157">20151001</span><span class="sxs-lookup"><span data-stu-id="b71ae-157">20151001</span></span> |<span data-ttu-id="b71ae-158">4</span><span class="sxs-lookup"><span data-stu-id="b71ae-158">4</span></span> |<span data-ttu-id="b71ae-159">2</span><span class="sxs-lookup"><span data-stu-id="b71ae-159">2</span></span> |
| <span data-ttu-id="b71ae-160">20151101</span><span class="sxs-lookup"><span data-stu-id="b71ae-160">20151101</span></span> |<span data-ttu-id="b71ae-161">4</span><span class="sxs-lookup"><span data-stu-id="b71ae-161">4</span></span> |<span data-ttu-id="b71ae-162">2</span><span class="sxs-lookup"><span data-stu-id="b71ae-162">2</span></span> |
| <span data-ttu-id="b71ae-163">20151201</span><span class="sxs-lookup"><span data-stu-id="b71ae-163">20151201</span></span> |<span data-ttu-id="b71ae-164">4</span><span class="sxs-lookup"><span data-stu-id="b71ae-164">4</span></span> |<span data-ttu-id="b71ae-165">2</span><span class="sxs-lookup"><span data-stu-id="b71ae-165">2</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b71ae-166">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b71ae-166">Next steps</span></span>
<span data-ttu-id="b71ae-167">Bir SQL Server veritabanına geçiş yapmak için bkz. [SQL Server veritabanı geçişi](sql-database-cloud-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="b71ae-167">To migrate a SQL Server database, see [SQL Server database migration](sql-database-cloud-migrate.md).</span></span>

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
