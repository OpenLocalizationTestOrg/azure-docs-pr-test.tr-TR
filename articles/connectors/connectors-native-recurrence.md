---
title: logic apps aaaAdd hello yinelenme tetikleyici | Microsoft Docs
description: "Merhaba yinelenme tetikleyici, genel bakış ve nasıl toouse bir Azure mantıksal uygulama ile."
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 51dd4f22-7dc5-41af-a0a9-e7148378cd50
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: e7c625c382a88a1e7cdfff4ddc0caf55727232bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-recurrence-trigger"></a>Merhaba yinelenme tetikleyici ile çalışmaya başlama
Merhaba yinelenme tetikleyicisini kullanarak hello bulutta güçlü iş akışları oluşturabilirsiniz.

Örneğin, şunları yapabilirsiniz:

* İş akışı toorun SQL saklı yordamı her gün zamanlayın.
* Merhaba belirli bir hashtag hakkında geçen hafta içinde tüm tweet'leri özetini e-posta.

bir mantıksal uygulama Hello yinelenme tetikleyici kullanmaya tooget bkz [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-a-recurrence-trigger"></a>Bir yineleme tetikleyici kullanın
Bir tetikleyici bir mantıksal uygulama tanımlı kullanılan toostart hello iş akışı olabilecek bir olaydır. [Tetikleyiciler hakkında daha fazla bilgi](connectors-overview.md).

Nasıl bir yinelenme yukarı tooset tetikleyen bir mantıksal uygulama bir örnek sırası şöyledir:

1. Merhaba eklemek **yineleme** tetikleyici hello bir mantıksal uygulama ilk adımı olarak.
2. Merhaba parametrelerinde hello yineleme aralığını doldurun.

Merhaba mantıksal uygulama artık çalışma sonrasında her zaman aralığı başlatır.

![HTTP tetikleyicisi](./media/connectors-native-recurrence/using-trigger.png)

## <a name="trigger-details"></a>Tetikleyici ayrıntıları
Merhaba yinelenme tetikleyici hello aşağıdaki yapılandırabileceğiniz özelliklere sahiptir.

Bu mantıksal uygulama belirtilen bir süre sonra ateşlenir.
A * gerekli bir alan olduğu anlamına gelir.

| Görünen ad | Özellik adı | Açıklama |
| --- | --- | --- |
| Sıklık * |frequency |zaman birimi Hello: `Second`, `Minute`, `Hour`, `Day`, veya `Year`. |
| Aralık * |interval |Merhaba yinelemesi sıklığı verilen hello Hello aralığı. |
| Saat Dilimi |saat dilimi |Bir başlangıç saati UTC uzaklığı sağlanırsa, bu saat dilimi kullanılır. |
| Başlangıç zamanı |startTime |Merhaba başlangıç saati [ISO 8601 biçim](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations). |

<br>

## <a name="next-steps"></a>Sonraki adımlar
Şimdi, hello platform deneyin ve [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md). Keşfedebilirsiniz bakarak logic apps içinde kullanılabilir diğer bağlayıcıları hello bizim [API'leri listesi](apis-list.md).

