---
title: "aaaError & özel durum işleme - Azure Logic Apps | Microsoft Docs"
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
ms.openlocfilehash: 326a252310c8dfb154e583f91c9421675e448d1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="handle-errors-and-exceptions-in-azure-logic-apps"></a><span data-ttu-id="37f84-103">Hataları ve Azure Logic Apps içinde özel durumları işleme</span><span class="sxs-lookup"><span data-stu-id="37f84-103">Handle errors and exceptions in Azure Logic Apps</span></span>

<span data-ttu-id="37f84-104">Azure mantıksal uygulamaları zengin araçlar sağlar ve desenler toohelp, tümleştirmeler sağlam ve hatalarına karşı dayanıklı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="37f84-104">Azure Logic Apps provides rich tools and patterns toohelp you make sure your integrations are robust and resilient against failures.</span></span> <span data-ttu-id="37f84-105">Herhangi bir tümleştirme mimarideki emin tooappropriately tanıtıcı kapalı kalma süresi yapma hello zorluk oluşturur veya bağımlı sistemlerden verir.</span><span class="sxs-lookup"><span data-stu-id="37f84-105">Any integration architecture poses hello challenge of making sure tooappropriately handle downtime or issues from dependent systems.</span></span> <span data-ttu-id="37f84-106">Logic Apps hataları işleme yapar, vermiş bir ilk sınıf deneyimi hello araçları, iş akışlarında özel durumları ve hataları tooact gerekir.</span><span class="sxs-lookup"><span data-stu-id="37f84-106">Logic Apps makes handling errors a first-class experience, giving you hello tools you need tooact on exceptions and errors in your workflows.</span></span>

## <a name="retry-policies"></a><span data-ttu-id="37f84-107">İlkeleri yeniden deneyin</span><span class="sxs-lookup"><span data-stu-id="37f84-107">Retry policies</span></span>

<span data-ttu-id="37f84-108">Bir yeniden deneme ilkesi hello en temel özel durumu ve hata işleme türüdür.</span><span class="sxs-lookup"><span data-stu-id="37f84-108">A retry policy is hello most basic type of exception and error handling.</span></span> <span data-ttu-id="37f84-109">İlk istek zaman aşımına uğradı ya da başarısız olursa (bir 429 sonuçları herhangi bir istek veya 5xx yanıtı), bu ilkeyi hello eylem yeniden denemeniz gerekir olup olmadığını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="37f84-109">If an initial request timed out or failed (any request that results in a 429 or 5xx response), this policy defines whether hello action should retry.</span></span> <span data-ttu-id="37f84-110">Varsayılan olarak, tüm eylemler 20 saniye aralıklarında 4 ek defa yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="37f84-110">By default, all actions retry 4 additional times over 20-second intervals.</span></span> <span data-ttu-id="37f84-111">Merhaba ilk istek alırsa, bunu bir `500 Internal Server Error` yanıtı hello iş akışı altyapısının duraklatır 20 saniye ve hello isteği yeniden denemeleri.</span><span class="sxs-lookup"><span data-stu-id="37f84-111">So if hello first request receives a `500 Internal Server Error` response, hello workflow engine pauses for 20 seconds, and attempts hello request again.</span></span> <span data-ttu-id="37f84-112">Tüm yeniden denemelerden sonra hello yanıt hala bir özel durum ya da başarısız olması durumunda hello iş akışı devam eder ve işaretleri hello eylem durumu olarak `Failed`.</span><span class="sxs-lookup"><span data-stu-id="37f84-112">If after all retries, hello response is still an exception or failure, hello workflow continues and marks hello action status as `Failed`.</span></span>

<span data-ttu-id="37f84-113">Yeniden deneme ilkelerini hello yapılandırabilirsiniz **girişleri** belirli bir eylem için.</span><span class="sxs-lookup"><span data-stu-id="37f84-113">You can configure retry policies in hello **inputs** for a particular action.</span></span> <span data-ttu-id="37f84-114">Örneğin, bir yeniden deneme ilkesi tootry kadar 4 kez 1 saatlik aralıklarında yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="37f84-114">For example, you can configure a retry policy tootry as many as 4 times over 1-hour intervals.</span></span> <span data-ttu-id="37f84-115">Giriş özellikleri hakkında ayrıntılar için bkz: [iş akışı eylemleri ve Tetikleyicileri][retryPolicyMSDN].</span><span class="sxs-lookup"><span data-stu-id="37f84-115">For full details about input properties, see [Workflow Actions and Triggers][retryPolicyMSDN].</span></span>

