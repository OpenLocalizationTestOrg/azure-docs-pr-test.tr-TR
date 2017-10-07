---
title: "İstemci sertifikası kimlik doğrulaması - Azure API Management kullanarak aaaSecure arka uç hizmetlerini | Microsoft Docs"
description: "Nasıl toosecure arka uç hizmetlerini kullanan istemci sertifikası kimlik Azure API Management hakkında bilgi edinin."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 43453331-39b2-4672-80b8-0a87e4fde3c6
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 565bb61044fed1158944202c36e8abe30edf5729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosecure-back-end-services-using-client-certificate-authentication-in-azure-api-management"></a>Nasıl toosecure arka uç hizmetlerini kullanan istemci sertifikası kimlik Azure API Management
API Management istemci sertifikalarını kullanan hello yetenek toosecure erişim toohello arka uç hizmetine bir API sağlar. Bu kılavuz toomanage hello API yayımcı portalında sertifikaları nasıl ve nasıl gösterir tooconfigure bir API toouse sertifika tooaccess onun arka uç hizmeti.

Merhaba API Management REST API kullanarak sertifikaların yönetilmesi hakkında daha fazla bilgi için bkz: [Azure API Management REST API sertifikası varlık][Azure API Management REST API Certificate entity].

## <a name="prerequisites"></a>Önkoşulları
Bu kılavuz size nasıl tooconfigure için arka uç hizmeti, API Management hizmet örneği toouse istemci sertifikası kimlik doğrulaması tooaccess hello gösterir. bir API. Bu konuda aşağıdaki hello adımları önce istemci sertifikası kimlik doğrulaması için yapılandırılmış, arka uç hizmetine sahip olmanız gerekir ([tooconfigure sertifika kimlik doğrulaması Azure Web sitelerine bakın toothis makale] [ tooconfigure certificate authentication in Azure WebSites refer toothis article]), ve erişim toohello sertifika ve hello hello API Management yayımcı portalında yüklemeyle hello sertifikanın parolasını sahiptir.

## <a name="step1"></a>Bir istemci sertifikasını karşıya yükle
başlatıldı, tooget tıklatın **yayımcı portalına** API Management hizmetiniz için hello Azure Portalı'nda. Bu toohello API Management yayımcı portalına götürür.

![API yayımcı portalı][api-management-management-console]

> Henüz bir API Management hizmeti örneği oluşturmadıysanız, bkz: [bir API Management hizmet örneği oluşturma] [ Create an API Management service instance] hello içinde [Azure API Management ile çalışmaya başlama] [ Get started with Azure API Management] Öğreticisi.
> 
> 

Tıklatın **güvenlik** hello gelen **API Management** hello sol ve tıklatın menüsünde **istemci sertifikalarını**.

![İstemci sertifikaları][api-management-security-client-certificates]

Yeni bir sertifika tooupload tıklatın **karşıya yükleme sertifika**.

![Sertifikayı karşıya yükleme][api-management-upload-certificate]

Tooyour sertifika göz atın ve sonra hello sertifikanın hello parola girin.

> Merhaba sertifika bulunmalıdır **.pfx** biçimi. Otomatik olarak imzalanan sertifikalar izin verilir.
> 
> 

![Sertifikayı karşıya yükleme][api-management-upload-certificate-form]

Tıklatın **karşıya** tooupload hello sertifika.

> Merhaba sertifika parolası şu anda doğrulanır. Yanlış ise, bir hata iletisi görüntülenir.
> 
> 

![Karşıya sertifika][api-management-certificate-uploaded]

Merhaba sertifika yüklendikten sonra üzerinde hello göründüğü **istemci sertifikalarını** sekmesi. Birden fazla sertifika varsa, hello konu not edin veya bir API toouse yapılandırma sertifikaları, olan kullanılan tooselect hello sertifika hello aşağıdakileri anlatıldığı gibi son dört karakterini hello parmak izi, hello [yapılandırma bir API toouse Ağ Geçidi kimlik doğrulaması için bir istemci sertifikası] [ Configure an API toouse a client certificate for gateway authentication] bölümü.

> Örneğin, kendinden imzalı bir sertifika kullanırken, sertifika zinciri doğrulamasını devre dışı tooturn olarak bu SSS'de açıklanan hello adımları izleyin [öğesi](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end).
> 
> 

