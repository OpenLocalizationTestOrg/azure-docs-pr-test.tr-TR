---
title: "çok kiracılı SaaS uygulamaları ve Azure SQL veritabanı için aaaDesign desenleri | Microsoft Docs"
description: "Bu makalede hello gereksinimleri açıklanır ve bulut ortamında çalışan birden çok Kiracı veritabanı uygulamaları ortak veri mimarisi desenlerini tooconsider gerekir ve bu modellerle ilişkili çeşitli bileşim hello. Ayrıca, Azure SQL Database, kendi esnek havuzlar ve esnek araçlar ile nasıl yardımcı bu gereksinimlere ödün şekilde açıklar."
keywords: 
services: sql-database
documentationcenter: 
author: srinia
manager: jhubbard
editor: 
ms.assetid: 1dd20c6b-ddbb-40ef-ad34-609d398d008a
ms.service: sql-database
ms.custom: scale out apps
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sqldb-design
ms.date: 02/01/2017
ms.author: srinia
ms.openlocfilehash: a4b58935b08cb78792e65a675d680de708b709fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="design-patterns-for-multi-tenant-saas-applications-and-azure-sql-database"></a>Tasarım desenleri çok kiracılı SaaS uygulamaları ve Azure SQL veritabanı
Bu makalede, bulut ortamında çalışan bir hizmet (SaaS) veritabanı uygulamaları olarak hello gereksinimleri ve çok kiracılı yazılım ortak veri mimarisi desenlerini hakkında öğrenebilirsiniz. Ayrıca, tooconsider gerekir ve dengelemeler farklı tasarım desenleri hello hello faktörleri anlatılmaktadır. Esnek havuzlar ve esnek araçları Azure SQL veritabanı'nda, diğer hedefleri ödün vermeden belirli gereksinimlerinizi karşılayacak yardımcı olabilir.

Geliştiriciler bazen kiralama modelleri için çok kiracılı uygulamalara hello veri katmanlarını tasarlarken, uzun vadeli en iyi ilgi alanlarına göre çalışan seçimleri yapın. Başlangıçta, en az bir geliştirici geliştirme ve Kiracı yalıtımını veya hello ölçeklenebilirlik uygulamanın daha önemli olarak bulut hizmeti sağlayıcısı maliyetlerini kolaylığı bakışını. Bu seçimi daha sonra toocustomer memnuniyet sorunları ve pahalı indirmelere-düzeltme açabilir.

Çok kiracılı uygulama bulut ortamında bulunan bir uygulamasıdır ve aynı Hizmetleri toohundreds ya da kimin etmeyin paylaşma veya diğer kişilerin verileri görmek kiracılar binlerce kümesidir hello sağlar. Bulut tarafından barındırılan bir ortamda Hizmetleri tootenants sağlayan bir SaaS uygulaması örneğidir.

## <a name="multi-tenant-applications"></a>Çok kiracılı uygulamalar
Çok kiracılı uygulamalara veri ve iş yükü kolayca bölümlenebilir. Bir kiracı hello sınırlar içinde en çok istekte gerçekleştirildiği için verileri ve iş yükü, örneğin, Kiracı bölümlere bölüm. Bu özellik hello veri ve hello iş yükü devredilen ve bu makalede açıklanan hello uygulama düzenleri korur.

Geliştiricilerin bu tür bir uygulama hello tüm yelpazesini dahil olmak üzere, bulut tabanlı uygulamalar arasında kullanın:

* SaaS uygulamaları olarak geçirileceğini toohello olan iş ortağı veritabanı uygulamaları bulut
* Plan hello hello buluttan oluşturulmuş SaaS uygulamaları
* Doğrudan, müşteri dönük uygulamaları
* Çalışanla yüz yüze gelinen kurumsal uygulamalar

