---
title: "aaaGet başlatılan Azure AD uygulamaları ile tümleştirme | Microsoft Docs"
description: "Bu makalede, Azure Active Directory (AD) şirket içi uygulamaları ve bulut uygulamaları ile tümleştirmek için bir başlangıç kılavuzuna getirilmiştir."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: db6d210d-c970-49e9-bd20-36d984bcd1c3
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: asteen
ms.openlocfilehash: 5a7a851e8418083fee72ab58477a9cab75d0d4bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-azure-active-directory-with-applications-getting-started-guide"></a>Azure Active Directory alma uygulamaları ile tümleştirme Kılavuzu
## <a name="overview"></a>Genel Bakış
Bu konuda hedeflenen toogive olduğundan, Azure Active Directory (AD ile) uygulamaları tümleştirmek için bir yol haritası. Merhaba bölümlerinde aşağıdaki içeren daha ayrıntılı bir konu kısa bir özeti hangi bu başlangıç kılavuzuna ilgili tooyou bölümlerdir tanımlayabilir.  Merhaba bağlantıları daha ayrıntılı bilgi edinmek için her konu üzerinde izleyin.

## <a name="before-you-begin-take-inventory"></a>Başlamadan önce envanteri
Azure AD ile toointegrating uygulamaları hemen önce olduğunuz nerede ve toogo istediğiniz önemli tooknow vardır.  Hello aşağıdaki sorular, Azure AD uygulama tümleştirme projesi hakkında düşünmek hedeflenen toohelp vardır.

### <a name="application-inventory"></a>Uygulama envanteri
* Tüm uygulamalarınızın nerede? Bunları Kime ait?
* Ne tür bir kimlik doğrulama uygulamalarınızı gerektiriyor mu?
* Erişim toowhich uygulamaları gerek duyan?
* Yeni bir uygulama toodeploy istiyor musunuz?
  * Şirket içi derleme ve bir Azure işlem örneğinde dağıtma?
  * Hello Azure uygulama Galerisi kullanılabilir olan bir kullanacaksınız?

### <a name="user-and-group-inventory"></a>Kullanıcı ve Grup envanteri
* Kullanıcı hesaplarınızı bulunduğu?
  * Şirket içi Active Directory
  * Azure AD
  * Sahip olduğunuz bir ayrı uygulama veritabanı içinde
  * Tasdik edilmemiş uygulamalar
  * Tüm hello yukarıdaki
* Hangi izinleri ve rol atamalarını bireysel kullanıcılar şu anda var mı? Erişimleri tooreview gerekiyor mu yoksa, kullanıcı erişimi ve rol atamalarını uygun olduğundan emin misiniz?
* Grupları, şirket içi Active Directory'de zaten oluşturulmuş?
  * Gruplarınızı nasıl düzenlenir?
  * Merhaba Grup üyeleri kim?
  * Hangi izinleri/rol atamalarını hello gruplar şu anda var mı?
* Tümleştirme önce kullanıcı/Grup veritabanlarını tooclean gerekiyor mu?  (Bu oldukça önemli bir soru içindir. Çöp girişi, atık.)

### <a name="access-management-inventory"></a>Erişim Yönetimi envanteri
* Şu anda kullanıcı erişimi tooapplications yönetme? Toochange gerekiyor mu?  Diğer yolları toomanage erişim gibi ile göz önünde bulundurduğunuzdan [RBAC](role-based-access-control-configure.md) Örneğin?
* Erişim toowhat gerek duyan?

Bu soruların yanıtları tooall hello Önden belki yok ancak Tamam olmasıdır.  Bu kılavuz, bu sorulara yanıt ve bazı bilinçli kararlar almanıza yardımcı olabilir.

