---
title: "aaaCall, tetikleyin veya HTTP uç noktaları - Azure Logic Apps ile iş akışı iç içe | Microsoft Docs"
description: "HTTP uç noktaları toocall, tetikleyici veya iç içe iş akışları için Azure Logic Apps ayarlamanız"
services: logic-apps
keywords: "İş akışları, HTTP uç noktaları"
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 73ba2a70-03e9-4982-bfc8-ebfaad798bc2
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 03/31/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 072a314c3bff75ab7696f86bb063bb7c03c4ae89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="call-trigger-or-nest-workflows-with-http-endpoints-in-logic-apps"></a>HTTP uç noktaları logic apps içinde iş akışlarıyla iç içe veya, tetikleyici çağırın

Böylece tetiklemek veya mantıksal uygulamalarınızı bir URL yoluyla çağrı logic apps Tetikleyicileri olarak zaman uyumlu HTTP uç noktaları yerel getirebilir. Ayrıca, iş akışları aranabilir uç noktaları desenini kullanarak logic apps içinde yerleştirebilirsiniz.

toocreate HTTP uç noktaları, gelen istekleri mantıksal uygulamalarınızı alabilmesi tetikler ekleyebilirsiniz:

* [İstek](../connectors/connectors-native-reqres.md)

* [API bağlantı Web kancası](logic-apps-workflow-actions-triggers.md#api-connection-trigger)

* [HTTP Web kancası](../connectors/connectors-native-webhook.md)

   > [!NOTE]
   > Örneklerde hello kullansa da **isteği** tetikleyici, kullanabileceğiniz herhangi birini hello listelenen HTTP tetikleyiciler ve tüm ilkeler, toohello özdeş diğer tetikleyici türleri uygulanır..

## <a name="set-up-an-http-endpoint-for-your-logic-app"></a>Mantıksal uygulamanız için bir HTTP uç nokta ayarlama

bir HTTP uç noktası toocreate gelen istekleri alabilen tetikleyici ekleyin.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com "Azure portal"). Tooyour mantıksal uygulama gidin ve mantığı Uygulama Tasarımcısı'nı açın.

2. Gelen istekleri almak mantıksal uygulamanızı sağlayan bir tetikleyici ekleyin. Örneğin, hello ekleyin **isteği** tetikleyici tooyour mantıksal uygulama.

