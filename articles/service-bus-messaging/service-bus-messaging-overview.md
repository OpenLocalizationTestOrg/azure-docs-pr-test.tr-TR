---
title: "aaaAzure Service Bus Mesajlaşma hizmetine genel bakış | Microsoft Docs"
description: "Service Bus mesajlaşması ve Azure Geçiş’in açıklaması"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: f99766cb-8f4b-4baf-b061-4b1e2ae570e4
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: get-started-article
ms.date: 05/25/2017
ms.author: sethm
ms.openlocfilehash: ede2904e11544d8f9428a2d657dcc77dacd95ac4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-messaging-flexible-data-delivery-in-hello-cloud"></a>Service Bus Mesajlaşma hizmeti: hello bulutta esnek veri teslimatı
Microsoft Azure Service Bus, güvenilir bir bilgi teslimatı hizmetidir. Bu hizmet amacını Hello toomake daha kolay iletişimidir. İki veya daha fazla taraf tooexchange bilgi almak istediğinizde, bir iletişim yönetici ihtiyaç duyar. Service Bus ise aracılı ya da üçüncü taraf iletişim mekanizmasıdır. Bu benzer tooa posta hello Fiziksel dünyadaki hizmetidir. Posta hizmetleri çok kolay toosend farklı türdeki mektupların ve teslimat garantileriyle çeşitli paketlerle herhangi bir yere hello world kolaylaştırır.

Benzer toohello posta harfler, Service Bus teslim hello gönderen ve hello alıcı esnek bilgi teslimat hizmetidir. ileti hizmeti hello sağlar hello iki tarafların hiçbir zaman çevrimiçi aynı saat veya hello kullanılabilir olmasalar aynı tam Merhaba her iki olsa bile, hello bilgi teslim saati. Aracısız iletişim benzer tooplacing bir telefon araması (veya bir telefon araması toobe - aracılı mesajlaşmaya benzeyen daha çok çağrı bekletme ve arayan kimliği önce kullanılma) olsa da bu şekilde, ileti benzer toosending bir harf ortamıdır.

Merhaba ileti gönderen ayrıca gibi işlemler, Yineleme algılaması, zamana bağlı süre sonu ve toplu işleme teslimat özelliklerini çeşitli isteyebilirsiniz. Bu düzenler de posta hizmetindekilerle benzerlik gösterir: tekrar teslimat, gerekli imza, adres değişikliği veya geri çağırma.

Service Bus, iki farklı mesajlaşma desenini destekler: *Azure Geçişi* ve *Service Bus Mesajlaşması*.

## <a name="azure-relay"></a>Azure Geçişi
Merhaba [WCF geçiş](../service-bus-relay/relay-what-is-it.md) Azure geçiş bileşenidir birçok farklı aktarım protokolünü destekleyen merkezileştirilmiş (ancak yüksek yük dengeli) bir hizmet ve Web Hizmetleri standartları. Bunlar; SOAP, WS-* ve hatta REST'i bile içerir. Merhaba [geçiş hizmeti](../service-bus-relay/service-bus-dotnet-how-to-use-relay.md) birçok farklı geçiş bağlanabilirliği seçeneği sağlar ve mümkün olduğunda doğrudan eşler arası bağlantılar anlaşmasına yardım edebilir. Hizmet veri yolu hello Windows Communication Foundation (WCF), her ikisi de hesaba tooperformance ve kullanılabilirlik, kullanan .NET geliştiricileri için optimize edilmiştir ve SOAP ve REST arabirimleri aracılığıyla geçiş hizmetine tam erişim tooits sağlar. Bu, tüm SOAP ve REST programlama ortamı toointegrate Service Bus ile mümkün kılar.

Merhaba geçiş hizmeti, geleneksel tek yönlü mesajlaşmayı, istek/yanıt mesajlaşmasını ve eş eş Mesajlaşma destekler. Ayrıca olay dağıtımını destekler Internet kapsamda tooenable yayımlama-abone olma senaryoları ve Artırılmış uçtan uca verimliliğe yönelik çift yönlü yuva iletişimi. Merhaba geçişli Mesajlaşma düzeninde bir şirket içi hizmet toohello geçiş Hizmeti giden bir bağlantı noktası üzerinden bağlanır ve tooa belirli randevu adresine bağlanan iletişim için çift yönlü yuva oluşturur. Merhaba istemci hello randevu adresini hedef toohello geçiş hizmetine iletiler göndererek hello şirket içi hizmetiyle sonra iletişim kurabilir. Merhaba geçiş hizmeti sonra "iletileri toohello şirket içi hizmeti aracılığıyla hello çift yönlü Yuva zaten yerinde geçiş". Merhaba istemci gerekmez doğrudan bağlantı toohello şirket içi hizmet veya nerede bulunduğunu hello ve hello şirket içi hizmet gelen bağlantı noktalarının gerek yoktur gerekli BT tooknow değil hello Güvenlik Duvarı'nda Aç.