```json
"retryPolicy" : {
      "type": "<type-of-retry-policy>",
      "interval": <retry-interval>,
      "count": <number-of-retry-attempts>
    }
```

<span data-ttu-id="37f84-116">HTTP eylem tooretry 4 kez istediğinizi ve her denemesi arasındaki 10 dakika bekleyin, tanımı aşağıdaki hello kullanırsınız:</span><span class="sxs-lookup"><span data-stu-id="37f84-116">If you wanted your HTTP action tooretry 4 times and wait 10 minutes between each attempt, you would use hello following definition:</span></span>

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

<span data-ttu-id="37f84-117">Merhaba desteklenen sözdizimi hakkında daha fazla bilgi için bkz: [iş akışı eylemleri ve Tetikleyicileri yeniden deneme ilkesi bölümüne][retryPolicyMSDN].</span><span class="sxs-lookup"><span data-stu-id="37f84-117">For more information on supported syntax, see hello [retry-policy section in Workflow Actions and Triggers][retryPolicyMSDN].</span></span>

## <a name="catch-failures-with-hello-runafter-property"></a><span data-ttu-id="37f84-118">Merhaba RunAfter özelliği hatalarıyla catch</span><span class="sxs-lookup"><span data-stu-id="37f84-118">Catch failures with hello RunAfter property</span></span>

<span data-ttu-id="37f84-119">Her mantıksal uygulama eylem hangi eylemleri, iş akışınızı hello adımları sıralama gibi hello eylem başlatılmadan önce bitmesi gereken bildirir.</span><span class="sxs-lookup"><span data-stu-id="37f84-119">Each logic app action declares which actions must finish before hello action starts, like ordering hello steps in your workflow.</span></span> <span data-ttu-id="37f84-120">Merhaba eylem tanımı'nda bu sıralama hello adlandırılıyor `runAfter` özelliği.</span><span class="sxs-lookup"><span data-stu-id="37f84-120">In hello action definition, this ordering is known as hello `runAfter` property.</span></span> <span data-ttu-id="37f84-121">Bu özellik, hangi eylemleri ve eylem durumları yürütme hello eylemi açıklayan bir nesnedir.</span><span class="sxs-lookup"><span data-stu-id="37f84-121">This property is an object that describes which actions and action statuses execute hello action.</span></span> <span data-ttu-id="37f84-122">Varsayılan olarak, çok hello mantığı Uygulama Tasarımcısı eklenen tüm eylemleri ayarlamak`runAfter` hello önceki adımı Merhaba, önceki adımda `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="37f84-122">By default, all actions added through hello Logic App Designer are set too`runAfter` hello previous step if hello previous step `Succeeded`.</span></span> <span data-ttu-id="37f84-123">Ancak, önceki eylem olduğunda bu değeri toofire eylemleri özelleştirebilirsiniz `Failed`, `Skipped`, veya bu değerleri olası kümesi.</span><span class="sxs-lookup"><span data-stu-id="37f84-123">However, you can customize this value toofire actions when previous actions have `Failed`, `Skipped`, or a possible set of these values.</span></span> <span data-ttu-id="37f84-124">Bir öğe tooa tooadd istediyseniz sonra belirli bir eylemi Service Bus konu belirlenmiş `Insert_Row` başarısız olursa, aşağıdaki hello kullanabilir `runAfter` yapılandırma:</span><span class="sxs-lookup"><span data-stu-id="37f84-124">If you wanted tooadd an item tooa designated Service Bus topic after a specific action `Insert_Row` fails, you could use hello following `runAfter` configuration:</span></span>

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

