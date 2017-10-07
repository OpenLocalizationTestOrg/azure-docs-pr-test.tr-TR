---
title: "SensorTag cihaz & Azure IOT ağ geçidi - Ders 1: Intel NUC ayarlama | Microsoft Docs"
description: "Intel NUC toowork algılayıcı ve Azure IOT Hub toocollect Algılayıcı bilgilerine arasında bir IOT ağ geçidi olarak ayarlayın ve tooIoT Hub gönderebilirsiniz."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "IOT ağ geçidi, Intel nuc nuc bilgisayar, DE3815TYKE"
ms.assetid: 917090d6-35c2-495b-a620-ca6f9c02b317
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 7c3ab3b014713c7facb86b8e8622d70e60a960e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a>Intel NUC IOT ağ geçidi olarak ayarlayın
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

## <a name="what-you-will-do"></a>Ne yapacağını

- Intel NUC IOT ağ geçidi olarak ayarlayın.
- Intel NUC hello üzerinde Hello Azure IOT kenar paketini yükleyin.
- "Hello_world" örnek bir uygulama Intel NUC tooverify hello ağ geçidi işlevini hello üzerinde çalıştırın.

  > Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz

Bu alıştırmanın ilerisinde şunları öğreneceksiniz:

- Nasıl tooconnect Intel NUC çevre birimleri ile.
- Nasıl Intel NUC kullanma tooinstall ve güncelleştirme gerekli hello paketleri akıllı Paket Yöneticisi hello.
- Nasıl toorun hello "hello_world" uygulama tooverify hello ağ geçidi işlevselliği örnek.

## <a name="what-you-need"></a>Ne gerekiyor

