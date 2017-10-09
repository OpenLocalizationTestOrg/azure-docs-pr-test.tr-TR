---
title: "aaaEnable çevrimdışı eşitleme Azure mobil uygulamanızın (Cordova) | Microsoft Docs"
description: "Bilgi nasıl toouse mobil uygulama hizmeti toocache ve eşitleme çevrimdışı veri Cordova uygulamanızda"
documentationcenter: cordova
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: 1a3f685d-f79d-4f8b-ae11-ff96e79e9de9
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-cordova-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 4e6ae96c3d96dac8ebb3749354b83a04686831b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-cordova-mobile-app"></a>Cordova mobil uygulamanız için çevrimdışı eşitlemeyi etkinleştirme
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

Bu öğretici Azure Mobile Apps hello çevrimdışı eşitleme özelliği için Cordova tanıtır. Çevrimdışı eşitleme sağlayan bir mobil uygulama ile son kullanıcılar toointeract&mdash;görüntüleme, ekleme veya değiştirme veri&mdash;hiçbir ağ bağlantısı olduğunda bile. Değişiklikler yerel bir veritabanında depolanır.  Merhaba aygıt yeniden çevrimiçi olduktan sonra bu değişiklikleri hello uzak hizmeti ile eşitlenir.

Öğreticiyi tamamladığınızda oluşturduğunuz mobil uygulamalar hello için bu öğreticiyi hello Cordova hızlı başlangıç çözüm üzerinde temel [Apache Cordova Hızlı Başlangıç]. Bu öğreticide, hello hızlı başlangıç çözüm tooadd çevrimdışı özelliklerini Azure Mobile Apps güncelleştirin.  Biz de hello çevrimdışı özgü hello uygulama kodunda vurgulayın.

