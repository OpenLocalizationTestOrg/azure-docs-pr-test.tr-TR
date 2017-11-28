## <a name="view-the-solution-dashboard"></a><span data-ttu-id="02781-101">Çözüm panosunu görüntüleme</span><span class="sxs-lookup"><span data-stu-id="02781-101">View the solution dashboard</span></span>

<span data-ttu-id="02781-102">Çözüm panosu, dağıtılan çözümü yönetmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="02781-102">The solution dashboard enables you to manage the deployed solution.</span></span> <span data-ttu-id="02781-103">Örneğin, telemetriyi görüntüleyebilir, cihazları eklemek ve yöntemleri çağırma.</span><span class="sxs-lookup"><span data-stu-id="02781-103">For example, you can view telemetry, add devices, and invoke methods.</span></span>

1. <span data-ttu-id="02781-104">Sağlama tamamlandığında ve önceden yapılandırılmış çözümünüzün kutucuğu **Hazır**’ı gösterdiğinde, uzaktan izleme çözümü portalınızı yeni bir sekmede açmak için **Başlat**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="02781-104">When the provisioning is complete and the tile for your preconfigured solution indicates **Ready**, choose **Launch** to open your remote monitoring solution portal in a new tab.</span></span>

    ![Önceden yapılandırılmış çözümü başlatma][img-launch-solution]

1. <span data-ttu-id="02781-106">Varsayılan olarak, çözüm portalı *panoyu* gösterir.</span><span class="sxs-lookup"><span data-stu-id="02781-106">By default, the solution portal shows the *dashboard*.</span></span> <span data-ttu-id="02781-107">Sayfanın sol taraftaki menüyü kullanarak çözüm portalı diğer alanlara gidin.</span><span class="sxs-lookup"><span data-stu-id="02781-107">Navigate to other areas of the solution portal using the menu on the left-hand side of the page.</span></span>

    ![Önceden yapılandırılmış uzaktan izleme panosu][img-menu]

## <a name="add-a-device"></a><span data-ttu-id="02781-109">Cihaz ekleme</span><span class="sxs-lookup"><span data-stu-id="02781-109">Add a device</span></span>

<span data-ttu-id="02781-110">Bir cihazın önceden yapılandırılmış çözüme bağlanabilmesi için geçerli kimlik bilgileriyle kendini IoT Hub üzerinde tanıtması gerekir.</span><span class="sxs-lookup"><span data-stu-id="02781-110">For a device to connect to the preconfigured solution, it must identify itself to IoT Hub using valid credentials.</span></span> <span data-ttu-id="02781-111">Cihaz kimlik bilgilerini çözüm panosundan alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="02781-111">You can retrieve the device credentials from the solution dashboard.</span></span> <span data-ttu-id="02781-112">Cihaz kimlik bilgilerini bu öğreticinin sonraki adımlarında istemci uygulamanıza ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="02781-112">You include the device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="02781-113">Uzaktan izleme çözümünüze cihaz eklemek için çözüm panosunda aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="02781-113">To add a device to your remote monitoring solution, complete the following steps in the solution dashboard:</span></span>

1. <span data-ttu-id="02781-114">Panonun sol alt köşesinde **Cihaz ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="02781-114">In the lower left-hand corner of the dashboard, click **Add a device**.</span></span>

   ![Cihaz ekleme][1]

1. <span data-ttu-id="02781-116">**Özel Cihaz** panelinde **Yeni ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="02781-116">In the **Custom Device** panel, click **Add new**.</span></span>

   ![Özel cihaz ekleme][2]

1. <span data-ttu-id="02781-118">**Kendi Cihaz Kimliğimi tanımlamama izin ver**'i seçin.</span><span class="sxs-lookup"><span data-stu-id="02781-118">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="02781-119">Bir cihaz kimliği girin **device01**, tıklatın **denetleyin kimliği** adı çözümünüzde zaten kullanmadıysanız ve ardından doğrulamak için **oluşturma** cihaz sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="02781-119">Enter a Device ID such as **device01**, click **Check ID** to verify you haven't already used the name in your solution, and then click **Create** to provision the device.</span></span>

   ![Cihaz kimliği ekleme][3]

1. <span data-ttu-id="02781-121">Cihaz kimlik bilgilerini not edin (**cihaz kimliği**, **IOT Hub ana bilgisayar adına**, ve **aygıt anahtarı**).</span><span class="sxs-lookup"><span data-stu-id="02781-121">Make a note the device credentials (**Device ID**, **IoT Hub Hostname**, and **Device Key**).</span></span> <span data-ttu-id="02781-122">İstemci uygulamanızı Intel NUC üzerinde Uzaktan izleme çözümüne bağlanmak için bu değerleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="02781-122">Your client application on the Intel NUC needs these values to connect to the remote monitoring solution.</span></span> <span data-ttu-id="02781-123">Sonra da **Bitti**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="02781-123">Then click **Done**.</span></span>

    ![Cihaz kimlik bilgilerini görüntüleme][4]

1. <span data-ttu-id="02781-125">Çözüm panosundaki cihaz listesinden cihazınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="02781-125">Select your device in the device list in the solution dashboard.</span></span> <span data-ttu-id="02781-126">Ardından **Cihaz Ayrıntıları** panelinde **Cihazı Etkinleştir**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="02781-126">Then, in the **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="02781-127">Cihazınızın durumu **Çalışıyor** olarak değişir.</span><span class="sxs-lookup"><span data-stu-id="02781-127">The status of your device is now **Running**.</span></span> <span data-ttu-id="02781-128">Uzaktan izleme çözümü artık cihazınızdan telemetri verileri alabilir ve cihazınızda yöntemler çağırabilir.</span><span class="sxs-lookup"><span data-stu-id="02781-128">The remote monitoring solution can now receive telemetry from your device and invoke methods on the device.</span></span>

[img-launch-solution]: media/iot-suite-gateway-kit-view-solution/launch.png
[img-menu]: media/iot-suite-gateway-kit-view-solution/menu.png
[1]: media/iot-suite-gateway-kit-view-solution/suite0.png
[2]: media/iot-suite-gateway-kit-view-solution/suite1.png
[3]: media/iot-suite-gateway-kit-view-solution/suite2.png
[4]: media/iot-suite-gateway-kit-view-solution/suite3.png