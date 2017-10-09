---
title: "Azure Service Bus ve Event Hubs Protokolü Kılavuzu'nda aaaAMQP 1.0 | Microsoft Docs"
description: "Protokol Kılavuzu tooexpressions ve Azure Service Bus ve Event Hubs AMQP 1.0 açıklaması"
services: service-bus-messaging,event-hubs
documentationcenter: .net
author: clemensv
manager: timlt
editor: 
ms.assetid: d2d3d540-8760-426a-ad10-d5128ce0ae24
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: clemensv;hillaryc;sethm
ms.openlocfilehash: 882ce0fc84af11d9f61bc95dc3e4db0b67b2b020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# Azure Service Bus ve Event Hubs Protokolü Kılavuzu'nda AMQP 1.0

Hello Message Queuing protokolü 1.0 Gelişmiş zaman uyumsuz olarak, güvenli ve güvenilir bir şekilde iletileri iki taraf arasında aktarmak için bir standart çerçeveleme ve aktarım protokolüdür. Bunu hello Birincil Azure Service Bus Mesajlaşma hizmeti ve Azure Event Hubs protokolüdür. Her iki hizmet de HTTPS destekler. Ayrıca desteklenen hello özel SBMP Protokolü lehinde AMQP aşamalı olarak Sonlandırılmakta.

AMQP 1.0 hello ara yazılım satıcıları, Microsoft ve Red Hat gibi JP Morgan hello finansal hizmetler endüstri temsil eden Chase gibi birçok Mesajlaşma ara yazılım kullanıcılarla birlikte duruma geniş endüstri işbirliği sonucudur. Merhaba teknik Standartlaştırma hello AMQP protokolünü ve uzantı özellikleriyle ilgili OASIS forumudur ve ISO/IEC 19494 olarak uluslararası bir standart olarak resmi onay kazanmıştır.

## Hedefleri

Bu makalede kısaca hello temel kavramlar hello OASIS AMQP teknik komitesi şu anda sonuçlandırılmış taslak uzantısı belirtimleri, küçük bir kümesini birlikte hello AMQP 1.0 Mesajlaşma belirtiminin özetler ve nasıl Azure Service Bus açıklar uygular ve bu belirtimlere bağlı olarak oluşturur.

tüm mevcut AMQP 1.0 istemcisi yığını platform herhangi toobe mümkün toointeract Azure hizmet veri yolu AMQP 1.0 ile birlikte kullanarak herhangi bir geliştirici Hello hedef içindir.

Apache Proton veya AMQP.NET Lite gibi ortak genel amaçlı AMQP 1.0 yığınları zaten tüm çekirdek AMQP 1.0 hareketleri uygulayın. Bu temel hareketleri bazen bir üst düzey API'si ile sarılır; Apache Proton bile iki sunar, kesinlik temelli Messenger API hello ve reaktif rektör API hello.

Tartışma aşağıdaki hello AMQP bağlantıları, oturumları ve bağlantıları ve hello işlenmesini çerçeve aktarımları ve akış denetimi hello Yönetimi hello ilgili yığın (gibi Apache Protonun durgun-C) tarafından işlenir ve kadar varsa özel gerektirmez varsayıyoruz uygulama geliştiricilerinin gelen ilgilenilmesi gerekiyor. Bağlamalarında hello varlığı hello özelliği tooconnect ve toocreate gibi birkaç API elemanlar çeşit varsayıyoruz *gönderen* ve *alıcı* bazışeklinisahipsoyutlamanesneleri`send()`ve `receive()` işlemleri, sırasıyla.

Azure Service Bus, gelişmiş özelliklerini ileti gözatma veya oturumlar, yönetimi gibi ele alırken bu özellikleri AMQP terimleriyle aynı zamanda bu varsayılan API soyutlama üstünde katmanlı sahte bir uygulama olarak açıklanmıştır.

## AMQP nedir?

AMQP çerçeveleme ve aktarım protokolüdür. Çerçeveleme anlamına gelir, bir ağ bağlantısı her iki yönde akmasını ikili veri akışları için yapısı sağlar. Merhaba yapısı için ayrı veri bloğu sayısını adlı, kabul edilebilir açıklıkta sağlar *çerçeveleri*, toobe hello bağlı taraf arasında akar. Merhaba aktarma Özellikleri iletişim kuran her iki taraf çerçeveler zaman aktarılan ve ne zaman aktarımları tam değerlendirilmesi hakkında paylaşılan bir anlayış kurup emin olun.

Hala birkaç ileti aracıları tarafından kullanılmakta olan hello AMQP çalışma grubu tarafından üretilen süresi dolan taslak önceki sürümlerden farklı olarak bir ileti aracısı veya belirli bir topoloji hello varlığını hello çalışma grubunun son ve standartlaştırılmış AMQP 1.0 protokolü belgenizdeki değil ileti Aracısı içindeki varlıklar için.

Merhaba Protokolü gibi Azure Service Bus kuyrukları ve varlıkları, Yayımla/abone ol destekleyen ileti aracıları ile etkileşim için simetrik eşler arası iletişim için kullanılabilir. Bu ayrıca Mesajlaşma altyapısı ile etkileşim için hello Azure Event Hubs ile olduğu gibi hello etkileşim desenleri normal sıralarından farklı olduğu kullanılabilir. Bir Event Hub olayları tooit gönderildiğinde bir kuyruk gibi davranır, ancak olayları ondan okunduğunda daha seri bağlantılı depolama hizmeti gibi davranır; Ayrıca bir bant sürücüsü biraz benzer. Merhaba istemci hello kullanılabilir veri akışa bir uzaklık alır ve ardından bu uzaklık toohello en son kullanılabilir tüm olayları sunulur.

