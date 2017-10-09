---
title: "aaaInsulating Azure Service Bus uygulama kesintiler ve olağanüstü karşı | Microsoft Docs"
description: "Olası bir hizmet veri yolu kesinti karşı tooprotect uygulamalar kullanabileceğiniz teknikleri açıklar."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: tysonn
ms.assetid: fd9fa8ab-f4c4-43f7-974f-c876df1614d4
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/12/2017
ms.author: sethm
ms.openlocfilehash: 349b4968456c9f15375753d83495246f5a3ddfdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-insulating-applications-against-service-bus-outages-and-disasters"></a>Hizmet veri yolu kesintileri ve olağanüstü karşı uygulamalar insulating için en iyi uygulamalar
Görev açısından kritik uygulamalar bile hello bulunması planlanmayan kesintiler veya olağanüstü sürekli olarak çalışması gerekir. Bu konu tooprotect hizmet veri yolu uygulamaları potansiyel hizmet kesintisi veya olağanüstü durum karşı kullanabilir teknikleri açıklar.

Bir kesinti hello geçici olarak kullanım dışı kalması Azure hizmet veri yolu tanımlanır. Merhaba kesinti Service Bus Mesajlaşma deposu veya veri merkezinin tamamı bile hello gibi bazı bileşenleri etkileyebilir. Merhaba sorun çözüldükten sonra hizmet veri yolu yeniden kullanılabilir hale gelir. Genellikle, bir kesinti iletileri veya diğer veri kaybına neden olmaz. Belirli bir Mesajlaşma deposu hello kullanılamama bileşeni hatası örnektir. Bir güç kesintisi hello datacenter ya da hatalı veri merkezi ağ anahtarı, bir veri merkezi çapında kesinti örnektir. Bir kesinti birkaç dakika tooa birkaç gün sürebilir.

Bir olağanüstü durum hello kalıcı kaybı bir Service Bus ölçek birimi veya veri merkezi tanımlanır. Merhaba datacenter olabilir ya da yeniden kullanılabilir duruma gelebilir. Genellikle bir olağanüstü durum bazı veya tüm iletileri veya diğer veri kaybına neden olur. Yangın, taşmasını veya deprem afetler örnekleridir.

## <a name="current-architecture"></a>Geçerli mimari
Service Bus tooqueues veya konular gönderilen birden çok Mesajlaşma depoları toostore iletileri kullanır. Bölümlenmemiş kuyruk veya konu deposu Mesajlaşma tooone atanır. Bu ileti deposunu kullanılamıyorsa, kuyruk veya konu tüm işlemler başarısız olur.

Bir veri merkezi ile bağlantılı bir hizmet ad alanındaki tüm Service Bus Mesajlaşma varlıkları (kuyruklar, konular, geçişler) bulunur. Service Bus otomatik coğrafi çoğaltma veri etkinleştirmez veya birden çok veri merkezi bir ad alanı toospan izin vermez.

## <a name="protecting-against-acs-outages"></a>ACS kesintilere karşı koruma
ACS kimlik bilgilerini kullandığını ve ACS kullanılamaz hale, istemciler artık belirteçleri alabilir. Merhaba belirteçleri süresi dolana kadar ACS arıza hello zamanında bir belirteç olan istemcileri toouse Service Bus devam edebilirsiniz. Merhaba varsayılan belirteç ömrü 3 saattir.

ACS kesintilere karşı tooprotect paylaşılan erişim imzası (SAS) belirteçleri kullanın. Bu durumda, hello istemci gizli bir anahtar ile bir kendi kendine minted belirteç imzalama tarafından doğrudan Service Bus ile kimliğini doğrular. Çağrıları tooACS artık gerekli değildir. SAS belirteci hakkında daha fazla bilgi için bkz: [Service Bus kimlik doğrulama][Service Bus authentication].

## <a name="protecting-queues-and-topics-against-messaging-store-failures"></a>Kuyruklar ve konu başlıkları deposu başarısızlıkları Mesajlaşma karşı koruma
Bölümlenmemiş kuyruk veya konu deposu Mesajlaşma tooone atanır. Bu ileti deposunu kullanılamıyorsa, kuyruk veya konu tüm işlemler başarısız olur. A hello üzerinde sıra diğer yandan bölümlenmiş, birden çok parçalarını oluşur. Her parça farklı bir Mesajlaşma deposunda depolanır. Bir ileti tooa bölümlenmiş kuyruk veya konu gönderildiğinde, Service Bus hello ileti tooone hello parçaların atar. Merhaba karşılık gelen ileti deposu kullanılamıyorsa, hizmet veri yolu hello ileti tooa farklı parça, mümkünse yazar. Bölümlenen varlıklar hakkında daha fazla bilgi için bkz: [bölümlenmiş Mesajlaşma varlıkları][Partitioned messaging entities].

