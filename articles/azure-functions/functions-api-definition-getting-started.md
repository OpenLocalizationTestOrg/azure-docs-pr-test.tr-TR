---
title: "Azure işlevleri OpenAPI meta verilerle başlatıldı aaaGetting | Microsoft Docs"
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
ms.openlocfilehash: fee3464c9a0a11b6d3891ccd0e9c5343d6bedcad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-openapi-20-swagger-metadata-for-a-function-app-preview"></a>OpenAPI 2.0 (Swagger) oluşturma (Önizleme) bir işlev uygulaması için meta veriler

Bu belgede Azure işlevlerini barındırılan basit bir API için OpenAPI tanımı oluşturma hello adım adım sürecinde size kılavuzluk eder.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

### <a name="what-is-openapi-swagger"></a>OpenAPI (Swagger) nedir?
[Meta veri swagger](http://swagger.io/) hello işlevselliği tanımlayan bir dosyadır ve API'nizi modları işletim ve çeşitli diğer yazılımlar tarafından kullanılan REST API toobe barındıran bir işlev sağlar. Microsoft teklifleri ister PowerApps ve [API uygulamaları](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), gibi tooling 3 taraf geliştirici yanı sıra [Postman](https://www.getpostman.com/docs/importing_swagger) ve [pek çok daha fazla paket](http://swagger.io/tools/) tüm ile tüketilen, API toobe izin bir Swagger tanımı.

## <a name="prepare-function"></a>Bir işlev ile basit bir API oluşturma
  toocreate OpenAPI tanımı, ilk toocreate basit bir API işleviyle ihtiyacımız var. Bir işlev uygulaması üzerinde barındırılan bir API zaten varsa, düz toohello sonraki bölüme atlayabilirsiniz.
1. Yeni bir işlev uygulaması oluşturun.
    1. [Azure portal](https://portal.azure.com)  >  `+ New` > "İşlev uygulaması" için arama
1. Yeni işlev uygulamanız içinde yeni bir HTTP tetikleyicisi işlev oluştur
    1. İşlevinizi tanımlama çok basit bir REST API'si ile önceden doldurulmuş haldedir kodudur.
    1. "Hello {Giriş}" toohello işlevi hello gövdesinde veya bir sorgu parametresi olarak geçirilen herhangi bir dize döndürdü
1. Toohello Git `Integrate` yeni HTTP tetikleyicisini işlevinizi sekmesi
    1. İki durumlu `Allowed HTTP methods` çok`Selected methods`
    1. İçinde `Selected HTTP methods` her fiili POST dışında seçeneğinin işaretini kaldırın.
    ![Seçili HTTP yöntemleri](./media/functions-api-definition-getting-started/selectedHTTPmethods.png)
    1. Bu adım, daha sonra API tanımı basitleştirir.

## <a name="enable"></a>API tanımı desteğini etkinleştirme
1. Çok gidin`your function name` > `Platform Features` > `API Definition`
![tanım sekmesi](./media/functions-api-definition-getting-started/definitiontab.png)
1. Ayarlama `API Definition Source` çok`Function (preview)`
    1. Bu adım bir paketi bir uç nokta toohost işlevi uygulamanızın etki alanı, bir satır içi kopya hello OpenAPI dosyasından dahil olmak üzere, işlev uygulaması için OpenAPI seçeneklerini etkinleştirir [OpenAPI Düzenleyicisi](http://editor.swagger.io)ve bir hızlı başlangıç tanım Oluşturucu.
![Etkin tanımı](./media/functions-api-definition-getting-started/enabledefinition.png)

## <a name="create-definition"></a>Bir şablondan API tanımı oluşturma
1. Şuna tıklayın: `Generate API Definition template`
    1. Bu adım işlevi uygulamanız HTTP tetikleyicisini işlevleri için tarar ve functions.json toogenerate OpenAPI belge hello bilgilerinizi kullanır.
1. Bir işlem nesnesi çok ekleme`paths: /api/yourfunctionroute post:`
    1. tam bir OpenAPI Belge Anahattı Hello hızlı başlangıç OpenAPI belgedir. Daha fazla meta veri toobe işlemi nesneleri ve yanıt şablonlar gibi bir tam OpenAPI tanımı gerektirir.
    1. Hello örnek işlemi nesnesi aşağıdaki doldurulmuş bir bölüm oluşturur ve kullanır, bir parametre nesnesi ve yanıt nesnesi sahiptir.
    
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
    > Kullanıma [PowerApps için Swagger tanımı özelleştirme](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/) toolearn daha fazla.

1. Tıklatın `save` toosave değişikliklerinizi ![şablonu tanımını ekleme](./media/functions-api-definition-getting-started/addingtemplate.png)

## <a name="use-definition"></a>API tanımı kullanma
1. Kopyalama, `API definition URL` ham OpenAPI belgenizi yeni bir tarayıcı sekmesi tooview yapıştırın.
1. Test etme ve bu URL'yi kullanarak tümleştirme Araçlar OpenAPI belge tooany sayısı içeri aktarabilirsiniz.
    1. Çok sayıda Azure kullanarak OpenAPI belgenizi hello işlevi uygulama ayarlarınızı kaydedilmiş API tanımı URL'si mümkün tooautomatically alma kaynaklardır. Merhaba bir parçası olarak `Function` API tanımı kaynak, bu url, güncelleştiriyoruz.


## <a name="test-definition"></a>API tanımı Hello Swagger kullanıcı arabirimini tootest kullanma
Karışık hello API tanımı Düzenleyicisi toohello UI görünümü içinde yerleşik araçlarını var. test. API anahtarınızı ekleyin ve sonra hello `Try this operation` düğmesi her yöntemin altında. API tanımı tooformat hello isteklerinizi Hello aracı kullanır ve başarılı yanıtları tanımınızı doğru olduğunu gösterir.

### <a name="steps"></a>adımlar:

1. İşlev API anahtarınıza kopyalayın
    1. Merhaba API anahtarı HTTP tetikleyicisi işlevinizi altında bulunabilir `function name` > `Keys` > `Function Keys` 
   ![işlev tuşu](./media/functions-api-definition-getting-started/functionkey.png)
1. Toohello gidin `API Definition` sayfası.
    1. Tıklatın `Authenticate` ve işlev API anahtar toohello güvenlik nesnenizin hello üstüne ekleyin.
  ![OpenAPI anahtarı](./media/functions-api-definition-getting-started/definitionTest auth.png)
1. seçin`/api/yourfunctionroute` > `POST`
1. Tıklatın `Try it out` ve ad tootest girin
1. Başarı sonucu altında görmelisiniz `Pretty` 
 ![API tanımı test](./media/functions-api-definition-getting-started/definitionTest.png)

## <a name="next-steps"></a>Sonraki adımlar
* [OpenAPI tanımında işlevlerine genel bakış](functions-api-definition.md)
  * Merhaba OpenAPI desteği hakkında daha fazla bilgi için tam belgelerini okuyun.
* [Azure İşlevleri geliştirici başvurusu](functions-reference.md)  
  * İşlevleri kodlamak ve tetikleyicileri ve bağlamaları tanımlamak için programcı başvurusu
* [Azure İşlevleri GitHub deposu](https://github.com/Azure/Azure-Functions/)
  * Merhaba işlevleri GitHub toogive bize hello API tanımı destek Önizleme geribildirim bakın! GitHub sorunu güncelleştirilmiş toosee istediğiniz her şey için yapın.
