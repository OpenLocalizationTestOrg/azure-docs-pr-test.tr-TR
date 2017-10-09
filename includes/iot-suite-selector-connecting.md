> [!div class="op_single_selector"]
> * [<span data-ttu-id="d0fe0-101">Windows üzerinde C</span><span class="sxs-lookup"><span data-stu-id="d0fe0-101">C on Windows</span></span>](../articles/iot-suite/iot-suite-connecting-devices.md)
> * [<span data-ttu-id="d0fe0-102">Linux üzerinde C</span><span class="sxs-lookup"><span data-stu-id="d0fe0-102">C on Linux</span></span>](../articles/iot-suite/iot-suite-connecting-devices-linux.md)
> * [<span data-ttu-id="d0fe0-103">Node.js</span><span class="sxs-lookup"><span data-stu-id="d0fe0-103">Node.js</span></span>](../articles/iot-suite/iot-suite-connecting-devices-node.md)
> 
> 

## <a name="scenario-overview"></a><span data-ttu-id="d0fe0-104">Senaryoya genel bakış</span><span class="sxs-lookup"><span data-stu-id="d0fe0-104">Scenario overview</span></span>
<span data-ttu-id="d0fe0-105">Bu senaryoda, telemetri toohello Uzaktan izleme aşağıdaki hello gönderir bir cihaz oluşturma [önceden yapılandırılmış çözüm][lnk-what-are-preconfig-solutions]:</span><span class="sxs-lookup"><span data-stu-id="d0fe0-105">In this scenario, you create a device that sends hello following telemetry toohello remote monitoring [preconfigured solution][lnk-what-are-preconfig-solutions]:</span></span>

* <span data-ttu-id="d0fe0-106">Dış ortam sıcaklığı</span><span class="sxs-lookup"><span data-stu-id="d0fe0-106">External temperature</span></span>
* <span data-ttu-id="d0fe0-107">İç ortam sıcaklığı</span><span class="sxs-lookup"><span data-stu-id="d0fe0-107">Internal temperature</span></span>
* <span data-ttu-id="d0fe0-108">Nem oranı</span><span class="sxs-lookup"><span data-stu-id="d0fe0-108">Humidity</span></span>

<span data-ttu-id="d0fe0-109">Basitleştirmek için örnek değerler hello cihazda hello kodu oluşturur, ancak siz tooextend hello örnek gerçek algılayıcılar tooyour aygıt bağlanma ve gerçek telemetri göndermesini öneririz.</span><span class="sxs-lookup"><span data-stu-id="d0fe0-109">For simplicity, hello code on hello device generates sample values, but we encourage you tooextend hello sample by connecting real sensors tooyour device and sending real telemetry.</span></span>

<span data-ttu-id="d0fe0-110">Merhaba de mümkün toorespond toomethods hello çözüm panodan çağrılır ve özellik değerleri hello çözüm panosunda istenen aygıttır.</span><span class="sxs-lookup"><span data-stu-id="d0fe0-110">hello device is also able toorespond toomethods invoked from hello solution dashboard and desired property values set in hello solution dashboard.</span></span>

<span data-ttu-id="d0fe0-111">toocomplete Bu öğretici, etkin bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0fe0-111">toocomplete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="d0fe0-112">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0fe0-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="d0fe0-113">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="d0fe0-113">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

## <a name="before-you-start"></a><span data-ttu-id="d0fe0-114">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="d0fe0-114">Before you start</span></span>
<span data-ttu-id="d0fe0-115">Cihazınız için kod yazmadan önce, önceden yapılandırılmış uzaktan izleme çözümünüzü ve bu çözümde yeni bir özel cihaz hazırlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0fe0-115">Before you write any code for your device, you must provision your remote monitoring preconfigured solution and provision a new custom device in that solution.</span></span>

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="d0fe0-116">Önceden yapılandırılmış uzaktan izleme çözümünüzü sağlama</span><span class="sxs-lookup"><span data-stu-id="d0fe0-116">Provision your remote monitoring preconfigured solution</span></span>
<span data-ttu-id="d0fe0-117">Bu öğreticide oluşturduğunuz hello cihaz gönderir veri tooan hello örneği [Uzaktan izleme] [ lnk-remote-monitoring] çözüm önceden yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="d0fe0-117">hello device you create in this tutorial sends data tooan instance of hello [remote monitoring][lnk-remote-monitoring] preconfigured solution.</span></span> <span data-ttu-id="d0fe0-118">Uzaktan izleme çözümü Azure hesabınızda hello sağladığınız zaten yapmadıysanız, hello aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="d0fe0-118">If you haven't already provisioned hello remote monitoring preconfigured solution in your Azure account, use hello following steps:</span></span>