Merhaba AMQP 1.0 protokolü tasarlanmış toobe daha fazla belirtimleri tooenhance özelliklerini etkinleştirme Genişletilebilir ' dir. Bu belgede ele alınan hello üç uzantısı belirtimleri bu gösterilmektedir. Burada hello yerel AMQP TCP bağlantı noktalarını yapılandırma olabilir zor varolan HTTPS/WebSockets altyapı üzerinden iletişim için bir bağlama belirtimi tanımlar nasıl toolayer AMQP WebSockets üzerinden. Bir istek/yanıt hello Mesajlaşma altyapısı ile etkileşmek için şekilde yönetim amacıyla veya tooprovide gelişmiş işlevselliği, hello AMQP yönetim belirtimi için gerekli hello temel etkileşim temelleri tanımlar. Merhaba AMQP talep tabanlı güvenlik belirtimi Federasyon yetkilendirme Modeli tümleştirmesi için tanımlar nasıl tooassociate ve bağlantıları ile ilişkili yetkilendirme belirteçleri yenileyin.

## Temel AMQP senaryoları

Bu bölümde hello temel AMQP 1.0 bağlantıları, oturumları ve bağlantıları oluşturma ve hizmet veri yolu varlıklarını kuyruklar, konu başlıkları ve abonelikler gibi iletileri tooand transfer içeren Azure Service Bus ile kullanımını açıklar.

AMQP nasıl çalıştığı hakkında hello en yetkili kaynak toolearn, hello AMQP 1.0 belirtimi olmakla birlikte hello belirtimi tooprecisely Kılavuzu Uygulama ve tooteach hello Protokolü yazıldı. Bu bölümde, hizmet veri yolu AMQP 1.0 nasıl kullandığını tanımlamak için gerektiği şekilde kadar terminolojisi Tanıtımı odaklanır. Daha kapsamlı bir giriş tooAMQP, yanı sıra daha geniş bir tartışma AMQP 1.0, gözden geçirebilirsiniz [bu video indirmelere][this video course].

### Bağlantıları ve oturumlar

AMQP çağrıları hello programlar iletişim *kapsayıcıları*; bu içeren *düğümleri*, hangi hello iletişim kurmasını olan bu kapsayıcıların içinde varlıklar. Bir kuyruk böyle bir düğüm olabilir. Tek bir bağlantı düğümler arasında birçok iletişim yolları için kullanılabilmesi için AMQP çoğullama için sağlar; Örneğin, bir uygulama istemci aynı anda bir kuyruk ve gönderme tooanother sırası hello aynı alabilir ağ bağlantısı.

![][1]

Merhaba ağ bağlantısı, böylece hello kapsayıcısında sabitlenmiştir. Merhaba istemci rolü dinler ve gelen TCP bağlantılarını kabul hello alıcı rolü'nde, bir giden TCP yuva bağlantı tooa kapsayıcısı yapmadan hello kapsayıcısında tarafından başlatılır. Merhaba bağlantı el sıkışması hello Protokolü sürüm anlaşması, bildirme veya aktarım düzeyi güvenlik (TLS/SSL) ve bir kimlik doğrulama/yetkilendirme el sıkışma SASL üzerinde temel hello bağlantı kapsamda hello kullanımını anlaşması içerir.

Azure hizmet veri yolu her zaman TLS hello kullanımı gerektirir. Merhaba TCP bağlantısı TLS ile Merhaba AMQP Protokolü anlaşması girmeden önce ilk yayılan ve ayrıca TCP bağlantı noktası 5672 üzerinden yapabildiği hello sunucusu zorunlu yükseltmesini hemen sunar bağlantılarını destekler aslına 5671, TCP bağlantı noktası üzerinden bağlantılarını destekler Merhaba AMQP belirlenen modelini kullanarak bağlantı tooTLS. Merhaba AMQP WebSockets bağlama eşdeğer tooAMQP 5671 bağlantıları olan TCP bağlantı noktası 443'ü bir tüneli oluşturur.

Merhaba bağlantı ve TLS ayarlama sonra Service Bus iki SASL mekanizması seçenekleri sunar:

* SASL DÜZ genellikle, kullanıcı adı ve parola kimlik bilgileri tooa sunucusu geçirmek için kullanılır. Hizmet veri yolu adlandırılmış ancak hesapları yok [paylaşılan erişim güvenlik kuralları](service-bus-sas.md), hakları confer ve bir anahtar ile ilişkili. bir kuralın adını Hello hello kullanıcı adı ve başlangıç anahtarı kullanılan (metin Base64 ile kodlanmış olarak) hello parola olarak kullanılır. Kural seçilen hello ile ilişkili hello hakları hello bağlantısından hello işlemlerini yönetir.
* SASL anonim hello istemci daha sonra açıklanan toouse hello talep tabanlı güvenlik (CBS) modeli istediğinde SASL yetkilendirme atlayarak için kullanılır. Bu seçeneği, istemci bağlantısı anonim olarak kısa bir süre sırasında hangi hello istemci yalnızca hello CBS uç noktasıyla etkileşim kurabilen kurulabilir ve hello CBS el sıkışma tamamlamanız gerekir.

Merhaba taşıma bağlantısı kurulduktan sonra Merhaba kapsayıcılara her hello en büyük çerçeve boyutu bildirmek istiyorum toohandle oldukları ve hello bağlantıda etkinlik yoksa boşta kalma zaman aşımından sonra bunlar tek taraflı bağlantısını kesin.

Ayrıca kaç eşzamanlı kanalları desteklenen bildirin. Bir kanal hello bağlantı üzerinde tek yönlü giden, sanal aktarımı yoludur. Bir oturum her hello birbirine kapsayıcıları tooform çift yönlü iletişim yolunun bir kanaldan alır.

Oturumları pencere tabanlı akış denetimi modeli vardır; bir oturum oluşturulduğunda, isteğe bağlı olarak kaç çerçeve içine istekli tooaccept olan taraflara bildirir onun penceresi alırsınız. Merhaba tarafların exchange çerçeveler, aktarılan gibi çerçeve penceresi ve aktarımları hello penceresi dolu olduğunda ve hello pencere sıfırlama veya hello kullanarak genişletilmiş kadar Durdur doldurun *akış performative* (*performative*hello AMQP terimdir hello iki taraf arasında alınıp protokol düzeyi hareketleri için).

