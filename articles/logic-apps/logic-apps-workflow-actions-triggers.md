---
title: aaaWorkflow eylemleri ve Tetikleyicileri - Azure Logic Apps | Microsoft Docs
description: 
services: logic-apps
author: MandiOhlinger
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 86a53bb3-01ba-4e83-89b7-c9a7074cb159
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 11/17/2016
ms.author: LADocs; mandia
ms.openlocfilehash: 857927b7d7df3fc9cdc4931ffdb613efde0db9f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="workflow-actions-and-triggers-for-azure-logic-apps"></a><span data-ttu-id="f0cdf-102">İş akışı eylemleri ve Azure Logic Apps için Tetikleyiciler</span><span class="sxs-lookup"><span data-stu-id="f0cdf-102">Workflow actions and triggers for Azure Logic Apps</span></span>

<span data-ttu-id="f0cdf-103">Logic apps tetikleyiciler ve Eylemler oluşur.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-103">Logic apps consist of triggers and actions.</span></span> <span data-ttu-id="f0cdf-104">Tetikleyiciler altı tür vardır.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-104">There are six types of triggers.</span></span> <span data-ttu-id="f0cdf-105">Her tür farklı arabirimi ve farklı bir davranışı vardır.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-105">Each type has different interface and different behavior.</span></span> <span data-ttu-id="f0cdf-106">Merhaba hello ayrıntılarını bakarak ilgili diğer ayrıntıları öğrenebilirsiniz [iş akışı tanımlama dili](logic-apps-workflow-definition-language.md).</span><span class="sxs-lookup"><span data-stu-id="f0cdf-106">You can also learn about other details by looking at hello details of hello [Workflow Definition Language](logic-apps-workflow-definition-language.md).</span></span>  
  
<span data-ttu-id="f0cdf-107">Toolearn tetikleyiciler ve Eylemler ve nasıl bunları toobuild logic apps tooimprove kullanabilir hakkında daha fazla iş süreçlerini ve iş akışları okumaya devam edin.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-107">Read on toolearn more about triggers and actions and how you might use them toobuild logic apps tooimprove your business processes and workflows.</span></span>  
  
### <a name="triggers"></a><span data-ttu-id="f0cdf-108">Tetikleyiciler</span><span class="sxs-lookup"><span data-stu-id="f0cdf-108">Triggers</span></span>  

<span data-ttu-id="f0cdf-109">Tetikleyicinin mantığını uygulama akışınızın bir farklı çalıştır başlatabilirsiniz hello çağrıları belirtir.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-109">A trigger specifies hello calls that can initiate a run of your logic app workflow.</span></span> <span data-ttu-id="f0cdf-110">Merhaba iki farklı şekilde tooinitiate, iş akışınızın bir farklı çalıştır şunlardır:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-110">Here are hello two different ways tooinitiate a run of your workflow:</span></span>  
  
-   <span data-ttu-id="f0cdf-111">Yoklama tetikleyici</span><span class="sxs-lookup"><span data-stu-id="f0cdf-111">A polling trigger</span></span>  

-   <span data-ttu-id="f0cdf-112">Anında iletme tetikleyici - arama hello tarafından [iş akışı hizmeti REST API'si](https://docs.microsoft.com/rest/api/logic/workflows)</span><span class="sxs-lookup"><span data-stu-id="f0cdf-112">A push trigger - by calling hello [Workflow Service REST API](https://docs.microsoft.com/rest/api/logic/workflows)</span></span>  
  
<span data-ttu-id="f0cdf-113">Tüm Tetikleyicileri bu üst düzey öğeleri içerir:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-113">All triggers contain these top-level elements:</span></span>  
  
```json
"<name-of-the-trigger>" : {
    "type": "<type-of-trigger>",
    "inputs": { <settings-for-the-call> },
    "recurrence": {  
        "frequency": "Second|Minute|Hour|Week|Month|Year",
        "interval": "<recurrence interval in units of frequency>"
    },
    "conditions": [ <array-of-required-conditions > ],
    "splitOn" : "<property toocreate runs for>",
    "operationOptions": "<operation options on hello trigger>"
}
```

### <a name="trigger-types-and-their-inputs"></a><span data-ttu-id="f0cdf-114">Tetikleyici türlerini ve bunların girişleri</span><span class="sxs-lookup"><span data-stu-id="f0cdf-114">Trigger types and their inputs</span></span>  

<span data-ttu-id="f0cdf-115">Bu tür tetikleyici sunucusu kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-115">You can use these types of triggers:</span></span>
  
-   <span data-ttu-id="f0cdf-116">**İstek** \- hello mantıksal uygulama, toocall için bir uç nokta yapar</span><span class="sxs-lookup"><span data-stu-id="f0cdf-116">**Request** \- Makes hello logic app an endpoint for you toocall</span></span>  
  
-   <span data-ttu-id="f0cdf-117">**Yineleme** \- ateşlenir dayalı tanımlanmış bir zamanlamaya göre</span><span class="sxs-lookup"><span data-stu-id="f0cdf-117">**Recurrence** \- Fires based on a defined schedule</span></span>  
  
-   <span data-ttu-id="f0cdf-118">**HTTP** \- bir HTTP web uç noktası yoklar.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-118">**HTTP** \- Polls an HTTP web endpoint.</span></span> <span data-ttu-id="f0cdf-119">Merhaba HTTP uç noktası tooa belirli tetikleme sözleşme uygun olmalıdır \- bir 202 kullanarak ya da\-zaman uyumsuz desen veya bir dizi döndürerek</span><span class="sxs-lookup"><span data-stu-id="f0cdf-119">hello HTTP endpoint must conform tooa specific triggering contract \- either by using a 202\-async pattern, or by returning an array</span></span>  
  
-   <span data-ttu-id="f0cdf-120">**ApiConnection** \- hello HTTP gibi yoklamalar tetikleyin, ancak bunu hello yararlanan [Microsoft tarafından yönetilen API'ler](https://docs.microsoft.com/azure/connectors/apis-list)</span><span class="sxs-lookup"><span data-stu-id="f0cdf-120">**ApiConnection** \- Polls like hello HTTP trigger, however, it takes advantage of hello [Microsoft-managed APIs](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>  
  
-   <span data-ttu-id="f0cdf-121">**HTTPWebhook** \- açılır uç noktası, benzer toohello el ile tetikleyici, ancak, bir de çağırır tooa URL tooregister belirtilen ve kaldırılamadı</span><span class="sxs-lookup"><span data-stu-id="f0cdf-121">**HTTPWebhook** \- Opens an endpoint, similar toohello Manual trigger, however, it also calls out tooa specified URL tooregister and unregister</span></span>  
  
-   <span data-ttu-id="f0cdf-122">**ApiConnectionWebhook** \- hello Microsoft tarafından yönetilen API yararlanarak HTTPWebhook tetikleyici hello gibi çalışır</span><span class="sxs-lookup"><span data-stu-id="f0cdf-122">**ApiConnectionWebhook** \- Operates like hello HTTPWebhook trigger by taking advantage of hello Microsoft-managed APIs</span></span>       
    <span data-ttu-id="f0cdf-123">Farklı bir kümesini her tetikleyici türünde **girişleri** davranışını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-123">Each trigger type has a different set of **inputs** that defines its behavior.</span></span>  
  
## <a name="request-trigger"></a><span data-ttu-id="f0cdf-124">Tetikleyici isteği</span><span class="sxs-lookup"><span data-stu-id="f0cdf-124">Request trigger</span></span>  

<span data-ttu-id="f0cdf-125">Bu tetikleyici bir uç noktası olarak bir HTTP isteği tooinvoke mantıksal uygulamanızı çağıran işlevi görür.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-125">This trigger serves as an endpoint that you call via an HTTP Request tooinvoke your logic app.</span></span> <span data-ttu-id="f0cdf-126">Bir istek tetikleyici aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-126">A request trigger looks like this example:</span></span>  
  
```json
"<name-of-the-trigger>" : {
    "type" : "request",
    "kind": "http",
    "inputs" : {
        "schema" : {
            "properties" : {
                "myInputProperty1" : { "type" : "string" },
                "myInputProperty2" : { "type" : "number" }
            },
        "required" : [ "myInputProperty1" ],
        "type" : "object"
        }
    }
} 
```

<span data-ttu-id="f0cdf-127">Ayrıca adlı isteğe bağlı bir özellik olan **şema**:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-127">There is also an optional property called **schema**:</span></span>  
  
|<span data-ttu-id="f0cdf-128">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="f0cdf-128">Element name</span></span>|<span data-ttu-id="f0cdf-129">Gerekli</span><span class="sxs-lookup"><span data-stu-id="f0cdf-129">Required</span></span>|<span data-ttu-id="f0cdf-130">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f0cdf-130">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="f0cdf-131">Şema</span><span class="sxs-lookup"><span data-stu-id="f0cdf-131">schema</span></span>|<span data-ttu-id="f0cdf-132">Hayır</span><span class="sxs-lookup"><span data-stu-id="f0cdf-132">No</span></span>|<span data-ttu-id="f0cdf-133">JSON şeması hello gelen isteği doğrular.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-133">A JSON schema that validates hello incoming request.</span></span> <span data-ttu-id="f0cdf-134">Sonraki iş akışı adımları hangi özellikleri tooreference bilmeniz yardımcı olmak için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-134">Useful for helping subsequent workflow steps know which properties tooreference.</span></span>|

<span data-ttu-id="f0cdf-135">tooinvoke Bu uç noktaya toocall hello gereksinim *listCallbackUrl* API.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-135">tooinvoke this endpoint, you need toocall hello *listCallbackUrl* API.</span></span> <span data-ttu-id="f0cdf-136">Bkz: [iş akışı hizmeti REST API'si](https://docs.microsoft.com/rest/api/logic/workflows).</span><span class="sxs-lookup"><span data-stu-id="f0cdf-136">See [Workflow Service REST API](https://docs.microsoft.com/rest/api/logic/workflows).</span></span>  
  
## <a name="recurrence-trigger"></a><span data-ttu-id="f0cdf-137">Yineleme tetikleyici</span><span class="sxs-lookup"><span data-stu-id="f0cdf-137">Recurrence trigger</span></span>  

<span data-ttu-id="f0cdf-138">Bir yineleme tetikleyici tanımlanmış bir zamanlamaya göre çalıştırır biridir.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-138">A Recurrence trigger is one that runs based on a defined schedule.</span></span> <span data-ttu-id="f0cdf-139">Bu tür bir tetikleyici, aşağıdaki örnekte olduğu gibi görünebilir:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-139">Such a trigger might look like this example:</span></span>  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

<span data-ttu-id="f0cdf-140">Gördüğünüz gibi bir basit yol toorun bir iş akışı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-140">As you can see, it is a simple way toorun a workflow.</span></span>  
  
|<span data-ttu-id="f0cdf-141">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="f0cdf-141">Element name</span></span>|<span data-ttu-id="f0cdf-142">Gerekli</span><span class="sxs-lookup"><span data-stu-id="f0cdf-142">Required</span></span>|<span data-ttu-id="f0cdf-143">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f0cdf-143">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="f0cdf-144">frequency</span><span class="sxs-lookup"><span data-stu-id="f0cdf-144">frequency</span></span>|<span data-ttu-id="f0cdf-145">Evet</span><span class="sxs-lookup"><span data-stu-id="f0cdf-145">Yes</span></span>|<span data-ttu-id="f0cdf-146">Ne sıklıkta hello tetikleyici yürütür.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-146">How often hello trigger executes.</span></span> <span data-ttu-id="f0cdf-147">Bu değerlerden yalnızca birini kullanın: saniye, dakika, saat, gün, hafta, ay veya yıl</span><span class="sxs-lookup"><span data-stu-id="f0cdf-147">Use only one of these possible values: second, minute, hour, day, week, month, or year</span></span>|  
|<span data-ttu-id="f0cdf-148">interval</span><span class="sxs-lookup"><span data-stu-id="f0cdf-148">interval</span></span>|<span data-ttu-id="f0cdf-149">Evet</span><span class="sxs-lookup"><span data-stu-id="f0cdf-149">Yes</span></span>|<span data-ttu-id="f0cdf-150">Merhaba yinelemesi sıklığı verilen hello aralığı</span><span class="sxs-lookup"><span data-stu-id="f0cdf-150">Interval of hello given frequency for hello recurrence</span></span>|  
|<span data-ttu-id="f0cdf-151">startTime</span><span class="sxs-lookup"><span data-stu-id="f0cdf-151">startTime</span></span>|<span data-ttu-id="f0cdf-152">Hayır</span><span class="sxs-lookup"><span data-stu-id="f0cdf-152">No</span></span>|<span data-ttu-id="f0cdf-153">Bir startTime UTC uzaklığı sağlanırsa, bu saat dilimi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-153">If a startTime is provided without a UTC offset, this timeZone is used.</span></span>|  
|<span data-ttu-id="f0cdf-154">saat dilimi</span><span class="sxs-lookup"><span data-stu-id="f0cdf-154">timeZone</span></span>|<span data-ttu-id="f0cdf-155">Yok</span><span class="sxs-lookup"><span data-stu-id="f0cdf-155">no</span></span>|<span data-ttu-id="f0cdf-156">Bir startTime UTC uzaklığı sağlanırsa, bu saat dilimi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-156">If a startTime is provided without a UTC offset, this timeZone is used.</span></span>|  
  
<span data-ttu-id="f0cdf-157">Ayrıca, bir tetikleyici toostart hello gelecekteki belirli bir noktada yürütme zamanlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-157">You can also schedule a trigger toostart executing at some point in hello future.</span></span> <span data-ttu-id="f0cdf-158">Haftalık rapor her Pazartesi toostart isterseniz, örneğin, hello mantığı uygulama toostart her Pazartesi tetikleyici aşağıdaki hello oluşturarak zamanlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-158">For example, if you want toostart a weekly report every Monday you can schedule hello logic app toostart every Monday by creating hello following trigger:</span></span>  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Week",
        "interval": "1",
        "startTime" : "2015-06-22T00:00:00Z"
    }
}
```

## <a name="http-trigger"></a><span data-ttu-id="f0cdf-159">HTTP tetikleyicisi</span><span class="sxs-lookup"><span data-stu-id="f0cdf-159">HTTP trigger</span></span>  

<span data-ttu-id="f0cdf-160">HTTP Tetikleyicileri belirtilen uç nokta yoklamak ve hello yanıt toodetermine hello iş akışı yürütülmesi gereken olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-160">HTTP triggers poll a specified endpoint and check hello response toodetermine whether hello workflow should be executed.</span></span> <span data-ttu-id="f0cdf-161">Merhaba girişleri nesne parametreleri gerekli tooconstruct bir HTTP çağrısıyla hello kümesini alır:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-161">hello inputs object takes hello set of parameters required tooconstruct an HTTP call:</span></span>  
  
|<span data-ttu-id="f0cdf-162">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="f0cdf-162">Element name</span></span>|<span data-ttu-id="f0cdf-163">Gerekli</span><span class="sxs-lookup"><span data-stu-id="f0cdf-163">Required</span></span>|<span data-ttu-id="f0cdf-164">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f0cdf-164">Description</span></span>|<span data-ttu-id="f0cdf-165">Tür</span><span class="sxs-lookup"><span data-stu-id="f0cdf-165">Type</span></span>|  
|----------------|------------|---------------|--------|  
|<span data-ttu-id="f0cdf-166">Yöntemi</span><span class="sxs-lookup"><span data-stu-id="f0cdf-166">method</span></span>|<span data-ttu-id="f0cdf-167">Evet</span><span class="sxs-lookup"><span data-stu-id="f0cdf-167">yes</span></span>|<span data-ttu-id="f0cdf-168">HTTP yöntemleri aşağıdaki hello biri olabilir: GET, POST, PUT, DELETE, düzeltme eki veya HEAD</span><span class="sxs-lookup"><span data-stu-id="f0cdf-168">Can be one of hello following HTTP methods: GET, POST, PUT, DELETE, PATCH, or HEAD</span></span>|<span data-ttu-id="f0cdf-169">Dize</span><span class="sxs-lookup"><span data-stu-id="f0cdf-169">String</span></span>|  
|<span data-ttu-id="f0cdf-170">URI</span><span class="sxs-lookup"><span data-stu-id="f0cdf-170">uri</span></span>|<span data-ttu-id="f0cdf-171">Evet</span><span class="sxs-lookup"><span data-stu-id="f0cdf-171">yes</span></span>|<span data-ttu-id="f0cdf-172">çağrılan hello http veya https uç noktası.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-172">hello http or https endpoint that is called.</span></span> <span data-ttu-id="f0cdf-173">2 kilobayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-173">Maximum of 2 kilobytes.</span></span>|<span data-ttu-id="f0cdf-174">Dize</span><span class="sxs-lookup"><span data-stu-id="f0cdf-174">String</span></span>|  
|<span data-ttu-id="f0cdf-175">Sorguları</span><span class="sxs-lookup"><span data-stu-id="f0cdf-175">queries</span></span>|<span data-ttu-id="f0cdf-176">Hayır</span><span class="sxs-lookup"><span data-stu-id="f0cdf-176">No</span></span>|<span data-ttu-id="f0cdf-177">Merhaba sorgu parametreleri tooadd toohello URL'yi temsil eden bir nesne.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-177">An object representing hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="f0cdf-178">Örneğin, `"queries" : { "api-version": "2015-02-01" }` ekler `?api-version=2015-02-01` toohello URL.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-178">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|<span data-ttu-id="f0cdf-179">Nesne</span><span class="sxs-lookup"><span data-stu-id="f0cdf-179">Object</span></span>|  
|<span data-ttu-id="f0cdf-180">Üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="f0cdf-180">headers</span></span>|<span data-ttu-id="f0cdf-181">Hayır</span><span class="sxs-lookup"><span data-stu-id="f0cdf-181">No</span></span>|<span data-ttu-id="f0cdf-182">Her toohello isteği gönderilir hello üstbilgilerinin temsil eden bir nesne.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-182">An object representing each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="f0cdf-183">Örneğin, tooset hello dil ve istek üzerine yazın:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="f0cdf-183">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|<span data-ttu-id="f0cdf-184">Nesne</span><span class="sxs-lookup"><span data-stu-id="f0cdf-184">Object</span></span>|  
|<span data-ttu-id="f0cdf-185">Gövde</span><span class="sxs-lookup"><span data-stu-id="f0cdf-185">body</span></span>|<span data-ttu-id="f0cdf-186">Hayır</span><span class="sxs-lookup"><span data-stu-id="f0cdf-186">No</span></span>|<span data-ttu-id="f0cdf-187">Toohello endpoint gönderilen hello yükünü temsil eden bir nesne.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-187">An object representing hello payload that is sent toohello endpoint.</span></span>|<span data-ttu-id="f0cdf-188">Nesne</span><span class="sxs-lookup"><span data-stu-id="f0cdf-188">Object</span></span>|  
|<span data-ttu-id="f0cdf-189">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="f0cdf-189">retryPolicy</span></span>|<span data-ttu-id="f0cdf-190">Hayır</span><span class="sxs-lookup"><span data-stu-id="f0cdf-190">No</span></span>|<span data-ttu-id="f0cdf-191">Merhaba yeniden deneme davranışı 4xx veya 5xx hataları özelleştirmenize olanak sağlayan bir nesne.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-191">An object that lets you customize hello retry behavior for 4xx or 5xx errors.</span></span>|<span data-ttu-id="f0cdf-192">Nesne</span><span class="sxs-lookup"><span data-stu-id="f0cdf-192">Object</span></span>|  
|<span data-ttu-id="f0cdf-193">Kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="f0cdf-193">authentication</span></span>|<span data-ttu-id="f0cdf-194">Hayır</span><span class="sxs-lookup"><span data-stu-id="f0cdf-194">No</span></span>|<span data-ttu-id="f0cdf-195">İstek hello temsil hello yöntemi kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-195">Represents hello method that hello request should be authenticated.</span></span> <span data-ttu-id="f0cdf-196">Bu nesne üzerinde daha fazla bilgi için bkz [Scheduler giden bağlantı kimlik doğrulaması](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span><span class="sxs-lookup"><span data-stu-id="f0cdf-196">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span></span> <span data-ttu-id="f0cdf-197">Zamanlayıcı daha desteklenen bir özellik yok: `authority` varsayılan olarak, bu değer `https://login.windows.net` belirtilmediğinde, ancak gibi farklı bir kitleye kullanabilirsiniz`https://login.windows\-ppe.net`</span><span class="sxs-lookup"><span data-stu-id="f0cdf-197">Beyond scheduler, there is one more supported property: `authority` By default, this value is `https://login.windows.net` when not specified, but you can use a different audience like `https://login.windows\-ppe.net`</span></span>|<span data-ttu-id="f0cdf-198">Nesne</span><span class="sxs-lookup"><span data-stu-id="f0cdf-198">Object</span></span>|  
  
