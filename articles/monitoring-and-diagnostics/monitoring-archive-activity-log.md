---
title: "aaaArchive hello Azure etkinlik günlüğü | Microsoft Docs"
description: "Tooarchive Azure etkinliklerinizi nasıl oturum depolama hesabındaki uzun vadeli bekletme için öğrenin."
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
ms.openlocfilehash: 58c6d3a3a31398287f66f76999d48f2942ab5109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="archive-hello-azure-activity-log"></a><span data-ttu-id="ba941-103">Arşiv hello Azure etkinlik günlüğü</span><span class="sxs-lookup"><span data-stu-id="ba941-103">Archive hello Azure Activity Log</span></span>
<span data-ttu-id="ba941-104">Bu makalede, biz hello Azure portal, PowerShell cmdlet'lerini veya platformlar arası CLI tooarchive nasıl kullanabileceğinizi gösterir, [ **Azure etkinlik günlüğü** ](monitoring-overview-activity-logs.md) depolama hesabındaki.</span><span class="sxs-lookup"><span data-stu-id="ba941-104">In this article, we show how you can use hello Azure portal, PowerShell Cmdlets, or Cross-Platform CLI tooarchive your [**Azure Activity Log**](monitoring-overview-activity-logs.md) in a storage account.</span></span> <span data-ttu-id="ba941-105">Bu seçenek (ile Merhaba bekletme ilkesi üzerinde tam denetim) 90 gün boyunca daha uzun, etkinlik günlüğü, statik çözümleme denetim veya yedekleme tooretain istiyorsanız yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="ba941-105">This option is useful if you would like tooretain your Activity Log longer than 90 days (with full control over hello retention policy) for audit, static analysis, or backup.</span></span> <span data-ttu-id="ba941-106">Tooretain yalnızca gerekiyorsa, olayları 90 gün veya daha az, etkinlik günlüğü olaylarını arşivleme etkinleştirmeden hello Azure platformu 90 gün boyunca tutulur beri tooset arşivleme tooa depolama hesabı, gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="ba941-106">If you only need tooretain your events for 90 days or less you do not need tooset up archival tooa storage account, since Activity Log events are retained in hello Azure platform for 90 days without enabling archival.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ba941-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ba941-107">Prerequisites</span></span>
<span data-ttu-id="ba941-108">Başlamadan önce çok ihtiyacınız[depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account) arşiv etkinlik günlüğü toowhich.</span><span class="sxs-lookup"><span data-stu-id="ba941-108">Before you begin, you need too[create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) toowhich you can archive your Activity Log.</span></span> <span data-ttu-id="ba941-109">Böylece daha iyi erişim toomonitoring veri denetimi içinde depolanmış, diğer izleme olmayan verilere sahip varolan bir depolama hesabı kullanmamanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="ba941-109">We highly recommend that you do not use an existing storage account that has other, non-monitoring data stored in it so that you can better control access toomonitoring data.</span></span> <span data-ttu-id="ba941-110">Tanılama günlüklerini ve ölçümleri tooa depolama hesabı arşivlemeye çalışıyorsunuz, etkinlik günlüğü için de tookeep tüm izleme verilerini merkezi bir konumda ancak, bu algılama toouse bu depolama hesabı kalmasına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="ba941-110">However, if you are also archiving Diagnostic Logs and metrics tooa storage account, it may make sense toouse that storage account for your Activity Log as well tookeep all monitoring data in a central location.</span></span> <span data-ttu-id="ba941-111">kullandığınız hello depolama hesabı, genel amaçlı depolama hesabı, blob storage hesabı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ba941-111">hello storage account you use must be a general purpose storage account, not a blob storage account.</span></span> <span data-ttu-id="ba941-112">Merhaba depolama hesabı hello toobe yok uygun RBAC erişim tooboth abonelikleri hello ayarı yapılandıran hello kullanıcının sahip olduğu sürece günlükleri yayma hello abonelik aynı abonelik.</span><span class="sxs-lookup"><span data-stu-id="ba941-112">hello storage account does not have toobe in hello same subscription as hello subscription emitting logs as long as hello user who configures hello setting has appropriate RBAC access tooboth subscriptions.</span></span>

