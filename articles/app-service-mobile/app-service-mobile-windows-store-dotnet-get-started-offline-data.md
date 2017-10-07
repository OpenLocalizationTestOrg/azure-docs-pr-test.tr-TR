---
title: "Mobile Apps ile Evrensel Windows Platformu (UWP) uygulamanız için çevrimdışı eşitleme aaaEnable | Microsoft Docs"
description: "Bilgi nasıl toouse bir Azure mobil uygulaması toocache ve eşitleme çevrimdışı veri Evrensel Windows Platformu (UWP) uygulamanızda."
documentationcenter: windows
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: 8fe51773-90de-4014-8a38-41544446d9b5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: a9f4ad02e92c2c423f10f07b7f1a4270aafd6c6f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-windows-app"></a>Windows uygulamanız için çevrimdışı eşitlemeyi etkinleştirme
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>Genel Bakış
Bu öğretici nasıl tooadd çevrimdışı destek tooa Evrensel Windows Platformu (UWP) uygulamasını bir Azure mobil uygulama arka ucu kullanarak gösterir. Çevrimdışı eşitleme son kullanıcıların toointeract görüntüleme, ekleme veya ağ bağlantısı olduğunda bile veri - değiştirme mobil bir uygulama ile--sağlar. Değişiklikler yerel bir veritabanında depolanır. Merhaba aygıt yeniden çevrimiçi olduktan sonra bu değişiklikleri hello uzak arka uç ile eşitlenir.

