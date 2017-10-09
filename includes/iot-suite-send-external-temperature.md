## <a name="configure-hello-nodejs-simulated-device"></a><span data-ttu-id="7e4ba-101">Merhaba Node.js sanal cihaz yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7e4ba-101">Configure hello Node.js simulated device</span></span>
1. <span data-ttu-id="7e4ba-102">Merhaba Uzaktan izleme panosunda tıklatın **+ bir cihaz ekleme** ve ardından ekleyin bir *özel cihaz*.</span><span class="sxs-lookup"><span data-stu-id="7e4ba-102">On hello remote monitoring dashboard, click **+ Add a device** and then add a *custom device*.</span></span> <span data-ttu-id="7e4ba-103">Merhaba IOT Hub ana bilgisayar adı, cihaz kimliği ve cihaz anahtarını Not.</span><span class="sxs-lookup"><span data-stu-id="7e4ba-103">Make a note of hello IoT Hub hostname, device id, and device key.</span></span> <span data-ttu-id="7e4ba-104">Merhaba remote_monitoring.js aygıt istemci uygulaması hazırlarken, bunları daha sonra Bu öğreticide gerekir.</span><span class="sxs-lookup"><span data-stu-id="7e4ba-104">You need them later in this tutorial when you prepare hello remote_monitoring.js device client application.</span></span>
2. <span data-ttu-id="7e4ba-105">Bu Node.js sürümünü olun 0.12.x sürümü veya daha sonra dağıtım makinenize yüklü.</span><span class="sxs-lookup"><span data-stu-id="7e4ba-105">Ensure that Node.js version 0.12.x or later is installed on your development machine.</span></span> <span data-ttu-id="7e4ba-106">Çalıştırma `node --version` bir komut isteminde veya bir kabuk toocheck hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="7e4ba-106">Run `node --version` at a command prompt or in a shell toocheck hello version.</span></span> <span data-ttu-id="7e4ba-107">Linux üzerinde bir paket Yöneticisi tooinstall Node.js kullanma hakkında daha fazla bilgi için bkz: [yükleme Node.js Paket Yöneticisi aracılığıyla][node-linux].</span><span class="sxs-lookup"><span data-stu-id="7e4ba-107">For information about using a package manager tooinstall Node.js on Linux, see [Installing Node.js via package manager][node-linux].</span></span>
3. <span data-ttu-id="7e4ba-108">Node.js yüklendiğinde hello en son sürümünü hello kopyalama [azure IOT sdk düğüm] [ lnk-github-repo] depo tooyour geliştirme makine.</span><span class="sxs-lookup"><span data-stu-id="7e4ba-108">When you have installed Node.js, clone hello latest version of hello [azure-iot-sdk-node][lnk-github-repo] repository tooyour development machine.</span></span> <span data-ttu-id="7e4ba-109">Her zaman hello kullan **ana** hello en son sürümünü hello kitaplıklar ve örnekler için dal.</span><span class="sxs-lookup"><span data-stu-id="7e4ba-109">Always use hello **master** branch for hello latest version of hello libraries and samples.</span></span>
4. <span data-ttu-id="7e4ba-110">Merhaba yerel kopyasından [azure IOT sdk düğüm] [ lnk-github-repo] deposu, geliştirme makinenizde hello düğümü/aygıt/samples klasörü tooan boş klasöründen aşağıdaki iki dosyaları kopyalama hello:</span><span class="sxs-lookup"><span data-stu-id="7e4ba-110">From your local copy of hello [azure-iot-sdk-node][lnk-github-repo] repository, copy hello following two files from hello node/device/samples folder tooan empty folder on your development machine:</span></span>
   
   * <span data-ttu-id="7e4ba-111">Packages.JSON</span><span class="sxs-lookup"><span data-stu-id="7e4ba-111">packages.json</span></span>
   * <span data-ttu-id="7e4ba-112">remote_monitoring.js</span><span class="sxs-lookup"><span data-stu-id="7e4ba-112">remote_monitoring.js</span></span>
5. <span data-ttu-id="7e4ba-113">Merhaba remote_monitoring.js dosyasını açın ve değişken tanımını izleyen Merhaba bakın:</span><span class="sxs-lookup"><span data-stu-id="7e4ba-113">Open hello remote_monitoring.js file and look for hello following variable definition:</span></span>
   
    ```
    var connectionString = "[IoT Hub device connection string]";
    ```
6. <span data-ttu-id="7e4ba-114">Değiştir **[IOT Hub cihaz bağlantı dizesi]** cihaz bağlantı dizesine sahip.</span><span class="sxs-lookup"><span data-stu-id="7e4ba-114">Replace **[IoT Hub device connection string]** with your device connection string.</span></span> <span data-ttu-id="7e4ba-115">IOT Hub ana bilgisayar adı, cihaz kimliği ve 1. adımda not yapılan aygıt anahtarı için başlangıç değerlerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="7e4ba-115">Use hello values for your IoT Hub hostname, device id, and device key that you made a note of in step 1.</span></span> <span data-ttu-id="7e4ba-116">Bir aygıt bağlantı dizesi biçimi aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="7e4ba-116">A device connection string has hello following format:</span></span>
   
    ```
    HostName={your IoT Hub hostname};DeviceId={your device id};SharedAccessKey={your device key}
    ```
   
    <span data-ttu-id="7e4ba-117">IOT Hub ana bilgisayar adına ise **contoso** ve cihaz kimliğinizi **mydevice**, bağlantı dizenizi hello parçacığını aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="7e4ba-117">If your IoT Hub hostname is **contoso** and your device id is **mydevice**, your connection string looks like hello following snippet:</span></span>
   
    ```
    var connectionString = "HostName=contoso.azure-devices.net;DeviceId=mydevice;SharedAccessKey=2s ... =="
    ```
7. Merhaba dosyasını kaydedin. <span data-ttu-id="7e4ba-119">Aşağıdaki komutlar bir kabuk ya da komut istemi kullanarak bu dosyaları tooinstall hello gerekli paketleri içeren hello klasördeki hello çalıştırın ve hello örnek uygulamayı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="7e4ba-119">Run hello following commands in a shell or command prompt in hello folder that contains these files tooinstall hello necessary packages and then run hello sample application:</span></span>
   
    ```
    npm install
    node remote_monitoring.js
    ```

## <a name="observe-dynamic-telemetry-in-action"></a><span data-ttu-id="7e4ba-120">Eylem dinamik telemetri inceleyin</span><span class="sxs-lookup"><span data-stu-id="7e4ba-120">Observe dynamic telemetry in action</span></span>
<span data-ttu-id="7e4ba-121">Başlangıç Panosu hello sıcaklık ve nem telemetrisinden hello varolan sanal cihazlar gösterir:</span><span class="sxs-lookup"><span data-stu-id="7e4ba-121">hello dashboard shows hello temperature and humidity telemetry from hello existing simulated devices:</span></span>

![Merhaba varsayılan pano][image1]

<span data-ttu-id="7e4ba-123">Merhaba Node.js sanal cihaz hello önceki bölümde çalıştırdığınız seçerseniz, sıcaklık ve nem dış sıcaklığı telemetri bakın:</span><span class="sxs-lookup"><span data-stu-id="7e4ba-123">If you select hello Node.js simulated device you ran in hello previous section, you see temperature, humidity, and external temperature telemetry:</span></span>

![Dış sıcaklığı toohello Pano Ekle][image2]

<span data-ttu-id="7e4ba-125">Merhaba Uzaktan izleme çözümü otomatik olarak hello ek dış sıcaklığı telemetri türünü algılar ve hello Panoda toohello grafik ekler.</span><span class="sxs-lookup"><span data-stu-id="7e4ba-125">hello remote monitoring solution automatically detects hello additional external temperature telemetry type and adds it toohello chart on hello dashboard.</span></span>

[node-linux]: https://github.com/nodejs/node-v0.x-archive/wiki/Installing-Node.js-via-package-manager
[lnk-github-repo]: https://github.com/Azure/azure-iot-sdk-node
[image1]: media/iot-suite-send-external-temperature/image1.png
[image2]: media/iot-suite-send-external-temperature/image2.png