---
title: "Azure akış Analizi ile aaaReal zamanı Twitter düşünceleri çözümleme | Microsoft Docs"
description: "Bilgi nasıl toouse Stream Analytics gerçek zamanlı Twitter düşünceleri çözümleme için. Olay oluşturma toodata canlı bir Pano üzerinde Adım Adım Kılavuzu."
keywords: "gerçek zamanlı twitter eğilim analizi, düşünceleri analiz, sosyal medya analizi, eğilim analizi örneği"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 42068691-074b-4c3b-a527-acafa484fda2
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: jeffstok
ms.openlocfilehash: 157790caa7ea6f5570dd9c9d3bd9694d437eb4c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-twitter-sentiment-analysis-in-azure-stream-analytics"></a>Azure Stream Analytics gerçek zamanlı Twitter düşünceleri analizi

Bilgi nasıl toobuild düşünceleri analiz çözümü gerçek zamanlı getiren tarafından sosyal medya analizi için Twitter olayları Azure Event Hubs'a. Bir Azure akış analizi sorgu tooanalyze hello veri ve iki depoda hello sonuçlar daha sonra kullanmak için veya bir Pano kullanın sonra yazma ve [Power BI](https://powerbi.com/) tooprovide Öngörüler gerçek zamanlı.

Sosyal medya analiz araçları, kuruluşların oluşturan eğilim konularını anlamanıza yardımcı olur. Konular ve sosyal medya içinde postaları hacmi yüksek olan alışkanlıklarınızı bunun oluşturan eğilim konulardır. Olarak da adlandırılır düşünceleri analiz *fikir araştırma*, sosyal medya analizi araçları toodetermine alışkanlıklarınızı ürün, fikir ve benzeri doğru kullanır. 

Gerçek zamanlı Twitter eğilim analizi hello diyez abonelik modeli toolisten toospecific anahtar sözcükler (diyez etiketlerini) sağladığından harika bir analiz Aracı'nın bir örnektir ve akış hello düşünceleri analizini geliştirin.

## <a name="scenario-social-media-sentiment-analysis-in-real-time"></a>Senaryo: Sosyal medya düşünceleri gerçek zamanlı analiz

Bir haber medya Web sitesi olan bir şirket rakiplere üzerinde bir avantaj hemen ilgili tooits okuyucular olduğu site içeriğin bulunduğu tarafından sağlamasını ilgileniyor. Hello şirket Twitter veri analizini gerçek zamanlı düşünceleri yaparak ilgili tooreaders olan konularda sosyal medya çözümlemesini kullanır.

Twitter'da, gerçek zamanlı tooidentify oluşturan eğilim konuları şirket gereksinimlerini gerçek zamanlı analiz hello tweet birim ve önemli konular için düşünceleri hakkında hello. Diğer bir deyişle, hello gerek akış bu sosyal medya üzerinde temel alan bir düşünceleri analiz analytics altyapısıdır.

## <a name="prerequisites"></a>Ön koşullar
Bu öğreticide, tooTwitter bağlanır ve (hangi ayarlayabileceğiniz) belirli diyez etiketlerini sahip tweet'leri benzeyen bir istemci uygulaması kullanın. Sırayla toorun uygulama hello ve analiz hello Azure akış analizi kullanarak tweet'leri hello şunlara sahip olmanız gerekir:

* Bir Azure aboneliği
* Bir Twitter hesabı 
* Bir Twitter uygulama ve hello [OAuth erişim belirtecinin](https://dev.twitter.com/oauth/overview/application-owner-access-tokens) bu uygulama için. Üst düzey hakkında yönergeler sağlıyoruz toocreate Twitter uygulamayı daha sonra.
* Merhaba Twitter okur Merhaba TwitterWPFClient uygulaması akış. tooget bu uygulama, yükleme hello [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) dosya Github'dan ve bilgisayarınızdaki bir klasöre hello paketin sıkıştırmasını. Toosee hello kaynak kodu istediğiniz ve bir hata ayıklayıcıda Merhaba uygulaması Çalıştır hello kaynak kodundan alabilir [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator). 

## <a name="create-an-event-hub-for-streaming-analytics-input"></a>Bir event hub'akış analizi girişi için oluşturma

Merhaba örnek uygulaması olaylar oluşturur ve bunları tooan Azure olay hub'ı iter. Azure event hubs'a akış analizi için olay alım hello tercih edilen yöntemdir. Daha fazla bilgi için bkz: Merhaba [Azure Event Hubs belgelerine](../event-hubs/event-hubs-what-is-event-hubs.md).


### <a name="create-an-event-hub-namespace-and-event-hub"></a>Bir olay hub'ad alanı ve olay hub'ı Oluştur
Bu yordam, önce bir olay hub'ad alanı oluşturun ve ardından bir olay hub'ı toothat ad alanı ekleyin. Olay hub'ı ad alanları kullanılır toologically grubunun ilişkili olay bus örnekleri. 

1. Oturum toohello Azure portal ve tıklatın **yeni** > **nesnelerin interneti** > **olay hub'ı**. 

2. Merhaba, **ad alanı oluşturma** dikey penceresinde gibi bir ad alanı adı girin `<yourname>-socialtwitter-eh-ns`. Merhaba ad alanı için herhangi bir ad kullanabilirsiniz, ancak hello adı geçerli bir URL olmalıdır ve Azure arasında benzersiz olması gerekir. 
    
3. Bir aboneliği seçin ve oluşturmak veya bir kaynak grubu seçin ve ardından **oluşturma**. 

    ![Bir olay hub'ad alanı oluşturma](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub-namespace.png)
 
4. Merhaba ad alanı dağıtmayı bitirdiğinde hello olay hub'ad alanı, Azure kaynak listesinde bulun. 

5. Merhaba yeni ad alanına tıklayın ve hello ad alanı dikey penceresinde tıklayın  **+ &nbsp;olay hub'ı**. 

    ![Yeni bir olay hub'ı oluşturmak için hello Event Hub'ı Ekle düğmesi ](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub-button.png)    
 
6. Ad hello yeni olay hub'ı `socialtwitter-eh`. Farklı bir ad kullanabilirsiniz. Bunu yaparsanız, hello adı daha sonra gerektiğinden, not edin. Merhaba olay hub'ı için diğer seçenekleri tooset gerekmez.

    ![Yeni bir olay hub'ı oluşturmak için dikey penceresi](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub.png)
 
7. **Oluştur**'a tıklayın.


### <a name="grant-access-toohello-event-hub"></a>GRANT erişim toohello olay hub'ı

Bir işlem tooan event hub'ı veri göndermeden önce hello olay hub'ı, uygun erişim veren bir ilke olması gerekir. Merhaba erişim ilkesi yetkilendirme bilgilerini içeren bir bağlantı dizesi oluşturur.

1.  Merhaba olay ad alanı dikey penceresinde tıklayın **olay hub'ları** ve ardından yeni olay hub'ınızı hello adına tıklayın.

2.  Merhaba olay hub dikey penceresinde tıklayın **paylaşılan erişim ilkeleri** ve ardından  **+ &nbsp;Ekle**.

    >[!NOTE]
    >Merhaba olay hub değil hello olay hub'ı ad çalıştığınız emin olun.

3.  Adlı ilke Ekle `socialtwitter-access` ve **talep**seçin **Yönet**.

    ![Yeni bir olay hub'ı erişim ilkesi oluşturmak için dikey penceresi](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-shared-access-policy-manage.png)
 
4.  **Oluştur**'a tıklayın.

5.  Hello İlkesi dağıtıldıktan sonra paylaşılan erişim ilkeleri hello listesinde tıklayın.

6.  Etiketli Bul hello kutusunu **bağlantı dize birincil anahtarı** ve hello Kopyala düğmesine bir sonraki toohello bağlantı dizesi'ı tıklatın. 
    
    ![Merhaba erişim ilkesinden Hello birincil bağlantı dizesi anahtarını kopyalama](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-shared-access-policy-copy-connection-string.png)
 
7.  Merhaba bağlantı dizesi, bir metin düzenleyicisine yapıştırın. Bazı küçük düzenlemeler tooit yaptıktan sonra hello için sonraki bölümde, bu bağlantı dizesi gerekir.

    Merhaba bağlantı dizesi şu şekildedir:

        Endpoint=sb://YOURNAME-socialtwitter-eh-ns.servicebus.windows.net/;SharedAccessKeyName=socialtwitter-access;SharedAccessKey=Gw2NFZw6r...FxKbXaC2op6a0ZsPkI=;EntityPath=socialtwitter-eh

    Merhaba bağlantı dizesi noktalı virgülle ayırarak, birden çok anahtar-değer çiftleri içerdiğine dikkat edin: `Endpoint`, `SharedAccessKeyName`, `SharedAccessKey`, ve `EntityPath`.  

    > [!NOTE]
    > Güvenlik için hello bağlantı dizesi hello örnekte bölümleri kaldırıldı.

8.  Merhaba Metin Düzenleyicisi'nde hello kaldırmak `EntityPath` hello bağlantı dizesinden çifti (yakalanması tooremove hello noktalı unutmayın). İşiniz bittiğinde, hello bağlantı dizesi şu şekildedir:

        Endpoint=sb://YOURNAME-socialtwitter-eh-ns.servicebus.windows.net/;SharedAccessKeyName=socialtwitter-access;SharedAccessKey=Gw2NFZw6r...FxKbXaC2op6a0ZsPkI=


## <a name="configure-and-start-hello-twitter-client-application"></a>Yapılandırma ve hello Twitter istemci uygulamasını başlatın
Merhaba istemci uygulaması tweet olayları doğrudan Twitter'dan alır. İçinde toodo bunu sipariş, izni toocall hello akış API'leri Twitter gerekiyor. izni, uygulamanın benzersiz kimlik bilgilerini (örneğin, OAuth belirteci) oluşturur Twitter oluşturduğunuz tooconfigure. API çağrıları yaptığında, daha sonra bu kimlik bilgileri hello istemci uygulaması toouse yapılandırabilirsiniz. 

### <a name="create-a-twitter-application"></a>Bir Twitter uygulaması oluşturma
Bu öğretici için kullanabileceğiniz bir Twitter uygulaması zaten yoksa bir tane oluşturabilirsiniz. Zaten bir Twitter hesabı olması gerekir.

> [!NOTE]
> bir uygulama oluşturma ve hello anahtarları, gizli ve belirteç alma Twitter tam işleminde Hello değişebilir. Bu yönergeleri hello Twitter sitesinde bakın eşleşmiyorsa, toohello Twitter Geliştirici belgelerinize bakın.

1. Toohello Git [Twitter Uygulama Yönetimi sayfasında](https://apps.twitter.com/). 

2. Yeni bir uygulama oluşturun. 

    * Merhaba Web sitesi URL'si için geçerli bir URL belirtin. Canlı site toobe yok. (Yalnızca belirtemezsiniz `localhost`.)
    * Merhaba geri çağırma alanı boş bırakın. Bu öğretici için kullandığınız Merhaba istemci uygulaması geri aramalar gerektirmez.

    ![Twitter içinde bir uygulama oluşturma](./media/stream-analytics-twitter-sentiment-analysis-trends/create-twitter-application.png)

3. İsteğe bağlı olarak, yalnızca tooread hello uygulamanın izinleri değiştirin.

4. Merhaba uygulaması oluşturulduğunda toohello Git **anahtarları ve erişim belirteçleri** sayfası.

5. Merhaba düğmesi toogenerate bir erişim belirteci ve erişim belirteci gizli anahtarı'ı tıklatın.

Hello sonraki yordamda gerektiğinden bu bilgiler faydalı, tutun.

>[!NOTE]
>Merhaba anahtarları ve gizli anahtarları hello Twitter uygulama için erişim tooyour Twitter hesabı sağlayın. Bu bilgileri gizli olarak değerlendirir, Twitter parolanızı olduğu gibi aynı hello. Örneğin, bir uygulama tooothers size bu bilgileri katıştırma. 


### <a name="configure-hello-client-application"></a>Merhaba istemci uygulaması yapılandırın
TooTwitter verileri kullanarak bağlanan bir istemci uygulaması oluşturduk [Twitter'ın akış API'leri](https://dev.twitter.com/streaming/overview) toocollect tweet olaylar hakkında konular belirli bir dizi. Merhaba uygulamanın kullandığı hello [Sentiment140](http://help.sentiment140.com/) düşünceleri değeri tooeach tweet aşağıdaki hello atar açık kaynak aracı:

* 0 negatif =
* 2 = neutral =
* 4 pozitif =

Merhaba tweet olayları düşünceleri değeri atandıktan sonra bunlar daha önce oluşturduğunuz toohello olay hub'ı atılır.

Merhaba uygulamayı çalıştırmadan önce hello Twitter anahtarları ve hello olay hub bağlantı dizesine gibi belirli bilgileri gerektirir. Bu yolla hello yapılandırma bilgileri sağlayabilir:

* Merhaba uygulamayı çalıştırın ve ardından hello uygulamanın UI tooenter hello anahtarları, gizli ve bağlantı dizesini kullanın. Bunu yaparsanız, hello yapılandırma bilgilerini geçerli oturumunuz için kullanılır, ancak bunu kaydedilmez.
* Merhaba uygulamanın .config dosyasına ve kümesi hello değerlerini düzenleyin. Bu yaklaşım hello yapılandırma bilgilerini devam ederse, ancak aynı zamanda bu olası hassas bilgiler düz metin, bilgisayarınızda depolanır gelir.

Merhaba aşağıdaki yordamı her iki yaklaşımın belgeler. 

1. Karşıdan yükleyip hello sıkıştırması açılmış olduğundan emin olun [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) hello önkoşullarını listelendiği gibi uygulama.

2. tooset hello değerleri çalışma zamanında (ve yalnızca hello geçerli oturum için), çalıştırmak hello `TwitterWPFClient.exe` uygulama. Merhaba uygulaması istediğinde, hello aşağıdaki değerleri girin:

    * Merhaba Twitter tüketici anahtarı (API anahtarı).
    * Merhaba Twitter tüketici gizli anahtarı (API gizli).
    * Merhaba Twitter erişim belirteci.
    * Merhaba Twitter erişim belirteci gizli anahtarı.
    * daha önce kaydettiğiniz hello bağlantı dizesi bilgileri. Merhaba kaldırdığınız hello bağlantı dizesini kullandığınızdan emin olun `EntityPath` gelen anahtar-değer çifti.
    * toodetermine düşünceleri için istediğiniz hello Twitter anahtar sözcükler.

   ![Çalıştıran, örtülü ayarları gösteren TwitterWpfClient uygulama](./media/stream-analytics-twitter-sentiment-analysis-trends/wpfclientlines.png)

3. tooset hello değerleri kalıcı olarak, bir metin düzenleyicisi tooopen hello TwitterWpfClient.exe.config dosyasını kullanın. Merhaba sonra `<appSettings>` öğesi, bunu yapın:

    * Ayarlama `oauth_consumer_key` toohello Twitter tüketici anahtarı (API anahtarı). 
    * Ayarlama `oauth_consumer_secret` toohello Twitter tüketici gizli anahtarı (API gizli).
    * Ayarlama `oauth_token` toohello Twitter erişim belirteci.
    * Ayarlama `oauth_token_secret` toohello Twitter erişim belirteci gizli anahtarı.

    Merhaba devamındaki `<appSettings>` öğesi, bu değişiklikleri yapın:

    * Ayarlama `EventHubName` toohello olay hub'ı adı (diğer bir deyişle, hello varlık yolu toohello değeri).
    * Ayarlama `EventHubNameConnectionString` toohello bağlantı dizesi. Merhaba kaldırdığınız hello bağlantı dizesini kullandığınızdan emin olun `EntityPath` gelen anahtar-değer çifti.

    Merhaba `<appSettings>` bölümü aşağıdaki örneğine hello gibi görünüyor. (Daha anlaşılır olması ve güvenlik için biz bazı satırlar Sarmalanan ve bazı karakterler kaldırılmış.)

    ![Merhaba Twitter anahtarları ve gizli anahtarları ve hello olay hub'ı bağlantı dizesi bilgilerini gösteren bir metin düzenleyicisinde TwitterWpfClient uygulama yapılandırma dosyası](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-tiwtter-app-config.png)
 
4. Merhaba uygulaması zaten başlatmadıysanız TwitterWpfClient.exe Şimdi Çalıştır. 

5. Merhaba Yeşil Başlat düğmesi toocollect sosyal düşünceleri'ı tıklatın. Merhaba Tweet olaylara bakın **CreatedAt**, **konu**, ve **SentimentScore** tooyour olay hub'ı gönderilen değerler.

    ![Tweet'leri listesini gösteren TwitterWpfClient uygulaması çalışıyor](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-twitter-app-listing.png)

    >[!NOTE]
    >Hataları görmek ve hello alt kısmında hello penceresinde görüntülenen tweet'leri akışı görmüyorsanız, hello anahtarları ve gizli anahtarları denetleyin. Ayrıca hello bağlantı dizesini kontrol edin (Merhaba içermediğinden emin olun `EntityPath` anahtar ve değer.)


## <a name="create-a-stream-analytics-job"></a>Akış Analizi işi oluşturma

Twitter gelen gerçek zamanlı akış tweet olaylarını, akış analizi işi tooanalyze bu olayları gerçek zamanlı olarak ayarlayabilirsiniz.

1. Hello Azure portal'ı tıklatın **yeni** > **nesnelerin interneti** > **Stream Analytics işi**.

2. Ad hello iş `socialtwitter-sa-job` ve abonelik, kaynak grubunu ve konumu belirtin.

    Bir fikir tooplace hello iş ve hello event hub'ında hello olan en iyi performans ve bunu için aynı bölge bölgeler arasında tootransfer veri ödemeniz gerekmez.

    ![Yeni bir Stream Analytics işi oluşturma](./media/stream-analytics-twitter-sentiment-analysis-trends/newjob.png)

3. **Oluştur**'a tıklayın.

    Merhaba iş oluşturulur ve hello portal iş ayrıntılarını görüntüler.


## <a name="specify-hello-job-input"></a>Merhaba iş giriş belirtin

1. Stream Analytics işinizde altında **iş topoloji** hello iş dikey penceresinde hello ortadaki tıklatın **girişleri**. 

2. Merhaba, **girişleri** dikey penceresinde tıklatın  **+ &nbsp;Ekle** ve ardından hello dikey şu değerlerle doldurun:

    * **Giriş diğer adı**: hello adını kullan `TwitterStream`. Farklı bir ad kullanırsanız, daha sonra gerektiğinden, not edin.
    * **Kaynak türünü**: seçin **veri akışı**.
    * **Kaynak**: seçin **olay hub'ı**.
    * **Alma seçeneği**: seçin **geçerli aboneliğe ilişkin kullanım olay hub'ı**. 
    * **Hizmet veri yolu ad alanı**: daha önce oluşturduğunuz hello olay hub'ad alanı seçin (`<yourname>-socialtwitter-eh-ns`).
    * **Olay hub'ı**: daha önce oluşturduğunuz Select hello olay hub'ı (`socialtwitter-eh`).
    * **Olay hub'ı ilke adı**: daha önce oluşturduğunuz hello erişim ilkesi seçin (`socialtwitter-access`).

    ![Akış analizi işi için yeni giriş oluşturma](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-twitter-new-input.png)

3. **Oluştur**'a tıklayın.


## <a name="specify-hello-job-query"></a>Merhaba iş sorgusu belirtin

Akış analizi dönüşümleri açıklayan bir basit ve bildirim temelli sorgu modelini destekler. toolearn hello dili hakkında daha fazla bilgi görmek hello [Azure Stream Analytics sorgu dili başvurusu](https://msdn.microsoft.com/library/azure/dn834998.aspx).  Bu öğretici, yazar ve birkaç sorgu Twitter verileri üzerinde test yardımcı olur.

kullanabileceğiniz belirtilenlerden konular arasındaki toocompare hello sayısı, bir [atlayan pencere](https://msdn.microsoft.com/library/azure/dn835055.aspx) tooget hello beş saniyede belirtilenlerden konusuna göre sayısı.

1. Kapat hello **girişleri** yapmadıysanız dikey.

2. Merhaba iş dikey penceresinde hello tıklayın **sorgu** kutusu. Azure hello girişleri listeler ve toohello çıktı gönderilmiş gibi hello proje için yapılandırılmış ve olanak sağlayan bir sorgu oluşturmanıza olanak tanır çıkışları hello Giriş akışı Dönüştür.

3. Bu hello TwitterWpfClient uygulama çalıştığından emin olun. 

3. Merhaba, **sorgu** dikey penceresinde hello nokta sonraki toohello tıklatın `TwitterStream` girin ve ardından **örnek giriş verilerinden**.

    ![Menü seçeneklerini toouse için örnek veri hello akış analizi işi girişi, verilerle"Seçili örnek Giriş"](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-sample-data-from-input.png)

    Bu akış ne kadar süreyle tooread hello girişi bakımından tanımlanmış ne kadar örnek veri tooget belirtmenize olanak sağlar. bir dikey pencere açılır.

4. Ayarlama **dakika** too3 ve ardından **Tamam**. 
    
    !["3 Seçili dakika ile" Merhaba Giriş akışı örnekleme seçenekleri.](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-input-create-sample-data.png)

    Azure hello Giriş akışı verilerden 3 dakika eşitleyeceğini örnekleri ve hello örnek verileri hazır olduğunda size bildirir. (Bu kısa biraz uzun sürebilir.) 

    Merhaba örnek verileri geçici olarak depolanır ve açmak hello sorgu penceresi açıkken kullanılabilir. Hello sorgu penceresini kapattığınızda, hello örnek veriler atılır ve yeni bir örnek veri kümesi toocreate sahip. 

5. Merhaba Kod Düzenleyicisi toohello aşağıdaki Hello sorguyu değiştirin:

    ```
    SELECT System.Timestamp as Time, Topic, COUNT(*)
    FROM TwitterStream TIMESTAMP BY CreatedAt
    GROUP BY TUMBLINGWINDOW(s, 5), Topic
    ```

    Varsa kullanmadı `TwitterStream` hello giriş için diğer ad hello, diğer adınızı alternatif `TwitterStream` hello sorgu.  

    Bu sorgu hello kullanan **TIMESTAMP BY** anahtar sözcüğü toospecify hello yükü toobe hello zamana bağlı hesaplamanın kullanılan bir zaman damgası alanı. Bu alan belirtilmezse, hello Pencereleme işlemi her olay hello olay hub'ına gelen hello saati kullanılarak gerçekleştirilir. Merhaba "geliş saati vs uygulama zamanı" bölümünde daha fazla bilgi edinin [Stream Analytics sorgu başvurusu](https://msdn.microsoft.com/library/azure/dn834998.aspx).

    Ayrıca bu sorgu hello kullanarak bir zaman damgası her penceresinde hello sonunun erişir **System.Timestamp** özelliği.

5. Tıklatın **Test**. Merhaba sorgu, örneklenen hello veri karşı çalışır.
    
6. **Kaydet** düğmesine tıklayın. Bu hello sorgu hello akış analizi işi bir parçası olarak kaydeder. (Merhaba örnek verileri kaydetmez.)


## <a name="experiment-using-different-fields-from-hello-stream"></a>Deneme hello akışından farklı alanları kullanma 

Hello aşağıdaki tablo veri akışı JSON hello parçası olan hello alanları listeler. Ücretsiz tooexperiment hello sorgu Düzenleyicisi'nde eşitleyerek.

|JSON özelliği | Tanım|
|--- | ---|
|CreatedAt | Başlangıç saati, hello tweet oluşturuldu|
|Konu | Merhaba eşleşen hello konu belirtilen anahtar sözcüğü|
|SentimentScore | Merhaba düşünceleri puan Sentiment140|
|Yazar | Merhaba tweet gönderilen hello Twitter tanıtıcısı|
|Metin | Merhaba tam hello tweet gövdesi|


## <a name="create-an-output-sink"></a>Çıkış havuzu oluşturma

Şimdi bir olay akışı, bir olay hub'ı giriş tooingest olayları ve sorgu tooperform dönüştürme hello akış üzerinden tanımladınız. Merhaba son toodefine hello işi için çıkış havuzu adımdır.  

Bu öğreticide, bir araya getirilir hello tweet olayları hello iş sorgu tooAzure Blob Depolama yazma.  SQL Database, Azure Table storage, sonuçları tooAzure olay hub'ları da gönderebilir veya Power BI bağlı olarak uygulamanız gerekir.

## <a name="specify-hello-job-output"></a>Merhaba iş çıktısı belirtin

1. Merhaba, **iş topoloji** bölümünde, hello tıklatın **çıkış** kutusu. 

2. Merhaba, **çıkışları** dikey penceresinde tıklatın  **+ &nbsp;Ekle** ve ardından hello dikey şu değerlerle doldurun:

    * **Çıkış diğer adları**: hello adını kullan `TwitterStream-Output`. 
    * **Havuz**: seçin **Blob storage**.
    * **İçe aktarma seçenekleri**: seçin **blob storage'ı geçerli aboneliğe ilişkin kullanma**.
    * **Depolama hesabı**. Seçin **yeni bir depolama hesabı oluşturun.**
    * **Depolama hesabı** (ikinci kutusu). Girin `YOURNAMEsa`, burada `YOURNAME` adınızı veya başka bir benzersiz bir dize. Merhaba adı yalnızca küçük harfler ve sayılar kullanabilirsiniz ve Azure arasında benzersiz olması gerekir. 
    * **Kapsayıcı**. Girin `socialtwitter`.
    Merhaba depolama hesabı adı ve kapsayıcı adı kullanılan birlikte tooprovide bu gibi hello blob depolama için bir URI şunlardır: 

    `http://YOURNAMEsa.blob.core.windows.net/socialtwitter/...`
    
    ![Stream Analytics işi için "Yeni çıkış" dikey](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-output-blob-storage.png)
    
4. **Oluştur**'a tıklayın. 

    Azure hello depolama hesabı oluşturur ve bir anahtarı otomatik olarak oluşturur. 

5. Kapat hello **çıkışları** dikey. 


## <a name="start-hello-job"></a>Merhaba işi Başlat

İş Girişi, sorgu ve çıktı belirtilir. Hazır toostart hello Stream Analytics işi var.

1. Bu hello TwitterWpfClient uygulama çalıştığından emin olun. 

2. Merhaba iş dikey penceresinde tıklayın **Başlat**.

    ![Merhaba Stream Analytics işi Başlat](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-sa-job-start-output.png)

3. Merhaba, **başlangıç işi** dikey penceresinde için **iş çıktısı başlangıç zamanı**seçin **şimdi** ve ardından **Başlat**. 

    ![Dikey penceresinde hello Stream Analytics işi "işlemini Başlat"](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-sa-job-start-job-blade.png)

    Azure sizi uyarır hello iş başlatıldı ve hello iş dikey penceresinde hello durumu olarak görüntülendiğinde **çalıştıran**.

    ![İşi çalıştırma](./media/stream-analytics-twitter-sentiment-analysis-trends/jobrunning.png)

## <a name="view-output-for-sentiment-analysis"></a>Görünüm çıktı düşünceleri analiz için

İşinizi çalışmaya başladıktan ve hello gerçek zamanlı Twitter akışı işleme sonra hello çıktı düşünceleri analiz için görüntüleyebilirsiniz.

Gibi bir araç kullanabilirsiniz [Azure Storage Gezgini](https://http://storageexplorer.com/) veya [Azure Gezgini](http://www.cerebrata.com/products/azure-explorer/introduction) işinizi çıktı gerçek zamanlı olarak tooview. Buradan, kullandığınız [Power BI](https://powerbi.com/) tooextend, uygulama tooinclude özelleştirilmiş bir pano gibi bir ekran aşağıdaki hello gösterilen hello:

![Power BI](./media/stream-analytics-twitter-sentiment-analysis-trends/power-bi.png)


## <a name="create-another-query-tooidentify-trending-topics"></a>Tooidentify oluşturan eğilim konuları başka bir sorgu oluşturun

Toounderstand Twitter düşünceleri kullanabileceğiniz başka bir sorguya dayalı bir [kayan pencere](https://msdn.microsoft.com/library/azure/dn835051.aspx). tooidentify oluşturan eğilim konular, belirtilen sürede belirtilenlerden için eşik değer arası konuları arayın.

Bu öğreticinin Hello amaçları doğrultusunda, 20 katından fazla hello son 5 saniye açıklanan konuları denetleyin.

1. Merhaba iş dikey penceresinde tıklayın **durdurmak** toostop hello işi. 

2. Merhaba, **iş topoloji** bölümünde, hello tıklatın **sorgu** kutusu. 

3. Merhaba sorgu toohello aşağıdakileri değiştirin:

    ```    
    SELECT System.Timestamp as Time, Topic, COUNT(*) as Mentions
    FROM TwitterStream TIMESTAMP BY CreatedAt
    GROUP BY SLIDINGWINDOW(s, 5), topic
    HAVING COUNT(*) > 20
    ```

4. **Kaydet** düğmesine tıklayın.

5. Bu hello TwitterWpfClient uygulama çalıştığından emin olun. 

6. Tıklatın **Başlat** hello yeni bir sorgu kullanarak toorestart hello işi.


## <a name="get-support"></a>Destek alın
Daha fazla yardım için deneyin bizim [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Sonraki adımlar
* [Giriş tooAzure akış analizi](stream-analytics-introduction.md)
* [Azure Akış Analizi'ni kullanmaya başlama](stream-analytics-real-time-fraud-detection.md)
* [Azure Akış Analizi işlerini ölçeklendirme](stream-analytics-scale-jobs.md)
* [Azure Akış Analizi Sorgu Dili Başvurusu](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Akış Analizi Yönetimi REST API'si Başvurusu](https://msdn.microsoft.com/library/azure/dn835031.aspx)