WCF "geçiş" bağlamalarının bir paketini kullanarak şirket içi hizmet hello geçiş hizmeti arasında hello bağlantı başlatır. Merhaba arka planda hello geçiş bağlamaları hello bulutta Service Bus ile tümleşen tootransport bağlama öğeleri tasarlanmış toocreate WCF kanalı bileşenlerini eşleşir.

WCF geçiş birçok avantaj sunar, ancak hello server gerektirir ve istemci tooboth aynı sırada toosend zaman ileti alıp hello çevrimiçi olmalıdır. Bu tarayıcılar gibi mobil uygulamalar, yalnızca bazen bağlanan ve benzeri istemciler veya hangi hello istekler genellikle uzun ömürlü değil, HTTP Stili iletişim için en uygun değildir. Aracılı mesajlaşma, ayrılmış iletişimi destekler ve kendine özgü avantajları vardır. Örneğin, istemciler ve sunucular gerektiğinde bağlanır ve zaman uyumsuz olarak işlemlerini gerçekleştirir.

## <a name="brokered-messaging"></a>Aracılı mesajlaşma
Buna karşılık toohello düzeni, Service Bus Mesajlaşma, geçiş veya [aracılı Mesajlaşma](service-bus-queues-topics-subscriptions.md) olarak zaman uyumsuz veya "geçici olarak düşünülebilir." Üreticiler (göndericiler) ve tüketicilerin (Alıcılar) sahip çevrimiçi toobe Merhaba aynı anda. Merhaba Mesajlaşma altyapısı depoladıktan iletileri bir "aracıda" (kuyruk gibi) hello kullanıcı taraf hazır tooreceive kadar bunları. Bu, ya da gönüllü bağlantısı kesilmiş hello dağıtılmış uygulama toobe hello bileşenlerinin sağlar; Örneğin Bakım veya hello tüm sistem etkilemeden tooa bileşen kilitlenme nedeniyle. Ayrıca, hello alıcı uygulamanın yalnızca gerekli toorun hello hello iş günü sonunda olup bir stok yönetim sisteminin gibi hello günün belirli zamanlarında yalnızca çevrimiçi toocome olabilir.

Merhaba çekirdek hello Service Bus aracılı Mesajlaşma altyapısının kuyruklar, konu başlıkları ve abonelikleri bileşenleridir.  Hello birincil fark konuları toomultiple alıcılar gönderme dahil olmak üzere Gelişmiş içerik tabanlı Yönlendirme ve teslimat mantığı için kullanılabilen Yayınla/Abone ol işlevlerini desteklemesidir. Bu bileşenler zamana bağlı ayırma, yayımla/abone ol ve yük dengelemesi gibi yeni, zaman uyumsuz mesajlaşma senaryolarına olanak sağlar. Bu mesajlaşma varlıkları hakkında daha fazla bilgi edinmek için bkz. [Service Bus kuyrukları, konu başlıkları ve abonelikleri](service-bus-queues-topics-subscriptions.md).

Merhaba WCF geçiş altyapısıyla hello aracılı Mesajlaşma gibi yetenek WCF ve .NET Framework programcıları için ve ayrıca REST aracılığıyla sağlanır.

## <a name="next-steps"></a>Sonraki adımlar
Service Bus Mesajlaşma, hakkında daha fazla toolearn aşağıdaki konularda hello bakın.

* [Service Bus ile ilgili temel bilgiler](service-bus-fundamentals-hybrid-solutions.md)
* [Service Bus kuyrukları, konu başlıkları ve abonelikleri](service-bus-queues-topics-subscriptions.md)
* [Nasıl toouse Service Bus kuyrukları](service-bus-dotnet-get-started-with-queues.md)
* [Nasıl toouse Service Bus konuları ve abonelikleri](service-bus-dotnet-how-to-use-topics-subscriptions.md)

