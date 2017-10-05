---
title: "App Service API uygulaması Tetikleyicileri | Microsoft Docs"
description: "Azure App Service'deki bir API uygulamasında Tetikleyicileri gerçekleştirme"
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
ms.openlocfilehash: 3ddfb142e7f1a47e2a8564387da785acf36fa61f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-api-app-triggers"></a>Azure App Service API uygulaması tetikleyicileri
> [!NOTE]
> Makalenin bu sürümü, API apps 2014-12-01-Önizleme şema sürümü için geçerlidir.
>
>

## <a name="overview"></a>Genel Bakış
Bu makalede, API uygulaması Tetikleyicileri uygulamak ve bir mantıksal uygulama kullanma açıklanmaktadır.

Bu konudaki kod parçacıkları tümünün kopyalandığı [FileWatcher API uygulaması kod örneği](http://go.microsoft.com/fwlink/?LinkId=534802).

Kodu derlemek ve çalıştırmak için bu makaledeki için aşağıdaki nuget paketini karşıdan yüklemek için gereken Not: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).

## <a name="what-are-api-app-triggers"></a>API uygulaması Tetikleyicileri nelerdir?
Böylece istemciler API uygulamasının olaya yanıt olarak uygun eylemi gerçekleştirin bir olay tetikleyin için API uygulaması için ortak bir senaryodur. Bu senaryoyu destekler REST API'si mekanizması bir API uygulaması Tetikleyici adı verilir.

Örneğin, istemci kodunuzun kullandığını varsayalım [Twitter Bağlayıcısı API uygulaması](../connectors/connectors-create-api-twitter.md) ve belirli sözcükleri içeren yeni tweet'leri üzerinde dayalı bir eylemi gerçekleştirmek kodunuzu gerekiyor. Bu durumda, bu gereksinimi kolaylaştırmak için yoklama veya itme tetikleyicisi ayarlayabilir.

## <a name="poll-trigger-versus-push-trigger"></a>Yoklama tetikleyici itme tetikleyici karşılaştırması
İki tür tetikleyici sunucusu şu anda desteklenir:

* Yoklama tetikleyici - istemci bildirimi harekete bir olay için API uygulaması yoklar.
* Bir olay başlatıldığında itme tetikleyici - istemci API uygulaması tarafından bildirilir

### <a name="poll-trigger"></a>Yoklama tetikleyici
Yoklama tetikleyici normal bir REST API uygulanır ve istemcilerine (örneğin, bir mantıksal uygulama) bildirim almak için yoklamak için bekliyor. İstemci durumunu korumak, ancak yoklama tetikleyici durum bilgisiz.

İstek ve yanıt paketleri ilgili aşağıdaki bilgileri yoklama tetikleyici sözleşme anahtar bazı yönleri gösterilmiştir:

* İstek
  * HTTP yöntemini: Al
  * Parametreler
    * triggerState - yoklama tetikleyici düzgün veya bildirim döndürülecek karar verebilir böylece durumlarına belirtilen durumuna bağlı belirtmek istemcilerin bu isteğe bağlı parametre sağlar.
    * API özel parametreler
* Yanıt
  * Durum kodu **200** - istek geçerli ve tetikleyici bildirimden yoktur. Bildirim içeriğini yanıt gövdesi olacaktır. Ek bildirim verileri bir sonraki istek çağrısı ile alınması gereken bir "Yeniden deneme-sonra" üstbilgisi yanıt gösterir.
  * Durum kodu **202** - istek geçerlidir, ancak tetikleyici öğesinden yeni bildirim yoktur.
  * Durum kodu **4xx** -isteği geçerli değil. İstemci isteği yeniden.
  * Durum kodu **5xx** -isteği bir iç sunucu hatası ve/veya geçici bir sorun içinde sonuçlandı. İstemci isteği yeniden denemeniz gerekir.

