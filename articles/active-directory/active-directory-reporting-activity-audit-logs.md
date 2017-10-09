---
title: "aaaAudit etkinlik raporları hello Azure Active Directory portalında | Microsoft Docs"
description: "Giriş toohello denetim hello Azure Active Directory portalında etkinlik raporları"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: a1f93126-77d1-4345-ab7d-561066041161
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 1567673f5030fc707b017c069f2ba7587962e5cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="audit-activity-reports-in-hello-azure-active-directory-portal"></a>Etkinlik raporları hello Azure Active Directory portalında denetleme 

Azure Active Directory (Azure AD) raporlama ile ortamınızı nasıl çalıştığını toodetermine gereksinim hello bilgileri elde edebilirsiniz.

Azure AD raporlama mimarisi hello bileşenleri aşağıdaki Merhaba oluşur:

- **Etkinlik** 
    - **Oturum açma etkinliklerini** – yönetilen uygulamalar ve kullanıcı oturum açma etkinliklerini hello kullanımı hakkında bilgi
    - **Denetim günlükleri**: Kullanıcılar ve grup yönetimi, yönetilen uygulamalarınız ve dizin etkinlikleriniz hakkında sistem etkinliği bilgileri.
- **Güvenlik** 
    - **Riskli oturum açma işlemleri** -bir riskli oturum açma bir hello meşru bir kullanıcı hesabının sahibi olmayan kişi tarafından gerçekleştirilmiş olabilecek bir oturum açma girişimi için göstergesidir. Daha fazla bilgi için bkz. Riskli oturum açma işlemleri.
    - **Riskli oldukları belirlenen kullanıcılar** - Riskli kullanıcı, güvenliği tehlikeye girmiş olabilecek bir kullanıcı hesabının göstergesidir. Daha fazla bilgi için bkz. Riskli oldukları belirlenen kullanıcılar.

Bu konuda hello denetim etkinlikleri genel bir bakış sağlar.
 
## <a name="who-can-access-hello-data"></a>Merhaba veri erişebilecek mi?
* Merhaba Güvenlik Yöneticisi veya güvenlik okuyucu roldeki kullanıcılar
* Genel Yöneticiler
* Bireysel kullanıcılar (yönetici olmayanlar) kendi etkinliklerini görebilir


## <a name="audit-logs"></a>Denetim günlükleri

Azure Active Directory'de Hello denetim günlüklerini kayıtları sistem etkinliklerin uyumluluk sağlar.  
İlk giriş noktası verileri denetleme tooall olan **denetim günlüklerini** hello içinde **etkinlik** bölümünü **Azure Active Directory**.

![Denetim günlükleri](./media/active-directory-reporting-activity-audit-logs/61.png "Denetim günlükleri")

Denetim günlüklerinin aşağıdakileri gösteren bir varsayılan liste görünümü vardır:

- Başlangıç tarihi ve saati hello oluşum
- Başlatıcı hello / aktör (*kimin*) etkinliğin 
- Merhaba etkinliği (*ne*) 
- Merhaba hedef

![Denetim günlükleri](./media/active-directory-reporting-activity-audit-logs/18.png "Denetim günlükleri")

Tıklatarak hello liste görünümü özelleştirebilirsiniz **sütunları** hello araç.

![Denetim günlükleri](./media/active-directory-reporting-activity-audit-logs/19.png "Denetim günlükleri")

Bu toodisplay ek alanlar etkinleştirir veya zaten görüntülenen alanları kaldırın.

![Denetim günlükleri](./media/active-directory-reporting-activity-audit-logs/21.png "Denetim günlükleri")


Merhaba liste görünümünde bir öğeyi tıklatarak bunu hakkında tüm kullanılabilir ayrıntıları alın.

![Denetim günlükleri](./media/active-directory-reporting-activity-audit-logs/22.png "Denetim günlükleri")


## <a name="filtering-audit-logs"></a>Denetim günlüklerini filtreleme

Merhaba aşağı toonarrow veri tooa düzeyinde çalışır, alanları izleyen hello kullanarak hello denetim verileri filtreleyebilirsiniz bildirdi:

- Tarih aralığı
- Başlatan (Aktör)
- Kategori
- Etkinlik kaynak türü
- Etkinlik

![Denetim günlükleri](./media/active-directory-reporting-activity-audit-logs/23.png "Denetim günlükleri")


Merhaba **tarih aralığı** filtre etkinleştirir tooyou toodefine hello için bir zaman çerçevesi veri döndürdü.  
Olası değerler şunlardır:

- 1 ay
- 7 gün
- 24 saat
- Özel

Özel bir zaman çerçevesi seçerken başlangıç ve bitiş zamanını yapılandırabilirsiniz.

Merhaba **tarafından başlatılan** filtre, toodefine bir aktör'ın adı veya evrensel asıl adı (UPN) sağlar.

Merhaba **kategori** filtre filtre aşağıdaki Merhaba, tooselect sağlar:

- Tümü
- Çekirdek kategori
- Çekirdek dizin
- Self servis parola yönetimi
- Self servis grup yönetimi
- Hesap sağlama - Otomatik parola geçişi
- Davetli kullanıcılar
- MIM hizmeti
- Kimlik Koruması
- B2C

Merhaba **etkinlik kaynak türü** filtre hello aşağıdakilerden birini filtreler tooselect sağlar:

- Tümü 
- Grup
- Dizin
- Kullanıcı
- Uygulama
- İlke
- Cihaz
- Diğer

Seçtiğinizde, **grup** olarak **etkinlik kaynak türü**, tooalso sağlayan bir ek filtre kategorisi alma sağlayan bir **kaynak**:

- Azure AD
- O365


Merhaba **etkinlik** filtre hello kategori ve etkinlik kaynak türü seçimi yaptığınız dayanır. Belirli bir etkinliğe toosee istediğiniz ya da Tümünü Seç seçebilirsiniz. 

Merhaba grafik API'si https://graph.windows.net/$ tenantdomain/etkinlikleri/auditActivityTypes kullanarak tüm denetim etkinlikleri hello listesini elde edebilirsiniz? api sürümü beta = nerede $tenantdomain = etki alanı adı veya toohello makalesine başvurun [denetleme raporu olayları](active-directory-reporting-audit-events.md).


## <a name="audit-logs-shortcuts"></a>Denetim günlükleri kısayolları

Ayrıca çok**Azure Active Directory**, hello Azure portal, iki ek giriş noktaları ile tooaudit verileri sağlar:

- Kullanıcılar ve gruplar
- Kurumsal uygulamalar

### <a name="users-and-groups-audit-logs"></a>Kullanıcı ve gruplara yönelik denetim günlükleri

Kullanıcı ve grup tabanlı denetim raporları ile yanıtlar tooquestions gibi alabilirsiniz:

- Hangi güncelleştirme türlerini uygulanan hello kullanıcılar silinmiş?

- Kaç adet kullanıcı değiştirildi?

- Kaç adet parola değiştirildi?

- Bir yönetici bir dizinde neler yaptı?

- Eklenen hello grupları nelerdir?

- Üyelik değişiklikleri olan gruplar var mı?

- Grubun sahiplerini Hello değişti mi?

- Hangi lisansları tooa grup veya kullanıcı atanmış?

Yalnızca ilgili toousers ve gruplar verileri denetleme tooreview istiyorsanız, filtre uygulanmış bir görünüm altında bulabilirsiniz **denetim günlüklerini** hello içinde **etkinlik** hello bölümünü **kullanıcılar ve gruplar**. Bu giriş noktasında, **Etkinlik Kaynağı Türü** olarak **Kullanıcılar ve gruplar** önceden seçilidir.

![Denetim günlükleri](./media/active-directory-reporting-activity-audit-logs/93.png "Denetim günlükleri")

### <a name="enterprise-applications-audit-logs"></a>Kurumsal uygulamaların denetim günlükleri

Uygulama tabanlı denetim raporları, yanıtları tooquestions gibi alabilirsiniz:

* Eklenen veya güncelleştirilen hello uygulamalar nelerdir?
* Kaldırılan hello uygulamalar nelerdir?
* Belirli bir uygulamaya ait bir hizmet ilkesi değiştirildi mi?
* Uygulamaları Hello adlarını değişti mi?
* Kimin onayı tooan uygulamasını vermiş?

Yalnızca ilgili tooyour uygulamalar verileri denetleme tooreview istiyorsanız, filtre uygulanmış bir görünüm altında bulabilirsiniz **denetim günlüklerini** hello içinde **etkinlik** hello bölümünü **kurumsal uygulamalar**  dikey. Bu giriş noktasında, **Etkinlik Kaynağı Türü** olarak **Kurumsal uygulamalar** önceden seçilidir.

![Denetim günlükleri](./media/active-directory-reporting-activity-audit-logs/134.png "Denetim günlükleri")

Bu görünümü daha fazla toojust aşağı filtreleyebilirsiniz **grupları** veya yalnızca **kullanıcılar**.

![Denetim günlükleri](./media/active-directory-reporting-activity-audit-logs/25.png "Denetim günlükleri")


## <a name="next-steps"></a>Sonraki adımlar

Merhaba raporlama genel bakış için bkz: [Azure Active Directory raporlama](active-directory-reporting-azure-portal.md).

