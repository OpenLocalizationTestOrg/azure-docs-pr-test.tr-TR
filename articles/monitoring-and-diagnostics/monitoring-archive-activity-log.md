---
title: "Azure etkinlik günlüğü arşiv | Microsoft Docs"
description: "Bir depolama hesabı, uzun vadeli bekletme için Azure etkinlik günlüğü arşiv öğrenin."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/09/2016
ms.author: johnkem
ms.openlocfilehash: 0e3a5b84f57eac96249430fa1c2c4cc076c2926a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="archive-the-azure-activity-log"></a><span data-ttu-id="cf6f7-103">Arşiv Azure etkinlik günlüğü</span><span class="sxs-lookup"><span data-stu-id="cf6f7-103">Archive the Azure Activity Log</span></span>
<span data-ttu-id="cf6f7-104">Bu makalede, biz arşivlemek için Azure portal, PowerShell cmdlet'leri veya platformlar arası CLI nasıl kullanabileceğinizi gösterir, [ **Azure etkinlik günlüğü** ](monitoring-overview-activity-logs.md) depolama hesabındaki.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-104">In this article, we show how you can use the Azure portal, PowerShell Cmdlets, or Cross-Platform CLI to archive your [**Azure Activity Log**](monitoring-overview-activity-logs.md) in a storage account.</span></span> <span data-ttu-id="cf6f7-105">Bu seçenek, Denetim, statik çözümleme veya yedekleme (ile bekletme ilkesi üzerinde tam denetim) 90 gün daha uzun süre, etkinlik günlüğü korumak istiyorsanız kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-105">This option is useful if you would like to retain your Activity Log longer than 90 days (with full control over the retention policy) for audit, static analysis, or backup.</span></span> <span data-ttu-id="cf6f7-106">Yalnızca, olayları 90 gün boyunca Koru gerek isterseniz daha az, etkinlik günlüğü olaylarını arşivleme etkinleştirmeden Azure platform 90 gün boyunca tutulur bu yana bir depolama hesabına arşivleme ayarlamanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-106">If you only need to retain your events for 90 days or less you do not need to set up archival to a storage account, since Activity Log events are retained in the Azure platform for 90 days without enabling archival.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cf6f7-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="cf6f7-107">Prerequisites</span></span>
<span data-ttu-id="cf6f7-108">Başlamadan önce şunları gerçekleştirmeniz [depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account) etkinlik günlüğü arşiv.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-108">Before you begin, you need to [create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) to which you can archive your Activity Log.</span></span> <span data-ttu-id="cf6f7-109">Böylece daha iyi İzleme verilerine erişimi denetleyebilirsiniz içine depolanmış, diğer izleme olmayan verilere sahip varolan bir depolama hesabı kullanmamanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-109">We highly recommend that you do not use an existing storage account that has other, non-monitoring data stored in it so that you can better control access to monitoring data.</span></span> <span data-ttu-id="cf6f7-110">Tanılama günlüklerini ve ölçümler bir depolama hesabına arşivlemeye çalışıyorsunuz, ancak, merkezi bir konumda tüm izleme verilerini korumak için etkinlik günlüğü de bu depolama hesabını kullanmak için anlamlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-110">However, if you are also archiving Diagnostic Logs and metrics to a storage account, it may make sense to use that storage account for your Activity Log as well to keep all monitoring data in a central location.</span></span> <span data-ttu-id="cf6f7-111">Kullandığınız depolama hesabı, genel amaçlı depolama hesabı, blob storage hesabı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-111">The storage account you use must be a general purpose storage account, not a blob storage account.</span></span> <span data-ttu-id="cf6f7-112">Depolama hesabı ayarı yapılandıran kullanıcı her iki aboneliğin uygun RBAC erişime sahip olduğu sürece günlükleri yayma abonelik ile aynı abonelikte olması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-112">The storage account does not have to be in the same subscription as the subscription emitting logs as long as the user who configures the setting has appropriate RBAC access to both subscriptions.</span></span>