## <a name="log-profile"></a><span data-ttu-id="ba941-113">Günlük profili</span><span class="sxs-lookup"><span data-stu-id="ba941-113">Log Profile</span></span>
<span data-ttu-id="ba941-114">tooarchive hello etkinlik günlüğü hello aşağıdaki yöntemlerden birini kullanarak, ayarladığınız hello **günlük profili** aboneliği.</span><span class="sxs-lookup"><span data-stu-id="ba941-114">tooarchive hello Activity Log using any of hello methods below, you set hello **Log Profile** for a subscription.</span></span> <span data-ttu-id="ba941-115">Merhaba günlük profili hello depolanan ya da akışı olayların türünü tanımlar ve hello çıkışları — depolama hesabı ve/veya olay hub'ı.</span><span class="sxs-lookup"><span data-stu-id="ba941-115">hello Log Profile defines hello type of events that are stored or streamed and hello outputs—storage account and/or event hub.</span></span> <span data-ttu-id="ba941-116">Ayrıca bir depolama hesabında depolanan olayları için hello bekletme ilkesi (gün tooretain sayısı) tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ba941-116">It also defines hello retention policy (number of days tooretain) for events stored in a storage account.</span></span> <span data-ttu-id="ba941-117">Merhaba bekletme ilkesi toozero ayarlarsanız, olaylar süresiz olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="ba941-117">If hello retention policy is set toozero, events are stored indefinitely.</span></span> <span data-ttu-id="ba941-118">Aksi takdirde, bu tooany değerinin 1 ile 2147483647 arasında ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="ba941-118">Otherwise, this can be set tooany value between 1 and 2147483647.</span></span> <span data-ttu-id="ba941-119">Bekletme ilkeleri uygulanan gün başına, hello bitiş saati (UTC) oturum şekilde hello bekletme ilkesi sunulmuştur hello günden silinir.</span><span class="sxs-lookup"><span data-stu-id="ba941-119">Retention policies are applied per-day, so at hello end of a day (UTC), logs from hello day that is now beyond hello retention policy will be deleted.</span></span> <span data-ttu-id="ba941-120">Bir günlük bir Bekletme İlkesi nesneniz varsa, örneğin, bugün hello günün hello başında hello hello gün dünden günlüklerinden silinecek.</span><span class="sxs-lookup"><span data-stu-id="ba941-120">For example, if you had a retention policy of one day, at hello beginning of hello day today hello logs from hello day before yesterday would be deleted.</span></span> <span data-ttu-id="ba941-121">[Daha fazla bilgiyi hakkında günlük profilleri burada](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile).</span><span class="sxs-lookup"><span data-stu-id="ba941-121">[You can read more about log profiles here](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile).</span></span> 

## <a name="archive-hello-activity-log-using-hello-portal"></a><span data-ttu-id="ba941-122">Arşiv hello hello portal kullanarak Etkinlik günlüğü</span><span class="sxs-lookup"><span data-stu-id="ba941-122">Archive hello Activity Log using hello portal</span></span>
1. <span data-ttu-id="ba941-123">Merhaba Hello Portalı'nda tıklatın **etkinlik günlüğü** hello sol taraftaki gezinti bağlantısına.</span><span class="sxs-lookup"><span data-stu-id="ba941-123">In hello portal, click hello **Activity Log** link on hello left-side navigation.</span></span> <span data-ttu-id="ba941-124">Merhaba etkinlik günlüğü için bir bağlantı görmüyorsanız, hello tıklatın **daha Hizmetleri** ilk bağlantı.</span><span class="sxs-lookup"><span data-stu-id="ba941-124">If you don’t see a link for hello Activity Log, click hello **More Services** link first.</span></span>
   
    ![TooActivity günlük dikey gidin](media/monitoring-archive-activity-log/act-log-portal-navigate.png)
