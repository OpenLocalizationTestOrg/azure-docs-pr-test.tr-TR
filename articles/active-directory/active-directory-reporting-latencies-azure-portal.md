---
title: Gecikme raporlama Azure Active Directory | Microsoft Docs
description: "Azure portalında göstermeyi raporlama olayları için geçen süreyi hakkında bilgi edinin"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: mtillman
editor: 
ms.assetid: 9b88958d-94a2-4f4b-a18c-616f0617a24e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/15/2017
ms.author: markvi;dhanyahk
ms.reviewer: dhanyahk
ms.openlocfilehash: 5ec41817fede495b8262e28d2d614a480d98ff3b
ms.sourcegitcommit: 68aec76e471d677fd9a6333dc60ed098d1072cfc
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/18/2017
---
# <a name="azure-active-directory-reporting-latencies"></a>Gecikme raporlama Azure Active Directory

İle [raporlama](active-directory-preview-explainer.md) Azure Active Directory ortamınızı nasıl çalıştığını belirlemek için gereken tüm bilgileri alın. Veri raporlama için Azure Portalı'nda gösterilmesi için gereken süre miktarını gecikme süresi de denir. 

Bu konu Azure Portalı'ndaki tüm raporlama kategorileri gecikme bilgileri listeler. 


## <a name="activity-reports"></a>Etkinlik raporları

Etkinlik Raporlama iki alan vardır:

- **Oturum açma etkinlikleri**: Yönetilen uygulamaların kullanımı ve kullanıcıların oturum açma etkinlikleri hakkında bilgiler
- **Denetim günlükleri** - Kullanıcılar ve grup yönetimi, yönetilen uygulamalarınız ve dizin etkinlikleriniz hakkında sistem etkinliği bilgileri

Aşağıdaki tabloda, etkinlik raporları gecikme bilgileri listeler.

| Rapor | Minimum | Ortalama | Açıklamalar |
| :-- | --- | --- | :-- |
| Denetim günlükleri | 30 dakika  | 1 saat  |Bazı durumlarda, gösterilmeye denetim etkinlik verilerini 2 saate kadar sürebilir.|
| Oturum açma işlemleri | 15 dakika  | 2 saat |Bazı durumlarda, oturum açma etkinliği veri görünmesini 24 saate kadar sürebilir. Bu, eski office uygulamalarından gelen oturum açma işlemleri etkinlik verilerini içerir. |







## <a name="security-reports"></a>Güvenlik raporları

Raporlama güvenliği, iki alan vardır:

- **Riskli oturum açma işlemleri** - Riskli oturum açma işlemi bir kullanıcı hesabının meşru sahibi olmayan bir kişi tarafından gerçekleştirilmiş olabilecek oturum açma girişiminin göstergesidir. 
- **Riskli oldukları belirlenen kullanıcılar** - Riskli kullanıcı, güvenliği tehlikeye girmiş olabilecek bir kullanıcı hesabının göstergesidir. 

Aşağıdaki tabloda güvenlik raporları gecikme bilgileri listeler.

| Rapor | Minimum | Ortalama | Maksimum |
| :-- | --- | --- | --- |
| Risk altındaki kullanıcılar          | 5 dakika   | 15 dakika  | 2 saat  |
| Riskli oturum açma işlemleri         | 5 dakika   | 15 dakika  | 2 saat  |

## <a name="risk-events"></a>Risk olayları

Azure Active Directory kullanıcı hesaplarınızı ilgili kuşkulu eylemleri algılamak için Uyarlamalı machine learning algoritmaları ve buluşsal yöntemler kullanır. Her kuşkulu eylem bir kayıt çağrılan risk olayı depolanan algıladı.

Aşağıdaki tabloda, risk olaylarını gecikme bilgileri listeler.

| Rapor | Minimum | Ortalama | Maksimum |
| :-- | --- | --- | --- |
| Anonim IP adreslerinden oturum açma işlemleri |5 dakika |15 dakika |2 saat |
| Alışılmadık konumlardan oturum açma işlemleri |5 dakika |15 dakika |2 saat |
| Sızan kimlik bilgilerine sahip kullanıcılar |2 saat |4 saat |8 saat |
| Alışılmadık konumlara imkansız seyahat |5 dakika |1 saat |8 saat  |
| Bulaşma olan cihazlardan oturum açma işlemleri |2 saat |4 saat |8 saat  |
| Şüpheli etkinlik gösteren IP adreslerinden gerçekleştirilen oturum açma işlemleri |2 saat |4 saat |8 saat  |



## <a name="next-steps"></a>Sonraki adımlar

Azure portalında etkinlik raporları hakkında daha fazla bilgi edinmek istiyorsanız, bkz:

- [Azure Active Directory portalında oturum açma etkinliği raporları](active-directory-reporting-activity-sign-ins.md)
- [Azure Active Directory portalında denetim etkinlik raporları](active-directory-reporting-activity-audit-logs.md)

Azure portalında güvenlik raporları hakkında daha fazla bilgi edinmek istiyorsanız, bkz:

- [Azure Active Directory portalında risk güvenlik raporu kullanıcılar](active-directory-reporting-security-user-at-risk.md)
- [Azure Active Directory portalında riskli oturum açma işlemleri raporu](active-directory-reporting-security-risky-sign-ins.md)

Risk olaylar hakkında daha fazla bilgi edinmek istiyorsanız, bkz: [Azure Active Directory risk olaylarını](active-directory-reporting-risk-events.md).
