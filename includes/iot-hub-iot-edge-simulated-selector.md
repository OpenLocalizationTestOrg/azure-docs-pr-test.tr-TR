> [!div class="op_single_selector"]
> * [<span data-ttu-id="55e71-101">Linux</span><span class="sxs-lookup"><span data-stu-id="55e71-101">Linux</span></span>](../articles/iot-hub/iot-hub-linux-iot-edge-simulated-device.md)
> * [<span data-ttu-id="55e71-102">Windows</span><span class="sxs-lookup"><span data-stu-id="55e71-102">Windows</span></span>](../articles/iot-hub/iot-hub-windows-iot-edge-simulated-device.md)

<span data-ttu-id="55e71-103">Bu kılavuz [sanal cihaz bulut karşıya örnek] nasıl kullanılacağını gösterir [Azure IOT kenar] [ lnk-sdk] sanal cihazlar IOT Hub'ına cihaz bulut telemetri göndermek için .</span><span class="sxs-lookup"><span data-stu-id="55e71-103">This walkthrough of the [Simulated Device Cloud Upload sample] shows you how to use [Azure IoT Edge][lnk-sdk] to send device-to-cloud telemetry to IoT Hub from simulated devices.</span></span>

<span data-ttu-id="55e71-104">Bu kılavuzda aşağıdaki konular ele alınmaktadır:</span><span class="sxs-lookup"><span data-stu-id="55e71-104">This walkthrough covers:</span></span>

* <span data-ttu-id="55e71-105">**Mimari**: Mimari bilgilerini [sanal cihaz bulut karşıya örnek].</span><span class="sxs-lookup"><span data-stu-id="55e71-105">**Architecture**: architectural information about the [Simulated Device Cloud Upload sample].</span></span>
* <span data-ttu-id="55e71-106">**Derleme ve çalıştırma**: örneği derlemek ve çalıştırmak için gerekli adımlar.</span><span class="sxs-lookup"><span data-stu-id="55e71-106">**Build and run**: the steps required to build and run the sample.</span></span>

## <a name="architecture"></a><span data-ttu-id="55e71-107">Mimari</span><span class="sxs-lookup"><span data-stu-id="55e71-107">Architecture</span></span>

<span data-ttu-id="55e71-108">[sanal cihaz bulut karşıya örnek] telemetri benzetimli aygıtlardan bir IOT hub'ına gönderir. bir ağ geçidi oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="55e71-108">The [Simulated Device Cloud Upload sample] shows how to create a gateway that sends telemetry from simulated devices to an IoT hub.</span></span> <span data-ttu-id="55e71-109">Bir aygıt için doğrudan IOT Hub'ına bağlanmak mümkün olmayabilir cihaz:</span><span class="sxs-lookup"><span data-stu-id="55e71-109">A device may not be able to connect directly to IoT Hub because the device:</span></span>

* <span data-ttu-id="55e71-110">IOT Hub tarafından anlaşılan bir iletişim protokolü kullanmaz.</span><span class="sxs-lookup"><span data-stu-id="55e71-110">Does not use a communications protocol understood by IoT Hub.</span></span>
* <span data-ttu-id="55e71-111">IOT Hub tarafından atanmış kimlik anımsaması akıllı değil.</span><span class="sxs-lookup"><span data-stu-id="55e71-111">Is not smart enough to remember the identity assigned to it by IoT Hub.</span></span>

<span data-ttu-id="55e71-112">Bir IOT sınır ağ geçidi aşağıdaki yollarla bu sorunları çözebilir:</span><span class="sxs-lookup"><span data-stu-id="55e71-112">An IoT Edge gateway can solve these problems in the following ways:</span></span>

* <span data-ttu-id="55e71-113">Ağ Geçidi aygıt tarafından kullanılan protokol CİHAZDAN cihaz bulut telemetri alır ve IOT hub'ın IOT hub tarafından anlaşılan protokolünü kullanarak bu iletileri iletir bilir.</span><span class="sxs-lookup"><span data-stu-id="55e71-113">The gateway understands the protocol used by the device, receives device-to-cloud telemetry from the device, and forwards those messages to IoT Hub using a protocol understood by the IoT hub.</span></span>

* <span data-ttu-id="55e71-114">Ağ geçidi aygıtına IOT hub'ı kimlikleri eşler ve bir cihaz IOT Hub'ına iletileri gönderdiğinde bir proxy gibi davranır.</span><span class="sxs-lookup"><span data-stu-id="55e71-114">The gateway maps IoT Hub identities to devices and acts as a proxy when a device sends messages to IoT Hub.</span></span>

<span data-ttu-id="55e71-115">Aşağıdaki diyagramda IOT kenar modüller de dahil olmak üzere örnek ana bileşenlerini gösterir:</span><span class="sxs-lookup"><span data-stu-id="55e71-115">The following diagram shows the main components of the sample, including the IoT Edge modules:</span></span>

![][1]

