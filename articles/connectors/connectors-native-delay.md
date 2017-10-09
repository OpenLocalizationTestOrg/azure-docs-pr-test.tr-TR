---
title: logic apps gecikmeden aaaAdd | Microsoft Docs
description: "Merhaba genel bakış gecikmesi ve gecikme-Eylemler kadar ve nasıl toouse bunları Azure mantıksal uygulama ile."
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 915f48bf-3bd8-4656-be73-91a941d0afcd
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: e5bc9d639adbddc01ee0f6a4c68716f586d4344a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-delay-and-delay-until-actions"></a>Merhaba ile çalışmaya başlama gecikmesi ve gecikme-Eylemler kadar
Merhaba gecikme kullanarak ve "gecikme-kadar" Eylemler, iş akışı senaryoları tamamlayabilirsiniz.

Örneğin, şunları yapabilirsiniz:

* Haftanın günü toosend durumu güncelleştirilene kadar e-posta bekleyin.
* Bir HTTP çağrısıyla kadar gecikme hello iş akışı hello sonuç alma ve sürdürme önce zaman toofinish sahiptir.

bir mantıksal uygulama Hello gecikme eylem kullanmaya tooget bkz [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-hello-delay-actions"></a>Merhaba gecikme eylemlerini kullanın
Bir eylem, bir mantıksal uygulama tanımlı hello iş akışı tarafından gerçekleştirilen bir işlemdir. [Eylemler hakkında daha fazla bilgi](connectors-overview.md).

Nasıl toouse bir gecikme adım bir mantıksal uygulama bir örnek sırası şöyledir:

1. Bir tetikleyici ekledikten sonra tıklatın **yeni adım** tooadd bir eylem.
2. Arama **gecikme** toobring hello gecikme Eylemler ayarlama. Bu örnekte, biz seçecektir **gecikme**.
   
    ![Gecikme Eylemler](./media/connectors-native-delay/using-action-1.png)
3. Merhaba eylem özellikleri tooconfigure hello gecikme tamamlayın.
   
    ![Gecikme yapılandırma](./media/connectors-native-delay/using-action-2.png)
4. Tıklatın **kaydetmek** toopublish ve hello mantıksal uygulama etkinleştirin.

## <a name="action-details"></a>Eylem ayrıntıları
Merhaba yinelenme tetikleyici hello aşağıdaki yapılandırılabilir özelliklere sahiptir.

### <a name="delay-action"></a>Gecikme eylemi
Bu eylem gecikmeler hello belirli bir zaman aralığı için çalıştırın.
A * gerekli bir alan olduğu anlamına gelir.

| Görünen ad | Özellik adı | Açıklama |
| --- | --- | --- |
| Sayısı * |Sayısı |zaman birimleri toodelay Hello sayısı |
| Birim * |Birim |zaman birimi Hello: `Second`, `Minute`, `Hour`, veya`Day` |

<br>

### <a name="delay-until-action"></a>Gecikme-eylem kadar
Bu eylem, belirtilen bir tarih/saat kadar çalıştırmak hello geciktirir.
A * gerekli bir alan olduğu anlamına gelir.

| Görünen ad | Özellik adı | Açıklama |
| --- | --- | --- |
| Yıl * |timestamp |(GMT) kadar Hello yıl toodelay |
| Ay * |timestamp |(GMT) kadar Hello ay toodelay |
| Gün * |timestamp |(GMT) kadar Hello gün toodelay |

<br>

## <a name="next-steps"></a>Sonraki adımlar
Şimdi, hello platform deneyin ve [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md). Keşfedebilirsiniz bakarak logic apps içinde kullanılabilir diğer bağlayıcıları hello bizim [API'leri listesi](apis-list.md).

