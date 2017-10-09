---
title: "aaaConnected Fabrika Azure IOT paketi çözümünde gezinme | Microsoft Docs"
description: "Hello Azure IOT önceden yapılandırılmış çözüm açıklaması Fabrika ve mimarisinin bağlı."
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
ms.date: 07/27/2017
ms.author: dobett
ms.openlocfilehash: 7fd55c51351659401349cfde91a20fce1045b4f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connected-factory-preconfigured-solution-walkthrough"></a>Önceden yapılandırılmış bağlı fabrika çözüm kılavuzu

Merhaba IOT paketi bağlı Fabrika [önceden yapılandırılmış çözüm] [ lnk-preconfigured-solutions] uçtan uca endüstriyel çözümünü uygulamasıdır:

* OPC UA sunucuları benzetimli Fabrika Üretim satırları ve gerçek OPC UA sunucu cihazlarda çalışan benzetimli tooboth endüstriyel aygıtlarını bağlar. Merhaba OPC UA hakkında daha fazla bilgi için bkz: [bağlı Fabrika SSS](iot-suite-faq-cf.md).
* Bu cihazların ve üretim hatlarının işlem KPI ve OEE değerlerini gösterir.
* Bulut tabanlı bir uygulama OPC UA sunucu sistemleri ile kullanılan toointeract nasıl olabilir gösterir.
* Tooconnect kendi OPC UA sunucusu aygıtları sağlar.
* Toobrowse sağlar ve hello OPC UA sunucu verilerini değiştirme.
* OPC UA sunucularınızdan hello veri özelleştirilmiş görünümleri Hello Azure zaman serisi Öngörüler (TSI) hizmeti tooprovide ile tümleşir.

Merhaba çözüm kendi uygulamanız için bir başlangıç noktası olarak kullanabilirsiniz ve [özelleştirme] [ lnk-customize] , toomeet kendi belirli iş gereksinimlerinizi.

Bu makalede bazı temel öğeleri bağlı hello Fabrika çözüm tooenable hello anlatılmaktadır nasıl çalıştığını toounderstand. Bu bilgiler şunları yapmanıza yardımcı olur:

* Merhaba çözümde sorunları giderin.
* Plan nasıl toocustomize toohello çözüm toomeet belirli gereksinimlerinizi.
* Azure hizmetlerini kullanan kendi IoT çözümünüzü tasarlama.

Daha fazla bilgi için bkz: Merhaba [bağlı Fabrika SSS](iot-suite-faq-cf.md).

## <a name="logical-architecture"></a>Mantıksal mimari

Diyagram aşağıdaki hello hello hello önceden yapılandırılmış çözümün mantıksal bileşenlerinin ana hatların vermektedir:

![Bağlı fabrika mantıksal mimarisi][connected-factory-logical]

## <a name="communication-patterns"></a>Kimlik doğrulaması desenleri

