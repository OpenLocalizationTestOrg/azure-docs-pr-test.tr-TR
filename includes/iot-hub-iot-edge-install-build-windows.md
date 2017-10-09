## <a name="install-hello-prerequisites"></a><span data-ttu-id="2583f-101">Merhaba Önkoşulları Yükleme</span><span class="sxs-lookup"><span data-stu-id="2583f-101">Install hello prerequisites</span></span>

1. <span data-ttu-id="2583f-102">Yükleme [Visual Studio 2015 veya 2017](https://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="2583f-102">Install [Visual Studio 2015 or 2017](https://www.visualstudio.com).</span></span> <span data-ttu-id="2583f-103">Merhaba kullanabilirsiniz hello lisans gereksinimlerini karşılıyorsa Community Edition boş.</span><span class="sxs-lookup"><span data-stu-id="2583f-103">You can use hello free Community Edition if you meet hello licensing requirements.</span></span> <span data-ttu-id="2583f-104">Visual C++ emin tooinclude ve NuGet Paket Yöneticisi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="2583f-104">Be sure tooinclude Visual C++ and NuGet Package Manager.</span></span>

1. <span data-ttu-id="2583f-105">Yükleme [git](http://www.git-scm.com) ve git.exe hello komut satırından çalıştırabilir emin olun.</span><span class="sxs-lookup"><span data-stu-id="2583f-105">Install [git](http://www.git-scm.com) and make sure you can run git.exe from hello command line.</span></span>

1. <span data-ttu-id="2583f-106">Yükleme [CMake](https://cmake.org/download/) ve cmake.exe hello komut satırından çalıştırabilir emin olun.</span><span class="sxs-lookup"><span data-stu-id="2583f-106">Install [CMake](https://cmake.org/download/) and make sure you can run cmake.exe from hello command line.</span></span> <span data-ttu-id="2583f-107">CMake sürüm 3.7.2 veya üzeri önerilir.</span><span class="sxs-lookup"><span data-stu-id="2583f-107">CMake version 3.7.2 or later is recommended.</span></span> <span data-ttu-id="2583f-108">Merhaba **.msi** yükleyicisi, Windows hello kolay seçeneği bulunur.</span><span class="sxs-lookup"><span data-stu-id="2583f-108">hello **.msi** installer is hello easiest option on Windows.</span></span> <span data-ttu-id="2583f-109">CMake toohello eklemek için yol hello yükleyici istediğinde geçerli kullanıcının en az hello.</span><span class="sxs-lookup"><span data-stu-id="2583f-109">Add CMake toohello PATH for at least hello current user when hello installer prompts you.</span></span>

1. <span data-ttu-id="2583f-110">Yükleme [Python 2.7](https://www.python.org/downloads/release/python-27).</span><span class="sxs-lookup"><span data-stu-id="2583f-110">Install [Python 2.7](https://www.python.org/downloads/release/python-27).</span></span> <span data-ttu-id="2583f-111">Python tooyour eklediğinizden emin olun `PATH` ortam değişkeninde **Denetim Masası -> Sistem -> Gelişmiş Sistem Ayarları -> ortam değişkenleri**.</span><span class="sxs-lookup"><span data-stu-id="2583f-111">Make sure you add Python tooyour `PATH` environment variable in **Control Panel -> System -> Advanced system settings -> Environment Variables**.</span></span>

1. <span data-ttu-id="2583f-112">Bir komut isteminde, aşağıdaki komut tooclone hello Azure IOT kenar GitHub depo tooyour yerel makine hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="2583f-112">At a command prompt, run hello following command tooclone hello Azure IoT Edge GitHub repository tooyour local machine:</span></span>

    ```cmd
    git clone https://github.com/Azure/iot-edge.git
    ```

## <a name="how-toobuild-hello-sample"></a><span data-ttu-id="2583f-113">Nasıl toobuild hello örnek</span><span class="sxs-lookup"><span data-stu-id="2583f-113">How toobuild hello sample</span></span>

<span data-ttu-id="2583f-114">Artık hello IOT kenar çalışma zamanı ve örnekleri yerel makinenizde oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2583f-114">You can now build hello IoT Edge runtime and samples on your local machine:</span></span>

1. <span data-ttu-id="2583f-115">Açık bir **VS 2015 için geliştirici komut istemi** veya **VS 2017 için geliştirici komut istemi** komut istemi.</span><span class="sxs-lookup"><span data-stu-id="2583f-115">Open a **Developer Command Prompt for VS 2015** or **Developer Command Prompt for VS 2017** command prompt.</span></span>

1. <span data-ttu-id="2583f-116">Merhaba yerel kopyasını toohello kök klasörüne gidin **IOT kenar** deposu.</span><span class="sxs-lookup"><span data-stu-id="2583f-116">Navigate toohello root folder in your local copy of hello **iot-edge** repository.</span></span>

1. <span data-ttu-id="2583f-117">Yapı betiği aşağıdaki gibi çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="2583f-117">Run the build script as follows:</span></span>

    ```cmd
    tools\build.cmd --disable-native-remote-modules
    ```

<span data-ttu-id="2583f-118">Bu komut dosyasını bir Visual Studio çözümü dosyası oluşturur ve hello çözüm oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2583f-118">This script creates a Visual Studio solution file and builds hello solution.</span></span> <span data-ttu-id="2583f-119">Hello hello Visual Studio çözüm bulabilirsiniz **yapı** hello yerel kopyasını klasöründe **IOT kenar** deposu.</span><span class="sxs-lookup"><span data-stu-id="2583f-119">You can find hello Visual Studio solution in hello **build** folder in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="2583f-120">Toobuild istiyorsanız ve hello birim testleri çalıştırma hello eklemek `--run-unittests` parametresi.</span><span class="sxs-lookup"><span data-stu-id="2583f-120">If you want toobuild and run hello unit tests, add hello `--run-unittests` parameter.</span></span> <span data-ttu-id="2583f-121">Toobuild istiyorsanız ve hello son tooend testler hello eklemek `--run-e2e-tests`.</span><span class="sxs-lookup"><span data-stu-id="2583f-121">If you want toobuild and run hello end tooend tests, add hello `--run-e2e-tests`.</span></span>

> [!NOTE]
> <span data-ttu-id="2583f-122">Merhaba her çalıştırdığınızda **build.cmd** komut dosyası, siler ve sonra da hello yeniden oluşturur **yapı** hello yerel kopyasını hello kök klasöründe klasöründe **IOT kenar** deposu.</span><span class="sxs-lookup"><span data-stu-id="2583f-122">Every time you run hello **build.cmd** script, it deletes and then recreates hello **build** folder in hello root folder of your local copy of hello **iot-edge** repository.</span></span>
