---
title: "OMS günlük analizi uyarı REST API kullanarak"
description: "Günlük analizi uyarı REST API, bu yer Operations Management Suite (OMS) günlük analizi uyarıları oluşturma ve yönetme olanak sağlar.  Bu makalede, farklı işlemler gerçekleştirmek için API ve çeşitli örnekler ayrıntıları sağlar."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 628ad256-7181-4a0d-9e68-4ed60c0f3f04
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5ce72ffef4394bf3bbe39fa420c4fcaa965ae35c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-alert-rules-in-log-analytics-with-rest-api"></a><span data-ttu-id="1881f-104">Oluşturma ve uyarı kurallarında günlük analizi REST API ile yönetme</span><span class="sxs-lookup"><span data-stu-id="1881f-104">Create and manage alert rules in Log Analytics with REST API</span></span>
<span data-ttu-id="1881f-105">Günlük analizi uyarı REST API, uyarıları Operations Management Suite (OMS) oluşturma ve yönetme olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="1881f-105">The Log Analytics Alert REST API allows you to create and manage alerts in Operations Management Suite (OMS).</span></span>  <span data-ttu-id="1881f-106">Bu makalede, farklı işlemler gerçekleştirmek için API ve çeşitli örnekler ayrıntıları sağlar.</span><span class="sxs-lookup"><span data-stu-id="1881f-106">This article provides details of the API and several examples for performing different operations.</span></span>

