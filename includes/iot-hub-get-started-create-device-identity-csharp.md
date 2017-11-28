## <a name="create-a-device-identity"></a><span data-ttu-id="5d87f-101">Cihaz kimliği oluşturma</span><span class="sxs-lookup"><span data-stu-id="5d87f-101">Create a device identity</span></span>
<span data-ttu-id="5d87f-102">Bu bölümde, IoT hub'ınızdaki kimlik kayıt defterinde cihaz kimliği oluşturan bir .NET konsol uygulaması oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="5d87f-102">In this section, you create a .NET console app that creates a device identity in the identity registry in your IoT hub.</span></span> <span data-ttu-id="5d87f-103">Kimlik kayıt defterinde girişi olmayan bir cihaz IoT hub'ına bağlanamaz.</span><span class="sxs-lookup"><span data-stu-id="5d87f-103">A device cannot connect to IoT hub unless it has an entry in the identity registry.</span></span> <span data-ttu-id="5d87f-104">Daha fazla bilgi için [IoT Hub geliştirici kılavuzunun][lnk-devguide-identity] "Kimlik kayıt defteri" bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="5d87f-104">For more information, see the "Identity registry" section of the [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="5d87f-105">Bu konsol uygulamasını çalıştırdığınızda, cihazınızın IoT Hub'a cihaz-bulut iletileri gönderdiğinde kendisini tanımlamak için kullanabileceği benzersiz bir cihaz kimliği ve anahtarı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="5d87f-105">When you run this console app, it generates a unique device ID and key that your device can use to identify itself when it sends device-to-cloud messages to IoT Hub.</span></span> <span data-ttu-id="5d87f-106">Cihaz Kimlikleri büyük/küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="5d87f-106">Device IDs are case sensitive.</span></span>

1. <span data-ttu-id="5d87f-107">Visual Studio’da **Konsol Uygulaması (.NET Framework)** proje şablonunu kullanarak yeni bir çözüme bir Visual C# Windows Klasik Masaüstü projesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5d87f-107">In Visual Studio, add a Visual C# Windows Classic Desktop project to a new solution by using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="5d87f-108">.NET Framework sürümünün 4.5.1 veya sonraki bir sürüm olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="5d87f-108">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="5d87f-109">Projeyi **CreateDeviceIdentity** ve çözümü **IoTHubGetStarted** olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="5d87f-109">Name the project **CreateDeviceIdentity** and name the solution **IoTHubGetStarted**.</span></span>
   
    ![Yeni Visual C# Windows Klasik Masaüstü projesi][10]
2. <span data-ttu-id="5d87f-111">Çözüm Gezgini'nde **CreateDeviceIdentity** projesine sağ tıklayın ve ardından **NuGet Paketlerini Yönet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5d87f-111">In Solution Explorer, right-click the **CreateDeviceIdentity** project, and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="5d87f-112">**NuGet Paket Yöneticisi** penceresinde **Gözat**'ı seçin, **microsoft.azure.devices**'ı aratın, **Microsoft.Azure.Devices** paketini yüklemek için **Yükle**'yi seçin ve kullanım koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="5d87f-112">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="5d87f-113">Bu yordam ile [Azure IoT hizmet SDK'sı][lnk-nuget-service-sdk] NuGet paketi ve bağımlılıkları indirilir, yüklenir ve bu pakete bir başvuru eklenir.</span><span class="sxs-lookup"><span data-stu-id="5d87f-113">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet Paket Yöneticisi penceresi][11]
4. <span data-ttu-id="5d87f-115">Aşağıdaki `using` deyimlerini **Program.cs** dosyasının üst kısmına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="5d87f-115">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Common.Exceptions;
5. <span data-ttu-id="5d87f-116">**Program** sınıfına aşağıdaki alanları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5d87f-116">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="5d87f-117">Yer tutucu değerini, önceki bölümde hub için oluşturduğunuz IoT Hub bağlantı dizesiyle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="5d87f-117">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="5d87f-118">**Program** sınıfına aşağıdaki yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="5d87f-118">Add the following method to the **Program** class:</span></span>
   
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
   
    <span data-ttu-id="5d87f-119">Bu yöntem, **myFirstDevice** kimliği ile bir cihaz kimliği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5d87f-119">This method creates a device identity with ID **myFirstDevice**.</span></span> <span data-ttu-id="5d87f-120">(Bu cihaz kimliği, kimlik kayıt defterinde zaten varsa, kod yalnızca mevcut cihaz bilgilerini alır.) Bu durumda uygulama, bu kimliğin birincil anahtarını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="5d87f-120">(If that device ID already exists in the identity registry, the code simply retrieves the existing device information.) The app then displays the primary key for that identity.</span></span> <span data-ttu-id="5d87f-121">IoT hub'ınıza bağlanmak için sanal cihaz uygulamasında bu anahtarı kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="5d87f-121">You use this key in the simulated device app to connect to your IoT hub.</span></span>
[!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

7. <span data-ttu-id="5d87f-122">Son olarak, **Main** yöntemine aşağıdaki satırları ekleyin:</span><span class="sxs-lookup"><span data-stu-id="5d87f-122">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddDeviceAsync().Wait();
        Console.ReadLine();
8. <span data-ttu-id="5d87f-123">Bu uygulamayı çalıştırın ve cihaz anahtarını not edin.</span><span class="sxs-lookup"><span data-stu-id="5d87f-123">Run this application, and make a note of the device key.</span></span>
   
    ![Uygulama tarafından üretilen cihaz anahtarı][12]

> [!NOTE]
> <span data-ttu-id="5d87f-125">IoT Hub kimlik kayıt defteri, yalnızca IoT hub'ına güvenli erişim sağlamak amacıyla cihaz kimliklerini depolar.</span><span class="sxs-lookup"><span data-stu-id="5d87f-125">The IoT Hub identity registry only stores device identities to enable secure access to the IoT hub.</span></span> <span data-ttu-id="5d87f-126">Güvenlik kimlik bilgileri olarak kullanılmak üzere cihaz kimliklerini ve anahtarlarını ve tek bir cihaza erişimi devre dışı bırakmak için kullanabileceğiniz etkin/devre dışı bayrağını depolar.</span><span class="sxs-lookup"><span data-stu-id="5d87f-126">It stores device IDs and keys to use as security credentials, and an enabled/disabled flag that you can use to disable access for an individual device.</span></span> <span data-ttu-id="5d87f-127">Uygulamanızın cihaza özgü diğer meta verileri depolaması gerekiyorsa uygulamaya özgü bir depo kullanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5d87f-127">If your application needs to store other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="5d87f-128">Daha fazla bilgi için bkz. [IoT Hub geliştirici kılavuzu][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="5d87f-128">For more information, see [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 

<!-- Images. -->
[10]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp1.png
[11]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp2.png
[12]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp3.png


<!-- Links -->
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
