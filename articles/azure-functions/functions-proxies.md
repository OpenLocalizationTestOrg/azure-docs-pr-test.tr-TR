---
title: "Azure işlevleri proxy'leri ile aaaWork | Microsoft Docs"
description: "Hakkında genel bakış toouse Azure işlevleri proxy'leri"
services: functions
documentationcenter: 
author: mattchenderson
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/11/2017
ms.author: mahender
ms.openlocfilehash: 4d94c89e8f8f2d2c771b01bae142bf9a4f3b7f2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-azure-functions-proxies-preview"></a>Azure işlevleri proxy'leri (Önizleme) ile çalışma

> [!NOTE] 
> Azure işlevleri proxy'leri şu anda önizlemede değil. Önizleme, ancak standart işlevleri faturalama tooproxy yürütmeleri uygularken ücretsizdir. Daha fazla bilgi için bkz: [Azure işlevleri fiyatlandırma](https://azure.microsoft.com/pricing/details/functions/).

Bu makalede açıklanır nasıl tooconfigure ve Azure işlevleri proxy'leri ile çalışır. Bu özellik ile başka bir kaynak tarafından uygulanan işlevi uygulamanızdan uç noktalarını belirtebilirsiniz. İstemciler için tek bir API yüzeyi hala sunarken büyük bir API uygulamasına (olduğu gibi bir mikro Hizmet Mimarisi), birden çok işlev uygulamalarının bu proxy'leri toobreak kullanabilirsiniz.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]


## <a name="enable"></a>Azure işlevleri proxy'leri etkinleştir

Proxy'leri varsayılan olarak etkin değildir. Merhaba özellik devre dışı bırakıldı, ancak bunlar yürütülemeyecek proxy'leri oluşturabilirsiniz. tooenable proxy'leri hello aşağıdaki:

1. Açık hello [Azure portal], ve ardından tooyour işlev uygulaması gidin.
2. Seçin **işlev uygulaması ayarları**.
3. Anahtar **etkinleştirmek Azure işlevleri proxy'leri (Önizleme)** çok**üzerinde**.

Yeni özellikleri kullanılabilir duruma geldiğinde tooupdate hello proxy çalışma zamanı Ayrıca buraya dönebilirsiniz.


## <a name="create"></a>Bir proxy sunucu oluşturma

Bu bölümde, nasıl toocreate proxy'sine bir hello işlevleri portalına gösterir.

1. Açık hello [Azure portal], ve ardından tooyour işlev uygulaması gidin.
2. Merhaba sol bölmesinde seçin **yeni proxy**.
3. Proxy için bir ad sağlayın.
4. Merhaba belirterek bu işlev uygulaması sunulan hello uç noktası yapılandırmak **rota şablonu** ve **HTTP yöntemleri**. Bu parametreler için according toohello kuralları davranır [HTTP Tetikleyicileri].
5. Set hello **arka uç URL'si** tooanother uç noktası. Bu uç noktaya başka bir işlev uygulaması işlevinde olabilir veya diğer herhangi bir API'yi olabilir. Merhaba değeri toobe statik gerekmez ve başvurusu yapabilir [uygulama ayarları] ve [hello özgün istemci istek parametrelerinden].
6. **Oluştur**'a tıklayın.

Proxy şimdi işlevi uygulamanızdan yeni bir uç noktası olarak bulunmaktadır. İstemci açısından bakıldığında, bu eşdeğer tooan Azure işlevlerinde HttpTrigger olur. Merhaba Proxy URL'si kopyalayarak ve sık kullanılan HTTP istemci ile test yeni proxy deneyebilirsiniz.

## <a name="modify-requests-responses"></a>İsteklerin ve yanıtların değiştirme

Azure işlevleri proxy'leriyle istekleri tooand yanıtları hello arka uçtan değiştirebilirsiniz. Bu dönüşümleri tanımlandığı gibi değişkenleri kullanabilirsiniz [değişkenlerini kullanın].

### <a name="modify-backend-request"></a>Merhaba arka uç isteği değiştirme