## <a name="protecting-against-datacenter-outages-or-disasters"></a>Veri Merkezi kesintilerini veya olağanüstü karşı koruma
tooallow iki veri merkezi arasında bir yük devretme için her veri merkezinde bir Service Bus hizmeti ad alanı oluşturabilirsiniz. Örneğin, Service Bus hizmeti ad alanı hello **contosoPrimary.servicebus.windows.net** hello Amerika Birleşik Devletleri Kuzey/Orta bölgesinde bulunan ve **contosoSecondary.servicebus.windows.net**hello BİZE Güney/Orta bölgesinde bulunan. Service Bus varlık Mesajlaşma bir veri merkezi kesintisinden hello bulunması erişilebilir kalması gereken, varlığın her iki ad alanları oluşturabilirsiniz.

Daha fazla bilgi için "Service Bus Azure veri merkezi içinde hatası" bölümünde hello bkz [zaman uyumsuz desenleri ve yüksek kullanılabilirlik Mesajlaşma][Asynchronous messaging patterns and high availability].

## <a name="protecting-relay-endpoints-against-datacenter-outages-or-disasters"></a>Veri Merkezi kesintilerini veya olağanüstü karşı koruma geçiş uç noktaları
Coğrafi çoğaltma geçiş uç noktaları Service Bus kesintileri hello bulunması erişilebilir bir geçiş uç nokta toobe kullanıma sunan bir hizmet sağlar. tooachieve coğrafi çoğaltma, hello hizmeti farklı ad alanlarında iki geçiş uç noktalar oluşturmanız gerekir. Merhaba ad alanları farklı veri merkezlerinde bulunmalıdır ve hello iki uç nokta adları farklı olmalıdır. Örneğin, birincil bir uç nokta altında ulaşılabilen **contosoPrimary.servicebus.windows.net/myPrimaryService**altında ikincil kendisine karşılık gelen ulaşılabilen yaparken **contosoSecondary.servicebus.windows.net/mySecondaryService**.

Merhaba hizmeti sonra her iki bitiş noktasında dinler ve bir istemci ya da uç noktası aracılığıyla hello hizmet çağırabilirsiniz. Bir istemci uygulaması rastgele birincil endpoint hello gibi hello geçişler birini seçer ve kendi isteği toohello etkin uç gönderir. Merhaba işlemi bir hata kodu ile başarısız olursa, o hello geçiş uç noktası kullanılamıyor bu hatayı gösterir. Merhaba uygulaması bir kanal toohello yedekleme uç nokta açar ve hello isteği yeniden yayımlar. Bu noktada rolleri hello etkin ve hello yedekleme uç noktaları geçiş: Merhaba istemci uygulaması hello eski etkin uç nokta toobe hello yeni yedekleme uç noktası ve hello eski yedekleme endpoint toobe hello yeni etkin uç noktası göz önünde bulundurur. Her ikisi de işlemleri başarısız gönderirseniz hello iki varlık hello rolleri değişmeden kalır ve bir hata döndürdü.

Merhaba [coğrafi çoğaltma ile Service Bus geçişli iletileri] [ Geo-replication with Service Bus relayed Messages] örnek gösterilmektedir nasıl tooreplicate iletir.

## <a name="protecting-queues-and-topics-against-datacenter-outages-or-disasters"></a>Kuyruklar ve konu başlıkları datacenter kesintileri ya da olağanüstü karşı koruma
tooachieve esnekliği kullanarak aracılı Mesajlaşma, veri merkezi kesintilere karşı Service Bus iki yaklaşım destekler: *etkin* ve *pasif* çoğaltma. Belirtilen kuyruk veya konu bir veri merkezi kesintisinden hello bulunması erişilebilir kalması gereken varsa her bir yaklaşım, her iki ad alanları oluşturabilirsiniz. Her iki varlığa hello olabilir aynı adı. Örneğin, birincil bir kuyruk altında ulaşılabilen **contosoPrimary.servicebus.windows.net/myQueue**altında ikincil kendisine karşılık gelen ulaşılabilen yaparken **contosoSecondary.servicebus.windows.net/myQueue**.

Merhaba uygulaması kalıcı gönderenin alıcı iletişim gerektirmiyorsa Merhaba uygulaması bir dayanıklı istemci-tarafı sıra tooprevent ileti kaybına ve tooshield hello gönderenden geçici hizmet veri yolu hataları uygulayabilirsiniz.

## <a name="active-replication"></a>Etkin çoğaltma
Etkin çoğaltma varlıklar her işlem için her iki ad kullanır. Bir ileti gönderen herhangi bir istemci hello iki kopyasını gönderir aynı ileti. Merhaba ilk kopyayı toohello birincil varlık gönderilen (örneğin, **contosoPrimary.servicebus.windows.net/sales**), ve hello ikinci bir kopyası selamlama iletisine toohello ikincil varlık gönderilen (örneğin,  **contosoSecondary.servicebus.windows.net/sales**).

Bir istemci, her iki sıralarından iletilerini alır. ilk iletinin kopyasını Hello alıcısı işlemler hello ve hello ikinci kopya engellenir. toosuppress yinelenen iletileri hello gönderen her iletinin benzersiz bir tanımlayıcı etiketlemeniz gerekir. Her iki kopyasını selamlama iletisine ile Merhaba etiketlenmelidir aynı tanımlayıcısı. Merhaba kullanabilirsiniz [BrokeredMessage.MessageId] [ BrokeredMessage.MessageId] veya [BrokeredMessage.Label] [ BrokeredMessage.Label] özellikleri ya da bir özel özellik tootag hello İleti. Merhaba alıcı zaten aldığı iletileri listesini bulundurmanız gerekir.

