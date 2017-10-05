---
title: "Microsoft Azure ölçümlerini genel bakış | Microsoft Docs"
description: "Ölçümleri ve bunların kullanılması Microsoft Azure genel bakış"
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 405ec51c-0946-4ec9-b535-60f65c4a5bd1
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/02/2017
ms.author: johnkem
ms.openlocfilehash: 3aff83ab2c157a18f4af6200a79bae7e5d6f0ea2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="overview-of-metrics-in-microsoft-azure"></a><span data-ttu-id="cb4ea-103">Microsoft Azure ölçümlerini genel bakış</span><span class="sxs-lookup"><span data-stu-id="cb4ea-103">Overview of metrics in Microsoft Azure</span></span>
<span data-ttu-id="cb4ea-104">Microsoft Azure'da ölçümleri nelerdir bu makalede faydaları ve bunları kullanmaya başlamak nasıl.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-104">This article describes what metrics are in Microsoft Azure, their benefits, and how to start using them.</span></span>  

## <a name="what-are-metrics"></a><span data-ttu-id="cb4ea-105">Ölçümleri nelerdir?</span><span class="sxs-lookup"><span data-stu-id="cb4ea-105">What are metrics?</span></span>
<span data-ttu-id="cb4ea-106">Azure İzleyicisi, performans ve sistem durumu, iş yüklerinin Azure üzerinde görünürlük elde etmek için telemetri kullanmasına olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-106">Azure Monitor enables you to consume telemetry to gain visibility into the performance and health of your workloads on Azure.</span></span> <span data-ttu-id="cb4ea-107">En önemli Azure telemetri verileri çoğu Azure kaynaklar tarafından gösterilen (performans sayaçlarını olarak da bilinir) ölçümleri türüdür.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-107">The most important type of Azure telemetry data is the metrics (also called performance counters) emitted by most Azure resources.</span></span> <span data-ttu-id="cb4ea-108">Azure İzleyicisi'ni yapılandırma ve izleme ve sorun giderme için bu ölçümleri kullanmak için çeşitli yöntemler sağlar.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-108">Azure Monitor provides several ways to configure and consume these metrics for monitoring and troubleshooting.</span></span>

## <a name="what-can-you-do-with-metrics"></a><span data-ttu-id="cb4ea-109">Ölçümleri ile neler yapabileceğiniz?</span><span class="sxs-lookup"><span data-stu-id="cb4ea-109">What can you do with metrics?</span></span>
<span data-ttu-id="cb4ea-110">Ölçümleri telemetri değerli bir kaynaktır ve aşağıdaki görevleri yapmanıza olanak sağlar:</span><span class="sxs-lookup"><span data-stu-id="cb4ea-110">Metrics are a valuable source of telemetry and enable you to do the following tasks:</span></span>

* <span data-ttu-id="cb4ea-111">**Performans İzleme** kendi ölçümleri portal grafik Çizdirmek ve bu grafik bir Pano için sabitleme kaynağın (örneğin, bir VM, Web sitesi ya da mantıksal uygulama).</span><span class="sxs-lookup"><span data-stu-id="cb4ea-111">**Track the performance** of your resource (such as a VM, website, or logic app) by plotting its metrics on a portal chart and pinning that chart to a dashboard.</span></span>
* <span data-ttu-id="cb4ea-112">**Bir sorun bildirim alma** , etkiler, kaynak performans ölçüm belirli bir eşiği kestiği olduğunda.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-112">**Get notified of an issue** that impacts the performance of your resource when a metric crosses a certain threshold.</span></span>
* <span data-ttu-id="cb4ea-113">**Otomatik eylemler yapılandırma**otomatik ölçeklendirmeyi bir kaynak veya runbook belirli bir eşiği ölçüm kestiği zaman tetiklemeden gibi.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-113">**Configure automated actions**, such as autoscaling a resource or firing a runbook when a metric crosses a certain threshold.</span></span>
* <span data-ttu-id="cb4ea-114">**Gelişmiş analizler gerçekleştirmek** veya kaynağınız performans ya da kullanım eğilimlerini üzerinde raporlama.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-114">**Perform advanced analytics** or reporting on performance or usage trends of your resource.</span></span>
* <span data-ttu-id="cb4ea-115">**Arşiv** kaynağınız performans veya sistem durumu geçmişini **uyumluluk veya Denetim** amaçlar.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-115">**Archive** the performance or health history of your resource **for compliance or auditing** purposes.</span></span>