Varsayılan olarak, hello arka uç isteği hello özgün istek bir kopyası olarak başlatılır. Ayrıca toosetting hello arka uç URL'si, değişiklikleri toohello HTTP yöntemi, üst bilgiler ve sorgu dizesi parametreleri yapabilirsiniz. Merhaba değiştirilen değerleri başvuru [uygulama ayarları] ve [hello özgün istemci istek parametrelerinden].

Şu anda arka uç istekleri değiştirmek için hiçbir portal deneyimi yoktur. toolearn tooapply proxies.json, bu özellikten nasıl görürüm [requestOverrides nesnesi tanımlayın].

### <a name="modify-response"></a>Merhaba yanıtı değiştirebilir

Varsayılan olarak, hello istemci yanıt hello arka uç yanıt bir kopyası olarak başlatılır. Değişiklikleri toohello yanıtın durum kodu, neden ifadesini, üstbilgiler ve gövde yapabilirsiniz. Merhaba değiştirilen değerleri başvuru [uygulama ayarları], [hello özgün istemci istek parametrelerinden], ve [hello arka uç yanıt parametrelerinden].

Şu anda, yanıtları değiştirmek için hiçbir portal deneyimi yoktur. toolearn tooapply proxies.json, bu özellikten nasıl görürüm [responseOverrides nesnesi tanımlayın].

## <a name="using-variables"></a>Değişkenleri kullanma

bir proxy için başlangıç yapılandırmasını toobe statik gerekmez. Bu toouse değişkenleri hello ilk istek, hello arka uç yanıt ya da uygulama ayarları koşulu.

### <a name="request-parameters"></a>Başvuru İstek parametreleri

İstek parametreleri toohello arka uç URL'si özelliği girdi olarak veya isteklerin ve yanıtların değiştirerek bir parçası olarak kullanabilirsiniz. Bazı parametreler hello temel proxy yapılandırma dosyasında belirtilen hello rota şablondan bağlı olabilir ve diğerleri hello gelen istek özelliklerinden gelebilir.

#### <a name="route-template-parameters"></a>Rota şablon parametreleri
Merhaba rota şablonda kullanılan parametreler ada göre başvurulan kullanılabilir toobe bağlıdır. Merhaba parametre adı kaşlı ({}) içine alınır.

Örneğin, bir proxy gibi bir rota şablonu varsa `/pets/{petId}`, hello arka uç URL'si hello değerini içerebilir `{petId}`, olarak `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`. Merhaba rota şablonu bir joker karakter olarak gibi kesilip kesilmediğini `/api/{*restOfPath}`, hello değeri `{restOfPath}` hello gelen istek yol bölümlerinin kalan hello dize gösterimidir.

#### <a name="additional-request-parameters"></a>Ek İstek parametreleri
Ayrıca toohello rota şablonu parametreleri, değerleri aşağıdaki hello yapılandırma değerleri kullanılabilir:

* **{request.method}** : Merhaba hello özgün istekte kullanılan HTTP yöntemi.
* **{request.headers. \<HeaderName\>}**: hello özgün isteğinden okunabilir bir üstbilgi. Değiştir  *\<HeaderName\>*  tooread istediğiniz hello üstbilgisinin hello ada sahip. Merhaba üstbilgi hello isteğinde bulunmuyorsa hello değer hello boş dize olacaktır.
* **{request.querystring. \<ParameterName\>}**: hello özgün isteğinden okunabilir bir sorgu dizesi parametresi. Değiştir  *\<ParameterName\>*  tooread istediğiniz hello parametresinin hello ada sahip. Merhaba parametre hello isteğinde bulunmuyorsa hello değer hello boş dize olacaktır.

### <a name="response-parameters"></a>Başvuru arka uç yanıt parametreleri

Yanıt parametrelerinin hello yanıt toohello istemci değiştirerek bir parçası olarak kullanılabilir. değerleri aşağıdaki hello yapılandırma değerleri kullanılabilir:

* **{backend.response.statusCode}** : Merhaba hello arka uç yanıtta döndürülen HTTP durum kodu.
* **{backend.response.statusReason}** : hello arka uç yanıtta döndürülen hello HTTP neden ifadesini.
* **{backend.response.headers. \<HeaderName\>}**: hello arka uç yanıttan okunabilir bir üstbilgi. Değiştir  *\<HeaderName\>*  tooread istediğiniz hello üstbilgisinin hello adı. Merhaba üstbilgi hello isteğinde bulunmuyorsa hello değer hello boş dize olacaktır.

### <a name="use-appsettings"></a>Başvuru uygulama ayarları

Ayrıca başvurabilir [hello işlev uygulaması için tanımlanan uygulama ayarları](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) hello ayarı adı yüzde işaretleri (%) çevreleyen tarafından.

Örneğin, arka uç URL'sini *https://%ORDER_PROCESSING_HOST%/api/orders* "Merhaba ORDER_PROCESSING_HOST ayarı hello değerle değiştirilen ORDER_PROCESSING_HOST %" olması gerekir.

> [!TIP] 
> Birden çok dağıtım varsa, arka uç ana bilgisayarlar için uygulama ayarları kullanın veya test ortamları. Bu şekilde, her zaman Konuşmayı emin yapabileceğiniz sağ geri toohello end bu ortam için.

## <a name="advanced-configuration"></a>Gelişmiş yapılandırma

yapılandırdığınız hello proxy'leri hello işlevi uygulama dizin kökünde bulunan bir proxies.json dosyasında depolanır. El ile bu dosyasını düzenleyin ve hello birini kullandığınızda, uygulamanızın bir parçası olarak dağıtmanız [dağıtım yöntemleri](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) bu işlevleri destekler. Merhaba özelliği olmalı [etkin](#enable) işlenen hello dosya toobe için. 

> [!TIP] 
> Bir hello dağıtım yöntemleri ayarlamadıysanız hello portalında hello proxies.json dosyayla çalışabilirsiniz. Git tooyour işlev uygulaması, select **Platform özellikleri**ve ardından **App Service Düzenleyicisi**. Bunu yaparak, hello tüm dosya yapısı işlevi uygulamanızın görüntüleyin ve ardından değişiklikleri yapın.

Proxies.JSON adlandırılmış proxy'leri ve tanımlarını oluşan bir proxy nesnesi tarafından tanımlanır. İsteğe bağlı olarak, düzenleyicinizi destekliyorsa, başvurabileceğiniz bir [JSON şeması](http://json.schemastore.org/proxies) için kod tamamlama. Bir örnek dosyası hello şuna benzeyebilir:

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "backendUri": "https://<AnotherApp>.azurewebsites.net/api/<FunctionName>"
        }
    }
}
```

Her proxy gibi kolay bir ada sahip *proxy1* örnek önceki hello içinde. Merhaba karşılık gelen proxy tanım nesnesi, aşağıdaki özelliklere hello tarafından tanımlanır:

* **matchCondition**:--Bu proxy hello yürütülmesini tetiklemek hello istekleri tanımlayan bir nesne gerekli. İle paylaşılan iki özellikler içeren [HTTP Tetikleyicileri]:
    * _yöntemleri_: proxy hello hello HTTP yöntemleri bir dizi yanıt verir. Belirtilmezse, hello proxy tooall HTTP yöntemleri hello rotada yanıt verir.
    * _Rota_: gerekli--hangi URL'lerin proxy isteği denetleme hello rota şablonu tanımlar yanıt verir. Farklı olarak HTTP tetikleyicileri, varsayılan değer yoktur.
* **backendUri**: hello arka uç kaynak toowhich hello isteği hello URL'sini yönlendirilirken. Bu değer, uygulama ayarları ve parametreleri hello özgün istemci isteğinden başvurabilirsiniz. Bu özellik dahil edilmezse, Azure işlevlerinin bir HTTP 200 Tamam ile yanıt verir.
* **requestOverrides**: dönüşümleri toohello arka uç isteği tanımlayan bir nesne. Bkz: [requestOverrides nesnesi tanımlayın].
* **responseOverrides**: dönüşümleri toohello istemci yanıt tanımlayan bir nesne. Bkz: [responseOverrides nesnesi tanımlayın].

> [!NOTE] 
> Merhaba rota Özelliği Azure işlevleri proxy'leri hello işlevleri ana bilgisayar yapılandırmasının hello routeprefix öğesi özelliğini dikkate almaz. Tooinclude /api gibi bir önek istiyorsanız hello rota özelliğinde eklenmesi gerekir.

### <a name="requestOverrides"></a>RequestOverrides nesnesi tanımlayın

Merhaba requestOverrides nesnesi hello arka uç kaynak çağrıldığında toohello istek yapılan değişiklikleri tanımlar. Merhaba nesne hello aşağıdaki özelliklere göre tanımlanır:

* **backend.Request.Method**: Merhaba toocall hello arka uç kullanılan HTTP yöntemi.
* **backend.Request.QueryString. \<ParameterName\>**: hello çağrısı toohello arka uç için ayarlanabilir bir sorgu dizesi parametresi. Değiştir  *\<ParameterName\>*  tooset istediğiniz hello parametresinin hello ada sahip. Merhaba boş dize sağlanırsa, hello parametre hello arka uç isteği dahil edilmez.
* **backend.Request.Headers. \<HeaderName\>**: hello çağrısı toohello arka uç için ayarlanabilecek üstbilgi. Değiştir  *\<HeaderName\>*  tooset istediğiniz hello üstbilgisinin hello ada sahip. Merhaba boş dize sağlarsanız, hello üstbilgi hello arka uç isteği dahil edilmez.

Uygulama ayarları ve parametreleri değerleri hello özgün istemci isteğinden başvuruda bulunabilir.

Örnek bir yapılandırma hello şuna benzeyebilir:

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "backendUri": "https://<AnotherApp>.azurewebsites.net/api/<FunctionName>",
            "requestOverrides": {
                "backend.request.headers.Accept": "application/xml",
                "backend.request.headers.x-functions-key": "%ANOTHERAPP_API_KEY%"
            }
        }
    }
}
```

