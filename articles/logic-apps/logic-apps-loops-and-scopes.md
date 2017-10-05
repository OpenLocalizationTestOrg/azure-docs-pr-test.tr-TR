---
title: "Döngüler ve kapsamları oluşturun ya da iş akışları - Azure Logic Apps verilerde debatch | Microsoft Docs"
description: "Veri, kapsamları, Grup eylemlere yinelemek için döngüler oluşturun veya Azure Logic Apps içinde daha fazla iş akışlarını başlatmak için veri debatch."
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
ms.openlocfilehash: 413a2ba9107ca259ed577825bf0a17ff5622f1ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="logic-apps-loops-scopes-and-debatching"></a><span data-ttu-id="0b785-103">Logic Apps Döngüleri, Kapsamları ve Ayırma</span><span class="sxs-lookup"><span data-stu-id="0b785-103">Logic Apps Loops, Scopes, and Debatching</span></span>
  
<span data-ttu-id="0b785-104">Logic Apps, çeşitli yollarla dizilerle, koleksiyonlar, toplu işlemler, iş sağlar ve bir iş akışı içinde döngüye girer.</span><span class="sxs-lookup"><span data-stu-id="0b785-104">Logic Apps provides a number of ways to work with arrays, collections, batches, and loops within a workflow.</span></span>
  
## <a name="foreach-loop-and-arrays"></a><span data-ttu-id="0b785-105">ForEach döngüsü ve diziler</span><span class="sxs-lookup"><span data-stu-id="0b785-105">ForEach loop and arrays</span></span>
  
<span data-ttu-id="0b785-106">Logic Apps, bir veri kümesi üzerinde döngü ve her öğe için bir eylem gerçekleştirmek sağlar.</span><span class="sxs-lookup"><span data-stu-id="0b785-106">Logic Apps allows you to loop over a set of data and perform an action for each item.</span></span>  <span data-ttu-id="0b785-107">Bu aracılığıyla mümkündür `foreach` eylem.</span><span class="sxs-lookup"><span data-stu-id="0b785-107">This is possible via the `foreach` action.</span></span>  <span data-ttu-id="0b785-108">Eklenecek belirtebilirsiniz Tasarımcısı'nda bir her döngü için.</span><span class="sxs-lookup"><span data-stu-id="0b785-108">In the designer, you can specify to add a for each loop.</span></span>  <span data-ttu-id="0b785-109">Üzerinden yinelemek istediğiniz dizi seçtikten sonra Eylemler eklemeye başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0b785-109">After selecting the array you wish to iterate over, you can begin adding actions.</span></span>  <span data-ttu-id="0b785-110">Şu anda foreach döngüsü başına yalnızca bir eylem için sınırlı olur, ancak bu kısıtlama, önümüzdeki haftalarda kaldırılmış.</span><span class="sxs-lookup"><span data-stu-id="0b785-110">Currently you are limited to only one action per foreach loop, but this restriction will be lifted in the coming weeks.</span></span>  <span data-ttu-id="0b785-111">Bir kez döngü içinde dizinin her değerinde gerçekleşmesi gerektiğini belirtmek başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0b785-111">Once within the loop you can begin to specify what should occur at each value of the array.</span></span>

<span data-ttu-id="0b785-112">Kod görünümünü kullanıyorsanız, belirleyebileceğiniz bir aşağıdaki gibi her bir döngü için.</span><span class="sxs-lookup"><span data-stu-id="0b785-112">If using code-view, you can specify a for each loop like below.</span></span>  <span data-ttu-id="0b785-113">Bu örneği olan bir 'microsoft.com' içeren her bir e-posta adresi için bir e-posta gönderir her bir döngü için:</span><span class="sxs-lookup"><span data-stu-id="0b785-113">This is an example of a for each loop that sends an email for each email address that contains 'microsoft.com':</span></span>

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
  
  <span data-ttu-id="0b785-114">A `foreach` Eylem yineleme üzerinden dizi en çok 5000 satır.</span><span class="sxs-lookup"><span data-stu-id="0b785-114">A `foreach` action can iterate over arrays up to 5,000 rows.</span></span>  <span data-ttu-id="0b785-115">Her yineleme paralel olarak varsayılan olarak yürütülür.</span><span class="sxs-lookup"><span data-stu-id="0b785-115">Each iteration will execute in parallel by default.</span></span>  

