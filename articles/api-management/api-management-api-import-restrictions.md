---
title: aaaRestrictions ve bilinen sorunlar Azure API Management API alma | Microsoft Docs
description: "Bilinen sorunlar ve Azure API Management hello açık API, WSDL veya WADL biçimlerini kullanarak içe kısıtlamalar ayrıntıları."
services: api-management
documentationcenter: 
author: mattfarm
manager: vlvinogr
editor: 
ms.assetid: 7a5a63f0-3e72-49d3-a28c-1bb23ab495e2
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: apipm
ms.openlocfilehash: 0bed5ace47de6ccbfbecba25ea6b69c5329de089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="api-import-restrictions-and-known-issues"></a>API içeri aktarma kısıtlamaları ve bilinen sorunlar
## <a name="about-this-list"></a>Bu liste hakkında
Her türlü çabayı tooensure yapılan sırada bu API'nizi Azure API Management alma olarak sorunsuzdur ve sorunsuz mümkün olduğunca biz bazen kısıtlamaları zorunlu tuttukları veya başarıyla içeri aktarmadan önce düzeltilinceye toobe gerektiren sorunları belirlemek. Bu makalede, bu belgeleri hello alma biçimini hello API tarafından organize.

## <a name="open-api"></a>API/Swagger açın
Açık API belgenizi alma hataları alıyorsanız, genel olarak, Lütfen, doğrulandı, - olun hello Tasarımcısını kullanarak, yeni Azure Portalı'nı (Tasarım - ön uç - açık API Belirtimi Düzenleyici) hello veya 3 ile aracı gibi taraf <a href="http://www.swagger.io"> Swagger Editor</a>.

* **Ana bilgisayar adı** biz bir ana bilgisayar adı özniteliği gerektirir.
* **Temel yolu** biz temel yolu özniteliği gerektirir.
* **Düzenleri** biz bir şema dizisi gerektirir. 

## <a name="wsdl"></a>WSDL
WSDL dosyaları kullanılan toogenerate SOAP doğrudan API'ları, ya bir SOAP ve REST API'si arka hello olarak.

* **WSDL: import** şu anda bu özniteliği kullanılarak API'leri desteklemiyoruz. Müşteriler, bir belgeye içe hello öğeleri birleştirmeniz gerekir.
* **Birden çok bölümü olan iletiler** şu anda desteklenmiyor.
* **WCF wsHttpBinding** Windows Communication Foundation ile oluşturulan SOAP Hizmetleri basicHttpBinding kullanması gereken - wsHttpBinding desteklenmiyor.
* **MTOM** MTOM kullanan hizmetler <em>olabilir</em> çalışır. Resmi desteği şu anda önerilmez.
* **Özyineleme** türlerini tanımlanan yinelemeli olarak (örneğin kendilerini tooan dizisi bakın) desteklenmez.

## <a name="wadl"></a>WADL
Şu anda hiçbir bilinen WADL alma sorunları vardır.


[api-management-management-console]: ./media/api-management-howto-add-operations/api-management-management-console.png
[api-management-operations]: ./media/api-management-howto-add-operations/api-management-operations.png
[api-management-add-operation]: ./media/api-management-howto-add-operations/api-management-add-operation.png
[api-management-http-method]: ./media/api-management-howto-add-operations/api-management-http-method.png
[api-management-url-template]: ./media/api-management-howto-add-operations/api-management-url-template.png
[api-management-url-template-rewrite]: ./media/api-management-howto-add-operations/api-management-url-template-rewrite.png
[api-management-description]: ./media/api-management-howto-add-operations/api-management-description.png
[api-management-caching-tab]: ./media/api-management-howto-add-operations/api-management-caching-tab.png
[api-management-request-parameters]: ./media/api-management-howto-add-operations/api-management-request-parameters.png
[api-management-request-body]: ./media/api-management-howto-add-operations/api-management-request-body.png
[api-management-response-code]: ./media/api-management-howto-add-operations/api-management-response-code.png
[api-management-response-body-content-type]: ./media/api-management-howto-add-operations/api-management-response-body-content-type.png
[api-management-response-body]: ./media/api-management-howto-add-operations/api-management-response-body.png


[api-management-contoso-api]: ./media/api-management-howto-add-operations/api-management-contoso-api.png

[api-management-add-new-api]: ./media/api-management-howto-add-operations/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-add-operations/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-add-operations/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-add-operations/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-add-operations/api-management-echo-operations.png

[Add an operation]: #add-operation
[Operation caching]: #operation-caching
[Request parameters]: #request-parameters
[Request body]: #request-body
[Responses]: #responses
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocache operation results in Azure API Management]: api-management-howto-cache.md
