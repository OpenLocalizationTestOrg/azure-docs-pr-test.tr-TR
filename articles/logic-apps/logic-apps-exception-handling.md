---
title: "Hata & özel durum işleme - Azure Logic Apps | Microsoft Docs"
description: "Hata ve özel durum işleme Azure Logic Apps içinde desenleri"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: e50ab2f2-1fdc-4d2a-be40-995a6cc5a0d4
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 9af2f71b3d288cc6f4e271d0915545d43a1249bc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="handle-errors-and-exceptions-in-azure-logic-apps"></a><span data-ttu-id="3d1d6-103">Hataları ve Azure Logic Apps içinde özel durumları işleme</span><span class="sxs-lookup"><span data-stu-id="3d1d6-103">Handle errors and exceptions in Azure Logic Apps</span></span>

<span data-ttu-id="3d1d6-104">Desenler, tümleştirmeler emin olun yardımcı olmak için güçlü ve hatalarına karşı dayanıklı ve Azure mantıksal uygulamaları zengin araçlar sağlar.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-104">Azure Logic Apps provides rich tools and patterns to help you make sure your integrations are robust and resilient against failures.</span></span> <span data-ttu-id="3d1d6-105">Herhangi bir tümleştirme mimarideki kesinti süresi veya bağımlı sistemleri sorunlarını uygun şekilde işlemek üzere emin yapma zorluk oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-105">Any integration architecture poses the challenge of making sure to appropriately handle downtime or issues from dependent systems.</span></span> <span data-ttu-id="3d1d6-106">Logic Apps, iş akışlarınızı hataları ve özel durumları hareket için ihtiyacınız olan araçları vermiş birinci sınıf bir deneyim hataları işleme yapar.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-106">Logic Apps makes handling errors a first-class experience, giving you the tools you need to act on exceptions and errors in your workflows.</span></span>

## <a name="retry-policies"></a><span data-ttu-id="3d1d6-107">İlkeleri yeniden deneyin</span><span class="sxs-lookup"><span data-stu-id="3d1d6-107">Retry policies</span></span>

<span data-ttu-id="3d1d6-108">Bir yeniden deneme ilkesi özel durumu ve hata işleme en temel türüdür.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-108">A retry policy is the most basic type of exception and error handling.</span></span> <span data-ttu-id="3d1d6-109">İlk istek zaman aşımına uğradı ya da başarısız olursa (bir 429 sonuçları herhangi bir istek veya 5xx yanıtı), bu ilkeyi eylemi yeniden denemeniz gerekir olup olmadığını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-109">If an initial request timed out or failed (any request that results in a 429 or 5xx response), this policy defines whether the action should retry.</span></span> <span data-ttu-id="3d1d6-110">Varsayılan olarak, tüm eylemler 20 saniye aralıklarında 4 ek defa yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-110">By default, all actions retry 4 additional times over 20-second intervals.</span></span> <span data-ttu-id="3d1d6-111">İlk istek alırsa, bunu bir `500 Internal Server Error` yanıt, iş akışı altyapısının duraklatır 20 saniye ve isteği yeniden dener.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-111">So if the first request receives a `500 Internal Server Error` response, the workflow engine pauses for 20 seconds, and attempts the request again.</span></span> <span data-ttu-id="3d1d6-112">Tüm yeniden denemeler yapıldıktan sonra yanıt hala bir özel durum ya da hata ise, iş akışı devam eder ve eylem durumu olarak işaretler `Failed`.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-112">If after all retries, the response is still an exception or failure, the workflow continues and marks the action status as `Failed`.</span></span>

<span data-ttu-id="3d1d6-113">Yeniden deneme ilkelerini yapılandırabilirsiniz **girişleri** belirli bir eylem için.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-113">You can configure retry policies in the **inputs** for a particular action.</span></span> <span data-ttu-id="3d1d6-114">Örneğin, 1 saat aralıklarında olarak en fazla 4 kez denemek için bir yeniden deneme ilkesi yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-114">For example, you can configure a retry policy to try as many as 4 times over 1-hour intervals.</span></span> <span data-ttu-id="3d1d6-115">Giriş özellikleri hakkında ayrıntılar için bkz: [iş akışı eylemleri ve Tetikleyicileri][retryPolicyMSDN].</span><span class="sxs-lookup"><span data-stu-id="3d1d6-115">For full details about input properties, see [Workflow Actions and Triggers][retryPolicyMSDN].</span></span>