## <a name="log-profile"></a><span data-ttu-id="cf6f7-113">Günlük profili</span><span class="sxs-lookup"><span data-stu-id="cf6f7-113">Log Profile</span></span>
<span data-ttu-id="cf6f7-114">Aşağıdaki yöntemlerden birini kullanarak Etkinlik günlüğü arşivlemek için ayarladığınız **günlük profili** aboneliği.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-114">To archive the Activity Log using any of the methods below, you set the **Log Profile** for a subscription.</span></span> <span data-ttu-id="cf6f7-115">Günlük profili depolanan ya da akışı olayları ve çıkışları türünü tanımlar — depolama hesabı ve/veya olay hub'ı.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-115">The Log Profile defines the type of events that are stored or streamed and the outputs—storage account and/or event hub.</span></span> <span data-ttu-id="cf6f7-116">Ayrıca bir depolama hesabında depolanan olayları için bekletme ilkesi (tutulacağı gün sayısı) tanımlar.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-116">It also defines the retention policy (number of days to retain) for events stored in a storage account.</span></span> <span data-ttu-id="cf6f7-117">Bekletme İlkesi sıfır olarak ayarlanırsa, olaylar süresiz olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-117">If the retention policy is set to zero, events are stored indefinitely.</span></span> <span data-ttu-id="cf6f7-118">Aksi takdirde, bu 1 ile 2147483647 arasında herhangi bir değere ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-118">Otherwise, this can be set to any value between 1 and 2147483647.</span></span> <span data-ttu-id="cf6f7-119">Bekletme ilkeleri uygulanan başına günlük, olduğundan, ilke (UTC) dışında tutma sunulmuştur gün günlüklerinden gün sonunda silinir.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-119">Retention policies are applied per-day, so at the end of a day (UTC), logs from the day that is now beyond the retention policy will be deleted.</span></span> <span data-ttu-id="cf6f7-120">Örneğin, bir günlük bir Bekletme İlkesi nesneniz varsa, günün bugün başında dünden önceki gün günlüklerinden silinecek.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-120">For example, if you had a retention policy of one day, at the beginning of the day today the logs from the day before yesterday would be deleted.</span></span> <span data-ttu-id="cf6f7-121">[Daha fazla bilgiyi hakkında günlük profilleri burada](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile).</span><span class="sxs-lookup"><span data-stu-id="cf6f7-121">[You can read more about log profiles here](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile).</span></span> 

## <a name="archive-the-activity-log-using-the-portal"></a><span data-ttu-id="cf6f7-122">Portalı kullanarak Etkinlik günlüğü</span><span class="sxs-lookup"><span data-stu-id="cf6f7-122">Archive the Activity Log using the portal</span></span>
1. <span data-ttu-id="cf6f7-123">Portalı'nda tıklatın **etkinlik günlüğü** sol taraftaki gezinti bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-123">In the portal, click the **Activity Log** link on the left-side navigation.</span></span> <span data-ttu-id="cf6f7-124">Etkinlik günlüğü için bir bağlantı görmüyorsanız tıklatın **daha Hizmetleri** ilk bağlantı.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-124">If you don’t see a link for the Activity Log, click the **More Services** link first.</span></span>
   
    ![Etkinlik günlüğü dikey penceresine gidin](media/monitoring-archive-activity-log/act-log-portal-navigate.png)
2. <span data-ttu-id="cf6f7-126">Dikey pencerenin üstündeki **verme**.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-126">At the top of the blade, click **Export**.</span></span>
   
    ![Dışa Aktar düğmesini tıklatın](media/monitoring-archive-activity-log/act-log-portal-export-button.png)
3. <span data-ttu-id="cf6f7-128">Görüntülenen dikey penceresinde, onay kutusunu için **dışarı aktarma bir depolama hesabına** ve bir depolama hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-128">In the blade that appears, check the box for **Export to a storage account** and select a storage account.</span></span>
   
    ![Bir depolama hesabı ayarlama](media/monitoring-archive-activity-log/act-log-portal-export-blade.png)
