---
title: "Azure işlevleri için aaaStream Analytics gerçek zamanlı işleme | Microsoft Docs"
description: "Bir hizmet veri yolu kuyruğu toopopulate bir Azure Redis önbelleği Stream Analytics işi hello çıktısından toouse bir Azure işlevi nasıl bağlanacağını öğrenin."
keywords: "veri akışı, redis önbelleği, hizmet veri yolu kuyruğu"
services: stream-analytics
author: ryancrawcour
manager: jhubbard
documentationcenter: 
ms.assetid: d428bb33-4244-4001-b93d-c77bed816527
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/28/2017
ms.author: ryancraw
ms.openlocfilehash: 5ef4fe76c2cadf896a80eeaf421f010c315918af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toostore-data-from-azure-stream-analytics-in-an-azure-redis-cache-using-azure-functions"></a>Nasıl bir Azure Redis Azure işlevleri kullanarak önbelleğinde Azure akış analizi toostore verileri
Azure Stream Analytics, hızlı bir şekilde geliştirmek ve düşük maliyetli çözümleri toogain gerçek zamanlı Öngörüler cihazlar, algılayıcılar, altyapı ve uygulamaları ya da veri dağıtmanıza olanak tanır. Gerçek zamanlı yönetim ve izleme, komut ve denetim, sahtekarlık algılama, bağlı araba ve çok daha fazlasını gibi çeşitli kullanım örnekleri sağlar. Bu tür birçok senaryoda, bir Azure Redis önbelleği gibi dağıtılmış veri deposuna Azure akış analizi tarafından yüzdelik toostore veri isteyebilirsiniz.

Telekomünikasyon şirket parçası olan varsayalım. Burada'ten gelen birden fazla çağrı hello aynı kimlik toodetect SIM sahtekarlık çalıştığınız, adresindeki aynı Merhaba, fakat coğrafi olarak farklı zaman konumları. Bir Azure Redis Önbelleği'nde tüm hello olası sahte telefon aramaları depolamanın görevli. Bu Web Günlüğü'ndeki, nasıl kolayca göreviniz tamamlayabileceğiniz üzerinde size rehberlik sağlar. 

## <a name="prerequisites"></a>Ön koşullar
Tam hello [gerçek zamanlı sahtekarlık algılama] [ fraud-detection] ASA için gözden geçirme

## <a name="architecture-overview"></a>Mimarisine genel bakış
![Ekran görüntüsü mimarisi](./media/stream-analytics-functions-redis/architecture-overview.png)

Şekil önceki hello gösterildiği gibi Stream Analytics giriş verisi toobe akış sorgulanan ve tooan çıktı gönderilen sağlar. Azure işlevleri, Hello çıktıya dayalı, sonra herhangi bir tür olay tetikleyebilir. 

Bu blogdaki Biz bu ardışık hello Azure işlevleri Bölümü'odak veya daha açık belirtmek gerekirse hello önbelleğine sahte verileri depolayan bir olay tetikleme hello.
Merhaba tamamladıktan sonra [gerçek zamanlı sahtekarlık algılama] [ fraud-detection] öğretici, elinizde bir giriş (bir event hub), bir sorgu ve önceden yapılandırılmış ve çalışan bir çıkış (blob depolama). Bu Web Günlüğü'ndeki biz hello çıktı toouse bir hizmet veri yolu kuyruğu bunun yerine değiştirin. Bundan sonra size bir Azure işlevi toothis sıra bağlayın. 

## <a name="create-and-connect-a-service-bus-queue-output"></a>Oluşturma ve bir hizmet veri yolu kuyruğu çıkış bağlama
toocreate bir hizmet veri yolu kuyruğu adımları 1 ve 2'ın hello .NET bölümü [hizmet veri yolu kuyrukları ile çalışmaya başlama][servicebus-getstarted].
Şimdi şimdi hello oluşturulduğu hello sıra toohello Stream Analytics işi bağlanmak önceki sahtekarlık algılama gözden geçirme.

1. Toohello Hello Azure portal, Git **çıkışları** seçin ve iş dikey **Ekle** hello sayfanın üst kısmındaki hello.
   
    ![Çıkış ekleme](./media/stream-analytics-functions-redis/adding-outputs.png)
2. Seçin **hizmet veri yolu kuyruğu** hello olarak **havuzu** ve Merhaba ekranında hello yönergeleri izleyin. Olması emin toochoose hello ad alanı hello hizmet veri yolu kuyruğu oluşturduğunuz [hizmet veri yolu kuyrukları ile çalışmaya başlama][servicebus-getstarted]. İşiniz bittiğinde hello "sağ" düğmesini tıklatın.
3. Hello aşağıdaki değerleri belirtin:
   
   * **Olayı seri hale getirici biçimi**: JSON
   * **Kodlama**: UTF8
   * **Biçim**: ayrılmış çizgi
4. Merhaba tıklatın **oluşturma** tooadd bu kaynak ve akış analizi toohello depolama hesabı başarıyla bağlanabildiğinizi tooverify düğme.
5. Merhaba, **sorgu** sekmesinde, hello geçerli sorgu hello şununla değiştirin. Değiştir * [YOUR hizmet veri yolu adı] * 3. adımda oluşturduğunuz hello çıkış ada sahip. 
   
    ```    
   
        SELECT 
            System.Timestamp as Time, CS1.CallingIMSI, CS1.CallingNum as CallingNum1, 
            CS2.CallingNum as CallingNum2, CS1.SwitchNum as Switch1, CS2.SwitchNum as Switch2
   
        INTO [YOUR SERVICE BUS NAME]
   
        FROM CallStream CS1 TIMESTAMP BY CallRecTime
        JOIN CallStream CS2 TIMESTAMP BY CallRecTime
            ON CS1.CallingIMSI = CS2.CallingIMSI AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5
   
        WHERE CS1.SwitchNum != CS2.SwitchNum
   
    ```

## <a name="create-an-azure-redis-cache"></a>Azure Redis Cache oluşturma
Hello .NET bölümünde izleyerek bir Azure Redis önbelleği oluşturma [nasıl tooUse Azure Redis önbelleği] [ use-rediscache] hello bölüm adlı kadar ***hello önbellek istemcilerini yapılandırın***.
Tamamlandıktan sonra yeni bir Redis önbelleği sahip. Altında **tüm ayarları**seçin **erişim anahtarları** ve hello Not ***birincil bağlantı dizesi***.

![Ekran görüntüsü mimarisi](./media/stream-analytics-functions-redis/redis-cache-keys.png)