```json
"retryPolicy" : {
      "type": "<type-of-retry-policy>",
      "interval": <retry-interval>,
      "count": <number-of-retry-attempts>
    }
```

<span data-ttu-id="3d1d6-116">4 kez yeniden deneyin ve her denemesi arasındaki 10 dakika bekleyin, HTTP eylemi istediyseniz, aşağıdaki tanımını kullanırsınız:</span><span class="sxs-lookup"><span data-stu-id="3d1d6-116">If you wanted your HTTP action to retry 4 times and wait 10 minutes between each attempt, you would use the following definition:</span></span>

```json
"HTTP": 
{
    "inputs": {
        "method": "GET",
        "uri": "http://myAPIendpoint/api/action",
        "retryPolicy" : {
            "type": "fixed",
            "interval": "PT10M",
            "count": 4
        }
    },
    "runAfter": {},
    "type": "Http"
}
```

<span data-ttu-id="3d1d6-117">Desteklenen sözdizimi hakkında daha fazla bilgi için bkz: [iş akışı eylemleri ve Tetikleyicileri yeniden deneme ilkesi bölümüne][retryPolicyMSDN].</span><span class="sxs-lookup"><span data-stu-id="3d1d6-117">For more information on supported syntax, see the [retry-policy section in Workflow Actions and Triggers][retryPolicyMSDN].</span></span>

## <a name="catch-failures-with-the-runafter-property"></a><span data-ttu-id="3d1d6-118">RunAfter özelliğiyle hatalarını yakalama</span><span class="sxs-lookup"><span data-stu-id="3d1d6-118">Catch failures with the RunAfter property</span></span>

<span data-ttu-id="3d1d6-119">Her mantıksal uygulama eylem hangi eylemleri iş akışınızda adımları sıralama gibi eylem başlamadan önce bitmesi gereken bildirir.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-119">Each logic app action declares which actions must finish before the action starts, like ordering the steps in your workflow.</span></span> <span data-ttu-id="3d1d6-120">Eylem tanımı'nda bu sıralama olarak bilinir `runAfter` özelliği.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-120">In the action definition, this ordering is known as the `runAfter` property.</span></span> <span data-ttu-id="3d1d6-121">Bu özellik, hangi eylemleri ve eylem durumları yürütme eylemi açıklayan bir nesnedir.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-121">This property is an object that describes which actions and action statuses execute the action.</span></span> <span data-ttu-id="3d1d6-122">Varsayılan olarak, mantıksal Uygulama Tasarımcısı eklenen tüm eylemleri ayarlamak `runAfter` önceki adımda, önceki adımda `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-122">By default, all actions added through the Logic App Designer are set to `runAfter` the previous step if the previous step `Succeeded`.</span></span> <span data-ttu-id="3d1d6-123">Bununla birlikte, bu değer, önceki eylem olduğunda Eylemler tetiklenecek özelleştirebilirsiniz `Failed`, `Skipped`, veya bu değerleri olası kümesi.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-123">However, you can customize this value to fire actions when previous actions have `Failed`, `Skipped`, or a possible set of these values.</span></span> <span data-ttu-id="3d1d6-124">Öğeyi sonra belirli bir eylemi atanmış bir Service Bus konu başlığına eklemek istiyorsanız `Insert_Row` başarısız olursa aşağıdakileri kullanabilirsiniz `runAfter` yapılandırma:</span><span class="sxs-lookup"><span data-stu-id="3d1d6-124">If you wanted to add an item to a designated Service Bus topic after a specific action `Insert_Row` fails, you could use the following `runAfter` configuration:</span></span>

```json
"Send_message": {
    "inputs": {
        "body": {
            "ContentData": "@{encodeBase64(body('Insert_Row'))}",
            "ContentType": "{ \"content-type\" : \"application/json\" }"
        },
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-westus.azure-apim.net/apim/servicebus"
            },
            "connection": {
                "name": "@parameters('$connections')['servicebus']['connectionId']"
            }
        },
        "method": "post",
        "path": "/@{encodeURIComponent('failures')}/messages"
    },
    "runAfter": {
        "Insert_Row": [
            "Failed"
        ]
    }
}
```