<span data-ttu-id="f0cdf-199">Merhaba HTTP tetikleyicisini hello HTTP API tooconform belirli bir desene toowork mantıksal uygulamanızı ile iyi ile gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-199">hello HTTP trigger requires hello HTTP API tooconform with a specific pattern toowork well with your logic app.</span></span> <span data-ttu-id="f0cdf-200">Alanları aşağıdaki hello gerektirir:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-200">It requires hello following fields:</span></span>  
  
|<span data-ttu-id="f0cdf-201">Yanıt</span><span class="sxs-lookup"><span data-stu-id="f0cdf-201">Response</span></span>|<span data-ttu-id="f0cdf-202">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f0cdf-202">Description</span></span>|  
|------------|---------------|  
|<span data-ttu-id="f0cdf-203">Durum kodu</span><span class="sxs-lookup"><span data-stu-id="f0cdf-203">Status code</span></span>|<span data-ttu-id="f0cdf-204">Durum kodu 200 \(Tamam\) toocause Çalıştır.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-204">Status code 200 \(OK\) toocause a run.</span></span> <span data-ttu-id="f0cdf-205">Diğer bir durum kodu bir Farklı Çalıştır neden olmaz.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-205">Any other status code doesn't cause a run.</span></span>|  
|<span data-ttu-id="f0cdf-206">Yeniden deneme\-üstbilgi sonra</span><span class="sxs-lookup"><span data-stu-id="f0cdf-206">Retry\-after header</span></span>|<span data-ttu-id="f0cdf-207">Merhaba mantıksal uygulama hello uç nokta yeniden yoklar kadar saniye sayısı.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-207">Number of seconds until hello logic app polls hello endpoint again.</span></span>|  
|<span data-ttu-id="f0cdf-208">Konum üstbilgisi</span><span class="sxs-lookup"><span data-stu-id="f0cdf-208">Location header</span></span>|<span data-ttu-id="f0cdf-209">Merhaba URL toocall hello sonraki yoklama aralığı.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-209">hello URL toocall on hello next polling interval.</span></span> <span data-ttu-id="f0cdf-210">Belirtilmezse, hello özgün URL'si kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-210">If not specified, hello original URL is used.</span></span>|  
  
<span data-ttu-id="f0cdf-211">İstekleri farklı türleri için farklı davranışlar bazı örnekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-211">Here are some examples of different behaviors for different types of requests:</span></span>  
  
|<span data-ttu-id="f0cdf-212">Yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="f0cdf-212">Response code</span></span>|<span data-ttu-id="f0cdf-213">Yeniden deneme\-sonra</span><span class="sxs-lookup"><span data-stu-id="f0cdf-213">Retry\-After</span></span>|<span data-ttu-id="f0cdf-214">Davranışı</span><span class="sxs-lookup"><span data-stu-id="f0cdf-214">Behavior</span></span>|  
|-----------------|----------------|------------|  
|<span data-ttu-id="f0cdf-215">200</span><span class="sxs-lookup"><span data-stu-id="f0cdf-215">200</span></span>|<span data-ttu-id="f0cdf-216">\(yok\)</span><span class="sxs-lookup"><span data-stu-id="f0cdf-216">\(none\)</span></span>|<span data-ttu-id="f0cdf-217">Değil geçerli tetikleyici yeniden deneme\-sonra gerekli ya da başka hello hiçbir zaman hello sonraki istek için yoklamaları altyapısıdır.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-217">Not a valid trigger, Retry\-After is required, or else hello engine never polls for hello next request.</span></span>|  
|<span data-ttu-id="f0cdf-218">202</span><span class="sxs-lookup"><span data-stu-id="f0cdf-218">202</span></span>|<span data-ttu-id="f0cdf-219">60</span><span class="sxs-lookup"><span data-stu-id="f0cdf-219">60</span></span>|<span data-ttu-id="f0cdf-220">Merhaba iş akışı tetiklemez.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-220">Do not trigger hello workflow.</span></span> <span data-ttu-id="f0cdf-221">Merhaba sonraki girişiminde bir dakika içinde gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-221">hello next attempt happens in one minute.</span></span>|  
|<span data-ttu-id="f0cdf-222">200</span><span class="sxs-lookup"><span data-stu-id="f0cdf-222">200</span></span>|<span data-ttu-id="f0cdf-223">10</span><span class="sxs-lookup"><span data-stu-id="f0cdf-223">10</span></span>|<span data-ttu-id="f0cdf-224">Merhaba iş akışını çalıştırma ve daha fazla içerik için 10 saniye içinde yeniden kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-224">Run hello workflow, and check again for more content in 10 seconds.</span></span>|  
|<span data-ttu-id="f0cdf-225">400</span><span class="sxs-lookup"><span data-stu-id="f0cdf-225">400</span></span>|<span data-ttu-id="f0cdf-226">\(yok\)</span><span class="sxs-lookup"><span data-stu-id="f0cdf-226">\(none\)</span></span>|<span data-ttu-id="f0cdf-227">Hatalı istek, hello iş akışı çalıştırmayın.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-227">Bad request, do not run hello workflow.</span></span> <span data-ttu-id="f0cdf-228">Varsa hiçbir **yeniden deneme ilkesi** tanımlanan hello varsayılan ilke kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-228">If there is no **Retry Policy** defined, then hello default policy is used.</span></span> <span data-ttu-id="f0cdf-229">Merhaba yeniden deneme sayısı üst sınırına ulaşıldı sonra hello tetikleyici artık geçerli değil.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-229">After hello number of retries has been reached, hello trigger is no longer valid.</span></span>|  
|<span data-ttu-id="f0cdf-230">500</span><span class="sxs-lookup"><span data-stu-id="f0cdf-230">500</span></span>|<span data-ttu-id="f0cdf-231">\(yok\)</span><span class="sxs-lookup"><span data-stu-id="f0cdf-231">\(none\)</span></span>|<span data-ttu-id="f0cdf-232">Sunucu hatası, hello iş akışı çalıştırmayın.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-232">Server error, do not run hello workflow.</span></span>  <span data-ttu-id="f0cdf-233">Varsa hiçbir **yeniden deneme ilkesi** tanımlanan hello varsayılan ilke kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-233">If there is no **Retry Policy** defined, then hello default policy is used.</span></span> <span data-ttu-id="f0cdf-234">Merhaba yeniden deneme sayısı üst sınırına ulaşıldı sonra hello tetikleyici artık geçerli değil.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-234">After hello number of retries has been reached, hello trigger is no longer valid.</span></span>|  
  
<span data-ttu-id="f0cdf-235">bir HTTP tetikleyicisi Hello çıkışları aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-235">hello outputs of an HTTP trigger look like this example:</span></span>  
  
|<span data-ttu-id="f0cdf-236">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="f0cdf-236">Element name</span></span>|<span data-ttu-id="f0cdf-237">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f0cdf-237">Description</span></span>|<span data-ttu-id="f0cdf-238">Tür</span><span class="sxs-lookup"><span data-stu-id="f0cdf-238">Type</span></span>|  
|----------------|---------------|--------|  
|<span data-ttu-id="f0cdf-239">Üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="f0cdf-239">headers</span></span>|<span data-ttu-id="f0cdf-240">Merhaba http yanıtının Hello üstbilgileri.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-240">hello headers of hello http response.</span></span>|<span data-ttu-id="f0cdf-241">Nesne</span><span class="sxs-lookup"><span data-stu-id="f0cdf-241">Object</span></span>|  
|<span data-ttu-id="f0cdf-242">Gövde</span><span class="sxs-lookup"><span data-stu-id="f0cdf-242">body</span></span>|<span data-ttu-id="f0cdf-243">Merhaba hello http yanıt gövdesi.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-243">hello body of hello http response.</span></span>|<span data-ttu-id="f0cdf-244">Nesne</span><span class="sxs-lookup"><span data-stu-id="f0cdf-244">Object</span></span>|  
  
## <a name="api-connection-trigger"></a><span data-ttu-id="f0cdf-245">API bağlantı tetikleyici</span><span class="sxs-lookup"><span data-stu-id="f0cdf-245">API Connection trigger</span></span>  

<span data-ttu-id="f0cdf-246">Merhaba API bağlantı tetikleyici temel işlevselliği de benzer toohello HTTP tetikleyici ' dir.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-246">hello API connection trigger is similar toohello HTTP trigger in its basic functionality.</span></span> <span data-ttu-id="f0cdf-247">Ancak, hello eylem tanımlamak için başlangıç parametreleri farklıdır.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-247">However, hello parameters for identifying hello action are different.</span></span> <span data-ttu-id="f0cdf-248">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-248">Here is an example:</span></span>  
  
```json
"dailyReport" : {
    "type": "ApiConnection",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://myarticles.example.com/"
            },
        }
        "connection": {
            "name": "@parameters('$connections')['myconnection'].name"
        }
    },  
    "method": "POST",
    "body": {
        "category": "awesomest"
    }
}
```

|<span data-ttu-id="f0cdf-249">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="f0cdf-249">Element name</span></span>|<span data-ttu-id="f0cdf-250">Gerekli</span><span class="sxs-lookup"><span data-stu-id="f0cdf-250">Required</span></span>|<span data-ttu-id="f0cdf-251">Tür</span><span class="sxs-lookup"><span data-stu-id="f0cdf-251">Type</span></span>|<span data-ttu-id="f0cdf-252">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f0cdf-252">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="f0cdf-253">ana bilgisayar</span><span class="sxs-lookup"><span data-stu-id="f0cdf-253">host</span></span>|<span data-ttu-id="f0cdf-254">Evet</span><span class="sxs-lookup"><span data-stu-id="f0cdf-254">Yes</span></span>||<span data-ttu-id="f0cdf-255">Merhaba ApiApp ağ geçidi ve kimliği barındırılan.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-255">hello ApiApp hosted gateway and id.</span></span>|  
|<span data-ttu-id="f0cdf-256">Yöntemi</span><span class="sxs-lookup"><span data-stu-id="f0cdf-256">method</span></span>|<span data-ttu-id="f0cdf-257">Evet</span><span class="sxs-lookup"><span data-stu-id="f0cdf-257">Yes</span></span>|<span data-ttu-id="f0cdf-258">Dize</span><span class="sxs-lookup"><span data-stu-id="f0cdf-258">String</span></span>|<span data-ttu-id="f0cdf-259">HTTP yöntemleri aşağıdaki hello biri olabilir: **almak**, **POST**, **PUT**, **silmek**, **düzeltme eki**, veya  **HEAD**</span><span class="sxs-lookup"><span data-stu-id="f0cdf-259">Can be one of hello following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="f0cdf-260">Sorguları</span><span class="sxs-lookup"><span data-stu-id="f0cdf-260">queries</span></span>|<span data-ttu-id="f0cdf-261">Hayır</span><span class="sxs-lookup"><span data-stu-id="f0cdf-261">No</span></span>|<span data-ttu-id="f0cdf-262">Nesne</span><span class="sxs-lookup"><span data-stu-id="f0cdf-262">Object</span></span>|<span data-ttu-id="f0cdf-263">Temsil hello sorgu parametreleri toobe toohello URL eklendi.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-263">Represents hello query parameters toobe added toohello URL.</span></span> <span data-ttu-id="f0cdf-264">Örneğin, `"queries" : { "api-version": "2015-02-01" }` ekler `?api-version=2015-02-01` toohello URL.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-264">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="f0cdf-265">Üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="f0cdf-265">headers</span></span>|<span data-ttu-id="f0cdf-266">Hayır</span><span class="sxs-lookup"><span data-stu-id="f0cdf-266">No</span></span>|<span data-ttu-id="f0cdf-267">Nesne</span><span class="sxs-lookup"><span data-stu-id="f0cdf-267">Object</span></span>|<span data-ttu-id="f0cdf-268">Her toohello isteği gönderilir hello üstbilgilerinin temsil eder.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-268">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="f0cdf-269">Örneğin, tooset hello dil ve istek üzerine yazın:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="f0cdf-269">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="f0cdf-270">Gövde</span><span class="sxs-lookup"><span data-stu-id="f0cdf-270">body</span></span>|<span data-ttu-id="f0cdf-271">Hayır</span><span class="sxs-lookup"><span data-stu-id="f0cdf-271">No</span></span>|<span data-ttu-id="f0cdf-272">Nesne</span><span class="sxs-lookup"><span data-stu-id="f0cdf-272">Object</span></span>|<span data-ttu-id="f0cdf-273">Toohello endpoint gönderilen hello yükünü temsil eder.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-273">Represents hello payload that is sent toohello endpoint.</span></span>|  
|<span data-ttu-id="f0cdf-274">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="f0cdf-274">retryPolicy</span></span>|<span data-ttu-id="f0cdf-275">Hayır</span><span class="sxs-lookup"><span data-stu-id="f0cdf-275">No</span></span>|<span data-ttu-id="f0cdf-276">Nesne</span><span class="sxs-lookup"><span data-stu-id="f0cdf-276">Object</span></span>|<span data-ttu-id="f0cdf-277">Toocustomize hello yeniden deneme davranışı 4xx veya 5xx hataları sağlar.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-277">Allows you toocustomize hello retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="f0cdf-278">Kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="f0cdf-278">authentication</span></span>|<span data-ttu-id="f0cdf-279">Hayır</span><span class="sxs-lookup"><span data-stu-id="f0cdf-279">No</span></span>|<span data-ttu-id="f0cdf-280">Nesne</span><span class="sxs-lookup"><span data-stu-id="f0cdf-280">Object</span></span>|<span data-ttu-id="f0cdf-281">İstek hello temsil hello yöntemi kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-281">Represents hello method that hello request should be authenticated.</span></span> <span data-ttu-id="f0cdf-282">Bu nesne üzerinde daha fazla bilgi için bkz [Scheduler giden bağlantı kimlik doğrulaması](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)</span><span class="sxs-lookup"><span data-stu-id="f0cdf-282">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)</span></span>|  
  