### <a name="sequential-foreach-loops"></a><span data-ttu-id="0b785-116">Sıralı ForEach döngüsü</span><span class="sxs-lookup"><span data-stu-id="0b785-116">Sequential ForEach loops</span></span>

<span data-ttu-id="0b785-117">Sırayla yürütmek foreach döngüsü etkinleştirmek için `Sequential` işlemi seçeneği eklenir.</span><span class="sxs-lookup"><span data-stu-id="0b785-117">To enable a foreach loop to execute sequentially, the `Sequential` operation option should be added.</span></span>

``` json
"forEach_email": {
        "type": "foreach",
        "foreach": "@body('email_filter')",
        "operationOptions": "Sequential",
        "..."
}
```
  
## <a name="until-loop"></a><span data-ttu-id="0b785-118">Döngü kadar</span><span class="sxs-lookup"><span data-stu-id="0b785-118">Until loop</span></span>
  
  <span data-ttu-id="0b785-119">Bir koşul yerine getirilene kadar bir eylem veya dizi eylem gerçekleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="0b785-119">You can perform an action or series of actions until a condition is met.</span></span>  <span data-ttu-id="0b785-120">Aradığınız yanıt elde edene kadar Bunun en yaygın senaryo bir uç nokta çağırıyor.</span><span class="sxs-lookup"><span data-stu-id="0b785-120">The most common scenario for this is calling an endpoint until you get the response you are looking for.</span></span>  <span data-ttu-id="0b785-121">Eklenecek belirtebilirsiniz Tasarımcısı'nda bir döngü kadar.</span><span class="sxs-lookup"><span data-stu-id="0b785-121">In the designer, you can specify to add an until loop.</span></span>  <span data-ttu-id="0b785-122">Döngü içinde eylemler eklendikten sonra çıkış koşulu olarak döngü ayarlayabileceğiniz sınırlar.</span><span class="sxs-lookup"><span data-stu-id="0b785-122">After adding actions inside the loop, you can set the exit condition, as well as the loop limits.</span></span>  <span data-ttu-id="0b785-123">Döngü döngüleri arasında 1 dakikalık bir gecikmeyle yoktur.</span><span class="sxs-lookup"><span data-stu-id="0b785-123">There is a 1 minute delay between loop cycles.</span></span>
  
  <span data-ttu-id="0b785-124">Kod görünümünü kullanıyorsanız, belirleyebileceğiniz bir döngü ister aşağıda kadar.</span><span class="sxs-lookup"><span data-stu-id="0b785-124">If using code-view, you can specify an until loop like below.</span></span>  <span data-ttu-id="0b785-125">Bu yanıt gövdesi 'Tamamlandı' değerine sahip kadar bir HTTP uç noktası çağrılmadan bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="0b785-125">This is an example of calling an HTTP endpoint until the response body has the value 'Completed'.</span></span>  <span data-ttu-id="0b785-126">Ne zaman tamamlanır ya da</span><span class="sxs-lookup"><span data-stu-id="0b785-126">It will complete when either</span></span> 
  
  * <span data-ttu-id="0b785-127">HTTP yanıtı 'Tamamlandı' durumuna sahip</span><span class="sxs-lookup"><span data-stu-id="0b785-127">HTTP Response has status of 'Completed'</span></span>
  * <span data-ttu-id="0b785-128">1 saat boyunca çalıştı</span><span class="sxs-lookup"><span data-stu-id="0b785-128">It has tried for 1 hour</span></span>
  * <span data-ttu-id="0b785-129">100 kez döngüye</span><span class="sxs-lookup"><span data-stu-id="0b785-129">It has looped 100 times</span></span>
  
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
  
