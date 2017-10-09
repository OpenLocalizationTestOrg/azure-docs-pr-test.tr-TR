> [!div class="op_single_selector"]
> * [Cihaz: Node.js Service: Node.js](../articles/iot-hub/iot-hub-node-node-device-management-get-started.md)
> * [Cihaz: Node.js Service: C#](../articles/iot-hub/iot-hub-csharp-node-device-management-get-started.md)
> * [Aygıt: Java hizmet: Java](../articles/iot-hub/iot-hub-java-java-device-management-getstarted.md)

Arka uç uygulamaları kullanabileceğiniz Azure IOT Hub temelleri gibi [cihaz çifti] [ lnk-devtwin] ve [doğrudan yöntemleri][lnk-c2dmethod], tooremotely başlatmak ve izleme cihazlarda cihaz yönetim işlemleri. Bu öğreticide, nasıl bir arka uç uygulaması ve cihaz uygulaması tooinitiate birlikte çalışır ve IOT hub'ı kullanarak bir uzak aygıt yeniden başlatma izlemek gösterilir.

Merhaba bulutta bir arka uç uygulamasından doğrudan yöntemi tooinitiate aygıt yönetimi Eylemler (örneğin, yeniden başlatma, Fabrika sıfırlaması ve üretici yazılımı güncelleştirmesi) kullanın. Merhaba aygıt sorumludur:

* IOT Hub'ından gönderilen hello yöntemi isteği işleme.
* Hello karşılık gelen aygıta özgü eylemin hello aygıtta başlatılıyor.
* Durum güncelleştirmeleri aracılığıyla sağlama *özellikleri bildirilen* tooIoT Hub.

Bir arka uç uygulaması hello bulut toorun cihaz çifti sorguları tooreport hello ilerlemeyi cihaz yönetim eylemlerinin kullanabilirsiniz.

[lnk-devtwin]: ../articles/iot-hub/iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
