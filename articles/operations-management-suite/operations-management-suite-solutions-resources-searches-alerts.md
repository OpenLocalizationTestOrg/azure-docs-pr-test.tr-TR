---
title: "aaaSaved arar ve uyarılar OMS çözümleri | Microsoft Docs"
description: "OMS çözümlerinde genellikle Kaydedilmiş aramaları hello çözümü tarafından toplanan günlük analizi tooanalyze verileri de içerir.  Aynı zamanda uyarılar toonotify hello kullanıcı tanımlar olabilir veya otomatik olarak yanıt tooa kritik sorunu eylemi gerçekleştirin.  Bu makalede, yönetim çözümlerine dahil şekilde nasıl toodefine günlük analizi arar ve Uyarıları bir ARM şablonu kaydedileceği açıklanmaktadır."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 93d7c5bbf061473833ca6c0a8e4d8e10d923f3ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-log-analytics-saved-searches-and-alerts-toooms-management-solution-preview"></a><span data-ttu-id="ff98b-105">Günlük analizi ekleme arar ve Uyarıları tooOMS kaydedilen yönetim çözümü (Önizleme)</span><span class="sxs-lookup"><span data-stu-id="ff98b-105">Adding Log Analytics saved searches and alerts tooOMS management solution (Preview)</span></span>

> [!NOTE]
> <span data-ttu-id="ff98b-106">Bu, şu anda önizlemede OMS yönetim çözümleri oluşturmak için başlangıç belgesidir.</span><span class="sxs-lookup"><span data-stu-id="ff98b-106">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="ff98b-107">Aşağıda açıklanan herhangi bir şema konu toochange ' dir.</span><span class="sxs-lookup"><span data-stu-id="ff98b-107">Any schema described below is subject toochange.</span></span>   


