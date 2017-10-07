---
title: "Azure işlevleri aaaOpenAPI meta verilerde | Microsoft Docs"
description: "Azure işlevleri OpenAPI desteği'ne genel bakış"
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
ms.openlocfilehash: fff8f14110469a002a6c9dca03f641672003a3a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="openapi-20-metadata-support-in-azure-functions-preview"></a>OpenAPI 2.0 meta verileri desteği Azure işlevlerinde (Önizleme)
OpenAPI 2.0 (önceki adıyla Swagger) meta verileri desteği Azure işlevleri toowrite OpenAPI 2.0 tanımının bir işlev uygulaması içinde kullanabileceğiniz bir önizleme özelliği değil. Bu dosyayı hello işlev uygulaması kullanarak ardından barındırabilir.

[OpenAPI meta veri](http://swagger.io/) bir REST API toobe barındırma işlevi çok çeşitli diğer yazılımlar tarafından tüketilen sağlar. Bu yazılım Microsoft teklifleri PowerApps ve hello gibi içerir [Azure App Service API Apps özelliğini](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), üçüncü taraf geliştirici araçları ister [Postman](https://www.getpostman.com/docs/importing_swagger), ve [çok daha fazla paket](http://swagger.io/tools/).

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

>[!TIP]
>Merhaba ile başlayan öneririz [başlama Öğreticisi](./functions-api-definition-getting-started.md) ve belirli özellikler hakkında daha fazla toothis belge toolearn döndürüyor.

## <a name="enable"></a>OpenAPI tanımı desteğini etkinleştir
Merhaba tüm OpenAPI ayarlarını yapılandırabilirsiniz **API tanımı** işlevi uygulamanızın sayfa **Platform özellikleri**.

tooenable hello nesil barındırılan OpenAPI tanımı ve bir hızlı başlangıç tanımı ayarlamak **API tanımı kaynak** çok**işlevi (Önizleme)**. **Dış URL** işlevi toouse başka bir yerde barındırılan bir OpenAPI tanımlanmasına olanak tanır.

## <a name="generate-definition"></a>İşlevin meta verilerini Swagger çatıyı oluştur
Bir şablonu ilk OpenAPI tanımınızı yazma başlamanıza yardımcı olabilir. Hello tanımı şablon özelliği bir seyrek OpenAPI tanımı tüm hello meta veriler hello function.json dosyasında her bir HTTP tetikleyicisi işlevleri için kullanarak oluşturur. Merhaba, API hakkında daha fazla bilgi toofill gerekir [OpenAPI belirtimi](http://swagger.io/specification/), istek ve yanıt şablonlar gibi.

Adım adım yönergeler için bkz: Merhaba [başlama Öğreticisi](./functions-api-definition-getting-started.md).

### <a name="templates"></a>Kullanılabilir şablonlar

|Ad| Açıklama |
|:-----|:-----|
|Oluşturulan tanımı|OpenAPI tanımı hello işlevin varolan meta verilerini çıkarsanabileceği bilgilerinin hello maksimum tutar.|

### <a name="quickstart-details"></a>Oluşturulan hello tanımında dahil meta verileri

oluşturulan eşlenen toohello Swagger çatıyı olduğu gibi hello tablo temsil aşağıdaki Azure portal ayarları ve function.json karşılık gelen verileri hello.

|Swagger.JSON|Portal UI|Function.JSON|
|:----|:-----|:-----|
|[Ana bilgisayar](http://swagger.io/specification/#fixed-fields-15)|**İşlev uygulaması ayarları** > **App Service ayarlarını** > **genel bakış** > **URL'si**|*Mevcut değil*
|[Yolları](http://swagger.io/specification/#paths-object-29)|**Tümleştirme** > **seçili HTTP yöntemleri**|Bağlamaları: yol
|[Yol öğesi](http://swagger.io/specification/#path-item-object-32)|**Tümleştirme** > **rota şablonu**|Bağlamaları: yöntemler
|[Güvenlik](http://swagger.io/specification/#security-scheme-object-112)|**Anahtarları**|*Mevcut değil*|
|Operationıd *|**Rota + izin verilen fiiller**|Rota + izin verilen fiiller|

\*Merhaba işlem kimliği, yalnızca PowerApps ve akış ile tümleştirmek için gereklidir.
> [!NOTE]
> Merhaba x-ms-Özet uzantısı bir görünen ad mantıksal uygulamalar, PowerApps ve akış sağlar.
>
> toolearn daha, fazla [PowerApps için Swagger tanımı özelleştirme](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/).

## <a name="CICD"></a>CI/CD tooset bir API tanımı kullanın

 Kaynak denetimi toomodify API tanımınızı kaynak denetiminden etkinleştirmeden önce API tanımı hello Portalı'nda barındırma etkinleştirmeniz gerekir. Bu yönergeleri izleyin:

1. Çok Gözat**API tanımı (Önizleme)** işlevi uygulama ayarları'nda.
  1. Ayarlama **API tanımı kaynak** çok**işlevi**.
  1. Tıklatın **oluşturmak API tanımı şablonu** ve ardından **kaydetmek** toocreate daha sonra değiştirmek için bir şablon tanımı.
  1. API tanımı URL'si ve anahtar unutmayın.
1. [Sürekli Tümleştirme/sürekli dağıtım (CI/CD) ayarlayın.](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment#continuous-deployment-requirements).
2. Swagger.JSON \site\wwwroot adresindeki kaynak denetiminde değiştirme\.azurefunctions\swagger\swagger.json.

Şimdi, değişiklikleri tooswagger.json deponuzun işlevi uygulamanızı hello API tanımı URL'si tarafından barındırılan ve de not ettiğiniz anahtarı 1.c adım.

## <a name="next-steps"></a>Sonraki adımlar
* [Başlangıç Öğreticisi](functions-api-definition-getting-started.md). Bizim izlenecek toosee eylem OpenAPI tanımında deneyin.
* [Azure işlevleri GitHub deposunu](https://github.com/Azure/Azure-Functions/). Merhaba işlevleri depo toogive bize hello API tanımı destek Önizleme geribildirim denetleyin. GitHub sorunu herhangi bir şey için güncelleştirilmiş toosee istiyor olun.
* [Azure işlevleri Geliştirici Başvurusu](functions-reference.md). İşlevlerin kodlanması ve tetikleyicilerin ve bağlamaların tanımlanması hakkında bilgi edinin.
