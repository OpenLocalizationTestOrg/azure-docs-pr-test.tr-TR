---
title: "SaaS uygulamaları için koşullu erişim aaaAzure | Microsoft Docs"
description: "Azure AD'de koşullu erişim, güvenilir bir ağda değil, kullanıcılar için tooconfigure uygulama başına çok faktörlü kimlik doğrulama erişim kuralları ve hello özelliği tooblock erişimi verir. "
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 51a1ee61-3ffe-4f65-b8de-ff21903e1e74
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 69748014c0c8e266ba66562980c784aba4c68d80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-active-directory-conditional-access"></a>Azure Active Directory koşullu erişimi kullanmaya başlama
Azure Active Directory için koşullu erişim [SaaS](https://azure.microsoft.com/overview/what-is-saas/) uygulamalar ve Azure AD bağlı grubu, konum ve uygulama duyarlılığına göre koşullu erişim yapılandırmanızı uygulamaları sağlar. 

Uygulama duyarlılığına göre koşullu erişim ile uygulama başına çok faktörlü kimlik doğrulaması (MFA) erişim kurallarını ayarlayabilmeniz için. Uygulama başına MFA güvenilir bir ağ üzerinde olmayan kullanıcılar için hello özelliği tooblock erişim sağlar. Atanan toohello uygulama ya da yalnızca içinde kullanıcılar için güvenlik grupları belirtilen MFA kuralları tooall kullanıcıların uygulayabilirsiniz.  Bunlar Merhaba uygulaması hello kuruluşunuzun ağınızda bir IP adresinden erişiyorsanız hello MFA gereksinimden dışlanan kullanıcılar.

Bu özellikler Azure Active Directory Premium lisansı satın kullanılabilir toocustomers olacaktır.

## <a name="scenario-prerequisites"></a>Senaryo önkoşulları
* Azure Active Directory Premium lisansı
* Federe veya yönetilen Azure Active Directory kiracısı
* Federasyon kiracıları, çok faktörlü kimlik doğrulamasının etkin olması gerekir.

## <a name="configure-per-application-access-rules"></a>Uygulama başına erişim kurallarını yapılandırın
Bu bölümde her uygulama için tooconfigure nasıl erişim açıklanmaktadır kuralları.

1. İçinde toohello için Azure AD genel yönetici olan bir hesabı kullanarak Klasik Azure portalında oturum açın.
2. Merhaba soldaki bölmede bulunan seçin **Active Directory**.
3. Merhaba dizin sekmesinde dizininizi seçin.
4. Select hello **uygulamaları** sekmesi.
5. Kural hello select Merhaba uygulaması için ayarlanacak.
6. Select hello **yapılandırma** sekmesi.
7. Toohello erişim kuralları bölümüne kaydırın. Merhaba istediğiniz erişim kuralını seçin.
8. Merhaba kuralın uygulanacağı hello kullanıcıları belirtin.
9. Hello İlkesi seçerek etkinleştirin **toobe etkin**.

## <a name="understanding-access-rules"></a>Anlama erişim kuralları
Bu bölümde hello Azure koşullu uygulama erişim desteklenen hello erişim kuralları ayrıntılı açıklamasını sağlar.

### <a name="specifying-hello-users-hello-access-rules-apply-to"></a>Erişim kuralları geçerli belirten hello kullanıcılar hello
Varsayılan olarak, erişim toohello uygulamaya sahip tooall kullanıcılar hello ilkesi uygulanır. Ancak, aynı zamanda belirtilen hello üyeleri olan hello İlkesi toousers kısıtlayabilirsiniz güvenlik grupları. Merhaba **Grup Ekle** düğmesi kullanılan tooselect bir ya da erişim kuralı hello daha fazla Grup hello Grup Seçimi iletişim kutusundan uygulanır. Bu iletişim kutusunu da seçili kullanılan tooremove grupları olabilir. Merhaba kuralları seçili tooapply tooGroups olduğunda hello erişim kuralları yalnızca belirtilen hello tooone ait olan kullanıcılar için zorunlu güvenlik grupları.

Güvenlik grupları de açıkça hariç tutulamaz hello İlkesi'nden hello seçerek **dışında** seçeneği ve bir veya daha fazla grup belirtme. Merhaba bir grubun üyesi olan kullanıcılar **dışında** listesi konu toohello çok faktörlü kimlik doğrulama gereksinimini olmaz, bu hello erişim kuralı, bir grubun üyesi olsa bile uygulanır.
Aşağıda gösterilen hello erişim kuralı hello Yöneticileri grubu toouse çok faktörlü kimlik doğrulaması'ndaki tüm kullanıcılar Merhaba uygulaması erişirken gerektirir.

![MFA ile koşullu erişim kurallarının ayarlanması](./media/active-directory-conditional-access-azuread-connected-apps/conditionalaccess-saas-apps.png)

## <a name="conditional-access-rules-with-mfa"></a>MFA ile koşullu erişim kuralları
Bir kullanıcı hello kullanıcı başına çok faktörlü kimlik doğrulaması özelliğini kullanarak yapılandırılmışsa hello kullanıcı bu ayarda hello uygulamasının hello çok faktörlü kimlik doğrulama kuralları ile birleştirin. Bu, hello uygulama çok faktörlü kimlik doğrulaması kurallardan bırakılan olsa bile, kullanıcı başına çok faktörlü kimlik doğrulaması için yapılandırılmış olan bir kullanıcı gerekli tooperform çok faktörlü kimlik doğrulaması anlamına gelir. Çok faktörlü kimlik doğrulama ve kullanıcı başına ayarları hakkında daha fazla bilgi edinin.

### <a name="access-rule-options"></a>Erişim kuralı seçenekleri
Seçenekler aşağıdaki hello desteklenir:

* **Çok faktörlü kimlik doğrulaması gerektiren**: hello kullanıcılar toowhom hello erişim kuralları uygulamak için ilke hello hello uygulamaya erişmeyi uygulandığı önce gerekli toocomplete çok faktörlü kimlik doğrulaması olacaktır.
* **Çalışma zaman değil, çok faktörlü kimlik doğrulaması gerektiren**: güvenilir bir IP adresinden gelen bir kullanıcı gerekli tooperform çok faktörlü kimlik doğrulaması olmayacaktır. Merhaba, IP adres aralıklarını hello çok faktörlü kimlik doğrulama ayarları sayfasında yapılandırılabilir güvenilir.
* **Çalışma zaman değil, erişimi engelleme**: güvenilir bir IP adresinden gelen olmayan bir kullanıcı engellenir. Merhaba, IP adres aralıklarını hello çok faktörlü kimlik doğrulama ayarları sayfasında yapılandırılabilir güvenilir.

### <a name="setting-rule-status"></a>Kuralın durumunu ayarlama
Erişim kuralı durumu hello kurallarını açma veya kapatma sağlar. Merhaba erişim kuralları devre dışı iken, hello çok faktörlü kimlik doğrulama gereksinimini zorlanmaz.

### <a name="access-rule-evaluation"></a>Erişim kuralı değerlendirme
Erişim kuralları, bir kullanıcı OAuth 2.0, Openıd Connect, SAML veya WS-Federasyon kullanan bir federasyon uygulaması eriştiğinde değerlendirilir. Ayrıca, erişim kuralları Hello OAuth 2.0 ve Openıd Connect bir yenileme belirteci tooacquire bir erişim belirteci kullandığınızda değerlendirilir. Bir yenileme belirteci kullanıldığında ilke değerlendirmesi başarısız olursa hata hello **invalid_grant** döndürülecek, bu gösterir hello kullanıcının ihtiyacı toore-toohello istemci kimlik doğrulaması.

### <a name="configure-federation-services-tooprovide-multi-factor-authentication"></a>Federasyon Hizmetleri tooprovide çok faktörlü kimlik doğrulamasını yapılandırma
Federasyon kiracıları için MFA hello veya Azure Active Directory tarafından işlem yapılabilir şirket içi AD FS sunucusu.

Varsayılan olarak, Azure Active Directory tarafından barındırılan bir sayfa MFA meydana gelir. tooconfigure MFA şirket hello **– SupportsMFA** özelliği çok ayarlanmalıdır**true** Azure Active Directory'de hello Azure AD modülü için Windows PowerShell kullanarak.

Merhaba aşağıdaki örnekte gösterilir nasıl tooenable MFA hello kullanarak şirket içi [Set-MsolDomainFederationSettings cmdlet'i](https://msdn.microsoft.com/library/azure/dn194088.aspx) hello contoso.com Kiracı üzerinde:

    Set-MsolDomainFederationSettings -DomainName contoso.com -SupportsMFA $true

Toplama toosetting hello Federasyon Kiracı AD FS örneği bu bayrak olmalıdır tooperform çok faktörlü kimlik doğrulaması yapılandırılmış. Merhaba yönergeleri izleyin [Azure multi-Factor Authentication şirket içi dağıtma](../multi-factor-authentication/multi-factor-authentication-get-started-server.md).

## <a name="related-articles"></a>İlgili makaleler
* [Active Directory tooAzure bağlı erişim tooOffice 365 ve diğer uygulamaların güvenliğini sağlama](active-directory-conditional-access.md)
* [Azure Active Directory'de Uygulama Yönetimi için Makale Dizini](active-directory-apps-index.md)

