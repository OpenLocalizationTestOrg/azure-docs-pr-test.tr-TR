## <a name="repeatability-during-copy"></a><span data-ttu-id="ecf39-101">Kopyalama sırasında Yinelenebilirlik</span><span class="sxs-lookup"><span data-stu-id="ecf39-101">Repeatability during Copy</span></span>
<span data-ttu-id="ecf39-102">Ne zaman veri tooAzure SQL/SQL Server diğer veriler kopyalama depolayan bir gereksinimlerini tookeep Yinelenebilirlik göz tooavoid istenmeyen sonuçları.</span><span class="sxs-lookup"><span data-stu-id="ecf39-102">When copying data tooAzure SQL/SQL Server from other data stores one needs tookeep repeatability in mind tooavoid unintended outcomes.</span></span> 

<span data-ttu-id="ecf39-103">Veri tooAzure SQL/SQL Server veritabanı kopyalama, kopyalama etkinliği varsayılan APPEND hello veri kümesi toohello havuz tablosu tarafından varsayılan olarak kullanacak.</span><span class="sxs-lookup"><span data-stu-id="ecf39-103">When copying data tooAzure SQL/SQL Server Database, copy activity will by default APPEND hello data set toohello sink table by default.</span></span> <span data-ttu-id="ecf39-104">Örneğin, iki içeren CSV (virgülle ayrılmış değerler veri) dosya kaynağından veri kopyalama tooAzure SQL/SQL Server veritabanına kaydeder sonra bu gibi görünüyor hangi hello tablo olur:</span><span class="sxs-lookup"><span data-stu-id="ecf39-104">For example, when copying data from a CSV (comma separated values data) file source containing two records tooAzure SQL/SQL Server Database, this is what hello table looks like:</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

<span data-ttu-id="ecf39-105">Hataları kaynak dosyasını ve aşağı boru güncelleştirilmiş hello miktarından 2 too4 itibaren hello kaynak dosyasında bulunan varsayalım.</span><span class="sxs-lookup"><span data-stu-id="ecf39-105">Suppose you found errors in source file and updated hello quantity of Down Tube from 2 too4 in hello source file.</span></span> <span data-ttu-id="ecf39-106">Belirli bir döneme ait yeniden hello veri dilimi çalıştırırsanız, iki yeni kayıt tooAzure SQL/SQL Server veritabanına eklenen bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ecf39-106">If you re-run hello data slice for that period, you’ll find two new records appended tooAzure SQL/SQL Server Database.</span></span> <span data-ttu-id="ecf39-107">Merhaba aşağıdaki hello tablodaki hello sütun hiçbiri hello birincil anahtar kısıtlaması olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="ecf39-107">hello below assumes none of hello columns in hello table have hello primary key constraint.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="ecf39-108">tooavoid Bu, aşağıda belirtildiği 2 mekanizmaları aşağıda hello yararlanarak toospecify UPSERT semantiği gerekir.</span><span class="sxs-lookup"><span data-stu-id="ecf39-108">tooavoid this, you will need toospecify UPSERT semantics by leveraging one of hello below 2 mechanisms stated below.</span></span>

> [!NOTE]
> <span data-ttu-id="ecf39-109">Bir dilim otomatik olarak Azure Data Factory içinde belirtilen hello yeniden deneme ilkesi uyarınca yeniden çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="ecf39-109">A slice can be re-run automatically in Azure Data Factory as per hello retry policy specified.</span></span>
> 
> 

### <a name="mechanism-1"></a><span data-ttu-id="ecf39-110">Mekanizması 1</span><span class="sxs-lookup"><span data-stu-id="ecf39-110">Mechanism 1</span></span>
<span data-ttu-id="ecf39-111">Yararlanabileceğiniz **sqlWriterCleanupScript** özelliği toofirst bir dilim çalıştırdığınızda temizleme eylemi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="ecf39-111">You can leverage **sqlWriterCleanupScript** property toofirst perform cleanup action when a slice is run.</span></span> 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

<span data-ttu-id="ecf39-112">Merhaba temizleme betiğini yürütülmesi, hello veri hello SQL tablosuna karşılık gelen toothat dilimden silebilirsiniz belirli bir dilim için kopyalama sırasında ilk.</span><span class="sxs-lookup"><span data-stu-id="ecf39-112">hello cleanup script would be executed first during copy for a given slice which would delete hello data from hello SQL Table corresponding toothat slice.</span></span> <span data-ttu-id="ecf39-113">Merhaba etkinlik sonradan hello veri hello SQL tablosuna ekler.</span><span class="sxs-lookup"><span data-stu-id="ecf39-113">hello activity will subsequently insert hello data into hello SQL Table.</span></span> 

