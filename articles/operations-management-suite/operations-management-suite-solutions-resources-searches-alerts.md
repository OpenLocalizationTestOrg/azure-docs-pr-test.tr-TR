---
title: "OMS çözümlerinde Kaydedilmiş aramaları ve Uyarıları | Microsoft Docs"
description: "OMS çözümlerinde genellikle Kaydedilmiş aramaları çözümü tarafından toplanan verileri çözümlemek için günlük analizi de içerir.  Ayrıca kullanıcıya bildirmek için uyarılar tanımlayın olabilir veya otomatik olarak yanıt kritik bir sorun için adımları uygulayın.  Bu makalede, günlük yönetim çözümlerine dahil şekilde bir ARM şablonu Kaydedilmiş aramaları ve Uyarıları analizi tanımlamak açıklar."
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
ms.openlocfilehash: 21c42a747a08c5386c65d10190baf0054a7adef8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="adding-log-analytics-saved-searches-and-alerts-to-oms-management-solution-preview"></a><span data-ttu-id="b0179-105">Günlük analizi ekleme arar ve Uyarıları kaydedilmiş OMS yönetim çözümü (Önizleme)</span><span class="sxs-lookup"><span data-stu-id="b0179-105">Adding Log Analytics saved searches and alerts to OMS management solution (Preview)</span></span>

> [!NOTE]
> <span data-ttu-id="b0179-106">Bu, şu anda önizlemede OMS yönetim çözümleri oluşturmak için başlangıç belgesidir.</span><span class="sxs-lookup"><span data-stu-id="b0179-106">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="b0179-107">Aşağıda açıklanan herhangi bir şema değiştirilebilir ' dir.</span><span class="sxs-lookup"><span data-stu-id="b0179-107">Any schema described below is subject to change.</span></span>   


