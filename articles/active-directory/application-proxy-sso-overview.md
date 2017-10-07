---
title: "Azure AD uygulama proxy'si için SSO aaaManage | Microsoft Docs"
description: "Merhaba temelleri uygulama proxy'si ile çoklu oturum açma hakkında bilgi edinin"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: a278751a5cb1bf98c970a4e5d2eb3edc3b784096
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-ad-application-proxy-provide-single-sign-on"></a>Azure AD uygulama proxy'si nasıl çoklu oturum açma sağlar?

Çoklu oturum açma bir anahtar Azure AD uygulama proxy'si öğesidir.  Kullanıcılarınız yalnızca toosign tooAzure hello bulutta Active Directory içinde olduğundan hello en iyi kullanıcı deneyimi sağlar. TooAzure Active Directory kimlik doğrulaması sonra hello uygulama ara sunucusu Bağlayıcısı hello kimlik doğrulama toohello şirket içi uygulama işler. Merhaba arka uç uygulaması uzak bir kullanıcı uygulama proxy'si ve etki alanına katılmış bir cihazda normal kullanım aracılığıyla oturum açmayı hello birbirinden bildiremez. 

Azure Active Directory toouse tek oturum açma tooyour uygulamalar için gereksinim duyduğunuz tooselect **Azure Active Directory** hello ön kimlik doğrulama yöntemi olarak. Seçerseniz **geçiş** kullanıcılarınızın tooAzure Active Directory hiç kimlik doğrulaması yok ancak yönlendirilmiş düz toohello uygulamasıdır. Bu ayar, önce bir uygulama yayımlamak veya tooyour uygulamada hello Azure portalına gidin ve hello uygulama Proxy ayarlarını düzenleyin yapılandırabilirsiniz. 

toosee, çoklu oturum açma seçenekleri, şu adımları izleyin:

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Çok gidin**Azure Active Directory** > **kurumsal uygulamalar** > **tüm uygulamaları**.
3. Çoklu oturum açma seçeneklerini seçin hello uygulama toomanage istiyor.
4. Seçin **çoklu oturum açma**.

   ![SSO açılır menü](./media/application-proxy-sso-overview/single-sign-on-mode.png)

Merhaba açılır menüsünde, tek oturum açma tooyour uygulama için beş seçenekleri gösterir:

* Azure AD çoklu oturum açma devre dışı özelliğini
* Parola tabanlı oturum açma
* Bağlantılı oturum açma
* Tümleşik Windows kimlik doğrulaması
* Üstbilgi tabanlı oturum açma

## <a name="azure-ad-single-sign-on-disabled"></a>Azure AD çoklu oturum açma devre dışı özelliğini

Çoklu oturum açma tooyour uygulaması için Azure Active Directory Tümleştirme toouse istemiyorsanız seçin **Azure AD çoklu oturum açma devre dışı özelliğini**. Bu seçenek ile kullanıcılarınızın iki kez doğrulanabilir. İlk olarak, tooAzure Active Directory kimlik doğrulaması ve toohello uygulamada oturum açın. 

Bu seçenek iyi bir şirket içi uygulamanız kullanıcıların tooauthenticate gerektirmez, ancak uzaktan erişim için bir güvenlik katmanı Azure Active Directory tooadd istediğiniz seçimdir. 

## <a name="password-based-sign-on"></a>Parola tabanlı oturum açma

Şirket içi uygulamalarınız için parola kasası olarak toouse Azure Active Directory istiyorsanız, tercih **parola tabanlı oturum açma**. Uygulamanızı erişim belirteçleri veya üstbilgileri yerine bir kullanıcı adı/parola bileşik kimlik doğrulamasını, bu seçenek iyi bir seçimdir. Parola tabanlı ile oturum açma, kullanıcılarınızın toohello uygulama hello toosign erişen ilk kez gerekir. Bundan sonra Azure Active Directory hello kullanıcı adı ve parola hello kullanıcı adına sağlar. 

Parola tabanlı oturum açmayı ayarlama hakkında daha fazla bilgi için bkz: [tek oturum açma için uygulama proxy'si ile vaulting parola](application-proxy-sso-azure-portal.md).

## <a name="linked-sign-on"></a>Bağlantılı oturum açma

Şirket içi kimliklerinizi için ayarlanmış bir tek oturum açma çözümü zaten varsa, seçin **bağlantılı oturum açma**. Bu seçenek, Azure Active Directory tooleverage varolan SSO çözümleri sağlar, ancak hala kullanıcılarınızın uzaktan erişim toohello uygulamaya sunar. 

Bağlantılı oturum açma (varolan çoklu oturum açma resmi olarak bilinir) özelliğini hakkında daha fazla bilgi için bkz: [uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).

## <a name="integrated-windows-authentication"></a>Tümleşik Windows kimlik doğrulaması

Şirket içi uygulamalarınız tümleşik Windows Authentication(IWA) kullanıyorsa ya da çoklu oturum açma için toouse Kerberos Kısıtlı temsilci (KCD) istiyorsanız seçin **tümleşik Windows kimlik doğrulaması**. Bu seçenek ile kullanıcılarınız tooauthenticate tooAzure Active Directory yeterlidir ve hello kullanıcı tooget bir Kerberos belirteci ve toohello uygulamada oturum hello uygulama ara sunucusu Bağlayıcısı temsil eder. 

Tümleşik Windows kimlik doğrulaması ayarlama hakkında daha fazla bilgi için bkz: [Kerberos Kısıtlı temsilci çoklu oturum açma için uygulama proxy'si ile](active-directory-application-proxy-sso-using-kcd.md).

## <a name="header-based-sign-on"></a>Üstbilgi tabanlı oturum açma 

Uygulamalarınız için kimlik doğrulama üstbilgileri kullanıyorsa seçin **üstbilgi tabanlı oturum açma**. Bu seçenek ile kullanıcılarınız tooauthentication hello Azure Active Directory yeterlidir. Microsoft iş ortaklarının bir üçüncü taraf kimlik doğrulama hizmeti ile Merhaba uygulaması için bir üstbilgi biçime hello Azure Active Directory'ye erişim belirteci çevrilen PingAccess çağrılır. 

Üstbilgi tabanlı kimlik doğrulaması ayarlama hakkında daha fazla bilgi için bkz: [üstbilgi tabanlı kimlik doğrulaması için çoklu oturum açma uygulama proxy'si ile](application-proxy-ping-access.md).

## <a name="next-steps"></a>Sonraki adımlar

- [Çoklu oturum açma için uygulama proxy'si ile vaulting parola](application-proxy-sso-azure-portal.md)
- [Kerberos Kısıtlı temsilci çoklu oturum açma için uygulama proxy'si ile uygulama](active-directory-application-proxy-sso-using-kcd.md)
- [Uygulama proxy'si ile çoklu oturum açma için üstbilgi tabanlı kimlik doğrulaması](application-proxy-ping-access.md) 
