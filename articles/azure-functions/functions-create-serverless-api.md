---
title: "Azure işlevleri kullanarak sunucusuz bir API aaaCreate | Microsoft Docs"
description: "Nasıl toocreate Azure işlevleri kullanarak sunucusuz bir API"
services: functions
author: mattchenderson
manager: erikre
ms.service: functions
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: tutorial
ms.date: 05/04/2017
ms.author: mahender
ms.custom: mvc
ms.openlocfilehash: 877e3b229d5477fc5fec594ccd284fb55d7f3c07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-serverless-api-using-azure-functions"></a>Azure işlevleri kullanarak sunucusuz bir API oluşturma

Bu öğreticide nasıl toobuild sağlar Azure işlevleri öğreneceksiniz yüksek düzeyde ölçeklenebilir API'leri. Azure işlevleri, bir uç nokta diller, Node.JS, C# ve daha fazlası da dahil olmak üzere çeşitli yerleşik HTTP tetikleyiciler ve kolay tooauthor anlamasını bağlamaları koleksiyonu ile gelir. Bu öğreticide, bir HTTP tetikleyicisi toohandle belirli eylemler API tasarımınızda özelleştirin. Ayrıca, Azure işlevleri proxy'leri ile tümleştirme ve sahte API'leri ayarlayarak API'nizi artan için hazırlarsınız. Tüm bunlar gerçekleştirilir hello işlevleri sunucusuz bilgi işlem ortamı en üstünde, kaynakları ölçeklendirme hakkında tooworry yok - yalnızca, API mantığına odaklanabilir şekilde.

## <a name="prerequisites"></a>Ön koşullar 

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

Merhaba elde edilen işlevi Bu öğretici hello kalanı için kullanılır.

### <a name="sign-in-tooazure"></a>İçinde tooAzure oturum

