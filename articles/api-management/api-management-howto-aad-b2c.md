---
title: "Azure Active Directory B2C - Azure API Management kullanarak aaaAuthorize Geliştirici hesaplarını | Microsoft Docs"
description: "Bilgi nasıl API Management'te Azure Active Directory B2C kullanarak tooauthorize kullanıcılar."
services: api-management
documentationcenter: API Management
author: miaojiang
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
ms.openlocfilehash: 28f7cae53138938dbbc848b4afcbf08b72690e37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthorize-developer-accounts-by-using-azure-active-directory-b2c-in-azure-api-management"></a>Azure API Management'te Azure Active Directory B2C kullanarak tooauthorize Geliştirici nasıl hesapları
## <a name="overview"></a>Genel Bakış
Azure Active Directory B2C bir tüketiciye yönelik web ve mobil uygulamaları için bulut kimlik yönetimi çözümüdür. Toomanage erişim tooyour Geliştirici Portalı kullanabilirsiniz. Bu kılavuz, API Management hizmeti toointegrate Azure Active Directory B2C ile de gerekli yapılandırmayla hello gösterir. Klasik Azure Active Directory kullanılarak erişim toohello Geliştirici Portalı etkinleştirme hakkında daha fazla bilgi için bkz: [nasıl tooauthorize Geliştirici kullanarak hesapları Azure Active Directory].

> [!NOTE]
> Bu kılavuzdaki toocomplete hello adımları, öncelikle bir Azure Active Directory B2C Kiracı toocreate bir uygulama olması gerekir. Ayrıca, toohave kaydolma ve oturum açma ilkeleri hazır gerekir. Daha fazla bilgi için bkz: [Azure Active Directory B2C genel bakış].

## <a name="authorize-developer-accounts-by-using-azure-active-directory-b2c"></a>Azure Active Directory B2C kullanarak Geliştirici hesaplarını yetkilendirmede

1. başlatıldı, tooget tıklatın **yayımcı portalına** hello API Management hizmetiniz için Azure Portalı'nda. Bu toohello API Management yayımcı portalına götürür.

   ![Yayımcı portalı][api-management-management-console]

   > [!NOTE]
   > Henüz bir API Management hizmeti örneği oluşturmadıysanız, bkz: [bir API Management hizmet örneği oluşturma] [ Create an API Management service instance] hello içinde [Azure API Management öğreticiileçalışmayabaşlama][Get started with Azure API Management].

2. Merhaba üzerinde **API Management** menüsünde tıklatın **güvenlik**. Merhaba üzerinde **kimlikleri** sekmesinde, seçin **Azure Active Directory B2C**.

  ![Dış kimlikler 1][api-management-howto-aad-b2c-security-tab]

3. Merhaba Not **tekrar yönlendirme URL'sini** ve hello Azure portal'ın Active Directory B2C tooAzure üzerinden geçin.

  ![Dış kimlikler 2][api-management-howto-aad-b2c-security-tab-reply-url]

4. Merhaba tıklatın **uygulamaları** düğmesi.

  ![Yeni bir uygulama 1 kaydetme][api-management-howto-aad-b2c-portal-menu]

5. Merhaba tıklatın **Ekle** düğmesini toocreate yeni bir Azure Active Directory B2C uygulaması.

  ![Yeni bir uygulama 2 kaydetme][api-management-howto-aad-b2c-add-button]

6. Merhaba, **yeni uygulama** dikey penceresinde hello uygulama için bir ad girin. Seçin **Evet** altında **Web uygulaması/Web API**ve seçin **Evet** altında **örtük akışına izin**. Ardından kopya hello **tekrar yönlendirme URL'sini** hello gelen **Azure Active Directory B2C** hello bölümünü **kimlikleri** sekmesinde hello yayımcı Portalı'nda ve helloyapıştırma**Yanıt URL'si** metin kutusu.

  ![Yeni bir uygulamayı 3 Kaydet][api-management-howto-aad-b2c-app-details]

