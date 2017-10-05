---
title: "Arşiv Azure tanılama günlüklerini | Microsoft Docs"
description: "Azure tanılama günlüklerinize bir depolama hesabı, uzun vadeli bekletme için arşiv öğrenin."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 3a55c73f-2ef3-45f3-8956-bcf9c0cb7e05
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem
ms.openlocfilehash: dbc5f89001dcb6cd1ab061cb0a9632e4e5d2c1c7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="archive-azure-diagnostic-logs"></a><span data-ttu-id="2445a-103">Arşiv Azure tanılama günlükleri</span><span class="sxs-lookup"><span data-stu-id="2445a-103">Archive Azure Diagnostic Logs</span></span>
<span data-ttu-id="2445a-104">Bu makalede, biz arşivlemek için Azure portal, PowerShell cmdlet'leri, CLI veya REST API nasıl kullanabileceğinizi gösterir, [Azure tanılama günlüklerini](monitoring-overview-of-diagnostic-logs.md) depolama hesabındaki.</span><span class="sxs-lookup"><span data-stu-id="2445a-104">In this article, we show how you can use the Azure portal, PowerShell Cmdlets, CLI, or REST API to archive your [Azure diagnostic logs](monitoring-overview-of-diagnostic-logs.md) in a storage account.</span></span> <span data-ttu-id="2445a-105">Bu seçenek, tanılama günlüklerinize denetim, statik çözümleme veya yedekleme için bir isteğe bağlı bekletme ilkesi ile korumak istiyorsanız kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="2445a-105">This option is useful if you would like to retain your diagnostic logs with an optional retention policy for audit, static analysis, or backup.</span></span> <span data-ttu-id="2445a-106">Depolama hesabı ayarı yapılandıran kullanıcı her iki aboneliğin uygun RBAC erişime sahip olduğu sürece günlükleri yayma kaynak ile aynı abonelikte olması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="2445a-106">The storage account does not have to be in the same subscription as the resource emitting logs as long as the user who configures the setting has appropriate RBAC access to both subscriptions.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2445a-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2445a-107">Prerequisites</span></span>
<span data-ttu-id="2445a-108">Başlamadan önce şunları gerçekleştirmeniz [depolama hesabı oluşturma](../storage/storage-create-storage-account.md) tanılama günlüklerinize arşiv.</span><span class="sxs-lookup"><span data-stu-id="2445a-108">Before you begin, you need to [create a storage account](../storage/storage-create-storage-account.md) to which you can archive your diagnostic logs.</span></span> <span data-ttu-id="2445a-109">Böylece daha iyi İzleme verilerine erişimi denetleyebilirsiniz içine depolanmış, diğer izleme olmayan verilere sahip varolan bir depolama hesabı kullanmamanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="2445a-109">We highly recommend that you do not use an existing storage account that has other, non-monitoring data stored in it so that you can better control access to monitoring data.</span></span> <span data-ttu-id="2445a-110">Ayrıca bir depolama hesabına tanılama ölçümleri ve etkinlik günlüğü arşivleme, ancak onu merkezi bir konumda tüm izleme verilerini korumak için tanılama günlükleri de bu depolama hesabını kullanmak için anlamlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="2445a-110">However, if you are also archiving your Activity Log and diagnostic metrics to a storage account, it may make sense to use that storage account for your diagnostic logs as well to keep all monitoring data in a central location.</span></span> <span data-ttu-id="2445a-111">Kullandığınız depolama hesabı, genel amaçlı depolama hesabı, blob storage hesabı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2445a-111">The storage account you use must be a general purpose storage account, not a blob storage account.</span></span>