4. <span data-ttu-id="cf6f7-130">Kaydırıcı veya metin kutusunu kullanarak, depolama hesabınızı etkinlik günlüğü olaylarını tutulmalıdır gün sayısı tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-130">Using the slider or text box, define a number of days for which Activity Log events should be kept in your storage account.</span></span> <span data-ttu-id="cf6f7-131">Verilerinizi süresiz olarak kalıcı'u depolama hesabına sahip tercih ederseniz, bu sayı sıfır olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-131">If you prefer to have your data persisted in the storage account indefinitely, set this number to zero.</span></span>
5. <span data-ttu-id="cf6f7-132">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-132">Click **Save**.</span></span>

## <a name="archive-the-activity-log-via-powershell"></a><span data-ttu-id="cf6f7-133">Arşiv PowerShell aracılığıyla etkinlik günlüğü</span><span class="sxs-lookup"><span data-stu-id="cf6f7-133">Archive the Activity Log via PowerShell</span></span>
```
Add-AzureRmLogProfile -Name my_log_profile -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus -RetentionInDays 180 -Categories Write,Delete,Action
```

| <span data-ttu-id="cf6f7-134">Özellik</span><span class="sxs-lookup"><span data-stu-id="cf6f7-134">Property</span></span> | <span data-ttu-id="cf6f7-135">Gerekli</span><span class="sxs-lookup"><span data-stu-id="cf6f7-135">Required</span></span> | <span data-ttu-id="cf6f7-136">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cf6f7-136">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cf6f7-137">StorageAccountId</span><span class="sxs-lookup"><span data-stu-id="cf6f7-137">StorageAccountId</span></span> |<span data-ttu-id="cf6f7-138">Hayır</span><span class="sxs-lookup"><span data-stu-id="cf6f7-138">No</span></span> |<span data-ttu-id="cf6f7-139">Kaynak Kimliği depolama hesabının etkinlik günlükleri kaydedilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-139">Resource ID of the Storage Account to which Activity Logs should be saved.</span></span> |
| <span data-ttu-id="cf6f7-140">Konumlar</span><span class="sxs-lookup"><span data-stu-id="cf6f7-140">Locations</span></span> |<span data-ttu-id="cf6f7-141">Evet</span><span class="sxs-lookup"><span data-stu-id="cf6f7-141">Yes</span></span> |<span data-ttu-id="cf6f7-142">Etkinlik günlüğü olaylarını toplamak istediğiniz bölgeler virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-142">Comma-separated list of regions for which you would like to collect Activity Log events.</span></span> <span data-ttu-id="cf6f7-143">Tüm bölgelerin bir listesi görüntüleyebilirsiniz [bu sayfasını ziyaret tarafından](https://azure.microsoft.com/en-us/regions) veya kullanarak [Azure Yönetimi REST API](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span><span class="sxs-lookup"><span data-stu-id="cf6f7-143">You can view a list of all regions [by visiting this page](https://azure.microsoft.com/en-us/regions) or by using [the Azure Management REST API](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span></span> |
| <span data-ttu-id="cf6f7-144">retentionInDays</span><span class="sxs-lookup"><span data-stu-id="cf6f7-144">RetentionInDays</span></span> |<span data-ttu-id="cf6f7-145">Evet</span><span class="sxs-lookup"><span data-stu-id="cf6f7-145">Yes</span></span> |<span data-ttu-id="cf6f7-146">Hangi olayların tutulacağını için 1 ile 2147483647 arasında gün sayısı.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-146">Number of days for which events should be retained, between 1 and 2147483647.</span></span> <span data-ttu-id="cf6f7-147">Sıfır değeri günlükleri süresiz olarak depolar (sürekli).</span><span class="sxs-lookup"><span data-stu-id="cf6f7-147">A value of zero stores the logs indefinitely (forever).</span></span> |
| <span data-ttu-id="cf6f7-148">Kategoriler</span><span class="sxs-lookup"><span data-stu-id="cf6f7-148">Categories</span></span> |<span data-ttu-id="cf6f7-149">Evet</span><span class="sxs-lookup"><span data-stu-id="cf6f7-149">Yes</span></span> |<span data-ttu-id="cf6f7-150">Toplanması gereken olay kategorileri virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-150">Comma-separated list of event categories that should be collected.</span></span> <span data-ttu-id="cf6f7-151">Olası değerler şunlardır: yazma, silme ve eylem.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-151">Possible values are Write, Delete, and Action.</span></span> |

