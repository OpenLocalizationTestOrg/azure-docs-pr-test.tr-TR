> [!div class="op_single_selector"]
> * [<span data-ttu-id="210e2-101">Node.js</span><span class="sxs-lookup"><span data-stu-id="210e2-101">Node.js</span></span>](../articles/iot-hub/iot-hub-node-node-twin-how-to-configure.md)
> * [<span data-ttu-id="210e2-102">C#/node.js</span><span class="sxs-lookup"><span data-stu-id="210e2-102">C#/Node.js</span></span>](../articles/iot-hub/iot-hub-csharp-node-twin-how-to-configure.md)
> * [<span data-ttu-id="210e2-103">C#</span><span class="sxs-lookup"><span data-stu-id="210e2-103">C#</span></span>](../articles/iot-hub/iot-hub-csharp-csharp-twin-how-to-configure.md)
> 
> 

## <a name="introduction"></a><span data-ttu-id="210e2-104">Giriş</span><span class="sxs-lookup"><span data-stu-id="210e2-104">Introduction</span></span>

<span data-ttu-id="210e2-105">İçinde [IOT Hub cihaz çiftlerini ile çalışmaya başlama][lnk-twin-tutorial], çözüm arka tooset cihaz meta verilerini nasıl son kullanma hakkında bilgi edindiniz *etiketleri*, rapor cihaz uygulaması cihaz koşulları kullanarak *özellikleri bildirilen*ve SQL benzeri bir dil kullanarak bu bilgileri sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="210e2-105">In [Get started with IoT Hub device twins][lnk-twin-tutorial], you learned how tooset device metadata from your solution back end using *tags*, report device conditions from a device app using *reported properties*, and query this information using a SQL-like language.</span></span>

<span data-ttu-id="210e2-106">Bu öğreticide, nasıl toouse hello hello cihaz çifti'nın öğreneceksiniz *özelliklerini istenen* ile birlikte *özellikleri bildirilen*, tooremotely cihaz uygulamalarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="210e2-106">In this tutorial, you will learn how toouse hello hello device twin's *desired properties* along with *reported properties*, tooremotely configure device apps.</span></span> <span data-ttu-id="210e2-107">Daha belirgin olarak Bu öğretici, bir cihaz çifti 's nasıl bildirilen gösterir ve istenen özellikler cihaz uygulamasının çok adımlı yapılandırmasını etkinleştirmek ve cihazlara hello görünürlük toohello çözüm arka ucu bu işlemi hello durumunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="210e2-107">More specifically, this tutorial shows how a device twin's reported and desired properties enable a multi-step configuration of a device application, and provide hello visibility toohello solution back end of hello status of this operation across all devices.</span></span> <span data-ttu-id="210e2-108">Cihaz yapılandırmaları hello rolü ile ilgili daha fazla bilgi bulabilirsiniz [cihaz yönetimine genel bakış IOT Hub ile][lnk-dm-overview].</span><span class="sxs-lookup"><span data-stu-id="210e2-108">You can find more information regarding hello role of device configurations in [Overview of device management with IoT Hub][lnk-dm-overview].</span></span>

<span data-ttu-id="210e2-109">Yüksek bir düzeyde cihaz çiftlerini kullanarak hello çözüm arka ucu toospecify hello istenen yapılandırma belirli komutları göndermek yerine, hello yönetilen cihazlar için etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="210e2-109">At a high level, using device twins enables hello solution back end toospecify hello desired configuration for hello managed devices, instead of sending specific commands.</span></span> <span data-ttu-id="210e2-110">Bu hello en iyi şekilde tooupdate yapılandırmasıyla (çok önemli olduğu belirli cihaz koşullar etkileyen hello özelliği tooimmediately belirli komutları Yürüt IOT senaryolarda), ayarı sorumlu hello aygıt koyar sürekli toohello raporlama oluştu Çözüm arka ucu hello geçerli durumu ve hello güncelleştirme işleminin olası hata koşulları.</span><span class="sxs-lookup"><span data-stu-id="210e2-110">This puts hello device in charge of setting up hello best way tooupdate its configuration (very important in IoT scenarios where specific device conditions affect hello ability tooimmediately carry out specific commands), while continually reporting toohello solution back end hello current state and potential error conditions of hello update process.</span></span> <span data-ttu-id="210e2-111">Bu deseni enstrümental toohello yönetimi, cihazların büyük kümelerinin aynıdır cihazlara hello çözüm arka ucu toohave tam görünürlüğünü hello yapılandırma işlemi hello durumunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="210e2-111">This pattern is instrumental toohello management of large sets of devices, as it enables hello solution back end toohave full visibility of hello state of hello configuration process across all devices.</span></span>

> [!NOTE]
> <span data-ttu-id="210e2-112">Burada aygıtları denetlenir daha etkileşimli bir şekilde (kullanıcı tarafından denetlenen bir uygulamadan fan etkinleştirin) senaryolarında kullanmayı [doğrudan yöntemleri][lnk-methods].</span><span class="sxs-lookup"><span data-stu-id="210e2-112">In scenarios where devices are controlled in a more interactive fashion (turn on a fan from a user-controlled app), consider using [direct methods][lnk-methods].</span></span>
> 
> 

<span data-ttu-id="210e2-113">Bu öğreticide, hello telemetri yapılandırmasını bir hedef cihaz ve, hello cihaz uygulaması sonucunda çok adımlı işlem tooapply bir yapılandırma izleyen hello çözüm arka uç değişiklikleri (gerektiren bir yazılım modülü yeniden, bu örnek için güncelleştirme öğretici basit bir gecikmeyle taklit eder).</span><span class="sxs-lookup"><span data-stu-id="210e2-113">In this tutorial, hello solution back end changes hello telemetry configuration of a target device and, as a result of that, hello device app follows a multi-step process tooapply a configuration update (for example, requiring a software module restart, which this tutorial simulates with a simple delay).</span></span>

<span data-ttu-id="210e2-114">Merhaba çözüm arka ucu hello yapılandırma hello cihaz çifti'nın istenen şekilde aşağıdaki hello özelliklerinde depolar:</span><span class="sxs-lookup"><span data-stu-id="210e2-114">hello solution back end stores hello configuration in hello device twin's desired properties in hello following way:</span></span>

        {
            ...
            "properties": {
                ...
                "desired": {
                    "telemetryConfig": {
                        "configId": "{id of hello configuration}",
                        "sendFrequency": "{config}"
                    }
                }
                ...
            }
            ...
        }

> [!NOTE]
> <span data-ttu-id="210e2-115">Yapılandırmaları karmaşık nesneler olabileceği için genellikle benzersiz kimlikler atanmışlarsa (karmaları veya [GUID'ler][lnk-guid]) toosimplify kendi karşılaştırmaları.</span><span class="sxs-lookup"><span data-stu-id="210e2-115">Since configurations can be complex objects, they are usually assigned unique ids (hashes or [GUIDs][lnk-guid]) toosimplify their comparisons.</span></span>
> 
> 

<span data-ttu-id="210e2-116">Merhaba cihaz uygulaması raporları istenen hello özelliği yansıtma geçerli yapılandırmasını **telemetryConfig** özellikleri hello bildirdi:</span><span class="sxs-lookup"><span data-stu-id="210e2-116">hello device app reports its current configuration mirroring hello desired property **telemetryConfig** in hello reported properties:</span></span>

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of hello current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Success",
                    }
                }
                ...
            }
        }

