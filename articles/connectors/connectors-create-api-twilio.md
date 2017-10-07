---
title: "aaaAdd hello Twilio bağlayıcı Azure Logic apps içinde | Microsoft Docs"
description: "REST API parametrelerle hello Twilio bağlayıcı genel bakış"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 43116187-4a2f-42e5-9852-a0d62f08c5fc
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 09/19/2016
ms.author: mandia; ladocs
ms.openlocfilehash: b2b487f34bc76bee24b4237a71ee767d0d22ff7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-twilio-connector"></a>Merhaba Twilio Bağlayıcısı ile çalışmaya başlama
TooTwilio toosend bağlanmak ve genel IP SMS ve MMS iletileri alabilirsiniz. Twilio ile şunları yapabilirsiniz:

* İş akışınız hello verileri Twilio Al esas oluşturun. 
* Bir ileti, liste iletiler ve daha fazlasını alma eylemlerini kullanın. Bu eylemler bir yanıt ve hello çıkış diğer eylemler için kullanılabilir yapın. Örneğin, yeni bir Twilio ileti aldığınızda, bu ileti almak ve bir hizmet veri yolu iş akışı kullanın. 

Bir mantıksal uygulama oluşturarak başlama; bkz: [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="create-a-connection-tootwilio"></a>Bir bağlantı tooTwilio oluşturma
Bu bağlayıcı tooyour logic apps eklediğinizde, Twilio değerleri aşağıdaki hello girin:

| Özellik | Gerekli | Açıklama |
| --- | --- | --- |
| Hesap Kimliği |Evet |Twilio hesabı Kimliğinizi girin |
| Erişim belirteci |Evet |Twilio erişim belirtecinizi girin |

> [!INCLUDE [Steps toocreate a connection tooTwilio](../../includes/connectors-create-api-twilio.md)]
> 
> 

Twilio erişim belirteci sahip değilseniz, bkz: [kullanıcı kimliği ve erişim belirteçleri](https://www.twilio.com/docs/api/chat/guides/identity).

## <a name="connector-specific-details"></a>Bağlayıcı özgü ayrıntıları

Tüm tetikleyiciler ve Eylemler hello swagger içinde tanımlanan görüntüleyebilir ve ayrıca hello herhangi bir sınır bkz. [Bağlayıcısı ayrıntıları](/connectors/twilio/).

## <a name="more-connectors"></a>Daha fazla bağlayıcılar
Toohello dönün [API'leri listesi](apis-list.md).
