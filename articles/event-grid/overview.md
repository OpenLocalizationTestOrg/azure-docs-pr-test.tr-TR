---
title: "Azure olay kılavuz genel bakış"
description: "Azure olay kılavuz ve onun kavramlarını açıklar."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/18/2017
ms.author: babanisa
ms.openlocfilehash: 59a834f32793e349d5639baf3c80dbcba274dfa8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="an-introduction-to-azure-event-grid"></a><span data-ttu-id="1e623-103">Azure olay kılavuzuna giriş</span><span class="sxs-lookup"><span data-stu-id="1e623-103">An introduction to Azure Event Grid</span></span>

<span data-ttu-id="1e623-104">Azure olay kılavuz, olay tabanlı mimari ile uygulamaları kolayca oluşturmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="1e623-104">Azure Event Grid allows you to easily build applications with event-based architectures.</span></span> <span data-ttu-id="1e623-105">Abone olma ve olay işleyicisi veya olayı göndermek için Web kancası uç noktası vermek istediğiniz Azure kaynağı seçin.</span><span class="sxs-lookup"><span data-stu-id="1e623-105">You select the Azure resource you would like to subscribe to, and give the event handler or WebHook endpoint to send the event to.</span></span> <span data-ttu-id="1e623-106">Olay kılavuz depolama BLOB'ları ve kaynak grupları gibi Azure hizmetlerinden gelen olaylar için yerleşik desteğe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="1e623-106">Event Grid has built-in support for events coming from Azure services, like storage blobs and resource groups.</span></span> <span data-ttu-id="1e623-107">Olay kılavuz özel konular ve özel Web kancalarını kullanarak uygulama ve üçüncü taraf olayları özel desteği de vardır.</span><span class="sxs-lookup"><span data-stu-id="1e623-107">Event Grid also has custom support for application and third-party events, using custom topics and custom webhooks.</span></span> 

<span data-ttu-id="1e623-108">Belirli olayları farklı uç noktalar, birden çok uç nokta için çok noktaya yayın yönlendirmek ve olaylarınızı güvenilir bir şekilde teslim emin olmak için filtreleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e623-108">You can use filters to route specific events to different endpoints, multicast to multiple endpoints, and make sure your events are reliably delivered.</span></span> <span data-ttu-id="1e623-109">Olay kılavuz, ayrıca özel ve üçüncü taraf olayları için destek oluşturdu.</span><span class="sxs-lookup"><span data-stu-id="1e623-109">Event Grid also has built in support for custom and third-party events.</span></span>

<span data-ttu-id="1e623-110">Önizleme sürümü için Event Grid tarafından **westus2** ve **westcentralus** konumları desteklenir.</span><span class="sxs-lookup"><span data-stu-id="1e623-110">For the preview release, Event Grid supports **westus2** and **westcentralus** locations.</span></span> <span data-ttu-id="1e623-111">Diğer bölgeler eklenir.</span><span class="sxs-lookup"><span data-stu-id="1e623-111">Other regions will be added.</span></span>

