---
title: "aaaHow toodetermine hangi çoklu oturum açma yöntemi toouse | Microsoft Docs"
description: "Azure AD tarafından desteklenen hello tek oturum açma modu anlamak ve nasıl için bir hangi toochoose hello uygulama toopick ilgilendiğiniz."
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
ms.openlocfilehash: 64f0bc1dc8281d1ab8222fd50eaceaf710704886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodetermine-what-single-sign-on-method-toouse"></a>Nasıl toodetermine hangi çoklu oturum açma yöntemi toouse

Bu makalede, Azure AD tarafından desteklenen toounderstand hello tek oturum açma modu Yardım ve nasıl için bir hangi toochoose hello uygulama toopick ilgilendiğiniz.

## <a name="single-sign-on-and-provisioning-modes-supported-by-specific-application-types"></a>Çoklu oturum açma ve belirli bir uygulama türleri tarafından desteklenen modları sağlama

Merhaba farklı çoklu oturum açma ve her uygulama türleri yukarıda hello tarafından desteklenen modları sağlama Hello tabloda açıklanmaktadır. Bu tablo toohelp kullanabileceğiniz hangi uygulamanın gereksinim toounderstand tooadd toosupport belirli bir amaca.

  ![AP türleri tablosu](./media/application-tables/table1.png)

## <a name="how-toochoose-a-single-sign-on-mode"></a>Nasıl toochoose tek bir oturum açma modu

desteklenen hello **çoklu oturum açma** modları Azure AD uygulamaları için aşağıda listelenmiştir.

-   **Azure AD çoklu oturum açma devre dışı özelliğini** – Azure AD çoklu oturum açma devre dışı özelliğini seçin **tek oturum açma modu** , çoklu oturum açma ile Azure AD ile henüz hazır değil toointegrate misiniz veya onu yalnızca sınama

-   **Bağlantılı oturum açma** – hello seçin [bağlantılı oturum açma](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **tek oturum açma modu** mevcut tek oturum açma çözümüyle zaten bağlı olan bir uygulamanız varsa ya da yalnızca istiyorsanız Basit bir bağlantı, kullanıcılarınızın toopublish kendi [uygulama erişim Paneli'ne](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) veya [Office 365 uygulama Başlatıcı](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)

-   **Parola tabanlı oturum açma** – hello seçin [parola tabanlı oturum açma](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **tek oturum açma modu** uygulamanız bir HTML kullanıcı adı ve parola alanı oluşturur ve toostore istiyorsanız, Kullanıcı adı ve parola toobe güvenli bir şekilde yeniden toohello uygulamayı daha sonra

-   **SAML tabanlı oturum açma** – hello seçin [SAML tabanlı oturum açma](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) çoklu oturum açma, uygulamanızın hello SAML veya Openıd Connect protokollerini destekler veya toobe mümkün toomap kullanıcılar isterseniz modu toospecific uygulama rolleri dayalı Talep kuralları, SAML tanımladığınız *(**Not:** hello uygulama proxy'si bir uygulama için yapılandırıldığında, bu seçenek kullanılamaz) *

-   **Üstbilgi tabanlı oturum açma** – bu seçin [üstbilgi tabanlı oturum açma](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) HTTP üstbilgisi destekleyen PingAccess kullanan bir uygulamanız varsa, tek oturum açma modu temel tooperform çoklu oturum üzerinde çok istediğiniz kimlik doğrulaması *(**Not:** bu seçenek yalnızca hello uygulama proxy'si ve PingAccess yapılandırıldığında bir uygulama için kullanılabilir) *

-   **Tümleşik Windows kimlik doğrulaması** – hello seçin [tümleşik Windows kimlik doğrulaması](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) çoklu oturum açma tooperform çoklu oturum üzerinde çok istediğiniz şirket içi WIA uygulamanın gösterme zaman modu*()*  *Not:** bu seçenek yalnızca hello uygulama proxy'si bir uygulama için yapılandırıldığında kullanılabilir) *

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

6.  Tooconfigure çoklu oturum açma hello uygulamasını seçin

7.  Merhaba uygulamanın yüklediği sonra tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.

## <a name="next-steps"></a>Sonraki adımlar
[Uygulama proxy'si ile çoklu oturum açma tooyour uygulamaları sağlayın](active-directory-application-proxy-sso-using-kcd.md)

