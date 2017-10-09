---
title: "aaaHow tooUse iOS için Azure Mobile Apps SDK'sı"
description: "Nasıl tooUse iOS için Azure Mobile Apps SDK'sı"
services: app-service\mobile
documentationcenter: ios
author: ysxu
manager: yochayk
editor: 
ms.assetid: 4e8e45df-c36a-4a60-9ad4-393ec10b7eb9
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/01/2016
ms.author: yuaxu
ms.openlocfilehash: fa299ab3f152bad12d821832fa9fb5495d1fa296
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-ios-client-library-for-azure-mobile-apps"></a><span data-ttu-id="0283f-103">Nasıl tooUse iOS için Azure Mobile Apps istemci kitaplığı</span><span class="sxs-lookup"><span data-stu-id="0283f-103">How tooUse iOS Client Library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="0283f-104">Bu kılavuz hello son kullanarak tooperform genel senaryolar öğretilmektedir [Azure Mobile Apps iOS SDK'sı][1].</span><span class="sxs-lookup"><span data-stu-id="0283f-104">This guide teaches you tooperform common scenarios using hello latest [Azure Mobile Apps iOS SDK][1].</span></span> <span data-ttu-id="0283f-105">Yeni tooAzure mobil uygulamalar varsa, ilk tamamlamak [Azure Mobile Apps Hızlı Başlangıç] toocreate bir arka uç bir tablo oluşturun ve önceden derlenmiş iOS Xcode projenizi indirin.</span><span class="sxs-lookup"><span data-stu-id="0283f-105">If you are new tooAzure Mobile Apps, first complete [Azure Mobile Apps Quick Start] toocreate a backend, create a table, and download a pre-built iOS Xcode project.</span></span> <span data-ttu-id="0283f-106">Bu kılavuzda, hello istemci-tarafı iOS SDK'sı odaklanın.</span><span class="sxs-lookup"><span data-stu-id="0283f-106">In this guide, we focus on hello client-side iOS SDK.</span></span> <span data-ttu-id="0283f-107">toolearn hakkında daha fazla bilgi için hello arka uç sunucu tarafı SDK Merhaba, hello Server SDK HOWTOs bakın.</span><span class="sxs-lookup"><span data-stu-id="0283f-107">toolearn more about hello server-side SDK for hello backend, see hello Server SDK HOWTOs.</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="0283f-108">Başvuru belgeleri</span><span class="sxs-lookup"><span data-stu-id="0283f-108">Reference documentation</span></span>
<span data-ttu-id="0283f-109">Merhaba başvuru belgeleri hello iOS istemci SDK'sı için aşağıda bulunur: [Azure Mobile Apps iOS istemci başvurusu][2].</span><span class="sxs-lookup"><span data-stu-id="0283f-109">hello reference documentation for hello iOS client SDK is located here: [Azure Mobile Apps iOS Client Reference][2].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="0283f-110">Desteklenen platformlar</span><span class="sxs-lookup"><span data-stu-id="0283f-110">Supported Platforms</span></span>
<span data-ttu-id="0283f-111">Merhaba iOS SDK'sı iOS 8.0 veya sonraki sürümleri için Objective-C projeleri, Swift 2.2 projeler ve Swift 2.3 projeleri destekler.</span><span class="sxs-lookup"><span data-stu-id="0283f-111">hello iOS SDK supports Objective-C projects, Swift 2.2 projects, and Swift 2.3 projects for iOS versions 8.0 or later.</span></span>

<span data-ttu-id="0283f-112">Merhaba "sunucu akış" kimlik doğrulaması için kullanıcı Arabirimi sunulan hello bir Web görünümü kullanır.</span><span class="sxs-lookup"><span data-stu-id="0283f-112">hello "server-flow" authentication uses a WebView for hello presented UI.</span></span>  <span data-ttu-id="0283f-113">Kimlik doğrulama başka bir yöntem gereklidir hello cihaz mümkün toopresent WebView UI değilse hello ürün dış hello kapsamını olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="0283f-113">If hello device is not able toopresent a WebView UI, then another method of authentication is required that is outside hello scope of hello product.</span></span>  
<span data-ttu-id="0283f-114">Bu SDK böylece Gözcü türü veya benzer şekilde kısıtlı aygıtlar için uygun değil.</span><span class="sxs-lookup"><span data-stu-id="0283f-114">This SDK is thus not suitable for Watch-type or similarly restricted devices.</span></span>

## <span data-ttu-id="0283f-115"><a name="Setup"></a>Kurulum ve Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="0283f-115"><a name="Setup"></a>Setup and Prerequisites</span></span>
<span data-ttu-id="0283f-116">Bu kılavuz, bir tablo ile bir arka uç oluşturduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="0283f-116">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="0283f-117">Bu kılavuz, o hello aynı şeması hello tablolar olarak bu öğreticiler tablolu varsayar.</span><span class="sxs-lookup"><span data-stu-id="0283f-117">This guide assumes that hello table has the same schema as hello tables in those tutorials.</span></span> <span data-ttu-id="0283f-118">Bu kılavuz Ayrıca, kodunuzda, başvuru varsayar `MicrosoftAzureMobile.framework` ve içeri aktarma `MicrosoftAzureMobile/MicrosoftAzureMobile.h`.</span><span class="sxs-lookup"><span data-stu-id="0283f-118">This guide also assumes that in your code, you reference `MicrosoftAzureMobile.framework` and import `MicrosoftAzureMobile/MicrosoftAzureMobile.h`.</span></span>

## <span data-ttu-id="0283f-119"><a name="create-client"></a>Nasıl yapılır: istemci oluşturma</span><span class="sxs-lookup"><span data-stu-id="0283f-119"><a name="create-client"></a>How to: Create Client</span></span>
<span data-ttu-id="0283f-120">tooaccess projenizdeki Azure Mobile Apps arka oluşturma bir `MSClient`.</span><span class="sxs-lookup"><span data-stu-id="0283f-120">tooaccess an Azure Mobile Apps backend in your project, create an `MSClient`.</span></span> <span data-ttu-id="0283f-121">Değiştir `AppUrl` hello uygulama URL'si ile.</span><span class="sxs-lookup"><span data-stu-id="0283f-121">Replace `AppUrl` with hello app URL.</span></span> <span data-ttu-id="0283f-122">Bırakabilir `gatewayURLString` ve `applicationKey` boş.</span><span class="sxs-lookup"><span data-stu-id="0283f-122">You may leave `gatewayURLString` and `applicationKey` empty.</span></span> <span data-ttu-id="0283f-123">Kimlik doğrulaması için bir ağ geçidi ayarladıysanız, doldurmak `gatewayURLString` hello ağ geçidi URL'si.</span><span class="sxs-lookup"><span data-stu-id="0283f-123">If you set up a gateway for authentication, populate `gatewayURLString` with hello gateway URL.</span></span>

<span data-ttu-id="0283f-124">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="0283f-124">**Objective-C**:</span></span>

```
MSClient *client = [MSClient clientWithApplicationURLString:@"AppUrl"];
```

<span data-ttu-id="0283f-125">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="0283f-125">**Swift**:</span></span>

```
let client = MSClient(applicationURLString: "AppUrl")
```


## <span data-ttu-id="0283f-126"><a name="table-reference"></a>Nasıl yapılır: Tablo başvurusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="0283f-126"><a name="table-reference"></a>How to: Create Table Reference</span></span>
<span data-ttu-id="0283f-127">tooaccess veya güncelleştirme veriler, bir başvuru toohello arka uç tablosu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0283f-127">tooaccess or update data, create a reference toohello backend table.</span></span> <span data-ttu-id="0283f-128">Değiştir `TodoItem` tablonuz hello adı</span><span class="sxs-lookup"><span data-stu-id="0283f-128">Replace `TodoItem` with hello name of your table</span></span>

<span data-ttu-id="0283f-129">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="0283f-129">**Objective-C**:</span></span>

```
MSTable *table = [client tableWithName:@"TodoItem"];
```

<span data-ttu-id="0283f-130">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="0283f-130">**Swift**:</span></span>

```
let table = client.tableWithName("TodoItem")
```


