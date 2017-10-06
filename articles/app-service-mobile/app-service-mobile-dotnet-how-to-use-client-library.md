---
title: "aaaWorking hello App Service Mobile Apps ile yönetilen istemci kitaplığı (Windows | Microsoft Docs"
description: "Bilgi nasıl toouse Azure App Service Mobile Apps ile Windows ve Xamarin uygulamaları için .NET istemcisi."
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 0280785c-e027-4e0d-aaf2-6f155e5a6197
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 01/04/2017
ms.author: glenga
ms.openlocfilehash: b056e606b19406398f5b6faabb0931ad651125e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-managed-client-for-azure-mobile-apps"></a>Nasıl toouse hello Azure Mobile Apps için yönetilen
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

## <a name="overview"></a>Genel Bakış
Bu kılavuz size nasıl hello kullanarak tooperform genel senaryolar için Azure App Service Mobile uygulamaları Windows ve Xamarin uygulamaları için istemci kitaplığı yönetilen gösterir. Yeni tooMobile uygulamalar varsa, ilk Tamamlanıyor hello düşünmelisiniz [Azure Mobile Apps quickstart] [ 1] Öğreticisi. Bu kılavuzda, biz hello üzerinde odaklanmak istemci-tarafı yönetilen SDK. toolearn hakkında daha fazla bilgi mobil uygulamaları için sunucu tarafı SDK'ları Merhaba, hello hello belgelerine bakın [.NET Server SDK] [ 2] veya [Node.js sunucusu SDK] [ 3].

## <a name="reference-documentation"></a>Başvuru belgeleri
Merhaba başvuru belgeleri hello istemci SDK'sı için aşağıda bulunur: [Azure Mobile Apps .NET istemci başvurusu][4].
Hello birkaç istemci örnekleri de bulabilirsiniz [Azure-Samples GitHub deposunu][5].

## <a name="supported-platforms"></a>Desteklenen platformlar
Merhaba .NET platformu hello aşağıdaki platformları destekler:

* Xamarin Android API 19 için 24 (KitKat Nougat aracılığıyla) aracılığıyla yayımlar.
* Xamarin iOS iOS 8.0 ve sonraki sürümler için serbest bırakır
* Evrensel Windows platformu
* Windows Phone 8.1
* Windows Phone 8.0 Silverlight uygulamalarının dışında

Merhaba "sunucu akış" kimlik doğrulaması için kullanıcı Arabirimi sunulan hello bir Web görünümü kullanır.  Merhaba cihaz mümkün toopresent WebView UI değilse, diğer kimlik doğrulama yöntemlerini gereklidir.  Bu SDK böylece Gözcü türü veya benzer şekilde kısıtlı aygıtlar için uygun değil.

## <a name="setup"></a>Kurulum ve Önkoşullar
Zaten oluşturulmuş ve en az bir tablo içeren mobil uygulama arka uç projeniz, yayımlanan olduğunu varsayıyoruz.  Bu konuda kullanılan hello kodda hello tablo adlı `TodoItem` ve sütunları aşağıdaki hello vardır: `Id`, `Text`, ve `Complete`. Aynı tablo oluşturulan tamamladığınızda hello bu tablodur [Azure Mobile Apps quickstart][1].

Merhaba karşılık gelen yazılan istemci-tarafı C# sınıfı aşağıdaki hello türüdür:

```
public class TodoItem
{
    public string Id { get; set; }

    [JsonProperty(PropertyName = "text")]
    public string Text { get; set; }

    [JsonProperty(PropertyName = "complete")]
    public bool Complete { get; set; }
}
```

Merhaba [JsonPropertyAttribute] [ 6] kullanılan toodefine hello olan *PropertyName* hello istemci alanı ve hello tablo alanı arasında eşleme.

nasıl toocreate tabloları, Mobile Apps arka toolearn bkz hello [.NET Server SDK konu] [ 7] veya hello [Node.js sunucusu SDK konusuna] [ 8] . Mobil uygulama arka oluşturduysanız hello Azure hızlı başlangıç Merhaba portal kullanarak, hello de kullanabilirsiniz **kolay tablolar** hello ayarı [Azure portal].

### <a name="how-to-install-hello-managed-client-sdk-package"></a>Nasıl yapılır: yükleme hello yönetilen istemci SDK paketi
Yöntemleri tooinstall hello aşağıdaki hello birini mobil uygulamaları için İstemci SDK paketi yönetilen [NuGet][9]:

* **Visual Studio** projenize sağ tıklayın, **NuGet paketlerini Yönet**, hello Ara `Microsoft.Azure.Mobile.Client` paketini ve ardından **yükleme**.
* **Xamarin Studio** projenize sağ tıklayın, **Ekle** > **NuGet paketleri Ekle**, hello Ara `Microsoft.Azure.Mobile.Client `paketini ve ardından **Ekle Paket**.

Ana etkinlik dosyanızda tooadd hello aşağıdakileri unutmayın **kullanarak** deyimi:

```
using Microsoft.WindowsAzure.MobileServices;
```

### <a name="symbolsource"></a>Nasıl yapılır: Visual Studio'da hata ayıklama simgeleri ile çalışma
Merhaba Microsoft.Azure.Mobile ad alanı Hello simgelerini bulunur [SymbolSource][10].  Toothe başvuran [SymbolSource yönergeleri] [ 11] toointegrate SymbolSource Visual Studio ile.

## <a name="create-client"></a>Merhaba Mobile Apps istemci oluşturma
Merhaba aşağıdaki kod oluşturur hello [MobileServiceClient] [ 12] kullanılan tooaccess olan nesne, mobil uygulamanızın arka ucuna.

```
var client = new MobileServiceClient("MOBILE_APP_URL");
```

Kod önceki hello yerine `MOBILE_APP_URL` hello mobil uygulama arka ucu hello URL'SİYLE hangi bulunursa, mobil uygulamanızın arka ucuna hello içinde dikey [Azure portal]. Merhaba MobileServiceClient nesne singleton olmalıdır.

## <a name="work-with-tables"></a>Tablolarla çalışma
Aşağıdaki bölümde ayrıntılara nasıl hello toosearch kayıtlarını almak ve hello tablo içindeki hello verileri değiştirebilir.  Aşağıdaki konularda hello ele alınmaktadır:

