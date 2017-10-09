---
title: "aaaIoT gerçek zamanlı veri akışlarını ve Azure akış analizi | Microsoft Docs"
description: "Akış analizi ve gerçek zamanlı veri işleme ile birlikte IoT algılayıcı etiketleri ve veri akışları"
keywords: "iot çözümü, iot ile çalışmaya başlama"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 3e829055-75ed-469f-91f5-f0dc95046bdb
ms.service: stream-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 422e6b719d0289880aa7f17fdc585e2b768c63d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-stream-analytics-tooprocess-data-from-iot-devices"></a>Azure Stream Analytics tooprocess verileri IOT cihazları ile çalışmaya başlama
Bu öğreticide şunları öğreneceksiniz nasıl toocreate akış işleme mantığı toogather veri nesnelerin interneti (IOT) cihazlarından. Gerçek dünya, nesnelerin interneti (IOT) kullanım örneği toodemonstrate nasıl kullanacağız toobuild çözümünüzü hızlı ve ekonomik.

## <a name="prerequisites"></a>Ön koşullar
* [Azure aboneliği](https://azure.microsoft.com/pricing/free-trial/)
* Örnek sorgu ve veri dosyaları [GitHub](https://aka.ms/azure-stream-analytics-get-started-iot)'dan indirilebilir

## <a name="scenario"></a>Senaryo
Merhaba endüstriyel Otomasyon alanında bir şirket olan Contoso, tamamen kendi üretim süreci otomatik. Bu fabrikada bulunan makineler Hello gerçek zamanlı veri akışları yayan özellikli algılayıcılara sahiptir. Bu senaryoda, bir üretim katı Yöneticisi için desenleri toohave gerçek zamanlı bilgiler alarak hello algılayıcı verileri toolook istediği ve bunlar üzerinde işlemler. Merhaba gelen veri akışından hello algılayıcı verileri toofind ilginç kalıpları üzerinden hello Stream Analytics Sorgu Dili'ni (SAQL) kullanacağız.

Burada, veriler bir Texas Instruments algılayıcı etiketi cihazında oluşturulmaktadır.

![Texas Instruments algılayıcı etiketi](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-01.jpg)

Merhaba veri yükünün kimliğinin hello JSON biçiminde ve hello aşağıdaki gibi görünür:

    {
        "time": "2016-01-26T20:47:53.0000000",  
        "dspl": "sensorE",  
        "temp": 123,  
        "hmdt": 34  
    }  

Gerçek hayattaki bir senaryoda, olayları bir akış şeklinde oluşturan bunun gibi yüzlerce algılayıcınız olabilir. İdeal olarak, bir ağ geçidi cihazı kod toopush bu olayları çok çalıştırırsınız:[Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) veya [Azure IOT hub'ları](https://azure.microsoft.com/services/iot-hub/). Stream Analytics işiniz bu olayları Event Hubs'dan alma ve ancak hello akışları karşı gerçek zamanlı analiz sorguları çalıştırmak. Merhaba, hello sonuçları tooone sonra gönderebilir [çıkışları desteklenen](stream-analytics-define-outputs.md).

Kullanım kolaylığı için, bu başlangıç kılavuzunda gerçek algılayıcı etiket cihazlarından yakalanan bir örnek veri dosyası sunulmaktadır. Merhaba örnek verilere sorguları çalıştırmak ve sonuçlarını görebilirsiniz. Sonraki öğreticilerde, öğreneceksiniz nasıl tooconnect, iş tooinputs ve çıkış ve toohello Azure hizmeti dağıtın.

## <a name="create-a-stream-analytics-job"></a>Akış Analizi işi oluşturma
1. Merhaba, [Azure portal](http://portal.azure.com), hello artı işaretini tıklatın ve ardından yazın **STREAM ANALYTICS** hello metin penceresi toohello sağ. Ardından **Stream Analytics işi** hello sonuçları listesinde.
   
    ![Yeni bir Akış Analizi işi oluşturma](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-02.png)
2. Benzersiz iş adı girin ve hello abonelik, iş için doğru bir hello doğrulayın. Ardından yeni bir kaynak grubu oluşturun veya aboneliğinizdeki mevcut bir kaynak grubunu seçin.
3. İşiniz için bir konum seçin. İşleme hızı ve maliyet hello seçerek veri aktarımı'azaltılmasına hello kaynak grubu ve istenen depolama hesabı ile aynı konumda önerilir.
   
    ![Yeni bir Akış Analizi işi oluşturma ayrıntıları](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-03.png)
   
   > [!NOTE]
   > Bu depolama hesabını her bölge için yalnızca bir kez oluşturmanız gerekir. Bu depolama birimi, ilgili bölgede oluşturulan tüm Akış Analizi işlerinde paylaşılır.
   > 
   > 
4. Panonuz işinizde Hello kutusunu tooplace denetleyin ve ardından **oluşturma**.
   
    ![iş oluşturma sürüyor](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-03a.png)
5. 'Bir dağıtım başladı...' görmelisiniz tarayıcı pencerenizin sağ üst hello görüntülenir. En kısa sürede tamamlandı tooa penceresi aşağıda gösterildiği gibi değiştirmek.
   
    ![iş oluşturma sürüyor](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-03b.png)

### <a name="create-an-azure-stream-analytics-query"></a>Azure Akış Analizi sorgusu oluşturma
İşinizi sonra ve yapı bir sorgu, zaman tooopen oluşturuldu. İşinizi hello döşeme tıklatarak kolayca erişebilirsiniz.

![İş kutucuğu](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-04.png)

Merhaba, **iş topoloji** bölmesi hello **sorgu** toogo toohello sorgu Düzenleyicisi'ni kutusu. Merhaba **sorgu** Düzenleyicisi hello gelen olay verilerini hello dönüşümü gerçekleştiren tooenter T-SQL sorgusu tanır.

![Sorgu kutusu](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-05.png)

### <a name="query-archive-your-raw-data"></a>Sorgu: Ham verilerinizi arşivleme
Hello Basit Sorgu biçimi, çıktı atanan tüm giriş verilerini tooits arşivler bir doğrudan sorgudur. Merhaba örnek veri dosyasını indirin [GitHub](https://aka.ms/azure-stream-analytics-get-started-iot) bilgisayarınızda tooa konum. 

1. Merhaba PassThrough.txt dosyasından Hello sorgu yapıştırın. 
   
    ![Giriş akışını test etme](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-06.png)
2. Merhaba üç nokta sonraki tooyour giriş tıklayın ve **dosyasından örnek verileri yükleme** kutusu.
   
    ![Giriş akışını test etme](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-06a.png)
3. Bir bölme hello üzerinde sağ bir sonucu olarak açıldığında, onu seçin hello HelloWorldASA-Inputstream.JSON veri dosya indirilen bulunduğunuz yerden ve'ı tıklatın **Tamam** hello bölmesini hello sonundaki.
   
    ![Giriş akışını test etme](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-06b.png)
4. Merhaba ardından **Test** gear hello penceresinin sol hello üst ve test sorgunuzu hello örnek veri kümesi karşı işlem. Merhaba işleme tam olarak sonuçları penceresi sorgunuzu açın.
   
    ![Test sonuçları](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-07.png)

### <a name="query-filter-hello-data-based-on-a-condition"></a>Sorgu: hello verileri bir koşula göre filtrele
Toofilter hello sonuçları bir koşula göre deneyelim. Yalnızca "sensorA" gelen olaylar için tooshow sonuçları isteriz. Merhaba, hello Filtering.txt dosyasında sorgudur.

![Bir veri akışını filtreleme](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-08.png)

Büyük küçük harfe duyarlı sorgu hello Not bir dize değeri karşılaştırır. Merhaba tıklatın **Test** yeniden tooexecute hello sorgu gear. Merhaba sorgu 1860 olay 389 satır döndürmelidir.

![Sorgu testine ilişkin ikinci çıktı sonuçları](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-09.png)

### <a name="query-alert-tootrigger-a-business-workflow"></a>Sorgu: Uyarı tootrigger bir iş akışı
Şimdi sorgumuzu daha ayrıntılı hale getirelim. Her algılayıcı türü için toomonitor ortalama sıcaklığı 30 saniyelik pencere başına istediğiniz ve yalnızca hello ortalama sıcaklık 100 derecenin ise sonuçları görüntüler. Biz hello aşağıdaki sorgu ve ardından yazacak **Test** toosee hello sonuçları. Merhaba, hello ThresholdAlerting.txt dosyasında sorgudur.

![30 saniyelik filtre sorgusu](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-10.png)

Şimdi hello ortalama Sıcaklığın 100'den büyük olduğu yalnızca 245 satırı ve algılayıcılar adlarını içeren sonuçları görmeniz gerekir. Bu sorgu tarafından olayların hello akış grupları **grupladık**, üzerinde hello algılayıcı adı olan bir **atlayan pencereyi** 30 saniye. Zamana bağlı sorguları zaman tooprogress nasıl istiyoruz belirtmelidir. Hello kullanarak **TIMESTAMP BY** yan tümcesi hello belirtmiş olduğunuz **OUTPUTTIME** sütun tooassociate süreleri zamana bağlı tüm hesaplamalar ile. Hakkında ayrıntılı bilgi için hello MSDN makaleleri okuyun [zaman Yönetimi](https://msdn.microsoft.com/library/azure/mt582045.aspx) ve [Pencereleme işlevleri](https://msdn.microsoft.com/library/azure/dn835019.aspx).

### <a name="query-detect-absence-of-events"></a>Sorgu: Var olmayan olayları algılama
Nasıl biz giriş olaylarını eksikliği sorgu toofind yazabilirim? Şimdi hello son zamanı algılayıcı gönderilen veri ve olayları hello sonraki dakika sonra göndermedi bulur. Merhaba, hello AbsenseOfEvent.txt dosyasında sorgudur.

![Var olmayan olayları algılama](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-11.png)

Burada kullandığımız bir **LEFT OUTER** toohello katılma aynı veri akışı (kendi kendine birleşme). Bir **INNER** birleşimde, yalnızca bir eşleşme bulunduğu zaman bir sonuç döndürülür.  İçin bir **LEFT OUTER** birleştirme, bir olay hello birleştirme yan sol hello eşleşmeyen, ise tüm sütunları hello sağ tarafı hello için NULL değere sahip bir satır döndürülür. Bu teknik çok kullanışlı toofind olayları olmayışı olur. [JOIN](https://msdn.microsoft.com/library/azure/dn835026.aspx) hakkında daha fazla bilgi edinmek için MSDN belgelerimize bakın.

## <a name="conclusion"></a>Sonuç
Bu öğretici Hello amacı nasıl toowrite farklı Stream Analytics sorgu dili sorgular ve bakın sonuçları hello tarayıcıda toodemonstrate budur. Ancak bu sadece bir başlangıçtır. Akış Analizi ile yapabileceğiniz daha birçok şey bulunmaktadır. Akış analizi girişleri ve çıkışları çeşitli destekler ve bile işlevini kullan Azure Machine Learning toomake, veri akışlarını çözümleme için güçlü bir araç. Stream Analytics hakkında daha fazla tooexplore kullanarak başlatabilirsiniz bizim [öğrenme haritamızı](https://azure.microsoft.com/documentation/learning-paths/stream-analytics/). Hakkında daha fazla bilgi için toowrite sorguları hakkında hello makaleyi okuyun, [ortak sorgu kalıpları](stream-analytics-stream-analytics-query-patterns.md).