- Bir Intel NUC Seti DE3815TYKE hello Intel IOT ağ geçidi yazılım paketi ile (Rüzgar Akarsu Linux * 7.0.0.13) önceden yüklenmiş. [Toopurchase Grove IOT ticari ağ geçidi Seti burayı](https://www.seeedstudio.com/Grove-IoT-Commercial-Gateway-Kit-p-2724.html).
- Ethernet kablosu.
- Klavye.
- Bir HDMI veya VGA kablosu.
- Bir HDMI veya VGA bağlantı noktasına sahip bir izleme.
- İsteğe bağlı: [Texas Instruments algılayıcı etiketi (CC2650STK)](http://www.ti.com/tool/cc2650stk)

![Ağ geçidi Seti](media/iot-hub-gateway-kit-lessons/lesson1/kit.png)

## <a name="connect-intel-nuc-with-hello-peripherals"></a>Intel NUC hello çevre ile bağlanma

Aşağıdaki Hello görüntü ile çeşitli çevre bağlı Intel NUC örneğidir:

1. Bağlı tooa klavye.
2. Tooa İzleyici VGA kablo veya HDMI kablo ile bağlı.
3. Kablolu Ethernet kablosu ile ağına bağlı tooa.
4. Güç kablosu bağlı tooa güç kaynakları.

![Intel NUC tooperipherals bağlı](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-toohello-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a>Ana bilgisayar üzerinden güvenli Kabuk (SSH) toohello Intel NUC sistem bağlayın

Klavye ve Intel NUC aygıtınızın bir izleyici tooget hello IP adresi gerekir. Merhaba IP zaten biliyorsanız, adresi önceden toostep bu bölümdeki 3 atlayabilirsiniz.

1. Intel NUC Hello üzerinde hello güç düğmesine basarak kapatma ve oturum açın.

   Merhaba varsayılan kullanıcı adı ve parola olan her ikisi de `root`.

       > Hit hello enter key on your keyboard if you see either of hello following errors when you boot: 'A TPM error (7) occurred attempting tooread a pcr value.' or 'Timeout, No TPM chip found, activating TPM-bypass!'

2. Merhaba çalıştırarak hello Intel NUC Hello IP adresini alın `ifconfig` hello Intel NUC aygıtta komutu.

   Merhaba komutu çıktısı bir örneği burada verilmiştir.

   ![Intel NUC IP gösteren ifconfig çıktı](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   Bu örnekte, aşağıdaki değer hello `inet addr:` toohello Intel NUC bir ana bilgisayardan bağlandığınızda gereken hello IP adresidir.

3. SSH istemcilerini, ana bilgisayar tooconnect tooIntel NUC aşağıdaki hello birini kullanın.

    - [PuTTY](http://www.putty.org/) Windows için.
    - Merhaba yerleşik SSH istemcisi Ubuntu veya macOS.

   Daha etkili ve verimli toooperate bir ana bilgisayardan bir Intel NUC olur. Intel NUC'ın IP adresi, hello kullanıcı adı ve parola tooconnect tooit bir SSH istemcisi. MacOS üzerinde SSH istemcisi kullanan örnek aşağıda verilmiştir.
   ![MacOS üzerinde çalışan SSH istemcisi](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)

## <a name="install-hello-azure-iot-edge-package"></a>Hello Azure IOT kenar paketini yükle

Hello Azure IOT kenar paket hello önceden derlenmiş ikili dosyaları IOT kenarı ve onun bağımlılıklarını içerir. Bu ikili dosyaları, Azure IOT kenar, hello Azure IOT SDK'sı ve hello karşılık gelen araçlar vardır. Merhaba ayrıca "hello_world" pakette örnek uygulamasıdır kullanılan toovalidate hello ağ geçidi işlevi. IOT kenar hello çekirdek hello ağ geçidi parçasıdır. 

Bu adımları tooinstall hello paket izleyin.

1. Merhaba IOT bulut deposu bir terminal penceresi komutlarda aşağıdaki hello çalıştırarak ekleyin:

   ```bash
   rpm --import https://iotdk.intel.com/misc/iot_pub2.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
   ```

   > Bu too'Include istediğinde 'y', bu kanal girin?'
   
   Alırsanız, bir `import read failed(-1)` hatası, komutları tooresolve hello sorunu aşağıdaki kullanım hello:
   ```bash
   wget http://iotdk.intel.com/misc/iot_pub2.key 
   rpm --import iot_pub2.key  
   ```

   Merhaba `rpm` içeri aktarmalar hello rpm anahtar komutu. Merhaba `smart channel` komut ekler hello rpm kanal toohello akıllı Paket Yöneticisi. Merhaba çalıştırmadan önce `smart update` görürsünüz, komut çıktısı ister aşağıda.

   ![RPM ve akıllı kanal komutları çıkış](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

2. Merhaba akıllı güncelleştirme komutu yürütün:

   ```bash
   smart update
   ```

3. Merhaba aşağıdaki komutu çalıştırarak Hello Azure IOT ağ geçidi paketini yükle:

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   `packagegroup-cloud-azure`Merhaba paket Hello adıdır. Merhaba `smart install` kullanılan tooinstall hello paket komuttur.

    > Çalışma hello şu komutu bu hatayı görüyorsanız: 'ortak anahtar yok'

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```
    > Bu hatayı görürseniz hello Intel NUC yeniden: 'hiçbir paket kul linux geliştirme sağlar'

   Merhaba paket yüklendikten sonra Intel NUC hazır toofunction bir ağ geçidi olarak var.

## <a name="run-hello-azure-iot-edge-helloworld-sample-application"></a>Hello Azure IOT kenar "hello_world" örnek uygulamayı çalıştırın

örnek uygulama aşağıdaki hello oluşturur bir ağ geçidi'nden bir `hello_world.json` dosya ve Azure IOT kenar mimarisi toolog hello world ileti tooa dosyası (log.txt) temel bileşenlerinin hello 5 saniyede kullanır.

Merhaba aşağıdaki komutları yürüterek hello Hello World örnek çalıştırabilirsiniz:

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

Birkaç dakika çalıştırın ve hello Enter anahtar toostop isabet Merhaba Merhaba Dünya uygulaması izin onu.
![Uygulama çıktısı](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)

> Enter tuşuna basın sonra görüntülenen 'geçersiz bağımsız değişken handle(NULL)' hataları yoksayabilirsiniz.

Şimdi hello_world klasörünüzde hello log.txt dosyasını açarak bu hello ağ geçidi başarıyla çalıştırdı doğrulayabilirsiniz ![log.txt dizin görünümü](media/iot-hub-gateway-kit-lessons/lesson1/logtxtdir.png)

Komutu aşağıdaki hello kullanarak log.txt açın:

```bash
vim log.txt
```

Ardından 5 saniyede hello ağ geçidi Hello World modülü tarafından yazılmış günlük iletilerini Merhaba biçimlendirilmiş JSON çıktısını olacaktır log.txt Merhaba içeriğine görürsünüz.
![log.txt dizin görünümü](media/iot-hub-gateway-kit-lessons/lesson1/logtxtview.png)

Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="summary"></a>Özet

Tebrikler! Intel NUC ayarlama bir ağ geçidi olarak tamamladınız. Hazır artık toomove toohello sonraki Ders tooset, ana bilgisayar üzerinde Azure IOT Hub oluşturma ve Azure IOT hub'ı mantıksal Cihazınızı kaydedin.

## <a name="next-steps"></a>Sonraki adımlar
[IOT ağ geçidi tooconnect aygıt tooAzure IOT hub'ı kullanın](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

