---
title: "Visual Studio için Azure Stream Analytics araçlarını kullanın | Microsoft Docs"
description: "Başlangıç öğreticisi için Visual Studio için Azure Stream Analytics araçları"
keywords: Visual studio
documentationcenter: 
services: stream-analytics
author: 
manager: 
editor: 
ms.assetid: a473ea0a-3eaa-4e5b-aaa1-fec7e9069f20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 
ms.author: 
ms.openlocfilehash: 618c1055795a75e0ed71dacddba3e076f81f4946
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-stream-analytics-tools-for-visual-studio"></a>Visual Studio için Azure Stream Analytics araçlarını kullanın
## <a name="introduction"></a>Giriş
Bu öğreticide, Visual Studio için Azure Stream Analytics araçları oluşturmak, yazar, yerel olarak test, yönetmek ve akış analizi işleri hata ayıklamak için nasıl kullanılacağını öğrenin. 

Bu öğreticiyi tamamladıktan sonra aşağıdakileri gerçekleştirebilirsiniz:
* Visual Studio için Stream Analytics araçları edinin.
* Yapılandırın ve akış analizi işi dağıtın.
* İşinizi yerel örnek verilerle yerel olarak test edin.
* Sorunları gidermek için izleme'yi kullanın.
* Var olan işleri projelerine verin.

