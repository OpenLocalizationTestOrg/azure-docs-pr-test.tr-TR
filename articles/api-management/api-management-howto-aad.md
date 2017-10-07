---
title: "Azure Active Directory - Azure API Management kullanarak aaaAuthorize Geliştirici hesapları | Microsoft Docs"
description: "Bilgi nasıl tooauthorize kullanıcıları API Management'te Azure Active Directory kullanarak."
services: api-management
documentationcenter: API Management
author: steved0x
manager: erikre
editor: 
ms.assetid: 33a69a83-94f2-4e4e-9cef-f2a5af3c9732
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: ebf5447a509a47df35e4262138bfcf423cb1dd5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthorize-developer-accounts-using-azure-active-directory-in-azure-api-management"></a>Nasıl tooauthorize Geliştirici kullanarak hesapları Azure API Management'te Azure Active Directory
## <a name="overview"></a>Genel Bakış
Bu kılavuz size nasıl tooenable erişim toohello Geliştirici portalı kullanıcıları için Azure Active Directory'den gösterir. Bu kılavuz Ayrıca, Azure Active Directory Kullanıcıları içeren dış grupları ekleyerek toomanage grupları Azure Active Directory Kullanıcıları nasıl hello gösterir.

> toocomplete hello adımları bu kılavuzda, ilk Azure Active Directory hangi toocreate bir uygulama olmalıdır.
> 
> 

## <a name="how-tooauthorize-developer-accounts-using-azure-active-directory"></a>Nasıl tooauthorize Geliştirici kullanarak hesapları Azure Active Directory
başlatıldı, tooget tıklatın **yayımcı portalına** hello API Management hizmetiniz için Azure Portalı'nda. Bu toohello API Management yayımcı portalına götürür.

![Yayımcı portalı][api-management-management-console]

> Henüz bir API Management hizmeti örneği oluşturmadıysanız, bkz: [bir API Management hizmet örneği oluşturma] [ Create an API Management service instance] hello içinde [Azure API Management ile çalışmaya başlama] [ Get started with Azure API Management] Öğreticisi.
> 
> 

Tıklatın **güvenlik** hello gelen **API Management** hello sol ve tıklatın menüsünde **dış kimlikler**.

![Dış kimlikler][api-management-security-external-identities]

Tıklatın **Azure Active Directory**. Merhaba Not **tekrar yönlendirme URL'sini** ve hello Klasik Azure portalı, Azure Active Directory tooyour üzerinden geçin.

![Dış kimlikler][api-management-security-aad-new]

Merhaba tıklatın **Ekle** düğmesini toocreate yeni bir Azure Active Directory uygulaması ve seçin **kuruluşumun geliştirmekte olduğu bir uygulama Ekle**.

![Yeni bir Azure Active Directory uygulaması ekleyin][api-management-new-aad-application-menu]

Select hello uygulama için bir ad girin **Web uygulaması ve/veya Web API**ve hello İleri düğmesine tıklayın.

![Yeni Azure Active Directory uygulaması][api-management-new-aad-application-1]

İçin **oturum açma URL'si**, Geliştirici Portalı oturum açma hello URL'sini girin. Bu örnekte, hello **oturum açma URL'si** olan `https://aad03.portal.current.int-azure-api.net/signin`. 

Hello için **uygulama kimliği URL'si**hello varsayılan etki alanı veya özel bir etki alanı hello Azure Active Directory girin ve benzersiz bir dize tooit ekleyin. Bu örnekte, varsayılan etki alanı hello **https://contoso5api.onmicrosoft.com** hello sonek ile kullanılır **/api** belirtilen.

![Yeni Azure Active Directory uygulama özellikleri][api-management-new-aad-application-2]

Merhaba onay düğmesine toosave'ı tıklatın ve Merhaba uygulaması oluşturup toohello geçiş **yapılandırma** tooconfigure hello yeni uygulama sekmesinde.

![Oluşturulan yeni Azure Active Directory uygulaması][api-management-new-aad-app-created]

