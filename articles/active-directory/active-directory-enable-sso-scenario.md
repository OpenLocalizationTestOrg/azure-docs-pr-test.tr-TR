---
title: "Azure Active Directory ile uygulamaları aaaManaging | Microsoft Docs"
description: "Şirket içi, Bulut ve SaaS uygulamaları ile Azure Active Directory Tümleştirme Bu makale hello avantajlarını."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 95b96f10-2d5c-4b78-8af8-d3657a24140f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: asteen
ms.openlocfilehash: 0016f8b433e101d8a150bc6d9be3931851578241
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-applications-with-azure-active-directory"></a>Azure Active Directory ile uygulamaları yönetme
Merhaba gerçek iş akışı veya içeriği işletmeler tüm uygulamalar için iki temel gereksinimlere sahiptir:

1. tooincrease üretkenlik uygulamaları kolayca toodiscover ve erişim olmalıdır
2. tooenable güvenlik ve idare, hello kuruluşun denetimi ve Gözetimi kimlerin ve her uygulamanın gerçekten erişiyor üzerinde gerekir.

İçinde bu en iyi sonucu elde edilebilir kimlik toocontrol kullanarak bulut uygulamalarının Merhaba Dünya "*kim toodo ne izin*".

Terminolojisi bilgisayar:

* *Kimin* olarak bilinen *kimlik* -hello kullanıcıların ve grupların Yönetimi
* *Ne* olarak bilinen *erişim yönetimi* – hello tooprotected kaynaklarına erişim yönetimi