## <a name="prerequisites"></a>Ön koşullar
Bu öğreticiyi tamamlamak için aşağıdaki önkoşulları karşılamanız gerekir:
* İçindeki "Stream Analytics işi oluştur" koyun adımlarını tamamlayın [Stream Analytics öğretici kullanarak bir IOT çözümü derleme](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics). 
* Visual Studio 2015, Visual Studio 2013 güncelleştirme 4 veya Visual Studio 2012 kullanın. Enterprise (Ultimate/Premium), Professional ve topluluk sürümleri desteklenir. Express sürümü desteklenmiyor. Visual Studio 2017 desteklenmiyor. 
* .NET sürüm 2.7.1 için Azure SDK'sını kullanın veya sonraki bir sürümü. [Web platformu yükleyicisini](http://www.microsoft.com/web/downloads/platform.aspx) kullanarak yükleyin.
* Yükleme [analiz araçları Visual Studio için akış](http://aka.ms/asatoolsvs).

## <a name="create-a-stream-analytics-project"></a>Stream Analytics projesi oluşturma
1. Visual Studio'da sırasıyla **dosya** menü ve select **yeni proje**. 

2. Sol taraftaki şablonları listesinden seçin **Stream Analytics** ve ardından **Azure Stream Analytics uygulaması**.

3. Proje girin **adı**, **konumu**, ve **çözüm adı** için diğer projeler yaptığınız gibi.

    ![Yeni Proje penceresinin](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-01.png)

    A **Ücretli** proje üretilir **Çözüm Gezgini**.

    ![Çözüm Gezgini'nde oluşturulan Ücretli proje](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-02.png)

## <a name="choose-the-correct-subscription"></a>Doğru abonelik seçin
1. Visual Studio'da sırasıyla **Görünüm** menü ve açık **Sunucu Gezgini**.

2. Azure hesabınızla oturum açın. 

## <a name="define-the-input-sources"></a>Giriş kaynağı tanımlayın
1.  İçinde **Çözüm Gezgini**, genişletin **girişleri** düğümü ve yeniden adlandırma **Input.json** için **EntryStream.json**. Çift **EntryStream.json**.
2.  **Giriş diğer adı** artık **EntryStream**. Giriş diğer adı sorgu komut dosyasındaki kullanılır. 
3.  İçinde **kaynak türü**seçin **veri akışı**.
4.  İçinde **kaynak**seçin **olay hub'ı**.
5.  İçinde **Service Bus Namespace**seçin **TollData** seçeneği.
6.  İçinde **olay hub'ı adı**seçin **girişi**.
7.  İçinde **olay hub'ı ilke adı**seçin **RootManageSharedAccessKey** (varsayılan değer).
8.  İçinde **olayı seri hale getirme biçimi**seçin **Json**. 
9.  İçinde **kodlama**seçin **UTF8**. Ayarlarınız aşağıdaki ekran görüntüsüne görünmelidir:

    ![Giriş penceresi](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-01.png)
 
10. Sihirbazı tamamlamak için tıklatın **kaydetmek**. Artık çıkış akışı oluşturmak için başka bir giriş kaynağı ekleyebilirsiniz. Sağ **girişleri** düğümü ve select **yeni öğe**.

    ![Yeni öğe](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-02.png)
 
11. Penceresinde seçin **Azure Stream Analytics giriş**, değiştirip **adı** için **ExitStream.json**. **Ekle**'ye tıklayın.

    ![Yeni öğe penceresi ekleyin](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-03.png)
 
12. Çift **ExitStream.json** proje ve siz de aynı adımları vermedi için giriş akış izleyin. Girilmelidir **çıkmak** için **olay hub'ı adı** aşağıdaki ekran görüntüsünde gösterildiği gibi:

    ![ExitStream penceresi](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-04.png)

    Şimdi iki giriş akışları tanımladınız:

    ![Giriş ve çıkış giriş akışları](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-05.png)
 
    Ardından, car kayıt verileri içeren blob dosyası için başvuru veri girişi ekleyin.

13. Sağ **girişleri** düğümünü proje ve akış girişleri için yaptığınız gibi aynı adımları sonra izleyin. İçinde **giriş diğer adı**, girin **kayıt**hem de **kaynak türü**seçin **başvuru verileri**.

    ![Kayıt penceresi](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-06.png)

14. İçinde **depolama hesabı**seçin **tolldata** seçeneği. İçinde **kapsayıcı**seçin **tolldata**hem de **yol deseni**, girin **registration.json**. Bu dosya adı büyük/küçük harfe duyarlıdır ve küçük harf olmalıdır.
15. Sihirbazı tamamlamak için tıklatın **kaydetmek**.

Şimdi tüm girişleri tanımlanır.

## <a name="define-the-output"></a>Çıktı tanımlayın
1.  İçinde **Çözüm Gezgini**, genişletin **girişleri** düğümü ve çift **Output.json**.

2.  İçinde **çıkış diğer adları**, girin **çıkış**. 
3.  İçinde **havuzu**seçin **SQL veritabanı**.
4.  İçinde **veritabanı**seçin **TollDataDB**.
5.  İçinde **kullanıcı adı**, girin **tolladmin**. 
6.  İçinde **parola**, girin **123toll!**.
7.  İçinde **tablo**, girin **TollDataRefJoin**.
8.  **Kaydet** düğmesine tıklayın.

    ![Çıktı penceresi](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-output-01.png)
 
## <a name="create-a-stream-analytics-query"></a>Stream Analytics sorgu oluşturma
Bu öğreticide, veri hat ilgili birkaç iş soruları yanıtlamak çalışır. Ayrıca, Stream Analytics ilgili yanıt vermek için kullanılan akış analizi sorgu oluşturur.
İlk Stream Analytics işiniz başlamadan önce basit bir senaryoyu ve sorgu söz dizimi inceleyelim.

### <a name="introduction-to-the-stream-analytics-query-language"></a>Stream Analytics sorgu dili giriş
Ücretli Stand girin taşıtlardan sayısını gerektiğini varsayalım. Bu örnek sürekli akışı olduğundan, bir süre tanımlamak zorunda. "Kaç taşıtlardan üç dakikada Ücretli Stand girin?" olarak soru değiştirme Veri saymak için bu şekilde, genellikle dönen sayım olarak da adlandırılır.

Bu soruya yanıt veren Stream Analytics sorgu arayın:

        SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*) AS Count 
        FROM EntryStream TIMESTAMP BY EntryTime 
        GROUP BY TUMBLINGWINDOW(minute, 3), TollId 

Akış analizi gibi SQL ve sorgu zaman ilgili yönlerini belirlemek için birkaç uzantıları ekler bir sorgu dili kullanır.

Daha fazla bilgi için bkz: [zaman Yönetimi](https://msdn.microsoft.com/library/azure/mt582045.aspx) ve [Pencereleme](https://msdn.microsoft.com/library/azure/dn835019.aspx) MSDN'den sorguda kullanılan yapılar.

İlk Stream Analytics sorgu yazılmış, test zamanı geldi. TollApp klasörü şu yol içinde yer alan örnek veri dosyalarını kullanın:

.. \TollApp\TollApp\Data

Bu klasör, aşağıdaki dosyaları içerir:
*   Entry.JSON
*   Exit.JSON
*   Registration.JSON

## <a name="count-the-number-of-vehicles-entering-a-toll-booth"></a>Ücretli Stand girme taşıtlardan sayısı
Projede çift **Script.asaql** komut dosyasında açmak için **sorgu Düzenleyicisi'ni**. Kopyalayın ve komut dosyası önceki bölümde düzenleyiciye yapıştırın. Sorgu Düzenleyicisi'ni IntelliSense, söz dizimi renklendirme ve hata işaret destekler.

![Sorgu Düzenleyicisi](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-query-01.png)
 
### <a name="test-stream-analytics-queries-locally"></a>Stream Analytics sorguları yerel olarak test etme

1. Bir sözdizimi hatası olup olmadığını görmek için sorguyu derlemek için projesine sağ tıklatın ve **yapı**. 

2. Bu örnek verileri sorgusu doğrulamak için yerel örnek verileri kullanabilirsiniz. Girişi sağ tıklatın ve seçin **yerel girdisi eklemek**.

    ![Yerel giriş Ekle](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-01.png)
 
3. Açılan pencerede, yerel yolundan örnek verileri seçin. **Kaydet** düğmesine tıklayın.

    ![Yerel giriş penceresi ekleyin](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-02.png)
 
    Adlı bir dosya **local_EntryStream.json** girişleri klasörünüze otomatik olarak eklenir.

    ![Girişleri klasöre eklenen dosya](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-03.png)
 
4. İçinde **sorgu Düzenleyicisi'ni**, tıklatın **yerel olarak çalıştır**. Veya F5 tuşuna basın.

    ![Yerel olarak çalıştırma](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-01.png)

    ![Yerel çıkış çalıştırma](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-02.png)

    Çıktıda görüntülemek için herhangi bir tuşa basın **ASA yerel çalıştırma sonucu** Visual Studio'daki. 

    ![ASA yerel çalıştırma sonucu penceresi](./media/stream-analytics-tools-for-vs/local-testing-output.png)

5. Tıklatın **sonuç Klasör Aç** çıktı dosyaları CSV ve JSON biçiminde her ikisini de denetlemek için.

    ![Sonuç klasör çıktısını açın](./media/stream-analytics-tools-for-vs/local-testing-files.png)
 

### <a name="sample-the-input-data"></a>Örnek giriş verisi
Ayrıca, yerel bir dosyaya örnek giriş verileri giriş kaynaklardan erişebilirsiniz. 
1. Giriş yapılandırma dosyasını sağ tıklatın ve seçin **örnek verileri**. 

   ![Örnek Veri](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-01.png)

    Şu an için yalnızca olay hub'ı veya IOT hub'ı örnek oluşturabilirsiniz. Diğer giriş kaynağı desteklenmez.

2. Açılan pencerede örnek verileri kaydetmek için kullanılan yerel yolunu girin. Tıklatın **örnek**.

    ![Örnek veri penceresi](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-02.png)
 
    Devam eden görebilirsiniz **çıkış** penceresi. 

    ![Çıktı penceresi](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-03.png)
 
### <a name="submit-a-stream-analytics-query-to-azure"></a>Azure Stream Analytics sorgu Gönder
1. İçinde **sorgu Düzenleyicisi'ni**, tıklatın **göndermek için Azure** komut dosyası Düzenleyicisi'nde.

    ![Azure'a Gönder](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-01.png)
 
2. Seçin **yeni bir Azure Stream Analytics işi oluşturmak**. Girin **iş adı**, doğru seçin **abonelik**. Tıklatın **gönderme**.

    ![İş pencere Gönder](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-02.png)

 
### <a name="start-a-job"></a>Bir işi Başlat
İşinizi oluşturulur, iş görünümünde otomatik olarak açılır. 
1. İşlemi başlatmak için tıklatın **yeşil ok** düğmesi.

    ![Bir işi Başlat](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-01.png)
 
2. Varsayılan ayar seçin ve tıklayın **Başlat**.
 
    ![İş penceresi başlangıç](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-02.png)

    İş **durum** değişikliklerini **çalıştıran**, ve **giriş olayları** ve **çıkış olaylarındaki** görünür.

    ![İş özeti çalışma durumu](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-03.png)

## <a name="check-the-results-in-visual-studio"></a>Visual Studio'da sonuçlarını denetleyin
1. Visual Studio'da açın **Sunucu Gezgini** ve sağ **TollDataRefJoin** tablo.
2. Seçin **Show Table Data** işinizi çıkışını görmek için.
   
    ![Sunucu Gezgini'nde tablo verileri göster seçimi](media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-check-results.jpg)


### <a name="view-the-job-metrics"></a>İş ölçümleri görüntüleyin
Bazı temel iş istatistiklerinde bulunabilir **iş ölçümleri**. 

![İş ölçümleri penceresi](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-metrics-01.png)

 
## <a name="list-the-job-in-server-explorer"></a>Sunucu Gezgininde iş listesi
İçinde **Sunucu Gezgini**, tıklatın **akış analizi işleri** ve ardından **yenileme**. İş altında görünür **akış analizi işleri**.

![Server Explorer'da listelenen stream Analytics işleri](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-list-jobs-01.png)


## <a name="open-the-job-view"></a>Proje görünümü Aç
İş görünümünde açmak için iş düğümünü genişletin ve çift **iş görünümünde** düğümü.

![İş görünümünde düğümü](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-view-01.png)


## <a name="export-an-existing-job-to-a-project"></a>Var olan bir projeyi
Var olan bir projeye verebilirsiniz iki yolu vardır.

İçinde **Sunucu Gezgini**, proje düğümüne sağ tıklayın **akış analizi işleri** düğümü ve select **verme yeni Stream Analytics projeye**.

![Yeni Stream Analytics projesine aktarma](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-01.png)

Proje içinde oluşturulan **Çözüm Gezgini**.

![Çözüm Gezgini'nde oluşturulan proje](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-02.png)
 
Ayrıca iş görünümünü kullanın ve tıklayın **proje oluştur**.

![Proje oluştur](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-03.png)

## <a name="known-issues-and-limitations"></a>Bilinen sorunlar ve sınırlamalar
 
- Power BI çıkışı ve Azure tarih Lake Store çıktı için desteği yoktur.
- Ekleyerek veya değiştirerek kullanıcı tanımlı işlevler JavaScript için düzenleyici desteği yoktur.

## <a name="next-steps"></a>Sonraki adımlar
* [Azure Stream Analytics'e giriş](stream-analytics-introduction.md)
* [Azure Stream Analytics'i kullanmaya başlama](stream-analytics-real-time-fraud-detection.md)
* [Azure Akış Analizi işlerini ölçeklendirme](stream-analytics-scale-jobs.md)
* [Azure Akış Analizi Sorgu Dili Başvurusu](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Akış Analizi Yönetimi REST API'si Başvurusu](https://msdn.microsoft.com/library/azure/dn835031.aspx)