2. <span data-ttu-id="ba941-126">Merhaba dikey penceresinde Hello üstünde tıklatın **verme**.</span><span class="sxs-lookup"><span data-stu-id="ba941-126">At hello top of hello blade, click **Export**.</span></span>
   
    ![Merhaba Dışa Aktar düğmesini tıklatın](media/monitoring-archive-activity-log/act-log-portal-export-button.png)
3. <span data-ttu-id="ba941-128">Merhaba kutuyu için görünür hello dikey penceresinde, **verme tooa depolama hesabı** ve bir depolama hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="ba941-128">In hello blade that appears, check hello box for **Export tooa storage account** and select a storage account.</span></span>
   
    ![Bir depolama hesabı ayarlama](media/monitoring-archive-activity-log/act-log-portal-export-blade.png)
4. <span data-ttu-id="ba941-130">Merhaba kaydırıcı veya metin kutusunu kullanarak, depolama hesabınızı etkinlik günlüğü olaylarını tutulmalıdır gün sayısı tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="ba941-130">Using hello slider or text box, define a number of days for which Activity Log events should be kept in your storage account.</span></span> <span data-ttu-id="ba941-131">Verilerinizi hello depolama hesabında süresiz olarak kalıcı toohave tercih ederseniz, bu sayı toozero ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ba941-131">If you prefer toohave your data persisted in hello storage account indefinitely, set this number toozero.</span></span>
5. <span data-ttu-id="ba941-132">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ba941-132">Click **Save**.</span></span>

## <a name="archive-hello-activity-log-via-powershell"></a><span data-ttu-id="ba941-133">Arşiv hello PowerShell aracılığıyla etkinlik günlüğü</span><span class="sxs-lookup"><span data-stu-id="ba941-133">Archive hello Activity Log via PowerShell</span></span>
```
Add-AzureRmLogProfile -Name my_log_profile -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus -RetentionInDays 180 -Categories Write,Delete,Action
```

