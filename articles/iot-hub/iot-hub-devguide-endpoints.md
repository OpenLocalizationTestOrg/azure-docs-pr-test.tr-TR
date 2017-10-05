---
title: "Azure IOT Hub uç noktaları anlama | Microsoft Docs"
description: "Geliştirici Kılavuzu - IOT Hub hakkında başvuru bilgileri aygıt bakan ve hizmeti kullanıma yönelik uç noktalar."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 57ba52ae-19c6-43e4-bc6c-d8a5c2476e95
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 93ada731fe70cf7d294537241f8104c0b89940ed
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="reference---iot-hub-endpoints"></a><span data-ttu-id="b0c6e-103">Başvuru - IOT Hub uç noktaları</span><span class="sxs-lookup"><span data-stu-id="b0c6e-103">Reference - IoT Hub endpoints</span></span>

## <a name="iot-hub-names"></a><span data-ttu-id="b0c6e-104">IOT Hub adları</span><span class="sxs-lookup"><span data-stu-id="b0c6e-104">IoT Hub names</span></span>

<span data-ttu-id="b0c6e-105">Şirket portalı'nda uç noktalarınızı barındıran IOT hub'ı adı bulabilirsiniz **genel bakış** dikey.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-105">You can find the name of the IoT hub that hosts your endpoints in the portal on the **Overview** blade.</span></span> <span data-ttu-id="b0c6e-106">IOT hub'ı DNS adını varsayılan olarak, aşağıdaki gibi görünür: `{your iot hub name}.azure-devices.net`.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-106">By default, the DNS name of an IoT hub looks like: `{your iot hub name}.azure-devices.net`.</span></span>