1. <span data-ttu-id="d0fe0-119">Merhaba üzerinde <https://www.azureiotsuite.com/> sayfasında,  **+**  toocreate bir çözüm.</span><span class="sxs-lookup"><span data-stu-id="d0fe0-119">On hello <https://www.azureiotsuite.com/> page, click **+** toocreate a solution.</span></span>
2. <span data-ttu-id="d0fe0-120">Tıklatın **seçin** hello üzerinde **Uzaktan izleme** çözümünüzü toocreate panel.</span><span class="sxs-lookup"><span data-stu-id="d0fe0-120">Click **Select** on hello **Remote monitoring** panel toocreate your solution.</span></span>
3. <span data-ttu-id="d0fe0-121">Hello üzerinde **Uzaktan izleme çözümü oluşturma** want bir **çözüm adı** seçiminizi, hello seçin **bölge** toodeploy için istediğiniz ve hello Azure seçin Abonelik toowant toouse.</span><span class="sxs-lookup"><span data-stu-id="d0fe0-121">On hello **Create Remote monitoring solution** page, enter a **Solution name** of your choice, select hello **Region** you want toodeploy to, and select hello Azure subscription toowant toouse.</span></span> <span data-ttu-id="d0fe0-122">Ardından **Çözüm oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d0fe0-122">Then click **Create solution**.</span></span>
4. <span data-ttu-id="d0fe0-123">Merhaba sağlama işlemi tamamlanana kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="d0fe0-123">Wait until hello provisioning process completes.</span></span>

> [!WARNING]
> <span data-ttu-id="d0fe0-124">Merhaba önceden yapılandırılmış çözümleri Faturalanabilir Azure Hizmetleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="d0fe0-124">hello preconfigured solutions use billable Azure services.</span></span> <span data-ttu-id="d0fe0-125">Tooremove hello aboneliğiniz önceden yapılandırılmış çözümü ile bittiğinde mutlaka tooavoid gereksiz herhangi bir ücret.</span><span class="sxs-lookup"><span data-stu-id="d0fe0-125">Be sure tooremove hello preconfigured solution from your subscription when you are done with it tooavoid any unnecessary charges.</span></span> <span data-ttu-id="d0fe0-126">Merhaba ziyaret ederek önceden yapılandırılmış bir çözüm aboneliğinizden tamamen kaldırabilirsiniz <https://www.azureiotsuite.com/> sayfası.</span><span class="sxs-lookup"><span data-stu-id="d0fe0-126">You can completely remove a preconfigured solution from your subscription by visiting hello <https://www.azureiotsuite.com/> page.</span></span>
> 
> 

<span data-ttu-id="d0fe0-127">Sağlama işlemi hello Uzaktan izleme çözümü için hello tamamlandığında, tıklatın **başlatma** tooopen hello çözüm Panosu tarayıcınızda.</span><span class="sxs-lookup"><span data-stu-id="d0fe0-127">When hello provisioning process for hello remote monitoring solution finishes, click **Launch** tooopen hello solution dashboard in your browser.</span></span>

![Çözüm panosu][img-dashboard]

### <a name="provision-your-device-in-hello-remote-monitoring-solution"></a><span data-ttu-id="d0fe0-129">Cihazınızı Uzaktan izleme çözümü hello sağlama</span><span class="sxs-lookup"><span data-stu-id="d0fe0-129">Provision your device in hello remote monitoring solution</span></span>
> [!NOTE]
> <span data-ttu-id="d0fe0-130">Çözümünüzde önceden bir cihaz hazırladıysanız bu adımı atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0fe0-130">If you have already provisioned a device in your solution, you can skip this step.</span></span> <span data-ttu-id="d0fe0-131">Merhaba istemci uygulaması oluşturduğunuzda tooknow hello cihaz kimlik bilgileri gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0fe0-131">You need tooknow hello device credentials when you create hello client application.</span></span>
> 
> 

