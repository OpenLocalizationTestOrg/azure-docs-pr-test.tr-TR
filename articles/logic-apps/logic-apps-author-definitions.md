---
title: "JSON - Azure Logic Apps aaaDefine iş akışlarıyla | Microsoft Docs"
description: "Nasıl logic apps için JSON içinde toowrite iş akışı tanımları"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 03/29/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 0d69d334ecee9c3e7f8684cfde68ef0e85280358
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-workflow-definitions-for-logic-apps-using-json"></a>JSON kullanarak logic apps için iş akışı tanımları oluşturma

İş akışı tanımları için oluşturabileceğiniz [Azure Logic Apps](logic-apps-what-are-logic-apps.md) basit ve bildirim temelli JSON dili. Henüz yapmadıysanız, ilk gözden [nasıl toocreate ilk mantıksal uygulamanızı mantığı Uygulama Tasarımcısı ile](logic-apps-create-a-logic-app.md). Ayrıca bkz.: Merhaba [tam hello iş akışı tanımlama dili başvurusu](http://aka.ms/logicappsdocs).

## <a name="repeat-steps-over-a-list"></a>Bir liste arasındaki adımları yineleyin

too10, 000 öğeleri vardır ve her öğe için bir eylem gerçekleştirmek, hello kullanma bir dizi aracılığıyla tooiterate [foreach türü](logic-apps-loops-and-scopes.md).

## <a name="handle-failures-if-something-goes-wrong"></a>Bir sorun yaşanırsa hataları işleme

Tooinclude genellikle, istediğiniz bir *düzeltme adım* — yürütür bazı mantığı *ve yalnızca,* biri veya birkaçı çağrılarınızı başarısız. Bu örnek verileri çeşitli yerlerden alır, ancak hello çağrısı başarısız olursa, böylece biz daha sonra bu hata izleyebilirsiniz tooPOST bir ileti yere istiyoruz:  

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {},
  "triggers": {
    "Request": {
      "type": "request",
      "kind": "http"
    }
  },
  "actions": {
    "readData": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      }
    },
    "postToErrorMessageQueue": {
      "type": "ApiConnection",
      "inputs": "...",
      "runAfter": {
        "readData": [
          "Failed"
        ]
      }
    }
  },
  "outputs": {}
}
```

toospecify, `postToErrorMessageQueue` sonra yalnızca çalışan `readData` sahip `Failed`, hello kullan `runAfter` özelliği, örneğin, olası bir değer listesi toospecify böylece `runAfter` olabilir `["Succeeded", "Failed"]`.

Bu örnek şimdi hello hata işlemesi nedeniyle son olarak, biz artık farklı çalıştır hello işaretlemek `Failed`. Çalıştırma hello sahip, bu örnekte bu hata işleme için hello adım eklediğimiz olduğundan `Succeeded` rağmen tek bir adımda `Failed`.

## <a name="execute-two-or-more-steps-in-parallel"></a>İki veya daha fazla adım Paralel yürütme

toorun paralel olarak birden çok eylem hello `runAfter` özelliği çalışma zamanında eşdeğer olmalıdır. 

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {},
  "triggers": {
    "Request": {
      "kind": "http",
      "type": "Request"
    }
  },
  "actions": {
    "readData": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      }
    },
    "branch1": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    },
    "branch2": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    }
  },
  "outputs": {}
}
```

Bu örnekte, her ikisi de `branch1` ve `branch2` toorun sonra ayarlanır `readData`. Sonuç olarak, her iki dalları paralel olarak çalıştırın. Her iki dalları için Hello zaman damgası aynıdır.

![Paralel](media/logic-apps-author-definitions/parallel.png)

## <a name="join-two-parallel-branches"></a>İki paralel dalları katılma

