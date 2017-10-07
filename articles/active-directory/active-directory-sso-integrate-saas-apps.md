---
title: "SaaS uygulamaları ile Azure Active Directory çoklu oturum açma aaaIntegrate | Microsoft Docs"
description: "Çoklu oturum açma kimlik doğrulaması ve merkezi erişim yönetimi Azure Active Directory'de SaaS uygulamaları için sağlama kullanıcı etkinleştirin. Hakkında genel bakış toointegrate Azure Active Directory tooSaaS uygulamalar."
services: active-directory
keywords: "Azure AD SaaS uygulamaları ile tümleştirme"
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 53b9d341-d1fc-4bbb-ac7c-3f4c68fcf00a
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/17/2017
ms.author: curtand
ms.reviewer: aaronsm
ms.openlocfilehash: fe621a30429c81c32470635d105ae3e95184efa1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-active-directory-single-sign-on-with-saas-apps"></a>Azure Active Directory çoklu oturum açma SaaS uygulamaları ile tümleştirme
> [!div class="op_single_selector"]
> * [Azure portal](active-directory-enterprise-apps-manage-sso.md)
> * [Klasik Azure Portalı](active-directory-sso-integrate-saas-apps.md)
>
>

[!INCLUDE [active-directory-sso-use-case-intro](../../includes/active-directory-sso-use-case-intro.md)]

Kuruluşunuzun getiren bir uygulama için çoklu oturum açmayı ayarlama başladı tooget, varolan bir dizin Azure Active Directory (Azure AD) kullanacaksınız. Microsoft Azure, Office 365 veya Windows Intune elde bir Azure AD dizini kullanabilirsiniz. İki veya daha fazlası varsa, bkz: [Azure AD dizininizi yönetme](active-directory-administer.md) toodetermine hangi bir toouse.

> [!IMPORTANT]
> Microsoft önerir hello kullanarak Azure AD'yi yönetme [Azure AD Yönetim Merkezi](https://aad.portal.azure.com) hello yerine Azure portal hello bu makalede başvurulan Klasik Azure portalı. Nasıl tooassign Yönetici rolü hello Azure AD Yönetim Merkezi için bkz: [Azure Active Directory'de yönetici rolleri atama](active-directory-enterprise-apps-manage-sso.md).

## <a name="authentication"></a>Kimlik Doğrulaması
Uygulamalar için WS-Federation, SAML 2.0 hello veya protokolleri, Openıd Connect Azure Active Directory kullanan sertifikaları tooestablish güven ilişkileri imzalama destekler. Bu konu hakkında daha fazla bilgi için bkz: [için sertifikaları yönetme federe çoklu oturum açma](active-directory-sso-certs.md).

Yalnızca HTML form tabanlı oturum açma destekleyen uygulamalar için Azure Active Directory kullanan 'parola atlatma' tooestablish güven ilişkileri. Kuruluş toobe bu etkinleştirir hello kullanıcılar oturumunuz otomatik olarak tooa içinde hello kullanıcı hesabı bilgileri hello SaaS uygulaması kullanarak Azure AD tarafından SaaS uygulaması. Azure AD toplar ve güvenli bir şekilde hello kullanıcı hesabı bilgilerini ve hello ilgili parola depolar. Daha fazla bilgi için bkz: [parola tabanlı çoklu oturum açma](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).

## <a name="authorization"></a>Yetkilendirme
Çoklu oturum açma doğrulandıktan sonra sağlanan hesap kullanıcı yetkili toobe toouse bir uygulama sağlar. Kullanıcı sağlamayı el ile veya ekleyin ve Azure Active Directory'de yapılan değişikliklere göre hello SaaS uygulama kullanıcı bilgilerini kaldırmak, bazı durumlarda yapılabilir. Otomatik sağlama için var olan Azure AD bağlayıcılarını kullanma hakkında daha fazla bilgi için bkz: [otomatik kullanıcı sağlamayı ve SaaS uygulamaları için sağlamayı kaldırma özelliklerini](active-directory-saas-app-provisioning.md).