<span data-ttu-id="1881f-107">Günlük analizi arama REST API RESTful ve Azure Resource Manager REST API'si erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="1881f-107">The Log Analytics Search REST API is RESTful and can be accessed via the Azure Resource Manager REST API.</span></span> <span data-ttu-id="1881f-108">Bu belgede API kullanarak bir PowerShell komut satırı burada erişilen örnekler bulacaksınız [ARMClient](https://github.com/projectkudu/ARMClient), Azure Kaynak Yöneticisi API'si çağırma basitleştiren bir açık kaynak komut satırı aracı.</span><span class="sxs-lookup"><span data-stu-id="1881f-108">In this document you will find examples where the API is accessed from a PowerShell command line using  [ARMClient](https://github.com/projectkudu/ARMClient), an open source command line tool that simplifies invoking the Azure Resource Manager API.</span></span> <span data-ttu-id="1881f-109">ARMClient ve PowerShell kullanımını günlük analizi arama API erişmek için birçok seçenek biridir.</span><span class="sxs-lookup"><span data-stu-id="1881f-109">The use of ARMClient and PowerShell is one of many options to access the Log Analytics Search API.</span></span> <span data-ttu-id="1881f-110">Bu araçların OMS çalışma alanları çağrı yapmak ve bunların içindeki arama komutları gerçekleştirmek için RESTful Azure Kaynak Yöneticisi API'si kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="1881f-110">With these tools you can utilize the RESTful Azure Resource Manager API to make calls to OMS workspaces and perform search commands within them.</span></span> <span data-ttu-id="1881f-111">Arama sonuçlarını birçok farklı yolla programlı olarak kullanmanıza olanak sağlayan API arama sonuçlarını, JSON biçiminde çıktı.</span><span class="sxs-lookup"><span data-stu-id="1881f-111">The API will output search results to you in JSON format, allowing you to use the search results in many different ways programmatically.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1881f-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="1881f-112">Prerequisites</span></span>
<span data-ttu-id="1881f-113">Şu anda, uyarıları günlük analizi olarak kaydedilmiş bir aramayı ile yalnızca oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="1881f-113">Currently, alerts can only be created with a saved search in Log Analytics.</span></span>  <span data-ttu-id="1881f-114">Başvurabilirsiniz [günlük Search REST API'sini](log-analytics-log-search-api.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="1881f-114">You can refer to the [Log Search REST API](log-analytics-log-search-api.md) for more information.</span></span>

## <a name="schedules"></a><span data-ttu-id="1881f-115">Zamanlamalar</span><span class="sxs-lookup"><span data-stu-id="1881f-115">Schedules</span></span>
<span data-ttu-id="1881f-116">Kaydedilmiş bir aramayı bir veya daha fazla zamanlama olabilir.</span><span class="sxs-lookup"><span data-stu-id="1881f-116">A saved search can have one or more schedules.</span></span> <span data-ttu-id="1881f-117">Ne sıklıkta arama çalıştırma ve ölçütleri belirlenen zaman aralığı olan zamanlamayı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="1881f-117">The schedule defines how often the search is run and the time interval over which the criteria is identified.</span></span>
<span data-ttu-id="1881f-118">Zamanlamaları aşağıdaki tabloda özelliklere sahip.</span><span class="sxs-lookup"><span data-stu-id="1881f-118">Schedules have the properties in the following table.</span></span>

| <span data-ttu-id="1881f-119">Özellik</span><span class="sxs-lookup"><span data-stu-id="1881f-119">Property</span></span> | <span data-ttu-id="1881f-120">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1881f-120">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1881f-121">aralığı</span><span class="sxs-lookup"><span data-stu-id="1881f-121">Interval</span></span> |<span data-ttu-id="1881f-122">Arama ne sıklıkta çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="1881f-122">How often the search is run.</span></span> <span data-ttu-id="1881f-123">Dakika cinsinden ölçülür.</span><span class="sxs-lookup"><span data-stu-id="1881f-123">Measured in minutes.</span></span> |
| <span data-ttu-id="1881f-124">QueryTimeSpan</span><span class="sxs-lookup"><span data-stu-id="1881f-124">QueryTimeSpan</span></span> |<span data-ttu-id="1881f-125">Ölçüt değerlendirildiği zaman aralığı.</span><span class="sxs-lookup"><span data-stu-id="1881f-125">The time interval over which the criteria is evaluated.</span></span> <span data-ttu-id="1881f-126">Aralıktan büyük veya eşit olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1881f-126">Must be equal to or greater than Interval.</span></span> <span data-ttu-id="1881f-127">Dakika cinsinden ölçülür.</span><span class="sxs-lookup"><span data-stu-id="1881f-127">Measured in minutes.</span></span> |
| <span data-ttu-id="1881f-128">Sürüm</span><span class="sxs-lookup"><span data-stu-id="1881f-128">Version</span></span> |<span data-ttu-id="1881f-129">Kullanılan API sürümü.</span><span class="sxs-lookup"><span data-stu-id="1881f-129">The API version being used.</span></span>  <span data-ttu-id="1881f-130">Şu anda, bu her zaman 1 olarak ayarlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1881f-130">Currently, this should always be set to 1.</span></span> |

<span data-ttu-id="1881f-131">Örneğin, bir olay sorgusu bir aralığı 15 dakika ve 30 dakikalık bir zaman aralığı ile göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="1881f-131">For example, consider an event query with an Interval of 15 minutes and a Timespan of 30 minutes.</span></span> <span data-ttu-id="1881f-132">Bu durumda, sorgu 15 dakikada bir çalışır ve ölçütlerini gerçek üzerinden çözümlemek etseydi uyarı tetikleyen 30 dakikalık aralık.</span><span class="sxs-lookup"><span data-stu-id="1881f-132">In this case, the query would be run every 15 minutes, and an alert would be triggered if the criteria continued to resolve to true over a 30 minute span.</span></span>

### <a name="retrieving-schedules"></a><span data-ttu-id="1881f-133">Zamanlamalar alınıyor</span><span class="sxs-lookup"><span data-stu-id="1881f-133">Retrieving schedules</span></span>
<span data-ttu-id="1881f-134">Kayıtlı bir aramaya tüm zamanlamalar almak için Get yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="1881f-134">Use the Get method to retrieve all schedules for a saved search.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules?api-version=2015-03-20

<span data-ttu-id="1881f-135">Get yöntemi bir zamanlama Kimliğiyle kaydedilmiş bir aramayı için belirli bir zamanlama almak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="1881f-135">Use the Get method with a schedule ID to retrieve a particular schedule for a saved search.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20

<span data-ttu-id="1881f-136">Bir zamanlama için bir örnek yanıt aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="1881f-136">Following is a sample response for a schedule.</span></span>

```json
{
    "value": [{
        "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/MyWorkspace/savedSearches/0f0f4853-17f8-4ed1-9a03-8e888b0d16ec/schedules/a17b53ef-bd70-4ca4-9ead-83b00f2024a8",
        "etag": "W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\"",
        "properties": {
            "Interval": 15,
            "QueryTimeSpan": 15
        }
    }]
}
```

### <a name="creating-a-schedule"></a><span data-ttu-id="1881f-137">Bir zamanlama oluşturma</span><span class="sxs-lookup"><span data-stu-id="1881f-137">Creating a schedule</span></span>
<span data-ttu-id="1881f-138">Put yöntemini benzersiz zamanlama Kimliğine sahip yeni bir zamanlama oluşturmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="1881f-138">Use the Put method with a unique schedule ID to create a new schedule.</span></span>  <span data-ttu-id="1881f-139">Farklı ile ilişkili olsalar bile, iki zamanlamaları aynı Kimliğe sahip olamaz, kayıtlı aramalar unutmayın.</span><span class="sxs-lookup"><span data-stu-id="1881f-139">Note that two schedules cannot have the same ID even if they are associated with different saved searches.</span></span>  <span data-ttu-id="1881f-140">OMS konsolunda bir zamanlama oluşturmak, bir GUID zamanlama kimliği için oluşturulur</span><span class="sxs-lookup"><span data-stu-id="1881f-140">When you create a schedule in the OMS console, a GUID is created for the schedule ID.</span></span>

> [!NOTE]
> <span data-ttu-id="1881f-141">Tüm kayıtlı aramaları, çizelgeler ve günlük analizi API ile oluşturulan eylemler için ad, küçük olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1881f-141">The name for all saved searches, schedules, and actions created with the Log Analytics API must be in lowercase.</span></span>

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson

### <a name="editing-a-schedule"></a><span data-ttu-id="1881f-142">Bir zamanlama düzenleme</span><span class="sxs-lookup"><span data-stu-id="1881f-142">Editing a schedule</span></span>
<span data-ttu-id="1881f-143">Bu zamanlamayı değiştirmek için aynı kayıtlı arama için bir zamanlama kimlikli Put yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="1881f-143">Use the Put method with an existing schedule ID for the same saved search to modify that schedule.</span></span>  <span data-ttu-id="1881f-144">İstek gövdesini zamanlama etag eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1881f-144">The body of the request must include the etag of the schedule.</span></span>

      $scheduleJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\""','properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
      armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson


### <a name="deleting-schedules"></a><span data-ttu-id="1881f-145">Zamanlamalar silme</span><span class="sxs-lookup"><span data-stu-id="1881f-145">Deleting schedules</span></span>
<span data-ttu-id="1881f-146">Delete yöntemi bir zamanlama Kimliğine sahip bir zamanlama silmek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="1881f-146">Use the Delete method with a schedule ID to delete a schedule.</span></span>

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20


## <a name="actions"></a><span data-ttu-id="1881f-147">Eylemler</span><span class="sxs-lookup"><span data-stu-id="1881f-147">Actions</span></span>
<span data-ttu-id="1881f-148">Bir zamanlama birden çok eylemler olabilir.</span><span class="sxs-lookup"><span data-stu-id="1881f-148">A schedule can have multiple actions.</span></span> <span data-ttu-id="1881f-149">Bir posta gönderme veya bir runbook'u başlatma gibi gerçekleştirmek için bir veya daha fazla işlem bir eylem tanımlayabilir veya ne zaman bir arama sonuçlarını bazı ölçütlere uyan belirleyen bir eşik tanımlayabilir.</span><span class="sxs-lookup"><span data-stu-id="1881f-149">An action may define one or more processes to perform such as sending a mail or starting a runbook, or it may define a threshold that determines when the results of a search match some criteria.</span></span>  <span data-ttu-id="1881f-150">Böylece eşiğine ulaşıldığında işlemleri gerçekleştirilen bazı eylemler her ikisi de tanımlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="1881f-150">Some actions will define both so that the processes are performed when the threshold is met.</span></span>

<span data-ttu-id="1881f-151">Tüm eylemler aşağıdaki tabloda özelliklere sahip.</span><span class="sxs-lookup"><span data-stu-id="1881f-151">All actions have the properties in the following table.</span></span>  <span data-ttu-id="1881f-152">Farklı türde bir uyarı aşağıda açıklanan farklı ek özellikler vardır.</span><span class="sxs-lookup"><span data-stu-id="1881f-152">Different types of alerts have different additional properties which are described below.</span></span>

| <span data-ttu-id="1881f-153">Özellik</span><span class="sxs-lookup"><span data-stu-id="1881f-153">Property</span></span> | <span data-ttu-id="1881f-154">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1881f-154">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1881f-155">Tür</span><span class="sxs-lookup"><span data-stu-id="1881f-155">Type</span></span> |<span data-ttu-id="1881f-156">Eylem türü.</span><span class="sxs-lookup"><span data-stu-id="1881f-156">Type of the action.</span></span>  <span data-ttu-id="1881f-157">Şu anda olası uyarı ve Web kancası değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="1881f-157">Currently the possible values are Alert and Webhook.</span></span> |
| <span data-ttu-id="1881f-158">Ad</span><span class="sxs-lookup"><span data-stu-id="1881f-158">Name</span></span> |<span data-ttu-id="1881f-159">Uyarı görünen adı.</span><span class="sxs-lookup"><span data-stu-id="1881f-159">Display name for the alert.</span></span> |
| <span data-ttu-id="1881f-160">Sürüm</span><span class="sxs-lookup"><span data-stu-id="1881f-160">Version</span></span> |<span data-ttu-id="1881f-161">Kullanılan API sürümü.</span><span class="sxs-lookup"><span data-stu-id="1881f-161">The API version being used.</span></span>  <span data-ttu-id="1881f-162">Şu anda, bu her zaman 1 olarak ayarlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1881f-162">Currently, this should always be set to 1.</span></span> |

### <a name="retrieving-actions"></a><span data-ttu-id="1881f-163">Eylemler Alınıyor</span><span class="sxs-lookup"><span data-stu-id="1881f-163">Retrieving actions</span></span>
<span data-ttu-id="1881f-164">Tüm eylemler için bir zamanlama almak için Get yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="1881f-164">Use the Get method to retrieve all actions for a schedule.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules/{Schedule ID}/actions?api-version=2015-03-20

<span data-ttu-id="1881f-165">Get yöntemini eylem Kimliğine sahip bir zamanlama için belirli bir eylem almak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="1881f-165">Use the Get method with the action ID to retrieve a particular action for a schedule.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/actions/{Action ID}?api-version=2015-03-20

### <a name="creating-or-editing-actions"></a><span data-ttu-id="1881f-166">Oluşturma veya Eylemler düzenleme</span><span class="sxs-lookup"><span data-stu-id="1881f-166">Creating or editing actions</span></span>
<span data-ttu-id="1881f-167">Yeni bir eylem oluşturmak için zamanlama için benzersiz olan bir eylem kimliği ile Put yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="1881f-167">Use the Put method with an action ID that is unique to the schedule to create a new action.</span></span>  <span data-ttu-id="1881f-168">OMS konsolunda bir eylem oluşturduğunuzda, bir GUID için eylem kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="1881f-168">When you create an action in the OMS console, a GUID is for the action ID.</span></span>

> [!NOTE]
> <span data-ttu-id="1881f-169">Tüm kayıtlı aramaları, çizelgeler ve günlük analizi API ile oluşturulan eylemler için ad, küçük olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1881f-169">The name for all saved searches, schedules, and actions created with the Log Analytics API must be in lowercase.</span></span>

<span data-ttu-id="1881f-170">Bu zamanlamayı değiştirmek için aynı kayıtlı arama için bir eylem kimliğiyle Put yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="1881f-170">Use the Put method with an existing action ID for the same saved search to modify that schedule.</span></span>  <span data-ttu-id="1881f-171">İstek gövdesini zamanlama etag eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1881f-171">The body of the request must include the etag of the schedule.</span></span>

<span data-ttu-id="1881f-172">Aşağıdaki bölümlerde bu örnekler verilmiştir için yeni bir eylem oluşturmak için istek biçimi eylem türüne göre değişir.</span><span class="sxs-lookup"><span data-stu-id="1881f-172">The request format for creating a new action varies by action type so these examples are provided in the sections below.</span></span>

### <a name="deleting-actions"></a><span data-ttu-id="1881f-173">Eylemler siliniyor</span><span class="sxs-lookup"><span data-stu-id="1881f-173">Deleting actions</span></span>
<span data-ttu-id="1881f-174">Delete yöntemi eylem Kimlikli bir eylem silmek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="1881f-174">Use the Delete method with the action ID to delete an action.</span></span>

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/Actions/{Action ID}?api-version=2015-03-20

### <a name="alert-actions"></a><span data-ttu-id="1881f-175">Uyarı eylemleri</span><span class="sxs-lookup"><span data-stu-id="1881f-175">Alert Actions</span></span>
<span data-ttu-id="1881f-176">Bir zamanlama tek bir uyarı eylemi olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1881f-176">A Schedule should have one and only one Alert action.</span></span>  <span data-ttu-id="1881f-177">Uyarı eylemleri bir veya daha fazla aşağıdaki tabloda bölümler var.</span><span class="sxs-lookup"><span data-stu-id="1881f-177">Alert actions have one or more of the sections in the following table.</span></span>  <span data-ttu-id="1881f-178">Her daha aşağıda ayrıntılı olarak açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="1881f-178">Each is described in further detail below.</span></span>

| <span data-ttu-id="1881f-179">Bölüm</span><span class="sxs-lookup"><span data-stu-id="1881f-179">Section</span></span> | <span data-ttu-id="1881f-180">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1881f-180">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1881f-181">Eşik</span><span class="sxs-lookup"><span data-stu-id="1881f-181">Threshold</span></span> |<span data-ttu-id="1881f-182">Eylem çalıştırıldığında ölçütlerini.</span><span class="sxs-lookup"><span data-stu-id="1881f-182">Criteria for when the action is run.</span></span> |
| <span data-ttu-id="1881f-183">EmailNotification</span><span class="sxs-lookup"><span data-stu-id="1881f-183">EmailNotification</span></span> |<span data-ttu-id="1881f-184">Birden çok alıcıya posta gönderin.</span><span class="sxs-lookup"><span data-stu-id="1881f-184">Send mail to multiple recipients.</span></span> |
| <span data-ttu-id="1881f-185">Düzeltme</span><span class="sxs-lookup"><span data-stu-id="1881f-185">Remediation</span></span> |<span data-ttu-id="1881f-186">Bir runbook tanımlanan sorunu düzeltmeyi denemek için Azure Otomasyonu'nda başlatın.</span><span class="sxs-lookup"><span data-stu-id="1881f-186">Start a runbook in Azure Automation to attempt to correct identified issue.</span></span> |

#### <a name="thresholds"></a><span data-ttu-id="1881f-187">Eşikleri</span><span class="sxs-lookup"><span data-stu-id="1881f-187">Thresholds</span></span>
<span data-ttu-id="1881f-188">Bir uyarı eylem tek bir eşik olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1881f-188">An Alert action should have one and only one threshold.</span></span>  <span data-ttu-id="1881f-189">Kayıtlı arama sonuçlarını arama ile ilişkili bir eylem Eşikte eşleştiğinde, başka bir işlem bu uygulamada çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="1881f-189">When the results of a saved search match the threshold in an action associated with that search, then any other processes in that action are run.</span></span>  <span data-ttu-id="1881f-190">Böylece eşikleri içermeyen diğer türleri Eylemler ile kullanılan bir eylem yalnızca bir eşik de içerebilir.</span><span class="sxs-lookup"><span data-stu-id="1881f-190">An action can also contain only a threshold so that it can be used with actions of other types that don’t contain thresholds.</span></span>

<span data-ttu-id="1881f-191">Eşikleri aşağıdaki tabloda özelliklere sahip.</span><span class="sxs-lookup"><span data-stu-id="1881f-191">Thresholds have the properties in the following table.</span></span>

| <span data-ttu-id="1881f-192">Özellik</span><span class="sxs-lookup"><span data-stu-id="1881f-192">Property</span></span> | <span data-ttu-id="1881f-193">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1881f-193">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1881f-194">işleci</span><span class="sxs-lookup"><span data-stu-id="1881f-194">Operator</span></span> |<span data-ttu-id="1881f-195">Eşik karşılaştırma işleci.</span><span class="sxs-lookup"><span data-stu-id="1881f-195">Operator for the threshold comparison.</span></span> <br> <span data-ttu-id="1881f-196">gt şundan =</span><span class="sxs-lookup"><span data-stu-id="1881f-196">gt = Greater Than</span></span> <br> <span data-ttu-id="1881f-197">lt = küçüktür</span><span class="sxs-lookup"><span data-stu-id="1881f-197">lt = Less Than</span></span> |
| <span data-ttu-id="1881f-198">Değer</span><span class="sxs-lookup"><span data-stu-id="1881f-198">Value</span></span> |<span data-ttu-id="1881f-199">Eşik değeri.</span><span class="sxs-lookup"><span data-stu-id="1881f-199">Value for the threshold.</span></span> |

<span data-ttu-id="1881f-200">Örneğin, bir olay sorgusu zaman aralığı 15 dakika, 30 dakikalık bir Timespan ve 10'dan büyük bir eşik ile göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="1881f-200">For example, consider an event query with an Interval of 15 minutes, a Timespan of 30 minutes, and a Threshold of greater than 10.</span></span> <span data-ttu-id="1881f-201">Bu durumda, sorgu 15 dakikada bir çalışır ve 30 dakikalık aralık oluşturulan 10 olayları döndürülen bir uyarı tetikleyen.</span><span class="sxs-lookup"><span data-stu-id="1881f-201">In this case, the query would be run every 15 minutes, and an alert would be triggered if it returned 10 events that were created over a 30 minute span.</span></span>

<span data-ttu-id="1881f-202">Aşağıdaki örnek yanıt için bir eylem yalnızca bir eşik ile ' dir.</span><span class="sxs-lookup"><span data-stu-id="1881f-202">Following is a sample response for an action with only a threshold.</span></span>  

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My threshold action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "Version": 1
    }

<span data-ttu-id="1881f-203">Put yöntemini benzersiz eylem kimliği ile yeni bir eşik eylemi için bir zamanlama oluşturmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="1881f-203">Use the Put method with a unique action ID to create a new threshold action for a schedule.</span></span>  

    $thresholdJson = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

<span data-ttu-id="1881f-204">Put yöntemini var olan bir eylem kimliği ile bir zamanlama için bir eşik eylemi değiştirmek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="1881f-204">Use the Put method with an existing action ID to modify a threshold action for a schedule.</span></span>  <span data-ttu-id="1881f-205">İstek gövdesini eylemin etag eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1881f-205">The body of the request must include the etag of the action.</span></span>

    $thresholdJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

#### <a name="email-notification"></a><span data-ttu-id="1881f-206">E-posta bildirimi</span><span class="sxs-lookup"><span data-stu-id="1881f-206">Email Notification</span></span>
<span data-ttu-id="1881f-207">E-posta bildirimleri bir veya daha fazla alıcıya posta gönderin.</span><span class="sxs-lookup"><span data-stu-id="1881f-207">Email Notifications send mail to one or more recipients.</span></span>  <span data-ttu-id="1881f-208">Aşağıdaki tabloda özellikleri içerirler.</span><span class="sxs-lookup"><span data-stu-id="1881f-208">They include the properties in the following table.</span></span>

| <span data-ttu-id="1881f-209">Özellik</span><span class="sxs-lookup"><span data-stu-id="1881f-209">Property</span></span> | <span data-ttu-id="1881f-210">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1881f-210">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1881f-211">Alıcıları</span><span class="sxs-lookup"><span data-stu-id="1881f-211">Recipients</span></span> |<span data-ttu-id="1881f-212">Posta adresleri listesi.</span><span class="sxs-lookup"><span data-stu-id="1881f-212">List of mail addresses.</span></span> |
| <span data-ttu-id="1881f-213">Konu</span><span class="sxs-lookup"><span data-stu-id="1881f-213">Subject</span></span> |<span data-ttu-id="1881f-214">Posta konusu.</span><span class="sxs-lookup"><span data-stu-id="1881f-214">The subject of the mail.</span></span> |
| <span data-ttu-id="1881f-215">Eki</span><span class="sxs-lookup"><span data-stu-id="1881f-215">Attachment</span></span> |<span data-ttu-id="1881f-216">Bu her zaman "Hiçbiri" değerine sahip şekilde ekleri şu anda, desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="1881f-216">Attachments are not currently supported, so this will always have a value of “None”.</span></span> |

<span data-ttu-id="1881f-217">Aşağıdaki örnek yanıt bir eşik ile bir e-posta bildirim eylemi için ' dir.</span><span class="sxs-lookup"><span data-stu-id="1881f-217">Following is a sample response for an email notification action with a threshold.</span></span>  

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My email action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "EmailNotification": {
            "Recipients": [
                "recipient1@contoso.com",
                "recipient2@contoso.com"
            ],
            "Subject": "This is the subject",
            "Attachment": "None"
        },
        "Version": 1
    }

