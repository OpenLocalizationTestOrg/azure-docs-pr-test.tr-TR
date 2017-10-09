---
title: "aaaCreate döngüler ve kapsamları ya da iş akışları - Azure Logic Apps verilerde debatch | Microsoft Docs"
description: "Veriler, kapsamları, Grup eylemlere aracılığıyla döngüler tooiterate oluşturun veya daha fazla iş akışı Azure Logic Apps içinde veri toostart debatch."
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 75b52eeb-23a7-47dd-a42f-1351c6dfebdc
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/29/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: e612ec2e83541f028916a07bf12c44e7b1f57ad1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-loops-scopes-and-debatching"></a>Logic Apps Döngüleri, Kapsamları ve Ayırma
  
Logic Apps diziler, koleksiyonları, toplu işleri ve bir iş akışındaki döngüler yolları toowork sayısını sağlar.
  
## <a name="foreach-loop-and-arrays"></a>ForEach döngüsü ve diziler
  
Logic Apps bir veri kümesi üzerinde tooloop sağlar ve her öğe için bir eylemi gerçekleştirir.  Bu hello mümkündür `foreach` eylem.  Merhaba Tasarımcısı'nda tooadd belirtebilirsiniz bir her döngü için.  Merhaba dizi üzerinden tooiterate istediğiniz seçtikten sonra Eylemler eklemeye başlayabilirsiniz.  Şu anda sınırlı tooonly bir eylem foreach döngüsü başına olan, ancak bu kısıtlama hafta gelen hello kaldırılmış.  Bir kez hello döngü içinde her hello dizi değerinde gerekeni toospecify başlayabilirsiniz.

Kod görünümünü kullanıyorsanız, belirleyebileceğiniz bir aşağıdaki gibi her bir döngü için.  Bu örneği olan bir 'microsoft.com' içeren her bir e-posta adresi için bir e-posta gönderir her bir döngü için:

``` json
{
    "email_filter": {
        "type": "query",
        "inputs": {
            "from": "@triggerBody()['emails']",
            "where": "@contains(item()['email'], 'microsoft.com')"
        }
    },
    "forEach_email": {
        "type": "foreach",
        "foreach": "@body('email_filter')",
        "actions": {
            "send_email": {
                "type": "ApiConnection",
                "inputs": {
                "body": {
                    "to": "@item()",
                    "from": "me@contoso.com",
                    "message": "Hello, thank you for ordering"
                },
                "host": {
                    "connection": {
                        "id": "@parameters('$connections')['office365']['connection']['id']"
                    }
                },
                }
            }
        },
        "runAfter":{
            "email_filter": [ "Succeeded" ]
        }
    }
}
```
  
  A `foreach` eylem too5, 000 satırları yukarı diziler üzerinden yineleme.  Her yineleme paralel olarak varsayılan olarak yürütülür.  

### <a name="sequential-foreach-loops"></a>Sıralı ForEach döngüsü

foreach döngüsü tooexecute ardışık olarak hello tooenable `Sequential` işlemi seçeneği eklenir.

``` json
"forEach_email": {
        "type": "foreach",
        "foreach": "@body('email_filter')",
        "operationOptions": "Sequential",
        "..."
}
```
  
## <a name="until-loop"></a>Döngü kadar
  
  Bir koşul yerine getirilene kadar bir eylem veya dizi eylem gerçekleştirebilir.  Aradığınız hello yanıt elde edene kadar hello Bunun en yaygın senaryo bir uç nokta çağırıyor.  Merhaba Tasarımcısı'nda tooadd belirtebilirsiniz bir döngü kadar.  Eylemler hello döngü içinde ekledikten sonra hello çıkış koşulu yanı döngü sınırları hello.  Döngü döngüleri arasında 1 dakikalık bir gecikmeyle yoktur.
  
  Kod görünümünü kullanıyorsanız, belirleyebileceğiniz bir döngü ister aşağıda kadar.  Bu hello değeri 'Tamamlandı' hello yanıt gövdesi olana kadar bir HTTP uç noktası çağrılmadan bir örnektir.  Ne zaman tamamlanır ya da 
  
  * HTTP yanıtı 'Tamamlandı' durumuna sahip
  * 1 saat boyunca çalıştı
  * 100 kez döngüye
  
  ``` json
  {
      "until_successful":{
        "type": "until",
        "expression": "@equals(actions('http')['status'], 'Completed')",
        "limit": {
            "count": 100,
            "timeout": "PT1H"
        },
        "actions": {
            "create_resource": {
                "type": "http",
                "inputs": {
                    "url": "http://provisionRseource.com",
                    "body": {
                        "resourceId": "@triggerBody()"
                    }
                }
            }
        }
      }
  }
  ```
  
## <a name="spliton-and-debatching"></a>SplitOn ve debatching

Bazen bir tetikleyici bir dizi toodebatch istediğiniz ve bir iş akışı öğesi başına başlatmak öğeleri alabilirsiniz.  Bu hello gerçekleştirilebilir `spliton` komutu.  Varsayılan olarak, tetikleyici swagger bir dizi bir yükü belirtiyorsa, bir `spliton` eklenir ve bir çalışma öğesi başına başlatın.  SplitOn yalnızca tooa tetikleyici eklenebilir.  Bu el ile yapılandırılabildiğinden veya tanımı kod görünümünde geçersiz kılındı.  Şu anda SplitOn too5, 000 öğeleri yukarı diziler debatch.  Sahip olamaz bir `spliton` ve ayrıca hello zaman uyumlu yanıt desenini uygular.  Adında herhangi bir iş akışının sahip bir `response` eylem ayrıca çok`spliton` zaman uyumsuz olarak çalışacak ve hemen gönder `202 Accepted` yanıt.  

SplitOn kod görünümünde aşağıdaki örneğine hello belirtilebilir.  Bu öğeleri dizisini alır ve her satırda debatches.

```
{
    "myDebatchTrigger": {
        "type": "Http",
        "inputs": {
            "url": "http://getNewCustomers",
        },
        "recurrence": {
            "frequencey": "Second",
            "interval": 15
        },
        "spliton": "@triggerBody()['rows']"
    }
}
```

## <a name="scopes"></a>Kapsamları

Bu, olası toogroup birlikte bir kapsamı kullanarak eylemleri bir dizi olur.  Özel durum işleme uygulamak için özellikle yararlıdır.  Merhaba Tasarımcısı'nda yeni bir kapsam ekleyin ve onu içinde herhangi bir eylem eklemeye başlamak.  Merhaba aşağıdaki gibi kod görünümünde kapsamları tanımlayabilirsiniz:


```
{
    "myScope": {
        "type": "scope",
        "actions": {
            "call_bing": {
                "type": "http",
                "inputs": {
                    "url": "http://www.bing.com"
                }
            }
        }
    }
}
```