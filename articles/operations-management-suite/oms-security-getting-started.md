---
title: "Operations Management Suite güvenlik ve denetim çözümü ile aaaGetting başlatıldı | Microsoft Docs"
description: "Bu belge, tooget Operations Management Suite güvenlik ve denetim çözüm özellikleri toomonitor ile karma bulut başlatılan yardımcı olur."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 754796ef-a43e-468a-86c9-04a2eda55b5b
ms.service: operations-management-suite
ms.custom: oms-security
ms.topic: get-started-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: yurid
ms.openlocfilehash: 5cb3e5dbb3e60f9702a34c9413ddc1bf2b14b411
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-operations-management-suite-security-and-audit-solution"></a>Operations Management Suite Güvenlik ve Denetim Çözümünü kullanmaya başlama
Bu belge, size her bir seçenekte yol göstererek Operations Management Suite (OMS) Güvenlik ve Denetim çözümü becerilerini hızlıca kullanmaya başlamanıza yardımcı olur.

## <a name="what-is-oms"></a>OMS nedir?
Microsoft Operations Management Suite (OMS), şirket içi ve bulut altyapınızı yönetmenize ve korumanıza yardımcı olan, Microsoft'un bulut tabanlı BT yönetim çözümüdür. OMS hakkında daha fazla bilgi için hello makaleyi okuyun [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx).

## <a name="oms-security-and-audit-dashboard"></a>OMS Güvenlik ve Denetim panosu
Merhaba OMS güvenlik ve denetim çözümü sağlar, kuruluşunuzun kapsamlı bir görünüme BT güvenlik tutumunu dikkat etmeniz gereken önemli sorunlar için yerleşik arama sorguları. Merhaba **güvenlik ve Denetim** Pano olan her şeyi hello giriş ekranı ilgili OMS toosecurity. Bilgisayarlarınızı hello güvenlik durumunu üst düzey bir anlayış sağlar. Son 24 saat, 7 gün hello tüm olayları veya diğer özel zaman çerçevesi ayrıca hello özelliği tooview içerir. tooaccess hello **güvenlik ve Denetim** Panosu, aşağıdaki adımları izleyin:

1. Merhaba, **Microsoft Operations Management Suite** ana Pano tıklatın **ayarları** hello sol bölme.
2. Merhaba, **ayarları** dikey altında **çözümleri** tıklatın **güvenlik ve Denetim** seçeneği.
3. Merhaba **güvenlik ve Denetim** Pano görüntülenir:
   
    ![OMS Güvenlik ve Denetim panosu](./media/oms-security-getting-started/oms-getting-started-fig1-ga.png)

Bu panoyu hello için ilk kez erişme ve OMS tarafından izlenen cihazlar yoksa hello döşeme hello Aracısı'ndan alınan verilerle doldurulmaz. Merhaba aracı yükledikten sonra bazı zaman toopopulate alabilir, hala toohello bulut karşıya gibi bu nedenle başlangıçta gördüğünüz bazı veriler eksik olabilir.  Bu durumda, bazı kutucuklar somut bilgileri olmadan normal toosee olur. Okuma [bağlanmak Windows bilgisayarları doğrudan tooOMS](https://technet.microsoft.com/library/mt484108.aspx) hakkında daha fazla bilgi için Windows sisteminde tooinstall OMS aracısı ve [bağlanmak Linux bilgisayarları tooOMS](https://technet.microsoft.com/library/mt622052.aspx) hakkında daha fazla bilgi için tooperform bu görevi bir Linux sisteminde.

> [!NOTE]
> Merhaba Aracısı etkin olan hello geçerli olaylara göre örneği için bilgisayar adı, IP adresi ve kullanıcı adı hello bilgi toplar. Ancak belgeler/dosyalar, veritabanı adı veya özel veriler toplanmaz.   
> 
> 