Açık hello Azure portalı. toodo Bu, çok oturum[https://portal.azure.com](https://portal.azure.com) Azure hesabınızla.

## <a name="customize-your-http-function"></a>HTTP işlevinizi özelleştirme

Varsayılan olarak, HTTP tetiklemeli işlevin yapılandırılmış tooaccept olan herhangi bir HTTP yöntemi. Ayrıca varsayılan URL hello formunun olduğu `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`. Merhaba hızlı başlangıç, ardından izlediyseniz `<funcname>` büyük olasılıkla "HttpTriggerJS1" şöyle görünür. Bu bölümde, hello işlevi toorespond yalnızca tooGET istekler değiştirecek `/api/hello` yerine rota. 

Tooyour işlevinde hello Azure portalına gidin. Seçin **tümleştir** sol gezinti hello içinde.

![Bir HTTP işlevi özelleştirme](./media/functions-create-serverless-api/customizing-http.png)

Merhaba tabloda belirtildiği gibi HTTP tetikleyicisi ayarlarını kullanın.

| Alan | Örnek değer | Açıklama |
|---|---|---|
| İzin verilen HTTP yöntemleri | Seçili yöntemleri | Hangi HTTP yöntemlerini kullanılan tooinvoke olabilir belirler bu işlevi |
| Seçili HTTP yöntemleri | AL | Yalnızca seçili HTTP yöntemleri toobe tooinvoke bu işlev kullanılan sağlar |
| Rota şablonu | / Merhaba | Kullanılan tooinvoke hangi rota belirler bu işlevi |

Merhaba içermeyen Not `/api` bu genel bir ayar tarafından gerçekleştirilir gibi temel yol önekini hello rota şablonu.

**Kaydet** düğmesine tıklayın.

HTTP işlevlerini özelleştirme hakkında daha fazla bilgiyi [Azure işlevleri HTTP ve Web kancası bağlamaları](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint).

### <a name="test-your-api"></a>API'nizi test

Ardından, işlevi toosee hello yeni API yüzeyi ile çalışma test.

Sol gezinti hello hello işlevin adını tıklayarak geri toohello geliştirme sayfasına gidin.

Tıklatın **Al işlevi URL** ve hello URL'yi kopyalayın. Merhaba kullandığını görürsünüz `/api/hello` şimdi rota.

Yeni bir tarayıcı sekmesi ya da tercih edilen REST istemciniz Hello URL'sini kopyalayın. Tarayıcılar GET varsayılan olarak kullanır.

Merhaba işlevi çalıştırın ve çalıştığını doğrulayın. Bir sorgu dizesi toosatisfy hello quickstart kodu olarak tooprovide hello "name" parametre gerekebilir.

Ayrıca, başka bir HTTP yöntemini tooconfirm hello işlevi yürütülmez ile Merhaba uç noktası çağrılmadan deneyebilirsiniz. Bunun için toouse cURL, Postman veya Fiddler gibi bir REST istemcisi gerekir.

## <a name="proxies-overview"></a>Proxy'leri genel bakış

Merhaba sonraki bölümde, bir proxy üzerinden API'nizi belirir. Azure işlevleri proxy'leri tooforward istekleri tooother kaynakları sağlayan bir önizleme özelliğidir. Bir HTTP uç noktası HTTP tetikleyicisi ile olduğu gibi tanımlayın, ancak bu uç çağrıldığında kodu tooexecute yazmak yerine, bir URL tooa uzak uygulamasını sağlar. Bu, istemcilerin tooconsume için kolay olan tek bir API yüzeyi içine birden çok API kaynakları toocompose sağlar. API'nizi mikro olarak toobuild isterseniz, bu özellikle yararlıdır.

Bir proxy gibi tooany HTTP kaynak gösterebilir:
- Azure İşlevleri 
- API uygulamaları [Azure uygulama hizmeti](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)
- Docker kapsayıcılarında [Linux uygulama hizmeti](https://docs.microsoft.com/azure/app-service/app-service-linux-readme)
- Barındırılan herhangi bir API'yi

toolearn proxy'leri hakkında daha fazla bilgi görmek [Azure işlevleri proxy'leri (Önizleme) çalışmaya].

## <a name="create-your-first-proxy"></a>İlk proxy oluşturma

Bu bölümde, yeni bir proxy hangi görevi görür bir ön uç tooyour oluşturacağınız Genel API. 

### <a name="setting-up-hello-frontend-environment"></a>Merhaba ön uç ortamını ayarlama

Çok Hello adımları yineleyin[bir işlev uygulaması oluşturma](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app) toocreate yeni bir işlev uygulaması proxy oluşturacak içinde. Bu yeni uygulama için bizim API hello ön uç hizmet verir ve önceden düzenlemekte olduğunuz hello işlev uygulaması arka ucu olarak hizmet verecektir.

Tooyour yeni ön uç işlev uygulaması hello portalında gidin.

Seçin **ayarları**. Ardından geçiş **etkinleştirmek Azure işlevleri proxy'leri (Önizleme)** çok "açık".

Seçin **Platform ayarları** ve **uygulama ayarları**.

Çok ilerleyin**uygulama ayarları** ve "HELLO_HOST" anahtarı ile yeni bir ayar oluşturun. Değer toohello ana bilgisayar, arka uç işlevi uygulamanızın ayarlamak `<YourApp>.azurewebsites.net`. Bu, HTTP işlevinizi test edilirken daha önce kopyaladığınız hello URL parçasıdır. Bu ayar daha sonra hello yapılandırmasında başvuru.

> [!NOTE] 
> Uygulama ayarları hello proxy için sabit kodlanmış ortamı bağımlılık hello ana bilgisayar yapılandırma tooprevent için önerilir. Uygulama ayarları kullanarak hello proxy yapılandırması ortamlar arasında taşıyabilirsiniz ve hello ortama özgü uygulama ayarları uygulanacak anlamına gelir.

**Kaydet** düğmesine tıklayın.

### <a name="creating-a-proxy-on-hello-frontend"></a>Bir proxy hello ön uç üzerinde oluşturma

Merhaba portalında geri tooyour ön uç işlevi uygulamasına gidin.

Merhaba sol gezinti bölmesinde hello oturum plus '+' sonraki çok tıklayın "Proxy'leri (Önizleme)".

![Bir proxy sunucu oluşturma](./media/functions-create-serverless-api/creating-proxy.png)

Merhaba tabloda belirtildiği gibi proxy ayarlarını kullanın.

| Alan | Örnek değer | Açıklama |
|---|---|---|
| Ad | HelloProxy | Yalnızca yönetim için kullanılan bir kolay ad |
| Rota şablonu | / api/hello | Kullanılan tooinvoke hangi rota belirler bu proxy |
| Arka uç URL'si | https://%HELLO_HOST%/api/Hello | Merhaba uç noktası toowhich hello isteği yönlendirilirken belirtir |

Proxy'leri sağlamaz, hello Not `/api` taban yol öneki ve hello rota şablona dahil bu gerekir.

Merhaba `%HELLO_HOST%` sözdizimi, daha önce oluşturduğunuz hello uygulama ayarı başvuru. Merhaba, URL tooyour özgün işlevi işaret edecek çözümlendi.

**Oluştur**'a tıklayın.

Merhaba Proxy URL'si kopyalayarak ve hello tarayıcıda veya test sık kullanılan HTTP istemci ile yeni proxy deneyebilirsiniz.

## <a name="create-a-mock-api"></a>Sahte bir API oluşturma

Ardından, çözümünüz için bir proxy toocreate sahte bir API kullanır. Bu istemci geliştirme sağlar tam olarak uygulanan hello arka uç gerek olmadan tooprogress. Geliştirme, daha sonra bu mantığı destekleyen yeni bir işlev uygulaması oluşturmak ve proxy tooit yönlendirir.

toocreate bu mock API, yeni bir proxy hello kullanarak bu kez oluşturacağız [App Service Düzenleyicisi](https://github.com/projectkudu/kudu/wiki/App-Service-Editor). başlatıldı, tooget tooyour işlev uygulaması hello portalında gidin. Seçin **Platform özellikleri** ve Bul **App Service Düzenleyicisi**. Bu tıklandığında hello App Service Düzenleyicisi yeni sekmede açılır.

Seçin `proxies.json` sol gezinti hello içinde. Bu, proxy'leri tamamı için hello yapılandırma depolayan hello dosyasıdır. Merhaba birini kullanırsanız [işlevleri dağıtım yöntemleri](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment), bu kaynak denetiminde koruyacaktır hello dosyasıdır. Bu dosya hakkında daha fazla toolearn bkz [proxy'leri Gelişmiş Yapılandırma](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration).

O ana kadarki izlediyseniz, proxies.json hello aşağıdaki gibi görünmelidir:

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "HelloProxy": {
            "matchCondition": {
                "route": "/api/hello"
            },
            "backendUri": "https://%HELLO_HOST%/api/hello"
        }
    }
}
```

Sonraki sahte API'nizi ekleyeceksiniz. Proxies.json dosyanızı hello şununla değiştirin:

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "HelloProxy": {
            "matchCondition": {
                "route": "/api/hello"
            },
            "backendUri": "https://%HELLO_HOST%/api/hello"
        },
        "GetUserByName" : {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/users/{username}"
            },
            "responseOverrides": {
                "response.statusCode": "200",
                "response.headers.Content-Type" : "application/json",
                "response.body": {
                    "name": "{username}",
                    "description": "Awesome developer and master of serverless APIs",
                    "skills": [
                        "Serverless",
                        "APIs",
                        "Azure",
                        "Cloud"
                    ]
                }
            }
        }
    }
}
```