<span data-ttu-id="1881f-218">Put yöntemini benzersiz eylem kimliği ile yeni bir e-posta eylemi için bir zamanlama oluşturmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="1881f-218">Use the Put method with a unique action ID to create a new e-mail action for a schedule.</span></span>  <span data-ttu-id="1881f-219">Aşağıdaki örnek, bir e-posta bildirimi bir eşik ile oluşturur, bu nedenle kayıtlı arama sonuçlarını eşiği aştığında posta gönderilir.</span><span class="sxs-lookup"><span data-stu-id="1881f-219">The following example creates an email notification with a threshold so the mail is sent when the results of the saved search exceed the threshold.</span></span>

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is the subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

<span data-ttu-id="1881f-220">Put yöntemini var olan bir eylem kimliği ile bir zamanlama için bir e-posta eylemi değiştirmek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="1881f-220">Use the Put method with an existing action ID to modify an e-mail action for a schedule.</span></span>  <span data-ttu-id="1881f-221">İstek gövdesini eylemin etag eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1881f-221">The body of the request must include the etag of the action.</span></span>

    $emailJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is the subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

#### <a name="remediation-actions"></a><span data-ttu-id="1881f-222">Düzeltme eylemleri</span><span class="sxs-lookup"><span data-stu-id="1881f-222">Remediation actions</span></span>
<span data-ttu-id="1881f-223">Düzeltmeler, Azure automation'da uyarı tarafından tanımlanan sorunu düzeltmeye çalışır bir runbook başlatın.</span><span class="sxs-lookup"><span data-stu-id="1881f-223">Remediations start a runbook in Azure Automation that attempts to correct the problem identified by the alert.</span></span>  <span data-ttu-id="1881f-224">Bir düzeltme eylemi kullanılan runbook için bir Web kancası oluşturun ve ardından URI WebhookUri özelliğinde belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1881f-224">You must create a webhook for the runbook used in a remediation action and then specify the URI in the WebhookUri property.</span></span>  <span data-ttu-id="1881f-225">OMS konsolunu kullanarak bu eylemi oluşturduğunuzda, yeni bir Web kancası runbook için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="1881f-225">When you create this action using the OMS console, a new webhook is automatically created for the runbook.</span></span>