## <a name="archive-the-activity-log-via-cli"></a><span data-ttu-id="cf6f7-152">Arşiv CLI yoluyla etkinlik günlüğü</span><span class="sxs-lookup"><span data-stu-id="cf6f7-152">Archive the Activity Log via CLI</span></span>
```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --locations global,westus,eastus,northeurope --retentionInDays 180 –categories Write,Delete,Action
```

| <span data-ttu-id="cf6f7-153">Özellik</span><span class="sxs-lookup"><span data-stu-id="cf6f7-153">Property</span></span> | <span data-ttu-id="cf6f7-154">Gerekli</span><span class="sxs-lookup"><span data-stu-id="cf6f7-154">Required</span></span> | <span data-ttu-id="cf6f7-155">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cf6f7-155">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cf6f7-156">ad</span><span class="sxs-lookup"><span data-stu-id="cf6f7-156">name</span></span> |<span data-ttu-id="cf6f7-157">Evet</span><span class="sxs-lookup"><span data-stu-id="cf6f7-157">Yes</span></span> |<span data-ttu-id="cf6f7-158">Günlük profilinin adı.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-158">Name of your log profile.</span></span> |
| <span data-ttu-id="cf6f7-159">storageId</span><span class="sxs-lookup"><span data-stu-id="cf6f7-159">storageId</span></span> |<span data-ttu-id="cf6f7-160">Hayır</span><span class="sxs-lookup"><span data-stu-id="cf6f7-160">No</span></span> |<span data-ttu-id="cf6f7-161">Kaynak Kimliği depolama hesabının etkinlik günlükleri kaydedilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-161">Resource ID of the Storage Account to which Activity Logs should be saved.</span></span> |
| <span data-ttu-id="cf6f7-162">Konumları</span><span class="sxs-lookup"><span data-stu-id="cf6f7-162">locations</span></span> |<span data-ttu-id="cf6f7-163">Evet</span><span class="sxs-lookup"><span data-stu-id="cf6f7-163">Yes</span></span> |<span data-ttu-id="cf6f7-164">Etkinlik günlüğü olaylarını toplamak istediğiniz bölgeler virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-164">Comma-separated list of regions for which you would like to collect Activity Log events.</span></span> <span data-ttu-id="cf6f7-165">Tüm bölgelerin bir listesi görüntüleyebilirsiniz [bu sayfasını ziyaret tarafından](https://azure.microsoft.com/en-us/regions) veya kullanarak [Azure Yönetimi REST API](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span><span class="sxs-lookup"><span data-stu-id="cf6f7-165">You can view a list of all regions [by visiting this page](https://azure.microsoft.com/en-us/regions) or by using [the Azure Management REST API](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span></span> |
| <span data-ttu-id="cf6f7-166">retentionInDays</span><span class="sxs-lookup"><span data-stu-id="cf6f7-166">retentionInDays</span></span> |<span data-ttu-id="cf6f7-167">Evet</span><span class="sxs-lookup"><span data-stu-id="cf6f7-167">Yes</span></span> |<span data-ttu-id="cf6f7-168">Hangi olayların tutulacağını için 1 ile 2147483647 arasında gün sayısı.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-168">Number of days for which events should be retained, between 1 and 2147483647.</span></span> <span data-ttu-id="cf6f7-169">Sıfır değeri günlükleri süresiz olarak depolar (sürekli).</span><span class="sxs-lookup"><span data-stu-id="cf6f7-169">A value of zero will store the logs indefinitely (forever).</span></span> |
| <span data-ttu-id="cf6f7-170">kategorileri</span><span class="sxs-lookup"><span data-stu-id="cf6f7-170">categories</span></span> |<span data-ttu-id="cf6f7-171">Evet</span><span class="sxs-lookup"><span data-stu-id="cf6f7-171">Yes</span></span> |<span data-ttu-id="cf6f7-172">Toplanması gereken olay kategorileri virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-172">Comma-separated list of event categories that should be collected.</span></span> <span data-ttu-id="cf6f7-173">Olası değerler şunlardır: yazma, silme ve eylem.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-173">Possible values are Write, Delete, and Action.</span></span> |

