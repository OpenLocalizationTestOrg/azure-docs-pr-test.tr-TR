---
title: "SaaS uygulamaları için Azure koşullu erişim | Microsoft Docs"
description: "Azure AD'de koşullu erişim uygulama başına çok faktörlü kimlik doğrulama erişim kuralları ve güvenilir bir ağda değil, kullanıcılar için erişimi engelleme özelliği yapılandırmanıza olanak sağlar. "
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
ms.openlocfilehash: efaa70467346e910a78a63d182041029bb34b1cc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="getting-started-with-azure-active-directory-conditional-access"></a>Azure Active Directory koşullu erişimi kullanmaya başlama
Azure Active Directory için koşullu erişim [SaaS](https://azure.microsoft.com/overview/what-is-saas/) uygulamalar ve Azure AD bağlı grubu, konum ve uygulama duyarlılığına göre koşullu erişim yapılandırmanızı uygulamaları sağlar. 

Uygulama duyarlılığına göre koşullu erişim ile uygulama başına çok faktörlü kimlik doğrulaması (MFA) erişim kurallarını ayarlayabilmeniz için. Uygulama başına MFA güvenilir bir ağ üzerinde olmayan kullanıcıların erişimini engellemek için yeteneği sağlar. Uygulama ya da yalnızca belirtilen güvenlik gruplarının içinde kullanıcılar için atanmış tüm kullanıcılar için MFA kurallarını uygulayabilirsiniz.  Bunlar uygulama kuruluşun ağınızda bir IP adresinden erişiyorsanız MFA gereksinimden dışlanan kullanıcılar.

Bu özellikler bir Azure Active Directory Premium lisansı satın alan müşteriler için kullanılabilir.

## <a name="scenario-prerequisites"></a>Senaryo önkoşulları
* Azure Active Directory Premium lisansı
* Federe veya yönetilen Azure Active Directory kiracısı
* Federasyon kiracıları, çok faktörlü kimlik doğrulamasının etkin olması gerekir.

## <a name="configure-per-application-access-rules"></a>Uygulama başına erişim kurallarını yapılandırın
Bu bölümde, uygulama başına erişim kurallarının nasıl yapılandırıldığı açıklanmaktadır.

1. Azure AD genel yönetici olan bir hesabı kullanarak Klasik Azure portalında oturum açın.
2. Sol bölmede **Active Directory**'yi seçin.
3. Dizin sekmesinde dizininizi seçin.
4. Seçin **uygulamaları** sekmesi.
5. Kural için ayarlanacak uygulaması'nı seçin.
6. **Configure (Yapılandır)** sekmesini seçin.
7. Erişim kuralları bölümüne gidin. İstediğiniz erişim kuralını seçin.
8. Kuralın uygulanacağı kullanıcıları belirtin.
9. İlke seçerek etkinleştirin **olması için etkin**.

## <a name="understanding-access-rules"></a>Anlama erişim kuralları
Bu bölümde Azure koşullu uygulama erişimi desteklenen erişim kuralları ayrıntılı açıklamasını sağlar.

### <a name="specifying-the-users-the-access-rules-apply-to"></a>Kullanıcıları belirten erişim kuralları için geçerlidir
Varsayılan olarak, uygulamaya erişimi olan tüm kullanıcılar için ilke uygulanır. Ancak, belirtilen güvenlik gruplarına üye olan kullanıcılara ilkeyi de kısıtlayabilirsiniz. **Grup Ekle** düğmesi erişim kuralının uygulanacağı Grup Seçimi iletişim kutusundan bir veya daha fazla gruplarını seçmek için kullanılır. Bu iletişim kutusu, seçili grupların kaldırmak için de kullanılabilir. Gruplara uygulanacak kuralları seçildiğinde erişim kuralları yalnızca belirtilen güvenlik gruplarının birine ait kullanıcılar için uygulanır.

Güvenlik grupları de açıkça ilkesinden seçerek **dışında** seçeneği ve bir veya daha fazla grup belirtme. Bir grubun üyesi olan kullanıcılar **dışında** erişim kuralın uygulanacağı bir grubunun bir üyesi olsa bile listesi çok faktörlü kimlik doğrulama gereksinimi tabi olmayacaktır.
Aşağıda gösterilen erişim kuralı uygulama erişirken çok faktörlü kimlik doğrulaması kullanacak şekilde yöneticileri gruptaki tüm kullanıcılar gerektirir.

![MFA ile koşullu erişim kurallarının ayarlanması](./media/active-directory-conditional-access-azuread-connected-apps/conditionalaccess-saas-apps.png)

## <a name="conditional-access-rules-with-mfa"></a>MFA ile koşullu erişim kuralları
Bir kullanıcı kullanıcı başına çok faktörlü kimlik doğrulaması özelliğini kullanarak yapılandırılmışsa bu ayar kullanıcının uygulamayı çok faktörlü kimlik doğrulama kuralları ile birleştirin. Bu, kullanıcı başına çok faktörlü kimlik doğrulaması için yapılandırılmış bir kullanıcı uygulama çok faktörlü kimlik doğrulama kurallarından bırakılan olsa bile, çok faktörlü kimlik doğrulaması gerçekleştirmek için gerekli anlamına gelir. Çok faktörlü kimlik doğrulama ve kullanıcı başına ayarları hakkında daha fazla bilgi edinin.

### <a name="access-rule-options"></a>Erişim kuralı seçenekleri
Aşağıdaki seçenekleri desteklenir:

* **Çok faktörlü kimlik doğrulaması gerektiren**: kendisine erişim kuralları uygulamak için kullanıcılar, ilkenin uygulandığı uygulama erişmeden önce tam çok faktörlü kimlik doğrulaması için gerekli olacaktır.
* **Çalışma zaman değil, çok faktörlü kimlik doğrulaması gerektiren**: güvenilir bir IP adresinden gelen bir kullanıcı çok faktörlü kimlik doğrulaması gerçekleştirmek için gerekli. Güvenilen IP adres aralıkları çok faktörlü kimlik doğrulama ayarları sayfasında yapılandırılabilir.
* **Çalışma zaman değil, erişimi engelleme**: güvenilir bir IP adresinden gelen olmayan bir kullanıcı engellenir. Güvenilen IP adres aralıkları çok faktörlü kimlik doğrulama ayarları sayfasında yapılandırılabilir.

### <a name="setting-rule-status"></a>Kuralın durumunu ayarlama
Erişim kuralı durumu kurallarını açma veya kapatma sağlar. Erişim kuralları devre dışı iken, çok faktörlü kimlik doğrulama gereksinimini zorlanmaz.

### <a name="access-rule-evaluation"></a>Erişim kuralı değerlendirme
Erişim kuralları, bir kullanıcı OAuth 2.0, Openıd Connect, SAML veya WS-Federasyon kullanan bir federasyon uygulaması eriştiğinde değerlendirilir. Ayrıca, OAuth 2.0 ve Openıd Connect bir erişim belirteci almak için bir yenileme belirteci kullandığınızda erişim kuralları değerlendirilir. Bir yenileme belirteci kullanıldığında, ilke değerlendirmesi başarısız olursa hata **invalid_grant** döndürülecek, bu gösterir kullanıcı istemciye yeniden kimlik doğrulaması gerekiyor.

### <a name="configure-federation-services-to-provide-multi-factor-authentication"></a>Çok faktörlü kimlik doğrulaması sağlamak için Federasyon hizmetlerini yapılandırma
Federasyon kiracıları için MFA şirket içi veya Azure Active Directory tarafından işlem yapılabilir AD FS sunucusu.

Varsayılan olarak, Azure Active Directory tarafından barındırılan bir sayfa MFA meydana gelir. MFA şirket yapılandırmak için **– SupportsMFA** özelliği ayarlanmalıdır **true** Azure Active Directory'de Windows PowerShell için Azure AD modülünü kullanarak.

Aşağıdaki örnek, şirket içi MFA kullanarak etkinleştirmek gösterilmiştir [Set-MsolDomainFederationSettings cmdlet'i](https://msdn.microsoft.com/library/azure/dn194088.aspx) contoso.com Kiracı üzerinde:

    Set-MsolDomainFederationSettings -DomainName contoso.com -SupportsMFA $true

Bu bayrak ayarlamaya ek olarak, Federasyon Kiracı AD FS örneği çok faktörlü kimlik doğrulaması gerçekleştirmek için yapılandırılmış olması gerekir. Yönergeleri izleyin [Azure multi-Factor Authentication şirket içi dağıtma](../multi-factor-authentication/multi-factor-authentication-get-started-server.md).

## <a name="related-articles"></a>İlgili makaleler
* [Azure Active Directory'ye bağlı Office 365 ve diğer uygulamalar için erişim güvenliğini sağlama](active-directory-conditional-access.md)
* [Azure Active Directory'de Uygulama Yönetimi için Makale Dizini](active-directory-apps-index.md)

