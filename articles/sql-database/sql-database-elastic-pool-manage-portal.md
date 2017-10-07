---
title: "Azure portal: SQL Database esnek havuzunu yönetme & Oluştur | Microsoft Docs"
description: "Nasıl toouse Azure portal ve SQL Database'in yerleşik zekaya toomanage, İzleyici ve boyutlandırmanıza ölçeklenebilir bir esnek havuz toooptimize veritabanı performansını hello ve maliyet yönetmek öğrenin."
keywords: 
services: sql-database
documentationcenter: 
author: ninarn
manager: jhubbard
editor: cgronlun
ms.assetid: 3dc9b7a3-4b10-423a-8e44-9174aca5cf3d
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.date: 06/06/2016
ms.author: ninarn
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: e0de952bc0c91177f64c04363630783d72435741
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-an-elastic-pool-with-hello-azure-portal"></a>Oluşturma ve bir esnek havuz hello Azure portal ile yönetme
Bu konu, nasıl gösterir toocreate ve ölçeklenebilir yönetmek [esnek havuzlar](sql-database-elastic-pool.md) hello Azure portal ile. Ayrıca oluşturabilir ve ile Azure esnek havuzunu yönetme [PowerShell](sql-database-elastic-pool-manage-powershell.md), REST API hello veya [C#](sql-database-elastic-pool-manage-csharp.md). Ayrıca oluşturun ve içine ve dışına esnek havuzlar kullanarak veritabanlarını taşıma [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).

## <a name="create-an-elastic-pool"></a>Esnek havuz oluşturma 

Bir esnek havuz oluşturmanın iki yolu vardır. İstediğiniz ya da bir öneri hello hizmetinden başlayın hello havuz kurulumunu biliyorsanız sıfırdan yapabilirsiniz. SQL veritabanı maliyet açısından daha verimli kullanım telemetri veritabanlarınız için geçmiş hello temel alarak için ise, bir esnek havuz Kurulumu önerdiği yerleşik zekaya sahiptir.

Bir sunucuda birden çok havuz oluşturabilirsiniz, ancak hello farklı sunuculara ait veritabanlarını ekleyemezsiniz aynı havuzu. 

> [!NOTE]
> Esnek havuzlar şu anda önizleme aşamasında oldukları Batı Hindistan dışında tüm Azure bölgelerinde genel olarak kullanılabilir (GA) durumdadır.  Bu bölgede esnek havuz GA’sı olabildiğince çabuk ortaya çıkar.
>

### <a name="step-1-create-an-elastic-pool"></a>1. adım: bir esnek havuz oluşturma

Mevcut bir esnek havuz oluşturma **server** dikey penceresinde hello portal hello en kolay yolu toomove varolan veritabanlarına bir esnek havuz değil.

> [!NOTE]
> Arayarak bir esnek havuz oluşturabilirsiniz **SQL esnek havuzu** hello içinde **Market** veya tıklatarak **+ Ekle** hello içinde **SQL esnek havuzu**dikey göz atın. Mümkün toospecify yeni veya var olan bir sunucu iş akışı sağlama bu havuzu üzerinden var.
>
>

1. Merhaba, [Azure portal](http://portal.azure.com/), tıklatın **daha fazla hizmet**  **>**  **SQL sunucuları**ve hello içeren hello server'ı tıklatın veritabanları tooadd tooan esnek havuz istiyor.
2. **Yeni havuz** düğmesine tıklayın.

    ![Havuz tooa sunucu ekleme](./media/sql-database-elastic-pool-create-portal/new-pool.png)

    **-VEYA-**

    Bulunduğunu belirten bir ileti esnek havuzlar hello sunucu için önerilen görebilirsiniz. Önerilen havuzları geçmişe yönelik veritabanı kullanımı telemetrisi göz önünde bulundurularak hello ileti toosee hello tıklatın hello katmanı toosee daha fazla ayrıntı ve ardından hello havuzu özelleştirmek. Bkz: [havuz önerilerini anlama](#understand-elastic-pool-recommendations) hello öneri nasıl sunulacağını için bu konudaki sonraki.

    ![önerilen havuz](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)

3. Merhaba **esnek havuz** dikey penceresi görünür, hello ayarları havuzunuz için burada belirttiğiniz olduğu. Tıkladıysanız **yeni havuz** fiyatlandırma katmanı hello hello önceki adımda olduğu **standart** varsayılan ve hiçbir veritabanı tarafından seçilir. Boş bir havuz oluşturmak veya mevcut veritabanlarından bu sunucu toomove kümesi hello havuza belirtin. Önerilen bir havuzu oluşturuyorsanız, fiyatlandırma katmanı, performans ayarlarını hello önerilen ve veritabanlarının listesini önceden doldurulmaz ancak hala bunları değiştirebilirsiniz.

    ![Esnek havuzu yapılandırma](./media/sql-database-elastic-pool-create-portal/configure-elastic-pool.png)

4. Merhaba esnek havuz için bir ad belirtin veya hello varsayılan olarak bırakın.

### <a name="step-2-choose-a-pricing-tier"></a>2. Adım: Fiyatlandırma katmanı seçme

Merhaba havuzun fiyatlandırma katmanı hello kullanılabilir toohello elastics hello havuzu ve hello maksimum sayısını Edtu (Maks eDTU) ve depolama (GB) kullanılabilir tooeach veritabanı özellikleri belirler. Ayrıntılı bilgi için bkz. Hizmet Katmanları.

Merhaba havuzu için toochange hello fiyatlandırma Katmanı'nı tıklatın **fiyatlandırma katmanı**, fiyatlandırma katmanı ve ardından hello tıklatın **seçin**.

> [!IMPORTANT]
> Merhaba fiyatlandırma katmanı seçin ve değişikliklerinizi tıklatılarak sonra **Tamam** hello son adımda fiyatlandırma katmanı hello havuzunun mümkün toochange hello olmayacaktır. toochange var olan bir esnek havuz için fiyatlandırma katmanı Merhaba, hello istenen fiyatlandırma katmanında bir esnek havuz oluşturun ve hello veritabanları toothis yeni havuzunu geçirin.
>

![Fiyatlandırma katmanı seçme](./media/sql-database-elastic-pool-create-portal/pricing-tier.png)

### <a name="step-3-configure-hello-pool"></a>3. adım: hello havuzu yapılandırma

Fiyatlandırma katmanı hello ayarladıktan sonra havuzu Yapılandır veritabanları, havuz edtu'larını ve depolama (havuz GB) ekleyebilir ve hello havuzunda hello minimum ve maksimum Edtu hello elastics için ayarladığınız tıklatın.

1. **Havuzu yapılandır**'a tıklayın.
2. Tooadd toohello havuzu istediğiniz hello veritabanlarını seçin. Merhaba havuz oluşturulurken bu adım isteğe bağlıdır. Merhaba havuzu oluşturulduktan sonra veritabanları eklenebilir.
    tooadd veritabanları'nı **veritabanı Ekle**, tooadd istediğiniz ve hello ardından hello veritabanları'nı **seçin** düğmesi.

    ![Veritabanı ekleme](./media/sql-database-elastic-pool-create-portal/add-databases.png)

    Merhaba veritabanları ile çalışırken yeterli geçmiş kullanımı telemetri varsa, hello **tahmini eDTU ve GB kullanımı** grafik ve hello **gerçek eDTU kullanımı** çubuk grafik güncelleştirme toohelp, yaptığınız yapılandırma kararlar. Ayrıca, hello hizmeti, bir öneri iletisi toohelp verebilir, boyutlandırmanıza hello havuzu. Bkz. [Dinamik Öneriler](#understand-elastic-pool-recommendations).

3. Merhaba Hello denetimleri kullanın **havuzu yapılandırma** sayfa tooexplore ayarları ve havuzunuzu yapılandırmak. Bkz: [esnek havuz sınırları](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) daha fazla bilgi için her bir hizmet katmanına yönelik sınırlar hakkında ayrıntı ve bkz [esnek havuzlar için fiyat ve performans konuları](sql-database-elastic-pool.md) ayrıntılı yönergeler boyutlandırmaya bir esnek havuz. Havuz ayarları hakkında daha fazla bilgi için bkz: [esnek havuz özellikleri](sql-database-elastic-pool.md#database-properties-for-pooled-databases).

    ![Esnek Havuzu Yapılandırma](./media/sql-database-elastic-pool-create-portal/configure-performance.png)

4. Tıklatın **seçin** hello içinde **havuzu Yapılandır** dikey ayarlarını değiştirdikten sonra.
5. Tıklatın **Tamam** toocreate hello havuzu.

## <a name="understand-elastic-pool-recommendations"></a>Esnek havuz önerilerini anlama

Merhaba SQL veritabanı hizmetinin kullanım geçmişini değerlendirir ve onu tek veritabanlarını kullanmaktan daha verimliyse bir veya daha fazla havuzun kullanılmasını önerir. Her öneri hello havuzu en uygun hello sunucunun veritabanlarına benzersiz bir alt kümesiyle yapılandırılır.

![önerilen havuz](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)  

Merhaba havuz önerisi şunları kapsar:

- Merhaba havuzu (temel, standart, Premium veya Premium RS) için bir fiyatlandırma katmanı
- Uygun **HAVUZ eDTU'ları** (havuz başına maksimum eDTU olarak da adlandırılır)
- Merhaba **maksimum eDTU** ve **eDTU minimum** veritabanı başına
- Merhaba hello havuzu için önerilen veritabanlarının listesi

> [!IMPORTANT]
> Merhaba hizmet Merhaba, son 30 gün telemetri havuzları öneren zaman dikkate alır. Esnek havuz için aday olarak kabul veritabanı toobe en az 7 gündür bulunmalıdır. Zaten bir elastik havuzda bulunan veritabanları, elastik havuz önerileri için aday olarak kabul edilmez.
>

Merhaba hizmeti kaynak gereksinimlerini değerlendirir ve maliyet verimliliğini taşıma hello tek veritabanlarını her hizmet katmanında hello havuzları halinde aynı katmanı. Örneğin, bir sunucudaki tüm Standart veritabanları Standart Esnek Havuz'a uygunluk açısından değerlendirilir. Bu, hello hizmeti bir standart veritabanının bir Premium havuza taşınması gibi çapraz katmanlı önerilerde bulunmadığı anlamına gelir.

Veritabanlarını toohello havuzuna eklendikten sonra öneriler dinamik olarak hello geçmiş kullanımı, seçtiğiniz hello veritabanlarının dikkate alarak oluşturulur. Bu öneriler hello eDTU ve GB kullanım grafiğinde ve bir öneri başlığının hello hello üstünde gösterilir **havuzu yapılandırma** dikey. Bu öneriler, bir esnek havuz oluşturma belirli veritabanlarınız için iyileştirilmiş hedeflenen tooassist içindir.

![dinamik öneriler](./media/sql-database-elastic-pool-create-portal/dynamic-recommendation.png)

## <a name="manage-and-monitor-an-elastic-pool"></a>Yönetme ve bir esnek Havuz izleme

Hello Azure portal toomonitor kullanın ve hello havuzu hello veritabanlarını ve esnek havuz yönetin. Merhaba Portalı'ndan bir esnek havuz ve hello veritabanları aynı havuz içindeki hello kullanımını izleyebilirsiniz. Ayrıca bir değişiklik kümesini tooyour esnek havuzu yapmak ve tüm değişiklikler hello aynı gönderme zamanı. Bu değişiklikler ekleyerek veya veritabanları kaldırma, esnek havuz ayarlarınızı değiştirme veya veritabanı ayarlarını değiştirerek içerir.

Grafiği aşağıdaki hello bir örnek esnek havuz gösterir. Merhaba görünümü içerir:

*  Kaynak kullanımını hello esnek havuz ve hello havuzunda kapsanan hello veritabanlarını izleme grafikleri.
*  Merhaba **yapılandırma** havuzu düğmesi toomake toohello esnek havuz değiştirir.
*  Merhaba **veritabanı oluşturma** bir veritabanı oluşturur düğmesi ve toohello geçerli esnek havuz ekler.
*  Yardımcı esnek işler, listedeki tüm veritabanlarında Transact SQL komut dosyaları çalıştırarak veritabanları çok sayıda yönetin.

![Havuz görünümü][2]

Kaynak kullanımı tooa belirli havuzu toosee gidebilirsiniz. Varsayılan olarak, hello hello son saat için yapılandırılmış tooshow depolama ve eDTU kullanımı havuzudur. Merhaba grafik yapılandırılmış tooshow farklı ölçümleri çeşitli zaman pencereleri olabilir.

1. Esnek havuz toowork ile seçin.
2. Altında **esnek Havuz izleme** olan etiketli bir grafik **kaynak kullanımı**. Merhaba grafiği tıklatın.

    ![Esnek Havuz izleme][3]

    Merhaba **ölçüm** , hello belirtilen zaman penceresi belirtilen ölçümleri hello ayrıntılı görünümünü gösteren dikey pencere açılır.   

    ![Ölçüm dikey penceresi][9]

### <a name="toocustomize-hello-chart-display"></a>toocustomize hello grafik görüntüleme

CPU yüzdesi, veri g/ç yüzdesi ve kullanılan günlük GÇ yüzdesi gibi diğer ölçümleri hello grafik ve hello ölçüm dikey penceresi toodisplay düzenleyebilirsiniz.

1. Merhaba ölçüm dikey penceresinde **Düzenle**.

    ![Düzenle'yi tıklatın][6]

2. Merhaba, **grafiği Düzenle** dikey penceresinde bir zaman aralığı (saat, bugün, geçmiş veya geçen hafta) seçin veya tıklatın **özel** tooselect herhangi bir tarih aralığı hello son iki hafta. Merhaba grafik türü (çubuğu veya satırı) seçin, sonra hello kaynakları toomonitor seçin.

   > [!Note]
   > Aynı ölçü hello görüntülenebilir hello Ölçümleriyle hello aynı grafik yalnızca saat. "EDTU yüzdesi" seçeneğini belirlerseniz Örneğin, ardından yalnızca diğer ölçümleri yüzdesiyle hello ölçü seçebilirsiniz.
   >

    ![Düzenle'yi tıklatın](./media/sql-database-elastic-pool-manage-portal/edit-chart.png)

3. Daha sonra, **Tamam**'a tıklayın.

## <a name="manage-and-monitor-databases-in-an-elastic-pool"></a>Yönetme ve esnek havuzdaki veritabanları izleme

Tek tek veritabanları için olası sorun de izlenebilir.

1. Altında **esnek veritabanı izleme**, beş veritabanları için ölçümleri görüntüleyen bir grafik yoktur. Varsayılan olarak, hello grafik hello üst 5 veritabanları hello havuzunda hello ortalama eDTU kullanımı tarafından son bir saat görüntüler. Merhaba grafiği tıklatın.

    ![Esnek Havuz izleme][4]

2. Merhaba **veritabanı kaynak kullanımını** dikey penceresi görünür. Merhaba havuzunda hello veritabanı kullanımının ayrıntılı bir görünüm sağlar. Merhaba dikey pencerenin alt bölümünde hello Hello kılavuzunda kullanarak, kullanım (yukarı too5 veritabanları) hello grafikte hello havuzu toodisplay tüm veritabanları seçebilirsiniz. Tıklayarak hello grafikte görüntülenen hello ölçümleri ve zaman penceresini özelleştirebilirsiniz **grafiği Düzenle**.

    ![Veritabanı kaynak kullanımı dikey][8]

### <a name="toocustomize-hello-view"></a>toocustomize hello görünümü

1. Merhaba, **veritabanı kaynak kullanımını** dikey penceresinde tıklatın **grafiği Düzenle**.

    ![Grafiği Düzenle'yi tıklatın](./media/sql-database-elastic-pool-manage-portal/db-utilization-blade.png)

2. Merhaba, **Düzenle** grafik dikey penceresinde, bir zaman aralığı (saat sonraya veya son 24 saat) seçin veya **özel** tooselect 2 hafta toodisplay geçmiş hello farklı günde bir.

    ![Özel'i tıklatın](./media/sql-database-elastic-pool-manage-portal/editchart-date-time.png)

3. Merhaba tıklatın **karşılaştırmak veritabanı tarafından** açılır tooselect veritabanları karşılaştırıldığında farklı bir ölçüm toouse.

    ![Merhaba grafiği Düzenle](./media/sql-database-elastic-pool-manage-portal/edit-comparison-metric.png)

### <a name="tooselect-databases-toomonitor"></a>tooselect veritabanları toomonitor

Merhaba hello veritabanı listesinde **veritabanı kaynak kullanımını** dikey penceresinde bulabilirsiniz belirli veritabanları hello listesinde hello sayfaları aracılığıyla bakarak veya veritabanının hello adını yazarak. Merhaba onay kutusunu tooselect hello veritabanını kullanın.

![Veritabanlarını toomonitor arayın][7]


## <a name="add-an-alert-tooan-elastic-pool-resource"></a>Bir uyarı tooan esnek havuz kaynak ekleyin

Merhaba esnek havuz sizin ayarladığınız bir kullanım eşiği geldiğinde, toopeople veya uyarı dizeleri tooURL uç noktaları e-posta Gönder kuralları tooan esnek havuz ekleyebilirsiniz.

**bir uyarı tooany kaynak tooadd:**

1. Hello tıklatın **kaynak kullanımı** grafik tooopen hello **ölçüm** dikey penceresinde tıklatın **uyarı Ekle**ve ardından hello hello bilgileri doldurun **uyarı ekleme Kural** dikey (**kaynak** toobe hello havuzu ile çalışırken yukarı otomatik olarak ayarlanır).
2. Tür a **adı** ve **açıklama** hello uyarı tooyou ve hello alıcıları tanımlar.
3. Seçin bir **ölçüm** hello listeden tooalert istiyor.

    Merhaba grafik bir eşik seçin, ölçüm toohelp için kaynak kullanımını dinamik olarak gösterir.

4. Seçin bir **koşulu** (büyüktür, küçüktür, vs.) ve bir **eşik**.
5. Seçin bir **süresi** ölçüm hello süresini hello uyarı Tetikleyicileri önce kural sağlanmalıdır.
6. **Tamam** düğmesine tıklayın.

Daha fazla bilgi için bkz: [Azure Portalı'nda SQL veritabanı uyarıları oluşturma](sql-database-insights-alerts-portal.md).

## <a name="move-a-database-into-an-elastic-pool"></a>Bir veritabanını bir esnek havuza taşıma

Ekleyebilir veya var olan bir havuzdan veritabanları kaldırabilirsiniz. Merhaba veritabanları diğer havuzlarında olabilir. Ancak, üzerinde aynı hello olan veritabanları yalnızca ekleyebileceğiniz mantıksal sunucu.

1. Hello dikey penceresinde hello havuzunun altında **esnek veritabanları** tıklatın **havuzu yapılandırma**.

    ![Havuzu Yapılandır'ı tıklatın][1]

2. Merhaba, **havuzu yapılandırma** dikey penceresinde tıklatın **toopool eklemek**.

    ![Ekle toopool tıklatın](./media/sql-database-elastic-pool-manage-portal/add-to-pool.png)


3. Merhaba, **eklemek veritabanları** dikey penceresinde, select hello veritabanı veya veritabanları tooadd toohello havuzu. Ardından **seçin**.

    ![Veritabanlarını tooadd seçin](./media/sql-database-elastic-pool-manage-portal/add-databases-pool.png)

    Merhaba **havuzu yapılandırma** listeleri, kendi durumu çok ayarlanmış eklenen toobe seçtiğiniz veritabanı hello artık dikey**bekleyen**.

    ![Bekleyen havuzu ekleme](./media/sql-database-elastic-pool-manage-portal/pending-additions.png)

3. Merhaba, **yapılandırma havuzu dikey**, tıklatın **kaydetmek**.

    ![Kaydet’e tıklayın.](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="move-a-database-out-of-an-elastic-pool"></a>Bir veritabanını bir esnek havuz dışına taşıma

1. Merhaba, **havuzu yapılandırma** dikey penceresinde, select hello veritabanı veya veritabanları tooremove.

    ![veritabanları listeleme](./media/sql-database-elastic-pool-manage-portal/select-pools-removal.png)

2. Tıklatın **havuzundan kaldırmak**.

    ![veritabanları listeleme](./media/sql-database-elastic-pool-manage-portal/click-remove.png)

    Merhaba **havuzu yapılandırma** kendi durumu çok ayarlanmış kaldırılan toobe seçtiğiniz veritabanı listeleri hello artık dikey**bekleyen**.

    ![Önizleme veritabanı ekleme ve kaldırma](./media/sql-database-elastic-pool-manage-portal/pending-removal.png)

3. Merhaba, **yapılandırma havuzu dikey**, tıklatın **kaydetmek**.

    ![Kaydet’e tıklayın.](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="change-performance-settings-of-an-elastic-pool"></a>Bir esnek havuz performans ayarlarını değiştir

Bir esnek havuz hello kaynak kullanımını izleme gibi bazı ayarlamalar gereklidir fark edebilirsiniz. Belki de hello havuzu hello performansı veya depolama sınırları değişikliği gerekir. Büyük olasılıkla toochange hello veritabanı ayarlarını hello havuzunda istiyor. Merhaba havuzu hiçbir zaman tooget hello iyi dengeyi performans ve maliyet konumunda hello Kurulumu değiştirebilirsiniz. Bkz: [ne zaman bir esnek havuz kullanılmalıdır?](sql-database-elastic-pool.md) daha fazla bilgi için.

toochange hello edtu'ları veya depolama havuzunu ve veritabanı başına Edtu başına sınırları:

1. Açık hello **havuzu yapılandırma** dikey.

    Altında **esnek havuzu ayarlarını**, her iki kaydırıcı toochange hello havuzu ayarlarını kullanın.

    ![Esnek havuz kaynak kullanımı](./media/sql-database-elastic-pool-manage-portal/resize-pool.png)

2. Merhaba ayarını değiştirdiğinde hello görüntü hello hello değişiklik aylık maliyeti tahmini gösterir.

    ![Bir esnek havuz ve yeni aylık maliyeti güncelleştirme](./media/sql-database-elastic-pool-manage-portal/pool-change-edtu.png)

## <a name="latency-of-elastic-pool-operations"></a>Esnek havuz işlemlerinin gecikme süresi
* Veritabanı veya en büyük veritabanı başına Edtu başına Hello min Edtu'lar genellikle değiştirme 5 dakika veya daha az tamamlar.
* Merhaba Edtu havuzu başına değiştirme hello toplam hello havuzdaki tüm veritabanları tarafından kullanılan alanı miktarına bağlıdır. Değişiklikler 100 GB için ortalama 90 dakika veya daha az sürer. Örneğin, tarafından kullanılan hello toplam alanı hello havuzdaki tüm veritabanları ise 200 GB hello havuz eDTU havuzu başına değiştirmek için gecikme süresi 3 saattir hello beklenen sonra veya daha az.

## <a name="next-steps"></a>Sonraki adımlar

- bir esnek havuz olup toounderstand [SQL Database esnek havuzunu](sql-database-elastic-pool.md).
- Esnek havuzlar kullanma ile ilgili yönergeler için bkz: [esnek havuzlar için fiyat ve performans konuları](sql-database-elastic-pool.md).
- toouse esnek iş toorun Transact-SQL betikleri hello havuzdaki veritabanları herhangi bir sayıda karşı bkz [esnek iş genel bakış](sql-database-elastic-jobs-overview.md).
- herhangi bir sayıda hello havuzdaki veritabanları arasında tooquery bkz [esnek sorgu genel bakış](sql-database-elastic-query-overview.md).
- İşlemleri için herhangi bir sayıda hello havuzdaki veritabanları Bkz [esnek işlemleri](sql-database-elastic-transactions-overview.md).


<!--Image references-->
[1]: ./media/sql-database-elastic-pool-manage-portal/configure-pool.png
[2]: ./media/sql-database-elastic-pool-manage-portal/basic.png
[3]: ./media/sql-database-elastic-pool-manage-portal/basic-2.png
[4]: ./media/sql-database-elastic-pool-manage-portal/basic-3.png
[5]: ./media/sql-database-elastic-pool-manage-portal/elastic-jobs.png
[6]: ./media/sql-database-elastic-pool-manage-portal/edit-metric.png
[7]: ./media/sql-database-elastic-pool-manage-portal/select-dbs.png
[8]: ./media/sql-database-elastic-pool-manage-portal/db-utilization.png
[9]: ./media/sql-database-elastic-pool-manage-portal/metric.png
