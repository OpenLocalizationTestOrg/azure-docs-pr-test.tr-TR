---
title: Azure CDN aaaLog analize | Microsoft Docs
description: "Müşteri, Günlük çözümlemesi için Azure CDN etkinleştirebilirsiniz."
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 95e18b3c-b987-46c2-baa8-a27a029e3076
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: v-semcev
ms.openlocfilehash: 56e5a4fec46fd156cf38252732afb4522741d009
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-logs-for-azure-cdn"></a><span data-ttu-id="89da2-103">Azure CDN için tanılama günlükleri</span><span class="sxs-lookup"><span data-stu-id="89da2-103">Diagnostics Logs for Azure CDN</span></span>

<span data-ttu-id="89da2-104">CDN uygulamanız için etkinleştirdikten sonra büyük olasılıkla toomonitor hello CDN kullanım, teslim hello durumunu denetleyin ve olası sorunları giderme.</span><span class="sxs-lookup"><span data-stu-id="89da2-104">After enabling CDN for your application, you will likely want toomonitor hello CDN usage, check hello health of your delivery, and troubleshoot potential issues.</span></span> <span data-ttu-id="89da2-105">Azure CDN ile bu özellikleri sağlar [CDN temel analiz](cdn-analyze-usage-patterns.md) ve [tanılama günlükleri](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)</span><span class="sxs-lookup"><span data-stu-id="89da2-105">Azure CDN provides these capabilities with [CDN Core Analytics](cdn-analyze-usage-patterns.md) and [Diagnostic Logs](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)</span></span>

## <a name="cdn-core-analytics"></a><span data-ttu-id="89da2-106">CDN temel analiz</span><span class="sxs-lookup"><span data-stu-id="89da2-106">CDN Core Analytics</span></span>
<span data-ttu-id="89da2-107">Verizon standart veya premium profil ile geçerli bir Azure CDN kullanıcı olarak, önceden mümkün tooview temel analiz hello ek portal hello "Manage" seçeneğinden hello Azure portal aracılığıyla erişilebilir demektir.</span><span class="sxs-lookup"><span data-stu-id="89da2-107">As a current Azure CDN user with Verizon standard or premium profile, you are already able tooview core analytics in hello supplemental portal accessible via hello "Manage" option from hello Azure portal.</span></span> 

## <a name="azure-diagnostic-logs"></a><span data-ttu-id="89da2-108">Azure tanılama günlükleri</span><span class="sxs-lookup"><span data-stu-id="89da2-108">Azure Diagnostic Logs</span></span>

<span data-ttu-id="89da2-109">Bu yeni özellik ile Azure, şimdi temel analiz görüntüleyebilir ve bunları dahil olmak üzere bir veya daha fazla hedefleri kaydedin:</span><span class="sxs-lookup"><span data-stu-id="89da2-109">Azure With this new feature, you can now view core analytics and save them into one or more destinations including:</span></span>

 - <span data-ttu-id="89da2-110">Azure Storage hesabı</span><span class="sxs-lookup"><span data-stu-id="89da2-110">Azure Storage account</span></span>
 - <span data-ttu-id="89da2-111">Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="89da2-111">Azure Event Hubs</span></span>
 - [<span data-ttu-id="89da2-112">OMS günlük analizi deposu</span><span class="sxs-lookup"><span data-stu-id="89da2-112">OMS Log Analytics repository</span></span>](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started)
 
 <span data-ttu-id="89da2-113">Bu özellik tooVerizon (standart ve Premium) ve Akamai (standart) CDN profilleri ait tüm CDN uç noktası için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="89da2-113">This feature is available for all CDN endpoints belonging tooVerizon (Standard & Premium) and Akamai (Standard) CDN Profiles.</span></span>

<span data-ttu-id="89da2-114">Özelleştirilmiş bir biçimde tüketebileceği böylece tanılama günlükleri tooexport temel kullanım ölçümleri, CDN uç noktası tooa çeşitli kaynaklardan gelen izin verin.</span><span class="sxs-lookup"><span data-stu-id="89da2-114">Diagnostics logs allow you tooexport basic usage metrics from your CDN endpoint tooa variety of sources so that you can consume them in a customized way.</span></span> <span data-ttu-id="89da2-115">Örneğin, bunu veri aktarma türleri hello:</span><span class="sxs-lookup"><span data-stu-id="89da2-115">For example, you can do hello following types of data export:</span></span>

- <span data-ttu-id="89da2-116">Veri tooblob depolama verme, tooCSV aktarın ve grafikleri oluşturun excel.</span><span class="sxs-lookup"><span data-stu-id="89da2-116">Export data tooblob storage, export tooCSV, and generate graphs in excel.</span></span>
- <span data-ttu-id="89da2-117">Veri tooevent hub'ları dışarı aktarın ve diğer azure hizmetleriyle verilerle ilişkilendirmek.</span><span class="sxs-lookup"><span data-stu-id="89da2-117">Export data tooevent hubs and correlate with data from other azure services.</span></span>
- <span data-ttu-id="89da2-118">Kendi OMS çalışma alanındaki veri toolog analizi ve görünüm verileri dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="89da2-118">Export data toolog analytics and view data in your own OMS work space</span></span>

<span data-ttu-id="89da2-119">Merhaba aşağıdaki şekilde veri tipik bir CDN temel analiz görünüme gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="89da2-119">hello following figure shows a typical CDN Core Analytics view into data.</span></span>

![Portal - tanılama günlükleri](./media/cdn-diagnostics-log/01_OMS-workspace.png)

<span data-ttu-id="89da2-121">*Şekil 1 - CDN temel analiz görünümü*</span><span class="sxs-lookup"><span data-stu-id="89da2-121">*Figure 1 - CDN Core Analytics view*</span></span>

<span data-ttu-id="89da2-122">izlenecek yol aşağıdaki hello hello çekirdek analiz verileri, adımlar hello özelliğini etkinleştirme ve bunları toovarious hedefleri teslim etme ve bu hedefleri tüketen hello şeması geçer.</span><span class="sxs-lookup"><span data-stu-id="89da2-122">hello following walkthrough goes through hello schema of hello core analytics data, steps involved in enabling hello feature and delivering them toovarious destinations, and consuming from these destinations.</span></span>

## <a name="enable-logging-with-azure-portal"></a><span data-ttu-id="89da2-123">Azure portal ile günlük kaydını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="89da2-123">Enable logging with Azure portal</span></span>

> [!NOTE]
> <span data-ttu-id="89da2-124">Merhaba tanılama günlükleri açık olan **kapalı** varsayılan olarak.</span><span class="sxs-lookup"><span data-stu-id="89da2-124">hello diagnostics logs are turned **off** by default.</span></span> 

<span data-ttu-id="89da2-125">CDN temel analiz tooenable günlüğüyle Hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="89da2-125">Follow hello steps below tooenable logging with CDN Core Analytics:</span></span>