<span data-ttu-id="1881f-226">Düzeltmeler aşağıdaki tabloda özellikleri içerir.</span><span class="sxs-lookup"><span data-stu-id="1881f-226">Remediations include the properties in the following table.</span></span>

| <span data-ttu-id="1881f-227">Özellik</span><span class="sxs-lookup"><span data-stu-id="1881f-227">Property</span></span> | <span data-ttu-id="1881f-228">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1881f-228">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1881f-229">RunbookName</span><span class="sxs-lookup"><span data-stu-id="1881f-229">RunbookName</span></span> |<span data-ttu-id="1881f-230">Runbook'un adı.</span><span class="sxs-lookup"><span data-stu-id="1881f-230">Name of the runbook.</span></span> <span data-ttu-id="1881f-231">Bu OMS çalışma alanınızdaki Otomasyon çözümünü yapılandırılan Otomasyon hesabı yayımlanan bir runbook'ta eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="1881f-231">This must match a published runbook in the automation account configured in the Automation Solution in your OMS workspace.</span></span> |
| <span data-ttu-id="1881f-232">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="1881f-232">WebhookUri</span></span> |<span data-ttu-id="1881f-233">Web kancası URI'si.</span><span class="sxs-lookup"><span data-stu-id="1881f-233">URI of the webhook.</span></span> |
| <span data-ttu-id="1881f-234">Süre sonu</span><span class="sxs-lookup"><span data-stu-id="1881f-234">Expiry</span></span> |<span data-ttu-id="1881f-235">Sona erme tarihi ve saati Web kancası.</span><span class="sxs-lookup"><span data-stu-id="1881f-235">The expiration date and time of the webhook.</span></span>  <span data-ttu-id="1881f-236">Web kancası bir sona erme yoksa, bu geçerli bir gelecek tarih olabilir.</span><span class="sxs-lookup"><span data-stu-id="1881f-236">If the webhook doesn’t have an expiration, then this can be any valid future date.</span></span> |

