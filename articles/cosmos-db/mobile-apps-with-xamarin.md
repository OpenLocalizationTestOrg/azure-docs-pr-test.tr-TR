---
title: Xamarin ve Azure Cosmos DB aaaBuild mobil uygulamalar | Microsoft Docs
description: "Xamarin iOS, Android veya formlar oluşturan bir Öğreticisi Azure Cosmos DB kullanarak uygulama. Azure Cosmos DB hızlı, planet ölçek, mobil uygulamaları için bulut veritabanı değil."
services: cosmos-db
documentationcenter: .net
author: arramac
manager: monicar
editor: 
ms.assetid: ff97881a-b41a-499d-b7ab-4f394df0e153
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/03/2017
ms.author: arramac
ms.openlocfilehash: 362a0e239a61e1309e1cf720c23151760952cf69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="build-mobile-applications-with-xamarin-and-azure-cosmos-db"></a>Xamarin ve Azure Cosmos DB mobil uygulamaları derleme
Azure Cosmos DB mobil uygulamaları için bir bulut veritabanıdır ve mobil uygulamaları toostore veri hello bulutta gerekir. Her şeyi mobil geliştiricinin ihtiyacı vardır. Bu tam olarak yönetilen isteğe bağlı olarak ölçeklenen bir hizmet olarak veritabanıdır. Kullanıcılarınızın Merhaba Dünya bulunan her yerde onu saydam, veri tooyour uygulamanıza kullanıma sunabilirsiniz. Hello kullanarak [Azure Cosmos DB .NET Core SDK](documentdb-sdk-dotnet-core.md), Xamarin mobil uygulamaları toointeract orta katman olmadan Azure Cosmos DB ile doğrudan etkinleştirebilirsiniz.