<span data-ttu-id="55e71-116">Modüller iletileri doğrudan birbirine geçirmez.</span><span class="sxs-lookup"><span data-stu-id="55e71-116">The modules do not pass messages directly to each other.</span></span> <span data-ttu-id="55e71-117">Modülleri iletilerini bir abonelik mekanizması kullanarak diğer modüller ve iletileri teslim bir iç aracısı için yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="55e71-117">The modules publish messages to an internal broker that delivers the messages to the other modules using a subscription mechanism.</span></span> <span data-ttu-id="55e71-118">Daha fazla bilgi için bkz: [Azure IOT Edge ile çalışmaya başlama][lnk-gw-getstarted].</span><span class="sxs-lookup"><span data-stu-id="55e71-118">For more information, see [Get started with Azure IoT Edge][lnk-gw-getstarted].</span></span>

### <a name="protocol-ingestion-module"></a><span data-ttu-id="55e71-119">Protokol alım modülü</span><span class="sxs-lookup"><span data-stu-id="55e71-119">Protocol ingestion module</span></span>

<span data-ttu-id="55e71-120">Bu modül veri aygıtlar, ağ geçidi üzerinden ve buluta gönderimini için başlangıç noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="55e71-120">This module is the starting point for receiving data from devices, through the gateway, and into the cloud.</span></span> <span data-ttu-id="55e71-121">Aşağıdaki örnekte, modül:</span><span class="sxs-lookup"><span data-stu-id="55e71-121">In the sample, the module:</span></span>

1. <span data-ttu-id="55e71-122">Benzetimli sıcaklık veri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="55e71-122">Creates simulated temperature data.</span></span> <span data-ttu-id="55e71-123">Fiziksel aygıtların kullanırsanız, modül fiziksel aygıtların verileri okur.</span><span class="sxs-lookup"><span data-stu-id="55e71-123">If you use physical devices, the module reads data from those physical devices.</span></span>
1. <span data-ttu-id="55e71-124">Bir ileti oluşturur.</span><span class="sxs-lookup"><span data-stu-id="55e71-124">Creates a message.</span></span>
1. <span data-ttu-id="55e71-125">Benzetimli sıcaklık verileri ileti içeriği yerleştirir.</span><span class="sxs-lookup"><span data-stu-id="55e71-125">Places the simulated temperature data into the message content.</span></span>
1. <span data-ttu-id="55e71-126">Sahte bir MAC adresine sahip bir özellik iletiye ekler.</span><span class="sxs-lookup"><span data-stu-id="55e71-126">Adds a property with a fake MAC address to the message.</span></span>
1. <span data-ttu-id="55e71-127">İleti zincirinde sonraki modülü için kullanılabilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="55e71-127">Makes the message available to the next module in the chain.</span></span>

<span data-ttu-id="55e71-128">Modül adı verilen **Protokolü X alım** önceki diyagramda adlı **sanal cihaz** kaynak kodundaki.</span><span class="sxs-lookup"><span data-stu-id="55e71-128">The module called **Protocol X ingestion** in the previous diagram is called **Simulated device** in the source code.</span></span>

### <a name="mac-lt-gt-iot-hub-id-module"></a><span data-ttu-id="55e71-129">MAC &lt;-&gt; IoT Hub kimlik modülü</span><span class="sxs-lookup"><span data-stu-id="55e71-129">MAC &lt;-&gt; IoT Hub ID module</span></span>

<span data-ttu-id="55e71-130">Bu modül için bir Mac adresi özelliğine sahip iletileri tarar.</span><span class="sxs-lookup"><span data-stu-id="55e71-130">This module scans for messages that have a Mac address property.</span></span> <span data-ttu-id="55e71-131">Aşağıdaki örnekte Protokolü alım modülü MAC adres özelliği ekler.</span><span class="sxs-lookup"><span data-stu-id="55e71-131">In the sample, the protocol ingestion module adds the MAC address property.</span></span> <span data-ttu-id="55e71-132">Modül böyle bir özellik bulursa, iletiyi bir IOT Hub cihaz anahtarı ile başka bir özellik ekler.</span><span class="sxs-lookup"><span data-stu-id="55e71-132">If the module finds such a property, it adds another property with an IoT Hub device key to the message.</span></span> <span data-ttu-id="55e71-133">Modül sonra ileti sonraki modüle zincirinde kullanılabilmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="55e71-133">The module then makes the message available to the next module in the chain.</span></span>

<span data-ttu-id="55e71-134">Sanal cihazlar IOT Hub cihaz kimliklerini ile ilişkilendirmek için MAC adreslerinin ve IOT hub'ı kimlikleri arasında bir eşleme Geliştirici ayarlar.</span><span class="sxs-lookup"><span data-stu-id="55e71-134">The developer sets up a mapping between MAC addresses and IoT Hub identities to associate the simulated devices with IoT Hub device identities.</span></span> <span data-ttu-id="55e71-135">Geliştirici eşleme modülü yapılandırmasının bir parçası el ile ekler.</span><span class="sxs-lookup"><span data-stu-id="55e71-135">The developer adds the mapping manually as part of the module configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="55e71-136">Bu örnekte benzersiz cihaz tanımlayıcısı olarak bir MAC adresi kullanılır ve bir IoT Hub cihaz kimliğiyle ilişkilendirilir.</span><span class="sxs-lookup"><span data-stu-id="55e71-136">This sample uses a MAC address as a unique device identifier and correlates it with an IoT Hub device identity.</span></span> <span data-ttu-id="55e71-137">Bununla birlikte, farklı bir benzersiz tanımlayıcı kullanan kendi modülünüzü yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="55e71-137">However, you can write your own module that uses a different unique identifier.</span></span> <span data-ttu-id="55e71-138">Örneğin, cihazlarınızı benzersiz seri numarasına sahip veya telemetri verilerini benzersiz katıştırılmış cihaz adı içerebilir.</span><span class="sxs-lookup"><span data-stu-id="55e71-138">For example, your devices may have unique serial numbers or the telemetry data may include a unique embedded device name.</span></span>

