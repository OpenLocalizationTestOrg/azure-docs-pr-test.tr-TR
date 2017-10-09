> [!div class="op_single_selector"]
> * [Linux](../articles/iot-hub/iot-hub-linux-iot-edge-simulated-device.md)
> * [Windows](../articles/iot-hub/iot-hub-windows-iot-edge-simulated-device.md)

Bu kılavuz hello [sanal cihaz bulut karşıya örnek] nasıl gösterir toouse [Azure IOT kenar] [ lnk-sdk] benzetimli gelen toosend cihaz bulut telemetri tooIoT Hub cihazlar.

Bu kılavuzda aşağıdaki konular ele alınmaktadır:

* **Mimari**: hello mimari bilgilerini [sanal cihaz bulut karşıya örnek].
* **Derleme ve çalıştırma**: hello adımları gerekli toobuild ve çalışma hello örnek.

## <a name="architecture"></a>Mimari

Merhaba [sanal cihaz bulut karşıya örnek] toocreate telemetri gönderen bir ağ geçidi aygıtları tooan IOT hub'ı nasıl benzetimli gösterir. Bir aygıt mümkün tooconnect olmayabilir doğrudan tooIoT Hub çünkü hello cihaz:

* IOT Hub tarafından anlaşılan bir iletişim protokolü kullanmaz.
* IOT Hub tarafından yeterince akıllı tooremember hello atanan kimlik tooit değil.

Bir IOT sınır ağ geçidi yolları aşağıdaki hello'de bu sorunları çözebilir:

* Merhaba ağ geçidi hello aygıt tarafından kullanılan hello Protokolü anlayan, cihaz bulut telemetri hello aygıttan alır ve bu iletileri tooIoT hello IOT hub tarafından anlaşılan protokolünü kullanarak Hub iletir.

* Merhaba ağ geçidi IOT hub'ı kimlikleri toodevices eşler ve bir cihaz iletileri tooIoT Hub gönderdiğinde bir proxy gibi davranır.

Aşağıdaki diyagramda hello hello örnek ana bileşenlerinin Merhaba, hello IOT kenar modüller de dahil olmak üzere gösterir:

![][1]

Merhaba modülleri iletileri geçirmek değil doğrudan tooeach diğer. Merhaba modülleri hello iletileri toohello abonelik mekanizmasını kullanarak diğer modüller sunar iletileri tooan iç Aracısı yayımlayın. Daha fazla bilgi için bkz: [Azure IOT Edge ile çalışmaya başlama][lnk-gw-getstarted].

### <a name="protocol-ingestion-module"></a>Protokol alım modülü

Bu modül için alıcı veri aygıtlardan hello ağ geçidi üzerinden ve hello buluta başlangıç noktası hello ' dir. Merhaba örnek hello Modülü:

1. Benzetimli sıcaklık veri oluşturur. Fiziksel aygıtların kullanırsanız, hello modülü fiziksel aygıtların verileri okur.
1. Bir ileti oluşturur.
1. Merhaba benzetimli sıcaklık verileri hello ileti içeriği yerleştirir.
1. Sahte bir MAC adresi toohello iletisiyle bir özellik ekler.
1. Merhaba ileti kullanılabilir toohello sonraki modüle hello zincirinde yapar.

adlı hello Modülü **Protokolü X alım** hello önceki diyagramda adlı **sanal cihaz** hello kaynak kodunda.

### <a name="mac-lt-gt-iot-hub-id-module"></a>MAC &lt;-&gt; IoT Hub kimlik modülü

Bu modül için bir Mac adresi özelliğine sahip iletileri tarar. Hello örnek hello Protokolü alım modülü hello MAC adres özelliği ekler. Merhaba modülü böyle bir özellik bulursa, bir IOT Hub cihaz anahtar toohello iletisi içeren başka bir özellik ekler. Merhaba modülü hello zincirinde sonra hello ileti kullanılabilir toohello sonraki modüle hale getirir.

MAC adreslerinin ve IOT hub'ı kimlikleri tooassociate benzetimli hello IOT Hub cihaz kimliklerini aygıtlarla arasında bir eşleme Hello Geliştirici ayarlar. Merhaba Geliştirici hello eşleme hello modülü yapılandırmasının bir parçası el ile ekler.

> [!NOTE]
> Bu örnekte benzersiz cihaz tanımlayıcısı olarak bir MAC adresi kullanılır ve bir IoT Hub cihaz kimliğiyle ilişkilendirilir. Bununla birlikte, farklı bir benzersiz tanımlayıcı kullanan kendi modülünüzü yazabilirsiniz. Örneğin, aygıtlarınızı benzersiz seri numarasına sahip veya bir benzersiz katıştırılmış cihaz adı hello telemetri verileri içerebilir.

### <a name="iot-hub-communication-module"></a>IoT Hub iletişim modülü

Bu modül iletileri bir IOT Hub ile Merhaba önceki modülü tarafından atanan aygıt anahtar özelliği alır. Merhaba modülü içerik tooIoT hub'ı kullanarak HTTP protokolü hello hello iletisi gönderir. HTTP IOT Hub tarafından anlaşılan üç protokolden Merhaba biridir.

Her sanal cihaz için bir bağlantı açarak yerine bu modül hello ağ geçidi toohello IOT hub'ından HTTP tek bir bağlantı açar. Merhaba modülü tüm benzetimli hello cihazlar gelen bağlantıları Bu bağlantı üzerinden sonra multiplexes. Bu yaklaşım, tek bir ağ geçidi tooconnect pek çok daha fazla aygıtları sağlar.

## <a name="before-you-get-started"></a>Başlamadan önce

Başlamadan önce şunları yapmalısınız:

* [IOT hub oluşturma] [ lnk-create-hub] Azure aboneliğinizde bu kılavuzda, hub toocomplete hello adı gerekir. Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.
* İki aygıtları tooyour IOT hub'ı ekleyin ve kendi kimlikleri ve cihaz anahtarlarını not edin. Merhaba kullanabilirsiniz [aygıt explorer] [ lnk-device-explorer] veya [iothub-explorer] [ lnk-iothub-explorer] tooadd hello oluşturduğunuz aygıtları toohello IOT hub'ınızı aracı Önceki adım ve kendi anahtarları alır.

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