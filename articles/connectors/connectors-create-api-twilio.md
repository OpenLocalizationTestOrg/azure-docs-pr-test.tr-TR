---
title: "Twilio bağlayıcı Azure Logic apps içinde ekleme | Microsoft Docs"
description: "REST API parametreleri Twilio bağlayıcısıyla genel bakış"
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
ms.openlocfilehash: 50361a3342a0d14ae02b2cb478bbb0f74b61bba0
ms.sourcegitcommit: be9a42d7b321304d9a33786ed8e2b9b972a5977e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/19/2018
---
# <a name="get-started-with-the-twilio-connector"></a>Twilio Bağlayıcısı ile çalışmaya başlama
Genel IP SMS ve MMS ileti gönderme ve alma için Twilio için bağlayın. Twilio ile şunları yapabilirsiniz:

* İş akışınız Twilio alma verileri temel alan oluşturun. 
* Bir ileti, liste iletiler ve daha fazlasını alma eylemlerini kullanın. Bu eylemler bir yanıt ve çıkış diğer eylemler için kullanılabilir yapın. Örneğin, yeni bir Twilio ileti aldığınızda, bu ileti almak ve bir hizmet veri yolu iş akışı kullanın. 

Bir mantıksal uygulama oluşturarak başlama; bkz: [mantıksal uygulama oluşturma](../logic-apps/quickstart-create-first-logic-app-workflow.md).

## <a name="create-a-connection-to-twilio"></a>Twilio bağlantı oluşturun.
Bu bağlayıcı mantıksal uygulamalarınızı eklediğinizde, aşağıdaki Twilio değerleri girin:

| Özellik | Gerekli | Açıklama |
| --- | --- | --- |
| Hesap Kimliği |Evet |Twilio hesabı Kimliğinizi girin |
| Erişim Belirteci |Evet |Twilio erişim belirtecinizi girin |

> [!INCLUDE [Steps to create a connection to Twilio](../../includes/connectors-create-api-twilio.md)]
> 
> 

Twilio erişim belirteci sahip değilseniz, bkz: [kullanıcı kimliği ve erişim belirteçleri](https://www.twilio.com/docs/api/chat/guides/identity).

## <a name="connector-specific-details"></a>Bağlayıcı özgü ayrıntıları

Tüm tetikleyiciler ve Eylemler swagger tanımlanan görüntüleyebilir ve ayrıca herhangi bir sınır bkz [Bağlayıcısı ayrıntıları](/connectors/twilio/).

## <a name="more-connectors"></a>Daha fazla bağlayıcılar
Geri dönerek [API'leri listesi](apis-list.md).