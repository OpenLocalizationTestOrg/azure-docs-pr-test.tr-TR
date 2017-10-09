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
# <a name="logic-apps-loops-scopes-and-debatching"></a><span data-ttu-id="3a31e-103">Logic Apps Döngüleri, Kapsamları ve Ayırma</span><span class="sxs-lookup"><span data-stu-id="3a31e-103">Logic Apps Loops, Scopes, and Debatching</span></span>
  
<span data-ttu-id="3a31e-104">Logic Apps diziler, koleksiyonları, toplu işleri ve bir iş akışındaki döngüler yolları toowork sayısını sağlar.</span><span class="sxs-lookup"><span data-stu-id="3a31e-104">Logic Apps provides a number of ways toowork with arrays, collections, batches, and loops within a workflow.</span></span>
  
## <a name="foreach-loop-and-arrays"></a><span data-ttu-id="3a31e-105">ForEach döngüsü ve diziler</span><span class="sxs-lookup"><span data-stu-id="3a31e-105">ForEach loop and arrays</span></span>
  
<span data-ttu-id="3a31e-106">Logic Apps bir veri kümesi üzerinde tooloop sağlar ve her öğe için bir eylemi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="3a31e-106">Logic Apps allows you tooloop over a set of data and perform an action for each item.</span></span>  <span data-ttu-id="3a31e-107">Bu hello mümkündür `foreach` eylem.</span><span class="sxs-lookup"><span data-stu-id="3a31e-107">This is possible via hello `foreach` action.</span></span>  <span data-ttu-id="3a31e-108">Merhaba Tasarımcısı'nda tooadd belirtebilirsiniz bir her döngü için.</span><span class="sxs-lookup"><span data-stu-id="3a31e-108">In hello designer, you can specify tooadd a for each loop.</span></span>  <span data-ttu-id="3a31e-109">Merhaba dizi üzerinden tooiterate istediğiniz seçtikten sonra Eylemler eklemeye başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3a31e-109">After selecting hello array you wish tooiterate over, you can begin adding actions.</span></span>  <span data-ttu-id="3a31e-110">Şu anda sınırlı tooonly bir eylem foreach döngüsü başına olan, ancak bu kısıtlama hafta gelen hello kaldırılmış.</span><span class="sxs-lookup"><span data-stu-id="3a31e-110">Currently you are limited tooonly one action per foreach loop, but this restriction will be lifted in hello coming weeks.</span></span>  <span data-ttu-id="3a31e-111">Bir kez hello döngü içinde her hello dizi değerinde gerekeni toospecify başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3a31e-111">Once within hello loop you can begin toospecify what should occur at each value of hello array.</span></span>

<span data-ttu-id="3a31e-112">Kod görünümünü kullanıyorsanız, belirleyebileceğiniz bir aşağıdaki gibi her bir döngü için.</span><span class="sxs-lookup"><span data-stu-id="3a31e-112">If using code-view, you can specify a for each loop like below.</span></span>  <span data-ttu-id="3a31e-113">Bu örneği olan bir 'microsoft.com' içeren her bir e-posta adresi için bir e-posta gönderir her bir döngü için:</span><span class="sxs-lookup"><span data-stu-id="3a31e-113">This is an example of a for each loop that sends an email for each email address that contains 'microsoft.com':</span></span>

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
  
  <span data-ttu-id="3a31e-114">A `foreach` eylem too5, 000 satırları yukarı diziler üzerinden yineleme.</span><span class="sxs-lookup"><span data-stu-id="3a31e-114">A `foreach` action can iterate over arrays up too5,000 rows.</span></span>  <span data-ttu-id="3a31e-115">Her yineleme paralel olarak varsayılan olarak yürütülür.</span><span class="sxs-lookup"><span data-stu-id="3a31e-115">Each iteration will execute in parallel by default.</span></span>  

