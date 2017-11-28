> [!div class="op_single_selector"]
> * [<span data-ttu-id="bd28d-101">Node.js</span><span class="sxs-lookup"><span data-stu-id="bd28d-101">Node.js</span></span>](../articles/iot-hub/iot-hub-node-node-twin-getstarted.md)
> * [<span data-ttu-id="bd28d-102">C#/node.js</span><span class="sxs-lookup"><span data-stu-id="bd28d-102">C#/Node.js</span></span>](../articles/iot-hub/iot-hub-csharp-node-twin-getstarted.md)
> * [<span data-ttu-id="bd28d-103">C#</span><span class="sxs-lookup"><span data-stu-id="bd28d-103">C#</span></span>](../articles/iot-hub/iot-hub-csharp-csharp-twin-getstarted.md)
> * [<span data-ttu-id="bd28d-104">Java</span><span class="sxs-lookup"><span data-stu-id="bd28d-104">Java</span></span>](../articles/iot-hub/iot-hub-java-java-twin-getstarted.md)

<span data-ttu-id="bd28d-105">Cihaz çiftleri, cihaz durumu bilgilerini (meta veriler, yapılandırmalar ve koşullar) depolayan JSON belgelerdir.</span><span class="sxs-lookup"><span data-stu-id="bd28d-105">Device twins are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="bd28d-106">IOT Hub cihaz çifti ona bağlanan her aygıt için devam ettirir.</span><span class="sxs-lookup"><span data-stu-id="bd28d-106">IoT Hub persists a device twin for each device that connects to it.</span></span>

<span data-ttu-id="bd28d-107">Cihaz çiftlerini kullanın:</span><span class="sxs-lookup"><span data-stu-id="bd28d-107">Use device twins to:</span></span>

* <span data-ttu-id="bd28d-108">Çözüm arka ucunuz cihaz meta verilerini depolar.</span><span class="sxs-lookup"><span data-stu-id="bd28d-108">Store device metadata from your solution back end.</span></span>
* <span data-ttu-id="bd28d-109">Kullanılabilir özellikler ve koşullar (örneğin, kullanılan bağlantı yöntemi) gibi geçerli durumu bilgileri, cihaz uygulamanızdan bildirin.</span><span class="sxs-lookup"><span data-stu-id="bd28d-109">Report current state information such as available capabilities and conditions (for example, the connectivity method used) from your device app.</span></span>
* <span data-ttu-id="bd28d-110">Cihaz uygulama ve arka uç uygulama arasında uzun süre çalışan iş akışları (örneğin, bellenim ve yapılandırma güncelleştirmeleri) durumunu eşitleyin.</span><span class="sxs-lookup"><span data-stu-id="bd28d-110">Synchronize the state of long-running workflows (such as firmware and configuration updates) between a device app and a back-end app.</span></span>
* <span data-ttu-id="bd28d-111">Cihaz meta verilerini, yapılandırma veya durumu sorgu.</span><span class="sxs-lookup"><span data-stu-id="bd28d-111">Query your device metadata, configuration, or state.</span></span>

> [!NOTE]
> <span data-ttu-id="bd28d-112">Cihaz çiftlerini cihaz yapılandırmalarını ve koşullar sorgulamak için ve eşitleme için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="bd28d-112">Device twins are designed for synchronization and for querying device configurations and conditions.</span></span> <span data-ttu-id="bd28d-113">Zaman cihaz çiftlerini kullanılacağı hakkında daha fazla bilgiler bulunabilir [cihaz çiftlerini anlamak][lnk-twins].</span><span class="sxs-lookup"><span data-stu-id="bd28d-113">More informations on when to use device twins can be found in [Understand device twins][lnk-twins].</span></span>

<span data-ttu-id="bd28d-114">Cihaz çiftlerini bir IOT hub ' depolanır ve içerir:</span><span class="sxs-lookup"><span data-stu-id="bd28d-114">Device twins are stored in an IoT hub and contain:</span></span>

* <span data-ttu-id="bd28d-115">*Etiketler*, cihaz meta verilerini yalnızca çözüm arka ucu tarafından; erişilebilir</span><span class="sxs-lookup"><span data-stu-id="bd28d-115">*tags*, device metadata accessible only by the solution back end;</span></span>
* <span data-ttu-id="bd28d-116">*Özellikler istenen*, JSON nesnelerinin çözümü tarafından değiştirilebilir, cihaz uygulaması tarafından; uç ve observable yedekleyin ve</span><span class="sxs-lookup"><span data-stu-id="bd28d-116">*desired properties*, JSON objects modifiable by the solution back end and observable by the device app; and</span></span>
* <span data-ttu-id="bd28d-117">*Özellikler bildirilen*, JSON nesnelerini cihaz uygulaması tarafından değiştirilebilir ve çözüm arka ucu tarafından okunabilir.</span><span class="sxs-lookup"><span data-stu-id="bd28d-117">*reported properties*, JSON objects modifiable by the device app and readable by the solution back end.</span></span> <span data-ttu-id="bd28d-118">Etiketleri ve özellikleri diziler içeremez, ancak nesneleri iç içe olamaz.</span><span class="sxs-lookup"><span data-stu-id="bd28d-118">Tags and properties cannot contain arrays, but objects can be nested.</span></span>

![][img-twin]

<span data-ttu-id="bd28d-119">Ayrıca, çözüm arka ucu yukarıdaki tüm verilere dayalı cihaz çiftlerini sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd28d-119">Additionally, the solution back end can query device twins based on all the above data.</span></span>
<span data-ttu-id="bd28d-120">Başvurmak [cihaz çiftlerini anlamak] [ lnk-twins] ve cihaz çiftlerini hakkında daha fazla bilgi için [IOT hub'ı sorgu dili] [ lnk-query] için başvuru sorgulama.</span><span class="sxs-lookup"><span data-stu-id="bd28d-120">Refer to [Understand device twins][lnk-twins] for more information about device twins, and to the [IoT Hub query language][lnk-query] reference for querying.</span></span>

> [!NOTE]
> <span data-ttu-id="bd28d-121">Şu anda cihaz çiftlerini MQTT protokolünü kullanarak IOT hub'a bağlanan cihazlar üzerinden erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="bd28d-121">At this time, device twins are accessible only from devices that connect to IoT Hub using the MQTT protocol.</span></span> <span data-ttu-id="bd28d-122">Lütfen [MQTT Destek] [ lnk-devguide-mqtt] MQTT kullanmak mevcut cihaz uygulaması dönüştürme hakkında yönergeler için makalenin.</span><span class="sxs-lookup"><span data-stu-id="bd28d-122">Please refer to the [MQTT support][lnk-devguide-mqtt] article for instructions on how to convert existing device app to use MQTT.</span></span>

<span data-ttu-id="bd28d-123">Bu öğretici şunların nasıl yapıldığını gösterir:</span><span class="sxs-lookup"><span data-stu-id="bd28d-123">This tutorial shows you how to:</span></span>

* <span data-ttu-id="bd28d-124">Ekler bir arka uç uygulaması oluşturma *etiketleri* cihaz çifti ve kendi bağlantı kanalı olarak raporları bir sanal cihaz uygulamasının bir *özelliği bildirilen* cihaz çifti üzerinde.</span><span class="sxs-lookup"><span data-stu-id="bd28d-124">Create a back-end app that adds *tags* to a device twin, and a simulated device app that reports its connectivity channel as a *reported property* on the device twin.</span></span>
* <span data-ttu-id="bd28d-125">Filtreler etiketler ve daha önce oluşturduğunuz özellikleri kullanarak arka uç uygulamanızı aygıtlardan sorgu.</span><span class="sxs-lookup"><span data-stu-id="bd28d-125">Query devices from your back-end app using filters on the tags and properties previously created.</span></span>

<!-- images -->
[img-twin]: media/iot-hub-selector-twin-get-started/twin.png

<!-- links -->
[lnk-query]: ../articles/iot-hub/iot-hub-devguide-query-language.md
[lnk-twins]: ../articles/iot-hub/iot-hub-devguide-device-twins.md
[lnk-d2c]: ../articles/iot-hub/iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: ../articles/iot-hub/iot-hub-mqtt-support.md