## <a name="create-an-azure-function"></a>Bir Azure işlevi oluşturma
İzleyin [ilk Azure işlevinizi oluşturma] [ functions-getstarted] öğretici tooget Azure işlevleri ile başlatıldı. İster toouse sonra İleri çok atlayabilirsiniz bir Azure işlevi zaten varsa[tooRedis önbellek yazma](#Writing-to-Redis-Cache)

1. Merhaba portal hello sol gezinti bölmesinden uygulama Hizmetleri'ni seçin ve ardından, Azure işlevi uygulama adı tooget toohello işlevin app Web sitesi tıklayın.
    ![Uygulama Hizmetleri işlevi listesinin ekran görüntüsü](./media/stream-analytics-functions-redis/app-services-function-list.png)
2. Tıklatın **yeni işlev > ServiceBusQueueTrigger – C#**. Aşağıdaki alanları Hello için bu yönergeleri izleyin:
   
   * **Kuyruk adı**: aynı adı hello sırada oluşturduğunuzda girdiğiniz hello adı olarak hello [hizmet veri yolu kuyrukları ile çalışmaya başlama] [ servicebus-getstarted] (Merhaba hizmet veri yolu hello adı değil). Stream Analytics çıktı bağlı toohello hello sırasına kullandığınızdan emin olun.
   * **Hizmet veri yolu bağlantı**: seçin **bir bağlantı dizesi eklemek**. toofind hello bağlantı dizesi, Git toohello Klasik portal seçin **Service Bus**, Merhaba, oluşturduğunuz hizmet veri yolu ve **bağlantı bilgilerini** Merhaba ekranında hello sonundaki. Bu sayfada ana Merhaba ekranında olduğundan emin olun. Kopyalama ve hello bağlantı dizesini yapıştırın. Ücretsiz tooenter herhangi bir bağlantı adı eşitleyerek.
     
       ![Hizmet veri yolu bağlantı ekran görüntüsü](./media/stream-analytics-functions-redis/servicebus-connection.png)
   * **ErişimHakları**: seçin **yönetme**
3. **Oluştur**'a tıklayın

## <a name="writing-tooredis-cache"></a>Yazma tooRedis önbelleği
Artık Service Bus kuyruğundaki iletileri okuyan bir Azure işlevi oluşturduk. Tüm toodo sol özelliği bu veri toohello Redis önbelleği bizim işlevi toowrite kullanın. 

1. Yeni oluşturduğunuz seçin **ServiceBusQueueTrigger**, tıklatıp **işlev uygulaması ayarları** hello sağ üst köşedeki üzerinde. Seçin **Git tooApp hizmet ayarları > Ayarlar > Uygulama ayarları**
2. Hello bağlantı dizeleri bölümü, hello bir ad oluşturmak **adı** bölümü. Yapıştırma hello birincil bağlantı dizesi hello bulunamadı **Redis önbelleği oluşturma** hello adımla **değeri** bölümü. Seçin **özel** burada yazacaktır **SQL veritabanı**.
3. Tıklatın **kaydetmek** hello üstünde.
   
    ![Hizmet veri yolu bağlantı ekran görüntüsü](./media/stream-analytics-functions-redis/function-connection-string.png)
4. Şimdi toohello uygulama hizmet ayarlarını geri dönün ve seçin **Araçlar > uygulama hizmeti Düzenleyicisi'ni (Önizleme) > üzerinde > Git**.
   
    ![Hizmet veri yolu bağlantı ekran görüntüsü](./media/stream-analytics-functions-redis/app-service-editor.png)
5. Tercih ettiğiniz bir düzenleyicide adlı bir JSON dosyası oluşturun **project.json** ile aşağıdaki hello ve tooyour yerel diske kaydedin.
   
        {
            "frameworks": {
                "net46": {
                    "dependencies": {
                        "StackExchange.Redis":"1.1.603",
                        "Newtonsoft.Json": "9.0.1"
                    }
                }
            }
        }
6. Bu dosya, işlevin (değil WWWROOT) kök dizine hello karşıya yükleyin. Adlı bir dosya görmelisiniz **böylece project.lock.json** otomatik olarak görüntülenmiyorsa, o hello Nuget onaylayan "StackExchange.Redis" ve "Newtonsoft.Json" paketleri içeri aktarıldığını.
7. Merhaba, **run.csx** dosya, hello önceden oluşturulan kodu koddan hello ile değiştirin. 2. adımda oluşturulan hello adıyla "Bağlantı adı" Merhaba lazyConnection işlevinde değiştirin **veri hello Redis önbelleğine depolamak**.

````

    using System;
    using System.Threading.Tasks;
    using StackExchange.Redis;
    using Newtonsoft.Json;
    using System.Configuration;

    public static void Run(string myQueueItem, TraceWriter log)
    {
        log.Info($"Function processed message: {myQueueItem}");

        // Connection refers tooa property that returns a ConnectionMultiplexer
        IDatabase db = Connection.GetDatabase();
        log.Info($"Created database {db}");

        // Parse JSON and extract hello time
        var message = JsonConvert.DeserializeObject<dynamic>(myQueueItem);
        string time = message.time;
        string callingnum1 = message.callingnum1;

        // Perform cache operations using hello cache object...
        // Simple put of integral data types into hello cache
        string key = time + " - " + callingnum1;
        db.StringSet(key, myQueueItem);
        log.Info($"Object put in database. Key is {key} and value is {myQueueItem}");

        // Simple get of data types from hello cache
        string value = db.StringGet(key);
        log.Info($"Database got: {value}"); 
    }

    // Connect toohello Service Bus
    private static Lazy<ConnectionMultiplexer> lazyConnection = 
        new Lazy<ConnectionMultiplexer>(() =>
            {
                var cnn = ConfigurationManager.ConnectionStrings["CONN NAME"].ConnectionString
                return ConnectionMultiplexer.Connect();
            });

    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }

````

## <a name="start-hello-stream-analytics-job"></a>Merhaba Stream Analytics işi Başlat
1. Merhaba telcodatagen.exe uygulaması başlatın. Merhaba kullanım aşağıdaki gibidir:````telcodatagen.exe [#NumCDRsPerHour] [SIM Card Fraud Probability] [#DurationHours]````
2. Merhaba portalında Hello akış analizi işi dikey penceresinden tıklayın **Başlat** hello sayfanın üst kısmındaki hello.
   
    ![Başlangıç işi ekran görüntüsü](./media/stream-analytics-functions-redis/starting-job.png)
3. Merhaba, **başlangıç işi** görünür, dikey seçin **şimdi** ve hello ardından **Başlat** hello ekranın hello düğmesini. Merhaba iş durumu tooStarting değiştirir ve bazı değişiklikler tooRunning saat sonra.
   
    ![Başlatma işi zaman seçimi ekran görüntüsü](./media/stream-analytics-functions-redis/start-job-time.png)

## <a name="run-solution-and-check-results"></a>Çözümü çalıştırmak ve sonuçları denetleyin
Tooyour geri dönerseniz **ServiceBusQueueTrigger** sayfasında, görmelisiniz oturum deyimleri. Bu günlükler hello veritabanına put hello hizmet veri yolu kuyruğu, gelen bir şey var ve başlangıç anahtarı olarak hello zaman kullanarak getirilen Göster!

verilerinizi, Redis önbelleğinde olan tooverify hello yeni Portalı'nda tooyour Redis önbelleği sayfasına gidin (Merhaba önceki gösterildiği gibi [bir Azure Redis önbelleği oluşturma](#Create-an-Azure-Redis-Cache) adım) ve konsol seçin.

Şimdi veri aslında hello önbelleğinde olduğunu Redis komutları tooconfirm yazabilirsiniz.

![Redis konsolunun ekran görüntüsü](./media/stream-analytics-functions-redis/redis-console.png)

## <a name="next-steps"></a>Sonraki adımlar
Biz hello yeni şey Azure işlevleri hakkında Çoğalması akış analizi birlikte yapabilirsiniz ve bu yeni olanaklar sizin için kilidini açarak umuyoruz. Sonraki istediğiniz üzerinde hiçbir görüş bildirmek isterseniz, ücretsiz toouse hello eşitleyerek [Azure UserVoice sitesinde](https://feedback.azure.com/forums/270577-stream-analytics).

Yeni Microsoft Azure varsa, tootry davet ediyoruz uzaklaştırmak için imzalama tarafından bir [ücretsiz Azure deneme hesabı](https://azure.microsoft.com/pricing/free-trial/). Yeni tooStream Analytics olduğunuz sonra çok davet ediyoruz[ilk Stream Analytics işi oluşturmak](stream-analytics-create-a-job.md).

Herhangi bir gereksinim duyarsanız Yardım veya sorularınız varsa, ileti [MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) veya [Stackoverflow](http://stackoverflow.com/questions/tagged/azure-stream-analytics) forumlar. 

Kaynakları aşağıdaki hello de görebilirsiniz:

* [Azure İşlevleri geliştirici başvurusu](../azure-functions/functions-reference.md)
* [Azure işlevleri C# Geliştirici Başvurusu](../azure-functions/functions-reference-csharp.md)
* [Azure işlevleri F # Geliştirici Başvurusu](../azure-functions/functions-reference-fsharp.md)
* [Azure işlevleri NodeJS Geliştirici Başvurusu](../azure-functions/functions-reference.md)
* [Azure işlevleri Tetikleyicileri ve bağlamaları](../azure-functions/functions-triggers-bindings.md)
* [Nasıl toomonitor Azure Redis önbelleği](../redis-cache/cache-how-to-monitor.md)

Tüm hello en son haberleri ve özellikleri, güncel toostay izleyin [ @AzureStreaming ](https://twitter.com/AzureStreaming) Twitter'da.

[fraud-detection]: stream-analytics-real-time-fraud-detection.md
[servicebus-getstarted]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[use-rediscache]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md
[functions-getstarted]: ../azure-functions/functions-create-first-azure-function.md
