---
title: "CSV aaaLoad verilerden dosya Azure SQL veritabanına (bcp) | Microsoft Docs"
description: "Küçük boyutlu veriler için Azure SQL veritabanına bcp tooimport verileri kullanır."
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
ms.openlocfilehash: 9350e459aa844223820fbbd849a830cf0354d4e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-csv-into-azure-sql-database-flat-files"></a><span data-ttu-id="59759-103">CSV dosyasından Azure SQL Veritabanı'na veri yükleme (düz dosyalar)</span><span class="sxs-lookup"><span data-stu-id="59759-103">Load data from CSV into Azure SQL Database (flat files)</span></span>
<span data-ttu-id="59759-104">Azure SQL veritabanına bir CSV dosyasından hello bcp komut satırı yardımcı programını tooimport veri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59759-104">You can use hello bcp command-line utility tooimport data from a CSV file into Azure SQL Database.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="59759-105">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="59759-105">Before you begin</span></span>
### <a name="prerequisites"></a><span data-ttu-id="59759-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="59759-106">Prerequisites</span></span>
<span data-ttu-id="59759-107">Bu makalede toocomplete hello adımlar, gerekir:</span><span class="sxs-lookup"><span data-stu-id="59759-107">toocomplete hello steps in this article, you need:</span></span>

* <span data-ttu-id="59759-108">Azure SQL Database mantıksal sunucusu ve veritabanı</span><span class="sxs-lookup"><span data-stu-id="59759-108">An Azure SQL Database logical server and database</span></span>
* <span data-ttu-id="59759-109">Merhaba bcp komut satırı yardımcı programının yüklü olması</span><span class="sxs-lookup"><span data-stu-id="59759-109">hello bcp command-line utility installed</span></span>
* <span data-ttu-id="59759-110">Merhaba sqlcmd komut satırı yardımcı programının yüklü olması</span><span class="sxs-lookup"><span data-stu-id="59759-110">hello sqlcmd command-line utility installed</span></span>