3.  Altında **iste gövde JSON şeması**, isteğe bağlı olarak bir JSON şeması hello tetikleyici tooreceive beklediğiniz hello için Yükü (veri) girebilirsiniz.

    Merhaba Tasarımcısı mantıksal uygulamanızı tooconsume, ayrıştırma ve hello tetikleyici, iş akışı aracılığıyla geçişi veriler kullanabileceğiniz belirteçleri oluşturmak için bu şemayı kullanır. 
    Hakkında daha fazla bilgi [JSON şemaları oluşturulan belirteçleri](#generated-tokens).

    Bu örnekte, hello Tasarımcısı'nda gösterilen hello şema girin:

    ```json
    {
      "type": "object",
      "properties": {
        "address": {
          "type": "string"
        }
      },
      "required": [
        "address"
      ]
    }
    ```

    ![Merhaba isteği Eylem Ekle][1]

    > [!TIP]
    > 
    > Örnek bir JSON yükü için bir şema gibi bir araçtan oluşturabileceğiniz [jsonschema.net](http://jsonschema.net/), veya hello **isteği** seçerek tetikleyici **kullanım örnek yükü toogenerate şeması**. 
    > Örnek yükünüzü girin ve seçin **Bitti**.

    Örneğin, bu örnek yükü:

    ```json
    {
       "address": "21 2nd Street, New York, New York"
    }
    ```

    Bu şemayı oluşturur:

    ```json
    }
       "type": "object",
       "properties": {
          "address": {
             "type": "string" 
          }
       }
    }
    ```

4.  Mantıksal uygulamanızı kaydedin. Altında **HTTP POST toothis URL**, artık bu örnek gibi bir oluşturulan geri çağırma URL'si bulmanız gerekir:

    ![Uç noktası için oluşturulan geri çağırma URL'si](./media/logic-apps-http-endpoint/generated-endpoint-url.png)

    Bu URL'yi bir paylaşılan erişim imzası (SAS) anahtarı kimlik doğrulaması için kullanılan hello sorgu parametrelerini içerir. 
    Hello Azure portal, mantığı uygulama genel bakış gelen hello HTTP uç noktası URL'si de alabilirsiniz. Altında **tetikleyici geçmişi**, tetikleyici seçin:

    ![Azure Portalı'ndan HTTP uç noktasının URL'sini alın][2]

    Veya bu çağrı yaparak hello URL alabilirsiniz:

    ```
    POST https://management.azure.com/{logic-app-resourceID}/triggers/{myendpointtrigger}/listCallbackURL?api-version=2016-06-01
    ```

## <a name="change-hello-http-method-for-your-trigger"></a>Tetikleyicinizin Hello HTTP yöntemini değiştirme

Varsayılan olarak, hello **isteği** tetikleyici bir HTTP POST isteği bekliyor, ancak farklı bir HTTP yöntemini kullanabilirsiniz. 

> [!NOTE]
> Yalnızca bir yöntem türü belirtebilirsiniz.

1. Üzerinde **isteği** tetikleyin, seçin **Gelişmiş Seçenekleri Göster**.

2. Açık hello **yöntemi** listesi. Bu örnek için select **almak** böylece HTTP uç noktanın URL'sini daha sonra test edebilirsiniz.

    > [!NOTE]
    > Herhangi bir HTTP yöntemini seçin veya özel bir yöntem için kendi mantıksal uygulama belirtin.

    ![HTTP yöntemini değiştirme](./media/logic-apps-http-endpoint/change-method.png)

## <a name="accept-parameters-through-your-http-endpoint-url"></a>HTTP uç nokta URL'nizi aracılığıyla parametreleri kabul et

HTTP uç noktası URL'si tooaccept parametrelerinizi istediğinizde, tetikleyicinin göreli yol özelleştirin.

1. Üzerinde **isteği** tetikleyin, seçin **Gelişmiş Seçenekleri Göster**. 

2. Altında **yöntemi**, istek toouse istediğiniz hello HTTP yöntemini belirtin. Bu örnekte, hello seçin **almak** böylece HTTP uç noktanın URL'sini test, yapmadıysanız yöntemi.

      > [!NOTE]
      > Tetikleyici için göreli bir yol belirttiğinizde, tetikleyici için bir HTTP yöntemini de açıkça belirtmeniz gerekir.

3. Altında **göreli yol**, URL'niz, örneğin, kabul etmelidir hello parametresi için göreli yol hello belirtin `customers/{customerID}`.

    ![Merhaba HTTP yöntemi ve parametresi için göreli yolunu belirtin](./media/logic-apps-http-endpoint/relativeurl.png)

4. toouse parametresi Merhaba, ekleme bir **yanıt** eylem tooyour mantıksal uygulama. (Seçin, tetikleyici altında **yeni adım** > **Eylem Ekle** > **yanıt**) 

5. Yanıt 's **gövde**, hello belirteci, tetikleyicinin göreli yolda belirtilen hello parametresi için içerir.

    Örneğin, tooreturn `Hello {customerID}`, yanıtın güncelleştirme **gövde** ile `Hello {customerID token}`. 
    Merhaba dinamik içerik listesinde görünür ve hello Göster `customerID` , tooselect için belirteç.

    ![Parametre tooresponse gövde ekleme](./media/logic-apps-http-endpoint/relativeurlresponse.png)

    **Gövde** bu örnekteki gibi görünmelidir:

    ![Yanıt gövdesi parametresi](./media/logic-apps-http-endpoint/relative-url-with-parameter.png)

6. Mantıksal uygulamanızı kaydedin. 

    HTTP uç nokta URL'nizi şimdi hello göreli yol, örneğin içerir: 

    HTTPS & # 58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...

7. HTTP uç noktası, kopyalama ve yapıştırma güncelleştirilmiş URL başka bir tarayıcı penceresine hello ancak Değiştir tootest `{customerID}` ile `123456`, ve Enter tuşuna basın.

    Tarayıcınız bu metin göstermesi gerekir: 

    `Hello 123456`

<a name="generated-tokens"></a>
### <a name="tokens-generated-from-json-schemas-for-your-logic-app"></a>Mantıksal uygulamanız için JSON şemaları üretilen belirteçleri

Bir JSON şeması sağladığınız zaman, **isteği** tetikleyin, hello mantığı Uygulama Tasarımcısı belirteçleri özellikleri için bu şemada oluşturur. Mantıksal uygulama akışı aracılığıyla veri geçirme daha sonra bu belirteçleri kullanabilirsiniz.

Merhaba eklerseniz, bu örneğin `title` ve `name` özellikleri tooyour JSON şeması, kendi belirteçleri daha sonraki iş akışı adımlarda kullanılabilir toouse sunulmuştur. 

Merhaba tam JSON şeması şöyledir:

```json
{
   "type": "object",
   "properties": {
      "address": {
         "type": "string"
      },
      "title": {
         "type": "string"
      },
      "name": {
         "type": "string"
      }
   },
   "required": [
      "address",
      "title",
      "name"
   ]
}
```

## <a name="create-nested-workflows-for-logic-apps"></a>Logic apps iç içe geçmiş iş akışları oluşturmak

İstekleri alabilen diğer mantıksal uygulamalar ekleyerek mantıksal uygulamanızı iş akışları yerleştirebilirsiniz. tooinclude bu mantığı uygulamalar ekleme hello **Azure Logic Apps - Logic Apps iş akışı seçin** eylem tooyour tetikleyici. Daha sonra uygun mantığı uygulamalardan seçebilirsiniz.

![Başka bir mantıksal uygulama Ekle](./media/logic-apps-http-endpoint/choose-logic-apps-workflow.png)

## <a name="call-or-trigger-logic-apps-through-http-endpoints"></a>HTTP uç noktaları aracılığıyla logic apps tetiklemek veya çağırın

HTTP uç noktanızı oluşturduktan sonra mantıksal uygulamanızı aracılığıyla tetikleyebilir bir `POST` yöntemi toohello tam URL. Logic apps doğrudan erişimli uç noktaları için yerleşik destek vardır.

## <a name="reference-content-from-an-incoming-request"></a>Gelen istek başvuru içeriği

Merhaba içerik türü kullanıcının ise `application/json`, hello gelen istekte özelliklerine başvurabilirsiniz. Aksi takdirde, içerik tooother API'leri geçirebilirsiniz tek bir ikili birim olarak kabul edilir. tooreference hello iş akışı içinde bu içerik, o içeriği dönüştürmeniz gerekir. Örneğin, geçirdiğiniz `application/xml` içerik, kullanabileceğiniz `@xpath()` bir XPath ayıklama için veya `@json()` XML tooJSON dönüştürmek için. Hakkında bilgi edinin [içerik türleriyle çalışma](../logic-apps/logic-apps-content-type.md).

tooget hello hello kullanabileceğiniz gelen isteğinden, çıktı `@triggerOutputs()` işlevi. Merhaba çıktı aşağıdaki örnekte olduğu gibi görünebilir:

```json
{
    "headers": {
        "content-type" : "application/json"
    },
    "body": {
        "myProperty" : "property value"
    }
}
```

tooaccess hello `body` özelliği özellikle kullanabileceğiniz hello `@triggerBody()` kısayol. 

## <a name="respond-toorequests"></a>Toorequests yanıt

Bir mantıksal uygulama içerik toohello çağıran döndürerek Başlat toorespond toocertain istekleri isteyebilirsiniz. tooconstruct hello durum kodu, başlığı ve yanıt için gövde hello kullanabilir **yanıt** eylem. Bu eylem yalnızca sonunda Merhaba, iş akışı mantığı uygulamanıza herhangi bir yerde görünebilir.

> [!NOTE] 
> Mantıksal uygulamanızı içermiyorsa bir **yanıt**, hello HTTP uç noktası yanıt *hemen* ile bir **202 kabul edilen** durumu. Ayrıca, hello özgün istek tooget hello yanıt için hello yanıt için gereken tüm adımları içinde hello bitmesi gereken [istek zaman aşımı sınırı](./logic-apps-limits-and-config.md) hello iş akışı iç içe geçmiş mantıksal uygulama olarak gerektirmediği sürece. Bu sınırı içinde yanıt meydana gelirse hello gelen istek zaman aşımına uğradı ve hello HTTP yanıtı alır **408 istemci zaman aşımı**. İç içe geçmiş logic apps için hello üst mantıksal uygulama toowait yanıt ne kadar zaman gerekli olduğuna bakılmaksızın, tamamlanana kadar devam eder.

### <a name="construct-hello-response"></a>Yapı hello yanıt

Merhaba yanıt gövdesi içinde birden fazla üst bilgi ve içerik herhangi bir türde içerebilir. Bizim örnek yanıt hello yanıt içerik türü var. hello üstbilgisini belirtir `application/json`. ve hello gövdesinde `title` ve `name`bağlı olarak daha önce hello için güncelleştirilmiş hello JSON şeması **isteği** tetikleyici.

![HTTP yanıtının eylem][3]

Yanıtları bu özelliklere sahiptir:

| Özellik | Açıklama |
| --- | --- |
| statusCode |Yanıt veren toohello gelen istek için Hello HTTP durum kodu belirtir. Bu kod 2xx, 4xx veya 5xx ile başlayan tüm geçerli durum kodu olabilir. Ancak, 3xx durum kodları izin verilmez. |
| Üstbilgileri |Herhangi bir sayıda üstbilgileri tooinclude hello yanıt olarak tanımlar. |
| Gövde |Bir dize olabilir bir gövde nesnesi, JSON nesnesi veya bir önceki adımda başvurulan bile ikili içerik belirtir. |

Gibi görünüyor şimdi hello için hangi hello JSON şeması işte **yanıt** eylem:

``` json
"Response": {
   "inputs": {
      "body": {
         "title": "@{triggerBody()?['title']}",
         "name": "@{triggerBody()?['name']}"
      },
      "headers": {
           "content-type": "application/json"
      },
      "statusCode": 200
   },
   "runAfter": {},
   "type": "Response"
}
```

> [!TIP]
> Merhaba mantığı Uygulama Tasarımcısı üzerinde mantıksal uygulamanızı tooview hello tam JSON tanımını seçin **kod görünümü**.

## <a name="q--a"></a>Soru-Cevap

#### <a name="q-what-about-url-security"></a>S: ne hakkında URL güvenlik?

Y: azure güvenli bir şekilde bir paylaşılan erişim imzası (SAS) kullanarak logic app geri çağırma URL'leri oluşturur. Bu imza sorgu parametresi olarak geçtiği ve mantıksal uygulamanızı tetikleyebilir önce doğrulanması gerekir. Azure mantıksal uygulama, hello Tetikleyici adı ve gerçekleştirilir hello işlemi başına gizli bir anahtar benzersiz bir birleşimini kullanarak hello imza oluşturur. Bu nedenle birisi erişim toohello gizli mantığı uygulama anahtarı olmadığı sürece, geçerli bir imzası oluşturulamaz.

   > [!IMPORTANT]
   > Üretim ve güvenli sistemler için mantıksal uygulamanızı doğrudan hello tarayıcıdan çünkü çağırma karşı önerilir:
   > 
   > * Merhaba paylaşılan erişim anahtarı hello URL'de görünür.
   > * Mantıksal uygulama müşterileri arasında güvenli içerik ilkeleri tooshared etki alanları nedeniyle yönetemez.

#### <a name="q-can-i-configure-http-endpoints-further"></a>S: daha fazla HTTP uç noktaları yapılandırabilir?

A: Evet HTTP uç noktaları aracılığıyla daha gelişmiş yapılandırma desteği [ **API Management**](../api-management/api-management-key-concepts.md). Tooconsistently yönetmek için mantıksal uygulamalar dahil olmak üzere tüm Apı'lerinizi, bu hizmet ayrıca hello özelliği sunar, özel etki alanı adlarını ayarlama, daha fazla kimlik doğrulama yöntemleri ve daha fazla bilgi, örneğin kullanın:

* [Değişiklik hello istek yöntemi](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#SetRequestMethod)
* [Merhaba URL kesimleri hello isteğinin değiştirme](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#RewriteURL)
* Merhaba, API Management etki alanlarında ayarlama [Azure portal](https://portal.azure.com/ "Azure portalı")
* Temel kimlik doğrulaması için ilke toocheck ayarlama

#### <a name="q-what-changed-when-hello-schema-migrated-from-hello-december-1-2014-preview"></a>S: Merhaba şema hello 1 Aralık 2014 Önizlemesi'nden geçirilen ne değiştirilir?

A: Bu değişiklikler hakkında bir özeti aşağıda verilmiştir:

| 1 Aralık 2014 Önizleme | 1 Haziran 2016 |
| --- | --- |
| Tıklatın **HTTP dinleyicisi** API uygulaması |Tıklatın **el ile tetikleyici** (hiçbir API uygulaması gereklidir) |
| HTTP dinleyicisi ayarı "*yanıt otomatik olarak gönderir*" |Ya da dahil bir **yanıt** eylemin hello iş akışı tanımı yer almıyor |
| Temel veya OAuth kimlik doğrulamasını yapılandırma |API Yönetimi |
| HTTP yöntemini yapılandırma |Altında **Gelişmiş Seçenekleri Göster**, bir HTTP yöntemini seçin |
| Göreli yolunu Yapılandır |Altında **Gelişmiş Seçenekleri Göster**, göreli bir yol ekleme |
| Başvuru hello gelen gövdesi aracılığıyla`@triggerOutputs().body.Content` |Aracılığıyla başvurusu`@triggerOutputs().body` |
| **HTTP yanıt gönderme** hello HTTP dinleyicisi eylemi |Tıklatın **yanıt tooHTTP isteği** (hiçbir API uygulaması gereklidir) |

## <a name="get-help"></a>Yardım alın

tooask sorular soruları ve hangi diğer Azure mantığı kullanıcılar gittiğini, uygulamaların ziyaret hello öğrenin [Azure Logic Apps Forumu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp Azure mantıksal uygulamaları ve bağlayıcıların geliştirmek, oy veya hello fikir gönderme [Azure Logic Apps kullanıcı geri bildirim sitesi](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Sonraki adımlar

* [Mantıksal uygulama tanımları yazma](./logic-apps-author-definitions.md)
* [Hataları ve özel durumları işleme](./logic-apps-exception-handling.md)

[1]: ./media/logic-apps-http-endpoint/manualtrigger.png
[2]: ./media/logic-apps-http-endpoint/manualtriggerurl.png
[3]: ./media/logic-apps-http-endpoint/response.png
