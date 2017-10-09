## <span data-ttu-id="8d45b-101"><a name="create-client"></a>İstemci bağlantısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8d45b-101"><a name="create-client"></a>Create a client connection</span></span>
<span data-ttu-id="8d45b-102">Bir `WindowsAzure.MobileServiceClient` nesnesi oluşturarak istemci bağlantısı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8d45b-102">Create a client connection by creating a `WindowsAzure.MobileServiceClient` object.</span></span>  <span data-ttu-id="8d45b-103">Değiştir `appUrl` URL tooyour mobil uygulama ile.</span><span class="sxs-lookup"><span data-stu-id="8d45b-103">Replace `appUrl` with the URL tooyour Mobile App.</span></span>

```
var client = WindowsAzure.MobileServiceClient(appUrl);
```

## <span data-ttu-id="8d45b-104"><a name="table-reference"></a>Tablolarla çalışma</span><span class="sxs-lookup"><span data-stu-id="8d45b-104"><a name="table-reference"></a>Work with tables</span></span>
<span data-ttu-id="8d45b-105">tooaccess veya güncelleştirme veriler, bir başvuru toohello arka uç tablosu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8d45b-105">tooaccess or update data, create a reference toohello backend table.</span></span> <span data-ttu-id="8d45b-106">Değiştir `tableName` tablonuz hello adı</span><span class="sxs-lookup"><span data-stu-id="8d45b-106">Replace `tableName` with hello name of your table</span></span>

```
var table = client.getTable(tableName);
```

<span data-ttu-id="8d45b-107">Bir tablo başvurusu oluşturduktan sonra tablonuzla başka işlemler yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8d45b-107">Once you have a table reference, you can work further with your table:</span></span>