Merhaba [Service Bus aracılı iletiler coğrafi çoğaltma] [ Geo-replication with Service Bus Brokered Messages] örnek Mesajlaşma, etkin çoğaltma gösterir.

> [!NOTE]
> Merhaba etkin çoğaltma yaklaşım hello işlemlerinin sayısı iki katına çıkarır, bu nedenle, bu yaklaşım toohigher maliyet yol açabilir.
> 
> 

## <a name="passive-replication"></a>Pasif çoğaltma
Merhaba hataya serbest durumda pasif çoğaltma hello iki Mesajlaşma varlıkları yalnızca birini kullanır. Bir istemci hello ileti toohello etkin varlık gönderir. Merhaba işlem hello etkin varlıkta konakları hello etkin varlık kullanılamayabilir hello datacenter belirten bir hata kodu ile başarısız olursa, hello istemci hello ileti toohello yedekleme varlık bir kopyasını gönderir. Bu noktada hello etkin ve hello yedekleme varlıkları rolleri geçiş: hello gönderen istemci hello eski etkin varlık toobe hello yeni yedekleme varlık göz önünde bulundurur ve hello eski yedekleme varlıktır hello yeni etkin varlık. Her ikisi de işlemleri başarısız gönderirseniz hello iki varlık hello rolleri değişmeden kalır ve bir hata döndürdü.

Bir istemci, her iki sıralarından iletilerini alır. Bir fırsat olduğundan bu hello alıcı aynı iletisi, hello hello iki kopyasını alır alıcı yinelenen iletileri bastırmak gerekir. Gözardı edebileceğini aynı şekilde etkin çoğaltma için açıklandığı gibi hello çoğaltır.

Genel olarak, çoğu durumda yalnızca bir işlem yapıldığından pasif çoğaltma etkin çoğaltma daha ekonomik. Gecikme süresi, üretilen iş ve para maliyet aynı toohello çoğaltılmamış senaryosu verilebilir.

Pasif çoğaltma kullanırken hello aşağıdaki senaryoları iletileri kaybolabilir veya iki kez alındı:

* **İleti gecikme veya kayıp**: hello gönderen bir ileti m1 toohello birincil sırası gönderildi ve ardından hello alıcı m1 almadan önce hello sıra kullanılamaz hale varsayılır. Merhaba gönderen bir sonraki ileti m2 toohello ikincil sırası gönderir. Merhaba birincil kuyruk geçici olarak devre dışı ise, hello sıra yeniden kullanılabilir hale geldikten sonra hello alıcı m1 alır. Bir olağanüstü durumda hello alıcı hiçbir zaman m1 alabilirsiniz.
* **Alma yinelenen**: Bu hello gönderen bir ileti m toohello birincil sırası gönderir varsayalım. Hizmet veri yolu başarıyla m işler ancak toosend yanıt başarısız olur. İşlem zaman aşımına Hello gönderdikten sonra hello gönderen m toohello ikincil sıra özdeş bir kopyasını gönderir. Merhaba alıcı mümkün tooreceive hello ilk kopyasını m ise Hello birincil kuyruk kullanılamaz hale önce hello alıcı yaklaşık hello m ve her iki kopyalarını alan aynı anda. Merhaba birincil kuyruk kullanılamaz hale önce hello alıcı mümkün tooreceive hello ilk kopyasını m değilse, hello alıcı başlangıçta yalnızca hello ikinci bir kopyası m alır, ancak hello birincil kuyruk kullanılabilir hale geldiğinde m ikinci bir kopyasını alır.

Merhaba [coğrafi çoğaltma ile Service Bus aracılı ileti] [ Geo-replication with Service Bus Brokered Messages] örnek Mesajlaşma, pasif çoğaltma gösterir.

## <a name="next-steps"></a>Sonraki adımlar
Olağanüstü durum kurtarma hakkında daha fazla toolearn bu makalelere bakın:

* [Azure SQL veritabanı iş sürekliliği][Azure SQL Database Business Continuity]
* [Azure için esnek uygulamalar tasarlama][Azure resiliency technical guidance]

[Service Bus Authentication]: service-bus-authentication-and-authorization.md
[Partitioned messaging entities]: service-bus-partitioning.md
[Asynchronous messaging patterns and high availability]: service-bus-async-messaging.md#failure-of-service-bus-within-an-azure-datacenter
[Geo-replication with Service Bus Relayed Messages]: http://code.msdn.microsoft.com/Geo-replication-with-16dbfecd
[BrokeredMessage.MessageId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId
[BrokeredMessage.Label]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label
[Geo-replication with Service Bus Brokered Messages]: http://code.msdn.microsoft.com/Geo-replication-with-f5688664
[Azure SQL Database Business Continuity]: ../sql-database/sql-database-business-continuity.md
[Azure resiliency technical guidance]: /azure/architecture/resiliency
