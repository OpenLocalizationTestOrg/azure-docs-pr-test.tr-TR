---
title: "Azure SQL veritabanı kullanarak aaaDesign yüksek oranda kullanılabilir hizmet | Microsoft Docs"
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
ms.openlocfilehash: 815f754ba7014cd8a1108a2d84c2a8f71d7030a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="designing-highly-available-services-using-azure-sql-database"></a>Azure SQL veritabanı kullanarak yüksek oranda kullanılabilir hizmetler tasarlama

Derleme ve Azure SQL veritabanı yüksek oranda kullanılabilir hizmetleri dağıtma, kullandığınız [yük devretme grupları ve etkin coğrafi çoğaltma](sql-database-geo-replication-overview.md) tooprovide esnekliği tooregional hataları ve geri dönülemez kesintiler ve etkinleştirme Hızlı Kurtarma toohello ikincil veritabanları. Bu makale üzerinde ortak uygulama düzenleri odaklanır ve hello avantajları ve dengelemeler her seçenekle hello uygulama dağıtımı gereksinimleri, hello hizmet düzeyi sözleşmesi hedefleme, bağlı olarak ele almaktadır trafiği gecikme ve maliyetlerin. Esnek havuzlar etkin coğrafi çoğaltma hakkında daha fazla bilgi için bkz: [esnek havuz olağanüstü durum kurtarma stratejilerini](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md).

## <a name="design-pattern-1-active-passive-deployment-for-cloud-disaster-recovery-with-a-co-located-database"></a>Tasarım deseni 1: Aktif-Pasif dağıtım birlikte bulunan bir veritabanı ile bulut olağanüstü durum kurtarma
Bu seçenek ile Merhaba özellikleri aşağıdaki uygulamalar için uygundur:

* Tek bir Azure bölgesindeki etkin örneği
* Okuma-yazma (RW) erişim toodata güçlü bağımlılığı
* Merhaba web uygulaması hello veritabanı arasında çapraz bölge bağlantısı toolatency ve trafik maliyeti kabul edilebilir değil    

Bu durumda, hello uygulama dağıtım topolojisi tüm uygulama bileşenleri etkilendiğini ve bir birim olarak toofailover gerektiğinde bölgesel afetler işlemek için optimize edilmiştir. Coğrafi artıklık hello uygulama mantığını ve hello veritabanı çoğaltılmış tooanother bölge ancak hello normal koşullar altında hello uygulama iş yükü için kullanılmaz. Merhaba ikincil bölge'Hello uygulamada yapılandırılan toouse SQL bağlantı dizesi toohello ikincil bir veritabanı olmalıdır. Trafik Yöneticisi toouse ayarlanmış [yük devretme yönlendirme yöntemini](../traffic-manager/traffic-manager-configure-failover-routing-method.md).  

> [!NOTE]
> [Azure trafik Yöneticisi](../traffic-manager/traffic-manager-overview.md) bu makalede yalnızca gösterim amacıyla kullanılmıştır. Yük devretme yönlendirme yöntemini destekleyen hiçbir yük dengeleme çözümü kullanabilirsiniz.    
>

Aşağıdaki diyagramda hello kesinti önce bu yapılandırma görülmektedir.

![SQL Database coğrafi çoğaltma yapılandırması. Bulut olağanüstü durum kurtarma.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern1-1.png)

Merhaba birincil bölgede kesinti sonrasında, hello SQL veritabanı hizmetinin hello birincil veritabanı erişilebilir değil ve hello otomatik yük devretme İlkesi hello parametrelere göre bir yük devretme toohello ikincil bir veritabanı tetikleyecek algılar. Uygulama SLA bağlı olarak, tooconfigure yetkisiz kullanım süresi hello kesinti hello algılanmasını ve hello yük devretme kendisi arasında bir karar verebilirsiniz. Yetkisiz kullanım süresi yapılandırma burada hello kesinti yıkıcı ve kullanılabilirlik hello bölgede hızlı bir şekilde geri yüklenemez veri kaybı toohello durumlarda hello riskini azaltır. Yük devretme hello veritabanının Hello yük devretme grubu Tetikleyicileri hello önce hello uç nokta yük devretme hello trafik Yöneticisi tarafından başlatılır, Merhaba web uygulaması mümkün tooreconnect toohello veritabanı değil. Merhaba veritabanı yük devretme tamamlandıktan hemen sonra hello uygulamanın girişimi tooreconnect otomatik olarak başarılı olur. 