Bu pencere tabanlı model kabaca toohello TCP penceresi tabanlı akış denetimi ancak hello yuva içinde hello oturum düzeyinde kavramdır. Böylece yüksek öncelikli trafiği daraltılmış normal trafiği gibi Otoyol express Şerit üzerinde rushed hello için birden fazla eşzamanlı oturum izin verme kavramı protokolün bulunmaktadır.

Azure hizmet veri yolu, her bağlantı için şu anda tam olarak bir oturum kullanır. Hizmet veri yolu en fazla çerçeve boyutu Hello 262.144 (256 K bayt) hizmet veri yolu Standart ve Event Hubs için bayttır. Service Bus Premium için 1.048.576 (1 MB) olur. Hizmet veri yolu, belirli bir oturum düzeyi azaltma windows koymak değil, ancak sıfırlar hello penceresi düzenli olarak bağlantı düzeyi akış denetimi bir parçası olarak (bkz [hello sonraki bölümde](#links)).

Bağlantılar, Kanallar ve oturumları kısa ömürlü. Hello arka plandaki bağlantı, bağlantılar, daraltır, TLS tüneli, SASL yetkilendirme bağlamı ve oturumları kurulmaları gerekir.

### Bağlantılar

AMQP iletileri bağlantıları üzerinden aktarılır. Bir yönde aktarma iletileri sağlayan bir oturumu üzerinden oluşturulan bir iletişim yolu bağlantıdır; Merhaba Aktarım durumu anlaşma hello bağlantısı ve çift yönlü hello bağlı taraflar arasında sona erer.

![][2]

Bağlantılar tarafından ya da kapsayıcı herhangi bir zamanda ve AMQP HTTP ve hello başlatma aktarımları ve aktarım yolu özel bir ayrıcalık oluşturma hello taraf olduğu MQTT dahil birçok diğer protokoller farklı yapar bir varolan oturumu üzerinden oluşturulabilir Merhaba yuva bağlantı.

Merhaba bağlantıyı başlatan kapsayıcı hello kapsayıcı tooaccept ters bağlantı ister ve rol göndereni veya alıcısı olarak seçer. Bu nedenle, kapsayıcı tek yönlü oluşturma başlatabilir ya da hello ikinci ile çift yönlü iletişim yolları bağlantılar çiftleri olarak modellenir.

Bağlantılar adlı ve düğümleri ile ilişkilendirilmiş. Merhaba'den itibaren belirtildiği gibi bir kapsayıcı içindeki varlıklar iletişim hello düğümleri olan.

Hizmet veri yolu, bir düğüm doğrudan eşdeğer tooa kuyruk, konu, bir abonelik veya bir kuyruk veya abonelik sahipsiz sırasına durumdadır. AMQP içinde kullanılan hello düğüm adı bu nedenle hello göreli hello varlık hello Service Bus ad alanı içinde adıdır. Bir kuyruk adlandırılmışsa **Sıram**, ayrıca kendi AMQP düğüm adı olmasıdır. Bir konu aboneliği "abonelikleri" kaynak koleksiyonu ve bu nedenle, bir abonelik sıralanmış tarafından hello HTTP API kuralını izleyen **alt** veya bir konu **mytopic** hello AMQP düğüm adı **abonelikleri/mytopic/alt**.

Merhaba bağlanan ayrıca gerekli toouse bağlantılar oluşturmak için bir yerel düğüm adı istemcidir; Service Bus bu düğüm adları hakkında Düzenleyici değil ve bunları yorumlar değil. AMQP 1.0 istemcisi yığınları genellikle bu kısa ömürlü düğüm adları hello hello istemci kapsamında benzersiz bir şema tooassure kullanın.

### Aktarımları

Bağlantı kurulduktan sonra o bağlantı üzerinden iletileri aktarılabilir. AMQP içinde bir aktarımı ile bir açık Protokolü hareketi yürütülür (Merhaba *aktarımı* performative), bir ileti gönderen tooreceiver bir bağlantı üzerinden taşır. Bir aktarım her iki taraf bu aktarım hello sonucunu paylaşılan bir anlayış kurduktan anlamına gelir, bu "kapatıldığında", tamamlanmış olur.

![][3]

Merhaba en basit durumda, "önceden kapatılmış," toosend iletileri hello istemci hello sonucu ilgilenen değil ve hello alıcı hello işlemi hello sonucunu hakkında herhangi bir geri bildirim sağlamıyor anlamına hello gönderen seçebilirsiniz. Bu mod hello AMQP protokolünü düzeyi Service Bus tarafından desteklenen, ancak hello istemci API hiçbirinde gösterilmeyen.

Merhaba normal iletileri gönderilir kapatılmamış ve hello alıcı sonra gösterir kabul ya da reddetme hello kullanarak durumdur *değerlendirme* performative. Reddetme hello alıcı selamlama iletisine herhangi bir nedenle kabul edilemiyor ve hello reddetme iletisi AMQP tarafından tanımlanan bir hata yapısıdır hello nedeni hakkında bilgi içeren oluşur. Service Bus içinde toointernal hatalar nedeniyle iletileri reddedilirse hello hizmeti destek istekleri dosyalama varsa, tanılama ipuçları toosupport personel sunmak için kullanılabilecek yapıyı içindeki ek bilgi döndürür. Daha sonra hatalar hakkında daha fazla bilgi edineceksiniz.

Özel reddetme hello biçimidir *yayımlanan* durumunda, bu hello alıcı belirten teknik itiraz toohello aktarım var, ancak ayrıca şekilde içinde hiçbir ilgi hello aktarım. Durum, örneğin, bir ileti olduğunda varolduğunu tooa Service Bus istemci teslim edilir ve çok selamlama iletisine "İptal" Merhaba istemci hello ileti işlenirken oluşan hello iş gerçekleştiremiyor çünkü seçer; Merhaba ileti teslimi kendisini hatalı değil. Bir bu duruma hello çeşididir *değiştiren* değişiklikleri toohello ileti serbest olarak veren durumu. Bu durumda, şu anda Service Bus tarafından kullanılmaz.

Merhaba AMQP 1.0 belirtimi tanımlar başka bir değerlendirme adlı durumu *alınan*, özellikle toohandle bağlantı kurtarma yardımcı olan. Bağlantı ve herhangi bir yeni bağlantı ve hello önceki bağlantıyı ve oturum zaman kayboldu oturumu üstünde teslimler bekleyen hello durumunu reconstituting bağlantı kurtarma sağlar.

Hizmet veri yolu bağlantı kurtarma desteklemiyor; Hello istemci kapatılmamış iletisiyle hello bağlantı tooService Bus kaybederse bekleyen Aktarım, bu ileti aktarma kaybolur ve hello istemci gerekir yeniden bağlanma, hello bağlantıyı yeniden kurmak ve hello aktarımı yeniden deneyin.

Bu nedenle, hizmet veri yolu ve Event Hubs "en az bir kez" nerede hello gönderen depolanır ve kabul selamlama iletisine garanti, ancak "tam bir kez" Merhaba hello sistem toorecover burada denenecek AMQP düzeyi aktarmalarına desteklemeyen aktarımları desteği bağlantı hello ve toonegotiate hello teslimat durumu tooavoid çoğaltma hello ileti aktarma devam edin.

olası yinelenen toocompensate gönderir, Service Bus kuyrukları ve konularından isteğe bağlı bir özellik olarak yinelenen algılama destekler. Yinelenen algılama kayıtları gelen tüm iletilerin iletisi kimlikleri bir kullanıcı tanımlı bir zaman penceresi sırasında hello sonra sessizce ile gönderilen tüm iletileri düşme o aynı penceresi sırasında aynı iletisi kimlikleri hello.

### Akış denetimi

Ayrıca toohello oturum düzeyi akış denetimi modeli daha önce ele alınan, her bir bağlantının kendi akış denetimi modeli vardır. Oturum düzeyi akış denetimi bağlantı düzeyi akış denetimi kaç ona bir bağlantıdan istediği toohandle iletileri sorumlu Merhaba uygulaması koyar sonra ve ne zaman toohandle çok fazla kareleri sahip hello kapsayıcı korur.

![][4]

Bir bağlantı aktarımları yalnızca hello göndericisi vardır yeterli ortaya çıkar *bağlantı kredi*. Bağlantı alacak olan hello kullanarak hello alıcı tarafından sayacın *akış* performative, olduğu tooa bağlantı kapsamlı. Merhaba göndereni bağlantı kredi atandığında, iletileri sunarak bu kredi yukarı toouse çalışır. Her ileti teslim azaltır kalan bağlantı kredi 1 ile Merhaba. Merhaba bağlantı alacak kullanıldığı zaman teslimler durdurun.

Hizmet veri yolu hello alıcı rolde olduğunda, böylece iletileri hemen gönderilebilir, Anında hello gönderen geniş bağlantı kredi ile sağlar. Hizmet veri yolu bağlantı alacak kullanıldığı şekilde bazen gönderir bir *akış* performative toohello gönderen tooupdate hello bağlantı kredi bakiyesi.

Hello gönderen rolü'nde, hizmet veri yolu iletileri toouse tüm bekleyen bağlantı kredi yukarı gönderir.

"Alma" çağrısı hello API düzeyinde çevirir bir *akış* performative alma hello tarafından ilk kredi hello istemci tarafından veri yolu ve Service Bus tüketir tooService kullanılabilir gönderilen, kilitleme hello kuyruğundan ileti kilidi ve onu aktarılıyor. Teslimat için kullanıma hazır bir ileti ise tüm bekleyen kredi herhangi bir bağlantıyı tarafından ile belirli varlık varış sırayla kayıtlı olarak kalır, ve iletiler kilitlenir ve kullanılabilir olduklarında, toouse tüm bekleyen kredi aktarılan kurdu.

Merhaba kilidi iletide hello aktarımı hello terminal durumlarından birine kapatıldığında de serbest *kabul*, *reddetti*, veya *serbest*. Selamlama iletisine hello terminal durumuna olduğunda hizmet yolundan kaldırılıyor *kabul*. Hizmet veri yolundaki kalır ve hello aktarımı hello herhangi diğer durumları ulaştığında toohello sonraki alıcı teslim edilir. Merhaba varlık son toorepeated redleri veya yayımları için izin verilen hello maksimum teslimat sayısı ulaştığında Service Bus hello varlığın sahipsiz sıraya selamlama iletisine otomatik olarak taşır.

Hello Service Bus API'lerine değil doğrudan kullanıma olsa bile bu tür bir seçenek Bugün, alt düzey AMQP protokolünü istemci kredi her alma isteği için bir ölçü "stili itme" modeline veren, hello bağlantı kredi modeli tooturn hello "çekme stili" etkileşim kullanabilir göndererek çok sayıda bağlantı KREDİLERİ ve daha fazla etkileşimi kullanılabilir olduklarında iletileri alacak. Anında iletme hello desteklenen [MessagingFactory.PrefetchCount](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_PrefetchCount) veya [MessageReceiver.PrefetchCount](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_PrefetchCount) özelliğini ayarlar. Sıfır olmayan olduklarında hello AMQP istemcisi hello bağlantı alacak olarak kullanır.

Merhaba ileti hello varlıktan selamlama iletisine zaman hello kablo put değil alındığında bu bağlamda hello kilit hello varlık içindeki hello iletideki hello sona erme saati Merhaba, önemli toounderstand başlatır. Merhaba istemci bağlantı kredi vererek hazırlık tooreceive iletileri gösterir. her, bu nedenle beklenen toobe etkin olarak çekilmesini iletileri hello ağ üzerinden hazır toohandle kullanılabilir ve bunları. Aksi takdirde selamlama iletisine bile teslim edilmeden önce hello ileti kilit dolmuş olabilir. bağlantı kredi akış denetimi Hello kullanarak doğrudan hello hemen hazırlık toodeal gönderilen kullanılabilir iletiler toohello alıcı ile yansıtmalıdır.

Özet olarak, hello aşağıdaki bölümler hello performative akış şematik bir genel bakış farklı API etkileşimleri sırasında sağlar. Her bölümde farklı bir mantıksal işlem açıklanmaktadır. Bu etkileşimler bazıları "yavaş bunlar yalnızca gerekli olduğunda gerçekleştirilebilir anlamına gelir," olabilir. Merhaba ilk ileti gönderilen ya da istenen kadar bir ileti gönderen oluşturma ağ etkileşim neden.

Aşağıdaki tablonun hello Hello okları hello performative akış yönü gösterir.

#### İleti alıcı oluşturma

| İstemci | Service Bus |
| --- | --- |
| --> () ekleme<br/>adı = {bağlantı adı}<br/>tanıtıcı {sayısal tanıtıcı} =<br/>Rol =**alıcı**,<br/>Kaynak = {varlık adı}<br/>Hedef = {istemci bağlantı kimliği}<br/>) |İstemci tooentity alıcısı olarak ekler. |
| Hizmet veri yolu yanıt hello bağlantı kendi sonuna ekleme |<--ekleme ()<br/>adı = {bağlantı adı}<br/>tanıtıcı {sayısal tanıtıcı} =<br/>Rol =**gönderen**,<br/>Kaynak = {varlık adı}<br/>Hedef = {istemci bağlantı kimliği}<br/>) |

#### İleti göndereni oluşturma

| İstemci | Service Bus |
| --- | --- |
| --> () ekleme<br/>adı = {bağlantı adı}<br/>tanıtıcı {sayısal tanıtıcı} =<br/>Rol =**gönderen**,<br/>Kaynak = {istemci bağlantı kimliği}<br/>Hedef = {varlık adı}<br/>) |Eylem yok |
| Eylem yok |<--ekleme ()<br/>adı = {bağlantı adı}<br/>tanıtıcı {sayısal tanıtıcı} =<br/>Rol =**alıcı**,<br/>Kaynak = {istemci bağlantı kimliği}<br/>Hedef = {varlık adı}<br/>) |

#### İletiyi gönderen (hata) oluşturma

| İstemci | Service Bus |
| --- | --- |
| --> () ekleme<br/>adı = {bağlantı adı}<br/>tanıtıcı {sayısal tanıtıcı} =<br/>Rol =**gönderen**,<br/>Kaynak = {istemci bağlantı kimliği}<br/>Hedef = {varlık adı}<br/>) |Eylem yok |
| Eylem yok |<--ekleme ()<br/>adı = {bağlantı adı}<br/>tanıtıcı {sayısal tanıtıcı} =<br/>Rol =**alıcı**,<br/>Kaynak = null,<br/>Hedef = null<br/>)<br/><br/><--detach ()<br/>tanıtıcı {sayısal tanıtıcı} =<br/>Kapalı =**doğru**,<br/>hata = {hata bilgisini}<br/>) |