<span data-ttu-id="1881f-237">Aşağıdaki örnek yanıt bir eşik ile bir düzeltme eylemi için ' dir.</span><span class="sxs-lookup"><span data-stu-id="1881f-237">Following is a sample response for a remediation action with a threshold.</span></span>

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My remediation action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "Remediation": {
            "RunbookName": "My-Runbook",
            "WebhookUri": "https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d",
            "Expiry": "2018-02-25T18:27:20"
            },
        "Version": 1
    }

<span data-ttu-id="1881f-238">Put yöntemini benzersiz eylem kimliği ile yeni bir düzeltme eylemi için bir zamanlama oluşturmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="1881f-238">Use the Put method with a unique action ID to create a new remediation action for a schedule.</span></span>  <span data-ttu-id="1881f-239">Aşağıdaki örnek, bir düzeltme bir eşik ile oluşturur, bu nedenle kayıtlı arama sonuçlarını eşiği aştığında runbook başlatıldıktan.</span><span class="sxs-lookup"><span data-stu-id="1881f-239">The following example creates a remediation with a threshold so the runbook is started when the results of the saved search exceed the threshold.</span></span>

    $remediateJson = "{'properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

<span data-ttu-id="1881f-240">Put yöntemini var olan bir eylem kimliği ile bir zamanlama için bir düzeltme eylemi değiştirmek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="1881f-240">Use the Put method with an existing action ID to modify a remediation action for a schedule.</span></span>  <span data-ttu-id="1881f-241">İstek gövdesini eylemin etag eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1881f-241">The body of the request must include the etag of the action.</span></span>

    $remediateJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