> [!NOTE]
> tooachieve tam olarak Merhaba uygulaması hello veritabanları ve yük devretme Eşgüdümlü, izleme yönteminizi insanlara ve el ile yük devretme hello web uygulama uç hello veritabanları ve kullanmanız gerekir.
>

Merhaba uygulamanın uç noktaları ve birlikte hello veritabanı Hello yük devretme işlemi tamamlandıktan sonra hello uygulama B hello bölgede hello kullanıcı isteklerini işleme yeniden başlar ve hello birincil veritabanı artık olduğundan hello veritabanıyla birlikte bulunan kalır Bölge b Bu senaryo diyagramı aşağıdaki hello gösterilmiştir. Tüm diyagramlarındaki Kesiksiz çizgi etkin bağlantıları göstermek, noktalı çizgiler askıya alınmış bağlantıları gösterir ve eylem Tetikleyicileri Durma işareti gösterir.

![Coğrafi çoğaltma: Yük devretme toosecondary veritabanı. Uygulama verileri yedekleme.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern1-2.png)

Merhaba ikincil bölge'de bir kesinti oluşursa, hello hello birincil ve ikincil veritabanı hello arasındaki çoğaltma bağlantısını askıya alındı ancak hello birincil veritabanı etkilenmez çünkü hello yük devretme tetiklenmez. Merhaba uygulamanın kullanılabilirliğini bu durumda, değiştirilmez ancak Merhaba uygulaması gösterilen çalışır ve bu nedenle durumda yüksek risk art arda iki bölgeler başarısız.