#### İletiyi Kapat alıcı/gönderen

| İstemci | Service Bus |
| --- | --- |
| --> detach ()<br/>tanıtıcı {sayısal tanıtıcı} =<br/>Kapalı =**true**<br/>) |Eylem yok |
| Eylem yok |<--detach ()<br/>tanıtıcı {sayısal tanıtıcı} =<br/>Kapalı =**true**<br/>) |

#### Gönder (başarılı)

| İstemci | Service Bus |
| --- | --- |
| Aktarım (--><br/>teslim kimliği = {sayısal tanıtıcı}<br/>teslim etiketi {ikili tanıtıcı} =<br/>Kapatılan =**false**,, daha =**yanlış**,<br/>Durum =**null**,<br/>sürdürme =**false**<br/>) |Eylem yok |
| Eylem yok |<--değerlendirme ()<br/>Rol alıcı =<br/>ilk = {teslim kimliği}<br/>Son = {teslim kimliği}<br/>Kapatılan =**doğru**,<br/>Durum =**kabul edildi**<br/>) |

#### Gönder (hata)

| İstemci | Service Bus |
| --- | --- |
| Aktarım (--><br/>teslim kimliği = {sayısal tanıtıcı}<br/>teslim etiketi {ikili tanıtıcı} =<br/>Kapatılan =**false**,, daha =**yanlış**,<br/>Durum =**null**,<br/>sürdürme =**false**<br/>) |Eylem yok |
| Eylem yok |<--değerlendirme ()<br/>Rol alıcı =<br/>ilk = {teslim kimliği}<br/>Son = {teslim kimliği}<br/>Kapatılan =**doğru**,<br/>Durum =**reddetti**()<br/>hata = {hata bilgisini}<br/>)<br/>) |

#### Al

| İstemci | Service Bus |
| --- | --- |
| Akış (--><br/>bağlantı kredi = 1<br/>) |Eylem yok |
| Eylem yok |< Aktarım ()<br/>teslim kimliği = {sayısal tanıtıcı}<br/>teslim etiketi {ikili tanıtıcı} =<br/>Kapatılan =**yanlış**,<br/>Daha fazla =**yanlış**,<br/>Durum =**null**,<br/>sürdürme =**false**<br/>) |
| Değerlendirme (--><br/>Rol =**alıcı**,<br/>ilk = {teslim kimliği}<br/>Son = {teslim kimliği}<br/>Kapatılan =**doğru**,<br/>Durum =**kabul edildi**<br/>) |Eylem yok |

#### Çok iletisi alıyorsunuz

| İstemci | Service Bus |
| --- | --- |
| Akış (--><br/>bağlantı kredi = 3<br/>) |Eylem yok |
| Eylem yok |< Aktarım ()<br/>teslim kimliği = {sayısal tanıtıcı}<br/>teslim etiketi {ikili tanıtıcı} =<br/>Kapatılan =**yanlış**,<br/>Daha fazla =**yanlış**,<br/>Durum =**null**,<br/>sürdürme =**false**<br/>) |
| Eylem yok |< Aktarım ()<br/>teslim kimliği = {sayısal tanıtıcı + 1}<br/>teslim etiketi {ikili tanıtıcı} =<br/>Kapatılan =**yanlış**,<br/>Daha fazla =**yanlış**,<br/>Durum =**null**,<br/>sürdürme =**false**<br/>) |
| Eylem yok |< Aktarım ()<br/>teslim kimliği = {sayısal tanıtıcı + 2}<br/>teslim etiketi {ikili tanıtıcı} =<br/>Kapatılan =**yanlış**,<br/>Daha fazla =**yanlış**,<br/>Durum =**null**,<br/>sürdürme =**false**<br/>) |
| Değerlendirme (--><br/>Rol alıcı =<br/>ilk = {teslim kimliği}<br/>Son = {teslim kimliği + 2}<br/>Kapatılan =**doğru**,<br/>Durum =**kabul edildi**<br/>) |Eylem yok |