<span data-ttu-id="d0fe0-132">Bir cihaz tooconnect toohello önceden yapılandırılmış çözümü kendisini tooIoT Hub tanımlamak gerekir geçerli kimlik bilgilerini kullanarak.</span><span class="sxs-lookup"><span data-stu-id="d0fe0-132">For a device tooconnect toohello preconfigured solution, it must identify itself tooIoT Hub using valid credentials.</span></span> <span data-ttu-id="d0fe0-133">Merhaba çözüm panodan hello aygıt kimlik bilgilerini alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0fe0-133">You can retrieve hello device credentials from hello solution dashboard.</span></span> <span data-ttu-id="d0fe0-134">Bu öğreticide daha sonra istemci uygulamanızda hello cihaz kimlik bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="d0fe0-134">You include hello device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="d0fe0-135">tooadd bir aygıt tooyour Uzaktan izleme çözümü, aşağıdaki tam hello hello çözüm panosunda adımlar:</span><span class="sxs-lookup"><span data-stu-id="d0fe0-135">tooadd a device tooyour remote monitoring solution, complete hello following steps in hello solution dashboard:</span></span>

1. <span data-ttu-id="d0fe0-136">Merhaba sol alt köşedeki hello Pano, tıklatın **bir cihaz ekleme**.</span><span class="sxs-lookup"><span data-stu-id="d0fe0-136">In hello lower left-hand corner of hello dashboard, click **Add a device**.</span></span>
   
   ![Cihaz ekleme][1]
2. <span data-ttu-id="d0fe0-138">Merhaba, **özel cihaz** öğesine tıklayın **yeni Ekle**.</span><span class="sxs-lookup"><span data-stu-id="d0fe0-138">In hello **Custom Device** panel, click **Add new**.</span></span>
   
   ![Özel cihaz ekleme][2]
3. <span data-ttu-id="d0fe0-140">**Kendi Cihaz Kimliğimi tanımlamama izin ver**'i seçin.</span><span class="sxs-lookup"><span data-stu-id="d0fe0-140">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="d0fe0-141">Bir cihaz kimliği girin **mydevice**, tıklatın **denetleyin kimliği** tooverify bu ad zaten kullanımda olmadığından ve ardından **oluşturma** tooprovision hello aygıt.</span><span class="sxs-lookup"><span data-stu-id="d0fe0-141">Enter a Device ID such as **mydevice**, click **Check ID** tooverify that name isn't already in use, and then click **Create** tooprovision hello device.</span></span>
   
   ![Cihaz kimliği ekleme][3]
4. <span data-ttu-id="d0fe0-143">Kimlik bilgilerini (cihaz kimliği, IOT Hub ana bilgisayar adına ve aygıt anahtarı) not hello aygıt olun.</span><span class="sxs-lookup"><span data-stu-id="d0fe0-143">Make a note hello device credentials (Device ID, IoT Hub Hostname, and Device Key).</span></span> <span data-ttu-id="d0fe0-144">İstemci uygulamanız bu değerleri tooconnect toohello Uzaktan izleme çözümü gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0fe0-144">Your client application needs these values tooconnect toohello remote monitoring solution.</span></span> <span data-ttu-id="d0fe0-145">Sonra da **Bitti**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d0fe0-145">Then click **Done**.</span></span>
   
    ![Cihaz kimlik bilgilerini görüntüleme][4]
5. <span data-ttu-id="d0fe0-147">Merhaba çözüm Panosu hello aygıt listesinde aygıtınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="d0fe0-147">Select your device in hello device list in hello solution dashboard.</span></span> <span data-ttu-id="d0fe0-148">Ardından hello **cihaz ayrıntıları** öğesine tıklayın **aygıtı etkinleştir**.</span><span class="sxs-lookup"><span data-stu-id="d0fe0-148">Then, in hello **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="d0fe0-149">Merhaba Cihazınızı durumudur şimdi **çalıştıran**.</span><span class="sxs-lookup"><span data-stu-id="d0fe0-149">hello status of your device is now **Running**.</span></span> <span data-ttu-id="d0fe0-150">Merhaba Uzaktan izleme çözümü şimdi aygıtınızdan telemetri almasına ve hello aygıtta yöntemleri çağırma.</span><span class="sxs-lookup"><span data-stu-id="d0fe0-150">hello remote monitoring solution can now receive telemetry from your device and invoke methods on hello device.</span></span>

[img-dashboard]: ./media/iot-suite-selector-connecting/dashboard.png
[1]: ./media/iot-suite-selector-connecting/suite0.png
[2]: ./media/iot-suite-selector-connecting/suite1.png
[3]: ./media/iot-suite-selector-connecting/suite2.png
[4]: ./media/iot-suite-selector-connecting/suite3.png

[lnk-what-are-preconfig-solutions]: ../articles/iot-suite/iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: ../articles/iot-suite/iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/