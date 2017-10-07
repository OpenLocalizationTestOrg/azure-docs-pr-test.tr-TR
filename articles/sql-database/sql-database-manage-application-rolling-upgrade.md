---
title: "aaaRolling uygulama yükseltmelerini - Azure SQL veritabanı | Microsoft Docs"
description: "Bilgi nasıl toouse Azure SQL Database coğrafi çoğaltma toosupport çevrimiçi yükseltmeler bulut uygulamanızın."
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: 58f42859-1e37-463c-a3d8-a3ca2e867148
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/16/2016
ms.author: sashan
ms.openlocfilehash: 18c56300916d129bff141624cc5c416b500408d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-rolling-upgrades-of-cloud-applications-using-sql-database-active-geo-replication"></a>SQL veritabanı etkin coğrafi çoğaltma'yı kullanarak bulut uygulamalarının yükseltmelerini yönetme
> [!NOTE]
> [Aktif coğrafi çoğaltma](sql-database-geo-replication-overview.md) tüm katmanlar tüm veritabanları için kullanıma sunulmuştur.
> 

Bilgi nasıl toouse [coğrafi çoğaltma](sql-database-geo-replication-overview.md) SQL veritabanı tooenable çalışırken bulut uygulamanızın yükseltme. Yükseltme benzer bir işlem olduğundan, iş sürekliliği planlama ve tasarım parçası olması gerekir. Biz yönetme hello iki farklı yöntemleri arayın bu makalede yükseltme işlemine ve hello avantajları ve dengelemeler her seçenekle tartışın. Web sitesi bağlı tooa tek bir veritabanı, veri katmanı olarak oluşan basit bir uygulama, bu makalenin Hello amacıyla kullanacağız. Amacımız hello son kullanıcı deneyimi üzerinde önemli bir etkisi olmadan hello uygulama tooversion 2 tooupgrade sürüm 1 ' dir. 

Merhaba yükseltme seçenekleri değerlendirirken Etkenler aşağıdaki hello düşünmelisiniz:

* Yükseltme sırasında uygulama kullanılabilirliği üzerindeki etkisini. Ne kadar süreyle hello uygulama işlevi sınırlı düşürülmüş veya olabilir.
* Özelliği tooroll yükseltmenin başarısız olması durumunda yedekleyin.
* Güvenlik Açığı hello yükseltme sırasında ilgisiz geri dönülemez bir hata oluşursa, hello uygulamasının.
* Maliyet toplam dolar.  Bu ek artıklık ve artımlı maliyetleri hello yükseltme işlemi tarafından kullanılan hello geçici bileşenleri içerir. 

## <a name="upgrading-applications-that-rely-on-database-backups-for-disaster-recovery"></a>Olağanüstü durum kurtarma için veritabanı yedeklemeleri kullanan uygulamalar yükseltme
Uygulamanızın üzerinde otomatik veritabanı yedeklemeyi kullanır ve olağanüstü durum kurtarma için coğrafi geri yükleme kullanıyorsa, bu genellikle dağıtılan tooa tek Azure bölgedir. Bu durumda hello yükseltme işlemi, tüm uygulama bileşenleri yedekleme dağıtımını hello yükseltme katılan oluşturma içerir. toominimize hello son kullanıcı kesintisi hello yük devretme profiliyle Azure trafik Yöneticisi (WATM) özelliğinden yararlanır.  Aşağıdaki diyagramda hello hello işletimsel ortamı önceki toohello yükseltme işlemi gösterilmektedir. uç nokta hello <i>contoso 1.azurewebsites.net</i> toobe yükseltilmesi gerekiyor hello uygulamasının üretim yuvasını temsil eder. tooenable hello özelliği tooroll geri Merhaba yükseltme, tam olarak eşitlenen bir kopyasını hello uygulama ile bir aşama yuva oluşturun. Merhaba aşağıdaki adımları hello yükseltme için gerekli tooprepare Merhaba uygulaması şunlardır:

1. Merhaba yükseltme için hazırlamak yuva oluşturun. ikincil bir veritabanı (1) oluşturmak ve hello özdeş bir web sitesinde dağıtan toodo aynı Azure bölgesi. İşlem dengeli hello tamamlanırsa hello ikincil toosee izleyin.
2. WATM'ye ile bir yük devretme profili <i>contoso 1.azurewebsites.net</i> çevrimiçi uç noktası olarak ve <i>contoso 2.azurewebsites.net</i> çevrimdışı olarak. 

> [!NOTE]
> Not hello hazırlık adımları Merhaba uygulaması hello üretim yuvasına etkilemez ve tam erişim modunda çalışabilir.
>  

