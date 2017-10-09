## <a name="build-iot-edge"></a><span data-ttu-id="3d050-101">IOT kenar derleme</span><span class="sxs-lookup"><span data-stu-id="3d050-101">Build IoT Edge</span></span>

<span data-ttu-id="3d050-102">Bu öğretici hello Uzaktan izleme çözümü ile özel IOT kenar modülleri toocommunicate kullanır.</span><span class="sxs-lookup"><span data-stu-id="3d050-102">This tutorial uses custom IoT Edge modules toocommunicate with hello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="3d050-103">Bu nedenle, özel kaynak kodu toobuild hello IOT kenar modüllerden gerekir.</span><span class="sxs-lookup"><span data-stu-id="3d050-103">Therefore, you need toobuild hello IoT Edge modules from custom source code.</span></span> <span data-ttu-id="3d050-104">Aşağıdaki bölümlerde hello nasıl tooinstall IOT kenarı ve yapı özel IOT kenar modülü hello açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="3d050-104">hello following sections describe how tooinstall IoT Edge and build hello custom IoT Edge module.</span></span>

### <a name="install-iot-edge"></a><span data-ttu-id="3d050-105">IOT kenar yükleyin</span><span class="sxs-lookup"><span data-stu-id="3d050-105">Install IoT Edge</span></span>

<span data-ttu-id="3d050-106">Merhaba aşağıdaki adımlar nasıl tooinstall hello hello Intel NUC IOT kenar yazılımı önceden derlenmiş açıklamaktadır:</span><span class="sxs-lookup"><span data-stu-id="3d050-106">hello following steps describe how tooinstall hello pre-compiled IoT Edge software on hello Intel NUC:</span></span>

1. <span data-ttu-id="3d050-107">Gerekli hello akıllı paketi depoları komutları Intel NUC hello üzerinde aşağıdaki hello çalıştırarak yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="3d050-107">Configure hello required smart package repositories by running hello following commands on hello Intel NUC:</span></span>

    ```bash
    smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
    smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
    ```

    <span data-ttu-id="3d050-108">Girin `y` zaman hello komut sizden çok**bu kanal içerir?**.</span><span class="sxs-lookup"><span data-stu-id="3d050-108">Enter `y` when hello command prompts you too**Include this channel?**.</span></span>

1. <span data-ttu-id="3d050-109">Merhaba akıllı Paket Yöneticisi hello aşağıdaki komutu çalıştırarak güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="3d050-109">Update hello smart package manager by running hello following command:</span></span>

    ```bash
    smart update
    ```

1. <span data-ttu-id="3d050-110">Merhaba aşağıdaki komutu çalıştırarak Hello Azure IOT kenar paketini yükle:</span><span class="sxs-lookup"><span data-stu-id="3d050-110">Install hello Azure IoT Edge package by running hello following command:</span></span>

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```

1. <span data-ttu-id="3d050-111">Merhaba yükleme tarafından çalışan hello "Hello world" örnek doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="3d050-111">Verify hello installation by running hello "Hello world" sample.</span></span> <span data-ttu-id="3d050-112">Bu örnek, beş saniyede bir hello world ileti toohello log.txT dosyası yazar.</span><span class="sxs-lookup"><span data-stu-id="3d050-112">This sample writes a hello world message toohello log.txT file every five seconds.</span></span> <span data-ttu-id="3d050-113">Merhaba aşağıdaki komutları hello "Hello world" örnek çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="3d050-113">hello following commands run hello "Hello world" sample:</span></span>

    ```bash
    cd /usr/share/azureiotgatewaysdk/samples/hello_world/
    ./hello_world hello_world.json
    ```

    <span data-ttu-id="3d050-114">Yoksay **geçersiz bağımsız değişken** hello örnek durdurduğunuzda iletileri.</span><span class="sxs-lookup"><span data-stu-id="3d050-114">Ignore any **invalid argument** messages when you stop hello sample.</span></span>

    <span data-ttu-id="3d050-115">Komut tooview hello hello günlük dosyasının içeriğini aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="3d050-115">Use hello following command tooview hello contents of hello log file:</span></span>

    ```bash
    cat log.txt | more
    ```

### <a name="troubleshooting"></a><span data-ttu-id="3d050-116">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="3d050-116">Troubleshooting</span></span>

<span data-ttu-id="3d050-117">Merhaba hata alırsanız, "hiçbir paket kul linux geliştirme sağlar.", hello Intel NUC yeniden başlatmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="3d050-117">If you receive hello error "No package provides util-linux-dev", try rebooting hello Intel NUC.</span></span>
