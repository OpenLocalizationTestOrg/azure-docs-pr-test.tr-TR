---
title: "aaaUsing OMS günlük analizi uyarı REST API'si"
description: "Merhaba günlük analizi uyarı REST API toocreate sağlar ve bu yer Operations Management Suite (OMS) günlük analizi uyarıları yönetin.  Bu makalede, farklı işlemler gerçekleştirmek için hello API ve çeşitli örnekler ayrıntıları sağlar."
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
ms.openlocfilehash: 418dc7eb71d6151c6380b8925f1f147a0e13b178
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-alert-rules-in-log-analytics-with-rest-api"></a><span data-ttu-id="4e0dc-104">Oluşturma ve uyarı kurallarında günlük analizi REST API ile yönetme</span><span class="sxs-lookup"><span data-stu-id="4e0dc-104">Create and manage alert rules in Log Analytics with REST API</span></span>
<span data-ttu-id="4e0dc-105">Merhaba günlük analizi uyarı REST API toocreate sağlar ve Uyarıları Operations Management Suite (OMS) yönetme.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-105">hello Log Analytics Alert REST API allows you toocreate and manage alerts in Operations Management Suite (OMS).</span></span>  <span data-ttu-id="4e0dc-106">Bu makalede, farklı işlemler gerçekleştirmek için hello API ve çeşitli örnekler ayrıntıları sağlar.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-106">This article provides details of hello API and several examples for performing different operations.</span></span>

