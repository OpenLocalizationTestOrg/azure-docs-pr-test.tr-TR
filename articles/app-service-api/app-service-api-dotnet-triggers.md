---
title: "aaaApp Service API uygulaması Tetikleyicileri | Microsoft Docs"
description: "Azure App Service'deki bir API uygulamasında tooimplement nasıl tetikler"
services: logic-apps
documentationcenter: .net
author: guangyang
manager: erikre
editor: jimbe
ms.assetid: 493c3703-786d-4434-9dca-8f77744b2f5d
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 08/25/2016
ms.author: rachelap
ms.openlocfilehash: 2d6b6a942a23c0a93987e9c48b69ecc739bfd814
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-api-app-triggers"></a>Azure App Service API uygulaması tetikleyicileri
> [!NOTE]
> Merhaba makalenin bu sürümü tooAPI apps 2014-12-01-Önizleme şema sürümü geçerlidir.
>
>

## <a name="overview"></a>Genel Bakış
Bu makalede nasıl tooimplement API uygulaması tetikler ve mantığı uygulamadan tüketen açıklanmaktadır.

Bu konudaki hello kod parçacıkları tümünün hello kopyalanır [FileWatcher API uygulaması kod örneği](http://go.microsoft.com/fwlink/?LinkId=534802).

Bu makale toobuild hello kodda için nuget paketi aşağıdaki ve çalıştırma toodownload hello gerekir Not: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).

## <a name="what-are-api-app-triggers"></a>API uygulaması Tetikleyicileri nelerdir?
Bir API uygulaması toofire bir olay için yaygın bir senaryo, böylelikle istemcilerin hello API uygulamasının yanıt toohello olayında hello uygun eylemi alabilir. Merhaba, bu senaryoyu destekler REST API'si mekanizması bir API uygulaması Tetikleyici adı verilir.

Örneğin, istemci kodunuzun hello kullanarak diyelim ki [Twitter Bağlayıcısı API uygulaması](../connectors/connectors-create-api-twitter.md) ve kodunuzu bir eylem dayalı belirli sözcükleri içeren yeni tweet'leri üzerinde tooperform gerekiyor. Bu durumda, bir yoklama ya da anında iletme tetikleyici toofacilitate bu gereksinimi ayarlayabilir.

## <a name="poll-trigger-versus-push-trigger"></a>Yoklama tetikleyici itme tetikleyici karşılaştırması
İki tür tetikleyici sunucusu şu anda desteklenir:

* Yoklama tetikleyici - istemci hello API uygulaması harekete bir olay bildirim için yoklar.
* Bir olay başlatıldığında itme tetikleyici - istemci hello API uygulaması tarafından bildirilir

### <a name="poll-trigger"></a>Yoklama tetikleyici
Yoklama tetikleyici normal bir REST API uygulanır ve kendi istemcilerinin (örneğin, bir mantıksal uygulama) toopoll bekliyor sipariş tooget bildirimi içinde. Merhaba istemci durumunu korumak, ancak hello yoklama tetikleyici kendisini durum bilgisiz.

Karşılama istek ve yanıt paketleri ile ilgili bilgiler aşağıdaki hello hello yoklama tetikleyici sözleşme anahtar bazı yönleri gösterilmiştir:

* İstek
  * HTTP yöntemini: Al
  * Parametreler
    * triggerState - Bu isteğe bağlı parametre istemcilerinin sağlar durumlarına yoklama tetikleyici hello şekilde yapabilirsiniz düzgün toospecify karar tooreturn bildirim veya temel alınarak hello durumu belirtilen.
    * API özel parametreler
* Yanıt
  * Durum kodu **200** - istek geçerli ve hello tetikleyici bildirimden yoktur. Merhaba bildirim Merhaba içeriğine hello yanıt gövdesi olacaktır. Ek bildirim verileri bir sonraki istek çağrısı ile alınması gereken bir "Yeniden deneme-sonra" üstbilgisi hello yanıt gösterir.
  * Durum kodu **202** - istek geçerlidir, ancak hello tetikleyici öğesinden yeni bildirim yoktur.
  * Durum kodu **4xx** -isteği geçerli değil. Merhaba istemci hello isteği yeniden.
  * Durum kodu **5xx** -isteği bir iç sunucu hatası ve/veya geçici bir sorun içinde sonuçlandı. Merhaba istemci hello isteği yeniden denemeniz gerekir.

