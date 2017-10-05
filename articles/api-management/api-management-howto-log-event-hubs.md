---
title: "Azure Event hubs'a Azure API Management olaylarını günlüğe kaydedecek şekilde nasıl | Microsoft Docs"
description: "Azure Event hubs'a Azure API Management'te olayları günlüğe kaydetme hakkında bilgi edinin."
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
ms.openlocfilehash: a310236179677046ec49930b07cfdffdadc37974
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-log-events-to-azure-event-hubs-in-azure-api-management"></a><span data-ttu-id="2b27b-103">Azure Event hubs'a Azure API Management'te olayları günlüğe kaydetme hakkında</span><span class="sxs-lookup"><span data-stu-id="2b27b-103">How to log events to Azure Event Hubs in Azure API Management</span></span>
<span data-ttu-id="2b27b-104">Azure Event Hubs, bağlı cihazlarınız ve uygulamalarınız tarafından üretilen oldukça büyük miktardaki verileri işleyip analiz edebilmeniz için saniye başına milyonlarca olayı işleyebilen ileri düzeyde ölçeklenebilir bir veri alım sistemidir.</span><span class="sxs-lookup"><span data-stu-id="2b27b-104">Azure Event Hubs is a highly scalable data ingress service that can ingest millions of events per second so that you can process and analyze the massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="2b27b-105">Event Hubs bir olay komut zincirinin "ön kapı" olarak görev yapan ve veriler bir event hub'ına toplandıktan sonra dönüştürülebilir ve tüm gerçek zamanlı analiz sağlayıcısı veya toplu işlem/depolama bağdaştırıcısı kullanılarak saklanır.</span><span class="sxs-lookup"><span data-stu-id="2b27b-105">Event Hubs acts as the "front door" for an event pipeline, and once data is collected into an event hub, it can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="2b27b-106">Event Hubs olay akışı üretimlerini bu olayların tüketilmesinden ayırır, böylece olay tüketicileri olaylara kendi zamanlamalarında erişebilir.</span><span class="sxs-lookup"><span data-stu-id="2b27b-106">Event Hubs decouples the production of a stream of events from the consumption of those events, so that event consumers can access the events on their own schedule.</span></span>

