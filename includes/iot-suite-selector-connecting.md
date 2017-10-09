> [!div class="op_single_selector"]
> * [Windows üzerinde C](../articles/iot-suite/iot-suite-connecting-devices.md)
> * [Linux üzerinde C](../articles/iot-suite/iot-suite-connecting-devices-linux.md)
> * [Node.js](../articles/iot-suite/iot-suite-connecting-devices-node.md)
> 
> 

## <a name="scenario-overview"></a>Senaryoya genel bakış
Bu senaryoda, telemetri toohello Uzaktan izleme aşağıdaki hello gönderir bir cihaz oluşturma [önceden yapılandırılmış çözüm][lnk-what-are-preconfig-solutions]:

* Dış ortam sıcaklığı
* İç ortam sıcaklığı
* Nem oranı

Basitleştirmek için örnek değerler hello cihazda hello kodu oluşturur, ancak siz tooextend hello örnek gerçek algılayıcılar tooyour aygıt bağlanma ve gerçek telemetri göndermesini öneririz.

Merhaba de mümkün toorespond toomethods hello çözüm panodan çağrılır ve özellik değerleri hello çözüm panosunda istenen aygıttır.

toocomplete Bu öğretici, etkin bir Azure hesabınızın olması gerekir. Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü][lnk-free-trial].

## <a name="before-you-start"></a>Başlamadan önce
Cihazınız için kod yazmadan önce, önceden yapılandırılmış uzaktan izleme çözümünüzü ve bu çözümde yeni bir özel cihaz hazırlamanız gerekir.

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a>Önceden yapılandırılmış uzaktan izleme çözümünüzü sağlama
Bu öğreticide oluşturduğunuz hello cihaz gönderir veri tooan hello örneği [Uzaktan izleme] [ lnk-remote-monitoring] çözüm önceden yapılandırılmış. Uzaktan izleme çözümü Azure hesabınızda hello sağladığınız zaten yapmadıysanız, hello aşağıdaki adımları kullanın:

1. Merhaba üzerinde <https://www.azureiotsuite.com/> sayfasında,  **+**  toocreate bir çözüm.
2. Tıklatın **seçin** hello üzerinde **Uzaktan izleme** çözümünüzü toocreate panel.
3. Hello üzerinde **Uzaktan izleme çözümü oluşturma** want bir **çözüm adı** seçiminizi, hello seçin **bölge** toodeploy için istediğiniz ve hello Azure seçin Abonelik toowant toouse. Ardından **Çözüm oluştur**'a tıklayın.
4. Merhaba sağlama işlemi tamamlanana kadar bekleyin.

> [!WARNING]
> Merhaba önceden yapılandırılmış çözümleri Faturalanabilir Azure Hizmetleri kullanın. Tooremove hello aboneliğiniz önceden yapılandırılmış çözümü ile bittiğinde mutlaka tooavoid gereksiz herhangi bir ücret. Merhaba ziyaret ederek önceden yapılandırılmış bir çözüm aboneliğinizden tamamen kaldırabilirsiniz <https://www.azureiotsuite.com/> sayfası.
> 
> 

Sağlama işlemi hello Uzaktan izleme çözümü için hello tamamlandığında, tıklatın **başlatma** tooopen hello çözüm Panosu tarayıcınızda.

![Çözüm panosu][img-dashboard]

### <a name="provision-your-device-in-hello-remote-monitoring-solution"></a>Cihazınızı Uzaktan izleme çözümü hello sağlama
> [!NOTE]
> Çözümünüzde önceden bir cihaz hazırladıysanız bu adımı atlayabilirsiniz. Merhaba istemci uygulaması oluşturduğunuzda tooknow hello cihaz kimlik bilgileri gerekir.
> 
> 

Bir cihaz tooconnect toohello önceden yapılandırılmış çözümü kendisini tooIoT Hub tanımlamak gerekir geçerli kimlik bilgilerini kullanarak. Merhaba çözüm panodan hello aygıt kimlik bilgilerini alabilirsiniz. Bu öğreticide daha sonra istemci uygulamanızda hello cihaz kimlik bilgileri içerir.

tooadd bir aygıt tooyour Uzaktan izleme çözümü, aşağıdaki tam hello hello çözüm panosunda adımlar:

1. Merhaba sol alt köşedeki hello Pano, tıklatın **bir cihaz ekleme**.
   
   ![Cihaz ekleme][1]
2. Merhaba, **özel cihaz** öğesine tıklayın **yeni Ekle**.
   
   ![Özel cihaz ekleme][2]
3. **Kendi Cihaz Kimliğimi tanımlamama izin ver**'i seçin. Bir cihaz kimliği girin **mydevice**, tıklatın **denetleyin kimliği** tooverify bu ad zaten kullanımda olmadığından ve ardından **oluşturma** tooprovision hello aygıt.
   
   ![Cihaz kimliği ekleme][3]
4. Kimlik bilgilerini (cihaz kimliği, IOT Hub ana bilgisayar adına ve aygıt anahtarı) not hello aygıt olun. İstemci uygulamanız bu değerleri tooconnect toohello Uzaktan izleme çözümü gerekir. Sonra da **Bitti**’ye tıklayın.
   
    ![Cihaz kimlik bilgilerini görüntüleme][4]
5. Merhaba çözüm Panosu hello aygıt listesinde aygıtınızı seçin. Ardından hello **cihaz ayrıntıları** öğesine tıklayın **aygıtı etkinleştir**. Merhaba Cihazınızı durumudur şimdi **çalıştıran**. Merhaba Uzaktan izleme çözümü şimdi aygıtınızdan telemetri almasına ve hello aygıtta yöntemleri çağırma.

[img-dashboard]: ./media/iot-suite-selector-connecting/dashboard.png
[1]: ./media/iot-suite-selector-connecting/suite0.png
[2]: ./media/iot-suite-selector-connecting/suite1.png
[3]: ./media/iot-suite-selector-connecting/suite2.png
[4]: ./media/iot-suite-selector-connecting/suite3.png

[lnk-what-are-preconfig-solutions]: ../articles/iot-suite/iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: ../articles/iot-suite/iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/