---
title: "Azure Premium Storage: Performans için tasarlama | Microsoft Docs"
description: "Azure Premium Storage kullanarak yüksek performanslı uygulamalar tasarlayın. Premium Storage, Azure sanal makinelerde çalışan g/Ç kullanımı yoğun iş yükleri için yüksek performanslı, düşük gecikmeli disk desteği sağlar."
services: storage
documentationcenter: na
author: aungoo-msft
manager: tadb
editor: tysonn
ms.assetid: e6a409c3-d31a-4704-a93c-0a04fdc95960
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: aungoo
ms.openlocfilehash: dde3e60ae4c8387150b65f0715166b5d549891e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-premium-storage-design-for-high-performance"></a>Azure Premium Storage: Yüksek performans tasarımı
## <a name="overview"></a>Genel Bakış
Bu makalede, Azure Premium Storage kullanarak yüksek performanslı uygulamalar oluşturmaya yönelik yönergeler sağlar. Uygulamanız tarafından kullanılan performansı en iyi uygulamalar uygulanabilir tootechnologies birlikte bu belgede sağlanan hello yönergeleri kullanabilirsiniz. Bu belge boyunca bir örnek olarak Premium depolama üzerinde çalışan SQL Server tooillustrate hello yönergeleri kullandık.

Biz bu makalede hello depolama katmanı için performans senaryosu olsa da, toooptimize hello uygulama katmanı gerekir. Örneğin, bir SharePoint grubunda Azure Premium Storage barındırıyorsanız, bu makale toooptimize hello veritabanı sunucusundan hello SQL Server örnekleri kullanabilirsiniz. Ayrıca, hello SharePoint grubun Web sunucusu ve uygulama sunucusu tooget hello çoğu performansını iyileştirin.

Bu makalede Azure Premium Storage uygulama performansı en iyi duruma getirme hakkında sık sorulan sorular aşağıdaki sorunuza yanıt almanıza yardımcı,

* Nasıl toomeasure, uygulama performansı?  
* Neden, beklenen yüksek performanslı görmediğinizden?  
* Hangi Etkenler Premium depolama, uygulama performansını etkiler?  
* Bu etkenler Premium depolama, uygulamanızın performansını nasıl etkiler?  
* Nasıl, IOPS, bant genişliği ve gecikme süresi için en iyi duruma getirebilirsiniz?  

Premium depolama üzerinde çalışan iş yüklerini yüksek performans hassas olduğundan özellikle Premium Storage için bu yönergeleri sağladık. Uygun olan yerlerde örnekler sağladık. Ayrıca, bazı standart depolama disklerle Iaas VM'ler üzerinde çalıştırılan bu yönergeleri tooapplications de uygulayabilirsiniz.

Yeni tooPremium depolama varsa, başlamadan önce ilk hello okuma [Premium Storage: Azure sanal makine iş yükleri için yüksek performanslı depolama](../storage-premium-storage.md) ve [Azure Storage ölçeklenebilirlik ve performans hedefleri](storage-scalability-targets.md)makaleler.

## <a name="application-performance-indicators"></a>Uygulama performans göstergeleri
Bir uygulama da ya da olmasın performans göstergeleri gibi kullanarak gerçekleştiriyor olup olmadığını biz değerlendirmek, ne kadar hızlı bir uygulama bir kullanıcı isteği, istek başına bir uygulama işleme ne kadar veri işleme, kaç uygulamanın belirli bir işleme istekleri bir kullanıcı, kendi İsteği gönderdikten sonra bir yanıt toowait tooget sahip zaman, ne kadar süre. Bu performans göstergeleri için Hello teknik koşulları olan, IOPS, üretilen iş veya bant genişliği ve gecikme süresi.

Bu bölümde, hello ortak performans göstergelerini Premium Storage hello bağlamda aşağıdakiler ele alınacaktır. Aşağıdaki bölümde, uygulama gereksinimleri toplama Merhaba, öğreneceksiniz nasıl toomeasure bu performans göstergeleri uygulamanızın. Daha sonra en iyi duruma getirme uygulama performansını, bu performans göstergelerini ve öneriler toooptimize etkileyen hello etkenleri hakkında bilgi edineceksiniz bunları.

## <a name="iops"></a>IOPS
IOPS sayısıdır uygulamanız bir saniye içinde depolama diskleri toohello gönderiyor ister. Bir giriş/çıkış işlem okunamadı veya sıralı veya rastgele yazma. OLTP uygulamaları çevrimiçi perakende Web sitesi gibi çok sayıda eşzamanlı kullanıcı hemen istekleri tooprocess gerekir. Merhaba kullanıcı isteklerini Ekle olan ve yoğun veritabanı işlemleri, hangi Merhaba uygulaması hızlı bir şekilde işlemelidir güncelleştirin. Bu nedenle, çok yüksek IOPS OLTP uygulamalar gerektirir. Bu tür uygulamalar, küçük ve rastgele g/ç istekleri milyonlarca işleyin. Bu tür bir uygulamanız varsa, IOPS hello uygulama altyapısı toooptimize tasarlamanız gerekir. Merhaba, daha sonra bölüm *uygulama performansı en iyi duruma getirme*, tooget dikkate almanız gereken tüm hello Etkenler ayrıntılı olarak aşağıdakiler ele yüksek IOPS.

Ne zaman bir premium depolama disk tooyour yüksek ölçekli VM, Azure sağlarken, garantili IOPS sayısını hello disk belirtimine göre ekleyin. Örneğin, bir P50 disk 7500 IOPS sağlar. Her yüksek ölçekli VM boyutu da sürdürebilmek belirli bir IOPS sınırı vardır. Örneğin, standart GS5 VM 80.000 IOPS sınırı vardır.

## <a name="throughput"></a>Aktarım hızı
Üretilen iş ya da bant genişliği hello uygulamanızı belirli bir aralıktaki depolama diskleri toohello gönderiyor veri miktarıdır. Uygulamanızı girdi/çıktı işlemleri büyük GÇ birim boyutlarını ile çalışıyorsa, yüksek verimlilik gerektirir. Veri ambarı uygulamalarını veri büyük bölümünü aynı anda erişebilir ve yaygın olarak toplu işlemleri tooissue tarama yoğun işlemleri eğilimlidir. Diğer bir deyişle, bu tür uygulamalar, daha yüksek verimlilik gerektirir. Bu tür bir uygulamanız varsa, üretilen iş için altyapı toooptimize tasarlamanız gerekir. Ayrıntı hello faktörlerinde Hello sonraki bölümde aşağıdakiler ele bu tooachieve ayarlamak gerekir.

Ne zaman bir premium depolama disk tooa yüksek ölçekli VM, Azure hükümleri verimlilik, disk belirtimine göre ekleyin. Örneğin, P50 disk 250 MB ikinci bir disk verimlilik sağlar. Her yüksek ölçekli VM boyutu bu karşılayabilir belirli üretilen iş sınırı da sahiptir. Örneğin, standart GS5 VM 2.000 saniyede bir en yüksek verimlilik sahiptir. 

Üretilen iş ve hello formülde aşağıda gösterildiği gibi IOPS arasında bir ilişki yoktur.

![](media/storage-premium-storage-performance/image1.png)

Bu nedenle uygulamanızın gerektirdiği önemli toodetermine hello en iyi performans ve IOPS değerlerini olur. Toooptimize birini deneyin gibi hello diğer ayrıca etkilenen. Bir sonraki bölümde *uygulama performansı en iyi duruma getirme*, biz IOPS ve üretilen iş en iyi duruma getirme hakkında daha ayrıntılı olarak ele alınacaktır.

## <a name="latency"></a>Gecikme süresi
Gecikme tek bir isteğin bir uygulama tooreceive sürdüğünü hello süresi, toohello depolama diskleri göndermek ve hello yanıt toohello istemci gönderme. Bu kritik uygulamanın performans toplama tooIOPS ve üretilen iş ölçüsüdür. Merhaba bir premium depolama diskini gecikme süresi, bir istek için tooretrieve hello bilgilerini alır ve iletişim hello süre tooyour uygulama yedekleyin. Premium depolama tutarlı düşük gecikme süreleri sağlar. Salt okunur ana bilgisayar premium depolama disklerde önbelleğe almayı etkinleştirirseniz, çok daha düşük okuma gecikmesi alabilirsiniz. Disk önbelleği sonraki bölümünde daha ayrıntılı üzerinde aşağıdakiler ele alınacaktır *uygulama performansı en iyi duruma getirme*.

Ne zaman, en iyi duruma getirme, uygulama tooget daha yüksek IOPS ve üretilen işi hello gecikme, uygulamanızın etkiler. Merhaba uygulama performans ayarlama sonra her zaman hello hello uygulama tooavoid gecikme süresi değerlendirme beklenmeyen yüksek gecikme davranışı.

## <a name="gather-application-performance-requirements"></a>Uygulama Performans gereksinimlerini toplama
Azure Premium Storage üzerinde çalışan yüksek performanslı uygulamalar tasarlama hello ilk adımıdır, uygulamanızın toounderstand hello performans gereksinimleri. Performans gereksinimlerini topladıktan sonra uygulama tooachieve hello en iyi performansı en iyi duruma getirebilirsiniz.