<span data-ttu-id="ecf39-114">Merhaba miktar olarak güncelleştirilir yeniden çalıştırın. ardından, bulur artık hello dilim varsa desired.</span><span class="sxs-lookup"><span data-stu-id="ecf39-114">If hello slice is now re-run, then you will find hello quantity is updated as desired.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="ecf39-115">Merhaba düz rondela kayıt hello özgün csv kaldırılır varsayalım.</span><span class="sxs-lookup"><span data-stu-id="ecf39-115">Suppose hello Flat Washer record is removed from hello original csv.</span></span> <span data-ttu-id="ecf39-116">Daha sonra yeniden çalıştırarak hello dilim sonuç aşağıdaki hello oluşturur:</span><span class="sxs-lookup"><span data-stu-id="ecf39-116">Then re-running hello slice would produce hello following result:</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```
<span data-ttu-id="ecf39-117">Yeni bir şey bitti toobe vardı.</span><span class="sxs-lookup"><span data-stu-id="ecf39-117">Nothing new had toobe done.</span></span> <span data-ttu-id="ecf39-118">Merhaba kopyalama etkinliği hello temizleme betik toodelete hello ilgili verilerini bu dilim verdi.</span><span class="sxs-lookup"><span data-stu-id="ecf39-118">hello copy activity ran hello cleanup script toodelete hello corresponding data for that slice.</span></span> <span data-ttu-id="ecf39-119">(Bu, daha sonra yer alan yalnızca 1 kaydı) hello csv hello giriş okuyun sonra ve tablo hello eklenir.</span><span class="sxs-lookup"><span data-stu-id="ecf39-119">Then it read hello input from hello csv (which then contained only 1 record) and inserted it into hello Table.</span></span> 

### <a name="mechanism-2"></a><span data-ttu-id="ecf39-120">Mekanizması 2</span><span class="sxs-lookup"><span data-stu-id="ecf39-120">Mechanism 2</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ecf39-121">Sliceıdentifiercolumnname Azure SQL Data Warehouse için şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="ecf39-121">sliceIdentifierColumnName is not supported for Azure SQL Data Warehouse at this time.</span></span> 

<span data-ttu-id="ecf39-122">Başka bir mekanizma tooachieve Yinelenebilirlik adanmış bir sütun sağlayarak olduğu (**Sliceıdentifiercolumnname**) tablo hello hedefleyin.</span><span class="sxs-lookup"><span data-stu-id="ecf39-122">Another mechanism tooachieve repeatability is by having a dedicated column (**sliceIdentifierColumnName**) in hello target Table.</span></span> <span data-ttu-id="ecf39-123">Bu sütun eşitlenmiş Azure Data Factory tooensure hello kaynak ve hedef Kal tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ecf39-123">This column would be used by Azure Data Factory tooensure hello source and destination stay synchronized.</span></span> <span data-ttu-id="ecf39-124">Bu yaklaşım, değiştirme veya hello hedef SQL tablo şemasını tanımlama esneklik olduğunda çalışır.</span><span class="sxs-lookup"><span data-stu-id="ecf39-124">This approach works when there is flexibility in changing or defining hello destination SQL Table schema.</span></span> 

<span data-ttu-id="ecf39-125">Bu sütun Azure Data Factory'nin Yinelenebilirlik amaçlar için kullanılır ve hello işlemde herhangi bir şema Azure Data Factory yapmaz toohello tablo değiştirir.</span><span class="sxs-lookup"><span data-stu-id="ecf39-125">This column would be used by Azure Data Factory for repeatability purposes and in hello process Azure Data Factory will not make any schema changes toohello Table.</span></span> <span data-ttu-id="ecf39-126">Yol toouse bu yaklaşım:</span><span class="sxs-lookup"><span data-stu-id="ecf39-126">Way toouse this approach:</span></span>

1. <span data-ttu-id="ecf39-127">Türünde bir sütun ikili (32) hello hedef SQL tablosu tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="ecf39-127">Define a column of type binary (32) in hello destination SQL Table.</span></span> <span data-ttu-id="ecf39-128">Bu sütunda hiç bir kısıtlama olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ecf39-128">There should be no constraints on this column.</span></span> <span data-ttu-id="ecf39-129">Şimdi bu sütun bu örnekte 'ColumnForADFuseOnly' adlandırın.</span><span class="sxs-lookup"><span data-stu-id="ecf39-129">Let's name this column as ‘ColumnForADFuseOnly’ for this example.</span></span>
2. <span data-ttu-id="ecf39-130">Merhaba kopyalama etkinliği şu şekilde kullanın:</span><span class="sxs-lookup"><span data-stu-id="ecf39-130">Use it in hello copy activity as follows:</span></span>
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "ColumnForADFuseOnly"
    }
    ```

<span data-ttu-id="ecf39-131">Azure Data Factory bu sütun, gerek göredir doldurmak tooensure hello kaynak ve hedef eşitlenmiş kalır.</span><span class="sxs-lookup"><span data-stu-id="ecf39-131">Azure Data Factory will populate this column as per its need tooensure hello source and destination stay synchronized.</span></span> <span data-ttu-id="ecf39-132">Bu sütundaki değerleri Hello dışında bu bağlamda hello kullanıcı tarafından kullanılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="ecf39-132">hello values of this column should not be used outside of this context by hello user.</span></span> 

<span data-ttu-id="ecf39-133">Benzer toomechanism 1, kopyalama etkinliği otomatik olarak ilk dilim hello hedef SQL tablosu verilen ve hello kopyalama etkinliği normalde çalıştırılan hello hello verilerini temizleme, dilim için kaynak toodestination tooinsert hello verileri.</span><span class="sxs-lookup"><span data-stu-id="ecf39-133">Similar toomechanism 1, Copy Activity will automatically first clean up hello data for hello given slice from hello destination SQL Table and then run hello copy activity normally tooinsert hello data from source toodestination for that slice.</span></span> 

