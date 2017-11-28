## <a name="configure-the-nodejs-simulated-device"></a><span data-ttu-id="b2e58-101">Node.js sanal cihaz yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b2e58-101">Configure the Node.js simulated device</span></span>
1. <span data-ttu-id="b2e58-102">Uzaktan izleme Panosu üzerinde tıklatın **+ bir cihaz ekleme** ve ardından ekleyin bir *özel cihaz*.</span><span class="sxs-lookup"><span data-stu-id="b2e58-102">On the remote monitoring dashboard, click **+ Add a device** and then add a *custom device*.</span></span> <span data-ttu-id="b2e58-103">IOT Hub ana bilgisayar adı, cihaz kimliği ve cihaz anahtarını Not.</span><span class="sxs-lookup"><span data-stu-id="b2e58-103">Make a note of the IoT Hub hostname, device id, and device key.</span></span> <span data-ttu-id="b2e58-104">Remote_monitoring.js aygıt istemci uygulaması hazırlarken, bunları daha sonra Bu öğreticide gerekir.</span><span class="sxs-lookup"><span data-stu-id="b2e58-104">You need them later in this tutorial when you prepare the remote_monitoring.js device client application.</span></span>
2. <span data-ttu-id="b2e58-105">Bu Node.js sürümünü olun 0.12.x sürümü veya daha sonra dağıtım makinenize yüklü.</span><span class="sxs-lookup"><span data-stu-id="b2e58-105">Ensure that Node.js version 0.12.x or later is installed on your development machine.</span></span> <span data-ttu-id="b2e58-106">Çalıştırma `node --version` bir komut isteminde veya bir kabuk sürümünü denetleyin.</span><span class="sxs-lookup"><span data-stu-id="b2e58-106">Run `node --version` at a command prompt or in a shell to check the version.</span></span> <span data-ttu-id="b2e58-107">Node.js Linux'ta yüklemek için bir paket Yöneticisi'ni kullanma hakkında daha fazla bilgi için bkz: [yükleme Node.js Paket Yöneticisi aracılığıyla][node-linux].</span><span class="sxs-lookup"><span data-stu-id="b2e58-107">For information about using a package manager to install Node.js on Linux, see [Installing Node.js via package manager][node-linux].</span></span>
3. <span data-ttu-id="b2e58-108">Node.js yüklendiğinde en son sürümünü kopyalama [azure IOT sdk düğüm] [ lnk-github-repo] geliştirme makinenizde depoya.</span><span class="sxs-lookup"><span data-stu-id="b2e58-108">When you have installed Node.js, clone the latest version of the [azure-iot-sdk-node][lnk-github-repo] repository to your development machine.</span></span> <span data-ttu-id="b2e58-109">Her zaman kullanmak **ana** en son sürümünü kitaplıklar ve örnekler için dal.</span><span class="sxs-lookup"><span data-stu-id="b2e58-109">Always use the **master** branch for the latest version of the libraries and samples.</span></span>
4. <span data-ttu-id="b2e58-110">Yerel kopyasından [azure IOT sdk düğüm] [ lnk-github-repo] deposu, aşağıdaki iki dosyaların kopyalanacağı düğümü/aygıt/samples klasör boş bir klasörün geliştirme makinenizde:</span><span class="sxs-lookup"><span data-stu-id="b2e58-110">From your local copy of the [azure-iot-sdk-node][lnk-github-repo] repository, copy the following two files from the node/device/samples folder to an empty folder on your development machine:</span></span>
   
   * <span data-ttu-id="b2e58-111">Packages.JSON</span><span class="sxs-lookup"><span data-stu-id="b2e58-111">packages.json</span></span>
   * <span data-ttu-id="b2e58-112">remote_monitoring.js</span><span class="sxs-lookup"><span data-stu-id="b2e58-112">remote_monitoring.js</span></span>