Bu yeni olmadan bir proxy, "GetUserByName" Merhaba backendUri özelliği ekler. Başka bir kaynak çağırmak yerine, bir yanıt geçersiz kılma kullanılarak proxy'leri hello varsayılan yanıttan değiştirir. İstek ve yanıt geçersiz kılmaları da arka uç URL'si ile birlikte kullanılabilir. Burada ihtiyacınız olabilecek toomodify üstbilgiler, sorgu parametreleri, vb. toolearn istek ve yanıt geçersiz kılmalar hakkında daha fazla bilgi, proxy tooa eski sistem gördüğünüzde, bu özellikle yararlı olacaktır [istekleri ve yanıtları proxy'leri değiştirme](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses).

Arama hello tarafından sahte API'nizi test `/api/users/{username}` bir tarayıcı veya sık kullandığınız REST istemcisinden kullanarak uç nokta. Emin tooreplace olması _{username}_ olan bir kullanıcı adı temsil eden bir dize değeri.

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, nasıl öğrenilen toobuild ve Azure işlevleri bir API özelleştirebilirsiniz. Ayrıca, nasıl toobring dahil olmak üzere çok sayıda API, birlikte birleşik bir API yüzeyi olarak mocks öğrendiniz. Tüm hello sunucusuz çalışırken Azure işlevleri tarafından sağlanan modeline işlem, bu teknikler toobuild API'ler herhangi karmaşıklık çıkışı kullanabilirsiniz.

Daha fazla API'nizi geliştirdikçe hello aşağıdaki başvurular yararlı olabilir:

- [Azure işlevleri HTTP ve Web kancası bağlamaları](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook)
- [Azure işlevleri proxy'leri (Önizleme) çalışmaya]
- [Azure işlevleri API (Önizleme) belgeleme](https://docs.microsoft.com/azure/azure-functions/functions-api-definition-getting-started)


[Create your first function]: https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function
[Azure işlevleri proxy'leri (Önizleme) çalışmaya]: https://docs.microsoft.com/azure/azure-functions/functions-proxies
