---
title: "aaaAzure olay kılavuz genel bakış"
description: "Azure olay kılavuz ve onun kavramlarını açıklar."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/18/2017
ms.author: babanisa
ms.openlocfilehash: 95dce22e9335df88e81b134143a6c14994c26b8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="an-introduction-tooazure-event-grid"></a><span data-ttu-id="4e632-103">Bir giriş tooAzure olay kılavuz</span><span class="sxs-lookup"><span data-stu-id="4e632-103">An introduction tooAzure Event Grid</span></span>

<span data-ttu-id="4e632-104">Azure olay kılavuz tooeasily yapı uygulamalarla olay tabanlı mimari sağlar.</span><span class="sxs-lookup"><span data-stu-id="4e632-104">Azure Event Grid allows you tooeasily build applications with event-based architectures.</span></span> <span data-ttu-id="4e632-105">Hello için toosubscribe gibi ve hello olay işleyicisi veya Web kancası uç nokta toosend hello olaya vermeniz Azure kaynak seçin.</span><span class="sxs-lookup"><span data-stu-id="4e632-105">You select hello Azure resource you would like toosubscribe to, and give hello event handler or WebHook endpoint toosend hello event to.</span></span> <span data-ttu-id="4e632-106">Olay kılavuz depolama BLOB'ları ve kaynak grupları gibi Azure hizmetlerinden gelen olaylar için yerleşik desteğe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="4e632-106">Event Grid has built-in support for events coming from Azure services, like storage blobs and resource groups.</span></span> <span data-ttu-id="4e632-107">Olay kılavuz özel konular ve özel Web kancalarını kullanarak uygulama ve üçüncü taraf olayları özel desteği de vardır.</span><span class="sxs-lookup"><span data-stu-id="4e632-107">Event Grid also has custom support for application and third-party events, using custom topics and custom webhooks.</span></span> 

<span data-ttu-id="4e632-108">Filtreler tooroute belirli olayları toodifferent uç noktaları, çok noktaya yayın toomultiple uç noktaları kullanın ve olaylarınızı güvenilir bir şekilde teslim emin olun.</span><span class="sxs-lookup"><span data-stu-id="4e632-108">You can use filters tooroute specific events toodifferent endpoints, multicast toomultiple endpoints, and make sure your events are reliably delivered.</span></span> <span data-ttu-id="4e632-109">Olay kılavuz, ayrıca özel ve üçüncü taraf olayları için destek oluşturdu.</span><span class="sxs-lookup"><span data-stu-id="4e632-109">Event Grid also has built in support for custom and third-party events.</span></span>

<span data-ttu-id="4e632-110">Merhaba Önizleme sürümü için olay kılavuz destekleyen **westus2** ve **westcentralus** konumları.</span><span class="sxs-lookup"><span data-stu-id="4e632-110">For hello preview release, Event Grid supports **westus2** and **westcentralus** locations.</span></span> <span data-ttu-id="4e632-111">Diğer bölgeler eklenir.</span><span class="sxs-lookup"><span data-stu-id="4e632-111">Other regions will be added.</span></span>