<span data-ttu-id="4e0dc-107">Merhaba günlük analizi Search REST API'sini RESTful olan ve hello Azure Resource Manager REST API'si erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-107">hello Log Analytics Search REST API is RESTful and can be accessed via hello Azure Resource Manager REST API.</span></span> <span data-ttu-id="4e0dc-108">Bu belgede hello API kullanarak bir PowerShell komut satırı burada erişilen örnekler bulacaksınız [ARMClient](https://github.com/projectkudu/ARMClient), çağırma basitleştiren bir açık kaynak komut satırı aracı hello Azure Kaynak Yöneticisi API'si.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-108">In this document you will find examples where hello API is accessed from a PowerShell command line using  [ARMClient](https://github.com/projectkudu/ARMClient), an open source command line tool that simplifies invoking hello Azure Resource Manager API.</span></span> <span data-ttu-id="4e0dc-109">Merhaba kullanımını ARMClient ve PowerShell birçok seçenekleri tooaccess hello günlük analizi arama API biridir.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-109">hello use of ARMClient and PowerShell is one of many options tooaccess hello Log Analytics Search API.</span></span> <span data-ttu-id="4e0dc-110">Bu araçların hello RESTful Azure Kaynak Yöneticisi API'si toomake çağrıları tooOMS çalışma alanları kullanma ve bunların içindeki arama komutları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-110">With these tools you can utilize hello RESTful Azure Resource Manager API toomake calls tooOMS workspaces and perform search commands within them.</span></span> <span data-ttu-id="4e0dc-111">Arama sonuçları tooyou toouse hello arama sonuçları birçok farklı yolla program aracılığıyla sağlayarak JSON biçiminde Hello API çıkarır.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-111">hello API will output search results tooyou in JSON format, allowing you toouse hello search results in many different ways programmatically.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4e0dc-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="4e0dc-112">Prerequisites</span></span>
<span data-ttu-id="4e0dc-113">Şu anda, uyarıları günlük analizi olarak kaydedilmiş bir aramayı ile yalnızca oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-113">Currently, alerts can only be created with a saved search in Log Analytics.</span></span>  <span data-ttu-id="4e0dc-114">Toohello başvurabilir [günlük Search REST API'sini](log-analytics-log-search-api.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-114">You can refer toohello [Log Search REST API](log-analytics-log-search-api.md) for more information.</span></span>

## <a name="schedules"></a><span data-ttu-id="4e0dc-115">Zamanlamalar</span><span class="sxs-lookup"><span data-stu-id="4e0dc-115">Schedules</span></span>
<span data-ttu-id="4e0dc-116">Kaydedilmiş bir aramayı bir veya daha fazla zamanlama olabilir.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-116">A saved search can have one or more schedules.</span></span> <span data-ttu-id="4e0dc-117">Merhaba zamanlama ne sıklıkta hello arama çalıştırılan tanımlar ve hello zaman aralığı içinde hangi hello ölçütleri tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-117">hello schedule defines how often hello search is run and hello time interval over which hello criteria is identified.</span></span>
<span data-ttu-id="4e0dc-118">Zamanlamaları, aşağıdaki tablonun hello hello özelliklere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-118">Schedules have hello properties in hello following table.</span></span>

| <span data-ttu-id="4e0dc-119">Özellik</span><span class="sxs-lookup"><span data-stu-id="4e0dc-119">Property</span></span> | <span data-ttu-id="4e0dc-120">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4e0dc-120">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4e0dc-121">aralığı</span><span class="sxs-lookup"><span data-stu-id="4e0dc-121">Interval</span></span> |<span data-ttu-id="4e0dc-122">Ne sıklıkta hello arama çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-122">How often hello search is run.</span></span> <span data-ttu-id="4e0dc-123">Dakika cinsinden ölçülür.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-123">Measured in minutes.</span></span> |
| <span data-ttu-id="4e0dc-124">QueryTimeSpan</span><span class="sxs-lookup"><span data-stu-id="4e0dc-124">QueryTimeSpan</span></span> |<span data-ttu-id="4e0dc-125">hangi hello ölçütleri değerlendirildiği hello zaman aralığı.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-125">hello time interval over which hello criteria is evaluated.</span></span> <span data-ttu-id="4e0dc-126">Eşit tooor aralığından daha büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-126">Must be equal tooor greater than Interval.</span></span> <span data-ttu-id="4e0dc-127">Dakika cinsinden ölçülür.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-127">Measured in minutes.</span></span> |
| <span data-ttu-id="4e0dc-128">Sürüm</span><span class="sxs-lookup"><span data-stu-id="4e0dc-128">Version</span></span> |<span data-ttu-id="4e0dc-129">Merhaba kullanılan API sürümü.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-129">hello API version being used.</span></span>  <span data-ttu-id="4e0dc-130">Şu anda, bu her zaman too1 olarak ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-130">Currently, this should always be set too1.</span></span> |

<span data-ttu-id="4e0dc-131">Örneğin, bir olay sorgusu bir aralığı 15 dakika ve 30 dakikalık bir zaman aralığı ile göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-131">For example, consider an event query with an Interval of 15 minutes and a Timespan of 30 minutes.</span></span> <span data-ttu-id="4e0dc-132">Bu durumda, hello sorgu 15 dakikada bir çalışır ve hello ölçütleri 30 dakikalık aralık tooresolve tootrue etseydi uyarı tetikleyen.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-132">In this case, hello query would be run every 15 minutes, and an alert would be triggered if hello criteria continued tooresolve tootrue over a 30 minute span.</span></span>

### <a name="retrieving-schedules"></a><span data-ttu-id="4e0dc-133">Zamanlamalar alınıyor</span><span class="sxs-lookup"><span data-stu-id="4e0dc-133">Retrieving schedules</span></span>
<span data-ttu-id="4e0dc-134">Kullanım hello kayıtlı bir aramaya tüm zamanlamalar yöntemi tooretrieve alın.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-134">Use hello Get method tooretrieve all schedules for a saved search.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules?api-version=2015-03-20

<span data-ttu-id="4e0dc-135">Kullanım hello belirli bir zamanlama için kaydedilmiş bir aramayı bir zamanlama kimliği tooretrieve yöntemiyle alın.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-135">Use hello Get method with a schedule ID tooretrieve a particular schedule for a saved search.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20

<span data-ttu-id="4e0dc-136">Bir zamanlama için bir örnek yanıt aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-136">Following is a sample response for a schedule.</span></span>

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

### <a name="creating-a-schedule"></a><span data-ttu-id="4e0dc-137">Bir zamanlama oluşturma</span><span class="sxs-lookup"><span data-stu-id="4e0dc-137">Creating a schedule</span></span>
<span data-ttu-id="4e0dc-138">Benzersiz zamanlama kimliği toocreate yeni bir zamanlama Hello Put yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-138">Use hello Put method with a unique schedule ID toocreate a new schedule.</span></span>  <span data-ttu-id="4e0dc-139">İki zamanlamaları olamaz sahip Merhaba, aynı kimliği kayıtlı aramalar farklı ile ilişkili olsa bile unutmayın.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-139">Note that two schedules cannot have hello same ID even if they are associated with different saved searches.</span></span>  <span data-ttu-id="4e0dc-140">Merhaba OMS konsolunda bir zamanlama oluşturmak, bir GUID hello zamanlama kimliği için oluşturulur</span><span class="sxs-lookup"><span data-stu-id="4e0dc-140">When you create a schedule in hello OMS console, a GUID is created for hello schedule ID.</span></span>

> [!NOTE]
> <span data-ttu-id="4e0dc-141">Tüm kayıtlı aramaları, zamanlamaları ve günlük analizi API hello ile oluşturulan eylemler için Hello adı küçük olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-141">hello name for all saved searches, schedules, and actions created with hello Log Analytics API must be in lowercase.</span></span>

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson

### <a name="editing-a-schedule"></a><span data-ttu-id="4e0dc-142">Bir zamanlama düzenleme</span><span class="sxs-lookup"><span data-stu-id="4e0dc-142">Editing a schedule</span></span>
<span data-ttu-id="4e0dc-143">Kimliği aynı kaydedilmiş hello için arama zamanlama toomodify mevcut bir zamanlamayı ile Merhaba Put yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-143">Use hello Put method with an existing schedule ID for hello same saved search toomodify that schedule.</span></span>  <span data-ttu-id="4e0dc-144">Merhaba hello istek gövdesi hello etag hello planının eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-144">hello body of hello request must include hello etag of hello schedule.</span></span>

      $scheduleJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\""','properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
      armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson


### <a name="deleting-schedules"></a><span data-ttu-id="4e0dc-145">Zamanlamalar silme</span><span class="sxs-lookup"><span data-stu-id="4e0dc-145">Deleting schedules</span></span>
<span data-ttu-id="4e0dc-146">Zamanlama kimliği toodelete bir zamanlama Hello Delete yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-146">Use hello Delete method with a schedule ID toodelete a schedule.</span></span>

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20


## <a name="actions"></a><span data-ttu-id="4e0dc-147">Eylemler</span><span class="sxs-lookup"><span data-stu-id="4e0dc-147">Actions</span></span>
<span data-ttu-id="4e0dc-148">Bir zamanlama birden çok eylemler olabilir.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-148">A schedule can have multiple actions.</span></span> <span data-ttu-id="4e0dc-149">Bir eylem bir posta gönderme veya bir runbook'u başlatma gibi bir veya daha fazla işlemleri tooperform tanımlayabilir veya ne zaman bir arama sonuçlarını hello bazı ölçütlere uyan belirleyen bir eşik tanımlayabilir.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-149">An action may define one or more processes tooperform such as sending a mail or starting a runbook, or it may define a threshold that determines when hello results of a search match some criteria.</span></span>  <span data-ttu-id="4e0dc-150">Merhaba eşiğine ulaşıldığında hello işlemlerin gerçekleştirilmesi bazı eylemler her ikisi de tanımlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-150">Some actions will define both so that hello processes are performed when hello threshold is met.</span></span>

<span data-ttu-id="4e0dc-151">Tüm eylemleri aşağıdaki tablonun hello hello özelliklere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-151">All actions have hello properties in hello following table.</span></span>  <span data-ttu-id="4e0dc-152">Farklı türde bir uyarı aşağıda açıklanan farklı ek özellikler vardır.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-152">Different types of alerts have different additional properties which are described below.</span></span>

| <span data-ttu-id="4e0dc-153">Özellik</span><span class="sxs-lookup"><span data-stu-id="4e0dc-153">Property</span></span> | <span data-ttu-id="4e0dc-154">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4e0dc-154">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4e0dc-155">Tür</span><span class="sxs-lookup"><span data-stu-id="4e0dc-155">Type</span></span> |<span data-ttu-id="4e0dc-156">Merhaba eylem türü.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-156">Type of hello action.</span></span>  <span data-ttu-id="4e0dc-157">Şu anda hello olası değerler, uyarı ve Web kancası olur.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-157">Currently hello possible values are Alert and Webhook.</span></span> |
| <span data-ttu-id="4e0dc-158">Ad</span><span class="sxs-lookup"><span data-stu-id="4e0dc-158">Name</span></span> |<span data-ttu-id="4e0dc-159">Merhaba uyarı görünen adı.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-159">Display name for hello alert.</span></span> |
| <span data-ttu-id="4e0dc-160">Sürüm</span><span class="sxs-lookup"><span data-stu-id="4e0dc-160">Version</span></span> |<span data-ttu-id="4e0dc-161">Merhaba kullanılan API sürümü.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-161">hello API version being used.</span></span>  <span data-ttu-id="4e0dc-162">Şu anda, bu her zaman too1 olarak ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-162">Currently, this should always be set too1.</span></span> |

### <a name="retrieving-actions"></a><span data-ttu-id="4e0dc-163">Eylemler Alınıyor</span><span class="sxs-lookup"><span data-stu-id="4e0dc-163">Retrieving actions</span></span>
<span data-ttu-id="4e0dc-164">Kullanım hello tüm eylemler için bir zamanlama yöntemi tooretrieve alın.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-164">Use hello Get method tooretrieve all actions for a schedule.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules/{Schedule ID}/actions?api-version=2015-03-20

<span data-ttu-id="4e0dc-165">Kullanım hello hello Eylem Kimliği tooretrieve yöntemiyle bir zamanlama için belirli bir eylemi alın.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-165">Use hello Get method with hello action ID tooretrieve a particular action for a schedule.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/actions/{Action ID}?api-version=2015-03-20

### <a name="creating-or-editing-actions"></a><span data-ttu-id="4e0dc-166">Oluşturma veya Eylemler düzenleme</span><span class="sxs-lookup"><span data-stu-id="4e0dc-166">Creating or editing actions</span></span>
<span data-ttu-id="4e0dc-167">Benzersiz toohello zamanlama toocreate yeni bir eylem bir eylem kimliği ile Merhaba Put yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-167">Use hello Put method with an action ID that is unique toohello schedule toocreate a new action.</span></span>  <span data-ttu-id="4e0dc-168">Bir eylemin hello OMS konsolunda oluşturduğunuzda, bir GUID için hello eylem kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-168">When you create an action in hello OMS console, a GUID is for hello action ID.</span></span>

> [!NOTE]
> <span data-ttu-id="4e0dc-169">Tüm kayıtlı aramaları, zamanlamaları ve günlük analizi API hello ile oluşturulan eylemler için Hello adı küçük olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-169">hello name for all saved searches, schedules, and actions created with hello Log Analytics API must be in lowercase.</span></span>

<span data-ttu-id="4e0dc-170">Kimliği aynı kaydedilmiş hello için arama zamanlama toomodify var olan bir eylem ile Merhaba Put yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-170">Use hello Put method with an existing action ID for hello same saved search toomodify that schedule.</span></span>  <span data-ttu-id="4e0dc-171">Merhaba hello istek gövdesi hello etag hello planının eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-171">hello body of hello request must include hello etag of hello schedule.</span></span>

<span data-ttu-id="4e0dc-172">Bu örnekler aşağıdaki hello bölümler sağlanan şekilde hello istek biçimi yeni bir eylem oluşturmak için eylem türüne göre değişir.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-172">hello request format for creating a new action varies by action type so these examples are provided in hello sections below.</span></span>

### <a name="deleting-actions"></a><span data-ttu-id="4e0dc-173">Eylemler siliniyor</span><span class="sxs-lookup"><span data-stu-id="4e0dc-173">Deleting actions</span></span>
<span data-ttu-id="4e0dc-174">Hello Eylem Kimliği toodelete eylemin Hello Delete yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-174">Use hello Delete method with hello action ID toodelete an action.</span></span>

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/Actions/{Action ID}?api-version=2015-03-20

### <a name="alert-actions"></a><span data-ttu-id="4e0dc-175">Uyarı eylemleri</span><span class="sxs-lookup"><span data-stu-id="4e0dc-175">Alert Actions</span></span>
<span data-ttu-id="4e0dc-176">Bir zamanlama tek bir uyarı eylemi olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-176">A Schedule should have one and only one Alert action.</span></span>  <span data-ttu-id="4e0dc-177">Uyarı eylemleri, bir veya daha fazla tablo aşağıdaki hello hello bölümlerde sahip.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-177">Alert actions have one or more of hello sections in hello following table.</span></span>  <span data-ttu-id="4e0dc-178">Her daha aşağıda ayrıntılı olarak açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-178">Each is described in further detail below.</span></span>

| <span data-ttu-id="4e0dc-179">Bölüm</span><span class="sxs-lookup"><span data-stu-id="4e0dc-179">Section</span></span> | <span data-ttu-id="4e0dc-180">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4e0dc-180">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4e0dc-181">Eşik</span><span class="sxs-lookup"><span data-stu-id="4e0dc-181">Threshold</span></span> |<span data-ttu-id="4e0dc-182">Merhaba eylemi çalıştırıldığında ölçütlerini.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-182">Criteria for when hello action is run.</span></span> |
| <span data-ttu-id="4e0dc-183">EmailNotification</span><span class="sxs-lookup"><span data-stu-id="4e0dc-183">EmailNotification</span></span> |<span data-ttu-id="4e0dc-184">Posta toomultiple alıcılar gönderin.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-184">Send mail toomultiple recipients.</span></span> |
| <span data-ttu-id="4e0dc-185">Düzeltme</span><span class="sxs-lookup"><span data-stu-id="4e0dc-185">Remediation</span></span> |<span data-ttu-id="4e0dc-186">Bir runbook'un Azure Otomasyon tooattempt tanımlanan toocorrect sorunu başlatın.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-186">Start a runbook in Azure Automation tooattempt toocorrect identified issue.</span></span> |

#### <a name="thresholds"></a><span data-ttu-id="4e0dc-187">Eşikleri</span><span class="sxs-lookup"><span data-stu-id="4e0dc-187">Thresholds</span></span>
<span data-ttu-id="4e0dc-188">Bir uyarı eylem tek bir eşik olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-188">An Alert action should have one and only one threshold.</span></span>  <span data-ttu-id="4e0dc-189">Kaydedilmiş bir aramayı Hello sonuçlarını arama ile ilişkili bir eylemin hello eşiği eşleştiğinde, başka bir işlem bu uygulamada çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-189">When hello results of a saved search match hello threshold in an action associated with that search, then any other processes in that action are run.</span></span>  <span data-ttu-id="4e0dc-190">Böylece eşikleri içermeyen diğer türleri Eylemler ile kullanılan bir eylem yalnızca bir eşik de içerebilir.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-190">An action can also contain only a threshold so that it can be used with actions of other types that don’t contain thresholds.</span></span>

<span data-ttu-id="4e0dc-191">Eşikleri aşağıdaki tablonun hello hello özelliklere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-191">Thresholds have hello properties in hello following table.</span></span>

| <span data-ttu-id="4e0dc-192">Özellik</span><span class="sxs-lookup"><span data-stu-id="4e0dc-192">Property</span></span> | <span data-ttu-id="4e0dc-193">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4e0dc-193">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4e0dc-194">işleci</span><span class="sxs-lookup"><span data-stu-id="4e0dc-194">Operator</span></span> |<span data-ttu-id="4e0dc-195">Merhaba eşik karşılaştırma işleci.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-195">Operator for hello threshold comparison.</span></span> <br> <span data-ttu-id="4e0dc-196">gt şundan =</span><span class="sxs-lookup"><span data-stu-id="4e0dc-196">gt = Greater Than</span></span> <br> <span data-ttu-id="4e0dc-197">lt = küçüktür</span><span class="sxs-lookup"><span data-stu-id="4e0dc-197">lt = Less Than</span></span> |
| <span data-ttu-id="4e0dc-198">Değer</span><span class="sxs-lookup"><span data-stu-id="4e0dc-198">Value</span></span> |<span data-ttu-id="4e0dc-199">Merhaba eşik değeri.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-199">Value for hello threshold.</span></span> |

<span data-ttu-id="4e0dc-200">Örneğin, bir olay sorgusu zaman aralığı 15 dakika, 30 dakikalık bir Timespan ve 10'dan büyük bir eşik ile göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-200">For example, consider an event query with an Interval of 15 minutes, a Timespan of 30 minutes, and a Threshold of greater than 10.</span></span> <span data-ttu-id="4e0dc-201">Bu durumda, hello sorgu 15 dakikada bir çalışır ve 30 dakikalık aralık oluşturulan 10 olayları döndürülen bir uyarı tetikleyen.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-201">In this case, hello query would be run every 15 minutes, and an alert would be triggered if it returned 10 events that were created over a 30 minute span.</span></span>

<span data-ttu-id="4e0dc-202">Aşağıdaki örnek yanıt için bir eylem yalnızca bir eşik ile ' dir.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-202">Following is a sample response for an action with only a threshold.</span></span>  

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

<span data-ttu-id="4e0dc-203">Merhaba Put yöntemi için bir zamanlama benzersiz Eylem Kimliği toocreate yeni bir eşik eylemi kullanın.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-203">Use hello Put method with a unique action ID toocreate a new threshold action for a schedule.</span></span>  

    $thresholdJson = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

<span data-ttu-id="4e0dc-204">Kullanım hello var olan bir eylem kimliği toomodify yöntemiyle bir zamanlama için bir eşik eylem yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-204">Use hello Put method with an existing action ID toomodify a threshold action for a schedule.</span></span>  <span data-ttu-id="4e0dc-205">Merhaba hello istek gövdesi hello eylemin hello etag eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-205">hello body of hello request must include hello etag of hello action.</span></span>

    $thresholdJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

#### <a name="email-notification"></a><span data-ttu-id="4e0dc-206">E-posta bildirimi</span><span class="sxs-lookup"><span data-stu-id="4e0dc-206">Email Notification</span></span>
<span data-ttu-id="4e0dc-207">Posta tooone ya da daha fazla alıcı e-posta bildirimleri gönderin.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-207">Email Notifications send mail tooone or more recipients.</span></span>  <span data-ttu-id="4e0dc-208">Bunlar, aşağıdaki tablonun hello hello özellikleri içerir.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-208">They include hello properties in hello following table.</span></span>

| <span data-ttu-id="4e0dc-209">Özellik</span><span class="sxs-lookup"><span data-stu-id="4e0dc-209">Property</span></span> | <span data-ttu-id="4e0dc-210">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4e0dc-210">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4e0dc-211">Alıcıları</span><span class="sxs-lookup"><span data-stu-id="4e0dc-211">Recipients</span></span> |<span data-ttu-id="4e0dc-212">Posta adresleri listesi.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-212">List of mail addresses.</span></span> |
| <span data-ttu-id="4e0dc-213">Konu</span><span class="sxs-lookup"><span data-stu-id="4e0dc-213">Subject</span></span> |<span data-ttu-id="4e0dc-214">Merhaba posta Hello konu.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-214">hello subject of hello mail.</span></span> |
| <span data-ttu-id="4e0dc-215">Eki</span><span class="sxs-lookup"><span data-stu-id="4e0dc-215">Attachment</span></span> |<span data-ttu-id="4e0dc-216">Bu her zaman "Hiçbiri" değerine sahip şekilde ekleri şu anda, desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-216">Attachments are not currently supported, so this will always have a value of “None”.</span></span> |

<span data-ttu-id="4e0dc-217">Aşağıdaki örnek yanıt bir eşik ile bir e-posta bildirim eylemi için ' dir.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-217">Following is a sample response for an email notification action with a threshold.</span></span>  

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
            "Subject": "This is hello subject",
            "Attachment": "None"
        },
        "Version": 1
    }

