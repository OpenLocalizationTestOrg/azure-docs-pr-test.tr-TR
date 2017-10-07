---
title: "Azure AD kullanarak aaaSharing hesapları | Microsoft Docs"
description: "Azure Active Directory kuruluş toosecurely paylaşımı hesapları şirket içi uygulamalar ve tüketici bulut Hizmetleri için nasıl sağladığını açıklar."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e2d77104-d978-46a3-bfea-03ffdf3b61e6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 9f98bfa97a6c9ba1566d3f921c1b676d5f3c2a88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sharing-accounts-with-azure-ad"></a>Azure AD ile hesapları paylaşma
## <a name="overview"></a>Genel Bakış
Bazen kuruluşlar için birden çok kişinin toouse tek bir kullanıcı adı ve parola gerekir. Bu genellikle iki durumlarda gerçekleşir:

* Her kullanıcı için bir benzersiz kullanıcı adı ve parolası gerektiren uygulamalar erişirken olup şirket içi uygulamalar veya tüketici bulut hizmetlerini (ör, Kurumsal sosyal medya hesapları).
* Çok kullanıcılı ortamlar oluştururken. Ayrıcalıkları yükselten tek, yerel bir hesap olabilir ve kullanılan toodo çekirdek Kurulum, yönetim ve kurtarma etkinliklerini (örneğin hello yerel "Genel yönetici" hesabı Salesforce Office 365 veya hello kök hesap için) olabilir.

Geleneksel olarak, bu hesapları hello kimlik bilgilerini (kullanıcı adı/parola) toohello sağ kişiler dağıtma veya bunları burada aracıları erişmesine birden çok güvenilen paylaşılan bir konumda Depolama tarafından paylaşılan.

Merhaba geleneksel paylaşım modelinin birkaç sakıncaları vardır:

* Erişim toonew uygulamaları etkinleştirme erişmesi toodistribute kimlik bilgileri tooeveryone gerektirir.
* Paylaşılan her uygulamanın kendi benzersiz kullanıcıların tooremember birden çok kimlik bilgileri kümesi gerektiren Paylaşılan kimlik bilgileri kümesi gerektirebilir. Birçok kimlik bilgilerini tooremember kullanıcınız olduğunda toorisky yöntemler dönecek hello riskini artırır. (örneğin parolaları yazma).
* Kimlerin erişimi tooan uygulama olduğunu bildiremez.
* Kimlerin olduğunu bildiremez *erişilen* bir uygulama.
* Tooremove access tooan uygulaması gerektiğinde, tooupdate hello kimlik bilgilerine sahip olması ve yeniden dağıtın tooeveryone toothat uygulama erişimi gerektirir.

## <a name="azure-active-directory-account-sharing"></a>Azure Active Directory hesabı paylaşımı
Azure AD yeni bir yaklaşım bu dezavantajları ortadan paylaşılan toousing hesapları sağlar.

Hello Azure AD yönetici bir kullanıcının erişim paneli hello kullanarak ve çoklu oturum açma bu uygulama için en iyi uyan özelliğini hello türü seçme erişebildiği hangi uygulamaların yapılandırır. Bu türlerinden birini *çoklu oturum parola tabanlı açma*, Azure AD bu uygulama için hello oturum açma işlemi sırasında "Aracısı" bir tür olarak davranmasına izin verir.

Kullanıcılar kendi Kurumsal hesap ile bir kez oturum açın. Merhaba budur düzenli olarak tooaccess kendi Masaüstü veya e-posta kullanırlar, aynı hesabı. Bul ve atanmış olan uygulamalara erişin. Paylaşılan hesaplarıyla, bu uygulamaların listesini herhangi bir sayıda Paylaşılan kimlik bilgileri içerebilir. Merhaba son kullanıcı tooremember gereksinim değil ya da hello çeşitli hesaplar kullanıyor olması yazma.

Paylaşılan hesapları yalnızca gözetim artırmak ve kullanılabilirliği artıran, bunlar Ayrıca, güvenliği artırmak. İzinleri toouse hello kimlik bilgilerine sahip kullanıcılar hello paylaşılan parola görmüyorum, ancak bunun yerine bir kimlik doğrulama bağımsızlıklar akışının bir parçası izinleri toouse hello parola Al. Ayrıca, bazı parola SSO uygulamaları ile Merhaba seçeneği toohave Azure AD elinizde düzenli aralıklarla, hello hesap güvenliği artırma, büyük ve karmaşık parolalar kullanarak rollover (güncelleştirme) hello parola. Hello Yöneticisi kolayca vermek veya erişimi tooan uygulama iptal et ve ayrıca kimin erişim toohello hesabı olduğunu ve kimlerin hello son erişilen bilmeniz.

Azure AD Premium ya da parola tek tüm türleri arasındaki temel lisanslı kullanıcılar, uygulamaları imzalamak herhangi Enterprise Mobility Suite (EMS için), paylaşılan hesaplarını destekler. Önceden tümleştirilmiş uygulamaların hello uygulama galerisinde binlerce hesaplarını paylaşabilir ve kendi parola kimlik doğrulaması uygulamayla ekleyebilirsiniz [özel SSO uygulamaları](active-directory-sso-integrate-saas-apps.md).

Hesap paylaşımını etkinleştir azure AD özellikleri içerir:

* [Parola çoklu oturum açma](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)
* Oturum açma parolası tek Aracısı
* [Grup ataması](active-directory-accessmanagement-self-service-group-management.md)
* Özel parola uygulamalar
* [Uygulama kullanım Pano/raporları](active-directory-passwords-get-insights.md)
* Son kullanıcı erişimi portalları
* [Uygulama proxy'si](active-directory-application-proxy-get-started.md)
* [Active Directory Marketi](https://azure.microsoft.com/marketplace/active-directory/all/)

## <a name="sharing-an-account"></a>Bir hesap paylaşımı
Azure AD toouse tooshare bir hesap gerekecektir:

* Bir uygulama eklemek [uygulama Galerisi](https://azure.microsoft.com/marketplace/active-directory/) veya [özel uygulama](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx)
* Merhaba uygulaması parola çoklu oturum açma (SSO) için yapılandırma
* Kullanım [grup tabanlı atama](active-directory-accessmanagement-group-saasapps.md) ve select hello seçeneği tooenter paylaşılan bir kimlik bilgisi
* İsteğe bağlı: Facebook, Twitter ve LinkedIn, gibi bazı uygulamalarda, hello seçeneğini etkinleştirebilirsiniz [Azure AD parola toplama-üzerinden otomatik](http://blogs.technet.com/b/ad/archive/2015/02/20/azure-ad-automated-password-roll-over-for-facebook-twitter-and-linkedin-now-in-preview.aspx)

Da paylaşılan hesabınızı çok faktörlü kimlik doğrulama (MFA) ile daha güvenli hale getirebilirsiniz (hakkında daha fazla bilgi [uygulamalarını Azure AD ile güvenli hale getirme](../multi-factor-authentication/multi-factor-authentication-get-started.md)) ve uygulama toohello kullanarak erişimini sahip hello özelliği toomanage temsilci [Azure AD Self Servis](active-directory-accessmanagement-self-service-group-management.md) Grup Yönetimi.

## <a name="related-articles"></a>İlgili makaleler
* [Azure Active Directory'de Uygulama Yönetimi için Makale Dizini](active-directory-apps-index.md)
* [Koşullu erişim ile uygulamaları koruma](active-directory-conditional-access.md)
* [Self Servis Grup Yönetimi/SSAA](active-directory-accessmanagement-self-service-group-management.md)