Aşağıdaki kod parçacığını bir yoklama Tetik uygulamak nasıl bir örnektir.

    // Implement a poll trigger.
    [HttpGet]
    [Route("api/files/poll/TouchedFiles")]
    public HttpResponseMessage TouchedFilesPollTrigger(
        // triggerState is a UTC timestamp
        string triggerState,
        // Additional parameters
        string searchPattern = "*")
    {
        // Check to see whether there is any file touched after the timestamp.
        var lastTriggerTimeUtc = DateTime.Parse(triggerState).ToUniversalTime();
        var touchedFiles = Directory.EnumerateFiles(rootPath, searchPattern, SearchOption.AllDirectories)
            .Select(f => FileInfoWrapper.FromFileInfo(new FileInfo(f)))
            .Where(fi => fi.LastAccessTimeUtc > lastTriggerTimeUtc);

        // If there are files touched after the timestamp, return their information.
        if (touchedFiles != null && touchedFiles.Count() != 0)
        {
            // Extension method provided by the AppService service SDK.
            return this.Request.EventTriggered(new { files = touchedFiles });
        }
        // If there are no files touched after the timestamp, tell the caller to poll again after 1 mintue.
        else
        {
            // Extension method provided by the AppService service SDK.
            return this.Request.EventWaitPoll(new TimeSpan(0, 1, 0));
        }
    }

Bu yoklama tetikleyici sınamak için aşağıdaki adımları izleyin:

1. Bir kimlik doğrulama ayarı olan API uygulaması dağıtma **ortak anonim**.
2. Çağrı **touch** bir dosya touch işlemi. Aşağıdaki resimde bir örnek istek Postman aracılığıyla gösterir.
   ![Postman aracılığıyla dokunma işlem çağırma](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)
3. Yoklama tetikleyiciyle çağrısı **triggerState** #2. adım önce bir zaman damgası parametresini ayarlayın. Aşağıdaki resimde Postman aracılığıyla örnek isteğini gösterir.
   ![Postman aracılığıyla çağrı yoklama tetikleyici](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)

### <a name="push-trigger"></a>Tetikleyici bildirme
Anında iletme tetikleyicinin belirli olay tetiklendiğinde bildirim almak için kaydettiniz istemciler için bildirimler iter normal bir REST API olarak uygulanır.

İstek ve yanıt paketleri ilgili aşağıdaki bilgileri anında tetikleyici sözleşme anahtar bazı yönleri gösterilmiştir.

* İstek
  * HTTP yöntemini: YERLEŞTİRME
  * Parametreler
    * Tetikleyici No: gerekli - itme tetikleyici kaydını temsil eden donuk dizesini (örneğin, bir GUID).
    * callbackUrl: gerekli - olay başlatıldığında çağırmak geri çağırma URL'si. Basit bir POST HTTP çağrısıyla çağrıdır.
    * API özel parametreler
* Yanıt
  * Durum kodu **200** -istemci başarılı kaydetmek için istek.
  * Durum kodu **4xx** -isteği geçerli değil. İstemci isteği yeniden.
  * Durum kodu **5xx** -isteği bir iç sunucu hatası ve/veya geçici bir sorun içinde sonuçlandı. İstemci isteği yeniden denemeniz gerekir.
* Geri çağırma
  * HTTP yöntemini: POST
  * İstek gövdesindeki: bildirim içeriği.

Aşağıdaki kod parçacığını nasıl anında iletme tetikleyici uygulanacağı örneğidir:

    // Implement a push trigger.
    [HttpPut]
    [Route("api/files/push/TouchedFiles/{triggerId}")]
    public HttpResponseMessage TouchedFilesPushTrigger(
        // triggerId is an opaque string.
        string triggerId,
        // A helper class provided by the AppService service SDK.
        // Here it defines the input of the push trigger is a string and the output to the callback is a FileInfoWrapper object.
        [FromBody]TriggerInput<string, FileInfoWrapper> triggerInput)
    {
        // Register the trigger to some trigger store.
        triggerStore.RegisterTrigger(triggerId, rootPath, triggerInput);

        // Extension method provided by the AppService service SDK indicating the registration is completed.
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
            // Use FileSystemWatcher to listen to file change event.
            var filter = string.IsNullOrEmpty(triggerInput.inputs) ? "*" : triggerInput.inputs;
            var watcher = new FileSystemWatcher(rootPath, filter);
            watcher.IncludeSubdirectories = true;
            watcher.EnableRaisingEvents = true;
            watcher.NotifyFilter = NotifyFilters.LastAccess;

            // When some file is changed, fire the push trigger.
            watcher.Changed +=
                (sender, e) => watcher_Changed(sender, e,
                    Runtime.FromAppSettings(),
                    triggerInput.GetCallback());

            // Assoicate the FileSystemWatcher object with the triggerId.
            _store[triggerId] = watcher;

        }

        // Fire the assoicated push trigger when some file is changed.
        void watcher_Changed(object sender, FileSystemEventArgs e,
            // AppService runtime object needed to invoke the callback.
            Runtime runtime,
            // The callback to invoke.
            ClientTriggerCallback<FileInfoWrapper> callback)
        {
            // Helper method provided by AppService service SDK to invoke a push trigger callback.
            callback.InvokeAsync(runtime, FileInfoWrapper.FromFileInfo(new FileInfo(e.FullPath)));
        }
    }