#### <a name="example"></a><span data-ttu-id="1881f-242">Örnek</span><span class="sxs-lookup"><span data-stu-id="1881f-242">Example</span></span>
<span data-ttu-id="1881f-243">Yeni bir e-posta Uyarı oluşturmak için tam bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="1881f-243">Following is a complete example to create a new email alert.</span></span>  <span data-ttu-id="1881f-244">Bu eşik ve e-posta içeren bir eylem birlikte yeni bir zamanlama oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1881f-244">This creates a new schedule along with an action containing a threshold and email.</span></span>

    $subscriptionId = "3d56705e-5b26-5bcc-9368-dbc8d2fafbfc"
    $resourceGroup  = "MyResourceGroup"    
    $workspaceName    = "MyWorkspace"
    $searchId       = "MySearch"
    $scheduleId     = "MySchedule"
    $thresholdId    = "MyThreshold"
    $actionId       = "MyEmailAction"

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/?api-version=2015-03-20 $scheduleJson

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Severity':'Warning', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is the subject', 'Attachment':'None'} }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/actions/$actionId/?api-version=2015-03-20 $emailJson

### <a name="webhook-actions"></a><span data-ttu-id="1881f-245">Web kancası eylemleri</span><span class="sxs-lookup"><span data-stu-id="1881f-245">Webhook actions</span></span>
<span data-ttu-id="1881f-246">Web kancası eylemleri, bir URL çağırma ve isteğe bağlı olarak gönderilecek bir yükü sağlayarak bir işlem başlatın.</span><span class="sxs-lookup"><span data-stu-id="1881f-246">Webhook actions start a process by calling a URL and optionally providing a payload to be sent.</span></span>  <span data-ttu-id="1881f-247">Azure Otomasyon çalışma kitabı dışındaki işlemler çağırabilir Web kancası için amacı dışında düzeltme eylemleri benzerdir.</span><span class="sxs-lookup"><span data-stu-id="1881f-247">They are similar to Remediation actions except they are meant for webhooks that may invoke processes other than Azure Automation runbooks.</span></span>  <span data-ttu-id="1881f-248">Uzak işlem teslim edilecek bir yükü sağlama ek seçeneği de sağlar.</span><span class="sxs-lookup"><span data-stu-id="1881f-248">They also provide the additional option of providing a payload to be delivered to the remote process.</span></span>

