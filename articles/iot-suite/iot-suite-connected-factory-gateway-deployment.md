---
title: "Azure IOT paketi bağlı aaaDeploy Fabrika ağ geçidi | Microsoft Docs"
description: "Toodeploy Windows veya Linux tooenable bağlantı toohello üzerinde bir ağ geçidi Fabrika nasıl bağlanacağını çözüm önceden yapılandırılmış."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: dobett
ms.openlocfilehash: 72436dec60eda0de20143f362fe740b0c4412f36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-gateway-on-windows-or-linux-for-hello-connected-factory-preconfigured-solution"></a>Windows veya Linux üzerinde bir ağ geçidi bağlı hello Fabrika önceden yapılandırılmış çözümü dağıtma

Merhaba toodeploy bağlı hello Fabrika önceden yapılandırılmış çözümü için ağ geçidi bir iki bileşenden oluşur gerekli yazılım:

* Merhaba *OPC Proxy* bağlantı tooIoT Hub oluşturur. Merhaba *OPC Proxy* sonra hello bağlı Fabrika çözüm portalında çalışan OPC tarayıcı tümleşik hello komut ve Denetim iletileri bekler.
* Merhaba *OPC yayımcı* tooexisting şirket içi OPC UA sunucularını bağlar ve telemetri iletilerini onlardan tooIoT Hub iletir.

Her iki bileşenler açık kaynaklı ve GitHub kaynağına ve Docker kapsayıcılar olarak kullanılabilir:

| GitHub | DockerHub |
| ------ | --------- |
| [OPC yayımcı][lnk-publisher-github] | [OPC yayımcı][lnk-publisher-docker] |
| [OPC Proxy][lnk-proxy-github] | [OPC Proxy][lnk-proxy-docker] |

Genel kullanıma yönelik IP adresi veya Delik hello ağ geçidi Güvenlik Duvarı'nda ya da bileşen için gerekli değildir. Merhaba OPC Proxy ve OPC yayımcı yalnızca giden bağlantı noktası 443, 5671 ve 8883 kullanın.