### İletiler

Merhaba aşağıdaki bölümlerde hangi özellikleri hello standart AMQP ileti bölümlerin Service Bus tarafından kullanılır ve bunların toohello hizmet veri yolu API'sini Ayarla nasıl eşleneceğine açıklanmaktadır.

#### üst bilgi

| Alan adı | Kullanım | API adı |
| --- | --- | --- |
| dayanıklı |- |- |
| Öncelik |- |- |
| TTL |Bu ileti için toolive zamanı |[TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive) |
| ilk alıcı |- |- |
| Teslimat sayısı |- |[DeliveryCount](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_DeliveryCount) |

#### properties

| Alan adı | Kullanım | API adı |
| --- | --- | --- |
| ileti kimliği |Bu ileti uygulama tanımlı, serbest biçimli tanımlayıcısı. Yinelenen algılama için kullanılır. |[MessageID](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId) |
| Kullanıcı Kimliği |Service Bus tarafından yorumlanan değil, uygulama tanımlı kullanıcı tanımlayıcısı. |Merhaba hizmet veri yolu API'si üzerinden erişilebilir değil. |
| çok|Service Bus tarafından yorumlanan değil, uygulama tanımlı hedef tanımlayıcısı. |[Hedef](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_To) |
| Konu |Service Bus tarafından yorumlanan değil, uygulama tanımlı ileti amacı tanımlayıcısı. |[Etiket](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) |
| yanıt çok|Uygulama tanımlı yanıt yolu göstergesi, Service Bus tarafından yorumlanan değil. |[ReplyTo](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_ReplyTo) |
| Bağıntı Kimliği |Service Bus tarafından yorumlanan değil, uygulama tanımlı bağıntı tanımlayıcısı. |[Correlationıd değeri](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_CorrelationId) |
| içerik türü |Uygulama tanımlı içerik türü göstergesi hello gövdesi, hizmet veri yolu tarafından yorumlanan değil. |[ContentType](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_ContentType) |
| İçerik kodlama |Uygulama tanımlı içerik kodlama göstergesi hello gövdesi, hizmet veri yolu tarafından yorumlanan değil. |Merhaba hizmet veri yolu API'si üzerinden erişilebilir değil. |
| mutlak bitiş zamanı |Bildirir hangi mutlak anlık hello ileti süresi dolar. Giriş (TTL gözlenen başlığı), göz ardı çıktıyı yetkili. |[ExpiresAtUtc](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_ExpiresAtUtc) |
| oluşturma zamanı |Bildirir hangi zaman hello ileti oluşturuldu. Service Bus tarafından kullanılmıyor |Merhaba hizmet veri yolu API'si üzerinden erişilebilir değil. |
| Grup Kimliği |Uygulama tanımlı ilgili bir dizi ileti tanımlayıcısı. Hizmet veri yolu oturumları için kullanılır. |[SessionID](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId) |
| Grup Sırası |Bir oturumu içinde selamlama iletisine Hello göreli sıra numarasını tanımlayan sayacı. Service Bus tarafından yoksayılır. |Merhaba hizmet veri yolu API'si üzerinden erişilebilir değil. |
| yanıt için Grup Kimliği |- |[ReplyToSessionId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_ReplyToSessionId) |

## Gelişmiş Service Bus özellikleri

Bu bölüm, Azure Service Bus'ın hello OASIS teknik komitesi AMQP için şu anda geliştirilmekte taslak uzantıları tooAMQP dayalı gelişmiş özelliklerini kapsar. Service Bus bu Taslaklar en son sürümlerini hello uygular ve bu Taslaklar standart durumuna ulaşmasını olarak sunulan değişiklikler devralır.

> [!NOTE]
> Service Bus Mesajlaşma hizmeti Gelişmiş işlemler istek/yanıt modeli aracılığıyla desteklenir. Bu işlemler Hello ayrıntılarını hello belgede açıklanan [hizmet veri yolu AMQP 1.0: istek-yanıt tabanlı işlemleri](service-bus-amqp-request-response.md).
> 
> 

### AMQP Yönetimi

Merhaba AMQP yönetim belirtimi hello olan ilk burada tartışılan hello taslak uzantıları. Bu belirtimi altyapı AMQP Mesajlaşma hello ile yönetim etkileşimleri izin AMQP protokolünü hello üzerinde katmanlanmış Protokolü hareketleri kümesini tanımlar. Merhaba belirtimi tanımlayan genel işlemleri gibi *oluşturma*, *okuma*, *güncelleştirme*, ve *silmek* içindeki varlıklar yönetmek için bir ileti altyapısı ve sorgu işlemleri kümesi.

Bu hareketleri hello istemci hello Mesajlaşma altyapısı arasında bir istek/yanıt etkileşimi gerektirir ve bu nedenle nasıl toomodel Bu etkileşim desen AMQP üstünde hello belirtimi tanımlar: hello istemci bağlanır toohello Mesajlaşma Altyapı, bir oturum başlatır ve bağlantıları çifti oluşturur. Bir bağlantıyı hello istemci gönderen olarak davranır ve alıcı, böylece bir çift yönlü kanalı olarak davranıp bağlantıları oluşturma gibi davranır hello diğer.

