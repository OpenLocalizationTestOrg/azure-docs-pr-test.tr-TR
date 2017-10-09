---
title: "aaaWhat hello Azure SQL veritabanı hizmetinin mi? | Microsoft Belgeleri"
description: "Bir giriş tooSQL veritabanı Al: Teknik Ayrıntılar ve özellikler Microsoft'un ilişkisel veritabanı yönetim sistemine (RDBMS) hello bulutta."
keywords: "Giriş toosql, giriş toosql, sql database nedir"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: cgronlun
ms.assetid: c561f600-a292-4e3b-b1d4-8ab89b81db48
ms.service: sql-database
ms.custom: overview
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 06/30/2017
ms.author: carlrab
ms.openlocfilehash: 24ca383ad7e140133d19debc8899f172ee4aa424
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-azure-sql-database-service"></a>Hello Azure SQL Database hizmeti nedir? 

SQL Veritabanı, Microsoft Azure'da yer alan ve ilişkisel veri, JSON, uzamsal ve XML gibi yapıları destekleyen çok amaçlı ilişkisel veritabanı hizmetidir. [Dinamik olarak ölçeklenebilir performans](sql-database-service-tiers.md) sunan bu hizmet çok büyük ölçekli analitik analiz ve raporlama için [columnstore dizinleri](https://docs.microsoft.com/sql/relational-databases/indexes/columnstore-indexes-overview) gibi seçenekler, raporlama ve çok büyük ölçekli işlemler için [bellek içi OLTP](sql-database-in-memory.md) özelliklerine sahiptir. Microsoft tüm düzeltme eki uygulama ve hello SQL kodunu temel sorunsuz bir şekilde güncelleştirme işler ve hemen tüm yönetimi altyapısını temel hello soyutlar. 