<span data-ttu-id="37f84-125">Bildirim hello `runAfter` özellik ayarlanmışsa toofire hello `Insert_Row` eylem `Failed`.</span><span class="sxs-lookup"><span data-stu-id="37f84-125">Notice hello `runAfter` property is set toofire if hello `Insert_Row` action is `Failed`.</span></span> <span data-ttu-id="37f84-126">Merhaba eylem durumu ise toorun hello eylem `Succeeded`, `Failed`, veya `Skipped`, şu sözdizimini kullanın:</span><span class="sxs-lookup"><span data-stu-id="37f84-126">toorun hello action if hello action status is `Succeeded`, `Failed`, or `Skipped`, use this syntax:</span></span>

```json
"runAfter": {
        "Insert_Row": [
            "Failed", "Succeeded", "Skipped"
        ]
    }
```

> [!TIP]
> <span data-ttu-id="37f84-127">Çalıştırın ve önceki bir eylemi başarısız oldu sonra başarıyla tamamlanmış eylemler olarak işaretlenmiş `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="37f84-127">Actions that run and complete successfully after a preceding action has failed, are marked as `Succeeded`.</span></span> <span data-ttu-id="37f84-128">Başarılı bir şekilde catch tüm hataları bir iş akışındaki hello varsa çalışmasına davranışı deyişle olarak işaretlenmiş `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="37f84-128">This behavior means that if you successfully catch all failures in a workflow, hello run itself is marked as `Succeeded`.</span></span>

## <a name="scopes-and-results-tooevaluate-actions"></a><span data-ttu-id="37f84-129">Kapsamlar ve sonuçları tooevaluate Eylemler</span><span class="sxs-lookup"><span data-stu-id="37f84-129">Scopes and results tooevaluate actions</span></span>

<span data-ttu-id="37f84-130">Sonra ayrı Eylemler çalıştırabilir benzer toohow de gruplandırabilirsiniz Eylemler birlikte içinde bir [kapsam](../logic-apps/logic-apps-loops-and-scopes.md), Eylemler mantıksal bir gruplandırması olarak davranır.</span><span class="sxs-lookup"><span data-stu-id="37f84-130">Similar toohow you can run after individual actions, you can also group actions together inside a [scope](../logic-apps/logic-apps-loops-and-scopes.md), which act as a logical grouping of actions.</span></span> <span data-ttu-id="37f84-131">Kapsamları mantıksal uygulama eylemleri düzenlemek için hem bir kapsam hello durumunu toplama değerlendirmesini gerçekleştirmek için faydalıdır.</span><span class="sxs-lookup"><span data-stu-id="37f84-131">Scopes are useful both for organizing your logic app actions, and for performing aggregate evaluations on hello status of a scope.</span></span> <span data-ttu-id="37f84-132">kapsamdaki tüm eylemler bitirdikten sonra hello kapsam kendisini bir durumunu alır.</span><span class="sxs-lookup"><span data-stu-id="37f84-132">hello scope itself receives a status after all actions in a scope have finished.</span></span> <span data-ttu-id="37f84-133">Merhaba kapsamı durumunu hello ile belirlenir aynı ölçüt olarak çalıştır.</span><span class="sxs-lookup"><span data-stu-id="37f84-133">hello scope status is determined with hello same criteria as a run.</span></span> <span data-ttu-id="37f84-134">Merhaba son eylem bir yürütme dal ise `Failed` veya `Aborted`, hello durumu `Failed`.</span><span class="sxs-lookup"><span data-stu-id="37f84-134">If hello final action in an execution branch is `Failed` or `Aborted`, hello status is `Failed`.</span></span>

<span data-ttu-id="37f84-135">kullanabileceğiniz toofire hello kapsamı içinde gerçekleşen hatalar için belirli eylemler, `runAfter` olarak işaretlenmiş bir kapsamla `Failed`.</span><span class="sxs-lookup"><span data-stu-id="37f84-135">toofire specific actions for any failures that happened within hello scope, you can use `runAfter` with a scope that is marked `Failed`.</span></span> <span data-ttu-id="37f84-136">Varsa *herhangi* Eylemler hello kapsamında başarısız, kapsam sağlar başarısız olduktan sonra çalıştıran tek işlem toocatch hataları oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="37f84-136">If *any* actions in hello scope fail, running after a scope fails lets you create a single action toocatch failures.</span></span>