### <a name="sequential-foreach-loops"></a><span data-ttu-id="3a31e-116">Sıralı ForEach döngüsü</span><span class="sxs-lookup"><span data-stu-id="3a31e-116">Sequential ForEach loops</span></span>

<span data-ttu-id="3a31e-117">foreach döngüsü tooexecute ardışık olarak hello tooenable `Sequential` işlemi seçeneği eklenir.</span><span class="sxs-lookup"><span data-stu-id="3a31e-117">tooenable a foreach loop tooexecute sequentially, hello `Sequential` operation option should be added.</span></span>

``` json
"forEach_email": {
        "type": "foreach",
        "foreach": "@body('email_filter')",
        "operationOptions": "Sequential",
        "..."
}
```
  
## <a name="until-loop"></a><span data-ttu-id="3a31e-118">Döngü kadar</span><span class="sxs-lookup"><span data-stu-id="3a31e-118">Until loop</span></span>
  
  <span data-ttu-id="3a31e-119">Bir koşul yerine getirilene kadar bir eylem veya dizi eylem gerçekleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="3a31e-119">You can perform an action or series of actions until a condition is met.</span></span>  <span data-ttu-id="3a31e-120">Aradığınız hello yanıt elde edene kadar hello Bunun en yaygın senaryo bir uç nokta çağırıyor.</span><span class="sxs-lookup"><span data-stu-id="3a31e-120">hello most common scenario for this is calling an endpoint until you get hello response you are looking for.</span></span>  <span data-ttu-id="3a31e-121">Merhaba Tasarımcısı'nda tooadd belirtebilirsiniz bir döngü kadar.</span><span class="sxs-lookup"><span data-stu-id="3a31e-121">In hello designer, you can specify tooadd an until loop.</span></span>  <span data-ttu-id="3a31e-122">Eylemler hello döngü içinde ekledikten sonra hello çıkış koşulu yanı döngü sınırları hello.</span><span class="sxs-lookup"><span data-stu-id="3a31e-122">After adding actions inside hello loop, you can set hello exit condition, as well as hello loop limits.</span></span>  <span data-ttu-id="3a31e-123">Döngü döngüleri arasında 1 dakikalık bir gecikmeyle yoktur.</span><span class="sxs-lookup"><span data-stu-id="3a31e-123">There is a 1 minute delay between loop cycles.</span></span>
  
  <span data-ttu-id="3a31e-124">Kod görünümünü kullanıyorsanız, belirleyebileceğiniz bir döngü ister aşağıda kadar.</span><span class="sxs-lookup"><span data-stu-id="3a31e-124">If using code-view, you can specify an until loop like below.</span></span>  <span data-ttu-id="3a31e-125">Bu hello değeri 'Tamamlandı' hello yanıt gövdesi olana kadar bir HTTP uç noktası çağrılmadan bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="3a31e-125">This is an example of calling an HTTP endpoint until hello response body has hello value 'Completed'.</span></span>  <span data-ttu-id="3a31e-126">Ne zaman tamamlanır ya da</span><span class="sxs-lookup"><span data-stu-id="3a31e-126">It will complete when either</span></span> 
  
  * <span data-ttu-id="3a31e-127">HTTP yanıtı 'Tamamlandı' durumuna sahip</span><span class="sxs-lookup"><span data-stu-id="3a31e-127">HTTP Response has status of 'Completed'</span></span>
  * <span data-ttu-id="3a31e-128">1 saat boyunca çalıştı</span><span class="sxs-lookup"><span data-stu-id="3a31e-128">It has tried for 1 hour</span></span>
  * <span data-ttu-id="3a31e-129">100 kez döngüye</span><span class="sxs-lookup"><span data-stu-id="3a31e-129">It has looped 100 times</span></span>
  
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
  
## <a name="spliton-and-debatching"></a><span data-ttu-id="3a31e-130">SplitOn ve debatching</span><span class="sxs-lookup"><span data-stu-id="3a31e-130">SplitOn and debatching</span></span>

