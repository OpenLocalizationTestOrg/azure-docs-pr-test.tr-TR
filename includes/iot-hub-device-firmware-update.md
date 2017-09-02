## <a name="create-a-simulated-device-app"></a>Sanal cihaz uygulaması oluşturma
Bu bölümde şunları yapacaksınız:

* Bulut tarafından çağrılan doğrudan bir yönteme yanıt veren bir Node.js konsol uygulaması oluşturma
* Sanal bir üretici yazılımı güncelleştirmesini tetikleme
* Cihaz ikizi sorgularının cihazları ve bir üretici yazılımı güncelleştirmesini en son ne zaman tamamladığını belirlemesi için rapor edilen özellikleri kullanın

1. adım: adlı boş bir klasör oluşturun **manageddevice**.  Komut isteminizde aşağıdaki komutu kullanarak **manageddevice** klasöründe bir package.json dosyası oluşturun. Tüm varsayılanları kabul edin:
   
    ```
    npm init
    ```

2. adım: İsteminizde komutu **manageddevice** klasörü yüklemek için aşağıdaki komutu çalıştırın, **azure IOT cihaz** ve **azure-IOT-cihaz-mqtt** cihaz SDK'sı paketler:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

3. adım: bir metin düzenleyicisi kullanarak, oluşturduğunuz bir **dmpatterns_fwupdate_device.js** dosyasını **manageddevice** klasör.