## <a name="storage-schema-of-the-activity-log"></a><span data-ttu-id="cf6f7-174">Etkinlik günlüğü depolama şeması</span><span class="sxs-lookup"><span data-stu-id="cf6f7-174">Storage schema of the Activity Log</span></span>
<span data-ttu-id="cf6f7-175">Arşivleme kurduktan sonra bir etkinlik günlüğü olay oluştuktan hemen sonra bir depolama kapsayıcısı depolama hesabında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-175">Once you have set up archival, a storage container will be created in the storage account as soon as an Activity Log event occurs.</span></span> <span data-ttu-id="cf6f7-176">Kapsayıcı içinde BLOB'ları, tanılama günlüklerini ve etkinlik günlüğü arasında aynı biçimde izleyin.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-176">The blobs within the container follow the same format across the Activity Log and Diagnostic Logs.</span></span> <span data-ttu-id="cf6f7-177">Bu BLOB'ları yapıdır:</span><span class="sxs-lookup"><span data-stu-id="cf6f7-177">The structure of these blobs is:</span></span>

> <span data-ttu-id="cf6f7-178">Öngörüler-işletimsel-günlükleri/name = varsayılan/ResourceId/ABONELİKLERİ = / {abonelik kimliği} / y = {dört basamaklı sayısal year} / m = {iki basamaklı sayısal ay} / d = {iki basamaklı sayısal günü} / h {iki basamaklı 24 saatlik hour}/m=00/PT1H.json =</span><span class="sxs-lookup"><span data-stu-id="cf6f7-178">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/{subscription ID}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="cf6f7-179">Örneğin, bir blob adı olabilir:</span><span class="sxs-lookup"><span data-stu-id="cf6f7-179">For example, a blob name might be:</span></span>

> <span data-ttu-id="cf6f7-180">insights-Operational-Logs/Name=default/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/y=2016/m=08/d=22/h=18/m=00/PT1H.JSON</span><span class="sxs-lookup"><span data-stu-id="cf6f7-180">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="cf6f7-181">Her bir PT1H.json blob JSON blobu blob URL'SİNDE belirtilen saat içinde gerçekleşen olayların içerir (örneğin h = 12).</span><span class="sxs-lookup"><span data-stu-id="cf6f7-181">Each PT1H.json blob contains a JSON blob of events that occurred within the hour specified in the blob URL (e.g. h=12).</span></span> <span data-ttu-id="cf6f7-182">Bunlar ortaya çıktığında mevcut saatte olayları PT1H.json dosyasına eklenir.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-182">During the present hour, events are appended to the PT1H.json file as they occur.</span></span> <span data-ttu-id="cf6f7-183">Dakika değeri (m 00 =) her zaman etkinlik günlüğü olaylarını tek tek bloblar saat başına ayrılmış bu yana 00.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-183">The minute value (m=00) is always 00, since Activity Log events are broken into individual blobs per hour.</span></span>

<span data-ttu-id="cf6f7-184">PT1H.json dosya içinde her olay bu biçim aşağıdaki "kayıtlar" dizisinde depolanır:</span><span class="sxs-lookup"><span data-stu-id="cf6f7-184">Within the PT1H.json file, each event is stored in the “records” array, following this format:</span></span>

