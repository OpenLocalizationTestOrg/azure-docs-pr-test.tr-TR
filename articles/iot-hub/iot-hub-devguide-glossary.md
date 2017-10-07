---
title: "aaaAzure IOT hub'ı terimler sözlüğü | Microsoft Docs"
description: "Geliştirici Kılavuzu - tooAzure IOT Hub ile ilgili sık kullanılan terimleri içeren sözlük."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 16ef29ea-a185-48c3-ba13-329325dc6716
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 217eb082c13e06df5c07543c65d498ad3e395939
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="glossary-of-iot-hub-terms"></a>IOT hub'ı terimler sözlüğü
Bu makalede bazı hello Ortak terimleri hello kullanılan IOT hub'ı makaleleri listeler.

## <a name="advanced-message-queueing-protocol"></a>Gelişmiş Message Queuing protokolü
[Message Queuing Protokolü (AMQP) Gelişmiş](https://www.amqp.org/) olan bir hello Mesajlaşma protokolleri [IOT hub'ı](#iot-hub) aygıtlarıyla iletişim kurmak için destekler. Hello Mesajlaşma IOT hub'ı destekleyen protokolleri hakkında daha fazla bilgi için bkz: [IOT Hub ile iletileri almasına ve göndermesine](iot-hub-devguide-messaging.md).

## <a name="azure-cli"></a>Azure CLI
Merhaba [Azure CLI](../cli-install-nodejs.md) oluşturmak ve Microsoft Azure kaynakları yönetmek için bir platformlar arası, açık kaynaklı, kabuk tabanlı komut bir araçtır. Bu sürümü hello CLI, Node.js kullanarak uygulanır.

## <a name="azure-cli-20"></a>Azure CLI 2.0
Merhaba [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) oluşturmak ve Microsoft Azure kaynakları yönetmek için bir platformlar arası, açık kaynaklı, kabuk tabanlı komut bir araçtır. Bu önizleme sürümü hello CLI, Python kullanılarak uygulanır.


## <a name="azure-iot-device-sdks"></a>Azure IOT cihaz SDK'ları
Vardır _cihaz SDK'ları_ toocreate etkinleştirmek birden çok dil için kullanılabilir [cihaz uygulamaları](#device-app) bir IOT hub ile etkileşim. Merhaba IOT hub'ı öğreticiler size yol gösterecektir toouse bu cihaz SDK'ları. Bu Github'da hello kaynak kodu ve hello cihaz SDK'ları hakkında daha fazla bilgi bulabilirsiniz [depo](https://github.com/Azure/azure-iot-sdks).

## <a name="azure-iot-edge"></a>Azure IoT Edge
IOT sınır ağ geçidi ile bağlı cihazlar toocommunicate ile etkinleştirmek toowrite uygulamaları etkinleştirir [IOT hub'ı](#iot-hub). Merhaba IOT kenar öğreticiler size yol gösterecektir toouse bu hizmet. Bu Github'da hello kaynak kodu ve Azure IOT kenar hakkında daha fazla bilgi bulabilirsiniz [depo](https://github.com/Azure/iot-edge).

## <a name="azure-iot-service-sdks"></a>Azure IOT hizmeti SDK'ları
Vardır _SDK hizmeti_ toocreate etkinleştirmek birden çok dil için kullanılabilir [arka uç uygulamaları](#back-end-app) bir IOT hub ile etkileşim. Merhaba IOT hub'ı öğreticiler size nasıl toouse bu hizmet Göster SDK'ları. Bu Github'da hello kaynak kodu ve hello hizmet SDK'ları hakkında daha fazla bilgi bulabilirsiniz [depo](https://github.com/Azure/azure-iot-sdks).

## <a name="azure-portal"></a>Azure portalına
Merhaba [Microsoft Azure portal](https://portal.azure.com) burada sağlamak ve Azure kaynaklarınızı yönetmek merkezi bir yerdir. İçerik kullanarak düzenler _dikey_. Toouse hello bazı hello IOT hub'ı öğreticileri istenebilir [Klasik Azure portalı](https://manage.windowsazure.com).

## <a name="azure-powershell"></a>Azure PowerShell
[Azure PowerShell](/powershell/azure/overview) koleksiyonudur cmdlet'lerini Windows PowerShell ile Azure toomanage kullanabilirsiniz. Merhaba cmdlet'leri toocreate kullanmak, test, dağıtmak ve çözümleri yönetmek ve Hizmetleri Azure platformu hello teslim.

## <a name="azure-resource-manager"></a>Azure Resource Manager
[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) hello kaynaklarla bir grup olarak çözümünüzdeki toowork sağlar. Dağıtma, güncelleştirme veya tek ve eşgüdümlü bir işlemle çözümünüzdeki hello kaynakları silin.

## <a name="azure-service-bus"></a>Azure Service Bus
[Hizmet veri yolu](../service-bus/index.md) Kurumsal Mesajlaşma ile iletişimi bulut etkin ve yardımcı olan geçirilen iletişimi hello bulut ile şirket içi çözümler bağlanmak sağlar. Service Bus hizmetini kullanmak bazı IOT hub'ı öğreticileri olun [sıraları](../service-bus-messaging/service-bus-messaging-overview.md).

## <a name="azure-storage"></a>Azure Storage
[Azure depolama](../storage/common/storage-introduction.md) bulut depolama çözümüdür. Toostore yapılandırılmamış kullanabileceğiniz hello Blob Depolama Birimi hizmeti içeren veri nesnesi. Bazı IOT hub'ı öğreticileri blob storage'ı kullanın.

## <a name="back-end-app"></a>Arka uç uygulama
Merhaba bağlamındaki [IOT hub'ı](#iot-hub), arka uç uygulama tooone hello service'e yönelik uç noktalar için bir IOT hub'ındaki bağlanan bir uygulamadır. Örneğin, bir arka uç uygulaması alacağı [cihaz bulut](#device-to-cloud)hello yönetmek veya iletileri [kimlik kayıt defteri](#identity-registry). Genellikle, bir arka uç uygulaması hello bulutta çalışır, ancak çoğu hello öğreticileri hello arka uç uygulamalar, yerel geliştirme makinenizde çalışan konsol uygulamalardır.

## <a name="built-in-endpoints"></a>Yerleşik uç noktaları
Her IOT hub'ı içeren yerleşik bir [endpoint](iot-hub-devguide-endpoints.md) Event Hub ile uyumlu olan. Olay hub'ları tooread cihaz bulut iletilerini Bu uç noktasından çalışan herhangi bir mekanizma kullanabilirsiniz.

## <a name="cloud-gateway"></a>Bulut ağ geçidi
Bağlantıyı doğrudan çok bağlanamıyor cihazlar için bir bulut ağ geçidi etkinleştirir[IOT hub'ı](#iot-hub). Bulut ağ geçidi Karşıtlık tooa hello bulutta barındırılan [alan ağ geçidi](#field-gateway) yerel tooyour aygıtları çalıştırır. Tooimplement protokol çevirisi, cihazlarınız için bir bulut ağ geçidi için tipik kullanım durumdur.

## <a name="cloud-to-device"></a>Bulut cihaz
Bir IOT hub tooa bağlı aygıtından gönderilen toomessages başvuruyor. Genellikle, bu iletiler, hello aygıt tootake bir eylem yönlendiren komutlardır. Daha fazla bilgi için bkz: [IOT Hub ile iletileri almasına ve göndermesine](iot-hub-devguide-messaging.md).

## <a name="connection-string"></a>Bağlantı dizesi
Uygulama kodu tooencapsulate hello gerekli bilgileri tooconnect tooan uç noktanızı içinde bağlantı dizelerini kullanın. Bir bağlantı dizesi genellikle hello endpoint ve güvenlik bilgileri, ancak bağlantı dizesi biçimleri hizmetleri arasında farklılık hello adresini içerir. Merhaba IOT Hub hizmeti ile ilişkili bağlantı dizesi iki tür vardır:
- *Cihaz bağlantı dizelerini* bir IOT hub üzerindeki aygıtları tooconnect toohello aygıt dönük uç noktaları etkinleştirin.
- *IOT Hub bağlantı dizelerini* bir IOT hub üzerindeki arka uç uygulamaları tooconnect toohello hizmet dönük uç noktaları etkinleştirin.

## <a name="custom-endpoints"></a>Özel uç noktaları
Oluşturabileceğiniz özel [uç noktaları](iot-hub-devguide-endpoints.md) bir IOT hub toodeliver üzerinde iletileri gönderilen tarafından bir [yönlendirme kuralı](#routing-rules). Özel uç noktaları tooan olay hub'ı, bir hizmet veri yolu kuyruğu ya da bir Service Bus konu doğrudan bağlanın.

## <a name="custom-gateway"></a>Özel ağ geçidi
Bağlantıyı doğrudan çok bağlanamıyor cihazlar için bir ağ geçidi etkinleştirir[IOT hub'ı](#iot-hub). Kullanabileceğiniz [Azure IOT kenar](#azure-iot-edge) üzerinde özel mantık toohandle iletileri, özel protokol dönüşümler ve başka bir işlem uygulayan toobuild özel ağ geçitleri hello sınır.

## <a name="data-point-message"></a>Veri noktası iletisi
Veri noktası iletisi bir [cihaz bulut](#device-to-cloud) içeren ileti [telemetri](#telemetry) Rüzgar hızı veya sıcaklık gibi verileri.

## <a name="desired-configuration"></a>İstenen yapılandırma
Merhaba bağlamındaki bir [cihaz çifti](iot-hub-devguide-device-twins.md), istenen yapılandırma toohello eksiksiz özelliklerinin ve meta veri hello cihazla eşitlenmesi gerektiği hello cihaz çiftine başvuruyor.

## <a name="desired-properties"></a>İstenen özellikleri
Merhaba bağlamındaki bir [cihaz çifti](iot-hub-devguide-device-twins.md), istenen özellikleri ile birlikte kullanılan hello cihaz çifti alt [özellikleri bildirilen](#reported-properties) toosynchronize aygıt yapılandırması veya koşul. İstenen özellikleri yalnızca ayarlanabilir bir [arka uç uygulama](#back-end-app) ve hello tarafından uyulması gereken [cihaz uygulaması](#device-app).

## <a name="device-to-cloud"></a>Cihaz bulut
Bağlı bir aygıttan çok gönderilen toomessages başvuruyor[IOT hub'ı](#iot-hub). Bu iletiler olabilir [veri noktası](#data-point-message) veya [etkileşimli](#interactive-message) iletileri. Daha fazla bilgi için bkz: [IOT Hub ile iletileri almasına ve göndermesine](iot-hub-devguide-messaging.md).

## <a name="device"></a>Cihaz
IOT Hello bağlamında, bir aygıt genellikle, veri toplayabilir veya diğer cihazları denetlemek bir küçük ölçekli, tek başına işlem cihazıdır. Örneğin, bir aygıt bir ortam izleme cihaz ya da bir greenhouse hello su kaynağı ve havalandırma sistemleri için bir denetleyici olabilir. Merhaba [aygıt katalog](https://catalog.azureiotsuite.com/) donanım aygıtları sertifikalı toowork ile bir listesini sağlar [IOT hub'ı](#iot-hub).

## <a name="device-app"></a>Cihaz uygulaması
Bir cihaz uygulamasının çalışır, [aygıt](#device) ve tanıtıcıları ile iletişim Merhaba, [IOT hub'ı](#iot-hub). Genellikle, hello birini kullanmanız [Azure IOT cihaz SDK'ları](#azure-iot-device-sdks) uygulamak zaman cihaz uygulaması. Birçok hello IOT öğreticileri kullandığınız bir [sanal cihaz](#simulated-device) kolaylık sağlamak için.

## <a name="device-condition"></a>Cihaz durumu
Şu anda kullanımda hello bağlantı yöntemi gibi toodevice durumu bilgileri tarafından bildirilen başvuruyor bir [cihaz uygulaması](#device-app). [Cihaz uygulamaları](#device-app) yeteneklerini de bildirebilirsiniz. Cihaz çiftlerini kullanarak koşul ve yetenek bilgi sorgulayabilirsiniz.

## <a name="device-data"></a>Cihaz verileri
Cihaz verileri başvuruyor hello IOT hub'ı depolanan toohello aygıt başına verileri [kimlik kayıt defteri](#identity-registry). Bu olası tooimport ve bu verileri dışarı aktarma.

## <a name="device-explorer"></a>Cihaz Gezgini
Merhaba [aygıt explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) Windows üzerinde çalışır ve, toomanage sağlayan bir araçtır aygıtlarınızı hello [kimlik kayıt defteri](#identity-registry).hello aracı da gönderebilir ve iletileri tooyour cihazlar alır.

## <a name="device-identities-rest-api"></a>Cihaz Kimlikleri REST API’si
Merhaba [aygıt kimlikleri REST API](https://docs.microsoft.com/rest/api/iothub/iothubresource) aygıtlarınızı kayıtlı hello toomanage etkinleştirir [kimlik kayıt defteri](#identity-registry) bir REST API kullanarak. Genellikle, üst düzey hello birini kullanmalıdır [SDK hizmeti](#azure-iot-service-sdks) IOT hub'ı öğreticileri hello gösterildiği gibi.

## <a name="device-identity"></a>Cihaz kimliği
Merhaba cihaz kimliği hello kayıtlı hello atanan benzersiz tanımlayıcı tooevery aygıttır [kimlik kayıt defteri](#identity-registry).

## <a name="device-management"></a>Cihaz yönetimi
Aygıt Yönetimi planlama, sağlama, yapılandırma, izleme ve devre dışı dahil olmak üzere, IOT çözümünüzün hello cihazları yönetmeyle ilgili hello tam yaşam döngüsü kapsar.

## <a name="device-management-patterns"></a>Cihaz yönetimi modelleri
[IOT hub'ı](#iot-hub) yeniden başlatma, fabrika ayarlarına sıfırlama gerçekleştirme ve bellenim güncelleştirmeleri aygıtlarınızda gerçekleştirme gibi sık kullanılan aygıt yönetimi desenlerini sağlar.

## <a name="device-messaging-rest-api"></a>Cihaz Mesajlaşma REST API’si
Merhaba kullanabilirsiniz [cihaz Mesajlaşma REST API](https://docs.microsoft.com/rest/api/iothub/httpruntime) aygıttan toosend cihaz-bulut iletileri tooan IOT hub'ı ve alma [bulut cihaz](#cloud-to-device) IOT hub'ı gelen iletileri. Genellikle, üst düzey hello birini kullanmalıdır [cihaz SDK'ları](#azure-iot-device-sdks) IOT hub'ı öğreticileri hello gösterildiği gibi.

## <a name="device-provisioning"></a>Cihaz sağlama
Cihaz sağlama olduğu hello ilk ekleme işleminin hello [aygıt verilerini](#device-data) toohello çözümünüz içinde depolar. Yeni bir cihaz tooconnect tooyour hub tooenable, bir cihaz kimliği ve anahtarları toohello IOT hub'ı eklemelisiniz [kimlik kayıt defteri](#identity-registry). Sağlama işlemi hello bir parçası olarak, diğer çözüm depolarında tooinitialize aygıta özgü veriler gerekebilir.

## <a name="device-twin"></a>Cihaz çifti
A [cihaz çifti](iot-hub-devguide-device-twins.md) meta verileri, yapılandırmaları ve koşulları gibi cihaz durumu bilgilerini depolar JSON belgesi. [IOT hub'ı](#iot-hub) IOT hub'ınıza sağlamak her cihaz için cihaz çifti devam ettirir. Cihaz çiftlerini etkinleştirmek, toosynchronize [aygıt koşullar](#device-condition) hello aygıt hello çözüm arasında yapılandırmaları arka uç ve. Cihaz çiftlerini toolocate belirli cihazlar ve sorgu hello uzun süre çalışan işlemleri durumunu sorgulayabilirsiniz.

## <a name="device-twin-queries"></a>Cihaz çifti sorguları
[Cihaz çifti sorguları](iot-hub-devguide-query-language.md) cihaz çiftlerini hello SQL benzeri IOT hub'ı sorgu dili tooretrieve bilgileri kullanın. Aynı IOT hub'ı sorgu dil tooretrieve bilgileri hakkında hello kullanabilirsiniz [işleri](#job) IOT hub'ınıza çalışıyor.

## <a name="device-twin-rest-api"></a>Cihaz çifti REST API'si
Merhaba kullanabilirsiniz [cihaz çifti REST API](https://docs.microsoft.com/rest/api/iothub/devicetwinapi) hello çözümden arka uç toomanage cihaz çiftlerini. Merhaba API sağlar tooretrieve ve güncelleştirme [cihaz çifti](#device-twin) özellikleri ve çağırma [doğrudan yöntemleri](#direct-method). Genellikle, üst düzey hello birini kullanmalıdır [SDK hizmeti](#azure-iot-service-sdks) IOT hub'ı öğreticileri hello gösterildiği gibi.

## <a name="device-twin-synchronization"></a>Cihaz çifti eşitleme
Cihaz çifti eşitlemenin kullandığı hello [özellikleri istenen](#desired-properties) cihaz çiftlerini tooconfigure içinde aygıtlar ve alma [özellikleri bildirilen](#reported-properties) , cihazları toostore hello cihaz çiftine gelen.

## <a name="direct-method"></a>Doğrudan yöntemi
A [doğrudan yöntemi](iot-hub-devguide-direct-methods.md) bir, tootrigger yöntemi tooexecute bir aygıtta bir IOT hub'ınızı API'sini çağırarak yoldur.

## <a name="endpoint"></a>Uç Nokta
IOT hub'ı birden çok gösterir [uç noktaları](iot-hub-devguide-endpoints.md) uygulamaları tooconnect toohello IOT hub'ınızı etkinleştirin. Gönderme gibi cihazlar tooperform işlemlerini etkinleştirmek aygıt'e yönelik uç noktalar vardır [cihaz bulut](#device-to-cloud) iletileri ve alma [bulut cihaz](#cloud-to-device) iletileri. Etkinleştirme hizmeti kullanıma yönelik yönetim uç noktalar vardır [arka uç uygulamaları](#back-end-app) tooperform işlemleri gibi [cihaz kimliği](#device-identity) ve cihaz çifti yönetimi. Hizmet dönük vardır [yerleşik uç noktaları](#built-in-endpoints) cihaz-bulut iletileri okumak için. Oluşturabileceğiniz [özel uç noktaları](#custom-endpoints) tooreceive cihaz bulut iletilerini tarafından gönderilen bir [yönlendirme kuralı](#routing-rules).

## <a name="event-hubs-service"></a>Olay hub'ları hizmeti
[Olay hub'ları](../event-hubs/event-hubs-what-is-event-hubs.md) milyonlarca işleyebilen bir yüksek düzeyde ölçeklenebilir veri alım sistemidir saniye başına olayların. Merhaba hizmet tooprocess sağlar ve veri bağlı cihazlarınız ve uygulamalarınız tarafından üretilen oldukça büyük miktardaki hello analiz edin. Merhaba IOT Hub hizmeti ile bir karşılaştırması için bkz: [karşılaştırma Azure IOT Hub ve Azure Event Hubs](iot-hub-compare-event-hubs.md).

## <a name="event-hub-compatible-endpoint"></a>Olay Hub ile uyumlu uç noktası
tooread [cihaz bulut](#device-to-cloud) tooyour IOT hub'a gönderilen iletileri, tooan uç noktası, hub'ına bağlanmak ve bu iletilerin bir Event Hub ile uyumlu yöntemi tooread kullanın. Event Hub ile uyumlu yöntemleri dahil hello kullanarak [olay hub'ları SDK'ları](../event-hubs/event-hubs-programming-guide.md) ve [Azure akış analizi](../stream-analytics/stream-analytics-introduction.md).

## <a name="field-gateway"></a>Alan ağ geçidi
Bağlantıyı doğrudan çok bağlanamıyor cihazlar için bir alan ağ geçidi etkinleştirir[IOT hub'ı](#iot-hub) ve genellikle cihazlarınızı yerel olarak dağıtılır. Daha fazla bilgi için bkz: [Azure IOT Hub nedir?](iot-hub-what-is-iot-hub.md)

## <a name="free-account"></a>Ücretsiz hesap
Oluşturabileceğiniz bir [ücretsiz Azure hesabı](https://azure.microsoft.com/pricing/free-trial/) toocomplete IOT hub'ı öğreticileri hello ve hello IOT Hub hizmeti (ve diğer Azure hizmetleriyle) deneyin.

## <a name="gateway"></a>Ağ geçidi
Bağlantıyı doğrudan çok bağlanamıyor cihazlar için bir ağ geçidi etkinleştirir[IOT hub'ı](#iot-hub). Ayrıca bkz. [alan ağ geçidi](#field-gateway), [bulut ağ geçidi](#cloud-gateway), ve [özel ağ geçidi](#custom-gateway).

## <a name="identity-registry"></a>Kimlik kayıt defteri
Merhaba [kimlik kayıt defteri](iot-hub-devguide-identity-registry.md) olan hello yerleşik bileşeni hello ayrı aygıtlar hakkındaki bilgileri depolayan bir IOT hub'ın izin tooconnect tooan IOT hub'ı.

## <a name="interactive-message"></a>Etkileşimli iletisi
Etkileşimli bir ileti bir [bulut cihaz](#cloud-to-device) hello çözüm arka ucu anlık bir eylemi tetikleyen ileti. Örneğin, bir aygıt tooa CRM sisteminde oturum otomatik olarak bir hata hakkında bir uyarı gönderebilir.

## <a name="iot-hub"></a>IoT Hub’ı
IOT hub'ı milyonlarca cihaza arasında güvenilir ve güvenli çift yönlü iletişimler sağlayan tam olarak yönetilen bir Azure hizmeti olduğundan ve bir çözüm arka ucu. Daha fazla bilgi için bkz: [Azure IOT Hub nedir?](iot-hub-what-is-iot-hub.md) Kullanarak, [Azure aboneliği](#subscription), IOT hub'ları toohandle iş yükleri Mesajlaşma, IOT oluşturabilirsiniz.

## <a name="iot-hub-metrics"></a>IOT hub'ı ölçümleri
[IOT hub'ı ölçümleri](iot-hub-metrics.md) hello IOT hub'ları hello durumuyla ilgili size, [Azure aboneliği](#subscription). IOT hub'ı ölçümleri etkinleştir, tooassess hello hizmeti ve hello cihazların genel durumunu hello tooit bağlı. IOT hub'ı ölçümleri IOT hub'ınıza neler olup bittiğini görmek ve toocontact Azure desteğine gerek kalmadan kök neden sorunları araştırmanıza yardımcı olabilir.

## <a name="iot-hub-query-language"></a>IOT hub'ı sorgulama dili
Merhaba [IOT hub'ı sorgu dili](iot-hub-devguide-query-language.md) tooquery sağlayan SQL benzeri bir dil olan, [işleri](#job) ve cihaz çiftlerini.

## <a name="iot-hub-resource-provider-rest-api"></a>IOT hub'ı kaynak sağlayıcısı REST API'si
Merhaba kullanabilirsiniz [IOT Hub kaynak sağlayıcısı REST API](https://docs.microsoft.com/rest/api/iothub/resourceprovider/iot-hub-resource-provider-rest) toomanage hello IOT hub'ları, [Azure aboneliği](#subscription) oluşturma, güncelleştirme ve hub'ları silme gibi işlemleri gerçekleştirme.

## <a name="iot-suite"></a>IoT Paketi
Azure IOT paketi önceden yapılandırılmış çözümleri birden çok Azure hizmetleriyle birlikte paketler. Bu önceden yapılandırılmış çözümler yaygın IOT senaryolarını uçtan uca uygulamaları ile hızlı şekilde kullanmaya tooget etkinleştirin. Daha fazla bilgi için bkz: [Azure IOT paketi nedir?](../iot-suite/iot-suite-overview.md)

## <a name="iothub-explorer"></a>ıothub Gezgini
Merhaba [iothub-explorer](https://github.com/azure/iothub-explorer) platformlar arası, komut satırı aracıdır. Merhaba aracı sağlar, toomanage aygıtlarınızı hello [kimlik kayıt defteri](#identity-registry)göndermek ve iletileri ve dosyaları, almasını ve IOT hub işlemlerini izleyebilirsiniz.

## <a name="job"></a>İş
Çözüm arka ucunuz kullanabilirsiniz [işleri](iot-hub-devguide-jobs.md) cihazlar tooschedule ve izleme etkinliklerini IOT hub'ınıza kayıtlı. Etkinlikler dahil cihaz çifti güncelleştirme [özelliklerini istenen](#desired-properties), güncelleştirme cihaz çifti [etiketleri](#tags)ve çağırma [doğrudan yöntemleri](#direct-method). [IOT hub'ı](#iot-hub) de işleri çok kullanır[tooand dışarı aktarma](iot-hub-devguide-identity-registry.md#import-and-export-device-identities) hello gelen [kimlik kayıt defteri](#identity-registry).

## <a name="jobs-rest-api"></a>İşlerini REST API'si
Merhaba [işleri REST API](https://docs.microsoft.com/rest/api/iothub/jobapi) toomanage sağlar [işleri](#job) IOT hub'ınıza çalışıyor.

## <a name="module"></a>Modül
İçinde [Azure IOT kenar](iot-hub-linux-iot-edge-get-started.md), [Modülü](iot-hub-linux-iot-edge-get-started.md) belirli bir görevi gerçekleştiren bir bileşenidir. Görevler, bir CİHAZDAN bir ileti alma, bir ileti dönüştürme ya da bir ileti tooan IOT hub'ı gönderme içerebilir. Bir aracı modülleri arasında iletilerini yönlendirmede sorumludur. Azure IOT kenar örnek modüllerini içerir. Kendi özel modüller de oluşturabilirsiniz.

## <a name="mqtt"></a>MQTT
[MQTT](http://mqtt.org/) olan bir hello Mesajlaşma protokolleri [IOT hub'ı](#iot-hub) aygıtlarıyla iletişim kurmak için destekler. Hello Mesajlaşma IOT hub'ı destekleyen protokolleri hakkında daha fazla bilgi için bkz: [IOT Hub ile iletileri almasına ve göndermesine](iot-hub-devguide-messaging.md).

## <a name="operations-monitoring"></a>İşlemleri izleme
IOT hub'ı [izleme işlemleri](iot-hub-operations-monitoring.md) toomonitor hello durumunu gerçek zamanlı IOT hub'ınızı işlemlerinin sağlar. [IOT hub'ı](#iot-hub) işlemlerinin birkaç kategoriler arasında olayları izler. Bir veya daha fazla kategorileri tooan IOT hub'ı uç işleme için gelen olayları göndermeyi seçebilirsiniz. Merhaba veri hataları izleme veya veri düzenlerini esas alarak daha karmaşık işleme ayarlayın.

## <a name="physical-device"></a>Fiziksel cihaz
Bir fiziksel aygıt tooan IOT hub'a bağlanan Raspberry Pi'yi gibi gerçek bir aygıttır. Kolaylık olması için birçok hello IOT hub'ı öğreticileri kullanmak [benzetimli aygıtları](#simulated-device) , toorun örnekleri yerel makinenizde tooenable.

## <a name="primary-and-secondary-keys"></a>Birincil ve ikincil anahtarları
Tooa aygıt dönük bağladığınızda veya hizmet'e yönelik uç noktası bir IOT hub'ında, [bağlantı dizesi](#connection-string) size erişim anahtar toogrant içerir. Bir aygıt toohello eklediğinizde [kimlik kayıt defteri](#identity-registry) veya ekleme bir [paylaşılan erişim ilkesi](#shared-access-policy) tooyour hub'ı hello hizmeti birincil ve ikincil bir anahtar oluşturur. Bir anahtar toohello IOT hub'ı erişimi kaybetmeden güncelleştirdiğinizde iki anahtarına sahip tooroll üzerinden bir anahtar tooanother sağlar.

## <a name="protocol-gateway"></a>Protokol ağ geçidi
Bir protokol ağ geçidi genellikle hello bulutta dağıtılır ve protokolü çok bağlanan cihazlar için çeviri hizmetleri sağlayan[IOT hub'ı](#iot-hub). Daha fazla bilgi için bkz: [Azure IOT Hub nedir?](iot-hub-what-is-iot-hub.md)

## <a name="quotas-and-throttling"></a>Kotalar ve azaltma
Vardır çeşitli [kotaları](iot-hub-devguide-quotas-throttling.md) tooyour kullanımını uygulamak [IOT hub'ı](#iot-hub), kotalar farklılık hello hello IOT hub'ı hello katmanını temel alan çoğu. [IOT hub'ı](#iot-hub) de geçerlidir [kısıtlar](iot-hub-devguide-quotas-throttling.md) çalışma zamanında hello hizmetinin tooyour kullanın.

## <a name="reported-configuration"></a>Bildirilen yapılandırma
Merhaba bağlamındaki bir [cihaz çifti](iot-hub-devguide-device-twins.md), bildirilen yapılandırma başvuruyor toohello eksiksiz özelliklerinin ve meta veri olmalıdır hello cihaz çiftine toohello çözüm arka ucu rapor.

## <a name="reported-properties"></a>Bildirilen özellikleri
Merhaba bağlamındaki bir [cihaz çifti](iot-hub-devguide-device-twins.md), Özellikler hello cihaz çifti ile kullanılan alt bildirilir [özelliklerini istenen](#desired-properties) toosynchronize aygıt yapılandırması veya koşul. Yalnızca ayarlanabilir hello tarafından bildirilen [cihaz uygulaması](#device-app) ve okunabilir ve tarafından sorgulanan bir [arka uç uygulama](#back-end-app).

## <a name="resource-group"></a>Kaynak grubu
[Azure Resource Manager](#azure-resource-manager) kullanan kaynak grupları toogroup ilgili kaynakları birlikte. Merhaba grubu üzerinde aynı anda bir kaynak grubu tooperform işlemlerini tüm hello kaynaklardaki kullanabilirsiniz.

## <a name="retry-policy"></a>Yeniden deneme ilkesi
Yeniden deneme ilkesi toohandle kullandığınız [geçici hataları](https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx) tooa bulut hizmeti bağladığınızda.

## <a name="routing-rules"></a>Yönlendirme kuralları
Yapılandırdığınız [yönlendirme kuralları](iot-hub-devguide-messages-read-custom.md) , IOT hub tooroute cihaz bulut iletilerini tooa içinde [yerleşik uç nokta](#built-in-endpoints) veya çok[özel uç noktaları](#custom-endpoints) çözüm arka işlemesi için Son.

## <a name="sasl-plain"></a>SASL DÜZ
SASL DÜZ hello bir protokol olan [AMQP](#advanced-message-queue-protocol) Protokolü tootransfer güvenlik belirteçlerini kullanır.

## <a name="shared-access-signature"></a>Paylaşılan erişim imzası
Paylaşılan erişim imzaları (SAS), SHA-256 güvenli karmaları veya URI dayalı bir kimlik doğrulama mekanizmasıdır. SAS kimlik doğrulaması iki bileşeni vardır: bir _paylaşılan erişim ilkesi_ ve _paylaşılan erişim imzası_ (genellikle bir belirteç olarak da adlandırılır). Bir cihaz IOT hub ile SAS tooauthenticate kullanır. [Arka uç uygulamaları](#back-end-app) ayrıca bir IOT hub'ındaki hello service'e yönelik uç noktaları SAS tooauthenticate kullanın. Genellikle, hello hello SAS belirteci dahil [bağlantı dizesi](#connection-string) uygulama tooestablish bir bağlantı tooan IOT hub'ı kullanır.

## <a name="shared-access-policy"></a>Paylaşılan Erişim İlkesi
Geçerli bir sahip tooanyone hello izinler bir paylaşılan erişim ilkesi tanımlar [birincil veya ikincil anahtarı](#primary-and-secondary-keys) Bu ilkeyle ilişkilendirilmiş. Merhaba, hub'ınız için hello paylaşılan erişim ilkeleri ve anahtarları yönetebilir [portal](#azure-portal).

## <a name="simulated-device"></a>Sanal cihaz
Kolaylık olması için IOT hub'ı öğreticilerini kullanma hello birçoğu, toorun yerel makinenizde örnekleri aygıtları tooenable benzetimi. Buna karşılık, bir [fiziksel aygıt](#physical-device) tooan IOT hub'a bağlanan Raspberry Pi'yi gibi gerçek bir aygıttır.

## <a name="solution"></a>Çözüm
A _çözüm_ bir veya daha fazla projeleri içeren tooa Visual Studio çözümü başvurabilir. A _çözüm_ cihazları gibi öğeleri içerir tooan IOT çözüm de başvurabilir [cihaz uygulamaları](#device-app), IOT hub'ı, diğer Azure hizmetleriyle ve [arka uç uygulamaları](#back-end-app).

## <a name="subscription"></a>Abonelik
Bir Azure aboneliği faturalama gerçekleştiği ' dir. Her Azure kaynak oluşturduğunuz veya Azure hizmeti kullandığınız tek bir abonelik ile ilişkilendirilir. Birçok kotaları da hello bir abonelik düzeyinde uygulanır.

## <a name="system-properties"></a>Sistem özellikleri
Merhaba bağlamındaki bir [cihaz çifti](iot-hub-devguide-device-twins.md), Sistem özellikleri salt okunurdur ve son etkinlik süresi ve bağlantı durumu gibi hello Aygıt kullanımı ile ilgili bilgiler içerir.

## <a name="tags"></a>Etiketler
Merhaba bağlamındaki bir [cihaz çifti](iot-hub-devguide-device-twins.md), etiketleri, cihaz meta verilerini depolanır ve bir JSON belgesinin hello formunda hello çözüm arka ucu tarafından alınır. Etiketler, bir cihazda görünür tooapps değildir.

## <a name="telemetry"></a>Telemetri
Cihazları Rüzgar hızı veya sıcaklık, gibi telemetri verileri toplama ve kullanma [veri noktası iletileri](#data-point-messages) toosend hello telemetri tooan IOT hub'ı.

## <a name="token-service"></a>Belirteç Hizmeti
Belirteç Hizmeti tooimplement bir kimlik doğrulama mekanizması aygıtlarınız için kullanabilirsiniz. IOT hub'ı kullanan [paylaşılan erişim ilkesi](#shared-access-policy) ile **DeviceConnect** izinleri toocreate *aygıt kapsamlı* belirteçleri. Bu belirteçler bir aygıt tooconnect tooyour IOT hub'ı etkinleştirin. Bir aygıt bir özel kimlik doğrulama mekanizması tooauthenticate hello belirteci hizmetiyle kullanır. Merhaba aygıt başarıyla doğruladığında, hello belirteci hizmeti IOT hub'ınızı hello aygıt toouse tooaccess için bir SAS belirteci verir.

## <a name="x509-client-certificate"></a>X.509 istemci sertifikası
Bir aygıt ile bir X.509 sertifikası tooauthenticate kullanabilirsiniz [IOT hub'ı](#iot-hub). X.509 sertifikası kullanarak bir alternatif toousing olan bir [SAS belirteci](#shared-access-signature).
