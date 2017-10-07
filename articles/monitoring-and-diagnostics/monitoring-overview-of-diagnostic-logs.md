---
title: "Azure tanılama günlüklerinin aaaOverview | Microsoft Docs"
description: "Azure tanılama günlüklerini nedir ve nasıl bir Azure kaynağı içinde gerçekleşen toounderstand olayların kullanabilmek için öğrenin."
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
ms.openlocfilehash: e38991c540626b4bb5b5b9a995276881ee58f368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-and-consume-log-data-from-your-azure-resources"></a><span data-ttu-id="1e4cf-103">Toplamak ve Azure kaynaklarınızdan günlük verilerini kullanma</span><span class="sxs-lookup"><span data-stu-id="1e4cf-103">Collect and consume log data from your Azure resources</span></span>

## <a name="what-are-azure-resource-diagnostic-logs"></a><span data-ttu-id="1e4cf-104">Azure kaynak tanılama günlüklerini nelerdir</span><span class="sxs-lookup"><span data-stu-id="1e4cf-104">What are Azure resource diagnostic logs</span></span>
<span data-ttu-id="1e4cf-105">**Azure kaynak düzeyi tanılama günlüklerini** olan bir kaynak tarafından gösterilen günlükleri, zengin, sık hello işlemi bu kaynağın hakkında veriler sağlar.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-105">**Azure resource-level diagnostic logs** are logs emitted by a resource that provide rich, frequent data about hello operation of that resource.</span></span> <span data-ttu-id="1e4cf-106">Bu günlükler Merhaba içeriğine kaynak türüne göre değişir.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-106">hello content of these logs varies by resource type.</span></span> <span data-ttu-id="1e4cf-107">Örneğin, ağ güvenlik grubu kural sayaçları ve anahtar kasası denetimleri kaynak günlükleri iki kategorisi vardır.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-107">For example, Network Security Group rule counters and Key Vault audits are two categories of resource logs.</span></span>