## <a name="what-are-the-characteristics-of-metrics"></a><span data-ttu-id="cb4ea-116">Ölçümleri özelliklerini nelerdir?</span><span class="sxs-lookup"><span data-stu-id="cb4ea-116">What are the characteristics of metrics?</span></span>
<span data-ttu-id="cb4ea-117">Ölçümleri aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="cb4ea-117">Metrics have the following characteristics:</span></span>

* <span data-ttu-id="cb4ea-118">Tüm ölçümleri sahip **bir dakikalık sıklığı**.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-118">All metrics have **one-minute frequency**.</span></span> <span data-ttu-id="cb4ea-119">Bir ölçü değeri dakikada, kaynaktan durumu ve kaynağınıza durumunu gerçek zamanlı görünürlük yakın vermiş alırsınız.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-119">You receive a metric value every minute from your resource, giving you near real-time visibility into the state and health of your resource.</span></span>
* <span data-ttu-id="cb4ea-120">Metrik **kullanılabilir hemen**.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-120">Metrics are **available immediately**.</span></span> <span data-ttu-id="cb4ea-121">Kabul ya da ek tanılama ayarlamak gerekmez.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-121">You don't need to opt in or set up additional diagnostics.</span></span>
* <span data-ttu-id="cb4ea-122">Erişebileceğiniz **geçmişi 30 gün** her ölçümü için.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-122">You can access **30 days of history** for each metric.</span></span> <span data-ttu-id="cb4ea-123">Son ve aylık eğilimler performansı veya kaynağınız durumunu hızlı bir şekilde bakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-123">You can quickly look at the recent and monthly trends in the performance or health of your resource.</span></span>

<span data-ttu-id="cb4ea-124">Ayrıca şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="cb4ea-124">You can also:</span></span>

* <span data-ttu-id="cb4ea-125">Bir ölçüm yapılandırma **bir bildirim gönderir ya da alan kural eylemi otomatik uyarı** zaman ölçümü kestiği ayarladığınız eşiği.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-125">Configure a metric **alert rule that sends a notification or takes automated action** when the metric crosses the threshold that you have set.</span></span> <span data-ttu-id="cb4ea-126">Otomatik ölçeklendirme, gelen istekleri karşılamak için kaynağı kullanıma ölçeklendirmenizi sağlar veya Web sitesi ya da bilgi işlem kaynakları yükler özel bir otomatik eylemdir.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-126">Autoscale is a special automated action that enables you to scale out your resource to meet incoming requests or loads on your website or computing resources.</span></span> <span data-ttu-id="cb4ea-127">Bir eşik geçmeden bir ölçüm bağlı içeri veya dışarı ölçeklendirmek için otomatik ölçeklendirme ayarı kural yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-127">You can configure an Autoscale setting rule to scale in or out based on a metric crossing a threshold.</span></span>

* <span data-ttu-id="cb4ea-128">**Rota** tüm ölçümleri anlık analytics, arama ve kaynaklarınızı ölçümleri verileri üzerinde özel uyarı etkinleştirmek için Application Insights ya da günlük analizi (OMS).</span><span class="sxs-lookup"><span data-stu-id="cb4ea-128">**Route** all metrics Application Insights or Log Analytics (OMS) to enable instant analytics, search, and custom alerting on metrics data from your resources.</span></span> <span data-ttu-id="cb4ea-129">Ayrıca bunları Azure Stream Analytics veya neredeyse gerçek zamanlı analiz için özel uygulamalar yönlendirmenize olanak sağlayarak bir olay Hub'ına ölçümleri akışını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-129">You can also stream metrics to an Event Hub, enabling you to then route them to Azure Stream Analytics or to custom apps for near-real time analysis.</span></span> <span data-ttu-id="cb4ea-130">Tanılama ayarları kullanarak akış olay hub'ı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-130">You set up Event Hub streaming using diagnostic settings.</span></span>