7. Merhaba tıklatın **oluşturma** düğmesi. Merhaba uygulaması oluşturulduğunda hello göründüğü **uygulamaları** dikey. Merhaba uygulama adı toosee ayrıntılarını'ı tıklatın.

  ![Yeni bir uygulama 4 kaydetme][api-management-howto-aad-b2c-app-created]

8. Merhaba gelen **özellikleri** dikey penceresinde, kopyalama hello **uygulama kimliği** toohello Pano.

  ![1 uygulama kimliği][api-management-howto-aad-b2c-app-id]

9. Geçiş geri toohello yayımcı portalı ve hello kimliği hello yapıştırma **istemci kimliği** metin kutusu.

  ![Uygulama kimliği 2][api-management-howto-aad-b2c-client-id]

10. Anahtarı geri toohello Azure portal, hello tıklatın **anahtarları** düğmesine tıklayın ve ardından **anahtar üret**. Tıklatın **kaydetmek** toosave hello yapılandırması ve görüntü hello **uygulama anahtarı**. Merhaba anahtar toohello panoya kopyalayın.

  ![1 uygulama anahtarı][api-management-howto-aad-b2c-app-key]

11. Anahtar geri toohello yayımcı portalı ve Yapıştır hello anahtara hello **gizli** metin kutusu.

  ![Uygulama anahtarı 2][api-management-howto-aad-b2c-client-secret]

12. Hello Azure Active Directory B2C kiracınızda Hello etki alanı adını belirtin **izin Kiracı**.

  ![İzin verilen Kiracı][api-management-howto-aad-b2c-allowed-tenant]

13. Merhaba belirtin **kaydolma İlkesi** ve **Signın İlkesi**. İsteğe bağlı olarak, ayrıca hello sağlayabilir **Profil Düzenleme İlkesi** ve **parola sıfırlama İlkesi**.

  ![İlkeler][api-management-howto-aad-b2c-policies]

  > [!NOTE]
  > İlkeler hakkında daha fazla bilgi için bkz: [Azure Active Directory B2C: Genişletilebilir ilke çerçevesini].

14. Merhaba istenen yapılandırma belirttikten sonra tıklatın **kaydetmek**.

  Hello değişiklikler kaydedildikten sonra geliştiriciler yeni hesapları mümkün toocreate olması ve Azure Active Directory B2C kullanarak toohello Geliştirici Portalı'nda oturum.

## <a name="sign-up-for-a-developer-account-by-using-azure-active-directory-b2c"></a>Azure Active Directory B2C kullanarak bir geliştirici hesabı için kaydolun

1. toosign Azure Active Directory B2C kullanarak bir geliştirici hesabı için yeni bir tarayıcı penceresi açın ve toohello Geliştirici portalına gidin. Merhaba tıklatın **kaydolun** düğmesi.

   ![Geliştirici Portalı 1][api-management-howto-aad-b2c-dev-portal]

2. İle toosign seçin **Azure Active Directory B2C**.

   ![Geliştirici Portalı 2][api-management-howto-aad-b2c-dev-portal-b2c-button]

3. Merhaba önceki bölümde yapılandırılmış yeniden yönlendirilen toohello kaydolma İlkesi demektir. Toosign e-posta adresinizi veya var olan sosyal hesaplarınızı birini kullanarak seçin.

   > [!NOTE]
   > Azure Active Directory B2C hello üzerinde etkin hello tek seçenek ise **kimlikleri** sekmesini hello yayımcı Portalı'nda, yeniden yönlendirilen toohello kaydolma İlkesi doğrudan olması.

   ![Geliştirici portalı][api-management-howto-aad-b2c-dev-portal-b2c-options]

   Merhaba kaydolma tamamlandığında yeniden yönlendirilen geri toohello Geliştirici Portalı demektir. API Management hizmet örneği için şimdi toohello Geliştirici Portalı'nda oturum açtınız.

    ![Kayıt tamamlandı][api-management-registration-complete]

## <a name="next-steps"></a>Sonraki adımlar

