---
title: "Azure Data Factory aaaRepeatable kopyasında | Microsoft Docs"
description: "Verileri kopyalayan bir dilim birden çok kez çalıştırma olsa bile nasıl tooavoid yineleyen öğrenin."
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
ms.openlocfilehash: 79a3fde2b700bf0a0e167479d6a86c5bee1bf7ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="repeatable-copy-in-azure-data-factory"></a><span data-ttu-id="12b6a-103">Azure Data Factory yinelenebilir kopyalama</span><span class="sxs-lookup"><span data-stu-id="12b6a-103">Repeatable copy in Azure Data Factory</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="12b6a-104">İlişkisel kaynaklardan yinelenebilir okuma</span><span class="sxs-lookup"><span data-stu-id="12b6a-104">Repeatable read from relational sources</span></span>
<span data-ttu-id="12b6a-105">İlişkisel veri depoları veri kopyalama işlemi sırasında Yinelenebilirlik göz tooavoid tutmak istenmeyen sonuçları.</span><span class="sxs-lookup"><span data-stu-id="12b6a-105">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="12b6a-106">Azure Data Factory'de bir dilim el ile çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="12b6a-106">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="12b6a-107">Bir hata oluştuğunda bir dilimi yeniden çalıştırmak için bir veri kümesi için yeniden deneme ilkesi de yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="12b6a-107">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="12b6a-108">Bir dilim iki yolla yeniden zaman, aynı veri hello emin toomake nasıl geçtiğinden bağımsız okuma gerekir dilim birçok kez çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="12b6a-108">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span>  
 
> [!NOTE]
> <span data-ttu-id="12b6a-109">Merhaba aşağıdaki örnekleri için Azure SQL ancak dikdörtgen veri kümeleri destekleyen geçerli tooany veri deposu.</span><span class="sxs-lookup"><span data-stu-id="12b6a-109">hello following samples are for Azure SQL but are applicable tooany data store that supports rectangular datasets.</span></span> <span data-ttu-id="12b6a-110">Tooadjust hello olabilir **türü** kaynak ve hello **sorgu** özelliği (örneğin: Sorgu sqlReaderQuery yerine) hello verilerini depolamak.</span><span class="sxs-lookup"><span data-stu-id="12b6a-110">You may have tooadjust hello **type** of source and hello **query** property (for example: query instead of sqlReaderQuery) for hello data store.</span></span>   