Bu makale, Xamarin ve Azure Cosmos DB mobil uygulamaları oluşturmak için bir öğretici sağlar. Merhaba öğreticiye hello tam kaynak kodunu bulabilirsiniz [Xamarin ve Azure Cosmos DB github'da](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin), nasıl dahil toomanage kullanıcılar ve izinler.

## <a name="azure-cosmos-db-capabilities-for-mobile-apps"></a>Mobil uygulamaları için Azure Cosmos DB özellikleri
Mobil uygulama geliştiricileri için anahtar özellikler aşağıdaki hello Azure Cosmos DB sağlar:

![Mobil uygulamaları için Azure Cosmos DB özellikleri](media/mobile-apps-with-xamarin/documentdb-for-mobile.png)

* Şemasız verileri üzerinden zengin sorgular. Azure Cosmos DB verileri heterojen koleksiyonları şemasız JSON belgeleri olarak depolar. Sunduğu [zengin ve hızlı sorguları](documentdb-sql-query.md) hello şemaları veya dizinleri hakkında tooworry gerekir.
* Hızlı işleme. İşlem yalnızca birkaç milisaniye Azure Cosmos DB tooread ve yazma belgelerle alır. İsteğe bağlı olarak Azure Cosmos DB yüzde 99,99 SLA ile geliştirir ve geliştiricilerin ihtiyaç duydukları hello verimlilik belirtebilirsiniz.
* Sınırsız ölçekleme. Azure Cosmos DB koleksiyonlarınızı [uygulamanız büyüdükçe büyümesine](partition-data.md). Küçük boyutlu veriler ve saniye başına istek yüzlerce verimi ile başlayabilirsiniz. Koleksiyonunuz veri ve büyük verimi toopetabytes istekleri saniye başına milyonlarca yüzlerce büyüyebilir.
* Genel olarak dağıtılmış. Kullanıcılar hello mobil uygulama gidin, genellikle Merhaba dünya genelindeki. Azure Cosmos veritabanı bir [Genel dağıtılmış veritabanı](distribute-data-globally.md). Merhaba harita toomake veri erişilebilir tooyour kullanıcılar'ı tıklatın.
* Yerleşik zengin yetkilendirme. Azure Cosmos DB ile gibi popüler düzenleri kolayca uygulayabilirsiniz [kullanıcı başına veri](https://aka.ms/documentdb-xamarin-todouser) veya çok kullanıcılı paylaşılan karmaşık özel yetkilendirme kodu olmadan veri.
* Jeo-uzamsal sorgular. Birçok mobil uygulamaları bugün coğrafi bağlamsal deneyimleri sunar. Birinci sınıf desteğiyle [Jeo-uzamsal türleri](geospatial.md), bu deneyimleri kolay tooaccomplish oluşturma Azure Cosmos DB yapar.
* İkili dosya eklerini. Uygulama verilerinizi genellikle ikili BLOB'ları içerir. Ekler için yerel destek daha kolay toouse Azure Cosmos DB bir tek bir Mağazanız uygulama verileriniz için olarak kolaylaştırır.

## <a name="azure-cosmos-db-and-xamarin-tutorial"></a>Azure Cosmos DB ve Xamarin Öğreticisi
Eğitmen gösterir nasıl aşağıdaki hello toobuild Xamarin ve Azure Cosmos DB kullanarak bir mobil uygulama. Merhaba öğreticiye hello tam kaynak kodunu bulabilirsiniz [Xamarin ve Azure Cosmos DB github'da](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin).

### <a name="get-started"></a>başlarken
Azure Cosmos DB ile başlatılan kolay tooget olur. Toohello Azure portalına gidin ve yeni bir Azure Cosmos DB hesabı oluşturun. Merhaba tıklatın **Hızlı Başlangıç** sekmesi. Zaten indirme hello Xamarin Forms Yapılacaklar listesi örnek tooyour Azure Cosmos DB hesabı bağlı. 

![Mobil uygulamaları için Azure Cosmos DB hızlı başlangıç](media/mobile-apps-with-xamarin/cosmos-db-quickstart.png)

Veya varolan bir Xamarin uygulaması varsa, hello ekleyebilirsiniz [Azure Cosmos DB NuGet paketini](documentdb-sdk-dotnet-core.md). Xamarin Forms paylaşılan kitaplıklar ve Xamarin.IOS, Xamarin.Android, Azure Cosmos DB destekler.

### <a name="work-with-data"></a>Verilerle çalışma
Veri kayıtlarını Azure Cosmos DB içinde heterojen koleksiyonları şemasız JSON belgeleri olarak depolanır. Hello farklı yapıları içeren belgeleri depolamak için aynı koleksiyon:

```cs
    var result = await client.CreateDocumentAsync(collectionLink, todoItem);
```

Xamarin projelerinizi şemasız verileri üzerinde dil ile tümleşik sorgu kullanabilirsiniz:

```cs
    var query = await client.CreateDocumentQuery<ToDoItem>(collectionLink)
                    .Where(todoItem => todoItem.Complete == false)
                    .AsDocumentQuery();

    Items = new List<TodoItem>();
    while (query.HasMoreResults) {
        Items.AddRange(await query.ExecuteNextAsync<TodoItem>());
    }
```
### <a name="add-users"></a>Kullanıcı ekle
Birçok başlatılan örnekleri alın gibi hello Azure Cosmos DB örnek indirdiğiniz hello uygulamanın kodda bir ana anahtar sabit kodlanmış kullanarak toohello hizmet kimliğini doğrular. Bu varsayılan yerel öykünücüsünde dışında herhangi bir yere toorun düşündüğünüz bir uygulama için iyi bir uygulama değildir. Merhaba ana anahtar elde yetkisiz bir kullanıcı varsa, tüm hello verileri Azure Cosmos DB hesabınızı boyunca tehlikeye girebilir. Bunun yerine, uygulama tooaccess yalnızca hello oturum açmış kullanıcı kayıtlarını hello istiyor. Azure Cosmos DB toogrant uygulama okuma veya okuma/yazma izni tooa koleksiyonu, bir bölüm anahtarı göre gruplandırılmış belgeleri ya da belirli bir belge geliştiricilerin sağlar. 

Bu adımları toomodify hello Yapılacaklar listesi uygulaması tooa çok kullanıcılı Yapılacaklar listesi uygulaması izleyin: 

  1. Facebook, Active Directory veya başka bir sağlayıcı kullanarak oturum açma tooyour uygulama ekleyin.

  2. Bir Azure Cosmos DB UserItems koleksiyonuyla oluşturma **/userId** hello bölüm anahtarı olarak. Merhaba bölüm anahtarı koleksiyonunuz için Azure Cosmos DB tooscale, uygulama kullanıcılarınızın hello sayıda sonsuz verir belirtme, toooffer hızlı sorguları devam ederken artar.

  3. Azure Cosmos DB kaynak belirteci Aracısı ekleyin. Bu basit Web API, kullanıcıların kimliğini doğrular ve kısa süreli belirteçler toosigned içindeki kullanıcılar kendi bölüm içinde yalnızca toohello belgeler erişimle sorunları. Bu örnekte, kaynak belirteci Aracısı App Service içinde barındırılır.

  4. Merhaba uygulama tooauthenticate tooResource belirteci Aracısı Facebook ile değiştirin ve hello kaynak belirteçleri hello oturum açmış kullanıcıların Facebook isteyin. Merhaba UserItems koleksiyonu verilerini daha sonra erişebilirsiniz.  

Bu desene tam kod örneğini bulabilirsiniz [kaynak belirteci Aracısı github'da](http://aka.ms/documentdb-xamarin-todouser). Bu diyagramda hello çözüm gösterilir:

![Azure Cosmos DB kullanıcılar ve izinler Aracısı](media/mobile-apps-with-xamarin/documentdb-resource-token-broker.png)

İki kullanıcılar toohave erişim toohello istiyorsanız aynı Yapılacaklar listesi, kaynak belirteci Aracısı ek izinler toohello erişim belirteci ekleyebilirsiniz.

### <a name="scale-on-demand"></a>İsteğe bağlı olarak ölçeklendirin
Azure Cosmos DB yönetilen bir hizmet olarak veritabanıdır. Kullanıcı tabanınızı büyüdükçe, VM'ler sağlama veya çekirdek artırma hakkında tooworry gerekmez. Tüm tootell Azure Cosmos DB gereken budur (verim) saniyede kaç işlemi uygulamanız gerekir. Merhaba verimlilik hello aracılığıyla belirtebilirsiniz **ölçek** verimlilik saniye başına istek birimleri (RUs) adlı bir ölçü kullanarak sekmesi. Örneğin, bir 1 KB belge üzerinde okuma işlemi 1 gerektirir RU. Uyarıları toohello de ekleyebilirsiniz **işleme** ölçüm toomonitor hello trafiği büyüme ve yangın uyarıları gibi hello verimlilik programlı olarak değiştirin.

![İsteğe bağlı Azure Cosmos DB ölçek işleme](media/mobile-apps-with-xamarin/cosmos-db-xamarin-scale.png)

### <a name="go-planet-scale"></a>Planet ölçek gidin
Uygulama kazançlar popülerliği Merhaba Dünya çapında kullanıcıların elde. Veya beklenmedik olaylar için hazırlanmış toobe istediğiniz olabilir. Toohello Azure portalına gidin ve Azure Cosmos DB hesabınızı açın. Merhaba harita toomake veri sürekli çoğaltma tooany numaranızı bölgelerinin Merhaba dünya genelindeki'ı tıklatın. Bu özellik, kullanıcılarınızın nerede olursa olsun, verilerinizi kullanılabilir hale getirir. Yük devretme ilkeleri toobe olasılıkları için hazırlanmış de ekleyebilirsiniz.

![Coğrafi bölgeler arasında Azure Cosmos DB ölçek](media/mobile-apps-with-xamarin/cosmos-db-xamarin-replicate.png)

Tebrikler. Merhaba çözüm tamamladınız ve Xamarin ve Azure Cosmos DB mobil uygulamaya sahip. Benzer adımları toobuild Cordova uygulamaları hello Azure Cosmos DB JavaScript SDK'sı ve yerel iOS/Android uygulamalar Azure Cosmos DB REST API'lerini kullanarak izleyin.

## <a name="next-steps"></a>Sonraki adımlar
* Görüntülemek için kaynak kodunu hello [Xamarin ve Azure Cosmos DB github'da](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin).
* Merhaba karşıdan [Azure Cosmos DB .NET Core SDK](documentdb-sdk-dotnet-core.md).
* Daha fazla kod örnekleri için bulma [.NET uygulamaları](documentdb-dotnet-samples.md).
* Hakkında bilgi edinin [Azure Cosmos DB zengin sorgu özellikleri](documentdb-sql-query.md).
* Hakkında bilgi edinin [Jeo-uzamsal destek Azure Cosmos veritabanı](geospatial.md).



