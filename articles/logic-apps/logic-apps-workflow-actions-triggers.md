---
title: "İş akışı eylemleri ve Tetikleyicileri - Azure Logic Apps | Microsoft Docs"
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
ms.openlocfilehash: bd3f1d225b974ebde889738bb435825658d1e1e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="workflow-actions-and-triggers-for-azure-logic-apps"></a><span data-ttu-id="fcfe4-102">İş akışı eylemleri ve Azure Logic Apps için Tetikleyiciler</span><span class="sxs-lookup"><span data-stu-id="fcfe4-102">Workflow actions and triggers for Azure Logic Apps</span></span>

<span data-ttu-id="fcfe4-103">Logic apps tetikleyiciler ve Eylemler oluşur.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-103">Logic apps consist of triggers and actions.</span></span> <span data-ttu-id="fcfe4-104">Tetikleyiciler altı tür vardır.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-104">There are six types of triggers.</span></span> <span data-ttu-id="fcfe4-105">Her tür farklı arabirimi ve farklı bir davranışı vardır.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-105">Each type has different interface and different behavior.</span></span> <span data-ttu-id="fcfe4-106">Ayrıntılarını bakarak ilgili diğer ayrıntıları öğrenebilirsiniz [iş akışı tanımlama dili](logic-apps-workflow-definition-language.md).</span><span class="sxs-lookup"><span data-stu-id="fcfe4-106">You can also learn about other details by looking at the details of the [Workflow Definition Language](logic-apps-workflow-definition-language.md).</span></span>  
  
<span data-ttu-id="fcfe4-107">İçin okumaya tetikleyiciler ve Eylemler ve iş süreçlerini ve iş akışları geliştirmek için mantığı uygulamalar oluşturmak için bunları nasıl kullanacağınızı hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-107">Read on to learn more about triggers and actions and how you might use them to build logic apps to improve your business processes and workflows.</span></span>  
  
### <a name="triggers"></a><span data-ttu-id="fcfe4-108">Tetikleyiciler</span><span class="sxs-lookup"><span data-stu-id="fcfe4-108">Triggers</span></span>  

<span data-ttu-id="fcfe4-109">Tetikleyicinin mantığını uygulama akışınızın bir farklı çalıştır başlatabilirsiniz çağrıları belirtir.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-109">A trigger specifies the calls that can initiate a run of your logic app workflow.</span></span> <span data-ttu-id="fcfe4-110">İş akışınızı yürütülmesi başlatmak için iki farklı şekilde şunlardır:</span><span class="sxs-lookup"><span data-stu-id="fcfe4-110">Here are the two different ways to initiate a run of your workflow:</span></span>  
  
-   <span data-ttu-id="fcfe4-111">Yoklama tetikleyici</span><span class="sxs-lookup"><span data-stu-id="fcfe4-111">A polling trigger</span></span>  

