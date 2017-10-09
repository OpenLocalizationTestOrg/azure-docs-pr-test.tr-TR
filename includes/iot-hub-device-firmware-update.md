## <a name="create-a-simulated-device-app"></a>Sanal cihaz uygulaması oluşturma
Bu bölümde şunları yapacaksınız:

* Merhaba bulut tarafından adlı tooa doğrudan yöntemi yanıt bir Node.js konsol uygulaması oluşturma
* Sanal bir üretici yazılımı güncelleştirmesini tetikleme
* Kullanım hello özellikleri tooenable cihaz çifti sorguları tooidentify aygıtlar ve bellenim güncelleştirme en son ne zaman tamamladıkları bildirdi

1. adım: adlı boş bir klasör oluşturun **manageddevice**.  Merhaba, **manageddevice** klasörü, komut, komut isteminde aşağıdaki hello kullanarak bir package.json dosyası oluşturun. Tüm hello Varsayılanları kabul edin:
   
    ```
    npm init
    ```

2. adım: İsteminizde komutu hello **manageddevice** klasörüne, komut tooinstall hello aşağıdaki hello **azure IOT cihaz** ve **azure-IOT-cihaz-mqtt** aygıt SDK paketler:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

3. adım: bir metin düzenleyicisi kullanarak, oluşturduğunuz bir **dmpatterns_fwupdate_device.js** hello dosyasında **manageddevice** klasör.

4. adım: hello aşağıdaki 'İste' hello hello başlangıç deyimleri ekleme **dmpatterns_fwupdate_device.js** dosyası:
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. adım: Ekleme bir **connectionString** değişken ve toocreate kullanan bir **istemci** örneği. Hello yerine `{yourdeviceconnectionstring}` hello bağlantı dizesiyle daha önce yaptığınız Not hello "bir cihaz kimliği oluşturma" bölümünde daha önce yer tutucu:
   
    ```
    var connectionString = '{yourdeviceconnectionstring}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

6. adım: hello aşağıdakileri ekleyin kullanılan tooupdate olduğu işlevi bildirilen özellikleri:
   
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

7. adım: indirme ve hello bellenim yansımayı benzetimini işlevleri aşağıdaki hello ekleyin:
   
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

8. adım: güncelleştirmeleri hello bellenim güncelleştirme durumu hello aracılığıyla özellikleri çok bildirilen işlevi aşağıdaki hello eklemek**bekleyen**. Genellikle, cihazları saat dilimi ve tarih ilkesi hello aygıt toostart indiriliyor ve hello güncelleştirmeyi uyguladıktan neden olan kullanılabilir bir güncelleştirme ve yöneticinin tanımladığı bildirilir. Bu işlev İlkesi çalışması gerektiğini mantığı tooenable burada hello. Kolaylık olması için devam etmeden toodownload hello bellenim görüntü önce dört saniye hello örnek bekler:
   
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

9. adım: güncelleştirmeleri hello bellenim güncelleştirme durumu hello aracılığıyla özellikleri çok bildirilen işlevi aşağıdaki hello eklemek**indirme**. Hello işlevi sonra bellenim indirme canlandırır ve son olarak güncelleştirmeleri bellenim güncelleştirme durumu tooeither hello **downloadFailed** veya **downloadComplete**:
   
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

10. adım: güncelleştirmeleri hello bellenim güncelleştirme durumu hello aracılığıyla özellikleri çok bildirilen işlevi aşağıdaki hello ekleme**uygulama**. Hello işlevi sonra uygulanan hello bellenim görüntü canlandırır ve son olarak güncelleştirmeleri bellenim güncelleştirme durumu tooeither hello **applyFailed** veya **applyComplete**:
    
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

11. adım: hello aşağıdaki işlev bu tanıtıcıları hello ekleme **firmwareUpdate** doğrudan yöntemi ve başlatır hello çok aşama bellenim güncelleştirme işlemi:
    
    ```
    var onFirmwareUpdate = function(request, response) {
    
      // Respond hello cloud app for hello direct method
      response.send(200, 'FirmwareUpdate started', function(err) {
        if (!err) {
          console.error('An error occured when sending a method response:\n' + err.toString());
        } else {
          console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
        }
      });
    
      // Get hello parameter from hello body of hello method request
      var fwPackageUri = request.payload.fwPackageUri;
    
      // Obtain hello device twin
      client.getTwin(function(err, twin) {
        if (err) {
          console.error('Could not get device twin.');
        } else {
          console.log('Device twin acquired.');
    
          // Start hello multi-stage firmware update
          waitToDownload(twin, fwPackageUri, function() {
            downloadImage(twin, fwPackageUri, function(imageData) {
              applyImage(twin, imageData, function() {});    
            });  
          });
    
        }
      });
    }
    ```

12. adım: Son olarak, tooyour IOT hub'a bağlanan koddan hello ekleyin:
    
    ```
    client.open(function(err) {
      if (err) {
        console.error('Could not connect tooIotHub client');
      }  else {
        console.log('Client connected tooIoT Hub.  Waiting for firmwareUpdate direct method.');
      }
    
      client.onDeviceMethod('firmwareUpdate', onFirmwareUpdate);
    });
    ```

> [!NOTE]
> tookeep şeyler basit, Bu öğretici herhangi bir yeniden deneme ilkesi uygulamaz. Üretim kodunda yeniden deneme ilkelerini (üstel geri alma), önerilen hello MSDN makalesinde uygulamalıdır [geçici hata işleme](https://msdn.microsoft.com/library/hh675232.aspx).
> 
> 