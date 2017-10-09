---
title: "IOT paketi aaaAzure bağlı Fabrika SSS | Microsoft Docs"
description: "IOT paketi bağlı fabrikası için sık sorulan sorular"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: corywink
ms.openlocfilehash: 4ae9beb0daf1b0578850cd652eaca7635b0d039d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-iot-suite-connected-factory-preconfigured-solution"></a>IOT paketi bağlı fabrikası için sık sorulan sorular önceden yapılandırılmış çözümü

Ayrıca bkz., genel hello [SSS](iot-suite-faq.md) IOT paketi için.

### <a name="where-can-i-find-hello-source-code-for-hello-preconfigured-solution"></a>Merhaba önceden yapılandırılmış çözümü hello kaynak kodu nereden bulabilirim?

Merhaba kaynak kodu, GitHub deposunu aşağıdaki hello depolanır:

* [Bağlı Fabrika önceden yapılandırılmış çözümü](https://github.com/Azure/azure-iot-connected-factory)

### <a name="what-is-opc-ua"></a>OPC UA nedir?

OPC birleşik mimarisi (2008'de serbest UA), bir platformdan bağımsız, hizmet odaklı birlikte çalışabilirlik standart ' dir. OPC UA çeşitli endüstriyel sistemleri ve cihazların endüstri PC'ler, PLC ve algılayıcılar gibi tarafından kullanılır. OPC UA hello OPC Klasik belirtimleri hello işlevselliğini bir Genişletilebilir Framework'e yerleşik güvenlik ile tümleşir. Merhaba OPC Foundation tarafından yönetilen bir standarttır. Merhaba [OPC Foundation](http://opcfoundation.org/) kar için not kuruluşunuzun birden fazla 440 üyelere sahip. Merhaba hello kuruluş toouse OPC belirtimleri toofacilitate çok satıcı, çok platformlu, güvenli ve güvenilir birlikte çalışabilirliği aracılığıyla hedefidir:

* Altyapı
* Belirtimleri
* Teknoloji
* İşlemler

### <a name="why-did-microsoft-choose-opc-ua-for-hello-connected-factory-preconfigured-solution"></a>Neden Microsoft OPC UA hello için Fabrika önceden yapılandırılmış çözüm bağlı seçmedi?

Bir açık, olmayan-özel, platform bağımsız, endüstri tanınan ve kanıtlanmış standart olduğu için Microsoft OPC UA seçtiniz. Geniş bir üretim işlemleri kümesi ile donanım arasında birlikte çalışabilirlik sağlama Industrie 4.0 (RAMI4.0) başvuru mimarisi çözümleri için gerekli değildir. Microsoft bizim müşteriler toobuild Industrie 4.0 çözümleri talep görür. OPC UA desteği müşteriler tooachieve için alt hello engel hedeflerine yardımcı olur ve hemen iş değeri toothem sağlar.

### <a name="how-do-i-add-a-public-ip-address-toohello-simulation-vm"></a>Bir ortak IP adresi toohello benzetimi VM nasıl eklenir?

İki seçenek tooadd hello IP adresine sahip:

* Merhaba PowerShell Betiği kullanmak `Simulation/Factory/Add-SimulationPublicIp.ps1` hello içinde [depo](https://github.com/Azure/azure-iot-connected-factory). Dağıtım adınızı parametre olarak geçirin. Yerel bir dağıtım için kullanmak `<your username>ConnFactoryLocal`. Merhaba betik hello VM hello IP adresini yazdırır.

* Hello Azure portal, dağıtımınızın hello kaynak grubunu bulun. Yerel bir dağıtımı dışında hello kaynak grubu çözümü olarak belirtilen hello adı veya dağıtım adı var. Merhaba yapı komut dosyası kullanarak bir yerel dağıtım için hello hello kaynak grubunun adıdır `<your username>ConnFactoryLocal`. Şimdi yeni bir ekleyin **genel IP adresi** kaynak toohello kaynak grubu.

> [!NOTE]
> Üzerinde hello hello yönergeleri izleyerek hello en son düzeltme eklerinin yüklemek her iki durumda da olun [Ubuntu Web sitesi](https://wiki.ubuntu.com/Security/Upgrades). VM'yi bir ortak IP adresi üzerinden erişilebilir olduğu müddetçe toodate için hello yüklemesini tutun.

### <a name="how-do-i-remove-hello-public-ip-address-toohello-simulation-vm"></a>Merhaba ortak IP adresi toohello benzetimi VM nasıl kaldırılsın mı?

İki seçenek tooremove hello IP adresine sahip:

* Merhaba PowerShell Betiği hello Simulation/Factory/Remove-SimulationPublicIp.ps1 [depo](https://github.com/Azure/azure-iot-connected-factory). Dağıtım adınızı parametre olarak geçirin. Yerel bir dağıtım için kullanmak `<your username>ConnFactoryLocal`. Merhaba betik hello VM hello IP adresini yazdırır.

* Hello Azure portal, dağıtımınızın hello kaynak grubunu bulun. Yerel bir dağıtımı dışında hello kaynak grubu çözümü olarak belirtilen hello adı veya dağıtım adı var. Merhaba yapı komut dosyası kullanarak bir yerel dağıtım için hello hello kaynak grubunun adıdır `<your username>ConnFactoryLocal`. Şimdi hello kaldırmak **genel IP adresi** hello kaynak grubundan kaynak.

### <a name="how-do-i-sign-in-toohello-simulation-vm"></a>Toohello benzetimi VM nasıl oturum?

Toohello benzetimi VM imzalama yalnızca desteklenen hello PowerShell Betiği kullanılarak çözümünüzü dağıttıysanız, `build.ps1` hello içinde [depo](https://github.com/Azure/azure-iot-connected-factory).

Www.azureiotsuite.com hello çözümden dağıttıysanız toohello VM oturumunuzu açamıyoruz. ' De, çünkü hello parolayı rastgele oluşturulan ve onu sıfırlayamazsınız oturum.

1. Genel bir IP adresi toohello VM ekleyin. Bkz: [bir ortak IP adresi toohello benzetimi VM nasıl ekleyebilirim?](#how-do-i-remove-the-public-ip-address-to-the-simulation-vm)
1. Bir SSH oturumu tooyour VM oluşturma hello VM hello IP adresini kullanarak.
1. Merhaba kullanıcıadı toouse olduğu: `docker`.
1. Merhaba parola toouse toodeploy kullanılan hello sürüme bağlıdır:
    * 1 Haziran 2017 önce Hello build.ps1 komut dosyası kullanılarak dağıtılan çözümleri için hello paroladır: `Passw0rd`.
    * 1 Haziran 2017 sonra Hello build.ps1 komut dosyası kullanılarak dağıtılan çözümleri için hello hello parola bulabilirsiniz `<name of your deployment>.config.user` dosya. Merhaba parola hello depolanan **VmAdminPassword** ayarı. hello kullanarak belirtmediğiniz sürece hello parola rastgele dağıtım sırasında oluşturulan `build.ps1` parametresi komut dosyası`-VmAdminPassword`

### <a name="how-do-i-stop-and-start-all-docker-processes-in-hello-simulation-vm"></a>Nasıl durdurun ve tüm docker işlemleri hello benzetimi VM başlatma?

1. Toohello benzetimi VM oturum açın. Bkz: [nasıl oturum toohello benzetimi VM?](#how-do-i-sign-in-to-the-simulation-vm)
1. hangi kapsayıcıları etkin toocheck çalıştırın: `docker ps`.
1. Tüm benzetimi kapsayıcıları toostop çalıştırın: `./stopsimulation`.
1. toostart tüm benzetimi kapsayıcıları:
    * Merhaba ada sahip bir kabuk değişken verme **IOTHUB_CONNECTIONSTRING**. Merhaba Hello değerini kullanın **IotHubOwnerConnectionString** hello ayarı `<name of your deployment>.config.user` dosya. Örneğin:

        ```
        export IOTHUB_CONNECTIONSTRING="HostName={yourdeployment}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={your key}"
        ```

    * `./startsimulation` öğesini çalıştırın.

### <a name="how-do-i-update-hello-simulation-in-hello-vm"></a>Merhaba VM hello benzetim nasıl güncelleştiririm?

Toohello benzetimi herhangi bir değişiklik yaptıysanız, hello PowerShell betiğini kullanabilirsiniz `build.ps1` hello içinde [deposu](https://github.com/Azure/azure-iot-connected-factory) hello kullanarak `updatedimulation` komutu. Bu komut tüm hello benzetimi bileşenleri oluşturur, hello VM hello benzetim durdurur, yükler, yükler ve bunları başlatır.

### <a name="how-do-i-find-out-hello-connection-string-of-hello-iot-hub-used-by-my-solution"></a>Merhaba hello IOT hub'ı my çözümü tarafından kullanılan bağlantı dizesi kullanıma nasıl bulabilirim?

Hello çözümünüzle dağıttıysanız `build.ps1` hello betiğinde [deposu](https://github.com/Azure/azure-iot-connected-factory), hello bağlantı dizesi değeridir hello **IotHubOwnerConnectionString** hello içinde `<name of your deployment>.config.user` dosya.

Merhaba bağlantı dizesi hello Azure portal kullanarak da bulabilirsiniz. Hello IOT hub'ı kaynak dağıtımınızın hello kaynak grubundaki'da, hello bağlantı dizesi ayarlarının bulun.

### <a name="which-iot-hub-devices-does-hello-connected-factory-simulation-use"></a>Hangi IOT Hub cihazları bağlı Fabrika benzetimi kullanımı hello?

Merhaba self kaydeder benzetimi hello aygıtları:

* Proxy.Beijing.corp.contoso
* Proxy.capetown.corp.contoso
* Proxy.Mumbai.corp.contoso
* Proxy.munich0.corp.contoso
* Proxy.Rio.corp.contoso
* Proxy.Seattle.corp.contoso
* Publisher.Beijing.corp.contoso
* Publisher.capetown.corp.contoso
* Publisher.Mumbai.corp.contoso
* Publisher.munich0.corp.contoso
* Publisher.Rio.corp.contoso
* Publisher.Seattle.corp.contoso

Hello kullanarak [DeviceExplorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) veya [iothub-explorer](https://github.com/azure/iothub-explorer) aracı, hangi aygıtların çözümünüzü kullanarak hello IOT hub ile kaydedilen kontrol edebilirsiniz. Bu araçları toouse hello bağlantı dizesi, dağıtımınızdaki hello IOT hub için gerekiyor.

### <a name="how-can-i-get-log-data-from-hello-simulation-components"></a>Merhaba benzetimi bileşenlerini günlük verilerini nasıl alabilirim?

Merhaba benzetimi günlük bilgilerini toolog dosyalarındaki tüm bileşenleri. Bu dosyalar hello VM hello klasöründe bulunabilir `home/docker/Logs`. tooretrieve hello günlükleri, hello PowerShell Betiği kullanabilir `Simulation/Factory/Get-SimulationLogs.ps1` hello içinde [depo](https://github.com/Azure/azure-iot-connected-factory).

Bu komut dosyasının toohello VM toosign gerekir. Merhaba oturum açma için tooprovide kimlik bilgileri gerekebilir. Bkz: [nasıl oturum toohello benzetimi VM?](#how-do-i-sign-in-to-the-simulation-vm) toofind hello kimlik bilgileri.

Merhaba komut dosyası ekler veya ortak bir IP adresi toohello VM, henüz bir sahip değil ve kaldırır kaldırır. Merhaba betik tüm günlük dosyalarını bir arşiv koyar ve hello arşiv tooyour geliştirme iş istasyonu indirir.

Alternatif olarak toohello VM SSH aracılığıyla oturum ve çalışma zamanında hello günlük dosyalarını inceleyin.

### <a name="how-can-i-check-if-hello-simulation-is-sending-data-toohello-cloud"></a>Merhaba benzetimi veri toohello bulut gönderme varsa nasıl kontrol edebilirsiniz?

Merhaba ile [DeviceExplorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) veya hello [iothub-explorer](https://github.com/azure/iothub-explorer) aracı, belirli aygıtlardan tooIoT Hub gönderilen hello verileri incelemek. Bu araçları toouse tooknow hello bağlantı dizesi, dağıtımınızdaki hello IOT hub için gerekiyor. Bkz: [nasıl bulabilirim hello hello IOT hub'ı my çözümü tarafından kullanılan bağlantı dizesi kullanıma?](#how-do-i-find-out-the-connection-string-of-the-iot-hub-used-by-my-solution)

Merhaba yayımcı aygıtlardan biri tarafından gönderilen hello verileri inceleyin:

* Publisher.Beijing.corp.contoso
* Publisher.capetown.corp.contoso
* Publisher.Mumbai.corp.contoso
* Publisher.munich0.corp.contoso
* Publisher.Rio.corp.contoso
* Publisher.Seattle.corp.contoso

TooIoT Hub gönderilen veri görürseniz, hello benzetimi ile ilgili bir sorun yoktur. İlk çözümleme adım olarak hello günlük dosyalarını hello benzetimi bileşenlerinin çözümlemeniz gerekir. Bkz: [günlük verilerini fotoğraf hello benzetimi bileşenleri nasıl alabilirim?](#how-can-i-get-log-data-from-the-simulation-components) Ardından, toostop deneyin ve hello benzetimi başlatmak ve gönderilen veri hala yoksa hello benzetimi tamamen güncelleştirin. Bkz: [hello VM hello benzetim nasıl güncelleştirebilirim?](#how-do-i-update-the-simulation-in-the-vm)

### <a name="next-steps"></a>Sonraki adımlar

Merhaba bazıları diğer özellikleri ve yetenekleri hello IOT paketi önceden yapılandırılmış çözümleri ayrıca keşfedebilirsiniz:

* [Önceden yapılandırılmış Tahmine dayalı bakım çözümüne genel bakış](iot-suite-predictive-overview.md)
* [Önceden yapılandırılmış bağlı Fabrika çözümüne genel bakış](iot-suite-connected-factory-overview.md)
* [Merhaba IOT güvenlikten plan](securing-iot-ground-up.md)
