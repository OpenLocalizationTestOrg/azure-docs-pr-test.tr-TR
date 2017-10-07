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
# <a name="how-toolog-events-tooazure-event-hubs-in-azure-api-management"></a>Nasıl toolog olayları tooAzure Azure API Management olay hub'ları
Azure Event Hubs işleme ve veri bağlı cihazlarınız ve uygulamalarınız tarafından üretilen oldukça büyük miktardaki hello çözümlemek ve böylece saniye başına milyonlarca olayı işleyebilen bir yüksek düzeyde ölçeklenebilir veri alım sistemidir. Olay hub'ları hello bir olay komut zincirinin "ön kapı" olarak görev yapan ve veriler bir event hub'ına toplandıktan sonra dönüştürülebilir ve tüm gerçek zamanlı analiz sağlayıcısı veya toplu işlem/depolama bağdaştırıcısı kullanılarak saklanır. Olay hub'ları, böylece olay tüketicileri hello olayları kendi zamanlamalarında erişebilir hello üretim hello üretimini ilgili olayların olay akışının ayırır.

Bu makalede yardımcı toohello olan [olay hub'ları ile Azure API Management tümleştirmek](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) video ve açıklar nasıl Azure Event Hubs kullanan toolog API Management olayları.

## <a name="create-an-azure-event-hub"></a>Bir Azure olay hub'ı Oluştur
Yeni bir olay Hub, oturum açma toohello toocreate [Klasik Azure portalı](https://manage.windowsazure.com) tıklatıp **yeni**->**uygulama hizmetleri**->**hizmet veri yolu**  -> **Olay hub'ı**->**hızlı Oluştur**. Bir olay hub'ı adını girin, bölge, bir abonelik seçin ve bir ad seçin. Daha önce bir ad alanı oluşturmadıysanız hello bir ad yazarak bir tane oluşturabilirsiniz **Namespace** metin kutusu. Tüm özellikleri yapılandırıldıktan sonra tıklatın **yeni bir olay hub'ı oluşturma** toocreate hello olay hub'ı.

![Olay hub'ı Oluştur][create-event-hub]

Ardından, toohello gidin **yapılandırma** sekmesinde yeni olay hub'ınız için ve iki oluşturmak **paylaşılan erişim ilkeleri**. Birinci hello ad **gönderme** ve verin **Gönder** izinleri.

![Gönderme İlkesi][sending-policy]

Merhaba ikinci bir ad **alma**, bu verin **dinleme** izinleri ve tıklatın **kaydetmek**.

![İlke alma][receiving-policy]

Her paylaşılan erişim ilkesinin uygulamaları toosend sağlar ve olayları tooand hello Event Hub ' alabilirsiniz. Bu ilkeler için tooaccess hello bağlantı dizelerini gidin toohello **Pano** sekmesini hello olay hub'ı tıklatın ve **bağlantı bilgilerini**.

![Bağlantı dizesi][event-hub-dashboard]

Merhaba **gönderme** bağlantı dizesi, olaylar, oturum açarken kullanılır ve hello **alma** bağlantı dizesi, olayların Event Hub'hello indirirken kullanılır.

![Bağlantı dizesi][event-hub-connection-string]

## <a name="create-an-api-management-logger"></a>Bir API Management Günlükçü oluşturma
Bir Event Hub sahip olduğunuza göre hello sonraki tooconfigure adımdır bir [Günlükçü](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) , API Management hizmeti olayları toohello olay hub'ı oturum açabilir.

API Management günlükçüleri hello kullanarak yapılandırılır [API Management REST API](http://aka.ms/smapi). Merhaba REST API için hello ilk kez kullanmadan önce hello gözden [Önkoşullar](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites) ve olduğundan emin olun [erişim toohello REST API etkin](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI).

toocreate bir Günlükçü URL şablon aşağıdaki hello kullanarak bir HTTP PUT İsteği olun.

`https://{your service}.management.azure-api.net/loggers/{new logger name}?api-version=2014-02-14-preview`

* Değiştir `{your service}` API Management hizmet örneğinizin hello adı.
* Değiştir `{new logger name}` yeni Günlükçü için hello istenen adda. Merhaba yapılandırdığınızda bu adı başvurur [günlük eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) İlkesi

Üstbilgileri toohello isteği aşağıdaki hello ekleyin.

* Content-Type: uygulama/json
* Yetkilendirme: SharedAccessSignature 58...
  * Merhaba oluşturma yönergeleri için `SharedAccessSignature` bkz [Azure API Management REST API kimlik doğrulama](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication).

Şablon aşağıdaki hello kullanarak hello istek gövdesini belirtin.

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

* `type`çok ayarlanmalıdır`AzureEventHub`.
* `description`Merhaba Günlükçü isteğe bağlı bir açıklama sağlar ve isterseniz sıfır uzunluğunda bir dize olabilir.
* `credentials`Merhaba içeren `name` ve `connectionString` Azure olay hub'ınızın.

Yaptığınızda hello isteği durum kodu hello Günlükçü oluşturduysanız `201 Created` döndürülür.

> [!NOTE]
> Diğer olası dönüş kodları ve bunların nedenleri için bkz: [Günlükçü oluşturma](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT). toosee listesi, güncelleştirme ve silme, hello bkz gibi diğer işlemlerin nasıl gerçekleştirmek [Günlükçü](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) varlık belgeleri.
>
>

## <a name="configure-log-to-eventhubs-policies"></a>Günlük eventhubs ilkeleri yapılandırma
API Management'te, Günlükçü yapılandırıldıktan sonra günlük eventhubs ilkeleri toolog istenen hello olayları yapılandırabilirsiniz. Merhaba günlük eventhubs İlkesi ya da hello kullanılabilir gelen İlkesi bölümüne veya hello giden ilke bölümü.

tooconfigure ilkeleri, oturum açma toohello [Azure portal](https://portal.azure.com)tooyour API Management hizmeti gidin ve tıklayın **yayımcı portalına** tooaccess hello yayımcı portalı.

![Yayımcı portalı][publisher-portal]

Tıklatın **ilkeleri** hello API Management menüde hello soldaki hello istenen ürün ve API seçin ve tıklatın **ilke Ekle**. Bu örnekte, biz İlkesi toohello ekleyeceğiniz **Echo API'si** hello içinde **sınırsız** ürün.

![İlke ekleme][add-policy]

Hello imleç Konumlandır `inbound` İlkesi hello'ye tıklayın **günlük tooEventHub** İlkesi tooinsert hello `log-to-eventhub` ilke deyimi şablonu.

![İlke düzenleyicisi][event-hub-policy]

```xml
<log-to-eventhub logger-id ='logger-id'>
  @( string.Join(",", DateTime.UtcNow, context.Deployment.ServiceName, context.RequestId, context.Request.IpAddress, context.Operation.Name))
</log-to-eventhub>
```

Değiştir `logger-id` hello önceki adımda yapılandırdığınız hello API Management Günlükçü hello adı.

Merhaba hello değeri olarak bir dize döndürür. herhangi bir ifade kullanabileceğiniz `log-to-eventhub` öğesi. Bu örnekte, başlangıç tarihi ve saati, hizmet adı, istek kimliği, istek IP adresi ve işlem adı içeren bir dize günlüğe kaydedilir.

Tıklatın **kaydetmek** toosave hello ilkesi yapılandırması güncelleştirildi. Kaydedilmeden hemen hello ilkesi etkindir ve olay hub'ı belirlenmiş oturum toohello olaylardır.

## <a name="next-steps"></a>Sonraki adımlar
* Azure Event Hubs hakkında daha fazla bilgi edinin
  * [Azure Event Hubs ile çalışmaya başlama](../event-hubs/event-hubs-c-getstarted-send.md)
  * [EventProcessorHost bulunan iletiler alma](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [Event Hubs programlama kılavuzu](../event-hubs/event-hubs-programming-guide.md)
* API Management ve Event Hubs ile tümleştirme hakkında daha fazla bilgi edinin
  * [Günlükçü varlık başvurusu](https://docs.microsoft.com/rest/api/apimanagement/loggers)
  * [Günlük eventhub ilke başvurusu](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#log-to-eventhub)
  * [Azure API Management, olay hub'ları ve Runscope Apı'lerinizi izleme](api-management-log-to-eventhub-sample.md)    

## <a name="watch-a-video-walkthrough"></a>Bir videosu izleme
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