<span data-ttu-id="1e4cf-108">Kaynak düzeyi tanılama günlükleri farklı hello [etkinlik günlüğü](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="1e4cf-108">Resource-level diagnostic logs differ from hello [Activity Log](monitoring-overview-activity-logs.md).</span></span> <span data-ttu-id="1e4cf-109">Merhaba etkinlik günlüğü kaynakları Kaynak Yöneticisi'ni kullanarak, örneğin, bir sanal makine oluşturma veya bir mantıksal uygulama silme gerçekleştirilen hello işlemleri hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-109">hello Activity Log provides insight into hello operations that were performed on resources in your subscription using Resource Manager, for example, creating a virtual machine or deleting a logic app.</span></span> <span data-ttu-id="1e4cf-110">Merhaba etkinlik günlüğü bir abonelik düzeyi günlüğü bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-110">hello Activity Log is a subscription-level log.</span></span> <span data-ttu-id="1e4cf-111">Kaynak düzeyi tanılama günlükleri, bu kaynak içinde kendisi, örneğin, gizli bir anahtar Kasası'nı alma gerçekleştirilen işlemler hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-111">Resource-level diagnostic logs provide insight into operations that were performed within that resource itself, for example, getting a secret from a Key Vault.</span></span>

<span data-ttu-id="1e4cf-112">Kaynak düzeyi tanılama günlüklerini de konuk işletim sistemi düzeyinde tanılama günlükleri farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-112">Resource-level diagnostic logs also differ from guest OS-level diagnostic logs.</span></span> <span data-ttu-id="1e4cf-113">Konuk işletim sistemi tanılama günlüklerini bu sanal makine içinde çalışan bir aracının tarafından toplanan veya diğer kaynak türü desteklenir.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-113">Guest OS diagnostic logs are those collected by an agent running inside of a virtual machine or other supported resource type.</span></span> <span data-ttu-id="1e4cf-114">Konuk işletim sistemi düzeyinde tanılama günlüklerini hello işletim sistemi ve sanal makine üzerinde çalışan uygulamalardan veri yakalama işlemi sırasında kaynak düzeyi tanılama günlüklerini hello Azure platformu kendisini hiçbir aracı ve yakalama kaynak özgü veri gerektirir.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-114">Resource-level diagnostic logs require no agent and capture resource-specific data from hello Azure platform itself, while guest OS-level diagnostic logs capture data from hello operating system and applications running on a virtual machine.</span></span>

<span data-ttu-id="1e4cf-115">Tüm kaynakları kaynak tanılama günlüklerini burada açıklanan yeni tür hello desteklemez.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-115">Not all resources support hello new type of resource diagnostic logs described here.</span></span> <span data-ttu-id="1e4cf-116">Bu makale, hangi kaynak türlerinin hello yeni kaynak düzeyi tanılama günlüklerini destek bölümüne listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-116">This article contains a section listing which resource types support hello new resource-level diagnostic logs.</span></span>

![<span data-ttu-id="1e4cf-117">Kaynağın tanılama günlükleri diğer türleri vs günlükleri</span><span class="sxs-lookup"><span data-stu-id="1e4cf-117">Resource diagnostics logs vs other types of logs</span></span> ](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_vs_other_logs_v5.png)

## <a name="what-you-can-do-with-resource-level-diagnostic-logs"></a><span data-ttu-id="1e4cf-118">Kaynak düzeyi tanılama günlükleri ile yapabilecekleriniz</span><span class="sxs-lookup"><span data-stu-id="1e4cf-118">What you can do with resource-level diagnostic logs</span></span>
<span data-ttu-id="1e4cf-119">Kaynağın tanılama günlükleri ile yapabileceğiniz hello şeylerden bazıları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1e4cf-119">Here are some of hello things you can do with resource diagnostic logs:</span></span>

![Kaynağın tanılama günlüklerinin mantıksal yerleştirme](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_Actions.png)


* <span data-ttu-id="1e4cf-121">Tooa kaydetmek [ **depolama hesabı** ](monitoring-archive-diagnostic-logs.md) denetim veya el ile İnceleme için.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-121">Save them tooa [**Storage Account**](monitoring-archive-diagnostic-logs.md) for auditing or manual inspection.</span></span> <span data-ttu-id="1e4cf-122">Merhaba bekletme süresi (gün) kullanarak belirtebilirsiniz **kaynak tanılama ayarlarını**.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-122">You can specify hello retention time (in days) using **resource diagnostic settings**.</span></span>
* <span data-ttu-id="1e4cf-123">[Çok akış**Event Hubs** ](monitoring-stream-diagnostic-logs-to-event-hubs.md) bir üçüncü taraf hizmeti veya Powerbı gibi özel analiz çözümü tarafından alımı için.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-123">[Stream them too**Event Hubs**](monitoring-stream-diagnostic-logs-to-event-hubs.md) for ingestion by a third-party service or custom analytics solution such as PowerBI.</span></span>
* <span data-ttu-id="1e4cf-124">Bunları ile analiz [OMS günlük analizi](../log-analytics/log-analytics-azure-storage.md)</span><span class="sxs-lookup"><span data-stu-id="1e4cf-124">Analyze them with [OMS Log Analytics](../log-analytics/log-analytics-azure-storage.md)</span></span>

<span data-ttu-id="1e4cf-125">Veya kullanımda olmayan olay hub'ları ad alanı hello aynı abonelik bir günlükleri yayma hello gibi bir depolama hesabı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-125">You can use a storage account or Event Hubs namespace that is not in hello same subscription as hello one emitting logs.</span></span> <span data-ttu-id="1e4cf-126">Merhaba ayarı yapılandıran hello kullanıcının hello uygun RBAC erişim tooboth abonelikleri olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-126">hello user who configures hello setting must have hello appropriate RBAC access tooboth subscriptions.</span></span>

## <a name="resource-diagnostic-settings"></a><span data-ttu-id="1e4cf-127">Kaynak tanılama ayarları</span><span class="sxs-lookup"><span data-stu-id="1e4cf-127">Resource diagnostic settings</span></span>
<span data-ttu-id="1e4cf-128">Kaynağın tanılama günlüklerini olmayan-kaynakları kaynak tanılama ayarları kullanılarak yapılandırılmış olan işlem.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-128">Resource diagnostic logs for non-Compute resources are configured using resource diagnostic settings.</span></span> <span data-ttu-id="1e4cf-129">**Kaynak tanılama ayarlarını** kaynak denetimi için:</span><span class="sxs-lookup"><span data-stu-id="1e4cf-129">**Resource diagnostic settings** for a resource control:</span></span>

* <span data-ttu-id="1e4cf-130">Kaynağın tanılama günlüklerini ve ölçümleri (depolama hesabı, olay hub'ları ve/veya OMS günlük analizi) gönderildiği.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-130">Where resource diagnostic logs and metrics are sent (Storage Account, Event Hubs, and/or OMS Log Analytics).</span></span>
* <span data-ttu-id="1e4cf-131">Günlük kategorilerini gönderilir ve ölçüm verileri de gönderilip.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-131">Which log categories are sent and whether metric data is also sent.</span></span>
* <span data-ttu-id="1e4cf-132">Her günlük kategori bir depolama hesabında ne kadar süre tutulacağını</span><span class="sxs-lookup"><span data-stu-id="1e4cf-132">How long each log category should be retained in a storage account</span></span>
    - <span data-ttu-id="1e4cf-133">Sıfır gün bekletme günlükleri sonsuza kadar tutulur anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-133">A retention of zero days means logs are kept forever.</span></span> <span data-ttu-id="1e4cf-134">Aksi takdirde hello değer 1 ile 2147483647 arasındaki gün herhangi bir sayıda olabilir.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-134">Otherwise, hello value can be any number of days between 1 and 2147483647.</span></span>
    - <span data-ttu-id="1e4cf-135">Bekletme ilkeleri ayarlanır, ancak yalnızca (örneğin, olay hub'ları veya OMS seçenekler seçilidir) günlükleri bir depolama hesabında depolama devre dışı bırakıldı, hello bekletme ilkeleri bir etkisi yoktur.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-135">If retention policies are set but storing logs in a Storage Account is disabled (for example, if only Event Hubs or OMS options are selected), hello retention policies have no effect.</span></span>
    - <span data-ttu-id="1e4cf-136">Bekletme ilkeleri uygulanan gün başına, hello bitiş saati (UTC) oturum şekilde hello bekletme ilkesi sunulmuştur hello günden silinir.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-136">Retention policies are applied per-day, so at hello end of a day (UTC), logs from hello day that is now beyond hello retention policy are deleted.</span></span> <span data-ttu-id="1e4cf-137">Bir günlük bir Bekletme İlkesi nesneniz varsa, örneğin, bugün hello günün hello başında hello hello gün dünden günlüklerinden silinecek.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-137">For example, if you had a retention policy of one day, at hello beginning of hello day today hello logs from hello day before yesterday would be deleted.</span></span>

<span data-ttu-id="1e4cf-138">Bu ayarlar hello hello Azure portalında bir kaynak için tanılama ayarları aracılığıyla, Azure PowerShell ve CLI komutları aracılığıyla veya hello aracılığıyla kolayca yapılandırılır [Azure İzleyici REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e4cf-138">These settings are easily configured via hello diagnostic settings for a resource in hello Azure portal, via Azure PowerShell and CLI commands, or via hello [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>

> [!WARNING]
> <span data-ttu-id="1e4cf-139">Tanılama günlüklerini ve hello konuk işletim sistemi katmanından işlem kaynakları (örneğin, VM'ler veya Service Fabric) kullanım ölçümlerini [yapılandırması ve çıkışları seçimi için ayrı bir mekanizma](../azure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="1e4cf-139">Diagnostic logs and metrics for from hello guest OS layer of Compute resources (for example, VMs or Service Fabric) use [a separate mechanism for configuration and selection of outputs](../azure-diagnostics.md).</span></span>
>
>

## <a name="how-tooenable-collection-of-resource-diagnostic-logs"></a><span data-ttu-id="1e4cf-140">Nasıl kaynak tanılama günlüklerini tooenable koleksiyonu</span><span class="sxs-lookup"><span data-stu-id="1e4cf-140">How tooenable collection of resource diagnostic logs</span></span>
<span data-ttu-id="1e4cf-141">Kaynağın tanılama günlüklerini koleksiyonunu etkinleştirilebilir [bir Resource Manager şablonunda kaynak oluştururken bir parçası olarak](./monitoring-enable-diagnostic-logs-using-template.md) veya bir kaynak hello Portalı'nda bu kaynağın sayfasından oluşturulduktan sonra.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-141">Collection of resource diagnostic logs can be enabled [as part of creating a resource in a Resource Manager template](./monitoring-enable-diagnostic-logs-using-template.md) or after a resource is created from that resource's page in hello portal.</span></span> <span data-ttu-id="1e4cf-142">Azure PowerShell veya CLI komutları veya hello Azure İzleyici REST API'sini kullanarak herhangi bir noktada koleksiyonu de etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-142">You can also enable collection at any point using Azure PowerShell or CLI commands, or using hello Azure Monitor REST API.</span></span>

> [!TIP]
> <span data-ttu-id="1e4cf-143">Bu yönergeleri tooevery kaynak doğrudan geçerli olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-143">These instructions may not apply directly tooevery resource.</span></span> <span data-ttu-id="1e4cf-144">Toocertain kaynak türleri uygulayabilir bu sayfa toounderstand özel adımlar hello sonundaki Hello şema bağlantılara bakın.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-144">See hello schema links at hello bottom of this page toounderstand special steps that may apply toocertain resource types.</span></span>
>
>

### <a name="enable-collection-of-resource-diagnostic-logs-in-hello-portal"></a><span data-ttu-id="1e4cf-145">Merhaba Portal'daki kaynak tanılama günlükleri toplamayı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="1e4cf-145">Enable collection of resource diagnostic logs in hello portal</span></span>
<span data-ttu-id="1e4cf-146">Tanılama günlükleri hello Azure kaynak koleksiyonunu etkinleştirebilirsiniz kaynak giderek tooa belirli bir kaynak tarafından ya da tooAzure İzleyici gezinme oluşturulduktan sonra portal.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-146">You can enable collection of resource diagnostic logs in hello Azure portal after a resource has been created either by going tooa specific resource or by navigating tooAzure Monitor.</span></span> <span data-ttu-id="1e4cf-147">tooenable Azure İzleyicisi aracılığıyla:</span><span class="sxs-lookup"><span data-stu-id="1e4cf-147">tooenable this via Azure Monitor:</span></span>

1. <span data-ttu-id="1e4cf-148">Merhaba, [Azure portal](http://portal.azure.com)tooAzure İzleyici gidin ve tıklayın **tanılama ayarları**</span><span class="sxs-lookup"><span data-stu-id="1e4cf-148">In hello [Azure portal](http://portal.azure.com), navigate tooAzure Monitor and click on **Diagnostic Settings**</span></span>

    ![Azure İzleyicisi İzleme bölümü](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

2. <span data-ttu-id="1e4cf-150">İsteğe bağlı olarak kaynak grubu veya kaynak türü tarafından hello listesini filtrelemek ve tooset tanılama ayarını istediğiniz hello kaynakta'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-150">Optionally filter hello list by resource group or resource type, then click on hello resource for which you would like tooset a diagnostic setting.</span></span>

3. <span data-ttu-id="1e4cf-151">Hiçbir ayar seçmiş olduğunuz hello kaynakta mevcut, istendiğinde toocreate bir ayar demektir.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-151">If no settings exist on hello resource you have selected, you are prompted toocreate a setting.</span></span> <span data-ttu-id="1e4cf-152">"Tanılamayı açın."'i tıklatın</span><span class="sxs-lookup"><span data-stu-id="1e4cf-152">Click "Turn on diagnostics."</span></span>

   ![Tanılama ayarını - ayar Ekle](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-none.png)

   <span data-ttu-id="1e4cf-154">Merhaba kaynakta mevcut ayarları varsa, bu kaynak üzerinde zaten yapılandırılmış ayarları listesini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-154">If there are existing settings on hello resource, you will see a list of settings already configured on this resource.</span></span> <span data-ttu-id="1e4cf-155">"Tanılama ayarını Ekle" yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-155">Click "Add diagnostic setting."</span></span>

   ![Tanılama ayarını ayarlar varolan - Ekle](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-multiple.png)

3. <span data-ttu-id="1e4cf-157">Ayar bir adı verin, her hedef toowhich toosend veri gibi ve hangi kaynak yapılandırmak her hedefi için kullanılan hello kutularını kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-157">Give your setting a name, check hello boxes for each destination toowhich you would like toosend data, and configure which resource is used for each destination.</span></span> <span data-ttu-id="1e4cf-158">İsteğe bağlı olarak, bu günlükler ayarlamak hello kullanarak birkaç gün tooretain **bekletme (gün)** kaydırıcılar (yalnızca geçerli toohello depolama hesabı hedef).</span><span class="sxs-lookup"><span data-stu-id="1e4cf-158">Optionally, set a number of days tooretain these logs by using hello **Retention (days)** sliders (only applicable toohello storage account destination).</span></span> <span data-ttu-id="1e4cf-159">Sıfır gün bekletme hello günlükleri süresiz olarak depolar.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-159">A retention of zero days stores hello logs indefinitely.</span></span>
   
   ![Tanılama ayarını ayarlar varolan - Ekle](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-configure.png)
    
4. <span data-ttu-id="1e4cf-161">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-161">Click **Save**.</span></span>

<span data-ttu-id="1e4cf-162">Yeni olay verilerini oluşturulan hemen birkaç dakika sonra hello ayarı bu kaynak için ayarları listesi görüntülenir ve tanılama günlüklerini toohello gönderilen yeni hedefleri belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-162">After a few moments, hello new setting appears in your list of settings for this resource, and diagnostic logs are sent toohello specified destinations as soon as new event data is generated.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-powershell"></a><span data-ttu-id="1e4cf-163">PowerShell aracılığıyla kaynak tanılama günlükleri toplamayı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="1e4cf-163">Enable collection of resource diagnostic logs via PowerShell</span></span>
<span data-ttu-id="1e4cf-164">kaynağın tanılama günlüklerini Azure PowerShell, aşağıdaki komutları kullanın hello aracılığıyla tooenable koleksiyonu:</span><span class="sxs-lookup"><span data-stu-id="1e4cf-164">tooenable collection of resource diagnostic logs via Azure PowerShell, use hello following commands:</span></span>

<span data-ttu-id="1e4cf-165">bir depolama hesabında tanılama günlüklerinin tooenable depolama bu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="1e4cf-165">tooenable storage of diagnostic logs in a storage account, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
```

<span data-ttu-id="1e4cf-166">Merhaba depolama hesabı kimliği hello depolama hesabı toowhich toosend hello istediğiniz günlükleri oluşturmak için kaynak kimliği hello.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-166">hello storage account ID is hello resource ID for hello storage account toowhich you want toosend hello logs.</span></span>

<span data-ttu-id="1e4cf-167">Tanılama günlüklerini tooan event hub ' tooenable akış bu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="1e4cf-167">tooenable streaming of diagnostic logs tooan event hub, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your Service Bus rule id] -Enabled $true
```

<span data-ttu-id="1e4cf-168">Merhaba hizmet veri yolu kural kimliği: Bu biçim bir dizeyle: `{Service Bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-168">hello service bus rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`.</span></span>

<span data-ttu-id="1e4cf-169">Tanılama günlüklerini tooa günlük analizi çalışma alanının tooenable gönderme bu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="1e4cf-169">tooenable sending of diagnostic logs tooa Log Analytics workspace, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of hello log analytics workspace] -Enabled $true
```

<span data-ttu-id="1e4cf-170">Merhaba kaynak kimliği komutu aşağıdaki hello kullanarak günlük analizi çalışma alanınızın elde edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1e4cf-170">You can obtain hello resource ID of your Log Analytics workspace using hello following command:</span></span>

```powershell
(Get-AzureRmOperationalInsightsWorkspace).ResourceId
```

<span data-ttu-id="1e4cf-171">Bu parametreleri tooenable birden çok çıktı seçenekleri birleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-171">You can combine these parameters tooenable multiple output options.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-cli"></a><span data-ttu-id="1e4cf-172">CLI aracılığıyla kaynak tanılama günlükleri toplamayı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="1e4cf-172">Enable collection of resource diagnostic logs via CLI</span></span>
<span data-ttu-id="1e4cf-173">Kaynak tanılama günlüklerini hello Azure CLI aracılığıyla tooenable koleksiyonu hello aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="1e4cf-173">tooenable collection of resource diagnostic logs via hello Azure CLI, use hello following commands:</span></span>

<span data-ttu-id="1e4cf-174">bir depolama hesabında tanılama günlüklerinin tooenable depolama bu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="1e4cf-174">tooenable storage of diagnostic logs in a Storage Account, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
```

<span data-ttu-id="1e4cf-175">Merhaba depolama hesabı kimliği hello depolama hesabı toowhich toosend hello istediğiniz günlükleri oluşturmak için kaynak kimliği hello.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-175">hello storage account ID is hello resource ID for hello storage account toowhich you want toosend hello logs.</span></span>

<span data-ttu-id="1e4cf-176">Tanılama günlüklerini tooan event hub ' tooenable akış bu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="1e4cf-176">tooenable streaming of diagnostic logs tooan event hub, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
```

<span data-ttu-id="1e4cf-177">Merhaba hizmet veri yolu kural kimliği: Bu biçim bir dizeyle: `{Service Bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-177">hello service bus rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`.</span></span>

<span data-ttu-id="1e4cf-178">Tanılama günlüklerini tooa günlük analizi çalışma alanının tooenable gönderme bu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="1e4cf-178">tooenable sending of diagnostic logs tooa Log Analytics workspace, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of hello log analytics workspace> --enabled true
```

<span data-ttu-id="1e4cf-179">Bu parametreleri tooenable birden çok çıktı seçenekleri birleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-179">You can combine these parameters tooenable multiple output options.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-rest-api"></a><span data-ttu-id="1e4cf-180">REST API aracılığıyla kaynak tanılama günlükleri toplamayı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="1e4cf-180">Enable collection of resource diagnostic logs via REST API</span></span>
<span data-ttu-id="1e4cf-181">Hello Azure İzleyici REST API'sini kullanarak toochange tanılama ayarlarını bkz [bu belgeyi](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e4cf-181">toochange diagnostic settings using hello Azure Monitor REST API, see [this document](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span>

## <a name="manage-resource-diagnostic-settings-in-hello-portal"></a><span data-ttu-id="1e4cf-182">Merhaba Portal'daki kaynak tanılama ayarlarını yönet</span><span class="sxs-lookup"><span data-stu-id="1e4cf-182">Manage resource diagnostic settings in hello portal</span></span>
<span data-ttu-id="1e4cf-183">Tüm kaynaklarınız tanılama ayarları ile ayarlandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-183">Ensure that all of your resources are set up with diagnostic settings.</span></span> <span data-ttu-id="1e4cf-184">Çok gidin**İzleyici** hello portal ve açık olarak **tanılama ayarlarını**.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-184">Navigate too**Monitor** in hello portal and open **Diagnostic settings**.</span></span>

![Tanılama günlüklerini dikey penceresinde hello portalı](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-nav.png)

<span data-ttu-id="1e4cf-186">"Daha fazla Hizmetleri" toofind hello İzleyici bölümüne tooclick olabilir.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-186">You may have tooclick "More services" toofind hello Monitor section.</span></span>

<span data-ttu-id="1e4cf-187">Burada görebilirsiniz ve tanılama ayarlarını toosee tanılaması etkin varsa destekleyen tüm kaynakları filtreleyin.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-187">Here you can view and filter all resources that support diagnostic settings toosee if they have diagnostics enabled.</span></span> <span data-ttu-id="1e4cf-188">Ayrıca, birden çok ayarları bir kaynakta ayarlandıysa toosee incelemek ve hangi depolama hesabı, olay hub'ları ad ve/veya veri akışının günlük analizi çalışma alanı denetleyin.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-188">You can also drill down toosee if multiple settings are set on a resource and check which storage account, Event Hubs namespace, and/or Log Analytics workspace that data are flowing to.</span></span>

![Tanılama günlüklerini sonuçları portalında](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

<span data-ttu-id="1e4cf-190">Merhaba burada etkinleştir, devre dışı bırakmak veya hello için tanılama ayarlarınızı değiştirmek için tanılama ayarları görünümü, Yukarı tanılama ayarını getirir ekleme kaynak seçtiniz.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-190">Adding a diagnostic setting brings up hello Diagnostic Settings view, where you can enable, disable, or modify your diagnostic settings for hello selected resource.</span></span>

## <a name="supported-services-categories-and-schemas-for-resource-diagnostic-logs"></a><span data-ttu-id="1e4cf-191">Desteklenen hizmetler, kategoriler ve kaynak tanılama günlükleri için şemaları</span><span class="sxs-lookup"><span data-stu-id="1e4cf-191">Supported services, categories, and schemas for resource diagnostic logs</span></span>
<span data-ttu-id="1e4cf-192">[Bu makaleye bakın](monitoring-diagnostic-logs-schema.md) desteklenen hizmetlerin ve hello günlük kategorileri ve bu hizmetler tarafından kullanılan şemalar tam bir listesi.</span><span class="sxs-lookup"><span data-stu-id="1e4cf-192">[See this article](monitoring-diagnostic-logs-schema.md) for a complete list of supported services and hello log categories and schemas used by those services.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e4cf-193">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1e4cf-193">Next steps</span></span>

* [<span data-ttu-id="1e4cf-194">Kaynağın tanılama günlükleri çok akış**olay hub'ları**</span><span class="sxs-lookup"><span data-stu-id="1e4cf-194">Stream resource diagnostic logs too**Event Hubs**</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [<span data-ttu-id="1e4cf-195">Hello Azure İzleyici REST API'sini kullanarak kaynak tanılama ayarlarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="1e4cf-195">Change resource diagnostic settings using hello Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931931.aspx)
* [<span data-ttu-id="1e4cf-196">Günlük analizi ile Azure depolama biriminden günlüklerini analiz edin</span><span class="sxs-lookup"><span data-stu-id="1e4cf-196">Analyze logs from Azure storage with Log Analytics</span></span>](../log-analytics/log-analytics-azure-storage.md)
