---
title: "hangi uygulamanın uygulama eklerken toouse yazın aaaHow toochoose | Microsoft Docs"
description: "Azure AD ile tümleştirebilir uygulamaları desteklenen hello türlerini anlamanız ve bunların ilgili yapılandırma seçenekleri"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 46e3672e7f5048b0fa54171f0fc169362c9d5ac6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toochoose-which-application-type-toouse-when-adding-an-application"></a>Nasıl toochoose hangi uygulamanın uygulama eklerken toouse yazın

Bu makalede toounderstand hello dört ana Azure AD ile tümleştirebilirsiniz uygulama türlerini yardımcı:

* Bunların her biri tarafından desteklenen özellikler
* Hangi uygulamanın neden seçebilirsiniz
* Bu uygulamanın çekirdek özellikleri nasıl tooconfigure ister nasıl kullanıcılardır **sağlanan**, veya ne **çoklu oturum açma** teknolojisi toouse.

## <a name="supported-application-types-in-azure-ad"></a>Azure AD'de desteklenen uygulama türleri

Kullanarak ekleyebileceğiniz azure AD destekler dört ana uygulama türleri hello **Ekle** özelliği bulunan altında **kurumsal uygulamalar**. Bunlar:

-   **Azure AD galeri uygulamaları** – bir tek oturum açma için Azure AD ile önceden tümleştirilmiş uygulama.

-   **Uygulama proxy'si uygulamalar** – tooprovide güvenli çoklu oturum açma tooexternally istediğiniz şirket içi ortamınızda çalışan bir uygulama.

-   **Özel geliştirilmiş uygulamaları** – üzerinde toodevelop kuruluşunuz isteyen bir uygulama hello Azure AD uygulama geliştirme platformu, ancak var henüz.

-   **Galeri olmayan uygulamaları** – kendi uygulamalarınızı Getir! İstediğiniz herhangi bir web bağlantıyı ya da bir kullanıcı adı ve parola alanı işleyen herhangi bir uygulama SAML veya Openıd Connect protokollerini destekler veya çoklu oturum açma için Azure AD ile toointegrate istediğiniz SCIM'yi destekler.

## <a name="features-and-capabilities-supported-by-all-hello-above-application-types"></a>Özellik ve tüm hello uygulama türleri yukarıda tarafından desteklenen yetenekler

Merhaba aşağıdaki özellikleri 4 uygulama türleri yukarıda hello hiçbiri tarafından Azure AD'de desteklenir:

-   **Hızlı Başlangıç** – izleyerek bir uygulama ile hızlı bir şekilde yapmalarını [basit dağıtım adımları](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications-getting-started)

-   **Genel Özellikler Yönetim** – alma bir [doğrudan ayrıntılı bağlantı](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users) tooan uygulama [hello marka özelleştirme](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-change-app-logo-user-azure-portal) bir uygulamanın veya [Merhaba uygulamasıdevredışıbırak](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) tüm kullanıcılar için.

-   **Kullanıcı ve Grup Yönetimi** – [atamak](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) veya [kaldırmak](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) kullanıcılar ve gruplar tooan uygulama ve isteğe bağlı olarak bu kullanıcılar ve gruplar erişiminiz Ata hello belirli uygulama rolleri

-   **Self Servis uygulamaya erişim** – kullanıcılar toorequest etkinleştirmek [Self Servis uygulamaya erişim](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) kendi uygulama erişimini tooan uygulamadan paneller ya da bir uygulama doğrudan ekleyerek veya [ Self Servis etkinleştirilmiş gruba katılıyor](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management), isteğe bağlı olarak hello boyunca iş onay gerektiren yolu

-   **Oturum açma günlükleri** – bkz [tüm oturum açma işlemleri tooan uygulama hello](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins), ya da tüm uygulamalarınızın

-   **Denetim günlükleri** – bkz [denetim günlüklerini değişiklikler tooan uygulama hakkında ayrıntılı](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs), veya tooall uygulamalarınızı

-   **Koşullu ve risk tabanlı erişim** – güçlü ayarlanmış [koşul tabanlı erişim kuralları](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access) kullanıcılar toosign tooa belirli uygulamasında çalıştığında uygulanır

-   **İzinleri Görünüm** – hello hiçbirini görüntülemek [OAuth2 izinleri](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent) bir uygulama dizininize erişim tooin, tek bir yerden sahiptir.

## <a name="single-sign-on-and-provisioning-modes-supported-by-specific-application-types"></a>Çoklu oturum açma ve belirli bir uygulama türleri tarafından desteklenen modları sağlama

Merhaba farklı çoklu oturum açma ve her uygulama türleri yukarıda hello tarafından desteklenen modları sağlama Hello tabloda açıklanmaktadır. Bu tablo toohelp kullanabileceğiniz hangi uygulamanın gereksinim toounderstand tooadd toosupport belirli bir amaca.

  ![Uygulama türleri tablosu](./media/application-tables/table1.png)

## <a name="how-toochoose-a-single-sign-on-mode"></a>Nasıl toochoose tek bir oturum açma modu

desteklenen hello **çoklu oturum açma** modları Azure AD uygulamaları için aşağıda listelenmiştir.

-   **Azure AD çoklu oturum açma devre dışı özelliğini** – Azure AD çoklu oturum açma devre dışı özelliğini seçin **tek oturum açma modu** , çoklu oturum açma ile Azure AD ile henüz hazır değil toointegrate misiniz veya onu yalnızca sınama

