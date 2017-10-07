---
title: "Benzetimli cihaz & Azure IOT ağ geçidi - Ders 1: NUC ayarlama | Microsoft Docs"
description: "Intel NUC toowork algılayıcı ve Azure IOT Hub toocollect Algılayıcı bilgilerine arasında bir IOT ağ geçidi olarak ayarlayın ve tooIoT Hub gönderebilirsiniz."
services: iot-hub
documentationcenter: 
author: shizn
manager: yjianfeng
tags: 
keywords: "IOT ağ geçidi, Intel nuc nuc bilgisayar, DE3815TYKE"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: f41d6b2e-9b00-40df-90eb-17d824bea883
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c2146c7cd8ca54adbd0af279364ec8484be1b45b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a>Intel NUC IOT ağ geçidi olarak ayarlayın

## <a name="what-you-will-do"></a>Ne yapacağını

- Intel NUC IOT ağ geçidi olarak ayarlayın.
- Intel NUC üzerinde Hello Azure IOT kenar paketini yükleyin.
- "Hello_world" örnek bir uygulama Intel NUC tooverify hello ağ geçidi işlevini çalıştırın.
Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz

Bu alıştırmanın ilerisinde şunları öğreneceksiniz:

- Nasıl tooconnect Intel NUC çevre birimleri ile.
- Nasıl Intel NUC kullanma tooinstall ve güncelleştirme gerekli hello paketleri akıllı Paket Yöneticisi hello.
- Nasıl toorun hello "hello_world" uygulama tooverify hello ağ geçidi işlevselliği örnek.

## <a name="what-you-need"></a>Ne gerekiyor

- Bir Intel NUC Seti DE3815TYKE hello Intel IOT ağ geçidi yazılım paketi ile (Rüzgar Akarsu Linux * 7.0.0.13) önceden yüklenmiş.
- Ethernet kablosu.
- Klavye.
- Bir HDMI veya VGA kablosu.
- Bir HDMI veya VGA bağlantı noktasına sahip bir izleme.

![Ağ geçidi Seti](media/iot-hub-gateway-kit-lessons/lesson1/kit_without_sensortag.png)

## <a name="connect-intel-nuc-with-hello-peripherals"></a>Intel NUC hello çevre ile bağlanma

Aşağıdaki Hello görüntü ile çeşitli çevre bağlı Intel NUC örneğidir:

1. Bağlı tooa klavye.
2. Toohello İzleyici VGA kablosu veya HDMI kablo tarafından bağlı.
3. Kablolu ağ tarafından Ethernet kablosu bağlı tooa.
4. Güç kablosu bağlı toohello güç kaynakları.

![Intel NUC tooperipherals bağlı](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-toohello-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a>Ana bilgisayar üzerinden güvenli Kabuk (SSH) toohello Intel NUC sistem bağlayın

Burada NUC Cihazınızı klavye ve monitör tooget başlangıç IP adresi gerekir. Merhaba IP biliyorsanız adresi toostep 3'te bu bölümü atlayabilirsiniz.

1. Intel NUC üzerinde hello güç düğmesi ve günlük hello sistemde tuşlarına basarak kapatın.

   Merhaba varsayılan kullanıcı adı ve parola olan her ikisi de `root`.

2. Merhaba çalıştırarak NUC Hello IP adresini alın `ifconfig` komutu. Bu adım hello NUC aygıtta yapılır.

   Merhaba komutu çıktısı bir örneği burada verilmiştir.

   ![NUC IP gösteren ifconfig çıktı](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   Bu örnekte, aşağıdaki değer hello `inet addr:` tooconnect uzaktan bir ana bilgisayar tooIntel NUC gelen planlarken, gereksinim duyduğunuz hello IP adresidir.

3. SSH istemcilerini, ana makine tooconnect tooIntel NUC aşağıdaki hello birini kullanın.

   - [PuTTY](http://www.putty.org/) Windows için.
   - Merhaba yapı içinde SSH istemcisi Ubuntu veya macOS.

   Bir ana bilgisayardan Intel NUC üzerinde daha etkili ve verimli toooperate olur. Merhaba hello IP adresi, kullanıcı adı ve parola gerekir SSH istemcisi tooconnect hello NUC. MacOS üzerinde hello örnek kullanım SSH istemcisi İşte.
   ![MacOS üzerinde çalışan SSH istemcisi](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)

## <a name="install-hello-azure-iot-edge-package"></a>Hello Azure IOT kenar paketini yükle

Hello Azure IOT kenar paket hello önceden derlenmiş ikili dosyaları hello SDK ve onun bağımlılıklarını içerir. Bu ikili dosyaları, Azure IOT kenar, hello Azure IOT SDK'sı ve hello karşılık gelen araçlar vardır. Merhaba paket kullanılan toovalidate hello ağ geçidi işlevi "hello_world" örnek bir uygulama da içerir. IOT kenar hello çekirdek hello ağ geçidi parçasıdır. tooinstall hello paketini, şu adımları izleyin:

1. Bir terminal penceresi komutlarda aşağıdaki hello çalıştırarak Hello IOT bulut deposunu ekleyin:

   ```bash
   rpm --import http://iotdk.intel.com/misc/iot_pub.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   ```

   Merhaba `rpm` içeri aktarmalar hello rpm anahtar komutu. Merhaba `smart channel` komut ekler hello rpm kanal toohello akıllı Paket Yöneticisi. Merhaba çalıştırmadan önce `smart update` komutu, gördüğünüz gibi bir çıktı aşağıda.

   ![RPM ve akıllı kanal komutları çıkış](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

   ```bash
   smart update
   ```

2. Merhaba aşağıdaki komutu çalıştırarak Hello paketini yükle:

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   `packagegroup-cloud-azure`Merhaba paket Hello adıdır. Merhaba `smart install` kullanılan tooinstall hello paket komuttur.

   Merhaba paket yüklendikten sonra Intel NUC beklenen toowork bir ağ geçidi olarak var.

## <a name="run-hello-azure-iot-edge-helloworld-sample-application"></a>Hello Azure IOT kenar "hello_world" örnek uygulamayı çalıştırın

Çok Git`azureiotgatewaysdk/samples` ve hello örnek "hello_world" örnek uygulamayı çalıştırın. Bu örnek uygulama ağ geçidi hello oluşturur `hello_world.json` dosya ve 5 saniyede hello temel bileşenlerini hello Azure IOT kenar mimarisi toolog hello world ileti tooa dosyası kullanır.

Merhaba aşağıdaki komutu çalıştırarak hello örnek "hello_world" örnek uygulama çalıştırabilirsiniz:

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

Merhaba örnek uygulaması hello aşağıdaki hello ağ geçidi işlevini düzgün çalışıp çalışmadığını çıktı üretir:

![Uygulama çıktısı](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)

Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="summary"></a>Özet

Tebrikler! Intel NUC ayarlama bir ağ geçidi olarak tamamladınız. Hazır artık toomove toohello sonraki Ders tooset, ana bilgisayar üzerinde Azure IOT hub oluşturma ve Azure IOT hub'ı mantıksal Cihazınızı kaydedin.

## <a name="next-steps"></a>Sonraki adımlar
[Ana bilgisayar ve Azure IOT hub'ı hazırlanın](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