<span data-ttu-id="89da2-126">İçinde toohello oturum [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="89da2-126">Sign in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="89da2-127">İş akışınız için etkin CDN zaten yoksa [Azure CDN'yi etkinleştirme](cdn-create-new-endpoint.md) devam etmeden önce.</span><span class="sxs-lookup"><span data-stu-id="89da2-127">If you don't already have CDN enabled for your workflow, [Enable Azure CDN](cdn-create-new-endpoint.md) before you continue.</span></span>

1. <span data-ttu-id="89da2-128">Merhaba Portalı'nda çok gidin**CDN profili**.</span><span class="sxs-lookup"><span data-stu-id="89da2-128">In hello portal, navigate too**CDN profile**.</span></span>
2. <span data-ttu-id="89da2-129">CDN profili seçin ve ardından hello CDN uç noktası tooenable istediğiniz **tanılama günlükleri**.</span><span class="sxs-lookup"><span data-stu-id="89da2-129">Select a CDN profile, then select hello CDN endpoint that you want tooenable **Diagnostics Logs**.</span></span>

    ![Portal - tanılama günlükleri](./media/cdn-diagnostics-log/02_Browse-to-Diagnostics-logs.png)

3. <span data-ttu-id="89da2-131">Çok Git**tanılama günlükleri** altında dikey **izleme** bölümünde ardından hello durumu çok değiştirin**üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="89da2-131">Go too**Diagnostics Logs** blade Under **Monitoring** section, then change hello status too**On**.</span></span>

    ![Portal - tanılama günlükleri](./media/cdn-diagnostics-log/03_Diagnostics-logs-options.png)

### <a name="enable-logging-with-azure-storage"></a><span data-ttu-id="89da2-133">Azure Storage ile günlük kaydını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="89da2-133">Enable logging with Azure Storage</span></span>
    
<span data-ttu-id="89da2-134">toouse Azure Storage toostore hello günlükleri, seçin **arşiv tooa depolama hesabı**, bekletme günleri seçin ve tıklatın **CoreAnalytics** altında **günlük**.</span><span class="sxs-lookup"><span data-stu-id="89da2-134">toouse Azure Storage toostore hello logs, select **Archive tooa storage account**, select retention days, and click **CoreAnalytics** under **Log**.</span></span>

![Portal - tanılama günlükleri](./media/cdn-diagnostics-log/04_Diagnostics-logs-storage.png)

<span data-ttu-id="89da2-136">*Şekil 2 - Azure Storage ile günlüğe kaydetme*</span><span class="sxs-lookup"><span data-stu-id="89da2-136">*Figure 2 - Logging with Azure Storage*</span></span>

### <a name="logging-with-oms-log-analytics"></a><span data-ttu-id="89da2-137">OMS günlük analizi ile günlüğe kaydetme</span><span class="sxs-lookup"><span data-stu-id="89da2-137">Logging with OMS Log Analytics</span></span>

<span data-ttu-id="89da2-138">toouse OMS günlük analizi toostore hello günlükleri, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="89da2-138">toouse OMS Log Analytics toostore hello logs, follow these steps:</span></span>

1. <span data-ttu-id="89da2-139">Merhaba gelen **tanılama günlükleri** altında dikey **izleme**seçin **tooLog Analytics gönderme** gelen</span><span class="sxs-lookup"><span data-stu-id="89da2-139">From hello **Diagnostics Logs** blade Under **Monitoring**, select **Send tooLog Analytics** from</span></span> 

    ![Portal - tanılama günlükleri](./media/cdn-diagnostics-log/05_Ready-to-Configure.png)    

2. <span data-ttu-id="89da2-141">Merhaba günlük analizi günlük yapılandırma üzerinde tıklayarak yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="89da2-141">Configure hello Log Analytics logging by clicking on Configure.</span></span> <span data-ttu-id="89da2-142">Bu, önceki bir çalışma alanı seçin veya yeni bir tane oluşturun tooa iletişim götürür.</span><span class="sxs-lookup"><span data-stu-id="89da2-142">This takes you tooa dialog where you can select a previous workspace or create a new one.</span></span>

    ![Portal - tanılama günlükleri](./media/cdn-diagnostics-log/06_Choose-workspace.png)

3. <span data-ttu-id="89da2-144">Tıklatın **yeni çalışma alanı oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="89da2-144">Click **Create New Workspace**.</span></span>

    ![Portal - tanılama günlükleri](./media/cdn-diagnostics-log/07_Create-new.png)

4. <span data-ttu-id="89da2-146">Ardından, yeni çalışma alanı adı, varolan abonelik, kaynak grubu (yeni veya var olan), konum ve fiyatlandırma katmanı seçmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="89da2-146">Next you must select a new workspace name, existing subscription, resource group (new or existing), location, and pricing tier.</span></span> <span data-ttu-id="89da2-147">Bu yapılandırma tooyour panoya sabitleme hello seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="89da2-147">You have hello option of pinning this configuration tooyour dashboard.</span></span> <span data-ttu-id="89da2-148">Tamam toocomplete hello Yapılandırması'nı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="89da2-148">Click OK toocomplete hello configuration.</span></span>

    <span data-ttu-id="89da2-149">Ardından, OMS çalışma ve kaynak grubu adları ile çalışma alanınızı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="89da2-149">Next you should see your workspace with your OMS Workspace and Resource group names.</span></span> <span data-ttu-id="89da2-150">Adları benzersiz olmalıdır ve yalnızca harf, rakam ve kısa çizgi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="89da2-150">Names must be unique and can only use letters, numbers, and hyphens.</span></span> <span data-ttu-id="89da2-151">Boşluk ve alt çizgi izin verilmiyor.</span><span class="sxs-lookup"><span data-stu-id="89da2-151">Spaces and underscores are not allowed.</span></span> 

    ![Portal - tanılama günlükleri](./media/cdn-diagnostics-log/08_Workspace-resource.png)

5. <span data-ttu-id="89da2-153">Sonraki çalışma alanınız oluşturuldu ve yapılandırma ekranında oturum tooyour döndürülen belirten kısa bir ileti alırsınız.</span><span class="sxs-lookup"><span data-stu-id="89da2-153">You next get a short message saying that your workspace has been created and you are returned tooyour logging configuration screen.</span></span> <span data-ttu-id="89da2-154">Günlük analizi çalışma alanınız hello adını doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="89da2-154">You can confirm hello name of your Log Analytics workspace.</span></span>

    ![Portal - tanılama günlükleri](./media/cdn-diagnostics-log/09_Return-to-logging.png)

    <span data-ttu-id="89da2-156">Merhaba günlük analizi yapılandırması ayarladıktan sonra CDN günlüğü için hello CoreAnalytics kutuyu da işaretlemeleri emin olun.</span><span class="sxs-lookup"><span data-stu-id="89da2-156">Once you have set up hello Log Analytics configuration, make sure you also check hello CoreAnalytics box for CDN logging.</span></span>

6. <span data-ttu-id="89da2-157">Her şeyi tooyour istediğiniz ise, hello tıklatın **kaydetmek** hello yapılandırma iletişim hello üstündeki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="89da2-157">If everything is tooyour liking, click hello **Save** button at hello top of hello configuration dialog.</span></span>

    ![Portal - tanılama günlükleri](./media/cdn-diagnostics-log/10_Save-me.png)

    <span data-ttu-id="89da2-159">Merhaba **kaydetmek** düğmesi artık etkin ve o hello üzerinde veya düğmeyi açık, ancak mavi mor yerine sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="89da2-159">hello **Save** button is no longer active and that hello ON/OFF button is now ON, but blue instead of purple.</span></span>

7. <span data-ttu-id="89da2-160">Yeni bir OMS çalışma alanınızı toosee istiyorsanız, Git tooyour Azure portal panosunda, günlük analizi çalışma alanınız hello adını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="89da2-160">If you want toosee your new OMS workspace, go tooyour Azure portal Dashboard, click hello name of your Log Analytics workspace.</span></span> <span data-ttu-id="89da2-161">Çalışma alanınızı sonraki görürsünüz (OMS çalışma hello solda vurgulanmış olduğundan emin olun).</span><span class="sxs-lookup"><span data-stu-id="89da2-161">Next you will see your workspace (make sure that OMS Workspace is highlighted on hello left).</span></span> <span data-ttu-id="89da2-162">Merhaba OMS portalı döşeme toosee üzerinde hello OMS deposu alanınızdaki'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="89da2-162">Click on hello OMS Portal tile toosee your workspace in hello OMS repository.</span></span> 

    ![Portal - tanılama günlükleri](./media/cdn-diagnostics-log/11_OMS-dashboard.png) 

    <span data-ttu-id="89da2-164">OMS deponuz hazır toolog veri sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="89da2-164">Your OMS repository is now ready toolog data.</span></span> <span data-ttu-id="89da2-165">İçinde bu verileri tooconsume sipariş, kullanmalısınız bir [OMS çözüm](#consuming-oms-log-analytics-data), bu makalenin sonraki bölümlerinde kapsanan.</span><span class="sxs-lookup"><span data-stu-id="89da2-165">In order tooconsume that data, you must use an [OMS Solution](#consuming-oms-log-analytics-data), covered later in this article.</span></span>

<span data-ttu-id="89da2-166">Günlük verileri gecikmeler hakkında daha fazla bilgi için [burada](#log-data-delays).</span><span class="sxs-lookup"><span data-stu-id="89da2-166">For more information about log data delays, go [here](#log-data-delays).</span></span>

## <a name="enable-logging-with-powershell"></a><span data-ttu-id="89da2-167">PowerShell ile günlük kaydını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="89da2-167">Enable logging with PowerShell</span></span>

<span data-ttu-id="89da2-168">Aşağıda Azure PowerShell cmdlet'leri aracılığıyla tooenable ve get tanılama günlüklerini nasıl hello üzerinde bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="89da2-168">Below is an example on how tooenable and get Diagnostic Logs via hello Azure PowerShell Cmdlets.</span></span>

###<a name="enabling-diagnostic-logs-in-a-storage-account"></a><span data-ttu-id="89da2-169">Bir depolama hesabında oturum tanılama etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="89da2-169">Enabling Diagnostic Logs in a Storage Account</span></span>

<span data-ttu-id="89da2-170">İlk oturum açın ve bir abonelik seçin:</span><span class="sxs-lookup"><span data-stu-id="89da2-170">First log in and select a subscription:</span></span>

    Login-AzureRmAccount 

    Select-AzureSubscription -SubscriptionId 


<span data-ttu-id="89da2-171">bir depolama hesabına tanılama günlüklerine tooEnable bu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="89da2-171">tooEnable Diagnostic Logs in a Storage Account, use this command:</span></span>

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}" -StorageAccountId "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicStorage/storageAccounts/{storageAccountName}" -Enabled $true -Categories CoreAnalytics
```
<span data-ttu-id="89da2-172">tooEnable tanılama günlükleri bir OMS çalışma alanında, bu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="89da2-172">tooEnable Diagnostics Logs in an OMS workspace, use this command:</span></span>

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/`{subscriptionId}<subscriptionId>
    .<subscriptionName>" -WorkspaceId "/subscriptions/<workspaceId>.<workspaceName>" -Enabled $true -Categories CoreAnalytics 
```



## <a name="consuming-diagnostics-logs-from-azure-storage"></a><span data-ttu-id="89da2-173">Azure depolama biriminden tanılama günlüklerini kullanma</span><span class="sxs-lookup"><span data-stu-id="89da2-173">Consuming diagnostics logs from Azure Storage</span></span>
<span data-ttu-id="89da2-174">Nasıl bunlar içinde Azure Storage hesabını düzenlenir ve sağlayan örnek kodu toodownload hello tooa CSV dosyasına kaydeder, bu bölümde hello CDN temel analiz hello şeması açıklanır.</span><span class="sxs-lookup"><span data-stu-id="89da2-174">This section describes hello schema of hello CDN core analytics, how these are organized inside of an Azure Storage Account and provides sample code toodownload hello logs in tooa CSV file.</span></span>

### <a name="using-microsoft-azure-storage-explorer"></a><span data-ttu-id="89da2-175">Microsoft Azure Storage Gezgini kullanma</span><span class="sxs-lookup"><span data-stu-id="89da2-175">Using Microsoft Azure Storage Explorer</span></span>
<span data-ttu-id="89da2-176">Hello çekirdek analiz verileri Azure depolama hesabı hello erişmeden önce önce bir aracı tooaccess Merhaba içeriğine bir depolama hesabı gerekir.</span><span class="sxs-lookup"><span data-stu-id="89da2-176">Before you can access hello core analytics data from hello Azure Storage Account, you first need a tool tooaccess hello contents in a storage account.</span></span> <span data-ttu-id="89da2-177">Varken çeşitli araçlar kullanılabilir hello pazarında, hello önerdiğimiz bir hello Microsoft Azure Storage Gezgini ' dir.</span><span class="sxs-lookup"><span data-stu-id="89da2-177">While there are several tools available in hello market, hello one that we recommend is hello Microsoft Azure Storage Explorer.</span></span> <span data-ttu-id="89da2-178">Merhaba aracından indirebilirsiniz [burada](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="89da2-178">You can download hello tool from [here](http://storageexplorer.com/).</span></span> <span data-ttu-id="89da2-179">Merhaba yazılım yükleyip yapılandırdıktan sonra toouse hedef toohello CDN tanılama günlükleri yapılandırılan aynı Azure depolama hesabı hello.</span><span class="sxs-lookup"><span data-stu-id="89da2-179">After downloading and installing hello software, configure it toouse hello same Azure Storage Account that was configured as a destination toohello CDN Diagnostics Logs.</span></span>

1.  <span data-ttu-id="89da2-180">Açık **Microsoft Azure Storage Gezgini**</span><span class="sxs-lookup"><span data-stu-id="89da2-180">Open **Microsoft Azure Storage Explorer**</span></span>
2.  <span data-ttu-id="89da2-181">Merhaba depolama hesabını bulun</span><span class="sxs-lookup"><span data-stu-id="89da2-181">Locate hello storage account</span></span>
3.  <span data-ttu-id="89da2-182">Toohello Git **"Blob kapsayıcıları"** düğümü altında bu depolama hesabı ve hello düğümünü genişletin</span><span class="sxs-lookup"><span data-stu-id="89da2-182">Go toohello **“Blob Containers”** node under this storage account and expand hello node</span></span>
4.  <span data-ttu-id="89da2-183">Adlı select hello kapsayıcı **"Öngörüler günlükleri coreanalytics"** ve çift tıklatın</span><span class="sxs-lookup"><span data-stu-id="89da2-183">Select hello container named **“insights-logs-coreanalytics”** and double-click it</span></span>
5.  <span data-ttu-id="89da2-184">Sonuçları göster ayarlama gibi görünen hello ile ilk düzeyi, başlangıç hello sağ taraftaki bölmede **"ResourceId ="**.</span><span class="sxs-lookup"><span data-stu-id="89da2-184">Results show up on hello right-hand pane starting with hello first level, which looks like **“resourceId=”**.</span></span> <span data-ttu-id="89da2-185">Merhaba dosya görene kadar tüm hello şekilde tıklayarak devam **PT1H.json**.</span><span class="sxs-lookup"><span data-stu-id="89da2-185">Continue clicking all hello way until you see hello file **PT1H.json**.</span></span> <span data-ttu-id="89da2-186">Not hello yolu açıklaması için aşağıdaki hello bakın.</span><span class="sxs-lookup"><span data-stu-id="89da2-186">See hello following note for explanation of hello path.</span></span>
6.  <span data-ttu-id="89da2-187">Her bir blob **PT1H.json** temsil eder, belirli bir CDN uç noktası veya kendi özel etki alanı için bir saat analiz günlükleri hello.</span><span class="sxs-lookup"><span data-stu-id="89da2-187">Each blob **PT1H.json** represents hello analytics logs for one hour for a specific CDN endpoint or its custom domain.</span></span>
7.  <span data-ttu-id="89da2-188">Bu JSON dosyasının Merhaba içeriğine Hello şeması hello bölümünde hello çekirdek analiz günlükleri şema açıklanan</span><span class="sxs-lookup"><span data-stu-id="89da2-188">hello schema of hello contents of this JSON file is described in hello section Schema of hello Core Analytics Logs</span></span>


> [!NOTE]
> <span data-ttu-id="89da2-189">**BLOB yol biçimi**</span><span class="sxs-lookup"><span data-stu-id="89da2-189">**Blob path format**</span></span>
> 
> <span data-ttu-id="89da2-190">Çekirdek analiz günlükleri saatte üretilir.</span><span class="sxs-lookup"><span data-stu-id="89da2-190">Core Analytics logs are generated every hour.</span></span> <span data-ttu-id="89da2-191">Bir saat için tüm veriler toplanır ve bir JSON yükü olarak tek bir Azure Blob içinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="89da2-191">All data for an hour are collected and stored inside a single Azure Blob as a JSON payload.</span></span> <span data-ttu-id="89da2-192">Merhaba yolu toothis Azure Blob hiyerarşik bir yapı gibi görünür.</span><span class="sxs-lookup"><span data-stu-id="89da2-192">hello path toothis Azure Blob appears as if there is a hierarchical structure.</span></span> <span data-ttu-id="89da2-193">Bu çünkü hello Depolama Gezgini araçları Yorumlar '/' dizin ayırıcı olarak ve kolaylık sağlamak için hello hiyerarşisini gösterir.</span><span class="sxs-lookup"><span data-stu-id="89da2-193">This is because hello Storage explorer tool interprets '/' as a directory separator and shows hello hierarchy for convenience.</span></span> <span data-ttu-id="89da2-194">Aslında, hello tam yolunu yalnızca hello blob adını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="89da2-194">Actually, hello whole path just represents hello blob name.</span></span> <span data-ttu-id="89da2-195">Bu ad hello BLOB adlandırma kuralı aşağıdaki hello izler</span><span class="sxs-lookup"><span data-stu-id="89da2-195">This name of hello blob follows hello following naming convention</span></span> 
    
    resourceId=/SUBSCRIPTIONS/{Subscription Id}/RESOURCEGROUPS/{Resource Group Name}/PROVIDERS/MICROSOFT.CDN/PROFILES/{Profile Name}/ENDPOINTS/{Endpoint Name}/ y={Year}/m={Month}/d={Day}/h={Hour}/m={Minutes}/PT1H.json

<span data-ttu-id="89da2-196">**Alanları açıklaması:**</span><span class="sxs-lookup"><span data-stu-id="89da2-196">**Description of fields:**</span></span>

|<span data-ttu-id="89da2-197">değer</span><span class="sxs-lookup"><span data-stu-id="89da2-197">value</span></span>|<span data-ttu-id="89da2-198">Açıklama</span><span class="sxs-lookup"><span data-stu-id="89da2-198">description</span></span>|
|-------|---------|
|<span data-ttu-id="89da2-199">Abonelik Kimliği</span><span class="sxs-lookup"><span data-stu-id="89da2-199">Subscription ID</span></span>    |<span data-ttu-id="89da2-200">Hello Azure abonelik kimliği.</span><span class="sxs-lookup"><span data-stu-id="89da2-200">ID of hello Azure Subscription.</span></span> <span data-ttu-id="89da2-201">Merhaba GUID biçiminde budur.</span><span class="sxs-lookup"><span data-stu-id="89da2-201">This is in hello Guid format.</span></span>|
|<span data-ttu-id="89da2-202">Kaynak</span><span class="sxs-lookup"><span data-stu-id="89da2-202">Resource</span></span> |<span data-ttu-id="89da2-203">Merhaba kaynak grubu toowhich hello CDN kaynak grubu adı ait.</span><span class="sxs-lookup"><span data-stu-id="89da2-203">Group Name   Name of hello resource group toowhich hello CDN resources belong.</span></span>|
|<span data-ttu-id="89da2-204">Profil adı</span><span class="sxs-lookup"><span data-stu-id="89da2-204">Profile Name</span></span> |<span data-ttu-id="89da2-205">Merhaba CDN profili adı</span><span class="sxs-lookup"><span data-stu-id="89da2-205">Name of hello CDN Profile</span></span>|
|<span data-ttu-id="89da2-206">Uç nokta adı</span><span class="sxs-lookup"><span data-stu-id="89da2-206">Endpoint Name</span></span> |<span data-ttu-id="89da2-207">Merhaba CDN uç noktası adı</span><span class="sxs-lookup"><span data-stu-id="89da2-207">Name of hello CDN Endpoint</span></span>|
|<span data-ttu-id="89da2-208">Yıl</span><span class="sxs-lookup"><span data-stu-id="89da2-208">Year</span></span>|  <span data-ttu-id="89da2-209">Örneğin, 2017 hello yılın 4 basamaklı gösterimi</span><span class="sxs-lookup"><span data-stu-id="89da2-209">4-digit representation of hello year for example, 2017</span></span>|
|<span data-ttu-id="89da2-210">Ay</span><span class="sxs-lookup"><span data-stu-id="89da2-210">Month</span></span>| <span data-ttu-id="89da2-211">Merhaba ay numarasına 2 basamaklı gösterimi.</span><span class="sxs-lookup"><span data-stu-id="89da2-211">2-digit representation of hello month number.</span></span> <span data-ttu-id="89da2-212">01 Ocak =... 12 Aralık =</span><span class="sxs-lookup"><span data-stu-id="89da2-212">01=January ... 12=December</span></span>|
|<span data-ttu-id="89da2-213">Gün</span><span class="sxs-lookup"><span data-stu-id="89da2-213">Day</span></span>|   <span data-ttu-id="89da2-214">Merhaba ayın hello 2 basamak gösterimi</span><span class="sxs-lookup"><span data-stu-id="89da2-214">2 digit representation of hello day of hello month</span></span>|
|<span data-ttu-id="89da2-215">PT1H.JSON</span><span class="sxs-lookup"><span data-stu-id="89da2-215">PT1H.json</span></span>| <span data-ttu-id="89da2-216">Merhaba analytics verilerinin depolandığı gerçek JSON dosyası</span><span class="sxs-lookup"><span data-stu-id="89da2-216">Actual JSON file where hello analytics data is stored</span></span>|

### <a name="exporting-hello-core-analytics-data-tooa-csv-file"></a><span data-ttu-id="89da2-217">Merhaba çekirdek analiz verileri tooa CSV dosyasını dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="89da2-217">Exporting hello Core Analytics Data tooa CSV File</span></span>

<span data-ttu-id="89da2-218">toomake kolay tooaccess sağladığımız temel analiz hello BT kullanılan tooeasily olabilen bir düz virgülle ayrılmış dosya biçimine hello JSON dosyaları indirme sağlayan bir araç için bir örnek kodu grafikler veya diğer toplamaları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="89da2-218">toomake it easy tooaccess hello Core Analytics, we provide a sample code for a tool, which allows downloading hello JSON files into a flat comma-separated file format, which can be used tooeasily create charts or other aggregations.</span></span>

<span data-ttu-id="89da2-219">İşte nasıl hello aracını kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="89da2-219">Here is how you can use hello tool:</span></span>

1.  <span data-ttu-id="89da2-220">Merhaba github bağlantıyı ziyaret edin: [https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv )</span><span class="sxs-lookup"><span data-stu-id="89da2-220">Visit hello github link: [https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv ](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv )</span></span>
2.  <span data-ttu-id="89da2-221">Merhaba kodu indirme</span><span class="sxs-lookup"><span data-stu-id="89da2-221">Download hello code</span></span>
3.  <span data-ttu-id="89da2-222">Yönergeler toocompile izleyin ve yapılandırma</span><span class="sxs-lookup"><span data-stu-id="89da2-222">Follow instructions toocompile and configure</span></span>
4.  <span data-ttu-id="89da2-223">Merhaba aracını çalıştırın</span><span class="sxs-lookup"><span data-stu-id="89da2-223">Run hello tool</span></span>
5.  <span data-ttu-id="89da2-224">Sonuçta elde edilen CSV dosyasını hello analiz verileri basit bir düz hiyerarşi içinde gösterir.</span><span class="sxs-lookup"><span data-stu-id="89da2-224">Resulting CSV file shows hello analytics data in a simple flat hierarchy.</span></span>

## <a name="consuming-diagnostics-logs-from-an-oms-log-analytics-repository"></a><span data-ttu-id="89da2-225">Tanılama günlüklerini bir OMS günlük analizi depodan kullanma</span><span class="sxs-lookup"><span data-stu-id="89da2-225">Consuming diagnostics logs from an OMS Log Analytics repository</span></span>
<span data-ttu-id="89da2-226">Günlük analizi Operations Management Suite (OMS), Bulut ve şirket içi ortamları toomaintain kendi kullanılabilirliğini ve performansını izler bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="89da2-226">Log Analytics is a service in Operations Management Suite (OMS) that monitors your cloud and on-premises environments toomaintain their availability and performance.</span></span> <span data-ttu-id="89da2-227">Bulut ve şirket içi ortamları ve diğer izleme araçları tooprovide analiz kaynaklar tarafından birden çok kaynakları genelinde oluşturulan veri toplar.</span><span class="sxs-lookup"><span data-stu-id="89da2-227">It collects data generated by resources in your cloud and on-premises environments and from other monitoring tools tooprovide analysis across multiple sources.</span></span> 

<span data-ttu-id="89da2-228">Günlük analizi toouse, şunları yapmalısınız [günlük kaydını etkinleştir](#enable-logging-with-azure-storage) bu makalenin önceki bölümlerinde açıklanan toohello Azure OMS günlük analizi deposu.</span><span class="sxs-lookup"><span data-stu-id="89da2-228">toouse Log Analytics, you must [enable logging](#enable-logging-with-azure-storage) toohello Azure OMS Log Analytics repository, which is discussed earlier in this article.</span></span>

### <a name="using-hello-oms-repository"></a><span data-ttu-id="89da2-229">Merhaba OMS deposu kullanma</span><span class="sxs-lookup"><span data-stu-id="89da2-229">Using hello OMS Repository</span></span>

 <span data-ttu-id="89da2-230">Diyagram aşağıdaki hello hello girdi hello mimarisi ve hello deposu çıkışları gösterir:</span><span class="sxs-lookup"><span data-stu-id="89da2-230">hello following diagram shows hello architecture of hello inputs and outputs of hello repository:</span></span>

![OMS günlük analizi deposu](./media/cdn-diagnostics-log/12_Repo-overview.png)

<span data-ttu-id="89da2-232">*Şekil 3 - günlük analizi deposu*</span><span class="sxs-lookup"><span data-stu-id="89da2-232">*Figure 3 - Log Analytics Repository*</span></span>

<span data-ttu-id="89da2-233">Yönetim çözümleri kullanılarak hello verileri çeşitli şekillerde görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="89da2-233">You can display hello data in a variety of ways by using Management Solutions.</span></span> <span data-ttu-id="89da2-234">Merhaba yönetim çözümleri edinebilirsiniz [Azure Marketi](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).</span><span class="sxs-lookup"><span data-stu-id="89da2-234">You can obtain Management Solutions from hello [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).</span></span>

<span data-ttu-id="89da2-235">Merhaba tıklayarak yönetim çözümleri Azure Marketi'nden yükleyebilirsiniz **Şimdi Al** her çözüm hello sonundaki bağlantı.</span><span class="sxs-lookup"><span data-stu-id="89da2-235">You can install management solutions from Azure marketplace by clicking hello **Get it now** link at hello bottom of each solution.</span></span>

### <a name="adding-an-oms-cdn-management-solution"></a><span data-ttu-id="89da2-236">OMS CDN yönetim çözümünü ekleme</span><span class="sxs-lookup"><span data-stu-id="89da2-236">Adding an OMS CDN Management Solution</span></span>

<span data-ttu-id="89da2-237">Bu adımları tooadd bir yönetim çözümü izleyin:</span><span class="sxs-lookup"><span data-stu-id="89da2-237">Follow these steps tooadd a Management Solution:</span></span>

1.   <span data-ttu-id="89da2-238">Zaten yapmadıysanız, toohello içinde Azure aboneliğinizi kullanarak Azure portalında oturum açın ve tooyour Pano gidin.</span><span class="sxs-lookup"><span data-stu-id="89da2-238">If you haven't already done so, sign in toohello Azure portal using your Azure subscription and go tooyour Dashboard.</span></span>
    <span data-ttu-id="89da2-239">![Azure Panosu](./media/cdn-diagnostics-log/13_Azure-dashboard.png)</span><span class="sxs-lookup"><span data-stu-id="89da2-239">![Azure Dashboard](./media/cdn-diagnostics-log/13_Azure-dashboard.png)</span></span>

2. <span data-ttu-id="89da2-240">Merhaba, **yeni** altında dikey **Market**seçin **izleme + Yönetim**.</span><span class="sxs-lookup"><span data-stu-id="89da2-240">In hello **New** blade under **Marketplace**, select **Monitoring + management**.</span></span>

    ![Market](./media/cdn-diagnostics-log/14_Marketplace.png)

3. <span data-ttu-id="89da2-242">Merhaba, **izleme + Yönetim** dikey penceresinde tıklatın **tümünü görmek**.</span><span class="sxs-lookup"><span data-stu-id="89da2-242">In hello **Monitoring + management** blade, click **See all**.</span></span>

    ![Tümünü incele](./media/cdn-diagnostics-log/15_See-all.png)

4.  <span data-ttu-id="89da2-244">CDN hello arama kutusuna arayın.</span><span class="sxs-lookup"><span data-stu-id="89da2-244">Search for CDN in hello search box.</span></span>

    ![Tümünü incele](./media/cdn-diagnostics-log/16_Search-for.png)

5.  <span data-ttu-id="89da2-246">Seçin **Azure CDN temel analiz**.</span><span class="sxs-lookup"><span data-stu-id="89da2-246">Select **Azure CDN Core Analytics**.</span></span> 

    ![Tümünü incele](./media/cdn-diagnostics-log/17_Core-analytics.png)

6.  <span data-ttu-id="89da2-248">' I tıklattıktan sonra **oluşturma**, size yeni bir OMS çalışma alanı toocreate sorular veya mevcut bir kullanın.</span><span class="sxs-lookup"><span data-stu-id="89da2-248">After clicking **Create**, you will be asked toocreate a new OMS workspace or use an existing one.</span></span> 

    ![Tümünü incele](./media/cdn-diagnostics-log/18_Adding-solution.png)

7.  <span data-ttu-id="89da2-250">Önce oluşturduğunuz hello çalışma alanını seçin.</span><span class="sxs-lookup"><span data-stu-id="89da2-250">Select hello workspace you created before.</span></span> <span data-ttu-id="89da2-251">Ardından tooadd bir Otomasyon hesabı gerekir.</span><span class="sxs-lookup"><span data-stu-id="89da2-251">You then need tooadd an automation account.</span></span>

    ![Tümünü incele](./media/cdn-diagnostics-log/19_Add-automation.png)

8. <span data-ttu-id="89da2-253">Merhaba aşağıdaki ekran doldurmak zorunda hello Otomasyon hesabı form gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="89da2-253">hello following screen shows hello automation account form you must fill out.</span></span> 

    ![Tümünü incele](./media/cdn-diagnostics-log/20_Automation.png)

9. <span data-ttu-id="89da2-255">Merhaba Otomasyon hesabı oluşturduktan sonra hazır tooadd olan çözümünüzü.</span><span class="sxs-lookup"><span data-stu-id="89da2-255">Once you have created hello automation account, you are ready tooadd your solution.</span></span> <span data-ttu-id="89da2-256">Merhaba tıklatın **oluşturma** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="89da2-256">Click hello **Create** button.</span></span>

    ![Tümünü incele](./media/cdn-diagnostics-log/21_Ready.png)

10. <span data-ttu-id="89da2-258">Çözümünüzü tooyour çalışma alanı şimdi eklendi.</span><span class="sxs-lookup"><span data-stu-id="89da2-258">Your solution has now been added tooyour workspace.</span></span> <span data-ttu-id="89da2-259">Azure portal Pano tooyour geri dönün.</span><span class="sxs-lookup"><span data-stu-id="89da2-259">Go back tooyour Azure portal Dashboard.</span></span>

    ![Tümünü incele](./media/cdn-diagnostics-log/22_Dashboard.png)

    <span data-ttu-id="89da2-261">Merhaba günlük analizi çalışma alanı toogo tooyour çalışma alanı oluşturulduğunda'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="89da2-261">Click hello Log Analytics workspace you created toogo tooyour workspace.</span></span> 

11. <span data-ttu-id="89da2-262">Merhaba tıklatın **OMS portalı** toosee yeni çözümünüz hello OMS portalında döşeme.</span><span class="sxs-lookup"><span data-stu-id="89da2-262">Click hello **OMS Portal** tile toosee your new solution in hello OMS portal.</span></span>

    ![Tümünü incele](./media/cdn-diagnostics-log/23_workspace.png)

12. <span data-ttu-id="89da2-264">OMS portalı Merhaba ekranında aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="89da2-264">Your OMS portal should now look like hello following screen:</span></span>

    ![Tümünü incele](./media/cdn-diagnostics-log/24_OMS-solution.png)

    <span data-ttu-id="89da2-266">Merhaba döşeme toosee birini birkaç görünüm verilerinizi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="89da2-266">Click one of hello tiles toosee several views into your data.</span></span>

    ![Tümünü incele](./media/cdn-diagnostics-log/25_Interior-view.png)

    <span data-ttu-id="89da2-268">Sola kaydırma yapabilirsiniz veya daha fazla sağ toosee tek bir görünüm hello verilerini temsil eden yerleştirir.</span><span class="sxs-lookup"><span data-stu-id="89da2-268">You can scroll left or right toosee further tiles representing individual views into hello data.</span></span> 

    <span data-ttu-id="89da2-269">Merhaba döşeme birine tıklayarak verileriniz hakkında daha fazla ayrıntı sağlar.</span><span class="sxs-lookup"><span data-stu-id="89da2-269">Clicking one of hello tiles gives you more details about your data.</span></span>

     ![Tümünü incele](./media/cdn-diagnostics-log/26_Further-detail.png)

### <a name="offers-and-pricing-tiers"></a><span data-ttu-id="89da2-271">Teklifler ve fiyatlandırma katmanları</span><span class="sxs-lookup"><span data-stu-id="89da2-271">Offers and pricing tiers</span></span>

<span data-ttu-id="89da2-272">Teklifler ve OMS yönetim çözümleri için fiyatlandırma katmanlarına görebilirsiniz [burada](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers).</span><span class="sxs-lookup"><span data-stu-id="89da2-272">You can see offers and pricing tiers for OMS management solutions [here](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers).</span></span>

### <a name="customizing-views"></a><span data-ttu-id="89da2-273">Görünümlerini özelleştirme</span><span class="sxs-lookup"><span data-stu-id="89da2-273">Customizing views</span></span>

<span data-ttu-id="89da2-274">Hello kullanarak verilerinizi hello görünümünü özelleştirebilirsiniz **Görünüm Tasarımcısı**.</span><span class="sxs-lookup"><span data-stu-id="89da2-274">You can customize hello view into your data by using hello **View Designer**.</span></span> <span data-ttu-id="89da2-275">Tooyour OMS çalışma alanına gidin ve tasarlamaya hello tıklayarak **Görünüm Tasarımcısı** döşeme.</span><span class="sxs-lookup"><span data-stu-id="89da2-275">Go tooyour OMS workspace and begin designing by clicking hello **View Designer** tile.</span></span>

![Görünüm Tasarımcısı](./media/cdn-diagnostics-log/27_Designer.png)

<span data-ttu-id="89da2-277">Sürükleme ve grafik türleri hello soldan bırakın ve sol hello üzerinde tooanalyze istediğiniz hello veri ayrıntıları doldurun.</span><span class="sxs-lookup"><span data-stu-id="89da2-277">You can drag and drop types of charts from hello left and fill in hello data details you want tooanalyze on hello left.</span></span>

![Görünüm Tasarımcısı](./media/cdn-diagnostics-log/28_Designer.png)

    
## <a name="log-data-delays"></a><span data-ttu-id="89da2-279">Günlük verileri gecikmeleri</span><span class="sxs-lookup"><span data-stu-id="89da2-279">Log data delays</span></span>

<span data-ttu-id="89da2-280">Verizon günlük veri gecikmeleri</span><span class="sxs-lookup"><span data-stu-id="89da2-280">Verizon log data delays</span></span> | <span data-ttu-id="89da2-281">Akamai günlük veri gecikmeleri</span><span class="sxs-lookup"><span data-stu-id="89da2-281">Akamai log data delays</span></span>
--- | ---
<span data-ttu-id="89da2-282">Verizon günlük verilerini 1 saat Gecikmeli ve uç nokta yayma işlemi tamamlandıktan sonra görünen too2 saatleri toostart yukarı gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="89da2-282">Verizon log data is 1 hour delayed, and take up too2 hours toostart appearing after endpoint propagation completion.</span></span> | <span data-ttu-id="89da2-283">Akamai günlük verilerini Gecikmeli 24 saat ve 24 saatten daha önce oluşturulduysa görünen too2 saatleri toostart alır.</span><span class="sxs-lookup"><span data-stu-id="89da2-283">Akamai log data is 24 hours delayed, and takes up too2 hours toostart appearing if it was created more than 24 hours ago.</span></span> <span data-ttu-id="89da2-284">Yeni oluşturulduysa, görünen hello günlükleri toostart için too25 saatlerini alabilir.</span><span class="sxs-lookup"><span data-stu-id="89da2-284">If it was recently created, it can take up too25 hours for hello logs toostart appearing.</span></span>

## <a name="diagnostic-log-types-for-cdn-core-analytics"></a><span data-ttu-id="89da2-285">CDN temel analiz için tanılama günlük türleri</span><span class="sxs-lookup"><span data-stu-id="89da2-285">Diagnostic log types for CDN Core Analytics</span></span>

<span data-ttu-id="89da2-286">HTTP yanıtı istatistiklerinin ve CDN POP/kenarları hello görülen çıkış istatistikleri gösteren ölçümleri içeren temel analiz günlükleri şu anda sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="89da2-286">We currently offer only Core Analytics logs, which contain metrics showing HTTP response statistics and egress statistics as seen from hello CDN POPs/edges.</span></span>

### <a name="core-analytics-metrics-details"></a><span data-ttu-id="89da2-287">Çekirdek Analytics ölçümleri ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="89da2-287">Core Analytics Metrics Details</span></span>
<span data-ttu-id="89da2-288">Aşağıdaki tablonun hello ölçümleri temel analiz günlüklerini hello kullanılabilir bir listesini gösterir.</span><span class="sxs-lookup"><span data-stu-id="89da2-288">hello following table shows a list of metrics available in hello Core Analytics logs.</span></span> <span data-ttu-id="89da2-289">Bu farklara en az olmasına rağmen tüm ölçümleri tüm sağlayıcılardan kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="89da2-289">Not all metrics are available from all providers, although such differences are minimal.</span></span> <span data-ttu-id="89da2-290">Ayrıca aşağıdaki tablonun hello belirli bir metrik sağlayıcıdan kullanılabilir olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="89da2-290">hello following table also shows if a given metric is available from a provider.</span></span> <span data-ttu-id="89da2-291">Merhaba ölçümleri trafiği üzerlerinde sahip CDN uç için kullanılabilir olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="89da2-291">Please note that hello metrics are available for only those CDN endpoints that have traffic on them.</span></span>


|<span data-ttu-id="89da2-292">Ölçüm</span><span class="sxs-lookup"><span data-stu-id="89da2-292">Metric</span></span>                     | <span data-ttu-id="89da2-293">Açıklama</span><span class="sxs-lookup"><span data-stu-id="89da2-293">Description</span></span>   | <span data-ttu-id="89da2-294">Verizon</span><span class="sxs-lookup"><span data-stu-id="89da2-294">Verizon</span></span>  | <span data-ttu-id="89da2-295">Akamai</span><span class="sxs-lookup"><span data-stu-id="89da2-295">Akamai</span></span> 
|---------------------------|---------------|---|---|
| <span data-ttu-id="89da2-296">RequestCountTotal</span><span class="sxs-lookup"><span data-stu-id="89da2-296">RequestCountTotal</span></span>         |<span data-ttu-id="89da2-297">Bu süre boyunca isteği isabet toplam sayısı</span><span class="sxs-lookup"><span data-stu-id="89da2-297">Total number of request hits during this period</span></span>| <span data-ttu-id="89da2-298">Evet</span><span class="sxs-lookup"><span data-stu-id="89da2-298">Yes</span></span>  |<span data-ttu-id="89da2-299">Evet</span><span class="sxs-lookup"><span data-stu-id="89da2-299">Yes</span></span>   |
| <span data-ttu-id="89da2-300">RequestCountHttpStatus2xx</span><span class="sxs-lookup"><span data-stu-id="89da2-300">RequestCountHttpStatus2xx</span></span> |<span data-ttu-id="89da2-301">Bir 2xx HTTP kod (örneğin, 200, 202) sonuçlandı tüm isteklerin sayısı</span><span class="sxs-lookup"><span data-stu-id="89da2-301">Count of all requests that resulted in a 2xx HTTP code (e.g. 200, 202)</span></span>              | <span data-ttu-id="89da2-302">Evet</span><span class="sxs-lookup"><span data-stu-id="89da2-302">Yes</span></span>  |<span data-ttu-id="89da2-303">Evet</span><span class="sxs-lookup"><span data-stu-id="89da2-303">Yes</span></span>   |
| <span data-ttu-id="89da2-304">RequestCountHttpStatus3xx</span><span class="sxs-lookup"><span data-stu-id="89da2-304">RequestCountHttpStatus3xx</span></span> | <span data-ttu-id="89da2-305">Bir 3xx HTTP kod (örneğin, 300, 302) sonuçlandı tüm isteklerin sayısı</span><span class="sxs-lookup"><span data-stu-id="89da2-305">Count of all requests that resulted in a 3xx HTTP code (e.g. 300, 302)</span></span>              | <span data-ttu-id="89da2-306">Evet</span><span class="sxs-lookup"><span data-stu-id="89da2-306">Yes</span></span>  |<span data-ttu-id="89da2-307">Evet</span><span class="sxs-lookup"><span data-stu-id="89da2-307">Yes</span></span>   |
| <span data-ttu-id="89da2-308">RequestCountHttpStatus4xx</span><span class="sxs-lookup"><span data-stu-id="89da2-308">RequestCountHttpStatus4xx</span></span> |<span data-ttu-id="89da2-309">Bir 4xx HTTP kod (örneğin, 400, 404) sonuçlandı tüm isteklerin sayısı</span><span class="sxs-lookup"><span data-stu-id="89da2-309">Count of all requests that resulted in a 4xx HTTP code (e.g. 400, 404)</span></span>               | <span data-ttu-id="89da2-310">Evet</span><span class="sxs-lookup"><span data-stu-id="89da2-310">Yes</span></span>   |<span data-ttu-id="89da2-311">Evet</span><span class="sxs-lookup"><span data-stu-id="89da2-311">Yes</span></span>   |
| <span data-ttu-id="89da2-312">RequestCountHttpStatus5xx</span><span class="sxs-lookup"><span data-stu-id="89da2-312">RequestCountHttpStatus5xx</span></span> | <span data-ttu-id="89da2-313">Bir 5xx HTTP kod (örneğin, 500, 504) sonuçlandı tüm isteklerin sayısı</span><span class="sxs-lookup"><span data-stu-id="89da2-313">Count of all requests that resulted in a 5xx HTTP code (e.g. 500, 504)</span></span>              | <span data-ttu-id="89da2-314">Evet</span><span class="sxs-lookup"><span data-stu-id="89da2-314">Yes</span></span>  |<span data-ttu-id="89da2-315">Evet</span><span class="sxs-lookup"><span data-stu-id="89da2-315">Yes</span></span>   |
| <span data-ttu-id="89da2-316">RequestCountHttpStatusOthers</span><span class="sxs-lookup"><span data-stu-id="89da2-316">RequestCountHttpStatusOthers</span></span> |  <span data-ttu-id="89da2-317">Diğer tüm HTTP kodları (dışında 2xx-5xx) sayısı</span><span class="sxs-lookup"><span data-stu-id="89da2-317">Count of all other HTTP codes (outside of 2xx-5xx)</span></span> | <span data-ttu-id="89da2-318">Evet</span><span class="sxs-lookup"><span data-stu-id="89da2-318">Yes</span></span>  |<span data-ttu-id="89da2-319">Evet</span><span class="sxs-lookup"><span data-stu-id="89da2-319">Yes</span></span>   |
| <span data-ttu-id="89da2-320">RequestCountHttpStatus200</span><span class="sxs-lookup"><span data-stu-id="89da2-320">RequestCountHttpStatus200</span></span> | <span data-ttu-id="89da2-321">200 HTTP kod yanıtıyla sonuçlanan tüm isteklerin sayısı</span><span class="sxs-lookup"><span data-stu-id="89da2-321">Count of all requests that resulted in a 200 HTTP code response</span></span>              |<span data-ttu-id="89da2-322">Hayır</span><span class="sxs-lookup"><span data-stu-id="89da2-322">No</span></span>   |<span data-ttu-id="89da2-323">Evet</span><span class="sxs-lookup"><span data-stu-id="89da2-323">Yes</span></span>   |
| <span data-ttu-id="89da2-324">RequestCountHttpStatus206</span><span class="sxs-lookup"><span data-stu-id="89da2-324">RequestCountHttpStatus206</span></span> | <span data-ttu-id="89da2-325">206 HTTP kod yanıtıyla sonuçlanan tüm isteklerin sayısı</span><span class="sxs-lookup"><span data-stu-id="89da2-325">Count of all requests that resulted in a 206 HTTP code response</span></span>              |<span data-ttu-id="89da2-326">Hayır</span><span class="sxs-lookup"><span data-stu-id="89da2-326">No</span></span>   |<span data-ttu-id="89da2-327">Evet</span><span class="sxs-lookup"><span data-stu-id="89da2-327">Yes</span></span>   |
| <span data-ttu-id="89da2-328">RequestCountHttpStatus302</span><span class="sxs-lookup"><span data-stu-id="89da2-328">RequestCountHttpStatus302</span></span> | <span data-ttu-id="89da2-329">Bir 302 HTTP kod yanıtıyla sonuçlanan tüm isteklerin sayısı</span><span class="sxs-lookup"><span data-stu-id="89da2-329">Count of all requests that resulted in a 302 HTTP code response</span></span>              |<span data-ttu-id="89da2-330">Hayır</span><span class="sxs-lookup"><span data-stu-id="89da2-330">No</span></span>   |<span data-ttu-id="89da2-331">Evet</span><span class="sxs-lookup"><span data-stu-id="89da2-331">Yes</span></span>   |
| <span data-ttu-id="89da2-332">RequestCountHttpStatus304</span><span class="sxs-lookup"><span data-stu-id="89da2-332">RequestCountHttpStatus304</span></span> |  <span data-ttu-id="89da2-333">304 HTTP kod yanıtıyla sonuçlanan tüm isteklerin sayısı</span><span class="sxs-lookup"><span data-stu-id="89da2-333">Count of all requests that resulted in a 304 HTTP code response</span></span>             |<span data-ttu-id="89da2-334">Hayır</span><span class="sxs-lookup"><span data-stu-id="89da2-334">No</span></span>   |<span data-ttu-id="89da2-335">Evet</span><span class="sxs-lookup"><span data-stu-id="89da2-335">Yes</span></span>   |
| <span data-ttu-id="89da2-336">RequestCountHttpStatus404</span><span class="sxs-lookup"><span data-stu-id="89da2-336">RequestCountHttpStatus404</span></span> | <span data-ttu-id="89da2-337">404 HTTP kod yanıtıyla sonuçlanan tüm isteklerin sayısı</span><span class="sxs-lookup"><span data-stu-id="89da2-337">Count of all requests that resulted in a 404 HTTP code response</span></span>              |<span data-ttu-id="89da2-338">Hayır</span><span class="sxs-lookup"><span data-stu-id="89da2-338">No</span></span>   |<span data-ttu-id="89da2-339">Evet</span><span class="sxs-lookup"><span data-stu-id="89da2-339">Yes</span></span>   |
| <span data-ttu-id="89da2-340">RequestCountCacheHit</span><span class="sxs-lookup"><span data-stu-id="89da2-340">RequestCountCacheHit</span></span> |<span data-ttu-id="89da2-341">Önbelleği isabet sonuçlandı tüm isteklerin sayısı.</span><span class="sxs-lookup"><span data-stu-id="89da2-341">Count of all requests that resulted in a Cache Hit.</span></span> <span data-ttu-id="89da2-342">Bu, doğrudan hello POP toohello istemci hello varlık sunulduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="89da2-342">This means hello asset was served directly from hello POP toohello Client.</span></span>               | <span data-ttu-id="89da2-343">Evet</span><span class="sxs-lookup"><span data-stu-id="89da2-343">Yes</span></span>  |<span data-ttu-id="89da2-344">Hayır</span><span class="sxs-lookup"><span data-stu-id="89da2-344">No</span></span>   |
| <span data-ttu-id="89da2-345">RequestCountCacheMiss</span><span class="sxs-lookup"><span data-stu-id="89da2-345">RequestCountCacheMiss</span></span> | <span data-ttu-id="89da2-346">Önbellek isabetsizliği sonuçlandı tüm isteklerin sayısı.</span><span class="sxs-lookup"><span data-stu-id="89da2-346">Count of all requests that resulted in a Cache Miss.</span></span> <span data-ttu-id="89da2-347">Bu hello varlık hello POP en yakın toohello istemcide bulunamadı ve bu nedenle kaynak hello alınan anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="89da2-347">This means hello asset was not found on hello POP closest toohello client, and therefore was retrieved from hello Origin.</span></span>              |<span data-ttu-id="89da2-348">Evet</span><span class="sxs-lookup"><span data-stu-id="89da2-348">Yes</span></span>   | <span data-ttu-id="89da2-349">Hayır</span><span class="sxs-lookup"><span data-stu-id="89da2-349">No</span></span>  |
| <span data-ttu-id="89da2-350">RequestCountCacheNoCache</span><span class="sxs-lookup"><span data-stu-id="89da2-350">RequestCountCacheNoCache</span></span> | <span data-ttu-id="89da2-351">Merhaba kenar tooa kullanıcı yapılandırmasını son önbelleğe engellenir tooan varlık isteklerinin tüm sayısı.</span><span class="sxs-lookup"><span data-stu-id="89da2-351">Count of all requests tooan asset that are prevented from being cached due tooa user configuration on hello edge.</span></span>              |<span data-ttu-id="89da2-352">Evet</span><span class="sxs-lookup"><span data-stu-id="89da2-352">Yes</span></span>   | <span data-ttu-id="89da2-353">Hayır</span><span class="sxs-lookup"><span data-stu-id="89da2-353">No</span></span>  |
| <span data-ttu-id="89da2-354">RequestCountCacheUncacheable</span><span class="sxs-lookup"><span data-stu-id="89da2-354">RequestCountCacheUncacheable</span></span> | <span data-ttu-id="89da2-355">Merhaba varlığın Cache-Control tarafından önbelleğe alınmış engellenir tooassets ister ve bunu POP veya hello HTTP istemci tarafından önbelleğe alınması gereken değil olduğunu belirtmek üstbilgileri süresi tüm sayısı</span><span class="sxs-lookup"><span data-stu-id="89da2-355">Count of all requests tooassets that are prevented from being cached by hello asset's Cache-Control and Expires headers, which indicate that it should not be cached on a POP or by hello HTTP client</span></span>                |<span data-ttu-id="89da2-356">Evet</span><span class="sxs-lookup"><span data-stu-id="89da2-356">Yes</span></span>   |<span data-ttu-id="89da2-357">Hayır</span><span class="sxs-lookup"><span data-stu-id="89da2-357">No</span></span>   |
| <span data-ttu-id="89da2-358">RequestCountCacheOthers</span><span class="sxs-lookup"><span data-stu-id="89da2-358">RequestCountCacheOthers</span></span> | <span data-ttu-id="89da2-359">Tarafından yukarıda kapsanmayan önbellek durumundaki tüm isteklerin sayısı.</span><span class="sxs-lookup"><span data-stu-id="89da2-359">Count of all requests with cache status not covered by above.</span></span>              |<span data-ttu-id="89da2-360">Evet</span><span class="sxs-lookup"><span data-stu-id="89da2-360">Yes</span></span>   | <span data-ttu-id="89da2-361">Hayır</span><span class="sxs-lookup"><span data-stu-id="89da2-361">No</span></span>  |
| <span data-ttu-id="89da2-362">EgressTotal</span><span class="sxs-lookup"><span data-stu-id="89da2-362">EgressTotal</span></span> | <span data-ttu-id="89da2-363">Giden veri aktarımı GB</span><span class="sxs-lookup"><span data-stu-id="89da2-363">Outbound data transfer in GB</span></span>              |<span data-ttu-id="89da2-364">Evet</span><span class="sxs-lookup"><span data-stu-id="89da2-364">Yes</span></span>   |<span data-ttu-id="89da2-365">Evet</span><span class="sxs-lookup"><span data-stu-id="89da2-365">Yes</span></span>   |
| <span data-ttu-id="89da2-366">EgressHttpStatus2xx</span><span class="sxs-lookup"><span data-stu-id="89da2-366">EgressHttpStatus2xx</span></span> | <span data-ttu-id="89da2-367">Giden veri aktarımı * 2xx HTTP durum kodları GB ile yanıtlar için</span><span class="sxs-lookup"><span data-stu-id="89da2-367">Outbound data transfer* for responses with 2xx HTTP status codes in GB</span></span>            |<span data-ttu-id="89da2-368">Evet</span><span class="sxs-lookup"><span data-stu-id="89da2-368">Yes</span></span>   |<span data-ttu-id="89da2-369">Hayır</span><span class="sxs-lookup"><span data-stu-id="89da2-369">No</span></span>   |
| <span data-ttu-id="89da2-370">EgressHttpStatus3xx</span><span class="sxs-lookup"><span data-stu-id="89da2-370">EgressHttpStatus3xx</span></span> | <span data-ttu-id="89da2-371">3xx HTTP durum kodları GB ile yanıtlar için giden veri aktarımı</span><span class="sxs-lookup"><span data-stu-id="89da2-371">Outbound data transfer for responses with 3xx HTTP status codes in GB</span></span>              |<span data-ttu-id="89da2-372">Evet</span><span class="sxs-lookup"><span data-stu-id="89da2-372">Yes</span></span>   |<span data-ttu-id="89da2-373">Hayır</span><span class="sxs-lookup"><span data-stu-id="89da2-373">No</span></span>   |
| <span data-ttu-id="89da2-374">EgressHttpStatus4xx</span><span class="sxs-lookup"><span data-stu-id="89da2-374">EgressHttpStatus4xx</span></span> | <span data-ttu-id="89da2-375">4xx HTTP durum kodları GB ile yanıtlar için giden veri aktarımı</span><span class="sxs-lookup"><span data-stu-id="89da2-375">Outbound data transfer for responses with 4xx HTTP status codes in GB</span></span>               |<span data-ttu-id="89da2-376">Evet</span><span class="sxs-lookup"><span data-stu-id="89da2-376">Yes</span></span>   | <span data-ttu-id="89da2-377">Hayır</span><span class="sxs-lookup"><span data-stu-id="89da2-377">No</span></span>  |
| <span data-ttu-id="89da2-378">EgressHttpStatus5xx</span><span class="sxs-lookup"><span data-stu-id="89da2-378">EgressHttpStatus5xx</span></span> | <span data-ttu-id="89da2-379">5xx HTTP durum kodları GB ile yanıtlar için giden veri aktarımı</span><span class="sxs-lookup"><span data-stu-id="89da2-379">Outbound data transfer for responses with 5xx HTTP status codes in GB</span></span>               |<span data-ttu-id="89da2-380">Evet</span><span class="sxs-lookup"><span data-stu-id="89da2-380">Yes</span></span>   |  <span data-ttu-id="89da2-381">Hayır</span><span class="sxs-lookup"><span data-stu-id="89da2-381">No</span></span> |
| <span data-ttu-id="89da2-382">EgressHttpStatusOthers</span><span class="sxs-lookup"><span data-stu-id="89da2-382">EgressHttpStatusOthers</span></span> | <span data-ttu-id="89da2-383">Giden veri aktarımı için diğer HTTP durum kodları GB yanıtları</span><span class="sxs-lookup"><span data-stu-id="89da2-383">Outbound data transfer for responses with other HTTP status codes in GB</span></span>                |<span data-ttu-id="89da2-384">Evet</span><span class="sxs-lookup"><span data-stu-id="89da2-384">Yes</span></span>   |<span data-ttu-id="89da2-385">Hayır</span><span class="sxs-lookup"><span data-stu-id="89da2-385">No</span></span>   |
| <span data-ttu-id="89da2-386">EgressCacheHit</span><span class="sxs-lookup"><span data-stu-id="89da2-386">EgressCacheHit</span></span> |  <span data-ttu-id="89da2-387">Giden veri teslim edilen yanıtlar için doğrudan hello CDN önbellekten CDN POP/kenarları hello üzerinde aktarımı</span><span class="sxs-lookup"><span data-stu-id="89da2-387">Outbound data transfer for responses that were delivered directly from hello CDN cache on hello CDN POPs/Edges</span></span>  |<span data-ttu-id="89da2-388">Evet</span><span class="sxs-lookup"><span data-stu-id="89da2-388">Yes</span></span>   |  <span data-ttu-id="89da2-389">Hayır</span><span class="sxs-lookup"><span data-stu-id="89da2-389">No</span></span> |
| <span data-ttu-id="89da2-390">EgressCacheMiss</span><span class="sxs-lookup"><span data-stu-id="89da2-390">EgressCacheMiss</span></span> | <span data-ttu-id="89da2-391">Sırasında değil POP sunucu en yakın hello bulunan ve hello kaynak sunucudan alınan yanıt için giden veri aktarımı</span><span class="sxs-lookup"><span data-stu-id="89da2-391">Outbound data transfer for responses that were not found on hello nearest POP server, and retrieved from hello origin server</span></span>              |<span data-ttu-id="89da2-392">Evet</span><span class="sxs-lookup"><span data-stu-id="89da2-392">Yes</span></span>   |  <span data-ttu-id="89da2-393">Hayır</span><span class="sxs-lookup"><span data-stu-id="89da2-393">No</span></span> |
| <span data-ttu-id="89da2-394">EgressCacheNoCache</span><span class="sxs-lookup"><span data-stu-id="89da2-394">EgressCacheNoCache</span></span> | <span data-ttu-id="89da2-395">Merhaba kenar tooa kullanıcı yapılandırmasını son önbelleğe engellenir varlıklar için giden veri aktarımı.</span><span class="sxs-lookup"><span data-stu-id="89da2-395">Outbound data transfer for assets that are prevented from being cached due tooa user configuration on hello edge.</span></span>                |<span data-ttu-id="89da2-396">Evet</span><span class="sxs-lookup"><span data-stu-id="89da2-396">Yes</span></span>   |<span data-ttu-id="89da2-397">Hayır</span><span class="sxs-lookup"><span data-stu-id="89da2-397">No</span></span>   |
| <span data-ttu-id="89da2-398">EgressCacheUncacheable</span><span class="sxs-lookup"><span data-stu-id="89da2-398">EgressCacheUncacheable</span></span> | <span data-ttu-id="89da2-399">Merhaba varlığın Cache-Control ve/veya onu POP veya hello HTTP istemci tarafından önbelleğe alınması gereken değil olduğunu belirtmek Expires üstbilgileri tarafından önbelleğe engellenir varlıklar için giden veri aktarımı</span><span class="sxs-lookup"><span data-stu-id="89da2-399">Outbound data transfer for assets that are prevented from being cached by hello asset's Cache-Control and/or Expires headers, which indicate that it should not be cached on a POP or by hello HTTP client</span></span>                    |<span data-ttu-id="89da2-400">Evet</span><span class="sxs-lookup"><span data-stu-id="89da2-400">Yes</span></span>   | <span data-ttu-id="89da2-401">Hayır</span><span class="sxs-lookup"><span data-stu-id="89da2-401">No</span></span>  |
| <span data-ttu-id="89da2-402">EgressCacheOthers</span><span class="sxs-lookup"><span data-stu-id="89da2-402">EgressCacheOthers</span></span> |  <span data-ttu-id="89da2-403">Giden veri diğer önbellek senaryolar için aktarır.</span><span class="sxs-lookup"><span data-stu-id="89da2-403">Outbound data transfers for other cache scenarios.</span></span>             |<span data-ttu-id="89da2-404">Evet</span><span class="sxs-lookup"><span data-stu-id="89da2-404">Yes</span></span>   | <span data-ttu-id="89da2-405">Hayır</span><span class="sxs-lookup"><span data-stu-id="89da2-405">No</span></span>  |

<span data-ttu-id="89da2-406">* Giden veri aktarımı CDN POP sunucuları toohello istemciden teslim tootraffic başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="89da2-406">*Outbound data transfer refers tootraffic delivered from CDN POP servers toohello client.</span></span>


### <a name="schema-of-hello-core-analytics-logs"></a><span data-ttu-id="89da2-407">Merhaba çekirdek analiz günlükleri şeması</span><span class="sxs-lookup"><span data-stu-id="89da2-407">Schema of hello Core Analytics Logs</span></span> 

<span data-ttu-id="89da2-408">Tüm günlükleri JSON biçiminde depolanır ve her bir giriş hello şema altına aşağıdaki dize alanları vardır:</span><span class="sxs-lookup"><span data-stu-id="89da2-408">All logs are stored in JSON format and each entry has string fields following hello below schema:</span></span>

```json
    "records": [
        {
            "time": "2017-04-27T01:00:00",
            "resourceId": "<ARM Resource Id of hello CDN Endpoint>",
            "operationName": "Microsoft.Cdn/profiles/endpoints/contentDelivery",
            "category": "CoreAnalytics",
            "properties": {
                "DomainName": "<Name of hello domain for which hello statistics is reported>",
                "RequestCountTotal": integer value,
                "RequestCountHttpStatus2xx": integer value,
                "RequestCountHttpStatus3xx": integer value,
                "RequestCountHttpStatus4xx": integer value,
                "RequestCountHttpStatus5xx": integer value,
                "RequestCountHttpStatusOthers": integer value,
                "RequestCountHttpStatus200": integer value,
                "RequestCountHttpStatus206": integer value,
                "RequestCountHttpStatus302": integer value,
                "RequestCountHttpStatus304": integer value,
                "RequestCountHttpStatus404": integer value,
                "RequestCountCacheHit": integer value,
                "RequestCountCacheMiss": integer value,
                "RequestCountCacheNoCache": integer value,
                "RequestCountCacheUncacheable": integer value,
                "RequestCountCacheOthers": integer value,
                "EgressTotal": double value,
                "EgressHttpStatus2xx": double value,
                "EgressHttpStatus3xx": double value,
                "EgressHttpStatus4xx": double value,
                "EgressHttpStatus5xx": double value,
                "EgressHttpStatusOthers": double value,
                "EgressCacheHit": double value,
                "EgressCacheMiss": double value,
                "EgressCacheNoCache": double value,
                "EgressCacheUncacheable": double value,
                "EgressCacheOthers": double value,
            }
        }

    ]
}
```

<span data-ttu-id="89da2-409">Burada Başlangıç 'saati' hello istatistikleri bildirilen hello saat sınır hello başlangıç saati gösterir.</span><span class="sxs-lookup"><span data-stu-id="89da2-409">Where hello ‘time’ represents hello start time of hello hour boundary for which hello statistics is reported.</span></span> <span data-ttu-id="89da2-410">Ölçüm çift veya tamsayı değeri yerine bir CDN sağlayıcı tarafından desteklenmediğinde bir null değer olacaktır.</span><span class="sxs-lookup"><span data-stu-id="89da2-410">When a metric is not supported by a CDN provider, instead of a double or integer value, there will be a null value.</span></span> <span data-ttu-id="89da2-411">Bu null değer ölçüm hello yokluğu gösterir ve bu 0 değerinden farklı.</span><span class="sxs-lookup"><span data-stu-id="89da2-411">This null value indicates hello absence of a metric, and this is different from a 0 value.</span></span> <span data-ttu-id="89da2-412">Ayrıca, bu ölçümleri hello uç noktasında yapılandırılmış etki alanı başına bir dizi olacaktır unutmayın.</span><span class="sxs-lookup"><span data-stu-id="89da2-412">Also note that there will be one set of these metrics per domain configured on hello endpoint.</span></span>

<span data-ttu-id="89da2-413">Aşağıdaki örnek özellikleri:</span><span class="sxs-lookup"><span data-stu-id="89da2-413">Example properties below:</span></span>

```json
{
     "DomainName": "manlingakamaitest2.azureedge.net",
     "RequestCountTotal": 480,
     "RequestCountHttpStatus2xx": 480,
     "RequestCountHttpStatus3xx": 0,
     "RequestCountHttpStatus4xx": 0,
     "RequestCountHttpStatus5xx": 0,
     "RequestCountHttpStatusOthers": 0,
     "RequestCountHttpStatus200": 480,
     "RequestCountHttpStatus206": 0,
     "RequestCountHttpStatus302": 0,
     "RequestCountHttpStatus304": 0,
     "RequestCountHttpStatus404": 0,
     "RequestCountCacheHit": null,
     "RequestCountCacheMiss": null,
     "RequestCountCacheNoCache": null,
     "RequestCountCacheUncacheable": null,
     "RequestCountCacheOthers": null,
     "EgressTotal": 0.09,
     "EgressHttpStatus2xx": null,
     "EgressHttpStatus3xx": null,
     "EgressHttpStatus4xx": null,
     "EgressHttpStatus5xx": null,
     "EgressHttpStatusOthers": null,
     "EgressCacheHit": null,
     "EgressCacheMiss": null,
     "EgressCacheNoCache": null,
     "EgressCacheUncacheable": null,
     "EgressCacheOthers": null
}

```

## <a name="additional-resources"></a><span data-ttu-id="89da2-414">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="89da2-414">Additional resources</span></span>

* [<span data-ttu-id="89da2-415">Azure tanılama günlükleri</span><span class="sxs-lookup"><span data-stu-id="89da2-415">Azure Diagnostic logs</span></span>](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)
* [<span data-ttu-id="89da2-416">Azure CDN ek Portalı aracılığıyla temel analiz</span><span class="sxs-lookup"><span data-stu-id="89da2-416">Core analytics via Azure CDN supplemental portal</span></span>](https://docs.microsoft.com/azure/cdn/cdn-analyze-usage-patterns)
* [<span data-ttu-id="89da2-417">Azure OMS günlük analizi</span><span class="sxs-lookup"><span data-stu-id="89da2-417">Azure OMS Log Analytics</span></span>](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-overview)
* [<span data-ttu-id="89da2-418">Azure günlük analizi REST API'si</span><span class="sxs-lookup"><span data-stu-id="89da2-418">Azure Log Analytics REST API</span></span>](https://docs.microsoft.com/en-us/rest/api/loganalytics)