<span data-ttu-id="4e0dc-218">Merhaba Put yöntemi için bir zamanlama benzersiz Eylem Kimliği toocreate yeni bir e-posta eylemi kullanın.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-218">Use hello Put method with a unique action ID toocreate a new e-mail action for a schedule.</span></span>  <span data-ttu-id="4e0dc-219">Hello hello kaydedilmiş arama sonuçlarını hello eşiği aştığında hello posta gönderilen şekilde hello aşağıdaki örnek bir e-posta bildirimi bir eşik ile oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-219">hello following example creates an email notification with a threshold so hello mail is sent when hello results of hello saved search exceed hello threshold.</span></span>

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

<span data-ttu-id="4e0dc-220">Merhaba Put yöntemini bir varolan eylem kimliği toomodify ile bir e-posta eylemi için bir zamanlama kullanın.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-220">Use hello Put method with an existing action ID toomodify an e-mail action for a schedule.</span></span>  <span data-ttu-id="4e0dc-221">Merhaba hello istek gövdesi hello eylemin hello etag eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-221">hello body of hello request must include hello etag of hello action.</span></span>

    $emailJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

#### <a name="remediation-actions"></a><span data-ttu-id="4e0dc-222">Düzeltme eylemleri</span><span class="sxs-lookup"><span data-stu-id="4e0dc-222">Remediation actions</span></span>
<span data-ttu-id="4e0dc-223">Düzeltmeler, Azure automation'da hello uyarı tarafından tanımlanan toocorrect hello sorun çalışır bir runbook başlatın.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-223">Remediations start a runbook in Azure Automation that attempts toocorrect hello problem identified by hello alert.</span></span>  <span data-ttu-id="4e0dc-224">Bir düzeltme eylemi kullanılan hello runbook için bir Web kancası oluşturun ve ardından hello URI hello WebhookUri özelliği belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-224">You must create a webhook for hello runbook used in a remediation action and then specify hello URI in hello WebhookUri property.</span></span>  <span data-ttu-id="4e0dc-225">Merhaba OMS konsolunu kullanarak bu eylemi oluşturduğunuzda, yeni bir Web kancası hello runbook için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-225">When you create this action using hello OMS console, a new webhook is automatically created for hello runbook.</span></span>