* [<span data-ttu-id="8d45b-108">Tablo sorgulama</span><span class="sxs-lookup"><span data-stu-id="8d45b-108">Query a Table</span></span>](#querying)
  * [<span data-ttu-id="8d45b-109">Verileri filtreleme</span><span class="sxs-lookup"><span data-stu-id="8d45b-109">Filtering Data</span></span>](#table-filter)
  * [<span data-ttu-id="8d45b-110">Verileri sayfalama</span><span class="sxs-lookup"><span data-stu-id="8d45b-110">Paging through Data</span></span>](#table-paging)
  * [<span data-ttu-id="8d45b-111">Verileri sıralama</span><span class="sxs-lookup"><span data-stu-id="8d45b-111">Sorting Data</span></span>](#sorting-data)
* [<span data-ttu-id="8d45b-112">Veri ekleme</span><span class="sxs-lookup"><span data-stu-id="8d45b-112">Inserting Data</span></span>](#inserting)
* [<span data-ttu-id="8d45b-113">Verileri değiştirme</span><span class="sxs-lookup"><span data-stu-id="8d45b-113">Modifying Data</span></span>](#modifying)
* [<span data-ttu-id="8d45b-114">Veri silme</span><span class="sxs-lookup"><span data-stu-id="8d45b-114">Deleting Data</span></span>](#deleting)

### <span data-ttu-id="8d45b-115"><a name="querying"></a>Nasıl yapılır: Tablo başvurusu sorgulama</span><span class="sxs-lookup"><span data-stu-id="8d45b-115"><a name="querying"></a>How to: Query a table reference</span></span>
<span data-ttu-id="8d45b-116">Bir tablo başvurusu olduktan sonra onu tooquery hello sunucusundaki veriler için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8d45b-116">Once you have a table reference, you can use it tooquery for data on hello server.</span></span>  <span data-ttu-id="8d45b-117">Sorgular "LINQ benzeri" bir dilde yapılır.</span><span class="sxs-lookup"><span data-stu-id="8d45b-117">Queries are made in a "LINQ-like" language.</span></span>
<span data-ttu-id="8d45b-118">tooreturn hello tablodan aşağıdaki kullanım hello tüm veri kod:</span><span class="sxs-lookup"><span data-stu-id="8d45b-118">tooreturn all data from hello table, use hello following code:</span></span>

```
/**
 * Process hello results that are received by a call tootable.read()
 *
 * @param {Object} results hello results as a pseudo-array
 * @param {int} results.length hello length of hello results array
 * @param {Object} results[] hello individual results
 */
function success(results) {
   var numItemsRead = results.length;

   for (var i = 0 ; i < results.length ; i++) {
       var row = results[i];
       // Each row is an object - hello properties are hello columns
   }
}

function failure(error) {
    throw new Error('Error loading data: ', error);
}

table
    .read()
    .then(success, failure);
```

<span data-ttu-id="8d45b-119">Merhaba başarı işlev hello sonuçlarıyla çağrılır.</span><span class="sxs-lookup"><span data-stu-id="8d45b-119">hello success function is called with hello results.</span></span>  <span data-ttu-id="8d45b-120">Kullanmayın `for (var i in results)` hello başarı içinde işlev hello sonuçlara dahil bilgi üzerinden yineleme şekilde, diğer sorgu işlevleri (gibi `.includeTotalCount()`) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8d45b-120">Do not use `for (var i in results)` in hello success function as that will iterate over information that is included in hello results when other query functions (such as `.includeTotalCount()`) are used.</span></span>

<span data-ttu-id="8d45b-121">Merhaba hello sorgu söz dizimi hakkında daha fazla bilgi için bkz. [sorgu nesne belgelerini].</span><span class="sxs-lookup"><span data-stu-id="8d45b-121">For more information on hello Query syntax, see hello [Query object documentation].</span></span>

#### <span data-ttu-id="8d45b-122"><a name="table-filter"></a>Merhaba sunucusundaki verileri filtreleme</span><span class="sxs-lookup"><span data-stu-id="8d45b-122"><a name="table-filter"></a>Filtering data on hello server</span></span>
<span data-ttu-id="8d45b-123">Kullanabileceğiniz bir `where` hello tablo başvurusu yan tümcesi:</span><span class="sxs-lookup"><span data-stu-id="8d45b-123">You can use a `where` clause on hello table reference:</span></span>

```
table
    .where({ userId: user.userId, complete: false })
    .read()
    .then(success, failure);
```

<span data-ttu-id="8d45b-124">Merhaba nesne filtreler işlevi de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8d45b-124">You can also use a function that filters hello object.</span></span>  <span data-ttu-id="8d45b-125">Bu durumda, hello `this` değişkeni filtre uygulanan toothe geçerli nesneye atanmış.</span><span class="sxs-lookup"><span data-stu-id="8d45b-125">In this case, hello `this` variable is assigned toothe current object being filtered.</span></span>  <span data-ttu-id="8d45b-126">koddan hello işlevsel olarak eşdeğer toohello önceki örnek verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="8d45b-126">hello following code is functionally equivalent toohello prior example:</span></span>

```
function filterByUserId(currentUserId) {
    return this.userId === currentUserId && this.complete === false;
}

table
    .where(filterByUserId, user.userId)
    .read()
    .then(success, failure);
```

#### <span data-ttu-id="8d45b-127"><a name="table-paging"></a>Verileri sayfalama</span><span class="sxs-lookup"><span data-stu-id="8d45b-127"><a name="table-paging"></a>Paging through data</span></span>
<span data-ttu-id="8d45b-128">Merhaba kullanan `take()` ve `skip()` yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="8d45b-128">Utilize hello `take()` and `skip()` methods.</span></span>  <span data-ttu-id="8d45b-129">Örneğin, 100-satırı kayıtlar toosplit hello tablo istiyorsanız:</span><span class="sxs-lookup"><span data-stu-id="8d45b-129">For example, if you wish toosplit hello table into 100-row records:</span></span>

```
var totalCount = 0, pages = 0;

// Step 1 - get hello total number of records
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

<span data-ttu-id="8d45b-130">Merhaba `.includeTotalCount()` kullanılan tooadd totalCount alan toohello sonuçları nesne bir yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="8d45b-130">hello `.includeTotalCount()` method is used tooadd a totalCount field toohello results object.</span></span>  <span data-ttu-id="8d45b-131">TotalCount alanı hello toplam hiçbir disk belleği kullanılırsa döndürülür kayıt sayısı ile doldurulur.</span><span class="sxs-lookup"><span data-stu-id="8d45b-131">The totalCount field is filled with hello total number of records that would be returned if no paging is used.</span></span>

<span data-ttu-id="8d45b-132">Daha sonra hello sayfa değişkeni ve bazı kullanıcı Arabirimi düğmeleri tooprovide sayfa listesi kullanabilirsiniz; kullanmak `loadPage()` hello yeni kayıtlar için her bir sayfa yüklenemiyor.</span><span class="sxs-lookup"><span data-stu-id="8d45b-132">You can then use hello pages variable and some UI buttons tooprovide a page list; use `loadPage()` to load hello new records for each page.</span></span>  <span data-ttu-id="8d45b-133">Daha önce yüklenmiş önbelleğe alma toospeed erişim toorecords uygulayın.</span><span class="sxs-lookup"><span data-stu-id="8d45b-133">Implement caching toospeed access toorecords that have already been loaded.</span></span>

#### <span data-ttu-id="8d45b-134"><a name="sorting-data"></a>Nasıl yapılır: Sıralanmış veriler döndürme</span><span class="sxs-lookup"><span data-stu-id="8d45b-134"><a name="sorting-data"></a>How to: Return sorted data</span></span>
<span data-ttu-id="8d45b-135">Kullanım hello `.orderBy()` veya `.orderByDescending()` sorgu yöntemleri:</span><span class="sxs-lookup"><span data-stu-id="8d45b-135">Use hello `.orderBy()` or `.orderByDescending()` query methods:</span></span>

```
table
    .orderBy('name')
    .read()
    .then(success, failure);
```

<span data-ttu-id="8d45b-136">Merhaba hello sorgu nesnesi hakkında daha fazla bilgi için bkz. [sorgu nesne belgelerini].</span><span class="sxs-lookup"><span data-stu-id="8d45b-136">For more information on hello Query object, see hello [Query object documentation].</span></span>

### <span data-ttu-id="8d45b-137"><a name="inserting"></a>Nasıl yapılır: Veri ekleme</span><span class="sxs-lookup"><span data-stu-id="8d45b-137"><a name="inserting"></a>How to: Insert data</span></span>
<span data-ttu-id="8d45b-138">JavaScript nesne hello uygun tarih çağrısı ile oluşturup `table.insert()` zaman uyumsuz olarak:</span><span class="sxs-lookup"><span data-stu-id="8d45b-138">Create a JavaScript object with hello appropriate date and call `table.insert()` asynchronously:</span></span>

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

<span data-ttu-id="8d45b-139">Başarılı ekleme üzerinde eşitleme işlemleri için gerekli olan ek alanlar hello ile eklenen hello öğesi döndürülür.</span><span class="sxs-lookup"><span data-stu-id="8d45b-139">On successful insertion, hello inserted item is returned with hello additional fields that are required for sync operations.</span></span>  <span data-ttu-id="8d45b-140">Sonraki güncelleştirmeler için önbelleğinizi bu bilgilerle güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="8d45b-140">Update your own cache with this information for later updates.</span></span>

<span data-ttu-id="8d45b-141">Hello Azure Mobile Apps Node.js sunucusu SDK Geliştirme amaçlı dinamik şema destekler.</span><span class="sxs-lookup"><span data-stu-id="8d45b-141">hello Azure Mobile Apps Node.js Server SDK supports dynamic schema for development purposes.</span></span>  <span data-ttu-id="8d45b-142">Dinamik şema bir INSERT veya update işleminde belirterek tooadd sütunlarını toohello tabloyu sağlar.</span><span class="sxs-lookup"><span data-stu-id="8d45b-142">Dynamic Schema allows you tooadd columns toohello table by specifying them in an insert or update operation.</span></span>  <span data-ttu-id="8d45b-143">Uygulama tooproduction taşımadan önce dinamik şema devre dışı bırakma öneririz.</span><span class="sxs-lookup"><span data-stu-id="8d45b-143">We recommend that you turn off dynamic schema before moving your application tooproduction.</span></span>

### <span data-ttu-id="8d45b-144"><a name="modifying"></a>Nasıl yapılır: Verileri değiştirme</span><span class="sxs-lookup"><span data-stu-id="8d45b-144"><a name="modifying"></a>How to: Modify data</span></span>
<span data-ttu-id="8d45b-145">Benzer toohello `.insert()` yöntemi, bir güncelleştirme nesnesi oluşturun ve gerekir'ı çağırın `.update()`.</span><span class="sxs-lookup"><span data-stu-id="8d45b-145">Similar toohello `.insert()` method, you should create an Update object and then call `.update()`.</span></span>  <span data-ttu-id="8d45b-146">Merhaba güncelleştirme nesnesi hello kayıt toobe güncelleştirilmiş hello Kimliğini içermelidir - hello kayıt okunurken veya çağrılırken hello kimliği elde `.insert()`.</span><span class="sxs-lookup"><span data-stu-id="8d45b-146">hello update object must contain hello ID of hello record toobe updated - hello ID is obtained when reading hello record or when calling `.insert()`.</span></span>

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

### <span data-ttu-id="8d45b-147"><a name="deleting"></a>Nasıl yapılır: Veri silme</span><span class="sxs-lookup"><span data-stu-id="8d45b-147"><a name="deleting"></a>How to: Delete data</span></span>
<span data-ttu-id="8d45b-148">toodelete bir kayıt çağrısı hello `.del()` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="8d45b-148">toodelete a record, call hello `.del()` method.</span></span>  <span data-ttu-id="8d45b-149">Nesne başvurusu geçişi hello kimliği:</span><span class="sxs-lookup"><span data-stu-id="8d45b-149">Pass hello ID in an object reference:</span></span>

```
table
    .del({ id: '7163bc7a-70b2-4dde-98e9-8818969611bd' })
    .done(function () {
        // Record is now deleted - update your cache
    }, failure);
```
