---
title: "aaaSimulated Raspberry Pi'yi toocloud (Node.js) - bağlanmak Raspberry Pi'yi web simulator tooAzure IOT hub'ı | Microsoft Docs"
description: "Raspberry Pi'yi toosend veri toohello Azure bulut için Raspberry Pi'yi web simulator tooAzure IOT hub'ı bağlayın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Böğürtlenli pi simulator, azure IOT Böğürtlenli pi Böğürtlenli PI IOT hub, Böğürtlenli pi veri toocloud, Böğürtlenli PI toocloud Gönder"
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/28/2017
ms.author: xshi
ms.openlocfilehash: 83736caf6ce723a49001058495a780f7f51946a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-online-simulator-tooazure-iot-hub-nodejs"></a>Raspberry Pi'yi çevrimiçi simulator tooAzure IOT hub'ı (Node.js) bağlanma

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

Bu öğreticide, Raspberry Pi'yi çevrimiçi simulator ile çalışmanın hello temelleri öğrenerek başlayın. Daha sonra nasıl tooseamlessly bağlanacağını hello Pi simulator toohello bulut kullanarak öğrenin [Azure IOT Hub](iot-hub-what-is-iot-hub.md). 

Fiziksel cihazlarınız varsa, ziyaret [bağlanmak Raspberry Pi'yi tooAzure IOT hub'ı](iot-hub-raspberry-pi-kit-node-get-started.md) tooget başlatıldı. 

<p>
<div id="diag" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#getstarted" target="_blank">
<img src="media/iot-hub-raspberry-pi-web-simulator/3_banner.png" alt="Connect Raspberry Pi web simulator tooAzure IoT Hub" width="400">
</div>
<p>
<div id="button" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#Getstarted" target="_blank">
<img src="media/iot-hub-raspberry-pi-web-simulator/6_button_default.png" alt="Start Raspberry Pi simulator" width="400" onmouseover="this.src='media/iot-hub-raspberry-pi-web-simulator/5_button_click.png';" onmouseout="this.src='media/iot-hub-raspberry-pi-web-simulator/6_button_default.png';">
</div>

## <a name="what-you-do"></a>Neler

* Raspberry Pi'yi çevrimiçi simulator Hello temellerini öğrenin.
* IOT hub'ı oluşturun.
* Bir cihaz IOT hub'ınıza Pi için kaydetme.
* Örnek bir uygulama Pi benzetimli toosend algılayıcı verileri tooyour IOT hub'ına çalıştırın.

Oluşturduğunuz sanal Raspberry Pi'yi tooan IOT hub bağlayın. Sonra hello simulator toogenerate algılayıcı verileri ile bir örnek uygulamayı çalıştırın. Son olarak, hello algılayıcı verileri tooyour IOT hub'ı gönderin.

## <a name="what-you-learn"></a>Öğrenecekleriniz

* Nasıl toocreate Azure IOT hub'ı ve yeni cihaz bağlantı dizenizi alın. Bir Azure hesabınız yoksa [ücretsiz Azure deneme hesabı oluşturma](https://azure.microsoft.com/free/) yalnızca birkaç dakika içinde.
* Nasıl toowork Raspberry Pi'yi çevrimiçi simulator ile.
* Nasıl toosend algılayıcı verileri tooyour IOT hub'ı.

## <a name="overview-of-raspberry-pi-web-simulator"></a>Raspberry Pi'yi web simulator genel bakış

Merhaba düğmesi toolaunch Raspberry Pi'yi çevrimiçi simülatörü'ı tıklatın.

> [!div class="button"]
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#GetStarted" target="_blank">Böğürtlenli Pi Simulator Başlat</a>

Merhaba web benzeticisinde üç alan vardır.
1. Derleme - hello varsayılan hattı bir Pi BME280 algılayıcı ve bir LED bağlayan alanıdır. Merhaba alanı Önizleme sürümünde kilitli özelleştirme bu nedenle şu anda yapamazsınız.
2. Alanı - toocode ile Raspberry Pi'yi için bir çevrimiçi kod düzenleyicisini kodlama. Merhaba varsayılan örnek uygulaması toocollect algılayıcı verilerini BME280 algılayıcı yardımcı olur ve tooyour Azure IOT Hub gönderir. Merhaba uygulaması ile gerçek Pi cihazları tamamen uyumludur. 
3. Tümleşik konsol penceresi - kodunuzu hello çıktısını gösterir. Bu pencere Hello üstünde üç düğme bulunur.
   * **Çalıştırma** -alan kodlama hello hello uygulamayı çalıştırın.
   * **Sıfırlama** -sıfırlama hello alanı toohello varsayılan örnek uygulaması kodlama.
   * **Katlama/genişletme** - hello sağ tarafı var olan bir düğme, toofold ve genişletin konsol penceresinde hello için açık.

> [!NOTE] 
Merhaba Raspberry Pi'yi web simulator Önizleme sürümünde kullanıma sunulmuştur. Toohear isteriz sesinizi hello içinde [Gitter Chatroom](https://gitter.im/Microsoft/raspberry-pi-web-simulator). Merhaba kaynak kodu üzerinde ortak [Github](https://github.com/Azure-Samples/raspberry-pi-web-simulator).

![Pi çevrimiçi simulator genel bakış](media/iot-hub-raspberry-pi-web-simulator/0_overview.png)

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]


## <a name="run-a-sample-application-on-pi-web-simulator"></a>Örnek bir uygulama Pi web simulator'da çalıştırma

1. Alan kodlama Merhaba varsayılan örnek uygulaması üzerinde çalıştığından emin olun. Satır 15 Hello yer tutucu hello Azure IOT hub cihaz bağlantı dizesi ile değiştirin.
   ![Merhaba cihaz bağlantı dizesini değiştirin](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)

2. Tıklatın **çalıştırmak** veya türü `npm start` toorun Merhaba uygulaması.


Aşağıdaki hello çıktı hello algılayıcı verilerini ve tooyour IOT hub gönderilen Merhaba iletileri gösterir görmelisiniz ![çıktısı - Raspberry Pi'yi tooyour IOT hub'ından gönderilen algılayıcı verileri](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)


## <a name="next-steps"></a>Sonraki adımlar

Bir örnek uygulama toocollect algılayıcı verilerini çalıştırdıktan ve tooyour IOT hub'ı gönderebilirsiniz.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