## <span data-ttu-id="0283f-131"><a name="querying"></a>Nasıl yapılır: veri sorgulama</span><span class="sxs-lookup"><span data-stu-id="0283f-131"><a name="querying"></a>How to: Query Data</span></span>
<span data-ttu-id="0283f-132">toocreate bir veritabanı sorgusu sorgu hello `MSTable` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="0283f-132">toocreate a database query, query hello `MSTable` object.</span></span> <span data-ttu-id="0283f-133">Merhaba aşağıdaki sorgu tüm hello öğeleri alır `TodoItem` ve günlükleri hello her öğenin metni.</span><span class="sxs-lookup"><span data-stu-id="0283f-133">hello following query gets all hello items in `TodoItem` and logs hello text of each item.</span></span>

<span data-ttu-id="0283f-134">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="0283f-134">**Objective-C**:</span></span>

```
[table readWithCompletion:^(MSQueryResult *result, NSError *error) {
        if(error) { // error is nil if no error occured
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) { // items is NSArray of records that match query
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

<span data-ttu-id="0283f-135">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="0283f-135">**Swift**:</span></span>

```
table.readWithCompletion { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```

## <span data-ttu-id="0283f-136"><a name="filtering"></a>Nasıl yapılır: Filtre veri döndürdü</span><span class="sxs-lookup"><span data-stu-id="0283f-136"><a name="filtering"></a>How to: Filter Returned Data</span></span>
<span data-ttu-id="0283f-137">toofilter sonuçları, birçok kullanılabilir seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="0283f-137">toofilter results, there are many available options.</span></span>

<span data-ttu-id="0283f-138">bir koşul kullanmak kullanarak toofilter bir `NSPredicate` ve `readWithPredicate`.</span><span class="sxs-lookup"><span data-stu-id="0283f-138">toofilter using a predicate, use an `NSPredicate` and `readWithPredicate`.</span></span> <span data-ttu-id="0283f-139">döndürülen veri toofind yalnızca tamamlanmamış Yapılacaklar öğelerini Hello aşağıdaki filtreler.</span><span class="sxs-lookup"><span data-stu-id="0283f-139">hello following filters returned data toofind only incomplete Todo items.</span></span>

<span data-ttu-id="0283f-140">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="0283f-140">**Objective-C**:</span></span>

```
// Create a predicate that finds items where complete is false
NSPredicate * predicate = [NSPredicate predicateWithFormat:@"complete == NO"];
// Query hello TodoItem table
[table readWithPredicate:predicate completion:^(MSQueryResult *result, NSError *error) {
        if(error) {
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) {
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

<span data-ttu-id="0283f-141">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="0283f-141">**Swift**:</span></span>

```
// Create a predicate that finds items where complete is false
let predicate =  NSPredicate(format: "complete == NO")
// Query hello TodoItem table
table.readWithPredicate(predicate) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```

## <span data-ttu-id="0283f-142"><a name="query-object"></a>Nasıl yapılır: MSQuery kullanın</span><span class="sxs-lookup"><span data-stu-id="0283f-142"><a name="query-object"></a>How to: Use MSQuery</span></span>
<span data-ttu-id="0283f-143">(sıralama dahil ve disk belleği), karmaşık bir sorgu oluşturmak tooperform bir `MSQuery` nesnesi, doğrudan veya bir koşulu kullanarak:</span><span class="sxs-lookup"><span data-stu-id="0283f-143">tooperform a complex query (including sorting and paging), create an `MSQuery` object, directly or by using a predicate:</span></span>

<span data-ttu-id="0283f-144">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="0283f-144">**Objective-C**:</span></span>

```
MSQuery *query = [table query];
MSQuery *query = [table queryWithPredicate: [NSPredicate predicateWithFormat:@"complete == NO"]];
```

<span data-ttu-id="0283f-145">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="0283f-145">**Swift**:</span></span>

```
let query = table.query()
let query = table.queryWithPredicate(NSPredicate(format: "complete == NO"))
```

<span data-ttu-id="0283f-146">`MSQuery`birkaç sorgu davranışları denetlemenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="0283f-146">`MSQuery` lets you control several query behaviors.</span></span>

* <span data-ttu-id="0283f-147">Sonuçları sırasını belirtin</span><span class="sxs-lookup"><span data-stu-id="0283f-147">Specify order of results</span></span>
* <span data-ttu-id="0283f-148">Hangi alanların tooreturn sınırla</span><span class="sxs-lookup"><span data-stu-id="0283f-148">Limit which fields tooreturn</span></span>
* <span data-ttu-id="0283f-149">Kaç tane tooreturn kayıtları sınırla</span><span class="sxs-lookup"><span data-stu-id="0283f-149">Limit how many records tooreturn</span></span>
* <span data-ttu-id="0283f-150">Yanıtta toplam sayısı belirtin</span><span class="sxs-lookup"><span data-stu-id="0283f-150">Specify total count in response</span></span>
* <span data-ttu-id="0283f-151">İstekte özel sorgu dizesi parametreleri belirtin</span><span class="sxs-lookup"><span data-stu-id="0283f-151">Specify custom query string parameters in request</span></span>
* <span data-ttu-id="0283f-152">Ek işlevler Uygula</span><span class="sxs-lookup"><span data-stu-id="0283f-152">Apply additional functions</span></span>

<span data-ttu-id="0283f-153">Yürütme bir `MSQuery` çağırarak sorgu `readWithCompletion` hello nesne üzerinde.</span><span class="sxs-lookup"><span data-stu-id="0283f-153">Execute an `MSQuery` query by calling `readWithCompletion` on hello object.</span></span>

## <span data-ttu-id="0283f-154"><a name="sorting"></a>Nasıl yapılır: MSQuery ile verileri sıralama</span><span class="sxs-lookup"><span data-stu-id="0283f-154"><a name="sorting"></a>How to: Sort Data with MSQuery</span></span>
<span data-ttu-id="0283f-155">toosort sonuçları bir örneğe bakalım.</span><span class="sxs-lookup"><span data-stu-id="0283f-155">toosort results, let's look at an example.</span></span> <span data-ttu-id="0283f-156">toosort alan 'text' artan sonra 'Tamamlandı' azalan, çağırma `MSQuery` sözlüğüdür:</span><span class="sxs-lookup"><span data-stu-id="0283f-156">toosort by field 'text' ascending, then by 'complete' descending, invoke `MSQuery` like so:</span></span>

<span data-ttu-id="0283f-157">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="0283f-157">**Objective-C**:</span></span>

```
[query orderByAscending:@"text"];
[query orderByDescending:@"complete"];
[query readWithCompletion:^(MSQueryResult *result, NSError *error) {
        if(error) {
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) {
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

<span data-ttu-id="0283f-158">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="0283f-158">**Swift**:</span></span>

```
query.orderByAscending("text")
query.orderByDescending("complete")
query.readWithCompletion { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```


## <span data-ttu-id="0283f-159"><a name="selecting"></a><a name="parameters"></a>Nasıl yapılır: alanları sınırlayabilir ve sorgu dizesi parametreleri MSQuery ile genişletin</span><span class="sxs-lookup"><span data-stu-id="0283f-159"><a name="selecting"></a><a name="parameters"></a>How to: Limit Fields and Expand Query String Parameters with MSQuery</span></span>
<span data-ttu-id="0283f-160">bir sorguda döndürülen toolimit alanları toobe hello hello alanların hello adlarını belirtin **selectFields** özelliği.</span><span class="sxs-lookup"><span data-stu-id="0283f-160">toolimit fields toobe returned in a query, specify hello names of hello fields in hello **selectFields** property.</span></span> <span data-ttu-id="0283f-161">Bu örnek yalnızca hello metin ve tamamlanan alanları döndürür:</span><span class="sxs-lookup"><span data-stu-id="0283f-161">This example returns only hello text and completed fields:</span></span>

<span data-ttu-id="0283f-162">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="0283f-162">**Objective-C**:</span></span>

```
query.selectFields = @[@"text", @"complete"];
```

<span data-ttu-id="0283f-163">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="0283f-163">**Swift**:</span></span>

```
query.selectFields = ["text", "complete"]
```

<span data-ttu-id="0283f-164">tooinclude ek sorgu dizesi parametreleri hello Server'daki (örneğin, özel bir sunucu tarafı komut dosyası bunları kullandığından) isteği, doldurmak `query.parameters` sözlüğüdür:</span><span class="sxs-lookup"><span data-stu-id="0283f-164">tooinclude additional query string parameters in hello server request (for example, because a custom server-side script uses them), populate `query.parameters` like so:</span></span>

<span data-ttu-id="0283f-165">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="0283f-165">**Objective-C**:</span></span>

```
query.parameters = @{
    @"myKey1" : @"value1",
    @"myKey2" : @"value2",
};
```

<span data-ttu-id="0283f-166">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="0283f-166">**Swift**:</span></span>

```
query.parameters = ["myKey1": "value1", "myKey2": "value2"]
```

## <span data-ttu-id="0283f-167"><a name="paging"></a>Nasıl yapılır: sayfa boyutu yapılandırın</span><span class="sxs-lookup"><span data-stu-id="0283f-167"><a name="paging"></a>How to: Configure Page Size</span></span>
<span data-ttu-id="0283f-168">Azure Mobile Apps ile Merhaba sayfa boyutu denetimleri hello arka uç tablolar aynı anda çekilen kayıt sayısı hello.</span><span class="sxs-lookup"><span data-stu-id="0283f-168">With Azure Mobile Apps, hello page size controls hello number of records that are pulled at a time from hello backend tables.</span></span> <span data-ttu-id="0283f-169">Bir arama çok`pull` veri hiçbir daha fazla kayıt toopull kadar bu sayfa boyutuna göre verileri, ardından toplu.</span><span class="sxs-lookup"><span data-stu-id="0283f-169">A call too`pull` data would then batch up data, based on this page size, until there are no more records toopull.</span></span>

<span data-ttu-id="0283f-170">Sayfa boyutu kullanarak olası tooconfigure olan **MSPullSettings** aşağıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="0283f-170">It's possible tooconfigure a page size using **MSPullSettings** as shown below.</span></span> <span data-ttu-id="0283f-171">Merhaba varsayılan sayfa boyutu 50'dir ve isteğe bağlı olarak aşağıdaki hello örnek too3 değiştirir.</span><span class="sxs-lookup"><span data-stu-id="0283f-171">hello default page size is 50, and hello example below changes it too3.</span></span>

<span data-ttu-id="0283f-172">Farklı bir sayfa boyutu performans nedenleriyle yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0283f-172">You could configure a different page size for performance reasons.</span></span> <span data-ttu-id="0283f-173">Çok sayıda küçük veri kayıt varsa, yüksek sayfa boyutu hello sunucu gidiş dönüş sayısını azaltır.</span><span class="sxs-lookup"><span data-stu-id="0283f-173">If you have a large number of small data records, a high page size reduces hello number of server round-trips.</span></span>

<span data-ttu-id="0283f-174">Bu ayar yalnızca hello sayfa boyutu hello istemci tarafında denetler.</span><span class="sxs-lookup"><span data-stu-id="0283f-174">This setting controls only hello page size on hello client side.</span></span> <span data-ttu-id="0283f-175">Merhaba istemci hello Mobile Apps arka desteklediğinden daha büyük sayfa için bir boyut isterse, hello sayfa boyutu hello maksimum hello arka uç tutulabilir yapılandırılmış toosupport olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="0283f-175">If hello client asks for a larger page size than hello Mobile Apps backend supports, hello page size is capped at hello maximum hello backend is configured toosupport.</span></span>

<span data-ttu-id="0283f-176">Bu ayrıca hello ayardır *numarası* veri kayıtlarını, değil hello *bayt boyutu*.</span><span class="sxs-lookup"><span data-stu-id="0283f-176">This setting is also hello *number* of data records, not hello *byte size*.</span></span>

<span data-ttu-id="0283f-177">Hello istemci sayfa boyutunu artırmak için hello sunucuda hello sayfa boyutunu artırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0283f-177">If you increase hello client page size, you should also increase hello page size on hello server.</span></span> <span data-ttu-id="0283f-178">Bkz: ["nasıl yapılır: hello tablo disk belleği boyutunu Ayarla"](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) hello toodo bu adımları için.</span><span class="sxs-lookup"><span data-stu-id="0283f-178">See ["How to: Adjust hello table paging size"](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for hello steps toodo this.</span></span>

<span data-ttu-id="0283f-179">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="0283f-179">**Objective-C**:</span></span>

```
  MSPullSettings *pullSettings = [[MSPullSettings alloc] initWithPageSize:3];
  [table  pullWithQuery:query queryId:@nil settings:pullSettings
                        completion:^(NSError * _Nullable error) {
                               if(error) {
                    NSLog(@"ERROR %@", error);
                }
                           }];
```


<span data-ttu-id="0283f-180">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="0283f-180">**Swift**:</span></span>

```
let pullSettings = MSPullSettings(pageSize: 3)
table.pullWithQuery(query, queryId:nil, settings: pullSettings) { (error) in
    if let err = error {
        print("ERROR ", err)
    }
}
```

## <span data-ttu-id="0283f-181"><a name="inserting"></a>Nasıl yapılır: Veri Ekle</span><span class="sxs-lookup"><span data-stu-id="0283f-181"><a name="inserting"></a>How to: Insert Data</span></span>
<span data-ttu-id="0283f-182">Yeni bir tablo satırının tooinsert oluşturma bir `NSDictionary` ve çağırma `table insert`.</span><span class="sxs-lookup"><span data-stu-id="0283f-182">tooinsert a new table row, create a `NSDictionary` and invoke `table insert`.</span></span> <span data-ttu-id="0283f-183">Varsa [dinamik şema] olduğu etkin hello Azure App Service mobil arka uç otomatik olarak yeni sütunlar üzerinde hello dayalı oluşturur `NSDictionary`.</span><span class="sxs-lookup"><span data-stu-id="0283f-183">If [Dynamic Schema] is enabled, hello Azure App Service mobile backend automatically generates new columns based on hello `NSDictionary`.</span></span>

<span data-ttu-id="0283f-184">Varsa `id` hello arka uç otomatik olarak yeni bir benzersiz kimlik oluşturur değil sağlanır</span><span class="sxs-lookup"><span data-stu-id="0283f-184">If `id` is not provided, hello backend automatically generates a new unique ID.</span></span> <span data-ttu-id="0283f-185">Kendi sağlamak `id` toouse e-posta adresleri, kullanıcı adlarını veya kendi özel değerlerinizi kimliği olarak</span><span class="sxs-lookup"><span data-stu-id="0283f-185">Provide your own `id` toouse email addresses, usernames, or your own custom values as ID.</span></span> <span data-ttu-id="0283f-186">Kendi Kimliğinizi sağlayarak, birleştirmeler ve işle ilgili veritabanı mantığı kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="0283f-186">Providing your own ID may ease joins and business-oriented database logic.</span></span>

<span data-ttu-id="0283f-187">Merhaba `result` eklenmiş hello yeni öğe içeriyor.</span><span class="sxs-lookup"><span data-stu-id="0283f-187">hello `result` contains hello new item that was inserted.</span></span> <span data-ttu-id="0283f-188">Sunucu mantığınızı bağlı olarak ek olabilir veya karşılaştırıldığında değiştirilen verileri toowhat toohello sunucu geçirildi.</span><span class="sxs-lookup"><span data-stu-id="0283f-188">Depending on your server logic, it may have additional or modified data compared toowhat was passed toohello server.</span></span>

<span data-ttu-id="0283f-189">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="0283f-189">**Objective-C**:</span></span>

```
NSDictionary *newItem = @{@"id": @"custom-id", @"text": @"my new item", @"complete" : @NO};
[table insert:newItem completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

<span data-ttu-id="0283f-190">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="0283f-190">**Swift**:</span></span>

```
let newItem = ["id": "custom-id", "text": "my new item", "complete": false]
table.insert(newItem) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

## <span data-ttu-id="0283f-191"><a name="modifying"></a>Nasıl yapılır: verileri değiştirme</span><span class="sxs-lookup"><span data-stu-id="0283f-191"><a name="modifying"></a>How to: Modify Data</span></span>
<span data-ttu-id="0283f-192">bir öğe ve çağrı tooupdate var olan bir satır değiştirme `update`:</span><span class="sxs-lookup"><span data-stu-id="0283f-192">tooupdate an existing row, modify an item and call `update`:</span></span>

<span data-ttu-id="0283f-193">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="0283f-193">**Objective-C**:</span></span>

```
NSMutableDictionary *newItem = [oldItem mutableCopy]; // oldItem is NSDictionary
[newItem setValue:@"Updated text" forKey:@"text"];
[table update:newItem completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

<span data-ttu-id="0283f-194">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="0283f-194">**Swift**:</span></span>

```
if let newItem = oldItem.mutableCopy() as? NSMutableDictionary {
    newItem["text"] = "Updated text"
    table2.update(newItem as [NSObject: AnyObject], completion: { (result, error) -> Void in
        if let err = error {
            print("ERROR ", err)
        } else if let item = result {
            print("Todo Item: ", item["text"])
        }
    })
}
```

<span data-ttu-id="0283f-195">Alternatif olarak, hello satır kimliği ve güncelleştirilmiş hello alan sağlayın:</span><span class="sxs-lookup"><span data-stu-id="0283f-195">Alternatively, supply hello row ID and hello updated field:</span></span>

<span data-ttu-id="0283f-196">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="0283f-196">**Objective-C**:</span></span>

```
[table update:@{@"id":@"custom-id", @"text":"my EDITED item"} completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

<span data-ttu-id="0283f-197">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="0283f-197">**Swift**:</span></span>

```
table.update(["id": "custom-id", "text": "my EDITED item"]) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

<span data-ttu-id="0283f-198">En azından hello `id` güncelleştirmeleri yaparken özniteliği ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0283f-198">At minimum, hello `id` attribute must be set when making updates.</span></span>

## <span data-ttu-id="0283f-199"><a name="deleting"></a>Nasıl yapılır: verileri Sil</span><span class="sxs-lookup"><span data-stu-id="0283f-199"><a name="deleting"></a>How to: Delete Data</span></span>
<span data-ttu-id="0283f-200">bir öğeyi, toodelete çağırma `delete` hello öğe:</span><span class="sxs-lookup"><span data-stu-id="0283f-200">toodelete an item, invoke `delete` with hello item:</span></span>

<span data-ttu-id="0283f-201">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="0283f-201">**Objective-C**:</span></span>

```
[table delete:item completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

<span data-ttu-id="0283f-202">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="0283f-202">**Swift**:</span></span>

```
table.delete(newItem as [NSObject: AnyObject]) { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

<span data-ttu-id="0283f-203">Alternatif olarak, satır kimliği sağlayarak Sil:</span><span class="sxs-lookup"><span data-stu-id="0283f-203">Alternatively, delete by providing a row ID:</span></span>

<span data-ttu-id="0283f-204">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="0283f-204">**Objective-C**:</span></span>

```
[table deleteWithId:@"37BBF396-11F0-4B39-85C8-B319C729AF6D" completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

<span data-ttu-id="0283f-205">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="0283f-205">**Swift**:</span></span>

```
table.deleteWithId("37BBF396-11F0-4B39-85C8-B319C729AF6D") { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

<span data-ttu-id="0283f-206">En azından hello `id` yapma sildiğinde özniteliği ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0283f-206">At minimum, hello `id` attribute must be set when making deletes.</span></span>

## <span data-ttu-id="0283f-207"><a name="customapi"></a>Nasıl yapılır: özel API çağrısı</span><span class="sxs-lookup"><span data-stu-id="0283f-207"><a name="customapi"></a>How to: Call Custom API</span></span>
<span data-ttu-id="0283f-208">Özel bir API ile herhangi bir arka uç işlevsellik getirebilir.</span><span class="sxs-lookup"><span data-stu-id="0283f-208">With a custom API, you can expose any backend functionality.</span></span> <span data-ttu-id="0283f-209">Toomap tooa tablo işlemi yok.</span><span class="sxs-lookup"><span data-stu-id="0283f-209">It doesn't have toomap tooa table operation.</span></span> <span data-ttu-id="0283f-210">Yalnızca ileti üzerinde daha fazla denetim kazanmak yapın, hatta okuma/kümesi üstbilgileri ve hello yanıt gövdesi biçimini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="0283f-210">Not only do you gain more control over messaging, you can even read/set headers and change hello response body format.</span></span> <span data-ttu-id="0283f-211">nasıl toocreate özel bir API hello arka uç üzerinde okuma toolearn [özel API'leri](app-service-mobile-node-backend-how-to-use-server-sdk.md#work-easy-apis)</span><span class="sxs-lookup"><span data-stu-id="0283f-211">toolearn how toocreate a custom API on hello backend, read [Custom APIs](app-service-mobile-node-backend-how-to-use-server-sdk.md#work-easy-apis)</span></span>

<span data-ttu-id="0283f-212">toocall özel bir API çağrısı `MSClient.invokeAPI`.</span><span class="sxs-lookup"><span data-stu-id="0283f-212">toocall a custom API, call `MSClient.invokeAPI`.</span></span> <span data-ttu-id="0283f-213">Merhaba istek ve yanıt içerik JSON olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="0283f-213">hello request and response content are treated as JSON.</span></span> <span data-ttu-id="0283f-214">toouse diğer medya türleri [kullanım hello diğer aşırı yüklemesini `invokeAPI` ] [ 5].</span><span class="sxs-lookup"><span data-stu-id="0283f-214">toouse other media types, [use hello other overload of `invokeAPI`][5].</span></span>  <span data-ttu-id="0283f-215">toomake bir `GET` yerine isteği bir `POST` isteği, kümesi parametresi `HTTPMethod` çok`"GET"` ve parametre `body` çok`nil` (GET istekleri İleti gövdeleri değil olduğundan.) Özel API'nizi diğer HTTP fiilleri destekliyorsa, değiştirme `HTTPMethod` uygun şekilde.</span><span class="sxs-lookup"><span data-stu-id="0283f-215">toomake a `GET` request instead of a `POST` request, set parameter `HTTPMethod` too`"GET"` and parameter `body` too`nil` (since GET requests do not have message bodies.) If your custom API supports other HTTP verbs, change `HTTPMethod` appropriately.</span></span>

<span data-ttu-id="0283f-216">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="0283f-216">**Objective-C**:</span></span>

```
[self.client invokeAPI:@"sendEmail"
                  body:@{ @"contents": @"Hello world!" }
            HTTPMethod:@"POST"
            parameters:@{ @"to": @"bill@contoso.com", @"subject" : @"Hi!" }
               headers:nil
            completion: ^(NSData *result, NSHTTPURLResponse *response, NSError *error) {
                if(error) {
                    NSLog(@"ERROR %@", error);
                } else {
                    // Do something with result
                }
            }];
```

<span data-ttu-id="0283f-217">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="0283f-217">**Swift**:</span></span>

```
client.invokeAPI("sendEmail",
            body: [ "contents": "Hello World" ],
            HTTPMethod: "POST",
            parameters: [ "to": "bill@contoso.com", "subject" : "Hi!" ],
            headers: nil)
            {
                (result, response, error) -> Void in
                if let err = error {
                    print("ERROR ", err)
                } else if let res = result {
                          // Do something with result
                }
        }
```

## <span data-ttu-id="0283f-218"><a name="templates"></a>Nasıl yapılır: yazmaç anında iletme şablonları toosend platformlar arası bildirimleri</span><span class="sxs-lookup"><span data-stu-id="0283f-218"><a name="templates"></a>How to: Register push templates toosend cross-platform notifications</span></span>
<span data-ttu-id="0283f-219">tooregister şablonları şablonlarıyla geçirmek, **client.push registerDeviceToken** istemci uygulamanızı yöntemi.</span><span class="sxs-lookup"><span data-stu-id="0283f-219">tooregister templates, pass templates with your **client.push registerDeviceToken** method in your client app.</span></span>

<span data-ttu-id="0283f-220">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="0283f-220">**Objective-C**:</span></span>

```
[client.push registerDeviceToken:deviceToken template:iOSTemplate completion:^(NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    }
}];
```

<span data-ttu-id="0283f-221">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="0283f-221">**Swift**:</span></span>

```
    client.push?.registerDeviceToken(NSData(), template: iOSTemplate, completion: { (error) in
        if let err = error {
            print("ERROR ", err)
        }
    })
```

<span data-ttu-id="0283f-222">Şablonlarınızı türü NSDictionary ve birden fazla şablon içinde biçimini izleyen hello içerebilir:</span><span class="sxs-lookup"><span data-stu-id="0283f-222">Your templates are of type NSDictionary and can contain multiple templates in hello following format:</span></span>

<span data-ttu-id="0283f-223">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="0283f-223">**Objective-C**:</span></span>

```
NSDictionary *iOSTemplate = @{ @"templateName": @{ @"body": @{ @"aps": @{ @"alert": @"$(message)" } } } };
```

<span data-ttu-id="0283f-224">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="0283f-224">**Swift**:</span></span>

```
let iOSTemplate = ["templateName": ["body": ["aps": ["alert": "$(message)"]]]]
```

<span data-ttu-id="0283f-225">Tüm etiketleri güvenlik hello isteğinden kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="0283f-225">All tags are stripped from hello request for security.</span></span>  <span data-ttu-id="0283f-226">tooadd etiketler tooinstallations veya yüklemeleri içinde şablonları için bkz: [hello .NET arka uç sunucusu SDK ile Azure Mobile Apps için iş][4].</span><span class="sxs-lookup"><span data-stu-id="0283f-226">tooadd tags tooinstallations or templates within installations, see [Work with hello .NET backend server SDK for Azure Mobile Apps][4].</span></span>  <span data-ttu-id="0283f-227">kayıtlı bu şablonları kullanarak toosend bildirimleri çalışabilirsiniz [bildirim hub'ları API'leri][3].</span><span class="sxs-lookup"><span data-stu-id="0283f-227">toosend notifications using these registered templates, work with [Notification Hubs APIs][3].</span></span>

## <span data-ttu-id="0283f-228"><a name="errors"></a>Nasıl yapılır: hata işleme</span><span class="sxs-lookup"><span data-stu-id="0283f-228"><a name="errors"></a>How to: Handle Errors</span></span>
<span data-ttu-id="0283f-229">Azure uygulama hizmeti mobil arka uç çağırdığınızda hello tamamlama bloğu içeren bir `NSError` parametresi.</span><span class="sxs-lookup"><span data-stu-id="0283f-229">When you call an Azure App Service mobile backend, hello completion block contains an `NSError` parameter.</span></span> <span data-ttu-id="0283f-230">Hata oluştuğunda, bu parametre nil olmayan olur.</span><span class="sxs-lookup"><span data-stu-id="0283f-230">When an error occurs, this parameter is non-nil.</span></span> <span data-ttu-id="0283f-231">Kodunuzda bu parametreyi denetleyin ve kod parçacıkları önceki hello gösterildiği gibi gerektiğinde Merhaba hatayı işleyebilir.</span><span class="sxs-lookup"><span data-stu-id="0283f-231">In your code, you should check this parameter and handle hello error as needed, as demonstrated in hello preceding code snippets.</span></span>

<span data-ttu-id="0283f-232">Merhaba dosya [ `<WindowsAzureMobileServices/MSError.h>` ] [ 6] hello sabitleri tanımlar `MSErrorResponseKey`, `MSErrorRequestKey`, ve `MSErrorServerItemKey`.</span><span class="sxs-lookup"><span data-stu-id="0283f-232">hello file [`<WindowsAzureMobileServices/MSError.h>`][6] defines hello constants `MSErrorResponseKey`, `MSErrorRequestKey`, and `MSErrorServerItemKey`.</span></span> <span data-ttu-id="0283f-233">tooget ilgili daha fazla verileri toohello hata:</span><span class="sxs-lookup"><span data-stu-id="0283f-233">tooget more data related toohello error:</span></span>

<span data-ttu-id="0283f-234">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="0283f-234">**Objective-C**:</span></span>

```
NSDictionary *serverItem = [error.userInfo objectForKey:MSErrorServerItemKey];
```

<span data-ttu-id="0283f-235">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="0283f-235">**Swift**:</span></span>

```
let serverItem = error.userInfo[MSErrorServerItemKey]
```

<span data-ttu-id="0283f-236">Ayrıca, her hata kodunu sabitleri hello dosya tanımlar:</span><span class="sxs-lookup"><span data-stu-id="0283f-236">In addition, hello file defines constants for each error code:</span></span>

<span data-ttu-id="0283f-237">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="0283f-237">**Objective-C**:</span></span>

```
if (error.code == MSErrorPreconditionFailed) {
```

<span data-ttu-id="0283f-238">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="0283f-238">**Swift**:</span></span>

```
if (error.code == MSErrorPreconditionFailed) {
```

## <span data-ttu-id="0283f-239"><a name="adal"></a>Nasıl yapılır: kullanıcıların hello Active Directory kimlik doğrulama kitaplığı ile kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="0283f-239"><a name="adal"></a>How to: Authenticate users with hello Active Directory Authentication Library</span></span>
<span data-ttu-id="0283f-240">Azure Active Directory'yi kullanarak uygulamanıza hello Active Directory Authentication Library (ADAL) toosign kullanıcılar kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="0283f-240">You can use hello Active Directory Authentication Library (ADAL) toosign users into your application using Azure Active Directory.</span></span> <span data-ttu-id="0283f-241">Bir kimlik sağlayıcısı SDK kullanarak istemci akış kimlik doğrulaması olan tercih toousing hello `loginWithProvider:completion:` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="0283f-241">Client flow authentication using an identity provider SDK is preferable toousing hello `loginWithProvider:completion:` method.</span></span>  <span data-ttu-id="0283f-242">İstemci akış kimlik doğrulaması daha yerel bir UX fikir sağlar ve ek özelleştirme için sağlar.</span><span class="sxs-lookup"><span data-stu-id="0283f-242">Client flow authentication provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="0283f-243">Aşağıdaki hello tarafından mobil uygulamanızın arka ucuna AAD oturum açma için yapılandırma [tooconfigure App Service nasıl Active Directory oturum açma için] [ 7] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="0283f-243">Configure your mobile app backend for AAD sign-in by following hello [How tooconfigure App Service for Active Directory login][7] tutorial.</span></span> <span data-ttu-id="0283f-244">Yerel istemci uygulaması kaydı emin toocomplete hello isteğe bağlı adım olun.</span><span class="sxs-lookup"><span data-stu-id="0283f-244">Make sure toocomplete hello optional step of registering a native client application.</span></span> <span data-ttu-id="0283f-245">İOS için öneririz URI'dir hello biçiminde o hello yeniden yönlendirme `<app-scheme>://<bundle-id>`.</span><span class="sxs-lookup"><span data-stu-id="0283f-245">For iOS, we recommend that hello redirect URI is of hello form `<app-scheme>://<bundle-id>`.</span></span> <span data-ttu-id="0283f-246">Daha fazla bilgi için bkz: Merhaba [ADAL iOS quickstart][8].</span><span class="sxs-lookup"><span data-stu-id="0283f-246">For more information, see hello [ADAL iOS quickstart][8].</span></span>
2. <span data-ttu-id="0283f-247">ADAL Cocoapods kullanarak yükleyin.</span><span class="sxs-lookup"><span data-stu-id="0283f-247">Install ADAL using Cocoapods.</span></span> <span data-ttu-id="0283f-248">Tanımı aşağıdaki, değiştirme, Podfile tooinclude hello Düzenle **YOUR proje** Xcode projenizi hello adı:</span><span class="sxs-lookup"><span data-stu-id="0283f-248">Edit your Podfile tooinclude hello following definition, replacing **YOUR-PROJECT** with hello name of your Xcode project:</span></span>

        source 'https://github.com/CocoaPods/Specs.git'
        link_with ['YOUR-PROJECT']
        xcodeproj 'YOUR-PROJECT'

   <span data-ttu-id="0283f-249">ve Pod hello:</span><span class="sxs-lookup"><span data-stu-id="0283f-249">and hello Pod:</span></span>

        pod 'ADALiOS'
3. <span data-ttu-id="0283f-250">Çalıştırma hello Terminali kullanarak `pod install` hello dizininden projenizi içeren ve oluşturulan hello Xcode çalışma alanı (Merhaba proje değil) açın.</span><span class="sxs-lookup"><span data-stu-id="0283f-250">Using hello Terminal, run `pod install` from hello directory containing your project, and then open hello generated Xcode workspace (not hello project).</span></span>
4. <span data-ttu-id="0283f-251">Kod tooyour uygulama aşağıdaki, kullanmakta olduğunuz toohello dil according hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0283f-251">Add hello following code tooyour application, according toohello language you are using.</span></span> <span data-ttu-id="0283f-252">Her, bu değişiklikleri yapın:</span><span class="sxs-lookup"><span data-stu-id="0283f-252">In each, make these replacements:</span></span>

   * <span data-ttu-id="0283f-253">Değiştir **INSERT yetkilisi burada** uygulamanızı sağlanan hello Kiracı hello adı.</span><span class="sxs-lookup"><span data-stu-id="0283f-253">Replace **INSERT-AUTHORITY-HERE** with hello name of hello tenant in which you provisioned your application.</span></span> <span data-ttu-id="0283f-254">Https://login.microsoftonline.com/contoso.onmicrosoft.com biçiminde olmalıdır. Bu değer, hello etki alanı sekmesinden hello [Klasik Azure portalı] Azure Active Directory'yi kopyalanabilir.</span><span class="sxs-lookup"><span data-stu-id="0283f-254">The format should be https://login.microsoftonline.com/contoso.onmicrosoft.com. This value can be copied from hello Domain tab in your Azure Active Directory in hello [Azure classic portal].</span></span>
   * <span data-ttu-id="0283f-255">Değiştir **Ekle-RESOURCE-kimliği-Buraya** , mobil uygulamanızın arka ucuna için hello istemci kimliği.</span><span class="sxs-lookup"><span data-stu-id="0283f-255">Replace **INSERT-RESOURCE-ID-HERE** with hello client ID for your mobile app backend.</span></span> <span data-ttu-id="0283f-256">İstemci kimliği hello edinebilirsiniz **Gelişmiş** altında sekmesinde **Azure Active Directory ayarları** hello Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="0283f-256">You can obtain the client ID from hello **Advanced** tab under **Azure Active Directory Settings** in hello portal.</span></span>
   * <span data-ttu-id="0283f-257">Değiştir **Ekle-istemci-kimliği-Buraya** hello yerel istemci uygulamasından kopyaladığınız hello istemci kimliği.</span><span class="sxs-lookup"><span data-stu-id="0283f-257">Replace **INSERT-CLIENT-ID-HERE** with hello client ID you copied from hello native client application.</span></span>
   * <span data-ttu-id="0283f-258">Değiştir **Ekle-REDIRECT-URI-Buraya** sitenizin ile */.auth/login/done* hello HTTPS şeması kullanarak uç nokta.</span><span class="sxs-lookup"><span data-stu-id="0283f-258">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using hello HTTPS scheme.</span></span> <span data-ttu-id="0283f-259">Bu değer çok benzer olmalıdır*https://contoso.azurewebsites.net/.auth/login/done*.</span><span class="sxs-lookup"><span data-stu-id="0283f-259">This value should be similar too*https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

<span data-ttu-id="0283f-260">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="0283f-260">**Objective-C**:</span></span>

    #import <ADALiOS/ADAuthenticationContext.h>
    #import <ADALiOS/ADAuthenticationSettings.h>
    // ...
    - (void) authenticate:(UIViewController*) parent
               completion:(void (^) (MSUser*, NSError*))completionBlock;
    {
        NSString *authority = @"INSERT-AUTHORITY-HERE";
        NSString *resourceId = @"INSERT-RESOURCE-ID-HERE";
        NSString *clientId = @"INSERT-CLIENT-ID-HERE";
        NSURL *redirectUri = [[NSURL alloc]initWithString:@"INSERT-REDIRECT-URI-HERE"];
        ADAuthenticationError *error;
        ADAuthenticationContext *authContext = [ADAuthenticationContext authenticationContextWithAuthority:authority error:&error];
        authContext.parentController = parent;
        [ADAuthenticationSettings sharedInstance].enableFullScreen = YES;
        [authContext acquireTokenWithResource:resourceId
                                     clientId:clientId
                                  redirectUri:redirectUri
                              completionBlock:^(ADAuthenticationResult *result) {
                                  if (result.status != AD_SUCCEEDED)
                                  {
                                      completionBlock(nil, result.error);;
                                  }
                                  else
                                  {
                                      NSDictionary *payload = @{
                                                                @"access_token" : result.tokenCacheStoreItem.accessToken
                                                                };
                                      [client loginWithProvider:@"aad" token:payload completion:completionBlock];
                                  }
                              }];
    }


<span data-ttu-id="0283f-261">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="0283f-261">**Swift**:</span></span>

    // add hello following imports tooyour bridging header:
    //        #import <ADALiOS/ADAuthenticationContext.h>
    //        #import <ADALiOS/ADAuthenticationSettings.h>

    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let authority = "INSERT-AUTHORITY-HERE"
        let resourceId = "INSERT-RESOURCE-ID-HERE"
        let clientId = "INSERT-CLIENT-ID-HERE"
        let redirectUri = NSURL(string: "INSERT-REDIRECT-URI-HERE")
        var error: AutoreleasingUnsafeMutablePointer<ADAuthenticationError?> = nil
        let authContext = ADAuthenticationContext(authority: authority, error: error)
        authContext.parentController = parent
        ADAuthenticationSettings.sharedInstance().enableFullScreen = true
        authContext.acquireTokenWithResource(resourceId, clientId: clientId, redirectUri: redirectUri) { (result) in
                if result.status != AD_SUCCEEDED {
                    completion(nil, result.error)
                }
                else {
                    let payload: [String: String] = ["access_token": result.tokenCacheStoreItem.accessToken]
                    client.loginWithProvider("aad", token: payload, completion: completion)
                }
            }
    }

## <span data-ttu-id="0283f-262"><a name="facebook-sdk"></a>Nasıl yapılır: Merhaba Facebook SDK'sı iOS için kullanıcılara kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="0283f-262"><a name="facebook-sdk"></a>How to: Authenticate users with hello Facebook SDK for iOS</span></span>
<span data-ttu-id="0283f-263">Facebook kullanarak uygulamanıza hello Facebook SDK'sı iOS toosign kullanıcılar için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0283f-263">You can use hello Facebook SDK for iOS toosign users into your application using Facebook.</span></span>  <span data-ttu-id="0283f-264">Bir istemci akış kimlik doğrulaması kullanmaktır tercih toousing hello `loginWithProvider:completion:` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="0283f-264">Using a client flow authentication is preferable toousing hello `loginWithProvider:completion:` method.</span></span>  <span data-ttu-id="0283f-265">Merhaba istemci akış kimlik doğrulaması daha yerel bir UX fikir sağlar ve ek özelleştirme için sağlar.</span><span class="sxs-lookup"><span data-stu-id="0283f-265">hello client flow authentication provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="0283f-266">İzleyerek, mobil uygulamanızın arka ucuna Facebook oturum açma için yapılandırma [tooconfigure App Service nasıl Facebook oturum açma için] [ 9] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="0283f-266">Configure your mobile app backend for Facebook sign-in by following the [How tooconfigure App Service for Facebook login][9] tutorial.</span></span>
2. <span data-ttu-id="0283f-267">Merhaba Facebook SDK'sı iOS için aşağıdaki hello tarafından yüklemek [Facebook SDK'sı iOS - Getting Started] [ 10] belgeleri.</span><span class="sxs-lookup"><span data-stu-id="0283f-267">Install hello Facebook SDK for iOS by following hello [Facebook SDK for iOS - Getting Started][10] documentation.</span></span> <span data-ttu-id="0283f-268">Bir uygulama oluşturmak yerine hello iOS platformu tooyour mevcut kayıt ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0283f-268">Instead of creating an app, you can add hello iOS platform tooyour existing registration.</span></span>
3. <span data-ttu-id="0283f-269">Facebook'ın belgeleri hello uygulama temsilci bazı Objective-C kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="0283f-269">Facebook's documentation includes some Objective-C code in hello App Delegate.</span></span> <span data-ttu-id="0283f-270">Kullanıyorsanız **Swift**, çevirileri AppDelegate.swift için aşağıdaki hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0283f-270">If you are using **Swift**, you can use hello following translations for AppDelegate.swift:</span></span>

        // Add hello following import tooyour bridging header:
        //        #import <FBSDKCoreKit/FBSDKCoreKit.h>

        func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
            FBSDKApplicationDelegate.sharedInstance().application(application, didFinishLaunchingWithOptions: launchOptions)
            // Add any custom logic here.
            return true
        }

        func application(application: UIApplication, openURL url: NSURL, sourceApplication: String?, annotation: AnyObject?) -> Bool {
            let handled = FBSDKApplicationDelegate.sharedInstance().application(application, openURL: url, sourceApplication: sourceApplication, annotation: annotation)
            // Add any custom logic here.
            return handled
        }
4. <span data-ttu-id="0283f-271">Toplama tooadding içinde `FBSDKCoreKit.framework` tooyour projesi, ayrıca bir başvuru çok ekleyin`FBSDKLoginKit.framework` hello de aynı şekilde.</span><span class="sxs-lookup"><span data-stu-id="0283f-271">In addition tooadding `FBSDKCoreKit.framework` tooyour project, also add a reference too`FBSDKLoginKit.framework` in hello same way.</span></span>
5. <span data-ttu-id="0283f-272">Kod tooyour uygulama aşağıdaki, kullanmakta olduğunuz toohello dil according hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0283f-272">Add hello following code tooyour application, according toohello language you are using.</span></span>

<span data-ttu-id="0283f-273">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="0283f-273">**Objective-C**:</span></span>

    #import <FBSDKLoginKit/FBSDKLoginKit.h>
    #import <FBSDKCoreKit/FBSDKAccessToken.h>
    // ...
    - (void) authenticate:(UIViewController*) parent
               completion:(void (^) (MSUser*, NSError*)) completionBlock;
    {        
        FBSDKLoginManager *loginManager = [[FBSDKLoginManager alloc] init];
        [loginManager
         logInWithReadPermissions: @[@"public_profile"]
         fromViewController:parent
         handler:^(FBSDKLoginManagerLoginResult *result, NSError *error) {
             if (error) {
                 completionBlock(nil, error);
             } else if (result.isCancelled) {
                 completionBlock(nil, error);
             } else {
                 NSDictionary *payload = @{
                                           @"access_token":result.token.tokenString
                                           };
                 [client loginWithProvider:@"facebook" token:payload completion:completionBlock];
             }
         }];
    }

<span data-ttu-id="0283f-274">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="0283f-274">**Swift**:</span></span>

    // Add hello following imports tooyour bridging header:
    //        #import <FBSDKLoginKit/FBSDKLoginKit.h>
    //        #import <FBSDKCoreKit/FBSDKAccessToken.h>

    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let loginManager = FBSDKLoginManager()
        loginManager.logInWithReadPermissions(["public_profile"], fromViewController: parent) { (result, error) in
            if (error != nil) {
                completion(nil, error)
            }
            else if result.isCancelled {
                completion(nil, error)
            }
            else {
                let payload: [String: String] = ["access_token": result.token.tokenString]
                client.loginWithProvider("facebook", token: payload, completion: completion)
            }
        }
    }

## <span data-ttu-id="0283f-275"><a name="twitter-fabric"></a>Nasıl yapılır: iOS için kullanıcılara Twitter doku ile kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="0283f-275"><a name="twitter-fabric"></a>How to: Authenticate users with Twitter Fabric for iOS</span></span>
<span data-ttu-id="0283f-276">Twitter kullanarak uygulamanıza iOS toosign kullanıcılar için doku kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0283f-276">You can use Fabric for iOS toosign users into your application using Twitter.</span></span> <span data-ttu-id="0283f-277">İstemci akış kimlik doğrulamasıdır tercih toousing hello `loginWithProvider:completion:` şekliyle yöntemi daha yerel bir UX fikir sağlar ve ek özelleştirme için sağlar.</span><span class="sxs-lookup"><span data-stu-id="0283f-277">Client Flow authentication is preferable toousing hello `loginWithProvider:completion:` method, as it provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="0283f-278">Aşağıdaki hello tarafından mobil uygulamanızın arka ucuna Twitter oturum açma için yapılandırma [tooconfigure App Service nasıl Twitter oturum açma için](app-service-mobile-how-to-configure-twitter-authentication.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="0283f-278">Configure your mobile app backend for Twitter sign-in by following hello [How tooconfigure App Service for Twitter login](app-service-mobile-how-to-configure-twitter-authentication.md) tutorial.</span></span>
2. <span data-ttu-id="0283f-279">Doku tooyour projesi tarafından aşağıdaki hello eklemek [iOS - Getting Started için doku] belgeleri ve TwitterKit ayarlama.</span><span class="sxs-lookup"><span data-stu-id="0283f-279">Add Fabric tooyour project by following hello [Fabric for iOS - Getting Started] documentation and setting up TwitterKit.</span></span>

   > [!NOTE]
   > <span data-ttu-id="0283f-280">Varsayılan olarak, doku bir Twitter uygulaması sizin için oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0283f-280">By default, Fabric creates a Twitter application for you.</span></span> <span data-ttu-id="0283f-281">Merhaba tüketici anahtarı ve tüketici önceki kod parçacıkları aşağıdaki hello kullanılarak oluşturulan gizli kaydederek bir uygulama oluşturmaya önleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0283f-281">You can avoid creating an application by registering hello Consumer Key and Consumer Secret you created earlier using hello following code snippets.</span></span>    <span data-ttu-id="0283f-282">Alternatif olarak, hello tüketici anahtarı değiştirebilir ve tüketici gizli anahtarı değerlerini tooApp hizmeti ile Merhaba değerleri sağlayın görmek hello [doku Panosu].</span><span class="sxs-lookup"><span data-stu-id="0283f-282">Alternatively, you can replace hello Consumer Key and Consumer Secret values that you provide tooApp Service with hello values you see in hello [Fabric Dashboard].</span></span> <span data-ttu-id="0283f-283">Bu seçeneği seçerseniz, emin tooset hello geri çağırma URL'si tooa yer tutucu değerini, aşağıdaki gibi olması `https://<yoursitename>.azurewebsites.net/.auth/login/twitter/callback`.</span><span class="sxs-lookup"><span data-stu-id="0283f-283">If you choose this option, be sure tooset hello callback URL tooa placeholder value, such as `https://<yoursitename>.azurewebsites.net/.auth/login/twitter/callback`.</span></span>
   >
   >

    <span data-ttu-id="0283f-284">Daha önce oluşturduğunuz hello gizli toouse seçerseniz, aşağıdaki kodu tooyour uygulama temsilci hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="0283f-284">If you choose toouse hello secrets you created earlier, add hello following code tooyour App Delegate:</span></span>

    <span data-ttu-id="0283f-285">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="0283f-285">**Objective-C**:</span></span>

        #import <Fabric/Fabric.h>
        #import <TwitterKit/TwitterKit.h>
        // ...
        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
        {
            [[Twitter sharedInstance] startWithConsumerKey:@"your_key" consumerSecret:@"your_secret"];
            [Fabric with:@[[Twitter class]]];
            // Add any custom logic here.
            return YES;
        }

    <span data-ttu-id="0283f-286">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="0283f-286">**Swift**:</span></span>

        import Fabric
        import TwitterKit
        // ...
        func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
            Twitter.sharedInstance().startWithConsumerKey("your_key", consumerSecret: "your_secret")
            Fabric.with([Twitter.self])
            // Add any custom logic here.
            return true
        }
3. <span data-ttu-id="0283f-287">Kod tooyour uygulama aşağıdaki, kullanmakta olduğunuz toohello dil according hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0283f-287">Add hello following code tooyour application, according toohello language you are using.</span></span>

<span data-ttu-id="0283f-288">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="0283f-288">**Objective-C**:</span></span>

    #import <TwitterKit/TwitterKit.h>
    // ...
    - (void)authenticate:(UIViewController*)parent completion:(void (^) (MSUser*, NSError*))completionBlock
    {
        [[Twitter sharedInstance] logInWithCompletion:^(TWTRSession *session, NSError *error) {
            if (session) {
                NSDictionary *payload = @{
                                            @"access_token":session.authToken,
                                            @"access_token_secret":session.authTokenSecret
                                        };
                [client loginWithProvider:@"twitter" token:payload completion:completionBlock];
            } else {
                completionBlock(nil, error);
            }
        }];
    }

<span data-ttu-id="0283f-289">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="0283f-289">**Swift**:</span></span>

    import TwitterKit
    // ...
    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let client = self.table!.client
        Twitter.sharedInstance().logInWithCompletion { session, error in
            if (session != nil) {
                let payload: [String: String] = ["access_token": session!.authToken, "access_token_secret": session!.authTokenSecret]
                client.loginWithProvider("twitter", token: payload, completion: completion)
            } else {
                completion(nil, error)
            }
        }
    }

## <span data-ttu-id="0283f-290"><a name="google-sdk"></a>Nasıl yapılır: kullanıcılar iOS için hello Google oturum açma SDK ile kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="0283f-290"><a name="google-sdk"></a>How to: Authenticate users with hello Google Sign-In SDK for iOS</span></span>
<span data-ttu-id="0283f-291">Bir Google hesabı kullanarak uygulamanıza hello Google oturum açma SDK iOS toosign kullanıcılar için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0283f-291">You can use hello Google Sign-In SDK for iOS toosign users into your application using a Google account.</span></span>  <span data-ttu-id="0283f-292">Google en son değişiklikleri tootheir OAuth güvenlik ilkeleri duyurdu.</span><span class="sxs-lookup"><span data-stu-id="0283f-292">Google recently announced changes tootheir OAuth security policies.</span></span>  <span data-ttu-id="0283f-293">Bu ilke değişikliklerini gelecekteki hello Google SDK'da hello kullanımını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="0283f-293">These policy changes will require hello use of the Google SDK in hello future.</span></span>

1. <span data-ttu-id="0283f-294">Aşağıdaki hello tarafından mobil uygulamanızın arka ucuna Google oturum açma için yapılandırma [tooconfigure App Service nasıl Google oturum açma için](app-service-mobile-how-to-configure-google-authentication.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="0283f-294">Configure your mobile app backend for Google sign-in by following hello [How tooconfigure App Service for Google login](app-service-mobile-how-to-configure-google-authentication.md) tutorial.</span></span>
2. <span data-ttu-id="0283f-295">Merhaba Google SDK'sı iOS için aşağıdaki hello tarafından yüklemek [Google oturum açma iOS için-başlangıç tümleştirme](https://developers.google.com/identity/sign-in/ios/start-integrating) belgeleri.</span><span class="sxs-lookup"><span data-stu-id="0283f-295">Install hello Google SDK for iOS by following hello [Google Sign-In for iOS - Start integrating](https://developers.google.com/identity/sign-in/ios/start-integrating) documentation.</span></span> <span data-ttu-id="0283f-296">"Merhaba kimlik doğrulaması ile bir arka uç sunucu" bölümüne atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0283f-296">You may skip hello "Authenticate with a Backend Server" section.</span></span>
3. <span data-ttu-id="0283f-297">Tooyour temsilcinin aşağıdaki hello eklemek `signIn:didSignInForUser:withError:` yöntemi, kullanmakta olduğunuz toohello dil göre.</span><span class="sxs-lookup"><span data-stu-id="0283f-297">Add hello following tooyour delegate's `signIn:didSignInForUser:withError:` method, according toohello language you are using.</span></span>

<span data-ttu-id="0283f-298">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="0283f-298">**Objective-C**:</span></span>

        NSDictionary *payload = @{
                                  @"id_token":user.authentication.idToken,
                                  @"authorization_code":user.serverAuthCode
                                  };

        [client loginWithProvider:@"google" token:payload completion:^(MSUser *user, NSError *error) {
            // ...
        }];

<span data-ttu-id="0283f-299">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="0283f-299">**Swift**:</span></span>

        let payload: [String: String] = ["id_token": user.authentication.idToken, "authorization_code": user.serverAuthCode]
        client.loginWithProvider("google", token: payload) { (user, error) in
            // ...
        }

1. <span data-ttu-id="0283f-300">Ayrıca ekleyin hello çok aşağıdaki emin olun`application:didFinishLaunchingWithOptions:` uygulamanızda temsilci, "SERVER_CLIENT_ID" hello ile değiştiriliyor aynı Bu, kullanılan tooconfigure uygulama hizmeti 1. adımda kimliği.</span><span class="sxs-lookup"><span data-stu-id="0283f-300">Make sure you also add hello following too`application:didFinishLaunchingWithOptions:` in your app delegate, replacing "SERVER_CLIENT_ID" with hello same ID that you used tooconfigure App Service in step 1.</span></span>

<span data-ttu-id="0283f-301">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="0283f-301">**Objective-C**:</span></span>

         [GIDSignIn sharedInstance].serverClientID = @"SERVER_CLIENT_ID";

 <span data-ttu-id="0283f-302">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="0283f-302">**Swift**:</span></span>

        GIDSignIn.sharedInstance().serverClientID = "SERVER_CLIENT_ID"


1. <span data-ttu-id="0283f-303">Kod tooyour hello uygulayan bir UIViewController uygulamasında aşağıdaki hello eklemek `GIDSignInUIDelegate` protokolü, kullanmakta olduğunuz toohello dil göre.</span><span class="sxs-lookup"><span data-stu-id="0283f-303">Add hello following code tooyour application in a UIViewController that implements hello `GIDSignInUIDelegate` protocol, according toohello language you are using.</span></span>  <span data-ttu-id="0283f-304">Yeniden imzalanmakta önce oturumu kapattınız ve kimlik bilgilerinizi yeniden tooenter gerekmeyen karşın, bir onay iletişim kutusu görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0283f-304">You are signed out before being signed in again, and although you don't need tooenter your credentials again, you see a consent dialog.</span></span>  <span data-ttu-id="0283f-305">Merhaba Oturum belirteci süresi dolan yalnızca bu yöntemi çağırın.</span><span class="sxs-lookup"><span data-stu-id="0283f-305">Only call this method when hello session token has expired.</span></span>

   <span data-ttu-id="0283f-306">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="0283f-306">**Objective-C**:</span></span>

       #import <Google/SignIn.h>
       // ...
       - (void)authenticate
       {
               [GIDSignIn sharedInstance].uiDelegate = self;
               [[GIDSignIn sharedInstance] signOut];
               [[GIDSignIn sharedInstance] signIn];
        }

   <span data-ttu-id="0283f-307">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="0283f-307">**Swift**:</span></span>

       // ...
       func authenticate() {
           GIDSignIn.sharedInstance().uiDelegate = self
           GIDSignIn.sharedInstance().signOut()
           GIDSignIn.sharedInstance().signIn()
       }

<!-- Anchors. -->

[What is Mobile Services]: #what-is
[Concepts]: #concepts
[Setup and Prerequisites]: #Setup
[How to: Create hello Mobile Services client]: #create-client
[How to: Create a table reference]: #table-reference
[How to: Query data from a mobile service]: #querying
[Filter returned data]: #filtering
[Sort returned data]: #sorting
[Return data in pages]: #paging
[Select specific columns]: #selecting
[How to: Bind data toohello user interface]: #binding
[How to: Insert data into a mobile service]: #inserting
[How to: Modify data in a mobile service]: #modifying
[How to: Authenticate users]: #authentication
[Cache authentication tokens]: #caching-tokens
[How to: Upload images and large files]: #blobs
[How to: Handle errors]: #errors
[How to: Design unit tests]: #unit-testing
[How to: Customize hello client]: #customizing
[Customize request headers]: #custom-headers
[Customize data type serialization]: #custom-serialization
[Next Steps]: #next-steps
[How to: Use MSQuery]: #query-object

<!-- Images. -->

<!-- URLs. -->
[Azure Mobile Apps Hızlı Başlangıç]: app-service-mobile-ios-get-started.md

[Add Mobile Services tooExisting App]: /develop/mobile/tutorials/get-started-data
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Validate and modify data in Mobile Services by using server scripts]: /develop/mobile/tutorials/validate-modify-and-augment-data-ios
[Mobile Services SDK]: https://go.microsoft.com/fwLink/p/?LinkID=266533
[Authentication]: /develop/mobile/tutorials/get-started-with-users-ios
[iOS SDK]: https://developer.apple.com/xcode

[Handling Expired Tokens]: http://go.microsoft.com/fwlink/p/?LinkId=301955
[Live Connect SDK]: http://go.microsoft.com/fwlink/p/?LinkId=301960
[Permissions]: http://msdn.microsoft.com/library/windowsazure/jj193161.aspx
[Service-side Authorization]: mobile-services-javascript-backend-service-side-authorization.md
[Use scripts tooauthorize users]: /develop/mobile/tutorials/authorize-users-in-scripts-ios
[dinamik şema]: http://go.microsoft.com/fwlink/p/?LinkId=296271
[How to: access custom parameters]: /develop/mobile/how-to-guides/work-with-server-scripts#access-headers
[Create a table]: http://msdn.microsoft.com/library/windowsazure/jj193162.aspx
[NSDictionary object]: http://go.microsoft.com/fwlink/p/?LinkId=301965
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[CLI toomanage Mobile Services tables]: /cli/azure/get-started-with-az-cli2
[Conflict-Handler]: mobile-services-ios-handling-conflicts-offline-data.md#add-conflict-handling

[doku Panosu]: https://www.fabric.io/home
[iOS - Getting Started için doku]: https://docs.fabric.io/ios/fabric/getting-started.html
[1]: https://github.com/Azure/azure-mobile-apps-ios-client/blob/master/README.md#ios-client-sdk
[2]: http://azure.github.io/azure-mobile-apps-ios-client/
[3]: https://msdn.microsoft.com/library/azure/dn495101.aspx
[4]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags
[5]: http://azure.github.io/azure-mobile-services/iOS/v3/Classes/MSClient.html#//api/name/invokeAPI:data:HTTPMethod:parameters:headers:completion:
[6]: https://github.com/Azure/azure-mobile-services/blob/master/sdk/iOS/src/MSError.h
[7]: app-service-mobile-how-to-configure-active-directory-authentication.md
[8]: ../active-directory/active-directory-devquickstarts-ios.md
[9]: app-service-mobile-how-to-configure-facebook-authentication.md
[10]: https://developers.facebook.com/docs/ios/getting-started
