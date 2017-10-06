---
title: "işlem düğümlerini Azure Batch havuzunda aaaAutomatically ölçeklendirme | Microsoft Docs"
description: "Etkin bir bulut havuzu toodynamically üzerinde otomatik ölçeklendirmeyi hello hello havuzdaki işlem düğümleri sayısını ayarlayın."
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: tysonn
ms.assetid: c624cdfc-c5f2-4d13-a7d7-ae080833b779
ms.service: batch
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: multiple
ms.date: 06/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b6d1e0c5d8e0e56e15a4d3588150f2466a689f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-automatic-scaling-formula-for-scaling-compute-nodes-in-a-batch-pool"></a>Bir Batch havuzunda işlem düğümlerini ölçeklendirme bir otomatik ölçeklendirme formülü oluşturma

Azure Batch havuzları tanımladığınız parametrelere göre otomatik olarak ölçeklendirebilirsiniz. Otomatik ölçeklendirme, toplu işlem düğümleri tooa havuzu görev taleplerini artış dinamik olarak ekler. ve bunlar azaldıkça işlem düğümleri kaldırır. Merhaba toplu uygulamanız tarafından kullanılan işlem düğümü sayısını otomatik olarak ayarlayarak, zaman ve para tasarrufu yapabilirsiniz. 

Otomatik bir işlem düğümleri havuzu üzerinde ile ilişkilendirerek ölçeklendirmeyi etkinleştirmek bir *otomatik ölçeklendirme formülü* tanımladığınız. Merhaba Batch hizmeti İş yükünüzün hello otomatik ölçeklendirme formülü toodetermine hello gerekli tooexecute olan işlem düğümü sayısını kullanır. İşlem düğümleri, ayrılmış düğümleri olabilir veya [düşük öncelikli düğümleri](batch-low-pri-vms.md). Toplu düzenli aralıklarla toplanan tooservice ölçüm verilerini yanıt verir. Bu ölçümleri verileri kullanarak, Batch hello formülünüzü ve yapılandırılabilir aralıklarla dayalı hello havuzdaki işlem düğümleri sayısını ayarlar.

Bir havuzu oluştururken veya var olan bir havuzu üzerinde otomatik ölçeklendirmeyi etkinleştirebilirsiniz. Varolan bir formülün otomatik ölçeklendirmeyi için yapılandırılan bir havuz üzerinde de değiştirebilirsiniz. Toplu otomatik ölçeklendirme, toopools ve toomonitor hello durumu atamadan önce formüller çalıştıran tooevaluate sağlar.

Bu makalede hello ele değişkenleri, işleçler, işlemleri ve işlevleri dahil olmak üzere, otomatik ölçeklendirme formüller yapmak çeşitli varlıklar. Aşağıdakiler ele nasıl tooobtain çeşitli kaynak ve görev ölçümleri yığın içindeki işlem. Kaynak kullanımı ve görev durumu, havuzun düğüm sayısı temelinde bu ölçümleri tooadjust kullanabilirsiniz. Batch REST ve .NET API'lerini nasıl tooconstruct bir formül ve her ikisini de kullanarak bir havuz üzerinde ölçeklendirme otomatik etkinleştir hello sonra açıklanmaktadır. Son olarak, biz birkaç örnek formüllerle sonlandırın.

