> [!div class="op_single_selector"]
> * [<span data-ttu-id="b6fd4-101">Windows üzerinde C</span><span class="sxs-lookup"><span data-stu-id="b6fd4-101">C on Windows</span></span>](../articles/iot-suite/iot-suite-connecting-devices.md)
> * [<span data-ttu-id="b6fd4-102">Linux üzerinde C</span><span class="sxs-lookup"><span data-stu-id="b6fd4-102">C on Linux</span></span>](../articles/iot-suite/iot-suite-connecting-devices-linux.md)
> * [<span data-ttu-id="b6fd4-103">Node.js</span><span class="sxs-lookup"><span data-stu-id="b6fd4-103">Node.js</span></span>](../articles/iot-suite/iot-suite-connecting-devices-node.md)
> 
> 

## <a name="scenario-overview"></a><span data-ttu-id="b6fd4-104">Senaryoya genel bakış</span><span class="sxs-lookup"><span data-stu-id="b6fd4-104">Scenario overview</span></span>
<span data-ttu-id="b6fd4-105">Bu senaryoda aşağıdaki telemetriyi önceden yapılandırılmış uzaktan izleme [çözümüne][lnk-what-are-preconfig-solutions] gönderen bir cihaz oluşturacaksınız:</span><span class="sxs-lookup"><span data-stu-id="b6fd4-105">In this scenario, you create a device that sends the following telemetry to the remote monitoring [preconfigured solution][lnk-what-are-preconfig-solutions]:</span></span>

* <span data-ttu-id="b6fd4-106">Dış ortam sıcaklığı</span><span class="sxs-lookup"><span data-stu-id="b6fd4-106">External temperature</span></span>
* <span data-ttu-id="b6fd4-107">İç ortam sıcaklığı</span><span class="sxs-lookup"><span data-stu-id="b6fd4-107">Internal temperature</span></span>
* <span data-ttu-id="b6fd4-108">Nem oranı</span><span class="sxs-lookup"><span data-stu-id="b6fd4-108">Humidity</span></span>

<span data-ttu-id="b6fd4-109">Örneği basitleştirmek amacıyla cihaz üzerindeki kod örnek değerler oluşturmaktadır. Ancak cihazınıza gerçek sensörler bağlayıp gerçek telemetri verileri göndererek örneği ileri taşımanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="b6fd4-109">For simplicity, the code on the device generates sample values, but we encourage you to extend the sample by connecting real sensors to your device and sending real telemetry.</span></span>

<span data-ttu-id="b6fd4-110">Cihaz ayrıca çözüm panosundan çağrılan yöntemlere ve çözüm panosunda ayarlanan istenen özellik değerlerine yanıt verebilir.</span><span class="sxs-lookup"><span data-stu-id="b6fd4-110">The device is also able to respond to methods invoked from the solution dashboard and desired property values set in the solution dashboard.</span></span>

<span data-ttu-id="b6fd4-111">Bu öğreticiyi tamamlamak için etkin bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b6fd4-111">To complete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="b6fd4-112">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6fd4-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="b6fd4-113">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="b6fd4-113">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

## <a name="before-you-start"></a><span data-ttu-id="b6fd4-114">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="b6fd4-114">Before you start</span></span>
<span data-ttu-id="b6fd4-115">Cihazınız için kod yazmadan önce, önceden yapılandırılmış uzaktan izleme çözümünüzü ve bu çözümde yeni bir özel cihaz hazırlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b6fd4-115">Before you write any code for your device, you must provision your remote monitoring preconfigured solution and provision a new custom device in that solution.</span></span>

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="b6fd4-116">Önceden yapılandırılmış uzaktan izleme çözümünüzü sağlama</span><span class="sxs-lookup"><span data-stu-id="b6fd4-116">Provision your remote monitoring preconfigured solution</span></span>
<span data-ttu-id="b6fd4-117">Bu öğreticide oluşturduğunuz cihaz, önceden yapılandırılmış bir [uzaktan izleme][lnk-remote-monitoring] çözümü örneğine veri göndermektedir.</span><span class="sxs-lookup"><span data-stu-id="b6fd4-117">The device you create in this tutorial sends data to an instance of the [remote monitoring][lnk-remote-monitoring] preconfigured solution.</span></span> <span data-ttu-id="b6fd4-118">Önceden yapılandırılmış uzaktan izleme çözümünüzü henüz Azure hesabınızda hazırlamadıysanız aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="b6fd4-118">If you haven't already provisioned the remote monitoring preconfigured solution in your Azure account, use the following steps:</span></span>

