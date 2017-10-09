## <a name="create-an-iot-hub"></a><span data-ttu-id="6f5cb-101">IoT hub oluşturma</span><span class="sxs-lookup"><span data-stu-id="6f5cb-101">Create an IoT hub</span></span>
<span data-ttu-id="6f5cb-102">Bir IOT hub, sanal cihaz uygulaması tooconnect için oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6f5cb-102">Create an IoT hub for your simulated device app tooconnect to.</span></span> <span data-ttu-id="6f5cb-103">Merhaba aşağıdaki adımlar, toocomplete bu nasıl görev tarafından gösterir hello Azure portal kullanarak.</span><span class="sxs-lookup"><span data-stu-id="6f5cb-103">hello following steps show you how toocomplete this task by using hello Azure portal.</span></span>

1. <span data-ttu-id="6f5cb-104">İçinde toohello oturum [Azure portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="6f5cb-104">Sign in toohello [Azure portal][lnk-portal].</span></span>
1. <span data-ttu-id="6f5cb-105">Hello harf çubuğu, tıklatın **yeni** > **nesnelerin interneti** > **IOT hub'ı**.</span><span class="sxs-lookup"><span data-stu-id="6f5cb-105">In hello Jumpbar, click **New** > **Internet of Things** > **IoT Hub**.</span></span>
   
    ![Azure portalı Atlama Çubuğu][1]
1. <span data-ttu-id="6f5cb-107">Merhaba, **IOT hub'ı** dikey penceresinde hello IOT hub'ınız için yapılandırmayı seçin.</span><span class="sxs-lookup"><span data-stu-id="6f5cb-107">In hello **IoT hub** blade, choose hello configuration for your IoT hub.</span></span>
   
    ![IOT hub'ı dikey penceresi][2]
   
   1. <span data-ttu-id="6f5cb-109">Merhaba, **adı** kutusuna, IOT hub'ınız için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="6f5cb-109">In hello **Name** box, enter a name for your IoT hub.</span></span> <span data-ttu-id="6f5cb-110">Merhaba, **adı** geçerli olduğundan ve kullanılabilir yeşil bir onay işareti hello görünür **adı** kutusu.</span><span class="sxs-lookup"><span data-stu-id="6f5cb-110">If hello **Name** is valid and available, a green check mark appears in hello **Name** box.</span></span>
    [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]
   
   1. <span data-ttu-id="6f5cb-111">Bir [fiyatlandırma ve ölçek katmanı][lnk-pricing] seçin.</span><span class="sxs-lookup"><span data-stu-id="6f5cb-111">Select a [pricing and scale tier][lnk-pricing].</span></span> <span data-ttu-id="6f5cb-112">Bu öğretici için belirli bir katman gerekmez.</span><span class="sxs-lookup"><span data-stu-id="6f5cb-112">This tutorial does not require a specific tier.</span></span> <span data-ttu-id="6f5cb-113">Bu öğretici için hello ücretsiz F1 katmanını kullanın.</span><span class="sxs-lookup"><span data-stu-id="6f5cb-113">For this tutorial, use hello free F1 tier.</span></span>
   1. <span data-ttu-id="6f5cb-114">**Kaynak grubunda** bir kaynak grubu oluşturun veya var olan bir kaynak grubunu seçin.</span><span class="sxs-lookup"><span data-stu-id="6f5cb-114">In **Resource group**, either create a resource group, or select an existing one.</span></span> <span data-ttu-id="6f5cb-115">Daha fazla bilgi için bkz: [Azure kaynaklarınızı grupları toomanage kaynağı kullanan][lnk-resource-groups].</span><span class="sxs-lookup"><span data-stu-id="6f5cb-115">For more information, see [Using resource groups toomanage your Azure resources][lnk-resource-groups].</span></span>
   1. <span data-ttu-id="6f5cb-116">İçinde **konumu**, seçin, IOT hub'ınızı konumu toohost hello.</span><span class="sxs-lookup"><span data-stu-id="6f5cb-116">In **Location**, select hello location toohost your IoT hub.</span></span> <span data-ttu-id="6f5cb-117">Bu öğretici için en yakın konumunuzu seçin.</span><span class="sxs-lookup"><span data-stu-id="6f5cb-117">For this tutorial, choose your nearest location.</span></span>
1. <span data-ttu-id="6f5cb-118">IoT hub'ı yapılandırma seçeneklerinizi seçtiğinizde **Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6f5cb-118">When you have chosen your IoT hub configuration options, click **Create**.</span></span>  <span data-ttu-id="6f5cb-119">Bu IOT hub'ınızı Azure toocreate birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="6f5cb-119">It can take a few minutes for Azure toocreate your IoT hub.</span></span> <span data-ttu-id="6f5cb-120">toocheck hello durum hello Sabitle veya hello bildirimleri panelinde hello ilerlemesini izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6f5cb-120">toocheck hello status, you can monitor hello progress on hello Startboard or in hello Notifications panel.</span></span>
   
    ![Yeni IOT hub'ı durumu][3]
1. <span data-ttu-id="6f5cb-122">Merhaba IOT hub'ı başarıyla oluşturuldu, IOT hub'hello Azure portal tooopen hello dikey penceresinde hello yeni IOT hub'ına yönelik hello yeni kutucuğa tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6f5cb-122">When hello IoT hub has been created successfully, click hello new tile for your IoT hub in hello Azure portal tooopen hello blade for hello new IoT hub.</span></span> <span data-ttu-id="6f5cb-123">Merhaba Not **ana bilgisayar adı**ve ardından **paylaşılan erişim ilkeleri**.</span><span class="sxs-lookup"><span data-stu-id="6f5cb-123">Make a note of hello **Hostname**, and then click **Shared access policies**.</span></span>
   
    ![Yeni IOT hub'ı dikey penceresi][4]
1. <span data-ttu-id="6f5cb-125">Merhaba, **paylaşılan erişim ilkeleri** dikey penceresinde hello tıklatın **iothubowner** İlkesi, kopyalayabilir ve hello IOT Hub bağlantı dizesine hello Not **iothubowner** dikey.</span><span class="sxs-lookup"><span data-stu-id="6f5cb-125">In hello **Shared access policies** blade, click hello **iothubowner** policy, and then copy and make note of hello IoT Hub connection string in hello **iothubowner** blade.</span></span> <span data-ttu-id="6f5cb-126">Daha fazla bilgi için bkz: [erişim denetimi] [ lnk-access-control] içinde hello "IOT Hub Geliştirici Kılavuzu."</span><span class="sxs-lookup"><span data-stu-id="6f5cb-126">For more information, see [Access control][lnk-access-control] in hello "IoT Hub developer guide."</span></span>
   
    ![Paylaşılan erişim ilkeleri dikey penceresi][5]

<!-- Images. -->
[1]: ./media/iot-hub-get-started-create-hub/create-iot-hub1.png
[2]: ./media/iot-hub-get-started-create-hub/create-iot-hub2.png
[3]: ./media/iot-hub-get-started-create-hub/create-iot-hub3.png
[4]: ./media/iot-hub-get-started-create-hub/create-iot-hub4.png
[5]: ./media/iot-hub-get-started-create-hub/create-iot-hub5.png

<!-- Links -->
[lnk-resource-groups]: ../articles/azure-resource-manager/resource-group-portal.md
[lnk-portal]: https://portal.azure.com/
[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-access-control]: ../articles/iot-hub/iot-hub-devguide-security.md
