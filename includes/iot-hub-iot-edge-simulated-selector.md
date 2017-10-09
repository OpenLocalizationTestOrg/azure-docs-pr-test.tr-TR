> [!div class="op_single_selector"]
> * [<span data-ttu-id="3ce51-101">Linux</span><span class="sxs-lookup"><span data-stu-id="3ce51-101">Linux</span></span>](../articles/iot-hub/iot-hub-linux-iot-edge-simulated-device.md)
> * [<span data-ttu-id="3ce51-102">Windows</span><span class="sxs-lookup"><span data-stu-id="3ce51-102">Windows</span></span>](../articles/iot-hub/iot-hub-windows-iot-edge-simulated-device.md)

<span data-ttu-id="3ce51-103">Bu kılavuz hello [sanal cihaz bulut karşıya örnek] nasıl gösterir toouse [Azure IOT kenar] [ lnk-sdk] benzetimli gelen toosend cihaz bulut telemetri tooIoT Hub cihazlar.</span><span class="sxs-lookup"><span data-stu-id="3ce51-103">This walkthrough of hello [Simulated Device Cloud Upload sample] shows you how toouse [Azure IoT Edge][lnk-sdk] toosend device-to-cloud telemetry tooIoT Hub from simulated devices.</span></span>

<span data-ttu-id="3ce51-104">Bu kılavuzda aşağıdaki konular ele alınmaktadır:</span><span class="sxs-lookup"><span data-stu-id="3ce51-104">This walkthrough covers:</span></span>

* <span data-ttu-id="3ce51-105">**Mimari**: hello mimari bilgilerini [sanal cihaz bulut karşıya örnek].</span><span class="sxs-lookup"><span data-stu-id="3ce51-105">**Architecture**: architectural information about hello [Simulated Device Cloud Upload sample].</span></span>
* <span data-ttu-id="3ce51-106">**Derleme ve çalıştırma**: hello adımları gerekli toobuild ve çalışma hello örnek.</span><span class="sxs-lookup"><span data-stu-id="3ce51-106">**Build and run**: hello steps required toobuild and run hello sample.</span></span>

## <a name="architecture"></a><span data-ttu-id="3ce51-107">Mimari</span><span class="sxs-lookup"><span data-stu-id="3ce51-107">Architecture</span></span>

<span data-ttu-id="3ce51-108">Merhaba [sanal cihaz bulut karşıya örnek] toocreate telemetri gönderen bir ağ geçidi aygıtları tooan IOT hub'ı nasıl benzetimli gösterir.</span><span class="sxs-lookup"><span data-stu-id="3ce51-108">hello [Simulated Device Cloud Upload sample] shows how toocreate a gateway that sends telemetry from simulated devices tooan IoT hub.</span></span> <span data-ttu-id="3ce51-109">Bir aygıt mümkün tooconnect olmayabilir doğrudan tooIoT Hub çünkü hello cihaz:</span><span class="sxs-lookup"><span data-stu-id="3ce51-109">A device may not be able tooconnect directly tooIoT Hub because hello device:</span></span>

* <span data-ttu-id="3ce51-110">IOT Hub tarafından anlaşılan bir iletişim protokolü kullanmaz.</span><span class="sxs-lookup"><span data-stu-id="3ce51-110">Does not use a communications protocol understood by IoT Hub.</span></span>
* <span data-ttu-id="3ce51-111">IOT Hub tarafından yeterince akıllı tooremember hello atanan kimlik tooit değil.</span><span class="sxs-lookup"><span data-stu-id="3ce51-111">Is not smart enough tooremember hello identity assigned tooit by IoT Hub.</span></span>

<span data-ttu-id="3ce51-112">Bir IOT sınır ağ geçidi yolları aşağıdaki hello'de bu sorunları çözebilir:</span><span class="sxs-lookup"><span data-stu-id="3ce51-112">An IoT Edge gateway can solve these problems in hello following ways:</span></span>

