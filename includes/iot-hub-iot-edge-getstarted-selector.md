> [!div class="op_single_selector"]
> * [Linux](../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md)
> * [Windows](../articles/iot-hub/iot-hub-windows-iot-edge-get-started.md)
> 
> 

Bu makalede hello ayrıntılı bir kılavuz sağlar [Hello World örnek kodunun] [ lnk-helloworld-sample] tooillustrate hello temel bileşenlerini hello [Azure IOT kenar] [ lnk-iot-edge] mimarisi. Merhaba örnek hello Azure IOT kenar toobuild beş saniyede bir "hello world" iletisini tooa dosyası günlüklerini basit bir ağ geçidi kullanır.

Bu kılavuzda aşağıdaki konular ele alınmaktadır:

* **Hello World örnek mimarisi**: açıklar nasıl [Azure IOT kenar mimari kavramlarını] [ lnk-edge-concepts] toohello Hello World örnek ve hello bileşenleri nasıl bir araya getireceğinizi uygulanır.
* **Nasıl toobuild hello örnek**: hello adımları gerekli toobuild hello örnek.
* **Nasıl toorun hello örnek**: hello adımları gerekli toorun hello örnek. 
* **Tipik çıkış**: hello örneği tooexpect hello örnek çalıştırdığınızda, çıktı.
* **Kod parçacıkları**: hello Hello World örnek nasıl uyguladığını kod parçacıkları tooshow koleksiyonu IOT sınır ağ geçidi bileşenlerini anahtar.


## <a name="hello-world-sample-architecture"></a>Hello World örnek mimarisi
Merhaba Hello World örnek hello önceki bölümde açıklanan hello kavramları göstermektedir. Merhaba Hello World örneği iki IOT kenar modülden oluşan bir işlem hattına sahip bir IOT sınır ağ geçidi uygular:

* Merhaba *Merhaba Dünya* modülü beş saniyede bir ileti oluşturur ve bunu toohello Günlükçü modülüne geçirir.
* Merhaba *Günlükçü* tooa dosya aldığı modülü yazma Merhaba iletileri.

![Azure IoT Edge ile oluşturulan Hello World örneğinin mimarisi][4]

Merhaba önceki bölümde açıklandığı gibi hello Hello World modülü geçemezse toohello Günlükçü modülü beş saniyede doğrudan iletileri. Bunun yerine, beş saniyede bir ileti toohello Aracısı yayımlar.

Merhaba Günlükçü modülü hello Aracısı'ndan hello iletiyi alır ve bunu temel hello ileti tooa dosyasının Merhaba içeriğine yazma davranır.

Merhaba Günlükçü modülü yalnızca hello Aracısı gelen iletileri kullanır, hiçbir zaman yeni ileti toohello Aracısı yayımlar.

![Azure IOT kenar modülleri arasında iletileri hello Aracısı nasıl yönlendirir][5]

Merhaba Yukarıdaki şekilde hello Hello World örnek ve hello göreli yollar hello mimarisi hello hello örnek farklı kısımlarını uygulayan toohello kaynak dosyaları gösterir [deposu][lnk-iot-edge]. Merhaba kodu kendiniz keşfedin veya kılavuz olarak aşağıdaki kod parçacıklarından hello kullanın.

<!-- Images -->
[4]: media/iot-hub-iot-edge-getstarted-selector/high_level_architecture.png
[5]: media/iot-hub-iot-edge-getstarted-selector/detailed_architecture.png

<!-- Links -->
[lnk-helloworld-sample]: https://github.com/Azure/iot-edge/tree/master/samples/hello_world
[lnk-iot-edge]: https://github.com/Azure/iot-edge
[lnk-edge-concepts]: ../articles/iot-hub/iot-hub-iot-edge-overview.md