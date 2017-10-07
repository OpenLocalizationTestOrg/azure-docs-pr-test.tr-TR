---
title: aaaHow toocreate Azure API Management API'leri
description: "Bilgi nasıl toocreate ve Azure API Management'te API'leri yapılandırın."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 14c20da4-f29f-4b28-bec7-3d4c50b734da
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 48ed8d93947253aa1e67ad995927ed6101cac072
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-apis-in-azure-api-management"></a>Nasıl toocreate Azure API Management API'leri
API Management bir API İstemci uygulamaları tarafından çağrılabilen işlemler kümesini temsil eder. Yeni API hello yayımcı portalında oluşturulur ve ardından operations eklenen hello istenen. Merhaba işlemleri eklendikten sonra hello API tooa ürün eklenir ve yayımlanabilir. Bir API yayımlandığında, geliştiriciler tarafından kullanılan abone tooand olabilir.

Bu kılavuz, hello işleminde hello ilk adımı gösterir: nasıl toocreate ve yeni bir API API Management içinde yapılandırın. Operations ekleme ve bir ürün yayımlama hakkında daha fazla bilgi için bkz: [nasıl tooadd işlemleri tooan API] [ How tooadd operations tooan API] ve [nasıl toocreate ürün ve yayımlama] [ How toocreate and publish a product].

## <a name="create-new-api"></a>Yeni bir API oluşturma
API oluşturulur ve hello yayımcı portalında yapılandırılır. tooaccess hello yayımcı portalı, tıklatın **yayımcı portalına** API Management hizmetiniz için hello Azure Portalı'nda.

![Yayımcı portalı][api-management-management-console]

> Henüz bir API Management hizmeti örneği oluşturmadıysanız, bkz: [bir API Management hizmet örneği oluşturma] [ Create an API Management service instance] hello içinde [Azure API Management ile çalışmaya başlama] [ Get started with Azure API Management] Öğreticisi.
> 
> 

Tıklatın **API'leri** hello gelen **API Management** sol hello ve ardından menüsünde **API ekleme**.

![API oluşturma][api-management-create-api]

Kullanım hello **yeni API ekleme** penceresi tooconfigure hello yeni API.

![Yeni API ekle][api-management-add-new-api]

alanları aşağıdaki hello kullanılan tooconfigure hello yeni API ' dir.

* **Web API adı** hello API için benzersiz ve açıklayıcı bir ad sağlar. Merhaba Geliştirici ve yayımcı portallarında görüntülenir.
* **Web hizmeti URL'si** başvuruları hello hello API uygulama HTTP hizmeti. API management toothis adresi isteklerini iletir.
* **Web API'si URL soneki** eklenmiş toohello temel hello API management hizmeti URL'sidir. Merhaba temel URL bir API Management hizmet örneği tarafından barındırılan tüm API'leri yaygındır. API Management API'leri kendi soneki ayırır ve bu nedenle hello soneki her API için belirtilen yayımcı için benzersiz olmalıdır.
* **Web API'si URL şeması** hangi protokollerin kullanılan tooaccess hello API olabileceğini belirler. HTTPs varsayılan olarak belirtilir.
* toooptionally bu yeni API tooa ürün eklemek için hello tıklatın **ürünler (isteğe bağlı)** açılır ve bir ürün seçin. Bu adım, yinelenen birden çok tooadd hello API toomultiple ürünleri kez olabilir.

Değerleri yapılandırılmış Hello istenen sonra tıklayın **kaydetmek**. Merhaba yeni API oluşturulduktan sonra hello hello API için Özet sayfasında hello yayımcı Portalı'nda görüntülenir.

![API özeti][api-management-api-summary]

## <a name="configure-api-settings"></a>API yapılandırma ayarları
Merhaba kullanabilirsiniz **ayarları** tooverify sekmesinde ve API hello yapılandırmasını düzenleyin. **Web API adı**, **Web hizmeti URL'si**, ve **Web API'si URL soneki** hello API oluşturulduğunda ve değiştirilebilir başlangıçta burada ayarlanır. **Açıklama** isteğe bağlı bir açıklama sağlar ve **Web API'si URL şeması** hangi protokollerin kullanılan tooaccess hello API olabileceğini belirler.

![API ayarları][api-management-api-settings]

tooconfigure ağ geçidi hello arka uç hizmeti için uygulama hello API, kimlik doğrulaması hello **güvenlik** sekmesini hello **kimlik bilgileriyle** açılan kullanılan tooconfigure olabilir **HTTP temel** veya **istemci sertifikalarını** kimlik doğrulaması. toouse HTTP temel kimlik doğrulaması, istenen hello kimlik bilgilerini girmeniz yeterlidir. İstemci sertifikası kimlik doğrulamasını kullanma hakkında daha fazla bilgi için bkz: [nasıl toosecure arka uç hizmetlerini kullanan istemci sertifikası kimlik Azure API Management'te][How toosecure back-end services using client certificate authentication in Azure API Management].

Merhaba **güvenlik** sekmesi ayrıca kullanılan tooconfigure olması **kullanıcı yetkilendirme** OAuth 2.0 kullanan. Daha fazla bilgi için bkz: [nasıl tooauthorize Geliştirici kullanarak hesapları Azure API Management'te OAuth 2.0][How tooauthorize developer accounts using OAuth 2.0 in Azure API Management].

![Temel kimlik doğrulama ayarları][api-management-api-settings-credentials]

Tıklatın **kaydetmek** toosave değişikliklerini API ayarları toohello yapın.

## <a name="next-steps"> </a>Sonraki adımlar
Bir API oluşturulduğunu ve yapılandırılan hello ayarları hello sonraki adımlar sonra tooadd hello işlemleri toohello API, hello API tooa ürün ekleme ve böylece geliştiriciler için kullanılabilir yayımlayın. Daha fazla bilgi için aşağıdaki makaleler hello bakın.

* [Nasıl tooadd işlemleri tooan API][How tooadd operations tooan API]
* [Nasıl toocreate ürün ve yayımlama][How toocreate and publish a product]

[api-management-create-api]: ./media/api-management-howto-create-apis/api-management-create-api.png
[api-management-management-console]: ./media/api-management-howto-create-apis/api-management-management-console.png
[api-management-add-new-api]: ./media/api-management-howto-create-apis/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-create-apis/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-create-apis/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-create-apis/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-create-apis/api-management-echo-operations.png

[What is an API?]: #what-is-api
[Create a new API]: #create-new-api
[Configure API settings]: #configure-api-settings
[Configure API operations]: #configure-api-operations
[Next steps]: #next-steps

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[How toosecure back-end services using client certificate authentication in Azure API Management]: api-management-howto-mutual-certificates.md
[How tooauthorize developer accounts using OAuth 2.0 in Azure API Management]: api-management-howto-oauth2.md
