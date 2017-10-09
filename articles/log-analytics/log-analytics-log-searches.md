---
title: "Azure günlük analizi günlük aramalarda aaaFind verilerle | Microsoft Docs"
description: "Günlük arar ve ortamınızda birden fazla kaynaktan herhangi bir makine verilerin bağıntısını toocombine izin verin."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: 0d7b6712-1722-423b-a60f-05389cde3625
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: bwren
ms.openlocfilehash: 1161857a0027f05726492417362cb24a8fe21ef8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="find-data-using-log-searches-in-log-analytics"></a>Günlük analizi günlük aramaları kullanarak veri bulma

>[!NOTE]
> Bu makalede günlük analizi hello geçerli sorgu dili kullanarak günlük arar.  Çalışma alanınızı yükseltilmiş toohello yüklediyse [yeni günlük analizi sorgu dili](log-analytics-log-search-upgrade.md), çok başvurmalıdır sonra[anlama günlük arar (yeni) günlük analizi](log-analytics-log-search-new.md).


Günlük analizi Hello özünde toocombine sağlayan hello günlük arama özelliktir ve ortamınızda birden fazla kaynaktan herhangi bir makine verilerin bağıntısını. Çözüm Ayrıca, ölçümleri belirli sorunu etrafına özetlenebilir günlük arama toobring güç sağlar.

Merhaba arama sayfası, bir sorgu oluşturabilirsiniz ve arama yaptığınızda sonra hello sonuçları modeli denetimlerini kullanarak filtre uygulayabilirsiniz. Gelişmiş sorgular tootransform, filtre ve rapor sonuçlarınıza oluşturabilirsiniz.

Ortak günlük arama sorguları çoğu çözüm sayfalarında görüntülenir. Hello OMS konsol döşeme tıklatın ya da günlük arama kullanarak tooother öğelerde hello öğenin tooview ayrıntılarını incelemek.

Bu öğreticide, biz günlük arama kullandığınızda örnekler toocover tüm hello temelleri gösterilecektir.

Biz basit, pratik örnekler başlatın ve böylece nasıl hello verilerden istediğinizi toouse hello sözdizimi tooextract hello Öngörüler hakkında pratik kullanım örnekleri bir anlayış alabilir üzerlerinde yapı.

Arama teknikleri alışık olduğunuz sonra hello gözden geçirebilirsiniz [günlük analizi oturum Arama başvurusu](log-analytics-search-reference.md).

## <a name="use-basic-filters"></a>Temel filtreleri kullanın
Merhaba ilk şey tooknow bu hello ilk önce herhangi bir arama sorgusu parçasıdır "|" dikey çizgi karakteri olan her zaman bir *filtre*. Bunu bir WHERE yan tümcesinde TSQL--olarak bunu belirler düşünün *ne* hello OMS veri deposundaki verileri toopull kısmı. Merhaba veri deposunda arama büyük ölçüde sorguda WHERE yan tümcesi hello ile başladığını doğal şekilde tooextract, istediğiniz hello veri hello özelliklerini belirtme hakkında olur.

Merhaba kullanabileceğiniz en temel filtreleri şunlardır *anahtar sözcükleri*'error' veya 'zaman aşımı' veya bir bilgisayar adı gibi. Bu basit sorgu türleri genellikle farklı şekiller dönüş aynı sonuç kümesi hello içindeki verilerin. Bu günlük analizi farklı sahip olmasından *türleri* hello sistem veri.

### <a name="tooconduct-a-simple-search"></a>tooconduct basit arama
1. Merhaba OMS portalında tıklatın **günlük arama**.  
    ![Ara kutucuğu](./media/log-analytics-log-searches/oms-overview-log-search.png)
2. Merhaba sorgu alanına yazın `error` ve ardından **arama**.  
    ![Arama hatası](./media/log-analytics-log-searches/oms-search-error.png)  
    Örneğin, hello sorgu için `error` hello aşağıdaki görüntüde 100.000 döndürülen **olay** (günlük yönetimi tarafından toplanan), kayıt 18 **ConfigurationAlert** (yapılandırma tarafından oluşturulan kayıtları Değerlendirme) ile 12 **ConfigurationChange** (Merhaba tarafından değişiklik izleme yakalanan) kaydeder.   
    ![Arama sonuçları](./media/log-analytics-log-searches/oms-search-results01.png)  

Bu filtreler gerçekten nesne türleri/sınıfları değildir. *Tür* yalnızca bir etiket ya da bir özellik ya da veri tooa parçası bir dize/ad/olan kategoriye ekli. Merhaba sistem bazı belgelerde olarak etiketlenir **türü: ConfigurationAlert** ve bazı olarak etiketlenir **türü: Perf**, veya **türü: olay**ve benzeri. Her bir arama sonucu, belge, kaydı veya giriş tüm hello Ham Özellikler ve değerlerinin her veri bu parçalarını görüntüler ve tooretrieve yalnızca hello kayıtlar istediğinizde, bu alan adları toospecify hello filtrede hello alan verilen bulunduğu kullanabilirsiniz değer.

*Tür* aslında tüm kayıtlar varsa, bir alan olup, diğer herhangi bir alandan farklı değildir. Bu işlem, başlangıç türü alanının hello değere göre kuruldu. Bu kayıt, farklı bir şekil veya form sahip olur. Arada **türü Perf =**, veya **türü olay =** de performans verisi veya olayları için toolearn tooquery gereksinim hello sözdizimi aşağıdaki gibidir.

Merhaba alan adı sonra ve hello değeri önce iki nokta üst üste (:) veya bir eşittir işareti (=) kullanabilirsiniz. **Olay türü:** ve **türü olay =** anlamı, seçebileceğiniz eşdeğerdir hello tercih ettiğiniz stili.

