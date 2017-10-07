---
title: "Azure Mobile Apps veri eşitleme aaaOffline | Microsoft Docs"
description: "Kavramsal başvurusu ve hello çevrimdışı veri eşitleme özelliği Azure mobil uygulamalar için genel bakış"
documentationcenter: windows
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: 982fb683-8884-40da-96e6-77eeca2500e3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 58673240ba433651faf1f619ca5da33dd6459d2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="offline-data-sync-in-azure-mobile-apps"></a>Azure Mobile Apps’te Çevrimdışı Veri Eşitleme
## <a name="what-is-offline-data-sync"></a>Çevrimdışı veri eşitlemeye nedir?
Çevrimdışı veri eşitlemeye istemci ve sunucu bir ağ bağlantısı işlev geliştiriciler toocreate uygulamaları kolaylaştırır Azure Mobile Apps SDK özelliği ' dir.

Uygulamanızı çevrimdışı modda olduğunda, yine oluşturun ve tooa yerel deposu kaydedilen verileri değiştirebilir. Merhaba uygulama yeniden çevrimiçi olduğunda, yerel değişiklikler, Azure mobil uygulama arka ucu ile eşitleyebilirsiniz. Merhaba özellik de aynı kayıt hem değiştirilir hello istemci hello ve arka uç hello çakışmalarını algılama için destek içerir. Çakışmaları hello sunucu veya hello istemci işlenebilir.

Çevrimdışı eşitleme birkaç avantaj vardır:

* Sunucu verilerini hello cihazda yerel olarak önbelleğe alarak uygulama yanıt hızını artırmak
* Ağ sorunları olduğunda yararlı kalır sağlam uygulamalar oluşturma
* Son kullanıcıların toocreate izin ve çok az kayıpla veya hiç bağlanabilirlik senaryolarını destekleyen hiçbir ağ erişimi olduğunda bile verileri değiştirme
* Birçok cihaz arasında veri eşitlemek ve hello aynı kaydı iki cihazlar tarafından değiştirildiğinde çakışmalarını Algıla
* Yüksek gecikmeli veya ölçülen ağlarda ağ kullanımını sınırla

Eğitim aşağıdaki hello nasıl tooadd çevrimdışı eşitleme Azure Mobile Apps kullanan tooyour mobil istemcilerin göster:

* [Android: Çevrimdışı eşitleme etkinleştir]
* [Apache Cordova: Çevrimdışı eşitleme etkinleştir](app-service-mobile-cordova-get-started-offline-data.md)
* [iOS: Çevrimdışı eşitleme etkinleştir]
* [Xamarin iOS: Çevrimdışı eşitleme etkinleştir]
* [Xamarin Android: Çevrimdışı eşitleme etkinleştir]
* [Xamarin.Forms: Etkinleştir çevrimdışı eşitleme](app-service-mobile-xamarin-forms-get-started-offline-data.md)
* [Evrensel Windows Platformu: etkinleştirmek çevrimdışı eşitleme]

## <a name="what-is-a-sync-table"></a>Bir eşitleme tablo nedir?
tooaccess hello "/ tabloları" uç nokta, SDK'ları sağlamak arabirimleri gibi hello Azure mobil istemci `IMobileServiceTable` (.NET İstemci SDK) veya `MSTable` (iOS istemci). Bu API'leri toohello Azure mobil uygulama arka ucu doğrudan bağlanın ve hello istemci aygıt bir ağ bağlantısı yoksa başarısız olur.

toosupport çevrimdışı kullanım, uygulamanızı yerine kullanması gereken hello *eşitleme tablo* API'leri gibi `IMobileServiceSyncTable` (.NET İstemci SDK) veya `MSSyncTable` (iOS istemci). Aynı CRUD işlemleri (oluşturma, okuma, güncelleştirme, silme) iş eşitleme karşı tüm hello API'leri tablo, bunlar okuma artık dışındaki veya tooa yazma *yerel deposu*. Eşitleme tablo işlemleri gerçekleştirilmeden önce hello yerel depolama başlatılmalıdır.