<span data-ttu-id="4e632-112">Bu makalede Azure olay kılavuz genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="4e632-112">This article provides an overview of Azure Event Grid.</span></span> <span data-ttu-id="4e632-113">Olay Kılavuzu ile çalışmaya tooget istiyorsanız, bkz: [Azure olay kılavuz oluşturma ve rota özel olaylarla](custom-event-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="4e632-113">If you want tooget started with Event Grid, see [Create and route custom events with Azure Event Grid](custom-event-quickstart.md).</span></span>

![Olay kılavuz işlevsel modeli](./media/overview/event-grid-functional-model.png)

<span data-ttu-id="4e632-115">Şu anda, Blob Storage bir yayımcı olarak genel kullanıma açık değil.</span><span class="sxs-lookup"><span data-stu-id="4e632-115">Currently, Blob Storage is not publicly available as a publisher.</span></span>

## <a name="concepts"></a><span data-ttu-id="4e632-116">Kavramlar</span><span class="sxs-lookup"><span data-stu-id="4e632-116">Concepts</span></span>

<span data-ttu-id="4e632-117">Azure olay kılavuzunda yapmalarını sağlayan beş kavram vardır:</span><span class="sxs-lookup"><span data-stu-id="4e632-117">There are five concepts in Azure Event Grid that let you get going:</span></span>

* <span data-ttu-id="4e632-118">**Olayları** -ne oldu.</span><span class="sxs-lookup"><span data-stu-id="4e632-118">**Events** - What happened.</span></span>
* <span data-ttu-id="4e632-119">**Olay kaynakları/yayımcıları** - hello olay gerçekleşen burada.</span><span class="sxs-lookup"><span data-stu-id="4e632-119">**Event sources/publishers** - Where hello event took place.</span></span>
* <span data-ttu-id="4e632-120">**Konular** -burada yayımcıları olayları göndermek endpoint hello.</span><span class="sxs-lookup"><span data-stu-id="4e632-120">**Topics** - hello endpoint where publishers send events.</span></span>
* <span data-ttu-id="4e632-121">**Olay abonelikleri** -hello uç noktası veya yerleşik mekanizması tooroute olaylar, bazen toomultiple işleyicileri.</span><span class="sxs-lookup"><span data-stu-id="4e632-121">**Event subscriptions** - hello endpoint or built-in mechanism tooroute events, sometimes toomultiple handlers.</span></span> <span data-ttu-id="4e632-122">Abonelikleri işleyicileri toointelligently filtre gelen olaylar tarafından da kullanılır.</span><span class="sxs-lookup"><span data-stu-id="4e632-122">Subscriptions are also used by handlers toointelligently filter incoming events.</span></span>
* <span data-ttu-id="4e632-123">**Olay işleyicileri** - hello uygulama veya hizmet tanımlandığında toohello olay.</span><span class="sxs-lookup"><span data-stu-id="4e632-123">**Event handlers** - hello app or service reacting toohello event.</span></span>

<span data-ttu-id="4e632-124">Bu kavramlar hakkında daha fazla bilgi için bkz: [Azure olay kılavuzunda kavramları](concepts.md).</span><span class="sxs-lookup"><span data-stu-id="4e632-124">For more information about these concepts, see [Concepts in Azure Event Grid](concepts.md).</span></span>

## <a name="capabilities"></a><span data-ttu-id="4e632-125">Özellikler</span><span class="sxs-lookup"><span data-stu-id="4e632-125">Capabilities</span></span>

<span data-ttu-id="4e632-126">Azure olay kılavuz hello önemli özelliklerinden bazıları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="4e632-126">Here are some of hello key features of Azure Event Grid:</span></span>

* <span data-ttu-id="4e632-127">**Basitlik** -Azure kaynak tooany olay işleyicisi veya uç noktasına tooaim olayları.</span><span class="sxs-lookup"><span data-stu-id="4e632-127">**Simplicity** - Point and click tooaim events from your Azure resource tooany event handler or endpoint.</span></span>
* <span data-ttu-id="4e632-128">**Filtreleme Gelişmiş** -filtre olay türü veya olay yayımlama yolu tooensure olay işleyicileri yalnızca ilgili olayları alma.</span><span class="sxs-lookup"><span data-stu-id="4e632-128">**Advanced filtering** - Filter on event type or event publish path tooensure event handlers only receive relevant events.</span></span>
* <span data-ttu-id="4e632-129">**Yayma** -birden çok uç noktaları toohello abone aynı olay toosend gerektiğinde bu hello olay tooas birçok yerde kopyalar.</span><span class="sxs-lookup"><span data-stu-id="4e632-129">**Fan-out** - Subscribe multiple endpoints toohello same event toosend copies of hello event tooas many places as needed.</span></span>
* <span data-ttu-id="4e632-130">**Güvenilirlik** -olayları teslim edilir üstel geri alma tooensure 24 saatlik Denemeyle kullanma.</span><span class="sxs-lookup"><span data-stu-id="4e632-130">**Reliability** - Utilize 24-hour retry with exponential backoff tooensure events are delivered.</span></span>
* <span data-ttu-id="4e632-131">**Olay başına ödeme** - ödeme yalnızca hello tutarı için olay kılavuzunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="4e632-131">**Pay-per-event** - Pay only for hello amount you use Event Grid.</span></span>
* <span data-ttu-id="4e632-132">**Yüksek verimlilik** -yapı yüksek hacimli iş yükleri üzerinde olay kılavuz saniye başına milyonlarca olayı desteği.</span><span class="sxs-lookup"><span data-stu-id="4e632-132">**High throughput** - Build high-volume workloads on Event Grid with support for millions of events per second.</span></span>
* <span data-ttu-id="4e632-133">**Yerleşik olayları** - hale getirmek ve hızlı bir şekilde kaynak tanımlanan yerleşik olaylar ile çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="4e632-133">**Built-in Events** - Get up and running quickly with resource-defined built-in events.</span></span>
* <span data-ttu-id="4e632-134">**Özel olaylar** -olay kılavuz rota, filtre ve güvenilir bir şekilde teslim özel olaylar uygulamanızda kullanın.</span><span class="sxs-lookup"><span data-stu-id="4e632-134">**Custom Events** - use Event Grid route, filter, and reliably deliver custom events in your app.</span></span>

## <a name="built-in-publisher-and-handler-integration"></a><span data-ttu-id="4e632-135">Yerleşik yayımcı ve işleyici ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="4e632-135">Built-in publisher and handler integration</span></span>

<span data-ttu-id="4e632-136">Azure Yayımcılar ve işleyicileri dahil olmak üzere çok sayıda hizmetlerini kullanarak yerleşik olay destek sunar.</span><span class="sxs-lookup"><span data-stu-id="4e632-136">Azure offers built-in event support using numerous services, including both publishers and handlers.</span></span>

### <a name="publishers"></a><span data-ttu-id="4e632-137">Yayımcılar</span><span class="sxs-lookup"><span data-stu-id="4e632-137">Publishers</span></span>

<span data-ttu-id="4e632-138">Şu anda hello aşağıdaki Azure hizmetlerinin yerleşik yayımcı için destek olay kılavuz vardır:</span><span class="sxs-lookup"><span data-stu-id="4e632-138">Currently, hello following Azure services have built-in publisher support for event grid:</span></span>

* <span data-ttu-id="4e632-139">Kaynak grupları (yönetim işlemlerini)</span><span class="sxs-lookup"><span data-stu-id="4e632-139">Resource Groups (management operations)</span></span>
* <span data-ttu-id="4e632-140">Azure abonelikleri (yönetim işlemlerini)</span><span class="sxs-lookup"><span data-stu-id="4e632-140">Azure Subscriptions (management operations)</span></span>
* <span data-ttu-id="4e632-141">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="4e632-141">Event Hubs</span></span>
* <span data-ttu-id="4e632-142">Özel konular</span><span class="sxs-lookup"><span data-stu-id="4e632-142">Custom Topics</span></span>

<span data-ttu-id="4e632-143">Diğer Azure hizmetleriyle bu yıl eklenir.</span><span class="sxs-lookup"><span data-stu-id="4e632-143">Other Azure services will be added this year.</span></span>

### <a name="handlers"></a><span data-ttu-id="4e632-144">İşleyicileri</span><span class="sxs-lookup"><span data-stu-id="4e632-144">Handlers</span></span>

<span data-ttu-id="4e632-145">Şu anda hello aşağıdaki Azure hizmetlerinin yerleşik işleyicisi için destek olay kılavuz vardır:</span><span class="sxs-lookup"><span data-stu-id="4e632-145">Currently, hello following Azure services have built-in handler support for Event Grid:</span></span> 

* <span data-ttu-id="4e632-146">Azure İşlevleri</span><span class="sxs-lookup"><span data-stu-id="4e632-146">Azure Functions</span></span>
* <span data-ttu-id="4e632-147">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="4e632-147">Logic Apps</span></span>
* <span data-ttu-id="4e632-148">Azure Otomasyonu</span><span class="sxs-lookup"><span data-stu-id="4e632-148">Azure Automation</span></span>
* <span data-ttu-id="4e632-149">Web kancaları</span><span class="sxs-lookup"><span data-stu-id="4e632-149">WebHooks</span></span>

<span data-ttu-id="4e632-150">Diğer Azure hizmetleriyle bu yıl eklenir.</span><span class="sxs-lookup"><span data-stu-id="4e632-150">Other Azure services will be added this year.</span></span>

## <a name="what-can-i-do-with-event-grid"></a><span data-ttu-id="4e632-151">Olay kılavuzla ne yapabilirim?</span><span class="sxs-lookup"><span data-stu-id="4e632-151">What can I do with Event Grid?</span></span>

<span data-ttu-id="4e632-152">Azure olay kılavuz birkaç çok sunucusuz artırmak özellikleri, ops otomasyon ve tümleştirme çalışma sağlar:</span><span class="sxs-lookup"><span data-stu-id="4e632-152">Azure Event Grid provides several capabilities that vastly improve serverless, ops automation, and integration work:</span></span> 

### <a name="serverless-application-architectures"></a><span data-ttu-id="4e632-153">Sunucusuz uygulama mimarileri</span><span class="sxs-lookup"><span data-stu-id="4e632-153">Serverless application architectures</span></span>

![Sunucusuz bir uygulama](./media/overview/serverless_web_app.png)

<span data-ttu-id="4e632-155">Event Grid, veri kaynaklarını ve olay işleyicilerini bağlar.</span><span class="sxs-lookup"><span data-stu-id="4e632-155">Event Grid connects data sources and event handlers.</span></span> <span data-ttu-id="4e632-156">Örneğin, olay kılavuz tooinstantly tetikleyici her zaman yeni bir fotoğraf tooa blob depolama kapsayıcısını eklenen sunucusuz işlevi toorun görüntü analiz kullanın.</span><span class="sxs-lookup"><span data-stu-id="4e632-156">For example, use Event Grid tooinstantly trigger a serverless function toorun image analysis each time a new photo is added tooa blob storage container.</span></span> 

### <a name="ops-automation"></a><span data-ttu-id="4e632-157">OPS Otomasyon</span><span class="sxs-lookup"><span data-stu-id="4e632-157">Ops Automation</span></span>

![Ops otomasyonu](./media/overview/Ops_automation.png)

<span data-ttu-id="4e632-159">Olay kılavuz toospeed Otomasyon sağlar ve ilke zorlama basitleştirin.</span><span class="sxs-lookup"><span data-stu-id="4e632-159">Event Grid allows you toospeed automation and simplify policy enforcement.</span></span> <span data-ttu-id="4e632-160">Örneğin Event Grid, sanal makine oluşturulduğunda veya SQL Veritabanı hazırlandığında Azure Otomasyonu’na bilgi verebilir.</span><span class="sxs-lookup"><span data-stu-id="4e632-160">For example, Event Grid can notify Azure Automation when a virtual machine is created, or a SQL Database is spun up.</span></span> <span data-ttu-id="4e632-161">Bu olaylar kullanılabilir tooautomatically meta veri işlemleri araçları, etiket sanal makineler ya da dosya iş öğeleri yerleştirin, hizmet yapılandırması uyumlu olduğunu denetleyin.</span><span class="sxs-lookup"><span data-stu-id="4e632-161">These events can be used tooautomatically check that service configurations are compliant, put metadata into operations tools, tag virtual machines, or file work items.</span></span>

### <a name="application-integration"></a><span data-ttu-id="4e632-162">Uygulama tümleştirme</span><span class="sxs-lookup"><span data-stu-id="4e632-162">Application integration</span></span>

![Uygulama tümleştirme](./media/overview/app_integration.png)

<span data-ttu-id="4e632-164">Event Grid, uygulamanızı diğer hizmetlerle bağlar.</span><span class="sxs-lookup"><span data-stu-id="4e632-164">Event Grid connects your app with other services.</span></span> <span data-ttu-id="4e632-165">Örneğin, uygulamanızın olay verileri tooEvent kılavuz, bir özel konu toosend oluşturun ve yönlendirme, Gelişmiş, güvenilir teslim yararlanmak ve Azure ile tümleştirme doğrudan.</span><span class="sxs-lookup"><span data-stu-id="4e632-165">For example, create a custom topic toosend your app's event data tooEvent Grid, and take advantage of its reliable delivery, advanced routing, and direct integration with Azure.</span></span> <span data-ttu-id="4e632-166">Alternatif olarak, kod yazmadan herhangi bir yere, Logic Apps tooprocess verilerle olay kılavuzunu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4e632-166">Alternatively, you can use Event Grid with Logic Apps tooprocess data anywhere, without writing code.</span></span> 

## <a name="how-is-event-grid-different-from-other-azure-integration-services"></a><span data-ttu-id="4e632-167">Olay kılavuz Azure tümleştirme hizmetlerinden farklı mı?</span><span class="sxs-lookup"><span data-stu-id="4e632-167">How is Event Grid different from other Azure integration services?</span></span>

<span data-ttu-id="4e632-168">Olay kılavuz olay denetimli, geriye dönük programlama sağlayan bir olay devre kartı ' dir.</span><span class="sxs-lookup"><span data-stu-id="4e632-168">Event Grid is an eventing backplane that enables event-driven, reactive programming.</span></span> <span data-ttu-id="4e632-169">Azure Hizmetleri ile son derece tümleşiktir ve üçüncü taraf hizmetleri ile tümleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="4e632-169">It is deeply integrated with Azure services and can be integrated with third-party services.</span></span> <span data-ttu-id="4e632-170">Merhaba olay iletisi tooreact toochanges Hizmetleri ve uygulamaları gereksinim hello bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="4e632-170">hello event message contains hello information you need tooreact toochanges in services and applications.</span></span> <span data-ttu-id="4e632-171">Olay kılavuz veri ardışık değil ve güncelleştirildi hello gerçek nesne dağıtmaz.</span><span class="sxs-lookup"><span data-stu-id="4e632-171">Event Grid is not a data pipeline, and does not deliver hello actual object that was updated.</span></span>

<span data-ttu-id="4e632-172">Hizmet veri yolu işlemleri, sıralama, yinelenen algılama ve anlık tutarlılığı gerektiren geleneksel kurumsal uygulamalar için uygundur.</span><span class="sxs-lookup"><span data-stu-id="4e632-172">Service Bus is well suited for traditional enterprise applications that require transactions, ordering, duplicate detection, and instantaneous consistency.</span></span> <span data-ttu-id="4e632-173">Olay kılavuz hızı, Ölçek, tekliflerden için tasarlanmış ve düşük maliyetli bir reaktif modeldeki ' dir.</span><span class="sxs-lookup"><span data-stu-id="4e632-173">Event Grid is designed for speed, scale, breadth, and low cost in a reactive model.</span></span> <span data-ttu-id="4e632-174">Uygun tooserverless mimarisidir.</span><span class="sxs-lookup"><span data-stu-id="4e632-174">It is well suited tooserverless architecture.</span></span>

<span data-ttu-id="4e632-175">Olay kılavuz Logic Apps ve Event Hubs gibi diğer Azure hizmetleriyle tamamlar.</span><span class="sxs-lookup"><span data-stu-id="4e632-175">Event Grid complements other Azure services like Logic Apps and Event Hubs.</span></span> <span data-ttu-id="4e632-176">Olay kılavuz tetikleyicileri, iş akışı mantığı uygulama toobegin hello.</span><span class="sxs-lookup"><span data-stu-id="4e632-176">Event Grid triggers hello logic app toobegin its workflow.</span></span> <span data-ttu-id="4e632-177">Event Hubs olay hub'ları yakalamak ve yapı veri giriş ve dönüştürme ardışık tooreact tooevents etkinleştirerek olay kılavuz ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="4e632-177">Event Hubs works with Event Grid by enabling you tooreact tooevents from Event Hubs Capture, and build data ingress and transformation pipelines.</span></span>

## <a name="how-much-does-event-grid-cost"></a><span data-ttu-id="4e632-178">Nasıl olay kılavuz maliyeti nedir?</span><span class="sxs-lookup"><span data-stu-id="4e632-178">How much does Event Grid cost?</span></span>

<span data-ttu-id="4e632-179">Azure olay kılavuz bir olay başına ödeme fiyatlandırma modelini kullanır, bu nedenle, yalnızca, kullanım için ücret ödersiniz.</span><span class="sxs-lookup"><span data-stu-id="4e632-179">Azure Event Grid uses a pay-per-event pricing model, so you only pay for what you use.</span></span>

<span data-ttu-id="4e632-180">0.60 milyon işlemleri ($0.30 Önizleme sırasında) başına olay kılavuz maliyetleri ve hello ayda ilk 100.000 işlemi boş.</span><span class="sxs-lookup"><span data-stu-id="4e632-180">Event Grid costs $0.60 per million operations ($0.30 during preview) and hello first 100,000 operation per month are free.</span></span> <span data-ttu-id="4e632-181">İşlem eşleştirme, teslim girişimi ve yönetim çağrıları Gelişmiş olay giriş tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="4e632-181">Operations are defined as event ingress, advanced match, delivery attempt, and management calls.</span></span>  <span data-ttu-id="4e632-182">Merhaba hakkında daha fazla ayrıntı bulunabilir [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/event-grid/).</span><span class="sxs-lookup"><span data-stu-id="4e632-182">More details can be found on hello [pricing page](https://azure.microsoft.com/pricing/details/event-grid/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e632-183">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4e632-183">Next steps</span></span>

* <span data-ttu-id="4e632-184">[Oluşturun ve toocustom olayları abone](custom-event-quickstart.md) atlama sağ ve hello Azure olay kılavuz quickstart kullanarak kendi özel olaylar tooany uç noktasını göndermeye başlayın.</span><span class="sxs-lookup"><span data-stu-id="4e632-184">[Create and subscribe toocustom events](custom-event-quickstart.md) Jump right in and start sending your own custom events tooany endpoint using hello Azure Event Grid quickstart.</span></span>
* <span data-ttu-id="4e632-185">[Logic Apps olay işleyici kullanarak](monitor-virtual-machine-changes-event-grid-logic-app.md) Logic Apps tooreact tooevents kullanarak bir uygulama oluşturmaya üzerinde bir öğretici olay kılavuz tarafından gönderilir.</span><span class="sxs-lookup"><span data-stu-id="4e632-185">[Using Logic Apps as an Event Handler](monitor-virtual-machine-changes-event-grid-logic-app.md) A tutorial on building an app using Logic Apps tooreact tooevents pushed by Event Grid.</span></span>
* [<span data-ttu-id="4e632-186">Olay kılavuz REST API Başvurusu</span><span class="sxs-lookup"><span data-stu-id="4e632-186">Event Grid REST API reference</span></span>](/rest/api/eventgrid)  
  <span data-ttu-id="4e632-187">Olay Aboneliklerini yönetmek için Azure olay kılavuz hello hakkında daha fazla teknik bilgi ve bir başvuru sağlar Yönlendirme ve filtreleme.</span><span class="sxs-lookup"><span data-stu-id="4e632-187">Provides more technical information about hello Azure Event Grid, and a reference for managing Event Subscriptions, routing, and filtering.</span></span>
