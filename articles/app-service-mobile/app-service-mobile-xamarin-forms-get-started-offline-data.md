---
title: "aaaEnable çevrimdışı eşitleme Azure mobil uygulamanızın (Xamarin.Forms) | Microsoft Docs"
description: "Bilgi nasıl toouse mobil uygulama hizmeti toocache ve eşitleme çevrimdışı veri Xamarin.Forms uygulamanızda"
documentationcenter: xamarin
author: ggailey777
manager: yochayk
editor: 
services: app-service\mobile
ms.assetid: acf0f874-3ea5-4410-bd22-b0e72140f3b5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/04/2016
ms.author: glenga
ms.openlocfilehash: 4b41404fc9507e82068fdf8aa612d57cbeb366bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-xamarinforms-mobile-app"></a>Xamarin.Forms mobil uygulamanız için çevrimdışı eşitlemeyi etkinleştirme
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>Genel Bakış
Bu öğretici Azure Mobile Apps hello çevrimdışı eşitleme özelliği için Xamarin.Forms tanıtır. Çevrimdışı eşitleme son kullanıcıların görüntüleme, ekleme veya ağ bağlantısı olduğunda bile veri--değiştirme bir mobil uygulamayla--etkileşime olanak sağlar. Değişiklikler yerel bir veritabanında depolanır. Merhaba aygıt yeniden çevrimiçi olduktan sonra bu değişiklikleri hello uzak hizmeti ile eşitlenir.

Bu öğretici hello Xamarin.Forms hızlı başlangıç çözüm üzerinde Mobile Apps için [bir Xamarin iOS uygulaması oluştur] öğreticiyi tamamladığınızda oluşturduğunuz temel alır. Xamarin.Forms Hello hızlı başlangıç çözüm yalnızca etkin toobe gereken hello kod toosupport çevrimdışı eşitleme, içerir. Bu öğreticide, hello hızlı başlangıç çözüm tooturn hello çevrimdışı Azure Mobile Apps özelliklerini üzerinde güncelleştirin. Biz de hello çevrimdışı özgü hello uygulama kodunda vurgulayın. Merhaba indirilen hızlı başlangıç çözümü kullanmıyorsanız hello veri erişim uzantı paketleri tooyour projesi eklemeniz gerekir. Server uzantısı paketleri hakkında daha fazla bilgi için bkz: [hello .NET arka uç sunucusu SDK ile Azure Mobile Apps için iş][1].

Merhaba çevrimdışı eşitleme özelliği hakkında daha fazla toolearn hello konusuna bakın [Azure Mobile Apps çevrimdışı veri eşitleme][2].

## <a name="enable-offline-sync-functionality-in-hello-quickstart-solution"></a>Çevrimdışı eşitleme işlevselliği hello hızlı başlangıç çözümde etkinleştir
Merhaba çevrimdışı eşitleme kod, C# önişlemci yönergeleri kullanarak hello projesinde eklenmiştir. Ne zaman hello **çevrimdışı\_eşitleme\_etkin** simgesiyle tanımlanır, bu kod yolları hello derlemede dahil edilir. Windows uygulamaları için hello SQLite platform de yüklemeniz gerekir.

1. Visual Studio'da hello çözüme sağ tıklayın > **çözüm için NuGet paketlerini Yönet...** , ardından arayın ve yükleyin **Microsoft.Azure.Mobile.Client.SQLiteStore** hello Çözümdeki tüm projeleri için NuGet paketi.
2. Hello Çözüm Gezgini, ile Merhaba projenizden hello Todoıtemmanager.cs dosyasını açın **taşınabilir** taşınabilir sınıf kitaplığı proje olan hello ad sonra önişlemci yönergesi aşağıdaki hello açıklamadan çıkarın:

        #define OFFLINE_SYNC_ENABLED
3. (İsteğe bağlı) toosupport Windows cihazları, SQLite çalışma zamanı paketleri aşağıdaki hello birini yükleyin:

   * **Windows 8.1 çalışma zamanı:** yükleme [Windows 8.1 için SQLite][3].
   * **Windows Phone 8.1:** yükleme [Windows Phone 8.1 için SQLite][4].
   * **Evrensel Windows platformu** yükleme [hello Evrensel Windows Evrensel SQLite][5].

     Merhaba quickstart Evrensel Windows projesi içermiyor rağmen hello Evrensel Windows platformu Xamarin Forms ile desteklenir.
4. (İsteğe bağlı) Her Windows uygulama projesine sağ **başvuruları** > **Başvuru Ekle...** , hello genişletin **Windows** klasörü > **uzantıları**.
    Merhaba uygun etkinleştirmek **SQLite for Windows** SDK ile birlikte hello **için Visual C++ 2013 çalışma zamanı Windows** SDK.
    Merhaba SQLite SDK adları biraz her Windows platformuyla farklılık gösterir.

