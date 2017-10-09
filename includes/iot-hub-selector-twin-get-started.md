> [!div class="op_single_selector"]
> * [Node.js](../articles/iot-hub/iot-hub-node-node-twin-getstarted.md)
> * [C#/node.js](../articles/iot-hub/iot-hub-csharp-node-twin-getstarted.md)
> * [C#](../articles/iot-hub/iot-hub-csharp-csharp-twin-getstarted.md)
> * [Java](../articles/iot-hub/iot-hub-java-java-twin-getstarted.md)

Cihaz çiftleri, cihaz durumu bilgilerini (meta veriler, yapılandırmalar ve koşullar) depolayan JSON belgelerdir. IOT Hub cihaz çifti tooit bağlanan her aygıt için devam ettirir.

Cihaz çiftlerini kullanın:

* Çözüm arka ucunuz cihaz meta verilerini depolar.
* Kullanılabilir özellikler ve koşullar (kullanılan gibi hello bağlantı yöntemi) gibi geçerli durumu bilgileri, cihaz uygulamanızdan bildirin.
* Cihaz uygulama ve arka uç uygulama arasında uzun süre çalışan iş akışları (örneğin, bellenim ve yapılandırma güncelleştirmeleri) Hello durumunu eşitleyin.
* Cihaz meta verilerini, yapılandırma veya durumu sorgu.

> [!NOTE]
> Cihaz çiftlerini cihaz yapılandırmalarını ve koşullar sorgulamak için ve eşitleme için tasarlanmıştır. Toouse cihaz çiftlerini zaman bulunabilir hakkında daha fazla bilgiler [cihaz çiftlerini anlamak][lnk-twins].

Cihaz çiftlerini bir IOT hub ' depolanır ve içerir:

* *Etiketler*, cihaz meta verilerini yalnızca hello çözüm arka ucu tarafından; erişilebilir
* *Özellikler istenen*, JSON nesnelerini hello çözümü tarafından değiştirilebilir hello cihaz uygulaması tarafından; başa bitiş ve observable ve
* *Özellikler bildirilen*, JSON nesnelerini hello cihaz uygulaması tarafından değiştirilebilir ve hello çözüm arka ucu tarafından okunabilir. Etiketleri ve özellikleri diziler içeremez, ancak nesneleri iç içe olamaz.

![][img-twin]

Ayrıca, hello çözüm arka ucu veri yukarıdaki tüm hello dayalı cihaz çiftlerini sorgulayabilirsiniz.
Çok başvuran[cihaz çiftlerini anlamak] [ lnk-twins] cihaz çiftlerini ve toohello hakkında daha fazla bilgi için [IOT hub'ı sorgu dili] [ lnk-query] başvurusu sorgulama için.

> [!NOTE]
> Şu anda cihaz çiftlerini tooIoT hub'a bağlanan aygıtlardan erişilebilir hello MQTT protokolünü kullanarak. Lütfen toohello bakın [MQTT Destek] [ lnk-devguide-mqtt] hakkında yönergeler için makalenin tooconvert mevcut aygıt uygulama toouse MQTT.

Bu öğretici şunların nasıl yapıldığını gösterir:

* Ekler bir arka uç uygulaması oluşturma *etiketleri* tooa cihaz çifti ve bağlantısını raporları bir sanal cihaz uygulamasının kanal olarak bir *özelliği bildirilen* hello cihaz çifti üzerinde.
* Merhaba etiketleri ve daha önce oluşturduğunuz özellikleri filtreleri kullanarak arka uç uygulamanızı aygıtlardan sorgu.

<!-- images -->
[img-twin]: media/iot-hub-selector-twin-get-started/twin.png

<!-- links -->
[lnk-query]: ../articles/iot-hub/iot-hub-devguide-query-language.md
[lnk-twins]: ../articles/iot-hub/iot-hub-devguide-device-twins.md
[lnk-d2c]: ../articles/iot-hub/iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: ../articles/iot-hub/iot-hub-mqtt-support.md