---
title: "Bağlı fabrika bakım çözüm kılavuzu - Azure | Microsoft Docs"
description: "Önceden yapılandırılmış Azure IoT Bağlı fabrika çözümü ve mimarisinin açıklaması."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 31fe13af-0482-47be-b4c8-e98e36625855
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/12/2017
ms.author: dobett
ms.openlocfilehash: 88fe50460baf8b7180da113b33a03120f39cf44f
ms.sourcegitcommit: aaba209b9cea87cb983e6f498e7a820616a77471
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/12/2017
---
# <a name="connected-factory-preconfigured-solution-walkthrough"></a>Önceden yapılandırılmış bağlı fabrika çözüm kılavuzu

Önceden yapılandırılmış IoT Paketi Bağlı fabrika [çözümü][lnk-preconfigured-solutions], aşağıdaki özellikleri sunan uçtan uca endüstriyel bir çözümün uygulamasıdır:

* Hem sanal fabrika üretim hatlarında OPC UA sunucuları çalıştıran sanal endüstriyel cihazlara hem de gerçek OPC UA sunucu cihazlarına bağlanır. OPC UA hakkında daha fazla bilgi için bkz. [Connected factory SSS](iot-suite-faq-cf.md).
* Bu cihazların ve üretim hatlarının işlem KPI ve OEE değerlerini gösterir.
* OPC UA sunucu sistemleri ile etkileşimde bulunmak için bulut tabanlı bir uygulamanın nasıl kullanılabileceğini gösterir.
* Kendi OPC UA sunucu cihazlarınıza bağlanmanızı sağlar.
* OPC UA sunucu verilerine göz atıp verileri değiştirmenizi sağlar.
* OPC UA sunucularınızdan verilerin özelleştirilmiş görünümlerini sağlamak üzere Azure Zaman Serisi Görüşleri (TSI) hizmetiyle tümleştirilir.

Çözümü kendi uygulamanız için bir başlangıç noktası olarak kullanabilir ve özel iş gereksinimlerinizi karşılayacak şekilde [özelleştirebilirsiniz][lnk-customize].

Bu makalede Bağlı fabrika çözümünün nasıl çalıştığını anlamanız için çözümün temel öğelerinden bazıları açıklanmaktadır. Makale aynı zamanda çözümdeki veri akışını açıklar. Bu bilgiler şunları yapmanıza yardımcı olur:

* Çözümdeki sorunları giderme.
* Çözümü kendinize özel gereksinimleri karşılayacak şekilde nasıl özelleştireceğinizi planlama.
* Azure hizmetlerini kullanan kendi IoT çözümünüzü tasarlama.

Daha fazla bilgi için bkz. [Connected factory SSS](iot-suite-faq-cf.md).

## <a name="logical-architecture"></a>Mantıksal mimari

Aşağıdaki diyagram önceden yapılandırılmış çözümün mantıksal bileşenlerinin ana hatların vermektedir:

![Bağlı fabrika mantıksal mimarisi][connected-factory-logical]

## <a name="communication-patterns"></a>Kimlik doğrulaması desenleri