<span data-ttu-id="3d1d6-125">Bildirim `runAfter` özelliği ayarlanmış olursa tetiklenecek `Insert_Row` eylem `Failed`.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-125">Notice the `runAfter` property is set to fire if the `Insert_Row` action is `Failed`.</span></span> <span data-ttu-id="3d1d6-126">Eylem durumu ise eylemi çalıştırmak için `Succeeded`, `Failed`, veya `Skipped`, şu sözdizimini kullanın:</span><span class="sxs-lookup"><span data-stu-id="3d1d6-126">To run the action if the action status is `Succeeded`, `Failed`, or `Skipped`, use this syntax:</span></span>

```json
"runAfter": {
        "Insert_Row": [
            "Failed", "Succeeded", "Skipped"
        ]
    }
```

> [!TIP]
> <span data-ttu-id="3d1d6-127">Çalıştırın ve önceki bir eylemi başarısız oldu sonra başarıyla tamamlanmış eylemler olarak işaretlenmiş `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-127">Actions that run and complete successfully after a preceding action has failed, are marked as `Succeeded`.</span></span> <span data-ttu-id="3d1d6-128">Bir iş akışını çalıştırma başarıyla catch tüm hatalar olarak işaretlenmişse, yani bu davranış `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-128">This behavior means that if you successfully catch all failures in a workflow, the run itself is marked as `Succeeded`.</span></span>

## <a name="scopes-and-results-to-evaluate-actions"></a><span data-ttu-id="3d1d6-129">Kapsamlar ve sonuçları Eylemler değerlendirmek için</span><span class="sxs-lookup"><span data-stu-id="3d1d6-129">Scopes and results to evaluate actions</span></span>

<span data-ttu-id="3d1d6-130">Nasıl çalıştırabileceğiniz benzer ayrı Eylemler sonra aynı zamanda Eylemler içinde gruplayabilirsiniz bir [kapsam](../logic-apps/logic-apps-loops-and-scopes.md), Eylemler mantıksal bir gruplandırması olarak davranır.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-130">Similar to how you can run after individual actions, you can also group actions together inside a [scope](../logic-apps/logic-apps-loops-and-scopes.md), which act as a logical grouping of actions.</span></span> <span data-ttu-id="3d1d6-131">Kapsamları mantıksal uygulama eylemleri düzenlemek için hem bir kapsamın durumu toplama değerlendirmesini gerçekleştirmek için faydalıdır.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-131">Scopes are useful both for organizing your logic app actions, and for performing aggregate evaluations on the status of a scope.</span></span> <span data-ttu-id="3d1d6-132">Kapsamdaki tüm eylemler bitirdikten sonra kapsam bir durumunu alır.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-132">The scope itself receives a status after all actions in a scope have finished.</span></span> <span data-ttu-id="3d1d6-133">Kapsam durumu Çalıştır aynı ölçütüne ile belirlenir.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-133">The scope status is determined with the same criteria as a run.</span></span> <span data-ttu-id="3d1d6-134">Son eylem bir yürütme dal ise `Failed` veya `Aborted`, durum `Failed`.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-134">If the final action in an execution branch is `Failed` or `Aborted`, the status is `Failed`.</span></span>

<span data-ttu-id="3d1d6-135">Kapsam içinde gerçekleşen hatalar için belirli eylemleri yangın için kullanabileceğiniz `runAfter` olarak işaretlenmiş bir kapsamla `Failed`.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-135">To fire specific actions for any failures that happened within the scope, you can use `runAfter` with a scope that is marked `Failed`.</span></span> <span data-ttu-id="3d1d6-136">Varsa *herhangi* Eylemler kapsamında başarısız, kapsam sağlar başarısız olduktan sonra çalışan hataları yakalamak için tek bir eylem oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-136">If *any* actions in the scope fail, running after a scope fails lets you create a single action to catch failures.</span></span>

### <a name="getting-the-context-of-failures-with-results"></a><span data-ttu-id="3d1d6-137">Sonuçları hatalarıyla bağlamı alma</span><span class="sxs-lookup"><span data-stu-id="3d1d6-137">Getting the context of failures with results</span></span>