<span data-ttu-id="4e0dc-226">Düzeltmeler, aşağıdaki tablonun hello hello özellikleri içerir.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-226">Remediations include hello properties in hello following table.</span></span>

| <span data-ttu-id="4e0dc-227">Özellik</span><span class="sxs-lookup"><span data-stu-id="4e0dc-227">Property</span></span> | <span data-ttu-id="4e0dc-228">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4e0dc-228">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4e0dc-229">RunbookName</span><span class="sxs-lookup"><span data-stu-id="4e0dc-229">RunbookName</span></span> |<span data-ttu-id="4e0dc-230">Merhaba runbook adı.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-230">Name of hello runbook.</span></span> <span data-ttu-id="4e0dc-231">Bu hello Otomasyon çözümünü OMS çalışma alanınızdaki yapılandırılan hello Otomasyon hesabı yayımlanan bir runbook'ta eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-231">This must match a published runbook in hello automation account configured in hello Automation Solution in your OMS workspace.</span></span> |
| <span data-ttu-id="4e0dc-232">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="4e0dc-232">WebhookUri</span></span> |<span data-ttu-id="4e0dc-233">Merhaba Web kancası URI'si.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-233">URI of hello webhook.</span></span> |
| <span data-ttu-id="4e0dc-234">Süre sonu</span><span class="sxs-lookup"><span data-stu-id="4e0dc-234">Expiry</span></span> |<span data-ttu-id="4e0dc-235">Merhaba sona erme tarihi ve saati hello Web kancası.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-235">hello expiration date and time of hello webhook.</span></span>  <span data-ttu-id="4e0dc-236">Merhaba Web kancası bir sona erme yoksa, bu geçerli bir gelecek tarih olabilir.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-236">If hello webhook doesn’t have an expiration, then this can be any valid future date.</span></span> |