* <span data-ttu-id="3ce51-113">Merhaba ağ geçidi hello aygıt tarafından kullanılan hello Protokolü anlayan, cihaz bulut telemetri hello aygıttan alır ve bu iletileri tooIoT hello IOT hub tarafından anlaşılan protokolünü kullanarak Hub iletir.</span><span class="sxs-lookup"><span data-stu-id="3ce51-113">hello gateway understands hello protocol used by hello device, receives device-to-cloud telemetry from hello device, and forwards those messages tooIoT Hub using a protocol understood by hello IoT hub.</span></span>

* <span data-ttu-id="3ce51-114">Merhaba ağ geçidi IOT hub'ı kimlikleri toodevices eşler ve bir cihaz iletileri tooIoT Hub gönderdiğinde bir proxy gibi davranır.</span><span class="sxs-lookup"><span data-stu-id="3ce51-114">hello gateway maps IoT Hub identities toodevices and acts as a proxy when a device sends messages tooIoT Hub.</span></span>

<span data-ttu-id="3ce51-115">Aşağıdaki diyagramda hello hello örnek ana bileşenlerinin Merhaba, hello IOT kenar modüller de dahil olmak üzere gösterir:</span><span class="sxs-lookup"><span data-stu-id="3ce51-115">hello following diagram shows hello main components of hello sample, including hello IoT Edge modules:</span></span>

![][1]

<span data-ttu-id="3ce51-116">Merhaba modülleri iletileri geçirmek değil doğrudan tooeach diğer.</span><span class="sxs-lookup"><span data-stu-id="3ce51-116">hello modules do not pass messages directly tooeach other.</span></span> <span data-ttu-id="3ce51-117">Merhaba modülleri hello iletileri toohello abonelik mekanizmasını kullanarak diğer modüller sunar iletileri tooan iç Aracısı yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="3ce51-117">hello modules publish messages tooan internal broker that delivers hello messages toohello other modules using a subscription mechanism.</span></span> <span data-ttu-id="3ce51-118">Daha fazla bilgi için bkz: [Azure IOT Edge ile çalışmaya başlama][lnk-gw-getstarted].</span><span class="sxs-lookup"><span data-stu-id="3ce51-118">For more information, see [Get started with Azure IoT Edge][lnk-gw-getstarted].</span></span>

### <a name="protocol-ingestion-module"></a><span data-ttu-id="3ce51-119">Protokol alım modülü</span><span class="sxs-lookup"><span data-stu-id="3ce51-119">Protocol ingestion module</span></span>

<span data-ttu-id="3ce51-120">Bu modül için alıcı veri aygıtlardan hello ağ geçidi üzerinden ve hello buluta başlangıç noktası hello ' dir.</span><span class="sxs-lookup"><span data-stu-id="3ce51-120">This module is hello starting point for receiving data from devices, through hello gateway, and into hello cloud.</span></span> <span data-ttu-id="3ce51-121">Merhaba örnek hello Modülü:</span><span class="sxs-lookup"><span data-stu-id="3ce51-121">In hello sample, hello module:</span></span>

1. <span data-ttu-id="3ce51-122">Benzetimli sıcaklık veri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3ce51-122">Creates simulated temperature data.</span></span> <span data-ttu-id="3ce51-123">Fiziksel aygıtların kullanırsanız, hello modülü fiziksel aygıtların verileri okur.</span><span class="sxs-lookup"><span data-stu-id="3ce51-123">If you use physical devices, hello module reads data from those physical devices.</span></span>
1. <span data-ttu-id="3ce51-124">Bir ileti oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3ce51-124">Creates a message.</span></span>
1. <span data-ttu-id="3ce51-125">Merhaba benzetimli sıcaklık verileri hello ileti içeriği yerleştirir.</span><span class="sxs-lookup"><span data-stu-id="3ce51-125">Places hello simulated temperature data into hello message content.</span></span>
1. <span data-ttu-id="3ce51-126">Sahte bir MAC adresi toohello iletisiyle bir özellik ekler.</span><span class="sxs-lookup"><span data-stu-id="3ce51-126">Adds a property with a fake MAC address toohello message.</span></span>
1. <span data-ttu-id="3ce51-127">Merhaba ileti kullanılabilir toohello sonraki modüle hello zincirinde yapar.</span><span class="sxs-lookup"><span data-stu-id="3ce51-127">Makes hello message available toohello next module in hello chain.</span></span>