Merhaba bu makaledeki adımlarda size yol gösterecektir Docker üzerinde kullanarak ağ geçidi bir toodeploy [Windows](#windows-deployment) veya [Linux](#linux-deployment). Merhaba ağ geçidi bağlantısı bağlı toohello Fabrika önceden yapılandırılmış çözümü sağlar.

> [!NOTE]
> Merhaba Docker kapsayıcısı içinde çalışan hello ağ geçidi yazılım [Azure IOT kenar].

## <a name="windows-deployment"></a>Windows Dağıtım

> [!NOTE]
> Bir ağ geçidi cihazı henüz yoksa, Microsoft ticari bir ağ geçidi ortaklarımızdan birinden satın önerir. Merhaba ziyaret [Azure IOT cihaz katalog] ağ geçidi cihazların Merhaba ile uyumlu bir listesini Fabrika çözüm bağlandı. Merhaba aygıt tooset hello ağ geçidi kurma gelir hello yönergeleri izleyin. Alternatif olarak, varolan geçitlerinizin birinde ayarlama yönergeleri toomanually aşağıdaki hello kullanın.

### <a name="install-docker"></a>Docker yükleyin

Yükleme [Windows için Docker] , Windows tabanlı ağ geçidi Cihazınızda. Windows Docker Kurulum sırasında ana makine tooshare docker'la üzerinde bir sürücü seçin. Merhaba, aşağıdaki Windows sisteminize Hello D sürücü paylaşımı hali gösterilmektedir:

![Docker yükleyin][img-install-docker]

Adlı bir klasör oluşturun **docker** hello hello kökünde paylaşılan sürücü.
Docker hello yükledikten sonra da bu adımı gerçekleştirebilirsiniz **ayarları** menüsü.

### <a name="configure-hello-gateway"></a>Merhaba ağ geçidini yapılandırma

1. Merhaba gereksinim **iothubowner** Azure IOT paketi bağlantı dizesi bağlı Fabrika dağıtım toocomplete hello ağ geçidi dağıtımı. Merhaba, [Azure portal], IOT Hub'hello kaynak grubunda oluşturulan bağlı hello Fabrika çözüm dağıtıldığında tooyour gidin. Tıklatın **paylaşılan erişim ilkeleri** tooaccess hello **iothubowner** bağlantı dizesi:

    ![Hello IOT Hub bağlantı dizesine bulur][img-hub-connection]

    Kopya hello **bağlantı dizesi--birincil anahtar** değeri.

1. Merhaba iki ağ geçidi modülleri çalıştırarak Hello ağ geçidi için IOT Hub'ınızı yapılandırma **sonra** ile bir komut isteminden:

    `docker run -it --rm -h <ApplicationName> -v //D/docker:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/CertificateStores -v //D/docker:/root/.dotnet/corefx/cryptography/x509stores microsoft/iot-gateway-opc-ua:1.0.0 <ApplicationName> "<IoTHubOwnerConnectionString>"`

    `docker run -it --rm -v //D/docker:/mapped microsoft/iot-gateway-opc-ua-proxy:0.1.3 -i -c "<IoTHubOwnerConnectionString>" -D /mapped/cs.db`

    * **&lt;ApplicationName&gt; ** hello biçiminde hello adı toogive tooyour OPC UA yayımcı olan **yayımcı.&lt; tam etki alanı adınızı&gt;**. Örneğin, Fabrika ağ olarak adlandırılır, **myfactorynetwork.com**, hello **ApplicationName** değer **publisher.myfactorynetwork.com**.
    * **&lt;IoTHubOwnerConnectionString&gt; ** hello olan **iothubowner** hello önceki adımda kopyaladığınız bağlantı dizesi. Bu bağlantı dizesini yalnızca bu adımda kullanılır, aşağıdaki adımları hello gerekmez:

    Kullandığınız hello eşlenen D:\\docker klasörü (Merhaba `-v` bağımsız değişkeni) sonraki toopersist hello hello ağ geçidi modülleri kullanan iki X.509 sertifikaları.

### <a name="run-hello-gateway"></a>Merhaba ağ geçidini çalıştırmak

1. Merhaba aşağıdaki komutları kullanarak hello ağ geçidini yeniden başlatın:

    `docker run -it --rm -h <ApplicationName> --expose 62222 -p 62222:62222 -v //D/docker:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/Logs -v //D/docker:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/CertificateStores -v //D/docker:/shared -v //D/docker:/root/.dotnet/corefx/cryptography/x509stores -e _GW_PNFP="/shared/publishednodes.JSON" microsoft/iot-gateway-opc-ua:1.0.0 <ApplicationName>`

    `docker run -it --rm -v //D/docker:/mapped microsoft/iot-gateway-opc-ua-proxy:0.1.3 -D /mapped/cs.db`

1. Güvenlik nedenleriyle hello iki X.509 sertifikalarını hello D: kalıcı\\docker klasör hello özel anahtarı içerir. Sınırlamak erişim toothis klasörü toohello kimlik bilgileri (genellikle **Yöneticiler**) toorun hello Docker kapsayıcısı kullanın. Sağ hello D:\\docker klasörü seçin **özellikleri**, ardından **güvenlik**ve ardından **Düzenle**. Vermek **Yöneticiler** tam denetim ve diğerlerinin kaldırın:

    ![GRANT izinleri tooDocker paylaşımı][img-docker-share]

1. Ağ bağlantısını doğrulayın. Merhaba komutu bir komut isteminden girin `ping publisher.<your fully qualified domain name>` tooping, ağ geçidi. Merhaba hedef erişilemediğinde hello IP adresi ve ağ geçidiniz üzerinde ağ geçidi toohello hosts dosyasının adını ekleyin. Merhaba hosts dosyasını hello bulunan **Windows\\System32\\sürücüleri\\vb.** klasör.

1. Ardından, tooconnect toohello yayımcı hello ağ geçidinde çalıştıran yerel bir OPC UA istemcisi kullanarak deneyin. OPC UA uç noktası URL'si hello `opc.tcp://publisher.<your fully qualified domain name>:62222`. OPC UA istemci yoksa kullanın indirin ve bir [açık kaynak OPC UA istemci].

1. Bu yerel testleri başarıyla tamamladıktan sonra toohello Gözat **kendi OPC UA sunucusuna** hello bağlı Fabrika çözüm portalında sayfası. Merhaba yayımcı uç noktasının URL'sini girin (`tcp://publisher.<your fully qualified domain name>:62222`) tıklatıp **Bağlan**. Bir sertifika uyarısı almak, ardından tıklatın **devam et.** Ardından bu hello bir hata alıyorsunuz yayımcı hello UA Web istemcisi güven değil. tooresolve bu hata, kopyalama hello **UA Web istemcisi** hello sertifikadan **D:\\docker\\reddetti sertifikaları\\sertifikaları** klasörü toohello **D:\\docker\\UA uygulamaları\\sertifikaları** hello ağ geçidinde klasör. Toorestart hello ağ geçidinin zorunda değilsiniz. Bu adımı yineleyin. Merhaba buluttan toohello ağ geçidi artık bağlanabilir ve hazır tooadd OPC UA sunucuları toohello çözüm demektir.

### <a name="add-your-opc-ua-servers"></a>OPC UA sunucularınızı ekleme

1. Toohello Gözat **kendi OPC UA sunucusuna** hello bağlı Fabrika çözüm portalında sayfası. Bağlı Fabrika portal hello ve OPC UA sunucu hello arasında bölüm tooestablish önceki hello olduğu gibi aynı adımları güven hello izleyin. Bu adım, karşılıklı güven hello hello sertifika Fabrika portal ve hello OPC UA sunucu bağlı ve bir bağlantı oluşturur oluşturur.

1. Merhaba OPC UA düğümleri ağaç OPC UA sunucunuzun gidin, hello OPC düğümleri sağ tıklatın ve seçin **yayımlama**. Bu şekilde yayımlama toowork için OPC UA sunucu hello ve hello yayımcı üzerinde hello olmalıdır aynı ağ. Diğer bir deyişle, hello tam olarak nitelenmiş etki alanı adı hello publisher'ın ise **publisher.mydomain.com** sonra OPC UA sunucu olması gerekir, örneğin, hello hello tam etki alanı adı **myopcuaserver.mydomain.com**. Kurulumunuzu farklıysa hello bulunan düğümleri toohello publishesnodes.json dosyasını el ile ekleyebilirsiniz **D:\\docker** klasör. Merhaba publishesnodes.json dosyası otomatik olarak hello üzerinde ilk başarılı oluşturulan bir OPC düğümünün yayımlayın.

1. Telemetri şimdi hello ağ geçidi aygıttan akar. Merhaba telemetri hello görüntüleyebilirsiniz **Fabrika konumları** hello bağlı Fabrika portal altında görünümünü **yeni Fabrika**.

## <a name="linux-deployment"></a>Linux dağıtımı

> [!NOTE]
> Bir ağ geçidi cihazı henüz yoksa, Microsoft ticari bir ağ geçidi ortaklarımızdan birinden satın önerir. Merhaba ziyaret [Azure IOT cihaz katalog] ağ geçidi cihazların Merhaba ile uyumlu bir listesini Fabrika çözüm bağlandı. Merhaba aygıt tooset hello ağ geçidi kurma gelir hello yönergeleri izleyin. Alternatif olarak, varolan geçitlerinizin birinde ayarlama yönergeleri toomanually aşağıdaki hello kullanın.

[Docker yükleme] Linux ağ geçidi cihazınız üzerinde.

### <a name="configure-hello-gateway"></a>Merhaba ağ geçidini yapılandırma

1. Merhaba gereksinim **iothubowner** Azure IOT paketi bağlantı dizesi bağlı Fabrika dağıtım toocomplete hello ağ geçidi dağıtımı. Merhaba, [Azure portal], IOT Hub'hello kaynak grubunda oluşturulan bağlı hello Fabrika çözüm dağıtıldığında tooyour gidin. Tıklatın **paylaşılan erişim ilkeleri** tooaccess hello **iothubowner** bağlantı dizesi:

    ![Hello IOT Hub bağlantı dizesine bulur][img-hub-connection]

    Kopya hello **bağlantı dizesi--birincil anahtar** değeri.

1. Merhaba iki ağ geçidi modülleri çalıştırarak Hello ağ geçidi için IOT Hub'ınızı yapılandırma **sonra** ile Kabuğu'ndan:

    `sudo docker run -it --rm -h <ApplicationName> -v /shared:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/ -v /shared:/root/.dotnet/corefx/cryptography/x509stores microsoft/iot-gateway-opc-ua:1.0.0 <ApplicationName> "<IoTHubOwnerConnectionString>"`

    `sudo docker run --rm -it -v /shared:/mapped microsoft/iot-gateway-opc-ua-proxy:0.1.3 -i -c "<IoTHubOwnerConnectionString>" -D /mapped/cs.db`

    * **&lt;ApplicationName&gt; ** OPC UA uygulama hello ağ geçidi oluşturur hello biçiminde hello hello adıdır **yayımcı.&lt; tam etki alanı adınızı&gt;**. Örneğin, **publisher.microsoft.com**.
    * **&lt;IoTHubOwnerConnectionString&gt; ** hello olan **iothubowner** hello önceki adımda kopyaladığınız bağlantı dizesi. Bu bağlantı dizesini yalnızca bu adımda kullanılır, aşağıdaki adımları hello gerekmez:

    Merhaba kullandığınız **/ paylaşılan** klasörü (Merhaba `-v` bağımsız değişkeni) sonraki toopersist hello hello ağ geçidi modülleri kullanan iki X.509 sertifikaları.

### <a name="run-hello-gateway"></a>Merhaba ağ geçidini çalıştırmak

1. Merhaba aşağıdaki komutları kullanarak hello ağ geçidini yeniden başlatın:

    `sudo docker run -it -h <ApplicationName> --expose 62222 -p 62222:62222 –-rm -v /shared:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/Logs -v /shared:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/CertificateStores -v /shared:/shared -v /shared:/root/.dotnet/corefx/cryptography/x509stores -e _GW_PNFP="/shared/publishednodes.JSON" microsoft/iot-gateway-opc-ua:1.0.0 <ApplicationName>`

    `sudo docker run -it -v /shared:/mapped microsoft/iot-gateway-opc-ua-proxy:0.1.3 -D /mapped/cs.db`

1. Güvenlik nedenleriyle hello iki X.509 sertifikalarını hello kalıcı **/ paylaşılan** klasör hello özel anahtarı içerir. Sınır erişim toothis klasörü toohello toorun kullandığınız kimlik bilgileri Docker kapsayıcısı hello. tooset hello izinlerini **kök** yalnızca hello kullanın `chmod` Kabuk hello klasörü komutu.

1. Ağ bağlantısını doğrulayın. Bir kabuğundan hello komutu girin `ping publisher.<your fully qualified domain name>` tooping, ağ geçidi. Merhaba hedef erişilemediğinde hello IP adresi ve ağ geçidiniz üzerinde ağ geçidi tooyour hosts dosyasının adını ekleyin. Merhaba hosts dosyasını hello bulunan **/vb.** klasör.

1. Ardından, tooconnect toohello yayımcı hello ağ geçidinde çalıştıran yerel bir OPC UA istemcisi kullanarak deneyin. OPC UA uç noktası URL'si hello `opc.tcp://publisher.<your fully qualified domain name>:62222`. OPC UA istemci yoksa kullanın indirin ve bir [açık kaynak OPC UA istemci].

1. Bu yerel testleri başarıyla tamamladıktan sonra toohello Gözat **kendi OPC UA sunucusuna** hello bağlı Fabrika çözüm portalında sayfası. Merhaba yayımcı uç noktasının URL'sini girin (`tcp://publisher.<your fully qualified domain name>:62222`) tıklatıp **Bağlan**. Bir sertifika uyarısı almak, ardından tıklatın **devam et.** Ardından bu hello bir hata alıyorsunuz yayımcı hello UA Web istemcisi güven değil. tooresolve bu hata, kopyalama hello **UA Web istemcisi** hello sertifikadan **/paylaşılan/reddedildi sertifikaları/sertifikaları** klasörü toohello **/shared/UA uygulamalar/sertifikaları** Merhaba ağ geçidi klasör. Toorestart hello ağ geçidinin zorunda değilsiniz. Bu adımı yineleyin. Merhaba buluttan toohello ağ geçidi artık bağlanabilir ve hazır tooadd OPC UA sunucuları toohello çözüm demektir.

### <a name="add-your-opc-ua-servers"></a>OPC UA sunucularınızı ekleme

1. Toohello Gözat **kendi OPC UA sunucusuna** hello bağlı Fabrika çözüm portalında sayfası. Bağlı Fabrika portal hello ve OPC UA sunucu hello arasında bölüm tooestablish önceki hello olduğu gibi aynı adımları güven hello izleyin. Bu adım, karşılıklı güven hello hello sertifika Fabrika portal ve hello OPC UA sunucu bağlı ve bir bağlantı oluşturur oluşturur.

1. Merhaba OPC UA düğümleri ağaç OPC UA sunucunuzun gidin, hello OPC düğümleri sağ tıklatın ve seçin **yayımlama**. Bu şekilde yayımlama toowork için OPC UA sunucu hello ve hello yayımcı üzerinde hello olmalıdır aynı ağ. Diğer bir deyişle, hello tam olarak nitelenmiş etki alanı adı hello publisher'ın ise **publisher.mydomain.com** sonra OPC UA sunucu olması gerekir, örneğin, hello hello tam etki alanı adı **myopcuaserver.mydomain.com**. Kurulumunuzu farklıysa hello bulunan düğümleri toohello publishesnodes.json dosyasını el ile ekleyebilirsiniz **/ paylaşılan** klasör. Merhaba publishesnodes.json otomatik olarak oluşturulan hello üzerinde ilk başarılı bir OPC düğümünün yayımlayın.

1. Telemetri şimdi hello ağ geçidi aygıttan akar. Merhaba telemetri hello görüntüleyebilirsiniz **Fabrika konumları** hello bağlı Fabrika portal altında görünümünü **yeni Fabrika**.

## <a name="next-steps"></a>Sonraki adımlar

Merhaba bağlı Fabrika hello mimarisi hakkında daha fazla toolearn önceden yapılandırılmış çözümü için bkz: [bağlı Fabrika önceden yapılandırılmış çözüm izlenecek][lnk-walkthrough].

[img-install-docker]: ./media/iot-suite-connected-factory-gateway-deployment/image1.png
[img-hub-connection]: ./media/iot-suite-connected-factory-gateway-deployment/image2.png
[img-docker-share]: ./media/iot-suite-connected-factory-gateway-deployment/image3.png

[Windows için docker]: https://www.docker.com/docker-windows
[Azure IOT cihaz Kataloğu]: https://catalog.azureiotsuite.com/?q=opc
[Azure portal]: http://portal.azure.com/
[açık kaynak OPC UA istemci]: https://github.com/OPCFoundation/UA-.NETStandardLibrary/tree/master/SampleApplications/Samples/Client.Net4
[Docker yükleyin]: https://www.docker.com/community-edition#/download
[lnk-walkthrough]: iot-suite-connected-factory-sample-walkthrough.md
[Azure IoT Edge]: https://github.com/Azure/iot-edge

[lnk-publisher-github]: https://github.com/Azure/iot-edge-opc-publisher
[lnk-publisher-docker]: https://hub.docker.com/r/microsoft/iot-gateway-opc-ua
[lnk-proxy-github]: https://github.com/Azure/iot-edge-opc-proxy
[lnk-proxy-docker]: https://hub.docker.com/r/microsoft/iot-gateway-opc-ua-proxy