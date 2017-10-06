---
title: "Azure API Management'te OAuth 2.0 kullanan aaaAuthorize Geliştirici hesaplarını | Microsoft Docs"
description: "Bilgi nasıl API Management'te OAuth 2.0 kullanan tooauthorize kullanıcılar."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 78c48247-64f0-4708-b2d0-98b61a821283
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 934901dd6df399470a3257bf7a3a9b9fb5f40d5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthorize-developer-accounts-using-oauth-20-in-azure-api-management"></a>Nasıl tooauthorize Geliştirici kullanarak hesapları Azure API Management'te OAuth 2.0
Birçok API'lerini destekleyen [OAuth 2.0](http://oauth.net/2/) toosecure API hello ve yalnızca geçerli kullanıcıların erişimi vardır ve yalnızca kaynak toowhich erişebilir bunlar başlıklı emin olun. Sipariş toouse Azure API Management'ın etkileşimli Geliştirici konsolunda gibi API'leri ile tooconfigure sağlayan hello hizmeti API, hizmet örneği toowork OAuth 2.0 ile etkin.

## <a name="prerequisites"></a>Önkoşulları
Bu kılavuz size nasıl tooconfigure, API Management hizmet örneği toouse geliştirici için OAuth 2.0 yetkilendirme hesapları, nasıl göstermez gösterir, ancak tooconfigure bir OAuth 2.0 sağlayıcı. Başlangıç adımları benzerdir ve API Management hizmet örneği içinde OAuth 2.0 yapılandırmada kullanılan bilgi gerekli hello parçalarıdır rağmen farklı sağlayıcısıdır her OAuth 2.0 için Hello yapılandırması aynı hello. Bu konuda bir OAuth 2.0 sağlayıcısı olarak Azure Active Directory kullanan örnekler gösterilmektedir.

> [!NOTE]
> Azure Active Directory'yi kullanarak OAuth 2.0 yapılandırma hakkında daha fazla bilgi için bkz: Merhaba [WebApp GraphAPI DotNet] [ WebApp-GraphAPI-DotNet] örnek.
> 
> 

## <a name="step1"></a>Bir OAuth 2.0 yetkilendirme Sunucusu API yönetimini yapılandırma
başlatıldı, tooget tıklatın **yayımcı portalına** API Management hizmetiniz için hello Azure Portalı'nda.

![Yayımcı portalı][api-management-management-console]

> [!NOTE]
> Henüz bir API Management hizmeti örneği oluşturmadıysanız, bkz: [bir API Management hizmet örneği oluşturma] [ Create an API Management service instance] hello içinde [Azure API Management ile çalışmaya başlama] [ Get started with Azure API Management] Öğreticisi.
> 
> 

Tıklatın **güvenlik** hello gelen **API Management** hello sol, tıklatma menüsünden **OAuth 2.0**ve ardından **yetkilendirme Sunucusu Ekle**.

![OAuth 2.0][api-management-oauth2]

' I tıklattıktan sonra **yetkilendirme Sunucusu Ekle**, hello yeni yetkilendirme sunucusu form görüntülenir.

![Yeni Sunucu][api-management-oauth2-server-1]

Hello bir ad ve isteğe bağlı bir açıklama girin **adı** ve **açıklama** alanları. 

> [!NOTE]
> Bu alanları hello geçerli API Management hizmet örneği içinde kullanılan tooidentify hello OAuth 2.0 yetkilendirme sunucusu ve değerlerine hello OAuth 2.0 sunucudan gelen.
> 
> 

Merhaba girin **istemci kayıt sayfası URL'si**. Bu sayfa, kullanıcıların oluşturmak ve kendi hesaplarını yönetme içindir ve kullanılan hello OAuth 2.0 sağlayıcısına bağlı olarak değişir. Merhaba **istemci kayıt sayfası URL'si** toohello sayfasında, kullanıcıların noktaları toocreate kullanın ve kullanıcı hesaplarının yönetimini desteklemek için OAuth 2.0 sağlayıcıları kendi hesaplarını yapılandırın. Bazı kuruluşlar yapılandırmazsanız veya hello OAuth 2.0 sağlayıcı destekliyorsa olsa bile bu işlevi kullanın. OAuth 2.0 sağlayıcınız yapılandırılmış hesaplarının kullanıcı yönetimini yoksa, şirketinizin hello URL veya URL gibi burada yer tutucu URL gibi girin `https://placeholder.contoso.com`.