### <a name="getting-hello-context-of-failures-with-results"></a><span data-ttu-id="37f84-137">Sonuçları hatalarıyla Merhaba içeriğine alma</span><span class="sxs-lookup"><span data-stu-id="37f84-137">Getting hello context of failures with results</span></span>

<span data-ttu-id="37f84-138">Bir kapsam hatalarını yakalama yararlı olsa da, bağlam toohelp tam olarak başarısız oldu, hangi eylemlerini anlama ve hatalar veya döndürüldü durum kodları isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="37f84-138">Although catching failures from a scope is useful, you might also want context toohelp you understand exactly which actions failed, and any errors or status codes that were returned.</span></span> <span data-ttu-id="37f84-139">Merhaba `@result()` iş akışı işlevinin kapsamdaki tüm eylemlerin hello sonucu ile ilgili bağlam sağlar.</span><span class="sxs-lookup"><span data-stu-id="37f84-139">hello `@result()` workflow function provides context about hello result of all actions in a scope.</span></span>

<span data-ttu-id="37f84-140">`@result()`tek bir parametre, kapsam adı alır ve tüm hello eylem sonuçlarını, kapsam içinde bir dizi döndürür.</span><span class="sxs-lookup"><span data-stu-id="37f84-140">`@result()` takes a single parameter, scope name, and returns an array of all hello action results from within that scope.</span></span> <span data-ttu-id="37f84-141">Bu eylem nesneleri aynı öznitelikleri hello hello dahil `@actions()` nesne, eylem başlangıç saati, eylem bitiş zamanı, eylem durumu, eylemi girişleri, eylem bağıntı kimlikleri ve eylem dahil olmak üzere çıkarır.</span><span class="sxs-lookup"><span data-stu-id="37f84-141">These action objects include hello same attributes as hello `@actions()` object, including action start time, action end time, action status, action inputs, action correlation IDs, and action outputs.</span></span> <span data-ttu-id="37f84-142">bir kapsamda başarısız herhangi bir eylem bağlamında toosend, siz kolayca eşleştirin bir `@result()` ile işlev bir `runAfter`.</span><span class="sxs-lookup"><span data-stu-id="37f84-142">toosend context of any actions that failed within a scope, you can easily pair an `@result()` function with a `runAfter`.</span></span>

<span data-ttu-id="37f84-143">tooexecute bir eylem *her* kapsamdaki eylem, `Failed`, filtre hello sonuçları tooactions dizi başarısız oldu, eşleştirin `@result()` ile bir  **[filtre dizisi](../connectors/connectors-native-query.md)**  eylem ve  **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)**  döngü.</span><span class="sxs-lookup"><span data-stu-id="37f84-143">tooexecute an action *for each* action in a scope that `Failed`, filter hello array of results tooactions that failed, you can pair `@result()` with a **[Filter Array](../connectors/connectors-native-query.md)** action and a **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)** loop.</span></span> <span data-ttu-id="37f84-144">Merhaba filtrelenmiş Sonuç dizisi alabilir ve hello kullanarak her hatası için bir eylem gerçekleştirmek **ForEach** döngü.</span><span class="sxs-lookup"><span data-stu-id="37f84-144">You can take hello filtered result array and perform an action for each failure using hello **ForEach** loop.</span></span> <span data-ttu-id="37f84-145">Merhaba kapsamında hello yanıt gövdesi başarısız herhangi bir eylem ile HTTP POST isteği gönderir ayrıntılı bir açıklama, ve ardından örneği `My_Scope`.</span><span class="sxs-lookup"><span data-stu-id="37f84-145">Here's an example, followed by a detailed explanation, that sends an HTTP POST request with hello response body of any actions that failed within hello scope `My_Scope`.</span></span>

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

<span data-ttu-id="37f84-146">Neler ayrıntılı kılavuz toodescribe şöyledir:</span><span class="sxs-lookup"><span data-stu-id="37f84-146">Here's a detailed walkthrough toodescribe what happens:</span></span>

1. <span data-ttu-id="37f84-147">içinde tüm eylemler tooget hello sonucu `My_Scope`, hello **filtre dizisi** eylem filtrelerini `@result('My_Scope')`.</span><span class="sxs-lookup"><span data-stu-id="37f84-147">tooget hello result of all actions within `My_Scope`, hello **Filter Array** action filters `@result('My_Scope')`.</span></span>

