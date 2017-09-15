## <span data-ttu-id="24f46-101"><a name="create-client"></a>İstemci bağlantısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="24f46-101"><a name="create-client"></a>Create a client connection</span></span>
<span data-ttu-id="24f46-102">Bir `WindowsAzure.MobileServiceClient` nesnesi oluşturarak istemci bağlantısı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="24f46-102">Create a client connection by creating a `WindowsAzure.MobileServiceClient` object.</span></span>  <span data-ttu-id="24f46-103">`appUrl` ifadesini Mobile Uygulamanızın URL’si ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="24f46-103">Replace `appUrl` with the URL to your Mobile App.</span></span>

```
var client = WindowsAzure.MobileServiceClient(appUrl);
```

## <span data-ttu-id="24f46-104"><a name="table-reference"></a>Tablolarla çalışma</span><span class="sxs-lookup"><span data-stu-id="24f46-104"><a name="table-reference"></a>Work with tables</span></span>
<span data-ttu-id="24f46-105">Verilere erişmek veya verileri güncelleştirmek için arka uç tablosuna başvuru oluşturun.</span><span class="sxs-lookup"><span data-stu-id="24f46-105">To access or update data, create a reference to the backend table.</span></span> <span data-ttu-id="24f46-106">`tableName` ifadesini tablonuzun adıyla değiştirin</span><span class="sxs-lookup"><span data-stu-id="24f46-106">Replace `tableName` with the name of your table</span></span>

```
var table = client.getTable(tableName);
```

<span data-ttu-id="24f46-107">Bir tablo başvurusu oluşturduktan sonra tablonuzla başka işlemler yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="24f46-107">Once you have a table reference, you can work further with your table:</span></span>