5. <span data-ttu-id="b2e58-113">Remote_monitoring.js dosyasını açın ve aşağıdaki değişken tanımı bakın:</span><span class="sxs-lookup"><span data-stu-id="b2e58-113">Open the remote_monitoring.js file and look for the following variable definition:</span></span>
   
    ```
    var connectionString = "[IoT Hub device connection string]";
    ```
6. <span data-ttu-id="b2e58-114">Değiştir **[IOT Hub cihaz bağlantı dizesi]** cihaz bağlantı dizesine sahip.</span><span class="sxs-lookup"><span data-stu-id="b2e58-114">Replace **[IoT Hub device connection string]** with your device connection string.</span></span> <span data-ttu-id="b2e58-115">IOT Hub ana bilgisayar adı, cihaz kimliği ve 1. adımda not yapılan aygıt anahtarı için değerleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="b2e58-115">Use the values for your IoT Hub hostname, device id, and device key that you made a note of in step 1.</span></span> <span data-ttu-id="b2e58-116">Bir aygıt bağlantı dizesi, aşağıdaki biçime sahiptir:</span><span class="sxs-lookup"><span data-stu-id="b2e58-116">A device connection string has the following format:</span></span>
   
    ```
    HostName={your IoT Hub hostname};DeviceId={your device id};SharedAccessKey={your device key}
    ```
   
    <span data-ttu-id="b2e58-117">IOT Hub ana bilgisayar adına ise **contoso** ve cihaz kimliğinizi **mydevice**, bağlantı dizenizi aşağıdaki kod parçacığını gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="b2e58-117">If your IoT Hub hostname is **contoso** and your device id is **mydevice**, your connection string looks like the following snippet:</span></span>
   
    ```
    var connectionString = "HostName=contoso.azure-devices.net;DeviceId=mydevice;SharedAccessKey=2s ... =="
    ```
7. Dosyayı kaydedin. <span data-ttu-id="b2e58-119">Bir kabuk ya da gerekli paketleri yüklemek ve örnek uygulamayı çalıştırmak için bu dosyaları içeren klasör komut isteminde aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="b2e58-119">Run the following commands in a shell or command prompt in the folder that contains these files to install the necessary packages and then run the sample application:</span></span>
   
    ```
    npm install
    node remote_monitoring.js
    ```

## <a name="observe-dynamic-telemetry-in-action"></a><span data-ttu-id="b2e58-120">Eylem dinamik telemetri inceleyin</span><span class="sxs-lookup"><span data-stu-id="b2e58-120">Observe dynamic telemetry in action</span></span>
<span data-ttu-id="b2e58-121">Pano varolan sanal aygıtlardan sıcaklık ve nem telemetrisi gösterir:</span><span class="sxs-lookup"><span data-stu-id="b2e58-121">The dashboard shows the temperature and humidity telemetry from the existing simulated devices:</span></span>

![Varsayılan Pano][image1]

<span data-ttu-id="b2e58-123">Önceki bölümde çalıştırdığınız Node.js sanal cihaz seçerseniz, sıcaklık ve nem dış sıcaklığı telemetri bakın:</span><span class="sxs-lookup"><span data-stu-id="b2e58-123">If you select the Node.js simulated device you ran in the previous section, you see temperature, humidity, and external temperature telemetry:</span></span>

![Dış sıcaklığı için Pano ekleyin][image2]

<span data-ttu-id="b2e58-125">Uzaktan izleme çözümü otomatik olarak ek dış sıcaklığı telemetri türünü algılar ve Pano grafiği ekler.</span><span class="sxs-lookup"><span data-stu-id="b2e58-125">The remote monitoring solution automatically detects the additional external temperature telemetry type and adds it to the chart on the dashboard.</span></span>

[node-linux]: https://github.com/nodejs/node-v0.x-archive/wiki/Installing-Node.js-via-package-manager
[lnk-github-repo]: https://github.com/Azure/azure-iot-sdk-node
[image1]: media/iot-suite-send-external-temperature/image1.png
[image2]: media/iot-suite-send-external-temperature/image2.png