| <span data-ttu-id="ba941-134">Özellik</span><span class="sxs-lookup"><span data-stu-id="ba941-134">Property</span></span> | <span data-ttu-id="ba941-135">Gerekli</span><span class="sxs-lookup"><span data-stu-id="ba941-135">Required</span></span> | <span data-ttu-id="ba941-136">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ba941-136">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ba941-137">StorageAccountId</span><span class="sxs-lookup"><span data-stu-id="ba941-137">StorageAccountId</span></span> |<span data-ttu-id="ba941-138">Hayır</span><span class="sxs-lookup"><span data-stu-id="ba941-138">No</span></span> |<span data-ttu-id="ba941-139">Kaynak Kimliğini hello depolama hesabı toowhich etkinlik günlükleri kaydedilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="ba941-139">Resource ID of hello Storage Account toowhich Activity Logs should be saved.</span></span> |
| <span data-ttu-id="ba941-140">Konumlar</span><span class="sxs-lookup"><span data-stu-id="ba941-140">Locations</span></span> |<span data-ttu-id="ba941-141">Evet</span><span class="sxs-lookup"><span data-stu-id="ba941-141">Yes</span></span> |<span data-ttu-id="ba941-142">Toocollect etkinlik günlüğü olaylarını istediğiniz bölgeler virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="ba941-142">Comma-separated list of regions for which you would like toocollect Activity Log events.</span></span> <span data-ttu-id="ba941-143">Tüm bölgelerin bir listesi görüntüleyebilirsiniz [bu sayfasını ziyaret tarafından](https://azure.microsoft.com/en-us/regions) veya kullanarak [Azure Yönetimi REST API hello](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span><span class="sxs-lookup"><span data-stu-id="ba941-143">You can view a list of all regions [by visiting this page](https://azure.microsoft.com/en-us/regions) or by using [hello Azure Management REST API](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span></span> |
| <span data-ttu-id="ba941-144">retentionInDays</span><span class="sxs-lookup"><span data-stu-id="ba941-144">RetentionInDays</span></span> |<span data-ttu-id="ba941-145">Evet</span><span class="sxs-lookup"><span data-stu-id="ba941-145">Yes</span></span> |<span data-ttu-id="ba941-146">Hangi olayların tutulacağını için 1 ile 2147483647 arasında gün sayısı.</span><span class="sxs-lookup"><span data-stu-id="ba941-146">Number of days for which events should be retained, between 1 and 2147483647.</span></span> <span data-ttu-id="ba941-147">Sıfır değeri hello günlükleri süresiz olarak depolar (sürekli).</span><span class="sxs-lookup"><span data-stu-id="ba941-147">A value of zero stores hello logs indefinitely (forever).</span></span> |
| <span data-ttu-id="ba941-148">Kategoriler</span><span class="sxs-lookup"><span data-stu-id="ba941-148">Categories</span></span> |<span data-ttu-id="ba941-149">Evet</span><span class="sxs-lookup"><span data-stu-id="ba941-149">Yes</span></span> |<span data-ttu-id="ba941-150">Toplanması gereken olay kategorileri virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="ba941-150">Comma-separated list of event categories that should be collected.</span></span> <span data-ttu-id="ba941-151">Olası değerler şunlardır: yazma, silme ve eylem.</span><span class="sxs-lookup"><span data-stu-id="ba941-151">Possible values are Write, Delete, and Action.</span></span> |

## <a name="archive-hello-activity-log-via-cli"></a><span data-ttu-id="ba941-152">Arşiv hello CLI aracılığıyla etkinlik günlüğü</span><span class="sxs-lookup"><span data-stu-id="ba941-152">Archive hello Activity Log via CLI</span></span>
```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --locations global,westus,eastus,northeurope --retentionInDays 180 –categories Write,Delete,Action
```

| <span data-ttu-id="ba941-153">Özellik</span><span class="sxs-lookup"><span data-stu-id="ba941-153">Property</span></span> | <span data-ttu-id="ba941-154">Gerekli</span><span class="sxs-lookup"><span data-stu-id="ba941-154">Required</span></span> | <span data-ttu-id="ba941-155">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ba941-155">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ba941-156">ad</span><span class="sxs-lookup"><span data-stu-id="ba941-156">name</span></span> |<span data-ttu-id="ba941-157">Evet</span><span class="sxs-lookup"><span data-stu-id="ba941-157">Yes</span></span> |<span data-ttu-id="ba941-158">Günlük profilinin adı.</span><span class="sxs-lookup"><span data-stu-id="ba941-158">Name of your log profile.</span></span> |
| <span data-ttu-id="ba941-159">storageId</span><span class="sxs-lookup"><span data-stu-id="ba941-159">storageId</span></span> |<span data-ttu-id="ba941-160">Hayır</span><span class="sxs-lookup"><span data-stu-id="ba941-160">No</span></span> |<span data-ttu-id="ba941-161">Kaynak Kimliğini hello depolama hesabı toowhich etkinlik günlükleri kaydedilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="ba941-161">Resource ID of hello Storage Account toowhich Activity Logs should be saved.</span></span> |
| <span data-ttu-id="ba941-162">Konumları</span><span class="sxs-lookup"><span data-stu-id="ba941-162">locations</span></span> |<span data-ttu-id="ba941-163">Evet</span><span class="sxs-lookup"><span data-stu-id="ba941-163">Yes</span></span> |<span data-ttu-id="ba941-164">Toocollect etkinlik günlüğü olaylarını istediğiniz bölgeler virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="ba941-164">Comma-separated list of regions for which you would like toocollect Activity Log events.</span></span> <span data-ttu-id="ba941-165">Tüm bölgelerin bir listesi görüntüleyebilirsiniz [bu sayfasını ziyaret tarafından](https://azure.microsoft.com/en-us/regions) veya kullanarak [Azure Yönetimi REST API hello](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span><span class="sxs-lookup"><span data-stu-id="ba941-165">You can view a list of all regions [by visiting this page](https://azure.microsoft.com/en-us/regions) or by using [hello Azure Management REST API](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span></span> |
| <span data-ttu-id="ba941-166">retentionInDays</span><span class="sxs-lookup"><span data-stu-id="ba941-166">retentionInDays</span></span> |<span data-ttu-id="ba941-167">Evet</span><span class="sxs-lookup"><span data-stu-id="ba941-167">Yes</span></span> |<span data-ttu-id="ba941-168">Hangi olayların tutulacağını için 1 ile 2147483647 arasında gün sayısı.</span><span class="sxs-lookup"><span data-stu-id="ba941-168">Number of days for which events should be retained, between 1 and 2147483647.</span></span> <span data-ttu-id="ba941-169">Sıfır değeri hello günlükleri süresiz olarak depolar (sürekli).</span><span class="sxs-lookup"><span data-stu-id="ba941-169">A value of zero will store hello logs indefinitely (forever).</span></span> |
| <span data-ttu-id="ba941-170">kategorileri</span><span class="sxs-lookup"><span data-stu-id="ba941-170">categories</span></span> |<span data-ttu-id="ba941-171">Evet</span><span class="sxs-lookup"><span data-stu-id="ba941-171">Yes</span></span> |<span data-ttu-id="ba941-172">Toplanması gereken olay kategorileri virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="ba941-172">Comma-separated list of event categories that should be collected.</span></span> <span data-ttu-id="ba941-173">Olası değerler şunlardır: yazma, silme ve eylem.</span><span class="sxs-lookup"><span data-stu-id="ba941-173">Possible values are Write, Delete, and Action.</span></span> |

## <a name="storage-schema-of-hello-activity-log"></a><span data-ttu-id="ba941-174">Merhaba etkinlik günlüğü depolama şeması</span><span class="sxs-lookup"><span data-stu-id="ba941-174">Storage schema of hello Activity Log</span></span>
<span data-ttu-id="ba941-175">Arşivleme kurduktan sonra bir etkinlik günlüğü olay oluştuktan hemen sonra bir depolama kapsayıcısı hello depolama hesabı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ba941-175">Once you have set up archival, a storage container will be created in hello storage account as soon as an Activity Log event occurs.</span></span> <span data-ttu-id="ba941-176">Merhaba BLOB'lar hello kapsayıcı içindeki aynı hello etkinlik günlüğü ve tanılama günlüklerini arasında biçimi hello izleyin.</span><span class="sxs-lookup"><span data-stu-id="ba941-176">hello blobs within hello container follow hello same format across hello Activity Log and Diagnostic Logs.</span></span> <span data-ttu-id="ba941-177">Bu BLOB Hello yapıdır:</span><span class="sxs-lookup"><span data-stu-id="ba941-177">hello structure of these blobs is:</span></span>

> <span data-ttu-id="ba941-178">Öngörüler-işletimsel-günlükleri/name = varsayılan/ResourceId/ABONELİKLERİ = / {abonelik kimliği} / y = {dört basamaklı sayısal year} / m = {iki basamaklı sayısal ay} / d = {iki basamaklı sayısal günü} / h {iki basamaklı 24 saatlik hour}/m=00/PT1H.json =</span><span class="sxs-lookup"><span data-stu-id="ba941-178">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/{subscription ID}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="ba941-179">Örneğin, bir blob adı olabilir:</span><span class="sxs-lookup"><span data-stu-id="ba941-179">For example, a blob name might be:</span></span>

> <span data-ttu-id="ba941-180">insights-Operational-Logs/Name=default/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/y=2016/m=08/d=22/h=18/m=00/PT1H.JSON</span><span class="sxs-lookup"><span data-stu-id="ba941-180">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="ba941-181">Her bir PT1H.json blob hello blob URL'SİNDE belirtilen hello saat içinde gerçekleşen olayların JSON blobu içerir (örneğin h = 12).</span><span class="sxs-lookup"><span data-stu-id="ba941-181">Each PT1H.json blob contains a JSON blob of events that occurred within hello hour specified in hello blob URL (e.g. h=12).</span></span> <span data-ttu-id="ba941-182">Bunlar ortaya çıktığında hello mevcut saat sırasında eklenmiş toohello PT1H.json dosya olaylardır.</span><span class="sxs-lookup"><span data-stu-id="ba941-182">During hello present hour, events are appended toohello PT1H.json file as they occur.</span></span> <span data-ttu-id="ba941-183">Merhaba dakika değeri (m 00 =) her zaman etkinlik günlüğü olaylarını tek tek bloblar saat başına ayrılmış bu yana 00.</span><span class="sxs-lookup"><span data-stu-id="ba941-183">hello minute value (m=00) is always 00, since Activity Log events are broken into individual blobs per hour.</span></span>

<span data-ttu-id="ba941-184">Merhaba PT1H.json dosyası içinde her olay bu biçim aşağıdaki hello "kayıtlar" dizisinde depolanır:</span><span class="sxs-lookup"><span data-stu-id="ba941-184">Within hello PT1H.json file, each event is stored in hello “records” array, following this format:</span></span>

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


| <span data-ttu-id="ba941-185">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="ba941-185">Element name</span></span> | <span data-ttu-id="ba941-186">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ba941-186">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ba941-187">time</span><span class="sxs-lookup"><span data-stu-id="ba941-187">time</span></span> |<span data-ttu-id="ba941-188">Merhaba olay hello Azure hizmetini işleme hello tarafından oluşturulan zaman damgası karşılık gelen hello olay isteği.</span><span class="sxs-lookup"><span data-stu-id="ba941-188">Timestamp when hello event was generated by hello Azure service processing hello request corresponding hello event.</span></span> |
| <span data-ttu-id="ba941-189">resourceId</span><span class="sxs-lookup"><span data-stu-id="ba941-189">resourceId</span></span> |<span data-ttu-id="ba941-190">Kaynak Kimliğini hello kaynak etkilenmiş.</span><span class="sxs-lookup"><span data-stu-id="ba941-190">Resource ID of hello impacted resource.</span></span> |
| <span data-ttu-id="ba941-191">operationName</span><span class="sxs-lookup"><span data-stu-id="ba941-191">operationName</span></span> |<span data-ttu-id="ba941-192">Merhaba işlemin adı.</span><span class="sxs-lookup"><span data-stu-id="ba941-192">Name of hello operation.</span></span> |
| <span data-ttu-id="ba941-193">category</span><span class="sxs-lookup"><span data-stu-id="ba941-193">category</span></span> |<span data-ttu-id="ba941-194">Merhaba eylem kategorisi örn.</span><span class="sxs-lookup"><span data-stu-id="ba941-194">Category of hello action, eg.</span></span> <span data-ttu-id="ba941-195">Yazma, okuma, eylem.</span><span class="sxs-lookup"><span data-stu-id="ba941-195">Write, Read, Action.</span></span> |
| <span data-ttu-id="ba941-196">resultType</span><span class="sxs-lookup"><span data-stu-id="ba941-196">resultType</span></span> |<span data-ttu-id="ba941-197">Merhaba Hello türü neden, örn.</span><span class="sxs-lookup"><span data-stu-id="ba941-197">hello type of hello result, eg.</span></span> <span data-ttu-id="ba941-198">Başarılı, başarısız, Başlat</span><span class="sxs-lookup"><span data-stu-id="ba941-198">Success, Failure, Start</span></span> |
| <span data-ttu-id="ba941-199">resultSignature</span><span class="sxs-lookup"><span data-stu-id="ba941-199">resultSignature</span></span> |<span data-ttu-id="ba941-200">Merhaba kaynak türüne bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="ba941-200">Depends on hello resource type.</span></span> |
| <span data-ttu-id="ba941-201">durationMs</span><span class="sxs-lookup"><span data-stu-id="ba941-201">durationMs</span></span> |<span data-ttu-id="ba941-202">Milisaniye cinsinden hello işlemi süresi</span><span class="sxs-lookup"><span data-stu-id="ba941-202">Duration of hello operation in milliseconds</span></span> |
| <span data-ttu-id="ba941-203">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="ba941-203">callerIpAddress</span></span> |<span data-ttu-id="ba941-204">Merhaba işlemi, UPN Talebi veya kullanılabilirliğine göre SPN talep yürüttü hello kullanıcının IP adresi.</span><span class="sxs-lookup"><span data-stu-id="ba941-204">IP address of hello user who has performed hello operation, UPN claim, or SPN claim based on availability.</span></span> |
| <span data-ttu-id="ba941-205">correlationId</span><span class="sxs-lookup"><span data-stu-id="ba941-205">correlationId</span></span> |<span data-ttu-id="ba941-206">Genellikle bir GUID hello dize biçiminde.</span><span class="sxs-lookup"><span data-stu-id="ba941-206">Usually a GUID in hello string format.</span></span> <span data-ttu-id="ba941-207">Bir correlationıd değeri paylaşan olayları ait toohello aynı uber eylemi.</span><span class="sxs-lookup"><span data-stu-id="ba941-207">Events that share a correlationId belong toohello same uber action.</span></span> |
| <span data-ttu-id="ba941-208">identity</span><span class="sxs-lookup"><span data-stu-id="ba941-208">identity</span></span> |<span data-ttu-id="ba941-209">JSON blob Hello yetkilendirme ve talep açıklayan.</span><span class="sxs-lookup"><span data-stu-id="ba941-209">JSON blob describing hello authorization and claims.</span></span> |
| <span data-ttu-id="ba941-210">Yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="ba941-210">authorization</span></span> |<span data-ttu-id="ba941-211">BLOB hello olay RBAC özelliklerinin.</span><span class="sxs-lookup"><span data-stu-id="ba941-211">Blob of RBAC properties of hello event.</span></span> <span data-ttu-id="ba941-212">Genellikle hello "eylem", "rol" ve "scope" özellikleri içerir.</span><span class="sxs-lookup"><span data-stu-id="ba941-212">Usually includes hello “action”, “role” and “scope” properties.</span></span> |
| <span data-ttu-id="ba941-213">düzeyi</span><span class="sxs-lookup"><span data-stu-id="ba941-213">level</span></span> |<span data-ttu-id="ba941-214">Merhaba olay düzeyi.</span><span class="sxs-lookup"><span data-stu-id="ba941-214">Level of hello event.</span></span> <span data-ttu-id="ba941-215">Değerleri aşağıdaki hello birini: "Kritik", "Error"Uyarı",", "Bilgi" ve "Ayrıntılı"</span><span class="sxs-lookup"><span data-stu-id="ba941-215">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="ba941-216">location</span><span class="sxs-lookup"><span data-stu-id="ba941-216">location</span></span> |<span data-ttu-id="ba941-217">Bölge hangi hello konumda oluştu (veya genel).</span><span class="sxs-lookup"><span data-stu-id="ba941-217">Region in which hello location occurred (or global).</span></span> |
| <span data-ttu-id="ba941-218">properties</span><span class="sxs-lookup"><span data-stu-id="ba941-218">properties</span></span> |<span data-ttu-id="ba941-219">Kümesi `<Key, Value>` hello hello olay ayrıntılarını açıklayan çiftleri (yani sözlük).</span><span class="sxs-lookup"><span data-stu-id="ba941-219">Set of `<Key, Value>` pairs (i.e. Dictionary) describing hello details of hello event.</span></span> |

> [!NOTE]
> <span data-ttu-id="ba941-220">Merhaba özellikleri ve bu özellikleri kullanımını hello kaynak bağlı olarak değişebilir.</span><span class="sxs-lookup"><span data-stu-id="ba941-220">hello properties and usage of those properties can vary depending on hello resource.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="ba941-221">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ba941-221">Next steps</span></span>
* [<span data-ttu-id="ba941-222">BLOB'ları çözümleme için karşıdan yükle</span><span class="sxs-lookup"><span data-stu-id="ba941-222">Download blobs for analysis</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)
* [<span data-ttu-id="ba941-223">Merhaba etkinlik günlüğü tooEvent hub akışı</span><span class="sxs-lookup"><span data-stu-id="ba941-223">Stream hello Activity Log tooEvent Hubs</span></span>](monitoring-stream-activity-logs-event-hubs.md)
* [<span data-ttu-id="ba941-224">Merhaba etkinlik günlüğü hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="ba941-224">Read more about hello Activity Log</span></span>](monitoring-overview-activity-logs.md)