İş ortağı veritabanı uygulamaları genellikle çok kiracılı uygulamalar gibi hello Bulut ve kökleri olanlar için tasarlanmıştır SaaS uygulamaları. Bu SaaS uygulamaları hizmet tootheir Kiracı olarak özel yazılım uygulaması sunar. Kiracılar hello uygulama hizmetine erişim ve tam sahiplik Merhaba uygulaması bir parçası olarak depolanan ilişkili veri. Ancak SaaS, kiracılar hello yararları tootake avantajı, kendi veriler üzerinde bazı denetim surrender gerekir. Güvenli ve diğer kiracılar verilerden yalıtılmış verilerini hello SaaS hizmet sağlayıcısı tookeep güvendikleri. Bu tür bir çok kiracılı SaaS uygulaması MYOB, SnelStart ve Salesforce.com gösterilebilir. Bu uygulamaların her biri Kiracı sınırları ve Destek hello uygulama tasarım desenleri bu makalede aşağıdakiler ele boyunca bölümlenebilir.

Bir doğrudan hizmet toocustomers ya da bir kuruluştaki (genellikle başvurulan tooas kullanıcılar yerine kiracılar) tooemployees sağlayan hello çok kiracılı uygulama spektrumun başka bir kategoride uygulamalardır. Müşteriler toohello hizmete abone olmak ve hizmet sağlayıcısı hello hello veri toplar ve depolar sahibi değilsiniz. Hizmet sağlayıcıları daha az sıkı gereksinimleri tookeep birbirinden kamu zorunlu ilke yönetmeliklerini yalıtılmış müşterilerin verilere sahip. Bu tür bir müşteri dönük çok kiracılı uygulama medya içerik sağlayıcıları Netflix, Spotify ve Xbox LIVE gibi gösterilebilir. Müşteri dönük kolayca bölümlenebilir uygulamaların diğer örnekler, Internet ölçekli uygulamalar ya da her hangi müşteri veya aygıt can nesnelerin interneti (IOT) uygulamalarında bir bölümü olarak hizmet. Bölüm sınırları, kullanıcıların ve aygıtların ayırabilirsiniz.

Kiracı, müşteri, kullanıcı veya aygıt gibi tek bir özellik kolayca boyunca tüm uygulamaları bölüm. (ERP) uygulama planlaması karmaşık kurumsal kaynak, örneğin, ürünler, siparişler ve müşteriler sahiptir. Genellikle, yüksek oranda birbirine bağlı tabloları binlerce ile karmaşık bir şeması vardır.

Tek bölüm stratejisi yok tooall tabloları uygulanır ve boyunca bir uygulamanın iş yükünü çalışır. Bu makalede kolayca bölümlenebilir veri ve iş yüklerine sahip birden çok kiracılı uygulamalara odaklanılmaktadır.

## <a name="multi-tenant-application-design-trade-offs"></a>Çok kiracılı uygulama tasarım dengelemeler
çok kiracılı uygulama geliştiricisi genellikle seçer hello tasarım deseni bir Etkenler aşağıdaki hello konusuna göre dayanır:

* **Kiracı yalıtımı**. Merhaba Geliştirici Kiracı istenmeyen erişimi tooother kiracılarınızın verilerin olduğunu tooensure gerekir. Merhaba yalıtım gereksinim gürültülü komşu koruma sağlayan, bir kiracının veri mümkün toorestore olması ve Kiracı özgü özelleştirmeler uygulamak gibi tooother özelliklerini genişletir.
* **Bulut kaynak maliyeti**. Bir SaaS uygulaması toobe maliyet açısından rekabetçi gerekir. Çok kiracılı uygulama geliştiricisi toooptimize için düşük maliyetli depolama alanı gibi bulut kaynaklarının hello kullanımını seçin ve maliyetleri işlem olabilir.
* **DevOps kolaylığı**. Çok kiracılı uygulama geliştiricisinin tooincorporate yalıtım koruma gerekir, Bakımı ve kendi uygulama ve veritabanı şeması hello sağlığını izlemek ve Kiracı sorunlarını giderme. Uygulama geliştirme ve işlem karmaşıklığı doğrudan tooincreased maliyet çevirir ve Kiracı tatmin sınar.
* **Ölçeklenebilirlik**. Merhaba özelliği tooincrementally kiracılar ve kapasite kesinlik temelli tooa başarılı SaaS işlemi olduğundan gereksinim duyan kiracılar için daha fazla ekleyin.

Faktörlerin her biri karşılaştırıldığında dengelemeler tooanother sahiptir. Merhaba en düşük maliyeti bulut Hello en kolay geliştirme deneyimi sunabilir değil teklifi. Bir geliştirici için önemli olduğunu toomake haberdar seçimleri Bu seçenekler ve bunların dengelemeler hakkında hello uygulamasının Tasarım işlemi sırasında.

Popüler geliştirme desen bir veya birkaç veritabanlarına birden çok kiracıya toopack olduğu. Bu yaklaşımın avantajları hello daha düşük maliyetli bir olduklarından, birkaç veritabanları ve sınırlı sayıda veritabanları ile çalışmanın hello göreli kolaylık sağlaması için ücret ödersiniz. Ancak, zaman içinde bir SaaS çok kiracılı uygulama geliştiricisinin bu seçenek Kiracı yalıtımı ve ölçeklenebilirlik önemli downsides olduğunu unutmayın. Kiracı yalıtımı önemli hale gelirse, ek çaba gerekli tooprotect Kiracı yetkisiz erişim veya gürültülü komşu paylaşılan depolama alanında verilerdir. Bu ek çaba, geliştirme çalışmalarını ve yalıtım bakım maliyetlerini önemli ölçüde artırabilir. Benzer şekilde, kiracılar eklenmesi gerekiyorsa, bu tasarım deseni genellikle uzmanlık tooredistribute Kiracı veri veritabanları tooproperly ölçek hello veri katmanı uygulamasının arasında gerektirir.  

Genellikle Kiracı yalıtımı, toobusinesses ve kuruluşların karşılamak SaaS çok kiracılı uygulamalarda temel bir gereksinimdir. Bir geliştirici tarafından algılanan avantajları Basitlik ve maliyet Kiracı yalıtımı ve ölçeklenebilirlik tempted. Bu dengelemeyi karmaşık ve pahalı hello hizmet büyüdükçe ve Kiracı yalıtımı gereksinimleri hale gibi daha önemli ve yönetilen hello uygulama katmanında kanıtlayabilirsiniz. Ancak, doğrudan, tüketiciye yönelik hizmet toocustomers sağlayan çok kiracılı uygulamalara, Kiracı yalıtımı için bulut kaynak maliyetini en iyi duruma getirme değerinden daha düşük bir öncelik olabilir.

## <a name="multi-tenant-data-models"></a>Çok kiracılı veri modelleri
Kiracı verileri yerleştirmek için ortak tasarım uygulamaları Şekil 1'de gösterilen üç ayrı modeli izleyin.

![çok kiracılı uygulama veri modelleri](./media/sql-database-design-patterns-multi-tenancy-saas-applications/sql-database-multi-tenant-data-models.png)

Şekil 1: Çok kiracılı veri modelleri için ortak tasarım yöntemler

* **Kiracı başına veritabanı**. Her bir kiracı kendi veritabanına sahip. Tüm Kiracı özgü veriler yalıtılmış toohello kiracının veritabanı ve diğer kiracılar ve bunların verilerinden yalıtılır.
* **Veritabanı parçalı paylaşılan**. Birden çok Kiracı birden çok veritabanlarından birini paylaşır. Kiracılar ayrı bir dizi tooeach veritabanı karması, aralığı veya liste bölümleme gibi bölümleme stratejisine kullanılarak atanır. Bu veri dağıtım stratejisini başvurulan tooas parçalama görülür.
* **Veritabanı tek paylaşılan**. Tek, bazen büyük bir veritabanı, bir kiracı Kimlik sütununda disambiguated tüm kiracılar için verileri içerir.

> [!NOTE]
> Bir uygulama geliştiricisi tooplace farklı kiracıların farklı veritabanı şemalarını seçin ve hello şema adı toodisambiguate hello farklı kiracıların kullanmak. Dinamik SQL hello kullanımı genellikle gerektirdiğinden ve planı önbelleğe alma etkin olamaz bu yaklaşım önerilmez. Merhaba bu makalenin sonraki bölümlerinde içinde Biz bu kategori, çok kiracılı uygulama için paylaşılan hello tablo yaklaşım odaklanılmaktadır.
> 
> 