-   **Bağlantılı oturum açma** – hello seçin [bağlantılı oturum açma](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **tek oturum açma modu** mevcut tek oturum açma çözümüyle zaten bağlı olan bir uygulamanız varsa ya da yalnızca istiyorsanız Basit bir bağlantı, kullanıcılarınızın toopublish kendi [uygulama erişim Paneli'ne](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) veya [Office 365 uygulama Başlatıcı](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)

-   **Parola tabanlı oturum açma** – hello seçin [parola tabanlı oturum açma](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **tek oturum açma modu** uygulamanız bir HTML kullanıcı adı ve parola alanı oluşturur ve toostore istiyorsanız, Kullanıcı adı ve parola toobe güvenli bir şekilde yeniden toohello uygulamayı daha sonra

-   **SAML tabanlı oturum açma** – hello seçin [SAML tabanlı oturum açma](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) çoklu oturum açma, uygulamanızın hello SAML veya Openıd Connect protokollerini destekler veya toobe mümkün toomap kullanıcılar isterseniz modu toospecific uygulama rolleri dayalı Talep kuralları, SAML tanımladığınız *

   >[!NOTE]
   >Merhaba uygulama proxy'si bir uygulama için yapılandırıldığında, bu seçenek kullanılamaz.
   >
   >

-   **Üstbilgi tabanlı oturum açma** – bu seçin [üstbilgi tabanlı oturum açma](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) HTTP üstbilgisi destekleyen PingAccess kullanan bir uygulamanız varsa, tek oturum açma modu temel tooperform çoklu oturum üzerinde çok istediğiniz kimlik doğrulaması

   >[!NOTE]
   >Bu seçenek, yalnızca Hello uygulama proxy'si ve PingAccess yapılandırıldığında bir uygulama için kullanılabilir.
   >
   >

-   **Tümleşik Windows kimlik doğrulaması** – hello seçin [tümleşik Windows kimlik doğrulaması](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) çoklu oturum açma tooperform çoklu oturum üzerinde çok istediğiniz şirket içi WIA uygulamanın gösterme zaman modu

   >[!NOTE]
   >Bu seçenek, yalnızca Hello uygulama proxy'si bir uygulama için yapılandırıldığında kullanılabilir.
   >
   >

## <a name="single-sign-on-modes-for-custom-developed-applications"></a>Özel geliştirilmiş uygulamalar için çoklu oturum açma modları

Uygulamaları hello geliştirilen özel sahip [özel geliştirilmiş uygulama](#_Custom-Developed_Applications) deneyimi de Yukarıda listelenmeyen ek tek oturum açma modunu destekler. Bunlar:

-   [OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code) oturum açma tabanlı

-   [Openıd Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code) oturum açma tabanlı

-   [WS-Federasyon 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) oturum açma tabanlı

-   [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) oturum açma tabanlı

Okuma hello [Azure Active Directory Geliştirici Kılavuzu](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) toolearn nasıl bunlar destekleyen toocreate özel geliştirilmiş uygulama tek oturum açma modları hakkında daha fazla bilgi.

## <a name="how-tooset-an-applications-single-sign-on-mode"></a>Tooset bir uygulamanın nasıl tek oturum açma modu

tooset uygulamaya ait **çoklu oturum açma** modu, aşağıdaki hello yönergeleri izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.

5.  Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.

  * Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**

6.  Tooconfigure çoklu oturum açma istediğiniz hello uygulaması'nı seçin.

7.  Merhaba uygulamanın yüklediği sonra tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.

## <a name="how-toochoose-a-provisioning-mode"></a>Nasıl toochoose sağlama modu

-   **El ile sağlama** – hello seçin [el ile](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#provisioning-modes) hazırlama modu var olan hesapları varsa veya bu uygulamaları Azure AD dışında toomanage hesabı istiyor.

-   **Otomatik sağlama** – hello seçin [otomatik](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#configuring-automatic-user-account-provisioning) **sağlama modu** API tabanlı tooenable otomatik sağlama ve/veya XML'deki sağlanmasını istiyorsanız toothis kullanıcı hesapları Uygulama 

   >[!NOTE]
   >Bu seçenek yalnızca hello içinde uygulamaları için kullanılabilir **öne çıkan** hello kategorisini [Azure AD uygulama galerisinde](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#the-new-and-improved-application-gallery).
   >
   >

-   **Otomatik sağlama SCIM'yi tabanlı** – kullanmak [SCIM'yi tabanlı otomatik sağlamayı](https://docs.microsoft.com/azure/active-directory/active-directory-scim-provisioning) değişiklikleri toousers ve değişiklikleri otomatik olarak gösterilen grupları algılamak için uygulamanızın hello SCIM'yi Protokolü destekliyorsa Azure AD ile tümleşik tooany uygulama 

   >[!NOTE]
   >Bu seçenek, belirli bir sağlama modu olarak listelenmez, ancak Azure AD ile tümleşik tüm uygulamalar için varsayılan olarak etkindir.
   >
   >

## <a name="how-tooset-an-applications-provisioning-mode"></a>Nasıl tooset bir uygulama sağlama modunda

tooset uygulamaya ait **sağlama** modu, aşağıdaki hello yönergeleri izleyin:

tooset uygulamaya ait **çoklu oturum açma** modu, aşağıdaki hello yönergeleri izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.

5.  Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.

  * Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**

6.  Tooconfigure sağlama istediğiniz hello uygulaması'nı seçin.

7.  Merhaba uygulamanın yüklediği sonra tıklayın **sağlama** hello uygulamanın sol taraftaki gezinti menüsünde.

## <a name="next-steps"></a>Sonraki adımlar
[Azure Active Directory ile uygulamaları yönetme](active-directory-enable-sso-scenario.md)