<span data-ttu-id="1881f-249">Web kancası eylemleri bir eşik gerekmez ancak bunun yerine bir uyarı eylem bir eşik ile sahip bir zamanlama eklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="1881f-249">Webhook actions do not have a threshold but instead should be added to a schedule that has an Alert action with a threshold.</span></span>  <span data-ttu-id="1881f-250">Eşiğine ulaşıldığında, tüm çalışan birden çok Web kancası eylemleri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1881f-250">You can add multiple Webhook actions that will all be run when the threshold is met.</span></span>

<span data-ttu-id="1881f-251">Web kancası eylemleri aşağıdaki tabloda özellikleri içerir.</span><span class="sxs-lookup"><span data-stu-id="1881f-251">Webhook actions include the properties in the following table.</span></span>

| <span data-ttu-id="1881f-252">Özellik</span><span class="sxs-lookup"><span data-stu-id="1881f-252">Property</span></span> | <span data-ttu-id="1881f-253">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1881f-253">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1881f-254">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="1881f-254">WebhookUri</span></span> |<span data-ttu-id="1881f-255">Posta konusu.</span><span class="sxs-lookup"><span data-stu-id="1881f-255">The subject of the mail.</span></span> |
| <span data-ttu-id="1881f-256">CustomPayload</span><span class="sxs-lookup"><span data-stu-id="1881f-256">CustomPayload</span></span> |<span data-ttu-id="1881f-257">Web kancası için gönderilecek özel yükü.</span><span class="sxs-lookup"><span data-stu-id="1881f-257">Custom payload to be sent to the webhook.</span></span>  <span data-ttu-id="1881f-258">Web kancası bekleniyor üzerinde biçimi bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="1881f-258">The format will depend on what the webhook is expecting.</span></span> |

