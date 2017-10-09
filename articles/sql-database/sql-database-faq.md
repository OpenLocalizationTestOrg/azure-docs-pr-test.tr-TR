---
title: "aaaAzure SQL veritabanı ile ilgili SSS | Microsoft Docs"
description: "Yanıtlar toocommon sorular müşteriler hello bulutta bir hizmet olarak bulut veritabanları ve Azure SQL Database, Microsoft'un ilişkisel veritabanı yönetim sistemine (RDBMS) ve veritabanı hakkında isteyin."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 1da12abc-0646-43ba-b564-e3b049a6487f
ms.service: sql-database
ms.custom: reference
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 02/07/2017
ms.author: sashan;carlrab
ms.openlocfilehash: 04c02f96e6e91cf314221134ee0ef6d24217ef45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-database-faq"></a>SQL Veritabanı SSS

## <a name="what-is-hello-current-version-of-sql-database"></a>SQL veritabanı'nın geçerli sürümü hello nedir?
Merhaba geçerli SQL veritabanı V12 sürümüdür. Sürüm V11 devre dışı bırakılmış.

## <a name="what-is-hello-sla-for-sql-database"></a>SQL veritabanı için başlangıç SLA nedir?
En az % 99,99 hello zaman müşterilerin kendi tek veya esnek temel, standart veya Premium Microsoft Azure SQL veritabanı ve bizim Internet ağ geçidi arasında bağlantı olacaktır garanti ediyoruz. Daha fazla bilgi için bkz: [SLA](http://azure.microsoft.com/support/legal/sla/).

## <a name="how-do-i-reset-hello-password-for-hello-server-admin"></a>Nasıl hello hello sunucu yöneticisi parolasını sıfırlama?
Merhaba, [Azure portal](https://portal.azure.com) tıklatın **SQL sunucuları**hello listeden hello sunucusunu seçin ve ardından **parola sıfırlama**.

## <a name="how-do-i-manage-databases-and-logins"></a>Veritabanlarını ve oturum açma bilgileri nasıl yönetebilirim?
Bkz: [veritabanları ve oturum açma bilgileri yönetme](sql-database-manage-logins.md).

## <a name="how-do-i-make-sure-only-authorized-ip-addresses-are-allowed-tooaccess-a-server"></a>Ne ı yalnızca yetkili IP adresleri olduğundan emin olun tooaccess izin verilen bir sunucu?
Bkz: [nasıl yapılır: SQL veritabanında güvenlik duvarı ayarlarını yapılandırma](sql-database-configure-firewall-settings.md).

## <a name="how-does-hello-usage-of-sql-database-show-up-on-my-bill"></a>SQL veritabanı hello kullanımını faturamı üzerinde nasıl göstermez?
SQL veritabanı faturaları tahmin edilebilir bir saatlik hızı üzerinde temel hello hizmet katmanı + performans on tek veritabanları veya esnek havuz başına Edtu düzeyi. Gerçek kullanım hesaplanan ve saatlik, faturanızı bir saat kesirlerini gösterebilir. böylece Faturalaması. Örneğin, 12 saat içindeki bir ay için bir veritabanı zaten varsa, faturanıza 0,5 gün kullanımını gösterir. Hizmet katmanları + performans düzeyini ve havuz başına Edtu ek olarak, bozuk out hello fatura toomake, kullanılan her bir ay içinde faturanıza veritabanı gün daha kolay toosee hello sayısı.

## <a name="what-if-a-single-database-is-active-for-less-than-an-hour-or-uses-a-higher-service-tier-for-less-than-an-hour"></a>Ne tek bir veritabanı değerinden bir saat için etkin veya daha az bir saatten daha yüksek bir hizmet katmanı kullanır?
Bir veritabanı kullanarak mevcut. her bir saat hello yüksek hizmet katmanı + performans bu saatte kullanım veya hello veritabanı değerinden bir saat için etkin olup olmadığını bağımsız olarak uygulanan düzey için faturalandırılır. Örneğin, tek bir veritabanı oluşturun ve daha sonra beş dakika silerseniz faturanızı bir veritabanı saat için bir ücret yansıtır. 

Örnekler

* Temel bir veritabanı oluşturun ve ardından hemen tooStandard S1 yükseltin, hello için hello standart S1 hızında ilk saat sizden ücret kesilir.
* 10: 00'da temel tooPremium bir veritabanı yükseltirseniz ve yükseltme 1: 35'da tamamlar 1: 00'da başlayan hello Premium hızında ücretlendirilen günü izleyen hello üzerinde 
* Premium tooBasic veritabanından 11: 00'da düşürmek varsa ve 2: 15'da tamamlandıktan sonra hello veritabanı hello Premium hızında 3: 00'a kadar geçmesi hello temel oranlarda doludur doludur.

## <a name="how-does-elastic-pool-usage-show-up-on-my-bill-and-what-happens-when-i-change-edtus-per-pool"></a>Nasıl esnek Havuz Kullanım faturamı ve değiştirdiğimde ne olacağını havuz başına Edtu görünmesini?
Esnek havuz ücretlendirilen Göster yukarı faturanızda esnek Dtu'lar (Edtu'lar) havuz başına Edtu altında gösterilen hello artışlarla [fiyatlandırma sayfası hello](https://azure.microsoft.com/pricing/details/sql-database/). Esnek havuzlar için veritabanı başına ücret ödemeden yoktur. Kullanım veya hello havuzu değerinden bir saat için etkin olup olmadığını bağımsız olarak hello en yüksek eDTU havuzu bulunduğu her saat için faturalandırılır. 

Örnekler

* Standart bir esnek havuz ile 200 Edtu'lar 11: 18'da oluşturursanız, beş veritabanları toohello havuzu ekleme, için 200 Edtu'lar hello tüm saat için 11'da başlayan ücretlendirilen Merhaba gün kalanı Hello.
* Gün 2, 5: 05'da, veritabanı 1 50 edtu'larını kullanmaya başladığında ve hello gün sürekli tutar. Veritabanları 2-5 dalgalanma gösteren 0 ile 80 Edtu'lar arasında. Merhaba günde hello gün boyunca değişen Edtu'lar tüketen beş veritabanları ekleyin. Gün 2 200 eDTU faturalandırılır tam bir günüdür. 
* Sabah üzerinde 3, 5 başka bir 15 veritabanları ekleyin. Burada tooincrease Edtu'lar 200 too400 hello havuzundan için 20: 05'da karar hello gün toohello noktası boyunca veritabanı kullanımı artırır Hello 200 eDTU düzeyinde ücretleri 8 pm kadar yürürlükte olan ve dört saat kalan hello too400 Edtu'lar artırır. 

## <a name="elastic-pool-billing-and-pricing-information"></a>Esnek havuz faturalama ve fiyatlandırma bilgileri
Esnek havuzlar özellikleri aşağıdaki hello faturalandırılır:

* Olduğunda bile hiçbir veritabanı hello havuzundaki bir esnek havuz oluşturulduktan sonra faturalandırılır.
* Bir esnek havuz saatlik faturalandırılır. Bu olduğu hello aynı tek veritabanlarının performans düzeyleri ettirilmesi sıklığı ölçümü.
* Yeniden boyutlandırılan tooa yeni bir esnek havuz ise, Edtu, ardından hello havuzu sayısı hello yeniden boyutlandırma işlemi tamamlanana kadar toohello yeni Edtu'lar miktarı göre faturalandırılır değil. Merhaba aynı tek veritabanlarını hello performans düzeyini değiştirme olarak desen izler.
* bir esnek havuz Hello bedelinin hello havuzunun edtu'larını hello sayısına dayalı olarak. bir esnek havuz Hello bedelinin hello numarası ve hello esnek veritabanları içindeki kullanımını bağımsızdır.
* Fiyat (havuz Edtu sayısı tarafından) hesaplanan x (eDTU fiyatı birimi).

Esnek havuz için Hello birim eDTU fiyat hello birim DTU fiyat hello tek bir veritabanı için daha yüksek aynı hizmet katmanı. Ayrıntılar için bkz. [SQL Veritabanı fiyatlandırması](https://azure.microsoft.com/pricing/details/sql-database/). 

toounderstand hello Edtu ve hizmet katmanları, bkz: [SQL Database seçenekleri ve performansı](sql-database-service-tiers.md).

## <a name="how-does-hello-use-of-active-geo-replication-in-an-elastic-pool-show-up-on-my-bill"></a>Nasıl hello etkin coğrafi çoğaltma faturamı üzerinde bir esnek havuz gösterisini içinde kullanıyor mu?
Kullanarak tek veritabanlarını aksine [aktif coğrafi çoğaltma](sql-database-geo-replication-overview.md) esnek veritabanları ile doğrudan bir faturalama etkisi yoktur.  Yalnızca her hello havuzları (birincil havuzu ve ikincil havuzu) için sağlanan hello edtu'ları için ücretlendirilirsiniz

## <a name="how-does-hello-use-of-hello-auditing-feature-impact-my-bill"></a>Nasıl hello özelliği etkisi denetim Merhaba faturamı kullanıyor mu?
Denetim üretilmiştir hello SQL Database hizmeti hiçbir ek maliyet ve kullanılabilir tooBasic, standart, Premium ve Premium RS veritabanları. Ancak, toostore hello denetim günlüklerini, bir Azure Storage hesabı ve tablolar ve Kuyruklar Azure Storage'da yer Fiyatlardan geçerli özellik kullanır, Denetim günlüğü hello boyutuna göre denetim hello.

## <a name="how-do-i-find-hello-right-service-tier-and-performance-level-for-single-databases-and-elastic-pools"></a>Tek veritabanları ve esnek havuzlar için hello doğru hizmet katmanını ve performans düzeyini nasıl bulurum?
Bazı araçlar kullanılabilir tooyou vardır. 

* Şirket içi veritabanları için hello kullanın [DTU boyutlandırma Danışmanı](http://dtucalculator.azurewebsites.net/) toorecommend hello veritabanları ve gerekli Dtu'lar ve esnek havuzlar için birden çok veritabanı değerlendirin.
* Tek bir veritabanı için bir havuzda olmaktan yararlı kullanıyorsanız, garanti eder bir geçmiş kullanımı desen görürse Azure'un akıllı altyapısı bir esnek havuz önerir. Bkz: [İzleyici ve hello Azure portal ile bir esnek havuzunu yönetme](sql-database-elastic-pool-manage-portal.md). Nasıl toodo hello matematik kendiniz hakkında daha fazla bilgi için bkz [esnek havuzlar için fiyat ve performans konuları](sql-database-elastic-pool.md)
* toosee yukarı veya aşağı toodial tek bir veritabanı gerekip gerekmediğini görmek [tek veritabanları için performans rehberi](sql-database-performance-guidance.md).

## <a name="how-often-can-i-change-hello-service-tier-or-performance-level-of-a-single-database"></a>Tek bir veritabanının hello hizmet katmanı veya performans düzeyi ne sıklıkta değiştirebilir miyim?
Merhaba hizmet Katmanı (temel, standart, Premium ve Premium RS arasında) değiştirebilir veya bir hizmet katmanına (örneğin, S1 tooS2) içindeki performans düzeyi istediğiniz sıklıkta hello. Önceki sürüm veritabanları için 24 saatlik bir dönemde dört kez toplam hello hizmet katmanı veya performans düzeyini değiştirebilirsiniz.

## <a name="how-often-can-i-adjust-hello-edtus-per-pool"></a>Merhaba Edtu havuzu başına ne sıklıkta göre ayarlayabilirsiniz?
Sıklıkta istiyor.

## <a name="how-long-does-it-take-toochange-hello-service-tier-or-performance-level-of-a-single-database-or-move-a-database-in-and-out-of-an-elastic-pool"></a>Ne kadar süreyle bu toochange hello hizmet katmanı veya performans düzeyi tek bir veritabanının zaman alabilir veya veritabanını bir esnek havuz ve bu moddan taşıma?
Bir veritabanı Hello Hizmet katmanını değiştirmeyi ve giriş ve çıkış havuzu taşıma arka plan işlemi olarak hello platformunda kopyalanan hello veritabanı toobe gerektirir. Değişen hello hizmet katmanı hello veritabanları hello boyutunu bağlı olarak birkaç dakika tooseveral saat sürebilir. Her iki durumda da hello veritabanları hello taşıma işlemi sırasında çevrimiçi ve kullanılabilir olmaya devam eder. Tek veritabanları değiştirme hakkında daha fazla bilgi için bkz [değişiklik hello bir veritabanının Hizmet katmanını](sql-database-service-tiers.md). 

## <a name="when-should-i-use-a-single-database-vs-elastic-databases"></a>Tek bir veritabanının esnek veritabanları ve ne zaman kullanmalıyım?
Genel olarak, esnek havuzlar için tipik bir tasarlanmış [hizmet olarak yazılım (SaaS) uygulama düzeni](sql-database-design-patterns-multi-tenancy-saas-applications.md), müşteri veya Kiracı başına tek bir veritabanı olduğu. Her veritabanı verimli maliyet genelde satın alma tek veritabanlarını ve işleminin toomeet hello değişken ve en yüksek talep. Havuzlarıyla, hello toplu performans hello havuzunun yönetin ve hello veritabanları yukarı ve aşağı otomatik olarak ölçeklendirin. Kullanım deseniyle garanti eder, azure'nın akıllı altyapısı veritabanları için bir havuz önerir. Ayrıntılar için bkz [esnek havuz Kılavuzu](sql-database-elastic-pool.md).

## <a name="what-does-it-mean-toohave-up-too200-of-your-maximum-provisioned-database-storage-for-backup-storage"></a>Ne toohave too200% en fazla sağlanan veritabanı deponuzda Yedekleme depolaması için anlama geliyor?
Yedekleme depolama hello depolama için kullanılan otomatik veritabanı yedeklerinizi ile ilişkili olan [noktası-içinde--geri yükleme](sql-database-recovery-using-backups.md#point-in-time-restore) ve [coğrafi geri yükleme](sql-database-recovery-using-backups.md#geo-restore). En fazla sağlanan veritabanı deponuzda hiçbir ek ücret ödemeden yedekleme depolama too200% Microsoft Azure SQL veritabanı sağlar. Örneğin, bir standart DB örneğini sağlanan bir veritabanı boyutu ile 250 GB varsa, 500 GB ek ücret ödemeden yedekleme depolama ile sağlanır. Veritabanınızı yedekleme depolama sağlanan hello aşarsa, Azure desteği ile iletişim kurarak tooreduce hello saklama dönemi seçin veya standart okuma erişimli coğrafi olarak yedekli depolama (RA-GRS) oranı faturalandırılır hello fazladan Yedekleme depolaması için ödeme yaparsınız. RA-GRS faturalama hakkında daha fazla bilgi için depolama fiyatlandırma ayrıntıları bakın.

## <a name="im-moving-from-webbusiness-toohello-new-service-tiers-what-do-i-need-tooknow"></a>Neler Web/iş toohello yeni hizmet katmanları, taşıma tooknow gerekir?
Azure SQL Web ve işletme veritabanları artık kullanımdan kaldırıldı. Merhaba temel, standart, Premium, Premium RS ve esnek katmanları Web ve işletme veritabanları devre dışı bırakma hello değiştirin. 

## <a name="what-is-an-expected-replication-lag-when-geo-replicating-a-database-between-two-regions-within-hello-same-azure-geography"></a>Coğrafi çoğaltma veritabanı içinde iki bölgeler arasında bir hello olduğunda aynı beklenen çoğaltma gecikmesi nedir Azure Coğrafya?
Biz şu anda beş saniyede bir RPO destekleyen hello coğrafi-ikincil Azure eşleştirilmiş bölge önerilen hello barındırıldığında hello çoğaltma gecikmesi değerden olmuştur ve hello aynı hizmet katmanını.

## <a name="what-is-an-expected-replication-lag-when-geo-secondary-is-created-in-hello-same-region-as-hello-primary-database"></a>Beklenen çoğaltma gecikmesi nedir coğrafi ikincil hello oluşturulduğunda ve aynı bölge hello birincil veritabanı olarak?
Ampirik verilerini temel alarak yok içi bölge ve arası bölge çoğaltma gecikmesi çok fazla birbirinden Azure eşleştirilmiş bölge önerilen hello kullanıldığında. 

## <a name="if-there-is-a-network-failure-between-two-regions-how-does-hello-retry-logic-work-when-geo-replication-is-set-up"></a>İki bölgeler arasında bir ağ hatası varsa, coğrafi çoğaltma ayarlarken hello yeniden deneme mantığı nasıl çalışır?
Bir bağlantıyı kes varsa, her 10 saniye toore tekrar-bağlantı kurabilir.

## <a name="what-can-i-do-tooguarantee-that-a-critical-change-on-hello-primary-database-is-replicated"></a>Merhaba birincil veritabanı üzerinde önemli bir değişiklik çoğaltılır tooguarantee ne yapabilirim?
Merhaba coğrafi-ikincil bir zaman uyumsuz çoğaltma ve tookeep çalışmayın hello birincil ile tam eşitleme içinde. Ancak, önemli değişiklikler yöntemi tooforce eşitleme tooensure hello çoğaltması (örneğin, parola güncelleştirmeleri) sağlıyoruz. Tüm kaydedilmiş işlemleri çoğaltılana hello çağıran iş parçacığı engellediğinden zorlanmış eşitleme performansını etkiler. Ayrıntılar için bkz [sp_wait_for_database_copy_sync](https://msdn.microsoft.com/library/dn467644.aspx). 

## <a name="what-tools-are-available-toomonitor-hello-replication-lag-between-hello-primary-database-and-geo-secondary"></a>Hangi Araçlar kullanılabilir toomonitor hello çoğaltma gecikmesi hello birincil veritabanı ile coğrafi ikincil arasında var mı?
Biz hello gerçek zamanlı çoğaltma gecikmesi hello birincil veritabanı ile coğrafi-ikincil bir DMV aracılığıyla arasında kullanıma sunar. Ayrıntılar için bkz [sys.dm_geo_replication_link_status](https://msdn.microsoft.com/library/mt575504.aspx).

## <a name="toomove-a-database-tooa-different-server-in-hello-same-subscription"></a>toomove veritabanı tooa içinde farklı bir sunucuya hello aynı abonelik
* Merhaba, [Azure portal](https://portal.azure.com), tıklatın **SQL veritabanları**hello listesinden bir veritabanı seçin ve ardından **kopya**. Bkz: [bir Azure SQL veritabanını kopyalama](sql-database-copy.md) daha fazla ayrıntı için.

## <a name="toomove-a-database-between-subscriptions"></a>toomove abonelikler arasında bir veritabanı
* Merhaba, [Azure portal](https://portal.azure.com), tıklatın **SQL sunucuları** ve veritabanınızı hello listeden barındıran hello sunucu seçin. Tıklatın **taşıma**ve ardından hello kaynakları toomove ve hello abonelik toomove seçin.