## <a name="popular-multi-tenant-data-models"></a>Popüler çok kiracılı veri modelleri
Önemli tooevaluate hello farklı türde çok kiracılı veri modelleri hello uygulama tasarım zaten belirledik dengelemeler bakımından olur. Bu etkenler daha önce açıklanan üç hello en yaygın çok kiracılı veri modelleri ve Şekil 2'de gösterildiği gibi veritabanı kullanımı niteleyen yardımcı olur.

* **Yalıtım**. kiracılar arasında yalıtım Hello derecesini bir veri modeli başarır ne kadar Kiracı yalıtımı ölçüsü olabilir.
* **Bulut kaynak maliyeti**. Kaynak kiracılar arasında paylaşımı Hello miktarı, bulut kaynak maliyeti en iyi duruma getirebilirsiniz. Bir kaynak hello işlem ve depolama maliyeti tanımlanabilir.
* **DevOps maliyet**. uygulama geliştirme, dağıtım ve yönetilebilirlik Hello kolaylığı genel SaaS işlemi maliyeti azaltır.  

Şekil 2'de hello Y ekseni Kiracı yalıtımı hello düzeyini gösterir. Merhaba X ekseni kaynak paylaşma hello düzeyini gösterir. Merhaba gri hello ortasında çapraz ok tooincrease veya düşüş eğilimi gösterir, DevOps maliyetleri hello yönünü belirtir.

![Popüler çok kiracılı uygulama tasarım desenleri](./media/sql-database-design-patterns-multi-tenancy-saas-applications/sql-database-popular-application-patterns.png)

Şekil 2: Popüler çok kiracılı veri modelleri

Merhaba sağ alt çeyreğinde Şekil 2'deki gösterir çok, paylaşılan bir tek veritabanı kullanan bir uygulama düzeni ve hello paylaşılan tablosu (veya ayrı şema) yaklaşım. Kaynak tüm kiracılar (CPU, bellek, giriş/çıkış) kaynakları tek bir veritabanında aynı veritabanı hello kullandığından paylaşımı uygundur. Ancak, Kiracı yalıtımı sınırlıdır. Itanium tabanlı sistemler için tootake ek adımlar tooprotect kiracılar birbirinden hello uygulama katmanında gerekebilir. Aşağıdaki ek adımları geliştirmek ve Merhaba uygulaması yönetmek hello DevOps maliyetini önemli ölçüde artırabilir. Merhaba veritabanını barındıran hello donanım hello ölçek tarafından sınırlı ölçeklenebilirlik.

Şekil 2'deki Hello sol alt Dörtgen Bölümlü birden çok veritabanı arasında birden çok kiracıya parçalı gösterir (genellikle, farklı donanım ölçek birimleri). Her veritabanını diğer desenleri hello ölçeklenebilirlik sorunu giderir kiracılar, bir alt barındırır. Daha fazla kiracılar için daha fazla kapasite gerekiyorsa, yeni veritabanlarını toonew donanım ölçek birimi ayrılan hello kiracılar kolayca yerleştirebilirsiniz. Ancak, kaynak paylaşma hello miktarı azalır. Kiracılar hello üzerinde aynı yerleştirilen yalnızca ölçek birimleri kaynakları paylaşır. Çok sayıda Kiracı hala otomatik olarak diğer kişilerin eylemlerine korunan olmadan birlikte bulunan için bu yaklaşım küçük geliştirme tootenant yalıtım sağlar. Uygulama karmaşıklığını yüksek kalır.