<span data-ttu-id="59759-111">Hello hello bcp ve sqlcmd yardımcı programlarını indirebilirsiniz [Microsoft Download Center][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="59759-111">You can download hello bcp and sqlcmd utilities from hello [Microsoft Download Center][Microsoft Download Center].</span></span>

### <a name="data-in-ascii-or-utf-16-format"></a><span data-ttu-id="59759-112">ASCII veya UTF-16 biçimindeki veriler</span><span class="sxs-lookup"><span data-stu-id="59759-112">Data in ASCII or UTF-16 format</span></span>
<span data-ttu-id="59759-113">Bu öğreticiyi kendi verilerinizle deniyorsanız verilerinizin toouse hello ASCII veya UTF-8 bcp desteklemediğinden UTF-16 kodlamasını gerekir.</span><span class="sxs-lookup"><span data-stu-id="59759-113">If you are trying this tutorial with your own data, your data needs toouse hello ASCII or UTF-16 encoding since bcp does not support UTF-8.</span></span> 

## <a name="1-create-a-destination-table"></a><span data-ttu-id="59759-114">1. Hedef tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="59759-114">1. Create a destination table</span></span>
<span data-ttu-id="59759-115">Bir tablo, SQL veritabanında hello hedef tablo olarak tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="59759-115">Define a table in SQL Database as hello destination table.</span></span> <span data-ttu-id="59759-116">Merhaba tablodaki Hello sütun toohello veriler, her satır, veri dosyanızın karşılık gelmelidir.</span><span class="sxs-lookup"><span data-stu-id="59759-116">hello columns in hello table must correspond toohello data in each row of your data file.</span></span>

<span data-ttu-id="59759-117">toocreate tablo, bir komut istemi açın ve sqlcmd.exe toorun hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="59759-117">toocreate a table, open a command prompt and use sqlcmd.exe toorun hello following command:</span></span>

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


## <a name="2-create-a-source-data-file"></a><span data-ttu-id="59759-118">2. Kaynak veri dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="59759-118">2. Create a source data file</span></span>
<span data-ttu-id="59759-119">Veri satırlarını yeni bir metin dosyasına aşağıdaki not defteri ve kopyalama hello açın ve ardından bu dosya tooyour yerel geçici dizin, C:\Temp\DimDate2.txt kaydedin.</span><span class="sxs-lookup"><span data-stu-id="59759-119">Open Notepad and copy hello following lines of data into a new text file and then save this file tooyour local temp directory, C:\Temp\DimDate2.txt.</span></span> <span data-ttu-id="59759-120">Bu veri ASCII biçimindedir.</span><span class="sxs-lookup"><span data-stu-id="59759-120">This data is in ASCII format.</span></span>

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

<span data-ttu-id="59759-121">(İsteğe bağlı) tooexport bir SQL Server veritabanından kendi verilerinizi bir komut istemi açın ve hello aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="59759-121">(Optional) tooexport your own data from a SQL Server database, open a command prompt and run hello following command.</span></span> <span data-ttu-id="59759-122">TableName (Tablo Adı), ServerName (Sunucu Adı), DatabaseName (Veritabanı Adı), Username (Kullanıcı Adı) ve Password (Parola) alanlarına kendi bilgilerinizi yazın.</span><span class="sxs-lookup"><span data-stu-id="59759-122">Replace TableName, ServerName, DatabaseName, Username, and Password with your own information.</span></span>

```bcp
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t , 
```

## <a name="3-load-hello-data"></a><span data-ttu-id="59759-123">3. Merhaba veri yükleme</span><span class="sxs-lookup"><span data-stu-id="59759-123">3. Load hello data</span></span>
<span data-ttu-id="59759-124">tooload hello verileri, bir komut istemi açın ve aşağıdaki komut, sunucu adı, veritabanı adı, kullanıcı adı ve parola alanlarına kendi bilgilerinizi hello değerleri değiştirerek hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="59759-124">tooload hello data, open a command prompt and run hello following command, replacing hello values for Server Name, Database name, Username, and Password with your own information.</span></span>

```bcp
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ,
```

<span data-ttu-id="59759-125">Bu komut tooverify hello verilerin düzgün şekilde yüklendiğini kullanın</span><span class="sxs-lookup"><span data-stu-id="59759-125">Use this command tooverify hello data was loaded properly</span></span>

```bcp
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="59759-126">Merhaba sonuçları aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="59759-126">hello results should look like this:</span></span>

| <span data-ttu-id="59759-127">DateId</span><span class="sxs-lookup"><span data-stu-id="59759-127">DateId</span></span> | <span data-ttu-id="59759-128">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="59759-128">CalendarQuarter</span></span> | <span data-ttu-id="59759-129">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="59759-129">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="59759-130">20150101</span><span class="sxs-lookup"><span data-stu-id="59759-130">20150101</span></span> |<span data-ttu-id="59759-131">1</span><span class="sxs-lookup"><span data-stu-id="59759-131">1</span></span> |<span data-ttu-id="59759-132">3</span><span class="sxs-lookup"><span data-stu-id="59759-132">3</span></span> |
| <span data-ttu-id="59759-133">20150201</span><span class="sxs-lookup"><span data-stu-id="59759-133">20150201</span></span> |<span data-ttu-id="59759-134">1</span><span class="sxs-lookup"><span data-stu-id="59759-134">1</span></span> |<span data-ttu-id="59759-135">3</span><span class="sxs-lookup"><span data-stu-id="59759-135">3</span></span> |
| <span data-ttu-id="59759-136">20150301</span><span class="sxs-lookup"><span data-stu-id="59759-136">20150301</span></span> |<span data-ttu-id="59759-137">1</span><span class="sxs-lookup"><span data-stu-id="59759-137">1</span></span> |<span data-ttu-id="59759-138">3</span><span class="sxs-lookup"><span data-stu-id="59759-138">3</span></span> |
| <span data-ttu-id="59759-139">20150401</span><span class="sxs-lookup"><span data-stu-id="59759-139">20150401</span></span> |<span data-ttu-id="59759-140">2</span><span class="sxs-lookup"><span data-stu-id="59759-140">2</span></span> |<span data-ttu-id="59759-141">4</span><span class="sxs-lookup"><span data-stu-id="59759-141">4</span></span> |
| <span data-ttu-id="59759-142">20150501</span><span class="sxs-lookup"><span data-stu-id="59759-142">20150501</span></span> |<span data-ttu-id="59759-143">2</span><span class="sxs-lookup"><span data-stu-id="59759-143">2</span></span> |<span data-ttu-id="59759-144">4</span><span class="sxs-lookup"><span data-stu-id="59759-144">4</span></span> |
| <span data-ttu-id="59759-145">20150601</span><span class="sxs-lookup"><span data-stu-id="59759-145">20150601</span></span> |<span data-ttu-id="59759-146">2</span><span class="sxs-lookup"><span data-stu-id="59759-146">2</span></span> |<span data-ttu-id="59759-147">4</span><span class="sxs-lookup"><span data-stu-id="59759-147">4</span></span> |
| <span data-ttu-id="59759-148">20150701</span><span class="sxs-lookup"><span data-stu-id="59759-148">20150701</span></span> |<span data-ttu-id="59759-149">3</span><span class="sxs-lookup"><span data-stu-id="59759-149">3</span></span> |<span data-ttu-id="59759-150">1</span><span class="sxs-lookup"><span data-stu-id="59759-150">1</span></span> |
| <span data-ttu-id="59759-151">20150801</span><span class="sxs-lookup"><span data-stu-id="59759-151">20150801</span></span> |<span data-ttu-id="59759-152">3</span><span class="sxs-lookup"><span data-stu-id="59759-152">3</span></span> |<span data-ttu-id="59759-153">1</span><span class="sxs-lookup"><span data-stu-id="59759-153">1</span></span> |
| <span data-ttu-id="59759-154">20150801</span><span class="sxs-lookup"><span data-stu-id="59759-154">20150801</span></span> |<span data-ttu-id="59759-155">3</span><span class="sxs-lookup"><span data-stu-id="59759-155">3</span></span> |<span data-ttu-id="59759-156">1</span><span class="sxs-lookup"><span data-stu-id="59759-156">1</span></span> |
| <span data-ttu-id="59759-157">20151001</span><span class="sxs-lookup"><span data-stu-id="59759-157">20151001</span></span> |<span data-ttu-id="59759-158">4</span><span class="sxs-lookup"><span data-stu-id="59759-158">4</span></span> |<span data-ttu-id="59759-159">2</span><span class="sxs-lookup"><span data-stu-id="59759-159">2</span></span> |
| <span data-ttu-id="59759-160">20151101</span><span class="sxs-lookup"><span data-stu-id="59759-160">20151101</span></span> |<span data-ttu-id="59759-161">4</span><span class="sxs-lookup"><span data-stu-id="59759-161">4</span></span> |<span data-ttu-id="59759-162">2</span><span class="sxs-lookup"><span data-stu-id="59759-162">2</span></span> |
| <span data-ttu-id="59759-163">20151201</span><span class="sxs-lookup"><span data-stu-id="59759-163">20151201</span></span> |<span data-ttu-id="59759-164">4</span><span class="sxs-lookup"><span data-stu-id="59759-164">4</span></span> |<span data-ttu-id="59759-165">2</span><span class="sxs-lookup"><span data-stu-id="59759-165">2</span></span> |

## <a name="next-steps"></a><span data-ttu-id="59759-166">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="59759-166">Next steps</span></span>
<span data-ttu-id="59759-167">bir SQL Server veritabanı toomigrate bkz [SQL Server veritabanı geçiş](sql-database-cloud-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="59759-167">toomigrate a SQL Server database, see [SQL Server database migration](sql-database-cloud-migrate.md).</span></span>

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
