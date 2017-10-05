---
title: "Logic apps içinde yineleme tetikleyici ekleme | Microsoft Docs"
description: "Yineleme tetikleyici ve bir Azure mantıksal uygulama ile kullanmak nasıl genel bakış."
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
ms.openlocfilehash: fe558958c316c8dba42163e277ae01451f712e5a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-recurrence-trigger"></a>Yineleme tetikleyici ile çalışmaya başlama
Yineleme tetikleyici kullanarak bulutta güçlü iş akışları oluşturabilirsiniz.

Örneğin, şunları yapabilirsiniz:

* Bir iş akışı SQL saklı yordamı her gün çalışacak şekilde zamanlayın.
* Belirli bir hashtag hakkında geçen hafta içinde tüm tweet'leri özetini e-posta.

Yineleme tetikleyici bir mantıksal uygulama kullanmaya başlamak için bkz: [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-a-recurrence-trigger"></a>Bir yineleme tetikleyici kullanın
Bir tetikleyici bir mantıksal uygulama tanımlı iş akışını başlatmak için kullanılan bir olaydır. [Tetikleyiciler hakkında daha fazla bilgi](connectors-overview.md).

Bir mantıksal uygulama yinelenme tetikleyici ayarlama konusunda bir örnek sırası şöyledir:

1. Ekleme **yineleme** tetikleyici bir mantıksal uygulama ilk adımı olarak.
2. Parametrelerde yineleme aralığını doldurun.

Mantıksal uygulama artık çalışma sonrasında her zaman aralığı başlatır.

![HTTP tetikleyicisi](./media/connectors-native-recurrence/using-trigger.png)

## <a name="trigger-details"></a>Tetikleyici ayrıntıları
Yineleme tetikleyici yapılandırabilirsiniz aşağıdaki özelliklere sahip.

Bu mantıksal uygulama belirtilen bir süre sonra ateşlenir.
A * gerekli bir alan olduğu anlamına gelir.

| Görünen ad | Özellik adı | Açıklama |
| --- | --- | --- |
| Sıklık * |Sıklık |Zaman birimi: `Second`, `Minute`, `Hour`, `Day`, veya `Year`. |
| Aralık * |aralığı |Verilen sıklığı aralığını yineleme için. |
| Saat Dilimi |saat dilimi |Bir başlangıç saati UTC uzaklığı sağlanırsa, bu saat dilimi kullanılır. |
| Başlangıç zamanı |startTime |Başlangıç saati [ISO 8601 biçim](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations). |

<br>

## <a name="next-steps"></a>Sonraki adımlar
Şimdi, platform deneyin ve [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md). Logic apps diğer kullanılabilir bağlayıcılar bakarak keşfedebilirsiniz bizim [API'leri listesi](apis-list.md).

