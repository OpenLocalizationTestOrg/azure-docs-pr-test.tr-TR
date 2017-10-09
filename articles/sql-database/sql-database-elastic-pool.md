---
title: "aaaWhat esnek havuzlar misiniz? Birden çok SQL veritabanı - Azure yönetme | Microsoft Docs"
description: "Yönetmek ve birden çok SQL veritabanı - ölçeklendirme yüzlerce ve binlik - esnek havuzlarını kullanarak. Bir fiyat kaynakların gerektiğinde dağıtabilirsiniz."
keywords: "birden çok veritabanı, veritabanı kaynakları, veritabanı performansı"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: b46e7fdc-2238-4b3b-a944-8ab36c5bdb8e
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.date: 07/31/2017
ms.author: carlrab
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 2098d7817ebe1277b5c131421f23c00803ec78f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="elastic-pools-help-you-manage-and-scale-multiple-sql-databases"></a>Esnek havuz yönetmek ve birden çok SQL veritabanı ölçekleme Yardım

SQL Database esnek havuzlar, yönetme ve değişen ve tahmin edilemeyen kullanım taleplerini sahip birden çok veritabanı ölçekleme için basit ve düşük maliyetli bir çözümdür. Esnek havuzdaki veritabanları Hello tek bir Azure SQL veritabanı sunucusuna olan ve kaynak kümesi sayısı paylaşan ([esnek veritabanı işlem birimleri](sql-database-what-is-a-dtu.md) (Edtu'lar)) bir kümesi fiyatla. Azure SQL Database esnek havuzlarını performans esneklik her veritabanı için teslim ederken SaaS geliştiriciler toooptimize hello fiyat performansı düşürür bütçenin veritabanları grubu için etkinleştirin.   

> [!NOTE]
> Esnek havuzlar şu anda önizleme aşamasında oldukları Batı Hindistan dışında tüm Azure bölgelerinde genel olarak kullanılabilir (GA) durumdadır.  Bu bölgede esnek havuz GA’sı olabildiğince çabuk ortaya çıkar.
>

## <a name="what-are-sql-elastic-pools"></a>SQL esnek havuzu nelerdir? 

SaaS geliştiricileri, birden fazla veritabanından oluşan büyük ölçekli veri katmanlarının üzerinde uygulamalar oluşturur. Ortak bir uygulama düzeni tooprovision her müşteri için tek bir veritabanına ' dir. Farklı müşterilere sık sık değişen ve tahmin edilemeyen kullanım desenlerini varsa ve her tek tek veritabanı kullanıcısı zor toopredict hello kaynak gereksinimlerini ancak. Geleneksel olarak, iki seçenek vardı: 

- En yüksek kullanımı ve ödeme, üzerinden dayalı kaynakları aşırı sağlamak veya
- Eksik sağlama toosave yükselmeleri sırasında performans ve müşteri memnuniyetini hello giderleri adresindeki maliyeti. 

Esnek havuzlar veritabanları ihtiyaç duydukları gereksinim hello performans kaynakları alma sağlayarak bu sorunu çözün. Bunlar, tahmin edilebilir bir bütçe içinde basit bir kaynak ayırma mekanizması sağlar. Esnek havuzları kullanan SaaS uygulamaları için Tasarım desenleri hakkında daha fazla toolearn bkz [Azure SQL veritabanı ile çok kiracılı SaaS uygulamaları için Tasarım desenleri](sql-database-design-patterns-multi-tenancy-saas-applications.md).

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Elastic-databases-helps-SaaS-developers-tame-explosive-growth/player]
>

Esnek havuzlar etkinleştirmek hello Geliştirici toopurchase [esnek veritabanı işlem birimleri](sql-database-what-is-a-dtu.md) (Edtu'lar) birden çok veritabanları tooaccommodate öngörülemeyen noktalarla kullanım tek tek veritabanı tarafından paylaşılan bir havuz için. bir havuz eDTU gereksinimini Hello hello toplama kullanımı veritabanlarını tarafından belirlenir. Edtu kullanılabilir toohello havuzu Hello sayısı hello Geliştirici bütçe tarafından denetlenir. Merhaba Geliştirici yalnızca veritabanları toohello havuzu ekler, hello minimum ve maksimum Edtu hello veritabanları için ayarlar ve bunların bütçeye bağlı hello havuzunun hello eDTU ayarlar. Bir geliştirici tooseamlessly büyüyen bir yalın başlangıç tooa olgun işletme kendi hizmetinden havuzlarını kullanabilirsiniz gitgide artan ölçek.

Merhaba havuz tek veritabanlarını hello esneklik tooauto ölçekli parametrelerini içinde verilir. Ağır yük altında daha fazla Edtu'lar toomeet isteğe bağlı bir veritabanı kullanabilir. Yükü az olan veritabanları daha az eDTU kullanır ve yükü bulunmayan veritabanları eDTU kullanmaz. Merhaba tüm havuz için yerine tek veritabanları için kaynak sağlama, yönetim görevlerini basitleştirir. Ayrıca hello havuzu için tahmin edilebilir bir bütçe sahip. Ek Edtu'lar tooan varolan veritabanı kapalı kalma süresiyle havuzuyla eklenebilir, hello veritabanları taşınmış toobe gerekebilir dışında tooprovide hello ek işlem kaynaklarını hello yeni eDTU ayırma için. Benzer şekilde, ek eDTU’lara artık ihtiyaç yoksa bunlar mevcut bir havuzdan ne zaman isterseniz kaldırılabilir. Ve ekleyebilir veya veritabanlarını toohello havuzu çıkarın. Bir veritabanı kaynakları tahmin edilebilir bir şekilde normalden az kullanıyorsa bu veritabanını havuzdan çıkarın.

Oluşturma ve hello kullanarak bir esnek havuzunu yönetme [Azure portal](sql-database-elastic-pool-manage-portal.md), [PowerShell](sql-database-elastic-pool-manage-powershell.md), [Transact-SQL](sql-database-elastic-pool-manage-tsql.md), [C#](sql-database-elastic-pool-manage-csharp.md), ve REST API hello. 

## <a name="when-should-you-consider-a-sql-database-elastic-pool"></a>Ne zaman bir SQL Database esnek havuzunu dikkat etmeliyim?

Havuzlar, belirli kullanım düzenlerine sahip çok sayıda veritabanı bulunan durumlar için çok uygundur. Söz konusu kullanım düzeni, belirli bir veritabanı için ortalama düşük düzeyde kullanım ile nispeten nadir zamanlarda kullanımın ani olarak artması şeklindedir.

Merhaba daha fazla veritabanı, tooa havuzu Merhaba, tasarruf hale büyük ekleyebilirsiniz. Uygulama kullanımı düzeni bağlı olarak bu en az iki S3 veritabanları ile olası toosee tasarrufları gösterir.  

Merhaba aşağıdaki bölümler, anlamanıza yardım nasıl belirli koleksiyonunuz veritabanlarının bir havuzda olmaktan atarsanız tooassess. Merhaba örnekler standart havuzlarını kullanabilirsiniz ancak hello aynı ilkeler de tooBasic ve Premium havuzları geçerlidir.

### <a name="assessing-database-utilization-patterns"></a>Veritabanı kullanım modellerini değerlendirme

Merhaba aşağıdaki şekilde kadar boşta kalma zaman harcayan, ancak da düzenli olarak etkinlikle ani bir veritabanı örneği gösterilmektedir. Bu model bir havuz için uygun olan kullanım modelidir:

   ![havuz için uygun bir tek veritabanı](./media/sql-database-elastic-pool/one-database.png)

Merhaba beş dakikalık süre, DB1 yükselmeleri too90 Dtu'lar yukarı gösterilen ancak beşten küçük Dtu'lar genel ortalama kullanım değildir. Performans düzeyi S3 toorun bu iş yükü tek bir veritabanında gerekli, ancak bu hello kaynakların çoğunu kullanılmayan düşük etkinlik dönemlerde bırakır.

Bir havuzu birden çok veritabanı arasında paylaşılan kullanılmayan bu Dtu'lar toobe sağlar ve böylece hello Dtu'lar gerekli ve genel maliyeti azaltır.

Merhaba önceki örnekte üzerinde oluşturma varsayalım DB1 benzer kullanımı desenlerle ek veritabanı vardır. Merhaba sonraki iki resimde içinde dört veritabanlarının kullanımını hello ve 20 veritabanları katmanlı hello tooillustrate hello çakışmayan doğasına kullanımlarını zaman içinde aynı grafik:

   ![bir havuz için uygun kullanım modeli ile dört veritabanı](./media/sql-database-elastic-pool/four-databases.png)

  ![bir havuz için uygun kullanım modeli ile yirmi veritabanı](./media/sql-database-elastic-pool/twenty-databases.png)

Şekil önceki hello hello siyah çizgiyle tüm 20 veritabanları arasında Hello toplama DTU kullanımı gösterilmiştir. Bu hello toplama DTU kullanımı hiçbir zaman 100 Dtu'lar aşıyor ve hello 20 veritabanları bu süre boyunca 100 Edtu'lar paylaşabilirsiniz gösterir olduğunu gösterir. Bu Dtu'lar 20 x azalma ve bir 13 x fiyat karşılaştırıldığında azaltma tooplacing her S3 performans düzeyleri tek veritabanları için hello veritabanlarının sonuçlanır.

Bu örnekte, aşağıdaki nedenlerden hello için idealdir:

* Bir veritabanındaki en yüksek kullanım ile ortalama kullanım arasında büyük farklar mevcuttur.  
* Merhaba en yüksek kullanımı her veritabanı için farklı noktalarda zamanında oluşur.
* eDTU'lar birden fazla veritabanı arasında paylaşılır.

Merhaba fiyat havuzu hello havuz Edtu işlevidir. Merhaba eDTU birim fiyat bir havuz için tek bir veritabanı için hello DTU birim fiyatı büyük x 1,5 olsa **havuz Edtu pek çok veritabanı tarafından paylaşılabilir ve daha az toplam Edtu'lar gerekli**. Bu farklılıklar fiyatlandırma ve eDTU paylaşımı havuzları sağlayabilir hello fiyat tasarrufları potansiyel olarak hello temelidir.  

Merhaba aşağıdaki kuralları altın karşılaştırıldığında maliyet toousing performans düzeyleri tek veritabanları için bir havuz teslim eden toodatabase sayısı ve veritabanı kullanımı Yardım tooensure azaltılmış ilgili.

### <a name="minimum-number-of-databases"></a>En az veritabanı sayısı

Merhaba performans düzeyleri tek veritabanları için Dtu Hello toplamını birden fazla 1.5 hello havuzu için gerekli hello Edtu'lar x ise, bir esnek havuz daha uygun maliyetli olması. Kullanılabilir boyutlar için bkz. [Elastik havuzlar ve elastik veritabanları için eDTU ve depolama limitleri](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).

***Örnek***<br>
En az iki S3 veritabanı veya en az 15 S0 veritabanları için 100 eDTU havuzu toobe performans düzeyleri için tek veritabanlarını kullanmaktan daha düşük maliyetli gereklidir.

### <a name="maximum-number-of-concurrently-peaking-databases"></a>Eşzamanlı olarak en üst seviyeye çıkan en fazla veritabanı sayısı

Edtu paylaşarak, bir havuzdaki tüm veritabanları aynı anda toohello sınırı kullanılabilir yukarı Edtu'lar performans düzeyleri için tek veritabanlarını kullanırken kullanabilirsiniz. eşzamanlı olarak en yüksek daha az veritabanları Merhaba, hello alt hello havuz eDTU ayarlama ve daha fazla uygun maliyetli hello havuzu hale hello olabilir. Genel olarak, değil fazlasını hello havuzunda hello veritabanlarının 2/3 (veya % 67) aynı anda tootheir eDTU en yüksek sınırlayın.

***Örnek***<br>
tooreduce maliyetleri 200 eDTU havuzu üç S3 veritabanları için en fazla iki bu veritabanları aynı anda kendi kullanımı en yüksek. Aksi takdirde, ikiden fazla bu dört S3 veritabanları aynı anda en yüksek, hello havuzu 200 edtu'ları fazla boyuta sahip toobe toomore gerekir. Merhaba havuzu 200 Edtu'den yeniden boyutlandırılan toomore ise, daha fazla S3 veritabanı eklenen toobe gerekir toohello havuzu tookeep maliyetleri tek veritabanları için performans düzeyleri değerinden daha düşük.

Bu örnek hello havuzunda diğer veritabanlarının kullanımını dikkate almaz unutmayın. Tüm veritabanları, bazı kullanımı belirli bir anda zamanında varsa, daha sonra 2/3 değerinden (veya % 67) hello veritabanlarının aynı anda en yüksek.

### <a name="dtu-utilization-per-database"></a>Veritabanı başına DTU kullanımı
Merhaba en yüksek ve ortalama kullanım veritabanı arasında büyük farklar düşük kullanımı uzun süren nokta ve kısa yüksek kullanım dönemlerini gösterir. Bu kullanım modeli, veritabanları arasında kaynakların paylaşılması için idealdir. Bir veritabanının en yüksek kullanımı ortalama kullanımından 1,5 kat fazla olduğunda, veritabanı havuz için düşünülmelidir.

***Örnek***<br>
Too100 Dtu'lar tarafı ve ortalama 67 Dtu'lar'ı kullanan bir S3 veritabanı ya da bir havuz Edtu paylaşmak için iyi bir aday küçük. Alternatif olarak, too20 Dtu'lar tarafı ve ortalama 13 Dtu'lar'ı kullanan bir S1 veritabanı ya da daha küçük bir havuz için iyi bir adaydır.

## <a name="how-do-i-choose-hello-correct-pool-size"></a>Merhaba doğru havuz boyutu nasıl seçer?

bir havuz için en iyi boyutu Hello hello toplama Edtu ve depolama kaynaklarını hello havuzdaki tüm veritabanları için gereken bağlıdır. Bu, hello hello aşağıdakilerden büyük belirleme içerir:

* Merhaba havuzdaki tüm veritabanları tarafından kullanılan en fazla Dtu'lar.
* Merhaba havuzdaki tüm veritabanları tarafından kullanılan en fazla depolama bayt sayısı.

Kullanılabilir boyutlar için bkz. [Elastik havuzlar ve elastik veritabanları için eDTU ve depolama limitleri](#what-are-the-resource-limits-for-elastic-pools).

SQL veritabanı otomatik olarak varolan bir SQL veritabanı sunucusuna veritabanlarında hello geçmiş kaynak kullanımını değerlendirir ve hello Azure portal hello uygun havuzu yapılandırması önerir. Toplama toohello önerileri hello eDTU kullanımı hello sunucudaki veritabanları için özel bir grup için yerleşik bir deneyim tahmin eder. Bu, bir "" çözümlemeleri toodo etkileşimli olarak veritabanları toohello havuzu ekleme ve tooget kaynak kullanım analizi kaldırarak ve Değişikliklerinizi kaydetmeden önce öneriler boyutlandırma sağlar. Nasıl yapılır konuları için bkz. [Elastik havuzlarını izleme, yönetme ve boyutlandırma](sql-database-elastic-pool-manage-portal.md).

Yeri tooling kullanamazsınız durumlarda hello aşağıdaki adım adım bir havuzu tek veritabanlarını daha düşük maliyetli olup olmadığını tahmin etmenize yardımcı olabilir:

1. Merhaba havuzu için aşağıdaki gibi gerekli hello Edtu'lar tahmin edersiniz:

   MAKS(<*Toplam veritabanı sayısı* X *Veritabanı başına ortalama DTU kullanımı*>,<br>
   <*Eşzamanlı olarak en üst seviyeye çıkan veritabanı sayısı* X *Veritabanı başına en yüksek DTU kullanımı*)
2. Merhaba hello havuzundaki tüm hello veritabanları için gerekli olan bayt sayısını ekleyerek Hello havuzu için gerekli hello depolama alanı tahmin edin. Ardından bu depolama alanı miktarını sağlar hello eDTU havuz boyutunu belirler. eDTU havuz boyutunu temel alan havuz depolama limitleri için bkz. [Elastik havuzlar ve elastik veritabanları için eDTU ve depolama limitleri](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).
3. Adım 1 ve 2. adım Hello hello eDTU tahminleri büyük alın.
4. Merhaba bkz [SQL veritabanı fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/sql-database/) ve hello en küçük eDTU havuzu boyutu Bul hello tahmin adım 3 büyüktür.
5. Tek veritabanları için hello uygun performans düzeylerini kullanma adım 5 toohello fiyatından Hello havuzu fiyat karşılaştırın.

### <a name="changing-elastic-pool-resources"></a>Esnek havuz kaynakları değiştirme

Artırın veya hello kaynakları kullanılabilir tooan esnek havuz kaynak gereksinimlerine göre azaltın.

* Veritabanı veya en büyük veritabanı başına Edtu başına Hello min Edtu'lar genellikle değiştirme 5 dakika veya daha az tamamlar.
* Merhaba Edtu havuzu başına değiştirme hello toplam hello havuzdaki tüm veritabanları tarafından kullanılan alanı miktarına bağlıdır. Değişiklikler 100 GB için ortalama 90 dakika veya daha az sürer. Örneğin, tarafından kullanılan hello toplam alanı hello havuzdaki tüm veritabanları ise 200 GB hello havuz eDTU havuzu başına değiştirmek için gecikme süresi 3 saattir hello beklenen sonra veya daha az.

## <a name="what-are-hello-resource-limits-for-elastic-pools"></a>Esnek havuzlar için hello kaynak sınırları nelerdir?

Aşağıdaki tablolar hello esnek havuzlar hello kaynak sınırları açıklanmaktadır.  Esnek havuzlar bulunan tek veritabanlarını Hello kaynak sınırları genellikle hello havuzları dışında tek veritabanları aynıdır Dtu'lar ve hello hizmet katmanına bağlı olduğunu unutmayın.  Örneğin, en fazla eş zamanlı çalışanların S2 veritabanını hello 120 çalışanları olur.  Bu nedenle, hello en fazla eş zamanlı çalışanlar, standart havuzdaki bir veritabanı için ise ayrıca 120 çalışanları hello hello havuzunda veritabanı başına maksimum DTU olduğundan (Bu eşdeğer tooS2) 50 Dtu'lar.

[!INCLUDE [SQL DB service tiers table for elastic pools](../../includes/sql-database-service-tiers-table-elastic-pools.md)]

Tüm bir esnek havuz Dtu kullandıysanız, her veritabanı hello havuzundaki kaynakları tooprocess sorguları eşit miktarda alır.  Merhaba SQL veritabanı hizmetinin kaynak eşitliği işlem süresi eşit dilimleri sağlayarak veritabanları arasında paylaşımı sağlar. Esnek havuz kaynak eşitliği paylaşımı ayrıca tooany hello veritabanı başına minimum DTU tooa sıfır olmayan bir değer ayarlandığında, aksi takdirde tooeach veritabanı garanti kaynak miktarıdır.

### <a name="database-properties-for-pooled-databases"></a>Havuza alınmış veritabanları için veritabanı özellikleri

Aşağıdaki tablonun hello havuza alınmış veritabanları için hello özellikleri açıklar.

| Özellik | Açıklama |
|:--- |:--- |
| Veritabanı başına Maks. eDTU |Merhaba maksimum hello havuzunda diğer veritabanları tarafından kullanılabilir kullanımını temel alan varsa, hello havuzunda herhangi bir veritabanı, kullanabilecek Edtu sayısı.  Veritabanı başına en fazla eDTU, veritabanı için kaynak garantisi anlamına gelmez.  Bu ayar hello havuzu tooall veritabanlarında uygulanan genel bir ayardır. Veritabanı başına maksimum Edtu yeterince toohandle yükselmeleri veritabanı kullanımı ayarlayın. Merhaba havuzu genellikle veritabanları için sıcak ve soğuk kullanım desenlerini varsayar beri dereceye fazla, burada tüm veritabanlarını değil aynı anda peaking beklenir. Örneğin, veritabanı başına en yüksek kullanımı hello 20 Edtu ve yalnızca % 20'hello havuzunda hello 100 veritabanlarının hello en yoğun varsayalım aynı anda.  Veritabanı başına maksimum Hello eDTU too20 Edtu'lar ayarlarsanız, ardından bunu makul tooovercommit hello 5 kez ve kümesi hello Edtu havuzu too400 başına tarafından havuzudur. |
| Veritabanı başına Min. eDTU |Merhaba minimum hello havuzunda herhangi bir veritabanı garanti Edtu sayısı.  Bu ayar hello havuzu tooall veritabanlarında uygulanan genel bir ayardır. Veritabanı başına minimum eDTU Hello too0 ayarlanabilir ve ayrıca hello varsayılan değerdir. Bu özellik 0 ile Merhaba ortalama eDTU kullanımı veritabanı başına arasında tooanywhere ayarlanır. Merhaba ürün hello havuzu ve veritabanı başına hello min Edtu veritabanlarında hello sayısının hello Edtu havuzu başına aşamaz.  Örneğin, 20 veritabanları havuzu varsa ve veritabanı başına eDTU minimum hello too10 Edtu'lar ayarlayın, sonra hello Edtu havuzu başına en az 200 Edtu kadar büyük olmalıdır. |
| Veritabanı başına maks. veri depolama alanı |Merhaba maksimum depolama havuzunda bir veritabanı için. Veritabanı depolama sınırlı toohello kalan havuzu depolama alanı ve veritabanı başına en fazla depolama daha küçük olacak şekilde havuza alınmış veritabanları havuzu depolama paylaşır. Veritabanı başına en fazla depolama hello veri dosyalarının maksimum boyutunu toohello başvuruyor ve günlük dosyaları tarafından kullanılan hello alanı içermez. |
|||

## <a name="using-other-sql-database-features-with-elastic-pools"></a>Esnek havuzları ile diğer SQL veritabanı özelliklerini kullanma

### <a name="elastic-jobs-and-elastic-pools"></a>Esnek işler ve esnek havuzlar

Bir havuz kullanılarak **[esnek işlerde](sql-database-elastic-jobs-overview.md)** betik çalıştırma yoluyla yönetim görevleri kolaylaştırılır. Elastik iş, çok sayıda veritabanından kaynaklanan sorunların çoğunu ortadan kaldırır. toobegin, bkz: [esnek işlerine Başlarken](sql-database-elastic-jobs-getting-started.md).

Birden fazla veritabanıyla çalışmak için kullanılabilen diğer veritabanı araçları hakkında daha fazla bilgi için bkz. [Azure SQL Veritabanı ile ölçek genişletme](sql-database-elastic-scale-introduction.md).

### <a name="business-continuity-options-for-databases-in-an-elastic-pool"></a>Esnek havuzdaki veritabanları için iş sürekliliği seçenekleri
Havuza veritabanları genellikle destek hello aynı [iş sürekliliği özellikleri](sql-database-business-continuity.md) kullanılabilir toosingle veritabanları olan.

- **Geri yükleme noktası**: noktası içinde zaman geri yükleme zamanında havuzu tooa içinde belirli bir noktaya otomatik veritabanı yedeklemeleri toorecover bir veritabanı kullanır. Bkz. [Belirli Bir Noktaya Geri Yükleme](sql-database-recovery-using-backups.md#point-in-time-restore)

- **Coğrafi geri yükleme**: coğrafi geri yükleme, bir veritabanı hello veritabanı barındırıldığı hello bölgede bir olay nedeniyle kullanılamadığında hello varsayılan kurtarma seçeneği sağlar. Bkz: [bir Azure SQL Database veya yük devretme tooa ikincil geri yükleme](sql-database-disaster-recovery.md)

- **Aktif coğrafi çoğaltma**: coğrafi geri yükleme sunabileceğiniz çok daha agresif kurtarma gereksinimlerine sahip uygulamalar için yapılandırma [aktif coğrafi çoğaltma](sql-database-geo-replication-overview.md).

## <a name="manage-sql-database-elastic-pools-using-hello-azure-portal"></a>Hello Azure portal kullanarak SQL Database esnek havuzlarını yönetme

### <a name="creating-a-new-sql-database-elastic-pool-using-hello-azure-portal"></a>Hello Azure portal kullanarak yeni bir SQL Database esnek havuzunu oluşturma

Hello Azure portalında bir esnek havuz oluşturmanın iki yolu vardır. İstediğiniz ya da bir öneri hello hizmetinden başlayın hello havuz kurulumunu biliyorsanız sıfırdan yapabilirsiniz. SQL veritabanı maliyet açısından daha verimli kullanım telemetri veritabanlarınız için geçmiş hello temel alarak için ise, bir esnek havuz Kurulumu önerdiği yerleşik zekaya sahiptir. 

Mevcut bir esnek havuz oluşturma **server** dikey penceresinde hello portal hello en kolay yolu toomove varolan veritabanlarına bir esnek havuz değil. Arayarak bir esnek havuz oluşturabilirsiniz **SQL esnek havuzu** hello içinde **Market** veya tıklatarak **+ Ekle** hello içinde **SQL esnek havuzu**dikey göz atın. Mümkün toospecify yeni veya var olan bir sunucu iş akışı sağlama bu havuzu üzerinden var.

> [!NOTE]
> Bir sunucuda birden çok havuz oluşturabilirsiniz, ancak hello farklı sunuculara ait veritabanlarını ekleyemezsiniz aynı havuzu.
>  

Merhaba havuzun fiyatlandırma katmanı hello kullanılabilir toohello elastics hello havuzu ve hello maksimum sayısını Edtu (Maks eDTU) ve depolama (GB) kullanılabilir tooeach veritabanı özellikleri belirler. Ayrıntılar için bkz [hizmet katmanları](#edtu-and-storage-limits-for-elastic-pools).

Merhaba havuzu için toochange hello fiyatlandırma Katmanı'nı tıklatın **fiyatlandırma katmanı**, fiyatlandırma katmanı ve ardından hello tıklatın **seçin**.

> [!IMPORTANT]
> Merhaba fiyatlandırma katmanı seçin ve değişikliklerinizi tıklatılarak sonra **Tamam** hello son adımda fiyatlandırma katmanı hello havuzunun mümkün toochange hello olmayacaktır. toochange var olan bir esnek havuz için fiyatlandırma katmanı Merhaba, hello istenen fiyatlandırma katmanında bir esnek havuz oluşturun ve hello veritabanları toothis yeni havuzunu geçirin.
>

Merhaba veritabanları ile çalışırken yeterli geçmiş kullanımı telemetri varsa, hello **tahmini eDTU ve GB kullanımı** grafik ve hello **gerçek eDTU kullanımı** çubuk grafik güncelleştirme toohelp, yaptığınız yapılandırma kararlar. Ayrıca, hello hizmeti, bir öneri iletisi toohelp verebilir, boyutlandırmanıza hello havuzu.

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

### <a name="manage-and-monitor-an-elastic-pool"></a>Yönetme ve bir esnek Havuz izleme

Hello Azure portal'da, esnek havuz ve hello veritabanları aynı havuz içindeki hello kullanımını izleyebilirsiniz. Ayrıca bir değişiklik kümesini tooyour esnek havuzu yapmak ve tüm değişiklikler hello aynı gönderme zamanı. Bu değişiklikler ekleyerek veya veritabanları kaldırma, esnek havuz ayarlarınızı değiştirme veya veritabanı ayarlarını değiştirerek içerir.

Grafiği aşağıdaki hello bir örnek esnek havuz gösterir. Merhaba görünümü içerir:

*  Kaynak kullanımını hello esnek havuz ve hello havuzunda kapsanan hello veritabanlarını izleme grafikleri.
*  Merhaba **yapılandırma** havuzu düğmesi toomake toohello esnek havuz değiştirir.
*  Merhaba **veritabanı oluşturma** bir veritabanı oluşturur düğmesi ve toohello geçerli esnek havuz ekler.
*  Yardımcı esnek işler, listedeki tüm veritabanlarında Transact SQL komut dosyaları çalıştırarak veritabanları çok sayıda yönetin.

![Havuz görünümü](./media/sql-database-elastic-pool-manage-portal/basic.png)

Kaynak kullanımı tooa belirli havuzu toosee gidebilirsiniz. Varsayılan olarak, hello hello son saat için yapılandırılmış tooshow depolama ve eDTU kullanımı havuzudur. Merhaba grafik yapılandırılmış tooshow farklı ölçümleri çeşitli zaman pencereleri olabilir. Merhaba tıklatın **kaynak kullanımı** altında grafik **esnek Havuz izleme** tooshow hello ayrıntılı görünümünü belirtilen ölçümleri hello belirtilen zaman penceresi.

![Esnek Havuz izleme](./media/sql-database-elastic-pool-manage-portal/basic-2.png)

![Ölçüm dikey penceresi](./media/sql-database-elastic-pool-manage-portal/metric.png)

### <a name="toocustomize-hello-chart-display"></a>toocustomize hello grafik görüntüleme

CPU yüzdesi, veri g/ç yüzdesi ve kullanılan günlük GÇ yüzdesi gibi diğer ölçümleri hello grafik ve hello ölçüm dikey penceresi toodisplay düzenleyebilirsiniz.

![Düzenle'yi tıklatın](./media/sql-database-elastic-pool-manage-portal/edit-metric.png)

Merhaba üzerinde **grafiği Düzenle** formu, bir zaman aralığı (saat, bugün, geçmiş veya geçen hafta) seçin veya tıklatın **özel** tooselect herhangi bir tarih aralığı hello son iki hafta. Çubuk veya çizgi grafiği arasında seçim yapın ve ardından hello kaynakları toomonitor seçin.

> [!Note]
> Aynı ölçü hello görüntülenebilir hello Ölçümleriyle hello aynı grafik yalnızca saat. "EDTU yüzdesi" seçeneğini belirlerseniz Örneğin, ardından yalnızca diğer ölçümleri yüzdesiyle hello ölçü seçebilirsiniz.
>

[Düzenle'yi tıklatın](./media/sql-database-elastic-pool-manage-portal/edit-chart.png)

### <a name="manage-and-monitor-databases-in-an-elastic-pool"></a>Yönetme ve esnek havuzdaki veritabanları izleme

Tek tek veritabanları için olası sorun de izlenebilir. Altında **esnek veritabanı izleme**, beş veritabanları için ölçümleri görüntüleyen bir grafik yoktur. Varsayılan olarak, hello grafik hello üst 5 veritabanları hello havuzunda hello ortalama eDTU kullanımı tarafından son bir saat görüntüler. 

![Esnek Havuz izleme](./media/sql-database-elastic-pool-manage-portal/basic-3.png)

Merhaba tıklatın **hello son bir saat için veritabanları için eDTU kullanımı** altında **esnek veritabanı izleme**. Bu açılır **veritabanı kaynak kullanımı** ve hello havuzunda hello veritabanı kullanımının ayrıntılı bir görünüm sağlar. Merhaba dikey pencerenin alt bölümünde hello Hello kılavuzunda kullanarak, kullanım (yukarı too5 veritabanları) hello grafikte hello havuzu toodisplay tüm veritabanları seçebilirsiniz. Tıklayarak hello grafikte görüntülenen hello ölçümleri ve zaman penceresini özelleştirebilirsiniz **grafiği Düzenle**.

![Veritabanı kaynak kullanımı dikey](./media/sql-database-elastic-pool-manage-portal/db-utilization.png)

### <a name="toocustomize-hello-view"></a>toocustomize hello görünümü

Merhaba grafik tooselect bir zaman aralığı (saat sonraya veya son 24 saat) düzenleyebilir veya tıklatın **özel** tooselect 2 hafta toodisplay geçmiş hello farklı günde bir.

![Grafiği Düzenle'yi tıklatın](./media/sql-database-elastic-pool-manage-portal/db-utilization-blade.png)

![Özel'i tıklatın](./media/sql-database-elastic-pool-manage-portal/editchart-date-time.png)

Merhaba tıklatarak **karşılaştırmak veritabanı tarafından** açılır tooselect veritabanları karşılaştırıldığında farklı bir ölçüm toouse.

![Merhaba grafiği Düzenle](./media/sql-database-elastic-pool-manage-portal/edit-comparison-metric.png)

### <a name="tooselect-databases-toomonitor"></a>tooselect veritabanları toomonitor

Merhaba hello veritabanı listesinde **veritabanı kaynak kullanımını** dikey penceresinde bulabilirsiniz belirli veritabanları hello listesinde hello sayfaları aracılığıyla bakarak veya veritabanının hello adını yazarak. Merhaba onay kutusunu tooselect hello veritabanını kullanın.

![Veritabanlarını toomonitor arayın](./media/sql-database-elastic-pool-manage-portal/select-dbs.png)


### <a name="add-an-alert-tooan-elastic-pool-resource"></a>Bir uyarı tooan esnek havuz kaynak ekleyin

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

### <a name="move-a-database-into-an-elastic-pool"></a>Bir veritabanını bir esnek havuza taşıma

Ekleyebilir veya var olan bir havuzdan veritabanları kaldırabilirsiniz. Merhaba veritabanları diğer havuzlarında olabilir. Ancak, üzerinde aynı hello olan veritabanları yalnızca ekleyebileceğiniz mantıksal sunucu.

 ![Havuzu Yapılandır'ı tıklatın](./media/sql-database-elastic-pool-manage-portal/configure-pool.png)

![Ekle toopool tıklatın](./media/sql-database-elastic-pool-manage-portal/add-to-pool.png)

![Veritabanlarını tooadd seçin](./media/sql-database-elastic-pool-manage-portal/add-databases-pool.png)

![Bekleyen havuzu ekleme](./media/sql-database-elastic-pool-manage-portal/pending-additions.png)

![Kaydet’e tıklayın.](./media/sql-database-elastic-pool-manage-portal/click-save.png)

### <a name="move-a-database-out-of-an-elastic-pool"></a>Bir veritabanını bir esnek havuz dışına taşıma

![veritabanları listeleme](./media/sql-database-elastic-pool-manage-portal/select-pools-removal.png)

![veritabanları listeleme](./media/sql-database-elastic-pool-manage-portal/click-remove.png)

![Önizleme veritabanı ekleme ve kaldırma](./media/sql-database-elastic-pool-manage-portal/pending-removal.png)

![Kaydet’e tıklayın.](./media/sql-database-elastic-pool-manage-portal/click-save.png)

### <a name="change-performance-settings-of-an-elastic-pool"></a>Bir esnek havuz performans ayarlarını değiştir

Bir esnek havuz hello kaynak kullanımını izleme gibi bazı ayarlamalar gereklidir fark edebilirsiniz. Belki de hello havuzu hello performansı veya depolama sınırları değişikliği gerekir. Büyük olasılıkla toochange hello veritabanı ayarlarını hello havuzunda istiyor. Merhaba havuzu hiçbir zaman tooget hello iyi dengeyi performans ve maliyet konumunda hello Kurulumu değiştirebilirsiniz. Bkz: [ne zaman bir esnek havuz kullanılmalıdır?](sql-database-elastic-pool.md) daha fazla bilgi için.

toochange hello edtu'ları veya depolama havuzunu ve veritabanı başına Edtu başına sınırları:

![Esnek havuz kaynak kullanımı](./media/sql-database-elastic-pool-manage-portal/resize-pool.png)

![Bir esnek havuz ve yeni aylık maliyeti güncelleştirme](./media/sql-database-elastic-pool-manage-portal/pool-change-edtu.png)

## <a name="manage-sql-database-elastic-pools-using-powershell"></a>PowerShell kullanarak SQL Database esnek havuzlarını yönetme

toocreate ve SQL Database esnek havuzlarını Azure PowerShell ile yönetme, PowerShell cmdlet'leri aşağıdaki hello kullanın. PowerShell yükseltme veya tooinstall gerekir, bkz: [yükleme Azure PowerShell Modülü](/powershell/azure/install-azurerm-ps). toocreate ve veritabanları, sunucuları ve güvenlik duvarı kuralları, bkz: yönetmek [oluşturma ve Azure SQL veritabanı sunucularının ve PowerShell kullanarak veritabanlarını](sql-database-servers-databases.md#manage-azure-sql-servers-databases-and-firewalls-using-powershell). 

> [!TIP]
> PowerShell örnek komut dosyaları için bkz: [esnek havuzlar oluşturmak ve PowerShell kullanarak havuz dışında havuzları arasında veritabanlarını taşımak](scripts/sql-database-move-database-between-pools-powershell.md) ve [kullanım PowerShell toomonitor ve ölçek SQL esnek havuzu Azure SQL veritabanı](scripts/sql-database-monitor-and-scale-pool-powershell.md).
>

| Cmdlet | Açıklama |
| --- | --- |
|[Yeni-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool)|Esnek veritabanı havuzu bir mantıksal SQL sunucusu üzerinde oluşturur.|
|[Get-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/get-azurermsqlelasticpool)|Mantıksal bir SQL Server'da esnek havuzlar ve özellik değerlerini alır.|
|[Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool)|Esnek veritabanı havuzu mantıksal SQL Server'da özelliklerini değiştirir.|
|[Remove-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/remove-azurermsqlelasticpool)|Esnek veritabanı havuzu mantıksal SQL Server'da siler.|
|[Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity)|Mantıksal SQL Server'da bir esnek havuz işlemlerinin Hello durumunu alır.|
|[New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase)|Yeni bir veritabanı var olan bir havuzu veya tek bir veritabanı oluşturur. |
|[Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase)|Bir veya daha fazla veritabanı alır.|
|[Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqldatabase)|Bir veritabanı özelliklerini ayarlar ya da var olan bir veritabanı içine, dışı veya esnek havuzlar arasında taşır.|
|[Remove-AzureRmSqlDatabase](/powershell/module/azurerm.sql/remove-azurermsqldatabase)|Bir veritabanı kaldırır.|

> [!TIP]
> Esnek havuzdaki birçok veritabanı oluşturulmasını hello portalı veya aynı anda yalnızca tek bir veritabanı oluşturabilirsiniz PowerShell cmdlet'lerini kullanarak tamamlanınca zaman alabilir. bir esnek havuz tooautomate oluşturma bkz [CreateOrUpdateElasticPoolAndPopulate](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).
>

## <a name="manage-sql-database-elastic-pools-using-hello-azure-cli"></a>SQL Database esnek havuzlarını Hello Azure CLI kullanarak yönetme

toocreate ve SQL Database esnek havuzlarını hello ile yönetme [Azure CLI](/cli/azure/overview), hello aşağıdaki kullanın [Azure CLI SQL veritabanı](/cli/azure/sql/db) komutları. Kullanım hello [bulut Kabuk](/azure/cloud-shell/overview) tarayıcınızda toorun hello CLI veya [yükleme](/cli/azure/install-azure-cli) macOS, Linux veya Windows üzerinde. 

> [!TIP]
> Azure CLI örnek komut dosyaları için bkz: [kullanım CLI toomove SQL esnek havuzu Azure SQL veritabanında](scripts/sql-database-move-database-between-pools-cli.md) ve [kullanım Azure CLI tooscale Azure SQL veritabanındaki bir SQL esnek havuzu](scripts/sql-database-scale-pool-cli.md).
>

| Cmdlet | Açıklama |
| --- | --- |
|[az sql esnek havuzu oluşturma](/cli/azure/sql/elastic-pool#create)|Bir esnek havuz oluşturur.|
|[az sql esnek havuzu listesi](/cli/azure/sql/elastic-pool#list)|Bir sunucu esnek havuzlar listesini döndürür.|
|[az sql esnek havuzu listesi-dbs](/cli/azure/sql/elastic-pool#list-dbs)|Bir esnek havuz veritabanlarının bir listesini döndürür.|
|[az sql esnek havuzu listesi-sürümleri](/cli/azure/sql/elastic-pool#list-editions)|Ayrıca, depolama sınırları, kullanılabilir havuz DTU ayarlarını bulundurur ve veritabanı ayarlarını başına. Sipariş tooreduce ayrıntı, ek depolama sınırları ve veritabanı başına ayarlar varsayılan olarak gizlidir.|
|[az sql esnek havuzu güncelleştirme](/cli/azure/sql/elastic-pool#update)|Bir esnek havuz güncelleştirir.|
|[az sql esnek havuzu silme](/cli/azure/sql/elastic-pool#delete)|Merhaba esnek havuz siler.|

## <a name="manage-sql-database-elastic-pools-using-transact-sql"></a>Transact-SQL kullanarak SQL Database esnek havuzlarını yönetme

içinde var olan esnek havuzlar veya Transact-SQL ile bir SQL Database esnek havuzunu tooreturn bilgilerini toocreate ve taşıma veritabanları T-SQL komutlarıyla aşağıdaki hello kullanın. Hello Azure portal kullanarak bu komutlar gönderebilirsiniz [SQL Server Management Studio](/sql/ssms/use-sql-server-management-studio), [Visual Studio Code](https://code.visualstudio.com/docs), veya tooan Azure SQL veritabanı sunucusuna bağlanmak ve Transact-SQL geçirmek başka bir programı komutları. toocreate ve veritabanları, sunucuları ve güvenlik duvarı kuralları, bkz: yönetmek [oluşturma ve Azure SQL veritabanı sunucularının ve Transact-SQL kullanarak veritabanlarını](sql-database-servers-databases.md#manage-azure-sql-servers-databases-and-firewalls-using-transact-sql).

> [!IMPORTANT]
> Oluşturmak, güncelleştirmek veya Transact-SQL kullanarak bir Azure SQL Database esnek havuzunu silmek olamaz. Ekleyebilir veya bir esnek havuzdan veritabanı kaldırma ve var olan esnek havuzları hakkında Dmv'leri tooreturn bilgileri kullanabilirsiniz.
>

| Komut | Açıklama |
| --- | --- |
|[Veritabanı (Azure SQL veritabanı) oluşturma](/sql/t-sql/statements/create-database-azure-sql-database)|Yeni bir veritabanı var olan bir havuzu veya tek bir veritabanı oluşturur. Bağlı toohello ana veritabanı toocreate yeni bir veritabanı olmalıdır.|
| [ALTER DATABASE (Azure SQL veritabanı)](/sql/t-sql/statements/alter-database-azure-sql-database) |Bir veritabanı içine, dışı veya esnek havuzlar arasında taşıyın.|
|[VERİTABANINI (Transact-SQL)](/sql/t-sql/statements/drop-database-transact-sql)|Bir veritabanını siler.|
|[sys.elastic_pool_resource_stats (Azure SQL veritabanı)](/sql/relational-databases/system-catalog-views/sys-elastic-pool-resource-stats-azure-sql-database)|Kaynak kullanım istatistikleri tüm hello esnek veritabanı havuzları için bir mantıksal sunucu döndürür. Her esnek veritabanı havuzu için 15 penceresi (dakika başına dört satır) bildirdiği saniyede için bir satır yok. Bu CPU, IO, günlük, depolama alanı tüketimi ve eşzamanlı istek/oturum kullanımı hello havuzdaki tüm veritabanları tarafından içerir.|
|[sys.database_service_objectives (Azure SQL veritabanı)](/sql/relational-databases/system-catalog-views/sys-database-service-objectives-azure-sql-database)|Döndürür edition (hizmet katmanı), hizmet hedefi (fiyatlandırma katmanı) ve esnek havuz adı, varsa Azure SQL veritabanına veya Azure SQL Data Warehouse için hello. Azure SQL Database sunucusu ana veritabanında toohello oturum açmış, bilgiler tüm veritabanlarını döndürür. Azure SQL Data Warehouse için bağlı toohello ana veritabanı olmalıdır.|

## <a name="manage-sql-database-elastic-pools-using-hello-rest-api"></a>SQL Database esnek havuzlarını Hello REST API kullanarak yönetme

toocreate ve SQL Database esnek havuzlar hello REST API kullanarak yönetmek için bkz: [Azure SQL Database REST API'sini](/rest/api/sql/).

## <a name="next-steps"></a>Sonraki adımlar

* Video için bkz: [Microsoft Virtual Academy video indirmelere Azure SQL Database esnek özellikleri hakkında](https://mva.microsoft.com/training-courses/elastic-database-capabilities-with-azure-sql-db-16554)
* Esnek havuzları kullanan SaaS uygulamaları için Tasarım desenleri hakkında daha fazla toolearn bkz [Azure SQL veritabanı ile çok kiracılı SaaS uygulamaları için Tasarım desenleri](sql-database-design-patterns-multi-tenancy-saas-applications.md).
* Esnek havuzları kullanan SaaS öğretici için bkz: [giriş toohello Wingtip SaaS uygulamasına](sql-database-wtp-overview.md).