Toorun öğeleri toohello ekleyerek paralel olarak ayarlanan iki eylem katılabilirsiniz `runAfter` hello önceki örnekte olduğu gibi özelliği.

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-04-01-preview/workflowdefinition.json#",
  "actions": {
    "readData": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {}
    },
    "branch1": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    },
    "branch2": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    },
    "join": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "branch1": [
          "Succeeded"
        ],
        "branch2": [
          "Succeeded"
        ]
      }
    }
  },
  "parameters": {},
  "triggers": {
    "Request": {
      "type": "Request",
      "kind": "Http",
      "inputs": {
        "schema": {}
      }
    }
  },
  "contentVersion": "1.0.0.0",
  "outputs": {}
}
```

![Paralel](media/logic-apps-author-definitions/join.png)

## <a name="map-list-items-tooa-different-configuration"></a>Liste öğeleri tooa farklı yapılandırma eşleme

Ardından, bir özelliğin hello değere göre tooget farklı içerik istiyoruz diyelim. Parametre olarak değerleri toodestinations haritasını oluşturabilir:  

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "specialCategories": {
      "defaultValue": [
        "science",
        "google",
        "microsoft",
        "robots",
        "NSA"
      ],
      "type": "Array"
    },
    "destinationMap": {
      "defaultValue": {
        "science": "http://www.nasa.gov",
        "microsoft": "https://www.microsoft.com/en-us/default.aspx",
        "google": "https://www.google.com",
        "robots": "https://en.wikipedia.org/wiki/Robot",
        "NSA": "https://www.nsa.gov/"
      },
      "type": "Object"
    }
  },
  "triggers": {
    "Request": {
      "type": "Request",
      "kind": "http"
    }
  },
  "actions": {
    "getArticles": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "https://ajax.googleapis.com/ajax/services/feed/load?v=1.0&q=http://feeds.wired.com/wired/index"
      }
    },
    "forEachArticle": {
      "type": "foreach",
      "foreach": "@body('getArticles').responseData.feed.entries",
      "actions": {
        "ifGreater": {
          "type": "if",
          "expression": "@greater(length(intersection(item().categories, parameters('specialCategories'))), 0)",
          "actions": {
            "getSpecialPage": {
              "type": "Http",
              "inputs": {
                "method": "GET",
                "uri": "@parameters('destinationMap')[first(intersection(item().categories, parameters('specialCategories')))]"
              }
            }
          }
        }
      },
      "runAfter": {
        "getArticles": [
          "Succeeded"
        ]
      }
    }
  }
}
```

Bu durumda, biz ilk makalelerin listesini alın. Parametre olarak tanımlandı hello kategoriye göre hello ikinci adım harita toolook hello URL yukarı hello içeriği almak için kullanır.

Burada bazı kez toonote: 

