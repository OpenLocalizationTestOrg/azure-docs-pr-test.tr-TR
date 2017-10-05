---
title: "Azure tanılama günlükleri'ne genel bakış | Microsoft Docs"
description: "Azure tanılama günlüklerini nelerdir ve bir Azure kaynağı içinde gerçekleşen olayların anlamak için bunları nasıl kullanacağınızı öğrenin."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: fe8887df-b0e6-46f8-b2c0-11994d28e44f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem; magoedte
ms.openlocfilehash: d59abde29fc7b73a799e5bf3659b02f824b693de
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="collect-and-consume-log-data-from-your-azure-resources"></a><span data-ttu-id="90db0-103">Toplamak ve Azure kaynaklarınızdan günlük verilerini kullanma</span><span class="sxs-lookup"><span data-stu-id="90db0-103">Collect and consume log data from your Azure resources</span></span>

## <a name="what-are-azure-resource-diagnostic-logs"></a><span data-ttu-id="90db0-104">Azure kaynak tanılama günlüklerini nelerdir</span><span class="sxs-lookup"><span data-stu-id="90db0-104">What are Azure resource diagnostic logs</span></span>
<span data-ttu-id="90db0-105">**Azure kaynak düzeyi tanılama günlüklerini** olan bir kaynak tarafından gösterilen günlükleri, o kaynak işlemi hakkında zengin, sık veriler sağlar.</span><span class="sxs-lookup"><span data-stu-id="90db0-105">**Azure resource-level diagnostic logs** are logs emitted by a resource that provide rich, frequent data about the operation of that resource.</span></span> <span data-ttu-id="90db0-106">Bu günlükler içeriğini kaynak türüne göre değişir.</span><span class="sxs-lookup"><span data-stu-id="90db0-106">The content of these logs varies by resource type.</span></span> <span data-ttu-id="90db0-107">Örneğin, ağ güvenlik grubu kural sayaçları ve anahtar kasası denetimleri kaynak günlükleri iki kategorisi vardır.</span><span class="sxs-lookup"><span data-stu-id="90db0-107">For example, Network Security Group rule counters and Key Vault audits are two categories of resource logs.</span></span>