<span data-ttu-id="210e2-117">Hello nasıl bildirilen Not **telemetryConfig** ek bir özelliğe sahiptir **durum**, tooreport hello hello yapılandırmasını güncelleştirme işleminin durumunu kullanılır.</span><span class="sxs-lookup"><span data-stu-id="210e2-117">Note how hello reported **telemetryConfig** has an additional property **status**, used tooreport hello state of hello configuration update process.</span></span>

<span data-ttu-id="210e2-118">Yeni bir istenen yapılandırma alındığında hello cihaz uygulaması hello bilgi değiştirerek bekleyen yapılandırma raporları:</span><span class="sxs-lookup"><span data-stu-id="210e2-118">When a new desired configuration is received, hello device app reports a pending configuration by changing hello information:</span></span>

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of hello current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Pending",
                        "pendingConfig": {
                            "changeId": "{id of hello pending configuration}",
                            "sendFrequency": "{pending configuration}"
                        }
                    }
                }
                ...
            }
        }

<span data-ttu-id="210e2-119">Ardından, daha sonraki bir zamanda, hello cihaz uygulaması hello başarı veya başarısızlık bu işlemin özelliği yukarıda hello güncelleştirerek rapor eder.</span><span class="sxs-lookup"><span data-stu-id="210e2-119">Then, at some later time, hello device app will report hello success or failure of this operation by updating hello above property.</span></span>
<span data-ttu-id="210e2-120">Nasıl hello çözüm arka ucu herhangi bir anda tooquery hello tüm hello aygıtlar arasında hello yapılandırma işleminin durumunu kullanabilir olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="210e2-120">Note how hello solution back end is able, at any time, tooquery hello status of hello configuration process across all hello devices.</span></span>

<span data-ttu-id="210e2-121">Bu öğretici şunların nasıl yapıldığını gösterir:</span><span class="sxs-lookup"><span data-stu-id="210e2-121">This tutorial shows you how to:</span></span>

* <span data-ttu-id="210e2-122">Merhaba çözüm arka uçtan yapılandırma güncelleştirmeleri alıp olarak birden çok güncelleştirme raporları bir sanal cihaz uygulaması oluşturma *özellikleri bildirilen* işlem hello yapılandırmasını güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="210e2-122">Create a simulated device app that receives configuration updates from hello solution back end, and reports multiple updates as *reported properties* on hello configuration update process.</span></span>
* <span data-ttu-id="210e2-123">Bir aygıt, istenen yapılandırma güncelleştirmeleri hello ve ardından yapılandırma güncelleştirme işlemi sorguları hello bir arka uç uygulaması oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="210e2-123">Create a back-end app that updates hello desired configuration of a device, and then queries hello configuration update process.</span></span>

<!-- links -->

[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: ../articles/iot-hub/iot-hub-device-management-overview.md
[lnk-twin-tutorial]: ../articles/iot-hub/iot-hub-node-node-twin-getstarted.md
[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier
