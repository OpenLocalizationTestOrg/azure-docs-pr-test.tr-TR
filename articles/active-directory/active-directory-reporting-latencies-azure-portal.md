---
title: aaaAzure Active Directory raporlama gecikmeleri | Microsoft Docs
description: "Merhaba, olayları tooshow ayarlama, Azure portalında raporlama için geçen süreyi hakkında bilgi edinin"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 9b88958d-94a2-4f4b-a18c-616f0617a24e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi;dhanyahk
ms.reviewer: dhanyahk
ms.openlocfilehash: eee959331262ba59b313dd038cb54699dbef48a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-latencies"></a>Gecikme raporlama Azure Active Directory

İle [raporlama](active-directory-preview-explainer.md) hello Azure Active Directory, toodetermine ortamınızı nasıl yapılması gereken tüm hello bilgileri alın. Merhaba hello Azure portal'ın veri tooshow yukarı olarak da bilinen gecikme raporlama için geçen süre miktarı. 

Bu konuda hello hello gecikme bilgileri hello Azure portal tüm raporlama kategorilerini listeler. 


## <a name="activity-reports"></a>Etkinlik raporları

Etkinlik Raporlama iki alan vardır:

- **Oturum açma etkinliklerini** – yönetilen uygulamalar ve kullanıcı oturum açma etkinliklerini hello kullanımı hakkında bilgi
- **Denetim günlükleri** - Kullanıcılar ve grup yönetimi, yönetilen uygulamalarınız ve dizin etkinlikleriniz hakkında sistem etkinliği bilgileri

Aşağıdaki tablonun hello hello gecikme bilgileri etkinlik raporları listeler.

| Rapor | Minimum | Ortalama | Maksimum |
| :-- | --- | --- | --- |
| Denetim günlükleri             | 30 dakika  | 45 dakika | 1 saat     |
| Oturum açma işlemleri               | 15 dakika  | 15 dakika | 2 saat *   |

>[!NOTE]
> Eski office uygulamalarından gelen gerçekleştirilen oturum açma etkinliği için bazı veriler, veri tooshow yukarı raporlama hello too8 saat sürebilir. 


## <a name="security-reports"></a>Güvenlik raporları

Raporlama güvenliği, iki alan vardır:

- **Riskli oturum açma işlemleri** -bir riskli oturum açma bir hello meşru bir kullanıcı hesabının sahibi olmayan kişi tarafından gerçekleştirilmiş olabilecek bir oturum açma girişimi için göstergesidir. 
- **Riskli oldukları belirlenen kullanıcılar** - Riskli kullanıcı, güvenliği tehlikeye girmiş olabilecek bir kullanıcı hesabının göstergesidir. 

Aşağıdaki tablonun hello hello gecikme bilgileri güvenlik raporları listeler.

| Rapor | Minimum | Ortalama | Maksimum |
| :-- | --- | --- | --- |
| Risk altındaki kullanıcılar          | 5 dakika   | 15 dakika  | 2 saat  |
| Riskli oturum açma işlemleri         | 5 dakika   | 15 dakika  | 2 saat  |

## <a name="risk-events"></a>Risk olayı

Azure Active Directory Uyarlamalı machine learning, ilgili tooyour kullanıcı hesapları olan algoritmalar ve buluşsal yöntemler toodetect şüpheli eylemleri kullanır. Her kuşkulu eylem bir kayıt çağrılan risk olayı depolanan algıladı.

Aşağıdaki tablonun hello hello gecikme bilgileri risk olaylarını listeler.

| Rapor | Minimum | Ortalama | Maksimum |
| :-- | --- | --- | --- |
| Anonim IP adreslerinden oturum açma işlemleri |5 dakika |15 dakika |2 saat |
| Alışılmadık konumlardan oturum açma işlemleri |5 dakika |15 dakika |2 saat |
| Sızan kimlik bilgilerine sahip kullanıcılar |2 saat |4 saat |8 saat |
| Mümkün olmayan seyahat tooatypical konumları |5 dakika |1 saat |8 saat  |
| Virüs bulaşmış cihazlardan oturum açma işlemleri |2 saat |4 saat |8 saat  |
| Şüpheli etkinlik gösteren IP adreslerinden gerçekleştirilen oturum açma işlemleri |2 saat |4 saat |8 saat  |



## <a name="next-steps"></a>Sonraki adımlar

Tooknow hello Azure portal'ın hello etkinlik raporları hakkında daha fazla bilgi istiyorsanız, bkz:

- [Hello Azure Active Directory portalında oturum açma etkinliği raporları](active-directory-reporting-activity-sign-ins.md)
- [Etkinlik raporları hello Azure Active Directory portalında denetleme](active-directory-reporting-activity-audit-logs.md)

Tooknow hello Azure portal'ın hello güvenlik raporları hakkında daha fazla bilgi istiyorsanız, bkz:

- [Risk güvenlik raporu hello Azure Active Directory portalında kullanıcılar](active-directory-reporting-security-user-at-risk.md)
- [Hello Azure Active Directory portalında riskli oturum açma işlemleri raporu](active-directory-reporting-security-risky-sign-ins.md)

Tooknow risk olaylar hakkında daha fazla bilgi istiyorsanız, bkz: [Azure Active Directory risk olaylarını](active-directory-reporting-risk-events.md).
