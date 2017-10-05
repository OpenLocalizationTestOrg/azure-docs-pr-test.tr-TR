---
title: "Sanal cihaz & Azure IOT ağ geçidi - Başlarken | Microsoft Docs"
description: "IOT ağ geçidi Starter Kit ile çalışmaya başlama, Azure IOT hub'ınızı oluşturun ve IOT hub'ı ağ geçidine bağlanmak"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Azure IOT hub, IOT ağ geçidi, noktalar, IOT Araç Seti Internet ile çalışmaya başlama"
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
ms.openlocfilehash: 916fa40d9ac857dfa72197b40c232834593d3891
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-simulated-device"></a>IOT ağ geçidi Starter Kit ile bir sanal cihaz ile çalışmaya başlama

> [!div class="op_single_selector"]
> * [SensorTag](iot-hub-gateway-kit-c-get-started.md)
> * [Sanal cihaz](iot-hub-gateway-kit-c-sim-get-started.md)

Bu öğreticide, ile çalışmanın temelleri öğrenerek başlamadan [IOT ağ geçidi Starter Kit](https://aka.ms/gateway-kit). Intel NUC ile Rüzgar Akarsu Linux çalıştıran çalışacaksınız. Şunları öğreneceksiniz seamleesly için Azure IOT hub'ı kullanarak bulut aygıtlarınıza nasıl bağlanacağını.

***
**Bir pakete henüz yok mu?:** tıklatın [burada](https://aka.ms/gateway-kit).
***

## <a name="lesson-1-configure-your-nuc"></a>Ders 1: NUC cihazınızı yapılandırma
![Lesson1 uçtan uca diyagramı](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson1.png)

Bu ders, Intel NUC (sonraki birim, bilgisayar) bir Azure IOT ağ geçidi olarak Seti'nde ayarlama, Azure IOT kenar paket üzerinde NUC yükleyin ve bir örnek uygulama ağ geçidi işlevlerini doğrulayın çalıştırın.

*Tahmini tamamlanma süresi: 15 dakika*

Git [Intel NUC IOT ağ geçidi olarak ayarlama](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)

## <a name="lesson-2-create-your-iot-hub"></a>Ders 2: IoT Hub'ı oluşturma
![Lesson2 uçtan uca diyagramı](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson2.png)

Bu ders, ana bilgisayara yazılım ve araçları yükleyin. Ardından, ücretsiz Azure hesabınızı oluşturmak, Azure IOT hub'ınızı sağlamak ve ilk Cihazınızı IOT hub'ı oluşturun.

Bu ders başlamadan önce Ders 1 tamamlayın.

### <a name="get-the-tools"></a>Araçları edinin
Yazılım ve araçları, ana bilgisayara yükleyin.

*Tahmini tamamlanma süresi: 20 dakika*

Git [araçları edinin](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)

### <a name="create-an-iot-hub-and-register-your-device"></a>IOT hub'ı oluşturma ve Cihazınızı kaydetme
Kaynak grubu oluşturmak, ilk Azure IOT hub'ınızı sağlamak ve Azure CLI kullanarak IOT hub'ına ilk aygıtınızı ekleyin.

*Tahmini tamamlanma süresi: 10 dakika*

Git [IOT hub'ı oluşturma ve Cihazınızı kaydetme](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)

## <a name="lesson-3-receive-messages-from-the-simulated-device-and-read-messages-from-your-iot-hub"></a>Ders 3: sanal cihaz iletileri almak ve IOT hub'ından iletileri okur
Bu ders, yapılandırma ve sanal cihaz uygulaması yürütülmesini, ağ geçidi otomatikleştirmek için komut dosyalarını kullanır. Sanal cihaz uygulamasının örnek sıcaklık verileri oluşturur ve bir IOT hub modülüne gönderir. IOT hub modülü alınan verileri paketler ve Azure IOT Edge'de sağlanan ağ geçidi çerçevesi aracılığıyla IOT hub'ınıza gönderir.

![Ders 3 uçtan uca diyagramı](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson3.png)

### <a name="configure-and-run-a-simulated-device"></a>Yapılandırma ve bir sanal cihaz çalıştırma
Örnek kodları hazırlayın. Ardından yapılandırın ve sanal cihaz örnek uygulamayı çalıştırın.

*Tahmini tamamlanma süresi: 15 dakika*

Git [yapılandırma ve çalıştırma bir sanal cihaz](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)

### <a name="read-messages-from-your-iot-hub"></a>IOT hub'ından iletilerini okuyun
Örnek kod, IOT hub'ından iletileri okumak için ana bilgisayarınız çalıştırın.

*Tahmini tamamlanma süresi: 15 dakika*

Git [IOT hub'ından iletilerini okuyun](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)

## <a name="lesson-4-save-messages-to-azure-table-storage"></a>Ders 4: İletileri Azure Tablo depolamaya kaydetme
IOT hub'ından gelen iletileri alır ve bunları Azure Table depolama alanına yazan bir Azure işlevi uygulaması oluşturursunuz.

![Ders 4 uçtan uca diyagramı](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a>Bir Azure işlevi uygulama ve Azure depolama hesabı oluştur
Bir Azure işlevi uygulama ve bir Azure Storage hesabı oluşturmak için bir Azure Resource Manager şablonunu kullanın.

*Tahmini tamamlanma süresi: 10 dakika*

Git [bir Azure işlevi uygulama ve Azure depolama hesabı oluştur](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)

### <a name="read-messages-persisted-in-azure-table-storage"></a>İletileri okuma Azure tablo Depolama'da kalıcı
Azure Table depolama alanına yazılır gibi ağ geçidi bulut iletileri izleyin.

*Tahmini tamamlanma süresi: 5 dakika*

Git [iletilerini okuma Azure Table storage ' kalıcı](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).

## <a name="troubleshooting"></a>Sorun giderme
Çözümlerinde dersleri sırasında herhangi bir sorun varsa, arayın [sorun giderme](iot-hub-gateway-kit-c-sim-troubleshooting.md) makalesi.

## <a name="explore-more"></a>Daha fazlasını keşfedin
Ziyaret [Intel IOT ağ geçidi Seti Geliştirici bölge](https://software.intel.com/en-us/iot/hardware/gateways/dev-kit) daha fazla bilgi için.