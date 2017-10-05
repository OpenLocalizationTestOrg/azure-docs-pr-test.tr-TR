---
title: "Tasarım Azure SQL veritabanı kullanarak yüksek oranda kullanılabilir hizmet | Microsoft Docs"
description: "Uygulama tasarımı için Azure SQL veritabanı kullanarak yüksek oranda kullanılabilir hizmetler hakkında bilgi edinin."
keywords: "Bulut olağanüstü durum kurtarma, olağanüstü durum kurtarma çözümleri, uygulama veri yedekleme, coğrafi çoğaltma, iş sürekliliği planlama"
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: e8a346ac-dd08-41e7-9685-46cebca04582
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 04/21/2017
ms.author: sashan
ms.openlocfilehash: 40fe0ae04eb94322356ed19773512e3bc383639c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="designing-highly-available-services-using-azure-sql-database"></a>Azure SQL veritabanı kullanarak yüksek oranda kullanılabilir hizmetler tasarlama

Derleme ve Azure SQL veritabanı yüksek oranda kullanılabilir hizmetleri dağıtma, kullandığınız [yük devretme grupları ve etkin coğrafi çoğaltma](sql-database-geo-replication-overview.md) bölgesel arızalara ve geri dönülemez kesintileri esnekliği sağlar ve Hızlı Kurtarma etkinleştirmek için ikincil veritabanları. Bu makale üzerinde ortak uygulama düzenleri odaklanır ve avantajları ve dengelemeler hedefleme, hizmet düzeyi sözleşmesi uygulama dağıtım gereksinimlerine bağlı olarak her seçenekle ele almaktadır trafiği gecikme ve maliyetlerin. Esnek havuzlar etkin coğrafi çoğaltma hakkında daha fazla bilgi için bkz: [esnek havuz olağanüstü durum kurtarma stratejilerini](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md).

## <a name="design-pattern-1-active-passive-deployment-for-cloud-disaster-recovery-with-a-co-located-database"></a>Tasarım deseni 1: Aktif-Pasif dağıtım birlikte bulunan bir veritabanı ile bulut olağanüstü durum kurtarma
Bu seçenek aşağıdaki özelliklere sahip uygulamalar için uygundur:

* Tek bir Azure bölgesindeki etkin örneği
* Veri okuma-yazma (RW) erişimi güçlü bağımlılığı
* Bölgeler arası bağlantı web uygulaması ve veritabanı arasındaki gecikme süresi ve trafik maliyet nedeniyle kabul edilebilir değil    

Bu durumda, uygulama dağıtım topolojisi tüm uygulama bileşenleri etkilendiğini ve yük devretme birimi olarak gerektiğinde bölgesel afetler işlemek için optimize edilmiştir. Coğrafi artıklık için uygulama mantığını ve veritabanı başka bir bölgeye çoğaltılır, ancak normal koşullar altında uygulama iş yükü için kullanılmaz. İkincil bölge uygulamada bir ikincil veritabanına SQL bağlantı dizesi kullanmak için yapılandırılmalıdır. Trafik Yöneticisi kullanmak üzere ayarlandı [yük devretme yönlendirme yöntemini](../traffic-manager/traffic-manager-configure-failover-routing-method.md).  

> [!NOTE]
> [Azure trafik Yöneticisi](../traffic-manager/traffic-manager-overview.md) bu makalede yalnızca gösterim amacıyla kullanılmıştır. Yük devretme yönlendirme yöntemini destekleyen hiçbir yük dengeleme çözümü kullanabilirsiniz.    
>

Aşağıdaki diyagramda bu yapılandırma bir kesinti önce gösterir.

![SQL Database coğrafi çoğaltma yapılandırması. Bulut olağanüstü durum kurtarma.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern1-1.png)