## <a name="review-hello-client-sync-code"></a>Merhaba istemci eşitleme kodu gözden geçirme
Zaten hello Eğitmen kodu hello içinde içereceği kısa genel bakış işte `#if OFFLINE_SYNC_ENABLED` yönergeleri. Çevrimdışı eşitleme hello Todoıtemmanager.cs proje hello taşınabilir sınıf kitaplığı proje dosyasında bir işlevdir. Merhaba özelliği kavramsal bir genel bakış için bkz: [çevrimdışı veri eşitlemeye Azure Mobile Apps içinde][2].

* Tablo işlemleri gerçekleştirilmeden önce hello yerel depolama başlatılmalıdır. Merhaba yerel deposu veritabanı hello başlatılmış **TodoItemManager** koddan hello kullanarak sınıfı oluşturucusu:

        var store = new MobileServiceSQLiteStore(OfflineDbPath);
        store.DefineTable<TodoItem>();

        //Initializes hello SyncContext using hello default IMobileServiceSyncHandler.
        this.client.SyncContext.InitializeAsync(store);

        this.todoTable = client.GetSyncTable<TodoItem>();

    Bu kod hello kullanarak yeni bir yerel SQLite veritabanı oluşturur **MobileServiceSQLiteStore** sınıfı.

    Merhaba **DefineTable** yöntemi, sağlanan hello türündeki hello alanlar eşleşen hello yerel deposunda bir tablo oluşturur.  Merhaba türü tooinclude hello uzak veritabanındaki tüm hello sütunları yok. Bu, olası toostore bir sütun alt kümesi olur.
* Merhaba **todoTable** alanındaki **TodoItemManager** olan bir **IMobileServiceSyncTable** yerine tür **IMobileServiceTable**. Sınıfı bu kullanır hello yerel veritabanı tüm oluşturmak okuyun, Güncelleştir ve Sil (CRUD) tablo işlemleri. Ne zaman bu değişiklikleri toohello mobil uygulama arka ucu çağırarak gönderilen karar **PushAsync** hello üzerinde **IMobileServiceSyncContext**. Merhaba eşitleme bağlamı tablo ilişkileri izleme ve bir istemci uygulaması değiştiren tüm tablolarda değişiklikleri Ftp'den korunmasına yardımcı olur **PushAsync** olarak adlandırılır.

    Merhaba aşağıdaki **SyncAsync** yöntemi toosync hello mobil uygulama arka ucu ile çağrılır:

        public async Task SyncAsync()
        {
            ReadOnlyCollection<MobileServiceTableOperationError> syncErrors = null;

            try
            {
                await this.client.SyncContext.PushAsync();

                await this.todoTable.PullAsync(
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

            // Simple error/conflict handling.
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

                    Debug.WriteLine(@"Error executing sync operation. Item: {0} ({1}). Operation discarded.",
                        error.TableName, error.Item["id"]);
                }
            }
        }

    Bu örnekte basit hata hello varsayılan eşitleme işleyiciyle işleme kullanır. Gerçek bir uygulamada ağ koşulları ve sunucu gibi çeşitli hatalar çakışmaları özel kullanarak hello işlemek **IMobileServiceSyncHandler** uygulaması.

## <a name="offline-sync-considerations"></a>Çevrimdışı eşitleme konuları
Merhaba örnek hello **SyncAsync** yöntemi yalnızca adlı başlatma ve ne zaman bir eşitleme istedi.  bir Android veya iOS uygulama hello öğeler listesindeki açılır menüsünden bir eşitleme tooinitiate; Windows için hello kullanma **eşitleme** düğmesi. Gerçek dünya uygulamada Hello ağ durumu değiştiğinde hello eşitleme tetikleyici de yapabilirsiniz.

Bir çekme beklemede olan bir tabloda karşı çalıştırıldığında yerel güncelleştirmeleri önceki bağlam push işlemi otomatik olarak Tetikleyicileri çekme hello bağlam tarafından izlenen. Yenileme, ekleme ve bu örnek öğelerde Tamamlanıyor, atlayabilirsiniz olduğunda açık hello **PushAsync** çağırın.

Sağlanan hello kodda hello uzak Todoıtem tablosu tüm kayıtları seçmeleri istenir, ancak bu da olası toofilter kayıtları sorgu kimliği ve sorgu geçirerek çok**PushAsync**. Daha fazla bilgi için hello bölümüne bakın *Artımlı eşitleme* içinde [çevrimdışı veri eşitlemeye Azure Mobile Apps içinde][2].

## <a name="run-hello-client-app"></a>Merhaba istemci uygulaması çalıştırın
Şu anda etkin çevrimdışı eşitleme ile Merhaba istemci uygulaması her platform toopopulate hello yerel deposu veritabanı üzerinde en az bir kez çalıştırın. Daha sonra çevrimdışı bir senaryo benzetimini hello uygulama çevrimdışı durumdayken hello verileri ve hello Yerel Depodaki değiştirebilirsiniz.

