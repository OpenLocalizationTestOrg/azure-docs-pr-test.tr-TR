---
title: Azure Stream Analytics aaaPower BI Panoda | Microsoft Docs
description: "Yüksek hacimli bir akış analizi işi verileri çözümlemek ve bir gerçek zamanlı akış Power BI Panosu toogather iş zekası kullanın."
keywords: "Analytics Pano, gerçek zamanlı Panosu"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: fe8db732-4397-4e58-9313-fec9537aa2ad
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: jeffstok
ms.openlocfilehash: cb9127576230e9d327b437b674f31cc23869bfff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-and-power-bi-a-real-time-analytics-dashboard-for-streaming-data"></a>Analizler ve Power BI akış: veri akışı için gerçek zamanlı analiz Panosu
Azure Stream Analytics, iş zekası araçları, baştaki hello birinin tootake avantajı sağlar [Microsoft Power BI](https://powerbi.com/). Bu makalede, bilgi nasıl iş zekası araçları, Azure akış analizi işi için çıkış olarak Power BI kullanarak oluşturun. Da bilgi nasıl toocreate ve gerçek zamanlı bir Panoda kullanın.

Bu makalede Stream Analytics hello devam [gerçek zamanlı sahtekarlık algılama](stream-analytics-real-time-fraud-detection.md) Öğreticisi. Bu öğreticide oluşturduğunuz hello iş akışı oluşturur ve böylece bir akış analizi işi tarafından algılanan sahte telefon aramaları görselleştirebilirsiniz çıktı Power BI ekler. 

İzleyebilir [video](https://www.youtube.com/watch?v=SGUpT-a99MA) bu senaryo gösterilmektedir.


## <a name="prerequisites"></a>Ön koşullar

Başlamadan önce hello aşağıdaki sahip olduğunuzdan emin olun:

* Bir Azure hesabı.
* Power BI için bir hesap. Bir iş veya Okul hesabı kullanabilirsiniz.
* Merhaba tamamlanmış bir sürümünü [gerçek zamanlı sahtekarlık algılama](stream-analytics-real-time-fraud-detection.md) Öğreticisi. Başlangıç Öğreticisi kurgusal telefonla meta verileri oluşturan bir uygulamayı içerir. Merhaba öğreticide, bir olay hub'ı oluşturun ve telefon araması veri toohello olay hub'ı akış hello gönderin. Sahte çağrıları (aynı hello sayı hello gelen çağrıları aynı, farklı konumlarda'saat) algıladığı için bir sorgu yazın. 


## <a name="add-power-bi-output"></a>Power BI çıkışı ekleme
Merhaba gerçek zamanlı sahtekarlık algılama öğreticide hello çıktı tooAzure Blob depolama alanına gönderilir. Bu bölümde, bilgi tooPower BI gönderir bir çıktı ekleyin.

1. Hello Azure portal, daha önce oluşturduğunuz hello akış analizi işi'ni açın. Merhaba önerilen ad kullandıysanız hello iş adlı `sa_frauddetection_job_demo`.

2. Select hello **çıkışları** hello işi Panosu hello ortadaki kutusuna ve ardından **+ Ekle**.

3. İçin **çıkış diğer adları**, girin `CallStream-PowerBI`. Farklı bir ad kullanabilirsiniz. Bunu yaparsanız, hello adı daha sonra gerektiğinden, not edin. 

4. Altında **havuzu**seçin **Power BI**.

   ![Power BI için bir çıktı oluşturmak](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut.png)

5. Tıklatın **yetkilendirmek**.

    Burada bir iş veya Okul hesabı için Azure kimlik bilgilerinizi sağlayabilir penceresi açılır. 

    ![Erişim tooPower BI kimlik bilgilerini girin](./media/stream-analytics-power-bi-dashboard/authorize-area.png)

6. Kimlik bilgilerinizi girin. Kimlik bilgilerinizi girdiğinizde Power BI alanınızı izni toohello akış analizi işi tooaccess de yaparken sonra unutmayın.

7. Ne zaman, döndürülen toohello **yeni çıktı** dikey penceresinde, aşağıdaki bilgilerle hello girin:

    * **Çalışma grubu**: Power BI kiracınızın toocreate hello dataset istediğiniz bir çalışma alanı seçin.
    * **Veri kümesi adı**: girin `sa-dataset`. Farklı bir ad kullanabilirsiniz. Bunu yaparsanız, bunu daha sonra kullanmak üzere not.
    * **Tablo adı**: girin `fraudulent-calls`. Şu anda, akış analizi işleri Power BI çıkışı bir veri kümesinde yalnızca bir tablo olabilir.

    ![PBI çalışma](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut-with-dataset-table.png)

    > [!WARNING]
    > Power BI bir veri kümesi varsa ve sahip tablo hello hello aynı adları hello Stream Analytics işinde belirttiğiniz olanları var olanları hello üzerine yazılır.
    > Siz açıkça bu veri kümesi ve tablo Power BI hesabınızı oluşturmamanızı öneririz. Merhaba işini pompa çıkış Power BI'da oturum başlatır ve akış analizi işi başlattığınızda otomatik olarak oluşturulur. Sorgu iş herhangi bir sonuç döndürmezse hello veri kümesi ve tablo oluşturulmaz.
    >

8. **Oluştur**'a tıklayın.

Merhaba veri kümesi ayarları aşağıdaki hello ile oluşturulur:

* **defaultRetentionPolicy: BasicFIFO**: FIFO, en çok 200.000 satırları içeren verilerdir.
* **defaultMode: pushStreaming**: hello dataset akış döşeme ve geleneksel rapor tabanlı görselleri (paketini destekler anında iletme).

Şu anda diğer bayraklarıyla veri kümesi oluşturulamıyor.

Power BI veri kümeleri hakkında daha fazla bilgi için bkz: Merhaba [Power BI REST API](https://msdn.microsoft.com/library/mt203562.aspx) başvuru.


## <a name="write-hello-query"></a>Merhaba sorgu yazma

1. Kapat hello **çıkışları** dikey penceresinde ve dönüş toohello iş dikey penceresi.

2. Merhaba tıklatın **sorgu** kutusu. 

3. Sorgu aşağıdaki hello girin. Bu sorgu hello sahtekarlık algılama öğreticide oluşturduğunuz benzer toohello kendi kendine birleşim sorgudur. Merhaba bu sorgu sonuçları toohello yeni oluşturduğunuz çıkış gönderir farktır (`CallStream-PowerBI`). 

    >[!NOTE]
    >Hello giriş değil adlandırırsanız `CallStream` hello sahtekarlık algılama öğreticide için adınızı alternatif `CallStream` hello içinde **FROM** ve **katılma** hello sorgu yan tümcelerinde.

        /* Our criteria for fraud:
        Calls made from hello same caller tootwo phone switches in different locations (for example, Australia and Europe) within five seconds */

        SELECT System.Timestamp AS WindowEnd, COUNT(*) AS FraudulentCalls
        INTO "CallStream-PowerBI"
        FROM "CallStream" CS1 TIMESTAMP BY CallRecTime
        JOIN "CallStream" CS2 TIMESTAMP BY CallRecTime

        /* Where hello caller is hello same, as indicated by IMSI (International Mobile Subscriber Identity) */
        ON CS1.CallingIMSI = CS2.CallingIMSI

        /* ...and date between CS1 and CS2 is between one and five seconds */
        AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5

        /* Where hello switch location is different */
        WHERE CS1.SwitchNum != CS2.SwitchNum
        GROUP BY TumblingWindow(Duration(second, 1))

4. **Kaydet** düğmesine tıklayın.


## <a name="test-hello-query"></a>Test hello sorgusu
Bu bölümde, isteğe bağlı ancak önerilir. 

1. Merhaba TelcoStreaming uygulama şu anda çalışmıyorsa başlatın, aşağıdaki adımları izleyerek:

    * Bir komut penceresi açın.
    * Merhaba telcogenerator.exe ve değiştirilmiş telcodatagen.exe.config dosyaları nerede toohello klasörüne gidin.
    * Merhaba aşağıdaki komutu çalıştırın:

            telcodatagen.exe 1000 .2 2

2. Merhaba, **sorgu** dikey penceresinde hello nokta sonraki toohello tıklatın `CallStream` girin ve ardından **örnek giriş verilerinden**.

3. Veri ve tıklatın üç dakika eşitleyeceğini istediğinizi belirtin **Tamam**. Merhaba veri örneklendirilen haberdar kadar bekleyin.

4. Tıklatın **Test** ve sonuçları alınırken emin olun.


## <a name="run-hello-job"></a>Merhaba işini çalıştır

1. Bu hello TelcoStreaming uygulama çalıştığından emin olun.

2. Kapat hello **sorgu** dikey.

3. Merhaba iş dikey penceresinde tıklayın **Başlat**.

    ![Merhaba Stream Analytics işi Başlat](./media/stream-analytics-power-bi-dashboard/stream-analytics-sa-job-start-output.png)

Akış analizi işi hello gelen akış sahte çağrılarında arayan başlatır. Hello iş ayrıca hello veri kümesi ve tablo Power BI'da oluşturur ve hello sahte çağrıları toothem ilgili veri göndermeye başlar.


## <a name="create-hello-dashboard-in-power-bi"></a>Power BI'da Hello pano oluşturun

1. Çok Git[Powerbi.com](https://powerbi.com) ve iş veya Okul hesabınızla oturum açın. Merhaba Stream Analytics işi sorgu sonuçları çıkışı yapıyorsa, veri kümesi zaten oluşturulmuş bakın:

    ![Power bı'da akış veri kümesi](./media/stream-analytics-power-bi-dashboard/streaming-dataset.png)

2. Çalışma alanınızda tıklatın  **+ &nbsp;oluşturma**.

    ![Power BI çalışma alanında Hello oluştur düğmesi](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard.png)

3. Yeni bir pano oluşturun ve adlandırın `Fraudulent Calls`.

    ![Bir pano oluşturun ve Power BI çalışma alanında bir ad verin](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard-name.png)

4. Merhaba penceresinin Hello üstünde tıklatın **Ekle döşeme**seçin **özel akış veri**ve ardından **sonraki**.

    ![Özel veri kümesi akış](./media/stream-analytics-power-bi-dashboard/custom-streaming-data.png)

5. Altında **bilgisayarınızı DATSETS**, kümenizi seçin ve ardından **sonraki**.

    ![Akış Veri kümenizi](./media/stream-analytics-power-bi-dashboard/your-streaming-dataset.png)

6. Altında **görselleştirme türü**seçin **kartı**ve ardından hello **alanları** listesinde **fraudulentcalls**.

    ![Yeni kutucuk için görselleştirme ayrıntıları](./media/stream-analytics-power-bi-dashboard/add-fraud.png)

7. **İleri**’ye tıklayın.

8. Başlık ve alt başlık gibi kutucuğu ayrıntıları doldurun.

    ![Başlık ve yeni kutucuk için alt başlığı](./media/stream-analytics-power-bi-dashboard/pbi-new-tile-details.png)

9. **Uygula**'ya tıklayın.

    Şimdi bir sahtekarlık sayaç var!

    ![Sahtekarlık sayacı](./media/stream-analytics-power-bi-dashboard/fraud-counter.png)

8. İzleme hello tooadd (4. adım ile başlayarak) bir kutucuk yeniden adımları. Bu süre, aşağıdaki hello:

    * Çok ulaştıklarında**görselleştirme türü**seçin **çizgi grafiği**. 
    * Eksen ekleme ve seçin **windowend**. 
    * Bir değer ekleyip seçin **fraudulentcalls**.
    * İçin **zaman penceresi toodisplay**seçin son 10 dakika hello.

    ![Bölme çizgi grafiği için oluşturma](./media/stream-analytics-power-bi-dashboard/pbi-create-tile-line-chart.png)

9. Tıklatın **sonraki**, başlık ve alt başlık eklemek ve tıklayın **Uygula**.

    Merhaba Power BI panosuna şimdi, iki veri görünümlerini sahte çağrıları hakkında veri akış hello algılanan olarak sağlar.

    ![Power BI panosuna sahte çağrıları için iki kutucuk gösteren tamamlandı](./media/stream-analytics-power-bi-dashboard/pbi-dashboard-fraudulent-calls-finished.png)


## <a name="learn-more-about-power-bi"></a>Power BI hakkında bilgi alın

Bu öğretici gösterir nasıl toocreate görselleştirmeleri bir veri kümesi için yalnızca birkaç tür. Power BI, kuruluşunuzun diğer müşteri iş zekası araçları oluşturmanıza yardımcı olabilir. Daha fazla fikir için kaynakları aşağıdaki hello bakın:

* Merhaba Power BI panosuna başka bir örneği için izleme [Power BI ile çalışmaya başlama](https://youtu.be/L-Z_6P56aas?t=1m58s) video.
* Akış analizi yapılandırma hakkında daha fazla bilgi için proje çıktı tooPower BI ve Power BI gruplarını kullanarak hello gözden [Power BI](stream-analytics-define-outputs.md#power-bi) hello bölümünü [Stream Analytics çıkarır](stream-analytics-define-outputs.md) makalesi. 
* Power BI genellikle kullanma hakkında daha fazla bilgi için bkz: [Power BI panoları](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/).


## <a name="learn-about-limitations-and-best-practices"></a>Sınırlamalar ve en iyi uygulamalar hakkında bilgi edinin
Şu anda Power BI kabaca saniye başına bir kez çağrılabilir. Akış görselleri 15 KB paketlerini destekler. Ötesinde, akış görselleri başarısız (ancak anında iletme toowork devam eder). Bu sınırlamalar nedeniyle Power BI kendisini en doğal olarak Azure akış analizi önemli veri yükünü azaltma burada mu toocases uygundur. Atlayan pencere veya veri gönderimi bir anında iletme saniye başına en fazla olduğunu ve sorgunuzu hello işleme gereksinimleri içinde adlandırıldığını Hopping penceresi tooensure kullanmanızı öneririz.

Saniye cinsinden pencerenizi eşitlik toocompute hello değeri toogive aşağıdaki hello kullanabilirsiniz:

![Equation1](./media/stream-analytics-power-bi-dashboard/equation1.png)  

Örneğin:

* Verileri bir saniyelik aralıklarda gönderme 1.000 cihazları var.
* Merhaba Power BI Pro saat başına 1.000.000 satır destekleyen SKU kullanıyor.
* Toopublish hello aygıt tooPower BI başına ortalama veri miktarını istiyor.

Sonuç olarak, hello eşitlik olur:

![Equation2](./media/stream-analytics-power-bi-dashboard/equation2.png)  

Bu yapılandırma verildiğinde, hello özgün sorgu toohello aşağıdakileri değiştirebilirsiniz:

    SELECT
        MAX(hmdt) AS hmdt,
        MAX(temp) AS temp,
        System.TimeStamp AS time,
        dspl
    INTO "CallStream-PowerBI"
    FROM
        Input TIMESTAMP BY time
    GROUP BY
        TUMBLINGWINDOW(ss,4),
        dspl


### <a name="renew-authorization"></a>Yetkilendirmeyi yenileyin
Merhaba parola işinizi oluşturulmuş veya son kimliği doğrulanmış oluşturulmasından sonra değiştirilmişse, Power BI hesabınızı tooreauthenticate gerekir. Azure Active Directory (Azure AD) kiracınızın Azure çok faktörlü kimlik doğrulaması yapılandırılmışsa, ayrıca toorenew Power BI yetkilendirme iki haftada gerekir. Yenilemezseniz, iş çıktısı eksikliği gibi Belirtiler görebilir veya bir `Authenticate user error` hello işlem günlüğüne kaydeder.

Benzer şekilde, hello belirtecin süresi dolduktan sonra bir iş başlatılır, bir hata oluşur ve hello işi başarısız olur. tooresolve bu sorunu çalıştıran hello işini durdurmak ve Power BI çıktı tooyour gidin. tooavoid veri kaybı select hello **yetkilendirmeyi yenileyin** işinizi hello gelen yeniden başlatın ve bağlama **son durdurulma zamanı**.

Power BI ile Merhaba yetkilendirme yenilendikten sonra yeşil bir uyarı hello sorunu Çözümlendi hello yetkilendirme alanı tooreflect görünür.

## <a name="get-help"></a>Yardım alın
Daha fazla yardım için deneyin bizim [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Sonraki adımlar
* [Giriş tooAzure akış analizi](stream-analytics-introduction.md)
* [Azure Akış Analizi'ni kullanmaya başlama](stream-analytics-real-time-fraud-detection.md)
* [Azure Akış Analizi işlerini ölçeklendirme](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics sorgu dili başvurusu](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics Yönetimi REST API Başvurusu](https://msdn.microsoft.com/library/azure/dn835031.aspx)
