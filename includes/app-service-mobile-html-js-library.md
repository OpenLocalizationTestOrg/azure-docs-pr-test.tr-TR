## <a name="create-client"></a>İstemci bağlantısı oluşturma
Bir `WindowsAzure.MobileServiceClient` nesnesi oluşturarak istemci bağlantısı oluşturun.  Değiştir `appUrl` URL tooyour mobil uygulama ile.

```
var client = WindowsAzure.MobileServiceClient(appUrl);
```

## <a name="table-reference"></a>Tablolarla çalışma
tooaccess veya güncelleştirme veriler, bir başvuru toohello arka uç tablosu oluşturun. Değiştir `tableName` tablonuz hello adı

```
var table = client.getTable(tableName);
```

Bir tablo başvurusu oluşturduktan sonra tablonuzla başka işlemler yapabilirsiniz:

* [Tablo sorgulama](#querying)
  * [Verileri filtreleme](#table-filter)
  * [Verileri sayfalama](#table-paging)
  * [Verileri sıralama](#sorting-data)
* [Veri ekleme](#inserting)
* [Verileri değiştirme](#modifying)
* [Veri silme](#deleting)

### <a name="querying"></a>Nasıl yapılır: Tablo başvurusu sorgulama
Bir tablo başvurusu olduktan sonra onu tooquery hello sunucusundaki veriler için kullanabilirsiniz.  Sorgular "LINQ benzeri" bir dilde yapılır.
tooreturn hello tablodan aşağıdaki kullanım hello tüm veri kod:

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

Merhaba başarı işlev hello sonuçlarıyla çağrılır.  Kullanmayın `for (var i in results)` hello başarı içinde işlev hello sonuçlara dahil bilgi üzerinden yineleme şekilde, diğer sorgu işlevleri (gibi `.includeTotalCount()`) kullanılır.

Merhaba hello sorgu söz dizimi hakkında daha fazla bilgi için bkz. [sorgu nesne belgelerini].

#### <a name="table-filter"></a>Merhaba sunucusundaki verileri filtreleme
Kullanabileceğiniz bir `where` hello tablo başvurusu yan tümcesi:

```
table
    .where({ userId: user.userId, complete: false })
    .read()
    .then(success, failure);
```

Merhaba nesne filtreler işlevi de kullanabilirsiniz.  Bu durumda, hello `this` değişkeni filtre uygulanan toothe geçerli nesneye atanmış.  koddan hello işlevsel olarak eşdeğer toohello önceki örnek verilmiştir:

```
function filterByUserId(currentUserId) {
    return this.userId === currentUserId && this.complete === false;
}

table
    .where(filterByUserId, user.userId)
    .read()
    .then(success, failure);
```

#### <a name="table-paging"></a>Verileri sayfalama
Merhaba kullanan `take()` ve `skip()` yöntemleri.  Örneğin, 100-satırı kayıtlar toosplit hello tablo istiyorsanız:

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

Merhaba `.includeTotalCount()` kullanılan tooadd totalCount alan toohello sonuçları nesne bir yöntemdir.  TotalCount alanı hello toplam hiçbir disk belleği kullanılırsa döndürülür kayıt sayısı ile doldurulur.

Daha sonra hello sayfa değişkeni ve bazı kullanıcı Arabirimi düğmeleri tooprovide sayfa listesi kullanabilirsiniz; kullanmak `loadPage()` hello yeni kayıtlar için her bir sayfa yüklenemiyor.  Daha önce yüklenmiş önbelleğe alma toospeed erişim toorecords uygulayın.

#### <a name="sorting-data"></a>Nasıl yapılır: Sıralanmış veriler döndürme
Kullanım hello `.orderBy()` veya `.orderByDescending()` sorgu yöntemleri:

```
table
    .orderBy('name')
    .read()
    .then(success, failure);
```

Merhaba hello sorgu nesnesi hakkında daha fazla bilgi için bkz. [sorgu nesne belgelerini].

### <a name="inserting"></a>Nasıl yapılır: Veri ekleme
JavaScript nesne hello uygun tarih çağrısı ile oluşturup `table.insert()` zaman uyumsuz olarak:

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

Başarılı ekleme üzerinde eşitleme işlemleri için gerekli olan ek alanlar hello ile eklenen hello öğesi döndürülür.  Sonraki güncelleştirmeler için önbelleğinizi bu bilgilerle güncelleştirin.

Hello Azure Mobile Apps Node.js sunucusu SDK Geliştirme amaçlı dinamik şema destekler.  Dinamik şema bir INSERT veya update işleminde belirterek tooadd sütunlarını toohello tabloyu sağlar.  Uygulama tooproduction taşımadan önce dinamik şema devre dışı bırakma öneririz.

### <a name="modifying"></a>Nasıl yapılır: Verileri değiştirme
Benzer toohello `.insert()` yöntemi, bir güncelleştirme nesnesi oluşturun ve gerekir'ı çağırın `.update()`.  Merhaba güncelleştirme nesnesi hello kayıt toobe güncelleştirilmiş hello Kimliğini içermelidir - hello kayıt okunurken veya çağrılırken hello kimliği elde `.insert()`.

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

### <a name="deleting"></a>Nasıl yapılır: Veri silme
toodelete bir kayıt çağrısı hello `.del()` yöntemi.  Nesne başvurusu geçişi hello kimliği:

```
table
    .del({ id: '7163bc7a-70b2-4dde-98e9-8818969611bd' })
    .done(function () {
        // Record is now deleted - update your cache
    }, failure);
```
