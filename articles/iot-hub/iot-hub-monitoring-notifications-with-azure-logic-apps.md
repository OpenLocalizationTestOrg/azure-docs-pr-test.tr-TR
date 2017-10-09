---
title: aaaIoT Uzaktan izleme ve Azure Logic Apps ile bildirimleri | Microsoft Docs
description: "IOT sıcaklık IOT hub'ınızı ve otomatik olarak izleme algılanan anormallikleri için e-posta bildirimleri tooyour posta göndermek için Azure mantıksal uygulamaları kullanın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "IOT, IOT bildirimleri izleme IOT Sıcaklık İzleme"
ms.assetid: 43043067-2e1f-42c9-953d-e2dce8fd86df
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: xshi
ms.openlocfilehash: 89396528ed63c37258e1b49f342f0723e686ecb3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="iot-remote-monitoring-and-notifications-with-azure-logic-apps-connecting-your-iot-hub-and-mailbox"></a>IOT Uzaktan izleme ve IOT hub ve posta kutusu bağlanma Azure Logic Apps ile bildirimleri

![Uçtan uca diyagramı](media/iot-hub-get-started-e2e-diagram/7.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

Azure mantıksal uygulamaları bir yöntem sunar tooautomate işlemleri bir dizi adımı olarak. Bir mantıksal uygulama çeşitli hizmetler ve protokoller bağlanabilirsiniz. Bir tetikleyici ile gibi 'Bir hesap eklendiğinde', başladıktan ve 'bir anında iletme bildirimi gönderme' gibi işlemleri birleştirilmesiyle gelmelidir. Bu özellik Logic Apps mükemmel bir IOT çözüm IOT için izleme, diğer kullanım senaryoları arasında anormallikleri için uyarı kaldığını gibi kolaylaştırır.

## <a name="what-you-learn"></a>Öğrenecekleriniz

Hakkında bilgi edineceksiniz nasıl toocreate IOT hub'ınızı ve Sıcaklık İzleme ve bildirimler için posta bağlayan bir mantıksal uygulama. Merhaba sıcaklığı 30 C olduğunda, istemci uygulaması işaretleri hello `temperatureAlert = "true"` hello iletisinde tooyour IOT hub'ı gönderir. Tetikleyiciler hello mantığı uygulama toosend selamlama iletisine, bir e-posta bildirimi.

## <a name="what-you-do"></a>Neler

* Hizmet veri yolu ad alanı oluşturun ve bir sıraya tooit ekleyin.
* Bir uç nokta ve bir yönlendirme kuralı tooyour IOT hub'ı ekleyin.
* Oluşturma, yapılandırma ve bir mantıksal uygulama test.

## <a name="what-you-need"></a>Ne gerekiyor

* Öğretici [Cihazınızı](iot-hub-raspberry-pi-kit-node-get-started.md) hangi hello gereksinimleri aşağıdaki kapsayan tamamlandı:
  * Etkin bir Azure aboneliği.
  * Azure IOT hub'ı aboneliğinizdeki.
  * Tooyour Azure IOT hub'ı iletileri gönderir bir istemci uygulaması.

## <a name="create-service-bus-namespace-and-add-a-queue-tooit"></a>Hizmet veri yolu ad alanı oluşturun ve bir sıraya tooit ekleyin

### <a name="create-a-service-bus-namespace"></a>Hizmet veri yolu ad alanı oluşturma

1. Merhaba üzerinde [Azure portal](https://portal.azure.com/), tıklatın **yeni** > **Kurumsal tümleştirme** > **Service Bus**.
1. Aşağıdaki bilgilerle hello sağlar:

   **Ad**: hello hizmet veri yolu hello adı.

   **Fiyatlandırma katmanı**: tıklatın **temel** > **seçin**. Merhaba temel katmanı, Bu öğretici için yeterlidir.

   **Kaynak grubu**: kullanım hello aynı IOT hub'ınızı kullanan kaynak grubu.

   **Konum**: kullanım hello aynı IOT hub'ınızı kullandığı konum.
1. **Oluştur**'a tıklayın.

   ![Hello Azure portalına hizmet veri yolu ad alanı oluşturma](media/iot-hub-monitoring-notifications-with-azure-logic-apps/1_create-service-bus-namespace-azure-portal.png)

### <a name="add-a-service-bus-queue"></a>Hizmet veri yolu kuyruğu ekleme

1. Merhaba hizmet veri yolu ad alanı açın ve ardından **+ sıraya**.
1. Merhaba sıra için bir ad girin ve ardından **oluşturma**.
1. Merhaba hizmet veri yolu kuyruğu açın ve ardından **paylaşılan erişim ilkeleri** > **+ Ekle**.
1. Hello İlkesi denetimi için bir ad girin **Yönet**ve ardından **oluşturma**.

   ![Hizmet veri yolu kuyruğu hello Azure portal Ekle](media/iot-hub-monitoring-notifications-with-azure-logic-apps/2_add-service-bus-queue-azure-portal.png)

## <a name="add-an-endpoint-and-a-routing-rule-tooyour-iot-hub"></a>Bir uç nokta ve bir yönlendirme kuralı tooyour IOT hub'ı ekleme

### <a name="add-an-endpoint"></a>Bir uç nokta ekleme

1. IOT hub'ınızı açın, uç noktaları > + Ekle.
1. Aşağıdaki bilgilerle hello girin:

   **Ad**: hello uç noktanın hello adı.

   **Uç nokta türü**: seçin **hizmet veri yolu kuyruğu**.

   **Hizmet veri yolu ad alanı**: oluşturduğunuz hello ad alanı seçin.

   **Service Bus kuyruğuna**: oluşturduğunuz Select hello sırası.
1. **Tamam** düğmesine tıklayın.

   ![Bir uç nokta tooyour IOT hub'hello Azure portal Ekle](media/iot-hub-monitoring-notifications-with-azure-logic-apps/3_add-iot-hub-endpoint-azure-portal.png)

### <a name="add-a-routing-rule"></a>Yönlendirme kuralı Ekle

1. IOT hub'ı tıklatın **yollar** > **+ Ekle**.
1. Aşağıdaki bilgilerle hello girin:

   **Ad**: hello yönlendirme kuralı hello adı.

   **Veri kaynağı**: seçin **DeviceMessages**.

   **Uç nokta**: oluşturduğunuz hello uç nokta seçin.

   **Sorgu dizesi**: girin `temperatureAlert = "true"`.
1. **Kaydet** düğmesine tıklayın.

   ![Hello Azure portalında bir yönlendirme kuralı Ekle](media/iot-hub-monitoring-notifications-with-azure-logic-apps/4_add-routing-rule-azure-portal.png)

## <a name="create-and-configure-a-logic-app"></a>Oluşturma ve bir mantıksal uygulama yapılandırma

### <a name="create-a-logic-app"></a>Mantıksal uygulama oluşturma

1. Merhaba, [Azure portal](https://portal.azure.com/), tıklatın **yeni** > **Kurumsal tümleştirme** > **mantıksal uygulama**.
1. Aşağıdaki bilgilerle hello girin:

   **Ad**: hello mantıksal uygulama hello adı.

   **Kaynak grubu**: kullanım hello aynı IOT hub'ınızı kullanan kaynak grubu.

   **Konum**: kullanım hello aynı IOT hub'ınızı kullandığı konum.
1. **Oluştur**'a tıklayın.

### <a name="configure-hello-logic-app"></a>Merhaba mantıksal uygulama yapılandırma

1. Logic Apps Tasarımcısı hello açar hello mantığı uygulamasını açın.
1. Hello Logic Apps Tasarımcı'da, tıklatın **boş mantıksal uygulama**.

   ![Hello Azure portal'ın boş mantıksal uygulama ile başlayın](media/iot-hub-monitoring-notifications-with-azure-logic-apps/5_start-with-blank-logic-app-azure-portal.png)

1. Tıklatın **Service Bus**.

   ![Hizmet veri yolu toostart hello Azure portalda mantıksal uygulamanızı oluşturma seçin](media/iot-hub-monitoring-notifications-with-azure-logic-apps/6_select-service-bus-when-creating-blank-logic-app-azure-portal.png)

1. Tıklatın **Service Bus – bir veya daha fazla ileti (Otomatik Tamamlama) kuyrukta geldiğinde**.
1. Hizmet veri yolu bağlantı oluşturun.
   1. Bir bağlantı adı girin.
   1. Merhaba hizmet veri yolu ad alanına tıklayın > merhaba hizmet veri yolu İlkesi > **oluşturma**.

      ![Mantıksal uygulamanız için bir hizmet veri yolu bağlantı hello Azure portal oluşturma](media/iot-hub-monitoring-notifications-with-azure-logic-apps/7_create-service-bus-connection-in-logic-app-azure-portal.png)

   1. Tıklatın **devam** hello hizmet veri yolu bağlantı oluşturulduktan sonra.
   1. Oluşturduğunuz hello kuyruk seçip girin `175` için **en fazla ileti sayısı**

      ![Mantıksal uygulamanızı Hello hello hizmet veri yolu bağlantı için en fazla ileti sayısı belirtin](media/iot-hub-monitoring-notifications-with-azure-logic-apps/8_specify-maximum-message-count-for-service-bus-connection-logic-app-azure-portal.png)
   1. Düğme toosave hello değişiklikleri "Kaydet" seçeneğini tıklatın.

1. SMTP hizmeti bağlantısı oluşturun.
   1. Tıklatın **yeni adım** > **Eylem Ekle**.
   1. Tür `SMTP`, hello tıklatın **SMTP** hizmet hello arama sonucunda ve ardından **SMTP - e-posta Gönder**.

      ![Bir SMTP bağlantı hello Azure portalda mantıksal uygulamanızı oluşturun](media/iot-hub-monitoring-notifications-with-azure-logic-apps/9_create-smtp-connection-logic-app-azure-portal.png)

   1. Posta Hello SMTP bilgilerini girin ve ardından **oluşturma**.

      ![Mantıksal uygulamanızı hello Azure portal, SMTP bağlantı bilgilerini girin](media/iot-hub-monitoring-notifications-with-azure-logic-apps/10_enter-smtp-connection-info-logic-app-azure-portal.png)

      Merhaba SMTP bilgilerini edinin [Hotmail/Outlook.com](https://support.office.com/en-us/article/Add-your-Outlook-com-account-to-another-mail-app-73f3b178-0009-41ae-aab1-87b80fa94970), [Gmail](https://support.google.com/a/answer/176600?hl=en), ve [Yahoo Posta](https://help.yahoo.com/kb/SLN4075.html).
   1. E-posta adresinizi girin **gelen** ve **için**, ve `High temperature detected` için **konu** ve **gövde**.
   1. **Kaydet** düğmesine tıklayın.

kaydettiğinizde hello mantıksal uygulama çalışma sıradadır.

## <a name="test-hello-logic-app"></a>Test hello mantıksal uygulama

1. Tooyour cihazı dağıtma Merhaba istemci uygulaması başlangıç [bağlanmak ESP8266 tooAzure IOT hub'ı](iot-hub-arduino-huzzah-esp8266-get-started.md).
1. Hello ortamı sıcaklığı 30 C. yukarıda hello SensorTag toobe geçici artırın Örneğin, Şamdan, SensorTag geçici açık.
1. Merhaba mantıksal uygulama tarafından gönderilen bir e-posta bildirim almanız gerekir.

   > [!NOTE]
   > E-posta hizmet sağlayıcınıza tooverify hello Gönderen Kimliği toomake hello e-posta gönderir, olduğundan emin gerekebilir.

## <a name="next-steps"></a>Sonraki adımlar

IOT hub'ınızı ve Sıcaklık İzleme ve bildirimler için posta bağlayan bir mantıksal uygulama başarıyla oluşturdunuz.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
