---
title: "aaaAPI uygulamaları giriş | Microsoft Docs"
description: "Azure App Service’in RESTful API’lerini geliştirmenize, barındırmanıza ve kullanmanıza nasıl yardımcı olduğunu öğrenin."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 60049a16-8159-47aa-a34b-110be0d8dab6
ms.service: app-service-api
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2016
ms.author: alkarche
ms.openlocfilehash: f066e96db667d4685480001bc43c2b1bff4ea352
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="api-apps-overview"></a>API Apps’e genel bakış
Daha kolay toodevelop olun Azure App Service teklif özellikleri API uygulamaları barındırmak ve hello Bulut ve şirket içi API'leri kullanır. API uygulamaları ile kurumsal düzeyde güvenlik, basit erişim denetimi, karma bağlantı, otomatik SDK oluşturma ve [Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md) ile sorunsuz tümleştirme elde edersiniz.

[Azure App Service](../app-service/app-service-value-prop-what-is.md) web, mobil ve tümleştirme senaryoları için tam yönetilen bir platformdur. API Apps, [Azure App Service](../app-service/app-service-value-prop-what-is.md) tarafından sunulan dört uygulama türünden biridir.

![Azure App Service’deki uygulama türleri](./media/app-service-api-apps-why-best-platform/appservicesuite.png)

## <a name="why-use-api-apps"></a>API Apps neden kullanılır?
API Apps’in önemli özelliklerinden bazıları şunlardır:

* **Mevcut API'nizi olarak Getir-olan** - hello hiçbirini kod toochange, varolan API'leri tootake avantajlarından API uygulamaları içinde yok--yalnızca kod tooan API uygulamanızı dağıtın. API’niz App Service tarafından desteklenen ASP.NET, C#, Java, PHP, Node.js ve Python gibi bir dili veya çerçeveyi kullanabilir.
* **Kolay kullanım** - [Swagger API’si meta verileri](http://swagger.io/) ile tümleşik destek, API’lerinizi çeşitli istemciler tarafından kullanılabilir hale getirir.  API’leriniz için C#, Java ve Javascript gibi çeşitli dillerde istemci kodlarını otomatik olarak oluşturun. Kodunuzu değiştirmeden [CORS](app-service-api-cors-consume-javascript.md)’u kolayca yapılandırın. Daha fazla bilgi için bkz. [API bulma ve kod oluşturma için App Service API Apps meta verileri](app-service-api-metadata.md) ve [CORS kullanarak JavaScript’ten bir API uygulaması kullanma](app-service-api-cors-consume-javascript.md). 
* **Basit erişim denetimi** -bir API uygulaması hiçbir değişiklik tooyour koduyla kimliği doğrulanmamış erişimden koruyun. Yerleşik kimlik doğrulama hizmetleri diğer hizmetlerin veya kullanıcıları temsil eden diğer istemcilerin erişimine karşı API'lerin güvenliğini sağlar. Desteklenen kimlik sağlayıcıları Azure Active Directory, Facebook, Twitter, Google ve Microsoft Hesabı’dır. İstemcileri, Active Directory Authentication Library (ADAL) veya hello Mobile Apps SDK'sını kullanabilirsiniz. Daha fazla bilgi için bkz. [Azure App Service’de API Apps için kimlik doğrulama ve yetkilendirme](app-service-api-authentication.md).
* **Visual Studio tümleştirmesi** -Visual Studio'daki ayrılmış Araçlar oluşturma, dağıtma, kullanma, hata ayıklama ve API uygulamaları yönetme hello işlemlerini kolaylaştırır. Daha fazla bilgi için bkz: [Announcing hello .NET için Azure SDK 2.8.1 ile](https://azure.microsoft.com/blog/announcing-azure-sdk-2-8-1-for-net/).
* **Logic Apps ile tümleştirme** - Oluşturduğunuz API uygulamaları [App Service Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md) tarafından kullanılabilir.  Daha fazla bilgi için bkz. [Logic Apps ile App Service üzerinde barındırılan özel API’nizi kullanma](../logic-apps/logic-apps-custom-hosted-api.md) ve [Yeni şema sürüm 2015-08-01-önizlemesi](../logic-apps/logic-apps-schema-2015-08-01.md).

Ayrıca, bir API uygulaması [Web Apps](../app-service-web/app-service-web-overview.md) ve [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) tarafından sunulan özelliklerden yararlanabilir. Merhaba ters doğruysa ayrıca: web uygulaması veya mobil uygulama toohost bir API kullanırsanız, bu istemci için Swagger meta verileri gibi API Apps özelliklerinden kod oluşturma ve CORS etki alanları arası tarayıcı erişimi için yararlanabilir. Merhaba hello üç uygulama türü (API, web, mobil) arasındaki tek fark hello adı ve hello Azure portalında bunlar için kullanılan simge konumudur.

## <a name="whats-hello-difference-between-api-apps-and-azure-api-management"></a>Merhaba API Apps ile Azure API Management arasındaki fark nedir?
API Apps ve [Azure API Management](../api-management/api-management-key-concepts.md) birbirini tamamlayan hizmetlerdir:

* API Management, API’lerin yönetilmesi ile ilgilidir. Bir API Management ön ucunu bir API toomonitor put ve kullanım azaltma, giriş ve çıkışı yönlendirmek, birkaç API bir uç noktada birleştirmek ve benzeri. Merhaba yönetilen API'ler herhangi bir yerde barındırılabilir.
* API Apps, API’lerin barındırılmasıyla ilgilidir. Merhaba hizmet, API'lerin geliştirilmesini ve kullanılmasını kolaylaştıran özellikler içerir, ancak bunu değil hello izleme, kısıtlama, düzenleme veya API Management algılamadığı birleştirerek tür. API Management özelliklerine ihtiyaç duymuyorsanız uygulamaları API Management kullanmadan API Uygulamaları içinde barındırabilirsiniz.

Aşağıdaki diyagram, API Uygulamaları ve diğer yerlerde barındırılan API’ler için kullanılan API Management’i göstermektedir.

![Azure API Management ve API Apps](./media/app-service-api-apps-why-best-platform/apia-apim.png)

API Management ve API Apps’in bazı özellikleri benzer işlevlere sahiptir.  Örneğin, her ikisi de CORS desteğini otomatik hale getirebilir. Merhaba iki hizmeti birlikte kullanıldığında, ön uç tooyour API apps hello olarak görev yaptığından API Management CORS için kullanırsınız. 

## <a name="getting-started"></a>Başlarken
Örnek kod tooone dağıtarak API Apps ile başlatılan tooget hello öğretici için tercih ettiğiniz çerçeveye bakın:

* [ASP.NET](app-service-api-dotnet-get-started.md) 
* [Node.js](app-service-api-nodejs-api-app.md) 
* [Java](app-service-api-java-api-app.md) 

API apps hakkında tooask sorular Başlat bir iş parçacığı hello [API Apps Forumunda](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureAPIApps). 

