> [!div class="op_single_selector"]
> * [Linux](../articles/iot-hub/iot-hub-linux-iot-edge-simulated-device.md)
> * [Windows](../articles/iot-hub/iot-hub-windows-iot-edge-simulated-device.md)

Bu kılavuz [sanal cihaz bulut karşıya örnek] nasıl kullanılacağını gösterir [Azure IOT kenar] [ lnk-sdk] sanal cihazlar IOT Hub'ına cihaz bulut telemetri göndermek için .

Bu kılavuzda aşağıdaki konular ele alınmaktadır:

* **Mimari**: Mimari bilgilerini [sanal cihaz bulut karşıya örnek].
* **Derleme ve çalıştırma**: örneği derlemek ve çalıştırmak için gerekli adımlar.

## <a name="architecture"></a>Mimari

[sanal cihaz bulut karşıya örnek] telemetri benzetimli aygıtlardan bir IOT hub'ına gönderir. bir ağ geçidi oluşturulacağını gösterir. Bir aygıt için doğrudan IOT Hub'ına bağlanmak mümkün olmayabilir cihaz:

* IOT Hub tarafından anlaşılan bir iletişim protokolü kullanmaz.
* IOT Hub tarafından atanmış kimlik anımsaması akıllı değil.

Bir IOT sınır ağ geçidi aşağıdaki yollarla bu sorunları çözebilir:

* Ağ Geçidi aygıt tarafından kullanılan protokol CİHAZDAN cihaz bulut telemetri alır ve IOT hub'ın IOT hub tarafından anlaşılan protokolünü kullanarak bu iletileri iletir bilir.

* Ağ geçidi aygıtına IOT hub'ı kimlikleri eşler ve bir cihaz IOT Hub'ına iletileri gönderdiğinde bir proxy gibi davranır.

Aşağıdaki diyagramda IOT kenar modüller de dahil olmak üzere örnek ana bileşenlerini gösterir:

![][1]

Modüller iletileri doğrudan birbirine geçirmez. Modülleri iletilerini bir abonelik mekanizması kullanarak diğer modüller ve iletileri teslim bir iç aracısı için yayımlayın. Daha fazla bilgi için bkz: [Azure IOT Edge ile çalışmaya başlama][lnk-gw-getstarted].

### <a name="protocol-ingestion-module"></a>Protokol alım modülü

Bu modül veri aygıtlar, ağ geçidi üzerinden ve buluta gönderimini için başlangıç noktasıdır. Aşağıdaki örnekte, modül:

1. Benzetimli sıcaklık veri oluşturur. Fiziksel aygıtların kullanırsanız, modül fiziksel aygıtların verileri okur.
1. Bir ileti oluşturur.
1. Benzetimli sıcaklık verileri ileti içeriği yerleştirir.
1. Sahte bir MAC adresine sahip bir özellik iletiye ekler.
1. İleti zincirinde sonraki modülü için kullanılabilir hale getirir.

Modül adı verilen **Protokolü X alım** önceki diyagramda adlı **sanal cihaz** kaynak kodundaki.

### <a name="mac-lt-gt-iot-hub-id-module"></a>MAC &lt;-&gt; IoT Hub kimlik modülü

Bu modül için bir Mac adresi özelliğine sahip iletileri tarar. Aşağıdaki örnekte Protokolü alım modülü MAC adres özelliği ekler. Modül böyle bir özellik bulursa, iletiyi bir IOT Hub cihaz anahtarı ile başka bir özellik ekler. Modül sonra ileti sonraki modüle zincirinde kullanılabilmesini sağlar.

Sanal cihazlar IOT Hub cihaz kimliklerini ile ilişkilendirmek için MAC adreslerinin ve IOT hub'ı kimlikleri arasında bir eşleme Geliştirici ayarlar. Geliştirici eşleme modülü yapılandırmasının bir parçası el ile ekler.

> [!NOTE]
> Bu örnekte benzersiz cihaz tanımlayıcısı olarak bir MAC adresi kullanılır ve bir IoT Hub cihaz kimliğiyle ilişkilendirilir. Bununla birlikte, farklı bir benzersiz tanımlayıcı kullanan kendi modülünüzü yazabilirsiniz. Örneğin, cihazlarınızı benzersiz seri numarasına sahip veya telemetri verilerini benzersiz katıştırılmış cihaz adı içerebilir.

### <a name="iot-hub-communication-module"></a>IoT Hub iletişim modülü

Bu modül iletileri bir IOT Hub ile önceki modülü tarafından atanan aygıt anahtar özelliği alır. Modül HTTP protokolünü kullanarak ileti içeriği IOT Hub'ına gönderir. HTTP, IoT Hub tarafından anlaşılan üç protokolden biridir.

Her sanal cihaz için bir bağlantı açarak yerine bu modül IOT hub'ına geçidinden tek bir HTTP bağlantısı açar. Modül, tüm sanal cihazların gelen bağlantıları Bu bağlantı üzerinden sonra multiplexes. Bu yaklaşım, pek çok daha fazla cihazları bağlamak tek bir ağ geçidi sağlar.

## <a name="before-you-get-started"></a>Başlamadan önce

Başlamadan önce şunları yapmalısınız:

* [IOT hub oluşturma] [ lnk-create-hub] Azure aboneliğinizde bu yönlendirmeyi tamamlamak için hub adı gerekiyor. Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.
* İki cihazlar IOT hub'ınızı ekleyin ve kendi kimlikleri ve cihaz anahtarlarını not edin. Kullanabilirsiniz [aygıt explorer] [ lnk-device-explorer] veya [iothub-explorer] [ lnk-iothub-explorer] cihazlarınızı IOT hub'ı önceki adımda oluşturduğunuz eklemek için aracı ve kendi anahtarları alır.

![][2]

<!-- Images -->
[1]: media/iot-hub-iot-edge-simulated-selector/image1.png
[2]: media/iot-hub-iot-edge-simulated-selector/image2.png

<!-- Links -->
[sanal cihaz bulut karşıya örnek]: https://github.com/Azure/iot-edge/blob/master/samples/simulated_device_cloud_upload/README.md
[lnk-sdk]: https://github.com/Azure/iot-edge
[lnk-gw-getstarted]: ../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md
[lnk-create-hub]: ../articles/iot-hub/iot-hub-create-through-portal.md