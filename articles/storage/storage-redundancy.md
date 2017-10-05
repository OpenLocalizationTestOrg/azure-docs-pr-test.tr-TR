---
title: "Azure Storage veri çoğaltması | Microsoft Docs"
description: "Microsoft Azure depolama hesabınızdaki veriler dayanıklılık ve yüksek kullanılabilirlik için çoğaltılır. Çoğaltma seçenekleri yerel olarak yedekli depolama (LRS), bölge olarak yedekli depolama (ZRS), coğrafi olarak yedekli depolama (GRS) ve okuma erişimli coğrafi olarak yedekli depolama (RA-GRS) içerir."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 86bdb6d4-da59-4337-8375-2527b6bdf73f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: marsma
ms.openlocfilehash: b9354484ff5b81e2561d017d039bf2c07a21a423
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-storage-replication"></a>Azure Storage çoğaltma

Microsoft Azure Depolama hesabınızdaki veriler, dayanıklılık ve yüksek kullanılabilirlik sağlamak için her zaman çoğaltılır. Çoğaltma işlemi, belirlediğiniz çoğaltma seçeneğine göre verilerinizi aynı veri merkezine veya ikinci bir veri merkezine kopyalar. Çoğaltma işlemi, geçici donanım hataları söz konusu olduğunda uygulamanızın çalışma süresini ve verilerinizi korur. Verileriniz için ikinci bir veri merkezi çoğaltılır, birincil konumda yıkıcı bir hatadan korunmaktadır.