<span data-ttu-id="4e0dc-237">Aşağıdaki örnek yanıt bir eşik ile bir düzeltme eylemi için ' dir.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-237">Following is a sample response for a remediation action with a threshold.</span></span>

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

<span data-ttu-id="4e0dc-238">Merhaba Put yöntemini benzersiz Eylem Kimliği toocreate yeni bir düzeltme eylemi için bir zamanlama kullanın.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-238">Use hello Put method with a unique action ID toocreate a new remediation action for a schedule.</span></span>  <span data-ttu-id="4e0dc-239">Merhaba hello kaydedilmiş arama sonuçlarını hello eşiği aştığında hello runbook başlatıldıktan şekilde hello aşağıdaki örnek bir düzeltme bir eşik ile oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-239">hello following example creates a remediation with a threshold so hello runbook is started when hello results of hello saved search exceed hello threshold.</span></span>

    $remediateJson = "{'properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

<span data-ttu-id="4e0dc-240">Merhaba Put yöntemini bir varolan eylem kimliği toomodify ile bir düzeltme eylemi için bir zamanlama kullanın.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-240">Use hello Put method with an existing action ID toomodify a remediation action for a schedule.</span></span>  <span data-ttu-id="4e0dc-241">Merhaba hello istek gövdesi hello eylemin hello etag eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-241">hello body of hello request must include hello etag of hello action.</span></span>

    $remediateJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

