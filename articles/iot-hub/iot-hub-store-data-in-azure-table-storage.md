---
title: "aaaSave IOT hub'ınızı tooAzure veri depolama iletileri | Microsoft Docs"
description: "Bir Azure işlevi uygulama toosave, IOT hub iletileri tooyour Azure tablo depolaması kullanın. Merhaba IOT hub iletileri IOT aygıtınızdan gönderilen algılayıcı verileri gibi bilgileri içerir."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "IOT veri depolama, IOT algılayıcı veri depolama"
ms.assetid: 62fd14fd-aaaa-4b3d-8367-75c1111b6269
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: be72d9ba9a781822926364351b50f58f5d96e94a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="save-iot-hub-messages-that-contain-sensor-data-tooyour-azure-table-storage"></a>Algılayıcı verileri tooyour Azure tablo depolaması içeren IOT hub iletileri kaydetme

![Uçtan uca diyagramı](media/iot-hub-get-started-e2e-diagram/3.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a>Öğrenecekleriniz

Toocreate bir Azure storage hesabını ve Azure app toostore IOT hub iletileri tablo depolama alanınızın nasıl işlev öğrenin.

## <a name="what-you-do"></a>Neler

- Bir Azure Storage hesabı oluşturun.
- IOT hub'ınızı bağlantısı tooread iletileri hazırlayın.
- Oluşturun ve bir Azure işlevi uygulamayı dağıtın.

## <a name="what-you-need"></a>Ne gerekiyor

- [Cihazınızı ayarlamak](iot-hub-raspberry-pi-kit-node-get-started.md) gereksinimlerine toocover hello:
  - Etkin bir Azure aboneliği
  - Aboneliğinizdeki IOT hub'ı 
  - Tooyour IOT hub'ı iletileri gönderir çalışan bir uygulama

## <a name="create-an-azure-storage-account"></a>Azure Storage hesabı oluşturma

1. Merhaba, [Azure portal](https://portal.azure.com/), tıklatın **yeni** > **depolama** > **depolama hesabı**  >   **Oluşturma**.

2. Merhaba hello depolama hesabı için gerekli bilgileri girin:

   ![Hello Azure portal depolama hesabı oluşturma](media\iot-hub-store-data-in-azure-table-storage\1_azure-portal-create-storage-account.png)

   * **Ad**: hello depolama hesabının hello adı. Merhaba adı genel olarak benzersiz olmalıdır.

   * **Kaynak grubu**: kullanım hello aynı IOT hub'ınızı kullanan kaynak grubu.

   * **PIN toodashboard**: hello panodan tooyour IOT hub'ı kolay erişim için bu seçeneği belirleyin.

3. **Oluştur**'a tıklayın.

## <a name="prepare-your-iot-hub-connection-tooread-messages"></a>IOT hub'ınızı bağlantısı tooread iletileri hazırlama

IOT hub'ı bir yerleşik olay hub ile uyumlu uç tooenable uygulamaları tooread IOT hub iletileri gösterir. Bu sırada, uygulamaları tüketici grupları tooread verileri IOT hub'ınızı kullanın. Bir Azure işlevi uygulama tooread verileri IOT hub'ından oluşturmadan önce aşağıdaki hello:

- IOT hub uç noktanızı Hello bağlantı dizesini edinin.
- IOT hub'ınız için bir tüketici grubu oluşturun.

### <a name="get-hello-connection-string-of-your-iot-hub-endpoint"></a>IOT hub uç noktanızı Hello bağlantı dizesi alma

1. IOT hub'ınızı açın.

2. Merhaba üzerinde **IOT hub'ı** bölmesi altında **ileti**, tıklatın **uç noktaları**.

3. Hello bölmesini altında sağ **yerleşik uç noktaları**, tıklatın **olayları**.

4. Merhaba, **özellikleri** bölmesinde, aşağıdaki değerleri Not hello:
   - Olay hub ile uyumlu uç noktası
   - Olay hub ile uyumlu adı

   ![IOT hub uç noktanızı Hello bağlantı dizesi hello Azure portal Al](media\iot-hub-store-data-in-azure-table-storage\2_azure-portal-iot-hub-endpoint-connection-string.png)

5. Merhaba, **IOT hub'ı** bölmesi altında **ayarları**, tıklatın **paylaşılan erişim ilkeleri**.

6. Tıklatın **iothubowner**.

7. Not hello **birincil anahtar** değeri.

8. IOT hub uç noktanızı Hello bağlantı dizesi gibi oluşturun:

   `Endpoint=<Event Hub-compatible endpoint>;SharedAccessKeyName=iothubowner;SharedAccessKey=<Primary key>`

   > [!NOTE]
   > Değiştir `<Event Hub-compatible endpoint>` ve `<Primary key>` daha önce not ettiğiniz hello değerlere sahip.

### <a name="create-a-consumer-group-for-your-iot-hub"></a>IOT hub'ınız için bir tüketici grubu oluştur

1. IOT hub'ınızı açın.

2. Merhaba, **IOT hub'ı** bölmesi altında **ileti**, tıklatın **uç noktaları**.

3. Hello bölmesini altında sağ **yerleşik uç noktaları**, tıklatın **olayları**.

4. Merhaba, **özellikleri** bölmesi altında **tüketici grupları**, bir ad girin ve ardından bir not edin.

5. **Kaydet** düğmesine tıklayın.

## <a name="create-and-deploy-an-azure-function-app"></a>Oluşturma ve bir Azure işlevi uygulama dağıtma

1. Merhaba, [Azure portal](https://portal.azure.com/), tıklatın **yeni** > **işlem** > **işlev uygulaması**  >   **Oluşturma**.

2. Merhaba hello işlev uygulaması için gerekli bilgileri girin.

   ![Hello Azure portal işlev uygulaması oluşturma](media\iot-hub-store-data-in-azure-table-storage\3_azure-portal-create-function-app.png)

   * **Uygulama adı**: hello işlevi uygulamasının hello adı. Merhaba adı genel olarak benzersiz olmalıdır.

   * **Kaynak grubu**: kullanım hello aynı IOT hub'ınızı kullanan kaynak grubu.

   * **Depolama hesabı**: Merhaba oluşturduğunuz depolama hesabı.

   * **PIN toodashboard**: hello panosundan kolay erişim toohello işlev uygulaması için bu seçeneği işaretleyin.

3. **Oluştur**'a tıklayın.

4. Merhaba işlev uygulaması oluşturulduktan sonra açın.

5. Merhaba işlevi uygulamada hello aşağıdakileri yaparak yeni bir işlev oluşturun:

   a. Tıklatın **yeni işlev**.

   b. Seçin **JavaScript** için **dil**, ve **veri işleme** için **senaryo**.

   c. Tıklatın **bu işlev oluşturma**ve ardından **yeni işlev**.

   d. Seçin **JavaScript** hello dilin ve **veri işleme** hello senaryosu için.

   e. Merhaba tıklatın **EventHubTrigger JavaScript** şablonu.

   f. Merhaba hello şablonu için gerekli bilgileri girin.

      * **İşlevinizin adı**: hello işlevinin hello adı.

      * **Olay hub'ı adı**: daha önce not ettiğiniz hello olay hub ile uyumlu adı.

      * **Olay Hub bağlantısı**: tooadd hello bağlantı dizesi, oluşturduğunuz hello IOT hub uç tıklatın **yeni**.

   g. **Oluştur**'a tıklayın.

6. Bir çıkış hello işlevinin hello aşağıdakileri yaparak yapılandırın:

   a. Tıklatın **tümleştirmek** > **yeni çıktı** > **Azure Table Storage** > **seçin**.

      ![Tablo depolama tooyour işlev uygulaması hello Azure portal Ekle](media\iot-hub-store-data-in-azure-table-storage\4_azure-portal-function-app-add-output-table-storage.png)

   b. Merhaba gerekli bilgileri girin.

      * **Tablo parametre adı**: kullanım `outputTable`, hangi kullanılacak hello Azure işlevin kodu.
      
      * **Tablo adı**: kullanım `deviceData`.

      * **Depolama hesabı bağlantısı**: tıklatın **yeni**ve ardından seçin veya depolama hesabınızı girin. Merhaba depolama hesabı görüntülenmiyorsa bkz [depolama hesabı gereksinimleri](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal#storage-account-requirements).
      
   c. **Kaydet** düğmesine tıklayın.

7. Altında **Tetikleyicileri**, tıklatın **Azure olay hub'ı (eventHubMessages)**.

8. Altında **Event Hub tüketici grubu**, oluşturulan ve ardından hello tüketici grubu hello adını **kaydetmek**.

9. Sol hello üzerinde oluşturulan hello işlevi tıklayın ve ardından **dosyaları görüntüle** hello sağ üzerinde.

10. Merhaba kodla `index.js` hello aşağıdaki ile:

   ```javascript
   'use strict';

   // This function is triggered each time a message is received in hello IoT hub.
   // hello message payload is persisted in an Azure storage table
 
   module.exports = function (context, iotHubMessage) {
    context.log('Message received: ' + JSON.stringify(iotHubMessage));
    var date = Date.now();
    var partitionKey = Math.floor(date / (24 * 60 * 60 * 1000)) + '';
    var rowKey = date + '';
    context.bindings.outputTable = {
     "partitionKey": partitionKey,
     "rowKey": rowKey,
     "message": JSON.stringify(iotHubMessage)
    };
    context.done();
   };
   ```

11. **Kaydet** düğmesine tıklayın.

Merhaba işlev uygulaması oluşturdunuz. Tablo deponuzda IOT hub'ınızın aldığı iletileri depolar.

> [!NOTE]
> Merhaba kullanabilirsiniz **çalıştırmak** düğmesini tootest hello işlev uygulaması. Tıkladığınızda **çalıştırmak**, hello sınama iletisi tooyour IOT hub'ı gönderilir. Merhaba varış hello iletisinin hello işlevi uygulama toostart tetiklemek ve hello ileti tooyour tablo depolama Kaydet gerekir. Merhaba **günlükleri** bölmesinde hello işleminin hello ayrıntıları kaydeder.

## <a name="verify-your-message-in-your-table-storage"></a>Tablo depolama alanınızın iletinize doğrulayın

1. Merhaba örnek uygulaması, aygıt toosend iletileri tooyour IOT hub'ına çalıştırın.

2. [Azure Storage Gezgini yükleyip](http://storageexplorer.com/).

3. Depolama Gezgini'ni açın, **Azure Hesap Ekle** > **oturum**ve ardından tooyour Azure hesabı açın.

4. Azure aboneliğiniz tıklayın > **depolama hesapları** > depolama hesabınız > **tabloları** > **deviceData**.

   Hello oturum, aygıt tooyour IOT hub'dan gönderilen iletileri görmelisiniz `deviceData` tablo.

## <a name="next-steps"></a>Sonraki adımlar

Azure depolama hesabı ve tablo deponuzda IOT hub'ınızın aldığı iletileri depolayan Azure işlev uygulaması başarıyla oluşturdunuz.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