Birincil bölgede kesinti sonrasında, SQL veritabanı hizmetinin birincil veritabanı erişilebilir değil ve otomatik yük devretme İlkesi parametrelere bağlı olarak ikincil veritabanı için bir yük devretme tetiklemek algılar. Uygulama SLA bağlı olarak, kesinti algılanmasını ve yük devretme kendisi arasında bir yetkisiz kullanım süresi yapılandırmak karar verebilirsiniz. Yetkisiz kullanım süresi yapılandırma burada kesinti yıkıcı ve kullanılabilirlik bölgede hızlı bir şekilde geri yüklenemez durumlarda veri kaybı riskini azaltır. Yük devretme grubu veritabanının yük devretmeyi tetikler önce uç nokta yük devretme trafik Yöneticisi tarafından başlatılır, web uygulaması veritabanına yeniden mümkün değildir. Veritabanı yük devretme tamamlandıktan hemen sonra uygulamanın otomatik olarak yeniden denemesi başarılı olur. 

> [!NOTE]
> Uygulama ve veritabanlarının tam olarak Eşgüdümlü yük devretme elde etmek için izleme yönteminizi insanlara ve web uygulama uç ve veritabanlarını el ile yük devretme kullanmanız gerekir.
>

Uygulama uç noktaları ve veritabanı için yük devretme işlemi tamamlandıktan sonra uygulama B bölgede kullanıcı isteklerini işleme yeniden başlar ve birincil veritabanı artık B. bölgede olduğundan veritabanı ile birlikte bulunan kalacak Bu senaryo aşağıdaki çizimde gösterilmiştir. Tüm diyagramlarındaki Kesiksiz çizgi etkin bağlantıları göstermek, noktalı çizgiler askıya alınmış bağlantıları gösterir ve eylem Tetikleyicileri Durma işareti gösterir.

![Coğrafi çoğaltma: Yük devretme ikincil veritabanına. Uygulama verileri yedekleme.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern1-2.png)

İkincil bölge'de bir kesinti oluşursa, birincil ve ikincil veritabanı arasındaki çoğaltma bağlantısını askıya alındı ancak birincil veritabanı etkilenmez çünkü yük devretme tetiklenmez. Uygulama kullanılabilirliği bu durumda, değiştirilmez ancak uygulama gösterilen çalışır ve bu nedenle durumda yüksek risk art arda iki bölgeler başarısız.

