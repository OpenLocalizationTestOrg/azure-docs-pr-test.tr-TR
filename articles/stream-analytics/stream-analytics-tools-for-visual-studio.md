---
title: "Visual Studio için Azure Stream Analytics araçları aaaUse | Microsoft Docs"
description: "Başlangıç Öğreticisi hello Visual Studio için Azure Stream Analytics araçları için"
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
ms.openlocfilehash: bda8e548040509a6f29f1b713268bc38f73228fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-stream-analytics-tools-for-visual-studio"></a>Visual Studio için Azure Stream Analytics araçlarını kullanın
## <a name="introduction"></a>Giriş
Bu öğreticide, nasıl toouse Azure Stream Analytics araçları Visual Studio toocreate için yazar, yerel olarak test, yönetmek ve akış analizi işleri hata ayıklama öğrenin. 

Bu öğreticiyi tamamladıktan sonra aşağıdakileri gerçekleştirebilirsiniz:
* Visual Studio için Stream Analytics araçları edinin.
* Yapılandırın ve akış analizi işi dağıtın.
* İşinizi yerel örnek verilerle yerel olarak test edin.
* İzleme tootroubleshoot sorunlar kullanın.
* Varolan işleri tooprojects verin.

## <a name="prerequisites"></a>Ön koşullar
toocomplete Bu öğretici önkoşulları aşağıdaki hello gerekir:
* Hello "Stream Analytics işi oluştur" koyun hello adımlarını tamamlayın [Stream Analytics öğretici kullanarak bir IOT çözümü derleme](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics). 
* Visual Studio 2015, Visual Studio 2013 güncelleştirme 4 veya Visual Studio 2012 kullanın. Enterprise (Ultimate/Premium), Professional ve topluluk sürümleri desteklenir. Express sürümü desteklenmiyor. Visual Studio 2017 desteklenmiyor. 
* Kullanım hello .NET sürüm 2.7.1 için Azure SDK'sı veya sonraki bir sürümü. Hello kullanarak yükleme [Web Platformu yükleyicisi](http://www.microsoft.com/web/downloads/platform.aspx).
* Merhaba yüklemek [akış analiz araçları Visual Studio için](http://aka.ms/asatoolsvs).

## <a name="create-a-stream-analytics-project"></a>Stream Analytics projesi oluşturma
1. Visual Studio'da hello tıklatın **dosya** menü ve select **yeni proje**. 

2. Merhaba şablonları listesinden hello soldaki seçin **Stream Analytics** ve ardından **Azure Stream Analytics uygulaması**.

3. Merhaba proje girin **adı**, **konumu**, ve **çözüm adı** için diğer projeler yaptığınız gibi.

    ![Yeni Proje penceresinin](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-01.png)

    A **Ücretli** proje üretilir **Çözüm Gezgini**.

    ![Çözüm Gezgini'nde oluşturulan Ücretli proje](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-02.png)

## <a name="choose-hello-correct-subscription"></a>Merhaba doğru abonelik seçin
1. Visual Studio'da hello tıklatın **Görünüm** menü ve açık **Sunucu Gezgini**.

2. Azure hesabınızla oturum açın. 

## <a name="define-hello-input-sources"></a>Merhaba giriş kaynaklarıyla tanımlayın
1.  İçinde **Çözüm Gezgini**, hello genişletin **girişleri** düğümü ve yeniden adlandırma **Input.json** çok**EntryStream.json**. Çift **EntryStream.json**.
2.  Merhaba **giriş diğer adı** artık **EntryStream**. Merhaba giriş diğer adı hello sorgu komut dosyasında kullanılır. 
3.  İçinde **kaynak türü**seçin **veri akışı**.
4.  İçinde **kaynak**seçin **olay hub'ı**.
5.  İçinde **Service Bus Namespace**seçin hello **TollData** seçeneği.
6.  İçinde **olay hub'ı adı**seçin **girişi**.
7.  İçinde **olay hub'ı ilke adı**seçin **RootManageSharedAccessKey** (Merhaba varsayılan değer).
8.  İçinde **olayı seri hale getirme biçimi**seçin **Json**. 
9.  İçinde **kodlama**seçin **UTF8**. Ayarlarınızı hello ekran aşağıdaki gibi görünmelidir:

    ![Giriş penceresi](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-01.png)
 
10. toofinish hello Sihirbazı'nı tıklatın **kaydetmek**. Artık başka bir giriş kaynağı toocreate hello çıkış akışı ekleyebilirsiniz. Sağ hello **girişleri** düğümü ve select **yeni öğe**.

    ![Yeni öğe](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-02.png)
 
11. Merhaba penceresinde seçin **Azure Stream Analytics giriş**, hello değiştirip **adı** çok**ExitStream.json**. **Ekle**'ye tıklayın.

    ![Yeni öğe penceresi ekleyin](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-03.png)
 
12. Çift **ExitStream.json** hello proje ve hello Giriş akışı için yaptığınız gibi aynı adımları izleyin hello. Emin tooenter olması **çıkmak** hello için **olay hub'ı adı** hello ekran aşağıdaki gösterildiği gibi:

    ![ExitStream penceresi](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-04.png)

    Şimdi iki giriş akışları tanımladınız:

    ![Giriş ve çıkış giriş akışları](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-05.png)
 
    Ardından, car kayıt verilerini içeren hello blob dosyası için başvuru veri girişi ekleyin.

13. Sağ hello **girişleri** düğümünü hello proje ve hello akış girişleri için yaptığınız gibi aynı adımları izleyin hello. İçinde **giriş diğer adı**, girin **kayıt**hem de **kaynak türü**seçin **başvuru verileri**.

    ![Kayıt penceresi](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-06.png)

14. İçinde **depolama hesabı**seçin hello **tolldata** seçeneği. İçinde **kapsayıcı**seçin **tolldata**hem de **yol deseni**, girin **registration.json**. Bu dosya adı büyük/küçük harfe duyarlıdır ve küçük harf olmalıdır.
15. toofinish hello Sihirbazı'nı tıklatın **kaydetmek**.

Şimdi tüm hello girişleri tanımlanır.

## <a name="define-hello-output"></a>Merhaba çıkış tanımlayın
1.  İçinde **Çözüm Gezgini**, hello genişletin **girişleri** düğümü ve çift **Output.json**.

2.  İçinde **çıkış diğer adları**, girin **çıkış**. 
3.  İçinde **havuzu**seçin **SQL veritabanı**.
4.  İçinde **veritabanı**seçin **TollDataDB**.
5.  İçinde **kullanıcı adı**, girin **tolladmin**. 
6.  İçinde **parola**, girin **123toll!**.
7.  İçinde **tablo**, girin **TollDataRefJoin**.
8.  **Kaydet** düğmesine tıklayın.

    ![Çıktı penceresi](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-output-01.png)
 
## <a name="create-a-stream-analytics-query"></a>Stream Analytics sorgu oluşturma
Bu öğretici tooanswer ilgili tootoll veri birkaç iş soruları çalışır. Ayrıca, Stream Analytics tooprovide ilgili yanıtlarında kullanılabilir Stream Analytics sorgu oluşturur.
İlk Stream Analytics işiniz başlamadan önce basit bir senaryo ve hello sorgu sözdizimi inceleyelim.

### <a name="introduction-toohello-stream-analytics-query-language"></a>Giriş toohello Stream Analytics sorgu dili
Ücretli Stand girin taşıtlardan toocount hello sayısı gerektiğini varsayalım. Bu örnek sürekli akışı olduğundan, bir süre toodefine sahip. "Kaç taşıtlardan üç dakikada Ücretli Stand girin?" Merhaba soru toobe değiştirme Yaygın olarak verilerdir bu şekilde toocount tooas hello dönen sayısı denir.

Bu soruya yanıt veren hello Stream Analytics sorgusu bakın:

        SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*) AS Count 
        FROM EntryStream TIMESTAMP BY EntryTime 
        GROUP BY TUMBLINGWINDOW(minute, 3), TollId 

Akış analizi gibi SQL ve birkaç uzantıları toospecify saati ile ilgili yönlerini hello sorgu ekleyen bir sorgu dili kullanır.

Daha fazla bilgi için bkz: [zaman Yönetimi](https://msdn.microsoft.com/library/azure/mt582045.aspx) ve [Pencereleme](https://msdn.microsoft.com/library/azure/dn835019.aspx) MSDN'den hello sorguda kullanılan yapılar.

İlk Stream Analytics sorgu yazılmış, zaman tootest olduğundan bu. Merhaba örnek veri dosyalarını TollApp klasörü yolu izleyerek hello içinde bulunan kullanın:

.. \TollApp\TollApp\Data

Bu klasör, aşağıdaki dosyaları hello içerir:
*   Entry.JSON
*   Exit.JSON
*   Registration.JSON

## <a name="count-hello-number-of-vehicles-entering-a-toll-booth"></a>Ücretli Stand girme taşıtlardan Hello sayısı
Hello projesinde çift **Script.asaql** tooopen hello komut dosyasında hello **sorgu Düzenleyicisi'ni**. Kopyalama ve hello betik hello önceki bölümde hello düzenleyicisine yapıştırın. IntelliSense, söz dizimi renklendirme ve hello hata işaret Hello sorgu Düzenleyicisi'ni destekler.

![Sorgu Düzenleyicisi](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-query-01.png)
 
### <a name="test-stream-analytics-queries-locally"></a>Stream Analytics sorguları yerel olarak test etme

1. bir sözdizimi hatası ise toocompile hello sorgu toosee hello projesine sağ tıklatın ve **yapı**. 

2. toovalidate bu sorguyu örnek verileri karşı yerel örnek verileri kullanabilirsiniz. Merhaba girişi sağ tıklatın ve seçin **yerel girdisi eklemek**.

    ![Yerel giriş Ekle](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-01.png)
 
3. Merhaba açılır penceresinde hello örnek verileri yerel yolundan seçin. **Kaydet** düğmesine tıklayın.

    ![Yerel giriş penceresi ekleyin](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-02.png)
 
    Adlı bir dosya **local_EntryStream.json** tooyour giriş klasörü otomatik olarak eklenir.

    ![Dosya eklenen tooinputs klasörü](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-03.png)
 
4. Merhaba, **sorgu Düzenleyicisi'ni**, tıklatın **yerel olarak çalıştır**. Veya hello F5 tuşuna basın.

    ![Yerel olarak çalıştırma](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-01.png)

    ![Yerel çıkış çalıştırma](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-02.png)

    Herhangi bir anahtar tooview hello çıktı hello basın **ASA yerel çalıştırma sonucu** Visual Studio'daki. 

    ![ASA yerel çalıştırma sonucu penceresi](./media/stream-analytics-tools-for-vs/local-testing-output.png)

5. Tıklatın **sonuç Klasör Aç** toocheck hello çıktı dosyaları hem de CSV ve JSON biçimi.

    ![Sonuç klasör çıktısını açın](./media/stream-analytics-tools-for-vs/local-testing-files.png)
 

### <a name="sample-hello-input-data"></a>Örnek hello giriş verileri
Ayrıca, giriş kaynağı tooa yerel dosyadan örnek giriş verileri de erişebilirsiniz. 
1. Merhaba giriş yapılandırma dosyasını sağ tıklatın ve seçin **örnek verileri**. 

   ![Örnek Veri](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-01.png)

    Şu an için yalnızca olay hub'ı veya IOT hub'ı örnek oluşturabilirsiniz. Diğer giriş kaynağı desteklenmez.

2. Merhaba açılır penceresinde hello kullanılan yerel yolu toosave hello örnek verileri girin. Tıklatın **örnek**.

    ![Örnek veri penceresi](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-02.png)
 
    Merhaba hello ediyor görebilirsiniz **çıkış** penceresi. 

    ![Çıktı penceresi](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-03.png)
 
### <a name="submit-a-stream-analytics-query-tooazure"></a>Stream Analytics sorgu tooAzure Gönder
1. Merhaba, **sorgu Düzenleyicisi'ni**, tıklatın **tooAzure gönderme** hello komut dosyası Düzenleyicisi'nde.

    ![TooAzure Gönder](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-01.png)
 
2. Seçin **yeni bir Azure Stream Analytics işi oluşturmak**. Merhaba girin **iş adı**ve select hello doğru **abonelik**. Tıklatın **gönderme**.

    ![İş pencere Gönder](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-02.png)

 
### <a name="start-a-job"></a>Bir işi Başlat
İşinizi oluşturulur, hello iş görünümünde otomatik olarak açılır. 
1. toostart hello işi, hello tıklatın **yeşil ok** düğmesi.

    ![Bir işi Başlat](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-01.png)
 
2. Merhaba varsayılan ayarı seçin ve'ı tıklatın **Başlat**.
 
    ![İş penceresi başlangıç](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-02.png)

    Merhaba iş **durum** çok değiştirir**çalıştıran**, ve **giriş olayları** ve **çıkış olaylarındaki** görünür.

    ![İş özeti çalışma durumu](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-03.png)

## <a name="check-hello-results-in-visual-studio"></a>Visual Studio'da hello sonuçları denetleyin
1. Visual Studio'da açın **Sunucu Gezgini** ve sağ hello **TollDataRefJoin** tablo.
2. Seçin **Show Table Data** işinizin toosee hello çıktı.
   
    ![Sunucu Gezgini'nde tablo verileri göster seçimi](media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-check-results.jpg)


### <a name="view-hello-job-metrics"></a>Merhaba iş metrikleri görüntüleyin
Bazı temel iş istatistiklerinde bulunabilir **iş ölçümleri**. 

![İş ölçümleri penceresi](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-metrics-01.png)

 
## <a name="list-hello-job-in-server-explorer"></a>Sunucu Gezgininde listesi hello işi
İçinde **Sunucu Gezgini**, tıklatın **akış analizi işleri** ve ardından **yenileme**. Merhaba iş altında görünür **akış analizi işleri**.

![Server Explorer'da listelenen stream Analytics işleri](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-list-jobs-01.png)


## <a name="open-hello-job-view"></a>Açık hello işi görüntüle
tooopen hello iş görünümünde, iş düğümünü genişletin ve hello çift **iş görünümünde** düğümü.

![İş görünümünde düğümü](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-view-01.png)


## <a name="export-an-existing-job-tooa-project"></a>Mevcut bir iş tooa projesini dışarı aktarma
Mevcut bir iş tooa projesini verebilirsiniz iki yolu vardır.

İçinde **Sunucu Gezgini**, sağ hello iş hello düğümünde **akış analizi işleri** düğümü ve select **tooNew Stream Analytics proje verme**.

![Stream Analytics proje tooNew dışarı aktarma](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-01.png)

Merhaba proje üretilir **Çözüm Gezgini**.

![Çözüm Gezgini'nde oluşturulan proje](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-02.png)
 
Ayrıca hello iş görünümünde kullanın ve tıklatın **proje oluştur**.

![Proje oluştur](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-03.png)

## <a name="known-issues-and-limitations"></a>Bilinen sorunlar ve sınırlamalar
 
- Power BI çıkışı ve Azure tarih Lake Store çıktı için desteği yoktur.
- Ekleyerek veya değiştirerek kullanıcı tanımlı işlevler JavaScript için düzenleyici desteği yoktur.

## <a name="next-steps"></a>Sonraki adımlar
* [Giriş tooAzure akış analizi](stream-analytics-introduction.md)
* [Azure Stream Analytics'i kullanmaya başlama](stream-analytics-real-time-fraud-detection.md)
* [Azure Akış Analizi işlerini ölçeklendirme](stream-analytics-scale-jobs.md)
* [Azure Akış Analizi Sorgu Dili Başvurusu](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Akış Analizi Yönetimi REST API'si Başvurusu](https://msdn.microsoft.com/library/azure/dn835031.aspx)