| Mantıksal işlemi | İstemci | Service Bus |
| --- | --- | --- |
| İstek yanıt yolu oluşturun |--> () ekleme<br/>adı = {*bağlantı adı*},<br/>tanıtıcı = {*sayısal tanıtıcı*},<br/>Rol =**gönderen**,<br/>Kaynak =**null**,<br/>target = "myentity / $management"<br/>) |Eylem yok |
| İstek yanıt yolu oluşturun |Eylem yok |\<--ekleme ()<br/>adı = {*bağlantı adı*},<br/>tanıtıcı = {*sayısal tanıtıcı*},<br/>Rol =**alıcı**,<br/>Kaynak = null,<br/>target = "myentity"<br/>) |
| İstek yanıt yolu oluşturun |--> () ekleme<br/>adı = {*bağlantı adı*},<br/>tanıtıcı = {*sayısal tanıtıcı*},<br/>Rol =**alıcı**,<br/>Kaynak = "myentity / $management"<br/>target = "myclient$ kimliği"<br/>) | |
| İstek yanıt yolu oluşturun |Eylem yok |\<--ekleme ()<br/>adı = {*bağlantı adı*},<br/>tanıtıcı = {*sayısal tanıtıcı*},<br/>Rol =**gönderen**,<br/>Kaynak "myentity" =<br/>target = "myclient$ kimliği"<br/>) |

Bu bağlantılar çiftinin hazır olması, hello istek/yanıt uygulama basittir: tooan varlık bu deseni anlar hello Mesajlaşma altyapısı içinde gönderilen bir ileti isteğidir. Bu istek iletisinde hello *Yanıtla* hello alanındaki *özellikleri* bölüm toohello ayarlanmış *hedef* hangi toodeliver hello yanıt üzerine hello bağlantı için tanımlayıcı. Varlık işleme hello hello isteği işler ve ardından sunuyor hello yanıt hello üzerinden bağlantı özelliği *hedef* tanımlayıcısıyla eşleşip belirtilen hello *Yanıtla* tanımlayıcısı.

Merhaba düzeni açıkça hello istemci kapsayıcı ve hello istemci tarafından oluşturulan tanımlayıcısını hello yanıt hedef için tüm istemciler arasında ve güvenlik nedenleriyle, ayrıca zor toopredict benzersiz olmasını gerektirir.

Merhaba ileti alışverişlerinde hello Yönetim Protokolü ve diğer tüm protokoller için aynı düzeni hello uygulama düzeyinde gerçekleşir, kullanım hello kullanılan; Yeni AMQP protokol düzeyi hareketleri tanımlamayın. Böylece uygulamaları hemen, bu uzantıları ile uyumlu AMQP 1.0 yığınları yararlanabilir bilerek, olmasıdır.

Hizmet veri yolu şu anda hello yönetim belirtimi hello çekirdek özelliklerinden herhangi birini, ancak uygulamaz hello yönetim belirtim tarafından tanımlanan hello istek/yanıt düzeni hello talep tabanlı güvenlik özelliği ve neredeyse tüm için temel Gelişmiş özellikleri hello aşağıdaki bölümlerde ele alınan hello.

### Talep tabanlı yetkilendirme

Merhaba AMQP talep tabanlı yetkilendirme (CBS) belirtimi taslak hello yönetim belirtimi istek/yanıt desenine oluşturur ve nasıl toouse güvenlik belirteçleri AMQP ile Federasyon için genelleştirilmiş bir modeli açıklanmaktadır.

Merhaba varsayılan güvenlik modelini hello girişte ele alınan AMQP SASL üzerinde temel alır ve hello AMQP bağlantı el sıkışması ile tümleşir. SASL kullanarak kendisi için bir dizi mekanizmaları tanımlanmışsa, resmi olarak SASL üzerinde leans herhangi bir iletişim kuralı yararlanabilir gelen genişletilebilir bir modeli sağlar hello avantajına sahiptir. Bu arasında "DÜZ" kullanıcı adları ve parolalar, "Dış" toobind tooTLS düzeyi güvenlik, "Anonim" tooexpress hello yokluğu açık kimlik doğrulama/yetkilendirme ve çok çeşitli izin ek mekanizmaları aktarımı için mekanizmalardır kimlik doğrulama ve/veya yetkilendirme kimlik bilgileri veya belirteçleri geçirme.

AMQP'ın SASL tümleştirme iki sakıncaları vardır:

* Tüm kimlik bilgilerini ve belirteçleri kapsamlı toohello bağlantı var. Bir ileti altyapısı varlık başına temelinde Ayrıştırılan tooprovide erişim denetim isteyebilirsiniz; Örneğin, hello taşıyıcı belirteci toosend tooqueue A ancak tooqueue B. izin verme Merhaba bağlantıda bağlantılı hello yetkilendirme bağlamına sahip tek bir bağlantı olası toouse olduğundan ve henüz sırası A ve b sırası için farklı erişim belirteçleri kullanın
* Erişim belirteçleri genellikle yalnızca sınırlı bir süre için geçerlidir. Bu geçerlilik hello kullanıcı tooperiodically yeniden Al belirteçleri gerektirir ve hello kullanıcının erişim izinleri değiştirdiyseniz, yeni bir belirteç veren bir fırsat toohello Belirteç Verenin toorefuse sağlar. AMQP bağlantıları uzun süreler için son. Merhaba SASL yalnızca bir fırsat tooset bir belirteç Mesajlaşma altyapısı ya da hello anlamına sahip toodisconnect hello istemci hello belirtecinin süresi dolduğunda mı yoksa tooaccept hello riski, ile sürekli iletişimine izin vermeniz gerekiyor bağlantı sırasında modelidir bir İstemci kimin olan erişim haklarını hello Ara iptal.

Service Bus tarafından uygulanan hello AMQP CBS belirtimi, hem de bu sorunları zarif bir çözüm sağlar: bir istemcinin her düğüm ve bu belirteçler, hello ileti akışı kesintiye uğratmadan süresi dolmadan önce tooupdate ile tooassociate erişim belirteçleri sağlar.

CBS tanımlar adlı bir sanal yönetim düğümü *$cbs*, hello Mesajlaşma altyapısı tarafından sağlanan toobe. Merhaba yönetim düğümü altyapı Mesajlaşma hello içindeki diğer düğümlere adına belirteçleri kabul eder.

Merhaba Protokolü hareketi hello yönetim belirtim tarafından tanımlanan istek/yanıt exchange ' dir. Merhaba bağlantılarıyla çifti anlamına gelir istemci hello kurar *$cbs* düğümünü ve ardından üzerinde bir istekte hello giden bağlantı ve hello yanıt bekler geçişleri hello gelen bağlantı.