<span data-ttu-id="1881f-259">Web kancası eylem ve bir eşik ile ilişkili bir uyarı eylem için örnek yanıt aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="1881f-259">Following is a sample response for webhook action and an associated alert action with a threshold.</span></span>

    {
        "__metadata": {},
        "value": [
            {
                "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/bwren/savedSearches/2d1b30fb-7f48-4de5-9614-79ee244b52de/schedules/b80f5621-7217-4007-b32d-165d14377093/Actions/72884702-acf9-4653-bb67-f42436b342b4",
                "etag": "W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"",
                "properties": {
                    "Type": "Webhook",
                    "Name": "My Webhook Action",
                    "WebhookUri": "https://oaaswebhookdf.cloudapp.net/webhooks?token=VfkYTIlpk%2fc%2bJBP",
                    "CustomPayload": "{\"fielld1\":\"value1\",\"field2\":\"value2\"}",
                    "Version": 1
                }
            },
            {
                "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/bwren/savedSearches/2d1b30fb-7f48-4de5-9614-79ee244b52de/schedules/b80f5621-7217-4007-b32d-165d14377093/Actions/90a27cf8-71b7-4df2-b04f-54ed01f1e4b6",
                "etag": "W/\"datetime'2016-02-26T20%3A25%3A00.565204Z'\"",
                "properties": {
                    "Type": "Alert",
                    "Name": "Threshold for my webhook action",
                    "Threshold": {
                        "Operator": "gt",
                        "Value": 10
                    },
                    "Version": 1
                }
            }
        ]
    }

#### <a name="create-or-edit-a-webhook-action"></a><span data-ttu-id="1881f-260">Oluşturma veya bir Web kancası eylemi düzenleme</span><span class="sxs-lookup"><span data-stu-id="1881f-260">Create or edit a webhook action</span></span>
<span data-ttu-id="1881f-261">Put yöntemini benzersiz eylem kimliği ile yeni bir Web kancası eylemi için bir zamanlama oluşturmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="1881f-261">Use the Put method with a unique action ID to create a new webhook action for a schedule.</span></span>  <span data-ttu-id="1881f-262">Kayıtlı arama sonuçlarını eşiği aştığında Web kancası tetiklenen amacıyla aşağıdaki örnek bir Web kancası eylemi ve bir uyarı eylem bir eşik ile oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1881f-262">The following example creates a Webhook action and an Alert action with a threshold so that the webhook will be triggered when the results of the saved search exceed the threshold.</span></span>

    $thresholdAction = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdAction

    $webhookAction = "{'properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

<span data-ttu-id="1881f-263">Put yöntemini var olan bir eylem kimliği ile bir zamanlama için bir Web kancası eylemi değiştirmek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="1881f-263">Use the Put method with an existing action ID to modify a webhook action for a schedule.</span></span>  <span data-ttu-id="1881f-264">İstek gövdesini eylemin etag eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1881f-264">The body of the request must include the etag of the action.</span></span>

    $webhookAction = "{'etag': 'W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"','properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

## <a name="next-steps"></a><span data-ttu-id="1881f-265">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1881f-265">Next steps</span></span>
* <span data-ttu-id="1881f-266">Kullanım [günlük aramalar gerçekleştirmek için REST API](log-analytics-log-search-api.md) günlük analizi içinde.</span><span class="sxs-lookup"><span data-stu-id="1881f-266">Use the [REST API to perform log searches](log-analytics-log-search-api.md) in Log Analytics.</span></span>