## <a name="what-is-a-local-store"></a>Yerel bir depo nedir?
Merhaba veri saklama katmanını hello istemci cihazda bir yerel deposudur. hello Azure Mobile Apps istemci SDK'ları yerel varsayılan bir sağlamak uygulama depolar. Windows, Xamarin ve Android, SQLite üzerinde temel alır. İos'ta, temel verilere dayanır.

SQLite tabanlı toouse hello uygulaması Windows Phone veya Windows mağazası 8.1 tooinstall bir SQLite uzantısı gerekir. Daha fazla bilgi için bkz: [Evrensel Windows Platformu: etkinleştirmek çevrimdışı eşitleme]. Android ve iOS nedenle gerekli tooreference SQLite kendi sürümü işletim sistemi kendisini hello aygıtta SQLite sürümüyle birlikte.

Geliştiriciler Ayrıca kendi yerel deposu uygulayabilirsiniz. Örneğin, hello mobil istemcide şifrelenmiş biçimde toostore veri istiyorsanız, şifreleme için SQLCipher kullanan yerel bir depo tanımlayabilirsiniz.

## <a name="what-is-a-sync-context"></a>Eşitleme bağlamı nedir?
A *eşitleme bağlamı* bir mobil istemci nesneyle ilişkilendirilen (gibi `IMobileServiceClient` veya `MSClient`) ve eşitleme tablolarla yapılan değişiklikleri izler. Merhaba eşitleme bağlamı tutar bir *işlem sırası*, hangi sonraki CUD işlemleri (oluşturma, güncelleştirme, silme) sıralı listesini tutar toohello sunucu gönderilmeyecek.

Yerel bir depo hello eşitleme bağlamı başlatma yöntemi kullanılarak ilişkilendirilen `IMobileServicesSyncContext.InitializeAsync(localstore)` hello içinde [.NET İstemci SDK].

## <a name="how-sync-works"></a>Eşitleme çevrimdışı nasıl çalışır
Eşitleme tabloları kullanırken, istemci kodunuzun bir Azure mobil uygulama arka ucu ile yerel değişiklikler olduğunda eşitlenir denetler. Oluncaya kadar bir çağrı çok şey toohello arka uç gönderilen*itme* yerel değişiklikler. Benzer şekilde, yalnızca olduğunda bir çağrı çok hello yerel deposu yeni verilerle doldurulur*çekme* veri.