<span data-ttu-id="3d1d6-138">Bir kapsam hatalarını yakalama yararlı olsa da, tam olarak başarısız oldu, hangi eylemleri ve hatalar veya döndürüldü durum kodları anlamanıza yardımcı olması için bağlamı da isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-138">Although catching failures from a scope is useful, you might also want context to help you understand exactly which actions failed, and any errors or status codes that were returned.</span></span> <span data-ttu-id="3d1d6-139">`@result()` İş akışı işlevinin kapsamdaki tüm eylemlerin sonucu ile ilgili bağlam sağlar.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-139">The `@result()` workflow function provides context about the result of all actions in a scope.</span></span>

<span data-ttu-id="3d1d6-140">`@result()`tek bir parametre, kapsam adı alır ve tüm eylem sonuçlarını, kapsam içinde bir dizi döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-140">`@result()` takes a single parameter, scope name, and returns an array of all the action results from within that scope.</span></span> <span data-ttu-id="3d1d6-141">Bu eylem nesneleri aynı özniteliklere dahil `@actions()` nesne, eylem başlangıç saati, eylem bitiş zamanı, eylem durumu, eylemi girişleri, eylem bağıntı kimlikleri ve eylem dahil olmak üzere çıkarır.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-141">These action objects include the same attributes as the `@actions()` object, including action start time, action end time, action status, action inputs, action correlation IDs, and action outputs.</span></span> <span data-ttu-id="3d1d6-142">Bir kapsamda başarısız herhangi bir eylem bağlamı göndermek için kolayca eşleştirilebileceği bir `@result()` ile işlev bir `runAfter`.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-142">To send context of any actions that failed within a scope, you can easily pair an `@result()` function with a `runAfter`.</span></span>

<span data-ttu-id="3d1d6-143">Bir eylem yürütmek için *her* kapsamdaki eylem, `Failed`, başarısız olan eylemler için sonuçları dizisi filtre, eşleştirin `@result()` ile bir  **[filtre dizisi](../connectors/connectors-native-query.md)**  eylem ve  **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)**  döngü.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-143">To execute an action *for each* action in a scope that `Failed`, filter the array of results to actions that failed, you can pair `@result()` with a **[Filter Array](../connectors/connectors-native-query.md)** action and a **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)** loop.</span></span> <span data-ttu-id="3d1d6-144">Filtrelenmiş Sonuç dizisi alabilir ve her hata kullanmak için bir eylem gerçekleştirmek **ForEach** döngü.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-144">You can take the filtered result array and perform an action for each failure using the **ForEach** loop.</span></span> <span data-ttu-id="3d1d6-145">Kapsam içinde başarısız oldu herhangi bir eylem yanıt gövdesi ile HTTP POST isteği gönderir ayrıntılı bir açıklama, ve ardından örneği `My_Scope`.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-145">Here's an example, followed by a detailed explanation, that sends an HTTP POST request with the response body of any actions that failed within the scope `My_Scope`.</span></span>

```json
"Filter_array": {
    "inputs": {
        "from": "@result('My_Scope')",
        "where": "@equals(item()['status'], 'Failed')"
    },
    "runAfter": {
        "My_Scope": [
            "Failed"
        ]
    },
    "type": "Query"
},
"For_each": {
    "actions": {
        "Log_Exception": {
            "inputs": {
                "body": "@item()['outputs']['body']",
                "method": "POST",
                "headers": {
                    "x-failed-action-name": "@item()['name']",
                    "x-failed-tracking-id": "@item()['clientTrackingId']"
                },
                "uri": "http://requestb.in/"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "foreach": "@body('Filter_array')",
    "runAfter": {
        "Filter_array": [
            "Succeeded"
        ]
    },
    "type": "Foreach"
}
```

<span data-ttu-id="3d1d6-146">Ne olacağını açıklamak için ayrıntılı bir kılavuz şöyledir:</span><span class="sxs-lookup"><span data-stu-id="3d1d6-146">Here's a detailed walkthrough to describe what happens:</span></span>

1. <span data-ttu-id="3d1d6-147">Tüm eylemlerin sonucu elde etmek için `My_Scope`, **filtre dizisi** eylem filtrelerini `@result('My_Scope')`.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-147">To get the result of all actions within `My_Scope`, the **Filter Array** action filters `@result('My_Scope')`.</span></span>

