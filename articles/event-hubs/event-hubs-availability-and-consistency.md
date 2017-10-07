---
title: "aaaAvailability ve Azure Event Hubs tutarlılık | Microsoft Docs"
description: "Nasıl tooprovide hello en büyük miktarda kullanılabilirlik ve Azure Event Hubs kullanarak tutarlılık bölümler."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 8f3637a1-bbd7-481e-be49-b3adf9510ba1
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: a8ededaae1589830da21cb8910ca694d2d628bd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-consistency-in-event-hubs"></a>Kullanılabilirlik ve Event Hubs tutarlılığı

## <a name="overview"></a>Genel Bakış
Azure Event Hubs kullanan bir [modeli bölümleme](event-hubs-features.md#partitions) tooimprove kullanılabilirlik ve tek olay hub'ı içinde paralelleştirme. Örneğin, dört bölüm bir event hub varsa ve bu bölümler birini bir yük dengeleme işlemi bir sunucu tooanother gelen taşınır, hala gönderebilir ve diğer üç bölümlerden alırsınız. Ayrıca, daha fazla bölümlemeye sahip olmak toohave sağlar, toplam verimliliği artırma, veri işleme daha fazla eşzamanlı okuyucu. Bölümlendirme ve dağıtılmış bir sistemde sıralama hello etkilerini anlama, çözüm tasarımı önemli bir yönüdür.

Bkz hello sıralama ve kullanılabilirlik arasındaki hello dengelemeyi açıklayan toohelp [CAP Teoremi](https://en.wikipedia.org/wiki/CAP_theorem), Brewer'ın Teoremi olarak da bilinir. Bu Teoremi tutarlılık, kullanılabilirlik ve bölüm dayanıklılık arasında hello seçim açıklanır.

Brewer'ın Teoremi tutarlılık ve kullanılabilirlik gibi tanımlar:
* Dayanıklılık bölüm: Merhaba bölümünde hata olduğunda bile verileri işlerken veri işleme sistem toocontinue özelliğidir.
* Kullanılabilirlik: başarısız olmayan düğüm makul bir süre (ile bir hata veya zaman aşımı) içinde makul bir yanıt döndürür.
* Tutarlılık: Okuma tooreturn hello en son yazma belirli bir istemcinin garanti edilmez.

## <a name="partition-tolerance"></a>Bölüm dayanıklılık
Olay hub'ları bölümlenmiş veri modeli üzerine inşa edilmiştir. Kurulum sırasında olay hub'ınıza hello bölüm sayısı yapılandırabilirsiniz ancak bu değer daha sonra değiştiremezsiniz. Bölümler Event Hubs ile kullanmalısınız olduğundan toomake uygulamanız için kullanılabilirlik ve tutarlılık hakkındaki kararınızı sahip.

## <a name="availability"></a>Kullanılabilirlik
Merhaba en basit yolu tooget kullanmaya olay hub'ları olan toouse hello varsayılan davranışı. Yeni bir oluşturursanız `EventHubClient` nesne ve hello kullan `Send` yöntemi, olayları olay hub'ınızdaki bölümler arasında otomatik olarak dağıtılır. Bu davranış hello büyük miktarda zaman verir.

Bu model hello en fazla çalışma zamanını gerektirir kullanım durumları için tercih edilir.

## <a name="consistency"></a>Tutarlılık
Bazı senaryolarda, olayların hello sıralama önemli olabilir. Örneğin, arka uç sistem tooprocess delete komutu önce güncelleştirme komutu isteyebilirsiniz. Bu örnekte, bir olayda hello bölüm anahtarı ayarlayın veya kullanın bir `PartitionSender` nesne tooonly belirli bölüm olayları tooa gönderin. Bu olaylar hello bölümünden okurken bunlar sırayla okunduğu sağlar.

Bu yapılandırma ile gönderdiğiniz hello belirli bölüm toowhich kullanılamıyorsa, bir hata yanıtı alırsınız göz önünde bulundurun. Bir benzeşim tooa tek bölüm yoksa bir karşılaştırma noktası olarak hello Event Hubs hizmeti, olay toohello sonraki kullanılabilir bölüm gönderir.

Sıralama, ayrıca çalışma zamanı, en üst düzeye çıkarma sırasında bir olası çözüm tooensure tooaggregate olayları, olay işleme uygulama bir parçası olarak olacaktır. Bu en kolay yolu tooaccomplish hello toostamp özel sıra sayısı özelliği ile bir olaydır. koddan hello bir örnek gösterilmektedir:

```csharp
// Get hello latest sequence number from your application
var sequenceNumber = GetNextSequenceNumber();
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set a custom sequence number property
data.Properties.Add("SequenceNumber", sequenceNumber);
// Send single message async
await eventHubClient.SendAsync(data);
```

Bu örnek, olay tooone hello kullanılabilir bölümlerinin olay hub'ınıza gönderir ve uygulamanızdan hello karşılık gelen sıra numarasını ayarlar. Bu çözüm, işleme uygulamanız tarafından tutulan durumu toobe gerektirir ancak büyük olasılıkla toobe kullanılabilir olduğu bir uç nokta, Gönderenler sağlar.

## <a name="next-steps"></a>Sonraki adımlar
Bağlantılar aşağıdaki hello ziyaret ederek Event Hubs hakkında daha fazla bilgi edinebilirsiniz:

* [Olay hub hizmetine genel bakış](event-hubs-what-is-event-hubs.md)
* [Olay Hub’ı oluşturma](event-hubs-create.md)