Bu öğreticide, hello UWP uygulaması projesi hello öğreticiden güncelleştirme [bir Windows uygulaması oluşturma] toosupport hello Azure Mobile Apps çevrimdışı özellikleri. Kullanmıyorsanız, hızlı başlangıç sunucu projesi hello indirilen, hello veri erişim uzantı paketleri tooyour projesi eklemeniz gerekir. Server uzantısı paketleri hakkında daha fazla bilgi için bkz: [hello .NET arka uç sunucusu SDK ile Azure Mobile Apps için iş](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

Merhaba çevrimdışı eşitleme özelliği hakkında daha fazla toolearn hello konusuna bakın [Azure Mobile Apps çevrimdışı veri eşitleme].

## <a name="requirements"></a>Gereksinimler
Bu öğretici, ön koşullar aşağıdaki hello gerektirir:

* Windows 8.1 veya sonraki sürümlerde çalışan Visual Studio 2013.
* Tamamlanmasından [bir Windows uygulaması oluşturma][bir windows uygulaması oluşturma].
* [Azure Mobile Services SQLite deposu][sqlite store nuget]
* [SQLite Evrensel Windows platformu geliştirme](http://www.sqlite.org/downloads)

## <a name="update-hello-client-app-toosupport-offline-features"></a>Merhaba istemci uygulaması toosupport çevrimdışı özelliklere güncelleştirme
Çevrimdışı bir senaryoda olduğunda azure mobil uygulama çevrimdışı özellikler, yerel bir veritabanı ile toointeract sağlar. toouse bu özellikler, uygulamanızda başlatma bir [SyncContext] [ synccontext] tooa yerel deposu. Tablonuz hello aracılığıyla başvuru [IMobileServiceSyncTable][IMobileServiceSyncTable] arabirimi. SQLite hello aygıtta hello yerel deposu olarak kullanılır.

1. Merhaba yüklemek [hello Evrensel Windows platformu için SQLite çalışma zamanı](http://sqlite.org/2016/sqlite-uwp-3120200.vsix).
2. Merhaba NuGet Paket Yöneticisi hello tamamlandı hello UWP uygulaması projesi için Visual Studio'da açın [bir Windows uygulaması oluşturma] Öğreticisi.
    Arayıp hello Yükle **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet paketi.
3. Çözüm Gezgini'nde sağ **başvuruları** > **Başvuru Ekle...** >**Evrensel Windows** > **uzantıları**, her ikisi de etkinleştirmek **Evrensel Windows platformu için SQLite** ve **Evrensel Windows platformu uygulamalar için Visual C++ 2015 çalışma zamanı**.

    ![SQLite UWP başvuru ekleme][1]
4. Merhaba MainPage.xaml.cs dosyasını açın ve hello açıklamadan çıkarın `#define OFFLINE_SYNC_ENABLED` tanımı.
5. Visual Studio'da hello basın **F5** anahtar toorebuild ve çalışma hello istemci uygulaması. Merhaba uygulaması çevrimdışı eşitleme etkinleştirilmeden önce onu aynı vermedi hello çalışır. Ancak, hello yerel veritabanı, artık çevrimdışı bir senaryoda kullanılabilir verilerle doldurulur.

## <a name="update-sync"></a>Merhaba uygulama toodisconnect hello arka güncelleştir
Bu bölümde, hello bağlantı tooyour mobil uygulama arka uç toosimulate bir çevrimdışı duruma bölün. Veri öğeleri eklediğinizde, özel durum işleyicisi, bu hello uygulama çevrimdışı modda olduğunu bildirir. Bu durumda, hello yerel eklenen yeni öğeler depolamak ve anında iletme bağlı bir durumda İleri çalıştırıldığında, mobil uygulama arka ucu hello için eşitlenir.

1. App.xaml.cs hello paylaşılan projesinde düzenleyin. Açıklama hello hello başlatılması çıkışı **MobileServiceClient** ve bir geçersiz mobil uygulama URL'si kullanan satır aşağıdaki hello ekleyin:

         public static MobileServiceClient MobileService = new MobileServiceClient("https://your-service.azurewebsites.fail");

    Ayrıca, wifi ve hello aygıt cep telefonu ağlarda devre dışı bırakarak çevrimdışı davranışı sergiler veya uçak modu kullanabilirsiniz.
2. Tuşuna **F5** hello uygulama toobuild ve çalıştırın. Ne zaman başlatılan uygulama hello üzerinde yenileme başarısız oldu, eşitleme dikkat edin.
3. Yeni öğeler girin ve anında iletme ile başarısız olduğunu fark bir [CancelledByNetworkError] durum her tıkladığınızda **kaydetmek**. Ancak, toohello mobil uygulama arka ucu gönderilemez kadar hello yeni Yapılacaklar öğelerini hello yerel depoda mevcut.  Bir üretim hello istemci uygulaması hala gibi davranır bu özel durumlar bastırmak, uygulama toohello mobil uygulamanızın arka ucuna bağlı.
4. Merhaba uygulamasını kapatın ve oluşturduğunuz hello yeni öğeler kalıcı toohello yerel deposu olduğunu tooverify yeniden başlatın.
5. (İsteğe bağlı) Visual Studio'da açın **Sunucu Gezgini**. Tooyour veritabanında gidin **Azure**->**SQL veritabanları**. Veritabanınıza sağ tıklatıp **SQL Server nesne Gezgini'nde Aç**. Şimdi tooyour SQL veritabanı tablosunda ve içeriği göz atabilirsiniz. Merhaba arka uç veritabanı Hello verilerde değişmediğini doğrulayın.
6. (İsteğe bağlı) Formda bir GET sorgu kullanarak, mobil arka uç Fiddler veya Postman tooquery gibi REST aracını `https://<your-mobile-app-backend-name>.azurewebsites.net/tables/TodoItem`.

## <a name="update-online-app"></a>Mobil uygulama arka Hello uygulama tooreconnect güncelleştir
Bu bölümde, hello uygulama toohello mobil uygulama arka ucu yeniden bağlanın. Bu değişiklikler hello uygulama bir ağ yeniden bağlanıldığında benzetimi.

Merhaba uygulaması ilk kez çalıştırdığınızda, hello `OnNavigatedTo` olay işleyicisi çağrılarını `InitLocalStoreAsync`. Bu yöntem sırayla çağırır `SyncAsync` yerel depolama hello arka uç veritabanı ile toosync. Merhaba uygulama başlangıçta toosync çalışır.

1. App.xaml.cs hello paylaşılan projeyi açın ve önceki başlangıcına açıklamadan çıkarın `MobileServiceClient` toouse hello doğru hello mobil uygulama URL'si.
2. Tuşuna hello **F5** anahtar toorebuild ve çalışma hello uygulama. Merhaba uygulama yerel değişikliklerinizi anında iletme ve çekme işlemlerini hello kullanarak hello Azure mobil uygulama arka ucu ile eşitlenen `OnNavigatedTo` olay işleyicisi yürütür.
3. (İsteğe bağlı) SQL Server Nesne Gezgini veya Fiddler gibi bir REST araç kullanarak veri görünümü hello güncelleştirildi. Bildirim hello veri hello Azure mobil uygulama arka uç veritabanı ve hello yerel deposu arasında eşitlendi.
4. Merhaba uygulamanın hello onay tıklayın birkaç öğeleri toocomplete bunları hello yerel deposunda kutusu.

   `UpdateCheckedTodoItem`çağrıları `SyncAsync` hello mobil uygulama arka ucu ile tamamlandı toosync her öğesi. `SyncAsync`hem İtme hem de çekme çağırır. Ancak, **bir tabloda bir çekme yürütme zaman hello istemci yapılan değişiklikler için bir itme her zaman otomatik olarak yürütülür**. Bu davranış, tüm tabloları ilişkileri birlikte hello yerel deposunda tutarlı kalmasını sağlar. Bu davranış beklenmeyen bir itme neden olabilir.  Bu davranış hakkında daha fazla bilgi için bkz: [Azure Mobile Apps çevrimdışı veri eşitleme].

## <a name="api-summary"></a>API özeti
toosupport hello çevrimdışı özelliklerini mobil hizmetler, kullandık hello [IMobileServiceSyncTable] arabirim ve başlatıldı [MobileServiceClient.SyncContext] [ synccontext] yerel bir SQLite veritabanı ile. Merhaba yerel depo Hello işlemleri meydana gelirken hello uygulama hala bağlı olarak ne zaman çevrimdışı hello normal CRUD işlemleri mobil uygulamalar için çalışır. yöntemler aşağıdaki hello kullanılan toosynchronize hello yerel deposu hello sunucusuyla şunlardır:

* **[PushAsync]**  bu yöntemi bir üyesi olduğundan [IMobileServicesSyncContext], tüm tablolar arasında değişiklikleri toohello arka uç gönderilir. Yalnızca yerel değişiklikler kayıtları toohello sunucu gönderilir.
* **[PullAsync]**  çekme başlattığınız bir [IMobileServiceSyncTable]. Merhaba tabloda izlenen değişiklik olduğunda örtük bir anında iletme toomake hello yerel deposu ilişkileri yanı sıra tüm tablolarda tutarlı kalmasını çalıştırılır. Merhaba *pushOtherTables* olup olmadığı diğer hello bağlamda tabloları örtük bir anında iletme içinde gönderilen parametresi denetler. Merhaba *sorgu* parametresi alan bir [IMobileServiceTableQuery<T> ] [ IMobileServiceTableQuery] veya OData sorgu dizesi toofilter hello veri döndürdü. Merhaba *QueryId* parametresi kullanılır toodefine Artımlı eşitleme. Daha fazla bilgi için bkz: [çevrimdışı veri eşitlemeye Azure Mobile Apps içinde](app-service-mobile-offline-data-sync.md#how-sync-works).
* **[PurgeAsync]**  düzenli aralıklarla bu yöntem toopurge eski verileri uygulamanızı hello yerel depodan çağırmanız gerekir. Kullanım hello *zorla* henüz eşitlenmemiş değişiklikleri toopurge gerektiğinde parametresi.

Bu kavramlar hakkında daha fazla bilgi için bkz: [çevrimdışı veri eşitlemeye Azure Mobile Apps içinde](app-service-mobile-offline-data-sync.md#how-sync-works).

## <a name="more-info"></a>Daha fazla bilgi
Merhaba aşağıdaki konular ek bilgiler üzerinde mobil uygulamaların hello çevrimdışı eşitleme özelliği sağlar:

* [Azure Mobile Apps çevrimdışı veri eşitleme]
* [Azure Mobile Apps .NET SDK'sı nasıl yapılır][8]

<!-- Anchors. -->
[Update hello app toosupport offline features]: #enable-offline-app
[Update hello sync behavior of hello app]: #update-sync
[Update hello app tooreconnect your Mobile Apps backend]: #update-online-app
[Next Steps]:#next-steps

<!-- Images -->
[1]: ./media/app-service-mobile-windows-store-dotnet-get-started-offline-data/app-service-mobile-add-reference-sqlite-dialog.png
[11]: ./media/app-service-mobile-windows-store-dotnet-get-started-offline-data/app-service-mobile-add-wp81-reference-sqlite-dialog.png
[13]: ./media/app-service-mobile-windows-store-dotnet-get-started-offline-data/cpu-architecture.png


<!-- URLs. -->
[Azure Mobile Apps çevrimdışı veri eşitleme]: app-service-mobile-offline-data-sync.md
[bir windows uygulaması oluşturma]: app-service-mobile-windows-store-dotnet-get-started.md
[SQLite for Windows 8.1]: http://go.microsoft.com/fwlink/?LinkID=716919
[SQLite for Windows Phone 8.1]: http://go.microsoft.com/fwlink/?LinkID=716920
[SQLite for Windows 10]: http://go.microsoft.com/fwlink/?LinkID=716921
[synccontext]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.mobileserviceclient.synccontext(v=azure.10).aspx
[sqlite store nuget]: https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client.SQLiteStore/
[IMobileServiceSyncTable]: https://msdn.microsoft.com/library/azure/mt691742(v=azure.10).aspx
[IMobileServiceTableQuery]: https://msdn.microsoft.com/library/azure/dn250631(v=azure.10).aspx
[IMobileServicesSyncContext]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.imobileservicesynccontext(v=azure.10).aspx
[MobileServicePushFailedException]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.mobileservicepushfailedexception(v=azure.10).aspx
[Status]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.mobileservicepushcompletionresult.status(v=azure.10).aspx
[CancelledByNetworkError]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.mobileservicepushstatus(v=azure.10).aspx
[PullAsync]: https://msdn.microsoft.com/library/azure/mt667558(v=azure.10).aspx
[PushAsync]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.mobileservicesynccontextextensions.pushasync(v=azure.10).aspx
[PurgeAsync]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.imobileservicesynctable.purgeasync(v=azure.10).aspx
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