## <a name="update-hello-sync-behavior-of-hello-client-app"></a>Merhaba istemci uygulamanın Hello eşitleme davranışı güncelleştir
Bu bölümde, hello istemci projesi toosimulate çevrimdışı bir senaryo arka ucunuz için geçersiz uygulama URL'si kullanarak değiştirin. Alternatif olarak, Cihazınızı çok taşıyarak ağ bağlantıları devre dışı dışı bırakabilirsiniz "Uçak modu."  Veri öğeleri ekleyin veya değiştirildiğinde, bu değişiklikleri hello yerel deposunda tutulan, ancak eşitlenmedi toohello arka uç veri depolamak hello bağlantı yeniden kurulur kurulmaz kadar.

1. Hello Çözüm Gezgini, hello hello Constants.cs proje dosyasını açın **taşınabilir** proje ve hello değerini değiştirin `ApplicationURL` toopoint tooan geçersiz URL:

        public static string ApplicationURL = @"https://your-service.azurewebsites.net/";
2. Açık hello Todoıtemmanager.cs hello dosyasından **taşınabilir** proje ardından ekleyin bir **catch** hello temel için **özel durum** sınıfı toohello **try... catch** engelleyin **SyncAsync**. Bu **catch** blok hello özel durum iletisi toohello konsolu gibi Yazar:

            catch (Exception ex)
            {
                Console.Error.WriteLine(@"Exception: {0}", ex.Message);
            }
3. Derleme ve hello istemci uygulamasını çalıştırın.  Bazı yeni öğeleri ekleyin. Bir özel durum her girişimi toosync hello arka ucu ile için hello konsolunda kaydedilir dikkat edin. Toohello mobil arka uç gönderilemez kadar bu yeni öğeler hello yerel depoda yalnızca mevcut. Bu gibi bağlı toohello arka uç, tüm oluşturma, okuma destekleyen, güncelleştirme, Sil (CRUD) işlemleri hello istemci uygulaması davranır.
4. Merhaba uygulamasını kapatın ve oluşturduğunuz hello yeni öğeler kalıcı toohello yerel deposu olduğunu tooverify yeniden başlatın.
5. (İsteğe bağlı) Visual Studio tooview hello arka uç veritabanı hello verilerde değişmediğini, Azure SQL veritabanı tablosu toosee kullanın.

    Visual Studio'da açın **Sunucu Gezgini**. Tooyour veritabanında gidin **Azure**->**SQL veritabanları**. Veritabanınıza sağ tıklatıp **SQL Server nesne Gezgini'nde Aç**. Şimdi tooyour SQL veritabanı tablosunda ve içeriği göz atabilirsiniz.

## <a name="update-hello-client-app-tooreconnect-your-mobile-backend"></a>Mobil arka Hello istemci uygulaması tooreconnect güncelleştir
Bu bölümde, hangi tooan çevrimiçi duruma gelmeye hello uygulama benzetim hello uygulama toohello mobil arka uç, yeniden bağlanın. Merhaba yenileme hareketi gerçekleştirdiğinizde, eşitlenen tooyour mobil arka uç verilerdir.

1. Constants.cs yeniden açın. Doğru hello `applicationURL` toopoint toohello URL düzeltin.
2. Yeniden oluşturma ve hello istemci uygulamasını çalıştırın. Merhaba uygulama başlatıldıktan sonra toosync hello mobil uygulama arka ucu ile çalışır. Hiçbir özel durum hello hata ayıklama konsolunda tutulduğunu doğrulayın.
3. (İsteğe bağlı) Görünüm hello güncelleştirilmiş verileri SQL Server Nesne Gezgini veya Fiddler gibi bir REST araç kullanarak veya [Postman][6]. Bildirim hello veri hello arka uç veritabanı ve hello yerel deposu arasında eşitlendi.

    Merhaba veri hello yerel deposu hello veritabanı arasında eşitlenen ve uygulamanızı değilken eklediğiniz hello öğelerini içeren dikkat edin.

## <a name="additional-resources"></a>Ek Kaynaklar
* [Azure Mobile Apps çevrimdışı veri eşitleme][2]
* [Azure Mobile Apps .NET SDK'sı nasıl yapılır][8]

<!-- URLs. -->
[1]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[2]: app-service-mobile-offline-data-sync.md
[3]: http://go.microsoft.com/fwlink/p/?LinkID=716919
[4]: http://go.microsoft.com/fwlink/p/?LinkID=716920
[5]: http://sqlite.org/2016/sqlite-uwp-3120200.vsix
[6]: https://www.getpostman.com/
[7]: http://www.telerik.com/fiddler
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