```
{
    "records": [
        {
            "time": "2015-01-21T22:14:26.9792776Z",
            "resourceId": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
            "operationName": "microsoft.support/supporttickets/write",
            "category": "Write",
            "resultType": "Success",
            "resultSignature": "Succeeded.Created",
            "durationMs": 2826,
            "callerIpAddress": "111.111.111.11",
            "correlationId": "c776f9f4-36e5-4e0e-809b-c9b3c3fb62a8",
            "identity": {
                "authorization": {
                    "scope": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
                    "action": "microsoft.support/supporttickets/write",
                    "evidence": {
                        "role": "Subscription Admin"
                    }
                },
                "claims": {
                    "aud": "https://management.core.windows.net/",
                    "iss": "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",
                    "iat": "1421876371",
                    "nbf": "1421876371",
                    "exp": "1421880271",
                    "ver": "1.0",
                    "http://schemas.microsoft.com/identity/claims/tenantid": "1e8d8218-c5e7-4578-9acc-9abbd5d23315 ",
                    "http://schemas.microsoft.com/claims/authnmethodsreferences": "pwd",
                    "http://schemas.microsoft.com/identity/claims/objectidentifier": "2468adf0-8211-44e3-95xq-85137af64708",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "admin@contoso.com",
                    "puid": "20030000801A118C",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "9vckmEGF7zDKk1YzIY8k0t1_EAPaXoeHyPRn6f413zM",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname": "John",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname": "Smith",
                    "name": "John Smith",
                    "groups": "cacfe77c-e058-4712-83qw-f9b08849fd60,7f71d11d-4c41-4b23-99d2-d32ce7aa621c,31522864-0578-4ea0-9gdc-e66cc564d18c",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name": " admin@contoso.com",
                    "appid": "c44b4083-3bq0-49c1-b47d-974e53cbdf3c",
                    "appidacr": "2",
                    "http://schemas.microsoft.com/identity/claims/scope": "user_impersonation",
                    "http://schemas.microsoft.com/claims/authnclassreference": "1"
                }
            },
            "level": "Information",
            "location": "global",
            "properties": {
                "statusCode": "Created",
                "serviceRequestId": "50d5cddb-8ca0-47ad-9b80-6cde2207f97c"
            }
        }
    ]
}
```


