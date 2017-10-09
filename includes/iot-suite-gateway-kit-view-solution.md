## <a name="view-hello-solution-dashboard"></a><span data-ttu-id="03261-101">Görünüm hello çözüm Panosu</span><span class="sxs-lookup"><span data-stu-id="03261-101">View hello solution dashboard</span></span>

<span data-ttu-id="03261-102">Merhaba çözüm Panosu toomanage dağıtılan hello çözümü sağlar.</span><span class="sxs-lookup"><span data-stu-id="03261-102">hello solution dashboard enables you toomanage hello deployed solution.</span></span> <span data-ttu-id="03261-103">Örneğin, telemetriyi görüntüleyebilir, cihazları eklemek ve yöntemleri çağırma.</span><span class="sxs-lookup"><span data-stu-id="03261-103">For example, you can view telemetry, add devices, and invoke methods.</span></span>

1. <span data-ttu-id="03261-104">Ne zaman hello Sağlama tamamlandıktan ve önceden yapılandırılmış çözümünüzün kutucuğu hello gösterir **hazır**, seçin **başlatma** tooopen Uzaktan izleme çözümü portalınızı yeni bir sekmede.</span><span class="sxs-lookup"><span data-stu-id="03261-104">When hello provisioning is complete and hello tile for your preconfigured solution indicates **Ready**, choose **Launch** tooopen your remote monitoring solution portal in a new tab.</span></span>

    ![Merhaba önceden yapılandırılmış çözüm başlatma][img-launch-solution]

1. <span data-ttu-id="03261-106">Varsayılan olarak, hello çözüm portalı hello gösterir *Pano*.</span><span class="sxs-lookup"><span data-stu-id="03261-106">By default, hello solution portal shows hello *dashboard*.</span></span> <span data-ttu-id="03261-107">Merhaba sol taraftaki hello sayfasının hello menüsünü kullanarak hello çözüm portalı tooother alanlarının gidin.</span><span class="sxs-lookup"><span data-stu-id="03261-107">Navigate tooother areas of hello solution portal using hello menu on hello left-hand side of hello page.</span></span>

    ![Önceden yapılandırılmış uzaktan izleme panosu][img-menu]

## <a name="add-a-device"></a><span data-ttu-id="03261-109">Cihaz ekleme</span><span class="sxs-lookup"><span data-stu-id="03261-109">Add a device</span></span>

<span data-ttu-id="03261-110">Bir cihaz tooconnect toohello önceden yapılandırılmış çözümü kendisini tooIoT Hub tanımlamak gerekir geçerli kimlik bilgilerini kullanarak.</span><span class="sxs-lookup"><span data-stu-id="03261-110">For a device tooconnect toohello preconfigured solution, it must identify itself tooIoT Hub using valid credentials.</span></span> <span data-ttu-id="03261-111">Merhaba çözüm panodan hello aygıt kimlik bilgilerini alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="03261-111">You can retrieve hello device credentials from hello solution dashboard.</span></span> <span data-ttu-id="03261-112">Bu öğreticide daha sonra istemci uygulamanızda hello cihaz kimlik bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="03261-112">You include hello device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="03261-113">tooadd bir aygıt tooyour Uzaktan izleme çözümü, aşağıdaki tam hello hello çözüm panosunda adımlar:</span><span class="sxs-lookup"><span data-stu-id="03261-113">tooadd a device tooyour remote monitoring solution, complete hello following steps in hello solution dashboard:</span></span>

1. <span data-ttu-id="03261-114">Merhaba sol alt köşedeki hello Pano, tıklatın **bir cihaz ekleme**.</span><span class="sxs-lookup"><span data-stu-id="03261-114">In hello lower left-hand corner of hello dashboard, click **Add a device**.</span></span>

   ![Cihaz ekleme][1]

1. <span data-ttu-id="03261-116">Merhaba, **özel cihaz** öğesine tıklayın **yeni Ekle**.</span><span class="sxs-lookup"><span data-stu-id="03261-116">In hello **Custom Device** panel, click **Add new**.</span></span>

   ![Özel cihaz ekleme][2]

1. <span data-ttu-id="03261-118">**Kendi Cihaz Kimliğimi tanımlamama izin ver**'i seçin.</span><span class="sxs-lookup"><span data-stu-id="03261-118">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="03261-119">Bir cihaz kimliği girin **device01**, tıklatın **denetleyin kimliği** hello adı çözümünüzde zaten kullanmadıysanız ve ardından tooverify **oluşturma** tooprovision hello aygıt.</span><span class="sxs-lookup"><span data-stu-id="03261-119">Enter a Device ID such as **device01**, click **Check ID** tooverify you haven't already used hello name in your solution, and then click **Create** tooprovision hello device.</span></span>

   ![Cihaz kimliği ekleme][3]

1. <span data-ttu-id="03261-121">Kimlik bilgilerini not hello aygıt yapın (**cihaz kimliği**, **IOT Hub ana bilgisayar adına**, ve **aygıt anahtarı**).</span><span class="sxs-lookup"><span data-stu-id="03261-121">Make a note hello device credentials (**Device ID**, **IoT Hub Hostname**, and **Device Key**).</span></span> <span data-ttu-id="03261-122">İstemci uygulamanızı hello Intel NUC üzerinde bu değerleri tooconnect toohello Uzaktan izleme çözümü gerekir.</span><span class="sxs-lookup"><span data-stu-id="03261-122">Your client application on hello Intel NUC needs these values tooconnect toohello remote monitoring solution.</span></span> <span data-ttu-id="03261-123">Sonra da **Bitti**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="03261-123">Then click **Done**.</span></span>

    ![Cihaz kimlik bilgilerini görüntüleme][4]

1. <span data-ttu-id="03261-125">Merhaba çözüm Panosu hello aygıt listesinde aygıtınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="03261-125">Select your device in hello device list in hello solution dashboard.</span></span> <span data-ttu-id="03261-126">Ardından hello **cihaz ayrıntıları** öğesine tıklayın **aygıtı etkinleştir**.</span><span class="sxs-lookup"><span data-stu-id="03261-126">Then, in hello **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="03261-127">Merhaba Cihazınızı durumudur şimdi **çalıştıran**.</span><span class="sxs-lookup"><span data-stu-id="03261-127">hello status of your device is now **Running**.</span></span> <span data-ttu-id="03261-128">Merhaba Uzaktan izleme çözümü şimdi aygıtınızdan telemetri almasına ve hello aygıtta yöntemleri çağırma.</span><span class="sxs-lookup"><span data-stu-id="03261-128">hello remote monitoring solution can now receive telemetry from your device and invoke methods on hello device.</span></span>

[img-launch-solution]: media/iot-suite-gateway-kit-view-solution/launch.png
[img-menu]: media/iot-suite-gateway-kit-view-solution/menu.png
[1]: media/iot-suite-gateway-kit-view-solution/suite0.png
[2]: media/iot-suite-gateway-kit-view-solution/suite1.png
[3]: media/iot-suite-gateway-kit-view-solution/suite2.png
[4]: media/iot-suite-gateway-kit-view-solution/suite3.png