![SQL veritabanı Git çoğaltma yapılandırması. Bulut olağanüstü durum kurtarma.](media/sql-database-manage-application-rolling-upgrade/Option1-1.png)

Merhaba hazırlık adımları tamamladıktan sonra hello uygulama hello gerçek yükseltme için hazır. Aşağıdaki diyagramda hello hello yükseltme işleminde hello adımlar gösterilmektedir. 

1. Merhaba birincil veritabanı hello üretim yuvası yalnızca tooread modunda (3) ayarlayın. Bu durum, bu hello güvenli olduğunu garanti edemez üretim hello uygulama (V1) örneğini kalacak salt okunur böylece hello farklılıklara hello V1 ve V2 veritabanı örnekleri arasında önleme hello yükseltme sırasında.  
2. Merhaba planlanan sonlandırma modu (4) kullanılarak hello ikincil veritabanı bağlantısını kesin. Merhaba birincil veritabanı tam olarak eşitlenen bağımsız bir kopyasını oluşturur. Bu veritabanı yükseltilir.
3. Hello birincil veritabanı tooread yazma modunu ve hello aşama yuvası (5) hello yükseltme betiğini çalıştırın.     

![SQL Database coğrafi çoğaltma yapılandırması. Bulut olağanüstü durum kurtarma.](media/sql-database-manage-application-rolling-upgrade/Option1-2.png)

Merhaba yükseltmesi başarıyla tamamlandı, hazır tooswitch Merhaba son kullanıcıların aşamalı toohello kopyalama hello uygulaması sunulmuştur. Merhaba üretim yuvasına hello uygulamasının artık hale gelir.  Bu diyagramda aşağıdaki hello üzerinde gösterildiği gibi birkaç adım içerir.

1. Merhaba çevrimiçi endpoint hello WATM profilinde çok geçiş<i>contoso 2.azurewebsites.net</i>, hangi noktaları toohello V2 sürüm hello web sitesinin (6). Şimdi hello V2 uygulama hello üretim yuvasıyla haline gelir ve hello son kullanıcı trafiğidir yönlendirilmiş tooit.  
2. Güvenli bir şekilde şekilde hello V1 uygulama bileşenleri artık ihtiyacınız varsa bunları (7) kaldırın.   

![SQL Database coğrafi çoğaltma yapılandırması. Bulut olağanüstü durum kurtarma.](media/sql-database-manage-application-rolling-upgrade/Option1-3.png)

Merhaba yükseltme işlemi başarısız olursa, örneğin hello yükseltme komut dosyası, tooan hata nedeniyle hello aşama yuvası sayılacağı tehlikeye. tooroll hello uygulama toohello yükseltme öncesi durumu hello üretim yuvası toofull erişim hello uygulamada yalnızca geri yedekleyin. Merhaba adımlar hello sonraki diyagramda gösterilmektedir.    

1. Merhaba veritabanı kopyası tooread-yazma modunda (8) olarak ayarlayın. Bu geri yükler hello üretim yuvasındaki işlevsel olarak tam V1 hello.
2. Merhaba kök neden analizi yapmak ve tehlikeye hello bileşenleri hello aşama yuva (9) kaldırın. 

Bu noktada Merhaba uygulaması tam olarak işlevsel ve hello yükseltme adımları yinelenebilir.

> [!NOTE]
> zaten çok noktaları gibi hello geri alma WATM profilinde değişiklik gerektirmez<i>contoso 1.azurewebsites.net</i> etkin uç nokta hello gibi.
> 
> 

![SQL Database coğrafi çoğaltma yapılandırması. Bulut olağanüstü durum kurtarma.](media/sql-database-manage-application-rolling-upgrade/Option1-4.png)

başlangıç anahtarı **avantajı** bu uygulamanın basit adımları kümesini kullanarak tek bir bölgedeki yükseltebilirsiniz seçeneğidir. Merhaba dolar hello yükseltme nispeten düşük maliyetidir. Merhaba ana **kolaylığını** olduğundan, hello yükseltme hello kurtarma toohello yükseltme öncesi durumu sırasında yıkıcı bir hata oluşursa, içeren farklı bir bölgeye ve geri yükleme hello veritabanından hello uygulamasının yeniden dağıtımı coğrafi geri yükleme kullanarak yedekleme. Bu işlem, önemli kapalı kalma sürelerine neden olur.   

