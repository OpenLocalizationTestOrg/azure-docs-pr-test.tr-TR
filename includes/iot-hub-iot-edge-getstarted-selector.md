> [!div class="op_single_selector"]
> * [<span data-ttu-id="81cea-101">Linux</span><span class="sxs-lookup"><span data-stu-id="81cea-101">Linux</span></span>](../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md)
> * [<span data-ttu-id="81cea-102">Windows</span><span class="sxs-lookup"><span data-stu-id="81cea-102">Windows</span></span>](../articles/iot-hub/iot-hub-windows-iot-edge-get-started.md)
> 
> 

<span data-ttu-id="81cea-103">Bu makalede hello ayrıntılı bir kılavuz sağlar [Hello World örnek kodunun] [ lnk-helloworld-sample] tooillustrate hello temel bileşenlerini hello [Azure IOT kenar] [ lnk-iot-edge] mimarisi.</span><span class="sxs-lookup"><span data-stu-id="81cea-103">This article provides a detailed walkthrough of hello [Hello World sample code][lnk-helloworld-sample] tooillustrate hello fundamental components of hello [Azure IoT Edge][lnk-iot-edge] architecture.</span></span> <span data-ttu-id="81cea-104">Merhaba örnek hello Azure IOT kenar toobuild beş saniyede bir "hello world" iletisini tooa dosyası günlüklerini basit bir ağ geçidi kullanır.</span><span class="sxs-lookup"><span data-stu-id="81cea-104">hello sample uses hello Azure IoT Edge toobuild a simple gateway that logs a "hello world" message tooa file every five seconds.</span></span>

<span data-ttu-id="81cea-105">Bu kılavuzda aşağıdaki konular ele alınmaktadır:</span><span class="sxs-lookup"><span data-stu-id="81cea-105">This walkthrough covers:</span></span>

* <span data-ttu-id="81cea-106">**Hello World örnek mimarisi**: açıklar nasıl [Azure IOT kenar mimari kavramlarını] [ lnk-edge-concepts] toohello Hello World örnek ve hello bileşenleri nasıl bir araya getireceğinizi uygulanır.</span><span class="sxs-lookup"><span data-stu-id="81cea-106">**Hello World sample architecture**: Describes how [Azure IoT Edge architectural concepts][lnk-edge-concepts] apply toohello Hello World sample and how hello components fit together.</span></span>
* <span data-ttu-id="81cea-107">**Nasıl toobuild hello örnek**: hello adımları gerekli toobuild hello örnek.</span><span class="sxs-lookup"><span data-stu-id="81cea-107">**How toobuild hello sample**: hello steps required toobuild hello sample.</span></span>
* <span data-ttu-id="81cea-108">**Nasıl toorun hello örnek**: hello adımları gerekli toorun hello örnek.</span><span class="sxs-lookup"><span data-stu-id="81cea-108">**How toorun hello sample**: hello steps required toorun hello sample.</span></span> 
* <span data-ttu-id="81cea-109">**Tipik çıkış**: hello örneği tooexpect hello örnek çalıştırdığınızda, çıktı.</span><span class="sxs-lookup"><span data-stu-id="81cea-109">**Typical output**: An example of hello output tooexpect when you run hello sample.</span></span>
* <span data-ttu-id="81cea-110">**Kod parçacıkları**: hello Hello World örnek nasıl uyguladığını kod parçacıkları tooshow koleksiyonu IOT sınır ağ geçidi bileşenlerini anahtar.</span><span class="sxs-lookup"><span data-stu-id="81cea-110">**Code snippets**: A collection of code snippets tooshow how hello Hello World sample implements key IoT Edge gateway components.</span></span>