## <a name="step1a"></a>Bir istemci sertifikası silme
bir sertifika toodelete tıklatın **silmek** hello istenen sertifika yanında.

![Sertifikayı Sil][api-management-certificate-delete]

Tıklatın **Evet, silmeden** tooconfirm.

![Silmeyi onayla][api-management-confirm-delete]

Merhaba sertifika bir API tarafından kullanılıyorsa, bir uyarı ekranı görüntülenir. Merhaba önce kaldırmalısınız toodelete hello sertifika sertifika yapılandırılmış toouse olan tüm API'lerinin bu.

![Silmeyi onayla][api-management-confirm-delete-policy]

## <a name="step2"></a>API toouse Ağ Geçidi kimlik doğrulaması için bir istemci sertifikası yapılandırma
Tıklatın **API'leri** hello gelen **API Management** hello menüsünde sol, istenen hello API hello adına tıklayın ve hello tıklatın **güvenlik** sekmesi.

![API Güvenlik][api-management-api-security]

Seçin **istemci sertifikalarını** hello gelen **kimlik bilgileriyle** aşağı açılan liste.

![İstemci sertifikaları][api-management-mutual-certificates]

Select hello hello istenen sertifika **istemci sertifikası** aşağı açılan liste. Birden fazla sertifika varsa hello önceki bölümde toodetermine hello doğru sertifikaya belirtildiği gibi hello parmak izi son dört karakterini hello veya hello konu arayın.

![Sertifika Seç][api-management-select-certificate]

Tıklatın **kaydetmek** toosave hello yapılandırma değişikliği toohello API.

> Bu değişikliği hemen etkili olur ve bu API toooperations kullanacağı çağrıları sertifika tooauthenticate hello arka uç sunucusunda hello.
> 
> 

![API Değişiklikleri Kaydet][api-management-save-api]

> Ağ Geçidi kimlik doğrulaması bir API için hello arka uç hizmeti için bir sertifika belirtildiğinde, bu API için hello ilkesinin bir parçası olur ve hello İlkesi Düzenleyicisi'nde görüntülenebilir.
> 
> 

![Sertifika İlkesi][api-management-certificate-policy]

## <a name="next-steps"></a>Sonraki adımlar
HTTP temel veya paylaşılan gizli kimlik doğrulaması gibi arka uç hizmetinizin diğer yolları toosecure hakkında daha fazla bilgi için aşağıdaki videoyu hello bakın.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Last-mile-Security/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-mutual-certificates/api-management-management-console.png
[api-management-security-client-certificates]: ./media/api-management-howto-mutual-certificates/api-management-security-client-certificates.png
[api-management-upload-certificate]: ./media/api-management-howto-mutual-certificates/api-management-upload-certificate.png
[api-management-upload-certificate-form]: ./media/api-management-howto-mutual-certificates/api-management-upload-certificate-form.png
[api-management-certificate-uploaded]: ./media/api-management-howto-mutual-certificates/api-management-certificate-uploaded.png
[api-management-api-security]: ./media/api-management-howto-mutual-certificates/api-management-api-security.png
[api-management-mutual-certificates]: ./media/api-management-howto-mutual-certificates/api-management-mutual-certificates.png
[api-management-select-certificate]: ./media/api-management-howto-mutual-certificates/api-management-select-certificate.png
[api-management-save-api]: ./media/api-management-howto-mutual-certificates/api-management-save-api.png
[api-management-certificate-policy]: ./media/api-management-howto-mutual-certificates/api-management-certificate-policy.png
[api-management-certificate-delete]: ./media/api-management-howto-mutual-certificates/api-management-certificate-delete.png
[api-management-confirm-delete]: ./media/api-management-howto-mutual-certificates/api-management-confirm-delete.png
[api-management-confirm-delete-policy]: ./media/api-management-howto-mutual-certificates/api-management-confirm-delete-policy.png



[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Azure API Management REST API Certificate entity]: http://msdn.microsoft.com/library/azure/dn783483.aspx
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[tooconfigure certificate authentication in Azure WebSites refer toothis article]: https://azure.microsoft.com/en-us/documentation/articles/app-service-web-configure-tls-mutual-auth/

[Prerequisites]: #prerequisites
[Upload a client certificate]: #step1
[Delete a client certificate]: #step1a
[Configure an API toouse a client certificate for gateway authentication]: #step2
[Test hello configuration by calling an operation in hello Developer Portal]: #step3
[Next steps]: #next-steps



