---
title: "aaaHow toolog olayları tooAzure olay hub'ları Azure API Management | Microsoft Docs"
description: "Bilgi nasıl toolog olayları tooAzure olay hub'ları Azure API Management'te."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 88f6507d-7460-4eb2-bffd-76025b73f8c4
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 09ca65fc48a874467c6662858f7594e9b19fcdb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toolog-events-tooazure-event-hubs-in-azure-api-management"></a><span data-ttu-id="d4149-103">Nasıl toolog olayları tooAzure Azure API Management olay hub'ları</span><span class="sxs-lookup"><span data-stu-id="d4149-103">How toolog events tooAzure Event Hubs in Azure API Management</span></span>
<span data-ttu-id="d4149-104">Azure Event Hubs işleme ve veri bağlı cihazlarınız ve uygulamalarınız tarafından üretilen oldukça büyük miktardaki hello çözümlemek ve böylece saniye başına milyonlarca olayı işleyebilen bir yüksek düzeyde ölçeklenebilir veri alım sistemidir.</span><span class="sxs-lookup"><span data-stu-id="d4149-104">Azure Event Hubs is a highly scalable data ingress service that can ingest millions of events per second so that you can process and analyze hello massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="d4149-105">Olay hub'ları hello bir olay komut zincirinin "ön kapı" olarak görev yapan ve veriler bir event hub'ına toplandıktan sonra dönüştürülebilir ve tüm gerçek zamanlı analiz sağlayıcısı veya toplu işlem/depolama bağdaştırıcısı kullanılarak saklanır.</span><span class="sxs-lookup"><span data-stu-id="d4149-105">Event Hubs acts as hello "front door" for an event pipeline, and once data is collected into an event hub, it can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="d4149-106">Olay hub'ları, böylece olay tüketicileri hello olayları kendi zamanlamalarında erişebilir hello üretim hello üretimini ilgili olayların olay akışının ayırır.</span><span class="sxs-lookup"><span data-stu-id="d4149-106">Event Hubs decouples hello production of a stream of events from hello consumption of those events, so that event consumers can access hello events on their own schedule.</span></span>