<span data-ttu-id="b0c6e-107">Azure DNS, IOT hub'ınız için özel bir DNS adı oluşturmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-107">You can use Azure DNS to create a custom DNS name for your IoT hub.</span></span> <span data-ttu-id="b0c6e-108">Daha fazla bilgi için bkz: [bir Azure hizmetini özel etki alanı ayarları sağlamak için Azure DNS'yi](../dns/dns-custom-domain.md#azure-iot).</span><span class="sxs-lookup"><span data-stu-id="b0c6e-108">For more information, see [Use Azure DNS to provide custom domain settings for an Azure service](../dns/dns-custom-domain.md#azure-iot).</span></span>

## <a name="list-of-built-in-iot-hub-endpoints"></a><span data-ttu-id="b0c6e-109">Yerleşik IOT Hub uç noktaları listesi</span><span class="sxs-lookup"><span data-stu-id="b0c6e-109">List of built-in IoT Hub endpoints</span></span>

<span data-ttu-id="b0c6e-110">Azure IOT hub'ı çeşitli aktörler için işlevselliği kullanıma sunan çok kiracılı bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-110">Azure IoT Hub is a multi-tenant service that exposes its functionality to various actors.</span></span> <span data-ttu-id="b0c6e-111">Aşağıdaki diyagramda, IOT hub'ı gösterir çeşitli uç noktalarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-111">The following diagram shows the various endpoints that IoT Hub exposes.</span></span>

![IoT Hub uç noktaları][img-endpoints]

<span data-ttu-id="b0c6e-113">Aşağıdaki listede uç noktalar açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="b0c6e-113">The following list describes the endpoints:</span></span>

* <span data-ttu-id="b0c6e-114">**Kaynak sağlayıcısı**.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-114">**Resource provider**.</span></span> <span data-ttu-id="b0c6e-115">IOT hub'ı kaynak sağlayıcısı kullanıma sunan bir [Azure Resource Manager] [ lnk-arm] arabirimi.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-115">The IoT Hub resource provider exposes an [Azure Resource Manager][lnk-arm] interface.</span></span> <span data-ttu-id="b0c6e-116">Bu arabirim, Azure abonelik sahipleri oluşturun ve IOT hub'ları silin ve IOT hub'ı özelliklerini güncelleştirmek için etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-116">This interface enables Azure subscription owners to create and delete IoT hubs, and to update IoT hub properties.</span></span> <span data-ttu-id="b0c6e-117">IOT hub'ı özelliklerini yöneten [hub düzeyindeki güvenlik ilkeleri][lnk-accesscontrol], cihaz düzeyinde erişim denetimi ve bulut-cihaz ve cihaz bulut Mesajlaşma işlevsel seçeneklerini aksine.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-117">IoT Hub properties govern [hub-level security policies][lnk-accesscontrol], as opposed to device-level access control, and functional options for cloud-to-device and device-to-cloud messaging.</span></span> <span data-ttu-id="b0c6e-118">IOT hub'ı kaynak sağlayıcısı ayrıca sağlar [cihaz kimliklerini verme][lnk-importexport].</span><span class="sxs-lookup"><span data-stu-id="b0c6e-118">The IoT Hub resource provider also enables you to [export device identities][lnk-importexport].</span></span>
* <span data-ttu-id="b0c6e-119">**Cihaz Kimlik Yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-119">**Device identity management**.</span></span> <span data-ttu-id="b0c6e-120">Her IOT hub cihaz kimlikleri yönetmek için HTTP REST uç noktalar kümesi sunar (oluşturma, alma, güncelleştirme ve silme).</span><span class="sxs-lookup"><span data-stu-id="b0c6e-120">Each IoT hub exposes a set of HTTP REST endpoints to manage device identities (create, retrieve, update, and delete).</span></span> <span data-ttu-id="b0c6e-121">[Cihaz kimliklerini] [ lnk-device-identities] cihaz kimlik doğrulaması ve erişim denetimi için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-121">[Device identities][lnk-device-identities] are used for device authentication and access control.</span></span>
* <span data-ttu-id="b0c6e-122">**Cihaz çifti Yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-122">**Device twin management**.</span></span> <span data-ttu-id="b0c6e-123">Her IOT hub'ı sorgu ve güncelleştirme hizmeti dönük HTTP REST uç noktasına kümesi sunan [cihaz çiftlerini] [ lnk-twins] (güncelleştirme etiketleri ve özellikleri).</span><span class="sxs-lookup"><span data-stu-id="b0c6e-123">Each IoT hub exposes a set of service-facing HTTP REST endpoint to query and update [device twins][lnk-twins] (update tags and properties).</span></span>
* <span data-ttu-id="b0c6e-124">**İşlerini Yönetim**.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-124">**Jobs management**.</span></span> <span data-ttu-id="b0c6e-125">Her IOT hub'ı sorgulamak ve yönetmek için hizmet dönük HTTP REST uç nokta kümesi sunan [işleri][lnk-jobs].</span><span class="sxs-lookup"><span data-stu-id="b0c6e-125">Each IoT hub exposes a set of service-facing HTTP REST endpoint to query and manage [jobs][lnk-jobs].</span></span>
* <span data-ttu-id="b0c6e-126">**Cihaz uç noktaları**.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-126">**Device endpoints**.</span></span> <span data-ttu-id="b0c6e-127">IOT Hub kimlik kayıt defterinde her cihaz için uç noktalar kümesi sunar:</span><span class="sxs-lookup"><span data-stu-id="b0c6e-127">For each device in the identity registry, IoT Hub exposes a set of endpoints:</span></span>

  * <span data-ttu-id="b0c6e-128">*Cihaz bulut iletilerini göndermek*.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-128">*Send device-to-cloud messages*.</span></span> <span data-ttu-id="b0c6e-129">Bu uç noktaya bir aygıtın kullandığı [cihaz bulut iletilerini göndermek][lnk-d2c].</span><span class="sxs-lookup"><span data-stu-id="b0c6e-129">A device uses this endpoint to [send device-to-cloud messages][lnk-d2c].</span></span>
  * <span data-ttu-id="b0c6e-130">*Bulut-cihaz iletilerini*.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-130">*Receive cloud-to-device messages*.</span></span> <span data-ttu-id="b0c6e-131">Hedeflenen almak için bu uç noktası bir aygıtı kullandığı [bulut-cihaz iletilerini][lnk-c2d].</span><span class="sxs-lookup"><span data-stu-id="b0c6e-131">A device uses this endpoint to receive targeted [cloud-to-device messages][lnk-c2d].</span></span>
  * <span data-ttu-id="b0c6e-132">*Dosya yüklemeleri başlatmak*.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-132">*Initiate file uploads*.</span></span> <span data-ttu-id="b0c6e-133">Bir cihaz IOT Hub'ına bir Azure depolama SAS URI'sini almak için bu uç nokta kullanır [bir dosyayı karşıya yüklemeyi][lnk-upload].</span><span class="sxs-lookup"><span data-stu-id="b0c6e-133">A device uses this endpoint to receive an Azure Storage SAS URI from IoT Hub to [upload a file][lnk-upload].</span></span>
  * <span data-ttu-id="b0c6e-134">*Alma ve güncelleştirme cihaz çifti özellikleri*.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-134">*Retrieve and update device twin properties*.</span></span> <span data-ttu-id="b0c6e-135">Bir aygıt bu uç nokta erişmek için kullanır. kendi [cihaz çifti][lnk-twins]ait özellikler.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-135">A device uses this endpoint to access its [device twin][lnk-twins]'s properties.</span></span>
  * <span data-ttu-id="b0c6e-136">*Doğrudan yöntemi isteklerini alacak*.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-136">*Receive direct method requests*.</span></span> <span data-ttu-id="b0c6e-137">Bir aygıt bu uç nokta dinlemek için kullanır. [doğrudan yöntemi][lnk-methods]'s istekleri.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-137">A device uses this endpoint to listen for [direct method][lnk-methods]'s requests.</span></span>

    <span data-ttu-id="b0c6e-138">Bu uç noktalar kullanılarak kullanıma sunulan [MQTT v3.1.1][lnk-mqtt], HTTP 1.1 ve [AMQP 1.0] [ lnk-amqp] protokoller.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-138">These endpoints are exposed using [MQTT v3.1.1][lnk-mqtt], HTTP 1.1, and [AMQP 1.0][lnk-amqp] protocols.</span></span> <span data-ttu-id="b0c6e-139">AMQP kullanılabilir ayrıca üzerinden [WebSockets] [ lnk-websockets] bağlantı noktası 443'tür.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-139">AMQP is also available over [WebSockets][lnk-websockets] on port 443.</span></span>

    <span data-ttu-id="b0c6e-140">Yalnızca kullandığınızda cihaz çiftlerini ve yöntemleri uç noktaları kullanılabilir [MQTT v3.1.1] [ lnk-mqtt] protokolü.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-140">The device twins and methods endpoints are available only when you use the [MQTT v3.1.1][lnk-mqtt] protocol.</span></span>

* <span data-ttu-id="b0c6e-141">**Hizmet uç noktaları**.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-141">**Service endpoints**.</span></span> <span data-ttu-id="b0c6e-142">Her IOT hub uç noktaları, aygıtlar ile iletişim kurmak çözüm arka ucunuz için bir dizi kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-142">Each IoT hub exposes a set of endpoints  for your solution back end to communicate with your devices.</span></span> <span data-ttu-id="b0c6e-143">Bunun tek istisnası Bu uç noktalar yalnızca kullanarak gösterilen [AMQP] [ lnk-amqp] protokolü.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-143">With one exception, these endpoints are only exposed using the [AMQP][lnk-amqp] protocol.</span></span> <span data-ttu-id="b0c6e-144">Yöntem çağırma uç noktası HTTP protokolü üzerinden açıktır.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-144">The method invocation endpoint is exposed over the HTTP protocol.</span></span>
  
  * <span data-ttu-id="b0c6e-145">*Cihaz bulut iletilerini*.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-145">*Receive device-to-cloud messages*.</span></span> <span data-ttu-id="b0c6e-146">Bu uç nokta ile uyumlu [Azure Event Hubs][lnk-event-hubs].</span><span class="sxs-lookup"><span data-stu-id="b0c6e-146">This endpoint is compatible with [Azure Event Hubs][lnk-event-hubs].</span></span> <span data-ttu-id="b0c6e-147">Bir arka uç hizmeti okumak için kullanabileceğiniz [cihaz bulut iletilerini] [ lnk-d2c] cihazlar tarafından gönderilen.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-147">A back-end service can use it to read the [device-to-cloud messages][lnk-d2c] sent by your devices.</span></span> <span data-ttu-id="b0c6e-148">Bu yerleşik bir uç nokta ek olarak IOT hub'ınızı özel uç noktaları oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-148">You can create custom endpoints on your IoT hub in addition to this built-in endpoint.</span></span>
  * <span data-ttu-id="b0c6e-149">*Bulut-cihaz iletilerini göndermek ve teslim alındı bildirimleri almak*.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-149">*Send cloud-to-device messages and receive delivery acknowledgments*.</span></span> <span data-ttu-id="b0c6e-150">Bu uç noktalar güvenilir göndermek çözüm arka ucunuz etkinleştirmek [bulut-cihaz iletilerini][lnk-c2d]ve karşılık gelen teslim veya süre sonu bildirimleri almak için.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-150">These endpoints enable your solution back end to send reliable [cloud-to-device messages][lnk-c2d], and to receive the corresponding delivery or expiration acknowledgments.</span></span>
  * <span data-ttu-id="b0c6e-151">*Dosya bildirimlerin*.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-151">*Receive file notifications*.</span></span> <span data-ttu-id="b0c6e-152">Bu ileti uç aygıtlarınızı başarıyla bir dosyayı karşıya yüklediğinizde bildirimlerini almak üzere sağlar.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-152">This messaging endpoint allows you to receive notifications of when your devices successfully upload a file.</span></span> 
  * <span data-ttu-id="b0c6e-153">*Yöntem çağırma doğrudan*.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-153">*Direct method invocation*.</span></span> <span data-ttu-id="b0c6e-154">Bu uç noktaya çağırmak bir arka uç hizmeti sağlayan bir [doğrudan yöntemi] [ lnk-methods] bir aygıtta.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-154">This endpoint allows a back-end service to invoke a [direct method][lnk-methods] on a device.</span></span>
  * <span data-ttu-id="b0c6e-155">*Alma olaylarını izleme işlemleri*.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-155">*Receive operations monitoring events*.</span></span> <span data-ttu-id="b0c6e-156">Bu uç noktayı alma işlemlerinin, IOT hub'ınızı bunları yaymak üzere yapılandırılmışsa, olayları izleme sağlar.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-156">This endpoint allows you to receive operations monitoring events if your IoT hub has been configured to emit them.</span></span> <span data-ttu-id="b0c6e-157">Daha fazla bilgi için bkz: [izleme IOT hub'ı operations][lnk-operations-mon].</span><span class="sxs-lookup"><span data-stu-id="b0c6e-157">For more information, see [IoT Hub operations monitoring][lnk-operations-mon].</span></span>

<span data-ttu-id="b0c6e-158">[Azure IOT SDK'ları] [ lnk-sdks] makalede, bu uç noktalar erişmek için çeşitli yolları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-158">The [Azure IoT SDKs][lnk-sdks] article describes the various ways to access these endpoints.</span></span>

<span data-ttu-id="b0c6e-159">Tüm IOT Hub uç noktaları kullanma [TLS] [ lnk-tls] protokolü ve uç nokta yok şifrelenmemiş ve güvenli kanallar üzerinde gösterilen herhangi bir zamanda.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-159">All IoT Hub endpoints use the [TLS][lnk-tls] protocol, and no endpoint is ever exposed on unencrypted/unsecured channels.</span></span>

## <a name="custom-endpoints"></a><span data-ttu-id="b0c6e-160">Özel uç noktaları</span><span class="sxs-lookup"><span data-stu-id="b0c6e-160">Custom endpoints</span></span>

<span data-ttu-id="b0c6e-161">İleti yönlendirme için uç noktalar olarak hareket edecek, IOT hub'ına aboneliğinizde var olan Azure Hizmetleri bağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-161">You can link existing Azure services in your subscription to your IoT hub to act as endpoints for message routing.</span></span> <span data-ttu-id="b0c6e-162">Bu uç noktalar hizmet uç noktalar olarak hareket ve iç havuzlar ileti yollar için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-162">These endpoints act as service endpoints and are used as sinks for message routes.</span></span> <span data-ttu-id="b0c6e-163">Cihazları doğrudan ek uç noktaları için yazamıyor.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-163">Devices cannot write directly to the additional endpoints.</span></span> <span data-ttu-id="b0c6e-164">İleti yollar hakkında daha fazla bilgi için üzerinde Geliştirici Kılavuzu girişine bakın [IOT hub ile ileti gönderme ve alma][lnk-devguide-messaging].</span><span class="sxs-lookup"><span data-stu-id="b0c6e-164">To learn more about message routes, see the developer guide entry on [sending and receiving messages with IoT hub][lnk-devguide-messaging].</span></span>

<span data-ttu-id="b0c6e-165">IOT Hub aşağıdaki Azure hizmetlerini ek uç noktalar olarak şu anda destekler:</span><span class="sxs-lookup"><span data-stu-id="b0c6e-165">IoT Hub currently supports the following Azure services as additional endpoints:</span></span>

* <span data-ttu-id="b0c6e-166">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="b0c6e-166">Event Hubs</span></span>
* <span data-ttu-id="b0c6e-167">Service Bus Kuyrukları</span><span class="sxs-lookup"><span data-stu-id="b0c6e-167">Service Bus Queues</span></span>
* <span data-ttu-id="b0c6e-168">Service Bus Konuları</span><span class="sxs-lookup"><span data-stu-id="b0c6e-168">Service Bus Topics</span></span>

<span data-ttu-id="b0c6e-169">IOT Hub, ileti yönlendirmesinin çalışması için bu hizmet uç noktaları yazma erişimi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-169">IoT Hub needs write access to these service endpoints for message routing to work.</span></span> <span data-ttu-id="b0c6e-170">Azure Portalı aracılığıyla uç noktalarınızı yapılandırırsanız, sizin için gerekli izinleri eklenir.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-170">If you configure your endpoints through the Azure portal, the necessary permissions are added for you.</span></span> <span data-ttu-id="b0c6e-171">Hizmetlerinizin beklenen verimlilik desteklemek üzere yapılandırdığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-171">Make sure you configure your services to support the expected throughput.</span></span> <span data-ttu-id="b0c6e-172">IOT çözümünüzü ilk yapılandırırken, ek noktalarınızı izlemek ve gerçek yükleme için gerekli ayarlamaları yapmak gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-172">When you first configure your IoT solution, you may need to monitor your additional endpoints and make any necessary adjustments for the actual load.</span></span>

<span data-ttu-id="b0c6e-173">IOT hub'ı ileti Bu uç noktasına tüm aynı uç noktası birden çok yönlendiren bir ileti eşleşirse, yalnızca bir kez sunar.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-173">If a message matches multiple routes that all point to the same endpoint, IoT Hub delivers message to that endpoint only once.</span></span> <span data-ttu-id="b0c6e-174">Bu nedenle, hizmet veri yolu kuyruğu ya da konu yinelenenleri kaldırmayı yapılandırma gerekmez.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-174">Therefore, you do not need to configure deduplication on your Service Bus queue or topic.</span></span> <span data-ttu-id="b0c6e-175">Bölümlenmiş sıralarındaki bölüm benzeşim ileti sıralama güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-175">In partitioned queues, partition affinity guarantees message ordering.</span></span>

> [!NOTE]
> <span data-ttu-id="b0c6e-176">Service Bus kuyrukları ve konularından IOT Hub uç noktaları değil olarak kullanılan **oturumları** veya **yinelenen saptama** etkin.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-176">Service Bus queues and topics used as IoT Hub endpoints must not have **Sessions** or **Duplicate Detection** enabled.</span></span> <span data-ttu-id="b0c6e-177">Bu seçeneklerden birini etkinleştirilmişse, uç nokta olarak görünür **ulaşılamıyor** Azure portalında.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-177">If either of those options are enabled, the endpoint appears as **Unreachable** in the Azure portal.</span></span>

<span data-ttu-id="b0c6e-178">Ekleyebileceğiniz uç noktaların sayısını sınırları için bkz: [kotalar ve azaltma][lnk-devguide-quotas].</span><span class="sxs-lookup"><span data-stu-id="b0c6e-178">For the limits on the number of endpoints you can add, see [Quotas and throttling][lnk-devguide-quotas].</span></span>

## <a name="field-gateways"></a><span data-ttu-id="b0c6e-179">Alan ağ geçitleri</span><span class="sxs-lookup"><span data-stu-id="b0c6e-179">Field gateways</span></span>

<span data-ttu-id="b0c6e-180">Bir IOT çözümündeki bir *alan ağ geçidi* , cihazlarınız ve IOT Hub uç noktaları arasında bulunur.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-180">In an IoT solution, a *field gateway* sits between your devices and your IoT Hub endpoints.</span></span> <span data-ttu-id="b0c6e-181">Aygıtlarınızı yakın genellikle yer alır.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-181">It is typically located close to your devices.</span></span> <span data-ttu-id="b0c6e-182">Aygıtlarınızı, cihazlar tarafından desteklenen bir protokolü kullanarak doğrudan alan ağ geçidi ile iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-182">Your devices communicate directly with the field gateway by using a protocol supported by the devices.</span></span> <span data-ttu-id="b0c6e-183">IOT Hub tarafından desteklenen bir protokolünü kullanarak bir IOT hub'ı uç alan ağ geçidi bağlanır.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-183">The field gateway connects to an IoT Hub endpoint using a protocol that is supported by IoT Hub.</span></span> <span data-ttu-id="b0c6e-184">Bir alan ağ geçidi, adanmış bir donanımsal cihaz veya özel ağ geçidi yazılımını çalıştıran bir düşük güç bilgisayar olabilir.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-184">A field gateway might be a dedicated hardware device or a low-power computer running custom gateway software.</span></span>

<span data-ttu-id="b0c6e-185">Kullanabileceğiniz [Azure IOT kenar] [ lnk-iot-edge] bir alan ağ geçidi uygulamak için.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-185">You can use [Azure IoT Edge][lnk-iot-edge] to implement a field gateway.</span></span> <span data-ttu-id="b0c6e-186">IOT kenar aynı IOT Hub bağlantı üzerine birden çok aygıt çoğullama iletişimlerinden gibi işlevsellikler sunar.</span><span class="sxs-lookup"><span data-stu-id="b0c6e-186">IoT Edge offers functionality such as multiplexing communications from multiple devices onto the same IoT Hub connection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b0c6e-187">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b0c6e-187">Next steps</span></span>

<span data-ttu-id="b0c6e-188">Bu IOT Hub Geliştirici Kılavuzu'ndaki diğer başvuru konuları içerir:</span><span class="sxs-lookup"><span data-stu-id="b0c6e-188">Other reference topics in this IoT Hub developer guide include:</span></span>

* <span data-ttu-id="b0c6e-189">[Cihaz çiftlerini, işler ve ileti yönlendirme için IOT hub'ı sorgulama dili][lnk-devguide-query]</span><span class="sxs-lookup"><span data-stu-id="b0c6e-189">[IoT Hub query language for device twins, jobs, and message routing][lnk-devguide-query]</span></span>
* <span data-ttu-id="b0c6e-190">[Kotalar ve azaltma][lnk-devguide-quotas]</span><span class="sxs-lookup"><span data-stu-id="b0c6e-190">[Quotas and throttling][lnk-devguide-quotas]</span></span>
* <span data-ttu-id="b0c6e-191">[IOT Hub MQTT desteği][lnk-devguide-mqtt]</span><span class="sxs-lookup"><span data-stu-id="b0c6e-191">[IoT Hub MQTT support][lnk-devguide-mqtt]</span></span>

[lnk-iot-edge]: https://github.com/Azure/iot-edge

[img-endpoints]: ./media/iot-hub-devguide-endpoints/endpoints.png
[lnk-amqp]: https://www.amqp.org/
[lnk-mqtt]: http://mqtt.org/
[lnk-websockets]: https://tools.ietf.org/html/rfc6455
[lnk-arm]: ../azure-resource-manager/resource-group-overview.md
[lnk-event-hubs]: http://azure.microsoft.com/documentation/services/event-hubs/

[lnk-tls]: https://tools.ietf.org/html/rfc5246


[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-accesscontrol]: iot-hub-devguide-security.md#access-control-and-permissions
[lnk-importexport]: iot-hub-devguide-identity-registry.md#import-and-export-device-identities
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-device-identities]: iot-hub-devguide-identity-registry.md
[lnk-upload]: iot-hub-devguide-file-upload.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-jobs]: iot-hub-devguide-jobs.md

[lnk-devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
[lnk-operations-mon]: iot-hub-operations-monitoring.md
