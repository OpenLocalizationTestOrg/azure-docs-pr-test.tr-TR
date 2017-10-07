---
title: "Azure Storage aaaData çoğaltmasında | Microsoft Docs"
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
ms.openlocfilehash: ce48d1992fec7bd5ed32feb96b86bef88ca759df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-replication"></a>Azure Storage çoğaltma

Microsoft Azure depolama hesabı her zaman olduğu Hello verilerde tooensure dayanıklılık ve yüksek kullanılabilirlik çoğaltılan. Aynı veri merkezinde ya da çoğaltma seçeneğine bağlı olarak seçtiğiniz tooa ikinci veri merkezi, verilerinizi içinde ya da hello çoğaltma kopyalar. Çoğaltma, verilerinizi korur ve geçici donanım arızalarında hello olay, uygulama yukarı zamanında korur. Verilerinizi çoğaltılmış tooa ikinci veri merkezi ise, hello birincil konumda yıkıcı bir hatadan korunmaktadır.

Çoğaltma sağlar, depolama hesabınız hello karşıladığını [depolama için hizmet düzeyi sözleşmesi (SLA)](https://azure.microsoft.com/support/legal/sla/storage/) bile hello karşılaştığı hataların içinde. Bkz. Azure depolama hakkında bilgi için başlangıç SLA dayanıklılık ve kullanılabilirlik için güvence altına alır.

Bir depolama hesabı oluşturduğunuzda, çoğaltma seçenekleri aşağıdaki hello birini seçebilirsiniz:

* [Yerel olarak yedekli depolama (LRS)](#locally-redundant-storage)
* [Bölgesel olarak yedekli depolama (ZRS)](#zone-redundant-storage)
* [Coğrafi olarak yedekli depolama (GRS)](#geo-redundant-storage)
* [Okuma erişimli coğrafi olarak yedekli depolama (RA-GRS)](#read-access-geo-redundant-storage)

Bir depolama hesabı oluşturduğunuzda okuma erişimli coğrafi olarak yedekli depolama (RA-GRS) hello varsayılan seçenektir.

Aşağıdaki tablonun hello sonraki bölümlerinde daha ayrıntılı çoğaltma her türünü adres hello farklarını LRS, ZRS, GRS ve RA-GRS, hızlı bir genel bakış sağlar.

| Çoğaltma stratejisi | LRS | ZRS | GRS | RA-GRS |
|:--- |:--- |:--- |:--- |:--- |
| Veriler birden çok veri merkezi arasında çoğaltılır. |Hayır |Evet |Evet |Evet |
| Verileri bir ikincil konum yanı sıra hello birincil konumu okuyabilir. |Hayır |Hayır |Hayır |Evet |
| Ayrı düğümlerde tutulan veri kopyası sayısı. |3 |3 |6 |6 |

Bkz: [Azure Storage fiyatlandırması](https://azure.microsoft.com/pricing/details/storage/) hello farklı artıklık seçenekleri için fiyatlandırma bilgilerini için.

> [!NOTE]
> Premium depolama yalnızca yerel olarak yedekli depolama (LRS) destekler. Premium depolama hakkında daha fazla bilgi için bkz: [Premium Storage: Azure sanal makine iş yükleri için yüksek performanslı depolama](../storage-premium-storage.md).
>

## <a name="locally-redundant-storage"></a>Yerel olarak yedekli depolama
Yerel olarak yedekli depolama (LRS), depolama hesabınız oluşturuldu hello bölgede bir veri merkezinde barındırılır üç kez bir depolama ölçek birimi içindeki verilerinizi çoğaltır. Yalnızca yazılı tooall üç çoğaltmaları silindikten sonra Yazma isteği başarıyla döndürür. Bu üç çoğaltmaların her ayrı hata etki alanları ve bir depolama ölçek birimi içinde yükseltme etki alanları bulunur.

Bir depolama ölçek birimi depolama düğümleri raflarının koleksiyonudur. Hata etki alanı (FD) hata fiziksel bir birimi temsil eder ve toohello ait düğümleri olarak kabul edilebilir düğümleri oluşan bir gruptur aynı fiziksel raf. Bir yükseltme etki alanına (UD), hizmet yükseltmesi (sunum) hello işlemi sırasında birlikte yükseltilir düğümleri grubudur. Merhaba üç çoğaltmaları verileri tek bir rafa donanım arızası etkiler olsa bile veya düğümler piyasaya sürme sırasında yükseltildiğinde olduğundan bir depolama ölçek birimi tooensure içinde UDs ve FDs yayılır.

LRS hello en düşük maliyeti seçenek ve en az karşılaştırıldığında dayanıklılık tooother seçenekleri sunar. Bir veri merkezi düzeyi olağanüstü (vb. taşmasını yangın) Hello olayda tüm üç çoğaltmaları kayıp veya kurtarılamaz olabilir. Coğrafi olarak yedekli depolama (GRS) toomitigate Bu risk, çoğu uygulama için önerilir.

Yerel olarak yedekli depolama hala belirli senaryolarda istenebilir:

* En yüksek bant genişliği üst sınırı Azure Storage çoğaltma seçenekleri sağlar.
* Uygulamanızı kolayca canlandırılabilir veri depoluyorsa, LRS için tercih edebilirsiniz.
* Bazı uygulamalar, yalnızca bir ülke toodata idare gereksinimleri nedeniyle içinde kısıtlı tooreplicating verilerdir. Eşleştirilmiş bir bölge başka bir ülkede olabilir. Bölge çiftleri hakkında daha fazla bilgi için bkz: [Azure bölgeleri](https://azure.microsoft.com/regions/).

## <a name="zone-redundant-storage"></a>Bölge olarak yedekli depolama
Bölge olarak yedekli depolama (ZRS) verilerinizi böylece LRS'den daha fazla dayanıklılık sağlayan ek toostoring üç çoğaltmaları benzer tooLRS, bir veya iki bölgede içinde veri merkezleri arasında zaman uyumsuz olarak çoğaltır. Merhaba birincil veri merkezi kullanılamıyor veya kurtarılamaz olsa bile, ZRS içinde depolanan verileri dayanıklı.
Toouse ZRS planlama müşteriler kullanan:

* ZRS, yalnızca blok bloblar genel amaçlı depolama hesapları için kullanılabilir ve yalnızca depolama hizmeti sürümleri 2014-02-14 içinde ve üzerinde desteklenir.
* Zaman uyumsuz çoğaltma olduğu yerel bir olağanüstü durum hello olayı içinde bir gecikme gerektirdiğinden hello veri hello birincil kurtarılamazsa, henüz değişiklikleri toohello ikincil çoğaltılan olası kaybolur.
* Microsoft yük devretme toohello ikincil başlatana kadar hello çoğaltma kullanılamayabilir.
* ZRS hesapları sonraki tooLRS veya GRS dönüştürülemez. Benzer şekilde, varolan LRS veya GRS hesabı olamaz tooa ZRS hesabı dönüştürülür.
* ZRS hesapları, ölçümleri veya günlüğe kaydetme özelliğine sahip.

## <a name="geo-redundant-storage"></a>Coğrafi Olarak Yedekli Depolama
Coğrafi olarak yedekli depolama (GRS) hello birincil bölge çıktığınızda mil yüzlerce olduğundan, veri tooa ikincil bölge çoğaltır. Etkin GRS depolama hesabınız varsa, verilerinizi bile hello durumda tam bölgesel bir kesintinin veya hangi hello birincil bölge kurtarılamaz olağanüstü durum dayanıklı.

Etkin GRS ile bir depolama hesabı için bir güncelleştirme burada üç kez çoğaltılır ilk taahhüt toohello birincil bölge ' dir. Merhaba güncelleştirme zaman uyumsuz olarak kopyalandığı sonra toohello ikincil bölge, burada, ayrıca yinelendiğini üç kez.

GRS ile hem hello birincil ve ikincil bölgeler çoğaltmalar ayrı hata etki alanlarında yönetmek ve LRS ile açıklandığı gibi bir depolama ölçek birimi etki alanlarını yükseltme.

Dikkate alınacak noktalar:

* Zaman uyumsuz çoğaltma değil henüz çoğaltılmamış değişiklikleri mümkün olan bölgesel bir olağanüstü durum hello olayı içinde bir gecikme gerektirdiğinden hello veri hello birincil bölgesinden kurtarılamazsa, toohello ikincil bölge kaybolur.
* Microsoft yük devretme toohello ikincil bölge başlatır sürece hello çoğaltma kullanılamıyor. Microsoft bir yük devretme toohello ikincil bölge ' ı başlattığınızda, hello yük devretme tamamlandıktan sonra toothat verilerini okuma ve yazma erişimi gerekir. Daha fazla bilgi için lütfen bkz [olağanüstü durum kurtarma Kılavuzu](../storage-disaster-recovery-guidance.md). 
* Bir uygulama tooread hello ikincil bölgesinden isterse, hello kullanıcı RA-GRS etkinleştirmeniz gerekir.

Bir depolama hesabı oluşturduğunuzda, hello hello hesap için birincil bölge seçin. Merhaba ikincil bölge'hello birincil bölgeye göre belirlenir ve değiştirilemez. Aşağıdaki tablonun hello hello birincil ve ikincil bölge eşleştirmeleri gösterilir.

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
> ABD kamu Virginia ikincil BİZE kamu Texas bölgedir. Daha önce BİZE kamu Virginia BİZE kamu Iowa bir ikincil bölge ' kullanılan. Depolama hesapları bir ikincil bölge olması gibi hala BİZE kamu Iowa yararlanan bir ikincil bölge tooUS kamu Texas geçirildi. 
> 
> 

## <a name="read-access-geo-redundant-storage"></a>Coğrafi olarak yedekli depolamaya okuma erişimi
Okuma erişimli coğrafi olarak yedekli depolama (RA-GRS) salt okunur erişim toohello veri hello ikincil konumdaki Ayrıca iki bölgede toohello çoğaltma GRS tarafından sağlanan sağlayarak depolama hesabınız için kullanılabilirliği en üst düzeye çıkarır.

Salt okunur erişim tooyour hello ikincil bölge verilerde etkinleştirdiğinizde, verilerinizi ayrıca depolama hesabınız için toohello birincil uç noktası ikincil bir noktadaki kullanılabilir durumdadır. Merhaba ikincil uç benzer toohello birincil uç noktası, ancak hello sonek ekler `–secondary` toohello hesap adı. Örneğin, birincil uç noktası için Blob hizmeti hello ise `myaccount.blob.core.windows.net`, ikincil uç noktanız ise `myaccount-secondary.blob.core.windows.net`. Depolama hesabınız için erişim tuşları Hello olan hello aynı hem de birincil ve ikincil uç noktaları hello için.

Dikkate alınacak noktalar:

* Uygulamanız toomanage, RA-GRS kullanırken etkileşimde hangi uç noktaya sahip.
* Zaman uyumsuz çoğaltma değil henüz çoğaltılmamış değişiklikleri mümkün olan bölgesel bir olağanüstü durum hello olayı içinde bir gecikme gerektirdiğinden hello veri hello birincil bölgesinden kurtarılamazsa, toohello ikincil bölge kaybolur.
* Microsoft yük devretme toohello ikincil bölge başlatırsa hello yük devretme tamamlandıktan sonra toothat verilerini okuma ve yazma erişimi gerekir. Daha fazla bilgi için lütfen bkz [olağanüstü durum kurtarma Kılavuzu](../storage-disaster-recovery-guidance.md). 
* RA-GRS, yüksek kullanılabilirlik sağlamak için tasarlanmıştır. Ölçeklenebilirlik yönergeleri için lütfen hello inceleyin [performans denetim listesi](../storage-performance-checklist.md).

## <a name="frequently-asked-questions"></a>Sık sorulan sorular

<a id="howtochange"></a>
#### <a name="1-how-can-i-change-hello-geo-replication-type-of-my-storage-account"></a>1. Merhaba coğrafi çoğaltma depolama Hesabımı türünü nasıl değiştirebilir miyim?

   Merhaba coğrafi çoğaltma depolama hesabınız LRS, GRS, arasında türünü değiştirebilirsiniz ve RA-GRS kullanarak hello [Azure portal](https://portal.azure.com/), [Azure Powershell](storage-powershell-guide-full.md) veya program aracılığıyla birçok depolama istemci birini kullanarak Kitaplıkları. Lütfen ZRS hesapları dönüştürülen LRS veya GRS olamayacağını unutmayın. Benzer şekilde, varolan LRS veya GRS hesabı olamaz tooa ZRS hesabı dönüştürülür.

<a id="changedowntime"></a>
#### <a name="2-will-there-be-any-down-time-if-i-change-hello-replication-type-of-my-storage-account"></a>2. Depolama Hesabımı hello çoğaltma türünü değiştirirseniz var. herhangi kesinti olacak?

   Hayır, olmayacak herhangi kesinti.

<a id="changecost"></a>
#### <a name="3-will-there-be-any-additional-cost-if-i-change-hello-replication-type-of-my-storage-account"></a>3. Depolama Hesabımı hello çoğaltma türünü değiştirirseniz, ek bir maliyet var. olacak?

   Evet. LRS tooGRS (veya RA-GRS) depolama hesabınız için değiştirirseniz, birincil konumda toohello ikincil konumdan mevcut veri kopyalama söz konusu çıkışı için ek bir ücret doğurur. Merhaba ilk veri kopyalandıktan sonra da başka coğrafi hello birincil toosecondary konumdan hello veri çoğaltmak için ek çıkış ücret yoktur. bant genişliği ücretleri Hello ayrıntılarını hello üzerinde bulunabilir [Azure depolama Fiyatlandırma sayfasında](https://azure.microsoft.com/pricing/details/storage/blobs/). GRS tooLRS değiştirirseniz, ek bir maliyet yoktur, ancak verilerinizi hello ikincil konumdan silinir.

<a id="ragrsbenefits"></a>
#### <a name="4-how-can-ra-grs-help-me"></a>4. RA-GRS bana nasıl yardımcı?
   
   GRS depolama hello birincil bölge çıktığınızda mil yüzlerce olan bir birincil tooa ikincil bölge'verilerinizden çoğaltılmasını sağlar. Böyle bir durumda, hatta hello durumda tam bölgesel bir kesintinin veya hangi hello birincil bölge kurtarılamaz olağanüstü durum dayanıklı verilerdir. RA-GRS depolama bu içerir ve hello ikincil konumdan hello özelliği tooread hello veri ekler. Konusunda fikir edinmek için tooleverage bu özelliği, çok başvurun[tasarlama yüksek oranda kullanılabilir RA-GRS depolama kullanan uygulamalar](../storage-designing-ha-apps-with-ragrs.md). 

<a id="lastsynctime"></a>
#### <a name="5-is-there-a-way-for-me-toofigure-out-how-long-it-takes-tooreplicate-my-data-from-hello-primary-toohello-secondary-region"></a>5. Bir yol benim için tooreplicate verilerimi hello birincil toohello ikincil bölge ' süreyi çıkışı toofigure var?
   
   RA-GRS depolama kullanıyorsanız, hello depolama hesabınızın son eşitleme zamanı kontrol edebilirsiniz. Son eşitleme saati GMT tarih/saat değeridir; tüm birincil yazma hello son eşitleme zamanı önce başarıyla toohello ikincil konum kullanılabilir toobe hello ikincil konumdan okuma oldukları anlamına yazılmıştır. Birincil hello sonra son eşitleme süresi okumalar henüz kullanılabilir durumda olmayabilir veya yazar. Bu değeri hello kullanarak sorgulama yapabilirsiniz [Azure portal](https://portal.azure.com/), [Azure PowerShell](storage-powershell-guide-full.md), veya program aracılığıyla kullanarak hello REST API veya depolama istemcisi kitaplıklarını hello biri. 

<a id="outage"></a>
#### <a name="6-how-can-i-switch-toohello-secondary-region-if-there-is-an-outage-in-hello-primary-region"></a>6. Merhaba birincil bölgede bir kesinti durumunda nasıl toohello ikincil bölge geçebilirsiniz?
   
   Lütfen toohello makalesine başvurun [bir Azure Storage kesinti oluşursa hangi toodo](../storage-disaster-recovery-guidance.md) daha fazla ayrıntı için.

<a id="rpo-rto"></a>
#### <a name="7-what-is-hello-rpo-and-rto-with-grs"></a>7. Ne olduğunu hello RPO ve GRS ile RTO?
   
   Kurtarma noktası hedefi (RPO): GRS ve RA-GRS, hello depolama hizmeti zaman uyumsuz olarak çoğaltır coğrafi hello veri hello birincil toohello ikincil konumdan. Önemli bir bölgesel olağanüstü durum yoktur ve bir yük devretme gerçekleştirilen toobe varsa, coğrafi olarak çoğaltılmış edilmemiş son delta değişiklikler kaybolabilir. Merhaba süreyi dakika cinsinden kaybedilen olası veri başvurulan tooas hello (yani hello zaman toowhich veri noktasında kurtarılabilir) RPO ' dir. Genellikle bir RPO 15 dakikadan kısa sahibiz, olmasına rağmen şu anda hiçbir SLA ne kadar süreyle coğrafi çoğaltma üzerinde alır.

   Kurtarma süresi hedefi (RTO): Bir ölçü ne kadar süreyle bize toodo hello yük devretme alır ve biz toodo bir yük devretme varsa hello depolama hesabı çevrimiçi dönmek budur. Başlangıç saati toodo hello yük devretme hello aşağıdakileri içerir:
    * Bize tooinvestigate alır ve biz hello birincil konumda hello verileri kurtarabilir veya toodo bir yük devretme ihtiyacımız belirleyen hello süre.
    * Merhaba birincil DNS girişlerini toopoint toohello ikincil konum değiştirerek yük devretme hello hesabı.

   Biz, hello veri kurtarma ihtimali varsa, biz hello yük devretme yapmayı bekletir ve hello birincil konumda hello veri kurtarma odaklanmak için verilerinizi çok ciddiye koruma hello sorumluluk alır. Hello gelecekteki, biz tooprovide bir API tooallow planlama, tootrigger hesap düzeyinde bir yük devretme, hangi sonra izin, toocontrol hello RTO kendiniz, ancak bu henüz kullanılabilir değil.
   
## <a name="next-steps"></a>Sonraki adımlar
* [RA-GRS depolama kullanarak yüksek oranda kullanılabilir uygulamalar tasarlama](../storage-designing-ha-apps-with-ragrs.md)
* [Azure Depolama fiyatlandırması](https://azure.microsoft.com/pricing/details/storage/)
* [Azure storage hesapları hakkında](../storage-create-storage-account.md)
* [Azure Storage ölçeklenebilirlik ve performans hedefleri](storage-scalability-targets.md)
* [Microsoft Azure Depolama artıklık seçenekleri ve okuma erişimi coğrafi olarak yedekli depolama](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/11/introducing-read-access-geo-replicated-storage-ra-grs-for-windows-azure-storage.aspx)
* [SOSP belgesi - Azure Storage: Yüksek oranda kullanılabilir depolama sahip bulut hizmeti güçlü tutarlılık](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)