4. adım: aşağıdaki 'İste' deyimleri başlangıcında ekleme **dmpatterns_fwupdate_device.js** dosyası:
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. adım: Ekleme bir **connectionString** değişkeni ve oluşturmak için kullanın bir **istemci** örneği. `{yourdeviceconnectionstring}` yer tutucusunu, daha önce "Cihaz kimliği oluşturma" bölümünde not aldığınız bağlantı dizesiyle değiştirin:
   
    ```
    var connectionString = '{yourdeviceconnectionstring}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

6. adım: bildirilen özelliklerini güncelleştirmek için kullanılan aşağıdaki işlevi ekleyin:
   
    ```
    var reportFWUpdateThroughTwin = function(twin, firmwareUpdateValue) {
      var patch = {
          iothubDM : {
            firmwareUpdate : firmwareUpdateValue
          }
      };
   
      twin.properties.reported.update(patch, function(err) {
        if (err) throw err;
        console.log('twin state reported: ' + firmwareUpdateValue.status);
      });
    };
    ```

7. adım: indirme ve bellenim yansımayı benzetimini aşağıdaki işlevi ekleyin:
   
    ```
    var simulateDownloadImage = function(imageUrl, callback) {
      var error = null;
      var image = "[fake image data]";
   
      console.log("Downloading image from " + imageUrl);
   
      callback(error, image);
    }
   
    var simulateApplyImage = function(imageData, callback) {
      var error = null;
   
      if (!imageData) {
        error = {message: 'Apply image failed because of missing image data.'};
      }
   
      callback(error);
    }
    ```

8. adım: güncelleştirmeleri bildirilen özellikleri aracılığıyla bellenim güncelleştirme durumu aşağıdaki işlevi ekleyin **bekleyen**. Genellikle, cihazlar kullanılabilir güncelleştirmeden haberdar edilir ve yönetici tarafından tanımlanan bir ilke, cihazın güncelleştirmeyi indirip uygulamaya başlamasına neden olur. Bu işlev, ilgili ilkeyi etkinleştirme mantığının çalışması gereken yerdir. Kolaylık olması için örnek dört bellenim görüntüsünü karşıdan yüklemek için saniye devam etmeden önce bekler:
   
    ```
    var waitToDownload = function(twin, fwPackageUriVal, callback) {
      var now = new Date();
   
      reportFWUpdateThroughTwin(twin, {
        fwPackageUri: fwPackageUriVal,
        status: 'waiting',
        error : null,
        startedWaitingTime : now.toISOString()
      });
      setTimeout(callback, 4000);
    };
    ```

9. adım: güncelleştirmeleri bildirilen özellikleri aracılığıyla bellenim güncelleştirme durumu aşağıdaki işlevi ekleyin **indirme**. Bundan sonra işlev bir üretici yazılımı indirme işlemini taklit eder ve son olarak üretici yazılımı güncelleştirme durumunu **downloadFailed** ya da **downloadComplete** olarak güncelleştirir:
   
    ```
    var downloadImage = function(twin, fwPackageUriVal, callback) {
      var now = new Date();   
   
      reportFWUpdateThroughTwin(twin, {
        status: 'downloading',
      });
   
      setTimeout(function() {
        // Simulate download
        simulateDownloadImage(fwPackageUriVal, function(err, image) {
   
          if (err)
          {
            reportFWUpdateThroughTwin(twin, {
              status: 'downloadfailed',
              error: {
                code: error_code,
                message: error_message,
              }
            });
          }
          else {        
            reportFWUpdateThroughTwin(twin, {
              status: 'downloadComplete',
              downloadCompleteTime: now.toISOString(),
            });
   
            setTimeout(function() { callback(image); }, 4000);   
          }
        });
   
      }, 4000);
    }
    ```

10. adım: güncelleştirmeleri bildirilen özellikleri aracılığıyla bellenim güncelleştirme durumu aşağıdaki işlevi ekleyin **uygulama**. Bundan sonra işlev bir üretici yazılımı görüntüsünü uygulama işlemini taklit eder ve son olarak üretici yazılımı güncelleştirme durumunu **applyFailed** ya da **applyComplete** olarak güncelleştirir:
    
    ```
    var applyImage = function(twin, imageData, callback) {
      var now = new Date();   
    
      reportFWUpdateThroughTwin(twin, {
        status: 'applying',
        startedApplyingImage : now.toISOString()
      });
    
      setTimeout(function() {
    
        // Simulate apply firmware image
        simulateApplyImage(imageData, function(err) {
          if (err) {
            reportFWUpdateThroughTwin(twin, {
              status: 'applyFailed',
              error: {
                code: err.error_code,
                message: err.error_message,
              }
            });
          } else { 
            reportFWUpdateThroughTwin(twin, {
              status: 'applyComplete',
              lastFirmwareUpdate: now.toISOString()
            });    
    
          }
        });
    
        setTimeout(callback, 4000);
    
      }, 4000);
    }
    ```

11. adım: işleme aşağıdaki işlevi ekleyin **firmwareUpdate** doğrudan yöntemi ve başlatır çok aşama bellenim güncelleştirme işleminin:
    
    ```
    var onFirmwareUpdate = function(request, response) {
    
      // Respond the cloud app for the direct method
      response.send(200, 'FirmwareUpdate started', function(err) {
        if (!err) {
          console.error('An error occured when sending a method response:\n' + err.toString());
        } else {
          console.log('Response to method \'' + request.methodName + '\' sent successfully.');
        }
      });
    
      // Get the parameter from the body of the method request
      var fwPackageUri = request.payload.fwPackageUri;
    
      // Obtain the device twin
      client.getTwin(function(err, twin) {
        if (err) {
          console.error('Could not get device twin.');
        } else {
          console.log('Device twin acquired.');
    
          // Start the multi-stage firmware update
          waitToDownload(twin, fwPackageUri, function() {
            downloadImage(twin, fwPackageUri, function(imageData) {
              applyImage(twin, imageData, function() {});    
            });  
          });
    
        }
      });
    }
    ```

12. adım: Son olarak, IOT hub'ınızı bağlayan aşağıdaki kodu ekleyin:
    
    ```
    client.open(function(err) {
      if (err) {
        console.error('Could not connect to IotHub client');
      }  else {
        console.log('Client connected to IoT Hub.  Waiting for firmwareUpdate direct method.');
      }
    
      client.onDeviceMethod('firmwareUpdate', onFirmwareUpdate);
    });
    ```

> [!NOTE]
> Sade ve basit bir anlatım gözetildiği için bu öğretici herhangi bir yeniden deneme ilkesi uygulamaz. Üretim kodunda yeniden deneme ilkelerini (üstel geri alma), önerilen MSDN makalesinde uygulamalıdır [geçici hata işleme](https://msdn.microsoft.com/library/hh675232.aspx).
> 
> 