Şekil 2'deki Hello sol üst Dörtgen Bölümlü hello üçüncü yaklaşımdır. Her bir kiracının veri kendi veritabanında yerleştirir. Bu yaklaşım iyi Kiracı yalıtımı özelliklere sahiptir ancak her veritabanı kendi özel kaynakları olduğunda kaynak paylaşma sınırlar. Bu yaklaşım tüm kiracılar tahmin edilebilir iş yükleriniz varsa iyi olur. Kiracı İş yükleri daha az öngörülebilir hale gelirse hello sağlayıcısı kaynak paylaşma iyileştirilemiyor. Karşılaştırıldığında, SaaS uygulamaları için yaygın bir durumdur. Merhaba sağlayıcısı ya da toomeet taleplerini veya alt kaynakları aşırı hazırlamanız gerekir. Her iki eylem sonuçlarını daha yüksek maliyetleri ya da daha düşük Kiracı memnuniyet. Bir kaynak kiracılar arasında paylaşımı daha yüksek derecede arzu toomake hello çözümü daha düşük maliyetli hale gelir. Veritabanı artan hello sayısı ayrıca DevOps maliyet toodeploy artırır ve Merhaba uygulaması korumak. Bu sorunları rağmen hello en iyi ve en kolay yalıtım kiracılar için bu yöntem sağlar.

Bu etkenler ayrıca bir müşteri seçer hello tasarım deseni etkiler:

* **Kiracı veri sahipliğini**. Kiracıların kendi veri sahipliğini korumak uygulama hello düzeni Kiracı başına tek bir veritabanının korur.
* **Ölçek**. Binlerce veya kiracılar milyonlarca yüzlerce hedefleyen bir uygulama veritabanı parçalama gibi yaklaşımlar paylaşımı korur. Yalıtım gereksinimleri hala yol açabilir.
* **Değer ve iş modeli**. Bir uygulama, kullanıcının her Kiracı gelir küçük (değerinden ABD Doları), daha az önemli hale yalıtımı gereksinimleri ve paylaşılan bir veritabanı algılama yapıyorsa. Kiracı başına gelir birkaç dolar veya daha fazla ise, bir kiracı başına veritabanı daha uygun modelidir. Geliştirme maliyetleri azaltmasına yardımcı olabilir.

İdeal çok kiracılı bir model Hello tasarım Şekil 2'de gösterilen dengelemeler göz önüne alındığında, en iyi kaynak kiracılar arasında paylaşımı ile tooincorporate iyi Kiracı yalıtımı özelliklerini gerekir. Bu model hello sağ üst köşede çeyreğinde Şekil 2 ' açıklanan hello kategori sığar.