Aşağıdaki kod parçacığını hello nasıl tooimplement bir yoklama tetikleyen bir örnektir.

    // Implement a poll trigger.
    [HttpGet]
    [Route("api/files/poll/TouchedFiles")]
    public HttpResponseMessage TouchedFilesPollTrigger(
        // triggerState is a UTC timestamp
        string triggerState,
        // Additional parameters
        string searchPattern = "*")
    {
        // Check toosee whether there is any file touched after hello timestamp.
        var lastTriggerTimeUtc = DateTime.Parse(triggerState).ToUniversalTime();
        var touchedFiles = Directory.EnumerateFiles(rootPath, searchPattern, SearchOption.AllDirectories)
            .Select(f => FileInfoWrapper.FromFileInfo(new FileInfo(f)))
            .Where(fi => fi.LastAccessTimeUtc > lastTriggerTimeUtc);

        // If there are files touched after hello timestamp, return their information.
        if (touchedFiles != null && touchedFiles.Count() != 0)
        {
            // Extension method provided by hello AppService service SDK.
            return this.Request.EventTriggered(new { files = touchedFiles });
        }
        // If there are no files touched after hello timestamp, tell hello caller toopoll again after 1 mintue.
        else
        {
            // Extension method provided by hello AppService service SDK.
            return this.Request.EventWaitPoll(new TimeSpan(0, 1, 0));
        }
    }

tootest bu yoklama tetiklemek, şu adımları izleyin:

1. Merhaba API uygulaması bir kimlik doğrulama ayarı ile dağıtmak **ortak anonim**.
2. Merhaba çağrısı **touch** işlemi tootouch bir dosya. Görüntü aşağıdaki hello örnek istek Postman aracılığıyla gösterir.
   ![Postman aracılığıyla dokunma işlem çağırma](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)
3. Merhaba yoklama hello tetikleyiciyle çağrısı **triggerState** parametre tooa zaman damgası önceki tooStep #2. Merhaba aşağıdaki görüntüde hello örnek istek Postman aracılığıyla gösterir.
   ![Postman aracılığıyla çağrı yoklama tetikleyici](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)

### <a name="push-trigger"></a>Tetikleyici bildirme
Anında iletme tetikleyicinin belirli olay tetiklendiğinde bildirim toobe kaydolan bildirimleri tooclients iter normal bir REST API uygulanır.

Karşılama istek ve yanıt paketleri ile ilgili bilgiler aşağıdaki hello hello itme tetikleyici sözleşme anahtar bazı yönleri gösterilmiştir.

* İstek
  * HTTP yöntemini: YERLEŞTİRME
  * Parametreler
    * Tetikleyici No: gerekli - opak dize (GUID gibi) gösteren bir itme tetikleyici kaydını hello.
    * callbackUrl: gerekli - hello olay başlatıldığında hello geri çağırma tooinvoke URL'si. Merhaba, basit bir POST HTTP çağrısıyla çağrıdır.
    * API özel parametreler
* Yanıt
  * Durum kodu **200** -istek tooregister istemci başarılı.
  * Durum kodu **4xx** -isteği geçerli değil. Merhaba istemci hello isteği yeniden.
  * Durum kodu **5xx** -isteği bir iç sunucu hatası ve/veya geçici bir sorun içinde sonuçlandı. Merhaba istemci hello isteği yeniden denemeniz gerekir.
* Geri çağırma
  * HTTP yöntemini: POST
  * İstek gövdesindeki: bildirim içeriği.