2. <span data-ttu-id="37f84-148">Merhaba için koşul **filtre dizisi** herhangi `@result()` çok durum eşit olan öğe`Failed`.</span><span class="sxs-lookup"><span data-stu-id="37f84-148">hello condition for **Filter Array** is any `@result()` item that has status equal too`Failed`.</span></span> <span data-ttu-id="37f84-149">Bu durum tüm eylem sonuçlarını hello diziyle filtreler `My_Scope` yalnızca tooan diziyle eylem sonuçlarını başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="37f84-149">This condition filters hello array with all action results from `My_Scope` tooan array with only failed action results.</span></span>

3. <span data-ttu-id="37f84-150">Gerçekleştirmek bir **her** hello eylemini **filtre dizi** çıkarır.</span><span class="sxs-lookup"><span data-stu-id="37f84-150">Perform a **For Each** action on hello **Filtered Array** outputs.</span></span> <span data-ttu-id="37f84-151">Bu adım bir eylem gerçekleştirir *her* önceden filtre eylem sonucu başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="37f84-151">This step performs an action *for each* failed action result that was previously filtered.</span></span>

    <span data-ttu-id="37f84-152">Merhaba kapsamında tek bir eylem başarısız olursa hello Eylemler hello `foreach` yalnızca bir kez çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="37f84-152">If a single action in hello scope failed, hello actions in hello `foreach` run only once.</span></span> 
    <span data-ttu-id="37f84-153">Çok sayıda başarısız Eylemler hatası başına tek bir eylem neden olur.</span><span class="sxs-lookup"><span data-stu-id="37f84-153">Many failed actions cause one action per failure.</span></span>

4. <span data-ttu-id="37f84-154">Bir HTTP POST hello üzerinde Gönder `foreach` öğesi yanıt gövdesi veya `@item()['outputs']['body']`.</span><span class="sxs-lookup"><span data-stu-id="37f84-154">Send an HTTP POST on hello `foreach` item response body, or `@item()['outputs']['body']`.</span></span> <span data-ttu-id="37f84-155">Merhaba `@result()` öğesi şekli olan hello aynı hello `@actions()` şekil ve ayrıştırılabilir aynı hello yolu.</span><span class="sxs-lookup"><span data-stu-id="37f84-155">hello `@result()` item shape is hello same as hello `@actions()` shape, and can be parsed hello same way.</span></span>

5. <span data-ttu-id="37f84-156">Hello başarısız Eylem adına sahip iki özel üstbilgi dahil `@item()['name']` ve hello başarısız oldu, izleme kimliği çalışma istemci `@item()['clientTrackingId']`.</span><span class="sxs-lookup"><span data-stu-id="37f84-156">Include two custom headers with hello failed action name `@item()['name']` and hello failed run client tracking ID `@item()['clientTrackingId']`.</span></span>

<span data-ttu-id="37f84-157">Başvuru için tek bir örneği burada verilmiştir `@result()` hello gösteren öğesi `name`, `body`, ve `clientTrackingId` hello önceki örnekte Ayrıştırılan özellikleri.</span><span class="sxs-lookup"><span data-stu-id="37f84-157">For reference, here's an example of a single `@result()` item, showing hello `name`, `body`, and `clientTrackingId` properties that are parsed in hello previous example.</span></span> <span data-ttu-id="37f84-158">Dışında bir `foreach`, `@result()` bu nesneleri içeren bir dizi döndürür.</span><span class="sxs-lookup"><span data-stu-id="37f84-158">Outside of a `foreach`, `@result()` returns an array of these objects.</span></span>

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

<span data-ttu-id="37f84-159">tooperform farklı özel durum işleme desenleri, daha önce gösterilen hello ifadeleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="37f84-159">tooperform different exception handling patterns, you can use hello expressions shown previously.</span></span> <span data-ttu-id="37f84-160">Tek özel durum eylemin hello tüm filtrelenmiş dizisi hataları kabul hello kapsamı dışında işleme tooexecute seçin ve hello kaldırmak `foreach`.</span><span class="sxs-lookup"><span data-stu-id="37f84-160">You might choose tooexecute a single exception handling action outside hello scope that accepts hello entire filtered array of failures, and remove hello `foreach`.</span></span> <span data-ttu-id="37f84-161">Merhaba yararlı olan diğer özellikleri de içerebilir `@result()` daha önce gösterilen yanıt.</span><span class="sxs-lookup"><span data-stu-id="37f84-161">You can also include other useful properties from hello `@result()` response shown previously.</span></span>