## <a name="multi-tenancy-support-in-azure-sql-database"></a>Azure SQL veritabanı çoklu kiracı desteği
Azure SQL veritabanı Şekil 2'de gösterilen tüm çok kiracılı uygulama desenleri destekler. Esnek havuzları ile hello yalıtım hello veritabanı başına-Kiracı avantajları (bkz. Şekil 3'te hello sağ üst köşede Dörtgen Bölümlü) yaklaşmak ve iyi kaynak paylaşma birleştiren bir uygulama düzeni de destekler. Esnek veritabanı araçlarını ve SQL veritabanı özelliklerini hello maliyet toodevelop azaltmak ve birçok veritabanı (gölgeli hello alanında Şekil 3'te gösterilen) olan bir uygulama çalıştırmak yardımcı olur. Bu araçlar, yapı ve hello çok veritabanı desenleri birini kullanan uygulamaları yönetmenize yardımcı olabilir.

![Azure SQL veritabanı düzenleri](./media/sql-database-design-patterns-multi-tenancy-saas-applications/sql-database-patterns-sqldb.png)

Şekil 3: Çok kiracılı uygulama düzenleri Azure SQL veritabanı

## <a name="database-per-tenant-model-with-elastic-pools-and-tools"></a>Kiracı başına veritabanı modeliyle esnek havuzlar ve araçları
Esnek havuzlar SQL veritabanında kaynak Kiracı veritabanları toobetter destek hello Kiracı başına veritabanı yaklaşım arasında paylaşımı Kiracı yalıtımı birleştirin. SQL veritabanı bir çok kiracılı uygulamalara yapı SaaS sağlayıcısı için veri katmanı çözümüdür. Kaynak kiracılar arasında paylaşımı Hello yükünü hello uygulama katmanı toohello veritabanı hizmet katmanından kaydırır. Merhaba karmaşıklığını yönetme ve veritabanları arasında ölçekte sorgulama esnek işler, esnek sorgu, esnek işlemleri ve hello esnek veritabanı istemci kitaplığı ile basitleştirilmiştir.

| Uygulama gereksinimleri | SQL veritabanı özellikleri |
| --- | --- |
| Kiracı yalıtımı ve kaynak paylaşma |[Esnek havuzlar](sql-database-elastic-pool.md): SQL veritabanı kaynak havuzu ayırma ve hello kaynakları çeşitli veritabanları arasında paylaşın. Ayrıca, tek veritabanlarını kadar kaynakları hello havuzundan gerekli tooaccommodate kapasite talep ani çizebilirsiniz Kiracı İş yükleri, son toochanges. Esnek havuz Hello kendisini yukarı veya aşağı gerektiği şekilde genişletilebilir. Esnek havuzlar Ayrıca, yönetilebilirlik ve izleme ve hello havuzu düzeyinde sorun giderme kolaylığı sağlar. |
| DevOps kolaylığı veritabanları arasında |[Esnek havuzlar](sql-database-elastic-pool.md): daha önce belirtildiği gibi. |
| | [Esnek sorgu](sql-database-elastic-query-horizontal-partitioning.md): Sorgu raporlama veritabanları arasında veya çapraz-Kiracı çözümleme. |
| | [Esnek iş](sql-database-elastic-jobs-overview.md): Paket ve veritabanı bakım işlemleri güvenilir bir şekilde dağıtmak veya veritabanı şeması toomultiple veritabanları değiştirir. |
| | [Esnek işlemleri](sql-database-elastic-transactions-overview.md): işlem tooseveral veritabanları atomik ve yalıtılmış bir şekilde değiştirir. Uygulamaları birkaç veritabanı işlemleri "tümü veya hiçbiri" garanti gerektiğinde esnek hareket gerekli değildir. |
| | [Esnek veritabanı istemci Kitaplığı](sql-database-elastic-database-client-library.md): veri dağıtımları yönetmek ve harita kiracılar toodatabases. |

## <a name="shared-models"></a>Paylaşılan modelleri
Birçok SaaS sağlayıcıları için daha önce açıklandığı gibi bir paylaşılan model yaklaşım Kiracı yalıtımı sorunları ile ilgili problemler ve karmaşıklık uygulama geliştirme ve Bakım neden olabilir. Ancak, bir hizmeti tooconsumers, Kiracı doğrudan sağlayan çok kiracılı uygulamalar için yalıtım gereksinimleri maliyeti en aza olarak yüksek bir öncelik olmayabilir. Bunlar, bir veya daha fazla veritabanı en yüksek yoğunluklu tooreduce maliyetleri mümkün toopack kiracılar olabilir. Paylaşılan veritabanı modelleri tek bir veritabanı veya birden çok parçalı veritabanı kullanan kaynak paylaşma ve genel maliyet ek verimliliği neden olabilir. Azure SQL veritabanı müşterilere yardımcı olun bazı özellikleri için Gelişmiş Güvenlik ve yönetim hello veri katmanındaki ölçekte yalıtım oluşturmak sağlar.

| Uygulama gereksinimleri | SQL veritabanı özellikleri |
| --- | --- |
| Güvenlik yalıtımı özellikleri |[Satır düzeyi güvenlik](https://msdn.microsoft.com/library/dn765131.aspx) |
| [Veritabanı şeması](https://msdn.microsoft.com/library/dd207005.aspx) | |
| DevOps kolaylığı veritabanları arasında |[Esnek sorgu](sql-database-elastic-query-horizontal-partitioning.md) |
| | [Esnek işler](sql-database-elastic-jobs-overview.md) |
| | [Esnek işlemleri](sql-database-elastic-transactions-overview.md) |
| | [Elastik veritabanı istemci kitaplığı](sql-database-elastic-database-client-library.md) |
| | [Esnek veritabanı bölme ve birleştirme](sql-database-elastic-scale-overview-split-and-merge.md) |

## <a name="summary"></a>Özet
Kiracı yalıtımı gereksinimleri en çok kiracılı SaaS uygulamaları için önemlidir. Merhaba en iyi seçenek tooprovide yalıtım yoğun hello Kiracı başına veritabanı yaklaşım doğru leans. Merhaba diğer iki yaklaşım maliyet ve risk önemli ölçüde artırır becerikli Geliştirme ekibiniz tooprovide yalıtımı gerektiren karmaşık uygulama katmanları yatırım gerektirir. Yalıtım gereksinimleri erken hello hizmeti geliştirme katılmayan varsa, bunları retrofitting hello ilk iki modellerinde daha pahalı olabilir. Merhaba ana dezavantajları Hello Kiracı başına veritabanı modeli ile ilişkili son paylaşımı, tooreduced ve Bakım ve birçok veritabanlarını yönetmeyle ilgili tooincreased bulut kaynak maliyetleri ' dir. Bu dengelemeler yaptıklarında SaaS uygulama geliştiriciler genellikle güçlük.

Ana engelleri çoğu bulut veritabanı hizmet sağlayıcısı ile dengelemeler olabilir, ancak Azure SQL veritabanı, esnek havuz ve esnek veritabanı özelliklerini hello engelleri ortadan kaldırır. SaaS geliştiriciler, bir kiracı başına veritabanı modeli hello yalıtım özelliklerini birleştirmek ve esnek havuzlar ve ilişkili araçlarını kullanarak birçok veritabanı kaynak paylaşımı ve hello yönetilebilirlik geliştirmeleri en iyi duruma getirme.

Hiçbir Kiracı yalıtımı gereksinimleri sahip ve kimlerin kiracılar yüksek yoğunluklu bir veritabanında paketi çok kiracılı uygulama sağlayıcılarının, paylaşılan veri kaynağı paylaşımı ek verimliliği de sonuç modeller ve genel maliyetini azaltmak bulabilirsiniz. Azure SQL Database esnek veritabanı araçlarını, parçalama kitaplıkları ve güvenlik özellikleri oluşturmak ve yönetmek çok kiracılı uygulamalara SaaS sağlayıcıları yardımcı olur.

## <a name="next-steps"></a>Sonraki adımlar
[Esnek veritabanı araçlarını kullanmaya başlama](sql-database-elastic-scale-get-started.md) hello istemci Kitaplığı gösteren örnek bir uygulama ile.

Oluşturma bir [SaaS için esnek havuz özel Pano](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools-custom-dashboard) esnek havuzlar için uygun maliyetli ve ölçeklenebilir veritabanı çözümü kullanan bir örnek uygulama ile.

Çok Hello Azure SQL veritabanı araçlarını kullanın[çıkışı varolan veritabanları tooscale geçirmek](sql-database-elastic-convert-to-use-elastic-tools.md).

kullanarak bir esnek havuz toocreate hello Azure portal, bkz: [bir esnek havuz oluşturma](sql-database-elastic-pool-manage-portal.md).  

Nasıl çok öğrenin[izlemek ve esnek havuzunu yönetme](sql-database-elastic-pool-manage-portal.md).

## <a name="additional-resources"></a>Ek kaynaklar

* [Dağıtma ve Azure SQL veritabanı - Wingtip SaaS kullanan çok kiracılı uygulama keşfedin](sql-database-saas-tutorial.md)
* [Bir Azure esnek havuz nedir?](sql-database-elastic-pool.md)
* [Azure SQL Veritabanı ile ölçek genişletme](sql-database-elastic-scale-introduction.md)
* [çok kiracılı uygulamalarla esnek veritabanı araçlarını ve satır düzeyi güvenlik](sql-database-elastic-tools-multi-tenant-row-level-security.md)
* [Azure Active Directory ve Openıd Connect kullanarak çok kiracılı uygulamalara kimlik doğrulaması](../guidance/guidance-multitenant-identity-authenticate.md)
* [Tailspin Surveys uygulaması](../guidance/guidance-multitenant-identity-tailspin.md)


## <a name="questions-and-feature-requests"></a>Sorular ve özellik istekleri

Sorular için bize hello Bul [SQL veritabanı Forumu](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted). Özellik isteği hello eklemek [SQL veritabanı geri bildirim Forumunda](https://feedback.azure.com/forums/217321-sql-database/).

