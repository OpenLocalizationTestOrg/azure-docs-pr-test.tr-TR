---
title: "Azure Data Factory yinelenebilir kopyasında | Microsoft Docs"
description: "Yinelenen verileri kopyalayan bir dilim birden çok kez çalıştırma olsa bile kaçının öğrenin."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 5b88a235915bf35fec701eee4a5f80beb4a67632
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="repeatable-copy-in-azure-data-factory"></a><span data-ttu-id="cac3e-103">Azure Data Factory yinelenebilir kopyalama</span><span class="sxs-lookup"><span data-stu-id="cac3e-103">Repeatable copy in Azure Data Factory</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="cac3e-104">İlişkisel kaynaklardan yinelenebilir okuma</span><span class="sxs-lookup"><span data-stu-id="cac3e-104">Repeatable read from relational sources</span></span>
<span data-ttu-id="cac3e-105">İlişkisel veri kopyalama verileri depoladığında, Yinelenebilirlik istenmeyen sonuçları önlemek için göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="cac3e-105">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="cac3e-106">Azure Data Factory'de bir dilim el ile çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cac3e-106">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="cac3e-107">Bir hata oluştuğunda bir dilimi yeniden çalıştırmak için bir veri kümesi için yeniden deneme ilkesi de yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cac3e-107">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="cac3e-108">Bir dilim iki yolla yeniden çalıştırıldığında, aynı veri dilimi çalıştırmak kaç kez geçtiğinden bağımsız okuduğunuzdan emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="cac3e-108">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span>  
 
> [!NOTE]
> <span data-ttu-id="cac3e-109">Aşağıdaki örnekler için Azure SQL ancak dikdörtgen veri kümeleri destekleyen herhangi bir veri deposuna uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="cac3e-109">The following samples are for Azure SQL but are applicable to any data store that supports rectangular datasets.</span></span> <span data-ttu-id="cac3e-110">Ayarlamanız gerekebilir **türü** kaynağının ve **sorgu** özelliği (örneğin: Sorgu sqlReaderQuery yerine) verilerini depolamak.</span><span class="sxs-lookup"><span data-stu-id="cac3e-110">You may have to adjust the **type** of source and the **query** property (for example: query instead of sqlReaderQuery) for the data store.</span></span>   

