## <a name="create-a-device-identity"></a><span data-ttu-id="83377-101">Cihaz kimliği oluşturma</span><span class="sxs-lookup"><span data-stu-id="83377-101">Create a device identity</span></span>
<span data-ttu-id="83377-102">Bu bölümde, hello kimlik IOT hub'ınızı kayıt defterinde bir cihaz kimliği oluşturan bir .NET konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="83377-102">In this section, you create a .NET console app that creates a device identity in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="83377-103">Merhaba kimlik kayıt defterinde girişi olmayan sürece bir aygıt tooIoT hub bağlanamıyor.</span><span class="sxs-lookup"><span data-stu-id="83377-103">A device cannot connect tooIoT hub unless it has an entry in hello identity registry.</span></span> <span data-ttu-id="83377-104">Daha fazla bilgi için hello hello "Kimlik kayıt defteri" bölümüne bakın [IOT Hub Geliştirici Kılavuzu][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="83377-104">For more information, see hello "Identity registry" section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="83377-105">Bu konsol uygulamasını çalıştırdığınızda, benzersiz cihaz kimliği oluşturur ve cihaz bulut gönderdiğinde Cihazınızı tooidentify kendisini kullanabileceğiniz anahtar tooIoT Hub iletileri.</span><span class="sxs-lookup"><span data-stu-id="83377-105">When you run this console app, it generates a unique device ID and key that your device can use tooidentify itself when it sends device-to-cloud messages tooIoT Hub.</span></span> <span data-ttu-id="83377-106">Cihaz Kimlikleri büyük/küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="83377-106">Device IDs are case sensitive.</span></span>

1. <span data-ttu-id="83377-107">Visual Studio'da hello kullanarak bir Visual C# Windows Klasik Masaüstü projesi tooa yeni çözüm Ekle **konsol uygulaması (.NET Framework)** proje şablonu.</span><span class="sxs-lookup"><span data-stu-id="83377-107">In Visual Studio, add a Visual C# Windows Classic Desktop project tooa new solution by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="83377-108">Merhaba .NET Framework sürümünün 4.5.1 olduğundan emin olun veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="83377-108">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="83377-109">Ad hello proje **CreateDeviceIdentity** ve ad hello çözümü **IoTHubGetStarted**.</span><span class="sxs-lookup"><span data-stu-id="83377-109">Name hello project **CreateDeviceIdentity** and name hello solution **IoTHubGetStarted**.</span></span>
   
    ![Yeni Visual C# Windows Klasik Masaüstü projesi][10]
2. <span data-ttu-id="83377-111">Çözüm Gezgini'nde hello sağ **CreateDeviceIdentity** proje ve ardından **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="83377-111">In Solution Explorer, right-click hello **CreateDeviceIdentity** project, and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="83377-112">Merhaba, **NuGet Paket Yöneticisi** penceresinde, seçin **Gözat**, arama **microsoft.azure.devices**seçin **yükleme** tooinstall Merhaba **Microsoft.Azure.Devices** paketini ve hello kullanım koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="83377-112">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="83377-113">Bu yordam indirir, yükler ve başvuru toohello ekler [Azure IOT hizmeti SDK'sını] [ lnk-nuget-service-sdk] NuGet paketi ve bağımlılıklarını.</span><span class="sxs-lookup"><span data-stu-id="83377-113">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet Paket Yöneticisi penceresi][11]
4. <span data-ttu-id="83377-115">Merhaba aşağıdakileri ekleyin `using` deyimleri hello hello üstündeki **Program.cs** dosyası:</span><span class="sxs-lookup"><span data-stu-id="83377-115">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Common.Exceptions;
5. <span data-ttu-id="83377-116">Aşağıdaki alanları toohello hello eklemek **Program** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="83377-116">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="83377-117">Merhaba hello önceki bölümde oluşturduğunuz hello hub'ın IOT Hub bağlantı dizesine sahip Hello yer tutucu değerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="83377-117">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="83377-118">Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="83377-118">Add hello following method toohello **Program** class:</span></span>
   
        private static async Task AddDeviceAsync()
        {
            string deviceId = "myFirstDevice";
            Device device;
            try
            {
                device = await registryManager.AddDeviceAsync(new Device(deviceId));
            }
            catch (DeviceAlreadyExistsException)
            {
                device = await registryManager.GetDeviceAsync(deviceId);
            }
            Console.WriteLine("Generated device key: {0}", device.Authentication.SymmetricKey.PrimaryKey);
        }
   
    <span data-ttu-id="83377-119">Bu yöntem, **myFirstDevice** kimliği ile bir cihaz kimliği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="83377-119">This method creates a device identity with ID **myFirstDevice**.</span></span> <span data-ttu-id="83377-120">(Bu cihaz kimliği hello kimlik kayıt defterinde zaten varsa, hello kodu yalnızca hello var olan cihaz bilgilerini alır.) Merhaba uygulama daha sonra bu kimliğin birincil anahtar hello görüntüler.</span><span class="sxs-lookup"><span data-stu-id="83377-120">(If that device ID already exists in hello identity registry, hello code simply retrieves hello existing device information.) hello app then displays hello primary key for that identity.</span></span> <span data-ttu-id="83377-121">Benzetimli hello cihaz uygulama tooconnect tooyour IOT hub'da bu anahtarı kullanın.</span><span class="sxs-lookup"><span data-stu-id="83377-121">You use this key in hello simulated device app tooconnect tooyour IoT hub.</span></span>
[!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

7. <span data-ttu-id="83377-122">Son olarak, aşağıdaki satırları toohello hello eklemek **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="83377-122">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddDeviceAsync().Wait();
        Console.ReadLine();
8. <span data-ttu-id="83377-123">Bu uygulamayı çalıştırın ve hello cihaz anahtarını not edin.</span><span class="sxs-lookup"><span data-stu-id="83377-123">Run this application, and make a note of hello device key.</span></span>
   
    ![Merhaba uygulama tarafından üretilen cihaz anahtarı][12]

> [!NOTE]
> <span data-ttu-id="83377-125">Merhaba IOT Hub kimlik kayıt defteri, yalnızca cihaz kimlikleri tooenable güvenli erişim toohello IOT hub'ı depolar.</span><span class="sxs-lookup"><span data-stu-id="83377-125">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="83377-126">Cihaz kimliklerini ve anahtarlarını toouse güvenlik kimlik bilgileri ve toodisable erişim için tek bir cihaza kullanabilirsiniz bir etkin/devre dışı bayrağını depolar.</span><span class="sxs-lookup"><span data-stu-id="83377-126">It stores device IDs and keys toouse as security credentials, and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="83377-127">Uygulamanızın cihaza özgü diğer meta verileri toostore gerekiyorsa, bir uygulamaya özgü depo kullanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="83377-127">If your application needs toostore other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="83377-128">Daha fazla bilgi için bkz. [IoT Hub geliştirici kılavuzu][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="83377-128">For more information, see [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 

<!-- Images. -->
[10]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp1.png
[11]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp2.png
[12]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp3.png


<!-- Links -->
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
