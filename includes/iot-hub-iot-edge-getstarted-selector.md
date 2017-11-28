> [!div class="op_single_selector"]
> * [<span data-ttu-id="618c9-101">Linux</span><span class="sxs-lookup"><span data-stu-id="618c9-101">Linux</span></span>](../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md)
> * [<span data-ttu-id="618c9-102">Windows</span><span class="sxs-lookup"><span data-stu-id="618c9-102">Windows</span></span>](../articles/iot-hub/iot-hub-windows-iot-edge-get-started.md)
> 
> 

<span data-ttu-id="618c9-103">Bu makalede [Azure IoT Edge][lnk-iot-edge] mimarisinin temel bileşenlerini göstermek üzere [Hello World örnek kodunun][lnk-helloworld-sample] ayrıntılı bilgileri verilmektedir.</span><span class="sxs-lookup"><span data-stu-id="618c9-103">This article provides a detailed walkthrough of the [Hello World sample code][lnk-helloworld-sample] to illustrate the fundamental components of the [Azure IoT Edge][lnk-iot-edge] architecture.</span></span> <span data-ttu-id="618c9-104">Örnek, "hello world" iletisini her beş saniyede bir dosyaya kaydeden basit bir ağ geçidi oluşturmak üzere Azure IoT Edge'i kullanır.</span><span class="sxs-lookup"><span data-stu-id="618c9-104">The sample uses the Azure IoT Edge to build a simple gateway that logs a "hello world" message to a file every five seconds.</span></span>

<span data-ttu-id="618c9-105">Bu kılavuzda aşağıdaki konular ele alınmaktadır:</span><span class="sxs-lookup"><span data-stu-id="618c9-105">This walkthrough covers:</span></span>

* <span data-ttu-id="618c9-106">**Hello World örnek mimarisi**: açıklar nasıl [Azure IOT kenar mimari kavramlarını] [ lnk-edge-concepts] Hello World örneği ve bileşenlerin nasıl bir araya getireceğinizi için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="618c9-106">**Hello World sample architecture**: Describes how [Azure IoT Edge architectural concepts][lnk-edge-concepts] apply to the Hello World sample and how the components fit together.</span></span>
* <span data-ttu-id="618c9-107">**Örneği oluşturma**: Örneği oluşturmak için gerekli adımlar.</span><span class="sxs-lookup"><span data-stu-id="618c9-107">**How to build the sample**: The steps required to build the sample.</span></span>
* <span data-ttu-id="618c9-108">**Örneği çalıştırma**: Örneği çalıştırmak için gerekli adımlar.</span><span class="sxs-lookup"><span data-stu-id="618c9-108">**How to run the sample**: The steps required to run the sample.</span></span> 
* <span data-ttu-id="618c9-109">**Tipik çıkış**: Örneği çalıştırdığınızda beklenecek çıktı örneği.</span><span class="sxs-lookup"><span data-stu-id="618c9-109">**Typical output**: An example of the output to expect when you run the sample.</span></span>
* <span data-ttu-id="618c9-110">**Kod parçacıkları**: Hello World örnek anahtar IOT sınır ağ geçidi bileşenlerini nasıl uyguladığını gösteren kod parçacıkları koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="618c9-110">**Code snippets**: A collection of code snippets to show how the Hello World sample implements key IoT Edge gateway components.</span></span>


## <a name="hello-world-sample-architecture"></a><span data-ttu-id="618c9-111">Hello World örnek mimarisi</span><span class="sxs-lookup"><span data-stu-id="618c9-111">Hello World sample architecture</span></span>
<span data-ttu-id="618c9-112">Hello World örneği önceki bölümde açıklanan kavramları göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="618c9-112">The Hello World sample illustrates the concepts described in the previous section.</span></span> <span data-ttu-id="618c9-113">Hello World örneği iki IOT kenar modülden oluşan bir işlem hattına sahip bir IOT sınır ağ geçidi uygular:</span><span class="sxs-lookup"><span data-stu-id="618c9-113">The Hello World sample implements a IoT Edge gateway that has a pipeline made up of two IoT Edge modules:</span></span>

* <span data-ttu-id="618c9-114">*Hello world* modülü beş saniyede bir ileti oluşturur ve günlükçü modülüne geçirir.</span><span class="sxs-lookup"><span data-stu-id="618c9-114">The *hello world* module creates a message every five seconds and passes it to the logger module.</span></span>
* <span data-ttu-id="618c9-115">*Günlükçü* modülü aldığı iletileri bir dosyaya yazar.</span><span class="sxs-lookup"><span data-stu-id="618c9-115">The *logger* module writes the messages it receives to a file.</span></span>

![Azure IoT Edge ile oluşturulan Hello World örneğinin mimarisi][4]

<span data-ttu-id="618c9-117">Önceki bölümde açıklandığı gibi Hello World modülü iletileri beş saniyede bir günlükçü modülüne doğrudan iletmez.</span><span class="sxs-lookup"><span data-stu-id="618c9-117">As described in the previous section, the Hello World module does not pass messages directly to the logger module every five seconds.</span></span> <span data-ttu-id="618c9-118">Bunun yerine, beş saniyede bir aracıya bir ileti yayımlar.</span><span class="sxs-lookup"><span data-stu-id="618c9-118">Instead, it publishes a message to the broker every five seconds.</span></span>

<span data-ttu-id="618c9-119">Günlükçü modülü aracıdan iletiyi alır ve buna göre davranırken iletinin içeriğini bir dosyaya yazar.</span><span class="sxs-lookup"><span data-stu-id="618c9-119">The logger module receives the message from the broker and acts upon it, writing the contents of the message to a file.</span></span>

<span data-ttu-id="618c9-120">Günlükçü modülü yalnızca aracıdan gelen iletileri kullanır, aracıya hiçbir zaman yeni ileti yayımlamaz.</span><span class="sxs-lookup"><span data-stu-id="618c9-120">The logger module only consumes messages from the broker, it never publishes new messages to the broker.</span></span>

![Aracının Azure IoT Edge’deki modüller arasında iletileri yönlendirme yöntemi][5]

<span data-ttu-id="618c9-122">Yukarıdaki şekilde Hello World örneğinin mimarisi ve örneğin farklı kısımlarını [depoda][lnk-iot-edge] kullanan kaynak dosyalarının ilgili yolları gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="618c9-122">The figure above shows the architecture of the Hello World sample and the relative paths to the source files that implement different portions of the sample in the [repository][lnk-iot-edge].</span></span> <span data-ttu-id="618c9-123">Kodu kendiniz keşfedin veya kılavuz olarak aşağıdaki kod parçacıklarından birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="618c9-123">Explore the code on your own, or use the code snippets below as a guide.</span></span>

<!-- Images -->
[4]: media/iot-hub-iot-edge-getstarted-selector/high_level_architecture.png
[5]: media/iot-hub-iot-edge-getstarted-selector/detailed_architecture.png

<!-- Links -->
[lnk-helloworld-sample]: https://github.com/Azure/iot-edge/tree/master/samples/hello_world
[lnk-iot-edge]: https://github.com/Azure/iot-edge
[lnk-edge-concepts]: ../articles/iot-hub/iot-hub-iot-edge-overview.md