Aşağıdaki kod parçacığını hello nasıl tooimplement push tetikleyen bir örnektir:

    // Implement a push trigger.
    [HttpPut]
    [Route("api/files/push/TouchedFiles/{triggerId}")]
    public HttpResponseMessage TouchedFilesPushTrigger(
        // triggerId is an opaque string.
        string triggerId,
        // A helper class provided by hello AppService service SDK.
        // Here it defines hello input of hello push trigger is a string and hello output toohello callback is a FileInfoWrapper object.
        [FromBody]TriggerInput<string, FileInfoWrapper> triggerInput)
    {
        // Register hello trigger toosome trigger store.
        triggerStore.RegisterTrigger(triggerId, rootPath, triggerInput);

        // Extension method provided by hello AppService service SDK indicating hello registration is completed.
        return this.Request.PushTriggerRegistered(triggerInput.GetCallback());
    }

    // A simple in-memory trigger store.
    public class InMemoryTriggerStore
    {
        private static InMemoryTriggerStore instance;

        private IDictionary<string, FileSystemWatcher> _store;

        private InMemoryTriggerStore()
        {
            _store = new Dictionary<string, FileSystemWatcher>();
        }

        public static InMemoryTriggerStore Instance
        {
            get
            {
                if (instance == null)
                {
                    instance = new InMemoryTriggerStore();
                }
                return instance;
            }
        }

        // Register a push trigger.
        public void RegisterTrigger(string triggerId, string rootPath,
            TriggerInput<string, FileInfoWrapper> triggerInput)
        {
            // Use FileSystemWatcher toolisten toofile change event.
            var filter = string.IsNullOrEmpty(triggerInput.inputs) ? "*" : triggerInput.inputs;
            var watcher = new FileSystemWatcher(rootPath, filter);
            watcher.IncludeSubdirectories = true;
            watcher.EnableRaisingEvents = true;
            watcher.NotifyFilter = NotifyFilters.LastAccess;

            // When some file is changed, fire hello push trigger.
            watcher.Changed +=
                (sender, e) => watcher_Changed(sender, e,
                    Runtime.FromAppSettings(),
                    triggerInput.GetCallback());

            // Assoicate hello FileSystemWatcher object with hello triggerId.
            _store[triggerId] = watcher;

        }

        // Fire hello assoicated push trigger when some file is changed.
        void watcher_Changed(object sender, FileSystemEventArgs e,
            // AppService runtime object needed tooinvoke hello callback.
            Runtime runtime,
            // hello callback tooinvoke.
            ClientTriggerCallback<FileInfoWrapper> callback)
        {
            // Helper method provided by AppService service SDK tooinvoke a push trigger callback.
            callback.InvokeAsync(runtime, FileInfoWrapper.FromFileInfo(new FileInfo(e.FullPath)));
        }
    }

tootest bu yoklama tetiklemek, şu adımları izleyin:

1. Merhaba API uygulaması bir kimlik doğrulama ayarı ile dağıtmak **ortak anonim**.
2. Çok Gözat[http://requestb.in/](http://requestb.in/) toocreate geri çağırma URL'si olarak davranacak bir RequestBin.
3. Merhaba itme tetikleyicisi bir GUID olarak ile çağrı **Tetikleyici No** ve RequestBin URL'si olarak hello **callbackUrl**.
   ![Postman aracılığıyla gönderme tetikleyici çağırın](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)
4. Merhaba çağrısı **touch** işlemi tootouch bir dosya. Görüntü aşağıdaki hello örnek istek Postman aracılığıyla gösterir.
   ![Postman aracılığıyla dokunma işlem çağırma](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)
5. Anında iletme tetikleyici geri çağırma hello onay hello RequestBin tooconfirm özelliği çıkışıyla çağrılır.
   ![Postman aracılığıyla çağrı yoklama tetikleyici](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)

### <a name="describe-triggers-in-api-definition"></a>API tanımı Tetikleyicileri açıklayın
Merhaba Tetikleyicileri uygulama ve API uygulaması tooAzure dağıtma sonra toohello gidin **API tanımı** dikey penceresinde hello Azure Önizleme portalı ve Tetikleyicileri hello tarafından yönlendirilen UI içinde otomatik olarak tanınır göreceksiniz Merhaba hello API uygulamasının Swagger 2.0 API tanımı.

![API tanımı dikey penceresi](./media/app-service-api-dotnet-triggers/apidefinitionblade.PNG)

Merhaba tıklatırsanız **karşıdan Swagger** düğmesi ve açık hello JSON dosyası, aşağıdaki sonuçları benzer toohello göreceksiniz:

    "/api/files/poll/TouchedFiles": {
      "get": {
        "operationId": "Files_TouchedFilesPollTrigger",
        ...
        "x-ms-scheduler-trigger": "poll"
      }
    },
    "/api/files/push/TouchedFiles/{triggerId}": {
      "put": {
        "operationId": "Files_TouchedFilesPushTrigger",
        ...
        "x-ms-scheduler-trigger": "push"
      }
    }

Merhaba uzantı özelliği **x-ms-schedular-tetikleyici** nasıl Tetikleyicileri API tanımı'nda açıklanan olan ve hello tooone, isterse hello API tanımı hello ağ geçidi aracılığıyla istediğinde hello API uygulama ağ geçidi tarafından otomatik olarak eklenir Ölçüt aşağıdaki hello. (, Bu özellik el ile de ekleyebilirsiniz.)

* Yoklama tetikleyici
  * Merhaba HTTP yöntemini ise **almak**.
  * Merhaba, **Operationıd** özelliği içeren hello dize **tetikleyici**.
  * Merhaba, **parametreleri** özelliği içeren bir parametre ile bir **adı** çok ayarlanan özelliği**triggerState**.
* Tetikleyici bildirme
  * Merhaba HTTP yöntemini ise **PUT**.
  * Merhaba, **Operationıd** özelliği içeren hello dize **tetikleyici**.
  * Merhaba, **parametreleri** özelliği içeren bir parametre ile bir **adı** çok ayarlanan özelliği**Tetikleyici No**.

## <a name="use-api-app-triggers-in-logic-apps"></a>Logic apps içinde API uygulaması Tetikleyicileri kullanın
### <a name="list-and-configure-api-app-triggers-in-hello-logic-apps-designer"></a>Liste ve API uygulaması Tetikleyicileri hello Logic apps Tasarımcısı'nda yapılandırma
Bir mantıksal uygulama hello oluşturursanız, aynı kaynak grubunda Merhaba API uygulaması, mümkün tooadd olacaktır, yalnızca tıklatarak Tasarımcı tuvaline toohello. görüntüleri aşağıdaki hello bu gösterilmektedir:

![Mantıksal Uygulama Tasarımcısı'nda tetikleyicileri](./media/app-service-api-dotnet-triggers/triggersinlogicappdesigner.PNG)

![Yoklama tetikleyici mantığı Uygulama Tasarımcısı'nda yapılandırma](./media/app-service-api-dotnet-triggers/configurepolltriggerinlogicappdesigner.PNG)

![Anında iletme tetikleyici mantığı Uygulama Tasarımcısı'nda yapılandırma](./media/app-service-api-dotnet-triggers/configurepushtriggerinlogicappdesigner.PNG)

## <a name="optimize-api-app-triggers-for-logic-apps"></a>API uygulaması Tetikleyicileri mantıksal uygulamalar için en iyi duruma getirme
Tetikleyiciler tooan API uygulama ekledikten sonra bir mantıksal uygulama hello API uygulamasını kullanırken tooimprove hello deneyimi yapabileceğiniz birkaç şey vardır.

Örneğin, hello **triggerState** parametresi için yoklama Tetikleyicileri hello mantıksal uygulama ifadesinde aşağıdaki toohello ayarlanmalıdır. Bu ifade hello son hello mantıksal uygulama hello tetikleyiciyle çalıştırılışı değerlendirmek ve bu değer döndürmesi gerekir.  

    @coalesce(triggers()?.outputs?.body?['triggerState'], '')

Not: Yukarıdaki hello ifadeyi kullanılan hello işlevleri açıklaması için üzerinde toohello belgelerine başvurun [mantığı uygulama iş akışı tanımlama dili](https://msdn.microsoft.com/library/azure/dn948512.aspx).

Mantığı uygulama kullanıcıların Merhaba tooprovide hello ifade yukarıda gereksinim **triggerState** hello tetikleyici kullanırken parametresi. Bu değer önceden olası toohave hello uzantısı özelliği aracılığıyla hello mantığı Uygulama Tasarımcısı tarafından olduğu **x-ms-Zamanlayıcı-öneri**.  Merhaba **x-ms-görünürlük** uzantısı özelliği tooa değerini ayarlanabilir *iç* böylece hello parametrenin kendisinin hello designer'ı gösterilmez.  Aşağıdaki kod parçacığında Merhaba, gösterilmektedir.

    "/api/Messages/poll": {
      "get": {
        "operationId": "Messages_NewMessageTrigger",
        "parameters": [
          {
            "name": "triggerState",
            "in": "query",
            "required": true,
            "x-ms-visibility": "internal",
            "x-ms-scheduler-recommendation": "@coalesce(triggers()?.outputs?.body?['triggerState'], '')",
            "type": "string"
          }
        ]
        ...
        "x-ms-scheduler-trigger": "poll"
      }
    }

Anında iletme Tetikleyicileri hello **Tetikleyici No** parametresi hello mantıksal uygulama benzersiz şekilde tanımlamalıdır. Önerilen en iyi uygulama bu özellik toohello adını kullanarak hello iş akışı hello ifade aşağıdaki tooset şöyledir:

    @workflow().name

Hello kullanarak **x-ms-Zamanlayıcı-öneri** ve **x-ms-görünürlük** hello API uygulaması kendi API tanımı uzantısı özellikleri iletmek toohello mantığı Uygulama Tasarımcısı tooautomatically bu ayarı Merhaba kullanıcı ifadesi.

        "parameters":[  
          {  
            "name":"triggerId",
            "in":"path",
            "required":true,
            "x-ms-visibility":"internal",
            "x-ms-scheduler-recommendation":"@workflow().name",
            "type":"string"
          },


### <a name="add-extension-properties-in-api-defintion"></a>API tanımı uzantısı özellikleri ekleyin
-Hello uzantısı özellikleri gibi ek meta veri bilgileri **x-ms-Zamanlayıcı-öneri** ve **x-ms-görünürlük** -iki yoldan biriyle hello API tanımı eklenebilir: statik veya dinamik.

Statik meta verilerini hello doğrudan düzenleyebilirsiniz */metadata/apiDefinition.swagger.json* dosya projenizde ve hello özellikleri el ile ekleyin.

Dinamik meta verileri kullanarak API uygulamaları için hello SwaggerConfig.cs dosya tooadd bu uzantılar ekleyebilirsiniz bir işlemi filtresini düzenleyebilirsiniz.

    GlobalConfiguration.Configuration
        .EnableSwagger(c =>
            {
                ...
                c.OperationFilter<TriggerStateFilter>();
                ...
            }


Merhaba, bu sınıf uygulanan toofacilitate hello dinamik meta verileri senaryo nasıl olabilir örneği aşağıdadır.

    // Add extension properties on hello triggerState parameter
    public class TriggerStateFilter : IOperationFilter
    {

        public void Apply(Operation operation, SchemaRegistry schemaRegistry, System.Web.Http.Description.ApiDescription apiDescription)
        {
            if (operation.operationId.IndexOf("Trigger", StringComparison.InvariantCultureIgnoreCase) >= 0)
            {
                // this is a possible trigger
                var triggerStateParam = operation.parameters.FirstOrDefault(x => x.name.Equals("triggerState"));
                if (triggerStateParam != null)
                {
                    if (triggerStateParam.vendorExtensions == null)
                    {
                        triggerStateParam.vendorExtensions = new Dictionary<string, object>();
                    }

                    // add 2 vendor extensions
                    // x-ms-visibility: set too'internal' toosignify this is an internal field
                    // x-ms-scheduler-recommendation: set tooa value that logic app can use
                    triggerStateParam.vendorExtensions.Add("x-ms-visibility", "internal");
                    triggerStateParam.vendorExtensions.Add("x-ms-scheduler-recommendation",
                                                           "@coalesce(triggers()?.outputs?.body?['triggerState'], '')");
                }
            }
        }
    }
