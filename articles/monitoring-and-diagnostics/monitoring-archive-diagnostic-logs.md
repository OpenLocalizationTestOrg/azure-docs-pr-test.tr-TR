---
title: "aaaArchive Azure tanılama günlükleri | Microsoft Docs"
description: "Nasıl tooarchive bir depolama hesabı, uzun vadeli bekletme için Azure tanılama günlükleri öğrenin."
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
ms.openlocfilehash: bc9edbd3a649023a728b7fe77130dba2b6e6370d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="archive-azure-diagnostic-logs"></a><span data-ttu-id="31ca3-103">Arşiv Azure tanılama günlükleri</span><span class="sxs-lookup"><span data-stu-id="31ca3-103">Archive Azure Diagnostic Logs</span></span>
<span data-ttu-id="31ca3-104">Bu makalede, nasıl hello Azure portal, PowerShell cmdlet'leri, CLI, kullanın veya REST API tooarchive gösteriyoruz, [Azure tanılama günlüklerini](monitoring-overview-of-diagnostic-logs.md) depolama hesabındaki.</span><span class="sxs-lookup"><span data-stu-id="31ca3-104">In this article, we show how you can use hello Azure portal, PowerShell Cmdlets, CLI, or REST API tooarchive your [Azure diagnostic logs](monitoring-overview-of-diagnostic-logs.md) in a storage account.</span></span> <span data-ttu-id="31ca3-105">Bu seçenek, Denetim, statik çözümleme veya yedekleme için bir isteğe bağlı bekletme ilkesi ile tanılama günlükleri tooretain istiyorsanız yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="31ca3-105">This option is useful if you would like tooretain your diagnostic logs with an optional retention policy for audit, static analysis, or backup.</span></span> <span data-ttu-id="31ca3-106">Merhaba depolama hesabı hello toobe yok uygun RBAC erişim tooboth abonelikleri hello ayarı yapılandıran hello kullanıcının sahip olduğu sürece günlükleri yayma hello kaynak aynı abonelik.</span><span class="sxs-lookup"><span data-stu-id="31ca3-106">hello storage account does not have toobe in hello same subscription as hello resource emitting logs as long as hello user who configures hello setting has appropriate RBAC access tooboth subscriptions.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="31ca3-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="31ca3-107">Prerequisites</span></span>
<span data-ttu-id="31ca3-108">Başlamadan önce çok ihtiyacınız[depolama hesabı oluşturma](../storage/storage-create-storage-account.md) tanılama günlüklerinize arşiv toowhich.</span><span class="sxs-lookup"><span data-stu-id="31ca3-108">Before you begin, you need too[create a storage account](../storage/storage-create-storage-account.md) toowhich you can archive your diagnostic logs.</span></span> <span data-ttu-id="31ca3-109">Böylece daha iyi erişim toomonitoring veri denetimi içinde depolanmış, diğer izleme olmayan verilere sahip varolan bir depolama hesabı kullanmamanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="31ca3-109">We highly recommend that you do not use an existing storage account that has other, non-monitoring data stored in it so that you can better control access toomonitoring data.</span></span> <span data-ttu-id="31ca3-110">Ayrıca Tanılama ölçümleri tooa depolama hesabı ve etkinlik günlüğü arşivleme, tanılama tookeep de merkezi bir konumda tüm izleme verilerini günlükleri için ancak, bu algılama toouse bu depolama hesabı kalmasına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="31ca3-110">However, if you are also archiving your Activity Log and diagnostic metrics tooa storage account, it may make sense toouse that storage account for your diagnostic logs as well tookeep all monitoring data in a central location.</span></span> <span data-ttu-id="31ca3-111">kullandığınız hello depolama hesabı, genel amaçlı depolama hesabı, blob storage hesabı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="31ca3-111">hello storage account you use must be a general purpose storage account, not a blob storage account.</span></span>