## <a name="prerequisites"></a>Ön koşullar
* Bir Azure aboneliği ve bir Azure Active Directory dizin.  Bir Azure aboneliğiniz yoksa, ücretsiz 30 gün boyunca Azure deneyebilirsiniz. [Deneyin!](https://azure.microsoft.com/trial/get-started-active-directory/)

## <a name="application-integration-with-azure-ad"></a>Azure AD ile uygulama tümleştirmesi
### <a name="finding-unsanctioned-cloud-applications-with-cloud-app-discovery"></a>Cloud App Discovery ile bulut uygulamaları tasdik bulma
Yukarıda belirtildiği gibi şimdiye kadar kuruluşunuz tarafından yönetilen henüz uygulamalar olabilir.  Merhaba envanteri işleminin bir parçası olarak, tasdik olası toofind bulut uygulamalarını değil. Bkz: [Cloud App Discovery tasdik edilmemiş bulut uygulamalarıyla bulma](active-directory-cloudappdiscovery-whatis.md).

### <a name="authentication-types"></a>Kimlik doğrulama türleri
Uygulamalarınızın her birinde farklı kimlik doğrulama gereksinimleri olabilir. Azure AD ile imzalama sertifikalarının SAML 2.0, WS-Federasyon, veya Openıd Connect protokollerinin yanı parola çoklu oturum açma kullanan uygulamalar ile kullanılabilir. Uygulama hakkında daha fazla bilgi için bkz: Azure AD ile kullanmak için kimlik doğrulama türleri [sertifikaların yönetilmesi için Federasyon çoklu oturum açma Azure Active Directory'de](active-directory-sso-certs.md) ve [parola temel çoklu oturum açma](active-directory-appssoaccess-whatis.md).

### <a name="enabling-sso-with-azure-ad-app-proxy"></a>Azure AD uygulama proxy'si ile SSO etkinleştirme
Microsoft Azure AD uygulama proxy'si ile erişim tooapplications özel ağınızda güvenli bir şekilde, her yerden ve herhangi bir cihazda bulunan sağlayabilir. Ortamınızda bir uygulama proxy Bağlayıcısı yükledikten sonra Azure AD ile kolayca yapılandırılabilir.

### <a name="integrating-applications-with-azure-ad"></a>Uygulamaları Azure AD ile tümleştirme
Merhaba aşağıdaki makalelere uygulamaları Azure AD ile tümleştirmek ve bazı kılavuzluk hello farklı şekilde ele alır.

* [Hangi Active Directory toouse belirleme](active-directory-administer.md)
* [Hello Azure uygulama galerisinde uygulamaları kullanma](active-directory-appssoaccess-whatis.md)
* [SaaS uygulamaları öğreticiler listesi tümleştirme](active-directory-saas-tutorial-list.md)

## <a name="managing-access-tooapplications"></a>Erişim tooapplications yönetme
Merhaba Aşağıdaki makaleler Azure AD bağlayıcıları kullanarak Azure AD ve Azure AD ile tümleşik olan sonra erişim tooapplications yönetebilirsiniz yolları açıklanmaktadır.

* [Azure AD kullanarak erişim tooapps yönetme](active-directory-managing-access-to-apps.md)
* [Azure AD Bağlayıcılarla otomatikleştirme](active-directory-saas-app-provisioning.md)
* [Kullanıcıları tooan uygulama atama](active-directory-applications-guiding-developers-assigning-users.md)
* [Tooan uygulama grupları atama](active-directory-applications-guiding-developers-assigning-groups.md)
* [Hesapları paylaşma](active-directory-sharing-accounts.md)

## <a name="integrating-custom-applications"></a>Özel uygulamaları tümleştirme
Yeni bir uygulama yazıyorsanız ve hello güç Azure AD yararlanarak içinde tooassist geliştiriciler istiyorsanız, bkz [Guiding geliştiriciler](active-directory-applications-guiding-developers-for-lob-applications.md).

Azure uygulama Galerisi, özel uygulama toohello tooadd istiyorsanız, bkz: ["kendi uygulamanızı Azure AD Self Servis SAML yapılandırmayla getir"](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx).

## <a name="see-also"></a>Ayrıca bkz.
* [Azure Active Directory'de Uygulama Yönetimi için Makale Dizini](active-directory-apps-index.md)

