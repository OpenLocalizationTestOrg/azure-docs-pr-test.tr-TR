## <a name="view-device-telemetry-in-hello-dashboard"></a>Görünüm cihaz telemetrisi hello panosunda
Uzaktan izleme çözümü sağlar, tooview hello telemetri aygıtlarınızı tooIoT Hub Gönder hello panosunda Hello.

1. Tarayıcınızda dönüş toohello Uzaktan izleme çözüm panosunu, tıklatın **aygıtları** hello Sol paneli toonavigate toohello içinde **cihazlar listesi**.
2. Merhaba, **cihazlar listesi**, Cihazınızı hello durumunu olduğunu görmeniz gerekir **çalıştıran**. Aksi durumda, tıklatın **aygıtı etkinleştir** hello içinde **cihaz ayrıntıları** paneli.
   
    ![Cihaz durumunu görüntüle][18]
3. Tıklatın **Pano** tooreturn toohello Pano hello Cihazınızı seçin **aygıt tooView** açılan tooview kendi telemetri. Merhaba telemetri hello örnek uygulamadan iç sıcaklık için 50 birime, 55 birimleri için dış sıcaklık ve nem için 50 birime ' dir.
   
    ![Cihaz telemetrisini görüntüleme][img-telemetry]

## <a name="invoke-a-method-on-your-device"></a>Cihazınızda bir yöntem çağırma
Hello Pano hello Uzaktan izleme çözümünde IOT hub'ı aracılığıyla aygıtlarınızdaki tooinvoke yöntemleri sağlar. Örneğin, hello Uzaktan izleme çözümü, bir aygıt yeniden başlatma yöntemini toosimulate çağırabilirsiniz.

1. Merhaba Uzaktan izleme çözüm panosunda, tıklatın **aygıtları** hello Sol paneli toonavigate toohello içinde **cihazlar listesi**.
2. Tıklatın **cihaz kimliği** aygıtınızın hello **cihazlar listesi**.
3. Merhaba, **cihaz ayrıntıları** öğesine tıklayın **yöntemleri**.
   
    ![Cihaz yöntemleri][13]
4. Merhaba, **yöntemi** açılan listesinde, select **InitiateFirmwareUpdate**ve ardından **FWPACKAGEURI** sahte bir URL girin. Tıklatın **yöntemi çağırma** hello aygıtta toocall hello yöntemi.
   
    ![Cihaz yöntemi çağırma][14]
   

5. Merhaba aygıt hello yöntemi işlediğinde aygıt kodunuzu çalıştırmaya hello konsolunda bir ileti görür. Merhaba yöntemi Hello sonuçlarını toohello geçmişi hello çözüm portalında eklendi:

    ![Yöntem geçmişini görüntüleme][img-method-history]

## <a name="next-steps"></a>Sonraki adımlar
Merhaba makale [özelleştirme önceden yapılandırılmış çözümleri] [ lnk-customize] Bu örnek genişletebilir bazı yolları açıklanmaktadır. Gerçek sensörler kullanma ve ek komutlar uygulama gibi eklemeler yapabilirsiniz.

Merhaba hakkında daha fazla bilgiyi [hello azureiotsuite.com sitesindeki izinler][lnk-permissions].

[13]: ./media/iot-suite-visualize-connecting/suite4.png
[14]: ./media/iot-suite-visualize-connecting/suite7-1.png
[18]: ./media/iot-suite-visualize-connecting/suite10.png
[img-telemetry]: ./media/iot-suite-visualize-connecting/telemetry.png
[img-method-history]: ./media/iot-suite-visualize-connecting/history.png
[lnk-customize]: ../articles/iot-suite/iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-permissions]: ../articles/iot-suite/iot-suite-permissions.md