<span data-ttu-id="cac3e-111">Genellikle, ilişkisel depoları okurken, yalnızca o dilim karşılık gelen verileri okumak istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="cac3e-111">Usually, when reading from relational stores, you want to read only the data corresponding to that slice.</span></span> <span data-ttu-id="cac3e-112">Bunu yapmanın bir yolu, Azure Data Factory'de kullanılabilir WindowStart ve WindowEnd sistem değişkenleri kullanılarak olacaktır.</span><span class="sxs-lookup"><span data-stu-id="cac3e-112">A way to do so would be by using the WindowStart and WindowEnd system variables available in Azure Data Factory.</span></span> <span data-ttu-id="cac3e-113">Azure Data Factory'de burada işlevleri ve değişkenler hakkında bilgi [Azure Data Factory - işlevler ve sistem değişkenleri](data-factory-functions-variables.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="cac3e-113">Read about the variables and functions in Azure Data Factory here in the [Azure Data Factory - Functions and System Variables](data-factory-functions-variables.md) article.</span></span> <span data-ttu-id="cac3e-114">Örnek:</span><span class="sxs-lookup"><span data-stu-id="cac3e-114">Example:</span></span> 

```json
"source": {
    "type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm\\'', WindowStart, WindowEnd)"
},
```
<span data-ttu-id="cac3e-115">Bu sorgu MyTable tablosundan (WindowStart -> WindowEnd) dilim süresi aralığını kalan verileri okur.</span><span class="sxs-lookup"><span data-stu-id="cac3e-115">This query reads data that falls in the slice duration range (WindowStart -> WindowEnd) from the table MyTable.</span></span> <span data-ttu-id="cac3e-116">Bu dilimin yeniden çalıştırın, ayrıca her zaman aynı veri okuduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="cac3e-116">Rerun of this slice would also always ensure that the same data is read.</span></span> 

<span data-ttu-id="cac3e-117">Diğer durumlarda, tüm tablo bölümünü okumanız önerilir ve sqlReaderQuery gibi tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="cac3e-117">In other cases, you may wish to read the entire table and may define the sqlReaderQuery as follows:</span></span>

```json
"source": 
{            
    "type": "SqlSource",
    "sqlReaderQuery": "select * from MyTable"
},
```

## <a name="repeatable-write-to-sqlsink"></a><span data-ttu-id="cac3e-118">SqlSink yinelenebilir yazma</span><span class="sxs-lookup"><span data-stu-id="cac3e-118">Repeatable write to SqlSink</span></span>
<span data-ttu-id="cac3e-119">Veri kopyalama işlemi sırasında **Azure SQL/SQL Server** diğer veri depolarına, Yinelenebilirlik istenmeyen sonuçları önlemek için göz önünde bulundurmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="cac3e-119">When copying data to **Azure SQL/SQL Server** from other data stores, you need to keep repeatability in mind to avoid unintended outcomes.</span></span> 

<span data-ttu-id="cac3e-120">Azure SQL/SQL Server veritabanına veri kopyalama, kopyalama etkinliği verileri varsayılan olarak havuz tabloya ekler.</span><span class="sxs-lookup"><span data-stu-id="cac3e-120">When copying data to Azure SQL/SQL Server Database, the copy activity appends data to the sink table by default.</span></span> <span data-ttu-id="cac3e-121">Bir Azure SQL/SQL Server veritabanında aşağıdaki tabloya iki kayıtlarını içeren bir CSV (virgülle ayrılmış değerler) dosyasından veri kopyalama söyleyin.</span><span class="sxs-lookup"><span data-stu-id="cac3e-121">Say, you are copying data from a CSV (comma-separated values) file containing two records to the following table in an Azure SQL/SQL Server Database.</span></span> <span data-ttu-id="cac3e-122">Bir dilim çalıştığında, iki kayıt SQL tablosuna kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="cac3e-122">When a slice runs, the two records are copied to the SQL table.</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

<span data-ttu-id="cac3e-123">Kaynak dosyasında hata buldu ve miktarını aşağı boru 2-4 güncelleştirilmiş varsayalım.</span><span class="sxs-lookup"><span data-stu-id="cac3e-123">Suppose you found errors in source file and updated the quantity of Down Tube from 2 to 4.</span></span> <span data-ttu-id="cac3e-124">Veri dilimi belirli bir döneme ait el ile yeniden, Azure SQL/SQL Server veritabanına eklenen iki yeni kayıtlar bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cac3e-124">If you rerun the data slice for that period manually, you’ll find two new records appended to Azure SQL/SQL Server Database.</span></span> <span data-ttu-id="cac3e-125">Bu örnek, tablodaki sütunların hiçbiri birincil anahtar kısıtlaması olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="cac3e-125">This example assumes that none of the columns in the table has the primary key constraint.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="cac3e-126">Bu davranışı önlemek için aşağıdaki iki mekanizma birini kullanarak UPSERT semantiği belirtmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="cac3e-126">To avoid this behavior, you need to specify UPSERT semantics by using one of the following two mechanisms:</span></span>

### <a name="mechanism-1-using-sqlwritercleanupscript"></a><span data-ttu-id="cac3e-127">Mekanizması 1: sqlWriterCleanupScript kullanma</span><span class="sxs-lookup"><span data-stu-id="cac3e-127">Mechanism 1: using sqlWriterCleanupScript</span></span>
<span data-ttu-id="cac3e-128">Kullanabileceğiniz **sqlWriterCleanupScript** bir dilim çalıştırıldığında verileri eklemeden önce havuz tablodaki verileri temizlemek için özellik.</span><span class="sxs-lookup"><span data-stu-id="cac3e-128">You can use the **sqlWriterCleanupScript** property to clean up data from the sink table before inserting the data when a slice is run.</span></span> 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

<span data-ttu-id="cac3e-129">Bir dilim çalıştığında, temizleme betiğini dilimi SQL tablosundan karşılık gelen verileri silmek için önce çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="cac3e-129">When a slice runs, the cleanup script is run first to delete data that corresponds to the slice from the SQL table.</span></span> <span data-ttu-id="cac3e-130">Kopyalama etkinliği, ardından veri SQL tablosuna ekler.</span><span class="sxs-lookup"><span data-stu-id="cac3e-130">The copy activity then inserts data into the SQL Table.</span></span> <span data-ttu-id="cac3e-131">Dilimi yeniden çalıştırın, miktarı güncelleştirilir istenen şekilde.</span><span class="sxs-lookup"><span data-stu-id="cac3e-131">If the slice is rerun, the quantity is updated as desired.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="cac3e-132">Düz rondela kaydı özgün csv kaldırılana varsayalım.</span><span class="sxs-lookup"><span data-stu-id="cac3e-132">Suppose the Flat Washer record is removed from the original csv.</span></span> <span data-ttu-id="cac3e-133">Dilim yeniden çalıştırma aşağıdaki sonucu oluşturur:</span><span class="sxs-lookup"><span data-stu-id="cac3e-133">Then rerunning the slice would produce the following result:</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="cac3e-134">Kopyalama etkinliği, dilim karşılık gelen verileri silmek için temizleme betiğini verdi.</span><span class="sxs-lookup"><span data-stu-id="cac3e-134">The copy activity ran the cleanup script to delete the corresponding data for that slice.</span></span> <span data-ttu-id="cac3e-135">Giriş (hangi sonra yalnızca bir kayıt bulunan) csv okuma sonra ve tabloya eklenen.</span><span class="sxs-lookup"><span data-stu-id="cac3e-135">Then it read the input from the csv (which then contained only one record) and inserted it into the Table.</span></span> 

### <a name="mechanism-2-using-sliceidentifiercolumnname"></a><span data-ttu-id="cac3e-136">Mekanizması 2: Sliceıdentifiercolumnname kullanma</span><span class="sxs-lookup"><span data-stu-id="cac3e-136">Mechanism 2: using sliceIdentifierColumnName</span></span>
> [!IMPORTANT]
> <span data-ttu-id="cac3e-137">Şu anda Sliceıdentifiercolumnname Azure SQL veri ambarı için desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="cac3e-137">Currently, sliceIdentifierColumnName is not supported for Azure SQL Data Warehouse.</span></span> 

<span data-ttu-id="cac3e-138">Yinelenebilirlik elde etmek için ikinci hedef tablo ayrılmış sütun (Sliceıdentifiercolumnname) sağlayarak mekanizmadır.</span><span class="sxs-lookup"><span data-stu-id="cac3e-138">The second mechanism to achieve repeatability is by having a dedicated column (sliceIdentifierColumnName) in the target Table.</span></span> <span data-ttu-id="cac3e-139">Azure Data Factory tarafından bu sütun kaynak ve hedef eşitlenmesine emin olmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="cac3e-139">This column would be used by Azure Data Factory to ensure the source and destination stay synchronized.</span></span> <span data-ttu-id="cac3e-140">Bu yaklaşım, değiştirme veya hedef SQL tablo şemasını tanımlama esneklik olduğunda çalışır.</span><span class="sxs-lookup"><span data-stu-id="cac3e-140">This approach works when there is flexibility in changing or defining the destination SQL Table schema.</span></span> 

<span data-ttu-id="cac3e-141">Bu sütun Yinelenebilirlik amaçlar için Azure Data Factory tarafından kullanılır ve işlem sırasında tablonun herhangi bir şema değişikliği Azure Data Factory yapmaz.</span><span class="sxs-lookup"><span data-stu-id="cac3e-141">This column is used by Azure Data Factory for repeatability purposes and in the process Azure Data Factory does not make any schema changes to the Table.</span></span> <span data-ttu-id="cac3e-142">Bu yaklaşımı kullanmak için yol:</span><span class="sxs-lookup"><span data-stu-id="cac3e-142">Way to use this approach:</span></span>

1. <span data-ttu-id="cac3e-143">Türünde bir sütun tanımlamak **ikili (32)** hedef SQL tablosu.</span><span class="sxs-lookup"><span data-stu-id="cac3e-143">Define a column of type **binary (32)** in the destination SQL Table.</span></span> <span data-ttu-id="cac3e-144">Bu sütunda hiç bir kısıtlama olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="cac3e-144">There should be no constraints on this column.</span></span> <span data-ttu-id="cac3e-145">Şimdi bu sütun, bu örnek için AdfSliceIdentifier adlandırın.</span><span class="sxs-lookup"><span data-stu-id="cac3e-145">Let's name this column as AdfSliceIdentifier for this example.</span></span>


    <span data-ttu-id="cac3e-146">Kaynak tablosu:</span><span class="sxs-lookup"><span data-stu-id="cac3e-146">Source table:</span></span>

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL
    )
    ```

    <span data-ttu-id="cac3e-147">Hedef Tablo:</span><span class="sxs-lookup"><span data-stu-id="cac3e-147">Destination table:</span></span> 

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL,
       [AdfSliceIdentifier] [binary](32) NULL
    )
    ```

