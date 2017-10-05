---
title: "Azure IOT paketi bağlı Fabrika SSS | Microsoft Docs"
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
ms.openlocfilehash: 35cf824210a14410d7ea2aedddde0040309901f9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="frequently-asked-questions-for-iot-suite-connected-factory-preconfigured-solution"></a>IOT paketi bağlı fabrikası için sık sorulan sorular önceden yapılandırılmış çözümü

Ayrıca bkz.: Genel [SSS](iot-suite-faq.md) IOT paketi için.

### <a name="where-can-i-find-the-source-code-for-the-preconfigured-solution"></a>Önceden yapılandırılmış çözüm için kaynak kodunu nereden bulabilirim?

Kaynak kodu aşağıdaki GitHub deposunda depolanır:

* [Bağlı Fabrika önceden yapılandırılmış çözümü](https://github.com/Azure/azure-iot-connected-factory)

### <a name="what-is-opc-ua"></a>OPC UA nedir?

OPC birleşik mimarisi (2008'de serbest UA), bir platformdan bağımsız, hizmet odaklı birlikte çalışabilirlik standart ' dir. OPC UA çeşitli endüstriyel sistemleri ve cihazların endüstri PC'ler, PLC ve algılayıcılar gibi tarafından kullanılır. OPC UA OPC Klasik belirtimleri işlevselliğini bir Genişletilebilir Framework'e yerleşik güvenlik ile tümleşir. OPC Foundation tarafından yönetilen bir standarttır. [OPC Foundation](http://opcfoundation.org/) kar için not kuruluşunuzun birden fazla 440 üyelere sahip. Kuruluş amacı çok satıcı, çok platformlu, güvenli ve güvenilir birlikte çalışabilirliği aracılığıyla kolaylaştırmak için OPC belirtimleri kullanmaktır:

* Altyapı
* Belirtimleri
* Teknoloji
* İşlemler

### <a name="why-did-microsoft-choose-opc-ua-for-the-connected-factory-preconfigured-solution"></a>Neden Microsoft OPC UA bağlı Fabrika önceden yapılandırılmış çözümü seçin?

Bir açık, olmayan-özel, platform bağımsız, endüstri tanınan ve kanıtlanmış standart olduğu için Microsoft OPC UA seçtiniz. Geniş bir üretim işlemleri kümesi ile donanım arasında birlikte çalışabilirlik sağlama Industrie 4.0 (RAMI4.0) başvuru mimarisi çözümleri için gerekli değildir. Microsoft, müşterilerimizin Industrie 4.0 çözümleri oluşturmak üzere talep görür. OPC UA desteği engel müşterilerin hedeflerine ulaşması alt yardımcı olur ve onları hemen iş değerine sağlar.

### <a name="how-do-i-add-a-public-ip-address-to-the-simulation-vm"></a>VM benzetimi için nasıl bir ortak IP adresi eklensin mi?

IP adresi eklemek için iki seçeneğiniz vardır:

* PowerShell Betiği kullanmak `Simulation/Factory/Add-SimulationPublicIp.ps1` içinde [depo](https://github.com/Azure/azure-iot-connected-factory). Dağıtım adınızı parametre olarak geçirin. Yerel bir dağıtım için kullanmak `<your username>ConnFactoryLocal`. Komut dosyası VM IP adresini yazdırır.

* Azure portalında, dağıtımınızın kaynak grubunu bulun. Yerel bir dağıtımı dışında kaynak grubu çözümü olarak belirtilen adı veya dağıtım adı var. Yapı komut dosyasını kullanarak yerel bir dağıtımı için kaynak grubunun adıdır `<your username>ConnFactoryLocal`. Şimdi yeni bir ekleyin **genel IP adresi** kaynak grubuna kaynak.

> [!NOTE]
> Yönergeleri izleyerek en son düzeltme eklerini yüklediğiniz her iki durumda da olun [Ubuntu Web sitesi](https://wiki.ubuntu.com/Security/Upgrades). VM'yi bir ortak IP adresi üzerinden erişilebilir olduğu müddetçe yükleme için güncel tutun.

### <a name="how-do-i-remove-the-public-ip-address-to-the-simulation-vm"></a>Genel IP adresi VM benzetimi için nasıl kaldırılsın mı?

IP adresini kaldırmak için iki seçeneğiniz vardır:

* PowerShell komut dosyası, Simulation/Factory/Remove-SimulationPublicIp.ps1 kullanım [depo](https://github.com/Azure/azure-iot-connected-factory). Dağıtım adınızı parametre olarak geçirin. Yerel bir dağıtım için kullanmak `<your username>ConnFactoryLocal`. Komut dosyası VM IP adresini yazdırır.

* Azure portalında, dağıtımınızın kaynak grubunu bulun. Yerel bir dağıtımı dışında kaynak grubu çözümü olarak belirtilen adı veya dağıtım adı var. Yapı komut dosyasını kullanarak yerel bir dağıtımı için kaynak grubunun adıdır `<your username>ConnFactoryLocal`. Şimdi kaldırmak **genel IP adresi** kaynak kaynak grubu.

### <a name="how-do-i-sign-in-to-the-simulation-vm"></a>VM benzetimi nasıl oturum?

VM benzetimi için oturum açma yalnızca desteklenen PowerShell Betiği kullanılarak çözümünüzü dağıttıysanız, `build.ps1` içinde [depo](https://github.com/Azure/azure-iot-connected-factory).

Www.azureiotsuite.com çözümden dağıttıysanız VM oturum açamaz. ' De, çünkü parolayı rastgele oluşturulan ve onu sıfırlayamazsınız oturum.

1. Bir ortak IP adresi VM'ye ekleyin. Bkz: [VM benzetimi için bir ortak IP adresi nasıl ekleyebilirim?](#how-do-i-remove-the-public-ip-address-to-the-simulation-vm)
1. VM IP adresini kullanarak, VM için bir SSH oturumu oluşturun.
1. Kullanılacak kullanıcı adı: `docker`.
1. Kullanılacak parolayı dağıtmak için kullanılan sürümüne bağlıdır:
    * 1 Haziran 2017 önce build.ps1 komut dosyası kullanılarak dağıtılan çözümleri için bir paroladır: `Passw0rd`.
    * 1 Haziran 2017 sonra build.ps1 komut dosyası kullanılarak dağıtılan çözümleri için parolayı bulabilirsiniz `<name of your deployment>.config.user` dosya. Parola depolanan **VmAdminPassword** ayarı. Kullanarak belirtmediğiniz sürece parolayı rastgele dağıtım sırasında oluşturulan `build.ps1` parametresi komut dosyası`-VmAdminPassword`

### <a name="how-do-i-stop-and-start-all-docker-processes-in-the-simulation-vm"></a>Nasıl durdurun ve tüm docker işlemleri benzetimi VM başlatma?

1. VM benzetimi için oturum açın. Bkz: [nasıl oturum benzetimi VM?](#how-do-i-sign-in-to-the-simulation-vm)
1. Hangi kapsayıcıları etkin denetlemek için çalıştırın: `docker ps`.
1. Tüm benzetimi kapsayıcıları durdurmak için çalıştırın: `./stopsimulation`.
1. Tüm benzetimi kapsayıcıları başlatmak için:
    * Ada sahip bir kabuk değişken verme **IOTHUB_CONNECTIONSTRING**. Değerini kullanmak **IotHubOwnerConnectionString** ayarı `<name of your deployment>.config.user` dosya. Örneğin:

        ```
        export IOTHUB_CONNECTIONSTRING="HostName={yourdeployment}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={your key}"
        ```

    * `./startsimulation` öğesini çalıştırın.

### <a name="how-do-i-update-the-simulation-in-the-vm"></a>VM'deki benzetimi nasıl güncelleştiririm?

Benzetimi herhangi bir değişiklik yaptıysanız, PowerShell Betiği kullanabilirsiniz `build.ps1` içinde [deposu](https://github.com/Azure/azure-iot-connected-factory) kullanarak `updatedimulation` komutu. Bu komut tüm benzetimi bileşenleri oluşturur, VM'deki benzetimi durdurur, yükler, yükler ve bunları başlatır.

### <a name="how-do-i-find-out-the-connection-string-of-the-iot-hub-used-by-my-solution"></a>IOT hub'ı my çözümü tarafından kullanılan bağlantı dizesi kullanıma nasıl bulabilirim?

Çözümünüzle birlikte dağıttıysanız `build.ps1` içindeki komut dosyası [deposu](https://github.com/Azure/azure-iot-connected-factory), bağlantı dizesi değeri **IotHubOwnerConnectionString** içinde `<name of your deployment>.config.user` dosya.

Azure Portalı'nı kullanarak bağlantı dizesini de bulabilirsiniz. Kaynak grubu, dağıtımınızın IOT Hub'kaynağında bağlantı dizesi ayarlarının bulun.

### <a name="which-iot-hub-devices-does-the-connected-factory-simulation-use"></a>Hangi IOT Hub cihazları bağlı Fabrika benzetimi kullanıyor mu?

Benzetim self aşağıdaki cihazları kaydeder:

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

Kullanarak [DeviceExplorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) veya [iothub-explorer](https://github.com/azure/iothub-explorer) aracı, hangi aygıtların çözümünüzü kullanarak IOT hub ile kaydedilen kontrol edebilirsiniz. Bu araçları kullanmak için bağlantı dizesi için IOT hub'ı dağıtımınızda gerekir.

### <a name="how-can-i-get-log-data-from-the-simulation-components"></a>Günlük verileri benzetimi bileşenlerini nasıl alabilirim?

Tüm bileşenleri benzetimde bilgileri günlük dosyalarına oturum açın. Bu dosyalar VM'yi klasöründe bulunabilir `home/docker/Logs`. Günlükleri almak için PowerShell betiğini kullanabilirsiniz `Simulation/Factory/Get-SimulationLogs.ps1` içinde [depo](https://github.com/Azure/azure-iot-connected-factory).

Bu komut VM oturum açması gerekiyor. Oturum açma için kimlik bilgilerini sağlamanız gerekebilir. Bkz: [nasıl oturum benzetimi VM?](#how-do-i-sign-in-to-the-simulation-vm) kimlik bilgileri bulunamadı.

Komut dosyası ekler veya bir ortak IP adresi VM henüz bir sahip değil ve kaldırır kaldırır. Betik tüm günlük dosyalarını bir arşiv koyar ve Arşiv geliştirme istasyonunuza indirir.

Alternatif olarak VM SSH aracılığıyla oturum açın ve çalışma zamanında günlük dosyalarını inceleyin.

### <a name="how-can-i-check-if-the-simulation-is-sending-data-to-the-cloud"></a>Benzetim buluta veri gönderme, nasıl kontrol edebilirsiniz?

İle [DeviceExplorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) veya [iothub-explorer](https://github.com/azure/iothub-explorer) aracı, belirli aygıtlardan IOT Hub'ına gönderilen verileri incelemek. Bu araçları kullanmak için dağıtımınızdaki IOT hub'ına yönelik bağlantı dizesini bilmeniz gerekir. Bkz: [nasıl bulabilirim my çözümü tarafından kullanılan IOT hub bağlantı dizesi kullanıma?](#how-do-i-find-out-the-connection-string-of-the-iot-hub-used-by-my-solution)

Yayımcı aygıtlardan biri tarafından gönderilen verileri inceleyin:

* Publisher.Beijing.corp.contoso
* Publisher.capetown.corp.contoso
* Publisher.Mumbai.corp.contoso
* Publisher.munich0.corp.contoso
* Publisher.Rio.corp.contoso
* Publisher.Seattle.corp.contoso

IOT Hub'ına gönderilen veri görürseniz, benzetimi ile ilgili bir sorun yoktur. İlk çözümleme adım olarak günlük dosyaları benzetimi bileşenlerinin çözümlemeniz gerekir. Bkz: [benzetimi bileşenlerini günlük verilerini nasıl alabilirim?](#how-can-i-get-log-data-from-the-simulation-components) Ardından, durdurmak ve benzetimi başlatmak ve hala gönderilen veri yoksa benzetimi tamamen güncelleştirmek deneyin. Bkz: [VM'deki benzetimi nasıl güncelleştirebilirim?](#how-do-i-update-the-simulation-in-the-vm)

### <a name="next-steps"></a>Sonraki adımlar

Önceden yapılandırılmış IoT Suite çözümlerinin diğer özelliklerinden bazılarını da keşfedebilirsiniz:

* [Önceden yapılandırılmış Tahmine dayalı bakım çözümüne genel bakış](iot-suite-predictive-overview.md)
* [Önceden yapılandırılmış bağlı Fabrika çözümüne genel bakış](iot-suite-connected-factory-overview.md)
* [IOT güvenlik sıfırdan](securing-iot-ground-up.md)