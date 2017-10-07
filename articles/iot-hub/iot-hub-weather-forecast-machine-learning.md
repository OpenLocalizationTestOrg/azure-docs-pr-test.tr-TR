---
title: "IOT hub'ı verilerle Azure Machine Learning kullanarak tahmin aaaWeather | Microsoft Docs"
description: "Azure Machine Learning toopredict hello Yağmur olasılığını hello sıcaklık ve nem algılayıcı IOT hub'ınızı topladığı veri tabanlı kullanın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: machine learning hava durumu tahmini
ms.assetid: 8ba7d9e7-699c-4448-b353-0f3e1429d198
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: xshi
ms.openlocfilehash: 04abe97558ccfc152bae2e0d435033433c0023dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="weather-forecast-using-hello-sensor-data-from-your-iot-hub-in-azure-machine-learning"></a>IOT hub'ınızı hello algılayıcı verilerini Azure Machine Learning kullanarak hava durumu tahmini

![Uçtan uca diyagramı](media/iot-hub-get-started-e2e-diagram/6.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

Machine learning, mevcut veri tooforecast gelecekteki davranışları, sonuçları ve eğilimleri öğrenin bilgisayarlar yardımcı olan veri bilimi bir tekniktir. Azure Machine Learning olası tooquickly kolaylaştıran bir bulut Tahmine dayalı analiz hizmeti oluşturma ve Tahmine dayalı modelleri analiz çözümleri olarak dağıtma ' dir.

## <a name="what-you-learn"></a>Öğrenecekleriniz

Nasıl toouse Azure Machine Learning toodo hava tahmini (Yağmur olasılığını) kullanarak izin ver hello Azure IOT hub'ınızı sıcaklık ve nem verilerden öğrenin. Yağmur Hello olasılığını hello hazırlıklı hava durumu Tahmini modeli çıkışıdır. Merhaba modeli geçmiş verileri tooforecast sıcaklık ve nem göre Yağmur olasılığını bağlı yerleşik olarak bulunur.

## <a name="what-you-do"></a>Neler

- Merhaba hava durumu Tahmini modeli bir web hizmeti olarak dağıtın.
- IOT hub'ınızı bir tüketici grubu ekleyerek veri erişimi için hazırlanın.
- Stream Analytics işi oluşturmak ve hello projeye yapılandırın:
  - IOT hub'ından sıcaklık ve nem verilerini okur.
  - Merhaba web hizmeti tooget hello Yağmur fırsat çağırın.
  - Merhaba sonuç tooan Azure blob depolama kaydedin.
- Microsoft Azure Storage Gezgini tooview hello hava tahmini kullanın.

## <a name="what-you-need"></a>Ne gerekiyor

- Öğretici [Cihazınızı](iot-hub-raspberry-pi-kit-node-get-started.md) hangi hello gereksinimleri aşağıdaki kapsayan tamamlandı:
  - Etkin bir Azure aboneliği.
  - Azure IOT hub'ı aboneliğinizdeki.
  - Tooyour Azure IOT hub'ı iletileri gönderir bir istemci uygulaması.
- Bir Azure Machine Learning Studio hesabı. ([Machine Learning Studio ücretsiz deneyin](https://studio.azureml.net/)).

## <a name="deploy-hello-weather-prediction-model-as-a-web-service"></a>Merhaba hava durumu Tahmini modeli bir web hizmeti olarak dağıtma

1. Toohello Git [hava durumu Tahmini modeli sayfasına](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1).
1. Tıklatın **Studio'da Aç** Microsoft Azure Machine Learning Studio'da.
   ![Açık hello hava durumu Tahmini modeli sayfasında Cortana Intelligence Galerisi](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)
1. Tıklatın **çalıştırmak** toovalidate hello hello modelinde adımları. Bu adım 2 dakika toocomplete sürebilir.
   ![Azure Machine Learning Studio'da Aç hello hava durumu Tahmini modeli](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)
1. Tıklatın **WEB hizmetini kurma** > **Tahmine dayalı Web hizmeti**.
   ![Azure Machine Learning Studio'da Hello hava durumu tahmini model dağıtma](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)
1. Merhaba şemada hello sürükleyin **Web hizmeti girişi** modülü hello yakın bir yerde **Score Model** modülü.
1. Merhaba bağlanmak **Web hizmeti girişi** modülü toohello **Score Model** modülü.
   ![Azure Machine Learning Studio'da iki modülleri Bağlan](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)
1. Tıklatın **çalıştırmak** toovalidate hello hello modelinde adımları.
1. Tıklatın **WEB hizmeti Dağıt** bir web hizmeti olarak toodeploy hello modeli.
1. Hello modeli Hello Panoda hello karşıdan **Excel 2010 veya önceki çalışma kitabı** için **istek/yanıt**.

   > [!Note]
   > Hello karşıdan olun **Excel 2010 veya önceki çalışma kitabı** bilgisayarınızda Excel daha sonraki bir sürümünü çalıştırıyor olsanız bile.

   ![Merhaba Excel hello istek YANITI uç noktası için karşıdan yükle](media/iot-hub-weather-forecast-machine-learning/5_download-endpoint-app-excel-for-request-response.png)

1. Merhaba Excel çalışma kitabını, hello Not **WEB hizmeti URL'si** ve **erişim tuşu**.

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a>Oluşturma, yapılandırma ve akış analizi işi çalıştırma

### <a name="create-a-stream-analytics-job"></a>Akış Analizi işi oluşturma

1. Merhaba, [Azure portal](https://ms.portal.azure.com/), tıklatın **yeni** > **nesnelerin interneti** > **Stream Analytics işi**.
1. Aşağıdaki bilgilerle hello işi için hello girin.

   **İş adı**: hello işinin hello adı. Merhaba adı genel olarak benzersiz olmalıdır.

   **Kaynak grubu**: kullanım hello aynı IOT hub'ınızı kullanan kaynak grubu.

   **Konum**: kullanım hello aynı konumu, kaynak grubu olarak.

   **PIN toodashboard**: kolay erişim tooyour IOT hub'hello panosundan için bu seçeneği işaretleyin.

   ![Stream Analytics işi oluşturma](media/iot-hub-weather-forecast-machine-learning/7_create-stream-analytics-job-azure.png)

1. **Oluştur**'a tıklayın.

### <a name="add-an-input-toohello-stream-analytics-job"></a>Bir giriş toohello Stream Analytics işi ekleme

1. Açık hello Stream Analytics işi.
1. Altında **iş topoloji**, tıklatın **girişleri**.
1. Merhaba, **girişleri** bölmesinde tıklatın **Ekle**ve ardından aşağıdaki bilgilerle hello girin:

   **Giriş diğer adı**: hello hello giriş için benzersiz diğer ad.

   **Kaynak**: seçin **IOT hub'ı**.

   **Tüketici grubu**: oluşturduğunuz Select hello tüketici grubu.

   ![Azure'da bir giriş toohello Stream Analytics işi ekleme](media/iot-hub-weather-forecast-machine-learning/8_add-input-stream-analytics-job-azure.png)

1. **Oluştur**'a tıklayın.

### <a name="add-an-output-toohello-stream-analytics-job"></a>Bir çıkış toohello Stream Analytics işi ekleme

1. Altında **iş topoloji**, tıklatın **çıkışları**.
1. Hello içinde **çıkışları** bölmesinde tıklatın **Ekle**ve ardından aşağıdaki bilgilerle hello girin:

   **Çıkış diğer adları**: hello hello çıktı için benzersiz diğer ad.

   **Havuz**: seçin **Blob Storage**.

   **Depolama hesabı**: Merhaba blob depolama alanınızın için depolama hesabı. Bir depolama hesabı oluşturun veya var olan bir kullanın.

   **Kapsayıcı**: hello blob kaydettiğiniz yere hello kapsayıcı. Bir kapsayıcı oluşturmak veya mevcut bir kullanın.

   **Olayı seri hale getirme biçimi**: seçin **CSV**.

   ![Azure'da bir çıktı toohello Stream Analytics işi ekleme](media/iot-hub-weather-forecast-machine-learning/9_add-output-stream-analytics-job-azure.png)

1. **Oluştur**'a tıklayın.

### <a name="add-a-function-toohello-stream-analytics-job-toocall-hello-web-service-you-deployed"></a>Bir işlev toohello dağıttığınız Stream Analytics işi toocall hello web hizmeti Ekle

1. Altında **iş topoloji**, tıklatın **işlevleri** > **Ekle**.
1. Aşağıdaki bilgilerle hello girin:

   **İşlev diğer**: girin `machinelearning`.

   **İşlev türü**: seçin **Azure ML**.

   **Alma seçeneği**: seçin **farklı bir abonelik alma**.

   **URL**: hello Excel çalışma kitabından hello aşağı ettiğiniz bir WEB hizmeti URL'si girin.

   **Anahtar**: hello Excel çalışma kitabından hello aşağı ettiğiniz erişim anahtarı girin.

   ![Azure'da işlevi toohello akış analizi işi ekleme](media/iot-hub-weather-forecast-machine-learning/10_add-function-stream-analytics-job-azure.png)

1. **Oluştur**'a tıklayın.

### <a name="configure-hello-query-of-hello-stream-analytics-job"></a>Merhaba Stream Analytics işi Hello sorgusu yapılandırın

1. Altında **iş topoloji**, tıklatın **sorgu**.
1. Merhaba var olan kodu koddan hello ile değiştirin:

   ```sql
   WITH machinelearning AS (
      SELECT EventEnqueuedUtcTime, temperature, humidity, machinelearning(temperature, humidity) as result from [YourInputAlias]
   )
   Select System.Timestamp time, CAST (result.[temperature] AS FLOAT) AS temperature, CAST (result.[humidity] AS FLOAT) AS humidity, CAST (result.[Scored Probabilities] AS FLOAT ) AS 'probabalities of rain'
   Into [YourOutputAlias]
   From machinelearning
   ```

   Değiştir `[YourInputAlias]` hello işin giriş hello diğer adına sahip.

   Değiştir `[YourOutputAlias]` hello işin hello çıkış diğer adına sahip.

1. **Kaydet** düğmesine tıklayın.

### <a name="run-hello-stream-analytics-job"></a>Merhaba Stream Analytics işini çalıştır

Merhaba Stream Analytics işinde tıklatın **Başlat** > **şimdi** > **Başlat**. Merhaba işi başarıyla başladıktan sonra hello iş durumu değişiklikleri **durduruldu** çok**çalıştıran**.

![Merhaba Stream Analytics işini çalıştır](media/iot-hub-weather-forecast-machine-learning/11_run-stream-analytics-job-azure.png)

## <a name="use-microsoft-azure-storage-explorer-tooview-hello-weather-forecast"></a>Microsoft Azure Storage Gezgini tooview hello hava tahmini kullanın

Merhaba istemci uygulaması toostart toplama ve veri tooyour IOT hub sıcaklık ve nem gönderme çalıştırın. IOT hub'ınızın aldığı her ileti için hello Stream Analytics işi hello hava tahmini web hizmeti tooproduce hello olasılığını Yağmur çağırır. Merhaba sonuç sonra tooyour Azure blob depolama kaydedilir. Azure Storage Gezgini tooview hello sonuç kullanabileceğiniz bir araçtır.

1. [Microsoft Azure Storage Gezgini yükleyip](http://storageexplorer.com/).
1. Azure Depolama Gezgini'ni açın.
1. İçinde tooyour Azure hesabı oturum açın.
1. Aboneliğinizi seçin.
1. Aboneliğinizi tıklayın > **depolama hesapları** > depolama hesabınız > **Blob kapsayıcıları** >, kapsayıcı.
1. Bir .csv dosyası toosee hello sonuç açın. Merhaba son sütun kayıtları Yağmur olasılığını hello.

   ![Azure Machine Learning ile hava tahmini sonucu alın](media/iot-hub-weather-forecast-machine-learning/12_get-weather-forecast-result-azure-machine-learning.png)

## <a name="summary"></a>Özet

Azure Machine Learning tooproduce hello IOT hub'ınızı alan hello sıcaklık ve nem verilerine dayalı Yağmur olasılığını başarıyla kullandığınız.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]