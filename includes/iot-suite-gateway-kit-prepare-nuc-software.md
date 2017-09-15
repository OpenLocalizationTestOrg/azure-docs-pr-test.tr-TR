## <a name="build-iot-edge"></a><span data-ttu-id="1f126-101">IOT kenar derleme</span><span class="sxs-lookup"><span data-stu-id="1f126-101">Build IoT Edge</span></span>

<span data-ttu-id="1f126-102">Bu öğretici özel IOT kenar modüller Uzaktan izleme önceden yapılandırılmış çözümü ile iletişim kurmak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="1f126-102">This tutorial uses custom IoT Edge modules to communicate with the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="1f126-103">Bu nedenle, özel kaynak kodu modüllerden IOT kenar yapı gerekir.</span><span class="sxs-lookup"><span data-stu-id="1f126-103">Therefore, you need to build the IoT Edge modules from custom source code.</span></span> <span data-ttu-id="1f126-104">Aşağıdaki bölümlerde IOT kenar yüklemek ve özel IOT kenar modülü oluşturmak nasıl açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="1f126-104">The following sections describe how to install IoT Edge and build the custom IoT Edge module.</span></span>

### <a name="install-iot-edge"></a><span data-ttu-id="1f126-105">IOT kenar yükleyin</span><span class="sxs-lookup"><span data-stu-id="1f126-105">Install IoT Edge</span></span>

<span data-ttu-id="1f126-106">Aşağıdaki adımlar, Intel NUC üzerinde önceden derlenmiş IOT kenar yazılımı yüklemek açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="1f126-106">The following steps describe how to install the pre-compiled IoT Edge software on the Intel NUC:</span></span>

1. <span data-ttu-id="1f126-107">Gerekli akıllı paket depoları Intel NUC üzerinde aşağıdaki komutları çalıştırarak yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="1f126-107">Configure the required smart package repositories by running the following commands on the Intel NUC:</span></span>

    ```bash
    smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
    smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
    ```

    <span data-ttu-id="1f126-108">Girin `y` zaman komutu ister **bu kanal içerir?**.</span><span class="sxs-lookup"><span data-stu-id="1f126-108">Enter `y` when the command prompts you to **Include this channel?**.</span></span>

1. <span data-ttu-id="1f126-109">Aşağıdaki komutu çalıştırarak akıllı Paket Yöneticisi güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="1f126-109">Update the smart package manager by running the following command:</span></span>

    ```bash
    smart update
    ```

1. <span data-ttu-id="1f126-110">Azure IOT kenar paket, aşağıdaki komutu çalıştırarak yükleyin:</span><span class="sxs-lookup"><span data-stu-id="1f126-110">Install the Azure IoT Edge package by running the following command:</span></span>

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```

1. <span data-ttu-id="1f126-111">"Hello world" örnek çalıştırarak yüklemeyi doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="1f126-111">Verify the installation by running the "Hello world" sample.</span></span> <span data-ttu-id="1f126-112">Bu örnek bir hello world iletisini her beş saniyede log.txT dosyasına yazar.</span><span class="sxs-lookup"><span data-stu-id="1f126-112">This sample writes a hello world message to the log.txT file every five seconds.</span></span> <span data-ttu-id="1f126-113">"Hello world" örnek aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="1f126-113">The following commands run the "Hello world" sample:</span></span>

    ```bash
    cd /usr/share/azureiotgatewaysdk/samples/hello_world/
    ./hello_world hello_world.json
    ```

    <span data-ttu-id="1f126-114">Yoksay **geçersiz bağımsız değişken** örnek durdurduğunuzda iletileri.</span><span class="sxs-lookup"><span data-stu-id="1f126-114">Ignore any **invalid argument** messages when you stop the sample.</span></span>

    <span data-ttu-id="1f126-115">Günlük dosyasının içeriğini görüntülemek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="1f126-115">Use the following command to view the contents of the log file:</span></span>

    ```bash
    cat log.txt | more
    ```

### <a name="troubleshooting"></a><span data-ttu-id="1f126-116">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="1f126-116">Troubleshooting</span></span>

<span data-ttu-id="1f126-117">"Hiçbir paket kul linux geliştirme sağlar" hatasını alırsanız, Intel NUC yeniden başlatmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="1f126-117">If you receive the error "No package provides util-linux-dev", try rebooting the Intel NUC.</span></span>