1. <span data-ttu-id="b6fd4-119"><https://www.azureiotsuite.com/> sayfasında çözüm oluşturmak için **+** öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b6fd4-119">On the <https://www.azureiotsuite.com/> page, click **+** to create a solution.</span></span>
2. <span data-ttu-id="b6fd4-120">Çözümünüzü oluşturmak için **Uzaktan izleme** panelindeki **Seç**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b6fd4-120">Click **Select** on the **Remote monitoring** panel to create your solution.</span></span>
3. <span data-ttu-id="b6fd4-121">**Uzaktan izleme çözümü oluştur** sayfasında bir **Çözüm adı** belirleyin, dağıtmak istediğiniz **Bölgeyi** seçin ve kullanmak istediğiniz Azure aboneliğini belirtin.</span><span class="sxs-lookup"><span data-stu-id="b6fd4-121">On the **Create Remote monitoring solution** page, enter a **Solution name** of your choice, select the **Region** you want to deploy to, and select the Azure subscription to want to use.</span></span> <span data-ttu-id="b6fd4-122">Ardından **Çözüm oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b6fd4-122">Then click **Create solution**.</span></span>
4. <span data-ttu-id="b6fd4-123">Sağlama işleminin tamamlanmasını bekleyin.</span><span class="sxs-lookup"><span data-stu-id="b6fd4-123">Wait until the provisioning process completes.</span></span>

> [!WARNING]
> <span data-ttu-id="b6fd4-124">Önceden yapılandırılmış çözümler, faturalanabilir Azure hizmetlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="b6fd4-124">The preconfigured solutions use billable Azure services.</span></span> <span data-ttu-id="b6fd4-125">Gereksiz ücretlerden kaçınmak için işinizi tamamladıktan sonra önceden yapılandırılmış çözümü aboneliğinizden kaldırmayı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b6fd4-125">Be sure to remove the preconfigured solution from your subscription when you are done with it to avoid any unnecessary charges.</span></span> <span data-ttu-id="b6fd4-126">Önceden yapılandırılmış çözümü aboneliğinizden tamamen kaldırmak için <https://www.azureiotsuite.com/> sayfasını ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="b6fd4-126">You can completely remove a preconfigured solution from your subscription by visiting the <https://www.azureiotsuite.com/> page.</span></span>
> 
> 

<span data-ttu-id="b6fd4-127">Uzaktan izleme çözümü için sağlama işlemi tamamlandıktan sonra çözüm panosunu tarayıcınızda açmak için **Başlat**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b6fd4-127">When the provisioning process for the remote monitoring solution finishes, click **Launch** to open the solution dashboard in your browser.</span></span>

![Çözüm panosu][img-dashboard]

### <a name="provision-your-device-in-the-remote-monitoring-solution"></a><span data-ttu-id="b6fd4-129">Cihazınızı uzaktan izleme çözümünde sağlama</span><span class="sxs-lookup"><span data-stu-id="b6fd4-129">Provision your device in the remote monitoring solution</span></span>
> [!NOTE]
> <span data-ttu-id="b6fd4-130">Çözümünüzde önceden bir cihaz hazırladıysanız bu adımı atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6fd4-130">If you have already provisioned a device in your solution, you can skip this step.</span></span> <span data-ttu-id="b6fd4-131">İstemci uygulamasını oluştururken cihaz kimlik bilgilerini bilmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b6fd4-131">You need to know the device credentials when you create the client application.</span></span>
> 
> 

