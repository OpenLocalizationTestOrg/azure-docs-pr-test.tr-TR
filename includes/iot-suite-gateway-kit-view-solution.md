## <a name="view-hello-solution-dashboard"></a>Görünüm hello çözüm Panosu

Merhaba çözüm Panosu toomanage dağıtılan hello çözümü sağlar. Örneğin, telemetriyi görüntüleyebilir, cihazları eklemek ve yöntemleri çağırma.

1. Ne zaman hello Sağlama tamamlandıktan ve önceden yapılandırılmış çözümünüzün kutucuğu hello gösterir **hazır**, seçin **başlatma** tooopen Uzaktan izleme çözümü portalınızı yeni bir sekmede.

    ![Merhaba önceden yapılandırılmış çözüm başlatma][img-launch-solution]

1. Varsayılan olarak, hello çözüm portalı hello gösterir *Pano*. Merhaba sol taraftaki hello sayfasının hello menüsünü kullanarak hello çözüm portalı tooother alanlarının gidin.

    ![Önceden yapılandırılmış uzaktan izleme panosu][img-menu]

## <a name="add-a-device"></a>Cihaz ekleme

Bir cihaz tooconnect toohello önceden yapılandırılmış çözümü kendisini tooIoT Hub tanımlamak gerekir geçerli kimlik bilgilerini kullanarak. Merhaba çözüm panodan hello aygıt kimlik bilgilerini alabilirsiniz. Bu öğreticide daha sonra istemci uygulamanızda hello cihaz kimlik bilgileri içerir.

tooadd bir aygıt tooyour Uzaktan izleme çözümü, aşağıdaki tam hello hello çözüm panosunda adımlar:

1. Merhaba sol alt köşedeki hello Pano, tıklatın **bir cihaz ekleme**.

   ![Cihaz ekleme][1]

1. Merhaba, **özel cihaz** öğesine tıklayın **yeni Ekle**.

   ![Özel cihaz ekleme][2]

1. **Kendi Cihaz Kimliğimi tanımlamama izin ver**'i seçin. Bir cihaz kimliği girin **device01**, tıklatın **denetleyin kimliği** hello adı çözümünüzde zaten kullanmadıysanız ve ardından tooverify **oluşturma** tooprovision hello aygıt.

   ![Cihaz kimliği ekleme][3]

1. Kimlik bilgilerini not hello aygıt yapın (**cihaz kimliği**, **IOT Hub ana bilgisayar adına**, ve **aygıt anahtarı**). İstemci uygulamanızı hello Intel NUC üzerinde bu değerleri tooconnect toohello Uzaktan izleme çözümü gerekir. Sonra da **Bitti**’ye tıklayın.

    ![Cihaz kimlik bilgilerini görüntüleme][4]

1. Merhaba çözüm Panosu hello aygıt listesinde aygıtınızı seçin. Ardından hello **cihaz ayrıntıları** öğesine tıklayın **aygıtı etkinleştir**. Merhaba Cihazınızı durumudur şimdi **çalıştıran**. Merhaba Uzaktan izleme çözümü şimdi aygıtınızdan telemetri almasına ve hello aygıtta yöntemleri çağırma.

[img-launch-solution]: media/iot-suite-gateway-kit-view-solution/launch.png
[img-menu]: media/iot-suite-gateway-kit-view-solution/menu.png
[1]: media/iot-suite-gateway-kit-view-solution/suite0.png
[2]: media/iot-suite-gateway-kit-view-solution/suite1.png
[3]: media/iot-suite-gateway-kit-view-solution/suite2.png
[4]: media/iot-suite-gateway-kit-view-solution/suite3.png