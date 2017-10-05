---
title: "C üzerinde mbed kullanarak bir cihazı bağlanma | Microsoft Docs"
description: "Bir mbed cihazda çalışan C yazılmış bir uygulama kullanarak Azure IOT paketi önceden yapılandırılmış Uzaktan izleme çözümü bir aygıt bağlanmaya açıklar."
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
ms.openlocfilehash: ef7b78f85a787f8fbe22c0e26aa34f0cd1685d58
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-your-device-to-the-remote-monitoring-preconfigured-solution-mbed"></a>Cihazınızı Uzaktan izleme önceden yapılandırılmış çözümü (mbed) bağlanma

## <a name="scenario-overview"></a>Senaryoya genel bakış
Bu senaryoda aşağıdaki telemetriyi önceden yapılandırılmış uzaktan izleme [çözümüne][lnk-what-are-preconfig-solutions] gönderen bir cihaz oluşturacaksınız:

* Dış ortam sıcaklığı
* İç ortam sıcaklığı
* Nem oranı

Örneği basitleştirmek amacıyla cihaz üzerindeki kod örnek değerler oluşturmaktadır. Ancak cihazınıza gerçek sensörler bağlayıp gerçek telemetri verileri göndererek örneği ileri taşımanızı öneririz.

Cihaz ayrıca çözüm panosundan çağrılan yöntemlere ve çözüm panosunda ayarlanan istenen özellik değerlerine yanıt verebilir.

Bu öğreticiyi tamamlamak için etkin bir Azure hesabınızın olması gerekir. Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü][lnk-free-trial].

## <a name="before-you-start"></a>Başlamadan önce
Cihazınız için kod yazmadan önce, önceden yapılandırılmış uzaktan izleme çözümünüzü ve bu çözümde yeni bir özel cihaz hazırlamanız gerekir.

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a>Önceden yapılandırılmış uzaktan izleme çözümünüzü sağlama
Bu öğreticide oluşturduğunuz cihaz, önceden yapılandırılmış bir [uzaktan izleme][lnk-remote-monitoring] çözümü örneğine veri göndermektedir. Önceden yapılandırılmış uzaktan izleme çözümünüzü henüz Azure hesabınızda hazırlamadıysanız aşağıdaki adımları uygulayın:

1. <https://www.azureiotsuite.com/> sayfasında çözüm oluşturmak için **+** öğesine tıklayın.
2. Çözümünüzü oluşturmak için **Uzaktan izleme** panelindeki **Seç**'e tıklayın.
3. **Uzaktan izleme çözümü oluştur** sayfasında bir **Çözüm adı** belirleyin, dağıtmak istediğiniz **Bölgeyi** seçin ve kullanmak istediğiniz Azure aboneliğini belirtin. Ardından **Çözüm oluştur**'a tıklayın.
4. Sağlama işleminin tamamlanmasını bekleyin.

> [!WARNING]
> Önceden yapılandırılmış çözümler, faturalanabilir Azure hizmetlerini kullanır. Gereksiz ücretlerden kaçınmak için işinizi tamamladıktan sonra önceden yapılandırılmış çözümü aboneliğinizden kaldırmayı unutmayın. Önceden yapılandırılmış çözümü aboneliğinizden tamamen kaldırmak için <https://www.azureiotsuite.com/> sayfasını ziyaret edin.
> 
> 

Uzaktan izleme çözümü için sağlama işlemi tamamlandıktan sonra çözüm panosunu tarayıcınızda açmak için **Başlat**'a tıklayın.

![Çözüm panosu][img-dashboard]

### <a name="provision-your-device-in-the-remote-monitoring-solution"></a>Cihazınızı uzaktan izleme çözümünde sağlama
> [!NOTE]
> Çözümünüzde önceden bir cihaz hazırladıysanız bu adımı atlayabilirsiniz. İstemci uygulamasını oluştururken cihaz kimlik bilgilerini bilmeniz gerekir.
> 
> 

Bir cihazın önceden yapılandırılmış çözüme bağlanabilmesi için geçerli kimlik bilgileriyle kendini IoT Hub üzerinde tanıtması gerekir. Cihaz kimlik bilgilerini çözüm panosundan alabilirsiniz. Cihaz kimlik bilgilerini bu öğreticinin sonraki adımlarında istemci uygulamanıza ekleyebilirsiniz.