## <a name="diagnostic-settings"></a><span data-ttu-id="2445a-112">Tanılama ayarları</span><span class="sxs-lookup"><span data-stu-id="2445a-112">Diagnostic settings</span></span>
<span data-ttu-id="2445a-113">Aşağıdaki yöntemlerden birini kullanarak tanılama günlüklerinize arşivlemek için ayarladığınız bir **tanılama ayarını** belirli bir kaynak için.</span><span class="sxs-lookup"><span data-stu-id="2445a-113">To archive your diagnostic logs using any of the methods below, you set a **diagnostic setting** for a particular resource.</span></span> <span data-ttu-id="2445a-114">Kaynağın tanılama ayarını kategorilerini günlükleri ve hedef için (depolama hesabı, olay hub'ları ad alanı veya günlük analizi) gönderilen ölçüm verileri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="2445a-114">A diagnostic setting for a resource defines the categories of logs and metric data sent to a destination (storage account, Event Hubs namespace, or Log Analytics).</span></span> <span data-ttu-id="2445a-115">Ayrıca her bir günlük kategorisi ve ölçüm verileri bir depolama hesabında depolanan olayları için bekletme ilkesi (tutulacağı gün sayısı) tanımlar.</span><span class="sxs-lookup"><span data-stu-id="2445a-115">It also defines the retention policy (number of days to retain) for events of each log category and metric data stored in a storage account.</span></span> <span data-ttu-id="2445a-116">Bir bekletme ilkesi sıfır olarak ayarlanırsa, bu günlüğü kategori olaylar (yani, sonsuza kadar söylemeniz) süresiz olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="2445a-116">If a retention policy is set to zero, events for that log category are stored indefinitely (that is to say, forever).</span></span> <span data-ttu-id="2445a-117">Bir bekletme ilkesi, aksi takdirde herhangi bir sayıda gün 1 ile 2147483647 arasında olabilir.</span><span class="sxs-lookup"><span data-stu-id="2445a-117">A retention policy can otherwise be any number of days between 1 and 2147483647.</span></span> <span data-ttu-id="2445a-118">[Daha fazla bilgiyi burada tanılama ayarları hakkında](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span><span class="sxs-lookup"><span data-stu-id="2445a-118">[You can read more about diagnostic settings here](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span></span> <span data-ttu-id="2445a-119">Bekletme ilkeleri uygulanan başına günlük, olduğundan, ilke (UTC) dışında tutma sunulmuştur gün günlüklerinden gün sonunda silinir.</span><span class="sxs-lookup"><span data-stu-id="2445a-119">Retention policies are applied per-day, so at the end of a day (UTC), logs from the day that is now beyond the retention policy will be deleted.</span></span> <span data-ttu-id="2445a-120">Bir günlük bir Bekletme İlkesi nesneniz varsa, örneğin, günün bugün başında dünden önceki gün günlüklerinden silinecek</span><span class="sxs-lookup"><span data-stu-id="2445a-120">For example, if you had a retention policy of one day, at the beginning of the day today the logs from the day before yesterday would be deleted</span></span>

## <a name="archive-diagnostic-logs-using-the-portal"></a><span data-ttu-id="2445a-121">Portalı kullanarak arşiv tanılama günlükleri</span><span class="sxs-lookup"><span data-stu-id="2445a-121">Archive diagnostic logs using the portal</span></span>
1. <span data-ttu-id="2445a-122">Portal, Azure izleyicisine gidin ve tıklayın **tanılama ayarları**</span><span class="sxs-lookup"><span data-stu-id="2445a-122">In the portal, navigate to Azure Monitor and click on **Diagnostic Settings**</span></span>

    ![Azure İzleyicisi İzleme bölümü](media/monitoring-archive-diagnostic-logs/diagnostic-settings-blade.png)

2. <span data-ttu-id="2445a-124">İsteğe bağlı olarak kaynak grubu veya kaynak türü listeyi filtrelemek sonra tanılama ayarını ayarlamak istediğiniz kaynak'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="2445a-124">Optionally filter the list by resource group or resource type, then click on the resource for which you would like to set a diagnostic setting.</span></span>

3. <span data-ttu-id="2445a-125">Hiçbir ayar kaynağı varsa, sizden istenir bir ayar oluşturmak için seçtiğiniz.</span><span class="sxs-lookup"><span data-stu-id="2445a-125">If no settings exist on the resource you have selected, you are prompted to create a setting.</span></span> <span data-ttu-id="2445a-126">"Tanılamayı açın."'i tıklatın</span><span class="sxs-lookup"><span data-stu-id="2445a-126">Click "Turn on diagnostics."</span></span>

   ![Tanılama ayarını - ayar Ekle](media/monitoring-archive-diagnostic-logs/diagnostic-settings-none.png)

   <span data-ttu-id="2445a-128">Kaynak üzerinde var olan ayarları varsa, bu kaynak üzerinde zaten yapılandırılmış ayarları listesini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="2445a-128">If there are existing settings on the resource, you will see a list of settings already configured on this resource.</span></span> <span data-ttu-id="2445a-129">"Tanılama ayarını Ekle" yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="2445a-129">Click "Add diagnostic setting."</span></span>

   ![Tanılama ayarını ayarlar varolan - Ekle](media/monitoring-archive-diagnostic-logs/diagnostic-settings-multiple.png)

3. <span data-ttu-id="2445a-131">Ayarı, bir ad verin ve için kutuyu **verme depolama hesabına**, bir depolama hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="2445a-131">Give your setting a name and check the box for **Export to Storage Account**, then select a storage account.</span></span> <span data-ttu-id="2445a-132">İsteğe bağlı olarak, bu günlükler kullanarak korumak için gün sayısını ayarlayın **bekletme (gün)** kaydırıcılar.</span><span class="sxs-lookup"><span data-stu-id="2445a-132">Optionally, set a number of days to retain these logs by using the **Retention (days)** sliders.</span></span> <span data-ttu-id="2445a-133">Sıfır gün bekletme günlükleri süresiz olarak depolar.</span><span class="sxs-lookup"><span data-stu-id="2445a-133">A retention of zero days stores the logs indefinitely.</span></span>
   
   ![Tanılama ayarını ayarlar varolan - Ekle](media/monitoring-archive-diagnostic-logs/diagnostic-settings-configure.png)
    
4. <span data-ttu-id="2445a-135">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2445a-135">Click **Save**.</span></span>

<span data-ttu-id="2445a-136">Birkaç dakika sonra yeni bir ayar bu kaynak için ayarları listesi görüntülenir ve yeni olay verilerini oluşturulan hemen bu depolama hesabına tanılama günlüklerini arşivlenir.</span><span class="sxs-lookup"><span data-stu-id="2445a-136">After a few moments, the new setting appears in your list of settings for this resource, and diagnostic logs are archived to that storage account as soon as new event data is generated.</span></span>

## <a name="archive-diagnostic-logs-via-azure-powershell"></a><span data-ttu-id="2445a-137">Azure PowerShell aracılığıyla arşiv tanılama günlükleri</span><span class="sxs-lookup"><span data-stu-id="2445a-137">Archive diagnostic logs via Azure PowerShell</span></span>
```
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg -StorageAccountId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Categories networksecuritygroupevent,networksecuritygrouprulecounter -Enabled $true -RetentionEnabled $true -RetentionInDays 90
```

| <span data-ttu-id="2445a-138">Özellik</span><span class="sxs-lookup"><span data-stu-id="2445a-138">Property</span></span> | <span data-ttu-id="2445a-139">Gerekli</span><span class="sxs-lookup"><span data-stu-id="2445a-139">Required</span></span> | <span data-ttu-id="2445a-140">Açıklama</span><span class="sxs-lookup"><span data-stu-id="2445a-140">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2445a-141">ResourceId</span><span class="sxs-lookup"><span data-stu-id="2445a-141">ResourceId</span></span> |<span data-ttu-id="2445a-142">Evet</span><span class="sxs-lookup"><span data-stu-id="2445a-142">Yes</span></span> |<span data-ttu-id="2445a-143">Kaynağın tanılama ayarını ayarlamak istediğiniz kaynak kimliği.</span><span class="sxs-lookup"><span data-stu-id="2445a-143">Resource ID of the resource on which you want to set a diagnostic setting.</span></span> |
| <span data-ttu-id="2445a-144">StorageAccountId</span><span class="sxs-lookup"><span data-stu-id="2445a-144">StorageAccountId</span></span> |<span data-ttu-id="2445a-145">Hayır</span><span class="sxs-lookup"><span data-stu-id="2445a-145">No</span></span> |<span data-ttu-id="2445a-146">Tanılama günlüklerini kaydedilmesi gereken depolama hesabının kaynak kimliği.</span><span class="sxs-lookup"><span data-stu-id="2445a-146">Resource ID of the Storage Account to which Diagnostic Logs should be saved.</span></span> |
| <span data-ttu-id="2445a-147">Kategoriler</span><span class="sxs-lookup"><span data-stu-id="2445a-147">Categories</span></span> |<span data-ttu-id="2445a-148">Hayır</span><span class="sxs-lookup"><span data-stu-id="2445a-148">No</span></span> |<span data-ttu-id="2445a-149">Etkinleştirmek için günlük kategorileri virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="2445a-149">Comma-separated list of log categories to enable.</span></span> |
| <span data-ttu-id="2445a-150">Etkin</span><span class="sxs-lookup"><span data-stu-id="2445a-150">Enabled</span></span> |<span data-ttu-id="2445a-151">Evet</span><span class="sxs-lookup"><span data-stu-id="2445a-151">Yes</span></span> |<span data-ttu-id="2445a-152">Tanılama etkin veya bu kaynağa devre dışı olup olmadığını gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="2445a-152">Boolean indicating whether diagnostics are enabled or disabled on this resource.</span></span> |
| <span data-ttu-id="2445a-153">RetentionEnabled</span><span class="sxs-lookup"><span data-stu-id="2445a-153">RetentionEnabled</span></span> |<span data-ttu-id="2445a-154">Hayır</span><span class="sxs-lookup"><span data-stu-id="2445a-154">No</span></span> |<span data-ttu-id="2445a-155">Bir bekletme ilkesi bu kaynakta etkin olmadığını gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="2445a-155">Boolean indicating if a retention policy are enabled on this resource.</span></span> |
| <span data-ttu-id="2445a-156">retentionInDays</span><span class="sxs-lookup"><span data-stu-id="2445a-156">RetentionInDays</span></span> |<span data-ttu-id="2445a-157">Hayır</span><span class="sxs-lookup"><span data-stu-id="2445a-157">No</span></span> |<span data-ttu-id="2445a-158">Kendisi için olayları 1 ile 2147483647 arasında korunması gereken gün sayısı.</span><span class="sxs-lookup"><span data-stu-id="2445a-158">Number of days for which events should be retained between 1 and 2147483647.</span></span> <span data-ttu-id="2445a-159">Sıfır değeri günlükleri süresiz olarak depolar.</span><span class="sxs-lookup"><span data-stu-id="2445a-159">A value of zero stores the logs indefinitely.</span></span> |

## <a name="archive-diagnostic-logs-via-the-cross-platform-cli"></a><span data-ttu-id="2445a-160">Platformlar arası CLI aracılığıyla arşiv tanılama günlükleri</span><span class="sxs-lookup"><span data-stu-id="2445a-160">Archive diagnostic logs via the Cross-Platform CLI</span></span>
```
azure insights diagnostic set --resourceId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg --storageId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage –categories networksecuritygroupevent,networksecuritygrouprulecounter --enabled true
```

| <span data-ttu-id="2445a-161">Özellik</span><span class="sxs-lookup"><span data-stu-id="2445a-161">Property</span></span> | <span data-ttu-id="2445a-162">Gerekli</span><span class="sxs-lookup"><span data-stu-id="2445a-162">Required</span></span> | <span data-ttu-id="2445a-163">Açıklama</span><span class="sxs-lookup"><span data-stu-id="2445a-163">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2445a-164">resourceId</span><span class="sxs-lookup"><span data-stu-id="2445a-164">resourceId</span></span> |<span data-ttu-id="2445a-165">Evet</span><span class="sxs-lookup"><span data-stu-id="2445a-165">Yes</span></span> |<span data-ttu-id="2445a-166">Kaynağın tanılama ayarını ayarlamak istediğiniz kaynak kimliği.</span><span class="sxs-lookup"><span data-stu-id="2445a-166">Resource ID of the resource on which you want to set a diagnostic setting.</span></span> |
| <span data-ttu-id="2445a-167">storageId</span><span class="sxs-lookup"><span data-stu-id="2445a-167">storageId</span></span> |<span data-ttu-id="2445a-168">Hayır</span><span class="sxs-lookup"><span data-stu-id="2445a-168">No</span></span> |<span data-ttu-id="2445a-169">Tanılama günlüklerini kaydedilmesi gereken depolama hesabının kaynak kimliği.</span><span class="sxs-lookup"><span data-stu-id="2445a-169">Resource ID of the Storage Account to which diagnostic logs should be saved.</span></span> |
| <span data-ttu-id="2445a-170">kategorileri</span><span class="sxs-lookup"><span data-stu-id="2445a-170">categories</span></span> |<span data-ttu-id="2445a-171">Hayır</span><span class="sxs-lookup"><span data-stu-id="2445a-171">No</span></span> |<span data-ttu-id="2445a-172">Etkinleştirmek için günlük kategorileri virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="2445a-172">Comma-separated list of log categories to enable.</span></span> |
| <span data-ttu-id="2445a-173">Etkin</span><span class="sxs-lookup"><span data-stu-id="2445a-173">enabled</span></span> |<span data-ttu-id="2445a-174">Evet</span><span class="sxs-lookup"><span data-stu-id="2445a-174">Yes</span></span> |<span data-ttu-id="2445a-175">Tanılama etkin veya bu kaynağa devre dışı olup olmadığını gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="2445a-175">Boolean indicating whether diagnostics are enabled or disabled on this resource.</span></span> |

## <a name="archive-diagnostic-logs-via-the-rest-api"></a><span data-ttu-id="2445a-176">REST API aracılığıyla arşiv tanılama günlükleri</span><span class="sxs-lookup"><span data-stu-id="2445a-176">Archive diagnostic logs via the REST API</span></span>
<span data-ttu-id="2445a-177">[Bu belgede bakın](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings) Azure İzleyici REST API'sini kullanarak tanılama ayarlama nasıl ayarlanacağı hakkında bilgi için.</span><span class="sxs-lookup"><span data-stu-id="2445a-177">[See this document](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings) for information on how you can set up a diagnostic setting using the Azure Monitor REST API.</span></span>

## <a name="schema-of-diagnostic-logs-in-the-storage-account"></a><span data-ttu-id="2445a-178">Tanılama günlüklerini depolama hesabındaki şeması</span><span class="sxs-lookup"><span data-stu-id="2445a-178">Schema of diagnostic logs in the storage account</span></span>
<span data-ttu-id="2445a-179">Arşivleme kurduktan sonra bir depolama kapsayıcısı etkinleştirdiğiniz günlük kategorilerden birini olay oluştuktan hemen sonra depolama hesabı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="2445a-179">Once you have set up archival, a storage container is created in the storage account as soon as an event occurs in one of the log categories you have enabled.</span></span> <span data-ttu-id="2445a-180">Kapsayıcı içinde BLOB'ları, tanılama günlüklerini ve etkinlik günlüğü arasında aynı biçimde izleyin.</span><span class="sxs-lookup"><span data-stu-id="2445a-180">The blobs within the container follow the same format across Diagnostic Logs and the Activity Log.</span></span> <span data-ttu-id="2445a-181">Bu BLOB'ları yapıdır:</span><span class="sxs-lookup"><span data-stu-id="2445a-181">The structure of these blobs is:</span></span>

> <span data-ttu-id="2445a-182">Öngörüler - günlükleri-{günlük kategori adı} / ResourceId = / ABONELİKLERİ / {abonelik kimliği} /RESOURCEGROUPS/ {kaynak grubu adı} /PROVIDERS/ {kaynak sağlayıcı adı} / {kaynak türü} / {kaynak adı} / y = {dört basamaklı sayısal year} / m = {iki basamaklı sayısal month} / d = {iki basamaklı sayısal günü} / h = {iki basamaklı 24 saatlik hour}/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="2445a-182">insights-logs-{log category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/RESOURCEGROUPS/{resource group name}/PROVIDERS/{resource provider name}/{resource type}/{resource name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="2445a-183">Veya daha basit bir şekilde</span><span class="sxs-lookup"><span data-stu-id="2445a-183">Or, more simply,</span></span>

> <span data-ttu-id="2445a-184">Öngörüler - günlükleri-{günlük kategori adı} / ResourceId = / {kaynak kimliği} / y = {dört basamaklı sayısal year} / m = {iki basamaklı sayısal month} / d = {iki basamaklı sayısal günü} / h = {iki basamaklı 24 saatlik hour}/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="2445a-184">insights-logs-{log category name}/resourceId=/{resource Id}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="2445a-185">Örneğin, bir blob adı olabilir:</span><span class="sxs-lookup"><span data-stu-id="2445a-185">For example, a blob name might be:</span></span>

> <span data-ttu-id="2445a-186">insights-logs-networksecuritygrouprulecounter/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUP/TESTNSG/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="2445a-186">insights-logs-networksecuritygrouprulecounter/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUP/TESTNSG/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="2445a-187">Her bir PT1H.json blob JSON blobu blob URL'SİNDE belirtilen saat içinde gerçekleşen olayların içerir (örneğin, h = 12).</span><span class="sxs-lookup"><span data-stu-id="2445a-187">Each PT1H.json blob contains a JSON blob of events that occurred within the hour specified in the blob URL (for example, h=12).</span></span> <span data-ttu-id="2445a-188">Bunlar ortaya çıktığında mevcut saatte olayları PT1H.json dosyasına eklenir.</span><span class="sxs-lookup"><span data-stu-id="2445a-188">During the present hour, events are appended to the PT1H.json file as they occur.</span></span> <span data-ttu-id="2445a-189">Dakika değeri (m 00 =) her zaman tanılama günlük olayları tek tek bloblar saat başına ayrılmış bu yana 00.</span><span class="sxs-lookup"><span data-stu-id="2445a-189">The minute value (m=00) is always 00, since diagnostic log events are broken into individual blobs per hour.</span></span>

<span data-ttu-id="2445a-190">PT1H.json dosya içinde her olay bu biçim aşağıdaki "kayıtlar" dizisinde depolanır:</span><span class="sxs-lookup"><span data-stu-id="2445a-190">Within the PT1H.json file, each event is stored in the “records” array, following this format:</span></span>

```
{
    "records": [
        {
            "time": "2016-07-01T00:00:37.2040000Z",
            "systemId": "46cdbb41-cb9c-4f3d-a5b4-1d458d827ff1",
            "category": "NetworkSecurityGroupRuleCounter",
            "resourceId": "/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/TESTNSG",
            "operationName": "NetworkSecurityGroupCounters",
            "properties": {
                "vnetResourceGuid": "{12345678-9012-3456-7890-123456789012}",
                "subnetPrefix": "10.3.0.0/24",
                "macAddress": "000123456789",
                "ruleName": "/subscriptions/ s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg/securityRules/default-allow-rdp",
                "direction": "In",
                "type": "allow",
                "matchedConnections": 1988
            }
        }
    ]
}
```

| <span data-ttu-id="2445a-191">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="2445a-191">Element name</span></span> | <span data-ttu-id="2445a-192">Açıklama</span><span class="sxs-lookup"><span data-stu-id="2445a-192">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2445a-193">time</span><span class="sxs-lookup"><span data-stu-id="2445a-193">time</span></span> |<span data-ttu-id="2445a-194">Olay işleme olay karşılık gelen isteği Azure hizmeti tarafından oluşturulan zaman damgası.</span><span class="sxs-lookup"><span data-stu-id="2445a-194">Timestamp when the event was generated by the Azure service processing the request corresponding the event.</span></span> |
| <span data-ttu-id="2445a-195">resourceId</span><span class="sxs-lookup"><span data-stu-id="2445a-195">resourceId</span></span> |<span data-ttu-id="2445a-196">Etkilenen kaynağının kaynak kimliği.</span><span class="sxs-lookup"><span data-stu-id="2445a-196">Resource ID of the impacted resource.</span></span> |
| <span data-ttu-id="2445a-197">operationName</span><span class="sxs-lookup"><span data-stu-id="2445a-197">operationName</span></span> |<span data-ttu-id="2445a-198">İşlemin adı.</span><span class="sxs-lookup"><span data-stu-id="2445a-198">Name of the operation.</span></span> |
| <span data-ttu-id="2445a-199">category</span><span class="sxs-lookup"><span data-stu-id="2445a-199">category</span></span> |<span data-ttu-id="2445a-200">Olay günlüğü kategori.</span><span class="sxs-lookup"><span data-stu-id="2445a-200">Log category of the event.</span></span> |
| <span data-ttu-id="2445a-201">properties</span><span class="sxs-lookup"><span data-stu-id="2445a-201">properties</span></span> |<span data-ttu-id="2445a-202">Kümesi `<Key, Value>` olay ayrıntılarını açıklayan çiftleri (yani sözlük).</span><span class="sxs-lookup"><span data-stu-id="2445a-202">Set of `<Key, Value>` pairs (i.e. Dictionary) describing the details of the event.</span></span> |

> [!NOTE]
> <span data-ttu-id="2445a-203">Özellikleri ve bu özellikleri kullanımını kaynak bağlı olarak değişebilir.</span><span class="sxs-lookup"><span data-stu-id="2445a-203">The properties and usage of those properties can vary depending on the resource.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="2445a-204">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2445a-204">Next steps</span></span>
* [<span data-ttu-id="2445a-205">BLOB'ları çözümleme için karşıdan yükle</span><span class="sxs-lookup"><span data-stu-id="2445a-205">Download blobs for analysis</span></span>](../storage/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="2445a-206">Bir olay hub'ları ad alanına akış tanılama günlükleri</span><span class="sxs-lookup"><span data-stu-id="2445a-206">Stream diagnostic logs to an Event Hubs namespace</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [<span data-ttu-id="2445a-207">Tanılama günlükleri hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="2445a-207">Read more about diagnostic logs</span></span>](monitoring-overview-of-diagnostic-logs.md)
