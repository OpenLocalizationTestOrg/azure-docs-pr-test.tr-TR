# <a name="get-started-using-azure-stream-analytics-real-time-fraud-detection"></a>Azure Stream Analytics'i kullanmaya başlama: Gerçek zamanlı sahtekarlık algılama

Bu öğretici nasıl bir uçtan uca çizimi sağlar toouse Azure Stream Analytics. Aşağıdakileri nasıl yapacağınızı öğrenirsiniz: 

* Getir olayları Azure Event Hubs bir örneğine akış. Bu öğreticide, cep telefonu meta veri kayıtlarını akışı benzetim sağladığımız bir uygulaması kullanacaksınız.

* Bilgi toplama veya desenlerini bakarak SQL benzeri Stream Analytics sorgu tootransform veri yazma. Nasıl toouse sorgu tooexamine gelen akış hello ve sahte olabilir çağrıları için Ara görürsünüz.

* İlgili ek bilgileri analiz hello sonuçları tooan çıkış havuzu (Depolama) gönderin. Bu durumda, hello şüpheli çağrısı veri tooAzure Blob Depolama göndereceğiz.

Bu öğreticide, telefon araması verilerine dayalı gerçek zamanlı sahtekarlık algılama hello örneği kullanın. Ancak biz göstermeye hello teknik sahtekarlık algılama, kredi kartı sahtekarlık veya kimlik hırsızlığı gibi diğer türleri için de uygundur. 

## <a name="scenario-telecommunications-and-sim-fraud-detection-in-real-time"></a>Senaryo: Gerçek zamanlı telekomünikasyon ve SIM sahtekarlık algılama

Telekomünikasyon şirket, fazla miktarda verinin gelen çağrıları için sahiptir. Merhaba şirket, böylece müşteriler bildir veya hizmet için belirli sayıda kapatın toodetect sahte gerçek zamanlı olarak çağırır ister. SIM sahtekarlık bir tür içerir hello gelen birden çok çağrıları hello geçici aynı kimliğe aynı zaman ancak coğrafi olarak farklı konumlarda. toodetect sahtekarlık, bu tür hello şirket gereksinimlerini tooexamine gelen telefon kaydeder ve belirli kalıpları aramak — bu durumda, hello yapılan aramalar için aynı anda farklı ülkelerde. Bu kategoriye herhangi bir telefon kayıt toostorage sonraki çözümleme için yazılmıştır.

## <a name="prerequisites"></a>Ön koşullar

Bu öğreticide, örnek telefon araması meta verilerini oluşturur bir istemci uygulaması kullanarak, telefon araması veri benzetimi. Bazı uygulama hello hello kayıtları sahte çağrıları görünümlü üretir. 

Başlamadan önce hello aşağıdaki sahip olduğunuzdan emin olun:

* Bir Azure hesabı.
* Merhaba çağırma olayı Oluşturucu uygulama. Bu hello indirerek elde [TelcoGenerator.zip dosya](http://download.microsoft.com/download/8/B/D/8BD50991-8D54-4F59-AB83-3354B69C8A7E/TelcoGenerator.zip) hello Microsoft Download Center gelen. Bu paket, bilgisayarınızdaki bir klasöre ayıklayın. Toosee hello kaynak kod ve çalışma hello uygulamada bir hata ayıklayıcısı isterseniz, hello uygulama kaynak kodundan alabilirsiniz [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator). 

    >[!NOTE]
    >Windows hello yüklediğiniz .zip dosyasını engelleyebilir. Unzip olamaz, hello dosyasını sağ tıklatın ve seçin **özellikleri**. Merhaba görürseniz, "Bu dosya başka bir bilgisayardan gelen ve olması engellenen toohelp korumak bu bilgisayar" iletisi, select hello **Engellemeyi Kaldır** seçeneğini ve ardından **Uygula**.

Merhaba akış analizi işi tooexamine hello sonuçlarını istiyorsanız, Azure Blob Storage kapsayıcısının hello içeriğini görüntülemek için ayrıca bir aracı gerekir. Visual Studio kullanırsanız, kullanabileceğiniz [Visual Studio için Azure Araçları](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-resources-server-explorer-browse-manage) veya [Visual Studio Cloud Explorer](https://docs.microsoft.com/en-us/azure/vs-azure-tools-resources-managing-with-cloud-explorer). Alternatif olarak, tek başına araçlarla yükleyebilirsiniz [Azure Storage Gezgini](http://storageexplorer.com/) veya [Azure Gezgini](http://www.cerebrata.com/products/azure-explorer/introduction). 

## <a name="create-an-azure-event-hubs-tooingest-events"></a>Azure olay hub'ları tooingest olaylar oluşturma

tooanalyze bir veri akışı, *alma* Azure içine. Tipik bir şekilde tooingest toouse verilerdir [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md), olanak sağlayan, saniye başına milyonlarca olayı alma ve sonra işlem ve hello olay bilgileri depolar. Bu öğretici için bir olay hub'ı oluşturabilir ve ardından hello çağırma olayı Oluşturucu uygulama gönderme çağrısı veri toothat olay hub'ı sağlayabilirsiniz. Event hubs hakkında daha fazla bilgi için bkz: Merhaba [Azure Service Bus belgelerine](https://docs.microsoft.com/en-us/azure/service-bus/).

>[!NOTE]
>Bu yordamı daha ayrıntılı bir sürümü için bkz: [bir olay hub'ları ad alanı oluşturma ve bir olay hub'ı kullanarak Azure portalında hello](../event-hubs/event-hubs-create.md). 

### <a name="create-a-namespace-and-event-hub"></a>Bir ad alanı ve olay hub'ı Oluştur
Bu yordam, önce bir olay hub'ad alanı oluşturun ve ardından bir olay hub'ı toothat namepsace ekleyin. Olay hub'ı ad alanları kullanılır toologically grubunun ilişkili olay bus örnekleri. 

1. Azure portal hello oturum ve'ı tıklatın **yeni** > **nesnelerin interneti** > **olay hub'ı**. 

2. Merhaba, **ad alanı oluşturma** dikey penceresinde gibi bir ad alanı adı girin `<yourname>-eh-ns-demo`. Merhaba ad alanı için herhangi bir ad kullanabilirsiniz, ancak hello adı geçerli bir URL olmalıdır ve Azure arasında benzersiz olması gerekir. 
    
3. Bir aboneliği seçin ve oluşturmak veya bir kaynak grubu seçin ve ardından **oluşturma**. 

    ![Bir olay hub'ad alanı oluşturma](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-eventhub-namespace-new-portal.png)
 
4. Merhaba ad alanı dağıtmayı bitirdiğinde hello olay hub'ad alanı, Azure kaynak listesinde bulun. 

5. Merhaba yeni ad alanına tıklayın ve hello ad alanı dikey penceresinde tıklayın  **+ &nbsp;olay hub'ı**. 

    ![Yeni bir olay hub'ı oluşturmak için hello Event Hub'ı Ekle düğmesi ](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-eventhub-button-new-portal.png)    
 
6. Ad hello yeni olay hub'ı `sa-eh-frauddetection-demo`. Farklı bir ad kullanabilirsiniz. Bunu yaparsanız, hello adı daha sonra gerektiğinden, not edin. Tooset diğer seçenekleri hello olay hub'ı şimdi gerekmez.

    ![Yeni bir olay hub'ı oluşturmak için dikey penceresi](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-eventhub-new-portal.png)
    
 
7. **Oluştur**'a tıklayın.
### <a name="grant-access-toohello-event-hub-and-get-a-connection-string"></a>Toohello event hub'ı erişim vermek ve bir bağlantı dizesi alma

Bir işlem tooan event hub'ı veri göndermeden önce hello olay hub'ı, uygun erişim veren bir ilke olması gerekir. Merhaba erişim ilkesi yetkilendirme bilgilerini içeren bir bağlantı dizesi oluşturur.

1.  Merhaba olay ad alanı dikey penceresinde tıklayın **olay hub'ları** ve ardından yeni olay hub'ınızı hello adına tıklayın.

2.  Merhaba olay hub dikey penceresinde tıklayın **paylaşılan erişim ilkeleri** ve ardından  **+ &nbsp;Ekle**.

    >[!NOTE]
    >Merhaba olay hub değil hello olay hub'ı ad çalıştığınız emin olun.

3.  Adlı ilke Ekle `sa-policy-manage-demo` ve **talep**seçin **Yönet**.

    ![Yeni bir olay hub'ı erişim ilkesi oluşturmak için dikey penceresi](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-shared-access-policy-manage-new-portal.png)
 
4.  **Oluştur**'a tıklayın.

5.  Hello İlkesi dağıtıldıktan sonra paylaşılan erişim ilkeleri hello listesinde tıklayın.

6.  Etiketli Bul hello kutusunu **bağlantı dize birincil anahtarı** ve hello Kopyala düğmesine bir sonraki toohello bağlantı dizesi'ı tıklatın. 
    
    ![Merhaba erişim ilkesinden Hello birincil bağlantı dizesi anahtarını kopyalama](./media/stream-analytics-real-time-fraud-detection/stream-analytics-shared-access-policy-copy-connection-string-new-portal.png)
 
7.  Merhaba bağlantı dizesi, bir metin düzenleyicisine yapıştırın. Bazı küçük düzenlemeler tooit yaptıktan sonra hello için sonraki bölümde, bu bağlantı dizesi gerekir.

    Merhaba bağlantı dizesi şu şekildedir:

        Endpoint=sb://YOURNAME-eh-ns-demo.servicebus.windows.net/;SharedAccessKeyName=sa-policy-manage-demo;SharedAccessKey=Gw2NFZwU1Di+rxA2T+6hJYAtFExKRXaC2oSQa0ZsPkI=;EntityPath=sa-eh-frauddetection-demo

    Merhaba bağlantı dizesi noktalı virgülle ayırarak, birden çok anahtar-değer çiftleri içerdiğine dikkat edin: `Endpoint`, `SharedAccessKeyName`, `SharedAccessKey`, ve `EntityPath`.  

## <a name="configure-and-start-hello-event-generator-application"></a>Yapılandırma ve hello olay Oluşturucu uygulamasını başlatın

Merhaba TelcoGenerator uygulama başlamadan önce yeni oluşturduğunuz çağrısı kayıtları toohello olay hub'ı göndereceğiz böylece, yapılandırın.

### <a name="configure-hello-telcogeneratorapp"></a>Merhaba TelcoGeneratorapp yapılandırın

1.  Merhaba bağlantı dizesi kopyaladığınız hello Düzenleyicisi'nde hello Not `EntityPath` değer ve Kaldır'ı hello `EntityPath` (unutmayın yakalanması tooremove hello noktalı virgül) çifti. 

2.  Burada, hello TelcoGenerator.zip dosyasının sıkıştırması açılmış hello klasöründe hello telcodatagen.exe.config dosyasına bir düzenleyicide açın. (Birden fazla .config dosyası, bu nedenle hello sağa bir açık olduğundan emin olun.)

3.  Merhaba, `<appSettings>` öğesi, bunu yapın:

    * Merhaba hello değerini ayarlamak `EventHubName` anahtar toohello olay hub'ı adı (diğer bir deyişle, hello varlık yolu toohello değeri).
    * Merhaba hello değerini ayarlamak `Microsoft.ServiceBus.ConnectionString` anahtar toohello bağlantı dizesi. 

    Merhaba `<appSettings>` bölümü aşağıdaki örneğine hello gibi görünür. (Daha anlaşılır olması, biz hello satıra gibi ve bazı karakterler hello yetkilendirme belirtecinden kaldırıldı.)

    ![Merhaba, olay hub adını ve bağlantı dizesini gösteren TelcoGenerator uygulama yapılandırma dosyası](./media/stream-analytics-real-time-fraud-detection/stream-analytics-telcogenerator-config-file-app-settings.png)
 
4.  Merhaba dosyasını kaydedin. 

### <a name="start-hello-app"></a>Merhaba uygulamayı başlatın
1.  Bir komut penceresi açın ve hello TelcoGenerator uygulama sıkıştırması açılmış olduğu toohello klasörü değiştirin.
2.  Merhaba aşağıdaki komutu girin:

        telcodatagen.exe 1000 .2 2

    Merhaba Parametreler şunlardır: 

    * Saat başına CDR sayısı. 
    * SIM kart sahtekarlık olasılık: Sıklıkla, tüm çağrıları yüzdesi olarak bu hello uygulama sahte bir çağrı benzetimini yapmak. Başlangıç değeri 2'dir yaklaşık %20 hello çağrısı kayıtların sahte görüneceğini anlamına gelir.
    * Saat cinsinden süre. Uygulama hello saat Hello sayısını çalıştırmanız gerekir. Ayrıca, hello uygulama hello komut satırında Ctrl + C tuşlarına basarak istediğiniz zaman durdurabilirsiniz.

    Birkaç saniye sonra bunları toohello olay hub'ı gönderir olarak telefon araması kayıtları Merhaba ekranında görüntüleme hello uygulaması başlatır.

Bu gerçek zamanlı sahtekarlık algılama uygulamada kullanarak hello anahtar alanları bazıları hello aşağıda verilmiştir:

|**Kayıt**|**Tanımı**|
|----------|--------------|
|`CallrecTime`|Merhaba zaman damgası hello çağrısı için başlangıç saati. |
|`SwitchNum`|Merhaba telefon anahtar tooconnect hello çağrısı kullanılır. Bu örnekte, kaynağı (ABD, Çin, İngiltere, Almanya veya Avustralya) hello ülke temsil eden dizeleri hello anahtarlar şunlardır. |
|`CallingNum`|Merhaba çağıran Hello telefon numarası. |
|`CallingIMSI`|Merhaba uluslararası mobil abone kimliği (IMSI). Merhaba çağıran benzersiz tanıtıcısı hello budur. |
|`CalledNum`|Merhaba çağrı alıcı Hello telefon numarası. |
|`CalledIMSI`|Uluslararası mobil abone kimliği (IMSI). Bu hello çağrısı alıcısının hello benzersiz tanımlayıcısı değil. |


## <a name="create-a-stream-analytics-job-toomanage-streaming-data"></a>Veri akış Stream Analytics işi toomanage oluşturma

Çağrı olayların bir akışa sahip olduğunuza göre bir akış analizi işi ayarlayabilirsiniz. Merhaba iş ayarladığınız hello olay hub'dan verileri okur. 

### <a name="create-hello-job"></a>Merhaba işi oluşturma 

1. Hello Azure portal'ı tıklatın **yeni** > **nesnelerin interneti** > **Stream Analytics işi**.

2. Ad hello iş `sa_frauddetection_job_demo`, abonelik, kaynak grubunu ve konumu belirtin.

    Bir fikir tooplace hello iş ve hello event hub'ında hello olan en iyi performans ve bunu için aynı bölge bölgeler arasında tootransfer veri ödemeniz gerekmez.

    ![Yeni Stream Analytics işi oluşturma](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-sa-job-new-portal.png)

3. **Oluştur**'a tıklayın.

    Merhaba iş oluşturulur ve hello portal iş ayrıntılarını görüntüler. Henüz hiçbir şey ancak çalıştığı — bunu başlamadan önce tooconfigure hello iş sahip.

### <a name="configure-job-input"></a>İş Girişi yapılandırın

1. Merhaba Pano veya hello **tüm kaynakları** dikey bulun ve seçin hello `sa_frauddetection_job_demo` Stream Analytics işi. 
2. Merhaba, **iş topoloji** hello Stream Analytics iş dikey penceresi, bölümüne tıklatın hello **giriş** kutusu.

    ![Giriş kutusuna hello akış analizi işi dikey topoloji altında](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-input-box-new-portal.png)
 
3. Tıklatın  **+ &nbsp;Ekle** ve ardından hello dikey şu değerlerle doldurun:

    * **Giriş diğer adı**: hello adını kullan `CallStream`. Farklı bir ad kullanırsanız, daha sonra ihtiyacınız olacak çünkü bunu not edin.
    * **Kaynak türünü**: seçin **veri akışı**. (**Başvuru verileri** Bu öğreticide kullanmayacaksa toostatic arama verileri ifade eder.)
    * **Kaynak**: seçin **olay hub'ı**.
    * **Alma seçeneği**: seçin **geçerli aboneliğe ilişkin kullanım olay hub'ı**. 
    * **Hizmet veri yolu ad alanı**: daha önce oluşturduğunuz hello olay hub'ad alanı seçin (`<yourname>-eh-ns-demo`).
    * **Olay hub'ı**: daha önce oluşturduğunuz Select hello olay hub'ı (`sa-eh-frauddetection-demo`).
    * **Olay hub'ı ilke adı**: daha önce oluşturduğunuz hello erişim ilkesi seçin (`sa-policy-manage-demo`).

    ![Akış analizi işi için yeni giriş oluşturma](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-sa-input-new-portal.png)

4. **Oluştur**'a tıklayın.

## <a name="create-queries-tootransform-real-time-data"></a>Tootransform gerçek zamanlı verileri sorgular oluşturma

Bu noktada, gelen bir veri akışı tooread ayarlamak akış analizi işi var. Merhaba sonraki toocreate hello verileri gerçek zamanlı analiz dönüştürme adımdır. Bunun için bir sorgu oluşturarak. Akış analizi dönüştürmeleri için gerçek zamanlı işleme açıklayan bir basit ve bildirim temelli sorgu modelini destekler. Merhaba sorguları bazı uzantılar belirli toostream analytics sahip SQL benzeri bir dil kullanın. 

Çok basit bir sorgu yalnızca tüm hello gelen verileri okuyabilir. Ancak, genellikle özel veriler için veya hello verilerdeki ilişkileri arayın sorgular oluşturun. Merhaba öğreticinin bu bölümünde oluşturun ve birkaç sorgu toolearn çözümleme için bir giriş akışı dönüştürebilirsiniz birkaç şekilde sınayın. 

Burada oluşturduğunuz hello sorgular yalnızca hello dönüştürülen veriler toohello ekranı görüntüler. Sonraki bölümde, çıkış havuzu ve hello dönüştürülen veriler toothat havuz Yazar bir sorgu yapılandıracaksınız.

toolearn hello dili hakkında daha fazla bilgi görmek hello [Azure Stream Analytics sorgu dili başvurusu](https://msdn.microsoft.com/library/dn834998.aspx).

### <a name="get-sample-data-for-testing-queries"></a>Sorguları test etmek için örnek veri al

Merhaba TelcoGenerator uygulama çağrısı kayıtları toohello olay hub'ı gönderme ve Stream Analytics iş hello olay hub'dan yapılandırılmış tooread. Bir sorgu tootest hello iş toomake doğru okuma emin kullanabilirsiniz. çok hello Azure konsolunda bir sorguyu sınamak, örnek verileri gerekir. Bu kılavuzda hello event hub'ına gelen hello akıştan örnek verileri ayıklamak.

1. Bu hello TelcoGenerator uygulaması çalıştıran ve çağrı kayıtları oluşturan emin olun.
2. Hello Portalı'nda toohello akış analizi işi dikey penceresine dönün. (Merhaba dikey kapattıysanız, arama `sa_frauddetection_job_demo` hello içinde **tüm kaynakları** dikey.)
3. Merhaba tıklatın **sorgu** kutusu. Azure hello girişleri listeler ve toohello çıktı gönderilmiş gibi hello proje için yapılandırılmış ve olanak sağlayan bir sorgu oluşturmanıza olanak tanır çıkışları hello Giriş akışı Dönüştür.
4. Merhaba, **sorgu** dikey penceresinde hello nokta sonraki toohello tıklatın `CallStream` girin ve ardından **örnek giriş verilerinden**.

    ![Menü seçeneklerini toouse için örnek veri hello akış analizi işi girişi, verilerle"Seçili örnek Giriş"](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-sample-data-from-input.png)

    Bu akış ne kadar süreyle tooread hello girişi bakımından tanımlanmış ne kadar örnek veri tooget belirtmenize olanak sağlar. bir dikey pencere açılır.

5. Ayarlama **dakika** too3 ve ardından **Tamam**. 
    
    !["3 Seçili dakika ile" Merhaba Giriş akışı örnekleme seçenekleri.](./media/stream-analytics-real-time-fraud-detection/stream-analytics-input-create-sample-data.png)

    Azure hello Giriş akışı verilerden 3 dakika eşitleyeceğini örnekleri ve hello örnek verileri hazır olduğunda size bildirir. (Bu kısa biraz uzun sürebilir.) 

Merhaba örnek verileri geçici olarak depolanır ve açmak hello sorgu penceresi açıkken kullanılabilir. Merhaba sorgu penceresini kapattığınızda, hello örnek veriler atılır ve yeni bir örnek veri kümesi toocreate sahip olacaksınız. 

Alternatif olarak, örnek veriler olan bir .json dosyası alabilirsiniz [github'dan](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/telco.json)ve ardından bu .json dosyası toouse hello için örnek veri olarak karşıya yükleme `CallStream` giriş. 

### <a name="test-using-a-pass-through-query"></a>Bir doğrudan geçirilen sorgu kullanmadan test edin

Her olay tooarchive istiyorsanız, tüm hello alanları hello olayın hello yükte doğrudan sorgu tooread kullanabilirsiniz.

1. Merhaba sorgu penceresinde, bu sorguyu girin:

        SELECT 
            *
        FROM 
            CallStream

    >[!NOTE]
    >İle SQL gibi anahtar sözcükler büyük küçük harfe duyarlı değildir ve boşluk önemli değildir.

    Bu sorguda `CallStream` olan hello alias hello giriş oluşturduğunuzda belirttiğiniz. Farklı bir diğer ad kullandıysanız, bunun yerine bu adı kullanın.

2. Tıklatın **Test**.

    Merhaba Stream Analytics işi hello örnek verileri karşı hello sorgusu çalıştırır ve hello çıktı hello penceresinin hello altında görüntüler. Bu hello olay hub'ı ve hello akış analizi işi düzgün yapılandırılmış olduğunu bildirir. (Belirtildiği gibi daha sonra çıkış havuzu bu hello oluşturacağınız veri için sorgu yazabilirsiniz.)

    ![Stream Analytics işi çıkış, oluşturulan 73 kaydı gösteriliyor](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output.png)

    Merhaba tam kayıt sayısı, gördüğünüz kaç kayıt 3 dakika örneğinizi yakalanan bağlı olacaktır.
 
### <a name="reduce-hello-number-of-fields-using-a-column-projection"></a>Bir sütun projeksiyonu kullanarak alanları Hello sayısını azaltın

Çoğu durumda, çözümleme hello Giriş akışı tüm hello sütunlarından gerekmez. Daha küçük bir dizi alanları daha hello doğrudan sorgusunda döndürülen bir sorgu tooproject kullanabilirsiniz.

1. Merhaba Kod Düzenleyicisi toohello aşağıdaki Hello sorguyu değiştirin:

        SELECT CallRecTime, SwitchNum, CallingIMSI, CallingNum, CalledNum 
        FROM 
            CallStream

2. Tıklatın **Test** yeniden. 

    ![Stream Analytics işi çıkış oluşturulan 25 kayıtları gösteren projeksiyon için](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output-projection.png)
 
### <a name="count-incoming-calls-by-region-tumbling-window-with-aggregation"></a>Count gelen bölgeye göre çağırır: atlayan pencere toplama ile

Toocount hello gelen başına çağrı sayısı bölge istediğinizi varsayalım. Sayımı gibi toplama işlevleri tooperform istediğinizde (Merhaba veri akışı kendisini etkili bir şekilde sonsuz olduğundan) akış veri toosegment hello akış zamana bağlı birimlerine ihtiyacınız var. Akış analizi kullanarak bunu [pencere işlevi](stream-analytics-window-functions.md). Bir birim olarak söz konusu pencereyi içindeki hello verileri sonra çalışabilirsiniz.

Bu dönüştürme için bir dizi çakışmadığından zamana bağlı windows istediğiniz — her pencere, gruplandırabilirsiniz veri ve toplama ayrık kümesine sahip. Bu pencere başvurulan tooas türünde bir *atlayan pencere* . Merhaba atlayan pencere içinde göre gruplandırılmış hello gelen çağrıların sayısını alabilir `SwitchNum`, burada hello aramanın hello ülke temsil eder. 

1. Merhaba Kod Düzenleyicisi toohello aşağıdaki Hello sorguyu değiştirin:

        SELECT 
            System.Timestamp as WindowEnd, SwitchNum, COUNT(*) as CallCount 
        FROM
            CallStream TIMESTAMP BY CallRecTime 
        GROUP BY TUMBLINGWINDOW(s, 5), SwitchNum

    Bu sorgu hello kullanır `Timestamp By` hello anahtar sözcük `FROM` hello hangi zaman damgası alanında giriş akışı toouse toodefine hello atlayan pencere yan tümcesi toospecify. Merhaba penceresinde hello veri kesimler halinde hello tarafından bu durumda, böler `CallRecTime` her bir kayıttaki alan. (Hiçbir alan belirtilmezse, her olay hello olay hub'ına ulaştığında hello zaman hello Pencereleme işlemi kullanır. "Geliş saati Vs uygulama saati" bölümüne bakın [Stream Analytics sorgu dili başvurusu](https://msdn.microsoft.com/library/azure/dn834998.aspx). 

    Merhaba projeksiyon içeren `System.Timestamp`, her penceresinde hello sonunun zaman damgası döndürür. 

    toouse atlayan pencere istediğiniz toospecify kullandığınız hello [TUMBLINGWINDOW](https://msdn.microsoft.com/library/dn835055.aspx) hello işlevinde `GROUP BY `yan tümcesi. Merhaba işlevinde bir zaman birimi (herhangi bir yere milisaniyeye tooa günde bir) ve pencere boyutunu (kaç birimleri) belirtin. Bu örnekte, nedenle ülkeye göre bir sayısı için her 5 saniyede eşitleyeceğini çağrılarının karşılaşırsınız hello atlayan pencere 5 saniyelik aralıklarına oluşur.

2. Tıklatın **Test** yeniden. Bu hello zaman damgaları altında Hello sonuçlarında fark **WindowEnd** 5 saniyelik artışlarla şunlardır.

    ![Stream Analytics işi çıkış oluşturulan 13 kayıtları gösteren toplama için](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output-aggregation.png)
 
### <a name="detect-sim-fraud-using-a-self-join"></a>Kendi kendine birleşim kullanarak SIM sahtekarlık algılama

Bu örnekte, biz sahte kullanım hello aynı kaynaklanan toobe çağrıları düşünebilirsiniz kullanıcı ancak birbirleriyle 5 saniye içinde farklı konumlarda. Örneğin, hello aynı kullanıcı yasal çağrısından hello ABD ve Avustralya'da hello adresindeki yapamaz aynı anda. 

toocheck bu durumlarda, veri toojoin hello akış tooitself hello üzerinde temel akış hello kendi kendine birleşim kullanabileceğiniz `CallRecTime` değeri. Çağrı hello burada kaydeder için sonra bakabilir `CallingIMSI` değeri (sayı kaynaklanan hello) aynı hello olduğu, ancak hello `SwitchNum` değeri (kaynağı ülke) olan değil hello aynı.

Veri akış ile bir birleşim kullandığınızda hello birleştirme satırları eşleşen ne kadar hello bazı sınırlamalar zamanında ayrılabilir sağlamanız gerekir. (Daha önce belirtildiği gibi veri akış hello etkili bir şekilde sınırsızdır.) Merhaba ilişki Hello zaman sınırları içinde hello belirtilen `ON` hello kullanarak hello JOIN yan tümcesinde `DATEDIFF` işlevi. Bu durumda, hello birleşim bir çağrı veri 5 saniye aralığını temel alır.

1. Merhaba Kod Düzenleyicisi toohello aşağıdaki Hello sorguyu değiştirin: 

        SELECT  System.Timestamp as Time, 
            CS1.CallingIMSI, 
            CS1.CallingNum as CallingNum1, 
            CS2.CallingNum as CallingNum2, 
            CS1.SwitchNum as Switch1, 
            CS2.SwitchNum as Switch2 
        FROM CallStream CS1 TIMESTAMP BY CallRecTime 
            JOIN CallStream CS2 TIMESTAMP BY CallRecTime 
            ON CS1.CallingIMSI = CS2.CallingIMSI 
            AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5 
        WHERE CS1.SwitchNum != CS2.SwitchNum

    Bu sorgu hello dışında herhangi bir SQL birleşimin gibidir `DATEDIFF` hello birleştirme işlevi. Bu bir sürümüdür `DATEDIFF` belirli tooStreaming Analytics olan ve hello görünmelidir `ON...BETWEEN` yan tümcesi. Merhaba zaman birimi (Bu örnekte saniye) ve hello diğer adlar hello iki kaynakları hello birleştirme için parametreleridir. (Bu farklıdır standart SQL hello `DATEDIFF` işlevi.) 

    Merhaba `WHERE` yan tümcesi içeren hello sahte çağrısı bayrakları hello koşul: hello kaynak anahtarları olan değil hello aynı. 

2. Tıklatın **Test** yeniden. 

    ![Stream Analytics işi çıkış oluşturulan kendi kendine birleşim, gösterme 6 kayıtlar için](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output-self-join.png)

3. **Kaydet** düğmesine tıklayın. Bu hello kendi kendine birleşim sorgu hello akış analizi işi bir parçası olarak kaydeder. (Merhaba örnek verileri kaydetmez.)

    ![Akış analizi işi Kaydet](./media/stream-analytics-real-time-fraud-detection/stream-analytics-query-editor-save-button-new-portal.png)

## <a name="create-an-output-sink-toostore-transformed-data"></a>Bir çıkış havuzu toostore dönüştürülmüş verileri oluşturma

Bir olay akışı, bir olay hub'ı giriş tooingest olayları ve sorgu tooperform dönüştürme hello akış üzerinden tanımladığınız. Merhaba son adımdır toodefine hello işi için çıkış havuzu — diğer bir deyişle, bir yere toowrite hello akışa dönüştürüldüğünde. 

Birçok kaynakları çıkış havuzlarını kullanabilirsiniz — bir SQL Server veritabanı, tablo depolama, Data Lake storage, Power BI ve hatta başka bir olay hub'ı. Bu öğretici için hello akış tooAzure yapılandırılmamış verileri düzenler beri sonraki çözümleme için olay bilgilerini toplamak için tipik bir seçimdir Blob Storage yazacaksınız.

Blob depolama hesabınız varsa, kullanabilirsiniz. Bu öğretici için nasıl toocreate yeni bir depolama hesabı yalnızca Bu öğretici için göstereceğiz.

### <a name="create-an-azure-blob-storage-account"></a>Bir Azure Blob Storage hesabı oluşturma

1. Hello Azure portal, toohello akış analizi işi dikey penceresine dönün. (Merhaba dikey kapattıysanız, arama `sa_frauddetection_job_demo` hello içinde **tüm kaynakları** dikey.)
2. Merhaba, **iş topoloji** bölümünde, hello tıklatın **çıkış** kutusu. 
3. Merhaba, **çıkışları** dikey penceresinde tıklatın  **+ &nbsp;Ekle** ve ardından hello dikey şu değerlerle doldurun:

    * **Çıkış diğer adları**: hello adını kullan `CallStream-FraudulentCalls`. 
    * **Havuz**: seçin **Blob storage**.
    * **İçe aktarma seçenekleri**: seçin **blob storage'ı geçerli aboneliğe ilişkin kullanma**.
    * **Depolama hesabı**. Seçin **yeni depolama hesabı oluşturun.**
    * **Depolama hesabı** (ikinci kutusu). Girin `YOURNAMEsademo`, burada `YOURNAME` adınızı veya başka bir benzersiz bir dize. Merhaba adı yalnızca küçük harfler ve sayılar kullanabilirsiniz ve Azure arasında benzersiz olması gerekir. 
    * **Kapsayıcı**. Girin `sa-fraudulentcalls-demo`.
    Merhaba depolama hesabı adı ve kapsayıcı adı kullanılan birlikte tooprovide bu gibi hello blob depolama için bir URI şunlardır: 

    `http://yournamesademo.blob.core.windows.net/sa-fraudulentcalls-demo/...`
    
    ![Stream Analytics işi için "Yeni çıkış" dikey](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-output-blob-storage-new-console.png)
    
4. **Oluştur**'a tıklayın. 

    Azure hello depolama hesabı oluşturur ve bir anahtarı otomatik olarak oluşturur. 

5. Kapat hello **çıkışları** dikey. 

## <a name="start-hello-streaming-analytics-job"></a>Merhaba akış analizi işi Başlat

Merhaba iş artık yapılandırılmıştır. Bir giriş (Merhaba olay hub), bir dönüştürme (Merhaba sorgu toolook sahte aramalar için) ve bir çıkış (blob depolama) belirlediniz. Şimdi hello işi başlatabilirsiniz. 

1. Merhaba TelcoGenerator uygulama çalıştığından emin olun.

2. Merhaba iş dikey penceresinde tıklayın **Başlat**.

    ![Merhaba Stream Analytics işi Başlat](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-start-output.png)

3. Merhaba, **başlangıç işi** dikey penceresinde, iş çıktısı başlangıç saati, select **şimdi**. 

4. Tıklatın **Başlat**. 

    ![Dikey penceresinde hello Stream Analytics işi "işlemini Başlat"](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-start-job-blade.png)

    Azure sizi uyarır hello iş başlatıldı ve hello iş dikey penceresinde hello durumu olarak görüntülendiğinde **çalıştıran**.

    ![Stream Analytics iş durumu, "Çalışır" gösterme](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-running-status.png)
    

## <a name="examine-hello-transformed-data"></a>Dönüştürülen hello veri inceleyin

Artık tam bir akış analizi işi var. Hello iş telefon araması meta veri akışı inceleyerek, gerçek zamanlı sahte telefon aramaları için arama ve bu sahte çağrıları toostorage hakkında bilgi yazma. 

toocomplete Bu öğretici, hello akış analizi işi tarafından yakalanan hello veri toolook isteyebilirsiniz. Merhaba veri tooAzure Blog depolama öbekleri (dosyaları) yazılmakta. Azure Blob Storage okuyan herhangi bir aracı kullanabilirsiniz. Merhaba önkoşullar bölümünde belirtildiği gibi Visual Studio'da Azure uzantıları kullanabilir veya gibi bir araç kullanabilirsiniz [Azure Storage Gezgini](http://storageexplorer.com/) veya [Azure Gezgini](http://www.cerebrata.com/products/azure-explorer/introduction). 

Blob depolama birimindeki bir dosyanın içeriğini hello incelediğinizde, hello aşağıdaki gibi bir şey görürsünüz:

![Akış analizi çıktı ile Azure blob storage](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-blob-storage-view.png)
 

## <a name="clean-up-resources"></a>Kaynakları temizleme

Merhaba sahtekarlık algılama senaryoyla devam etmek ve Bu öğreticide oluşturduğunuz hello kaynakları kullanan diğer makaleler sahibiz. Merhaba önerileri altında toocontinue istiyorsanız bkz **sonraki adımlar** daha sonra.

Böylece gereksiz Azure ücrete tabi yoktur ancak, işiniz bittiğinde ve sizin oluşturduğunuz hello kaynakları gerekmiyorsa bunları silebilirsiniz. Bu durumda, aşağıdaki hello öneririz:

1. Merhaba akış analizi işi durdurun. Merhaba, **işleri** dikey penceresinde tıklatın **durdurmak** hello üstünde.
2. Merhaba Telco Oluşturucu uygulamayı durdurun. Merhaba uygulama başlatıldığı hello komut penceresinde Ctrl + C tuşlarına basın.
3. Bu öğretici için yeni bir blob depolama hesabı oluşturduysanız, onu silin. 
4. Merhaba akış analizi işi silin.
5. Merhaba olay hub'ı silin.
6. Merhaba olay hub'ı ad alanını silin.

## <a name="get-support"></a>Destek alın

Daha fazla yardım için deneyin bizim [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Sonraki adımlar

Bu öğretici makaleler hello ile devam edebilirsiniz:

* [Analizler ve Power BI akış: veri akışı için gerçek zamanlı analiz Pano](stream-analytics-power-bi-dashboard.md). Bu makalede nasıl toosend hello TelCo çıktısını hello Stream Analytics işi gerçek zamanlı Görselleştirme ve analiz için BI tooPower gösterilmektedir.
* [Nasıl bir Azure Redis Azure işlevleri kullanarak önbelleğinde Azure akış analizi toostore verileri](stream-analytics-functions-redis.md). Bu makalede nasıl toouse Azure işlevleri toowrite sahte tooan Azure Redis önbelleği Service Bus kuyruğuna aracılığıyla çağırır gösterilmektedir.

Stream Analytics hakkında daha fazla bilgi için genel olarak, bu makaleler deneyin:

* [Giriş tooAzure akış analizi](stream-analytics-introduction.md)
* [Azure Akış Analizi işlerini ölçeklendirme](stream-analytics-scale-jobs.md)
* [Azure Akış Analizi Sorgu Dili Başvurusu](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Akış Analizi Yönetimi REST API'si Başvurusu](https://msdn.microsoft.com/library/azure/dn835031.aspx)