2. <span data-ttu-id="3d1d6-148">Koşul için **filtre dizisi** herhangi `@result()` Durum eşit olan öğe `Failed`.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-148">The condition for **Filter Array** is any `@result()` item that has status equal to `Failed`.</span></span> <span data-ttu-id="3d1d6-149">Bu durum tüm eylem sonuçlarını diziyle filtreler `My_Scope` sahip bir dizi yalnızca eylem sonuçlarını başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-149">This condition filters the array with all action results from `My_Scope` to an array with only failed action results.</span></span>

3. <span data-ttu-id="3d1d6-150">Gerçekleştirmek bir **her** eylemini **filtre dizi** çıkarır.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-150">Perform a **For Each** action on the **Filtered Array** outputs.</span></span> <span data-ttu-id="3d1d6-151">Bu adım bir eylem gerçekleştirir *her* önceden filtre eylem sonucu başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-151">This step performs an action *for each* failed action result that was previously filtered.</span></span>

    <span data-ttu-id="3d1d6-152">Kapsam içinde tek bir eylem başarısız olduysa, Eylemler `foreach` yalnızca bir kez çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-152">If a single action in the scope failed, the actions in the `foreach` run only once.</span></span> 
    <span data-ttu-id="3d1d6-153">Çok sayıda başarısız Eylemler hatası başına tek bir eylem neden olur.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-153">Many failed actions cause one action per failure.</span></span>

4. <span data-ttu-id="3d1d6-154">Bir HTTP POST gönderme `foreach` öğesi yanıt gövdesi veya `@item()['outputs']['body']`.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-154">Send an HTTP POST on the `foreach` item response body, or `@item()['outputs']['body']`.</span></span> <span data-ttu-id="3d1d6-155">`@result()` Öğesi şekli aynı olup `@actions()` şekil ve aynı şekilde ayrıştırılır.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-155">The `@result()` item shape is the same as the `@actions()` shape, and can be parsed the same way.</span></span>

5. <span data-ttu-id="3d1d6-156">Başarısız eylem adı ile iki özel üstbilgileri dahil `@item()['name']` çalıştırıp başarısız istemci izleme kimliği `@item()['clientTrackingId']`.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-156">Include two custom headers with the failed action name `@item()['name']` and the failed run client tracking ID `@item()['clientTrackingId']`.</span></span>

<span data-ttu-id="3d1d6-157">Başvuru için tek bir örneği burada verilmiştir `@result()` öğesi, gösteren `name`, `body`, ve `clientTrackingId` önceki örnekte Ayrıştırılan özellikleri.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-157">For reference, here's an example of a single `@result()` item, showing the `name`, `body`, and `clientTrackingId` properties that are parsed in the previous example.</span></span> <span data-ttu-id="3d1d6-158">Dışında bir `foreach`, `@result()` bu nesneleri içeren bir dizi döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-158">Outside of a `foreach`, `@result()` returns an array of these objects.</span></span>

```json
{
    "name": "Example_Action_That_Failed",
    "inputs": {
        "uri": "https://myfailedaction.azurewebsites.net",
        "method": "POST"
    },
    "outputs": {
        "statusCode": 404,
        "headers": {
            "Date": "Thu, 11 Aug 2016 03:18:18 GMT",
            "Server": "Microsoft-IIS/8.0",
            "X-Powered-By": "ASP.NET",
            "Content-Length": "68",
            "Content-Type": "application/json"
        },
        "body": {
            "code": "ResourceNotFound",
            "message": "/docs/folder-name/resource-name does not exist"
        }
    },
    "startTime": "2016-08-11T03:18:19.7755341Z",
    "endTime": "2016-08-11T03:18:20.2598835Z",
    "trackingId": "bdd82e28-ba2c-4160-a700-e3a8f1a38e22",
    "clientTrackingId": "08587307213861835591296330354",
    "code": "NotFound",
    "status": "Failed"
}
```