## <a name="diagnostic-settings"></a><span data-ttu-id="31ca3-112">Tanılama ayarları</span><span class="sxs-lookup"><span data-stu-id="31ca3-112">Diagnostic settings</span></span>
<span data-ttu-id="31ca3-113">Merhaba aşağıdaki yöntemlerden birini kullanarak, tanılama günlüklerini tooarchive, ayarladığınız bir **tanılama ayarını** belirli bir kaynak için.</span><span class="sxs-lookup"><span data-stu-id="31ca3-113">tooarchive your diagnostic logs using any of hello methods below, you set a **diagnostic setting** for a particular resource.</span></span> <span data-ttu-id="31ca3-114">Kaynağın tanılama ayarını günlükleri hello kategorilerini tanımlar ve ölçüm verileri tooa hedef (depolama hesabı, olay hub'ları ad alanı veya günlük analizi) gönderilir.</span><span class="sxs-lookup"><span data-stu-id="31ca3-114">A diagnostic setting for a resource defines hello categories of logs and metric data sent tooa destination (storage account, Event Hubs namespace, or Log Analytics).</span></span> <span data-ttu-id="31ca3-115">Ayrıca her bir günlük kategorisi ve ölçüm verileri bir depolama hesabında depolanan olayları için hello bekletme ilkesi (gün tooretain sayısı) tanımlar.</span><span class="sxs-lookup"><span data-stu-id="31ca3-115">It also defines hello retention policy (number of days tooretain) for events of each log category and metric data stored in a storage account.</span></span> <span data-ttu-id="31ca3-116">Bir bekletme ilkesi toozero ayarlarsanız, bu günlüğü kategori olaylar (yani toosay, sonsuza kadar) süresiz olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="31ca3-116">If a retention policy is set toozero, events for that log category are stored indefinitely (that is toosay, forever).</span></span> <span data-ttu-id="31ca3-117">Bir bekletme ilkesi, aksi takdirde herhangi bir sayıda gün 1 ile 2147483647 arasında olabilir.</span><span class="sxs-lookup"><span data-stu-id="31ca3-117">A retention policy can otherwise be any number of days between 1 and 2147483647.</span></span> <span data-ttu-id="31ca3-118">[Daha fazla bilgiyi burada tanılama ayarları hakkında](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span><span class="sxs-lookup"><span data-stu-id="31ca3-118">[You can read more about diagnostic settings here](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span></span> <span data-ttu-id="31ca3-119">Bekletme ilkeleri uygulanan gün başına, hello bitiş saati (UTC) oturum şekilde hello bekletme ilkesi sunulmuştur hello günden silinir.</span><span class="sxs-lookup"><span data-stu-id="31ca3-119">Retention policies are applied per-day, so at hello end of a day (UTC), logs from hello day that is now beyond hello retention policy will be deleted.</span></span> <span data-ttu-id="31ca3-120">Bir günlük bir Bekletme İlkesi nesneniz varsa, örneğin, bugün hello günün hello başında hello hello gün dünden günlüklerinden silinecek</span><span class="sxs-lookup"><span data-stu-id="31ca3-120">For example, if you had a retention policy of one day, at hello beginning of hello day today hello logs from hello day before yesterday would be deleted</span></span>

## <a name="archive-diagnostic-logs-using-hello-portal"></a><span data-ttu-id="31ca3-121">Merhaba portal kullanarak arşiv tanılama günlükleri</span><span class="sxs-lookup"><span data-stu-id="31ca3-121">Archive diagnostic logs using hello portal</span></span>
1. <span data-ttu-id="31ca3-122">Merhaba portalında tooAzure İzleyici gidin ve tıklayın **tanılama ayarları**</span><span class="sxs-lookup"><span data-stu-id="31ca3-122">In hello portal, navigate tooAzure Monitor and click on **Diagnostic Settings**</span></span>

    ![Azure İzleyicisi İzleme bölümü](media/monitoring-archive-diagnostic-logs/diagnostic-settings-blade.png)

2. <span data-ttu-id="31ca3-124">İsteğe bağlı olarak kaynak grubu veya kaynak türü tarafından hello listesini filtrelemek ve tooset tanılama ayarını istediğiniz hello kaynakta'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="31ca3-124">Optionally filter hello list by resource group or resource type, then click on hello resource for which you would like tooset a diagnostic setting.</span></span>

3. <span data-ttu-id="31ca3-125">Hiçbir ayar seçmiş olduğunuz hello kaynakta mevcut, istendiğinde toocreate bir ayar demektir.</span><span class="sxs-lookup"><span data-stu-id="31ca3-125">If no settings exist on hello resource you have selected, you are prompted toocreate a setting.</span></span> <span data-ttu-id="31ca3-126">"Tanılamayı açın."'i tıklatın</span><span class="sxs-lookup"><span data-stu-id="31ca3-126">Click "Turn on diagnostics."</span></span>

   ![Tanılama ayarını - ayar Ekle](media/monitoring-archive-diagnostic-logs/diagnostic-settings-none.png)

   <span data-ttu-id="31ca3-128">Merhaba kaynakta mevcut ayarları varsa, bu kaynak üzerinde zaten yapılandırılmış ayarları listesini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="31ca3-128">If there are existing settings on hello resource, you will see a list of settings already configured on this resource.</span></span> <span data-ttu-id="31ca3-129">"Tanılama ayarını Ekle" yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="31ca3-129">Click "Add diagnostic setting."</span></span>

   ![Tanılama ayarını ayarlar varolan - Ekle](media/monitoring-archive-diagnostic-logs/diagnostic-settings-multiple.png)

3. <span data-ttu-id="31ca3-131">Ayarı, bir ad verin ve hello kutuyu **tooStorage hesap verme**, bir depolama hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="31ca3-131">Give your setting a name and check hello box for **Export tooStorage Account**, then select a storage account.</span></span> <span data-ttu-id="31ca3-132">İsteğe bağlı olarak, bu günlükler ayarlamak hello kullanarak birkaç gün tooretain **bekletme (gün)** kaydırıcılar.</span><span class="sxs-lookup"><span data-stu-id="31ca3-132">Optionally, set a number of days tooretain these logs by using hello **Retention (days)** sliders.</span></span> <span data-ttu-id="31ca3-133">Sıfır gün bekletme hello günlükleri süresiz olarak depolar.</span><span class="sxs-lookup"><span data-stu-id="31ca3-133">A retention of zero days stores hello logs indefinitely.</span></span>
   
   ![Tanılama ayarını ayarlar varolan - Ekle](media/monitoring-archive-diagnostic-logs/diagnostic-settings-configure.png)
    
4. <span data-ttu-id="31ca3-135">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="31ca3-135">Click **Save**.</span></span>

<span data-ttu-id="31ca3-136">Hello yeni ayar birkaç dakika sonra bu kaynak için ayarları listesi görüntülenir ve tanılama günlüklerin arşivlenmiş toothat depolama üretilen yeni olay verilerini hemen hesap.</span><span class="sxs-lookup"><span data-stu-id="31ca3-136">After a few moments, hello new setting appears in your list of settings for this resource, and diagnostic logs are archived toothat storage account as soon as new event data is generated.</span></span>

## <a name="archive-diagnostic-logs-via-azure-powershell"></a><span data-ttu-id="31ca3-137">Azure PowerShell aracılığıyla arşiv tanılama günlükleri</span><span class="sxs-lookup"><span data-stu-id="31ca3-137">Archive diagnostic logs via Azure PowerShell</span></span>
```
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg -StorageAccountId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Categories networksecuritygroupevent,networksecuritygrouprulecounter -Enabled $true -RetentionEnabled $true -RetentionInDays 90
```

| <span data-ttu-id="31ca3-138">Özellik</span><span class="sxs-lookup"><span data-stu-id="31ca3-138">Property</span></span> | <span data-ttu-id="31ca3-139">Gerekli</span><span class="sxs-lookup"><span data-stu-id="31ca3-139">Required</span></span> | <span data-ttu-id="31ca3-140">Açıklama</span><span class="sxs-lookup"><span data-stu-id="31ca3-140">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="31ca3-141">ResourceId</span><span class="sxs-lookup"><span data-stu-id="31ca3-141">ResourceId</span></span> |<span data-ttu-id="31ca3-142">Evet</span><span class="sxs-lookup"><span data-stu-id="31ca3-142">Yes</span></span> |<span data-ttu-id="31ca3-143">Kaynak Kimliği hello kaynağın tanılama ayarını tooset istiyor.</span><span class="sxs-lookup"><span data-stu-id="31ca3-143">Resource ID of hello resource on which you want tooset a diagnostic setting.</span></span> |
| <span data-ttu-id="31ca3-144">StorageAccountId</span><span class="sxs-lookup"><span data-stu-id="31ca3-144">StorageAccountId</span></span> |<span data-ttu-id="31ca3-145">Hayır</span><span class="sxs-lookup"><span data-stu-id="31ca3-145">No</span></span> |<span data-ttu-id="31ca3-146">Kaynak Kimliğini hello depolama hesabı toowhich tanılama günlüklerini kaydedilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="31ca3-146">Resource ID of hello Storage Account toowhich Diagnostic Logs should be saved.</span></span> |
| <span data-ttu-id="31ca3-147">Kategoriler</span><span class="sxs-lookup"><span data-stu-id="31ca3-147">Categories</span></span> |<span data-ttu-id="31ca3-148">Hayır</span><span class="sxs-lookup"><span data-stu-id="31ca3-148">No</span></span> |<span data-ttu-id="31ca3-149">Günlük kategorileri tooenable virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="31ca3-149">Comma-separated list of log categories tooenable.</span></span> |
| <span data-ttu-id="31ca3-150">Etkin</span><span class="sxs-lookup"><span data-stu-id="31ca3-150">Enabled</span></span> |<span data-ttu-id="31ca3-151">Evet</span><span class="sxs-lookup"><span data-stu-id="31ca3-151">Yes</span></span> |<span data-ttu-id="31ca3-152">Tanılama etkin veya bu kaynağa devre dışı olup olmadığını gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="31ca3-152">Boolean indicating whether diagnostics are enabled or disabled on this resource.</span></span> |
| <span data-ttu-id="31ca3-153">RetentionEnabled</span><span class="sxs-lookup"><span data-stu-id="31ca3-153">RetentionEnabled</span></span> |<span data-ttu-id="31ca3-154">Hayır</span><span class="sxs-lookup"><span data-stu-id="31ca3-154">No</span></span> |<span data-ttu-id="31ca3-155">Bir bekletme ilkesi bu kaynakta etkin olmadığını gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="31ca3-155">Boolean indicating if a retention policy are enabled on this resource.</span></span> |
| <span data-ttu-id="31ca3-156">retentionInDays</span><span class="sxs-lookup"><span data-stu-id="31ca3-156">RetentionInDays</span></span> |<span data-ttu-id="31ca3-157">Hayır</span><span class="sxs-lookup"><span data-stu-id="31ca3-157">No</span></span> |<span data-ttu-id="31ca3-158">Kendisi için olayları 1 ile 2147483647 arasında korunması gereken gün sayısı.</span><span class="sxs-lookup"><span data-stu-id="31ca3-158">Number of days for which events should be retained between 1 and 2147483647.</span></span> <span data-ttu-id="31ca3-159">Sıfır değeri hello günlükleri süresiz olarak depolar.</span><span class="sxs-lookup"><span data-stu-id="31ca3-159">A value of zero stores hello logs indefinitely.</span></span> |

## <a name="archive-diagnostic-logs-via-hello-cross-platform-cli"></a><span data-ttu-id="31ca3-160">Merhaba platformlar arası CLI aracılığıyla arşiv tanılama günlükleri</span><span class="sxs-lookup"><span data-stu-id="31ca3-160">Archive diagnostic logs via hello Cross-Platform CLI</span></span>
```
azure insights diagnostic set --resourceId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg --storageId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage –categories networksecuritygroupevent,networksecuritygrouprulecounter --enabled true
```

| <span data-ttu-id="31ca3-161">Özellik</span><span class="sxs-lookup"><span data-stu-id="31ca3-161">Property</span></span> | <span data-ttu-id="31ca3-162">Gerekli</span><span class="sxs-lookup"><span data-stu-id="31ca3-162">Required</span></span> | <span data-ttu-id="31ca3-163">Açıklama</span><span class="sxs-lookup"><span data-stu-id="31ca3-163">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="31ca3-164">resourceId</span><span class="sxs-lookup"><span data-stu-id="31ca3-164">resourceId</span></span> |<span data-ttu-id="31ca3-165">Evet</span><span class="sxs-lookup"><span data-stu-id="31ca3-165">Yes</span></span> |<span data-ttu-id="31ca3-166">Kaynak Kimliği hello kaynağın tanılama ayarını tooset istiyor.</span><span class="sxs-lookup"><span data-stu-id="31ca3-166">Resource ID of hello resource on which you want tooset a diagnostic setting.</span></span> |
| <span data-ttu-id="31ca3-167">storageId</span><span class="sxs-lookup"><span data-stu-id="31ca3-167">storageId</span></span> |<span data-ttu-id="31ca3-168">Hayır</span><span class="sxs-lookup"><span data-stu-id="31ca3-168">No</span></span> |<span data-ttu-id="31ca3-169">Kaynak Kimliği hello depolama hesabı toowhich tanılama günlüklerinin kaydedilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="31ca3-169">Resource ID of hello Storage Account toowhich diagnostic logs should be saved.</span></span> |
| <span data-ttu-id="31ca3-170">kategorileri</span><span class="sxs-lookup"><span data-stu-id="31ca3-170">categories</span></span> |<span data-ttu-id="31ca3-171">Hayır</span><span class="sxs-lookup"><span data-stu-id="31ca3-171">No</span></span> |<span data-ttu-id="31ca3-172">Günlük kategorileri tooenable virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="31ca3-172">Comma-separated list of log categories tooenable.</span></span> |
| <span data-ttu-id="31ca3-173">Etkin</span><span class="sxs-lookup"><span data-stu-id="31ca3-173">enabled</span></span> |<span data-ttu-id="31ca3-174">Evet</span><span class="sxs-lookup"><span data-stu-id="31ca3-174">Yes</span></span> |<span data-ttu-id="31ca3-175">Tanılama etkin veya bu kaynağa devre dışı olup olmadığını gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="31ca3-175">Boolean indicating whether diagnostics are enabled or disabled on this resource.</span></span> |

## <a name="archive-diagnostic-logs-via-hello-rest-api"></a><span data-ttu-id="31ca3-176">Merhaba REST API aracılığıyla arşiv tanılama günlükleri</span><span class="sxs-lookup"><span data-stu-id="31ca3-176">Archive diagnostic logs via hello REST API</span></span>
<span data-ttu-id="31ca3-177">[Bu belgede bakın](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings) hello Azure İzleyici REST API'sini kullanarak tanılama ayarlama nasıl ayarlanacağı hakkında bilgi için.</span><span class="sxs-lookup"><span data-stu-id="31ca3-177">[See this document](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings) for information on how you can set up a diagnostic setting using hello Azure Monitor REST API.</span></span>

## <a name="schema-of-diagnostic-logs-in-hello-storage-account"></a><span data-ttu-id="31ca3-178">Tanılama günlüklerini hello depolama hesabındaki şeması</span><span class="sxs-lookup"><span data-stu-id="31ca3-178">Schema of diagnostic logs in hello storage account</span></span>
<span data-ttu-id="31ca3-179">Arşivleme ayarlamış olduğunuz sonra etkinleştirdiğiniz hello günlük kategorilerden birini olay oluştuktan hemen sonra bir depolama kapsayıcısı hello depolama hesabı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="31ca3-179">Once you have set up archival, a storage container is created in hello storage account as soon as an event occurs in one of hello log categories you have enabled.</span></span> <span data-ttu-id="31ca3-180">Merhaba BLOB'lar hello kapsayıcı içindeki aynı arasında tanılama günlüklerini biçimi hello ve hello etkinlik günlüğü izleyin.</span><span class="sxs-lookup"><span data-stu-id="31ca3-180">hello blobs within hello container follow hello same format across Diagnostic Logs and hello Activity Log.</span></span> <span data-ttu-id="31ca3-181">Bu BLOB Hello yapıdır:</span><span class="sxs-lookup"><span data-stu-id="31ca3-181">hello structure of these blobs is:</span></span>

> <span data-ttu-id="31ca3-182">Öngörüler - günlükleri-{günlük kategori adı} / ResourceId = / ABONELİKLERİ / {abonelik kimliği} /RESOURCEGROUPS/ {kaynak grubu adı} /PROVIDERS/ {kaynak sağlayıcı adı} / {kaynak türü} / {kaynak adı} / y = {dört basamaklı sayısal year} / m = {iki basamaklı sayısal month} / d = {iki basamaklı sayısal günü} / h = {iki basamaklı 24 saatlik hour}/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="31ca3-182">insights-logs-{log category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/RESOURCEGROUPS/{resource group name}/PROVIDERS/{resource provider name}/{resource type}/{resource name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="31ca3-183">Veya daha basit bir şekilde</span><span class="sxs-lookup"><span data-stu-id="31ca3-183">Or, more simply,</span></span>

> <span data-ttu-id="31ca3-184">Öngörüler - günlükleri-{günlük kategori adı} / ResourceId = / {kaynak kimliği} / y = {dört basamaklı sayısal year} / m = {iki basamaklı sayısal month} / d = {iki basamaklı sayısal günü} / h = {iki basamaklı 24 saatlik hour}/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="31ca3-184">insights-logs-{log category name}/resourceId=/{resource Id}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="31ca3-185">Örneğin, bir blob adı olabilir:</span><span class="sxs-lookup"><span data-stu-id="31ca3-185">For example, a blob name might be:</span></span>

> <span data-ttu-id="31ca3-186">insights-logs-networksecuritygrouprulecounter/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUP/TESTNSG/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="31ca3-186">insights-logs-networksecuritygrouprulecounter/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUP/TESTNSG/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="31ca3-187">Her bir PT1H.json blob hello blob URL'SİNDE belirtilen hello saat içinde gerçekleşen olayların JSON blobu içerir (örneğin, h = 12).</span><span class="sxs-lookup"><span data-stu-id="31ca3-187">Each PT1H.json blob contains a JSON blob of events that occurred within hello hour specified in hello blob URL (for example, h=12).</span></span> <span data-ttu-id="31ca3-188">Bunlar ortaya çıktığında hello mevcut saat sırasında eklenmiş toohello PT1H.json dosya olaylardır.</span><span class="sxs-lookup"><span data-stu-id="31ca3-188">During hello present hour, events are appended toohello PT1H.json file as they occur.</span></span> <span data-ttu-id="31ca3-189">Merhaba dakika değeri (m 00 =) her zaman tanılama günlük olayları tek tek bloblar saat başına ayrılmış bu yana 00.</span><span class="sxs-lookup"><span data-stu-id="31ca3-189">hello minute value (m=00) is always 00, since diagnostic log events are broken into individual blobs per hour.</span></span>

<span data-ttu-id="31ca3-190">Merhaba PT1H.json dosyası içinde her olay bu biçim aşağıdaki hello "kayıtlar" dizisinde depolanır:</span><span class="sxs-lookup"><span data-stu-id="31ca3-190">Within hello PT1H.json file, each event is stored in hello “records” array, following this format:</span></span>

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

| <span data-ttu-id="31ca3-191">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="31ca3-191">Element name</span></span> | <span data-ttu-id="31ca3-192">Açıklama</span><span class="sxs-lookup"><span data-stu-id="31ca3-192">Description</span></span> |
| --- | --- |
| <span data-ttu-id="31ca3-193">time</span><span class="sxs-lookup"><span data-stu-id="31ca3-193">time</span></span> |<span data-ttu-id="31ca3-194">Merhaba olay hello Azure hizmetini işleme hello tarafından oluşturulan zaman damgası karşılık gelen hello olay isteği.</span><span class="sxs-lookup"><span data-stu-id="31ca3-194">Timestamp when hello event was generated by hello Azure service processing hello request corresponding hello event.</span></span> |
| <span data-ttu-id="31ca3-195">resourceId</span><span class="sxs-lookup"><span data-stu-id="31ca3-195">resourceId</span></span> |<span data-ttu-id="31ca3-196">Kaynak Kimliğini hello kaynak etkilenmiş.</span><span class="sxs-lookup"><span data-stu-id="31ca3-196">Resource ID of hello impacted resource.</span></span> |
| <span data-ttu-id="31ca3-197">operationName</span><span class="sxs-lookup"><span data-stu-id="31ca3-197">operationName</span></span> |<span data-ttu-id="31ca3-198">Merhaba işlemin adı.</span><span class="sxs-lookup"><span data-stu-id="31ca3-198">Name of hello operation.</span></span> |
| <span data-ttu-id="31ca3-199">category</span><span class="sxs-lookup"><span data-stu-id="31ca3-199">category</span></span> |<span data-ttu-id="31ca3-200">Merhaba olay günlüğü kategori.</span><span class="sxs-lookup"><span data-stu-id="31ca3-200">Log category of hello event.</span></span> |
| <span data-ttu-id="31ca3-201">properties</span><span class="sxs-lookup"><span data-stu-id="31ca3-201">properties</span></span> |<span data-ttu-id="31ca3-202">Kümesi `<Key, Value>` hello hello olay ayrıntılarını açıklayan çiftleri (yani sözlük).</span><span class="sxs-lookup"><span data-stu-id="31ca3-202">Set of `<Key, Value>` pairs (i.e. Dictionary) describing hello details of hello event.</span></span> |

> [!NOTE]
> <span data-ttu-id="31ca3-203">Merhaba özellikleri ve bu özellikleri kullanımını hello kaynak bağlı olarak değişebilir.</span><span class="sxs-lookup"><span data-stu-id="31ca3-203">hello properties and usage of those properties can vary depending on hello resource.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="31ca3-204">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="31ca3-204">Next steps</span></span>
* [<span data-ttu-id="31ca3-205">BLOB'ları çözümleme için karşıdan yükle</span><span class="sxs-lookup"><span data-stu-id="31ca3-205">Download blobs for analysis</span></span>](../storage/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="31ca3-206">Tooan olay hub'ları ad akış tanılama günlükleri</span><span class="sxs-lookup"><span data-stu-id="31ca3-206">Stream diagnostic logs tooan Event Hubs namespace</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [<span data-ttu-id="31ca3-207">Tanılama günlükleri hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="31ca3-207">Read more about diagnostic logs</span></span>](monitoring-overview-of-diagnostic-logs.md)