| <span data-ttu-id="cf6f7-185">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="cf6f7-185">Element name</span></span> | <span data-ttu-id="cf6f7-186">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cf6f7-186">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cf6f7-187">time</span><span class="sxs-lookup"><span data-stu-id="cf6f7-187">time</span></span> |<span data-ttu-id="cf6f7-188">Olay işleme olay karşılık gelen isteği Azure hizmeti tarafından oluşturulan zaman damgası.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-188">Timestamp when the event was generated by the Azure service processing the request corresponding the event.</span></span> |
| <span data-ttu-id="cf6f7-189">resourceId</span><span class="sxs-lookup"><span data-stu-id="cf6f7-189">resourceId</span></span> |<span data-ttu-id="cf6f7-190">Etkilenen kaynağının kaynak kimliği.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-190">Resource ID of the impacted resource.</span></span> |
| <span data-ttu-id="cf6f7-191">operationName</span><span class="sxs-lookup"><span data-stu-id="cf6f7-191">operationName</span></span> |<span data-ttu-id="cf6f7-192">İşlemin adı.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-192">Name of the operation.</span></span> |
| <span data-ttu-id="cf6f7-193">category</span><span class="sxs-lookup"><span data-stu-id="cf6f7-193">category</span></span> |<span data-ttu-id="cf6f7-194">Eylem kategorisi örn.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-194">Category of the action, eg.</span></span> <span data-ttu-id="cf6f7-195">Yazma, okuma, eylem.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-195">Write, Read, Action.</span></span> |
| <span data-ttu-id="cf6f7-196">resultType</span><span class="sxs-lookup"><span data-stu-id="cf6f7-196">resultType</span></span> |<span data-ttu-id="cf6f7-197">Sonuç türü örn.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-197">The type of the result, eg.</span></span> <span data-ttu-id="cf6f7-198">Başarılı, başarısız, Başlat</span><span class="sxs-lookup"><span data-stu-id="cf6f7-198">Success, Failure, Start</span></span> |
| <span data-ttu-id="cf6f7-199">resultSignature</span><span class="sxs-lookup"><span data-stu-id="cf6f7-199">resultSignature</span></span> |<span data-ttu-id="cf6f7-200">Kaynak türüne bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-200">Depends on the resource type.</span></span> |
| <span data-ttu-id="cf6f7-201">durationMs</span><span class="sxs-lookup"><span data-stu-id="cf6f7-201">durationMs</span></span> |<span data-ttu-id="cf6f7-202">Milisaniye cinsinden işlem süresi</span><span class="sxs-lookup"><span data-stu-id="cf6f7-202">Duration of the operation in milliseconds</span></span> |
| <span data-ttu-id="cf6f7-203">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="cf6f7-203">callerIpAddress</span></span> |<span data-ttu-id="cf6f7-204">İşlem, UPN Talebi veya kullanılabilirliğine göre SPN talep yürüttü kullanıcının IP adresi.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-204">IP address of the user who has performed the operation, UPN claim, or SPN claim based on availability.</span></span> |
| <span data-ttu-id="cf6f7-205">correlationId</span><span class="sxs-lookup"><span data-stu-id="cf6f7-205">correlationId</span></span> |<span data-ttu-id="cf6f7-206">Genellikle bir GUID dize biçiminde.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-206">Usually a GUID in the string format.</span></span> <span data-ttu-id="cf6f7-207">Bir correlationıd değeri paylaşan olayları aynı uber eyleme ait.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-207">Events that share a correlationId belong to the same uber action.</span></span> |
| <span data-ttu-id="cf6f7-208">identity</span><span class="sxs-lookup"><span data-stu-id="cf6f7-208">identity</span></span> |<span data-ttu-id="cf6f7-209">Yetkilendirme ve talep tanımlayan JSON blobu.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-209">JSON blob describing the authorization and claims.</span></span> |
| <span data-ttu-id="cf6f7-210">Yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="cf6f7-210">authorization</span></span> |<span data-ttu-id="cf6f7-211">BLOB olay RBAC özelliklerinin.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-211">Blob of RBAC properties of the event.</span></span> <span data-ttu-id="cf6f7-212">Genellikle "eylem", "rol" ve "scope" özellikleri içerir.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-212">Usually includes the “action”, “role” and “scope” properties.</span></span> |
| <span data-ttu-id="cf6f7-213">düzeyi</span><span class="sxs-lookup"><span data-stu-id="cf6f7-213">level</span></span> |<span data-ttu-id="cf6f7-214">Olay düzeyi.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-214">Level of the event.</span></span> <span data-ttu-id="cf6f7-215">Aşağıdaki değerlerden birini: "Kritik", "Error"Uyarı",", "Bilgi" ve "Ayrıntılı"</span><span class="sxs-lookup"><span data-stu-id="cf6f7-215">One of the following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="cf6f7-216">location</span><span class="sxs-lookup"><span data-stu-id="cf6f7-216">location</span></span> |<span data-ttu-id="cf6f7-217">Bölge konumu gerçekleştiği (veya genel).</span><span class="sxs-lookup"><span data-stu-id="cf6f7-217">Region in which the location occurred (or global).</span></span> |
| <span data-ttu-id="cf6f7-218">properties</span><span class="sxs-lookup"><span data-stu-id="cf6f7-218">properties</span></span> |<span data-ttu-id="cf6f7-219">Kümesi `<Key, Value>` olay ayrıntılarını açıklayan çiftleri (yani sözlük).</span><span class="sxs-lookup"><span data-stu-id="cf6f7-219">Set of `<Key, Value>` pairs (i.e. Dictionary) describing the details of the event.</span></span> |

> [!NOTE]
> <span data-ttu-id="cf6f7-220">Özellikleri ve bu özellikleri kullanımını kaynak bağlı olarak değişebilir.</span><span class="sxs-lookup"><span data-stu-id="cf6f7-220">The properties and usage of those properties can vary depending on the resource.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="cf6f7-221">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cf6f7-221">Next steps</span></span>
* [<span data-ttu-id="cf6f7-222">BLOB'ları çözümleme için karşıdan yükle</span><span class="sxs-lookup"><span data-stu-id="cf6f7-222">Download blobs for analysis</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)
* [<span data-ttu-id="cf6f7-223">Akış Event hubs'a etkinlik günlüğü</span><span class="sxs-lookup"><span data-stu-id="cf6f7-223">Stream the Activity Log to Event Hubs</span></span>](monitoring-stream-activity-logs-event-hubs.md)
* [<span data-ttu-id="cf6f7-224">Etkinlik günlüğü hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="cf6f7-224">Read more about the Activity Log</span></span>](monitoring-overview-activity-logs.md)

