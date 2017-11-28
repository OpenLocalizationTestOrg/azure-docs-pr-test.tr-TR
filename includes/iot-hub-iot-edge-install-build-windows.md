## <a name="install-the-prerequisites"></a><span data-ttu-id="d5bae-101">Yükleme önkoşulları</span><span class="sxs-lookup"><span data-stu-id="d5bae-101">Install the prerequisites</span></span>

1. <span data-ttu-id="d5bae-102">Yükleme [Visual Studio 2015 veya 2017](https://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="d5bae-102">Install [Visual Studio 2015 or 2017](https://www.visualstudio.com).</span></span> <span data-ttu-id="d5bae-103">Lisans gereksinimlerini karşılıyorsa, ücretsiz Community sürümü kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d5bae-103">You can use the free Community Edition if you meet the licensing requirements.</span></span> <span data-ttu-id="d5bae-104">Visual C++ ve NuGet Paket Yöneticisi eklediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="d5bae-104">Be sure to include Visual C++ and NuGet Package Manager.</span></span>

1. <span data-ttu-id="d5bae-105">Yükleme [git](http://www.git-scm.com) ve git.exe komut satırından çalıştırabilir emin olun.</span><span class="sxs-lookup"><span data-stu-id="d5bae-105">Install [git](http://www.git-scm.com) and make sure you can run git.exe from the command line.</span></span>

1. <span data-ttu-id="d5bae-106">Yükleme [CMake](https://cmake.org/download/) ve cmake.exe komut satırından çalıştırabilir emin olun.</span><span class="sxs-lookup"><span data-stu-id="d5bae-106">Install [CMake](https://cmake.org/download/) and make sure you can run cmake.exe from the command line.</span></span> <span data-ttu-id="d5bae-107">CMake sürüm 3.7.2 veya üzeri önerilir.</span><span class="sxs-lookup"><span data-stu-id="d5bae-107">CMake version 3.7.2 or later is recommended.</span></span> <span data-ttu-id="d5bae-108">**.Msi** yükleyicisi, Windows'da kolay seçeneği bulunur.</span><span class="sxs-lookup"><span data-stu-id="d5bae-108">The **.msi** installer is the easiest option on Windows.</span></span> <span data-ttu-id="d5bae-109">En az CMake yolu Ekle yükleyici istediğinde geçerli kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="d5bae-109">Add CMake to the PATH for at least the current user when the installer prompts you.</span></span>

1. <span data-ttu-id="d5bae-110">Yükleme [Python 2.7](https://www.python.org/downloads/release/python-27).</span><span class="sxs-lookup"><span data-stu-id="d5bae-110">Install [Python 2.7](https://www.python.org/downloads/release/python-27).</span></span> <span data-ttu-id="d5bae-111">Python için eklemenize emin olun, `PATH` ortam değişkeninde **Denetim Masası -> Sistem -> Gelişmiş Sistem Ayarları -> ortam değişkenleri**.</span><span class="sxs-lookup"><span data-stu-id="d5bae-111">Make sure you add Python to your `PATH` environment variable in **Control Panel -> System -> Advanced system settings -> Environment Variables**.</span></span>

1. <span data-ttu-id="d5bae-112">Bir komut isteminde yerel makinenize Azure IOT kenar GitHub deposuna kopyalamak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="d5bae-112">At a command prompt, run the following command to clone the Azure IoT Edge GitHub repository to your local machine:</span></span>

    ```cmd
    git clone https://github.com/Azure/iot-edge.git
    ```

## <a name="how-to-build-the-sample"></a><span data-ttu-id="d5bae-113">Örnek oluşturma</span><span class="sxs-lookup"><span data-stu-id="d5bae-113">How to build the sample</span></span>

<span data-ttu-id="d5bae-114">Artık IOT kenar çalışma zamanı ve örnekleri yerel makinenizde oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d5bae-114">You can now build the IoT Edge runtime and samples on your local machine:</span></span>

1. <span data-ttu-id="d5bae-115">Açık bir **VS 2015 için geliştirici komut istemi** veya **VS 2017 için geliştirici komut istemi** komut istemi.</span><span class="sxs-lookup"><span data-stu-id="d5bae-115">Open a **Developer Command Prompt for VS 2015** or **Developer Command Prompt for VS 2017** command prompt.</span></span>

1. <span data-ttu-id="d5bae-116">**iot-edge** deposunun yerel kopyasındaki kök klasöre gidin.</span><span class="sxs-lookup"><span data-stu-id="d5bae-116">Navigate to the root folder in your local copy of the **iot-edge** repository.</span></span>

1. <span data-ttu-id="d5bae-117">Yapı betiği aşağıdaki gibi çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="d5bae-117">Run the build script as follows:</span></span>

    ```cmd
    tools\build.cmd --disable-native-remote-modules
    ```

<span data-ttu-id="d5bae-118">Bu komut dosyasını bir Visual Studio çözümü dosyası oluşturur ve çözüm oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d5bae-118">This script creates a Visual Studio solution file and builds the solution.</span></span> <span data-ttu-id="d5bae-119">Visual Studio çözümünde bulabilirsiniz **yapı** yerel kopyasını klasöründe **IOT kenar** deposu.</span><span class="sxs-lookup"><span data-stu-id="d5bae-119">You can find the Visual Studio solution in the **build** folder in your local copy of the **iot-edge** repository.</span></span> <span data-ttu-id="d5bae-120">İstiyorsanız derleme ve birim testleri çalıştırma, ekleme `--run-unittests` parametresi.</span><span class="sxs-lookup"><span data-stu-id="d5bae-120">If you want to build and run the unit tests, add the `--run-unittests` parameter.</span></span> <span data-ttu-id="d5bae-121">Derleme ve uçtan uca testler, eklemek istiyorsanız, `--run-e2e-tests`.</span><span class="sxs-lookup"><span data-stu-id="d5bae-121">If you want to build and run the end to end tests, add the `--run-e2e-tests`.</span></span>

> [!NOTE]
> <span data-ttu-id="d5bae-122">Her çalıştırdığınızda **build.cmd** komut dosyası, onu siler ve sonra yeniden oluşturur **yapı** klasörü kök klasöründe yerel kopyasının **IOT kenar** deposu.</span><span class="sxs-lookup"><span data-stu-id="d5bae-122">Every time you run the **build.cmd** script, it deletes and then recreates the **build** folder in the root folder of your local copy of the **iot-edge** repository.</span></span>