> [!NOTE]
> Olağanüstü durum kurtarma için uygulama sınırlı dağıtım tootwo bölgeleriyle hello yapılandırma öneririz. Bunun nedeni çoğu, Merhaba yalnızca iki bölgede Azure coğrafyalara sahip. Bu yapılandırma, uygulamanızın hem bölgeler bir eşzamanlı geri dönülemez hatasından koruma sağlamaz.  Bu tür bir hatanın olası olayda, veritabanlarınızı üçüncü bölge kullanarak kurtarabilirsiniz [coğrafi geri yükleme işlemi](sql-database-disaster-recovery.md#recover-using-geo-restore).
>

Merhaba kesinti azaltıldığından sonra hello ikincil veritabanı otomatik olarak hello birincil ile yeniden eşitler. Eşitleme sırasında hello birincil performansını hello eşitlenen toobe gereken veri miktarı bağlı olarak biraz etkilenebilir. Merhaba Aşağıdaki diyagramda bir kesinti hello ikincil bölgede gösterilmektedir.

![İkincil veritabanının birincil ile eşitlenmiş. Bulut olağanüstü durum kurtarma.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern1-3.png)

başlangıç anahtarı **avantajları** bu tasarım modeli şunlardır:

* Merhaba aynı web herhangi bir bölgeye özgü yapılandırma ve hiçbir ek mantık tooreact toohello yük devretme olmayan dağıtılan tooboth bölgelerde uygulamasıdır. 
* Yük devretme Merhaba web uygulaması olarak Hello uygulamanızın performansı etkilenmez ve hello veritabanı birlikte bulunan her zaman.

Merhaba ana **kolaylığını** Merhaba yedekli uygulaması olan hello ikincil bölge örneğinde yalnızca olağanüstü durum kurtarma için kullanılır.

## <a name="design-pattern-2-active-active-deployment-for-application-load-balancing"></a>Tasarım deseni 2: uygulama Yük Dengeleme için etkin-etkin dağıtım
Bu bulut olağanüstü durum kurtarma seçeneği ile Merhaba özellikleri aşağıdaki uygulamalar için uygundur:

* Veritabanı yüksek oranını toowrites okur
* Veritabanı hello yazma gecikmesi için hello son kullanıcı deneyimi daha önemli okuma gecikmesi 
* Farklı bir bağlantı dizesi kullanarak, salt okunur mantığı okuma-yazma mantığından ayrılabilir
* Salt okunur mantığı hello en son güncelleştirmeleri ile tam olarak eşitlenmekte olan veriler üzerinde bağlı değildir  

Bu özelliklere uygulamalarınız varsa, yük de farklı bölgelerdeki birden çok uygulama örnekleri arasında hello son kullanıcı bağlantıları Dengeleme önemli ölçüde artırabilir hello genel son kullanıcı deneyimi. İki hello bölgelerinin DR çifti hello seçilmelidir ve hello yük devretme grubu bu bölgede hello veritabanları içermelidir. tooimplement yük dengeleyici her bölge etkin hello uygulama örneğini hello okuma-yazma (RW) bağlı mantığı toohello okuma-yazma dinleyicisi uç noktası ile Merhaba yük devretme grubunun olması gerekir. Merhaba birincil veritabanı kesinti tarafından etkilenip bu hello yük devretme otomatik olarak başlatılacak garanti. Merhaba salt okunur mantığı (RO) Merhaba web uygulaması, doğrudan bu bölgede toohello veritabanı bağlanmanız gerekir. Trafik Yöneticisi toouse ayarlanmalıdır [performans yönlendirme](../traffic-manager/traffic-manager-configure-performance-routing-method.md) ile [uç nokta izleme](../traffic-manager/traffic-manager-monitoring.md) her bir uygulama örneği için etkinleştirilmiş.

#1 deseniyle olduğu gibi benzer bir izleme uygulaması dağıtmayı düşünmelisiniz. Ancak #1 deseniyle farklı olarak, uygulama izleme hello hello uç nokta yük devretme tetiklemek için sorumlu olmaz.

> [!NOTE]
> Bu desen birden fazla ikincil veritabanı kullanıyor, ancak yalnızca ikincil bölge b'de hello yük devretme için kullanılacak ve hello yük devretme grubunun bir parçası olması gerekir.
>

Trafik Yöneticisi performansı yönlendirme toodirect hello kullanıcı bağlantıları toohello uygulama örneği yakın toohello kullanıcının coğrafi konum için yapılandırılmış olması gerekir. Aşağıdaki diyagramda hello kesinti önce bu yapılandırma gösterilmektedir.

![Hiçbir kesinti: performans yönlendirme toonearest uygulama. Coğrafi çoğaltma.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern2-1.png)

A hello bölgede bir veritabanı kesinti algılanırsa, hello yük devretme grubu b bölgede ikincil bölge A toohello hello birincil veritabanı yük devretme otomatik olarak başlatır Okuma-yazma bağlantıları hello web uygulamasında değil etkilenecek şekilde hello okuma-yazma dinleyicisi uç nokta tooregion B da otomatik olarak güncelleştirir. Merhaba trafik Yöneticisi hello çevrimdışı son nokta hello yönlendirme tablosundan dışlayacak ancak Yönlendirme hello son kullanıcı trafiği toohello kalan çevrimiçi örnekleri devam eder. her zaman toohello veritabanı hello işaret edecek şekilde hello salt okunur SQL bağlantı dizelerini etkilenecek değil aynı bölgede. 

Aşağıdaki diyagramda hello hello yeni yapılandırmayı hello yük devretme sonrasında göstermektedir.

![Yük devretme sonrasında yapılandırması. Bulut olağanüstü durum kurtarma.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern2-2.png)

Merhaba ikincil bölgeler birinde kesinti durumunda, hello trafik Yöneticisi otomatik olarak hello çevrimdışı uç noktası bu bölgede hello yönlendirme tablosundan kaldırır. Merhaba çoğaltma kanal toohello ikincil veritabanı bu bölgede askıya alınır. Merhaba kalan bölgeleri Bu senaryoda ek kullanıcı trafiği aldığından hello kesintisi sırasında hello uygulamanızın performansı etkilenir. Merhaba kesinti azaltıldığından sonra hello hello etkilenen bölgede ikincil veritabanı hemen hello birincil ile eşitlenir. Merhaba sırasında hello birincil eşitleme performansını eşitlenen toobe gereken veri miktarı hello bağlı olarak biraz etkilenebilir. B. bölgede bir kesinti diyagramı aşağıdaki hello gösterir

![Kesinti ikincil bölge içinde. Olağanüstü durum kurtarma - coğrafi çoğaltma bulut.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern2-3.png)

başlangıç anahtarı **avantajı** bu düzeni birden fazla ikincil kopya tooachieve hello en iyi son kullanıcı performans arasında hello uygulama iş yükü ölçeklendirebilirsiniz tasarımdır. Merhaba **dengelerin** bu seçeneği şunlardır:

* Okuma-yazma bağlantıları hello uygulama örnekleri ile veritabanı arasında değişen gecikme süresi ve maliyet gerekir
* Merhaba kesintisi sırasında uygulama performansı etkilenir

> [!NOTE]
> Benzer bir yaklaşım kullanılabilir toooffload özelleştirilmiş raporlama işleri, iş zekası araçları veya yedekleme gibi iş yükleri. Genellikle, bu iş yükleri önemli veritabanı kaynaklarını tüketebilir bu nedenle, hello birini ikincil veritabanları için hello performans düzeyi eşleşen toohello beklenen iş yükü ile atamanız önerilir.
>

## <a name="design-pattern-3-active-passive-deployment-for-data-preservation"></a>Tasarım deseni 3: Aktif-Pasif dağıtımı için veri koruma
Bu seçenek ile Merhaba özellikleri aşağıdaki uygulamalar için uygundur:

* Tüm veri kayıplarını yüksek iş sorununa neden olur. Merhaba kesinti yıkıcı ise hello veritabanı yük devretme yalnızca son çare olarak kullanılabilir.
* Merhaba uygulaması işlemlerinin salt okunur ve okuma-yazma modlarını destekler ve "salt okunur modda" bir süre çalışabilir.

Merhaba okuma-yazma bağlantı zaman aşımı hataları alma başlattığınızda bu modelinde Merhaba uygulaması yalnızca tooread moda geçer. Merhaba Web uygulaması dağıtılan tooboth bölgeleri ve bağlantı toohello okuma-yazma dinleyicisi bitiş noktası ve farklı bir bağlantı toohello salt okunur dinleyicisi uç noktası içerir. Merhaba trafik Yöneticisi toouse ayarlanmalıdır [yük devretme yönlendirme](../traffic-manager/traffic-manager-configure-failover-routing-method.md) ile [uç nokta izleme](../traffic-manager/traffic-manager-monitoring.md) her bölgede hello uygulama uç noktası için etkinleştirilmiş.

Aşağıdaki diyagramda hello kesinti önce bu yapılandırma gösterilmektedir.

![Yük devretme önce Aktif-Pasif dağıtımı. Bulut olağanüstü durum kurtarma.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern3-1.png)

Merhaba trafik Yöneticisi bir bağlantı hatası tooregion A algıladığında, bu otomatik olarak kullanıcı trafiği toohello uygulama örneği B. bölgede geçer Bu desen ile veri kaybı tooa yeterince yüksek değerli hello yetkisiz kullanım süresi örneğin 24 saat ayarladığınız önemlidir. Bu süre içinde hello kesinti azaltıldığından varsa veri kaybı önlenmiş olur sağlayacaktır. Hello B hello bölgede Web uygulaması etkinleştirildiğinde hello okuma-yazma işlemleri başarısız olmaya başlar. Bu noktada, toohello salt okunur moda geçer. Bu mod hello istekleri otomatik olarak yönlendirilmiş toohello ikincil veritabanı olacaktır. Yıkıcı bir hata hello Hello durumda kesinti hello yetkisiz kullanım süresi içinde azaltılması gereken değil ve hello yük devretme grubu hello yük devretme tetiklenir. Sonra bu hello okuma-yazma dinleyicisi kullanılabilir olacağı ve hello çağrıları tooit başarısız durduracak. Bu diyagramda aşağıdaki hello tarafından gösterilmiştir.

![Kesinti: Uygulama salt okunur modda. Bulut olağanüstü durum kurtarma.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern3-2.png)

Merhaba kesinti hello birincil bölgede hello yetkisiz kullanım süresi içinde azaltılan, trafik Yöneticisi bağlantı hello geri hello birincil bölgede algılar ve kullanıcı trafiğinin geri toohello uygulama örneği A. bölgede geçer Bu uygulama örneği sürdürür ve bölge A. hello birincil veritabanı kullanarak okuma-yazma modunda çalışır

Bölge B ve hello yük devretme grubu anahtarları hello salt okunur dinleyici tooregion A. hello trafik Yöneticisi B hello bölgede kesinti durumunda, hello uygulama uç noktası hello başarısızlığını algılar Bu kesinti hello son kullanıcı deneyimi olumsuz etkilemez ancak hello birincil veritabanı hello kesintisi sırasında sunulur. Bu diyagramda aşağıdaki hello tarafından gösterilmiştir.

![Kesinti: İkincil veritabanı. Bulut olağanüstü durum kurtarma.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern3-3.png)

Hello kesinti azaltıldığından sonra hello ikincil veritabanı hemen hello birincil ile eşitlenir ve hello salt okunur dinleyicisi anahtarlı geri toohello ikincil veritabanı bölgede b Eşitleme sırasında hello birincil performansını hello eşitlenen toobe gereken veri miktarı bağlı olarak biraz etkilenebilir.

Bu tasarım deseni vardır **avantajları**:

* Merhaba geçici kesintileri sırasında veri kaybı ortadan kaldırır.
* Kapalı kalma süresi yalnızca nasıl hızlı bir şekilde trafik Yöneticisi yapılandırılabilir hello bağlantı hatası algılar üzerinde bağlıdır.

Merhaba **kolaylığını** değil:

* Uygulamanın mümkün toooperate salt okunur modda olması gerekir.

> [!NOTE]
> Bir kalıcı hizmet kesintisi hello bölgede olması durumunda, el ile veritabanı yük devretme etkinleştirmek ve hello veri kaybı kabul edin. Merhaba uygulaması hello ikincil bölge okuma-yazma erişimi toohello veritabanıyla işlevsel olacaktır.
>

## <a name="business-continuity-planning-choose-an-application-design-for-cloud-disaster-recovery"></a>İş sürekliliği planlama: Bulut olağanüstü durum kurtarma için bir uygulama tasarımı seçin
Özel bulut olağanüstü durum kurtarma stratejiniz birleştirin veya bu tasarım desenleri toobest uygulamanızın ihtiyaçlarını karşılayan hello genişletin.  Daha önce belirtildiği gibi seçtiğiniz hello stratejisi toooffer tooyour müşteriler istediğiniz ve uygulama dağıtım topolojisi hello SLA hello üzerinde temel alır. toohelp kararınızı Kılavuzu, aşağıdaki tablonun hello hello tahmini veri kaybı veya kurtarma noktası hedefi (RPO) ve tahmini kurtarma süresini (Ekle) göre hello seçimler karşılaştırır.

| düzeni | RPO | EKLE |
|:--- |:--- |:--- |
| Aktif-Pasif dağıtım birlikte bulunan veritabanı erişimi olan olağanüstü durum kurtarma |Okuma-yazma erişimi < 5 saniye |Hata algılama süresi + DNS TTL |
| Uygulama Yük Dengeleme için etkin-etkin dağıtım |Okuma-yazma erişimi < 5 saniye |Hata algılama süresi + DNS TTL |
| Veri koruma için Aktif-Pasif dağıtımı |Salt okunur erişim < 5 saniye | Salt okunur erişim = 0 |
||Okuma-yazma erişimi sıfır = | Okuma-yazma erişimi = hatası algılama zamanı + veri kaybı yetkisiz kullanım süresi |
|||

## <a name="next-steps"></a>Sonraki adımlar
* Azure SQL veritabanı otomatik yedeklemeler hakkında toolearn bakın [SQL veritabanı otomatik yedeklemeler](sql-database-automated-backups.md)
* İş sürekliliğine genel bakış ve senaryolar için bkz: [iş sürekliliğine genel bakış](sql-database-business-continuity.md)
* Kurtarma için otomatik yedeklemeler kullanma hakkında toolearn bakın [bir veritabanı hello hizmeti tarafından başlatılan yedeklerden geri yükleme](sql-database-recovery-using-backups.md)
* toolearn daha hızlı kurtarma seçenekleri hakkında bkz [aktif coğrafi çoğaltma](sql-database-geo-replication-overview.md)  
* arşivleme için otomatik yedeklemeler kullanma hakkında toolearn bakın [veritabanı kopyalama](sql-database-copy.md)
* Esnek havuzlar etkin coğrafi çoğaltma hakkında daha fazla bilgi için bkz: [esnek havuz olağanüstü durum kurtarma stratejilerini](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md).