Merhaba form Hello sonraki bölümü içerir hello **yetki kodu izin türleri**, **yetkilendirme uç noktası URL'si**, ve **yetkilendirme isteği yöntemi** ayarlar.

![Yeni Sunucu][api-management-oauth2-server-2]

Merhaba belirtin **yetki kodu izin türleri** istenen hello türleri denetleyerek. **Yetkilendirme kodu** varsayılan olarak belirtilir.

Merhaba girin **yetkilendirme uç noktası URL'si**. Azure Active Directory'de, bu URL URL, aşağıdaki benzer toohello olacaktır nerede `<client_id>` uygulama toohello OAuth 2.0 sunucunuzu tanımlayan hello istemci kimliği ile değiştirilir.

`https://login.microsoftonline.com/<client_id>/oauth2/authorize`

Merhaba **yetkilendirme isteği yöntemi** hello yetkilendirme isteği toohello OAuth 2.0 sunucusu nasıl gönderileceğini belirtir. Varsayılan olarak **almak** seçilir.

Merhaba sonraki bölümde yaptığı hello **belirteç uç nokta URL'si**, **istemci kimlik doğrulama yöntemleri**, **yöntemi gönderme erişim belirteci**, ve **varsayılan kapsamı** belirtilir.

![Yeni Sunucu][api-management-oauth2-server-3]

Bir Azure Active Directory OAuth 2.0 sunucusu için hello **belirteç uç nokta URL'si** biçimi, aşağıdaki hello olacaktır nerede `<APPID>` hello biçimi olan `yourapp.onmicrosoft.com`.

`https://login.microsoftonline.com/<APPID>/oauth2/token`

Merhaba için varsayılan ayar **istemci kimlik doğrulama yöntemleri** olan **temel**, ve **yöntemi gönderme erişim belirteci** olan **Authorization Üstbilgisi**. Bu değerleri bu bölümde hello birlikte hello formunun yapılandırılmış **varsayılan kapsamı**.

Merhaba **istemci kimlik bilgileri** bölüm içerir hello **istemci kimliği** ve **gizli**, hello oluşturma ve yapılandırma sürecinde, OAuth 2.0 elde hangi Sunucu. Bir kez hello **istemci kimliği** ve **gizli** , hello belirtilen **redirect_uri** hello için **yetkilendirme kodu** oluşturulur. Bu URI kullanılan tooconfigure hello yanıt OAuth 2.0 server yapılandırmanızda URL'dir.

![Yeni Sunucu][api-management-oauth2-server-4]

Varsa **yetki kodu izin türleri** çok ayarlanır**kaynak sahibi parolası**, hello **kaynak sahibi parolası kimlik bilgileri** bölümdür kullanılan toospecify bu kimlik bilgileri; Aksi takdirde boş bırakabilirsiniz.

![Yeni Sunucu][api-management-oauth2-server-5]

Merhaba form tamamlandıktan sonra tıklatın **kaydetmek** toosave hello API Management OAuth 2.0 yetkilendirme sunucu yapılandırması. Merhaba sunucu yapılandırması kaydedildikten sonra bu yapılandırma, hello sonraki bölümde gösterildiği gibi API'leri toouse yapılandırabilirsiniz.

## <a name="step2"></a>API toouse OAuth 2.0 kullanıcı yetkilendirme yapılandırın
Tıklatın **API'leri** hello gelen **API Management** hello menüsünde sol, istenen hello API hello adına tıklayın,'ı tıklatın **güvenlik**ve ardından hello kutuyu için **OAuth 2.0**.

![Kullanıcı kimlik doğrulaması][api-management-user-authorization]

İstenen select hello **yetkilendirme sunucusu** hello aşağı açılan liste ve tıklatın **kaydetmek**.