#### <a name="example"></a><span data-ttu-id="4e0dc-242">Örnek</span><span class="sxs-lookup"><span data-stu-id="4e0dc-242">Example</span></span>
<span data-ttu-id="4e0dc-243">Tam örnek toocreate yeni bir e-posta uyarı aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-243">Following is a complete example toocreate a new email alert.</span></span>  <span data-ttu-id="4e0dc-244">Bu eşik ve e-posta içeren bir eylem birlikte yeni bir zamanlama oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-244">This creates a new schedule along with an action containing a threshold and email.</span></span>

    $subscriptionId = "3d56705e-5b26-5bcc-9368-dbc8d2fafbfc"
    $resourceGroup  = "MyResourceGroup"    
    $workspaceName    = "MyWorkspace"
    $searchId       = "MySearch"
    $scheduleId     = "MySchedule"
    $thresholdId    = "MyThreshold"
    $actionId       = "MyEmailAction"

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/?api-version=2015-03-20 $scheduleJson

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Severity':'Warning', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/actions/$actionId/?api-version=2015-03-20 $emailJson

### <a name="webhook-actions"></a><span data-ttu-id="4e0dc-245">Web kancası eylemleri</span><span class="sxs-lookup"><span data-stu-id="4e0dc-245">Webhook actions</span></span>
<span data-ttu-id="4e0dc-246">Web kancası eylemleri, bir URL çağırma ve isteğe bağlı olarak gönderilen bir yükü toobe sağlayan bir işlem başlatın.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-246">Webhook actions start a process by calling a URL and optionally providing a payload toobe sent.</span></span>  <span data-ttu-id="4e0dc-247">Azure Otomasyon çalışma kitabı dışındaki işlemler çağırabilir Web kancası için amacı dışında benzer tooRemediation Eylemler oldukları.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-247">They are similar tooRemediation actions except they are meant for webhooks that may invoke processes other than Azure Automation runbooks.</span></span>  <span data-ttu-id="4e0dc-248">Yükü teslim toobe toohello uzak bir işlem sağlayarak hello ek bir seçeneğiniz de sağlar.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-248">They also provide hello additional option of providing a payload toobe delivered toohello remote process.</span></span>

