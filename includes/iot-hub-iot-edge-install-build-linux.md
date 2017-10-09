## <a name="install-hello-prerequisites"></a><span data-ttu-id="8e2ba-101">Merhaba Önkoşulları Yükleme</span><span class="sxs-lookup"><span data-stu-id="8e2ba-101">Install hello prerequisites</span></span>

<span data-ttu-id="8e2ba-102">Bu öğreticide Hello adımları Ubuntu Linux çalıştıran varsayalım.</span><span class="sxs-lookup"><span data-stu-id="8e2ba-102">hello steps in this tutorial assume you are running Ubuntu Linux.</span></span>

<span data-ttu-id="8e2ba-103">Bir Kabuğu'nu açın ve aşağıdaki komutları tooinstall hello önkoşul hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="8e2ba-103">Open a shell and run hello following commands tooinstall hello prerequisite packages:</span></span>

```bash
sudo apt-get update
sudo apt-get install curl build-essential libcurl4-openssl-dev git cmake libssl-dev uuid-dev valgrind libglib2.0-dev libtool autoconf
```

<span data-ttu-id="8e2ba-104">Merhaba Kabuğu'nda komutu tooclone hello Azure IOT kenar GitHub depo tooyour yerel makine aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="8e2ba-104">In hello shell, run hello following command tooclone hello Azure IoT Edge GitHub repository tooyour local machine:</span></span>

```bash
git clone https://github.com/Azure/iot-edge.git
```

## <a name="how-toobuild-hello-sample"></a><span data-ttu-id="8e2ba-105">Nasıl toobuild hello örnek</span><span class="sxs-lookup"><span data-stu-id="8e2ba-105">How toobuild hello sample</span></span>

<span data-ttu-id="8e2ba-106">Artık hello IOT kenar çalışma zamanı ve örnekleri yerel makinenizde oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8e2ba-106">You can now build hello IoT Edge runtime and samples on your local machine:</span></span>

1. <span data-ttu-id="8e2ba-107">Bir kabuk açın.</span><span class="sxs-lookup"><span data-stu-id="8e2ba-107">Open a shell.</span></span>

1. <span data-ttu-id="8e2ba-108">Merhaba yerel kopyasını toohello kök klasörüne gidin **IOT kenar** deposu.</span><span class="sxs-lookup"><span data-stu-id="8e2ba-108">Navigate toohello root folder in your local copy of hello **iot-edge** repository.</span></span>

1. <span data-ttu-id="8e2ba-109">Yapı betiği aşağıdaki gibi çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="8e2ba-109">Run the build script as follows:</span></span>

    ```sh
    tools/build.sh --disable-native-remote-modules
    ```

<span data-ttu-id="8e2ba-110">Bu komut dosyası kullanır **cmake** yardımcı programı toocreate adlı bir klasör **yapı** hello kök klasöründe yerel kopyasını **IOT kenar** depo ve derleme görevleri dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8e2ba-110">This script uses the **cmake** utility toocreate a folder called **build** in hello root folder of your local copy of the **iot-edge** repository and generate a makefile.</span></span> <span data-ttu-id="8e2ba-111">Merhaba betik sonra birim testleri ve son tooend testleri atlanıyor hello çözüm oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8e2ba-111">hello script then builds hello solution, skipping unit tests and end tooend tests.</span></span> <span data-ttu-id="8e2ba-112">Toobuild istiyorsanız ve hello birim testleri çalıştırma hello eklemek `--run-unittests` parametresi.</span><span class="sxs-lookup"><span data-stu-id="8e2ba-112">If you want toobuild and run hello unit tests, add hello `--run-unittests` parameter.</span></span> <span data-ttu-id="8e2ba-113">Toobuild istiyorsanız ve hello son tooend testler hello eklemek `--run-e2e-tests`.</span><span class="sxs-lookup"><span data-stu-id="8e2ba-113">If you want toobuild and run hello end tooend tests, add hello `--run-e2e-tests`.</span></span>

> [!NOTE]
> <span data-ttu-id="8e2ba-114">Merhaba her çalıştırdığınızda **build.sh** komut dosyası, siler ve sonra da hello yeniden oluşturur **yapı** hello yerel kopyasını hello kök klasöründe klasöründe **IOT kenar** deposu.</span><span class="sxs-lookup"><span data-stu-id="8e2ba-114">Every time you run hello **build.sh** script, it deletes and then recreates hello **build** folder in hello root folder of your local copy of hello **iot-edge** repository.</span></span>
