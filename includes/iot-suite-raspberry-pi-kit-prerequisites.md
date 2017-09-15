## <a name="prerequisites"></a><span data-ttu-id="8efbe-101">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8efbe-101">Prerequisites</span></span>

<span data-ttu-id="8efbe-102">Bu öğreticiyi tamamlamak için etkin bir Azure aboneliğinizin olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8efbe-102">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="8efbe-103">Hesabınız yoksa yalnızca birkaç dakika içinde ücretsiz bir deneme sürümü hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8efbe-103">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="8efbe-104">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="8efbe-104">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

### <a name="required-software"></a><span data-ttu-id="8efbe-105">Gerekli yazılım</span><span class="sxs-lookup"><span data-stu-id="8efbe-105">Required software</span></span>

<span data-ttu-id="8efbe-106">Komut satırı Raspberry Pi'yi üzerinde uzaktan erişim sağlamak için Masaüstü makinenizde SSH istemcisi gerekir.</span><span class="sxs-lookup"><span data-stu-id="8efbe-106">You need SSH client on your desktop machine to enable you to remotely access the command line on the Raspberry Pi.</span></span>

- <span data-ttu-id="8efbe-107">Windows, bir SSH istemcisi içermez.</span><span class="sxs-lookup"><span data-stu-id="8efbe-107">Windows does not include an SSH client.</span></span> <span data-ttu-id="8efbe-108">Kullanmanızı öneririz [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="8efbe-108">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="8efbe-109">Çoğu Linux dağıtımları ve Mac OS komut satırı SSH yardımcı programı içerir.</span><span class="sxs-lookup"><span data-stu-id="8efbe-109">Most Linux distributions and Mac OS include the command-line SSH utility.</span></span> <span data-ttu-id="8efbe-110">Daha fazla bilgi için bkz: [SSH kullanarak Linux veya Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span><span class="sxs-lookup"><span data-stu-id="8efbe-110">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

### <a name="required-hardware"></a><span data-ttu-id="8efbe-111">Gerekli donanım</span><span class="sxs-lookup"><span data-stu-id="8efbe-111">Required hardware</span></span>

<span data-ttu-id="8efbe-112">Komut satırı Raspberry Pi'yi üzerinde uzaktan bağlanmak etkinleştirmek için bir masaüstü bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="8efbe-112">A desktop computer to enable you to connect remotely to the command line on the Raspberry Pi.</span></span>

<span data-ttu-id="8efbe-113">[Microsoft IOT Starter Kit Raspberry Pi 3] [ lnk-starter-kits] veya eşdeğer bileşenleri.</span><span class="sxs-lookup"><span data-stu-id="8efbe-113">[Microsoft IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] or equivalent components.</span></span> <span data-ttu-id="8efbe-114">Bu öğretici Seti'nden aşağıdaki öğeleri kullanır:</span><span class="sxs-lookup"><span data-stu-id="8efbe-114">This tutorial uses the following items from the kit:</span></span>

- <span data-ttu-id="8efbe-115">Böğürtlenli Pi 3</span><span class="sxs-lookup"><span data-stu-id="8efbe-115">Raspberry Pi 3</span></span>
- <span data-ttu-id="8efbe-116">MicroSD kartı (ile NOOBS)</span><span class="sxs-lookup"><span data-stu-id="8efbe-116">MicroSD Card (with NOOBS)</span></span>
- <span data-ttu-id="8efbe-117">Bir USB Mini kablosu</span><span class="sxs-lookup"><span data-stu-id="8efbe-117">A USB Mini cable</span></span>
- <span data-ttu-id="8efbe-118">Ethernet kablosu</span><span class="sxs-lookup"><span data-stu-id="8efbe-118">An Ethernet cable</span></span>
- <span data-ttu-id="8efbe-119">BME280 algılayıcısı</span><span class="sxs-lookup"><span data-stu-id="8efbe-119">BME280 sensor</span></span>
- <span data-ttu-id="8efbe-120">Breadboard</span><span class="sxs-lookup"><span data-stu-id="8efbe-120">Breadboard</span></span>
- <span data-ttu-id="8efbe-121">Anahtar kabloları</span><span class="sxs-lookup"><span data-stu-id="8efbe-121">Jumper wires</span></span>
- <span data-ttu-id="8efbe-122">Rezistanslar</span><span class="sxs-lookup"><span data-stu-id="8efbe-122">Resistors</span></span>
- <span data-ttu-id="8efbe-123">LED'leri</span><span class="sxs-lookup"><span data-stu-id="8efbe-123">LEDs</span></span>

[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/