### <a name="responseOverrides"></a>ResponseOverrides nesnesi tanımlayın

Merhaba requestOverrides nesnesi geri toohello istemci geçti toohello yanıt yapılan değişiklikleri tanımlar. Merhaba nesne hello aşağıdaki özelliklere göre tanımlanır:

* **response.statusCode**: hello HTTP durum kodu toobe toohello istemci döndürdü.
* **response.statusReason**: hello HTTP neden tümcecik toobe toohello istemci döndürdü.
* **Response.body**: hello gövde toobe hello dize gösterimini toohello istemci döndürdü.
* **Response.Headers. \<HeaderName\>**: hello yanıt toohello istemci için ayarlanabilecek üstbilgi. Değiştir  *\<HeaderName\>*  tooset istediğiniz hello üstbilgisinin hello ada sahip. Merhaba boş dize sağlarsanız, hello üstbilgi hello yanıtta dahil edilmez.

Uygulama ayarları, hello özgün istemci istek parametrelerinden ve parametreleri değerleri hello arka uç yanıttan başvuruda bulunabilir.

Örnek bir yapılandırma hello şuna benzeyebilir:

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "responseOverrides": {
                "response.body": "Hello, {test}",
                "response.headers.Content-Type": "text/plain"
            }
        }
    }
}
```
> [!NOTE] 
> Bu örnekte, hello gövde doğrudan, bu nedenle Hayır ayarlı `backendUri` özelliği gereklidir. Merhaba örnek API'leri mocking için Azure işlevleri proxy'leri nasıl kullanacağınızı gösterir.

[Azure portal]: https://portal.azure.com
[HTTP Tetikleyicileri]: https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#http-trigger
[Modify hello back-end request]: #modify-backend-request
[Modify hello response]: #modify-response
[requestOverrides nesnesi tanımlayın]: #requestOverrides
[responseOverrides nesnesi tanımlayın]: #responseOverrides
[uygulama ayarları]: #use-appsettings
[değişkenlerini kullanın]: #using-variables
[hello özgün istemci istek parametrelerinden]: #request-parameters
[hello arka uç yanıt parametrelerinden]: #response-parameters