<span data-ttu-id="12b6a-111">Genellikle, ilişkisel depoları okunurken toothat dilim karşılık gelen tooread hello veriler yalnızca istiyor.</span><span class="sxs-lookup"><span data-stu-id="12b6a-111">Usually, when reading from relational stores, you want tooread only hello data corresponding toothat slice.</span></span> <span data-ttu-id="12b6a-112">Bir şekilde toodo şekilde Azure Data Factory'de hello WindowStart ve WindowEnd sistem değişkenleri kullanılabilir kullanarak olacaktır.</span><span class="sxs-lookup"><span data-stu-id="12b6a-112">A way toodo so would be by using hello WindowStart and WindowEnd system variables available in Azure Data Factory.</span></span> <span data-ttu-id="12b6a-113">Merhaba değişkenleri ve hello burada Azure Data factory'de işlevleri hakkında bilgi [Azure Data Factory - işlevler ve sistem değişkenleri](data-factory-functions-variables.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="12b6a-113">Read about hello variables and functions in Azure Data Factory here in hello [Azure Data Factory - Functions and System Variables](data-factory-functions-variables.md) article.</span></span> <span data-ttu-id="12b6a-114">Örnek:</span><span class="sxs-lookup"><span data-stu-id="12b6a-114">Example:</span></span> 

```json
"source": {
    "type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm\\'', WindowStart, WindowEnd)"
},
```
<span data-ttu-id="12b6a-115">Bu sorgu MyTable hello tablosundan hello dilim süresi aralığını (WindowStart -> WindowEnd) içinde kalan verileri okur.</span><span class="sxs-lookup"><span data-stu-id="12b6a-115">This query reads data that falls in hello slice duration range (WindowStart -> WindowEnd) from hello table MyTable.</span></span> <span data-ttu-id="12b6a-116">Bu dilimin yeniden çalıştırın ayrıca her zaman aynı veri okuma, hello emin.</span><span class="sxs-lookup"><span data-stu-id="12b6a-116">Rerun of this slice would also always ensure that hello same data is read.</span></span> 

<span data-ttu-id="12b6a-117">Diğer durumlarda, tooread hello tüm tablo isteyebilir ve hello sqlReaderQuery gibi tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="12b6a-117">In other cases, you may wish tooread hello entire table and may define hello sqlReaderQuery as follows:</span></span>

```json
"source": 
{            
    "type": "SqlSource",
    "sqlReaderQuery": "select * from MyTable"
},
```

## <a name="repeatable-write-toosqlsink"></a><span data-ttu-id="12b6a-118">Yinelenebilir yazma tooSqlSink</span><span class="sxs-lookup"><span data-stu-id="12b6a-118">Repeatable write tooSqlSink</span></span>
<span data-ttu-id="12b6a-119">Veriler çok kopyalarken**Azure SQL/SQL Server** tookeep Yinelenebilirlik göz tooavoid içinde gereken diğer veri depolarına, istenmeyen sonuçları.</span><span class="sxs-lookup"><span data-stu-id="12b6a-119">When copying data too**Azure SQL/SQL Server** from other data stores, you need tookeep repeatability in mind tooavoid unintended outcomes.</span></span> 

<span data-ttu-id="12b6a-120">Veri tooAzure SQL/SQL Server veritabanı kopyalama işlemi sırasında hello kopyalama etkinliği varsayılan olarak veri toohello havuz tablosuna ekler.</span><span class="sxs-lookup"><span data-stu-id="12b6a-120">When copying data tooAzure SQL/SQL Server Database, hello copy activity appends data toohello sink table by default.</span></span> <span data-ttu-id="12b6a-121">Deyin, aşağıdaki tablonun bir Azure SQL/SQL Server veritabanında bir CSV (virgülle ayrılmış değerler) dosyasını içeren iki kayıt toohello gelen veri kopyalarsınız.</span><span class="sxs-lookup"><span data-stu-id="12b6a-121">Say, you are copying data from a CSV (comma-separated values) file containing two records toohello following table in an Azure SQL/SQL Server Database.</span></span> <span data-ttu-id="12b6a-122">Bir dilim çalıştığında hello iki kopyalanan toohello SQL tablosu kayıtlarıdır.</span><span class="sxs-lookup"><span data-stu-id="12b6a-122">When a slice runs, hello two records are copied toohello SQL table.</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

<span data-ttu-id="12b6a-123">Kaynak dosyasında hata buldu ve aşağı boru hello miktarından 2 too4 itibaren güncelleştirilmiş varsayalım.</span><span class="sxs-lookup"><span data-stu-id="12b6a-123">Suppose you found errors in source file and updated hello quantity of Down Tube from 2 too4.</span></span> <span data-ttu-id="12b6a-124">Merhaba veri dilimi belirli bir döneme ait el ile yeniden, iki yeni kayıt tooAzure SQL/SQL Server veritabanına eklenen bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="12b6a-124">If you rerun hello data slice for that period manually, you’ll find two new records appended tooAzure SQL/SQL Server Database.</span></span> <span data-ttu-id="12b6a-125">Bu örnek hello tablodaki hello sütun hiçbiri hello birincil anahtar kısıtlaması olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="12b6a-125">This example assumes that none of hello columns in hello table has hello primary key constraint.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="12b6a-126">tooavoid Bu davranış, toospecify UPSERT semantiği iki mekanizma aşağıdaki hello birini kullanarak gerekir:</span><span class="sxs-lookup"><span data-stu-id="12b6a-126">tooavoid this behavior, you need toospecify UPSERT semantics by using one of hello following two mechanisms:</span></span>

### <a name="mechanism-1-using-sqlwritercleanupscript"></a><span data-ttu-id="12b6a-127">Mekanizması 1: sqlWriterCleanupScript kullanma</span><span class="sxs-lookup"><span data-stu-id="12b6a-127">Mechanism 1: using sqlWriterCleanupScript</span></span>
<span data-ttu-id="12b6a-128">Merhaba kullanabilirsiniz **sqlWriterCleanupScript** özelliği tooclean bir dilim çalıştırdığınızda hello veri eklemeden önce hello havuz tablodan veri ayarlama.</span><span class="sxs-lookup"><span data-stu-id="12b6a-128">You can use hello **sqlWriterCleanupScript** property tooclean up data from hello sink table before inserting hello data when a slice is run.</span></span> 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

<span data-ttu-id="12b6a-129">Bir dilim çalıştığında hello temizleme betiğini toohello dilim hello SQL tablosundan karşılık gelen ilk toodelete veri çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="12b6a-129">When a slice runs, hello cleanup script is run first toodelete data that corresponds toohello slice from hello SQL table.</span></span> <span data-ttu-id="12b6a-130">Merhaba kopyalama etkinliği, ardından SQL tablosu hello veri ekler.</span><span class="sxs-lookup"><span data-stu-id="12b6a-130">hello copy activity then inserts data into hello SQL Table.</span></span> <span data-ttu-id="12b6a-131">Merhaba dilimi yeniden çalıştırın, hello miktar güncelleştirilir istenen şekilde.</span><span class="sxs-lookup"><span data-stu-id="12b6a-131">If hello slice is rerun, hello quantity is updated as desired.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="12b6a-132">Merhaba düz rondela kayıt hello özgün csv kaldırılır varsayalım.</span><span class="sxs-lookup"><span data-stu-id="12b6a-132">Suppose hello Flat Washer record is removed from hello original csv.</span></span> <span data-ttu-id="12b6a-133">Yeniden çalıştırma hello dilim sonuç aşağıdaki hello sonra oluşturur:</span><span class="sxs-lookup"><span data-stu-id="12b6a-133">Then rerunning hello slice would produce hello following result:</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="12b6a-134">Merhaba kopyalama etkinliği hello temizleme betik toodelete hello ilgili verilerini bu dilim verdi.</span><span class="sxs-lookup"><span data-stu-id="12b6a-134">hello copy activity ran hello cleanup script toodelete hello corresponding data for that slice.</span></span> <span data-ttu-id="12b6a-135">(Bu, daha sonra yer alan yalnızca bir kayıt) hello csv hello giriş okuyun sonra ve tablo hello eklenir.</span><span class="sxs-lookup"><span data-stu-id="12b6a-135">Then it read hello input from hello csv (which then contained only one record) and inserted it into hello Table.</span></span> 

### <a name="mechanism-2-using-sliceidentifiercolumnname"></a><span data-ttu-id="12b6a-136">Mekanizması 2: Sliceıdentifiercolumnname kullanma</span><span class="sxs-lookup"><span data-stu-id="12b6a-136">Mechanism 2: using sliceIdentifierColumnName</span></span>
> [!IMPORTANT]
> <span data-ttu-id="12b6a-137">Şu anda Sliceıdentifiercolumnname Azure SQL veri ambarı için desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="12b6a-137">Currently, sliceIdentifierColumnName is not supported for Azure SQL Data Warehouse.</span></span> 

<span data-ttu-id="12b6a-138">Merhaba ikinci mekanizması tooachieve Yinelenebilirlik hello hedef tablo ayrılmış sütun (Sliceıdentifiercolumnname) sağlayarak ' dir.</span><span class="sxs-lookup"><span data-stu-id="12b6a-138">hello second mechanism tooachieve repeatability is by having a dedicated column (sliceIdentifierColumnName) in hello target Table.</span></span> <span data-ttu-id="12b6a-139">Bu sütun eşitlenmiş Azure Data Factory tooensure hello kaynak ve hedef Kal tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="12b6a-139">This column would be used by Azure Data Factory tooensure hello source and destination stay synchronized.</span></span> <span data-ttu-id="12b6a-140">Bu yaklaşım, değiştirme veya hello hedef SQL tablo şemasını tanımlama esneklik olduğunda çalışır.</span><span class="sxs-lookup"><span data-stu-id="12b6a-140">This approach works when there is flexibility in changing or defining hello destination SQL Table schema.</span></span> 

<span data-ttu-id="12b6a-141">Bu sütun Yinelenebilirlik amaçlar için Azure Data Factory tarafından kullanılır ve hello işlemde herhangi bir şema Azure Data Factory yapmaz toohello tablo değiştirir.</span><span class="sxs-lookup"><span data-stu-id="12b6a-141">This column is used by Azure Data Factory for repeatability purposes and in hello process Azure Data Factory does not make any schema changes toohello Table.</span></span> <span data-ttu-id="12b6a-142">Yol toouse bu yaklaşım:</span><span class="sxs-lookup"><span data-stu-id="12b6a-142">Way toouse this approach:</span></span>

1. <span data-ttu-id="12b6a-143">Türünde bir sütun tanımlamak **ikili (32)** hello hedef SQL tablosu.</span><span class="sxs-lookup"><span data-stu-id="12b6a-143">Define a column of type **binary (32)** in hello destination SQL Table.</span></span> <span data-ttu-id="12b6a-144">Bu sütunda hiç bir kısıtlama olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="12b6a-144">There should be no constraints on this column.</span></span> <span data-ttu-id="12b6a-145">Şimdi bu sütun, bu örnek için AdfSliceIdentifier adlandırın.</span><span class="sxs-lookup"><span data-stu-id="12b6a-145">Let's name this column as AdfSliceIdentifier for this example.</span></span>


    <span data-ttu-id="12b6a-146">Kaynak tablosu:</span><span class="sxs-lookup"><span data-stu-id="12b6a-146">Source table:</span></span>

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL
    )
    ```

    <span data-ttu-id="12b6a-147">Hedef Tablo:</span><span class="sxs-lookup"><span data-stu-id="12b6a-147">Destination table:</span></span> 

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL,
       [AdfSliceIdentifier] [binary](32) NULL
    )
    ```