## <a name="azure-diagnostics-and-telemetry"></a><span data-ttu-id="37f84-162">Azure tanılama ve telemetri</span><span class="sxs-lookup"><span data-stu-id="37f84-162">Azure Diagnostics and telemetry</span></span>

<span data-ttu-id="37f84-163">Merhaba önceki desenleri mükemmel şekilde toohandle hataları ve özel durumları çalışması içinde alır, ancak ayrıca tanımlamak ve tooerrors çalışmasına Merhaba bağımsız yanıt.</span><span class="sxs-lookup"><span data-stu-id="37f84-163">hello previous patterns are great way toohandle errors and exceptions within a run, but you can also identify and respond tooerrors independent of hello run itself.</span></span> 
<span data-ttu-id="37f84-164">[Azure tanılama](../logic-apps/logic-apps-monitor-your-logic-apps.md) tüm iş akışı (tüm çalışma ve eylem durumları dahil) olayları tooan Azure Storage hesabı veya bir Azure olay hub'ı basit yol toosend sağlar.</span><span class="sxs-lookup"><span data-stu-id="37f84-164">[Azure Diagnostics](../logic-apps/logic-apps-monitor-your-logic-apps.md) provides a simple way toosend all workflow events (including all run and action statuses) tooan Azure Storage account or an Azure Event Hub.</span></span> <span data-ttu-id="37f84-165">tooevaluate çalıştırma durumları, hello günlüklerini ve ölçümleri izleyin veya tercih ettiğiniz izleme aracı yayımlama.</span><span class="sxs-lookup"><span data-stu-id="37f84-165">tooevaluate run statuses, you can monitor hello logs and metrics, or publish them into any monitoring tool you prefer.</span></span> <span data-ttu-id="37f84-166">Bir olası seçenektir toostream Azure Event Hub'ına aracılığıyla tüm hello olaylarını [Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="37f84-166">One potential option is toostream all hello events through Azure Event Hub into [Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span></span> <span data-ttu-id="37f84-167">Stream Analytics içinde herhangi bir anormallikleri, ortalama veya hataları kapalı dinamik sorgular hello tanılama günlüklerini yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="37f84-167">In Stream Analytics, you can write live queries off any anomalies, averages, or failures from hello diagnostic logs.</span></span> <span data-ttu-id="37f84-168">Akış analizi kuyruklar, konular, SQL, Azure Cosmos DB ve Power BI gibi tooother veri kaynaklarını kolayca çıkarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="37f84-168">Stream Analytics can easily output tooother data sources like queues, topics, SQL, Azure Cosmos DB, and Power BI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="37f84-169">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="37f84-169">Next Steps</span></span>

* [<span data-ttu-id="37f84-170">Bir müşteri hata işleme Azure Logic Apps ile nasıl derler bakın</span><span class="sxs-lookup"><span data-stu-id="37f84-170">See how a customer builds error handling with Azure Logic Apps</span></span>](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
* [<span data-ttu-id="37f84-171">Daha fazla Logic Apps örnekleri ve senaryoları Bul</span><span class="sxs-lookup"><span data-stu-id="37f84-171">Find more Logic Apps examples and scenarios</span></span>](../logic-apps/logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="37f84-172">Nasıl toocreate dağıtımları mantıksal uygulamalar için otomatik öğrenin</span><span class="sxs-lookup"><span data-stu-id="37f84-172">Learn how toocreate automated deployments for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
* [<span data-ttu-id="37f84-173">Visual Studio ile mantıksal uygulamalar oluşturma ve dağıtma</span><span class="sxs-lookup"><span data-stu-id="37f84-173">Build and deploy logic apps with Visual Studio</span></span>](logic-apps-deploy-from-vs.md)

<!-- References -->
[retryPolicyMSDN]: https://docs.microsoft.com/rest/api/logic/actions-and-triggers#Anchor_9
