---
title: "B2B için şemalar izleme aaaCustom izleme - Azure Logic Apps | Microsoft Docs"
description: "Özel İzleme şemaları toomonitor B2B iletileri Azure tümleştirme hesabınızda işlemlerdeki oluşturun."
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 433ae852-a833-44d3-a3c3-14cca33403a2
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8cf26a43d89f0414a2a8c5ef59d804235afeb5d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-tracking-toomonitor-your-complete-workflow-end-to-end"></a>İş akışını tam, uçtan uca izleme toomonitor etkinleştir
İzleme AS2 veya X12 gibi iş iş akışınızı farklı kısımlarını iletileri için etkinleştirebileceğiniz olduğunu izleme yerleşik yoktur. Bir mantıksal uygulama, BizTalk Server, SQL Server veya başka bir katmanında içeren iş akışları oluşturduğunuzda, hello başına toohello sonundan akışınızı olayları kaydeder özel izleme işlevini etkinleştirebilirsiniz. 

Bu konu, mantıksal uygulamanızı dışında hello katmanlarında kullanabilirsiniz özel kod sağlar. 

## <a name="custom-tracking-schema"></a>Özel İzleme şeması
````java

        {
            "sourceType": "",
            "source": {

            "workflow": {
                "systemId": ""
            },
            "runInstance": {
                "runId": ""
            },
            "operation": {
                "operationName": "",
                "repeatItemScopeName": "",
                "repeatItemIndex": "",
                "trackingId": "",
                "correlationId": "",
                "clientRequestId": ""
                }
            },
            "events": [
            {
                "eventLevel": "",
                "eventTime": "",
                "recordType": "",
                "record": {                
                }
            }
         ]
      }

````

| Özellik | Tür | Açıklama |
| --- | --- | --- |
| Kaynak türü |   | Çalıştırma hello kaynak türü. İzin verilen değerler **Microsoft.Logic/workflows** ve **özel**. (Zorunlu) |
| Kaynak |   | Merhaba kaynak türü ise **Microsoft.Logic/workflows**, hello kaynak bilgileri, bu şemayı toofollow gerekiyor. Merhaba kaynak türü ise **özel**, hello schema bir JToken'dır. (Zorunlu) |
| SistemKimliği | Dize | Mantıksal uygulama sistem kimliği (Zorunlu) |
| çalıştırma kodu | Dize | Mantıksal uygulama kimliği çalıştırın (Zorunlu) |
| operationName | Dize | Merhaba işlemi (örneğin, eylem veya tetikleyici) adı. (Zorunlu) |
| repeatItemScopeName | Dize | Öğe adı Hello eylem içinde ise yineleyin bir `foreach` / `until` döngü. (Zorunlu) |
| repeatItemIndex | Tamsayı | Merhaba eylem içinde olup olmadığını bir `foreach` / `until` döngü. Merhaba yinelenen öğe dizini belirtir. (Zorunlu) |
| İzleme kodu | Dize | İzleme kimliği, toocorrelate Merhaba iletileri. (İsteğe bağlı) |
| correlationId | Dize | Bağıntı kimliği, toocorrelate Merhaba iletileri. (İsteğe bağlı) |
| ClientRequestId | Dize | İstemci toocorrelate iletileri doldurabilirsiniz. (İsteğe bağlı) |
| eventLevel |   | Merhaba olay düzeyi. (Zorunlu) |
| EventTime |   | YYYY-AA-DDTHH:MM:SS.00000Z UTC biçiminde hello olay zamanı. (Zorunlu) |
| RecordType |   | Merhaba İzle kayıt türü. Değer izin verilen **özel**. (Zorunlu) |
| Kayıt |   | Özel bir kayıt türü. İzin verilen JToken biçimindedir. (Zorunlu) |

## <a name="b2b-protocol-tracking-schemas"></a>B2B Protokolü izleme şemaları
B2B Protokolü şemaları izleme hakkında daha fazla bilgi için bkz:
* [AS2 izleme şemaları](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)   
* [X12 izleme şemaları](logic-apps-track-integration-account-x12-tracking-schema.md)

## <a name="next-steps"></a>Sonraki adımlar
* Daha fazla bilgi edinmek [B2B iletileri izleme](logic-apps-monitor-b2b-message.md).   
* Hakkında bilgi edinin [hello Operations Management Suite portalına B2B iletilerinde izleme](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).
* Merhaba hakkında daha fazla bilgi [Kurumsal tümleştirme paketi](../logic-apps/logic-apps-enterprise-integration-overview.md).