Çoğaltma işlemi, hata durumunda bile depolama hesabınızın [Depolama için Hizmet Düzeyi Sözleşmesi'ne (SLA)](https://azure.microsoft.com/support/legal/sla/storage/) uymasını sağlar. Azure Depolama'nın dayanıklılık ve kullanılabilirlikle ilgili sağladığı garantiler hakkında bilgi edinmek için SLA'ya göz atın.

Bir depolama hesabı oluşturduğunuzda şu çoğaltma seçeneklerinden birini seçebilirsiniz:

* [Yerel olarak yedekli depolama (LRS)](#locally-redundant-storage)
* [Bölgesel olarak yedekli depolama (ZRS)](#zone-redundant-storage)
* [Coğrafi olarak yedekli depolama (GRS)](#geo-redundant-storage)
* [Okuma erişimli coğrafi olarak yedekli depolama (RA-GRS)](#read-access-geo-redundant-storage)

Bir depolama hesabı oluşturduğunuzda okuma erişimli coğrafi olarak yedekli depolama (RA-GRS) varsayılan seçenektir.

Aşağıdaki tabloda daha ayrıntılı çoğaltma her türünü sonraki bölümlerinde ele LRS, ZRS, GRS ve RA-GRS, arasındaki farklar hızlı bir genel bakış sağlar.

| Çoğaltma stratejisi | LRS | ZRS | GRS | RA-GRS |
|:--- |:--- |:--- |:--- |:--- |
| Veriler birden çok veri merkezi arasında çoğaltılır. |Hayır |Evet |Evet |Evet |
| Verileri ikincil bir konuma yanı sıra birincil konumda okuyabilir. |Hayır |Hayır |Hayır |Evet |
| Ayrı düğümlerde tutulan veri kopyası sayısı. |3 |3 |6 |6 |

Bkz: [Azure Storage fiyatlandırması](https://azure.microsoft.com/pricing/details/storage/) farklı artıklık seçenekleri için fiyatlandırma bilgilerini için.

> [!NOTE]
> Premium depolama yalnızca yerel olarak yedekli depolama (LRS) destekler. Premium depolama hakkında daha fazla bilgi için bkz: [Premium Storage: Azure sanal makine iş yükleri için yüksek performanslı depolama](storage-premium-storage.md).
>

> [!NOTE]
> Azure File storage, yalnızca yerel olarak yedekli depolama (LRS) ve georedundant depolama (GRS) destekler. Azure File Storage hakkında daha fazla bilgi için bkz: [Azure File storage genel bakış](storage-files-introduction.md).
>

## <a name="locally-redundant-storage"></a>Yerel olarak yedekli depolama
Yerel olarak yedekli depolama (LRS), depolama hesabınız oluşturuldu bölgede bir veri merkezinde barındırılır üç kez bir depolama ölçek birimi içindeki verilerinizi çoğaltır. Yalnızca tüm üç çoğaltmalar için yazıldıktan sonra Yazma isteği başarıyla döndürür. Bu üç çoğaltmaların her ayrı hata etki alanları ve bir depolama ölçek birimi içinde yükseltme etki alanları bulunur.

Bir depolama ölçek birimi depolama düğümleri raflarının koleksiyonudur. Hata etki alanı (FD) hata fiziksel bir birimi temsil eder ve aynı fiziksel raf ait düğümleri olarak kabul düğümlerinin bir gruptur. Bir yükseltme etki alanına (UD), hizmet yükseltmesi (sunum) işlemi sırasında birlikte yükseltilir düğümleri grubudur. Üç çoğaltmaları verileri tek bir rafa donanım arızası etkiler olsa bile veya düğümler piyasaya sürme sırasında yükseltildiğinde olduğundan emin olmak için bir depolama ölçek birimi içinde UDs ve FDs yayılır.

LRS en düşük maliyeti seçeneği ve diğer seçenekleri karşılaştırıldığında en az düzeyde dayanıklılık sunar. Bir veri merkezi düzeyi olağanüstü (vb. taşmasını yangın) durumda, tüm üç çoğaltmaları kayıp veya kurtarılamaz olabilir. Bu riski azaltmak için coğrafi olarak yedekli depolama (GRS) çoğu uygulama için önerilir.

Yerel olarak yedekli depolama hala belirli senaryolarda istenebilir:

* En yüksek bant genişliği üst sınırı Azure Storage çoğaltma seçenekleri sağlar.
* Uygulamanızı kolayca canlandırılabilir veri depoluyorsa, LRS için tercih edebilirsiniz.
* Bazı uygulamalar, yalnızca veri idare gereksinimleri nedeniyle bir ülke içinde veri çoğaltmak için kısıtlanır. Eşleştirilmiş bir bölge başka bir ülkede olabilir. Bölge çiftleri hakkında daha fazla bilgi için bkz: [Azure bölgeleri](https://azure.microsoft.com/regions/).

## <a name="zone-redundant-storage"></a>Bölge olarak yedekli depolama
Bölge olarak yedekli depolama (ZRS) verilerinizi benzer LRS, böylece LRS'den daha fazla dayanıklılık sağlamak için üç çoğaltmaları depolamak yanı sıra bir veya iki bölgeleri içindeki veri merkezleri arasında zaman uyumsuz olarak çoğaltır. Birincil veri merkezindeki kullanılamıyor veya kurtarılamaz olsa bile, ZRS içinde depolanan verileri dayanıklı.
ZRS kullanmayı planlıyorsanız müşteriler kullanan:

* ZRS, yalnızca blok bloblar genel amaçlı depolama hesapları için kullanılabilir ve yalnızca depolama hizmeti sürümleri 2014-02-14 içinde ve üzerinde desteklenir.
* Zaman uyumsuz çoğaltma bir gecikme gerektirdiğinden, yerel bir olağanüstü durumda birincil sunucudan verileri kurtarılamazsa, ikincil henüz çoğaltılmamış değişiklikler kaybolacak mümkündür.
* İkincil bir yük devretme Microsoft başlatana kadar çoğaltma kullanılamayabilir.
* ZRS hesapları daha sonra LRS veya GRS dönüştürülemez. Benzer şekilde, varolan LRS veya GRS hesabı ZRS hesabına dönüştürülemiyor.
* ZRS hesapları, ölçümleri veya günlüğe kaydetme özelliğine sahip.

## <a name="geo-redundant-storage"></a>Coğrafi Olarak Yedekli Depolama
Coğrafi olarak yedekli depolama (GRS) verileriniz birincil bölge çıktığınızda mil yüzlerce olan ikincil bir bölgeye çoğaltır. Etkin GRS depolama hesabınız varsa, verilerinizi bile tam bölgesel bir kesintinin veya bir olağanüstü durumda birincil bölge kurtarılabilir değil söz konusu olduğunda dayanıklı.

Etkin GRS ile bir depolama hesabı için bir güncelleştirme burada üç kez çoğaltılır birincil bölge için ilk kararlıdır. Daha sonra güncelleştirmeyi zaman uyumsuz olarak burada bunu da üç kez çoğaltılır ikincil bölgeye çoğaltılır.

GRS ile birincil ve ikincil bölgeler çoğaltmalar ayrı hata etki alanlarında yönetmek ve etki alanı ile LRS açıklandığı gibi bir depolama ölçek birimi içinde yükseltin.

Dikkate alınacak noktalar:

* Zaman uyumsuz çoğaltma bir gecikme gerektirdiğinden, bölgesel bir olağanüstü durumda birincil bölgesinden veri kurtarılamazsa, ikincil bölge'ye henüz çoğaltılmamış değişiklikler kaybolacak mümkündür.
* Microsoft yük devretme ikincil bölge başlatır sürece çoğaltma kullanılamıyor. Microsoft bir yük devretme ikincil bölge başlatın varsa, okuduğunuz ve yük devretme sonrasında bu verilere yazma erişimi tamamlandı. Daha fazla bilgi için lütfen bkz [olağanüstü durum kurtarma Kılavuzu](storage-disaster-recovery-guidance.md). 
* Kullanıcı, bir uygulama ikincil bölgesinden okumak isterse, RA-GRS etkinleştirmeniz gerekir.

Bir depolama hesabı oluşturduğunuzda, hesap için birincil bölge seçin. İkincil bölge birincil bölgeye göre belirlenir ve değiştirilemez. Aşağıdaki tabloda birincil ve ikincil bölge eşleştirmeleri gösterilir.

| Birincil | İkincil |
| --- | --- |
| Orta Kuzey ABD |Orta Güney ABD |
| Orta Güney ABD |Orta Kuzey ABD |
| Doğu ABD |Batı ABD |
| Batı ABD |Doğu ABD |
| ABD Doğu 2 |Orta ABD |
| Orta ABD |ABD Doğu 2 |
| Kuzey Avrupa |Batı Avrupa |
| Batı Avrupa |Kuzey Avrupa |
| Güneydoğu Asya |Doğu Asya |
| Doğu Asya |Güneydoğu Asya |
| Doğu Çin |Kuzey Çin |
| Kuzey Çin |Doğu Çin |
| Japonya Doğu |Japonya Batı |
| Japonya Batı |Japonya Doğu |
| Güney Brezilya |Orta Güney ABD |
| Avustralya Doğu |Avustralya Güneydoğu |
| Avustralya Güneydoğu |Avustralya Doğu |
| Hindistan Güney |Hindistan Orta |
| Hindistan Orta |Hindistan Güney |
| Hindistan Batı |Hindistan Güney |
| ABD Devleti Iowa |ABD Devleti Virginia |
| ABD Devleti Virginia |ABD Devleti Texas |
| ABD Devleti Texas |ABD Devleti Arizona |
| ABD Devleti Arizona |ABD Devleti Texas |
| Orta Kanada |Doğu Kanada |
| Doğu Kanada |Orta Kanada |
| Birleşik Krallık Batı |Birleşik Krallık Güney |
| Birleşik Krallık Güney |Birleşik Krallık Batı |
| Almanya Orta |Almanya Kuzeydoğu |
| Almanya Kuzeydoğu |Almanya Orta |
| Batı ABD 2 |Batı Orta ABD |
| Batı Orta ABD |Batı ABD 2 |

Azure tarafından desteklenen bölgeler hakkında güncel bilgiler için bkz: [Azure bölgeleri](https://azure.microsoft.com/regions/).

>[!NOTE]  
> ABD kamu Virginia ikincil BİZE kamu Texas bölgedir. Daha önce BİZE kamu Virginia BİZE kamu Iowa bir ikincil bölge ' kullanılan. Depolama hesapları hala bir ikincil bölge'olarak BİZE kamu Iowa yararlanan bir ikincil bölge BİZE kamu Texas Geçirilmekte olan. 
> 
> 

## <a name="read-access-geo-redundant-storage"></a>Coğrafi olarak yedekli depolamaya okuma erişimi
Okuma erişimli coğrafi olarak yedekli depolama (RA-GRS) GRS tarafından sağlanan iki bölgede çoğaltma ek olarak ikincil konumdaki verileri salt okunur erişim sağlayarak depolama hesabınız için kullanılabilirliği en üst düzeye çıkarır.

İkincil bölge verilerinize salt okunur erişimi etkinleştirdiğinizde, verilerinizi depolama hesabınız için birincil endpoint ek olarak ikincil bir uç noktası kullanılabilir. İkincil uç birincil uç noktasına benzer, ancak son ekine ekler `–secondary` hesap adı. Örneğin, Blob Hizmeti uç noktanızı birincil ise `myaccount.blob.core.windows.net`, ikincil uç noktanız ise `myaccount-secondary.blob.core.windows.net`. Erişim tuşları depolama hesabınız için birincil ve ikincil uç için aynıdır.

Dikkate alınacak noktalar:

* Bunu ile RA-GRS kullanırken etkileşimde hangi uç noktaya yönetmek, uygulamanızın sahiptir.
* Zaman uyumsuz çoğaltma bir gecikme gerektirdiğinden, bölgesel bir olağanüstü durumda birincil bölgesinden veri kurtarılamazsa, ikincil bölge'ye henüz çoğaltılmamış değişiklikler kaybolacak mümkündür.
* Microsoft ikincil bölgeye yük devretme durumunda başlatır, okuduğunuz ve yük devretme sonrasında bu verilere yazma erişimi tamamlandı. Daha fazla bilgi için lütfen bkz [olağanüstü durum kurtarma Kılavuzu](storage-disaster-recovery-guidance.md). 
* RA-GRS, yüksek kullanılabilirlik sağlamak için tasarlanmıştır. Ölçeklenebilirlik yönergeleri için lütfen inceleyin [performans denetim listesi](storage-performance-checklist.md).

## <a name="frequently-asked-questions"></a>Sık sorulan sorular

<a id="howtochange"></a>
#### <a name="1-how-can-i-change-the-geo-replication-type-of-my-storage-account"></a>1. Depolama Hesabımı coğrafi çoğaltma türünü nasıl değiştirebilir miyim?

   Depolama hesabınız LRS, GRS ve RA-GRS kullanarak arasında coğrafi çoğaltma türünü değiştirebilirsiniz [Azure portal](https://portal.azure.com/), [Azure Powershell](storage-powershell-guide-full.md) veya program aracılığıyla bizim birçok depolama istemci kitaplıklarından birini kullanma. Lütfen ZRS hesapları dönüştürülen LRS veya GRS olamayacağını unutmayın. Benzer şekilde, varolan LRS veya GRS hesabı ZRS hesabına dönüştürülemiyor.

<a id="changedowntime"></a>
#### <a name="2-will-there-be-any-down-time-if-i-change-the-replication-type-of-my-storage-account"></a>2. Depolama Hesabımı çoğaltma türünü değiştirirseniz var. herhangi kesinti olacak?

   Hayır, olmayacak herhangi kesinti.

<a id="changecost"></a>
#### <a name="3-will-there-be-any-additional-cost-if-i-change-the-replication-type-of-my-storage-account"></a>3. Depolama Hesabımı çoğaltma türünü değiştirirseniz, ek bir maliyet var. olacak mı?

   Evet. Depolama hesabınız için GRS (veya RA-GRS) LRS'den değiştirirseniz, var olan verileri birincil konumdan ikincil konuma kopyalanması söz konusu çıkışı için ek bir ücret doğurur. İlk veri kopyalandıktan sonra coğrafi veri birincil sunucudan ikincil konuma çoğaltmak için daha fazla ek çıkış ücretsiz yoktur. Bant genişliği ücretleri ayrıntılarını bulunabilir [Azure depolama Fiyatlandırma sayfasında](https://azure.microsoft.com/pricing/details/storage/blobs/). LRS için GRS değiştirirseniz, ek bir maliyet yoktur, ancak ikincil konumdan verileriniz silinir.

<a id="ragrsbenefits"></a>
#### <a name="4-how-can-ra-grs-help-me"></a>4. RA-GRS bana nasıl yardımcı?
   
   GRS depolama çoğaltmayı birincil sunucudan verileriniz birincil bölge çıktığınızda mil yüzlerce olan ikincil bir bölgeye sağlar. Böyle bir durumda, hatta tam bölgesel bir kesintinin veya bir olağanüstü durumda birincil bölge kurtarılabilir değil söz konusu olduğunda dayanıklı verilerdir. RA-GRS depolama bu içerir ve verileri ikincil konumdan okuma özelliği ekler. Bu özelliği kullanabilmeniz nasıl hakkında bazı fikir edinmek için lütfen [tasarlama yüksek oranda kullanılabilir RA-GRS depolama kullanan uygulamalar](storage-designing-ha-apps-with-ragrs.md). 

<a id="lastsynctime"></a>
#### <a name="5-is-there-a-way-for-me-to-figure-out-how-long-it-takes-to-replicate-my-data-from-the-primary-to-the-secondary-region"></a>5. Bana verilerimi birincil sunucudan ikincil bölge'ye çoğaltmak için gereken süreyi şekil için bir yolu var mı?
   
   RA-GRS depolama kullanıyorsanız, depolama hesabınıza son eşitleme zamanı kontrol edebilirsiniz. Son eşitleme saati GMT tarih/saat değeridir; Son eşitleme zamanı önce tüm birincil yazma ikincil konumdan okumak kullanılabilir olan hangi ortalama ikincil konumuna başarıyla yazılmamış. Son eşitleme süresi okumalar henüz kullanılabilir durumda olmayabilir veya sonra birincil yazar. Bu değeri kullanarak sorgulama yapabilirsiniz [Azure portal](https://portal.azure.com/), [Azure PowerShell](storage-powershell-guide-full.md), veya program aracılığıyla REST API veya depolama istemci kitaplıklarından birini kullanarak. 

<a id="outage"></a>
#### <a name="6-how-can-i-switch-to-the-secondary-region-if-there-is-an-outage-in-the-primary-region"></a>6. Birincil bölgede bir kesinti durumunda nasıl ikincil bölge'ye geçebilirsiniz?
   
   Lütfen makalesine başvurun [bir Azure Storage kesinti oluşursa yapmanız gerekenler](storage-disaster-recovery-guidance.md) daha fazla ayrıntı için.

<a id="rpo-rto"></a>
#### <a name="7-what-is-the-rpo-and-rto-with-grs"></a>7. RPO ve GRS ile RTO nedir?
   
   Kurtarma noktası hedefi (RPO): GRS ve RA-GRS depolama hizmeti zaman uyumsuz olarak coğrafi çoğaltır verilerini birincil ve ikincil konum. Önemli bir bölgesel olağanüstü durum yoktur ve bir yük devretme gerçekleştirilecek sahipse, coğrafi olarak çoğaltılmış edilmemiş son delta değişiklikler kaybolabilir. Kayıp olası veri dakika sayısı (yani noktası verilerin kurtarılabilmesini zamanında) RPO olarak adlandırılır. Genellikle bir RPO 15 dakikadan kısa sahibiz, olmasına rağmen şu anda hiçbir SLA ne kadar süreyle coğrafi çoğaltma üzerinde alır.

   Kurtarma süresi hedefi (RTO): Bu, yük devretme işlemi gerçekleştirin ve bir yük devretme yapmak varsa depolama hesabı çevrimiçine almak için bize süreyi bir ölçüsüdür. Yük devretme için zaman aşağıdakileri içerir:
    * Bize araştırmak ve biz birincil konumdaki verileri kurtarabilir veya gerekiyorsa belirlemek için gereken süreyi biz bir yük devretme yapmanız gerekir.
    * İkincil konumunu gösterecek şekilde yük devretme, birincil DNS girişlerini değiştirerek hesabı.

   Biz, veri kurtarma ihtimali varsa, biz yük devretme yapmayı bekletir ve birincil konumda veri kurtarma odaklanmak için verilerinizi çok ciddiye koruma sorumluluğunu alın. Gelecekte, ardından RTO kendiniz denetlemenize olanak tanır, bir hesap düzeyinde bir yük devretme tetiklemek izin vermek için bir API sağlayan planlıyoruz ancak bu henüz kullanılabilir değil.
   
## <a name="next-steps"></a>Sonraki adımlar
* [RA-GRS depolama kullanarak yüksek oranda kullanılabilir uygulamalar tasarlama](storage-designing-ha-apps-with-ragrs.md)
* [Azure Depolama fiyatlandırması](https://azure.microsoft.com/pricing/details/storage/)
* [Azure storage hesapları hakkında](storage-create-storage-account.md)
* [Azure Storage ölçeklenebilirlik ve performans hedefleri](storage-scalability-targets.md)
* [Microsoft Azure Depolama artıklık seçenekleri ve okuma erişimi coğrafi olarak yedekli depolama](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/11/introducing-read-access-geo-replicated-storage-ra-grs-for-windows-azure-storage.aspx)
* [SOSP belgesi - Azure Storage: Yüksek oranda kullanılabilir depolama sahip bulut hizmeti güçlü tutarlılık](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)

