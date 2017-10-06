---
title: "Azure Cosmos veritabanı aaaConsistency düzeyleri | Microsoft Docs"
description: "Azure Cosmos DB beş tutarlılık düzeyleri toohelp Bakiye nihai tutarlılık, kullanılabilirlik ve gecikme dengelemeler sahiptir."
keywords: "Nihai tutarlılık, azure cosmos db, azure, Microsoft azure"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: cgronlun
documentationcenter: 
ms.assetid: 3fe51cfa-a889-4a4a-b320-16bf871fe74c
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: mimig
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac399c229d0856cd811bc81568536e519af3300f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tunable-data-consistency-levels-in-azure-cosmos-db"></a>İnce ayarlanabilir veri tutarlılık düzeylerini Azure Cosmos veritabanı
Azure Cosmos DB her veri modeli için aklınızda genel dağıtım plan hello gelen tasarlanmıştır. Tasarlanmış toooffer tahmin edilebilir düşük gecikme süresi garantileri, % 99,99 kullanılabilirlik SLA olan ve birden çok iyi tanımlanmış tutarlılık modelleri rahat. Şu anda Azure Cosmos DB beş tutarlılık düzeyi sunar: güçlü, sınırlanmış eskime durumu, oturum, tutarlı öneki ve son. 

Yanında **güçlü** ve **nihai tutarlılık** modelleri Azure Cosmos DB üç daha fazla dikkatle kod oluşturulmuş ve kullanıma hazır hale getirilmiş tutarlılık modeli sunar ve sahip dağıtılmış veritabanı tarafından yaygın olarak sunulan gerçek dünya durumlara karşı oluştuğu doğrulandı. Merhaba bunlar **sınırlanmış eskime durumu**, **oturum**, ve **tutarlı önek** tutarlılık düzeyi. Topluca bu beş tutarlılık düzeyleri toomake iyi reasoned dengelemeler tutarlılık, kullanılabilirlik ve gecikme süresi arasında etkinleştirin. 

## <a name="distributed-databases-and-consistency"></a>Dağıtılmış veritabanları ve tutarlılık
Ticari olarak dağıtılmış veritabanları iki kategoriye ayrılır: iyi tanımlanmış, kanıtlanabilir tutarlılık seçenekleri sunmayan veritabanları ve iki olağan dışı programlama seçeneği (güçlü ve nihai tutarlılık) sunan veritabanları. 

eski yüklerini uygulama geliştiricileri kendi çoğaltma kurallarının minutia hello ve tutarlılık, kullanılabilirlik, gecikme ve verimlilik arasında toomake zor dengelemeden bekliyor. Merhaba ikinci bir baskısı toochoose hello iki uç nokta birini koyar. Rağmen Hello bol miktarda araştırma ve 50'den fazla tutarlılık modelleri için tekliflerini hello dağıtılmış veritabanı topluluk mümkün toocommercialize tutarlılık düzeyleri güçlü ve nihai tutarlılık dışında yedeklenmedi. Cosmos DB sağlayan geliştiriciler toochoose hello tutarlılık spektrumun – güçlü, boyunca beş iyi tanımlanmış tutarlılık modelleri arasında sınırlanmış eskime durumu, [oturum](http://dl.acm.org/citation.cfm?id=383631), tutarlı öneki ve son. 

![Azure Cosmos DB birden çok sunar (gevşek) tutarlılık modelleri toochoose gelen iyi tanımlanmış](./media/consistency-levels/five-consistency-levels.png)

Aşağıdaki tablonun hello hello belirli garanti her tutarlılık düzeyi sunar gösterilmektedir.
 
**Tutarlılık Düzeyleri ve garantiler**

