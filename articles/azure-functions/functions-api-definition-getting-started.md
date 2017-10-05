---
title: "Azure işlevleri OpenAPI meta veriler ile çalışmaya başlama | Microsoft Docs"
description: "Başlarken OpenAPI desteğiyle Azure işlevleri"
services: functions
documentationcenter: 
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 03/23/2017
ms.author: alkarche
ms.openlocfilehash: 9b861aacf31e17866293732dc2323f56014c1877
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="creating-openapi-20-swagger-metadata-for-a-function-app-preview"></a>OpenAPI 2.0 (Swagger) oluşturma (Önizleme) bir işlev uygulaması için meta veriler

Bu belgede Azure işlevlerini barındırılan basit bir API için OpenAPI tanımı oluşturma adım adım sürecinde size kılavuzluk eder.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

### <a name="what-is-openapi-swagger"></a>OpenAPI (Swagger) nedir?
[Meta veri swagger](http://swagger.io/) işlevsellik ve API'nizi işletim modlarını tanımlar ve çeşitli diğer yazılımlar tarafından kullanılması için bir REST API barındırma işlevi sağlayan bir dosyadır. Microsoft teklifleri ister PowerApps ve [API uygulamaları](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), gibi tooling 3 taraf geliştirici yanı sıra [Postman](https://www.getpostman.com/docs/importing_swagger) ve [pek çok daha fazla paket](http://swagger.io/tools/) tüm bir Swagger tanımı tüketilmesi API'nizi izin.

## <a name="prepare-function"></a>Bir işlev ile basit bir API oluşturma
  OpenAPI tanımı oluşturmak için önce bir işlevi basit bir API oluşturmak ihtiyacımız. Bir işlev uygulaması üzerinde barındırılan bir API zaten varsa, doğrudan bir sonraki bölüme atlayabilirsiniz.
1. Yeni bir işlev uygulaması oluşturun.
    1. [Azure portal](https://portal.azure.com)  >  `+ New` > "İşlev uygulaması" için arama
1. Yeni işlev uygulamanız içinde yeni bir HTTP tetikleyicisi işlev oluştur
    1. İşlevinizi tanımlama çok basit bir REST API'si ile önceden doldurulmuş haldedir kodudur.
    1. "Hello {Giriş}" sorgu parametresi olarak veya gövdedeki işleve herhangi bir dize döndürdü
1. Git `Integrate` yeni HTTP tetikleyicisini işlevinizi sekmesi
    1. İki durumlu `Allowed HTTP methods` için`Selected methods`
    1. İçinde `Selected HTTP methods` her fiili POST dışında seçeneğinin işaretini kaldırın.
    ![Seçili HTTP yöntemleri](./media/functions-api-definition-getting-started/selectedHTTPmethods.png)
    1. Bu adım, daha sonra API tanımı basitleştirir.

## <a name="enable"></a>API tanımı desteğini etkinleştirme
1. Gidin `your function name`  >  `Platform Features`  >  `API Definition` 
 ![tanım sekmesi](./media/functions-api-definition-getting-started/definitiontab.png)
1. Ayarlama `API Definition Source` için`Function (preview)`
    1. Bu adım bir paketi işlevi uygulamanızın etki alanı, bir satır içi kopyasını OpenAPI dosyasından barındırmak için bir uç nokta da dahil olmak üzere, işlev uygulaması için OpenAPI seçeneklerini etkinleştirir [OpenAPI Düzenleyicisi](http://editor.swagger.io)ve bir hızlı başlangıç tanım Oluşturucu.
![Etkin tanımı](./media/functions-api-definition-getting-started/enabledefinition.png)

## <a name="create-definition"></a>Bir şablondan API tanımı oluşturma
1. Şuna tıklayın: `Generate API Definition template`
    1. Bu adım işlevi uygulamanız HTTP tetikleyicisini işlevleri için tarar ve OpenAPI belge oluşturmak için functions.json bilgilerinizi kullanır.
1. İşlemi nesneye ekleme`paths: /api/yourfunctionroute post:`
    1. Hızlı Başlangıç OpenAPI tam OpenAPI Belge Anahattı belgedir. Daha fazla meta veri işlemi nesneleri ve yanıt şablonlar gibi bir tam OpenAPI tanımı olmasını gerektirir.
    1. Aşağıdaki örnek işlemi nesnesi doldurulmuş bir bölüm oluşturur ve kullanır, bir parametre nesnesi ve yanıt nesnesi vardır.
    
    ```yaml
      post:
        operationId: /api/yourfunctionroute/post
        consumes: [application/json]
        produces: [application/json]
        parameters:
          - name: name
            in: body
            description: Your name
            x-ms-summary: Your name
            required: true
            schema:
              type: object
              properties:
                name:
                  type: string
        description: >-
          Replace with Operation Object
          #http://swagger.io/specification/#operationObject
        responses:
          '200':
            description: A Greeting
            x-ms-summary: Your name
            schema:
              type: string
        security:
          - apikeyQuery: []
    ```
    
    > [!NOTE]
    >  x-ms-Özet bir görünen ad Logic Apps, akış ve PowerApps sağlar.
    >
    > Kullanıma [PowerApps için Swagger tanımı özelleştirme](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/) daha fazla bilgi için.

1. Tıklatın `save` yaptığınız değişiklikleri kaydetmek için ![şablonu tanımını ekleme](./media/functions-api-definition-getting-started/addingtemplate.png)

## <a name="use-definition"></a>API tanımı kullanma
1. Kopyalama, `API definition URL` ham OpenAPI belgeyi görüntülemek için yeni bir tarayıcı sekmesi yapıştırın.
1. Herhangi bir sayıda test etmek ve bu URL'yi kullanarak tümleştirme için Araçlar OpenAPI belgenizi aktarabilirsiniz.
    1. Çok sayıda Azure kaynaklarını OpenAPI belgenizi işlevi uygulama ayarlarınızı kaydedilmiş API tanımı URL'si kullanarak otomatik olarak içeri aktaramıyor. Bir parçası olarak `Function` API tanımı kaynak, bu url, güncelleştiriyoruz.


## <a name="test-definition"></a>API tanımı test etmek için Swagger kullanıcı arabirimini kullanma
Karışık API tanımı Düzenleyicisi'ni UI görünümüne yerleşik araçlar vardır test. API anahtarınızı ekleyin ve ardından `Try this operation` düğmesi her yöntemin altında. Araç API tanımı istekleri biçimlendirmek için kullanır ve başarılı yanıtları tanımınızı doğru olduğunu gösterir.

### <a name="steps"></a>adımlar:

1. İşlev API anahtarınıza kopyalayın
    1. API anahtarını HTTP tetikleyicisi işlevinizi altında bulunabilir `function name` > `Keys` > `Function Keys` 
   ![işlev tuşu](./media/functions-api-definition-getting-started/functionkey.png)
1. Gidin `API Definition` sayfası.
    1. Tıklatın `Authenticate` ve üst güvenlik nesnesine işlevi API anahtarınızı ekleyin.
  ![OpenAPI anahtarı](./media/functions-api-definition-getting-started/definitionTest auth.png)
1. seçin`/api/yourfunctionroute` > `POST`
1. Tıklatın `Try it out` ve test etmek için bir ad girin
1. Başarı sonucu altında görmelisiniz `Pretty` 
 ![API tanımı test](./media/functions-api-definition-getting-started/definitionTest.png)

## <a name="next-steps"></a>Sonraki adımlar
* [OpenAPI tanımında işlevlerine genel bakış](functions-api-definition.md)
  * OpenAPI desteği hakkında daha fazla bilgi için tam belgelerini okuyun.
* [Azure İşlevleri geliştirici başvurusu](functions-reference.md)  
  * İşlevleri kodlamak ve tetikleyicileri ve bağlamaları tanımlamak için programcı başvurusu
* [Azure İşlevleri GitHub deposu](https://github.com/Azure/Azure-Functions/)
  * API tanımı destek Önizleme'bize geri bildirim sağlamak için bu işlevler GitHub göz atın! GitHub sorunu görmek için güncelleştirilmiş istediğiniz her şey için yapın.
