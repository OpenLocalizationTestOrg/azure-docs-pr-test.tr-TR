---
title: "aaaDesigning Azure okuma erişimli coğrafi olarak yedekli depolama (RA-GRS) kullanarak yüksek oranda kullanılabilir uygulamalar | Microsoft Docs"
description: "Nasıl toouse Azure RA-GRS depolama tooarchitect esnek bir yüksek oranda kullanılabilir uygulama yeterli toohandle kesintileri."
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 8f040b0f-8926-4831-ac07-79f646f31926
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 1/19/2017
ms.author: robinsh
ms.openlocfilehash: e4a9fe7ef33eecd894408b3c1ef59920a248d1bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="designing-highly-available-applications-using-ra-grs"></a>Yüksek oranda kullanılabilir RA-GRS kullanarak uygulamalar tasarlama

Bir ortak bulut tabanlı altyapılar uygulamalarını barındırmak için yüksek oranda kullanılabilir bir platform sağlar özelliğidir. Bulut tabanlı uygulaması geliştiricileri düşünmeniz gerekir dikkatle nasıl tooleverage bu platform toodeliver yüksek oranda kullanılabilir uygulamalar tootheir kullanıcılar. Bu makalede özellikle nasıl geliştiriciler hello Azure depolama okuma erişimi coğrafi olarak yedekli depolama (RA-GRS) toomake kullanabilir üzerinde daha fazla kullanılabilir uygulamalarını odaklanır.