<span data-ttu-id="3d1d6-159">Farklı özel durum desenleri işleme gerçekleştirmek için daha önce gösterilen ifadeleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-159">To perform different exception handling patterns, you can use the expressions shown previously.</span></span> <span data-ttu-id="3d1d6-160">Tek özel durum hataları tüm filtrelenmiş dizisi kabul kapsamı dışında eylem işleme yürütülecek seçin ve Kaldır `foreach`.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-160">You might choose to execute a single exception handling action outside the scope that accepts the entire filtered array of failures, and remove the `foreach`.</span></span> <span data-ttu-id="3d1d6-161">Diğer yararlı olan özellikleri de içerebilir `@result()` daha önce gösterilen yanıt.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-161">You can also include other useful properties from the `@result()` response shown previously.</span></span>

## <a name="azure-diagnostics-and-telemetry"></a><span data-ttu-id="3d1d6-162">Azure tanılama ve telemetri</span><span class="sxs-lookup"><span data-stu-id="3d1d6-162">Azure Diagnostics and telemetry</span></span>

<span data-ttu-id="3d1d6-163">Önceki desenleri şekilde hataları ve çalışması içinde özel durumları işlemek harika, ancak aynı zamanda tanımlamak ve hataları yürütülmesi bağımsız yanıt.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-163">The previous patterns are great way to handle errors and exceptions within a run, but you can also identify and respond to errors independent of the run itself.</span></span> 
<span data-ttu-id="3d1d6-164">[Azure tanılama](../logic-apps/logic-apps-monitor-your-logic-apps.md) bir Azure Storage hesabı veya bir Azure olay hub'ı (tüm çalışma ve eylem durumları dahil) tüm iş akışı olayları göndermek için basit bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-164">[Azure Diagnostics](../logic-apps/logic-apps-monitor-your-logic-apps.md) provides a simple way to send all workflow events (including all run and action statuses) to an Azure Storage account or an Azure Event Hub.</span></span> <span data-ttu-id="3d1d6-165">Çalışma durumlarını değerlendirmek için günlükleri ve ölçümleri izleyin veya tercih ettiğiniz izleme aracı yayımlama.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-165">To evaluate run statuses, you can monitor the logs and metrics, or publish them into any monitoring tool you prefer.</span></span> <span data-ttu-id="3d1d6-166">Olası bir seçenek olan Azure Event Hub'ına aracılığıyla tüm olayları akışını sağlamak için [Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="3d1d6-166">One potential option is to stream all the events through Azure Event Hub into [Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span></span> <span data-ttu-id="3d1d6-167">Stream Analytics içinde herhangi bir anormallikleri, ortalama veya hataları kapalı dinamik sorgular tanılama günlükleri yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-167">In Stream Analytics, you can write live queries off any anomalies, averages, or failures from the diagnostic logs.</span></span> <span data-ttu-id="3d1d6-168">Akış analizi, kuyruklar, konular, SQL, Azure Cosmos DB ve Power BI gibi diğer veri kaynakları için kolayca çıkarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3d1d6-168">Stream Analytics can easily output to other data sources like queues, topics, SQL, Azure Cosmos DB, and Power BI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d1d6-169">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="3d1d6-169">Next Steps</span></span>

* [<span data-ttu-id="3d1d6-170">Bir müşteri hata işleme Azure Logic Apps ile nasıl derler bakın</span><span class="sxs-lookup"><span data-stu-id="3d1d6-170">See how a customer builds error handling with Azure Logic Apps</span></span>](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
* [<span data-ttu-id="3d1d6-171">Daha fazla Logic Apps örnekleri ve senaryoları Bul</span><span class="sxs-lookup"><span data-stu-id="3d1d6-171">Find more Logic Apps examples and scenarios</span></span>](../logic-apps/logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="3d1d6-172">Mantıksal uygulamalar için otomatik dağıtımları oluşturmayı öğrenin</span><span class="sxs-lookup"><span data-stu-id="3d1d6-172">Learn how to create automated deployments for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
* [<span data-ttu-id="3d1d6-173">Visual Studio ile mantıksal uygulamalar oluşturma ve dağıtma</span><span class="sxs-lookup"><span data-stu-id="3d1d6-173">Build and deploy logic apps with Visual Studio</span></span>](logic-apps-deploy-from-vs.md)

<!-- References -->
[retryPolicyMSDN]: https://docs.microsoft.com/rest/api/logic/actions-and-triggers#Anchor_9
