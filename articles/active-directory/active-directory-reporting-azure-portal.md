---
title: Active Directory aaaAzure raporlama | Microsoft Docs
description: "Azure Active Directory raporlamasına genel bir bakış sağlar."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 6141a333-38db-478a-927e-526f1e7614f4
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: c91813acbdc4b0bfcd164169b0b575accac227d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting"></a>Azure Active Directory raporlama

Azure Active Directory raporlamasıyla, ortamınızın nasıl çalıştığıyla ilgili fikir edinebilirsiniz.  
sağlanan hello veri sağlar:

- Uygulama ve hizmetlerinizin kullanıcılarınız tarafından nasıl kullanıldığını saptayabilirsiniz
- Ortamınızı Hello sağlığını etkileyen olası riskleri Algıla
- Kullanıcılarınızın işlerini yapmalarını engelleyen sorunları giderebilirsiniz  

Merhaba raporlama mimarisi üzerinde iki ana ayaklar dayanır:

- Güvenlik raporları
- Etkinlik raporları

![Raporlama](./media/active-directory-reporting-azure-portal/01.png)



## <a name="security-reports"></a>Güvenlik raporları

Azure Active Directory'de Hello güvenlik raporları, kuruluşunuzdaki kimlikleri, tooprotect yardımcı olur.  
Azure Active Directory'de iki tür güvenlik raporu vardır:

- **Bayrak eklenen kullanıcılar için risk** - hello [bayrak eklenen kullanıcılar için risk güvenlik raporu](active-directory-reporting-security-user-at-risk.md), geçirildiğini kullanıcı hesapları özetini almak.

- **Riskli oturum açma işlemleri** - hello [riskli oturum açma güvenlik raporu](active-directory-reporting-security-risky-sign-ins.md), yasal sahibi bir kullanıcı hesabı olan kişi tarafından gerçekleştirilmiş olabilecek oturum açma denemeleri hello değil için bir gösterge alın. 

**Hangi Azure AD lisans tooaccess bir güvenlik raporu gerekiyor mu?**  
Azure Active Directory'nin tüm sürümlerinde size riskli oldukları belirlenen kullanıcılar ve riskli oturum açma işlemleri raporları sağlanır.  
Bununla birlikte, rapor ayrıntı düzeyini hello hello sürümleri arasında farklılık gösterir: 

- Merhaba, **Azure Active Directory ücretsiz ve Basic sürümleri**, zaten risk ve riskli oturum açma işlemleri için işaretlenen kullanıcıların bir listesini alın. 

- Merhaba **Azure Active Directory Premium 1** edition'ı genişletir bu modeli de tooexamine sağlayarak her rapor için algılanan risk olayı temel hello bazıları. 

- Merhaba **Azure Active Directory Premium 2** edition hello sizinle en hakkında ayrıntılı bilgi risk olaylarını temel hello ve ayrıca, otomatik olarak tooconfigured yanıt tooconfigure güvenlik ilkeleri sağlar sağlar risk düzeyleri.


## <a name="activity-reports"></a>Etkinlik raporları

Azure Active Directory'de iki tür etkinlik raporu vardır:

- **Denetim günlükleri** - hello [denetim günlüklerini Etkinlik Raporu](active-directory-reporting-activity-audit-logs.md) kiracınızda gerçekleştirilen her görev toohello geçmişine erişim sağlar.

- **Oturum açma işlemleri** - hello [gerçekleştirilen oturum açma etkinliği raporu](active-directory-reporting-activity-sign-ins.md), belirleyebilirsiniz, hello denetim günlüklerini raporu tarafından bildirilen hello görevleri gerçekleştiren.



Merhaba **denetim günlüklerini rapor** sistem faaliyetleri kayıtlarıyla için uyumluluk sağlar.
Başkalarının arasında veri tooaddress yaygın senaryolar gibi sağlar hello sağlanan:

- Kişi bilgilerimi Kiracı erişim tooan Yönetici grubu aldı. Ona kim erişim verdi? 

- Kullanıcıların belirli bir uygulamaya imzalama tooknow hello listesini istediğiniz ı itibaren son edildi hello uygulama ve tooknow de yapmak istiyorsanız

- Tooknow kaç parola sıfırlama gerçekleştiği my Kiracı istiyorum


**Hangi Azure AD lisans tooaccess hello denetim günlüklerini rapor gerekiyor mu?**  
Merhaba denetim günlüklerini raporu lisanslara sahip özellikler için kullanılabilir. Belirli bir özellik için bir lisans varsa, günlük bilgilerini Denetim erişim toohello de gerekir.

Daha fazla ayrıntı için bkz: **hello ücretsiz, temel ve Premium sürümlerinde genel olarak kullanılabilir özelliklerini karşılaştırma** içinde [Azure Active Directory özellikleri ve yetenekleri](https://www.microsoft.com/cloud-platform/azure-active-directory-features).   



Merhaba **gerçekleştirilen oturum açma etkinliği raporu** etkinleştirir tootoofind tooquestions gibi yanıt verir:

- Bir kullanıcı oturum açma hello desenini nedir?
- Bir hafta içerisinde kaç adet kullanıcı oturum açtı?
- Bu oturum açma işlemleri hello durumu nedir?


**Hangi Azure AD lisans musunuz tooaccess gerçekleştirilen oturum açma etkinliği raporu hello?**  
gerçekleştirilen oturum açma etkinliği raporu tooaccess Merhaba, Kiracı kendisiyle ilişkili bir Azure AD Premium lisansına sahip olması gerekir.


## <a name="programmatic-access"></a>Programlı erişim

Toplama toohello kullanıcı arabiriminde, Azure Active Directory raporlama da sizinle sağlar [programlı erişim](active-directory-reporting-api-getting-started-azure-portal.md) raporlama verilerini toohello. Bu raporların Hello veriler SIEM sistemleri, Denetim ve iş zekası araçları gibi çok kullanışlı tooyour uygulamalar olabilir. bir dizi REST tabanlı API'ler aracılığıyla programlı erişim toohello veri API'leri sağlamak Hello Azure AD raporlama. Çeşitli programlama dilleri ve araçlarından bu API'leri çağırabilirsiniz. 


## <a name="next-steps"></a>Sonraki adımlar

Azure Active Directory'de çeşitli rapor türleri tooknow hello hakkında daha fazla bilgi istiyorsanız, bkz:

- [Riskli olarak işaretlenen kullanıcılar raporu](active-directory-reporting-security-user-at-risk.md)
- [Riskli oturum açma işlemleri raporu](active-directory-reporting-security-risky-sign-ins.md)
- [Denetim günlükleri raporu](active-directory-reporting-activity-audit-logs.md)
- [Oturum açma günlükleri raporu](active-directory-reporting-activity-sign-ins.md)

Tooknow API raporlama hello kullanarak verileri raporlama hello hello erişme hakkında daha fazla bilgi istiyorsanız, bkz: 

- [Hello Azure Active Directory raporlama API'si ile çalışmaya başlama](active-directory-reporting-api-getting-started-azure-portal.md)


<!--Image references-->
[1]: ./media/active-directory-reporting-azure-portal/ic195031.png