Artıklık – (yerel olarak yedekli depolama) LRS, ZRS (bölge olarak yedekli depolama), (coğrafi olarak yedekli depolama) GRS ve RA-GRS (coğrafi olarak yedekli depolamaya okuma erişimi) için dört seçeneğiniz vardır. Bu makalede toodiscuss GRS ve RA-GRS adımıdır. GRS ile verilerinizin üç kopyasını hello depolama hesabı oluştururken seçtiğiniz hello birincil bölge içinde tutulur. Üç ek kopya Azure tarafından belirtilen bir ikincil bölge içinde zaman uyumsuz olarak korunur. RA-grs okuma erişimi toohello ikincil kopya olması dışında aynı şeyi GRS hello. Merhaba farklı Azure Storage artıklık seçenekleri hakkında daha fazla bilgi için bkz: [Azure Storage çoğaltma](https://docs.microsoft.com/en-us/azure/storage/storage-redundancy). Merhaba çoğaltma makalede ayrıca hello birincil ve ikincil bölgeler hello eşleştirmelerini gösterilmektedir.

Bu makalede ve bağlantı tooa tam bir örnek, indirin ve çalıştırın hello sonunda bulunan kod parçacıkları vardır.

## <a name="key-features-of-ra-grs"></a>RA-GRS temel özellikleri

Biz hakkında konuşun önce toouse RA-GRS depolama özelliklerini ve davranışı hakkında şimdi konuşun.

* Azure depolama ikincil bir bölgede birincil bölgenizde hello verileri salt okunur bir kopyasını tutar; Yukarıda belirtildiği gibi hello depolama hizmeti hello ikincil bölge'hello konumunu belirler.

* Merhaba salt okunur kopyasıdır [sonuçta tutarlı](https://en.wikipedia.org/wiki/Eventual_consistency) hello birincil bölgede hello verilerle.

* BLOB'lar, tablolar ve Kuyruklar hello ikincil bölge için Sorgulayabileceğiniz bir *son eşitleme zamanı* hello son hello birincil toohello ikincil bölge Çoğaltmada gerçekleştiği belirten değer. (Bu RA-GRS artıklık şu anda yok Azure File storage için desteklenmiyor.)

* Merhaba birincil veya ikincil bölge içindeki hello verilerle hello depolama istemci kitaplığı toointeract kullanabilirsiniz. Ayrıca yönlendirebilirsiniz okuma istekleri otomatik olarak toohello ikincil bölge Okuma isteği toohello birincil bölge Zaman aşımına uğrarsa.

* Merhaba veri hello birincil bölgede hello erişilebilirliğini etkileyen önemli bir sorun varsa, hello Azure ekibi bir coğrafi hangi noktada toohello birincil bölge işaret eden hello DNS girişlerini değiştirilen toopoint toohello ikincil bölge olacaktır yük devretme, tetikleyebilir.

* Bir coğrafi yük devretme gerçekleşirse, Azure yeni bir ikincil konum seçin ve hello veri toothat konumu çoğaltmak ardından hello ikincil DNS girişlerini tooit gelin. Merhaba depolama hesabı çoğaltma tamamlanana kadar hello ikincil uç kullanılamaz. Daha fazla bilgi için lütfen bkz [bir Azure Storage kesinti oluşursa hangi toodo](https://docs.microsoft.com/en-us/azure/storage/storage-disaster-recovery-guidance).

## <a name="application-design-considerations-when-using-ra-grs"></a>RA-GRS kullanırken uygulama tasarım konuları

Merhaba ana amacı, bu makalenin tooshow olduğu, nasıl toodesign toofunction (bir sınırlı kapasite ile birlikte) daha büyük bir felaket hello birincil veri hello olayı içinde devam edecek bir uygulama Merkezi. Bunun için bir sorun olmasa tooread hello ikincil bölge ' geçiş yapma ve hello birincil bölge yeniden kullanılabilir olduğunda yeniden geçiş yapmayı sağlayarak uygulama toohandle geçici veya uzun süreli sorunları.

### <a name="using-eventually-consistent-data"></a>Sonuçta tutarlı verileri kullanma

Önerilen Bu çözüm, eski veri toohello çağrı yapan uygulamanın olabilir kesebilirsiniz tooreturn olduğunu varsayar. Merhaba ikincil veri sonuçta tutarlı olduğundan hello veri toohello birincil yazılmıştır, ancak hello güncelleştirme toohello ikincil hello birincil bölge erişilemez geçtiğinde, çoğaltma bitmedi mümkündür.

Örneğin, müşteriniz başarılı bir güncelleştirme gönderme, ve hello güncelleştirme yayılan toohello ikincil önce sonra hello birincil gidin. Bu durumda, Hello müşteri sonra geri tooread hello veri isterse, kendisinin güncelleştirilmiş hello veri yerine hello eski veri alır. Merhaba müşteri ileti nasıl bu kabul edilebilir ise ve bu durumda, karar vermeniz gerekir. Nasıl toocheck hello son eşitleme zamanı hello ikincil veriler üzerinde daha sonra bu makalede toosee hello ikincil güncel ise görürsünüz.

### <a name="handling-services-separately-or-all-together"></a>Ayrı ayrı veya hepsini bir araya Hizmetleri işleme

Merhaba diğer hizmetlerin hala tam olarak işlevsel durumdayken olası değil, ancak kullanılabilir bir hizmet toobecome için mümkündür. Tanıtıcı hello yeniden deneme ve salt okunur modda her biri için ayrı olarak hizmet verebilir (BLOB, kuyruklar, tablolar) ya da yeniden deneme tüm hello depolama hizmetleri için genel birlikte işleyebilir.

Örneğin, kuyruklar ve BLOB'lar uygulamanızda kullanırsanız, bunların her biri için ayrı kod toohandle yeniden denenebilir hataları tooput karar verebilirsiniz. Daha sonra bir yeniden deneme hello blob hizmetinden Al, ancak hello sıra hizmeti hala çalıştığından, yalnızca hello parçası blobları işlediği uygulamanızı etkilenir. Karar verirseniz toohandle tüm depolama hizmeti genel olarak yeniden dener ve çağrısı toohello blob hizmeti yeniden denenebilir hata döndürür ve istekleri tooboth hello blob hizmeti ve hello kuyruk hizmeti etkilenir.

Sonuç olarak, bu, uygulamanızın hello karmaşıklığına bağlıdır. Hizmeti tarafından toohandle hello hataları karar verebilirsiniz, ancak bunun yerine tooredirect okuma istekleri tüm depolama hizmetleri toohello ikincil bölge için herhangi bir depolama hizmeti ile ilgili bir sorun hello birincil bölgede algıladığınızda hello uygulamasını ve salt okunur modda çalıştırmak.

### <a name="other-considerations"></a>Diğer konular

Bunlar olan hello diğer noktalar, bu makalenin hello kalan aşağıdakiler ele alınacaktır.

*   Yeniden deneme, hello devre kesici desen kullanan okuma isteklerinin işlenmesi

*   Sonuçta tutarlı verileri ve hello son eşitleme zamanı

*   Test Etme

## <a name="running-your-application-in-read-only-mode"></a>Salt okunur modda da uygulamanızı çalıştırma

başarısız mümkün toohandle hem okuma isteklerinin olmalıdır ve güncelleştirme isteği başarısız oldu (Bu durumda ekler, güncelleştirmeleri ve silme işlemleri anlamına güncelleştirmesiyle) toouse RA-GRS depolama. Merhaba birincil veri merkezi başarısız olursa, okuma isteklerinin yeniden yönlendirilen toohello ikincil veri merkezi olabilir, ancak hello ikincil salt okunur olduğu için güncelleştirme isteklerinin olamaz. Bu nedenle, bazı yolu toorun salt okunur modda uygulamanız gerekir.

Örneğin, herhangi bir güncelleştirme istekleri toohello depolama hizmeti göndermeden önce denetlenecek bayrağı ayarlayabilirsiniz. Merhaba güncelleştirme isteklerinin birini geldiğinde, atlayın ve uygun yanıtı toohello müşteri döndürür. Hatta hello Sorun çözülene kadar bazı özellikler değerlerinin toodisable istediğiniz ve bu özellikleri geçici olarak kullanılamıyor kullanıcıları bilgilendirin.

Toohandle hataları her hizmet için ayrı ayrı karar verirseniz, hizmeti tarafından salt okunur modda uygulamanızda toohandle hello özelliği toorun de gerekir. Salt okunur bayrakları etkinleştirilebilir her hizmet için sahip olabilir ve devre dışı bırakılır ve tanıtıcı kodunuzda hello uygun yerlerde uygun bayrağı hello.

Salt okunur modda uygulamanızda başka bir yan avantajına sahiptir – size verir mümkün toorun olan hello özelliği tooensure ana uygulama yükseltme sırasında işlevleri sınırlıdır. Yükseltme yaparken hiç kimse hello hello birincil bölge verilere sağlama, uygulama toorun salt okunur mod ve noktası toohello ikincil veri merkezi içinde tetikleyebilir.

## <a name="handling-updates-when-running-in-read-only-mode"></a>Güncelleştirmeler salt okunur modda çalışırken işleme

Birçok yolu vardır toohandle güncelleştirme salt okunur modda çalışırken ister. Biz bu kapsamlı kapak olmaz ancak genellikle birkaç düşündüğünüz desenleri vardır.

1.  Tooyour kullanıcı yanıt ve şu anda güncelleştirmeleri kabul ettiğiniz değil söyleyin. Örneğin, bir kişi yönetim sistemi müşteriler tooaccess kişi bilgilerini etkinleştirme ancak güncelleştirmeleri olmamasını.

2.  Sıraya alma güncelleştirmelerinizi başka bir bölgede olabilir. Bu durumda, farklı bir bölgede bekleyen güncelleştirme istekleri tooa sıranız yazma ve hello birincil veri merkezi yeniden çevrimiçi olduktan sonra bu istekleri bir şekilde tooprocess olması. Bu senaryoda, istenen bu hello güncelleştirmeyi daha sonra işlenmek üzere sıraya bilmeniz hello müşteri izin vermemelisiniz.

3.  Başka bir bölgede tooa depolama hesabı güncelleştirmelerinizi yazabilirsiniz. Merhaba birincil veri merkezi tekrar çevrimiçi olduğunda, bu güncelleştirmeleri hello verilerin hello yapısını bağlı olarak hello birincil veri yolu toomerge sahip olabilir. Örneğin, bir tarih damgası hello adı ile ayrı dosyalar oluşturuyorsanız, bu dosyaları geri toohello birincil bölge kopyalayabilirsiniz. Bu günlüğe kaydetme ve IOT verileri gibi bazı iş yükleri için çalışır.

## <a name="handling-retries"></a>Yeniden deneme işleme

Bunu nasıl hangi hataları yeniden denenebilir bilmeniz? Bu hello depolama istemcisi kitaplığı tarafından belirlenir. Örneğin, onu yeniden deneniyor başarı de büyük olasılıkla tooresult olmadığından 404 hatası (kaynak bulunamadı) yeniden denenebilir değil. Merhaba diğer yandan, bir 500 sunucu hatası olduğundan ve yalnızca geçici bir sorun olabilir yeniden denenebilir hatasıdır. Daha fazla ayrıntı için hello denetleyin [açık kaynak kodu hello ExponentialRetry sınıfı için](https://github.com/Azure/azure-storage-net/blob/87b84b3d5ee884c7adc10e494e2c7060956515d0/Lib/Common/RetryPolicies/ExponentialRetry.cs) hello .NET depolama istemci Kitaplığı'nda. (Merhaba ShouldRetry yöntemi bakın.)

### <a name="read-requests"></a>Okuma isteği

Birincil depolama ile ilgili bir sorun varsa Okuma isteği yeniden yönlendirilen toosecondary depolama olabilir. İçinde yukarıda olarak belirtildiği [sonunda tutarlı verileri kullanarak](#using-eventually-consistent-data), uygulama toopotentially eski verileri okumak için kabul edilebilir olmalıdır. Merhaba depolama istemci kitaplığı tooaccess RA-GRS veri kullanıyorsanız, hello için bir değer ayarlayarak Okuma isteği hello yeniden deneme davranışını belirtebilirsiniz **LocationMode** hello aşağıdaki özellik tooone:

*   **PrimaryOnly** (Merhaba varsayılan)

*   **PrimaryThenSecondary**

*   **SecondaryOnly**

*   **SecondaryThenPrimary**

Merhaba ayarlandığında **LocationMode** çok**PrimaryThenSecondary**hello ilk okuyun, istek toohello birincil uç nokta yeniden denenebilir hatayla başarısız olursa, hello istemci otomatik olarak başka bir okuma yapar toohello ikincil uç isteyin. Ardından sunucu zaman aşımı Hello hata olması durumunda hello hizmetinden yeniden denenebilir hata almadan önce hello istemci hello zaman aşımı tooexpire toowait gerekir.

Alırken temelde iki senaryo tooconsider karar verirken nasıl toorespond tooa yeniden denenebilir hata:

*   Bu yalıtılmış bir sorundur ve sonraki istekleri toohello birincil uç nokta yeniden denenebilir hata döndürmez. Geçici ağ hatası olduğunda, bu durum oluşabilir bir örnektir.

    Bu senaryoda, yoktur önemli performansta düşme olmaz elde etmeyle **LocationMode** çok ayarlamak**PrimaryThenSecondary** yalnızca seyrek böyle gibi.

*   Bu hello depolama hizmetleri hello birincil bölge içinde en az biri ile ilgili bir sorun olduğunu ve sonraki istekleri toothat hello birincil bölge alt hizmetinde büyük olasılıkla tooreturn yeniden denenebilir hata bir süre. Bu hello birincil bölge tamamen erişilemez örneğidir.

    Bu senaryoda, bulunmaktadır performans tüm okuma istekleri hello birincil endpoint ilk deneyin, hello zaman aşımı tooexpire için bekleyin ve ardından toohello ikincil uç geçiş için.

Bu senaryolarda, bunları olmadığını hello birincil uç noktası ile devam eden bir sorundur ve tüm okuma isteklerinin ayarlayarak toohello ikincil uç noktaya hello doğrudan göndermek tanımlamanız gerekir **LocationMode** özelliği çok **SecondaryOnly**. Şu anda salt okunur modda hello uygulama toorun aynı zamanda değiştirmeniz gerekir. Bu yaklaşım hello adlandırılıyor [devre kesici düzeni](https://msdn.microsoft.com/library/dn589784.aspx).

### <a name="update-requests"></a>Güncelleştirme isteği

Merhaba devre kesici düzeni uygulanan tooupdate istekleri de olabilir. Ancak, güncelleştirme isteklerinin salt okunur yeniden yönlendirilen toosecondary depolama olamaz. Bu istekler için hello bırakmanız **LocationMode** çok ayarlanan özelliği**PrimaryOnly** (Merhaba varsayılan). toohandle bu hataları – bir satırda – 10 hataları gibi bir ölçüm toothese istekleri geçerli ve salt okunur modda hello uygulamasına, eşiğine ulaşıldığında geçiş yapabilirsiniz. Kullanabileceğiniz hello olanlar hello devre kesici desen hakkında hello sonraki bölümde, aşağıda açıklandığı şekilde tooupdate modu döndürmek için aynı yöntemleri.

## <a name="circuit-breaker-pattern"></a>Devre kesici düzeni

Uygulamanızda Hello devre kesici desenini kullanarak büyük olasılıkla toofail art arda olduğundan bir işlem yeniden deneniyor engelleyebilir. Merhaba işlem katlanarak yeniden sırada zaman ayırdığınız yerine hello uygulama toocontinue toorun sağlar. Merhaba hataya sabit zaman zaman Merhaba uygulaması hello işlemi yeniden deneyebilirsiniz de algılar.

### <a name="how-tooimplement-hello-circuit-breaker-pattern"></a>Nasıl tooimplement hello devre kesici düzeni

tooidentify birincil uç noktası ile devam eden bir sorun olduğunu, ne sıklıkta hello istemci yeniden denenebilir hatayla karşılaştığında izleyebilirsiniz. Her durumda farklı olduğundan, toodecide sahip hello eşik üzerinde toouse hello karar tooswitch toohello ikincil uç noktası için istediğiniz ve salt okunur modda hello uygulamayı çalıştırın. Örneğin, bir satırda hiçbir başarı ile 10 hata varsa tooperform hello anahtar karar. % 90'hello istekleri 2 dakikalık bir dönemde başarısız olursa bir başka örnek tooswitch ' dir.

Merhaba ilk senaryo için yalnızca hello başarısızlık sayısı tutabilir ve varsa en fazla, ayarlanmış hello sayısı geri toozero hello ulaşmadan önce başarılı. Merhaba ikinci senaryo için toouse olan tek yönlü tooimplement hello MemoryCache nesnesinde (.NET). Her istek için bir CacheItem toohello önbellek ekleyin, hello değeri toosuccess (1) ayarlayın veya (0) başarısız ve hello sona erme saati too2 dakika şimdi (veya ne olursa olsun, zaman sınırlaması) ayarlayın. Bir girdi sona erme süresine ulaşıldığında hello girişi otomatik olarak kaldırılır. Bu bir çalışırken 2 dakikalık penceresi verir. Bir istek toohello depolama hizmeti yaptığınızda, ilk LINQ sorgusu hello MemoryCache nesnesi toocalculate hello yüzde başarı arasında hello değerlerin toplamını ve hello sayısına göre bölme kullanın. Merhaba yüzde başarı (örneğin, % 10) bazı eşiğin altına düştüğünde hello ayarlamak **LocationMode** özelliği için okuma isteklerinin çok**SecondaryOnly** ve salt okunur modda önce hello uygulamasına geçiş devam ediliyor.

Merhaba eşik hataların yapılandırılabilir parametreler yapmadan dikkate almanız gereken şekilde toomake hello anahtar hizmet tooservice, uygulamanızda gelen değişebilir toodetermine kullanılır. Ayrıca her hizmetinde yeniden denenebilir hatayla toohandle ayrı ayrı karar veya olarak, daha önce bahsedildiği gibi budur.

Başka bir husustur nasıl toohandle bir uygulama birden çok örneğini ve her örnek yeniden denenebilir hata algıladığınızda hangi toodo. Örneğin, aynı uygulama yüklenen hello ile çalışan 20 VM'ye sahip. Her örneği ayrı ayrı işlemek? Yolu bir örneği bir sorun olduğunda sorunlarınız bir örneğini başlatır, bu bir örnek toolimit hello yanıt toojust istiyor musunuz veya tootry toohave istiyorsunuz tüm örneklerini hello aynı yanıt? Merhaba örnekleri ayrı olarak işleme toocoordinate hello yanıt arasında gezinmek çalışırken daha çok daha kolaydır, ancak bunu nasıl yapacağınız uygulamanızın mimarisine bağlıdır.

### <a name="options-for-monitoring-hello-error-frequency"></a>Merhaba hata sıklığı izleme seçenekleri

Tooswitch toohello ikincil bölge ve değişiklik üzerinden hello olduğunda uygulama toorun salt okunur modda yeniden deneme sırasını toodetermine içinde hello birincil bölgede hello sıklığını izleme için üç ana seçeneğiniz vardır.

*   Hello için bir işleyici ekleyin [ **yeniden deneniyor** ](http://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.operationcontext.retrying.aspx) hello olayda [ **OperationContext** ](http://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.operationcontext.aspx) tooyour depolama isteklerini iletmek – hello budur nesnesi yöntemi bu makalede gösterilen ve örnek eşlik hello kullanılır. Merhaba istemcinin bir isteği yeniden deneme zaman bu olayları yangın, tootrack ne sıklıkta etkinleştirme hello istemci birincil bir uç noktada yeniden denenebilir hatayla karşılaştığında.

    ```csharp 
    operationContext.Retrying += (sender, arguments) =>
    {
        // Retrying in hello primary region
        if (arguments.Request.Host == primaryhostname)
            ...
    };
    ```

*   Merhaba, [ **değerlendir** ](http://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.retrypolicies.iextendedretrypolicy.evaluate.aspx) yöntemi bir özel yeniden deneme İlkesi'nde çalıştırabilirsiniz özel kod her bir yeniden deneme gerçekleşir. Yeniden deneme olduğunda, bu da, yeniden deneme davranışı fırsat toomodify hello verir toplama toorecording içinde.

    ```csharp 
    public RetryInfo Evaluate(RetryContext retryContext,
    OperationContext operationContext)
    {
        var statusCode = retryContext.LastRequestResult.HttpStatusCode;
        if (retryContext.CurrentRetryCount >= this.maximumAttempts
        || ((statusCode &gt;= 300 && statusCode &lt; 500 && statusCode != 408)
        || statusCode == 501 // Not Implemented
        || statusCode == 505 // Version Not Supported
            ))
        {
        // Do not retry
            return null;
        }

        // Monitor retries in hello primary location
        ...

        // Determine RetryInterval and TargetLocation
        RetryInfo info =
            CreateRetryInfo(retryContext.CurrentRetryCount);

        return info;
    }
    ```

*   Merhaba üçüncü tooimplement kukla ile birincil storage uç noktanız sürekli olarak ping uygulamanızda özel bir izleme bileşeni yaklaşımdır, sistem durumunu (örneğin, küçük bir blob okuma) istekleri toodetermine okuyun. Bu, bazı kaynaklar ancak önemli ölçüde kalırsınız. Eşiğe ulaştığında bir sorun algılandığında, ardından hello anahtar çok gerçekleştireceği**SecondaryOnly** ve salt okunur modda.

Belirli bir noktada tooswitch geri toousing hello birincil uç noktası ve güncelleştirmelere izin isteyeceksiniz. Yukarıda listelenen hello ilk iki yöntemden birini kullanıyorsanız, yalnızca geri toohello birincil endpoint geçin ve rasgele seçilen bir zaman miktarı veya işlemlerinin sayısı gerçekleştirildikten sonra güncelleştirme modunu etkinleştirmek. Ardından, hello yeniden deneme mantığı yeniden Git izin verebilirsiniz. Merhaba sorunun giderilmiş, toouse hello birincil endpoint devam ve güncelleştirmelere izin verecek. Hala bir sorun varsa, bu kez daha geri toohello ikincil uç noktası ve salt okunur modda ayarlamış hello ölçütleri başarısız sonra geçiş yapar.

Ping hello birincil depolama endpoint yeniden, başarılı olduğunda hello üçüncü senaryo için geri hello anahtar çok tetikleyebilir**PrimaryOnly** ve güncelleştirmelere izin devam edin.

## <a name="handling-eventually-consistent-data"></a>Sonuçta tutarlı verileri işleme

RA-GRS hello birincil toohello ikincil bölge ' işlemleri yineleyerek çalışır. Bu çoğaltma işlemi hello ikincil bölge'hello verilerde olduğunu garanti *sonuçta tutarlı*. Merhaba ikincil bölge'de aynı olarak sipariş hello içinde bu hello birincil bölge içinde tüm hello işlemleri sonunda hello ikincil bölge'de görünür, ancak olabileceğini bir gecikme göründükleri önce anlamına gelir ve hello işlemleri garantisi yoktur gelmesini Bunlar ilk olarak hello birincil bölgede uygulandı. İşlemlerinizi sırasıyla dışında hello ikincil bölgede ulaşırsa, *olabilir* hello hizmet arayı kapatıncaya kadar verilerinizi hello ikincil bölge toobe tutarsız bir durumda göz önünde bulundurun.

Merhaba aşağıdaki tabloda gösterilmektedir çalışan toomake hello ayrıntılarını güncelleştirdiğinizde ne gerçekleşebilir örneği her hello üyesi *Yöneticiler* rol. Bu örnek Hello artırmak amacıyla için bu hello güncelleştirmenin gerektirdiği **çalışan** varlık ve güncelleştirme bir **Yönetici rolü** Yöneticiler toplam sayısı hello sayısı olan varlık. Nasıl hello güncelleştirmeleri bozuk hello ikincil bölge'de uygulandığını dikkat edin.

| **Saat** | **İşlem**                                            | **Çoğaltma**                       | **Son eşitleme zamanı** | **Sonuç** |
|----------|------------------------------------------------------------|---------------------------------------|--------------------|------------| 
| T0       | İşlem A: <br> Çalışanı Ekle <br> birincil varlık |                                   |                    | İşlem A tooprimary eklenen<br> henüz çoğaltılmamış. |
| T1       |                                                            | İşlem A <br> Çoğaltılan<br> İkincil | T1 | İşlem A toosecondary çoğaltılan. <br>Son eşitleme zamanı güncelleştirildi.    |
| T2       | İşlem B:<br>Güncelleştirme<br> çalışan varlık<br> birincil  |                                | T1                 | İşlem tooprimary yazılmış B,<br> henüz çoğaltılmamış.  |
| T3       | İşlem C:<br> Güncelleştirme <br>Yönetici<br>Rol varlığı<br>birincil |                    | T1                 | İşlem tooprimary yazılmış C,<br> henüz çoğaltılmamış.  |
| *T4*     |                                                       | İşlem C <br>Çoğaltılan<br> İkincil | T1         | İşlem C toosecondary çoğaltılan.<br>Olduğundan güncelleştirilmedi LastSyncTime <br>işlem B henüz çoğaltılmamış.|
| *T5*     | Varlıkların okuma <br>İkincil                           |                                  | T1                 | Çalışanın hello eski değer alma <br> Varlık işlem B kurmadı çünkü <br> henüz çoğaltılan. Merhaba yeni değerini alın<br> Yönetici rolü varlığı C olduğundan<br> Çoğaltılan. Son eşitleme zamanı hala tamamlanmamış<br> Silinmiş olduğundan güncelleştirilmiş işlem B<br> Çoğaltılan kurmadı. Size söyleyebilir<br>Yönetici rolü varlığı tutarsız. <br>Merhaba varlık tarih/saat sonra olduğundan <br>Merhaba son eşitleme zamanı. |
| *T6*     |                                                      | İşlem B<br> Çoğaltılan<br> İkincil | T6                 | *T6* – C aracılığıyla tüm işlemlerin <br>edilmiş çoğaltılan, son eşitleme zamanı<br> güncelleştirilir. |

Bu örnekte, hello istemci anahtarları tooreading T5 hello ikincil bölge'den varsayalım. Başarılı bir şekilde hello okuyabilirsiniz **Yönetici rolü** varlık şu anda, ancak hello varlık hello hello sayısı ile tutarlı değil yöneticiler sayısı için bir değer içeriyorsa **çalışan** varlıklar Yöneticiler hello ikincil bölge, şu anda işaretlenmedi. İstemci yalnızca bu değerle tutarsız bilgiler olduğunu hello risk görüntüleyebilirsiniz. Alternatif olarak, hello istemci toodetermine bu hello çalışabilir **Yönetici rolü** hello güncelleştirmeleri sıralama dışında gerçekleşen ve sonra bu olayının hello kullanıcı bildirmeniz büyük olasılıkla tutarsız bir durumda olduğundan.

toorecognize, büyük olasılıkla tutarsız veriler içerdiğinden emin hello istemci hello hello değerini kullanabilir *son eşitleme zamanı* herhangi bir anda bir depolama birimi hizmeti sorgulayarak alabilirsiniz. Bu size bildirir hello zaman zaman hello ikincil bölge'hello verileri son tutarlı ve hello hizmet uygulandığında tüm işlemleri önceki toothat noktası zamanında hello. Merhaba hizmet hello ekledikten sonra yukarıda gösterilen hello örnekte **çalışan** hello ikincil bölge varlıkta hello son eşitleme Zamanı ayarlanmış çok*T1*. Kalır *T1* hello hello hizmet güncelleştirmeleri kadar **çalışan** çok olarak ayarlandığında hello ikincil bölge varlık*T6*. Merhaba istemci hello hello varlıkta, okur, son eşitleme zamanı alır, *T5*, onu hello varlıkta hello damgasıyla karşılaştırabilirsiniz. Merhaba varlık Hello zaman damgasını hello sonraki zaman, son eşitleme sonra hello varlık büyük olasılıkla tutarsız bir durumda olur ve ne olursa olsun, uygulamanız için hello uygun eylemi gerçekleştirin. Bu alanı kullanarak hello son güncelleştirme toohello birincil tamamlandığı bilmeniz gerekir.

## <a name="testing"></a>Test Etme

Bu, uygulamanızın yeniden denenebilir hatalarla karşılaştığında beklendiği gibi davranır önemli tootest olur. Örneğin, uygulama anahtarları toohello ikincil hello tootest gerekir ve salt okunur moduna bir sorun algılar ve anahtarlar geri zaman hello birincil bölge yeniden kullanılabilir duruma gelir. toodo Bu, ne sıklıkta ortaya denetlemek ve bir şekilde toosimulate yeniden denenebilir hata gerekir.

Kullanabileceğiniz [Fiddler](http://www.telerik.com/fiddler) toointercept ve HTTP yanıtını bir betik içinde değiştirin. Bu komut dosyasını birincil uç noktasından gelen yanıtları tanımlamak ve depolama istemci kitaplığı yeniden denenebilir hata olarak tanır bu hello hello HTTP durum kodu tooone değiştirin. Bu kod parçacığını hello yanıtları tooread isteklerini karşılar Fiddler komut basit bir örnek gösterilmektedir **employeedata** tablo tooreturn 502 durumu:

```java
static function OnBeforeResponse(oSession: Session) {
    ...
    if ((oSession.hostname == "\[yourstorageaccount\].table.core.windows.net")
      && (oSession.PathAndQuery.StartsWith("/employeedata?$filter"))) {
        oSession.responseCode = 502;
    }
}
```

Bu örnek toointercept istekleri daha geniş ölçüdeki genişletmek ve yalnızca hello değiştirme **yanıt kodu** bazı bunları toobetter benzetimini gerçek dünya senaryoları. Fiddler betikleri özelleştirme hakkında daha fazla bilgi için bkz: [bir istek veya yanıt değiştirme](http://docs.telerik.com/fiddler/KnowledgeBase/FiddlerScript/ModifyRequestOrResponse) hello Fiddler belge içinde.

Hello eşikleri, uygulama yalnızca tooread modu yapılandırılabilir geçiş yaptıysanız, üretim dışı işlem birimleri ile daha kolay tootest hello davranış olacaktır.

## <a name="next-steps"></a>Sonraki Adımlar

* Merhaba LastSyncTime nasıl ayarlanır, başka bir örnek de dahil olmak üzere ilgili okuma erişimi coğrafi Yedeklilik daha fazla bilgi için lütfen bkz [Windows Azure Depolama artıklık seçenekleri ve okuma erişimli coğrafi olarak yedekli depolama](https://blogs.msdn.microsoft.com/windowsazurestorage/2013/12/11/windows-azure-storage-redundancy-options-and-read-access-geo-redundant-storage/).

* Lütfen nasıl toomake hello geri ve İleri hello birincil ve ikincil uç noktaları arasında geçiş gösteren tam bir örnek için bkz: [Azure kullanan örnekler – hello devre kesici düzeni RA-GRS depolama ile](https://github.com/Azure-Samples/storage-dotnet-circuit-breaker-pattern-ha-apps-using-ra-grs).