<span data-ttu-id="2b27b-107">Bu makalede bir yardımcı olan [olay hub'ları ile Azure API Management tümleştirmek](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) video ve Azure Event Hubs kullanarak API Management olaylarını günlüğe kaydedecek şekilde açıklar.</span><span class="sxs-lookup"><span data-stu-id="2b27b-107">This article is a companion to the [Integrate Azure API Management with Event Hubs](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) video and describes how to log API Management events using Azure Event Hubs.</span></span>

## <a name="create-an-azure-event-hub"></a><span data-ttu-id="2b27b-108">Bir Azure olay hub'ı Oluştur</span><span class="sxs-lookup"><span data-stu-id="2b27b-108">Create an Azure Event Hub</span></span>
<span data-ttu-id="2b27b-109">Yeni bir olay hub'ı oluşturmak için oturum için açma [Klasik Azure portalı](https://manage.windowsazure.com) tıklatıp **yeni**->**uygulama hizmetleri**->**hizmet veri yolu**  -> **Olay hub'ı**->**hızlı Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="2b27b-109">To create a new Event Hub, sign-in to the [Azure classic portal](https://manage.windowsazure.com) and click **New**->**App Services**->**Service Bus**->**Event Hub**->**Quick Create**.</span></span> <span data-ttu-id="2b27b-110">Bir olay hub'ı adını girin, bölge, bir abonelik seçin ve bir ad seçin.</span><span class="sxs-lookup"><span data-stu-id="2b27b-110">Enter an Event Hub name, region, select a subscription, and select a namespace.</span></span> <span data-ttu-id="2b27b-111">Daha önce bir ad alanı oluşturmadıysanız bir ad yazarak bir tane oluşturabilirsiniz **Namespace** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="2b27b-111">If you haven't previously created a namespace you can create one by typing a name in the **Namespace** textbox.</span></span> <span data-ttu-id="2b27b-112">Tüm özellikleri yapılandırıldıktan sonra tıklatın **yeni bir olay hub'ı oluşturma** olay hub'ı oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="2b27b-112">Once all properties are configured, click **Create a new Event Hub** to create the Event Hub.</span></span>

![Olay hub'ı Oluştur][create-event-hub]

<span data-ttu-id="2b27b-114">Ardından, gitmek **yapılandırma** sekmesinde yeni olay hub'ınız için ve iki oluşturmak **paylaşılan erişim ilkeleri**.</span><span class="sxs-lookup"><span data-stu-id="2b27b-114">Next, navigate to the **Configure** tab for your new Event Hub and create two **shared access policies**.</span></span> <span data-ttu-id="2b27b-115">Adı ilk **gönderme** ve verin **Gönder** izinleri.</span><span class="sxs-lookup"><span data-stu-id="2b27b-115">Name the first one **Sending** and give it **Send** permissions.</span></span>

![Gönderme İlkesi][sending-policy]

<span data-ttu-id="2b27b-117">Ad ikinci **alma**, bu verin **dinleme** izinleri ve tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="2b27b-117">Name the second one **Receiving**, give it **Listen** permissions, and click **Save**.</span></span>

![İlke alma][receiving-policy]

<span data-ttu-id="2b27b-119">Her paylaşılan erişim ilkesinin uygulamaların olayları olay hub'ı gelen ve giden gönderip almasına izin verir.</span><span class="sxs-lookup"><span data-stu-id="2b27b-119">Each shared access policy allows applications to send and receive events to and from the Event Hub.</span></span> <span data-ttu-id="2b27b-120">Bu ilkeler için bağlantı dizelerini erişmek için gidin **Pano** sekmesini tıklatın ve olay hub'ı **bağlantı bilgilerini**.</span><span class="sxs-lookup"><span data-stu-id="2b27b-120">To access the connection strings for these policies, navigate to the **Dashboard** tab of the Event Hub and click **Connection information**.</span></span>

![Bağlantı dizesi][event-hub-dashboard]

<span data-ttu-id="2b27b-122">**Gönderme** bağlantı dizesi, olaylar, oturum açarken kullanılır ve **alma** bağlantı dizesi, olayların Event Hub'ından indirirken kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2b27b-122">The **Sending** connection string is used when logging events, and the **Receiving** connection string is used when downloading events from the Event Hub.</span></span>

![Bağlantı dizesi][event-hub-connection-string]

## <a name="create-an-api-management-logger"></a><span data-ttu-id="2b27b-124">Bir API Management Günlükçü oluşturma</span><span class="sxs-lookup"><span data-stu-id="2b27b-124">Create an API Management logger</span></span>
<span data-ttu-id="2b27b-125">Bir Event Hub sahip olduğunuza göre sonraki adıma yapılandırmaktır bir [Günlükçü](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) , API Management hizmeti bu olayları Event Hub'ına oturum açabilir.</span><span class="sxs-lookup"><span data-stu-id="2b27b-125">Now that you have an Event Hub, the next step is to configure a [Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) in your API Management service so that it can log events to the Event Hub.</span></span>

<span data-ttu-id="2b27b-126">API Management günlükçüleri kullanılarak yapılandırılmış olan [API Management REST API](http://aka.ms/smapi).</span><span class="sxs-lookup"><span data-stu-id="2b27b-126">API Management loggers are configured using the [API Management REST API](http://aka.ms/smapi).</span></span> <span data-ttu-id="2b27b-127">REST API ilk kez kullanmadan önce gözden [Önkoşullar](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites) ve olduğundan emin olun [REST API erişim etkin](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI).</span><span class="sxs-lookup"><span data-stu-id="2b27b-127">Before using the REST API for the first time, review the [prerequisites](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites) and ensure that you have [enabled access to the REST API](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI).</span></span>

<span data-ttu-id="2b27b-128">Günlükçü oluşturmak için aşağıdaki URL şablonu kullanarak bir HTTP PUT isteği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2b27b-128">To create a logger, make an HTTP PUT request using the following URL template.</span></span>

`https://{your service}.management.azure-api.net/loggers/{new logger name}?api-version=2014-02-14-preview`

* <span data-ttu-id="2b27b-129">Değiştir `{your service}` API Management hizmet örneği adı.</span><span class="sxs-lookup"><span data-stu-id="2b27b-129">Replace `{your service}` with the name of your API Management service instance.</span></span>
* <span data-ttu-id="2b27b-130">Değiştir `{new logger name}` yeni Günlükçü için istenen adı ile.</span><span class="sxs-lookup"><span data-stu-id="2b27b-130">Replace `{new logger name}` with the desired name for your new logger.</span></span> <span data-ttu-id="2b27b-131">Yapılandırdığınızda bu adı başvurur [günlük eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) İlkesi</span><span class="sxs-lookup"><span data-stu-id="2b27b-131">You will reference this name when you configure the [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) policy</span></span>

<span data-ttu-id="2b27b-132">Aşağıdaki üst bilgiler isteği ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2b27b-132">Add the following headers to the request.</span></span>

* <span data-ttu-id="2b27b-133">Content-Type: uygulama/json</span><span class="sxs-lookup"><span data-stu-id="2b27b-133">Content-Type : application/json</span></span>
* <span data-ttu-id="2b27b-134">Yetkilendirme: SharedAccessSignature 58...</span><span class="sxs-lookup"><span data-stu-id="2b27b-134">Authorization : SharedAccessSignature 58...</span></span>
  * <span data-ttu-id="2b27b-135">Oluşturma yönergeleri için `SharedAccessSignature` bkz [Azure API Management REST API kimlik doğrulama](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication).</span><span class="sxs-lookup"><span data-stu-id="2b27b-135">For instructions on generating the `SharedAccessSignature` see [Azure API Management REST API Authentication](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication).</span></span>

<span data-ttu-id="2b27b-136">Aşağıdaki şablonu kullanarak istek gövdesini belirtin.</span><span class="sxs-lookup"><span data-stu-id="2b27b-136">Specify the request body using the following template.</span></span>

```json
{
  "type" : "AzureEventHub",
  "description" : "Sample logger description",
  "credentials" : {
    "name" : "Name of the Event Hub from the Azure Classic Portal",
    "connectionString" : "Endpoint=Event Hub Sender connection string"
    }
}
```

* <span data-ttu-id="2b27b-137">`type`ayarlanmalıdır `AzureEventHub`.</span><span class="sxs-lookup"><span data-stu-id="2b27b-137">`type` must be set to `AzureEventHub`.</span></span>
* <span data-ttu-id="2b27b-138">`description`günlükçünün isteğe bağlı bir açıklama sağlar ve isterseniz sıfır uzunluğunda bir dize olabilir.</span><span class="sxs-lookup"><span data-stu-id="2b27b-138">`description` provides an optional description of the logger and can be a zero length string if desired.</span></span>
* <span data-ttu-id="2b27b-139">`credentials`içeren `name` ve `connectionString` Azure olay hub'ınızın.</span><span class="sxs-lookup"><span data-stu-id="2b27b-139">`credentials` contains the `name` and `connectionString` of your Azure Event Hub.</span></span>

<span data-ttu-id="2b27b-140">Yaptığınızda isteği durum kodu Günlükçü oluşturduysanız `201 Created` döndürülür.</span><span class="sxs-lookup"><span data-stu-id="2b27b-140">When you make the request, if the logger is created a status code of `201 Created` is returned.</span></span>

> [!NOTE]
> <span data-ttu-id="2b27b-141">Diğer olası dönüş kodları ve bunların nedenleri için bkz: [Günlükçü oluşturma](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT).</span><span class="sxs-lookup"><span data-stu-id="2b27b-141">For other possible return codes and their reasons, see [Create a Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT).</span></span> <span data-ttu-id="2b27b-142">Görmek için nasıl listesi, güncelleştirme ve silme, bkz: gibi diğer işlemleri [Günlükçü](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) varlık belgeleri.</span><span class="sxs-lookup"><span data-stu-id="2b27b-142">To see how perform other operations such as list, update, and delete, see the [Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) entity documentation.</span></span>
>
>

## <a name="configure-log-to-eventhubs-policies"></a><span data-ttu-id="2b27b-143">Günlük eventhubs ilkeleri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="2b27b-143">Configure log-to-eventhubs policies</span></span>
<span data-ttu-id="2b27b-144">API Management'te, Günlükçü yapılandırıldıktan sonra günlük eventhubs ilkelerinizi istenen olaylarını günlüğe kaydedecek şekilde yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2b27b-144">Once your logger is configured in API Management, you can configure your log-to-eventhubs policies to log the desired events.</span></span> <span data-ttu-id="2b27b-145">Günlük eventhubs ilkesi gelen ilke bölümünü veya giden ilke bölümünü kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="2b27b-145">The log-to-eventhubs policy can be used in either the inbound policy section or the outbound policy section.</span></span>

<span data-ttu-id="2b27b-146">İlkeleri yapılandırmak için oturum için açma [Azure portal](https://portal.azure.com)API Management hizmetiniz gidin ve tıklayın **yayımcı portalına** yayımcı portalına erişmek için.</span><span class="sxs-lookup"><span data-stu-id="2b27b-146">To configure policies, sign-in to the [Azure portal](https://portal.azure.com), navigate to your API Management service, and click **Publisher portal** to access the publisher portal.</span></span>

![Yayımcı portalı][publisher-portal]

<span data-ttu-id="2b27b-148">Tıklatın **ilkeleri** sol API Management menüsünde istenen ürün ve API seçin ve tıklayın **ilke Ekle**.</span><span class="sxs-lookup"><span data-stu-id="2b27b-148">Click **Policies** in the API Management menu on the left, select the desired product and API, and click **Add policy**.</span></span> <span data-ttu-id="2b27b-149">Bu örnekte, biz bir ilkeye eklediğiniz **Echo API'si** içinde **sınırsız** ürün.</span><span class="sxs-lookup"><span data-stu-id="2b27b-149">In this example we're adding a policy to the **Echo API** in the **Unlimited** product.</span></span>

![İlke ekleme][add-policy]

<span data-ttu-id="2b27b-151">İmleç Konumlandır `inbound` İlkesi bölümüne ve tıklatın **EventHub günlüğüne** eklemek için ilke `log-to-eventhub` ilke deyimi şablonu.</span><span class="sxs-lookup"><span data-stu-id="2b27b-151">Position your cursor in the `inbound` policy section and click the **Log to EventHub** policy to insert the `log-to-eventhub` policy statement template.</span></span>

![İlke düzenleyicisi][event-hub-policy]

```xml
<log-to-eventhub logger-id ='logger-id'>
  @( string.Join(",", DateTime.UtcNow, context.Deployment.ServiceName, context.RequestId, context.Request.IpAddress, context.Operation.Name))
</log-to-eventhub>
```

<span data-ttu-id="2b27b-153">Değiştir `logger-id` önceki adımda yapılandırdığınız API Management günlükçü adı.</span><span class="sxs-lookup"><span data-stu-id="2b27b-153">Replace `logger-id` with the name of the API Management logger you configured in the previous step.</span></span>

<span data-ttu-id="2b27b-154">Değeri olarak bir dize döndürür. herhangi bir ifade kullanabileceğiniz `log-to-eventhub` öğesi.</span><span class="sxs-lookup"><span data-stu-id="2b27b-154">You can use any expression that returns a string as the value for the `log-to-eventhub` element.</span></span> <span data-ttu-id="2b27b-155">Bu örnekte, tarih ve saat, hizmet adı, istek kimliği, istek IP adresi ve işlem adı içeren bir dize günlüğe kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="2b27b-155">In this example a string containing the date and time, service name, request id, request ip address, and operation name is logged.</span></span>

<span data-ttu-id="2b27b-156">Tıklatın **kaydetmek** güncelleştirilmiş ilke yapılandırmasını kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="2b27b-156">Click **Save** to save the updated policy configuration.</span></span> <span data-ttu-id="2b27b-157">Kaydedilmeden hemen ilkesi etkindir ve belirlenen olay Hub'ına olayları kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="2b27b-157">As soon as it is saved the policy is active and events are logged to the designated Event Hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b27b-158">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2b27b-158">Next steps</span></span>
* <span data-ttu-id="2b27b-159">Azure Event Hubs hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="2b27b-159">Learn more about Azure Event Hubs</span></span>
  * [<span data-ttu-id="2b27b-160">Azure Event Hubs ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="2b27b-160">Get started with Azure Event Hubs</span></span>](../event-hubs/event-hubs-c-getstarted-send.md)
  * [<span data-ttu-id="2b27b-161">EventProcessorHost bulunan iletiler alma</span><span class="sxs-lookup"><span data-stu-id="2b27b-161">Receive messages with EventProcessorHost</span></span>](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [<span data-ttu-id="2b27b-162">Event Hubs programlama kılavuzu</span><span class="sxs-lookup"><span data-stu-id="2b27b-162">Event Hubs programming guide</span></span>](../event-hubs/event-hubs-programming-guide.md)
* <span data-ttu-id="2b27b-163">API Management ve Event Hubs ile tümleştirme hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="2b27b-163">Learn more about API Management and Event Hubs integration</span></span>
  * [<span data-ttu-id="2b27b-164">Günlükçü varlık başvurusu</span><span class="sxs-lookup"><span data-stu-id="2b27b-164">Logger entity reference</span></span>](https://docs.microsoft.com/rest/api/apimanagement/loggers)
  * [<span data-ttu-id="2b27b-165">Günlük eventhub ilke başvurusu</span><span class="sxs-lookup"><span data-stu-id="2b27b-165">log-to-eventhub policy reference</span></span>](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#log-to-eventhub)
  * [<span data-ttu-id="2b27b-166">Azure API Management, olay hub'ları ve Runscope Apı'lerinizi izleme</span><span class="sxs-lookup"><span data-stu-id="2b27b-166">Monitor your APIs with Azure API Management, Event Hubs and Runscope</span></span>](api-management-log-to-eventhub-sample.md)    

## <a name="watch-a-video-walkthrough"></a><span data-ttu-id="2b27b-167">Bir videosu izleme</span><span class="sxs-lookup"><span data-stu-id="2b27b-167">Watch a video walkthrough</span></span>
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
