---
title: "aaaEnable çevrimdışı eşitleme Azure mobil uygulamanızın (Xamarin iOS)"
description: "Bilgi nasıl toouse mobil uygulama hizmeti toocache ve eşitleme çevrimdışı verileri Xamarin iOS uygulaması"
documentationcenter: xamarin
author: ggailey777
manager: cfowler
editor: 
services: app-service\mobile
ms.assetid: 828a287c-5d58-4540-9527-1309ebb0f32b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 5243f2d292377d8de103a40f45d649394f11b97c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-xamarinios-mobile-app"></a>Xamarin.iOS mobil uygulamanız için çevrimdışı eşitlemeyi etkinleştirin
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>Genel Bakış
Bu öğretici Xamarin.iOS için Azure Mobile Apps hello çevrimdışı eşitleme özelliğini sunar. Çevrimdışı eşitleme son kullanıcıların toointeract görüntüleme, ekleme veya ağ bağlantısı olduğunda bile veri--değiştirme mobil bir uygulama ile--sağlar. Değişiklikler yerel bir veritabanında depolanır. Merhaba aygıt yeniden çevrimiçi olduktan sonra bu değişiklikleri hello uzak hizmeti ile eşitlenir.

Bu öğreticide, hello Xamarin.iOS uygulaması projeden güncelleştirme [bir Xamarin iOS uygulaması oluşturma] toosupport hello Azure Mobile Apps çevrimdışı özellikleri. Kullanmıyorsanız, hızlı başlangıç sunucu projesi hello indirilen, hello veri erişim uzantısı paketlerini projenize eklemeniz gerekir. Server uzantısı paketleri hakkında daha fazla bilgi için bkz: [hello .NET arka uç sunucusu SDK ile Azure Mobile Apps için iş](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

Merhaba çevrimdışı eşitleme özelliği hakkında daha fazla toolearn hello konusuna bakın [Azure Mobile Apps çevrimdışı veri eşitleme].

## <a name="update-hello-client-app-toosupport-offline-features"></a>Merhaba istemci uygulaması toosupport çevrimdışı özelliklere güncelleştirme
Çevrimdışı bir senaryoda olduğunda azure mobil uygulama çevrimdışı özellikler, yerel bir veritabanı ile toointeract sağlar. Bu özellikler, uygulamanızda toouse başlatma bir [SyncContext] tooa yerel deposu. Tablonuz hello [IMobileServiceSyncTable] arabirimi aracılığıyla başvuru. SQLite hello aygıtta hello yerel deposu olarak kullanılır.

1. Açık hello NuGet Paket Yöneticisi hello tamamlandı hello projesinde [bir Xamarin iOS uygulaması oluşturma] öğretici, ardından arayın ve yükleme hello **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet Paket.
2. Merhaba QSTodoService.cs dosyasını açın ve hello açıklamadan çıkarın `#define OFFLINE_SYNC_ENABLED` tanımı.
3. Yeniden oluşturma ve hello istemci uygulamasını çalıştırın. Merhaba uygulaması çevrimdışı eşitleme etkinleştirilmeden önce onu aynı vermedi hello çalışır. Ancak, hello yerel veritabanı, artık çevrimdışı bir senaryoda kullanılabilir verilerle doldurulur.

## <a name="update-sync"></a>Merhaba uygulama toodisconnect hello arka güncelleştir
Bu bölümde, hello bağlantı tooyour mobil uygulama arka uç toosimulate bir çevrimdışı duruma bölün. Veri öğeleri eklediğinizde, özel durum işleyicisi, bu hello uygulama çevrimdışı modda olduğunu bildirir. Bu durumda, hello yerel eklenen yeni öğeler depolamak ve anında iletme bağlı bir durumda İleri çalıştırıldığında, mobil uygulama arka ucu hello için eşitlenir.

1. QSToDoService.cs hello paylaşılan projesinde düzenleyin. Değişiklik hello **applicationURL** toopoint tooan geçersiz URL:

         const string applicationURL = @"https://your-service.azurewebsites.fail";

    Ayrıca, wifi ve hello aygıt cep telefonu ağlarda devre dışı bırakma veya uçak modu kullanılarak çevrimdışı davranışı sergiler.
2. Derleme ve hello uygulamayı çalıştırın. Ne zaman başlatılan uygulama hello üzerinde yenileme başarısız oldu, eşitleme dikkat edin.
3. Yeni öğeler girin ve anında iletme her tıkladığınızda [CancelledByNetworkError] durumu ile başarısız fark **kaydetmek**. Ancak, toohello mobil uygulama arka ucu gönderilemez kadar hello yeni Yapılacaklar öğelerini hello yerel depoda mevcut.  Bir üretim hello istemci uygulaması hala gibi davranır bu özel durumlar bastırmak, uygulama toohello mobil uygulamanızın arka ucuna bağlı.
4. Merhaba uygulamasını kapatın ve oluşturduğunuz hello yeni öğeler kalıcı toohello yerel deposu olduğunu tooverify yeniden başlatın.
5. (İsteğe bağlı) Bir Bilgisayara Visual Studio yüklüyse açmak **Sunucu Gezgini**. Tooyour veritabanında gidin **Azure**-> **SQL veritabanları**. Veritabanınıza sağ tıklatıp **SQL Server nesne Gezgini'nde Aç**. Şimdi tooyour SQL veritabanı tablosunda ve içeriği göz atabilirsiniz. Merhaba arka uç veritabanı Hello verilerde değişmediğini doğrulayın.
6. (İsteğe bağlı) Formda bir GET sorgu kullanarak, mobil arka uç Fiddler veya Postman tooquery gibi REST aracını `https://<your-mobile-app-backend-name>.azurewebsites.net/tables/TodoItem`.

## <a name="update-online-app"></a>Mobil uygulama arka Hello uygulama tooreconnect güncelleştir
Bu bölümde, hello uygulama toohello mobil uygulama arka ucu yeniden bağlanın. Bu, çevrimdışı duruma tooan çevrimiçi duruma hello mobil uygulama arka ucu ile taşınan hello uygulama benzetimini yapar.   Ağ bağlantısını devre dışı bırakarak hello ağ arıza benzetimli, hiçbir kod değişiklikleri gereklidir.
Merhaba ağ yeniden etkinleştirin.  Merhaba uygulaması ilk kez çalıştırdığınızda, hello `RefreshDataAsync` yöntemi çağrılır. Bu sırayla çağırır `SyncAsync` yerel depolama hello arka uç veritabanı ile toosync.

1. QSToDoService.cs hello paylaşılan projeyi açın ve hello değişikliğinizi geri **applicationURL** özelliği.
2. Yeniden oluşturun ve hello uygulamayı çalıştırın. Merhaba uygulama yerel değişikliklerinizi anında iletme ve çekme işlemlerini hello kullanarak hello Azure mobil uygulama arka ucu ile eşitlenen `OnRefreshItemsSelected` yöntemini yürütür.
3. (İsteğe bağlı) SQL Server Nesne Gezgini veya Fiddler gibi bir REST araç kullanarak veri görünümü hello güncelleştirildi. Bildirim hello veri hello Azure mobil uygulama arka uç veritabanı ve hello yerel deposu arasında eşitlendi.
4. Merhaba uygulamanın hello onay tıklayın birkaç öğeleri toocomplete bunları hello yerel deposunda kutusu.

   `CompleteItemAsync`çağrıları `SyncAsync` hello mobil uygulama arka ucu ile tamamlandı toosync her öğesi. `SyncAsync`hem İtme hem de çekme çağırır.
   **Bir tabloda bir çekme yürütme zaman hello istemci yapılan değişiklikler için anında iletme hello istemci eşitleme bağlamı üzerinde her zaman ilk otomatik olarak yürütülür**. Merhaba örtük itme hello yerel deposu ilişkileri yanı sıra tüm tablolarda tutarlı kalmasını sağlar. Bu davranış hakkında daha fazla bilgi için bkz: [Azure Mobile Apps çevrimdışı veri eşitleme].

## <a name="review-hello-client-sync-code"></a>Merhaba istemci eşitleme kodu gözden geçirme
Başlangıç Öğreticisi tamamlandığında yüklediğiniz hello Xamarin istemci projesi [bir Xamarin iOS uygulaması oluşturma] zaten yerel bir SQLite veritabanı kullanarak çevrimdışı eşitlemeyi destekleyen kodunu içerir. Burada, hello Eğitmen kodu zaten eklenmiş bir kısa genel bakış verilmiştir. Merhaba özelliği kavramsal bir genel bakış için bkz: [Azure Mobile Apps çevrimdışı veri eşitleme].

* Tablo işlemleri gerçekleştirilmeden önce hello yerel depolama başlatılmalıdır. Merhaba yerel deposu veritabanı başlatılmış zaman `QSTodoListViewController.ViewDidLoad()` yürütür `QSTodoService.InitializeStoreAsync()`. Bu yöntem hello kullanarak yeni bir yerel SQLite veritabanı oluşturur `MobileServiceSQLiteStore` hello Azure mobil uygulaması istemci SDK'sı tarafından sağlanan sınıfı.

    Merhaba `DefineTable` yöntemi, sağlanan hello türündeki hello alanlar eşleşen hello yerel deposunda bir tablo oluşturur `ToDoItem` bu durumda. Merhaba türü tooinclude hello uzak veritabanındaki tüm hello sütunları yok. Bu, olası toostore yalnızca bir sütun alt kümesi olur.

        // QSTodoService.cs

        public async Task InitializeStoreAsync()
        {
            var store = new MobileServiceSQLiteStore(localDbPath);
            store.DefineTable<ToDoItem>();

            // Uses hello default conflict handler, which fails on conflict
            await client.SyncContext.InitializeAsync(store);
        }
* Merhaba `todoTable` üyesi `QSTodoService` hello olan `IMobileServiceSyncTable` yerine tür `IMobileServiceTable`. Merhaba IMobileServiceSyncTable tüm oluşturma, okuma, güncelleştirme ve (CRUD) tablo işlemleri toohello yerel deposu veritabanı silme yönlendirir.

    Ne zaman bu değişiklikleri toohello Azure mobil uygulama arka ucu çağırarak gönderilen karar `IMobileServiceSyncContext.PushAsync()`. Merhaba eşitleme bağlamı tablo ilişkileri izleme ve bir istemci uygulaması değiştiren tüm tablolarda değişiklikleri Ftp'den korunmasına yardımcı olur `PushAsync` olarak adlandırılır.

    sağlanan hello kod çağrıları `QSTodoService.SyncAsync()` hello todoıtem listesi yenilenir veya todoıtem eklenen veya tamamlanan her toosync. Uygulama eşitlemeler her yerel değişiklikten sonra. Bir çekme hello bağlamdan bekleyen yerel güncelleştirmeleri izlenen bir tabloya karşı yürütülürse, o çekme işlemi otomatik olarak bir bağlam itme ilk tetikler.

    Sağlanan hello kodda, tüm kayıtları hello uzak `TodoItem` tablo sorgulanabilir ancak sorgu kimliği ve sorgu geçirerek da olası toofilter kayıtları olan çok`PushAsync`. Daha fazla bilgi için hello bölümüne bakın *Artımlı eşitleme* içinde [Azure Mobile Apps çevrimdışı veri eşitleme].

        // QSTodoService.cs
        public async Task SyncAsync()
        {
            try
            {
                await client.SyncContext.PushAsync();
                await todoTable.PullAsync("allTodoItems", todoTable.CreateQuery()); // query ID is used for incremental sync
            }

            catch (MobileServiceInvalidOperationException e)
            {
                Console.Error.WriteLine(@"Sync Failed: {0}", e.Message);
            }
        }

## <a name="additional-resources"></a>Ek Kaynaklar
* [Azure Mobile Apps çevrimdışı veri eşitleme]
* [Azure Mobile Apps .NET SDK'sı nasıl yapılır][8]

<!-- Images -->

<!-- URLs. -->
[bir Xamarin iOS uygulaması oluşturma]: app-service-mobile-xamarin-ios-get-started.md
[Azure Mobile Apps çevrimdışı veri eşitleme]: app-service-mobile-offline-data-sync.md
[SyncContext]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.mobileserviceclient.synccontext(v=azure.10).aspx
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
