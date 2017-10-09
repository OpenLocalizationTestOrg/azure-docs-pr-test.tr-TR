---
title: "Eylem grupları uyarı davranışını aaaSMS | Microsoft Docs"
description: "SMS ileti biçimi ve yanıt veren tooSMS iletileri toounsubscribe resubscribe veya Yardım isteyin."
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
ms.openlocfilehash: 3cd09b1903e3472f6402f62b74409d97e7e7ea97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sms-alert-behavior-in-action-groups"></a>SMS eylemi gruplarındaki davranışı uyar
## <a name="overview"></a>Genel Bakış ##
Eylem grupları tooconfigure alıcıları listesini etkinleştirin. Bu gruplar daha sonra etkinlik günlüğü uyarıları tanımlarken yararlanılabilir; Hello etkinlik günlüğü uyarı tetiklendiğinde, belirli bir eylem grubu bildirim sağlama. Mekanizmaları desteklenen uyarı hello SMS biridir; Merhaba uyarıları çift yönlü iletişimi destekler. Bir kullanıcı tooan uyarısını yanıt verebilir:

- **Uyarılardan aboneliği:** bir kullanıcı tüm Eylem grupları veya tekil eylem grubu için tüm SMS uyarılardan aboneliğinizi iptal edebilirsiniz.  
- **Tooalerts resubscribe:** tooall SMS uyarıları tüm Eylem grupları veya tekil eylem grup için bir kullanıcı resubscribe.  
- **Yardım isteğinde:** kullanıcı hello SMS hakkında daha fazla bilgi isteyebilir. Yeniden yönlendirilen toothis makale olacaktır

Bu makalede hello SMS uyarıları hello davranışını yer almaktadır ve hello yanıt eylemleri hello kullanıcı hello kullanıcı hello yerel ayar temel alabilir:

## <a name="usacanada-sms-behavior"></a>ABD/Kanada SMS davranışı
### <a name="receiving-an-sms-alert"></a>SMS uyarı alma
Bir uyarı oluşturulduğunda bir eylem grubunun bir parçası yapılandırılmış bir SMS alıcı SMS alır. Merhaba SMS bilgisinden hello yürütecek:
* Bu uyarı gönderildiği hello eylem grubunun kısaad
- Merhaba uyarı başlığı

### <a name="unsubscribing-from-sms-alerts-for-one-action-group"></a>Aboneliğini iptal etmek için bir eylem grubu SMS uyarıları
Bir kullanıcı SMS uyarılar için bir eylem grubu için yanıt veren toohello shortcode 20873 hello sözcüklerle tarafından aboneliğinizi iptal edebilirsiniz: "devre dışı &lt;eylem grubunun kısaad&gt;".

Örn Merhaba kısaad "Azure" ile bir eylem grubu için uyarılardan toounsubscribe isteyen kullanıcı "Azure devre dışı bırak" diyen bir SMS toohello shortcode 20873 göndermek

### <a name="unsubscribing-from-sms-alerts-for-all-action-groups"></a>Tüm Eylem grupları için SMS uyarı aboneliğini
Bir kullanıcının tüm Eylem grupları için tüm SMS uyarılardan yanıt veren toohello shortcode anahtar sözcükler aşağıdaki hello biri tarafından 20873 herhangi biriyle aboneliğinizi iptal edebilirsiniz:
* DURDUR

Örn Tüm eylem gruplarında, tüm SMS uyarılardan toounsubscribe isteyen kullanıcı "Durdur" diyen bir SMS toohello shortcode 20873 göndermek

>[!NOTE]
>Bir kullanıcı iptal etti SMS uyarır, ancak daha sonra tooa yeni eylem grubu eklenir; Bunlar yeni o eylemi grubu SMS uyarı almak, ancak tüm önceki eylem gruplarından aboneliği kalır.
>
>

### <a name="resubscribing-toosms-alerts-for-one-action-group"></a>Bir eylem grubu için resubscribing tooSMS uyarıları
Bir kullanıcı tarafından yanıt veren toohello shortcode 20873 hello sözcüklerle tooSMS bir eylem grubu için uyarılar için resubscribe: "etkinleştirme &lt;eylem grubunun kısaad&gt;".

Örn Bir eylem grubu hello kısaad "Azure" ile tooresubscribe tooalerts isteyen bir kullanıcı "Azure etkinleştir" diyen bir SMS toohello shortcode 20873 göndermek

### <a name="resubscribing-toosms-alerts-for-all-action-groups"></a>Tüm Eylem grupları için resubscribing tooSMS uyarıları
Bir kullanıcı tooall SMS tüm Eylem grupları için uyarılar için yanıt veren toohello shortcode anahtar sözcükler aşağıdaki hello biri tarafından 20873 herhangi biriyle resubscribe:

* BAŞLAT

Örn Tüm eylem gruplarında, tüm SMS uyarılardan toounsubscribe isteyen kullanıcı "Başlat" diyen bir SMS toohello shortcode 20873 göndermek

### <a name="requesting-help-via-sms"></a>SMS aracılığıyla Yardım isteme
Bir kullanıcı herhangi bir anahtar sözcük aşağıdaki hello ile yanıt veren toohello shortcode 20873 tarafından alınan hello SMS hakkında daha fazla bilgi isteyebilir:
* YARDIM

Bir yanıt toohello kullanıcı ile bir bağlantı toothis makalesi gönderilir.

## <a name="next-steps"></a>Sonraki Adımlar
Alma bir [etkinlik günlüğü uyarıları genel bakış](monitoring-overview-alerts.md) ve nasıl tooget uyarı öğrenin  
Daha fazla bilgi edinmek [SMS hız sınırı](monitoring-alerts-rate-limiting.md)  
Daha fazla bilgi edinmek [Eylem grupları](monitoring-action-groups.md)