Bu yoklama tetikleyici sınamak için aşağıdaki adımları izleyin:

1. Bir kimlik doğrulama ayarı olan API uygulaması dağıtma **ortak anonim**.
2. Gözat [http://requestb.in/](http://requestb.in/) geri çağırma URL'si olarak davranacak bir RequestBin oluşturmak için.
3. Bir GUID olarak itme tetikleyiciyle çağrısı **Tetikleyici No** ve RequestBin URL'si olarak **callbackUrl**.
   ![Postman aracılığıyla gönderme tetikleyici çağırın](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)
4. Çağrı **touch** bir dosya touch işlemi. Aşağıdaki resimde bir örnek istek Postman aracılığıyla gösterir.
   ![Postman aracılığıyla dokunma işlem çağırma](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)
5. Anında iletme tetikleyici geri çağırma özelliği çıkışıyla çağrılır onaylamak için RequestBin denetleyin.
   ![Postman aracılığıyla çağrı yoklama tetikleyici](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)

### <a name="describe-triggers-in-api-definition"></a>API tanımı Tetikleyicileri açıklayın
Tetikleyiciler uygulama ve API uygulamanızı Azure'a dağıtan sonra gidin **API tanımı** dikey Azure Önizleme portalını ve Tetikleyicileri Swagger tarafından yönetilen kullanıcı arabiriminde otomatik olarak tanınır göreceksiniz 2.0 API uygulaması API tanımı.

![API tanımı dikey penceresi](./media/app-service-api-dotnet-triggers/apidefinitionblade.PNG)

Tıklatırsanız **karşıdan Swagger** düğmesini tıklatın ve JSON dosyasını açın, aşağıdakine benzer sonuçlar görürsünüz:

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

Uzantı özelliği **x-ms-schedular-tetikleyici** nasıl Tetikleyicileri API tanımı'nda açıklanan olduğu ve varsa ağ geçidi üzerinden API tanımı istediğinde API uygulama ağ geçidi tarafından otomatik olarak eklenen birini isteği aşağıdaki ölçütleri. (, Bu özellik el ile de ekleyebilirsiniz.)

* Yoklama tetikleyici
  * HTTP yöntemi ise **almak**.
  * Varsa **Operationıd** özelliği içeren dize **tetikleyici**.
  * Varsa **parametreleri** özelliği içeren bir parametre ile bir **adı** özelliğini **triggerState**.
* Tetikleyici bildirme
  * HTTP yöntemi ise **PUT**.
  * Varsa **Operationıd** özelliği içeren dize **tetikleyici**.
  * Varsa **parametreleri** özelliği içeren bir parametre ile bir **adı** özelliğini **Tetikleyici No**.

## <a name="use-api-app-triggers-in-logic-apps"></a>Logic apps içinde API uygulaması Tetikleyicileri kullanın
### <a name="list-and-configure-api-app-triggers-in-the-logic-apps-designer"></a>Liste ve API uygulaması Tetikleyicileri Logic apps Tasarımcısı'nda yapılandırma
API uygulaması ile aynı kaynak grubunda bir mantıksal uygulama oluşturursanız, yalnızca tıklayarak Tasarımcı tuvaline eklemek mümkün olacaktır. Aşağıdaki görüntüler bu gösterilmektedir:

![Mantıksal Uygulama Tasarımcısı'nda tetikleyicileri](./media/app-service-api-dotnet-triggers/triggersinlogicappdesigner.PNG)

![Yoklama tetikleyici mantığı Uygulama Tasarımcısı'nda yapılandırma](./media/app-service-api-dotnet-triggers/configurepolltriggerinlogicappdesigner.PNG)

![Anında iletme tetikleyici mantığı Uygulama Tasarımcısı'nda yapılandırma](./media/app-service-api-dotnet-triggers/configurepushtriggerinlogicappdesigner.PNG)

## <a name="optimize-api-app-triggers-for-logic-apps"></a>API uygulaması Tetikleyicileri mantıksal uygulamalar için en iyi duruma getirme
Bir API uygulaması Tetikleyicileri ekledikten sonra API uygulaması bir mantıksal uygulama kullanırken deneyimini iyileştirmek için yapabileceğiniz birkaç işlem vardır.

Örneğin, **triggerState** parametresi için yoklama Tetikleyicileri mantıksal uygulama aşağıdaki ifadesinde ayarlanmalıdır. Bu ifade mantıksal uygulama tetikleyiciyle son çağrılmasını değerlendirmek ve bu değer döndürmesi gerekir.  

    @coalesce(triggers()?.outputs?.body?['triggerState'], '')

Not: Yukarıdaki ifadeyi kullanılan işlevler açıklaması için üzerinde belgelere bakın [mantığı uygulama iş akışı tanımlama dili](https://msdn.microsoft.com/library/azure/dn948512.aspx).

Mantıksal uygulama kullanıcılarınızın yukarıda ifadesi sağlamak gerekir **triggerState** tetikleyici kullanırken parametresi. Uzantı özelliği aracılığıyla mantığı Uygulama Tasarımcısı tarafından önceden bu değeri olması mümkündür **x-ms-Zamanlayıcı-öneri**.  **X-ms-görünürlük** uzantı özelliği için bir değer ayarlanabilir *iç* böylece parametre designer'ı gösterilmez.  Aşağıdaki kod parçacığında, gösterilmektedir.

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

Anında iletme Tetikleyicileri **Tetikleyici No** parametresi mantıksal uygulama benzersiz şekilde tanımlamalıdır. Aşağıdaki ifade kullanarak iş akışının adı için bu özelliği ayarlamak için önerilen en iyi yöntem değil:

    @workflow().name

Kullanarak **x-ms-Zamanlayıcı-öneri** ve **x-ms-görünürlük** API uygulaması kendi API tanımı uzantısı özellikleri iletmek için bu deyim için otomatik olarak ayarlamak için mantığı Uygulama Tasarımcısı Kullanıcı.

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
-Uzantısı özellikleri gibi ek meta veri bilgileri **x-ms-Zamanlayıcı-öneri** ve **x-ms-görünürlük** -iki yoldan biriyle API tanımı eklenebilir: statik veya dinamik.

Statik meta verileri için doğrudan düzenleyebilirsiniz */metadata/apiDefinition.swagger.json* dosya projenizde ve özellikleri el ile ekleyin.

Dinamik meta verileri kullanarak API uygulamaları için bu uzantılar ekleyebilirsiniz bir işlemi filtre eklemek için SwaggerConfig.cs dosyasını düzenleyebilirsiniz.

    GlobalConfiguration.Configuration
        .EnableSwagger(c =>
            {
                ...
                c.OperationFilter<TriggerStateFilter>();
                ...
            }


Bu sınıf dinamik meta verileri senaryo kolaylaştırmak için nasıl uygulanabileceği bir örnek verilmiştir.

    // Add extension properties on the triggerState parameter
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
                    // x-ms-visibility: set to 'internal' to signify this is an internal field
                    // x-ms-scheduler-recommendation: set to a value that logic app can use
                    triggerStateParam.vendorExtensions.Add("x-ms-visibility", "internal");
                    triggerStateParam.vendorExtensions.Add("x-ms-scheduler-recommendation",
                                                           "@coalesce(triggers()?.outputs?.body?['triggerState'], '')");
                }
            }
        }
    }