Bu nedenle, hello çalışamazsa Perf = kayıtları 'CounterName' adlı bir alana sahip sonra benzeyen bir sorgu yazabilirsiniz `Type=Perf CounterName="% Processor Time"`.

Bu size yalnızca hello performans verilerini hello performans sayacı adı "% işlemci zamanı" olduğu sunar.

### <a name="toosearch-for-processor-time-performance-data"></a>işlemci zamanı performans verileri için toosearch
* Merhaba arama sorgusu alanına yazın`Type=Perf CounterName="% Processor Time"`

Ayrıca daha belirli ve kullanabilirsiniz **InstanceName = _ 'Toplam'** hello sorguda olduğu bir Windows performans sayacı. Bir model ve başka de seçebilirsiniz **alan: değer**. Merhaba filtre, hello sorgu çubuğunda tooyour filtre otomatik olarak eklenir. Bu görüntü aşağıdaki hello görebilirsiniz. Size gösterir nerede tooclick tooadd **InstanceName: '_Total'** herhangi bir şey yazarak olmadan toohello sorgu.

![Arama modeli](./media/log-analytics-log-searches/oms-search-facet.png)

Sorgunuz artık hale gelir`Type=Perf CounterName="% Processor Time" InstanceName="_Total"`

Bu örnekte, toospecify yok **türü Perf =** tooget toothis sonucu. CounterName ve InstanceName Hello alanları türündeki kayıtlar için yalnızca olduğundan Perf, hello sorgu = yeterince spesifik tooreturn hello aynı sonuçları uzun, önceki bir hello aynıdır:

```
CounterName="% Processor Time" InstanceName="_Total"
```

Merhaba sorgudaki tüm hello filtreleri olarak değerlendirilir olmasıdır *ve* birbirleriyle. Etkili bir şekilde hello toohello ölçüt eklemek daha fazla alan daha az size daha belirli ve Gelişmiş sonuçları.

Örneğin, hello sorgu `Type=Event EventLog="Windows PowerShell"` çok aynıdır`Type=Event AND EventLog="Windows PowerShell"`. Oturum açmış ve hello Windows PowerShell olay günlüğünden toplanan tüm olayları döndürür. Birden çok kez art arda aynı modeli, ardından hello sorunu hello arama çubuğunu dağıtmayı, ancak hello örtük AND işleci her zaman olduğu için bunu hala aynı sonuçları hello döner tamamen yüzeysel--hello seçerek bir filtre eklerseniz.

Merhaba örtük AND işleci açıkça değil işlecini kullanarak kolayca ters çevirebilirsiniz. Örneğin:

`Type:Event NOT(EventLog:"Windows PowerShell")`ya da eşdeğer `Type=Event EventLog!="Windows PowerShell"` hello Windows PowerShell günlük olmayan tüm diğer günlüklerinden tüm olayları döndürür.

Ya da diğer Boole işleci gibi kullanabilir 'Veya'. Merhaba aşağıdaki döndürür kayıtları için hangi hello ya da uygulama veya sistem olay günlüğüne olan sorgu.

```
EventLog=Application OR EventLog=System
```

Sorgu yukarıda Hello kullanarak için her iki günlük girişlerini alırsınız hello aynı sonuç kümesi.

Merhaba veya bırakarak hello örtük ve yerinde kaldırırsanız, tooBOTH günlükleri ait bir olay günlüğü girişi olmadığından Bununla birlikte, ardından hello aşağıdaki sorguyu herhangi bir sonuç oluşturmaz. Her olay günlüğü girişi tooonly hello iki günlükleri birini yazıldı.

```
EventLog=Application EventLog=System
```


## <a name="use-additional-filters"></a>Ek filtreleri kullanın
Merhaba aşağıdaki sorguyu veri gönderdiğiniz tüm hello bilgisayarlar için 2 olay günlüğü girişleri döndürür.

```
EventLog=Application OR EventLog=System
```

![arama sonuçları](./media/log-analytics-log-searches/oms-search-results03.png)

Merhaba alanları veya filtreleri birini seçerek, diğer tüm olanlar hariç hello sorgu tooa belirli bilgisayar, daraltın. Merhaba sonuçta elde edilen sorgu hello aşağıdaki benzeyecektir.

```
EventLog=Application OR EventLog=System Computer=SERVER1.contoso.com
```

Merhaba nedeniyle eşdeğer toohello aşağıdaki olduğu örtük and

```
EventLog=Application OR EventLog=System AND Computer=SERVER1.contoso.com
```

Her sorgu açık sırasının hello değerlendirilir. Not hello parantez.

```
(EventLog=Application OR EventLog=System) AND Computer=SERVER1.contoso.com
```

Merhaba olay günlüğü alanı gibi yalnızca, ekleyerek yalnızca belirli bir bilgisayarlar kümesi için verileri alabilir veya. Örneğin:

```
(EventLog=Application OR EventLog=System) AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com OR Computer=SERVER3.contoso.com)
```

Benzer şekilde, bu sorgu return aşağıdaki hello **% CPU süresi** hello seçilen iki bilgisayar için.

```
CounterName="% Processor Time"  AND InstanceName="_Total" AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com)
```

### <a name="field-types"></a>Alan türleri
Filtre oluştururken, farklı türde günlük aramaları tarafından döndürülen alanları ile çalışma hello farklar anlamanız gerekir.

**Aranabilir alanlara** mavi arama sonuçlarında göster.  Aranabilir alanları arama koşulları belirli toohello alanı hello aşağıdaki gibi kullanabilirsiniz:

```
Type: Event EventLevelName: "Error"
Type: SecurityEvent Computer:Contains("contoso.com")
Type: Event EventLevelName IN {"Error","Warning"}
```