* **Anında iletme**: anında iletme hello eşitleme bağlamı üzerinde bir işlemi olduğundan ve tüm CUD değişiklikleri hello son zorlama itibaren gönderir. Bu BT Not mümkün değil toosend Aksi takdirde işlemleri bozuk gönderilebilir yalnızca tek bir tablonun değişiklikler olduğundan. Anında iletme hangi sırayla server veritabanınıza değiştirir REST çağrılarını tooyour Azure mobil uygulama arka ucu, bir dizi yürütür.
* **Çekme**: çekme olabilir ve bir tablo başına temelinde gerçekleştirilir sorgu tooretrieve ile yalnızca bir veri alt kümesini hello sunucu özelleştirilmiş. Azure Mobile istemci SDK'ları hello sonra hello sonuç verileri hello yerel deposuna ekleyin.
* **Örtük iter**: çekme bekleyen yerel güncelleştirmeleri içeren bir tablo karşı yürütülürse, hello çekme ilk yürüten bir `push()` hello eşitleme bağlamı üzerinde. Bu itme zaten kuyruğa alınmış değişiklikleri ve yeni verileri hello sunucusundan arasındaki çakışmaları en aza indirmenize yardımcı olur.
* **Artımlı eşitleme**: hello ilk parametre toohello çekme işlemi bir *sorgu adı* yalnızca hello istemcide kullanılır. Null olmayan sorgu adı kullanırsanız, hello Azure Mobile SDK gerçekleştiren bir *Artımlı eşitleme*. Bir çekme işlemi sonuçları, bir dizi döndürür her zaman hello son `updatedAt` zaman damgası, sonuç kümesinden hello SDK yerel sistem tablolarında depolanır. Sonraki çekme işlemleri yalnızca kayıtları sonra zaman damgası alın.

  toouse Artımlı eşitleme sunucunuzun döndürmelidir anlamlı `updatedAt` değerleri ve bu alana göre sıralama desteklemesi gerekir. Ancak, Hello SDK kendi sıralama hello updatedAt alanı ekler olduğundan, kendi sahip bir çekme sorgu kullanamazsınız `orderBy` yan tümcesi.

  Merhaba sorgu adı, seçtiğiniz herhangi bir dize olabilir, ancak uygulamanızda mantıksal her sorgu için benzersiz olmalıdır.
  Aksi takdirde, farklı çekme işlemleri hello üzerine yazabilir aynı Artımlı eşitleme zaman damgası ve sorgularınızı hatalı sonuçlar dönebilirsiniz.

  Merhaba sorgu parametresi varsa, tek yönlü toocreate benzersiz sorgu adı tooincorporate hello parametre değeridir.
  UserId üzerinde filtreleme, örneğin, sorgu adı gibi (C# ') aşağıdakilerden biri olabilir:

        await todoTable.PullAsync("todoItems" + userid,
            syncTable.Where(u => u.UserId == userid));

  Artımlı eşitlenmemiş tooopt istiyorsanız geçirmek `null` sorgu kimliği hello gibi Bu durumda, tüm kayıtlar her çağrıda çok alınır`PullAsync`, büyük olasılıkla yetersiz olduğu.
* **Temizleme**: hello içindekiler yerel deposu hello kullanarak temizleyebilirsiniz `IMobileServiceSyncTable.PurgeAsync`.
  Temizleme, eski veri hello istemci veritabanında varsa veya bekleyen tüm değişiklikleri toodiscard istiyorsanız gerekli olabilir.

  Bir temizleme hello yerel deposu tablosundan temizler. Varsa, özel durum hello temizleme verir hello server veritabanı ile eşitlemeyi sürece bekleyen işlemler hello *temizleme zorla* parametrenin ayarlanmış.

  Eski veri hello istemcide örnek olarak, Device1 yalnızca tamamlanmamış öğeleri çeker hello "Yapılacaklar listesi" örnekte varsayalım. Başka bir aygıt tarafından Hello sunucuda tamamlandı "sütlü satın al" olarak işaretlenmiş bir todoıtem. Ancak, Device1 hala olmayan öğeler yalnızca çekiyor nedeni yerel depolama "sütlü satın al" todoıtem tamamlanma hello içeriyor. Bir temizleme eski bu öğeyi temizler.

## <a name="next-steps"></a>Sonraki adımlar
* [iOS: Çevrimdışı eşitleme etkinleştir]
* [Xamarin iOS: Çevrimdışı eşitleme etkinleştir]
* [Xamarin Android: Çevrimdışı eşitleme etkinleştir]
* [Evrensel Windows Platformu: etkinleştirmek çevrimdışı eşitleme]

<!-- Links -->
[.NET İstemci SDK]: app-service-mobile-dotnet-how-to-use-client-library.md
[Android: Çevrimdışı eşitleme etkinleştir]: app-service-mobile-android-get-started-offline-data.md
[iOS: Çevrimdışı eşitleme etkinleştir]: app-service-mobile-ios-get-started-offline-data.md
[Xamarin iOS: Çevrimdışı eşitleme etkinleştir]: app-service-mobile-xamarin-ios-get-started-offline-data.md
[Xamarin Android: Çevrimdışı eşitleme etkinleştir]: app-service-mobile-xamarin-android-get-started-offline-data.md
[Evrensel Windows Platformu: etkinleştirmek çevrimdışı eşitleme]: app-service-mobile-windows-store-dotnet-get-started-offline-data.md