* [<span data-ttu-id="24f46-108">Tablo sorgulama</span><span class="sxs-lookup"><span data-stu-id="24f46-108">Query a Table</span></span>](#querying)
  * [<span data-ttu-id="24f46-109">Verileri filtreleme</span><span class="sxs-lookup"><span data-stu-id="24f46-109">Filtering Data</span></span>](#table-filter)
  * [<span data-ttu-id="24f46-110">Verileri sayfalama</span><span class="sxs-lookup"><span data-stu-id="24f46-110">Paging through Data</span></span>](#table-paging)
  * [<span data-ttu-id="24f46-111">Verileri sıralama</span><span class="sxs-lookup"><span data-stu-id="24f46-111">Sorting Data</span></span>](#sorting-data)
* [<span data-ttu-id="24f46-112">Veri ekleme</span><span class="sxs-lookup"><span data-stu-id="24f46-112">Inserting Data</span></span>](#inserting)
* [<span data-ttu-id="24f46-113">Verileri değiştirme</span><span class="sxs-lookup"><span data-stu-id="24f46-113">Modifying Data</span></span>](#modifying)
* [<span data-ttu-id="24f46-114">Veri silme</span><span class="sxs-lookup"><span data-stu-id="24f46-114">Deleting Data</span></span>](#deleting)

### <span data-ttu-id="24f46-115"><a name="querying"></a>Nasıl yapılır: Tablo başvurusu sorgulama</span><span class="sxs-lookup"><span data-stu-id="24f46-115"><a name="querying"></a>How to: Query a table reference</span></span>
<span data-ttu-id="24f46-116">Bir tablo başvurusu oluşturduktan sonra sunucudaki verileri sorgulamak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24f46-116">Once you have a table reference, you can use it to query for data on the server.</span></span>  <span data-ttu-id="24f46-117">Sorgular "LINQ benzeri" bir dilde yapılır.</span><span class="sxs-lookup"><span data-stu-id="24f46-117">Queries are made in a "LINQ-like" language.</span></span>
<span data-ttu-id="24f46-118">Tablodan tüm verileri döndürmek için aşağıdaki kodu kullanın:</span><span class="sxs-lookup"><span data-stu-id="24f46-118">To return all data from the table, use the following code:</span></span>

```
/**
 * Process the results that are received by a call to table.read()
 *
 * @param {Object} results the results as a pseudo-array
 * @param {int} results.length the length of the results array
 * @param {Object} results[] the individual results
 */
function success(results) {
   var numItemsRead = results.length;

   for (var i = 0 ; i < results.length ; i++) {
       var row = results[i];
       // Each row is an object - the properties are the columns
   }
}

function failure(error) {
    throw new Error('Error loading data: ', error);
}

table
    .read()
    .then(success, failure);
```

<span data-ttu-id="24f46-119">Sonuçlarla birlikte başarı işlevi çağrılır.</span><span class="sxs-lookup"><span data-stu-id="24f46-119">The success function is called with the results.</span></span>  <span data-ttu-id="24f46-120">Başarı işlevinde `for (var i in results)` öğesini kullanmayın, aksi takdirde diğer sorgu işlevleri (`.includeTotalCount()` gibi) kullanıldığında sonuçlara eklenen bilgilerin üzerine yinelenir.</span><span class="sxs-lookup"><span data-stu-id="24f46-120">Do not use `for (var i in results)` in the success function as that will iterate over information that is included in the results when other query functions (such as `.includeTotalCount()`) are used.</span></span>

<span data-ttu-id="24f46-121">Sorgu söz dizimi hakkında daha fazla bilgi için [Query nesnesi belgelerine] bakın.</span><span class="sxs-lookup"><span data-stu-id="24f46-121">For more information on the Query syntax, see the [Query object documentation].</span></span>

#### <span data-ttu-id="24f46-122"><a name="table-filter"></a>Sunucu üzerindeki verileri filtreleme</span><span class="sxs-lookup"><span data-stu-id="24f46-122"><a name="table-filter"></a>Filtering data on the server</span></span>
<span data-ttu-id="24f46-123">Tablo başvurusunda bir `where` yan tümcesi kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="24f46-123">You can use a `where` clause on the table reference:</span></span>

```
table
    .where({ userId: user.userId, complete: false })
    .read()
    .then(success, failure);
```

<span data-ttu-id="24f46-124">Ayrıca, nesneyi filtreleyen bir işlev de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24f46-124">You can also use a function that filters the object.</span></span>  <span data-ttu-id="24f46-125">Bu durumda, `this` değişkeni filtre uygulanan geçerli nesneye atanır.</span><span class="sxs-lookup"><span data-stu-id="24f46-125">In this case, the `this` variable is assigned to the current object being filtered.</span></span>  <span data-ttu-id="24f46-126">Aşağıdaki kod önceki örnek ile işlevsel olarak eşdeğerdir:</span><span class="sxs-lookup"><span data-stu-id="24f46-126">The following code is functionally equivalent to the prior example:</span></span>

```
function filterByUserId(currentUserId) {
    return this.userId === currentUserId && this.complete === false;
}

table
    .where(filterByUserId, user.userId)
    .read()
    .then(success, failure);
```

#### <span data-ttu-id="24f46-127"><a name="table-paging"></a>Verileri sayfalama</span><span class="sxs-lookup"><span data-stu-id="24f46-127"><a name="table-paging"></a>Paging through data</span></span>
<span data-ttu-id="24f46-128">`take()` ve `skip()` yöntemlerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="24f46-128">Utilize the `take()` and `skip()` methods.</span></span>  <span data-ttu-id="24f46-129">Örneğin, tabloyu 100 satırlı kayıtlara bölmek istiyorsanız:</span><span class="sxs-lookup"><span data-stu-id="24f46-129">For example, if you wish to split the table into 100-row records:</span></span>

```
var totalCount = 0, pages = 0;

// Step 1 - get the total number of records
table.includeTotalCount().take(0).read(function (results) {
    totalCount = results.totalCount;
    pages = Math.floor(totalCount/100) + 1;
    loadPage(0);
}, failure);

function loadPage(pageNum) {
    let skip = pageNum * 100;
    table.skip(skip).take(100).read(function (results) {
        for (var i = 0 ; i < results.length ; i++) {
            var row = results[i];
            // Process each row
        }
    }
}
```

<span data-ttu-id="24f46-130">Sonuç nesnesine bir totalCount alanı eklemek için `.includeTotalCount()` yöntemi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="24f46-130">The `.includeTotalCount()` method is used to add a totalCount field to the results object.</span></span>  <span data-ttu-id="24f46-131">Sayfalama kullanılmazsa döndürülecek toplam kayıt sayısı TotalCount alanına doldurulur.</span><span class="sxs-lookup"><span data-stu-id="24f46-131">The totalCount field is filled with the total number of records that would be returned if no paging is used.</span></span>

<span data-ttu-id="24f46-132">Bir sayfa listesi sağlamak için pages değişkenini ve bazı kullanıcı arabirimi düğmelerini kullanabilirsiniz; her sayfanın yeni kayıtlarını yüklemek için `loadPage()` seçeneğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="24f46-132">You can then use the pages variable and some UI buttons to provide a page list; use `loadPage()` to load the new records for each page.</span></span>  <span data-ttu-id="24f46-133">Daha önce yüklenmiş kayıtlara hızlı erişim için önbelleğe almayı uygulayın.</span><span class="sxs-lookup"><span data-stu-id="24f46-133">Implement caching to speed access to records that have already been loaded.</span></span>

#### <span data-ttu-id="24f46-134"><a name="sorting-data"></a>Nasıl yapılır: Sıralanmış veriler döndürme</span><span class="sxs-lookup"><span data-stu-id="24f46-134"><a name="sorting-data"></a>How to: Return sorted data</span></span>
<span data-ttu-id="24f46-135">`.orderBy()` veya `.orderByDescending()` sorgu yöntemlerini kullanın:</span><span class="sxs-lookup"><span data-stu-id="24f46-135">Use the `.orderBy()` or `.orderByDescending()` query methods:</span></span>

```
table
    .orderBy('name')
    .read()
    .then(success, failure);
```

<span data-ttu-id="24f46-136">Query nesnesi hakkında daha fazla bilgi için [Query nesnesi belgelerine] bakın.</span><span class="sxs-lookup"><span data-stu-id="24f46-136">For more information on the Query object, see the [Query object documentation].</span></span>

### <span data-ttu-id="24f46-137"><a name="inserting"></a>Nasıl yapılır: Veri ekleme</span><span class="sxs-lookup"><span data-stu-id="24f46-137"><a name="inserting"></a>How to: Insert data</span></span>
<span data-ttu-id="24f46-138">Uygun tarihle bir JavaScript nesnesi oluşturun ve `table.insert()` öğesini zaman uyumsuz olarak çağırın:</span><span class="sxs-lookup"><span data-stu-id="24f46-138">Create a JavaScript object with the appropriate date and call `table.insert()` asynchronously:</span></span>

```javascript
var newItem = {
    name: 'My Name',
    signupDate: new Date()
};

table
    .insert(newItem)
    .done(function (insertedItem) {
        var id = insertedItem.id;
    }, failure);
```

<span data-ttu-id="24f46-139">Ekleme başarılı olduğunda, eklenen öğe eşitleme işlemleri için gereken diğer alanlarla birlikte döndürülür.</span><span class="sxs-lookup"><span data-stu-id="24f46-139">On successful insertion, the inserted item is returned with the additional fields that are required for sync operations.</span></span>  <span data-ttu-id="24f46-140">Sonraki güncelleştirmeler için önbelleğinizi bu bilgilerle güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="24f46-140">Update your own cache with this information for later updates.</span></span>

<span data-ttu-id="24f46-141">Azure Mobile Apps Node.js Sunucu SDK’sı, geliştirme için dinamik şemayı destekler.</span><span class="sxs-lookup"><span data-stu-id="24f46-141">The Azure Mobile Apps Node.js Server SDK supports dynamic schema for development purposes.</span></span>  <span data-ttu-id="24f46-142">Dinamik Şema, bir insert veya update işleminde sütun belirterek tabloya sütun eklemenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="24f46-142">Dynamic Schema allows you to add columns to the table by specifying them in an insert or update operation.</span></span>  <span data-ttu-id="24f46-143">Uygulamanızı üretime taşımadan önce dinamik şemanın kapatılması önerilir.</span><span class="sxs-lookup"><span data-stu-id="24f46-143">We recommend that you turn off dynamic schema before moving your application to production.</span></span>

### <span data-ttu-id="24f46-144"><a name="modifying"></a>Nasıl yapılır: Verileri değiştirme</span><span class="sxs-lookup"><span data-stu-id="24f46-144"><a name="modifying"></a>How to: Modify data</span></span>
<span data-ttu-id="24f46-145">`.insert()` yöntemine benzer şekilde, bir Update nesnesi oluşturup `.update()` öğesini çağırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="24f46-145">Similar to the `.insert()` method, you should create an Update object and then call `.update()`.</span></span>  <span data-ttu-id="24f46-146">Update nesnesi, güncelleştirilecek kaydın kimliğini içermelidir; bu kimlik, kayıt okunurken veya `.insert()` çağrılırken elde edilir.</span><span class="sxs-lookup"><span data-stu-id="24f46-146">The update object must contain the ID of the record to be updated - the ID is obtained when reading the record or when calling `.insert()`.</span></span>

```javascript
var updateItem = {
    id: '7163bc7a-70b2-4dde-98e9-8818969611bd',
    name: 'My New Name'
};

table
    .update(updateItem)
    .done(function (updatedItem) {
        // You can now update your cached copy
    }, failure);
```

### <span data-ttu-id="24f46-147"><a name="deleting"></a>Nasıl yapılır: Veri silme</span><span class="sxs-lookup"><span data-stu-id="24f46-147"><a name="deleting"></a>How to: Delete data</span></span>
<span data-ttu-id="24f46-148">Bir kaydı silmek için `.del()` yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="24f46-148">To delete a record, call the `.del()` method.</span></span>  <span data-ttu-id="24f46-149">Kimliği bir nesne başvurusuna geçirin:</span><span class="sxs-lookup"><span data-stu-id="24f46-149">Pass the ID in an object reference:</span></span>

```
table
    .del({ id: '7163bc7a-70b2-4dde-98e9-8818969611bd' })
    .done(function () {
        // Record is now deleted - update your cache
    }, failure);
```