Aksi takdirde, el ile kullanıcı bilgileri tooan uygulama ekleyebilir, veya hello marketi'ndeki kullanılabilir diğer sağlama çözümleri kullanır.

## <a name="access"></a>Access
Azure AD kuruluşunuzdaki toodeploy uygulamaları tooend kullanıcılar birkaç özelleştirilebilir yolu sağlar. Herhangi bir belirli dağıtım veya erişim çözümü kilitli değil. Kullanabileceğiniz [hello gereksinimlerinize en uygun çözümü](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).

## <a name="additional-considerations-for-applications-already-in-use"></a>Ek hususlar uygulamalar zaten kullanımda
Kuruluşunuz zaten kullanan bir uygulama için tek kaydolma ayarı, yeni bir uygulama için yeni hesaplar oluşturma hello işleminden farklı bir işlemdir. İlk adımlar da dahil olmak üzere birkaç vardır: hello uygulama tooAzure AD kimlikleri kullanıcı kimliklerini eşleme ve kullanıcılar ile tümleştirildikten sonra tooan uygulamada oturum nasıl yaşayacağınızı anlama.

> [!NOTE]
> tooset SSO olan bir uygulamanın yukarı hem de Azure AD'de toohave genel yönetici haklarına sahip olmanız gerekir ve SaaS uygulamasına hello.
>
>

### <a name="mapping-user-accounts"></a>Kullanıcı hesapları eşleme
Bir kullanıcının kimliğini genellikle bir e-posta adresi veya kullanıcı asıl adı (UPN) benzersiz bir tanımlayıcı vardır. Toolink (map) ihtiyacınız olacak her bir kullanıcının uygulama kimliği tootheir ilgili Azure AD kimliği. Vardır birkaç yolu tooaccomplish bu nasıl bağlı olarak uygulama kimlik doğrulama hello gereksinimi.

Azure AD kimliklerle uygulama kimlikleri eşleme hakkında daha fazla bilgi için bkz: [hello SAML belirtecinde verilen talepler özelleştiriliyor](http://social.technet.microsoft.com/wiki/contents/articles/31257.azure-active-directory-customizing-claims-issued-in-the-saml-token-for-pre-integrated-apps.aspx) ve [sağlama öznitelik eşlemelerini özelleştirme](active-directory-saas-customizing-attribute-mappings.md).

### <a name="understanding-hello-users-log-in-experience"></a>Merhaba kullanıcının oturum açma deneyimi anlama
Zaten bir uygulama için SSO'i tümleştirdiğinizde kullanıcı deneyimi hello toorealize etkilenecek önemlidir. Tüm uygulamalar için kullanıcılar kendi Azure AD kimlik bilgilerini toosign kullanmaya başlar. Ayrıca, farklı portal tooaccess hello uygulamaları kullanmalıdır olabilir.

Merhaba uygulamanın oturum arabiriminde SSO bazı uygulamalar için yapılabilir, ancak diğer uygulamalar için hello kullanıcı toogo merkezi bir portal üzerinden gibi gerekir ([My uygulamaları](http://myapps.microsoft.com) veya [Office365](http://portal.office.com/myapps)) içinde toosign. SSO ve kullanıcı deneyimlerini farklı türlerde hello hakkında daha fazla bilgi [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

Başka bir değerli kaynaktır *kullanıcı izni gizleme* hello içinde [Guiding geliştiriciler](active-directory-applications-guiding-developers-for-lob-applications.md) makalesi.

## <a name="next-steps"></a>Sonraki adımlar
Merhaba uygulama Galerisi Bul SaaS uygulamaları için Azure AD bir dizi sağlar [öğreticileri nasıl toointegrate SaaS uygulamaları](active-directory-saas-tutorial-list.md).

Uygulama uygulama galerisinde değilse, yapabilecekleriniz [toohello Azure AD uygulama galerisinde özel bir uygulama eklemek](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx).

Tüm itibaren bu sorunların hello Azure.com Kitaplığı ' nda daha fazla ayrıntı yok [uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md).

Ayrıca, hello kaçırmayın [Azure Active Directory'de uygulama yönetimi için makale dizini](active-directory-apps-index.md).