Çözümler, önemli müşteri taleplerine yönelik mantık, görselleştirme ve veri alımı kurallarından oluşan bir koleksiyondur. Güvenlik ve Denetim tek bir çözümdür; diğer çözümler ayrıca eklenebilir. Merhaba makale okuma [çözümleri Ekle](https://technet.microsoft.com/library/mt674635.aspx) hakkında daha fazla bilgi için tooadd yeni bir çözüm.

Merhaba OMS güvenlik ve Denetim Panosu dört ana kategoride düzenlenmiştir:

* **Güvenlik etki alanları**: Bu alanda sunulan mümkün toofurther olacaktır zaman içindeki güvenlik kayıtları keşfetmek, erişim kötü amaçlı yazılım değerlendirmesi, değerlendirme, ağ güvenliği, kimlik ve erişim bilgileri, bilgisayarları güvenlik olayları ile güncelleştirin ve hızlı bir şekilde sahip erişim tooAzure Güvenlik Merkezi panosunu.
* **Önem düzeyindeki sorunlar**: Bu seçenek tooquickly sağlayacak etkin sorunlar hello sayısını tanımlamak ve hello bu sorunların önem derecesi.
* **Algılama (Önizleme)**: kaynaklarınızı karşı yer alırken güvenlik uyarıları görselleştirme tooidentify saldırı desenleri sağlar.
* **Tehdit Intelligence**: hello sayısı toplam giden kötü amaçlı IP trafiğinin, hello kötü amaçlı tehdit türünü ve burada bu IP'leri geliyor gelen gösteren bir harita sunucularıyla görselleştirme tarafından tooidentify saldırı desenleri sağlar. 
* **Ortak Güvenlik sorguları**: Bu seçenek, hello en yaygın güvenlik listesini sorgular ortamınızı toomonitor kullanabileceğiniz sağlar. Bu sorguları birine tıkladığınızda hello açılır **arama** hello sonuçlarla dikey penceresinde bu sorgu için.

> [!NOTE]
> OMS'nin verilerinizi nasıl koruduğuna ilişkin daha fazla bilgi için bkz. OMS verilerinizin güvenliğini nasıl sağlar?.
> 
> 

## <a name="security-domains"></a>Güvenlik etki alanları
Kaynak İzleme önemli toobe mümkün tooquickly erişim hello geçerli durumu ortamınızın olur. Ancak, belirli bir noktada, ortamınızdaki zamanında olanlar tooa daha iyi anlamak açabilir geçmiş hello oluşan önemli toobe mümkün tootrack geri olayları da sağlar. 

> [!NOTE]
> veri saklama toohello OMS fiyatlandırma planı göre yapılır. Daha fazla bilgi için hello ziyaret [Microsoft Operations Management Suite](https://www.microsoft.com/server-cloud/operations-management-suite/pricing.aspx) fiyatlandırma sayfası.
> 
> 

Olay yanıtlama ve adli araştırma senaryoları hello kullanılabilir hello sonuçlarından doğrudan yararlanacaktır **zaman içindeki güvenlik kayıtları** döşeme.

![Zaman içindeki güvenlik kayıtları](./media/oms-security-getting-started/oms-getting-started-fig2.JPG)

Bu kutucuğa tıkladığınızda hello **arama** dikey penceresi açılır, sorgu sonucu gösteren **güvenlik olaylarını** (tür SecurityEvents =) üzerinde hello son yedi gün, aşağıda gösterildiği gibi temel verilerle:

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Zaman içindeki güvenlik kayıtları](./media/oms-security-getting-started/oms-getting-started-fig3.JPG)

Merhaba arama sonucu iki bölmelerinde bölünür: hello sol bölmesinde, bu olayları bulundu, bu bilgisayarların bulunan hesapları hello sayısı ve hello türleri hello bilgisayarlar bulundu güvenlik olaylarını hello sayısı dökümünü sağlar etkinlikler. Merhaba sağ bölmede hello toplam sonuçları ve hello güvenlik olaylarını hello bilgisayarın adını ve olay etkinliği ile kronolojik bir görünümünü sağlar. Tıklatarak **Göster daha fazla** tooview hello olay verileri, hello olay kimliği ve hello olay kaynağı gibi bu olay hakkında daha ayrıntılı.

> [!NOTE]
> OMS arama sorgusu hakkında daha fazla bilgi için bkz. [OMS arama başvurusu](https://technet.microsoft.com/library/mt450427.aspx).
> 
> 

### <a name="antimalware-assessment"></a>Kötü amaçlı yazılımdan koruma değerlendirmesi
Bu seçenek, tooquickly yetersiz koruma ve bir kötü amaçlı yazılımdan tehlikeye bilgisayarları ile bilgisayarları tanımlamak sağlar. Durum ve izlenen hello sunucularda algılanan tehditler okunur ve veri hello kötü amaçlı yazılım değerlendirmesi işleme hello bulutta toohello OMS hizmetine gönderilir. Algılanan tehditler içeren sunucular ve koruması yetersiz olan sunucular hello tıklattıktan sonra erişilebilir olan hello kötü amaçlı yazılım değerlendirmesi panosunda gösterilir **kötü amaçlı yazılımdan koruma değerlendirme** döşeme. 

![kötü amaçlı yazılım değerlendirmesi](./media/oms-security-getting-started/oms-getting-started-fig4-ga.png)

Tüm diğer Canlı kutucuk OMS panosunda yer gibi üzerine tıkladığınızda hello **arama** hello sorgu sonucu ile dikey penceresi açılır. Hello tıklarsanız bu seçeneğin **raporlama** altında seçeneği **koruma durumu**, olarak hello bilgisayarın adını ve kendi sıra içeren bu tek giriş gösterir hello sorgu sonucu gerekir aşağıda gösterilmektedir:

![arama sonucu](./media/oms-security-getting-started/oms-getting-started-fig5.png)

> [!NOTE]
> *RANK* olan tooreflect hello hello koruma durumunu vermiş bir düzeyde (, kapalı, güncelleştirilmiş, vb.) ve bulunan tehditleri. Bir sayı yardımcı toomake toplamalar sahip.
> 
> 

Merhaba bilgisayarın adına tıklayın, bu bilgisayar için hello koruma durumunun hello kronolojik görünümünü yüklemeniz gerekir. Bu, toounderstand hello kötü amaçlı yazılımdan koruma kez yüklenmişse ve belirli bir noktada kaldırılıp ihtiyacınız senaryoları için çok kullanışlıdır.   

### <a name="update-assessment"></a>Güncelleştirme değerlendirmesi
Bu seçeneği etkinleştirir, tooquickly belirlemek Etkilenme toopotential güvenlik sorunları hello olup veya nasıl bu güncelleştirmeler, ortamınız için önemlidir. OMS güvenlik ve denetim çözümü yalnızca, bu güncelleştirmeleri hello görselleştirme sağlamak, Merhaba gerçek veriler gelir [güncelleştirme yönetimi çözümleri](oms-solution-update-management.md), OMS içinde farklı bir modüle olduğu. Burada hello güncelleştirmelere bir örnek olarak:

![sistem güncelleştirmeleri](./media/oms-security-getting-started/oms-getting-started-fig6-new.png)

> [!NOTE]
> Güncelleştirme Yönetimi çözümü hakkında daha fazla bilgi için, [OMS’de Güncelleştirme Yönetimi çözümü](oms-solution-update-management.md) konusunu okuyun.
> 
> 

### <a name="identity-and-access"></a>Kimlik ve Erişim
Kimliği hello denetim olmalıdır düzlemi kimliğinizi koruma kuruluşunuz için en önemli öncelik olması gerekir. Merhaba geçmiş kuruluşlar geçici çevreyi yoktu ve bu çevreyi hello birincil savunma sınırları biri olan olsa da, günümüzde daha fazla veri ve daha fazla uygulama toohello bulut taşıma ile Merhaba kimlik hello yeni çevre olur. 

> [!NOTE]
> şu anda hello veri yalnızca güvenlik olaylarını oturum açma verileri (olay kimliği 4624) hello gelecekteki Office365 oturum açma bilgileri temel alır ve Azure AD verileri de dahil edilir.
> 
> 

Kimlik etkinliklerinizi izleyerek bir olay yer veya reaktif Eylemler toostop saldırı girişiminde yapmasından önce mümkün tootake öngörülü önlemler olacaktır. Merhaba **kimlik ve erişim** Pano başarısız girişim toolog kilitli hesapları bu girişimler sırasında kullanılan hello kullanıcının hesabı üzerinde hello sayısı dahil olmak üzere, kimlik durumu, genel bir bakış sağlar hesaplarıyla değiştirilemez ya da parola ve şu anda oturum açtığınız hesabı sayısını sıfırlayın. 

Hello tıkladığınızda **kimlik ve erişim** döşeme Panosu aşağıdaki hello görürsünüz:

![kimlik ve erişim](./media/oms-security-getting-started/oms-getting-started-fig7-ga.png)

Bu Panoda Hello bilgilerine hemen potansiyel şüpheli etkinlik tooidentify yardımcı olabilir. Örneğin, vardır 338 denemeleri toolog olarak **yönetici** ve % 100'bu girişimleri başarısız oldu. Bu durum, bu hesaba karşı gerçekleştirilen bir deneme yanılma saldırısından kaynaklanıyor olabilir. Bu hesaptaki tıklatırsanız toodetermine hello hedef kaynak bu olası saldırı yardımcı olabilecek daha fazla bilgi edinir:

![arama sonuçları](./media/oms-security-getting-started/oms-getting-started-fig8.JPG)

Merhaba ayrıntılı bir rapor sağlar bu olay hakkında önemli bilgiler dahil olmak üzere: hello hedef bilgisayar, oturum açma (içindeki case bu ağ oturumu) hello etkinliğinde (Bu örnek olay 4625) hello türü ve kapsamlı bir zaman çizelgesi her girişimi. 

### <a name="computers"></a>Bilgisayarlar
Bu kutucuğu kullanılan tooaccess güvenlik olaylarını etkin olan tüm bilgisayarlar olabilir. Bu kutucukta tıklattığınızda her bilgisayarda hello güvenlik olaylarını ve olayların hello numarasına sahip bilgisayarların listesini görürsünüz:

![Bilgisayarlar](./media/oms-security-getting-started/oms-getting-started-fig9.JPG)

Araştırmanızı her bilgisayarda tıklayarak devam edin ve işaretlenmiş hello güvenlik olayları gözden geçirin.

### <a name="threat-intelligence"></a>Tehdit Bilgisi

BT yöneticileri, OMS güvenlik ve denetim kullanılabilir Hello tehdit bilgileri seçeneğini kullanarak, güvenlik tehditlerine karşı hello ortamında, örneğin tanımlamak, belirli bir bilgisayardaki bir botnet parçası olup olmadığını belirleyebilmek. Saldırganlar bu bilgisayar toohello komut ve denetim gizlice bağlandığında kötü amaçlı yazılım yapacağıyla yüklediğinizde bilgisayarlar çoğunlukla düğümler olabilir. Ayrıca, darknet gibi yeraltı iletişim kanallarından gelen olası tehditleri de belirleyebilir. Okuyarak tehdit bilgileri hakkında daha fazla bilgi [izleme ve yanıt toosecurity uyarıları Operations Management Suite güvenlik ve denetim çözümü](oms-security-responding-alerts.md) makalesi.

Bazı senaryolarda, izlenen bir bilgisayardan erişilen olası bir kötü amaçlı IP ile karşılaşabilirsiniz:

![Tehdit bilgisi haritası](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig6.png)

Bu uyarı ve diğerleri içinde Merhaba aynı kategoride, OMS güvenlik yararlanarak oluşturulan [Microsoft tehdit bilgileri](https://youtu.be/O4WtxgUrDc8). Merhaba tehdit bilgileri veri Microsoft tarafından toplanan yanı sıra başında tehdit Intelligence sağlayıcılardan satın. Bu veriler, sık sık güncelleştirilir ve toofast taşıma tehditleri uyarlanan. Tooits yapısı, bu güvenlik bilgileri sırasında diğer kaynakları ile birleştirilmelidir [araştırma](https://blogs.technet.microsoft.com/msoms/2016/12/08/investigating-suspicious-activity-in-a-hybrid-cloud-with-oms-security/) bir güvenlik uyarısı. 

### <a name="baseline-assessment"></a>Temel Değerlendirme

Dünya çapındaki sektör ve devlet kuruluşlarıyla birlikte Microsoft, yüksek güvenlikli sunucu dağıtımlarını temsil eden bir Windows yapılandırması tanımlar. Bu yapılandırma, kayıt defteri anahtarlarının, denetim ilkesi ayarlarının ve güvenlik ilkesi ayarlarının yanı sıra Microsoft'un bu ayarlar için önerilen değerlerinden oluşan bir kümedir. Bu kural kümesi, Güvenlik temeli olarak bilinir. Bu seçenek hakkında daha fazla bilgi için [Operations Management Suite Güvenlik ve Denetim Çözümünde Temel Değerlendirmesi](oms-security-baseline.md) makalesini okuyun.

### <a name="azure-security-center"></a>Azure Güvenlik Merkezi
Bu kutucuğu temel bir kısayol tooaccess Azure Güvenlik Merkezi panosunu olur. Bu çözüm hakkında daha fazla bilgi için bkz. [Azure Güvenlik Merkezini Kullanmaya Başlama](../security-center/security-center-get-started.md).

## <a name="notable-issues"></a>Önemli sorunlar
Bu grup seçeneklerinin ana amacı Hello tooprovide kritik, uyarı ve bilgilendirici sınıflandırarak, ortamınızda sahip hello sorunlarını hızlı bir görünümünü ' dir. Bu sorunların bir görsel öğe olduğu etkin sorun türü döşeme Merhaba, ancak, daha fazla ayrıntı bunları hakkında tooexplore izin vermez için gereksinim duyduğunuz toouse hello alt kısmı kaç nesneler (sayı) bunu içeriyor hello sorunu (ad) hello adına sahip bu kutucuğu ve nasıl bunu (önem DERECESİ) önemlidir.

![Önemli sorunlar](./media/oms-security-getting-started/oms-getting-started-fig10.JPG)

Bu sorunları hello farklı alanlarında zaten kapsanan görebilirsiniz **güvenlik etki alanları** bu görünüm hello amacı eklenir Grup: tek bir yerden ortamınızdaki en önemli sorunlardan hello görselleştirin.

## <a name="detections-preview"></a>Algılama (Önizleme)
Merhaba bu seçeneği ana amacı olan tooallow BT tooquickly aracılığıyla olası tehditler tootheir ortamı ve bu tehdit hello önemini belirleyin.

![Tehdit Bilgisi](./media/oms-security-getting-started/oms-getting-started-fig12.png)

Bu seçenek ayrıca sırasında kullanılabilir bir [olay yanıtlama araştırma](https://blogs.msdn.microsoft.com/azuresecurity/2016/11/30/investigating-suspicious-activity-in-a-hybrid-cloud-with-oms-security/) tooperform hello değerlendirmesi ve hello saldırı hakkında daha fazla bilgi edinin.

> [!NOTE]
> Hakkında daha fazla bilgi için toouse OMS olay yanıtı için bu videoyu izleyin: [nasıl tooLeverage hello Azure Güvenlik Merkezi & Microsoft Operations Management Suite bir olay yanıtı için](https://channel9.msdn.com/Blogs/Taste-of-Premier/ToP1703).
> 
> 

## <a name="threat-intelligence"></a>Tehdit Bilgisi
Merhaba hello güvenlik ve denetim çözümü Intelligence bölümünü visualizes hello olası bir saldırı desenleri çeşitli şekillerde yeni tehdit: Merhaba giden kötü amaçlı IP trafiğinin sunucularıyla toplam sayısı, kötü amaçlı tehdit türü ve nereye gösteren bir harita hello bu IP'leri ' ten gelen. Merhaba Haritası etkileşim ve hello IP'leri daha fazla bilgi için tıklatın.

Sarı iğneleri hello haritaya kötü amaçlı Ip'lerle giden trafiği belirtir. Bu sunucuları toohello Internet toosee gelen kötü amaçlı trafiği kullanıma sunulan, ancak bunların hiçbiri başarılı emin bu girişimleri toomake incelemeniz önerilir seyrek değil. Bu göstergeler IIS günlüklerini, İletilen Verileri ve Windows Güvenlik Duvarı günlüklerini temel alır.  

![Tehdit Bilgisi](./media/oms-security-getting-started/oms-getting-started-fig11-ga.png)

## <a name="common-security-queries"></a>Ortak güvenlik sorguları
Ortak Güvenlik sorguları Hello listesi, toorapidly erişim kaynağın bilgiler için yararlı ve ortamınıza 's gereksinimlerine göre özelleştirin. Bu ortak sorgular şunlardır:

* Tüm Güvenlik Etkinlikleri
* Güvenlik etkinliklerini hello bilgisayar "bilgisayar01.contoso.com" (kendi bilgisayarınızın adıyla değiştirin)
* Merhaba bilgisayar "bilgisayar01.contoso.com" hesap "Yönetici" (kendi bilgisayarınızın ve hesabınızın adıyla değiştirin) için güvenlik etkinlikleri
* Bilgisayara göre Oturum Açma Etkinliği
* Herhangi bir bilgisayarda Microsoft kötü amaçlı yazılımdan koruma yazılımını sonlandıran hesaplar
* Merhaba Microsoft kötü amaçlı yazılımdan koruma işlemi burada sonlandırıldığı bilgisayarlar
* "Hash.exe" işleminin (farklı bir işlem adıyla değiştirin) yürütüldüğü bilgisayarlar
* Yürütülen tüm İşlem adları
* Hesaba göre Oturum Açma Etkinliği
* Uzaktan oturum açan hello bilgisayar "bilgisayar01.contoso.com" (kendi bilgisayarınızın adıyla değiştirin) hesaplarında

## <a name="see-also"></a>Ayrıca bkz.
Bu belgede, sunulan tooOMS güvenlik ve denetim çözüm bulunuyordu. toolearn OMS güvenlik hakkında daha fazla bilgi makaleleri aşağıdaki hello bakın:

* [Operations Management Suite'e (OMS) genel bakış](operations-management-suite-overview.md)
* [İzleme ve yanıt tooSecurity uyarıları Operations Management Suite güvenlik ve denetim çözümü](oms-security-responding-alerts.md)
* [Operations Management Suite Güvenlik ve Denetim Çözümünde Kaynakları İzleme](oms-security-monitoring-resources.md)