<span data-ttu-id="90db0-108">Kaynak düzeyi tanılama günlükleri farklı [etkinlik günlüğü](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="90db0-108">Resource-level diagnostic logs differ from the [Activity Log](monitoring-overview-activity-logs.md).</span></span> <span data-ttu-id="90db0-109">Etkinlik günlüğü kaynakları Kaynak Yöneticisi'ni kullanarak, örneğin, bir sanal makine oluşturma veya bir mantıksal uygulama silme gerçekleştirilen işlemler hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="90db0-109">The Activity Log provides insight into the operations that were performed on resources in your subscription using Resource Manager, for example, creating a virtual machine or deleting a logic app.</span></span> <span data-ttu-id="90db0-110">Etkinlik günlüğü bir abonelik düzeyi günlüğü bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="90db0-110">The Activity Log is a subscription-level log.</span></span> <span data-ttu-id="90db0-111">Kaynak düzeyi tanılama günlükleri, bu kaynak içinde kendisi, örneğin, gizli bir anahtar Kasası'nı alma gerçekleştirilen işlemler hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="90db0-111">Resource-level diagnostic logs provide insight into operations that were performed within that resource itself, for example, getting a secret from a Key Vault.</span></span>

<span data-ttu-id="90db0-112">Kaynak düzeyi tanılama günlüklerini de konuk işletim sistemi düzeyinde tanılama günlükleri farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="90db0-112">Resource-level diagnostic logs also differ from guest OS-level diagnostic logs.</span></span> <span data-ttu-id="90db0-113">Konuk işletim sistemi tanılama günlüklerini bu sanal makine içinde çalışan bir aracının tarafından toplanan veya diğer kaynak türü desteklenir.</span><span class="sxs-lookup"><span data-stu-id="90db0-113">Guest OS diagnostic logs are those collected by an agent running inside of a virtual machine or other supported resource type.</span></span> <span data-ttu-id="90db0-114">Konuk işletim sistemi düzeyinde tanılama günlüklerini işletim sistemi ve sanal makine üzerinde çalışan uygulamalardan veri yakalama işlemi sırasında kaynak düzeyi tanılama günlüklerini Azure platformu kendisini hiçbir aracı ve yakalama kaynak özgü veri gerektirir.</span><span class="sxs-lookup"><span data-stu-id="90db0-114">Resource-level diagnostic logs require no agent and capture resource-specific data from the Azure platform itself, while guest OS-level diagnostic logs capture data from the operating system and applications running on a virtual machine.</span></span>

<span data-ttu-id="90db0-115">Tüm kaynakları kaynak tanılama günlüklerini burada açıklanan yeni türünü desteklemez.</span><span class="sxs-lookup"><span data-stu-id="90db0-115">Not all resources support the new type of resource diagnostic logs described here.</span></span> <span data-ttu-id="90db0-116">Bu makale, hangi kaynak türlerinin yeni kaynak düzeyi tanılama günlüklerini destek listeleyen bir bölüm içerir.</span><span class="sxs-lookup"><span data-stu-id="90db0-116">This article contains a section listing which resource types support the new resource-level diagnostic logs.</span></span>

![<span data-ttu-id="90db0-117">Kaynağın tanılama günlükleri diğer türleri vs günlükleri</span><span class="sxs-lookup"><span data-stu-id="90db0-117">Resource diagnostics logs vs other types of logs</span></span> ](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_vs_other_logs_v5.png)

## <a name="what-you-can-do-with-resource-level-diagnostic-logs"></a><span data-ttu-id="90db0-118">Kaynak düzeyi tanılama günlükleri ile yapabilecekleriniz</span><span class="sxs-lookup"><span data-stu-id="90db0-118">What you can do with resource-level diagnostic logs</span></span>
<span data-ttu-id="90db0-119">Kaynağın tanılama günlükleri ile yapabileceği şeylerden bazıları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="90db0-119">Here are some of the things you can do with resource diagnostic logs:</span></span>

![Kaynağın tanılama günlüklerinin mantıksal yerleştirme](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_Actions.png)


* <span data-ttu-id="90db0-121">Bunları kaydetmek bir [ **depolama hesabı** ](monitoring-archive-diagnostic-logs.md) denetim veya el ile İnceleme için.</span><span class="sxs-lookup"><span data-stu-id="90db0-121">Save them to a [**Storage Account**](monitoring-archive-diagnostic-logs.md) for auditing or manual inspection.</span></span> <span data-ttu-id="90db0-122">Bekletme süresi (gün) kullanarak belirtebilirsiniz **kaynak tanılama ayarlarını**.</span><span class="sxs-lookup"><span data-stu-id="90db0-122">You can specify the retention time (in days) using **resource diagnostic settings**.</span></span>
* <span data-ttu-id="90db0-123">[Bunları akış **Event Hubs** ](monitoring-stream-diagnostic-logs-to-event-hubs.md) bir üçüncü taraf hizmeti veya Powerbı gibi özel analiz çözümü tarafından alımı için.</span><span class="sxs-lookup"><span data-stu-id="90db0-123">[Stream them to **Event Hubs**](monitoring-stream-diagnostic-logs-to-event-hubs.md) for ingestion by a third-party service or custom analytics solution such as PowerBI.</span></span>
* <span data-ttu-id="90db0-124">Bunları ile analiz [OMS günlük analizi](../log-analytics/log-analytics-azure-storage.md)</span><span class="sxs-lookup"><span data-stu-id="90db0-124">Analyze them with [OMS Log Analytics](../log-analytics/log-analytics-azure-storage.md)</span></span>

<span data-ttu-id="90db0-125">Bir depolama hesabı veya günlükleri yayma biri ile aynı abonelikte değil olay hub'ları ad alanı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90db0-125">You can use a storage account or Event Hubs namespace that is not in the same subscription as the one emitting logs.</span></span> <span data-ttu-id="90db0-126">Ayar yapılandıran kullanıcının uygun RBAC her iki aboneliğin erişiminiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="90db0-126">The user who configures the setting must have the appropriate RBAC access to both subscriptions.</span></span>

## <a name="resource-diagnostic-settings"></a><span data-ttu-id="90db0-127">Kaynak tanılama ayarları</span><span class="sxs-lookup"><span data-stu-id="90db0-127">Resource diagnostic settings</span></span>
<span data-ttu-id="90db0-128">Kaynağın tanılama günlüklerini olmayan-kaynakları kaynak tanılama ayarları kullanılarak yapılandırılmış olan işlem.</span><span class="sxs-lookup"><span data-stu-id="90db0-128">Resource diagnostic logs for non-Compute resources are configured using resource diagnostic settings.</span></span> <span data-ttu-id="90db0-129">**Kaynak tanılama ayarlarını** kaynak denetimi için:</span><span class="sxs-lookup"><span data-stu-id="90db0-129">**Resource diagnostic settings** for a resource control:</span></span>

* <span data-ttu-id="90db0-130">Kaynağın tanılama günlüklerini ve ölçümleri (depolama hesabı, olay hub'ları ve/veya OMS günlük analizi) gönderildiği.</span><span class="sxs-lookup"><span data-stu-id="90db0-130">Where resource diagnostic logs and metrics are sent (Storage Account, Event Hubs, and/or OMS Log Analytics).</span></span>
* <span data-ttu-id="90db0-131">Günlük kategorilerini gönderilir ve ölçüm verileri de gönderilip.</span><span class="sxs-lookup"><span data-stu-id="90db0-131">Which log categories are sent and whether metric data is also sent.</span></span>
* <span data-ttu-id="90db0-132">Her günlük kategori bir depolama hesabında ne kadar süre tutulacağını</span><span class="sxs-lookup"><span data-stu-id="90db0-132">How long each log category should be retained in a storage account</span></span>
    - <span data-ttu-id="90db0-133">Sıfır gün bekletme günlükleri sonsuza kadar tutulur anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="90db0-133">A retention of zero days means logs are kept forever.</span></span> <span data-ttu-id="90db0-134">Aksi takdirde, değer 1 ile 2147483647 arasındaki gün herhangi bir sayıda olabilir.</span><span class="sxs-lookup"><span data-stu-id="90db0-134">Otherwise, the value can be any number of days between 1 and 2147483647.</span></span>
    - <span data-ttu-id="90db0-135">Bekletme ilkeleri ayarlanır, ancak yalnızca (örneğin, olay hub'ları veya OMS seçenekler seçilidir) günlükleri bir depolama hesabında depolama devre dışı bırakıldı, bekletme ilkeleri bir etkisi yoktur.</span><span class="sxs-lookup"><span data-stu-id="90db0-135">If retention policies are set but storing logs in a Storage Account is disabled (for example, if only Event Hubs or OMS options are selected), the retention policies have no effect.</span></span>
    - <span data-ttu-id="90db0-136">Bekletme ilkeleri uygulanan başına günlük, olduğundan, bir gün (UTC) dışında tutma sunulmuştur gün günlüklerinden sonunda İlkesi silinir.</span><span class="sxs-lookup"><span data-stu-id="90db0-136">Retention policies are applied per-day, so at the end of a day (UTC), logs from the day that is now beyond the retention policy are deleted.</span></span> <span data-ttu-id="90db0-137">Örneğin, bir günlük bir Bekletme İlkesi nesneniz varsa, günün bugün başında dünden önceki gün günlüklerinden silinecek.</span><span class="sxs-lookup"><span data-stu-id="90db0-137">For example, if you had a retention policy of one day, at the beginning of the day today the logs from the day before yesterday would be deleted.</span></span>

<span data-ttu-id="90db0-138">Bu ayarlar Azure portalında bir kaynak için tanılama ayarları aracılığıyla, CLI komutları ve Azure PowerShell aracılığıyla veya aracılığıyla kolayca yapılandırılır [Azure İzleyici REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="90db0-138">These settings are easily configured via the diagnostic settings for a resource in the Azure portal, via Azure PowerShell and CLI commands, or via the [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>

> [!WARNING]
> <span data-ttu-id="90db0-139">Tanılama günlüklerini ve konuk işletim sistemi katmanından işlem kaynakları (örneğin, VM'ler veya Service Fabric) kullanım ölçümlerini [yapılandırması ve çıkışları seçimi için ayrı bir mekanizma](../azure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="90db0-139">Diagnostic logs and metrics for from the guest OS layer of Compute resources (for example, VMs or Service Fabric) use [a separate mechanism for configuration and selection of outputs](../azure-diagnostics.md).</span></span>
>
>

## <a name="how-to-enable-collection-of-resource-diagnostic-logs"></a><span data-ttu-id="90db0-140">Kaynağın tanılama günlüklerini koleksiyonunu etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="90db0-140">How to enable collection of resource diagnostic logs</span></span>
<span data-ttu-id="90db0-141">Kaynağın tanılama günlüklerini koleksiyonunu etkinleştirilebilir [bir Resource Manager şablonunda kaynak oluştururken bir parçası olarak](./monitoring-enable-diagnostic-logs-using-template.md) veya bir kaynak Portalı'nda bu kaynağın sayfasından oluşturulduktan sonra.</span><span class="sxs-lookup"><span data-stu-id="90db0-141">Collection of resource diagnostic logs can be enabled [as part of creating a resource in a Resource Manager template](./monitoring-enable-diagnostic-logs-using-template.md) or after a resource is created from that resource's page in the portal.</span></span> <span data-ttu-id="90db0-142">Azure PowerShell veya CLI komutları kullanarak ya da Azure İzleyici REST API'sini kullanarak herhangi bir noktada koleksiyonu de etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90db0-142">You can also enable collection at any point using Azure PowerShell or CLI commands, or using the Azure Monitor REST API.</span></span>

> [!TIP]
> <span data-ttu-id="90db0-143">Bu yönergeleri doğrudan her kaynak için geçerli olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="90db0-143">These instructions may not apply directly to every resource.</span></span> <span data-ttu-id="90db0-144">Bazı kaynak türleri için geçerli olmayabilir özel adımlarını anlamak için bu sayfanın sonundaki şema bağlantılara bakın.</span><span class="sxs-lookup"><span data-stu-id="90db0-144">See the schema links at the bottom of this page to understand special steps that may apply to certain resource types.</span></span>
>
>

### <a name="enable-collection-of-resource-diagnostic-logs-in-the-portal"></a><span data-ttu-id="90db0-145">Portaldaki kaynak tanılama günlükleri toplamayı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="90db0-145">Enable collection of resource diagnostic logs in the portal</span></span>
<span data-ttu-id="90db0-146">Bir kaynak için belirli bir kaynak giderek ya da Azure İzleyicisi gezinme oluşturulduktan sonra kaynak tanılama günlüklerini Azure portalında koleksiyonunu etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90db0-146">You can enable collection of resource diagnostic logs in the Azure portal after a resource has been created either by going to a specific resource or by navigating to Azure Monitor.</span></span> <span data-ttu-id="90db0-147">Bu Azure izleyicisini etkinleştirmek için:</span><span class="sxs-lookup"><span data-stu-id="90db0-147">To enable this via Azure Monitor:</span></span>

1. <span data-ttu-id="90db0-148">İçinde [Azure portal](http://portal.azure.com), Azure izleyicisine gidin ve tıklayın **tanılama ayarları**</span><span class="sxs-lookup"><span data-stu-id="90db0-148">In the [Azure portal](http://portal.azure.com), navigate to Azure Monitor and click on **Diagnostic Settings**</span></span>

    ![Azure İzleyicisi İzleme bölümü](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

2. <span data-ttu-id="90db0-150">İsteğe bağlı olarak kaynak grubu veya kaynak türü listeyi filtrelemek sonra tanılama ayarını ayarlamak istediğiniz kaynak'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="90db0-150">Optionally filter the list by resource group or resource type, then click on the resource for which you would like to set a diagnostic setting.</span></span>

3. <span data-ttu-id="90db0-151">Hiçbir ayar kaynağı varsa, sizden istenir bir ayar oluşturmak için seçtiğiniz.</span><span class="sxs-lookup"><span data-stu-id="90db0-151">If no settings exist on the resource you have selected, you are prompted to create a setting.</span></span> <span data-ttu-id="90db0-152">"Tanılamayı açın."'i tıklatın</span><span class="sxs-lookup"><span data-stu-id="90db0-152">Click "Turn on diagnostics."</span></span>

   ![Tanılama ayarını - ayar Ekle](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-none.png)

   <span data-ttu-id="90db0-154">Kaynak üzerinde var olan ayarları varsa, bu kaynak üzerinde zaten yapılandırılmış ayarları listesini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="90db0-154">If there are existing settings on the resource, you will see a list of settings already configured on this resource.</span></span> <span data-ttu-id="90db0-155">"Tanılama ayarını Ekle" yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="90db0-155">Click "Add diagnostic setting."</span></span>

   ![Tanılama ayarını ayarlar varolan - Ekle](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-multiple.png)

3. <span data-ttu-id="90db0-157">Ayar bir adı verin, veri göndermek ve hangi kaynak her hedefi için kullanılan yapılandırmak istediğiniz her hedef için kutuları işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="90db0-157">Give your setting a name, check the boxes for each destination to which you would like to send data, and configure which resource is used for each destination.</span></span> <span data-ttu-id="90db0-158">İsteğe bağlı olarak, bu günlükler kullanarak korumak için gün sayısını ayarlayın **bekletme (gün)** kaydırıcılar (yalnızca depolama hesabı hedef için geçerlidir).</span><span class="sxs-lookup"><span data-stu-id="90db0-158">Optionally, set a number of days to retain these logs by using the **Retention (days)** sliders (only applicable to the storage account destination).</span></span> <span data-ttu-id="90db0-159">Sıfır gün bekletme günlükleri süresiz olarak depolar.</span><span class="sxs-lookup"><span data-stu-id="90db0-159">A retention of zero days stores the logs indefinitely.</span></span>
   
   ![Tanılama ayarını ayarlar varolan - Ekle](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-configure.png)
    
4. <span data-ttu-id="90db0-161">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="90db0-161">Click **Save**.</span></span>

<span data-ttu-id="90db0-162">Birkaç dakika sonra yeni bir ayar bu kaynak için ayarları listesi görüntülenir ve yeni olay verilerini oluşturulan hemen tanılama günlüklerini belirtilen hedefe gönderilir.</span><span class="sxs-lookup"><span data-stu-id="90db0-162">After a few moments, the new setting appears in your list of settings for this resource, and diagnostic logs are sent to the specified destinations as soon as new event data is generated.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-powershell"></a><span data-ttu-id="90db0-163">PowerShell aracılığıyla kaynak tanılama günlükleri toplamayı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="90db0-163">Enable collection of resource diagnostic logs via PowerShell</span></span>
<span data-ttu-id="90db0-164">Azure PowerShell aracılığıyla kaynak tanılama günlükleri toplamayı etkinleştirmek için aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="90db0-164">To enable collection of resource diagnostic logs via Azure PowerShell, use the following commands:</span></span>

<span data-ttu-id="90db0-165">Tanılama günlüklerinin bir depolama hesabındaki depolama etkinleştirmek için bu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="90db0-165">To enable storage of diagnostic logs in a storage account, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
```

<span data-ttu-id="90db0-166">Depolama hesabı kimliği günlükleri göndermek istediğiniz depolama hesabını kaynak kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="90db0-166">The storage account ID is the resource ID for the storage account to which you want to send the logs.</span></span>

<span data-ttu-id="90db0-167">Bir olay hub'ına tanılama günlüklerini akışını etkinleştirmek için bu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="90db0-167">To enable streaming of diagnostic logs to an event hub, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your Service Bus rule id] -Enabled $true
```

<span data-ttu-id="90db0-168">Hizmet veri yolu kural kimliği bu biçiminde bir dizedir: `{Service Bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="90db0-168">The service bus rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`.</span></span>

<span data-ttu-id="90db0-169">Günlük analizi çalışma alanı için tanılama günlüklerinin gönderilmesine izin vermek için bu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="90db0-169">To enable sending of diagnostic logs to a Log Analytics workspace, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of the log analytics workspace] -Enabled $true
```

<span data-ttu-id="90db0-170">Aşağıdaki komutu kullanarak, günlük analizi çalışma alanı kaynak Kimliğini elde edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="90db0-170">You can obtain the resource ID of your Log Analytics workspace using the following command:</span></span>

```powershell
(Get-AzureRmOperationalInsightsWorkspace).ResourceId
```

<span data-ttu-id="90db0-171">Birden çok çıktı seçenekleri etkinleştirmek için bu parametreler birleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90db0-171">You can combine these parameters to enable multiple output options.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-cli"></a><span data-ttu-id="90db0-172">CLI aracılığıyla kaynak tanılama günlükleri toplamayı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="90db0-172">Enable collection of resource diagnostic logs via CLI</span></span>
<span data-ttu-id="90db0-173">Azure CLI aracılığıyla kaynak tanılama günlükleri toplamayı etkinleştirmek için aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="90db0-173">To enable collection of resource diagnostic logs via the Azure CLI, use the following commands:</span></span>

<span data-ttu-id="90db0-174">Tanılama günlüklerinin bir depolama hesabındaki depolama etkinleştirmek için bu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="90db0-174">To enable storage of diagnostic logs in a Storage Account, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
```

<span data-ttu-id="90db0-175">Depolama hesabı kimliği günlükleri göndermek istediğiniz depolama hesabını kaynak kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="90db0-175">The storage account ID is the resource ID for the storage account to which you want to send the logs.</span></span>

<span data-ttu-id="90db0-176">Bir olay hub'ına tanılama günlüklerini akışını etkinleştirmek için bu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="90db0-176">To enable streaming of diagnostic logs to an event hub, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
```

<span data-ttu-id="90db0-177">Hizmet veri yolu kural kimliği bu biçiminde bir dizedir: `{Service Bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="90db0-177">The service bus rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`.</span></span>

<span data-ttu-id="90db0-178">Günlük analizi çalışma alanı için tanılama günlüklerinin gönderilmesine izin vermek için bu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="90db0-178">To enable sending of diagnostic logs to a Log Analytics workspace, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of the log analytics workspace> --enabled true
```

<span data-ttu-id="90db0-179">Birden çok çıktı seçenekleri etkinleştirmek için bu parametreler birleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90db0-179">You can combine these parameters to enable multiple output options.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-rest-api"></a><span data-ttu-id="90db0-180">REST API aracılığıyla kaynak tanılama günlükleri toplamayı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="90db0-180">Enable collection of resource diagnostic logs via REST API</span></span>
<span data-ttu-id="90db0-181">Azure İzleyici REST API'sini kullanarak tanılama ayarlarını değiştirmek için bkz: [bu belgeyi](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span><span class="sxs-lookup"><span data-stu-id="90db0-181">To change diagnostic settings using the Azure Monitor REST API, see [this document](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span>

## <a name="manage-resource-diagnostic-settings-in-the-portal"></a><span data-ttu-id="90db0-182">Portaldaki kaynak tanılama ayarlarını yönet</span><span class="sxs-lookup"><span data-stu-id="90db0-182">Manage resource diagnostic settings in the portal</span></span>
<span data-ttu-id="90db0-183">Tüm kaynaklarınız tanılama ayarları ile ayarlandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="90db0-183">Ensure that all of your resources are set up with diagnostic settings.</span></span> <span data-ttu-id="90db0-184">Gidin **İzleyici** portal ve açık **tanılama ayarlarını**.</span><span class="sxs-lookup"><span data-stu-id="90db0-184">Navigate to **Monitor** in the portal and open **Diagnostic settings**.</span></span>

![Tanılama günlüklerini dikey penceresinde portalı](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-nav.png)

<span data-ttu-id="90db0-186">"Daha fazla Hizmetleri" öğesine tıklamanız gerekebilir izleme bölümü bulunamıyor.</span><span class="sxs-lookup"><span data-stu-id="90db0-186">You may have to click "More services" to find the Monitor section.</span></span>

<span data-ttu-id="90db0-187">Burada görebilirsiniz ve tanılaması etkin olup olmadığını görmek için tanılama ayarları destekleyen tüm kaynakları filtreleyin.</span><span class="sxs-lookup"><span data-stu-id="90db0-187">Here you can view and filter all resources that support diagnostic settings to see if they have diagnostics enabled.</span></span> <span data-ttu-id="90db0-188">Birden çok ayarları bir kaynak üzerinde ayarlanmış ve hangi depolama hesabı, olay hub'ları ad ve/veya veri akışının günlük analizi çalışma alanı denetleyin görmek için ayrıntıya inebilir.</span><span class="sxs-lookup"><span data-stu-id="90db0-188">You can also drill down to see if multiple settings are set on a resource and check which storage account, Event Hubs namespace, and/or Log Analytics workspace that data are flowing to.</span></span>

![Tanılama günlüklerini sonuçları portalında](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

<span data-ttu-id="90db0-190">Burada etkinleştir, devre dışı bırakmak veya seçilen kaynak için tanılama ayarlarınızı değiştirmek için tanılama ayarları görünümü oluşturan bir tanılama ayarı ekleme getirir.</span><span class="sxs-lookup"><span data-stu-id="90db0-190">Adding a diagnostic setting brings up the Diagnostic Settings view, where you can enable, disable, or modify your diagnostic settings for the selected resource.</span></span>

## <a name="supported-services-categories-and-schemas-for-resource-diagnostic-logs"></a><span data-ttu-id="90db0-191">Desteklenen hizmetler, kategoriler ve kaynak tanılama günlükleri için şemaları</span><span class="sxs-lookup"><span data-stu-id="90db0-191">Supported services, categories, and schemas for resource diagnostic logs</span></span>
<span data-ttu-id="90db0-192">[Bu makaleye bakın](monitoring-diagnostic-logs-schema.md) desteklenen Hizmetleri ve günlük kategorileri ve bu hizmetler tarafından kullanılan şemalar tam bir listesi.</span><span class="sxs-lookup"><span data-stu-id="90db0-192">[See this article](monitoring-diagnostic-logs-schema.md) for a complete list of supported services and the log categories and schemas used by those services.</span></span>

## <a name="next-steps"></a><span data-ttu-id="90db0-193">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="90db0-193">Next steps</span></span>

* [<span data-ttu-id="90db0-194">Akış kaynak tanılama günlüklerine **olay hub'ları**</span><span class="sxs-lookup"><span data-stu-id="90db0-194">Stream resource diagnostic logs to **Event Hubs**</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [<span data-ttu-id="90db0-195">Azure İzleyici REST API'sini kullanarak kaynak tanılama ayarlarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="90db0-195">Change resource diagnostic settings using the Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931931.aspx)
* [<span data-ttu-id="90db0-196">Günlük analizi ile Azure depolama biriminden günlüklerini analiz edin</span><span class="sxs-lookup"><span data-stu-id="90db0-196">Analyze logs from Azure storage with Log Analytics</span></span>](../log-analytics/log-analytics-azure-storage.md)
