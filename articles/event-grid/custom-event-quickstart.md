---
title: "Azure olay kılavuz aaaCustom olaylarını | Microsoft Docs"
description: "Toothat olayına abone ve Azure olay kılavuz toopublish bir konuyu kullanın."
services: event-grid
keywords: 
author: djrosanova
ms.author: darosa
ms.date: 08/15/2017
ms.topic: hero-article
ms.service: event-grid
ms.openlocfilehash: 5055df1c970b043cadf06978a076f7f5c83501cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-route-custom-events-with-azure-event-grid"></a><span data-ttu-id="1ccff-103">Azure Event Grid ile özel olaylar oluşturma ve yönlendirme</span><span class="sxs-lookup"><span data-stu-id="1ccff-103">Create and route custom events with Azure Event Grid</span></span>

<span data-ttu-id="1ccff-104">Azure olay kılavuz hello bulut için bir olay hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="1ccff-104">Azure Event Grid is an eventing service for hello cloud.</span></span> <span data-ttu-id="1ccff-105">Bu makalede, hello Azure CLI toocreate özel bir konu kullanın, toohello konu abone ve hello olay tooview hello sonuç tetikler.</span><span class="sxs-lookup"><span data-stu-id="1ccff-105">In this article, you use hello Azure CLI toocreate a custom topic, subscribe toohello topic, and trigger hello event tooview hello result.</span></span> <span data-ttu-id="1ccff-106">Genellikle, bir Web kancası veya Azure işlevi gibi toohello olay yanıt olayları tooan uç nokta gönderin.</span><span class="sxs-lookup"><span data-stu-id="1ccff-106">Typically, you send events tooan endpoint that responds toohello event, such as, a webhook or Azure Function.</span></span> <span data-ttu-id="1ccff-107">Ancak, toosimplify Bu makale, yalnızca karışılama iletileri toplar hello olayları tooa URL'sini gönderin.</span><span class="sxs-lookup"><span data-stu-id="1ccff-107">However, toosimplify this article, you send hello events tooa URL that merely collects hello messages.</span></span> <span data-ttu-id="1ccff-108">Bu URL’yi [RequestBin](https://requestb.in/) adlı açık kaynak, üçüncü taraf bir aracı kullanarak oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="1ccff-108">You create this URL by using an open source, third-party tool called [RequestBin](https://requestb.in/).</span></span>

>[!NOTE]
><span data-ttu-id="1ccff-109">**RequestBin** ağır iş yüklerinde kullanım için tasarlanmamış açık kaynaklı bir araçtır.</span><span class="sxs-lookup"><span data-stu-id="1ccff-109">**RequestBin** is an open source tool that is not intended for high throughput usage.</span></span> <span data-ttu-id="1ccff-110">Merhaba burada hello aracının tamamen demonstrative kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1ccff-110">hello use of hello tool here is purely demonstrative.</span></span> <span data-ttu-id="1ccff-111">Aynı anda birden fazla olay gönderme, tüm olaylarınızı hello aracında göremeyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1ccff-111">If you push more than one event at a time, you might not see all of your events in hello tool.</span></span>

<span data-ttu-id="1ccff-112">İşiniz bittiğinde, hello olay verilerini tooan endpoint gönderildi bakın.</span><span class="sxs-lookup"><span data-stu-id="1ccff-112">When you are finished, you see that hello event data has been sent tooan endpoint.</span></span>

![Olay verileri](./media/custom-event-quickstart/request-result.png)