*  [Azure Active Directory B2C genel bakış]
*  [Azure Active Directory B2C: Genişletilebilir ilke çerçevesini]
*  [Azure Active Directory B2C, kimlik sağlayıcısı bir Microsoft hesabı kullanın]
*  [Azure Active Directory B2C, kimlik sağlayıcısı bir Google hesabı kullan]
*  [Azure Active Directory B2C, kimlik sağlayıcısı LinkedIn hesabını kullan]
*  [Azure Active Directory B2C, kimlik sağlayıcısı Facebook hesabıyla kullanın]




[api-management-howto-aad-b2c-security-tab]: ./media/api-management-howto-aad-b2c/api-management-b2c-security-tab.PNG
[api-management-howto-aad-b2c-security-tab-reply-url]: ./media/api-management-howto-aad-b2c/api-management-b2c-security-tab-reply-url.PNG
[api-management-howto-aad-b2c-portal-menu]: ./media/api-management-howto-aad-b2c/api-management-b2c-portal-menu.PNG
[api-management-howto-aad-b2c-add-button]: ./media/api-management-howto-aad-b2c/api-management-b2c-add-button.PNG
[api-management-howto-aad-b2c-app-details]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-details.PNG
[api-management-howto-aad-b2c-app-created]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-created.PNG
[api-management-howto-aad-b2c-app-id]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-id.PNG
[api-management-howto-aad-b2c-client-id]: ./media/api-management-howto-aad-b2c/api-management-b2c-client-id.PNG
[api-management-howto-aad-b2c-app-key]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-key.PNG
[api-management-howto-aad-b2c-app-key-saved]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-key-saved.PNG
[api-management-howto-aad-b2c-client-secret]: ./media/api-management-howto-aad-b2c/api-management-b2c-client-secret.PNG
[api-management-howto-aad-b2c-allowed-tenant]: ./media/api-management-howto-aad-b2c/api-management-b2c-allowed-tenant.PNG
[api-management-howto-aad-b2c-policies]: ./media/api-management-howto-aad-b2c/api-management-b2c-policies.PNG
[api-management-howto-aad-b2c-dev-portal]: ./media/api-management-howto-aad-b2c/api-management-b2c-dev-portal.PNG
[api-management-howto-aad-b2c-dev-portal-b2c-button]: ./media/api-management-howto-aad-b2c/api-management-b2c-dev-portal-b2c-button.PNG
[api-management-howto-aad-b2c-dev-portal-b2c-options]: ./media/api-management-howto-aad-b2c/api-management-b2c-dev-portal-b2c-options.PNG
[api-management-complete-registration]: ./media/api-management-howto-aad/api-management-complete-registration.PNG
[api-management-registration-complete]: ./media/api-management-howto-aad/api-management-registration-complete.png

[api-management-management-console]: ./media/api-management-howto-aad/api-management-management-console.png
[api-management-security-external-identities]: ./media/api-management-howto-aad/api-management-b2c-security-tab.png
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
[api-management-aad-app-multi-tenant]: ./media/api-management-howto-aad/api-management-aad-app-multi-tenant.png
[api-management-aad-reply-url]: ./media/api-management-howto-aad/api-management-aad-reply-url.png
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
[Azure Active Directory B2C genel bakış]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-overview
[nasıl tooauthorize Geliştirici kullanarak hesapları Azure Active Directory]: https://docs.microsoft.com/azure/api-management/api-management-howto-aad
[Azure Active Directory B2C: Genişletilebilir ilke çerçevesini]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-policies
[Azure Active Directory B2C, kimlik sağlayıcısı bir Microsoft hesabı kullanın]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-msa-app
[Azure Active Directory B2C, kimlik sağlayıcısı bir Google hesabı kullan]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-goog-app
[Azure Active Directory B2C, kimlik sağlayıcısı Facebook hesabıyla kullanın]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-fb-app
[Azure Active Directory B2C, kimlik sağlayıcısı LinkedIn hesabını kullan]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-li-app

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API toouse OAuth 2.0 user authorization]: #step2
[Test hello OAuth 2.0 user authorization in hello Developer Portal]: #step3
[Next steps]: #next-steps

[Log in toohello Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account
