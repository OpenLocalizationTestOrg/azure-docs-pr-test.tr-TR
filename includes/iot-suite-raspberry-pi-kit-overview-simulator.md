## <a name="overview"></a><span data-ttu-id="34f86-101">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="34f86-101">Overview</span></span>

<span data-ttu-id="34f86-102">Bu öğreticide, aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="34f86-102">In this tutorial, you complete the following steps:</span></span>

- <span data-ttu-id="34f86-103">Önceden yapılandırılmış Uzaktan izleme çözümü örneği Azure aboneliğinize dağıtın.</span><span class="sxs-lookup"><span data-stu-id="34f86-103">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span></span> <span data-ttu-id="34f86-104">Bu adım, otomatik olarak dağıtır ve birden çok Azure hizmetlerini yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="34f86-104">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="34f86-105">Bilgisayarınız ve Uzaktan izleme çözümü ile iletişim kurmak için aygıtınızı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="34f86-105">Set up your device to communicate with your computer and the remote monitoring solution.</span></span>
- <span data-ttu-id="34f86-106">Uzaktan izleme çözümüne bağlama için örnek aygıt kodunu güncelleştirin ve çözüm panosunda görüntüleyebilirsiniz sanal telemetriyi gönderin.</span><span class="sxs-lookup"><span data-stu-id="34f86-106">Update the sample device code to connect to the remote monitoring solution, and send simulated telemetry that you can view on the solution dashboard.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="34f86-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="34f86-107">Prerequisites</span></span>

<span data-ttu-id="34f86-108">Bu öğreticiyi tamamlamak için etkin bir Azure aboneliğinizin olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="34f86-108">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="34f86-109">Hesabınız yoksa yalnızca birkaç dakika içinde ücretsiz bir deneme sürümü hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34f86-109">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="34f86-110">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="34f86-110">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

### <a name="required-software"></a><span data-ttu-id="34f86-111">Gerekli yazılım</span><span class="sxs-lookup"><span data-stu-id="34f86-111">Required software</span></span>

<span data-ttu-id="34f86-112">Komut satırı Raspberry Pi'yi üzerinde uzaktan erişim sağlamak için Masaüstü makinenizde SSH istemcisi gerekir.</span><span class="sxs-lookup"><span data-stu-id="34f86-112">You need SSH client on your desktop machine to enable you to remotely access the command line on the Raspberry Pi.</span></span>

- <span data-ttu-id="34f86-113">Windows, bir SSH istemcisi içermez.</span><span class="sxs-lookup"><span data-stu-id="34f86-113">Windows does not include an SSH client.</span></span> <span data-ttu-id="34f86-114">Kullanmanızı öneririz [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="34f86-114">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="34f86-115">Çoğu Linux dağıtımları ve Mac OS komut satırı SSH yardımcı programı içerir.</span><span class="sxs-lookup"><span data-stu-id="34f86-115">Most Linux distributions and Mac OS include the command-line SSH utility.</span></span> <span data-ttu-id="34f86-116">Daha fazla bilgi için bkz: [SSH kullanarak Linux veya Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span><span class="sxs-lookup"><span data-stu-id="34f86-116">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

### <a name="required-hardware"></a><span data-ttu-id="34f86-117">Gerekli donanım</span><span class="sxs-lookup"><span data-stu-id="34f86-117">Required hardware</span></span>

<span data-ttu-id="34f86-118">Komut satırı Raspberry Pi'yi üzerinde uzaktan bağlanmak etkinleştirmek için bir masaüstü bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="34f86-118">A desktop computer to enable you to connect remotely to the command line on the Raspberry Pi.</span></span>

<span data-ttu-id="34f86-119">[Microsoft IOT Starter Kit Raspberry Pi 3] [ lnk-starter-kits] veya eşdeğer bileşenleri.</span><span class="sxs-lookup"><span data-stu-id="34f86-119">[Microsoft IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] or equivalent components.</span></span> <span data-ttu-id="34f86-120">Bu öğretici Seti'nden aşağıdaki öğeleri kullanır:</span><span class="sxs-lookup"><span data-stu-id="34f86-120">This tutorial uses the following items from the kit:</span></span>

- <span data-ttu-id="34f86-121">Böğürtlenli Pi 3</span><span class="sxs-lookup"><span data-stu-id="34f86-121">Raspberry Pi 3</span></span>
- <span data-ttu-id="34f86-122">MicroSD kartı (ile NOOBS)</span><span class="sxs-lookup"><span data-stu-id="34f86-122">MicroSD Card (with NOOBS)</span></span>
- <span data-ttu-id="34f86-123">Bir USB Mini kablosu</span><span class="sxs-lookup"><span data-stu-id="34f86-123">A USB Mini cable</span></span>
- <span data-ttu-id="34f86-124">Ethernet kablosu</span><span class="sxs-lookup"><span data-stu-id="34f86-124">An Ethernet cable</span></span>

[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/