Çözüm, OPC UA telemetri verilerini JSON biçiminde IoT Hub’a göndermek için [OPC UA Pub/Sub belirtimini](https://opcfoundation.org/news/opc-foundation-news/opc-foundation-announces-support-of-publish-subscribe-for-opc-ua/) kullanır. Çözüm bu amaçla [OPC Yayımcısı](https://github.com/Azure/iot-edge-opc-publisher) IoT Edge modülünü kullanır.

Çözüm ayrıca şirket içi OPC UA sunucuları ile bağlantı kurabilen bir web uygulaması ile tümleşik OPC UA istemcisine sahiptir. İstemci bir [ters proxy](https://wikipedia.org/wiki/Reverse_proxy) kullanır ve şirket içi güvenlik duvarında bağlantı noktası açmayı gerektirmeksizin bağlantıyı oluşturmak için IoT Hub’dan yardım alır. Bu iletişim deseni [hizmet destekli iletişim](https://blogs.msdn.microsoft.com/clemensv/2014/02/09/service-assisted-communication-for-connected-devices/) olarak adlandırılır. Çözüm bu amaçla [OPC Proxy](https://github.com/Azure/iot-edge-opc-proxy/) IoT Edge modülünü kullanır.


## <a name="simulation"></a>Benzetim

Sanal istasyonlar ve sanal üretim yürütme sistemleri (MES) bir fabrikanın üretim hattını oluşturur. Sanal cihazlar ve OPC Yayımcı Modülü, OPC Fundation tarafından yayımlanan [OPC UA .NET Standardı][lnk-OPC-UA-NET-Standard]’nı temel alır.

OPC Proxy ve OPC Yayımcısı [Azure IoT Edge][lnk-Azure-IoT-Gateway]'i temel alan modüller olarak uygulanır. Her sanal üretim hattına bağlı, atanmış bir ağ geçidi bulunur.

Tüm benzetim bileşenleri bir Azure Linux VM’sinde barındırılan Docker kapsayıcıları içinde çalışır. Benzetim, varsayılan olarak sekiz sanal üretim hattını çalıştırmak üzere yapılandırılmıştır.

## <a name="simulated-production-line"></a>Sanal üretim hattı

Üretim hattı, parça üretir. Farklı istasyonlardan oluşur: derleme istasyonu, test istasyonu ve paketleme istasyonu.

Benzetim çalışır, OPC UA düğümleri aracılığıyla gösterilen verileri çalıştırır ve güncelleştirir. Tüm sanal üretim hattı istasyonları, OPC UA aracılığıyla MES tarafından düzenlenir.

## <a name="simulated-manufacturing-execution-system"></a>Sanal üretim yürütme sistemi

MES, istasyon durumu değişikliklerini algılamak üzere üretim hattındaki her bir istasyonu OPC UA aracılığıyla izler. İstasyonları denetlemek üzere OPC UA yöntemlerini çağırır ve işlem tamamlanana kadar ürünü bir istasyondan diğerine geçirir.

## <a name="gateway-opc-publisher-module"></a>Ağ geçidi OPC yayımcı modülü

OPC Yayımcı Modülü, istasyonun OPC UA sunucularına bağlanır ve yayımlanacak OPC düğümlerine abone olur. Modül, düğüm verilerini JSON biçimine dönüştürür, şifreler ve OPC UA Pub/Sub iletileri olarak IoT Hub’a gönderir.

OPC Yayımcı modülü, yalnızca bir giden https bağlantı noktası (443) gerektirir ve mevcut kuruluş altyapısı ile birlikte çalışabilir.

## <a name="gateway-opc-proxy-module"></a>Ağ geçidi OPC proxy modülü

Ağ Geçidi OPC UA Proxy Modülü, ikili OPC UA komutu ile denetim iletileri arasında tünel oluşturur ve yalnızca bir giden https bağlantı noktası (443) gerektirir. Web Proxy’leri dahil olmak üzere, mevcut kuruluş altyapısı ile birlikte çalıştırabilir.

Paketlenmiş TCP/IP verilerini uygulama katmanında aktarmak üzere IoT Hub Cihaz yöntemlerini kullanır ve böylece SSL/TLS kullanarak uç nokta güveni, veri şifreleme ve bütünlüğü sağlar.

Proxy üzerinden geçirilen OPC UA ikili protokolü, UA kimlik doğrulaması ve şifrelemesi kullanır.

## <a name="azure-time-series-insights"></a>Azure Zaman Serisi Görüşleri

Ağ Geçidi OPC Yayımcı Modülü, veri değerlerindeki değişikliği algılamak üzere OPC UA sunucu düğümlerine abone olur. Düğümlerden birinde veri değişikliği algılanırsa, bu modül Azure IoT Hub’a iletiler gönderir.

IoT Hub, Azure TSI’ye bir olay kaynağı gönderir. TSI, iletilere eklenen zaman damgalarına bağlı olarak verileri 30 gün boyunca saklar. Bu veriler şunlardır:

* OPC UA ApplicationUri
* OPC UA NodeId
* Düğümün değeri
* Kaynak zaman damgası
* OPC UA DisplayName

Şu anda TSI, müşterilerin verileri saklama süresini özelleştirmesine izin vermemektedir.

TSI bir **SearchSpan** (**Time.From**, **Time.To**) kullanarak düğüm verilerinde sorgu çalıştırır ve **OPC UA ApplicationUri** veya **OPC UA NodeId** veya **OPC UA DisplayName**’e göre toplar.

OEE ve KPI ölçeklerine ait verileri ve zaman serisi grafiklerini almak için, veriler olay sayısı, Toplam, Ortalama, En Az ve En Fazla değerlerine göre toplanır.

Zaman serisi, farklı bir işlem kullanılarak oluşturulur. OEE ve KPI’lar, istasyona dayalı verilerden hesaplanır ve uygulamadaki topoloji (üretim hatları, fabrikalar, kuruluş) için oluşturulur.

Buna ek olarak, OEE ve KPI topolojisi için zaman serisi, görüntülenen bir zaman aralığı hazır olduğunda uygulamada hesaplanır. Örneğin, gün görünümü saatte bir kez güncelleştirilir.

Düğüm verilerinin zaman serisi görünümü, zaman aralığı toplaması kullanılarak doğrudan TSI’den gelir.

## <a name="iot-hub"></a>IoT Hub’ı
[IoT hub’ı][lnk-IoT Hub], OPC Yayımcı Modülünden buluta gönderilen verileri alır ve Azure TSI hizmetinde kullanılabilir hale getirir. 

IoT Hub çözümde aynı zamanda şunları yapar:
- Tüm OPC Yayımcı Modülleri ve tüm OPC Proxy Modülleri için kimlikleri depolayan bir kimlik kayıt defteri tutar.
- OPC Proxy Modülünün iki yönlü iletişimi için taşıma kanalı olarak kullanılır.

## <a name="azure-storage"></a>Azure Storage
Çözüm, VM’nin disk deposu ve dağıtım verilerinin depolanması için Azure blob depolama kullanır.

## <a name="web-app"></a>Web uygulaması
Önceden yapılandırılmış çözümün bir parçası olarak dağıtılan web uygulaması; tümleşik OPC UA istemcisi, uyarı işleme ve telemetri görselleştirmesinden oluşur.

## <a name="telemetry-data-flow"></a>Telemetri veri akışı

![Telemetri veri akışı](media/iot-suite-connected-factory-walkthrough/telemetry_dataflow.png)

### <a name="flow-steps"></a>Akış adımları

1. OPC Publisher, yerel sertifika depolama alanından gerekli OPC UA X509 sertifikalarını ve IoT Hub güvenlik kimlik bilgilerini okur.
    - OPC Publisher gerekirse sertifika depolama alanında eksik olan sertifikaları veya kimlik bilgilerini oluşturur ve depolar.

2. OPC Publisher kendini IoT Hub'a kaydeder.
    - Yapılandırılmış protokolü kullanır. IoT Hub istemci SDK'sı destekli tüm protokolleri kullanabilir. Varsayılan MQTT olarak belirlenmiştir.
    - Protokol iletişiminin güvenliği TLS tarafından sağlanır.

3. OPC Publisher yapılandırma dosyasını okur.

4. OPC Publisher, yapılandırılmış olan her bir OPC UA Server için bir OPC Session oluşturur.
    - TCP bağlantısını kullanır.
    - OPC Publisher ve OPC UA Server, X509 sertifikalarını kullanarak birbirlerinin kimliğini doğrular.
    - Sonraki tüm OPC UA trafiği, yapılandırılmış olan OPC UA şifreleme mekanizması tarafından şifrelenir.
    - OPC Publisher, yapılandırılmış olan her yayımlama aralığı için OPC Session içinde bir OPC Subscription oluşturur.
    - OPC Subscription içinde yayımlamak üzere OPC Nodes için OPC Monitored öğeleri oluşturur.

5. İzlenen bir OPC Node değeri değişirse OPC UA Server güncelleştirmeleri OPC Publisher'a gönderir.

6. OPC Publisher yeni değeri dönüştürür.
    - Toplu işleme etkinse birden fazla değişikliği toplu olarak işler.
    - Bir IoT Hub iletisi oluşturur.

7. OPC Publisher, IoT Hub'a bir ileti gönderir.
    - Yapılandırılmış protokolü kullanır.
    - İletişim güvenliği TLS tarafından sağlanır.

8. Zaman Serisi Öngörüleri (TSI), IoT Hub iletilerini okur.
    - TCP/TLS üzerinden AMQP kullanır.
    - Bu adım veri merkezi içinde gerçekleştirilir.

9. TSI içindeki bekleyen veriler.

10. Azure AppService içindeki bağlı fabrika WebApp, gerekli verileri TSI kaynağından sorgular.
    - TCP/TLS güvenli iletişimini kullanır.
    - Bu adım veri merkezi içinde gerçekleştirilir.

11. Web tarayıcısı Bağlı fabrika WebApp öğesine bağlanır.
    - Bağlı fabrika panosunu oluşturur.
    - HTTPS üzerinden bağlanır.
    - Bağlı fabrika uygulaması erişimi için kullanıcının Azure Active Directory kimlik doğrulamasından geçmesi gerekir.
    - Bağlı fabrika uygulamasına giden WebApi çağrılarının güvenliği, Sahtekarlığı Önleme Belirteçleri ile sağlanır.

12. Veri güncelleştirmelerinde bağlı fabrika WebApp girişi güncel verileri web tarayıcısına gönderir.
    - SignalR protokolünü kullanır.
    - Güvenliği TCP/TLS ile sağlanır.

## <a name="browsing-data-flow"></a>Göz atma veri akışı

![Göz atma veri akışı](media/iot-suite-connected-factory-walkthrough/browsing_dataflow.png)

### <a name="flow-steps"></a>Akış adımları

1. OPC Proxy (sunucu bileşeni) başlatılır.
    - Paylaşılan erişim anahtarlarını yerel depolama alanından okur.
    - Gerekirse depolama alanındaki eksik erişim anahtarlarını depolar.

2. OPC Proxy (sunucu bileşeni) kendisini IoT Hub'a kaydeder.
    - Bilinen cihazların tümünü IoT Hub'dan okur.
    - Socket veya Websocket üzerinden TLS üzerinden MQTT kullanır.

3. Web tarayıcısı Bağlı fabrika WebApp öğesine bağlanır ve Bağlı fabrika panosunu oluşturur.
    - HTTPS kullanır.
    - Kullanıcı bağlanmak istediği OPC UA sunucusunu seçer.

4. Bağlı fabrika WebApp öğesi, seçilen OPC UA sunucusu ile bir OPC UA Session oluşturur.
    - OPC UA yığınını kullanır.

5. OPC Proxy taşıma işlemi, OPC UA yığınından bir istek alarak OPC UA sunucusuyla bir TCP yuva bağlantısı kurar.
    - Yalnızca TCP yükünü alır ve değiştirmeden kullanır.
    - Bu adım Bağlı fabrika WebApp öğesi içinde gerçekleştirilir.

6. OPC Proxy (istemci bileşeni), IoT Hub cihaz kaydında OPC Proxy (sunucu bileşeni) girişini arar. Ardından IoT Hub içinde OPC Proxy (sunucu bileşeni) cihazının bir cihaz yöntemini çağırır.
    - OPC Proxy araması için TCP/TLS üzerinden HTTPS kullanır.
    - OPC UA sunucusuyla TCP yuvası bağlantısı için TCP/TLS üzerinden HTTPS kullanır.
    - Bu adım veri merkezi içinde gerçekleştirilir.

7. IoT Hub, OPC Proxy (sunucu bileşeni) cihazında bir cihaz yöntemi çağırır.
    - OPC UA sunucusuyla TCP yuvası bağlantısı kurmak için Socket veya Secure Websocket bağlantısı üzerinden TLS üzerinden MQTT kullanır.

8. OPC Proxy (sunucu bileşeni), TCP yükünü atölye ağına gönderir.

9. OPC UA sunucusu yükü işler ve yanıtı geri gönderir.

10. Yanıt OPC Proxy (sunucu bileşeni) yuvası tarafından alınır.
    - OPC Proxy verileri cihaz yönteminin dönüş değeri olarak IoT Hub ve OPC Proxy (istemci bileşeni) öğelerine gönderir.
    - Bu veriler Bağlı fabrika uygulamasındaki OPC UA yığınına gönderilir.

11. Bağlı fabrika WebApp, OPC Browser UX değerini OPC UA sunucusundan aldığı özgün OPC UA verileriyle zenginleştirmiş bir şekilde oluşturulmak üzere Web Tarayıcısına döndürür.
    - OPC Browser IX istemci tarafı OPC adres alanına göz atarken ve OPC adres alanındaki düğümlere işlevleri uygularken verileri bağlı fabrika WebApp kaynağından almak için güvenliği Sahtekarlığı Önleme Belirteçleriyle sağlanan HTTPS üzerinden AJAX çağrıları kullanır.
    - İstemci gerekirse OPC UA sunucusuyla bilgi alışverişi yapmak için 4-10 arasındaki iletişim adımlarını kullanır.

> [!NOTE]
> OPC Proxy (sunucu bileşeni) ve OPC Proxy (istemci) bileşeni OPC UA iletişimiyle ilgili tüm TCP trafiği için 4-10 arası adımları gerçekleştirir.

> [!NOTE]
> Bağlı fabrika WebApp öğesi içindeki OPC UA sunucusu ve OPC UA yığını için OPC Proxy iletişimi şeffaftır ve tüm OPC UA kimlik doğrulama ve şifreleme güvenlik özellikleri geçerlidir.

## <a name="next-steps"></a>Sonraki adımlar

Aşağıdaki makaleleri okuyarak IoT Paketi ile çalışmaya başlayabilirsiniz:

* [azureiotsuite.com sitesindeki izinler][lnk-permissions]
* [Bağlı fabrika önceden yapılandırılmış çözümü için Windows veya Linux’ta ağ geçidi dağıtma](iot-suite-connected-factory-gateway-deployment.md)
* [OPC Publisher başvuru uygulaması](iot-suite-connected-factory-publisher.md).

[connected-factory-logical]:media/iot-suite-connected-factory-walkthrough/cf-logical-architecture.png

[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-customize]: iot-suite-v1-guidance-on-customizing-preconfigured-solutions.md
[lnk-IoT Hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-OPC-UA-NET-Standard]:https://github.com/OPCFoundation/UA-.NETStandardLibrary
[lnk-Azure-IoT-Gateway]: https://github.com/azure/iot-edge
[lnk-permissions]: iot-suite-v1-permissions.md
