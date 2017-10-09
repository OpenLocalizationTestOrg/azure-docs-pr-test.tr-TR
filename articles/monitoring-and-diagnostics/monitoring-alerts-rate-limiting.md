---
title: "SMS, e-postalar ve Web kancalarını aaaRate sınırlama | Microsoft Docs"
description: "Azure olası SMS, e-posta veya Web kancası bildirimleri bir eylem grubundan hello sayısını nasıl sınırlar anlayın."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: ancav
ms.openlocfilehash: 1cd08a5b982c82bb02e0bf93451aa1fcd9bc34af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="rate-limiting-for-sms-messages-emails-and-webhook-posts"></a>SMS iletileri, e-postalar ve Web kancası için gönderileri sınırlama oranı
Hız sınırlaması tooa belirli telefon numarası veya e-posta adresi çok fazla bildirimler gönderildiğinde oluşan bildirimleri ertelenmesi olur. Hız sınırlaması uyarıları yönetilebilir ve kullanılabilir olmasını sağlar.

SMS ve e-posta için hello kuralları aynı hello. Merhaba hızı sınırı eşik ise:

 - **SMS**: bir saat içinde 10 iletileri.
 - **E-posta**: 100 iletileri bir saat içinde.

## <a name="rate-limit-rules"></a>Hızı sınırı kuralları
- Belirli bir telefon numarası veya e-posta hello eşik izin verdiğinden daha fazla ileti aldığında sınırlı hızıdır.
- Bir telefon numarası veya e-posta çok sayıda abonelikleri eylem gruplarının bir parçası olabilir. Hız sınırlaması abonelikler arasında geçerlidir. Merhaba eşiğe hemen birden çok aboneliklerden gönderilen iletileri olsa bile geçerlidir.  
- Bir telefon numarası veya e-posta oranı sınırlı olduğunda, başka bir bildirim toocommunicate gönderilir hız sınırlaması hello. Merhaba durumları hello zaman sınırlaması oranı bildirim süresi dolar.

## <a name="rate-limit-of-webhooks"></a>Web kancası hızı sınırı ##
Web kancası için yerinde sınırlama kuru yoktur.

## <a name="next-steps"></a>Sonraki adımlar ##
* Daha fazla bilgi edinmek [SMS uyarı davranış](monitoring-sms-alert-behavior.md).
* Alma bir [etkinlik günlüğü uyarıları genel bakış](monitoring-overview-alerts.md)ve öğrenin nasıl tooreceive uyarıları.  
* Nasıl çok öğrenin[hizmeti sistem durumu bildirimi gönderilen her uyarıları yapılandırmak](monitoring-activity-log-alerts-on-service-notifications.md).