*   Merhaba [ `intersection()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#intersection) işlevi hello kategori tanımlanan kategorilere bilinen hello birini eşleşip eşleşmediğini denetler.

*   Biz hello kategori aldıktan sonra biz hello öğesi köşeli ayraç kullanarak hello eşlemesinden çekebilir:`parameters[...]`

## <a name="process-strings"></a>İşlem dizeleri

Çeşitli işlevler toomanipulate dizelerini kullanabilirsiniz. Örneğin, biz toopass tooa sistem istiyoruz, ancak biz karakter kodlama için uygun işleme hakkında emin olmayan bir dize olduğunu varsayalım. Bir seçenektir toobase64 bu dizesini kodlayın. Ancak, bir URL'de kaçış tooavoid tooreplace birkaç karakter çağıracaksınız. 

Hello ilk beş karakter olmayan kullanıldığı için de bir dizenin hello sipariş adını istiyoruz.

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "order": {
      "defaultValue": {
        "quantity": 10,
        "id": "myorder1",
        "orderer": "NAME=Contoso"
      },
      "type": "Object"
    }
  },
  "triggers": {
    "request": {
      "type": "request",
      "kind": "http"
    }
  },
  "actions": {
    "order": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://www.example.com/?id=@{replace(replace(base64(substring(parameters('order').orderer,5,sub(length(parameters('order').orderer), 5) )),'+','-') ,'/' ,'_' )}"
      }
    }
  },
  "outputs": {}
}
```

Toooutside içinde çalışma:

1. Merhaba alma [ `length()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#length) hello sipariş ın eden adı için böylece biz geri alma hello toplam karakter sayısı.

2. Daha kısa bir dize istiyoruz çünkü 5 çıkarın.

3. Aslında, hello ele [ `substring()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#substring). Biz dizininde Başlat `5` ve hello dize geri kalanı hello gidin.

4. Bu alt dizeyi tooa Dönüştür [ `base64()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#base64) dize.

5. [`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace)Tüm hello `+` ile karakterleri `-` karakter.

6. [`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace)Tüm hello `/` ile karakterleri `_` karakter.

## <a name="work-with-date-times"></a>Tarih süreleri ile çalışma

Özellikle doğal olarak desteklemeyen bir veri kaynağından alınan toopull veriler çalışırken tarih kez yararlı olabilir *Tetikleyicileri*. Tarih Saatler ne kadar çeşitli adımları kaplayan bulmak için de kullanabilirsiniz.

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "order": {
      "defaultValue": {
        "quantity": 10,
        "id": "myorder1"
      },
      "type": "Object"
    }
  },
  "triggers": {
    "Request": {
      "type": "request",
      "kind": "http"
    }
  },
  "actions": {
    "order": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://www.example.com/?id=@{parameters('order').id}"
      }
    },
    "ifTimingWarning": {
      "type": "If",
      "expression": "@less(actions('order').startTime,addseconds(utcNow(),-1))",
      "actions": {
        "timingWarning": {
          "type": "Http",
          "inputs": {
            "method": "GET",
            "uri": "http://www.example.com/?recordLongOrderTime=@{parameters('order').id}&currentTime=@{utcNow('r')}"
          }
        }
      },
      "runAfter": {
        "order": [
          "Succeeded"
        ]
      }
    }
  },
  "outputs": {}
}
```

Bu örnekte, biz hello ayıklamak `startTime` hello önceki adımdaki. Biz hello geçerli saati almak ve bir ikinci çıkarma sonra:

[`addseconds(..., -1)`](https://msdn.microsoft.com/library/azure/mt643789.aspx#addseconds) 

İsterseniz zaman, diğer birimleri kullanabilirsiniz `minutes` veya `hours`. Son olarak, biz bu iki değer karşılaştırabilirsiniz. Hello ilk değer hello ikinci değer sonra bir saniyeden küçükse hello sipariş ilk yerleştirilen geçen.

tooformat tarihleri dize biçimlendiricileri kullanırız. Örneğin, tooget hello RFC1123, kullandığımız [ `utcnow('r')` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow). Tarih biçimlendirme hakkında toolearn bkz [iş akışı tanımlama dili](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).

## <a name="deployment-parameters-for-different-environments"></a>Farklı ortamlar için dağıtım parametreleri

Genellikle, bir geliştirme ortamı, hazırlık ortamı ve bir üretim ortamında dağıtım yaşam döngüleri vardır. Örneğin, kullanabilirsiniz hello tüm ortamlarda aynı tanımın ancak farklı veritabanlarını kullanır. Benzer şekilde, toouse isteyebilirsiniz farklı bölgelere yüksek kullanılabilirlik için aynı tanımın hello ancak her mantıksal uygulama örneğini tootalk toothat bölgenin veritabanı istiyor.
Bu senaryo parametrelerinin alma farklı *çalışma zamanı* Burada bunun yerine, kullanmanız gereken hello `trigger()` hello önceki örnekte olduğu gibi işlev.

Bu örnek gibi temel bir tanımıyla başlatabilirsiniz:

```
{
    "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "uri": {
            "type": "string"
        }
    },
    "triggers": {
        "request": {
          "type": "request",
          "kind": "http"
        }
    },
    "actions": {
        "readData": {
            "type": "Http",
            "inputs": {
                "method": "GET",
                "uri": "@parameters('uri')"
            }
        }
    },
    "outputs": {}
}
```

Merhaba gerçek içinde `PUT` hello parametre sağlayabilir hello logic apps için istek `uri`. Varsayılan değeri artık mevcut olmadığından, bu parametre hello mantığı uygulama yükü gerektirir:

```
{
    "properties": {},
        "definition": {
          // Use hello definition from above here
        },
        "parameters": {
            "connection": {
                "value": "https://my.connection.that.is.per.enviornment"
            }
        }
    },
    "location": "westus"
}
``` 

Her bir ortamda hello için farklı bir değer sağlayabilir `connection` parametresi. 

Tüm oluşturmak ve mantıksal uygulamaları yönetmek için seçenekleri hello hello bakın [REST API belgeleri](https://msdn.microsoft.com/library/azure/mt643787.aspx). 