| Tutarlılık Düzeyi | Garantiler |
| --- | --- |
| Güçlü | Doğrusallaştırma |
| Sınırlanmış Eskime Durumu | Tutarlı Ön Ek. -k ön eklerine veya t aralığına göre yazma işlemlerinin arkasındaki gecikmeyi okur |
| Oturum   | Tutarlı Ön Ek. Monoton okuma, monoton yazma, yazdıklarınızı okuma, okuduktan sonra yazma |
| Tutarlı Ön Ek | Hiçbir boşluk içeren tüm hello güncelleştirmelerini bazı öneki güncelleştirmeler döndürdü. |
| Nihai  | Bozuk okumalar |

Merhaba varsayılan tutarlılık düzeyi Cosmos DB hesabınızdaki yapılandırabilir (ve daha sonra hello tutarlılığı belirli Okuma isteği için geçersiz kılar). Dahili olarak, hello varsayılan tutarlılık düzeyi toodata bölgeleri kapsayabilir hello bölüm kümeleri içinde geçerlidir. Sınırlanmış eskime durumu % 20 tercih ve oturum tutarlılığı yaklaşık bizim kiracılar %73 kullanın. Yaklaşık %3 müşterilerimizin çeşitli tutarlılık düzeylerini başlangıçta kendi uygulama için belirli tutarlılık seçim şekilde önce deneme inceleyin. Ayrıca bizim kiracılar % 2'yalnızca bir istek başına tutarlılık düzeylerini geçersiz kılma inceleyin. 

