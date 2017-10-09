> [!div class="op_single_selector"]
> * [<span data-ttu-id="ce75a-101">Node.js</span><span class="sxs-lookup"><span data-stu-id="ce75a-101">Node.js</span></span>](../articles/iot-hub/iot-hub-node-node-twin-getstarted.md)
> * [<span data-ttu-id="ce75a-102">C#/node.js</span><span class="sxs-lookup"><span data-stu-id="ce75a-102">C#/Node.js</span></span>](../articles/iot-hub/iot-hub-csharp-node-twin-getstarted.md)
> * [<span data-ttu-id="ce75a-103">C#</span><span class="sxs-lookup"><span data-stu-id="ce75a-103">C#</span></span>](../articles/iot-hub/iot-hub-csharp-csharp-twin-getstarted.md)
> * [<span data-ttu-id="ce75a-104">Java</span><span class="sxs-lookup"><span data-stu-id="ce75a-104">Java</span></span>](../articles/iot-hub/iot-hub-java-java-twin-getstarted.md)

<span data-ttu-id="ce75a-105">Cihaz çiftleri, cihaz durumu bilgilerini (meta veriler, yapılandırmalar ve koşullar) depolayan JSON belgelerdir.</span><span class="sxs-lookup"><span data-stu-id="ce75a-105">Device twins are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="ce75a-106">IOT Hub cihaz çifti tooit bağlanan her aygıt için devam ettirir.</span><span class="sxs-lookup"><span data-stu-id="ce75a-106">IoT Hub persists a device twin for each device that connects tooit.</span></span>

<span data-ttu-id="ce75a-107">Cihaz çiftlerini kullanın:</span><span class="sxs-lookup"><span data-stu-id="ce75a-107">Use device twins to:</span></span>

* <span data-ttu-id="ce75a-108">Çözüm arka ucunuz cihaz meta verilerini depolar.</span><span class="sxs-lookup"><span data-stu-id="ce75a-108">Store device metadata from your solution back end.</span></span>
* <span data-ttu-id="ce75a-109">Kullanılabilir özellikler ve koşullar (kullanılan gibi hello bağlantı yöntemi) gibi geçerli durumu bilgileri, cihaz uygulamanızdan bildirin.</span><span class="sxs-lookup"><span data-stu-id="ce75a-109">Report current state information such as available capabilities and conditions (for example, hello connectivity method used) from your device app.</span></span>
* <span data-ttu-id="ce75a-110">Cihaz uygulama ve arka uç uygulama arasında uzun süre çalışan iş akışları (örneğin, bellenim ve yapılandırma güncelleştirmeleri) Hello durumunu eşitleyin.</span><span class="sxs-lookup"><span data-stu-id="ce75a-110">Synchronize hello state of long-running workflows (such as firmware and configuration updates) between a device app and a back-end app.</span></span>
* <span data-ttu-id="ce75a-111">Cihaz meta verilerini, yapılandırma veya durumu sorgu.</span><span class="sxs-lookup"><span data-stu-id="ce75a-111">Query your device metadata, configuration, or state.</span></span>

> [!NOTE]
> <span data-ttu-id="ce75a-112">Cihaz çiftlerini cihaz yapılandırmalarını ve koşullar sorgulamak için ve eşitleme için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="ce75a-112">Device twins are designed for synchronization and for querying device configurations and conditions.</span></span> <span data-ttu-id="ce75a-113">Toouse cihaz çiftlerini zaman bulunabilir hakkında daha fazla bilgiler [cihaz çiftlerini anlamak][lnk-twins].</span><span class="sxs-lookup"><span data-stu-id="ce75a-113">More informations on when toouse device twins can be found in [Understand device twins][lnk-twins].</span></span>

<span data-ttu-id="ce75a-114">Cihaz çiftlerini bir IOT hub ' depolanır ve içerir:</span><span class="sxs-lookup"><span data-stu-id="ce75a-114">Device twins are stored in an IoT hub and contain:</span></span>

* <span data-ttu-id="ce75a-115">*Etiketler*, cihaz meta verilerini yalnızca hello çözüm arka ucu tarafından; erişilebilir</span><span class="sxs-lookup"><span data-stu-id="ce75a-115">*tags*, device metadata accessible only by hello solution back end;</span></span>
* <span data-ttu-id="ce75a-116">*Özellikler istenen*, JSON nesnelerini hello çözümü tarafından değiştirilebilir hello cihaz uygulaması tarafından; başa bitiş ve observable ve</span><span class="sxs-lookup"><span data-stu-id="ce75a-116">*desired properties*, JSON objects modifiable by hello solution back end and observable by hello device app; and</span></span>
* <span data-ttu-id="ce75a-117">*Özellikler bildirilen*, JSON nesnelerini hello cihaz uygulaması tarafından değiştirilebilir ve hello çözüm arka ucu tarafından okunabilir.</span><span class="sxs-lookup"><span data-stu-id="ce75a-117">*reported properties*, JSON objects modifiable by hello device app and readable by hello solution back end.</span></span> <span data-ttu-id="ce75a-118">Etiketleri ve özellikleri diziler içeremez, ancak nesneleri iç içe olamaz.</span><span class="sxs-lookup"><span data-stu-id="ce75a-118">Tags and properties cannot contain arrays, but objects can be nested.</span></span>

![][img-twin]

<span data-ttu-id="ce75a-119">Ayrıca, hello çözüm arka ucu veri yukarıdaki tüm hello dayalı cihaz çiftlerini sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ce75a-119">Additionally, hello solution back end can query device twins based on all hello above data.</span></span>
<span data-ttu-id="ce75a-120">Çok başvuran[cihaz çiftlerini anlamak] [ lnk-twins] cihaz çiftlerini ve toohello hakkında daha fazla bilgi için [IOT hub'ı sorgu dili] [ lnk-query] başvurusu sorgulama için.</span><span class="sxs-lookup"><span data-stu-id="ce75a-120">Refer too[Understand device twins][lnk-twins] for more information about device twins, and toohello [IoT Hub query language][lnk-query] reference for querying.</span></span>

> [!NOTE]
> <span data-ttu-id="ce75a-121">Şu anda cihaz çiftlerini tooIoT hub'a bağlanan aygıtlardan erişilebilir hello MQTT protokolünü kullanarak.</span><span class="sxs-lookup"><span data-stu-id="ce75a-121">At this time, device twins are accessible only from devices that connect tooIoT Hub using hello MQTT protocol.</span></span> <span data-ttu-id="ce75a-122">Lütfen toohello bakın [MQTT Destek] [ lnk-devguide-mqtt] hakkında yönergeler için makalenin tooconvert mevcut aygıt uygulama toouse MQTT.</span><span class="sxs-lookup"><span data-stu-id="ce75a-122">Please refer toohello [MQTT support][lnk-devguide-mqtt] article for instructions on how tooconvert existing device app toouse MQTT.</span></span>

<span data-ttu-id="ce75a-123">Bu öğretici şunların nasıl yapıldığını gösterir:</span><span class="sxs-lookup"><span data-stu-id="ce75a-123">This tutorial shows you how to:</span></span>

* <span data-ttu-id="ce75a-124">Ekler bir arka uç uygulaması oluşturma *etiketleri* tooa cihaz çifti ve bağlantısını raporları bir sanal cihaz uygulamasının kanal olarak bir *özelliği bildirilen* hello cihaz çifti üzerinde.</span><span class="sxs-lookup"><span data-stu-id="ce75a-124">Create a back-end app that adds *tags* tooa device twin, and a simulated device app that reports its connectivity channel as a *reported property* on hello device twin.</span></span>
* <span data-ttu-id="ce75a-125">Merhaba etiketleri ve daha önce oluşturduğunuz özellikleri filtreleri kullanarak arka uç uygulamanızı aygıtlardan sorgu.</span><span class="sxs-lookup"><span data-stu-id="ce75a-125">Query devices from your back-end app using filters on hello tags and properties previously created.</span></span>

<!-- images -->
[img-twin]: media/iot-hub-selector-twin-get-started/twin.png

<!-- links -->
[lnk-query]: ../articles/iot-hub/iot-hub-devguide-query-language.md
[lnk-twins]: ../articles/iot-hub/iot-hub-devguide-device-twins.md
[lnk-d2c]: ../articles/iot-hub/iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: ../articles/iot-hub/iot-hub-mqtt-support.md