---
title: "Eylem grupları SMS uyarı davranışını | Microsoft Docs"
description: "SMS ileti biçimi ve SMS iletileri aboneliğinizi iptal etmek için yanıt resubscribe veya Yardım isteyin."
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
ms.openlocfilehash: 012f001356463a8a7d9b95f186111959627f2c28
ms.sourcegitcommit: b07d06ea51a20e32fdc61980667e801cb5db7333
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/08/2017
---
# <a name="sms-alert-behavior-in-action-groups"></a>SMS eylemi gruplarındaki davranışı uyar
## <a name="overview"></a>Genel Bakış ##
Eylem grupları alıcıları listesini yapılandırmanıza olanak sağlar. Bu gruplar daha sonra etkinlik günlüğü uyarıları tanımlarken yararlanılabilir; Etkinlik günlüğü uyarı tetiklendiğinde, belirli bir eylem grubu bildirim sağlama. Desteklenen uyarı mekanizmaları SMS biridir; Uyarıları çift yönlü iletişimi destekler. Bir kullanıcı için bir uyarı yanıt vermesini sağlayabilirsiniz:

- **Uyarılardan aboneliği:** bir kullanıcı tüm Eylem grupları veya tekil eylem grubu için tüm SMS uyarılardan aboneliğinizi iptal edebilirsiniz.  
- **Uyarılar resubscribe:** bir kullanıcı için tüm Eylem grupları veya tekil eylem grubu için tüm SMS uyarıları resubscribe.  
- **Yardım isteğinde:** bir kullanıcı SMS hakkında daha fazla bilgi isteyebilir. Bu makalede yönlendirilir

Bu makalede, SMS uyarıları davranışını yer almaktadır ve yanıt kullanıcıya kullanıcının bölgesel ayarına göre eylemleri gerçekleştirebilirsiniz:

## <a name="usacanada-sms-behavior"></a>ABD/Kanada SMS davranışı
### <a name="receiving-an-sms-alert"></a>SMS uyarı alma
Bir uyarı oluşturulduğunda bir eylem grubunun bir parçası yapılandırılmış bir SMS alıcı SMS alır. SMS aşağıdaki bilgileri yürütecek:
* Bu uyarı gönderildiği eylem grubunun kısaad
- Uyarı başlığı

### <a name="unsubscribing-from-sms-alerts-for-one-action-group"></a>Aboneliğini iptal etmek için bir eylem grubu SMS uyarıları
Bir kullanıcı SMS uyarılar için bir eylem grubu için anahtar sözcükleri kısa koduyla 29873 yanıtlama aboneliğinizi iptal edebilirsiniz: "devre dışı &lt;eylem grubunun kısaad&gt;".

Örn Kısaad "Azure" ile bir eylem grubu için uyarıları aboneliğinizi iptal etmek isteyen bir kullanıcı bir SMS "Azure devre dışı bırak" diyen kısa koda 29873 göndermek

### <a name="unsubscribing-from-sms-alerts-for-all-action-groups"></a>Tüm Eylem grupları için SMS uyarı aboneliğini
Bir kullanıcının tüm Eylem grupları için tüm SMS uyarılardan kısa bir kod aşağıdaki anahtar sözcükler biriyle 29873 yanıtlama aboneliğinizi iptal edebilirsiniz:
* DURDUR

Örn Tüm Eylem grupları için tüm SMS uyarıları aboneliğinizi iptal etmek isteyen bir kullanıcı bir SMS "Durdur" diyen kısa koda 29873 göndermek

>[!NOTE]
>Bir kullanıcı iptal etti SMS uyarır, ancak daha sonra yeni bir eylem grubuna eklenir; Bunlar yeni o eylemi grubu SMS uyarı almak, ancak tüm önceki eylem gruplarından aboneliği kalır.
>
>

### <a name="resubscribing-to-sms-alerts-for-one-action-group"></a>Bir eylem grubu için SMS uyarılar resubscribing
Bir kullanıcı SMS için bir eylem grubu için uyarılar için anahtar sözcükleri kısa koduyla 29873 yanıtlama resubscribe: "etkinleştirme &lt;eylem grubunun kısaad&gt;".

Örn Kısaad "Azure" ile bir eylem grubu için uyarılar resubscribe isteyen bir kullanıcı bir SMS "Azure etkinleştir" diyen kısa koda 29873 göndermek

### <a name="resubscribing-to-sms-alerts-for-all-action-groups"></a>Tüm Eylem grupları için SMS uyarıları resubscribing
Bir kullanıcı için tüm Eylem grupları için uyarılar için tüm SMS kısa bir kod aşağıdaki anahtar sözcükler biriyle 29873 yanıtlama resubscribe:

* BAŞLAT

Örn Tüm Eylem grupları için tüm SMS uyarıları aboneliğinizi iptal etmek isteyen bir kullanıcı bir SMS "Başlat" diyen kısa koda 29873 göndermek

### <a name="requesting-help-via-sms"></a>SMS aracılığıyla Yardım isteme
Bir kullanıcı, kısa bir kod aşağıdaki anahtar sözcükler biriyle 29873 yanıt tarafından alınan SMS hakkında daha fazla bilgi için isteyebilirsiniz:
* YARDIM

Yanıt, kullanıcıya bu makaleye bir bağlantı gönderilir.

## <a name="next-steps"></a>Sonraki Adımlar
Alma bir [etkinlik günlüğü uyarıları genel bakış](monitoring-overview-alerts.md) ve uyarı öğrenin  
Daha fazla bilgi edinmek [SMS hız sınırı](monitoring-alerts-rate-limiting.md)  
Daha fazla bilgi edinmek [Eylem grupları](monitoring-action-groups.md)
