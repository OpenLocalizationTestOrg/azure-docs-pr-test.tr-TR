## <a name="create-an-iot-hub"></a>IoT hub oluşturma
Bir IOT hub, sanal cihaz uygulaması tooconnect için oluşturun. Merhaba aşağıdaki adımlar, toocomplete bu nasıl görev tarafından gösterir hello Azure portal kullanarak.

1. İçinde toohello oturum [Azure portal][lnk-portal].
1. Hello harf çubuğu, tıklatın **yeni** > **nesnelerin interneti** > **IOT hub'ı**.
   
    ![Azure portalı Atlama Çubuğu][1]
1. Merhaba, **IOT hub'ı** dikey penceresinde hello IOT hub'ınız için yapılandırmayı seçin.
   
    ![IOT hub'ı dikey penceresi][2]
   
   1. Merhaba, **adı** kutusuna, IOT hub'ınız için bir ad girin. Merhaba, **adı** geçerli olduğundan ve kullanılabilir yeşil bir onay işareti hello görünür **adı** kutusu.
    [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]
   
   1. Bir [fiyatlandırma ve ölçek katmanı][lnk-pricing] seçin. Bu öğretici için belirli bir katman gerekmez. Bu öğretici için hello ücretsiz F1 katmanını kullanın.
   1. **Kaynak grubunda** bir kaynak grubu oluşturun veya var olan bir kaynak grubunu seçin. Daha fazla bilgi için bkz: [Azure kaynaklarınızı grupları toomanage kaynağı kullanan][lnk-resource-groups].
   1. İçinde **konumu**, seçin, IOT hub'ınızı konumu toohost hello. Bu öğretici için en yakın konumunuzu seçin.
1. IoT hub'ı yapılandırma seçeneklerinizi seçtiğinizde **Oluştur**'a tıklayın.  Bu IOT hub'ınızı Azure toocreate birkaç dakika sürebilir. toocheck hello durum hello Sabitle veya hello bildirimleri panelinde hello ilerlemesini izleyebilirsiniz.
   
    ![Yeni IOT hub'ı durumu][3]
1. Merhaba IOT hub'ı başarıyla oluşturuldu, IOT hub'hello Azure portal tooopen hello dikey penceresinde hello yeni IOT hub'ına yönelik hello yeni kutucuğa tıklayın. Merhaba Not **ana bilgisayar adı**ve ardından **paylaşılan erişim ilkeleri**.
   
    ![Yeni IOT hub'ı dikey penceresi][4]
1. Merhaba, **paylaşılan erişim ilkeleri** dikey penceresinde hello tıklatın **iothubowner** İlkesi, kopyalayabilir ve hello IOT Hub bağlantı dizesine hello Not **iothubowner** dikey. Daha fazla bilgi için bkz: [erişim denetimi] [ lnk-access-control] içinde hello "IOT Hub Geliştirici Kılavuzu."
   
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