2. <span data-ttu-id="12b6a-148">Merhaba kopyalama etkinliği şu şekilde kullanın:</span><span class="sxs-lookup"><span data-stu-id="12b6a-148">Use it in hello copy activity as follows:</span></span>
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "AdfSliceIdentifier"
    }
    ```

<span data-ttu-id="12b6a-149">Azure Data Factory doldurur bu sütun, gerek göredir tooensure hello kaynak ve hedef eşitlenmiş kalır.</span><span class="sxs-lookup"><span data-stu-id="12b6a-149">Azure Data Factory populates this column as per its need tooensure hello source and destination stay synchronized.</span></span> <span data-ttu-id="12b6a-150">Bu sütundaki değerleri Hello dışında bu bağlamda kullanılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="12b6a-150">hello values of this column should not be used outside of this context.</span></span> 

<span data-ttu-id="12b6a-151">Benzer toomechanism 1, kopyalama etkinliği hello veri dilimi hello hedef SQL tablosu verilen hello için otomatik olarak temizler.</span><span class="sxs-lookup"><span data-stu-id="12b6a-151">Similar toomechanism 1, Copy Activity automatically cleans up hello data for hello given slice from hello destination SQL Table.</span></span> <span data-ttu-id="12b6a-152">Ardından toohello hedef tablodaki kaynaktan veri ekler.</span><span class="sxs-lookup"><span data-stu-id="12b6a-152">It then inserts data from source in toohello destination table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="12b6a-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="12b6a-153">Next steps</span></span>
<span data-ttu-id="12b6a-154">Merhaba, JSON örnekleri tamamlamak için bağlayıcı makaleler gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="12b6a-154">Review hello following connector articles that for complete JSON examples:</span></span> 

- [<span data-ttu-id="12b6a-155">Azure SQL Veritabanı</span><span class="sxs-lookup"><span data-stu-id="12b6a-155">Azure SQL Database</span></span>](data-factory-azure-sql-connector.md)
- [<span data-ttu-id="12b6a-156">Azure SQL Veri Ambarı</span><span class="sxs-lookup"><span data-stu-id="12b6a-156">Azure SQL Data Warehouse</span></span>](data-factory-azure-sql-data-warehouse-connector.md)
- [<span data-ttu-id="12b6a-157">SQL Server</span><span class="sxs-lookup"><span data-stu-id="12b6a-157">SQL Server</span></span>](data-factory-sqlserver-connector.md)