Uzaktan izleme çözümünüze cihaz eklemek için çözüm panosunda aşağıdaki adımları tamamlayın:

1. Panonun sol alt köşesinde **Cihaz ekle**'ye tıklayın.
   
   ![Cihaz ekleme][1]
2. **Özel Cihaz** panelinde **Yeni ekle**'ye tıklayın.
   
   ![Özel cihaz ekleme][2]
3. **Kendi Cihaz Kimliğimi tanımlamama izin ver**'i seçin. **cihazım** gibi bir Cihaz Kimliği girin, adın kullanımda olmadığını doğrulamak için **Kimliği denetle**'ye tıklayın ve ardından cihazı hazırlamak için **Oluştur**'a tıklayın.
   
   ![Cihaz kimliği ekleme][3]
4. Cihaz kimlik bilgilerini (Cihaz Kimliği, IoT Hub Ana Bilgisayar Adı ve Cihaz Anahtarı) not edin. İstemci uygulamanız uzaktan izleme çözümüne bağlanmak için bu değerleri kullanır. Sonra da **Bitti**’ye tıklayın.
   
    ![Cihaz kimlik bilgilerini görüntüleme][4]
5. Çözüm panosundaki cihaz listesinden cihazınızı seçin. Ardından **Cihaz Ayrıntıları** panelinde **Cihazı Etkinleştir**'e tıklayın. Cihazınızın durumu **Çalışıyor** olarak değişir. Uzaktan izleme çözümü artık cihazınızdan telemetri verileri alabilir ve cihazınızda yöntemler çağırabilir.

[img-dashboard]: ./media/iot-suite-connecting-devices-mbed/dashboard.png
[1]: ./media/iot-suite-connecting-devices-mbed/suite0.png
[2]: ./media/iot-suite-connecting-devices-mbed/suite1.png
[3]: ./media/iot-suite-connecting-devices-mbed/suite2.png
[4]: ./media/iot-suite-connecting-devices-mbed/suite3.png

[lnk-what-are-preconfig-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

## <a name="build-and-run-the-c-sample-solution"></a>Derleme ve C örnek çözümü çalıştırma

Aşağıdaki yönergeler bağlanmak için gereken adımlar anlatılmaktadır bir [mbed etkin Freescale FRDM K64F] [ lnk-mbed-home] Uzaktan izleme çözümü cihaza.

### <a name="connect-the-mbed-device-to-your-network-and-desktop-machine"></a>Mbed aygıt ağ ve Masaüstü makinenize bağlanın

1. Mbed aygıtı Ethernet kablosu kullanarak ağınıza bağlayın. Örnek uygulama Internet erişimi gerektirdiğinden bu adım gereklidir.

1. Bkz: [mbed ile çalışmaya başlama] [ lnk-mbed-getstarted] masaüstü bilgisayarınıza mbed Cihazınızı bağlamak için.

1. Windows masaüstü bilgisayarınıza çalıştırıyorsa, bkz: [PC yapılandırma] [ lnk-mbed-pcconnect] mbed Cihazınızı seri bağlantı noktası erişimi yapılandırmak için.

### <a name="create-an-mbed-project-and-import-the-sample-code"></a>Bir mbed projesi oluşturun ve örnek kodunu alma

Bazı örnek kod bir mbed projeye eklemek için aşağıdaki adımları izleyin. Uzaktan izleme başlangıç projesi içeri aktarıp MQTT Protokolü yerine AMQP protokolünü kullanmak için proje değiştirin. Şu anda IOT Hub cihaz yönetimi özelliklerini kullanmak için MQTT Protokolü kullanmanız gerekir.

1. Web tarayıcınızda mbed.org Git [Geliştirici site](https://developer.mbed.org/). Kaydolmuş olmasanız (ücretsiz) hesap oluşturmak için bir seçenek görürsünüz. Aksi takdirde, hesap kimlik bilgileriyle oturum açın. Ardından **derleyici** sayfanın sağ üst köşesindeki. Bu eylem getirir *çalışma* arabirimi.

1. Kullanmakta olduğunuz donanım platformu pencerenin sağ üst köşesinde göründüğünden emin olun veya donanım platformunuz seçmek için sağ alt köşesindeki simgesine tıklayın.

1. Tıklatın **alma** ana menüdeki. Ardından **URL'den almak için burayı tıklatın**.
   
    ![Mbed çalışma alanına alma Başlat][6]

1. Açılan pencerede, bağlantı için örnek kod https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/ girin'yi tıklatın **alma**.
   
    ![Örnek kod mbed çalışma alanına alma][7]

1. Bu projeyi içeri aktarma, çeşitli kitaplıkları da alır, mbed derleyici penceresinde görebilirsiniz. Bazı sağlanan ve Azure IOT ekibi tarafından korunan ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/), [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/), [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/), [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/)), diğerleri ise, üçüncü taraf kitaplıklar mbed kitaplıkları Kataloğu'nda kullanılabilir.
   
    ![Görünüm mbed proje][8]