2. <span data-ttu-id="cac3e-148">Kopyalama etkinliği şu şekilde kullanın:</span><span class="sxs-lookup"><span data-stu-id="cac3e-148">Use it in the copy activity as follows:</span></span>
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "AdfSliceIdentifier"
    }
    ```

<span data-ttu-id="cac3e-149">Azure Data Factory bu sütun kaynak ve hedef eşitlenmesine emin olmak için gerek göredir doldurur.</span><span class="sxs-lookup"><span data-stu-id="cac3e-149">Azure Data Factory populates this column as per its need to ensure the source and destination stay synchronized.</span></span> <span data-ttu-id="cac3e-150">Bu sütundaki değerleri bu bağlamı dışında kullanılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="cac3e-150">The values of this column should not be used outside of this context.</span></span> 

<span data-ttu-id="cac3e-151">Benzer şekilde mekanizması 1, kopyalama etkinliği otomatik olarak verilen dilim hedef SQL tablosu için verileri temizler.</span><span class="sxs-lookup"><span data-stu-id="cac3e-151">Similar to mechanism 1, Copy Activity automatically cleans up the data for the given slice from the destination SQL Table.</span></span> <span data-ttu-id="cac3e-152">Ardından veri kaynağından hedef tabloya ekler.</span><span class="sxs-lookup"><span data-stu-id="cac3e-152">It then inserts data from source in to the destination table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="cac3e-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cac3e-153">Next steps</span></span>
<span data-ttu-id="cac3e-154">Tam JSON örnekler için makaleler aşağıdaki Bağlayıcısı'nı gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="cac3e-154">Review the following connector articles that for complete JSON examples:</span></span> 

- [<span data-ttu-id="cac3e-155">Azure SQL Veritabanı</span><span class="sxs-lookup"><span data-stu-id="cac3e-155">Azure SQL Database</span></span>](data-factory-azure-sql-connector.md)
- [<span data-ttu-id="cac3e-156">Azure SQL Veri Ambarı</span><span class="sxs-lookup"><span data-stu-id="cac3e-156">Azure SQL Data Warehouse</span></span>](data-factory-azure-sql-data-warehouse-connector.md)
- [<span data-ttu-id="cac3e-157">SQL Server</span><span class="sxs-lookup"><span data-stu-id="cac3e-157">SQL Server</span></span>](data-factory-sqlserver-connector.md)