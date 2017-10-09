## <a name="create-a-device-identity"></a><span data-ttu-id="5ff19-101">Cihaz kimliği oluşturma</span><span class="sxs-lookup"><span data-stu-id="5ff19-101">Create a device identity</span></span>

<span data-ttu-id="5ff19-102">Bu bölümde, kullandığınız hello [Azure portal] [ lnk-azure-portal] toocreate hello kimlik IOT hub'ınızı kayıt defterinde bir cihaz kimliği.</span><span class="sxs-lookup"><span data-stu-id="5ff19-102">In this section, you use hello [Azure portal][lnk-azure-portal] toocreate a device identity in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="5ff19-103">Merhaba kimlik kayıt defterinde girişi olmayan sürece bir aygıt tooIoT hub bağlanamıyor.</span><span class="sxs-lookup"><span data-stu-id="5ff19-103">A device cannot connect tooIoT hub unless it has an entry in hello identity registry.</span></span> <span data-ttu-id="5ff19-104">Daha fazla bilgi için hello hello "Kimlik kayıt defteri" bölümüne bakın [IOT Hub Geliştirici Kılavuzu][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="5ff19-104">For more information, see hello "Identity registry" section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="5ff19-105">Merhaba **aygıt Explorer** hello portal benzersiz cihaz kimliği ve anahtarı tooIoT hub'a bağlandığında Cihazınızı tooidentify kendisini kullanabilir oluşturmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="5ff19-105">hello **Device Explorer** in hello portal helps you generate a unique device ID and key that your device can use tooidentify itself when it connects tooIoT Hub.</span></span> <span data-ttu-id="5ff19-106">Cihaz Kimlikleri büyük/küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="5ff19-106">Device IDs are case sensitive.</span></span>

1. <span data-ttu-id="5ff19-107">İçinde toohello oturumunuz emin olun [Azure portal][lnk-azure-portal].</span><span class="sxs-lookup"><span data-stu-id="5ff19-107">Make sure you are signed in toohello [Azure portal][lnk-azure-portal].</span></span>

1. <span data-ttu-id="5ff19-108">Hello harf çubuğu, tıklatın **tüm kaynakları** ve IOT hub'ı kaynağınız bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ff19-108">In hello Jumpbar, click **All resources** and find your IoT hub resource.</span></span>

    ![Tooyour IOT hub'ı gidin][img-find-iothub]

1. <span data-ttu-id="5ff19-110">IOT hub'ı kaynağınız açıldığında hello tıklatın **aygıt Explorer** aracı ve ardından **Ekle** hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="5ff19-110">When your IoT hub resource is opened, click hello **Device Explorer** tool, and then click **Add** at hello top.</span></span> <span data-ttu-id="5ff19-111">Hello için yeni Cihazınızı gibi ad **myDeviceId**, tıklatıp **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="5ff19-111">Provide hello name for your new device, such as **myDeviceId**, and click **Save**.</span></span>

    ![Portalda cihaz kimliği oluşturma][img-create-device]

   <span data-ttu-id="5ff19-113">Bu IOT hub'ınız için yeni bir cihaz kimliği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5ff19-113">This creates a new device identity for your IoT hub.</span></span>

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

1. <span data-ttu-id="5ff19-114">Merhaba, **aygıt Explorer**'s aygıt listesinde yeni oluşturulan hello aygıt tıklayın ve hello Not **bağlantı dizesi---birincil anahtar**.</span><span class="sxs-lookup"><span data-stu-id="5ff19-114">In hello **Device Explorer**'s device list, click hello newly created device and make note of hello **Connection string---primary key**.</span></span> 

    ![Cihaz bağlantı dizesi][img-connection-string]

> [!NOTE]
> <span data-ttu-id="5ff19-116">Merhaba IOT Hub kimlik kayıt defteri, yalnızca cihaz kimlikleri tooenable güvenli erişim toohello IOT hub'ı depolar.</span><span class="sxs-lookup"><span data-stu-id="5ff19-116">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="5ff19-117">Cihaz kimliklerini ve anahtarlarını toouse güvenlik kimlik bilgileri ve toodisable erişim için tek bir cihaza kullanabilirsiniz bir etkin/devre dışı bayrağını depolar.</span><span class="sxs-lookup"><span data-stu-id="5ff19-117">It stores device IDs and keys toouse as security credentials, and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="5ff19-118">Uygulamanızın cihaza özgü diğer meta verileri toostore gerekiyorsa, bir uygulamaya özgü depo kullanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5ff19-118">If your application needs toostore other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="5ff19-119">Daha fazla bilgi için bkz. [IoT Hub geliştirici kılavuzu][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="5ff19-119">For more information, see [IoT Hub developer guide][lnk-devguide-identity].</span></span>

<!-- Images. -->
[img-find-iothub]: ./media/iot-hub-get-started-create-device-identity-portal/find-iothub.png
[img-create-device]: ./media/iot-hub-get-started-create-device-identity-portal/create-identity-portal.png
[img-connection-string]: ./media/iot-hub-get-started-create-device-identity-portal/device-connection-string.png


<!-- Links -->
[lnk-azure-portal]: https://portal.azure.com
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md

