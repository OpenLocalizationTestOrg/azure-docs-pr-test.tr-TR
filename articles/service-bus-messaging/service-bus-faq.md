---
title: "aaaAzure Service Bus sık sorulan sorular (SSS) | Microsoft Docs"
description: "Azure Service Bus hakkında bazı sık sorulan sorular yanıtlanmaktadır."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: cc75786d-3448-4f79-9fec-eef56c0027ba
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: 71fe9eac46647a3e4026dbcaf2196984dd4b6a44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-faq"></a>Hizmet Veri Yolu SSS
Bu makalede, Microsoft Azure Service Bus hakkında sık sorulan bazı sorular yanıtlanmaktadır. Merhaba ziyaret edebilirsiniz [Azure destek SSS](http://go.microsoft.com/fwlink/?LinkID=185083) genel Azure fiyatlandırma ve destek bilgileri için.

## <a name="general-questions-about-azure-service-bus"></a>Azure Service Bus hakkında genel sorular
### <a name="what-is-azure-service-bus"></a>Azure Service Bus nedir?
[Azure Service Bus](service-bus-messaging-overview.md) ayrılmış sistemleri arasında toosend veri sağlayan bir zaman uyumsuz Mesajlaşma bulut platformudur. Microsoft bu özellik, toohost sipariş toouse içinde kendi donanımınızın herhangi biri gerekmediği anlamına gelir bir hizmet olarak sunar.

### <a name="what-is-a-service-bus-namespace"></a>Bir hizmet veri yolu ad alanı nedir?
A [ad alanı](service-bus-create-namespace-portal.md) uygulamanızı Service Bus kaynaklarını adreslemek için kapsam bir kapsayıcı sağlar. Bir tane gerekli toouse hizmet veri yolu olan ve hello biri Başlarken ilk adımlar olacaktır.

### <a name="what-is-an-azure-service-bus-queue"></a>Bir Azure hizmet veri yolu kuyruğu nedir?
A [Service Bus kuyruğuna](service-bus-queues-topics-subscriptions.md) iletileri depolandığı bir varlıktır. Birden çok uygulama veya birbiriyle toocommunicate gerektiren dağıtılmış bir uygulama birden fazla bölümü olduğunda sıraları özellikle yararlı olur. birden fazla ürün (iletileri) alınan ve sonra o konumdan gönderilen hello sıra benzer tooa dağıtım merkezi olmamasıdır.

### <a name="what-are-azure-service-bus-topics-and-subscriptions"></a>Azure Service Bus konuları ve abonelikleri nelerdir?
Bir konu sırası olarak canlandırılabilir ve birden çok abonelik kullanırken, bu daha zengin bir Mesajlaşma modeli olur; bir çok iletişim aracı temelde. Bu yayımlama/abonelik modelini (veya *pub/alt*) birden çok abonelik toohave içeren bir ileti tooa konu birden çok uygulama tarafından alınan ileti gönderir bir uygulama sağlar.

### <a name="what-is-a-partitioned-entity"></a>Bölümlenmiş bir varlık nedir?
Geleneksel kuyruk veya konu tek ileti aracısı tarafından işlenen ve bir Mesajlaşma deposunda depolanır. A [bölümlenmiş kuyruk veya konu](service-bus-partitioning.md) birden çok ileti aracıları tarafından işlenen ve birden çok Mesajlaşma deposunda depolanır. Bölümlenmiş kuyruk veya konu, genel üretilen işi hello Bunun anlamı artık tek ileti Aracısı ya da ileti deposu hello performans ile sınırlıdır. Ayrıca, bir Mesajlaşma deposu geçici bir kesinti bölümlenmiş kuyruk veya konu kullanılamaz işlemez.

Sıralama bölümleme varlıklar kullanırken sağlanmaz olduğunu unutmayın. Bir bölüm kullanılamıyor hello olayda hala gönderebilir ve diğer bölümler hello iletileri alacak.

## <a name="best-practices"></a>En iyi uygulamalar
### <a name="what-are-some-azure-service-bus-best-practices"></a>Bazı Azure Service Bus en iyi uygulamalar nelerdir?
* [Hizmet veri yolu kullanarak performans iyileştirmeleri için en iyi uygulamaları] [ Best practices for performance improvements using Service Bus] – nasıl alışverişi sırasında toooptimize performans iletileri bu makalede açıklanır.

### <a name="what-should-i-know-before-creating-entities"></a>Ne ı varlıklar oluşturmadan önce bilmeniz gerekenler?
aşağıdaki özelliklere bir kuyruk ve konu hello değişmez. Lütfen bu, yeni bir yedek varlık oluşturmadan değiştirilemez olarak varlıklarınızı sağlarken bu dikkate alın.

* Boyut
* Bölümleme
* Oturumlar
* Yinelenen algılama
* Varlık express

## <a name="pricing"></a>Fiyatlandırma
Bu bölümde hello Service Bus fiyatlandırma yapısı hakkında bazı sık sorulan sorular yanıtlanmaktadır.

Merhaba [Service fiyatlandırma ve faturalama Bus](service-bus-pricing-billing.md) makalede açıklanır hello fatura ölçümler Service Bus ve Service Bus seçenekleri fiyatlandırması hakkında bilgi için bkz: [Service Bus fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/service-bus/).

Merhaba ziyaret edebilirsiniz [Azure desteği ile ilgili SSS](http://go.microsoft.com/fwlink/?LinkID=185083) genel Azure fiyatlandırma bilgileri için. 

### <a name="how-do-you-charge-for-service-bus"></a>Hizmet veri yolu için nasıl ücret?
Hizmet veri yolu fiyatlandırma hakkında tam bilgi için lütfen bkz [Service Bus fiyatlandırma ayrıntıları][Pricing overview]. Ayrıca toohello fiyatlar aksi belirtilmedikçe, ilişkili veri aktarımları, uygulamanızın sağlandı hello veri merkezi dışında çıkışı için ücretlendirilirsiniz.

### <a name="what-usage-of-service-bus-is-subject-toodata-transfer-what-is-not"></a>Hangi kullanımını Service Bus konu toodata transfer mi? Ne değil misiniz?
Belirli bir Azure bölgesi içinde herhangi bir veri aktarımı yanı gelen veri aktarımı hiçbir ücret ödemeden sağlanır. Veri aktarımı bir bölge dışında bulunan konu tooegress ücretleri olan [burada](https://azure.microsoft.com/pricing/details/bandwidth/).

### <a name="does-service-bus-charge-for-storage"></a>Hizmet veri yolu, depolama için ücretli mi?
Hayır, hizmet veri yolu için depolama ücret değil. Ancak, bir kota sınırlama hello en büyük sıra/konu kalıcı veri miktarı yoktur. Merhaba sonraki SSS bakın.

## <a name="quotas"></a>Kotalar

Service Bus sınırlarını ve kotaları listesi için bkz: Merhaba [Service Bus kotaları genel bakış][Quotas overview].

### <a name="does-service-bus-have-any-usage-quotas"></a>Hizmet veri yolu olan kullanım kotaları var mı?
Varsayılan olarak, her bulut için Microsoft hizmet tüm müşteri'nin abonelikler arasında hesaplanan bir toplama aylık kullanım kotası ayarlar. Lütfen, bu sınırları birden fazla gerekebilir anlamak için böylece biz gereksinimlerinizi anlamak ve bu sınırları uygun şekilde ayarlayın herhangi bir zamanda Müşteri Hizmetleri'ne başvurun. Hizmet veri yolu için hello toplama kullanım kotası ayda 5 milyar iletileri ' dir.

Merhaba sağ toodisable kullanım kotalarını belirtilen aydaki aştı bir müşteri hesabı yedek olsa da, biz e-posta bildirimi sağlamak ve herhangi bir işlem gerçekleştirmeden önce bir müşteri birden çok deneme toocontact olun. Müşteriler bu kotalar aşan hala hello kotaları aşan ücretleri için sorumlu olacaktır.

Diğer hizmetleri gibi Azure üzerinde hizmet veri yolu Orta kaynak kullanımını olduğunu belirli kotaları tooensure kümesi zorlar. Hello bu Kotalar hakkında daha fazla ayrıntı bulabilirsiniz [Service Bus kotaları genel bakış][Quotas overview].

## <a name="troubleshooting"></a>Sorun giderme
### <a name="what-are-some-of-hello-exceptions-generated-by-azure-service-bus-apis-and-their-suggested-actions"></a>Azure Service Bus API'lerine ve bunların önerilen eylemleri tarafından oluşturulan hello özel durumlar bazıları nelerdir?
Olası Service Bus özel durumlar listesi için bkz: [özel durumlar genel bakış][Exceptions overview].

### <a name="what-is-a-shared-access-signature-and-which-languages-support-generating-a-signature"></a>Paylaşılan erişim imzası nedir ve hangi dilleri imza oluşturma destekliyor?
Paylaşılan erişim imzaları SHA-256 güvenli karmaları veya URI'ler için temel kimlik doğrulama mekanizması değil. Hakkında bilgi için toogenerate kendi imzaları düğümü, PHP, Java ve C\#, hello bkz [paylaşılan erişim imzaları] [ Shared Access Signatures] makalesi.

## <a name="subscription-and-namespace-management"></a>Abonelik ve ad alanı yönetimi
### <a name="how-do-i-migrate-a-namespace-tooanother-azure-subscription"></a>Ad alanı tooanother Azure aboneliği nasıl geçişini?

Her iki hello kullanarak bir Azure aboneliği tooanother bir ad alanı taşıyabilirsiniz [Azure portal](https://portal.azure.com) veya PowerShell komutları. Sipariş tooexecute hello işlemde hello ad alanı zaten etkin olması gerekir. Merhaba komutları yürütülürken hello kullanıcı her iki hello kaynağı üzerinde bir yönetici olmanız ve abonelikleri hedef gerekir.

#### <a name="portal"></a>Portal

toouse hello Azure portal toomigrate hizmet veri yolu ad alanları tooanother abonelik hello yönergeleri izleyin [burada](../azure-resource-manager/resource-group-move-resources.md#use-portal). 

#### <a name="powershell"></a>PowerShell

Merhaba aşağıdaki PowerShell komut dizisi bir ad bir Azure aboneliği tooanother taşır. tooexecute bu işlemi hello ad alanı zaten etkin olmalı ve hello PowerShell komutlarını çalıştırarak hello kullanıcı her iki hello kaynak ve hedef abonelikler üzerinde bir yönetici olması gerekir.

```powershell
# Create a new resource group in target subscription
Select-AzureRmSubscription -SubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff'
New-AzureRmResourceGroup -Name 'targetRG' -Location 'East US'

# Move namespace from source subscription tootarget subscription
Select-AzureRmSubscription -SubscriptionId 'aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa'
$res = Find-AzureRmResource -ResourceNameContains mynamespace -ResourceType 'Microsoft.ServiceBus/namespaces'
Move-AzureRmResource -DestinationResourceGroupName 'targetRG' -DestinationSubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff' -ResourceId $res.ResourceId
```

## <a name="next-steps"></a>Sonraki adımlar
Service Bus hakkında daha fazla toolearn aşağıdaki konularda hello bakın.

* [Azure Service Bus Premium (blog yayını) Tanıtımı](http://azure.microsoft.com/blog/introducing-azure-service-bus-premium-messaging/)
* [Azure Service Bus Premium (Channel9) Tanıtımı](https://channel9.msdn.com/Blogs/Subscribe/Introducing-Azure-Service-Bus-Premium-Messaging)
* [Hizmet veri yolu genel bakış](service-bus-messaging-overview.md)
* [Azure Service Bus mimarisine genel bakış](service-bus-fundamentals-hybrid-solutions.md)
* [Service Bus kuyrukları ile çalışmaya başlama](service-bus-dotnet-get-started-with-queues.md)

[Best practices for performance improvements using Service Bus]: service-bus-performance-improvements.md
[Best practices for insulating applications against Service Bus outages and disasters]: service-bus-outages-disasters.md
[Pricing overview]: https://azure.microsoft.com/pricing/details/service-bus/
[Quotas overview]: service-bus-quotas.md
[Exceptions overview]: service-bus-messaging-exceptions.md
[Shared Access Signatures]: service-bus-sas.md