Her iki bileşenin birlikte olarak da bilinir *kimlik ve erişim yönetimi (IAM)*, hello tarafından tanımlanan [Gartner](http://www.gartner.com/it-glossary/identity-and-access-management-iam) grup olarak "*hello hello sağ sağlayan güvenlik uzmanlık Kişiler tooaccess hello sağ kaynakları hello sağ hello sağ nedeniyle kez*".

Tamam, böylece hello sorun nedir? IAM ise *yönetilmiyor* tümleşik bir çözüm ile tek bir yerde:

* Kimlik yöneticilerin sahip oluşturma ve kullanıcı hesaplarını tüm uygulamalarda ayrı ayrı güncelleştirme tooindividually yedekli ve zaman alıcı etkinlik.
* Kullanıcıların birden çok kimlik bilgilerini tooaccess hello uygulamaları ile toowork ihtiyaç duydukları toomemorize vardır. Sonuç olarak, kullanıcılar parolalarını aşağı toowrite eğilimindedir veya diğer veri güvenlik risklerini de beraberinde getirir diğer parola yönetimi çözümleri kullanın.
* Yedekli, uzun süren etkinlikler kullanıcılar hello miktarını azaltın ve yöneticiler işletmenizin alt çizgi artan iş etkinliklerini çalışıyoruz.

Bu nedenle, kuruluşlar tümleşik IAM çözümleri benimsenmesi gelen engeller genellikle ne?

* Birçok teknik çözümleri dağıtılan ve kendi uygulamaları için her bir kuruluş tarafından uyarlanan toobe gereken yazılım platformlarının dayanır.
* Bulut uygulamalarını genellikle BT organizasyonu mevcut IAM çözümleriyle tümleştirilebilir daha yüksek bir hızda benimsenen.
* Güvenlik ve araç İzleme ek özelleştirme ve tümleştirme tooachieve kapsamlı E2E senaryoları gerektirir.

## <a name="azure-active-directory-integrated-with-applications"></a>Azure Active Directory uygulamalarıyla tümleşik
Azure Active Directory, Microsoft Identity Service (Idaas) çözümü olarak şu:

* Bulut hizmeti olarak IAM sağlar 
* Merkezi erişim yönetimi, çoklu oturum açma (SSO) ve raporlama sağlar 
* Destekleyen tümleşik erişim yönetimi için [uygulamaları binlerce](https://azure.microsoft.com/marketplace/active-directory/) hello uygulama galerisinde Salesforce, Google Apps, kutusunu, Concur ve benzeri. 

Azure Active Directory ile iş ortakları için yayımlama tüm uygulamaları ve müşterilerin (iş veya tüketici) sahip hello aynı kimlik ve erişim yönetimi özellikleri.<br> Bu, toosignificantly işletim maliyetlerini azaltmak olanak tanır.

Ne tooimplement hello uygulama galerisinde henüz listelenmeyen bir uygulama gerekiyor? Bu uygulamalar hello uygulama galerisinden için SSO yapılandırmaktan biraz daha uzun süren olmakla birlikte, Azure AD hello yapılandırmayla yardımcı olan bir sihirbaz sağlar.

Azure AD Hello değerini "yalnızca" bulut uygulamalarını gider. Ayrıca, ile şirket içi uygulamalara güvenli uzaktan erişim sağlayarak kullanabilirsiniz. Güvenli uzaktan erişim VPN veya diğer geleneksel uzaktan erişim yönetimi uygulamaları hello hello gereksinimini ortadan kaldırabilirsiniz.

Merkezi erişim yönetimi ve çoklu oturum açma (SSO) için tüm uygulamalarınızı sağlayarak, Azure AD toohello ana veri güvenliği ve üretkenlik sorunlarını hello çözümü sağlar.

* Kullanıcılar daha fazla zaman tooincome bitti oluşturma veya iş işlemleri etkinlikleri vermiş üzerinde bir oturum ile birden çok uygulama erişebilir.
* Kimlik Yöneticiler tek bir yerde erişim tooapplications yönetebilir.

Merhaba avantajı hello kullanıcı ve şirketiniz için açıktır. Bir kimlik yöneticisi ve hello kuruluş hello avantajları daha yakın bir göz atalım.

## <a name="integrated-application-benefits"></a>Tümleşik uygulama avantajları
Merhaba SSO işleminin iki adımı vardır:

* Kimlik doğrulaması, hello hello kullanıcının kimliğini doğrulama işlemi.
* Yetkilendirme kararı tooenable hello veya bir erişim ilkesi ile erişim tooa kaynak engelleyin.

Azure AD toomanage uygulamaları ve etkinleştir SSO kullanırken:

* Merhaba kullanıcının şirket içi (örneğin, AD) veya Azure AD hesabının kimlik doğrulaması yapılır.
* Atama ve koruma hello Azure AD ilkesinde tutarlı bir son kullanıcı deneyimi sağlamak ve tooadd atama, konumları ve iç yeteneklerini bağımsız olarak herhangi bir uygulama MFA koşullara etkinleştirme yetkilendirme yürütür.

Bu şekilde hello yetkilendirme hello toounderstand hello hedef uygulamaya geçirilmeden önemli nasıl Merhaba uygulaması Azure AD ile tümleşik bağlı olarak değişir.

* **Uygulama hizmeti sağlayıcısı tarafından önceden tümleştirilmiş** gibi Office 365 ve Azure, bunlar doğrudan Azure AD'de oluşturulmuş ve kapsamlı kimlik ve erişim yönetimi yeteneklerini için ona bağlı olan uygulamalar. Erişim toothese uygulamaları dizin bilgileri ve belirteç verme etkindir.
* **Uygulamalar önceden tümleştirilmiş Microsoft ve özel uygulamalar tarafından** bir iç uygulama dizini kullanır ve Azure AD bağımsız olarak çalışabilir bağımsız bulut uygulamaları şunlardır. Erişim toothese uygulamalar, uygulama eşlenen belirli kimlik bilgisi tooan uygulama hesabı vererek etkindir. Merhaba uygulama özellikleri bağlı olarak, bir Federasyon belirteç veya kullanıcı adı ve hello uygulamada önceden hazırlanmış olan bir hesabın parolasını hello kimlik bilgisi olabilir.
* **Şirket içi uygulamalara** öncelikle erişim tooon içi uygulamaları etkinleştirme hello Azure AD uygulama proxy'si aracılığıyla yayımlanan uygulamaları. Bu uygulamaları Windows Server Active Directory gibi bir merkezi şirket içi dizin kullanır. Erişim toothese uygulamaları hello proxy toodeliver hello uygulama içerik toohello son kullanıcı oturum açma hello şirket içi gereksinim uygularken sırasında tetikleme tarafından etkindir.

Bir kullanıcı, kuruluşa katılan, örneğin, toocreate bir hesap hello kullanıcı için oturum açma hello birincil işlemleri için Azure AD'de gerekir. Bu kullanıcı erişimi tooa yönetilen uygulama Salesforce gibi gerektiriyorsa, ayrıca Salesforce bu kullanıcı için bir hesap toocreate gerekir ve toohello Azure hesabı toomake SSO iş bağlayın. Merhaba kullanıcı kuruluşunuzdan ayrıldığında önerilir toodelete hello Azure AD hesabının olduğu ve IAM depoları hello uygulamaların hello kullanıcının erişebildiği tüm karşılık gelen hesaplarında hello.

## <a name="access-detection"></a>Erişim algılama
Modern kuruluşlarda, BT departmanları, kullanılmakta olan tüm hello bulut uygulamaları tanımaz genellikle. Azure AD Cloud App Discovery ile birlikte, bu uygulamaları ile bir çözüm toodetect sağlar.

## <a name="account-management"></a>Hesap yönetimi
Geleneksel olarak, hello hesaplarını yönetmek çeşitli uygulamalar tarafından gerçekleştirilen bir el ile işlem olup BT veya hello kuruluşta kişisel destekler. Azure AD hesap yönetimi tüm hizmet sağlayıcısı tümleşik uygulamalar ve otomatik kullanıcı sağlamayı destekleyen Microsoft veya SAML JIT tarafından önceden tümleştirilmiş uygulamaların tam otomatik.

## <a name="automated-user-provisioning"></a>Otomatik kullanıcı hazırlama
Bazı uygulamalar Otomasyon arabirimleri oluşturma ve temizleme (veya devre dışı bırakma) hesaplarının sağlayın. Bir sağlayıcı böyle bir arabirim sunuyorsa, Azure AD tarafından yararlanır. Bu yönetim görevlerini otomatik olarak gerçekleşir, işletim maliyetlerini azaltır ve yetkisiz erişim olasılığını hello azalttığından ortamınızın hello güvenliğini artırır.

## <a name="access-management"></a>Erişim Yönetimi
Azure AD kullanarak erişim tooapplications tek tek kullanarak veya atamaları güdümlü kural yönetebilirsiniz. Ayrıca, erişim yönetimi toohello doğru kişilerin hello kuruluş sağlama hello en iyi gözetim ve Yardım Masası üzerindeki azalan hello yük devredebilirsiniz.

## <a name="on-premises-applications"></a>Şirket içi uygulamalar
Uygulama proxy'si yerleşik hello toopublish tutarlı ikisinde kaynaklanan, şirket içi uygulamalar tooyour kullanıcılarınızın Azure AD izleme, raporlama ve güvenlik özellikleri modern bulut uygulama ve hello avantajlarını deneyimiyle erişim sağlar .

## <a name="reporting-and-monitoring"></a>Raporlama ve izleme
Azure AD önceden tümleştirilmiş raporlama ve izleme kimin erişimi tooapplications olduğunu ve bunlar aslında bunları kullanıldığında tooknow sağlayan özellikler sunar.

## <a name="related-capabilities"></a>İlgili özellikleri
Azure AD ile ayrıntılı erişim ilkeleri ve önceden tümleştirilmiş MFA uygulamalarınızla güvenliğini sağlayabilirsiniz. Azure MFA hakkında daha fazla toolearn [Azure MFA](https://azure.microsoft.com/services/multi-factor-authentication/).

## <a name="getting-started"></a>Başlarken
uygulamaları Azure AD ile tümleştirme başlatılan tooget ele hello göz [Azure Active Directory Tümleştirme alma uygulamalarla Başlangıç Kılavuzu](active-directory-integrating-applications-getting-started.md).

## <a name="see-also"></a>Ayrıca bkz.
[Azure Active Directory'de Uygulama Yönetimi için Makale Dizini](active-directory-apps-index.md)