Merhaba istek iletisi hello aşağıdaki uygulama özelliklere sahiptir:

| Anahtar | İsteğe bağlı | Değer türü | Değer içeriği |
| --- | --- | --- | --- |
| işlemi |Hayır |Dize |**PUT-token** |
| type |Hayır |Dize |Merhaba belirtecin koyulmuş Hello türü. |
| ad |Hayır |Dize |Merhaba "İzleyici" toowhich hello belirteci geçerlidir. |
| süre sonu |Evet |timestamp |Merhaba belirteci Hello süre sonu zamanı. |

Merhaba *adı* özelliği ile hangi hello belirteci olacaktır ilişkili hello varlık tanımlar. Service Bus içinde kullanıcının hello yolu toohello kuyruk veya konu başlığının/aboneliğinin. Merhaba *türü* özelliği hello belirteç türü tanımlar:

| Belirteç türü | Belirteç açıklaması | Gövde türü | Notlar |
| --- | --- | --- | --- |
| amqp:jwt |JSON Web Token (JWT) |AMQP değeri (dize) |Henüz kullanılamıyor. |
| amqp:swt |Basit Web Token (SWT) |AMQP değeri (dize) |Yalnızca desteklenen AAD/ACS tarafından yayınlanan SWT belirteçleri için |
| servicebus.Windows.NET:sastoken |Hizmet veri yolu SAS belirteci |AMQP değeri (dize) |- |

Belirteçleri hakları confer. Hizmet veri yolu bilir üç temel hakları hakkında: "Gönderme" etkinleştirir gönderme, "Dinleme" alma sağlar ve "Manage" bulmada varlıklar sağlar. AAD/ACS tarafından açıkça yayınlanan SWT belirteçleri talepler olarak bu hakları içerir. Hizmet veri yolu SAS belirteci hello ad alanı veya varlık yapılandırılan toorules başvurun ve bu kuralları haklarıyla yapılandırılır. Bu kuralla ilişkili hello anahtar imzalama hello belirteciyle böylece hello belirteci express hello ilgili hakları yapar. bir varlık kullanımıyla ilişkili hello belirteci *put belirteci* verir hello hello varlıkla hello belirteci hakları başına istemci toointeract bağlı. Burada hello istemci alır hello üzerinde bir bağlantı *gönderen* rolünü hello üzerinde alma sağ; "Gönderme" Merhaba gerektiren *alıcı* rolünün hello "Dinleme" hakkı olması gerekir.

Merhaba yanıt iletisi sahip hello aşağıdaki *uygulama özellikleri* değerleri

| Anahtar | İsteğe bağlı | Değer türü | Değer içeriği |
| --- | --- | --- | --- |
| Durum kodu |Hayır |Int |HTTP yanıt kodunu **[RFC2616]**. |
| Durum açıklaması |Evet |Dize |Merhaba durum açıklaması. |

Merhaba istemci çağırabilir *put belirteci* art arda ve hello Mesajlaşma altyapısı herhangi bir varlık için. kapsamlı toohello geçerli istemci Hello belirteçler olan ve hello bağlantı düştüğünde hello geçerli bağlantıda bağlantılı, anlamı hello sunucu tutulan herhangi bir belirtece bırakır.

Merhaba geçerli hizmet veri yolu uygulaması hello SASL yöntemi "Anonim" ile birlikte CBS yalnızca sağlar. SSL/TLS bağlantısı her zaman önceki toohello SASL el sıkışma mevcut olması gerekir.

Merhaba anonim mekanizması bu nedenle AMQP 1.0 istemcisi seçilen hello tarafından desteklenmesi gerekir. İlk bağlantı el sıkışması hello ilk oturum oluşturma dahil olmak üzere, hello anonim erişim anlamına gelir, hizmet veri yolu kimin hello bağlantı oluşturma bilerek olur.

Merhaba bağlantı ve oturum kurulduğunda sonra hello ekleme toohello bağlantıları *$cbs* düğümü ve hello gönderme *put belirteci* isteği olan hello işlemlerine izin yalnızca. Geçerli bir belirteci kullanarak başarıyla ayarlanmalıdır bir *put belirteci* isteği hello bağlantı kurulduktan sonra bazı 20 saniye içinde varlık düğümü için aksi hello bağlantısı tek taraflı Service Bus tarafından bırakılır.

Merhaba istemci belirteci süre sonu izlemek için daha sonra sorumludur. Bir belirtecinin süresi dolduğunda, Service Bus hello bağlantı toohello ilgili varlık üzerinde derhal tüm bağlantılar bırakır. tooprevent Bu, hello istemci yerine hello belirteci hello düğüm için yeni bir sanal hello aracılığıyla herhangi bir zamanda ile *$cbs* yönetim düğümüyle aynı hello *put belirteci* hareket ve hello'olmadan alma Merhaba yük yolu o akışları farklı bağlantıları üzerinden trafiği.

## Sonraki adımlar

AMQP, hakkında daha fazla toolearn bağlantılar aşağıdaki hello ziyaret edin:

* [Hizmet veri yolu AMQP genel bakış]
* [AMQP 1.0 desteği bölümlenmiş Service Bus kuyrukları ve konuları]
* [Windows Server için hizmet veri yolu AMQP]

[this video course]: https://www.youtube.com/playlist?list=PLmE4bZU0qx-wAP02i0I7PJWvDWoCytEjD
[1]: ./media/service-bus-amqp-protocol-guide/amqp1.png
[2]: ./media/service-bus-amqp-protocol-guide/amqp2.png
[3]: ./media/service-bus-amqp-protocol-guide/amqp3.png
[4]: ./media/service-bus-amqp-protocol-guide/amqp4.png

[Hizmet veri yolu AMQP genel bakış]: service-bus-amqp-overview.md
[AMQP 1.0 desteği bölümlenmiş Service Bus kuyrukları ve konuları]: service-bus-partitioned-queues-and-topics-amqp-overview.md
[Windows Server için hizmet veri yolu AMQP]: https://msdn.microsoft.com/library/dn574799.aspx
