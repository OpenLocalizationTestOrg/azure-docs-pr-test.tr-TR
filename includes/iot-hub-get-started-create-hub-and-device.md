## <a name="create-an-iot-hub"></a><span data-ttu-id="a3be6-101">IoT hub oluşturma</span><span class="sxs-lookup"><span data-stu-id="a3be6-101">Create an IoT hub</span></span>

1. <span data-ttu-id="a3be6-102">Merhaba, [Azure portal](https://portal.azure.com/), tıklatın **yeni** > **nesnelerin interneti** > **IOT hub'ı**.</span><span class="sxs-lookup"><span data-stu-id="a3be6-102">In hello [Azure portal](https://portal.azure.com/), click **New** > **Internet of Things** > **IoT Hub**.</span></span>

   ![Hello Azure portal IOT hub oluşturma](../articles/iot-hub/media/iot-hub-create-hub-and-device/1_create-azure-iot-hub-portal.png)
2. <span data-ttu-id="a3be6-104">Merhaba, **IOT hub'ı** bölmesinde, IOT hub'ınız için bilgisinden hello girin:</span><span class="sxs-lookup"><span data-stu-id="a3be6-104">In hello **IoT hub** pane, enter hello following information for your IoT hub:</span></span>

     <span data-ttu-id="a3be6-105">**Ad**: Merhaba IOT hub'ınızın adını girin.</span><span class="sxs-lookup"><span data-stu-id="a3be6-105">**Name**: Enter hello name of your IoT hub.</span></span> <span data-ttu-id="a3be6-106">Girdiğiniz hello adı geçerli ise, yeşil bir onay işareti görünür.</span><span class="sxs-lookup"><span data-stu-id="a3be6-106">If hello name you enter is valid, a green check mark appears.</span></span>

     <span data-ttu-id="a3be6-107">**Fiyatlandırma ve ölçek katmanı**: Select hello **F1 - boş** katmanı.</span><span class="sxs-lookup"><span data-stu-id="a3be6-107">**Pricing and scale tier**: Select hello **F1 - Free** tier.</span></span> <span data-ttu-id="a3be6-108">Bu seçenek bu tanıtım için yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="a3be6-108">This option is sufficient for this demo.</span></span> <span data-ttu-id="a3be6-109">Daha fazla bilgi için bkz: Merhaba [fiyatlandırma ve ölçek katmanı](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="a3be6-109">For more information, see hello [Pricing and scale tier](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

     <span data-ttu-id="a3be6-110">**Kaynak grubu**: bir kaynak grubu toohost hello IOT hub oluşturmanız veya mevcut bir kullanın.</span><span class="sxs-lookup"><span data-stu-id="a3be6-110">**Resource group**: Create a resource group toohost hello IoT hub or use an existing one.</span></span> <span data-ttu-id="a3be6-111">Daha fazla bilgi için bkz: [kullanım kaynak gruplarını toomanage Azure kaynaklarınızı](../articles/azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a3be6-111">For more information, see [Use resource groups toomanage your Azure resources](../articles/azure-resource-manager/resource-group-portal.md).</span></span>

     <span data-ttu-id="a3be6-112">**Konum**: Merhaba hello IOT hub'ı oluşturulduğu en yakın konumu tooyou seçin.</span><span class="sxs-lookup"><span data-stu-id="a3be6-112">**Location**: Select hello closest location tooyou where hello IoT hub is created.</span></span>

     <span data-ttu-id="a3be6-113">**PIN toodashboard**: hello panodan tooyour IOT hub'ı kolay erişim için bu seçeneği belirleyin.</span><span class="sxs-lookup"><span data-stu-id="a3be6-113">**Pin toodashboard**: Select this option for easy access tooyour IoT hub from hello dashboard.</span></span>

   ![IOT hub'ınızı bilgi toocreate girin](../articles/iot-hub/media/iot-hub-create-hub-and-device/2_fill-in-fields-for-azure-iot-hub-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]

3. <span data-ttu-id="a3be6-115">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a3be6-115">Click **Create**.</span></span> <span data-ttu-id="a3be6-116">IOT hub'ınızı birkaç dakika toocreate alabilir.</span><span class="sxs-lookup"><span data-stu-id="a3be6-116">Your IoT hub might take a few minutes toocreate.</span></span> <span data-ttu-id="a3be6-117">Merhaba ediyor görebilirsiniz **bildirimleri** bölmesi.</span><span class="sxs-lookup"><span data-stu-id="a3be6-117">You can see progress in hello **Notifications** pane.</span></span>

   ![IoT hub’ınıza ilişkin ilerleme durumu bildirimlerine bakın](../articles/iot-hub/media/iot-hub-create-hub-and-device/3_notification-azure-iot-hub-creation-progress-portal.png)

4. <span data-ttu-id="a3be6-119">IOT hub'ınızı oluşturulduktan sonra Başlangıç panosunda'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a3be6-119">After your IoT hub is created, click it on hello dashboard.</span></span> <span data-ttu-id="a3be6-120">Merhaba Not **ana bilgisayar adı**ve ardından **paylaşılan erişim ilkeleri**.</span><span class="sxs-lookup"><span data-stu-id="a3be6-120">Make a note of hello **Hostname**, and then click **Shared access policies**.</span></span>

   ![IOT hub'ınızın Hello konak adını Al](../articles/iot-hub/media/iot-hub-create-hub-and-device/4_get-azure-iot-hub-hostname-portal.png)

5. <span data-ttu-id="a3be6-122">Merhaba, **paylaşılan erişim ilkeleri** bölmesinde hello tıklatın **iothubowner** İlkesi ve ardından Kopyala ve not edin hello **bağlantı dizesi** IOT hub'ınızın.</span><span class="sxs-lookup"><span data-stu-id="a3be6-122">In hello **Shared access policies** pane, click hello **iothubowner** policy, and then copy and make a note of hello **Connection string** of your IoT hub.</span></span> <span data-ttu-id="a3be6-123">Daha fazla bilgi için bkz: [Denetim erişim tooIoT Hub](../articles/iot-hub/iot-hub-devguide-security.md).</span><span class="sxs-lookup"><span data-stu-id="a3be6-123">For more information, see [Control access tooIoT Hub](../articles/iot-hub/iot-hub-devguide-security.md).</span></span>

> [!NOTE] 
<span data-ttu-id="a3be6-124">Bu kurulum öğreticisinde bu iothubowner bağlantı dizesi gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="a3be6-124">You will not need this iothubowner connection string for this set-up tutorial.</span></span> <span data-ttu-id="a3be6-125">Ancak, bu kurulum tamamlandıktan sonra bazı farklı IOT senaryolarını hello öğretici için gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="a3be6-125">However, you may need it for some of hello tutorials on different IoT scenarios after you complete this set-up.</span></span>

   ![IoT hub bağlantı dizenizi alma](../articles/iot-hub/media/iot-hub-create-hub-and-device/5_get-azure-iot-hub-connection-string-portal.png)

## <a name="register-a-device-in-hello-iot-hub-for-your-device"></a><span data-ttu-id="a3be6-127">Merhaba IOT hub, cihazınız için bir cihaz kaydetme</span><span class="sxs-lookup"><span data-stu-id="a3be6-127">Register a device in hello IoT hub for your device</span></span>

1. <span data-ttu-id="a3be6-128">Merhaba, [Azure portal](https://portal.azure.com/), IOT hub'ınızı açın.</span><span class="sxs-lookup"><span data-stu-id="a3be6-128">In hello [Azure portal](https://portal.azure.com/), open your IoT hub.</span></span>

2. <span data-ttu-id="a3be6-129">**Device Explorer**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a3be6-129">Click **Device Explorer**.</span></span>
3. <span data-ttu-id="a3be6-130">Merhaba aygıt Gezgini bölmesinde **Ekle** tooadd bir aygıt tooyour IOT hub'ı.</span><span class="sxs-lookup"><span data-stu-id="a3be6-130">In hello Device Explorer pane, click **Add** tooadd a device tooyour IoT hub.</span></span> <span data-ttu-id="a3be6-131">Ardından aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="a3be6-131">Then do hello following:</span></span>

   <span data-ttu-id="a3be6-132">**Cihaz kimliği**: hello hello yeni cihaz Kimliğini girin.</span><span class="sxs-lookup"><span data-stu-id="a3be6-132">**Device ID**: Enter hello ID of hello new device.</span></span> <span data-ttu-id="a3be6-133">Cihaz Kimlikleri büyük/küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="a3be6-133">Device IDs are case sensitive.</span></span>

   <span data-ttu-id="a3be6-134">**Kimlik Doğrulama Türü**: **Simetrik Anahtar**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="a3be6-134">**Authentication Type**: Select **Symmetric Key**.</span></span>

   <span data-ttu-id="a3be6-135">**Anahtarları Otomatik Onayla**: Bu onay kutusunu işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="a3be6-135">**Auto Generate Keys**: Select this check box.</span></span>

   <span data-ttu-id="a3be6-136">**Aygıt tooIoT Hub bağlanmak**: tıklatın **etkinleştirmek**.</span><span class="sxs-lookup"><span data-stu-id="a3be6-136">**Connect device tooIoT Hub**: Click **Enable**.</span></span>

   ![Bir aygıt hello IOT hub'ınızın cihaz Explorer ekleme](../articles/iot-hub/media/iot-hub-create-hub-and-device/6_add-device-in-azure-iot-hub-device-explorer-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

4. <span data-ttu-id="a3be6-138">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a3be6-138">Click **Save**.</span></span>
5. <span data-ttu-id="a3be6-139">Merhaba aygıt oluşturulduktan sonra hello aygıt hello açmak **aygıt Explorer** bölmesi.</span><span class="sxs-lookup"><span data-stu-id="a3be6-139">After hello device is created, open hello device in hello **Device Explorer** pane.</span></span>
6. <span data-ttu-id="a3be6-140">Merhaba bağlantı dizesi hello birincil anahtarı not edin.</span><span class="sxs-lookup"><span data-stu-id="a3be6-140">Make a note of hello primary key of hello connection string.</span></span>

   ![Merhaba cihaz bağlantı dizesi Al](../articles/iot-hub/media/iot-hub-create-hub-and-device/7_get-device-connection-string-in-device-explorer-portal.png)
