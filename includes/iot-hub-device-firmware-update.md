## <a name="create-a-simulated-device-app"></a><span data-ttu-id="6afd9-101">Sanal cihaz uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="6afd9-101">Create a simulated device app</span></span>
<span data-ttu-id="6afd9-102">Bu bölümde şunları yapacaksınız:</span><span class="sxs-lookup"><span data-stu-id="6afd9-102">In this section, you:</span></span>

* <span data-ttu-id="6afd9-103">Merhaba bulut tarafından adlı tooa doğrudan yöntemi yanıt bir Node.js konsol uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="6afd9-103">Create a Node.js console app that responds tooa direct method called by hello cloud</span></span>
* <span data-ttu-id="6afd9-104">Sanal bir üretici yazılımı güncelleştirmesini tetikleme</span><span class="sxs-lookup"><span data-stu-id="6afd9-104">Trigger a simulated firmware update</span></span>
* <span data-ttu-id="6afd9-105">Kullanım hello özellikleri tooenable cihaz çifti sorguları tooidentify aygıtlar ve bellenim güncelleştirme en son ne zaman tamamladıkları bildirdi</span><span class="sxs-lookup"><span data-stu-id="6afd9-105">Use hello reported properties tooenable device twin queries tooidentify devices and when they last completed a firmware update</span></span>

<span data-ttu-id="6afd9-106">1. adım: adlı boş bir klasör oluşturun **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="6afd9-106">Step 1: Create an empty folder called **manageddevice**.</span></span>  <span data-ttu-id="6afd9-107">Merhaba, **manageddevice** klasörü, komut, komut isteminde aşağıdaki hello kullanarak bir package.json dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6afd9-107">In hello **manageddevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="6afd9-108">Tüm hello Varsayılanları kabul edin:</span><span class="sxs-lookup"><span data-stu-id="6afd9-108">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```

<span data-ttu-id="6afd9-109">2. adım: İsteminizde komutu hello **manageddevice** klasörüne, komut tooinstall hello aşağıdaki hello **azure IOT cihaz** ve **azure-IOT-cihaz-mqtt** aygıt SDK paketler:</span><span class="sxs-lookup"><span data-stu-id="6afd9-109">Step 2: At your command prompt in hello **manageddevice** folder, run hello following command tooinstall hello **azure-iot-device** and **azure-iot-device-mqtt** Device SDK packages:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

<span data-ttu-id="6afd9-110">3. adım: bir metin düzenleyicisi kullanarak, oluşturduğunuz bir **dmpatterns_fwupdate_device.js** hello dosyasında **manageddevice** klasör.</span><span class="sxs-lookup"><span data-stu-id="6afd9-110">Step 3: Using a text editor, create a **dmpatterns_fwupdate_device.js** file in hello **manageddevice** folder.</span></span>