## <a name="upgrading-applications-that-rely-on-database-geo-replication-for-disaster-recovery"></a>Olağanüstü durum kurtarma için veritabanı coğrafi çoğaltma kullanan uygulamalar yükseltme
Coğrafi çoğaltma iş sürekliliği için uygulamanızı yararlanır, etkin bir birincil bölge dağıtım ve yedekleme bölge bekleme bir dağıtımda sahip farklı bölgelere dağıtılan tooat en az iki olur. Ayrıca toohello Etkenler daha önce hello yükseltme işlemi, güvence altına almalıdır belirtildiği:

* Merhaba uygulaması hello yükseltme işlemi sırasında her zaman geri dönülemez hatalarından korumalı olarak kalır
* Merhaba coğrafi olarak yedekli hello uygulama bileşenlerinin hello active bileşenleri ile paralel yükseltilir

tooachieve hello yük devretme kullanarak Azure trafik Yöneticisi (WATM) özelliğinden yararlanır bu hedefleri tane aktif, üç yedekleme uç noktaları ile profil.  Aşağıdaki diyagramda hello hello işletimsel ortamı önceki toohello yükseltme işlemi gösterilmektedir. Merhaba web siteleri <i>contoso 1.azurewebsites.net</i> ve <i>contoso dr.azurewebsites.net</i> üretim yuvasına hello uygulamasının tam coğrafi artıklık ile temsil eder. tooenable hello özelliği tooroll geri Merhaba yükseltme, tam olarak eşitlenen bir kopyasını hello uygulama ile bir aşama yuva oluşturun. Merhaba yükseltme işlemi sırasında yıkıcı bir hata oluşması durumunda Merhaba uygulaması hızla kurtarabilirsiniz tooensure gerektiğinden, hello aşama yuvası toobe coğrafi olarak yedekli de gerekir. Merhaba aşağıdaki adımları hello yükseltme için gerekli tooprepare Merhaba uygulaması şunlardır:

1. Merhaba yükseltme için hazırlamak yuva oluşturun. ikincil bir veritabanı (1) oluşturmak ve hello hello web sitesinde özdeş bir kopyasını dağıtan toodo aynı Azure bölgesi. İşlem dengeli hello tamamlanırsa hello ikincil toosee izleyin.
2. Coğrafi çoğaltma tarafından hello aşama yuvasında coğrafi olarak yedekli ikincil bir veritabanı oluşturmak hello ikincil veritabanı toohello yedekleme bölge (denir "coğrafi çoğaltma zincirleme"). İşlem dengeli hello tamamlanmış (3) ise hello yedekleme ikincil toosee izleyin.
3. Merhaba yedekleme bölgede hello web sitesi yedek bir kopyasını oluşturun ve onu toohello coğrafi olarak yedekli ikincil (4) bağlayabilirsiniz.  
4. Merhaba ek uç noktaları ekleme <i>contoso 2.azurewebsites.net</i> ve <i>contoso 3.azurewebsites.net</i> toohello yük devretme profilinde WATM çevrimdışı uç noktalar (5) olarak. 

> [!NOTE]
> Not hello hazırlık adımları Merhaba uygulaması hello üretim yuvasına etkilemez ve tam erişim modunda çalışabilir.
> 
> 

![SQL Database coğrafi çoğaltma yapılandırması. Bulut olağanüstü durum kurtarma.](media/sql-database-manage-application-rolling-upgrade/Option2-1.png)

Hello hazırlık adımları tamamlandığında, hello aşama yuvası hello yükseltme için hazır olur. Aşağıdaki diyagramda hello hello yükseltme adımları gösterilmektedir.

1. Merhaba birincil veritabanı hello üretim yuvası yalnızca tooread modunda (6) ayarlayın. Bu durum, bu hello güvenli olduğunu garanti edemez üretim hello uygulama (V1) örneğini kalacak salt okunur böylece hello farklılıklara hello V1 ve V2 veritabanı örnekleri arasında önleme hello yükseltme sırasında.  
2. Merhaba ikincil veritabanı bağlantısını hello planlanan sonlandırma modu (7) hello kullanarak aynı bölge. Birincil hello sonlandırma sonra otomatik olarak olacak hello birincil veritabanı tam olarak eşitlenen bağımsız bir kopyasını oluşturur. Bu veritabanı yükseltilir.
3. Merhaba birincil veritabanı hello aşama yuvası tooread-yazma modunda açın ve hello yükseltme komut dosyası (8) çalıştırın.    

![SQL Database coğrafi çoğaltma yapılandırması. Bulut olağanüstü durum kurtarma.](media/sql-database-manage-application-rolling-upgrade/Option2-2.png)

