---
title: "bir Azure Storage hesabı aaaHow toomonitor | Microsoft Docs"
description: "Nasıl toomonitor kullanarak bir depolama hesabı azure'da hello Azure portal hakkında bilgi edinin."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: b83cba7b-4627-4ba7-b5d0-f1039fe30e78
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: marsma
ms.openlocfilehash: 9a939e0b5db687c1b7b7857399321f681df2056a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-storage-account-in-hello-azure-portal"></a><span data-ttu-id="91ae4-103">İzleyici bir depolama hesabında hello Azure portalı</span><span class="sxs-lookup"><span data-stu-id="91ae4-103">Monitor a storage account in hello Azure portal</span></span>

<span data-ttu-id="91ae4-104">[Azure Storage Analytics](../storage-analytics.md) tabloları ve tüm depolama hizmetleri ve günlükleri BLOB, kuyruklar, ölçümleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="91ae4-104">[Azure Storage Analytics](../storage-analytics.md) provides metrics for all storage services, and logs for blobs, queues, and tables.</span></span> <span data-ttu-id="91ae4-105">Merhaba kullanabilirsiniz [Azure portal](https://portal.azure.com) tooconfigure hangi ölçümleri ve günlükleri hesabınız için kaydedilen ve ölçümleri verilerinizi görsel gösterimi sağlamak grafikleri yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="91ae4-105">You can use hello [Azure portal](https://portal.azure.com) tooconfigure which metrics and logs are recorded for your account, and configure charts that provide visual representations of your metrics data.</span></span>

> [!NOTE]
> <span data-ttu-id="91ae4-106">Hello Azure portal izleme verileri inceleniyor ile ilişkili maliyetleri vardır.</span><span class="sxs-lookup"><span data-stu-id="91ae4-106">There are costs associated with examining monitoring data in hello Azure portal.</span></span> <span data-ttu-id="91ae4-107">Daha fazla bilgi için bkz: [depolama çözümlemeleri ve faturalama](/rest/api/storageservices/Storage-Analytics-and-Billing).</span><span class="sxs-lookup"><span data-stu-id="91ae4-107">For more information, see [Storage Analytics and Billing](/rest/api/storageservices/Storage-Analytics-and-Billing).</span></span>
>
> <span data-ttu-id="91ae4-108">Azure File storage şu anda Storage Analytics ölçümleri destekliyor, ancak henüz günlük kaydını desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="91ae4-108">Azure File storage currently supports Storage Analytics metrics, but does not yet support logging.</span></span>
>
> <span data-ttu-id="91ae4-109">Bir çoğaltma türü, bölge olarak yedekli depolama (ZRS) şu anda depolama hesaplarıyla hello ölçümleri veya etkin bir günlüğe kaydetme özelliğine sahip değilsiniz.</span><span class="sxs-lookup"><span data-stu-id="91ae4-109">Storage accounts with a replication type of Zone-Redundant Storage (ZRS) currently do not have hello metrics or logging capability enabled.</span></span>
> 
> <span data-ttu-id="91ae4-110">Kapsamlı bir kılavuz depolama çözümlemeleri ve diğer araçları tooidentify kullanma hakkında bilgi için tanılama ve Azure Storage ile ilgili sorunları giderme bkz [izleme, tanılama ve Microsoft Azure Storage sorun giderme](../storage-monitoring-diagnosing-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="91ae4-110">For an in-depth guide on using Storage Analytics and other tools tooidentify, diagnose, and troubleshoot Azure Storage-related issues, see [Monitor, diagnose, and troubleshoot Microsoft Azure Storage](../storage-monitoring-diagnosing-troubleshooting.md).</span></span>
>

## <a name="configure-monitoring-for-a-storage-account"></a><span data-ttu-id="91ae4-111">Bir depolama hesabı için izlemeyi Yapılandır</span><span class="sxs-lookup"><span data-stu-id="91ae4-111">Configure monitoring for a storage account</span></span>

1. <span data-ttu-id="91ae4-112">Merhaba, [Azure portal](https://portal.azure.com)seçin **depolama hesapları**, sonra da hello depolama hesabı adı tooopen hello hesap Panosu.</span><span class="sxs-lookup"><span data-stu-id="91ae4-112">In hello [Azure portal](https://portal.azure.com), select **Storage accounts**, then hello storage account name tooopen hello account dashboard.</span></span>
1. <span data-ttu-id="91ae4-113">Seçin **tanılama** hello içinde **izleme** hello menü dikey bölümü.</span><span class="sxs-lookup"><span data-stu-id="91ae4-113">Select **Diagnostics** in hello **MONITORING** section of hello menu blade.</span></span>

    ![MonitoringOptions](./media/storage-monitor-storage-account/stg-enable-metrics-00.png)

1. <span data-ttu-id="91ae4-115">Select hello **türü** her ölçümleri verilerin **hizmet** toomonitor istiyor ve hello **Bekletme İlkesi** hello veriler için.</span><span class="sxs-lookup"><span data-stu-id="91ae4-115">Select hello **type** of metrics data for each **service** you wish toomonitor, and hello **retention policy** for hello data.</span></span> <span data-ttu-id="91ae4-116">Ayrıca ayarlayarak izleme devre dışı bırakabilirsiniz **durum** çok**devre dışı**.</span><span class="sxs-lookup"><span data-stu-id="91ae4-116">You can also disable monitoring by setting **Status** too**Off**.</span></span>

    ![MonitoringOptions](./media/storage-monitor-storage-account/stg-enable-metrics-01.png)

   <span data-ttu-id="91ae4-118">Her hizmet için etkinleştirebilirsiniz ölçümleri her ikisi de yeni depolama hesapları için varsayılan olarak etkinleştirilen iki tür vardır:</span><span class="sxs-lookup"><span data-stu-id="91ae4-118">There are two types of metrics you can enable for each service, both of which are enabled by default for new storage accounts:</span></span>

   * <span data-ttu-id="91ae4-119">**Birleşik**: giriş/çıkış, kullanılabilirlik, gecikme ve başarı yüzdeleri gibi ölçümleri toplar.</span><span class="sxs-lookup"><span data-stu-id="91ae4-119">**Aggregate**: Collects metrics such as ingress/egress, availability, latency, and success percentages.</span></span> <span data-ttu-id="91ae4-120">Bu ölçümler hello blob, kuyruk, tablo ve Dosya Hizmetleri için toplanır.</span><span class="sxs-lookup"><span data-stu-id="91ae4-120">These metrics are aggregated for hello blob, queue, table, and file services.</span></span>
   * <span data-ttu-id="91ae4-121">**API başına**: ek toohello toplama ölçümlerini, hello Azure depolama hizmeti API'si her depolama işlem ölçümlerini aynı kümesini toplar hello.</span><span class="sxs-lookup"><span data-stu-id="91ae4-121">**Per API**: In addition toohello aggregate metrics, collects hello same set of metrics for each storage operation in hello Azure Storage service API.</span></span>

   <span data-ttu-id="91ae4-122">tooset hello veri bekletme ilkesi, taşıma hello **bekletme (gün)** kaydırıcı veya hello 1 too365 gelen veri tooretain gün sayısını girin.</span><span class="sxs-lookup"><span data-stu-id="91ae4-122">tooset hello data retention policy, move hello **Retention (days)** slider or enter hello number of days of data tooretain, from 1 too365.</span></span> <span data-ttu-id="91ae4-123">Yeni depolama hesapları için Hello varsayılan yedi gündür.</span><span class="sxs-lookup"><span data-stu-id="91ae4-123">hello default for new storage accounts is seven days.</span></span> <span data-ttu-id="91ae4-124">Tooset bir bekletme ilkesi istemiyorsanız sıfır girin.</span><span class="sxs-lookup"><span data-stu-id="91ae4-124">If you do not want tooset a retention policy, enter zero.</span></span> <span data-ttu-id="91ae4-125">Bekletme İlkesi yok ise, izleme verilerini tooyou toodelete hello olur.</span><span class="sxs-lookup"><span data-stu-id="91ae4-125">If there is no retention policy, it is up tooyou toodelete hello monitoring data.</span></span>

   > [!WARNING]
   > <span data-ttu-id="91ae4-126">Ölçüm verilerini el ile sildiğinizde ücretlendirilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91ae4-126">You are charged when you manually delete metrics data.</span></span> <span data-ttu-id="91ae4-127">Eski analiz verileri (veri bekletme ilkeniz eski) herhangi bir ücret ödemeden hello sistem tarafından silinir.</span><span class="sxs-lookup"><span data-stu-id="91ae4-127">Stale analytics data (data older than your retention policy) is deleted by hello system at no cost.</span></span> <span data-ttu-id="91ae4-128">Tooretain depolama analiz verileri hesabınız için ne kadar süreyle istediğinize bağlı bir bekletme ilkesi ayarı öneririz.</span><span class="sxs-lookup"><span data-stu-id="91ae4-128">We recommend setting a retention policy based on how long you want tooretain storage analytics data for your account.</span></span> <span data-ttu-id="91ae4-129">Bkz: [ne yapmak tabi storage ölçümleri etkinleştirdiğinizde ücretlendirilen?](../common/storage-enable-and-view-metrics.md#what-charges-do-you-incur-when-you-enable-storage-metrics) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="91ae4-129">See [What charges do you incur when you enable storage metrics?](../common/storage-enable-and-view-metrics.md#what-charges-do-you-incur-when-you-enable-storage-metrics) for more information.</span></span>
   >

1. <span data-ttu-id="91ae4-130">Merhaba İzleme yapılandırmasını tamamladığınızda, seçin **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="91ae4-130">When you finish hello monitoring configuration, select **Save**.</span></span>

<span data-ttu-id="91ae4-131">Varsayılan bir ölçümleri hello bireysel hizmet Kanatlar (blob, kuyruk, tablo ve dosya) yanı sıra hello depolama hesabı dikey grafiklerinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="91ae4-131">A default set of metrics is displayed in charts on hello storage account blade, as well as hello individual service blades (blob, queue, table, and file).</span></span> <span data-ttu-id="91ae4-132">Bir hizmet için ölçümleri etkinleştirdikten sonra kendi grafiklerinde veri tooappear tooan saattir yukarı sürebilir.</span><span class="sxs-lookup"><span data-stu-id="91ae4-132">Once you've enabled metrics for a service, it may take up tooan hour for data tooappear in its charts.</span></span> <span data-ttu-id="91ae4-133">Seçebileceğiniz **Düzenle** üzerinde herhangi bir ölçümü grafik çok[hangi ölçümlerini yapılandırma](#how-to-customize-metrics-charts) hello grafikte görüntülenen.</span><span class="sxs-lookup"><span data-stu-id="91ae4-133">You can select **Edit** on any metric chart too[configure which metrics](#how-to-customize-metrics-charts) are displayed in hello chart.</span></span>

<span data-ttu-id="91ae4-134">Ölçümleri toplama ve günlüğe kaydetme ayarlayarak devre dışı bırakabilirsiniz **durum** çok**devre dışı**.</span><span class="sxs-lookup"><span data-stu-id="91ae4-134">You can disable metrics collection and logging by setting **Status** too**Off**.</span></span>

> [!NOTE]
> <span data-ttu-id="91ae4-135">Azure depolama kullanan [tablo depolama](../common/storage-introduction.md#table-storage) toostore hello ölçümleri depolama hesabı ve hesabınızda tablolardaki depoları hello ölçümleri.</span><span class="sxs-lookup"><span data-stu-id="91ae4-135">Azure Storage uses [table storage](../common/storage-introduction.md#table-storage) toostore hello metrics for your storage account, and stores hello metrics in tables in your account.</span></span> <span data-ttu-id="91ae4-136">Daha fazla bilgi için bkz.</span><span class="sxs-lookup"><span data-stu-id="91ae4-136">For more information, see.</span></span> <span data-ttu-id="91ae4-137">[Ölçümleri nasıl depolandığını](../common/storage-analytics.md#how-metrics-are-stored).</span><span class="sxs-lookup"><span data-stu-id="91ae4-137">[How metrics are stored](../common/storage-analytics.md#how-metrics-are-stored).</span></span>
>

## <a name="customize-metrics-charts"></a><span data-ttu-id="91ae4-138">Ölçümler grafiklerde özelleştirme</span><span class="sxs-lookup"><span data-stu-id="91ae4-138">Customize metrics charts</span></span>

<span data-ttu-id="91ae4-139">Aşağıdaki yordam toochoose hello hangi depolama ölçümleri tooview ölçümleri grafik kullanın.</span><span class="sxs-lookup"><span data-stu-id="91ae4-139">Use hello following procedure toochoose which storage metrics tooview in a metrics chart.</span></span> 

1. <span data-ttu-id="91ae4-140">Hello Azure portalında bir depolama ölçüm grafik görüntüleyerek başlatın.</span><span class="sxs-lookup"><span data-stu-id="91ae4-140">Start by displaying a storage metric chart in hello Azure portal.</span></span> <span data-ttu-id="91ae4-141">Merhaba grafiklerde bulabilirsiniz **depolama hesabı dikey** ve hello **ölçümleri** dikey bir bireysel hizmet (blob, kuyruk, tablo, dosya).</span><span class="sxs-lookup"><span data-stu-id="91ae4-141">You can find charts on hello **storage account blade** and in hello **Metrics** blade for an individual service (blob, queue, table, file).</span></span>

   <span data-ttu-id="91ae4-142">Bu örnekte, biz hello üzerinde görünür grafiği aşağıdaki hello çalışmak **depolama hesabı dikey**:</span><span class="sxs-lookup"><span data-stu-id="91ae4-142">In this example, we work with hello following chart that appears on hello **storage account blade**:</span></span>

   ![Azure portalında grafiği seçimi](./media/storage-monitor-storage-account/stg-customize-chart-00.png)

1. <span data-ttu-id="91ae4-144">Ardından, hello grafik tooopen hello içinde herhangi bir yere tıklayın **ölçüm** dikey.</span><span class="sxs-lookup"><span data-stu-id="91ae4-144">Next, click anywhere within hello chart tooopen hello **Metric** blade.</span></span> <span data-ttu-id="91ae4-145">Seçin **grafiği Düzenle** tooopen hello **grafiği Düzenle** dikey.</span><span class="sxs-lookup"><span data-stu-id="91ae4-145">Select **Edit chart** tooopen hello **Edit Chart** blade.</span></span>

   ![Grafik düğmesini grafik dikey Düzenle](./media/storage-monitor-storage-account/stg-customize-chart-01.png)

1. <span data-ttu-id="91ae4-147">Merhaba üzerinde **grafiği Düzenle** dikey penceresinde, select hello **zaman aralığı** hello ölçümleri toodisplay hello grafik ve Merhaba, **hizmet** (blob, kuyruk, tablo, dosya) istediğinizden, ölçümleri toodisplay.</span><span class="sxs-lookup"><span data-stu-id="91ae4-147">On hello **Edit Chart** blade, select hello **Time Range** of hello metrics toodisplay in hello chart, and hello **service** (blob, queue, table, file) whose metrics you wish toodisplay.</span></span> <span data-ttu-id="91ae4-148">Burada size toodisplay hello Geçen haftaki ölçümleri hello blob hizmeti için seçtiğiniz:</span><span class="sxs-lookup"><span data-stu-id="91ae4-148">Here we've selected toodisplay hello past week's metrics for hello blob service:</span></span>

   ![Merhaba grafiği Düzenle dikey penceresinde zaman aralığı ve hizmet seçimi](./media/storage-monitor-storage-account/stg-customize-chart-02.png)

1. <span data-ttu-id="91ae4-150">Select hello tek **ölçümleri** gibi hello grafikte görüntülenen, ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="91ae4-150">Select hello individual **metrics** you'd like displayed in hello chart, then click **OK**.</span></span> <span data-ttu-id="91ae4-151">Örneğin, burada size toodisplay hello seçmiş olduğunuz *ContainerCount* ve *ObjectCount* ölçümleri:</span><span class="sxs-lookup"><span data-stu-id="91ae4-151">For example, here we've chosen toodisplay hello *ContainerCount* and *ObjectCount* metrics:</span></span>

   ![Grafiği Düzenle dikey tek tek ölçüm seçim](./media/storage-monitor-storage-account/stg-customize-chart-03.png)

<span data-ttu-id="91ae4-153">Grafik ayarlarınızı değil hello koleksiyon, toplama veya izleme verilerinin hello depolama hesabındaki depolama etkiler, yalnızca ölçüm verilerinin görüntülenmesi hello.</span><span class="sxs-lookup"><span data-stu-id="91ae4-153">Your chart settings do not affect hello collection, aggregation, or storage of monitoring data in hello storage account, only hello viewing of metrics data.</span></span>

### <a name="metrics-availability-in-charts"></a><span data-ttu-id="91ae4-154">Ölçümleri kullanılabilirlik grafiklerinde</span><span class="sxs-lookup"><span data-stu-id="91ae4-154">Metrics availability in charts</span></span>

<span data-ttu-id="91ae4-155">hangi hizmette hello açılan seçtiğiniz kullanılabilir ölçümler değişiklik Hello listesini temel ve düzenlediğiniz hello grafik hello birim türü.</span><span class="sxs-lookup"><span data-stu-id="91ae4-155">hello list of available metrics changes based on which service you've chosen in hello drop-down, and hello unit type of hello chart you're editing.</span></span> <span data-ttu-id="91ae4-156">Örneğin, yüzde ölçümleri gibi seçebilirsiniz *PercentNetworkError* ve *PercentThrottlingError* yalnızca birimleri yüzde olarak gösteren bir grafik düzenliyorsanız:</span><span class="sxs-lookup"><span data-stu-id="91ae4-156">For example, you can select percentage metrics like *PercentNetworkError* and *PercentThrottlingError* only if you're editing a chart that displays units in percentage:</span></span>

![İstek hata yüzdesi grafik hello Azure portalı](./media/storage-monitor-storage-account/stg-customize-chart-04.png)

### <a name="metrics-resolution"></a><span data-ttu-id="91ae4-158">Ölçümleri çözümleme</span><span class="sxs-lookup"><span data-stu-id="91ae4-158">Metrics resolution</span></span>

<span data-ttu-id="91ae4-159">Merhaba ölçümleri tanılamada seçili hesabınız için kullanılabilir olan hello ölçümleri hello çözünürlüğünü belirler:</span><span class="sxs-lookup"><span data-stu-id="91ae4-159">hello metrics you selected in Diagnostics determines hello resolution of hello metrics that are available for your account:</span></span>

* <span data-ttu-id="91ae4-160">**Birleşik** izleme giriş/çıkış, kullanılabilirlik, gecikme ve başarı yüzdeleri gibi ölçümleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="91ae4-160">**Aggregate** monitoring provides metrics such as ingress/egress, availability, latency, and success percentages.</span></span> <span data-ttu-id="91ae4-161">Bu ölçümler hello blob, tablo, dosya ve kuyruk Hizmetleri toplanır.</span><span class="sxs-lookup"><span data-stu-id="91ae4-161">These metrics are aggregated from hello blob, table, file, and queue services.</span></span>
* <span data-ttu-id="91ae4-162">**API başına** yüksekse çözümleme tek depolama işlemleri için kullanılabilir ölçümleri ayrıca toohello hizmet düzeyi toplamalar sağlar.</span><span class="sxs-lookup"><span data-stu-id="91ae4-162">**Per API** provides finer resolution, with metrics available for individual storage operations, in addition toohello service-level aggregates.</span></span>

## <a name="configure-metrics-alerts"></a><span data-ttu-id="91ae4-163">Ölçümleri uyarılarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="91ae4-163">Configure metrics alerts</span></span>

<span data-ttu-id="91ae4-164">Uyarıları toonotify oluşturmak için depolama kaynak ölçümleri eşiklerine olduğunda.</span><span class="sxs-lookup"><span data-stu-id="91ae4-164">You can create alerts toonotify you when thresholds have been reached for storage resource metrics.</span></span>

1. <span data-ttu-id="91ae4-165">tooopen hello **uyarı kuralları dikey**, toohello aşağı **izleme** hello bölümünü **menü dikey** seçip **uyarı kuralları**.</span><span class="sxs-lookup"><span data-stu-id="91ae4-165">tooopen hello **Alert rules blade**, scroll down toohello **MONITORING** section of hello **Menu blade** and select **Alert rules**.</span></span>
1. <span data-ttu-id="91ae4-166">Seçin **uyarı Ekle** tooopen hello **uyarı kuralı eklemek** dikey penceresi</span><span class="sxs-lookup"><span data-stu-id="91ae4-166">Select **Add alert** tooopen hello **Add an alert rule** blade</span></span>
1. <span data-ttu-id="91ae4-167">Seçin bir **kaynak** (blob, dosya, kuyruk, tablo) açılan hello ve girin bir **adı** ve **açıklama** , yeni bir uyarı kuralı.</span><span class="sxs-lookup"><span data-stu-id="91ae4-167">Select a **Resource** (blob, file, queue, table) from hello drop-down, and enter a **Name** and **Description** for your new alert rule.</span></span>
1. <span data-ttu-id="91ae4-168">Select hello **ölçüm** tooadd bir uyarı bir uyarı için istediğinizi **koşulu**ve bir **eşik**.</span><span class="sxs-lookup"><span data-stu-id="91ae4-168">Select hello **Metric** for which you'd like tooadd an alert, an alert **Condition**, and a **Threshold**.</span></span> <span data-ttu-id="91ae4-169">Merhaba eşik birim türü değişiklikleri hello ölçüm bağlı olarak seçtiğiniz.</span><span class="sxs-lookup"><span data-stu-id="91ae4-169">hello threshold unit type changes depending on hello metric you've chosen.</span></span> <span data-ttu-id="91ae4-170">Örneğin, "count" Merhaba birim için türüdür *ContainerCount*, hello birimi hello için sırasında *PercentNetworkError* ölçümüdür yüzdesi.</span><span class="sxs-lookup"><span data-stu-id="91ae4-170">For example, "count" is hello unit type for *ContainerCount*, while hello unit for hello *PercentNetworkError* metric is a percentage.</span></span>
1. <span data-ttu-id="91ae4-171">Select hello **süresi**.</span><span class="sxs-lookup"><span data-stu-id="91ae4-171">Select hello **Period**.</span></span> <span data-ttu-id="91ae4-172">Ulaşmak veya aşan ölçümleri eşik hello dönem içinde bir uyarıyı tetikleyecek hello.</span><span class="sxs-lookup"><span data-stu-id="91ae4-172">Metrics that reach or exceed hello Threshold within hello period trigger an alert.</span></span>
1. <span data-ttu-id="91ae4-173">(İsteğe bağlı) Yapılandırma **e-posta** ve **Web kancası** bildirimleri.</span><span class="sxs-lookup"><span data-stu-id="91ae4-173">(Optional) Configure **Email** and **Webhook** notifications.</span></span> <span data-ttu-id="91ae4-174">Web kancası hakkında daha fazla bilgi için bkz: [bir Web kancası Azure ölçüm uyarıyı yapılandırmak](../../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="91ae4-174">For more information on webhooks, see [Configure a webhook on an Azure metric alert](../../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span> <span data-ttu-id="91ae4-175">E-posta veya Web kancası bildirimleri yapılandırmazsanız, uyarıları yalnızca hello Azure portalında görünür.</span><span class="sxs-lookup"><span data-stu-id="91ae4-175">If you do not configure email or webhook notifications, alerts will appear only in hello Azure portal.</span></span>

!['Bir uyarı kuralı Ekle' dikey penceresinde hello Azure portalı](./media/storage-monitor-storage-account/stg-alert-rules-01.png)

## <a name="add-metrics-charts-toohello-portal-dashboard"></a><span data-ttu-id="91ae4-177">Ölçümler grafiklerde toohello portal Pano Ekle</span><span class="sxs-lookup"><span data-stu-id="91ae4-177">Add metrics charts toohello portal dashboard</span></span>

<span data-ttu-id="91ae4-178">Herhangi bir depolama hesapları tooyour portalı panonuza için Azure Storage ölçümleri grafikleri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91ae4-178">You can add Azure Storage metrics charts for any of your storage accounts tooyour portal dashboard.</span></span>

1. <span data-ttu-id="91ae4-179">Select tıklatın **düzenleme Pano** hello panonuz görüntülerken [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="91ae4-179">Select click **Edit dashboard** while viewing your dashboard in hello [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="91ae4-180">Merhaba, **döşeme galeri**seçin **Bul bölmeleri tarafından** > **türü**.</span><span class="sxs-lookup"><span data-stu-id="91ae4-180">In hello **Tile Gallery**, select **Find tiles by** > **Type**.</span></span>
1. <span data-ttu-id="91ae4-181">Seçin **türü** > **depolama hesapları**.</span><span class="sxs-lookup"><span data-stu-id="91ae4-181">Select **Type** > **Storage accounts**.</span></span>
1. <span data-ttu-id="91ae4-182">İçinde **kaynakları**, ölçümleri tooadd toohello Pano istediğiniz hello depolama hesabını seçin.</span><span class="sxs-lookup"><span data-stu-id="91ae4-182">In **Resources**, select hello storage account whose metrics you wish tooadd toohello dashboard.</span></span>
1. <span data-ttu-id="91ae4-183">Seçin **kategorileri** > **izleme**.</span><span class="sxs-lookup"><span data-stu-id="91ae4-183">Select **Categories** > **Monitoring**.</span></span>
1. <span data-ttu-id="91ae4-184">Sürükle ve bırak hello grafik döşeme panonuz görüntülenmesini istediğiniz hello ölçümü için üzerine.</span><span class="sxs-lookup"><span data-stu-id="91ae4-184">Drag-and-drop hello chart tile onto your dashboard for hello metric you'd like displayed.</span></span> <span data-ttu-id="91ae4-185">Merhaba panosunda görüntülenen tüm ölçümleri istediğiniz için yineleyin.</span><span class="sxs-lookup"><span data-stu-id="91ae4-185">Repeat for all metrics you'd like displayed on hello dashboard.</span></span> <span data-ttu-id="91ae4-186">Merhaba, görüntü aşağıdaki hello "BLOB'lar - toplam istek" grafik örnek olarak vurgulanır, ancak tüm hello grafikler panonuz yerleştirme için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="91ae4-186">In hello following image, hello "Blobs - Total requests" chart is highlighted as an example, but all hello charts are available for placement on your dashboard.</span></span>

   ![Azure portalında döşeme Galerisi](./media/storage-monitor-storage-account/stg-customize-dashboard-01.png)
1. <span data-ttu-id="91ae4-188">Seçin **özelleştirme Bitti** ekleme grafikleri bittiğinde hello panonun hello üstüne yakın.</span><span class="sxs-lookup"><span data-stu-id="91ae4-188">Select **Done customizing** near hello top of hello dashboard when you're done adding charts.</span></span>

<span data-ttu-id="91ae4-189">Grafikler tooyour Pano ekledikten sonra daha fazla bunları açıklandığı gibi özelleştirebilirsiniz [ölçümler grafiklerde özelleştirme](#how-to-customize-metrics-charts).</span><span class="sxs-lookup"><span data-stu-id="91ae4-189">Once you've added charts tooyour dashboard, you can further customize them as described in [Customize metrics charts](#how-to-customize-metrics-charts).</span></span>

## <a name="configure-logging"></a><span data-ttu-id="91ae4-190">Günlük tutmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="91ae4-190">Configure logging</span></span>

<span data-ttu-id="91ae4-191">Azure Storage toosave tanılama günlükleri için okuma, yazma ve silme istekleri hello blob, tablo ve kuyruk Hizmetleri için söyleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91ae4-191">You can instruct Azure Storage toosave diagnostics logs for read, write, and delete requests for hello blob, table, and queue services.</span></span> <span data-ttu-id="91ae4-192">ayarladığınız hello veri bekletme ilkesi toothese günlükleri de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="91ae4-192">hello data retention policy you set also applies toothese logs.</span></span>

> [!NOTE]
> <span data-ttu-id="91ae4-193">Azure File storage şu anda Storage Analytics ölçümleri destekliyor, ancak henüz günlük kaydını desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="91ae4-193">Azure File storage currently supports Storage Analytics metrics, but does not yet support logging.</span></span>
>

1. <span data-ttu-id="91ae4-194">Merhaba, [Azure portal](https://portal.azure.com)seçin **depolama hesapları**, sonra hello depolama hesabı tooopen hello depolama hesabı dikey penceresinde hello adı.</span><span class="sxs-lookup"><span data-stu-id="91ae4-194">In hello [Azure portal](https://portal.azure.com), select **Storage accounts**, then hello name of hello storage account tooopen hello storage account blade.</span></span>
1. <span data-ttu-id="91ae4-195">Seçin **tanılama** hello içinde **izleme** hello menü dikey bölümü.</span><span class="sxs-lookup"><span data-stu-id="91ae4-195">Select **Diagnostics** in hello **MONITORING** section of hello menu blade.</span></span>

    ![Hello Azure portal'ın tanılama menü öğesi izleme altında.](./media/storage-monitor-storage-account/stg-enable-metrics-00.png)
    
1. <span data-ttu-id="91ae4-197">Olun **durum** çok ayarlanır**üzerinde**ve select hello **Hizmetleri** tooenable günlüğe kaydetme için istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="91ae4-197">Ensure **Status** is set too**On**, and select hello **services** for which you'd like tooenable logging.</span></span>

    ![Hello Azure portalında oturum açmayı Yapılandır.](./media/storage-monitor-storage-account/stg-enable-logging-01.png)
1. <span data-ttu-id="91ae4-199">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="91ae4-199">Click **Save**.</span></span>

<span data-ttu-id="91ae4-200">Merhaba tanılama günlükleri, depolama hesabınızdaki $logs adlı blob kapsayıcısında kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="91ae4-200">hello diagnostics logs are saved in a blob container named $logs in your storage account.</span></span> <span data-ttu-id="91ae4-201">Hello gibi bir Depolama Gezgini kullanarak hello günlük verilerini görüntüleyebilir [Microsoft Storage Gezgini](http://storageexplorer.com), veya program aracılığıyla hello depolama istemci kitaplığı veya PowerShell kullanarak.</span><span class="sxs-lookup"><span data-stu-id="91ae4-201">You can view hello log data using a storage explorer like hello [Microsoft Storage Explorer](http://storageexplorer.com), or programmatically using hello storage client library or PowerShell.</span></span>

<span data-ttu-id="91ae4-202">Merhaba $logs kapsayıcı erişme hakkında daha fazla bilgi için bkz: [depolama günlüğünü etkinleştirme ve erişim günlüğü verilerini](/rest/api/storageservices/enabling-storage-logging-and-accessing-log-data).</span><span class="sxs-lookup"><span data-stu-id="91ae4-202">For information about accessing hello $logs container, see [Enabling Storage Logging and Accessing Log Data](/rest/api/storageservices/enabling-storage-logging-and-accessing-log-data).</span></span>

## <a name="next-steps"></a><span data-ttu-id="91ae4-203">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="91ae4-203">Next steps</span></span>

* <span data-ttu-id="91ae4-204">İlgili diğer ayrıntıları bulmak [günlüğe kaydetme ve faturalama ölçümleri](../storage-analytics.md) depolama çözümlemeleri için.</span><span class="sxs-lookup"><span data-stu-id="91ae4-204">Find more details about [metrics, logging, and billing](../storage-analytics.md) for Storage Analytics.</span></span>
* <span data-ttu-id="91ae4-205">[Azure Storage ölçümleri ve görünüm ölçüm verilerini etkinleştirme](../storage-enable-and-view-metrics.md) PowerShell kullanarak ve C# ile programlı olarak.</span><span class="sxs-lookup"><span data-stu-id="91ae4-205">[Enable Azure Storage metrics and view metrics data](../storage-enable-and-view-metrics.md) by using PowerShell and programmatically with C#.</span></span>