<span data-ttu-id="f0cdf-283">ana bilgisayar için Hello özellikleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-283">hello properties for host are:</span></span>  
  
|<span data-ttu-id="f0cdf-284">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="f0cdf-284">Element name</span></span>|<span data-ttu-id="f0cdf-285">Gerekli</span><span class="sxs-lookup"><span data-stu-id="f0cdf-285">Required</span></span>|<span data-ttu-id="f0cdf-286">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f0cdf-286">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="f0cdf-287">API runtimeUrl</span><span class="sxs-lookup"><span data-stu-id="f0cdf-287">api runtimeUrl</span></span>|<span data-ttu-id="f0cdf-288">Evet</span><span class="sxs-lookup"><span data-stu-id="f0cdf-288">Yes</span></span>|<span data-ttu-id="f0cdf-289">Merhaba Hello uç noktasını API yönetilen.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-289">hello endpoint of hello managed API.</span></span>|  
|<span data-ttu-id="f0cdf-290">Bağlantı adı</span><span class="sxs-lookup"><span data-stu-id="f0cdf-290">connection name</span></span>||<span data-ttu-id="f0cdf-291">Bir başvuru tooa parametre çağrılmalıdır `$connection` ve iş akışı kullanır hello yönetilen hello API bağlantı hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-291">Must be a reference tooa parameter called `$connection` and is hello name of hello managed API connection that hello workflow uses.</span></span>|
  
<span data-ttu-id="f0cdf-292">bir API bağlantı tetikleyicisi Hello çıkışları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-292">hello outputs of an API connection trigger are:</span></span>
  
|<span data-ttu-id="f0cdf-293">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="f0cdf-293">Element name</span></span>|<span data-ttu-id="f0cdf-294">Tür</span><span class="sxs-lookup"><span data-stu-id="f0cdf-294">Type</span></span>|<span data-ttu-id="f0cdf-295">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f0cdf-295">Description</span></span>|  
|----------------|--------|---------------|  
|<span data-ttu-id="f0cdf-296">Üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="f0cdf-296">headers</span></span>|<span data-ttu-id="f0cdf-297">Nesne</span><span class="sxs-lookup"><span data-stu-id="f0cdf-297">Object</span></span>|<span data-ttu-id="f0cdf-298">Merhaba http yanıtının Hello üstbilgileri.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-298">hello headers of hello http response.</span></span>|  
|<span data-ttu-id="f0cdf-299">Gövde</span><span class="sxs-lookup"><span data-stu-id="f0cdf-299">body</span></span>|<span data-ttu-id="f0cdf-300">Nesne</span><span class="sxs-lookup"><span data-stu-id="f0cdf-300">Object</span></span>|<span data-ttu-id="f0cdf-301">Merhaba hello http yanıt gövdesi.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-301">hello body of hello http response.</span></span>|  
  
## <a name="httpwebhook-trigger"></a><span data-ttu-id="f0cdf-302">HTTPWebhook tetikleyici</span><span class="sxs-lookup"><span data-stu-id="f0cdf-302">HTTPWebhook trigger</span></span>  

<span data-ttu-id="f0cdf-303">bir uç nokta, benzer toohello el ile tetikleyici, ancak hello HTTPWebhook tetikleyici de tooa çağırır hello HTTPWebhook tetikleyici açar URL tooregister belirtilen ve kaydını silin.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-303">hello HTTPWebhook trigger opens an endpoint, similar toohello manual trigger, but hello HTTPWebhook trigger also calls out tooa specified URL tooregister and unregister.</span></span> <span data-ttu-id="f0cdf-304">Bir HTTPWebhook tetikleyicisi aşağıdaki gibi görünmelidir örneği şöyledir:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-304">Here's an example of what an HTTPWebhook trigger might look like:</span></span>  

```json
"myappspottrigger": {
    "type": "httpWebhook",
    "inputs": {
        "subscribe": {
            "method": "POST",
            "uri": "https://pubsubhubbub.appspot.com/subscribe",
            "headers": { },
            "body": {
                "hub.callback": "@{listCallbackUrl()}",
                "hub.mode": "subscribe",
                "hub.topic": "https://pubsubhubbub.appspot.com/articleCategories/technology"
            },
            "authentication": { },
            "retryPolicy": { }
        },
        "unsubscribe": {
            "url": "https://pubsubhubbub.appspot.com/subscribe",
            "body": {
                "hub.callback": "@{workflow().endpoint}@{listCallbackUrl()}",
                "hub.mode": "unsubscribe",
                "hub.topic": "https://pubsubhubbub.appspot.com/articleCategories/technology"
            },
            "method": "POST",
            "authentication": { }
        }
    },
    "conditions": [ ]
    }
```

<span data-ttu-id="f0cdf-305">Bu bölümler çoğunu isteğe bağlıdır ve hello Web kancası hello davranışını hangi bölümlerinin sağlanan atlanmış veya bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-305">Many of these sections are optional, and hello behavior of hello Webhook depends on which sections are provided or omitted.</span></span>  
<span data-ttu-id="f0cdf-306">bir Web kancası Hello özelliklerini aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-306">hello properties of a Webhook are as follows:</span></span>  
  
|<span data-ttu-id="f0cdf-307">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="f0cdf-307">Element name</span></span>|<span data-ttu-id="f0cdf-308">Gerekli</span><span class="sxs-lookup"><span data-stu-id="f0cdf-308">Required</span></span>|<span data-ttu-id="f0cdf-309">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f0cdf-309">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="f0cdf-310">abone olma</span><span class="sxs-lookup"><span data-stu-id="f0cdf-310">subscribe</span></span>|<span data-ttu-id="f0cdf-311">Hayır</span><span class="sxs-lookup"><span data-stu-id="f0cdf-311">No</span></span>|<span data-ttu-id="f0cdf-312">Merhaba Hello tetikleyici oluşturulduğunda ve hello ilk kaydı gerçekleştiren çağrılan isteği giden.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-312">hello outgoing request that is called when hello trigger is created and performs hello initial registration.</span></span>|  
|<span data-ttu-id="f0cdf-313">Aboneliği Kaldır</span><span class="sxs-lookup"><span data-stu-id="f0cdf-313">unsubscribe</span></span>|<span data-ttu-id="f0cdf-314">Hayır</span><span class="sxs-lookup"><span data-stu-id="f0cdf-314">No</span></span>|<span data-ttu-id="f0cdf-315">Merhaba Hello tetikleyici silindiğinde isteği giden.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-315">hello outgoing request when hello trigger is deleted.</span></span>|  
  
-   <span data-ttu-id="f0cdf-316">**Abone** olan hello giden toostart dinleme tooevents yaptı çağrısı.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-316">**Subscribe** is hello outgoing call that's made toostart listening tooevents.</span></span> <span data-ttu-id="f0cdf-317">Bu çağrı aynı normal HTTP Eylemler hello parametre kümesine yapmak hello ile başlar.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-317">This call starts with hello same set of parameters that hello normal HTTP actions do.</span></span> <span data-ttu-id="f0cdf-318">Bu giden çağrı hiçbir zaman hello yapılan herhangi bir şekilde değişiklikler iş akışı, örneğin, her hello kimlik yapılır ya da hello tetikleyici parametreleri değişiklik girdisini.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-318">This outgoing call is made any time hello workflow changes in any way, for example, whenever hello credentials are rolled, or hello trigger's input parameters change.</span></span>
  
    <span data-ttu-id="f0cdf-319">toosupport bu çağrı, yeni bir işlev yok: `@listCallbackUrl()`.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-319">toosupport this call, there is a new function: `@listCallbackUrl()`.</span></span> <span data-ttu-id="f0cdf-320">Bu işlev, bu iş akışındaki belirli Bu tetikleyici için benzersiz bir URL döndürür.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-320">This function returns a unique URL for this specific trigger in this workflow.</span></span> <span data-ttu-id="f0cdf-321">Merhaba hizmet REST kullanan hello uç noktaları için benzersiz tanımlayıcı hello temsil eder.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-321">It represents hello unique identifier for hello endpoints that use hello Service REST.</span></span>  
  
-   <span data-ttu-id="f0cdf-322">**Aboneliği** bir işlem Bu tetikleyici geçersiz dahil olmak üzere işler olduğunda çağrılır:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-322">**Unsubscribe** is called when an operation renders this trigger invalid, including:</span></span>  
  
    -   <span data-ttu-id="f0cdf-323">Silme veya hello tetikleyici devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="f0cdf-323">Deleting or disabling hello trigger</span></span>  
  
    -   <span data-ttu-id="f0cdf-324">Silme veya hello iş akışını devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="f0cdf-324">Deleting or disabling hello workflow</span></span>  
  
    -   <span data-ttu-id="f0cdf-325">Silme veya hello abonelik devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="f0cdf-325">Deleting or disabling hello subscription</span></span>  
  
    <span data-ttu-id="f0cdf-326">Merhaba mantıksal uygulama otomatik olarak hello çağıran eylem aboneliği.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-326">hello logic app automatically calls hello unsubscribe action.</span></span> <span data-ttu-id="f0cdf-327">toothis işlevini hello parametreleri aynı hello HTTP tetikleyici olarak hello.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-327">hello parameters toothis function are hello same as hello HTTP trigger.</span></span>  
  
    <span data-ttu-id="f0cdf-328">Merhaba hello HTTPWebhook tetikleyici çıkışları hello gelen istek Merhaba içeriğine şunlardır:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-328">hello outputs of hello HTTPWebhook trigger are hello contents of hello incoming request:</span></span>  
  
|<span data-ttu-id="f0cdf-329">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="f0cdf-329">Element name</span></span>|<span data-ttu-id="f0cdf-330">Tür</span><span class="sxs-lookup"><span data-stu-id="f0cdf-330">Type</span></span>|<span data-ttu-id="f0cdf-331">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f0cdf-331">Description</span></span>|  
|-----------------|--------|---------------|  
|<span data-ttu-id="f0cdf-332">Üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="f0cdf-332">headers</span></span>|<span data-ttu-id="f0cdf-333">Nesne</span><span class="sxs-lookup"><span data-stu-id="f0cdf-333">Object</span></span>|<span data-ttu-id="f0cdf-334">Merhaba http istek üstbilgilerinin Hello.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-334">hello headers of hello http request.</span></span>|  
|<span data-ttu-id="f0cdf-335">Gövde</span><span class="sxs-lookup"><span data-stu-id="f0cdf-335">body</span></span>|<span data-ttu-id="f0cdf-336">Nesne</span><span class="sxs-lookup"><span data-stu-id="f0cdf-336">Object</span></span>|<span data-ttu-id="f0cdf-337">Merhaba hello http istek gövdesi.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-337">hello body of hello http request.</span></span>|  

<span data-ttu-id="f0cdf-338">Bir Web kancası eylemi sınırları hello belirtilebilir aynı şekilde [HTTP zaman uyumsuz sınırları](#asynchronous-limits).</span><span class="sxs-lookup"><span data-stu-id="f0cdf-338">Limits on a webhook action can be specified in hello same manner as [HTTP Asynchronous Limits](#asynchronous-limits).</span></span>
  

## <a name="conditions"></a><span data-ttu-id="f0cdf-339">Koşullar</span><span class="sxs-lookup"><span data-stu-id="f0cdf-339">Conditions</span></span>  

<span data-ttu-id="f0cdf-340">Merhaba iş akışı çalışıp çalışmayacağını olup olmadığını, herhangi bir tetikleyici için bir veya daha fazla koşullar toodetermine kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-340">For any trigger, you can use one or more conditions toodetermine whether hello workflow should run or not.</span></span> <span data-ttu-id="f0cdf-341">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-341">For example:</span></span>  

```json
"dailyReport" : {
    "type": "recurrence",
    "conditions": [ {
        "expression": "@parameters('sendReports')"
    } ],
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

<span data-ttu-id="f0cdf-342">Bu durumda, rapor yalnızca Tetikleyicileri hello iş akışı çalışırken hello `sendReports` parametresini tootrue ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-342">In this case, hello report only triggers while hello workflow's `sendReports` parameter is set tootrue.</span></span> <span data-ttu-id="f0cdf-343">Son olarak, koşullar hello tetikleyici hello durum kodunu başvurabilir.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-343">Finally, conditions may reference hello status code of hello trigger.</span></span> <span data-ttu-id="f0cdf-344">Örneğin, yalnızca Web sitenizin bir durum kodu 500, aşağıdaki gibi geri döndüğünde devre dışı bir iş akışı kazandırın:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-344">For example, you could kick off a workflow only when your website returns a status code 500, as follows:</span></span>
  
```  
"conditions": [  
        {  
          "expression": "@equals(triggers().code, 'InternalServerError')"  
        }  
      ]  
```  
  
> [!NOTE]  
> <span data-ttu-id="f0cdf-345">Herhangi bir ifade hello tetikleyici hello durum kodunu başvurduğunda \(herhangi bir şekilde\), hello varsayılan davranışı \(200 yalnızca Tetikle \(Tamam\) \) değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-345">When any expression references hello status code of hello trigger \(in any way\), hello default behavior \(trigger only on 200 \(OK\)\) is replaced.</span></span> <span data-ttu-id="f0cdf-346">Örneğin, durum kodu 200 ve 201 durum kodunu tootrigger isterseniz, tooinclude gerekir: `@or(equals(triggers().code, 200),equals(triggers().code,201))` koşulunuz olarak.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-346">For example, if you want tootrigger on both status code 200 and status code 201, you have tooinclude: `@or(equals(triggers().code, 200),equals(triggers().code,201))` as your condition.</span></span>  
  
## <a name="start-multiple-runs-for-a-request"></a><span data-ttu-id="f0cdf-347">Bir istek için birden çok çalışmalarını Başlat</span><span class="sxs-lookup"><span data-stu-id="f0cdf-347">Start multiple runs for a request</span></span>

<span data-ttu-id="f0cdf-348">tek bir istek için birden çok çalıştırır kapalı tookick `splitOn` toopoll yoklama aralıkları arasında birden çok yeni öğeleri olan bir uç nokta istediğinizde, örneğin, yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-348">tookick off multiple runs for a single request, `splitOn` is useful, for example, when you want toopoll an endpoint that can have multiple new items between polling intervals.</span></span>
  
<span data-ttu-id="f0cdf-349">İle `splitOn`, her biri istediğiniz öğeleri hello dizisi içerir hello yanıt yükünün hello özelliği belirtin toouse toostart hello tetikleyici yürütülmesi.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-349">With `splitOn`, you specify hello property inside hello response payload that contains hello array of items, each of which you want toouse toostart a run of hello trigger.</span></span> <span data-ttu-id="f0cdf-350">Örneğin, yanıt aşağıdaki hello döndüren bir API olduğunu düşünün:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-350">For example, imagine you have an API that returns hello following response:</span></span>  
  
```json
{
    "Status" : "success",
    "Rows" : [
        {  
            "id" : 938109380,
            "name" : "mycoolrow"
        },
        {
            "id" : 938109381,
            "name" : "another row"
        }
    ]
}
```
  
<span data-ttu-id="f0cdf-351">Bu örnek gibi tetikleyici gerçekleştirebilmesi için mantıksal uygulamanızı hello satırları içeriği, yalnızca gerekir:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-351">Your logic app only needs hello Rows content, so you can construct your trigger like this example:</span></span>  
  
```json
"mysplitter" : {
    "type" : "http",
    "recurrence": {
        "frequency": "Minute",
        "interval": "1"
    },
    "intputs" : {
        "uri" : "https://mydomain.com/myAPI",
        "method" : "GET"
    },
    "splitOn" : "@triggerBody()?.Rows"
}
```
  
<span data-ttu-id="f0cdf-352">Daha sonra hello iş akışı tanımında `@triggerBody().name` döndürür `mycoolrow` ilk çalıştırma hello için ve `another row` hello ikinci çalıştırma için.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-352">Then, in hello workflow definition, `@triggerBody().name` returns `mycoolrow` for hello first run, and `another row` for hello second run.</span></span> <span data-ttu-id="f0cdf-353">Bu örnek gibi Hello tetikleyici çıkışları bakın:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-353">hello trigger outputs look like this example:</span></span>  
  
```json
{
    "body" : {
        "id" : 938109381,
        "name" : "another row"
    }
}
```

<span data-ttu-id="f0cdf-354">Kullanırsanız, bunu `SplitOn`, hello dizi dışında bu durumda, hello hello özellikler alınamıyor `Status` alan.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-354">So if you use `SplitOn`, you can't get hello properties that are outside hello array, in this case, hello `Status` field.</span></span>  
  
> [!NOTE]  
> <span data-ttu-id="f0cdf-355">Bu örnekte, kullandığımız hello `?` işleci toobe mümkün tooavoid hello durumunda bir hata `Rows` özelliği mevcut değil.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-355">In this example, we use hello `?` operator toobe able tooavoid a failure if hello `Rows` property is not present.</span></span> 
  
## <a name="single-run-instance"></a><span data-ttu-id="f0cdf-356">Tek çalışma örneği</span><span class="sxs-lookup"><span data-stu-id="f0cdf-356">Single run instance</span></span>

<span data-ttu-id="f0cdf-357">Tüm etkin metinler tamamladıysanız, yineleme özelliği tooonly yangın sahip Tetikleyicileri yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-357">You can configure triggers that have a recurrence property tooonly fire if all active runs have completed.</span></span> <span data-ttu-id="f0cdf-358">Bir çalıştırma sürüyor olsa zamanlanmış bir yinelenme meydana gelirse, hello tetikleyici atlar ve hello sonraki zamanlanmış yineleme aralığı toocheck kadar yeniden bekler.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-358">If a scheduled recurrence occurs while there is an in-progress run, hello trigger skips and waits until hello next scheduled recurrence interval toocheck again.</span></span>

<span data-ttu-id="f0cdf-359">Bu ayar hello işlemi seçeneklerle yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-359">You can configure this setting through hello operation options:</span></span>

```json
"triggers": {
    "mytrigger": {
        "type": "http",
        "inputs": { ... },
        "recurrence": { ... },
        "operationOptions": "singleInstance"
    }
}
```

## <a name="types-and-inputs"></a><span data-ttu-id="f0cdf-360">Türleri ve girişleri</span><span class="sxs-lookup"><span data-stu-id="f0cdf-360">Types and inputs</span></span>  

<span data-ttu-id="f0cdf-361">Eylemler, her benzersiz davranışına sahip birçok tür vardır.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-361">There are many types of actions, each with unique behavior.</span></span> <span data-ttu-id="f0cdf-362">Koleksiyon Eylemler kendisini içinde birçok diğer eylemler içerebilir.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-362">Collection actions may contain many other actions within itself.</span></span>

### <a name="standard-actions"></a><span data-ttu-id="f0cdf-363">Standart Eylemler</span><span class="sxs-lookup"><span data-stu-id="f0cdf-363">Standard actions</span></span>  

-   <span data-ttu-id="f0cdf-364">**HTTP** bir HTTP web uç noktası bu eylemi çağırır.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-364">**HTTP** This action calls an HTTP web endpoint.</span></span>  
  
-   <span data-ttu-id="f0cdf-365">**ApiConnection** \- Bu eylem HTTP eylemi hello gibi davranır, ancak kullanır hello Microsoft tarafından yönetilen API'ler.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-365">**ApiConnection** \- This action behaves like hello HTTP action, but uses hello Microsoft-managed APIs.</span></span>  
  
-   <span data-ttu-id="f0cdf-366">**ApiConnectionWebhook** \- gibi HTTPWebhook ancak kullanır hello Microsoft tarafından yönetilen API'ler.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-366">**ApiConnectionWebhook** \- Like HTTPWebhook, but uses hello Microsoft-managed APIs.</span></span>  
  
-   <span data-ttu-id="f0cdf-367">**Yanıt** \- gelen bir arama için bir yanıt bu eylemi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-367">**Response** \- This action defines a response for an incoming call.</span></span>  
  
-   <span data-ttu-id="f0cdf-368">**Bekleyin** \- bu basit işlem sabit bir tutar saat veya belirli bir süre kadar bekler.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-368">**Wait** \- This simple action waits a fixed amount of time or until a specific time.</span></span>  
  
-   <span data-ttu-id="f0cdf-369">**İş akışı** \- Bu eylem bir iç içe geçmiş iş akışını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-369">**Workflow** \- This action represents a nested workflow.</span></span>  

-   <span data-ttu-id="f0cdf-370">**İşlev** \- Bu eylem bir Azure işlevi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-370">**Function** \- This action represents an Azure Function.</span></span>

### <a name="collection-actions"></a><span data-ttu-id="f0cdf-371">Koleksiyon Eylemler</span><span class="sxs-lookup"><span data-stu-id="f0cdf-371">Collection actions</span></span>

-   <span data-ttu-id="f0cdf-372">**Kapsam** \- bu eylemi diğer Eylemler, mantıksal bir gruplandırmasıdır.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-372">**Scope** \- This action is a logical grouping of other actions.</span></span>

-   <span data-ttu-id="f0cdf-373">**Koşul** \- Bu eylem bir ifadeyi değerlendirir ve hello karşılık gelen sonuç dal yürütür.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-373">**Condition** \- This action evaluates an expression and executes hello corresponding result branch.</span></span>

-   <span data-ttu-id="f0cdf-374">**ForEach** \- döngü Bu eylem bir dizisini yineler ve her öğe için iç eylemleri gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-374">**ForEach** \- This looping action iterates through an array and performs inner actions for each item.</span></span>

-   <span data-ttu-id="f0cdf-375">**Kadar** \- tootrue bir koşul sonuçları kadar bu döngü eylem iç Eylemler yürütür.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-375">**Until** \- This looping action executes inner actions until a condition results tootrue.</span></span>
  
<span data-ttu-id="f0cdf-376">Her eylem farklı bir dizi türü **girişleri** bir eylemin davranışını tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-376">Each type of action has a different set of **inputs** that define an action's behavior.</span></span>  
  
## <a name="http-action"></a><span data-ttu-id="f0cdf-377">HTTP eylemi</span><span class="sxs-lookup"><span data-stu-id="f0cdf-377">HTTP action</span></span>  

<span data-ttu-id="f0cdf-378">HTTP Eylemler belirtilen uç noktasını çağırmak ve hello yanıt toodetermine hello iş akışının çalışması gerektiğini olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-378">HTTP actions call a specified endpoint and check hello response toodetermine whether hello workflow should run.</span></span> <span data-ttu-id="f0cdf-379">Merhaba **girişleri** nesnesini parametreleri gerekli tooconstruct hello HTTP çağrısı hello kümesini alır:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-379">hello **inputs** object takes hello set of parameters required tooconstruct hello HTTP call:</span></span>  
  
|<span data-ttu-id="f0cdf-380">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="f0cdf-380">Element name</span></span>|<span data-ttu-id="f0cdf-381">Gerekli</span><span class="sxs-lookup"><span data-stu-id="f0cdf-381">Required</span></span>|<span data-ttu-id="f0cdf-382">Tür</span><span class="sxs-lookup"><span data-stu-id="f0cdf-382">Type</span></span>|<span data-ttu-id="f0cdf-383">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f0cdf-383">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="f0cdf-384">Yöntemi</span><span class="sxs-lookup"><span data-stu-id="f0cdf-384">method</span></span>|<span data-ttu-id="f0cdf-385">Evet</span><span class="sxs-lookup"><span data-stu-id="f0cdf-385">Yes</span></span>|<span data-ttu-id="f0cdf-386">Dize</span><span class="sxs-lookup"><span data-stu-id="f0cdf-386">String</span></span>|<span data-ttu-id="f0cdf-387">HTTP yöntemleri aşağıdaki hello biri olabilir: **almak**, **POST**, **PUT**, **silmek**, **düzeltme eki**, veya  **HEAD**</span><span class="sxs-lookup"><span data-stu-id="f0cdf-387">Can be one of hello following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="f0cdf-388">URI</span><span class="sxs-lookup"><span data-stu-id="f0cdf-388">uri</span></span>|<span data-ttu-id="f0cdf-389">Evet</span><span class="sxs-lookup"><span data-stu-id="f0cdf-389">Yes</span></span>|<span data-ttu-id="f0cdf-390">Dize</span><span class="sxs-lookup"><span data-stu-id="f0cdf-390">String</span></span>|<span data-ttu-id="f0cdf-391">çağrılan hello http veya https uç noktası.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-391">hello http or https endpoint that is called.</span></span> <span data-ttu-id="f0cdf-392">En fazla uzunluğu 2 kilobayttır.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-392">Maximum length is 2 kilobytes.</span></span>|  
|<span data-ttu-id="f0cdf-393">Sorguları</span><span class="sxs-lookup"><span data-stu-id="f0cdf-393">queries</span></span>|<span data-ttu-id="f0cdf-394">Hayır</span><span class="sxs-lookup"><span data-stu-id="f0cdf-394">No</span></span>|<span data-ttu-id="f0cdf-395">Nesne</span><span class="sxs-lookup"><span data-stu-id="f0cdf-395">Object</span></span>|<span data-ttu-id="f0cdf-396">Merhaba sorgu parametreleri tooadd toohello URL'yi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-396">Represents hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="f0cdf-397">Örneğin, `"queries" : { "api-version": "2015-02-01" }` ekler `?api-version=2015-02-01` toohello URL.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-397">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="f0cdf-398">Üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="f0cdf-398">headers</span></span>|<span data-ttu-id="f0cdf-399">Hayır</span><span class="sxs-lookup"><span data-stu-id="f0cdf-399">No</span></span>|<span data-ttu-id="f0cdf-400">Nesne</span><span class="sxs-lookup"><span data-stu-id="f0cdf-400">Object</span></span>|<span data-ttu-id="f0cdf-401">Her toohello isteği gönderilir hello üstbilgilerinin temsil eder.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-401">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="f0cdf-402">Örneğin, tooset hello dil ve istek üzerine yazın:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="f0cdf-402">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="f0cdf-403">Gövde</span><span class="sxs-lookup"><span data-stu-id="f0cdf-403">body</span></span>|<span data-ttu-id="f0cdf-404">Hayır</span><span class="sxs-lookup"><span data-stu-id="f0cdf-404">No</span></span>|<span data-ttu-id="f0cdf-405">Nesne</span><span class="sxs-lookup"><span data-stu-id="f0cdf-405">Object</span></span>|<span data-ttu-id="f0cdf-406">Toohello endpoint gönderilen hello yükünü temsil eder.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-406">Represents hello payload that is sent toohello endpoint.</span></span>|  
|<span data-ttu-id="f0cdf-407">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="f0cdf-407">retryPolicy</span></span>|<span data-ttu-id="f0cdf-408">Hayır</span><span class="sxs-lookup"><span data-stu-id="f0cdf-408">No</span></span>|<span data-ttu-id="f0cdf-409">Nesne</span><span class="sxs-lookup"><span data-stu-id="f0cdf-409">Object</span></span>|<span data-ttu-id="f0cdf-410">Merhaba yeniden deneme davranışı 4xx veya 5xx hataları özelleştirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-410">Lets you customize hello retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="f0cdf-411">operationsOptions</span><span class="sxs-lookup"><span data-stu-id="f0cdf-411">operationsOptions</span></span>|<span data-ttu-id="f0cdf-412">Hayır</span><span class="sxs-lookup"><span data-stu-id="f0cdf-412">No</span></span>|<span data-ttu-id="f0cdf-413">Dize</span><span class="sxs-lookup"><span data-stu-id="f0cdf-413">String</span></span>|<span data-ttu-id="f0cdf-414">Özel davranışlar toooverride Hello kümesini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-414">Defines hello set of special behaviors toooverride.</span></span>|  
|<span data-ttu-id="f0cdf-415">Kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="f0cdf-415">authentication</span></span>|<span data-ttu-id="f0cdf-416">Hayır</span><span class="sxs-lookup"><span data-stu-id="f0cdf-416">No</span></span>|<span data-ttu-id="f0cdf-417">Nesne</span><span class="sxs-lookup"><span data-stu-id="f0cdf-417">Object</span></span>|<span data-ttu-id="f0cdf-418">İstek hello temsil hello yöntemi kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-418">Represents hello method that hello request should be authenticated.</span></span> <span data-ttu-id="f0cdf-419">Bu nesne üzerinde daha fazla bilgi için bkz [Scheduler giden bağlantı kimlik doğrulaması](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span><span class="sxs-lookup"><span data-stu-id="f0cdf-419">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span></span> <span data-ttu-id="f0cdf-420">Zamanlayıcı daha desteklenen bir özellik yok: `authority`.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-420">Beyond scheduler, there is one more supported property: `authority`.</span></span> <span data-ttu-id="f0cdf-421">Varsayılan olarak, `https://login.windows.net` belirtilmediğinde, ancak gibi farklı bir kitleye kullanabilirsiniz`https://login.windows\-ppe.net`</span><span class="sxs-lookup"><span data-stu-id="f0cdf-421">By default, this is `https://login.windows.net` when not specified, but you can use a different audience like `https://login.windows\-ppe.net`</span></span>|  
  
<span data-ttu-id="f0cdf-422">HTTP Eylemler \(ve API bağlantısı\) Eylemler destek ilkeleri yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-422">HTTP actions \(and API Connection\) actions support retry policies.</span></span> <span data-ttu-id="f0cdf-423">Bir yeniden deneme ilkesi toointermittent hataları, HTTP durum işlemleri uygular kodları 408, 429 ve ayrıca tooany bağlantı özel durumlarda 5xx.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-423">A retry policy applies toointermittent failures, characterized as HTTP status codes 408, 429, and 5xx, in addition tooany connectivity exceptions.</span></span> <span data-ttu-id="f0cdf-424">Bu ilke hello kullanarak açıklanan *retryPolicy* aşağıda gösterildiği gibi tanımlanan nesnesi:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-424">This policy is described using hello *retryPolicy* object defined as shown here:</span></span>
  
```json
"retryPolicy" : {
    "type": "<type-of-retry-policy>",
    "interval": <retry-interval>,
    "count": <number-of-retry-attempts>
}
```
  
<span data-ttu-id="f0cdf-425">Merhaba yeniden deneme aralığı hello ISO 8601 biçiminde belirtilir.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-425">hello retry interval is specified in hello ISO 8601 format.</span></span> <span data-ttu-id="f0cdf-426">Hello en büyük değer bir saat olsa da bu aralık varsayılan ve 20 saniye, en küçük değerini sahiptir.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-426">This interval has a default and minimum value of 20 seconds, while hello maximum value is one hour.</span></span> <span data-ttu-id="f0cdf-427">Merhaba varsayılan ve en fazla yeniden deneme sayısı dört saattir.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-427">hello default and maximum retry count is four hours.</span></span> <span data-ttu-id="f0cdf-428">Merhaba yeniden deneme ilkesi tanımı belirtilmezse, bir `fixed` stratejisi varsayılan yeniden deneme sayısı ve aralığı değerlerle kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-428">If hello retry policy definition is not specified, a `fixed` strategy is used with default retry count and interval values.</span></span> <span data-ttu-id="f0cdf-429">toodisable hello yeniden deneme İlkesi ayarlamak türü çok`None`.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-429">toodisable hello retry policy, set its type too`None`.</span></span>  
  
<span data-ttu-id="f0cdf-430">Her denemesi arasındaki 30 saniyelik gecikmeyle üç yürütmeleri toplam aralıklı hatalar varsa örneğin, hello aşağıdaki eylemi getirilirken hello en son haberleri iki kez yeniden dener:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-430">For example, hello following action retries fetching hello latest news two times, if there are intermittent failures, for a total of three executions, with a 30-second delay between each attempt:</span></span>  
  
```json
"latestNews" : {
    "type": "http",
    "inputs": {
        "method": "GET",
        "uri": "https://mynews.example.com/latest",
        "retryPolicy" : {
            "type": "fixed",
            "interval": "PT30S",
            "count": 2
        }
    }
}
```
### <a name="asynchronous-patterns"></a><span data-ttu-id="f0cdf-431">Zaman uyumsuz desenleri</span><span class="sxs-lookup"><span data-stu-id="f0cdf-431">Asynchronous patterns</span></span>

<span data-ttu-id="f0cdf-432">Varsayılan olarak, tüm HTTP tabanlı eylemleri hello standart zaman uyumsuz işlem düzenini destekler.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-432">By default, all HTTP-based actions support hello standard asynchronous operation pattern.</span></span> <span data-ttu-id="f0cdf-433">Merhaba uzak sunucu bu hello istek gösterirse bir 202 işleme için kabul edilir şekilde \(kabul edilen\) yanıtı hello Logic Apps altyapısı tutar yoklama terminal ulaşmasını kadar hello yanıtın konumu üstbilgisinde belirtilen hello URL'si durumu \(olmayan bir\-202 yanıt\).</span><span class="sxs-lookup"><span data-stu-id="f0cdf-433">So if hello remote server indicates that hello request is accepted for processing with a 202 \(Accepted\) response, hello Logic Apps engine keeps polling hello URL specified in hello response's location header until reaching a terminal state \(a non\-202 response\).</span></span>  
  
<span data-ttu-id="f0cdf-434">toodisable hello zaman uyumsuz davranışı, daha önce açıklandığı gibi ayarlanmış bir `DisableAsyncPattern` hello eylem girişleri seçeneği.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-434">toodisable hello asynchronous behavior previously described, set a `DisableAsyncPattern` option in hello action inputs.</span></span> <span data-ttu-id="f0cdf-435">Bu durumda, hello eylemin hello çıktı hello ilk 202 yanıt hello sunucusundan temel alır.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-435">In this case, hello output of hello action is based on hello initial 202 response from hello server.</span></span>  
  
```json
"invokeLongRunningOperation" : {
    "type": "http",
    "inputs": {
        "method": "POST",
        "uri": "https://host.example.com/resources"
    },
    "operationOptions": "DisableAsyncPattern"
}
```

#### <a name="asynchronous-limits"></a><span data-ttu-id="f0cdf-436">Zaman uyumsuz sınırları</span><span class="sxs-lookup"><span data-stu-id="f0cdf-436">Asynchronous Limits</span></span>

<span data-ttu-id="f0cdf-437">Zaman uyumsuz desen kendi süresi tooa belirli bir zaman aralığı içinde sınırlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-437">An asynchronous pattern can be limited in its duration tooa specific time interval.</span></span>  <span data-ttu-id="f0cdf-438">Terminal durumuna erişmeden Hello zaman aralığı sona erdiğinde, hello eylemin hello durumunu işaretlenecek `Cancelled` koduyla `ActionTimedOut`.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-438">If hello time interval elapses without reaching a terminal state, hello status of hello action will be marked `Cancelled` with a code of `ActionTimedOut`.</span></span>  <span data-ttu-id="f0cdf-439">ISO 8601 biçiminde Hello sınırı zaman aşımı belirtildi.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-439">hello limit timeout is specified in ISO 8601 format.</span></span>  <span data-ttu-id="f0cdf-440">Sınırları sözdizimi aşağıdaki hello ile belirtilebilir:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-440">Limits can be specified with hello following syntax:</span></span>

``` json
"<action-name>": {
    "type": "workflow|webhook|http|apiconnectionwebhook|apiconnection",
    "inputs": { },
    "limit": {
        "timeout": "PT10S"
    }
}
```
  
## <a name="api-connection"></a><span data-ttu-id="f0cdf-441">API bağlantısı</span><span class="sxs-lookup"><span data-stu-id="f0cdf-441">API Connection</span></span>  

<span data-ttu-id="f0cdf-442">API bağlantı Microsoft tarafından yönetilen bir bağlayıcı başvuruda bulunan bir eylemdir.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-442">API Connection is an action that references a Microsoft-managed connector.</span></span>
<span data-ttu-id="f0cdf-443">Bu eylem, bir başvuru tooa geçerli bağlantı ve hello API ve gerekli parametreleri hakkında bilgi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-443">This action requires a reference tooa valid connection, and information on hello API and parameters required.</span></span>

|<span data-ttu-id="f0cdf-444">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="f0cdf-444">Element name</span></span>|<span data-ttu-id="f0cdf-445">Gerekli</span><span class="sxs-lookup"><span data-stu-id="f0cdf-445">Required</span></span>|<span data-ttu-id="f0cdf-446">Tür</span><span class="sxs-lookup"><span data-stu-id="f0cdf-446">Type</span></span>|<span data-ttu-id="f0cdf-447">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f0cdf-447">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="f0cdf-448">ana bilgisayar</span><span class="sxs-lookup"><span data-stu-id="f0cdf-448">host</span></span>|<span data-ttu-id="f0cdf-449">Evet</span><span class="sxs-lookup"><span data-stu-id="f0cdf-449">Yes</span></span>|<span data-ttu-id="f0cdf-450">Nesne</span><span class="sxs-lookup"><span data-stu-id="f0cdf-450">Object</span></span>|<span data-ttu-id="f0cdf-451">Merhaba runtimeUrl ve başvuru toohello bağlantı nesnesi gibi Hello bağlayıcı bilgileri temsil eder</span><span class="sxs-lookup"><span data-stu-id="f0cdf-451">Represents hello connector information such as hello runtimeUrl and reference toohello connection object</span></span>|
|<span data-ttu-id="f0cdf-452">Yöntemi</span><span class="sxs-lookup"><span data-stu-id="f0cdf-452">method</span></span>|<span data-ttu-id="f0cdf-453">Evet</span><span class="sxs-lookup"><span data-stu-id="f0cdf-453">Yes</span></span>|<span data-ttu-id="f0cdf-454">Dize</span><span class="sxs-lookup"><span data-stu-id="f0cdf-454">String</span></span>|<span data-ttu-id="f0cdf-455">HTTP yöntemleri aşağıdaki hello biri olabilir: **almak**, **POST**, **PUT**, **silmek**, **düzeltme eki**, veya  **HEAD**</span><span class="sxs-lookup"><span data-stu-id="f0cdf-455">Can be one of hello following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="f0cdf-456">Yol</span><span class="sxs-lookup"><span data-stu-id="f0cdf-456">path</span></span>|<span data-ttu-id="f0cdf-457">Evet</span><span class="sxs-lookup"><span data-stu-id="f0cdf-457">Yes</span></span>|<span data-ttu-id="f0cdf-458">Dize</span><span class="sxs-lookup"><span data-stu-id="f0cdf-458">String</span></span>|<span data-ttu-id="f0cdf-459">Merhaba API işlemi Hello yolu.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-459">hello path of hello API operation.</span></span>|  
|<span data-ttu-id="f0cdf-460">Sorguları</span><span class="sxs-lookup"><span data-stu-id="f0cdf-460">queries</span></span>|<span data-ttu-id="f0cdf-461">Hayır</span><span class="sxs-lookup"><span data-stu-id="f0cdf-461">No</span></span>|<span data-ttu-id="f0cdf-462">Nesne</span><span class="sxs-lookup"><span data-stu-id="f0cdf-462">Object</span></span>|<span data-ttu-id="f0cdf-463">Merhaba sorgu parametreleri tooadd toohello URL'yi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-463">Represents hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="f0cdf-464">Örneğin, `"queries" : { "api-version": "2015-02-01" }` ekler `?api-version=2015-02-01` toohello URL.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-464">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="f0cdf-465">Üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="f0cdf-465">headers</span></span>|<span data-ttu-id="f0cdf-466">Hayır</span><span class="sxs-lookup"><span data-stu-id="f0cdf-466">No</span></span>|<span data-ttu-id="f0cdf-467">Nesne</span><span class="sxs-lookup"><span data-stu-id="f0cdf-467">Object</span></span>|<span data-ttu-id="f0cdf-468">Her toohello isteği gönderilir hello üstbilgilerinin temsil eder.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-468">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="f0cdf-469">Örneğin, tooset hello dil ve istek üzerine yazın:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="f0cdf-469">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="f0cdf-470">Gövde</span><span class="sxs-lookup"><span data-stu-id="f0cdf-470">body</span></span>|<span data-ttu-id="f0cdf-471">Hayır</span><span class="sxs-lookup"><span data-stu-id="f0cdf-471">No</span></span>|<span data-ttu-id="f0cdf-472">Nesne</span><span class="sxs-lookup"><span data-stu-id="f0cdf-472">Object</span></span>|<span data-ttu-id="f0cdf-473">Toohello endpoint gönderilen hello yükünü temsil eder.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-473">Represents hello payload that is sent toohello endpoint.</span></span>|  
|<span data-ttu-id="f0cdf-474">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="f0cdf-474">retryPolicy</span></span>|<span data-ttu-id="f0cdf-475">Hayır</span><span class="sxs-lookup"><span data-stu-id="f0cdf-475">No</span></span>|<span data-ttu-id="f0cdf-476">Nesne</span><span class="sxs-lookup"><span data-stu-id="f0cdf-476">Object</span></span>|<span data-ttu-id="f0cdf-477">Merhaba yeniden deneme davranışı 4xx veya 5xx hataları özelleştirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-477">Lets you customize hello retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="f0cdf-478">operationsOptions</span><span class="sxs-lookup"><span data-stu-id="f0cdf-478">operationsOptions</span></span>|<span data-ttu-id="f0cdf-479">Hayır</span><span class="sxs-lookup"><span data-stu-id="f0cdf-479">No</span></span>|<span data-ttu-id="f0cdf-480">Dize</span><span class="sxs-lookup"><span data-stu-id="f0cdf-480">String</span></span>|<span data-ttu-id="f0cdf-481">Özel davranışlar toooverride Hello kümesini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-481">Defines hello set of special behaviors toooverride.</span></span>|  

```json
"Send_Email": {
    "type": "apiconnection",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-df.azure-apim.net/apim/office365"
            },
            "connection": {
                "name": "@parameters('$connections')['office365']['connectionId']"
            }
        },
        "method": "post",
        "body": {
            "Subject": "New Tweet from @{triggerBody()['TweetedBy']}",
            "Body": "@{triggerBody()['TweetText']}",
            "To": "me@example.com"
        },
        "path": "/Mail"
    },
    "runAfter": {}
    }
```

## <a name="api-connection-webhook-action"></a><span data-ttu-id="f0cdf-482">API bağlantısı Web kancası eylemi</span><span class="sxs-lookup"><span data-stu-id="f0cdf-482">API Connection webhook action</span></span>

```json
"Send_approval_email": {
    "type": "apiconnectionwebhook",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-df.azure-apim.net/apim/office365"
            },
            "connection": {
                "name": "@parameters('$connections')['office365']['connectionId']"
            }
        },
        "body": {
            "Message": {
                "Subject": "Approval Request",
                "Options": "Approve, Reject",
                "Importance": "Normal",
                "To": "me@email.com"
            }
        },
        "path": "/approvalmail",
        "authentication": "@parameters('$authentication')"
    },
    "runAfter": {}
}
```

<span data-ttu-id="f0cdf-483">Bir Web kancası eylemi sınırları hello belirtilebilir aynı şekilde [HTTP zaman uyumsuz sınırları](#asynchronous-limits).</span><span class="sxs-lookup"><span data-stu-id="f0cdf-483">Limits on a webhook action can be specified in hello same manner as [HTTP Asynchronous Limits](#asynchronous-limits).</span></span>
  
## <a name="response-action"></a><span data-ttu-id="f0cdf-484">Yanıt eylemi</span><span class="sxs-lookup"><span data-stu-id="f0cdf-484">Response action</span></span>  

<span data-ttu-id="f0cdf-485">Bu eylem türü bir HTTP isteğinden hello tüm yanıt yükü içerir ve bir statusCode, metnini ve üst bilgileri içerir:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-485">This action type contains hello entire response payload from an HTTP request and includes a statusCode, body, and headers:</span></span>  
  
```json
"myresponse" : {
    "type" : "response",
    "inputs" : {
        "statusCode" : 200,
        "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        },
        "headers" : {
            "x-ms-date" : "@utcnow()",
            "Content-type" : "application/json"
        }
    },
    "runAfter": {}
}
```
  
<span data-ttu-id="f0cdf-486">Merhaba yanıt eylem tooother Eylemler uygulanmaz özel sınırlamalar vardır.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-486">hello response action has special restrictions that don't apply tooother actions.</span></span> <span data-ttu-id="f0cdf-487">Bu avantajlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-487">Specifically:</span></span>  
  
-   <span data-ttu-id="f0cdf-488">Belirleyici yanıt toohello gelen isteği gerektiğinden yanıt eylemlerinizi bir tanım paralel olamaz.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-488">Response actions cannot be parallel in a definition because a deterministic response toohello incoming request is required.</span></span>  
  
-   <span data-ttu-id="f0cdf-489">Merhaba gelen istek yanıt aldıktan sonra bir yanıt eylemi ulaştıysanız, hello eylem olarak kabul başarısız \(çakışma\), ve bunun sonucunda çalıştırmak hello `Failed`.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-489">If a response action is reached after hello incoming request has received a response, hello action is considered failed \(conflict\), and as a result, hello run is `Failed`.</span></span>  
  
-   <span data-ttu-id="f0cdf-490">Yanıt eylemleri içeren bir iş akışının olamaz `splitOn` , tetikleyici içinde birçok çalışır bir çağrı neden olduğundan.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-490">A workflow with Response actions cannot have `splitOn` in its trigger because one call causes many runs.</span></span> <span data-ttu-id="f0cdf-491">Sonuç olarak, Hello akış PUT ve nedeni hatalı istek olduğunda bu doğrulanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-491">As a result, this should be validated when hello flow is PUT and cause a Bad Request.</span></span>  
  
## <a name="wait-action"></a><span data-ttu-id="f0cdf-492">Eylem bekleyin</span><span class="sxs-lookup"><span data-stu-id="f0cdf-492">Wait action</span></span>  

<span data-ttu-id="f0cdf-493">Merhaba `wait` eylemin hello belirtilen zaman aralığı için iş akışı yürütme askıya alır.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-493">hello `wait` action suspends workflow execution for hello specified interval.</span></span> <span data-ttu-id="f0cdf-494">Örneğin, toowait 15 dakika, bu kod parçacığında kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-494">For example, toowait 15 minutes, you can use this snippet:</span></span>  
  
```json
"waitForFifteenMinutes" : {
    "type": "wait",
    "inputs": {
        "interval": {
            "unit" : "minute",
            "count" : 15
        }
    }
}
```  
  
<span data-ttu-id="f0cdf-495">Alternatif olarak, toowait zaman belirli bir süre kadar bu örnek kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-495">Alternatively, toowait until a specific moment in time, you can use this example:</span></span>  
  
```json
"waitUntilOctober" : {
    "type": "wait",
    "inputs": {
        "until": {
            "timestamp" : "2016-10-01T00:00:00Z"
        }
    }
}
```
  
> [!NOTE]  
> <span data-ttu-id="f0cdf-496">Merhaba bekleme süresini ya da hello kullanılarak belirtilebilir **aralığı** nesne veya hello **kadar** nesnesi, ancak ikisini birden değil.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-496">hello wait duration can be either specified using hello **interval** object or hello **until** object, but not both.</span></span>  
  
|<span data-ttu-id="f0cdf-497">Ad</span><span class="sxs-lookup"><span data-stu-id="f0cdf-497">Name</span></span>|<span data-ttu-id="f0cdf-498">Gerekli</span><span class="sxs-lookup"><span data-stu-id="f0cdf-498">Required</span></span>|<span data-ttu-id="f0cdf-499">Tür</span><span class="sxs-lookup"><span data-stu-id="f0cdf-499">Type</span></span>|<span data-ttu-id="f0cdf-500">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f0cdf-500">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="f0cdf-501">interval</span><span class="sxs-lookup"><span data-stu-id="f0cdf-501">interval</span></span>|<span data-ttu-id="f0cdf-502">Hayır</span><span class="sxs-lookup"><span data-stu-id="f0cdf-502">No</span></span>|<span data-ttu-id="f0cdf-503">Nesne</span><span class="sxs-lookup"><span data-stu-id="f0cdf-503">Object</span></span>|<span data-ttu-id="f0cdf-504">Merhaba zaman miktarına göre süre bekleyin.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-504">hello wait duration based on amount of time.</span></span>|  
|<span data-ttu-id="f0cdf-505">aralığı birimi</span><span class="sxs-lookup"><span data-stu-id="f0cdf-505">interval unit</span></span>|<span data-ttu-id="f0cdf-506">Evet</span><span class="sxs-lookup"><span data-stu-id="f0cdf-506">Yes</span></span>|<span data-ttu-id="f0cdf-507">Dize</span><span class="sxs-lookup"><span data-stu-id="f0cdf-507">String</span></span>|<span data-ttu-id="f0cdf-508">Bu aralıklar birini: saniye, dakika, saat, gün, hafta, ay, yıl.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-508">One of these intervals: second, minute, hour, day, week, month, year.</span></span>|  
|<span data-ttu-id="f0cdf-509">Aralık sayısı</span><span class="sxs-lookup"><span data-stu-id="f0cdf-509">interval count</span></span>|<span data-ttu-id="f0cdf-510">Evet</span><span class="sxs-lookup"><span data-stu-id="f0cdf-510">Yes</span></span>|<span data-ttu-id="f0cdf-511">Dize</span><span class="sxs-lookup"><span data-stu-id="f0cdf-511">String</span></span>|<span data-ttu-id="f0cdf-512">İç birim verilen hello üzerinde temel süresi.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-512">Duration based on hello given internal unit.</span></span>|  
|<span data-ttu-id="f0cdf-513">kadar</span><span class="sxs-lookup"><span data-stu-id="f0cdf-513">until</span></span>|<span data-ttu-id="f0cdf-514">Hayır</span><span class="sxs-lookup"><span data-stu-id="f0cdf-514">No</span></span>|<span data-ttu-id="f0cdf-515">Nesne</span><span class="sxs-lookup"><span data-stu-id="f0cdf-515">Object</span></span>|<span data-ttu-id="f0cdf-516">Merhaba zamandaki bir noktasında temel süre bekleyin.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-516">hello wait duration based on a point in time.</span></span>|  
|<span data-ttu-id="f0cdf-517">zaman damgası kadar</span><span class="sxs-lookup"><span data-stu-id="f0cdf-517">until timestamp</span></span>|<span data-ttu-id="f0cdf-518">Evet</span><span class="sxs-lookup"><span data-stu-id="f0cdf-518">Yes</span></span>|<span data-ttu-id="f0cdf-519">Dize</span><span class="sxs-lookup"><span data-stu-id="f0cdf-519">String</span></span>|<span data-ttu-id="f0cdf-520">Dize &#124; hello bekleme süresi dolduğunda UTC zamanı başlangıç noktası.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-520">String&#124;hello point in time in UTC when hello wait expires.</span></span>|  

## <a name="query-action"></a><span data-ttu-id="f0cdf-521">Sorgu eylemi</span><span class="sxs-lookup"><span data-stu-id="f0cdf-521">Query action</span></span>

<span data-ttu-id="f0cdf-522">Merhaba `query` eylemi bir koşula göre bir dizi filtre olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-522">hello `query` action lets you filter an array based on a condition.</span></span> <span data-ttu-id="f0cdf-523">Örneğin, 2'den büyük tooselect sayılar, kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-523">For example, tooselect numbers greater than 2, you can use:</span></span>

```json
"FilterNumbers" : {
    "type": "query",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "where": "@greater(item(), 2)"
    }
}
```

<span data-ttu-id="f0cdf-524">Merhaba hello çıktısını `query` hello koşulu karşılıyor hello Giriş dizisinin öğelerinden sahip bir dizi eylemdir.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-524">hello output from hello `query` action is an array that has elements from hello input array that satisfy hello condition.</span></span>

> [!NOTE]
> <span data-ttu-id="f0cdf-525">Hiçbir değer hello belirtecini karşılıyorsa `where` koşul, hello boş bir dizi sonucudur.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-525">If no values satisfy hello `where` condition, hello result is an empty array.</span></span>

|<span data-ttu-id="f0cdf-526">Ad</span><span class="sxs-lookup"><span data-stu-id="f0cdf-526">Name</span></span>|<span data-ttu-id="f0cdf-527">Gerekli</span><span class="sxs-lookup"><span data-stu-id="f0cdf-527">Required</span></span>|<span data-ttu-id="f0cdf-528">Tür</span><span class="sxs-lookup"><span data-stu-id="f0cdf-528">Type</span></span>|<span data-ttu-id="f0cdf-529">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f0cdf-529">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="f0cdf-530">Kaynak</span><span class="sxs-lookup"><span data-stu-id="f0cdf-530">from</span></span>|<span data-ttu-id="f0cdf-531">Evet</span><span class="sxs-lookup"><span data-stu-id="f0cdf-531">Yes</span></span>|<span data-ttu-id="f0cdf-532">Dizi</span><span class="sxs-lookup"><span data-stu-id="f0cdf-532">Array</span></span>|<span data-ttu-id="f0cdf-533">Merhaba kaynak dizi.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-533">hello source array.</span></span>|
|<span data-ttu-id="f0cdf-534">Burada</span><span class="sxs-lookup"><span data-stu-id="f0cdf-534">where</span></span>|<span data-ttu-id="f0cdf-535">Evet</span><span class="sxs-lookup"><span data-stu-id="f0cdf-535">Yes</span></span>|<span data-ttu-id="f0cdf-536">Dize</span><span class="sxs-lookup"><span data-stu-id="f0cdf-536">String</span></span>|<span data-ttu-id="f0cdf-537">Merhaba kaynak dizinin Hello koşulu tooapply tooeach öğesi.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-537">hello condition tooapply tooeach element of hello source array.</span></span>|

## <a name="select-action"></a><span data-ttu-id="f0cdf-538">Bir eylem seçin</span><span class="sxs-lookup"><span data-stu-id="f0cdf-538">Select action</span></span>

<span data-ttu-id="f0cdf-539">Merhaba `select` eylem yeni bir değer dizideki her öğe proje olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-539">hello `select` action lets you project each element of an array into a new value.</span></span>
<span data-ttu-id="f0cdf-540">Örneğin, bir dizi sayılara nesnelerinin dizisi tooconvert kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-540">For example, tooconvert an array of numbers into an array of objects, you can use:</span></span>

```json
"SelectNumbers" : {
    "type": "select",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "select": { "number": "@item()" }
    }
}
```

<span data-ttu-id="f0cdf-541">Merhaba hello çıktısını `select` aynı kardinalite olarak dönüştürülen her bir öğesiyle Giriş dizisinin hello olarak tanımlanan hello hello tarafından sahip bir dizi eylemdir `select` özelliği.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-541">hello output of hello `select` action is an array that has hello same cardinality as hello input array, with each element transformed as defined by hello `select` property.</span></span> <span data-ttu-id="f0cdf-542">Merhaba giriş boş bir dizi hello çıktı da boş bir dizi ise.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-542">If hello input is an empty array, hello output is also an empty array.</span></span>

|<span data-ttu-id="f0cdf-543">Ad</span><span class="sxs-lookup"><span data-stu-id="f0cdf-543">Name</span></span>|<span data-ttu-id="f0cdf-544">Gerekli</span><span class="sxs-lookup"><span data-stu-id="f0cdf-544">Required</span></span>|<span data-ttu-id="f0cdf-545">Tür</span><span class="sxs-lookup"><span data-stu-id="f0cdf-545">Type</span></span>|<span data-ttu-id="f0cdf-546">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f0cdf-546">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="f0cdf-547">Kaynak</span><span class="sxs-lookup"><span data-stu-id="f0cdf-547">from</span></span>|<span data-ttu-id="f0cdf-548">Evet</span><span class="sxs-lookup"><span data-stu-id="f0cdf-548">Yes</span></span>|<span data-ttu-id="f0cdf-549">Dizi</span><span class="sxs-lookup"><span data-stu-id="f0cdf-549">Array</span></span>|<span data-ttu-id="f0cdf-550">Merhaba kaynak dizi.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-550">hello source array.</span></span>|
|<span data-ttu-id="f0cdf-551">seçin</span><span class="sxs-lookup"><span data-stu-id="f0cdf-551">select</span></span>|<span data-ttu-id="f0cdf-552">Evet</span><span class="sxs-lookup"><span data-stu-id="f0cdf-552">Yes</span></span>|<span data-ttu-id="f0cdf-553">Herhangi biri</span><span class="sxs-lookup"><span data-stu-id="f0cdf-553">Any</span></span>|<span data-ttu-id="f0cdf-554">Merhaba kaynak dizinin Hello projeksiyon tooapply tooeach öğesi.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-554">hello projection tooapply tooeach element of hello source array.</span></span>|

## <a name="terminate-action"></a><span data-ttu-id="f0cdf-555">Sonlandırma eylemi</span><span class="sxs-lookup"><span data-stu-id="f0cdf-555">Terminate action</span></span>

<span data-ttu-id="f0cdf-556">Merhaba sonlandırma eyleminin yürütülen tüm eylemler durduruluyor ve kalan herhangi bir eylem atlanıyor Çalıştır hello iş akışının yürütülmesini durdurur.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-556">hello Terminate action stops execution of hello workflow run, aborting any in-flight actions, and skipping any remaining actions.</span></span> <span data-ttu-id="f0cdf-557">Örneğin, tooterminate durumuna sahip bir Farklı Çalıştır **başarısız**, aşağıdaki kod parçacığında hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-557">For example, tooterminate a run with status **Failed**, you can use hello following snippet:</span></span>

```json
"HandleUnexpectedResponse" : {
    "type": "terminate",
    "inputs": {
        "runStatus" : "failed",
        "runError": {
            "code": "UnexpectedResponse",
            "message": "Received an unexpected response.",
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="f0cdf-558">Zaten tamamlanmış eylemler tarafından hello etkilenmez sonlandırma eylemi.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-558">Actions already completed are not affected by hello terminate action.</span></span>

|<span data-ttu-id="f0cdf-559">Ad</span><span class="sxs-lookup"><span data-stu-id="f0cdf-559">Name</span></span>|<span data-ttu-id="f0cdf-560">Gerekli</span><span class="sxs-lookup"><span data-stu-id="f0cdf-560">Required</span></span>|<span data-ttu-id="f0cdf-561">Tür</span><span class="sxs-lookup"><span data-stu-id="f0cdf-561">Type</span></span>|<span data-ttu-id="f0cdf-562">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f0cdf-562">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="f0cdf-563">runStatus</span><span class="sxs-lookup"><span data-stu-id="f0cdf-563">runStatus</span></span>|<span data-ttu-id="f0cdf-564">Evet</span><span class="sxs-lookup"><span data-stu-id="f0cdf-564">Yes</span></span>|<span data-ttu-id="f0cdf-565">Dize</span><span class="sxs-lookup"><span data-stu-id="f0cdf-565">String</span></span>|<span data-ttu-id="f0cdf-566">Merhaba hedef durumu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-566">hello target run status.</span></span> <span data-ttu-id="f0cdf-567">Her iki **başarısız** veya **iptal**.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-567">Either **Failed** or **Cancelled**.</span></span>|
|<span data-ttu-id="f0cdf-568">runError</span><span class="sxs-lookup"><span data-stu-id="f0cdf-568">runError</span></span>|<span data-ttu-id="f0cdf-569">Hayır</span><span class="sxs-lookup"><span data-stu-id="f0cdf-569">No</span></span>|<span data-ttu-id="f0cdf-570">Nesne</span><span class="sxs-lookup"><span data-stu-id="f0cdf-570">Object</span></span>|<span data-ttu-id="f0cdf-571">Merhaba hata ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-571">hello error details.</span></span> <span data-ttu-id="f0cdf-572">Ne zaman desteklenen yalnızca **runStatus** çok ayarlanır**başarısız**.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-572">Only supported when **runStatus** is set too**Failed**.</span></span>|
|<span data-ttu-id="f0cdf-573">runError kodu</span><span class="sxs-lookup"><span data-stu-id="f0cdf-573">runError code</span></span>|<span data-ttu-id="f0cdf-574">Hayır</span><span class="sxs-lookup"><span data-stu-id="f0cdf-574">No</span></span>|<span data-ttu-id="f0cdf-575">Dize</span><span class="sxs-lookup"><span data-stu-id="f0cdf-575">String</span></span>|<span data-ttu-id="f0cdf-576">Merhaba hata kodu çalıştırma.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-576">hello run error code.</span></span>|
|<span data-ttu-id="f0cdf-577">runError iletisi</span><span class="sxs-lookup"><span data-stu-id="f0cdf-577">runError message</span></span>|<span data-ttu-id="f0cdf-578">Hayır</span><span class="sxs-lookup"><span data-stu-id="f0cdf-578">No</span></span>|<span data-ttu-id="f0cdf-579">Dize</span><span class="sxs-lookup"><span data-stu-id="f0cdf-579">String</span></span>|<span data-ttu-id="f0cdf-580">Merhaba, hata iletisi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-580">hello run error message.</span></span>|

## <a name="compose-action"></a><span data-ttu-id="f0cdf-581">Eylem oluşturma</span><span class="sxs-lookup"><span data-stu-id="f0cdf-581">Compose action</span></span>

<span data-ttu-id="f0cdf-582">Merhaba Oluştur eylemi, rastgele bir nesne oluşturmak olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-582">hello Compose action lets you construct an arbitrary object.</span></span> <span data-ttu-id="f0cdf-583">Merhaba Hello çıktısını oluşturan eylem girdilerinden değerlendirme hello sonucudur.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-583">hello output of hello compose action is hello result of evaluating its inputs.</span></span> <span data-ttu-id="f0cdf-584">Örneğin, hello kullanabilirsiniz birden çok eylem eylem toomerge çıkışları oluşturun:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-584">For example, you can use hello compose action toomerge outputs of multiple actions:</span></span>

```json
"composeUserRecord" : {
    "type": "compose",
    "inputs": {
        "firstName": "@actions('getUser').firstName",
        "alias": "@actions('getUser').alias",
        "thumbnailLink": "@actions('lookupThumbnail').url"
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="f0cdf-585">Merhaba **oluşturma** eylem kullanılan tooconstruct nesneleri, dizileri ve yerel olarak XML ve ikili gibi mantıksal uygulamalar tarafından desteklenen herhangi bir türü de dahil olmak üzere herhangi bir çıktı olabilir.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-585">hello **Compose** action can be used tooconstruct any output, including objects, arrays, and any other type natively supported by logic apps like XML and binary.</span></span>

## <a name="table-action"></a><span data-ttu-id="f0cdf-586">Tablo eylemi</span><span class="sxs-lookup"><span data-stu-id="f0cdf-586">Table action</span></span>

<span data-ttu-id="f0cdf-587">Merhaba `table` öğeleri dizisi bir tooconvert sağlayan bir **CSV** veya **HTML** tablo.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-587">hello `table` allows you tooconvert an array of items into a **CSV** or **HTML** table.</span></span>

<span data-ttu-id="f0cdf-588">Varsayalım @triggerBody() değil</span><span class="sxs-lookup"><span data-stu-id="f0cdf-588">Suppose @triggerBody() is</span></span>

```json
[{
  "id": 0,
  "name": "apples"
},{
  "id": 1, 
  "name": "oranges"
}]
```

<span data-ttu-id="f0cdf-589">Ve hello eylem olarak tanımlanması izin verin</span><span class="sxs-lookup"><span data-stu-id="f0cdf-589">And let hello action be defined as</span></span>

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html"
    }
}
```

<span data-ttu-id="f0cdf-590">Yukarıdaki Hello oluşturur</span><span class="sxs-lookup"><span data-stu-id="f0cdf-590">hello above would produce</span></span>

<table><thead><tr><th><span data-ttu-id="f0cdf-591">id</span><span class="sxs-lookup"><span data-stu-id="f0cdf-591">id</span></span></th><th><span data-ttu-id="f0cdf-592">ad</span><span class="sxs-lookup"><span data-stu-id="f0cdf-592">name</span></span></th></tr></thead><tbody><tr><td><span data-ttu-id="f0cdf-593">0</span><span class="sxs-lookup"><span data-stu-id="f0cdf-593">0</span></span></td><td><span data-ttu-id="f0cdf-594">elmalar</span><span class="sxs-lookup"><span data-stu-id="f0cdf-594">apples</span></span></td></tr><tr><td><span data-ttu-id="f0cdf-595">1</span><span class="sxs-lookup"><span data-stu-id="f0cdf-595">1</span></span></td><td><span data-ttu-id="f0cdf-596">portakallar</span><span class="sxs-lookup"><span data-stu-id="f0cdf-596">oranges</span></span></td></tr></tbody></table><span data-ttu-id="f0cdf-597">"</span><span class="sxs-lookup"><span data-stu-id="f0cdf-597">"</span></span>

<span data-ttu-id="f0cdf-598">Sipariş toocustomize hello tabloda hello sütunları açıkça belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-598">In order toocustomize hello table, you can specify hello columns explicitly.</span></span> <span data-ttu-id="f0cdf-599">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-599">For example:</span></span>

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html",
        "columns": [{
          "header": "produce id",
          "value": "@item().id"
        },{
          "header": "description",
          "value": "@concat('fresh ', item().name)"
        }]
    }
}
```

<span data-ttu-id="f0cdf-600">Yukarıdaki Hello oluşturur</span><span class="sxs-lookup"><span data-stu-id="f0cdf-600">hello above would produce</span></span>

<table><thead><tr><th><span data-ttu-id="f0cdf-601">kimliği oluşturmak</span><span class="sxs-lookup"><span data-stu-id="f0cdf-601">produce id</span></span></th><th><span data-ttu-id="f0cdf-602">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f0cdf-602">description</span></span></th></tr></thead><tbody><tr><td><span data-ttu-id="f0cdf-603">0</span><span class="sxs-lookup"><span data-stu-id="f0cdf-603">0</span></span></td><td><span data-ttu-id="f0cdf-604">Yeni elmalar</span><span class="sxs-lookup"><span data-stu-id="f0cdf-604">fresh apples</span></span></td></tr><tr><td><span data-ttu-id="f0cdf-605">1</span><span class="sxs-lookup"><span data-stu-id="f0cdf-605">1</span></span></td><td><span data-ttu-id="f0cdf-606">Yeni portakallar</span><span class="sxs-lookup"><span data-stu-id="f0cdf-606">fresh oranges</span></span></td></tr></tbody></table><span data-ttu-id="f0cdf-607">"</span><span class="sxs-lookup"><span data-stu-id="f0cdf-607">"</span></span>

<span data-ttu-id="f0cdf-608">Merhaba, `from` özellik değeri boş bir dizi, hello çıkış boş bir tablo.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-608">If hello `from` property value is an empty array, hello output is an empty table.</span></span>

|<span data-ttu-id="f0cdf-609">Ad</span><span class="sxs-lookup"><span data-stu-id="f0cdf-609">Name</span></span>|<span data-ttu-id="f0cdf-610">Gerekli</span><span class="sxs-lookup"><span data-stu-id="f0cdf-610">Required</span></span>|<span data-ttu-id="f0cdf-611">Tür</span><span class="sxs-lookup"><span data-stu-id="f0cdf-611">Type</span></span>|<span data-ttu-id="f0cdf-612">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f0cdf-612">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="f0cdf-613">Kaynak</span><span class="sxs-lookup"><span data-stu-id="f0cdf-613">from</span></span>|<span data-ttu-id="f0cdf-614">Evet</span><span class="sxs-lookup"><span data-stu-id="f0cdf-614">Yes</span></span>|<span data-ttu-id="f0cdf-615">Dizi</span><span class="sxs-lookup"><span data-stu-id="f0cdf-615">Array</span></span>|<span data-ttu-id="f0cdf-616">Merhaba kaynak dizi.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-616">hello source array.</span></span>|
|<span data-ttu-id="f0cdf-617">Biçimi</span><span class="sxs-lookup"><span data-stu-id="f0cdf-617">format</span></span>|<span data-ttu-id="f0cdf-618">Evet</span><span class="sxs-lookup"><span data-stu-id="f0cdf-618">Yes</span></span>|<span data-ttu-id="f0cdf-619">Dize</span><span class="sxs-lookup"><span data-stu-id="f0cdf-619">String</span></span>|<span data-ttu-id="f0cdf-620">Biçim, ya da hello **CSV** veya **HTML**.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-620">hello format, either **CSV** or **HTML**.</span></span>|
|<span data-ttu-id="f0cdf-621">sütunları</span><span class="sxs-lookup"><span data-stu-id="f0cdf-621">columns</span></span>|<span data-ttu-id="f0cdf-622">Hayır</span><span class="sxs-lookup"><span data-stu-id="f0cdf-622">No</span></span>|<span data-ttu-id="f0cdf-623">Dizi</span><span class="sxs-lookup"><span data-stu-id="f0cdf-623">Array</span></span>|<span data-ttu-id="f0cdf-624">Merhaba sütun.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-624">hello columns.</span></span> <span data-ttu-id="f0cdf-625">Merhaba tablonun toooverride hello varsayılan şekil sağlar.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-625">Allows toooverride hello default shape of hello table.</span></span>|
|<span data-ttu-id="f0cdf-626">sütun başlığı</span><span class="sxs-lookup"><span data-stu-id="f0cdf-626">column header</span></span>|<span data-ttu-id="f0cdf-627">Hayır</span><span class="sxs-lookup"><span data-stu-id="f0cdf-627">No</span></span>|<span data-ttu-id="f0cdf-628">Dize</span><span class="sxs-lookup"><span data-stu-id="f0cdf-628">String</span></span>|<span data-ttu-id="f0cdf-629">Merhaba sütunun başlığını Hello.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-629">hello header of hello column.</span></span>|
|<span data-ttu-id="f0cdf-630">Sütun değeri</span><span class="sxs-lookup"><span data-stu-id="f0cdf-630">column value</span></span>|<span data-ttu-id="f0cdf-631">Evet</span><span class="sxs-lookup"><span data-stu-id="f0cdf-631">Yes</span></span>|<span data-ttu-id="f0cdf-632">Dize</span><span class="sxs-lookup"><span data-stu-id="f0cdf-632">String</span></span>|<span data-ttu-id="f0cdf-633">Merhaba sütunun Hello değeri.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-633">hello value of hello column.</span></span>|

## <a name="workflow-action"></a><span data-ttu-id="f0cdf-634">İş akışı eylemi</span><span class="sxs-lookup"><span data-stu-id="f0cdf-634">Workflow action</span></span>   

|<span data-ttu-id="f0cdf-635">Ad</span><span class="sxs-lookup"><span data-stu-id="f0cdf-635">Name</span></span>|<span data-ttu-id="f0cdf-636">Gerekli</span><span class="sxs-lookup"><span data-stu-id="f0cdf-636">Required</span></span>|<span data-ttu-id="f0cdf-637">Tür</span><span class="sxs-lookup"><span data-stu-id="f0cdf-637">Type</span></span>|<span data-ttu-id="f0cdf-638">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f0cdf-638">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="f0cdf-639">ana bilgisayar kimliği</span><span class="sxs-lookup"><span data-stu-id="f0cdf-639">host id</span></span>|<span data-ttu-id="f0cdf-640">Evet</span><span class="sxs-lookup"><span data-stu-id="f0cdf-640">Yes</span></span>|<span data-ttu-id="f0cdf-641">Dize</span><span class="sxs-lookup"><span data-stu-id="f0cdf-641">String</span></span>|<span data-ttu-id="f0cdf-642">Merhaba iş akışı toocall istediğiniz Hello kaynak kimliği.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-642">hello resource ID of hello workflow that you want toocall.</span></span>|  
|<span data-ttu-id="f0cdf-643">ana bilgisayar tetikleyiciadı</span><span class="sxs-lookup"><span data-stu-id="f0cdf-643">host triggerName</span></span>|<span data-ttu-id="f0cdf-644">Evet</span><span class="sxs-lookup"><span data-stu-id="f0cdf-644">Yes</span></span>|<span data-ttu-id="f0cdf-645">Dize</span><span class="sxs-lookup"><span data-stu-id="f0cdf-645">String</span></span>|<span data-ttu-id="f0cdf-646">tooinvoke istediğiniz hello tetikleyici Hello adı.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-646">hello name of hello trigger that you want tooinvoke.</span></span>|  
|<span data-ttu-id="f0cdf-647">Sorguları</span><span class="sxs-lookup"><span data-stu-id="f0cdf-647">queries</span></span>|<span data-ttu-id="f0cdf-648">Hayır</span><span class="sxs-lookup"><span data-stu-id="f0cdf-648">No</span></span>|<span data-ttu-id="f0cdf-649">Nesne</span><span class="sxs-lookup"><span data-stu-id="f0cdf-649">Object</span></span>|<span data-ttu-id="f0cdf-650">Merhaba sorgu parametreleri tooadd toohello URL'yi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-650">Represents hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="f0cdf-651">Örneğin, `"queries" : { "api-version": "2015-02-01" }` ekler `?api-version=2015-02-01` toohello URL.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-651">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="f0cdf-652">Üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="f0cdf-652">headers</span></span>|<span data-ttu-id="f0cdf-653">Hayır</span><span class="sxs-lookup"><span data-stu-id="f0cdf-653">No</span></span>|<span data-ttu-id="f0cdf-654">Nesne</span><span class="sxs-lookup"><span data-stu-id="f0cdf-654">Object</span></span>|<span data-ttu-id="f0cdf-655">Her toohello isteği gönderilir hello üstbilgilerinin temsil eder.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-655">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="f0cdf-656">Örneğin, tooset hello dil ve istek üzerine yazın:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="f0cdf-656">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="f0cdf-657">Gövde</span><span class="sxs-lookup"><span data-stu-id="f0cdf-657">body</span></span>|<span data-ttu-id="f0cdf-658">Hayır</span><span class="sxs-lookup"><span data-stu-id="f0cdf-658">No</span></span>|<span data-ttu-id="f0cdf-659">Nesne</span><span class="sxs-lookup"><span data-stu-id="f0cdf-659">Object</span></span>|<span data-ttu-id="f0cdf-660">Toohello endpoint gönderilen hello yükünü temsil eder.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-660">Represents hello payload sent toohello endpoint.</span></span>|  
  
```json
"mynestedwf" : {
    "type" : "workflow",
    "inputs" : {
        "host" : {
            "id" : "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Logic/mywf001",
            "triggerName " : "mytrigger001"
        },
        "queries" : {
            "extrafield" : "specialValue"
        },  
        "headers" : {
            "x-ms-date" : "@utcnow()",
            "Content-type" : "application/json"
        },
        "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        }
    },
    "runAfter": {}
    }
```
  
<span data-ttu-id="f0cdf-661">Bir erişim denetimi hello iş akışında yapılan \(daha belirgin olarak hello tetikleyici\), başka bir deyişle toohello iş akışı erişim.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-661">An access check is made on hello workflow \(more specifically, hello trigger\), meaning you need access toohello workflow.</span></span>  
  
<span data-ttu-id="f0cdf-662">Merhaba çıkarır hello `workflow` eylemin hello tanımlanan dayalı `response` hello alt iş akışı eylemi.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-662">hello outputs from hello `workflow` action are based on what you defined in hello `response` action in hello child workflow.</span></span> <span data-ttu-id="f0cdf-663">Herhangi bir tanımlamadığınız varsa `response` eylemi ve ardından hello çıkışları boş.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-663">If you have not defined any `response` action, then hello outputs are empty.</span></span>  

## <a name="function-action"></a><span data-ttu-id="f0cdf-664">İşlev eylemi</span><span class="sxs-lookup"><span data-stu-id="f0cdf-664">Function action</span></span>   

|<span data-ttu-id="f0cdf-665">Ad</span><span class="sxs-lookup"><span data-stu-id="f0cdf-665">Name</span></span>|<span data-ttu-id="f0cdf-666">Gerekli</span><span class="sxs-lookup"><span data-stu-id="f0cdf-666">Required</span></span>|<span data-ttu-id="f0cdf-667">Tür</span><span class="sxs-lookup"><span data-stu-id="f0cdf-667">Type</span></span>|<span data-ttu-id="f0cdf-668">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f0cdf-668">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="f0cdf-669">İşlev kimliği</span><span class="sxs-lookup"><span data-stu-id="f0cdf-669">function id</span></span>|<span data-ttu-id="f0cdf-670">Evet</span><span class="sxs-lookup"><span data-stu-id="f0cdf-670">Yes</span></span>|<span data-ttu-id="f0cdf-671">Dize</span><span class="sxs-lookup"><span data-stu-id="f0cdf-671">String</span></span>|<span data-ttu-id="f0cdf-672">tooinvoke istediğiniz hello işlevini Hello kaynak kimliği.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-672">hello resource ID of hello function that you want tooinvoke.</span></span>|  
|<span data-ttu-id="f0cdf-673">Yöntemi</span><span class="sxs-lookup"><span data-stu-id="f0cdf-673">method</span></span>|<span data-ttu-id="f0cdf-674">Hayır</span><span class="sxs-lookup"><span data-stu-id="f0cdf-674">No</span></span>|<span data-ttu-id="f0cdf-675">Dize</span><span class="sxs-lookup"><span data-stu-id="f0cdf-675">String</span></span>|<span data-ttu-id="f0cdf-676">Merhaba HTTP yöntemini tooinvoke hello işlevi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-676">hello HTTP method used tooinvoke hello function.</span></span> <span data-ttu-id="f0cdf-677">Varsayılan olarak, olmasından `POST` belirtilmemiş olduğunda.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-677">By default, it is `POST` when not specified.</span></span>|  
|<span data-ttu-id="f0cdf-678">Sorguları</span><span class="sxs-lookup"><span data-stu-id="f0cdf-678">queries</span></span>|<span data-ttu-id="f0cdf-679">Hayır</span><span class="sxs-lookup"><span data-stu-id="f0cdf-679">No</span></span>|<span data-ttu-id="f0cdf-680">Nesne</span><span class="sxs-lookup"><span data-stu-id="f0cdf-680">Object</span></span>|<span data-ttu-id="f0cdf-681">Merhaba sorgu parametreleri tooadd toohello URL'yi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-681">Represents hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="f0cdf-682">Örneğin, `"queries" : { "api-version": "2015-02-01" }` ekler `?api-version=2015-02-01` toohello URL.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-682">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="f0cdf-683">Üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="f0cdf-683">headers</span></span>|<span data-ttu-id="f0cdf-684">Hayır</span><span class="sxs-lookup"><span data-stu-id="f0cdf-684">No</span></span>|<span data-ttu-id="f0cdf-685">Nesne</span><span class="sxs-lookup"><span data-stu-id="f0cdf-685">Object</span></span>|<span data-ttu-id="f0cdf-686">Her toohello isteği gönderilir hello üstbilgilerinin temsil eder.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-686">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="f0cdf-687">Örneğin, tooset başlangıç dili ve istek üzerine türü: `"headers" : { "Accept-Language": "en-us" }`.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-687">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us" }`.</span></span>|  
|<span data-ttu-id="f0cdf-688">Gövde</span><span class="sxs-lookup"><span data-stu-id="f0cdf-688">body</span></span>|<span data-ttu-id="f0cdf-689">Hayır</span><span class="sxs-lookup"><span data-stu-id="f0cdf-689">No</span></span>|<span data-ttu-id="f0cdf-690">Nesne</span><span class="sxs-lookup"><span data-stu-id="f0cdf-690">Object</span></span>|<span data-ttu-id="f0cdf-691">Toohello endpoint gönderilen hello yükünü temsil eder.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-691">Represents hello payload sent toohello endpoint.</span></span>|  

```json
"myfunc" : {
    "type" : "Function",
    "inputs" : {
        "function" : {
            "id" : "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Web/sites/myfuncapp/functions/myfunc"
        },
        "queries" : {
            "extrafield" : "specialValue"
        },  
        "headers" : {
            "x-ms-date" : "@utcnow()"
        },
        "method" : "POST",
    "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        }
    },
    "runAfter": {}
}
```

<span data-ttu-id="f0cdf-692">Merhaba mantıksal uygulama kaydettiğinizde, biz başvurulan hello işlevi üzerinde bazı denetimler gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-692">When you save hello logic app, we perform some checks on hello referenced function:</span></span>
-   <span data-ttu-id="f0cdf-693">Toohave erişim toohello işlevi gerekir.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-693">You need toohave access toohello function.</span></span>
-   <span data-ttu-id="f0cdf-694">Yalnızca standart HTTP tetikleyicisi veya genel JSON Web kancası tetikleyici izin verilir.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-694">Only standard HTTP trigger or generic JSON webhook trigger is allowed.</span></span>
-   <span data-ttu-id="f0cdf-695">Tanımlı yol olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-695">It should not have any route defined.</span></span>
-   <span data-ttu-id="f0cdf-696">Yalnızca "işlev" ve "anonim" yetki düzeyini izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-696">Only "function" and "anonymous" authorization level is allowed.</span></span>

<span data-ttu-id="f0cdf-697">Merhaba tetikleme URL'si alınan, önbelleğe alınan ve çalışma zamanında kullanılan.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-697">hello trigger URL is retrieved, cached, and used at runtime.</span></span> <span data-ttu-id="f0cdf-698">Herhangi bir işlem önbelleğe hello URL geçersiz kılar, dolayısıyla hello eylem çalışma zamanında başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-698">So if any operation invalidates hello cached URL, hello action fails at runtime.</span></span> <span data-ttu-id="f0cdf-699">Bu, geçici toowork mantığı uygulama tooretrieve neden ve hello tetikleme URL'si tekrar önbelleğe hello mantıksal uygulama yeniden kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-699">toowork around this, save hello logic app again, which will cause logic app tooretrieve and cache hello trigger URL again.</span></span>

## <a name="collection-actions-scopes-and-loops"></a><span data-ttu-id="f0cdf-700">Koleksiyon eylemleri (kapsamlar ve döngüler)</span><span class="sxs-lookup"><span data-stu-id="f0cdf-700">Collection actions (scopes and loops)</span></span>

<span data-ttu-id="f0cdf-701">Bazı eylem türleri kendilerini içinde eylemler içerebilir.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-701">Some action types can contain actions within themselves.</span></span> <span data-ttu-id="f0cdf-702">Bir koleksiyon içinde başvurusu Eylemler doğrudan hello koleksiyonu dışında başvurulabilir.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-702">Reference actions within a collection can be referenced directly outside of hello collection.</span></span> <span data-ttu-id="f0cdf-703">Tanımladıysanız `http` bir kapsamda `@body('http')` herhangi bir iş akışında hala geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-703">If you defined `http` in a scope, `@body('http')` is still valid anywhere in a workflow.</span></span> <span data-ttu-id="f0cdf-704">Bir koleksiyon içinde eylemler için `runAfter` içindeki diğer eylemleri hello aynı koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-704">Actions within a collection can `runAfter` only other actions within hello same collection.</span></span>

## <a name="scope-action"></a><span data-ttu-id="f0cdf-705">Kapsam eylemi</span><span class="sxs-lookup"><span data-stu-id="f0cdf-705">Scope action</span></span>

<span data-ttu-id="f0cdf-706">Merhaba `scope` eylem sağlar, mantıksal olarak bir iş akışında Grup eylemler.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-706">hello `scope` action lets you logically group actions in a workflow.</span></span>

|<span data-ttu-id="f0cdf-707">Ad</span><span class="sxs-lookup"><span data-stu-id="f0cdf-707">Name</span></span>|<span data-ttu-id="f0cdf-708">Gerekli</span><span class="sxs-lookup"><span data-stu-id="f0cdf-708">Required</span></span>|<span data-ttu-id="f0cdf-709">Tür</span><span class="sxs-lookup"><span data-stu-id="f0cdf-709">Type</span></span>|<span data-ttu-id="f0cdf-710">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f0cdf-710">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="f0cdf-711">Eylemler</span><span class="sxs-lookup"><span data-stu-id="f0cdf-711">actions</span></span>|<span data-ttu-id="f0cdf-712">Evet</span><span class="sxs-lookup"><span data-stu-id="f0cdf-712">Yes</span></span>|<span data-ttu-id="f0cdf-713">Nesne</span><span class="sxs-lookup"><span data-stu-id="f0cdf-713">Object</span></span>|<span data-ttu-id="f0cdf-714">İç Eylemler tooexecute hello kapsam içinde</span><span class="sxs-lookup"><span data-stu-id="f0cdf-714">Inner actions tooexecute within hello scope</span></span>|

```json
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

## <a name="foreach-action"></a><span data-ttu-id="f0cdf-715">ForEach eylemi</span><span class="sxs-lookup"><span data-stu-id="f0cdf-715">ForEach action</span></span>

<span data-ttu-id="f0cdf-716">Bu döngü eylem bir dizisini yineler ve her öğe için iç eylemleri gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-716">This looping action iterates through an array and performs inner actions for each item.</span></span> <span data-ttu-id="f0cdf-717">Varsayılan olarak, paralel (20 yürütmeleri paralel birer birer) hello foreach döngüsü yürütür.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-717">By default, hello foreach loop executes in parallel (20 executions in parallel at a time).</span></span> <span data-ttu-id="f0cdf-718">Hello kullanarak yürütme kurallarını ayarlayabilmeniz için `operationOptions` parametresi.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-718">You can set execution rules using hello `operationOptions` parameter.</span></span>

|<span data-ttu-id="f0cdf-719">Ad</span><span class="sxs-lookup"><span data-stu-id="f0cdf-719">Name</span></span>|<span data-ttu-id="f0cdf-720">Gerekli</span><span class="sxs-lookup"><span data-stu-id="f0cdf-720">Required</span></span>|<span data-ttu-id="f0cdf-721">Tür</span><span class="sxs-lookup"><span data-stu-id="f0cdf-721">Type</span></span>|<span data-ttu-id="f0cdf-722">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f0cdf-722">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="f0cdf-723">Eylemler</span><span class="sxs-lookup"><span data-stu-id="f0cdf-723">actions</span></span>|<span data-ttu-id="f0cdf-724">Evet</span><span class="sxs-lookup"><span data-stu-id="f0cdf-724">Yes</span></span>|<span data-ttu-id="f0cdf-725">Nesne</span><span class="sxs-lookup"><span data-stu-id="f0cdf-725">Object</span></span>|<span data-ttu-id="f0cdf-726">İç Eylemler tooexecute hello döngü içinde</span><span class="sxs-lookup"><span data-stu-id="f0cdf-726">Inner actions tooexecute within hello loop</span></span>|
|<span data-ttu-id="f0cdf-727">foreach</span><span class="sxs-lookup"><span data-stu-id="f0cdf-727">foreach</span></span>|<span data-ttu-id="f0cdf-728">Evet</span><span class="sxs-lookup"><span data-stu-id="f0cdf-728">Yes</span></span>|<span data-ttu-id="f0cdf-729">Dize</span><span class="sxs-lookup"><span data-stu-id="f0cdf-729">string</span></span>|<span data-ttu-id="f0cdf-730">Merhaba dizi tooiterate üzerinden</span><span class="sxs-lookup"><span data-stu-id="f0cdf-730">hello array tooiterate over</span></span>|
|<span data-ttu-id="f0cdf-731">operationOptions</span><span class="sxs-lookup"><span data-stu-id="f0cdf-731">operationOptions</span></span>|<span data-ttu-id="f0cdf-732">Yok</span><span class="sxs-lookup"><span data-stu-id="f0cdf-732">no</span></span>|<span data-ttu-id="f0cdf-733">Dize</span><span class="sxs-lookup"><span data-stu-id="f0cdf-733">string</span></span>|<span data-ttu-id="f0cdf-734">İşlemi için herhangi bir seçenek davranışı.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-734">Any operation options for behavior.</span></span> <span data-ttu-id="f0cdf-735">Şu anda yalnızca destekler `sequential` tooexecute yineleme sırayla (varsayılan davranıştır paralel)</span><span class="sxs-lookup"><span data-stu-id="f0cdf-735">Currently only supports `sequential` tooexecute iterations sequentially (default behavior is parallel)</span></span>|

```json
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
                }
                "host": {
                    "connection": {
                        "id": "@parameters('$connections')['office365']['connection']['id']"
                    }
                }
            }
        }
    },
    "runAfter":{
        "email_filter": [ "Succeeded" ]
    }
}
```

## <a name="until-action"></a><span data-ttu-id="f0cdf-736">Eylem kadar</span><span class="sxs-lookup"><span data-stu-id="f0cdf-736">Until action</span></span>

<span data-ttu-id="f0cdf-737">Bir koşul tootrue sonuçları kadar bu döngü eylem iç Eylemler yürütür.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-737">This looping action executes inner actions until a condition results tootrue.</span></span>

|<span data-ttu-id="f0cdf-738">Ad</span><span class="sxs-lookup"><span data-stu-id="f0cdf-738">Name</span></span>|<span data-ttu-id="f0cdf-739">Gerekli</span><span class="sxs-lookup"><span data-stu-id="f0cdf-739">Required</span></span>|<span data-ttu-id="f0cdf-740">Tür</span><span class="sxs-lookup"><span data-stu-id="f0cdf-740">Type</span></span>|<span data-ttu-id="f0cdf-741">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f0cdf-741">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="f0cdf-742">Eylemler</span><span class="sxs-lookup"><span data-stu-id="f0cdf-742">actions</span></span>|<span data-ttu-id="f0cdf-743">Evet</span><span class="sxs-lookup"><span data-stu-id="f0cdf-743">Yes</span></span>|<span data-ttu-id="f0cdf-744">Nesne</span><span class="sxs-lookup"><span data-stu-id="f0cdf-744">Object</span></span>|<span data-ttu-id="f0cdf-745">İç Eylemler tooexecute hello döngü içinde</span><span class="sxs-lookup"><span data-stu-id="f0cdf-745">Inner actions tooexecute within hello loop</span></span>|
|<span data-ttu-id="f0cdf-746">ifade</span><span class="sxs-lookup"><span data-stu-id="f0cdf-746">expression</span></span>|<span data-ttu-id="f0cdf-747">Evet</span><span class="sxs-lookup"><span data-stu-id="f0cdf-747">Yes</span></span>|<span data-ttu-id="f0cdf-748">Dize</span><span class="sxs-lookup"><span data-stu-id="f0cdf-748">string</span></span>|<span data-ttu-id="f0cdf-749">Her yinelemeden sonra Hello ifade tooevaluate</span><span class="sxs-lookup"><span data-stu-id="f0cdf-749">hello expression tooevaluate after each iteration</span></span>|
|<span data-ttu-id="f0cdf-750">Sınırı</span><span class="sxs-lookup"><span data-stu-id="f0cdf-750">limit</span></span>|<span data-ttu-id="f0cdf-751">Evet</span><span class="sxs-lookup"><span data-stu-id="f0cdf-751">yes</span></span>|<span data-ttu-id="f0cdf-752">Nesne</span><span class="sxs-lookup"><span data-stu-id="f0cdf-752">Object</span></span>|<span data-ttu-id="f0cdf-753">Merhaba sınırları hello döngü - en az bir sınır için tanımlanmış olması gerekir</span><span class="sxs-lookup"><span data-stu-id="f0cdf-753">hello limits for hello loop - at least one limit must be defined</span></span>|
|<span data-ttu-id="f0cdf-754">Sayısı</span><span class="sxs-lookup"><span data-stu-id="f0cdf-754">count</span></span>|<span data-ttu-id="f0cdf-755">Yok</span><span class="sxs-lookup"><span data-stu-id="f0cdf-755">no</span></span>|<span data-ttu-id="f0cdf-756">Int</span><span class="sxs-lookup"><span data-stu-id="f0cdf-756">int</span></span>|<span data-ttu-id="f0cdf-757">Merhaba sınırı toohello gerçekleştirilebilir yineleme sayısı</span><span class="sxs-lookup"><span data-stu-id="f0cdf-757">hello limit toohello number of iterations that can be performed</span></span>|
|<span data-ttu-id="f0cdf-758">Zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="f0cdf-758">timeout</span></span>|<span data-ttu-id="f0cdf-759">Yok</span><span class="sxs-lookup"><span data-stu-id="f0cdf-759">no</span></span>|<span data-ttu-id="f0cdf-760">Dize</span><span class="sxs-lookup"><span data-stu-id="f0cdf-760">string</span></span>|<span data-ttu-id="f0cdf-761">ne kadar süreyle döndürmelidir için hello zaman aşımı.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-761">hello timeout for how long it should loop.</span></span>  <span data-ttu-id="f0cdf-762">ISO 8601 biçim</span><span class="sxs-lookup"><span data-stu-id="f0cdf-762">ISO 8601 format</span></span>|


```json
 "Until_succeeded": {
    "actions": {
        "Http": {
            "inputs": {
                "method": "GET",
                "uri": "http://myurl"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "expression": "@equals(outputs('Http')['statusCode', 200)",
    "limit": {
        "count": 1000,
        "timeout": "PT1H"
    },
    "runAfter": {},
    "type": "Until"
}
```

## <a name="conditions---if-action"></a><span data-ttu-id="f0cdf-763">-Varsa koşulları eylemi</span><span class="sxs-lookup"><span data-stu-id="f0cdf-763">Conditions - If Action</span></span>

<span data-ttu-id="f0cdf-764">Merhaba `If` eylem, bir koşulu değerlendirmek ve olup hello ifadeyi çok hesaplar üzerinde dayalı bir dal yürütme sağlar`true`.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-764">hello `If` action lets you evaluate a condition and execute a branch based on whether hello expression evaluates too`true`.</span></span>

|<span data-ttu-id="f0cdf-765">Ad</span><span class="sxs-lookup"><span data-stu-id="f0cdf-765">Name</span></span>|<span data-ttu-id="f0cdf-766">Gerekli</span><span class="sxs-lookup"><span data-stu-id="f0cdf-766">Required</span></span>|<span data-ttu-id="f0cdf-767">Tür</span><span class="sxs-lookup"><span data-stu-id="f0cdf-767">Type</span></span>|<span data-ttu-id="f0cdf-768">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f0cdf-768">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="f0cdf-769">Eylemler</span><span class="sxs-lookup"><span data-stu-id="f0cdf-769">actions</span></span>|<span data-ttu-id="f0cdf-770">Evet</span><span class="sxs-lookup"><span data-stu-id="f0cdf-770">Yes</span></span>|<span data-ttu-id="f0cdf-771">Nesne</span><span class="sxs-lookup"><span data-stu-id="f0cdf-771">Object</span></span>|<span data-ttu-id="f0cdf-772">İfade çok değerlendirirken, iç Eylemler tooexecute`true`</span><span class="sxs-lookup"><span data-stu-id="f0cdf-772">Inner actions tooexecute when expression evaluates too`true`</span></span>|
|<span data-ttu-id="f0cdf-773">ifade</span><span class="sxs-lookup"><span data-stu-id="f0cdf-773">expression</span></span>|<span data-ttu-id="f0cdf-774">Evet</span><span class="sxs-lookup"><span data-stu-id="f0cdf-774">Yes</span></span>|<span data-ttu-id="f0cdf-775">Dize</span><span class="sxs-lookup"><span data-stu-id="f0cdf-775">string</span></span>|<span data-ttu-id="f0cdf-776">Merhaba ifade tooevaluate</span><span class="sxs-lookup"><span data-stu-id="f0cdf-776">hello expression tooevaluate</span></span>|
|<span data-ttu-id="f0cdf-777">else</span><span class="sxs-lookup"><span data-stu-id="f0cdf-777">else</span></span>|<span data-ttu-id="f0cdf-778">Yok</span><span class="sxs-lookup"><span data-stu-id="f0cdf-778">no</span></span>|<span data-ttu-id="f0cdf-779">Nesne</span><span class="sxs-lookup"><span data-stu-id="f0cdf-779">Object</span></span>|<span data-ttu-id="f0cdf-780">İfade çok değerlendirirken, iç Eylemler tooexecute`false`</span><span class="sxs-lookup"><span data-stu-id="f0cdf-780">Inner actions tooexecute when expression evaluates too`false`</span></span>|
  
```json
"My_condition": {
    "actions": {
        "If_true": {
            "inputs": {
                "method": "GET",
                "uri": "http://myurl"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "else": {
        "actions": {
            "if_false": {
                "inputs": {
                    "method": "GET",
                    "uri": "http://myurl"
                },
                "runAfter": {},
                "type": "Http"
            }
        }
    },
    "expression": "@equals(triggerBody(), json(true))",
    "runAfter": {},
    "type": "If"
}
```  
  
<span data-ttu-id="f0cdf-781">Merhaba aşağıdaki tabloda koşullar bir eylemi ifade nasıl kullanabileceğiniz örnekler gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-781">hello following table shows examples of how conditions can use expressions in an action:</span></span>  
  
|<span data-ttu-id="f0cdf-782">JSON değeri</span><span class="sxs-lookup"><span data-stu-id="f0cdf-782">JSON value</span></span>|<span data-ttu-id="f0cdf-783">Sonuç</span><span class="sxs-lookup"><span data-stu-id="f0cdf-783">Result</span></span>|  
|--------------|----------|  
|`"expression": "@parameters('hasSpecialAction')"`|<span data-ttu-id="f0cdf-784">Tootrue değerlendirecek herhangi bir değer bu koşul toopass neden olur.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-784">Any value that would evaluate tootrue causes this condition toopass.</span></span> <span data-ttu-id="f0cdf-785">Yalnızca Boole ifadeleri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-785">Only Boolean expressions are supported.</span></span> <span data-ttu-id="f0cdf-786">tooconvert diğer türleri tooBoolean, kullanım işlevleri `empty`, `equals`.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-786">tooconvert other types tooBoolean, use functions `empty`, `equals`.</span></span>|  
|`"expression": "@greater(actions('act1').output.value, parameters('threshold'))"`|<span data-ttu-id="f0cdf-787">Karşılaştırma işlevleri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-787">Comparison functions are supported.</span></span> <span data-ttu-id="f0cdf-788">Act1 Hello çıktısını hello eşik değerinden yüksek olduğunda burada hello örneğin hello eylem yalnızca yürütür.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-788">For hello example here, hello action only executes when hello output of act1 is greater than hello threshold.</span></span>|  
|`"expression": "@or(greater(actions('act1').output.value, parameters('threshold')), less(actions('act1').output.value, 100))"`|<span data-ttu-id="f0cdf-789">Mantığı da desteklenen toocreate Boolean ifadeleri iç içe işlevlerdir.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-789">Logic functions are also supported toocreate nested Boolean expressions.</span></span> <span data-ttu-id="f0cdf-790">Bu durumda, act1 Hello çıktısını hello eşiğin üstünde veya altında 100 olduğunda hello eylem yürütür.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-790">In this case, hello action executes when hello output of act1 is above hello threshold or below 100.</span></span>|  
|`"expression": "@equals(length(actions('act1').outputs.errors), 0))"`|<span data-ttu-id="f0cdf-791">Bir dizinin tüm öğeleri varsa, dizi işlevleri toocheck kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-791">You can use array functions toocheck if an array has any items.</span></span> <span data-ttu-id="f0cdf-792">Bu durumda, Hello hataları dizi boş olduğunda hello eylem yürütür.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-792">In this case, hello action executes when hello errors array is empty.</span></span>| 
|`"expression": "parameters('hasSpecialAction')"`|<span data-ttu-id="f0cdf-793">Hata - geçerli bir @ için gerekli olduğundan koşul koşulları.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-793">Error - not a valid condition because @ is required for conditions.</span></span>|  
  
<span data-ttu-id="f0cdf-794">Bir koşul başarıyla değerlendirilirse hello koşulu olarak işaretlenmiş `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-794">If a condition evaluates successfully, hello condition is marked as `Succeeded`.</span></span> <span data-ttu-id="f0cdf-795">Ya da hello içinde eylemler `actions` veya `else` nesneleri değerlendirmek çok`Succeeded` yürütülen ve başarılı oldu, `Failed` yürütülen ve başarısız olduğunda veya `Skipped` zaman o şubedeki yürütülmez.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-795">Actions within either hello `actions` or `else` objects evaluate too`Succeeded` when executed and succeeded, `Failed` when executed and failed, or `Skipped` when that branch is not executed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0cdf-796">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f0cdf-796">Next steps</span></span>

[<span data-ttu-id="f0cdf-797">İş akışı hizmeti REST API'si</span><span class="sxs-lookup"><span data-stu-id="f0cdf-797">Workflow Service REST API</span></span>](https://docs.microsoft.com/rest/api/logic/workflows)
