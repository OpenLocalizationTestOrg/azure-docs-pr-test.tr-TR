> [!div class="op_single_selector"]
> * [Node.js](../articles/iot-hub/iot-hub-node-node-twin-how-to-configure.md)
> * [C#/node.js](../articles/iot-hub/iot-hub-csharp-node-twin-how-to-configure.md)
> * [C#](../articles/iot-hub/iot-hub-csharp-csharp-twin-how-to-configure.md)
> 
> 

## <a name="introduction"></a>Giriş

İçinde [IOT Hub cihaz çiftlerini ile çalışmaya başlama][lnk-twin-tutorial], çözüm arka tooset cihaz meta verilerini nasıl son kullanma hakkında bilgi edindiniz *etiketleri*, rapor cihaz uygulaması cihaz koşulları kullanarak *özellikleri bildirilen*ve SQL benzeri bir dil kullanarak bu bilgileri sorgulayabilirsiniz.

Bu öğreticide, nasıl toouse hello hello cihaz çifti'nın öğreneceksiniz *özelliklerini istenen* ile birlikte *özellikleri bildirilen*, tooremotely cihaz uygulamalarını yapılandırın. Daha belirgin olarak Bu öğretici, bir cihaz çifti 's nasıl bildirilen gösterir ve istenen özellikler cihaz uygulamasının çok adımlı yapılandırmasını etkinleştirmek ve cihazlara hello görünürlük toohello çözüm arka ucu bu işlemi hello durumunu sağlar. Cihaz yapılandırmaları hello rolü ile ilgili daha fazla bilgi bulabilirsiniz [cihaz yönetimine genel bakış IOT Hub ile][lnk-dm-overview].

Yüksek bir düzeyde cihaz çiftlerini kullanarak hello çözüm arka ucu toospecify hello istenen yapılandırma belirli komutları göndermek yerine, hello yönetilen cihazlar için etkinleştirir. Bu hello en iyi şekilde tooupdate yapılandırmasıyla (çok önemli olduğu belirli cihaz koşullar etkileyen hello özelliği tooimmediately belirli komutları Yürüt IOT senaryolarda), ayarı sorumlu hello aygıt koyar sürekli toohello raporlama oluştu Çözüm arka ucu hello geçerli durumu ve hello güncelleştirme işleminin olası hata koşulları. Bu deseni enstrümental toohello yönetimi, cihazların büyük kümelerinin aynıdır cihazlara hello çözüm arka ucu toohave tam görünürlüğünü hello yapılandırma işlemi hello durumunu sağlar.

> [!NOTE]
> Burada aygıtları denetlenir daha etkileşimli bir şekilde (kullanıcı tarafından denetlenen bir uygulamadan fan etkinleştirin) senaryolarında kullanmayı [doğrudan yöntemleri][lnk-methods].
> 
> 

Bu öğreticide, hello telemetri yapılandırmasını bir hedef cihaz ve, hello cihaz uygulaması sonucunda çok adımlı işlem tooapply bir yapılandırma izleyen hello çözüm arka uç değişiklikleri (gerektiren bir yazılım modülü yeniden, bu örnek için güncelleştirme öğretici basit bir gecikmeyle taklit eder).

Merhaba çözüm arka ucu hello yapılandırma hello cihaz çifti'nın istenen şekilde aşağıdaki hello özelliklerinde depolar:

        {
            ...
            "properties": {
                ...
                "desired": {
                    "telemetryConfig": {
                        "configId": "{id of hello configuration}",
                        "sendFrequency": "{config}"
                    }
                }
                ...
            }
            ...
        }

> [!NOTE]
> Yapılandırmaları karmaşık nesneler olabileceği için genellikle benzersiz kimlikler atanmışlarsa (karmaları veya [GUID'ler][lnk-guid]) toosimplify kendi karşılaştırmaları.
> 
> 

Merhaba cihaz uygulaması raporları istenen hello özelliği yansıtma geçerli yapılandırmasını **telemetryConfig** özellikleri hello bildirdi:

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of hello current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Success",
                    }
                }
                ...
            }
        }

Hello nasıl bildirilen Not **telemetryConfig** ek bir özelliğe sahiptir **durum**, tooreport hello hello yapılandırmasını güncelleştirme işleminin durumunu kullanılır.

Yeni bir istenen yapılandırma alındığında hello cihaz uygulaması hello bilgi değiştirerek bekleyen yapılandırma raporları:

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of hello current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Pending",
                        "pendingConfig": {
                            "changeId": "{id of hello pending configuration}",
                            "sendFrequency": "{pending configuration}"
                        }
                    }
                }
                ...
            }
        }

Ardından, daha sonraki bir zamanda, hello cihaz uygulaması hello başarı veya başarısızlık bu işlemin özelliği yukarıda hello güncelleştirerek rapor eder.
Nasıl hello çözüm arka ucu herhangi bir anda tooquery hello tüm hello aygıtlar arasında hello yapılandırma işleminin durumunu kullanabilir olduğuna dikkat edin.

Bu öğretici şunların nasıl yapıldığını gösterir:

* Merhaba çözüm arka uçtan yapılandırma güncelleştirmeleri alıp olarak birden çok güncelleştirme raporları bir sanal cihaz uygulaması oluşturma *özellikleri bildirilen* işlem hello yapılandırmasını güncelleştirin.
* Bir aygıt, istenen yapılandırma güncelleştirmeleri hello ve ardından yapılandırma güncelleştirme işlemi sorguları hello bir arka uç uygulaması oluşturursunuz.

<!-- links -->

[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: ../articles/iot-hub/iot-hub-device-management-overview.md
[lnk-twin-tutorial]: ../articles/iot-hub/iot-hub-node-node-twin-getstarted.md
[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier
