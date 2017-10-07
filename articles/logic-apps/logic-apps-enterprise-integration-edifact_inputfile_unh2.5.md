---
title: "aaaLogic uygulamaları EDIFACT kod çözme B2B gidermek UNH2.5 - Azure Logic Apps | Microsoft Docs"
description: "EDIFACT kod çözme Azure Logic Apps B2B UNH2.5 çözmek"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 6d85242d0f828fa52cdc9689938f3ba1e51b1183
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toohandle-edifact-documents-having-unh25-segment"></a>Nasıl toohandle EDIFACT UNH2.5 sahip belgeleri kesimi
UNH2.5 hello EDIFACT belgede mevcut olduğunda, şema arama için kullanılıyor. 

Örnek: Merhaba UNH alandır **EAN008** hello EDIFACT iletisi  
UNH + SSDD1 + SİPARİŞLERİ: D: 03B: KALDIRIN:**EAN008**'  

Adımları toofollow toohandle hello iletisi 
1. Merhaba Şemayı Güncelleştir
2. Merhaba sözleşmesi ayarlarını kontrol edin  

## <a name="update-hello-schema"></a>Merhaba Şemayı Güncelleştir
tooprocess selamlama iletisine toodeploy hello UNH2.5 kök düğümü adı şemasıyla gerekir.  Merhaba şema kök adı verilen bir örnek için olacaktır **EFACT_D03B_ORDERS_EAN008**  

Farklı bir UNH2.5 segment ile her D03B_ORDERS için tek bir şema toodeploy gerekir.  

## <a name="add-schema-toohello-edifact-agreement"></a>Şema toohello EDIFACT sözleşmesi ekleme
### <a name="edifact-decode"></a>EDIFACT kod çözme
tooDecode gelen ileti Merhaba, hello şema yapılandırma hello EDIFACT sözleşmesi alma ayarları
1. Merhaba şema toohello tümleştirme hesabı Ekle    
2. Merhaba şema yapılandırma hello EDIFACT sözleşmesi ayarları alırsınız. 
3. EDIFACT sözleşmesi tıklatıp **JSON olarak Düzenle**.  Merhaba alma sözleşmesinde UNH2.5 değeri eklemek **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png)

### <a name="edifact-encode"></a>EDIFACT kodlama
tooEncode gelen ileti Merhaba, hello şema hello EDIFACT sözleşmesi gönderme ayarlarını yapılandırın
1. Merhaba şema toohello tümleştirme hesabı Ekle    
2. Merhaba şema hello EDIFACT sözleşmesi gönderme ayarlarını yapılandırın. 
3. EDIFACT sözleşmesi tıklatıp **JSON olarak Düzenle**.  Merhaba Gönderme Sözleşmesi UNH2.5 değeri eklemek **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png)

## <a name="next-steps"></a>Sonraki Adımlar
* [Tümleştirme hesap anlaşmaları hakkında daha fazla bilgi](../logic-apps/logic-apps-enterprise-integration-agreements.md "Kurumsal tümleştirme anlaşmaları hakkında bilgi edinin")  