<span data-ttu-id="3ce51-128">adlı hello Modülü **Protokolü X alım** hello önceki diyagramda adlı **sanal cihaz** hello kaynak kodunda.</span><span class="sxs-lookup"><span data-stu-id="3ce51-128">hello module called **Protocol X ingestion** in hello previous diagram is called **Simulated device** in hello source code.</span></span>

### <a name="mac-lt-gt-iot-hub-id-module"></a><span data-ttu-id="3ce51-129">MAC &lt;-&gt; IoT Hub kimlik modülü</span><span class="sxs-lookup"><span data-stu-id="3ce51-129">MAC &lt;-&gt; IoT Hub ID module</span></span>

<span data-ttu-id="3ce51-130">Bu modül için bir Mac adresi özelliğine sahip iletileri tarar.</span><span class="sxs-lookup"><span data-stu-id="3ce51-130">This module scans for messages that have a Mac address property.</span></span> <span data-ttu-id="3ce51-131">Hello örnek hello Protokolü alım modülü hello MAC adres özelliği ekler.</span><span class="sxs-lookup"><span data-stu-id="3ce51-131">In hello sample, hello protocol ingestion module adds hello MAC address property.</span></span> <span data-ttu-id="3ce51-132">Merhaba modülü böyle bir özellik bulursa, bir IOT Hub cihaz anahtar toohello iletisi içeren başka bir özellik ekler.</span><span class="sxs-lookup"><span data-stu-id="3ce51-132">If hello module finds such a property, it adds another property with an IoT Hub device key toohello message.</span></span> <span data-ttu-id="3ce51-133">Merhaba modülü hello zincirinde sonra hello ileti kullanılabilir toohello sonraki modüle hale getirir.</span><span class="sxs-lookup"><span data-stu-id="3ce51-133">hello module then makes hello message available toohello next module in hello chain.</span></span>

<span data-ttu-id="3ce51-134">MAC adreslerinin ve IOT hub'ı kimlikleri tooassociate benzetimli hello IOT Hub cihaz kimliklerini aygıtlarla arasında bir eşleme Hello Geliştirici ayarlar.</span><span class="sxs-lookup"><span data-stu-id="3ce51-134">hello developer sets up a mapping between MAC addresses and IoT Hub identities tooassociate hello simulated devices with IoT Hub device identities.</span></span> <span data-ttu-id="3ce51-135">Merhaba Geliştirici hello eşleme hello modülü yapılandırmasının bir parçası el ile ekler.</span><span class="sxs-lookup"><span data-stu-id="3ce51-135">hello developer adds hello mapping manually as part of hello module configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="3ce51-136">Bu örnekte benzersiz cihaz tanımlayıcısı olarak bir MAC adresi kullanılır ve bir IoT Hub cihaz kimliğiyle ilişkilendirilir.</span><span class="sxs-lookup"><span data-stu-id="3ce51-136">This sample uses a MAC address as a unique device identifier and correlates it with an IoT Hub device identity.</span></span> <span data-ttu-id="3ce51-137">Bununla birlikte, farklı bir benzersiz tanımlayıcı kullanan kendi modülünüzü yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3ce51-137">However, you can write your own module that uses a different unique identifier.</span></span> <span data-ttu-id="3ce51-138">Örneğin, aygıtlarınızı benzersiz seri numarasına sahip veya bir benzersiz katıştırılmış cihaz adı hello telemetri verileri içerebilir.</span><span class="sxs-lookup"><span data-stu-id="3ce51-138">For example, your devices may have unique serial numbers or hello telemetry data may include a unique embedded device name.</span></span>