<span data-ttu-id="b6fd4-132">Bir cihazın önceden yapılandırılmış çözüme bağlanabilmesi için geçerli kimlik bilgileriyle kendini IoT Hub üzerinde tanıtması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b6fd4-132">For a device to connect to the preconfigured solution, it must identify itself to IoT Hub using valid credentials.</span></span> <span data-ttu-id="b6fd4-133">Cihaz kimlik bilgilerini çözüm panosundan alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6fd4-133">You can retrieve the device credentials from the solution dashboard.</span></span> <span data-ttu-id="b6fd4-134">Cihaz kimlik bilgilerini bu öğreticinin sonraki adımlarında istemci uygulamanıza ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6fd4-134">You include the device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="b6fd4-135">Uzaktan izleme çözümünüze cihaz eklemek için çözüm panosunda aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="b6fd4-135">To add a device to your remote monitoring solution, complete the following steps in the solution dashboard:</span></span>

1. <span data-ttu-id="b6fd4-136">Panonun sol alt köşesinde **Cihaz ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b6fd4-136">In the lower left-hand corner of the dashboard, click **Add a device**.</span></span>
   
   ![Cihaz ekleme][1]
2. <span data-ttu-id="b6fd4-138">**Özel Cihaz** panelinde **Yeni ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b6fd4-138">In the **Custom Device** panel, click **Add new**.</span></span>
   
   ![Özel cihaz ekleme][2]
3. <span data-ttu-id="b6fd4-140">**Kendi Cihaz Kimliğimi tanımlamama izin ver**'i seçin.</span><span class="sxs-lookup"><span data-stu-id="b6fd4-140">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="b6fd4-141">**cihazım** gibi bir Cihaz Kimliği girin, adın kullanımda olmadığını doğrulamak için **Kimliği denetle**'ye tıklayın ve ardından cihazı hazırlamak için **Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b6fd4-141">Enter a Device ID such as **mydevice**, click **Check ID** to verify that name isn't already in use, and then click **Create** to provision the device.</span></span>
   
   ![Cihaz kimliği ekleme][3]
4. <span data-ttu-id="b6fd4-143">Cihaz kimlik bilgilerini (Cihaz Kimliği, IoT Hub Ana Bilgisayar Adı ve Cihaz Anahtarı) not edin.</span><span class="sxs-lookup"><span data-stu-id="b6fd4-143">Make a note the device credentials (Device ID, IoT Hub Hostname, and Device Key).</span></span> <span data-ttu-id="b6fd4-144">İstemci uygulamanız uzaktan izleme çözümüne bağlanmak için bu değerleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="b6fd4-144">Your client application needs these values to connect to the remote monitoring solution.</span></span> <span data-ttu-id="b6fd4-145">Sonra da **Bitti**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b6fd4-145">Then click **Done**.</span></span>
   
    ![Cihaz kimlik bilgilerini görüntüleme][4]
5. <span data-ttu-id="b6fd4-147">Çözüm panosundaki cihaz listesinden cihazınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="b6fd4-147">Select your device in the device list in the solution dashboard.</span></span> <span data-ttu-id="b6fd4-148">Ardından **Cihaz Ayrıntıları** panelinde **Cihazı Etkinleştir**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b6fd4-148">Then, in the **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="b6fd4-149">Cihazınızın durumu **Çalışıyor** olarak değişir.</span><span class="sxs-lookup"><span data-stu-id="b6fd4-149">The status of your device is now **Running**.</span></span> <span data-ttu-id="b6fd4-150">Uzaktan izleme çözümü artık cihazınızdan telemetri verileri alabilir ve cihazınızda yöntemler çağırabilir.</span><span class="sxs-lookup"><span data-stu-id="b6fd4-150">The remote monitoring solution can now receive telemetry from your device and invoke methods on the device.</span></span>

[img-dashboard]: ./media/iot-suite-selector-connecting/dashboard.png
[1]: ./media/iot-suite-selector-connecting/suite0.png
[2]: ./media/iot-suite-selector-connecting/suite1.png
[3]: ./media/iot-suite-selector-connecting/suite2.png
[4]: ./media/iot-suite-selector-connecting/suite3.png

[lnk-what-are-preconfig-solutions]: ../articles/iot-suite/iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: ../articles/iot-suite/iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/