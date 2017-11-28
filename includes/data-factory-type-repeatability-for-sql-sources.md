## <a name="repeatability-during-copy"></a><span data-ttu-id="7fe69-101">Kopyalama sırasında Yinelenebilirlik</span><span class="sxs-lookup"><span data-stu-id="7fe69-101">Repeatability during Copy</span></span>
<span data-ttu-id="7fe69-102">Azure SQL/SQL Server veri kopyalamayı diğer verilerden depoladığında bir Yinelenebilirlik istenmeyen sonuçları önlemek için göz önünde bulundurmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7fe69-102">When copying data to Azure SQL/SQL Server from other data stores one needs to keep repeatability in mind to avoid unintended outcomes.</span></span> 

<span data-ttu-id="7fe69-103">Azure SQL/SQL Server veritabanına veri kopyalama, kopyalama etkinliği varsayılan APPEND havuz tablosu veri kümesi varsayılan olarak kullanacak.</span><span class="sxs-lookup"><span data-stu-id="7fe69-103">When copying data to Azure SQL/SQL Server Database, copy activity will by default APPEND the data set to the sink table by default.</span></span> <span data-ttu-id="7fe69-104">Örneğin, verileri Azure SQL/SQL Server veritabanına iki kayıtlarını içeren bir CSV (virgülle ayrılmış değerler veri kaynağından) dosya kopyalarken, bu tablonun benzer.</span><span class="sxs-lookup"><span data-stu-id="7fe69-104">For example, when copying data from a CSV (comma separated values data) file source containing two records to Azure SQL/SQL Server Database, this is what the table looks like:</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

<span data-ttu-id="7fe69-105">Kaynak dosyasında hata buldu ve miktarını aşağı boru 2-4 kaynak dosyasında güncelleştirilmiş varsayalım.</span><span class="sxs-lookup"><span data-stu-id="7fe69-105">Suppose you found errors in source file and updated the quantity of Down Tube from 2 to 4 in the source file.</span></span> <span data-ttu-id="7fe69-106">Veri dilimi belirli bir döneme ait yeniden çalıştırırsanız, Azure SQL/SQL Server veritabanına eklenen iki yeni kayıtlar bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7fe69-106">If you re-run the data slice for that period, you’ll find two new records appended to Azure SQL/SQL Server Database.</span></span> <span data-ttu-id="7fe69-107">Aşağıdaki tablodaki sütunların hiçbiri birincil anahtar kısıtlaması varsayar.</span><span class="sxs-lookup"><span data-stu-id="7fe69-107">The below assumes none of the columns in the table have the primary key constraint.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="7fe69-108">Bunu önlemek için aşağıdakilerden birini yararlanarak UPSERT semantiği belirtin gerekecektir aşağıda belirtildiği 2 mekanizmaları aşağıda.</span><span class="sxs-lookup"><span data-stu-id="7fe69-108">To avoid this, you will need to specify UPSERT semantics by leveraging one of the below 2 mechanisms stated below.</span></span>

> [!NOTE]
> <span data-ttu-id="7fe69-109">Bir dilim otomatik olarak Azure Data Factory içinde belirtilen yeniden deneme ilkesi uyarınca yeniden çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="7fe69-109">A slice can be re-run automatically in Azure Data Factory as per the retry policy specified.</span></span>
> 
> 

### <a name="mechanism-1"></a><span data-ttu-id="7fe69-110">Mekanizması 1</span><span class="sxs-lookup"><span data-stu-id="7fe69-110">Mechanism 1</span></span>
<span data-ttu-id="7fe69-111">Yararlanabileceğiniz **sqlWriterCleanupScript** bir dilim çalıştırıldığında ilk temizleme eylemi gerçekleştirmek için özellik.</span><span class="sxs-lookup"><span data-stu-id="7fe69-111">You can leverage **sqlWriterCleanupScript** property to first perform cleanup action when a slice is run.</span></span> 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

<span data-ttu-id="7fe69-112">Temizleme betiğini yürütülen hangi verileri bu dilim karşılık gelen SQL tablosundan siler belirli bir dilim için kopyalama sırasında ilk.</span><span class="sxs-lookup"><span data-stu-id="7fe69-112">The cleanup script would be executed first during copy for a given slice which would delete the data from the SQL Table corresponding to that slice.</span></span> <span data-ttu-id="7fe69-113">Etkinlik sonradan verileri SQL tablosuna ekler.</span><span class="sxs-lookup"><span data-stu-id="7fe69-113">The activity will subsequently insert the data into the SQL Table.</span></span> 