Merhaba önceki bölümde hello ortak performans göstergelerini IOPS, üretilen iş ve gecikme açıklanmıştır. Bu performans göstergelerinin kritik tooyour uygulama toodeliver istenen hello kullanıcı deneyimi olan tanımlamanız gerekir. Örneğin, yüksek IOPS bir saniyede milyonlarca işlem işleme tooOLTP uygulamaların çoğu önemlidir. Oysa yüksek verimlilik büyük miktarlarda verinin bir saniyede işleme veri ambarı uygulamalar için önemlidir. Son derece düşük gecikme süresi, Web siteleri akış canlı video gibi gerçek zamanlı uygulamalar için önemlidir.

Ardından, uygulamanızın yaşam süresi boyunca hello en yüksek performans gereksinimlerini ölçer. Merhaba örnek denetim altındaki bir başlangıç kullanın. Kayıt hello en yüksek performans gereksinimlerini normal sırasında en yüksek ve yoğun olmayan saatlerde iş yükü nokta. Tüm iş yükleri düzeyleri için gereksinimleri tanımlayarak mümkün toodetermine olacaktır Merhaba, uygulamanızın genel performans gereksinimi. Örneğin, bir e-ticaret Web sitesi normal iş yükünü hello çoğu günde bir yıl ile hizmet hello işlemleri olacaktır. Merhaba en yüksek iş yükü hello Web sitesinin tatilde veya özel satış olayları sırasında hizmet hello hareketleri olacaktır. Hello en yüksek iş yükü sınırlı bir süre için genellikle deneyimli olmakla birlikte, uygulama tooscale iki zorunlu kılabilir veya daha fazla zaman, normal işlem. Merhaba 50 yüzdebirlik, 90 yüzdebirlik ve 99 yüzdebirlik gereksinimleri öğrenin. Bu tüm aykırı değerlerini hello performans gereksinimleri filtrelemenize yardımcı olur ve hello doğru değerleri için en iyi duruma getirme üzerinde çabalarınız odaklanabilirsiniz.

**Uygulama Performans gereksinimlerini denetim listesi**

| **Performans gereksinimleri** | **50. Yüzdeliğini** | **90 yüzdebirlik** | **99 yüzdebirlik** |
| --- | --- | --- | --- |
| En çok, Saniye başına işlem | | | |
| % Okuma işlemleri | | | |
| % Yazma işlemleri | | | |
| % Rastgele işlemleri | | | |
| % Sıralı işlemleri | | | |
| G/ç isteği boyutu | | | |
| Ortalama işleme | | | |
| En çok, Aktarım hızı | | | |
| Min. Gecikme süresi | | | |
| Ortalama gecikme süresi | | | |
| En çok, CPU | | | |
| Ortalama CPU | | | |
| En çok, Bellek | | | |
| Ortalama bellek | | | |
| Sıra Derinliği | | | |

> [!NOTE]
> Beklenen gelişmeye uygulamanızın üzerinde göre bu sayı ölçeklendirme göz önünde bulundurmalısınız. Daha sonra performansı artırmak için daha zor toochange hello altyapı olabileceğinden, önceden büyüme için iyi bir fikir tooplan var.
>
>

Varolan bir uygulamaya sahip ve toomove tooPremium depolama istiyorsanız ilk hello varolan uygulama yukarıda hello denetim listesini oluşturun. Ardından, uygulamanızda açıklanan yönergeleri göre Premium depolama ve tasarım Merhaba uygulaması prototipi yapı *uygulama performansı en iyi duruma getirme* bu belgenin sonraki bölümünde. Merhaba sonraki bölümde toogather hello performans ölçümleri kullanabilirsiniz hello araçlarını açıklar.