<span data-ttu-id="1e623-112">Bu makalede Azure olay kılavuz genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="1e623-112">This article provides an overview of Azure Event Grid.</span></span> <span data-ttu-id="1e623-113">Olay kılavuzla başlamak istiyorsanız, bkz: [Azure olay kılavuz oluşturma ve rota özel olaylarla](custom-event-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="1e623-113">If you want to get started with Event Grid, see [Create and route custom events with Azure Event Grid](custom-event-quickstart.md).</span></span>

![Olay kılavuz işlevsel modeli](./media/overview/event-grid-functional-model.png)

<span data-ttu-id="1e623-115">Şu anda, Blob Storage bir yayımcı olarak genel kullanıma açık değil.</span><span class="sxs-lookup"><span data-stu-id="1e623-115">Currently, Blob Storage is not publicly available as a publisher.</span></span>

## <a name="concepts"></a><span data-ttu-id="1e623-116">Kavramlar</span><span class="sxs-lookup"><span data-stu-id="1e623-116">Concepts</span></span>

<span data-ttu-id="1e623-117">Azure olay kılavuzunda yapmalarını sağlayan beş kavram vardır:</span><span class="sxs-lookup"><span data-stu-id="1e623-117">There are five concepts in Azure Event Grid that let you get going:</span></span>

* <span data-ttu-id="1e623-118">**Olayları** -ne oldu.</span><span class="sxs-lookup"><span data-stu-id="1e623-118">**Events** - What happened.</span></span>
* <span data-ttu-id="1e623-119">**Olay kaynakları/yayımcıları** - burada olay gerçekleşen.</span><span class="sxs-lookup"><span data-stu-id="1e623-119">**Event sources/publishers** - Where the event took place.</span></span>
* <span data-ttu-id="1e623-120">**Konular** -burada yayımcıları olayları göndereceği.</span><span class="sxs-lookup"><span data-stu-id="1e623-120">**Topics** - The endpoint where publishers send events.</span></span>
* <span data-ttu-id="1e623-121">**Olay abonelikleri** -rota olayları, bazen birden çok işleyici için uç nokta veya yerleşik mekanizması.</span><span class="sxs-lookup"><span data-stu-id="1e623-121">**Event subscriptions** - The endpoint or built-in mechanism to route events, sometimes to multiple handlers.</span></span> <span data-ttu-id="1e623-122">Abonelikleri akıllıca gelen olayları filtrelemek için işleyiciler tarafından da kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1e623-122">Subscriptions are also used by handlers to intelligently filter incoming events.</span></span>
* <span data-ttu-id="1e623-123">**Olay işleyicileri** -uygulama veya hizmet olaya tepki verme.</span><span class="sxs-lookup"><span data-stu-id="1e623-123">**Event handlers** - The app or service reacting to the event.</span></span>

<span data-ttu-id="1e623-124">Bu kavramlar hakkında daha fazla bilgi için bkz: [Azure olay kılavuzunda kavramları](concepts.md).</span><span class="sxs-lookup"><span data-stu-id="1e623-124">For more information about these concepts, see [Concepts in Azure Event Grid](concepts.md).</span></span>

## <a name="capabilities"></a><span data-ttu-id="1e623-125">Özellikler</span><span class="sxs-lookup"><span data-stu-id="1e623-125">Capabilities</span></span>

<span data-ttu-id="1e623-126">Azure olay kılavuz önemli özelliklerinden bazıları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1e623-126">Here are some of the key features of Azure Event Grid:</span></span>

* <span data-ttu-id="1e623-127">**Basitlik** -Point'ye tıklayın, Azure kaynak olaylarından herhangi bir olay işleyicisi veya uç nokta hedeflenir.</span><span class="sxs-lookup"><span data-stu-id="1e623-127">**Simplicity** - Point and click to aim events from your Azure resource to any event handler or endpoint.</span></span>
* <span data-ttu-id="1e623-128">**Filtreleme Gelişmiş** -filtre olay türü veya olay olay işleyicileri yalnızca ilgili olayları aldığınızdan emin olmak için yol yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="1e623-128">**Advanced filtering** - Filter on event type or event publish path to ensure event handlers only receive relevant events.</span></span>
* <span data-ttu-id="1e623-129">**Yayma** -birden çok uç nokta gerektiğinde sayıda basamağa olay kopyalarını göndermesini aynı olaya abone olun.</span><span class="sxs-lookup"><span data-stu-id="1e623-129">**Fan-out** - Subscribe multiple endpoints to the same event to send copies of the event to as many places as needed.</span></span>
* <span data-ttu-id="1e623-130">**Güvenilirlik** -olayları teslim edilir emin olmak için üstel geri alma 24 saatlik Denemeyle kullanma.</span><span class="sxs-lookup"><span data-stu-id="1e623-130">**Reliability** - Utilize 24-hour retry with exponential backoff to ensure events are delivered.</span></span>
* <span data-ttu-id="1e623-131">**Olay başına ödeme** - ödeme tutarını yalnızca olay kılavuzunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="1e623-131">**Pay-per-event** - Pay only for the amount you use Event Grid.</span></span>
* <span data-ttu-id="1e623-132">**Yüksek verimlilik** -yapı yüksek hacimli iş yükleri üzerinde olay kılavuz saniye başına milyonlarca olayı desteği.</span><span class="sxs-lookup"><span data-stu-id="1e623-132">**High throughput** - Build high-volume workloads on Event Grid with support for millions of events per second.</span></span>
* <span data-ttu-id="1e623-133">**Yerleşik olayları** - hale getirmek ve hızlı bir şekilde kaynak tanımlanan yerleşik olaylar ile çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="1e623-133">**Built-in Events** - Get up and running quickly with resource-defined built-in events.</span></span>
* <span data-ttu-id="1e623-134">**Özel olaylar** -olay kılavuz rota, filtre ve güvenilir bir şekilde teslim özel olaylar uygulamanızda kullanın.</span><span class="sxs-lookup"><span data-stu-id="1e623-134">**Custom Events** - use Event Grid route, filter, and reliably deliver custom events in your app.</span></span>

## <a name="built-in-publisher-and-handler-integration"></a><span data-ttu-id="1e623-135">Yerleşik yayımcı ve işleyici ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="1e623-135">Built-in publisher and handler integration</span></span>

<span data-ttu-id="1e623-136">Azure Yayımcılar ve işleyicileri dahil olmak üzere çok sayıda hizmetlerini kullanarak yerleşik olay destek sunar.</span><span class="sxs-lookup"><span data-stu-id="1e623-136">Azure offers built-in event support using numerous services, including both publishers and handlers.</span></span>

### <a name="publishers"></a><span data-ttu-id="1e623-137">Yayımcılar</span><span class="sxs-lookup"><span data-stu-id="1e623-137">Publishers</span></span>

<span data-ttu-id="1e623-138">Şu anda aşağıdaki Azure hizmetlerini olay kılavuz için yerleşik yayımcı desteğine sahiptir:</span><span class="sxs-lookup"><span data-stu-id="1e623-138">Currently, the following Azure services have built-in publisher support for event grid:</span></span>

* <span data-ttu-id="1e623-139">Kaynak grupları (yönetim işlemlerini)</span><span class="sxs-lookup"><span data-stu-id="1e623-139">Resource Groups (management operations)</span></span>
* <span data-ttu-id="1e623-140">Azure abonelikleri (yönetim işlemlerini)</span><span class="sxs-lookup"><span data-stu-id="1e623-140">Azure Subscriptions (management operations)</span></span>
* <span data-ttu-id="1e623-141">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="1e623-141">Event Hubs</span></span>
* <span data-ttu-id="1e623-142">Özel konular</span><span class="sxs-lookup"><span data-stu-id="1e623-142">Custom Topics</span></span>

<span data-ttu-id="1e623-143">Diğer Azure hizmetleriyle bu yıl eklenir.</span><span class="sxs-lookup"><span data-stu-id="1e623-143">Other Azure services will be added this year.</span></span>

### <a name="handlers"></a><span data-ttu-id="1e623-144">İşleyicileri</span><span class="sxs-lookup"><span data-stu-id="1e623-144">Handlers</span></span>

<span data-ttu-id="1e623-145">Şu anda aşağıdaki Azure hizmetlerini olay kılavuz yerleşik işleyici desteği vardır:</span><span class="sxs-lookup"><span data-stu-id="1e623-145">Currently, the following Azure services have built-in handler support for Event Grid:</span></span> 

* <span data-ttu-id="1e623-146">Azure İşlevleri</span><span class="sxs-lookup"><span data-stu-id="1e623-146">Azure Functions</span></span>
* <span data-ttu-id="1e623-147">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="1e623-147">Logic Apps</span></span>
* <span data-ttu-id="1e623-148">Azure Otomasyonu</span><span class="sxs-lookup"><span data-stu-id="1e623-148">Azure Automation</span></span>
* <span data-ttu-id="1e623-149">Web kancaları</span><span class="sxs-lookup"><span data-stu-id="1e623-149">WebHooks</span></span>

<span data-ttu-id="1e623-150">Diğer Azure hizmetleriyle bu yıl eklenir.</span><span class="sxs-lookup"><span data-stu-id="1e623-150">Other Azure services will be added this year.</span></span>

## <a name="what-can-i-do-with-event-grid"></a><span data-ttu-id="1e623-151">Olay kılavuzla ne yapabilirim?</span><span class="sxs-lookup"><span data-stu-id="1e623-151">What can I do with Event Grid?</span></span>

<span data-ttu-id="1e623-152">Azure olay kılavuz birkaç çok sunucusuz artırmak özellikleri, ops otomasyon ve tümleştirme çalışma sağlar:</span><span class="sxs-lookup"><span data-stu-id="1e623-152">Azure Event Grid provides several capabilities that vastly improve serverless, ops automation, and integration work:</span></span> 

### <a name="serverless-application-architectures"></a><span data-ttu-id="1e623-153">Sunucusuz uygulama mimarileri</span><span class="sxs-lookup"><span data-stu-id="1e623-153">Serverless application architectures</span></span>

![Sunucusuz bir uygulama](./media/overview/serverless_web_app.png)

<span data-ttu-id="1e623-155">Event Grid, veri kaynaklarını ve olay işleyicilerini bağlar.</span><span class="sxs-lookup"><span data-stu-id="1e623-155">Event Grid connects data sources and event handlers.</span></span> <span data-ttu-id="1e623-156">Event Grid’i örneğin bir blob depolama kapsayıcısına eklenen her yeni fotoğrafta görüntü analizini çalıştıracak sunucusuz bir işlev tetiklemek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e623-156">For example, use Event Grid to instantly trigger a serverless function to run image analysis each time a new photo is added to a blob storage container.</span></span> 

### <a name="ops-automation"></a><span data-ttu-id="1e623-157">OPS Otomasyon</span><span class="sxs-lookup"><span data-stu-id="1e623-157">Ops Automation</span></span>

![Ops otomasyonu](./media/overview/Ops_automation.png)

<span data-ttu-id="1e623-159">Event Grid, otomasyonu hızlandırmanızı ve ilke uygulamayı basitleştirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="1e623-159">Event Grid allows you to speed automation and simplify policy enforcement.</span></span> <span data-ttu-id="1e623-160">Örneğin Event Grid, sanal makine oluşturulduğunda veya SQL Veritabanı hazırlandığında Azure Otomasyonu’na bilgi verebilir.</span><span class="sxs-lookup"><span data-stu-id="1e623-160">For example, Event Grid can notify Azure Automation when a virtual machine is created, or a SQL Database is spun up.</span></span> <span data-ttu-id="1e623-161">Bu olaylar hizmet yapılandırmalarının uyumlu olup olmadığını otomatik olarak denetlemek, operasyon araçlarına meta verileri eklemek, sanal makineleri etiketlemek ve iş öğelerini dosyalamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1e623-161">These events can be used to automatically check that service configurations are compliant, put metadata into operations tools, tag virtual machines, or file work items.</span></span>

### <a name="application-integration"></a><span data-ttu-id="1e623-162">Uygulama tümleştirme</span><span class="sxs-lookup"><span data-stu-id="1e623-162">Application integration</span></span>

![Uygulama tümleştirme](./media/overview/app_integration.png)

<span data-ttu-id="1e623-164">Event Grid, uygulamanızı diğer hizmetlerle bağlar.</span><span class="sxs-lookup"><span data-stu-id="1e623-164">Event Grid connects your app with other services.</span></span> <span data-ttu-id="1e623-165">Örneğin, olay kılavuza uygulamanızın olay verileri göndermek ve yönlendirme, Gelişmiş, güvenilir teslim yararlanmak için özel bir konu oluşturun ve Azure ile tümleştirme doğrudan.</span><span class="sxs-lookup"><span data-stu-id="1e623-165">For example, create a custom topic to send your app's event data to Event Grid, and take advantage of its reliable delivery, advanced routing, and direct integration with Azure.</span></span> <span data-ttu-id="1e623-166">Ayrıca Event Grid’i Logic Apps ile birlikte kullanarak kod yazmadan her yerden veri işleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e623-166">Alternatively, you can use Event Grid with Logic Apps to process data anywhere, without writing code.</span></span> 

## <a name="how-is-event-grid-different-from-other-azure-integration-services"></a><span data-ttu-id="1e623-167">Olay kılavuz Azure tümleştirme hizmetlerinden farklı mı?</span><span class="sxs-lookup"><span data-stu-id="1e623-167">How is Event Grid different from other Azure integration services?</span></span>

<span data-ttu-id="1e623-168">Olay kılavuz olay denetimli, geriye dönük programlama sağlayan bir olay devre kartı ' dir.</span><span class="sxs-lookup"><span data-stu-id="1e623-168">Event Grid is an eventing backplane that enables event-driven, reactive programming.</span></span> <span data-ttu-id="1e623-169">Azure Hizmetleri ile son derece tümleşiktir ve üçüncü taraf hizmetleri ile tümleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="1e623-169">It is deeply integrated with Azure services and can be integrated with third-party services.</span></span> <span data-ttu-id="1e623-170">Olay iletisi hizmetler ve uygulamalar değişikliklere tepki vermek için gereken bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="1e623-170">The event message contains the information you need to react to changes in services and applications.</span></span> <span data-ttu-id="1e623-171">Olay kılavuz veri ardışık değil ve güncelleştirildi gerçek nesne dağıtmaz.</span><span class="sxs-lookup"><span data-stu-id="1e623-171">Event Grid is not a data pipeline, and does not deliver the actual object that was updated.</span></span>

<span data-ttu-id="1e623-172">Hizmet veri yolu işlemleri, sıralama, yinelenen algılama ve anlık tutarlılığı gerektiren geleneksel kurumsal uygulamalar için uygundur.</span><span class="sxs-lookup"><span data-stu-id="1e623-172">Service Bus is well suited for traditional enterprise applications that require transactions, ordering, duplicate detection, and instantaneous consistency.</span></span> <span data-ttu-id="1e623-173">Olay kılavuz hızı, Ölçek, tekliflerden için tasarlanmış ve düşük maliyetli bir reaktif modeldeki ' dir.</span><span class="sxs-lookup"><span data-stu-id="1e623-173">Event Grid is designed for speed, scale, breadth, and low cost in a reactive model.</span></span> <span data-ttu-id="1e623-174">Bunu sunucusuz mimarisi için uygundur.</span><span class="sxs-lookup"><span data-stu-id="1e623-174">It is well suited to serverless architecture.</span></span>

<span data-ttu-id="1e623-175">Olay kılavuz Logic Apps ve Event Hubs gibi diğer Azure hizmetleriyle tamamlar.</span><span class="sxs-lookup"><span data-stu-id="1e623-175">Event Grid complements other Azure services like Logic Apps and Event Hubs.</span></span> <span data-ttu-id="1e623-176">Olay kılavuz kendi iş akışını başlatmak için mantıksal uygulama tetikler.</span><span class="sxs-lookup"><span data-stu-id="1e623-176">Event Grid triggers the logic app to begin its workflow.</span></span> <span data-ttu-id="1e623-177">Olay hub'ları, hub olayı yakalamak olaylarına tepki vermek ve veri giriş ve dönüşüm işlem hatlarını oluşturmak etkinleştirerek olay kılavuzla çalışır.</span><span class="sxs-lookup"><span data-stu-id="1e623-177">Event Hubs works with Event Grid by enabling you to react to events from Event Hubs Capture, and build data ingress and transformation pipelines.</span></span>

## <a name="how-much-does-event-grid-cost"></a><span data-ttu-id="1e623-178">Nasıl olay kılavuz maliyeti nedir?</span><span class="sxs-lookup"><span data-stu-id="1e623-178">How much does Event Grid cost?</span></span>

<span data-ttu-id="1e623-179">Azure olay kılavuz bir olay başına ödeme fiyatlandırma modelini kullanır, bu nedenle, yalnızca, kullanım için ücret ödersiniz.</span><span class="sxs-lookup"><span data-stu-id="1e623-179">Azure Event Grid uses a pay-per-event pricing model, so you only pay for what you use.</span></span>

<span data-ttu-id="1e623-180">0.60 milyon işlemleri ($0.30 Önizleme sırasında) başına olay kılavuz maliyetleri ve ilk 100.000 işlemi her ay ücretsiz.</span><span class="sxs-lookup"><span data-stu-id="1e623-180">Event Grid costs $0.60 per million operations ($0.30 during preview) and the first 100,000 operation per month are free.</span></span> <span data-ttu-id="1e623-181">İşlem eşleştirme, teslim girişimi ve yönetim çağrıları Gelişmiş olay giriş tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="1e623-181">Operations are defined as event ingress, advanced match, delivery attempt, and management calls.</span></span>  <span data-ttu-id="1e623-182">Daha fazla ayrıntı bulunabilir [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/event-grid/).</span><span class="sxs-lookup"><span data-stu-id="1e623-182">More details can be found on the [pricing page](https://azure.microsoft.com/pricing/details/event-grid/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e623-183">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1e623-183">Next steps</span></span>

* <span data-ttu-id="1e623-184">[Oluşturma ve özel olaylarına abone olma](custom-event-quickstart.md) atlama sağ taraf ve özel olaylarınızı Azure olay kılavuz hızlı başlangıç kullanarak herhangi bir uç nokta için göndermeye başlayın.</span><span class="sxs-lookup"><span data-stu-id="1e623-184">[Create and subscribe to custom events](custom-event-quickstart.md) Jump right in and start sending your own custom events to any endpoint using the Azure Event Grid quickstart.</span></span>
* <span data-ttu-id="1e623-185">[Logic Apps olay işleyici kullanarak](monitor-virtual-machine-changes-event-grid-logic-app.md) olaylarına tepki vermek için Logic Apps kullanarak bir uygulama oluşturmaya üzerinde bir öğretici olay kılavuz tarafından gönderilir.</span><span class="sxs-lookup"><span data-stu-id="1e623-185">[Using Logic Apps as an Event Handler](monitor-virtual-machine-changes-event-grid-logic-app.md) A tutorial on building an app using Logic Apps to react to events pushed by Event Grid.</span></span>
* [<span data-ttu-id="1e623-186">Olay kılavuz REST API Başvurusu</span><span class="sxs-lookup"><span data-stu-id="1e623-186">Event Grid REST API reference</span></span>](/rest/api/eventgrid)  
  <span data-ttu-id="1e623-187">Olay Aboneliklerini yönetmek için Azure olay kılavuz ve başvurusu hakkında daha fazla teknik bilgi sağlayan Yönlendirme ve filtreleme.</span><span class="sxs-lookup"><span data-stu-id="1e623-187">Provides more technical information about the Azure Event Grid, and a reference for managing Event Subscriptions, routing, and filtering.</span></span>