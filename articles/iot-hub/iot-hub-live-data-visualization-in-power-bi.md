---
title: "Azure IOT Hub – Power BI algılayıcı verilerini aaaReal zaman veri Görselleştirme | Microsoft Docs"
description: "Hello algılayıcı ' toplanan ve tooyour Azure IOT hub gönderilen Power BI toovisualize sıcaklık ve nem verileri kullanın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "gerçek zamanlı veri görselleştirme, dinamik veri görselleştirme algılayıcı verileri Görselleştirme"
ms.assetid: e67c9c09-6219-4f0f-ad42-58edaaa74f61
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: xshi
ms.openlocfilehash: d79ce757a9f2ab7a4744e8a0c523106e0f72cecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-real-time-sensor-data-from-azure-iot-hub-using-power-bi"></a>Azure IOT Hub'ın Power BI kullanarak gerçek zamanlı algılayıcı verilerini görselleştirmek

![Uçtan uca diyagramı](media/iot-hub-get-started-e2e-diagram/4.png)


[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a>Öğrenecekleriniz

Hakkında bilgi edineceksiniz nasıl Azure IOT hub'ınızı alan toovisualize gerçek zamanlı algılayıcı verilerini Power BI tarafından. Tootry istiyorsanız hello veri görselleştirme IOT hub'ınıza Web uygulamalarıyla, lütfen bkz. [kullanım Azure Web Apps toovisualize gerçek zamanlı algılayıcı verileri Azure IOT Hub](iot-hub-live-data-visualization-in-web-apps.md).

## <a name="what-you-do"></a>Neler

- IOT hub'ınızı bir tüketici grubu ekleyerek veri erişimi için hazırlanın.
- Oluşturmak, yapılandırmak ve veri aktarımı için Stream Analytics işi, IOT hub tooyour Power BI hesabınızı çalıştırın.
- Oluşturma ve Power BI rapor toovisualize hello veri yayımlama.

## <a name="what-you-need"></a>Ne gerekiyor

- Öğretici [Cihazınızı](iot-hub-raspberry-pi-kit-node-get-started.md) hangi hello gereksinimleri aşağıdaki kapsayan tamamlandı:
  - Etkin bir Azure aboneliği.
  - Azure IOT hub'ı aboneliğinizdeki.
  - Tooyour Azure IOT hub'ı iletileri gönderir bir istemci uygulaması.
- Power BI hesabınız. ([Power BI ücretsiz deneyin](https://powerbi.microsoft.com/))

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a>Oluşturma, yapılandırma ve akış analizi işi çalıştırma

### <a name="create-a-stream-analytics-job"></a>Akış Analizi işi oluşturma

1. İçinde Azure portal Merhaba, yeni tıklayın > nesnelerin interneti > Stream Analytics işi.
1. Aşağıdaki bilgilerle hello işi için hello girin.

   **İş adı**: hello işinin hello adı. Merhaba adı genel olarak benzersiz olmalıdır.

   **Kaynak grubu**: kullanım hello aynı IOT hub'ınızı kullanan kaynak grubu.

   **Konum**: kullanım hello aynı konumu, kaynak grubu olarak.

   **PIN toodashboard**: kolay erişim tooyour IOT hub'hello panosundan için bu seçeneği işaretleyin.

   ![Stream Analytics işi oluşturma](media/iot-hub-live-data-visualization-in-power-bi/2_create-stream-analytics-job-azure.png)

1. **Oluştur**'a tıklayın.

### <a name="add-an-input-toohello-stream-analytics-job"></a>Bir giriş toohello Stream Analytics işi ekleme

1. Açık hello Stream Analytics işi.
1. Altında **iş topoloji**, tıklatın **girişleri**.
1. Merhaba, **girişleri** bölmesinde tıklatın **Ekle**ve ardından aşağıdaki bilgilerle hello girin:

   **Giriş diğer adı**: hello hello giriş için benzersiz diğer ad.

   **Kaynak**: seçin **IOT hub'ı**.

   **Tüketici grubu**: yeni oluşturduğunuz Select hello tüketici grubu.
1. **Oluştur**'a tıklayın.

   ![Azure'da bir giriş tooa Stream Analytics işi ekleme](media/iot-hub-live-data-visualization-in-power-bi/3_add-input-to-stream-analytics-job-azure.png)

### <a name="add-an-output-toohello-stream-analytics-job"></a>Bir çıkış toohello Stream Analytics işi ekleme

1. Altında **iş topoloji**, tıklatın **çıkışları**.
1. Hello içinde **çıkışları** bölmesinde tıklatın **Ekle**ve ardından aşağıdaki bilgilerle hello girin:

   **Çıkış diğer adları**: hello hello çıktı için benzersiz diğer ad.

   **Havuz**: seçin **Power BI**.
1. Tıklatın **Authorize**ve Power BI hesabınızda oturum açın.
1. Yetkilendirildikten sonra aşağıdaki bilgilerle hello girin:

   **Çalışma grubu**: hedef grup çalışma alanınızı seçin.

   **Veri kümesi adı**: bir veri kümesi adı girin.

   **Tablo adı**: Tablo adı girin.
1. **Oluştur**'a tıklayın.

   ![Azure'da bir çıktı tooa Stream Analytics işi ekleme](media/iot-hub-live-data-visualization-in-power-bi/4_add-output-to-stream-analytics-job-azure.png)

### <a name="configure-hello-query-of-hello-stream-analytics-job"></a>Merhaba Stream Analytics işi Hello sorgusu yapılandırın

1. Altında **iş topoloji**, tıklatın **sorgu**.
1. Değiştir `[YourInputAlias]` hello işin giriş hello diğer adına sahip.
1. Değiştir `[YourOutputAlias]` hello işin hello çıkış diğer adına sahip.
1. **Kaydet** düğmesine tıklayın.

   ![Azure'da bir sorgu tooa Stream Analytics işi ekleme](media/iot-hub-live-data-visualization-in-power-bi/5_add-query-stream-analytics-job-azure.png)

### <a name="run-hello-stream-analytics-job"></a>Merhaba Stream Analytics işini çalıştır

Merhaba Stream Analytics işinde tıklatın **Başlat** > **şimdi** > **Başlat**. Merhaba işi başarıyla başladıktan sonra hello iş durumu değişiklikleri **durduruldu** çok**çalıştıran**.

![Azure Stream Analytics işini çalıştır](media/iot-hub-live-data-visualization-in-power-bi/6_run-stream-analytics-job-azure.png)

## <a name="create-and-publish-a-power-bi-report-toovisualize-hello-data"></a>Oluşturma ve bir Power BI rapor toovisualize hello verileri yayımlama

1. Merhaba örnek uygulaması aygıtınızda çalıştığından emin olun. Toohello öğreticileri altında başvurabilir, varsa [Cihazınızı](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started).
1. İçinde tooyour oturum [Power BI](https://powerbi.microsoft.com/en-us/) hesabı.
1. Merhaba çıktı hello Stream Analytics işi için oluşturduğunuzda ayarladığınız toohello Grup çalışma alanına gidin.
1. Tıklatın **veri kümeleri akış**.

   Merhaba Stream Analytics işi çıkış hello oluşturduğunuzda belirttiğiniz listelenen hello dataset görmeniz gerekir.
1. Altında **Eylemler**, hello ilk simge toocreate bir raporu tıklatın.

   ![Microsoft Power BI raporu oluşturma](media/iot-hub-live-data-visualization-in-power-bi/7_create-power-bi-report-microsoft.png)

1. Bir çizgi grafiği tooshow gerçek zamanlı sıcaklık zamanla oluşturun.
   1. Merhaba rapor oluşturma sayfasında bir çizgi grafiği ekleyin.
   1. Merhaba üzerinde **alanları** bölmesinde hello çıktı hello Stream Analytics işi için oluşturduğunuzda belirttiğiniz hello tablosunu genişletin.
   1. Sürükleme **EventEnqueuedUtcTime** çok**eksen** hello üzerinde **görselleştirmeleri** bölmesi.
   1. Sürükleme **sıcaklık** çok**değerleri**.

      Şimdi bir çizgi grafiği oluşturulur. Merhaba x ekseni hello UTC saat diliminde tarih ve saati görüntüler. Merhaba y ekseni hello algılayıcı sıcaklık görüntüler.

      ![Bir çizgi grafiği için sıcaklık tooa Microsoft Power BI raporu ekleme](media/iot-hub-live-data-visualization-in-power-bi/8_add-line-chart-for-temperature-to-power-bi-report-microsoft.png)

1. Başka bir çizgi grafiği tooshow gerçek zamanlı nem zamanla oluşturun. toodo Bu, aynı adımları yukarıda hello izleyin ve yerleştirin **EventEnqueuedUtcTime** hello x ekseni üzerinde ve **nem** hello y ekseni üzerinde.

   ![Bir çizgi grafiği için nem tooa Microsoft Power BI raporu ekleme](media/iot-hub-live-data-visualization-in-power-bi/9_add-line-chart-for-humidity-to-power-bi-report-microsoft.png)

1. Tıklatın **kaydetmek** toosave hello rapor.
1. Tıklatın **dosya** > **tooweb yayımlama**.
1. Tıklatın **oluşturma katıştırma kodunu**ve ardından **Yayımla**.

Web günlüğünüze veya Web sitesi herkes rapor erişim ve bir kod parçacığı toointegrate hello raporu ile paylaşabilir hello rapor bağlantısı sağlanan.

![Microsoft Power BI rapor yayımlayın](media/iot-hub-live-data-visualization-in-power-bi/10_publish-power-bi-report-microsoft.png)

Microsoft ayrıca hello sunar [Power BI mobil uygulamalarından](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/) görüntüleme ve Power BI panolarınızı ve raporlarınızı ile etkileşim için mobil Cihazınızda.

## <a name="next-steps"></a>Sonraki adımlar

Azure IOT hub'ından Power BI toovisualize gerçek zamanlı algılayıcı verilerini başarıyla kullanmış olduğunuz.
Azure IOT hub'ı bir alternatif bir yol toovisualize verileri yoktur. Bkz: [kullanım Azure Web Apps toovisualize gerçek zamanlı algılayıcı verileri Azure IOT Hub](iot-hub-live-data-visualization-in-web-apps.md).

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