[!INCLUDE [quickstarts-free-trial-note.md](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="1ccff-114">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu makalede Azure CLI hello en son sürümünü kullandığınızı gerektirir (2.0.14 veya üstü).</span><span class="sxs-lookup"><span data-stu-id="1ccff-114">If you choose tooinstall and use hello CLI locally, this article requires that you are running hello latest version of Azure CLI (2.0.14 or later).</span></span> <span data-ttu-id="1ccff-115">çalıştırma toofind hello sürüm `az --version`.</span><span class="sxs-lookup"><span data-stu-id="1ccff-115">toofind hello version, run `az --version`.</span></span> <span data-ttu-id="1ccff-116">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="1ccff-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="1ccff-117">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="1ccff-117">Create a resource group</span></span>

<span data-ttu-id="1ccff-118">Event Grid konuları Azure kaynaklarıdır ve bir Azure kaynak grubuna yerleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="1ccff-118">Event Grid topics are Azure resources, and must be placed in an Azure resource group.</span></span> <span data-ttu-id="1ccff-119">Merhaba kaynak grubu hangi Azure kaynakları dağıtılan yönetilen ve mantıksal bir koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="1ccff-119">hello resource group is a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="1ccff-120">Bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](/cli/azure/group#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="1ccff-120">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> 

<span data-ttu-id="1ccff-121">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *gridResourceGroup* hello içinde *westus2* konumu.</span><span class="sxs-lookup"><span data-stu-id="1ccff-121">hello following example creates a resource group named *gridResourceGroup* in hello *westus2* location.</span></span>

```azurecli-interactive
az group create --name gridResourceGroup --location westus2
```

## <a name="create-a-custom-topic"></a><span data-ttu-id="1ccff-122">Özel konu oluşturma</span><span class="sxs-lookup"><span data-stu-id="1ccff-122">Create a custom topic</span></span>

<span data-ttu-id="1ccff-123">Konu, olaylarınızı gönderdiğiniz kullanıcı tanımlı bir uç nokta sağlar.</span><span class="sxs-lookup"><span data-stu-id="1ccff-123">A topic provides a user-defined endpoint that you post your events to.</span></span> <span data-ttu-id="1ccff-124">Merhaba aşağıdaki örnek hello konu kaynak grubunuzdaki oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1ccff-124">hello following example creates hello topic in your resource group.</span></span> <span data-ttu-id="1ccff-125">`<topic_name>` değerini konunuz için benzersiz bir adla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="1ccff-125">Replace `<topic_name>` with a unique name for your topic.</span></span> <span data-ttu-id="1ccff-126">bir DNS girişi tarafından temsil edilen çünkü hello konu adı benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1ccff-126">hello topic name must be unique because it is represented by a DNS entry.</span></span> <span data-ttu-id="1ccff-127">Merhaba Önizleme sürümü için olay kılavuz destekleyen **westus2** ve **westcentralus** konumları.</span><span class="sxs-lookup"><span data-stu-id="1ccff-127">For hello preview release, Event Grid supports **westus2** and **westcentralus** locations.</span></span>

```azurecli-interactive
az eventgrid topic create --name <topic_name> -l westus2 -g gridResourceGroup
```

## <a name="create-a-message-endpoint"></a><span data-ttu-id="1ccff-128">İleti uç noktası oluşturma</span><span class="sxs-lookup"><span data-stu-id="1ccff-128">Create a message endpoint</span></span>

<span data-ttu-id="1ccff-129">Toohello konu abone önce hello uç noktası hello olay iletisi için oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="1ccff-129">Before subscribing toohello topic, let's create hello endpoint for hello event message.</span></span> <span data-ttu-id="1ccff-130">Kod toorespond toohello olay yazmak yerine, bunları görüntüleyebilmeniz Merhaba iletileri toplayan bir uç nokta oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="1ccff-130">Rather than write code toorespond toohello event, let's create an endpoint that collects hello messages so you can view them.</span></span> <span data-ttu-id="1ccff-131">RequestBin bir açık kaynaklı, toocreate bir uç nokta sağlar üçüncü taraf aracı ve tooit gönderilen istekleri Görüntüle ' dir.</span><span class="sxs-lookup"><span data-stu-id="1ccff-131">RequestBin is an open source, third-party tool that enables you toocreate an endpoint, and view requests that are sent tooit.</span></span> <span data-ttu-id="1ccff-132">Çok Git[RequestBin](https://requestb.in/), tıklatıp **bir RequestBin oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="1ccff-132">Go too[RequestBin](https://requestb.in/), and click **Create a RequestBin**.</span></span>  <span data-ttu-id="1ccff-133">Toohello konu abone olurken gerektiğinden hello depo URL'yi kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="1ccff-133">Copy hello bin URL, because you need it when subscribing toohello topic.</span></span>

## <a name="subscribe-tooa-topic"></a><span data-ttu-id="1ccff-134">Tooa konu abone olma</span><span class="sxs-lookup"><span data-stu-id="1ccff-134">Subscribe tooa topic</span></span>

<span data-ttu-id="1ccff-135">Hangi olayların tooa konu tootell olay kılavuz abone tootrack istiyor.</span><span class="sxs-lookup"><span data-stu-id="1ccff-135">You subscribe tooa topic tootell Event Grid which events you want tootrack.</span></span> <span data-ttu-id="1ccff-136">Merhaba aşağıdaki örnekte oluşturulan ve olay bildirimi hello uç noktası olarak RequestBin hello URL geçirir toohello konu abone olur.</span><span class="sxs-lookup"><span data-stu-id="1ccff-136">hello following example subscribes toohello topic you created, and passes hello URL from RequestBin as hello endpoint for event notification.</span></span> <span data-ttu-id="1ccff-137">Değiştir `<event_subscription_name>` aboneliğiniz için benzersiz bir ad ile ve `<URL_from_RequestBin>` bölüm önceki hello hello değerinden ile.</span><span class="sxs-lookup"><span data-stu-id="1ccff-137">Replace `<event_subscription_name>` with a unique name for your subscription, and `<URL_from_RequestBin>` with hello value from hello preceding section.</span></span> <span data-ttu-id="1ccff-138">Bir uç nokta abone olurken belirterek, olay kılavuz hello olayları toothat uç noktasını yönlendirme işler.</span><span class="sxs-lookup"><span data-stu-id="1ccff-138">By specifying an endpoint when subscribing, Event Grid handles hello routing of events toothat endpoint.</span></span> <span data-ttu-id="1ccff-139">İçin `<topic_name>`, daha önce oluşturduğunuz hello değerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="1ccff-139">For `<topic_name>`, use hello value you created earlier.</span></span> 

```azurecli-interactive
az eventgrid topic event-subscription create --name <event_subscription_name> \
  --endpoint <URL_from_RequestBin> \
  -g gridResourceGroup \
  --topic-name <topic_name>
```

## <a name="send-an-event-tooyour-topic"></a><span data-ttu-id="1ccff-140">Bir olay tooyour konu gönderin</span><span class="sxs-lookup"><span data-stu-id="1ccff-140">Send an event tooyour topic</span></span>

<span data-ttu-id="1ccff-141">Şimdi, şimdi bir olay toosee tetikleyecek olay kılavuz hello ileti tooyour endpoint nasıl dağıtır.</span><span class="sxs-lookup"><span data-stu-id="1ccff-141">Now, let's trigger an event toosee how Event Grid distributes hello message tooyour endpoint.</span></span> <span data-ttu-id="1ccff-142">İlk olarak, anahtarı hello konusuna ve şimdi hello URL'sini alma.</span><span class="sxs-lookup"><span data-stu-id="1ccff-142">First, let's get hello URL and key for hello topic.</span></span> <span data-ttu-id="1ccff-143">Tekrar belirtmek gerekirse, `<topic_name>` için kendi konu adınızı kullanın.</span><span class="sxs-lookup"><span data-stu-id="1ccff-143">Again, use your topic name for `<topic_name>`.</span></span>

```azurecli-interactive
endpoint=$(az eventgrid topic show --name <topic_name> -g gridResourceGroup --query "endpoint" --output tsv)
key=$(az eventgrid topic key list --name <topic_name> -g gridResourceGroup --query "key1" --output tsv)
```

<span data-ttu-id="1ccff-144">toosimplify bu makalede örnek olay verileri toosend toohello konusunu ayarlar.</span><span class="sxs-lookup"><span data-stu-id="1ccff-144">toosimplify this article, we have set up sample event data toosend toohello topic.</span></span> <span data-ttu-id="1ccff-145">Genellikle, bir uygulama veya Azure hizmet hello olay veri gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="1ccff-145">Typically, an application or Azure service would send hello event data.</span></span> <span data-ttu-id="1ccff-146">Aşağıdaki örnek hello hello olay verilerini alır:</span><span class="sxs-lookup"><span data-stu-id="1ccff-146">hello following example gets hello event data:</span></span>

```azurecli-interactive
body=$(eval echo "'$(curl https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/event-grid/customevent.json)'")
```

<span data-ttu-id="1ccff-147">Varsa, `echo "$body"` hello tam olay görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1ccff-147">If you `echo "$body"` you can see hello full event.</span></span> <span data-ttu-id="1ccff-148">Merhaba `data` hello JSON öğesidir olayınızın hello yükü.</span><span class="sxs-lookup"><span data-stu-id="1ccff-148">hello `data` element of hello JSON is hello payload of your event.</span></span> <span data-ttu-id="1ccff-149">Bu alana doğru oluşturulmuş herhangi bir JSON gelebilir.</span><span class="sxs-lookup"><span data-stu-id="1ccff-149">Any well-formed JSON can go in this field.</span></span> <span data-ttu-id="1ccff-150">Merhaba konu alanı, Gelişmiş Yönlendirme ve filtreleme için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1ccff-150">You can also use hello subject field for advanced routing and filtering.</span></span>

<span data-ttu-id="1ccff-151">CURL, HTTP istekleri gerçekleştiren bir yardımcı programdır.</span><span class="sxs-lookup"><span data-stu-id="1ccff-151">CURL is a utility that performs HTTP requests.</span></span> <span data-ttu-id="1ccff-152">Bu makalede, CURL toosend hello olay tooour konu kullanırız.</span><span class="sxs-lookup"><span data-stu-id="1ccff-152">In this article, we use CURL toosend hello event tooour topic.</span></span> 

```azurecli-interactive
curl -X POST -H "aeg-sas-key: $key" -d "$body" $endpoint
```

<span data-ttu-id="1ccff-153">Merhaba olay tetiklenir ve olay kılavuz hello ileti toohello uç nokta abone olurken yapılandırdığınız gönderilir.</span><span class="sxs-lookup"><span data-stu-id="1ccff-153">You have triggered hello event, and Event Grid sent hello message toohello endpoint you configured when subscribing.</span></span> <span data-ttu-id="1ccff-154">Daha önce oluşturduğunuz RequestBin URL toohello göz atın.</span><span class="sxs-lookup"><span data-stu-id="1ccff-154">Browse toohello RequestBin URL that you created earlier.</span></span> <span data-ttu-id="1ccff-155">Veya açık olan RequestBin tarayıcınızda Yenile’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1ccff-155">Or, click refresh in your open RequestBin browser.</span></span> <span data-ttu-id="1ccff-156">Yalnızca gönderilen hello olayın bakın.</span><span class="sxs-lookup"><span data-stu-id="1ccff-156">You see hello event you just sent.</span></span> 

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

## <a name="clean-up-resources"></a><span data-ttu-id="1ccff-157">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="1ccff-157">Clean up resources</span></span>
<span data-ttu-id="1ccff-158">Bu olay ile çalışma toocontinue planı yoksa bu makalede oluşturulan hello kaynakları temizlemek değil.</span><span class="sxs-lookup"><span data-stu-id="1ccff-158">If you plan toocontinue working with this event, do not clean up hello resources created in this article.</span></span> <span data-ttu-id="1ccff-159">Toocontinue düşünmüyorsanız, bu makaledeki oluşturulan komut toodelete hello kaynakları aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="1ccff-159">If you do not plan toocontinue, use hello following command toodelete hello resources you created in this article.</span></span>

```azurecli-interactive
az group delete --name gridResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="1ccff-160">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1ccff-160">Next steps</span></span>

<span data-ttu-id="1ccff-161">Artık bildiğinize göre nasıl toocreate konuları ve olay abonelikleri hakkında daha fazla bilgi hangi olay kılavuz yapmanıza yardımcı olabilir:</span><span class="sxs-lookup"><span data-stu-id="1ccff-161">Now that you know how toocreate topics and event subscriptions, learn more about what Event Grid can help you do:</span></span>

- [<span data-ttu-id="1ccff-162">Event Grid Hakkında</span><span class="sxs-lookup"><span data-stu-id="1ccff-162">About Event Grid</span></span>](overview.md)
- [<span data-ttu-id="1ccff-163">Azure Event Grid ve Logic Apps ile sanal makine değişikliklerini izleme</span><span class="sxs-lookup"><span data-stu-id="1ccff-163">Monitor virtual machine changes with Azure Event Grid and Logic Apps</span></span>](monitor-virtual-machine-changes-event-grid-logic-app.md)
