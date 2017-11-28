## <a name="create-a-simulated-device-app"></a><span data-ttu-id="457d3-101">Sanal cihaz uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="457d3-101">Create a simulated device app</span></span>
<span data-ttu-id="457d3-102">Bu bölümde şunları yapacaksınız:</span><span class="sxs-lookup"><span data-stu-id="457d3-102">In this section, you:</span></span>

* <span data-ttu-id="457d3-103">Bulut tarafından çağrılan doğrudan bir yönteme yanıt veren bir Node.js konsol uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="457d3-103">Create a Node.js console app that responds to a direct method called by the cloud</span></span>
* <span data-ttu-id="457d3-104">Sanal bir üretici yazılımı güncelleştirmesini tetikleme</span><span class="sxs-lookup"><span data-stu-id="457d3-104">Trigger a simulated firmware update</span></span>
* <span data-ttu-id="457d3-105">Cihaz ikizi sorgularının cihazları ve bir üretici yazılımı güncelleştirmesini en son ne zaman tamamladığını belirlemesi için rapor edilen özellikleri kullanın</span><span class="sxs-lookup"><span data-stu-id="457d3-105">Use the reported properties to enable device twin queries to identify devices and when they last completed a firmware update</span></span>

<span data-ttu-id="457d3-106">1. adım: adlı boş bir klasör oluşturun **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="457d3-106">Step 1: Create an empty folder called **manageddevice**.</span></span>  <span data-ttu-id="457d3-107">Komut isteminizde aşağıdaki komutu kullanarak **manageddevice** klasöründe bir package.json dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="457d3-107">In the **manageddevice** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="457d3-108">Tüm varsayılanları kabul edin:</span><span class="sxs-lookup"><span data-stu-id="457d3-108">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```

<span data-ttu-id="457d3-109">2. adım: İsteminizde komutu **manageddevice** klasörü yüklemek için aşağıdaki komutu çalıştırın, **azure IOT cihaz** ve **azure-IOT-cihaz-mqtt** cihaz SDK'sı paketler:</span><span class="sxs-lookup"><span data-stu-id="457d3-109">Step 2: At your command prompt in the **manageddevice** folder, run the following command to install the **azure-iot-device** and **azure-iot-device-mqtt** Device SDK packages:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

<span data-ttu-id="457d3-110">3. adım: bir metin düzenleyicisi kullanarak, oluşturduğunuz bir **dmpatterns_fwupdate_device.js** dosyasını **manageddevice** klasör.</span><span class="sxs-lookup"><span data-stu-id="457d3-110">Step 3: Using a text editor, create a **dmpatterns_fwupdate_device.js** file in the **manageddevice** folder.</span></span>

<span data-ttu-id="457d3-111">4. adım: aşağıdaki 'İste' deyimleri başlangıcında ekleme **dmpatterns_fwupdate_device.js** dosyası:</span><span class="sxs-lookup"><span data-stu-id="457d3-111">Step 4: Add the following 'require' statements at the start of the **dmpatterns_fwupdate_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
<span data-ttu-id="457d3-112">5. adım: Ekleme bir **connectionString** değişkeni ve oluşturmak için kullanın bir **istemci** örneği.</span><span class="sxs-lookup"><span data-stu-id="457d3-112">Step 5: Add a **connectionString** variable and use it to create a **Client** instance.</span></span> <span data-ttu-id="457d3-113">`{yourdeviceconnectionstring}` yer tutucusunu, daha önce "Cihaz kimliği oluşturma" bölümünde not aldığınız bağlantı dizesiyle değiştirin:</span><span class="sxs-lookup"><span data-stu-id="457d3-113">Replace the `{yourdeviceconnectionstring}` placeholder with the connection string you previously made a note of in the "Create a device identity" section previously:</span></span>
   
    ```
    var connectionString = '{yourdeviceconnectionstring}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

<span data-ttu-id="457d3-114">6. adım: bildirilen özelliklerini güncelleştirmek için kullanılan aşağıdaki işlevi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="457d3-114">Step 6: Add the following function that is used to update reported properties:</span></span>
   
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

<span data-ttu-id="457d3-115">7. adım: indirme ve bellenim yansımayı benzetimini aşağıdaki işlevi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="457d3-115">Step 7: Add the following functions that simulate downloading and applying the firmware image:</span></span>
   
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