* [Bir tablo başvurusu oluşturma](#instantiating)
* [Verileri sorgulama](#querying)
* [Döndürülen veri filtreleme](#filtering)
* [Döndürülen veriler sıralama](#sorting)
* [Dönüş verileri sayfalarında](#paging)
* [Belirli sütunları seçin](#selecting)
* [Bir kayıt kimliğine göre arama](#lookingup)
* [Türsüz sorgularıyla ele alma](#untypedqueries)
* [Veri ekleme](#inserting)
* [Verileri güncelleştirme](#updating)
* [Verileri silme](#deleting)
* [Çakışma çözümü ve iyimser eşzamanlılık](#optimisticconcurrency)
* [Bağlama tooa Windows kullanıcı arabirimi](#binding)
* [Merhaba sayfa boyutunu değiştirme](#pagesize)

### <a name="instantiating"></a>Nasıl yapılır: bir tablo başvurusu oluşturma
Erişen ve arka uç tablodaki verileri değiştiren tüm hello kod üzerinde hello işlevleri çağırır `MobileServiceTable` nesnesi. Bir başvuru toohello tablosu tarafından arama hello elde [GetTable] şekilde yöntemi:

```
IMobileServiceTable<TodoItem> todoTable = client.GetTable<TodoItem>();
```

Merhaba, nesne hello yazılan serileştirme modelini kullanan döndürdü. Türsüz serileştirme modeli de desteklenir. Aşağıdaki örnek [başvuru tooan türü belirsiz bir tablo oluşturur]:

```
// Get an untyped table reference
IMobileServiceTable untypedTodoTable = client.GetTable("TodoItem");
```

Türsüz sorgularda OData sorgu dizesi temel hello belirtmeniz gerekir.

### <a name="querying"></a>Nasıl yapılır: Mobil uygulamanızın veri sorgulama
Bu bölümde, nasıl tooissue işlevselliği aşağıdaki hello içeren toohello mobil uygulama arka sorgular açıklanmaktadır:

* [Döndürülen veri filtreleme](#filtering)
* [Döndürülen veriler sıralama](#sorting)
* [Dönüş verileri sayfalarında](#paging)
* [Belirli sütunları seçin](#selecting)
* [Veri Kimliğe göre arayın](#lookingup)

> [!NOTE]
> Bir sunucu tabanlı sayfa boyutu tüm satırları döndürülmesini zorlanan tooprevent ' dir.  Disk belleği hello hizmet olumsuz etkileyen büyük veri kümeleri için varsayılan istekleri tutar.  50 satır birden çok tooreturn kullanmak hello `Skip` ve `Take` açıklandığı gibi yöntemi [veri sayfalarında dönmek](#paging).

### <a name="filtering"></a>Nasıl yapılır: Filtre veri döndürdü
Merhaba aşağıdaki kod gösterir nasıl toofilter verileri de dahil olmak üzere bir `Where` sorgu yan tümcesi. Tüm öğeleri döndürür `todoTable` , `Complete` özelliği eşittir çok`false`. Merhaba [burada] işlevi hello tablo hello sorgusu koşulu filtreleme bir satır uygular.

```
// This query filters out completed TodoItems and items without a timestamp.
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToListAsync();
```

Tarayıcının geliştirici araçları gibi ileti denetleme yazılımı kullanarak hello hello gönderilen istek toohello arka uç URI'sini görüntüleyebilir veya [Fiddler]. URI hello isteğiyle bakarsanız, hello sorgu dizesi değiştirildiğini dikkat edin:

```
GET /tables/todoitem?$filter=(complete+eq+false) HTTP/1.1
```

Bu OData isteği hello Server SDK'sı tarafından bir SQL sorgusu çevrilir:

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
```

Merhaba toohello geçirilen işlevi `Where` yöntemi koşulları rastgele bir sayı olabilir.

```
// This query filters out completed TodoItems where Text isn't null
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false && todoItem.Text != null)
    .ToListAsync();
```

Bu örnek SQL sorgusu hello Server SDK tarafından çevrilmesi:

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
          AND ISNULL(text, 0) = 0
```

Bu sorgu, birden çok yan tümcesine da bölünebilir:

```
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .Where(todoItem => todoItem.Text != null)
    .ToListAsync();
```

Merhaba iki yöntem eşdeğerdir ve birbirlerinin yerine kullanılabilir.  Önceki seçenek Hello&mdash;bir sorgu birden fazla koşullarında birleştirme,&mdash;daha compact ve önerilen.

Hello `Where` yan tümcesi olması işlemlerini destekleyen hello OData alt çevrilir. İşlemler şunları içerir:

* İlişkisel işleçler (==,! =, <, < =, >, > =),
* Aritmetik işleçler (+, -, /, *, %),
* Precision (Math.Floor, Math.Ceiling), numara
* Dize işlevleri (Uzunluk, Substring, Değiştir, IndexOf, StartsWith, EndsWith)
* Tarih özellikleri (yıl, ay, gün, saat, dakika, saniye)
* Erişim, nesne özelliklerini ve
* Bu işlemleri birleştirme ifadeler.

Ne göz önünde bulundurularak sunucusu SDK hello desteklediğinde, hello düşünebilirsiniz [OData v3 belgelerine].

### <a name="sorting"></a>Nasıl yapılır: sıralama döndürülen verileri
Merhaba aşağıdaki kod gösterir nasıl toosort verileri de dahil olmak üzere bir [OrderBy] veya [OrderByDescending] hello sorgusunda işlevi. Öğelerden döndürür `todoTable` hello göre artan `Text` alan.

```
// Sort items in ascending order by Text field
MobileServiceTableQuery<TodoItem> query = todoTable
                .OrderBy(todoItem => todoItem.Text)
List<TodoItem> items = await query.ToListAsync();

// Sort items in descending order by Text field
MobileServiceTableQuery<TodoItem> query = todoTable
                .OrderByDescending(todoItem => todoItem.Text)
List<TodoItem> items = await query.ToListAsync();
```

### <a name="paging"></a>Nasıl yapılır: veri sayfalarında Döndür
Varsayılan olarak, hello arka uç yalnızca hello ilk 50 satırları döndürür. Arama hello tarafından döndürülen satır sayısını hello artırabilirsiniz [ele] yöntemi. Kullanım `Take` hello birlikte [atla] yöntemi toorequest "Merhaba sorgu tarafından döndürülen belirli bir sayfa" Merhaba toplam veri kümesinin. Merhaba çalıştırıldığında, aşağıdaki sorguyu hello ilk üç öğeleri hello tablodaki döndürür.

```
// Define a filtered query that returns hello top 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Take(3);
List<TodoItem> items = await query.ToListAsync();
```

Merhaba aşağıdaki değiştirilen sorgu atlar hello ilk üç sonuçları ve sonraki üç sonuçları döndürür hello. Bu sorgu hello ikinci "sayfasının" Merhaba sayfa boyutu üç öğe olduğu veri üretir.

```
// Define a filtered query that skips hello top 3 items and returns hello next 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Skip(3).Take(3);
List<TodoItem> items = await query.ToListAsync();
```

Merhaba [IncludeTotalCount] yöntemi için toplam sayıyı hello ister *tüm* Merhaba, belirtilen herhangi bir disk belleği/sınırı koşul yoksayılıyor verilinceye kaydeder:

```
query = query.IncludeTotalCount();
```

Gerçek dünya uygulamada sayfaları arasında gezinmek için bir çağrı cihazı denetim veya karşılaştırılabilir UI örnekle önceki sorgular benzer toohello kullanabilirsiniz.

> [!NOTE]
> toooverride hello 50 satır sınırı bir mobil uygulama arka ucu, hello de uygulamalısınız [EnableQueryAttribute] toohello genel alma yöntemini ve Başlangıç disk belleği davranışı belirtin. Ne zaman uygulanan toohello yöntemi, aşağıdaki hello en fazla döndürülen satır too1000 ayarlar:
>
> `[EnableQuery(MaxTop=1000)]`


### <a name="selecting"></a>Nasıl yapılır: Belirli sütunları seçin
Özellikler tooinclude hello içinde hangi kümesi ekleyerek sonuçları belirtebilirsiniz bir [seçin] yan tümcesi tooyour sorgu. Örneğin, kod gösterir nasıl aşağıdaki hello tooselect tek bir alana ve ayrıca nasıl tooselect ve birden çok alan Biçimlendir:

```
// Select one field -- just hello Text
MobileServiceTableQuery<TodoItem> query = todoTable
                .Select(todoItem => todoItem.Text);
List<string> items = await query.ToListAsync();

// Select multiple fields -- both Complete and Text info
MobileServiceTableQuery<TodoItem> query = todoTable
                .Select(todoItem => string.Format("{0} -- {1}",
                    todoItem.Text.PadRight(30), todoItem.Complete ?
                    "Now complete!" : "Incomplete!"));
List<string> items = await query.ToListAsync();
```

Tüm işlevleri şimdiye kadar anlatılan hello olan biz zincirleme bunları tutmak için eklenebilir. Her zincirleme çağrı hello sorgusunun daha fazla etkiler. Daha fazla örnek:

```
MobileServiceTableQuery<TodoItem> query = todoTable
                .Where(todoItem => todoItem.Complete == false)
                .Select(todoItem => todoItem.Text)
                .Skip(3).
                .Take(3);
List<string> items = await query.ToListAsync();
```

### <a name="lookingup"></a>Nasıl yapılır: veri Kimliğe göre arayın
Merhaba [LookupAsync] işlevi kullanılan toolook nesneleri belirli bir kimliğe sahip hello veritabanından olabilir

```
// This query filters out hello item with hello ID of 37BBF396-11F0-4B39-85C8-B319C729AF6D
TodoItem item = await todoTable.LookupAsync("37BBF396-11F0-4B39-85C8-B319C729AF6D");
```

### <a name="untypedqueries"></a>Nasıl yapılır: türsüz sorgularını Yürüt
Türsüz tablo nesneyi kullanarak bir sorgu yürütülürken açıkça hello OData sorgu dizesi çağırarak belirtmeniz gerekir [ReadAsync], aşağıdaki örneğine hello olarak:

```
// Lookup untyped data using OData
JToken untypedItems = await untypedTodoTable.ReadAsync("$filter=complete eq 0&$orderby=text");
```

Bir özellik paketi gibi kullandığınız JSON değerleri ulaşırsınız. Merhaba JToken ve Newtonsoft Json.NET hakkında daha fazla bilgi için bkz: [Json.NET] site.

### <a name="inserting"></a>Nasıl yapılır: bir mobil uygulama arka ucu veri Ekle
Tüm istemci türleri adlı bir üye içermelidir **kimliği**, olduğu varsayılan olarak bir dize. Bu **kimliği** CRUD işlemleri gerçekleştirmek için gereken ve koddan çevrimdışı eşitleme. Merhaba göstermektedir nasıl toouse hello [InsertAsync] yöntemi tooinsert yeni satırlar bir tabloya. Merhaba parametresi .NET nesnesi olarak eklenen hello veri toobe içerir.

```
await todoTable.InsertAsync(todoItem);
```

Benzersiz ve özel bir kimlik değeri hello dahil edilmemesi durumunda `todoItem` bir ekleme sırasında bir GUID hello sunucusu tarafından oluşturulur.
Alabilirsiniz hello hello çağrısı döndükten sonra hello nesne inceleyerek kimliği oluşturulur.

Veri tooinsert türsüz, Json.NET yararlanmak:

```
JObject jo = new JObject();
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

Benzersiz bir dize kimliği olarak bir e-posta adresi kullanarak örnek aşağıda verilmiştir:

```
JObject jo = new JObject();
jo.Add("id", "myemail@emaildomain.com");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

### <a name="working-with-id-values"></a>KOD değerleri ile çalışma
Mobil uygulamaları destekleyen özel benzersiz bir dize değerleri Merhaba tablonun için **kimliği** sütun. Bir dize değeri uygulamaların hello kimliği kullanıcı adlarını veya e-posta adresleri gibi özel değerler toouse sağlar.  Dize kimlikleri ile Merhaba aşağıdaki avantajları sağlar:

* Gidiş dönüş toohello veritabanı yapmadan kimlikleri üretilir.
* Farklı tablolar veya veritabanlarına daha kolay toomerge kayıtlarıdır.
* Kimlikleri değerleri daha iyi bir uygulama mantığı ile tümleştirebilirsiniz.

Bir dize kimliği değeri eklenen bir kayıtta ayarlanmadığında hello mobil uygulama arka ucu benzersiz bir değer için bir kimlik oluşturur. Merhaba kullanabilirsiniz [Guid.NewGuid] kendi Kimliğinizi değerleri, hello istemcide veya hello arka uç yöntemi toogenerate.

```
JObject jo = new JObject();
jo.Add("id", Guid.NewGuid().ToString("N"));
```

### <a name="modifying"></a>Nasıl yapılır: bir mobil uygulama arka ucu verileri değiştirme
Merhaba aşağıdaki kod gösterir nasıl toouse hello [UpdateAsync] yöntemi tooupdate hello varolan bir kayıtla aynı kimliği yeni bilgilerle. Merhaba parametresi .NET nesnesi olarak güncelleştirilen hello veri toobe içerir.

```
await todoTable.UpdateAsync(todoItem);
```

tooupdate türsüz veri, avantajlarından alabilir [Json.NET] gibi:

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.UpdateAsync(jo);
```

Bir `id` alan bir güncelleştirme yaparken belirtilmelidir. Merhaba arka uç kullanan hello `id` tooupdate satır alan tooidentify. Merhaba `id` alan hello hello sonucundan elde edilebilir `InsertAsync` çağırın. Bir `ArgumentException` hello sağlamadan tooupdate öğeyi çalışırsanız tetiklenir `id` değeri.

### <a name="deleting"></a>Nasıl yapılır: bir mobil uygulama arka ucu verileri Sil
Merhaba aşağıdaki kod gösterir nasıl toouse hello [DeleteAsync] yöntemi toodelete var olan bir örneği. Merhaba örneği hello tarafından tanımlanan `id` alan hello kümesinde `todoItem`.

```
await todoTable.DeleteAsync(todoItem);
```

Veri toodelete türsüz, Json.NET avantajlarından şekilde alabilir:

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
await table.DeleteAsync(jo);
```

Bir silme isteği yaptığınızda, bir kimliği belirtilmelidir. Diğer özellikler toohello hizmet geçmedi veya hello hizmeti göz ardı edilir. Merhaba sonucunu bir `DeleteAsync` çağrıdır genellikle `null`. Merhaba kimliği toopass hello hello sonucundan elde edilebilir `InsertAsync` çağırın. A `MobileServiceInvalidOperationException` hello belirtmeden toodelete öğeyi çalıştığınızda durum `id` alan.

### <a name="optimisticconcurrency"></a>Nasıl yapılır: kullanım iyimser eşzamanlılık çakışması çözümleme
İki veya daha fazla istemcileri yazma değişiklikleri toohello aynı öğe hello aynı saat. Çakışma algılaması hello son yazma herhangi bir önceki güncelleştirme üzerine yazacak. **İyimser eşzamanlılık denetimini** her işlem tamamlayabilir ve bu nedenle hiçbir kaynak kilitleme kullanmaz varsayar.  Bir işlem gerçekleştirmeden önce başka bir işlem hello veri değiştirdi iyimser eşzamanlılık denetimini doğrular. Merhaba veri değiştirilirse işlemi sonlandırdı hello geri alınır.

Mobil uygulamaları hello kullanarak değişiklikleri tooeach öğesi izleyerek iyimser eşzamanlılık denetimini destekleyen `version` , mobil uygulamanızın arka ucuna her tablo için tanımlanan sistem özelliği sütun. Bir kayıt güncelleştirilir, her zaman Mobile Apps hello ayarlar `version` söz konusu özellik kayıt tooa yeni bir değer. Her güncelleştirme isteği sırasında hello `version` özelliktir hello istekte hello kaydının karşılaştırılan toohello hello sunucuda hello kaydı için aynı özelliği. Sürüm ile aktarılırsa hello isteği hello arka uç eşleşmiyor sonra hello istemci kitaplığı başlatır bir `MobileServicePreconditionFailedException<T>` özel durum. Merhaba özel durumla dahil hello hello kayıt sürümünden hello arka uç içeren hello sunucuları hello kayıt türüdür. Merhaba uygulama daha sonra bu bilgileri toodecide olup kullanabilirsiniz tooexecute hello güncelleştirme isteğini yeniden hello doğru `version` hello arka uç toocommit değişikliklerden değeri.

Merhaba tablo sınıfındaki hello için bir sütun tanımlamak `version` sistem özelliği tooenable iyimser eşzamanlılık. Örneğin:

```
public class TodoItem
{
    public string Id { get; set; }

    [JsonProperty(PropertyName = "text")]
    public string Text { get; set; }

    [JsonProperty(PropertyName = "complete")]
    public bool Complete { get; set; }

    // *** Enable Optimistic Concurrency *** //
    [JsonProperty(PropertyName = "version")]
    public string Version { set; get; }
}
```

Türsüz tabloları kullanarak uygulamaları etkinleştirme iyimser eşzamanlılık ayarı hello tarafından `Version` üzerinde bayrak `SystemProperties` Merhaba tablo gibi.

```
//Enable optimistic concurrency by retrieving version
todoTable.SystemProperties |= MobileServiceSystemProperties.Version;
```

İçinde toplama tooenabling iyimser eşzamanlılık, siz de hello catch gerekir `MobileServicePreconditionFailedException<T>` kodunuzda çağrılırken özel durum [UpdateAsync].  Merhaba doğru uygulayarak Hello çakışmayı `version` toothe güncelleştirilmiş kayıt ve çağrı [UpdateAsync] kayıt hello ile çözümlendi. koddan hello nasıl tooresolve bir yazma çakışması kez algılandığını gösterir:

```
private async void UpdateToDoItem(TodoItem item)
{
    MobileServicePreconditionFailedException<TodoItem> exception = null;

    try
    {
        //update at hello remote table
        await todoTable.UpdateAsync(item);
    }
    catch (MobileServicePreconditionFailedException<TodoItem> writeException)
    {
        exception = writeException;
    }

    if (exception != null)
    {
        // Conflict detected, hello item has changed since hello last query
        // Resolve hello conflict between hello local and server item
        await ResolveConflict(item, exception.Item);
    }
}


private async Task ResolveConflict(TodoItem localItem, TodoItem serverItem)
{
    //Ask user toochoose hello resoltion between versions
    MessageDialog msgDialog = new MessageDialog(
        String.Format("Server Text: \"{0}\" \nLocal Text: \"{1}\"\n",
        serverItem.Text, localItem.Text),
        "CONFLICT DETECTED - Select a resolution:");

    UICommand localBtn = new UICommand("Commit Local Text");
    UICommand ServerBtn = new UICommand("Leave Server Text");
    msgDialog.Commands.Add(localBtn);
    msgDialog.Commands.Add(ServerBtn);

    localBtn.Invoked = async (IUICommand command) =>
    {
        // tooresolve hello conflict, update hello version of hello item being committed. Otherwise, you will keep
        // catching a MobileServicePreConditionFailedException.
        localItem.Version = serverItem.Version;

        // Updating recursively here just in case another change happened while hello user was making a decision
        UpdateToDoItem(localItem);
    };

    ServerBtn.Invoked = async (IUICommand command) =>
    {
        RefreshTodoItems();
    };

    await msgDialog.ShowAsync();
}
```

Merhaba daha fazla bilgi için bkz: [çevrimdışı veri eşitlemeye Azure Mobile Apps içinde] konu.

### <a name="binding"></a>Nasıl yapılır: bağlama Mobile Apps veri tooa Windows kullanıcı arabirimi
Bu bölüm, nasıl bir Windows uygulamasında kullanıcı Arabirimi öğeleri kullanarak veri nesneleri toodisplay döndürülen gösterir.  Aşağıdaki kod örneği, tamamlanmamış öğeleri için bir sorgu ile Merhaba listesi toohello kaynağı bağlar. [MobileServiceCollection] mobil uygulamaları algılayan bir bağlama koleksiyonu oluşturur.

```
// This query filters out completed TodoItems.
MobileServiceCollection<TodoItem, TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToCollectionAsync();

// itemsControl is an IEnumerable that could be bound tooa UI list control
IEnumerable itemsControl  = items;

// Bind this tooa ListBox
ListBox lb = new ListBox();
lb.ItemsSource = items;
```

Bazı denetimler hello yönetilen bir arabirim adlı çalışma zamanı desteği [ISupportIncrementalLoading]. Bu arabirim denetimleri toorequest verir hello kullanıcı kaydırdığında ek veriler. Bu arabirim için evrensel Windows uygulamaları için yerleşik destek [MobileServiceIncrementalLoadingCollection], otomatik olarak işleme hello denetimleri gelen çağrıları. Kullanım `MobileServiceIncrementalLoadingCollection` şekilde Windows uygulamalarında:

```
MobileServiceIncrementalLoadingCollection<TodoItem,TodoItem> items;
items = todoTable.Where(todoItem => todoItem.Complete == false).ToIncrementalLoadingCollection();

ListBox lb = new ListBox();
lb.ItemsSource = items;
```

toouse hello Windows Phone 8 ve "Silverlight" uygulamaları, kullanım hello üzerinde yeni bir koleksiyon `ToCollection` genişletme yöntemleri `IMobileServiceTableQuery<T>` ve `IMobileServiceTable<T>`. Çağrı tooload verileri `LoadMoreItemsAsync()`.

```
MobileServiceCollection<TodoItem, TodoItem> items = todoTable.Where(todoItem => todoItem.Complete==false).ToCollection();
await items.LoadMoreItemsAsync();
```

Çağrılarak oluşturulan hello koleksiyonu kullandığınızda `ToCollectionAsync` veya `ToCollection`, ilişkili tooUI denetimler olabilir bir koleksiyon alın.  Bu disk belleği algılayan koleksiyonudur.  Merhaba koleksiyon verileri ağ üzerinden yüklüyor olduğundan, bazen yükleme başarısız olur. toohandle böyle hataları geçersiz kılma hello `OnException` yöntemi `MobileServiceIncrementalLoadingCollection` gelen çağrıları çok kaynaklanan toohandle özel durumları`LoadMoreItemsAsync`.

Tablonuzda fazla alan var ancak yalnızca toodisplay istediğiniz göz önünde bulundurun bazıları, denetimi. Önceki bölümde hello hello kılavuzunu kullanabilir "[belirli sütunları seçmek](#selecting)" Merhaba UI içinde tooselect belirli sütunlardaki toodisplay.

### <a name="pagesize"></a>Değişiklik hello sayfa boyutu
Azure mobil uygulamalar varsayılan olarak en fazla istek başına 50 öğe döndürür.  Merhaba istemci ve sunucudaki hello maksimum sayfa boyutunu artırarak Başlangıç disk belleği boyutunu değiştirebilirsiniz.  tooincrease istenen sayfa boyutu Merhaba, belirtin `PullOptions` kullanırken `PullAsync()`:

```
PullOptions pullOptions = new PullOptions
    {
        MaxPageSize = 100
    };
```

Merhaba yaptığınız varsayılarak `PageSize` eşit tooor hello sunucu içindeki 100'den büyük, bir istek en fazla 100 öğeleri döndürür.

## <a name="#offlinesync"></a>Çevrimdışı tablolarla çalışma
Çevrimdışı tabloları yerel bir SQLite deposu toostore veri çevrimdışı olduğunda kullanın.  Tüm tablo işlemleri hello karşı yapılır hello uzak sunucu deposu yerine yerel SQLite depolar.  Çevrimdışı bir tablo toocreate ilk projenizi hazırlayın:

1. Visual Studio'da hello çözüme sağ tıklayın > **çözüm için NuGet paketlerini Yönet...** , ardından arayın ve yükleyin **Microsoft.Azure.Mobile.Client.SQLiteStore** hello Çözümdeki tüm projeleri için NuGet paketi.
2. (İsteğe bağlı) toosupport Windows cihazları, SQLite çalışma zamanı paketleri aşağıdaki hello birini yükleyin:

   * **Windows 8.1 çalışma zamanı:** yükleme [Windows 8.1 için SQLite][3].
   * **Windows Phone 8.1:** yükleme [Windows Phone 8.1 için SQLite][4].
   * **Evrensel Windows platformu** yükleme [Evrensel Windows hello için SQLite][5].
3. (İsteğe bağlı). Windows cihazlar için tıklatın **başvuruları** > **Başvuru Ekle...** , hello genişletin **Windows** klasörü > **uzantıları**, uygun hello etkinleştirmek **SQLite için Windows** hello birlikteSDK **Windows için Visual C++ 2013 çalışma zamanı** SDK.
    Merhaba SQLite SDK adları biraz her Windows platformuyla farklılık gösterir.

Bir tablo başvurusu oluşturulmadan önce hello yerel depolama karşı hazırlıklı olmalıdır:

```
var store = new MobileServiceSQLiteStore(Constants.OfflineDbPath);
store.DefineTable<TodoItem>();

//Initializes hello SyncContext using hello default IMobileServiceSyncHandler.
await this.client.SyncContext.InitializeAsync(store);
```

Merhaba istemci hemen oluşturulduktan sonra depolama başlatma normal olarak gerçekleştirilir.  Merhaba **OfflineDbPath** filename desteklediğiniz tüm platformlarda kullanmaya uygun olmalıdır.  Merhaba yol tam nitelenmiş bir yol ise (diğer bir deyişle, bir eğik çizgi ile başlar), bu yolun kullanılır.  Merhaba yolu tam olarak nitelenmiş değil, hello dosya bir platforma özgü konuma yerleştirilir.

* İOS ve Android cihazlar için hello varsayılan hello "Kişisel dosyalar" klasör yoludur.
* Windows cihazlar için hello uygulamaya özgü "AppData" klasörü hello varsayılan yoldur.

Bir tablo başvurusu hello kullanılarak edinilebilir `GetSyncTable<>` yöntemi:

```
var table = client.GetSyncTable<TodoItem>();
```

Tooauthenticate toouse çevrimdışı bir tablo gerekmez.  Merhaba arka uç hizmeti ile iletişim kurarken tooauthenticate yeterlidir.

### <a name="syncoffline"></a>Çevrimdışı bir tablo eşitleniyor
Çevrimdışı tabloları hello arka ucuyla varsayılan olarak eşitlenmez.  Eşitleme iki parçalara bölünür.  Yeni öğeler indirmelerinin değişiklikleri ayrı olarak gönderebilir.  Tipik eşitleme yöntemi şöyledir:

```
public async Task SyncAsync()
{
    ReadOnlyCollection<MobileServiceTableOperationError> syncErrors = null;

    try
    {
        await this.client.SyncContext.PushAsync();

        await this.todoTable.PullAsync(
            //hello first parameter is a query name that is used internally by hello client SDK tooimplement incremental sync.
            //Use a different query name for each unique query in your program
            "allTodoItems",
            this.todoTable.CreateQuery());
    }
    catch (MobileServicePushFailedException exc)
    {
        if (exc.PushResult != null)
        {
            syncErrors = exc.PushResult.Errors;
        }
    }

    // Simple error/conflict handling. A real application would handle hello various errors like network conditions,
    // server conflicts and others via hello IMobileServiceSyncHandler.
    if (syncErrors != null)
    {
        foreach (var error in syncErrors)
        {
            if (error.OperationKind == MobileServiceTableOperationKind.Update && error.Result != null)
            {
                //Update failed, reverting tooserver's copy.
                await error.CancelAndUpdateItemAsync(error.Result);
            }
            else
            {
                // Discard local change.
                await error.CancelAndDiscardItemAsync();
            }

            Debug.WriteLine(@"Error executing sync operation. Item: {0} ({1}). Operation discarded.", error.TableName, error.Item["id"]);
        }
    }
}
```

İlk bağımsız değişkeni çok hello`PullAsync` null, artımlı eşitleme değil kullanılır.  Her eşitleme işlemi, tüm kayıtları alır.

Merhaba SDK gerçekleştirir örtülü `PushAsync()` kayıtları çekme önce.

Çakışma işleme olur bir `PullAsync()` yöntemi.  Hello çakışmalı aynı başa çevrimiçi tabloları şekilde.  Merhaba çakışma üretileceğini zaman `PullAsync()` hello INSERT, update veya delete sırasında yerine olarak adlandırılır. Birden çok çakışma görülüyorsa, bunların tek MobileServicePushFailedException paketlenmiştir.  Her hata ayrı olarak işler.

## <a name="#customapi"></a>Özel bir API ile çalışma
Özel bir API değil tooan INSERT eşleme, güncelleştirme, silme veya okuma işlemi sunucusu işlevselliği kullanıma toodefine özel uç noktaları sağlar. Özel bir API kullanarak, okuma ve HTTP ileti üstbilgilerini ayarlama ve JSON dışında bir ileti gövdesinin biçimi tanımlama gibi Mesajlaşma üzerinde daha fazla denetim olabilir.

Merhaba birini çağırarak özel bir API çağrısı [InvokeApiAsync] hello istemcide yöntemleri. Örneğin, aşağıdaki kod hello bir POST isteği toohello gönderir **completeAll** hello arka uç API:

```
var result = await client.InvokeApiAsync<MarkAllResult>("completeAll", System.Net.Http.HttpMethod.Post, null);
```

Bu form yazılan yöntem çağrısı ve o hello gerektirir **MarkAllResult** dönüş türü tanımlanmıştır. Yazılan ve türsüz yöntemleri desteklenir.

Merhaba InvokeApiAsync() yöntemi toohello hello API ile başlayan sürece toocall istediğiniz '/ api /' API başına bir '/'.
Örneğin:

* `InvokeApiAsync("completeAll",...)`Merhaba arka uçta /api/completeAll çağırır
* `InvokeApiAsync("/.auth/me",...)`Merhaba arka uçta /.auth/Me çağırır

Tanımlı değil Bu WebAPIs Azure Mobile Apps ile de dahil olmak üzere tüm Webapı InvokeApiAsync toocall kullanabilirsiniz.  InvokeApiAsync() kullandığınızda, kimlik doğrulama üstbilgileri dahil olmak üzere hello uygun üstbilgileri hello isteği gönderilir.

## <a name="authentication"></a>Kullanıcıların kimlik doğrulaması
Mobile Apps, kimlik doğrulaması ve çeşitli dış kimlik sağlayıcılarını kullanarak uygulama kullanıcıları yetkilendirmek destekler: Facebook, Google, Microsoft Account, Twitter ve Azure Active Directory. Tooonly kimliği doğrulanmış kullanıcıların belirli işlemler için tabloları toorestrict erişim izinlerini ayarlayabilirsiniz. Sunucu komut dosyalarında kimliği doğrulanmış kullanıcılar tooimplement yetkilendirme kuralları hello kimliğini de kullanabilirsiniz. Merhaba öğretici daha fazla bilgi için bkz [Ekle kimlik doğrulama tooyour uygulama].

İki kimlik doğrulama akışı desteklenir: *istemcisi yönetilen* ve *sunucusu yönetilen* akış. Merhaba sağlayıcının web kimlik doğrulaması arabirimde alacağından hello akış sunucusu tarafından yönetilen hello Basit kimlik doğrulama deneyimi sağlar. sağlayıcıya özgü aygıta özgü SDK'ları üzerinde alacağından hello istemcisi yönetilen akış aygıta özgü özellikleri ile daha derin tümleştirme sağlar.

> [!NOTE]
> İstemci tarafından yönetilen bir akış üretim uygulamalarınızı kullanmanızı öneririz.

tooset kimlik doğrulaması kurma, bir veya daha fazla kimlik sağlayıcıları ile uygulamanızı kaydetmeniz gerekir.  Merhaba kimlik sağlayıcısı, bir istemci kimliği ve uygulamanız için bir istemci parolası oluşturur.  Bu değerler, arka uç tooenable Azure App Service kimlik doğrulama/yetkilendirme sonra ayarlanır.  Daha fazla bilgi için izleyin hello ayrıntılı yönergeler öğreticide [Ekle kimlik doğrulama tooyour uygulama].

Aşağıdaki konularda hello Bu bölümde ele alınmıştır:

* [Yönetilen istemci kimlik doğrulaması](#clientflow)
* [Yönetilen sunucu kimlik doğrulaması](#serverflow)
* [Önbelleğe alma hello kimlik doğrulama belirteci](#caching)

### <a name="clientflow"></a>Yönetilen istemci kimlik doğrulaması
Uygulamanızı bağımsız olarak hello kimlik sağlayıcısı başvurun ve ardından hello döndürülen belirteç ile arka oturum açma sırasında sağlayın. Bu istemci akışı tooprovide kullanıcılar ya da tooretrieve ek kullanıcı verilerini hello kimlik sağlayıcısı için çoklu oturum açma deneyimini etkinleştirir. Merhaba kimlik sağlayıcısı SDK daha yerel bir UX fikir sağlar ve ek özelleştirme için sağlar istemci akış kimlik doğrulaması tercih edilen toousing server akış aynıdır.

Akış olmayan istemci kimlik doğrulaması desenler izleyen Merhaba örnekler verilmiştir:

* [Active Directory kimlik doğrulama kitaplığı](#adal)
* [Facebook veya Google](#client-facebook)
* [Live SDK](#client-livesdk)

#### <a name="adal"></a>Kullanıcılar hello Active Directory kimlik doğrulama kitaplığı ile kimlik doğrulaması
Azure Active Directory kimlik doğrulaması kullanarak hello istemciden hello Active Directory Authentication Library (ADAL) tooinitiate kullanıcı kimlik doğrulamasını kullanabilirsiniz.

1. Aşağıdaki hello tarafından mobil uygulamanızın arka ucuna AAD oturum açma için yapılandırma [tooconfigure App Service nasıl Active Directory oturum açma için] Öğreticisi. Yerel istemci uygulaması kaydı emin toocomplete hello isteğe bağlı adım olun.
2. Visual Studio veya Xamarin Studio, projenizin açın ve bir başvuru toothe ekleyin `Microsoft.IdentityModel.CLients.ActiveDirectory` NuGet paketi. Arama yaparken, yayın öncesi sürümlerini içerir.
3. Kod tooyour uygulama aşağıdaki, kullanmakta olduğunuz toohello platform according hello ekleyin. Her, değişiklikleri izleyen hello olun:

   * Değiştir **INSERT yetkilisi burada** uygulamanızı sağlanan hello Kiracı hello adı. Https://login.microsoftonline.com/contoso.onmicrosoft.com biçiminde olmalıdır. Bu değer hello etki alanı sekmesinden hello Azure Active Directory'yi kopyalanabilir [Klasik Azure portalı].
   * Değiştir **Ekle-RESOURCE-kimliği-Buraya** , mobil uygulamanızın arka ucuna için hello istemci kimliği. Hello hello istemci kimliği elde edebilirsiniz **Gelişmiş** altında sekmesinde **Azure Active Directory ayarları** hello Portalı'nda.
   * Değiştir **Ekle-istemci-kimliği-Buraya** hello yerel istemci uygulamasından kopyaladığınız hello istemci kimliği.
   * Değiştir **Ekle-REDIRECT-URI-Buraya** sitenizin ile */.auth/login/done* hello HTTPS şeması kullanarak uç nokta. Bu değer çok benzer olmalıdır*https://contoso.azurewebsites.net/.auth/login/done*.

     Her platform için gereken hello kod aşağıdaki gibidir:

     **Windows:**

    ```
    private MobileServiceUser user;
    private async Task AuthenticateAsync()
    {

        string authority = "INSERT-AUTHORITY-HERE";
        string resourceId = "INSERT-RESOURCE-ID-HERE";
        string clientId = "INSERT-CLIENT-ID-HERE";
        string redirectUri = "INSERT-REDIRECT-URI-HERE";
        while (user == null)
        {
            string message;
            try
            {
                AuthenticationContext ac = new AuthenticationContext(authority);
                AuthenticationResult ar = await ac.AcquireTokenAsync(resourceId, clientId,
                    new Uri(redirectUri), new PlatformParameters(PromptBehavior.Auto, false) );
                JObject payload = new JObject();
                payload["access_token"] = ar.AccessToken;
                user = await App.MobileService.LoginAsync(
                    MobileServiceAuthenticationProvider.WindowsAzureActiveDirectory, payload);
                message = string.Format("You are now logged in - {0}", user.UserId);
            }
            catch (InvalidOperationException)
            {
                message = "You must log in. Login Required";
            }
            var dialog = new MessageDialog(message);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
    }
    ```

     **Xamarin.iOS**

    ```
    private MobileServiceUser user;
    private async Task AuthenticateAsync(UIViewController view)
    {

        string authority = "INSERT-AUTHORITY-HERE";
        string resourceId = "INSERT-RESOURCE-ID-HERE";
        string clientId = "INSERT-CLIENT-ID-HERE";
        string redirectUri = "INSERT-REDIRECT-URI-HERE";
        try
        {
            AuthenticationContext ac = new AuthenticationContext(authority);
            AuthenticationResult ar = await ac.AcquireTokenAsync(resourceId, clientId,
                new Uri(redirectUri), new PlatformParameters(view));
            JObject payload = new JObject();
            payload["access_token"] = ar.AccessToken;
            user = await client.LoginAsync(
                MobileServiceAuthenticationProvider.WindowsAzureActiveDirectory, payload);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine(@"ERROR - AUTHENTICATION FAILED {0}", ex.Message);
        }
    }
    ```

     **Xamarin.Android**

    ```
    private MobileServiceUser user;
    private async Task AuthenticateAsync()
    {

        string authority = "INSERT-AUTHORITY-HERE";
        string resourceId = "INSERT-RESOURCE-ID-HERE";
        string clientId = "INSERT-CLIENT-ID-HERE";
        string redirectUri = "INSERT-REDIRECT-URI-HERE";
        try
        {
            AuthenticationContext ac = new AuthenticationContext(authority);
            AuthenticationResult ar = await ac.AcquireTokenAsync(resourceId, clientId,
                new Uri(redirectUri), new PlatformParameters(this));
            JObject payload = new JObject();
            payload["access_token"] = ar.AccessToken;
            user = await client.LoginAsync(
                MobileServiceAuthenticationProvider.WindowsAzureActiveDirectory, payload);
        }
        catch (Exception ex)
        {
            AlertDialog.Builder builder = new AlertDialog.Builder(this);
            builder.SetMessage(ex.Message);
            builder.SetTitle("You must log in. Login Required");
            builder.Create().Show();
        }
    }
    protected override void OnActivityResult(int requestCode, Result resultCode, Intent data)
    {

        base.OnActivityResult(requestCode, resultCode, data);
        AuthenticationAgentContinuationHelper.SetAuthenticationAgentContinuationEventArgs(requestCode, resultCode, data);
    }
    ```

#### <a name="client-facebook"></a>Çoklu oturum Facebook veya Google uygulamasından bir belirteç kullanarak açma
Facebook veya Google için bu parçacığında gösterildiği gibi hello istemci akışı kullanabilirsiniz.

```
var token = new JObject();
// Replace access_token_value with actual value of your access token obtained
// using hello Facebook or Google SDK.
token.Add("access_token", "access_token_value");

private MobileServiceUser user;
private async Task AuthenticateAsync()
{
    while (user == null)
    {
        string message;
        try
        {
            // Change MobileServiceAuthenticationProvider.Facebook
            // tooMobileServiceAuthenticationProvider.Google if using Google auth.
            user = await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook, token);
            message = string.Format("You are now logged in - {0}", user.UserId);
        }
        catch (InvalidOperationException)
        {
            message = "You must log in. Login Required";
        }

        var dialog = new MessageDialog(message);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }
}
```

#### <a name="client-livesdk"></a>Microsoft Account kullanarak çoklu oturum açma Live SDK hello
tooauthenticate kullanıcılar, Microsoft hesabı Geliştirici Merkezi hello uygulamanızı kaydetmeniz gerekir. Kayıt ayrıntıları, mobil uygulama arka uçta yapılandırın. toocreate bir Microsoft hesabı kaydı ve tooyour mobil uygulama arka ucu bağlanın, tam hello adımları [kaydetmek, uygulama toouse bir Microsoft hesabı oturum açma]. Uygulamanızı Windows mağazası ve Windows Phone 8/Silverlight sürümüne sahipseniz, hello Windows mağazası sürümü ilk kaydedin.

Merhaba aşağıdaki kod Live SDK'sını kullanarak kimliğini doğrular ve belirteç toosign tooyour mobil uygulama arka ucuna döndürülen hello kullanır.

```
private LiveConnectSession session;
    //private static string clientId = "<microsoft-account-client-id>";
private async System.Threading.Tasks.Task AuthenticateAsync()
{

    // Get hello URL hello Mobile App backend.
    var serviceUrl = App.MobileService.ApplicationUri.AbsoluteUri;

    // Create hello authentication client for Windows Store using hello service URL.
    LiveAuthClient liveIdClient = new LiveAuthClient(serviceUrl);
    //// Create hello authentication client for Windows Phone using hello client ID of hello registration.
    //LiveAuthClient liveIdClient = new LiveAuthClient(clientId);

    while (session == null)
    {
        // Request hello authentication token from hello Live authentication service.
        // hello wl.basic scope should always be requested.  Other scopes can be added
        LiveLoginResult result = await liveIdClient.LoginAsync(new string[] { "wl.basic" });
        if (result.Status == LiveConnectSessionStatus.Connected)
        {
            session = result.Session;

            // Get information about hello logged-in user.
            LiveConnectClient client = new LiveConnectClient(session);
            LiveOperationResult meResult = await client.GetAsync("me");

            // Use hello Microsoft account auth token toosign in tooApp Service.
            MobileServiceUser loginResult = await App.MobileService
                .LoginWithMicrosoftAccountAsync(result.Session.AuthenticationToken);

            // Display a personalized sign-in greeting.
            string title = string.Format("Welcome {0}!", meResult.Result["first_name"]);
            var message = string.Format("You are now logged in - {0}", loginResult.UserId);
            var dialog = new MessageDialog(message, title);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
        else
        {
            session = null;
            var dialog = new MessageDialog("You must log in.", "Login Required");
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
    }
}
```

Daha fazla bilgi için bkz: Merhaba [Windows Live SDK] belgeleri.

### <a name="serverflow"></a>Yönetilen sunucu kimlik doğrulaması
Kimlik sağlayıcınızı kaydettiğinizde, hello çağrısı [LoginAsync] hello [MobileServiceClient] hello ile yöntemi [MobileServiceAuthenticationProvider] sağlayıcınız değeri. Örneğin, hello aşağıdaki kod bir sunucu akış oturum açma Facebook kullanarak başlatır.

```
private MobileServiceUser user;
private async System.Threading.Tasks.Task Authenticate()
{
    while (user == null)
    {
        string message;
        try
        {
            user = await client
                .LoginAsync(MobileServiceAuthenticationProvider.Facebook);
            message =
                string.Format("You are now logged in - {0}", user.UserId);
        }
        catch (InvalidOperationException)
        {
            message = "You must log in. Login Required";
        }

        var dialog = new MessageDialog(message);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }
}
```

Facebook dışında bir kimlik sağlayıcısı kullanıyorsanız, hello değerini değiştirme [MobileServiceAuthenticationProvider] sağlayıcınız için toohello değeri.

Bir sunucu akışında hello oturum açma sayfası hello seçilen sağlayıcıya görüntüleyerek Azure App Service hello OAuth kimlik doğrulaması akışı yönetir.  Bir kez hello kimlik sağlayıcısı döndürür, Azure App Service, bir uygulama hizmeti kimlik doğrulama belirteci oluşturur. Merhaba [LoginAsync] yöntemi döndürür bir [MobileServiceUser], her iki hello sağlayan [UserID] Merhaba kimliği doğrulanmış kullanıcı ve hello [ MobileServiceAuthenticationToken], JSON web Token (JWT). Bu belirteç önbelleğe alınabilir süresi sona erene kadar yeniden kullanılabilir. Daha fazla bilgi için bkz: [önbelleğe alma hello kimlik doğrulama belirteci](#caching).

### <a name="caching"></a>Önbelleğe alma hello kimlik doğrulama belirteci
Bazı durumlarda, hello çağrısı toohello oturum açma yöntemi hello kimlik doğrulama belirteci hello sağlayıcısından depolayarak hello ilk başarılı kimlik doğrulamasından sonra önlenebilir.  Windows mağazası ve UWP uygulamalar kullanabilir [PasswordVault] toocache gibi simge bir başarılı oturum açma işleminden sonra geçerli kimlik doğrulama:

```
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook);

PasswordVault vault = new PasswordVault();
vault.Add(new PasswordCredential("Facebook", client.currentUser.UserId,
    client.currentUser.MobileServiceAuthenticationToken));
```

Hello UserID değeri hello hello kimlik bilgileri kullanıcı adı depolanır ve parola hello depolanan hello hello belirtecidir. Sonraki start-ups üzerinde hello denetleyebilirsiniz **PasswordVault** önbelleğe alınmış kimlik bilgileri. bulunan ve aksi durumda tooauthenticate hello arka ucu ile yeniden deneme hello aşağıdaki örnekte önbelleğe alınmış kimlik bilgilerini kullanır:

```
// Try tooretrieve stored credentials.
var creds = vault.FindAllByResource("Facebook").FirstOrDefault();
if (creds != null)
{
    // Create hello current user from hello stored credentials.
    client.currentUser = new MobileServiceUser(creds.UserName);
    client.currentUser.MobileServiceAuthenticationToken =
        vault.Retrieve("Facebook", creds.UserName).Password;
}
else
{
    // Regular login flow and cache hello token as shown above.
}
```

Bir kullanıcı oturum açtığınızda, hello depolanan kimlik bilgileri, aşağıdaki gibi de kaldırmanız gerekir:

```
client.Logout();
vault.Remove(vault.Retrieve("Facebook", client.currentUser.UserId));
```

Xamarin uygulamaları kullanma hello [Xamarin.Auth] API'leri toosecurely deposu kimlik bir **hesap** nesnesi. Merhaba bu API'leri kullanarak bir örnek için bkz: [AuthStore.cs] hello kod dosyasında [örnek paylaşımı ContosoMoments fotoğraf](https://github.com/azure-appservice-samples/ContosoMoments).

Yönetilen istemci kimlik doğrulaması kullandığınızda, Facebook veya Twitter'da gibi sağlayıcınızdan elde hello erişim belirteci önbelleğe alabilir. Bu belirteç sağlanan toorequest yeni bir kimlik doğrulama belirteci hello arka aşağıdaki gibi olabilir:

```
var token = new JObject();
// Replace <your_access_token_value> with actual value of your access token
token.Add("access_token", "<your_access_token_value>");

// Authenticate using hello access token.
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook, token);
```

## <a name="pushnotifications"></a>Anında iletme bildirimleri
Merhaba aşağıdaki konular anında iletme bildirimleri kapsar:

* [Anında iletme bildirimleri için kaydolun](#register-for-push)
* [Windows mağazası paket SID'si alın](#package-sid)
* [Platformlar arası şablonları ile kaydetme](#register-xplat)

### <a name="register-for-push"></a>Nasıl yapılır: anında iletme bildirimleri için kaydolun
Merhaba Mobile Apps istemci tooregister Azure Notification Hubs ile anında iletme bildirimleri için etkinleştirir. Kaydederken, hello platforma özgü elde bir tanıtıcı elde anında bildirim hizmeti (PNS). Hello kayıt oluşturduğunuzda, ardından tüm etiketlerin yanı sıra bu değer sağlayın. Merhaba aşağıdaki kodu Windows uygulamanız anında iletme bildirimleri için hello Windows bildirim Hizmeti'ni (WNS) ile kaydeder:

```
private async void InitNotificationsAsync()
{
    // Request a push notification channel.
    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // Register for notifications using hello new channel.
    await MobileService.GetPush().RegisterNativeAsync(channel.Uri, null);
}
```

TooWNS Ftp'den sonra yapmanız gerekenler [Windows mağazası paket SID'si elde](#package-sid).  Windows uygulamaları hakkında daha fazla bilgi için şablon kayıtlar için tooregister nasıl görürüm dahil olmak üzere [Ekle anında iletme bildirimleri tooyour uygulama].

Etiketler hello istemciden isteyen desteklenmiyor.  Etiket istekleri sessizce kaydından bırakılır.
Cihazınızı etiketlerle tooregister istiyorsanız, sizin adınıza hello bildirim hub'ları API tooperform hello kayıt kullanan bir özel API oluşturun.  [Merhaba özel API çağrısı](#customapi) hello yerine `RegisterNativeAsync()` yöntemi.

### <a name="package-sid"></a>Nasıl yapılır: Windows mağazası paket SID'si alın
Bir paket SID'si Windows mağazası uygulamalarında anında iletme bildirimleri etkinleştirmek için gereklidir.  tooreceive bir paket SID'si, uygulamanızı Windows mağazası hello ile kaydedin.

tooobtain bu değer:

1. Visual Studio Çözüm Gezgini'nde hello Windows mağazası uygulama projesine sağ tıklayın, tıklatın **deposu** > **uygulamayı hello mağaza ile ilişkilendir...** .
2. Başlangıç Sihirbazı'nda tıklatın **sonraki**, Microsoft hesabınızla oturum açın, uygulamanız için bir ad yazın **yeni bir uygulama adı yedek**, ardından **ayırma**.
3. Merhaba uygulama kaydı başarıyla oluşturuldu, select hello uygulama adı sonra tıklatın **sonraki**ve ardından **ilişkilendirmek**.
4. İçinde toohello oturum [Windows Geliştirme Merkezi] Microsoft Account kullanarak. Altında **uygulamalarım**, oluşturduğunuz hello uygulama kayıt'a tıklayın.
5. Tıklatın **Uygulama Yönetimi** > **uygulama kimliği**ve ardından toofind kaydırın, **paket SID'si**.

Merhaba paket SID'si birçok kullanımı, bir URI olarak toouse gerekir; bu durumda kabul *ms-app: / /* hello düzeni olarak. Paketinizin bir önek olarak bu değer birleştirerek biçimlendirilmiş SID hello sürümünü not edin.

Xamarin uygulamaları bazı ek kod toobe mümkün tooregister hello iOS veya Android platformları üzerinde çalışan uygulama gerekiyor. Daha fazla bilgi için platformunuz hello konuya bakın:

* [Xamarin.Android](app-service-mobile-xamarin-android-get-started-push.md#add-push)
* [Xamarin.iOS](app-service-mobile-xamarin-ios-get-started-push.md#add-push-notifications-to-your-app)

### <a name="register-xplat"></a>Nasıl yapılır: yazmaç anında iletme şablonları toosend platformlar arası bildirimleri
tooregister şablonlarını kullanma hello `RegisterAsync()` şekilde hello şablonlarıyla yöntemi:

```
JObject templates = myTemplates();
MobileService.GetPush().RegisterAsync(channel.Uri, templates);
```

Şablonlarınızı olmalıdır `JObject` türleri ve birden fazla şablon içinde JSON biçimini izleyen hello içerebilir:

```
public JObject myTemplates()
{
    // single template for Windows Notification Service toast
    var template = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(message)</text></binding></visual></toast>";

    var templates = new JObject
    {
        ["generic-message"] = new JObject
        {
            ["body"] = template,
            ["headers"] = new JObject
            {
                ["X-WNS-Type"] = "wns/toast"
            },
            ["tags"] = new JArray()
        },
        ["more-templates"] = new JObject {...}
    };
    return templates;
}
```

Merhaba yöntemi **RegisterAsync()** de ikincil döşeme kabul eder:

```
MobileService.GetPush().RegisterAsync(string channelUri, JObject templates, JObject secondaryTiles);
```

Tüm etiketleri hemen güvenlik için kayıt sırasında kaldırılır. tooadd tooinstallations ya da şablon yüklemeleri içinde etiketleri, [hello .NET arka uç sunucusu SDK çalışmak için Azure Mobile Apps] bakın.

kayıtlı bu şablonları kullanılarak toosend bildirimleri başvuran toohello [bildirim hub'ları API'leri].

## <a name="misc"></a>Çeşitli konuları
### <a name="errors"></a>Nasıl yapılır: hata işleme
Merhaba arka ucuna bir hata ortaya çıktığında hello istemci SDK başlatır bir `MobileServiceInvalidOperationException`.  Aşağıdaki örnekte gösterildiği nasıl toohandle hello arka ucu tarafından döndürülen bir özel durum:

```
private async void InsertTodoItem(TodoItem todoItem)
{
    // This code inserts a new TodoItem into hello database. When hello operation completes
    // and App Service has assigned an Id, hello item is added toohello CollectionView
    try
    {
        await todoTable.InsertAsync(todoItem);
        items.Add(todoItem);
    }
    catch (MobileServiceInvalidOperationException e)
    {
        // Handle error
    }
}
```

Başka bir örnek hata koşulları postalarla hello bulunabilir [Mobile Apps dosyaları örnek]. [LoggingHandler] örnek toohello arka uç yapılan işleyici toolog hello istekleri günlüğe kaydetme temsilci sağlar.

### <a name="headers"></a>Nasıl yapılır: özelleştirme istek üstbilgileri
toosupport belirli uygulama senaryonuz hello mobil uygulama arka ucu ile toocustomize iletişim gerekebilir. Örneğin, bir özel üst bilgi tooevery giden istek tooadd istediğiniz veya bile yanıtları durum kodları değiştirin. Özel bir kullanabilirsiniz [DelegatingHandler], aşağıdaki örneğine hello olarak:

```
public async Task CallClientWithHandler()
{
    MobileServiceClient client = new MobileServiceClient("AppUrl", new MyHandler());
    IMobileServiceTable<TodoItem> todoTable = client.GetTable<TodoItem>();
    var newItem = new TodoItem { Text = "Hello world", Complete = false };
    await todoTable.InsertAsync(newItem);
}

public class MyHandler : DelegatingHandler
{
    protected override async Task<HttpResponseMessage>
        SendAsync(HttpRequestMessage request, CancellationToken cancellationToken)
    {
        // Change hello request-side here based on hello HttpRequestMessage
        request.Headers.Add("x-my-header", "my value");

        // Do hello request
        var response = await base.SendAsync(request, cancellationToken);

        // Change hello response-side here based on hello HttpResponseMessage

        // Return hello modified response
        return response;
    }
}
```


<!-- Anchors. -->


<!-- Images. -->

<!-- URLs. -->
[1]: app-service-mobile-windows-store-dotnet-get-started.md
[2]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[3]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[4]: https://msdn.microsoft.com/en-us/library/azure/mt419521(v=azure.10).aspx
[5]: https://github.com/Azure-Samples
[6]: http://www.newtonsoft.com/json/help/html/Properties_T_Newtonsoft_Json_JsonPropertyAttribute.htm
[7]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#define-table-controller
[8]: app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations
[9]: https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/
[10]: http://www.symbolsource.org/
[11]: http://www.symbolsource.org/Public/Wiki/Using
[12]: https://msdn.microsoft.com/en-us/library/azure/microsoft.windowsazure.mobileservices.mobileserviceclient(v=azure.10).aspx

[Ekle kimlik doğrulama tooyour uygulama]: app-service-mobile-windows-store-dotnet-get-started-users.md
[çevrimdışı veri eşitlemeye Azure Mobile Apps içinde]: app-service-mobile-offline-data-sync.md
[Ekle anında iletme bildirimleri tooyour uygulama]: app-service-mobile-windows-store-dotnet-get-started-push.md
[kaydetmek, uygulama toouse bir Microsoft hesabı oturum açma]: app-service-mobile-how-to-configure-microsoft-authentication.md
[tooconfigure App Service nasıl Active Directory oturum açma için]: app-service-mobile-how-to-configure-active-directory-authentication.md

<!-- Microsoft URLs. -->
[MobileServiceCollection]: https://msdn.microsoft.com/en-us/library/azure/dn250636(v=azure.10).aspx
[MobileServiceIncrementalLoadingCollection]: https://msdn.microsoft.com/en-us/library/azure/dn268408(v=azure.10).aspx
[MobileServiceAuthenticationProvider]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceauthenticationprovider(v=azure.10).aspx
[MobileServiceUser]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser(v=azure.10).aspx
[ MobileServiceAuthenticationToken]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.mobileserviceauthenticationtoken(v=azure.10).aspx
[GetTable]: https://msdn.microsoft.com/en-us/library/azure/jj554275(v=azure.10).aspx
[başvuru tooan türü belirsiz bir tablo oluşturur]: https://msdn.microsoft.com/en-us/library/azure/jj554278(v=azure.10).aspx
[DeleteAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296407(v=azure.10).aspx
[IncludeTotalCount]: https://msdn.microsoft.com/en-us/library/azure/dn250560(v=azure.10).aspx
[InsertAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296400(v=azure.10).aspx
[InvokeApiAsync]: https://msdn.microsoft.com/en-us/library/azure/dn268343(v=azure.10).aspx
[LoginAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296411(v=azure.10).aspx
[LookupAsync]: https://msdn.microsoft.com/en-us/library/azure/jj871654(v=azure.10).aspx
[OrderBy]: https://msdn.microsoft.com/en-us/library/azure/dn250572(v=azure.10).aspx
[OrderByDescending]: https://msdn.microsoft.com/en-us/library/azure/dn250568(v=azure.10).aspx
[ReadAsync]: https://msdn.microsoft.com/en-us/library/azure/mt691741(v=azure.10).aspx
[ele]: https://msdn.microsoft.com/en-us/library/azure/dn250574(v=azure.10).aspx
[seçin]: https://msdn.microsoft.com/en-us/library/azure/dn250569(v=azure.10).aspx
[atla]: https://msdn.microsoft.com/en-us/library/azure/dn250573(v=azure.10).aspx
[UpdateAsync]: https://msdn.microsoft.com/en-us/library/azure/dn250536.(v=azure.10)aspx
[Kullanıcı Kimliği]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.userid(v=azure.10).aspx
[burada]: https://msdn.microsoft.com/en-us/library/azure/dn250579(v=azure.10).aspx
[Azure portal]: https://portal.azure.com/
[Klasik Azure portalı]: https://manage.windowsazure.com/
[EnableQueryAttribute]: https://msdn.microsoft.com/library/system.web.http.odata.enablequeryattribute.aspx
[Guid.NewGuid]: https://msdn.microsoft.com/en-us/library/system.guid.newguid(v=vs.110).aspx
[ISupportIncrementalLoading]: http://msdn.microsoft.com/library/windows/apps/Hh701916.aspx
[Windows Geliştirme Merkezi]: https://dev.windows.com/en-us/overview
[DelegatingHandler]: https://msdn.microsoft.com/library/system.net.http.delegatinghandler(v=vs.110).aspx
[Windows Live SDK]: https://msdn.microsoft.com/en-us/library/bb404787.aspx
[PasswordVault]: http://msdn.microsoft.com/library/windows/apps/windows.security.credentials.passwordvault.aspx
[ProtectedData]: http://msdn.microsoft.com/library/system.security.cryptography.protecteddata%28VS.95%29.aspx
[bildirim hub'ları API'leri]: https://msdn.microsoft.com/library/azure/dn495101.aspx
[Mobile Apps dosyaları örnek]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files
[LoggingHandler]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files/blob/master/src/client/MobileAppsFilesSample/Helpers/LoggingHandler.cs#L63

<!-- External URLs -->
[OData v3 belgelerine]: http://www.odata.org/documentation/odata-version-3-0/
[Fiddler]: http://www.telerik.com/fiddler
[Json.NET]: http://www.newtonsoft.com/json
[Xamarin.Auth]: https://components.xamarin.com/view/xamarin.auth/
[AuthStore.cs]: https://github.com/azure-appservice-samples/ContosoMoments
[ContosoMoments photo sharing sample]: https://github.com/azure-appservice-samples/ContosoMoments