> [!IMPORTANT]
> Bir toplu işlem hesabı oluşturduğunuzda, hello belirtebilirsiniz [hesabı Yapılandırması](batch-api-basics.md#account), havuzları bir toplu işlem hizmeti aboneliği (Merhaba varsayılan) ya da kullanıcı aboneliğinizi ayrılan belirler. Merhaba varsayılan toplu hizmet yapılandırması, toplu işlem hesabı oluşturduysanız, hesabınızı işleme için kullanılan çekirdek sınırlı tooa sayısı sayısıdır. Merhaba Batch hizmeti işlem düğümlerini yalnızca toothat çekirdek sınırına ölçeklendirir. Bu nedenle, Batch hizmeti hello hello otomatik ölçeklendirme formülü tarafından belirtilen işlem düğüm sayısını ulaşabilir değil. Bkz: [hello Azure Batch hizmeti için kotalar ve sınırlar](batch-quota-limit.md) görüntüleme ve hesap kotalarını artırma hakkında bilgi.
>
>Hesabınızı hello kullanıcı aboneliği yapılandırmayla oluşturduysanız, hesabınızı hello hello abonelik için çekirdek kota paylaşır. Daha fazla bilgi için [Azure aboneliği ve hizmet limitleri, kotalar ve kısıtlamalar](../azure-subscription-service-limits.md) sayfasındaki [Sanal Makine limitleri](../azure-subscription-service-limits.md#virtual-machines-limits) bölümüne bakın.
>
>

## <a name="automatic-scaling-formulas"></a>Otomatik ölçeklendirme formüller
Otomatik ölçeklendirme formülü bir veya daha fazla deyimleri içeren tanımladığınız bir dize değeridir. Merhaba otomatik ölçeklendirme formülü tooa havuzunun atanan [autoScaleFormula] [ rest_autoscaleformula] öğesi (Batch REST) ya da [CloudPool.AutoScaleFormula] [ net_cloudpool_autoscaleformula] özelliğini (Batch .NET). Merhaba Batch hizmeti işlem düğümleri formül toodetermine hello hedef sayısı hello havuzunda hello sonraki işleme aralığını kullanır. Merhaba formül dizesi 8 KB'yi aşamaz, noktalı virgülle ayrılır ve satır sonları ve açıklamalar içerebilen too100 deyimleri içerebilir.

Otomatik ölçeklendirme formüllerini bir toplu otomatik ölçeklendirme "language" düşünebilirsiniz Formül deyimleri hem hizmet tanımlı değişkenleri (Merhaba Batch hizmeti tarafından tanımlanan) hem de kullanıcı tarafından tanımlanan değişkenleri (tanımladığınız) içerebilir serbest biçimli ifadelerini. Yerleşik türler, işleçler ve işlevleri kullanarak bu değerleri üzerinde çeşitli işlemler yapabilirler. Örneğin, bir deyim form aşağıdaki hello alabilir:

```
$myNewVariable = function($ServiceDefinedVariable, $myCustomVariable);
```

Formülleri genellikle önceki deyimlerinde elde edilen değerleri işlemleri birden çok ifade içerir. Örneğin, biz için bir değer edinip `variable1`, tooa işlevi toopopulate geçirmek `variable2`:

```
$variable1 = function1($ServiceDefinedVariable);
$variable2 = function2($OtherServiceDefinedVariable, $variable1);
```

Bu ifadeler, otomatik ölçeklendirme formülü tooarrive işlem düğümlerinin hedef numaralı dahil edin. Ayrılmış düğümleri ve düşük öncelikli düğümleri kendi hedef ayarları olması, böylece her düğüm türü için bir hedef tanımlayabilirsiniz. Otomatik ölçeklendirme formülü bir hedef değer ayrılmış düğümleri, düşük öncelikli düğümler için bir hedef değer veya her ikisi de dahil edebilirsiniz.

Merhaba hedef düğüm sayısı daha yüksek, düşük veya hello geçerli türü hello havuzdaki düğüm sayısını aynı hello. Toplu işlem belirli bir aralıkla bir havuzun otomatik ölçeklendirme formülü değerlendirir (bkz [otomatik aralıklarla ölçeklendirme](#automatic-scaling-interval)). Toplu hello değerlendirme sırasında otomatik ölçeklendirme formülü belirtir hello havuz toohello sayısı düğümünde her tür hello hedef sayısını ayarlar.

### <a name="sample-autoscale-formula"></a>Örnek otomatik ölçeklendirme formülü

Çoğu senaryo için ayarlanan toowork olabilir bir otomatik ölçeklendirme formülü bir örneği burada verilmiştir. Merhaba değişkenleri `startingNumberOfVMs` ve `maxNumberofVMs` hello örnek formül ayarlanmış tooyour gereksinimleri olabilir. Bu formülü ayrılmış düğümleri ölçeklendirir ancak değiştirilmiş tooapply tooscale düşük öncelikli düğümleri de olabilir. 

```
startingNumberOfVMs = 1;
maxNumberofVMs = 25;
pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
$TargetDedicatedNodes=min(maxNumberofVMs, pendingTaskSamples);
```

Bu otomatik ölçeklendirme formülü ile Merhaba havuzu başlangıçta tek bir VM ile oluşturulur. Merhaba `$PendingTasks` ölçüm çalışan ya da kuyruğa alınmış görevlerin hello sayısını tanımlar. Merhaba formül hello ortalama sayısı Bekleyen Görevler hello Son 180 saniye bulur ve ayarlar hello `$TargetDedicatedNodes` değişkeni buna göre. Merhaba formülü ayrılmış düğümlerin hedef sayısını hello hiçbir zaman 25 VM'ler aştığını sağlar. Yeni görevler gönderildiği gibi hello havuzu otomatik olarak artar. Görevleri tam olarak boş bir birer birer VM'ler olur ve hello otomatik ölçeklendirme formülü hello havuzu küçültür.

## <a name="variables"></a>Değişkenler
Her ikisi de kullanabilirsiniz **hizmet tanımlı** ve **kullanıcı tanımlı** otomatik ölçeklendirme formüller değişkenleri. Merhaba hizmet tanımlı değişkenler toohello Batch hizmeti oluşturulur. Bazı hizmet tanımlı değişkenler okuma-yazma ve bazı salt okunurdur. Kullanıcı tarafından tanımlanan tanımlarsınız değişkenleri değişkenlerdir. Merhaba önceki bölümde gösterilen hello örnek formülünde `$TargetDedicatedNodes` ve `$PendingTasks` hizmet tanımlı değişkenlerdir. Değişkenleri `startingNumberOfVMs` ve `maxNumberofVMs` kullanıcı tanımlı değişkenlerdir.

> [!NOTE]
> Hizmet tarafından tanımlanan değişkenler her zaman bir dolar işareti ($) öncesinde olur. Kullanıcı tanımlı değişkenleri hello dolar işareti isteğe bağlıdır.
>
>

Aşağıdaki tablolar hello hem de okuma-yazma ve Batch hizmeti tarafından tanımlanan salt okunur değişkenler hello gösterir.

Alın ve hello değişkenlerin değerleri, bu hizmet tarafından tanımlanan bir havuzda toomanage hello işlem düğümü sayısını ayarlayın:

| Okuma-yazma hizmet tanımlı değişkenler | Açıklama |
| --- | --- |
| $TargetDedicatedNodes |işlem düğümleri hello havuzu için Hello hedef sayısını ayrılmış. bir havuzu her zaman hello istenen düğüm sayısını elde edebilirsiniz değil çünkü hello ayrılmış düğüm sayısı hedef olarak belirtilir. Örneğin, ayrılmış düğümlerin hedef sayısını hello değiştirilirse otomatik ölçeklendirme değerlendirme hello önce tarafından havuzu hello ilk hedef ulaştı sonra hello havuzu hello hedef ulaşabilir değil. <br /><br /> Toplu işlem hesabı düğümü veya çekirdek kotası Hello hedef aşarsa, bir havuzda hello Batch hizmeti yapılandırması ile oluşturulan bir hesap hedefine elde. Merhaba hedef hello paylaşılan çekirdek kotası hello abonelik için aşarsa hello kullanıcı aboneliği yapılandırması ile oluşturulan bir hesap havuzunda hedefine elde.|
| $TargetLowPriorityNodes |düşük öncelikli Hello hedef sayısını işlem düğümlerini hello havuzu için. bir havuzu her zaman hello istenen düğüm sayısını elde edebilirsiniz değil çünkü hello düşük öncelikli düğüm sayısı hedef olarak belirtilir. Örneğin, düşük öncelikli düğümlerin hedef sayısını hello değiştirilirse otomatik ölçeklendirme değerlendirme hello önce tarafından havuzu hello ilk hedef ulaştı sonra hello havuzu hello hedef ulaşabilir değil. Toplu işlem hesabı düğümü veya çekirdek kotası Hello hedef aşarsa, bir havuzu de hedefine elde. <br /><br /> Düşük öncelikli işlem düğümleri hakkında daha fazla bilgi için bkz: [toplu işlemi (Önizleme) ile düşük öncelikli sanal makineleri kullanmak](batch-low-pri-vms.md). |
| $NodeDeallocationOption |işlem düğümü havuzdan kaldırıldığında oluşan hello eylem. Olası değerler şunlardır:<ul><li>**requeue**--görevleri hemen sonlandırır ve böylece bunlar yeniden bunları geri hello işi sıraya koyar.<li>**sonlandırma**--görevleri hemen sonlandırır ve hello iş kuyruktan kaldırır.<li>**net_offline_option**--çalışmakta olan görevleri toofinish ve ardından hello düğümü hello havuzundan kaldırır bekler.<li>**retaineddata**--hello yerel görev korunur üzerindeki tüm verileri hello düğümü toobe bekler Temizlenen hello düğümü hello havuzundan kaldırmadan önce.</ul> |

Merhaba Batch hizmeti ölçümleri temel alan bu hizmet tarafından tanımlanan değişkenler toomake ayarlamalar hello değeri elde edebilirsiniz:

| Salt okunur hizmet tanımlı değişkenler | Açıklama |
| --- | --- |
| $CPUPercent |Merhaba ortalama CPU kullanımı yüzdesi. |
| $WallClockSeconds |Merhaba tüketilen saniye sayısı. |
| $MemoryBytes |kullanılan megabayt cinsinden ortalama sayısı Hello. |
| $DiskBytes |Merhaba ortalama hello yerel diskler üzerinde kullanılan gigabayt sayısı. |
| $DiskReadBytes |Merhaba okunan bayt sayısı. |
| $DiskWriteBytes |Merhaba yazılan bayt sayısı. |
| $DiskReadOps |disk okuma işlemleri Merhaba sayımını gerçekleştirilir. |
| $DiskWriteOps |Merhaba gerçekleştirilen yazma disk işlemlerinin sayısı. |
| $NetworkInBytes |Merhaba gelen bayt sayısı. |
| $NetworkOutBytes |Merhaba Giden bayt sayısı. |
| $SampleNodeCount |işlem düğümleri Hello sayısı. |
| $ActiveTasks |hazır tooexecute ancak değil henüz yürütülen görevler Hello sayısı. Merhaba $ActiveTasks sayısı hello etkin durumda olan ve bağımlılıklarını memnun tüm görevleri içerir. Merhaba etkin durumda olan ancak bağımlılıklarını değil uyduğunuzdan herhangi bir görevi hello $ActiveTasks sayısını hariç tutulur.|
| $RunningTasks |Merhaba sayıda görev çalışır durumda. |
| $PendingTasks |$ActiveTasks ve $RunningTasks toplamı Hello. |
| $SucceededTasks |Merhaba sayıda görev başarıyla tamamlandı. |
| $FailedTasks |başarısız görevleri Hello sayısı. |
| $CurrentDedicatedNodes |işlem düğümleri Hello geçerli sayısı ayrılmış. |
| $CurrentLowPriorityNodes |düşük öncelikli geçerli sayısı Hello işlem düğümleri, biterse tüm düğümleri de dahil olmak üzere. |
| $PreemptedNodeCount | Merhaba hello havuzdaki biterse durumda düğüm sayısı. |

> [!TIP]
> Merhaba hello önceki tabloda gösterilen salt okunur, hizmet tarafından tanımlanan değişkenlerdir *nesneleri* tooaccess veri her ile ilgili çeşitli yöntemler sağlar. Daha fazla bilgi için bkz: [örnek verileri elde](#getsampledata) bu makalenin ilerisinde yer.
>
>

## <a name="types"></a>Türler
Bu tür bir formüle desteklenir:

* Çift
* doubleVec
* doubleVecList
* Dize
* zaman damgası--zaman damgası üyeleri aşağıdaki hello içeren bileşik bir yapıdır:

  * Yıl
  * Ay (1-12)
  * gün (1-31)
  * Haftanın günü (Merhaba biçiminde numarası; Örneğin, Pazartesi günü için 1)
  * saat (24 saatlik sayı biçiminde; Örneğin, 13 13'te anlamına gelir)
  * dakika (00-59)
  * İkinci (00-59)
* TimeInterval

  * TimeInterval_Zero
  * TimeInterval_100ns
  * TimeInterval_Microsecond
  * TimeInterval_Millisecond
  * TimeInterval_Second
  * TimeInterval_Minute
  * TimeInterval_Hour
  * TimeInterval_Day
  * TimeInterval_Week
  * TimeInterval_Year

## <a name="operations"></a>İşlemler
Bu işlemler hello önceki bölümde listelenen hello türleri üzerinde izin verilir.

| İşlem | Desteklenen işleçleri | Sonuç türü |
| --- | --- | --- |
| çift *işleci* çift |+, -, *, / |Çift |
| çift *işleci* TimeInterval |* |TimeInterval |
| doubleVec *işleci* çift |+, -, *, / |doubleVec |
| doubleVec *işleci* doubleVec |+, -, *, / |doubleVec |
| TimeInterval *işleci* çift |*, / |TimeInterval |
| TimeInterval *işleci* TimeInterval |+, - |TimeInterval |
| TimeInterval *işleci* zaman damgası |+ |timestamp |
| zaman damgası *işleci* TimeInterval |+ |timestamp |
| zaman damgası *işleci* zaman damgası |- |TimeInterval |
| *İşleç*çift |-, ! |Çift |
| *İşleç*TimeInterval |- |TimeInterval |
| çift *işleci* çift |<, <=, ==, >=, >, != |Çift |
| dize *işleci* dize |<, <=, ==, >=, >, != |Çift |
| zaman damgası *işleci* zaman damgası |<, <=, ==, >=, >, != |Çift |
| TimeInterval *işleci* TimeInterval |<, <=, ==, >=, >, != |Çift |
| çift *işleci* çift |&&, &#124;&#124; |Çift |

Bir çift Üçlü operatör ile sınarken (`double ? statement1 : statement2`), sıfır olmayan olan **true**, ve sıfır **false**.

## <a name="functions"></a>İşlevler
Bu önceden tanımlanmış **işlevleri** otomatik ölçeklendirme formülü tanımlamakta toouse için kullanılabilir.

| İşlevi | Dönüş türü | Açıklama |
| --- | --- | --- |
| AVG(doubleVecList) |Çift |Ortalama değer hello doubleVecList tüm değerleri döndürür hello. |
| Len(doubleVecList) |Çift |Merhaba doubleVecList oluşturulan hello vektör uzunluğunu döndürür hello. |
| LG(double) |Çift |Merhaba günlük hello temel 2 Çift döndürür. |
| LG(doubleVecList) |doubleVec |Merhaba component-wise günlük hello doubleVecList temel 2 döndürür. Bir vec(double) açıkça hello parametresi için geçirilmelidir. Aksi takdirde hello çift lg(double) sürümü varsayılır. |
| ln(double) |Çift |Döndürür hello çift doğal günlüğünü hello. |
| ln(doubleVecList) |doubleVec |Merhaba component-wise günlük hello doubleVecList temel 2 döndürür. Bir vec(double) açıkça hello parametresi için geçirilmelidir. Aksi takdirde hello çift lg(double) sürümü varsayılır. |
| log(double) |Çift |Merhaba günlük hello temel 10 çift döndürür. |
| log(doubleVecList) |doubleVec |Merhaba component-wise günlük hello doubleVecList temel 10 döndürür. Bir vec(double) açıkça hello tek çift parametresi için geçirilmelidir. Aksi takdirde hello çift log(double) sürümü varsayılır. |
| max(doubleVecList) |Çift |Merhaba doubleVecList en büyük değeri döndürür hello. |
| Min(doubleVecList) |Çift |Döndürür hello doubleVecList en küçük değerin hello. |
| Norm(doubleVecList) |Çift |Döndürür hello doubleVecList oluşturulan hello vektör, iki norm hello. |
| Yüzdelik (doubleVec v, çift p) |Çift |Döndürür hello vektör v yüzdebirlik öğesinin hello. |
| rand() |Çift |0,0 ile 1,0 arasında rastgele bir değeri döndürür. |
| Range(doubleVecList) |Çift |Merhaba minimum ve maksimum değerleri arasındaki Hello fark hello doubleVecList döndürür. |
| Std(doubleVecList) |Çift |Merhaba doubleVecList hello değerleri örnek standart sapmasını döndürür hello. |
| Stop() | |Merhaba otomatik ölçeklendirmeyi ifadesi değerlendirmesi durdurur. |
| SUM(doubleVecList) |Çift |Merhaba doubleVecList hello bileşenlerinin tümünü toplamını döndürür hello. |
| saat (dateTime dize = "") |timestamp |Hiçbir parametre geçirilir ya da onu aktarılırsa zaman damgası hello dateTime dizesinin hello hello hello zaman damgası geçerli saati döndürür. Desteklenen tarih/saat biçimleri W3C DTF ve RFC 1123 olacaktır. |
| VAL (doubleVec v, çift i) |Çift |Konumda i vektör v, başlangıç dizini sıfır ile Merhaba öğeyi Hello değerini döndürür. |

Bazı hello önceki tabloda açıklanan hello işlevleri listesini bağımsız değişken olarak kabul edebilir. Merhaba virgülle ayrılmış listesi olduğu herhangi bir bileşimini *çift* ve *doubleVec*. Örneğin:

`doubleVecList := ( (double | doubleVec)+(, (double | doubleVec) )* )?`

Merhaba *doubleVecList* değerdir dönüştürülmüş tooa tek *doubleVec* değerlendirme önce. Örneğin, varsa `v = [1,2,3]`, ardından çağırma `avg(v)` eşdeğer toocalling olan `avg(1,2,3)`. Çağırma `avg(v, 7)` eşdeğer toocalling olan `avg(1,2,3,7)`.

## <a name="getsampledata"></a>Örnek verileri alma
Otomatik ölçeklendirme formüller hello Batch hizmeti tarafından sağlanan ölçüm verilerini (örnekler) hareket. Bir formülü büyüyor veya hello hizmetinden alır hello değerlere göre havuz boyutu küçültür. açıklandığı gibi hello hizmet tanımlı değişkenler daha önce bu nesneyle ilişkili tooaccess verileri çeşitli yöntemler sağlayan nesneleridir. Örneğin, hello aşağıdaki ifade bir istek tooget hello CPU kullanımı son beş dakika gösterir:

```
$CPUPercent.GetSample(TimeInterval_Minute * 5)
```

| Yöntem | Açıklama |
| --- | --- |
| GetSample() |Merhaba `GetSample()` yöntemi vektör verilerini örnekleri döndürür.<br/><br/>Ölçüm verilerini 30 saniyede bir örnektir. Diğer bir deyişle, örnekleri her 30 saniyede elde edilir. Ancak aşağıda belirtildiği gibi bir örnek ne zaman kullanılacağını ve kullanılabilir tooa formülü olduğunda arasında bir gecikme yoktur. Bu nedenle, belirli bir süre için tüm örnekleri bir formüle değerlendirme için kullanılabilir.<ul><li>`doubleVec GetSample(double count)`<br/>Toplanan hello en son örnekleri gelen örnekleri tooobtain Hello sayısını belirtir.<br/><br/>`GetSample(1)`Merhaba son kullanılabilir örneği döndürür. Ölçümleri ister için `$CPUPercent`, imkansız tooknow olduğundan ancak, bu kullanılmamalıdır *zaman* hello örnek toplanmıştır. Son olabilir ya da sistem sorunları nedeniyle daha eski olabilir. Böyle durumlarda toouse aşağıda gösterildiği gibi bir zaman aralığı içinde daha iyidir.<li>`doubleVec GetSample((timestamp or timeinterval) startTime [, double samplePercent])`<br/>Örnek verileri toplamak için bir zaman çerçevesi belirtir. İsteğe bağlı olarak, bu da zaman çerçevesi hello bulunmalıdır örnekleri hello yüzdesi istenen belirtir.<br/><br/>`$CPUPercent.GetSample(TimeInterval_Minute * 10)`20 örnekleri hello son 10 dakika için tüm örnekleri hello CPUPercent geçmişinde mevcut olup olmadığını döndürür. Merhaba son dakika geçmişi kullanılabilir değilse, ancak yalnızca 18 örnekleri döndürülür. Bu durumda:<br/><br/>`$CPUPercent.GetSample(TimeInterval_Minute * 10, 95)`Merhaba örnekler yüzde 90'ından yalnızca kullanılabilir olmadığından başarısız olur.<br/><br/>`$CPUPercent.GetSample(TimeInterval_Minute * 10, 80)`başarılı.<li>`doubleVec GetSample((timestamp or timeinterval) startTime, (timestamp or timeinterval) endTime [, double samplePercent])`<br/>Başlangıç zamanı ve bitiş saati ile veri toplama için bir zaman çerçevesi belirtir.<br/><br/>Yukarıda belirtildiği gibi bir örnek ne zaman kullanılacağını ve kullanılabilir tooa formülü olduğunda arasında bir gecikme olur. Merhaba kullanırken bu gecikme göz önünde bulundurun `GetSample` yöntemi. Bkz: `GetSamplePercent` aşağıda. |
| GetSamplePeriod() |Bir geçmiş örnek veri kümesinde gerçekleştirilen örnekleri Hello dönemi döndürür. |
| Count() işlevi |Örnek hello ölçüm geçmişinde toplam sayısını döndürür hello. |
| HistoryBeginTime() |Merhaba eski kullanılabilir veri örneği hello ölçümü için zaman damgasını döndürür hello. |
| GetSamplePercent() |Belirli bir zaman aralığı için kullanılabilen örnekleri yüzdesini döndürür hello. Örneğin:<br/><br/>`doubleVec GetSamplePercent( (timestamp or timeinterval) startTime [, (timestamp or timeinterval) endTime] )`<br/><br/>Çünkü hello `GetSample` yöntem başarısız döndürülen örnekleri hello yüzdesi hello küçükse `samplePercent` belirtilen hello kullanabilirsiniz `GetSamplePercent` yöntemi toocheck ilk. Ardından, yetersiz örnekleri hello otomatik ölçeklendirme değerlendirme durdurma olmadan yoksa alternatif bir eylem gerçekleştirebilirsiniz. |

### <a name="samples-sample-percentage-and-hello-getsample-method"></a>Örnekleri, örnek yüzdesi ve hello *GetSample()* yöntemi
otomatik ölçeklendirme formülü Hello temel işlevleri tooobtain görev ve kaynak ölçüm verilerinin ve verilere dayanan havuz boyutunu Ayarla. Bu nedenle, önemli toohave otomatik ölçeklendirme formüller (örnekler) ölçüm verileri ile nasıl etkileşim NET bir anlayış olur.

**Örnekler**

Merhaba Batch hizmeti düzenli aralıklarla görev ve kaynak ölçümleri örneklerini alır ve bunları kullanılabilir tooyour otomatik ölçeklendirme formüller sunar. Bu örnekler, her 30 saniyede hello Batch hizmeti tarafından kaydedilir. Ancak, genellikle bir gecikme olur ve bunlar çok kullanılabilir hale getirilir (ve tarafından okunur olduğunda) olduğunda bu örnekleri kaydedilmiş arasında otomatik ölçeklendirme formüller. Ayrıca, ağ ve diğer altyapı sorunlar gibi toovarious Etkenler örnekleri için belirli bir aralık kaydedilmemiş olabilir.

**Örnek yüzdesi**

Zaman `samplePercent` toohello geçirilen `GetSample()` yöntemi veya hello `GetSamplePercent()` yöntemi çağrıldığında, _yüzde_ hello toplam olası hello Batch hizmeti tarafından kaydedilen örnek sayısı arasında tooa karşılaştırma başvuruyor ve kullanılabilir tooyour otomatik ölçeklendirme formülü olan örnek Hello sayısı.

Örneğin 10 dakikalık timespan bakalım. Örnekleri her 30 saniyede 10 dakikalık timespan içinde kayıtlı olduğundan, hello toplam sayısı toplu işi tarafından kaydedilen örnekleri 20 örnekleri (dakika başına 2) olacaktır. Ancak, toohello yapısında gecikme hello raporlama mekanizması ve Azure içindeki diğer sorunlar, olabilir yalnızca okumak için kullanılabilir tooyour otomatik ölçeklendirme formülü olan 15 örnekleri. Bu nedenle, örneğin, söz konusu 10 dakikalık dönem için yalnızca %75 hello toplam kaydedilen örnekleri sayısının kullanılabilir tooyour formül olabilir.

**GetSample() ve örnek aralıkları**

Devam eden toobe büyüyen ve havuzlarınızı küçültme, otomatik ölçeklendirme formülüdür &mdash; düğüm ekleme veya düğümleri kaldırma. Düğümleri para maliyet olduğundan, formüller yeterli verilerine dayalı analiz akıllı bir yöntem kullanın tooensure istiyorsunuz. Bu nedenle, eğilim türü çözümlemesi formüllerde kullanmanızı öneririz. Bu tür büyür ve toplanan örnekleri bir aralığı tabanlı havuzlarınızı küçültür.

Bu nedenle, toodo kullanmak `GetSample(interval look-back start, interval look-back end)` tooreturn vektör örnekleri:

```
$runningTasksSample = $RunningTasks.GetSample(1 * TimeInterval_Minute, 6 * TimeInterval_Minute);
```

Satırın yukarısında Hello toplu işi tarafından değerlendirildiğinde değerlerin vektör olarak örnekleri bir dizi döndürür. Örneğin:

```
$runningTasksSample=[1,1,1,1,1,1,1,1,1,1];
```

Hello vektör örnekleri derledik sonra gibi İşlevler ardından kullanabilirsiniz `min()`, `max()`, ve `avg()` hello tooderive anlamlı değerleri aralığı toplanır.

Belirli bir örnek yüzdeden küçük belirli bir süre için kullanılabilir durumdaysa, ek güvenlik için bir formül değerlendirme toofail zorlayabilirsiniz. Formül Değerlendirme toofail zorla zaman hello örnekleri yüzdesi belirtilen hello formülü değerlendirmesi kullanılabilir değilse toplu toocease daha fazla isteyin. Bu durumda, hiçbir değişiklik toohello havuz boyutu yapılır. toospecify örnekler hello değerlendirme toosucceed için gerekli bir yüzdesini belirtin, bu, üçüncü parametre çok hello gibi`GetSample()`. Burada, örnekler yüzde 75'ini gereksinimi belirtilir:

```
$runningTasksSample = $RunningTasks.GetSample(60 * TimeInterval_Second, 120 * TimeInterval_Second, 75);
```

Örnek kullanılabilirlik bir gecikme olabilir çünkü, tooalways bir dakikadan daha eski bir arka plan görünüm başlangıç saatine sahip bir zaman aralığı belirtin önemlidir. Merhaba sistemi aracılığıyla örnekleri toopropagate şekilde örnekleri için hello aralığında yaklaşık bir dakika sürer `(0 * TimeInterval_Second, 60 * TimeInterval_Second)` kullanılamayabilir. Merhaba yüzdesi parametresinin tekrar kullanabilirsiniz `GetSample()` tooforce belirli örnek yüzdesi gereksinimi.

> [!IMPORTANT]
> Biz **tavsiye** , **bağlı olan kaçının *yalnızca* üzerinde `GetSample(1)` , otomatik ölçeklendirme formüllerde**. Bunun nedeni, `GetSample(1)` temelde diyor toohello Batch hizmeti, "Beni hello sahip olduğunuz son örnekten verin Hayır önemli alınan ne kadar zaman önce." Yalnızca tek bir örnek olduğundan ve eski bir örnek olabilir olduğundan, son görev veya kaynak durumunu hello daha büyük resmi temsilcisi olmayabilir. Kullanırsanız `GetSample(1)`, daha büyük bir deyim bir parçası olduğundan emin olun ve formülünüzü güvenen veri noktası hello değil.
>
>

## <a name="metrics"></a>Ölçümler
Bir formülü tanımlarken, hem kaynak hem de görev ölçümleri kullanabilirsiniz. Merhaba almak ve değerlendirmek hello ölçümleri verilerine dayalı hello havuzundaki ayrılmış düğümlerin hedef sayısını ayarlayın. Merhaba bkz [değişkenleri](#variables) bölümünde yukarıda her ölçümü hakkında daha fazla bilgi için.

<table>
  <tr>
    <th>Ölçüm</th>
    <th>Açıklama</th>
  </tr>
  <tr>
    <td><b>Kaynak</b></td>
    <td><p>Kaynak ölçümleri hello CPU, hello bant genişliği, işlem düğümleri hello bellek kullanımını dayalıdır ve düğüm sayısını hello.</p>
        <p> Bu hizmet tarafından tanımlanan değişkenler, düğüm sayısına göre ayarlamaları yapmak için yararlıdır:</p>
    <p><ul>
            <li>$TargetDedicatedNodes</li>
            <li>$TargetLowPriorityNodes</li>
            <li>$CurrentDedicatedNodes</li>
            <li>$CurrentLowPriorityNodes</li>
            <li>$preemptedNodeCount</li>
            <li>$SampleNodeCount</li>
    </ul></p>
    <p>Bu hizmet tarafından tanımlanan değişkenler, düğüm kaynak kullanımına bağlı ayarlamaları yapmak için yararlıdır:</p>
    <p><ul>
      <li>$CPUPercent</li>
      <li>$WallClockSeconds</li>
      <li>$MemoryBytes</li>
      <li>$DiskBytes</li>
      <li>$DiskReadBytes</li>
      <li>$DiskWriteBytes</li>
      <li>$DiskReadOps</li>
      <li>$DiskWriteOps</li>
      <li>$NetworkInBytes</li>
      <li>$NetworkOutBytes</li></ul></p>
  </tr>
  <tr>
    <td><b>Görev</b></td>
    <td><p>Görev ölçümleri hello durumunun etkin gibi görevler, temel ve tamamlandı. Merhaba aşağıdaki hizmet tanımlı değişkenler görev ölçümleri temel havuz boyutu ayarlamaları yapmak için yararlıdır:</p>
    <p><ul>
      <li>$ActiveTasks</li>
      <li>$RunningTasks</li>
      <li>$PendingTasks</li>
      <li>$SucceededTasks</li>
            <li>$FailedTasks</li></ul></p>
        </td>
  </tr>
</table>

## <a name="write-an-autoscale-formula"></a>Otomatik ölçeklendirme formülü yazma
Otomatik ölçeklendirme formülü bileşenleri yukarıda hello kullan deyimleri oluşturan tarafından yapı sonra bu ifadeleri tam bir formüle birleştirin. Bu bölümde, bazı gerçek ölçeklendirme kararları gerçekleştirebileceğiniz bir örnek otomatik ölçeklendirme formülü oluşturun.

İlk olarak, şirketinizdeki bizim yeni otomatik ölçeklendirme formülü için hello gereksinimleri tanımlayın. Merhaba formülü gerekir:

1. CPU kullanımı yüksekse, adanmış bir işlem düğümleri havuzunda hello hedef sayısını artırın.
2. CPU kullanımı düşük olduğunda hello hedef adanmış bir işlem düğümleri havuzunda sayısını azaltın.
3. Her zaman ayrılmış düğümleri too400 hello sayısını sınırlayın.

tooincrease hello yüksek CPU kullanımı sırasında düğüm sayısını tanımlayan bir kullanıcı tanımlı değişken doldurur hello deyimi (`$totalDedicatedNodes`) hello geçerli düğümlerin hedef sayısını ayrılmış, ancak yalnızca 110 yüzdesi ise bir değer ile en düşük ortalama CPU kullanımını hello Son 10 dakika sırasında Hello yüzde 70'idi. Aksi takdirde hello değeri hello geçerli ayrılmış düğüm sayısı için kullanın.

```
$totalDedicatedNodes =
    (min($CPUPercent.GetSample(TimeInterval_Minute * 10)) > 0.7) ?
    ($CurrentDedicatedNodes * 1.1) : $CurrentDedicatedNodes;
```

çok*azaltmak* ayrılmış düğüm sayısını düşük CPU kullanımı sırasında Merhaba, bizim formül kümeleri hello sonraki deyiminde aynı hello `$totalDedicatedNodes` hello geçerli düğümlerin hedef sayısını ayrılmış Merhaba, değişken too90 yüzdesi ortalama CPU kullanımı Hello son 60 dakika altında yüzde 20 oluştu. Aksi takdirde hello geçerli değerini kullanın `$totalDedicatedNodes` biz yukarıdaki hello ifade doldurulmuş.

```
$totalDedicatedNodes =
    (avg($CPUPercent.GetSample(TimeInterval_Minute * 60)) < 0.2) ?
    ($CurrentDedicatedNodes * 0.9) : $totalDedicatedNodes;
```

Şimdi adanmış bir işlem düğümleri tooa en fazla 400 hello hedef sayısı sınırı:

```
$TargetDedicatedNodes = min(400, $totalDedicatedNodes)
```

Merhaba tam formülü şöyledir:

```
$totalDedicatedNodes =
    (min($CPUPercent.GetSample(TimeInterval_Minute * 10)) > 0.7) ?
    ($CurrentDedicatedNodes * 1.1) : $CurrentDedicatedNodes;
$totalDedicatedNodes =
    (avg($CPUPercent.GetSample(TimeInterval_Minute * 60)) < 0.2) ?
    ($CurrentDedicatedNodes * 0.9) : $totalDedicatedNodes;
$TargetDedicatedNodes = min(400, $totalDedicatedNodes)
```

## <a name="create-an-autoscale-enabled-pool-with-net"></a>.NET ile birlikte otomatik ölçeklendirme özellikli bir havuz oluşturma

toocreate .NET içinde etkin otomatik ölçeklendirmeyi havuzuyla şu adımları izleyin:

1. Merhaba havuzuyla oluşturma [BatchClient.PoolOperations.CreatePool](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.createpool).
2. Set hello [CloudPool.AutoScaleEnabled](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleenabled) özelliği çok`true`.
3. Set hello [CloudPool.AutoScaleFormula](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleformula) otomatik ölçeklendirme formülü özelliğiyle.
4. (İsteğe bağlı) Set hello [CloudPool.AutoScaleEvaluationInterval](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleevaluationinterval) özelliği (varsayılan değer 15 dakika).
5. Merhaba havuzuyla yürütme [CloudPool.Commit](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.commit) veya [CommitAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.commitasync).

Merhaba aşağıdaki kod parçacığını bir otomatik ölçeklendirme özellikli havuzu .NET içinde oluşturur. Hello havuzun otomatik ölçeklendirme formülü ayrılmış düğümleri too5 Pazartesi günleri ve her bir hello haftanın gününü 1 hello hedef sayısını ayarlar. Merhaba [otomatik ölçeklendirme aralığı](#automatic-scaling-interval) olan too30 dakika ayarlayın. Bu ve diğer C# kod parçacıkları bu makalede, hello `myBatchClient` hello düzgün başlatılmadı örneğidir [BatchClient] [ net_batchclient] sınıfı.

```csharp
CloudPool pool = myBatchClient.PoolOperations.CreatePool(
                    poolId: "mypool",
                    virtualMachineSize: "small", // single-core, 1.75 GB memory, 225 GB disk
                    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "5"));    
pool.AutoScaleEnabled = true;
pool.AutoScaleFormula = "$TargetDedicatedNodes = (time().weekday == 1 ? 5:1);";
pool.AutoScaleEvaluationInterval = TimeSpan.FromMinutes(30);
await pool.CommitAsync();
```

> [!IMPORTANT]
> Otomatik ölçeklendirme özellikli bir havuz oluşturduğunuzda, hello belirtmeyin _targetDedicatedComputeNodes_ parametresi veya hello _targetLowPriorityComputeNodes_ hello parametresini çağrı çok **CreatePool**. Bunun yerine, hello belirtin **AutoScaleEnabled** ve **AutoScaleFormula** hello havuzu özellikleri. Bu özelliklerin değerlerini Hello hello hedef her düğüm türünün sayısını belirler. Toomanually otomatik ölçeklendirme özellikli bir havuz Ayrıca, yeniden boyutlandırma (örneğin, [BatchClient.PoolOperations.ResizePoolAsync][net_poolops_resizepoolasync]), ilk **devre dışı** üzerinde otomatik ölçeklendirme Havuz Merhaba, sonra yeniden boyutlandırın.
>
>

Ayrıca tooBatch .NET hello başka birini kullanabilirsiniz [Batch SDK'ları](batch-apis-tools.md#azure-accounts-for-batch-development), [Batch REST](https://docs.microsoft.com/rest/api/batchservice/), [Batch PowerShell cmdlet'leri](batch-powershell-cmdlets-get-started.md)ve hello [toplu CLI](batch-cli-get-started.md)tooconfigure otomatik ölçeklendirmeyi.


### <a name="automatic-scaling-interval"></a>Otomatik ölçeklendirme aralığı
Varsayılan olarak, hello Batch hizmeti bir havuzun boyutu tooits 15 dakikada bir otomatik ölçeklendirme formülü göre ayarlar. Aşağıdaki havuzu özelliklere hello kullanarak bu aralığı yapılandırılabilir:

* [CloudPool.AutoScaleEvaluationInterval] [ net_cloudpool_autoscaleevalinterval] (Batch .NET)
* [autoScaleEvaluationInterval] [ rest_autoscaleinterval] (REST API'si)

Hello minimum aralık beş dakikadır ve en fazla hello 168 saattir. Bu aralığın dışında kalan bir aralık belirtilirse, hello Batch hizmeti hatalı istek (400) bir hata döndürür.

> [!NOTE]
> Otomatik ölçeklendirmeyi şu anda hedeflenen toorespond toochanges değerinden bir dakika içinde değil, ancak yerine olduğu hedeflenen tooadjust hello boyutu havuzunuzun kademeli olarak bir iş yükünü çalıştırmak gibi.
>
>

## <a name="enable-autoscaling-on-an-existing-pool"></a>Var olan bir havuzu üzerinde otomatik ölçeklendirmeyi etkinleştirme

Her Batch SDK'sı bir şekilde tooenable otomatik ölçeklendirmeyi sağlar. Örneğin:

* [BatchClient.PoolOperations.EnableAutoScaleAsync] [ net_enableautoscaleasync] (Batch .NET)
* [Otomatik bir havuz üzerinde ölçeklendirmeyi etkinleştirmek] [ rest_enableautoscale] (REST API'si)

Var olan bir havuzu üzerinde otomatik ölçeklendirmeyi etkinleştirdiğinizde, aşağıdaki noktaları göz önünde hello tutun:

* Merhaba isteği tooenable otomatik ölçeklendirmeyi kesilirken otomatik ölçeklendirmeyi şu anda hello havuzunda devre dışıysa, hello isteği gönderdiğinizde, geçerli otomatik ölçeklendirme formülü belirtmeniz gerekir. İsteğe bağlı olarak, otomatik ölçeklendirme deneme aralığı belirtebilirsiniz. Bir aralık belirtmezseniz hello varsayılan değer 15 dakika kullanılır.
* Otomatik ölçeklendirme hello havuzunda etkinse, otomatik ölçeklendirme formülü, bir deneme aralığı ya da her ikisini de belirtebilirsiniz. Bu özelliklerden en az birini belirtmeniz gerekir.

  * Yeni bir otomatik ölçeklendirme değerlendirme aralığı belirtirseniz, hello varolan değerlendirme zamanlamasını durdurulur ve yeni bir zamanlama başlatılır. Merhaba yeni zamanlamanın başlangıç zamanı hangi hello isteği tooenable otomatik ölçeklendirmeyi verilmiş hello saattir.
  * Her iki hello otomatik ölçeklendirme formülü veya değerlendirme aralığını atlarsanız, hello Batch hizmeti toouse hello geçerli değeri bu ayarı devam eder.

> [!NOTE]
> Merhaba değerlerini belirtilmişse *targetDedicatedComputeNodes* veya *targetLowPriorityComputeNodes* hello parametrelerinin **CreatePool** hello oluşturduğunuzda yöntemi otomatik ölçeklendirme formülü hello değerlendirildiğinde havuzu .NET veya başka bir dilde daha sonra bu değerler karşılaştırılabilir parametrelerinde hello yoksayılır.
>
>

Bu C# kod parçacığını hello kullanan [Batch .NET] [ net_api] kitaplığı tooenable otomatik ölçeklendirmeyi var olan bir havuzu üzerinde:

```csharp
// Define hello autoscaling formula. This formula sets hello target number of nodes
// too5 on Mondays, and 1 on every other day of hello week
string myAutoScaleFormula = "$TargetDedicatedNodes = (time().weekday == 1 ? 5:1);";

// Set hello autoscale formula on hello existing pool
await myBatchClient.PoolOperations.EnableAutoScaleAsync(
    "myexistingpool",
    autoscaleFormula: myAutoScaleFormula);
```

### <a name="update-an-autoscale-formula"></a>Otomatik ölçeklendirme formülü güncelleştir

Mevcut bir otomatik ölçeklendirme özellikli havuz hello yeni formül'yla yeniden çağrı hello işlemi tooenable otomatik ölçeklendirmeyi tooupdate hello formül. Örneğin, otomatik ölçeklendirmeyi zaten etkinleştirilmişse `myexistingpool` .NET koddan hello yürütüldüğünde, otomatik ölçeklendirme formülü hello içeriğiyle değiştirilir `myNewFormula`.

```csharp
await myBatchClient.PoolOperations.EnableAutoScaleAsync(
    "myexistingpool",
    autoscaleFormula: myNewFormula);
```

### <a name="update-hello-autoscale-interval"></a>Güncelleştirme hello otomatik ölçeklendirme aralığı

tooupdate hello otomatik ölçeklendirme değerlendirme aralığı mevcut bir otomatik ölçeklendirme özellikli havuz başlangıç yeni aralığı'yla yeniden çağrı hello işlemi tooenable otomatik ölçeklendirmeyi. Örneğin, tooset hello otomatik ölçeklendirme değerlendirme aralığı too60 dakika otomatik ölçeklendirme özellikli .NET içinde zaten bir havuz için:

```csharp
await myBatchClient.PoolOperations.EnableAutoScaleAsync(
    "myexistingpool",
    autoscaleEvaluationInterval: TimeSpan.FromMinutes(60));
```

## <a name="evaluate-an-autoscale-formula"></a>Otomatik ölçeklendirme Formülü Değerlendir

Bir formülü tooa havuzu uygulamadan önce değerlendirebilir. Bu şekilde, hello formülü üretime koymadan önce deyimleri nasıl değerlendirmek hello formül toosee test edebilirsiniz.

otomatik ölçeklendirme formülü tooevaluate, önce geçerli bir formül ile Merhaba havuzunda otomatik ölçeklendirmeyi etkinleştirmeniz gerekir. tootest bir formül otomatik ölçeklendirmeyi henüz yok havuzunda etkin, kullanım hello tek satır formülü `$TargetDedicatedNodes = 0` ilk etkinleştirdiğinizde otomatik ölçeklendirmeyi. Ardından, tootest istediğiniz tooevaluate hello formülü aşağıdaki hello birini kullanın:

* [BatchClient.PoolOperations.EvaluateAutoScale](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.evaluateautoscale) veya [EvaluateAutoScaleAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.evaluateautoscaleasync)

    Bu Batch .NET yöntemleri hello kimliği var olan bir havuzu ve hello otomatik ölçeklendirme formülü tooevaluate içeren bir dize gerektirir.

* [Otomatik ölçeklendirme Formülü Değerlendir](https://docs.microsoft.com/rest/api/batchservice/evaluate-an-automatic-scaling-formula)

    Bu REST API isteği hello URI hello Havuz kimliği belirtin ve hello hello otomatik ölçeklendirme formülü *autoScaleFormula* hello istek gövdesi öğesidir. Merhaba yanıt hello işleminin ilgili toohello formülü olabilecek hata bilgilerini içerir.

Bu [Batch .NET] [ net_api] kod parçacığında, biz otomatik ölçeklendirme formülü değerlendirin. Merhaba havuzu etkin otomatik ölçeklendirmeyi yoksa, biz öncelikle etkinleştirin.

```csharp
// First obtain a reference tooan existing pool
CloudPool pool = await batchClient.PoolOperations.GetPoolAsync("myExistingPool");

// If autoscaling isn't already enabled on hello pool, enable it.
// You can't evaluate an autoscale formula on non-autoscale-enabled pool.
if (pool.AutoScaleEnabled == false)
{
    // We need a valid autoscale formula tooenable autoscaling on the
    // pool. This formula is valid, but won't resize hello pool:
    await pool.EnableAutoScaleAsync(
        autoscaleFormula: "$TargetDedicatedNodes = {pool.CurrentDedicatedNodes};",
        autoscaleEvaluationInterval: TimeSpan.FromMinutes(5));

    // Batch limits EnableAutoScaleAsync calls tooonce every 30 seconds.
    // Because we want tooapply our new autoscale formula below if it
    // evaluates successfully, and we *just* enabled autoscaling on
    // this pool, we pause here tooensure we pass that threshold.
    Thread.Sleep(TimeSpan.FromSeconds(31));

    // Refresh hello properties of hello pool so that we've got the
    // latest value for AutoScaleEnabled
    await pool.RefreshAsync();
}

// We must ensure that autoscaling is enabled on hello pool prior to
// evaluating a formula
if (pool.AutoScaleEnabled == true)
{
    // hello formula tooevaluate - adjusts target number of nodes based on
    // day of week and time of day
    string myFormula = @"
        $curTime = time();
        $workHours = $curTime.hour >= 8 && $curTime.hour < 18;
        $isWeekday = $curTime.weekday >= 1 && $curTime.weekday <= 5;
        $isWorkingWeekdayHour = $workHours && $isWeekday;
        $TargetDedicatedNodes = $isWorkingWeekdayHour ? 20:10;
    ";

    // Perform hello autoscale formula evaluation. Note that this code does not
    // actually apply hello formula toohello pool.
    AutoScaleRun eval =
        await batchClient.PoolOperations.EvaluateAutoScaleAsync(pool.Id, myFormula);

    if (eval.Error == null)
    {
        // Evaluation success - print hello results of hello AutoScaleRun.
        // This will display hello values of each variable as evaluated by the
        // autoscale formula.
        Console.WriteLine("AutoScaleRun.Results: " +
            eval.Results.Replace("$", "\n    $"));

        // Apply hello formula toohello pool since it evaluated successfully
        await batchClient.PoolOperations.EnableAutoScaleAsync(pool.Id, myFormula);
    }
    else
    {
        // Evaluation failed, output hello message associated with hello error
        Console.WriteLine("AutoScaleRun.Error.Message: " +
            eval.Error.Message);
    }
}
```

Bu kod parçacığında gösterildiği hello formülü başarılı değerlendirmesi için benzer sonuçlar üretir:

```
AutoScaleRun.Results:
    $TargetDedicatedNodes=10;
    $NodeDeallocationOption=requeue;
    $curTime=2016-10-13T19:18:47.805Z;
    $isWeekday=1;
    $isWorkingWeekdayHour=0;
    $workHours=0
```

## <a name="get-information-about-autoscale-runs"></a>Otomatik ölçeklendirme çalışmaları hakkında bilgi edinin

Formül olarak gerçekleştirme tooensure düzenli aralıklarla toplu havuzunuzun üzerinde gerçekleştirir hello otomatik ölçeklendirmeyi çalıştırır hello sonuçlarını denetlemenizi öneririz bekleniyordu. toodo bu nedenle, Al (veya yenileme) bir başvuru toohello havuzu ve hello çalıştırmak, son otomatik ölçeklendirme özelliklerini inceleyin.

Batch .NET içinde hello [CloudPool.AutoScaleRun](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscalerun) özelliği hello son otomatik hello havuzu üzerinde gerçekleştirilen çalışır ölçeklendirme hakkında bilgi sağlayan çeşitli özellikler vardır:

* [AutoScaleRun.Timestamp](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.autoscalerun.timestamp)
* [AutoScaleRun.Results](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.autoscalerun.results)
* [AutoScaleRun.Error](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.autoscalerun.error)

Hello REST API, hello [bir havuzu hakkında bilgi alma](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-pool) isteği hello son otomatik hello çalıştırın ölçeklendirme içerir hello havuzu hakkındaki bilgileri döndürür [autoScaleRun](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-pool#bk_autrun) özelliği.

Merhaba aşağıdaki C# kod parçacığını kullanan hello Batch .NET kitaplığı tooprint havuzu üzerinde çalışır hello son otomatik ölçeklendirmeyi bilgilerini _myPool_:

```csharp
await Cloud pool = myBatchClient.PoolOperations.GetPoolAsync("myPool");
Console.WriteLine("Last execution: " + pool.AutoScaleRun.Timestamp);
Console.WriteLine("Result:" + pool.AutoScaleRun.Results.Replace("$", "\n  $"));
Console.WriteLine("Error: " + pool.AutoScaleRun.Error);
```

Önceki kod parçacığında hello örnek çıktı:

```
Last execution: 10/14/2016 18:36:43
Result:
  $TargetDedicatedNodes=10;
  $NodeDeallocationOption=requeue;
  $curTime=2016-10-14T18:36:43.282Z;
  $isWeekday=1;
  $isWorkingWeekdayHour=0;
  $workHours=0
Error:
```

## <a name="example-autoscale-formulas"></a>Örnek otomatik ölçeklendirme formüller
Bir havuzda işlem kaynakları, farklı şekillerde tooadjust hello miktarını gösteren birkaç formüller bakalım.

### <a name="example-1-time-based-adjustment"></a>Örnek 1: Zamana dayalı ayarlama
Merhaba hello haftanın gününü ve günün saatini göre tooadjust hello havuz boyutu istediğinizi varsayalım. Bu örnek nasıl hello düğümlerin azaltın veya tooincrease hello sayısı buna göre havuz gösterir.

Merhaba formülü hello önce geçerli saati alır. Haftanın günü (1-5) ise ve çalışma saatleri içinde (too6 8: 00 PM), hello hedef havuz boyutu, too20 düğümleri ayarlanır. Aksi takdirde too10 düğümleri ayarladı.

```
$curTime = time();
$workHours = $curTime.hour >= 8 && $curTime.hour < 18;
$isWeekday = $curTime.weekday >= 1 && $curTime.weekday <= 5;
$isWorkingWeekdayHour = $workHours && $isWeekday;
$TargetDedicatedNodes = $isWorkingWeekdayHour ? 20:10;
```

### <a name="example-2-task-based-adjustment"></a>Örnek 2: Görev tabanlı ayarlama
Bu örnekte, hello havuz boyutu hello sırasındaki görevleri hello sayısına göre ayarlanır. Hem açıklamaları hem de satır sonu formül dizelerde kabul edilir.

```csharp
// Get pending tasks for hello past 15 minutes.
$samples = $ActiveTasks.GetSamplePercent(TimeInterval_Minute * 15);
// If we have fewer than 70 percent data points, we use hello last sample point,
// otherwise we use hello maximum of last sample point and hello history average.
$tasks = $samples < 70 ? max(0,$ActiveTasks.GetSample(1)) : max( $ActiveTasks.GetSample(1), avg($ActiveTasks.GetSample(TimeInterval_Minute * 15)));
// If number of pending tasks is not 0, set targetVM toopending tasks, otherwise
// half of current dedicated.
$targetVMs = $tasks > 0? $tasks:max(0, $TargetDedicatedNodes/2);
// hello pool size is capped at 20, if target VM value is more than that, set it
// too20. This value should be adjusted according tooyour use case.
$TargetDedicatedNodes = max(0, min($targetVMs, 20));
// Set node deallocation mode - keep nodes active only until tasks finish
$NodeDeallocationOption = taskcompletion;
```

### <a name="example-3-accounting-for-parallel-tasks"></a>Örnek 3: Paralel Görevler için hesap oluşturma
Bu örnek hello havuz boyutu hello görevleri sayısına göre ayarlar. Bu formülü ayrıca hesap hello alır [MaxTasksPerComputeNode] [ net_maxtasks] hello havuzu için ayarlanan değeri. Bu yaklaşım durumlarda faydalıdır nerede [paralel görev yürütme](batch-parallel-node-tasks.md) havuzunuzun üzerinde etkin.

```csharp
// Determine whether 70 percent of hello samples have been recorded in hello past
// 15 minutes; if not, use last sample
$samples = $ActiveTasks.GetSamplePercent(TimeInterval_Minute * 15);
$tasks = $samples < 70 ? max(0,$ActiveTasks.GetSample(1)) : max( $ActiveTasks.GetSample(1),avg($ActiveTasks.GetSample(TimeInterval_Minute * 15)));
// Set hello number of nodes tooadd tooone-fourth hello number of active tasks (the
// MaxTasksPerComputeNode property on this pool is set too4, adjust this number
// for your use case)
$cores = $TargetDedicatedNodes * 4;
$extraVMs = (($tasks - $cores) + 3) / 4;
$targetVMs = ($TargetDedicatedNodes + $extraVMs);
// Attempt toogrow hello number of compute nodes toomatch hello number of active
// tasks, with a maximum of 3
$TargetDedicatedNodes = max(0,min($targetVMs,3));
// Keep hello nodes active until hello tasks finish
$NodeDeallocationOption = taskcompletion;
```

### <a name="example-4-setting-an-initial-pool-size"></a>Örnek 4: ilk havuz boyutu ayarlama
C# kod parçacığını ayarlar bir otomatik ölçeklendirme formülü olan gösterir havuz boyutu tooa hello Bu örnek ilk bir süre için düğüm sayısı belirtildi. Merhaba havuz boyutu hello çalışan sayısına göre ayarlar ve hello ilk sonra süre etkin görevleri geçtikten.

Aşağıdaki kod parçacığını hello formülde Hello:

* Merhaba ilk havuz boyutu toofour düğümleri ayarlar.
* Merhaba havuz boyutu hello içinde ilk 10 dakika hello havuzunun yaşam döngüsünün ayarlanmaz.
* Merhaba en fazla değer 10 dakika sonra edinir hello çalışan sayısı ve etkin son 60 dakika içinde hello görevler.
  * Her iki değerler 0 (hiçbir görev çalışan ya da hello etkin son 60 dakika gösteren) ise hello havuz boyutu too0 ayarlanır.
  * İki değer sıfırdan büyük olması durumunda değişiklik yapılmaz.

```csharp
string now = DateTime.UtcNow.ToString("r");
string formula = string.Format(@"
    $TargetDedicatedNodes = {1};
    lifespan         = time() - time(""{0}"");
    span             = TimeInterval_Minute * 60;
    startup          = TimeInterval_Minute * 10;
    ratio            = 50;

    $TargetDedicatedNodes = (lifespan > startup ? (max($RunningTasks.GetSample(span, ratio), $ActiveTasks.GetSample(span, ratio)) == 0 ? 0 : $TargetDedicatedNodes) : {1});
    ", now, 4);
```

## <a name="next-steps"></a>Sonraki adımlar
* [Eşzamanlı düğüm görevleri ile Azure toplu işlem kaynak kullanımını en üst düzeye](batch-parallel-node-tasks.md) nasıl birden fazla görev aynı anda havuzunuzdaki hello işlem düğümlerinde yürütebilirsiniz hakkında ayrıntılar içerir. Ayrıca tooautoscaling, bu özellik toolower iş süresi paradan tasarruf bazı iş yükleri için yardımcı olabilir.
* Başka bir verimlilik güçlendirici toplu uygulama sorgularınızı hello en iyi yolu Batch hizmetindeki hello emin olun. Bkz: [hello Azure Batch hizmetinin verimli bir şekilde sorgu](batch-efficient-list-queries.md) toolearn toolimit hello nasıl hello hatta binlerce hello durumunu sorguladığınızda yayılan veri miktarını işlem düğümleri veya görevler.

[net_api]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch
[net_batchclient]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.batchclient
[net_cloudpool_autoscaleformula]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleformula
[net_cloudpool_autoscaleevalinterval]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleevaluationinterval
[net_enableautoscaleasync]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.enableautoscaleasync
[net_maxtasks]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.maxtaskspercomputenode
[net_poolops_resizepoolasync]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.resizepoolasync

[rest_api]: https://docs.microsoft.com/rest/api/batchservice/
[rest_autoscaleformula]: https://docs.microsoft.com/rest/api/batchservice/enable-automatic-scaling-on-a-pool
[rest_autoscaleinterval]: https://docs.microsoft.com/rest/api/batchservice/enable-automatic-scaling-on-a-pool
[rest_enableautoscale]: https://docs.microsoft.com/rest/api/batchservice/enable-automatic-scaling-on-a-pool
