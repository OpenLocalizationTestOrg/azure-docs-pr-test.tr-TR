---
title: "aaaEnable çevrimdışı eşitleme için Azure mobil uygulamanız (Android)"
description: "Bilgi nasıl toouse App Service Mobile Apps toocache ve eşitleme çevrimdışı veri Android uygulamanızdaki"
documentationcenter: android
author: ggailey777
manager: syntaxc4
services: app-service\mobile
ms.assetid: 32a8a079-9b3c-4faf-8588-ccff02097224
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 34508c7394610cf9127e1753637940826b8fd06a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-android-mobile-app"></a>Android mobil uygulamanızı için çevrimdışı eşitlemeyi etkinleştirme
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>Genel Bakış
Bu öğretici, Android için Azure Mobile Apps hello çevrimdışı eşitleme özelliği kapsar. Çevrimdışı eşitleme sağlayan bir mobil uygulama ile son kullanıcılar toointeract&mdash;görüntüleme, ekleme veya değiştirme veri&mdash;hiçbir ağ bağlantısı olduğunda bile. Değişiklikler yerel bir veritabanında depolanır. Merhaba aygıt yeniden çevrimiçi olduktan sonra bu değişiklikleri hello uzak arka uç ile eşitlenir.

İlk Azure Mobile Apps deneyiminizi varsa hello öğretici ilk tamamlanmalıdır [Android uygulaması oluşturma]. Kullanmıyorsanız, hızlı başlangıç sunucu projesi hello indirilen, hello veri erişim uzantı paketleri tooyour projesi eklemeniz gerekir. Server uzantısı paketleri hakkında daha fazla bilgi için bkz: [hello .NET arka uç sunucusu SDK ile Azure Mobile Apps için iş](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

Merhaba çevrimdışı eşitleme özelliği hakkında daha fazla toolearn hello konusuna bakın [Azure Mobile Apps çevrimdışı veri eşitleme].

## <a name="update-hello-app-toosupport-offline-sync"></a>Merhaba uygulama toosupport çevrimdışı eşitleme güncelleştir
Çevrimdışı Eşitleme ile tooand yazma'dan okuma bir *eşitleme tablo* (hello kullanarak *IMobileServiceSyncTable* arabirimi), parçası olduğu bir **SQLite** aygıtınızda veritabanı.

kullandığınız toopush ve çekme değişiklikleri hello cihaz ve Azure Mobile Services arasında bir *eşitleme bağlamı* (*MobileServiceClient.SyncContext*), hangi hello yerel veritabanını başlatılamadı toostore verilerini yerel olarak yükleyin.

1. İçinde `TodoActivity.java`, yorum hello varolan tanımını çıkışı `mToDoTable` ve hello eşitleme tablo sürümü açıklamadan çıkarın:
   
        private MobileServiceSyncTable<ToDoItem> mToDoTable;
2. Merhaba, `onCreate` yöntemi, yorum hello varolan başlatılması çıkışı `mToDoTable` ve bu tanımı açıklamadan çıkarın:
   
        mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
3. İçinde `refreshItemsFromTable` açıklama hello tanımını çıkışı `results` ve bu tanımı açıklamadan çıkarın:
   
        // Offline Sync
        final List<ToDoItem> results = refreshItemsFromMobileServiceTableSyncTable();
4. Açıklama hello tanımını çıkışı `refreshItemsFromMobileServiceTable`.
5. Merhaba tanımını açıklamadan çıkarın `refreshItemsFromMobileServiceTableSyncTable`:
   
        private List<ToDoItem> refreshItemsFromMobileServiceTableSyncTable() throws ExecutionException, InterruptedException {
            //sync hello data
            sync().get();
            Query query = QueryOperations.field("complete").
                    eq(val(false));
            return mToDoTable.read(query).get();
        }
6. Merhaba tanımını açıklamadan çıkarın `sync`:
   
        private AsyncTask<Void, Void, Void> sync() {
            AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
                @Override
                protected Void doInBackground(Void... params) {
                    try {
                        MobileServiceSyncContext syncContext = mClient.getSyncContext();
                        syncContext.push().get();
                        mToDoTable.pull(null).get();
                    } catch (final Exception e) {
                        createAndShowDialogFromTask(e, "Error");
                    }
                    return null;
                }
            };
            return runAsyncTask(task);
        }

## <a name="test-hello-app"></a>Test hello uygulama
Bu bölümde, üzerinde hello davranışı WiFi ile test ve sonra çevrimdışı bir senaryo WiFi toocreate açın.

Veri öğeleri eklediğinizde, hello basın kadar bunlar hello yerel SQLite mağaza, ancak değil eşitlenen toohello mobil hizmet tutulur **yenileme** düğmesi. Diğer uygulamalara veri eşitlenen toobe gerektiği zaman ilgili farklı gereksinimlere sahip, ancak tanıtım amacıyla bu öğreticide açıkça isteği hello kullanıcı vardır.

Bu düğmesine bastığınızda, yeni bir arka plan görevi başlatır. Önce tüm değişiklikleri toohello yerel deposu eşitleme bağlamı sonra Azure toohello yerel tablodan tüm çeken değiştirilen verileri kullanarak iter.

### <a name="offline-testing"></a>Çevrimdışı test etme
1. Yerleştir hello aygıt ya da benzeticisinde *uçak modu*. Bu, çevrimdışı bir senaryo doğurur.
2. Bazı eklemek *Yapılacaklar* öğeler veya bazı öğeler tamamlandı olarak işaretle. Merhaba cihaz veya benzetici (veya zorla kapatma hello uygulama) çıkmak ve yeniden başlatın. Tutuluyor çünkü değişikliklerinizi hello aygıtta devam ediyor olduğunu doğrulayın hello yerel SQLite deposunda.
3. Görüntüleme hello Azure Merhaba içeriğine *Todoıtem* SQL aracıyla ya da gibi tablo *SQL Server Management Studio*, veya REST istemcisi gibi *Fiddler* veya  *Postman*. Merhaba yeni öğelerin bulunduğunu doğrulayın *değil* eşitlenen toohello sunucu edildi
   
       + Node.js arka ucu için toohello Git [Azure portal](https://portal.azure.com/), tıklatıp mobil uygulamanızın arka uç **kolay tablolar** > **Todoıtem** hello tooviewMerhabaiçeriğine`TodoItem` tablo.
       + Bir .NET arka ucu için Görünüm hello tablosu bir SQL aracı ile ya da gibi içeriği *SQL Server Management Studio*, veya bir REST istemcisi gibi *Fiddler* veya *Postman*.
4. WiFi üzerinde hello aygıt ya da simulator açın. Ardından, hello'e basın **yenileme** düğmesi.
5. Merhaba Todoıtem verileri hello Azure portalında yeniden görüntüleyin. Merhaba yeni ve değiştirilmiş Todoıtems şimdi gösterilmelidir.

## <a name="additional-resources"></a>Ek Kaynaklar
* [Azure Mobile Apps çevrimdışı veri eşitleme]
* [Bulut kapsar: Azure Mobile Services'ın çevrimdışı eşitleme] \(Not: hello video Mobile Services'de olsa da, çevrimdışı eşitleme Azure Mobile Apps benzer şekilde çalışır\)

<!-- URLs. -->

[Azure Mobile Apps çevrimdışı veri eşitleme]: app-service-mobile-offline-data-sync.md

[Android uygulaması oluşturma]: app-service-mobile-android-get-started.md

[Bulut kapsar: Azure Mobile Services'ın çevrimdışı eşitleme]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/

