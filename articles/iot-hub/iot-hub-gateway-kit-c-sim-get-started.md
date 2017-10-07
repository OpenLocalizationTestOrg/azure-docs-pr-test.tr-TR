---
title: "Sanal cihaz & Azure IOT ağ geçidi - Başlarken | Microsoft Docs"
description: "IOT ağ geçidi Starter Kit ile çalışmaya başlama, Azure IOT hub'ınızı oluşturun ve ağ geçidi toohello IOT hub'ı Bağlan"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Azure IOT hub, IOT ağ geçidi, Başlarken hello nesnelerin interneti, IOT Araç Seti"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 0c110b8b-bee4-4aec-a18a-dfc292aa17a3
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 1a54a5e5f1c1d9b2e657c9e4448274256e2533f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-simulated-device"></a>IOT ağ geçidi Starter Kit ile bir sanal cihaz ile çalışmaya başlama

> [!div class="op_single_selector"]
> * [SensorTag](iot-hub-gateway-kit-c-get-started.md)
> * [Sanal cihaz](iot-hub-gateway-kit-c-sim-get-started.md)

Bu öğreticide, ile çalışmanın temelleri hello öğrenerek başlamadan [IOT ağ geçidi Starter Kit](https://aka.ms/gateway-kit). Intel NUC ile Rüzgar Akarsu Linux çalıştıran çalışacaksınız. Nasıl tooseamleesly bağlanacağını aygıtları toohello bulut Azure IOT hub'ı kullanarak öğreneceksiniz.

***
**Bir pakete henüz yok mu?:** tıklatın [burada](https://aka.ms/gateway-kit).
***

## <a name="lesson-1-configure-your-nuc"></a>Ders 1: NUC cihazınızı yapılandırma
![Lesson1 uçtan uca diyagramı](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson1.png)

Bu ders içinde Intel NUC (sonraki birim, bilgisayar) hello Seti Azure IOT ağ geçidi olarak ayarlamak, NUC üzerinde hello Azure IOT kenar paketi yükleyin ve bir örnek uygulama tooverify hello ağ geçidi işlevi çalıştırın.

*Zaman toocomplete tahmini: 15 dakika*

Çok Git[Intel NUC IOT ağ geçidi olarak ayarlama](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)

## <a name="lesson-2-create-your-iot-hub"></a>Ders 2: IoT Hub'ı oluşturma
![Lesson2 uçtan uca diyagramı](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson2.png)

Bu alıştırmanın ilerisinde ana bilgisayarınızda hello araçları ve yazılımını yükleyin. Ardından, ücretsiz Azure hesabı oluşturun, Azure IOT hub'ınızı sağlamanıza ve ilk aygıtınızı hello IOT hub'ı oluşturmak.

Bu ders başlamadan önce Ders 1 tamamlayın.

### <a name="get-hello-tools"></a>Merhaba araçları edinin
Merhaba araçları ve yazılım, ana bilgisayara yükleyin.

*Zaman toocomplete tahmini: 20 dakika*

Çok Git[alma hello araçları](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)

### <a name="create-an-iot-hub-and-register-your-device"></a>IOT hub'ı oluşturma ve Cihazınızı kaydetme
Kaynak grubu oluşturmak, ilk Azure IOT hub'ınızı sağlamak ve hello Azure CLI kullanarak ilk aygıt toohello IOT hub'ınızı ekleyin.

*Zaman toocomplete tahmini: 10 dakika*

Çok Git[IOT hub'ı oluşturma ve Cihazınızı kaydetme](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)

## <a name="lesson-3-receive-messages-from-hello-simulated-device-and-read-messages-from-your-iot-hub"></a>Ders 3: hello benzetimli aygıttan iletileri almasına ve IOT hub'ından iletileri okur
Bu alıştırmanın ilerisinde, ağ geçidi betikleri tooautomate hello yapılandırması ve sanal cihaz uygulaması yürütülmesi kullanır. Merhaba sanal cihaz uygulamasının örnek sıcaklık verileri oluşturur ve tooan IOT hub modül gönderir. IOT hub modülü paketleri Hello veri tooyour IOT hub'ı sağlanan hello ağ geçidi çerçevesi aracılığıyla Azure IOT Edge'de gönderir ve alınan hello.

![Ders 3 uçtan uca diyagramı](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson3.png)

### <a name="configure-and-run-a-simulated-device"></a>Yapılandırma ve bir sanal cihaz çalıştırma
Merhaba örnek kodları hazırlayın. Ardından yapılandırıp benzetimli hello aygıt örnek uygulamayı çalıştırın.

*Zaman toocomplete tahmini: 15 dakika*

Çok Git[yapılandırma ve çalıştırma bir sanal cihaz](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)

### <a name="read-messages-from-your-iot-hub"></a>IOT hub'ından iletilerini okuyun
Örnek kod, IOT hub'ından ana bilgisayar tooread hello iletilerde çalıştırın.

*Zaman toocomplete tahmini: 15 dakika*

Çok Git[IOT hub'ından iletilerini okuyun](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)

## <a name="lesson-4-save-messages-tooazure-table-storage"></a>Ders 4: iletileri tooAzure tablo depolama kaydedin.
IOT hub'ından gelen iletileri alır ve bunları tooAzure Table storage yazan bir Azure işlevi uygulaması oluşturursunuz.

![Ders 4 uçtan uca diyagramı](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a>Bir Azure işlevi uygulama ve Azure depolama hesabı oluştur
Bir Azure Resource Manager şablonu toocreate bir Azure işlevi uygulama ve bir Azure Storage hesabı kullanın.

*Zaman toocomplete tahmini: 10 dakika*

Çok Git[bir Azure işlevi uygulama ve Azure depolama hesabı oluştur](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)

### <a name="read-messages-persisted-in-azure-table-storage"></a>İletileri okuma Azure tablo Depolama'da kalıcı
TooAzure Table storage yazıldığı şekilde hello ağ geçidi bulut iletileri izleyin.

*Zaman toocomplete tahmini: 5 dakika*

Çok Git[iletilerini okuma Azure Table storage ' kalıcı](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).

## <a name="troubleshooting"></a>Sorun giderme
Merhaba çözümlerinde hello dersleri sırasında herhangi bir sorun varsa, arayın [sorun giderme](iot-hub-gateway-kit-c-sim-troubleshooting.md) makalesi.

## <a name="explore-more"></a>Daha fazlasını keşfedin
Merhaba ziyaret [Intel IOT ağ geçidi Seti Geliştirici bölge](https://software.intel.com/en-us/iot/hardware/gateways/dev-kit) toolearn daha fazla.
