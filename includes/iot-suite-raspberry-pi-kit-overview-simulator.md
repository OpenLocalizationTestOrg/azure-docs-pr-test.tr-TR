## <a name="overview"></a><span data-ttu-id="8508a-101">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="8508a-101">Overview</span></span>

<span data-ttu-id="8508a-102">Bu öğreticide, hello aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="8508a-102">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="8508a-103">Merhaba Uzaktan izleme önceden yapılandırılmış çözüm tooyour Azure aboneliği örneği dağıtın.</span><span class="sxs-lookup"><span data-stu-id="8508a-103">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="8508a-104">Bu adım, otomatik olarak dağıtır ve birden çok Azure hizmetlerini yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="8508a-104">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="8508a-105">Bilgisayarınız ve hello Uzaktan izleme çözümü ile cihaz toocommunicate ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="8508a-105">Set up your device toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="8508a-106">Merhaba örnek aygıt kodu tooconnect toohello Uzaktan izleme çözümü güncelleştirmek ve hello çözüm panosunda görüntüleyebilirsiniz sanal telemetriyi gönderin.</span><span class="sxs-lookup"><span data-stu-id="8508a-106">Update hello sample device code tooconnect toohello remote monitoring solution, and send simulated telemetry that you can view on hello solution dashboard.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8508a-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8508a-107">Prerequisites</span></span>

<span data-ttu-id="8508a-108">toocomplete Bu öğreticide, bir etkin Azure aboneliği gerekir.</span><span class="sxs-lookup"><span data-stu-id="8508a-108">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="8508a-109">Hesabınız yoksa yalnızca birkaç dakika içinde ücretsiz bir deneme sürümü hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8508a-109">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="8508a-110">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="8508a-110">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

### <a name="required-software"></a><span data-ttu-id="8508a-111">Gerekli yazılım</span><span class="sxs-lookup"><span data-stu-id="8508a-111">Required software</span></span>

<span data-ttu-id="8508a-112">Tooremotely erişim hello komut satırı Raspberry Pi'yi hello üzerinde Masaüstü makine tooenable üzerinde SSH istemcisi gerekir.</span><span class="sxs-lookup"><span data-stu-id="8508a-112">You need SSH client on your desktop machine tooenable you tooremotely access hello command line on hello Raspberry Pi.</span></span>

- <span data-ttu-id="8508a-113">Windows, bir SSH istemcisi içermez.</span><span class="sxs-lookup"><span data-stu-id="8508a-113">Windows does not include an SSH client.</span></span> <span data-ttu-id="8508a-114">Kullanmanızı öneririz [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="8508a-114">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="8508a-115">Çoğu Linux dağıtımları ve Mac OS komut satırı SSH yardımcı programını hello içerir.</span><span class="sxs-lookup"><span data-stu-id="8508a-115">Most Linux distributions and Mac OS include hello command-line SSH utility.</span></span> <span data-ttu-id="8508a-116">Daha fazla bilgi için bkz: [SSH kullanarak Linux veya Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span><span class="sxs-lookup"><span data-stu-id="8508a-116">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

### <a name="required-hardware"></a><span data-ttu-id="8508a-117">Gerekli donanım</span><span class="sxs-lookup"><span data-stu-id="8508a-117">Required hardware</span></span>

<span data-ttu-id="8508a-118">Bir masaüstü bilgisayar tooenable, tooconnect uzaktan toohello komut satırı Raspberry Pi'yi hello üzerinde.</span><span class="sxs-lookup"><span data-stu-id="8508a-118">A desktop computer tooenable you tooconnect remotely toohello command line on hello Raspberry Pi.</span></span>

<span data-ttu-id="8508a-119">[Microsoft IOT Starter Kit Raspberry Pi 3] [ lnk-starter-kits] veya eşdeğer bileşenleri.</span><span class="sxs-lookup"><span data-stu-id="8508a-119">[Microsoft IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] or equivalent components.</span></span> <span data-ttu-id="8508a-120">Bu öğretici aşağıdaki hello Seti'nden öğelerindeki hello kullanır:</span><span class="sxs-lookup"><span data-stu-id="8508a-120">This tutorial uses hello following items from hello kit:</span></span>

- <span data-ttu-id="8508a-121">Böğürtlenli Pi 3</span><span class="sxs-lookup"><span data-stu-id="8508a-121">Raspberry Pi 3</span></span>
- <span data-ttu-id="8508a-122">MicroSD kartı (ile NOOBS)</span><span class="sxs-lookup"><span data-stu-id="8508a-122">MicroSD Card (with NOOBS)</span></span>
- <span data-ttu-id="8508a-123">Bir USB Mini kablosu</span><span class="sxs-lookup"><span data-stu-id="8508a-123">A USB Mini cable</span></span>
- <span data-ttu-id="8508a-124">Ethernet kablosu</span><span class="sxs-lookup"><span data-stu-id="8508a-124">An Ethernet cable</span></span>

[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/