-   <span data-ttu-id="fcfe4-112">Çağırarak itme tetikleyici - [iş akışı hizmeti REST API'si](https://docs.microsoft.com/rest/api/logic/workflows)</span><span class="sxs-lookup"><span data-stu-id="fcfe4-112">A push trigger - by calling the [Workflow Service REST API](https://docs.microsoft.com/rest/api/logic/workflows)</span></span>  
  
<span data-ttu-id="fcfe4-113">Tüm Tetikleyicileri bu üst düzey öğeleri içerir:</span><span class="sxs-lookup"><span data-stu-id="fcfe4-113">All triggers contain these top-level elements:</span></span>  
  
```json
"<name-of-the-trigger>" : {
    "type": "<type-of-trigger>",
    "inputs": { <settings-for-the-call> },
    "recurrence": {  
        "frequency": "Second|Minute|Hour|Week|Month|Year",
        "interval": "<recurrence interval in units of frequency>"
    },
    "conditions": [ <array-of-required-conditions > ],
    "splitOn" : "<property to create runs for>",
    "operationOptions": "<operation options on the trigger>"
}
```

### <a name="trigger-types-and-their-inputs"></a><span data-ttu-id="fcfe4-114">Tetikleyici türlerini ve bunların girişleri</span><span class="sxs-lookup"><span data-stu-id="fcfe4-114">Trigger types and their inputs</span></span>  

<span data-ttu-id="fcfe4-115">Bu tür tetikleyici sunucusu kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fcfe4-115">You can use these types of triggers:</span></span>
  
-   <span data-ttu-id="fcfe4-116">**İstek** \- mantıksal uygulamayı çağırmak size bir uç nokta yapar</span><span class="sxs-lookup"><span data-stu-id="fcfe4-116">**Request** \- Makes the logic app an endpoint for you to call</span></span>  
  
-   <span data-ttu-id="fcfe4-117">**Yineleme** \- ateşlenir dayalı tanımlanmış bir zamanlamaya göre</span><span class="sxs-lookup"><span data-stu-id="fcfe4-117">**Recurrence** \- Fires based on a defined schedule</span></span>  
  
-   <span data-ttu-id="fcfe4-118">**HTTP** \- bir HTTP web uç noktası yoklar.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-118">**HTTP** \- Polls an HTTP web endpoint.</span></span> <span data-ttu-id="fcfe4-119">HTTP uç noktası için belirli bir tetikleme sözleşme uymalıdır \- bir 202 kullanarak ya da\-zaman uyumsuz desen veya bir dizi döndürerek</span><span class="sxs-lookup"><span data-stu-id="fcfe4-119">The HTTP endpoint must conform to a specific triggering contract \- either by using a 202\-async pattern, or by returning an array</span></span>  
  
-   <span data-ttu-id="fcfe4-120">**ApiConnection** \- HTTP gibi yoklamalar tetikleyin, ancak bunu yararlanan [Microsoft tarafından yönetilen API'ler](https://docs.microsoft.com/azure/connectors/apis-list)</span><span class="sxs-lookup"><span data-stu-id="fcfe4-120">**ApiConnection** \- Polls like the HTTP trigger, however, it takes advantage of the [Microsoft-managed APIs](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>  
  
-   <span data-ttu-id="fcfe4-121">**HTTPWebhook** \- uç noktası, el ile tetikleyici, Bununla birlikte, benzer bir açılır de çağırır kaydedin ve kaydı için belirtilen URL</span><span class="sxs-lookup"><span data-stu-id="fcfe4-121">**HTTPWebhook** \- Opens an endpoint, similar to the Manual trigger, however, it also calls out to a specified URL to register and unregister</span></span>  
  
-   <span data-ttu-id="fcfe4-122">**ApiConnectionWebhook** \- Operates Microsoft tarafından yönetilen API'ları yararlanarak HTTPWebhook tetikleyici gibi</span><span class="sxs-lookup"><span data-stu-id="fcfe4-122">**ApiConnectionWebhook** \- Operates like the HTTPWebhook trigger by taking advantage of the Microsoft-managed APIs</span></span>       
    <span data-ttu-id="fcfe4-123">Farklı bir kümesini her tetikleyici türünde **girişleri** davranışını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-123">Each trigger type has a different set of **inputs** that defines its behavior.</span></span>  
  
## <a name="request-trigger"></a><span data-ttu-id="fcfe4-124">Tetikleyici isteği</span><span class="sxs-lookup"><span data-stu-id="fcfe4-124">Request trigger</span></span>  

<span data-ttu-id="fcfe4-125">Bu tetikleyici bir uç nokta mantıksal uygulamanızı çağırmak için bir HTTP isteği çağıran işlevi görür.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-125">This trigger serves as an endpoint that you call via an HTTP Request to invoke your logic app.</span></span> <span data-ttu-id="fcfe4-126">Bir istek tetikleyici aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="fcfe4-126">A request trigger looks like this example:</span></span>  
  
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

<span data-ttu-id="fcfe4-127">Ayrıca adlı isteğe bağlı bir özellik olan **şema**:</span><span class="sxs-lookup"><span data-stu-id="fcfe4-127">There is also an optional property called **schema**:</span></span>  
  
|<span data-ttu-id="fcfe4-128">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="fcfe4-128">Element name</span></span>|<span data-ttu-id="fcfe4-129">Gerekli</span><span class="sxs-lookup"><span data-stu-id="fcfe4-129">Required</span></span>|<span data-ttu-id="fcfe4-130">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fcfe4-130">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="fcfe4-131">Şema</span><span class="sxs-lookup"><span data-stu-id="fcfe4-131">schema</span></span>|<span data-ttu-id="fcfe4-132">Hayır</span><span class="sxs-lookup"><span data-stu-id="fcfe4-132">No</span></span>|<span data-ttu-id="fcfe4-133">JSON şeması gelen isteği doğrular.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-133">A JSON schema that validates the incoming request.</span></span> <span data-ttu-id="fcfe4-134">Sonraki iş akışı adımları başvurmak için hangi özelliklerin bilmeniz yardımcı olmak için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-134">Useful for helping subsequent workflow steps know which properties to reference.</span></span>|

<span data-ttu-id="fcfe4-135">Bu uç noktaya çağrılacak çağırması gerekir *listCallbackUrl* API.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-135">To invoke this endpoint, you need to call the *listCallbackUrl* API.</span></span> <span data-ttu-id="fcfe4-136">Bkz: [iş akışı hizmeti REST API'si](https://docs.microsoft.com/rest/api/logic/workflows).</span><span class="sxs-lookup"><span data-stu-id="fcfe4-136">See [Workflow Service REST API](https://docs.microsoft.com/rest/api/logic/workflows).</span></span>  
  
## <a name="recurrence-trigger"></a><span data-ttu-id="fcfe4-137">Yineleme tetikleyici</span><span class="sxs-lookup"><span data-stu-id="fcfe4-137">Recurrence trigger</span></span>  

<span data-ttu-id="fcfe4-138">Bir yineleme tetikleyici tanımlanmış bir zamanlamaya göre çalıştırır biridir.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-138">A Recurrence trigger is one that runs based on a defined schedule.</span></span> <span data-ttu-id="fcfe4-139">Bu tür bir tetikleyici, aşağıdaki örnekte olduğu gibi görünebilir:</span><span class="sxs-lookup"><span data-stu-id="fcfe4-139">Such a trigger might look like this example:</span></span>  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

<span data-ttu-id="fcfe4-140">Gördüğünüz gibi bir iş akışını çalıştırmak için basit bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-140">As you can see, it is a simple way to run a workflow.</span></span>  
  
|<span data-ttu-id="fcfe4-141">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="fcfe4-141">Element name</span></span>|<span data-ttu-id="fcfe4-142">Gerekli</span><span class="sxs-lookup"><span data-stu-id="fcfe4-142">Required</span></span>|<span data-ttu-id="fcfe4-143">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fcfe4-143">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="fcfe4-144">Sıklık</span><span class="sxs-lookup"><span data-stu-id="fcfe4-144">frequency</span></span>|<span data-ttu-id="fcfe4-145">Evet</span><span class="sxs-lookup"><span data-stu-id="fcfe4-145">Yes</span></span>|<span data-ttu-id="fcfe4-146">Ne sıklıkta tetikleyici yürütür.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-146">How often the trigger executes.</span></span> <span data-ttu-id="fcfe4-147">Bu değerlerden yalnızca birini kullanın: saniye, dakika, saat, gün, hafta, ay veya yıl</span><span class="sxs-lookup"><span data-stu-id="fcfe4-147">Use only one of these possible values: second, minute, hour, day, week, month, or year</span></span>|  
|<span data-ttu-id="fcfe4-148">aralığı</span><span class="sxs-lookup"><span data-stu-id="fcfe4-148">interval</span></span>|<span data-ttu-id="fcfe4-149">Evet</span><span class="sxs-lookup"><span data-stu-id="fcfe4-149">Yes</span></span>|<span data-ttu-id="fcfe4-150">Verilen sıklığı aralığını yineleme için</span><span class="sxs-lookup"><span data-stu-id="fcfe4-150">Interval of the given frequency for the recurrence</span></span>|  
|<span data-ttu-id="fcfe4-151">startTime</span><span class="sxs-lookup"><span data-stu-id="fcfe4-151">startTime</span></span>|<span data-ttu-id="fcfe4-152">Hayır</span><span class="sxs-lookup"><span data-stu-id="fcfe4-152">No</span></span>|<span data-ttu-id="fcfe4-153">Bir startTime UTC uzaklığı sağlanırsa, bu saat dilimi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-153">If a startTime is provided without a UTC offset, this timeZone is used.</span></span>|  
|<span data-ttu-id="fcfe4-154">saat dilimi</span><span class="sxs-lookup"><span data-stu-id="fcfe4-154">timeZone</span></span>|<span data-ttu-id="fcfe4-155">Yok</span><span class="sxs-lookup"><span data-stu-id="fcfe4-155">no</span></span>|<span data-ttu-id="fcfe4-156">Bir startTime UTC uzaklığı sağlanırsa, bu saat dilimi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-156">If a startTime is provided without a UTC offset, this timeZone is used.</span></span>|  
  
<span data-ttu-id="fcfe4-157">Ayrıca, belirli bir noktada gelecekte çalıştırmaya başlamak için bir tetikleyici zamanlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-157">You can also schedule a trigger to start executing at some point in the future.</span></span> <span data-ttu-id="fcfe4-158">Örneğin, haftalık bir rapor her Pazartesi başlatmak istiyorsanız aşağıdaki tetikleyici oluşturarak her Pazartesi başlatmak için mantıksal uygulama zamanlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fcfe4-158">For example, if you want to start a weekly report every Monday you can schedule the logic app to start every Monday by creating the following trigger:</span></span>  

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

## <a name="http-trigger"></a><span data-ttu-id="fcfe4-159">HTTP tetikleyicisi</span><span class="sxs-lookup"><span data-stu-id="fcfe4-159">HTTP trigger</span></span>  

<span data-ttu-id="fcfe4-160">HTTP Tetikleyicileri belirtilen uç nokta yoklamak ve iş akışı yürütülüp yürütülmeyeceğini belirlemek için yanıtı denetleyin.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-160">HTTP triggers poll a specified endpoint and check the response to determine whether the workflow should be executed.</span></span> <span data-ttu-id="fcfe4-161">Giriş nesnesi bir HTTP çağrısıyla oluşturmak için gerekli parametreleri kümesini alır:</span><span class="sxs-lookup"><span data-stu-id="fcfe4-161">The inputs object takes the set of parameters required to construct an HTTP call:</span></span>  
  
|<span data-ttu-id="fcfe4-162">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="fcfe4-162">Element name</span></span>|<span data-ttu-id="fcfe4-163">Gerekli</span><span class="sxs-lookup"><span data-stu-id="fcfe4-163">Required</span></span>|<span data-ttu-id="fcfe4-164">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fcfe4-164">Description</span></span>|<span data-ttu-id="fcfe4-165">Tür</span><span class="sxs-lookup"><span data-stu-id="fcfe4-165">Type</span></span>|  
|----------------|------------|---------------|--------|  
|<span data-ttu-id="fcfe4-166">Yöntemi</span><span class="sxs-lookup"><span data-stu-id="fcfe4-166">method</span></span>|<span data-ttu-id="fcfe4-167">Evet</span><span class="sxs-lookup"><span data-stu-id="fcfe4-167">yes</span></span>|<span data-ttu-id="fcfe4-168">Aşağıdaki HTTP yöntemlerden biri olabilir: GET, POST, PUT, DELETE, düzeltme eki veya HEAD</span><span class="sxs-lookup"><span data-stu-id="fcfe4-168">Can be one of the following HTTP methods: GET, POST, PUT, DELETE, PATCH, or HEAD</span></span>|<span data-ttu-id="fcfe4-169">Dize</span><span class="sxs-lookup"><span data-stu-id="fcfe4-169">String</span></span>|  
|<span data-ttu-id="fcfe4-170">URI</span><span class="sxs-lookup"><span data-stu-id="fcfe4-170">uri</span></span>|<span data-ttu-id="fcfe4-171">Evet</span><span class="sxs-lookup"><span data-stu-id="fcfe4-171">yes</span></span>|<span data-ttu-id="fcfe4-172">Çağrılan http veya https uç noktası.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-172">The http or https endpoint that is called.</span></span> <span data-ttu-id="fcfe4-173">2 kilobayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-173">Maximum of 2 kilobytes.</span></span>|<span data-ttu-id="fcfe4-174">Dize</span><span class="sxs-lookup"><span data-stu-id="fcfe4-174">String</span></span>|  
|<span data-ttu-id="fcfe4-175">Sorguları</span><span class="sxs-lookup"><span data-stu-id="fcfe4-175">queries</span></span>|<span data-ttu-id="fcfe4-176">Hayır</span><span class="sxs-lookup"><span data-stu-id="fcfe4-176">No</span></span>|<span data-ttu-id="fcfe4-177">URL'ye eklemek için sorgu parametreleri temsil eden bir nesne.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-177">An object representing the query parameters to add to the URL.</span></span> <span data-ttu-id="fcfe4-178">Örneğin, `"queries" : { "api-version": "2015-02-01" }` ekler `?api-version=2015-02-01` URL.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-178">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|<span data-ttu-id="fcfe4-179">Nesne</span><span class="sxs-lookup"><span data-stu-id="fcfe4-179">Object</span></span>|  
|<span data-ttu-id="fcfe4-180">Üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="fcfe4-180">headers</span></span>|<span data-ttu-id="fcfe4-181">Hayır</span><span class="sxs-lookup"><span data-stu-id="fcfe4-181">No</span></span>|<span data-ttu-id="fcfe4-182">Her isteği gönderilen üstbilgilerini temsil eden bir nesne.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-182">An object representing each of the headers that is sent to the request.</span></span> <span data-ttu-id="fcfe4-183">Örneğin, dilini ayarlamak ve bir istek yazmak için şunu yazın:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="fcfe4-183">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|<span data-ttu-id="fcfe4-184">Nesne</span><span class="sxs-lookup"><span data-stu-id="fcfe4-184">Object</span></span>|  
|<span data-ttu-id="fcfe4-185">Gövde</span><span class="sxs-lookup"><span data-stu-id="fcfe4-185">body</span></span>|<span data-ttu-id="fcfe4-186">Hayır</span><span class="sxs-lookup"><span data-stu-id="fcfe4-186">No</span></span>|<span data-ttu-id="fcfe4-187">Uç noktasına gönderilen yükünü temsil eden bir nesne.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-187">An object representing the payload that is sent to the endpoint.</span></span>|<span data-ttu-id="fcfe4-188">Nesne</span><span class="sxs-lookup"><span data-stu-id="fcfe4-188">Object</span></span>|  
|<span data-ttu-id="fcfe4-189">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="fcfe4-189">retryPolicy</span></span>|<span data-ttu-id="fcfe4-190">Hayır</span><span class="sxs-lookup"><span data-stu-id="fcfe4-190">No</span></span>|<span data-ttu-id="fcfe4-191">4xx veya 5xx hataları yeniden deneme davranışı özelleştirmenize olanak sağlayan bir nesne.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-191">An object that lets you customize the retry behavior for 4xx or 5xx errors.</span></span>|<span data-ttu-id="fcfe4-192">Nesne</span><span class="sxs-lookup"><span data-stu-id="fcfe4-192">Object</span></span>|  
|<span data-ttu-id="fcfe4-193">Kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="fcfe4-193">authentication</span></span>|<span data-ttu-id="fcfe4-194">Hayır</span><span class="sxs-lookup"><span data-stu-id="fcfe4-194">No</span></span>|<span data-ttu-id="fcfe4-195">İsteğin kimliği olduğunu yöntemi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-195">Represents the method that the request should be authenticated.</span></span> <span data-ttu-id="fcfe4-196">Bu nesne üzerinde daha fazla bilgi için bkz [Scheduler giden bağlantı kimlik doğrulaması](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span><span class="sxs-lookup"><span data-stu-id="fcfe4-196">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span></span> <span data-ttu-id="fcfe4-197">Zamanlayıcı daha desteklenen bir özellik yok: `authority` varsayılan olarak, bu değer `https://login.windows.net` belirtilmediğinde, ancak gibi farklı bir kitleye kullanabilirsiniz`https://login.windows\-ppe.net`</span><span class="sxs-lookup"><span data-stu-id="fcfe4-197">Beyond scheduler, there is one more supported property: `authority` By default, this value is `https://login.windows.net` when not specified, but you can use a different audience like `https://login.windows\-ppe.net`</span></span>|<span data-ttu-id="fcfe4-198">Nesne</span><span class="sxs-lookup"><span data-stu-id="fcfe4-198">Object</span></span>|  
  
<span data-ttu-id="fcfe4-199">HTTP tetikleyicisini iyi mantığı uygulamanızın üzerinde çalışmak için belirli bir desendeki uygun olması HTTP API gerektiriyor.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-199">The HTTP trigger requires the HTTP API to conform with a specific pattern to work well with your logic app.</span></span> <span data-ttu-id="fcfe4-200">Aşağıdaki alanları gerektirir:</span><span class="sxs-lookup"><span data-stu-id="fcfe4-200">It requires the following fields:</span></span>  
  
|<span data-ttu-id="fcfe4-201">Yanıt</span><span class="sxs-lookup"><span data-stu-id="fcfe4-201">Response</span></span>|<span data-ttu-id="fcfe4-202">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fcfe4-202">Description</span></span>|  
|------------|---------------|  
|<span data-ttu-id="fcfe4-203">Durum kodu</span><span class="sxs-lookup"><span data-stu-id="fcfe4-203">Status code</span></span>|<span data-ttu-id="fcfe4-204">Durum kodu 200 \(Tamam\) Çalıştır neden olacak.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-204">Status code 200 \(OK\) to cause a run.</span></span> <span data-ttu-id="fcfe4-205">Diğer bir durum kodu bir Farklı Çalıştır neden olmaz.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-205">Any other status code doesn't cause a run.</span></span>|  
|<span data-ttu-id="fcfe4-206">Yeniden deneme\-üstbilgi sonra</span><span class="sxs-lookup"><span data-stu-id="fcfe4-206">Retry\-after header</span></span>|<span data-ttu-id="fcfe4-207">Mantıksal uygulama uç nokta yeniden yoklar kadar saniye sayısı.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-207">Number of seconds until the logic app polls the endpoint again.</span></span>|  
|<span data-ttu-id="fcfe4-208">Konum üstbilgisi</span><span class="sxs-lookup"><span data-stu-id="fcfe4-208">Location header</span></span>|<span data-ttu-id="fcfe4-209">Sonraki yoklama aralığını üzerinde çağrısı için URL.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-209">The URL to call on the next polling interval.</span></span> <span data-ttu-id="fcfe4-210">Belirtilmezse, özgün URL'si kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-210">If not specified, the original URL is used.</span></span>|  
  
<span data-ttu-id="fcfe4-211">İstekleri farklı türleri için farklı davranışlar bazı örnekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="fcfe4-211">Here are some examples of different behaviors for different types of requests:</span></span>  
  
|<span data-ttu-id="fcfe4-212">Yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="fcfe4-212">Response code</span></span>|<span data-ttu-id="fcfe4-213">Yeniden deneme\-sonra</span><span class="sxs-lookup"><span data-stu-id="fcfe4-213">Retry\-After</span></span>|<span data-ttu-id="fcfe4-214">Davranışı</span><span class="sxs-lookup"><span data-stu-id="fcfe4-214">Behavior</span></span>|  
|-----------------|----------------|------------|  
|<span data-ttu-id="fcfe4-215">200</span><span class="sxs-lookup"><span data-stu-id="fcfe4-215">200</span></span>|<span data-ttu-id="fcfe4-216">\(yok\)</span><span class="sxs-lookup"><span data-stu-id="fcfe4-216">\(none\)</span></span>|<span data-ttu-id="fcfe4-217">Değil geçerli tetikleyici yeniden deneme\-sonra gereklidir veya başka altyapısı sonraki istek için hiçbir zaman yoklar.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-217">Not a valid trigger, Retry\-After is required, or else the engine never polls for the next request.</span></span>|  
|<span data-ttu-id="fcfe4-218">202</span><span class="sxs-lookup"><span data-stu-id="fcfe4-218">202</span></span>|<span data-ttu-id="fcfe4-219">60</span><span class="sxs-lookup"><span data-stu-id="fcfe4-219">60</span></span>|<span data-ttu-id="fcfe4-220">İş akışı tetiklemez.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-220">Do not trigger the workflow.</span></span> <span data-ttu-id="fcfe4-221">Sonraki girişiminde bir dakika içinde gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-221">The next attempt happens in one minute.</span></span>|  
|<span data-ttu-id="fcfe4-222">200</span><span class="sxs-lookup"><span data-stu-id="fcfe4-222">200</span></span>|<span data-ttu-id="fcfe4-223">10</span><span class="sxs-lookup"><span data-stu-id="fcfe4-223">10</span></span>|<span data-ttu-id="fcfe4-224">İş akışını çalıştırmak ve daha fazla içerik için 10 saniye içinde yeniden kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-224">Run the workflow, and check again for more content in 10 seconds.</span></span>|  
|<span data-ttu-id="fcfe4-225">400</span><span class="sxs-lookup"><span data-stu-id="fcfe4-225">400</span></span>|<span data-ttu-id="fcfe4-226">\(yok\)</span><span class="sxs-lookup"><span data-stu-id="fcfe4-226">\(none\)</span></span>|<span data-ttu-id="fcfe4-227">Hatalı istek, iş akışı çalıştırmayın.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-227">Bad request, do not run the workflow.</span></span> <span data-ttu-id="fcfe4-228">Varsa hiçbir **yeniden deneme ilkesi** tanımlanan varsayılan ilke kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-228">If there is no **Retry Policy** defined, then the default policy is used.</span></span> <span data-ttu-id="fcfe4-229">Yeniden deneme sayısı üst sınırına ulaşıldı sonra tetikleyici artık geçerli değil.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-229">After the number of retries has been reached, the trigger is no longer valid.</span></span>|  
|<span data-ttu-id="fcfe4-230">500</span><span class="sxs-lookup"><span data-stu-id="fcfe4-230">500</span></span>|<span data-ttu-id="fcfe4-231">\(yok\)</span><span class="sxs-lookup"><span data-stu-id="fcfe4-231">\(none\)</span></span>|<span data-ttu-id="fcfe4-232">Sunucu hatası, iş akışı çalıştırmayın.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-232">Server error, do not run the workflow.</span></span>  <span data-ttu-id="fcfe4-233">Varsa hiçbir **yeniden deneme ilkesi** tanımlanan varsayılan ilke kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-233">If there is no **Retry Policy** defined, then the default policy is used.</span></span> <span data-ttu-id="fcfe4-234">Yeniden deneme sayısı üst sınırına ulaşıldı sonra tetikleyici artık geçerli değil.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-234">After the number of retries has been reached, the trigger is no longer valid.</span></span>|  
  
<span data-ttu-id="fcfe4-235">Bir HTTP tetikleyicisi çıkışları aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="fcfe4-235">The outputs of an HTTP trigger look like this example:</span></span>  
  
|<span data-ttu-id="fcfe4-236">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="fcfe4-236">Element name</span></span>|<span data-ttu-id="fcfe4-237">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fcfe4-237">Description</span></span>|<span data-ttu-id="fcfe4-238">Tür</span><span class="sxs-lookup"><span data-stu-id="fcfe4-238">Type</span></span>|  
|----------------|---------------|--------|  
|<span data-ttu-id="fcfe4-239">Üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="fcfe4-239">headers</span></span>|<span data-ttu-id="fcfe4-240">Http yanıtı üstbilgileri.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-240">The headers of the http response.</span></span>|<span data-ttu-id="fcfe4-241">Nesne</span><span class="sxs-lookup"><span data-stu-id="fcfe4-241">Object</span></span>|  
|<span data-ttu-id="fcfe4-242">Gövde</span><span class="sxs-lookup"><span data-stu-id="fcfe4-242">body</span></span>|<span data-ttu-id="fcfe4-243">Http yanıt gövdesi.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-243">The body of the http response.</span></span>|<span data-ttu-id="fcfe4-244">Nesne</span><span class="sxs-lookup"><span data-stu-id="fcfe4-244">Object</span></span>|  
  
## <a name="api-connection-trigger"></a><span data-ttu-id="fcfe4-245">API bağlantı tetikleyici</span><span class="sxs-lookup"><span data-stu-id="fcfe4-245">API Connection trigger</span></span>  

<span data-ttu-id="fcfe4-246">API bağlantı tetikleyici temel işlevselliğini HTTP tetikleyicinin benzer.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-246">The API connection trigger is similar to the HTTP trigger in its basic functionality.</span></span> <span data-ttu-id="fcfe4-247">Bununla birlikte, eylem tanımlamak için farklı parametreleridir.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-247">However, the parameters for identifying the action are different.</span></span> <span data-ttu-id="fcfe4-248">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="fcfe4-248">Here is an example:</span></span>  
  
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

|<span data-ttu-id="fcfe4-249">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="fcfe4-249">Element name</span></span>|<span data-ttu-id="fcfe4-250">Gerekli</span><span class="sxs-lookup"><span data-stu-id="fcfe4-250">Required</span></span>|<span data-ttu-id="fcfe4-251">Tür</span><span class="sxs-lookup"><span data-stu-id="fcfe4-251">Type</span></span>|<span data-ttu-id="fcfe4-252">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fcfe4-252">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="fcfe4-253">ana bilgisayar</span><span class="sxs-lookup"><span data-stu-id="fcfe4-253">host</span></span>|<span data-ttu-id="fcfe4-254">Evet</span><span class="sxs-lookup"><span data-stu-id="fcfe4-254">Yes</span></span>||<span data-ttu-id="fcfe4-255">Ağ geçidi ve kimliği ApiApp barındırılan.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-255">The ApiApp hosted gateway and id.</span></span>|  
|<span data-ttu-id="fcfe4-256">Yöntemi</span><span class="sxs-lookup"><span data-stu-id="fcfe4-256">method</span></span>|<span data-ttu-id="fcfe4-257">Evet</span><span class="sxs-lookup"><span data-stu-id="fcfe4-257">Yes</span></span>|<span data-ttu-id="fcfe4-258">Dize</span><span class="sxs-lookup"><span data-stu-id="fcfe4-258">String</span></span>|<span data-ttu-id="fcfe4-259">Aşağıdaki HTTP yöntemlerden biri olabilir: **almak**, **POST**, **PUT**, **silmek**, **düzeltme eki**, veya  **HEAD**</span><span class="sxs-lookup"><span data-stu-id="fcfe4-259">Can be one of the following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="fcfe4-260">Sorguları</span><span class="sxs-lookup"><span data-stu-id="fcfe4-260">queries</span></span>|<span data-ttu-id="fcfe4-261">Hayır</span><span class="sxs-lookup"><span data-stu-id="fcfe4-261">No</span></span>|<span data-ttu-id="fcfe4-262">Nesne</span><span class="sxs-lookup"><span data-stu-id="fcfe4-262">Object</span></span>|<span data-ttu-id="fcfe4-263">URL'ye eklenecek sorgu parametreleri temsil eder.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-263">Represents the query parameters to be added to the URL.</span></span> <span data-ttu-id="fcfe4-264">Örneğin, `"queries" : { "api-version": "2015-02-01" }` ekler `?api-version=2015-02-01` URL.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-264">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|  
|<span data-ttu-id="fcfe4-265">Üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="fcfe4-265">headers</span></span>|<span data-ttu-id="fcfe4-266">Hayır</span><span class="sxs-lookup"><span data-stu-id="fcfe4-266">No</span></span>|<span data-ttu-id="fcfe4-267">Nesne</span><span class="sxs-lookup"><span data-stu-id="fcfe4-267">Object</span></span>|<span data-ttu-id="fcfe4-268">Her isteği gönderilen üstbilgilerinin temsil eder.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-268">Represents each of the headers that is sent to the request.</span></span> <span data-ttu-id="fcfe4-269">Örneğin, dilini ayarlamak ve bir istek yazmak için şunu yazın:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="fcfe4-269">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="fcfe4-270">Gövde</span><span class="sxs-lookup"><span data-stu-id="fcfe4-270">body</span></span>|<span data-ttu-id="fcfe4-271">Hayır</span><span class="sxs-lookup"><span data-stu-id="fcfe4-271">No</span></span>|<span data-ttu-id="fcfe4-272">Nesne</span><span class="sxs-lookup"><span data-stu-id="fcfe4-272">Object</span></span>|<span data-ttu-id="fcfe4-273">Uç noktasına gönderilen yükünü temsil eder.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-273">Represents the payload that is sent to the endpoint.</span></span>|  
|<span data-ttu-id="fcfe4-274">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="fcfe4-274">retryPolicy</span></span>|<span data-ttu-id="fcfe4-275">Hayır</span><span class="sxs-lookup"><span data-stu-id="fcfe4-275">No</span></span>|<span data-ttu-id="fcfe4-276">Nesne</span><span class="sxs-lookup"><span data-stu-id="fcfe4-276">Object</span></span>|<span data-ttu-id="fcfe4-277">4xx veya 5xx hataları yeniden deneme davranışını özelleştirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-277">Allows you to customize the retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="fcfe4-278">Kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="fcfe4-278">authentication</span></span>|<span data-ttu-id="fcfe4-279">Hayır</span><span class="sxs-lookup"><span data-stu-id="fcfe4-279">No</span></span>|<span data-ttu-id="fcfe4-280">Nesne</span><span class="sxs-lookup"><span data-stu-id="fcfe4-280">Object</span></span>|<span data-ttu-id="fcfe4-281">İsteğin kimliği olduğunu yöntemi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-281">Represents the method that the request should be authenticated.</span></span> <span data-ttu-id="fcfe4-282">Bu nesne üzerinde daha fazla bilgi için bkz [Scheduler giden bağlantı kimlik doğrulaması](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)</span><span class="sxs-lookup"><span data-stu-id="fcfe4-282">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)</span></span>|  
  
<span data-ttu-id="fcfe4-283">Konak özellikleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="fcfe4-283">The properties for host are:</span></span>  
  
|<span data-ttu-id="fcfe4-284">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="fcfe4-284">Element name</span></span>|<span data-ttu-id="fcfe4-285">Gerekli</span><span class="sxs-lookup"><span data-stu-id="fcfe4-285">Required</span></span>|<span data-ttu-id="fcfe4-286">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fcfe4-286">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="fcfe4-287">API runtimeUrl</span><span class="sxs-lookup"><span data-stu-id="fcfe4-287">api runtimeUrl</span></span>|<span data-ttu-id="fcfe4-288">Evet</span><span class="sxs-lookup"><span data-stu-id="fcfe4-288">Yes</span></span>|<span data-ttu-id="fcfe4-289">Yönetilen API uç noktası.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-289">The endpoint of the managed API.</span></span>|  
|<span data-ttu-id="fcfe4-290">Bağlantı adı</span><span class="sxs-lookup"><span data-stu-id="fcfe4-290">connection name</span></span>||<span data-ttu-id="fcfe4-291">Adlı bir parametre için bir başvurusu olmalıdır `$connection` ve iş akışının kullandığı yönetilen API bağlantı adıdır.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-291">Must be a reference to a parameter called `$connection` and is the name of the managed API connection that the workflow uses.</span></span>|
  
<span data-ttu-id="fcfe4-292">Bir API bağlantı tetikleyicisi çıkışları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="fcfe4-292">The outputs of an API connection trigger are:</span></span>
  
|<span data-ttu-id="fcfe4-293">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="fcfe4-293">Element name</span></span>|<span data-ttu-id="fcfe4-294">Tür</span><span class="sxs-lookup"><span data-stu-id="fcfe4-294">Type</span></span>|<span data-ttu-id="fcfe4-295">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fcfe4-295">Description</span></span>|  
|----------------|--------|---------------|  
|<span data-ttu-id="fcfe4-296">Üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="fcfe4-296">headers</span></span>|<span data-ttu-id="fcfe4-297">Nesne</span><span class="sxs-lookup"><span data-stu-id="fcfe4-297">Object</span></span>|<span data-ttu-id="fcfe4-298">Http yanıtı üstbilgileri.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-298">The headers of the http response.</span></span>|  
|<span data-ttu-id="fcfe4-299">Gövde</span><span class="sxs-lookup"><span data-stu-id="fcfe4-299">body</span></span>|<span data-ttu-id="fcfe4-300">Nesne</span><span class="sxs-lookup"><span data-stu-id="fcfe4-300">Object</span></span>|<span data-ttu-id="fcfe4-301">Http yanıt gövdesi.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-301">The body of the http response.</span></span>|  
  
## <a name="httpwebhook-trigger"></a><span data-ttu-id="fcfe4-302">HTTPWebhook tetikleyici</span><span class="sxs-lookup"><span data-stu-id="fcfe4-302">HTTPWebhook trigger</span></span>  

<span data-ttu-id="fcfe4-303">Bir uç nokta, el ile tetikleyiciye benzer HTTPWebhook tetikleyici açar ancak HTTPWebhook tetikleyici de kaydetme ve kaydını kaldırmak için belirtilen URL çağırır.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-303">The HTTPWebhook trigger opens an endpoint, similar to the manual trigger, but the HTTPWebhook trigger also calls out to a specified URL to register and unregister.</span></span> <span data-ttu-id="fcfe4-304">Bir HTTPWebhook tetikleyicisi aşağıdaki gibi görünmelidir örneği şöyledir:</span><span class="sxs-lookup"><span data-stu-id="fcfe4-304">Here's an example of what an HTTPWebhook trigger might look like:</span></span>  

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

<span data-ttu-id="fcfe4-305">Bu bölümler çoğunu isteğe bağlıdır ve Web kancası davranışını hangi bölümlerinin sağlanan atlanmış veya bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-305">Many of these sections are optional, and the behavior of the Webhook depends on which sections are provided or omitted.</span></span>  
<span data-ttu-id="fcfe4-306">Bir Web kancası özelliklerini aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="fcfe4-306">The properties of a Webhook are as follows:</span></span>  
  
|<span data-ttu-id="fcfe4-307">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="fcfe4-307">Element name</span></span>|<span data-ttu-id="fcfe4-308">Gerekli</span><span class="sxs-lookup"><span data-stu-id="fcfe4-308">Required</span></span>|<span data-ttu-id="fcfe4-309">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fcfe4-309">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="fcfe4-310">abone olma</span><span class="sxs-lookup"><span data-stu-id="fcfe4-310">subscribe</span></span>|<span data-ttu-id="fcfe4-311">Hayır</span><span class="sxs-lookup"><span data-stu-id="fcfe4-311">No</span></span>|<span data-ttu-id="fcfe4-312">Tetikleyici oluşturulduğunda ve ilk kaydı gerçekleştiren çağrılan giden istek.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-312">The outgoing request that is called when the trigger is created and performs the initial registration.</span></span>|  
|<span data-ttu-id="fcfe4-313">Aboneliği Kaldır</span><span class="sxs-lookup"><span data-stu-id="fcfe4-313">unsubscribe</span></span>|<span data-ttu-id="fcfe4-314">Hayır</span><span class="sxs-lookup"><span data-stu-id="fcfe4-314">No</span></span>|<span data-ttu-id="fcfe4-315">Tetikleyici silindiğinde giden istek.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-315">The outgoing request when the trigger is deleted.</span></span>|  
  
-   <span data-ttu-id="fcfe4-316">**Abone** olaylarını dinleme başlatmak için yaptığı giden çağrıdır.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-316">**Subscribe** is the outgoing call that's made to start listening to events.</span></span> <span data-ttu-id="fcfe4-317">Bu çağrı normal HTTP eylemleri gerçekleştirebilirsiniz parametreleri aynı kümesiyle başlatır.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-317">This call starts with the same set of parameters that the normal HTTP actions do.</span></span> <span data-ttu-id="fcfe4-318">Bu giden çağrı herhangi bir iş akışı herhangi bir şekilde, örneğin, kimlik bilgileri alınır veya tetikleyici giriş parametreleri değiştirmek her değiştiğinde yapılır.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-318">This outgoing call is made any time the workflow changes in any way, for example, whenever the credentials are rolled, or the trigger's input parameters change.</span></span>
  
    <span data-ttu-id="fcfe4-319">Bu çağrı desteklemek için bir yeni işlevi yoktur: `@listCallbackUrl()`.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-319">To support this call, there is a new function: `@listCallbackUrl()`.</span></span> <span data-ttu-id="fcfe4-320">Bu işlev, bu iş akışındaki belirli Bu tetikleyici için benzersiz bir URL döndürür.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-320">This function returns a unique URL for this specific trigger in this workflow.</span></span> <span data-ttu-id="fcfe4-321">Bu hizmet REST kullanan uç noktaları için benzersiz tanımlayıcıyı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-321">It represents the unique identifier for the endpoints that use the Service REST.</span></span>  
  
-   <span data-ttu-id="fcfe4-322">**Aboneliği** bir işlem Bu tetikleyici geçersiz dahil olmak üzere işler olduğunda çağrılır:</span><span class="sxs-lookup"><span data-stu-id="fcfe4-322">**Unsubscribe** is called when an operation renders this trigger invalid, including:</span></span>  
  
    -   <span data-ttu-id="fcfe4-323">Silme veya tetikleyici devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="fcfe4-323">Deleting or disabling the trigger</span></span>  
  
    -   <span data-ttu-id="fcfe4-324">Silme veya iş akışını devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="fcfe4-324">Deleting or disabling the workflow</span></span>  
  
    -   <span data-ttu-id="fcfe4-325">Silme veya abonelik devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="fcfe4-325">Deleting or disabling the subscription</span></span>  
  
    <span data-ttu-id="fcfe4-326">Mantıksal uygulama otomatik olarak abonelikten eylemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-326">The logic app automatically calls the unsubscribe action.</span></span> <span data-ttu-id="fcfe4-327">Bu işlev parametreleri HTTP tetikleyicisini ile aynıdır.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-327">The parameters to this function are the same as the HTTP trigger.</span></span>  
  
    <span data-ttu-id="fcfe4-328">Gelen istek içeriği HTTPWebhook tetikleyici çıkışları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="fcfe4-328">The outputs of the HTTPWebhook trigger are the contents of the incoming request:</span></span>  
  
|<span data-ttu-id="fcfe4-329">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="fcfe4-329">Element name</span></span>|<span data-ttu-id="fcfe4-330">Tür</span><span class="sxs-lookup"><span data-stu-id="fcfe4-330">Type</span></span>|<span data-ttu-id="fcfe4-331">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fcfe4-331">Description</span></span>|  
|-----------------|--------|---------------|  
|<span data-ttu-id="fcfe4-332">Üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="fcfe4-332">headers</span></span>|<span data-ttu-id="fcfe4-333">Nesne</span><span class="sxs-lookup"><span data-stu-id="fcfe4-333">Object</span></span>|<span data-ttu-id="fcfe4-334">Http isteği üstbilgileri.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-334">The headers of the http request.</span></span>|  
|<span data-ttu-id="fcfe4-335">Gövde</span><span class="sxs-lookup"><span data-stu-id="fcfe4-335">body</span></span>|<span data-ttu-id="fcfe4-336">Nesne</span><span class="sxs-lookup"><span data-stu-id="fcfe4-336">Object</span></span>|<span data-ttu-id="fcfe4-337">Http istek gövdesi.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-337">The body of the http request.</span></span>|  

<span data-ttu-id="fcfe4-338">Bir Web kancası eylemi sınırları, aynı şekilde belirtilebilir [HTTP zaman uyumsuz sınırları](#asynchronous-limits).</span><span class="sxs-lookup"><span data-stu-id="fcfe4-338">Limits on a webhook action can be specified in the same manner as [HTTP Asynchronous Limits](#asynchronous-limits).</span></span>
  

## <a name="conditions"></a><span data-ttu-id="fcfe4-339">Koşullar</span><span class="sxs-lookup"><span data-stu-id="fcfe4-339">Conditions</span></span>  

<span data-ttu-id="fcfe4-340">Herhangi bir tetikleyici için iş akışı veya çalıştırılması gerekip gerekmediğini belirlemek için bir veya daha fazla koşulları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-340">For any trigger, you can use one or more conditions to determine whether the workflow should run or not.</span></span> <span data-ttu-id="fcfe4-341">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="fcfe4-341">For example:</span></span>  

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

<span data-ttu-id="fcfe4-342">Bu durumda, rapor yalnızca Tetikleyicileri iş akışı çalışırken `sendReports` parametrenin ayarlanmış true.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-342">In this case, the report only triggers while the workflow's `sendReports` parameter is set to true.</span></span> <span data-ttu-id="fcfe4-343">Son olarak, koşullar tetikleyici durum kodunu başvurabilir.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-343">Finally, conditions may reference the status code of the trigger.</span></span> <span data-ttu-id="fcfe4-344">Örneğin, yalnızca Web sitenizin bir durum kodu 500, aşağıdaki gibi geri döndüğünde devre dışı bir iş akışı kazandırın:</span><span class="sxs-lookup"><span data-stu-id="fcfe4-344">For example, you could kick off a workflow only when your website returns a status code 500, as follows:</span></span>
  
```  
"conditions": [  
        {  
          "expression": "@equals(triggers().code, 'InternalServerError')"  
        }  
      ]  
```  
  
> [!NOTE]  
> <span data-ttu-id="fcfe4-345">Herhangi bir ifade tetikleyici durum kodunu başvurduğunda \(herhangi bir şekilde\), varsayılan davranışı \(200 yalnızca Tetikle \(Tamam\) \) değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-345">When any expression references the status code of the trigger \(in any way\), the default behavior \(trigger only on 200 \(OK\)\) is replaced.</span></span> <span data-ttu-id="fcfe4-346">Durum kodu 200 hem 201 durum kodunu tetiklemek istiyorsanız, örneğin, dahil etmek zorunda: `@or(equals(triggers().code, 200),equals(triggers().code,201))` koşulunuz olarak.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-346">For example, if you want to trigger on both status code 200 and status code 201, you have to include: `@or(equals(triggers().code, 200),equals(triggers().code,201))` as your condition.</span></span>  
  
## <a name="start-multiple-runs-for-a-request"></a><span data-ttu-id="fcfe4-347">Bir istek için birden çok çalışmalarını Başlat</span><span class="sxs-lookup"><span data-stu-id="fcfe4-347">Start multiple runs for a request</span></span>

<span data-ttu-id="fcfe4-348">Tek bir istek için birden çok çalıştırır kapalı kazandırın için `splitOn` yoklama aralıkları arasında birden çok yeni öğeleri olan bir uç nokta yoklamak istediğinizde, örneğin, yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-348">To kick off multiple runs for a single request, `splitOn` is useful, for example, when you want to poll an endpoint that can have multiple new items between polling intervals.</span></span>
  
<span data-ttu-id="fcfe4-349">İle `splitOn`, her biri tetikleyicinin çalıştırmasını başlatmak için kullanmak istediğiniz öğeleri dizisi içeren yanıt yükünün özelliğini belirtin.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-349">With `splitOn`, you specify the property inside the response payload that contains the array of items, each of which you want to use to start a run of the trigger.</span></span> <span data-ttu-id="fcfe4-350">Örneğin, aşağıdaki yanıtı döndüren bir API olduğunu düşünün:</span><span class="sxs-lookup"><span data-stu-id="fcfe4-350">For example, imagine you have an API that returns the following response:</span></span>  
  
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
  
<span data-ttu-id="fcfe4-351">Bu örnek gibi tetikleyici gerçekleştirebilmesi için mantıksal uygulamanızı yalnızca satır içerik gerekir:</span><span class="sxs-lookup"><span data-stu-id="fcfe4-351">Your logic app only needs the Rows content, so you can construct your trigger like this example:</span></span>  
  
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
  
<span data-ttu-id="fcfe4-352">Daha sonra iş akışı tanımında `@triggerBody().name` döndürür `mycoolrow` ilk çalıştırma için ve `another row` ikinci çalıştırma için.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-352">Then, in the workflow definition, `@triggerBody().name` returns `mycoolrow` for the first run, and `another row` for the second run.</span></span> <span data-ttu-id="fcfe4-353">Bu örnek tetikleyici çıkışları görünümlü:</span><span class="sxs-lookup"><span data-stu-id="fcfe4-353">The trigger outputs look like this example:</span></span>  
  
```json
{
    "body" : {
        "id" : 938109381,
        "name" : "another row"
    }
}
```

<span data-ttu-id="fcfe4-354">Kullanırsanız, bunu `SplitOn`, bu durumda, dizi dışında olan özellikler alınamıyor `Status` alan.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-354">So if you use `SplitOn`, you can't get the properties that are outside the array, in this case, the `Status` field.</span></span>  
  
> [!NOTE]  
> <span data-ttu-id="fcfe4-355">Bu örnekte, kullandığımız `?` bir hata durumunda kaçınabilirsiniz işleci `Rows` özelliği mevcut değil.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-355">In this example, we use the `?` operator to be able to avoid a failure if the `Rows` property is not present.</span></span> 
  
## <a name="single-run-instance"></a><span data-ttu-id="fcfe4-356">Tek çalışma örneği</span><span class="sxs-lookup"><span data-stu-id="fcfe4-356">Single run instance</span></span>

<span data-ttu-id="fcfe4-357">Tüm etkin metinler tamamladıysanız, yalnızca tetiklenecek yinelenme özelliğine sahip Tetikleyicileri yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-357">You can configure triggers that have a recurrence property to only fire if all active runs have completed.</span></span> <span data-ttu-id="fcfe4-358">Bir çalıştırma sürüyor olsa zamanlanmış bir yinelenme meydana gelirse, tetikleyici atlar ve yeniden denetlemek için bir sonraki zamanlanmış yinelenme aralığı kadar bekler.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-358">If a scheduled recurrence occurs while there is an in-progress run, the trigger skips and waits until the next scheduled recurrence interval to check again.</span></span>

<span data-ttu-id="fcfe4-359">Bu ayar işlemi seçeneklerle yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fcfe4-359">You can configure this setting through the operation options:</span></span>

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

## <a name="types-and-inputs"></a><span data-ttu-id="fcfe4-360">Türleri ve girişleri</span><span class="sxs-lookup"><span data-stu-id="fcfe4-360">Types and inputs</span></span>  

<span data-ttu-id="fcfe4-361">Eylemler, her benzersiz davranışına sahip birçok tür vardır.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-361">There are many types of actions, each with unique behavior.</span></span> <span data-ttu-id="fcfe4-362">Koleksiyon Eylemler kendisini içinde birçok diğer eylemler içerebilir.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-362">Collection actions may contain many other actions within itself.</span></span>

### <a name="standard-actions"></a><span data-ttu-id="fcfe4-363">Standart Eylemler</span><span class="sxs-lookup"><span data-stu-id="fcfe4-363">Standard actions</span></span>  

-   <span data-ttu-id="fcfe4-364">**HTTP** bir HTTP web uç noktası bu eylemi çağırır.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-364">**HTTP** This action calls an HTTP web endpoint.</span></span>  
  
-   <span data-ttu-id="fcfe4-365">**ApiConnection** \- Bu eylem HTTP eylemi gibi davranır, ancak Microsoft tarafından yönetilen API'lerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-365">**ApiConnection** \- This action behaves like the HTTP action, but uses the Microsoft-managed APIs.</span></span>  
  
-   <span data-ttu-id="fcfe4-366">**ApiConnectionWebhook** \- gibi HTTPWebhook, ancak Microsoft tarafından yönetilen API'lerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-366">**ApiConnectionWebhook** \- Like HTTPWebhook, but uses the Microsoft-managed APIs.</span></span>  
  
-   <span data-ttu-id="fcfe4-367">**Yanıt** \- gelen bir arama için bir yanıt bu eylemi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-367">**Response** \- This action defines a response for an incoming call.</span></span>  
  
-   <span data-ttu-id="fcfe4-368">**Bekleyin** \- bu basit işlem sabit bir tutar saat veya belirli bir süre kadar bekler.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-368">**Wait** \- This simple action waits a fixed amount of time or until a specific time.</span></span>  
  
-   <span data-ttu-id="fcfe4-369">**İş akışı** \- Bu eylem bir iç içe geçmiş iş akışını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-369">**Workflow** \- This action represents a nested workflow.</span></span>  

-   <span data-ttu-id="fcfe4-370">**İşlev** \- Bu eylem bir Azure işlevi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-370">**Function** \- This action represents an Azure Function.</span></span>

### <a name="collection-actions"></a><span data-ttu-id="fcfe4-371">Koleksiyon Eylemler</span><span class="sxs-lookup"><span data-stu-id="fcfe4-371">Collection actions</span></span>

-   <span data-ttu-id="fcfe4-372">**Kapsam** \- bu eylemi diğer Eylemler, mantıksal bir gruplandırmasıdır.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-372">**Scope** \- This action is a logical grouping of other actions.</span></span>

-   <span data-ttu-id="fcfe4-373">**Koşul** \- Bu eylem bir ifadeyi değerlendirir ve karşılık gelen sonuç dal yürütür.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-373">**Condition** \- This action evaluates an expression and executes the corresponding result branch.</span></span>

-   <span data-ttu-id="fcfe4-374">**ForEach** \- döngü Bu eylem bir dizisini yineler ve her öğe için iç eylemleri gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-374">**ForEach** \- This looping action iterates through an array and performs inner actions for each item.</span></span>

-   <span data-ttu-id="fcfe4-375">**Kadar** \- bir koşul true olarak sonuçları kadar bu döngü eylem iç Eylemler yürütür.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-375">**Until** \- This looping action executes inner actions until a condition results to true.</span></span>
  
<span data-ttu-id="fcfe4-376">Her eylem farklı bir dizi türü **girişleri** bir eylemin davranışını tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-376">Each type of action has a different set of **inputs** that define an action's behavior.</span></span>  
  
## <a name="http-action"></a><span data-ttu-id="fcfe4-377">HTTP eylemi</span><span class="sxs-lookup"><span data-stu-id="fcfe4-377">HTTP action</span></span>  

<span data-ttu-id="fcfe4-378">HTTP Eylemler belirtilen uç noktasını çağırmak ve iş akışı çalıştırılması gerekip gerekmediğini belirlemek için yanıtı denetleyin.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-378">HTTP actions call a specified endpoint and check the response to determine whether the workflow should run.</span></span> <span data-ttu-id="fcfe4-379">**Girişleri** nesnesini HTTP çağrısıyla oluşturmak için gerekli parametreleri kümesini alır:</span><span class="sxs-lookup"><span data-stu-id="fcfe4-379">The **inputs** object takes the set of parameters required to construct the HTTP call:</span></span>  
  
|<span data-ttu-id="fcfe4-380">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="fcfe4-380">Element name</span></span>|<span data-ttu-id="fcfe4-381">Gerekli</span><span class="sxs-lookup"><span data-stu-id="fcfe4-381">Required</span></span>|<span data-ttu-id="fcfe4-382">Tür</span><span class="sxs-lookup"><span data-stu-id="fcfe4-382">Type</span></span>|<span data-ttu-id="fcfe4-383">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fcfe4-383">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="fcfe4-384">Yöntemi</span><span class="sxs-lookup"><span data-stu-id="fcfe4-384">method</span></span>|<span data-ttu-id="fcfe4-385">Evet</span><span class="sxs-lookup"><span data-stu-id="fcfe4-385">Yes</span></span>|<span data-ttu-id="fcfe4-386">Dize</span><span class="sxs-lookup"><span data-stu-id="fcfe4-386">String</span></span>|<span data-ttu-id="fcfe4-387">Aşağıdaki HTTP yöntemlerden biri olabilir: **almak**, **POST**, **PUT**, **silmek**, **düzeltme eki**, veya  **HEAD**</span><span class="sxs-lookup"><span data-stu-id="fcfe4-387">Can be one of the following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="fcfe4-388">URI</span><span class="sxs-lookup"><span data-stu-id="fcfe4-388">uri</span></span>|<span data-ttu-id="fcfe4-389">Evet</span><span class="sxs-lookup"><span data-stu-id="fcfe4-389">Yes</span></span>|<span data-ttu-id="fcfe4-390">Dize</span><span class="sxs-lookup"><span data-stu-id="fcfe4-390">String</span></span>|<span data-ttu-id="fcfe4-391">Çağrılan http veya https uç noktası.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-391">The http or https endpoint that is called.</span></span> <span data-ttu-id="fcfe4-392">En fazla uzunluğu 2 kilobayttır.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-392">Maximum length is 2 kilobytes.</span></span>|  
|<span data-ttu-id="fcfe4-393">Sorguları</span><span class="sxs-lookup"><span data-stu-id="fcfe4-393">queries</span></span>|<span data-ttu-id="fcfe4-394">Hayır</span><span class="sxs-lookup"><span data-stu-id="fcfe4-394">No</span></span>|<span data-ttu-id="fcfe4-395">Nesne</span><span class="sxs-lookup"><span data-stu-id="fcfe4-395">Object</span></span>|<span data-ttu-id="fcfe4-396">URL'ye eklemek için sorgu parametreleri temsil eder.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-396">Represents the query parameters to add to the URL.</span></span> <span data-ttu-id="fcfe4-397">Örneğin, `"queries" : { "api-version": "2015-02-01" }` ekler `?api-version=2015-02-01` URL.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-397">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|  
|<span data-ttu-id="fcfe4-398">Üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="fcfe4-398">headers</span></span>|<span data-ttu-id="fcfe4-399">Hayır</span><span class="sxs-lookup"><span data-stu-id="fcfe4-399">No</span></span>|<span data-ttu-id="fcfe4-400">Nesne</span><span class="sxs-lookup"><span data-stu-id="fcfe4-400">Object</span></span>|<span data-ttu-id="fcfe4-401">Her isteği gönderilen üstbilgilerinin temsil eder.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-401">Represents each of the headers that is sent to the request.</span></span> <span data-ttu-id="fcfe4-402">Örneğin, dilini ayarlamak ve bir istek yazmak için şunu yazın:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="fcfe4-402">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="fcfe4-403">Gövde</span><span class="sxs-lookup"><span data-stu-id="fcfe4-403">body</span></span>|<span data-ttu-id="fcfe4-404">Hayır</span><span class="sxs-lookup"><span data-stu-id="fcfe4-404">No</span></span>|<span data-ttu-id="fcfe4-405">Nesne</span><span class="sxs-lookup"><span data-stu-id="fcfe4-405">Object</span></span>|<span data-ttu-id="fcfe4-406">Uç noktasına gönderilen yükünü temsil eder.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-406">Represents the payload that is sent to the endpoint.</span></span>|  
|<span data-ttu-id="fcfe4-407">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="fcfe4-407">retryPolicy</span></span>|<span data-ttu-id="fcfe4-408">Hayır</span><span class="sxs-lookup"><span data-stu-id="fcfe4-408">No</span></span>|<span data-ttu-id="fcfe4-409">Nesne</span><span class="sxs-lookup"><span data-stu-id="fcfe4-409">Object</span></span>|<span data-ttu-id="fcfe4-410">4xx veya 5xx hataları yeniden deneme davranışını özelleştirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-410">Lets you customize the retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="fcfe4-411">operationsOptions</span><span class="sxs-lookup"><span data-stu-id="fcfe4-411">operationsOptions</span></span>|<span data-ttu-id="fcfe4-412">Hayır</span><span class="sxs-lookup"><span data-stu-id="fcfe4-412">No</span></span>|<span data-ttu-id="fcfe4-413">Dize</span><span class="sxs-lookup"><span data-stu-id="fcfe4-413">String</span></span>|<span data-ttu-id="fcfe4-414">Geçersiz kılmak için özel davranışları kümesini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-414">Defines the set of special behaviors to override.</span></span>|  
|<span data-ttu-id="fcfe4-415">Kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="fcfe4-415">authentication</span></span>|<span data-ttu-id="fcfe4-416">Hayır</span><span class="sxs-lookup"><span data-stu-id="fcfe4-416">No</span></span>|<span data-ttu-id="fcfe4-417">Nesne</span><span class="sxs-lookup"><span data-stu-id="fcfe4-417">Object</span></span>|<span data-ttu-id="fcfe4-418">İsteğin kimliği olduğunu yöntemi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-418">Represents the method that the request should be authenticated.</span></span> <span data-ttu-id="fcfe4-419">Bu nesne üzerinde daha fazla bilgi için bkz [Scheduler giden bağlantı kimlik doğrulaması](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span><span class="sxs-lookup"><span data-stu-id="fcfe4-419">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span></span> <span data-ttu-id="fcfe4-420">Zamanlayıcı daha desteklenen bir özellik yok: `authority`.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-420">Beyond scheduler, there is one more supported property: `authority`.</span></span> <span data-ttu-id="fcfe4-421">Varsayılan olarak, `https://login.windows.net` belirtilmediğinde, ancak gibi farklı bir kitleye kullanabilirsiniz`https://login.windows\-ppe.net`</span><span class="sxs-lookup"><span data-stu-id="fcfe4-421">By default, this is `https://login.windows.net` when not specified, but you can use a different audience like `https://login.windows\-ppe.net`</span></span>|  
  
<span data-ttu-id="fcfe4-422">HTTP Eylemler \(ve API bağlantısı\) Eylemler destek ilkeleri yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-422">HTTP actions \(and API Connection\) actions support retry policies.</span></span> <span data-ttu-id="fcfe4-423">408, 429 ve tüm bağlantı özel durumları yanı sıra 5xx aralıklı hatalar, HTTP durum kodları işlemleri için bir yeniden deneme ilkesi uygulanır.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-423">A retry policy applies to intermittent failures, characterized as HTTP status codes 408, 429, and 5xx, in addition to any connectivity exceptions.</span></span> <span data-ttu-id="fcfe4-424">Bu ilke kullanılarak tanımlanır *retryPolicy* aşağıda gösterildiği gibi tanımlanan nesnesi:</span><span class="sxs-lookup"><span data-stu-id="fcfe4-424">This policy is described using the *retryPolicy* object defined as shown here:</span></span>
  
```json
"retryPolicy" : {
    "type": "<type-of-retry-policy>",
    "interval": <retry-interval>,
    "count": <number-of-retry-attempts>
}
```
  
<span data-ttu-id="fcfe4-425">Yeniden deneme aralığını ISO 8601 biçiminde belirtilir.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-425">The retry interval is specified in the ISO 8601 format.</span></span> <span data-ttu-id="fcfe4-426">En büyük değer bir saat olsa da bu aralığı 20 saniye varsayılan ve en az değerine sahip.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-426">This interval has a default and minimum value of 20 seconds, while the maximum value is one hour.</span></span> <span data-ttu-id="fcfe4-427">Varsayılan ve en fazla yeniden deneme sayısı dört saattir.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-427">The default and maximum retry count is four hours.</span></span> <span data-ttu-id="fcfe4-428">Yeniden deneme ilkesi tanımı belirtilmezse, bir `fixed` stratejisi varsayılan yeniden deneme sayısı ve aralığı değerlerle kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-428">If the retry policy definition is not specified, a `fixed` strategy is used with default retry count and interval values.</span></span> <span data-ttu-id="fcfe4-429">Yeniden deneme ilkesi devre dışı bırakmak için türünü ayarlamak `None`.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-429">To disable the retry policy, set its type to `None`.</span></span>  
  
<span data-ttu-id="fcfe4-430">Her denemesi arasındaki 30 saniyelik gecikmeyle üç yürütmeleri toplam aralıklı hatalar varsa en son haberleri iki kez getiriliyor. Örneğin, aşağıdaki eylem yeniden deneme sayısı:</span><span class="sxs-lookup"><span data-stu-id="fcfe4-430">For example, the following action retries fetching the latest news two times, if there are intermittent failures, for a total of three executions, with a 30-second delay between each attempt:</span></span>  
  
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
### <a name="asynchronous-patterns"></a><span data-ttu-id="fcfe4-431">Zaman uyumsuz desenleri</span><span class="sxs-lookup"><span data-stu-id="fcfe4-431">Asynchronous patterns</span></span>

<span data-ttu-id="fcfe4-432">Varsayılan olarak, tüm HTTP tabanlı eylemleri standart zaman uyumsuz işlem düzenini destekler.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-432">By default, all HTTP-based actions support the standard asynchronous operation pattern.</span></span> <span data-ttu-id="fcfe4-433">Uzak sunucu isteği bir 202 işleme için kabul edilir olduğunu gösteriyorsa, bunu \(kabul edilen\) yanıt, Logic Apps altyapısı tutar yoklama terminaldurumunaulaşmasınıkadaryanıtınkonumuüstbilgisindebelirtilenURL\(olmayan bir\-202 yanıt\).</span><span class="sxs-lookup"><span data-stu-id="fcfe4-433">So if the remote server indicates that the request is accepted for processing with a 202 \(Accepted\) response, the Logic Apps engine keeps polling the URL specified in the response's location header until reaching a terminal state \(a non\-202 response\).</span></span>  
  
<span data-ttu-id="fcfe4-434">Daha önce açıklanan zaman uyumsuz davranışı devre dışı bırakmak için ayarlanmış bir `DisableAsyncPattern` eylem girişleri seçeneği.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-434">To disable the asynchronous behavior previously described, set a `DisableAsyncPattern` option in the action inputs.</span></span> <span data-ttu-id="fcfe4-435">Bu durumda, eylemin çıkış sunucusundan ilk 202 yanıt temel alır.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-435">In this case, the output of the action is based on the initial 202 response from the server.</span></span>  
  
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

#### <a name="asynchronous-limits"></a><span data-ttu-id="fcfe4-436">Zaman uyumsuz sınırları</span><span class="sxs-lookup"><span data-stu-id="fcfe4-436">Asynchronous Limits</span></span>

<span data-ttu-id="fcfe4-437">Zaman uyumsuz desen süresinin belirli bir zaman aralığı için sınırlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-437">An asynchronous pattern can be limited in its duration to a specific time interval.</span></span>  <span data-ttu-id="fcfe4-438">Terminal durumuna erişmeden zaman aralığını aşılırsa, eylemin durumunu işaretlenecek `Cancelled` koduyla `ActionTimedOut`.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-438">If the time interval elapses without reaching a terminal state, the status of the action will be marked `Cancelled` with a code of `ActionTimedOut`.</span></span>  <span data-ttu-id="fcfe4-439">Sınır zaman aşımı ISO 8601 biçiminde belirtilir.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-439">The limit timeout is specified in ISO 8601 format.</span></span>  <span data-ttu-id="fcfe4-440">Sınırları, aşağıdaki sözdizimi ile belirtilebilir:</span><span class="sxs-lookup"><span data-stu-id="fcfe4-440">Limits can be specified with the following syntax:</span></span>

``` json
"<action-name>": {
    "type": "workflow|webhook|http|apiconnectionwebhook|apiconnection",
    "inputs": { },
    "limit": {
        "timeout": "PT10S"
    }
}
```
  
## <a name="api-connection"></a><span data-ttu-id="fcfe4-441">API bağlantısı</span><span class="sxs-lookup"><span data-stu-id="fcfe4-441">API Connection</span></span>  

<span data-ttu-id="fcfe4-442">API bağlantı Microsoft tarafından yönetilen bir bağlayıcı başvuruda bulunan bir eylemdir.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-442">API Connection is an action that references a Microsoft-managed connector.</span></span>
<span data-ttu-id="fcfe4-443">Bu eylem geçerli bir bağlantı ve API ve gerekli parametreleri hakkında bilgi için bir başvuru gerektirir.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-443">This action requires a reference to a valid connection, and information on the API and parameters required.</span></span>

|<span data-ttu-id="fcfe4-444">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="fcfe4-444">Element name</span></span>|<span data-ttu-id="fcfe4-445">Gerekli</span><span class="sxs-lookup"><span data-stu-id="fcfe4-445">Required</span></span>|<span data-ttu-id="fcfe4-446">Tür</span><span class="sxs-lookup"><span data-stu-id="fcfe4-446">Type</span></span>|<span data-ttu-id="fcfe4-447">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fcfe4-447">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="fcfe4-448">ana bilgisayar</span><span class="sxs-lookup"><span data-stu-id="fcfe4-448">host</span></span>|<span data-ttu-id="fcfe4-449">Evet</span><span class="sxs-lookup"><span data-stu-id="fcfe4-449">Yes</span></span>|<span data-ttu-id="fcfe4-450">Nesne</span><span class="sxs-lookup"><span data-stu-id="fcfe4-450">Object</span></span>|<span data-ttu-id="fcfe4-451">Bağlantı nesnesine başvuru ve runtimeUrl gibi bağlayıcı bilgileri temsil eder</span><span class="sxs-lookup"><span data-stu-id="fcfe4-451">Represents the connector information such as the runtimeUrl and reference to the connection object</span></span>|
|<span data-ttu-id="fcfe4-452">Yöntemi</span><span class="sxs-lookup"><span data-stu-id="fcfe4-452">method</span></span>|<span data-ttu-id="fcfe4-453">Evet</span><span class="sxs-lookup"><span data-stu-id="fcfe4-453">Yes</span></span>|<span data-ttu-id="fcfe4-454">Dize</span><span class="sxs-lookup"><span data-stu-id="fcfe4-454">String</span></span>|<span data-ttu-id="fcfe4-455">Aşağıdaki HTTP yöntemlerden biri olabilir: **almak**, **POST**, **PUT**, **silmek**, **düzeltme eki**, veya  **HEAD**</span><span class="sxs-lookup"><span data-stu-id="fcfe4-455">Can be one of the following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="fcfe4-456">Yol</span><span class="sxs-lookup"><span data-stu-id="fcfe4-456">path</span></span>|<span data-ttu-id="fcfe4-457">Evet</span><span class="sxs-lookup"><span data-stu-id="fcfe4-457">Yes</span></span>|<span data-ttu-id="fcfe4-458">Dize</span><span class="sxs-lookup"><span data-stu-id="fcfe4-458">String</span></span>|<span data-ttu-id="fcfe4-459">API işlemi yolu.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-459">The path of the API operation.</span></span>|  
|<span data-ttu-id="fcfe4-460">Sorguları</span><span class="sxs-lookup"><span data-stu-id="fcfe4-460">queries</span></span>|<span data-ttu-id="fcfe4-461">Hayır</span><span class="sxs-lookup"><span data-stu-id="fcfe4-461">No</span></span>|<span data-ttu-id="fcfe4-462">Nesne</span><span class="sxs-lookup"><span data-stu-id="fcfe4-462">Object</span></span>|<span data-ttu-id="fcfe4-463">URL'ye eklemek için sorgu parametreleri temsil eder.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-463">Represents the query parameters to add to the URL.</span></span> <span data-ttu-id="fcfe4-464">Örneğin, `"queries" : { "api-version": "2015-02-01" }` ekler `?api-version=2015-02-01` URL.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-464">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|  
|<span data-ttu-id="fcfe4-465">Üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="fcfe4-465">headers</span></span>|<span data-ttu-id="fcfe4-466">Hayır</span><span class="sxs-lookup"><span data-stu-id="fcfe4-466">No</span></span>|<span data-ttu-id="fcfe4-467">Nesne</span><span class="sxs-lookup"><span data-stu-id="fcfe4-467">Object</span></span>|<span data-ttu-id="fcfe4-468">Her isteği gönderilen üstbilgilerinin temsil eder.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-468">Represents each of the headers that is sent to the request.</span></span> <span data-ttu-id="fcfe4-469">Örneğin, dilini ayarlamak ve bir istek yazmak için şunu yazın:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="fcfe4-469">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="fcfe4-470">Gövde</span><span class="sxs-lookup"><span data-stu-id="fcfe4-470">body</span></span>|<span data-ttu-id="fcfe4-471">Hayır</span><span class="sxs-lookup"><span data-stu-id="fcfe4-471">No</span></span>|<span data-ttu-id="fcfe4-472">Nesne</span><span class="sxs-lookup"><span data-stu-id="fcfe4-472">Object</span></span>|<span data-ttu-id="fcfe4-473">Uç noktasına gönderilen yükünü temsil eder.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-473">Represents the payload that is sent to the endpoint.</span></span>|  
|<span data-ttu-id="fcfe4-474">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="fcfe4-474">retryPolicy</span></span>|<span data-ttu-id="fcfe4-475">Hayır</span><span class="sxs-lookup"><span data-stu-id="fcfe4-475">No</span></span>|<span data-ttu-id="fcfe4-476">Nesne</span><span class="sxs-lookup"><span data-stu-id="fcfe4-476">Object</span></span>|<span data-ttu-id="fcfe4-477">4xx veya 5xx hataları yeniden deneme davranışını özelleştirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-477">Lets you customize the retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="fcfe4-478">operationsOptions</span><span class="sxs-lookup"><span data-stu-id="fcfe4-478">operationsOptions</span></span>|<span data-ttu-id="fcfe4-479">Hayır</span><span class="sxs-lookup"><span data-stu-id="fcfe4-479">No</span></span>|<span data-ttu-id="fcfe4-480">Dize</span><span class="sxs-lookup"><span data-stu-id="fcfe4-480">String</span></span>|<span data-ttu-id="fcfe4-481">Geçersiz kılmak için özel davranışları kümesini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-481">Defines the set of special behaviors to override.</span></span>|  

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

## <a name="api-connection-webhook-action"></a><span data-ttu-id="fcfe4-482">API bağlantısı Web kancası eylemi</span><span class="sxs-lookup"><span data-stu-id="fcfe4-482">API Connection webhook action</span></span>

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

<span data-ttu-id="fcfe4-483">Bir Web kancası eylemi sınırları, aynı şekilde belirtilebilir [HTTP zaman uyumsuz sınırları](#asynchronous-limits).</span><span class="sxs-lookup"><span data-stu-id="fcfe4-483">Limits on a webhook action can be specified in the same manner as [HTTP Asynchronous Limits](#asynchronous-limits).</span></span>
  
## <a name="response-action"></a><span data-ttu-id="fcfe4-484">Yanıt eylemi</span><span class="sxs-lookup"><span data-stu-id="fcfe4-484">Response action</span></span>  

<span data-ttu-id="fcfe4-485">Bu eylem türü bir HTTP isteği tüm yanıt yükü içerir ve bir statusCode, metnini ve üst bilgileri içerir:</span><span class="sxs-lookup"><span data-stu-id="fcfe4-485">This action type contains the entire response payload from an HTTP request and includes a statusCode, body, and headers:</span></span>  
  
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
  
<span data-ttu-id="fcfe4-486">Yanıt eylemi diğer eylemler için uygulama özel sınırlamalar vardır.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-486">The response action has special restrictions that don't apply to other actions.</span></span> <span data-ttu-id="fcfe4-487">Bu avantajlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="fcfe4-487">Specifically:</span></span>  
  
-   <span data-ttu-id="fcfe4-488">Gelen istek belirleyici yanıt gerektiğinden yanıt eylemlerinizi bir tanım paralel olamaz.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-488">Response actions cannot be parallel in a definition because a deterministic response to the incoming request is required.</span></span>  
  
-   <span data-ttu-id="fcfe4-489">Gelen istek yanıt aldıktan sonra bir yanıt eylemi ulaştıysanız, eylem olarak kabul başarısız \(çakışma\), ve sonuç olarak, çalışma `Failed`.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-489">If a response action is reached after the incoming request has received a response, the action is considered failed \(conflict\), and as a result, the run is `Failed`.</span></span>  
  
-   <span data-ttu-id="fcfe4-490">Yanıt eylemleri içeren bir iş akışının olamaz `splitOn` , tetikleyici içinde birçok çalışır bir çağrı neden olduğundan.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-490">A workflow with Response actions cannot have `splitOn` in its trigger because one call causes many runs.</span></span> <span data-ttu-id="fcfe4-491">Sonuç olarak, akış PUT ve nedeni hatalı istek olduğunda bu doğrulanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-491">As a result, this should be validated when the flow is PUT and cause a Bad Request.</span></span>  
  
## <a name="wait-action"></a><span data-ttu-id="fcfe4-492">Eylem bekleyin</span><span class="sxs-lookup"><span data-stu-id="fcfe4-492">Wait action</span></span>  

<span data-ttu-id="fcfe4-493">`wait` Eylem iş akışı yürütme belirtilen zaman aralığı için askıya alır.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-493">The `wait` action suspends workflow execution for the specified interval.</span></span> <span data-ttu-id="fcfe4-494">Örneğin, 15 dakika beklemek için bu parçacığı kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fcfe4-494">For example, to wait 15 minutes, you can use this snippet:</span></span>  
  
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
  
<span data-ttu-id="fcfe4-495">Alternatif olarak, zaman içinde belirli bir süre kadar beklemek için bu örnek kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fcfe4-495">Alternatively, to wait until a specific moment in time, you can use this example:</span></span>  
  
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
> <span data-ttu-id="fcfe4-496">Bekleme süresi kullanılarak da belirtilebilir **aralığı** nesne veya **kadar** nesnesi, ancak ikisini birden değil.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-496">The wait duration can be either specified using the **interval** object or the **until** object, but not both.</span></span>  
  
|<span data-ttu-id="fcfe4-497">Ad</span><span class="sxs-lookup"><span data-stu-id="fcfe4-497">Name</span></span>|<span data-ttu-id="fcfe4-498">Gerekli</span><span class="sxs-lookup"><span data-stu-id="fcfe4-498">Required</span></span>|<span data-ttu-id="fcfe4-499">Tür</span><span class="sxs-lookup"><span data-stu-id="fcfe4-499">Type</span></span>|<span data-ttu-id="fcfe4-500">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fcfe4-500">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="fcfe4-501">aralığı</span><span class="sxs-lookup"><span data-stu-id="fcfe4-501">interval</span></span>|<span data-ttu-id="fcfe4-502">Hayır</span><span class="sxs-lookup"><span data-stu-id="fcfe4-502">No</span></span>|<span data-ttu-id="fcfe4-503">Nesne</span><span class="sxs-lookup"><span data-stu-id="fcfe4-503">Object</span></span>|<span data-ttu-id="fcfe4-504">Zaman miktarına bağlı bekleme süresi.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-504">The wait duration based on amount of time.</span></span>|  
|<span data-ttu-id="fcfe4-505">aralığı birimi</span><span class="sxs-lookup"><span data-stu-id="fcfe4-505">interval unit</span></span>|<span data-ttu-id="fcfe4-506">Evet</span><span class="sxs-lookup"><span data-stu-id="fcfe4-506">Yes</span></span>|<span data-ttu-id="fcfe4-507">Dize</span><span class="sxs-lookup"><span data-stu-id="fcfe4-507">String</span></span>|<span data-ttu-id="fcfe4-508">Bu aralıklar birini: saniye, dakika, saat, gün, hafta, ay, yıl.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-508">One of these intervals: second, minute, hour, day, week, month, year.</span></span>|  
|<span data-ttu-id="fcfe4-509">Aralık sayısı</span><span class="sxs-lookup"><span data-stu-id="fcfe4-509">interval count</span></span>|<span data-ttu-id="fcfe4-510">Evet</span><span class="sxs-lookup"><span data-stu-id="fcfe4-510">Yes</span></span>|<span data-ttu-id="fcfe4-511">Dize</span><span class="sxs-lookup"><span data-stu-id="fcfe4-511">String</span></span>|<span data-ttu-id="fcfe4-512">Verilen iç birimine dayalı süresi.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-512">Duration based on the given internal unit.</span></span>|  
|<span data-ttu-id="fcfe4-513">kadar</span><span class="sxs-lookup"><span data-stu-id="fcfe4-513">until</span></span>|<span data-ttu-id="fcfe4-514">Hayır</span><span class="sxs-lookup"><span data-stu-id="fcfe4-514">No</span></span>|<span data-ttu-id="fcfe4-515">Nesne</span><span class="sxs-lookup"><span data-stu-id="fcfe4-515">Object</span></span>|<span data-ttu-id="fcfe4-516">Bekleme süresi bir noktasında zaman dayanır.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-516">The wait duration based on a point in time.</span></span>|  
|<span data-ttu-id="fcfe4-517">zaman damgası kadar</span><span class="sxs-lookup"><span data-stu-id="fcfe4-517">until timestamp</span></span>|<span data-ttu-id="fcfe4-518">Evet</span><span class="sxs-lookup"><span data-stu-id="fcfe4-518">Yes</span></span>|<span data-ttu-id="fcfe4-519">Dize</span><span class="sxs-lookup"><span data-stu-id="fcfe4-519">String</span></span>|<span data-ttu-id="fcfe4-520">Dize &#124; Bekleme süresi dolduğunda UTC zaman içinde nokta.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-520">String&#124;The point in time in UTC when the wait expires.</span></span>|  

## <a name="query-action"></a><span data-ttu-id="fcfe4-521">Sorgu eylemi</span><span class="sxs-lookup"><span data-stu-id="fcfe4-521">Query action</span></span>

<span data-ttu-id="fcfe4-522">`query` Eylemi bir koşula göre bir dizi filtre olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-522">The `query` action lets you filter an array based on a condition.</span></span> <span data-ttu-id="fcfe4-523">Örneğin, 2'den büyük sayılar seçmek için kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fcfe4-523">For example, to select numbers greater than 2, you can use:</span></span>

```json
"FilterNumbers" : {
    "type": "query",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "where": "@greater(item(), 2)"
    }
}
```

<span data-ttu-id="fcfe4-524">Çıktısını `query` koşulu karşılıyor giriş dizisi öğelerinden sahip bir dizi eylemdir.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-524">The output from the `query` action is an array that has elements from the input array that satisfy the condition.</span></span>

> [!NOTE]
> <span data-ttu-id="fcfe4-525">Hiçbir değer belirtecini karşılıyorsa `where` sonucu durumudur boş bir dizi.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-525">If no values satisfy the `where` condition, the result is an empty array.</span></span>

|<span data-ttu-id="fcfe4-526">Ad</span><span class="sxs-lookup"><span data-stu-id="fcfe4-526">Name</span></span>|<span data-ttu-id="fcfe4-527">Gerekli</span><span class="sxs-lookup"><span data-stu-id="fcfe4-527">Required</span></span>|<span data-ttu-id="fcfe4-528">Tür</span><span class="sxs-lookup"><span data-stu-id="fcfe4-528">Type</span></span>|<span data-ttu-id="fcfe4-529">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fcfe4-529">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="fcfe4-530">Kaynak</span><span class="sxs-lookup"><span data-stu-id="fcfe4-530">from</span></span>|<span data-ttu-id="fcfe4-531">Evet</span><span class="sxs-lookup"><span data-stu-id="fcfe4-531">Yes</span></span>|<span data-ttu-id="fcfe4-532">Dizi</span><span class="sxs-lookup"><span data-stu-id="fcfe4-532">Array</span></span>|<span data-ttu-id="fcfe4-533">Kaynak dizi.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-533">The source array.</span></span>|
|<span data-ttu-id="fcfe4-534">Burada</span><span class="sxs-lookup"><span data-stu-id="fcfe4-534">where</span></span>|<span data-ttu-id="fcfe4-535">Evet</span><span class="sxs-lookup"><span data-stu-id="fcfe4-535">Yes</span></span>|<span data-ttu-id="fcfe4-536">Dize</span><span class="sxs-lookup"><span data-stu-id="fcfe4-536">String</span></span>|<span data-ttu-id="fcfe4-537">Kaynak dizinin her öğeye uygulamak için koşulu.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-537">The condition to apply to each element of the source array.</span></span>|

## <a name="select-action"></a><span data-ttu-id="fcfe4-538">Bir eylem seçin</span><span class="sxs-lookup"><span data-stu-id="fcfe4-538">Select action</span></span>

<span data-ttu-id="fcfe4-539">`select` Eylemi yeni bir değer dizideki her öğe proje olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-539">The `select` action lets you project each element of an array into a new value.</span></span>
<span data-ttu-id="fcfe4-540">Örneğin, bir dizi sayının nesnelerinin bir dizisi dönüştürmek için kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fcfe4-540">For example, to convert an array of numbers into an array of objects, you can use:</span></span>

```json
"SelectNumbers" : {
    "type": "select",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "select": { "number": "@item()" }
    }
}
```

<span data-ttu-id="fcfe4-541">Çıktısını `select` giriş dizisi olarak aynı kardinalite tarafından tanımlandığı şekilde dönüştürülmüş her öğeye sahip olan bir dizi eylemdir `select` özelliği.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-541">The output of the `select` action is an array that has the same cardinality as the input array, with each element transformed as defined by the `select` property.</span></span> <span data-ttu-id="fcfe4-542">Girdi boş bir dizi çıkışı da boş bir dizi ise.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-542">If the input is an empty array, the output is also an empty array.</span></span>

|<span data-ttu-id="fcfe4-543">Ad</span><span class="sxs-lookup"><span data-stu-id="fcfe4-543">Name</span></span>|<span data-ttu-id="fcfe4-544">Gerekli</span><span class="sxs-lookup"><span data-stu-id="fcfe4-544">Required</span></span>|<span data-ttu-id="fcfe4-545">Tür</span><span class="sxs-lookup"><span data-stu-id="fcfe4-545">Type</span></span>|<span data-ttu-id="fcfe4-546">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fcfe4-546">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="fcfe4-547">Kaynak</span><span class="sxs-lookup"><span data-stu-id="fcfe4-547">from</span></span>|<span data-ttu-id="fcfe4-548">Evet</span><span class="sxs-lookup"><span data-stu-id="fcfe4-548">Yes</span></span>|<span data-ttu-id="fcfe4-549">Dizi</span><span class="sxs-lookup"><span data-stu-id="fcfe4-549">Array</span></span>|<span data-ttu-id="fcfe4-550">Kaynak dizi.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-550">The source array.</span></span>|
|<span data-ttu-id="fcfe4-551">seçin</span><span class="sxs-lookup"><span data-stu-id="fcfe4-551">select</span></span>|<span data-ttu-id="fcfe4-552">Evet</span><span class="sxs-lookup"><span data-stu-id="fcfe4-552">Yes</span></span>|<span data-ttu-id="fcfe4-553">Herhangi biri</span><span class="sxs-lookup"><span data-stu-id="fcfe4-553">Any</span></span>|<span data-ttu-id="fcfe4-554">Kaynak dizinin her öğeye uygulamak için yansıtma.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-554">The projection to apply to each element of the source array.</span></span>|

## <a name="terminate-action"></a><span data-ttu-id="fcfe4-555">Sonlandırma eylemi</span><span class="sxs-lookup"><span data-stu-id="fcfe4-555">Terminate action</span></span>

<span data-ttu-id="fcfe4-556">Sonlandırma eyleminin yürütülen tüm eylemler durduruluyor ve kalan herhangi bir eylem atlanıyor iş akışı çalışmanın yürütülmesi durdurur.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-556">The Terminate action stops execution of the workflow run, aborting any in-flight actions, and skipping any remaining actions.</span></span> <span data-ttu-id="fcfe4-557">Örneğin, bir çalışma durumuna sahip sonlandırmak için **başarısız**, aşağıdaki kod parçacığında kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fcfe4-557">For example, to terminate a run with status **Failed**, you can use the following snippet:</span></span>

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
> <span data-ttu-id="fcfe4-558">Zaten tamamlanmış Eylemler Sonlandır eylemi tarafından etkilenmez.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-558">Actions already completed are not affected by the terminate action.</span></span>

|<span data-ttu-id="fcfe4-559">Ad</span><span class="sxs-lookup"><span data-stu-id="fcfe4-559">Name</span></span>|<span data-ttu-id="fcfe4-560">Gerekli</span><span class="sxs-lookup"><span data-stu-id="fcfe4-560">Required</span></span>|<span data-ttu-id="fcfe4-561">Tür</span><span class="sxs-lookup"><span data-stu-id="fcfe4-561">Type</span></span>|<span data-ttu-id="fcfe4-562">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fcfe4-562">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="fcfe4-563">runStatus</span><span class="sxs-lookup"><span data-stu-id="fcfe4-563">runStatus</span></span>|<span data-ttu-id="fcfe4-564">Evet</span><span class="sxs-lookup"><span data-stu-id="fcfe4-564">Yes</span></span>|<span data-ttu-id="fcfe4-565">Dize</span><span class="sxs-lookup"><span data-stu-id="fcfe4-565">String</span></span>|<span data-ttu-id="fcfe4-566">Hedef durumu çalıştırma.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-566">The target run status.</span></span> <span data-ttu-id="fcfe4-567">Her iki **başarısız** veya **iptal**.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-567">Either **Failed** or **Cancelled**.</span></span>|
|<span data-ttu-id="fcfe4-568">runError</span><span class="sxs-lookup"><span data-stu-id="fcfe4-568">runError</span></span>|<span data-ttu-id="fcfe4-569">Hayır</span><span class="sxs-lookup"><span data-stu-id="fcfe4-569">No</span></span>|<span data-ttu-id="fcfe4-570">Nesne</span><span class="sxs-lookup"><span data-stu-id="fcfe4-570">Object</span></span>|<span data-ttu-id="fcfe4-571">Hata ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-571">The error details.</span></span> <span data-ttu-id="fcfe4-572">Ne zaman desteklenen yalnızca **runStatus** ayarlanır **başarısız**.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-572">Only supported when **runStatus** is set to **Failed**.</span></span>|
|<span data-ttu-id="fcfe4-573">runError kodu</span><span class="sxs-lookup"><span data-stu-id="fcfe4-573">runError code</span></span>|<span data-ttu-id="fcfe4-574">Hayır</span><span class="sxs-lookup"><span data-stu-id="fcfe4-574">No</span></span>|<span data-ttu-id="fcfe4-575">Dize</span><span class="sxs-lookup"><span data-stu-id="fcfe4-575">String</span></span>|<span data-ttu-id="fcfe4-576">Çalışma hata kodu.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-576">The run error code.</span></span>|
|<span data-ttu-id="fcfe4-577">runError iletisi</span><span class="sxs-lookup"><span data-stu-id="fcfe4-577">runError message</span></span>|<span data-ttu-id="fcfe4-578">Hayır</span><span class="sxs-lookup"><span data-stu-id="fcfe4-578">No</span></span>|<span data-ttu-id="fcfe4-579">Dize</span><span class="sxs-lookup"><span data-stu-id="fcfe4-579">String</span></span>|<span data-ttu-id="fcfe4-580">Çalışma hata iletisi.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-580">The run error message.</span></span>|

## <a name="compose-action"></a><span data-ttu-id="fcfe4-581">Eylem oluşturma</span><span class="sxs-lookup"><span data-stu-id="fcfe4-581">Compose action</span></span>

<span data-ttu-id="fcfe4-582">Oluşturma eylem rastgele bir nesne oluşturmak olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-582">The Compose action lets you construct an arbitrary object.</span></span> <span data-ttu-id="fcfe4-583">Oluşturma eylem çıktısını girdilerinden değerlendirme sonucudur.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-583">The output of the compose action is the result of evaluating its inputs.</span></span> <span data-ttu-id="fcfe4-584">Örneğin, birden çok eylem çıkışları birleştirmek için oluşturma eylemini kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fcfe4-584">For example, you can use the compose action to merge outputs of multiple actions:</span></span>

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
> <span data-ttu-id="fcfe4-585">**Oluşturma** eylem nesneleri, dizileri ve yerel olarak XML ve ikili gibi mantıksal uygulamalar tarafından desteklenen herhangi bir türü de dahil olmak üzere herhangi bir çıktı oluşturmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-585">The **Compose** action can be used to construct any output, including objects, arrays, and any other type natively supported by logic apps like XML and binary.</span></span>

## <a name="table-action"></a><span data-ttu-id="fcfe4-586">Tablo eylemi</span><span class="sxs-lookup"><span data-stu-id="fcfe4-586">Table action</span></span>

<span data-ttu-id="fcfe4-587">`table` Öğeleri dizisi dönüştürmenize olanak sağlayan bir **CSV** veya **HTML** tablo.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-587">The `table` allows you to convert an array of items into a **CSV** or **HTML** table.</span></span>

<span data-ttu-id="fcfe4-588">Varsayalım @triggerBody() değil</span><span class="sxs-lookup"><span data-stu-id="fcfe4-588">Suppose @triggerBody() is</span></span>

```json
[{
  "id": 0,
  "name": "apples"
},{
  "id": 1, 
  "name": "oranges"
}]
```

<span data-ttu-id="fcfe4-589">Ve olarak tanımladığı eylem izin verin</span><span class="sxs-lookup"><span data-stu-id="fcfe4-589">And let the action be defined as</span></span>

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html"
    }
}
```

<span data-ttu-id="fcfe4-590">Yukarıdaki oluşturur</span><span class="sxs-lookup"><span data-stu-id="fcfe4-590">The above would produce</span></span>

<table><thead><tr><th><span data-ttu-id="fcfe4-591">id</span><span class="sxs-lookup"><span data-stu-id="fcfe4-591">id</span></span></th><th><span data-ttu-id="fcfe4-592">ad</span><span class="sxs-lookup"><span data-stu-id="fcfe4-592">name</span></span></th></tr></thead><tbody><tr><td><span data-ttu-id="fcfe4-593">0</span><span class="sxs-lookup"><span data-stu-id="fcfe4-593">0</span></span></td><td><span data-ttu-id="fcfe4-594">elmalar</span><span class="sxs-lookup"><span data-stu-id="fcfe4-594">apples</span></span></td></tr><tr><td><span data-ttu-id="fcfe4-595">1</span><span class="sxs-lookup"><span data-stu-id="fcfe4-595">1</span></span></td><td><span data-ttu-id="fcfe4-596">portakallar</span><span class="sxs-lookup"><span data-stu-id="fcfe4-596">oranges</span></span></td></tr></tbody></table><span data-ttu-id="fcfe4-597">"</span><span class="sxs-lookup"><span data-stu-id="fcfe4-597">"</span></span>

<span data-ttu-id="fcfe4-598">Tablo özelleştirmek için sütunları açıkça belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-598">In order to customize the table, you can specify the columns explicitly.</span></span> <span data-ttu-id="fcfe4-599">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="fcfe4-599">For example:</span></span>

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

<span data-ttu-id="fcfe4-600">Yukarıdaki oluşturur</span><span class="sxs-lookup"><span data-stu-id="fcfe4-600">The above would produce</span></span>

<table><thead><tr><th><span data-ttu-id="fcfe4-601">kimliği oluşturmak</span><span class="sxs-lookup"><span data-stu-id="fcfe4-601">produce id</span></span></th><th><span data-ttu-id="fcfe4-602">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fcfe4-602">description</span></span></th></tr></thead><tbody><tr><td><span data-ttu-id="fcfe4-603">0</span><span class="sxs-lookup"><span data-stu-id="fcfe4-603">0</span></span></td><td><span data-ttu-id="fcfe4-604">Yeni elmalar</span><span class="sxs-lookup"><span data-stu-id="fcfe4-604">fresh apples</span></span></td></tr><tr><td><span data-ttu-id="fcfe4-605">1</span><span class="sxs-lookup"><span data-stu-id="fcfe4-605">1</span></span></td><td><span data-ttu-id="fcfe4-606">Yeni portakallar</span><span class="sxs-lookup"><span data-stu-id="fcfe4-606">fresh oranges</span></span></td></tr></tbody></table><span data-ttu-id="fcfe4-607">"</span><span class="sxs-lookup"><span data-stu-id="fcfe4-607">"</span></span>

<span data-ttu-id="fcfe4-608">Varsa `from` özellik değeri boş bir dizi, çıktı boş bir tablo.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-608">If the `from` property value is an empty array, the output is an empty table.</span></span>

|<span data-ttu-id="fcfe4-609">Ad</span><span class="sxs-lookup"><span data-stu-id="fcfe4-609">Name</span></span>|<span data-ttu-id="fcfe4-610">Gerekli</span><span class="sxs-lookup"><span data-stu-id="fcfe4-610">Required</span></span>|<span data-ttu-id="fcfe4-611">Tür</span><span class="sxs-lookup"><span data-stu-id="fcfe4-611">Type</span></span>|<span data-ttu-id="fcfe4-612">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fcfe4-612">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="fcfe4-613">Kaynak</span><span class="sxs-lookup"><span data-stu-id="fcfe4-613">from</span></span>|<span data-ttu-id="fcfe4-614">Evet</span><span class="sxs-lookup"><span data-stu-id="fcfe4-614">Yes</span></span>|<span data-ttu-id="fcfe4-615">Dizi</span><span class="sxs-lookup"><span data-stu-id="fcfe4-615">Array</span></span>|<span data-ttu-id="fcfe4-616">Kaynak dizi.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-616">The source array.</span></span>|
|<span data-ttu-id="fcfe4-617">Biçimi</span><span class="sxs-lookup"><span data-stu-id="fcfe4-617">format</span></span>|<span data-ttu-id="fcfe4-618">Evet</span><span class="sxs-lookup"><span data-stu-id="fcfe4-618">Yes</span></span>|<span data-ttu-id="fcfe4-619">Dize</span><span class="sxs-lookup"><span data-stu-id="fcfe4-619">String</span></span>|<span data-ttu-id="fcfe4-620">Biçim ya da **CSV** veya **HTML**.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-620">The format, either **CSV** or **HTML**.</span></span>|
|<span data-ttu-id="fcfe4-621">sütunları</span><span class="sxs-lookup"><span data-stu-id="fcfe4-621">columns</span></span>|<span data-ttu-id="fcfe4-622">Hayır</span><span class="sxs-lookup"><span data-stu-id="fcfe4-622">No</span></span>|<span data-ttu-id="fcfe4-623">Dizi</span><span class="sxs-lookup"><span data-stu-id="fcfe4-623">Array</span></span>|<span data-ttu-id="fcfe4-624">Sütunlar.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-624">The columns.</span></span> <span data-ttu-id="fcfe4-625">Tablonun varsayılan Şekil geçersiz kılmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-625">Allows to override the default shape of the table.</span></span>|
|<span data-ttu-id="fcfe4-626">sütun başlığı</span><span class="sxs-lookup"><span data-stu-id="fcfe4-626">column header</span></span>|<span data-ttu-id="fcfe4-627">Hayır</span><span class="sxs-lookup"><span data-stu-id="fcfe4-627">No</span></span>|<span data-ttu-id="fcfe4-628">Dize</span><span class="sxs-lookup"><span data-stu-id="fcfe4-628">String</span></span>|<span data-ttu-id="fcfe4-629">Sütun başlığı.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-629">The header of the column.</span></span>|
|<span data-ttu-id="fcfe4-630">Sütun değeri</span><span class="sxs-lookup"><span data-stu-id="fcfe4-630">column value</span></span>|<span data-ttu-id="fcfe4-631">Evet</span><span class="sxs-lookup"><span data-stu-id="fcfe4-631">Yes</span></span>|<span data-ttu-id="fcfe4-632">Dize</span><span class="sxs-lookup"><span data-stu-id="fcfe4-632">String</span></span>|<span data-ttu-id="fcfe4-633">Sütun değeri.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-633">The value of the column.</span></span>|

## <a name="workflow-action"></a><span data-ttu-id="fcfe4-634">İş akışı eylemi</span><span class="sxs-lookup"><span data-stu-id="fcfe4-634">Workflow action</span></span>   

|<span data-ttu-id="fcfe4-635">Ad</span><span class="sxs-lookup"><span data-stu-id="fcfe4-635">Name</span></span>|<span data-ttu-id="fcfe4-636">Gerekli</span><span class="sxs-lookup"><span data-stu-id="fcfe4-636">Required</span></span>|<span data-ttu-id="fcfe4-637">Tür</span><span class="sxs-lookup"><span data-stu-id="fcfe4-637">Type</span></span>|<span data-ttu-id="fcfe4-638">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fcfe4-638">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="fcfe4-639">ana bilgisayar kimliği</span><span class="sxs-lookup"><span data-stu-id="fcfe4-639">host id</span></span>|<span data-ttu-id="fcfe4-640">Evet</span><span class="sxs-lookup"><span data-stu-id="fcfe4-640">Yes</span></span>|<span data-ttu-id="fcfe4-641">Dize</span><span class="sxs-lookup"><span data-stu-id="fcfe4-641">String</span></span>|<span data-ttu-id="fcfe4-642">Aramak istediğiniz iş akışı kaynak kimliği.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-642">The resource ID of the workflow that you want to call.</span></span>|  
|<span data-ttu-id="fcfe4-643">ana bilgisayar tetikleyiciadı</span><span class="sxs-lookup"><span data-stu-id="fcfe4-643">host triggerName</span></span>|<span data-ttu-id="fcfe4-644">Evet</span><span class="sxs-lookup"><span data-stu-id="fcfe4-644">Yes</span></span>|<span data-ttu-id="fcfe4-645">Dize</span><span class="sxs-lookup"><span data-stu-id="fcfe4-645">String</span></span>|<span data-ttu-id="fcfe4-646">Çağrılacak istediğiniz Tetikleyici adı.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-646">The name of the trigger that you want to invoke.</span></span>|  
|<span data-ttu-id="fcfe4-647">Sorguları</span><span class="sxs-lookup"><span data-stu-id="fcfe4-647">queries</span></span>|<span data-ttu-id="fcfe4-648">Hayır</span><span class="sxs-lookup"><span data-stu-id="fcfe4-648">No</span></span>|<span data-ttu-id="fcfe4-649">Nesne</span><span class="sxs-lookup"><span data-stu-id="fcfe4-649">Object</span></span>|<span data-ttu-id="fcfe4-650">URL'ye eklemek için sorgu parametreleri temsil eder.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-650">Represents the query parameters to add to the URL.</span></span> <span data-ttu-id="fcfe4-651">Örneğin, `"queries" : { "api-version": "2015-02-01" }` ekler `?api-version=2015-02-01` URL.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-651">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|  
|<span data-ttu-id="fcfe4-652">Üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="fcfe4-652">headers</span></span>|<span data-ttu-id="fcfe4-653">Hayır</span><span class="sxs-lookup"><span data-stu-id="fcfe4-653">No</span></span>|<span data-ttu-id="fcfe4-654">Nesne</span><span class="sxs-lookup"><span data-stu-id="fcfe4-654">Object</span></span>|<span data-ttu-id="fcfe4-655">Her isteği gönderilen üstbilgilerinin temsil eder.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-655">Represents each of the headers that is sent to the request.</span></span> <span data-ttu-id="fcfe4-656">Örneğin, dilini ayarlamak ve bir istek yazmak için şunu yazın:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="fcfe4-656">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="fcfe4-657">Gövde</span><span class="sxs-lookup"><span data-stu-id="fcfe4-657">body</span></span>|<span data-ttu-id="fcfe4-658">Hayır</span><span class="sxs-lookup"><span data-stu-id="fcfe4-658">No</span></span>|<span data-ttu-id="fcfe4-659">Nesne</span><span class="sxs-lookup"><span data-stu-id="fcfe4-659">Object</span></span>|<span data-ttu-id="fcfe4-660">Uç noktasına gönderilen yükünü temsil eder.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-660">Represents the payload sent to the endpoint.</span></span>|  
  
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
  
<span data-ttu-id="fcfe4-661">Bir erişim denetimi akışında yapılan \(daha belirgin olarak tetikleyici\), iş akışı erişmesi gereken anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-661">An access check is made on the workflow \(more specifically, the trigger\), meaning you need access to the workflow.</span></span>  
  
<span data-ttu-id="fcfe4-662">Çıkışlarından `workflow` eylem ne tanımlanan üzerinde dayalı `response` alt iş akışı eylemi.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-662">The outputs from the `workflow` action are based on what you defined in the `response` action in the child workflow.</span></span> <span data-ttu-id="fcfe4-663">Herhangi bir tanımlamadığınız varsa `response` eylemi ve ardından çıkışları boş.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-663">If you have not defined any `response` action, then the outputs are empty.</span></span>  

## <a name="function-action"></a><span data-ttu-id="fcfe4-664">İşlev eylemi</span><span class="sxs-lookup"><span data-stu-id="fcfe4-664">Function action</span></span>   

|<span data-ttu-id="fcfe4-665">Ad</span><span class="sxs-lookup"><span data-stu-id="fcfe4-665">Name</span></span>|<span data-ttu-id="fcfe4-666">Gerekli</span><span class="sxs-lookup"><span data-stu-id="fcfe4-666">Required</span></span>|<span data-ttu-id="fcfe4-667">Tür</span><span class="sxs-lookup"><span data-stu-id="fcfe4-667">Type</span></span>|<span data-ttu-id="fcfe4-668">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fcfe4-668">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="fcfe4-669">İşlev kimliği</span><span class="sxs-lookup"><span data-stu-id="fcfe4-669">function id</span></span>|<span data-ttu-id="fcfe4-670">Evet</span><span class="sxs-lookup"><span data-stu-id="fcfe4-670">Yes</span></span>|<span data-ttu-id="fcfe4-671">Dize</span><span class="sxs-lookup"><span data-stu-id="fcfe4-671">String</span></span>|<span data-ttu-id="fcfe4-672">Çağırmak için istediğiniz işlev kaynak kimliği.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-672">The resource ID of the function that you want to invoke.</span></span>|  
|<span data-ttu-id="fcfe4-673">Yöntemi</span><span class="sxs-lookup"><span data-stu-id="fcfe4-673">method</span></span>|<span data-ttu-id="fcfe4-674">Hayır</span><span class="sxs-lookup"><span data-stu-id="fcfe4-674">No</span></span>|<span data-ttu-id="fcfe4-675">Dize</span><span class="sxs-lookup"><span data-stu-id="fcfe4-675">String</span></span>|<span data-ttu-id="fcfe4-676">İşlevi çağırmak için kullanılan HTTP yöntemi.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-676">The HTTP method used to invoke the function.</span></span> <span data-ttu-id="fcfe4-677">Varsayılan olarak, olmasından `POST` belirtilmemiş olduğunda.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-677">By default, it is `POST` when not specified.</span></span>|  
|<span data-ttu-id="fcfe4-678">Sorguları</span><span class="sxs-lookup"><span data-stu-id="fcfe4-678">queries</span></span>|<span data-ttu-id="fcfe4-679">Hayır</span><span class="sxs-lookup"><span data-stu-id="fcfe4-679">No</span></span>|<span data-ttu-id="fcfe4-680">Nesne</span><span class="sxs-lookup"><span data-stu-id="fcfe4-680">Object</span></span>|<span data-ttu-id="fcfe4-681">URL'ye eklemek için sorgu parametreleri temsil eder.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-681">Represents the query parameters to add to the URL.</span></span> <span data-ttu-id="fcfe4-682">Örneğin, `"queries" : { "api-version": "2015-02-01" }` ekler `?api-version=2015-02-01` URL.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-682">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|  
|<span data-ttu-id="fcfe4-683">Üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="fcfe4-683">headers</span></span>|<span data-ttu-id="fcfe4-684">Hayır</span><span class="sxs-lookup"><span data-stu-id="fcfe4-684">No</span></span>|<span data-ttu-id="fcfe4-685">Nesne</span><span class="sxs-lookup"><span data-stu-id="fcfe4-685">Object</span></span>|<span data-ttu-id="fcfe4-686">Her isteği gönderilen üstbilgilerinin temsil eder.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-686">Represents each of the headers that is sent to the request.</span></span> <span data-ttu-id="fcfe4-687">Örneğin, bir isteği dil ve türünü ayarlamak için: `"headers" : { "Accept-Language": "en-us" }`.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-687">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us" }`.</span></span>|  
|<span data-ttu-id="fcfe4-688">Gövde</span><span class="sxs-lookup"><span data-stu-id="fcfe4-688">body</span></span>|<span data-ttu-id="fcfe4-689">Hayır</span><span class="sxs-lookup"><span data-stu-id="fcfe4-689">No</span></span>|<span data-ttu-id="fcfe4-690">Nesne</span><span class="sxs-lookup"><span data-stu-id="fcfe4-690">Object</span></span>|<span data-ttu-id="fcfe4-691">Uç noktasına gönderilen yükünü temsil eder.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-691">Represents the payload sent to the endpoint.</span></span>|  

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

<span data-ttu-id="fcfe4-692">Mantıksal uygulama kaydettiğinizde, biz başvurulan işlev üzerinde bazı denetimler gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="fcfe4-692">When you save the logic app, we perform some checks on the referenced function:</span></span>
-   <span data-ttu-id="fcfe4-693">İşlev erişiminizin olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-693">You need to have access to the function.</span></span>
-   <span data-ttu-id="fcfe4-694">Yalnızca standart HTTP tetikleyicisi veya genel JSON Web kancası tetikleyici izin verilir.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-694">Only standard HTTP trigger or generic JSON webhook trigger is allowed.</span></span>
-   <span data-ttu-id="fcfe4-695">Tanımlı yol olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-695">It should not have any route defined.</span></span>
-   <span data-ttu-id="fcfe4-696">Yalnızca "işlev" ve "anonim" yetki düzeyini izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-696">Only "function" and "anonymous" authorization level is allowed.</span></span>

<span data-ttu-id="fcfe4-697">Tetikleme URL'si alınan, önbelleğe alınmış ve çalışma zamanında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-697">The trigger URL is retrieved, cached, and used at runtime.</span></span> <span data-ttu-id="fcfe4-698">Herhangi bir işlem önbelleğe alınmış URL'sini geçersiz kılar, dolayısıyla eylemi çalışma zamanında başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-698">So if any operation invalidates the cached URL, the action fails at runtime.</span></span> <span data-ttu-id="fcfe4-699">Bu sorunu çözmek için almak ve tetikleme URL'si tekrar önbelleğe mantıksal uygulama neden olacak mantıksal uygulama yeniden kaydedin.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-699">To work around this, save the logic app again, which will cause logic app to retrieve and cache the trigger URL again.</span></span>

## <a name="collection-actions-scopes-and-loops"></a><span data-ttu-id="fcfe4-700">Koleksiyon eylemleri (kapsamlar ve döngüler)</span><span class="sxs-lookup"><span data-stu-id="fcfe4-700">Collection actions (scopes and loops)</span></span>

<span data-ttu-id="fcfe4-701">Bazı eylem türleri kendilerini içinde eylemler içerebilir.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-701">Some action types can contain actions within themselves.</span></span> <span data-ttu-id="fcfe4-702">Bir koleksiyon içinde başvurusu Eylemler doğrudan dışında koleksiyonu başvurulabilir.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-702">Reference actions within a collection can be referenced directly outside of the collection.</span></span> <span data-ttu-id="fcfe4-703">Tanımladıysanız `http` bir kapsamda `@body('http')` herhangi bir iş akışında hala geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-703">If you defined `http` in a scope, `@body('http')` is still valid anywhere in a workflow.</span></span> <span data-ttu-id="fcfe4-704">Bir koleksiyon içinde eylemler olabilir `runAfter` yalnızca aynı koleksiyondaki diğer eylemler.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-704">Actions within a collection can `runAfter` only other actions within the same collection.</span></span>

## <a name="scope-action"></a><span data-ttu-id="fcfe4-705">Kapsam eylemi</span><span class="sxs-lookup"><span data-stu-id="fcfe4-705">Scope action</span></span>

<span data-ttu-id="fcfe4-706">`scope` Eylem sağlar, mantıksal olarak bir iş akışında Grup eylemler.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-706">The `scope` action lets you logically group actions in a workflow.</span></span>

|<span data-ttu-id="fcfe4-707">Ad</span><span class="sxs-lookup"><span data-stu-id="fcfe4-707">Name</span></span>|<span data-ttu-id="fcfe4-708">Gerekli</span><span class="sxs-lookup"><span data-stu-id="fcfe4-708">Required</span></span>|<span data-ttu-id="fcfe4-709">Tür</span><span class="sxs-lookup"><span data-stu-id="fcfe4-709">Type</span></span>|<span data-ttu-id="fcfe4-710">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fcfe4-710">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="fcfe4-711">Eylemler</span><span class="sxs-lookup"><span data-stu-id="fcfe4-711">actions</span></span>|<span data-ttu-id="fcfe4-712">Evet</span><span class="sxs-lookup"><span data-stu-id="fcfe4-712">Yes</span></span>|<span data-ttu-id="fcfe4-713">Nesne</span><span class="sxs-lookup"><span data-stu-id="fcfe4-713">Object</span></span>|<span data-ttu-id="fcfe4-714">Kapsam içinde yürütmek için iç Eylemler</span><span class="sxs-lookup"><span data-stu-id="fcfe4-714">Inner actions to execute within the scope</span></span>|

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

## <a name="foreach-action"></a><span data-ttu-id="fcfe4-715">ForEach eylemi</span><span class="sxs-lookup"><span data-stu-id="fcfe4-715">ForEach action</span></span>

<span data-ttu-id="fcfe4-716">Bu döngü eylem bir dizisini yineler ve her öğe için iç eylemleri gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-716">This looping action iterates through an array and performs inner actions for each item.</span></span> <span data-ttu-id="fcfe4-717">Varsayılan olarak, (20 yürütmeleri paralel birer birer) paralel foreach döngüsü yürütür.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-717">By default, the foreach loop executes in parallel (20 executions in parallel at a time).</span></span> <span data-ttu-id="fcfe4-718">Yürütme kurallarını kullanarak ayarlayabilirsiniz `operationOptions` parametresi.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-718">You can set execution rules using the `operationOptions` parameter.</span></span>

|<span data-ttu-id="fcfe4-719">Ad</span><span class="sxs-lookup"><span data-stu-id="fcfe4-719">Name</span></span>|<span data-ttu-id="fcfe4-720">Gerekli</span><span class="sxs-lookup"><span data-stu-id="fcfe4-720">Required</span></span>|<span data-ttu-id="fcfe4-721">Tür</span><span class="sxs-lookup"><span data-stu-id="fcfe4-721">Type</span></span>|<span data-ttu-id="fcfe4-722">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fcfe4-722">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="fcfe4-723">Eylemler</span><span class="sxs-lookup"><span data-stu-id="fcfe4-723">actions</span></span>|<span data-ttu-id="fcfe4-724">Evet</span><span class="sxs-lookup"><span data-stu-id="fcfe4-724">Yes</span></span>|<span data-ttu-id="fcfe4-725">Nesne</span><span class="sxs-lookup"><span data-stu-id="fcfe4-725">Object</span></span>|<span data-ttu-id="fcfe4-726">Döngü içinde yürütmek için iç Eylemler</span><span class="sxs-lookup"><span data-stu-id="fcfe4-726">Inner actions to execute within the loop</span></span>|
|<span data-ttu-id="fcfe4-727">foreach</span><span class="sxs-lookup"><span data-stu-id="fcfe4-727">foreach</span></span>|<span data-ttu-id="fcfe4-728">Evet</span><span class="sxs-lookup"><span data-stu-id="fcfe4-728">Yes</span></span>|<span data-ttu-id="fcfe4-729">Dize</span><span class="sxs-lookup"><span data-stu-id="fcfe4-729">string</span></span>|<span data-ttu-id="fcfe4-730">Dizi üzerinden yineleme</span><span class="sxs-lookup"><span data-stu-id="fcfe4-730">The array to iterate over</span></span>|
|<span data-ttu-id="fcfe4-731">operationOptions</span><span class="sxs-lookup"><span data-stu-id="fcfe4-731">operationOptions</span></span>|<span data-ttu-id="fcfe4-732">Yok</span><span class="sxs-lookup"><span data-stu-id="fcfe4-732">no</span></span>|<span data-ttu-id="fcfe4-733">Dize</span><span class="sxs-lookup"><span data-stu-id="fcfe4-733">string</span></span>|<span data-ttu-id="fcfe4-734">İşlemi için herhangi bir seçenek davranışı.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-734">Any operation options for behavior.</span></span> <span data-ttu-id="fcfe4-735">Şu anda yalnızca destekler `sequential` yineleme sırayla yürütmek için (varsayılan davranıştır paralel)</span><span class="sxs-lookup"><span data-stu-id="fcfe4-735">Currently only supports `sequential` to execute iterations sequentially (default behavior is parallel)</span></span>|

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

## <a name="until-action"></a><span data-ttu-id="fcfe4-736">Eylem kadar</span><span class="sxs-lookup"><span data-stu-id="fcfe4-736">Until action</span></span>

<span data-ttu-id="fcfe4-737">Bir koşul true olarak sonuçları kadar bu döngü eylem iç Eylemler yürütür.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-737">This looping action executes inner actions until a condition results to true.</span></span>

|<span data-ttu-id="fcfe4-738">Ad</span><span class="sxs-lookup"><span data-stu-id="fcfe4-738">Name</span></span>|<span data-ttu-id="fcfe4-739">Gerekli</span><span class="sxs-lookup"><span data-stu-id="fcfe4-739">Required</span></span>|<span data-ttu-id="fcfe4-740">Tür</span><span class="sxs-lookup"><span data-stu-id="fcfe4-740">Type</span></span>|<span data-ttu-id="fcfe4-741">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fcfe4-741">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="fcfe4-742">Eylemler</span><span class="sxs-lookup"><span data-stu-id="fcfe4-742">actions</span></span>|<span data-ttu-id="fcfe4-743">Evet</span><span class="sxs-lookup"><span data-stu-id="fcfe4-743">Yes</span></span>|<span data-ttu-id="fcfe4-744">Nesne</span><span class="sxs-lookup"><span data-stu-id="fcfe4-744">Object</span></span>|<span data-ttu-id="fcfe4-745">Döngü içinde yürütmek için iç Eylemler</span><span class="sxs-lookup"><span data-stu-id="fcfe4-745">Inner actions to execute within the loop</span></span>|
|<span data-ttu-id="fcfe4-746">ifade</span><span class="sxs-lookup"><span data-stu-id="fcfe4-746">expression</span></span>|<span data-ttu-id="fcfe4-747">Evet</span><span class="sxs-lookup"><span data-stu-id="fcfe4-747">Yes</span></span>|<span data-ttu-id="fcfe4-748">Dize</span><span class="sxs-lookup"><span data-stu-id="fcfe4-748">string</span></span>|<span data-ttu-id="fcfe4-749">Her yinelemeden sonra değerlendirilecek ifade</span><span class="sxs-lookup"><span data-stu-id="fcfe4-749">The expression to evaluate after each iteration</span></span>|
|<span data-ttu-id="fcfe4-750">Sınırı</span><span class="sxs-lookup"><span data-stu-id="fcfe4-750">limit</span></span>|<span data-ttu-id="fcfe4-751">Evet</span><span class="sxs-lookup"><span data-stu-id="fcfe4-751">yes</span></span>|<span data-ttu-id="fcfe4-752">Nesne</span><span class="sxs-lookup"><span data-stu-id="fcfe4-752">Object</span></span>|<span data-ttu-id="fcfe4-753">Döngü - en az bir sınır sınırlarını tanımlanmış olması gerekir</span><span class="sxs-lookup"><span data-stu-id="fcfe4-753">The limits for the loop - at least one limit must be defined</span></span>|
|<span data-ttu-id="fcfe4-754">Sayısı</span><span class="sxs-lookup"><span data-stu-id="fcfe4-754">count</span></span>|<span data-ttu-id="fcfe4-755">Yok</span><span class="sxs-lookup"><span data-stu-id="fcfe4-755">no</span></span>|<span data-ttu-id="fcfe4-756">Int</span><span class="sxs-lookup"><span data-stu-id="fcfe4-756">int</span></span>|<span data-ttu-id="fcfe4-757">Gerçekleştirilebilir yineleme sayısını sınırla</span><span class="sxs-lookup"><span data-stu-id="fcfe4-757">The limit to the number of iterations that can be performed</span></span>|
|<span data-ttu-id="fcfe4-758">Zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="fcfe4-758">timeout</span></span>|<span data-ttu-id="fcfe4-759">Yok</span><span class="sxs-lookup"><span data-stu-id="fcfe4-759">no</span></span>|<span data-ttu-id="fcfe4-760">Dize</span><span class="sxs-lookup"><span data-stu-id="fcfe4-760">string</span></span>|<span data-ttu-id="fcfe4-761">Ne kadar süreyle döndürmelidir için zaman aşımı.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-761">The timeout for how long it should loop.</span></span>  <span data-ttu-id="fcfe4-762">ISO 8601 biçim</span><span class="sxs-lookup"><span data-stu-id="fcfe4-762">ISO 8601 format</span></span>|


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

## <a name="conditions---if-action"></a><span data-ttu-id="fcfe4-763">-Varsa koşulları eylemi</span><span class="sxs-lookup"><span data-stu-id="fcfe4-763">Conditions - If Action</span></span>

<span data-ttu-id="fcfe4-764">`If` Eylem, bir koşulu değerlendirmek ve olup olmadığını ifade değerlendiren üzerinde dayalı bir dal yürütme sağlar `true`.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-764">The `If` action lets you evaluate a condition and execute a branch based on whether the expression evaluates to `true`.</span></span>

|<span data-ttu-id="fcfe4-765">Ad</span><span class="sxs-lookup"><span data-stu-id="fcfe4-765">Name</span></span>|<span data-ttu-id="fcfe4-766">Gerekli</span><span class="sxs-lookup"><span data-stu-id="fcfe4-766">Required</span></span>|<span data-ttu-id="fcfe4-767">Tür</span><span class="sxs-lookup"><span data-stu-id="fcfe4-767">Type</span></span>|<span data-ttu-id="fcfe4-768">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fcfe4-768">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="fcfe4-769">Eylemler</span><span class="sxs-lookup"><span data-stu-id="fcfe4-769">actions</span></span>|<span data-ttu-id="fcfe4-770">Evet</span><span class="sxs-lookup"><span data-stu-id="fcfe4-770">Yes</span></span>|<span data-ttu-id="fcfe4-771">Nesne</span><span class="sxs-lookup"><span data-stu-id="fcfe4-771">Object</span></span>|<span data-ttu-id="fcfe4-772">İfade olarak değerlendirildiğinde yürütmek için iç Eylemler`true`</span><span class="sxs-lookup"><span data-stu-id="fcfe4-772">Inner actions to execute when expression evaluates to `true`</span></span>|
|<span data-ttu-id="fcfe4-773">ifade</span><span class="sxs-lookup"><span data-stu-id="fcfe4-773">expression</span></span>|<span data-ttu-id="fcfe4-774">Evet</span><span class="sxs-lookup"><span data-stu-id="fcfe4-774">Yes</span></span>|<span data-ttu-id="fcfe4-775">Dize</span><span class="sxs-lookup"><span data-stu-id="fcfe4-775">string</span></span>|<span data-ttu-id="fcfe4-776">Değerlendirilecek ifade</span><span class="sxs-lookup"><span data-stu-id="fcfe4-776">The expression to evaluate</span></span>|
|<span data-ttu-id="fcfe4-777">else</span><span class="sxs-lookup"><span data-stu-id="fcfe4-777">else</span></span>|<span data-ttu-id="fcfe4-778">Yok</span><span class="sxs-lookup"><span data-stu-id="fcfe4-778">no</span></span>|<span data-ttu-id="fcfe4-779">Nesne</span><span class="sxs-lookup"><span data-stu-id="fcfe4-779">Object</span></span>|<span data-ttu-id="fcfe4-780">İfade olarak değerlendirildiğinde yürütmek için iç Eylemler`false`</span><span class="sxs-lookup"><span data-stu-id="fcfe4-780">Inner actions to execute when expression evaluates to `false`</span></span>|
  
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
  
<span data-ttu-id="fcfe4-781">Aşağıdaki tabloda koşullar bir eylemi ifade nasıl kullanabileceğiniz örnekler gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="fcfe4-781">The following table shows examples of how conditions can use expressions in an action:</span></span>  
  
|<span data-ttu-id="fcfe4-782">JSON değeri</span><span class="sxs-lookup"><span data-stu-id="fcfe4-782">JSON value</span></span>|<span data-ttu-id="fcfe4-783">Sonuç</span><span class="sxs-lookup"><span data-stu-id="fcfe4-783">Result</span></span>|  
|--------------|----------|  
|`"expression": "@parameters('hasSpecialAction')"`|<span data-ttu-id="fcfe4-784">True olarak değerlendirecek herhangi bir değer geçirmek bu koşul neden olur.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-784">Any value that would evaluate to true causes this condition to pass.</span></span> <span data-ttu-id="fcfe4-785">Yalnızca Boole ifadeleri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-785">Only Boolean expressions are supported.</span></span> <span data-ttu-id="fcfe4-786">Diğer türleri Boolean değerine dönüştürmek için işlevlerini kullanın `empty`, `equals`.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-786">To convert other types to Boolean, use functions `empty`, `equals`.</span></span>|  
|`"expression": "@greater(actions('act1').output.value, parameters('threshold'))"`|<span data-ttu-id="fcfe4-787">Karşılaştırma işlevleri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-787">Comparison functions are supported.</span></span> <span data-ttu-id="fcfe4-788">Act1 çıktısı eşik değerinden yüksek olduğunda örnek için eylem yalnızca yürütür.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-788">For the example here, the action only executes when the output of act1 is greater than the threshold.</span></span>|  
|`"expression": "@or(greater(actions('act1').output.value, parameters('threshold')), less(actions('act1').output.value, 100))"`|<span data-ttu-id="fcfe4-789">Mantığı işlevleri iç içe geçmiş Boole ifadeleri oluşturmak için de desteklenir.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-789">Logic functions are also supported to create nested Boolean expressions.</span></span> <span data-ttu-id="fcfe4-790">Bu durumda, act1 çıktısını eşiğin üstünde veya altında 100 olduğunda eylemi yürütür.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-790">In this case, the action executes when the output of act1 is above the threshold or below 100.</span></span>|  
|`"expression": "@equals(length(actions('act1').outputs.errors), 0))"`|<span data-ttu-id="fcfe4-791">Dizi işlevleri, bir dizinin tüm öğeleri olup olmadığını denetlemek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-791">You can use array functions to check if an array has any items.</span></span> <span data-ttu-id="fcfe4-792">Bu durumda, hataları dizi boş olduğunda eylemi yürütür.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-792">In this case, the action executes when the errors array is empty.</span></span>| 
|`"expression": "parameters('hasSpecialAction')"`|<span data-ttu-id="fcfe4-793">Hata - geçerli bir @ için gerekli olduğundan koşul koşulları.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-793">Error - not a valid condition because @ is required for conditions.</span></span>|  
  
<span data-ttu-id="fcfe4-794">Bir koşul başarıyla değerlendirilirse koşul olarak işaretlenmiş `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-794">If a condition evaluates successfully, the condition is marked as `Succeeded`.</span></span> <span data-ttu-id="fcfe4-795">Ya da içinde eylemler `actions` veya `else` nesneleri değerlendirmek için `Succeeded` yürütülen ve başarılı oldu, `Failed` yürütülen ve başarısız olduğunda veya `Skipped` zaman o şubedeki yürütülmez.</span><span class="sxs-lookup"><span data-stu-id="fcfe4-795">Actions within either the `actions` or `else` objects evaluate to `Succeeded` when executed and succeeded, `Failed` when executed and failed, or `Skipped` when that branch is not executed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fcfe4-796">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fcfe4-796">Next steps</span></span>

[<span data-ttu-id="fcfe4-797">İş akışı hizmeti REST API'si</span><span class="sxs-lookup"><span data-stu-id="fcfe4-797">Workflow Service REST API</span></span>](https://docs.microsoft.com/rest/api/logic/workflows)