<span data-ttu-id="7fe69-114">Dilimi yeniden çalıştırın. ardından, miktarı olarak güncelleştirilir bulacaksınız şimdi ise, istenen.</span><span class="sxs-lookup"><span data-stu-id="7fe69-114">If the slice is now re-run, then you will find the quantity is updated as desired.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="7fe69-115">Düz rondela kaydı özgün csv kaldırılana varsayalım.</span><span class="sxs-lookup"><span data-stu-id="7fe69-115">Suppose the Flat Washer record is removed from the original csv.</span></span> <span data-ttu-id="7fe69-116">Dilimi yeniden çalıştırmak aşağıdaki sonucu oluşturur:</span><span class="sxs-lookup"><span data-stu-id="7fe69-116">Then re-running the slice would produce the following result:</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```
<span data-ttu-id="7fe69-117">Yeni bir şey yapılması gerekiyordu.</span><span class="sxs-lookup"><span data-stu-id="7fe69-117">Nothing new had to be done.</span></span> <span data-ttu-id="7fe69-118">Kopyalama etkinliği, dilim karşılık gelen verileri silmek için temizleme betiğini verdi.</span><span class="sxs-lookup"><span data-stu-id="7fe69-118">The copy activity ran the cleanup script to delete the corresponding data for that slice.</span></span> <span data-ttu-id="7fe69-119">Giriş (hangi sonra yalnızca 1 kaydı bulunan) csv okuma sonra ve tabloya eklenen.</span><span class="sxs-lookup"><span data-stu-id="7fe69-119">Then it read the input from the csv (which then contained only 1 record) and inserted it into the Table.</span></span> 

### <a name="mechanism-2"></a><span data-ttu-id="7fe69-120">Mekanizması 2</span><span class="sxs-lookup"><span data-stu-id="7fe69-120">Mechanism 2</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7fe69-121">Sliceıdentifiercolumnname Azure SQL Data Warehouse için şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="7fe69-121">sliceIdentifierColumnName is not supported for Azure SQL Data Warehouse at this time.</span></span> 

<span data-ttu-id="7fe69-122">Ayrılmış bir sütun sağlayarak Yinelenebilirlik elde etmek için başka bir mekanizma olan (**Sliceıdentifiercolumnname**) hedef tablo.</span><span class="sxs-lookup"><span data-stu-id="7fe69-122">Another mechanism to achieve repeatability is by having a dedicated column (**sliceIdentifierColumnName**) in the target Table.</span></span> <span data-ttu-id="7fe69-123">Azure Data Factory tarafından bu sütun kaynak ve hedef eşitlenmesine emin olmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7fe69-123">This column would be used by Azure Data Factory to ensure the source and destination stay synchronized.</span></span> <span data-ttu-id="7fe69-124">Bu yaklaşım, değiştirme veya hedef SQL tablo şemasını tanımlama esneklik olduğunda çalışır.</span><span class="sxs-lookup"><span data-stu-id="7fe69-124">This approach works when there is flexibility in changing or defining the destination SQL Table schema.</span></span> 

<span data-ttu-id="7fe69-125">Bu sütun Azure Data Factory'nin Yinelenebilirlik amaçlar için kullanılır ve işlem sırasında tablonun herhangi bir şema değişikliği Azure Data Factory yapmaz.</span><span class="sxs-lookup"><span data-stu-id="7fe69-125">This column would be used by Azure Data Factory for repeatability purposes and in the process Azure Data Factory will not make any schema changes to the Table.</span></span> <span data-ttu-id="7fe69-126">Bu yaklaşımı kullanmak için yol:</span><span class="sxs-lookup"><span data-stu-id="7fe69-126">Way to use this approach:</span></span>

1. <span data-ttu-id="7fe69-127">Türünde bir sütun ikili (32) hedef SQL tablosu tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="7fe69-127">Define a column of type binary (32) in the destination SQL Table.</span></span> <span data-ttu-id="7fe69-128">Bu sütunda hiç bir kısıtlama olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7fe69-128">There should be no constraints on this column.</span></span> <span data-ttu-id="7fe69-129">Şimdi bu sütun bu örnekte 'ColumnForADFuseOnly' adlandırın.</span><span class="sxs-lookup"><span data-stu-id="7fe69-129">Let's name this column as ‘ColumnForADFuseOnly’ for this example.</span></span>
2. <span data-ttu-id="7fe69-130">Kopyalama etkinliği şu şekilde kullanın:</span><span class="sxs-lookup"><span data-stu-id="7fe69-130">Use it in the copy activity as follows:</span></span>
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "ColumnForADFuseOnly"
    }
    ```

<span data-ttu-id="7fe69-131">Azure Data Factory bu sütun kaynak ve hedef eşitlenmesine emin olmak için gerek göredir doldurur.</span><span class="sxs-lookup"><span data-stu-id="7fe69-131">Azure Data Factory will populate this column as per its need to ensure the source and destination stay synchronized.</span></span> <span data-ttu-id="7fe69-132">Bu sütundaki değerleri dışında bu bağlamda kullanıcı tarafından kullanılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="7fe69-132">The values of this column should not be used outside of this context by the user.</span></span> 

<span data-ttu-id="7fe69-133">Benzer şekilde mekanizması 1, kopyalama etkinliği otomatik olarak ayarlanır hedef SQL tablosu verilen dilim için verileri ilk Temizle ve normal veri kaynağından bu dilim için hedef eklemek için kopyalama etkinliği çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7fe69-133">Similar to mechanism 1, Copy Activity will automatically first clean up the data for the given slice from the destination SQL Table and then run the copy activity normally to insert the data from source to destination for that slice.</span></span> 

