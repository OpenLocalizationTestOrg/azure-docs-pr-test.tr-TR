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
# <a name="create-workflow-definitions-for-logic-apps-using-json"></a><span data-ttu-id="5c677-103">JSON kullanarak logic apps için iş akışı tanımları oluşturma</span><span class="sxs-lookup"><span data-stu-id="5c677-103">Create workflow definitions for logic apps using JSON</span></span>

<span data-ttu-id="5c677-104">İş akışı tanımları için oluşturabileceğiniz [Azure Logic Apps](logic-apps-what-are-logic-apps.md) basit ve bildirim temelli JSON dili.</span><span class="sxs-lookup"><span data-stu-id="5c677-104">You can create workflow definitions for [Azure Logic Apps](logic-apps-what-are-logic-apps.md) with simple, declarative JSON language.</span></span> <span data-ttu-id="5c677-105">Henüz yapmadıysanız, ilk gözden [nasıl toocreate ilk mantıksal uygulamanızı mantığı Uygulama Tasarımcısı ile](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="5c677-105">If you haven't already, first review [how toocreate your first logic app with Logic App Designer](logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="5c677-106">Ayrıca bkz.: Merhaba [tam hello iş akışı tanımlama dili başvurusu](http://aka.ms/logicappsdocs).</span><span class="sxs-lookup"><span data-stu-id="5c677-106">Also, see hello [full reference for hello Workflow Definition Language](http://aka.ms/logicappsdocs).</span></span>

## <a name="repeat-steps-over-a-list"></a><span data-ttu-id="5c677-107">Bir liste arasındaki adımları yineleyin</span><span class="sxs-lookup"><span data-stu-id="5c677-107">Repeat steps over a list</span></span>

<span data-ttu-id="5c677-108">too10, 000 öğeleri vardır ve her öğe için bir eylem gerçekleştirmek, hello kullanma bir dizi aracılığıyla tooiterate [foreach türü](logic-apps-loops-and-scopes.md).</span><span class="sxs-lookup"><span data-stu-id="5c677-108">tooiterate through an array that has up too10,000 items and perform an action for each item, use hello [foreach type](logic-apps-loops-and-scopes.md).</span></span>

## <a name="handle-failures-if-something-goes-wrong"></a><span data-ttu-id="5c677-109">Bir sorun yaşanırsa hataları işleme</span><span class="sxs-lookup"><span data-stu-id="5c677-109">Handle failures if something goes wrong</span></span>

<span data-ttu-id="5c677-110">Tooinclude genellikle, istediğiniz bir *düzeltme adım* — yürütür bazı mantığı *ve yalnızca,* biri veya birkaçı çağrılarınızı başarısız.</span><span class="sxs-lookup"><span data-stu-id="5c677-110">Usually, you want tooinclude a *remediation step* — some logic that executes *if and only if* one or more of your calls fail.</span></span> <span data-ttu-id="5c677-111">Bu örnek verileri çeşitli yerlerden alır, ancak hello çağrısı başarısız olursa, böylece biz daha sonra bu hata izleyebilirsiniz tooPOST bir ileti yere istiyoruz:</span><span class="sxs-lookup"><span data-stu-id="5c677-111">This example gets data from various places, but if hello call fails, we want tooPOST a message somewhere so we can track down that failure later:</span></span>  

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

<span data-ttu-id="5c677-112">toospecify, `postToErrorMessageQueue` sonra yalnızca çalışan `readData` sahip `Failed`, hello kullan `runAfter` özelliği, örneğin, olası bir değer listesi toospecify böylece `runAfter` olabilir `["Succeeded", "Failed"]`.</span><span class="sxs-lookup"><span data-stu-id="5c677-112">toospecify that `postToErrorMessageQueue` only runs after `readData` has `Failed`, use hello `runAfter` property, for example, toospecify a list of possible values, so that `runAfter` could be `["Succeeded", "Failed"]`.</span></span>

<span data-ttu-id="5c677-113">Bu örnek şimdi hello hata işlemesi nedeniyle son olarak, biz artık farklı çalıştır hello işaretlemek `Failed`.</span><span class="sxs-lookup"><span data-stu-id="5c677-113">Finally, because this example now handles hello error, we no longer mark hello run as `Failed`.</span></span> <span data-ttu-id="5c677-114">Çalıştırma hello sahip, bu örnekte bu hata işleme için hello adım eklediğimiz olduğundan `Succeeded` rağmen tek bir adımda `Failed`.</span><span class="sxs-lookup"><span data-stu-id="5c677-114">Because we added hello step for handling this failure in this example, hello run has `Succeeded` although one step `Failed`.</span></span>

## <a name="execute-two-or-more-steps-in-parallel"></a><span data-ttu-id="5c677-115">İki veya daha fazla adım Paralel yürütme</span><span class="sxs-lookup"><span data-stu-id="5c677-115">Execute two or more steps in parallel</span></span>

<span data-ttu-id="5c677-116">toorun paralel olarak birden çok eylem hello `runAfter` özelliği çalışma zamanında eşdeğer olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5c677-116">toorun multiple actions in parallel, hello `runAfter` property must be equivalent at runtime.</span></span> 

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

<span data-ttu-id="5c677-117">Bu örnekte, her ikisi de `branch1` ve `branch2` toorun sonra ayarlanır `readData`.</span><span class="sxs-lookup"><span data-stu-id="5c677-117">In this example, both `branch1` and `branch2` are set toorun after `readData`.</span></span> <span data-ttu-id="5c677-118">Sonuç olarak, her iki dalları paralel olarak çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5c677-118">As a result, both branches run in parallel.</span></span> <span data-ttu-id="5c677-119">Her iki dalları için Hello zaman damgası aynıdır.</span><span class="sxs-lookup"><span data-stu-id="5c677-119">hello timestamp for both branches is identical.</span></span>

![Paralel](media/logic-apps-author-definitions/parallel.png)

## <a name="join-two-parallel-branches"></a><span data-ttu-id="5c677-121">İki paralel dalları katılma</span><span class="sxs-lookup"><span data-stu-id="5c677-121">Join two parallel branches</span></span>

<span data-ttu-id="5c677-122">Toorun öğeleri toohello ekleyerek paralel olarak ayarlanan iki eylem katılabilirsiniz `runAfter` hello önceki örnekte olduğu gibi özelliği.</span><span class="sxs-lookup"><span data-stu-id="5c677-122">You can join two actions that are set toorun in parallel by adding items toohello `runAfter` property as in hello previous example.</span></span>

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

## <a name="map-list-items-tooa-different-configuration"></a><span data-ttu-id="5c677-124">Liste öğeleri tooa farklı yapılandırma eşleme</span><span class="sxs-lookup"><span data-stu-id="5c677-124">Map list items tooa different configuration</span></span>

<span data-ttu-id="5c677-125">Ardından, bir özelliğin hello değere göre tooget farklı içerik istiyoruz diyelim.</span><span class="sxs-lookup"><span data-stu-id="5c677-125">Next, let's say that we want tooget different content based on hello value of a property.</span></span> <span data-ttu-id="5c677-126">Parametre olarak değerleri toodestinations haritasını oluşturabilir:</span><span class="sxs-lookup"><span data-stu-id="5c677-126">We can create a map of values toodestinations as a parameter:</span></span>  

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

<span data-ttu-id="5c677-127">Bu durumda, biz ilk makalelerin listesini alın.</span><span class="sxs-lookup"><span data-stu-id="5c677-127">In this case, we first get a list of articles.</span></span> <span data-ttu-id="5c677-128">Parametre olarak tanımlandı hello kategoriye göre hello ikinci adım harita toolook hello URL yukarı hello içeriği almak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="5c677-128">Based on hello category that was defined as a parameter, hello second step uses a map toolook up hello URL for getting hello content.</span></span>

<span data-ttu-id="5c677-129">Burada bazı kez toonote:</span><span class="sxs-lookup"><span data-stu-id="5c677-129">Some times toonote here:</span></span> 

*   <span data-ttu-id="5c677-130">Merhaba [ `intersection()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#intersection) işlevi hello kategori tanımlanan kategorilere bilinen hello birini eşleşip eşleşmediğini denetler.</span><span class="sxs-lookup"><span data-stu-id="5c677-130">hello [`intersection()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#intersection) function checks whether hello category matches one of hello known defined categories.</span></span>

*   <span data-ttu-id="5c677-131">Biz hello kategori aldıktan sonra biz hello öğesi köşeli ayraç kullanarak hello eşlemesinden çekebilir:`parameters[...]`</span><span class="sxs-lookup"><span data-stu-id="5c677-131">After we get hello category, we can pull hello item from hello map using square brackets: `parameters[...]`</span></span>

## <a name="process-strings"></a><span data-ttu-id="5c677-132">İşlem dizeleri</span><span class="sxs-lookup"><span data-stu-id="5c677-132">Process strings</span></span>

<span data-ttu-id="5c677-133">Çeşitli işlevler toomanipulate dizelerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5c677-133">You can use various functions toomanipulate strings.</span></span> <span data-ttu-id="5c677-134">Örneğin, biz toopass tooa sistem istiyoruz, ancak biz karakter kodlama için uygun işleme hakkında emin olmayan bir dize olduğunu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="5c677-134">For example, suppose we have a string that we want toopass tooa system, but we aren't confident about proper handling for character encoding.</span></span> <span data-ttu-id="5c677-135">Bir seçenektir toobase64 bu dizesini kodlayın.</span><span class="sxs-lookup"><span data-stu-id="5c677-135">One option is toobase64 encode this string.</span></span> <span data-ttu-id="5c677-136">Ancak, bir URL'de kaçış tooavoid tooreplace birkaç karakter çağıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="5c677-136">However, tooavoid escaping in a URL, we are going tooreplace a few characters.</span></span> 

<span data-ttu-id="5c677-137">Hello ilk beş karakter olmayan kullanıldığı için de bir dizenin hello sipariş adını istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="5c677-137">We also want a substring of hello order's name because hello first five characters are not used.</span></span>

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

<span data-ttu-id="5c677-138">Toooutside içinde çalışma:</span><span class="sxs-lookup"><span data-stu-id="5c677-138">Working from inside toooutside:</span></span>

1. <span data-ttu-id="5c677-139">Merhaba alma [ `length()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#length) hello sipariş ın eden adı için böylece biz geri alma hello toplam karakter sayısı.</span><span class="sxs-lookup"><span data-stu-id="5c677-139">Get hello [`length()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#length) for hello orderer's name, so we get back hello total number of characters.</span></span>

2. <span data-ttu-id="5c677-140">Daha kısa bir dize istiyoruz çünkü 5 çıkarın.</span><span class="sxs-lookup"><span data-stu-id="5c677-140">Subtract 5 because we want a shorter string.</span></span>

3. <span data-ttu-id="5c677-141">Aslında, hello ele [ `substring()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#substring).</span><span class="sxs-lookup"><span data-stu-id="5c677-141">Actually, take hello [`substring()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#substring).</span></span> <span data-ttu-id="5c677-142">Biz dizininde Başlat `5` ve hello dize geri kalanı hello gidin.</span><span class="sxs-lookup"><span data-stu-id="5c677-142">We start at index `5` and go hello remainder of hello string.</span></span>

4. <span data-ttu-id="5c677-143">Bu alt dizeyi tooa Dönüştür [ `base64()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#base64) dize.</span><span class="sxs-lookup"><span data-stu-id="5c677-143">Convert this substring tooa [`base64()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#base64) string.</span></span>

5. <span data-ttu-id="5c677-144">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace)Tüm hello `+` ile karakterleri `-` karakter.</span><span class="sxs-lookup"><span data-stu-id="5c677-144">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) all hello `+` characters with `-` characters.</span></span>

6. <span data-ttu-id="5c677-145">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace)Tüm hello `/` ile karakterleri `_` karakter.</span><span class="sxs-lookup"><span data-stu-id="5c677-145">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) all hello `/` characters with `_` characters.</span></span>

## <a name="work-with-date-times"></a><span data-ttu-id="5c677-146">Tarih süreleri ile çalışma</span><span class="sxs-lookup"><span data-stu-id="5c677-146">Work with Date Times</span></span>

<span data-ttu-id="5c677-147">Özellikle doğal olarak desteklemeyen bir veri kaynağından alınan toopull veriler çalışırken tarih kez yararlı olabilir *Tetikleyicileri*.</span><span class="sxs-lookup"><span data-stu-id="5c677-147">Date Times can be useful, particularly when you are trying toopull data from a data source that doesn't naturally support *triggers*.</span></span> <span data-ttu-id="5c677-148">Tarih Saatler ne kadar çeşitli adımları kaplayan bulmak için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5c677-148">You can also use Date Times for finding how long various steps are taking.</span></span>

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

<span data-ttu-id="5c677-149">Bu örnekte, biz hello ayıklamak `startTime` hello önceki adımdaki.</span><span class="sxs-lookup"><span data-stu-id="5c677-149">In this example, we extract hello `startTime` from hello previous step.</span></span> <span data-ttu-id="5c677-150">Biz hello geçerli saati almak ve bir ikinci çıkarma sonra:</span><span class="sxs-lookup"><span data-stu-id="5c677-150">Then we get hello current time, and subtract one second:</span></span>

[`addseconds(..., -1)`](https://msdn.microsoft.com/library/azure/mt643789.aspx#addseconds) 

<span data-ttu-id="5c677-151">İsterseniz zaman, diğer birimleri kullanabilirsiniz `minutes` veya `hours`.</span><span class="sxs-lookup"><span data-stu-id="5c677-151">You can use other units of time, like `minutes` or `hours`.</span></span> <span data-ttu-id="5c677-152">Son olarak, biz bu iki değer karşılaştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5c677-152">Finally, we can compare these two values.</span></span> <span data-ttu-id="5c677-153">Hello ilk değer hello ikinci değer sonra bir saniyeden küçükse hello sipariş ilk yerleştirilen geçen.</span><span class="sxs-lookup"><span data-stu-id="5c677-153">If hello first value is less than hello second value, then more than one second has passed since hello order was first placed.</span></span>

<span data-ttu-id="5c677-154">tooformat tarihleri dize biçimlendiricileri kullanırız.</span><span class="sxs-lookup"><span data-stu-id="5c677-154">tooformat dates, we can use string formatters.</span></span> <span data-ttu-id="5c677-155">Örneğin, tooget hello RFC1123, kullandığımız [ `utcnow('r')` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span><span class="sxs-lookup"><span data-stu-id="5c677-155">For example, tooget hello RFC1123, we use [`utcnow('r')`](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span></span> <span data-ttu-id="5c677-156">Tarih biçimlendirme hakkında toolearn bkz [iş akışı tanımlama dili](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span><span class="sxs-lookup"><span data-stu-id="5c677-156">toolearn about date formatting, see [Workflow Definition Language](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span></span>

## <a name="deployment-parameters-for-different-environments"></a><span data-ttu-id="5c677-157">Farklı ortamlar için dağıtım parametreleri</span><span class="sxs-lookup"><span data-stu-id="5c677-157">Deployment parameters for different environments</span></span>

<span data-ttu-id="5c677-158">Genellikle, bir geliştirme ortamı, hazırlık ortamı ve bir üretim ortamında dağıtım yaşam döngüleri vardır.</span><span class="sxs-lookup"><span data-stu-id="5c677-158">Commonly, deployment lifecycles have a development environment, a staging environment, and a production environment.</span></span> <span data-ttu-id="5c677-159">Örneğin, kullanabilirsiniz hello tüm ortamlarda aynı tanımın ancak farklı veritabanlarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="5c677-159">For example, you might use hello same definition in all these environments but use different databases.</span></span> <span data-ttu-id="5c677-160">Benzer şekilde, toouse isteyebilirsiniz farklı bölgelere yüksek kullanılabilirlik için aynı tanımın hello ancak her mantıksal uygulama örneğini tootalk toothat bölgenin veritabanı istiyor.</span><span class="sxs-lookup"><span data-stu-id="5c677-160">Likewise, you might want toouse hello same definition across different regions for high availability but want each logic app instance tootalk toothat region's database.</span></span>
<span data-ttu-id="5c677-161">Bu senaryo parametrelerinin alma farklı *çalışma zamanı* Burada bunun yerine, kullanmanız gereken hello `trigger()` hello önceki örnekte olduğu gibi işlev.</span><span class="sxs-lookup"><span data-stu-id="5c677-161">This scenario differs from taking parameters at *runtime* where instead, you should use hello `trigger()` function as in hello previous example.</span></span>

<span data-ttu-id="5c677-162">Bu örnek gibi temel bir tanımıyla başlatabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5c677-162">You can start with a basic definition like this example:</span></span>

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

<span data-ttu-id="5c677-163">Merhaba gerçek içinde `PUT` hello parametre sağlayabilir hello logic apps için istek `uri`.</span><span class="sxs-lookup"><span data-stu-id="5c677-163">In hello actual `PUT` request for hello logic apps, you can provide hello parameter `uri`.</span></span> <span data-ttu-id="5c677-164">Varsayılan değeri artık mevcut olmadığından, bu parametre hello mantığı uygulama yükü gerektirir:</span><span class="sxs-lookup"><span data-stu-id="5c677-164">Because a default value no longer exists, hello logic app payload requires this parameter:</span></span>

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

<span data-ttu-id="5c677-165">Her bir ortamda hello için farklı bir değer sağlayabilir `connection` parametresi.</span><span class="sxs-lookup"><span data-stu-id="5c677-165">In each environment, you can provide a different value for hello `connection` parameter.</span></span> 

<span data-ttu-id="5c677-166">Tüm oluşturmak ve mantıksal uygulamaları yönetmek için seçenekleri hello hello bakın [REST API belgeleri](https://msdn.microsoft.com/library/azure/mt643787.aspx).</span><span class="sxs-lookup"><span data-stu-id="5c677-166">For all hello options that you have for creating and managing logic apps, see hello [REST API documentation](https://msdn.microsoft.com/library/azure/mt643787.aspx).</span></span> 