Birden çok Azure Active dizinleri bu uygulama için kullanılan toobe kullanacaksanız tıklatın **Evet** için **uygulamasıdır çok kiracılı**. Merhaba varsayılandır **Hayır**.

![Çok kiracılı uygulama][api-management-aad-app-multi-tenant]

Kopya hello **tekrar yönlendirme URL'sini** hello gelen **Azure Active Directory** hello bölümünü **dış kimlikler** sekmesinde hello yayımcı Portalı'nda ve helloyapıştırma**Yanıt URL'si** metin kutusu. 

![Yanıt URL'si][api-management-aad-reply-url]

Kaydırma toohello alt Merhaba yapılandırma sekmesi, select hello **uygulama izinleri** aşağı açılır ve denetleme **dizin verilerini okuma**.

![Uygulama izinleri][api-management-aad-app-permissions]

Select hello **temsilci izinleri** aşağı açılır ve denetleme **oturum açmayı etkinleştir ve kullanıcıların profilleri okuma**.

![Temsilci izinleri][api-management-aad-delegated-permissions]

> Uygulama ve temsilci izinleri hakkında daha fazla bilgi için bkz: [erişme hello grafik API'si][Accessing hello Graph API].
> 
> 

Kopya hello **istemci kimliği** toohello Pano.

![İstemci kimliği][api-management-aad-app-client-id]

Geri toohello yayımcı portalına geçin ve hello Yapıştır **istemci kimliği** hello Azure Active Directory Uygulama yapılandırmasından kopyalanır.

![İstemci kimliği][api-management-client-id]

Geçin geri toohello Azure Active Directory yapılandırması ve hello tıklatın **seçin süresi** hello açılan **anahtarları** bölüm ve bir aralık belirtin. Bu örnekte, **1 yıl** kullanılır.

![Anahtar][api-management-aad-key-before-save]

Tıklatın **kaydetmek** toosave hello yapılandırma ve görüntü hello anahtarı. Merhaba anahtar toohello panoya kopyalayın.

> Bu anahtarı not edin. Hello Azure Active Directory yapılandırması penceresini kapattığınızda hello anahtarı yeniden görüntülenemiyor.
> 
> 

![Anahtar][api-management-aad-key-after-save]

Anahtar geri toohello yayımcı portalı ve Yapıştır hello anahtara hello **gizli** metin kutusu.

![İstemci parolası][api-management-client-secret]

**Kiracılar izin** erişim toohello hello API Management hizmet örneği, API hangi dizinleri sahip belirtir. Merhaba toogrant erişim istediğiniz Azure Active Directory örnekleri toowhich Hello etki alanları belirtin. Birden çok etki alanı, satır başı, boşluk veya virgülle ayırabilirsiniz.

![İzin verilen kiracılar][api-management-client-allowed-tenants]


Yapılandırma belirtilen Hello istenen sonra tıklayın **kaydetmek**.

![Kaydet][api-management-client-allowed-tenants-save]

Azure Active Directory oturum açabilir toohello Geliştirici Portalı'nda hello adımları izleyerek hello hello kullanıcılar Hello değişiklikler kaydedildikten sonra belirtilen [toohello Geliştirici portalında bir Azure Active Directory hesabı kullanarak oturum] [Log in toohello Developer portal using an Azure Active Directory account].

Birden çok etki alanı hello belirtilebilir **izin kiracılar** bölümü. Merhaba uygulaması kaydedildiği hello özgün etki alanı farklı bir etki alanından herhangi bir kullanıcı oturum önce hello farklı etki alanının genel yönetici dizin verilerini hello uygulama tooaccess izni vermesi gerekir. toogrant izni hello genel yönetici çok gitmesini`https://<URL of your developer portal>/aadadminconsent` (örneğin, https://contoso.portal.azure-api.net/aadadminconsent) hello toogive erişim tooand istedikleri Active Directory Kiracı hello etki alanı adındaki türünü gönderme tıklatın. Merhaba aşağıdaki örnek, bir genel yönetici `miaoaad.onmicrosoft.com` toogive izin toothis belirli Geliştirici Portalı çalışıyor. 

![İzinler][api-management-aad-consent]

Merhaba sonraki ekranda, istendiğinde tooconfirm hello izin vermiş hello genel yönetici olacaktır. 

![İzinler][api-management-permissions-form]

> İçinde toolog izinleri önce genel bir yönetici tarafından verilen genel olmayan bir yönetici çalışırsa hello oturum açma denemesi başarısız olur ve hata ekranı görüntülenir.
> 
> 

## <a name="how-tooadd-an-external-azure-active-directory-group"></a>Tooadd dış Azure Active Directory Grup nasıl
Kullanıcılar Azure Active Directory erişimi etkinleştirdikten sonra API Management toomore Azure Active Directory gruplarına hello geliştiriciler hello grubundaki hello ilişkilendirme istenen hello ürünleri ile kolayca yönetmenize ekleyebilirsiniz.

> tooconfigure dış bir Azure Active Directory grubu olan hello Azure Active Directory ilk hello kimlikleri sekmesinde hello önceki bölümdeki hello yordamı izleyerek yapılandırılması gerekir. 
> 
> 

Dış Azure Active Directory grupları hello eklenen **görünürlük** toogrant erişim toohello grubu istediğiniz hello ürün sekmesinde. Tıklatın **ürünleri**ve ardından hello istenen ürün hello adına tıklayın.

![Ürünü yapılandırma][api-management-configure-product]

Geçiş toohello **görünürlük** sekmesine ve tıklayın **Azure Active Directory grupları Ekle**.

![Grupları Ekle][api-management-add-groups]

Select hello **Azure Active Directory Kiracısı** hello aşağı açılan liste ve hello istenen hello grubunda sonra tür hello adını **grupları** toobe metin kutusuna eklenir.

![Grup Seç][api-management-select-group]

Bu grup adı hello bulunabilir **grupları** hello aşağıdaki örnekte gösterildiği gibi Azure Active Directory için liste.

![Azure Active Directory grupları listesi][api-management-aad-groups-list]

Tıklatın **Ekle** toovalidate hello grup adı ve hello grubunu ekleyin. Bu örnekte, hello **Contoso 5 geliştiriciler** dış grubuna eklenir. 

![Eklenen grubu][api-management-aad-group-added]

Tıklatın **kaydetmek** toosave hello yeni Grup Seçimi.

Bir Azure Active Directory grubu bir üründen yapılandırıldıktan sonra kullanılabilir toobe üzerinde hello işaretli olduğu **görünürlük** sekmesini hello diğer ürünleri hello API Management hizmet örneği.

tooreview ve bunlar eklendikten sonra dış gruplar hello hello grubundan hello adını hello özelliklerini yapılandıramadı **grupları** sekmesi.

![Grupları yönetme][api-management-groups]

Buradan hello düzenleyebilirsiniz **adı** ve hello **açıklama** hello grubunun.

![Grubu Düzenle][api-management-edit-group]

Merhaba kullanıcılardan yapılandırılmış Azure Active Directory toohello Geliştirici Portalı ve görünümünde oturum ve görünürlük bölümden hello hello yönergeleri takip ederek sahip oldukları tooany grupları abone.

## <a name="how-toolog-in-toohello-developer-portal-using-an-azure-active-directory-account"></a>Nasıl toolog toohello Geliştirici portalında bir Azure Active Directory hesabı kullanarak
Merhaba önceki bölümlerde, yapılandırılmış bir Azure Active Directory hesabı kullanarak hello Geliştirici Portalı içine toolog hello kullanarak yeni bir tarayıcı penceresi açın **oturum açma URL'si** hello Active Directory Uygulama Yapılandırması ve tıklatın **Azure Active Directory**.

![Geliştirici Portalı][api-management-dev-portal-signin]

Azure Active Directory'yi hello kullanıcılar birini Hello kimlik bilgilerini girin ve tıklayın **oturum**.

![Oturum aç][api-management-aad-signin]

Ek bilgileri gerekiyorsa, Kayıt formuyla istenebilir. Merhaba kayıt formunu tamamladıktan ve tıklayın **kaydolun**.

![Kayıt][api-management-complete-registration]

Kullanıcı artık hello Geliştirici Portalı, API Management hizmet örneğinizin içine kaydedilir.

![Kayıt tamamlandı][api-management-registration-complete]

[api-management-management-console]: ./media/api-management-howto-aad/api-management-management-console.png
[api-management-security-external-identities]: ./media/api-management-howto-aad/api-management-security-external-identities.png
[api-management-security-aad-new]: ./media/api-management-howto-aad/api-management-security-aad-new.png
[api-management-new-aad-application-menu]: ./media/api-management-howto-aad/api-management-new-aad-application-menu.png
[api-management-new-aad-application-1]: ./media/api-management-howto-aad/api-management-new-aad-application-1.png
[api-management-new-aad-application-2]: ./media/api-management-howto-aad/api-management-new-aad-application-2.png
[api-management-new-aad-app-created]: ./media/api-management-howto-aad/api-management-new-aad-app-created.png
[api-management-aad-app-permissions]: ./media/api-management-howto-aad/api-management-aad-app-permissions.png
[api-management-aad-app-client-id]: ./media/api-management-howto-aad/api-management-aad-app-client-id.png
[api-management-client-id]: ./media/api-management-howto-aad/api-management-client-id.png
[api-management-aad-key-before-save]: ./media/api-management-howto-aad/api-management-aad-key-before-save.png
[api-management-aad-key-after-save]: ./media/api-management-howto-aad/api-management-aad-key-after-save.png
[api-management-client-secret]: ./media/api-management-howto-aad/api-management-client-secret.png
[api-management-client-allowed-tenants]: ./media/api-management-howto-aad/api-management-client-allowed-tenants.png
[api-management-client-allowed-tenants-save]: ./media/api-management-howto-aad/api-management-client-allowed-tenants-save.png
[api-management-aad-delegated-permissions]: ./media/api-management-howto-aad/api-management-aad-delegated-permissions.png
[api-management-dev-portal-signin]: ./media/api-management-howto-aad/api-management-dev-portal-signin.png
[api-management-aad-signin]: ./media/api-management-howto-aad/api-management-aad-signin.png
[api-management-complete-registration]: ./media/api-management-howto-aad/api-management-complete-registration.png
[api-management-registration-complete]: ./media/api-management-howto-aad/api-management-registration-complete.png
[api-management-aad-app-multi-tenant]: ./media/api-management-howto-aad/api-management-aad-app-multi-tenant.png
[api-management-aad-reply-url]: ./media/api-management-howto-aad/api-management-aad-reply-url.png
[api-management-aad-consent]: ./media/api-management-howto-aad/api-management-aad-consent.png
[api-management-permissions-form]: ./media/api-management-howto-aad/api-management-permissions-form.png
[api-management-configure-product]: ./media/api-management-howto-aad/api-management-configure-product.png
[api-management-add-groups]: ./media/api-management-howto-aad/api-management-add-groups.png
[api-management-select-group]: ./media/api-management-howto-aad/api-management-select-group.png
[api-management-aad-groups-list]: ./media/api-management-howto-aad/api-management-aad-groups-list.png
[api-management-aad-group-added]: ./media/api-management-howto-aad/api-management-aad-group-added.png
[api-management-groups]: ./media/api-management-howto-aad/api-management-groups.png
[api-management-edit-group]: ./media/api-management-howto-aad/api-management-edit-group.png

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
[Accessing hello Graph API]: http://msdn.microsoft.com/library/azure/dn132599.aspx#BKMK_Graph

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API toouse OAuth 2.0 user authorization]: #step2
[Test hello OAuth 2.0 user authorization in hello Developer Portal]: #step3
[Next steps]: #next-steps

[Log in toohello Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account