## <a name="spliton-and-debatching"></a><span data-ttu-id="0b785-130">SplitOn ve debatching</span><span class="sxs-lookup"><span data-stu-id="0b785-130">SplitOn and debatching</span></span>

<span data-ttu-id="0b785-131">Bazen bir tetikleyici bir dizi debatch ve bir iş akışı öğesi başına başlatmak istediğiniz öğeleri alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0b785-131">Sometimes a trigger may receive an array of items that you want to debatch and start a workflow per item.</span></span>  <span data-ttu-id="0b785-132">Bu aracılığıyla gerçekleştirilebilir `spliton` komutu.</span><span class="sxs-lookup"><span data-stu-id="0b785-132">This can be accomplished via the `spliton` command.</span></span>  <span data-ttu-id="0b785-133">Varsayılan olarak, tetikleyici swagger bir dizi bir yükü belirtiyorsa, bir `spliton` eklenir ve bir çalışma öğesi başına başlatın.</span><span class="sxs-lookup"><span data-stu-id="0b785-133">By default, if your trigger swagger specifies a payload that is an array, a `spliton` will be added and start a run per item.</span></span>  <span data-ttu-id="0b785-134">SplitOn yalnızca bir tetikleyiciye eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="0b785-134">SplitOn can only be added to a trigger.</span></span>  <span data-ttu-id="0b785-135">Bu el ile yapılandırılabildiğinden veya tanımı kod görünümünde geçersiz kılındı.</span><span class="sxs-lookup"><span data-stu-id="0b785-135">This can be manually configured or overridden in definition code-view.</span></span>  <span data-ttu-id="0b785-136">Şu anda SplitOn debatch en fazla 5000 öğeleri dizi.</span><span class="sxs-lookup"><span data-stu-id="0b785-136">Currently SplitOn can debatch arrays up to 5,000 items.</span></span>  <span data-ttu-id="0b785-137">Sahip olamaz bir `spliton` ve ayrıca zaman uyumlu yanıt desenini uygular.</span><span class="sxs-lookup"><span data-stu-id="0b785-137">You cannot have a `spliton` and also implement the synchronous response pattern.</span></span>  <span data-ttu-id="0b785-138">Adında herhangi bir iş akışının sahip bir `response` ek olarak eylem `spliton` zaman uyumsuz olarak çalışacak ve hemen gönder `202 Accepted` yanıt.</span><span class="sxs-lookup"><span data-stu-id="0b785-138">Any workflow called that has a `response` action in addition to `spliton` will run asynchronously and send an immediate `202 Accepted` response.</span></span>  

<span data-ttu-id="0b785-139">SplitOn kod görünümünde aşağıdaki örnek olarak belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="0b785-139">SplitOn can be specified in code-view as the following example.</span></span>  <span data-ttu-id="0b785-140">Bu öğeleri dizisini alır ve her satırda debatches.</span><span class="sxs-lookup"><span data-stu-id="0b785-140">This receives an array of items and debatches on each row.</span></span>

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

## <a name="scopes"></a><span data-ttu-id="0b785-141">Kapsamları</span><span class="sxs-lookup"><span data-stu-id="0b785-141">Scopes</span></span>

<span data-ttu-id="0b785-142">Bir dizi eylem birlikte bir kapsamı kullanarak Grup mümkündür.</span><span class="sxs-lookup"><span data-stu-id="0b785-142">It is possible to group a series of actions together using a scope.</span></span>  <span data-ttu-id="0b785-143">Özel durum işleme uygulamak için özellikle yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="0b785-143">This is particularly useful for implementing exception handling.</span></span>  <span data-ttu-id="0b785-144">Tasarımcıda yeni bir kapsam ekleyin ve onu içinde herhangi bir eylem eklemeye başlamak.</span><span class="sxs-lookup"><span data-stu-id="0b785-144">In the designer you can add a new scope, and begin adding any actions inside of it.</span></span>  <span data-ttu-id="0b785-145">Aşağıdaki gibi kod görünümünde kapsamları tanımlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0b785-145">You can define scopes in code-view like the following:</span></span>


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