<span data-ttu-id="4e0dc-249">Web kancası eylemleri bir eşik gerekmez ancak bunun yerine bir eşik ile uyarı bir eylemi var. tooa zamanlama eklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-249">Webhook actions do not have a threshold but instead should be added tooa schedule that has an Alert action with a threshold.</span></span>  <span data-ttu-id="4e0dc-250">Merhaba eşiğine ulaşıldığında, tüm çalışan birden çok Web kancası eylemleri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-250">You can add multiple Webhook actions that will all be run when hello threshold is met.</span></span>

<span data-ttu-id="4e0dc-251">Web kancası eylemleri aşağıdaki tablonun hello hello özellikleri içerir.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-251">Webhook actions include hello properties in hello following table.</span></span>

| <span data-ttu-id="4e0dc-252">Özellik</span><span class="sxs-lookup"><span data-stu-id="4e0dc-252">Property</span></span> | <span data-ttu-id="4e0dc-253">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4e0dc-253">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4e0dc-254">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="4e0dc-254">WebhookUri</span></span> |<span data-ttu-id="4e0dc-255">Merhaba posta Hello konu.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-255">hello subject of hello mail.</span></span> |
| <span data-ttu-id="4e0dc-256">CustomPayload</span><span class="sxs-lookup"><span data-stu-id="4e0dc-256">CustomPayload</span></span> |<span data-ttu-id="4e0dc-257">Özel yük toobe toohello Web kancası gönderdi.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-257">Custom payload toobe sent toohello webhook.</span></span>  <span data-ttu-id="4e0dc-258">Merhaba biçimi hangi hello Web kancası bekleniyor bağlı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-258">hello format will depend on what hello webhook is expecting.</span></span> |

