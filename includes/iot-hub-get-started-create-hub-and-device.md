## <a name="create-an-iot-hub"></a>IoT hub oluşturma

1. Merhaba, [Azure portal](https://portal.azure.com/), tıklatın **yeni** > **nesnelerin interneti** > **IOT hub'ı**.

   ![Hello Azure portal IOT hub oluşturma](../articles/iot-hub/media/iot-hub-create-hub-and-device/1_create-azure-iot-hub-portal.png)
2. Merhaba, **IOT hub'ı** bölmesinde, IOT hub'ınız için bilgisinden hello girin:

     **Ad**: Merhaba IOT hub'ınızın adını girin. Girdiğiniz hello adı geçerli ise, yeşil bir onay işareti görünür.

     **Fiyatlandırma ve ölçek katmanı**: Select hello **F1 - boş** katmanı. Bu seçenek bu tanıtım için yeterlidir. Daha fazla bilgi için bkz: Merhaba [fiyatlandırma ve ölçek katmanı](https://azure.microsoft.com/pricing/details/iot-hub/).

     **Kaynak grubu**: bir kaynak grubu toohost hello IOT hub oluşturmanız veya mevcut bir kullanın. Daha fazla bilgi için bkz: [kullanım kaynak gruplarını toomanage Azure kaynaklarınızı](../articles/azure-resource-manager/resource-group-portal.md).

     **Konum**: Merhaba hello IOT hub'ı oluşturulduğu en yakın konumu tooyou seçin.

     **PIN toodashboard**: hello panodan tooyour IOT hub'ı kolay erişim için bu seçeneği belirleyin.

   ![IOT hub'ınızı bilgi toocreate girin](../articles/iot-hub/media/iot-hub-create-hub-and-device/2_fill-in-fields-for-azure-iot-hub-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]

3. **Oluştur**'a tıklayın. IOT hub'ınızı birkaç dakika toocreate alabilir. Merhaba ediyor görebilirsiniz **bildirimleri** bölmesi.

   ![IoT hub’ınıza ilişkin ilerleme durumu bildirimlerine bakın](../articles/iot-hub/media/iot-hub-create-hub-and-device/3_notification-azure-iot-hub-creation-progress-portal.png)

4. IOT hub'ınızı oluşturulduktan sonra Başlangıç panosunda'ı tıklatın. Merhaba Not **ana bilgisayar adı**ve ardından **paylaşılan erişim ilkeleri**.

   ![IOT hub'ınızın Hello konak adını Al](../articles/iot-hub/media/iot-hub-create-hub-and-device/4_get-azure-iot-hub-hostname-portal.png)

5. Merhaba, **paylaşılan erişim ilkeleri** bölmesinde hello tıklatın **iothubowner** İlkesi ve ardından Kopyala ve not edin hello **bağlantı dizesi** IOT hub'ınızın. Daha fazla bilgi için bkz: [Denetim erişim tooIoT Hub](../articles/iot-hub/iot-hub-devguide-security.md).

> [!NOTE] 
Bu kurulum öğreticisinde bu iothubowner bağlantı dizesi gerekli değildir. Ancak, bu kurulum tamamlandıktan sonra bazı farklı IOT senaryolarını hello öğretici için gerekebilir.

   ![IoT hub bağlantı dizenizi alma](../articles/iot-hub/media/iot-hub-create-hub-and-device/5_get-azure-iot-hub-connection-string-portal.png)

## <a name="register-a-device-in-hello-iot-hub-for-your-device"></a>Merhaba IOT hub, cihazınız için bir cihaz kaydetme

1. Merhaba, [Azure portal](https://portal.azure.com/), IOT hub'ınızı açın.

2. **Device Explorer**’a tıklayın.
3. Merhaba aygıt Gezgini bölmesinde **Ekle** tooadd bir aygıt tooyour IOT hub'ı. Ardından aşağıdaki hello:

   **Cihaz kimliği**: hello hello yeni cihaz Kimliğini girin. Cihaz Kimlikleri büyük/küçük harfe duyarlıdır.

   **Kimlik Doğrulama Türü**: **Simetrik Anahtar**’ı seçin.

   **Anahtarları Otomatik Onayla**: Bu onay kutusunu işaretleyin.

   **Aygıt tooIoT Hub bağlanmak**: tıklatın **etkinleştirmek**.

   ![Bir aygıt hello IOT hub'ınızın cihaz Explorer ekleme](../articles/iot-hub/media/iot-hub-create-hub-and-device/6_add-device-in-azure-iot-hub-device-explorer-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

4. **Kaydet** düğmesine tıklayın.
5. Merhaba aygıt oluşturulduktan sonra hello aygıt hello açmak **aygıt Explorer** bölmesi.
6. Merhaba bağlantı dizesi hello birincil anahtarı not edin.

   ![Merhaba cihaz bağlantı dizesi Al](../articles/iot-hub/media/iot-hub-create-hub-and-device/7_get-device-connection-string-in-device-explorer-portal.png)