* <span data-ttu-id="cb4ea-131">**Arşiv depolama ölçümleri** daha uzun bekletme veya çevrimdışı raporlama için kullanın.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-131">**Archive metrics to storage** for longer retention or use them for offline reporting.</span></span> <span data-ttu-id="cb4ea-132">Kaynağınız için tanılama ayarlarını yapılandırdığınızda, Azure Blob depolama alanına ölçümlerinizi yönlendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-132">You can route your metrics to Azure Blob storage when you configure diagnostic settings for your resource.</span></span>

* <span data-ttu-id="cb4ea-133">Kolayca bulmak, erişim ve **tüm ölçümleri görüntülemek** bir kaynak seçin ve bir grafik ölçümleri çizim Azure Portalı aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-133">Easily discover, access, and **view all metrics** via the Azure portal when you select a resource and plot the metrics on a chart.</span></span>

* <span data-ttu-id="cb4ea-134">**Tüketen** yeni Azure İzleyici REST API'leri aracılığıyla ölçümleri.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-134">**Consume** the metrics via the new Azure Monitor REST APIs.</span></span>

* <span data-ttu-id="cb4ea-135">**Sorgu** PowerShell cmdlet'lerini veya platformlar arası REST API kullanarak ölçümleri.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-135">**Query** metrics by using the PowerShell cmdlets or the Cross-Platform REST API.</span></span>

  ![Azure İzleyicisi'nde ölçümleri yönlendirme](./media/monitoring-overview-metrics/Metrics_Overview_v4.png)

## <a name="access-metrics-via-the-portal"></a><span data-ttu-id="cb4ea-137">Portal üzerinden erişim ölçümleri</span><span class="sxs-lookup"><span data-stu-id="cb4ea-137">Access metrics via the portal</span></span>
<span data-ttu-id="cb4ea-138">Aşağıda Azure portalını kullanarak bir ölçüm grafik oluşturmak nasıl hızlı bir kılavuz vardır.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-138">Following is a quick walkthrough of how to create a metric chart by using the Azure portal.</span></span>

### <a name="to-view-metrics-after-creating-a-resource"></a><span data-ttu-id="cb4ea-139">Bir kaynak oluşturduktan sonra ölçümleri görüntülemek için</span><span class="sxs-lookup"><span data-stu-id="cb4ea-139">To view metrics after creating a resource</span></span>
1. <span data-ttu-id="cb4ea-140">Azure Portalı'nı açın.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-140">Open the Azure portal.</span></span>
2. <span data-ttu-id="cb4ea-141">Azure App Service Web sitesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-141">Create an Azure App Service website.</span></span>
3. <span data-ttu-id="cb4ea-142">Bir Web sitesini oluşturduktan sonra Git **genel bakış** Web sitesinin dikey.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-142">After you create a website, go to the **Overview** blade of the website.</span></span>
4. <span data-ttu-id="cb4ea-143">Yeni ölçümleri olarak görüntüleyebileceğiniz bir **izleme** döşeme.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-143">You can view new metrics as a **Monitoring** tile.</span></span> <span data-ttu-id="cb4ea-144">Ardından, döşemesini düzenleyin ve daha fazla ölçümleri seçin.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-144">You can then edit the tile and select more metrics.</span></span>

   ![Azure İzleyicisi'nde kaynak ölçümleri](./media/monitoring-overview-metrics/MetricsOverview1.png)

### <a name="to-access-all-metrics-in-a-single-place"></a><span data-ttu-id="cb4ea-146">Tüm ölçümlerini tek bir yerde erişmek için</span><span class="sxs-lookup"><span data-stu-id="cb4ea-146">To access all metrics in a single place</span></span>
1. <span data-ttu-id="cb4ea-147">Azure Portalı'nı açın.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-147">Open the Azure portal.</span></span>
2. <span data-ttu-id="cb4ea-148">Yeni gidin **İzleyici** sekmesini seçin ve sonra **ölçümleri** altındaki seçeneği.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-148">Navigate to the new **Monitor** tab, and then and select the **Metrics** option underneath it.</span></span>
3. <span data-ttu-id="cb4ea-149">Aboneliğiniz, kaynak grubu ve kaynak adının aşağı açılan listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-149">Select your subscription, resource group, and the name of the resource from the drop-down list.</span></span>
4. <span data-ttu-id="cb4ea-150">Kullanılabilir ölçümler listesini görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-150">View the available metrics list.</span></span> <span data-ttu-id="cb4ea-151">Ardından ilgilendiğiniz ve tasarlayın ölçümü seçin.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-151">Then select the metric you are interested in and plot it.</span></span>
5. <span data-ttu-id="cb4ea-152">Bu Pano için sabitleme sağ üst köşesinde üzerinde tıklayarak sabitleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-152">You can pin it to the dashboard by clicking the pin on the upper-right corner.</span></span>

   ![Azure İzleyici tek bir yerde tüm ölçümlerini erişim](./media/monitoring-overview-metrics/MetricsOverview2.png)

> [!NOTE]
> <span data-ttu-id="cb4ea-154">Herhangi bir ek tanılama ayar sanal makine ölçek ayarlar ve VM'lerin (Azure Resource Manager tabanlı) ana bilgisayar düzeyinde ölçümleri erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-154">You can access host-level metrics from VMs (Azure Resource Manager-based) and virtual machine scale sets without any additional diagnostic setup.</span></span> <span data-ttu-id="cb4ea-155">Bu yeni ana bilgisayar düzeyinde ölçümleri, Windows ve Linux örnekleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-155">These new host-level metrics are available for Windows and Linux instances.</span></span> <span data-ttu-id="cb4ea-156">Bu ölçümler zaman Azure tanılama Vm'lerinizdeki veya sanal makine ölçek kümeleri kapatmanız erişiminiz olan konuk işletim sistemi düzeyinde ölçümleri ile karıştırılmamalıdır üzeresiniz.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-156">These metrics are not to be confused with the Guest-OS-level metrics that you have access to when you turn on Azure Diagnostics on your VMs or virtual machine scale sets.</span></span> <span data-ttu-id="cb4ea-157">Tanılama yapılandırma hakkında daha fazla bilgi edinmek için [Microsoft Azure tanılama nedir](../azure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="cb4ea-157">To learn more about configuring Diagnostics, see [What is Microsoft Azure Diagnostics](../azure-diagnostics.md).</span></span>
>
>

## <a name="access-metrics-via-the-rest-api"></a><span data-ttu-id="cb4ea-158">REST API üzerinden erişim ölçümleri</span><span class="sxs-lookup"><span data-stu-id="cb4ea-158">Access metrics via the REST API</span></span>
<span data-ttu-id="cb4ea-159">Azure ölçümleri Azure İzleyici API'leri erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-159">Azure Metrics can be accessed via the Azure Monitor APIs.</span></span> <span data-ttu-id="cb4ea-160">Yardımcı iki API'ları bulmak ve erişim ölçümleri vardır:</span><span class="sxs-lookup"><span data-stu-id="cb4ea-160">There are two APIs that help you discover and access metrics:</span></span>

* <span data-ttu-id="cb4ea-161">Kullanım [Azure İzleyici ölçüm tanımlarını REST API](https://msdn.microsoft.com/library/mt743621.aspx) hizmeti için kullanılabilir ölçümleri listesi erişmek için.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-161">Use the [Azure Monitor Metric definitions REST API](https://msdn.microsoft.com/library/mt743621.aspx) to access the list of metrics that are available for a service.</span></span>
* <span data-ttu-id="cb4ea-162">Kullanım [Azure İzleyici ölçümleri REST API](https://msdn.microsoft.com/library/mt743622.aspx) gerçek ölçümleri verilere erişmek için.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-162">Use the [Azure Monitor Metrics REST API](https://msdn.microsoft.com/library/mt743622.aspx) to access the actual metrics data.</span></span>

> [!NOTE]
> <span data-ttu-id="cb4ea-163">Bu makale aracılığıyla ölçümleri kapsamaktadır [ölçümleri için yeni API](https://msdn.microsoft.com/library/dn931930.aspx) Azure kaynakları için.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-163">This article covers the metrics via the [new API for metrics](https://msdn.microsoft.com/library/dn931930.aspx) for Azure resources.</span></span> <span data-ttu-id="cb4ea-164">Yeni ölçüm tanımlarını API için API sürümü 2016-03-01 ve ölçüm API'si sürümü 2016-09-01.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-164">The API version for the new metric definitions API is 2016-03-01 and the version for metrics API is 2016-09-01.</span></span> <span data-ttu-id="cb4ea-165">Eski ölçüm tanımlarını ve ölçümler API sürümü 2014-04-01 ile erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-165">The legacy metric definitions and metrics can be accessed with the API version 2014-04-01.</span></span>
>
>

<span data-ttu-id="cb4ea-166">Azure İzleyici REST API'lerini kullanarak daha ayrıntılı bilgi için bkz: [Azure İzleyici REST API izlenecek](monitoring-rest-api-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="cb4ea-166">For a more detailed walkthrough using the Azure Monitor REST APIs, see [Azure Monitor REST API walkthrough](monitoring-rest-api-walkthrough.md).</span></span>

## <a name="export-metrics"></a><span data-ttu-id="cb4ea-167">Dışarı aktarma ölçümleri</span><span class="sxs-lookup"><span data-stu-id="cb4ea-167">Export metrics</span></span>
<span data-ttu-id="cb4ea-168">Gidebilirsiniz **tanılama ayarları** altında dikey **İzleyici** sekmesinde ve ölçümleri için dışarı aktarma seçeneklerini görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-168">You can go to the **Diagnostics settings** blade under the **Monitor** tab and view the export options for metrics.</span></span> <span data-ttu-id="cb4ea-169">Blob depolama alanına yönlendirilecek ölçümleri (ve tanılama günlükleri) Azure Event Hubs veya OMS bu makalede daha önce bahsedilen kullanım örnekleri için seçebileceğiniz.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-169">You can select metrics (and diagnostic logs) to be routed to Blob storage, to Azure Event Hubs, or to OMS for use-cases that were mentioned previously in this article.</span></span>

 ![Azure İzleyicisi'nde ölçümleri dışa aktarma seçenekleri](./media/monitoring-overview-metrics/MetricsOverview3.png)

<span data-ttu-id="cb4ea-171">Bu Resource Manager şablonları yapılandırabilirsiniz [PowerShell](insights-powershell-samples.md), [Azure CLI](insights-cli-samples.md), veya [REST API'leri](https://msdn.microsoft.com/library/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="cb4ea-171">You can configure this via Resource Manager templates, [PowerShell](insights-powershell-samples.md), [Azure CLI](insights-cli-samples.md), or [REST APIs](https://msdn.microsoft.com/library/dn931943.aspx).</span></span>

## <a name="take-action-on-metrics"></a><span data-ttu-id="cb4ea-172">Ölçümleri eylem</span><span class="sxs-lookup"><span data-stu-id="cb4ea-172">Take action on metrics</span></span>
<span data-ttu-id="cb4ea-173">Bildirimleri almak veya ölçüm verilerini otomatik eylemleri için uyarı kuralları veya otomatik ölçeklendirme ayarlarını yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-173">To receive notifications or take automated actions on metric data, you can configure alert rules or Autoscale settings.</span></span>

### <a name="configure-alert-rules"></a><span data-ttu-id="cb4ea-174">Uyarı kurallarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="cb4ea-174">Configure alert rules</span></span>
<span data-ttu-id="cb4ea-175">Uyarı kuralları ölçümleri yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-175">You can configure alert rules on metrics.</span></span> <span data-ttu-id="cb4ea-176">Bu uyarı kuralları, bir ölçüm belirli bir eşiği aşıldığında, kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-176">These alert rules can check if a metric has crossed a certain threshold.</span></span> <span data-ttu-id="cb4ea-177">Bunlar daha sonra e-posta ile bildir veya özel komut dosyaları çalıştırmak için kullanılan bir Web kancası tetiklenecek.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-177">They can then notify you via email or fire a webhook that can be used to run any custom script.</span></span> <span data-ttu-id="cb4ea-178">Web kancası, üçüncü taraf ürün tümleştirmeler yapılandırmak için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-178">You can also use the webhook to configure third-party product integrations.</span></span>

 ![Ölçümleri ve Azure İzleyicisi'nde uyarı kuralları](./media/monitoring-overview-metrics/MetricsOverview4.png)

### <a name="autoscale-your-azure-resources"></a><span data-ttu-id="cb4ea-180">Otomatik ölçeklendirme Azure kaynakları</span><span class="sxs-lookup"><span data-stu-id="cb4ea-180">Autoscale your Azure resources</span></span>
<span data-ttu-id="cb4ea-181">Bazı Azure kaynaklarını veya ölçeklendirme, iş yüklerini işlemek üzere birden çok örneğini destekler.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-181">Some Azure resources support the scaling out or in of multiple instances to handle your workloads.</span></span> <span data-ttu-id="cb4ea-182">Otomatik ölçeklendirme, uygulama hizmeti (Web uygulamaları), sanal makine ölçek kümeleri ve klasik Azure bulut Hizmetleri için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-182">Autoscale applies to App Service (Web Apps), virtual machine scale sets, and classic Azure Cloud Services.</span></span> <span data-ttu-id="cb4ea-183">İş yükünüzün etkiler belirli bir ölçüm belirttiğiniz bir eşik kestiği olduğunda veya ölçeklendirmek için otomatik ölçeklendirme kuralları yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-183">You can configure Autoscale rules to scale out or in when a certain metric that impacts your workload crosses a threshold that you specify.</span></span> <span data-ttu-id="cb4ea-184">Daha fazla bilgi için bkz: [otomatik ölçeklendirmeyi genel bakış](monitoring-overview-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="cb4ea-184">For more information, see [Overview of autoscaling](monitoring-overview-autoscale.md).</span></span>

 ![Ölçümleri ve Azure İzleyicisi'nde otomatik ölçeklendirme](./media/monitoring-overview-metrics/MetricsOverview5.png)

## <a name="learn-about-supported-services-and-metrics"></a><span data-ttu-id="cb4ea-186">Desteklenen hizmetler ve ölçümleri hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="cb4ea-186">Learn about supported services and metrics</span></span>
<span data-ttu-id="cb4ea-187">Yeni bir ölçüm altyapısı Azure izleyicisidir.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-187">Azure Monitor is a new metrics infrastructure.</span></span> <span data-ttu-id="cb4ea-188">Azure portalı ve Azure İzleyici API yeni sürüm aşağıdaki Azure hizmetlerini destekler:</span><span class="sxs-lookup"><span data-stu-id="cb4ea-188">It supports the following Azure services in the Azure portal and the new version of the Azure Monitor API:</span></span>

* <span data-ttu-id="cb4ea-189">Sanal makineleri (Azure Resource Manager tabanlı)</span><span class="sxs-lookup"><span data-stu-id="cb4ea-189">VMs (Azure Resource Manager-based)</span></span>
* <span data-ttu-id="cb4ea-190">Sanal makine ölçek kümeleri</span><span class="sxs-lookup"><span data-stu-id="cb4ea-190">Virtual machine scale sets</span></span>
* <span data-ttu-id="cb4ea-191">Batch</span><span class="sxs-lookup"><span data-stu-id="cb4ea-191">Batch</span></span>
* <span data-ttu-id="cb4ea-192">Olay hub'ları ad alanı</span><span class="sxs-lookup"><span data-stu-id="cb4ea-192">Event Hubs namespace</span></span>
* <span data-ttu-id="cb4ea-193">Hizmet veri yolu ad alanı (yalnızca premium SKU)</span><span class="sxs-lookup"><span data-stu-id="cb4ea-193">Service Bus namespace (premium SKU only)</span></span>
* <span data-ttu-id="cb4ea-194">SQL veritabanı (sürüm 12)</span><span class="sxs-lookup"><span data-stu-id="cb4ea-194">SQL Database (version 12)</span></span>
* <span data-ttu-id="cb4ea-195">SQL esnek havuzu</span><span class="sxs-lookup"><span data-stu-id="cb4ea-195">Elastic SQL Pool</span></span>
* <span data-ttu-id="cb4ea-196">Web Siteleri</span><span class="sxs-lookup"><span data-stu-id="cb4ea-196">Websites</span></span>
* <span data-ttu-id="cb4ea-197">Web sunucu grupları</span><span class="sxs-lookup"><span data-stu-id="cb4ea-197">Web server farms</span></span>
* <span data-ttu-id="cb4ea-198">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="cb4ea-198">Logic Apps</span></span>
* <span data-ttu-id="cb4ea-199">IOT hub'ları</span><span class="sxs-lookup"><span data-stu-id="cb4ea-199">IoT hubs</span></span>
* <span data-ttu-id="cb4ea-200">Redis Önbelleği</span><span class="sxs-lookup"><span data-stu-id="cb4ea-200">Redis Cache</span></span>
* <span data-ttu-id="cb4ea-201">Ağ: Uygulama ağ geçitleri</span><span class="sxs-lookup"><span data-stu-id="cb4ea-201">Networking: Application gateways</span></span>
* <span data-ttu-id="cb4ea-202">Arama</span><span class="sxs-lookup"><span data-stu-id="cb4ea-202">Search</span></span>

<span data-ttu-id="cb4ea-203">Desteklenen tüm hizmetleri ve bunların ölçümlere ayrıntılı bir listesini görüntüleyebileceğiniz [Azure İzleyici ölçümleri--kaynak türü başına desteklenen ölçümleri](monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="cb4ea-203">You can view a detailed list of all the supported services and their metrics at [Azure Monitor metrics--supported metrics per resource type](monitoring-supported-metrics.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb4ea-204">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cb4ea-204">Next steps</span></span>
<span data-ttu-id="cb4ea-205">Bu makale boyunca bağlantılara bakın.</span><span class="sxs-lookup"><span data-stu-id="cb4ea-205">Refer to the links throughout this article.</span></span> <span data-ttu-id="cb4ea-206">Ayrıca, hakkında bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="cb4ea-206">Additionally, learn about:</span></span>  

* [<span data-ttu-id="cb4ea-207">Otomatik ölçeklendirme için ortak ölçümleri</span><span class="sxs-lookup"><span data-stu-id="cb4ea-207">Common metrics for autoscaling</span></span>](insights-autoscale-common-metrics.md)
* [<span data-ttu-id="cb4ea-208">Uyarı kuralları oluşturma</span><span class="sxs-lookup"><span data-stu-id="cb4ea-208">How to create alert rules</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="cb4ea-209">Günlük analizi ile Azure depolama biriminden günlüklerini analiz edin</span><span class="sxs-lookup"><span data-stu-id="cb4ea-209">Analyze logs from Azure storage with Log Analytics</span></span>](../log-analytics/log-analytics-azure-storage.md)