![Kullanıcı kimlik doğrulaması][api-management-user-authorization-save]

## <a name="step3"></a>Test hello OAuth 2.0 kullanıcı yetkilendirme hello Geliştirici Portalı
OAuth 2.0 yetkilendirme sunucunuz yapılandırılmış ve bu sunucu, API toouse yapılandırılmış sonra test toohello Geliştirici Portalı giderek ve bir API çağırma.  Tıklatın **Geliştirici Portalı** hello sağ üst menüsündeki içinde.

![Geliştirici portalı][api-management-developer-portal-menu]

Tıklatın **API'leri** hello üst menü seçip **Echo API'si**.

![Echo API’si][api-management-apis-echo-api]

> [!NOTE]
> Yapılandırılmış tek bir API veya görünür tooyour hesabı, API'lere tıklamak sizi doğrudan bu API'nin toohello işlemlerine götürür varsa.
> 
> 

Select hello **GET kaynağı** işlemi, tıklatın **açık Konsolu**ve ardından **yetkilendirme kodu** hello açılan gelen.

![Konsolu açma][api-management-open-console]

Zaman **yetkilendirme kodu** olduğunu belirlenirse, bir açılır pencere hello oturum açma formunda hello OAuth 2.0 sağlayıcı ile görüntülenir. Bu örnekte hello oturum açma formu Azure Active Directory tarafından sağlanmıştır.

> [!NOTE]
> Açılır pencerelere varsa, gereken devre dışı tooenable istenir hello tarayıcı tarafından bunları. Bunları etkinleştirdikten sonra Seç **yetkilendirme kodu** yeniden ve hello oturum açma formu görüntülenir.
> 
> 

![Oturum aç][api-management-oauth2-signin]

Oturum açtıktan sonra hello **istek üst** ile doldurulan bir `Authorization : Bearer` hello isteği yetkilendirir üstbilgi.

![İstek üstbilgisi belirteci][api-management-request-header-token]

Bu noktada parametreleri kalan hello istenen hello değerlerini yapılandırmak ve hello isteği gönderin. 

## <a name="next-steps"></a>Sonraki adımlar
Merhaba aşağıdaki video ve eşlik eden OAuth 2.0 ve API Management kullanma hakkında daha fazla bilgi için bkz: [makale](api-management-howto-protect-backend-with-aad.md).

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Protecting-Web-API-Backend-with-Azure-Active-Directory-and-API-Management/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-oauth2/api-management-management-console.png
[api-management-oauth2]: ./media/api-management-howto-oauth2/api-management-oauth2.png
[api-management-user-authorization]: ./media/api-management-howto-oauth2/api-management-user-authorization.png
[api-management-user-authorization-save]: ./media/api-management-howto-oauth2/api-management-user-authorization-save.png
[api-management-oauth2-signin]: ./media/api-management-howto-oauth2/api-management-oauth2-signin.png
[api-management-request-header-token]: ./media/api-management-howto-oauth2/api-management-request-header-token.png
[api-management-developer-portal-menu]: ./media/api-management-howto-oauth2/api-management-developer-portal-menu.png
[api-management-open-console]: ./media/api-management-howto-oauth2/api-management-open-console.png
[api-management-oauth2-server-1]: ./media/api-management-howto-oauth2/api-management-oauth2-server-1.png
[api-management-oauth2-server-2]: ./media/api-management-howto-oauth2/api-management-oauth2-server-2.png
[api-management-oauth2-server-3]: ./media/api-management-howto-oauth2/api-management-oauth2-server-3.png
[api-management-oauth2-server-4]: ./media/api-management-howto-oauth2/api-management-oauth2-server-4.png
[api-management-oauth2-server-5]: ./media/api-management-howto-oauth2/api-management-oauth2-server-5.png
[api-management-apis-echo-api]: ./media/api-management-howto-oauth2/api-management-apis-echo-api.png


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API toouse OAuth 2.0 user authorization]: #step2
[Test hello OAuth 2.0 user authorization in hello Developer Portal]: #step3
[Next steps]: #next-steps