> [!NOTE]
> Olağanüstü durum kurtarma için iki bölgede uygulama dağıtımı sınırlı yapılandırmayla öneririz. Azure farklı coğrafyalara çoğunu yalnızca iki bölgede sahip olmasıdır. Bu yapılandırma, uygulamanızın hem bölgeler bir eşzamanlı geri dönülemez hatasından koruma sağlamaz.  Bu tür bir hatanın olası olayda, veritabanlarınızı üçüncü bölge kullanarak kurtarabilirsiniz [coğrafi geri yükleme işlemi](sql-database-disaster-recovery.md#recover-using-geo-restore).
>

Kesinti azaltıldığından sonra ikincil veritabanı otomatik olarak birincil ile yeniden eşitler. Eşitleme sırasında birincil performansını eşitlenmesi için gereken veri miktarı bağlı olarak biraz etkilenebilir. Aşağıdaki diyagram, kesinti ikincil bölge içinde gösterir.

![İkincil veritabanının birincil ile eşitlenmiş. Bulut olağanüstü durum kurtarma.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern1-3.png)

Anahtar **avantajları** bu tasarım modeli şunlardır:

* Aynı web uygulamasını hem bölgeler herhangi bir bölgeye özgü yapılandırma ve yük devretmeyi tepki vermek için ilave bir mantık olmadan dağıtılır. 
* Yük devretme web uygulaması olarak uygulama performansı etkilenmez ve veritabanı birlikte bulunan her zaman.

Ana **kolaylığını** ikincil bölge olarak yedekli uygulama örneğinde yalnızca olağanüstü durum kurtarma için kullanılan.

## <a name="design-pattern-2-active-active-deployment-for-application-load-balancing"></a>Tasarım deseni 2: uygulama Yük Dengeleme için etkin-etkin dağıtım
Bu bulut olağanüstü durum kurtarma seçeneğini aşağıdaki özelliklere sahip uygulamalar için uygundur:

* Veritabanı okuma yazma işlemleri için yüksek oranı
* Veritabanı yazma gecikmesi için son kullanıcı deneyimi daha önemli okuma gecikmesi 
* Farklı bir bağlantı dizesi kullanarak, salt okunur mantığı okuma-yazma mantığından ayrılabilir
* Salt okunur mantığı en son güncelleştirmeleri ile tam olarak eşitlenmekte olan veriler üzerinde bağlı değildir  

Bu özelliklere uygulamalarınız varsa, son kullanıcı bağlantıları arasında birden fazla uygulama örneğinin de farklı bölgelerdeki dengelemesini genel son kullanıcı deneyimi önemli ölçüde artırabilir. İki bölgelerinin DR çifti olarak seçilmesi gerekir ve yük devretme grubu bu bölgede veritabanlarını içermelidir. Yük Dengeleme uygulamak için her bölge uygulama etkin bir örneği yük devretme grubunun okuma-yazma dinleyicisi uç noktasına bağlı okuma-yazma (RW) mantığı ile olmalıdır. Birincil veritabanında bir kesinti durumunda etkilenip, yük devretme'nin otomatik olarak başlatılan garanti. Salt okunur mantık (RO) web uygulaması, bu bölgedeki veritabanına doğrudan bağlanmanız gerekir. Trafik Yöneticisi ayarlanmalıdır kullanmak için [performans yönlendirme](../traffic-manager/traffic-manager-configure-performance-routing-method.md) ile [uç nokta izleme](../traffic-manager/traffic-manager-monitoring.md) her bir uygulama örneği için etkinleştirilmiş.

#1 deseniyle olduğu gibi benzer bir izleme uygulaması dağıtmayı düşünmelisiniz. Ancak #1 deseniyle izleme uygulama uç nokta yük devretme tetiklemek için sorumlu olmaz.

> [!NOTE]
> Bu deseni birden fazla ikincil veritabanı kullanıyor, ancak ikincil bölge b yalnızca yük devretme için kullanılacak ve yük devretme grubunun bir parçası olması gerekir.
>

Trafik Yöneticisi performansı doğrudan kullanıcının coğrafi konuma yakın uygulama örneği için kullanıcı bağlantılar için yönlendirme için yapılandırılmalıdır. Aşağıdaki diyagramda bu yapılandırma bir kesinti önce gösterilmektedir.

![Hiçbir kesinti: performans için en yakın uygulama yönlendirme. Coğrafi çoğaltma.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern2-1.png)

Bir bölgede bir veritabanı kesinti algılanırsa, yük devretme grubu otomatik olarak B. bölgede ikincil bir bölgeye birincil veritabanının yük devretmesi başlatır Okuma-yazma bağlantıları web uygulamasında değil etkilenecek şekilde bölge B okuma-yazma dinleyicisi uç nokta da otomatik olarak güncelleştirilecektir. Trafik Yöneticisi çevrimdışı son nokta yönlendirme tablosundan dışlayacak ancak geri kalan çevrimiçi örneklerine son kullanıcı trafik yönlendirme devam eder. Bunlar her zaman aynı bölgede veritabanı üzerine gibi salt okunur SQL bağlantı dizelerini etkilenmiş değil. 

Aşağıdaki diyagram, yük devretme sonrasında yeni yapılandırmayı gösterir.

![Yük devretme sonrasında yapılandırması. Bulut olağanüstü durum kurtarma.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern2-2.png)

İkincil bölgeler birinde kesinti durumunda, trafik Yöneticisi otomatik olarak çevrimdışı uç noktası bu bölgede yönlendirme tablosundan kaldırır. Bu bölgede ikincil veritabanı çoğaltma kanala askıya alınır. Kalan bölgeleri Bu senaryoda ek kullanıcı trafiği aldığından sırasında kesinti uygulamanızın performansı etkilenir. Kesinti azaltıldığından sonra etkilenen bölgede ikincil veritabanı hemen birincil ile eşitlenir. Eşitleme sırasında birincil performansını eşitlenmesi için gereken veri miktarı bağlı olarak biraz etkilenebilir. Aşağıdaki diyagram kesinti B. bölgede gösterir

![Kesinti ikincil bölge içinde. Olağanüstü durum kurtarma - coğrafi çoğaltma bulut.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern2-3.png)

Anahtar **avantajı** bu düzeni arasında birden fazla ikincil en iyi son kullanıcı performans elde etmek için uygulama iş yükü ölçeklendirebilirsiniz tasarımdır. **Dengelerin** bu seçeneği şunlardır:

* Uygulama örnekleri ile veritabanı arasındaki okuma-yazma bağlantıları değişen gecikme süresi ve maliyet gerekir
* Kesinti sırasında uygulama performansı etkilenir

> [!NOTE]
> Benzer bir yaklaşım, raporlama işleri, iş zekası araçları veya yedekleme gibi özelleştirilmiş iş yükleri boşaltmak için kullanılabilir. Genellikle, bu iş yükleri önemli veritabanı kaynaklarını tüketebilir bu nedenle, ikincil veritabanlarından birini kendileri için beklenen iş yükü için eşleşen performans düzeyiyle atamanız önerilir.
>

## <a name="design-pattern-3-active-passive-deployment-for-data-preservation"></a>Tasarım deseni 3: Aktif-Pasif dağıtımı için veri koruma
Bu seçenek aşağıdaki özelliklere sahip uygulamalar için uygundur:

* Tüm veri kayıplarını yüksek iş sorununa neden olur. Kesinti yıkıcı ise veritabanı yük devretme yalnızca son çare olarak kullanılabilir.
* Uygulama işlemlerinin salt okunur ve okuma-yazma modlarını destekler ve "salt okunur modda" bir süre çalışabilir.

Okuma-yazma bağlantı zaman aşımı hataları alma başlattığınızda bu modelinde uygulama salt okunur moda geçer. Web uygulaması hem bölgelere dağıtılan ve okuma-yazma dinleyicisi uç noktası bağlantısı ve salt okunur dinleyicisi uç noktası için farklı bağlantı içerir. Trafik Yöneticisi'ni kullanmak için ayarlanması gereken [yük devretme yönlendirme](../traffic-manager/traffic-manager-configure-failover-routing-method.md) ile [uç nokta izleme](../traffic-manager/traffic-manager-monitoring.md) her bölgede uygulama uç noktası için etkinleştirilmiş.

Aşağıdaki diyagramda bu yapılandırma bir kesinti önce gösterilmektedir.

![Yük devretme önce Aktif-Pasif dağıtımı. Bulut olağanüstü durum kurtarma.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern3-1.png)

Trafik Yöneticisi bir bölge için bir bağlantı hatası algıladığında, bu otomatik olarak kullanıcı trafiğinin B. bölgede uygulama örneğine geçer Bu desen ile veri kaybı yetkisiz kullanım süresi yeterince yüksek bir değere örneğin 24 saat ayarladığınız önemlidir. Bu süre içinde kesinti azaltıldığından, veri kaybı önlenmiş olur sağlayacaktır. Web uygulaması B bölgede etkinleştirildiğinde okuma-yazma işlemleri başarısız olmaya başlar. Bu noktada, salt okunur moda geçmesi. Bu modda istekleri otomatik olarak ikincil veritabanına yönlendirilir. Yıkıcı bir hata durumunda hizmet kesintisi yetkisiz kullanım süresi içinde azaltılması gereken değil ve yük devretme grubu yük devretmeyi tetikler. Sonra okuma-yazma dinleyicisi kullanılabilir olacağı ve başarısız olan çağrılar durdurur. Bu tarafından Aşağıdaki diyagramda gösterilmiştir.

![Kesinti: Uygulama salt okunur modda. Bulut olağanüstü durum kurtarma.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern3-2.png)

Kesinti birincil bölge içinde yetkisiz kullanım süresi içinde azaltılan, trafik Yöneticisi bağlantı geri birincil bölgede algılar ve kullanıcı trafiğinin A. bölgede uygulama örneğine geri geçer Bu uygulama örneği sürdürür ve birincil veritabanı A. bölgede kullanarak okuma-yazma modunda çalışır

Uygulama uç noktası B bölgede başarısızlığını ve yük devretme grubu anahtarları salt okunur dinleyicisi bölgeye a B bölgede kesinti durumunda, trafik Yöneticisi algılar Bu kesinti için son kullanıcı deneyimi olumsuz etkilemez ancak birincil veritabanı kesinti sırasında sunulur. Bu tarafından Aşağıdaki diyagramda gösterilmiştir.

![Kesinti: İkincil veritabanı. Bulut olağanüstü durum kurtarma.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern3-3.png)

Kesinti azaltıldığından sonra ikincil veritabanını hemen birincil ile eşitlenir ve salt okunur dinleyicisi B. bölgede ikincil veritabanına geri çevrilir Eşitleme sırasında birincil performansını eşitlenmesi için gereken veri miktarı bağlı olarak biraz etkilenebilir.

Bu tasarım deseni vardır **avantajları**:

* Geçici kesintileri sırasında veri kaybı ortadan kaldırır.
* Kapalı kalma süresi yalnızca nasıl hızlı bir şekilde trafik Yöneticisi yapılandırılabilir bağlantı hatası algılar üzerinde bağlıdır.

**Kolaylığını** değil:

* Uygulamanın salt okunur modda çalışabilir olması gerekir.

> [!NOTE]
> Bir kalıcı hizmet kesintisi bölgede olması durumunda, el ile veritabanı yük devretme etkinleştirmek ve veri kaybını kabul edin. Uygulama veritabanı için okuma-yazma erişimi olan ikincil bölge işlevsel olacaktır.
>

## <a name="business-continuity-planning-choose-an-application-design-for-cloud-disaster-recovery"></a>İş sürekliliği planlama: Bulut olağanüstü durum kurtarma için bir uygulama tasarımı seçin
Özel bulut olağanüstü durum kurtarma stratejiniz birleştirebilir veya en iyi uygulamanızın ihtiyaçlarını karşılamak için bu tasarım desenleri genişletir.  Daha önce belirtildiği gibi seçtiğiniz stratejisi müşterileriniz ve uygulama dağıtım topolojisi sunmak isteyebilirsiniz SLA temel alır. Kararınızı rehberlik için aşağıdaki tabloda, tahmini veri kaybı tabanlı seçenekleri karşılaştırılmaktadır veya kurtarma noktası hedefi (RPO) ve tahmini kurtarma süresi (Ekle).

| düzeni | RPO | EKLE |
|:--- |:--- |:--- |
| Aktif-Pasif dağıtım birlikte bulunan veritabanı erişimi olan olağanüstü durum kurtarma |Okuma-yazma erişimi < 5 saniye |Hata algılama süresi + DNS TTL |
| Uygulama Yük Dengeleme için etkin-etkin dağıtım |Okuma-yazma erişimi < 5 saniye |Hata algılama süresi + DNS TTL |
| Veri koruma için Aktif-Pasif dağıtımı |Salt okunur erişim < 5 saniye | Salt okunur erişim = 0 |
||Okuma-yazma erişimi sıfır = | Okuma-yazma erişimi = hatası algılama zamanı + veri kaybı yetkisiz kullanım süresi |
|||

## <a name="next-steps"></a>Sonraki adımlar
* Veritabanı Yedeklemeleri otomatik Azure SQL hakkında bilgi edinmek için bkz: [SQL veritabanı otomatik yedeklemeler](sql-database-automated-backups.md)
* İş sürekliliğine genel bakış ve senaryolar için bkz: [iş sürekliliğine genel bakış](sql-database-business-continuity.md)
* Kurtarma için otomatik yedeklemeler kullanma hakkında bilgi edinmek için bkz: [bir veritabanı hizmeti tarafından başlatılan yedeklerden geri yükleme](sql-database-recovery-using-backups.md)
* Daha hızlı kurtarma seçenekleri hakkında bilgi edinmek için [aktif coğrafi çoğaltma](sql-database-geo-replication-overview.md)  
* Arşivleme için otomatik yedeklemeler kullanma hakkında bilgi edinmek için bkz: [veritabanı kopyalama](sql-database-copy.md)
* Esnek havuzlar etkin coğrafi çoğaltma hakkında daha fazla bilgi için bkz: [esnek havuz olağanüstü durum kurtarma stratejilerini](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md).
