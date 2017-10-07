---
title: "Azure IOT hub'ınızı – Web Apps algılayıcı verilerini aaaReal zaman veri Görselleştirme | Microsoft Docs"
description: "Hello algılayıcı ' toplanan ve tooyour IOT hub gönderilen Microsoft Azure App Service toovisualize sıcaklık ve nem veri Hello Web Apps özelliğini kullanın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "gerçek zamanlı veri görselleştirme, dinamik veri görselleştirme algılayıcı verileri Görselleştirme"
ms.assetid: e42b07a8-ddd4-476e-9bfb-903d6b033e91
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: 72f2dffee1c2f975948820eee9f2e287c3f77255
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-real-time-sensor-data-from-your-azure-iot-hub-by-using-hello-web-apps-feature-of-azure-app-service"></a>Azure App Service Web Apps özelliğini hello kullanarak Azure IOT hub'ınızı gerçek zamanlı algılayıcı verilerini görselleştirmek

![Uçtan uca diyagramı](media/iot-hub-get-started-e2e-diagram/5.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a>Öğrenecekleriniz

Bu öğreticide, bir web uygulaması çalıştıran tarafından IOT hub'ınızın aldığı toovisualize gerçek zamanlı algılayıcı verilerini bir web uygulamasını nasıl barındırılan öğrenin. Power BI kullanarak tootry toovisualize hello veri IOT hub'ınıza istiyorsanız bkz [kullanım Power BI toovisualize gerçek zamanlı algılayıcı verileri Azure IOT Hub](iot-hub-live-data-visualization-in-power-bi.md).

## <a name="what-you-do"></a>Neler

- Hello Azure portalında bir web uygulaması oluşturun.
- IOT hub'ınızı bir tüketici grubu ekleyerek veri erişimi için hazırlanın.
- IOT hub'ınızı gelen Hello web uygulama tooread algılayıcı verileri yapılandırın.
- Merhaba web uygulaması tarafından barındırılan bir web uygulaması toobe karşıya yükleyin.
- Merhaba web uygulama toosee gerçek zamanlı sıcaklık ve nem verileri IOT hub'ından açın.

## <a name="what-you-need"></a>Ne gerekiyor

- [Cihazınızı ayarlamak](iot-hub-raspberry-pi-kit-node-get-started.md), hello gereksinimleri aşağıdaki kapsar:
  - Etkin bir Azure aboneliği
  - Aboneliğinizdeki IOT hub'ı
  - Tooyour IOT hub'ı iletileri gönderen bir istemci uygulaması
- [Git indir](https://www.git-scm.com/downloads)

## <a name="create-a-web-app"></a>Web uygulaması oluşturma

1. Merhaba, [Azure portal](https://ms.portal.azure.com/), tıklatın **yeni** > **Web + mobil** > **Web uygulaması**.
2. Benzersiz iş adını girin, hello abonelik doğrulayın, bir kaynak grubu ve select bir konum belirtin **PIN toodashboard**ve ardından **oluşturma**.

   Merhaba seçmenizi öneririz, kaynak grubunuzun aynı konumda. Bunun yapılması, işlem hızı yardımcı olur ve veri aktarımı hello maliyetini azaltır.

   ![Web uygulaması oluşturma](media/iot-hub-live-data-visualization-in-web-apps/2_create-web-app-azure.png)

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="configure-hello-web-app-tooread-data-from-your-iot-hub"></a>IOT hub'ınızı gelen Hello web uygulama tooread verileri yapılandırma

1. Yalnızca sağlanan hello web uygulamasını açın.
2. Tıklatın **uygulama ayarları**ve ardından, **uygulama ayarları**, anahtar/değer çiftlerinin aşağıdaki hello ekleyin:

   | Anahtar                                   | Değer                                                        |
   |---------------------------------------|--------------------------------------------------------------|
   | Azure.IoT.IoTHub.ConnectionString     | Iothub Gezgini'nden elde                                |
   | Azure.IoT.IoTHub.ConsumerGroup        | Merhaba adını hello tüketici grubu tooyour IOT hub'ı Ekle  |

   ![Anahtar/değer çiftleri ile ayarları tooyour web uygulaması Ekle](media/iot-hub-live-data-visualization-in-web-apps/4_web-app-settings-key-value-azure.png)

3. Tıklatın **uygulama ayarları**altında **genel ayarları**, iki durumlu hello **Web yuvaları** seçeneğini ve ardından **kaydetmek**.

   ![İki durumlu hello Web yuva seçeneği](media/iot-hub-live-data-visualization-in-web-apps/10_toggle_web_sockets.png)

## <a name="upload-a-web-application-toobe-hosted-by-hello-web-app"></a>Merhaba web uygulaması tarafından barındırılan bir web uygulaması toobe karşıya yükle

Github'da, IOT hub'ınızı gerçek zamanlı algılayıcı verileri görüntüleyen bir web uygulaması kullanılabilir yaptık. Toodo gereken tek şey hello web uygulama toowork bir Git deposu ile yapılandırma Merhaba web uygulaması Github'dan indirin ve hello web uygulama toohost tooAzure karşıya yükleyin.

1. Merhaba web uygulamasında tıklatın **dağıtım seçenekleri** > **Kaynağı Seç** > **yerel Git deposu**ve ardından **Tamam**.

   ![Web uygulama dağıtım toouse hello yerel Git deponuzu yapılandırın](media/iot-hub-live-data-visualization-in-web-apps/5_configure-web-app-deployment-local-git-repository-azure.png)

2. Tıklatın **dağıtım kimlik bilgileri**, bir kullanıcı adı ve parola toouse tooconnect toohello Git deposu oluşturma ve ardından **kaydetmek**.

3. Tıklatın **genel bakış**, hello değerini not edin **Git kopyası URL'si**.

   ![Web uygulamanızın Hello Git kopya URL'si](media/iot-hub-live-data-visualization-in-web-apps/7_web-app-git-clone-url-azure.png)

4. Bir komut veya yerel bilgisayarınızda terminal penceresi açın.

5. Github'dan Hello web uygulamasını indirmeye ve hello web uygulama toohost tooAzure yükleyin. toodo, bu nedenle, hello aşağıdaki komutları çalıştırın:

   ```bash
   git clone https://github.com/Azure-Samples/web-apps-node-iot-hub-data-visualization.git
   cd web-apps-node-iot-hub-data-visualization
   git remote add webapp <Git clone URL>
   git push webapp master:master
   ```

   > [!NOTE]
   > \<Git kopyalama URL'si\> hello üzerinde bulunan hello Git deposu hello URL'sidir **genel bakış** hello web uygulaması sayfasında.

## <a name="open-hello-web-app-toosee-real-time-temperature-and-humidity-data-from-your-iot-hub"></a>IOT hub'ından Hello web uygulama toosee gerçek zamanlı sıcaklık ve nem verileri açın

Merhaba üzerinde **genel bakış** sayfa hello URL tooopen hello web uygulaması, web uygulamanızın ' ı tıklatın.

![Web uygulamanızın Hello URL'sini alma](media/iot-hub-live-data-visualization-in-web-apps/8_web-app-url-azure.png)

IOT hub'ından hello gerçek zamanlı sıcaklık ve nem veri görmeniz gerekir.

![Gerçek zamanlı sıcaklık ve nem gösteren web uygulama sayfası](media/iot-hub-live-data-visualization-in-web-apps/9_web-app-page-show-real-time-temperature-humidity-azure.png)

> [!NOTE]
> Merhaba örnek uygulaması aygıtınızda çalıştığından emin olun. Boş bir grafik alırsınız istemiyorsanız, toohello öğreticileri altında başvurabilir [Cihazınızı](iot-hub-raspberry-pi-kit-node-get-started.md).

## <a name="next-steps"></a>Sonraki adımlar
IOT hub'ından web uygulama toovisualize gerçek zamanlı algılayıcı verilerini başarıyla kullanmış olduğunuz.

Bir alternatif yol toovisualize verileri için Azure IOT Hub, görmek [IOT hub'ınızı kullanın Power BI toovisualize gerçek zamanlı algılayıcı verileri](iot-hub-live-data-visualization-in-power-bi.md).

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