SQL veritabanını paylaşan kendi kod tabanını ile Merhaba [Microsoft SQL Server veritabanı motorunun](https://docs.microsoft.com/sql/sql-server/sql-server-technical-documentation). Microsoft'un bulut ilk stratejisi, SQL Server'ın en yeni işlevleri hello yayımlanan ilk tooSQL veritabanı ve tooSQL sunucusunun kendisi var. Yükseltme - ve bu yeni özelliklere sahip veritabanları milyonlarca test veya bu yaklaşım düzeltme eki uygulama için hiçbir ek yükü en yeni SQL Server özellikleriyle ile Merhaba sağlar. Yeni özellikler açıklandıkça haberdar olmak için bkz:

- **[SQL veritabanı için Azure yol haritası](https://azure.microsoft.com/roadmap/?category=databases)**: yeni ve sonraki yakında kullanıma yer toofind. 
- **[Azure SQL Veritabanı blogu](https://azure.microsoft.com/blog/topics/database)**: SQL Server ürün ekibi üyelerinin SQL Veritabanı haberleri ve özellikleri hakkında yazdıkları blog. 

SQL Veritabanı birden fazla hizmet düzeyinde kesinti süresi olmadan dinamik kararlılık, yerleşik zeka iyileştirmesi, global düzeyde ölçeklenebilirlik ve kullanılabilirlik ile gelişmiş güvenlik seçeneklerine sahip tahmin edilebilir performansı neredeyse sıfır yönetim gereksinimiyle sunar. Bu özellikler, hızlı uygulama geliştirme ve zaman toomarket hızlandırmaya, yerine çok değerli bir zaman ve kaynak toomanaging sanal makineleri ve altyapıyı ayırma toofocus izin verir. Merhaba SQL veritabanı şu anda 38 verilerde hizmetidir Merhaba dünya genelinde veritabanınızı yakın bir veri merkezindeki toorun sağlayan düzenli olarak çevrimiçine daha fazla veri merkezleri ile hizalar.

> [!NOTE]
> Azure'un platform güvenliği hakkında bilgi edinmek için de [Azure Güven Merkezi](https://azure.microsoft.com/support/trust-center/security/)'ni ziyaret edebilirsiniz.
>

## <a name="scalable-performance-and-pools"></a>Ölçeklenebilir performans ve havuzlar

SQL Veritabanı ile her veritabanı diğerlerinden ayrı ve taşınabilir olmanın yanı sıra garantili performans düzeyinde ve kendi [hizmet katmanında](sql-database-service-tiers.md) yer alır. SQL veritabanı için farklı gereksinimleri farklı performans düzeyleri sağlar ve toobe havuza alınmış toomaximize hello kaynaklarının kullanımını ve paradan tasarruf veritabanları etkinleştirir.

### <a name="adjust-performance-and-scale-without-downtime"></a>Kesinti olmadan performansı ayarlama ve ölçeklendirme

SQL veritabanı toosupport basit tooheavyweight veritabanı iş yükleri dört hizmet katmanları sunar: temel, standart, Premium ve Premium RS. Düşük bir maliyetle aylık küçük, tek bir veritabanı üzerinde ilk uygulamanızı oluşturun ve ardından, hizmet katmanı hiçbir zaman toomeet hello ihtiyaçlarını çözümünüzü el ile veya programlama değiştirin. Kapalı kalma süresi tooyour uygulama veya tooyour müşteriler olmadan performans ayarlayabilirsiniz. Veritabanı tootransparently yanıt kaynak gereksinimlerini ve etkinleştirir, tooonly gereksinim duyduğunuzda ihtiyacınız hello kaynaklar için ödeme değiştirme toorapidly dinamik ölçeklenebilirlik sağlar.

   ![ölçeklendirme](./media/sql-database-what-is-a-dtu/single_db_dtus.png)

### <a name="elastic-pools-toomaximize-resource-utilization"></a>Esnek havuzlar toomaximize kaynak kullanımı

Birçok işletme ve uygulamalar için tek veritabanlarını mümkün toocreate olması ve performans yukarı veya aşağı isteğe bağlı özellikle kullanım desenlerini nispeten tahmin edilebilir yeterince ise çevir. Ancak tahmin edilemeyen kullanım biçimlerine sahipseniz, bunu sabit toomanage maliyetleri ve iş modelinizin yapabilirsiniz. [Esnek havuzlar](sql-database-elastic-pool.md) tasarlanmış toosolve bu sorunu olan. Merhaba kavram, basit bir işlemdir. Tek bir veritabanının yerine performans kaynakları tooa havuzu ayırma ve hello toplu performans kaynakların hello havuzunun yerine tek veritabanı performansı için ödeme yaparsınız. 

   ![elastik havuzlar](./media/sql-database-what-is-a-dtu/sqldb_elastic_pools.png)

Esnek havuzları ile isteğe bağlı kaynaklar için arttıkça veritabanı performansını yukarı ve aşağı arama üzerinde toofocus gerek yoktur. Merhaba havuza alınmış veritabanları hello performans kaynaklarını hello esnek havuzun gerektiğinde tüketebilir. Havuza alınmış veritabanları kullanabilir, ancak tek tek veritabanı kullanımına olmasa bile maliyetleriniz tahmin edilebilir böylece hello sınırları hello havuzunun aşmayan. Daha fazla nedir, şunları yapabilirsiniz [veritabanları toohello havuzu ekleyip](sql-database-elastic-pool-manage-portal.md), tüm denetim bir bütçe içinde veritabanları toothousands sayıda uygulamanızdan ölçeklendirme. En fazla kaynak kullanılabilir toodatabases hiçbir veritabanı hello havuzundaki tüm kullanan hello havuzu tooensure içinde havuz kaynakları ve havuza alınmış her veritabanı kaynakları garanti edilen en düşük miktarda olduğunu hello ve denetim hello minimum de kullanabilirsiniz. Esnek havuzları kullanan SaaS uygulamaları için Tasarım desenleri hakkında daha fazla toolearn bkz [SQL veritabanı ile çok kiracılı SaaS uygulamaları için Tasarım desenleri](sql-database-design-patterns-multi-tenancy-saas-applications.md).

### <a name="blend-single-databases-with-pooled-databases"></a>Tek veritabanlarını havuza alınmış veritabanlarıyla karıştırma

İster tek veritabanlarını isterseniz elastik havuzları seçin, tercihlerinizi dilediğiniz zaman değiştirebilirsiniz. Tek veritabanlarını esnek havuzlar blend ve hızlı ve kolay bir şekilde hello hizmet katmanları tek veritabanları ve esnek havuzlar değiştirme tooadapt tooyour durum. Merhaba gücü ve erişim Azure ile karışımı ve diğer Azure SQL veritabanı toomeet benzersiz uygulamanızı tasarım gereksinimleri, sürücü maliyet ve kaynak verimliliği ile Hizmetleri ve yeni iş fırsatlarını yakalamak eşleştirme olabilir.

### <a name="extensive-monitoring-and-alerting-capabilities"></a>Kapsamlı izleme ve uyarı özellikleri

Ancak, tek veritabanları ve esnek havuzlar göreli performansını hello nasıl karşılaştırabilirsiniz? Yukarı ve aşağı çevirdiğinizde hello sağ tıklayın durdurma nasıl bilebilirsiniz? Merhaba kullandığınız [yerleşik performans izleme](sql-database-performance.md) ve [uyarı](sql-database-insights-alerts-portal.md) araçları, temel hello performans değerlendirmeleri birlikte [tek veritabanları için veritabanı işlem birimleri (Dtu'lar) ve Esnek havuz için Dtu'lar (Edtu'lar) esnek](sql-database-what-is-a-dtu.md). Bu araçları kullanarak, hello etkisini yukarı veya aşağı geçerli göre ölçeklendirme hızla değerlendirebilirsiniz veya proje performans gereksinimlerine. Ayrıntılı bilgi için bkz. [SQL Database seçenekleri ve performansı: Her hizmet katmanında nelerin kullanılabildiğini anlama](sql-database-service-tiers.md).

SQL Veritabanı ayrıca izlemeyi kolaylaştırmak için [ölçümler ve tanılama günlükleri oluşturabilir](sql-database-metrics-diag-logging.md). SQL veritabanı toostore kaynak kullanımı, çalışanlar ve oturumlar ve bu Azure kaynakları birine bağlantısını yapılandırabilirsiniz:

- **Azure Depolama**: Küçük maliyetlerle çok sayıda telemetri arşivleme için
- **Azure Olay Hub'ı**: SQL Veritabanı telemetrisini özel izleme çözümünüz veya yoğun işlem hatlarıyla tümleştirmek için
- **Azure Log Analytics**: Raporlama, uyarı ve azaltma özelliklerine sahip yerleşik izleme çözümü için

    ![architecture](./media/sql-database-metrics-diag-logging/architecture.png)

## <a name="availability-capabilities"></a>Kullanılabilirlik özellikleri

Azure'ın Microsoft yönetimindeki veri merkezlerinin küresel bir ağı tarafından desteklenen ve endüstri lideri niteliğinde %99,99'luk bir kullanılabilirlik oranı sunan hizmet düzeyi sözleşmesi [(SLA)](http://azure.microsoft.com/support/legal/sla/), uygulamanızın 7/24 kesintiye uğramamasına yardımcı olur. SQL Veritabanı ayrıca aşağıdakiler dahil olmak üzere yerleşik [iş sürekliliği ve global ölçeklenebilirlik](sql-database-business-continuity.md) özelliklerine sahiptir:

- **[Otomatik yedekleme](sql-database-automated-backups.md)**: SQL Veritabanı otomatik olarak tam, değişiklik ve işlem günlüğü kapsamlı yedeklemeler gerçekleştirir.
- **[Zaman içinde nokta geri yüklemeler](sql-database-recovery-using-backups.md)**: SQL veritabanı süre hello otomatik yedekleme saklama dönemi içinde kurtarma tooany noktası destekler.
- **[Aktif coğrafi çoğaltma](sql-database-geo-replication-overview.md)**: SQL veritabanı sağlar, tooconfigure toofour okunabilir ikincil yukarı ya da hello aynı veritabanları veya Azure veri merkezlerinde genel olarak dağıtılmış.  Örneğin, eşzamanlı salt okunur işlemler yüksek hacimli bir katalog veritabanına sahip bir SaaS uygulaması varsa, genel kullanım aktif coğrafi çoğaltma tooenable ölçek okuyun ve tooread iş yüklerinin performans sorunlarını hello birincil üzerinde kaldırın. 
- **[Yük devretme grupları](sql-database-geo-replication-overview.md)**: SQL veritabanı sağlar tooenable yüksek kullanılabilirlik ve Yük Dengeleme saydam coğrafi çoğaltma ve yük devretme veritabanlarını ve esnek havuzlar büyük kümeleri dahil olmak üzere genel ölçekte. Yük devretme gruplar ve en az yönetim yükü tüm hello karmaşık izleme, Yönlendirme ve yük devretme orchestration tooSQL veritabanı bırakarak Genel dağıtılmış SaaS uygulamaları aktif coğrafi çoğaltma etkinleştirir oluşturma.

## <a name="built-in-intelligence"></a>Yerleşik zeka

SQL veritabanı ile performans ve güvenlik, uygulamanızın en üst düzeye çıkarır ve önemli ölçüde çalıştıran ve veritabanlarını yönetme hello maliyetleri azaltmanıza yardımcı olur yerleşik zekaya alın. Müşteri milyonlarca gün boyunca iş yükleri çalıştıran, SQL veritabanı toplar ve tam olarak hello perde arkasında müşteri gizliliğine saygı göstermek sırasında telemetri verileri büyük bir miktarını işler. Böylece Hello hizmet öğrenin ve uygulamanız ile uyum çeşitli algoritmalar sürekli hello telemetri verileri değerlendiriyorsanız. Bu analize dayalı olarak, hello hizmeti performans önerileri uyarlanmış tooyour belirli iş yükü geliştirme ile gelir. 

### <a name="automatic-performance-tuning"></a>Otomatik performans ayarlama

SQL veritabanı toomonitor gerektiğini hello ayrıntılı bir anlayış sorgular sağlar. SQL veritabanının veritabanı desenleri hakkında öğrenir ve veritabanı şeması tooyour yükünüzü, tooadapt sağlar. SQL Veritabanı, [SQL Veritabanı Danışmanı](sql-database-advisor.md),'nı kullanarak performans ayarlama önerilerinde bulunur. Siz de bu ayarları gözden geçirebilir ve uygulayabilirsiniz. Ancak özellikle birden fazla veritabanıyla ilgilenirken bir veritabanını sürekli izlemek zor ve yorucu bir görevdir. Veritabanları büyük sayıda yönetme bile tüm kullanılabilir araçları ve SQL Database ve Azure portal sağlayan raporları verimli bir şekilde imkansız toodo olabilir. İzleme ve veritabanınızı el ile ayarlama yerine, izleme ve eylemleri tooSQL ayarlama hello bazıları için temsilci seçme düşünebilirsiniz otomatik ayarlama özelliğini kullanarak veritabanı. SQL veritabanı otomatik olarak öneriler, testleri, uygulayın ve her ayarlama Eylemler tooensure hello performansını artırma tutar doğrular. Bu şekilde, SQL veritabanı otomatik olarak tooyour iş yükü denetimli ve güvenli bir şekilde uyum sağlar. Otomatik ayarlama, veritabanınızın hello performansı dikkatlice izlenen ve önce ve sonra her ayar eylemi karşılaştırılır ve hello performansı değil, eylem ayarlama hello geri anlamına gelir.

Bugün, çok ortaklarımızın çalıştıran biri [SaaS çok kiracılı uygulamaları](sql-database-design-patterns-multi-tenancy-saas-applications.md) SQL veritabanının üst kısmında toomake uygulamalarını her zaman kararlı ve öngörülebilir performans olmasını ayarlama otomatik performansına bağlı. Bunlar için bu özellik büyük ölçüde performans olay hello gece hello ortadaki sahip olmanın hello riskini azaltır. Kendi müşteri tabanı parçası ayrıca SQL Server kullandığından, ayrıca, hello kullandıkları aynı dizin önerileri, SQL Server müşterilerine SQL veritabanı toohelp tarafından sağlanan.

SQL Veritabanında iki otomatik ayarlama yöntemi mevcuttur:

- **[Otomatik dizin yönetimi](sql-database-automatic-tuning.md#automatic-index-management)**: Veritabanınıza eklenmesi ve veritabanınızdan kaldırılması gereken dizinleri tanımlar.
- **[Otomatik plan düzeltme](sql-database-automatic-tuning.md#automatic-plan-choice-correction)**: Sorunlu planları tanımlar ve SQL planı performans sorunlarını düzeltir (çok yakında, SQL Server 2017 ile kullanılabilir).

### <a name="adaptive-query-processing"></a>Uyarlamalı sorgu işleme

Merhaba de ekliyoruz [Uyarlamalı sorgu işleme](/sql/relational-databases/performance/adaptive-query-processing) özellikleri tooSQL tablo değerli işlevler birden fazla deyim için bir araya eklemeli yürütme dahil olmak üzere veritabanı ailesi toplu iş modu bellek grant geri bildirim ve modu Uyarlamalı birleştirmeler toplu işlem . Bu Uyarlamalı sorgu işleme özelliklerin her biri daha fazla performans sorunları ilgili toohistorically çözümü sorgu iyileştirme sorunların çözümüne yardımcı benzer "öğrenin ve uyum" teknikleri uygulanır.

### <a name="intelligent-threat-detection"></a>Akıllı tehdit algılama

 [SQL tehdit algılama](sql-database-threat-detection.md) yararlanır [SQL veritabanı denetimi](sql-database-auditing.md) toocontinuously İzleyici Azure SQL veritabanları için zararlı deneme tooaccess hassas verileri. SQL tehdit algılama müşteriler toodetect sağlar ve güvenlik uyarıları anormal etkinlikler sağlayarak göründüklerinde toopotential tehditlerine yanıt güvenliği, yeni bir katman sağlar. Şüpheli veritabanı etkinlikleri, potansiyel açıklar, SQL ekleme saldırıları ve anormal veritabanı erişim modellerinin tespit edilmesi halinde kullanıcılar uyarılır. Algılama uyarıları şüpheli etkinlik ayrıntılarını sağlayın ve eylem nasıl önerilir SQL tehdit tooinvestigate ve hello tehdidi azaltmak. Merhaba olay girişimi tooaccess sonuçlarından ihlal ya da hello veritabanındaki verileri yararlanma kullanıcılar hello şüpheli olayları toodetermine keşfedebilirsiniz. Tehdit algılama basit tooaddress olası tehditler toohello veritabanı hello gerek toobe güvenlik Uzman olmadan kolaylaştırır veya sistemleri izleme Gelişmiş Güvenlik yönetin.

## <a name="advanced-security-and-compliance"></a>Gelişmiş koruma ve uyumluluk

SQL veritabanı sağlayan bir dizi [yerleşik güvenlik ve uyumluluk özellikleri](sql-database-security-overview.md) toohelp uygulamanızı çeşitli güvenlik ve uyumluluk gereksinimlerini karşılamak. 

### <a name="auditing-for-compliance-and-security"></a>Uyumluluk ve güvenlik denetimi

[SQL veritabanı denetimi](sql-database-auditing.md) veritabanı olaylarını izler ve bunları Azure depolama hesabınızdaki tooan denetim günlüğünü yazar. Denetim mevzuatla uyumluluk, veritabanı etkinliğini anlama ve işletme sorunlarını veya şüpheli güvenlik ihlallerini işaret edebilecek farklılıklar ve anormal durumlar hakkında öngörü sahip olmanıza yardımcı olabilir.

### <a name="data-encryption-at-rest"></a>Bekleme sırasında veri şifrelemesi

SQL veritabanı [saydam veri şifreleme](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database) gerçek zamanlı şifreleme ve şifre çözme hello veritabanının, ilişkili yedeklemelerinizi gerçekleştirerek kötü amaçlı etkinliği hello tehdide karşı korumaya yardımcı olur ve işlem günlüğü dosyalarını bekleyen değişiklikleri toohello uygulama gerek kalmadan. Mayıs 2017'den itibaren oluşturulan tüm yeni Azure SQL veritabanları otomatik olarak saydam veri şifrelemesi (TDE) ile korunmaktadır. Depolama medyası çalınması karşı birçok uyumluluk standartlarını tooprotect gerektirdiği rest sırasında şifreleme teknolojisi kanıtlanmış SQL'in TDE var. Müşteriler hello TDE şifreleme anahtarları ve diğer gizli anahtarları Azure anahtar kasası kullanarak bir güvenli ve uyumlu şekilde yönetebilirsiniz.

### <a name="data-encryption-in-motion"></a>Hareket halinde veri şifrelemesi

SQL veritabanı olan hello yalnızca veritabanı sistem toooffer koruması yürütülen, REST ve sorgu ile işleme sırasında önemli verilerin [her zaman şifreli](https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-database-engine). Her zaman şifreli benzersiz veri sunan bir endüstri-ilk olan kritik verilerin hello hırsızlığı içeren ihlallerine karşı güvenlik. Örneğin, her zaman şifreli ile müşterilerin kredi kartı numaralarını hello veritabanında sorgu işleme sırasında bile her zaman, şifrelenmiş kullanım hello noktada şifre çözme verileri izin vererek, yetkili personel veya tooprocess ihtiyaç duyan uygulamalar tarafından depolanır.

### <a name="dynamic-data-masking"></a>Dinamik veri maskeleme

[SQL veritabanı dinamik veri maskeleme](sql-database-dynamic-data-masking-get-started.md) toonon ayrıcalıklı kullanıcılar maskeleyerek gizli verilerin açığa sınırlar. Dinamik veri maskeleme yardımcı olan müşteriler toodesignate etkinleştirerek yetkisiz erişim toosensitive verilerin engellemek hello hassas verileri tooreveal hello uygulama katmanı üzerinde en az etkiyle ne kadarının. Bunu hello verileri hello veritabanında değişip değişmediğini sırada, belirlenen veritabanı alanları hello hassas verileri sorgu hello sonuç kümesinde gizler ilke tabanlı güvenlik özelliğidir.

### <a name="row-level-security"></a>Satır düzeyi güvenlik

[Satır düzeyi güvenlik](https://docs.microsoft.com/sql/relational-databases/security/row-level-security) müşteriler toocontrol erişim toorows bir sorgu yürütülürken hello kullanıcı hello özellikler temelinde bir veritabanı tablosundaki sağlar (gibi grubu üyeliği veya yürütme bağlamı olarak). Satır düzeyi güvenlik (RLS) hello tasarım ve uygulamanızda güvenlik kodlama basitleştirir. RLS tooimplement kısıtlamalar veri satırı erişimi sağlar. Örneğin çalışanları ilgili tootheir departmanı olan veri satırına erişmesini ya da Müşteri'nin veri erişim tooonly hello veri ilgili tootheir şirket kısıtlama.

### <a name="azure-active-directory-integration-and-multi-factor-authentication"></a>Azure Active Directory tümleştirmesi ve çok faktörlü kimlik doğrulaması

SQL veritabanı sağlar, toocentrally veritabanı kullanıcısı ve diğer Microsoft Hizmetleri ile kimliklerini yönetmek [Azure Active Directory Tümleştirme](sql-database-aad-authentication.md). Bu özellik, izin yönetimini kolaylaştırırken güvenliği artırır. Azure Active Directory destekler [çok faktörlü kimlik doğrulaması](sql-database-ssms-mfa-authentication.md) destekleyen tek bir oturum açma işlemi sırasında (MFA) tooincrease veri ve uygulama güvenlik.

### <a name="compliance-certification"></a>Uyumluluk sertifikası

SQL Veritabanı düzenli olarak denetimden geçmektedir ve birden fazla uyumluluk standardı sertifikasına sahiptir. Merhaba daha fazla bilgi için bkz: [Microsoft Azure Trust Center](https://azure.microsoft.com/support/trust-center/), hello en güncel listesini bulabilirsiniz burada [SQL veritabanı uyumluluk sertifikalarından](https://azure.microsoft.com/support/trust-center/services/).

## <a name="easy-to-use-tools"></a>Kullanımı kolay araçlar

SQL Veritabanı uygulama oluşturma ve uygulamaların bakımını yapma işlemlerinin daha kolay ve daha verimli şekilde yapılmasını sağlar. SQL veritabanı, en iyi neler toofocus sağlar: harika uygulamaları oluşturma. Sahip olduğunuz araçları ve becerileri kullanarak SQL Veritabanı ile yönetebilir ve geliştirebilirsiniz.

- **[Azure portal hello](https://portal.azure.com/)**: tüm Azure hizmetlerini yönetmek için web tabanlı bir uygulama 
- **[SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)**: SQL Server tooSQL veritabanı ' herhangi bir SQL altyapı yönetmek için bir ücretsiz ve indirilebilir istemci uygulaması
- **[Visual Studio'daki SQL Server Veri Araçları](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)**: SQL Server ilişkisel veritabanları, Azure SQL veritabanları, Integration Services paketleri, Analysis Services veri modelleri ve Reporting Services raporları geliştirebileceğiniz ücretsiz ve indirilebilir istemci uygulaması.
- **[Visual Studio Code](https://code.visualstudio.com/docs)**: ücretsiz, indirilebilir, açık kaynaklı, Windows, macOS ve uzantılarını hello dahil olmak üzere, Linux için kod düzenleyicisini [mssql uzantısı](https://aka.ms/mssql-marketplace) Microsoft SQL Server'ı sorgulamak için Azure SQL Database ve SQL veri ambarı.

SQL veritabanı, Python, Java, Node.js, PHP, Ruby ve hello MacOS .NET, Linux ve Windows uygulamaları oluşturma destekler. SQL veritabanı destekler hello aynı [bağlantı kitaplıkları](sql-database-libraries.md) SQL sunucusu olarak.

## <a name="engage-with-hello-sql-server-engineering-team"></a>Merhaba SQL Server mühendislik ekibi ile göster

- [DBA Stack Exchange](https://dba.stackexchange.com/questions/tagged/sql-server): Veritabanı yönetimi hakkında sorular için
- [Stack Overflow](http://stackoverflow.com/questions/tagged/sql-server): Geliştirme hakkında sorular için
- [MSDN Forumları](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver): Teknik sorular için
- [Microsoft Connect](https://connect.microsoft.com/SQLServer/Feedback): Hata bildirimleri ve özellik istekleri için
- [Reddit](https://www.reddit.com/r/SQLServer/): SQL Server’ı tartışmak için

## <a name="next-steps"></a>Sonraki adımlar

- Merhaba bkz [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/sql-database/) tek veritabanı ve esnek havuzlar maliyet karşılaştırmaları ve hesaplayıcıları için.

- Bu hızlı başlattığınız tooget başlatır bakın:

  - [Hello Azure portalında bir SQL veritabanı oluşturma](sql-database-get-started-portal.md)  
  - [Hello Azure CLI ile bir SQL veritabanı oluşturma](sql-database-get-started-cli.md)
  - [PowerShell ile SQL veritabanı oluşturma](sql-database-get-started-powershell.md)

- Azure CLI ve PowerShell örnekleri için bkz.:
  - [SQL Veritabanı için Azure CLI örnekleri](sql-database-cli-samples.md)
  - [SQL Veritabanı için Azure PowerShell örnekleri](sql-database-powershell-samples.md)
