## <a name="create-a-device-identity"></a>Cihaz kimliği oluşturma
Bu bölümde, hello kimlik IOT hub'ınızı kayıt defterinde bir cihaz kimliği oluşturan bir .NET konsol uygulaması oluşturun. Merhaba kimlik kayıt defterinde girişi olmayan sürece bir aygıt tooIoT hub bağlanamıyor. Daha fazla bilgi için hello hello "Kimlik kayıt defteri" bölümüne bakın [IOT Hub Geliştirici Kılavuzu][lnk-devguide-identity]. Bu konsol uygulamasını çalıştırdığınızda, benzersiz cihaz kimliği oluşturur ve cihaz bulut gönderdiğinde Cihazınızı tooidentify kendisini kullanabileceğiniz anahtar tooIoT Hub iletileri. Cihaz Kimlikleri büyük/küçük harfe duyarlıdır.

1. Visual Studio'da hello kullanarak bir Visual C# Windows Klasik Masaüstü projesi tooa yeni çözüm Ekle **konsol uygulaması (.NET Framework)** proje şablonu. Merhaba .NET Framework sürümünün 4.5.1 olduğundan emin olun veya sonraki bir sürümü. Ad hello proje **CreateDeviceIdentity** ve ad hello çözümü **IoTHubGetStarted**.
   
    ![Yeni Visual C# Windows Klasik Masaüstü projesi][10]
2. Çözüm Gezgini'nde hello sağ **CreateDeviceIdentity** proje ve ardından **NuGet paketlerini Yönet**.
3. Merhaba, **NuGet Paket Yöneticisi** penceresinde, seçin **Gözat**, arama **microsoft.azure.devices**seçin **yükleme** tooinstall Merhaba **Microsoft.Azure.Devices** paketini ve hello kullanım koşullarını kabul edin. Bu yordam indirir, yükler ve başvuru toohello ekler [Azure IOT hizmeti SDK'sını] [ lnk-nuget-service-sdk] NuGet paketi ve bağımlılıklarını.
   
    ![NuGet Paket Yöneticisi penceresi][11]
4. Merhaba aşağıdakileri ekleyin `using` deyimleri hello hello üstündeki **Program.cs** dosyası:
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Common.Exceptions;
5. Aşağıdaki alanları toohello hello eklemek **Program** sınıfı. Merhaba hello önceki bölümde oluşturduğunuz hello hub'ın IOT Hub bağlantı dizesine sahip Hello yer tutucu değerini değiştirin.
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
6. Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı:
   
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
   
    Bu yöntem, **myFirstDevice** kimliği ile bir cihaz kimliği oluşturur. (Bu cihaz kimliği hello kimlik kayıt defterinde zaten varsa, hello kodu yalnızca hello var olan cihaz bilgilerini alır.) Merhaba uygulama daha sonra bu kimliğin birincil anahtar hello görüntüler. Benzetimli hello cihaz uygulama tooconnect tooyour IOT hub'da bu anahtarı kullanın.
[!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

7. Son olarak, aşağıdaki satırları toohello hello eklemek **ana** yöntemi:
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddDeviceAsync().Wait();
        Console.ReadLine();
8. Bu uygulamayı çalıştırın ve hello cihaz anahtarını not edin.
   
    ![Merhaba uygulama tarafından üretilen cihaz anahtarı][12]

> [!NOTE]
> Merhaba IOT Hub kimlik kayıt defteri, yalnızca cihaz kimlikleri tooenable güvenli erişim toohello IOT hub'ı depolar. Cihaz kimliklerini ve anahtarlarını toouse güvenlik kimlik bilgileri ve toodisable erişim için tek bir cihaza kullanabilirsiniz bir etkin/devre dışı bayrağını depolar. Uygulamanızın cihaza özgü diğer meta verileri toostore gerekiyorsa, bir uygulamaya özgü depo kullanması gerekir. Daha fazla bilgi için bkz. [IoT Hub geliştirici kılavuzu][lnk-devguide-identity].
> 
> 

<!-- Images. -->
[10]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp1.png
[11]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp2.png
[12]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp3.png


<!-- Links -->
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
