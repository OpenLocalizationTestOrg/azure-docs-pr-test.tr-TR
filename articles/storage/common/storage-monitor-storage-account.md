---
title: "Bir Azure depolama hesabı izleme | Microsoft Docs"
description: "Azure portalı kullanarak bir Azure depolama hesabında izlemek öğrenin."
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
ms.openlocfilehash: e8fbc4ecdffe62806019f494e1412cfedbccf71f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="monitor-a-storage-account-in-the-azure-portal"></a><span data-ttu-id="f9a39-103">Azure portalında bir depolama hesabını izleme</span><span class="sxs-lookup"><span data-stu-id="f9a39-103">Monitor a storage account in the Azure portal</span></span>

<span data-ttu-id="f9a39-104">[Azure Storage Analytics](../storage-analytics.md) tabloları ve tüm depolama hizmetleri ve günlükleri BLOB, kuyruklar, ölçümleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="f9a39-104">[Azure Storage Analytics](../storage-analytics.md) provides metrics for all storage services, and logs for blobs, queues, and tables.</span></span> <span data-ttu-id="f9a39-105">Kullanabileceğiniz [Azure portal](https://portal.azure.com) hesabınız için kaydedilen hangi ölçümleri ve günlükleri yapılandırmak ve ölçümleri verilerinizi görsel gösterimi sağlamak grafikleri yapılandırmak için.</span><span class="sxs-lookup"><span data-stu-id="f9a39-105">You can use the [Azure portal](https://portal.azure.com) to configure which metrics and logs are recorded for your account, and configure charts that provide visual representations of your metrics data.</span></span>

> [!NOTE]
> <span data-ttu-id="f9a39-106">Azure portalında izleme verileri inceleniyor ile ilişkili maliyetleri vardır.</span><span class="sxs-lookup"><span data-stu-id="f9a39-106">There are costs associated with examining monitoring data in the Azure portal.</span></span> <span data-ttu-id="f9a39-107">Daha fazla bilgi için bkz: [depolama çözümlemeleri ve faturalama](/rest/api/storageservices/Storage-Analytics-and-Billing).</span><span class="sxs-lookup"><span data-stu-id="f9a39-107">For more information, see [Storage Analytics and Billing](/rest/api/storageservices/Storage-Analytics-and-Billing).</span></span>
>
> <span data-ttu-id="f9a39-108">Azure File storage şu anda Storage Analytics ölçümleri destekliyor, ancak henüz günlük kaydını desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="f9a39-108">Azure File storage currently supports Storage Analytics metrics, but does not yet support logging.</span></span>
>
> <span data-ttu-id="f9a39-109">Bir çoğaltma türü, bölge olarak yedekli depolama (ZRS) şu anda depolama hesaplarıyla ölçümleri veya etkin bir günlüğe kaydetme özelliğine sahip değilsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9a39-109">Storage accounts with a replication type of Zone-Redundant Storage (ZRS) currently do not have the metrics or logging capability enabled.</span></span>
> 
> <span data-ttu-id="f9a39-110">Ayrıntılı bir kılavuz tanımlamak, tanılama ve Azure Storage ile ilgili sorunları gidermek için depolama çözümlemeleri ve diğer araçları kullanma hakkında bilgi için bkz: [izleme, tanılama ve Microsoft Azure Storage sorun giderme](../storage-monitoring-diagnosing-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="f9a39-110">For an in-depth guide on using Storage Analytics and other tools to identify, diagnose, and troubleshoot Azure Storage-related issues, see [Monitor, diagnose, and troubleshoot Microsoft Azure Storage](../storage-monitoring-diagnosing-troubleshooting.md).</span></span>
>

## <a name="configure-monitoring-for-a-storage-account"></a><span data-ttu-id="f9a39-111">Bir depolama hesabı için izlemeyi Yapılandır</span><span class="sxs-lookup"><span data-stu-id="f9a39-111">Configure monitoring for a storage account</span></span>

1. <span data-ttu-id="f9a39-112">İçinde [Azure portal](https://portal.azure.com)seçin **depolama hesapları**, hesap panosunu açmak için sonra depolama hesabı adı.</span><span class="sxs-lookup"><span data-stu-id="f9a39-112">In the [Azure portal](https://portal.azure.com), select **Storage accounts**, then the storage account name to open the account dashboard.</span></span>
1. <span data-ttu-id="f9a39-113">Seçin **tanılama** içinde **izleme** menü dikey bölüm.</span><span class="sxs-lookup"><span data-stu-id="f9a39-113">Select **Diagnostics** in the **MONITORING** section of the menu blade.</span></span>

    ![MonitoringOptions](./media/storage-monitor-storage-account/stg-enable-metrics-00.png)

1. <span data-ttu-id="f9a39-115">Seçin **türü** her ölçümleri verilerin **hizmet** , izlemek istediğiniz ve **Bekletme İlkesi** veriler için.</span><span class="sxs-lookup"><span data-stu-id="f9a39-115">Select the **type** of metrics data for each **service** you wish to monitor, and the **retention policy** for the data.</span></span> <span data-ttu-id="f9a39-116">Ayrıca ayarlayarak izleme devre dışı bırakabilirsiniz **durum** için **devre dışı**.</span><span class="sxs-lookup"><span data-stu-id="f9a39-116">You can also disable monitoring by setting **Status** to **Off**.</span></span>

    ![MonitoringOptions](./media/storage-monitor-storage-account/stg-enable-metrics-01.png)

   <span data-ttu-id="f9a39-118">Her hizmet için etkinleştirebilirsiniz ölçümleri her ikisi de yeni depolama hesapları için varsayılan olarak etkinleştirilen iki tür vardır:</span><span class="sxs-lookup"><span data-stu-id="f9a39-118">There are two types of metrics you can enable for each service, both of which are enabled by default for new storage accounts:</span></span>

   * <span data-ttu-id="f9a39-119">**Birleşik**: giriş/çıkış, kullanılabilirlik, gecikme ve başarı yüzdeleri gibi ölçümleri toplar.</span><span class="sxs-lookup"><span data-stu-id="f9a39-119">**Aggregate**: Collects metrics such as ingress/egress, availability, latency, and success percentages.</span></span> <span data-ttu-id="f9a39-120">Bu ölçümler blob, kuyruk, tablo ve Dosya Hizmetleri için toplanır.</span><span class="sxs-lookup"><span data-stu-id="f9a39-120">These metrics are aggregated for the blob, queue, table, and file services.</span></span>
   * <span data-ttu-id="f9a39-121">**API başına**: Birleşik ölçümlerin yanı sıra, Azure depolama hizmeti API'si her depolama işlem ölçümlerini aynı kümesini toplar.</span><span class="sxs-lookup"><span data-stu-id="f9a39-121">**Per API**: In addition to the aggregate metrics, collects the same set of metrics for each storage operation in the Azure Storage service API.</span></span>

   <span data-ttu-id="f9a39-122">Veri Bekletme İlkesi ayarlamak üzere taşıma **bekletme (gün)** kaydırıcı veya 1 ile 365 arasında korumak için veri gün sayısı girin.</span><span class="sxs-lookup"><span data-stu-id="f9a39-122">To set the data retention policy, move the **Retention (days)** slider or enter the number of days of data to retain, from 1 to 365.</span></span> <span data-ttu-id="f9a39-123">Yeni depolama hesapları için varsayılan yedi gündür.</span><span class="sxs-lookup"><span data-stu-id="f9a39-123">The default for new storage accounts is seven days.</span></span> <span data-ttu-id="f9a39-124">Bir bekletme ilkesi ayarlamak istemiyorsanız sıfır girin.</span><span class="sxs-lookup"><span data-stu-id="f9a39-124">If you do not want to set a retention policy, enter zero.</span></span> <span data-ttu-id="f9a39-125">Bekletme İlkesi yok ise, izleme verilerini silmek için size bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="f9a39-125">If there is no retention policy, it is up to you to delete the monitoring data.</span></span>

   > [!WARNING]
   > <span data-ttu-id="f9a39-126">Ölçüm verilerini el ile sildiğinizde ücretlendirilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9a39-126">You are charged when you manually delete metrics data.</span></span> <span data-ttu-id="f9a39-127">Eski analiz verileri (veri bekletme ilkeniz eski) herhangi bir ücret ödemeden sistem tarafından silinir.</span><span class="sxs-lookup"><span data-stu-id="f9a39-127">Stale analytics data (data older than your retention policy) is deleted by the system at no cost.</span></span> <span data-ttu-id="f9a39-128">Ne kadar süreyle, depolama hesabınız için analiz verileri korumak istediğinize bağlı bir bekletme ilkesi ayarı öneririz.</span><span class="sxs-lookup"><span data-stu-id="f9a39-128">We recommend setting a retention policy based on how long you want to retain storage analytics data for your account.</span></span> <span data-ttu-id="f9a39-129">Bkz: [ne yapmak tabi storage ölçümleri etkinleştirdiğinizde ücretlendirilen?](../common/storage-enable-and-view-metrics.md#what-charges-do-you-incur-when-you-enable-storage-metrics) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="f9a39-129">See [What charges do you incur when you enable storage metrics?](../common/storage-enable-and-view-metrics.md#what-charges-do-you-incur-when-you-enable-storage-metrics) for more information.</span></span>
   >

1. <span data-ttu-id="f9a39-130">İzleme yapılandırmasını tamamladığınızda, seçin **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="f9a39-130">When you finish the monitoring configuration, select **Save**.</span></span>

<span data-ttu-id="f9a39-131">Ölçümleri varsayılan bir bireysel hizmet Kanatlar (blob, kuyruk, tablo ve dosya) yanı sıra depolama hesabı dikey grafiklerinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="f9a39-131">A default set of metrics is displayed in charts on the storage account blade, as well as the individual service blades (blob, queue, table, and file).</span></span> <span data-ttu-id="f9a39-132">Bir hizmet için ölçümleri etkinleştirdikten sonra kendi grafikte görüntülenecek veri bir saate kadar sürebilir.</span><span class="sxs-lookup"><span data-stu-id="f9a39-132">Once you've enabled metrics for a service, it may take up to an hour for data to appear in its charts.</span></span> <span data-ttu-id="f9a39-133">Seçebileceğiniz **Düzenle** ölçüm herhangi grafik [hangi ölçümlerini yapılandırın](#how-to-customize-metrics-charts) grafikte görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="f9a39-133">You can select **Edit** on any metric chart to [configure which metrics](#how-to-customize-metrics-charts) are displayed in the chart.</span></span>

<span data-ttu-id="f9a39-134">Ölçümleri toplama ve günlüğe kaydetme ayarlayarak devre dışı bırakabilirsiniz **durum** için **devre dışı**.</span><span class="sxs-lookup"><span data-stu-id="f9a39-134">You can disable metrics collection and logging by setting **Status** to **Off**.</span></span>

> [!NOTE]
> <span data-ttu-id="f9a39-135">Azure depolama kullanan [tablo depolama](../common/storage-introduction.md#table-storage) hesabınızda tablolardaki depolama hesabı ve depoları ölçümler için ölçümler depolamak için.</span><span class="sxs-lookup"><span data-stu-id="f9a39-135">Azure Storage uses [table storage](../common/storage-introduction.md#table-storage) to store the metrics for your storage account, and stores the metrics in tables in your account.</span></span> <span data-ttu-id="f9a39-136">Daha fazla bilgi için bkz.</span><span class="sxs-lookup"><span data-stu-id="f9a39-136">For more information, see.</span></span> <span data-ttu-id="f9a39-137">[Ölçümleri nasıl depolandığını](../common/storage-analytics.md#how-metrics-are-stored).</span><span class="sxs-lookup"><span data-stu-id="f9a39-137">[How metrics are stored](../common/storage-analytics.md#how-metrics-are-stored).</span></span>
>

## <a name="customize-metrics-charts"></a><span data-ttu-id="f9a39-138">Ölçümler grafiklerde özelleştirme</span><span class="sxs-lookup"><span data-stu-id="f9a39-138">Customize metrics charts</span></span>

<span data-ttu-id="f9a39-139">Ölçümleri grafik görüntülemek için hangi depolama ölçümleri seçmek için aşağıdaki yordamı kullanın.</span><span class="sxs-lookup"><span data-stu-id="f9a39-139">Use the following procedure to choose which storage metrics to view in a metrics chart.</span></span> 

1. <span data-ttu-id="f9a39-140">Azure portalında bir depolama ölçüm grafik görüntüleyerek başlatın.</span><span class="sxs-lookup"><span data-stu-id="f9a39-140">Start by displaying a storage metric chart in the Azure portal.</span></span> <span data-ttu-id="f9a39-141">Grafikler bulabilirsiniz **depolama hesabı dikey** ve **ölçümleri** dikey bir bireysel hizmet (blob, kuyruk, tablo, dosya).</span><span class="sxs-lookup"><span data-stu-id="f9a39-141">You can find charts on the **storage account blade** and in the **Metrics** blade for an individual service (blob, queue, table, file).</span></span>

   <span data-ttu-id="f9a39-142">Bu örnekte, biz kasasındaki aşağıdaki grafikte çalışmak **depolama hesabı dikey**:</span><span class="sxs-lookup"><span data-stu-id="f9a39-142">In this example, we work with the following chart that appears on the **storage account blade**:</span></span>

   ![Azure portalında grafiği seçimi](./media/storage-monitor-storage-account/stg-customize-chart-00.png)

1. <span data-ttu-id="f9a39-144">Ardından, açmak için grafik içinde herhangi bir yere tıklayın **ölçüm** dikey.</span><span class="sxs-lookup"><span data-stu-id="f9a39-144">Next, click anywhere within the chart to open the **Metric** blade.</span></span> <span data-ttu-id="f9a39-145">Seçin **grafiği Düzenle** açmak için **grafiği Düzenle** dikey.</span><span class="sxs-lookup"><span data-stu-id="f9a39-145">Select **Edit chart** to open the **Edit Chart** blade.</span></span>

   ![Grafik düğmesini grafik dikey Düzenle](./media/storage-monitor-storage-account/stg-customize-chart-01.png)

1. <span data-ttu-id="f9a39-147">Üzerinde **grafiği Düzenle** dikey penceresinde, select **zaman aralığı** grafikte görüntülenecek ölçümleri ve **hizmet** (blob, kuyruk, tablo, dosya) görüntülemek istediğiniz, ölçümleri.</span><span class="sxs-lookup"><span data-stu-id="f9a39-147">On the **Edit Chart** blade, select the **Time Range** of the metrics to display in the chart, and the **service** (blob, queue, table, file) whose metrics you wish to display.</span></span> <span data-ttu-id="f9a39-148">Burada size blob hizmeti için geçen hafta ölçümlerini görüntülemek için seçtiğiniz:</span><span class="sxs-lookup"><span data-stu-id="f9a39-148">Here we've selected to display the past week's metrics for the blob service:</span></span>

   ![Grafiği Düzenle dikey penceresinde zaman aralığı ve hizmet seçimi](./media/storage-monitor-storage-account/stg-customize-chart-02.png)

1. <span data-ttu-id="f9a39-150">Tek tek seçin **ölçümleri** gibi grafikte görüntülenen, ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="f9a39-150">Select the individual **metrics** you'd like displayed in the chart, then click **OK**.</span></span> <span data-ttu-id="f9a39-151">Örneğin, burada biz görüntülemek seçtiğiniz *ContainerCount* ve *ObjectCount* ölçümleri:</span><span class="sxs-lookup"><span data-stu-id="f9a39-151">For example, here we've chosen to display the *ContainerCount* and *ObjectCount* metrics:</span></span>

   ![Grafiği Düzenle dikey tek tek ölçüm seçim](./media/storage-monitor-storage-account/stg-customize-chart-03.png)

<span data-ttu-id="f9a39-153">Koleksiyon, toplama veya izleme verilerinin yalnızca ölçüm verilerinin görüntülenmesi depolama hesabındaki depolama grafik ayarlarınızı etkilemez.</span><span class="sxs-lookup"><span data-stu-id="f9a39-153">Your chart settings do not affect the collection, aggregation, or storage of monitoring data in the storage account, only the viewing of metrics data.</span></span>

### <a name="metrics-availability-in-charts"></a><span data-ttu-id="f9a39-154">Ölçümleri kullanılabilirlik grafiklerinde</span><span class="sxs-lookup"><span data-stu-id="f9a39-154">Metrics availability in charts</span></span>

<span data-ttu-id="f9a39-155">Düzenlediğiniz açılır ve grafiğin birim türünü seçtiğiniz hangi hizmet üzerinde temel ölçümler değişiklikleri listesi.</span><span class="sxs-lookup"><span data-stu-id="f9a39-155">The list of available metrics changes based on which service you've chosen in the drop-down, and the unit type of the chart you're editing.</span></span> <span data-ttu-id="f9a39-156">Örneğin, yüzde ölçümleri gibi seçebilirsiniz *PercentNetworkError* ve *PercentThrottlingError* yalnızca birimleri yüzde olarak gösteren bir grafik düzenliyorsanız:</span><span class="sxs-lookup"><span data-stu-id="f9a39-156">For example, you can select percentage metrics like *PercentNetworkError* and *PercentThrottlingError* only if you're editing a chart that displays units in percentage:</span></span>

![İstek hata yüzdesi grafik Azure portalında](./media/storage-monitor-storage-account/stg-customize-chart-04.png)

### <a name="metrics-resolution"></a><span data-ttu-id="f9a39-158">Ölçümleri çözümleme</span><span class="sxs-lookup"><span data-stu-id="f9a39-158">Metrics resolution</span></span>

<span data-ttu-id="f9a39-159">Tanılama'seçilen ölçümleri hesabınız için kullanılabilir ölçümleri çözünürlüğünü belirler:</span><span class="sxs-lookup"><span data-stu-id="f9a39-159">The metrics you selected in Diagnostics determines the resolution of the metrics that are available for your account:</span></span>

* <span data-ttu-id="f9a39-160">**Birleşik** izleme giriş/çıkış, kullanılabilirlik, gecikme ve başarı yüzdeleri gibi ölçümleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="f9a39-160">**Aggregate** monitoring provides metrics such as ingress/egress, availability, latency, and success percentages.</span></span> <span data-ttu-id="f9a39-161">Bu ölçümler blob, tablo, dosya ve kuyruk Hizmetleri toplanır.</span><span class="sxs-lookup"><span data-stu-id="f9a39-161">These metrics are aggregated from the blob, table, file, and queue services.</span></span>
* <span data-ttu-id="f9a39-162">**API başına** yüksekse çözümleme tek depolama işlemleri için kullanılabilir ölçümleri Ayrıca hizmet düzeyi toplamalar sağlar.</span><span class="sxs-lookup"><span data-stu-id="f9a39-162">**Per API** provides finer resolution, with metrics available for individual storage operations, in addition to the service-level aggregates.</span></span>

## <a name="configure-metrics-alerts"></a><span data-ttu-id="f9a39-163">Ölçümleri uyarılarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f9a39-163">Configure metrics alerts</span></span>

<span data-ttu-id="f9a39-164">Depolama kaynak ölçümleri için eşiklerine olduğunda sizi bilgilendirmek üzere uyarılar oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9a39-164">You can create alerts to notify you when thresholds have been reached for storage resource metrics.</span></span>

1. <span data-ttu-id="f9a39-165">Açmak için **uyarı kuralları dikey**, aşağı kaydırarak **izleme** bölümünü **menü dikey** seçip **uyarı kuralları**.</span><span class="sxs-lookup"><span data-stu-id="f9a39-165">To open the **Alert rules blade**, scroll down to the **MONITORING** section of the **Menu blade** and select **Alert rules**.</span></span>
1. <span data-ttu-id="f9a39-166">Seçin **uyarı Ekle** açmak için **uyarı kuralı eklemek** dikey penceresi</span><span class="sxs-lookup"><span data-stu-id="f9a39-166">Select **Add alert** to open the **Add an alert rule** blade</span></span>
1. <span data-ttu-id="f9a39-167">Seçin bir **kaynak** (blob, dosya, kuyruk, tablo) açılan gelen ve girin bir **adı** ve **açıklama** , yeni bir uyarı kuralı.</span><span class="sxs-lookup"><span data-stu-id="f9a39-167">Select a **Resource** (blob, file, queue, table) from the drop-down, and enter a **Name** and **Description** for your new alert rule.</span></span>
1. <span data-ttu-id="f9a39-168">Seçin **ölçüm** , bir uyarı, bir uyarı eklemek istediğiniz için **koşulu**ve bir **eşik**.</span><span class="sxs-lookup"><span data-stu-id="f9a39-168">Select the **Metric** for which you'd like to add an alert, an alert **Condition**, and a **Threshold**.</span></span> <span data-ttu-id="f9a39-169">Eşik birim türü seçtiğiniz ölçüm bağlı olarak değiştirir.</span><span class="sxs-lookup"><span data-stu-id="f9a39-169">The threshold unit type changes depending on the metric you've chosen.</span></span> <span data-ttu-id="f9a39-170">Örneğin, "count" birim türü olduğundan *ContainerCount*, while birimini *PercentNetworkError* ölçümüdür yüzdesi.</span><span class="sxs-lookup"><span data-stu-id="f9a39-170">For example, "count" is the unit type for *ContainerCount*, while the unit for the *PercentNetworkError* metric is a percentage.</span></span>
1. <span data-ttu-id="f9a39-171">Seçin **süresi**.</span><span class="sxs-lookup"><span data-stu-id="f9a39-171">Select the **Period**.</span></span> <span data-ttu-id="f9a39-172">Ulaşmak ya da süresi içinde eşiğini aşan ölçümleri bir uyarı tetikler.</span><span class="sxs-lookup"><span data-stu-id="f9a39-172">Metrics that reach or exceed the Threshold within the period trigger an alert.</span></span>
1. <span data-ttu-id="f9a39-173">(İsteğe bağlı) Yapılandırma **e-posta** ve **Web kancası** bildirimleri.</span><span class="sxs-lookup"><span data-stu-id="f9a39-173">(Optional) Configure **Email** and **Webhook** notifications.</span></span> <span data-ttu-id="f9a39-174">Web kancası hakkında daha fazla bilgi için bkz: [bir Web kancası Azure ölçüm uyarıyı yapılandırmak](../../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="f9a39-174">For more information on webhooks, see [Configure a webhook on an Azure metric alert](../../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span> <span data-ttu-id="f9a39-175">E-posta veya Web kancası bildirimleri yapılandırmazsanız, uyarıları yalnızca Azure Portalı'nda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="f9a39-175">If you do not configure email or webhook notifications, alerts will appear only in the Azure portal.</span></span>

!['Bir uyarı kuralı Ekle' dikey Azure portalında](./media/storage-monitor-storage-account/stg-alert-rules-01.png)

## <a name="add-metrics-charts-to-the-portal-dashboard"></a><span data-ttu-id="f9a39-177">Portal panosuna ölçümleri grafikler ekleyin</span><span class="sxs-lookup"><span data-stu-id="f9a39-177">Add metrics charts to the portal dashboard</span></span>

<span data-ttu-id="f9a39-178">Portalı panonuza herhangi bir depolama hesaplarınızı için Azure Storage ölçümleri grafikleri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9a39-178">You can add Azure Storage metrics charts for any of your storage accounts to your portal dashboard.</span></span>

1. <span data-ttu-id="f9a39-179">Select tıklatın **düzenleme Pano** Panonuzda görüntülerken [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f9a39-179">Select click **Edit dashboard** while viewing your dashboard in the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="f9a39-180">İçinde **döşeme galeri**seçin **Bul bölmeleri tarafından** > **türü**.</span><span class="sxs-lookup"><span data-stu-id="f9a39-180">In the **Tile Gallery**, select **Find tiles by** > **Type**.</span></span>
1. <span data-ttu-id="f9a39-181">Seçin **türü** > **depolama hesapları**.</span><span class="sxs-lookup"><span data-stu-id="f9a39-181">Select **Type** > **Storage accounts**.</span></span>
1. <span data-ttu-id="f9a39-182">İçinde **kaynakları**, ölçümleri panoya eklemek istediğiniz depolama hesabını seçin.</span><span class="sxs-lookup"><span data-stu-id="f9a39-182">In **Resources**, select the storage account whose metrics you wish to add to the dashboard.</span></span>
1. <span data-ttu-id="f9a39-183">Seçin **kategorileri** > **izleme**.</span><span class="sxs-lookup"><span data-stu-id="f9a39-183">Select **Categories** > **Monitoring**.</span></span>
1. <span data-ttu-id="f9a39-184">Sürükle ve bırak grafik döşeme panonuz görüntülenmesini istediğiniz ölçümü için üzerine.</span><span class="sxs-lookup"><span data-stu-id="f9a39-184">Drag-and-drop the chart tile onto your dashboard for the metric you'd like displayed.</span></span> <span data-ttu-id="f9a39-185">Panoda görüntülenen tüm ölçümleri istediğiniz için yineleyin.</span><span class="sxs-lookup"><span data-stu-id="f9a39-185">Repeat for all metrics you'd like displayed on the dashboard.</span></span> <span data-ttu-id="f9a39-186">Aşağıdaki görüntüde, örnek olarak "BLOB'lar - toplam istek" grafik vurgulanmış, ancak tüm grafikler panonuz yerleştirme için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f9a39-186">In the following image, the "Blobs - Total requests" chart is highlighted as an example, but all the charts are available for placement on your dashboard.</span></span>

   ![Azure portalında döşeme Galerisi](./media/storage-monitor-storage-account/stg-customize-dashboard-01.png)
1. <span data-ttu-id="f9a39-188">Seçin **özelleştirme Bitti** üstüne yakın panonun ekleme grafikleri bittiğinde.</span><span class="sxs-lookup"><span data-stu-id="f9a39-188">Select **Done customizing** near the top of the dashboard when you're done adding charts.</span></span>

<span data-ttu-id="f9a39-189">Panonuza grafikleri ekledikten sonra daha fazla bunları açıklandığı gibi özelleştirebilirsiniz [ölçümler grafiklerde özelleştirme](#how-to-customize-metrics-charts).</span><span class="sxs-lookup"><span data-stu-id="f9a39-189">Once you've added charts to your dashboard, you can further customize them as described in [Customize metrics charts](#how-to-customize-metrics-charts).</span></span>

## <a name="configure-logging"></a><span data-ttu-id="f9a39-190">Günlük tutmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f9a39-190">Configure logging</span></span>

<span data-ttu-id="f9a39-191">Tanılama günlüklerini okuma kaydetmek yazma ve silme istekleri blob, tablo ve kuyruk Hizmetleri için Azure Storage söyleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9a39-191">You can instruct Azure Storage to save diagnostics logs for read, write, and delete requests for the blob, table, and queue services.</span></span> <span data-ttu-id="f9a39-192">Ayarladığınız veri bekletme ilkesi, bu günlükler için de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="f9a39-192">The data retention policy you set also applies to these logs.</span></span>

> [!NOTE]
> <span data-ttu-id="f9a39-193">Azure File storage şu anda Storage Analytics ölçümleri destekliyor, ancak henüz günlük kaydını desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="f9a39-193">Azure File storage currently supports Storage Analytics metrics, but does not yet support logging.</span></span>
>

1. <span data-ttu-id="f9a39-194">İçinde [Azure portal](https://portal.azure.com)seçin **depolama hesapları**, ardından depolama hesabı dikey penceresini açmak için depolama hesabının adı.</span><span class="sxs-lookup"><span data-stu-id="f9a39-194">In the [Azure portal](https://portal.azure.com), select **Storage accounts**, then the name of the storage account to open the storage account blade.</span></span>
1. <span data-ttu-id="f9a39-195">Seçin **tanılama** içinde **izleme** menü dikey bölüm.</span><span class="sxs-lookup"><span data-stu-id="f9a39-195">Select **Diagnostics** in the **MONITORING** section of the menu blade.</span></span>

    ![Azure portalında tanılama menü öğesi izleme altında.](./media/storage-monitor-storage-account/stg-enable-metrics-00.png)
    
1. <span data-ttu-id="f9a39-197">Sağlamak **durum** ayarlanır **üzerinde**seçip **Hizmetleri** , günlüğü etkinleştirmek istediğiniz için.</span><span class="sxs-lookup"><span data-stu-id="f9a39-197">Ensure **Status** is set to **On**, and select the **services** for which you'd like to enable logging.</span></span>

    ![Azure portalında oturum açmayı yapılandırın.](./media/storage-monitor-storage-account/stg-enable-logging-01.png)
1. <span data-ttu-id="f9a39-199">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f9a39-199">Click **Save**.</span></span>

<span data-ttu-id="f9a39-200">Tanılama günlüklerini $logs depolama hesabınızdaki adlı blob kapsayıcısında kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="f9a39-200">The diagnostics logs are saved in a blob container named $logs in your storage account.</span></span> <span data-ttu-id="f9a39-201">Bir Depolama Gezgini gibi kullanarak günlük verilerini görüntüleyebilir [Microsoft Storage Gezgini](http://storageexplorer.com), veya program aracılığıyla depolama istemci kitaplığı veya PowerShell kullanarak.</span><span class="sxs-lookup"><span data-stu-id="f9a39-201">You can view the log data using a storage explorer like the [Microsoft Storage Explorer](http://storageexplorer.com), or programmatically using the storage client library or PowerShell.</span></span>

<span data-ttu-id="f9a39-202">$Logs kapsayıcı erişme hakkında daha fazla bilgi için bkz: [depolama günlüğünü etkinleştirme ve erişim günlüğü verilerini](/rest/api/storageservices/enabling-storage-logging-and-accessing-log-data).</span><span class="sxs-lookup"><span data-stu-id="f9a39-202">For information about accessing the $logs container, see [Enabling Storage Logging and Accessing Log Data](/rest/api/storageservices/enabling-storage-logging-and-accessing-log-data).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f9a39-203">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f9a39-203">Next steps</span></span>

* <span data-ttu-id="f9a39-204">İlgili diğer ayrıntıları bulmak [günlüğe kaydetme ve faturalama ölçümleri](../storage-analytics.md) depolama çözümlemeleri için.</span><span class="sxs-lookup"><span data-stu-id="f9a39-204">Find more details about [metrics, logging, and billing](../storage-analytics.md) for Storage Analytics.</span></span>
* <span data-ttu-id="f9a39-205">[Azure Storage ölçümleri ve görünüm ölçüm verilerini etkinleştirme](../storage-enable-and-view-metrics.md) PowerShell kullanarak ve C# ile programlı olarak.</span><span class="sxs-lookup"><span data-stu-id="f9a39-205">[Enable Azure Storage metrics and view metrics data](../storage-enable-and-view-metrics.md) by using PowerShell and programmatically with C#.</span></span>