<span data-ttu-id="ff98b-108">[OMS yönetim çözümlerine](operations-management-suite-solutions.md) genellikle içerecektir [kayıtlı aramalar](../log-analytics/log-analytics-log-searches.md) hello çözümü tarafından toplanan günlük analizi tooanalyze veri.</span><span class="sxs-lookup"><span data-stu-id="ff98b-108">[Management solutions in OMS](operations-management-suite-solutions.md) will typically include [saved searches](../log-analytics/log-analytics-log-searches.md) in Log Analytics tooanalyze data collected by hello solution.</span></span>  <span data-ttu-id="ff98b-109">Ayrıca tanımlayabilir [uyarıları](../log-analytics/log-analytics-alerts.md) toonotify hello kullanıcı ya da otomatik olarak yanıt tooa kritik sorunu eylemi gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="ff98b-109">They may also define [alerts](../log-analytics/log-analytics-alerts.md) toonotify hello user or automatically take action in response tooa critical issue.</span></span>  <span data-ttu-id="ff98b-110">Günlük analizi toodefine arar ve uyarılar kaydedilme bu makalede bir [kaynak yönetimi şablonu](../resource-manager-template-walkthrough.md) içinde eklenebilir şekilde [yönetim çözümleri](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="ff98b-110">This article describes how toodefine Log Analytics saved searches and alerts in a [Resource Management template](../resource-manager-template-walkthrough.md) so they can be included in [management solutions](operations-management-suite-solutions-creating.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ff98b-111">Merhaba bu makaledeki örnekler parametreleri ve ya da gerekli veya ortak toomanagement çözümleri ve açıklanan değişkenleri kullanma [Operations Management Suite (OMS) yönetimi çözümleri oluşturma](operations-management-suite-solutions-creating.md)</span><span class="sxs-lookup"><span data-stu-id="ff98b-111">hello samples in this article use parameters and variables that are either required or common toomanagement solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="ff98b-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ff98b-112">Prerequisites</span></span>
<span data-ttu-id="ff98b-113">Bu makale, zaten çok konusunda bilgi sahibi olduğunuzu varsayar[bir yönetim çözümü oluşturma](operations-management-suite-solutions-creating.md) ve hello yapısını bir [ARM şablonu](../resource-group-authoring-templates.md) ve çözüm dosya.</span><span class="sxs-lookup"><span data-stu-id="ff98b-113">This article assumes that you're already familiar with how too[create a management solution](operations-management-suite-solutions-creating.md) and hello structure of an [ARM template](../resource-group-authoring-templates.md) and solution file.</span></span>


## <a name="log-analytics-workspace"></a><span data-ttu-id="ff98b-114">Günlük analizi çalışma alanı</span><span class="sxs-lookup"><span data-stu-id="ff98b-114">Log Analytics Workspace</span></span>
<span data-ttu-id="ff98b-115">Günlük analizi tüm kaynaklarında bulunan bir [çalışma](../log-analytics/log-analytics-manage-access.md).</span><span class="sxs-lookup"><span data-stu-id="ff98b-115">All resources in Log Analytics are contained in a [workspace](../log-analytics/log-analytics-manage-access.md).</span></span>  <span data-ttu-id="ff98b-116">Bölümünde açıklandığı gibi [OMS çalışma ve Automation hesabı](operations-management-suite-solutions.md#oms-workspace-and-automation-account) hello çalışma hello Yönetimi çözümünde dahil değildir ancak hello çözüm yüklenmeden önce mevcut olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff98b-116">As described in [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) hello workspace isn't included in hello management solution but must exist before hello solution is installed.</span></span>  <span data-ttu-id="ff98b-117">Kullanılabilir değilse, hello çözüm yükleme başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="ff98b-117">If it isn't available, then hello solution install will fail.</span></span>

<span data-ttu-id="ff98b-118">Merhaba hello çalışma her günlük analizi kaynak hello adlarında adıdır.</span><span class="sxs-lookup"><span data-stu-id="ff98b-118">hello name of hello workspace is in hello name of each Log Analytics resource.</span></span>  <span data-ttu-id="ff98b-119">Bu hello ile Merhaba çözümde yapılır **çalışma** savedsearch kaynak örneği aşağıdaki hello olduğu gibi parametre.</span><span class="sxs-lookup"><span data-stu-id="ff98b-119">This is done in hello solution with hello **workspace** parameter as in hello following example of a savedsearch resource.</span></span>

    "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearchId'))]"


## <a name="saved-searches"></a><span data-ttu-id="ff98b-120">Kaydedilen aramalar</span><span class="sxs-lookup"><span data-stu-id="ff98b-120">Saved Searches</span></span>
<span data-ttu-id="ff98b-121">Dahil [kayıtlı aramalar](../log-analytics/log-analytics-log-searches.md) çözümünüz tarafından toplanan çözüm tooallow kullanıcılar tooquery veri.</span><span class="sxs-lookup"><span data-stu-id="ff98b-121">Include [saved searches](../log-analytics/log-analytics-log-searches.md) in a solution tooallow users tooquery data collected by your solution.</span></span>  <span data-ttu-id="ff98b-122">Kaydedilmiş aramaları altında görünür **Sık Kullanılanlar** hello OMS portalında ve **kayıtlı aramaları** hello Azure Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="ff98b-122">Saved searches will appear under **Favorites** in hello OMS portal and **Saved Searches** in hello Azure portal .</span></span>  <span data-ttu-id="ff98b-123">Kaydedilmiş bir aramayı de her uyarı için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="ff98b-123">A saved search is also required for each alert.</span></span>   

<span data-ttu-id="ff98b-124">[Günlük analizi kaydedilen arama](../log-analytics/log-analytics-log-searches.md) kaynaklarınız türü `Microsoft.OperationalInsights/workspaces/savedSearches` ve yapı izlenerek hello sahiptir.</span><span class="sxs-lookup"><span data-stu-id="ff98b-124">[Log Analytics saved search](../log-analytics/log-analytics-log-searches.md) resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches` and have hello following structure.</span></span>  <span data-ttu-id="ff98b-125">Kopyalayabilir ve çözüm dosyanıza Bu kod parçacığını yapıştırın ve hello parametre adlarını değiştirmek için bu ortak değişkenleri ve parametreleri içerir.</span><span class="sxs-lookup"><span data-stu-id="ff98b-125">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
        ],
        "tags": { },
        "properties": {
            "etag": "*",
            "query": "[variables('SavedSearch').Query]",
            "displayName": "[variables('SavedSearch').DisplayName]",
            "category": "[variables('SavedSearch').Category]"
        }
    }



<span data-ttu-id="ff98b-126">Her bir kayıtlı arama hello özelliklerinin aşağıdaki tablonun hello açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="ff98b-126">Each of hello properties of a saved search are described in hello following table.</span></span> 

| <span data-ttu-id="ff98b-127">Özellik</span><span class="sxs-lookup"><span data-stu-id="ff98b-127">Property</span></span> | <span data-ttu-id="ff98b-128">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff98b-128">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ff98b-129">category</span><span class="sxs-lookup"><span data-stu-id="ff98b-129">category</span></span> | <span data-ttu-id="ff98b-130">Merhaba kayıtlı arama Hello kategorisi.</span><span class="sxs-lookup"><span data-stu-id="ff98b-130">hello category for hello saved search.</span></span>  <span data-ttu-id="ff98b-131">Merhaba konsolunda birlikte gruplanır şekilde herhangi aynı çözüm genellikle paylaşacak hello tek bir kategori kayıtlı aramalar.</span><span class="sxs-lookup"><span data-stu-id="ff98b-131">Any saved searches in hello same solution will often share a single category so they are grouped together in hello console.</span></span> |
| <span data-ttu-id="ff98b-132">görünen adı</span><span class="sxs-lookup"><span data-stu-id="ff98b-132">displayname</span></span> | <span data-ttu-id="ff98b-133">Merhaba adı toodisplay hello Portalı'nda arama kaydedildi.</span><span class="sxs-lookup"><span data-stu-id="ff98b-133">Name toodisplay for hello saved search in hello portal.</span></span> |
| <span data-ttu-id="ff98b-134">sorgu</span><span class="sxs-lookup"><span data-stu-id="ff98b-134">query</span></span> | <span data-ttu-id="ff98b-135">Sorgu toorun.</span><span class="sxs-lookup"><span data-stu-id="ff98b-135">Query toorun.</span></span> |

> [!NOTE]
> <span data-ttu-id="ff98b-136">JSON olarak yorumlanabilecek karakterler içeriyorsa toouse kaçış karakterleri hello sorgusunda gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="ff98b-136">You may need toouse escape characters in hello query if it includes characters that could be interpreted as JSON.</span></span>  <span data-ttu-id="ff98b-137">Örneğin, sorgu, **türü: AzureActivity OperationName:"Microsoft.Compute/virtualMachines/write"**, hello Çözüm dosyasındaki yazılmalıdır **türü: AzureActivity işlemadı:\" Microsoft.Compute/virtualMachines/write\"**.</span><span class="sxs-lookup"><span data-stu-id="ff98b-137">For example, if your query was **Type:AzureActivity OperationName:"Microsoft.Compute/virtualMachines/write"**, it should be written in hello solution file as **Type:AzureActivity OperationName:\"Microsoft.Compute/virtualMachines/write\"**.</span></span>

## <a name="alerts"></a><span data-ttu-id="ff98b-138">Uyarılar</span><span class="sxs-lookup"><span data-stu-id="ff98b-138">Alerts</span></span>
<span data-ttu-id="ff98b-139">[Analytics uyarıları oturum](../log-analytics/log-analytics-alerts.md) düzenli aralıklarla kaydedilmiş bir aramayı çalıştırma uyarı kuralları tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ff98b-139">[Log Analytics alerts](../log-analytics/log-analytics-alerts.md) are created by alert rules that run a saved search on a regular interval.</span></span>  <span data-ttu-id="ff98b-140">Merhaba hello sorgunun sonuçlarını belirtilen ölçütlere uyan varsa bir uyarı kaydı oluşturulur ve bir veya daha fazla eylem çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ff98b-140">If hello results of hello query match specified criteria, an alert record is created and one or more actions are run.</span></span>  

<span data-ttu-id="ff98b-141">Bir yönetim çözümüne uyarı kuralları üç farklı kaynaklar aşağıdaki hello yapılır.</span><span class="sxs-lookup"><span data-stu-id="ff98b-141">Alert rules in a management solution are made up of hello following three different resources.</span></span>

- <span data-ttu-id="ff98b-142">**Kayıtlı arama.**</span><span class="sxs-lookup"><span data-stu-id="ff98b-142">**Saved search.**</span></span>  <span data-ttu-id="ff98b-143">Çalıştırılacak hello günlük arama tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ff98b-143">Defines hello log search that will be run.</span></span>  <span data-ttu-id="ff98b-144">Birden çok uyarı kurallarını, tek bir kayıtlı arama paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ff98b-144">Multiple alert rules can share a single saved search.</span></span>
- <span data-ttu-id="ff98b-145">**Zamanlama.**</span><span class="sxs-lookup"><span data-stu-id="ff98b-145">**Schedule.**</span></span>  <span data-ttu-id="ff98b-146">Ne sıklıkta hello günlük arama çalıştırılacak tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ff98b-146">Defines how often hello log search will be run.</span></span>  <span data-ttu-id="ff98b-147">Her uyarı kuralı tek bir zamanlama sahip olur.</span><span class="sxs-lookup"><span data-stu-id="ff98b-147">Each alert rule will have one and only one schedule.</span></span>
- <span data-ttu-id="ff98b-148">**Uyarı eylem.**</span><span class="sxs-lookup"><span data-stu-id="ff98b-148">**Alert action.**</span></span>  <span data-ttu-id="ff98b-149">Her uyarı kuralı bir eylem kaynak türüne sahip olacaktır **uyarı** hello hello ölçütlerini ne zaman bir uyarı kaydı oluşturulur ve uyarının önem derecesi hello gibi hello uyarı ayrıntılarını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ff98b-149">Each alert rule will have one action resource with a type of **Alert** that defines hello details of hello alert such as hello criteria for when an alert record will be created and hello alert's severity.</span></span>  <span data-ttu-id="ff98b-150">Merhaba eylem kaynak isteğe bağlı olarak bir posta ve runbook yanıt tanımlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="ff98b-150">hello action resource will optionally define a mail and runbook response.</span></span>
- <span data-ttu-id="ff98b-151">**Web kancası eylem (isteğe bağlı).**</span><span class="sxs-lookup"><span data-stu-id="ff98b-151">**Webhook action (optional).**</span></span>  <span data-ttu-id="ff98b-152">Merhaba uyarı kuralı, bir Web kancası çağıracaktır sonra başka bir işlem kaynak türüne sahip gerektirir **Web kancası**.</span><span class="sxs-lookup"><span data-stu-id="ff98b-152">If hello alert rule will call a webhook, then it requires an additional action resource with a type of **Webhook**.</span></span>    

<span data-ttu-id="ff98b-153">Kaynaklar, yukarıda açıklanan arama kaydedildi.</span><span class="sxs-lookup"><span data-stu-id="ff98b-153">Saved search resources are described above.</span></span>  <span data-ttu-id="ff98b-154">Merhaba kaynaklar aşağıda açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="ff98b-154">hello other resources are described below.</span></span>


### <a name="schedule-resource"></a><span data-ttu-id="ff98b-155">Zamanlama kaynak</span><span class="sxs-lookup"><span data-stu-id="ff98b-155">Schedule resource</span></span>

<span data-ttu-id="ff98b-156">Kaydedilmiş bir aramayı her zamanlamayı ayrı bir uyarı kuralı temsil eden ile bir veya daha fazla zamanlama olabilir.</span><span class="sxs-lookup"><span data-stu-id="ff98b-156">A saved search can have one or more schedules with each schedule representing a separate alert rule.</span></span> <span data-ttu-id="ff98b-157">Merhaba zamanlama ne sıklıkta hello arama çalıştırılır ve zaman aralığı içinde hangi hello veriler alınır hello tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ff98b-157">hello schedule defines how often hello search is run and hello time interval over which hello data is retrieved.</span></span>  <span data-ttu-id="ff98b-158">Zamanlama kaynaklarınız türü `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/` ve yapı izlenerek hello sahiptir.</span><span class="sxs-lookup"><span data-stu-id="ff98b-158">Schedule resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/` and have hello following structure.</span></span> <span data-ttu-id="ff98b-159">Kopyalayabilir ve çözüm dosyanıza Bu kod parçacığını yapıştırın ve hello parametre adlarını değiştirmek için bu ortak değişkenleri ve parametreleri içerir.</span><span class="sxs-lookup"><span data-stu-id="ff98b-159">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 


    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name)]"
        ],
        "properties": {
            "etag": "*",
            "interval": "[variables('Schedule').Interval]",
            "queryTimeSpan": "[variables('Schedule').TimeSpan]",
            "enabled": "[variables('Schedule').Enabled]"
        }
    }



