---
title: Azure hizmet veri yolu AMQP 1.0 aaaOverview | Microsoft Docs
description: "Kullanma hakkında bilgi edinin Gelişmiş Message Queuing Protokolü (AMQP) 1.0 azure'da hello."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 0e8d19cc-de36-478e-84ae-e089bbc2d515
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/27/2017
ms.author: sethm
ms.openlocfilehash: c35a20c50dd24845d9a4c7a0251e8240848a6f4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="amqp-10-support-in-service-bus"></a>Hizmet veri yolu AMQP 1.0 desteği
Her ikisi de Azure hizmet veri yolu bulut hizmeti ve şirket içi hello [Windows Server için hizmet veri yolu (hizmet veri yolu 1.1)](https://msdn.microsoft.com/library/dn282144.aspx) destek hello Gelişmiş Message Queuing Protokolü (AMQP) 1.0. AMQP, toobuild platformlar arası, açık bir standart protokol kullanan karma uygulamalar sağlar. Farklı diller ve çerçeveler kullanılarak oluşturulan ve farklı işletim sistemlerinde çalışan bileşenleri kullanan uygulamalar oluşturabilirsiniz. Tüm bu bileşenlerin tooService Bus bağlanabilir ve sorunsuz bir şekilde yapılandırılmış iş iletileri verimli bir şekilde ve tam bir güvenilirlik, exchange.

## <a name="introduction-what-is-amqp-10-and-why-is-it-important"></a>Giriş: AMQP 1.0 nedir ve neden önemlidir?
Geleneksel olarak, ileti odaklı ara yazılım ürünleri istemci uygulamaları ve aracıları arasındaki iletişim için özel protokoller kullanmış. Başka bir deyişle, belirli bir satıcının Mesajlaşma Aracısı seçtikten sonra istemci uygulamaları toothat Aracısı o satıcının kitaplıkları tooconnect kullanmanız gerekir. Bir uygulama tooa farklı ürün taşıma tüm bağlı hello uygulamaları kod değişikliklerini gerektirdiğinden bu satıcıya, bağımlılığı derecesini sonuçlanır. 

Ayrıca, farklı satıcılardan Mesajlaşma aracıları bağlanma hassas. Bu, genellikle uygulama düzeyi köprüleme toomove bir sistem tooanother ve iletileri kendi özel ileti biçimleri arasında tootranslate gerektirir. Bu ortak bir gereksinimdir; Örneğin, ne zaman yeni bir birleştirilmiş arabirimde tooolder farklı sistemleri sağlamak veya gerekir BT sistemleri bir birleşme aşağıdaki tümleştirin.

Merhaba yazılım endüstrisinin hızlı taşınan bir iştir; Yeni programlama dilleri ve uygulama çerçeveleri bazen bewildering hızı sunulur. Benzer şekilde, BT sistemlerinin hello gereksinimleri zamanla gelişmesi ve geliştiricilerin tootake özelliklerinden hello en son platform istiyorsunuz. Ancak, bazen hello seçili Mesajlaşma satıcı bu platformu desteklemez. Mesajlaşma protokolleri özeldir, diğerleri için mümkün değildir, çünkü bu yeni platformlar için tooprovide kitaplıkları. Bu nedenle, ağ geçitleri veya etkinleştirmeniz köprüleri toocontinue toouse hello Mesajlaşma Ürün oluşturma gibi yaklaşımlar kullanmanız gerekir.

Gelişmiş Message Queuing Protokolü (AMQP) 1.0 sorunlardan motive hello Hello geliştirme. JP Morgan olan, en finansal hizmetler firmalarından gibi ileti odaklı Ara ağır kullanıcılarının Chase, kaynaklanan. Merhaba hedef basit: toocreate olası toobuild ileti tabanlı uygulamalar farklı diller, çerçeveler ve işletim sistemleri kullanılarak oluşturulan bileşenleri kullanılarak yapılan bir açık standart Mesajlaşma Protokolü tüm türünün en iyi bileşenlerini kullanan bir Üreticiler aralığı.

## <a name="amqp-10-technical-features"></a>AMQP 1.0 Teknik Özellikleri
AMQP 1.0 toobuild sağlam, platformlar arası ileti gönderme uygulamaları kullanabilirsiniz verimli, güvenilir ve hat düzeyinde bir Mesajlaşma iletişim kuralıdır. Merhaba Protokolü basit bir hedef içeriyor: hello güvenli, güvenilir ve verimli aktarım iletileri iki taraf arasında toodefine hello mekanizması. Merhaba iletilerini kendileri heterojen göndericiler ile alıcılar yapılandırılmış tooexchange iş iletilere göz tam uygunluğunu sağlayan bir taşınabilir veri gösterimi kullanılarak kodlanır. Merhaba, hello en önemli özelliklerin özeti aşağıdadır:

* **Verimli**: AMQP 1.0 protokolüdür Merhaba kodlama ikili kullanır protokol yönergeleri ve iş iletileri aktarılırken hello bir bağlantıya dayalı. Gelişmiş Akış denetimi düzenleri toomaximize hello hello ağ ve kullanımını bağlı hello bileşenleri içerir. Bu, tasarlanmış toostrike verimlilik, esneklik ve birlikte çalışabilirlik arasında bir denge hello Protokolü idi belirtti.
* **Güvenilir**: Merhaba AMQP 1.0 protokolü yangın ve unut tooreliable gelen güvenilirlik garanti aralıklı tam olarak değiştirilen iletileri toobe sağlar-kere teslim onaylanır.
* **Esnek**: AMQP 1.0 olan kullanılan toosupport farklı topoloji olabilir esnek bir protokoldür. Merhaba aynı Protokolü istemci istemci, istemci aracısı ve Aracısı Aracısı iletişimi için kullanılabilir.
* **Aracısı modeli bağımsız**: Merhaba AMQP 1.0 belirtimi yapmaz gereksinimlere aracısı tarafından kullanılan hello Mesajlaşma modeli. Bu mümkün olduğu anlamına gelir tooeasily Mesajlaşma aracıları AMQP 1.0 destek tooexisting ekleyin.

## <a name="amqp-10-is-a-standard-with-a-capital-s"></a>AMQP 1.0 olan bir standart (büyük harf ait olan ')
AMQP 1.0 Uluslararası bir standart olan ISO ve IEC ISO/IEC 19464:2014 olarak onaylandı.

AMQP 1.0 çekirdek Grup 20'den fazla şirketleri tarafından 2008 beri geliştirilmekte açıldı teknolojisi üreticiler ve son kullanıcı firmalarından. Bu süre boyunca kullanıcı firmalarından gerçek iş gereksinimleri katkısı ve hello teknolojisi satıcılar hello Protokolü toomeet gereksinimler gelişim göstermiştir. Merhaba işlemi boyunca bunlar toovalidate hello kendi uygulamalarını işlerliği işbirliği Atölyeleri satıcılar katılan.

Ekim 2011 hello geliştirme iş tooa teknik komitesi hello terfi, yapılandırılmış bilgi standartları (OASIS) Merhaba kuruluş içinde geçti ve hello OASIS AMQP 1.0 standart Ekim 2012'de serbest. Merhaba aşağıdaki firmalarından hello teknik komitesi içinde hello standart hello geliştirme sırasında katılmış:

* **Teknoloji satıcılar**: Axway yazılım, Huawei teknolojileri, IIT yazılım, INETCO sistemleri, Kaazing, Microsoft, Mitre Corporation, Primeton teknolojileri, devam eden yazılım, Red Hat, SITA, yazılım AG, Solace sistemleri, VMware, WSO2, Zenika.
* **Kullanıcı firmalarından**: banka, Amerika, kredi Suisse, Alman Boerse, Goldman Sachs, JPMorgan Chase.

Merhaba bazıları, genellikle açık standartlar avantajları şunlardır bildirdi:

* Daha az olasılığı satıcı kilit açma
* Birlikte çalışabilirlik
* Geniş kullanılabilirliğini kitaplıkları ve araçları
* Kullanım dışı kalma karşı koruma
* Bilgili personel kullanılabilirliği
* Alt ve yönetilebilir riski

## <a name="amqp-10-and-service-bus"></a>AMQP 1.0 ve hizmet veri yolu
Azure hizmet veri yolu AMQP 1.0 desteği hello Service Bus queuing yararlanan şimdi ve yayımlama/aracılı Mesajlaşma özellikleri verimli bir ikili protokolünü kullanarak platformları aralığından abonelik anlamına gelir. Ayrıca, diller, çerçevelerinin ve işletim sistemlerinin bir karışımını kullanılarak oluşturulan bileşenlerden oluşan uygulamalar oluşturabilir.

Merhaba aşağıdaki şekilde bir örnek dağıtımında hangi hello standart Java ileti hizmeti (JMS) API kullanılarak yazılmış Linux üzerinde çalışan Java ve Windows, hizmet veri yolu AMQP 1.0 kullanarak aracılığıyla exchange iletileri üzerinde çalışan .NET istemcilerinin gösterilmektedir.

![][0]

**Şekil 1: platformlar arası Service Bus ve AMQP 1.0 kullanarak ileti gösteren örnek dağıtım senaryosu**

Bu zaman hello toowork Service Bus ile aşağıdaki istemci kitaplıklarından bilinmektedir:

| Dil | Kitaplık |
| --- | --- |
| Java |Apache Qpid Java ileti hizmeti (JMS) istemcisi<br/>IIT yazılım SwiftMQ Java istemcisi |
| C |Apache Qpid Proton-C |
| PHP |Apache Qpid Proton-PHP |
| Python |Apache Qpid Proton-Python |
| C# |AMQP .net Lite |

**Şekil 2: Tablo AMQP 1.0 istemci kitaplıkları**

## <a name="summary"></a>Özet
* AMQP 1.0 toobuild platformlar arası karma uygulamaların kullanabileceği açık, güvenilir bir Mesajlaşma iletişim kuralıdır. AMQP 1.0 bir OASIS standardıdır.
* AMQP 1.0 desteği artık Windows Server için hizmet veri yolu (hizmet veri yolu 1.1) yanı sıra Azure Service Bus içinde kullanılabilir. Fiyatlandırma aynı protokolleri varolan hello hello olur.

## <a name="next-steps"></a>Sonraki adımlar
Toolearn daha hazır mısınız? Aşağıdaki bağlantılar hello ziyaret edin:

* [.NET gelen hizmet veri yolu AMQP ile kullanma]
* [Java'dan hizmet veri yolu AMQP ile kullanma]
* [Bir Azure Linux VM'de Proton-C Apache Qpid yükleme]
* [Windows Server için hizmet veri yolu AMQP]

[0]: ./media/service-bus-amqp-overview/service-bus-amqp-1.png
[.NET gelen hizmet veri yolu AMQP ile kullanma]: service-bus-amqp-dotnet.md
[Java'dan hizmet veri yolu AMQP ile kullanma]: service-bus-amqp-java.md
[Bir Azure Linux VM'de Proton-C Apache Qpid yükleme]: service-bus-amqp-apache.md
[Windows Server için hizmet veri yolu AMQP]: https://msdn.microsoft.com/library/dn574799.aspx