<span data-ttu-id="3a31e-131">Bazen bir tetikleyici bir dizi toodebatch istediğiniz ve bir iş akışı öğesi başına başlatmak öğeleri alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3a31e-131">Sometimes a trigger may receive an array of items that you want toodebatch and start a workflow per item.</span></span>  <span data-ttu-id="3a31e-132">Bu hello gerçekleştirilebilir `spliton` komutu.</span><span class="sxs-lookup"><span data-stu-id="3a31e-132">This can be accomplished via hello `spliton` command.</span></span>  <span data-ttu-id="3a31e-133">Varsayılan olarak, tetikleyici swagger bir dizi bir yükü belirtiyorsa, bir `spliton` eklenir ve bir çalışma öğesi başına başlatın.</span><span class="sxs-lookup"><span data-stu-id="3a31e-133">By default, if your trigger swagger specifies a payload that is an array, a `spliton` will be added and start a run per item.</span></span>  <span data-ttu-id="3a31e-134">SplitOn yalnızca tooa tetikleyici eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="3a31e-134">SplitOn can only be added tooa trigger.</span></span>  <span data-ttu-id="3a31e-135">Bu el ile yapılandırılabildiğinden veya tanımı kod görünümünde geçersiz kılındı.</span><span class="sxs-lookup"><span data-stu-id="3a31e-135">This can be manually configured or overridden in definition code-view.</span></span>  <span data-ttu-id="3a31e-136">Şu anda SplitOn too5, 000 öğeleri yukarı diziler debatch.</span><span class="sxs-lookup"><span data-stu-id="3a31e-136">Currently SplitOn can debatch arrays up too5,000 items.</span></span>  <span data-ttu-id="3a31e-137">Sahip olamaz bir `spliton` ve ayrıca hello zaman uyumlu yanıt desenini uygular.</span><span class="sxs-lookup"><span data-stu-id="3a31e-137">You cannot have a `spliton` and also implement hello synchronous response pattern.</span></span>  <span data-ttu-id="3a31e-138">Adında herhangi bir iş akışının sahip bir `response` eylem ayrıca çok`spliton` zaman uyumsuz olarak çalışacak ve hemen gönder `202 Accepted` yanıt.</span><span class="sxs-lookup"><span data-stu-id="3a31e-138">Any workflow called that has a `response` action in addition too`spliton` will run asynchronously and send an immediate `202 Accepted` response.</span></span>  

<span data-ttu-id="3a31e-139">SplitOn kod görünümünde aşağıdaki örneğine hello belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="3a31e-139">SplitOn can be specified in code-view as hello following example.</span></span>  <span data-ttu-id="3a31e-140">Bu öğeleri dizisini alır ve her satırda debatches.</span><span class="sxs-lookup"><span data-stu-id="3a31e-140">This receives an array of items and debatches on each row.</span></span>

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

## <a name="scopes"></a><span data-ttu-id="3a31e-141">Kapsamları</span><span class="sxs-lookup"><span data-stu-id="3a31e-141">Scopes</span></span>

<span data-ttu-id="3a31e-142">Bu, olası toogroup birlikte bir kapsamı kullanarak eylemleri bir dizi olur.</span><span class="sxs-lookup"><span data-stu-id="3a31e-142">It is possible toogroup a series of actions together using a scope.</span></span>  <span data-ttu-id="3a31e-143">Özel durum işleme uygulamak için özellikle yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="3a31e-143">This is particularly useful for implementing exception handling.</span></span>  <span data-ttu-id="3a31e-144">Merhaba Tasarımcısı'nda yeni bir kapsam ekleyin ve onu içinde herhangi bir eylem eklemeye başlamak.</span><span class="sxs-lookup"><span data-stu-id="3a31e-144">In hello designer you can add a new scope, and begin adding any actions inside of it.</span></span>  <span data-ttu-id="3a31e-145">Merhaba aşağıdaki gibi kod görünümünde kapsamları tanımlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3a31e-145">You can define scopes in code-view like hello following:</span></span>


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