Merhaba çevrimdışı eşitleme özelliği hakkında daha fazla toolearn hello konusuna bakın [Azure Mobile Apps çevrimdışı veri eşitleme]. Merhaba API kullanım ayrıntıları için bkz [API belgelerine](https://azure.github.io/azure-mobile-apps-js-client).

## <a name="add-offline-sync-toohello-quickstart-solution"></a>Çevrimdışı eşitleme toohello hızlı başlangıç çözüme ekleyin
Merhaba çevrimdışı eşitleme kodu toohello uygulama eklenmesi gerekir. Çevrimdışı eşitleme hello Azure Mobile Apps eklentisi hello projeye dahil bağlandığınızda tooyour uygulama otomatik olarak eklenen hello cordova sqlite depolama eklentisi gerektiriyor. Merhaba hızlı başlangıç projesi bu eklenti her ikisi de içerir.

1. Visual Studio'nun Çözüm Gezgini'nde, index.js açın ve aşağıdaki kodu hello değiştirin

        var client,            // Connection toohello Azure Mobile App backend
           todoItemTable;      // Reference tooa table endpoint on backend

    Bu kodu:

        var client,            // Connection toohello Azure Mobile App backend
           todoItemTable,      // Reference tooa table endpoint on backend
           syncContext;        // Reference toooffline data sync context

2. Ardından, kod aşağıdaki hello değiştirin:

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net');

    Bu kodu:

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net');
        var store = new WindowsAzure.MobileServiceSqliteStore('store.db');

        store.defineTable({
          name: 'todoitem',
          columnDefinitions: {
              id: 'string',
              text: 'string',
              complete: 'boolean',
              version: 'string'
          }
        });

        // Get hello sync context from hello client
        syncContext = client.getSyncContext();

    Merhaba önceki kod eklemeler hello yerel deposunu başlatmak ve kullanılan hello sütun değerlerini eşleşen yerel bir tablo tanımlayın Azure son yedekleyin. (Bu kodda tüm sütun değerlerini tooinclude gerekmez.)  Merhaba `version` alan hello mobil arka uç tarafından korunur ve Çakışma çözümlemesi için kullanılır.

    Bir başvuru toohello eşitleme bağlamı çağırarak alma **getSyncContext**. Merhaba eşitleme bağlamı tablo ilişkileri izleme ve bir istemci uygulaması değiştiren tüm tablolarda değişiklikleri Ftp'den korunmasına yardımcı olur `.push()` olarak adlandırılır.

3. Merhaba uygulama tooyour mobil uygulamayı uygulama URL'si güncelleştirin.

4. Ardından, bu kodu değiştirin:

        todoItemTable = client.getTable('todoitem'); // todoitem is hello table name

    Bu kodu:

        // Initialize hello sync context with hello store
        syncContext.initialize(store).then(function () {

        // Get hello local table reference.
        todoItemTable = client.getSyncTable('todoitem');

        syncContext.pushHandler = {
            onConflict: function (pushError) {
                // Handle hello conflict.
                console.log("Sync conflict! " + pushError.getError().message);
                // Update failed, revert tooserver's copy.
                pushError.cancelAndDiscard();
              },
              onError: function (pushError) {
                  // Handle hello error
                  // In hello simulated offline state, you get "Sync error! Unexpected connection failure."
                  console.log("Sync error! " + pushError.getError().message);
              }
        };

        // Call a function tooperform hello actual sync
        syncBackend();

        // Refresh hello todoItems
        refreshDisplay();

        // Wire up hello UI Event Handler for hello Add Item
        $('#add-item').submit(addItemHandler);
        $('#refresh').on('click', refreshDisplay);

    Merhaba önceki kod hello eşitleme bağlamını başlatır ve ardından (yerine getTable) getSyncTable tooget başvuru toohello yerel tablo çağırır.

    Kod bu kullanır hello yerel veritabanı tüm oluşturmak okuma, güncelleştirme ve Sil (CRUD) tablo işlemleri.

    Bu örnekte basit hata eşitleme çakışmalarını işleme gerçekleştirir. Gerçek bir uygulamada işlemek ağ koşulları, sunucu çakışmaları ve diğerleri gibi çeşitli hatalar hello. Kod örnekleri için bkz: Merhaba [çevrimdışı eşitleme örnek].

5. Ardından, bu işlevi tooperform hello gerçek eşitleme ekleyin.

        function syncBackend() {

          // Sync local store tooAzure table when app loads, or when login complete.
          syncContext.push().then(function () {
              // Push completed

          });

          // Pull items from hello Azure table after syncing tooAzure.
          syncContext.pull(new WindowsAzure.Query('todoitem'));
        }

    Toopush toohello mobil uygulama arka ucu çağırarak değiştiğinde karar **syncContext.push()**. Örneğin, çağırabilirsiniz **syncBackend** düğmesi olay işleyicisi bağlı tooa Eşitle düğmesi içinde.

## <a name="offline-sync-considerations"></a>Çevrimdışı eşitleme konuları

Merhaba örnek hello **itme** yöntemi **syncContext** yalnızca uygulama başlangıç oturum açma için hello geri çağırma işlevi adı verilir.  Gerçek dünya uygulamada el ile tetiklenen bu eşitleme işlevine veya hello ağ durumu değiştiğinde de yapabilirsiniz.

Çekme beklemede olan bir tabloda karşı çalıştırıldığında yerel güncelleştirmeleri bir anında iletme işlemi otomatik olarak Tetikleyicileri çekme hello bağlam tarafından izlenir. Yenileme, ekleme ve bu örnek öğelerde Tamamlanıyor, atlayabilirsiniz olduğunda açık hello **itme** yedek olabileceğinden çağırın.

Sağlanan hello kodda hello uzak Todoıtem tablosu tüm kayıtları seçmeleri istenir, ancak bu da olası toofilter kayıtları sorgu kimliği ve sorgu geçirerek çok**itme**. Daha fazla bilgi için hello bölümüne bakın *Artımlı eşitleme* içinde [Azure Mobile Apps çevrimdışı veri eşitleme].

## <a name="optional-disable-authentication"></a>(İsteğe bağlı) Kimlik doğrulaması devre dışı bırak

Yok tooset çevrimdışı eşitleme sınama önce kimlik doğrulamasını kurmak istediğiniz, oturum açma için hello geri çağırma işlevi çıkışı açıklama, ancak içinde hello kod bırakın hello geri çağırma işlevi uncommented.  Merhaba oturum açma çizgi yorum sonra hello kod aşağıdaki gibidir:

      // Login toohello service.
      // client.login('twitter')
      //    .then(function () {
        syncContext.initialize(store).then(function () {
          // Leave hello rest of hello code in this callback function  uncommented.
                ...
        });
      // }, handleError);

Merhaba uygulama eşitlemeler hello hello uygulama çalıştırdığınızda Azure arka uç ile şimdi.

## <a name="run-hello-client-app"></a>Merhaba istemci uygulaması çalıştırın
Şu anda etkin çevrimdışı eşitleme ile Merhaba istemci uygulaması en az bir kez hello yerel deposu veritabanı doldurmak için her platformda çalıştırabilirsiniz. Daha sonra çevrimdışı bir senaryo benzetimini hello uygulama çevrimdışı durumdayken hello verileri ve hello Yerel Depodaki değiştirebilirsiniz.

## <a name="optional-test-hello-sync-behavior"></a>(İsteğe bağlı) Test hello eşitleme davranışı
Bu bölümde, arka ucunuz için geçersiz uygulama URL'si kullanarak hello istemci projesi toosimulate çevrimdışı bir senaryo değiştirin. Veri öğeleri ekleyin veya değiştirildiğinde, bu değişiklikler yerel depoda tutulur, ancak hello bağlantı yeniden kurulur kurulmaz kadar eşitlenen toohello arka uç veri deposu olup olmadığı.

1. Çözüm Gezgini hello, hello index.js proje dosyasını açın ve koddan hello gibi geçersiz bir URL'ye hello uygulama URL'si toopoint değiştirin:

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net-fail');

2. Merhaba CSP index.HTML içinde güncelleştirme `<meta>` öğeyle hello aynı geçersiz URL.

        <meta http-equiv="Content-Security-Policy" content="default-src 'self' data: gap: http://yourmobileapp.azurewebsites.net-fail; style-src 'self'; media-src *">

3. Derleme ve hello istemci uygulamayı çalıştırın ve hello uygulama hello arka ucuyla oturum açtıktan sonra eşitleme girişiminde bulunduğunda bir özel durum hello konsolunda kaydedilir dikkat edin. Bunlar toohello mobil arka uç gönderilen kadar eklediğiniz tüm yeni öğeler hello yerel depoda yalnızca mevcut. Merhaba istemci uygulaması bağlı toohello arka uç olduğu gibi davranır.

4. Merhaba uygulamasını kapatın ve oluşturduğunuz hello yeni öğeler kalıcı toohello yerel deposu olduğunu tooverify yeniden başlatın.

5. (İsteğe bağlı) Visual Studio tooview hello arka uç veritabanı hello verilerde değişmediğini, Azure SQL veritabanı tablosu toosee kullanın.

    Visual Studio'da açın **Sunucu Gezgini**. Tooyour veritabanında gidin **Azure**->**SQL veritabanları**. Veritabanınıza sağ tıklatıp **SQL Server nesne Gezgini'nde Aç**. Şimdi tooyour SQL veritabanı tablosunda ve içeriği göz atabilirsiniz.

## <a name="optional-test-hello-reconnection-tooyour-mobile-backend"></a>(İsteğe bağlı) Test hello yeniden bağlanmayı tooyour mobil arka uç

Bu bölümde, çevrimiçi duruma gelmeye hello uygulama benzetim hello uygulama toohello mobil arka uç, yeniden bağlanın. Oturum açtığınızda, eşitlenen tooyour mobil arka uç verilerdir.

1. İndex.js yeniden açın ve hello uygulama URL'si geri yükleyin.
2. İndex.HTML yeniden açın ve hello CSP hello uygulama URL'SİNDE düzeltmek `<meta>` öğesi.
3. Yeniden oluşturma ve hello istemci uygulamasını çalıştırın. Merhaba uygulama toosync hello mobil uygulama arka ucu ile oturum açtıktan sonra çalışır. Hiçbir özel durum hello hata ayıklama konsolunda tutulduğunu doğrulayın.
4. (İsteğe bağlı) SQL Server Nesne Gezgini veya Fiddler gibi bir REST araç kullanarak veri görünümü hello güncelleştirildi. Bildirim hello veri hello arka uç veritabanı ve hello yerel deposu arasında eşitlendi.

    Merhaba veri hello yerel deposu hello veritabanı arasında eşitlenen ve uygulamanızı değilken eklediğiniz hello öğelerini içeren dikkat edin.

## <a name="additional-resources"></a>Ek kaynaklar
* [Azure Mobile Apps çevrimdışı veri eşitleme]
* [Apache Cordova için Visual Studio Araçları]

## <a name="next-steps"></a>Sonraki adımlar
* Çevrimdışı eşitleme özelliklerini hello çakışma çözümlemesinde gibi daha gelişmiş gözden [çevrimdışı eşitleme örnek]
* Gözden hello çevrimdışı eşitleme hello API başvuru [API belgelerine](https://azure.github.io/azure-mobile-apps-js-client).

<!-- ##Summary -->

<!-- Images -->

<!-- URLs. -->
[Apache Cordova Hızlı Başlangıç]: app-service-mobile-cordova-get-started.md
[çevrimdışı eşitleme örnek]: https://github.com/Azure-Samples/app-service-mobile-cordova-client-conflict-handling
[Azure Mobile Apps çevrimdışı veri eşitleme]: app-service-mobile-offline-data-sync.md
[Cloud Cover: Offline Sync in Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Adding Authentication]: app-service-mobile-cordova-get-started-users.md
[authentication]: app-service-mobile-cordova-get-started-users.md
[Work with hello .NET backend server SDK for Azure Mobile Apps]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Visual Studio Community 2015]: http://www.visualstudio.com/
[Apache Cordova için Visual Studio Araçları]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md
[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md