### <a name="iot-hub-communication-module"></a><span data-ttu-id="55e71-139">IoT Hub iletişim modülü</span><span class="sxs-lookup"><span data-stu-id="55e71-139">IoT Hub communication module</span></span>

<span data-ttu-id="55e71-140">Bu modül iletileri bir IOT Hub ile önceki modülü tarafından atanan aygıt anahtar özelliği alır.</span><span class="sxs-lookup"><span data-stu-id="55e71-140">This module takes messages with an IoT Hub device key property that was assigned by the previous module.</span></span> <span data-ttu-id="55e71-141">Modül HTTP protokolünü kullanarak ileti içeriği IOT Hub'ına gönderir.</span><span class="sxs-lookup"><span data-stu-id="55e71-141">The module sends the message content to IoT Hub using the HTTP protocol.</span></span> <span data-ttu-id="55e71-142">HTTP, IoT Hub tarafından anlaşılan üç protokolden biridir.</span><span class="sxs-lookup"><span data-stu-id="55e71-142">HTTP is one of the three protocols understood by IoT Hub.</span></span>

<span data-ttu-id="55e71-143">Her sanal cihaz için bir bağlantı açarak yerine bu modül IOT hub'ına geçidinden tek bir HTTP bağlantısı açar.</span><span class="sxs-lookup"><span data-stu-id="55e71-143">Instead of opening a connection for each simulated device, this module opens a single HTTP connection from the gateway to the IoT hub.</span></span> <span data-ttu-id="55e71-144">Modül, tüm sanal cihazların gelen bağlantıları Bu bağlantı üzerinden sonra multiplexes.</span><span class="sxs-lookup"><span data-stu-id="55e71-144">The module then multiplexes connections from all the simulated devices over that connection.</span></span> <span data-ttu-id="55e71-145">Bu yaklaşım, pek çok daha fazla cihazları bağlamak tek bir ağ geçidi sağlar.</span><span class="sxs-lookup"><span data-stu-id="55e71-145">This approach enables a single gateway to connect many more devices.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="55e71-146">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="55e71-146">Before you get started</span></span>

<span data-ttu-id="55e71-147">Başlamadan önce şunları yapmalısınız:</span><span class="sxs-lookup"><span data-stu-id="55e71-147">Before you get started, you must:</span></span>

* <span data-ttu-id="55e71-148">[IOT hub oluşturma] [ lnk-create-hub] Azure aboneliğinizde bu yönlendirmeyi tamamlamak için hub adı gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="55e71-148">[Create an IoT hub][lnk-create-hub] in your Azure subscription, you need the name of your hub to complete this walkthrough.</span></span> <span data-ttu-id="55e71-149">Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="55e71-149">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="55e71-150">İki cihazlar IOT hub'ınızı ekleyin ve kendi kimlikleri ve cihaz anahtarlarını not edin.</span><span class="sxs-lookup"><span data-stu-id="55e71-150">Add two devices to your IoT hub and make a note of their ids and device keys.</span></span> <span data-ttu-id="55e71-151">Kullanabilirsiniz [aygıt explorer] [ lnk-device-explorer] veya [iothub-explorer] [ lnk-iothub-explorer] cihazlarınızı IOT hub'ı önceki adımda oluşturduğunuz eklemek için aracı ve kendi anahtarları alır.</span><span class="sxs-lookup"><span data-stu-id="55e71-151">You can use the [device explorer][lnk-device-explorer] or [iothub-explorer][lnk-iothub-explorer] tool to add your devices to the IoT hub you created in the previous step and retrieve their keys.</span></span>

![][2]

<!-- Images -->
[1]: media/iot-hub-iot-edge-simulated-selector/image1.png
[2]: media/iot-hub-iot-edge-simulated-selector/image2.png

<!-- Links -->
<span data-ttu-id="55e71-152">[sanal cihaz bulut karşıya örnek]: https://github.com/Azure/iot-edge/blob/master/samples/simulated_device_cloud_upload/README.md</span><span class="sxs-lookup"><span data-stu-id="55e71-152">[Simulated Device Cloud Upload sample]: https://github.com/Azure/iot-edge/blob/master/samples/simulated_device_cloud_upload/README.md</span></span>
[lnk-sdk]: https://github.com/Azure/iot-edge
[lnk-gw-getstarted]: ../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md
[lnk-create-hub]: ../articles/iot-hub/iot-hub-create-through-portal.md