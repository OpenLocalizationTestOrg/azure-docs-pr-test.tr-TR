## <a name="create-a-device-identity"></a>Cihaz kimliği oluşturma

Bu bölümde, kullandığınız hello [Azure portal] [ lnk-azure-portal] toocreate hello kimlik IOT hub'ınızı kayıt defterinde bir cihaz kimliği. Merhaba kimlik kayıt defterinde girişi olmayan sürece bir aygıt tooIoT hub bağlanamıyor. Daha fazla bilgi için hello hello "Kimlik kayıt defteri" bölümüne bakın [IOT Hub Geliştirici Kılavuzu][lnk-devguide-identity]. Merhaba **aygıt Explorer** hello portal benzersiz cihaz kimliği ve anahtarı tooIoT hub'a bağlandığında Cihazınızı tooidentify kendisini kullanabilir oluşturmanıza yardımcı olur. Cihaz Kimlikleri büyük/küçük harfe duyarlıdır.

1. İçinde toohello oturumunuz emin olun [Azure portal][lnk-azure-portal].

1. Hello harf çubuğu, tıklatın **tüm kaynakları** ve IOT hub'ı kaynağınız bulabilirsiniz.

    ![Tooyour IOT hub'ı gidin][img-find-iothub]

1. IOT hub'ı kaynağınız açıldığında hello tıklatın **aygıt Explorer** aracı ve ardından **Ekle** hello üstünde. Hello için yeni Cihazınızı gibi ad **myDeviceId**, tıklatıp **kaydetmek**.

    ![Portalda cihaz kimliği oluşturma][img-create-device]

   Bu IOT hub'ınız için yeni bir cihaz kimliği oluşturur.

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

1. Merhaba, **aygıt Explorer**'s aygıt listesinde yeni oluşturulan hello aygıt tıklayın ve hello Not **bağlantı dizesi---birincil anahtar**. 

    ![Cihaz bağlantı dizesi][img-connection-string]

> [!NOTE]
> Merhaba IOT Hub kimlik kayıt defteri, yalnızca cihaz kimlikleri tooenable güvenli erişim toohello IOT hub'ı depolar. Cihaz kimliklerini ve anahtarlarını toouse güvenlik kimlik bilgileri ve toodisable erişim için tek bir cihaza kullanabilirsiniz bir etkin/devre dışı bayrağını depolar. Uygulamanızın cihaza özgü diğer meta verileri toostore gerekiyorsa, bir uygulamaya özgü depo kullanması gerekir. Daha fazla bilgi için bkz. [IoT Hub geliştirici kılavuzu][lnk-devguide-identity].

<!-- Images. -->
[img-find-iothub]: ./media/iot-hub-get-started-create-device-identity-portal/find-iothub.png
[img-create-device]: ./media/iot-hub-get-started-create-device-identity-portal/create-identity-portal.png
[img-connection-string]: ./media/iot-hub-get-started-create-device-identity-portal/device-connection-string.png


<!-- Links -->
[lnk-azure-portal]: https://portal.azure.com
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md