Cosmos DB nihai tutarlılık güçlü veya sınırlanmış eskime durumu tutarlılığı ile okuma olarak ucuz iki kez ve okuma oturumunda, tutarlı önek sunulamıyor. Cosmos DB endüstri lideri tutarlılığı garanti birlikte kullanılabilirliği, performansı ve gecikme süresi dahil olmak üzere kapsamlı % 99,99 SLA sahiptir. Kullanıyoruz bir [linearizability denetleyicisi](http://dl.acm.org/citation.cfm?id=1806634), sürekli olarak bizim hizmet telemetri çalışır ve açık yayımlanmaması herhangi tutarlılık ihlalleri tooyou bildirir. İçin eskime durumu, biz İzleyici ve rapor herhangi bir ihlali sürdü ve t sınırları ilişkisindeki. Tüm beş gevşek tutarlılık düzeyleri için biz de hello rapor [probabilistic sınırlanmış eskime durumu ölçüm](http://dl.acm.org/citation.cfm?id=2212359) doğrudan tooyou.  

## <a name="scope-of-consistency"></a>Tutarlılık kapsamı
Tutarlılık Hello kesinliği kapsamlı tooa tek kullanıcı isteğidir. Yazma isteği tooan ekleme, değiştirme, upsert karşılık gelen veya işlem silin. Yazma gibi ile bir okuma/sorgu de kapsamlı tooa tek kullanıcı isteği bir işlemdir. Merhaba kullanıcı gerekli toopaginate büyük olabilir sonuç kümesi, birden çok bölüm kapsayıcı, ancak her işlem kapsamlı tooa tek sayfa ve gelen tek bir bölüm içinde sunulan okuyun.

## <a name="consistency-levels"></a>Tutarlılık düzeyleri
Cosmos DB hesabınızın altında veritabanı hesabınızdaki tooall koleksiyonları (ve veritabanları) için geçerlidir, varsayılan tutarlılık düzeyi yapılandırabilirsiniz. Varsayılan olarak, tüm okuma ve hello karşı verilen sorgular tarafından kullanıcı tanımlı kaynakları hello veritabanı hesabında belirtilen hello varsayılan tutarlılık düzeyi kullanın. Belirli bir okuma/sorgu hello tutarlılık düzeyi hafifletin her hello kullanarak desteklenen API isteği. Bu bölümde açıklandığı gibi belirli tutarlılık ve performans arasında NET bir denge sağlamak hello Azure Cosmos DB çoğaltma protokolü tarafından desteklenen tutarlılık düzeylerini beş türü vardır.

**Güçlü**: 

* Güçlü tutarlılık sunan bir [linearizability](https://aphyr.com/posts/313-strong-consistency-models) garantisi hello ile garantili tooreturn hello en son sürümünü öğeyi okur. 
* Güçlü tutarlılık işlemi tarafından çoğaltmalarının hello çoğunluğu çekirdek yürütüldükten sonra yazma yalnızca görünür olmasını sağlar. Bir yazma ya da zaman uyumlu olarak işlemi hello birincil ve ikincil kopya hello çekirdek tarafından kararlıdır veya iptal edilir. Okuma her zaman çekirdek okuma hello çoğunluğu tarafından onaylanan, bir istemci her zaman tooread hello en son alınan yazma garanti ve kaydedilmemiş ya da kısmi bir yazma hiçbir zaman görebilirsiniz. 
* Yapılandırılmış toouse güçlü tutarlılık azure Cosmos DB hesapları birden fazla Azure bölgesine Azure Cosmos DB hesaplarıyla ilişkilendiremezsiniz. 
* Merhaba okuma işlemi maliyetini (cinsinden [istek birimleri](request-units.md) tüketilen) ile güçlü tutarlılık oturum daha yüksek ve nihai, ancak aynı sınırlanmış eskime durumu hello.

**Sınırlanmış eskime durumu**: 

* Sınırlanmış eskime durumu tutarlılığı garanti hello okuma yazma tarafından arkasında en fazla geri kalabilir olduğunu *K* sürümleri veya bir öğenin önekleri veya *t* zaman aralığı. 
* Sınırlanmış eskime durumu seçme gerektiğinde, bu nedenle, "eskime durumu" Merhaba iki şekilde yapılandırılabilir: sürümleri sayısı *K* olarak hello okuma öteleme hello yazma ve hello zaman aralığı arkasındaki hello öğesinin *t* 
* Sınırlanmış eskime durumu teklifleri toplam genel dışında içinde sırada hello "eskime durumu penceresi." garanti mevcut bir bölge içinde ve dışında hello "eskime durumu penceresi." Merhaba monoton okuma 
* Sınırlanmış eskime durumu oturumu veya nihai tutarlılık daha güçlü bir tutarlılık garanti sağlar. Genel olarak dağıtılmış uygulamalar için burada, toohave güçlü tutarlılık gibi ancak % 99,99 kullanılabilirlik ve düşük gecikme süresi de istediğiniz senaryolar için sınırlanmış eskime durumu kullanmanızı öneririz. 
* Sınırlanmış eskime durumu tutarlılığı ile yapılandırılmış olan azure Cosmos DB hesapları Azure bölgeleri herhangi bir sayıda Azure Cosmos DB hesaplarıyla ilişkilendirebilirsiniz. 
* ile bir okuma işlemi (RUs tüketilen) bakımından maliyetini Hello sınırlanmış eskime durumu oturum ve nihai tutarlılık maliyetinden daha yüksek, ancak aynı güçlü tutarlılık hello.

**Oturum**: 

* Güçlü ve sınırlanmış eskime durumu tutarlılığı düzeyleri tarafından sunulan hello genel tutarlılık modelleri oturum tutarlılığı kapsamlı tooa istemci oturumdur. 
* Oturum tutarlılığı monoton okuma, monoton yazma ve okuma kendi yazma (RYW) garanti garanti bu yana bir aygıt veya kullanıcı oturumu burada dahil tüm senaryoları için idealdir. 
* Oturum tutarlılığı, oturum açmak için tahmin edilebilir tutarlılık sağlar ve hello en düşük gecikme süreli yazma işlemleri ve okuma sunarken verimlilik maksimum okuyun. 
* Oturum tutarlılığı ile yapılandırılmış olan azure Cosmos DB hesapları Azure bölgeleri herhangi bir sayıda Azure Cosmos DB hesaplarıyla ilişkilendirebilirsiniz. 
* okuma işlemi (RUs tüketilen) bakımından maliyetini tutarlılık düzeyi güçlü ve sınırlanmış eskime durumu değerinden ancak birden fazla nihai tutarlılık oturum ile Merhaba

<a id="consistent-prefix"></a>
**Tutarlı önek**: 

* Tutarlı önek daha fazla yazma olmaması durumunda hello Grup içerisinde hello çoğaltmalar sonunda yakınsamasını garanti eder. 
* Tutarlı önek okuma hiçbir zaman bozuk yazma bkz güvence altına alır. Yazma hello sırayla gerçekleştirilen varsa `A, B, C`, bir istemci ya da görür sonra `A`, `A,B`, veya `A,B,C`, ancak hiçbir zaman bozuk gibi `A,C` veya `B,A,C`.
* Tutarlı önek tutarlılık ile yapılandırılmış olan azure Cosmos DB hesapları Azure bölgeleri herhangi bir sayıda Azure Cosmos DB hesaplarıyla ilişkilendirebilirsiniz. 

**Son**: 

* Nihai tutarlılık, daha fazla yazma olmaması durumunda hello Grup içerisinde hello çoğaltmalar sonunda yakınsamasını garanti eder. 
* Nihai tutarlılık hello zayıf tutarlılık istemci önce gördü hello olanları daha eski olan hello değerleri nereden biçimidir.
* Nihai tutarlılık hello zayıf okuma tutarlılığı ancak hem okuma hem de yazma işlemleri için en düşük gecikme süresine teklifleri hello sağlar.
* Nihai tutarlılık ile yapılandırılmış olan azure Cosmos DB hesapları Azure bölgeleri herhangi bir sayıda Azure Cosmos DB hesaplarıyla ilişkilendirebilirsiniz. 
* Merhaba okuma işlemi (RUs tüketilen) bakımından maliyetini hello nihai tutarlılık hello tüm hello Azure Cosmos DB tutarlılık düzeylerini en düşük düzeydir.

## <a name="configuring-hello-default-consistency-level"></a>Merhaba varsayılan tutarlılık düzeyi yapılandırılıyor
1. Merhaba, [Azure portal](https://portal.azure.com/), buna atlama çubuğu Merhaba, tıklatın **Azure Cosmos DB**.
2. Merhaba, **Azure Cosmos DB** dikey penceresinde, select hello veritabanı hesabı toomodify.
3. Merhaba hesabı dikey penceresinde tıklayın **varsayılan tutarlılık**.
4. Merhaba, **varsayılan tutarlılık** dikey penceresinde, select hello yeni tutarlılık düzeyi ve tıklatın **kaydetmek**.
   
    ![Merhaba ayarlar simgesine ve varsayılan tutarlılık giriş vurgulama ekran görüntüsü](./media/consistency-levels/database-consistency-level-1.png)

## <a name="consistency-levels-for-queries"></a>Sorgular için tutarlılık düzeyleri
Varsayılan olarak, kullanıcı tanımlı, kaynaklar için hello tutarlılık düzeyi sorgular için hello aynı gibi hello tutarlılık düzeyi okur. Varsayılan olarak, her ekleme, değiştirme veya silme öğesi toohello Cosmos DB kapsayıcısının hello dizini zaman uyumlu olarak güncelleştirilir. Toohonor hello aynı tutarlılık düzeyi şekilde hello sorguları noktası okuma bu etkinleştirir. Azure Cosmos DB yazma en iyi duruma getirilmiş ve yazma, zaman uyumlu dizin Bakım ve tutarlı sorguları hizmet veren sürekli birimleri destekler, ancak belirli koleksiyonlar tooupdate kendi dizini gevşek yapılandırabilirsiniz. Yavaş dizin daha hello yazma performansı artırır ve öncelikle okuma ağır bir iş yükü olduğunda toplu alım senaryoları için idealdir.  

| Dizin oluşturma modu | Okur | Sorgular |
| --- | --- | --- |
| CONSISTENT (varsayılan) |Güçlü, sınırlanmış eskime durumu, oturum, tutarlı önek arasından seçin ya da son |Güçlü, sınırlanmış eskime durumu, seçim oturumu veya son |
| Geç |Güçlü, sınırlanmış eskime durumu, oturum, tutarlı önek arasından seçin ya da son |Nihai |
| None |Güçlü, sınırlanmış eskime durumu, oturum, tutarlı önek arasından seçin ya da son |Uygulanamaz |

Olarak okuma istekleriyle her API belirli sorgu istekte hello tutarlılık düzeyi düşürün.

## <a name="next-steps"></a>Sonraki adımlar
Toodo tutarlılık düzeyleri ve bileşim hakkında daha fazla okunurken istiyorsanız kaynakları aşağıdaki hello öneririz:

* Doug Terry. Çoğaltılan verilerin tutarlılık Beyzbol (video) açıklanmıştır.   
  [https://www.YouTube.com/Watch?v=gluIh8zd26I](https://www.youtube.com/watch?v=gluIh8zd26I)
* Doug Terry. Çoğaltılan verilerin tutarlılık Beyzbol açıklanmıştır.   
  [http://Research.microsoft.com/pubs/157411/ConsistencyAndBaseballReport.PDF](http://research.microsoft.com/pubs/157411/ConsistencyAndBaseballReport.pdf)
* Doug Terry. Oturum garanti zayıf tutarlı çoğaltılan veriler için.   
  [http://DL.ACM.org/citation.cfm?id=383631](http://dl.acm.org/citation.cfm?id=383631)
* Daniel Abadi. Modern dağıtılmış veritabanı sistemleri tasarım tutarlılık bileşim: CAP hello Öykü yalnızca bir parçası olan ".   
  [http://computer.org/CSDL/mags/co/2012/02/mco2012020037-Abs.HTML](http://computer.org/csdl/mags/co/2012/02/mco2012020037-abs.html)
* Peter Bailis, Shivaram Venkataraman, Michael J. Franklin, Joseph M. Hellerstein, nleri Stoica. İçin pratik kısmi çekirdekleri sınırlanmış eskime durumu (PBS) probabilistic.   
  [http://vldb.org/pvldb/vol5/p776_peterbailis_vldb2012.PDF](http://vldb.org/pvldb/vol5/p776_peterbailis_vldb2012.pdf)
* Werner Vogels. Son tutarlı - tekrar ziyaret.    
  [http://allthingsdistributed.com/2008/12/eventually_consistent.HTML](http://allthingsdistributed.com/2008/12/eventually_consistent.html)
* Moni Naor, Avishai Wool, hello yük, kapasite ve kullanılabilirlik, çekirdek sistemleri, bilgi işlem, v.27 n.2, p.423 447, Nisan 1998 SIAM günlük.
  [http://epubs.siam.org/doi/Abs/10.1137/S0097539795281232](http://epubs.siam.org/doi/abs/10.1137/S0097539795281232)
* Sebastian Burckhardt, Chris Dern, Macanal Musuvathi, Roy Tan, Line-up: bir tam ve otomatik linearizability denetleyicisi, dil tasarım ve uygulama, Haziran 05-10, 2010, Toronto, Ontario programlama hello 2010 ACM SIGPLAN konferans bildirileri, Kanada [DOI > 10.1145/1806596.1806634] [http://dl.acm.org/citation.cfm?id=1806634](http://dl.acm.org/citation.cfm?id=1806634)
* Peter Bailis, Shivaram Venkataraman, Michael J. Franklin, Joseph M. Hellerstein nleri Stoica Probabilistically eskime durumu pratik kısmi çekirdeklerine, hello VLDB Endowment, v.5 n.8, p.776 787, Nisan 2012 bildirileri için sınırlı [http:// DL.ACM.org/citation.cfm?id=2212359](http://dl.acm.org/citation.cfm?id=2212359)