<span data-ttu-id="457d3-116">8. adım: güncelleştirmeleri bildirilen özellikleri aracılığıyla bellenim güncelleştirme durumu aşağıdaki işlevi ekleyin **bekleyen**.</span><span class="sxs-lookup"><span data-stu-id="457d3-116">Step 8: Add the following function that updates the firmware update status through the reported properties to **waiting**.</span></span> <span data-ttu-id="457d3-117">Genellikle, cihazlar kullanılabilir güncelleştirmeden haberdar edilir ve yönetici tarafından tanımlanan bir ilke, cihazın güncelleştirmeyi indirip uygulamaya başlamasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="457d3-117">Typically, devices are informed of an available update and an administrator defined policy causes the device to start downloading and applying the update.</span></span> <span data-ttu-id="457d3-118">Bu işlev, ilgili ilkeyi etkinleştirme mantığının çalışması gereken yerdir.</span><span class="sxs-lookup"><span data-stu-id="457d3-118">This function is where the logic to enable that policy should run.</span></span> <span data-ttu-id="457d3-119">Kolaylık olması için örnek dört bellenim görüntüsünü karşıdan yüklemek için saniye devam etmeden önce bekler:</span><span class="sxs-lookup"><span data-stu-id="457d3-119">For simplicity, the sample waits for four seconds before proceeding to download the firmware image:</span></span>
   
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

<span data-ttu-id="457d3-120">9. adım: güncelleştirmeleri bildirilen özellikleri aracılığıyla bellenim güncelleştirme durumu aşağıdaki işlevi ekleyin **indirme**.</span><span class="sxs-lookup"><span data-stu-id="457d3-120">Step 9: Add the following function that updates the firmware update status through the reported properties to **downloading**.</span></span> <span data-ttu-id="457d3-121">Bundan sonra işlev bir üretici yazılımı indirme işlemini taklit eder ve son olarak üretici yazılımı güncelleştirme durumunu **downloadFailed** ya da **downloadComplete** olarak güncelleştirir:</span><span class="sxs-lookup"><span data-stu-id="457d3-121">The function then simulates a firmware download and finally updates the firmware update status to either **downloadFailed** or **downloadComplete**:</span></span>
   
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

<span data-ttu-id="457d3-122">10. adım: güncelleştirmeleri bildirilen özellikleri aracılığıyla bellenim güncelleştirme durumu aşağıdaki işlevi ekleyin **uygulama**.</span><span class="sxs-lookup"><span data-stu-id="457d3-122">Step 10: Add the following function that updates the firmware update status through the reported properties to **applying**.</span></span> <span data-ttu-id="457d3-123">Bundan sonra işlev bir üretici yazılımı görüntüsünü uygulama işlemini taklit eder ve son olarak üretici yazılımı güncelleştirme durumunu **applyFailed** ya da **applyComplete** olarak güncelleştirir:</span><span class="sxs-lookup"><span data-stu-id="457d3-123">The function then simulates applying the firmware image and finally updates the firmware update status to either **applyFailed** or **applyComplete**:</span></span>
    
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

<span data-ttu-id="457d3-124">11. adım: işleme aşağıdaki işlevi ekleyin **firmwareUpdate** doğrudan yöntemi ve başlatır çok aşama bellenim güncelleştirme işleminin:</span><span class="sxs-lookup"><span data-stu-id="457d3-124">Step 11: Add the following function that handles the **firmwareUpdate** direct method and initiates the multi-stage firmware update process:</span></span>
    
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

<span data-ttu-id="457d3-125">12. adım: Son olarak, IOT hub'ınızı bağlayan aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="457d3-125">Step 12: Finally, add the following code that connects to your IoT hub:</span></span>
    
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
> <span data-ttu-id="457d3-126">Sade ve basit bir anlatım gözetildiği için bu öğretici herhangi bir yeniden deneme ilkesi uygulamaz.</span><span class="sxs-lookup"><span data-stu-id="457d3-126">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="457d3-127">Üretim kodunda yeniden deneme ilkelerini (üstel geri alma), önerilen MSDN makalesinde uygulamalıdır [geçici hata işleme](https://msdn.microsoft.com/library/hh675232.aspx).</span><span class="sxs-lookup"><span data-stu-id="457d3-127">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling](https://msdn.microsoft.com/library/hh675232.aspx).</span></span>
> 
> 