Merhaba çözüm kullanır hello [OPC UA Pub/alt belirtimi](https://opcfoundation.org/news/opc-foundation-news/opc-foundation-announces-support-of-publish-subscribe-for-opc-ua/) toosend JSON biçiminde OPC UA telemetri verileri tooIoT Hub. Merhaba çözüm kullanır hello [OPC yayımcı](https://github.com/Azure/iot-edge-opc-publisher) bu amaç için IOT kenar modülü.

Merhaba çözümü, ayrıca şirket içi OPC UA sunucuları ile bağlantı kurabilir bir web uygulaması tümleşik bir OPC UA istemcisi vardır. Merhaba istemcinin kullandığı bir [ters proxy](https://wikipedia.org/wiki/Reverse_proxy) ve açık bağlantı noktalarını hello şirket içi Güvenlik Duvarı'nda gerek kalmadan IOT hub'ı toomake hello bağlantısından Yardım alır. Bu iletişim deseni [hizmet destekli iletişim](https://blogs.msdn.microsoft.com/clemensv/2014/02/09/service-assisted-communication-for-connected-devices/) olarak adlandırılır. Merhaba çözüm kullanır hello [OPC Proxy](https://github.com/Azure/iot-edge-opc-proxy/) bu amaç için IOT kenar modülü.


## <a name="simulation"></a>Benzetim

Sanal istasyonlar ve benzetimli hello üretim yürütme sistemleri (MES) bir Fabrika üretim hizalamak olun hello. Merhaba sanal cihazlar ve hello OPC yayımcı modülü üzerinde hello dayalı [OPC UA .NET standart] [ lnk-OPC-UA-NET-Standard] hello OPC Foundation tarafından yayımlanan.

Merhaba OPC Proxy ve OPC yayımcı modülleri dayalı olarak uygulanan [Azure IOT kenar][lnk-Azure-IoT-Gateway]. Her sanal üretim hattına bağlı, atanmış bir ağ geçidi bulunur.

Tüm benzetim bileşenleri bir Azure Linux VM’sinde barındırılan Docker kapsayıcıları içinde çalışır. Merhaba benzetimi yapılandırılmış toorun sekiz sanal üretim varsayılan satırdır.

## <a name="simulated-production-line"></a>Sanal üretim hattı

Üretim hattı, parça üretir. Farklı istasyonlardan oluşur: derleme istasyonu, test istasyonu ve paketleme istasyonu.

Merhaba benzetimi çalışır ve hello OPC UA düğümleri kullanıma sunulan hello verileri güncelleştirir. Tüm sanal üretim hattı istasyonları, hello OPC UA aracılığıyla MES tarafından düzenlenir.

## <a name="simulated-manufacturing-execution-system"></a>Sanal üretim yürütme sistemi

Merhaba MES hello üretim satırı OPC UA toodetect istasyon durumu değiştiğinde aracılığıyla her istasyon izler. OPC UA yöntemleri toocontrol hello istasyonları çağırır ve tamamlanıncaya kadar bir ürün bir istasyon toohello sonraki geçirir.

## <a name="gateway-opc-publisher-module"></a>Ağ geçidi OPC yayımcı modülü

OPC yayımcı modülü toohello istasyon OPC UA sunucularını bağlar ve yayımlanan toohello OPC düğümleri toobe abone olur. Merhaba modülü hello düğümü verileri JSON biçimine dönüştürür, onu şifreler ve tooIoT Hub OPC UA Pub/alt iletileri olarak gönderir.

Hello OPC yayımcı modülü yalnızca bir giden https bağlantı noktası (443) gerektirir ve var olan kuruluş altyapısı ile çalışabilirsiniz.

## <a name="gateway-opc-proxy-module"></a>Ağ geçidi OPC proxy modülü

ağ geçidi OPC UA Proxy modülü Hello ikili OPC UA komut ve Denetim iletileri tünelleri ve yalnızca giden https bağlantı noktası (443) gerektirir. Web Proxy’leri dahil olmak üzere, mevcut kuruluş altyapısı ile birlikte çalıştırabilir.

IOT Hub cihaz yöntemleri packetized tootransfer TCP/IP'yi veri hello uygulama katmanında kullanır ve böylece uç nokta güven, veri şifreleme ve SSL/TLS kullanarak bütünlüğü sağlar.

Merhaba OPC UA ikili Protokolü hello proxy üzerinden kendisini geçişli UA kimlik doğrulama ve şifreleme kullanır.

## <a name="azure-time-series-insights"></a>Azure Zaman Serisi Görüşleri

ağ geçidi OPC yayımcı modülü Hello tooOPC UA server düğümleri toodetect değişiklik hello veri değerleri abone olur. Bir veri değişikliği hello düğümlerinden biri algılanırsa, bu modül iletileri tooAzure IOT hub'ı sonra gönderir.

IOT hub'ı bir olay kaynağı tooAzure TSI sağlar. TSI depoları veri damgalarının bağlı olarak 30 gün için toohello iletileri bağlı. Bu veriler şunlardır:

* OPC UA ApplicationUri
* OPC UA NodeId
* Merhaba düğümünün değeri
* Kaynak zaman damgası
* OPC UA DisplayName

Şu anda TSI müşteriler izin vermiyor toocustomize ne kadar süreyle tookeep hello verilerini istedikleri.

TSI bir SearchSpan (Time.From, Time.To) kullanarak düğüme karşı sorgulama yapar ve OPC UA ApplicationUri ya da OPC UA NodeId veya OPC UA DisplayName’e göre toplar.

tooretrieve hello veri hello OEE ve KPI ölçerler ve hello zaman serisi grafikler, veriler için olayları, Sum, Avg, Min ve Max sayısına göre toplanır.

Merhaba zaman serisi, farklı bir işlem kullanılarak oluşturulur. OEE ve KPI'leri istasyon temel verilerinden hesaplanır ve hello topolojisi (Üretim satırları, oluşturucuları, Kurumsal) için hello uygulamada kabarcıklanma.

Buna ek olarak, görüntülenen bir timespan hazır olduğunda OEE ve KPI topolojisi için zaman serisi hello uygulamada hesaplanır. Örneğin, hello gün görünümü tam saatte bir güncelleştirilir.

Merhaba zaman serisi düğümü verilerin görünümünü doğrudan bir toplama için timespan kullanarak TSI gelir.

## <a name="iot-hub"></a>IoT Hub’ı
Merhaba [IOT hub'ı] [ lnk-IoT Hub] hello OPC yayımcı modülü hello buluta gönderilen verileri alır ve kullanılabilir toohello Azure TSI hizmeti sağlar. 

Merhaba IOT hub'ı hello çözümde de:
- Tüm OPC yayımcı modülü ve tüm OPC Proxy modülleri için hello kimliklerini depolar kimlik kayıt defteri tutar.
- Taşıma kanalını hello OPC Proxy modülü çift yönlü iletişimi için kullanılır.

## <a name="azure-storage"></a>Azure Storage
Merhaba çözüm hello VM ve toostore veri dağıtımı için disk depolama alanı olarak Azure blob depolama kullanır.

## <a name="web-app"></a>Web uygulaması
bir tümleşik OPC UA istemci, işleme uyarıları ve telemetri görselleştirme oluşur hello önceden yapılandırılmış çözümün bir parçası olarak dağıtılan hello web uygulaması.

## <a name="next-steps"></a>Sonraki adımlar

Makaleler hello okuyarak IOT paketi ile çalışmaya başlayabilirsiniz:

* [Merhaba azureiotsuite.com sitesindeki izinler][lnk-permissions]
* [Windows veya Linux üzerinde bir ağ geçidi bağlı hello Fabrika önceden yapılandırılmış çözümü dağıtma](iot-suite-connected-factory-gateway-deployment.md)

[connected-factory-logical]:media/iot-suite-connected-factory-walkthrough/cf-logical-architecture.png

[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-IoT Hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-OPC-UA-NET-Standard]:https://github.com/OPCFoundation/UA-.NETStandardLibrary
[lnk-Azure-IoT-Gateway]: https://github.com/azure/iot-edge
[lnk-permissions]: iot-suite-permissions.md