1. İçinde **programın çalışma**, sağ tıklatın **ıothub\_amqp\_aktarım** kitaplığı tıklatın **silmek**ve ardından **Tamam** onaylamak için.

1. İçinde **Program çalışma**, sağ tıklatın **azure\_amqp\_c** kitaplığı tıklatın **silmek**ve ardından **Tamam** onaylamak için.

1. Sağ **remote_monitoring** proje **Program çalışma**seçin **içeri aktarma kitaplığını**seçeneğini belirleyip **URL'den**.
   
    ![Mbed çalışma alanına kitaplığı alma Başlat][6]

1. Açılan pencerede bağlantısı için MQTT taşıma kitaplığı https://developer.mbed.org/users/AzureIoTClient/code/iothub girin\_mqtt\_aktarım / ardından **alma**.
   
    ![İçeri aktarma kitaplığını mbed çalışma][12]

1. Https://developer.mbed.org/users/AzureIoTClient/code/azure MQTT Kitaplığı eklemek için önceki adımı yineleyin\_umqtt\_c /.

1. Çalışma alanınızı şimdi aşağıdaki gibi görünür:

    ![Mbed çalışma alanını görüntüle][13]

1. Uzak açmak\_monitoring\remote_monitoring.c dosya ve varolan Değiştir `#include` deyimleri ile aşağıdaki kodu:

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
1. Tüm kalan kodda uzaktan silme\_monitoring\remote\_monitoring.c dosya.

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-the-sample"></a>Derleme ve örnek çalıştırma

Çağırmak için kodu ekleyin **uzak\_izleme\_çalıştırmak** işlev oluşturmak ve cihaz uygulamayı çalıştırın.

1. Ekleme bir **ana** işlevi uzaktan sonuna aşağıdaki kod ile\_çağrılacak monitoring.c dosya **uzak\_izleme\_çalıştırmak** işlevi:
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. Tıklatın **derleme** program oluşturmak için. Güvenli bir şekilde tüm uyarılarını gözardı ancak derleme hataları oluşturursa devam etmeden önce düzeltin.

1. Yapı başarılı olursa, mbed derleyici Web sitesi projenizin adına sahip bir .bin dosyası oluşturur ve yerel makinenize indirir. .Bin dosyasını aygıtına kopyalayın. Cihaza .bin dosyasını kaydetme yeniden başlatın ve .bin dosyasında yer alan programı çalıştırmak için cihazın neden olur. Mbed aygıtta Sıfırla düğmesine basarak istediğiniz zaman program el ile yeniden başlatabilirsiniz.

1. PuTTY gibi bir SSH istemci uygulaması kullanarak cihazı bağlayın. Windows Aygıt Yöneticisi'ni denetleyerek aygıtınızın kullandığı seri bağlantı noktası belirleyebilirsiniz.
   
    ![][11]

1. PuTTY içinde tıklatın **seri** bağlantı türü. Aygıt genellikle 9600 baud hızında bağlanır, şekilde içinde 9600 girin **hızı** kutusu. Ardından **açık**.

1. Program yürütme başlar. Pano sıfırlamanız gerekebilir (CTRL + Break tuşlarına basın veya panosu'nın Sıfırla düğmesine basın) programı otomatik olarak bağladığınızda başlamazsa.
   
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