## <a name="hello-world-sample-architecture"></a><span data-ttu-id="81cea-111">Hello World örnek mimarisi</span><span class="sxs-lookup"><span data-stu-id="81cea-111">Hello World sample architecture</span></span>
<span data-ttu-id="81cea-112">Merhaba Hello World örnek hello önceki bölümde açıklanan hello kavramları göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="81cea-112">hello Hello World sample illustrates hello concepts described in hello previous section.</span></span> <span data-ttu-id="81cea-113">Merhaba Hello World örneği iki IOT kenar modülden oluşan bir işlem hattına sahip bir IOT sınır ağ geçidi uygular:</span><span class="sxs-lookup"><span data-stu-id="81cea-113">hello Hello World sample implements a IoT Edge gateway that has a pipeline made up of two IoT Edge modules:</span></span>

* <span data-ttu-id="81cea-114">Merhaba *Merhaba Dünya* modülü beş saniyede bir ileti oluşturur ve bunu toohello Günlükçü modülüne geçirir.</span><span class="sxs-lookup"><span data-stu-id="81cea-114">hello *hello world* module creates a message every five seconds and passes it toohello logger module.</span></span>
* <span data-ttu-id="81cea-115">Merhaba *Günlükçü* tooa dosya aldığı modülü yazma Merhaba iletileri.</span><span class="sxs-lookup"><span data-stu-id="81cea-115">hello *logger* module writes hello messages it receives tooa file.</span></span>

![Azure IoT Edge ile oluşturulan Hello World örneğinin mimarisi][4]

<span data-ttu-id="81cea-117">Merhaba önceki bölümde açıklandığı gibi hello Hello World modülü geçemezse toohello Günlükçü modülü beş saniyede doğrudan iletileri.</span><span class="sxs-lookup"><span data-stu-id="81cea-117">As described in hello previous section, hello Hello World module does not pass messages directly toohello logger module every five seconds.</span></span> <span data-ttu-id="81cea-118">Bunun yerine, beş saniyede bir ileti toohello Aracısı yayımlar.</span><span class="sxs-lookup"><span data-stu-id="81cea-118">Instead, it publishes a message toohello broker every five seconds.</span></span>

<span data-ttu-id="81cea-119">Merhaba Günlükçü modülü hello Aracısı'ndan hello iletiyi alır ve bunu temel hello ileti tooa dosyasının Merhaba içeriğine yazma davranır.</span><span class="sxs-lookup"><span data-stu-id="81cea-119">hello logger module receives hello message from hello broker and acts upon it, writing hello contents of hello message tooa file.</span></span>

<span data-ttu-id="81cea-120">Merhaba Günlükçü modülü yalnızca hello Aracısı gelen iletileri kullanır, hiçbir zaman yeni ileti toohello Aracısı yayımlar.</span><span class="sxs-lookup"><span data-stu-id="81cea-120">hello logger module only consumes messages from hello broker, it never publishes new messages toohello broker.</span></span>

![Azure IOT kenar modülleri arasında iletileri hello Aracısı nasıl yönlendirir][5]

<span data-ttu-id="81cea-122">Merhaba Yukarıdaki şekilde hello Hello World örnek ve hello göreli yollar hello mimarisi hello hello örnek farklı kısımlarını uygulayan toohello kaynak dosyaları gösterir [deposu][lnk-iot-edge].</span><span class="sxs-lookup"><span data-stu-id="81cea-122">hello figure above shows hello architecture of hello Hello World sample and hello relative paths toohello source files that implement different portions of hello sample in hello [repository][lnk-iot-edge].</span></span> <span data-ttu-id="81cea-123">Merhaba kodu kendiniz keşfedin veya kılavuz olarak aşağıdaki kod parçacıklarından hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="81cea-123">Explore hello code on your own, or use hello code snippets below as a guide.</span></span>

<!-- Images -->
[4]: media/iot-hub-iot-edge-getstarted-selector/high_level_architecture.png
[5]: media/iot-hub-iot-edge-getstarted-selector/detailed_architecture.png

<!-- Links -->
[lnk-helloworld-sample]: https://github.com/Azure/iot-edge/tree/master/samples/hello_world
[lnk-iot-edge]: https://github.com/Azure/iot-edge
[lnk-edge-concepts]: ../articles/iot-hub/iot-hub-iot-edge-overview.md