### <a name="iot-hub-communication-module"></a><span data-ttu-id="3ce51-139">IoT Hub iletişim modülü</span><span class="sxs-lookup"><span data-stu-id="3ce51-139">IoT Hub communication module</span></span>

<span data-ttu-id="3ce51-140">Bu modül iletileri bir IOT Hub ile Merhaba önceki modülü tarafından atanan aygıt anahtar özelliği alır.</span><span class="sxs-lookup"><span data-stu-id="3ce51-140">This module takes messages with an IoT Hub device key property that was assigned by hello previous module.</span></span> <span data-ttu-id="3ce51-141">Merhaba modülü içerik tooIoT hub'ı kullanarak HTTP protokolü hello hello iletisi gönderir.</span><span class="sxs-lookup"><span data-stu-id="3ce51-141">hello module sends hello message content tooIoT Hub using hello HTTP protocol.</span></span> <span data-ttu-id="3ce51-142">HTTP IOT Hub tarafından anlaşılan üç protokolden Merhaba biridir.</span><span class="sxs-lookup"><span data-stu-id="3ce51-142">HTTP is one of hello three protocols understood by IoT Hub.</span></span>

<span data-ttu-id="3ce51-143">Her sanal cihaz için bir bağlantı açarak yerine bu modül hello ağ geçidi toohello IOT hub'ından HTTP tek bir bağlantı açar.</span><span class="sxs-lookup"><span data-stu-id="3ce51-143">Instead of opening a connection for each simulated device, this module opens a single HTTP connection from hello gateway toohello IoT hub.</span></span> <span data-ttu-id="3ce51-144">Merhaba modülü tüm benzetimli hello cihazlar gelen bağlantıları Bu bağlantı üzerinden sonra multiplexes.</span><span class="sxs-lookup"><span data-stu-id="3ce51-144">hello module then multiplexes connections from all hello simulated devices over that connection.</span></span> <span data-ttu-id="3ce51-145">Bu yaklaşım, tek bir ağ geçidi tooconnect pek çok daha fazla aygıtları sağlar.</span><span class="sxs-lookup"><span data-stu-id="3ce51-145">This approach enables a single gateway tooconnect many more devices.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="3ce51-146">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="3ce51-146">Before you get started</span></span>

<span data-ttu-id="3ce51-147">Başlamadan önce şunları yapmalısınız:</span><span class="sxs-lookup"><span data-stu-id="3ce51-147">Before you get started, you must:</span></span>

* <span data-ttu-id="3ce51-148">[IOT hub oluşturma] [ lnk-create-hub] Azure aboneliğinizde bu kılavuzda, hub toocomplete hello adı gerekir.</span><span class="sxs-lookup"><span data-stu-id="3ce51-148">[Create an IoT hub][lnk-create-hub] in your Azure subscription, you need hello name of your hub toocomplete this walkthrough.</span></span> <span data-ttu-id="3ce51-149">Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3ce51-149">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="3ce51-150">İki aygıtları tooyour IOT hub'ı ekleyin ve kendi kimlikleri ve cihaz anahtarlarını not edin.</span><span class="sxs-lookup"><span data-stu-id="3ce51-150">Add two devices tooyour IoT hub and make a note of their ids and device keys.</span></span> <span data-ttu-id="3ce51-151">Merhaba kullanabilirsiniz [aygıt explorer] [ lnk-device-explorer] veya [iothub-explorer] [ lnk-iothub-explorer] tooadd hello oluşturduğunuz aygıtları toohello IOT hub'ınızı aracı Önceki adım ve kendi anahtarları alır.</span><span class="sxs-lookup"><span data-stu-id="3ce51-151">You can use hello [device explorer][lnk-device-explorer] or [iothub-explorer][lnk-iothub-explorer] tool tooadd your devices toohello IoT hub you created in hello previous step and retrieve their keys.</span></span>

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