**Serbest metin aranabilir alanları** arama sonuçlarında gri gösterilir.  Arama koşulları belirli toohello alanı aranabilir alanları gibi ile kullanılamaz.  Yalnızca bir sorgu hello aşağıdaki gibi tüm alanlar boyunca gerçekleştirirken aranır.

```
"Error"
Type: Event "Exception"
```


### <a name="boolean-operators"></a>Boole işleçleri
DateTime ve sayısal alanlar ile kullanarak değerleri için arama yapabilirsiniz *büyük*, *küçük daha*, ve *küçük veya eşit*. Basit işleçleri gibi kullanabilir >, <>, =, < =,! hello sorgu arama çubuğunda =.

Belirli bir süre için belirli bir olay günlüğü sorgulayabilirsiniz. Örneğin, hello son 24 saat anımsatıcı ifade aşağıdaki hello ile ifade edilir.

```
EventLog=System TimeGenerated>NOW-24HOURS
```


#### <a name="toosearch-using-a-boolean-operator"></a>Boole işleci kullanılarak toosearch
* Merhaba arama sorgusu alanına yazın`EventLog=System TimeGenerated>NOW-24HOURS`  
    ![Boole değeri ile arama](./media/log-analytics-log-searches/oms-search-boolean.png)

Kontrol edebilirsiniz, ancak zaman aralığı grafik hello ve çoğu kez hello sorgu doğrudan zaman filtresi avantajları tooincluding vardır, toodo isteyebilirsiniz. Örneğin, bu harika burada kılabilirsiniz hello bağımsız olarak her bölme için hello süresi panolarla çalışır *genel* hello panosu sayfasında Saat Seçici. Daha fazla bilgi için bkz: [zaman önemlidir panosunda](http://cloudadministrator.wordpress.com/2014/10/19/system-center-advisor-restarted-time-matters-in-dashboard-part-6/).

Zamanına göre filtreleme, Merhaba sonuçlar elde göz önünde bulundurmanız *kesişim* Merhaba iki dönemler: hello OMS portalında (S1) belirtilen birinin hello ve biri (S2) hello sorguda belirtilen hello.

![kesişim](./media/log-analytics-log-searches/oms-search-intersection.png)

Merhaba dönemleri, örneğin burada seçtiğiniz hello OMS portalında kesiştiği yok, bu, gelir **bu hafta** ve burada tanımladığınız hello sorgusunda **geçen hafta**, olmaz ve ardından hiçbir kesişim yoktur herhangi bir sonuç alırsınız.

Karşılaştırma işleçleri Hello TimeGenerated alanı için kullanılan aynı zamanda diğer durumlarda faydalıdır. Örneğin, sayısal alanlar ile.

Örneğin, yapılandırma değerlendirmesi'nin uyarılar önem derecesi değerlerini aşağıdaki hello sahip verilen:

* 0 bilgi =
* 1 uyarı =
* 2 kritik =

Uyarı ve kritik uyarılar için sorgu ve de sorgu aşağıdaki hello bilgilendirme raporlarla hariç:

```
Type=ConfigurationAlert  Severity>=1
```


Aralık belirtilen sorguların de kullanabilirsiniz. Bu değer sırayla hello başlangıcını ve bitişini aralığı sağlayabilir anlamına gelir. Örneğin, hello burada hello Operations Manager olay günlüğündeki olaylar istiyorsanız EventID büyük veya ona eşit too2100 ancak değerden daha fazla 2199, sorgu aşağıdaki hello bunları döndürecektir sonra.

```
Type=Event EventLog="Operations Manager" EventID:[2100..2199]
```


> [!NOTE]
> kullanmalısınız hello aralığı sözdizimi şöyledir hello iki nokta üst üste (:) alan: değer ayırıcı ve *değil* hello eşittir (=). Merhaba alt ve üst uç hello aralığının köşeli parantez içine almanız ve bunları iki nokta (.) ile ayırın.
>
>

## <a name="manipulate-search-results"></a>Arama sonuçları işlemek
Verileri için arama yapıyorsanız, arama sorgunuzu toorefine istediğiniz ve hello sonuçlar üzerinde denetim iyi düzeyine sahip. Sonuçları alınırken, komutları tootransform uygulayabilirsiniz bunları.

Günlük analizi aramaları komutlarda *gerekir* hello dikey çizgi karakteri (|) sonra izleyin. Bir filtre her zaman bir sorgu dizesi hello ilk bölümü olması gerekir. Merhaba veri kümesi üzerinde çalıştığınız tanımlar ve ardından "Bu sonuçların bir komuta geçirir". Ardından, hello kanal tooadd ek komutlarını kullanabilirsiniz. Gevşek benzer toohello Windows PowerShell komut zincirini budur.

Genel olarak, hello günlük analizi arama dili toofollow PowerShell stili ve yönergeleri toomake çalışır BT benzer toohello BT uzmanları ve tooease hello öğrenme eğrisi.

Ne yaptıklarını kolayca anlayabilirsiniz şekilde komutları fiiller adlara sahip.  

### <a name="sort"></a>Sırala
Merhaba sıralama komutu, bir veya birden çok alanlara göre sıralama toodefine hello sağlar. Varsayılan olarak kullanmayın olsa bile, azalan bir zorunlu kılınır. Merhaba en son sonuçları her zaman arama sonuçları hello üstünde olur. Bunun anlamı ile bir aramayı çalıştırırken `Type=Event EventID=1234` ne gerçekten sizin için yürütülen olan:

```
Type=Event EventID=1234 **| Sort TimeGenerated desc**
```

Günlüklerde bilginiz deneyimi hello türü olmasıdır. Örneğin, Windows Olay Görüntüleyicisi'ni hello.

Sıralama toochange hello şekilde sonuçların döndürülmesini kullanabilirsiniz. Merhaba aşağıdaki örneklerde bunun nasıl çalıştığı gösterilmektedir.

```
Type=Event EventID=1234 | Sort TimeGenerated asc
```

```
Type=Event EventID=1234 | Sort Computer asc
```

```
Type=Event EventID=1234 | Sort Computer asc,TimeGenerated desc
```


Merhaba basit yukarıdaki, komutları nasıl--örnekler döndürülen filtre hello hello sonuçları hello şeklini değiştirin.

### <a name="limit-and-top"></a>Ve üst sınırı
Daha az bilinen başka bir komuta sınırıdır. PowerShell benzeri fiil sınırıdır. Sınır işlevsel olarak aynı toohello üst komuttur. Merhaba aşağıdaki sorguları hello aynı sonuçları döndürür.

```
Type=Event EventID=600 | Limit 1
```

```
Type=Event EventID=600 | Top 1
```


#### <a name="toosearch-using-top"></a>üst kullanarak toosearch
* Merhaba arama sorgusu alanına yazın`Type=Event EventID=600 | Top 1`   
    ![Arama üst](./media/log-analytics-log-searches/oms-search-top.png)

Merhaba görüntüde yukarıdaki EventID 358 bin kayıtlarıyla vardır = 600. Merhaba alanları, modelleri ve her zaman döndürülen hello sonuçları hakkında bilgi gösterir sol hello filtreleri *hello filtre bölümü tarafından* tüm dikey çizgi karakterinden önce hello parçasıdır hello sorgu. Merhaba **sonuçları** bölmesinde çünkü hello örnek komut şeklinde ve hello sonuçları dönüştürülmüş hello en son 1 sonuç, yalnızca döndürür.

### <a name="select"></a>Şunu seçin:
Merhaba SELECT komutu Select-Object PowerShell'de gibi davranır. Tüm özgün özelliklerine sahip olmayan filtrelenen sonuçları döndürür. Bunun yerine, yalnızca belirttiğiniz hello özellikleri seçer.

#### <a name="toorun-a-search-using-hello-select-command"></a>bir arama hello select komutunu kullanarak toorun
1. Aramada, yazın `Type=Event` ve ardından **arama**.
2. Tıklatın **+ daha fazla Göster** sonuçları hello tüm hello özelliklere sahip hello sonuçları tooview birinde.
3. Bazıları açıkça hello sorgu değişiklikleri çok seçin ve`Type=Event | Select Computer,EventID,RenderedDescription`.  
    ![Ara'yı seçin](./media/log-analytics-log-searches/oms-search-select.png)

Bu komut, toocontrol arama çıkış ve genellikle hello tam kayıt değil, araştırması için yalnızca gerçekten önemli veri hello bölümleri seçin istediğinizde özellikle yararlıdır. Farklı türlerde kayıtlar varsa, bu da yararlıdır *bazı* ortak özellikler, ama *tüm* kendi ortak özellikleridir. , Daha doğal olarak bir tablo gibi görünen bir çıktı oluşturmak veya tooa CSV dosyasına dışarı aktardığınız ve Excel'de massaged iyi çalışır.

## <a name="use-hello-measure-command"></a>Merhaba ölçü komutunu kullanın
ÖLÇÜ hello en çok yönlü günlük analizi aramaları komutlarda biridir. Tooapply istatistiksel tanır *işlevleri* tooyour veri ve toplama sonuçları belirli bir alana göre gruplandırılmış. Ölçü destekleyen birden çok istatistik işlevleri vardır.

### <a name="measure-count"></a>Ölçü Count() işlevi
ilk istatistiksel işlevi toowork ile Merhaba ve hello basit toounderstand biri hello *count()* işlevi.

Bir arama sorgusundan gibi sonuçları `Type=Event`, arama sonuçları tarafında kalan hello üzerinde modelleri olarak da bilinir filtrelerini göster. Merhaba filtreleri hello sonuçları için belirli bir alan değerleriyle dağıtımını yürütülen hello aramada gösterir.

![Ara ölçü birimi sayısı](./media/log-analytics-log-searches/oms-search-measure-count01.png)

Örneğin, yukarıdaki görüntü hello hello görürsünüz **bilgisayar** alan ve gösterir hello sonuçlarında hello neredeyse 739 bin olayları içinde olduğunu hello 68 benzersiz ve ayrı değerlerini **bilgisayar** Kayıtların alan. Merhaba kutucuğu yalnızca hello yazılan hello en yaygın 5 değerler üst 5 hello gösterir **bilgisayar** alanları), bu alan belirli değeri içeren belgeleri hello sayısına göre sıralanmış. Merhaba görüntüde neredeyse 369 bin olayları arasında– 90 bin hello OpsInsights04.contoso.com bilgisayardan 83 bin hello DB03.contoso.com bilgisayardan gelen vb. – görebilirsiniz.

Ne Hello kutucuğu, yalnızca hello yalnızca ilk 5 gösterir. bu yana tüm değerlerinin toosee istiyorsunuz?

Hangi hello ölçü olan komut hello count() işlevini kullanarak yapabilirsiniz. Bu işlev, herhangi bir parametre kullanmaz. Yalnızca istediğiniz toogroup tarafından – hello hello alan belirttiğiniz **bilgisayar** bu durumda alan:

`Type=Event | Measure count() by Computer`

![Ara ölçü birimi sayısı](./media/log-analytics-log-searches/oms-search-measure-count-computer.png)

Ancak, **bilgisayar** kullanılan bir alan *içinde* veri – her parçası ilişkisel veritabanı dahil olan ve ayrı olmadığından **bilgisayar** herhangi bir yere nesne. Yalnızca, değerleri hello *içinde* veri tanımlayabilir hello hangi varlık oluşturulan bunları ve diğer özellikleri sayısı ve hello veri – yönlerini bu nedenle hello terim *modeli*. Ancak, yalnızca de diğer alanlara göre gruplandırabilirsiniz. Merhaba özgün hello ölçü komuta yöneltilen neredeyse 739 bin olayları sonuçlarını da adlı bir alan olduğundan **EventID**, uygulayabileceğiniz hello bu alana göre aynı teknik toogroup ve EventID olayların sayısını alın:

```
Type=Event | Measure count() by EventID
```

Belirli bir değer içeren hello gerçek kayıt sayısı ilgilendiğiniz değil, ancak yalnızca bir listesini istiyorsanız bunun yerine hello kendilerini değerleri varsa, ekleyebileceğiniz bir *seçin* sonunda hello ve yalnızca select hello ilk sütun komutu:

```
Type=Event | Measure count() by EventID | Select EventID
```

Ardından daha karmaşık almak ve hello hello sorgu sonuçlarında önceden sıralama veya hello sütunları hello kılavuzunda çok yalnızca tıklayın.

```
Type=Event | Measure count() by EventID | Select EventID | Sort EventID asc
```

#### <a name="toosearch-using-measure-count"></a>Ölçü count kullanarak toosearch
* Merhaba arama sorgusu alanına yazın`Type=Event | Measure count() by EventID`
* Append `| Select EventID` hello sorgu toohello sonu.
* Son olarak, append `| Sort EventID asc` hello sorgu toohello sonu.

Birkaç önemli noktaları toonotice vardır ve vurgulama:

İlk olarak, gördüğünüz hello sonuçları hello özgün ham sonuçları artık değildir. Bunun yerine, toplanan sonuçları – oldukları temelde sonuçları grupları. Bu bir sorun değildir, ancak çok farklı bir farklı veri şekli hello kolay bir şekilde hello toplama/istatistiksel işlevi sonucu olarak oluşturulan hello özgün ham şeklin ile etkileşim anlamanız gerekir.

İkinci, **ölçmek sayısı** şu anda döndürür üst 100 farklı sonuçlar yalnızca hello. Bu sınır toohello diğer istatistik işlevleri geçerli değildir. Bu nedenle, ölçü count() uygulamadan önce belirli öğeleri toouse daha kesin bir filtre ilk toosearch genellikle gerekir.

## <a name="use-hello-max-and-min-functions-with-hello-measure-command"></a>Merhaba ölçü komutuyla Hello maksimum ve minimum işlevlerini kullanın
Çeşitli senaryolarda nerede **ölçü Max()** ve **ölçü MIN()** yararlıdır. Bununla birlikte, her işlev ters olduğundan birbirinden biz Max() göstermeye ve, MIN() ile kendiniz deneyebilirsiniz.

Güvenlik olayları için sorgu, sahip oldukları bir **düzeyi** değişebilir özelliği. Örneğin:

```
Type=SecurityEvent
```

![Ara ölçü sayısı Başlat](./media/log-analytics-log-searches/oms-search-measure-max01.png)

Tüm hello güvenlik tooview hello en yüksek değer istiyorsanız hello Grup alana göre ortak bir bilgisayarı verilen olayları kullanabilirsiniz

```
Type=ConfigurationAlert | Measure Max(Level) by Computer
```

![Ölçü max bilgisayar arama](./media/log-analytics-log-searches/oms-search-measure-max02.png)

Vardı hello bilgisayarlar için görüntüleyeceği **düzeyi** kayıtları, bunların çoğu sahip en az düzey 8, birçok 16 düzeyini vardı.

```
Type=ConfigurationAlert | Measure Max(Severity) by Computer
```

![bilgisayar arama ölçü max süresi oluşturulan](./media/log-analytics-log-searches/oms-search-measure-max03.png)

Bu işlev numaralarıyla iyi çalışır, ancak DateTime alanları ile de çalışır. Hello için yararlı toocheck son olduğu veya her bilgisayar için herhangi bir veri parçası için en son zaman damgasını dizinli. Örneğin: ne zaman hello en son güvenlik olayı bildirildi her makine için?

```
Type=ConfigurationChange | Measure Max(TimeGenerated) by Computer
```

## <a name="use-hello-avg-function-with-hello-measure-command"></a>Merhaba avg işlevi ile Merhaba ölçü komutunu kullanın
Merhaba Avg() istatistiksel işlevi ölçü ile kullanılan bazı alan için toocalculate hello ortalama değer sağlar ve aynı ya da diğer alan grubu tarafından hello sonuçlanır. Bu durumda, performans verileri gibi çeşitli yararlı olur.

Performans verileri ile başlayacağız. OMS şu anda hem Windows hem de Linux makineler performans sayaçlarını toplar unutmayın.

için toosearch *tüm* performans verileri, hello en temel sorgudur:

```
Type=Perf
```

![Arama avg Başlat](./media/log-analytics-log-searches/oms-search-avg01.png)

Hello fark ilk şey günlük analizi, üç Perspektifler gösterir.: hangi hello grafikleri; hello gerçek kayıtları gösteren gösterir listesi Tablo, performans sayacı verileri tablo görünümünü gösterir; ve ölçümleri, performans sayaçları hello grafiklerde gösterir.

Merhaba görüntüde yukarıdaki hello aşağıdaki belirtmek işaretlenmiş alanlar iki kümesi vardır:

* Hello ilk kümesi hello sorgu filtresi Windows performans sayacı adı, nesne adı ve örnek adını tanımlar. Bu büyük olasılıkla en yaygın olarak modelleri/filtre olarak kullanacağınız hello alanları
* **CounterValue** hello gerçek hello sayaç değeri. Bu örnekte, hello değerdir *75*.
* **TimeGenerated** 12:51, 24 saatlik zaman biçiminde değil.

Merhaba ölçümleri grafik bir görünümünü aşağıdadır.

![Arama avg Başlat](./media/log-analytics-log-searches/oms-search-avg02.png)

Merhaba Perf kayıt şekli okumayı ve diğer arama teknikleri hakkında okuyun sonra bu tür sayısal veriler ölçü Avg() tooaggregate kullanabilirsiniz.

Basit bir örnek aşağıda verilmiştir:

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" | Measure Avg(CounterValue) by Computer
```

![Ortalama görüntülendiğinden arama](./media/log-analytics-log-searches/oms-search-avg03.png)

Bu örnekte, hello toplam CPU süresi performans sayacı ve bilgisayar bazında ortalama seçin. Sonuçları tooonly hello son 6 saat toonarrow istiyorsanız, başlangıç zamanı filtre denetimi kullanabilir veya sorgunuzda aşağıdaki gibi belirtin:

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer
```

### <a name="toosearch-using-hello-avg-function-with-hello-measure-command"></a>Merhaba ölçü komutuyla Hello avg işlevi kullanarak toosearch
* Merhaba arama sorgusu, kutusuna `Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer`.

Toplama ve ilişkilendirmek veri *arasında* bilgisayarlar. Örneğin, diğeri her düğüm eşit tooany olduğu Grup çeşit konakların kümesine sahiptir ve yalnızca aynı türde çalışma ve yük kabaca dengelenmelidir tüm hello yaparlar düşünün. Tek aşağıdaki sorgulamak ve ortalamalar hello tüm grup için alma hello ile Git bunların sayaçlarını alabilirsiniz. Aşağıdaki örneğine hello ile Merhaba bilgisayarlar seçerek başlatabilirsiniz:

```
Type=Perf AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

Merhaba bilgisayarlara sahip olduğunuza göre aynı zamanda yalnızca tooselect iki ana performans göstergelerini (KPI'lar) istediğiniz: CPU kullanımı % ve % boş Disk alanı. Bu nedenle, bu hello sorgu parçası haline gelir:

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS
```

Artık aşağıdaki örneğine hello ile bilgisayarları ve sayaçları ekleyebilirsiniz:

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

Çok belirli bir seçim olduğundan hello **Avg() ölçmek** komutu dönebilirsiniz hello ortalama bilgisayar tarafından değil, ancak hello grubu CounterName gruplandırarak tarafından yeterlidir. Örneğin:

```
Type=Perf  InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03") | Measure Avg(CounterValue) by CounterName
```

Bu, birkaç ortamınızı ait KPI'ları yararlı compact bir görünümünü sağlar.

![Arama avg gruplandırma](./media/log-analytics-log-searches/oms-search-avg04.png)

Bir Panoda hello arama sorgusu kolayca kullanabilirsiniz. Örneğin, hello arama sorgusunu kaydetmek ve Pano adlı ondan oluşturma *Web grubu KPI'ları*. panoları, kullanma hakkında daha fazla toolearn bkz [günlük analizi özel bir pano oluşturun](log-analytics-dashboards.md).

![Arama avg Panosu](./media/log-analytics-log-searches/oms-search-avg05.png)

### <a name="use-hello-sum-function-with-hello-measure-command"></a>Merhaba ölçü komutuyla Hello TOPLA işlevini kullanın
Merhaba ölçü komutu benzer tooother işlevlerini Hello toplam işlevdir. Nasıl toouse hello konumundaki toplam işlev hakkında bir örnek görebilirsiniz [W3C IIS günlüklerini Microsoft Azure operasyonel Öngörüler aramada](http://blogs.msdn.com/b/dmuscett/archive/2014/09/20/w3c-iis-logs-search-in-system-center-advisor-limited-preview.aspx).

Sayı, tarih saatler ve metin dizelerini Max() ve MIN() kullanabilirsiniz. Metin dizelerini ile alfabetik olarak sıralanan ve ilk alın ve en son.

Ancak, sayısal alanlar dışında herhangi bir şeyle Sum() kullanamazsınız. Bu durum, tooAvg() de geçerlidir.

### <a name="use-hello-percentile-function-with-hello-measure-command"></a>Merhaba yüzdebirlik işlevi ile Merhaba ölçü komutunu kullanın
Bunu yalnızca sayısal alanlarında kullanabilirsiniz hello yüzdebirlik işlevi benzer tooAvg() ve Sum() olmamasıdır. Bir sayısal alana 1 too99 arasında herhangi bir yüzdebirlik kullanabilirsiniz. Her ikisi de kullanabilirsiniz **yüzdelik** ve **pct** komutları. Aşağıda birkaç örnek verilmiştir:  

```
Type:Perf CounterName:"DiskTransers/sec" |measure percentile95(CurrentValue) by Computer
```
```
Type:Perf ObjectName=LogicalDisk CounterName="Current Disk Queue Length" Computer="MyComputerName" | measure pct65(CurrentValue) by InstanceName
```

## <a name="use-hello-where-command"></a>Komutunu Hello kullanın
Burada komutu filtresi gibi çalışır, ancak hello ardışık düzen toofurther filtrede uygulanabilir hello ölçü komutu tarafından – bir sorgu hello başında filtrelenen karşılıklı tooraw sonuçları olarak üretilmiş sonuçları bir araya getirilir.

Örneğin:

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer
```

Başka bir kanal Ekle "|" karakter ve hello komutu tooonly, ortalama CPU ile %80 olduğu bilgisayarları nereden hello örnek:

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer | Where AVGCPU>80
```

Microsoft System Center - Operations Manager aşinaysanız komutu burada Yönetim Paketi terimleriyle Merhaba düşünebilirsiniz. Hello örnek kural olsaydı, hello ilk bölümü hello hello veri kaynağı ve hello komutu hello koşul algılama olduğu olacaktır.

Bir kutucuk olarak hello sorgu kullanabilirsiniz **My Pano**, monitör, türlerdeki bilgisayar CPU aşırı kullanılan olduğunda toosee olarak. panolar, hakkında daha fazla toolearn bkz [günlük analizi özel bir pano oluşturun](log-analytics-dashboards.md). Ayrıca, oluşturabilir ve hello mobil uygulama kullanarak panoları kullanın. Daha fazla bilgi için bkz: [OMS mobil uygulama ](http://www.windowsphone.com/en-us/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865). İçinde Hello alt iki döşeme görüntü aşağıdaki Merhaba, hello İzleyicisi görüntülenen listesini görebilirsiniz ve bir sayı olarak. Aslında, her zaman hello numara toobe sıfır istediğiniz ve boş liste toobe hello. Aksi halde, bir uyarı koşulu belirtir. Gerekirse, hangi makinelerin göz baskısı altında olan tootake kullanabilirsiniz.

![Mobil Pano](./media/log-analytics-log-searches/oms-search-mobile.png)

## <a name="use-hello-in-operator"></a>Merhaba işlecinde kullanın
Merhaba *IN* işleci ile birlikte *NOT ın* bağımsız değişken olarak başka bir arama dahil aramalar toouse subsearches sağlar. Bunların içerdiği içinde başka bir küme ayraçları {} içinde *birincil* veya *dış* arama. Merhaba sonucu subsearch, genellikle farklı sonuçlar listesi sonra birincil arama bir bağımsız değişken olarak kullanılır.

Arama ifadesi, ancak bir aramadan oluşturulabilir, doğrudan açıklamak olamaz, verilerinizi subsearches toomatch alt kümelerini kullanabilirsiniz. Örneğin, bir arama toofind'ın tüm olayları kullanmayı düşünüyorsanız *güvenlik güncelleştirmeleri eksik olan bilgisayarlar*, yeniden toodesign ilk tanımlayan bir subsearch gerekiyor *güvenlik güncelleştirmeleri eksik olan bilgisayarlar*  önce ait toothose konakları olayları bulur.

Bu nedenle, express *şu anda eksik olan bilgisayarlar gerekli güvenlik güncelleştirmeleri* sorgu aşağıdaki hello ile:

```
Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer
```    

![Arama örnekte](./media/log-analytics-log-searches/oms-search-in01-revised.png)

Merhaba listesine sahip olduktan sonra bu bilgisayarlar için olayları arar bir dış (birincil) arama içine iç arama toofeed hello bilgisayarların bir listesini hello aramayı kullanabilirsiniz. Merhaba iç arama ayraçlar içinde kapsayan ve hello ın işlecini kullanarak hello dış arama filtresi/alan için olası değerler olarak sonuçlarını besleme bunu. Merhaba sorgu benzeyecektir:

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer}
```
![Arama örnekte](./media/log-analytics-log-searches/oms-search-in02-revised.png)

Ayrıca hello iç arama için kullanılan filtre hello Sistem Güncelleştirme değerlendirmesi bildirimi hello tüm bilgisayarların bir anlık görüntü her 24 saatte sürüyor. Yalnızca bir gün için arama yaparak daha basit ve hassas hello iç sorgu yapabilirsiniz. Merhaba dış arama yerine hello saat seçimini hello kullanıcı arabiriminde, son 7 gün hello olayları alınırken kullanır. Bkz: [Boole işleçleri](#boolean-operators) zamanı işleçleri hakkında daha fazla bilgi.

Çünkü, dış bir hello iç arama için bir filtre değeri olarak yalnızca kullanım hello sonuçlarını Merhaba, yine de hello dış arama komutlarda uygulayabilir. Örneğin, hala başka bir ölçü komutuyla olayları yukarıda Grup hello yapabilirsiniz:

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer} | measure count() by Source
```

![Arama örnekte](./media/log-analytics-log-searches/oms-search-in03-revised.png)

Günlük analizi Hizmet tarafı zaman aşımları, tooreturn sonuçları az miktarda için de içerdiğinden ve genellikle, iç sorgu tooexecute hızla istersiniz. Merhaba iç sorgu daha fazla sonuç döndürürse, hello sonuç listesi, hangi olası hello dış arama tooreturn yanlış sonuçlara neden olabilecek kesilmiş.

Merhaba iç arama şu anda tooprovide gereken başka bir kuraldır *toplanmış* sonuçları. Diğer bir deyişle, içermesi gereken bir *ölçü* komut; şu anda bir dış arama ham sonuçları akışı olamaz.

Ayrıca, yalnızca bir ın işleci olabilir ve hello son filtre hello sorgusunda olması gerekir. Bu temelde engeller birden çok subsearches çalıştıran veya birden çok giriş işleç olamaz: hello noktasıdır yalnızca bir alt/iç arama önemli her dış Ara mümkündür.

Bu sınırları olsa da ın pek çok bağlantılı aramalar sağlar ve toodefine sağlar bilgisayarlar, kullanıcılar veya dosyaları – gibi benzeri toogroups verilerinizde ne olursa olsun hello alanları içerir. Daha fazla örnekler şunlardır:

**Tüm güncelleştirmeler, otomatik güncelleştirme ayarlarını devre dışı bilgisayarlardan eksik**

```
Type=Update UpdateState=Needed Optional=false Computer IN {Type=UpdateSummary WindowsUpdateSetting=Manual | measure count() by Computer} | measure count() by KBID
```

**SQL Server (SQL değerlendirmesi çalıştırdığı =) çalıştıran bilgisayarlardan tüm hata olayları**

```
Type=Event EventLevelName=error Computer IN {Type=SQLAssessmentRecommendation | measure count() by Computer}
```

**Etki alanı denetleyicileri (AD değerlendirmesi çalıştırdığı =) bilgisayarlardan tüm güvenlik olayları**

```
Type=SecurityEvent Computer IN { Type=ADAssessmentRecommendation | measure count() by Computer }
```

**Hangi diğer hesapları toohello üzerinde oturum burada hesabı BACONLAND\jochan açmış aynı bilgisayar?**

```
Type=SecurityEvent EventID=4624   Account!="BACONLAND\\jochan" Computer IN { Type=SecurityEvent EventID=4624   Account="BACONLAND\\jochan" | measure count() by Computer } | measure count() by Account
```

## <a name="use-hello-distinct-command"></a>Merhaba ayrı komutunu kullanın
Merhaba adı da anlaşılacağı gibi bu komut bir alan için farklı değerler listesini sağlar. Bu, şaşırtıcı basit ancak çok yararlı olur. Merhaba aynı ölçü count() komutuyla yanı sıra, aşağıda gösterilen elde edilebilir.

```
Type=Event | Measure count() by Computer
```

![FARKLI arama komut örneği](./media/log-analytics-log-searches/oms-search-distinct01-revised.png)

Tüm ilgilendiğiniz yalnızca farklı değerleri ve hello olmayıp bu değerlere sahip belgelerin bir listesi ise, ancak ardından DISTINCT çıktı temizleyici ve daha kolay tooread ve kısa sözdizimi, aşağıda gösterildiği gibi sağlayabilir.

```
Type=Event | Distinct Computer
```
![FARKLI arama komut örneği](./media/log-analytics-log-searches/oms-search-distinct02-revised.png)

## <a name="use-hello-countdistinct-function-with-hello-measure-command"></a>Merhaba ölçü komutuyla Hello countdistinct işlevini kullanın
Merhaba countdistinct işlevi hello her grup içindeki farklı değerleri sayar. Örneğin, olabilir toocount hello raporlama her türü için benzersiz bilgisayar sayısı kullanılır:

```
* | measure countdistinct(Computer) by Type
```

![OMS countdistinct](./media/log-analytics-log-searches/oms-countdistinct.png)

## <a name="use-hello-measure-interval-command"></a>Merhaba ölçü aralığı komutunu kullanın
İle gerçek zamanlı performans verileri toplama toplayabilir ve herhangi bir performans sayacı günlük analizi, görselleştirme. Yalnızca girme hello sorgu **türü: Perf** sayaçları ve günlük analizi ortamınızdaki sunucularının hello sayısına dayalı olarak ölçüm grafikleri binlerce döndürür. İsteğe bağlı ölçüm toplama ile Merhaba bakabilirsiniz genel ölçümleri ortamınızda bir yüksek düzeyde ve gerektiği gibi daha ayrıntılı veri derin Dalış.

Tooknow tüm bilgisayarlar arasında hello ortalama CPU nedir istediğinizi düşünelim. Sonuçları düzeltilmesini çünkü her bilgisayar için ortalama CPU hello bakarak faydalı olmayabilir. toolook daha fazla ayrıntı içine, Sonuç kümenizi daha küçük birer penceresi öbekleri ve görünüm bir zaman serisinin arasında farklı boyutları toplayabilirsiniz. Örneğin, hello saatlik CPU kullanımı ortalaması tüm bilgisayarlar arasında şu şekilde gerçekleştirebilirsiniz:

```
Type:Perf CounterName="% Processor Time" InstanceName="_Total" | measure avg(CounterValue) by Computer Interval 1HOUR
```

![Ölçü ortalama aralığı](./media/log-analytics-log-searches/oms-measure-avg-interval.png)

Varsayılan olarak bu sonuçları çok serisi etkileşimli satırı grafik görüntülenir.  Bu grafik serisi (y ekseni rescaling ile), yakınlaştırma ve vurgulama geçiş destekler.  Merhaba tablo görüntüleme seçeneği gerekirse hello ham verileri görüntülemek için kullanılabilir durumda kalır.

Diğer alanlara göre de gruplandırabilirsiniz. Bu örnekte, belirli bir bilgisayar için tüm hello % sayaçları adresindeki arayan ve her sayacın hello saatlik 70 yüzdebirlik değeri nedir tooknow istiyorum:

```
Type:Perf Computer=beefpatty4 CounterName=%* InstanceName=_Total | measure percentile70(CounterValue) by CounterName Interval 1HOUR
```
Bir şey toonote bu sorgular değil sınırlı tooperformance sayaçları olmasıdır. Bunları tooany ölçüm uygulayabilirsiniz. Bu örnekte, ı W3C IIS günlüklerine arayan. Her isteği işlemek için bir 5 dakikalık aralık boyunca sürer hello en uzun süre nedir tooknow istiyorum:

```
Type:W3CIISLog | measure max(TimeTaken) by csMethod Interval 5MINUTES
```

### <a name="use-multiple-aggregates-in-one-query"></a>Tek bir sorguda birden çok toplamalar kullanın
Birden çok toplama yan tümcesi bir ölçü komutta belirtebilirsiniz.  Her biri bağımsız olarak diğer adı olabilir.  Bir diğer ad hello kaynaklanan verilmemişse alan adı kullanıldı hello toplama işlevi olur (yani, avg(CounterValue)) için "avg(CounterValue)".

 ```
Type=WireData | measure avg(ReceivedBytes), avg(SentBytes) by Direction interval 1hour
```
![OMS multiaggregates1](./media/log-analytics-log-searches/oms-multiaggregates1.png)

Bir örnek daha:

 ```
* | measure countdistinct(Computer) as Computers, count() as TotalRecords by Type
```


## <a name="next-steps"></a>Sonraki adımlar
Günlük aramaları hakkında ek bilgi için bkz:

* Kullanım [günlük analizi özel alanları](log-analytics-custom-fields.md) tooextend günlük arar.
* Gözden geçirme hello [günlük analizi oturum Arama başvurusu](log-analytics-search-reference.md) tooview tüm hello arama alanları ve modelleri günlük analizi içinde kullanılabilir.