<span data-ttu-id="ff98b-160">Aşağıdaki tablonun hello zamanlama kaynakların Hello özellikleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ff98b-160">hello properties for schedule resources are described in hello following table.</span></span>

| <span data-ttu-id="ff98b-161">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="ff98b-161">Element name</span></span> | <span data-ttu-id="ff98b-162">Gerekli</span><span class="sxs-lookup"><span data-stu-id="ff98b-162">Required</span></span> | <span data-ttu-id="ff98b-163">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff98b-163">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="ff98b-164">Etkin</span><span class="sxs-lookup"><span data-stu-id="ff98b-164">enabled</span></span>       | <span data-ttu-id="ff98b-165">Evet</span><span class="sxs-lookup"><span data-stu-id="ff98b-165">Yes</span></span> | <span data-ttu-id="ff98b-166">Merhaba uyarı oluşturulduğunda etkinleştirilip etkinleştirilmeyeceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff98b-166">Specifies whether hello alert is enabled when it's created.</span></span> |
| <span data-ttu-id="ff98b-167">interval</span><span class="sxs-lookup"><span data-stu-id="ff98b-167">interval</span></span>      | <span data-ttu-id="ff98b-168">Evet</span><span class="sxs-lookup"><span data-stu-id="ff98b-168">Yes</span></span> | <span data-ttu-id="ff98b-169">Ne sıklıkta hello sorgu dakika içinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="ff98b-169">How often hello query runs in minutes.</span></span> |
| <span data-ttu-id="ff98b-170">QueryTimeSpan</span><span class="sxs-lookup"><span data-stu-id="ff98b-170">queryTimeSpan</span></span> | <span data-ttu-id="ff98b-171">Evet</span><span class="sxs-lookup"><span data-stu-id="ff98b-171">Yes</span></span> | <span data-ttu-id="ff98b-172">Hangi tooevaluate sonuçları üzerinden dakika cinsinden süre uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="ff98b-172">Length of time in minutes over which tooevaluate results.</span></span> |

<span data-ttu-id="ff98b-173">Merhaba zamanlama kaynak hello zamanlama önce oluşturulan kaydedilmiş aramayı hello bağlı.</span><span class="sxs-lookup"><span data-stu-id="ff98b-173">hello schedule resource should depend on hello saved search so that it's created before hello schedule.</span></span>


### <a name="actions"></a><span data-ttu-id="ff98b-174">Eylemler</span><span class="sxs-lookup"><span data-stu-id="ff98b-174">Actions</span></span>
<span data-ttu-id="ff98b-175">Merhaba tarafından belirtilen eylemi kaynak iki tür vardır **türü** özelliği.</span><span class="sxs-lookup"><span data-stu-id="ff98b-175">There are two types of action resource specified by hello **Type** property.</span></span>  <span data-ttu-id="ff98b-176">Bir zamanlama gerektiren **uyarı** hello uyarı kuralı ve bir uyarı oluşturulduğunda, hangi eylemleri alınır hello ayrıntılarını tanımlayan eylem.</span><span class="sxs-lookup"><span data-stu-id="ff98b-176">A schedule requires one **Alert** action which defines hello details of hello alert rule and what actions are taken when an alert is created.</span></span>  <span data-ttu-id="ff98b-177">Ayrıca içerebilir bir **Web kancası** eylem bir Web kancası hello uyarıdan çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ff98b-177">It may also include a **Webhook** action if a webhook should be called from hello alert.</span></span>  