<span data-ttu-id="b0179-108">[OMS yönetim çözümlerine](operations-management-suite-solutions.md) genellikle içerecektir [kayıtlı aramalar](../log-analytics/log-analytics-log-searches.md) çözümü tarafından toplanan verileri çözümlemek için günlük analizi içinde.</span><span class="sxs-lookup"><span data-stu-id="b0179-108">[Management solutions in OMS](operations-management-suite-solutions.md) will typically include [saved searches](../log-analytics/log-analytics-log-searches.md) in Log Analytics to analyze data collected by the solution.</span></span>  <span data-ttu-id="b0179-109">Ayrıca tanımlayabilir [uyarıları](../log-analytics/log-analytics-alerts.md) kullanıcıya bildir veya otomatik olarak yanıt kritik bir sorun için adımları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="b0179-109">They may also define [alerts](../log-analytics/log-analytics-alerts.md) to notify the user or automatically take action in response to a critical issue.</span></span>  <span data-ttu-id="b0179-110">Bu makalede nasıl günlük kayıtlı aramalar analizi tanımlayacağınızı açıklar ve Uyarıları gelen bir [kaynak yönetimi şablonu](../resource-manager-template-walkthrough.md) içinde eklenebilir şekilde [yönetim çözümleri](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="b0179-110">This article describes how to define Log Analytics saved searches and alerts in a [Resource Management template](../resource-manager-template-walkthrough.md) so they can be included in [management solutions](operations-management-suite-solutions-creating.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b0179-111">Bu makaledeki örnekler parametreleri ve gerekli olduğunu veya yönetim çözümleri için ortak olduğunu ve açıklanan değişkenleri kullanma [Operations Management Suite (OMS) yönetimi çözümleri oluşturma](operations-management-suite-solutions-creating.md)</span><span class="sxs-lookup"><span data-stu-id="b0179-111">The samples in this article use parameters and variables that are either required or common to management solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="b0179-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b0179-112">Prerequisites</span></span>
<span data-ttu-id="b0179-113">Bu makale, zaten nasıl hakkında bilgi sahibi olduğunuzu varsayar [bir yönetim çözümü oluşturma](operations-management-suite-solutions-creating.md) ve yapısı bir [ARM şablonu](../resource-group-authoring-templates.md) ve çözüm dosya.</span><span class="sxs-lookup"><span data-stu-id="b0179-113">This article assumes that you're already familiar with how to [create a management solution](operations-management-suite-solutions-creating.md) and the structure of an [ARM template](../resource-group-authoring-templates.md) and solution file.</span></span>


## <a name="log-analytics-workspace"></a><span data-ttu-id="b0179-114">Günlük analizi çalışma alanı</span><span class="sxs-lookup"><span data-stu-id="b0179-114">Log Analytics Workspace</span></span>
<span data-ttu-id="b0179-115">Günlük analizi tüm kaynaklarında bulunan bir [çalışma](../log-analytics/log-analytics-manage-access.md).</span><span class="sxs-lookup"><span data-stu-id="b0179-115">All resources in Log Analytics are contained in a [workspace](../log-analytics/log-analytics-manage-access.md).</span></span>  <span data-ttu-id="b0179-116">Bölümünde açıklandığı gibi [OMS çalışma ve Automation hesabı](operations-management-suite-solutions.md#oms-workspace-and-automation-account) çalışma yönetimi çözümünde dahil değildir ancak çözüm yüklenmeden önce mevcut olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b0179-116">As described in [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) the workspace isn't included in the management solution but must exist before the solution is installed.</span></span>  <span data-ttu-id="b0179-117">Kullanılabilir değilse, çözüm yükleme başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="b0179-117">If it isn't available, then the solution install will fail.</span></span>

<span data-ttu-id="b0179-118">Her günlük analizi kaynak adına çalışma adıdır.</span><span class="sxs-lookup"><span data-stu-id="b0179-118">The name of the workspace is in the name of each Log Analytics resource.</span></span>  <span data-ttu-id="b0179-119">Bu çözümle yapılır **çalışma** savedsearch kaynak aşağıdaki örnekteki gibi parametre.</span><span class="sxs-lookup"><span data-stu-id="b0179-119">This is done in the solution with the **workspace** parameter as in the following example of a savedsearch resource.</span></span>

    "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearchId'))]"


## <a name="saved-searches"></a><span data-ttu-id="b0179-120">Kaydedilen aramalar</span><span class="sxs-lookup"><span data-stu-id="b0179-120">Saved Searches</span></span>
<span data-ttu-id="b0179-121">Dahil [kayıtlı aramalar](../log-analytics/log-analytics-log-searches.md) çözümünüz tarafından toplanan sorgu veri kullanıcılarına izin vermek için bir çözüm içinde.</span><span class="sxs-lookup"><span data-stu-id="b0179-121">Include [saved searches](../log-analytics/log-analytics-log-searches.md) in a solution to allow users to query data collected by your solution.</span></span>  <span data-ttu-id="b0179-122">Kaydedilmiş aramaları altında görünür **Sık Kullanılanlar** OMS portalında ve **kayıtlı aramaları** Azure portalında.</span><span class="sxs-lookup"><span data-stu-id="b0179-122">Saved searches will appear under **Favorites** in the OMS portal and **Saved Searches** in the Azure portal .</span></span>  <span data-ttu-id="b0179-123">Kaydedilmiş bir aramayı de her uyarı için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="b0179-123">A saved search is also required for each alert.</span></span>   

<span data-ttu-id="b0179-124">[Günlük analizi kaydedilen arama](../log-analytics/log-analytics-log-searches.md) kaynaklarınız türü `Microsoft.OperationalInsights/workspaces/savedSearches` ve aşağıdaki yapı ayarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="b0179-124">[Log Analytics saved search](../log-analytics/log-analytics-log-searches.md) resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches` and have the following structure.</span></span>  <span data-ttu-id="b0179-125">Kopyalayabilir ve çözüm dosyanıza Bu kod parçacığını yapıştırın ve parametre adlarını değiştirmek için bu ortak değişkenleri ve parametreleri içerir.</span><span class="sxs-lookup"><span data-stu-id="b0179-125">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

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



<span data-ttu-id="b0179-126">Kaydedilmiş bir aramayı özelliklerin her biri aşağıdaki tabloda açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="b0179-126">Each of the properties of a saved search are described in the following table.</span></span> 

| <span data-ttu-id="b0179-127">Özellik</span><span class="sxs-lookup"><span data-stu-id="b0179-127">Property</span></span> | <span data-ttu-id="b0179-128">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b0179-128">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="b0179-129">category</span><span class="sxs-lookup"><span data-stu-id="b0179-129">category</span></span> | <span data-ttu-id="b0179-130">Kayıtlı arama kategorisi.</span><span class="sxs-lookup"><span data-stu-id="b0179-130">The category for the saved search.</span></span>  <span data-ttu-id="b0179-131">Konsolunda birlikte gruplanır şekilde aynı çözümüne kaydedilmiş yapılan aramalar genellikle tek bir kategori paylaşır.</span><span class="sxs-lookup"><span data-stu-id="b0179-131">Any saved searches in the same solution will often share a single category so they are grouped together in the console.</span></span> |
| <span data-ttu-id="b0179-132">görünen adı</span><span class="sxs-lookup"><span data-stu-id="b0179-132">displayname</span></span> | <span data-ttu-id="b0179-133">Portalı'nda kayıtlı arama için görüntülenecek adı.</span><span class="sxs-lookup"><span data-stu-id="b0179-133">Name to display for the saved search in the portal.</span></span> |
| <span data-ttu-id="b0179-134">sorgu</span><span class="sxs-lookup"><span data-stu-id="b0179-134">query</span></span> | <span data-ttu-id="b0179-135">Çalıştırılacak sorgu.</span><span class="sxs-lookup"><span data-stu-id="b0179-135">Query to run.</span></span> |

> [!NOTE]
> <span data-ttu-id="b0179-136">JSON olarak yorumlanabilecek karakterler içeriyorsa, sorguda kaçış karakterleri kullanmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="b0179-136">You may need to use escape characters in the query if it includes characters that could be interpreted as JSON.</span></span>  <span data-ttu-id="b0179-137">Örneğin, sorgu, **türü: AzureActivity OperationName:"Microsoft.Compute/virtualMachines/write"**, çözüm dosyasındaki yazılmalıdır **türü: AzureActivity işlemadı:\" Microsoft.Compute/virtualMachines/write\"**.</span><span class="sxs-lookup"><span data-stu-id="b0179-137">For example, if your query was **Type:AzureActivity OperationName:"Microsoft.Compute/virtualMachines/write"**, it should be written in the solution file as **Type:AzureActivity OperationName:\"Microsoft.Compute/virtualMachines/write\"**.</span></span>

## <a name="alerts"></a><span data-ttu-id="b0179-138">Uyarılar</span><span class="sxs-lookup"><span data-stu-id="b0179-138">Alerts</span></span>
<span data-ttu-id="b0179-139">[Analytics uyarıları oturum](../log-analytics/log-analytics-alerts.md) düzenli aralıklarla kaydedilmiş bir aramayı çalıştırma uyarı kuralları tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="b0179-139">[Log Analytics alerts](../log-analytics/log-analytics-alerts.md) are created by alert rules that run a saved search on a regular interval.</span></span>  <span data-ttu-id="b0179-140">Sorgu eşleşmesinin sonuçlarını ölçütleri belirtilmişse, bir uyarı kaydı oluşturulur ve bir veya daha fazla eylem çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b0179-140">If the results of the query match specified criteria, an alert record is created and one or more actions are run.</span></span>  

<span data-ttu-id="b0179-141">Uyarı kurallarında bir yönetim çözümü, aşağıdaki üç farklı kaynakları yapılır.</span><span class="sxs-lookup"><span data-stu-id="b0179-141">Alert rules in a management solution are made up of the following three different resources.</span></span>

- <span data-ttu-id="b0179-142">**Kayıtlı arama.**</span><span class="sxs-lookup"><span data-stu-id="b0179-142">**Saved search.**</span></span>  <span data-ttu-id="b0179-143">Çalıştırılacak günlük arama tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b0179-143">Defines the log search that will be run.</span></span>  <span data-ttu-id="b0179-144">Birden çok uyarı kurallarını, tek bir kayıtlı arama paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b0179-144">Multiple alert rules can share a single saved search.</span></span>
- <span data-ttu-id="b0179-145">**Zamanlama.**</span><span class="sxs-lookup"><span data-stu-id="b0179-145">**Schedule.**</span></span>  <span data-ttu-id="b0179-146">Günlük arama ne sıklıkta çalışacak tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b0179-146">Defines how often the log search will be run.</span></span>  <span data-ttu-id="b0179-147">Her uyarı kuralı tek bir zamanlama sahip olur.</span><span class="sxs-lookup"><span data-stu-id="b0179-147">Each alert rule will have one and only one schedule.</span></span>
- <span data-ttu-id="b0179-148">**Uyarı eylem.**</span><span class="sxs-lookup"><span data-stu-id="b0179-148">**Alert action.**</span></span>  <span data-ttu-id="b0179-149">Her uyarı kuralı bir eylem kaynak türüne sahip olacaktır **uyarı** ne zaman bir uyarı kaydı oluşturulur ve uyarının önem derecesi ölçütlerini gibi uyarı ayrıntılarını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b0179-149">Each alert rule will have one action resource with a type of **Alert** that defines the details of the alert such as the criteria for when an alert record will be created and the alert's severity.</span></span>  <span data-ttu-id="b0179-150">Eylem kaynak isteğe bağlı olarak bir posta ve runbook yanıt tanımlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="b0179-150">The action resource will optionally define a mail and runbook response.</span></span>
- <span data-ttu-id="b0179-151">**Web kancası eylem (isteğe bağlı).**</span><span class="sxs-lookup"><span data-stu-id="b0179-151">**Webhook action (optional).**</span></span>  <span data-ttu-id="b0179-152">Uyarı kuralı bir Web kancası çağırır sonra başka bir işlem kaynak türüne sahip gerektirir **Web kancası**.</span><span class="sxs-lookup"><span data-stu-id="b0179-152">If the alert rule will call a webhook, then it requires an additional action resource with a type of **Webhook**.</span></span>    

<span data-ttu-id="b0179-153">Kaynaklar, yukarıda açıklanan arama kaydedildi.</span><span class="sxs-lookup"><span data-stu-id="b0179-153">Saved search resources are described above.</span></span>  <span data-ttu-id="b0179-154">Diğer kaynaklar aşağıda açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="b0179-154">The other resources are described below.</span></span>


### <a name="schedule-resource"></a><span data-ttu-id="b0179-155">Zamanlama kaynak</span><span class="sxs-lookup"><span data-stu-id="b0179-155">Schedule resource</span></span>

<span data-ttu-id="b0179-156">Kaydedilmiş bir aramayı her zamanlamayı ayrı bir uyarı kuralı temsil eden ile bir veya daha fazla zamanlama olabilir.</span><span class="sxs-lookup"><span data-stu-id="b0179-156">A saved search can have one or more schedules with each schedule representing a separate alert rule.</span></span> <span data-ttu-id="b0179-157">Ne sıklıkta arama çalıştırma ve verilerin alınacağı zaman aralığı olan zamanlamayı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b0179-157">The schedule defines how often the search is run and the time interval over which the data is retrieved.</span></span>  <span data-ttu-id="b0179-158">Zamanlama kaynaklarınız türü `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/` ve aşağıdaki yapı ayarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="b0179-158">Schedule resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/` and have the following structure.</span></span> <span data-ttu-id="b0179-159">Kopyalayabilir ve çözüm dosyanıza Bu kod parçacığını yapıştırın ve parametre adlarını değiştirmek için bu ortak değişkenleri ve parametreleri içerir.</span><span class="sxs-lookup"><span data-stu-id="b0179-159">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 


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



<span data-ttu-id="b0179-160">Zamanlama kaynaklar için özellikler aşağıdaki tabloda açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="b0179-160">The properties for schedule resources are described in the following table.</span></span>

| <span data-ttu-id="b0179-161">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="b0179-161">Element name</span></span> | <span data-ttu-id="b0179-162">Gerekli</span><span class="sxs-lookup"><span data-stu-id="b0179-162">Required</span></span> | <span data-ttu-id="b0179-163">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b0179-163">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="b0179-164">Etkin</span><span class="sxs-lookup"><span data-stu-id="b0179-164">enabled</span></span>       | <span data-ttu-id="b0179-165">Evet</span><span class="sxs-lookup"><span data-stu-id="b0179-165">Yes</span></span> | <span data-ttu-id="b0179-166">Oluşturulduğunda uyarının etkin olup olmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="b0179-166">Specifies whether the alert is enabled when it's created.</span></span> |
| <span data-ttu-id="b0179-167">aralığı</span><span class="sxs-lookup"><span data-stu-id="b0179-167">interval</span></span>      | <span data-ttu-id="b0179-168">Evet</span><span class="sxs-lookup"><span data-stu-id="b0179-168">Yes</span></span> | <span data-ttu-id="b0179-169">Ne sıklıkta sorgu dakika içinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="b0179-169">How often the query runs in minutes.</span></span> |
| <span data-ttu-id="b0179-170">QueryTimeSpan</span><span class="sxs-lookup"><span data-stu-id="b0179-170">queryTimeSpan</span></span> | <span data-ttu-id="b0179-171">Evet</span><span class="sxs-lookup"><span data-stu-id="b0179-171">Yes</span></span> | <span data-ttu-id="b0179-172">Sonuçları değerlendirileceği üzerinden dakika cinsinden süre uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="b0179-172">Length of time in minutes over which to evaluate results.</span></span> |

<span data-ttu-id="b0179-173">Zamanlama önce oluşturulan zamanlama kaynak kayıtlı arama üzerinde bağımlı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b0179-173">The schedule resource should depend on the saved search so that it's created before the schedule.</span></span>


### <a name="actions"></a><span data-ttu-id="b0179-174">Eylemler</span><span class="sxs-lookup"><span data-stu-id="b0179-174">Actions</span></span>
<span data-ttu-id="b0179-175">Belirtilen eylem kaynak iki tür vardır **türü** özelliği.</span><span class="sxs-lookup"><span data-stu-id="b0179-175">There are two types of action resource specified by the **Type** property.</span></span>  <span data-ttu-id="b0179-176">Bir zamanlama gerektiren **uyarı** uyarı kuralı ve bir uyarı oluşturulduğunda, hangi eylemleri alınır ayrıntılarını tanımlayan eylem.</span><span class="sxs-lookup"><span data-stu-id="b0179-176">A schedule requires one **Alert** action which defines the details of the alert rule and what actions are taken when an alert is created.</span></span>  <span data-ttu-id="b0179-177">Ayrıca içerebilir bir **Web kancası** eylem bir Web kancası uyarıdan çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b0179-177">It may also include a **Webhook** action if a webhook should be called from the alert.</span></span>  

<span data-ttu-id="b0179-178">Eylem kaynaklarınız türü `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`.</span><span class="sxs-lookup"><span data-stu-id="b0179-178">Action resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`.</span></span>  

#### <a name="alert-actions"></a><span data-ttu-id="b0179-179">Uyarı eylemleri</span><span class="sxs-lookup"><span data-stu-id="b0179-179">Alert actions</span></span>

<span data-ttu-id="b0179-180">Her biri zaman çizelgeleri **uyarı** eylem.</span><span class="sxs-lookup"><span data-stu-id="b0179-180">Every schedule will have one **Alert** action.</span></span>  <span data-ttu-id="b0179-181">Bu, uyarı ve isteğe bağlı olarak bildirim ve düzeltme eylemlerinin ayrıntılarını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b0179-181">This defines the details of the alert and optionally notification and remediation actions.</span></span>  <span data-ttu-id="b0179-182">Bir bildirim bir veya daha fazla adrese bir e-posta gönderir.</span><span class="sxs-lookup"><span data-stu-id="b0179-182">A notification sends an email to one or more addresses.</span></span>  <span data-ttu-id="b0179-183">Bir düzeltme algılanan sorunu düzeltmek girişiminde Azure Otomasyonu'nda bir runbook başlatır.</span><span class="sxs-lookup"><span data-stu-id="b0179-183">A remediation starts a runbook in Azure Automation to attempt to remediate the detected issue.</span></span>

<span data-ttu-id="b0179-184">Uyarı eylemleri aşağıdaki yapı ayarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="b0179-184">Alert actions have the following structure.</span></span>  <span data-ttu-id="b0179-185">Kopyalayabilir ve çözüm dosyanıza Bu kod parçacığını yapıştırın ve parametre adlarını değiştirmek için bu ortak değişkenleri ve parametreleri içerir.</span><span class="sxs-lookup"><span data-stu-id="b0179-185">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 



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

<span data-ttu-id="b0179-186">Uyarı eylemi kaynaklar için özellikler aşağıdaki tabloda açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="b0179-186">The properties for Alert action resources are described in the following tables.</span></span>

| <span data-ttu-id="b0179-187">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="b0179-187">Element name</span></span> | <span data-ttu-id="b0179-188">Gerekli</span><span class="sxs-lookup"><span data-stu-id="b0179-188">Required</span></span> | <span data-ttu-id="b0179-189">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b0179-189">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="b0179-190">Tür</span><span class="sxs-lookup"><span data-stu-id="b0179-190">Type</span></span> | <span data-ttu-id="b0179-191">Evet</span><span class="sxs-lookup"><span data-stu-id="b0179-191">Yes</span></span> | <span data-ttu-id="b0179-192">Eylem türü.</span><span class="sxs-lookup"><span data-stu-id="b0179-192">Type of the action.</span></span>  <span data-ttu-id="b0179-193">Bu **uyarı** uyarı eylemleri için.</span><span class="sxs-lookup"><span data-stu-id="b0179-193">This will be **Alert** for alert actions.</span></span> |
| <span data-ttu-id="b0179-194">Ad</span><span class="sxs-lookup"><span data-stu-id="b0179-194">Name</span></span> | <span data-ttu-id="b0179-195">Evet</span><span class="sxs-lookup"><span data-stu-id="b0179-195">Yes</span></span> | <span data-ttu-id="b0179-196">Uyarı görünen adı.</span><span class="sxs-lookup"><span data-stu-id="b0179-196">Display name for the alert.</span></span>  <span data-ttu-id="b0179-197">Bu uyarı kuralı için konsolunda görüntülenen addır.</span><span class="sxs-lookup"><span data-stu-id="b0179-197">This is the name that's displayed in the console for the alert rule.</span></span> |
| <span data-ttu-id="b0179-198">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b0179-198">Description</span></span> | <span data-ttu-id="b0179-199">Hayır</span><span class="sxs-lookup"><span data-stu-id="b0179-199">No</span></span> | <span data-ttu-id="b0179-200">Uyarı isteğe bağlı bir açıklama.</span><span class="sxs-lookup"><span data-stu-id="b0179-200">Optional description of the alert.</span></span> |
| <span data-ttu-id="b0179-201">Önem Derecesi</span><span class="sxs-lookup"><span data-stu-id="b0179-201">Severity</span></span> | <span data-ttu-id="b0179-202">Evet</span><span class="sxs-lookup"><span data-stu-id="b0179-202">Yes</span></span> | <span data-ttu-id="b0179-203">Aşağıdaki değerlerden uyarı kaydının önem derecesi:</span><span class="sxs-lookup"><span data-stu-id="b0179-203">Severity of the alert record from the following values:</span></span><br><br> <span data-ttu-id="b0179-204">**Kritik**</span><span class="sxs-lookup"><span data-stu-id="b0179-204">**Critical**</span></span><br><span data-ttu-id="b0179-205">**Uyarı**</span><span class="sxs-lookup"><span data-stu-id="b0179-205">**Warning**</span></span><br><span data-ttu-id="b0179-206">**Bilgilendirme**</span><span class="sxs-lookup"><span data-stu-id="b0179-206">**Informational**</span></span> |


##### <a name="threshold"></a><span data-ttu-id="b0179-207">Eşik</span><span class="sxs-lookup"><span data-stu-id="b0179-207">Threshold</span></span>
<span data-ttu-id="b0179-208">Bu bölüm gereklidir.</span><span class="sxs-lookup"><span data-stu-id="b0179-208">This section is required.</span></span>  <span data-ttu-id="b0179-209">Uyarı eşiği özelliklerini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b0179-209">It defines the properties for the alert threshold.</span></span>

| <span data-ttu-id="b0179-210">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="b0179-210">Element name</span></span> | <span data-ttu-id="b0179-211">Gerekli</span><span class="sxs-lookup"><span data-stu-id="b0179-211">Required</span></span> | <span data-ttu-id="b0179-212">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b0179-212">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="b0179-213">işleci</span><span class="sxs-lookup"><span data-stu-id="b0179-213">Operator</span></span> | <span data-ttu-id="b0179-214">Evet</span><span class="sxs-lookup"><span data-stu-id="b0179-214">Yes</span></span> | <span data-ttu-id="b0179-215">Aşağıdaki değerlerden karşılaştırma işleci:</span><span class="sxs-lookup"><span data-stu-id="b0179-215">Operator for the comparison from the following values:</span></span><br><br><span data-ttu-id="b0179-216">**gt büyük =<br>lt = küçüktür**</span><span class="sxs-lookup"><span data-stu-id="b0179-216">**gt = greater than<br>lt = less than**</span></span> |
| <span data-ttu-id="b0179-217">Değer</span><span class="sxs-lookup"><span data-stu-id="b0179-217">Value</span></span> | <span data-ttu-id="b0179-218">Evet</span><span class="sxs-lookup"><span data-stu-id="b0179-218">Yes</span></span> | <span data-ttu-id="b0179-219">Sonuçları karşılaştırmak için değer.</span><span class="sxs-lookup"><span data-stu-id="b0179-219">The value to compare the results.</span></span> |


##### <a name="metricstrigger"></a><span data-ttu-id="b0179-220">MetricsTrigger</span><span class="sxs-lookup"><span data-stu-id="b0179-220">MetricsTrigger</span></span>
<span data-ttu-id="b0179-221">Bu bölümde isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="b0179-221">This section is optional.</span></span>  <span data-ttu-id="b0179-222">Bir ölçüm ölçüm uyarı içerir.</span><span class="sxs-lookup"><span data-stu-id="b0179-222">Include it for a metric measurement alert.</span></span>

> [!NOTE]
> <span data-ttu-id="b0179-223">Ölçüm ölçüm uyarılar şu anda genel önizlemede.</span><span class="sxs-lookup"><span data-stu-id="b0179-223">Metric measurement alerts are currently in public preview.</span></span> 

| <span data-ttu-id="b0179-224">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="b0179-224">Element name</span></span> | <span data-ttu-id="b0179-225">Gerekli</span><span class="sxs-lookup"><span data-stu-id="b0179-225">Required</span></span> | <span data-ttu-id="b0179-226">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b0179-226">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="b0179-227">TriggerCondition</span><span class="sxs-lookup"><span data-stu-id="b0179-227">TriggerCondition</span></span> | <span data-ttu-id="b0179-228">Evet</span><span class="sxs-lookup"><span data-stu-id="b0179-228">Yes</span></span> | <span data-ttu-id="b0179-229">Eşik ihlallerini veya aşağıdaki değerlerden ardışık ihlallerini toplam sayısını olup olmadığını belirtir:</span><span class="sxs-lookup"><span data-stu-id="b0179-229">Specifies whether the threshold is for total number of breaches or consecutive breaches from the following values:</span></span><br><br><span data-ttu-id="b0179-230">**Toplam<br>ardışık**</span><span class="sxs-lookup"><span data-stu-id="b0179-230">**Total<br>Consecutive**</span></span> |
| <span data-ttu-id="b0179-231">işleci</span><span class="sxs-lookup"><span data-stu-id="b0179-231">Operator</span></span> | <span data-ttu-id="b0179-232">Evet</span><span class="sxs-lookup"><span data-stu-id="b0179-232">Yes</span></span> | <span data-ttu-id="b0179-233">Aşağıdaki değerlerden karşılaştırma işleci:</span><span class="sxs-lookup"><span data-stu-id="b0179-233">Operator for the comparison from the following values:</span></span><br><br><span data-ttu-id="b0179-234">**gt büyük =<br>lt = küçüktür**</span><span class="sxs-lookup"><span data-stu-id="b0179-234">**gt = greater than<br>lt = less than**</span></span> |
| <span data-ttu-id="b0179-235">Değer</span><span class="sxs-lookup"><span data-stu-id="b0179-235">Value</span></span> | <span data-ttu-id="b0179-236">Evet</span><span class="sxs-lookup"><span data-stu-id="b0179-236">Yes</span></span> | <span data-ttu-id="b0179-237">Sayısı uyarıyı tetikleyecek ölçütler karşılanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b0179-237">Number of the times the criteria must be met to trigger the alert.</span></span> |

##### <a name="throttling"></a><span data-ttu-id="b0179-238">Azaltma</span><span class="sxs-lookup"><span data-stu-id="b0179-238">Throttling</span></span>
<span data-ttu-id="b0179-239">Bu bölümde isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="b0179-239">This section is optional.</span></span>  <span data-ttu-id="b0179-240">Bazı süreyi bir uyarı oluşturulduktan sonra için aynı kural uyarıları gizlemek istiyorsanız, bu bölüm içerir.</span><span class="sxs-lookup"><span data-stu-id="b0179-240">Include this section if you want to suppress alerts from the same rule for some amount of time after an alert is created.</span></span>

| <span data-ttu-id="b0179-241">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="b0179-241">Element name</span></span> | <span data-ttu-id="b0179-242">Gerekli</span><span class="sxs-lookup"><span data-stu-id="b0179-242">Required</span></span> | <span data-ttu-id="b0179-243">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b0179-243">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="b0179-244">Dakika Cinsiden Süre</span><span class="sxs-lookup"><span data-stu-id="b0179-244">DurationInMinutes</span></span> | <span data-ttu-id="b0179-245">Dahil edilen öğesi azaltma, Evet</span><span class="sxs-lookup"><span data-stu-id="b0179-245">Yes if Throttling element included</span></span> | <span data-ttu-id="b0179-246">Aynı uyarı kuralı birinden oluşturulduktan sonra uyarıları gizlemek için dakika sayısı.</span><span class="sxs-lookup"><span data-stu-id="b0179-246">Number of minutes to suppress alerts after one from the same alert rule is created.</span></span> |

##### <a name="emailnotification"></a><span data-ttu-id="b0179-247">EmailNotification</span><span class="sxs-lookup"><span data-stu-id="b0179-247">EmailNotification</span></span>
 <span data-ttu-id="b0179-248">Bu bölümde isteğe bağlı bir veya daha fazla alıcıya posta göndermek için uyarı istiyorsanız ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b0179-248">This section is optional  Include it if you want the alert to send mail to one or more recipients.</span></span>

| <span data-ttu-id="b0179-249">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="b0179-249">Element name</span></span> | <span data-ttu-id="b0179-250">Gerekli</span><span class="sxs-lookup"><span data-stu-id="b0179-250">Required</span></span> | <span data-ttu-id="b0179-251">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b0179-251">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="b0179-252">Alıcıları</span><span class="sxs-lookup"><span data-stu-id="b0179-252">Recipients</span></span> | <span data-ttu-id="b0179-253">Evet</span><span class="sxs-lookup"><span data-stu-id="b0179-253">Yes</span></span> | <span data-ttu-id="b0179-254">Virgülle ayrılmış bir uyarı aşağıdaki örnekte olduğu gibi oluşturulduğunda, bildirim göndermek için e-posta adresleri listesi.</span><span class="sxs-lookup"><span data-stu-id="b0179-254">Comma delimited list of email addresses to send notification when an alert is created such as in the following example.</span></span><br><br><span data-ttu-id="b0179-255">**[ "recipient1@contoso.com", "recipient2@contoso.com" ]**</span><span class="sxs-lookup"><span data-stu-id="b0179-255">**[ "recipient1@contoso.com", "recipient2@contoso.com" ]**</span></span> |
| <span data-ttu-id="b0179-256">Konu</span><span class="sxs-lookup"><span data-stu-id="b0179-256">Subject</span></span> | <span data-ttu-id="b0179-257">Evet</span><span class="sxs-lookup"><span data-stu-id="b0179-257">Yes</span></span> | <span data-ttu-id="b0179-258">Posta konu satırı.</span><span class="sxs-lookup"><span data-stu-id="b0179-258">Subject line of the mail.</span></span> |
| <span data-ttu-id="b0179-259">Eki</span><span class="sxs-lookup"><span data-stu-id="b0179-259">Attachment</span></span> | <span data-ttu-id="b0179-260">Hayır</span><span class="sxs-lookup"><span data-stu-id="b0179-260">No</span></span> | <span data-ttu-id="b0179-261">Ekleri şu anda desteklenmemektedir.</span><span class="sxs-lookup"><span data-stu-id="b0179-261">Attachments are not currently supported.</span></span>  <span data-ttu-id="b0179-262">Bu öğe dahil ise olmalıdır **hiçbiri**.</span><span class="sxs-lookup"><span data-stu-id="b0179-262">If this element is included, it should be **None**.</span></span> |


##### <a name="remediation"></a><span data-ttu-id="b0179-263">Düzeltme</span><span class="sxs-lookup"><span data-stu-id="b0179-263">Remediation</span></span>
<span data-ttu-id="b0179-264">Bu bölümde isteğe yanıt olarak uyarı başlatmak üzere bir runbook'u istiyorsanız ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b0179-264">This section is optional  Include it if you want a runbook to start in response to the alert.</span></span> |

| <span data-ttu-id="b0179-265">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="b0179-265">Element name</span></span> | <span data-ttu-id="b0179-266">Gerekli</span><span class="sxs-lookup"><span data-stu-id="b0179-266">Required</span></span> | <span data-ttu-id="b0179-267">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b0179-267">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="b0179-268">RunbookName</span><span class="sxs-lookup"><span data-stu-id="b0179-268">RunbookName</span></span> | <span data-ttu-id="b0179-269">Evet</span><span class="sxs-lookup"><span data-stu-id="b0179-269">Yes</span></span> | <span data-ttu-id="b0179-270">Başlatmak için runbook'un adı.</span><span class="sxs-lookup"><span data-stu-id="b0179-270">Name of the runbook to start.</span></span> |
| <span data-ttu-id="b0179-271">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="b0179-271">WebhookUri</span></span> | <span data-ttu-id="b0179-272">Evet</span><span class="sxs-lookup"><span data-stu-id="b0179-272">Yes</span></span> | <span data-ttu-id="b0179-273">Runbook için Web kancası URI'si.</span><span class="sxs-lookup"><span data-stu-id="b0179-273">Uri of the webhook for the runbook.</span></span> |
| <span data-ttu-id="b0179-274">Süre sonu</span><span class="sxs-lookup"><span data-stu-id="b0179-274">Expiry</span></span> | <span data-ttu-id="b0179-275">Hayır</span><span class="sxs-lookup"><span data-stu-id="b0179-275">No</span></span> | <span data-ttu-id="b0179-276">Tarih ve saat düzeltme süresi dolar.</span><span class="sxs-lookup"><span data-stu-id="b0179-276">Date and time that the remediation expires.</span></span> |

#### <a name="webhook-actions"></a><span data-ttu-id="b0179-277">Web kancası eylemleri</span><span class="sxs-lookup"><span data-stu-id="b0179-277">Webhook actions</span></span>

<span data-ttu-id="b0179-278">Web kancası eylemleri, bir URL çağırma ve isteğe bağlı olarak gönderilecek bir yükü sağlayarak bir işlem başlatın.</span><span class="sxs-lookup"><span data-stu-id="b0179-278">Webhook actions start a process by calling a URL and optionally providing a payload to be sent.</span></span> <span data-ttu-id="b0179-279">Azure Otomasyon çalışma kitabı dışındaki işlemler çağırabilir Web kancası için amacı dışında düzeltme eylemleri benzerdir.</span><span class="sxs-lookup"><span data-stu-id="b0179-279">They are similar to Remediation actions except they are meant for webhooks that may invoke processes other than Azure Automation runbooks.</span></span> <span data-ttu-id="b0179-280">Uzak işlem teslim edilecek bir yükü sağlama ek seçeneği de sağlar.</span><span class="sxs-lookup"><span data-stu-id="b0179-280">They also provide the additional option of providing a payload to be delivered to the remote process.</span></span>

<span data-ttu-id="b0179-281">Uyarınız bir Web kancası çağırır sonra bir eylem kaynak türüne sahip gerekir **Web kancası** ek olarak **uyarı** eylem kaynak.</span><span class="sxs-lookup"><span data-stu-id="b0179-281">If your alert will call a webhook, then it will need an action resource with a type of **Webhook** in addition to the **Alert** action resource.</span></span>  

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

<span data-ttu-id="b0179-282">Web kancası eylem kaynaklar için özellikler aşağıdaki tabloda açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="b0179-282">The properties for Webhook action resources are described in the following tables.</span></span>

| <span data-ttu-id="b0179-283">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="b0179-283">Element name</span></span> | <span data-ttu-id="b0179-284">Gerekli</span><span class="sxs-lookup"><span data-stu-id="b0179-284">Required</span></span> | <span data-ttu-id="b0179-285">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b0179-285">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="b0179-286">type</span><span class="sxs-lookup"><span data-stu-id="b0179-286">type</span></span> | <span data-ttu-id="b0179-287">Evet</span><span class="sxs-lookup"><span data-stu-id="b0179-287">Yes</span></span> | <span data-ttu-id="b0179-288">Eylem türü.</span><span class="sxs-lookup"><span data-stu-id="b0179-288">Type of the action.</span></span>  <span data-ttu-id="b0179-289">Bu **Web kancası** Web kancası eylemleri için.</span><span class="sxs-lookup"><span data-stu-id="b0179-289">This will be **Webhook** for webhook actions.</span></span> |
| <span data-ttu-id="b0179-290">ad</span><span class="sxs-lookup"><span data-stu-id="b0179-290">name</span></span> | <span data-ttu-id="b0179-291">Evet</span><span class="sxs-lookup"><span data-stu-id="b0179-291">Yes</span></span> | <span data-ttu-id="b0179-292">Eylem görünen adı.</span><span class="sxs-lookup"><span data-stu-id="b0179-292">Display name for the action.</span></span>  <span data-ttu-id="b0179-293">Bu konsolunda görüntülenmez.</span><span class="sxs-lookup"><span data-stu-id="b0179-293">This is not displayed in the console.</span></span> |
| <span data-ttu-id="b0179-294">wehookUri</span><span class="sxs-lookup"><span data-stu-id="b0179-294">wehookUri</span></span> | <span data-ttu-id="b0179-295">Evet</span><span class="sxs-lookup"><span data-stu-id="b0179-295">Yes</span></span> | <span data-ttu-id="b0179-296">Web kancası için URI.</span><span class="sxs-lookup"><span data-stu-id="b0179-296">Uri for the webhook.</span></span> |
| <span data-ttu-id="b0179-297">CustomPayload</span><span class="sxs-lookup"><span data-stu-id="b0179-297">customPayload</span></span> | <span data-ttu-id="b0179-298">Hayır</span><span class="sxs-lookup"><span data-stu-id="b0179-298">No</span></span> | <span data-ttu-id="b0179-299">Web kancası için gönderilecek özel yükü.</span><span class="sxs-lookup"><span data-stu-id="b0179-299">Custom payload to be sent to the webhook.</span></span> <span data-ttu-id="b0179-300">Web kancası bekleniyor üzerinde biçimi bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="b0179-300">The format will depend on what the webhook is expecting.</span></span> |




## <a name="sample"></a><span data-ttu-id="b0179-301">Örnek</span><span class="sxs-lookup"><span data-stu-id="b0179-301">Sample</span></span>

<span data-ttu-id="b0179-302">Aşağıdaki kaynakları içermektedir içeren bir çözüm örneği aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="b0179-302">Following is a sample of a solution that include that includes the following resources:</span></span>

- <span data-ttu-id="b0179-303">Kayıtlı arama</span><span class="sxs-lookup"><span data-stu-id="b0179-303">Saved search</span></span>
- <span data-ttu-id="b0179-304">Zamanlama</span><span class="sxs-lookup"><span data-stu-id="b0179-304">Schedule</span></span>
- <span data-ttu-id="b0179-305">Uyarı eylemi</span><span class="sxs-lookup"><span data-stu-id="b0179-305">Alert action</span></span>
- <span data-ttu-id="b0179-306">Web kancası eylemi</span><span class="sxs-lookup"><span data-stu-id="b0179-306">Webhook action</span></span>

<span data-ttu-id="b0179-307">Örnek kullanır [standart çözüm parametreleri](operations-management-suite-solutions-solution-file.md#parameters) cmdlet'e kod değerleri kaynak tanımlarında aksine bir çözümde yaygın olarak kullanılacak değişkenleri.</span><span class="sxs-lookup"><span data-stu-id="b0179-307">The sample uses [standard solution parameters](operations-management-suite-solutions-solution-file.md#parameters) variables that would commonly be used in a solution as opposed to hardcoding values in the resource definitions.</span></span>

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
              "Description": "List of recipients for the email alert separated by semicolon"
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


<span data-ttu-id="b0179-308">Aşağıdaki parametre dosyası bu çözüm için örnek değerleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="b0179-308">The following parameter file provides samples values for this solution.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="b0179-309">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b0179-309">Next steps</span></span>
* <span data-ttu-id="b0179-310">[Görünümler ekleme](operations-management-suite-solutions-resources-views.md) Yönetimi çözümünüz için.</span><span class="sxs-lookup"><span data-stu-id="b0179-310">[Add views](operations-management-suite-solutions-resources-views.md) to your management solution.</span></span>
* <span data-ttu-id="b0179-311">[Otomasyon runbook'ları ve diğer kaynakları eklemek](operations-management-suite-solutions-resources-automation.md) Yönetimi çözümünüz için.</span><span class="sxs-lookup"><span data-stu-id="b0179-311">[Add Automation runbooks and other resources](operations-management-suite-solutions-resources-automation.md) to your management solution.</span></span>

