---
title: "aaaConditional erişim tooon içi uygulamaları - Azure AD | Microsoft Docs"
description: "Nasıl tooset uygulamalar için koşullu erişim kullanarak uzaktan erişilen toobe yayımladığınız kapsayan Azure AD uygulama proxy'si."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 2e97722b-eb4e-4078-b607-9fed210d8a0f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 7bed25dd4ba17941e77d8c4b2b9ba4edcf0cf597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-conditional-access-in-azure-ad-application-proxy"></a>Azure AD uygulama proxy'si koşullu erişim ile çalışma

>[!NOTE]
>Bu makale toohello devre dışı bırakıldığını Azure Klasik portalı geçerlidir. Merhaba kullanmanızı öneririz [Azure portal](https://portal.azure.com). Hello Azure portal, uygulama proxy'si uygulamalara sahip aynı özelliklere koşullu erişim gibi diğer SaaS uygulama hello. koşullu erişim hakkında daha fazla toolearn bkz [Azure Active Directory'de koşullu erişimi kullanmaya başlama](active-directory-conditional-access-azure-portal-get-started.md).

Erişimi yapılandırma kuralları toogrant koşullu erişim tooapplications yayımlanan uygulama proxy'si kullanma. Şunları yapmanızı sağlar:

* Uygulama başına çok faktörlü kimlik doğrulaması gerektirir
* Yalnızca kullanıcıların iş olmadığında çok faktörlü kimlik doğrulaması gerektirir
* İşte olmadıkları zaman kullanıcıların hello uygulamaya erişmeyi engelle

Bu kurallar, uygulanan tooall kullanıcıları ve grupları veya yalnızca toospecific kullanıcıları ve grupları olabilir. Varsayılan olarak erişimi toohello uygulama sahip tooall kullanıcılar hello kuralı uygular. Ancak hello kural belirtilen güvenlik gruplarına üye olan kısıtlı toousers olabilir.  

Erişim kuralları, bir kullanıcı OAuth 2.0, Openıd Connect, SAML veya WS-Federasyon kullanan bir federasyon uygulaması eriştiğinde değerlendirilir. Ayrıca, bir yenileme belirteci kullanılan tooacquire bir erişim belirteci olduğunda erişim kuralları OAuth 2.0 ve Openıd Connect ile değerlendirilir.

## <a name="conditional-access-prerequisites"></a>Koşullu erişim önkoşulları
* Abonelik tooAzure Active Directory Premium
* Federe veya yönetilen bir Azure Active Directory kiracısı
* Federasyon kiracıları multi-Factor authentication (MFA) gerekli  
    ![Erişim kuralları yapılandırın - çok faktörlü kimlik doğrulaması gerektirir](./media/active-directory-application-proxy-conditional-access/application-proxy-conditional-access.png)

## <a name="configure-per-application-multi-factor-authentication"></a>Uygulama başına çok faktörlü kimlik doğrulamasını yapılandırma
1. Yönetici hello olarak Klasik Azure portalında oturum açın.
2. TooActive dizinine gidin ve tooenable uygulama proxy'si istediğiniz hello dizini seçin.
3. Tıklatın **uygulamaları** ve toohello aşağı **erişim kuralları** bölümü. Merhaba erişim kuralları bölümünde yalnızca federe kimlik doğrulaması kullanan uygulama proxy'si kullanılarak yayımlanan uygulamalar için görüntülenir.
4. Merhaba kuralı seçerek etkinleştirin **erişim kurallarını etkinleştirme** çok**üzerinde**.
5. Kuralları uygula hello kullanıcılar ve gruplar toowhom hello belirtin. Kullanım hello **Grup Ekle** tooselect toowhich hello erişim kuralın uygulanacağı bir veya daha fazla grupları düğmesine tıklayın. Bu iletişim kutusunu da seçili kullanılan tooremove grupları olabilir.  Hello kuralları seçili tooapply toogroups olduğunda hello erişim kuralları, belirtilen hello tooone ait kullanıcılar için uygulanır güvenlik grupları.  

   * tooexplicitly dışlama güvenlik gruplarını hello kuraldan denetle **dışında** ve bir veya daha fazla gruplarını belirtin. Merhaba listesi dışında bir grubun üyeleri olan kullanıcılar gerekli tooperform çok faktörlü kimlik doğrulaması olup olmadığı.  
   * Bir kullanıcı hello kullanıcı başına çok faktörlü kimlik doğrulama özelliği kullanılarak yapılandırıldıysa, bu ayar hello uygulama çok faktörlü kimlik doğrulama kurallarını önceliklidir. Merhaba uygulamanın çok faktörlü kimlik doğrulaması kurallardan bırakılan bile, kullanıcı başına çok faktörlü kimlik doğrulaması için yapılandırılmış gerekli tooperform çok faktörlü kimlik doğrulaması kullanıcıdır. Daha fazla bilgi edinmek [çok faktörlü kimlik doğrulama ve kullanıcı başına ayarları](../multi-factor-authentication/multi-factor-authentication.md).
6. Tooset istediğiniz hello erişim kuralını seçin:

   * **Çok faktörlü kimlik doğrulaması gerektiren**: toowhom erişim kuralları uygula kullanıcılardır gerekli toocomplete çok faktörlü kimlik doğrulaması erişilirken hello uygulama toowhich hello kuralı uygulanmadan önce.
   * **Çalışma zaman değil, çok faktörlü kimlik doğrulaması gerektiren**: kullanıcıların güvenilir bir IP adresinden tooaccess hello uygulama çalışırken gerekli tooperform çok faktörlü kimlik doğrulaması olmayacak. Merhaba, IP adres aralıklarını hello çok faktörlü kimlik doğrulama ayarları sayfasında yapılandırılabilir güvenilir.
   * **Çalışma zaman değil, erişimi engelleme**: kullanıcıların şirket ağınızın dışındaki tooaccess hello uygulama çalışırken mümkün tooaccess Merhaba uygulaması olmayacak.

## <a name="configuring-mfa-for-federation-services"></a>MFA için Federasyon Hizmetleri Yapılandırılıyor
Federasyon kiracıları için çok faktörlü kimlik doğrulaması (MFA) hello veya Azure Active Directory tarafından işlem yapılabilir şirket içi AD FS sunucusu. Varsayılan olarak, MFA Azure Active Directory tarafından barındırılan herhangi bir sayfada gerçekleşir. tooconfigure MFA şirket içi, Windows PowerShell ve kullanım hello – SupportsMFA özelliği tooset hello Azure AD modülünü çalıştırın.

Merhaba aşağıdaki örnekte gösterilir nasıl tooenable MFA hello kullanarak şirket içi [Set-MsolDomainFederationSettings cmdlet'i](https://msdn.microsoft.com/library/azure/dn194088.aspx) hello contoso.com Kiracı üzerinde:`Set-MsolDomainFederationSettings -DomainName contoso.com -SupportsMFA $true `

Toplama toosetting hello Federasyon Kiracı AD FS örneği bu bayrak olmalıdır tooperform çok faktörlü kimlik doğrulaması yapılandırılmış. Merhaba yönergeleri izleyin [Microsoft Azure çok faktörlü kimlik doğrulaması şirket içi dağıtma](../multi-factor-authentication/multi-factor-authentication-get-started-server.md).

## <a name="see-also"></a>Ayrıca bkz.
* [Talepleri kullanan uygulamalarla çalışma](active-directory-application-proxy-claims-aware-apps.md)
* [Uygulama proxy'si ile uygulama yayımlama](active-directory-application-proxy-publish.md)
* [Çoklu oturum açmayı etkinleştirme](active-directory-application-proxy-sso-using-kcd.md)
* [Kendi etki alanı adınızı kullanarak uygulama yayımlama](active-directory-application-proxy-custom-domains.md)

Merhaba en son haberler ve güncelleştirmeler için hello denetleyin [uygulama ara sunucusu bloguna](http://blogs.technet.com/b/applicationproxyblog/)
