---
title: "Azure Event Grid için Özel Olaylar | Microsoft Docs"
description: "Azure Event Grid’i kullanarak bir konu yayımlayın ve o olaya abone olun."
services: event-grid
keywords: 
author: djrosanova
ms.author: darosa
ms.date: 08/15/2017
ms.topic: hero-article
ms.service: event-grid
ms.openlocfilehash: 0290836bebadb20085a3ce84dddc088c3af385da
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-route-custom-events-with-azure-event-grid"></a><span data-ttu-id="015e3-103">Azure Event Grid ile özel olaylar oluşturma ve yönlendirme</span><span class="sxs-lookup"><span data-stu-id="015e3-103">Create and route custom events with Azure Event Grid</span></span>

<span data-ttu-id="015e3-104">Azure Event Grid, bulut için bir olay oluşturma hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="015e3-104">Azure Event Grid is an eventing service for the cloud.</span></span> <span data-ttu-id="015e3-105">Bu makalede, Azure CLI aracını kullanarak özel bir konu oluşturur, konuya abone olur ve sonucu görüntülemek için olayı tetiklersiniz.</span><span class="sxs-lookup"><span data-stu-id="015e3-105">In this article, you use the Azure CLI to create a custom topic, subscribe to the topic, and trigger the event to view the result.</span></span> <span data-ttu-id="015e3-106">Normalde olayları olaya yanıt veren bir uç noktaya (web kancası veya Azure İşlevi gibi) gönderirsiniz.</span><span class="sxs-lookup"><span data-stu-id="015e3-106">Typically, you send events to an endpoint that responds to the event, such as, a webhook or Azure Function.</span></span> <span data-ttu-id="015e3-107">Ancak, bu makaleyi basitleştirmek amacıyla olayları yalnızca iletileri toplayan bir URL’ye gönderirsiniz.</span><span class="sxs-lookup"><span data-stu-id="015e3-107">However, to simplify this article, you send the events to a URL that merely collects the messages.</span></span> <span data-ttu-id="015e3-108">Bu URL’yi [RequestBin](https://requestb.in/) adlı açık kaynak, üçüncü taraf bir aracı kullanarak oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="015e3-108">You create this URL by using an open source, third-party tool called [RequestBin](https://requestb.in/).</span></span>

>[!NOTE]
><span data-ttu-id="015e3-109">**RequestBin** ağır iş yüklerinde kullanım için tasarlanmamış açık kaynaklı bir araçtır.</span><span class="sxs-lookup"><span data-stu-id="015e3-109">**RequestBin** is an open source tool that is not intended for high throughput usage.</span></span> <span data-ttu-id="015e3-110">Burada araç tamamen gösterim amaçlı kullanılmıştır.</span><span class="sxs-lookup"><span data-stu-id="015e3-110">The use of the tool here is purely demonstrative.</span></span> <span data-ttu-id="015e3-111">Aynı anda birden fazla olay gönderirseniz araçta tüm olaylarınızı göremeyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="015e3-111">If you push more than one event at a time, you might not see all of your events in the tool.</span></span>

<span data-ttu-id="015e3-112">İşiniz bittiğinde, olay verilerinin bir uç noktaya gönderildiğini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="015e3-112">When you are finished, you see that the event data has been sent to an endpoint.</span></span>

![Olay verileri](./media/custom-event-quickstart/request-result.png)

[!INCLUDE [quickstarts-free-trial-note.md](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="015e3-114">CLI'yi yerel olarak yükleyip kullanmayı tercih ederseniz bu makale için Azure CLI’nın en son sürümünü (2.0.14 veya sonraki) kullanıyor olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="015e3-114">If you choose to install and use the CLI locally, this article requires that you are running the latest version of Azure CLI (2.0.14 or later).</span></span> <span data-ttu-id="015e3-115">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="015e3-115">To find the version, run `az --version`.</span></span> <span data-ttu-id="015e3-116">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="015e3-116">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="015e3-117">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="015e3-117">Create a resource group</span></span>

<span data-ttu-id="015e3-118">Event Grid konuları Azure kaynaklarıdır ve bir Azure kaynak grubuna yerleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="015e3-118">Event Grid topics are Azure resources, and must be placed in an Azure resource group.</span></span> <span data-ttu-id="015e3-119">Kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal koleksiyondur.</span><span class="sxs-lookup"><span data-stu-id="015e3-119">The resource group is a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="015e3-120">[az group create](/cli/azure/group#create) komutuyla bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="015e3-120">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> 

<span data-ttu-id="015e3-121">Aşağıdaki örnek *westus2* konumunda *gridResourceGroup* adlı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="015e3-121">The following example creates a resource group named *gridResourceGroup* in the *westus2* location.</span></span>

```azurecli-interactive
az group create --name gridResourceGroup --location westus2
```

## <a name="create-a-custom-topic"></a><span data-ttu-id="015e3-122">Özel konu oluşturma</span><span class="sxs-lookup"><span data-stu-id="015e3-122">Create a custom topic</span></span>

<span data-ttu-id="015e3-123">Konu, olaylarınızı gönderdiğiniz kullanıcı tanımlı bir uç nokta sağlar.</span><span class="sxs-lookup"><span data-stu-id="015e3-123">A topic provides a user-defined endpoint that you post your events to.</span></span> <span data-ttu-id="015e3-124">Aşağıdaki örnekte, konu kaynak grubunuzda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="015e3-124">The following example creates the topic in your resource group.</span></span> <span data-ttu-id="015e3-125">`<topic_name>` değerini konunuz için benzersiz bir adla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="015e3-125">Replace `<topic_name>` with a unique name for your topic.</span></span> <span data-ttu-id="015e3-126">Konu adı bir DNS girdisi ile temsil edildiğinden benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="015e3-126">The topic name must be unique because it is represented by a DNS entry.</span></span> <span data-ttu-id="015e3-127">Önizleme sürümü için Event Grid tarafından **westus2** ve **westcentralus** konumları desteklenir.</span><span class="sxs-lookup"><span data-stu-id="015e3-127">For the preview release, Event Grid supports **westus2** and **westcentralus** locations.</span></span>

```azurecli-interactive
az eventgrid topic create --name <topic_name> -l westus2 -g gridResourceGroup
```

## <a name="create-a-message-endpoint"></a><span data-ttu-id="015e3-128">İleti uç noktası oluşturma</span><span class="sxs-lookup"><span data-stu-id="015e3-128">Create a message endpoint</span></span>

<span data-ttu-id="015e3-129">Konuya abone olmadan önce olay iletisi için uç noktayı oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="015e3-129">Before subscribing to the topic, let's create the endpoint for the event message.</span></span> <span data-ttu-id="015e3-130">Konuya yanıt vermek için kod yazmak yerine, görüntüleyebilmeniz için iletileri toplayan bir uç nokta oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="015e3-130">Rather than write code to respond to the event, let's create an endpoint that collects the messages so you can view them.</span></span> <span data-ttu-id="015e3-131">RequestBin, bir uç nokta oluşturmanıza ve buna gönderilen istekleri görüntülemenize imkan tanıyan açık kaynak, üçüncü taraf bir araçtır.</span><span class="sxs-lookup"><span data-stu-id="015e3-131">RequestBin is an open source, third-party tool that enables you to create an endpoint, and view requests that are sent to it.</span></span> <span data-ttu-id="015e3-132">[RequestBin](https://requestb.in/)’e gidip **Create a RequestBin** (RequestBin oluştur) seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="015e3-132">Go to [RequestBin](https://requestb.in/), and click **Create a RequestBin**.</span></span>  <span data-ttu-id="015e3-133">Daha sonra konuya abone olurken gerekecek kutu URL’sini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="015e3-133">Copy the bin URL, because you need it when subscribing to the topic.</span></span>

## <a name="subscribe-to-a-topic"></a><span data-ttu-id="015e3-134">Bir konuya abone olma</span><span class="sxs-lookup"><span data-stu-id="015e3-134">Subscribe to a topic</span></span>

<span data-ttu-id="015e3-135">Event Grid’e hangi olayları izlemek istediğinizi bildirmek için bir konuya abone olursunuz. Aşağıdaki örnek, oluşturduğunuz konuya abone olur ve RequestBin URL’sini olay bildirimi için uç nokta olarak geçirir.</span><span class="sxs-lookup"><span data-stu-id="015e3-135">You subscribe to a topic to tell Event Grid which events you want to track. The following example subscribes to the topic you created, and passes the URL from RequestBin as the endpoint for event notification.</span></span> <span data-ttu-id="015e3-136">`<event_subscription_name>` değerini aboneliğiniz için benzersiz bir adla, `<URL_from_RequestBin>` değerini ise önceki bölümden bir değerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="015e3-136">Replace `<event_subscription_name>` with a unique name for your subscription, and `<URL_from_RequestBin>` with the value from the preceding section.</span></span> <span data-ttu-id="015e3-137">Abone olurken bir uç nokta belirttiğinizde, Event Grid olayların bu uç noktaya yönlendirilmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="015e3-137">By specifying an endpoint when subscribing, Event Grid handles the routing of events to that endpoint.</span></span> <span data-ttu-id="015e3-138">`<topic_name>` için daha önce oluşturduğunuz değeri kullanın.</span><span class="sxs-lookup"><span data-stu-id="015e3-138">For `<topic_name>`, use the value you created earlier.</span></span> 

```azurecli-interactive
az eventgrid topic event-subscription create --name <event_subscription_name> \
  --endpoint <URL_from_RequestBin> \
  -g gridResourceGroup \
  --topic-name <topic_name>
```

## <a name="send-an-event-to-your-topic"></a><span data-ttu-id="015e3-139">Konunuza olay gönderme</span><span class="sxs-lookup"><span data-stu-id="015e3-139">Send an event to your topic</span></span>

<span data-ttu-id="015e3-140">Şimdi, Event Grid’in iletiyi uç noktanıza nasıl dağıttığını görmek için bir olay tetikleyelim.</span><span class="sxs-lookup"><span data-stu-id="015e3-140">Now, let's trigger an event to see how Event Grid distributes the message to your endpoint.</span></span> <span data-ttu-id="015e3-141">İlk olarak konunun URL’sini ve anahtarını alalım.</span><span class="sxs-lookup"><span data-stu-id="015e3-141">First, let's get the URL and key for the topic.</span></span> <span data-ttu-id="015e3-142">Tekrar belirtmek gerekirse, `<topic_name>` için kendi konu adınızı kullanın.</span><span class="sxs-lookup"><span data-stu-id="015e3-142">Again, use your topic name for `<topic_name>`.</span></span>

```azurecli-interactive
endpoint=$(az eventgrid topic show --name <topic_name> -g gridResourceGroup --query "endpoint" --output tsv)
key=$(az eventgrid topic key list --name <topic_name> -g gridResourceGroup --query "key1" --output tsv)
```

<span data-ttu-id="015e3-143">Bu makaleyi basitleştirmek için konuya gönderilmek üzere örnek olay verileri ayarladık.</span><span class="sxs-lookup"><span data-stu-id="015e3-143">To simplify this article, we have set up sample event data to send to the topic.</span></span> <span data-ttu-id="015e3-144">Normalde olay verilerini bir uygulama veya Azure hizmeti gönderir.</span><span class="sxs-lookup"><span data-stu-id="015e3-144">Typically, an application or Azure service would send the event data.</span></span> <span data-ttu-id="015e3-145">Aşağıdaki örnek, olay verilerini alır:</span><span class="sxs-lookup"><span data-stu-id="015e3-145">The following example gets the event data:</span></span>

```azurecli-interactive
body=$(eval echo "'$(curl https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/event-grid/customevent.json)'")
```

<span data-ttu-id="015e3-146">`echo "$body"` durumunda olayın tamamını görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="015e3-146">If you `echo "$body"` you can see the full event.</span></span> <span data-ttu-id="015e3-147">JSON’un `data` öğesi, olayınızın yüküdür.</span><span class="sxs-lookup"><span data-stu-id="015e3-147">The `data` element of the JSON is the payload of your event.</span></span> <span data-ttu-id="015e3-148">Bu alana doğru oluşturulmuş herhangi bir JSON gelebilir.</span><span class="sxs-lookup"><span data-stu-id="015e3-148">Any well-formed JSON can go in this field.</span></span> <span data-ttu-id="015e3-149">Ayrıca, gelişmiş yönlendirme ve filtreleme için konu alanını da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="015e3-149">You can also use the subject field for advanced routing and filtering.</span></span>

<span data-ttu-id="015e3-150">CURL, HTTP istekleri gerçekleştiren bir yardımcı programdır.</span><span class="sxs-lookup"><span data-stu-id="015e3-150">CURL is a utility that performs HTTP requests.</span></span> <span data-ttu-id="015e3-151">Bu makalede, olayı konumuza göndermek için CURL kullanıyoruz.</span><span class="sxs-lookup"><span data-stu-id="015e3-151">In this article, we use CURL to send the event to our topic.</span></span> 

```azurecli-interactive
curl -X POST -H "aeg-sas-key: $key" -d "$body" $endpoint
```

<span data-ttu-id="015e3-152">Olayı tetiklediniz ve Event Grid iletiyi abone olurken yapılandırdığınız uç noktaya gönderdi.</span><span class="sxs-lookup"><span data-stu-id="015e3-152">You have triggered the event, and Event Grid sent the message to the endpoint you configured when subscribing.</span></span> <span data-ttu-id="015e3-153">Daha önce oluşturduğunuz RequestBin URL’sine gidin.</span><span class="sxs-lookup"><span data-stu-id="015e3-153">Browse to the RequestBin URL that you created earlier.</span></span> <span data-ttu-id="015e3-154">Veya açık olan RequestBin tarayıcınızda Yenile’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="015e3-154">Or, click refresh in your open RequestBin browser.</span></span> <span data-ttu-id="015e3-155">Az önce gönderdiğiniz olayı görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="015e3-155">You see the event you just sent.</span></span> 

```json
[{
  "id": "1807",
  "eventType": "recordInserted",
  "subject": "myapp/vehicles/motorcycles",
  "eventTime": "2017-08-10T21:03:07+00:00",
  "data": {
    "make": "Ducati",
    "model": "Monster"
  },
  "topic": "/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/topics/{topic}"
}]
```

## <a name="clean-up-resources"></a><span data-ttu-id="015e3-156">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="015e3-156">Clean up resources</span></span>
<span data-ttu-id="015e3-157">Bu olayla çalışmaya devam etmeyi planlıyorsanız bu makalede oluşturulan kaynakları temizlemeyin.</span><span class="sxs-lookup"><span data-stu-id="015e3-157">If you plan to continue working with this event, do not clean up the resources created in this article.</span></span> <span data-ttu-id="015e3-158">Devam etmeyi planlamıyorsanız, aşağıdaki komutu kullanarak bu makalede oluşturduğunuz kaynakları silin.</span><span class="sxs-lookup"><span data-stu-id="015e3-158">If you do not plan to continue, use the following command to delete the resources you created in this article.</span></span>

```azurecli-interactive
az group delete --name gridResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="015e3-159">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="015e3-159">Next steps</span></span>

<span data-ttu-id="015e3-160">Artık konu oluşturma ve olay aboneliklerini öğrendiğinize göre, Event Grid’in size nasıl yardımcı olabileceği konusunda daha fazla bilgi edinebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="015e3-160">Now that you know how to create topics and event subscriptions, learn more about what Event Grid can help you do:</span></span>

- [<span data-ttu-id="015e3-161">Event Grid Hakkında</span><span class="sxs-lookup"><span data-stu-id="015e3-161">About Event Grid</span></span>](overview.md)
- [<span data-ttu-id="015e3-162">Azure Event Grid ve Logic Apps ile sanal makine değişikliklerini izleme</span><span class="sxs-lookup"><span data-stu-id="015e3-162">Monitor virtual machine changes with Azure Event Grid and Logic Apps</span></span>](monitor-virtual-machine-changes-event-grid-logic-app.md)
