---
title: "JSON - Azure Logic Apps ile iş akışları tanımlama | Microsoft Docs"
description: "İş akışı tanımları JSON'de logic apps için yazma"
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
ms.openlocfilehash: 7f9e5a10066df8a464c285273e77a85c0d562ebb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-workflow-definitions-for-logic-apps-using-json"></a><span data-ttu-id="da8eb-103">JSON kullanarak logic apps için iş akışı tanımları oluşturma</span><span class="sxs-lookup"><span data-stu-id="da8eb-103">Create workflow definitions for logic apps using JSON</span></span>

<span data-ttu-id="da8eb-104">İş akışı tanımları için oluşturabileceğiniz [Azure Logic Apps](logic-apps-what-are-logic-apps.md) basit ve bildirim temelli JSON dili.</span><span class="sxs-lookup"><span data-stu-id="da8eb-104">You can create workflow definitions for [Azure Logic Apps](logic-apps-what-are-logic-apps.md) with simple, declarative JSON language.</span></span> <span data-ttu-id="da8eb-105">Henüz yapmadıysanız, ilk gözden [mantığı Uygulama Tasarımcısı ile ilk mantıksal uygulamanızı oluşturmak nasıl](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="da8eb-105">If you haven't already, first review [how to create your first logic app with Logic App Designer](logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="da8eb-106">Ayrıca bkz [tam başvuru için iş akışı tanımlama dili](http://aka.ms/logicappsdocs).</span><span class="sxs-lookup"><span data-stu-id="da8eb-106">Also, see the [full reference for the Workflow Definition Language](http://aka.ms/logicappsdocs).</span></span>

## <a name="repeat-steps-over-a-list"></a><span data-ttu-id="da8eb-107">Bir liste arasındaki adımları yineleyin</span><span class="sxs-lookup"><span data-stu-id="da8eb-107">Repeat steps over a list</span></span>

<span data-ttu-id="da8eb-108">10.000 öğelerine sahip bir dizi yinelemek ve her öğe için bir eylem gerçekleştirmek için kullanmanız [foreach türü](logic-apps-loops-and-scopes.md).</span><span class="sxs-lookup"><span data-stu-id="da8eb-108">To iterate through an array that has up to 10,000 items and perform an action for each item, use the [foreach type](logic-apps-loops-and-scopes.md).</span></span>

## <a name="handle-failures-if-something-goes-wrong"></a><span data-ttu-id="da8eb-109">Bir sorun yaşanırsa hataları işleme</span><span class="sxs-lookup"><span data-stu-id="da8eb-109">Handle failures if something goes wrong</span></span>

<span data-ttu-id="da8eb-110">Genellikle, dahil etmek istediğiniz bir *düzeltme adım* — yürütür bazı mantığı *ve yalnızca,* biri veya birkaçı çağrılarınızı başarısız.</span><span class="sxs-lookup"><span data-stu-id="da8eb-110">Usually, you want to include a *remediation step* — some logic that executes *if and only if* one or more of your calls fail.</span></span> <span data-ttu-id="da8eb-111">Bu örnek verileri çeşitli yerlerden alır, ancak çağrısı başarısız olursa, böylece biz daha sonra bu hata izleyebilirsiniz ileti yere POSTALAMA istiyoruz:</span><span class="sxs-lookup"><span data-stu-id="da8eb-111">This example gets data from various places, but if the call fails, we want to POST a message somewhere so we can track down that failure later:</span></span>  

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

<span data-ttu-id="da8eb-112">Belirtmek için `postToErrorMessageQueue` sonra yalnızca çalışan `readData` sahip `Failed`, kullanın `runAfter` olası değerler listesini belirtmek için özellik, örneğin, böylece `runAfter` olabilir `["Succeeded", "Failed"]`.</span><span class="sxs-lookup"><span data-stu-id="da8eb-112">To specify that `postToErrorMessageQueue` only runs after `readData` has `Failed`, use the `runAfter` property, for example, to specify a list of possible values, so that `runAfter` could be `["Succeeded", "Failed"]`.</span></span>

<span data-ttu-id="da8eb-113">Bu örnek şimdi hata işlemesi nedeniyle son olarak, biz artık Çalıştır işaretlemek `Failed`.</span><span class="sxs-lookup"><span data-stu-id="da8eb-113">Finally, because this example now handles the error, we no longer mark the run as `Failed`.</span></span> <span data-ttu-id="da8eb-114">Bu örnekte bu hata işleme için adım eklediğimiz çünkü Çalıştır sahip `Succeeded` rağmen tek bir adımda `Failed`.</span><span class="sxs-lookup"><span data-stu-id="da8eb-114">Because we added the step for handling this failure in this example, the run has `Succeeded` although one step `Failed`.</span></span>

## <a name="execute-two-or-more-steps-in-parallel"></a><span data-ttu-id="da8eb-115">İki veya daha fazla adım Paralel yürütme</span><span class="sxs-lookup"><span data-stu-id="da8eb-115">Execute two or more steps in parallel</span></span>

<span data-ttu-id="da8eb-116">Paralel olarak birden çok eylem çalıştırmak için `runAfter` özelliği çalışma zamanında eşdeğer olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="da8eb-116">To run multiple actions in parallel, the `runAfter` property must be equivalent at runtime.</span></span> 

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

<span data-ttu-id="da8eb-117">Bu örnekte, her ikisi de `branch1` ve `branch2` çalışacak şekilde ayarlanmış `readData`.</span><span class="sxs-lookup"><span data-stu-id="da8eb-117">In this example, both `branch1` and `branch2` are set to run after `readData`.</span></span> <span data-ttu-id="da8eb-118">Sonuç olarak, her iki dalları paralel olarak çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="da8eb-118">As a result, both branches run in parallel.</span></span> <span data-ttu-id="da8eb-119">Her iki dalları için zaman damgası aynıdır.</span><span class="sxs-lookup"><span data-stu-id="da8eb-119">The timestamp for both branches is identical.</span></span>

![Paralel](media/logic-apps-author-definitions/parallel.png)

## <a name="join-two-parallel-branches"></a><span data-ttu-id="da8eb-121">İki paralel dalları katılma</span><span class="sxs-lookup"><span data-stu-id="da8eb-121">Join two parallel branches</span></span>

<span data-ttu-id="da8eb-122">Öğelerine ekleyerek paralel olarak çalışacak şekilde ayarlanmış iki eylem katılabilirsiniz `runAfter` özelliği önceki örnekte olduğu gibi.</span><span class="sxs-lookup"><span data-stu-id="da8eb-122">You can join two actions that are set to run in parallel by adding items to the `runAfter` property as in the previous example.</span></span>

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

## <a name="map-list-items-to-a-different-configuration"></a><span data-ttu-id="da8eb-124">Liste öğeleri için farklı bir yapılandırma eşleme</span><span class="sxs-lookup"><span data-stu-id="da8eb-124">Map list items to a different configuration</span></span>

<span data-ttu-id="da8eb-125">Ardından, bir özellik değeri temel alınarak farklı içerik almak istiyoruz diyelim.</span><span class="sxs-lookup"><span data-stu-id="da8eb-125">Next, let's say that we want to get different content based on the value of a property.</span></span> <span data-ttu-id="da8eb-126">Parametre olarak değerleri hedeflere haritasını oluşturabilir:</span><span class="sxs-lookup"><span data-stu-id="da8eb-126">We can create a map of values to destinations as a parameter:</span></span>  

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

<span data-ttu-id="da8eb-127">Bu durumda, biz ilk makalelerin listesini alın.</span><span class="sxs-lookup"><span data-stu-id="da8eb-127">In this case, we first get a list of articles.</span></span> <span data-ttu-id="da8eb-128">İkinci adım parametre olarak tanımlandı kategoriye göre içeriği almak için URL aramak için bir harita kullanır.</span><span class="sxs-lookup"><span data-stu-id="da8eb-128">Based on the category that was defined as a parameter, the second step uses a map to look up the URL for getting the content.</span></span>

<span data-ttu-id="da8eb-129">Burada dikkat edilecek bazı süresi:</span><span class="sxs-lookup"><span data-stu-id="da8eb-129">Some times to note here:</span></span> 

*   <span data-ttu-id="da8eb-130">[ `intersection()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#intersection) İşlevi kategori bilinen tanımlı kategorilerden birini eşleşip eşleşmediğini denetler.</span><span class="sxs-lookup"><span data-stu-id="da8eb-130">The [`intersection()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#intersection) function checks whether the category matches one of the known defined categories.</span></span>

*   <span data-ttu-id="da8eb-131">Biz kategori aldıktan sonra biz köşeli ayraç kullanarak harita öğesinden çekebilir:`parameters[...]`</span><span class="sxs-lookup"><span data-stu-id="da8eb-131">After we get the category, we can pull the item from the map using square brackets: `parameters[...]`</span></span>

## <a name="process-strings"></a><span data-ttu-id="da8eb-132">İşlem dizeleri</span><span class="sxs-lookup"><span data-stu-id="da8eb-132">Process strings</span></span>

<span data-ttu-id="da8eb-133">Dizeleri işlemek için çeşitli işlevleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="da8eb-133">You can use various functions to manipulate strings.</span></span> <span data-ttu-id="da8eb-134">Örneğin, bir sisteme geçirmek için istiyoruz bir dize sahip olduğumuz ancak biz karakter kodlama için uygun işleme hakkında emin değilseniz varsayalım.</span><span class="sxs-lookup"><span data-stu-id="da8eb-134">For example, suppose we have a string that we want to pass to a system, but we aren't confident about proper handling for character encoding.</span></span> <span data-ttu-id="da8eb-135">Bir seçenektir base64 için bu dizesini kodlayın.</span><span class="sxs-lookup"><span data-stu-id="da8eb-135">One option is to base64 encode this string.</span></span> <span data-ttu-id="da8eb-136">Ancak, bir URL kaçış önlemek için sizi birkaç karakterlerini değiştirmek için adımıdır.</span><span class="sxs-lookup"><span data-stu-id="da8eb-136">However, to avoid escaping in a URL, we are going to replace a few characters.</span></span> 

<span data-ttu-id="da8eb-137">İlk beş karakter olmayan kullanıldığından de sipariş adını alt dizeyi istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="da8eb-137">We also want a substring of the order's name because the first five characters are not used.</span></span>

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

<span data-ttu-id="da8eb-138">Çalışmasını içinde için dışında:</span><span class="sxs-lookup"><span data-stu-id="da8eb-138">Working from inside to outside:</span></span>

1. <span data-ttu-id="da8eb-139">Alma [ `length()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#length) için sipariş eden'ın adı, böylece biz geri alma toplam karakter sayısı.</span><span class="sxs-lookup"><span data-stu-id="da8eb-139">Get the [`length()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#length) for the orderer's name, so we get back the total number of characters.</span></span>

2. <span data-ttu-id="da8eb-140">Daha kısa bir dize istiyoruz çünkü 5 çıkarın.</span><span class="sxs-lookup"><span data-stu-id="da8eb-140">Subtract 5 because we want a shorter string.</span></span>

3. <span data-ttu-id="da8eb-141">Aslında, ele [ `substring()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#substring).</span><span class="sxs-lookup"><span data-stu-id="da8eb-141">Actually, take the [`substring()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#substring).</span></span> <span data-ttu-id="da8eb-142">Biz dizininde Başlat `5` ve dizenin geri kalanı gidin.</span><span class="sxs-lookup"><span data-stu-id="da8eb-142">We start at index `5` and go the remainder of the string.</span></span>

4. <span data-ttu-id="da8eb-143">Bu alt dizeyi Dönüştür bir [ `base64()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#base64) dize.</span><span class="sxs-lookup"><span data-stu-id="da8eb-143">Convert this substring to a [`base64()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#base64) string.</span></span>

5. <span data-ttu-id="da8eb-144">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace)tüm `+` ile karakterleri `-` karakter.</span><span class="sxs-lookup"><span data-stu-id="da8eb-144">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) all the `+` characters with `-` characters.</span></span>

6. <span data-ttu-id="da8eb-145">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace)tüm `/` ile karakterleri `_` karakter.</span><span class="sxs-lookup"><span data-stu-id="da8eb-145">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) all the `/` characters with `_` characters.</span></span>

## <a name="work-with-date-times"></a><span data-ttu-id="da8eb-146">Tarih süreleri ile çalışma</span><span class="sxs-lookup"><span data-stu-id="da8eb-146">Work with Date Times</span></span>

<span data-ttu-id="da8eb-147">Özellikle doğal olarak desteklemeyen bir veri kaynağından veri almasına izin verirken tarih kez yararlı olabilir *Tetikleyicileri*.</span><span class="sxs-lookup"><span data-stu-id="da8eb-147">Date Times can be useful, particularly when you are trying to pull data from a data source that doesn't naturally support *triggers*.</span></span> <span data-ttu-id="da8eb-148">Tarih Saatler ne kadar çeşitli adımları kaplayan bulmak için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="da8eb-148">You can also use Date Times for finding how long various steps are taking.</span></span>

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

<span data-ttu-id="da8eb-149">Bu örnekte, biz ayıklamak `startTime` önceki adımdan.</span><span class="sxs-lookup"><span data-stu-id="da8eb-149">In this example, we extract the `startTime` from the previous step.</span></span> <span data-ttu-id="da8eb-150">Biz geçerli saati almak ve bir ikinci çıkarma sonra:</span><span class="sxs-lookup"><span data-stu-id="da8eb-150">Then we get the current time, and subtract one second:</span></span>

[`addseconds(..., -1)`](https://msdn.microsoft.com/library/azure/mt643789.aspx#addseconds) 

<span data-ttu-id="da8eb-151">İsterseniz zaman, diğer birimleri kullanabilirsiniz `minutes` veya `hours`.</span><span class="sxs-lookup"><span data-stu-id="da8eb-151">You can use other units of time, like `minutes` or `hours`.</span></span> <span data-ttu-id="da8eb-152">Son olarak, biz bu iki değer karşılaştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="da8eb-152">Finally, we can compare these two values.</span></span> <span data-ttu-id="da8eb-153">İlk değer ikinci değer sonra bir saniyeden küçükse sırasını ilk yerleştirilen geçen.</span><span class="sxs-lookup"><span data-stu-id="da8eb-153">If the first value is less than the second value, then more than one second has passed since the order was first placed.</span></span>

<span data-ttu-id="da8eb-154">Tarihleri biçimlendirmek için dize biçimlendiricileri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="da8eb-154">To format dates, we can use string formatters.</span></span> <span data-ttu-id="da8eb-155">Örneğin, RFC1123 almak için kullanırız [ `utcnow('r')` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span><span class="sxs-lookup"><span data-stu-id="da8eb-155">For example, to get the RFC1123, we use [`utcnow('r')`](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span></span> <span data-ttu-id="da8eb-156">Tarih biçimlendirme hakkında bilgi edinmek için [iş akışı tanımlama dili](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span><span class="sxs-lookup"><span data-stu-id="da8eb-156">To learn about date formatting, see [Workflow Definition Language](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span></span>

## <a name="deployment-parameters-for-different-environments"></a><span data-ttu-id="da8eb-157">Farklı ortamlar için dağıtım parametreleri</span><span class="sxs-lookup"><span data-stu-id="da8eb-157">Deployment parameters for different environments</span></span>

<span data-ttu-id="da8eb-158">Genellikle, bir geliştirme ortamı, hazırlık ortamı ve bir üretim ortamında dağıtım yaşam döngüleri vardır.</span><span class="sxs-lookup"><span data-stu-id="da8eb-158">Commonly, deployment lifecycles have a development environment, a staging environment, and a production environment.</span></span> <span data-ttu-id="da8eb-159">Örneğin, aynı tanımın tüm bu ortamlarda ancak farklı veritabanlarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="da8eb-159">For example, you might use the same definition in all these environments but use different databases.</span></span> <span data-ttu-id="da8eb-160">Benzer şekilde, aynı tanımın farklı bölgeler arasında yüksek kullanılabilirlik için kullanın, ancak her logic app örneği bölgenin veritabanı ile iletişim kurmak istediğiniz isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="da8eb-160">Likewise, you might want to use the same definition across different regions for high availability but want each logic app instance to talk to that region's database.</span></span>
<span data-ttu-id="da8eb-161">Bu senaryo parametrelerinin alma farklı *çalışma zamanı* Burada bunun yerine, kullanmanız gereken `trigger()` önceki örnekte olduğu gibi işlev.</span><span class="sxs-lookup"><span data-stu-id="da8eb-161">This scenario differs from taking parameters at *runtime* where instead, you should use the `trigger()` function as in the previous example.</span></span>

<span data-ttu-id="da8eb-162">Bu örnek gibi temel bir tanımıyla başlatabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="da8eb-162">You can start with a basic definition like this example:</span></span>

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

<span data-ttu-id="da8eb-163">Fiili olarak `PUT` isteği logic apps için parametre sağlayabilir `uri`.</span><span class="sxs-lookup"><span data-stu-id="da8eb-163">In the actual `PUT` request for the logic apps, you can provide the parameter `uri`.</span></span> <span data-ttu-id="da8eb-164">Varsayılan değeri artık mevcut olmadığından, bu parametre mantığı uygulama yükü gerektirir:</span><span class="sxs-lookup"><span data-stu-id="da8eb-164">Because a default value no longer exists, the logic app payload requires this parameter:</span></span>

```
{
    "properties": {},
        "definition": {
          // Use the definition from above here
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

<span data-ttu-id="da8eb-165">Her bir ortamda için farklı bir değer sağlayabilir `connection` parametresi.</span><span class="sxs-lookup"><span data-stu-id="da8eb-165">In each environment, you can provide a different value for the `connection` parameter.</span></span> 

<span data-ttu-id="da8eb-166">Oluşturma ve mantıksal uygulamaları yönetmek için tüm seçenekleri için bkz: [REST API belgeleri](https://msdn.microsoft.com/library/azure/mt643787.aspx).</span><span class="sxs-lookup"><span data-stu-id="da8eb-166">For all the options that you have for creating and managing logic apps, see the [REST API documentation](https://msdn.microsoft.com/library/azure/mt643787.aspx).</span></span> 
