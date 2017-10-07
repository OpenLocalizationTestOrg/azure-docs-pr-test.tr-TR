---
title: "C üzerinde mbed kullanarak cihazı aaaConnect | Microsoft Docs"
description: "Nasıl tooconnect aygıt toohello Azure IOT paketi Uzaktan izleme çözümü mbed cihazda çalışan C yazılmış bir uygulama kullanarak önceden yapılandırılmış açıklar."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 9551075e-dcf9-488f-943e-d0eb0e6260be
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: dobett
ROBOTS: NOINDEX
ms.openlocfilehash: dcd1e74635e8dec678a59bff060a73f7cfabd124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-mbed"></a>Uzaktan izleme çözümü (mbed), cihaz toohello Bağlan

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

1. Merhaba üzerinde <https://www.azureiotsuite.com/> sayfasında, ** + ** toocreate bir çözüm.
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

[img-dashboard]: ./media/iot-suite-connecting-devices-mbed/dashboard.png
[1]: ./media/iot-suite-connecting-devices-mbed/suite0.png
[2]: ./media/iot-suite-connecting-devices-mbed/suite1.png
[3]: ./media/iot-suite-connecting-devices-mbed/suite2.png
[4]: ./media/iot-suite-connecting-devices-mbed/suite3.png

[lnk-what-are-preconfig-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

## <a name="build-and-run-hello-c-sample-solution"></a>Derleme ve çalıştırma hello C örnek çözümü

Merhaba aşağıdaki yönergeler açıklar hello adımları bağlanmak için bir [mbed etkin Freescale FRDM K64F] [ lnk-mbed-home] aygıt toohello Uzaktan izleme çözümü.

### <a name="connect-hello-mbed-device-tooyour-network-and-desktop-machine"></a>Merhaba mbed aygıt tooyour ağ ve Masaüstü makine Bağlan

1. Merhaba mbed aygıt tooyour ağ Ethernet kablosu kullanarak bağlanın. Bu adım gerekli çünkü Hello örnek uygulama Internet erişimi gerektirir.

1. Bkz: [mbed ile çalışmaya başlama] [ lnk-mbed-getstarted] tooconnect mbed aygıt tooyour masaüstü bilgisayar.

1. Windows masaüstü bilgisayarınıza çalıştırıyorsa, bkz: [PC yapılandırma] [ lnk-mbed-pcconnect] tooconfigure seri bağlantı noktası erişim tooyour mbed aygıtı.

### <a name="create-an-mbed-project-and-import-hello-sample-code"></a>Bir mbed projesi oluşturun ve hello örnek kodunu alma

Bu adımları tooadd bazı örnek kod tooan mbed proje izleyin. Merhaba Uzaktan izleme başlangıç projesi içeri aktarıp hello proje toouse hello hello AMQP protokolünü yerine MQTT protokol değiştirin. Şu anda toouse hello MQTT Protokolü toouse hello cihaz yönetim özellikleri IOT hub'ı gerekir.

1. Web tarayıcınızda toohello mbed.org Git [Geliştirici site](https://developer.mbed.org/). Kaydolmuş olmasanız seçeneği toocreate (boş) bir hesap görürsünüz. Aksi takdirde, hesap kimlik bilgileriyle oturum açın. Ardından **derleyici** hello sağ üst köşesinde hello sayfa içinde. Bu eylem toohello getirir *çalışma* arabirimi.

1. Kullanmakta olduğunuz hello donanım platformu hello sağ üst köşesinde hello penceresi içinde görüntülenir veya hello hello sağ köşesindeki tooselect donanım platformunuz simgesini emin olun.

1. Tıklatın **alma** hello ana menüsündeki. Ardından **tooimport URL'den burayı**.
   
    ![Başlangıç alma toombed çalışma][6]

1. Merhaba açılır penceresinde hello bağlantı hello örnek kodu https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/ için girin'yi tıklatın **alma**.
   
    ![Örnek kod toombed çalışma alma][7]

1. Bu projeyi içeri aktarma, çeşitli kitaplıkları da alır, hello mbed derleyici penceresinde görebilirsiniz. Bazı sağlanan ve hello Azure IOT ekibi tarafından korunan ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/), [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/), [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/), [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/)), diğerleri ise, üçüncü taraf kitaplıklar hello mbed kitaplıkları Kataloğu'nda kullanılabilir.
   
    ![Görünüm mbed proje][8]

1. Merhaba, **Program çalışma**, sağ hello **ıothub\_amqp\_aktarım** kitaplığı,'ı tıklatın **silmek**ve ardından**Tamam** tooconfirm.

