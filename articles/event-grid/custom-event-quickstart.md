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
# <a name="create-and-route-custom-events-with-azure-event-grid"></a>Azure Event Grid ile özel olaylar oluşturma ve yönlendirme

Azure olay kılavuz hello bulut için bir olay hizmetidir. Bu makalede, hello Azure CLI toocreate özel bir konu kullanın, toohello konu abone ve hello olay tooview hello sonuç tetikler. Genellikle, bir Web kancası veya Azure işlevi gibi toohello olay yanıt olayları tooan uç nokta gönderin. Ancak, toosimplify Bu makale, yalnızca karışılama iletileri toplar hello olayları tooa URL'sini gönderin. Bu URL’yi [RequestBin](https://requestb.in/) adlı açık kaynak, üçüncü taraf bir aracı kullanarak oluşturursunuz.

>[!NOTE]
>**RequestBin** ağır iş yüklerinde kullanım için tasarlanmamış açık kaynaklı bir araçtır. Merhaba burada hello aracının tamamen demonstrative kullanılır. Aynı anda birden fazla olay gönderme, tüm olaylarınızı hello aracında göremeyebilirsiniz.

İşiniz bittiğinde, hello olay verilerini tooan endpoint gönderildi bakın.

![Olay verileri](./media/custom-event-quickstart/request-result.png)

[!INCLUDE [quickstarts-free-trial-note.md](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu makalede Azure CLI hello en son sürümünü kullandığınızı gerektirir (2.0.14 veya üstü). çalıştırma toofind hello sürüm `az --version`. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme](/cli/azure/install-azure-cli).

## <a name="create-a-resource-group"></a>Kaynak grubu oluşturma

Event Grid konuları Azure kaynaklarıdır ve bir Azure kaynak grubuna yerleştirilmelidir. Merhaba kaynak grubu hangi Azure kaynakları dağıtılan yönetilen ve mantıksal bir koleksiyonudur.

Bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](/cli/azure/group#create) komutu. 

Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *gridResourceGroup* hello içinde *westus2* konumu.

```azurecli-interactive
az group create --name gridResourceGroup --location westus2
```

## <a name="create-a-custom-topic"></a>Özel konu oluşturma

Konu, olaylarınızı gönderdiğiniz kullanıcı tanımlı bir uç nokta sağlar. Merhaba aşağıdaki örnek hello konu kaynak grubunuzdaki oluşturur. `<topic_name>` değerini konunuz için benzersiz bir adla değiştirin. bir DNS girişi tarafından temsil edilen çünkü hello konu adı benzersiz olmalıdır. Merhaba Önizleme sürümü için olay kılavuz destekleyen **westus2** ve **westcentralus** konumları.

```azurecli-interactive
az eventgrid topic create --name <topic_name> -l westus2 -g gridResourceGroup
```

## <a name="create-a-message-endpoint"></a>İleti uç noktası oluşturma

Toohello konu abone önce hello uç noktası hello olay iletisi için oluşturalım. Kod toorespond toohello olay yazmak yerine, bunları görüntüleyebilmeniz Merhaba iletileri toplayan bir uç nokta oluşturalım. RequestBin bir açık kaynaklı, toocreate bir uç nokta sağlar üçüncü taraf aracı ve tooit gönderilen istekleri Görüntüle ' dir. Çok Git[RequestBin](https://requestb.in/), tıklatıp **bir RequestBin oluşturma**.  Toohello konu abone olurken gerektiğinden hello depo URL'yi kopyalayın.

## <a name="subscribe-tooa-topic"></a>Tooa konu abone olma

Hangi olayların tooa konu tootell olay kılavuz abone tootrack istiyor. Merhaba aşağıdaki örnekte oluşturulan ve olay bildirimi hello uç noktası olarak RequestBin hello URL geçirir toohello konu abone olur. Değiştir `<event_subscription_name>` aboneliğiniz için benzersiz bir ad ile ve `<URL_from_RequestBin>` bölüm önceki hello hello değerinden ile. Bir uç nokta abone olurken belirterek, olay kılavuz hello olayları toothat uç noktasını yönlendirme işler. İçin `<topic_name>`, daha önce oluşturduğunuz hello değerini kullanın. 

```azurecli-interactive
az eventgrid topic event-subscription create --name <event_subscription_name> \
  --endpoint <URL_from_RequestBin> \
  -g gridResourceGroup \
  --topic-name <topic_name>
```

## <a name="send-an-event-tooyour-topic"></a>Bir olay tooyour konu gönderin

Şimdi, şimdi bir olay toosee tetikleyecek olay kılavuz hello ileti tooyour endpoint nasıl dağıtır. İlk olarak, anahtarı hello konusuna ve şimdi hello URL'sini alma. Tekrar belirtmek gerekirse, `<topic_name>` için kendi konu adınızı kullanın.

```azurecli-interactive
endpoint=$(az eventgrid topic show --name <topic_name> -g gridResourceGroup --query "endpoint" --output tsv)
key=$(az eventgrid topic key list --name <topic_name> -g gridResourceGroup --query "key1" --output tsv)
```

toosimplify bu makalede örnek olay verileri toosend toohello konusunu ayarlar. Genellikle, bir uygulama veya Azure hizmet hello olay veri gönderebilir. Aşağıdaki örnek hello hello olay verilerini alır:

```azurecli-interactive
body=$(eval echo "'$(curl https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/event-grid/customevent.json)'")
```

Varsa, `echo "$body"` hello tam olay görebilirsiniz. Merhaba `data` hello JSON öğesidir olayınızın hello yükü. Bu alana doğru oluşturulmuş herhangi bir JSON gelebilir. Merhaba konu alanı, Gelişmiş Yönlendirme ve filtreleme için de kullanabilirsiniz.

CURL, HTTP istekleri gerçekleştiren bir yardımcı programdır. Bu makalede, CURL toosend hello olay tooour konu kullanırız. 

```azurecli-interactive
curl -X POST -H "aeg-sas-key: $key" -d "$body" $endpoint
```

Merhaba olay tetiklenir ve olay kılavuz hello ileti toohello uç nokta abone olurken yapılandırdığınız gönderilir. Daha önce oluşturduğunuz RequestBin URL toohello göz atın. Veya açık olan RequestBin tarayıcınızda Yenile’ye tıklayın. Yalnızca gönderilen hello olayın bakın. 

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

## <a name="clean-up-resources"></a>Kaynakları temizleme
Bu olay ile çalışma toocontinue planı yoksa bu makalede oluşturulan hello kaynakları temizlemek değil. Toocontinue düşünmüyorsanız, bu makaledeki oluşturulan komut toodelete hello kaynakları aşağıdaki hello kullanın.

```azurecli-interactive
az group delete --name gridResourceGroup
```

## <a name="next-steps"></a>Sonraki adımlar

Artık bildiğinize göre nasıl toocreate konuları ve olay abonelikleri hakkında daha fazla bilgi hangi olay kılavuz yapmanıza yardımcı olabilir:

- [Event Grid Hakkında](overview.md)
- [Azure Event Grid ve Logic Apps ile sanal makine değişikliklerini izleme](monitor-virtual-machine-changes-event-grid-logic-app.md)
