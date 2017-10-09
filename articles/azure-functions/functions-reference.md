---
title: "Azure işlevleri geliştirmek için aaaGuidance | Microsoft Docs"
description: "Hello Azure işlevleri kavramlar ve teknikler toodevelop işlevlerinin Azure, tüm programlama dilleri ve bağlamaları gerektiğini öğrenin."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "Geliştirici Kılavuzu, azure işlevleri, İşlevler, olay işleme, Web kancalarını, dinamik işlem, sunucusuz mimarisi"
ms.assetid: d8efe41a-bef8-4167-ba97-f3e016fcd39e
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/30/2017
ms.author: chrande
ms.openlocfilehash: 86d37dae5333f615faafc966e9da6e08e0a6354e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-developers-guide"></a>Azure işlevleri Geliştirici Kılavuzu
Azure işlevleri, belirli işlevleri birkaç temel teknik kavramlar ve bileşenler hello dil veya kullandığınız bağlama bağımsız olarak paylaşın. Verilen dil veya bağlama ayrıntıları belirli tooa öğrenme moduna geçmek önce bunların tooall geçerlidir bu genel bakışta aracılığıyla emin tooread olun.

Bu makalede, zaten hello okuduğunuz varsayılır [Azure işlevlerine genel bakış](functions-overview.md) ve bilginiz [WebJobs SDK'sı kavramları Tetikleyicileri ve bağlamaları hello JobHost çalışma zamanı gibi](../app-service-web/websites-dotnet-webjobs-sdk.md). Azure işlevleri Web işleri SDK'si hello üzerinde dayanır. 

## <a name="function-code"></a>İşlev kodu
A *işlevi* Azure işlevlerinde hello birincil kavramdır. Kod bir işlev için tercih ettiğiniz dilde yazmak ve hello kodu kaydetmek ve yapılandırma dosyaları aynı klasörde hello. Merhaba yapılandırma adlandırılan `function.json`, JSON yapılandırma verilerini içerir. Çeşitli diller desteklenir ve her birinin biraz farklı deneyimi en iyi duruma getirilmiş toowork o dil için en iyi vardır. 

Merhaba function.json dosyası hello işlev bağlamaları ve diğer yapılandırma ayarlarını tanımlar. Bu dosya toodetermine hello olayları toomonitor ve yürütme toopass verisine ve dönüş verileri nasıl işlev Hello çalışma zamanı kullanır. Merhaba, function.json dosyası örneği verilmiştir.

```json
{
    "disabled":false,
    "bindings":[
        // ... bindings here
        {
            "type": "bindingType",
            "direction": "in",
            "name": "myParamName",
            // ... more depending on binding
        }
    ]
}
```

Set hello `disabled` özelliği çok`true` çalıştırılmasını tooprevent hello işlevi.

Merhaba `bindings` özelliktir burada Tetikleyicileri ve bağlamaları yapılandırın. Her bağlama birkaç genel ayarları ve belirli tooa bağlama belirli türdeki bazı ayarlar paylaşır. Her bağlama ayarları şu hello gerektirir:

| Özellik | Değerleri/türleri | Yorumlar |
| --- | --- | --- |
| `type` |Dize |Bağlama türü. Örneğin, `queueTrigger`. |
| `direction` |'in', 'out' |Merhaba bağlama alıcı hello işlevine veya gönderen verilerini hello işlevden için olup olmadığını gösterir. |
| `name` |Dize |Merhaba kullanılan hello adı veri hello işlevinde bağlı. C# ' ta bir bağımsız değişken adı budur; JavaScript için bir anahtar/değer listesi hello anahtarında kullanıcının. |

## <a name="function-app"></a>İşlev uygulaması
Bir işlev uygulaması birlikte Azure App Service tarafından yönetilen bir veya daha fazla tekil işlevler oluşur. Tüm hello işlevleri bir işlev uygulaması paylaşımda aynı fiyatlandırma planı, sürekli dağıtımı ve çalışma zamanı sürümü hello. Tüm hello paylaşır içinde birden çok dil can yazılmış işlevleri aynı uygulama işlevi. Bir işlev uygulaması bir şekilde tooorganize olarak düşünün ve topluca işlevlerinizi yönetin. 

## <a name="runtime-script-host-and-web-host"></a>Çalışma zamanı (komut dosyası ana bilgisayarı ve web ana bilgisayarı)
Merhaba çalışma zamanı ya da komut dosyası ana bilgisayarı, olaylarını dinler, toplar ve verileri gönderir ve sonuçta kodunuzun çalıştığı hello temel Web işleri SDK'si ana bilgisayardır. 

toofacilitate HTTP tetikleyiciler, ayrıca hello komut dosyası ana bilgisayarı üretim senaryolarında önünde tasarlanmış toosit olan bir web ana bilgisayarı vardır. İki ana sahip hello web ana bilgisayar tarafından yönetilen hello ön uç trafiğinden tooisolate hello komut dosyası ana bilgisayarı yardımcı olur.

## <a name="folder-structure"></a>Klasör yapısı
[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

Azure App Service'teki işlevleri tooa işlevi uygulamasına dağıtmak için bir proje ayarlama, bu klasör yapısı, site kodu olarak davranabilirsiniz. Sürekli tümleştirme ve dağıtım gibi mevcut araçlar kullanabilir veya özel dağıtım yapmak için komut dosyaları zaman paket yükleme dağıtmak veya transpilation kod.

> [!NOTE]
> Toodeploy emin olun, `host.json` dosya ve işlev klasörleri doğrudan toohello `wwwroot` klasör. Merhaba içermez `wwwroot` dağıtımlarınızı klasöründe. Aksi takdirde, şunun `wwwroot\wwwroot` klasörler. 
> 
> 

## <a id="fileupdate"></a>Nasıl tooupdate işlev uygulama dosyaları
Azure portal Hello yerleşik hello işlevi Düzenleyicisi hello güncelleştirme olanak tanır *function.json* dosyası ve bir işlev için hello kod dosyası. tooupload veya diğer güncelleştirme dosyaları gibi *package.json* veya *project.json* veya bağımlılıkları, diğer dağıtım yöntemleri toouse sahip.

Tüm hello için işlev uygulamalarının uygulama hizmeti üzerinde yerleşiktir [dağıtım seçenekleri kullanılabilir toostandard web uygulamaları](../app-service-web/web-sites-deploy.md) de işlevi uygulamaları için kullanılabilir. Burada, bazı yöntemler tooupload kullanın ya da güncelleştirme işlevi uygulama dosyaları bulunmaktadır. 

#### <a name="toouse-app-service-editor"></a>toouse App Service Düzenleyicisi
1. Hello Azure işlevleri Portalı'nda tıklatın **işlev uygulaması ayarları**.
2. Merhaba, **Gelişmiş ayarları** 'yi tıklatın **Git tooApp hizmet ayarlarını**.
3. Tıklatın **App Service Düzenleyicisi** uygulama menüsünden NAV altında **geliştirme araçları**.
4. tıklatın **Git**.
   
   Uygulama hizmeti Düzenleyicisi yüklendikten sonra hello görürsünüz *host.json* altındaki dosya ve işlev klasörleri *wwwroot*. 
5. Açık dosyaları tooedit bunları veya sürükleyip geliştirme makine tooupload dosyalarınızdan.

#### <a name="toouse-hello-function-apps-scm-kudu-endpoint"></a>toouse hello işlevi uygulamanın SCM (Kudu) uç noktası
1. Gidin: `https://<function_app_name>.scm.azurewebsites.net`.
2. Tıklatın **Debug konsol > CMD**.
3. Çok gidin`D:\home\site\wwwroot\` tooupdate *host.json* veya `D:\home\site\wwwroot\<function_name>` tooupdate bir işlevin dosyaları.
4. Sürükle ve bırak hello dosya kılavuzunda hello uygun klasöre tooupload istediğiniz bir dosya. Dosya burada bırakamazsınız hello dosya kılavuzunda iki alan vardır. İçin *.zip* dosyaları, bir kutusu hello etiketle görünür "tooupload buraya sürükleyin ve sıkıştırmasını açın." Diğer dosya türleri için hello dosya kılavuzunda ancak hello "sıkıştırmasını" kutusunu dışında bırakın.

<!--NOTE: I've removed documentation on FTP, because it does not sync triggers on hello consumption plan --DonnaM -->

#### <a name="toouse-continuous-deployment"></a>toouse sürekli dağıtım
Merhaba konudaki Hello yönergeleri [Azure işlevleri için sürekli dağıtım](functions-continuous-deployment.md).

## <a name="parallel-execution"></a>Paralel yürütme
Birden çok tetikleyici olaylar tek iş parçacıklı işlevi çalışma zamanı bunları işleyebileceğinden daha hızlı oluştuğunda hello çalışma zamanı hello işlevinde birden çok kez paralel çağırabilir.  Bir işlev uygulaması hello kullanıyorsanız [barındırma planı tüketim](functions-scale.md#how-the-consumption-plan-works), hello işlev uygulaması ölçek genişletme otomatik olarak.  Merhaba işlev uygulaması, her bir örneğini hello uygulama çalıştırıldığını barındırma planı veya bir normal tüketim hello [App Service barındırma planı](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md), eş zamanlı işlev çağrılarını birden çok iş parçacığı kullanma paralel işlem.  en fazla eş zamanlı işlev çağrılarını her işlevi app örneğindeki Hello hello işlev uygulaması içinde diğer işlevleri tarafından kullanılan hello kaynakları yanı sıra kullanılan tetikleyici hello türünü göre değişir.

## <a name="functions-runtime-versioning"></a>İşlevler çalışma zamanı sürüm oluşturma

Merhaba işlevleri çalışma zamanı hello kullanarak hello sürümü yapılandırabilirsiniz `FUNCTIONS_EXTENSION_VERSION` uygulama ayarı. Örneğin, "~ 1" Merhaba değeri işlevi uygulamanızı 1 kendi ana sürüm kullanacağını gösterir. En işlevi uygulamaları yükseltilmiş tooeach yeni alt sürümü bulunur. Hello hello işlevi uygulamanızı'nün tam sürümünü görüntüleyebilirsiniz **ayarları** hello Azure Portal sekmesindedir.

## <a name="repositories"></a>Depolar
Azure işlevleri Hello kodunu açık bir kaynaktır ve GitHub depolarının depolanır:

* [Azure işlevleri çalışma zamanı](https://github.com/Azure/azure-webjobs-sdk-script/)
* [Azure işlevleri portalına](https://github.com/projectkudu/AzureFunctionsPortal)
* [Azure işlevleri şablonları](https://github.com/Azure/azure-webjobs-sdk-templates/)
* [Azure Web işleri SDK'si](https://github.com/Azure/azure-webjobs-sdk/)
* [Azure Web işleri SDK'si uzantıları](https://github.com/Azure/azure-webjobs-sdk-extensions/)

## <a name="bindings"></a>Bağlamalar
Aşağıda, tüm desteklenen bağlamaları tablosu verilmiştir.

[!INCLUDE [dynamic compute](../../includes/functions-bindings.md)]

## <a name="reporting-issues"></a>Raporlama konuları
[!INCLUDE [Reporting Issues](../../includes/functions-reporting-issues.md)]

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi için kaynakları aşağıdaki hello bakın:

* [Azure İşlevleri için En İyi Uygulamalar](functions-best-practices.md)
* [Azure işlevleri C# Geliştirici Başvurusu](functions-reference-csharp.md)
* [Azure işlevleri F # Geliştirici Başvurusu](functions-reference-fsharp.md)
* [Azure işlevleri NodeJS Geliştirici Başvurusu](functions-reference-node.md)
* [Azure işlevleri Tetikleyicileri ve bağlamaları](functions-triggers-bindings.md)
* [Azure işlevleri: Gezisine hello](https://blogs.msdn.microsoft.com/appserviceteam/2016/04/27/azure-functions-the-journey/) hello Azure App Service ekip blogunda. Azure işlevlerinin nasıl geliştirilmiştir geçmişi.