1. Merhaba, **Program çalışma**, sağ hello **azure\_amqp\_c** kitaplığı tıklatın **silmek**ve ardından **Tamam ** tooconfirm.

1. Sağ hello **remote_monitoring** hello bir projede **Program çalışma**seçin **içeri aktarma kitaplığını**seçeneğini belirleyip **URL'den**.
   
    ![Kitaplık alma toombed çalışma Başlat][6]

1. Merhaba açılır penceresinde hello bağlantıyı hello MQTT taşıma kitaplığı https://developer.mbed.org/users/AzureIoTClient/code/iothub için girin\_mqtt\_aktarım / ardından **alma**.
   
    ![Kitaplık toombed çalışma alma][12]

1. Yineleme hello önceki adım tooadd hello MQTT kitaplığındaki https://developer.mbed.org/users/AzureIoTClient/code/azure\_umqtt\_c /.

1. Çalışma alanınızı şimdi hello aşağıdaki gibi görünür:

    ![Mbed çalışma alanını görüntüle][13]

1. Açık hello uzak\_monitoring\remote_monitoring.c dosya ve hello Değiştir varolan `#include` koddan hello ifadelerle:

    ```c
    #include "iothubtransportmqtt.h"
    #include "schemalib.h"
    #include "iothub_client.h"
    #include "serializer_devicetwin.h"
    #include "schemaserializer.h"
    #include "azure_c_shared_utility/threadapi.h"
    #include "azure_c_shared_utility/platform.h"
    #include "parson.h"

    #ifdef MBED_BUILD_TIMESTAMP
    #include "certs.h"
    #endif // MBED_BUILD_TIMESTAMP
    ```
1. Merhaba uzak kodda kalan tüm hello silme\_monitoring\remote\_monitoring.c dosya.

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-hello-sample"></a>Derleme ve hello örnek çalıştırma

Kod tooinvoke hello eklemek **uzak\_izleme\_çalıştırmak** işlev oluşturmak ve hello cihaz uygulamayı çalıştırın.

1. Ekleme bir **ana** işlevi hello uzak hello sonuna aşağıdaki kod ile\_monitoring.c dosya tooinvoke hello **uzak\_izleme\_çalıştırmak** işlevi:
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. Tıklatın **derleme** toobuild hello program. Güvenli bir şekilde tüm uyarılarını gözardı ancak hello derleme hataları oluşturursa devam etmeden önce düzeltin.

1. Merhaba yapı başarılı olursa, hello mbed derleyici Web projenizin hello adla .bin dosyası oluşturur ve tooyour yerel makine indirir. Merhaba .bin dosyasını toohello aygıt kopyalayın. Merhaba .bin dosyasını toohello aygıt kaydetme hello aygıt toorestart neden olur ve hello .bin dosyasının içerdiği hello programını çalıştırın. Merhaba mbed aygıtta hello sıfırlama düğmesine basarak istediğiniz zaman hello program el ile yeniden başlatabilirsiniz.

1. PuTTY gibi bir SSH istemci uygulaması kullanarak toohello aygıtı bağlayın. Windows Aygıt Yöneticisi'ni denetleyerek aygıtınızın kullandığı hello seri bağlantı noktası belirleyebilirsiniz.
   
    ![][11]

1. PuTTY içinde hello tıklatın **seri** bağlantı türü. Hello aygıt genellikle 9600 baud hızında bağlanır, böylece 9600 hello girin **hızı** kutusu. Ardından **açık**.

1. Merhaba program yürütme başlar. Merhaba programı otomatik olarak bağladığınızda başlamazsa tooreset hello Panosu (CTRL + Break veya tuşuna hello panosu'nın Sıfırla düğmesine basın) olabilir.
   
    ![][10]

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[6]: ./media/iot-suite-connecting-devices-mbed/mbed1.png
[7]: ./media/iot-suite-connecting-devices-mbed/mbed2a.png
[8]: ./media/iot-suite-connecting-devices-mbed/mbed3a.png
[10]: ./media/iot-suite-connecting-devices-mbed/putty.png
[11]: ./media/iot-suite-connecting-devices-mbed/mbed6.png
[12]: ./media/iot-suite-connecting-devices-mbed/mbed7.png
[13]: ./media/iot-suite-connecting-devices-mbed/mbed8.png

[lnk-mbed-home]: https://developer.mbed.org/platforms/FRDM-K64F/
[lnk-mbed-getstarted]: https://developer.mbed.org/platforms/FRDM-K64F/#getting-started-with-mbed
[lnk-mbed-pcconnect]: https://developer.mbed.org/platforms/FRDM-K64F/#pc-configuration