Merhaba yükseltmesi başarıyla tamamlandı, artık hazır tooswitch hello son kullanıcıların toohello V2 hello uygulama sürümü bulunur. Aşağıdaki diyagramda hello hello adımlar gösterilmektedir.

1. Merhaba etkin uç nokta hello WATM profilinde çok geçiş<i>contoso 2.azurewebsites.net</i>, şimdi hello web sitesinin (9) toohello V2 sürümünü gösterir. Şimdi hello V2 uygulama üretim yuvasıyla haline gelir ve yönlendirilmiş tooit son kullanıcı trafiğidir. 
2. Güvenli bir şekilde şekilde hello V1 uygulama artık ihtiyacınız varsa onu (10 ve 11) kaldırın.  

![SQL Database coğrafi çoğaltma yapılandırması. Bulut olağanüstü durum kurtarma.](media/sql-database-manage-application-rolling-upgrade/Option2-3.png)

Merhaba yükseltme işlemi başarısız olursa, örneğin hello yükseltme komut dosyası, tooan hata nedeniyle hello aşama yuvası sayılacağı tehlikeye. tooroll hello uygulama toohello yükseltme öncesi durumu yalnızca tam erişimi olan hello üretim yuvasındaki toousing Merhaba uygulaması geri yedekleyin. Merhaba adımlar hello sonraki diyagramda gösterilmektedir.    

1. Set hello birincil veritabanı kopyası hello üretim yuvası tooread-yazma modunda (12). Bu geri yükler hello üretim yuvasındaki işlevsel olarak tam V1 hello.
2. Merhaba kök neden analizi yapmak ve tehlikeye hello bileşenleri hello aşama yuvada (13 ve 14) kaldırın. 

Bu noktada Merhaba uygulaması tam olarak işlevsel ve hello yükseltme adımları yinelenebilir.

> [!NOTE]
> zaten çok noktaları gibi hello geri alma WATM profilinde değişiklik gerektirmez <i>contoso 1.azurewebsites.net</i> etkin uç nokta hello gibi.
> 
> 

![SQL Database coğrafi çoğaltma yapılandırması. Bulut olağanüstü durum kurtarma.](media/sql-database-manage-application-rolling-upgrade/Option2-4.png)

başlangıç anahtarı **avantajı** bu hello uygulama ve onun coğrafi olarak yedekli kopyalama paralel hello yükseltme sırasında iş sürekliliği ödün vermeden yükseltebilirsiniz, seçeneğidir. Merhaba ana **kolaylığını** her uygulama bileşeninin çift artıklığı gerektirir ve bu nedenle daha yüksek dolar maliyet oluşturur. Ayrıca, daha karmaşık bir iş akışı içerir. 

## <a name="summary"></a>Özet
Merhaba makalesinde açıklanan hello iki yükseltme yöntemleri maliyet karmaşıklığı ve hello dolar içinde farklılık gösterir ancak her ikisi de hello son kullanıcı sınırlı yalnızca tooread işlemleri olduğunda hello süresini en aza indirerek üzerinde odaklanın. Bu süre doğrudan hello yükseltme komut dosyası hello süreye göre tanımlanır. Merhaba veritabanı boyutuna bağlı değildir, hello hizmet katmanı, size, seçerseniz, hello web sitesi yapılandırması ve kolayca denetleyemezsiniz diğer etkenlere bağlı. Tüm hello hazırlık adımları hello yükseltme adımları ayrılmış Merhaba üretim uygulaması etkilemeden yapılabilir Bunun nedeni. Merhaba yükseltme komut dosyası Hello verimliliğini yükseltmeler sırasında hello son kullanıcı deneyimini belirleyen hello anahtar faktördür. Bu nedenle, artırabilir hello en iyi hello yükseltme komut dosyası olarak verimli hale çabalarınız odaklanan yoludur.  

## <a name="next-steps"></a>Sonraki adımlar
* İş sürekliliğine genel bakış ve senaryolar için bkz: [iş sürekliliğine genel bakış](sql-database-business-continuity.md).
* Azure SQL veritabanı otomatik yedeklemeler hakkında toolearn bkz [SQL veritabanı yedeklemeleri otomatik](sql-database-automated-backups.md).
* Kurtarma için otomatik yedeklemeler kullanma hakkında toolearn bkz [bir veritabanını otomatik yedeklerden geri](sql-database-recovery-using-backups.md).
* toolearn daha hızlı kurtarma seçenekleri hakkında bkz [aktif coğrafi çoğaltma](sql-database-geo-replication-overview.md).