<span data-ttu-id="4e0dc-259">Web kancası eylem ve bir eşik ile ilişkili bir uyarı eylem için örnek yanıt aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-259">Following is a sample response for webhook action and an associated alert action with a threshold.</span></span>

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

#### <a name="create-or-edit-a-webhook-action"></a><span data-ttu-id="4e0dc-260">Oluşturma veya bir Web kancası eylemi düzenleme</span><span class="sxs-lookup"><span data-stu-id="4e0dc-260">Create or edit a webhook action</span></span>
<span data-ttu-id="4e0dc-261">Merhaba Put yöntemi için bir zamanlama benzersiz Eylem Kimliği toocreate yeni bir Web kancası eylemi kullanın.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-261">Use hello Put method with a unique action ID toocreate a new webhook action for a schedule.</span></span>  <span data-ttu-id="4e0dc-262">Böylece Hello hello kaydedilmiş arama sonuçlarını hello eşiği aştığında hello Web kancası tetiklenen hello aşağıdaki örnek bir Web kancası eylemi ve bir uyarı eylem bir eşik ile oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-262">hello following example creates a Webhook action and an Alert action with a threshold so that hello webhook will be triggered when hello results of hello saved search exceed hello threshold.</span></span>

    $thresholdAction = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdAction

    $webhookAction = "{'properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

<span data-ttu-id="4e0dc-263">Merhaba Put yöntemini bir varolan eylem kimliği toomodify ile bir Web kancası eylemi için bir zamanlama kullanın.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-263">Use hello Put method with an existing action ID toomodify a webhook action for a schedule.</span></span>  <span data-ttu-id="4e0dc-264">Merhaba hello istek gövdesi hello eylemin hello etag eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-264">hello body of hello request must include hello etag of hello action.</span></span>

    $webhookAction = "{'etag': 'W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"','properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

## <a name="next-steps"></a><span data-ttu-id="4e0dc-265">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4e0dc-265">Next steps</span></span>
* <span data-ttu-id="4e0dc-266">Kullanım hello [REST API tooperform günlük aramaları](log-analytics-log-search-api.md) günlük analizi içinde.</span><span class="sxs-lookup"><span data-stu-id="4e0dc-266">Use hello [REST API tooperform log searches](log-analytics-log-search-api.md) in Log Analytics.</span></span>

