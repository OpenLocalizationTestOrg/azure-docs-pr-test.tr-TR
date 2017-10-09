## <a name="configure-hello-nodejs-simulated-device"></a>Merhaba Node.js sanal cihaz yapılandırma
1. Merhaba Uzaktan izleme panosunda tıklatın **+ bir cihaz ekleme** ve ardından ekleyin bir *özel cihaz*. Merhaba IOT Hub ana bilgisayar adı, cihaz kimliği ve cihaz anahtarını Not. Merhaba remote_monitoring.js aygıt istemci uygulaması hazırlarken, bunları daha sonra Bu öğreticide gerekir.
2. Bu Node.js sürümünü olun 0.12.x sürümü veya daha sonra dağıtım makinenize yüklü. Çalıştırma `node --version` bir komut isteminde veya bir kabuk toocheck hello sürümü. Linux üzerinde bir paket Yöneticisi tooinstall Node.js kullanma hakkında daha fazla bilgi için bkz: [yükleme Node.js Paket Yöneticisi aracılığıyla][node-linux].
3. Node.js yüklendiğinde hello en son sürümünü hello kopyalama [azure IOT sdk düğüm] [ lnk-github-repo] depo tooyour geliştirme makine. Her zaman hello kullan **ana** hello en son sürümünü hello kitaplıklar ve örnekler için dal.
4. Merhaba yerel kopyasından [azure IOT sdk düğüm] [ lnk-github-repo] deposu, geliştirme makinenizde hello düğümü/aygıt/samples klasörü tooan boş klasöründen aşağıdaki iki dosyaları kopyalama hello:
   
   * Packages.JSON
   * remote_monitoring.js
5. Merhaba remote_monitoring.js dosyasını açın ve değişken tanımını izleyen Merhaba bakın:
   
    ```
    var connectionString = "[IoT Hub device connection string]";
    ```
6. Değiştir **[IOT Hub cihaz bağlantı dizesi]** cihaz bağlantı dizesine sahip. IOT Hub ana bilgisayar adı, cihaz kimliği ve 1. adımda not yapılan aygıt anahtarı için başlangıç değerlerini kullanın. Bir aygıt bağlantı dizesi biçimi aşağıdaki hello sahiptir:
   
    ```
    HostName={your IoT Hub hostname};DeviceId={your device id};SharedAccessKey={your device key}
    ```
   
    IOT Hub ana bilgisayar adına ise **contoso** ve cihaz kimliğinizi **mydevice**, bağlantı dizenizi hello parçacığını aşağıdaki gibi görünür:
   
    ```
    var connectionString = "HostName=contoso.azure-devices.net;DeviceId=mydevice;SharedAccessKey=2s ... =="
    ```
7. Merhaba dosyasını kaydedin. Aşağıdaki komutlar bir kabuk ya da komut istemi kullanarak bu dosyaları tooinstall hello gerekli paketleri içeren hello klasördeki hello çalıştırın ve hello örnek uygulamayı çalıştırın:
   
    ```
    npm install
    node remote_monitoring.js
    ```

## <a name="observe-dynamic-telemetry-in-action"></a>Eylem dinamik telemetri inceleyin
Başlangıç Panosu hello sıcaklık ve nem telemetrisinden hello varolan sanal cihazlar gösterir:

![Merhaba varsayılan pano][image1]

Merhaba Node.js sanal cihaz hello önceki bölümde çalıştırdığınız seçerseniz, sıcaklık ve nem dış sıcaklığı telemetri bakın:

![Dış sıcaklığı toohello Pano Ekle][image2]

Merhaba Uzaktan izleme çözümü otomatik olarak hello ek dış sıcaklığı telemetri türünü algılar ve hello Panoda toohello grafik ekler.

[node-linux]: https://github.com/nodejs/node-v0.x-archive/wiki/Installing-Node.js-via-package-manager
[lnk-github-repo]: https://github.com/Azure/azure-iot-sdk-node
[image1]: media/iot-suite-send-external-temperature/image1.png
[image2]: media/iot-suite-send-external-temperature/image2.png