<span data-ttu-id="6afd9-111">4. adım: hello aşağıdaki 'İste' hello hello başlangıç deyimleri ekleme **dmpatterns_fwupdate_device.js** dosyası:</span><span class="sxs-lookup"><span data-stu-id="6afd9-111">Step 4: Add hello following 'require' statements at hello start of hello **dmpatterns_fwupdate_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
<span data-ttu-id="6afd9-112">5. adım: Ekleme bir **connectionString** değişken ve toocreate kullanan bir **istemci** örneği.</span><span class="sxs-lookup"><span data-stu-id="6afd9-112">Step 5: Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span> <span data-ttu-id="6afd9-113">Hello yerine `{yourdeviceconnectionstring}` hello bağlantı dizesiyle daha önce yaptığınız Not hello "bir cihaz kimliği oluşturma" bölümünde daha önce yer tutucu:</span><span class="sxs-lookup"><span data-stu-id="6afd9-113">Replace hello `{yourdeviceconnectionstring}` placeholder with hello connection string you previously made a note of in hello "Create a device identity" section previously:</span></span>
   
    ```
    var connectionString = '{yourdeviceconnectionstring}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

<span data-ttu-id="6afd9-114">6. adım: hello aşağıdakileri ekleyin kullanılan tooupdate olduğu işlevi bildirilen özellikleri:</span><span class="sxs-lookup"><span data-stu-id="6afd9-114">Step 6: Add hello following function that is used tooupdate reported properties:</span></span>
   
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

<span data-ttu-id="6afd9-115">7. adım: indirme ve hello bellenim yansımayı benzetimini işlevleri aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="6afd9-115">Step 7: Add hello following functions that simulate downloading and applying hello firmware image:</span></span>
   
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

<span data-ttu-id="6afd9-116">8. adım: güncelleştirmeleri hello bellenim güncelleştirme durumu hello aracılığıyla özellikleri çok bildirilen işlevi aşağıdaki hello eklemek**bekleyen**.</span><span class="sxs-lookup"><span data-stu-id="6afd9-116">Step 8: Add hello following function that updates hello firmware update status through hello reported properties too**waiting**.</span></span> <span data-ttu-id="6afd9-117">Genellikle, cihazları saat dilimi ve tarih ilkesi hello aygıt toostart indiriliyor ve hello güncelleştirmeyi uyguladıktan neden olan kullanılabilir bir güncelleştirme ve yöneticinin tanımladığı bildirilir.</span><span class="sxs-lookup"><span data-stu-id="6afd9-117">Typically, devices are informed of an available update and an administrator defined policy causes hello device toostart downloading and applying hello update.</span></span> <span data-ttu-id="6afd9-118">Bu işlev İlkesi çalışması gerektiğini mantığı tooenable burada hello.</span><span class="sxs-lookup"><span data-stu-id="6afd9-118">This function is where hello logic tooenable that policy should run.</span></span> <span data-ttu-id="6afd9-119">Kolaylık olması için devam etmeden toodownload hello bellenim görüntü önce dört saniye hello örnek bekler:</span><span class="sxs-lookup"><span data-stu-id="6afd9-119">For simplicity, hello sample waits for four seconds before proceeding toodownload hello firmware image:</span></span>
   
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

<span data-ttu-id="6afd9-120">9. adım: güncelleştirmeleri hello bellenim güncelleştirme durumu hello aracılığıyla özellikleri çok bildirilen işlevi aşağıdaki hello eklemek**indirme**.</span><span class="sxs-lookup"><span data-stu-id="6afd9-120">Step 9: Add hello following function that updates hello firmware update status through hello reported properties too**downloading**.</span></span> <span data-ttu-id="6afd9-121">Hello işlevi sonra bellenim indirme canlandırır ve son olarak güncelleştirmeleri bellenim güncelleştirme durumu tooeither hello **downloadFailed** veya **downloadComplete**:</span><span class="sxs-lookup"><span data-stu-id="6afd9-121">hello function then simulates a firmware download and finally updates hello firmware update status tooeither **downloadFailed** or **downloadComplete**:</span></span>
   
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

<span data-ttu-id="6afd9-122">10. adım: güncelleştirmeleri hello bellenim güncelleştirme durumu hello aracılığıyla özellikleri çok bildirilen işlevi aşağıdaki hello ekleme**uygulama**.</span><span class="sxs-lookup"><span data-stu-id="6afd9-122">Step 10: Add hello following function that updates hello firmware update status through hello reported properties too**applying**.</span></span> <span data-ttu-id="6afd9-123">Hello işlevi sonra uygulanan hello bellenim görüntü canlandırır ve son olarak güncelleştirmeleri bellenim güncelleştirme durumu tooeither hello **applyFailed** veya **applyComplete**:</span><span class="sxs-lookup"><span data-stu-id="6afd9-123">hello function then simulates applying hello firmware image and finally updates hello firmware update status tooeither **applyFailed** or **applyComplete**:</span></span>
    
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

<span data-ttu-id="6afd9-124">11. adım: hello aşağıdaki işlev bu tanıtıcıları hello ekleme **firmwareUpdate** doğrudan yöntemi ve başlatır hello çok aşama bellenim güncelleştirme işlemi:</span><span class="sxs-lookup"><span data-stu-id="6afd9-124">Step 11: Add hello following function that handles hello **firmwareUpdate** direct method and initiates hello multi-stage firmware update process:</span></span>
    
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

<span data-ttu-id="6afd9-125">12. adım: Son olarak, tooyour IOT hub'a bağlanan koddan hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="6afd9-125">Step 12: Finally, add hello following code that connects tooyour IoT hub:</span></span>
    
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
> <span data-ttu-id="6afd9-126">tookeep şeyler basit, Bu öğretici herhangi bir yeniden deneme ilkesi uygulamaz.</span><span class="sxs-lookup"><span data-stu-id="6afd9-126">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="6afd9-127">Üretim kodunda yeniden deneme ilkelerini (üstel geri alma), önerilen hello MSDN makalesinde uygulamalıdır [geçici hata işleme](https://msdn.microsoft.com/library/hh675232.aspx).</span><span class="sxs-lookup"><span data-stu-id="6afd9-127">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling](https://msdn.microsoft.com/library/hh675232.aspx).</span></span>
> 
> 