<span data-ttu-id="ff98b-178">Eylem kaynaklarınız türü `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`.</span><span class="sxs-lookup"><span data-stu-id="ff98b-178">Action resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`.</span></span>  

#### <a name="alert-actions"></a><span data-ttu-id="ff98b-179">Uyarı eylemleri</span><span class="sxs-lookup"><span data-stu-id="ff98b-179">Alert actions</span></span>

<span data-ttu-id="ff98b-180">Her biri zaman çizelgeleri **uyarı** eylem.</span><span class="sxs-lookup"><span data-stu-id="ff98b-180">Every schedule will have one **Alert** action.</span></span>  <span data-ttu-id="ff98b-181">Merhaba ayrıntılarını hello uyarı ve isteğe bağlı olarak bildirim ve düzeltme eylemleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ff98b-181">This defines hello details of hello alert and optionally notification and remediation actions.</span></span>  <span data-ttu-id="ff98b-182">Bir e-posta tooone bir bildirim gönderir veya daha fazla adresleri.</span><span class="sxs-lookup"><span data-stu-id="ff98b-182">A notification sends an email tooone or more addresses.</span></span>  <span data-ttu-id="ff98b-183">Bir düzeltme Azure Otomasyonu tooattempt tooremediate algılanan hello sayısındaki bir runbook başlatır.</span><span class="sxs-lookup"><span data-stu-id="ff98b-183">A remediation starts a runbook in Azure Automation tooattempt tooremediate hello detected issue.</span></span>

<span data-ttu-id="ff98b-184">Uyarı eylemleri yapı izlenerek hello vardır.</span><span class="sxs-lookup"><span data-stu-id="ff98b-184">Alert actions have hello following structure.</span></span>  <span data-ttu-id="ff98b-185">Kopyalayabilir ve çözüm dosyanıza Bu kod parçacığını yapıştırın ve hello parametre adlarını değiştirmek için bu ortak değişkenleri ve parametreleri içerir.</span><span class="sxs-lookup"><span data-stu-id="ff98b-185">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 



    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name, '/', variables('Alert').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name, '/schedules/', variables('Schedule').Name)]"
        ],
        "properties": {
            "etag": "*",
            "type": "Alert",
            "name": "[variables('Alert').Name]",
            "description": "[variables('Alert').Description]",
            "severity": "[variables('Alert').Severity]",
            "threshold": {
                "operator": "[variables('Alert').Threshold.Operator]",
                "value": "[variables('Alert').Threshold.Value]",
                "metricsTrigger": {
                    "triggerCondition": "[variables('Alert').Threshold.Trigger.Condition]",
                    "operator": "[variables('Alert').Trigger.Operator]",
                    "value": "[variables('Alert').Trigger.Value]"
                },
            },
            "emailNotification": {
                "recipients": [
                    "[variables('Alert').Recipients]"
                ],
                "subject": "[variables('Alert').Subject]"
            },
            "remediation": {
                "runbookName": "[variables('Alert').Remedition.RunbookName]",
                "webhookUri": "[variables('Alert').Remedition.WebhookUri]"
            }
        }
    }

<span data-ttu-id="ff98b-186">Uyarı eylemi kaynakların Hello özellikleri tabloları aşağıdaki hello açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ff98b-186">hello properties for Alert action resources are described in hello following tables.</span></span>

| <span data-ttu-id="ff98b-187">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="ff98b-187">Element name</span></span> | <span data-ttu-id="ff98b-188">Gerekli</span><span class="sxs-lookup"><span data-stu-id="ff98b-188">Required</span></span> | <span data-ttu-id="ff98b-189">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff98b-189">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="ff98b-190">Tür</span><span class="sxs-lookup"><span data-stu-id="ff98b-190">Type</span></span> | <span data-ttu-id="ff98b-191">Evet</span><span class="sxs-lookup"><span data-stu-id="ff98b-191">Yes</span></span> | <span data-ttu-id="ff98b-192">Merhaba eylem türü.</span><span class="sxs-lookup"><span data-stu-id="ff98b-192">Type of hello action.</span></span>  <span data-ttu-id="ff98b-193">Bu **uyarı** uyarı eylemleri için.</span><span class="sxs-lookup"><span data-stu-id="ff98b-193">This will be **Alert** for alert actions.</span></span> |
| <span data-ttu-id="ff98b-194">Ad</span><span class="sxs-lookup"><span data-stu-id="ff98b-194">Name</span></span> | <span data-ttu-id="ff98b-195">Evet</span><span class="sxs-lookup"><span data-stu-id="ff98b-195">Yes</span></span> | <span data-ttu-id="ff98b-196">Merhaba uyarı görünen adı.</span><span class="sxs-lookup"><span data-stu-id="ff98b-196">Display name for hello alert.</span></span>  <span data-ttu-id="ff98b-197">Bu hello uyarı kuralı için başlangıç konsolunda görüntülenen hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="ff98b-197">This is hello name that's displayed in hello console for hello alert rule.</span></span> |
| <span data-ttu-id="ff98b-198">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff98b-198">Description</span></span> | <span data-ttu-id="ff98b-199">Hayır</span><span class="sxs-lookup"><span data-stu-id="ff98b-199">No</span></span> | <span data-ttu-id="ff98b-200">Merhaba uyarı isteğe bağlı bir açıklama.</span><span class="sxs-lookup"><span data-stu-id="ff98b-200">Optional description of hello alert.</span></span> |
| <span data-ttu-id="ff98b-201">Önem Derecesi</span><span class="sxs-lookup"><span data-stu-id="ff98b-201">Severity</span></span> | <span data-ttu-id="ff98b-202">Evet</span><span class="sxs-lookup"><span data-stu-id="ff98b-202">Yes</span></span> | <span data-ttu-id="ff98b-203">Önem derecesi değerlerini aşağıdaki hello uyarı kaydından hello:</span><span class="sxs-lookup"><span data-stu-id="ff98b-203">Severity of hello alert record from hello following values:</span></span><br><br> <span data-ttu-id="ff98b-204">**Kritik**</span><span class="sxs-lookup"><span data-stu-id="ff98b-204">**Critical**</span></span><br><span data-ttu-id="ff98b-205">**Uyarı**</span><span class="sxs-lookup"><span data-stu-id="ff98b-205">**Warning**</span></span><br><span data-ttu-id="ff98b-206">**Bilgilendirme**</span><span class="sxs-lookup"><span data-stu-id="ff98b-206">**Informational**</span></span> |


##### <a name="threshold"></a><span data-ttu-id="ff98b-207">Eşik</span><span class="sxs-lookup"><span data-stu-id="ff98b-207">Threshold</span></span>
<span data-ttu-id="ff98b-208">Bu bölüm gereklidir.</span><span class="sxs-lookup"><span data-stu-id="ff98b-208">This section is required.</span></span>  <span data-ttu-id="ff98b-209">Merhaba uyarı eşiği hello özelliklerini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ff98b-209">It defines hello properties for hello alert threshold.</span></span>

| <span data-ttu-id="ff98b-210">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="ff98b-210">Element name</span></span> | <span data-ttu-id="ff98b-211">Gerekli</span><span class="sxs-lookup"><span data-stu-id="ff98b-211">Required</span></span> | <span data-ttu-id="ff98b-212">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff98b-212">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="ff98b-213">işleci</span><span class="sxs-lookup"><span data-stu-id="ff98b-213">Operator</span></span> | <span data-ttu-id="ff98b-214">Evet</span><span class="sxs-lookup"><span data-stu-id="ff98b-214">Yes</span></span> | <span data-ttu-id="ff98b-215">Değerleri aşağıdaki hello hello karşılaştırmadan işleci:</span><span class="sxs-lookup"><span data-stu-id="ff98b-215">Operator for hello comparison from hello following values:</span></span><br><br><span data-ttu-id="ff98b-216">**gt büyük =<br>lt = küçüktür**</span><span class="sxs-lookup"><span data-stu-id="ff98b-216">**gt = greater than<br>lt = less than**</span></span> |
| <span data-ttu-id="ff98b-217">Değer</span><span class="sxs-lookup"><span data-stu-id="ff98b-217">Value</span></span> | <span data-ttu-id="ff98b-218">Evet</span><span class="sxs-lookup"><span data-stu-id="ff98b-218">Yes</span></span> | <span data-ttu-id="ff98b-219">Merhaba değeri toocompare hello sonuçları.</span><span class="sxs-lookup"><span data-stu-id="ff98b-219">hello value toocompare hello results.</span></span> |


##### <a name="metricstrigger"></a><span data-ttu-id="ff98b-220">MetricsTrigger</span><span class="sxs-lookup"><span data-stu-id="ff98b-220">MetricsTrigger</span></span>
<span data-ttu-id="ff98b-221">Bu bölümde isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="ff98b-221">This section is optional.</span></span>  <span data-ttu-id="ff98b-222">Bir ölçüm ölçüm uyarı içerir.</span><span class="sxs-lookup"><span data-stu-id="ff98b-222">Include it for a metric measurement alert.</span></span>

> [!NOTE]
> <span data-ttu-id="ff98b-223">Ölçüm ölçüm uyarılar şu anda genel önizlemede.</span><span class="sxs-lookup"><span data-stu-id="ff98b-223">Metric measurement alerts are currently in public preview.</span></span> 

| <span data-ttu-id="ff98b-224">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="ff98b-224">Element name</span></span> | <span data-ttu-id="ff98b-225">Gerekli</span><span class="sxs-lookup"><span data-stu-id="ff98b-225">Required</span></span> | <span data-ttu-id="ff98b-226">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff98b-226">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="ff98b-227">TriggerCondition</span><span class="sxs-lookup"><span data-stu-id="ff98b-227">TriggerCondition</span></span> | <span data-ttu-id="ff98b-228">Evet</span><span class="sxs-lookup"><span data-stu-id="ff98b-228">Yes</span></span> | <span data-ttu-id="ff98b-229">Merhaba Eşik ihlallerini veya değerleri aşağıdaki hello gelen ardışık ihlallerini toplam sayısını olup olmadığını belirtir:</span><span class="sxs-lookup"><span data-stu-id="ff98b-229">Specifies whether hello threshold is for total number of breaches or consecutive breaches from hello following values:</span></span><br><br><span data-ttu-id="ff98b-230">**Toplam<br>ardışık**</span><span class="sxs-lookup"><span data-stu-id="ff98b-230">**Total<br>Consecutive**</span></span> |
| <span data-ttu-id="ff98b-231">işleci</span><span class="sxs-lookup"><span data-stu-id="ff98b-231">Operator</span></span> | <span data-ttu-id="ff98b-232">Evet</span><span class="sxs-lookup"><span data-stu-id="ff98b-232">Yes</span></span> | <span data-ttu-id="ff98b-233">Değerleri aşağıdaki hello hello karşılaştırmadan işleci:</span><span class="sxs-lookup"><span data-stu-id="ff98b-233">Operator for hello comparison from hello following values:</span></span><br><br><span data-ttu-id="ff98b-234">**gt büyük =<br>lt = küçüktür**</span><span class="sxs-lookup"><span data-stu-id="ff98b-234">**gt = greater than<br>lt = less than**</span></span> |
| <span data-ttu-id="ff98b-235">Değer</span><span class="sxs-lookup"><span data-stu-id="ff98b-235">Value</span></span> | <span data-ttu-id="ff98b-236">Evet</span><span class="sxs-lookup"><span data-stu-id="ff98b-236">Yes</span></span> | <span data-ttu-id="ff98b-237">Hello ölçütleri kez hello sayısı ölç tootrigger hello uyarı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ff98b-237">Number of hello times hello criteria must be met tootrigger hello alert.</span></span> |

##### <a name="throttling"></a><span data-ttu-id="ff98b-238">Azaltma</span><span class="sxs-lookup"><span data-stu-id="ff98b-238">Throttling</span></span>
<span data-ttu-id="ff98b-239">Bu bölümde isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="ff98b-239">This section is optional.</span></span>  <span data-ttu-id="ff98b-240">Toosuppress uyarılardan aynı bazı süreyi bir uyarı oluşturulduktan sonra için kural hello istiyorsanız bu bölümü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ff98b-240">Include this section if you want toosuppress alerts from hello same rule for some amount of time after an alert is created.</span></span>

| <span data-ttu-id="ff98b-241">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="ff98b-241">Element name</span></span> | <span data-ttu-id="ff98b-242">Gerekli</span><span class="sxs-lookup"><span data-stu-id="ff98b-242">Required</span></span> | <span data-ttu-id="ff98b-243">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff98b-243">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="ff98b-244">Dakika Cinsiden Süre</span><span class="sxs-lookup"><span data-stu-id="ff98b-244">DurationInMinutes</span></span> | <span data-ttu-id="ff98b-245">Dahil edilen öğesi azaltma, Evet</span><span class="sxs-lookup"><span data-stu-id="ff98b-245">Yes if Throttling element included</span></span> | <span data-ttu-id="ff98b-246">Aynı uyarı kuralı oluşturulan dakika toosuppress uyarıların hello birinden sonra sayısı.</span><span class="sxs-lookup"><span data-stu-id="ff98b-246">Number of minutes toosuppress alerts after one from hello same alert rule is created.</span></span> |

##### <a name="emailnotification"></a><span data-ttu-id="ff98b-247">EmailNotification</span><span class="sxs-lookup"><span data-stu-id="ff98b-247">EmailNotification</span></span>
 <span data-ttu-id="ff98b-248">Bu bölüm, bunu istiyorsanız hello uyarı toosend posta tooone ya da daha fazla alıcı isteğe bağlı dahil değildir.</span><span class="sxs-lookup"><span data-stu-id="ff98b-248">This section is optional  Include it if you want hello alert toosend mail tooone or more recipients.</span></span>

| <span data-ttu-id="ff98b-249">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="ff98b-249">Element name</span></span> | <span data-ttu-id="ff98b-250">Gerekli</span><span class="sxs-lookup"><span data-stu-id="ff98b-250">Required</span></span> | <span data-ttu-id="ff98b-251">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff98b-251">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="ff98b-252">Alıcıları</span><span class="sxs-lookup"><span data-stu-id="ff98b-252">Recipients</span></span> | <span data-ttu-id="ff98b-253">Evet</span><span class="sxs-lookup"><span data-stu-id="ff98b-253">Yes</span></span> | <span data-ttu-id="ff98b-254">Bir uyarı gibi aşağıdaki örneğine hello oluşturulduğunda e-posta virgülle ayrılmış listesini toosend bildirim giderir.</span><span class="sxs-lookup"><span data-stu-id="ff98b-254">Comma delimited list of email addresses toosend notification when an alert is created such as in hello following example.</span></span><br><br><span data-ttu-id="ff98b-255">**[ "recipient1@contoso.com", "recipient2@contoso.com" ]**</span><span class="sxs-lookup"><span data-stu-id="ff98b-255">**[ "recipient1@contoso.com", "recipient2@contoso.com" ]**</span></span> |
| <span data-ttu-id="ff98b-256">Konu</span><span class="sxs-lookup"><span data-stu-id="ff98b-256">Subject</span></span> | <span data-ttu-id="ff98b-257">Evet</span><span class="sxs-lookup"><span data-stu-id="ff98b-257">Yes</span></span> | <span data-ttu-id="ff98b-258">Merhaba posta konu satırı.</span><span class="sxs-lookup"><span data-stu-id="ff98b-258">Subject line of hello mail.</span></span> |
| <span data-ttu-id="ff98b-259">Eki</span><span class="sxs-lookup"><span data-stu-id="ff98b-259">Attachment</span></span> | <span data-ttu-id="ff98b-260">Hayır</span><span class="sxs-lookup"><span data-stu-id="ff98b-260">No</span></span> | <span data-ttu-id="ff98b-261">Ekleri şu anda desteklenmemektedir.</span><span class="sxs-lookup"><span data-stu-id="ff98b-261">Attachments are not currently supported.</span></span>  <span data-ttu-id="ff98b-262">Bu öğe dahil ise olmalıdır **hiçbiri**.</span><span class="sxs-lookup"><span data-stu-id="ff98b-262">If this element is included, it should be **None**.</span></span> |


##### <a name="remediation"></a><span data-ttu-id="ff98b-263">Düzeltme</span><span class="sxs-lookup"><span data-stu-id="ff98b-263">Remediation</span></span>
<span data-ttu-id="ff98b-264">Bu bölümde isteğe bağlı bir runbook toostart yanıt toohello uyarısında istiyorsanız ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ff98b-264">This section is optional  Include it if you want a runbook toostart in response toohello alert.</span></span> |

| <span data-ttu-id="ff98b-265">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="ff98b-265">Element name</span></span> | <span data-ttu-id="ff98b-266">Gerekli</span><span class="sxs-lookup"><span data-stu-id="ff98b-266">Required</span></span> | <span data-ttu-id="ff98b-267">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff98b-267">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="ff98b-268">RunbookName</span><span class="sxs-lookup"><span data-stu-id="ff98b-268">RunbookName</span></span> | <span data-ttu-id="ff98b-269">Evet</span><span class="sxs-lookup"><span data-stu-id="ff98b-269">Yes</span></span> | <span data-ttu-id="ff98b-270">Merhaba runbook toostart adı.</span><span class="sxs-lookup"><span data-stu-id="ff98b-270">Name of hello runbook toostart.</span></span> |
| <span data-ttu-id="ff98b-271">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="ff98b-271">WebhookUri</span></span> | <span data-ttu-id="ff98b-272">Evet</span><span class="sxs-lookup"><span data-stu-id="ff98b-272">Yes</span></span> | <span data-ttu-id="ff98b-273">Merhaba Web kancası hello runbook için URI.</span><span class="sxs-lookup"><span data-stu-id="ff98b-273">Uri of hello webhook for hello runbook.</span></span> |
| <span data-ttu-id="ff98b-274">Süre sonu</span><span class="sxs-lookup"><span data-stu-id="ff98b-274">Expiry</span></span> | <span data-ttu-id="ff98b-275">Hayır</span><span class="sxs-lookup"><span data-stu-id="ff98b-275">No</span></span> | <span data-ttu-id="ff98b-276">Tarih ve saat düzeltme hello süresi dolar.</span><span class="sxs-lookup"><span data-stu-id="ff98b-276">Date and time that hello remediation expires.</span></span> |

#### <a name="webhook-actions"></a><span data-ttu-id="ff98b-277">Web kancası eylemleri</span><span class="sxs-lookup"><span data-stu-id="ff98b-277">Webhook actions</span></span>

<span data-ttu-id="ff98b-278">Web kancası eylemleri, bir URL çağırma ve isteğe bağlı olarak gönderilen bir yükü toobe sağlayan bir işlem başlatın.</span><span class="sxs-lookup"><span data-stu-id="ff98b-278">Webhook actions start a process by calling a URL and optionally providing a payload toobe sent.</span></span> <span data-ttu-id="ff98b-279">Azure Otomasyon çalışma kitabı dışındaki işlemler çağırabilir Web kancası için amacı dışında benzer tooRemediation Eylemler oldukları.</span><span class="sxs-lookup"><span data-stu-id="ff98b-279">They are similar tooRemediation actions except they are meant for webhooks that may invoke processes other than Azure Automation runbooks.</span></span> <span data-ttu-id="ff98b-280">Yükü teslim toobe toohello uzak bir işlem sağlayarak hello ek bir seçeneğiniz de sağlar.</span><span class="sxs-lookup"><span data-stu-id="ff98b-280">They also provide hello additional option of providing a payload toobe delivered toohello remote process.</span></span>

<span data-ttu-id="ff98b-281">Uyarınız bir Web kancası çağırır sonra bir eylem kaynak türüne sahip gerekir **Web kancası** toplama toohello içinde **uyarı** eylem kaynak.</span><span class="sxs-lookup"><span data-stu-id="ff98b-281">If your alert will call a webhook, then it will need an action resource with a type of **Webhook** in addition toohello **Alert** action resource.</span></span>  

    {
      "name": "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name, '/', variables('Webhook').Name)]",
      "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions/",
      "apiVersion": "[variables('LogAnalyticsApiVersion')]",
      "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name, '/schedules/', variables('Schedule').Name)]"
      ],
      "properties": {
        "etag": "*",
        "type": "[variables('Alert').Webhook.Type]",
        "name": "[variables('Alert').Webhook.Name]",
        "webhookUri": "[variables('Alert').Webhook.webhookUri]",
        "customPayload": "[variables('Alert').Webhook.CustomPayLoad]"
      }
    }

<span data-ttu-id="ff98b-282">Web kancası eylem kaynakların Hello özellikleri tabloları aşağıdaki hello açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ff98b-282">hello properties for Webhook action resources are described in hello following tables.</span></span>

| <span data-ttu-id="ff98b-283">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="ff98b-283">Element name</span></span> | <span data-ttu-id="ff98b-284">Gerekli</span><span class="sxs-lookup"><span data-stu-id="ff98b-284">Required</span></span> | <span data-ttu-id="ff98b-285">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff98b-285">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="ff98b-286">type</span><span class="sxs-lookup"><span data-stu-id="ff98b-286">type</span></span> | <span data-ttu-id="ff98b-287">Evet</span><span class="sxs-lookup"><span data-stu-id="ff98b-287">Yes</span></span> | <span data-ttu-id="ff98b-288">Merhaba eylem türü.</span><span class="sxs-lookup"><span data-stu-id="ff98b-288">Type of hello action.</span></span>  <span data-ttu-id="ff98b-289">Bu **Web kancası** Web kancası eylemleri için.</span><span class="sxs-lookup"><span data-stu-id="ff98b-289">This will be **Webhook** for webhook actions.</span></span> |
| <span data-ttu-id="ff98b-290">ad</span><span class="sxs-lookup"><span data-stu-id="ff98b-290">name</span></span> | <span data-ttu-id="ff98b-291">Evet</span><span class="sxs-lookup"><span data-stu-id="ff98b-291">Yes</span></span> | <span data-ttu-id="ff98b-292">Merhaba eylem görünen adı.</span><span class="sxs-lookup"><span data-stu-id="ff98b-292">Display name for hello action.</span></span>  <span data-ttu-id="ff98b-293">Bu hello konsolunda görüntülenmez.</span><span class="sxs-lookup"><span data-stu-id="ff98b-293">This is not displayed in hello console.</span></span> |
| <span data-ttu-id="ff98b-294">wehookUri</span><span class="sxs-lookup"><span data-stu-id="ff98b-294">wehookUri</span></span> | <span data-ttu-id="ff98b-295">Evet</span><span class="sxs-lookup"><span data-stu-id="ff98b-295">Yes</span></span> | <span data-ttu-id="ff98b-296">Merhaba Web kancası için URI.</span><span class="sxs-lookup"><span data-stu-id="ff98b-296">Uri for hello webhook.</span></span> |
| <span data-ttu-id="ff98b-297">CustomPayload</span><span class="sxs-lookup"><span data-stu-id="ff98b-297">customPayload</span></span> | <span data-ttu-id="ff98b-298">Hayır</span><span class="sxs-lookup"><span data-stu-id="ff98b-298">No</span></span> | <span data-ttu-id="ff98b-299">Özel yük toobe toohello Web kancası gönderdi.</span><span class="sxs-lookup"><span data-stu-id="ff98b-299">Custom payload toobe sent toohello webhook.</span></span> <span data-ttu-id="ff98b-300">Merhaba biçimi hangi hello Web kancası bekleniyor bağlı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="ff98b-300">hello format will depend on what hello webhook is expecting.</span></span> |




## <a name="sample"></a><span data-ttu-id="ff98b-301">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff98b-301">Sample</span></span>

<span data-ttu-id="ff98b-302">Aşağıdaki kaynakları izleyerek hello içeren içeren bir çözüm örneğidir:</span><span class="sxs-lookup"><span data-stu-id="ff98b-302">Following is a sample of a solution that include that includes hello following resources:</span></span>

- <span data-ttu-id="ff98b-303">Kayıtlı arama</span><span class="sxs-lookup"><span data-stu-id="ff98b-303">Saved search</span></span>
- <span data-ttu-id="ff98b-304">Zamanlama</span><span class="sxs-lookup"><span data-stu-id="ff98b-304">Schedule</span></span>
- <span data-ttu-id="ff98b-305">Uyarı eylemi</span><span class="sxs-lookup"><span data-stu-id="ff98b-305">Alert action</span></span>
- <span data-ttu-id="ff98b-306">Web kancası eylemi</span><span class="sxs-lookup"><span data-stu-id="ff98b-306">Webhook action</span></span>

<span data-ttu-id="ff98b-307">Merhaba örnek kullanır [standart çözüm parametreleri](operations-management-suite-solutions-solution-file.md#parameters) bir çözüm olarak, yaygın olarak kullanılacak değişkenleri toohardcoding değerleri hello kaynak tanımlarında değil.</span><span class="sxs-lookup"><span data-stu-id="ff98b-307">hello sample uses [standard solution parameters](operations-management-suite-solutions-solution-file.md#parameters) variables that would commonly be used in a solution as opposed toohardcoding values in hello resource definitions.</span></span>

    {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0",
        "parameters": {
          "workspaceName": {
            "type": "string",
            "metadata": {
              "Description": "Name of Log Analytics workspace"
            }
          },
          "accountName": {
            "type": "string",
            "metadata": {
              "Description": "Name of Automation account"
            }
          },
          "workspaceregionId": {
            "type": "string",
            "metadata": {
              "Description": "Region of Log Analytics workspace"
            }
          },
          "regionId": {
            "type": "string",
            "metadata": {
              "Description": "Region of Automation account"
            }
          },
          "pricingTier": {
            "type": "string",
            "metadata": {
              "Description": "Pricing tier of both Log Analytics workspace and Azure Automation account"
            }
          },
          "recipients": {
            "type": "string",
            "metadata": {
              "Description": "List of recipients for hello email alert separated by semicolon"
            }
          }
        },
        "variables": {
          "SolutionName": "MySolution",
          "SolutionVersion": "1.0",
          "SolutionPublisher": "Contoso",
          "ProductName": "SampleSolution",
    
          "LogAnalyticsApiVersion": "2015-11-01-preview",
    
          "MySearch": {
            "displayName": "Error records by hour",
            "query": "Type=MyRecord_CL | measure avg(Rating_d) by Instance_s interval 60minutes",
            "category": "Samples",
            "name": "Samples-Count of data"
          },
          "MyAlert": {
            "Name": "[toLower(concat('myalert-',uniqueString(resourceGroup().id, deployment().name)))]",
            "DisplayName": "My alert rule",
            "Description": "Sample alert.  Fires when 3 error records found over hour interval.",
            "Severity": "Critical",
            "ThresholdOperator": "gt",
            "ThresholdValue": 3,
            "Schedule": {
              "Name": "[toLower(concat('myschedule-',uniqueString(resourceGroup().id, deployment().name)))]",
              "Interval": 15,
              "TimeSpan": 60
            },
            "MetricsTrigger": {
              "TriggerCondition": "Consecutive",
              "Operator": "gt",
              "Value": 3
            },
            "ThrottleMinutes": 60,
            "Notification": {
              "Recipients": [
                "[parameters('recipients')]"
              ],
              "Subject": "Sample alert"
            },
            "Remediation": {
              "RunbookName": "MyRemediationRunbook",
              "WebhookUri": "https://s1events.azure-automation.net/webhooks?token=TluBFH3GpX4IEAnFoImoAWLTULkjD%2bTS0yscyrr7ogw%3d"
            },
            "Webhook": {
              "Name": "MyWebhook",
              "Uri": "https://MyService.com/webhook",
              "Payload": "{\"field1\":\"value1\",\"field2\":\"value2\"}"
            }
          }
        },
        "resources": [
          {
            "name": "[concat(variables('SolutionName'), '[' ,parameters('workspacename'), ']')]",
            "location": "[parameters('workspaceRegionId')]",
            "tags": { },
            "type": "Microsoft.OperationsManagement/solutions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches', parameters('workspacename'), variables('MySearch').Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Webhook.Name)]"
            ],
            "properties": {
              "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
              "referencedResources": [
              ],
              "containedResources": [
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches', parameters('workspacename'), variables('MySearch').Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Webhook.Name)]"
              ]
            },
            "plan": {
              "name": "[concat(variables('SolutionName'), '[' ,parameters('workspaceName'), ']')]",
              "Version": "[variables('SolutionVersion')]",
              "product": "[variables('ProductName')]",
              "publisher": "[variables('SolutionPublisher')]",
              "promotionCode": ""
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [ ],
            "tags": { },
            "properties": {
              "etag": "*",
              "query": "[variables('MySearch').query]",
              "displayName": "[variables('MySearch').displayName]",
              "category": "[variables('MySearch').category]"
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/', variables('MyAlert').Schedule.Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name)]"
            ],
            "properties": {
              "etag": "*",
              "interval": "[variables('MyAlert').Schedule.Interval]",
              "queryTimeSpan": "[variables('MyAlert').Schedule.TimeSpan]",
              "enabled": true
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/',  variables('MyAlert').Schedule.Name, '/',  variables('MyAlert').Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/',  variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name)]"
            ],
            "properties": {
              "etag": "*",
              "Type": "Alert",
              "Name": "[variables('MyAlert').DisplayName]",
              "Description": "[variables('MyAlert').Description]",
              "Severity": "[variables('MyAlert').Severity]",
              "Threshold": {
                "Operator": "[variables('MyAlert').ThresholdOperator]",
                "Value": "[variables('MyAlert').ThresholdValue]",
                "MetricsTrigger": {
                  "TriggerCondition": "[variables('MyAlert').MetricsTrigger.TriggerCondition]",
                  "Operator": "[variables('MyAlert').MetricsTrigger.Operator]",
                  "Value": "[variables('MyAlert').MetricsTrigger.Value]"
                }
              },
              "Throttling": {
                "DurationInMinutes": "[variables('MyAlert').ThrottleMinutes]"
              },
              "EmailNotification": {
                "Recipients": "[variables('MyAlert').Notification.Recipients]",
                "Subject": "[variables('MyAlert').Notification.Subject]",
                "Attachment": "None"
              },
              "Remediation": {
                "RunbookName": "[variables('MyAlert').Remediation.RunbookName]",
                "WebhookUri": "[variables('MyAlert').Remediation.WebhookUri]"
              }
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/', variables('MyAlert').Schedule.Name, '/', variables('MyAlert').Webhook.Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name)]",
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name, '/actions/',variables('MyAlert').Name)]"
            ],
            "properties": {
              "etag": "*",
              "Type": "Webhook",
              "Name": "[variables('MyAlert').Webhook.Name]",
              "WebhookUri": "[variables('MyAlert').Webhook.Uri]",
              "CustomPayload": "[variables('MyAlert').Webhook.Payload]"
            }
          }
        ]
    }


<span data-ttu-id="ff98b-308">Aşağıdaki parametre dosyasına hello örnekleri değerleri için bu çözümü sağlar.</span><span class="sxs-lookup"><span data-stu-id="ff98b-308">hello following parameter file provides samples values for this solution.</span></span>

    {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "workspacename": {
                "value": "myWorkspace"
            },
            "accountName": {
                "value": "myAccount"
            },
            "workspaceregionId": {
                "value": "East US"
            },
            "regionId": {
                "value": "East US 2"
            },
            "pricingTier": {
                "value": "Free"
            },
            "recipients": {
                "value": "recipient1@contoso.com;recipient2@contoso.com"
            }
        }
    }


## <a name="next-steps"></a><span data-ttu-id="ff98b-309">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ff98b-309">Next steps</span></span>
* <span data-ttu-id="ff98b-310">[Görünümler ekleme](operations-management-suite-solutions-resources-views.md) tooyour yönetim çözümü.</span><span class="sxs-lookup"><span data-stu-id="ff98b-310">[Add views](operations-management-suite-solutions-resources-views.md) tooyour management solution.</span></span>
* <span data-ttu-id="ff98b-311">[Otomasyon runbook'ları ve diğer kaynakları eklemek](operations-management-suite-solutions-resources-automation.md) tooyour yönetim çözümü.</span><span class="sxs-lookup"><span data-stu-id="ff98b-311">[Add Automation runbooks and other resources](operations-management-suite-solutions-resources-automation.md) tooyour management solution.</span></span>