<span data-ttu-id="d4149-107">Bu makalede yardımcı toohello olan [olay hub'ları ile Azure API Management tümleştirmek](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) video ve açıklar nasıl Azure Event Hubs kullanan toolog API Management olayları.</span><span class="sxs-lookup"><span data-stu-id="d4149-107">This article is a companion toohello [Integrate Azure API Management with Event Hubs](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) video and describes how toolog API Management events using Azure Event Hubs.</span></span>

## <a name="create-an-azure-event-hub"></a><span data-ttu-id="d4149-108">Bir Azure olay hub'ı Oluştur</span><span class="sxs-lookup"><span data-stu-id="d4149-108">Create an Azure Event Hub</span></span>
<span data-ttu-id="d4149-109">Yeni bir olay Hub, oturum açma toohello toocreate [Klasik Azure portalı](https://manage.windowsazure.com) tıklatıp **yeni**->**uygulama hizmetleri**->**hizmet veri yolu**  -> **Olay hub'ı**->**hızlı Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="d4149-109">toocreate a new Event Hub, sign-in toohello [Azure classic portal](https://manage.windowsazure.com) and click **New**->**App Services**->**Service Bus**->**Event Hub**->**Quick Create**.</span></span> <span data-ttu-id="d4149-110">Bir olay hub'ı adını girin, bölge, bir abonelik seçin ve bir ad seçin.</span><span class="sxs-lookup"><span data-stu-id="d4149-110">Enter an Event Hub name, region, select a subscription, and select a namespace.</span></span> <span data-ttu-id="d4149-111">Daha önce bir ad alanı oluşturmadıysanız hello bir ad yazarak bir tane oluşturabilirsiniz **Namespace** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="d4149-111">If you haven't previously created a namespace you can create one by typing a name in hello **Namespace** textbox.</span></span> <span data-ttu-id="d4149-112">Tüm özellikleri yapılandırıldıktan sonra tıklatın **yeni bir olay hub'ı oluşturma** toocreate hello olay hub'ı.</span><span class="sxs-lookup"><span data-stu-id="d4149-112">Once all properties are configured, click **Create a new Event Hub** toocreate hello Event Hub.</span></span>

![Olay hub'ı Oluştur][create-event-hub]

<span data-ttu-id="d4149-114">Ardından, toohello gidin **yapılandırma** sekmesinde yeni olay hub'ınız için ve iki oluşturmak **paylaşılan erişim ilkeleri**.</span><span class="sxs-lookup"><span data-stu-id="d4149-114">Next, navigate toohello **Configure** tab for your new Event Hub and create two **shared access policies**.</span></span> <span data-ttu-id="d4149-115">Birinci hello ad **gönderme** ve verin **Gönder** izinleri.</span><span class="sxs-lookup"><span data-stu-id="d4149-115">Name hello first one **Sending** and give it **Send** permissions.</span></span>

![Gönderme İlkesi][sending-policy]

<span data-ttu-id="d4149-117">Merhaba ikinci bir ad **alma**, bu verin **dinleme** izinleri ve tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="d4149-117">Name hello second one **Receiving**, give it **Listen** permissions, and click **Save**.</span></span>

![İlke alma][receiving-policy]

<span data-ttu-id="d4149-119">Her paylaşılan erişim ilkesinin uygulamaları toosend sağlar ve olayları tooand hello Event Hub ' alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d4149-119">Each shared access policy allows applications toosend and receive events tooand from hello Event Hub.</span></span> <span data-ttu-id="d4149-120">Bu ilkeler için tooaccess hello bağlantı dizelerini gidin toohello **Pano** sekmesini hello olay hub'ı tıklatın ve **bağlantı bilgilerini**.</span><span class="sxs-lookup"><span data-stu-id="d4149-120">tooaccess hello connection strings for these policies, navigate toohello **Dashboard** tab of hello Event Hub and click **Connection information**.</span></span>

![Bağlantı dizesi][event-hub-dashboard]

<span data-ttu-id="d4149-122">Merhaba **gönderme** bağlantı dizesi, olaylar, oturum açarken kullanılır ve hello **alma** bağlantı dizesi, olayların Event Hub'hello indirirken kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d4149-122">hello **Sending** connection string is used when logging events, and hello **Receiving** connection string is used when downloading events from hello Event Hub.</span></span>

![Bağlantı dizesi][event-hub-connection-string]

## <a name="create-an-api-management-logger"></a><span data-ttu-id="d4149-124">Bir API Management Günlükçü oluşturma</span><span class="sxs-lookup"><span data-stu-id="d4149-124">Create an API Management logger</span></span>
<span data-ttu-id="d4149-125">Bir Event Hub sahip olduğunuza göre hello sonraki tooconfigure adımdır bir [Günlükçü](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) , API Management hizmeti olayları toohello olay hub'ı oturum açabilir.</span><span class="sxs-lookup"><span data-stu-id="d4149-125">Now that you have an Event Hub, hello next step is tooconfigure a [Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) in your API Management service so that it can log events toohello Event Hub.</span></span>

<span data-ttu-id="d4149-126">API Management günlükçüleri hello kullanarak yapılandırılır [API Management REST API](http://aka.ms/smapi).</span><span class="sxs-lookup"><span data-stu-id="d4149-126">API Management loggers are configured using hello [API Management REST API](http://aka.ms/smapi).</span></span> <span data-ttu-id="d4149-127">Merhaba REST API için hello ilk kez kullanmadan önce hello gözden [Önkoşullar](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites) ve olduğundan emin olun [erişim toohello REST API etkin](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI).</span><span class="sxs-lookup"><span data-stu-id="d4149-127">Before using hello REST API for hello first time, review hello [prerequisites](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites) and ensure that you have [enabled access toohello REST API](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI).</span></span>

<span data-ttu-id="d4149-128">toocreate bir Günlükçü URL şablon aşağıdaki hello kullanarak bir HTTP PUT İsteği olun.</span><span class="sxs-lookup"><span data-stu-id="d4149-128">toocreate a logger, make an HTTP PUT request using hello following URL template.</span></span>

`https://{your service}.management.azure-api.net/loggers/{new logger name}?api-version=2014-02-14-preview`

* <span data-ttu-id="d4149-129">Değiştir `{your service}` API Management hizmet örneğinizin hello adı.</span><span class="sxs-lookup"><span data-stu-id="d4149-129">Replace `{your service}` with hello name of your API Management service instance.</span></span>
* <span data-ttu-id="d4149-130">Değiştir `{new logger name}` yeni Günlükçü için hello istenen adda.</span><span class="sxs-lookup"><span data-stu-id="d4149-130">Replace `{new logger name}` with hello desired name for your new logger.</span></span> <span data-ttu-id="d4149-131">Merhaba yapılandırdığınızda bu adı başvurur [günlük eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) İlkesi</span><span class="sxs-lookup"><span data-stu-id="d4149-131">You will reference this name when you configure hello [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) policy</span></span>

<span data-ttu-id="d4149-132">Üstbilgileri toohello isteği aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d4149-132">Add hello following headers toohello request.</span></span>

* <span data-ttu-id="d4149-133">Content-Type: uygulama/json</span><span class="sxs-lookup"><span data-stu-id="d4149-133">Content-Type : application/json</span></span>
* <span data-ttu-id="d4149-134">Yetkilendirme: SharedAccessSignature 58...</span><span class="sxs-lookup"><span data-stu-id="d4149-134">Authorization : SharedAccessSignature 58...</span></span>
  * <span data-ttu-id="d4149-135">Merhaba oluşturma yönergeleri için `SharedAccessSignature` bkz [Azure API Management REST API kimlik doğrulama](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication).</span><span class="sxs-lookup"><span data-stu-id="d4149-135">For instructions on generating hello `SharedAccessSignature` see [Azure API Management REST API Authentication](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication).</span></span>

<span data-ttu-id="d4149-136">Şablon aşağıdaki hello kullanarak hello istek gövdesini belirtin.</span><span class="sxs-lookup"><span data-stu-id="d4149-136">Specify hello request body using hello following template.</span></span>

```json
{
  "type" : "AzureEventHub",
  "description" : "Sample logger description",
  "credentials" : {
    "name" : "Name of hello Event Hub from hello Azure Classic Portal",
    "connectionString" : "Endpoint=Event Hub Sender connection string"
    }
}
```

* <span data-ttu-id="d4149-137">`type`çok ayarlanmalıdır`AzureEventHub`.</span><span class="sxs-lookup"><span data-stu-id="d4149-137">`type` must be set too`AzureEventHub`.</span></span>
* <span data-ttu-id="d4149-138">`description`Merhaba Günlükçü isteğe bağlı bir açıklama sağlar ve isterseniz sıfır uzunluğunda bir dize olabilir.</span><span class="sxs-lookup"><span data-stu-id="d4149-138">`description` provides an optional description of hello logger and can be a zero length string if desired.</span></span>
* <span data-ttu-id="d4149-139">`credentials`Merhaba içeren `name` ve `connectionString` Azure olay hub'ınızın.</span><span class="sxs-lookup"><span data-stu-id="d4149-139">`credentials` contains hello `name` and `connectionString` of your Azure Event Hub.</span></span>

<span data-ttu-id="d4149-140">Yaptığınızda hello isteği durum kodu hello Günlükçü oluşturduysanız `201 Created` döndürülür.</span><span class="sxs-lookup"><span data-stu-id="d4149-140">When you make hello request, if hello logger is created a status code of `201 Created` is returned.</span></span>

> [!NOTE]
> <span data-ttu-id="d4149-141">Diğer olası dönüş kodları ve bunların nedenleri için bkz: [Günlükçü oluşturma](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT).</span><span class="sxs-lookup"><span data-stu-id="d4149-141">For other possible return codes and their reasons, see [Create a Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT).</span></span> <span data-ttu-id="d4149-142">toosee listesi, güncelleştirme ve silme, hello bkz gibi diğer işlemlerin nasıl gerçekleştirmek [Günlükçü](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) varlık belgeleri.</span><span class="sxs-lookup"><span data-stu-id="d4149-142">toosee how perform other operations such as list, update, and delete, see hello [Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) entity documentation.</span></span>
>
>

## <a name="configure-log-to-eventhubs-policies"></a><span data-ttu-id="d4149-143">Günlük eventhubs ilkeleri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d4149-143">Configure log-to-eventhubs policies</span></span>
<span data-ttu-id="d4149-144">API Management'te, Günlükçü yapılandırıldıktan sonra günlük eventhubs ilkeleri toolog istenen hello olayları yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d4149-144">Once your logger is configured in API Management, you can configure your log-to-eventhubs policies toolog hello desired events.</span></span> <span data-ttu-id="d4149-145">Merhaba günlük eventhubs İlkesi ya da hello kullanılabilir gelen İlkesi bölümüne veya hello giden ilke bölümü.</span><span class="sxs-lookup"><span data-stu-id="d4149-145">hello log-to-eventhubs policy can be used in either hello inbound policy section or hello outbound policy section.</span></span>

<span data-ttu-id="d4149-146">tooconfigure ilkeleri, oturum açma toohello [Azure portal](https://portal.azure.com)tooyour API Management hizmeti gidin ve tıklayın **yayımcı portalına** tooaccess hello yayımcı portalı.</span><span class="sxs-lookup"><span data-stu-id="d4149-146">tooconfigure policies, sign-in toohello [Azure portal](https://portal.azure.com), navigate tooyour API Management service, and click **Publisher portal** tooaccess hello publisher portal.</span></span>

![Yayımcı portalı][publisher-portal]

<span data-ttu-id="d4149-148">Tıklatın **ilkeleri** hello API Management menüde hello soldaki hello istenen ürün ve API seçin ve tıklatın **ilke Ekle**.</span><span class="sxs-lookup"><span data-stu-id="d4149-148">Click **Policies** in hello API Management menu on hello left, select hello desired product and API, and click **Add policy**.</span></span> <span data-ttu-id="d4149-149">Bu örnekte, biz İlkesi toohello ekleyeceğiniz **Echo API'si** hello içinde **sınırsız** ürün.</span><span class="sxs-lookup"><span data-stu-id="d4149-149">In this example we're adding a policy toohello **Echo API** in hello **Unlimited** product.</span></span>

![İlke ekleme][add-policy]

<span data-ttu-id="d4149-151">Hello imleç Konumlandır `inbound` İlkesi hello'ye tıklayın **günlük tooEventHub** İlkesi tooinsert hello `log-to-eventhub` ilke deyimi şablonu.</span><span class="sxs-lookup"><span data-stu-id="d4149-151">Position your cursor in hello `inbound` policy section and click hello **Log tooEventHub** policy tooinsert hello `log-to-eventhub` policy statement template.</span></span>

![İlke düzenleyicisi][event-hub-policy]

```xml
<log-to-eventhub logger-id ='logger-id'>
  @( string.Join(",", DateTime.UtcNow, context.Deployment.ServiceName, context.RequestId, context.Request.IpAddress, context.Operation.Name))
</log-to-eventhub>
```

<span data-ttu-id="d4149-153">Değiştir `logger-id` hello önceki adımda yapılandırdığınız hello API Management Günlükçü hello adı.</span><span class="sxs-lookup"><span data-stu-id="d4149-153">Replace `logger-id` with hello name of hello API Management logger you configured in hello previous step.</span></span>

<span data-ttu-id="d4149-154">Merhaba hello değeri olarak bir dize döndürür. herhangi bir ifade kullanabileceğiniz `log-to-eventhub` öğesi.</span><span class="sxs-lookup"><span data-stu-id="d4149-154">You can use any expression that returns a string as hello value for hello `log-to-eventhub` element.</span></span> <span data-ttu-id="d4149-155">Bu örnekte, başlangıç tarihi ve saati, hizmet adı, istek kimliği, istek IP adresi ve işlem adı içeren bir dize günlüğe kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="d4149-155">In this example a string containing hello date and time, service name, request id, request ip address, and operation name is logged.</span></span>

<span data-ttu-id="d4149-156">Tıklatın **kaydetmek** toosave hello ilkesi yapılandırması güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="d4149-156">Click **Save** toosave hello updated policy configuration.</span></span> <span data-ttu-id="d4149-157">Kaydedilmeden hemen hello ilkesi etkindir ve olay hub'ı belirlenmiş oturum toohello olaylardır.</span><span class="sxs-lookup"><span data-stu-id="d4149-157">As soon as it is saved hello policy is active and events are logged toohello designated Event Hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d4149-158">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d4149-158">Next steps</span></span>
* <span data-ttu-id="d4149-159">Azure Event Hubs hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="d4149-159">Learn more about Azure Event Hubs</span></span>
  * [<span data-ttu-id="d4149-160">Azure Event Hubs ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="d4149-160">Get started with Azure Event Hubs</span></span>](../event-hubs/event-hubs-c-getstarted-send.md)
  * [<span data-ttu-id="d4149-161">EventProcessorHost bulunan iletiler alma</span><span class="sxs-lookup"><span data-stu-id="d4149-161">Receive messages with EventProcessorHost</span></span>](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [<span data-ttu-id="d4149-162">Event Hubs programlama kılavuzu</span><span class="sxs-lookup"><span data-stu-id="d4149-162">Event Hubs programming guide</span></span>](../event-hubs/event-hubs-programming-guide.md)
* <span data-ttu-id="d4149-163">API Management ve Event Hubs ile tümleştirme hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="d4149-163">Learn more about API Management and Event Hubs integration</span></span>
  * [<span data-ttu-id="d4149-164">Günlükçü varlık başvurusu</span><span class="sxs-lookup"><span data-stu-id="d4149-164">Logger entity reference</span></span>](https://docs.microsoft.com/rest/api/apimanagement/loggers)
  * [<span data-ttu-id="d4149-165">Günlük eventhub ilke başvurusu</span><span class="sxs-lookup"><span data-stu-id="d4149-165">log-to-eventhub policy reference</span></span>](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#log-to-eventhub)
  * [<span data-ttu-id="d4149-166">Azure API Management, olay hub'ları ve Runscope Apı'lerinizi izleme</span><span class="sxs-lookup"><span data-stu-id="d4149-166">Monitor your APIs with Azure API Management, Event Hubs and Runscope</span></span>](api-management-log-to-eventhub-sample.md)    

## <a name="watch-a-video-walkthrough"></a><span data-ttu-id="d4149-167">Bir videosu izleme</span><span class="sxs-lookup"><span data-stu-id="d4149-167">Watch a video walkthrough</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Integrate-Azure-API-Management-with-Event-Hubs/player]
>
>

[publisher-portal]: ./media/api-management-howto-log-event-hubs/publisher-portal.png
[create-event-hub]: ./media/api-management-howto-log-event-hubs/create-event-hub.png
[event-hub-connection-string]: ./media/api-management-howto-log-event-hubs/event-hub-connection-string.png
[event-hub-dashboard]: ./media/api-management-howto-log-event-hubs/event-hub-dashboard.png
[receiving-policy]: ./media/api-management-howto-log-event-hubs/receiving-policy.png
[sending-policy]: ./media/api-management-howto-log-event-hubs/sending-policy.png
[event-hub-policy]: ./media/api-management-howto-log-event-hubs/event-hub-policy.png
[add-policy]: ./media/api-management-howto-log-event-hubs/add-policy.png