Bir denetim listesi benzer tooyour var olan uygulama için hello prototip oluşturun. Benchmarking araçlarını kullanarak hello iş yükleri benzetimini ve hello prototip uygulama performansına ölçebilirsiniz. Merhaba bölümüne bakarak [Benchmarking](#benchmarking) toolearn daha fazla. Premium depolama veya eşleşen aşan uygulama performans gereksinimlerinizi belirlemek için yaparak. Ardından, uygulayabileceğiniz hello üretim uygulamanız için aynı yönergeleri.

### <a name="counters-toomeasure-application-performance-requirements"></a>Toomeasure uygulama performans gereksinimlerini sayaçları
Uygulamanızın en iyi şekilde toomeasure performans gereksinimlerini Merhaba, hello sunucusunun hello işletim sistemi tarafından sağlanan toouse performans izleme araçları. Linux için Windows için PerfMon ve iostat kullanabilirsiniz. Bu araçları bölümün yukarısında hello karşılık gelen tooeach ölçü açıklandığı sayaçları yakalayın. Uygulamanızı çalışırken, normal, en yüksek ve yoğun olmayan saatlerde iş yükleri Bu sayaçlar hello değerlerini yakalama gerekir.

Merhaba PerfMon sayaçları işlemci, bellek ve her mantıksal disk ve fiziksel disk sunucunuzun için kullanılabilir. Premium depolama diskleri bir VM ile kullandığınızda, hello fiziksel disk sayaçları için her premium depolama diski, ve mantıksal disk sayaçları hello premium depolama disklerde oluşturulan her birim için. Uygulama İş yükünüzün konak hello diskleri hello değerlerini yakalama gerekir. Mantıksal ve fiziksel diskler arasında bir tooone eşleme ise toophysical disk sayaçları başvurabilir; Aksi takdirde toohello mantıksal disk sayaçları başvurun. Linux üzerinde hello iostat komutu CPU ve disk kullanımı raporu oluşturur. Merhaba disk kullanımı raporu fiziksel aygıt veya bölüm başına istatistikler sağlar. Bir veritabanı sunucusu, veri ve günlük ile ayrı disklerde varsa, her iki diskin için bu verileri toplayın. Aşağıdaki tablo diskler, işlemci ve bellek sayaçlarını açıklanmaktadır:

| Sayaç | Açıklama | PerfMon | Iostat |
| --- | --- | --- | --- |
| **IOPS veya saniye başına işlem** |Saniye başına toohello depolama disk g/ç istek sayısı verdi. |Disk Okuma/sn <br> Disk Yazma/sn |TP'leri <br> r/s <br> w/s |
| **Disk okuma ve yazma işlemleri** |% Okuma ve yazma hello disk üzerinde gerçekleştirilen işlemler. |% Disk okuma süresi <br> % Disk yazma süresi |r/s <br> w/s |
| **Üretilen iş** |Okunan veya toohello disk saniye başına yazılan veri miktarı. |Disk okuma bayt/sn <br> Disk Yazma Bayt/sn |kB_read/s <br> kB_wrtn/s |
| **Gecikme süresi** |Zaman toocomplete disk g/ç isteği toplam sayısı. |Ortalama Disk sn/Okuma <br> Ortalama disk sn/yazma |await <br> svctm |
| **G/ç boyutu** |g/ç istekleri Hello boyutunu toohello depolama diskleri verir. |Ortalama Disk bayt/okuma <br> Ortalama Disk Bayt/yazma |avgrq sz |
| **Sıra Derinliği** |Formu okuma veya toohello depolama diskini yazılmış bekleme toobe istekleri bekleyen g/ç sayısı. |Geçerli Disk Sırası Uzunluğu |avgqu sz |
| **Maks. Bellek** |Bellek miktarı toorun uygulama sorunsuz gerekli |% Kullanılan kaydedilmiş bayt |Vmstat kullanın |
| **Maks. CPU** |CPU miktarını toorun uygulama sorunsuz gerekli |% İşlemci zamanı |% kul |

Daha fazla bilgi edinmek [iostat](http://linuxcommand.org/man_pages/iostat1.html) ve [PerfMon](https://msdn.microsoft.com/library/aa645516.aspx).

## <a name="optimizing-application-performance"></a>Uygulama performansı en iyi duruma getirme
Premium depolama üzerinde çalışan bir uygulama performansını etkileyen ana faktörler hello yapısı, g/ç isteği, VM boyutunu, Disk boyutu, diskler, Disk önbelleğe alma, çoklu iş parçacığı kullanımı ve sıra derinliği sayısı adı verilir. Bu etkenler bazıları hello sistem tarafından sağlanan düğmelerini ile denetleyebilirsiniz. Birçok uygulama, bir seçenek tooalter hello g/ç boyutu ve sıra derinliği doğrudan vermeyebilir. Örneğin, SQL Server kullanıyorsanız, hello g/ç boyutu ve sıra derinliği seçemezsiniz. SQL Server hello en iyi g/ç boyutu ve sıra derinliği değerleri tooget hello çoğu performans seçer. Önemli toounderstand hello etkilerini Etkenler her iki tür, uygulama performansı, böylelikle uygun kaynaklara toomeet performans gereksinimlerine sağlayabilirsiniz.

Bu bölümde, oluşturduğunuz toohello uygulama gereksinimleri denetim listesi tooidentify başvurmak ne kadar uygulama performansı toooptimize gerekir. Mümkün toodetermine olacaktır, temel sayfasından Bu bölüm, hangi Etkenler tootune gerekir. toowitness uygulama kurulumunuza araçları değerlendirmesi çalıştırmak, uygulama performansı, her faktörü etkileri hello. Toohello başvuran [Benchmarking](#Benchmarking) hello adımları toorun Windows ve Linux VM'ler araçlarının değerlendirmesi ortak için bu makalenin sonunda bölüm.

### <a name="optimizing-iops-throughput-and-latency-at-a-glance"></a>IOPS, üretilen iş ve gecikme süresi bir bakışta en iyi duruma getirme
Tüm hello performans Etkenler ve hello adımları toooptimize IOPS, üretilen iş ve gecikmeyi Hello tabloda özetlenmiştir. Merhaba bu Özet aşağıdaki bölümler her anlatmaktadır çok daha kapsamlı bir faktördür.

| &nbsp; | **IOPS** | **Üretilen iş** | **Gecikme süresi** |
| --- | --- | --- | --- |
| **Örnek senaryo** |İkinci oranı başına çok yüksek işlem gerektiren Kurumsal OLTP uygulama. |Kurumsal veri uygulama işleme büyük miktarlarda veri ambarı. |Çevrimiçi oyun gibi anlık yanıtlar toouser istekleri gerektiren gerçek zamanlı uygulamaları. |
| Performans Etkenler | &nbsp; | &nbsp; | &nbsp; |
| **G/ç boyutu** |Küçük g/ç boyutu, daha yüksek IOPS ortaya çıkarır. |Daha büyük g/ç boyutu tooyields daha yüksek verimlilik. | &nbsp;|
| **VM boyutu** |Uygulama gereksiniminden daha büyük IOPS sağlayan bir VM boyutu kullanın. VM boyutları ve bunların IOPS sınırlarını buraya bakın. |Uygulama gereksiniminden daha büyük verimi sınırına sahip bir VM boyutu kullanın. VM boyutları ve bunların işleme sınırları buraya bakın. |Teklifler sınırları uygulama gereksiniminden daha büyük ölçeklendirme bir VM boyutu kullanın. VM boyutları ve bunların sınırlarını buraya bakın. |
| **Disk boyutu** |Uygulama gereksiniminden daha büyük IOPS sunan bir disk boyutu kullanın. Disk boyutları ve bunların IOPS sınırlarını buraya bakın. |Üretilen iş sınırı uygulama gereksiniminden daha büyük bir disk boyutu kullanın. Disk boyutları ve bunların işleme sınırları buraya bakın. |Teklifler sınırları uygulama gereksiniminden daha büyük ölçeklendirme bir disk boyutu kullanın. Disk boyutları ve bunların sınırlarını buraya bakın. |
| **VM ve Disk ölçek sınırları** |Merhaba VM boyutu seçilen IOPS sınırı premium depolama diskleri tarafından yönlendirilen toplam IOPS tooit bağlı daha büyük olmalıdır. |Üretilen iş sınırı hello VM boyutu seçilen premium depolama diskleri tarafından yönlendirilen toplam verimlilik tooit bağlı daha büyük olmalıdır. |Merhaba VM boyutu seçilen ölçek sınırları ekli premium depolama diskleri toplam ölçek sınırlarını büyük olmalıdır. |
| **Disk önbelleği** |Premium depolama okuma yoğun işlemleri tooget disklerle salt okunur önbellek etkinleştirmek yüksek okuma IOPS. | &nbsp; |Premium depolama disklerde hazır yoğun işlemleri tooget çok düşük okuma gecikme süreleriyle salt okunur önbellek etkinleştirin. |
| **Disk şeritleme** |Birden çok disk kullanın ve bunları birlikte tooget birleşik yüksek IOPS ve üretilen iş sınırı şeritler. VM başına birleşik sınırı hello Not bağlı premium disklerin toplam sınırları hello daha yüksek olmalıdır. | &nbsp; | &nbsp; |
| **Şerit boyutu** |OLTP uygulamalarda görülen rastgele küçük g/ç deseni için daha küçük stripe boyutu. Örneğin, SQL Server OLTP uygulama için Şerit boyutu 64 KB kullanın. |Veri ambarı uygulamalarda görülen sıralı büyük g/ç düzeni büyük stripe boyutu. Örneğin, SQL Server veri ambarı uygulaması için 256 KB Şerit boyutu kullanın. | &nbsp; |
| **Çoklu iş parçacığı kullanımı** |Çoklu iş parçacığı kullanımı toopush daha yüksek sayıda istekleri tooPremium toohigher IOPS götürür depolama ve işleme kullanın. Örneğin, SQL Server üzerinde daha fazla CPU tooSQL sunucu yüksek MAXDOP değeri tooallocate ayarlayın. | &nbsp; | &nbsp; |
| **Sıra Derinliği** |Daha büyük sıra derinliği daha yüksek IOPS sağlar. |Daha büyük sıra derinliği daha yüksek verimlilik verir. |Daha küçük sıra derinliği düşük gecikme verir. |

## <a name="nature-of-io-requests"></a>G/ç istekleri yapısı
Bir g/ç isteği, uygulamanızın gerçekleştirme giriş/çıkış işlem birimidir. G/ç istekleri, rastgele veya sıralı, Hello yapısını tanımlayan okuma veya yazma, küçük veya büyük, uygulamanızın hello performans gereksinimlerini belirlemenize yardımcı olur. G/ç istekleri, uygulama altyapınızı tasarlama toomake hello doğru kararlar çok önemli toounderstand hello yapısı olur.

G/ç boyutu hello daha önemli faktörler biridir. Merhaba g/ç boyutu, uygulamanız tarafından oluşturulan hello giriş/çıkış işlem isteğinin hello boyutudur. Hello g/ç boyutu, özellikle hello IOPS performans üzerinde önemli bir etkisi vardır ve mümkün tooachieve uygulama hello bant genişliği kadardır. Merhaba aşağıdaki formülü hello arasındaki ilişkiyi IOPS, gösterir g/ç boyutu ve bant genişliği/işleme.  
    ![](media/storage-premium-storage-performance/image1.png)

Bazı uygulamalar, g/ç boyutu, kullanırken bazı uygulamalar tooalter izin verin. Örneğin, SQL Server hello en iyi g/ç boyutu kendisini belirler ve kullanıcılar ile tüm düğmelerini toochange sağlamaz. Üzerindeki diğer yandan Merhaba, Oracle sağlar adlı bir parametre [DB\_ENGELLEME\_BOYUTU](https://docs.oracle.com/cd/B19306_01/server.102/b14211/iodesign.htm#i28815) yapılandırabileceğiniz kullandığı hello hello veritabanının g/ç isteği boyutu.

Toochange hello g/ç boyutu, izin verme, bir uygulama kullanıyorsanız, bu makale toooptimize hello performansını en uygun tooyour uygulama KPI hello yönergeleri kullanın. Örneğin,

* OLTP uygulamanın milyonlarca küçük ve rastgele g/ç istek oluşturur. Bu tür GÇ toohandle istekleri, uygulama altyapısı tooget tasarlamanız gerekir daha yüksek IOPS.  
* Bir veri ambarı uygulama büyük ve sıralı g/ç istekleri oluşturur. Bu, g/ç istekleri toohandle yazın, daha yüksek bant genişliği veya işleme uygulama altyapısı tooget tasarlamanız gerekir.

Toochange hello g/ç boyutu sağlayan bir uygulama kullanıyorsanız bu altın kural hello g/ç boyutu için ayrıca tooother performans yönergeleri kullanın,

* Küçük g/ç boyutu tooget daha yüksek IOPS. Örneğin, bir OLTP uygulama için 8 KB.  
* Daha büyük g/ç boyutu tooget daha yüksek bant genişliği verimliliği. Örneğin, 1024 KB bir veri ambarı uygulaması için.

İşte bir örnek nasıl, hello IOPS ve üretilen iş/bant genişliği, uygulamanız için hesaplayabilirsiniz üzerinde. P30 disk kullanarak bir uygulamayı göz önünde bulundurun. Merhaba maksimum IOPS ve üretilen iş/bant genişliği P30 disk elde edebilirsiniz, 5000 IOP ve 200 MB / saniye sırasıyla. Uygulamanız hello P30 disk ve en fazla IOPS 8 KB gibi daha küçük bir g/ç boyutu hello size bant genişliği elde edilen kullanmak hello gerektiriyorsa, mümkün tooget 40 MB saniyede sunulmuştur. Uygulamanızın en büyük verimi/P30 diskten bant hello ve daha büyük bir g/ç boyutu 1024 KB gibi kullandığınız gerektiriyorsa, ancak hello elde edilen IOPS daha az olacaktır 200 IOPS. Bu nedenle, her iki, uygulamanızın IOPS ve üretilen iş/bant genişliği gereksinimleri karşıladığından emin hello GÇ boyutunu ayarlayın. Aşağıdaki tabloda hello farklı GÇ boyutları ve bunların karşılık gelen IOPS ve üretilen iş için bir P30 disk özetler.

| Uygulama dağıtımı gereksinimi | G/ç boyutu | IOPS | Üretilen iş/bant genişliği |
| --- | --- | --- | --- |
| Maksimum IOPS |8 KB |5,000 |Saniye başına 40 MB |
| En fazla üretilen işi |1024 KB |200 |200 MB / saniye |
| En büyük verimi + yüksek IOPS |64 KB |3,200 |200 MB / saniye |
| Maksimum IOPS + yüksek verimlilik |32 KB |5,000 |Saniye başına 160 MB |

tooget IOPS ve hello maksimum tek premium depolama diskini değerden daha yüksek bant genişliği birlikte şeritli birden çok premium diskleri kullanın. Örneğin, iki P30 diskleri tooget saniyede bir birleşik IOPS 10.000 IOPS sayısı veya 400 MB birleşik verimini şeritler. Merhaba sonraki bölümde açıklandığı gibi hello birleştirilmiş disk IOPS ve üretilen iş destekleyen bir VM boyutu kullanmanız gerekir.

> [!NOTE]
> Her iki IOPS artırabilir veya diğer verimlilik hello da artırır gibi işleme veya IOPS sınırları hello diski veya VM herhangi birini artan zaman yaşamadığı emin olun.
>
>

g/ç boyutu uygulama performansı üzerindeki etkisini toowitness Merhaba, VM ve diskleri üzerinde Kıyaslama araçları çalıştırabilirsiniz. Birden çok test çalışmaları oluşturma ve farklı g/ç boyutu her çalışma toosee hello etkisi için kullanın. Toohello başvuran [Benchmarking](#Benchmarking) daha fazla ayrıntı için bu makalenin hello sonunda bölüm.

## <a name="high-scale-vm-sizes"></a>Yüksek ölçekli VM boyutları
Bir uygulama tasarlama başlattığınızda hello ilk şey toodo, VM toohost uygulamanızı seçin biridir. Premium depolama daha yüksek işlem gücü ve yüksek yerel disk g/ç performansı gerektiren uygulamaların yüksek ölçek VM boyutları ile birlikte gelir. Bu sanal makineleri hello yerel disk için daha hızlı işlemcilerde, daha yüksek bellek çekirdek oranı ve bir Solid-State sürücüsü (SSD) sağlayın. Premium Storage destekleyen yüksek ölçek VM'ler hello DS, DSv2 ve GS serisi VM'ler gösterilebilir.

Yüksek ölçekli VM'ler farklı boyutlarda farklı sayıda CPU çekirdekleri, bellek, işletim sistemi ve geçici disk boyutu ile kullanılabilir. Her VM boyutu en fazla toohello VM iliştirebilirsiniz veri diski sayısı da sahiptir. Bu nedenle, seçilen hello VM boyutu ne kadar işleme, bellek ve depolama kapasitesi, uygulamanız için kullanılabilir etkiler. Ayrıca, hello işlem ve depolama maliyeti de etkiler. Örneğin, hello en büyük VM boyutu DS serisi, DSv2 serisi ve GS serisi hello belirtimlerini aşağıda verilmiştir:

| VM boyutu | CPU çekirdekleri | Bellek | VM disk boyutları | En çok, Veri diskleri | Önbellek boyutu | IOPS | Bant genişliği önbellek g/ç sınırları |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_DS14 |16 |112 GB |İŞLETİM SİSTEMİ = 1023 GB <br> Yerel SSD 224 GB = |32 |576 GB |50.000 IOPS <br> Saniye başına 512 MB |4.000 IOPS ve saniye başına 33 MB |
| Standard_GS5 |32 |448 GB |İŞLETİM SİSTEMİ = 1023 GB <br> Yerel SSD 896 GB = |64 |4224 GB |80.000 IOPS <br> Saniye başına 2.000 MB |5000 IOP ve saniyede 50 MB |

tooview tüm kullanılabilir Azure VM boyutlarını, tam bir listesi başvurmak çok[Windows VM boyutları](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) veya [Linux VM boyutları](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Uygulama performansı gereksinimlerini ölçek tooyour istenen ve karşılayabilecek bir VM boyutu seçin. Ayrıca toothis, önemli noktalar VM boyutları seçerken aşağıdaki dikkate alın.

*Ölçek sınırları*  
Merhaba maksimum IOPS sınırları VM başına ve disk başına farklı ve birbirlerinden bağımsız. Merhaba uygulaması, hello premium diskleri ekli tooit yanı sıra hello VM hello sınırlarda IOPS yürüten emin olun. Aksi takdirde, uygulama performansı azaltma karşılaşırsınız.

Örnek olarak, en çok 4.000 IOPS bir uygulama dağıtımı gereksinimi olduğunu varsayın. tooachieve Bu, size sağlama DS1 VM P30 diskte. Merhaba P30 disk too5, 000 IOPS sunabilir. Ancak, hello DS1 VM sınırlı too3, 200 IOPS olur. Sonuç olarak, hello uygulama performansı hello VM sınırına 3,200 IOPS adresindeki tarafından kısıtlı ve performans olacaktır. tooprevent bu durumda, bir VM seçin ve her iki karşılayan uygulama gereksinimleri olacak boyutu disk.

*İşlemi maliyeti*  
Çoğu durumda, Premium depolama ile işlemi, genel maliyeti standart depolama kullanmaktan daha düşük olduğunu mümkündür.

Örneğin, 16.000 IOPS gerektiren bir uygulama göz önünde bulundurun. tooachieve bu performans standart gerekir\_16.000 32 standart depolama 1 TB diskleri kullanan bir maksimum IOPS verebilirsiniz D14 Azure Iaas sanal. Her 1TB standart depolama diskini en fazla 500 IOPS elde edebilirsiniz. Merhaba, bu VM'in aylık maliyeti $1,570 olacaktır tahmin. Merhaba aylık maliyeti 32 standart depolama disklerinin $1,638 olacaktır. Hello tahmin edilen toplam aylık maliyet $3,208 olacaktır.

Ancak, aynı Merhaba, barındırılıyorsa uygulama Premium depolama gerekir daha küçük bir VM boyutu ve daha az premium depolama diskleri, böylece hello genel maliyeti azaltır. Standart bir\_DS13 VM dört P30 diskler kullanarak hello 16.000 IOPS gereksinimi karşılamak. Merhaba DS13 VM 25,600 bir maksimum IOPS ve her P30 disk maksimum IOPS 5.000, sahiptir. Genel olarak, bu yapılandırma 5.000 x 4 = 20.000 elde edebilirsiniz IOPS. Merhaba, bu VM'in aylık maliyeti $1,003 olacaktır tahmin. Merhaba aylık maliyeti dört P30 premium depolama disklerinin $544.34 olacaktır. Hello tahmin edilen toplam aylık maliyet $1,544 olacaktır.

Aşağıdaki tabloda bu senaryonun hello Maliyet dökümü standart ve Premium depolama için özetler.

| &nbsp; | **Standart** | **Premium** |
| --- | --- | --- |
| **VM maliyet aylık** |$1,570.58 (standart\_D14) |$1,003.66 (standart\_DS13) |
| **Aylık maliyeti** |$1,638.40 (32 x 1 TB disk) |$544.34 (4 x P30 diskler) |
| **Aylık genel maliyeti** |$3,208.98 |$1,544.34 |

*Linux Distro'lar*  

Merhaba aldığınız Azure Premium Storage ile aynı düzeyde Windows ve Linux çalıştıran VM'ler için performans. Linux distro'lar birçok türdeki destekliyoruz ve hello tam listesi görmek [burada](../../virtual-machines/linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Farklı türlerde iş yükleri için farklı distro'lar daha iyi toonote uygun önemlidir. Performans, iş yükü çalıştıran hello distro bağlı olarak farklı düzeylerde görürsünüz. Merhaba Linux distro'lar uygulamanız ile test ve en iyi bir hello seçin.

Linux Premium Storage ile çalışırken, gerekli sürücüleri tooensure yüksek performansı hakkında hello en son güncelleştirmeleri denetleyin.

## <a name="premium-storage-disk-sizes"></a>Premium depolama Disk boyutları
Azure Premium Storage yedi disk boyutları şu anda sunar. Her disk boyutu IOPS, bant genişliği ve depolama için bir farklı ölçek sınırı vardır. Merhaba sağ Premium depolama Disk boyutu hello uygulama gereksinimleri ve hello yüksek ölçekli VM boyutuna bağlı olarak seçin. Merhaba tabloda hello yedi disk boyutları ve yeteneklerini gösterir. P4 ve P6 boyutları: şu anda yalnızca yönetilen diskler için desteklenir.

| Premium diskler türü  | P4    | P6    | P10   | P20   | P30   | P40   | P50   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| Disk boyutu           | 32 GB | 64 GB | 128 GB| 512 GB            | 1024 GB (1 TB)    | 2048 GB (2 TB)    | 4095 GB (4 TB)    | 
| Disk başına IOPS       | 120   | 240   | 500   | 2300              | 5000              | 7500              | 7500              | 
| Disk başına aktarım hızı | Saniye başına 25 MB  | Saniye başına 50 MB  | Saniyede 100 MB | 150 MB / saniye | 200 MB / saniye | Saniye başına 250 MB | Saniye başına 250 MB | 


Seçilen hello diskte bağlıdır seçtiğiniz kaç tane disk boyutu. Uygulama dağıtımı gereksinimi tek bir P50 disk veya birden çok P10 diskleri toomeet kullanabilirsiniz. Merhaba seçim yaparken, aşağıda listelenen hesabında dikkate alınacak noktalar alın.

*Ölçek sınırları (IOPS ve üretilen iş)*  
Her Premium disk boyutu Hello IOPS ve üretilen iş sınırları hello VM ölçek sınırlamaları uygulanmaya farklı ve bağımsız olur. Toplam IOPS hello emin olun ve verimlilik hello disklerden hello ölçek sınırları içinde seçilme VM boyutu.

Örneğin, en fazla 250 MB/sn üretilen iş bir uygulama gereksinimdir ve tek bir P30 diske sahip DS4 VM kullanıyorsanız. Merhaba DS4 VM too256 MB/sn verim verebilirsiniz. Ancak, tek bir P30 disk 200 MB/sn üretilen iş sınırı vardır. Sonuç olarak, Merhaba uygulaması 200 MB/sn toohello disk sınırı nedeniyle, kısıtlı. tooovercome bu sınır, birden fazla veri diskleri toohello VM sağlamak veya diskleri tooP40 veya P50 yeniden boyutlandırın.

> [!NOTE]
> Merhaba önbelleği tarafından sunulan okuma hello disk IOPS ve üretilen iş dahil edilmez, bu nedenle toodisk sınırları edilmez. Önbellek VM başına ayrı kendi IOPS ve üretilen iş sınırı vardır.
>
> Örneğin, başlangıçta okuma ve yazma işlemleri 60 MB/sn ve 40 MB/sn sırasıyla ' dir. Zaman içerisinde, hello önbellek warms ve daha fazla bilgi ve daha fazlasını hello okuma hello önbellekten görev yapar. Ardından, daha yüksek yazma verimlilik hello diskten elde edebilirsiniz.
>
>

*Disk sayısı*  
Uygulama gereksinimleri değerlendirerek gerekir diskleri Hello sayısını belirler. Her VM boyutu sınırı toohello VM iliştirebilirsiniz disk hello sayısı da sahiptir. Genellikle, bu iki kez hello çekirdek sayısıdır. Bu hello gereken diskler hello sayıda destekleyebilir seçtiğiniz VM boyutu emin olun.

Daha yüksek performans özellikleri karşılaştırıldığında tooStandard depolama diskleri hello Premium depolama diskleri sahip unutmayın. Standart depolama tooPremium depolama kullanarak Azure Iaas sanal makineden uygulamanızı geçiriyorsanız, bu nedenle, daha az premium diskleri gerekmesi muhtemeldir tooachieve hello aynı veya daha yüksek performans, uygulamanız için.

## <a name="disk-caching"></a>Disk önbelleği
Azure Premium Storage yararlanan yüksek ölçek VM'ler BlobCache adlı bir çok katmanlı önbelleğe alma teknoloji vardır. BlobCache önbelleğe alma işlemi için hello sanal makine RAM ve yerel SSD bileşimini kullanır. Bu önbellek hello Premium depolama kalıcı diskleri ve hello VM yerel diskler için kullanılabilir. Varsayılan olarak, bu önbellek ayarı tooRead/OS diskler için yazma ve Premium depolama alanında barındırılan veri diskleri için salt okunur olarak ayarlanır. Merhaba Premium depolama disklerde etkin disk önbelleğe alma ile Merhaba yüksek ölçekli VM'ler hello temel disk performansı aşan son derece yüksek düzeyde performans elde edebilirsiniz.

> [!WARNING]
> Azure disk Hello önbellek ayarını değiştirme ayırır ve hello hedef diski yeniden iliştirir. Merhaba işletim sistemi diski varsa hello VM yeniden başlatılır. Tüm uygulamalar/hello disk önbellek ayarını değiştirmeden önce bu kesintisi tarafından etkilenebilecek hizmetlerini durdurun.
>
>

BlobCache işleyişi hakkında daha fazla toolearn başvuran toohello içinde [Azure Premium Storage](https://azure.microsoft.com/blog/azure-premium-storage-now-generally-available-2/) blog postası.

Bu önemli tooenable hello sağ diskler kümesi üzerinde önbelleğidir. Premium disk üzerinde disk önbelleği etkinleştirmelisiniz mı hello iş yükü desenine bu diski bağımlı değil işleme. Aşağıdaki tabloda hello varsayılan işletim sistemi ve veri diskleri için önbellek ayarlarını gösterir.

| **Disk türü** | **Varsayılan önbellek ayarı** |
| --- | --- |
| İşletim sistemi diski |ReadWrite |
| Veri diski |None |

Aşağıdaki veri diskleri için önerilen disk önbellek ayarlarını Merhaba,

| **Önbelleğe alma ayarını disk** | **Ne zaman öneriye toouse bu ayarı** |
| --- | --- |
| None |Hiçbiri salt yazılır ve ağır yazma diskleri için konak önbelleği yapılandırın. |
| salt okunur |Konak önbelleği salt okunur ve okuma-yazma diskler için salt okunur olarak yapılandırın. |
| ReadWrite |Konak önbelleği yalnızca uygulamanızı düzgün yazma işliyorsa ReadWrite gerektiğinde veri toopersistent diskleri önbelleğe alınmış olarak yapılandırın. |

*Salt okunur*  
Premium depolama verileri önbelleğe alma diskleri ReadOnly yapılandırarak, düşük okuma gecikme süresine ulaşmanız ve çok yüksek okuma IOPS ve üretilen iş uygulamanız için alın. İki nedeni budur,

1. Okuma hello VM belleği ve yerel SSD önbelleğinden gerçekleştirilen, Azure blob depolama hello üzerinde olduğu hello verileri diskten okuma hızlıdır.  
2. Premium depolama hello disk IOPS ve üretilen iş doğrultusunda önbelleğinden okuma sunulan hello sayılmaz. Bu nedenle, uygulamanızın mümkün tooachieve daha yüksek olan toplam IOPS ve üretilen işi.

*ReadWrite*  
Varsayılan olarak, ReadWrite önbelleğe alma etkin hello OS diskler vardır. Yakın zamanda ReadWrite diskleri yanında verileri önbelleğe alma desteği ekledik. ReadWrite önbelleğe alma kullanıyorsanız, doğru şekilde toowrite hello veri önbelleği toopersistent disklerden olması gerekir. Örneğin, SQL Server tanıtıcıları yazma veri toohello kalıcı depolama disklerde kendi önbelleğe alınmış. Merhaba VM çökerse uygulamayla kalıcı hello işlemiyor ReadWrite önbelleği kullanılarak veri toodata kaybına yol açabilir gereklidir.

Örnek olarak, bu yönergeleri tooSQL sunucu uygulayabilirsiniz hello aşağıdakileri yaparak Premium depolama üzerinde çalışıyor

1. "Salt okunur" önbelleği premium depolama disklerde veri dosyalarını barındıran yapılandırın.  
   a.  veri sayfaları çok daha hızlı hello karşılaştırıldığında önbellek toodirectly hello veri disklerden alınır beri hello hızlı önbellek alt hello SQL Server sorgusu zamandan okur.  
   b.  Okuma önbelleğinden hizmet veren, ek işleme premium veri disklerinden kullanılabilir anlamına gelir. SQL Server daha fazla veri sayfaları ve diğer işlemleri yedekleme/geri yükleme gibi alma doğrultusunda bu ek üretilen iş kullanın, toplu iş yükleri ve dizin oluşturur.  
2. "Hiçbiri" yapılandırma önbelleği premium depolama disklerini barındırma hello günlük dosyaları.  
   a.  Günlük dosyaları öncelikle ağır yazma işlemleri sahiptir. Bu nedenle, salt okunur önbellek hello faydalanmaz.

## <a name="disk-striping"></a>Disk şeritleme
VM birkaç premium depolama kalıcı diskler ile Merhaba disklerin bağlı olduğu büyük ölçekli zaman olabilir birlikte tooaggregate kendi IOPS, bant genişliği ve depolama kapasitesini şeritli.

Windows, depolama alanları toostripe diskleri birlikte kullanabilirsiniz. Bir havuzda her disk için bir sütun yapılandırmanız gerekir. Aksi takdirde hello şeritli birim genel performansını trafiğinin hello disklere toouneven dağıtımını son beklenenden daha düşük olabilir.

Önemli: Sunucu Yöneticisi kullanıcı arabirimini kullanarak, too8 şeritli birim için sütunları hello toplam sayısını ayarlayabilirsiniz. Birden fazla 8 disk eklerken PowerShell toocreate hello birimi kullanın. PowerShell kullanarak, disk eşit toohello sayısı hello sütun sayısını ayarlayabilirsiniz. Örneğin, tek kümesi 16 diskler varsa; 16 sütundan hello belirtin *NumberOfColumns* hello parametresinin *New-VirtualDisk* PowerShell cmdlet'i.

Linux üzerinde hello MDADM yardımcı programı toostripe diskleri birlikte kullanın. Ayrıntılı adımlar Linux şeritleme disklerde çok başvurmak için[yapılandırma yazılım RAID Linux'ta](../../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

*Şerit boyutu*  
Disk şeritleme önemli bir yapılandırmada hello stripe boyutudur. Merhaba Şerit boyutu veya blok boyutu hello en küçük şeritli birim üzerinde uygulama gideren veri yığınını değil. yapılandırdığınız hello Şerit boyutu uygulama ve onun istek düzeni hello türüne bağlıdır. Merhaba yanlış Şerit boyutu seçerseniz, uygulamanızın performansını toodegraded müşteri adayları tooIO uyuşmazlığın yol açabilir.

Uygulamanız tarafından oluşturulan bir g/ç isteği hello disk stripe boyutundan daha büyükse Örneğin, hello depolama sistemi, Şerit üzerinde birim sınırları birden çok diskte yazar. Bu verileri tooaccess olduğu zaman gerçekleştirirken, birden çok Şerit birimleri toocomplete hello isteği arasında tooseek sahip olur. Bu tür davranış toplu etkisini Hello toosubstantial performans düşüşüne neden olabilir. Merhaba üzerinde hello g/ç isteği boyutu stripe boyutundan daha küçük doğası gereği rastgele ise hello g/ç istekleri hello üzerinde aynı ekleyebilir ise diğer yandan, bir performans sorununa yol açtığını ve sonuçta hello g/ç performansı önemli disk.

Uygulamanızı çalıştıran iş yükünün Hello türüne bağlı olarak, uygun stripe boyutu seçin. Rastgele küçük g/ç istekleri için daha küçük bir Şerit boyutu kullanın. Oysa için büyük sıralı g/ç istekleri daha büyük bir Şerit boyutu kullanır. Merhaba uygulaması için hello stripe boyutu önerileri Premium depolama üzerinde çalışan öğrenin. SQL Server için Şerit boyutu 64 KB OLTP iş yükleri için veri ambarı iş yükleri için 256 KB ve yapılandırın. Bkz: [Azure Vm'lerde SQL Server için performans en iyi uygulamaları](../../virtual-machines/windows/sql/virtual-machines-windows-sql-performance.md#disks-guidance) toolearn daha fazla.

> [!NOTE]
> En fazla 32 premium depolama diskleri DS serisi VM üzerinde ve GS serisi VM 64 premium depolama disklerde birlikte şeritler.
>
>

## <a name="multi-threading"></a>Çoklu iş parçacığı kullanımı
Azure Premium Storage platform toobe yüksek düzeyde paralel tasarlanmıştır. Bu nedenle, çok iş parçacıklı bir uygulama, bir tek iş parçacıklı uygulaması daha çok yüksek performans elde eder. Çok iş parçacıklı uygulama görevlerinin birden çok iş parçacıkları arasında böler ve yürütülmesinin kullanılarak hello VM tarafından verimliliğini ve disk kaynakları toohello maksimum artırır.

Örneğin, uygulamanızın tek bir çekirdek iki iş parçacığı kullanarak VM üzerinde çalışıyorsa, hello CPU hello iki iş parçacığı tooachieve verimliliği arasında geçiş yapabilirsiniz. Bir iş parçacığı üzerinde bir disk g/ç toocomplete bekliyor, ancak hello CPU başka bir iş parçacığı toohello geçiş yapabilirsiniz. Bu şekilde, iki iş parçacığı tek bir iş parçacığı misiniz fazlasını gerçekleştirebilirsiniz. Merhaba VM birden fazla çekirdek varsa, her çekirdek Paralel Görevler yürütebilir olduğundan daha fazla çalışma süresini azaltır.

Piyasada uygulamanın tek uygulayan mümkün toochange hello yolu olmayabilir iş parçacığı veya çoklu iş parçacığı kullanımı. Örneğin, SQL Server Çoklu CPU ve çok çekirdekli işleyebilir. Ancak, SQL Server hangi koşullar altında bir veya daha fazla iş parçacığı tooprocess bir sorgu özelliğinden yararlanır karar verir. Bu sorguları çalıştırmak ve çoklu iş parçacığı kullanan dizinleri oluşturun. Büyük tabloları birleştirme ve toohello kullanıcı döndürmeden önce verileri sıralama içerir bir sorgu için SQL Server büyük olasılıkla birden çok iş parçacığı kullanır. Ancak, bir kullanıcı SQL Server tek bir iş parçacığı veya birden çok iş parçacığı kullanarak bir sorgu yürütüp yürütmediğini denetleyemezsiniz.

Bu çoklu iş parçacığı veya paralel tooinfluence değiştirebilir yapılandırma ayarları bir uygulama işleme. Örneğin, SQL Server durumunda hello maksimum paralellik derecesi yapılandırma olur. Bu ayar MAXDOP, adlı tooconfigure hello en fazla SQL Server paralel işleme sırasında kullanabilir işlemci sayısını sağlar. Tek tek sorgular veya dizin işlemleri için MAXDOP yapılandırabilirsiniz. Sisteminizin toobalance kaynakları için önemli bir performans uygulamanın istediğinizde faydalıdır.

Örneğin, SQL Server kullanıyorsanız, uygulamanızı Yürütülüyor büyük bir sorgu ve bir dizin işlemini Merhaba deyin aynı anda. Bize daha fazla kullanıcı karşılaştırıldığında toohello büyük sorgu hello dizin işlemi toobe istediğinizi varsayalım. Böyle bir durumda hello dizin işlemi toobe hello MAXDOP değeri hello sorgu için daha yüksek MAXDOP değerini ayarlayabilirsiniz. Bu şekilde, SQL Server daha fazla hello dizin karşılaştırma işlemi toohello ayrılması işlemci sayısı için yararlanabilirsiniz işlemci sayısına sahip toohello büyük sorgu. Unutmayın, her işlem için SQL Server kullanacak iş parçacığı hello sayısını kontrol etmez. Merhaba en fazla işlemci için ayrılmış sayısını kontrol edebilirsiniz çoklu iş parçacığı kullanımı.

Daha fazla bilgi edinmek [derece, paralellik](https://technet.microsoft.com/library/ms188611.aspx) SQL Server'daki. Etkileyen gibi ayarları uygulamanız ve yapılandırmaları toooptimize performanslarını çoklu iş parçacığı bulmak.

## <a name="queue-depth"></a>Sıra Derinliği
Sıra Derinliği veya sırası uzunluğu hello veya sıra boyutu hello bekleyen g/ç istekleri hello sistemde sayısıdır. Sıra Derinliği Hello değerini hangi hello depolama diskleri işleme uygulamanızı hizalamak kaç tane g/ç işlemleri belirler. Bu makale viz. içinde IOPS, üretilen iş ve gecikme konuştuğumuz tüm hello üç uygulama performans göstergelerini etkiler.

Sıra Derinliği ve çoklu iş parçacığı olan yakından ilgili. Merhaba sıra derinliği değeri çoklu iş parçacığı ne kadar seçilebileceğini gösterir hello uygulama tarafından elde edilebilir. Merhaba sıra derinliği büyükse, uygulama daha fazla işlem eşzamanlı olarak, diğer bir deyişle, yürütebilir birden çok iş parçacığı. Uygulamanın çok iş parçacıklı olsa bile hello sıra derinliği, küçükse, eş zamanlı yürütme için tabandaki yeterli istekleri sahip değil.

Genellikle, hello devre dışı raf uygulamaları toochange hello sıra derinliği için izin vermez, yanlış bunu iyi'den daha fazla zarar ayarlayın. Uygulamaları hello sağ sıra derinliği tooget hello en iyi performans değerini ayarlar. Ancak, bu önemli toounderstand, bu kavram, böylelikle uygulamanızla performans sorunlarını giderebilirsiniz. Sıra Derinliği hello etkilerini sisteminizde Kıyaslama Araçlar çalıştırarak da görebilirsiniz.

Bazı uygulamalar, ayarlar tooinfluence hello sıra derinliği sağlar. Örneğin, SQL Server'da hello MAXDOP (maksimum paralellik derecesi) ayarı önceki bölümde açıklanmıştır. MAXDOP olduğu şekilde tooinfluence sıra derinliği ve çoklu iş parçacığı hello sıra derinliği değeri SQL Server'ın doğrudan değiştirmez ancak.

*Yüksek sıra derinliği*  
Merhaba disk üzerinde daha fazla işlem yukarı yüksek sıra derinliği satırları. Merhaba disk vaktinden kendi sırasındaki sonraki istek hello bilir. Sonuç olarak, hello disk işlemleri önceden zamanlayabilir ve en iyi bir sırayla işlem. Daha fazla istekleri toohello disk Hello uygulama gönderme olduğundan, daha fazla paralel IOs hello disk işleyebilir. Merhaba uygulama mümkün tooachieve nihayetinde olacak yüksek IOPS. Uygulama daha fazla isteği işleme beri hello Merhaba uygulaması toplam verimini da artırır.

Genellikle, bir uygulama 8 ile en yüksek verimlilik elde edebilirsiniz-16 + bekleyen GÇ ekli disk başına. Sıra Derinliği ise, uygulama yeterli IOs toohello sistemi dağıtmaya değil ve belirli bir dönemde daha az miktarda işleme. Diğer bir deyişle, daha az işleme.

Örneğin, SQL Server'da ayarı hello MAXDOP değeri bir sorgu için çok "4" toofour çekirdek tooexecute hello sorgulamasını kullanabilmek için SQL Server bildirir. SQL Server en iyi sıra derinliği değeri ve hello çekirdek sayısı hello sorgu yürütmesi için nedir belirler.

*En iyi sıra derinliği*  
Çok yüksek sıra derinliği değeri de kendi sakıncaları vardır. Sıra Derinliği değeri çok yüksekse, Merhaba uygulaması toodrive deneyecek çok yüksek IOPS. Uygulama yeterli sağlanan IOPS kalıcı disklerle olmadığı sürece, bu uygulama gecikme sürelerini olumsuz yönde etkileyebilir. Formül aşağıdaki IOPS, gecikme ve sıra derinliği arasındaki hello ilişkiyi gösterir.  
    ![](media/storage-premium-storage-performance/image6.png)

Sıra Derinliği tooany yüksek değerli ancak Merhaba uygulaması için yeterli IOPS gecikmeleri etkilemeden teslim tooan en iyi değer yapılandırmamalısınız. Örneğin, Hello uygulama gecikme toobe 1 milisaniyelik gerekirse, hello sıra derinliği 5.000 IOPS'yi olan tooachieve QD gerekli = 5000 x 0,001 = 5.

*Şeritli birim için sıra derinliği*  
Her diski ayrı ayrı bir en yüksek sıra derinliği sahip olacağı şekilde, bir şeritli birim için yeterince yüksek sıra derinliğini korumak. Örneğin, bir sıra derinliği 2 iter uygulamanın göz önünde bulundurun ve hello Şerit içine 4 disk yok. Merhaba iki g/ç isteği tootwo diskleri geçilir ve iki disk kalan boş olacaktır. Bu nedenle, tüm hello diskleri meşgul gibi hello sıra derinliği yapılandırın. Aşağıdaki formülü nasıl toodetermine hello şeritli birimler sıra derinliği gösterir.  
    ![](media/storage-premium-storage-performance/image7.png)

## <a name="throttling"></a>Azaltma
Azure Premium Storage hükümleri IOPS ve üretilen iş sayısı hello VM boyutları ve seçtiğiniz disk boyutları bağlı olarak belirtilen. Uygulamanızın hangi hello VM veya disk işleyebilir, bu sınırları yukarıda toodrive IOPS veya verimlilik çalışır verdiğinizde, Premium Storage bu kısıtlama. Bu, uygulamanızda performans hello biçiminde bildirimleri. Bu daha yüksek gecikme anlamına gelir, üretilen iş alt veya IOPS düşürün. Premium depolama kısıtlama değil, uygulamanızın tümüyle kaynaklarını elde özellikli nelerdir aşan başarısız olabilir. Bu nedenle, tooavoid performans son sorunları toothrottling, her zaman sağla yeterli kaynak uygulamanız için. Biz hello VM boyutları ve Disk boyutları bölümler yukarıda açıklanan dikkate alın. Değerlendirmesi olduğu hello en iyi şekilde toofigure hangi kaynakları toohost uygulamanız gerekir.

## <a name="benchmarking"></a>Değerlendirmesi
Değerlendirmesi farklı iş yükleri, uygulamanızın üzerinde benzetimini yapma ve her iş yükü için hello uygulama performansını ölçmek hello işlemidir. Bir önceki bölümde açıklanan başlangıç adımları kullanarak, hello uygulama performans gereksinimlerini aldınız. Araçlar hello uygulama barındırma hello vm'lerinde değerlendirmesi çalıştırarak uygulamanızı Premium Storage ile elde edebilirsiniz hello performans düzeylerini belirleyebilirsiniz. Bu bölümde, Azure Premium Storage diskler ile sağlanan standart bir DS14 VM değerlendirmesi örnekleri sunuyoruz.

Ortak Kıyaslama araçları Iometer ve FIO, Windows ve Linux için sırasıyla kullandık. Bu araçlar iş yükü ve ölçü hello sistem performansı gibi bir üretim benzetimi birden çok iş parçacığı oluşturma. Merhaba araçlarını kullanarak, bir uygulama için normalde değiştiremezsiniz blok boyutu ve sıra derinliğini gibi parametreleri de yapılandırabilirsiniz. Bu, daha fazla esneklik toodrive hello en yüksek performans yüksek ölçekte farklı uygulama iş yükleri için premium diskler ile sağlanan VM sağlar. Her Kıyaslama aracı hakkında daha fazla ziyaret toolearn [Iometer](http://www.iometer.org/) ve [FIO](http://freecode.com/projects/fio).

toofollow hello aşağıdaki örneklerde, standart DS14 VM oluşturun ve 11 Premium depolama diskleri toohello VM ekleyin. Hello 11 disklerin NoCacheWrites adlı bir birim şeritler ve ana bilgisayar "None" önbelleğe almayı ile 10 diskleri yapılandırın. Ana bilgisayar "Salt okunur olarak" Merhaba kalan disk üzerinde önbelleğe almayı yapılandırın ve bu diski CacheReads adlı bir birim oluşturun. Bu ayarı kullanarak, mümkün toosee hello maksimum okuma ve yazma performansı standart DS14 VM olacaktır. Premium diskler ile DS14 VM oluşturma hakkında ayrıntılı adımlar için çok Git[oluşturma ve kullanma bir Premium depolama hesabı için sanal makine veri diski](../storage-premium-storage.md).

*Önbellek Hello ısıtma*  
salt okunur ana bilgisayar önbelleğe almayı Hello diskle mümkün toogive olacaktır hello disk sınırdan daha yüksek IOPS. tooget bu maksimum performans hello konak önbellekten oku, önce bu diskin hello önbelleği sıcak gerekir. Bu, o hello okuma hangi Kıyaslama aracı CacheReads birimde yol açacak IOs gerçekten hello önbellek ve hello disk değil doğrudan isabetler sağlar. Merhaba Önbelleği İsabetli Okuma sonucu hello tek önbelleğinden ek IOPS disk etkin.

> **Önemli:**  
> VM yeniden başlatılıncaya kadar her zaman değerlendirmesi, çalıştırmadan önce hello önbelleği sıcak gerekir.
>
>

#### <a name="iometer"></a>Iometer
[Merhaba Iometer Aracı'nı indirme](http://sourceforge.net/projects/iometer/files/iometer-stable/2006-07-27/iometer-2006.07.27.win32.i386-setup.exe/download) hello VM üzerinde.

*Sınama dosyası*  
Iometer test değerlendirmesi hello çalışacağı hello biriminde depolanan bir test dosyası kullanır. Okuma sürücüler ve dosya toomeasure hello disk IOPS ve üretilen iş yazma bu test edin. Bir sağlamadınız değilse Iometer bu test dosyası oluşturur. Merhaba CacheReads ve NoCacheWrites birimlerde iobw.tst adlı bir 200 GB test dosyası oluşturun.

*Access belirtimleri*  
Merhaba belirtimleri, istek % okuma/yazma g/ç boyutu, % rastgele/sıralı yapılandırılmış olan Iometer içinde hello "Access belirtimleri" sekmesini kullanarak. Aşağıda açıklanan hello senaryoların her biri için bir erişim belirtimi oluşturun. Hello access belirtimleri oluşturun ve "Kaydet" uygun bir ad gibi – RandomWrites\_8K, RandomReads\_8 K. Merhaba karşılık gelen belirtimini hello testi senaryosu çalıştırırken seçin.

Access belirtimleri maksimum IOPS yazma senaryo örneği aşağıda gösterilen,  
    ![](media/storage-premium-storage-performance/image8.png)

*Maksimum IOPS Test belirtimleri*  
toodemonstrate maksimum IOPS, daha küçük isteği boyutu kullanın. 8 K istek boyutu ve rastgele yazma ve okuma için belirtimler oluşturmak.

| Erişim belirtimi | İsteği boyutu | Rastgele % | Okuma % |
| --- | --- | --- | --- |
| RandomWrites\_8 K |8K |100 |0 |
| RandomReads\_8 K |8K |100 |100 |

*En yüksek verimlilik Test belirtimleri*  
toodemonstrate en yüksek verimlilik, kullanımı daha büyük isteği boyutu. 64 K istek boyutu ve rastgele yazma ve okuma için belirtimler oluşturmak.

| Erişim belirtimi | İsteği boyutu | Rastgele % | Okuma % |
| --- | --- | --- | --- |
| RandomWrites\_64 K |64K |100 |0 |
| RandomReads\_64 K |64K |100 |100 |

*Merhaba Iometer Test çalıştırma*  
Önbellek toowarm Hello adımları uygulamanız

1. Aşağıda gösterilen değerleri içeren iki erişim belirtimleri oluşturun

   | Ad | İsteği boyutu | Rastgele % | Okuma % |
   | --- | --- | --- | --- |
   | RandomWrites\_1 MB |1MB |100 |0 |
   | RandomReads\_1 MB |1MB |100 |100 |
2. Aşağıdaki parametrelerle önbellek disk başlatma için hello Iometer testi çalıştırın. Üç çalışan iş parçacığı hello hedef birim ve 128 sıra derinliği için kullanın. Ayarlama süresi hello test too2hrs hello "Test Kur" sekmesinde "çalışma zamanı" Merhaba.

   | Senaryo | Hedef birim | Ad | Süre |
   | --- | --- | --- | --- |
   | Önbellek diski başlatın |CacheReads |RandomWrites\_1 MB |2hrs |
3. Aşağıdaki parametrelerle önbellek disk ısıtma için hello Iometer testi çalıştırın. Üç çalışan iş parçacığı hello hedef birim ve 128 sıra derinliği için kullanın. Ayarlama süresi hello test too2hrs hello "Test Kur" sekmesinde "çalışma zamanı" Merhaba.

   | Senaryo | Hedef birim | Ad | Süre |
   | --- | --- | --- | --- |
   | Önbellek diski sıcak |CacheReads |RandomReads\_1 MB |2hrs |

Önbellek disk warmed sonra aşağıda listelenen hello test senaryoları ile devam edin. toorun hello Iometer test kullanmak için en az üç çalışan iş parçacığı **her** hedef birim. Her çalışan iş parçacığı hello hedef birimi seçin, sıra derinliği ayarlayın ve kaydedilen hello test belirtimleri birini hello tablo toorun hello karşılık gelen test senaryosu aşağıda gösterildiği gibi seçin. Merhaba tabloda ayrıca beklenen sonuçları IOPS ve üretilen iş için bu testleri çalıştırırken gösterilir. Tüm senaryolarda, küçük g/ç boyutu 8KB ve 128 yüksek sıra derinliği kullanılır.

| Test senaryosu | Hedef birim | Ad | Sonuç |
| --- | --- | --- | --- |
| En çok, Okuma IOPS |CacheReads |RandomWrites\_8 K |50.000 IOPS |
| En çok, IOPS yazma |NoCacheWrites |RandomReads\_8 K |64.000 IOPS |
| En çok, Birleşik IOPS |CacheReads |RandomWrites\_8 K |100.000 IOPS |
| NoCacheWrites |RandomReads\_8 K | &nbsp; | &nbsp; |
| En çok, Okuma MB/sn |CacheReads |RandomWrites\_64 K |524 MB/sn |
| En çok, Yazma MB/sn |NoCacheWrites |RandomReads\_64 K |524 MB/sn |
| Birleşik MB/sn |CacheReads |RandomWrites\_64 K |1000 MB/sn |
| NoCacheWrites |RandomReads\_64 K | &nbsp; | &nbsp; |

Aşağıda birleşik IOPS ve üretilen iş senaryoları için Iometer test sonuçlarını hello ekran görüntüleri verilmiştir.

*Birleşik okuma ve yazma işlemleri maksimum IOPS*  
![](media/storage-premium-storage-performance/image9.png)

*Birleşik okuma ve yazma işlemleri en yüksek verimlilik*  
![](media/storage-premium-storage-performance/image10.png)

### <a name="fio"></a>FIO
FIO popüler araç toobenchmark depolama hello Linux VM'ler üzerinde ' dir. Merhaba esneklik tooselect farklı GÇ boyutları, sıralı veya rastgele okuma ve yazma işlemleri vardır. G/ç işlemleri işlemleri tooperform hello belirtilen veya çalışan iş parçacığı olarak çoğaltılır. Her iş parçacığı iş dosyalarını kullanarak gerçekleştirmelidir g/ç işlemleri hello türünü belirtebilirsiniz. Merhaba aşağıdaki örnekte gösterilen senaryoda her bir iş dosyası oluşturduk. Premium depolama üzerinde çalışan bu iş dosyaları toobenchmark farklı iş yükleri hello teknik özelliklerine değiştirebilirsiniz. Merhaba örneklerde, standart DS 14 VM çalışan bir kullanıyoruz **Ubuntu**. Aynı kurulum hello hello başlangıcını içinde açıklanan kullanım hello [bölüm değerlendirmesi](#Benchmarking) ve testleri değerlendirmesi hello çalıştırmadan önce hello önbellek sıcak.

Başlamadan önce [FIO karşıdan](https://github.com/axboe/fio) ve sanal makinenize yükleyin.

Ubuntu için komutu aşağıdaki hello Çalıştır

```
apt-get install fio
```

Yazma işlemlerini yürüten için dört çalışan iş parçacıkları ve dört çalışan iş parçacığı hello disklerde yönlendirmeli okuma işlemleri için kullanacağız. Merhaba yazma çalışanları trafiği çok ayarlamak önbellekle 10 diske sahip hello "nocache" birimde yürüten "None". Merhaba okuma çalışanları trafiği 1 disk önbelleği kümesiyle çok sahip hello "readcache" birimde yürüten "Salt okunur".

*Maksimum yazma IOPS*  
İle aşağıdaki özellikleri tooget Hello proje dosyası oluşturma maksimum IOPS yazma. "Fiowrite.ini" adı.

```
[global]
size=30g
direct=1
iodepth=256
ioengine=libaio
bs=8k

[writer1]
rw=randwrite
directory=/mnt/nocache
[writer2]
rw=randwrite
directory=/mnt/nocache
[writer3]
rw=randwrite
directory=/mnt/nocache
[writer4]
rw=randwrite
directory=/mnt/nocache
```

Not hello önceki bölümlerde açıklanan hello tasarım yönergeleri uyumlu olan temel görevlerden izleyin. Bu belirtimler temel toodrive olan maksimum IOPS  

* 256 yüksek sıra derinliği.  
* Küçük blok boyutu 8 KB.  
* Birden çok iş parçacığı rastgele yazma işlemlerini gerçekleştirme.

Komut tookick FIO test 30 saniye hello kapalı aşağıdaki hello Çalıştır  

```
sudo fio --runtime 30 fiowrite.ini
```

Merhaba test çalışırken mümkün toosee hello IOPS hello VM ve Premium disklerin teslim yazma sayısı olacaktır. Örnek Hello aşağıda gösterildiği gibi hello DS14 VM kendi maksimum IOPS sınırı 50.000 IOPS yazma iletmektir.  
    ![](media/storage-premium-storage-performance/image11.png)

*Maksimum IOPS okuma*  
İle aşağıdaki özellikleri tooget Hello proje dosyası oluşturma maksimum okuma IOPS. "Fioread.ini" adı.

```
[global]
size=30g
direct=1
iodepth=256
ioengine=libaio
bs=8k

[reader1]
rw=randread
directory=/mnt/readcache
[reader2]
rw=randread
directory=/mnt/readcache
[reader3]
rw=randread
directory=/mnt/readcache
[reader4]
rw=randread
directory=/mnt/readcache
```

Not hello önceki bölümlerde açıklanan hello tasarım yönergeleri uyumlu olan temel görevlerden izleyin. Bu belirtimler temel toodrive olan maksimum IOPS

* 256 yüksek sıra derinliği.  
* Küçük blok boyutu 8 KB.  
* Birden çok iş parçacığı rastgele yazma işlemlerini gerçekleştirme.

Komut tookick FIO test 30 saniye hello kapalı aşağıdaki hello Çalıştır

```
sudo fio --runtime 30 fioread.ini
```

Hello test çalışırken mümkün toosee hello okuma IOPS hello VM sayısı olacaktır ve Premium diskleri gönderiliyor. Örnek Hello aşağıda gösterildiği gibi hello DS14 VM birden fazla 64.000 okuma IOPS iletmektir. Merhaba disk ve hello önbelleği performansı birleşimidir.  
    ![](media/storage-premium-storage-performance/image12.png)

*En fazla okuma ve yazma IOPS*  
Oluşturma aşağıdaki belirtimler tooget maksimum hello iş dosyasıyla birlikte okuma ve yazma IOPS. "Fioreadwrite.ini" adı.

```
[global]
size=30g
direct=1
iodepth=128
ioengine=libaio
bs=4k

[reader1]
rw=randread
directory=/mnt/readcache
[reader2]
rw=randread
directory=/mnt/readcache
[reader3]
rw=randread
directory=/mnt/readcache
[reader4]
rw=randread
directory=/mnt/readcache

[writer1]
rw=randwrite
directory=/mnt/nocache
rate_iops=12500
[writer2]
rw=randwrite
directory=/mnt/nocache
rate_iops=12500
[writer3]
rw=randwrite
directory=/mnt/nocache
rate_iops=12500
[writer4]
rw=randwrite
directory=/mnt/nocache
rate_iops=12500
```

Not hello önceki bölümlerde açıklanan hello tasarım yönergeleri uyumlu olan temel görevlerden izleyin. Bu belirtimler temel toodrive olan maksimum IOPS

* 128 yüksek sıra derinliği.  
* Küçük blok boyutu 4 KB.  
* Birden çok iş parçacığı rastgele gerçekleştirme okur ve yazar.

Komut tookick FIO test 30 saniye hello kapalı aşağıdaki hello Çalıştır

```
sudo fio --runtime 30 fioreadwrite.ini
```

Merhaba test çalışırken mümkün toosee hello birleşik okuma sayısı ve VM hello ve Premium diskleri ileterek IOPS yazma. Örnek Hello aşağıda gösterildiği gibi hello DS14 VM 100. 000'den fazla birleşik okuma ve yazma IOPS iletmektir. Merhaba disk ve hello önbelleği performansı birleşimidir.  
    ![](media/storage-premium-storage-performance/image13.png)

*En büyük verimi birleştirilmiş*  
Okuma ve yazma verimlilik tooget hello maksimum birlikte, daha büyük blok boyutu ve büyük sıra derinliği okuma ve yazma işlemleri gerçekleştiren birden çok iş parçacığı ile kullanın. 64 KB blok boyutunu ve sıra derinliği 128 kullanabilirsiniz.

## <a name="next-steps"></a>Sonraki Adımlar
Azure Premium Storage hakkında daha fazla bilgi edinin:

* [Premium Depolama: Azure Sanal Makine İş Yükleri için Yüksek Performanslı Depolama](../storage-premium-storage.md)  

SQL Server kullanıcıları için SQL Server için performans en iyi uygulamaları makalelerini okuyun:

* [Azure sanal makinelerde SQL Server için performans en iyi yöntemler](../../virtual-machines/windows/sql/virtual-machines-windows-sql-performance.md)
* [Azure Premium Storage Azure VM'deki SQL Server için en yüksek performans sağlar](http://blogs.technet.com/b/dataplatforminsider/archive/2015/04/23/azure-premium-storage-provides-highest-performance-for-sql-server-in-azure-vm.aspx)
